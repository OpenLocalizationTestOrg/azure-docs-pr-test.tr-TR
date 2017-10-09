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
# <a name="create-an-oracle-database-in-an-azure-vm"></a><span data-ttu-id="1ca4d-103">Bir Oracle veritabanına bir Azure VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="1ca4d-103">Create an Oracle Database in an Azure VM</span></span>

<span data-ttu-id="1ca4d-104">Hello Azure CLI toodeploy hello Azure bir sanal makineden kullanarak bu kılavuzu ayrıntılarını [Oracle Market galeri görüntüsü](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) olarak 12 c Oracle veritabanına toocreate sipariş.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-104">This guide details using hello Azure CLI toodeploy an Azure virtual machine from hello [Oracle marketplace gallery image](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) in order toocreate an Oracle 12c database.</span></span> <span data-ttu-id="1ca4d-105">Merhaba sunucu dağıtıldığında, SSH yoluyla sipariş tooconfigure hello Oracle veritabanına bağlanır.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-105">Once hello server is deployed, you will connect via SSH in order tooconfigure hello Oracle database.</span></span> 

<span data-ttu-id="1ca4d-106">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="1ca4d-107">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu hızlı başlangıç hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-107">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="1ca4d-108">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-108">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="1ca4d-109">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="1ca4d-109">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="1ca4d-110">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="1ca4d-110">Create a resource group</span></span>

<span data-ttu-id="1ca4d-111">Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-111">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="1ca4d-112">Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="1ca4d-113">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *eastus* konumu.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-113">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```
## <a name="create-virtual-machine"></a><span data-ttu-id="1ca4d-114">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="1ca4d-114">Create virtual machine</span></span>

<span data-ttu-id="1ca4d-115">toocreate bir sanal makine (VM) kullanmak hello [az vm oluşturma](/cli/azure/vm#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-115">toocreate a virtual machine (VM), use hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="1ca4d-116">Merhaba aşağıdaki örnekte oluşturur adlı bir VM'den `myVM`.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-116">hello following example creates a VM named `myVM`.</span></span> <span data-ttu-id="1ca4d-117">Zaten bir varsayılan anahtar konumda yoksa, ayrıca SSH anahtarları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-117">It also creates SSH keys, if they do not already exist in a default key location.</span></span> <span data-ttu-id="1ca4d-118">toouse belirli bir ayarla anahtarları, hello kullan `--ssh-key-value` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-118">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="1ca4d-119">Merhaba VM oluşturduktan sonra Azure CLI aşağıdaki örneğine benzer toohello bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-119">After you create hello VM, Azure CLI displays information similar toohello following example.</span></span> <span data-ttu-id="1ca4d-120">Not hello değeri `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-120">Note hello value for `publicIpAddress`.</span></span> <span data-ttu-id="1ca4d-121">Bu adres tooaccess hello VM kullanın.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-121">You use this address tooaccess hello VM.</span></span>

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

## <a name="connect-toohello-vm"></a><span data-ttu-id="1ca4d-122">Toohello VM Bağlan</span><span class="sxs-lookup"><span data-stu-id="1ca4d-122">Connect toohello VM</span></span>

<span data-ttu-id="1ca4d-123">hello VM ile SSH oturumu bir toocreate hello aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-123">toocreate an SSH session with hello VM, use hello following command.</span></span> <span data-ttu-id="1ca4d-124">Başlangıç IP adresi ile hello yerine `publicIpAddress` , VM için değer.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-124">Replace hello IP address with hello `publicIpAddress` value for your VM.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="create-hello-database"></a><span data-ttu-id="1ca4d-125">Merhaba veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1ca4d-125">Create hello database</span></span>

<span data-ttu-id="1ca4d-126">Merhaba Oracle yazılım hello Market görüntüsü üzerinde zaten yüklü.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-126">hello Oracle software is already installed on hello Marketplace image.</span></span> <span data-ttu-id="1ca4d-127">Bir örnek veritabanı gibi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-127">Create a sample database as follows.</span></span> 

1.  <span data-ttu-id="1ca4d-128">Geçiş toohello *oracle* süper kullanıcı sonra Initialize hello dinleyici günlük kaydı için:</span><span class="sxs-lookup"><span data-stu-id="1ca4d-128">Switch toohello *oracle* superuser, then initialize hello listener for logging:</span></span>

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    ```

    <span data-ttu-id="1ca4d-129">Merhaba çıkış benzer toohello aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1ca4d-129">hello output is similar toohello following:</span></span>

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

2.  <span data-ttu-id="1ca4d-130">Merhaba veritabanı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="1ca4d-130">Create hello database:</span></span>

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

    <span data-ttu-id="1ca4d-131">Birkaç dakika toocreate hello veritabanı alır.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-131">It takes a few minutes toocreate hello database.</span></span>

3. <span data-ttu-id="1ca4d-132">Oracle değişkenlerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="1ca4d-132">Set Oracle variables</span></span>

<span data-ttu-id="1ca4d-133">Bağlanmadan önce tooset iki ortam değişkenleri gerekir: *ORACLE_HOME* ve *ORACLE_SID*.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-133">Before you connect, you need tooset two environment variables: *ORACLE_HOME* and *ORACLE_SID*.</span></span>

```bash
ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
ORACLE_SID=cdb1; export ORACLE_SID
```
<span data-ttu-id="1ca4d-134">ORACLE_HOME ve ORACLE_SID değişkenleri toohello .bashrc dosyası da ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-134">You also can add ORACLE_HOME and ORACLE_SID variables toohello .bashrc file.</span></span> <span data-ttu-id="1ca4d-135">Bu hello ortam değişkenleri gelecekteki oturum açma işlemleri için kaydetmeniz. Merhaba aşağıdaki onaylayın deyimleri toohello eklenmiştir `~/.bashrc` düzenleyiciyi kullanarak dosya.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-135">This would save hello environment variables for future sign-ins. Confirm hello following statements have been added toohello `~/.bashrc` file using editor of your choice.</span></span>

```bash
# Add ORACLE_HOME. 
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1 
# Add ORACLE_SID. 
export ORACLE_SID=cdb1 
```

## <a name="oracle-em-express-connectivity"></a><span data-ttu-id="1ca4d-136">Oracle EM hızlı bağlantı</span><span class="sxs-lookup"><span data-stu-id="1ca4d-136">Oracle EM Express connectivity</span></span>

<span data-ttu-id="1ca4d-137">Tooexplore hello veritabanı kullanabileceğiniz bir GUI yönetim aracı için Oracle EM Express'i ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-137">For a GUI management tool that you can use tooexplore hello database, set up Oracle EM Express.</span></span> <span data-ttu-id="1ca4d-138">tooconnect tooOracle EM Express, ilk Oracle hello bağlantı noktasına ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-138">tooconnect tooOracle EM Express, you must first set up hello port in Oracle.</span></span> 

1. <span data-ttu-id="1ca4d-139">Sqlplus kullanarak tooyour veritabanına bağlanın:</span><span class="sxs-lookup"><span data-stu-id="1ca4d-139">Connect tooyour database using sqlplus:</span></span>

    ```bash
    sqlplus / as sysdba
    ```

2. <span data-ttu-id="1ca4d-140">Bağlantı kurulduktan sonra başlangıç bağlantı noktası 5502 EM Express için ayarlayın</span><span class="sxs-lookup"><span data-stu-id="1ca4d-140">Once connected, set hello port 5502 for EM Express</span></span>

    ```bash
    exec DBMS_XDB_CONFIG.SETHTTPSPORT(5502);
    ```

3. <span data-ttu-id="1ca4d-141">Açık hello kapsayıcı PDB1 değilse zaten açık, ancak ilk onay hello durumu:</span><span class="sxs-lookup"><span data-stu-id="1ca4d-141">Open hello container PDB1 if not already opened, but first check hello status:</span></span>

    ```bash
    select con_id, name, open_mode from v$pdbs;
    ```

    <span data-ttu-id="1ca4d-142">Merhaba çıkış benzer toohello aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1ca4d-142">hello output is similar toohello following:</span></span>

    ```bash
      CON_ID NAME                           OPEN_MODE 
      ----------- ------------------------- ---------- 
      2           PDB$SEED                  READ ONLY 
      3           PDB1                      MOUNT
    ```

4. <span data-ttu-id="1ca4d-143">Varsa OPEN_MODE için hello `PDB1` okuma hello aşağıdakilere komutları tooopen PDB1 çalıştırmak yazma, değil:</span><span class="sxs-lookup"><span data-stu-id="1ca4d-143">If hello OPEN_MODE for `PDB1` is not READ WRITE, then run hello followings commands tooopen PDB1:</span></span>

   ```bash
    alter session set container=pdb1;
    alter database open;
   ```

<span data-ttu-id="1ca4d-144">Tootype gerek `quit` tooend hello sqlplus oturum ve türü `exit` toologout hello oracle kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-144">You need tootype `quit` tooend hello sqlplus session and type `exit` toologout of hello oracle user.</span></span>

## <a name="automate-database-startup-and-shutdown"></a><span data-ttu-id="1ca4d-145">Veritabanı başlatma ve kapatma otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="1ca4d-145">Automate database startup and shutdown</span></span>

<span data-ttu-id="1ca4d-146">Merhaba VM yeniden başlattığınızda hello Oracle veritabanı varsayılan olarak otomatik olarak başlamıyor.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-146">hello Oracle database by default doesn't automatically start when you restart hello VM.</span></span> <span data-ttu-id="1ca4d-147">Merhaba Oracle veritabanı toostart yukarı tooset otomatik olarak ilk kez oturum açtığınızda kök olarak.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-147">tooset up hello Oracle database toostart automatically, first sign in as root.</span></span> <span data-ttu-id="1ca4d-148">Ardından, oluşturun ve bazı sistem dosyaları güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-148">Then, create and update some system files.</span></span>

1. <span data-ttu-id="1ca4d-149">Kök olarak oturum açma</span><span class="sxs-lookup"><span data-stu-id="1ca4d-149">Sign on as root</span></span>
    ```bash
    sudo su -
    ```

2.  <span data-ttu-id="1ca4d-150">Merhaba dosyasını düzenleyin, sık kullanılan düzenleyicisini kullanarak `/etc/oratab` hello varsayılan değiştirip `N` çok`Y`:</span><span class="sxs-lookup"><span data-stu-id="1ca4d-150">Using your favorite editor, edit hello file `/etc/oratab` and change hello default `N` too`Y`:</span></span>

    ```bash
    cdb1:/u01/app/oracle/product/12.1.0/dbhome_1:Y
    ```

3.  <span data-ttu-id="1ca4d-151">Adlı bir dosya oluşturun `/etc/init.d/dbora` Yapıştır hello izleyerek içeriği:</span><span class="sxs-lookup"><span data-stu-id="1ca4d-151">Create a file named `/etc/init.d/dbora` and paste hello following contents:</span></span>

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

4.  <span data-ttu-id="1ca4d-152">İle dosyalarda izinleri değiştirme *chmod* gibi:</span><span class="sxs-lookup"><span data-stu-id="1ca4d-152">Change permissions on files with *chmod* as follows:</span></span>

    ```bash
    chgrp dba /etc/init.d/dbora
    chmod 750 /etc/init.d/dbora
    ```

5.  <span data-ttu-id="1ca4d-153">Sembolik bağlantılar için başlatma ve kapatma gibi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="1ca4d-153">Create symbolic links for startup and shutdown as follows:</span></span>

    ```bash
    ln -s /etc/init.d/dbora /etc/rc.d/rc0.d/K01dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc3.d/S99dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc5.d/S99dbora
    ```

6.  <span data-ttu-id="1ca4d-154">tootest yaptığınız değişiklikleri hello VM yeniden başlatın:</span><span class="sxs-lookup"><span data-stu-id="1ca4d-154">tootest your changes, restart hello VM:</span></span>

    ```bash
    reboot
    ```

## <a name="open-ports-for-connectivity"></a><span data-ttu-id="1ca4d-155">Bağlantı için açık bağlantı noktaları</span><span class="sxs-lookup"><span data-stu-id="1ca4d-155">Open ports for connectivity</span></span>

<span data-ttu-id="1ca4d-156">Merhaba son görev tooconfigure bazı dış uç noktalar değil.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-156">hello final task is tooconfigure some external endpoints.</span></span> <span data-ttu-id="1ca4d-157">Yukarı tooset hello VM korur Azure ağ güvenlik grubu Merhaba, ilk SSH oturumunuzda hello (dışında SSH önceki adımda yeniden başlatıldığı zaman başlayacağı zamana) VM çıkın.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-157">tooset up hello Azure Network Security Group that protects hello VM, first exit your SSH session in hello VM (should have been kicked out of SSH when rebooting in previous step).</span></span> 

1.  <span data-ttu-id="1ca4d-158">tooaccess hello Oracle veritabanı uzaktan kullanmak tooopen hello uç noktası ile ağ güvenlik grubu kural oluşturma [az ağ nsg kuralını](/cli/azure/network/nsg/rule#create) gibi:</span><span class="sxs-lookup"><span data-stu-id="1ca4d-158">tooopen hello endpoint that you use tooaccess hello Oracle database remotely, create a Network Security Group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) as follows:</span></span> 

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup\
        --nsg-name myVmNSG \
        --name allow-oracle \
        --protocol tcp \
        --priority 1001 \
        --destination-port-range 1521
    ```

2.  <span data-ttu-id="1ca4d-159">tooaccess Oracle EM Express uzaktan kullanmak tooopen hello uç noktası ile ağ güvenlik grubu kural oluşturma [az ağ nsg kuralını](/cli/azure/network/nsg/rule#create) gibi:</span><span class="sxs-lookup"><span data-stu-id="1ca4d-159">tooopen hello endpoint that you use tooaccess Oracle EM Express remotely, create a Network Security Group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) as follows:</span></span>

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup \
        --nsg-name myVmNSG \
        --name allow-oracle-EM \
        --protocol tcp \
        --priority 1002 \
        --destination-port-range 5502
    ```

3. <span data-ttu-id="1ca4d-160">Gerekirse, VM'yi yeniden hello genel IP adresi elde [az ağ ortak IP Göster](/cli/azure/network/public-ip#show) gibi:</span><span class="sxs-lookup"><span data-stu-id="1ca4d-160">If needed, obtain hello public IP address of your VM again with [az network public-ip show](/cli/azure/network/public-ip#show) as follows:</span></span>

    ```azurecli-interactive
    az network public-ip show \
        --resource-group myResourceGroup \
        --name myVMPublicIP \
        --query [ipAddress] \
        --output tsv
    ```

4.  <span data-ttu-id="1ca4d-161">EM Express tarayıcınızdan bağlayın.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-161">Connect EM Express from your browser.</span></span> <span data-ttu-id="1ca4d-162">Tarayıcınız EM (Flash yükleme gereklidir) Express ile uyumlu olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="1ca4d-162">Make sure your browser is compatible with EM Express (Flash install is required):</span></span> 

    ```
    https://<VM ip address or hostname>:5502/em
    ```

<span data-ttu-id="1ca4d-163">Hello kullanarak oturum açtığınızda **SYS** hesap ve hello denetleyin **SYSDBA'ın olarak** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-163">You can log in by using hello **SYS** account, and check hello **as sysdba** checkbox.</span></span> <span data-ttu-id="1ca4d-164">Kullanım hello parola **OraPasswd1** yüklemesi sırasında ayarladığınız.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-164">Use hello password **OraPasswd1** that you set during installation.</span></span> 

![Merhaba Oracle OEM hızlı oturum açma sayfasının ekran görüntüsü](./media/oracle-quick-start/oracle_oem_express_login.png)

## <a name="clean-up-resources"></a><span data-ttu-id="1ca4d-166">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="1ca4d-166">Clean up resources</span></span>

<span data-ttu-id="1ca4d-167">Azure üzerinde ilk Oracle veritabanınızı keşfetme tamamladıktan sonra hello VM artık gerekli olmadığında, hello kullanabilirsiniz [az grubu Sil](/cli/azure/group#delete) tooremove hello kaynak grubu, VM ve tüm ilişkili kaynakları komutu.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-167">Once you have finished exploring your first Oracle database on Azure and hello VM is no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="1ca4d-168">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1ca4d-168">Next steps</span></span>

<span data-ttu-id="1ca4d-169">Diğer hakkında bilgi edinin [Oracle çözümleri Azure üzerinde](oracle-considerations.md).</span><span class="sxs-lookup"><span data-stu-id="1ca4d-169">Learn about other [Oracle solutions on Azure](oracle-considerations.md).</span></span> 

<span data-ttu-id="1ca4d-170">Merhaba deneyin [yükleme ve Oracle otomatik Depolama Yönetimi yapılandırma](configure-oracle-asm.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="1ca4d-170">Try hello [Installing and Configuring Oracle Automated Storage Management](configure-oracle-asm.md) tutorial.</span></span>
