---
title: "birden çok NIC - Azure PowerShell ile bir VM aaaCreate | Microsoft Docs"
description: "Bilgi nasıl toocreate PowerShell kullanarak birden çok NIC ile VM."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 88880483-8f9e-4eeb-b783-64b8613407d9
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 507a413510da3ee69aefed324977ee40e442268b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-powershell"></a><span data-ttu-id="7b457-103">PowerShell kullanarak birden çok NIC ile VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="7b457-103">Create a VM with multiple NICs using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7b457-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7b457-104">PowerShell</span></span>](virtual-network-deploy-multinic-arm-ps.md)
> * [<span data-ttu-id="7b457-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7b457-105">Azure CLI</span></span>](virtual-network-deploy-multinic-arm-cli.md)
> * [<span data-ttu-id="7b457-106">Şablon</span><span class="sxs-lookup"><span data-stu-id="7b457-106">Template</span></span>](virtual-network-deploy-multinic-arm-template.md)
> * [<span data-ttu-id="7b457-107">PowerShell (Klasik)</span><span class="sxs-lookup"><span data-stu-id="7b457-107">PowerShell (Classic)</span></span>](virtual-network-deploy-multinic-classic-ps.md)
> * [<span data-ttu-id="7b457-108">Azure CLI (Klasik)</span><span class="sxs-lookup"><span data-stu-id="7b457-108">Azure CLI (Classic)</span></span>](virtual-network-deploy-multinic-classic-cli.md)

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="7b457-109">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7b457-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="7b457-110">Bu makalede, kullanarak yer almaktadır hello yerine çoğu yeni dağıtımlar için Microsoft önerir hello Resource Manager dağıtım modeli [Klasik dağıtım modeli](virtual-network-deploy-multinic-classic-ps.md).</span><span class="sxs-lookup"><span data-stu-id="7b457-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello [classic deployment model](virtual-network-deploy-multinic-classic-ps.md).</span></span>
>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="7b457-111">Merhaba aşağıdaki adımları kullanın adlı bir kaynak grubu *IaaSStory* hello WEB sunucuları ve bir kaynak grubu için adlı *IaaSStory arka uç* hello DB sunucuları için.</span><span class="sxs-lookup"><span data-stu-id="7b457-111">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b457-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7b457-112">Prerequisites</span></span>
<span data-ttu-id="7b457-113">DB sunucuları hello oluşturabilmeniz için önce toocreate hello gerekir *IaaSStory* hello gereken tüm kaynakların bu senaryo için kaynak grubuyla.</span><span class="sxs-lookup"><span data-stu-id="7b457-113">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="7b457-114">Bu kaynaklar toocreate tamamlamak hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="7b457-114">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="7b457-115">Çok gidin[hello şablon sayfasına](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="7b457-115">Navigate too[hello template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="7b457-116">Merhaba şablon sayfasındaki sağ toohello **üst kaynak grubu**, tıklatın **tooAzure dağıtmak**.</span><span class="sxs-lookup"><span data-stu-id="7b457-116">In hello template page, toohello right of **Parent resource group**, click **Deploy tooAzure**.</span></span>
3. <span data-ttu-id="7b457-117">Gerekirse, hello parametre değerlerini değiştirmek sonra hello Azure Önizleme portalı toodeploy hello kaynak grubunda hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="7b457-117">If needed, change hello parameter values, then follow hello steps in hello Azure preview portal toodeploy hello resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7b457-118">Depolama hesabı adları benzersiz olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="7b457-118">Make sure your storage account names are unique.</span></span> <span data-ttu-id="7b457-119">Azure üzerinde yinelenen depolama hesabı adları sahip olamaz.</span><span class="sxs-lookup"><span data-stu-id="7b457-119">You cannot have duplicate storage account names in Azure.</span></span>
> 

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a><span data-ttu-id="7b457-120">Arka uç VM'ler Hello oluşturma</span><span class="sxs-lookup"><span data-stu-id="7b457-120">Create hello back-end VMs</span></span>
<span data-ttu-id="7b457-121">Merhaba arka uç VM'ler kaynakları aşağıdaki hello hello oluşturulmasına bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="7b457-121">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="7b457-122">**Veri diskleri için depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="7b457-122">**Storage account for data disks**.</span></span> <span data-ttu-id="7b457-123">Daha iyi performans için premium depolama hesabı gerektirir katı hal sürücüsü (SSD) teknolojisi hello veritabanı sunucularında hello veri diski kullanır.</span><span class="sxs-lookup"><span data-stu-id="7b457-123">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="7b457-124">Emin hello toosupport premium depolama dağıttığınız Azure konumu olun.</span><span class="sxs-lookup"><span data-stu-id="7b457-124">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="7b457-125">**NIC**.</span><span class="sxs-lookup"><span data-stu-id="7b457-125">**NICs**.</span></span> <span data-ttu-id="7b457-126">Her VM veritabanı erişimi için iki NIC gerekir ve yönetimi için bir tane.</span><span class="sxs-lookup"><span data-stu-id="7b457-126">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="7b457-127">**Kullanılabilirlik kümesi**.</span><span class="sxs-lookup"><span data-stu-id="7b457-127">**Availability set**.</span></span> <span data-ttu-id="7b457-128">Tüm veritabanı sunucuları tooa tek kullanılabilirlik kümesi eklenir, tooensure hello VM'ler en az biri hazır ve çalışır bakımı sırasında.</span><span class="sxs-lookup"><span data-stu-id="7b457-128">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>  

### <a name="step-1---start-your-script"></a><span data-ttu-id="7b457-129">1. adım - kodunuzu Başlat</span><span class="sxs-lookup"><span data-stu-id="7b457-129">Step 1 - Start your script</span></span>
<span data-ttu-id="7b457-130">Kullanılan hello tam PowerShell komut dosyası indirebilirsiniz [burada](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="7b457-130">You can download hello full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-ps.ps1).</span></span> <span data-ttu-id="7b457-131">Ortamınızdaki toochange hello betik toowork Hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="7b457-131">Follow hello steps below toochange hello script toowork in your environment.</span></span>

1. <span data-ttu-id="7b457-132">Değiştirme hello değişkenlerin değerleri yukarıda dağıtılmış varolan kaynak grubunuz göre hello aşağıdaki [Önkoşullar](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="7b457-132">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $existingRGName        = "IaaSStory"
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    $remoteAccessNSGName   = "NSG-RemoteAccess"
    $stdStorageAccountName = "wtestvnetstoragestd"
    ```

2. <span data-ttu-id="7b457-133">Merhaba değerlerini değiştirin arka uç dağıtımınız için toouse istediğiniz hello değişkenleri aşağıdaki hello değerlerine göre.</span><span class="sxs-lookup"><span data-stu-id="7b457-133">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

    ```powershell
    $backendRGName         = "IaaSStory-Backend"
    $prmStorageAccountName = "wtestvnetstorageprm"
    $avSetName             = "ASDB"
    $vmSize                = "Standard_DS3"
    $publisher             = "MicrosoftSQLServer"
    $offer                 = "SQL2014SP1-WS2012R2"
    $sku                   = "Standard"
    $version               = "latest"
    $vmNamePrefix          = "DB"
    $osDiskPrefix          = "osdiskdb"
    $dataDiskPrefix        = "datadisk"
    $diskSize               = "120"    
    $nicNamePrefix         = "NICDB"
    $ipAddressPrefix       = "192.168.2."
    $numberOfVMs           = 2
    ```
3. <span data-ttu-id="7b457-134">Dağıtımınız için gerekli hello mevcut kaynakları alır.</span><span class="sxs-lookup"><span data-stu-id="7b457-134">Retrieve hello existing resources needed for your deployment.</span></span>

    ```powershell
    $vnet                  = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $existingRGName
    $backendSubnet         = $vnet.Subnets|?{$_.Name -eq $backendSubnetName}
    $remoteAccessNSG       = Get-AzureRmNetworkSecurityGroup -Name $remoteAccessNSGName -ResourceGroupName $existingRGName
    $stdStorageAccount     = Get-AzureRmStorageAccount -Name $stdStorageAccountName -ResourceGroupName $existingRGName
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="7b457-135">2. adım - Vm'leriniz için gerekli kaynakları oluşturma</span><span class="sxs-lookup"><span data-stu-id="7b457-135">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="7b457-136">Tüm VM'ler için kullanılabilirlik kümesi ve toocreate yeni bir kaynak grubu olan hello veri diskleri için bir depolama hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b457-136">You need toocreate a new resource group, a storage account for hello data disks, and an availability set for all VMs.</span></span> <span data-ttu-id="7b457-137">Seçecek her VM için hello yerel yönetici hesabı kimlik bilgileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b457-137">You alos need hello local administrator account credentials for each VM.</span></span> <span data-ttu-id="7b457-138">Bu kaynaklar toocreate yürütme hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="7b457-138">toocreate these resources, execute hello following steps.</span></span>

1. <span data-ttu-id="7b457-139">Yeni bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7b457-139">Create a new resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name $backendRGName -Location $location
    ```
2. <span data-ttu-id="7b457-140">Yukarıda oluşturduğunuz hello kaynak grubunda yeni bir premium depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7b457-140">Create a new premium storage account in hello resource group created above.</span></span>

    ```powershell
    $prmStorageAccount = New-AzureRmStorageAccount -Name $prmStorageAccountName `
    -ResourceGroupName $backendRGName -Type Premium_LRS -Location $location
    ```
3. <span data-ttu-id="7b457-141">Yeni bir kullanılabilirlik kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7b457-141">Create a new availability set.</span></span>

    ```powershell
    $avSet = New-AzureRmAvailabilitySet -Name $avSetName -ResourceGroupName $backendRGName -Location $location
    ```
4. <span data-ttu-id="7b457-142">Merhaba yerel yönetici hesabı kimlik bilgileri toobe her VM için kullanılan alın.</span><span class="sxs-lookup"><span data-stu-id="7b457-142">Get hello local administrator account credentials toobe used for each VM.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Type hello name and password for hello local administrator account."
    ```

### <a name="step-3---create-hello-nics-and-back-end-vms"></a><span data-ttu-id="7b457-143">3. adım - hello NIC ve arka uç VM'ler oluşturma</span><span class="sxs-lookup"><span data-stu-id="7b457-143">Step 3 - Create hello NICs and back-end VMs</span></span>
<span data-ttu-id="7b457-144">Ve oluşturma gibi birçok VM gerekli NIC ve sanal makineleri hello döngü içinde hello gibi bir döngü toocreate toouse gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b457-144">You need toouse a loop toocreate as many VMs as you want, and create hello necessary NICs and VMs within hello loop.</span></span> <span data-ttu-id="7b457-145">toocreate hello NIC ve sanal makineleri, aşağıdaki adımları hello yürütün.</span><span class="sxs-lookup"><span data-stu-id="7b457-145">toocreate hello NICs and VMs, execute hello following steps.</span></span>

1. <span data-ttu-id="7b457-146">Başlangıç bir `for` döngü toorepeat hello komutların toocreate VM iki NIC gerektiği gibi birçok kez hello hello değerine bağlı olarak `$numberOfVMs` değişkeni.</span><span class="sxs-lookup"><span data-stu-id="7b457-146">Start a `for` loop toorepeat hello commands toocreate a VM and two NICs as many times as necessary, based on hello value of hello `$numberOfVMs` variable.</span></span>
   
    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="7b457-147">NIC veritabanı erişimi için kullanılan hello oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7b457-147">Create hello NIC used for database access.</span></span>

    ```powershell
    $nic1Name = $nicNamePrefix + $suffixNumber + "-DA"
    $ipAddress1 = $ipAddressPrefix + ($suffixNumber + 3)
    $nic1 = New-AzureRmNetworkInterface -Name $nic1Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress1
    ```

3. <span data-ttu-id="7b457-148">NIC uzaktan erişim için kullanılan hello oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7b457-148">Create hello NIC used for remote access.</span></span> <span data-ttu-id="7b457-149">Nasıl bir ilişkili NSG tooit bu NIC'ye sahiptir dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="7b457-149">Notice how this NIC has an NSG associated tooit.</span></span>

    ```powershell
    $nic2Name = $nicNamePrefix + $suffixNumber + "-RA"
    $ipAddress2 = $ipAddressPrefix + (53 + $suffixNumber)
    $nic2 = New-AzureRmNetworkInterface -Name $nic2Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress2 `
    -NetworkSecurityGroupId $remoteAccessNSG.Id
    ```

4. <span data-ttu-id="7b457-150">Oluşturma `vmConfig` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="7b457-150">Create `vmConfig` object.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize -AvailabilitySetId $avSet.Id
    ```

5. <span data-ttu-id="7b457-151">VM başına iki veri diski oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7b457-151">Create two data disks per VM.</span></span> <span data-ttu-id="7b457-152">Merhaba veri diskleri daha önce oluşturduğunuz hello premium storage hesabında olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="7b457-152">Notice that hello data disks are in hello premium storage account created earlier.</span></span>

    ```powershell
    $dataDisk1Name = $vmName + "-" + $osDiskPrefix + "-1"
    $data1VhdUri = $prmStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $dataDisk1Name + ".vhd"
    Add-AzureRmVMDataDisk -VM $vmConfig -Name $dataDisk1Name -DiskSizeInGB $diskSize `
    -VhdUri $data1VhdUri -CreateOption empty -Lun 0

    $dataDisk2Name = $vmName + "-" + $dataDiskPrefix + "-2"
    $data2VhdUri = $prmStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $dataDisk2Name + ".vhd"
    Add-AzureRmVMDataDisk -VM $vmConfig -Name $dataDisk2Name -DiskSizeInGB $diskSize `
    -VhdUri $data2VhdUri -CreateOption empty -Lun 1
    ```

6. <span data-ttu-id="7b457-153">Merhaba işletim sistemi ve VM hello için kullanılan görüntü toobe yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="7b457-153">Configure hello operating system, and image toobe used for hello VM.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $vmName -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -PublisherName $publisher -Offer $offer -Skus $sku -Version $version
    ```

7. <span data-ttu-id="7b457-154">Toohello oluşturulan hello iki NIC ekleme `vmConfig` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="7b457-154">Add hello two NICs created above toohello `vmConfig` object.</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic2.Id
    ```

8. <span data-ttu-id="7b457-155">Merhaba işletim sistemi diski oluşturun ve hello VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7b457-155">Create hello OS disk and create hello VM.</span></span> <span data-ttu-id="7b457-156">Bildirim hello `}` hello bitiş `for` döngü.</span><span class="sxs-lookup"><span data-stu-id="7b457-156">Notice hello `}` ending hello `for` loop.</span></span>

    ```powershell
    $osDiskName = $vmName + "-" + $osDiskSuffix
    $osVhdUri = $stdStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $osDiskName + ".vhd"
    $vmConfig = Set-AzureRmVMOSDisk -VM $vmConfig -Name $osDiskName -VhdUri $osVhdUri -CreateOption fromImage
    New-AzureRmVM -VM $vmConfig -ResourceGroupName $backendRGName -Location $location
    }
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="7b457-157">Adım 4 - çalışma hello komut dosyası</span><span class="sxs-lookup"><span data-stu-id="7b457-157">Step 4 - Run hello script</span></span>
<span data-ttu-id="7b457-158">İndirilen ve değiştirilen hello betik gereksinimlerinize bağlı olarak toocreate hello arka uç veritabanı birden çok NIC içeren VM'ler kendisinin komut dosyası çalışma temel.</span><span class="sxs-lookup"><span data-stu-id="7b457-158">Now that you downloaded and changed hello script based on your needs, runt he script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="7b457-159">Komut dosyanızı kaydedin ve hello çalıştırın **PowerShell** komut istemi veya **PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="7b457-159">Save your script and run it from hello **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="7b457-160">Aşağıdaki gibi hello ilk çıktı görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="7b457-160">You will see hello initial output, as follows:</span></span>

        ResourceGroupName : IaaSStory-Backend
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
            Actions  NotActions
            =======  ==========
                *                  

        ResourceId        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend

2. <span data-ttu-id="7b457-161">Birkaç dakika sonra hello kimlik bilgileri istemi ve tıklatın doldurmak **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="7b457-161">After a few minutes, fill out hello credentials prompt and click **OK**.</span></span> <span data-ttu-id="7b457-162">Merhaba çıktı aşağıdaki tek bir VM'ye temsil eder.</span><span class="sxs-lookup"><span data-stu-id="7b457-162">hello output below represents a single VM.</span></span> <span data-ttu-id="7b457-163">Bildirim hello tüm işlem 8 dakika toocomplete sürdü.</span><span class="sxs-lookup"><span data-stu-id="7b457-163">Notice hello entire process took 8 minutes toocomplete.</span></span>

        ResourceGroupName            :
        Id                           :
        Name                         : DB2
        Type                         :
        Location                     :
        Tags                         :
        TagsText                     : null
        AvailabilitySetReference     : Microsoft.Azure.Management.Compute.Models.AvailabilitySetReference
        AvailabilitySetReferenceText :  {
                                    "ReferenceUri": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend/providers/Microsoft.Compute/availabilitySets/ASDB"
                                    }
        Extensions                   :
        ExtensionsText               : null
        HardwareProfile              : Microsoft.Azure.Management.Compute.Models.HardwareProfile
        HardwareProfileText          : {
                                        "VirtualMachineSize": "Standard_DS3"
                                       }
        InstanceView                 :
        InstanceViewText             : null
        NetworkProfile               :
        NetworkProfileText           : null
        OSProfile                    :
        OSProfileText                : null
        Plan                         :
        PlanText                     : null
        ProvisioningState            :
        StorageProfile               : Microsoft.Azure.Management.Compute.Models.StorageProfile
        StorageProfileText           : {
                                         "DataDisks": [
                                           {
                                             "Lun": 0,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-1",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-1.vhd"
                                             }
                                           }
                                         ],
                                         "ImageReference": null,
                                         "OSDisk": null
                                       }
        DataDiskNames                : {DB2-datadisk-1}
        NetworkInterfaceIDs          :
        RequestId                    :
        StatusCode                   : 0

        ResourceGroupName            :
        Id                           :
        Name                         : DB2
        Type                         :
        Location                     :
        Tags                         :
        TagsText                     : null
        AvailabilitySetReference     : Microsoft.Azure.Management.Compute.Models.AvailabilitySetReference
        AvailabilitySetReferenceText : {
                                         "ReferenceUri": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend/providers/
                                       Microsoft.Compute/availabilitySets/ASDB"
                                       }
        Extensions                   :
        ExtensionsText               : null
        HardwareProfile              : Microsoft.Azure.Management.Compute.Models.HardwareProfile
        HardwareProfileText          : {
                                         "VirtualMachineSize": "Standard_DS3"
                                       }
        InstanceView                 :
        InstanceViewText             : null
        NetworkProfile               :
        NetworkProfileText           : null
        OSProfile                    :
        OSProfileText                : null
        Plan                         :
        PlanText                     : null
        ProvisioningState            :
        StorageProfile               : Microsoft.Azure.Management.Compute.Models.StorageProfile
        StorageProfileText           : {
                                         "DataDisks": [
                                           {
                                             "Lun": 0,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-1",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-1.vhd"
                                             }
                                           },
                                           {
                                             "Lun": 1,
                                             "Caching": null,
                                             "CreateOption": "empty",
                                             "DiskSizeGB": 127,
                                             "Name": "DB2-datadisk-2",
                                             "SourceImage": null,
                                             "VirtualHardDisk": {
                                               "Uri": "https://wtestvnetstorageprm.blob.core.windows.net/vhds/DB2-datadisk-2.vhd"
                                             }
                                           }
                                         ],
                                         "ImageReference": null,
                                         "OSDisk": null
                                       }
        DataDiskNames                : {DB2-datadisk-1, DB2-datadisk-2}
        NetworkInterfaceIDs          :
        RequestId                    :
        StatusCode                   : 0
        EndTime             : [Date] [Time]
        Error               :
        Output              :
        StartTime           : [Date] [Time]
        Status              : Succeeded
        TrackingOperationId : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
        RequestId           : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx
        StatusCode          : OK
