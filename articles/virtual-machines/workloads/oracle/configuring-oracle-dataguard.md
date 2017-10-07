---
title: aaaImplement Oracle Data Guard Azure Linux VM'de | Microsoft Docs
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
ms.openlocfilehash: 101196b2f50dfca64d3eb1b4be56ff0c108693e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-data-guard-on-azure-linux-vm"></a>Azure Linux VM'de Oracle veri koruma uygulama 

Hello Azure CLI kullanılan toocreate olan ve hello komut satırından veya komut dosyalarında Azure kaynaklarını yönetin. Hello Azure CLI toodeploy bir Oracle hello Market galeri görüntüsü 12 C'den veritabanı kullanarak bu kılavuzu ayrıntıları. Merhaba Oracle veritabanı oluşturulduktan sonra bu belgede, gösterir adım adım nasıl tooinstall ve veri koruma Azure VM yapılandırabilirsiniz.

Başlamadan önce Azure CLI yüklenmiş bu hello emin olun. Daha fazla bilgi için bkz. [Azure CLI yükleme kılavuzu](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="prepare-hello-environment"></a>Merhaba ortamını hazırlayın
### <a name="assumptions"></a>Varsayımlar

tooperform hello, Oracle Data Guard yüklemek ihtiyacınız hello toocreate iki Azure sanal makineler aynı kullanılabilirlik kümesi. Merhaba Market görüntü toocreate hello VM'ler kullandığınız "Oracle: Oracle-veritabanı-Ee:12.1.0.2:latest".

Merhaba birincil VM (myVM1) çalışan bir Oracle örneği vardır.

Merhaba hello Oracle yazılımı yalnızca yüklü bekleme VM (myVM2) sahip.

### <a name="log-in-tooazure"></a>İçinde tooAzure oturum 

Tooyour hello Azure aboneliğiyle oturum [az oturum açma](/cli/azure/#login) komut ve hello ekrandaki yönergeleri izleyin.

```azurecli
az login
```

### <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu. Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır. 

Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myResourceGroup` hello içinde `westus` konumu.

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

Bir VM ile Merhaba oluşturma [az vm oluşturma](/cli/azure/vm#create) komutu. 

Merhaba aşağıdaki örnek adlı 2 VM'ler oluşturur `myVM1` ve `myVM2`. Zaten bir varsayılan anahtar konumda yoksa, SSH anahtarları oluşturur. toouse belirli bir ayarla anahtarları, hello kullan `--ssh-key-value` seçeneği.

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

VM oluşturulan hello, bir örnek aşağıdaki bilgileri benzer toohello hello Azure CLI kez gösterir: hello Al Not `publicIpAddress`. Kullanılan tooaccess hello VM adresidir.

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

Merhaba not edin `publicIpAddress` oluşturulduktan sonra da.

### <a name="open-hello-tcp-port-for-connectivity"></a>Bağlantı için Hello TCP bağlantı noktasını açın

Hello adım tooconfigure dış uç noktalar, Oracle DB hello uzaktan erişmesini sağlayan, hello aşağıdaki komutu yürütün.

MyVM1 için açık bağlantı noktası

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVmN1SG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

Sonuç benzer toohello yanıt aşağıdaki gibi görünmelidir:

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

### <a name="connect-toovirtual-machine"></a>Toovirtual makineyi bağlayın

Kullanım hello aşağıdaki toocreate SSH oturumu hello sanal makineyle bir komutu. Başlangıç IP adresi ile hello yerine `publicIpAddress` sanal makinenizin.

```bash 
ssh azureuser@<publicIpAddress>
```

### <a name="create-database-on-myvm1-primary"></a>MyVM1 üzerinde veritabanı oluşturma (birincil)

Merhaba sonraki adıma tooinstall hello veritabanı olacak şekilde hello Oracle yazılım hello Market görüntüsü üzerinde zaten yüklü. Merhaba ilk adımı hello 'oracle' süper kullanıcı çalışıyor.

```bash
sudo su - oracle
```

Merhaba veritabanı oluşturun:

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
Çıkış benzer toohello yanıt aşağıdaki gibi görünmelidir:

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
Look at hello log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for further details.
```

Merhaba ORACLE_SID ve ORACLE_HOME değişkenlerini ayarlama

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

İsteğe bağlı olarak, böylece bu ayarlar sonraki oturumlar için kaydedilir eklenen ORACLE_HOME ve ORACLE_SID toohello .bashrc dosyasını kullanabilirsiniz.

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

(Hangi hello kurtarma çok daha önce yaptığınız) Flashback açın ve STANDBY_FILE_MANAGEMENT tooauto ayarlayın

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
```

### <a name="service-setup-on-myvm1-primary"></a>MyVM1 (birincil) üzerinde hizmeti Kurulumu

Düzenleme veya $ORACLE_HOME\network\admin klasörünün bulunduğu hello tnsnames.ora dosyası oluşturma

Girdileri aşağıdaki hello ekleme

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

Düzenleme veya $ORACLE_HOME\network\admin klasörünün bulunduğu hello listener.ora dosya oluşturma

Girdileri aşağıdaki hello ekleme

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

Merhaba dinleyicisini başlatmak

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="service-setup-on-myvm2-standby"></a>Hizmeti Kurulumu myVM2 üzerinde (bekleme)

Düzenleme veya $ORACLE_HOME\network\admin klasörünün bulunduğu hello tnsnames.ora dosyası oluşturma

Girdileri aşağıdaki hello ekleme

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

Düzenleme veya $ORACLE_HOME\network\admin klasörünün bulunduğu hello listener.ora dosya oluşturma

Girdileri aşağıdaki hello ekleme

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

Merhaba dinleyicisini başlatmak

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

### <a name="restore-database-toomyvm2-standby"></a>Veritabanı toomyVM2 geri yükleme (bekleme)

Bir parametre dosyası oluştur ' / tmp/initcdb1_stby.ora' hello aşağıdakilere içeriğiyle
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

RMAN komutlarda aşağıdaki hello yürütme
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

Merhaba veri koruma Yöneticisi'ni ve oturum açma SYS ve parolası (OS kimlik doğrulaması kullanmayan yapın) kullanarak başlatın. Merhaba aşağıdakilere gerçekleştirin

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> CREATE CONFIGURATION my_dg_config AS PRIMARY DATABASE IS cdb1 CONNECT IDENTIFIER IS cdb1;
Configuration "my_dg_config" created with primary database "cdb1"
DGMGRL> ADD DATABASE cdb1_stby AS CONNECT IDENTIFIER IS cdb1_stby MAINTAINED AS PHYSICAL;
Database "cdb1_stby" added
DGMGRL> ENABLE CONFIGURATION;
Enabled.
```

Merhaba yapılandırmayı gözden geçir
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

Merhaba Oracle Data Guard Kurulum tamamlandı. Merhaba sonraki bölümde, nasıl tootest hello bağlantısı ve geçişi gösterilir.

### <a name="connect-database-from-client-machine"></a>İstemci makineden veritabanına bağlanın

Güncelleştirme veya genellikle $ORACLE_HOME\network\admin bulunur, istemci makinenizde hello tnsnames.ora dosyası oluşturun.

Merhaba IP ile değiştirmek, `publicIpAddress` myVM1 ve myVM2 için

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
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-data-guard-configuration"></a>Test veri koruma yapılandırması

### <a name="database-switchover-on-myvm1-primary"></a>Veritabanı geçiş myVM1 (birincil) üzerinde

Birincil toostandby (cdb1 toocdb1_stby) gelen tooswitch

```bash
$ dgmgrl sys/OraPasswd1@cdb1
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER toocdb1_stby;
Performing switchover NOW, please wait...
Operation requires a connection tooinstance "cdb1" on database "cdb1_stby"
Connecting tooinstance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1_stby" is opening...
Operation requires start up of instance "cdb1" on database "cdb1"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1_stby"
DGMGRL>
```

Artık mümkün tooconnect toohello bekleme veritabanı olmalıdır

Sqlplus Başlat

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="database-switch-back-on-myvm2-standby"></a>Veritabanı anahtarda geri myVM2 (bekleme)

geri tooswitch üzerinde myVM2 hello aşağıdakilere çalıştırın
```bash
$ dgmgrl sys/OraPasswd1@cdb1_stby
DGMGRL for Linux: Version 12.1.0.2.0 - 64bit Production

Copyright (c) 2000, 2013, Oracle. All rights reserved.

Welcome tooDGMGRL, type "help" for information.
Connected as SYSDBA.
DGMGRL> SWITCHOVER toocdb1;
Performing switchover NOW, please wait...
Operation requires a connection tooinstance "cdb1" on database "cdb1"
Connecting tooinstance "cdb1"...
Connected as SYSDBA.
New primary database "cdb1" is opening...
Operation requires start up of instance "cdb1" on database "cdb1_stby"
Starting instance "cdb1"...
ORACLE instance started.
Database mounted.
Switchover succeeded, new primary is "cdb1"
```

Bir kez daha, artık mümkün tooconnect toohello birincil veritabanı olması gerekir

Sqlplus Başlat

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

Bu hello yüklemesi ve Oracle linux üzerinde veri koruma yapılandırması tamamlandı.


## <a name="delete-virtual-machine"></a>Sanal makineyi silme

Artık gerekli olduğunda, komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu, VM olabilir ve ilişkili tüm kaynakları.

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Sonraki adımlar

[Yüksek oranda kullanılabilir sanal makine oluşturma öğreticisi](../../linux/create-cli-complete.md)

[VM dağıtımı CLI örneklerini keşfedin](../../linux/cli-samples.md)
