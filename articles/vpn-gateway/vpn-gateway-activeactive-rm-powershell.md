---
title: "VPN ağ geçitleri için etkin-etkin S2S VPN bağlantılarını yapılandırma: Azure Resource Manager: PowerShell | Microsoft Docs"
description: "Bu makalede Azure Resource Manager ve PowerShell kullanarak Azure VPN Gateway'ler ile etkin-etkin bağlantıları nasıl yapılandıracağınız anlatılmaktadır."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2017
ms.author: yushwang
ms.openlocfilehash: 964eedc7698e42bf0e082f0105845f2a339daf57
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-active-s2s-vpn-connections-with-azure-vpn-gateways"></a><span data-ttu-id="ea1a3-103">Azure VPN ağ geçitleri ile etkin-etkin S2S VPN bağlantılarını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ea1a3-103">Configure active-active S2S VPN connections with Azure VPN Gateways</span></span>

<span data-ttu-id="ea1a3-104">Bu makalede hello adımları toocreate etkin-etkin şirket içi ve hello Resource Manager dağıtım modeli ve PowerShell kullanarak VNet-VNet bağlantıları anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-104">This article walks you through hello steps toocreate active-active cross-premises and VNet-to-VNet connections using hello Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-highly-available-cross-premises-connections"></a><span data-ttu-id="ea1a3-105">Yüksek oranda kullanılabilir şirket içi bağlantılar hakkında</span><span class="sxs-lookup"><span data-stu-id="ea1a3-105">About Highly Available Cross-Premises Connections</span></span>
<span data-ttu-id="ea1a3-106">tooachieve yüksek kullanılabilirlik şirketler arası ve VNet-VNet bağlantısı için birden çok VPN ağ geçidi dağıtmak ve birden çok paralel ağlarınız ve Azure arasında bağlantı kurabilir gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-106">tooachieve high availability for cross-premises and VNet-to-VNet connectivity, you should deploy multiple VPN gateways and establish multiple parallel connections between your networks and Azure.</span></span> <span data-ttu-id="ea1a3-107">Lütfen bakın [yüksek oranda kullanılabilir şirketler arası ve VNet-VNet bağlantısı](vpn-gateway-highlyavailable.md) bağlantı seçenekleri ve topolojisini genel bakış.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-107">Please see [Highly Available Cross-Premises and VNet-to-VNet Connectivity](vpn-gateway-highlyavailable.md) for an overview of connectivity options and topology.</span></span>

<span data-ttu-id="ea1a3-108">Bu makalede bir aktif-aktif yukarı tooset VPN bağlantısı ve iki sanal ağlar arasında etkin-etkin bağlantı şirketler arası hello yönergeler sağlar:</span><span class="sxs-lookup"><span data-stu-id="ea1a3-108">This article provides hello instructions tooset up an active-active cross-premises VPN connection, and active-active connection between two virtual networks:</span></span>

* [<span data-ttu-id="ea1a3-109">Bölüm 1 - oluşturun ve Azure VPN ağ geçidinizi etkin-etkin modunda yapılandırın</span><span class="sxs-lookup"><span data-stu-id="ea1a3-109">Part 1 - Create and configure your Azure VPN gateway in active-active mode</span></span>](#aagateway)
* [<span data-ttu-id="ea1a3-110">Bölüm 2 - etkin-etkin şirketler arası bağlantı</span><span class="sxs-lookup"><span data-stu-id="ea1a3-110">Part 2 - Establish active-active cross-premises connections</span></span>](#aacrossprem)
* [<span data-ttu-id="ea1a3-111">Bölüm 3 - etkin-etkin VNet-VNet bağlantıları kurmak</span><span class="sxs-lookup"><span data-stu-id="ea1a3-111">Part 3 - Establish active-active VNet-to-VNet connections</span></span>](#aav2v)
* [<span data-ttu-id="ea1a3-112">Bölüm 4 - Güncelleştirme etkin-etkin ve etkin bekleme arasında varolan ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="ea1a3-112">Part 4 - Update existing gateway between active-active and active-standby</span></span>](#aaupdate)

<span data-ttu-id="ea1a3-113">Bu arada toobuild ihtiyaçlarınıza uygun bir yüksek oranda kullanılabilir, daha karmaşık ağ topolojisi birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-113">You can combine these together toobuild a more complex, highly available network topology that meets your needs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ea1a3-114">Lütfen bu hello etkin-etkin modu SKU'ları aşağıdaki yalnızca hello kullandığına dikkat edin:</span><span class="sxs-lookup"><span data-stu-id="ea1a3-114">Please note that hello active-active mode uses only hello following SKUs:</span></span> 
  * <span data-ttu-id="ea1a3-115">VpnGw1, VpnGw2, VpnGw3</span><span class="sxs-lookup"><span data-stu-id="ea1a3-115">VpnGw1, VpnGw2, VpnGw3</span></span>
  * <span data-ttu-id="ea1a3-116">HighPerformance (için eski eski SKU)</span><span class="sxs-lookup"><span data-stu-id="ea1a3-116">HighPerformance (for old legacy SKUs)</span></span>
> 
> 

## <span data-ttu-id="ea1a3-117"><a name ="aagateway"></a>Bölüm 1 - oluşturma ve etkin-etkin VPN ağ geçitlerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ea1a3-117"><a name ="aagateway"></a>Part 1 - Create and configure active-active VPN gateways</span></span>
<span data-ttu-id="ea1a3-118">Aşağıdaki adımları hello Azure VPN ağ geçidinizi etkin-etkin modlarında yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-118">hello following steps will configure your Azure VPN gateway in active-active modes.</span></span> <span data-ttu-id="ea1a3-119">Merhaba arasındaki farklar hello etkin-etkin ve etkin bekleme ağ geçitleri:</span><span class="sxs-lookup"><span data-stu-id="ea1a3-119">hello key differences between hello active-active and active-standby gateways:</span></span>

* <span data-ttu-id="ea1a3-120">İki ortak IP adresi ile iki ağ geçidi IP yapılandırması toocreate gerekir</span><span class="sxs-lookup"><span data-stu-id="ea1a3-120">You need toocreate two Gateway IP configurations with two public IP addresses</span></span>
* <span data-ttu-id="ea1a3-121">Merhaba EnableActiveActiveFeature bayrağı ayarlı</span><span class="sxs-lookup"><span data-stu-id="ea1a3-121">You need set hello EnableActiveActiveFeature flag</span></span>
* <span data-ttu-id="ea1a3-122">Merhaba ağ geçidi SKU'su VpnGw1, VpnGw2, VpnGw3 veya HighPerformance (eski SKU) olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-122">hello gateway SKU must be VpnGw1, VpnGw2, VpnGw3, or HighPerformance (legacy SKU).</span></span>

<span data-ttu-id="ea1a3-123">Merhaba diğer özellikleri olan hello hello etkin-etkin olmayan ağ geçitleri ile aynı.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-123">hello other properties are hello same as hello non-active-active gateways.</span></span> 

### <a name="before-you-begin"></a><span data-ttu-id="ea1a3-124">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="ea1a3-124">Before you begin</span></span>
* <span data-ttu-id="ea1a3-125">Azure aboneliğiniz olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-125">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="ea1a3-126">Henüz Azure aboneliğiniz yoksa [MSDN abonelik avantajlarınızı](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) etkinleştirebilir veya [ücretsiz bir hesap](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-126">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ea1a3-127">Tooinstall hello Azure Resource Manager PowerShell cmdlet'lerini gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-127">You'll need tooinstall hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="ea1a3-128">Bkz: [Azure PowerShell genel bakış](/powershell/azure/overview) hello PowerShell cmdlet'lerini yükleme hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-128">See [Overview of Azure PowerShell](/powershell/azure/overview) for more information about installing hello PowerShell cmdlets.</span></span>

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="ea1a3-129">1. adım - oluşturun ve VNet1 yapılandırın</span><span class="sxs-lookup"><span data-stu-id="ea1a3-129">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="ea1a3-130">1. Değişkenlerinizi bildirme</span><span class="sxs-lookup"><span data-stu-id="ea1a3-130">1. Declare your variables</span></span>
<span data-ttu-id="ea1a3-131">Bu alıştırmaya değişkenlerimizi bildirerek başlayacağız.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-131">For this exercise, we'll start by declaring our variables.</span></span> <span data-ttu-id="ea1a3-132">Merhaba örnekte bu alıştırmada hello değerleri kullanarak hello değişkenler bildirilmektedir.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-132">hello example below declares hello variables using hello values for this exercise.</span></span> <span data-ttu-id="ea1a3-133">Üretim için yapılandırma emin tooreplace hello değerleri kendi değerlerinizle olabilir.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-133">Be sure tooreplace hello values with your own when configuring for production.</span></span> <span data-ttu-id="ea1a3-134">Merhaba adımları toobecome yapılandırma bu tür tanıdık aracılığıyla çalıştırıyorsanız, bu değişkenleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-134">You can use these variables if you are running through hello steps toobecome familiar with this type of configuration.</span></span> <span data-ttu-id="ea1a3-135">Merhaba değişkenleri değiştirin ve sonra kopyalayın ve PowerShell konsolunuza yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-135">Modify hello variables, and then copy and paste into your PowerShell console.</span></span>

```powershell
$Sub1 = "Ross"
$RG1 = "TestAARG1"
$Location1 = "West US"
$VNetName1 = "TestVNet1"
$FESubName1 = "FrontEnd"
$BESubName1 = "Backend"
$GWSubName1 = "GatewaySubnet"
$VNetPrefix11 = "10.11.0.0/16"
$VNetPrefix12 = "10.12.0.0/16"
$FESubPrefix1 = "10.11.0.0/24"
$BESubPrefix1 = "10.12.0.0/24"
$GWSubPrefix1 = "10.12.255.0/27"
$VNet1ASN = 65010
$DNS1 = "8.8.8.8"
$GWName1 = "VNet1GW"
$GW1IPName1 = "VNet1GWIP1"
$GW1IPName2 = "VNet1GWIP2"
$GW1IPconf1 = "gw1ipconf1"
$GW1IPconf2 = "gw1ipconf2"
$Connection12 = "VNet1toVNet2"
$Connection151 = "VNet1toSite5_1"
$Connection152 = "VNet1toSite5_2"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="ea1a3-136">2. Tooyour abonelik bağlanın ve yeni bir kaynak grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="ea1a3-136">2. Connect tooyour subscription and create a new resource group</span></span>
<span data-ttu-id="ea1a3-137">TooPowerShell modu toouse hello Resource Manager cmdlet'lerini geçtiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-137">Make sure you switch tooPowerShell mode toouse hello Resource Manager cmdlets.</span></span> <span data-ttu-id="ea1a3-138">Daha fazla bilgi için [Windows PowerShell’i Resource Manager ile kullanma](../powershell-azure-resource-manager.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-138">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="ea1a3-139">PowerShell Konsolunuzu açın ve tooyour hesap bağlanın.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-139">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="ea1a3-140">Bağlandığınız örnek toohelp aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="ea1a3-140">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="ea1a3-141">3. TestVNet1 oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea1a3-141">3. Create TestVNet1</span></span>
<span data-ttu-id="ea1a3-142">Aşağıdaki Hello örneği TestVNet1 ve üç alt ağ, biri GatewaySubnet, biri FrontEnd ve diğeri Backend'dir adlı bir sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-142">hello sample below creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="ea1a3-143">Kendi değerlerinizi yerleştirirken ağ geçidi alt ağınızı özellikle GatewaySubnet olarak adlandırmanız önem taşır.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-143">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="ea1a3-144">Başka bir ad kullanırsanız ağ oluşturma işleminiz başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-144">If you name it something else, your gateway creation will fail.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-active-active-mode"></a><span data-ttu-id="ea1a3-145">2. adım - etkin-etkin moduyla TestVNet1 için hello VPN ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea1a3-145">Step 2 - Create hello VPN gateway for TestVNet1 with active-active mode</span></span>
#### <a name="1-create-hello-public-ip-addresses-and-gateway-ip-configurations"></a><span data-ttu-id="ea1a3-146">1. Merhaba ortak IP adresleri ve ağ geçidi IP yapılandırmaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea1a3-146">1. Create hello public IP addresses and gateway IP configurations</span></span>
<span data-ttu-id="ea1a3-147">Ağınız için oluşturacağınız isteği iki ortak IP adresleri toobe ayrılmış toohello ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-147">Request two public IP addresses toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="ea1a3-148">De hello alt ağı ve gerekli IP yapılandırmaları tanımlaması.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-148">You'll also define hello subnet and IP configurations required.</span></span>

```powershell
$gw1pip1 = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$gw1pip2 = New-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1
$gw1ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf2 -Subnet $subnet1 -PublicIpAddress $gw1pip2
```

#### <a name="2-create-hello-vpn-gateway-with-active-active-configuration"></a><span data-ttu-id="ea1a3-149">2. Etkin-etkin yapılandırmayla Hello VPN ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea1a3-149">2. Create hello VPN gateway with active-active configuration</span></span>
<span data-ttu-id="ea1a3-150">TestVNet1 için Hello sanal ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-150">Create hello virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="ea1a3-151">İki GatewayIpConfig giriş ve hello EnableActiveActiveFeature bayrağı ayarlanmış unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-151">Note that there are two GatewayIpConfig entries, and hello EnableActiveActiveFeature flag is set.</span></span> <span data-ttu-id="ea1a3-152">Bir ağ geçidi oluşturma biraz zaman alabilir (45 dakika veya daha fazla toocomplete).</span><span class="sxs-lookup"><span data-stu-id="ea1a3-152">Creating a gateway can take a while (45 minutes or more toocomplete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1,$gw1ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN -EnableActiveActiveFeature -Debug
```

#### <a name="3-obtain-hello-gateway-public-ip-addresses-and-hello-bgp-peer-ip-address"></a><span data-ttu-id="ea1a3-153">3. Merhaba ağ geçidi genel IP adresleri ve hello BGP eş IP adresi alın</span><span class="sxs-lookup"><span data-stu-id="ea1a3-153">3. Obtain hello gateway public IP addresses and hello BGP Peer IP address</span></span>
<span data-ttu-id="ea1a3-154">Merhaba ağ geçidi oluşturulduktan sonra tooobtain hello hello Azure VPN ağ geçidi BGP eşdeğer IP adresi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-154">Once hello gateway is created, you will need tooobtain hello BGP Peer IP address on hello Azure VPN Gateway.</span></span> <span data-ttu-id="ea1a3-155">Bu adres için şirket içi VPN cihazlarınızı BGP eşi gerekli tooconfigure hello Azure VPN ağ geçidi gibidir.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-155">This address is needed tooconfigure hello Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$gw1pip1 = Get-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1
$gw1pip2 = Get-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
```

<span data-ttu-id="ea1a3-156">VPN ağ geçidinizi ve ilgili BGP eş IP adreslerini her ağ geçidi örneği için ayrılan cmdlet'leri tooshow hello iki ortak IP adresleri aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="ea1a3-156">Use hello following cmdlets tooshow hello two public IP addresses allocated for your VPN gateway, and their corresponding BGP Peer IP addresses for each gateway instance:</span></span>

```powershell

    PS D:\> $gw1pip1.IpAddress
    40.112.190.5

    PS D:\> $gw1pip2.IpAddress
    138.91.156.129

    PS D:\> $vnet1gw.BgpSettingsText
    {
      "Asn": 65010,
      "BgpPeeringAddress": "10.12.255.4,10.12.255.5",
      "PeerWeight": 0
    }
```

<span data-ttu-id="ea1a3-157">Merhaba genel IP adresleri Hello sırasını hello ağ geçidi örnekleri ve karşılık gelen BGP eşliği adresleri hello için aynı hello.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-157">hello order of hello public IP addresses for hello gateway instances and hello corresponding BGP Peering Addresses are hello same.</span></span> <span data-ttu-id="ea1a3-158">Bu örnekte, hello ağ geçidi VM 40.112.190.5, genel IP ile BGP eşliği adresini 10.12.255.4 kullanır ve 138.91.156.129 hello ağ geçidiyle 10.12.255.5 kullanır.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-158">In this example, hello gateway VM with public IP of 40.112.190.5 will use 10.12.255.4 as its BGP Peering Address, and hello gateway with 138.91.156.129 will use 10.12.255.5.</span></span> <span data-ttu-id="ea1a3-159">Şirketinizdeki toohello etkin-etkin ağ geçidi bağlanan VPN cihazları ayarladığınızda, bu bilgiler gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-159">This information is needed when you set up your on premises VPN devices connecting toohello active-active gateway.</span></span> <span data-ttu-id="ea1a3-160">Merhaba ağ geçidi tüm adresleri ile Merhaba diyagramı gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="ea1a3-160">hello gateway is shown in hello diagram below with all addresses:</span></span>

![etkin-etkin ağ geçidi](./media/vpn-gateway-activeactive-rm-powershell/active-active-gw.png)

<span data-ttu-id="ea1a3-162">Merhaba ağ geçidi oluşturulduktan sonra bu ağ geçidi tooestablish etkin-etkin şirket içi veya VNet-VNet bağlantısı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-162">Once hello gateway is created, you can use this gateway tooestablish active-active cross-premises or VNet-to-VNet connection.</span></span> <span data-ttu-id="ea1a3-163">Aşağıdaki bölümlerde hello hello adımları toocomplete hello alıştırma yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-163">hello following sections will walk through hello steps toocomplete hello exercise.</span></span>

## <span data-ttu-id="ea1a3-164"><a name ="aacrossprem"></a>Bölüm 2 - bir aktif-aktif şirketler arası bağlantı kuramadı</span><span class="sxs-lookup"><span data-stu-id="ea1a3-164"><a name ="aacrossprem"></a>Part 2 - Establish an active-active cross-premises connection</span></span>
<span data-ttu-id="ea1a3-165">tooestablish şirketler arası bağlantı, gereksinim duyduğunuz toocreate bir yerel ağ geçidi toorepresent şirket içi VPN aygıtınızın ve hello yerel ağ geçidi ile bağlantı tooconnect hello Azure VPN ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-165">tooestablish a cross-premises connection, you need toocreate a Local Network Gateway toorepresent your on-premises VPN device, and a Connection tooconnect hello Azure VPN gateway with hello local network gateway.</span></span> <span data-ttu-id="ea1a3-166">Bu örnekte, hello Azure VPN ağ geçidi etkin-etkin modunda değil.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-166">In this example, hello Azure VPN gateway is in active-active mode.</span></span> <span data-ttu-id="ea1a3-167">Sonuç olarak, olsa bile yalnızca bir VPN cihazı (yerel ağ geçidi) ve bir bağlantı kaynak şirket, hem Azure VPN ağ geçidi örnekleri hello şirket içi aygıtla S2S VPN tünelleri oluşturacaktır.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-167">As a result, even though there is only one on-premises VPN device (local network gateway) and one connection resource, both Azure VPN gateway instances will establish S2S VPN tunnels with hello on-premises device.</span></span>

<span data-ttu-id="ea1a3-168">Devam etmeden önce lütfen tamamladığınızdan emin olun [Kısım 1](#aagateway) Bu alıştırmada.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-168">Before proceeding, please make sure you have completed [Part 1](#aagateway) of this exercise.</span></span>

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a><span data-ttu-id="ea1a3-169">1. adım - oluşturma ve hello yerel ağ geçidi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ea1a3-169">Step 1 - Create and configure hello local network gateway</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="ea1a3-170">1. Değişkenlerinizi bildirme</span><span class="sxs-lookup"><span data-stu-id="ea1a3-170">1. Declare your variables</span></span>
<span data-ttu-id="ea1a3-171">Bu alıştırmada hello diyagramda gösterildiği toobuild hello yapılandırma devam eder.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-171">This exercise will continue toobuild hello configuration shown in hello diagram.</span></span> <span data-ttu-id="ea1a3-172">Merhaba olanları hello değerlerle emin tooreplace olması yapılandırmanızın toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-172">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG5 = "TestAARG5"
$Location5 = "West US"
$LNGName51 = "Site5_1"
$LNGPrefix51 = "10.52.255.253/32"
$LNGIP51 = "131.107.72.22"
$LNGASN5 = 65050
$BGPPeerIP51 = "10.52.255.253"
```

<span data-ttu-id="ea1a3-173">Şeyler toonote hello yerel ağ geçidi parametreleri ilgili birkaç:</span><span class="sxs-lookup"><span data-stu-id="ea1a3-173">A couple of things toonote regarding hello local network gateway parameters:</span></span>

* <span data-ttu-id="ea1a3-174">Merhaba yerel ağ geçidi aynı hello veya VPN ağ geçidi hello farklı bir konum ve kaynak grubu olabilir.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-174">hello local network gateway can be in hello same or different location and resource group as hello VPN gateway.</span></span> <span data-ttu-id="ea1a3-175">Bu örnek bunları farklı kaynak gruplarında hello içinde gösterir, ancak aynı Azure konumu.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-175">This example shows them in different resource groups but in hello same Azure location.</span></span>
* <span data-ttu-id="ea1a3-176">Yukarıda gösterildiği gibi yalnızca bir şirket içi VPN cihazı ise hello etkin-etkin bağlantısı ile veya BGP protokolüne olmadan çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-176">If there is only one on-premises VPN device as shown above, hello active-active connection can work with or without BGP protocol.</span></span> <span data-ttu-id="ea1a3-177">Bu örnek BGP hello şirketler arası bağlantı için kullanır.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-177">This example uses BGP for hello cross-premises connection.</span></span>
* <span data-ttu-id="ea1a3-178">BGP etkinleştirilirse, toodeclare hello yerel ağ geçidi için gereksinim duyduğunuz hello önek hello konak BGP eşdeğer IP adresinizin, VPN cihazınızdaki adresidir.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-178">If BGP is enabled, hello prefix you need toodeclare for hello local network gateway is hello host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="ea1a3-179">Bu durumda, bir /32 olan "10.52.255.253/32" öneki.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-179">In this case, it's a /32 prefix of "10.52.255.253/32".</span></span>
* <span data-ttu-id="ea1a3-180">Bir anımsatıcı farklı BGP Asn'ler şirket içi ağlarınız ve Azure VNet arasında kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-180">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="ea1a3-181">Olan Merhaba, aynı şirket içi VPN aygıtınızın diğer BGP komşuları ile Merhaba ASN toopeer zaten kullanıyorsa, VNet ASN toochange gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-181">If they are hello same, you need toochange your VNet ASN if your on-premises VPN device already uses hello ASN toopeer with other BGP neighbors.</span></span>

#### <a name="2-create-hello-local-network-gateway-for-site5"></a><span data-ttu-id="ea1a3-182">2. Merhaba yerel ağ geçidi için Site5 oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea1a3-182">2. Create hello local network gateway for Site5</span></span>
<span data-ttu-id="ea1a3-183">Lütfen devam etmeden önce hala bağlı tooSubscription 1 olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-183">Before you continue, please make sure you are still connected tooSubscription 1.</span></span> <span data-ttu-id="ea1a3-184">Henüz oluşturulmaz hello kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-184">Create hello resource group if it is not yet created.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5
New-AzureRmLocalNetworkGateway -Name $LNGName51 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP51 -AddressPrefix $LNGPrefix51 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP51
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="ea1a3-185">2. adım - hello VNet ağ geçidi ve yerel ağ geçidi Bağlan</span><span class="sxs-lookup"><span data-stu-id="ea1a3-185">Step 2 - Connect hello VNet gateway and local network gateway</span></span>
#### <a name="1-get-hello-two-gateways"></a><span data-ttu-id="ea1a3-186">1. İki ağ geçidi Hello Al</span><span class="sxs-lookup"><span data-stu-id="ea1a3-186">1. Get hello two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw1 = Get-AzureRmLocalNetworkGateway  -Name $LNGName51 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a><span data-ttu-id="ea1a3-187">2. Merhaba TestVNet1 tooSite5 bağlantısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea1a3-187">2. Create hello TestVNet1 tooSite5 connection</span></span>
<span data-ttu-id="ea1a3-188">Bu adımda, hello bağlantı TestVNet1 tooSite5_1 "ile EnableBGP çok Ayarla" oluşturacağınız $True.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-188">In this step, you will create hello connection from TestVNet1 tooSite5_1 with "EnableBGP" set too$True.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection151 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw1 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-on-premises-vpn-device"></a><span data-ttu-id="ea1a3-189">3. Şirket içi VPN cihazınız için VPN ve BGP parametreleri</span><span class="sxs-lookup"><span data-stu-id="ea1a3-189">3. VPN and BGP parameters for your on-premises VPN device</span></span>
<span data-ttu-id="ea1a3-190">Aşağıdaki örnek Hello bu alıştırma için şirket içi VPN cihazınızdaki BGP yapılandırma bölümü hello girer hello parametreleri listelenir:</span><span class="sxs-lookup"><span data-stu-id="ea1a3-190">hello example below lists hello parameters you will enter into hello BGP configuration section on your on-premises VPN device for this exercise:</span></span>

    - <span data-ttu-id="ea1a3-191">Site5 ASN: 65050</span><span class="sxs-lookup"><span data-stu-id="ea1a3-191">Site5 ASN            : 65050</span></span>
    - <span data-ttu-id="ea1a3-192">Site5 BGP IP: 10.52.255.253</span><span class="sxs-lookup"><span data-stu-id="ea1a3-192">Site5 BGP IP         : 10.52.255.253</span></span>
    - <span data-ttu-id="ea1a3-193">Tooannounce önekleri: (örneğin) 10.51.0.0/16 ve 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="ea1a3-193">Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16</span></span>
    - <span data-ttu-id="ea1a3-194">Azure VNet ASN: 65010</span><span class="sxs-lookup"><span data-stu-id="ea1a3-194">Azure VNet ASN       : 65010</span></span>
    - <span data-ttu-id="ea1a3-195">Azure VNet BGP IP 1: 10.12.255.4 tünel too40.112.190.5 için</span><span class="sxs-lookup"><span data-stu-id="ea1a3-195">Azure VNet BGP IP 1  : 10.12.255.4 for tunnel too40.112.190.5</span></span>
    - <span data-ttu-id="ea1a3-196">Azure VNet BGP IP 2: 10.12.255.5 tünel too138.91.156.129 için</span><span class="sxs-lookup"><span data-stu-id="ea1a3-196">Azure VNet BGP IP 2  : 10.12.255.5 for tunnel too138.91.156.129</span></span>
    - <span data-ttu-id="ea1a3-197">Statik yollar: Hedef 10.12.255.4/32, nexthop hello VPN tüneli arabirimi too40.112.190.5 hedef 10.12.255.5/32, nexthop hello VPN tüneli arabirimi too138.91.156.129</span><span class="sxs-lookup"><span data-stu-id="ea1a3-197">Static routes        : Destination 10.12.255.4/32, nexthop hello VPN tunnel interface too40.112.190.5                        Destination 10.12.255.5/32, nexthop hello VPN tunnel interface too138.91.156.129</span></span>
    - <span data-ttu-id="ea1a3-198">eBGP Multihop: eBGP Cihazınızda gerekirse etkinleştirilmişse hello "multihop" seçeneği emin olun.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-198">eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed</span></span>

<span data-ttu-id="ea1a3-199">Merhaba IPSec bağlantısı kurulduktan sonra birkaç dakika ile Merhaba BGP eşliği oturumu başlatacak sonra hello bağlantı kurulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-199">hello connection should be established after a few minutes, and hello BGP peering session will start once hello IPsec connection is established.</span></span> <span data-ttu-id="ea1a3-200">Bu örnek, o ana kadarki aşağıda gösterilen hello diyagramı bunun sonucunda, yalnızca bir şirket içi VPN cihazı yapılandırmış:</span><span class="sxs-lookup"><span data-stu-id="ea1a3-200">This example so far has configured only one on-premises VPN device, resulting in hello diagram shown below:</span></span>

![etkin etkin crossprem](./media/vpn-gateway-activeactive-rm-powershell/active-active.png)

### <a name="step-3---connect-two-on-premises-vpn-devices-toohello-active-active-vpn-gateway"></a><span data-ttu-id="ea1a3-202">3. adım - iki şirket içi VPN aygıtları toohello etkin-etkin VPN ağ geçidi Bağlan</span><span class="sxs-lookup"><span data-stu-id="ea1a3-202">Step 3 - Connect two on-premises VPN devices toohello active-active VPN gateway</span></span>
<span data-ttu-id="ea1a3-203">Merhaba iki VPN aygıtları varsa aynı ağ şirket içi, bağlanan hello Azure VPN ağ geçidi toohello ikinci VPN cihazı tarafından çift artıklık elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-203">If you have two VPN devices at hello same on-premises network, you can achieve dual redundancy by connecting hello Azure VPN gateway toohello second VPN device.</span></span>

#### <a name="1-create-hello-second-local-network-gateway-for-site5"></a><span data-ttu-id="ea1a3-204">1. Merhaba ikinci yerel ağ geçidi için Site5 oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea1a3-204">1. Create hello second local network gateway for Site5</span></span>
<span data-ttu-id="ea1a3-205">Merhaba ağ geçidi IP adresi, adres öneki ve hello ikinci yerel ağ geçidi için BGP eşliği adresi hello hello önceki yerel ağ geçidi ile aynı çakışmaması gerekir, Not ağ şirket içi.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-205">Note that hello gateway IP address, address prefix, and BGP peering address for hello second local network gateway must not overlap with hello previous local network gateway for hello same on-premises network.</span></span>

```powershell
$LNGName52 = "Site5_2"
$LNGPrefix52 = "10.52.255.254/32"
$LNGIP52 = "131.107.72.23"
$BGPPeerIP52 = "10.52.255.254"

New-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP52 -AddressPrefix $LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP52
```

#### <a name="2-connect-hello-vnet-gateway-and-hello-second-local-network-gateway"></a><span data-ttu-id="ea1a3-206">2. Merhaba VNet ağ geçidi ve hello ikinci yerel ağ geçidi Bağlan</span><span class="sxs-lookup"><span data-stu-id="ea1a3-206">2. Connect hello VNet gateway and hello second local network gateway</span></span>
<span data-ttu-id="ea1a3-207">Merhaba bağlantı "ile EnableBGP çok Ayarla" TestVNet1 tooSite5_2 oluşturmak $True</span><span class="sxs-lookup"><span data-stu-id="ea1a3-207">Create hello connection from TestVNet1 tooSite5_2 with "EnableBGP" set too$True</span></span>

```powershell
$lng5gw2 = Get-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection152 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw2 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-second-on-premises-vpn-device"></a><span data-ttu-id="ea1a3-208">3. İkinci şirket içi VPN cihazınız için VPN ve BGP parametreleri</span><span class="sxs-lookup"><span data-stu-id="ea1a3-208">3. VPN and BGP parameters for your second on-premises VPN device</span></span>
<span data-ttu-id="ea1a3-209">Benzer şekilde, aşağıdaki listeleri hello parametrelerin hello ikinci VPN cihazı girer:</span><span class="sxs-lookup"><span data-stu-id="ea1a3-209">Similarly, below lists hello parameters you will enter into hello second VPN device:</span></span>

```
- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP 1  : 10.12.255.4 for tunnel too40.112.190.5
- Azure VNet BGP IP 2  : 10.12.255.5 for tunnel too138.91.156.129
- Static routes        : Destination 10.12.255.4/32, nexthop hello VPN tunnel interface too40.112.190.5
                         Destination 10.12.255.5/32, nexthop hello VPN tunnel interface too138.91.156.129
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

<span data-ttu-id="ea1a3-210">Merhaba (tüneller) bağlantı sonra çift yedekli VPN cihazları ve şirket içi ağınız ve Azure bağlanma tüneller olacaktır:</span><span class="sxs-lookup"><span data-stu-id="ea1a3-210">Once hello connection (tunnels) are established, you will have dual redundant VPN devices and tunnels connecting your on-premises network and Azure:</span></span>

![çift artıklık crossprem](./media/vpn-gateway-activeactive-rm-powershell/dual-redundancy.png)

## <span data-ttu-id="ea1a3-212"><a name ="aav2v"></a>Bölüm 3 - bir aktif-aktif VNet-VNet bağlantı kuramadı</span><span class="sxs-lookup"><span data-stu-id="ea1a3-212"><a name ="aav2v"></a>Part 3 - Establish an active-active VNet-to-VNet connection</span></span>
<span data-ttu-id="ea1a3-213">Bu bölüm BGP özellikli bir aktif-aktif VNet-VNet bağlantısı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-213">This section creates an active-active VNet-to-VNet connection with BGP.</span></span> 

<span data-ttu-id="ea1a3-214">Merhaba yönergelerde hello önceki adımlardan, yukarıda listelenen devam edin.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-214">hello instructions below continue from hello previous steps listed above.</span></span> <span data-ttu-id="ea1a3-215">Tamamlamanız gereken [Kısım 1](#aagateway) toocreate TestVNet1 yapılandırmak ve VPN ağ geçidi BGP ile Merhaba.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-215">You must complete [Part 1](#aagateway) toocreate and configure TestVNet1 and hello VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a><span data-ttu-id="ea1a3-216">1. adım - TestVNet2 ve hello VPN ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea1a3-216">Step 1 - Create TestVNet2 and hello VPN gateway</span></span>
<span data-ttu-id="ea1a3-217">Önemli toomake hello IP adres alanı hello yeni sanal ağın TestVNet2, herhangi bir VNet aralıkları ile çakışmaması emin olur.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-217">It is important toomake sure that hello IP address space of hello new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="ea1a3-218">Bu örnekte, sanal ağlar hello toohello ait aynı abonelik.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-218">In this example, hello virtual networks belong toohello same subscription.</span></span> <span data-ttu-id="ea1a3-219">VNet-VNet bağlantıları farklı abonelikler arasında ayarlayabilirsiniz; Lütfen çok başvurun[VNet-VNet bağlantı yapılandırma](vpn-gateway-vnet-vnet-rm-ps.md) toolearn daha ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-219">You can set up VNet-to-VNet connections between different subscriptions; please refer too[Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) toolearn more details.</span></span> <span data-ttu-id="ea1a3-220">Merhaba eklediğinizden emin olun "-EnableBgp $True" ne zaman oluşturmaya izin ver hello bağlantıları tooenable BGP.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-220">Make sure you add hello "-EnableBgp $True" when creating hello connections tooenable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="ea1a3-221">1. Değişkenlerinizi bildirme</span><span class="sxs-lookup"><span data-stu-id="ea1a3-221">1. Declare your variables</span></span>
<span data-ttu-id="ea1a3-222">Merhaba olanları hello değerlerle emin tooreplace olması yapılandırmanızın toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-222">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG2 = "TestAARG2"
$Location2 = "East US"
$VNetName2 = "TestVNet2"
$FESubName2 = "FrontEnd"
$BESubName2 = "Backend"
$GWSubName2 = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$VNet2ASN = 65020
$DNS2 = "8.8.8.8"
$GWName2 = "VNet2GW"
$GW2IPName1 = "VNet2GWIP1"
$GW2IPconf1 = "gw2ipconf1"
$GW2IPName2 = "VNet2GWIP2"
$GW2IPconf2 = "gw2ipconf2"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-testvnet2-in-hello-new-resource-group"></a><span data-ttu-id="ea1a3-223">2. TestVNet2 hello yeni kaynak grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="ea1a3-223">2. Create TestVNet2 in hello new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-hello-active-active-vpn-gateway-for-testvnet2"></a><span data-ttu-id="ea1a3-224">3. Merhaba etkin-etkin VPN ağ geçidi için TestVNet2 oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea1a3-224">3. Create hello active-active VPN gateway for TestVNet2</span></span>
<span data-ttu-id="ea1a3-225">Ağınız için oluşturacağınız isteği iki ortak IP adresleri toobe ayrılmış toohello ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-225">Request two public IP addresses toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="ea1a3-226">De hello alt ağı ve gerekli IP yapılandırmaları tanımlaması.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-226">You'll also define hello subnet and IP configurations required.</span></span>

```powershell
$gw2pip1 = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$gw2pip2 = New-AzureRmPublicIpAddress -Name $GW2IPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2 = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1
$gw2ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf2 -Subnet $subnet2 -PublicIpAddress $gw2pip2
```

<span data-ttu-id="ea1a3-227">Merhaba VPN ağ geçidi ile Merhaba numarası ve hello "EnableActiveActiveFeature" bayrak olarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-227">Create hello VPN gateway with hello AS number and hello "EnableActiveActiveFeature" flag.</span></span> <span data-ttu-id="ea1a3-228">Azure VPN gateway'lerinde hello varsayılan ASN kılmalıdır unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-228">Note that you must override hello default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="ea1a3-229">Merhaba Asn'ler hello bağlı sanal ağlar farklı tooenable BGP ve transit yönlendirme olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-229">hello ASNs for hello connected VNets must be different tooenable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1,$gw2ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet2ASN -EnableActiveActiveFeature
```

### <a name="step-2---connect-hello-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="ea1a3-230">2. adım - hello TestVNet1 ve TestVNet2 ağ geçitleri Bağlan</span><span class="sxs-lookup"><span data-stu-id="ea1a3-230">Step 2 - Connect hello TestVNet1 and TestVNet2 gateways</span></span>
<span data-ttu-id="ea1a3-231">Bu örnekte, her iki ağ geçitleri hello olan aynı abonelik.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-231">In this example, both gateways are in hello same subscription.</span></span> <span data-ttu-id="ea1a3-232">Bu adımda hello tamamlayabilirsiniz aynı PowerShell oturumunda.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-232">You can complete this step in hello same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="ea1a3-233">1. Her iki ağ geçitleri Al</span><span class="sxs-lookup"><span data-stu-id="ea1a3-233">1. Get both gateways</span></span>
<span data-ttu-id="ea1a3-234">Oturum açma ve tooSubscription 1 bağlanmak emin olun.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-234">Make sure you log in and connect tooSubscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="ea1a3-235">2. Her iki bağlantı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ea1a3-235">2. Create both connections</span></span>
<span data-ttu-id="ea1a3-236">Bu adımda TestVNet1 tooTestVNet2 hello bağlantısından ve hello bağlantı TestVNet2 tooTestVNet1 oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-236">In this step, you will create hello connection from TestVNet1 tooTestVNet2, and hello connection from TestVNet2 tooTestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="ea1a3-237">Her iki bağlantılarında emin tooenable BGP olması.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-237">Be sure tooenable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="ea1a3-238">Bu adımları tamamladıktan sonra hello olması bağlantı birkaç dakika içinde ve hello BGP eşliği oturumu olacaktır yukarı hello VNet-VNet bağlantısı ile çift artıklık tamamlandıktan sonra:</span><span class="sxs-lookup"><span data-stu-id="ea1a3-238">After completing these steps, hello connection will be establish in a few minutes, and hello BGP peering session will be up once hello VNet-to-VNet connection is completed with dual redundancy:</span></span>

![etkin etkin v2v](./media/vpn-gateway-activeactive-rm-powershell/vnet-to-vnet.png)

## <span data-ttu-id="ea1a3-240"><a name ="aaupdate"></a>Bölüm 4 - Güncelleştirme etkin-etkin ve etkin bekleme arasında varolan ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="ea1a3-240"><a name ="aaupdate"></a>Part 4 - Update existing gateway between active-active and active-standby</span></span>
<span data-ttu-id="ea1a3-241">Merhaba son kısım, mevcut bir Azure VPN ağ geçidi nasıl yapılandırabileceğiniz olmadığını açıklamak etkin bekleme tooactive etkin modundan veya tersi.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-241">hello last section will describe how you can configure an existing Azure VPN gateway from active-standby tooactive-active mode, or vice versa.</span></span>

> [!NOTE]
> <span data-ttu-id="ea1a3-242">Bu bölüm, önceden oluşturulmuş bir VPN ağ geçidi'nden standart tooHighPerformance, hello adımları tooresize eski SKU (eski SKU) içerir.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-242">This section includes hello steps tooresize a legacy SKU (old SKU) of an already created VPN gateway from Standard tooHighPerformance.</span></span> <span data-ttu-id="ea1a3-243">Bu adımları Merhaba, eski eski SKU tooone yükseltmeyin yeni SKU'ları.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-243">These steps do not upgrade an old legacy SKU tooone of hello new SKUs.</span></span>
> 
> 

### <a name="configure-an-active-standby-gateway-tooactive-active-gateway"></a><span data-ttu-id="ea1a3-244">Etkin bekleme ağ geçidi tooactive etkin ağ geçidini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ea1a3-244">Configure an active-standby gateway tooactive-active gateway</span></span>
#### <a name="1-gateway-parameters"></a><span data-ttu-id="ea1a3-245">1. Ağ geçidi parametreleri</span><span class="sxs-lookup"><span data-stu-id="ea1a3-245">1. Gateway parameters</span></span>
<span data-ttu-id="ea1a3-246">Aşağıdaki örneğine hello bir etkin-etkin ağ geçidi etkin bekleme ağ geçidi dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-246">hello following example converts an active-standby gateway into an active-active gateway.</span></span> <span data-ttu-id="ea1a3-247">Başka bir ortak IP adresi toocreate gerekir, ardından ikinci bir ağ geçidi IP yapılandırması ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-247">You need toocreate another public IP address, then add a second Gateway IP configuration.</span></span> <span data-ttu-id="ea1a3-248">Gösterildiği hello parametreleri kullanılır:</span><span class="sxs-lookup"><span data-stu-id="ea1a3-248">Below shows hello parameters used:</span></span>

```powershell
$GWName = "TestVNetAA1GW"
$VNetName = "TestVNetAA1"
$RG = "TestVPNActiveActive01"
$GWIPName2 = "gwpip2"
$GWIPconf2 = "gw1ipconf2"

$vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$location = $gw.Location
```

#### <a name="2-create-hello-public-ip-address-then-add-hello-second-gateway-ip-configuration"></a><span data-ttu-id="ea1a3-249">2. Merhaba genel IP adresi oluşturun, sonra hello ikinci ağ geçidi IP Yapılandırması Ekle</span><span class="sxs-lookup"><span data-stu-id="ea1a3-249">2. Create hello public IP address, then add hello second gateway IP configuration</span></span>

```powershell
$gwpip2 = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG -Location $location -AllocationMethod Dynamic
Add-AzureRmVirtualNetworkGatewayIpConfig -VirtualNetworkGateway $gw -Name $GWIPconf2 -Subnet $subnet -PublicIpAddress $gwpip2
```

#### <a name="3-enable-active-active-mode-and-update-hello-gateway"></a><span data-ttu-id="ea1a3-250">3. Etkin-etkin modu ve güncelleştirme hello ağ geçidini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="ea1a3-250">3. Enable active-active mode and update hello gateway</span></span>
<span data-ttu-id="ea1a3-251">PowerShell tootrigger hello gerçek güncelleştirmesi hello ağ geçidi nesnesi ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-251">You must set hello gateway object in PowerShell tootrigger hello actual update.</span></span> <span data-ttu-id="ea1a3-252">Standart olarak daha önce oluşturulmasından bu yana (yeniden boyutlandırılan) tooHighPerformance hello hello sanal ağ geçidi SKU'su aynı zamanda değiştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-252">hello SKU of hello virtual network gateway must also be changed (resized) tooHighPerformance since it was created previously as Standard.</span></span>

```powershell
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -EnableActiveActiveFeature -GatewaySku HighPerformance
```

<span data-ttu-id="ea1a3-253">Bu güncelleştirme 30 too45 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-253">This update can take 30 too45 minutes.</span></span>

### <a name="configure-an-active-active-gateway-tooactive-standby-gateway"></a><span data-ttu-id="ea1a3-254">Etkin-etkin ağ geçidi tooactive bekleme ağ geçidini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ea1a3-254">Configure an active-active gateway tooactive-standby gateway</span></span>
#### <a name="1-gateway-parameters"></a><span data-ttu-id="ea1a3-255">1. Ağ geçidi parametreleri</span><span class="sxs-lookup"><span data-stu-id="ea1a3-255">1. Gateway parameters</span></span>
<span data-ttu-id="ea1a3-256">Kullanım hello aynı yukarıdaki gibi parametreleri almak istediğiniz hello IP yapılandırmasının hello adı tooremove.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-256">Use hello same parameters as above, get hello name of hello IP configuration you want tooremove.</span></span>

```powershell
$GWName = "TestVNetAA1GW"
$RG = "TestVPNActiveActive01"

$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$ipconfname = $gw.IpConfigurations[1].Name
```

#### <a name="2-remove-hello-gateway-ip-configuration-and-disable-hello-active-active-mode"></a><span data-ttu-id="ea1a3-257">2. Merhaba ağ geçidi IP yapılandırmasını kaldırıp hello etkin-etkin modu devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="ea1a3-257">2. Remove hello gateway IP configuration and disable hello active-active mode</span></span>
<span data-ttu-id="ea1a3-258">Benzer şekilde, PowerShell tootrigger hello gerçek güncelleştirmesi hello ağ geçidi nesnesi ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-258">Similarly, you must set hello gateway object in PowerShell tootrigger hello actual update.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGatewayIpConfig -Name $ipconfname -VirtualNetworkGateway $gw
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -DisableActiveActiveFeature
```

<span data-ttu-id="ea1a3-259">Bu güncelleştirme too30 çok 45 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-259">This update can take up too30 too 45 minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea1a3-260">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ea1a3-260">Next steps</span></span>
<span data-ttu-id="ea1a3-261">Bağlantınız tamamlandıktan sonra sanal makineleri tooyour sanal ağları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea1a3-261">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="ea1a3-262">Adımlar için bkz. [Sanal Makine Oluşturma](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ea1a3-262">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
