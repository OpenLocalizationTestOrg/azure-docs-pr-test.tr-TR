---
title: "aaaImplement Oracle Golden kapısı Azure Linux VM'de | Microsoft Docs"
description: "Hızla bir Oracle Golden kapısı yukarı ve Azure ortamınızda çalışan alın."
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
ms.date: 05/19/2017
ms.author: rclaus
ms.openlocfilehash: 320cafd5d23ee472f0af9f92577bc6f432f65778
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-oracle-golden-gate-on-an-azure-linux-vm"></a>Bir Azure Linux VM'de Oracle Golden kapısı uygulama 

Hello Azure CLI kullanılan toocreate olan ve hello komut satırından veya komut dosyalarında Azure kaynaklarını yönetin. Bu kılavuzu nasıl toouse hello Azure CLI toodeploy 12 c bir Oracle veritabanı hello Azure Market galeri görüntüsünden ayrıntıları. 

Bu belge size adım adım gösterir nasıl toocreate, yükleyin ve Oracle Golden kapısı Azure VM temelinde yapılandırın.

Başlamadan önce Azure CLI yüklenmiş bu hello emin olun. Daha fazla bilgi için bkz. [Azure CLI yükleme kılavuzu](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="prepare-hello-environment"></a>Merhaba ortamını hazırlayın

tooperform hello Oracle Golden kapısı yükleme, gereksinim duyduğunuz hello toocreate iki Azure sanal makineler aynı kullanılabilirlik kümesi. Merhaba Market görüntü toocreate hello VM'ler kullandığınız **Oracle: Oracle-veritabanı-Ee:12.1.0.2:latest**.

Ayrıca toobe UNIX Düzenleyicisi VI aşina gerekir ve x11 (X Windows), temel bilgilere sahipsiniz.

Merhaba, hello ortamı yapılandırmasının özeti aşağıdadır:
> 
> |  | **Birincil site** | **Çoğaltma sitesi** |
> | --- | --- | --- |
> | **Oracle Sürüm** |Oracle 12c sürüm 2 – (12.1.0.2) |Oracle 12c sürüm 2 – (12.1.0.2)|
> | **Makine adı** |myVM1 |myVM2 |
> | **İşletim Sistemi** |Oracle Linux 6.x |Oracle Linux 6.x |
> | **Oracle SID** |CDB1 |CDB1 |
> | **Çoğaltma şeması** |TEST|TEST |
> | **Golden kapısı sahibi/çoğaltılır** |C ##GGADMIN |REPUSER |
> | **Golden kapısı işlemi** |EXTORA |REPORA|


### <a name="sign-in-tooazure"></a>İçinde tooAzure oturum 

Oturum açma tooyour hello Azure aboneliğinizle [az oturum açma](/cli/azure/#login) komutu. Ardından hello ekrandaki yönergeleri izleyin.

```azurecli
az login
```

### <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu. Bir Azure kaynak grubu bir mantıksal hangi Azure kaynaklarını dağıtılan içine ve hangi bunlar yönetilebilir bir kapsayıcısıdır. 

Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu `myResourceGroup` hello içinde `westus` konumu.

```azurecli
az group create --name myResourceGroup --location westus
```

### <a name="create-an-availability-set"></a>Kullanılabilirlik kümesi oluşturma

adımı aşağıdaki hello isteğe bağlıdır ancak önerilir. Daha fazla bilgi için bkz: [Azure kullanılabilirlik kümeleri Kılavuzu](https://docs.microsoft.com/azure/virtual-machines/windows/infrastructure-availability-sets-guidelines).

```azurecli
az vm availability-set create \
    --resource-group myResourceGroup \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

### <a name="create-a-virtual-machine"></a>Sanal makine oluşturma

Bir VM ile Merhaba oluşturma [az vm oluşturma](/cli/azure/vm#create) komutu. 

Merhaba aşağıdaki örnek adlı iki VM'ler oluşturur `myVM1` ve `myVM2`. Zaten bir varsayılan anahtar konumda yoksa, SSH anahtarları oluşturma. toouse belirli bir ayarla anahtarları, hello kullan `--ssh-key-value` seçeneği.

#### <a name="create-myvm1-primary"></a>MyVM1 (birincil) oluşturun:
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM1 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

Hello VM oluşturulduktan sonra aşağıdaki örneğine bilgi benzer toohello hello Azure CLI gösterir. (Merhaba not edin `publicIpAddress`. Bu kullanılan tooaccess hello VM adresidir.)

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

#### <a name="create-myvm2-replicate"></a>MyVM2 oluşturun (Çoğaltma):
```azurecli
az vm create \
     --resource-group myResourceGroup \
     --name myVM2 \
     --availability-set myAvailabilitySet \
     --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
     --size Standard_DS1_v2  \
     --generate-ssh-keys \
```

Merhaba not edin `publicIpAddress` de oluşturulduktan sonra.

### <a name="open-hello-tcp-port-for-connectivity"></a>Bağlantı için Hello TCP bağlantı noktasını açın

Merhaba sonraki tooaccess hello Oracle veritabanı'ı uzaktan etkinleştirme tooconfigure dış uç adımdır. tooconfigure dış uç noktalar Merhaba, hello aşağıdaki komutları çalıştırın.

#### <a name="open-hello-port-for-myvm1"></a>MyVM1 açık hello bağlantı noktası:

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm1NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

Merhaba sonuçları benzer toohello yanıt aşağıdaki gibi görünmelidir:

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

#### <a name="open-hello-port-for-myvm2"></a>MyVM2 açık hello bağlantı noktası:

```azurecli
az network nsg rule create --resource-group myResourceGroup\
    --nsg-name myVm2NSG --name allow-oracle\
    --protocol tcp --direction inbound --priority 999 \
    --source-address-prefix '*' --source-port-range '*' \
    --destination-address-prefix '*' --destination-port-range 1521 --access allow
```

### <a name="connect-toohello-virtual-machine"></a>Toohello sanal makineye bağlanma

Kullanım hello aşağıdaki toocreate SSH oturumu hello sanal makineyle bir komutu. Başlangıç IP adresi ile hello yerine `publicIpAddress` sanal makinenizin.

```bash 
ssh <publicIpAddress>
```

### <a name="create-hello-database-on-myvm1-primary"></a>Merhaba veritabanı üzerinde myVM1 (birincil) oluşturma

Merhaba sonraki adıma tooinstall hello veritabanı olacak şekilde hello Oracle yazılım hello Market görüntüsü üzerinde zaten yüklü. 

Merhaba yazılım hello 'oracle' süper kullanıcı çalıştırın:

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
Look at hello log file "/u01/app/oracle/cfgtoollogs/dbca/cdb1/cdb1.log" for more details.
```

Merhaba ORACLE_SID ve ORACLE_HOME değişkenleri ayarlayın.

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=gg1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

İsteğe bağlı olarak, ORACLE_HOME ve ORACLE_SID toohello .bashrc dosyası, ekleyebilirsiniz, böylece bu ayarlar gelecekteki oturum açma işlemleri için kaydedilir:

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=gg1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a>Oracle dinleyicisini başlatmak
```bash
$ sudo su - oracle
$ lsnrctl start
```

### <a name="create-hello-database-on-myvm2-replicate"></a>Merhaba veritabanı üzerinde myVM2 oluşturun (Çoğaltma)

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
Merhaba ORACLE_SID ve ORACLE_HOME değişkenleri ayarlayın.

```bash
$ ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
$ ORACLE_SID=cdb1; export ORACLE_SID
$ LD_LIBRARY_PATH=ORACLE_HOME/lib; export LD_LIBRARY_PATH
```

İsteğe bağlı olarak, böylece bu ayarlar gelecekteki oturum açma işlemleri için kaydedilir eklenen ORACLE_HOME ve ORACLE_SID toohello .bashrc dosyasını kullanabilirsiniz.

```bash
# add oracle home
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
# add oracle sid
export ORACLE_SID=cdb1
# add Oracle library path
export LD_LIBRARY_PATH=$ORACLE_HOME/lib
```

### <a name="start-oracle-listener"></a>Oracle dinleyicisini başlatmak
```bash
$ sudo su - oracle
$ lsnrctl start
```

## <a name="configure-golden-gate"></a>Golden kapısı yapılandırın 
Bu bölümde hello adımları uygulamanız tooconfigure Golden kapısı.

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
SQL> ALTER SYSTEM set enable_goldengate_replication=true;
SQL> ALTER PLUGGABLE DATABASE PDB1 OPEN;
SQL> ALTER SESSION SET CONTAINER=PDB1;
SQL> ALTER DATABASE ADD SUPPLEMENTAL LOG DATA;
SQL> EXIT;
```

### <a name="download-golden-gate-software"></a>Golden kapısı yazılımları indirme
toodownload ve hello Oracle Golden kapısı yazılım, aşağıdaki adımları tam hello hazırlayın:

1. Merhaba karşıdan **fbo_ggs_Linux_x64_shiphome.zip** hello dosyasından [Oracle Golden kapısı indirme sayfası](http://www.oracle.com/technetwork/middleware/goldengate/downloads/index.html). Başlık altında Hello karşıdan **Oracle Linux x86-64 için Oracle GoldenGate 12.x.x.x**, .zip dosyalarını toodownload bir dizi olmalıdır.

2. Merhaba .zip dosyaları tooyour istemci bilgisayara indirdikten sonra güvenli kopyalama Protokolü (SCP) toocopy hello dosyaları tooyour VM kullanın:

  ```bash
  $ scp fbo_ggs_Linux_x64_shiphome.zip <publicIpAddress>:<folder>
  ```

3. Merhaba .zip dosyalarını toohello taşıma **/ opt** klasör. Hello sahibi hello dosyaları, aşağıda gösterildiği gibi değiştirmek:

  ```bash
  $ sudo su -
  # mv <folder>/*.zip /opt
  ```

4. (Yükleme hello Linux sıkıştırmasını yardımcı programı henüz yüklü değilse) hello dosyaları sıkıştırmasını açın:

  ```bash
  # yum install unzip
  # cd /opt
  # unzip fbo_ggs_Linux_x64_shiphome.zip
  ```

5. Değiştirme izni:

  ```bash
  # chown -R oracle:oinstall /opt/fbo_ggs_Linux_x64_shiphome
  ```

### <a name="prepare-hello-client-and-vm-toorun-x11-for-windows-clients-only"></a>Merhaba istemci ve VM toorun x11 (yalnızca Windows istemcileri için) hazırlama
Bu isteğe bağlı bir adımdır. Bir Linux istemcisi kullanarak veya x11 zaten varsa bu adımı atlayabilirsiniz kurulumu.

1. PuTTY ve Xming tooyour Windows bilgisayarda indirin:

  * [PuTTY indirin](http://www.putty.org/)
  * [Xming indirin](https://xming.en.softonic.com/)

2.  PuTTY yükledikten sonra PuTTY klasörünü (örneğin, C:\Program Files\PuTTY) Merhaba, puttygen.exe (PuTTY anahtar Oluşturucu) çalıştırın.

3.  PuTTY anahtar oluşturma Aracı'nda:

  - toogenerate anahtar, select hello **Generate** düğmesi.
  - Başlangıç anahtarı Hello içeriğini kopyalayın (**Ctrl + C**).
  - Select hello **özel anahtarı Kaydet** düğmesi.
  - Görünür ve ardından hello uyarıyı göz ardı **Tamam**.

    ![Merhaba PuTTY anahtarı Oluşturucu sayfasının ekran görüntüsü](./media/oracle-golden-gate/puttykeygen.png)

4.  VM'nizi, şu komutları çalıştırın:

  ```bash
  # sudo su - oracle
  $ mkdir .ssh (if not already created)
  $ cd .ssh
  ```

5. Adlı bir dosya oluşturun **authorized_keys**. Bu dosyada hello anahtar Hello içeriğini yapıştırın ve hello dosyasını kaydedin.

  > [!NOTE]
  > başlangıç anahtarı hello dize içermelidir `ssh-rsa`. Ayrıca, başlangıç anahtarı Merhaba içeriğine tek satırlık metin olmalıdır.
  >  

6. PuTTY’yi başlatın. Merhaba, **kategori** bölmesinde, **bağlantı** > **SSH** > **Auth**. Merhaba, **kimlik doğrulama için özel anahtar dosyası** kutusunda, daha önce oluşturulan toohello anahtarı göz atın.

  ![Merhaba özel anahtarı ayarlama sayfasının ekran görüntüsü](./media/oracle-golden-gate/setprivatekey.png)

7. Merhaba, **kategori** bölmesinde, **bağlantı** > **SSH** > **X11**. Merhaba seçip **X11 Enable iletimi** kutusu.

  ![Merhaba etkinleştir X11 sayfasının ekran görüntüsü](./media/oracle-golden-gate/enablex11.png)

8. Merhaba, **kategori** bölmesinde çok Git**oturum**. Merhaba ana bilgisayar bilgilerini girin ve ardından **açık**.

  ![Merhaba oturum sayfasının ekran görüntüsü](./media/oracle-golden-gate/puttysession.png)

### <a name="install-golden-gate-software"></a>Golden kapısı yazılımı yükleyin

tooinstall Oracle Golden ağ geçidi, şu adımları tam hello:

1. Oracle oturum açın. (İçin bir parola istenmesini olmadan mümkün toosign olmalıdır.) Merhaba yüklemeye başlamadan önce Xming çalıştığından emin olun.
 
  ```bash
  $ cd /opt/fbo_ggs_Linux_x64_shiphome/Disk1
  $ ./runInstaller
  ```
2. 'Oracle veritabanı 12 c için Oracle GoldenGate' seçin. Ardından **sonraki** toocontinue.

  ![Merhaba yükleyici seçin yükleme sayfasının ekran görüntüsü](./media/oracle-golden-gate/golden_gate_install_01.png)

3. Merhaba yazılım konumunu değiştirebilirsiniz. Merhaba seçip **Yöneticisi'ni başlatın** kutusunda ve hello veritabanı konumu girin. Seçin **sonraki** toocontinue.

  ![Merhaba seçin yükleme sayfasının ekran görüntüsü](./media/oracle-golden-gate/golden_gate_install_02.png)

4. Hello stok dizini değiştirin ve ardından **sonraki** toocontinue.

  ![Merhaba seçin yükleme sayfasının ekran görüntüsü](./media/oracle-golden-gate/golden_gate_install_03.png)

5. Merhaba üzerinde **Özet** ekran, select **yükleme** toocontinue.

  ![Merhaba yükleyici seçin yükleme sayfasının ekran görüntüsü](./media/oracle-golden-gate/golden_gate_install_04.png)

6. İstendiğinde toorun bir komut dosyası 'kök olarak' olabilir. Bu durumda, ayrı bir oturum ssh toohello VM, sudo tooroot açın ve hello betiğini çalıştırın. Seçin **Tamam** devam edin.

  ![Merhaba seçin yükleme sayfasının ekran görüntüsü](./media/oracle-golden-gate/golden_gate_install_05.png)

7. Merhaba yükleme tamamlandığında seçin **Kapat** toocomplete hello işlemi.

  ![Merhaba seçin yükleme sayfasının ekran görüntüsü](./media/oracle-golden-gate/golden_gate_install_06.png)

### <a name="set-up-service-on-myvm1-primary"></a>MyVM1 hizmette (birincil) ayarlayın

1. Oluşturma veya hello tnsnames.ora dosyasını güncelleştirin:

  ```bash
  $ cd $ORACLE_HOME/network/admin
  $ vi tnsnames.ora

  cdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=cdb1)
      )
    )

  pdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=pdb1)
      )
    )
  ```

2. Merhaba Golden kapısı sahip ve kullanıcı hesapları oluşturun.

  > [!NOTE]
  > Merhaba sahip hesabı C ## önekine sahip olmalıdır.
  >

    ```bash
    $ sqlplus / as sysdba
    SQL> CREATE USER C##GGADMIN identified by ggadmin;
    SQL> EXEC dbms_goldengate_auth.grant_admin_privilege('C##GGADMIN',container=>'ALL');
    SQL> GRANT DBA tooC##GGADMIN container=all;
    SQL> connect C##GGADMIN/ggadmin
    SQL> ALTER SESSION SET CONTAINER=PDB1;
    SQL> EXIT;
    ```

3. Merhaba Golden kapısı test kullanıcı hesabı oluşturun:

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba tootest;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> @demo_ora_insert
  SQL> EXIT;
  ```

4. Merhaba extract parametre dosyası yapılandırın.

 Merhaba altın kapısı komut satırı arabirimi (ggsci) başlatın:

  ```bash
  $ sudo su - oracle
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> DBLOGIN USERID test@pdb1, PASSWORD test
  Successfully logged into database  pdb1
  GGSCI>  ADD SCHEMATRANDATA pdb1.test
  2017-05-23 15:44:25  INFO    OGG-01788  SCHEMATRANDATA has been added on schema test.
  2017-05-23 15:44:25  INFO    OGG-01976  SCHEMATRANDATA for scheduling columns has been added on schema test.

  GGSCI> EDIT PARAMS EXTORA
  ```
5. Merhaba (VI komutlarını kullanarak) aşağıdaki toohello EXTRACT parametre dosyasına ekleyin. Esc tuşuna basın, ': wq!' toosave dosyası. 

  ```bash
  EXTRACT EXTORA
  USERID C##GGADMIN, PASSWORD ggadmin
  RMTHOST 10.0.0.5, MGRPORT 7809
  RMTTRAIL ./dirdat/rt  
  DDL INCLUDE MAPPED
  DDLOPTIONS REPORT 
  LOGALLSUPCOLS
  UPDATERECORDFORMAT COMPACT
  TABLE pdb1.test.TCUSTMER;
  TABLE pdb1.test.TCUSTORD;
  ```
6. YAZMAÇ ayıklayın--tümleşik Ayıkla:

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci

  GGSCI> dblogin userid C##GGADMIN, password ggadmin
  Successfully logged into database CDB$ROOT.

  GGSCI> REGISTER EXTRACT EXTORA DATABASE CONTAINER(pdb1)

  2017-05-23 15:58:34  INFO    OGG-02003  Extract EXTORA successfully registered with database at SCN 1821260.

  GGSCI> exit
  ```
7. Extract denetim noktaları ayarlama ve gerçek zamanlı extract başlatın:

  ```bash
  $ ./ggsci
  GGSCI>  ADD EXTRACT EXTORA, INTEGRATED TRANLOG, BEGIN NOW
  EXTRACT (Integrated) added.

  GGSCI>  ADD RMTTRAIL ./dirdat/rt, EXTRACT EXTORA, MEGABYTES 10
  RMTTRAIL added.

  GGSCI>  START EXTRACT EXTORA

  Sending START request tooMANAGER ...
  EXTRACT EXTORA starting

  GGSCI > info all

  Program     Status      Group       Lag at Chkpt  Time Since Chkpt

  MANAGER     RUNNING
  EXTRACT     RUNNING     EXTORA      00:00:11      00:00:04
  ```
Bu adımda, daha sonra farklı bir bölümde kullanılacak SCN başlangıç hello bulur:

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> SELECT current_scn from v$database;
  CURRENT_SCN
  -----------
      1857887
  SQL> EXIT;
  ```

  ```bash
  $ ./ggsci
  GGSCI> EDIT PARAMS INITEXT
  ```

  ```bash
  EXTRACT INITEXT
  USERID C##GGADMIN, PASSWORD ggadmin
  RMTHOST 10.0.0.5, MGRPORT 7809
  RMTTASK REPLICAT, GROUP INITREP
  TABLE pdb1.test.*, SQLPREDICATE 'AS OF SCN 1857887'; 
  ```

  ```bash
  GGSCI> ADD EXTRACT INITEXT, SOURCEISTABLE
  ```

### <a name="set-up-service-on-myvm2-replicate"></a>MyVM2 hizmette ayarlayın (Çoğaltma)


1. Oluşturma veya hello tnsnames.ora dosyasını güncelleştirin:

  ```bash
  $ cd $ORACLE_HOME/network/admin
  $ vi tnsnames.ora

  cdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=cdb1)
      )
    )

  pdb1=
    (DESCRIPTION=
      (ADDRESS=
        (PROTOCOL=TCP)
        (HOST=localhost)
        (PORT=1521)
      )
      (CONNECT_DATA=
        (SERVER=dedicated)
        (SERVICE_NAME=pdb1)
      )
    )
  ```

2. Bir çoğaltma hesabı oluşturun:

  ```bash
  $ sqlplus / as sysdba
  SQL> alter session set container = pdb1;
  SQL> create user repuser identified by rep_pass container=current;
  SQL> grant dba toorepuser;
  SQL> exec dbms_goldengate_auth.grant_admin_privilege('REPUSER',container=>'PDB1');
  SQL> connect repuser/rep_pass@pdb1 
  SQL> EXIT;
  ```

3. Bir Golden kapısı test kullanıcı hesabı oluşturun:

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ sqlplus system/OraPasswd1@pdb1
  SQL> CREATE USER test identified by test DEFAULT TABLESPACE USERS TEMPORARY TABLESPACE TEMP;
  SQL> GRANT connect, resource, dba tootest;
  SQL> ALTER USER test QUOTA 100M on USERS;
  SQL> connect test/test@pdb1
  SQL> @demo_ora_create
  SQL> EXIT;
  ```

4. REPLICAT parametre dosyası tooreplicate değişiklikler: 

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS REPORA  
  ```
  REPORA parametresi dosyasının içeriği:

  ```bash
  REPLICAT REPORA
  ASSUMETARGETDEFS
  DISCARDFILE ./dirrpt/repora.dsc, PURGE, MEGABYTES 100
  DDL INCLUDE MAPPED
  DDLOPTIONS REPORT
  DBOPTIONS INTEGRATEDPARAMS(parallelism 6)
  USERID repuser@pdb1, PASSWORD rep_pass
  MAP pdb1.test.*, TARGET pdb1.test.*;
  ```

5. Replicat denetim noktası ayarlayın:

  ```bash
  GGSCI> ADD REPLICAT REPORA, INTEGRATED, EXTTRAIL ./dirdat/rt
  GGSCI> EDIT PARAMS INITREP

  ```

  ```bash
  REPLICAT INITREP
  ASSUMETARGETDEFS
  DISCARDFILE ./dirrpt/tcustmer.dsc, APPEND
  USERID repuser@pdb1, PASSWORD rep_pass
  MAP pdb1.test.*, TARGET pdb1.test.*;   
  ```

  ```bash
  GGSCI> ADD REPLICAT INITREP, SPECIALRUN
  ```

### <a name="set-up-hello-replication-myvm1-and-myvm2"></a>(MyVM1 ve myVM2) Hello çoğaltmayı ayarlama

#### <a name="1-set-up-hello-replication-on-myvm2-replicate"></a>1. MyVM2 hello çoğaltmayı ayarlayın (Çoğaltma)

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  GGSCI> EDIT PARAMS MGR
  ```
Merhaba dosyasını hello aşağıdakilerle güncelleştirin:

  ```bash
  PORT 7809
  ACCESSRULE, PROG *, IPADDR *, ALLOW
  ```
Hello Yöneticisi hizmetini durdurup yeniden başlatın:

  ```bash
  GGSCI> STOP MGR
  GGSCI> START MGR
  GGSCI> EXIT
  ```

#### <a name="2-set-up-hello-replication-on-myvm1-primary"></a>2. MyVM1 hello çoğaltmayı (birincil) ayarlayın

Merhaba ilk yükleme ve hatalar için onay başlatın:

```bash
$ cd /u01/app/oracle/product/12.1.0/oggcore_1
$ ./ggsci
GGSCI> START EXTRACT INITEXT
GGSCI> VIEW REPORT INITEXT
```
#### <a name="3-set-up-hello-replication-on-myvm2-replicate"></a>3. MyVM2 hello çoğaltmayı ayarlayın (Çoğaltma)

Önce aldığınız hello hello numarası SCN numarasıyla değiştirin:

  ```bash
  $ cd /u01/app/oracle/product/12.1.0/oggcore_1
  $ ./ggsci
  START REPLICAT REPORA, AFTERCSN 1857887
  ```
Merhaba çoğaltma başladıktan ve yeni kayıtlar tooTEST tablolar ekleyerek test edebilirsiniz.


### <a name="view-job-status-and-troubleshooting"></a>İş durumunu görüntüleme ve sorunlarını giderme

#### <a name="view-reports"></a>Raporları görüntüleme
tooview hello aşağıdaki komutları çalıştırın myVM1 üzerinde raporları:

  ```bash
  GGSCI> VIEW REPORT EXTORA 
  ```
 
tooview hello aşağıdaki komutları çalıştırın myVM2 üzerinde raporları:

  ```bash
  GGSCI> VIEW REPORT REPORA
  ```

#### <a name="view-status-and-history"></a>Görünüm durumu ve geçmişi
tooview durumunu ve geçmişini myVM1, hello aşağıdaki komutları çalıştırın:

  ```bash
  GGSCI> dblogin userid c##ggadmin, password ggadmin 
  GGSCI> INFO EXTRACT EXTORA, DETAIL
  ```

tooview durumunu ve geçmişini myVM2, hello aşağıdaki komutları çalıştırın:

  ```bash
  GGSCI> dblogin userid repuser@pdb1 password rep_pass 
  GGSCI> INFO REP REPORA, DETAIL
  ```
Bu, hello yükleme ve Oracle linux üzerinde Golden kapısı yapılandırmasını tamamlar.


## <a name="delete-hello-virtual-machine"></a>Merhaba sanal makineyi silme

Artık gerekli olmadığında, komutu aşağıdaki hello kullanılan tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları olabilir.

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Sonraki adımlar

[Yüksek oranda kullanılabilir sanal makine oluşturma öğreticisi](../../linux/create-cli-complete.md)

[VM dağıtımı CLI örneklerini keşfedin](../../linux/cli-samples.md)
