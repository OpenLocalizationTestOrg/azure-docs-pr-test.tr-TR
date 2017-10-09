---
title: "yönetilen bir VM görüntüden Azure VM aaaCreate | Microsoft Docs"
description: "Merhaba Resource Manager dağıtım modelinde Azure PowerShell kullanarak genelleştirilmiş yönetilen VM görüntüsü Windows sanal makine oluşturun."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: cynthn
ms.openlocfilehash: 5036ef1533c144a9a328e94599b359e0166f337d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-managed-image"></a><span data-ttu-id="ad570-103">Yönetilen bir görüntüden bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="ad570-103">Create a VM from a managed image</span></span>

<span data-ttu-id="ad570-104">Azure yönetilen bir VM görüntüsünden birden çok VM oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad570-104">You can create multiple VMs from a managed VM image in Azure.</span></span> <span data-ttu-id="ad570-105">Yönetilen bir VM görüntüsü hello bilgi gerekli toocreate hello işletim sistemi ve veri diskleri de dahil olmak üzere, bir VM içerir.</span><span class="sxs-lookup"><span data-stu-id="ad570-105">A managed VM image contains hello information necessary toocreate a VM, including hello OS and data disks.</span></span> <span data-ttu-id="ad570-106">Merhaba hello OS diskleri ve veri diskleri de dahil olmak üzere hello görüntüyü oluşturan, yönetilen diskleri olarak depolanan VHD.</span><span class="sxs-lookup"><span data-stu-id="ad570-106">hello VHDs that make up hello image, including both hello OS disks and any data disks, are stored as managed disks.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="ad570-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ad570-107">Prerequisites</span></span>

<span data-ttu-id="ad570-108">Toohave zaten gereksinim [yönetilen bir VM görüntüsü oluşturulan](capture-image-resource.md) oluşturmak için toouse hello yeni VM.</span><span class="sxs-lookup"><span data-stu-id="ad570-108">You need toohave already [created a managed VM image](capture-image-resource.md) toouse for creating hello new VM.</span></span> 

<span data-ttu-id="ad570-109">Merhaba AzureRM.Compute ve AzureRM.Network PowerShell modülleri hello en son sürümüne sahip olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="ad570-109">Make sure that you have hello latest versions of hello AzureRM.Compute and AzureRM.Network PowerShell modules.</span></span> <span data-ttu-id="ad570-110">PowerShell komut istemini yönetici olarak açın ve komut tooinstall aşağıdaki hello çalıştırın bunları.</span><span class="sxs-lookup"><span data-stu-id="ad570-110">Open a PowerShell prompt as an Administrator and run hello following command tooinstall them.</span></span>

```powershell
Install-Module AzureRM.Compute,AzureRM.Network
```
<span data-ttu-id="ad570-111">Daha fazla bilgi için bkz: [Azure PowerShell sürüm](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ad570-111">For more information, see [Azure PowerShell Versioning](/powershell/azure/overview).</span></span>



## <a name="collect-information-about-hello-image"></a><span data-ttu-id="ad570-112">Merhaba görüntü ile ilgili bilgileri toplama</span><span class="sxs-lookup"><span data-stu-id="ad570-112">Collect information about hello image</span></span>

<span data-ttu-id="ad570-113">İlk biz hello görüntü ile ilgili temel bilgileri toogather gerekir ve hello görüntüsü için bir değişken oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ad570-113">First we need toogather basic information about hello image and create a variable for hello image.</span></span> <span data-ttu-id="ad570-114">Bu örnek adında yönetilen bir VM görüntüsü kullanan **myImage** diğer bir deyişle içinde hello **myResourceGroup** hello kaynak grubunda **Batı Orta ABD** konumu.</span><span class="sxs-lookup"><span data-stu-id="ad570-114">This example uses a managed VM image named **myImage** that is in hello **myResourceGroup** resource group in hello **West Central US** location.</span></span> 

```powershell
$rgName = "myResourceGroup"
$location = "West Central US"
$imageName = "myImage"
$image = Get-AzureRMImage -ImageName $imageName -ResourceGroupName $rgName
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="ad570-115">Sanal ağ oluşturma</span><span class="sxs-lookup"><span data-stu-id="ad570-115">Create a virtual network</span></span>
<span data-ttu-id="ad570-116">Merhaba vNet ve alt hello oluşturma [sanal ağ](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ad570-116">Create hello vNet and subnet of hello [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="ad570-117">Merhaba alt ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ad570-117">Create hello subnet.</span></span> <span data-ttu-id="ad570-118">Bu örnek adlı bir alt ağı oluşturur **mySubnet** hello adres öneki ile **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="ad570-118">This example creates a subnet named **mySubnet** with hello address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="ad570-119">Merhaba sanal ağ oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ad570-119">Create hello virtual network.</span></span> <span data-ttu-id="ad570-120">Bu örnek adlı bir sanal ağ oluşturur **myVnet** hello adres öneki ile **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="ad570-120">This example creates a virtual network named **myVnet** with hello address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="ad570-121">Ortak IP adresi ve ağ arabirimi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ad570-121">Create a public IP address and network interface</span></span>

<span data-ttu-id="ad570-122">ihtiyacınız tooenable iletişimi hello sanal ağındaki hello sanal makineyle bir [genel IP adresi](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) ve ağ arabirimi.</span><span class="sxs-lookup"><span data-stu-id="ad570-122">tooenable communication with hello virtual machine in hello virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="ad570-123">Bir ortak IP adresi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ad570-123">Create a public IP address.</span></span> <span data-ttu-id="ad570-124">Bu örnek adlı ortak IP adresi oluşturur **myPip**.</span><span class="sxs-lookup"><span data-stu-id="ad570-124">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="ad570-125">Merhaba NIC oluşturun</span><span class="sxs-lookup"><span data-stu-id="ad570-125">Create hello NIC.</span></span> <span data-ttu-id="ad570-126">Bu örnek, adlandırılmış bir NIC oluşturur **myNic**.</span><span class="sxs-lookup"><span data-stu-id="ad570-126">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="ad570-127">Merhaba ağ güvenlik grubu ve bir RDP kuralı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ad570-127">Create hello network security group and an RDP rule</span></span>

<span data-ttu-id="ad570-128">toobe mümkün toolog tooyour içinde RDP kullanarak VM toohave 3389 numaralı bağlantı noktası üzerinde RDP erişimine izin veren bir ağ güvenlik kuralı (NSG) gerekir.</span><span class="sxs-lookup"><span data-stu-id="ad570-128">toobe able toolog in tooyour VM using RDP, you need toohave a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="ad570-129">Bu örnekte adlı bir NSG oluşturulur **myNsg** adlı kuralı içeren **myRdpRule** 3389 numaralı bağlantı noktası RDP trafiğine izin veren.</span><span class="sxs-lookup"><span data-stu-id="ad570-129">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="ad570-130">Nsg'ler hakkında daha fazla bilgi için bkz: [bağlantı noktalarını tooa VM PowerShell kullanarak Azure içinde açma](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ad570-130">For more information about NSGs, see [Opening ports tooa VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-hello-virtual-network"></a><span data-ttu-id="ad570-131">Merhaba sanal ağ için bir değişken oluşturma</span><span class="sxs-lookup"><span data-stu-id="ad570-131">Create a variable for hello virtual network</span></span>

<span data-ttu-id="ad570-132">Tamamlanan hello sanal ağ için bir değişken oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ad570-132">Create a variable for hello completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a><span data-ttu-id="ad570-133">Merhaba VM Hello kimlik bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="ad570-133">Get hello credentials for hello VM</span></span>

<span data-ttu-id="ad570-134">Merhaba aşağıdaki cmdlet'i yeni bir kullanıcı adı ve parola toouse hello yerel yönetici hesabı olarak hello VM uzaktan erişmek için gireceğiniz bir pencere açılır.</span><span class="sxs-lookup"><span data-stu-id="ad570-134">hello following cmdlet will open a window where you will enter a new user name and password toouse as hello local administrator account for remotely accessing hello VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="set-variables-for-hello-vm-name-computer-name-and-hello-size-of-hello-vm"></a><span data-ttu-id="ad570-135">Merhaba VM kümesi değişkenleri adı, bilgisayar adı ve hello hello VM boyutu</span><span class="sxs-lookup"><span data-stu-id="ad570-135">Set variables for hello VM name, computer name and hello size of hello VM</span></span>

1. <span data-ttu-id="ad570-136">Merhaba VM adı ve bilgisayar adı için değişkenler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ad570-136">Create variables for hello VM name and computer name.</span></span> <span data-ttu-id="ad570-137">Bu örnek hello VM adı olarak ayarlar **myVM** ve hello bilgisayar adı olarak **Bilgisayarım**.</span><span class="sxs-lookup"><span data-stu-id="ad570-137">This example sets hello VM name as **myVM** and hello computer name as **myComputer**.</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    ```
2. <span data-ttu-id="ad570-138">Merhaba hello sanal makine boyutunu ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ad570-138">Set hello size of hello virtual machine.</span></span> <span data-ttu-id="ad570-139">Bu örnekte **Standard_DS1_v2** VM boyuta sahip.</span><span class="sxs-lookup"><span data-stu-id="ad570-139">This example creates **Standard_DS1_v2** sized VM.</span></span> <span data-ttu-id="ad570-140">Merhaba bkz [VM boyutları](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="ad570-140">See hello [VM sizes](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentation for more information.</span></span>

    ```powershell
    $vmSize = "Standard_DS1_v2"
    ```

3. <span data-ttu-id="ad570-141">Merhaba VM adını ve boyutunu toohello VM yapılandırmasına ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ad570-141">Add hello VM name and size toohello VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a><span data-ttu-id="ad570-142">Set hello VM görüntüsü hello için kaynak görüntüsü olarak yeni VM</span><span class="sxs-lookup"><span data-stu-id="ad570-142">Set hello VM image as source image for hello new VM</span></span>

<span data-ttu-id="ad570-143">Yönetilen hello VM görüntüsü Hello Kimliğini kullanarak hello kaynak görüntüsü ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ad570-143">Set hello source image using hello ID of hello managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a><span data-ttu-id="ad570-144">Merhaba işletim sistemi yapılandırması ayarlayın ve hello NIC ekleyin</span><span class="sxs-lookup"><span data-stu-id="ad570-144">Set hello OS configuration and add hello NIC.</span></span>

<span data-ttu-id="ad570-145">Merhaba depolama türü (PremiumLRS veya StandardLRS) ve hello işletim sistemi diski hello boyutunu girin.</span><span class="sxs-lookup"><span data-stu-id="ad570-145">Enter hello storage type (PremiumLRS or StandardLRS) and hello size of hello OS disk.</span></span> <span data-ttu-id="ad570-146">Bu örnek hello hesap türü çok ayarlar**PremiumLRS**, disk boyutu çok hello**128 GB** ve disk çok önbelleğe alma**ReadWrite**.</span><span class="sxs-lookup"><span data-stu-id="ad570-146">This example sets hello account type too**PremiumLRS**, hello disk size too**128 GB** and disk caching too**ReadWrite**.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm  -StorageAccountType PremiumLRS -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a><span data-ttu-id="ad570-147">Merhaba VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="ad570-147">Create hello VM</span></span>

<span data-ttu-id="ad570-148">Oluşturma biz yerleşik ve hello depolanan hello Yapılandırması'nı kullanarak yeni Vm hello **$vm** değişkeni.</span><span class="sxs-lookup"><span data-stu-id="ad570-148">Create hello new Vm using hello configuration that we have built and stored in hello **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a><span data-ttu-id="ad570-149">VM oluşturulduğu bu hello doğrulayın</span><span class="sxs-lookup"><span data-stu-id="ad570-149">Verify that hello VM was created</span></span>
<span data-ttu-id="ad570-150">Tamamlandığında, yeni VM hello oluşturulan hello görmelisiniz [Azure portal](https://portal.azure.com) altında **Gözat** > **sanal makineleri**, veya hello aşağıdakileri kullanarak PowerShell komutları:</span><span class="sxs-lookup"><span data-stu-id="ad570-150">When complete, you should see hello newly created VM in hello [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using hello following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="ad570-151">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ad570-151">Next steps</span></span>
<span data-ttu-id="ad570-152">Yeni sanal makinenizi Azure PowerShell ile toomanage bkz [oluşturma ve hello Azure PowerShell modülü ile Windows sanal makineleri yönetme](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ad570-152">toomanage your new virtual machine with Azure PowerShell, see [Create and manage Windows VMs with hello Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

