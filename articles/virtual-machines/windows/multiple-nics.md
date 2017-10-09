---
title: "aaaCreate ve Windows birden çok NIC kullanan azure'da Vm'leri yönetmek | Microsoft Docs"
description: "Bilgi nasıl toocreate ve Azure PowerShell veya Resource Manager şablonları kullanarak birden çok NIC ekli tooit sahip bir Windows VM yönetin."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 9bff5b6d-79ac-476b-a68f-6f8754768413
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: c3c7d7569aca6f047238146d84b2ffccf05d4079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-windows-virtual-machine-that-has-multiple-nics"></a><span data-ttu-id="14852-103">Oluşturma ve birden çok NIC sahip olan bir Windows sanal makine yönetme</span><span class="sxs-lookup"><span data-stu-id="14852-103">Create and manage a Windows virtual machine that has multiple NICs</span></span>
<span data-ttu-id="14852-104">Azure sanal makineleri (VM'ler) birden çok sanal ağ arabirimi kartlarıyla (NIC) bağlı toothem olabilir.</span><span class="sxs-lookup"><span data-stu-id="14852-104">Virtual machines (VMs) in Azure can have multiple virtual network interface cards (NICs) attached toothem.</span></span> <span data-ttu-id="14852-105">Yaygın bir senaryo toohave farklı alt ağlar için ön uç ve arka uç bağlantısı olan veya ayrılmış bir ağ tooa izleme veya yedekleme çözümü.</span><span class="sxs-lookup"><span data-stu-id="14852-105">A common scenario is toohave different subnets for front-end and back-end connectivity, or a network dedicated tooa monitoring or backup solution.</span></span> <span data-ttu-id="14852-106">Bu makalede nasıl tooit toocreate birden çok NIC sahip bir VM ekli ayrıntıları verilmektedir.</span><span class="sxs-lookup"><span data-stu-id="14852-106">This article details how toocreate a VM that has multiple NICs attached tooit.</span></span> <span data-ttu-id="14852-107">Da bilgi nasıl tooadd veya kaldırma NIC var olan bir VM'den.</span><span class="sxs-lookup"><span data-stu-id="14852-107">You also learn how tooadd or remove NICs from an existing VM.</span></span> <span data-ttu-id="14852-108">Farklı [VM boyutları](sizes.md) NIC'ler değişen çok sayıda desteği, bu nedenle, VM buna göre boyutu.</span><span class="sxs-lookup"><span data-stu-id="14852-108">Different [VM sizes](sizes.md) support a varying number of NICs, so size your VM accordingly.</span></span>

<span data-ttu-id="14852-109">Ayrıntılı bilgi için kendi PowerShell komut dosyaları içinde birden çok NIC toocreate nasıl görürüm dahil olmak üzere [birden çok NIC VM'ler dağıtma](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="14852-109">For detailed information, including how toocreate multiple NICs within your own PowerShell scripts, see [deploying multiple-NIC VMs](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="14852-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="14852-110">Prerequisites</span></span>
<span data-ttu-id="14852-111">Merhaba sahip olduğunuzdan emin olun [yüklenmiş ve yapılandırılmış en son Azure PowerShell sürüm](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="14852-111">Make sure that you have hello [latest Azure PowerShell version installed and configured](/powershell/azure/overview).</span></span>

<span data-ttu-id="14852-112">Hello aşağıdaki örneklerde, örnek parametre adları kendi değerlerinizle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="14852-112">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="14852-113">Örnek parametre adlarında *myResourceGroup*, *myVnet*, ve *myVM*.</span><span class="sxs-lookup"><span data-stu-id="14852-113">Example parameter names include *myResourceGroup*, *myVnet*, and *myVM*.</span></span>


## <a name="create-a-vm-with-multiple-nics"></a><span data-ttu-id="14852-114">Birden çok NIC ile VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="14852-114">Create a VM with multiple NICs</span></span>
<span data-ttu-id="14852-115">İlk olarak, bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="14852-115">First, create a resource group.</span></span> <span data-ttu-id="14852-116">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroup* hello içinde *EastUs* konumu:</span><span class="sxs-lookup"><span data-stu-id="14852-116">hello following example creates a resource group named *myResourceGroup* in hello *EastUs* location:</span></span>

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "EastUS"
```

### <a name="create-virtual-network-and-subnets"></a><span data-ttu-id="14852-117">Sanal ağ ve alt ağlar oluşturun</span><span class="sxs-lookup"><span data-stu-id="14852-117">Create virtual network and subnets</span></span>
<span data-ttu-id="14852-118">Yaygın bir senaryo için sanal ağ toohave olan iki veya daha fazla alt ağ.</span><span class="sxs-lookup"><span data-stu-id="14852-118">A common scenario is for a virtual network toohave two or more subnets.</span></span> <span data-ttu-id="14852-119">Bir alt ağ ön uç trafiği için arka uç trafiği için diğer hello olabilir.</span><span class="sxs-lookup"><span data-stu-id="14852-119">One subnet may be for front-end traffic, hello other for back-end traffic.</span></span> <span data-ttu-id="14852-120">tooconnect tooboth alt ağlar, daha sonra VM birden çok NIC kullanın.</span><span class="sxs-lookup"><span data-stu-id="14852-120">tooconnect tooboth subnets, you then use multiple NICs on your VM.</span></span>

1. <span data-ttu-id="14852-121">İle iki sanal ağ alt ağları tanımlamak [yeni AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span><span class="sxs-lookup"><span data-stu-id="14852-121">Define two virtual network subnets with [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig).</span></span> <span data-ttu-id="14852-122">Merhaba aşağıdaki örnek tanımlar hello alt ağlar için *mySubnetFrontEnd* ve *mySubnetBackEnd*:</span><span class="sxs-lookup"><span data-stu-id="14852-122">hello following example defines hello subnets for *mySubnetFrontEnd* and *mySubnetBackEnd*:</span></span>

    ```powershell
    $mySubnetFrontEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetFrontEnd" `
        -AddressPrefix "192.168.1.0/24"
    $mySubnetBackEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetBackEnd" `
        -AddressPrefix "192.168.2.0/24"
    ```

2. <span data-ttu-id="14852-123">Sanal ağ ve alt ağları ile oluşturmak [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="14852-123">Create your virtual network and subnets with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="14852-124">Merhaba aşağıdaki örnek adlı bir sanal ağ oluşturur *myVnet*:</span><span class="sxs-lookup"><span data-stu-id="14852-124">hello following example creates a virtual network named *myVnet*:</span></span>

    ```powershell
    $myVnet = New-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" `
        -Location "EastUs" `
        -Name "myVnet" `
        -AddressPrefix "192.168.0.0/16" `
        -Subnet $mySubnetFrontEnd,$mySubnetBackEnd
    ```


### <a name="create-multiple-nics"></a><span data-ttu-id="14852-125">Birden çok NIC oluşturun</span><span class="sxs-lookup"><span data-stu-id="14852-125">Create multiple NICs</span></span>
<span data-ttu-id="14852-126">İki NIC ile oluşturma [yeni AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="14852-126">Create two NICs with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="14852-127">Bir NIC toohello ön uç alt ağı ve bir NIC toohello arka uç alt ekleyin.</span><span class="sxs-lookup"><span data-stu-id="14852-127">Attach one NIC toohello front-end subnet and one NIC toohello back-end subnet.</span></span> <span data-ttu-id="14852-128">Merhaba aşağıdaki örnekte oluşturur adlı NIC'ler *myNic1* ve *myNic2*:</span><span class="sxs-lookup"><span data-stu-id="14852-128">hello following example creates NICs named *myNic1* and *myNic2*:</span></span>

```powershell
$frontEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetFrontEnd'}
$myNic1 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic1" `
    -Location "EastUs" `
    -SubnetId $frontEnd.Id

$backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}
$myNic2 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic2" `
    -Location "EastUs" `
    -SubnetId $backEnd.Id
```

<span data-ttu-id="14852-129">Genellikle ayrıca oluşturduğunuz bir [ağ güvenlik grubu](../../virtual-network/virtual-networks-nsg.md) veya [yük dengeleyici](../../load-balancer/load-balancer-overview.md) toohelp yönetmek ve Vm'leriniz arasında trafiği dağıtın.</span><span class="sxs-lookup"><span data-stu-id="14852-129">Typically you also create a [network security group](../../virtual-network/virtual-networks-nsg.md) or [load balancer](../../load-balancer/load-balancer-overview.md) toohelp manage and distribute traffic across your VMs.</span></span> <span data-ttu-id="14852-130">Merhaba [birden çok NIC VM ayrıntılı](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) makale, bir ağ güvenlik grubu oluşturma ve NIC atama size kılavuzluk eder.</span><span class="sxs-lookup"><span data-stu-id="14852-130">hello [more detailed multiple-NIC VM](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md) article guides you through creating a network security group and assigning NICs.</span></span>

### <a name="create-hello-virtual-machine"></a><span data-ttu-id="14852-131">Merhaba sanal makine oluşturma</span><span class="sxs-lookup"><span data-stu-id="14852-131">Create hello virtual machine</span></span>
<span data-ttu-id="14852-132">Şimdi toobuild VM yapılandırmanızı başlatın.</span><span class="sxs-lookup"><span data-stu-id="14852-132">Now start toobuild your VM configuration.</span></span> <span data-ttu-id="14852-133">Her VM boyutu hello toplam sayısı tooa VM ekleyebilirsiniz NIC'ler için bir sınırı vardır.</span><span class="sxs-lookup"><span data-stu-id="14852-133">Each VM size has a limit for hello total number of NICs that you can add tooa VM.</span></span> <span data-ttu-id="14852-134">Daha fazla bilgi için bkz: [Windows VM boyutları](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="14852-134">For more information, see [Windows VM sizes](sizes.md).</span></span>

1. <span data-ttu-id="14852-135">VM kimlik bilgilerini toohello ayarlamak `$cred` şekilde değişkeni:</span><span class="sxs-lookup"><span data-stu-id="14852-135">Set your VM credentials toohello `$cred` variable as follows:</span></span>

    ```powershell
    $cred = Get-Credential
    ```

2. <span data-ttu-id="14852-136">VM ile tanımlama [AzureRmVMConfig yeni](/powershell/module/azurerm.compute/new-azurermvmconfig).</span><span class="sxs-lookup"><span data-stu-id="14852-136">Define your VM with [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig).</span></span> <span data-ttu-id="14852-137">Merhaba aşağıdaki örnek tanımlar adlı bir VM'den *myVM* ve ikiden fazla NIC'ler destekleyen bir VM boyutu kullanır (*Standard_DS3_v2*):</span><span class="sxs-lookup"><span data-stu-id="14852-137">hello following example defines a VM named *myVM* and uses a VM size that supports more than two NICs (*Standard_DS3_v2*):</span></span>

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS3_v2"
    ```

3. <span data-ttu-id="14852-138">VM yapılandırmanızı Hello kalan oluşturma [kümesi AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) ve [kümesi AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span><span class="sxs-lookup"><span data-stu-id="14852-138">Create hello rest of your VM configuration with [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) and [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage).</span></span> <span data-ttu-id="14852-139">Aşağıdaki örnek hello bir Windows Server 2016 VM oluşturur:</span><span class="sxs-lookup"><span data-stu-id="14852-139">hello following example creates a Windows Server 2016 VM:</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig `
        -Windows `
        -ComputerName "myVM" `
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig `
        -PublisherName "MicrosoftWindowsServer" `
        -Offer "WindowsServer" `
        -Skus "2016-Datacenter" `
        -Version "latest"
   ```

4. <span data-ttu-id="14852-140">Daha önce oluşturduğunuz ile Merhaba iki NIC ekleme [Ekle AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="14852-140">Attach hello two NICs that you previously created with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic2.Id
    ```

5. <span data-ttu-id="14852-141">Son olarak, VM oluşturma [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="14852-141">Finally, create your VM with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):</span></span>

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName "myResourceGroup" -Location "EastUs"
    ```

## <a name="add-a-nic-tooan-existing-vm"></a><span data-ttu-id="14852-142">VM varolan bir NIC tooan Ekle</span><span class="sxs-lookup"><span data-stu-id="14852-142">Add a NIC tooan existing VM</span></span>
<span data-ttu-id="14852-143">VM varolan bir sanal NIC tooan hello VM ayırması tooadd eklemek sanal NIC hello sonra hello VM başlatın.</span><span class="sxs-lookup"><span data-stu-id="14852-143">tooadd a virtual NIC tooan existing VM, you deallocate hello VM, add hello virtual NIC, then start hello VM.</span></span>

1. <span data-ttu-id="14852-144">Deallocate VM ile Merhaba [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="14852-144">Deallocate hello VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="14852-145">Merhaba aşağıdaki örnek kaldırır hello adlı VM *myVM* içinde *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="14852-145">hello following example deallocates hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="14852-146">Merhaba VM Hello varolan yapılandırmasını almak ile [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="14852-146">Get hello existing configuration of hello VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="14852-147">Merhaba aşağıdaki örnek alır bilgi hello adlı VM için *myVM* içinde *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="14852-147">hello following example gets information for hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="14852-148">Merhaba aşağıdaki örnekte oluşturur ile sanal bir NIC'ye [yeni AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) adlı *myNic3* , çok bağlı*mySubnetBackEnd*.</span><span class="sxs-lookup"><span data-stu-id="14852-148">hello following example creates a virtual NIC with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) named *myNic3* that is attached too*mySubnetBackEnd*.</span></span> <span data-ttu-id="14852-149">Sanal NIC durumda hello bağlı toohello adlı VM *myVM* içinde *myResourceGroup* ile [Ekle AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="14852-149">hello virtual NIC is then attached toohello VM named *myVM* in *myResourceGroup* with [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):</span></span>

    ```powershell
    # Get info for hello back end subnet
    $myVnet = Get-AzureRmVirtualNetwork -Name "myVnet" -ResourceGroupName "myResourceGroup"
    $backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}

    # Create a virtual NIC
    $myNic3 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
        -Name "myNic3" `
        -Location "EastUs" `
        -SubnetId $backEnd.Id

    # Get hello ID of hello new virtual NIC and add tooVM
    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "MyNic3").Id
    Add-AzureRmVMNetworkInterface -VM $vm -Id $nicId | Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```

    ### <a name="primary-virtual-nics"></a><span data-ttu-id="14852-150">Birincil sanal NIC</span><span class="sxs-lookup"><span data-stu-id="14852-150">Primary virtual NICs</span></span>
    <span data-ttu-id="14852-151">Merhaba multi-NIC VM Nıc'lerde birini toobe birincil gerekir.</span><span class="sxs-lookup"><span data-stu-id="14852-151">One of hello NICs on a multi-NIC VM needs toobe primary.</span></span> <span data-ttu-id="14852-152">Aşağıdakilerden birini varolan sanal NIC hello hello üzerinde VM zaten birincil olarak ayarlanmış, bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="14852-152">If one of hello existing virtual NICs on hello VM is already set as primary, you can skip this step.</span></span> <span data-ttu-id="14852-153">Merhaba aşağıdaki örnekte iki sanal NIC VM üzerinde mevcut şimdi tooadd istediğiniz varsayar ve ilk NIC hello (`[0]`) hello birincil olarak:</span><span class="sxs-lookup"><span data-stu-id="14852-153">hello following example assumes that two virtual NICs are now present on a VM and you wish tooadd hello first NIC (`[0]`) as hello primary:</span></span>
        
    ```powershell
    # List existing NICs on hello VM and find which one is primary
    $vm.NetworkProfile.NetworkInterfaces
    
    # Set NIC 0 toobe primary
    $vm.NetworkProfile.NetworkInterfaces[0].Primary = $true
    $vm.NetworkProfile.NetworkInterfaces[1].Primary = $false
    
    # Update hello VM state in Azure
    Update-AzureRmVM -VM $vm -ResourceGroupName "myResourceGroup"
    ```

4. <span data-ttu-id="14852-154">Başlangıç VM ile Merhaba [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="14852-154">Start hello VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

## <a name="remove-a-nic-from-an-existing-vm"></a><span data-ttu-id="14852-155">Bir NIC var olan bir sanal makineden kaldırın</span><span class="sxs-lookup"><span data-stu-id="14852-155">Remove a NIC from an existing VM</span></span>
<span data-ttu-id="14852-156">sanal bir NIC'ye tooremove var olan bir VM'den hello VM serbest bırakma, hello Kaldır sanal NIC sonra Başlangıç hello VM.</span><span class="sxs-lookup"><span data-stu-id="14852-156">tooremove a virtual NIC from an existing VM, you deallocate hello VM, remove hello virtual NIC, then start hello VM.</span></span>

1. <span data-ttu-id="14852-157">Deallocate VM ile Merhaba [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="14852-157">Deallocate hello VM with [Stop-AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm).</span></span> <span data-ttu-id="14852-158">Merhaba aşağıdaki örnek kaldırır hello adlı VM *myVM* içinde *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="14852-158">hello following example deallocates hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. <span data-ttu-id="14852-159">Merhaba VM Hello varolan yapılandırmasını almak ile [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="14852-159">Get hello existing configuration of hello VM with [Get-AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm).</span></span> <span data-ttu-id="14852-160">Merhaba aşağıdaki örnek alır bilgi hello adlı VM için *myVM* içinde *myResourceGroup*:</span><span class="sxs-lookup"><span data-stu-id="14852-160">hello following example gets information for hello VM named *myVM* in *myResourceGroup*:</span></span>

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. <span data-ttu-id="14852-161">NIC kaldırma ile Merhaba hakkında bilgi almak [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="14852-161">Get information about hello NIC remove with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface).</span></span> <span data-ttu-id="14852-162">Merhaba aşağıdaki örnek bilgilerini alır *myNic3*:</span><span class="sxs-lookup"><span data-stu-id="14852-162">hello following example gets information about *myNic3*:</span></span>

    ```powershell
    # List existing NICs on hello VM if you need toodetermine NIC name
    $vm.NetworkProfile.NetworkInterfaces

    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "myNic3").Id   
    ```

4. <span data-ttu-id="14852-163">Kaldırma NIC ile Merhaba [Kaldır AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) ve ardından güncelleştirme VM ile Merhaba [güncelleştirme-AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="14852-163">Remove hello NIC with [Remove-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface) and then update hello VM with [Update-AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm).</span></span> <span data-ttu-id="14852-164">Merhaba aşağıdaki örnek kaldırır *myNic3* ile alınan `$nicId` adım önceki hello içinde:</span><span class="sxs-lookup"><span data-stu-id="14852-164">hello following example removes *myNic3* as obtained by `$nicId` in hello preceding step:</span></span>

    ```powershell
    Remove-AzureRmVMNetworkInterface -VM $vm -NetworkInterfaceIDs $nicId | `
        Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```   

5. <span data-ttu-id="14852-165">Başlangıç VM ile Merhaba [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="14852-165">Start hello VM with [Start-AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):</span></span>

    ```powershell
    Start-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```   

## <a name="create-multiple-nics-with-templates"></a><span data-ttu-id="14852-166">Birden çok NIC ile şablonları oluşturma</span><span class="sxs-lookup"><span data-stu-id="14852-166">Create multiple NICs with templates</span></span>
<span data-ttu-id="14852-167">Azure Resource Manager şablonları bir şekilde toocreate birden çok NIC oluşturma gibi dağıtım işlemi sırasında birden fazla örneğini bir kaynak sağlayın.</span><span class="sxs-lookup"><span data-stu-id="14852-167">Azure Resource Manager templates provide a way toocreate multiple instances of a resource during deployment, such as creating multiple NICs.</span></span> <span data-ttu-id="14852-168">Resource Manager şablonları bildirim temelli JSON dosyaları toodefine ortamınız kullanın.</span><span class="sxs-lookup"><span data-stu-id="14852-168">Resource Manager templates use declarative JSON files toodefine your environment.</span></span> <span data-ttu-id="14852-169">Daha fazla bilgi için bkz: [genel bakış Azure Kaynak Yöneticisi'nin](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="14852-169">For more information, see [overview of Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="14852-170">Kullanabileceğiniz *kopya* toospecify hello örnekleri toocreate sayısı:</span><span class="sxs-lookup"><span data-stu-id="14852-170">You can use *copy* toospecify hello number of instances toocreate:</span></span>

```json
"copy": {
    "name": "multiplenics",
    "count": "[parameters('count')]"
}
```

<span data-ttu-id="14852-171">Daha fazla bilgi için bkz: [kullanarak birden çok örneği oluşturma *kopya*](../../resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="14852-171">For more information, see [creating multiple instances by using *copy*](../../resource-group-create-multiple.md).</span></span> 

<span data-ttu-id="14852-172">Aynı zamanda `copyIndex()` tooappend bir numara tooa kaynak adı.</span><span class="sxs-lookup"><span data-stu-id="14852-172">You can also use `copyIndex()` tooappend a number tooa resource name.</span></span> <span data-ttu-id="14852-173">Daha sonra oluşturabilirsiniz *myNic1*, *MyNic2* ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="14852-173">You can then create *myNic1*, *MyNic2* and so on.</span></span> <span data-ttu-id="14852-174">Merhaba aşağıdaki kodda hello dizin değeri ekleyerek bir örnek gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="14852-174">hello following code shows an example of appending hello index value:</span></span>

```json
"name": "[concat('myNic', copyIndex())]", 
```

<span data-ttu-id="14852-175">Tam örnek okuyabilirsiniz [Resource Manager şablonları kullanarak birden çok NIC oluşturma](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="14852-175">You can read a complete example of [creating multiple NICs by using Resource Manager templates](../../virtual-network/virtual-network-deploy-multinic-arm-template.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="14852-176">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="14852-176">Next steps</span></span>
<span data-ttu-id="14852-177">Gözden geçirme [Windows VM boyutları](sizes.md) zaman çalıştığınız toocreate birden çok NIC sahip bir VM.</span><span class="sxs-lookup"><span data-stu-id="14852-177">Review [Windows VM sizes](sizes.md) when you're trying toocreate a VM that has multiple NICs.</span></span> <span data-ttu-id="14852-178">Dikkat toohello en fazla sayıda her VM boyutu destekleyen NIC ücret ödersiniz.</span><span class="sxs-lookup"><span data-stu-id="14852-178">Pay attention toohello maximum number of NICs that each VM size supports.</span></span> 


