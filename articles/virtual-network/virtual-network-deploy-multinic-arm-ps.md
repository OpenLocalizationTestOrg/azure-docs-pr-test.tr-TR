---
title: "Birden çok NIC - Azure PowerShell ile bir VM oluşturma | Microsoft Docs"
description: "PowerShell kullanarak birden çok NIC ile VM oluşturmayı öğrenin."
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
ms.openlocfilehash: f3a11afd8fbd6a5e6b94cf1ebee7ea20665421bd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-multiple-nics-using-powershell"></a><span data-ttu-id="7f7cc-103">PowerShell kullanarak birden çok NIC ile VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="7f7cc-103">Create a VM with multiple NICs using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="7f7cc-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7f7cc-104">PowerShell</span></span>](virtual-network-deploy-multinic-arm-ps.md)
> * [<span data-ttu-id="7f7cc-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7f7cc-105">Azure CLI</span></span>](virtual-network-deploy-multinic-arm-cli.md)
> * [<span data-ttu-id="7f7cc-106">Şablon</span><span class="sxs-lookup"><span data-stu-id="7f7cc-106">Template</span></span>](virtual-network-deploy-multinic-arm-template.md)
> * [<span data-ttu-id="7f7cc-107">PowerShell (Klasik)</span><span class="sxs-lookup"><span data-stu-id="7f7cc-107">PowerShell (Classic)</span></span>](virtual-network-deploy-multinic-classic-ps.md)
> * [<span data-ttu-id="7f7cc-108">Azure CLI (Klasik)</span><span class="sxs-lookup"><span data-stu-id="7f7cc-108">Azure CLI (Classic)</span></span>](virtual-network-deploy-multinic-classic-cli.md)

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="7f7cc-109">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="7f7cc-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span>  <span data-ttu-id="7f7cc-110">Bu makale, Microsoft’un çoğu yeni dağıtım için [klasik dağıtım modeli](virtual-network-deploy-multinic-classic-ps.md) yerine önerdiği Resource Manager dağıtım modelini açıklamaktadır.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-110">This article covers using the Resource Manager deployment model, which Microsoft recommends for most new deployments instead of the [classic deployment model](virtual-network-deploy-multinic-classic-ps.md).</span></span>
>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="7f7cc-111">Adlı bir kaynak grubu aşağıdaki adımları kullanın *IaaSStory* WEB sunucuları ve bir kaynak grubu için adlı *IaaSStory arka uç* DB sunucuları için.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-111">The following steps use a resource group named *IaaSStory* for the WEB servers and a resource group named *IaaSStory-BackEnd* for the DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f7cc-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7f7cc-112">Prerequisites</span></span>
<span data-ttu-id="7f7cc-113">DB sunucuları oluşturabilmeniz için önce oluşturmanız gerekir *IaaSStory* bu senaryo için gereken tüm kaynakların kaynak grubuyla.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-113">Before you can create the DB servers, you need to create the *IaaSStory* resource group with all the necessary resources for this scenario.</span></span> <span data-ttu-id="7f7cc-114">Bu kaynakları oluşturmak için aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="7f7cc-114">To create these resources, complete the following steps:</span></span>

1. <span data-ttu-id="7f7cc-115">Gidin [şablon sayfasına](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span><span class="sxs-lookup"><span data-stu-id="7f7cc-115">Navigate to [the template page](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).</span></span>
2. <span data-ttu-id="7f7cc-116">Şablon sayfasındaki sağ tarafındaki **üst kaynak grubu**, tıklatın **Azure'a Dağıt**.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-116">In the template page, to the right of **Parent resource group**, click **Deploy to Azure**.</span></span>
3. <span data-ttu-id="7f7cc-117">Gerekirse, parametre değerlerini değiştirin, sonra kaynak grubu dağıtmak için Azure Önizleme Portalı'ndaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-117">If needed, change the parameter values, then follow the steps in the Azure preview portal to deploy the resource group.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7f7cc-118">Depolama hesabı adları benzersiz olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-118">Make sure your storage account names are unique.</span></span> <span data-ttu-id="7f7cc-119">Azure üzerinde yinelenen depolama hesabı adları sahip olamaz.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-119">You cannot have duplicate storage account names in Azure.</span></span>
> 

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-the-back-end-vms"></a><span data-ttu-id="7f7cc-120">Arka uç VM'ler oluşturma</span><span class="sxs-lookup"><span data-stu-id="7f7cc-120">Create the back-end VMs</span></span>
<span data-ttu-id="7f7cc-121">Arka uç VM'ler aşağıdaki kaynaklara oluşturulmasını bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="7f7cc-121">The back-end VMs depend on the creation of the following resources:</span></span>

* <span data-ttu-id="7f7cc-122">**Veri diskleri için depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-122">**Storage account for data disks**.</span></span> <span data-ttu-id="7f7cc-123">Daha iyi performans için veritabanı sunucularında veri diskler bir premium depolama hesabı gerektirir katı hal sürücüsü (SSD) teknolojisi kullanır.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-123">For better performance, the data disks on the database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="7f7cc-124">Premium depolama desteklemek için dağıtmanız Azure konumu emin olun.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-124">Make sure the Azure location you deploy to support premium storage.</span></span>
* <span data-ttu-id="7f7cc-125">**NIC**.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-125">**NICs**.</span></span> <span data-ttu-id="7f7cc-126">Her VM veritabanı erişimi için iki NIC gerekir ve yönetimi için bir tane.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-126">Each VM will have two NICs, one for database access, and one for management.</span></span>
* <span data-ttu-id="7f7cc-127">**Kullanılabilirlik kümesi**.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-127">**Availability set**.</span></span> <span data-ttu-id="7f7cc-128">Tüm veritabanı sunucuları, en az bir sanal makineleri çalışır durumda emin olmak için ayarlayın ve bakım sırasında çalıştıran tek bir kullanılabilirlik eklenir.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-128">All database servers will be added to a single availability set, to ensure at least one of the VMs is up and running during maintenance.</span></span>  

### <a name="step-1---start-your-script"></a><span data-ttu-id="7f7cc-129">1. adım - kodunuzu Başlat</span><span class="sxs-lookup"><span data-stu-id="7f7cc-129">Step 1 - Start your script</span></span>
<span data-ttu-id="7f7cc-130">Kullanılan tam PowerShell komut dosyası indirebilirsiniz [burada](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="7f7cc-130">You can download the full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/arm/virtual-network-deploy-multinic-arm-ps.ps1).</span></span> <span data-ttu-id="7f7cc-131">Ortamınızda çalışması için komut dosyasını değiştirmek için aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-131">Follow the steps below to change the script to work in your environment.</span></span>

1. <span data-ttu-id="7f7cc-132">Yukarıdaki dağıtılmış varolan kaynak grubunuz temelinde değişkenleri aşağıdaki değerlerini değiştirmek [Önkoşullar](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="7f7cc-132">Change the values of the variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $existingRGName        = "IaaSStory"
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    $remoteAccessNSGName   = "NSG-RemoteAccess"
    $stdStorageAccountName = "wtestvnetstoragestd"
    ```

2. <span data-ttu-id="7f7cc-133">Arka uç dağıtımınız için kullanmak istediğiniz değerleri temel alarak aşağıdaki değişkenlerinin değerlerini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-133">Change the values of the variables below based on the values you want to use for your backend deployment.</span></span>

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
3. <span data-ttu-id="7f7cc-134">Dağıtımınız için gereken mevcut kaynakları alır.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-134">Retrieve the existing resources needed for your deployment.</span></span>

    ```powershell
    $vnet                  = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $existingRGName
    $backendSubnet         = $vnet.Subnets|?{$_.Name -eq $backendSubnetName}
    $remoteAccessNSG       = Get-AzureRmNetworkSecurityGroup -Name $remoteAccessNSGName -ResourceGroupName $existingRGName
    $stdStorageAccount     = Get-AzureRmStorageAccount -Name $stdStorageAccountName -ResourceGroupName $existingRGName
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="7f7cc-135">2. adım - Vm'leriniz için gerekli kaynakları oluşturma</span><span class="sxs-lookup"><span data-stu-id="7f7cc-135">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="7f7cc-136">Yeni bir kaynak grubu, veri diskleri ve kullanılabilirlik tüm VM'ler için kümesi için bir depolama hesabı oluşturmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-136">You need to create a new resource group, a storage account for the data disks, and an availability set for all VMs.</span></span> <span data-ttu-id="7f7cc-137">Seçecek her VM için yerel yönetici hesabı kimlik bilgileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-137">You alos need the local administrator account credentials for each VM.</span></span> <span data-ttu-id="7f7cc-138">Bu kaynakları oluşturmak için aşağıdaki adımları yürütün.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-138">To create these resources, execute the following steps.</span></span>

1. <span data-ttu-id="7f7cc-139">Yeni bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-139">Create a new resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name $backendRGName -Location $location
    ```
2. <span data-ttu-id="7f7cc-140">Yukarıda oluşturduğunuz kaynak grubunda yeni bir premium depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-140">Create a new premium storage account in the resource group created above.</span></span>

    ```powershell
    $prmStorageAccount = New-AzureRmStorageAccount -Name $prmStorageAccountName `
    -ResourceGroupName $backendRGName -Type Premium_LRS -Location $location
    ```
3. <span data-ttu-id="7f7cc-141">Yeni bir kullanılabilirlik kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-141">Create a new availability set.</span></span>

    ```powershell
    $avSet = New-AzureRmAvailabilitySet -Name $avSetName -ResourceGroupName $backendRGName -Location $location
    ```
4. <span data-ttu-id="7f7cc-142">Yerel yönetici her VM için kullanılacak hesap kimlik bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-142">Get the local administrator account credentials to be used for each VM.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Type the name and password for the local administrator account."
    ```

### <a name="step-3---create-the-nics-and-back-end-vms"></a><span data-ttu-id="7f7cc-143">Adım 3 - NIC ve arka uç VM'ler oluşturma</span><span class="sxs-lookup"><span data-stu-id="7f7cc-143">Step 3 - Create the NICs and back-end VMs</span></span>
<span data-ttu-id="7f7cc-144">Ve gerekli NIC ve sanal makineleri döngüye içinde gibi birçok VM oluşturmak için bir döngü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-144">You need to use a loop to create as many VMs as you want, and create the necessary NICs and VMs within the loop.</span></span> <span data-ttu-id="7f7cc-145">NIC ve sanal makineleri oluşturmak için aşağıdaki adımları yürütün.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-145">To create the NICs and VMs, execute the following steps.</span></span>

1. <span data-ttu-id="7f7cc-146">Başlangıç bir `for` değerine göre bir VM ve gerektiği pek çok, iki NIC oluşturmak için komutları yinelemek için döngü `$numberOfVMs` değişkeni.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-146">Start a `for` loop to repeat the commands to create a VM and two NICs as many times as necessary, based on the value of the `$numberOfVMs` variable.</span></span>
   
    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="7f7cc-147">Veritabanı erişimi için kullanılan NIC oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-147">Create the NIC used for database access.</span></span>

    ```powershell
    $nic1Name = $nicNamePrefix + $suffixNumber + "-DA"
    $ipAddress1 = $ipAddressPrefix + ($suffixNumber + 3)
    $nic1 = New-AzureRmNetworkInterface -Name $nic1Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress1
    ```

3. <span data-ttu-id="7f7cc-148">Uzaktan erişim için kullanılan NIC oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-148">Create the NIC used for remote access.</span></span> <span data-ttu-id="7f7cc-149">Bu NIC için ilişkilendirilmiş bir NSG nasıl sahip dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-149">Notice how this NIC has an NSG associated to it.</span></span>

    ```powershell
    $nic2Name = $nicNamePrefix + $suffixNumber + "-RA"
    $ipAddress2 = $ipAddressPrefix + (53 + $suffixNumber)
    $nic2 = New-AzureRmNetworkInterface -Name $nic2Name -ResourceGroupName $backendRGName `
    -Location $location -SubnetId $backendSubnet.Id -PrivateIpAddress $ipAddress2 `
    -NetworkSecurityGroupId $remoteAccessNSG.Id
    ```

4. <span data-ttu-id="7f7cc-150">Oluşturma `vmConfig` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-150">Create `vmConfig` object.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize -AvailabilitySetId $avSet.Id
    ```

5. <span data-ttu-id="7f7cc-151">VM başına iki veri diski oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-151">Create two data disks per VM.</span></span> <span data-ttu-id="7f7cc-152">Veri diskleri daha önce oluşturduğunuz premium depolama hesabını olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-152">Notice that the data disks are in the premium storage account created earlier.</span></span>

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

6. <span data-ttu-id="7f7cc-153">İşletim sistemi yapılandırması ve VM için kullanılacak resim.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-153">Configure the operating system, and image to be used for the VM.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $vmName -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -PublisherName $publisher -Offer $offer -Skus $sku -Version $version
    ```

7. <span data-ttu-id="7f7cc-154">Yukarıda oluşturulan iki NIC ekleme `vmConfig` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-154">Add the two NICs created above to the `vmConfig` object.</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic2.Id
    ```

8. <span data-ttu-id="7f7cc-155">İşletim sistemi diski oluşturun ve VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-155">Create the OS disk and create the VM.</span></span> <span data-ttu-id="7f7cc-156">Bildirim `}` bitiş `for` döngü.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-156">Notice the `}` ending the `for` loop.</span></span>

    ```powershell
    $osDiskName = $vmName + "-" + $osDiskSuffix
    $osVhdUri = $stdStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $osDiskName + ".vhd"
    $vmConfig = Set-AzureRmVMOSDisk -VM $vmConfig -Name $osDiskName -VhdUri $osVhdUri -CreateOption fromImage
    New-AzureRmVM -VM $vmConfig -ResourceGroupName $backendRGName -Location $location
    }
    ```

### <a name="step-4---run-the-script"></a><span data-ttu-id="7f7cc-157">Adım 4 - komut dosyasını çalıştır</span><span class="sxs-lookup"><span data-stu-id="7f7cc-157">Step 4 - Run the script</span></span>
<span data-ttu-id="7f7cc-158">İndirilen ve gereksinimlerinize göre komut değiştirilen göre çalışma kendisinin komut dosyası arka uç veritabanı VM'ler ile birden çok NIC oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-158">Now that you downloaded and changed the script based on your needs, runt he script to create the back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="7f7cc-159">Komut dosyanızı kaydedin ve çalıştırın **PowerShell** komut istemi veya **PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-159">Save your script and run it from the **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="7f7cc-160">İlk çıkış gibi görürsünüz:</span><span class="sxs-lookup"><span data-stu-id="7f7cc-160">You will see the initial output, as follows:</span></span>

        ResourceGroupName : IaaSStory-Backend
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
            Actions  NotActions
            =======  ==========
                *                  

        ResourceId        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory-Backend

2. <span data-ttu-id="7f7cc-161">Birkaç dakika sonra kimlik bilgileri istemi ve tıklatın doldurmak **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-161">After a few minutes, fill out the credentials prompt and click **OK**.</span></span> <span data-ttu-id="7f7cc-162">Çıktı tek bir VM'ye temsil eder.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-162">The output below represents a single VM.</span></span> <span data-ttu-id="7f7cc-163">Bildirim tüm işlemini tamamlamak için 8 dakika sürdü.</span><span class="sxs-lookup"><span data-stu-id="7f7cc-163">Notice the entire process took 8 minutes to complete.</span></span>

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
