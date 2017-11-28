---
title: "aaaAvailability öğretici azure'da Windows sanal makineleri için ayarlar | Microsoft Docs"
description: "Merhaba kullanılabilirlik kümeleri için Windows azure'da VM hakkında bilgi edinin."
documentationcenter: 
services: virtual-machines-windows
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
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 853775c5f126dd815c1933f9d71d2274a75ea661
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a><span data-ttu-id="73a32-103">Nasıl toouse kullanılabilirlik kümeleri</span><span class="sxs-lookup"><span data-stu-id="73a32-103">How toouse availability sets</span></span>

<span data-ttu-id="73a32-104">Bu öğreticide, nasıl tooincrease hello kullanılabilirliği ve güvenilirliği bir özelliği kullanarak azure'da sanal makine çözümlerinizi kullanılabilirlik kümeleri adlı öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="73a32-104">In this tutorial, you will learn how tooincrease hello availability and reliability of your Virtual Machine solutions on Azure using a capability called Availability Sets.</span></span> <span data-ttu-id="73a32-105">Kullanılabilirlik kümeleri, Azure üzerinde dağıttığınız VM'lerin birden çok yalıtılmış donanım kümeler arasında dağıtılır, hello emin olun.</span><span class="sxs-lookup"><span data-stu-id="73a32-105">Availability sets ensure that hello VMs you deploy on Azure are distributed across multiple isolated hardware clusters.</span></span> <span data-ttu-id="73a32-106">Bunun yapılması Azure içinde bir donanım veya yazılım hatası olur, alt kümesini, VM'ler etkilenir ve çözümünüzün genel kullanılabilir ve işletimsel kullanmadan müşterilerinizin hello açısından kalacak sağlar.</span><span class="sxs-lookup"><span data-stu-id="73a32-106">Doing this ensures that if a hardware or software failure within Azure happens, only a sub-set of your VMs will be impacted and that your overall solution will remain available and operational from hello perspective of your customers using it.</span></span> 

<span data-ttu-id="73a32-107">Bu öğreticide şunların nasıl yapıldığını öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="73a32-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="73a32-108">Kullanılabilirlik kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="73a32-108">Create an availability set</span></span>
> * <span data-ttu-id="73a32-109">Bir kullanılabilirlik kümesine bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="73a32-109">Create a VM in an availability set</span></span>
> * <span data-ttu-id="73a32-110">Kullanılabilir VM boyutları denetleyin</span><span class="sxs-lookup"><span data-stu-id="73a32-110">Check available VM sizes</span></span>

<span data-ttu-id="73a32-111">Bu öğretici hello Azure PowerShell modülü 3,6 veya sonraki bir sürümü gerektiriyor.</span><span class="sxs-lookup"><span data-stu-id="73a32-111">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="73a32-112">Çalıştırma ` Get-Module -ListAvailable AzureRM` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="73a32-112">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="73a32-113">Tooupgrade gerekirse bkz [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="73a32-113">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>

## <a name="availability-set-overview"></a><span data-ttu-id="73a32-114">Kullanılabilirlik kümesi'ne genel bakış</span><span class="sxs-lookup"><span data-stu-id="73a32-114">Availability set overview</span></span>

<span data-ttu-id="73a32-115">Bir kullanılabilirlik kümesi kullanabileceğiniz bir mantıksal bir gruplandırma bir Azure veri merkezi içinde dağıtıldığında içine yerleştirin hello VM kaynakları birbirinden yalıtılmış Azure tooensure içinde bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="73a32-115">An Availability Set is a logical grouping capability that you can use in Azure tooensure that hello VM resources you place within it are isolated from each other when they are deployed within an Azure datacenter.</span></span> <span data-ttu-id="73a32-116">Bu hello VM'ler arasında birden fazla fiziksel sunucu çalıştırmak bir kullanılabilirlik kümesi içinde yerleştirin Azure sağlar, işlem rafları, depolama birimi ve ağ anahtarları.</span><span class="sxs-lookup"><span data-stu-id="73a32-116">Azure ensures that hello VMs you place within an Availability Set run across multiple physical servers, compute racks, storage units, and network switches.</span></span> <span data-ttu-id="73a32-117">Bu hello olay bir donanım ya da Azure yazılım hatası yalnızca bir alt kümesini, VM'ler etkilenir ve genel uygulamanız kalması ve toobe kullanılabilir tooyour müşteriler devam sağlar.</span><span class="sxs-lookup"><span data-stu-id="73a32-117">This ensures that in hello event of a hardware or Azure software failure, only a subset of your VMs will be impacted, and your overall application will stay up and continue toobe available tooyour customers.</span></span> <span data-ttu-id="73a32-118">Toobuild güvenilir bulut çözümleri istediğiniz kullanılabilirlik kümelerini kullanarak bir önemli özelliği tooleverage durumdur.</span><span class="sxs-lookup"><span data-stu-id="73a32-118">Using Availability Sets is an essential capability tooleverage when you want toobuild reliable cloud solutions.</span></span>

<span data-ttu-id="73a32-119">Şimdi burada 4 ön uç web sunucusu ve bir veritabanı ana bilgisayar 2 arka uç VM kullanmak bir tipik VM tabanlı çözümünü göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="73a32-119">Let’s consider a typical VM-based solution where you might have 4 front-end web servers and use 2 back-end VMs that host a database.</span></span> <span data-ttu-id="73a32-120">Azure ile Vm'leriniz dağıtmadan önce toodefine iki kullanılabilirlik kümeleri istiyor: hello "web" katmanı ve bir kullanılabilirlik kümesi için hello "veritabanı" katmanı için bir kullanılabilirlik kümesi.</span><span class="sxs-lookup"><span data-stu-id="73a32-120">With Azure, you’d want toodefine two availability sets before you deploy your VMs: one availability set for hello “web” tier and one availability set for hello “database” tier.</span></span> <span data-ttu-id="73a32-121">Ardından, bir parametre toohello az vm komutu oluşturun ve Azure otomatik olarak o hello hello içinde oluşturduğunuz VM'ler sağlayacak şekilde ayarlayın hello kullanılabilirlik belirtebilirsiniz yeni bir VM oluştururken kümesi yalıtılmış birden çok fiziksel donanım kaynaklarına arasında.</span><span class="sxs-lookup"><span data-stu-id="73a32-121">When you create a new VM you can then specify hello availability set as a parameter toohello az vm create command, and Azure will automatically ensure that hello VMs you create within hello available set are isolated across multiple physical hardware resources.</span></span> <span data-ttu-id="73a32-122">Bir Web sunucusu veya veritabanı sunucusu VM'ler üzerinde çalıştığı hello fiziksel donanım bir sorun varsa, o hello bilmeniz yani farklı donanıma olduğundan Web sunucusu ve veritabanı VM'ler diğer örneklerini düzgün çalışır durumda.</span><span class="sxs-lookup"><span data-stu-id="73a32-122">This means that if hello physical hardware that one of your Web Server or Database Server VMs is running on has a problem, you know that hello other instances of your Web Server and Database VMs will remain running fine because they are on different hardware.</span></span>

<span data-ttu-id="73a32-123">Azure içindeki güvenilir tabanlı VM çözümleri toodeploy istediğinizde kullanılabilirlik kümeleri her zaman kullanmalısınız.</span><span class="sxs-lookup"><span data-stu-id="73a32-123">You should always use Availability Sets when you want toodeploy reliable VM based solutions within Azure.</span></span>

## <a name="create-an-availability-set"></a><span data-ttu-id="73a32-124">Kullanılabilirlik kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="73a32-124">Create an availability set</span></span>

<span data-ttu-id="73a32-125">Kullanılabilirlik kümesi kullanarak oluşturabileceğiniz [yeni AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="73a32-125">You can create an availability set using [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="73a32-126">Bu örnekte, güncelleştirme ve hata etki alanları iki hello sayısı ayarlarız *2* hello kullanılabilirlik adlandırılmış kümesi için *myAvailabilitySet* hello içinde *myResourceGroupAvailability*kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="73a32-126">In this example, we set both hello number of update and fault domains at *2* for hello availability set named *myAvailabilitySet* in hello *myResourceGroupAvailability* resource group.</span></span>

<span data-ttu-id="73a32-127">Bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="73a32-127">Create a resource group.</span></span>

```powershell
New-AzureRmResourceGroup -Name myResourceGroupAvailability -Location EastUS
```


```powershell
New-AzureRmAvailabilitySet `
   -Location EastUS `
   -Name myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability `
   -Managed `
   -PlatformFaultDomainCount 2 `
   -PlatformUpdateDomainCount 2
```

## <a name="create-vms-inside-an-availability-set"></a><span data-ttu-id="73a32-128">VM'ler içinde bir kullanılabilirlik kümesi oluştur</span><span class="sxs-lookup"><span data-stu-id="73a32-128">Create VMs inside an availability set</span></span>

<span data-ttu-id="73a32-129">Sanal makineleri hello kullanılabilirlik kümesi toomake hello donanım üzerinde doğru şekilde dağıtıldığından emin içinde oluşturulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="73a32-129">VMs need toobe created within hello availability set toomake sure they are correctly distributed across hello hardware.</span></span> <span data-ttu-id="73a32-130">Var olan VM tooan kullanılabilirlik kümesi oluşturulduktan sonra eklenemez.</span><span class="sxs-lookup"><span data-stu-id="73a32-130">You can't add an existing VM tooan availability set after it is created.</span></span> 

<span data-ttu-id="73a32-131">bir konumda Hello donanım toomultiple güncelleştirme etki alanları ve hata etki alanları ayrılmıştır.</span><span class="sxs-lookup"><span data-stu-id="73a32-131">hello hardware in a location is divided in toomultiple update domains and fault domains.</span></span> <span data-ttu-id="73a32-132">Bir **güncelleştirme etki alanı** VM'ler ve hello yeniden temel alınan fiziksel donanım oluşan bir gruptur aynı anda.</span><span class="sxs-lookup"><span data-stu-id="73a32-132">An **update domain** is a group of VMs and underlying physical hardware that can be rebooted at hello same time.</span></span> <span data-ttu-id="73a32-133">İçinde sanal makineleri aynı hello **hata etki alanı** ortak bir güç kaynağı ve ağ anahtarı yanı sıra genel depolama paylaşın.</span><span class="sxs-lookup"><span data-stu-id="73a32-133">VMs in hello same **fault domain** share common storage as well as a common power source and network switch.</span></span> 

<span data-ttu-id="73a32-134">Yapılandırma kullanarak bir VM oluştururken [yeni AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) hello kullanılarak ayarlanan hello kullanılabilirliği belirtmek `-AvailabilitySetId` hello kullanılabilirlik kümesinin parametresi toospecify hello kimliği.</span><span class="sxs-lookup"><span data-stu-id="73a32-134">When you create a VM using configuration using [New-AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) you specify hello availability set using hello `-AvailabilitySetId` parameter toospecify hello ID of hello availability set.</span></span>

<span data-ttu-id="73a32-135">İle 2 VM oluşturma [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) hello kullanılabilirlik kümesinde.</span><span class="sxs-lookup"><span data-stu-id="73a32-135">Create 2 VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) in hello availability set.</span></span>

```powershell
$availabilitySet = Get-AzureRmAvailabilitySet `
    -ResourceGroupName myResourceGroupAvailability `
    -Name myAvailabilitySet

$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAvailability `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

for ($i=1; $i -le 2; $i++)
{
   $pip = New-AzureRmPublicIpAddress `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name "mypublicdns$(Get-Random)" `
        -AllocationMethod Static `
        -IdleTimeoutInMinutes 4

   $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
        -Name myNetworkSecurityGroupRuleRDP$i `
        -Protocol Tcp `
        -Direction Inbound `
        -Priority 1000 `
        -SourceAddressPrefix * `
        -SourcePortRange * `
        -DestinationAddressPrefix * `
        -DestinationPortRange 3389 `
        -Access Allow

   $nsg = New-AzureRmNetworkSecurityGroup `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name myNetworkSecurityGroup$i `
        -SecurityRules $nsgRuleRDP

   $nic = New-AzureRmNetworkInterface `
        -Name myNic$i `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -SubnetId $vnet.Subnets[0].Id `
        -PublicIpAddressId $pip.Id `
        -NetworkSecurityGroupId $nsg.Id

   # Here is where we specify hello availability set
   $vm = New-AzureRmVMConfig `
        -VMName myVM$i `
        -VMSize Standard_D1 `
        -AvailabilitySetId $availabilitySet.Id

   $vm = Set-AzureRmVMOperatingSystem `
        -VM $vm `
        -Windows -ComputerName myVM$i `   
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage `
        -VM $vm `
        -PublisherName MicrosoftWindowsServer `
        -Offer WindowsServer `
        -Skus 2016-Datacenter `
        -Version latest
   $vm = Set-AzureRmVMOSDisk `
        -VM $vm `
        -Name myOsDisk$i `
        -DiskSizeInGB 128 `
        -CreateOption FromImage `
        -Caching ReadWrite
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -VM $vm
}

```

<span data-ttu-id="73a32-136">Birkaç dakika toocreate alır ve her iki VM yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="73a32-136">It takes a few minutes toocreate and configure both VMs.</span></span> <span data-ttu-id="73a32-137">Tamamlandığında, temel alınan donanım hello arasında dağıtılmış 2 sanal makine sahip olur.</span><span class="sxs-lookup"><span data-stu-id="73a32-137">When finished, you will have 2 virtual machines distributed across hello underlying hardware.</span></span> 

## <a name="check-for-available-vm-sizes"></a><span data-ttu-id="73a32-138">Kullanılabilir VM boyutları denetle</span><span class="sxs-lookup"><span data-stu-id="73a32-138">Check for available VM sizes</span></span> 

<span data-ttu-id="73a32-139">Daha fazla sanal makineleri toohello kullanılabilirlik kümesi daha sonra ekleyebilirsiniz, ancak hangi VM boyutları hello donanımda kullanılabilir tooknow gerekir.</span><span class="sxs-lookup"><span data-stu-id="73a32-139">You can add more VMs toohello availability set later, but you need tooknow what VM sizes are available on hello hardware.</span></span> <span data-ttu-id="73a32-140">Kullanım [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) tüm hello kullanılabilir boyutları hello donanımda hello kullanılabilirlik kümesi için küme toolist.</span><span class="sxs-lookup"><span data-stu-id="73a32-140">Use [Get-AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) toolist all hello available sizes on hello hardware cluster for hello availability set.</span></span>

```powershell
Get-AzureRmVMSize `
   -AvailabilitySetName myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability  
```

## <a name="next-steps"></a><span data-ttu-id="73a32-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="73a32-141">Next steps</span></span>

<span data-ttu-id="73a32-142">Bu öğreticide, şunların nasıl yapıldığını öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="73a32-142">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="73a32-143">Kullanılabilirlik kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="73a32-143">Create an availability set</span></span>
> * <span data-ttu-id="73a32-144">Bir kullanılabilirlik kümesine bir VM oluşturma</span><span class="sxs-lookup"><span data-stu-id="73a32-144">Create a VM in an availability set</span></span>
> * <span data-ttu-id="73a32-145">Kullanılabilir VM boyutları denetleyin</span><span class="sxs-lookup"><span data-stu-id="73a32-145">Check available VM sizes</span></span>

<span data-ttu-id="73a32-146">Sanal makine ölçek kümeleri hakkında toohello sonraki öğretici toolearn ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="73a32-146">Advance toohello next tutorial toolearn about virtual machine scale sets.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="73a32-147">VM ölçek kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="73a32-147">Create a VM scale set</span></span>](tutorial-create-vmss.md)


