---
title: "Bir Oracle veritabanına bir Azure VM oluşturma | Microsoft Docs"
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
ms.openlocfilehash: 8683b016c4db2c66fb1dd994405b70c3d137a7fc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="create-an-oracle-database-in-an-azure-vm"></a><span data-ttu-id="8114a-103">Bir Oracle veritabanına bir Azure VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="8114a-103">Create an Oracle Database in an Azure VM</span></span>

<span data-ttu-id="8114a-104">Bir Azure sanal makineyi dağıtmak için Azure CLI kullanarak bu kılavuzu ayrıntılarını [Oracle Market galeri görüntüsü](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) 12 c Oracle veritabanı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="8114a-104">This guide details using the Azure CLI to deploy an Azure virtual machine from the [Oracle marketplace gallery image](https://azuremarketplace.microsoft.com/marketplace/apps/Oracle.OracleDatabase12102EnterpriseEdition?tab=Overview) in order to create an Oracle 12c database.</span></span> <span data-ttu-id="8114a-105">Sunucu dağıtıldığında, Oracle veritabanını yapılandırmak için SSH yoluyla bağlanır.</span><span class="sxs-lookup"><span data-stu-id="8114a-105">Once the server is deployed, you will connect via SSH in order to configure the Oracle database.</span></span> 

<span data-ttu-id="8114a-106">Azure aboneliğiniz yoksa başlamadan önce [ücretsiz bir hesap](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8114a-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8114a-107">CLI'yi yerel olarak yükleyip kullanmayı seçerseniz bu hızlı başlangıç için Azure CLI 2.0.4 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8114a-107">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="8114a-108">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8114a-108">Run `az --version` to find the version.</span></span> <span data-ttu-id="8114a-109">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8114a-109">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="8114a-110">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="8114a-110">Create a resource group</span></span>

<span data-ttu-id="8114a-111">[az group create](/cli/azure/group#create) komutuyla bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8114a-111">Create a resource group with the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="8114a-112">Azure kaynak grubu, Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="8114a-112">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="8114a-113">Aşağıdaki örnek *eastus* konumunda *myResourceGroup* adlı bir kaynak grubu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8114a-113">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```
## <a name="create-virtual-machine"></a><span data-ttu-id="8114a-114">Sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="8114a-114">Create virtual machine</span></span>

<span data-ttu-id="8114a-115">Bir sanal makine (VM) oluşturmak için kullanmak [az vm oluşturma](/cli/azure/vm#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="8114a-115">To create a virtual machine (VM), use the [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="8114a-116">Aşağıdaki örnekte `myVM` adlı bir VM oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="8114a-116">The following example creates a VM named `myVM`.</span></span> <span data-ttu-id="8114a-117">Zaten bir varsayılan anahtar konumda yoksa, ayrıca SSH anahtarları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8114a-117">It also creates SSH keys, if they do not already exist in a default key location.</span></span> <span data-ttu-id="8114a-118">Belirli bir anahtar kümesini kullanmak için `--ssh-key-value` seçeneğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="8114a-118">To use a specific set of keys, use the `--ssh-key-value` option.</span></span>  

```azurecli-interactive 
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --admin-username azureuser \
    --generate-ssh-keys
```

<span data-ttu-id="8114a-119">VM oluşturduktan sonra Azure CLI aşağıdaki örneğe benzer bilgiler görüntüler.</span><span class="sxs-lookup"><span data-stu-id="8114a-119">After you create the VM, Azure CLI displays information similar to the following example.</span></span> <span data-ttu-id="8114a-120">Değeri Not `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="8114a-120">Note the value for `publicIpAddress`.</span></span> <span data-ttu-id="8114a-121">VM erişmek için bu adresi kullanın.</span><span class="sxs-lookup"><span data-stu-id="8114a-121">You use this address to access the VM.</span></span>

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

## <a name="connect-to-the-vm"></a><span data-ttu-id="8114a-122">VM’ye bağlanma</span><span class="sxs-lookup"><span data-stu-id="8114a-122">Connect to the VM</span></span>

<span data-ttu-id="8114a-123">VM ile bir SSH oturumu oluşturmak için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="8114a-123">To create an SSH session with the VM, use the following command.</span></span> <span data-ttu-id="8114a-124">IP adresiyle değiştirin `publicIpAddress` , VM için değer.</span><span class="sxs-lookup"><span data-stu-id="8114a-124">Replace the IP address with the `publicIpAddress` value for your VM.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="create-the-database"></a><span data-ttu-id="8114a-125">Veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8114a-125">Create the database</span></span>

<span data-ttu-id="8114a-126">Oracle yazılım Market görüntüsü üzerinde zaten yüklü.</span><span class="sxs-lookup"><span data-stu-id="8114a-126">The Oracle software is already installed on the Marketplace image.</span></span> <span data-ttu-id="8114a-127">Bir örnek veritabanı gibi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8114a-127">Create a sample database as follows.</span></span> 

1.  <span data-ttu-id="8114a-128">Geçiş *oracle* süper kullanıcı sonra günlüğe kaydetme için dinleyici başlatılamadı:</span><span class="sxs-lookup"><span data-stu-id="8114a-128">Switch to the *oracle* superuser, then initialize the listener for logging:</span></span>

    ```bash
    $ sudo su - oracle
    $ lsnrctl start
    ```

    <span data-ttu-id="8114a-129">Çıkış aşağıdakine benzer:</span><span class="sxs-lookup"><span data-stu-id="8114a-129">The output is similar to the following:</span></span>

    ```bash
    Copyright (c) 1991, 2014, Oracle.  All rights reserved.

    Starting /u01/app/oracle/product/12.1.0/dbhome_1/bin/tnslsnr: please wait...

    TNSLSNR for Linux: Version 12.1.0.2.0 - Production
    Log messages written to /u01/app/oracle/diag/tnslsnr/myVM/listener/alert/log.xml
    Listening on: (DESCRIPTION=(ADDRESS=(PROTOCOL=tcp)(HOST=myVM.twltkue3xvsujaz1bvlrhfuiwf.dx.internal.cloudapp.net)(PORT=1521)))

    Connecting to (ADDRESS=(PROTOCOL=tcp)(HOST=)(PORT=1521))
    STATUS of the LISTENER
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
    The listener supports no services
    The command completed successfully
    ```

2.  <span data-ttu-id="8114a-130">Veritabanı oluştur:</span><span class="sxs-lookup"><span data-stu-id="8114a-130">Create the database:</span></span>

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

    <span data-ttu-id="8114a-131">Veritabanını oluşturmak için birkaç dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="8114a-131">It takes a few minutes to create the database.</span></span>

3. <span data-ttu-id="8114a-132">Oracle değişkenlerini ayarlama</span><span class="sxs-lookup"><span data-stu-id="8114a-132">Set Oracle variables</span></span>

<span data-ttu-id="8114a-133">Bağlanmadan önce iki ortam değişkenleri ayarlamanız gerekir: *ORACLE_HOME* ve *ORACLE_SID*.</span><span class="sxs-lookup"><span data-stu-id="8114a-133">Before you connect, you need to set two environment variables: *ORACLE_HOME* and *ORACLE_SID*.</span></span>

```bash
ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1; export ORACLE_HOME
ORACLE_SID=cdb1; export ORACLE_SID
```
<span data-ttu-id="8114a-134">.Bashrc dosyasına ORACLE_HOME ve ORACLE_SID değişkenlerini de ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8114a-134">You also can add ORACLE_HOME and ORACLE_SID variables to the .bashrc file.</span></span> <span data-ttu-id="8114a-135">Bu ortam değişkenleri gelecekteki oturum açma işlemleri için kaydeder.</span><span class="sxs-lookup"><span data-stu-id="8114a-135">This would save the environment variables for future sign-ins.</span></span> <span data-ttu-id="8114a-136">Aşağıdaki deyimleri eklenmiştir onaylayın `~/.bashrc` düzenleyiciyi kullanarak dosya.</span><span class="sxs-lookup"><span data-stu-id="8114a-136">Confirm the following statements have been added to the `~/.bashrc` file using editor of your choice.</span></span>

```bash
# Add ORACLE_HOME. 
export ORACLE_HOME=/u01/app/oracle/product/12.1.0/dbhome_1 
# Add ORACLE_SID. 
export ORACLE_SID=cdb1 
```

## <a name="oracle-em-express-connectivity"></a><span data-ttu-id="8114a-137">Oracle EM hızlı bağlantı</span><span class="sxs-lookup"><span data-stu-id="8114a-137">Oracle EM Express connectivity</span></span>

<span data-ttu-id="8114a-138">Veritabanı keşfetmek için kullanabileceğiniz bir GUI yönetim aracı için Oracle EM Express'i ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8114a-138">For a GUI management tool that you can use to explore the database, set up Oracle EM Express.</span></span> <span data-ttu-id="8114a-139">Oracle EM Express'e bağlanmak için önce Oracle bağlantı noktasına ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="8114a-139">To connect to Oracle EM Express, you must first set up the port in Oracle.</span></span> 

1. <span data-ttu-id="8114a-140">Sqlplus kullanarak veritabanınızı Bağlan:</span><span class="sxs-lookup"><span data-stu-id="8114a-140">Connect to your database using sqlplus:</span></span>

    ```bash
    sqlplus / as sysdba
    ```

2. <span data-ttu-id="8114a-141">Bağlandıktan sonra bağlantı noktası 5502 EM Express için ayarlama</span><span class="sxs-lookup"><span data-stu-id="8114a-141">Once connected, set the port 5502 for EM Express</span></span>

    ```bash
    exec DBMS_XDB_CONFIG.SETHTTPSPORT(5502);
    ```

3. <span data-ttu-id="8114a-142">Kapsayıcı PDB1 değilse zaten açık, ancak ilk onay durumu açın:</span><span class="sxs-lookup"><span data-stu-id="8114a-142">Open the container PDB1 if not already opened, but first check the status:</span></span>

    ```bash
    select con_id, name, open_mode from v$pdbs;
    ```

    <span data-ttu-id="8114a-143">Çıkış aşağıdakine benzer:</span><span class="sxs-lookup"><span data-stu-id="8114a-143">The output is similar to the following:</span></span>

    ```bash
      CON_ID NAME                           OPEN_MODE 
      ----------- ------------------------- ---------- 
      2           PDB$SEED                  READ ONLY 
      3           PDB1                      MOUNT
    ```

4. <span data-ttu-id="8114a-144">Varsa için OPEN_MODE `PDB1` okuma PDB1 açmak için aşağıdakilere komutları çalıştırmak yazma, değil:</span><span class="sxs-lookup"><span data-stu-id="8114a-144">If the OPEN_MODE for `PDB1` is not READ WRITE, then run the followings commands to open PDB1:</span></span>

   ```bash
    alter session set container=pdb1;
    alter database open;
   ```

<span data-ttu-id="8114a-145">Yazmanız gerekir `quit` türü ve sqlplus oturumu sona erdirmek için `exit` oracle kullanıcının oturum kapatma için.</span><span class="sxs-lookup"><span data-stu-id="8114a-145">You need to type `quit` to end the sqlplus session and type `exit` to logout of the oracle user.</span></span>

## <a name="automate-database-startup-and-shutdown"></a><span data-ttu-id="8114a-146">Veritabanı başlatma ve kapatma otomatikleştirme</span><span class="sxs-lookup"><span data-stu-id="8114a-146">Automate database startup and shutdown</span></span>

<span data-ttu-id="8114a-147">VM yeniden başlattığınızda Oracle veritabanı varsayılan tarafından otomatik olarak başlamıyor.</span><span class="sxs-lookup"><span data-stu-id="8114a-147">The Oracle database by default doesn't automatically start when you restart the VM.</span></span> <span data-ttu-id="8114a-148">Oracle veritabanı otomatik olarak başlayacak şekilde ayarlamak için ilk kök olarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="8114a-148">To set up the Oracle database to start automatically, first sign in as root.</span></span> <span data-ttu-id="8114a-149">Ardından, oluşturun ve bazı sistem dosyaları güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="8114a-149">Then, create and update some system files.</span></span>

1. <span data-ttu-id="8114a-150">Kök olarak oturum açma</span><span class="sxs-lookup"><span data-stu-id="8114a-150">Sign on as root</span></span>
    ```bash
    sudo su -
    ```

2.  <span data-ttu-id="8114a-151">Dosyasını düzenleyin, sık kullanılan düzenleyicisini kullanarak `/etc/oratab` ve varsayılan değeri değiştirmek `N` için `Y`:</span><span class="sxs-lookup"><span data-stu-id="8114a-151">Using your favorite editor, edit the file `/etc/oratab` and change the default `N` to `Y`:</span></span>

    ```bash
    cdb1:/u01/app/oracle/product/12.1.0/dbhome_1:Y
    ```

3.  <span data-ttu-id="8114a-152">Adlı bir dosya oluşturun `/etc/init.d/dbora` ve aşağıdaki içeriği yapıştırın:</span><span class="sxs-lookup"><span data-stu-id="8114a-152">Create a file named `/etc/init.d/dbora` and paste the following contents:</span></span>

    ```
    #!/bin/sh
    # chkconfig: 345 99 10
    # Description: Oracle auto start-stop script.
    #
    # Set ORA_HOME to be equivalent to $ORACLE_HOME.
    ORA_HOME=/u01/app/oracle/product/12.1.0/dbhome_1
    ORA_OWNER=oracle

    case "$1" in
    'start')
        # Start the Oracle databases:
        # The following command assumes that the Oracle sign-in
        # will not prompt the user for any values.
        # Remove "&" if you don't want startup as a background process.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbstart $ORA_HOME" &
        touch /var/lock/subsys/dbora
        ;;

    'stop')
        # Stop the Oracle databases:
        # The following command assumes that the Oracle sign-in
        # will not prompt the user for any values.
        su - $ORA_OWNER -c "$ORA_HOME/bin/dbshut $ORA_HOME" &
        rm -f /var/lock/subsys/dbora
        ;;
    esac
    ```

4.  <span data-ttu-id="8114a-153">İle dosyalarda izinleri değiştirme *chmod* gibi:</span><span class="sxs-lookup"><span data-stu-id="8114a-153">Change permissions on files with *chmod* as follows:</span></span>

    ```bash
    chgrp dba /etc/init.d/dbora
    chmod 750 /etc/init.d/dbora
    ```

5.  <span data-ttu-id="8114a-154">Sembolik bağlantılar için başlatma ve kapatma gibi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="8114a-154">Create symbolic links for startup and shutdown as follows:</span></span>

    ```bash
    ln -s /etc/init.d/dbora /etc/rc.d/rc0.d/K01dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc3.d/S99dbora
    ln -s /etc/init.d/dbora /etc/rc.d/rc5.d/S99dbora
    ```

6.  <span data-ttu-id="8114a-155">Değişikliklerinizi test etmek için VM yeniden başlatın:</span><span class="sxs-lookup"><span data-stu-id="8114a-155">To test your changes, restart the VM:</span></span>

    ```bash
    reboot
    ```

## <a name="open-ports-for-connectivity"></a><span data-ttu-id="8114a-156">Bağlantı için açık bağlantı noktaları</span><span class="sxs-lookup"><span data-stu-id="8114a-156">Open ports for connectivity</span></span>

<span data-ttu-id="8114a-157">Son görev bazı dış uç noktalar yapılandırmaktır.</span><span class="sxs-lookup"><span data-stu-id="8114a-157">The final task is to configure some external endpoints.</span></span> <span data-ttu-id="8114a-158">Azure ağ güvenliği VM koruma grubu ayarlamak için önce SSH oturumunuzun (dışında SSH önceki adımda yeniden başlatıldığı zaman başlayacağı zamana) VM'deki çıkın.</span><span class="sxs-lookup"><span data-stu-id="8114a-158">To set up the Azure Network Security Group that protects the VM, first exit your SSH session in the VM (should have been kicked out of SSH when rebooting in previous step).</span></span> 

1.  <span data-ttu-id="8114a-159">Oracle veritabanına uzaktan erişmek için kullandığınız uç nokta açmak için bir ağ güvenlik grubu kural oluştururken [az ağ nsg kuralını](/cli/azure/network/nsg/rule#create) gibi:</span><span class="sxs-lookup"><span data-stu-id="8114a-159">To open the endpoint that you use to access the Oracle database remotely, create a Network Security Group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) as follows:</span></span> 

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup\
        --nsg-name myVmNSG \
        --name allow-oracle \
        --protocol tcp \
        --priority 1001 \
        --destination-port-range 1521
    ```

2.  <span data-ttu-id="8114a-160">Oracle EM Express uzaktan erişmek için kullandığınız uç nokta açmak için bir ağ güvenlik grubu kural oluştururken [az ağ nsg kuralını](/cli/azure/network/nsg/rule#create) gibi:</span><span class="sxs-lookup"><span data-stu-id="8114a-160">To open the endpoint that you use to access Oracle EM Express remotely, create a Network Security Group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) as follows:</span></span>

    ```azurecli-interactive
    az network nsg rule create \
        --resource-group myResourceGroup \
        --nsg-name myVmNSG \
        --name allow-oracle-EM \
        --protocol tcp \
        --priority 1002 \
        --destination-port-range 5502
    ```

3. <span data-ttu-id="8114a-161">Gerekirse, VM'yi yeniden ile ortak IP adresi elde [az ağ ortak IP Göster](/cli/azure/network/public-ip#show) gibi:</span><span class="sxs-lookup"><span data-stu-id="8114a-161">If needed, obtain the public IP address of your VM again with [az network public-ip show](/cli/azure/network/public-ip#show) as follows:</span></span>

    ```azurecli-interactive
    az network public-ip show \
        --resource-group myResourceGroup \
        --name myVMPublicIP \
        --query [ipAddress] \
        --output tsv
    ```

4.  <span data-ttu-id="8114a-162">EM Express tarayıcınızdan bağlayın.</span><span class="sxs-lookup"><span data-stu-id="8114a-162">Connect EM Express from your browser.</span></span> <span data-ttu-id="8114a-163">Tarayıcınız EM (Flash yükleme gereklidir) Express ile uyumlu olduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="8114a-163">Make sure your browser is compatible with EM Express (Flash install is required):</span></span> 

    ```
    https://<VM ip address or hostname>:5502/em
    ```

<span data-ttu-id="8114a-164">Kullanarak oturum açtığınızda **SYS** hesap ve denetleme **SYSDBA'ın olarak** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="8114a-164">You can log in by using the **SYS** account, and check the **as sysdba** checkbox.</span></span> <span data-ttu-id="8114a-165">Parolayı kullanmak **OraPasswd1** yüklemesi sırasında ayarladığınız.</span><span class="sxs-lookup"><span data-stu-id="8114a-165">Use the password **OraPasswd1** that you set during installation.</span></span> 

![Oracle OEM hızlı oturum açma sayfasının ekran görüntüsü](./media/oracle-quick-start/oracle_oem_express_login.png)

## <a name="clean-up-resources"></a><span data-ttu-id="8114a-167">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="8114a-167">Clean up resources</span></span>

<span data-ttu-id="8114a-168">Azure üzerinde ilk Oracle veritabanınızı keşfetme tamamladıktan ve VM artık gerekli olmadığında, kullanabileceğiniz [az grubu Sil](/cli/azure/group#delete) VM, kaynak grubunu kaldırmak için komut ve ilişkili tüm kaynakları.</span><span class="sxs-lookup"><span data-stu-id="8114a-168">Once you have finished exploring your first Oracle database on Azure and the VM is no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="8114a-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8114a-169">Next steps</span></span>

<span data-ttu-id="8114a-170">Diğer hakkında bilgi edinin [Oracle çözümleri Azure üzerinde](oracle-considerations.md).</span><span class="sxs-lookup"><span data-stu-id="8114a-170">Learn about other [Oracle solutions on Azure](oracle-considerations.md).</span></span> 

<span data-ttu-id="8114a-171">Deneyin [yükleme ve Oracle otomatik Depolama Yönetimi yapılandırma](configure-oracle-asm.md) Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="8114a-171">Try the [Installing and Configuring Oracle Automated Storage Management](configure-oracle-asm.md) tutorial.</span></span>