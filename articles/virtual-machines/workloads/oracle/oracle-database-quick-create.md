---
title: "bir Oracle veritabanına Azure VM'deki aaaCreate | Microsoft Docs"
description: "Hızla bir Oracle veritabanına 12 c veritabanı ve Azure ortamınızda çalışan alın."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/17/2017
ms.author: rclaus
ms.openlocfilehash: 83205154c3275d5f57b46c8acfb0cb4e5c68a412
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-oracle-database-in-an-azure-vm"></a>Bir Oracle veritabanına bir Azure VM oluşturma

Hello Azure CLI toodeploy hello Azure bir sanal makineden kullanarak bu kılavuzu ayrıntılarını [Oracle Market galeri görüntüsü](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) olarak 12 c Oracle veritabanına toocreate sipariş. Merhaba sunucu dağıtıldığında, SSH yoluyla sipariş tooconfigure hello Oracle veritabanına bağlanır. 

Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.

[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu hızlı başlangıç hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).

## <a name="create-a-resource-group"></a>Kaynak grubu oluşturma

Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu. Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır. 

Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```
## <a name="create-virtual-machine"></a>Sanal makine oluşturma

toocreate bir sanal makine (VM) kullanmak hello [az vm oluşturma](/cli/azure/vm#create) komutu. 

Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den `myVM`. Zaten bir varsayılan anahtar konumda yoksa, ayrıca SSH anahtarları oluşturur. toouse belirli bir ayarla anahtarları, hello kullan `--ssh-key-value` seçeneği.  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --admin-username azureuser \
    --generate-ssh-keys
```

Merhaba VM oluşturduktan sonra Azure CLI aşağıdaki örneğine benzer toohello bilgileri görüntüler. Not hello değeri `publicIpAddress`. Bu adres tooaccess hello VM kullanın.

```azurecli
{
  "fqdns": "",
  "id": "/subscriptions/{snip}/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "westus",
  "macAddress": "00-0D-3A-36-2F-56",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "13.64.104.241",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="connect-toohello-vm"></a>Toohello VM Bağlan

hello VM ile SSH oturumu bir toocreate hello aşağıdaki komutu kullanın. Başlangıç IP adresi ile hello yerine `publicIpAddress` , VM için değer.

```bash 
ssh <publicIpAddress>
```

## <a name="create-hello-database"></a>Merhaba veritabanı oluşturma

Merhaba Oracle yazılım hello Market görüntüsü üzerinde zaten yüklü. Bir örnek veritabanı gibi oluşturun. 

1.  Geçiş toohello *oracle* süper kullanıcı sonra Initialize hello dinleyici günlük kaydı için:

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    ```

    Merhaba çıkış benzer toohello aşağıda verilmiştir:

    ```bash
    Copyright (c) 1991, 2014, Oracle.  All rights reserved.

    Starting /u01/app/oracle/product/12.1.0/dbhome_1/bin/tnslsnr: please wait...

    TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Log messages written too/u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))

    Connecting too(ADDRESS=(PROTOCOL=tcp)(HOST=)(PORT=1521))
    STATUS of hello LISTENER
    ------------------------
    Alias                     LISTENER
    Version                   TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Start Date                23-MAR-2017 15:32:08
    Uptime                    0 days 0 hr. 0 min. 0 sec
    Trace Level               off
    Security                  ON: Local OS Authentication
    SNMP                      OFF
    Listener Log File         /u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening Endpoints Summary...
    (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))
    hello listener supports no services
    hello command completed successfully
    ```

2.  Merhaba veritabanı oluşturun:

    ```bash
    dbca -silent \
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

    Birkaç dakika toocreate hello veritabanı alır.

3. Oracle değişkenlerini ayarlama

Bağlanmadan önce tooset iki ortam değişkenleri gerekir: *ORACLE_HOME* ve *ORACLE_SID*.

```bash
ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
ORACLE_SID=cdb1; export ORACLE_SID
```
ORACLE_HOME ve ORACLE_SID değişkenleri toohello .bashrc dosyası da ekleyebilirsiniz. Bu hello ortam değişkenleri gelecekteki oturum açma işlemleri için kaydetmeniz. Merhaba aşağıdaki onaylayın deyimleri toohello eklenmiştir `~/.bashrc` düzenleyiciyi kullanarak dosya.

```bash
# Add ORACLE_HOME. 
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1 
# Add ORACLE_SID. 
export ORACLE_SID=cdb1 
```

## <a name="oracle-em-express-connectivity"></a>Oracle EM hızlı bağlantı

Tooexplore hello veritabanı kullanabileceğiniz bir GUI yönetim aracı için Oracle EM Express'i ayarlayın. tooconnect tooOracle EM Express, ilk Oracle hello bağlantı noktasına ayarlamanız gerekir. 

1. Sqlplus kullanarak tooyour veritabanına bağlanın:

    ```bash
    sqlplus / as sysdba
    ```

2. Bağlantı kurulduktan sonra başlangıç bağlantı noktası 5502 EM Express için ayarlayın

    ```bash
    exec DBMS_XDB_CONFIG.SETHTTPSPORT(5502);
    ```

3. Açık hello kapsayıcı PDB1 değilse zaten açık, ancak ilk onay hello durumu:

    ```bash
    select con_id, name, open_mode from v$pdbs;
    ```

    Merhaba çıkış benzer toohello aşağıda verilmiştir:

    ```bash
      CON_ID NAME                           OPEN_MODE 
      ----------- ------------------------- ---------- 
      2           PDB$SEED                  READ ONLY 
      3           PDB1                      MOUNT
    ```

4. Varsa OPEN_MODE için hello `PDB1` okuma hello aşağıdakilere komutları tooopen PDB1 çalıştırmak yazma, değil:

   ```bash
    alter session set container=pdb1;
    alter database open;
   ```

Tootype gerek `quit` tooend hello sqlplus oturum ve türü `exit` toologout hello oracle kullanıcı.

## <a name="automate-database-startup-and-shutdown"></a>Veritabanı başlatma ve kapatma otomatikleştirme

Merhaba VM yeniden başlattığınızda hello Oracle veritabanı varsayılan olarak otomatik olarak başlamıyor. Merhaba Oracle veritabanı toostart yukarı tooset otomatik olarak ilk kez oturum açtığınızda kök olarak. Ardından, oluşturun ve bazı sistem dosyaları güncelleştirin.

1. Kök olarak oturum açma
    ```bash
    sudo su -
    ```

2.  Merhaba dosyasını düzenleyin, sık kullanılan düzenleyicisini kullanarak `/etc/oratab` hello varsayılan değiştirip `N` çok`Y`:

    ```bash
    cdb1:/u01/app/oracle/product/12.1.0/dbhome_1:Y
    ```

3.  Adlı bir dosya oluşturun `/etc/init.d/dbora` Yapıştır hello izleyerek içeriği:

    ```
    #!/bin/sh
    # chkconfig: 345 99 10
    # Description: Oracle auto start-stop script.
    #
    # Set ORA_HOME toobe equivalent too$ORACLE_HOME.
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle

    case "$1" in
    'start')
        # Start hello Oracle databases:
        # hello following command assumes that hello Oracle sign-in
        # will not prompt hello user for any values.
        # Remove "&" if you don't want startup as a background process.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" &
        touch /var/lock/subsys/dbora
        ;;

    'stop')
        # Stop hello Oracle databases:
        # hello following command assumes that hello Oracle sign-in
        # will not prompt hello user for any values.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" &
        rm -f /var/lock/subsys/dbora
        ;;
    esac
    ```

4.  İle dosyalarda izinleri değiştirme *chmod* gibi:

    ```bash
    chgrp dba /etc/init.d/dbora
    chmod 750 /etc/init.d/dbora
    ```

5.  Sembolik bağlantılar için başlatma ve kapatma gibi oluşturun:

    ```bash
    ln -s /etc/init.d/dbora /etc/rc.d/rc0.d/K01dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc3.d/S99dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc5.d/S99dbora
    ```

6.  tootest yaptığınız değişiklikleri hello VM yeniden başlatın:

    ```bash
    reboot
    ```

## <a name="open-ports-for-connectivity"></a>Bağlantı için açık bağlantı noktaları

Merhaba son görev tooconfigure bazı dış uç noktalar değil. Yukarı tooset hello VM korur Azure ağ güvenlik grubu Merhaba, ilk SSH oturumunuzda hello (dışında SSH önceki adımda yeniden başlatıldığı zaman başlayacağı zamana) VM çıkın. 

1.  tooaccess hello Oracle veritabanı uzaktan kullanmak tooopen hello uç noktası ile ağ güvenlik grubu kural oluşturma [az ağ nsg kuralını](/cli/azure/network/nsg/rule#create) gibi: 

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup\
        --nsg-name myVmNSG \
        --name allow-oracle \
        --protocol tcp \
        --priority 1001 \
        --destination-port-range 1521
    ```

2.  tooaccess Oracle EM Express uzaktan kullanmak tooopen hello uç noktası ile ağ güvenlik grubu kural oluşturma [az ağ nsg kuralını](/cli/azure/network/nsg/rule#create) gibi:

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup \
        --nsg-name myVmNSG \
        --name allow-oracle-EM \
        --protocol tcp \
        --priority 1002 \
        --destination-port-range 5502
    ```

3. Gerekirse, VM'yi yeniden hello genel IP adresi elde [az ağ ortak IP Göster](/cli/azure/network/public-ip#show) gibi:

    ```azurecli-interactive
    az network public-ip show \
        --resource-group myResourceGroup \
        --name myVMPublicIP \
        --query [ipAddress] \
        --output tsv
    ```

4.  EM Express tarayıcınızdan bağlayın. Tarayıcınız EM (Flash yükleme gereklidir) Express ile uyumlu olduğundan emin olun: 

    ```
    https://<VM ip address or hostname>:5502/em
    ```

Hello kullanarak oturum açtığınızda **SYS** hesap ve hello denetleyin **SYSDBA'ın olarak** onay kutusu. Kullanım hello parola **OraPasswd1** yüklemesi sırasında ayarladığınız. 

![Merhaba Oracle OEM hızlı oturum açma sayfasının ekran görüntüsü](./media/oracle-quick-start/oracle_oem_express_login.png)

## <a name="clean-up-resources"></a>Kaynakları temizleme

Azure üzerinde ilk Oracle veritabanınızı keşfetme tamamladıktan sonra hello VM artık gerekli olmadığında, hello kullanabilirsiniz [az grubu Sil](/cli/azure/group#delete) tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Sonraki adımlar

Diğer hakkında bilgi edinin [Oracle çözümleri Azure üzerinde](oracle-considerations.md). 

Merhaba deneyin [yükleme ve Oracle otomatik Depolama Yönetimi yapılandırma](configure-oracle-asm.md) Öğreticisi.
