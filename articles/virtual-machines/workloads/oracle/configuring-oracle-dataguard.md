---
title: Oracle Data Guard Azure Linux VM'de uygulamak | Microsoft Docs
description: "Hızla bir Oracle Data Guard yukarı ve Azure ortamınızda çalışan alın."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: v-shiuma
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: rclaus
ms.openlocfilehash: fe8b635936c74c5154ec83d34160b9aae61c45e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="implement-oracle-data-guard-on-azure-linux-vm"></a>Azure Linux VM'de Oracle veri koruma uygulama 

Azure CLI, komut satırından veya betik içindeki Azure kaynaklarını oluşturmak ve yönetmek için kullanılır. Bir Oracle Market galeri görüntüsü 12 C'den veritabanı dağıtmak için Azure CLI kullanarak bu kılavuzu ayrıntıları. Oracle veritabanı oluşturulduktan sonra bu belgede, adım adım yükleme ve veri koruma Azure VM yapılandırma gösterilmektedir.

Başlamadan önce Azure CLI’nin yüklü olduğundan emin olun. Daha fazla bilgi için bkz. [Azure CLI yükleme kılavuzu](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="prepare-the-environment"></a>Ortamı hazırlama
### <a name="assumptions"></a>Varsayımlar

Oracle Data Guard yüklemeyi gerçekleştirmek için aynı kullanılabilirlik kümesinde iki Azure sanal makineleri oluşturmanız gerekir. Sanal makineleri oluşturmak için kullandığınız Market görüntü "Oracle: Oracle-veritabanı-Ee:12.1.0.2:latest".

Birincil VM (myVM1) çalışan bir Oracle örneği vardır.

Bekleme yalnızca yüklü olan Oracle yazılım VM (myVM2) sahiptir.

### <a name="log-in-to-azure"></a>Azure'da oturum açma 

[az login](/cli/azure/#login) komutuyla Azure aboneliğinizde oturum açın ve ekrandaki yönergeleri izleyin.

```azurecli
az login
```

### <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

[az group create](/cli/azure/group#create) komutuyla bir kaynak grubu oluşturun. Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır. 

Aşağıdaki örnek `westus` konumunda `myResourceGroup` adlı bir kaynak grubu oluşturur.

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-availability-set"></a>Kullanılabilirlik kümesi oluşturma

Bu adım isteğe bağlıdır ancak önerilir. bkz: [Azure kullanılabilirlik kümeleri Kılavuzu](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines) daha fazla bilgi için.

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-virtual-machine"></a>Sanal makine oluşturma

[az vm create](/cli/azure/vm#create) komutuyla bir sanal makine oluşturun. 

Aşağıdaki örnek, 2 VM adlı oluşturur `myVM1` ve `myVM2`. Zaten bir varsayılan anahtar konumda yoksa, SSH anahtarları oluşturur. Belirli bir anahtar kümesini kullanmak için `--ssh-key-value` seçeneğini kullanın.

MyVM1 (birincil) oluşturma
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --admin-username azureuser \
     --generate-ssh-keys \
```

VM oluşturulduktan sonra Azure CLI bilgileri aşağıdaki örneğe benzer şekilde gösterir: Al Not `publicIpAddress`. Bu adres, VM’ye erişmek için kullanılır.

```azurecli
{
  "fqdns": "",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "westus",
  "macAddress": "00-0D-3A-36-2F-56",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.64.104.241",
  "resourceGroup": "myResourceGroup"
}
```

MyVM2 oluşturun (bekleme)
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --admin-username azureuser \
     --generate-ssh-keys \
```

Not edin `publicIpAddress` oluşturulduktan sonra da.

### <a name="open-the-tcp-port-for-connectivity"></a>Bağlantı için TCP bağlantı noktasını açın

Adım Oracle DB uzaktan erişim sağlayan dış uç noktalar yapılandırmak için aşağıdaki komutu yürütün.

MyVM1 için açık bağlantı noktası

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVmN1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

Sonuç aşağıdaki yanıta benzer görünmelidir:

```bash
{
  "access": "Allow",
  "description": null,
  "destinationAddressPrefix": "*",
  "destinationPortRange": "1521",
  "direction": "Inbound",
  "etag": "W/\"bd77dcae-e5fd-4bd6-a632-26045b646414\"",
  "id": "/subscriptions/<subscription-id>/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkSecurityGroups/myVmNSG/securityRules/allow-oracle",
  "name": "allow-oracle",
  "priority": 999,
  "protocol": "Tcp",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sourceAddressPrefix": "*",
  "sourcePortRange": "*"
}
```

MyVM2 için açık bağlantı noktası

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2N1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-to-virtual-machine"></a>Sanal makineye bağlanma

Sanal makine ile bir SSH oturumu oluşturmak için aşağıdaki komutu kullanın. IP adresini, sanal makinenizin `publicIpAddress` ile değiştirin.

```bash 
ssh azureuser@<publicIpAddress>
```

### <a name="create-database-on-myvm1-primary"></a>MyVM1 üzerinde veritabanı oluşturma (birincil)

Veritabanını yüklemek için sonraki adım olacak şekilde Oracle yazılım Market görüntüsü üzerinde zaten yüklü. İlk adım, 'oracle' süper kullanıcı çalışıyor.

```bash
sudo su - oracle
```

Veritabanı oluştur:

```bash
$ dbca -silent \
   -createDatabase \
   -templateName General_Purpose.dbc \
   -gdbname cdb1 \
   -sid cdb1 \
   -responseFile NO_VALUE \
   -characterSet AL32UTF8 \
   -sysPassword OraPasswd1 \
   -systemPassword OraPasswd1 \
   -createAsContainerDatabase true \
   -numberOfPDBs 1 \
   -pdbName pdb1 \
   -pdbAdminPassword OraPasswd1 \
   -databaseType MULTIPURPOSE \
   -automaticMemoryManagement false \
   -storageType FS \
   -ignorePreReqs
```
Çıktı aşağıdaki yanıta benzer görünmelidir:

```bash
Copying database files
1% complete
2% complete
8% complete
13% complete
19% complete
27% complete
Creating and starting Oracle instance
29% complete
32% complete
33% complete
34% complete
38% complete
42% complete
43% complete
45% complete
Completing Database Creation
48% complete
51% complete
53% complete
62% complete
70% complete
72% complete
Creating Pluggable Databases
78% complete
100% complete
Look at the log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for further details.
```

ORACLE_SID ve ORACLE_HOME değişkenlerini ayarlama

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

Böylece bu ayarlar sonraki oturumlar için kaydedilir isteğe bağlı olarak, eklenen ORACLE_HOME ve ORACLE_SID .bashrc dosyasına kullanabilirsiniz.

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="data-guard-configurations"></a>Veri koruma yapılandırmaları

### <a name="enable-archive-log-mode-on-myvm1-primary"></a>MyVM1 (birincil) arşiv günlük modunu etkinleştir

```bash
$ sqlplus / as sysdba
SQL> SELECT log_mode FROM v$database;

LOG_MODE
------------
NOARCHIVELOG

SQL> SHUTDOWN IMMEDIATE;
SQL> STARTUP MOUNT;
SQL> ALTER DATABASE ARCHIVELOG;
SQL> ALTER DATABASE OPEN;
```
Zorla günlüğe yazılmasını etkinleştirmek ve en az bir günlük dosyası bulunduğundan emin olun.

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

Bekleme Yinele günlükleri oluşturma

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

(Hangi kurtarma çok daha önce yaptığınız) Flashback açmak ve otomatik olarak STANDBY_FILE_MANAGEMENT ayarlayın

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
```

### <a name="service-setup-on-myvm1-primary"></a>MyVM1 (birincil) üzerinde hizmeti Kurulumu

Düzenleme veya $ORACLE_HOME\network\admin klasörünün bulunduğu tnsnames.ora dosyası oluşturma

Aşağıdaki girdileri ekleyin

```bash
cdb1 =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )

cdb1_stby =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )
```

Düzenleme veya $ORACLE_HOME\network\admin klasörünün bulunduğu listener.ora dosya oluşturma

Aşağıdaki girdileri ekleyin

```bash
LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )

SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (GLOBAL_DBNAME = cdb1_DGMGRL)
      (ORACLE_HOME = /u01/app/oracle/product/12.1.0/dbhome_1)
      (SID_NAME = cdb1)
    )
  )

ADR_BASE_LISTENER = /u01/app/oracle
```

Dinleyici Başlat

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="service-setup-on-myvm2-standby"></a>Hizmeti Kurulumu myVM2 üzerinde (bekleme)

Düzenleme veya $ORACLE_HOME\network\admin klasörünün bulunduğu tnsnames.ora dosyası oluşturma

Aşağıdaki girdileri ekleyin

```bash
cdb1 =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM1)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )

cdb1_stby =
  (DESCRIPTION =
    (ADDRESS_LIST =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
    )
    (CONNECT_DATA =
      (SID = cdb1)
    )
  )
```

Düzenleme veya $ORACLE_HOME\network\admin klasörünün bulunduğu listener.ora dosya oluşturma

Aşağıdaki girdileri ekleyin

```bash
LISTENER =
  (DESCRIPTION_LIST =
    (DESCRIPTION =
      (ADDRESS = (PROTOCOL = TCP)(HOST = myVM2)(PORT = 1521))
      (ADDRESS = (PROTOCOL = IPC)(KEY = EXTPROC1521))
    )
  )

SID_LIST_LISTENER =
  (SID_LIST =
    (SID_DESC =
      (GLOBAL_DBNAME = cdb1_DGMGRL)
      (ORACLE_HOME = /u01/app/oracle/product/12.1.0/dbhome_1)
      (SID_NAME = cdb1)
    )
  )

ADR_BASE_LISTENER = /u01/app/oracle
```

Dinleyici Başlat

```bash
$ lsnrctl stop
$ lsnrctl start
```

Veri koruma Aracısı'nı etkinleştirin
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="restore-database-to-myvm2-standby"></a>Veritabanını geri yüklemek için myVM2 (bekleme)

Bir parametre dosyası oluştur ' / tmp/initcdb1_stby.ora' aşağıdakilere içeriğiyle
```bash
*.db_name='cdb1'
```

Klasör Oluştur

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

Parola dosyası oluşturma

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0.2/db_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
Veritabanı myVM2 üzerinde Başlat

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

RMAN yardımcı programını kullanarak veritabanını geri yükleyin

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

İçinde RMAN aşağıdaki komutları yürütün
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

Veri koruma Aracısı'nı etkinleştirin
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a>Veri koruma Aracısı'nı (birincil) myVM1 yapılandırma

SYS ve parola (OS kimlik doğrulaması kullanmayan yapın) kullanarak oturum açın ve veri koruma Yöneticisi'ni başlatın. Aşağıdakileri gerçekleştirin

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome to DGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> CREATE CONFIGURATION my_dg_config AS PRIMARY DATABASE IS cdb1 CONNECT IDENTIFIER IS cdb1;
Configuration "my_dg_config" created with primary database "cdb1"
DGMGRL> ADD DATABASE cdb1_stby AS CONNECT IDENTIFIER IS cdb1_stby MAINTAINED AS PHYSICAL;
Database "cdb1_stby" added
DGMGRL> ENABLE CONFIGURATION;
Enabled.
```

Yapılandırmasını gözden geçirin.
```bash
DGMGRL> SHOW CONFIGURATION;

Configuration - my_dg_config

  Protection Mode: MaxPerformance
  Members:
  cdb1      - Primary database
    cdb1_stby - Physical standby database

Fast-Start Failover: DISABLED

Configuration Status:
SUCCESS   (status updated 26 seconds ago)
```

Bu, Oracle Data Guard Kurulum tamamlandı. Sonraki bölümde bağlantısı ve geçişi test etme gösterilir

### <a name="connect-database-from-client-machine"></a>İstemci makineden veritabanına bağlanın

Güncelleştirme veya genellikle $ORACLE_HOME\network\admin bulunur, istemci makinenizde tnsnames.ora dosyası oluşturun.

IP ile değiştirmek, `publicIpAddress` myVM1 ve myVM2 için

```bash
cdb1=
  (DESCRIPTION=
    (ADDRESS=
      (PROTOCOL=TCP)
      (HOST=<myVM1 IP address>)
      (PORT=1521)
    )
    (CONNECT_DATA=
      (SERVER=dedicated)
      (SERVICE_NAME=cdb1)
    )
  )

cdb1_stby=
  (DESCRIPTION=
    (ADDRESS=
      (PROTOCOL=TCP)
      (HOST=<myVM2 IP address>)
      (PORT=1521)
    )
    (CONNECT_DATA=
      (SERVER=dedicated)
      (SERVICE_NAME=cdb1_stby)
    )
  )
```

Sqlplus Başlat

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-data-guard-configuration"></a>Test veri koruma yapılandırması

### <a name="database-switchover-on-myvm1-primary"></a>Veritabanı geçiş myVM1 (birincil) üzerinde

Birincil bekleme moduna geçmek için (cdb1 cdb1_stby için)

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome to DGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER TO cdb1_stby;
Performing switchover NOW, please wait...
Operation requires a connection to instance "cdb1" on database "cdb1_stby"
Connecting to instance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1_stby" is opening...
Operation requires start up of instance "cdb1" on database "cdb1"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1_stby"
DGMGRL>
```

Artık bekleme veritabanına bağlanabilmek için olması gerekir

Sqlplus Başlat

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="database-switch-back-on-myvm2-standby"></a>Veritabanı anahtarda geri myVM2 (bekleme)

Geri geçiş yapmak için aşağıdakilere myVM2 üzerinde çalıştırın
```bash
$ dgmgrl sys/OraPasswd1@cdb1_stby
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome to DGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER TO cdb1;
Performing switchover NOW, please wait...
Operation requires a connection to instance "cdb1" on database "cdb1"
Connecting to instance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1" is opening...
Operation requires start up of instance "cdb1" on database "cdb1_stby"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1"
```

Bir kez daha, şimdi birincil veritabanına bağlanabilmek için olmanız gerekir

Sqlplus Başlat

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With the Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

Bu, yükleme ve veri koruma yapılandırmasını Oracle linux üzerinde tamamlandı.


## <a name="delete-virtual-machine"></a>Sanal makineyi silme

Kaynak Grubu, VM ve tüm ilgili kaynaklar artık gerekli olmadığında aşağıdaki komut kullanılarak kaldırılabilir.

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Sonraki adımlar

[Yüksek oranda kullanılabilir sanal makine oluşturma öğreticisi](../../linux/create-cli-complete.md)

[VM dağıtımı CLI örneklerini keşfedin](../../linux/cli-samples.md)
