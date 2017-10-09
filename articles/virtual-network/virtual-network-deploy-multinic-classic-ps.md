---
title: "aaaCreate birden çok NIC - Azure PowerShell'yle bir VM'yi (Klasik) | Microsoft Docs"
description: "Bilgi nasıl toocreate PowerShell kullanarak birden çok NIC'yle bir VM'yi (Klasik)."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 6e50f39a-2497-4845-a5d4-7332dbc203c5
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 90c967929bb418042c3fb7079e0f69246faac53c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-classic-with-multiple-nics-using-powershell"></a><span data-ttu-id="4fcc6-103">PowerShell kullanarak birden çok NIC ile VM (Klasik) oluşturun</span><span class="sxs-lookup"><span data-stu-id="4fcc6-103">Create a VM (Classic) with multiple NICs using PowerShell</span></span>

[!INCLUDE [virtual-network-deploy-multinic-classic-selectors-include.md](../../includes/virtual-network-deploy-multinic-classic-selectors-include.md)]

<span data-ttu-id="4fcc6-104">Sanal makineler (VM'ler) oluşturma ve birden çok ağ arabirimlerine (NIC'ler) tooeach, VM'lerin ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-104">You can create virtual machines (VMs) in Azure and attach multiple network interfaces (NICs) tooeach of your VMs.</span></span> <span data-ttu-id="4fcc6-105">Birden çok NIC NIC'ler arasında trafik türlerini ayrılması etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-105">Multiple NICs enable separation of traffic types across NICs.</span></span> <span data-ttu-id="4fcc6-106">Örneğin, bir başka yalnızca iç kaynakları ile iletişim kurar değil sırada NIC hello Internet ile iletişim kurabileceği toohello Internet bağlı.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-106">For example, one NIC might communicate with hello Internet, while another communicates only with internal resources not connected toohello Internet.</span></span> <span data-ttu-id="4fcc6-107">Merhaba özelliği tooseparate ağ trafiği birden çok NIC boyunca uygulama sunma ve WAN iyileştirmesi çözümleri gibi birçok ağ sanal uygulamaları için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-107">hello ability tooseparate network traffic across multiple NICs is required for many network virtual appliances, such as application delivery and WAN optimization solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4fcc6-108">Azure’da kaynak oluşturmak ve bunlarla çalışmak için iki farklı dağıtım modeli vardır:  [Resource Manager ve klasik](../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="4fcc6-108">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="4fcc6-109">Bu makalede, hello Klasik dağıtım modeli kullanılarak yer almaktadır.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-109">This article covers using hello classic deployment model.</span></span> <span data-ttu-id="4fcc6-110">Microsoft, en yeni dağıtımların hello Resource Manager modelini kullanmasını önerir.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-110">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="4fcc6-111">Bilgi nasıl tooperform hello kullanarak şu adımları [Resource Manager dağıtım modeli](virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="4fcc6-111">Learn how tooperform these steps using hello [Resource Manager deployment model](virtual-network-deploy-multinic-arm-ps.md).</span></span>

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

<span data-ttu-id="4fcc6-112">Merhaba aşağıdaki adımları kullanın adlı bir kaynak grubu *IaaSStory* hello WEB sunucuları ve bir kaynak grubu için adlı *IaaSStory arka uç* hello DB sunucuları için.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-112">hello following steps use a resource group named *IaaSStory* for hello WEB servers and a resource group named *IaaSStory-BackEnd* for hello DB servers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4fcc6-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="4fcc6-113">Prerequisites</span></span>

<span data-ttu-id="4fcc6-114">DB sunucuları hello oluşturabilmeniz için önce toocreate hello gerekir *IaaSStory* hello gereken tüm kaynakların bu senaryo için kaynak grubuyla.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-114">Before you can create hello DB servers, you need toocreate hello *IaaSStory* resource group with all hello necessary resources for this scenario.</span></span> <span data-ttu-id="4fcc6-115">Bu kaynaklar, tam izleyin adımları hello toocreate.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-115">toocreate these resources, complete hello steps that follow.</span></span> <span data-ttu-id="4fcc6-116">Merhaba hello adımları izleyerek bir sanal ağ oluşturma [bir sanal ağ oluşturma](virtual-networks-create-vnet-classic-netcfg-ps.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-116">Create a virtual network by following hello steps in hello [Create a virtual network](virtual-networks-create-vnet-classic-netcfg-ps.md) article.</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-back-end-vms"></a><span data-ttu-id="4fcc6-117">Arka uç VM'ler Hello oluşturma</span><span class="sxs-lookup"><span data-stu-id="4fcc6-117">Create hello back-end VMs</span></span>
<span data-ttu-id="4fcc6-118">Merhaba arka uç VM'ler kaynakları aşağıdaki hello hello oluşturulmasına bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="4fcc6-118">hello back-end VMs depend on hello creation of hello following resources:</span></span>

* <span data-ttu-id="4fcc6-119">**Arka uç alt**.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-119">**Backend subnet**.</span></span> <span data-ttu-id="4fcc6-120">Merhaba veritabanı sunucuları toosegregate trafiği ayrı bir alt parçası olacak.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-120">hello database servers will be part of a separate subnet, toosegregate traffic.</span></span> <span data-ttu-id="4fcc6-121">adlı sanal ağ içinde aşağıdaki Hello komut dosyası bekler bu alt ağ tooexist *WTestVnet*.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-121">hello script below expects this subnet tooexist in a vnet named *WTestVnet*.</span></span>
* <span data-ttu-id="4fcc6-122">**Veri diskleri için depolama hesabı**.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-122">**Storage account for data disks**.</span></span> <span data-ttu-id="4fcc6-123">Daha iyi performans için premium depolama hesabı gerektirir katı hal sürücüsü (SSD) teknolojisi hello veritabanı sunucularında hello veri diski kullanır.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-123">For better performance, hello data disks on hello database servers will use solid state drive (SSD) technology, which requires a premium storage account.</span></span> <span data-ttu-id="4fcc6-124">Emin hello toosupport premium depolama dağıttığınız Azure konumu olun.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-124">Make sure hello Azure location you deploy toosupport premium storage.</span></span>
* <span data-ttu-id="4fcc6-125">**Kullanılabilirlik kümesi**.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-125">**Availability set**.</span></span> <span data-ttu-id="4fcc6-126">Tüm veritabanı sunucuları tooa tek kullanılabilirlik kümesi eklenir, tooensure hello VM'ler en az biri hazır ve çalışır bakımı sırasında.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-126">All database servers will be added tooa single availability set, tooensure at least one of hello VMs is up and running during maintenance.</span></span>

### <a name="step-1---start-your-script"></a><span data-ttu-id="4fcc6-127">1. adım - kodunuzu Başlat</span><span class="sxs-lookup"><span data-stu-id="4fcc6-127">Step 1 - Start your script</span></span>
<span data-ttu-id="4fcc6-128">Kullanılan hello tam PowerShell komut dosyası indirebilirsiniz [burada](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span><span class="sxs-lookup"><span data-stu-id="4fcc6-128">You can download hello full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/classic/virtual-network-deploy-multinic-classic-ps.ps1).</span></span> <span data-ttu-id="4fcc6-129">Ortamınızdaki toochange hello betik toowork Hello adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-129">Follow hello steps below toochange hello script toowork in your environment.</span></span>

1. <span data-ttu-id="4fcc6-130">Değiştirme hello değişkenlerin değerleri yukarıda dağıtılmış varolan kaynak grubunuz göre hello aşağıdaki [Önkoşullar](#Prerequisites).</span><span class="sxs-lookup"><span data-stu-id="4fcc6-130">Change hello values of hello variables below based on your existing resource group deployed above in [Prerequisites](#Prerequisites).</span></span>

    ```powershell
    $location              = "West US"
    $vnetName              = "WTestVNet"
    $backendSubnetName     = "BackEnd"
    ```

2. <span data-ttu-id="4fcc6-131">Merhaba değerlerini değiştirin arka uç dağıtımınız için toouse istediğiniz hello değişkenleri aşağıdaki hello değerlerine göre.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-131">Change hello values of hello variables below based on hello values you want toouse for your backend deployment.</span></span>

    ```powershell
    $backendCSName         = "IaaSStory-Backend"
    $prmStorageAccountName = "iaasstoryprmstorage"
    $avSetName             = "ASDB"
    $vmSize                = "Standard_DS3"
    $diskSize              = 127
    $vmNamePrefix          = "DB"
    $dataDiskSuffix        = "datadisk"
    $ipAddressPrefix       = "192.168.2."
    $numberOfVMs           = 2
    ```

### <a name="step-2---create-necessary-resources-for-your-vms"></a><span data-ttu-id="4fcc6-132">2. adım - Vm'leriniz için gerekli kaynakları oluşturma</span><span class="sxs-lookup"><span data-stu-id="4fcc6-132">Step 2 - Create necessary resources for your VMs</span></span>
<span data-ttu-id="4fcc6-133">Yeni bir bulut hizmeti ve bir depolama hello veri diskleri için tüm VM'ler için hesap toocreate gerekir.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-133">You need toocreate a new cloud service and a storage account for hello data disks for all VMs.</span></span> <span data-ttu-id="4fcc6-134">Ayrıca toospecify görüntü ve yerel yönetici hesabı hello VM'ler için gerekir.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-134">You also need toospecify an image, and a local administrator account for hello VMs.</span></span> <span data-ttu-id="4fcc6-135">Bu kaynaklar toocreate tamamlamak hello adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="4fcc6-135">toocreate these resources, complete hello following steps:</span></span>

1. <span data-ttu-id="4fcc6-136">Yeni bir bulut hizmeti oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-136">Create a new cloud service.</span></span>

    ```powershell
    New-AzureService -ServiceName $backendCSName -Location $location
    ```

2. <span data-ttu-id="4fcc6-137">Yeni bir premium depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-137">Create a new premium storage account.</span></span>

    ```powershell
    New-AzureStorageAccount -StorageAccountName $prmStorageAccountName `
    -Location $location -Type Premium_LRS
    ```
3. <span data-ttu-id="4fcc6-138">Aboneliğiniz için geçerli depolama hesabı hello olarak yukarıda oluşturduğunuz hello depolama hesabını ayarlama.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-138">Set hello storage account created above as hello current storage account for your subscription.</span></span>

    ```powershell
    $subscription = Get-AzureSubscription | where {$_.IsCurrent -eq $true}  
    Set-AzureSubscription -SubscriptionName $subscription.SubscriptionName `
    -CurrentStorageAccountName $prmStorageAccountName
    ```

4. <span data-ttu-id="4fcc6-139">Merhaba VM için bir görüntü seçin.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-139">Select an image for hello VM.</span></span>

    ```powershell
    $image = Get-AzureVMImage `
    | where{$_.ImageFamily -eq "SQL Server 2014 RTM Web on Windows Server 2012 R2"} `
    | sort PublishedDate -Descending `
    | select -ExpandProperty ImageName -First 1
    ```

5. <span data-ttu-id="4fcc6-140">Merhaba yerel yönetici hesabının kimlik bilgilerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-140">Set hello local administrator account credentials.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Enter username and password for local admin account"
    ```

### <a name="step-3---create-vms"></a><span data-ttu-id="4fcc6-141">3. adım - VMs oluşturma</span><span class="sxs-lookup"><span data-stu-id="4fcc6-141">Step 3 - Create VMs</span></span>
<span data-ttu-id="4fcc6-142">Ve oluşturma gibi birçok VM gerekli NIC ve sanal makineleri hello döngü içinde hello gibi bir döngü toocreate toouse gerekir.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-142">You need toouse a loop toocreate as many VMs as you want, and create hello necessary NICs and VMs within hello loop.</span></span> <span data-ttu-id="4fcc6-143">toocreate hello NIC ve sanal makineleri, aşağıdaki adımları hello yürütün.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-143">toocreate hello NICs and VMs, execute hello following steps.</span></span>

1. <span data-ttu-id="4fcc6-144">Başlangıç bir `for` döngü toorepeat hello komutların toocreate VM iki NIC gerektiği gibi birçok kez hello hello değerine bağlı olarak `$numberOfVMs` değişkeni.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-144">Start a `for` loop toorepeat hello commands toocreate a VM and two NICs as many times as necessary, based on hello value of hello `$numberOfVMs` variable.</span></span>

    ```powershell
    for ($suffixNumber = 1; $suffixNumber -le $numberOfVMs; $suffixNumber++){
    ```

2. <span data-ttu-id="4fcc6-145">Oluşturma bir `VMConfig` hello görüntüsü, boyutu ve kullanılabilirlik Merhaba VM kümesi belirtme nesnesi.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-145">Create a `VMConfig` object specifying hello image, size, and availability set for hello VM.</span></span>

    ```powershell
    $vmName = $vmNamePrefix + $suffixNumber
    $vmConfig = New-AzureVMConfig -Name $vmName `
        -ImageName $image `
        -InstanceSize $vmSize `
        -AvailabilitySetName $avSetName
    ```

3. <span data-ttu-id="4fcc6-146">Merhaba VM Windows VM olarak sağlayın.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-146">Provision hello VM as a Windows VM.</span></span>

    ```powershell
    Add-AzureProvisioningConfig -VM $vmConfig -Windows `
        -AdminUsername $cred.UserName `
        -Password $cred.GetNetworkCredential().Password
    ```

4. <span data-ttu-id="4fcc6-147">Merhaba varsayılan NIC ayarlayabilir ve statik bir IP adresi atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-147">Set hello default NIC and assign it a static IP address.</span></span>

    ```powershell
    Set-AzureSubnet         -SubnetNames $backendSubnetName -VM $vmConfig
    Set-AzureStaticVNetIP   -IPAddress ($ipAddressPrefix+$suffixNumber+3) -VM $vmConfig
    ```

5. <span data-ttu-id="4fcc6-148">Her VM için ikinci bir NIC ekleyin.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-148">Add a second NIC for each VM.</span></span>

    ```powershell
    Add-AzureNetworkInterfaceConfig -Name ("RemoteAccessNIC"+$suffixNumber) `
    -SubnetName $backendSubnetName `
    -StaticVNetIPAddress ($ipAddressPrefix+(53+$suffixNumber)) `
    -VM $vmConfig
    ```

6. <span data-ttu-id="4fcc6-149">Toodata diskler için her bir VM oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-149">Create toodata disks for each VM.</span></span>

    ```powershell
    $dataDisk1Name = $vmName + "-" + $dataDiskSuffix + "-1"    
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk1Name `
    -LUN 0

    $dataDisk2Name = $vmName + "-" + $dataDiskSuffix + "-2"   
    Add-AzureDataDisk -CreateNew -VM $vmConfig `
    -DiskSizeInGB $diskSize `
    -DiskLabel $dataDisk2Name `
    -LUN 1
    ```

7. <span data-ttu-id="4fcc6-150">Her VM ve son hello döngü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-150">Create each VM, and end hello loop.</span></span>

    ```powershell
    New-AzureVM -VM $vmConfig `
    -ServiceName $backendCSName `
    -Location $location `
    -VNetName $vnetName
    }
    ```

### <a name="step-4---run-hello-script"></a><span data-ttu-id="4fcc6-151">Adım 4 - çalışma hello komut dosyası</span><span class="sxs-lookup"><span data-stu-id="4fcc6-151">Step 4 - Run hello script</span></span>
<span data-ttu-id="4fcc6-152">İndirilen ve değiştirilen hello betik gereksinimlerinize bağlı olarak toocreate hello arka uç veritabanı birden çok NIC içeren VM'ler kendisinin komut dosyası çalışma temel.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-152">Now that you downloaded and changed hello script based on your needs, runt he script toocreate hello back end database VMs with multiple NICs.</span></span>

1. <span data-ttu-id="4fcc6-153">Komut dosyanızı kaydedin ve hello çalıştırın **PowerShell** komut istemi veya **PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-153">Save your script and run it from hello **PowerShell** command prompt, or **PowerShell ISE**.</span></span> <span data-ttu-id="4fcc6-154">Merhaba ilk çıktısı, aşağıda gösterildiği gibi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-154">You will see hello initial output, as shown below.</span></span>

        OperationDescription    OperationId                          OperationStatus

        New-AzureService        xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureStorageAccount xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        
        WARNING: No deployment found in service: 'IaaSStory-Backend'.
2. <span data-ttu-id="4fcc6-155">Merhaba kimlik bilgileri istemi ve tıklatın gerekli hello bilgileri doldurun **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-155">Fill out hello information needed in hello credentials prompt and click **OK**.</span></span> <span data-ttu-id="4fcc6-156">Merhaba çıktı aşağıdaki döndürülür.</span><span class="sxs-lookup"><span data-stu-id="4fcc6-156">hello output below is returned.</span></span>

        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
        New-AzureVM             xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Succeeded
