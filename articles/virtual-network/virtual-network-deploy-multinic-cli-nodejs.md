---
title: "birden çok NIC - Azure CLI 1.0 ile VM aaaCreate | Microsoft Docs"
description: "Nasıl toocreate kullanarak birden çok NIC ile VM hello Azure CLI 1.0 öğrenin."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 8e906a4b-8583-4a97-9416-ee34cfa09a98
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 07c660b632bcdc004365a6f910ecf8a5c13cbc6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-hello-azure-cli-10"></a><span data-ttu-id="5541e-103">Bir VM ile birden çok NIC hello Azure CLI 1.0 kullanarak oluşturma</span><span class="sxs-lookup"><span data-stu-id="5541e-103">Create a VM with multiple NICs using hello Azure CLI 1.0</span></span>

[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="5541e-104">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="5541e-104">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="5541e-105">Bu makalede, kullanarak yer almaktadır hello yerine çoğu yeni dağıtımlar için Microsoft önerir hello Resource Manager dağıtım modeli [Klasik dağıtım modeli](virtual-network-deploy-multinic-classic-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5541e-105">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-cli.md).</span></span>
>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="5541e-106">Merhaba aşağıdaki adımları kullanın adlı bir kaynak grubu *IaaSStory* hello WEB sunucuları ve bir kaynak grubu için adlı *IaaSStory arka uç* hello DB sunucuları için.</span><span class="sxs-lookup"><span data-stu-id="5541e-106">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span> <span data-ttu-id="5541e-107">Hello Azure CLI 1.0 (Bu makalede) veya hello kullanarak bu görevi tamamlayabilirsiniz [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5541e-107">You can complete this task using hello Azure CLI 1.0 (this article) or hello [Azure CLI 2.0](virtual-network-deploy-static-pip-arm-cli.md).</span></span> <span data-ttu-id="5541e-108">Merhaba değerleri "" Merhaba senaryodan ayarlarla kaynakları izleyin hello adımları hello değişkenleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5541e-108">hello values in "" for hello variables in hello steps that follow create resources with settings from hello scenario.</span></span> <span data-ttu-id="5541e-109">Ortamınız için uygun şekilde Hello değerlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="5541e-109">Change hello values, as appropriate, for your environment.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5541e-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="5541e-110">Prerequisites</span></span>
<span data-ttu-id="5541e-111">DB sunucuları hello oluşturabilmeniz için önce toocreate hello gerekir *IaaSStory* hello gereken tüm kaynakların bu senaryo için kaynak grubuyla.</span><span class="sxs-lookup"><span data-stu-id="5541e-111">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="5541e-112">Bu kaynaklar toocreate tamamlamak hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="5541e-112">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="5541e-113">Çok gidin[hello şablon sayfasına](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="5541e-113">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="5541e-114">Merhaba şablon sayfasındaki sağ toohello **üst kaynak grubu**, tıklatın **tooAzure dağıtmak**.</span><span class="sxs-lookup"><span data-stu-id="5541e-114">In hello template page, toohello right of **Parent resource group**, click **Deploy tooAzure**.</span></span>
3. <span data-ttu-id="5541e-115">Gerekirse, hello parametre değerlerini değiştirmek sonra hello Azure Önizleme portalı toodeploy hello kaynak grubunda hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="5541e-115">If needed, change hello parameter values, then follow hello steps in hello Azure preview portal toodeploy hello resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5541e-116">Depolama hesabı adları benzersiz olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="5541e-116">Make sure your storage account names are unique.</span></span> <span data-ttu-id="5541e-117">Azure üzerinde yinelenen depolama hesabı adları sahip olamaz.</span><span class="sxs-lookup"><span data-stu-id="5541e-117">You cannot have duplicate storage account names in Azure.</span></span>
> 

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a><span data-ttu-id="5541e-118">Arka uç VM'ler Hello oluşturma</span><span class="sxs-lookup"><span data-stu-id="5541e-118">Create hello back-end VMs</span></span>
<span data-ttu-id="5541e-119">Merhaba arka uç VM'ler kaynakları aşağıdaki hello hello oluşturulmasına bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="5541e-119">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="5541e-120">**Veri diskleri için depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="5541e-120">**Storage account for data disks**.</span></span> <span data-ttu-id="5541e-121">Daha iyi performans için premium depolama hesabı gerektirir katı hal sürücüsü (SSD) teknolojisi hello veritabanı sunucularında hello veri diski kullanır.</span><span class="sxs-lookup"><span data-stu-id="5541e-121">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="5541e-122">Emin hello toosupport premium depolama dağıttığınız Azure konumu olun.</span><span class="sxs-lookup"><span data-stu-id="5541e-122">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="5541e-123">**NIC**.</span><span class="sxs-lookup"><span data-stu-id="5541e-123">**NICs**.</span></span> <span data-ttu-id="5541e-124">Her VM veritabanı erişimi için iki NIC gerekir ve yönetimi için bir tane.</span><span class="sxs-lookup"><span data-stu-id="5541e-124">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="5541e-125">**Kullanılabilirlik kümesi**.</span><span class="sxs-lookup"><span data-stu-id="5541e-125">**Availability set**.</span></span> <span data-ttu-id="5541e-126">Tüm veritabanı sunucuları tooa tek kullanılabilirlik kümesi eklenir, tooensure hello VM'ler en az biri hazır ve çalışır bakımı sırasında.</span><span class="sxs-lookup"><span data-stu-id="5541e-126">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="5541e-127">1. adım - kodunuzu Başlat</span><span class="sxs-lookup"><span data-stu-id="5541e-127">Step 1 - Start your script</span></span>
<span data-ttu-id="5541e-128">Kullanılan hello tam bash komut dosyası indirebilirsiniz [burada](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-cli.sh).</span><span class="sxs-lookup"><span data-stu-id="5541e-128">You can download hello full bash script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-cli.sh).</span></span> <span data-ttu-id="5541e-129">Ortamınızdaki toochange hello betik toowork Hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="5541e-129">Follow hello steps below toochange hello script toowork in your environment.</span></span>

1. <span data-ttu-id="5541e-130">Değiştirme hello değişkenlerin değerleri yukarıda dağıtılmış varolan kaynak grubunuz göre hello aşağıdaki [Önkoşullar](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="5541e-130">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```azurecli
    existingRGName="IaaSStory"
    location="westus"
    vnetName="WTestVNet"
    backendSubnetName="BackEnd"
    remoteAccessNSGName="NSG-RemoteAccess"
    ```
2. <span data-ttu-id="5541e-131">Merhaba değerlerini değiştirin arka uç dağıtımınız için toouse istediğiniz hello değişkenleri aşağıdaki hello değerlerine göre.</span><span class="sxs-lookup"><span data-stu-id="5541e-131">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

    ```azurecli
    backendRGName="IaaSStory-Backend"
    prmStorageAccountName="wtestvnetstorageprm"
    avSetName="ASDB"
    vmSize="Standard_DS3"
    diskSize=127
    publisher="Canonical"
    offer="UbuntuServer"
    sku="14.04.2-LTS"
    version="latest"
    vmNamePrefix="DB"
    osDiskName="osdiskdb"
    dataDiskName="datadisk"
    nicNamePrefix="NICDB"
    ipAddressPrefix="192.168.2."
    username='adminuser'
    password='adminP@ssw0rd'
    numberOfVMs=2
    ```

3. <span data-ttu-id="5541e-132">Merhaba Hello Kimliği almak `BackEnd` burada hello VM'ler oluşturulacak alt ağ.</span><span class="sxs-lookup"><span data-stu-id="5541e-132">Retrieve hello ID for hello `BackEnd` subnet where hello VMs will be created.</span></span> <span data-ttu-id="5541e-133">Merhaba NIC'ler ilişkili toobe toothis alt farklı kaynak grubunda olduğundan bu toodo gerekir.</span><span class="sxs-lookup"><span data-stu-id="5541e-133">You need toodo this since hello NICs toobe associated toothis subnet are in a different resource group.</span></span>

    ```azurecli
    subnetId="$(azure network vnet subnet show --resource-group $existingRGName \
            --vnet-name $vnetName \
            --name $backendSubnetName|grep Id)"
    subnetId=${subnetId#*/}
    ```

   > [!TIP]
   > <span data-ttu-id="5541e-134">Merhaba kullanımlar yukarıda ilk komut [grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html) ve [dize düzenlemesi](http://tldp.org/LDP/abs/html/string-manipulation.html) (daha açık belirtmek gerekirse substring kaldırma).</span><span class="sxs-lookup"><span data-stu-id="5541e-134">hello first command above uses [grep](http://tldp.org/LDP/Bash-Beginners-Guide/html/sect_04_02.html) and [string manipulation](http://tldp.org/LDP/abs/html/string-manipulation.html) (more specifically, substring removal).</span></span>
   >

4. <span data-ttu-id="5541e-135">Merhaba Hello Kimliği almak `NSG-RemoteAccess` NSG.</span><span class="sxs-lookup"><span data-stu-id="5541e-135">Retrieve hello ID for hello `NSG-RemoteAccess` NSG.</span></span> <span data-ttu-id="5541e-136">NSG olan farklı bir kaynak grubu içinde toothis Hello NIC'ler toobe ilişkili olduğundan bu toodo gerekir.</span><span class="sxs-lookup"><span data-stu-id="5541e-136">You need toodo this since hello NICs toobe associated toothis NSG are in a different resource group.</span></span>

    ```azurecli
    nsgId="$(azure network nsg show --resource-group $existingRGName \
        --name $remoteAccessNSGName|grep Id)"
        nsgId=${nsgId#*/}
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="5541e-137">2. adım - Vm'leriniz için gerekli kaynakları oluşturma</span><span class="sxs-lookup"><span data-stu-id="5541e-137">Step 2 - Create necessary resources for your VMs</span></span>

1. <span data-ttu-id="5541e-138">Tüm arka uç kaynaklar için yeni bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5541e-138">Create a new resource group for all backend resources.</span></span> <span data-ttu-id="5541e-139">Bildirim hello hello kullanımını `$backendRGName` hello kaynak grubu adı için değişken ve `$location` hello Azure bölgesi için.</span><span class="sxs-lookup"><span data-stu-id="5541e-139">Notice hello use of hello `$backendRGName` variable for hello resource group name, and `$location` for hello Azure region.</span></span>

    ```azurecli
    azure group create $backendRGName $location
    ```

2. <span data-ttu-id="5541e-140">Premium depolama hesabı hello işletim sistemi için ve veri diskleri toobe sizin tarafından VM'ler kullanılan oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5541e-140">Create a premium storage account for hello OS and data disks toobe used by yours VMs.</span></span>

    ```azurecli
    azure storage account create $prmStorageAccountName \
        --resource-group $backendRGName \
        --location $location \
        --type PLRS
    ```

3. <span data-ttu-id="5541e-141">Kullanılabilirlik Merhaba VM'ler kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5541e-141">Create an availability set for hello VMs.</span></span>

    ```azurecli
    azure availset create --resource-group $backendRGName \
        --location $location \
        --name $avSetName
    ```

### <a name="step-3---create-hello-nics-and-back-end-vms"></a><span data-ttu-id="5541e-142">3. adım - hello NIC ve arka uç VM'ler oluşturma</span><span class="sxs-lookup"><span data-stu-id="5541e-142">Step 3 - Create hello NICs and back-end VMs</span></span>

1. <span data-ttu-id="5541e-143">Döngü toocreate üzerinde hello göre birden çok VM Başlat `numberOfVMs` değişkenleri.</span><span class="sxs-lookup"><span data-stu-id="5541e-143">Start a loop toocreate multiple VMs, based on hello `numberOfVMs` variables.</span></span>

    ```azurecli
    for ((suffixNumber=1;suffixNumber<=numberOfVMs;suffixNumber++));
    do
    ```

2. <span data-ttu-id="5541e-144">Her VM için veritabanı erişimi için bir NIC oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5541e-144">For each VM, create a NIC for database access.</span></span>

    ```azurecli
    nic1Name=$nicNamePrefix$suffixNumber-DA
    x=$((suffixNumber+3))
    ipAddress1=$ipAddressPrefix$x
    azure network nic create --name $nic1Name \
        --resource-group $backendRGName \
        --location $location \
        --private-ip-address $ipAddress1 \
        --subnet-id $subnetId
    ```

3. <span data-ttu-id="5541e-145">Her VM için uzaktan erişim için bir NIC oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5541e-145">For each VM, create a NIC for remote access.</span></span> <span data-ttu-id="5541e-146">Bildirim hello `--network-security-group` parametresi, kullanılan tooassociate hello NIC tooan NSG.</span><span class="sxs-lookup"><span data-stu-id="5541e-146">Notice hello `--network-security-group` parameter, used tooassociate hello NIC tooan NSG.</span></span>

    ```azurecli
    nic2Name=$nicNamePrefix$suffixNumber-RA
    x=$((suffixNumber+53))
    ipAddress2=$ipAddressPrefix$x
    azure network nic create --name $nic2Name \
        --resource-group $backendRGName \
        --location $location \
        --private-ip-address $ipAddress2 \
        --subnet-id $subnetId $vnetName \
        --network-security-group-id $nsgId
    ```

4. <span data-ttu-id="5541e-147">Merhaba VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5541e-147">Create hello VM.</span></span>

    ```azurecli
    azure vm create --resource-group $backendRGName \
        --name $vmNamePrefix$suffixNumber \
        --location $location \
        --vm-size $vmSize \
        --subnet-id $subnetId \
        --availset-name $avSetName \
        --nic-names $nic1Name,$nic2Name \
        --os-type linux \
        --image-urn $publisher:$offer:$sku:$version \
        --storage-account-name $prmStorageAccountName \
        --storage-account-container-name vhds \
        --os-disk-vhd $osDiskName$suffixNumber.vhd \
        --admin-username $username \
        --admin-password $password
    ```

5. <span data-ttu-id="5541e-148">Her bir VM ile Merhaba iki veri diskleri ve son hello döngü oluşturma `done` komutu.</span><span class="sxs-lookup"><span data-stu-id="5541e-148">For each VM, create two data disks, and end hello loop with hello `done` command.</span></span>

    ```azurecli
    azure vm disk attach-new --resource-group $backendRGName \
        --vm-name $vmNamePrefix$suffixNumber \
        --storage-account-name $prmStorageAccountName \
        --storage-account-container-name vhds \
        --vhd-name $dataDiskName$suffixNumber-1.vhd \
        --size-in-gb $diskSize \
        --lun 0

    azure vm disk attach-new --resource-group $backendRGName \
        --vm-name $vmNamePrefix$suffixNumber \        
        --storage-account-name $prmStorageAccountName \
        --storage-account-container-name vhds \
        --vhd-name $dataDiskName$suffixNumber-2.vhd \
        --size-in-gb $diskSize \
        --lun 1
        done
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="5541e-149">Adım 4 - çalışma hello komut dosyası</span><span class="sxs-lookup"><span data-stu-id="5541e-149">Step 4 - Run hello script</span></span>
<span data-ttu-id="5541e-150">İndirilen ve hello betik hello betik toocreate hello geri çalıştırmak gereksinimlerinize göre değişti birden çok NIC içeren veritabanı VM'ler sonlandırın.</span><span class="sxs-lookup"><span data-stu-id="5541e-150">Now that you downloaded and changed hello script based on your needs, run hello script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="5541e-151">Komut dosyanızı kaydedin ve çalıştırın, **Bash** terminal.</span><span class="sxs-lookup"><span data-stu-id="5541e-151">Save your script and run it from your **Bash** terminal.</span></span> <span data-ttu-id="5541e-152">Merhaba ilk çıktısı, aşağıda gösterildiği gibi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="5541e-152">You will see hello initial output, as shown below.</span></span>
   
        info:    Executing command group create
        info:    Getting resource group IaaSStory-Backend
        info:    Creating resource group IaaSStory-Backend
        info:    Created resource group IaaSStory-Backend
        data:    Id:                  /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend
        data:    Name:                IaaSStory-Backend
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK
        info:    Executing command storage account create
        info:    Creating storage account
        info:    storage account create command OK
        info:    Executing command availset create
        info:    Looking up hello availability set "ASDB"
        info:    Creating availability set "ASDB"
        info:    availset create command OK
        info:    Executing command network nic create
        info:    Looking up hello network interface "NICDB1-DA"
        info:    Creating network interface "NICDB1-DA"
        info:    Looking up hello network interface "NICDB1-DA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB1-DA
        data:    Name                            : NICDB1-DA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command network nic create
        info:    Looking up hello network interface "NICDB1-RA"
        info:    Creating network interface "NICDB1-RA"
        info:    Looking up hello network interface "NICDB1-RA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB1-RA
        data:    Name                            : NICDB1-RA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    Network security group          : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/networkSecurityGroups/NSG-RemoteAccess
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.54
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command vm create
        info:    Looking up hello VM "DB1"
        info:    Using hello VM Size "Standard_DS3"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    Looking up hello availability set "ASDB"
        info:    Found an Availability set "ASDB"
        info:    Looking up hello NIC "NICDB1-DA"
        info:    Looking up hello NIC "NICDB1-RA"
        info:    Creating VM "DB1"
2. <span data-ttu-id="5541e-153">Birkaç dakika sonra hello yürütme sona erer ve hello rest aşağıda gösterildiği gibi hello çıktısını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="5541e-153">After a few minutes, hello execution will end and you will see hello rest of hello output as shown below.</span></span>
   
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB1"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk1-1.vhd
        info:    Updating VM "DB1"
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB1"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk1-2.vhd
        info:    Updating VM "DB1"
        info:    vm disk attach-new command OK
        info:    Executing command network nic create
        info:    Looking up hello network interface "NICDB2-DA"
        info:    Creating network interface "NICDB2-DA"
        info:    Looking up hello network interface "NICDB2-DA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB2-DA
        data:    Name                            : NICDB2-DA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.5
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command network nic create
        info:    Looking up hello network interface "NICDB2-RA"
        info:    Creating network interface "NICDB2-RA"
        info:    Looking up hello network interface "NICDB2-RA"
        data:    Id                              : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend/providers/Microsoft.Network/networkInterfaces/NICDB2-RA
        data:    Name                            : NICDB2-RA
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    Network security group          : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/networkSecurityGroups/NSG-RemoteAccess
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 192.168.2.55
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/BackEnd
        data:
        info:    network nic create command OK
        info:    Executing command vm create
        info:    Looking up hello VM "DB2"
        info:    Using hello VM Size "Standard_DS3"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    Looking up hello availability set "ASDB"
        info:    Found an Availability set "ASDB"
        info:    Looking up hello NIC "NICDB2-DA"
        info:    Looking up hello NIC "NICDB2-RA"
        info:    Creating VM "DB2"
        info:    vm create command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB2"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk2-1.vhd
        info:    Updating VM "DB2"
        info:    vm disk attach-new command OK
        info:    Executing command vm disk attach-new
        info:    Looking up hello VM "DB2"
        info:    Looking up hello storage account wtestvnetstorageprm
        info:    New data disk location: https://wtestvnetstorageprm.blob.core.windows.net/vhds/datadisk2-2.vhd
        info:    Updating VM "DB2"
        info:    vm disk attach-new command OK

