---
title: "Sanal makine ölçek aaaCreating ayarlar PowerShell cmdlet'lerini kullanarak | Microsoft Docs"
description: "Oluşturma ve İlk Azure sanal makine ölçek Azure PowerShell cmdlet'lerini kullanarak kümelerinizi yönetme kullanmaya başlama"
services: virtual-machines-windows
documentationcenter: 
author: danielsollondon
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 430d9d64-1f35-48f0-a4fd-9b69910ffa59
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/21/2017
ms.author: danielsollondon
ms.openlocfilehash: 7979be367d04c904b60d78849c1b751a52cc8caf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-virtual-machine-scale-sets-using-powershell-cmdlets"></a><span data-ttu-id="0aa05-103">PowerShell cmdlet'leri kullanılarak sanal makine ölçek kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="0aa05-103">Creating Virtual Machine Scale Sets using PowerShell cmdlets</span></span>
<span data-ttu-id="0aa05-104">Bu makalede nasıl toocreate (VMSS) bir sanal makine ölçek kümesi örnek anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0aa05-104">This article walks through an example of how toocreate a Virtual Machine scale set (VMSS).</span></span> <span data-ttu-id="0aa05-105">İlişkili ağ ve depolama ile üç düğümü ölçek kümesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0aa05-105">It creates a scale set of three nodes, with associated Networking and Storage.</span></span>

## <a name="first-steps"></a><span data-ttu-id="0aa05-106">İlk adımlar</span><span class="sxs-lookup"><span data-stu-id="0aa05-106">First Steps</span></span>
<span data-ttu-id="0aa05-107">Merhaba yüklü en son Azure PowerShell modülü vardır, toomake hello PowerShell cmdlet'leri sahip olduğunuzdan emin toomaintain gereken ve ölçek kümeleri oluşturma emin olun.</span><span class="sxs-lookup"><span data-stu-id="0aa05-107">Ensure you have hello latest Azure PowerShell module installed, toomake sure you have hello PowerShell commandlets needed toomaintain, and create scale sets.</span></span>
<span data-ttu-id="0aa05-108">Toohello komut satırı araçları Git [burada](http://aka.ms/webpi-azps) hello en son kullanılabilir Azure modüller.</span><span class="sxs-lookup"><span data-stu-id="0aa05-108">Go toohello command line tools [here](http://aka.ms/webpi-azps) for hello latest available Azure Modules.</span></span>

<span data-ttu-id="0aa05-109">toofind VMSS ilgili cmdlet'leri, hello arama dizesi kullanın \*VMSS\*.</span><span class="sxs-lookup"><span data-stu-id="0aa05-109">toofind VMSS related commandlets, use hello search string \*VMSS\*.</span></span> <span data-ttu-id="0aa05-110">Örneğin, _gcm *vmss*_</span><span class="sxs-lookup"><span data-stu-id="0aa05-110">For example, _gcm *vmss*_</span></span>

## <a name="creating-a-vmss"></a><span data-ttu-id="0aa05-111">Bir VMSS oluşturma</span><span class="sxs-lookup"><span data-stu-id="0aa05-111">Creating a VMSS</span></span>
#### <a name="create-resource-group"></a><span data-ttu-id="0aa05-112">Kaynak Grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="0aa05-112">Create Resource Group</span></span>
```
$loc = 'westus';
$rgname = 'mynewrgwu';
  New-AzureRmResourceGroup -Name $rgname -Location $loc -Force;
```

### <a name="create-networking-vnet--subnet"></a><span data-ttu-id="0aa05-113">Ağ oluşturma (VNET / alt ağ)</span><span class="sxs-lookup"><span data-stu-id="0aa05-113">Create Networking (VNET / Subnet)</span></span>
#### <a name="subnet-specification"></a><span data-ttu-id="0aa05-114">Alt ağ belirtimi</span><span class="sxs-lookup"><span data-stu-id="0aa05-114">Subnet Specification</span></span>
```
$subnetName = 'websubnet'
  $subnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix "10.0.0.0/24";
```

#### <a name="vnet-specification"></a><span data-ttu-id="0aa05-115">VNET belirtimi</span><span class="sxs-lookup"><span data-stu-id="0aa05-115">VNET Specification</span></span>
```
$vnet = New-AzureRmVirtualNetwork -Force -Name ('vnet' + $rgname) -ResourceGroupName $rgname -Location $loc -AddressPrefix "10.0.0.0/16" -Subnet $subnet;
$vnet = Get-AzureRmVirtualNetwork -Name ('vnet' + $rgname) -ResourceGroupName $rgname;

# In this case assume hello new subnet is hello only one
$subnetId = $vnet.Subnets[0].Id;
```

#### <a name="create-public-ip-resource-tooallow-external-access"></a><span data-ttu-id="0aa05-116">Genel IP kaynağı tooAllow dış erişim oluşturma</span><span class="sxs-lookup"><span data-stu-id="0aa05-116">Create Public IP Resource tooAllow External Access</span></span>
<span data-ttu-id="0aa05-117">Bu yük dengeleyici ilişkili toohello olacaktır.</span><span class="sxs-lookup"><span data-stu-id="0aa05-117">This will be bound toohello Load Balancer.</span></span>

```
$pubip = New-AzureRmPublicIpAddress -Force -Name ('pubip' + $rgname) -ResourceGroupName $rgname -Location $loc -AllocationMethod Dynamic -DomainNameLabel ('pubip' + $rgname);
$pubip = Get-AzureRmPublicIpAddress -Name ('pubip' + $rgname) -ResourceGroupName $rgname;
```

#### <a name="create-load-balancer"></a><span data-ttu-id="0aa05-118">Yük Dengeleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="0aa05-118">Create Load Balancer</span></span>
```
$frontendName = 'fe' + $rgname
$backendAddressPoolName = 'bepool' + $rgname
$probeName = 'vmssprobe' + $rgname
$inboundNatPoolName = 'innatpool' + $rgname
$lbruleName = 'lbrule' + $rgname
$lbName = 'vmsslb' + $rgname

# Bind Public IP tooLoad Balancer
$frontend = New-AzureRmLoadBalancerFrontendIpConfig -Name $frontendName -PublicIpAddress $pubip
```

#### <a name="configure-load-balancer"></a><span data-ttu-id="0aa05-119">Yük Dengeleyici yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0aa05-119">Configure Load Balancer</span></span>
<span data-ttu-id="0aa05-120">Arka uç adres havuzu yapılandırma oluşturabilir, bu hello ölçek kümesinde hello VM'ler hello NIC tarafından paylaşılır.</span><span class="sxs-lookup"><span data-stu-id="0aa05-120">Create Backend Address Pool Config, this will be shared by hello NICs of hello VMs in hello scale set.</span></span>

```
$backendAddressPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name $backendAddressPoolName
```

<span data-ttu-id="0aa05-121">Yük dengeli sonda bağlantı noktası kümesi, uygulamanız için uygun şekilde hello ayarlarını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="0aa05-121">Set Load Balanced Probe Port, change hello settings as appropriate for your application.</span></span>

```
$probe = New-AzureRmLoadBalancerProbeConfig -Name $probeName -RequestPath healthcheck.aspx -Protocol http -Port 80 -IntervalInSeconds 15 -ProbeCount 2
```

<span data-ttu-id="0aa05-122">Doğrudan yönlendirilmiş bağlantı (yükü dengelenmiş) için bir gelen NAT havuzu oluşturma toohello VM'ler hello ölçeğinde yük dengeleyici hello ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="0aa05-122">Create an inbound NAT pool for direct routed connectivity (not load balanced) toohello VMs in hello scale set via hello Load Balancer.</span></span> <span data-ttu-id="0aa05-123">Bu RDP kullanarak toodemonstrate ve uygulamanızda gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="0aa05-123">This is toodemonstrate using RDP and may not be required in your application.</span></span>

```
$frontendpoolrangestart = 3360
$frontendpoolrangeend = 3370
$backendvmport = 3389
$inboundNatPool = New-AzureRmLoadBalancerInboundNatPoolConfig -Name $inboundNatPoolName -FrontendIPConfigurationId `
$frontend.Id -Protocol Tcp -FrontendPortRangeStart $frontendpoolrangestart -FrontendPortRangeEnd $frontendpoolrangeend -BackendPort $backendvmport;
```

<span data-ttu-id="0aa05-124">Merhaba yük dengeli kuralı gösterir yük önceki adımlardan hello ayarlarını kullanarak Dengeleme bağlantı noktası 80 isteklerini bu örnek oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0aa05-124">Create hello Load Balanced Rule, this example shows load balancing port 80 requests, using hello settings from previous steps.</span></span>

```
$protocol = 'Tcp'
$feLBPort = 80
$beLBPort = 80

$lbrule = New-AzureRmLoadBalancerRuleConfig -Name $lbruleName `
-FrontendIPConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -Protocol $protocol -FrontendPort $feLBPort -BackendPort $beLBPort `
-IdleTimeoutInMinutes 15 -EnableFloatingIP -LoadDistribution SourceIP -Verbose;
```

<span data-ttu-id="0aa05-125">Yük Dengeleyici yapılandırması ile oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0aa05-125">Create Load Balancer with configuration.</span></span>

```
$actualLb = New-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname -Location $loc `
-FrontendIpConfiguration $frontend -BackendAddressPool $backendAddressPool `
-Probe $probe -LoadBalancingRule $lbrule -InboundNatPool $inboundNatPool -Verbose;
```

<span data-ttu-id="0aa05-126">LB ayarlarını denetleyin, yük denetleyin dengeli bağlantı noktası yapılandırmaları, Not, görmezsiniz hello ölçek kümesindeki sanal makineleri hello kadar gelen NAT kuralları oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="0aa05-126">Check  LB settings, check load balanced port configs, note, you will not see Inbound NAT rules until hello VMs in hello scale set are created.</span></span>

```
$expectedLb = Get-AzureRmLoadBalancer -Name $lbName -ResourceGroupName $rgname
```

##### <a name="configure-and-create-hello-scale-set"></a><span data-ttu-id="0aa05-127">Yapılandırma ve oluşturma hello ölçek kümesi</span><span class="sxs-lookup"><span data-stu-id="0aa05-127">Configure and Create hello scale set</span></span>
<span data-ttu-id="0aa05-128">Not: Bu altyapı örnek nasıl tooset yukarı dağıtmak ve ölçek web trafiği hello ölçek kümesini ancak hello VM'ler burada belirtilen görüntüleri üzerinden yüklü hiçbir web Hizmetleri yok gösterir.</span><span class="sxs-lookup"><span data-stu-id="0aa05-128">Note, this infrastructure example shows how tooset up distribute and scale web traffic across hello scale set, but hello VMs Images specified here do not have any web services installed.</span></span>

```
# specify scale set Name
$vmssName = 'vmss' + $rgname;

## specify VMSS specific details
$adminUsername = 'azadmin';
$adminPassword = "Password1234!";

$PublisherName = 'MicrosoftWindowsServer'
$Offer         = 'WindowsServer'
$Sku          = '2012-R2-Datacenter'
$Version       = 'latest'
$vmNamePrefix = 'winvmss'

###add an extension
$extname = 'BGInfo';
$publisher = 'Microsoft.Compute';
$exttype = 'BGInfo';
$extver = '2.1';
```

<span data-ttu-id="0aa05-129">NIC tooLoad dengeleyici ve alt ağ bağlama</span><span class="sxs-lookup"><span data-stu-id="0aa05-129">Bind NIC tooLoad Balancer and Subnet</span></span>

```
$ipCfg = New-AzureRmVmssIPConfig -Name 'nic' `
-LoadBalancerInboundNatPoolsId $actualLb.InboundNatPools[0].Id `
-LoadBalancerBackendAddressPoolsId $actualLb.BackendAddressPools[0].Id `
-SubnetId $subnetId;
```

<span data-ttu-id="0aa05-130">Ölçeği oluşturmak set Config</span><span class="sxs-lookup"><span data-stu-id="0aa05-130">Create scale set Config</span></span>

```
# Specify number of nodes
$numberofnodes = 3

$vmss = New-AzureRmVmssConfig -Location $loc -SkuCapacity $numberofnodes -SkuName 'Standard_A2' -UpgradePolicyMode 'automatic' `
    | Add-AzureRmVmssNetworkInterfaceConfiguration -Name $subnetName -Primary $true -IPConfiguration $ipCfg `
    | Set-AzureRmVmssOSProfile -ComputerNamePrefix $vmNamePrefix -AdminUsername $adminUsername -AdminPassword $adminPassword `
    | Set-AzureRmVmssStorageProfile -OsDiskCreateOption 'FromImage' -OsDiskCaching 'None' `
    -ImageReferenceOffer $Offer -ImageReferenceSku $Sku -ImageReferenceVersion $Version `
    -ImageReferencePublisher $PublisherName `
    | Add-AzureRmVmssExtension -Name $extname -Publisher $publisher -Type $exttype -TypeHandlerVersion $extver -AutoUpgradeMinorVersion $true
```

<span data-ttu-id="0aa05-131">Derleme ölçek kümesi yapılandırması</span><span class="sxs-lookup"><span data-stu-id="0aa05-131">Build scale set configuration</span></span>

```
New-AzureRmVmss -ResourceGroupName $rgname -Name $vmssName -VirtualMachineScaleSet $vmss -Verbose;
```

<span data-ttu-id="0aa05-132">Şimdi hello ölçek kümesini oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="0aa05-132">Now you have created hello scale set.</span></span> <span data-ttu-id="0aa05-133">Bağlantı toohello sınayabilirsiniz Bu örnekte, RDP kullanarak tek tek VM:</span><span class="sxs-lookup"><span data-stu-id="0aa05-133">You can test connecting toohello individual VM using RDP in this example:</span></span>

```
VM0 : pubipmynewrgwu.westus.cloudapp.azure.com:3360
VM1 : pubipmynewrgwu.westus.cloudapp.azure.com:3361
VM2 : pubipmynewrgwu.westus.cloudapp.azure.com:3362
```
