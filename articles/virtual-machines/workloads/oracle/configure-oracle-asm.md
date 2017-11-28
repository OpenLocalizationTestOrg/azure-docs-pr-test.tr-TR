---
title: "bir Azure Linux sanal makine üzerinde Oracle ASM yukarı aaaSet | Microsoft Docs"
description: "Hızlı bir şekilde Oracle ASM yukarı ve Azure ortamınızda çalışan alın."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: RicksterCDN
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/19/2017
ms.author: rclaus
ms.openlocfilehash: d6a7046638e919876477d46943faabcb1872acac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-oracle-asm-on-an-azure-linux-virtual-machine"></a><span data-ttu-id="90650-103">Bir Azure Linux sanal makinede Oracle ASM ayarlayın</span><span class="sxs-lookup"><span data-stu-id="90650-103">Set up Oracle ASM on an Azure Linux virtual machine</span></span>  

<span data-ttu-id="90650-104">Azure sanal makineler tam olarak yapılandırılabilir ve esnek bir bilgi işlem ortamı sağlar.</span><span class="sxs-lookup"><span data-stu-id="90650-104">Azure virtual machines provide a fully configurable and flexible computing environment.</span></span> <span data-ttu-id="90650-105">Bu öğretici hello yükleme ve yapılandırma, Oracle otomatik Depolama Yönetimi (ASM) ile birlikte temel Azure sanal makine dağıtımı kapsar.</span><span class="sxs-lookup"><span data-stu-id="90650-105">This tutorial covers basic Azure virtual machine deployment combined with hello installation and configuration of Oracle Automated Storage Management (ASM).</span></span>  <span data-ttu-id="90650-106">Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="90650-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="90650-107">Oluştur ve tooan Oracle veritabanı VM Bağlan</span><span class="sxs-lookup"><span data-stu-id="90650-107">Create and connect tooan Oracle Database VM</span></span>
> * <span data-ttu-id="90650-108">Yükleme ve Oracle otomatik Depolama Yönetimi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="90650-108">Install and configure Oracle Automated Storage Management</span></span>
> * <span data-ttu-id="90650-109">Oracle kılavuz altyapısını yükleme ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="90650-109">Install and configure Oracle Grid infrastructure</span></span>
> * <span data-ttu-id="90650-110">Bir Oracle ASM Yüklemeyi Başlat</span><span class="sxs-lookup"><span data-stu-id="90650-110">Initialize an Oracle ASM installation</span></span>
> * <span data-ttu-id="90650-111">ASM tarafından yönetilen bir Oracle DB oluştur</span><span class="sxs-lookup"><span data-stu-id="90650-111">Create an Oracle DB managed by ASM</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="90650-112">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, Bu öğretici hello Azure CLI Sürüm 2.0.4 çalıştırmasını gerektirir veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="90650-112">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="90650-113">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="90650-113">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="90650-114">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="90650-114">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-hello-environment"></a><span data-ttu-id="90650-115">Merhaba ortamını hazırlayın</span><span class="sxs-lookup"><span data-stu-id="90650-115">Prepare hello environment</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="90650-116">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="90650-116">Create a resource group</span></span>

<span data-ttu-id="90650-117">toocreate bir kaynak grubu kullanmak hello [az grubu oluşturma](/cli/azure/group#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="90650-117">toocreate a resource group, use hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="90650-118">Bir Azure kaynak grubu hangi Azure kaynakları dağıtılan yönetilen ve mantıksal bir kapsayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="90650-118">An Azure resource group is a logical container in which Azure resources are deployed and managed.</span></span> <span data-ttu-id="90650-119">Bu örnekte, bir kaynak grubu adında *myResourceGroup* hello içinde *eastus* bölge.</span><span class="sxs-lookup"><span data-stu-id="90650-119">In this example, a resource group named *myResourceGroup* in hello *eastus* region.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location eastus
```

### <a name="create-a-vm"></a><span data-ttu-id="90650-120">VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="90650-120">Create a VM</span></span>

<span data-ttu-id="90650-121">toocreate bir sanal makine hello Oracle veritabanı görüntüyü temel alarak ve toouse Oracle ASM yapılandırmak, hello kullanma [az vm oluşturma](/cli/azure/vm#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="90650-121">toocreate a virtual machine based on hello Oracle Database image and configure it toouse Oracle ASM, use hello [az vm create](/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="90650-122">Merhaba aşağıdaki örnek Standard_DS2_v2 boyutu 50 GB dört eklenen veri disklerini ile myVM adlı VM oluşturur.</span><span class="sxs-lookup"><span data-stu-id="90650-122">hello following example creates a VM named myVM that is a Standard_DS2_v2 size with four attached data disks of 50 GB each.</span></span> <span data-ttu-id="90650-123">Merhaba varsayılan anahtar konumunda Bunlar zaten yoksa, ayrıca SSH anahtarları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="90650-123">If they do not already exist in hello default key location, it also creates SSH keys.</span></span>  <span data-ttu-id="90650-124">toouse belirli bir ayarla anahtarları, hello kullan `--ssh-key-value` seçeneği.</span><span class="sxs-lookup"><span data-stu-id="90650-124">toouse a specific set of keys, use hello `--ssh-key-value` option.</span></span>  

   ```azurecli-interactive
   az vm create --resource-group myResourceGroup \
    --name myVM \
    --image Oracle:Oracle-Database-Ee:12.1.0.2:latest \
    --size Standard_DS2_v2 \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50 50 50 50
   ```

<span data-ttu-id="90650-125">Merhaba VM oluşturduktan sonra Azure CLI aşağıdaki örneğine benzer toohello bilgileri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="90650-125">After you create hello VM, Azure CLI displays information similar toohello following example.</span></span> <span data-ttu-id="90650-126">Not hello değeri `publicIpAddress`.</span><span class="sxs-lookup"><span data-stu-id="90650-126">Note hello value for `publicIpAddress`.</span></span> <span data-ttu-id="90650-127">Bu adres tooaccess hello VM kullanın.</span><span class="sxs-lookup"><span data-stu-id="90650-127">You use this address tooaccess hello VM.</span></span>

   ```azurecli
   {
     "fqdns": "",
     "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
     "location": "eastus",
     "macAddress": "00-0D-3A-36-2F-56",
     "powerState": "VM running",
     "privateIpAddress": "10.0.0.4",
     "publicIpAddress": "13.64.104.241",
     "resourceGroup": "myResourceGroup"
   }
   ```

### <a name="connect-toohello-vm"></a><span data-ttu-id="90650-128">Toohello VM Bağlan</span><span class="sxs-lookup"><span data-stu-id="90650-128">Connect toohello VM</span></span>

<span data-ttu-id="90650-129">toocreate ile SSH oturumu bir VM Merhaba ve diğer ayarları yapılandırmak, komutu aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="90650-129">toocreate an SSH session with hello VM and configure additional settings, use hello following command.</span></span> <span data-ttu-id="90650-130">Başlangıç IP adresi ile hello yerine `publicIpAddress` , VM için değer.</span><span class="sxs-lookup"><span data-stu-id="90650-130">Replace hello IP address with hello `publicIpAddress` value for your VM.</span></span>

```bash 
ssh <publicIpAddress>
```

## <a name="install-oracle-asm"></a><span data-ttu-id="90650-131">Oracle ASM yükleyin</span><span class="sxs-lookup"><span data-stu-id="90650-131">Install Oracle ASM</span></span>

<span data-ttu-id="90650-132">Oracle ASM, aşağıdaki adımları tam hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="90650-132">tooinstall Oracle ASM, complete hello following steps.</span></span> 

<span data-ttu-id="90650-133">Oracle ASM yükleme hakkında daha fazla bilgi için bkz: [ASMLib Oracle yüklemeler için Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html).</span><span class="sxs-lookup"><span data-stu-id="90650-133">For more information about installing Oracle ASM, see [Oracle ASMLib Downloads for Oracle Linux 6](http://www.oracle.com/technetwork/server-storage/linux/asmlib/ol6-1709075.html).</span></span>  

1. <span data-ttu-id="90650-134">Sipariş toocontinue ASM yüklemesiyle kök olarak toologin gerekir:</span><span class="sxs-lookup"><span data-stu-id="90650-134">You need toologin as root in order toocontinue with ASM installation:</span></span>

   ```bash
   sudo su -
   ```
   
2. <span data-ttu-id="90650-135">Bu ek komutlar tooinstall Oracle ASM bileşenleri çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="90650-135">Run these additional commands tooinstall Oracle ASM components:</span></span>

   ```bash
    yum list | grep oracleasm 
    yum -y install kmod-oracleasm.x86_64 
    yum -y install oracleasm-support.x86_64 
    wget http://download.oracle.com/otn_software/asmlib/oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    yum -y install oracleasmlib-2.0.12-1.el6.x86_64.rpm 
    rm -f oracleasmlib-2.0.12-1.el6.x86_64.rpm
   ```

3. <span data-ttu-id="90650-136">Oracle ASM yüklü olduğunu doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="90650-136">Verify that Oracle ASM is installed:</span></span>

   ```bash
   rpm -qa |grep oracleasm
   ```

    <span data-ttu-id="90650-137">Bu komutun çıktısı Hello bileşenleri aşağıdaki hello listesi:</span><span class="sxs-lookup"><span data-stu-id="90650-137">hello output of this command should list hello following components:</span></span>

    ```bash
   oracleasm-support-2.1.10-4.el6.x86_64
   kmod-oracleasm-2.0.8-15.el6_9.x86_64
   oracleasmlib-2.0.12-1.el6.x86_64
    ```

4. <span data-ttu-id="90650-138">ASM belirli kullanıcılar ve sipariş toofunction rollerinde doğru gerektirir.</span><span class="sxs-lookup"><span data-stu-id="90650-138">ASM requires specific users and roles in order toofunction correctly.</span></span> <span data-ttu-id="90650-139">Aşağıdaki komutları hello hello önkoşul kullanıcı hesapları ve grupları oluşturun:</span><span class="sxs-lookup"><span data-stu-id="90650-139">hello following commands create hello pre-requisite user accounts and groups:</span></span> 

   ```bash
    groupadd -g 54345 asmadmin 
    groupadd -g 54346 asmdba 
    groupadd -g 54347 asmoper 
    useradd -u 3000 -g oinstall -G dba,asmadmin,asmdba,asmoper grid 
    usermod -g oinstall -G dba,asmdba,asmadmin oracle
   ```

5. <span data-ttu-id="90650-140">Kullanıcılar ve gruplar oluşturulduğundan doğru doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="90650-140">Verify users and groups were created correctly:</span></span>

   ```bash
   id grid
   ```

    <span data-ttu-id="90650-141">Merhaba bu komutun çıktısı hello listesi kullanıcılar ve gruplar:</span><span class="sxs-lookup"><span data-stu-id="90650-141">hello output of this command should list hello following users and groups:</span></span>

    ```bash
    uid=3000(grid) gid=54321(oinstall) groups=54321(oinstall),54322(dba),54345(asmadmin),54346(asmdba),54347(asmoper)
    ```
 
6. <span data-ttu-id="90650-142">Kullanıcı için bir klasör oluşturun *kılavuz* ve hello sahibi:</span><span class="sxs-lookup"><span data-stu-id="90650-142">Create a folder for user *grid* and change hello owner:</span></span>

   ```bash
   mkdir /u01/app/grid 
   chown grid:oinstall /u01/app/grid
   ```

## <a name="set-up-oracle-asm"></a><span data-ttu-id="90650-143">Oracle ASM ayarlayın</span><span class="sxs-lookup"><span data-stu-id="90650-143">Set up Oracle ASM</span></span>

<span data-ttu-id="90650-144">Bu öğretici için hello varsayılan kullanıcıdır *kılavuz* ve hello varsayılan grup *asmadmin*.</span><span class="sxs-lookup"><span data-stu-id="90650-144">For this tutorial, hello default user is *grid* and hello default group is *asmadmin*.</span></span> <span data-ttu-id="90650-145">Bu hello olun *oracle* kullanıcı hello asmadmin grubunun bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="90650-145">Ensure that hello *oracle* user is part of hello asmadmin group.</span></span> <span data-ttu-id="90650-146">Oracle ASM yüklemenizi, aşağıdaki adımları tam hello yukarı tooset:</span><span class="sxs-lookup"><span data-stu-id="90650-146">tooset up your Oracle ASM installation, complete hello following steps:</span></span>

1. <span data-ttu-id="90650-147">Merhaba Oracle ASM kitaplığı sürücüsünü ayarı içerir hello varsayılan kullanıcı (Kılavuz) ve varsayılan grup (asmadmin) tanımlama hello sürücü toostart önyükleme yapılandırma yanı sıra (y seçin) ve önyükleme disklerde tooscan (y seçin).</span><span class="sxs-lookup"><span data-stu-id="90650-147">Setting up hello Oracle ASM library driver involves defining hello default user (grid) and default group (asmadmin) as well as configuring hello drive toostart on boot (choose y) and tooscan for disks on boot (choose y).</span></span> <span data-ttu-id="90650-148">Tooanswer hello hello komutu aşağıdaki istemleri gerekir:</span><span class="sxs-lookup"><span data-stu-id="90650-148">You need tooanswer hello prompts from hello following command:</span></span>

   ```bash
   /usr/sbin/oracleasm configure -i
   ```

   <span data-ttu-id="90650-149">Bu komutun çıktısı Hello izleyerek, yanıtlanan istemleri toobe ile durdurma benzer toohello görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="90650-149">hello output of this command should look similar toohello following, stopping with prompts toobe answered.</span></span>

    ```bash
   Configuring hello Oracle ASM library driver.

   This will configure hello on-boot properties of hello Oracle ASM library
   driver. hello following questions will determine whether hello driver is
   loaded on boot and what permissions it will have. hello current values
   will be shown in brackets ('[]'). Hitting <ENTER> without typing an
   answer will keep that current value. Ctrl-C will abort.

   Default user tooown hello driver interface []: grid
   Default group tooown hello driver interface []: asmadmin
   Start Oracle ASM library driver on boot (y/n) [n]: y
   Scan for Oracle ASM disks on boot (y/n) [y]: y
   Writing Oracle ASM library driver configuration: done
   ```

2. <span data-ttu-id="90650-150">Görünüm hello disk yapılandırması:</span><span class="sxs-lookup"><span data-stu-id="90650-150">View hello disk configuration:</span></span>
   ```bash
   cat /proc/partitions
   ```

   <span data-ttu-id="90650-151">Bu komutun çıktısı Hello benzer toohello kullanılabilir diskleri listesi aşağıdaki gibi görünmelidir</span><span class="sxs-lookup"><span data-stu-id="90650-151">hello output of this command should look similar toohello following listing of available disks</span></span>

   ```bash
   8       16   14680064 sdb
   8       17   14678976 sdb1
   8        0   52428800 sda
   8        1     512000 sda1
   8        2   51915776 sda2
   8       48   52428800 sdd
   8       64   52428800 sde
   8       80   52428800 sdf
   8       32   52428800 sdc
   11       0       1152 sr0
   ```

3. <span data-ttu-id="90650-152">Biçim disk */dev/sdc* hello çalıştırarak komutu aşağıdaki ve hello yanıtlama ile ister:</span><span class="sxs-lookup"><span data-stu-id="90650-152">Format disk */dev/sdc* by running hello following command and answering hello prompts with:</span></span>
   - <span data-ttu-id="90650-153">*n*Yeni bölüm için</span><span class="sxs-lookup"><span data-stu-id="90650-153">*n* for new partition</span></span>
   - <span data-ttu-id="90650-154">*p* birincil bölüm</span><span class="sxs-lookup"><span data-stu-id="90650-154">*p* for primary partition</span></span>
   - <span data-ttu-id="90650-155">*1* tooselect hello ilk bölüm</span><span class="sxs-lookup"><span data-stu-id="90650-155">*1* tooselect hello first partition</span></span>
   - <span data-ttu-id="90650-156">basın `enter` hello varsayılan ilk silindir için</span><span class="sxs-lookup"><span data-stu-id="90650-156">press `enter` for hello default first cylinder</span></span>
   - <span data-ttu-id="90650-157">basın `enter` hello varsayılan son silindir için</span><span class="sxs-lookup"><span data-stu-id="90650-157">press `enter` for hello default last cylinder</span></span>
   - <span data-ttu-id="90650-158">basın *w* toowrite hello değişiklikleri toohello bölümleme tablosu</span><span class="sxs-lookup"><span data-stu-id="90650-158">press *w* toowrite hello changes toohello partition table</span></span>  

   ```bash
   fdisk /dev/sdc
   ```
   
   <span data-ttu-id="90650-159">Yukarıda verilen hello yanıtlar kullanarak hello çıktı hello fdisk komutu için hello aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="90650-159">Using hello answers provided above, hello output for hello fdisk command should look like hello following:</span></span>

   ```bash
   Device contains not a valid DOS partition table, or Sun, SGI or OSF disklabel
   Building a new DOS disklabel with disk identifier 0xf865c6ca.
   Changes will remain in memory only, until you decide toowrite them.
   After that, of course, hello previous content won't be recoverable.

   Warning: invalid flag 0x0000 of partition table 4 will be corrected by w(rite)

   hello device presents a logical sector size that is smaller than
   hello physical sector size. Aligning tooa physical sector (or optimal
   I/O) size boundary is recommended, or performance may be impacted.

   WARNING: DOS-compatible mode is deprecated. It's strongly recommended to
           switch off hello mode (command 'c') and change display units to
           sectors (command 'u').

   Command (m for help): n
   Command action
     e   extended
     p   primary partition (1-4)
   p
   Partition number (1-4): 1
   First cylinder (1-6527, default 1):
   Using default value 1
   Last cylinder, +cylinders or +size{K,M,G} (1-6527, default 6527):
   Using default value 6527

   Command (m for help): w
   hello partition table has been altered!

   Calling ioctl() toore-read partition table.
   Syncing disks.
   ```

4. <span data-ttu-id="90650-160">Yineleme hello Fdisk komutu için önceki `/dev/sdd`, `/dev/sde`, ve `/dev/sdf`.</span><span class="sxs-lookup"><span data-stu-id="90650-160">Repeat hello preceding fdisk command for `/dev/sdd`, `/dev/sde`, and `/dev/sdf`.</span></span>

5. <span data-ttu-id="90650-161">Merhaba disk yapılandırmasını kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="90650-161">Check hello disk configuration:</span></span>

   ```bash
   cat /proc/partitions
   ```

   <span data-ttu-id="90650-162">Merhaba hello komutunun çıkışını hello aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="90650-162">hello output of hello command should look like hello following:</span></span>

   ```bash
   major minor  #blocks  name

     8       16   14680064 sdb
     8       17   14678976 sdb1
     8       32   52428800 sdc
     8       33   52428096 sdc1
     8       48   52428800 sdd
     8       49   52428096 sdd1
     8       64   52428800 sde
     8       65   52428096 sde1
     8       80   52428800 sdf
     8       81   52428096 sdf1
     8        0   52428800 sda
     8        1     512000 sda1
     8        2   51915776 sda2
     11       0    1048575 sr0
   ```

6. <span data-ttu-id="90650-163">Merhaba Oracle ASM hizmet durumunu denetleyin ve hello Oracle ASM hizmetini başlatın:</span><span class="sxs-lookup"><span data-stu-id="90650-163">Check hello Oracle ASM service status and start hello Oracle ASM service:</span></span>

   ```bash
   service oracleasm status 
   service oracleasm start
   ```

   <span data-ttu-id="90650-164">Merhaba hello komutunun çıkışını hello aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="90650-164">hello output of hello command should look like hello following:</span></span>
   
   ```bash
   Checking if ASM is loaded: no
   Checking if /dev/oracleasm is mounted: no
   Initializing hello Oracle ASMLib driver:                     [  OK  ]
   Scanning hello system for Oracle ASMLib disks:               [  OK  ]
   ```

7. <span data-ttu-id="90650-165">Oracle ASM diskleri oluşturun:</span><span class="sxs-lookup"><span data-stu-id="90650-165">Create Oracle ASM disks:</span></span>

   ```bash
   service oracleasm createdisk ASMSP /dev/sdc1 
   service oracleasm createdisk DATA /dev/sdd1 
   service oracleasm createdisk DATA1 /dev/sde1 
   service oracleasm createdisk FRA /dev/sdf1
   ```    

   <span data-ttu-id="90650-166">Merhaba hello komutunun çıkışını hello aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="90650-166">hello output of hello command should look like hello following:</span></span>

   ```bash
   Marking disk "ASMSP" as an ASM disk:                       [  OK  ]
   Marking disk "DATA" as an ASM disk:                        [  OK  ]
   Marking disk "DATA1" as an ASM disk:                       [  OK  ]
   Marking disk "FRA" as an ASM disk:                         [  OK  ]
   ```

8. <span data-ttu-id="90650-167">Oracle ASM diskleri listele:</span><span class="sxs-lookup"><span data-stu-id="90650-167">List Oracle ASM disks:</span></span>

   ```bash
   service oracleasm listdisks
   ```   

   <span data-ttu-id="90650-168">Merhaba hello komutunun çıkışını Oracle ASM diskleri aşağıdaki hello listesi:</span><span class="sxs-lookup"><span data-stu-id="90650-168">hello output of hello command should list off hello following Oracle ASM disks:</span></span>

   ```bash
    ASMSP
    DATA
    DATA1
    FRA
   ```

9. <span data-ttu-id="90650-169">Merhaba kök, oracle ve kılavuz kullanıcıların Hello parolalarını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="90650-169">Change hello passwords for hello root, oracle, and grid users.</span></span> <span data-ttu-id="90650-170">**Bu yeni parolalar Not** daha sonra hello yükleme sırasında kullandığınız gibi.</span><span class="sxs-lookup"><span data-stu-id="90650-170">**Make note of these new passwords** as you are using them later during hello installation.</span></span>

   ```bash
   passwd oracle 
   passwd grid 
   passwd root
   ```

10. <span data-ttu-id="90650-171">Başlangıç klasörü iznini değiştirin:</span><span class="sxs-lookup"><span data-stu-id="90650-171">Change hello folder permission:</span></span>

   ```bash
   chmod -R 775 /opt 
   chown grid:oinstall /opt 
   chown oracle:oinstall /dev/sdc1 
   chown oracle:oinstall /dev/sdd1 
   chown oracle:oinstall /dev/sde1 
   chown oracle:oinstall /dev/sdf1 
   chmod 600 /dev/sdc1 
   chmod 600 /dev/sdd1 
   chmod 600 /dev/sde1 
   chmod 600 /dev/sdf1
   ```

## <a name="download-and-prepare-oracle-grid-infrastructure"></a><span data-ttu-id="90650-172">Karşıdan yükle ve Oracle kılavuz altyapıyı hazırlama</span><span class="sxs-lookup"><span data-stu-id="90650-172">Download and prepare Oracle Grid Infrastructure</span></span>

<span data-ttu-id="90650-173">toodownload ve hello Oracle kılavuz altyapısı yazılımı, aşağıdaki adımları tam hello hazırlayın:</span><span class="sxs-lookup"><span data-stu-id="90650-173">toodownload and prepare hello Oracle Grid Infrastructure software, complete hello following steps:</span></span>

1. <span data-ttu-id="90650-174">Oracle kılavuz altyapı hello indirme [Oracle ASM indirme sayfası](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html).</span><span class="sxs-lookup"><span data-stu-id="90650-174">Download Oracle Grid Infrastructure from hello [Oracle ASM download page](http://www.oracle.com/technetwork/database/enterprise-edition/downloads/database12c-linux-download-2240591.html).</span></span> 

   <span data-ttu-id="90650-175">Başlıklı hello indirme altında **Oracle veritabanı Linux x86-64 12c sürüm 1 kılavuz altyapısına (12.1.0.2.0)**, hello iki .zip dosyalarını indirin.</span><span class="sxs-lookup"><span data-stu-id="90650-175">Under hello download titled **Oracle Database 12c Release 1 Grid Infrastructure (12.1.0.2.0) for Linux x86-64**, download hello two .zip files.</span></span>

2. <span data-ttu-id="90650-176">Merhaba .zip dosyaları tooyour istemci bilgisayara indirdikten sonra güvenli kopyalama Protokolü (SCP) toocopy hello dosyaları tooyour VM kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="90650-176">After you download hello .zip files tooyour client computer, you can use Secure Copy Protocol (SCP) toocopy hello files tooyour VM:</span></span>

   ```bash
   scp *.zip <publicIpAddress>:.
   ```

3. <span data-ttu-id="90650-177">SSH, Oracle VM sipariş toomove hello .zip dosyalarıyla hello Azure geri / klasör iptal et.</span><span class="sxs-lookup"><span data-stu-id="90650-177">SSH back into your Oracle VM in Azure in order toomove hello .zip files into hello /opt folder.</span></span> <span data-ttu-id="90650-178">Ardından, hello dosyaları hello sahibini değiştirin:</span><span class="sxs-lookup"><span data-stu-id="90650-178">Then, change hello owner of hello files:</span></span>

   ```bash
   ssh <publicIPAddress>
   sudo mv ./*.zip /opt
   cd /opt
   sudo chown grid:oinstall linuxamd64_12102_grid_1of2.zip
   sudo chown grid:oinstall linuxamd64_12102_grid_2of2.zip
   ```

4. <span data-ttu-id="90650-179">Merhaba dosyaları ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="90650-179">Unzip hello files.</span></span> <span data-ttu-id="90650-180">(Yükleme hello Linux sıkıştırmasını aracı önceden yüklüyse.)</span><span class="sxs-lookup"><span data-stu-id="90650-180">(Install hello Linux unzip tool if it's not already installed.)</span></span>
   
   ```bash
   sudo yum install unzip
   sudo unzip linuxamd64_12102_grid_1of2.zip
   sudo unzip linuxamd64_12102_grid_2of2.zip
   ```

5. <span data-ttu-id="90650-181">Değiştirme izni:</span><span class="sxs-lookup"><span data-stu-id="90650-181">Change permission:</span></span>
   
   ```bash
   sudo chown -R grid:oinstall /opt/grid
   ```

6. <span data-ttu-id="90650-182">Yapılandırılan güncelleştirme takas alanı.</span><span class="sxs-lookup"><span data-stu-id="90650-182">Update configured swap space.</span></span> <span data-ttu-id="90650-183">Oracle kılavuz bileşenleri en az 6.8 GB takas alanı tooinstall kılavuz gerekir.</span><span class="sxs-lookup"><span data-stu-id="90650-183">Oracle Grid components need at least 6.8 GB of swap space tooinstall Grid.</span></span> <span data-ttu-id="90650-184">Oracle Linux görüntüleri için azure'da Hello varsayılan takas dosya boyutu yalnızca 2048 MB'tır.</span><span class="sxs-lookup"><span data-stu-id="90650-184">hello default swap file size for Oracle Linux images in Azure is only 2048MB.</span></span> <span data-ttu-id="90650-185">Tooincrease gerek `ResourceDisk.SwapSizeMB` hello içinde `/etc/waagent.conf` dosya ve güncelleştirilmiş hello ayarları tootake etkisi sırayla hello WALinuxAgent hizmetini yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="90650-185">You need tooincrease `ResourceDisk.SwapSizeMB` in hello `/etc/waagent.conf` file and restart hello WALinuxAgent service in order for hello updated settings tootake effect.</span></span> <span data-ttu-id="90650-186">Salt okunur bir dosya olduğundan, toochange dosya izinleri tooenable yazma erişimi gerekir.</span><span class="sxs-lookup"><span data-stu-id="90650-186">Because it is a read-only file, you need toochange file permissions tooenable write access.</span></span>

   ```bash
   sudo chmod 777 /etc/waagent.conf  
   vi /etc/waagent.conf
   ```
   
   <span data-ttu-id="90650-187">Arama `ResourceDisk.SwapSizeMB` değiştirip hello değeri çok**8192**.</span><span class="sxs-lookup"><span data-stu-id="90650-187">Search for `ResourceDisk.SwapSizeMB` and change hello value too**8192**.</span></span> <span data-ttu-id="90650-188">Toopress gerekir `insert` tooenter ekleme modu, hello değeri türü **8192** ve tuşuna basarak `esc` tooreturn toocommand modu.</span><span class="sxs-lookup"><span data-stu-id="90650-188">You will need toopress `insert` tooenter insert mode, type in hello value of **8192** and then press `esc` tooreturn toocommand mode.</span></span> <span data-ttu-id="90650-189">toowrite hello değişiklikleri ve çıkma hello dosya türünü `:wq` ve basın `enter`.</span><span class="sxs-lookup"><span data-stu-id="90650-189">toowrite hello changes and quit hello file, type `:wq` and press `enter`.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="90650-190">Her zaman kullanmanız önerilir `WALinuxAgent` tooconfigure takas alanı böylece her zaman hello yerel diskteki kısa ömürlü (geçici disk) en iyi performans için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="90650-190">We highly recommend that you always use `WALinuxAgent` tooconfigure swap space so that it's always created on hello local ephemeral disk (temporary disk) for best performance.</span></span> <span data-ttu-id="90650-191">Daha fazla bilgi için bkz: [nasıl tooadd bir takas dosyası Linux Azure sanal makinelerinde](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="90650-191">For more information on, see [How tooadd a swap file in Linux Azure virtual machines](https://support.microsoft.com/en-us/help/4010058/how-to-add-a-swap-file-in-linux-azure-virtual-machines).</span></span>

## <a name="prepare-your-local-client-and-vm-toorun-x11"></a><span data-ttu-id="90650-192">Yerel istemci ve VM toorun x11 hazırlama</span><span class="sxs-lookup"><span data-stu-id="90650-192">Prepare your local client and VM toorun x11</span></span>
<span data-ttu-id="90650-193">Oracle ASM yapılandırma, bir grafik arabirim toocomplete hello yükleme ve yapılandırma gerektirir.</span><span class="sxs-lookup"><span data-stu-id="90650-193">Configuring Oracle ASM requires a graphical interface toocomplete hello install and configuration.</span></span> <span data-ttu-id="90650-194">Bu yükleme hello x11 Protokolü toofacilitate kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="90650-194">We are using hello x11 protocol toofacilitate this installation.</span></span> <span data-ttu-id="90650-195">X11 zaten olan bir istemci sistem (Mac veya Linux) kullanıyorsanız, özellikleri etkinleştirilmiş ve yapılandırılmış - bu yapılandırmasını atla ve özel tooWindows makineler kurulumu.</span><span class="sxs-lookup"><span data-stu-id="90650-195">If you are using a client system (Mac or Linux) that already has X11 capabilities enabled and configured - you can skip this configuration and setup exclusive tooWindows machines.</span></span> 

1. <span data-ttu-id="90650-196">[PuTTY karşıdan](http://www.putty.org/) ve [Xming karşıdan](https://xming.en.softonic.com/) tooyour Windows bilgisayarı.</span><span class="sxs-lookup"><span data-stu-id="90650-196">[Download PuTTY](http://www.putty.org/) and [download Xming](https://xming.en.softonic.com/) tooyour Windows computer.</span></span> <span data-ttu-id="90650-197">Merhaba varsayılan değerlerle devam etmeden önce bu uygulamaların her ikisi de toocomplete hello yüklemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="90650-197">You will need toocomplete hello installation of both of these applications with hello default values before proceeding.</span></span>

2. <span data-ttu-id="90650-198">PuTTY yükledikten sonra bir komut istemi açın, hello PuTTY klasörünü (örneğin, C:\Program Files\PuTTY) değiştirin ve çalıştırın `puttygen.exe` içinde bir anahtar toogenerate sipariş.</span><span class="sxs-lookup"><span data-stu-id="90650-198">After you install PuTTY, open a command prompt, change into hello PuTTY folder (for example, C:\Program Files\PuTTY), and run `puttygen.exe` in order toogenerate a key.</span></span>

3. <span data-ttu-id="90650-199">PuTTY anahtar oluşturma Aracı'nda:</span><span class="sxs-lookup"><span data-stu-id="90650-199">In PuTTY Key Generator:</span></span>
   
   1. <span data-ttu-id="90650-200">Merhaba seçerek bir anahtar oluşturmak `Generate` düğmesi.</span><span class="sxs-lookup"><span data-stu-id="90650-200">Generate a key by selecting hello `Generate` button.</span></span>
   2. <span data-ttu-id="90650-201">Başlangıç anahtarı (Ctrl + C) Hello içeriğini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="90650-201">Copy hello contents of hello key (Ctrl+C).</span></span>
   3. <span data-ttu-id="90650-202">Select hello `Save private key` düğmesi.</span><span class="sxs-lookup"><span data-stu-id="90650-202">Select hello `Save private key` button.</span></span>
   4. <span data-ttu-id="90650-203">Başlangıç anahtarı bir parola ile güvenli hale getirme hakkında hello uyarıyı yok sayın ve ardından `OK`.</span><span class="sxs-lookup"><span data-stu-id="90650-203">Ignore hello warning about securing hello key with a passphrase, and then select `OK`.</span></span>

   ![PuTTY anahtar oluşturucunun ekran görüntüsü](./media/oracle-asm/puttykeygen.png)

4. <span data-ttu-id="90650-205">VM'nizi, şu komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="90650-205">In your VM, run these commands:</span></span>

   ```bash
   sudo su - grid
   mkdir .ssh 
   cd .ssh
   ```

5. <span data-ttu-id="90650-206">Adlı bir dosya oluşturun `authorized_keys`.</span><span class="sxs-lookup"><span data-stu-id="90650-206">Create a file named `authorized_keys`.</span></span> <span data-ttu-id="90650-207">Bu dosyada hello anahtar Hello içeriğini yapıştırın ve hello dosyasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="90650-207">Paste hello contents of hello key in this file, and then save hello file.</span></span>

   > [!NOTE]
   > <span data-ttu-id="90650-208">başlangıç anahtarı hello dize içermelidir `ssh-rsa`.</span><span class="sxs-lookup"><span data-stu-id="90650-208">hello key must contain hello string `ssh-rsa`.</span></span> <span data-ttu-id="90650-209">Ayrıca, başlangıç anahtarı Merhaba içeriğine tek satırlık metin olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="90650-209">Also, hello contents of hello key must be a single line of text.</span></span>
   >  

6. <span data-ttu-id="90650-210">İstemci sisteminizde Putty'yi başlatın.</span><span class="sxs-lookup"><span data-stu-id="90650-210">On your client system, start PuTTY.</span></span> <span data-ttu-id="90650-211">Merhaba, **kategori** bölmesinde çok Git**bağlantı** > **SSH** > **Auth**. Merhaba, **kimlik doğrulama için özel anahtar dosyası** kutusunda, daha önce oluşturulan toohello anahtarı göz atın.</span><span class="sxs-lookup"><span data-stu-id="90650-211">In hello **Category** pane, go too**Connection** > **SSH** > **Auth**. In hello **Private key file for authentication** box, browse toohello key that you generated earlier.</span></span>

   ![Merhaba SSH kimlik doğrulaması seçeneklerinin ekran görüntüsü](./media/oracle-asm/setprivatekey.png)

7. <span data-ttu-id="90650-213">Merhaba, **kategori** bölmesinde çok Git**bağlantı** > **SSH** > **X11**.</span><span class="sxs-lookup"><span data-stu-id="90650-213">In hello **Category** pane, go too**Connection** > **SSH** > **X11**.</span></span> <span data-ttu-id="90650-214">Select hello **X11 Enable iletimi** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="90650-214">Select hello **Enable X11 forwarding** check box.</span></span>

   ![Ekran görüntüsü hello SSH X11 seçenekleri iletme](./media/oracle-asm/enablex11.png)

8. <span data-ttu-id="90650-216">Merhaba, **kategori** bölmesinde çok Git**oturum**.</span><span class="sxs-lookup"><span data-stu-id="90650-216">In hello **Category** pane, go too**Session**.</span></span> <span data-ttu-id="90650-217">Oracle ASM VM girin `<publicIPaddress>` hello ana bilgisayar adı iletişim kutusunda, yeni bir dolgu `Saved Session` adlandırın ve ardından tıklatın `Save`.</span><span class="sxs-lookup"><span data-stu-id="90650-217">Enter your Oracle ASM VM `<publicIPaddress>` in hello host name dialog box, fill in a new `Saved Session` name and then click on `Save`.</span></span>  <span data-ttu-id="90650-218">Kaydedildikten sonra tıklayın `open` tooconnect tooyour Oracle ASM sanal makine.</span><span class="sxs-lookup"><span data-stu-id="90650-218">Once saved, click on `open` tooconnect tooyour Oracle ASM virtual machine.</span></span>  <span data-ttu-id="90650-219">Merhaba, bağlandığınız ilk kez uyarı hello uzak sistem, kayıt defterinde önbelleğe alınmaz.</span><span class="sxs-lookup"><span data-stu-id="90650-219">hello first time you connect you are warned  hello remote system is not cached in your registry.</span></span> <span data-ttu-id="90650-220">Tıklayın `yes` tooadd onu ve devam edin.</span><span class="sxs-lookup"><span data-stu-id="90650-220">Click on `yes` tooadd it and continue.</span></span>

   ![Merhaba PuTTY oturum seçeneklerinin ekran görüntüsü](./media/oracle-asm/puttysession.png)

## <a name="install-oracle-grid-infrastructure"></a><span data-ttu-id="90650-222">Oracle kılavuz altyapısı yükleme</span><span class="sxs-lookup"><span data-stu-id="90650-222">Install Oracle Grid Infrastructure</span></span>

<span data-ttu-id="90650-223">tooinstall Oracle kılavuz altyapı, aşağıdaki adımları tam hello:</span><span class="sxs-lookup"><span data-stu-id="90650-223">tooinstall Oracle Grid Infrastructure, complete hello following steps:</span></span>

1. <span data-ttu-id="90650-224">Olarak oturum açın **kılavuz**.</span><span class="sxs-lookup"><span data-stu-id="90650-224">Sign in as **grid**.</span></span> <span data-ttu-id="90650-225">(İçin bir parola istenmesini olmadan mümkün toosign olmalıdır.)</span><span class="sxs-lookup"><span data-stu-id="90650-225">(You should be able toosign in without being prompted for a password.)</span></span> 

   > [!NOTE]
   > <span data-ttu-id="90650-226">Windows çalıştırıyorsanız, hello yüklemeye başlamadan önce Xming başlatıldığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="90650-226">If you are running Windows, make sure you have started Xming before you begin hello installation.</span></span>

   ```bash
   cd /opt/grid
   ./runInstaller
   ```

   <span data-ttu-id="90650-227">Oracle kılavuz altyapı 12c sürüm 1 yükleyicisi açılır.</span><span class="sxs-lookup"><span data-stu-id="90650-227">Oracle Grid Infrastructure 12c Release 1 Installer opens.</span></span> <span data-ttu-id="90650-228">(Merhaba yükleyici toostart birkaç dakika sürebilir.)</span><span class="sxs-lookup"><span data-stu-id="90650-228">(It might take a few minutes for hello  installer toostart.)</span></span>

2. <span data-ttu-id="90650-229">Merhaba üzerinde **yükleme seçeneği** sayfasında **yüklenir ve tek başına bir sunucu için Oracle kılavuz altyapı yapılandırma**.</span><span class="sxs-lookup"><span data-stu-id="90650-229">On hello **Select Installation Option** page, select **Install and Configure Oracle Grid Infrastructure for a Standalone Server**.</span></span>

   ![Merhaba Yükleyicisi'nin yükleme seçeneği sayfasının ekran görüntüsü](./media/oracle-asm/install01.png)

3. <span data-ttu-id="90650-231">Hello üzerinde **ürün dilleri seçin** sayfasında, olun **İngilizce** veya istediğiniz hello dil seçilidir.</span><span class="sxs-lookup"><span data-stu-id="90650-231">On hello **Select Product Languages** page, ensure **English** or hello language that you want is selected.</span></span>  <span data-ttu-id="90650-232">`next` öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="90650-232">Click `next`.</span></span>

4. <span data-ttu-id="90650-233">Merhaba üzerinde **ASM Disk grubu oluşturma** sayfa:</span><span class="sxs-lookup"><span data-stu-id="90650-233">On hello **Create ASM Disk Group** page:</span></span>
   - <span data-ttu-id="90650-234">Merhaba disk grubu için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="90650-234">Enter a name for hello disk group.</span></span>
   - <span data-ttu-id="90650-235">Altında **artıklık**seçin **dış**.</span><span class="sxs-lookup"><span data-stu-id="90650-235">Under **Redundancy**, select **External**.</span></span>
   - <span data-ttu-id="90650-236">Altında **ayırma birimi boyutu**seçin **4**.</span><span class="sxs-lookup"><span data-stu-id="90650-236">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="90650-237">Altında **disk Ekle**seçin **ORCLASMSP**.</span><span class="sxs-lookup"><span data-stu-id="90650-237">Under **Add Disks**, select **ORCLASMSP**.</span></span>
   - <span data-ttu-id="90650-238">`next` öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="90650-238">Click `next`.</span></span>

5. <span data-ttu-id="90650-239">Merhaba üzerinde **belirtin ASM parola** sayfası, select hello **bu hesaplar için aynı parolayı kullanın** seçeneği ve bir parola girin.</span><span class="sxs-lookup"><span data-stu-id="90650-239">On hello **Specify ASM Password** page, select hello **Use same passwords for these accounts** option, and enter a password.</span></span>

   ![Merhaba Yükleyicisi'nin belirtin ASM parola sayfasının ekran görüntüsü](./media/oracle-asm/install04.png)

6. <span data-ttu-id="90650-241">Merhaba üzerinde **yönetimi seçeneklerini belirtin** sayfasında hello seçeneği tooconfigure EM bulut denetim sahip.</span><span class="sxs-lookup"><span data-stu-id="90650-241">On hello **Specify Management Options** page, you have hello option tooconfigure EM Cloud Control.</span></span> <span data-ttu-id="90650-242">Biz bu seçenek atlanıyor - tıklatın `next` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="90650-242">We are skipping this option - click `next` toocontinue.</span></span> 

7. <span data-ttu-id="90650-243">Merhaba üzerinde **ayrıcalıklı işletim sistemi gruplarına** sayfasında, hello varsayılan ayarları kullanın.</span><span class="sxs-lookup"><span data-stu-id="90650-243">On hello **Privileged Operating System Groups** page, use hello default settings.</span></span> <span data-ttu-id="90650-244">Tıklatın `next` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="90650-244">Click `next` toocontinue.</span></span>

8. <span data-ttu-id="90650-245">Merhaba üzerinde **yükleme konumu belirtin** sayfasında, hello varsayılan ayarları kullanın.</span><span class="sxs-lookup"><span data-stu-id="90650-245">On hello **Specify Installation Location** page, use hello default settings.</span></span> <span data-ttu-id="90650-246">Tıklatın `next` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="90650-246">Click `next` toocontinue.</span></span>

9. <span data-ttu-id="90650-247">Merhaba üzerinde **Envanter Oluştur** sayfasında, hello stok dizini çok değiştirmek`/u01/app/grid/oraInventory`.</span><span class="sxs-lookup"><span data-stu-id="90650-247">On hello **Create Inventory** page, change hello Inventory Directory too`/u01/app/grid/oraInventory`.</span></span> <span data-ttu-id="90650-248">Tıklatın `next` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="90650-248">Click `next` toocontinue.</span></span>

   ![Merhaba Yükleyicisi'nin Envanter Oluştur sayfasının ekran görüntüsü](./media/oracle-asm/install08.png)

10. <span data-ttu-id="90650-250">Merhaba üzerinde **kök komut dosyası yürütme Yapılandırması** sayfası, select hello **otomatik yapılandırma komut dosyaları çalıştırmak** onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="90650-250">On hello **Root script execution configuration** page, select hello **Automatically run configuration scripts** check box.</span></span> <span data-ttu-id="90650-251">Merhaba seçip **"root" kullanıcı kimlik bilgisi kullanma** seçeneği ve hello kök kullanıcı parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="90650-251">Then, select hello **Use "root" user credential** option, and enter hello root user password.</span></span>

    ![Merhaba Yükleyicisi'nin kök komut dosyası yürütme yapılandırma sayfasının ekran görüntüsü](./media/oracle-asm/install09.png)

11. <span data-ttu-id="90650-253">Merhaba üzerinde **gerçekleştirmek önkoşul denetler** sayfasında hello geçerli kurulumu başarısız olur hatalarla.</span><span class="sxs-lookup"><span data-stu-id="90650-253">On hello **Perform Prerequisite Checks** page, hello current setup will fail with errors.</span></span> <span data-ttu-id="90650-254">Bu beklenen bir davranıştır.</span><span class="sxs-lookup"><span data-stu-id="90650-254">This is an expected behavior.</span></span> <span data-ttu-id="90650-255">`Fix & Check Again` öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="90650-255">Select `Fix & Check Again`.</span></span>

12. <span data-ttu-id="90650-256">Merhaba, **düzeltmesi betik** iletişim kutusu, tıklatın `OK`.</span><span class="sxs-lookup"><span data-stu-id="90650-256">In hello **Fixup Script** dialog box, click `OK`.</span></span>

13. <span data-ttu-id="90650-257">Merhaba üzerinde **Özet** sayfasında, seçtiğiniz ayarları gözden geçirin ve ardından `Install`.</span><span class="sxs-lookup"><span data-stu-id="90650-257">On hello **Summary** page, review your selected settings, and then click `Install`.</span></span>

    ![Merhaba Yükleyicisi'nin Özet sayfasının ekran görüntüsü](./media/oracle-asm/install12.png)

14. <span data-ttu-id="90650-259">Toobe ayrıcalıklı bir kullanıcı olarak çalıştırmanız gerekir, yapılandırma komut bildiren bir uyarı iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="90650-259">A warning dialog box appears informing you configuration scripts need toobe run as a privileged user.</span></span> <span data-ttu-id="90650-260">Tıklatın `Yes` toocontinue.</span><span class="sxs-lookup"><span data-stu-id="90650-260">Click `Yes` toocontinue.</span></span>

15. <span data-ttu-id="90650-261">Merhaba üzerinde **son** sayfasında, `Close` toofinish hello yükleme.</span><span class="sxs-lookup"><span data-stu-id="90650-261">On hello **Finish** page, click `Close` toofinish hello installation.</span></span>

## <a name="set-up-your-oracle-asm-installation"></a><span data-ttu-id="90650-262">Oracle ASM yüklemenizi ayarlayın</span><span class="sxs-lookup"><span data-stu-id="90650-262">Set up your Oracle ASM installation</span></span>

<span data-ttu-id="90650-263">Oracle ASM yüklemenizi, aşağıdaki adımları tam hello yukarı tooset:</span><span class="sxs-lookup"><span data-stu-id="90650-263">tooset up your Oracle ASM installation, complete hello following steps:</span></span>

1. <span data-ttu-id="90650-264">Hala oturum açmaya olarak olun **kılavuz**, sizin X11 gelen oturum.</span><span class="sxs-lookup"><span data-stu-id="90650-264">Ensure you are still signed in as **grid**, from your X11 session.</span></span> <span data-ttu-id="90650-265">Toohit gerekebilecek `enter` toorevive hello terminal.</span><span class="sxs-lookup"><span data-stu-id="90650-265">You might need toohit `enter` toorevive hello terminal.</span></span> <span data-ttu-id="90650-266">Ardından hello Oracle otomatik Depolama Yönetimi yapılandırma Yardımcısı'nı başlatın:</span><span class="sxs-lookup"><span data-stu-id="90650-266">Then launch hello Oracle Automated Storage Management Configuration Assistant:</span></span>

   ```bash
   cd /u01/app/grid/product/12.1.0/grid/bin
   ./asmca
   ```

   <span data-ttu-id="90650-267">Oracle ASM yapılandırma Yardımcısı'nı açar.</span><span class="sxs-lookup"><span data-stu-id="90650-267">Oracle ASM Configuration Assistant opens.</span></span>

2. <span data-ttu-id="90650-268">Merhaba, **yapılandırma ASM: Disk gruplarının** iletişim kutusunda, hello `Create` düğmesine tıklayın ve ardından `Show Advanced Options`.</span><span class="sxs-lookup"><span data-stu-id="90650-268">In hello **Configure ASM: Disk Groups** dialog box, click hello `Create` button, and then click `Show Advanced Options`.</span></span>

3. <span data-ttu-id="90650-269">Merhaba, **Disk grubu oluşturma** iletişim kutusunda:</span><span class="sxs-lookup"><span data-stu-id="90650-269">In hello **Create Disk Group** dialog box:</span></span>

   - <span data-ttu-id="90650-270">Merhaba disk grubu adı girin **veri**.</span><span class="sxs-lookup"><span data-stu-id="90650-270">Enter hello disk group name **DATA**.</span></span>
   - <span data-ttu-id="90650-271">Altında **üye diskleri Seç**seçin **ORCL_DATA** ve **ORCL_DATA1**.</span><span class="sxs-lookup"><span data-stu-id="90650-271">Under **Select Member Disks**, select **ORCL_DATA** and **ORCL_DATA1**.</span></span>
   - <span data-ttu-id="90650-272">Altında **ayırma birimi boyutu**seçin **4**.</span><span class="sxs-lookup"><span data-stu-id="90650-272">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="90650-273">Tıklatın `ok` toocreate hello disk grubu.</span><span class="sxs-lookup"><span data-stu-id="90650-273">Click `ok` toocreate hello disk group.</span></span>
   - <span data-ttu-id="90650-274">Tıklatın `ok` tooclose hello onay penceresi.</span><span class="sxs-lookup"><span data-stu-id="90650-274">Click `ok` tooclose hello confirmation window.</span></span>

   ![Merhaba Disk grubu oluştur iletişim kutusunun ekran görüntüsü](./media/oracle-asm/asm02.png)

4. <span data-ttu-id="90650-276">Merhaba, **yapılandırma ASM: Disk gruplarının** iletişim kutusunda, hello `Create` düğmesine tıklayın ve ardından `Show Advanced Options`.</span><span class="sxs-lookup"><span data-stu-id="90650-276">In hello **Configure ASM: Disk Groups** dialog box, click hello `Create` button, and then click `Show Advanced Options`.</span></span>

5. <span data-ttu-id="90650-277">Merhaba, **Disk grubu oluşturma** iletişim kutusunda:</span><span class="sxs-lookup"><span data-stu-id="90650-277">In hello **Create Disk Group** dialog box:</span></span>

   - <span data-ttu-id="90650-278">Merhaba disk grubu adı girin **FRA**.</span><span class="sxs-lookup"><span data-stu-id="90650-278">Enter hello disk group name **FRA**.</span></span>
   - <span data-ttu-id="90650-279">Altında **artıklık**seçin **dış (hiçbiri)**.</span><span class="sxs-lookup"><span data-stu-id="90650-279">Under **Redundancy**, select **External (none)**.</span></span>
   - <span data-ttu-id="90650-280">Altında **üye diskleri Seç**seçin **ORCL_FRA**.</span><span class="sxs-lookup"><span data-stu-id="90650-280">Under **Select Member Disks**, select **ORCL_FRA**.</span></span>
   - <span data-ttu-id="90650-281">Altında **ayırma birimi boyutu**seçin **4**.</span><span class="sxs-lookup"><span data-stu-id="90650-281">Under **Allocation Unit Size**, select **4**.</span></span>
   - <span data-ttu-id="90650-282">Tıklatın `ok` toocreate hello disk grubu.</span><span class="sxs-lookup"><span data-stu-id="90650-282">Click `ok` toocreate hello disk group.</span></span>
   - <span data-ttu-id="90650-283">Tıklatın `ok` tooclose hello onay penceresi.</span><span class="sxs-lookup"><span data-stu-id="90650-283">Click `ok` tooclose hello confirmation window.</span></span>

   ![Merhaba Disk grubu oluştur iletişim kutusunun ekran görüntüsü](./media/oracle-asm/asm04.png)

6. <span data-ttu-id="90650-285">Seçin **çıkış** tooclose ASM yapılandırma Yardımcısı.</span><span class="sxs-lookup"><span data-stu-id="90650-285">Select **Exit** tooclose ASM Configuration Assistant.</span></span>

   ![Ekran görüntüsü hello yapılandırma ASM: çıkış düğmesi Disk gruplar iletişim kutusu](./media/oracle-asm/asm05.png)

## <a name="create-hello-database"></a><span data-ttu-id="90650-287">Merhaba veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="90650-287">Create hello database</span></span>

<span data-ttu-id="90650-288">Oracle veritabanı yazılımını Hello hello Azure Market görüntüsü üzerinde zaten yüklü.</span><span class="sxs-lookup"><span data-stu-id="90650-288">hello Oracle database software is already installed on hello Azure Marketplace image.</span></span> <span data-ttu-id="90650-289">toocreate bir veritabanı, şu adımları tam hello:</span><span class="sxs-lookup"><span data-stu-id="90650-289">toocreate a database, complete hello following steps:</span></span>

1. <span data-ttu-id="90650-290">Kullanıcıların toohello Oracle süper kullanıcı geçin ve günlüğe kaydetme için hello dinleyici başlatılamadı:</span><span class="sxs-lookup"><span data-stu-id="90650-290">Switch users toohello Oracle superuser, and then initialize hello listener for logging:</span></span>

   ```bash
   su - oracle
   cd /u01/app/oracle/product/12.1.0/dbhome_1/bin
   ./dbca
   ```
   <span data-ttu-id="90650-291">Veritabanı yapılandırma Yardımcısı'nı açar.</span><span class="sxs-lookup"><span data-stu-id="90650-291">Database Configuration Assistant opens.</span></span>

2. <span data-ttu-id="90650-292">Merhaba üzerinde **veritabanı işlemi** sayfasında, `Create Database`.</span><span class="sxs-lookup"><span data-stu-id="90650-292">On hello **Database Operation** page, click `Create Database`.</span></span>

3. <span data-ttu-id="90650-293">Merhaba üzerinde **oluşturma modu** sayfa:</span><span class="sxs-lookup"><span data-stu-id="90650-293">On hello **Creation Mode** page:</span></span>

   - <span data-ttu-id="90650-294">Merhaba veritabanı için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="90650-294">Enter a name for hello database.</span></span>
   - <span data-ttu-id="90650-295">İçin **depolama türü**, olun **otomatik Depolama Yönetimi (ASM)** seçilir.</span><span class="sxs-lookup"><span data-stu-id="90650-295">For **Storage Type**, ensure **Automatic Storage Management (ASM)** is selected.</span></span>
   - <span data-ttu-id="90650-296">İçin **veritabanı dosya konumu**, hello varsayılan kullanmak ASM önerilen konum.</span><span class="sxs-lookup"><span data-stu-id="90650-296">For **Database Files Location**, use hello default ASM suggested location.</span></span>
   - <span data-ttu-id="90650-297">İçin **Hızlı Kurtarma alanında**, hello varsayılan kullanmak ASM önerilen konum.</span><span class="sxs-lookup"><span data-stu-id="90650-297">For **Fast Recovery Area**, use hello default ASM suggested location.</span></span>
   - <span data-ttu-id="90650-298">yazın bir **yönetici parolasını** ve **parolayı onaylayın**.</span><span class="sxs-lookup"><span data-stu-id="90650-298">type in an **Administrative Password** and **confirm password**.</span></span>
   - <span data-ttu-id="90650-299">olun `create as container database` seçilir.</span><span class="sxs-lookup"><span data-stu-id="90650-299">ensure `create as container database` is selected.</span></span>
   - <span data-ttu-id="90650-300">yazın bir `pluggable database name` değeri.</span><span class="sxs-lookup"><span data-stu-id="90650-300">type in a `pluggable database name` value.</span></span>

4. <span data-ttu-id="90650-301">Merhaba üzerinde **Özet** sayfasında, seçtiğiniz ayarları gözden geçirin ve ardından `Finish` toocreate hello veritabanı.</span><span class="sxs-lookup"><span data-stu-id="90650-301">On hello **Summary** page, review your selected settings, and then click `Finish` toocreate hello database.</span></span>

   ![Merhaba Özet sayfasının ekran görüntüsü](./media/oracle-asm/createdb03.png)

5. <span data-ttu-id="90650-303">Merhaba veritabanı oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="90650-303">hello Database has been created.</span></span> <span data-ttu-id="90650-304">Merhaba üzerinde **son** sayfasında, bu veritabanı toounlock ek hesapları toouse seçeneği ve hello parolalarını değiştirme hello sahip.</span><span class="sxs-lookup"><span data-stu-id="90650-304">On hello **Finish** page, you have hello option toounlock additional accounts toouse this database and change hello passwords.</span></span> <span data-ttu-id="90650-305">Bunu toodo istiyorsanız seçin **parola yönetimi** -Aksi takdirde tıklayın `close`.</span><span class="sxs-lookup"><span data-stu-id="90650-305">If you wish toodo so, select **Password Management** - otherwise click on `close`.</span></span>

## <a name="delete-hello-vm"></a><span data-ttu-id="90650-306">Merhaba VM silme</span><span class="sxs-lookup"><span data-stu-id="90650-306">Delete hello VM</span></span>

<span data-ttu-id="90650-307">Oracle otomatik Depolama Yönetimi, hello Oracle DB hello Azure Market görüntüsünden üzerinde başarıyla yapılandırdınız.</span><span class="sxs-lookup"><span data-stu-id="90650-307">You have successfully configured Oracle Automated Storage Management on hello Oracle DB image from hello Azure Marketplace.</span></span>  <span data-ttu-id="90650-308">Bu VM artık gerektiğinde komutu tooremove hello kaynak grubu, VM ve tüm ilgili kaynaklar aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="90650-308">When you no longer need this VM, you can use hello following command tooremove hello resource group, VM, and all related resources:</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="90650-309">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="90650-309">Next steps</span></span>

[<span data-ttu-id="90650-310">Öğretici: Oracle DataGuard yapılandırın</span><span class="sxs-lookup"><span data-stu-id="90650-310">Tutorial: Configure Oracle DataGuard</span></span>](configure-oracle-dataguard.md)

[<span data-ttu-id="90650-311">Öğretici: Oracle GoldenGate yapılandırın</span><span class="sxs-lookup"><span data-stu-id="90650-311">Tutorial: Configure Oracle GoldenGate</span></span>](Configure-oracle-golden-gate.md)

<span data-ttu-id="90650-312">Gözden geçirme [bir Oracle DB Mimari](oracle-design.md)</span><span class="sxs-lookup"><span data-stu-id="90650-312">Review [Architect an Oracle DB](oracle-design.md)</span></span>
