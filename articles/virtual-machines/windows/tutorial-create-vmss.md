---
title: "bir sanal makine ölçek kümeleri için Windows Azure aaaCreate | Microsoft Docs"
description: "Windows sanal makine ölçek kümesini kullanarak sanal makineleri üzerinde yüksek oranda kullanılabilir bir uygulama oluşturun ve dağıtın"
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: 
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: a3914571005c28a492c069d880992630851afae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-windows"></a><span data-ttu-id="f883d-103">Bir sanal makine ölçek kümesi oluşturma ve yüksek oranda kullanılabilir bir Windows uygulamasını dağıtma</span><span class="sxs-lookup"><span data-stu-id="f883d-103">Create a Virtual Machine Scale Set and deploy a highly available app on Windows</span></span>
<span data-ttu-id="f883d-104">Bir sanal makine ölçek kümesi toodeploy sağlar ve aynı, otomatik ölçeklendirme sanal makineler kümesi yönetin.</span><span class="sxs-lookup"><span data-stu-id="f883d-104">A virtual machine scale set allows you toodeploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="f883d-105">Merhaba hello ölçek kümesindeki VM'lerin sayısını elle ölçeklendirme ya da CPU kullanımı, bellek isteğe bağlı veya ağ trafiğini dayalı kurallar tooautoscale tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f883d-105">You can scale hello number of VMs in hello scale set manually, or define rules tooautoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="f883d-106">Bu öğreticide, Azure üzerinde ayarlanmış bir sanal makine ölçek dağıtın.</span><span class="sxs-lookup"><span data-stu-id="f883d-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="f883d-107">Aşağıdakileri nasıl yapacağınızı öğrenirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f883d-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f883d-108">Merhaba özel betik uzantısının toodefine bir IIS site tooscale kullanın</span><span class="sxs-lookup"><span data-stu-id="f883d-108">Use hello Custom Script Extension toodefine an IIS site tooscale</span></span>
> * <span data-ttu-id="f883d-109">Ölçek kümesi için bir yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="f883d-109">Create a load balancer for your scale set</span></span>
> * <span data-ttu-id="f883d-110">Bir sanal makine ölçek kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="f883d-110">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="f883d-111">Artırma veya azaltma hello ölçek kümesi örneği sayısı</span><span class="sxs-lookup"><span data-stu-id="f883d-111">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="f883d-112">Otomatik ölçeklendirme kuralları oluşturma</span><span class="sxs-lookup"><span data-stu-id="f883d-112">Create autoscale rules</span></span>

<span data-ttu-id="f883d-113">Bu öğretici hello Azure PowerShell modülü 3,6 veya sonraki bir sürümü gerektiriyor.</span><span class="sxs-lookup"><span data-stu-id="f883d-113">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="f883d-114">Çalıştırma ` Get-Module -ListAvailable AzureRM` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="f883d-114">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="f883d-115">Tooupgrade gerekirse bkz [yükleme Azure PowerShell Modülü](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="f883d-115">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="scale-set-overview"></a><span data-ttu-id="f883d-116">Ölçek kümesi'ne genel bakış</span><span class="sxs-lookup"><span data-stu-id="f883d-116">Scale Set overview</span></span>
<span data-ttu-id="f883d-117">Ölçek kümeleri kullanan benzer kavram, hakkında hello önceki öğreticide çok öğrenilen[yüksek oranda kullanılabilir sanal makineleri oluşturmak](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="f883d-117">Scale sets use similar concepts as you learned about in hello previous tutorial too[Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="f883d-118">VM ölçek kümesindeki bir kullanılabilirlik kümesindeki sanal makineleri gibi arıza ve güncelleştirme etki alanları arasında dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="f883d-118">VMs in a scale set are distributed across fault and update domains just like VMs in an availability set.</span></span>

<span data-ttu-id="f883d-119">VM ölçek kümesindeki gerektiği şekilde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="f883d-119">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="f883d-120">Otomatik ölçeklendirme kurallarını toocontrol tanımladığınız nasıl ve ne zaman VM'ler eklenir veya hello ölçek kümesinden kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="f883d-120">You define autoscale rules toocontrol how and when VMs are added or removed from hello scale set.</span></span> <span data-ttu-id="f883d-121">Bu kurallar temel alınarak ölçümleri CPU yükünü, bellek kullanımı veya ağ trafiğini gibi tetikleyebilir.</span><span class="sxs-lookup"><span data-stu-id="f883d-121">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="f883d-122">Ölçek too1, Azure platform görüntüsü kullandığınızda 000 VM'ler desteği ayarlar.</span><span class="sxs-lookup"><span data-stu-id="f883d-122">Scale sets support up too1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="f883d-123">Önemli yükleme veya VM özelleştirme gereksinimleri ile iş yükleri için çok isteyebilir[özel bir VM görüntüsü oluşturma](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="f883d-123">For workloads with significant installation or VM customization requirements, you may wish too[Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="f883d-124">Özel görüntü kullanırken ayarlayın ölçeğinde too100 Vm'leri yedekleme oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f883d-124">You can create up too100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-tooscale"></a><span data-ttu-id="f883d-125">Bir uygulama tooscale oluşturma</span><span class="sxs-lookup"><span data-stu-id="f883d-125">Create an app tooscale</span></span>
<span data-ttu-id="f883d-126">Ölçek kümesini oluşturmadan önce bir kaynak grubuyla oluşturmanız [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="f883d-126">Before you can create a scale set, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="f883d-127">Merhaba aşağıdaki örnekte oluşturur adlı bir kaynak grubu *myResourceGroupAutomate* hello içinde *EastUS* konumu:</span><span class="sxs-lookup"><span data-stu-id="f883d-127">hello following example creates a resource group named *myResourceGroupAutomate* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroupScaleSet -Location EastUS
```

<span data-ttu-id="f883d-128">Önceki bir öğreticide, nasıl çok öğrenilen[otomatikleştirmek VM Yapılandırması](tutorial-automate-vm-deployment.md) kullanarak hello özel betik uzantısı.</span><span class="sxs-lookup"><span data-stu-id="f883d-128">In an earlier tutorial, you learned how too[Automate VM configuration](tutorial-automate-vm-deployment.md) using hello Custom Script Extension.</span></span> <span data-ttu-id="f883d-129">Ölçek kümesi yapılandırması oluşturun, sonra özel betik uzantısının tooinstall uygulamak ve IIS yapılandırma:</span><span class="sxs-lookup"><span data-stu-id="f883d-129">Create a scale set configuration then apply a Custom Script Extension tooinstall and configure IIS:</span></span>

```powershell
# Create a config object
$vmssConfig = New-AzureRmVmssConfig `
    -Location EastUS `
    -SkuCapacity 2 `
    -SkuName Standard_DS2 `
    -UpgradePolicyMode Automatic

# Define hello script for your Custom Script Extension toorun
$publicSettings = @{
    "fileUris" = (,"https://raw.githubusercontent.com/iainfoulds/azure-samples/master/automate-iis.ps1");
    "commandToExecute" = "powershell -ExecutionPolicy Unrestricted -File automate-iis.ps1"
}

# Use Custom Script Extension tooinstall IIS and configure basic website
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig `
    -Name "customScript" `
    -Publisher "Microsoft.Compute" `
    -Type "CustomScriptExtension" `
    -TypeHandlerVersion 1.8 `
    -Setting $publicSettings
```

## <a name="create-scale-load-balancer"></a><span data-ttu-id="f883d-130">Ölçek yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="f883d-130">Create scale load balancer</span></span>
<span data-ttu-id="f883d-131">Bir Azure yük dengeleyici gelen trafiği sağlıklı VM'ler arasında dağıtarak yüksek kullanılabilirlik sağlayan bir katman 4 (TCP, UDP) yük dengeleyicidir.</span><span class="sxs-lookup"><span data-stu-id="f883d-131">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="f883d-132">Bir yük dengeleyici durum araştırması her VM üzerinde belirli bir bağlantı noktasını izler ve yalnızca trafik tooan dağıtır işletimsel VM.</span><span class="sxs-lookup"><span data-stu-id="f883d-132">A load balancer health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span> <span data-ttu-id="f883d-133">Daha fazla bilgi için hello sonraki öğretici bakın [nasıl tooload Bakiye Windows sanal makineleri](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="f883d-133">For more information, see hello next tutorial on [How tooload balance Windows virtual machines](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="f883d-134">Bir ortak IP adresi ve bağlantı noktası 80 üzerinde web trafiği dağıtan bir yük dengeleyicisi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="f883d-134">Create a load balancer that has a public IP address and distributes web traffic on port 80:</span></span>

```powershell
# Create a public IP address
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupScaleSet `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP

# Create a frontend and backend IP pool
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool

# Create hello load balancer
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool

# Create a load balancer health probe on port 80
Add-AzureRmLoadBalancerProbeConfig -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2

# Create a load balancer rule toodistribute traffic on port 80
Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80

# Update hello load balancer configuration
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

## <a name="create-a-scale-set"></a><span data-ttu-id="f883d-135">Bir ölçek kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="f883d-135">Create a scale set</span></span>
<span data-ttu-id="f883d-136">Şimdi bir sanal makine ölçek kümesi oluşturmak [yeni AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="f883d-136">Now create a virtual machine scale set with [New-AzureRmVmss](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="f883d-137">Merhaba aşağıdaki örnekte oluşturur ölçeği adlandırılmış Ayarla *myScaleSet*:</span><span class="sxs-lookup"><span data-stu-id="f883d-137">hello following example creates a scale set named *myScaleSet*:</span></span>

```powershell
# Reference a virtual machine image from hello gallery
Set-AzureRmVmssStorageProfile $vmssConfig `
  -ImageReferencePublisher MicrosoftWindowsServer `
  -ImageReferenceOffer WindowsServer `
  -ImageReferenceSku 2016-Datacenter `
  -ImageReferenceVersion latest

# Set up information for authenticating with hello virtual machine
Set-AzureRmVmssOsProfile $vmssConfig `
  -AdminUsername azureuser `
  -AdminPassword P@ssword! `
  -ComputerNamePrefix myVM

# Create hello virtual network resources
$subnet = New-AzureRmVirtualNetworkSubnetConfig `
  -Name "mySubnet" `
  -AddressPrefix 10.0.0.0/24
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName "myResourceGroupScaleSet" `
  -Name "myVnet" `
  -Location "EastUS" `
  -AddressPrefix 10.0.0.0/16 `
  -Subnet $subnet
$ipConfig = New-AzureRmVmssIpConfig `
  -Name "myIPConfig" `
  -LoadBalancerBackendAddressPoolsId $lb.BackendAddressPools[0].Id `
  -SubnetId $vnet.Subnets[0].Id

# Attach hello virtual network toohello config object
Add-AzureRmVmssNetworkInterfaceConfiguration `
  -VirtualMachineScaleSet $vmssConfig `
  -Name "network-config" `
  -Primary $true `
  -IPConfiguration $ipConfig

# Create hello scale set with hello config object (this step might take a few minutes)
New-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -Name myScaleSet `
  -VirtualMachineScaleSet $vmssConfig
```

<span data-ttu-id="f883d-138">Birkaç dakika toocreate alır ve tüm hello ölçek kümesi kaynakları ve VM'ler yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f883d-138">It takes a few minutes toocreate and configure all hello scale set resources and VMs.</span></span>


## <a name="test-your-app"></a><span data-ttu-id="f883d-139">Uygulamanızı test etme</span><span class="sxs-lookup"><span data-stu-id="f883d-139">Test your app</span></span>
<span data-ttu-id="f883d-140">toosee, IIS Web sitesi eylem elde hello genel IP adresi, yük dengeleyici ile [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="f883d-140">toosee your IIS website in action, obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="f883d-141">Merhaba aşağıdaki örnek alacağı için başlangıç IP adresi *myPublicIP* hello ölçek kümesinin bir parçası olarak oluşturulan:</span><span class="sxs-lookup"><span data-stu-id="f883d-141">hello following example obtains hello IP address for *myPublicIP* created as part of hello scale set:</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroupScaleSet -Name myPublicIP | select IpAddress
```

<span data-ttu-id="f883d-142">Tooa web tarayıcısında Hello genel IP adresi girin.</span><span class="sxs-lookup"><span data-stu-id="f883d-142">Enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="f883d-143">VM bu hello yük dengeleyici dağıtılmış trafiği hello hello ana dahil olmak üzere Hello uygulama görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="f883d-143">hello app is displayed, including hello hostname of hello VM that hello load balancer distributed traffic to:</span></span>

![Çalışan IIS sitesi](./media/tutorial-create-vmss/running-iis-site.png)

<span data-ttu-id="f883d-145">toosee hello ölçeği, eylemde ayarla, zorla yenileme web tarayıcısı toosee hello yük dengeleyici, uygulamanızı çalıştıran tüm hello VM'ler arasında trafiği dağıtın.</span><span class="sxs-lookup"><span data-stu-id="f883d-145">toosee hello scale set in action, you can force-refresh your web browser toosee hello load balancer distribute traffic across all hello VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="f883d-146">Yönetim görevleri</span><span class="sxs-lookup"><span data-stu-id="f883d-146">Management tasks</span></span>
<span data-ttu-id="f883d-147">Merhaba ölçek kümesini Hello yaşam döngüsü boyunca toorun gerekebilir bir veya daha fazla yönetim görevleri.</span><span class="sxs-lookup"><span data-stu-id="f883d-147">Throughout hello lifecycle of hello scale set, you may need toorun one or more management tasks.</span></span> <span data-ttu-id="f883d-148">Ayrıca, çeşitli yaşam döngüsü görevleri otomatikleştiren toocreate komut dosyaları isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f883d-148">Additionally, you may want toocreate scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="f883d-149">Azure PowerShell Bu görevleri hızlı şekilde toodo sağlar.</span><span class="sxs-lookup"><span data-stu-id="f883d-149">Azure PowerShell provides a quick way toodo those tasks.</span></span> <span data-ttu-id="f883d-150">Birkaç ortak görevler şunlardır.</span><span class="sxs-lookup"><span data-stu-id="f883d-150">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="f883d-151">Görünüm VM ölçek kümesindeki</span><span class="sxs-lookup"><span data-stu-id="f883d-151">View VMs in a scale set</span></span>
<span data-ttu-id="f883d-152">tooview, Ölçek çalışan sanal makineler listesi ayarlayabilir, kullanabilir [Get-AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) gibi:</span><span class="sxs-lookup"><span data-stu-id="f883d-152">tooview a list of VMs running in your scale set, use [Get-AzureRmVmssVM](/powershell/module/azurerm.compute/get-azurermvmssvm) as follows:</span></span>

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Loop through hello instanaces in your scale set
for ($i=1; $i -le ($scaleset.Sku.Capacity - 1); $i++) {
    Get-AzureRmVmssVM -ResourceGroupName myResourceGroupScaleSet `
      -VMScaleSetName myScaleSet `
      -InstanceId $i
}
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="f883d-153">Artırma veya azaltma VM örnekleri</span><span class="sxs-lookup"><span data-stu-id="f883d-153">Increase or decrease VM instances</span></span>
<span data-ttu-id="f883d-154">toosee hello örnek sayısı, şu anda bir ölçek kümesindeki, kullanın [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) ve sorgulayın *sku.capacity*:</span><span class="sxs-lookup"><span data-stu-id="f883d-154">toosee hello number of instances you currently have in a scale set, use [Get-AzureRmVmss](/powershell/module/azurerm.compute/get-azurermvmss) and query on *sku.capacity*:</span></span>

```powershell
Get-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -VMScaleSetName myScaleSet | `
    Select -ExpandProperty Sku
```

<span data-ttu-id="f883d-155">Daha sonra el ile artırabilir veya sanal makineler kümesi hello ölçeğinde hello sayısını azaltmak [güncelleştirme AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss).</span><span class="sxs-lookup"><span data-stu-id="f883d-155">You can then manually increase or decrease hello number of virtual machines in hello scale set with [Update-AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss).</span></span> <span data-ttu-id="f883d-156">Merhaba aşağıdaki örnek hello sayısını VM'ler, ölçeği çok ayarla ayarlar*5*:</span><span class="sxs-lookup"><span data-stu-id="f883d-156">hello following example sets hello number of VMs in your scale set too*5*:</span></span>

```powershell
# Get current scale set
$scaleset = Get-AzureRmVmss `
  -ResourceGroupName myResourceGroupScaleSet `
  -VMScaleSetName myScaleSet

# Set and update hello capacity of your scale set
$scaleset.sku.capacity = 5
Update-AzureRmVmss -ResourceGroupName myResourceGroupScaleSet `
    -Name myScaleSet `
    -VirtualMachineScaleSet $scaleset
```

<span data-ttu-id="f883d-157">Alır örneği sayısı birkaç dakika tooupdate hello belirttiyseniz, Ölçek kümesi.</span><span class="sxs-lookup"><span data-stu-id="f883d-157">If takes a few minutes tooupdate hello specified number of instances in your scale set.</span></span>


### <a name="configure-autoscale-rules"></a><span data-ttu-id="f883d-158">Otomatik ölçeklendirme kurallarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f883d-158">Configure autoscale rules</span></span>
<span data-ttu-id="f883d-159">El ile Merhaba örnek sayısı, Ölçek ölçeklendirmesini Ayarla yerine otomatik ölçeklendirme kurallarını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="f883d-159">Rather than manually scaling hello number of instances in your scale set, you define autoscale rules.</span></span> <span data-ttu-id="f883d-160">Bu kurallar, Ölçek durumlarda ayarlayın ve buna göre ölçümleri ve tanımladığınız eşikleri göre yanıt hello izleyin.</span><span class="sxs-lookup"><span data-stu-id="f883d-160">These rules monitor hello instances in your scale set and respond accordingly based on metrics and thresholds you define.</span></span> <span data-ttu-id="f883d-161">Hello ortalama CPU yükü 5 dakikalık bir süre içinde % 60'den büyük olduğunda aşağıdaki örneğine hello tarafından hello örneklerinin sayısını ölçeklendirir.</span><span class="sxs-lookup"><span data-stu-id="f883d-161">hello following example scales out hello number of instances by one when hello average CPU load is greater than 60% over a 5 minute period.</span></span> <span data-ttu-id="f883d-162">Merhaba ortalama CPU yükü daha sonra 5 dakikalık bir süre içinde % 30 düşerse hello örnekleri içinde bir örneği tarafından ölçeklenir:</span><span class="sxs-lookup"><span data-stu-id="f883d-162">If hello average CPU load then drops below 30% over a 5 minute period, hello instances are scaled in by one instance:</span></span>

```powershell
# Define your scale set information
$mySubscriptionId = (Get-AzureRmSubscription).Id
$myResourceGroup = "myResourceGroupScaleSet"
$myScaleSet = "myScaleSet"
$myLocation = "East US"

# Create a scale up rule tooincrease hello number instances after 60% average CPU usage exceeded for a 5 minute period
$myRuleScaleUp = New-AzureRmAutoscaleRule `
  -MetricName "Percentage CPU" `
  -MetricResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -Operator GreaterThan `
  -MetricStatistic Average `
  -Threshold 60 `
  -TimeGrain 00:01:00 `
  -TimeWindow 00:05:00 `
  -ScaleActionCooldown 00:05:00 `
  -ScaleActionDirection Increase `
  -ScaleActionValue 1

# Create a scale down rule toodecrease hello number of instances after 30% average CPU usage over a 5 minute period
$myRuleScaleDown = New-AzureRmAutoscaleRule `
  -MetricName "Percentage CPU" `
  -MetricResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -Operator LessThan `
  -MetricStatistic Average `
  -Threshold 30 `
  -TimeGrain 00:01:00 `
  -TimeWindow 00:05:00 `
  -ScaleActionCooldown 00:05:00 `
  -ScaleActionDirection Decrease `
  -ScaleActionValue 1

# Create a scale profile with your scale up and scale down rules
$myScaleProfile = New-AzureRmAutoscaleProfile `
  -DefaultCapacity 2  `
  -MaximumCapacity 10 `
  -MinimumCapacity 2 `
  -Rules $myRuleScaleUp,$myRuleScaleDown `
  -Name "autoprofile"

# Apply hello autoscale rules
Add-AzureRmAutoscaleSetting `
  -Location $myLocation `
  -Name "autosetting" `
  -ResourceGroup $myResourceGroup `
  -TargetResourceId /subscriptions/$mySubscriptionId/resourceGroups/$myResourceGroup/providers/Microsoft.Compute/virtualMachineScaleSets/$myScaleSet `
  -AutoscaleProfiles $myScaleProfile
```


## <a name="next-steps"></a><span data-ttu-id="f883d-163">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f883d-163">Next steps</span></span>
<span data-ttu-id="f883d-164">Bu öğreticide, bir sanal makine ölçek kümesi oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="f883d-164">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="f883d-165">Şunları öğrendiniz:</span><span class="sxs-lookup"><span data-stu-id="f883d-165">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="f883d-166">Merhaba özel betik uzantısının toodefine bir IIS site tooscale kullanın</span><span class="sxs-lookup"><span data-stu-id="f883d-166">Use hello Custom Script Extension toodefine an IIS site tooscale</span></span>
> * <span data-ttu-id="f883d-167">Ölçek kümesi için bir yük dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="f883d-167">Create a load balancer for your scale set</span></span>
> * <span data-ttu-id="f883d-168">Bir sanal makine ölçek kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="f883d-168">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="f883d-169">Artırma veya azaltma hello ölçek kümesi örneği sayısı</span><span class="sxs-lookup"><span data-stu-id="f883d-169">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="f883d-170">Otomatik ölçeklendirme kuralları oluşturma</span><span class="sxs-lookup"><span data-stu-id="f883d-170">Create autoscale rules</span></span>

<span data-ttu-id="f883d-171">Toohello sonraki öğretici toolearn Yük Dengeleme sanal makineler için kavramları hakkında daha fazla ilerleyin.</span><span class="sxs-lookup"><span data-stu-id="f883d-171">Advance toohello next tutorial toolearn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f883d-172">Sanal makinelerin yük dengelemesini</span><span class="sxs-lookup"><span data-stu-id="f883d-172">Load balance virtual machines</span></span>](tutorial-load-balancer.md)
