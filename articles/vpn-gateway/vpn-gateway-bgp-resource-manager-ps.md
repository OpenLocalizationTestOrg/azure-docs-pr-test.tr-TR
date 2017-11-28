---
title: "Azure VPN ağ geçitlerinde BGP yapılandırın: Resource Manager: PowerShell | Microsoft Docs"
description: "Bu makalede Azure Resource Manager ve PowerShell kullanarak Azure VPN Gateway'ler ile BGP nasıl yapılandıracağınız anlatılmaktadır."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 905b11a7-1333-482c-820b-0fd0f44238e5
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: yushwang
ms.openlocfilehash: a9d13ae6b319e2efa8965dc2955c9b89ac3fd12b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-bgp-on-azure-vpn-gateways-using-powershell"></a><span data-ttu-id="479a0-103">Nasıl tooconfigure BGP Azure VPN ağ geçitlerinde PowerShell'i kullanma</span><span class="sxs-lookup"><span data-stu-id="479a0-103">How tooconfigure BGP on Azure VPN Gateways using PowerShell</span></span>
<span data-ttu-id="479a0-104">Bu makalede bir şirket içi siteden siteye (S2S) VPN bağlantısı ve hello Resource Manager dağıtım modeli ve PowerShell kullanarak VNet-VNet bağlantısı hello adımları tooenable BGP anlatılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="479a0-104">This article walks you through hello steps tooenable BGP on a cross-premises Site-to-Site (S2S) VPN connection and a VNet-to-VNet connection using hello Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-bgp"></a><span data-ttu-id="479a0-105">BGP hakkında</span><span class="sxs-lookup"><span data-stu-id="479a0-105">About BGP</span></span>
<span data-ttu-id="479a0-106">BGP hello Internet tooexchange Yönlendirme ve ulaşılabilirlik bilgilerini iki veya daha fazla ağ arasında yaygın olarak kullanılan hello standart yönlendirme protokolüdür.</span><span class="sxs-lookup"><span data-stu-id="479a0-106">BGP is hello standard routing protocol commonly used in hello Internet tooexchange routing and reachability information between two or more networks.</span></span> <span data-ttu-id="479a0-107">BGP hello Azure VPN ağ geçitleri ve BGP eşlikleri veya Komşuları olarak adlandırılan, şirket içi VPN cihazlarınızı etkinleştirir, tooexchange "yolları", her iki ağ geçidini hello kullanılabilirlik size bildirir ve ulaşılabilirlik olanlar için önekleri hello ağ geçitlerinden veya yönlendiricilerden söz konusu aracılığıyla toogo.</span><span class="sxs-lookup"><span data-stu-id="479a0-107">BGP enables hello Azure VPN Gateways and your on-premises VPN devices, called BGP peers or neighbors, tooexchange "routes" that will inform both gateways on hello availability and reachability for those prefixes toogo through hello gateways or routers involved.</span></span> <span data-ttu-id="479a0-108">BGP, bir BGP eş tooall bir BGP ağ geçidinin öğrendiği yolları yayarak birden fazla ağ arasında geçiş yönlendirme de etkinleştirebilir diğer BGP eşleri.</span><span class="sxs-lookup"><span data-stu-id="479a0-108">BGP can also enable transit routing among multiple networks by propagating routes a BGP gateway learns from one BGP peer tooall other BGP peers.</span></span>

<span data-ttu-id="479a0-109">Bkz: [Azure VPN Gateways ile BGP'ye genel bakış](vpn-gateway-bgp-overview.md) BGP ve toounderstand hello teknik gereksinimleri ve konular BGP kullanmanın avantajları hakkında daha fazla tartışma için.</span><span class="sxs-lookup"><span data-stu-id="479a0-109">See [Overview of BGP with Azure VPN Gateways](vpn-gateway-bgp-overview.md) for more discussion on benefits of BGP and toounderstand hello technical requirements and considerations of using BGP.</span></span>

## <a name="getting-started-with-bgp-on-azure-vpn-gateways"></a><span data-ttu-id="479a0-110">Azure VPN ağ geçitlerinde BGP ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="479a0-110">Getting started with BGP on Azure VPN gateways</span></span>

<span data-ttu-id="479a0-111">Bu makale size hello adımları toodo hello görevleri aşağıdaki yardımcı olur:</span><span class="sxs-lookup"><span data-stu-id="479a0-111">This article walks you through hello steps toodo hello following tasks:</span></span>

* [<span data-ttu-id="479a0-112">Bölüm 1 - etkinleştir BGP, Azure VPN ağ geçidi</span><span class="sxs-lookup"><span data-stu-id="479a0-112">Part 1 - Enable BGP on your Azure VPN gateway</span></span>](#enablebgp)
* [<span data-ttu-id="479a0-113">Bölüm 2 - BGP şirketler arası bağlantı Kur</span><span class="sxs-lookup"><span data-stu-id="479a0-113">Part 2 - Establish a cross-premises connection with BGP</span></span>](#crossprembgp)
* [<span data-ttu-id="479a0-114">Bölüm 3 - BGP VNet-VNet bağlantı Kur</span><span class="sxs-lookup"><span data-stu-id="479a0-114">Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>](#v2vbgp)

<span data-ttu-id="479a0-115">Her bir parçasını hello yönergeleri BGP ağ bağlantınızı etkinleştirmek için temel yapı bloğu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="479a0-115">Each part of hello instructions forms a basic building block for enabling BGP in your network connectivity.</span></span> <span data-ttu-id="479a0-116">Tüm üç bölümden tamamlarsanız, hello Aşağıdaki diyagramda gösterildiği gibi hello topoloji oluşturun:</span><span class="sxs-lookup"><span data-stu-id="479a0-116">If you complete all three parts, you build hello topology as shown in hello following diagram:</span></span>

![BGP topolojisi](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

<span data-ttu-id="479a0-118">Bölümleri birlikte toobuild ihtiyaçlarınıza uygun bir daha karmaşık, çoklu atlamalı geçiş ağ birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="479a0-118">You can combine parts together toobuild a more complex, multi-hop, transit network that meets your needs.</span></span>

## <span data-ttu-id="479a0-119"><a name ="enablebgp"></a>Bölüm 1 - BGP hello Azure VPN ağ geçidi üzerinde yapılandırma</span><span class="sxs-lookup"><span data-stu-id="479a0-119"><a name ="enablebgp"></a>Part 1 - Configure BGP on hello Azure VPN Gateway</span></span>
<span data-ttu-id="479a0-120">Merhaba yapılandırma adımlarını hello hello Azure VPN ağ geçidi BGP parametrelerinin hello Aşağıdaki diyagramda gösterildiği gibi ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="479a0-120">hello configuration steps set up hello BGP parameters of hello Azure VPN gateway as shown in hello following diagram:</span></span>

![BGP ağ geçidi](./media/vpn-gateway-bgp-resource-manager-ps/bgp-gateway.png)

### <a name="before-you-begin"></a><span data-ttu-id="479a0-122">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="479a0-122">Before you begin</span></span>
* <span data-ttu-id="479a0-123">Azure aboneliğiniz olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="479a0-123">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="479a0-124">Henüz Azure aboneliğiniz yoksa [MSDN abonelik avantajlarınızı](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) etkinleştirebilir veya [ücretsiz bir hesap](https://azure.microsoft.com/pricing/free-trial/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="479a0-124">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="479a0-125">Hello Azure Resource Manager PowerShell cmdlet'lerini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="479a0-125">Install hello Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="479a0-126">Merhaba PowerShell cmdlet'lerini yükleme hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="479a0-126">For more information about installing hello PowerShell cmdlets, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> 

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="479a0-127">1. adım - oluşturun ve VNet1 yapılandırın</span><span class="sxs-lookup"><span data-stu-id="479a0-127">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="479a0-128">1. Değişkenlerinizi bildirme</span><span class="sxs-lookup"><span data-stu-id="479a0-128">1. Declare your variables</span></span>
<span data-ttu-id="479a0-129">Bu alıştırmada, değişkenlerimizi bildirerek başlayın.</span><span class="sxs-lookup"><span data-stu-id="479a0-129">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="479a0-130">Merhaba aşağıdaki örnekte bu alıştırmada hello değerleri kullanarak hello değişkenler bildirilmektedir.</span><span class="sxs-lookup"><span data-stu-id="479a0-130">hello following example declares hello variables using hello values for this exercise.</span></span> <span data-ttu-id="479a0-131">Üretim için yapılandırma emin tooreplace hello değerleri kendi değerlerinizle olabilir.</span><span class="sxs-lookup"><span data-stu-id="479a0-131">Be sure tooreplace hello values with your own when configuring for production.</span></span> <span data-ttu-id="479a0-132">Merhaba adımları toobecome yapılandırma bu tür tanıdık aracılığıyla çalıştırıyorsanız, bu değişkenleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="479a0-132">You can use these variables if you are running through hello steps toobecome familiar with this type of configuration.</span></span> <span data-ttu-id="479a0-133">Merhaba değişkenleri değiştirin ve sonra kopyalayın ve PowerShell konsolunuza yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="479a0-133">Modify hello variables, and then copy and paste into your PowerShell console.</span></span>

```powershell
$Sub1 = "Replace_With_Your_Subcription_Name"
$RG1 = "TestBGPRG1"
$Location1 = "East US"
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
$GWIPName1 = "VNet1GWIP"
$GWIPconfName1 = "gwipconf1"
$Connection12 = "VNet1toVNet2"
$Connection15 = "VNet1toSite5"
```

#### <a name="2-connect-tooyour-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="479a0-134">2. Tooyour abonelik bağlanın ve yeni bir kaynak grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="479a0-134">2. Connect tooyour subscription and create a new resource group</span></span>
<span data-ttu-id="479a0-135">toouse hello Resource Manager cmdlet'lerini tooPowerShell moduna geçtiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="479a0-135">toouse hello Resource Manager cmdlets, Make sure you switch tooPowerShell mode.</span></span> <span data-ttu-id="479a0-136">Daha fazla bilgi için [Windows PowerShell’i Resource Manager ile kullanma](../powershell-azure-resource-manager.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="479a0-136">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="479a0-137">PowerShell Konsolunuzu açın ve tooyour hesap bağlanın.</span><span class="sxs-lookup"><span data-stu-id="479a0-137">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="479a0-138">Bağlandığınız örnek toohelp aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="479a0-138">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="479a0-139">3. TestVNet1 oluşturma</span><span class="sxs-lookup"><span data-stu-id="479a0-139">3. Create TestVNet1</span></span>
<span data-ttu-id="479a0-140">Merhaba aşağıdaki örnekte TestVNet1 ve üç alt ağ, biri GatewaySubnet, biri FrontEnd ve diğeri Backend'dir adlı bir sanal ağ oluşturur.</span><span class="sxs-lookup"><span data-stu-id="479a0-140">hello following sample creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="479a0-141">Kendi değerlerinizi yerleştirirken ağ geçidi alt ağınızı özellikle GatewaySubnet olarak adlandırmanız önem taşır.</span><span class="sxs-lookup"><span data-stu-id="479a0-141">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="479a0-142">Başka bir ad kullanırsanız ağ geçidi oluşturma işleminiz başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="479a0-142">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-hello-vpn-gateway-for-testvnet1-with-bgp-parameters"></a><span data-ttu-id="479a0-143">2. adım - hello VPN ağ geçidi BGP parametrelerle TestVNet1 için oluşturma</span><span class="sxs-lookup"><span data-stu-id="479a0-143">Step 2 - Create hello VPN Gateway for TestVNet1 with BGP parameters</span></span>
#### <a name="1-create-hello-ip-and-subnet-configurations"></a><span data-ttu-id="479a0-144">1. Merhaba IP ve alt ağ yapılandırmaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="479a0-144">1. Create hello IP and subnet configurations</span></span>
<span data-ttu-id="479a0-145">Ağınız için oluşturacağınız bir ortak IP adresi toobe ayrılmış toohello ağ geçidi isteği.</span><span class="sxs-lookup"><span data-stu-id="479a0-145">Request a public IP address toobe allocated toohello gateway you will create for your VNet.</span></span> <span data-ttu-id="479a0-146">De gerekli hello alt ağ ve IP yapılandırmaları tanımlaması.</span><span class="sxs-lookup"><span data-stu-id="479a0-146">You'll also define hello required subnet and IP configurations.</span></span>

```powershell
$gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1
```

#### <a name="2-create-hello-vpn-gateway-with-hello-as-number"></a><span data-ttu-id="479a0-147">2. Merhaba VPN ağ geçidi ile Merhaba oluşturmak sayı olarak</span><span class="sxs-lookup"><span data-stu-id="479a0-147">2. Create hello VPN gateway with hello AS number</span></span>
<span data-ttu-id="479a0-148">TestVNet1 için Hello sanal ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="479a0-148">Create hello virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="479a0-149">BGP TestVNet1 için bir rota tabanlı VPN ağ geçidi ve aynı zamanda hello ek parametre, - Asn tooset hello ASN (AS numarası) gerektirir.</span><span class="sxs-lookup"><span data-stu-id="479a0-149">BGP requires a Route-Based VPN gateway, and also hello addition parameter, -Asn, tooset hello ASN (AS Number) for TestVNet1.</span></span> <span data-ttu-id="479a0-150">Merhaba ASN parametre ayarlamazsanız ASN 65515 atanır.</span><span class="sxs-lookup"><span data-stu-id="479a0-150">If you do not set hello ASN parameter, ASN 65515 is assigned.</span></span> <span data-ttu-id="479a0-151">Bir ağ geçidi oluşturma biraz zaman alabilir (30 dakika veya daha fazla toocomplete).</span><span class="sxs-lookup"><span data-stu-id="479a0-151">Creating a gateway can take a while (30 minutes or more toocomplete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance -Asn $VNet1ASN
```

#### <a name="3-obtain-hello-azure-bgp-peer-ip-address"></a><span data-ttu-id="479a0-152">3. Hello Azure BGP eşdeğer IP adresi al</span><span class="sxs-lookup"><span data-stu-id="479a0-152">3. Obtain hello Azure BGP Peer IP address</span></span>
<span data-ttu-id="479a0-153">Merhaba ağ geçidi oluşturulduktan sonra tooobtain hello hello Azure VPN ağ geçidi BGP eşdeğer IP adresi gerekir.</span><span class="sxs-lookup"><span data-stu-id="479a0-153">Once hello gateway is created, you need tooobtain hello BGP Peer IP address on hello Azure VPN Gateway.</span></span> <span data-ttu-id="479a0-154">Bu adres için şirket içi VPN cihazlarınızı BGP eşi gerekli tooconfigure hello Azure VPN ağ geçidi gibidir.</span><span class="sxs-lookup"><span data-stu-id="479a0-154">This address is needed tooconfigure hello Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet1gw.BgpSettingsText
```

<span data-ttu-id="479a0-155">Merhaba son komut hello karşılık gelen BGP yapılandırmaları hello Azure VPN ağ geçidi üzerinde gösterir; Örneğin:</span><span class="sxs-lookup"><span data-stu-id="479a0-155">hello last command shows hello corresponding BGP configurations on hello Azure VPN Gateway; for example:</span></span>

```powershell
$vnet1gw.BgpSettingsText
{
    "Asn": 65010,
    "BgpPeeringAddress": "10.12.255.30",
    "PeerWeight": 0
}
```

<span data-ttu-id="479a0-156">Merhaba ağ geçidi oluşturulduktan sonra bu ağ geçidi tooestablish şirket içi veya VNet-VNet bağlantısı BGP ile kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="479a0-156">Once hello gateway is created, you can use this gateway tooestablish cross-premises connection or VNet-to-VNet connection with BGP.</span></span> <span data-ttu-id="479a0-157">Merhaba aşağıdaki bölümlerde hello adımları toocomplete hello alıştırma yol.</span><span class="sxs-lookup"><span data-stu-id="479a0-157">hello following sections walk through hello steps toocomplete hello exercise.</span></span>

## <span data-ttu-id="479a0-158"><a name ="crossprembbgp"></a>Bölüm 2 - BGP şirketler arası bağlantı Kur</span><span class="sxs-lookup"><span data-stu-id="479a0-158"><a name ="crossprembbgp"></a>Part 2 - Establish a cross-premises connection with BGP</span></span>

<span data-ttu-id="479a0-159">tooestablish şirketler arası bağlantı, gereksinim duyduğunuz toocreate bir yerel ağ geçidi toorepresent şirket içi VPN aygıtınızın ve hello yerel ağ geçidi ile bağlantı tooconnect hello VPN ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="479a0-159">tooestablish a cross-premises connection, you need toocreate a Local Network Gateway toorepresent your on-premises VPN device, and a Connection tooconnect hello VPN gateway with hello local network gateway.</span></span> <span data-ttu-id="479a0-160">Bu adım adım makaleleri olsa da, bu makalede hello ek özellikler gerekli toospecify hello BGP yapılandırma parametrelerini içerir.</span><span class="sxs-lookup"><span data-stu-id="479a0-160">While there are articles that walk you through these steps, this article contains hello additional properties required toospecify hello BGP configuration parameters.</span></span>

![Şirket içi BGP](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crossprem.png)

<span data-ttu-id="479a0-162">Devam etmeden önce tamamladığınızdan emin olun [Kısım 1](#enablebgp) Bu alıştırmada.</span><span class="sxs-lookup"><span data-stu-id="479a0-162">Before proceeding, make sure you have completed [Part 1](#enablebgp) of this exercise.</span></span>

### <a name="step-1---create-and-configure-hello-local-network-gateway"></a><span data-ttu-id="479a0-163">1. adım - oluşturma ve hello yerel ağ geçidi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="479a0-163">Step 1 - Create and configure hello local network gateway</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="479a0-164">1. Değişkenlerinizi bildirme</span><span class="sxs-lookup"><span data-stu-id="479a0-164">1. Declare your variables</span></span>

<span data-ttu-id="479a0-165">Bu alıştırmada hello diyagramda gösterildiği toobuild hello yapılandırma devam eder.</span><span class="sxs-lookup"><span data-stu-id="479a0-165">This exercise continues toobuild hello configuration shown in hello diagram.</span></span> <span data-ttu-id="479a0-166">Merhaba olanları hello değerlerle emin tooreplace olması yapılandırmanızın toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="479a0-166">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG5 = "TestBGPRG5"
$Location5 = "East US 2"
$LNGName5 = "Site5"
$LNGPrefix50 = "10.52.255.254/32"
$LNGIP5 = "Your_VPN_Device_IP"
$LNGASN5 = 65050
$BGPPeerIP5 = "10.52.255.254"
```

<span data-ttu-id="479a0-167">Şeyler toonote hello yerel ağ geçidi parametreleri ilgili birkaç:</span><span class="sxs-lookup"><span data-stu-id="479a0-167">A couple of things toonote regarding hello local network gateway parameters:</span></span>

* <span data-ttu-id="479a0-168">Merhaba yerel ağ geçidi aynı hello veya VPN ağ geçidi hello farklı bir konum ve kaynak grubu olabilir.</span><span class="sxs-lookup"><span data-stu-id="479a0-168">hello local network gateway can be in hello same or different location and resource group as hello VPN gateway.</span></span> <span data-ttu-id="479a0-169">Bu örnek, bunları farklı kaynak gruplarında farklı konumlarda gösterir.</span><span class="sxs-lookup"><span data-stu-id="479a0-169">This example shows them in different resource groups in different locations.</span></span>
* <span data-ttu-id="479a0-170">Merhaba minimum önek toodeclare hello yerel ağ geçidi için gereksinim duyduğunuz hello konak BGP eşdeğer IP adresinizin, VPN cihazınızdaki adresidir.</span><span class="sxs-lookup"><span data-stu-id="479a0-170">hello minimum prefix you need toodeclare for hello local network gateway is hello host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="479a0-171">Bu durumda, bir /32 olan "10.52.255.254/32" öneki.</span><span class="sxs-lookup"><span data-stu-id="479a0-171">In this case, it's a /32 prefix of "10.52.255.254/32".</span></span>
* <span data-ttu-id="479a0-172">Bir anımsatıcı farklı BGP Asn'ler şirket içi ağlarınız ve Azure VNet arasında kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="479a0-172">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="479a0-173">Olan Merhaba, aynı şirket içi VPN aygıtınızın diğer BGP komşuları ile Merhaba ASN toopeer zaten kullanıyorsa, VNet ASN toochange gerekir.</span><span class="sxs-lookup"><span data-stu-id="479a0-173">If they are hello same, you need toochange your VNet ASN if your on-premises VPN device already uses hello ASN toopeer with other BGP neighbors.</span></span>

<span data-ttu-id="479a0-174">Devam etmeden önce halen bağlı tooSubscription 1 olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="479a0-174">Before you continue, make sure you are still connected tooSubscription 1.</span></span>

#### <a name="2-create-hello-local-network-gateway-for-site5"></a><span data-ttu-id="479a0-175">2. Merhaba yerel ağ geçidi için Site5 oluşturma</span><span class="sxs-lookup"><span data-stu-id="479a0-175">2. Create hello local network gateway for Site5</span></span>

<span data-ttu-id="479a0-176">Merhaba yerel ağ geçidi oluşturmadan önce onu, oluşturulmamışsa emin toocreate hello kaynak grubu olabilir.</span><span class="sxs-lookup"><span data-stu-id="479a0-176">Be sure toocreate hello resource group if it is not created, before you create hello local network gateway.</span></span> <span data-ttu-id="479a0-177">Merhaba yerel ağ geçidi için hello iki ek parametreler dikkat edin: Asn ve BgpPeerAddress.</span><span class="sxs-lookup"><span data-stu-id="479a0-177">Notice hello two additional parameters for hello local network gateway: Asn and BgpPeerAddress.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

### <a name="step-2---connect-hello-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="479a0-178">2. adım - hello VNet ağ geçidi ve yerel ağ geçidi Bağlan</span><span class="sxs-lookup"><span data-stu-id="479a0-178">Step 2 - Connect hello VNet gateway and local network gateway</span></span>

#### <a name="1-get-hello-two-gateways"></a><span data-ttu-id="479a0-179">1. İki ağ geçidi Hello Al</span><span class="sxs-lookup"><span data-stu-id="479a0-179">1. Get hello two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5
```

#### <a name="2-create-hello-testvnet1-toosite5-connection"></a><span data-ttu-id="479a0-180">2. Merhaba TestVNet1 tooSite5 bağlantısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="479a0-180">2. Create hello TestVNet1 tooSite5 connection</span></span>

<span data-ttu-id="479a0-181">Bu adımda TestVNet1 tooSite5 hello bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="479a0-181">In this step, you create hello connection from TestVNet1 tooSite5.</span></span> <span data-ttu-id="479a0-182">Belirtmeniz gerekir "-EnableBGP $True" tooenable BGP Bu bağlantı için.</span><span class="sxs-lookup"><span data-stu-id="479a0-182">You must specify "-EnableBGP $True" tooenable BGP for this connection.</span></span> <span data-ttu-id="479a0-183">Daha önce bahsedildiği gibi BGP ve BGP olmayan bağlantıları için olası toohave olduğu aynı Azure VPN ağ geçidi hello.</span><span class="sxs-lookup"><span data-stu-id="479a0-183">As discussed earlier, it is possible toohave both BGP and non-BGP connections for hello same Azure VPN Gateway.</span></span> <span data-ttu-id="479a0-184">BGP hello bağlantı özelliği etkin değilse, BGP parametreleri her iki ağ geçidini zaten yapılandırılmış olsa bile Azure BGP Bu bağlantı için izin vermez.</span><span class="sxs-lookup"><span data-stu-id="479a0-184">Unless BGP is enabled in hello connection property, Azure will not enable BGP for this connection even though BGP parameters are already configured on both gateways.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

<span data-ttu-id="479a0-185">Merhaba aşağıdaki örnekte bu alıştırmada, şirket içi VPN cihazınızın BGP yapılandırma bölümü hello girin hello parametreleri listelenir:</span><span class="sxs-lookup"><span data-stu-id="479a0-185">hello following example lists hello parameters you enter into hello BGP configuration section on your on-premises VPN device for this exercise:</span></span>

```

- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes tooannounce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP    : 10.12.255.30
- Static route         : Add a route for 10.12.255.30/32, with nexthop being hello VPN tunnel interface on your device
- eBGP Multihop        : Ensure hello "multihop" option for eBGP is enabled on your device if needed
```

<span data-ttu-id="479a0-186">Merhaba IPSec bağlantısı kurulduktan sonra birkaç dakika ve hello BGP eşliği oturumu başlatır sonra hello bağlantı kurulur.</span><span class="sxs-lookup"><span data-stu-id="479a0-186">hello connection is established after a few minutes, and hello BGP peering session starts once hello IPsec connection is established.</span></span>

## <span data-ttu-id="479a0-187"><a name ="v2vbgp"></a>Bölüm 3 - BGP VNet-VNet bağlantı Kur</span><span class="sxs-lookup"><span data-stu-id="479a0-187"><a name ="v2vbgp"></a>Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>

<span data-ttu-id="479a0-188">Bu bölüm BGP ile VNet-VNet bağlantı hello Aşağıdaki diyagramda gösterildiği gibi ekler:</span><span class="sxs-lookup"><span data-stu-id="479a0-188">This section adds a VNet-to-VNet connection with BGP, as shown in hello following diagram:</span></span>

![BGP VNet-VNet için](./media/vpn-gateway-bgp-resource-manager-ps/bgp-vnet2vnet.png)

<span data-ttu-id="479a0-190">yönergeleri izleyerek hello hello önceki adımlardan devam edin.</span><span class="sxs-lookup"><span data-stu-id="479a0-190">hello following instructions continue from hello previous steps.</span></span> <span data-ttu-id="479a0-191">Tamamlamanız gereken [bölümü ı](#enablebgp) toocreate TestVNet1 yapılandırmak ve VPN ağ geçidi BGP ile Merhaba.</span><span class="sxs-lookup"><span data-stu-id="479a0-191">You must complete [Part I](#enablebgp) toocreate and configure TestVNet1 and hello VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-hello-vpn-gateway"></a><span data-ttu-id="479a0-192">1. adım - TestVNet2 ve hello VPN ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="479a0-192">Step 1 - Create TestVNet2 and hello VPN gateway</span></span>

<span data-ttu-id="479a0-193">Önemli toomake hello IP adres alanı hello yeni sanal ağın TestVNet2, herhangi bir VNet aralıkları ile çakışmaması emin olur.</span><span class="sxs-lookup"><span data-stu-id="479a0-193">It is important toomake sure that hello IP address space of hello new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="479a0-194">Bu örnekte, sanal ağlar hello toohello ait aynı abonelik.</span><span class="sxs-lookup"><span data-stu-id="479a0-194">In this example, hello virtual networks belong toohello same subscription.</span></span> <span data-ttu-id="479a0-195">VNet-VNet bağlantıları farklı abonelikler arasında ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="479a0-195">You can set up VNet-to-VNet connections between different subscriptions.</span></span> <span data-ttu-id="479a0-196">Daha fazla bilgi için bkz: [VNet-VNet bağlantı yapılandırma](vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="479a0-196">For more information, see [Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md).</span></span> <span data-ttu-id="479a0-197">Merhaba eklediğinizden emin olun "-EnableBgp $True" ne zaman oluşturmaya izin ver hello bağlantıları tooenable BGP.</span><span class="sxs-lookup"><span data-stu-id="479a0-197">Make sure you add hello "-EnableBgp $True" when creating hello connections tooenable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="479a0-198">1. Değişkenlerinizi bildirme</span><span class="sxs-lookup"><span data-stu-id="479a0-198">1. Declare your variables</span></span>

<span data-ttu-id="479a0-199">Merhaba olanları hello değerlerle emin tooreplace olması yapılandırmanızın toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="479a0-199">Be sure tooreplace hello values with hello ones that you want toouse for your configuration.</span></span>

```powershell
$RG2 = "TestBGPRG2"
$Location2 = "West US"
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
$GWIPName2 = "VNet2GWIP"
$GWIPconfName2 = "gwipconf2"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-testvnet2-in-hello-new-resource-group"></a><span data-ttu-id="479a0-200">2. TestVNet2 hello yeni kaynak grubu oluştur</span><span class="sxs-lookup"><span data-stu-id="479a0-200">2. Create TestVNet2 in hello new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-hello-vpn-gateway-for-testvnet2-with-bgp-parameters"></a><span data-ttu-id="479a0-201">3. Merhaba VPN ağ geçidi BGP parametrelerle TestVNet2 için oluşturma</span><span class="sxs-lookup"><span data-stu-id="479a0-201">3. Create hello VPN gateway for TestVNet2 with BGP parameters</span></span>

<span data-ttu-id="479a0-202">Ağınız için oluşturacak ve gerekli hello alt ağ ve IP yapılandırmaları tanımlamak bir ortak IP adresi toobe ayrılmış toohello ağ geçidi isteği.</span><span class="sxs-lookup"><span data-stu-id="479a0-202">Request a public IP address toobe allocated toohello gateway you will create for your VNet and define hello required subnet and IP configurations.</span></span>

```powershell
$gwpip2    = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2     = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gwipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName2 -Subnet $subnet2 -PublicIpAddress $gwpip2
```

<span data-ttu-id="479a0-203">Merhaba VPN ağ geçidi ile Merhaba oluşturmak sayı olarak.</span><span class="sxs-lookup"><span data-stu-id="479a0-203">Create hello VPN gateway with hello AS number.</span></span> <span data-ttu-id="479a0-204">Merhaba varsayılan ASN, Azure VPN ağ geçitlerinde geçersiz kılmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="479a0-204">You must override hello default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="479a0-205">Merhaba Asn'ler hello bağlı sanal ağlar farklı tooenable BGP ve transit yönlendirme olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="479a0-205">hello ASNs for hello connected VNets must be different tooenable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gwipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku Standard -Asn $VNet2ASN
```

### <a name="step-2---connect-hello-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="479a0-206">2. adım - hello TestVNet1 ve TestVNet2 ağ geçitleri Bağlan</span><span class="sxs-lookup"><span data-stu-id="479a0-206">Step 2 - Connect hello TestVNet1 and TestVNet2 gateways</span></span>

<span data-ttu-id="479a0-207">Bu örnekte, her iki ağ geçitleri hello olan aynı abonelik.</span><span class="sxs-lookup"><span data-stu-id="479a0-207">In this example, both gateways are in hello same subscription.</span></span> <span data-ttu-id="479a0-208">Bu adımda hello tamamlayabilirsiniz aynı PowerShell oturumunda.</span><span class="sxs-lookup"><span data-stu-id="479a0-208">You can complete this step in hello same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="479a0-209">1. Her iki ağ geçitleri Al</span><span class="sxs-lookup"><span data-stu-id="479a0-209">1. Get both gateways</span></span>

<span data-ttu-id="479a0-210">Oturum açma ve tooSubscription 1 bağlanmak emin olun.</span><span class="sxs-lookup"><span data-stu-id="479a0-210">Make sure you log in and connect tooSubscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="479a0-211">2. Her iki bağlantı oluşturma</span><span class="sxs-lookup"><span data-stu-id="479a0-211">2. Create both connections</span></span>

<span data-ttu-id="479a0-212">Bu adımda, TestVNet2 tooTestVNet1 TestVNet1 tooTestVNet2 hello bağlantısından ve hello bağlantı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="479a0-212">In this step, you create hello connection from TestVNet1 tooTestVNet2, and hello connection from TestVNet2 tooTestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="479a0-213">Her iki bağlantılarında emin tooenable BGP olması.</span><span class="sxs-lookup"><span data-stu-id="479a0-213">Be sure tooenable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="479a0-214">Bu adımları tamamladıktan sonra birkaç dakika sonra hello bağlantı kurulur.</span><span class="sxs-lookup"><span data-stu-id="479a0-214">After completing these steps, hello connection is established after a few minutes.</span></span> <span data-ttu-id="479a0-215">Merhaba VNet-VNet bağlantı tamamlandığında hello BGP eşliği oturumu çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="479a0-215">hello BGP peering session is up once hello VNet-to-VNet connection is completed.</span></span>

<span data-ttu-id="479a0-216">Bu alıştırmada, tüm üç bölümden tamamladıysa, ağ topolojisi aşağıdaki hello kurduğunuz:</span><span class="sxs-lookup"><span data-stu-id="479a0-216">If you completed all three parts of this exercise, you have established hello following network topology:</span></span>

![BGP VNet-VNet için](./media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

## <a name="next-steps"></a><span data-ttu-id="479a0-218">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="479a0-218">Next steps</span></span>

<span data-ttu-id="479a0-219">Bağlantınız tamamlandıktan sonra sanal makineleri tooyour sanal ağları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="479a0-219">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="479a0-220">Adımlar için bkz. [Sanal Makine Oluşturma](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="479a0-220">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
