---
title: "bir Azure Linux sanal makine üzerinde aaaImplement Oracle Data Guard | Microsoft Docs"
description: "Hızlı bir şekilde Oracle Data Guard ve Azure ortamınızda çalışan alın."
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
ms.openlocfilehash: 6bb530098737e3ca7dd8bab3f4306ecbb620f3f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-data-guard-on-an-azure-linux-virtual-machine"></a>Bir Azure Linux sanal makinede Oracle veri koruma uygulama 

Azure CLI kullanılan toocreate olan ve hello komut satırından veya komut dosyalarında Azure kaynaklarını yönetin. Bu makalede nasıl toouse Azure CLI toodeploy bir Oracle veritabanına 12 c veritabanı hello Azure Market görüntüsünden açıklanmaktadır. Bu makalede daha sonra adım adım nasıl gösterilmektedir tooinstall ve veri koruma Azure sanal makine (VM) yapılandırın.

Başlamadan önce Azure CLI'ın yüklü olduğundan emin olun. Daha fazla bilgi için bkz: Merhaba [Azure CLI Yükleme Kılavuzu'na](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="prepare-hello-environment"></a>Merhaba ortamını hazırlayın
### <a name="assumptions"></a>Varsayımlar

tooinstall Oracle Data Guard, gereksinim duyduğunuz hello toocreate iki Azure sanal makineler aynı kullanılabilirlik kümesi:

- Merhaba birincil VM (myVM1) çalışan bir Oracle örneği vardır.
- Merhaba hello Oracle yazılımı yalnızca yüklü bekleme VM (myVM2) sahip.

Merhaba toocreate hello VM'ler kullandığınız Market görüntüsü olan Oracle: Oracle-veritabanı-Ee:12.1.0.2:latest.

### <a name="sign-in-tooazure"></a>İçinde tooAzure oturum 

Tooyour Azure aboneliği hello kullanarak oturum [az oturum açma](/cli/azure/#login) komut ve hello ekrandaki yönergeleri izleyin.

```azurecli
az login
```

### <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

Hello kullanarak bir kaynak grubu oluşturma [az grubu oluşturma](/cli/azure/group#create) komutu. Bir Azure kaynak grubu hangi Azure kaynakları dağıtılan yönetilen ve mantıksal bir kapsayıcısıdır. 

Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myResourceGroup` hello içinde `westus` konumu:

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a>Kullanılabilirlik kümesi oluşturma

Bir kullanılabilirlik kümesi oluşturmak isteğe bağlıdır, ancak kullanmanızı öneririz. Daha fazla bilgi için bkz: [Azure kullanılabilirlik kümeleri yönergeleri](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a>Sanal makine oluşturma

Hello kullanarak bir VM oluşturma [az vm oluşturma](/cli/azure/vm#create) komutu. 

Merhaba aşağıdaki örnek adlı iki VM'ler oluşturur `myVM1` ve `myVM2`. Zaten bir varsayılan anahtar konumda yoksa, ayrıca SSH anahtarları oluşturur. toouse belirli bir ayarla anahtarları, hello kullan `--ssh-key-value` seçeneği.

MyVM1 (birincil) oluşturun:
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

Merhaba VM oluşturduktan sonra Azure CLI örnek aşağıdaki bilgileri benzer toohello gösterir. Not hello değerini `publicIpAddress`. Bu adres tooaccess hello VM kullanın.

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

MyVM2 oluşturun (bekleme):
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

Not hello değerini `publicIpAddress` myVM2 oluşturduktan sonra.

### <a name="open-hello-tcp-port-for-connectivity"></a>Bağlantı için Hello TCP bağlantı noktasını açın

Bu adım, uzaktan erişim toohello Oracle veritabanı izin dış uç noktalar yapılandırır.

MyVM1 açık hello bağlantı noktası:

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

Merhaba sonuç benzer toohello yanıt aşağıdaki gibi görünmelidir:

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

MyVM2 açık hello bağlantı noktası:

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVM2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a>Toohello sanal makineye bağlanma

Kullanım hello aşağıdaki toocreate SSH oturumu hello sanal makineyle bir komutu. Başlangıç IP adresi ile hello yerine `publicIpAddress` sanal makineniz için değer.

```bash 
$ ssh azureuser@<publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a>Merhaba veritabanı üzerinde myVM1 (birincil) oluşturma

Merhaba sonraki adıma tooinstall hello veritabanı olacak şekilde hello Oracle yazılım hello Market görüntüsü üzerinde zaten yüklü. 

Toohello Oracle süper kullanıcı anahtarı:

```bash
$ sudo su - oracle
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

Merhaba ORACLE_SID ve ORACLE_HOME değişkenleri ayarlayın:

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
```

İsteğe bağlı olarak, ORACLE_HOME ve ORACLE_SID toohello /home/oracle/.bashrc dosyası, ekleyebilirsiniz, böylece bu ayarlar sonraki oturumlar için kaydedilir:

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

## <a name="configure-data-guard"></a>Veri koruma yapılandırma

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
Zorla günlüğe yazılmasını etkinleştirmek ve en az bir günlük dosyası bulunduğundan emin olun:

```bash
SQL> ALTER DATABASE FORCE LOGGING;
SQL> ALTER SYSTEM SWITCH LOGFILE;
```

Bekleme Yinele günlükleri oluşturun:

```bash
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo01.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo02.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo03.log') SIZE 50M;
SQL> ALTER DATABASE ADD STANDBY LOGFILE ('/u01/app/oracle/oradata/cdb1/standby_redo04.log') SIZE 50M;
```

(Kurtarma çok daha kolay hale getiren) Flashback açın ve bekleme ayarlayın\_dosya\_yönetim tooauto. Exit SQL * Plus bundan sonra.

```bash
SQL> ALTER DATABASE FLASHBACK ON;
SQL> ALTER SYSTEM SET STANDBY_FILE_MANAGEMENT=AUTO;
SQL> EXIT;
```

### <a name="set-up-service-on-myvm1-primary"></a>MyVM1 hizmette (birincil) ayarlayın

Düzenleyin veya hello $ORACLE_HOME\network\admin klasöründedir hello tnsnames.ora dosyası oluşturun.

Girdileri aşağıdaki hello ekleyin:

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

Düzenleyin veya hello $ORACLE_HOME\network\admin klasöründedir hello listener.ora dosyası oluşturun.

Girdileri aşağıdaki hello ekleyin:

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

Veri koruma Aracısı'nı etkinleştirin:
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```
Merhaba dinleyicisi başlatın:

```bash
$ lsnrctl stop
$ lsnrctl start
```

### <a name="set-up-service-on-myvm2-standby"></a>MyVM2 hizmette ayarlayın (bekleme)

SSH toomyVM2:

```bash 
$ ssh azureuser@<publicIpAddress>
```

Oracle oturum açın:

```bash
$ sudo su - oracle
```

Düzenleyin veya hello $ORACLE_HOME\network\admin klasöründedir hello tnsnames.ora dosyası oluşturun.

Girdileri aşağıdaki hello ekleyin:

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

Düzenleyin veya hello $ORACLE_HOME\network\admin klasöründedir hello listener.ora dosyası oluşturun.

Girdileri aşağıdaki hello ekleyin:

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

Merhaba dinleyicisi başlatın:

```bash
$ lsnrctl stop
$ lsnrctl start
```


### <a name="restore-hello-database-toomyvm2-standby"></a>Merhaba veritabanı toomyVM2 geri yükleme (bekleme)

Merhaba parametre dosyası /tmp/initcdb1_stby.ora içeriği aşağıdaki hello ile oluşturun:
```bash
*.db_name='cdb1'
```

Klasör Oluştur:

```bash
mkdir -p /u01/app/oracle/oradata/cdb1/pdbseed
mkdir -p /u01/app/oracle/oradata/cdb1/pdb1
mkdir -p /u01/app/oracle/fast_recovery_area/cdb1
mkdir -p /u01/app/oracle/admin/cdb1/adump
```

Bir parola dosyası oluşturun:

```bash
$ orapwd file=/u01/app/oracle/product/12.1.0/dbhome_1/dbs/orapwcdb1 password=OraPasswd1 entries=10
```
Merhaba veritabanı üzerinde myVM2 başlatın:

```bash
$ export ORACLE_SID=cdb1
$ sqlplus / as sysdba

SQL> STARTUP NOMOUNT PFILE='/tmp/initcdb1_stby.ora';
SQL> EXIT;
```

Merhaba veritabanı hello RMAN aracını kullanarak geri yükleyin:

```bash
$ rman TARGET sys/OraPasswd1@cdb1 AUXILIARY sys/OraPasswd1@cdb1_stby
```

RMAN komutlarda aşağıdaki hello çalıştırın:
```bash
DUPLICATE TARGET DATABASE
  FOR STANDBY
  FROM ACTIVE DATABASE
  DORECOVER
  SPFILE
    SET db_unique_name='CDB1_STBY' COMMENT 'Is standby'
  NOFILENAMECHECK;
```

Merhaba komutu tamamlandığında iletileri benzer toohello aşağıdaki görmeniz gerekir. RMAN çıkın.
```bash
media recovery complete, elapsed time: 00:00:00
Finished recover at 29-JUN-17
Finished Duplicate Db at 29-JUN-17

RMAN> EXIT;
```

İsteğe bağlı olarak, ORACLE_HOME ve ORACLE_SID toohello /home/oracle/.bashrc dosyası, ekleyebilirsiniz, böylece bu ayarlar sonraki oturumlar için kaydedilir:

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
```

Veri koruma Aracısı'nı etkinleştirin:
```bash
$ sqlplus / as sysdba
SQL> ALTER SYSTEM SET dg_broker_start=true;
SQL> EXIT;
```

### <a name="configure-data-guard-broker-on-myvm1-primary"></a>Veri koruma Aracısı'nı (birincil) myVM1 yapılandırma

Veri Koruma Yöneticisi'ni başlatın ve SYS ve parola kullanarak oturum açın. (İşletim sistemi kimlik doğrulamasını kullanmayın.) Merhaba aşağıdakileri gerçekleştirin:

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

Merhaba yapılandırmayı gözden geçir:
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

Merhaba Oracle Data Guard Kurulum tamamladınız. Merhaba sonraki bölümde nasıl tootest bağlantı hello ve geçebilir gösterilir.

### <a name="connect-hello-database-from-hello-client-machine"></a>Merhaba istemci makineden Hello veritabanına bağlanın

Güncelleştirin veya istemci makinenizde hello tnsnames.ora dosyası oluşturun. Bu genellikle $ORACLE_HOME\network\admin dosyasıdır.

Merhaba IP adresleriyle değiştirin, `publicIpAddress` myVM1 ve myVM2 değerleri:

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

Başlangıç SQL * Plus:

```bash
$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```
## <a name="test-hello-data-guard-configuration"></a>Test hello veri koruma yapılandırması

### <a name="switch-over-hello-database-on-myvm1-primary"></a>Merhaba veritabanında myVM1 (birincil) üzerinden geçiş

Birincil toostandby (cdb1 toocdb1_stby) gelen tooswitch:

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

Şimdi toohello bekleme veritabanı bağlanabilir.

Başlangıç SQL * Plus:

```bash

$ sqlplus sys/OraPasswd1@cdb1_stby
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

### <a name="switch-over-hello-database-on-myvm2-standby"></a>MyVM2 hello veritabanında üzerinden geçiş (bekleme)

üzerinde tooswitch üzerinde myVM2 hello aşağıdakileri çalıştırın:
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

Bir kez daha, mümkün tooconnect toohello birincil veritabanı artık olması gerekir.

Başlangıç SQL * Plus:

```bash

$ sqlplus sys/OraPasswd1@cdb1
SQL*Plus: Release 12.2.0.1.0 Production on Wed May 10 14:18:31 2017

Copyright (c) 1982, 2016, Oracle.  All rights reserved.

Connected to:
Oracle Database 12c Enterprise Edition Release 12.1.0.2.0 - 64bit Production
With hello Partitioning, OLAP, Advanced Analytics and Real Application Testing options

SQL>
```

Merhaba yükleme ve Oracle Linux üzerinde veri koruma yapılandırmasını tamamladınız.


## <a name="delete-hello-virtual-machine"></a>Merhaba sanal makineyi silme

VM artık hello olduğunda komut tooremove hello kaynak grubu, VM ve tüm ilgili kaynaklar aşağıdaki hello kullanabilirsiniz:

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Sonraki adımlar

[Öğretici: yüksek oranda kullanılabilir sanal makineler oluşturma](../../linux/create-cli-complete.md)

[VM dağıtımı Azure CLI örnekleri keşfedin](../../linux/cli-samples.md)
