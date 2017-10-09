---
title: "Azure VPN ağ geçitleri toomultiple şirket içi ilke tabanlı VPN aygıtlarını bağlamak: Azure Resource Manager: PowerShell | Microsoft Docs"
description: "Bu makalede Azure Resource Manager ve PowerShell kullanarak Azure yol tabanlı VPN ağ geçidi toomultiple ilke tabanlı VPN aygıtları nasıl yapılandıracağınız anlatılmaktadır."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/27/2017
ms.author: yushwang
ms.openlocfilehash: 866c78d96305207106a66cc3300c355e4b6bfbb7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-azure-vpn-gateways-toomultiple-on-premises-policy-based-vpn-devices-using-powershell"></a><span data-ttu-id="71d86-103">PowerShell kullanarak Azure VPN ağ geçitleri toomultiple şirket içi ilke tabanlı VPN aygıtlarını bağlamak</span><span class="sxs-lookup"><span data-stu-id="71d86-103">Connect Azure VPN gateways toomultiple on-premises policy-based VPN devices using PowerShell</span></span>

<span data-ttu-id="71d86-104">Bu makalede özel IPSec/IKE ilkeler S2S VPN bağlantılarında yararlanan bir Azure yol tabanlı VPN ağ geçidi tooconnect toomultiple şirket içi ilke tabanlı VPN aygıtları yapılandırmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="71d86-104">This article helps you configure an Azure route-based VPN gateway tooconnect toomultiple on-premises policy-based VPN devices leveraging custom IPsec/IKE policies on S2S VPN connections.</span></span>

## <a name="about-policy-based-and-route-based-vpn-gateways"></a><span data-ttu-id="71d86-105">İlke tabanlı ve rota tabanlı VPN ağ geçitleri hakkında</span><span class="sxs-lookup"><span data-stu-id="71d86-105">About policy-based and route-based VPN gateways</span></span>

<span data-ttu-id="71d86-106">İlke - *karşılaştırması* rota tabanlı VPN aygıtları farklı hello IPSec trafiği seçici bir bağlantıda nasıl ayarlanır:</span><span class="sxs-lookup"><span data-stu-id="71d86-106">Policy- *vs.* route-based VPN devices differ in how hello IPsec traffic selectors are set on a connection:</span></span>

* <span data-ttu-id="71d86-107">**İlke tabanlı** VPN aygıtları nasıl trafiği şifrelenmiş/şifresi IPSec tüneller hem ağları toodefine ön ekleri hello birleşimlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="71d86-107">**Policy-based** VPN devices use hello combinations of prefixes from both networks toodefine how traffic is encrypted/decrypted through IPsec tunnels.</span></span> <span data-ttu-id="71d86-108">Bu genelde paket filtreleme gerçekleştiren güvenlik duvarı cihazlarda yerleşik olarak bulunur.</span><span class="sxs-lookup"><span data-stu-id="71d86-108">It is typically built on firewall devices that perform packet filtering.</span></span> <span data-ttu-id="71d86-109">IPSec tüneli şifreleme ve şifre çözme toohello paket filtreleme ve işleme altyapısı eklenir.</span><span class="sxs-lookup"><span data-stu-id="71d86-109">IPsec tunnel encryption and decryption are added toohello packet filtering and processing engine.</span></span>
* <span data-ttu-id="71d86-110">**Rota tabanlı** let yönlendirme iletme tabloları doğrudan trafiği toodifferent IPSec tünelleri ve VPN aygıtları kullanın herhangi herhangi (joker karakterler) trafiği seçicileri.</span><span class="sxs-lookup"><span data-stu-id="71d86-110">**Route-based** VPN devices use any-to-any (wildcard) traffic selectors, and let routing/forwarding tables direct traffic toodifferent IPsec tunnels.</span></span> <span data-ttu-id="71d86-111">Genellikle, burada her IPSec tüneli bir ağ arabirimi veya VTI (sanal tünel arabirimi) olarak modellenir yönlendirici platformlarda oluşturulmuştur.</span><span class="sxs-lookup"><span data-stu-id="71d86-111">It is typically built on router platforms where each IPsec tunnel is modeled as a network interface or VTI (virtual tunnel interface).</span></span>

<span data-ttu-id="71d86-112">Merhaba aşağıdaki diyagramlarda hello iki modeli vurgula:</span><span class="sxs-lookup"><span data-stu-id="71d86-112">hello following diagrams highlight hello two models:</span></span>

### <a name="policy-based-vpn-example"></a><span data-ttu-id="71d86-113">İlke tabanlı VPN örneği</span><span class="sxs-lookup"><span data-stu-id="71d86-113">Policy-based VPN example</span></span>
![İlke tabanlı](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedmultisite.png)

### <a name="route-based-vpn-example"></a><span data-ttu-id="71d86-115">Rota tabanlı VPN örneği</span><span class="sxs-lookup"><span data-stu-id="71d86-115">Route-based VPN example</span></span>
![Rota tabanlı](./media/vpn-gateway-connect-multiple-policybased-rm-ps/routebasedmultisite.png)

### <a name="azure-support-for-policy-based-vpn"></a><span data-ttu-id="71d86-117">Azure ilke temelli VPN desteği</span><span class="sxs-lookup"><span data-stu-id="71d86-117">Azure support for policy-based VPN</span></span>
<span data-ttu-id="71d86-118">Şu anda Azure VPN ağ geçitlerinin iki modlarını destekler: rota tabanlı VPN ağ geçitleri ve ilke tabanlı VPN ağ geçitleri.</span><span class="sxs-lookup"><span data-stu-id="71d86-118">Currently, Azure supports both modes of VPN gateways: route-based VPN gateways and policy-based VPN gateways.</span></span> <span data-ttu-id="71d86-119">Farklı teknik özelliklerine sonucunda, farklı platformlarda iç oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="71d86-119">They are built on different internal platforms, which result in different specifications:</span></span>

|                          | <span data-ttu-id="71d86-120">**PolicyBased VPN ağ geçidi**</span><span class="sxs-lookup"><span data-stu-id="71d86-120">**PolicyBased VPN Gateway**</span></span> | <span data-ttu-id="71d86-121">**RouteBased VPN ağ geçidi**</span><span class="sxs-lookup"><span data-stu-id="71d86-121">**RouteBased VPN Gateway**</span></span>               |
| ---                      | ---                         | ---                                      |
| <span data-ttu-id="71d86-122">**Azure ağ geçidi SKU'su**</span><span class="sxs-lookup"><span data-stu-id="71d86-122">**Azure Gateway SKU**</span></span>    | <span data-ttu-id="71d86-123">Temel</span><span class="sxs-lookup"><span data-stu-id="71d86-123">Basic</span></span>                       | <span data-ttu-id="71d86-124">Temel, standart, HighPerformance</span><span class="sxs-lookup"><span data-stu-id="71d86-124">Basic, Standard, HighPerformance</span></span>         |
| <span data-ttu-id="71d86-125">**IKE sürümü**</span><span class="sxs-lookup"><span data-stu-id="71d86-125">**IKE version**</span></span>          | <span data-ttu-id="71d86-126">IKEv1</span><span class="sxs-lookup"><span data-stu-id="71d86-126">IKEv1</span></span>                       | <span data-ttu-id="71d86-127">IKEv2</span><span class="sxs-lookup"><span data-stu-id="71d86-127">IKEv2</span></span>                                    |
| <span data-ttu-id="71d86-128">**Maks. S2S bağlantılarının**</span><span class="sxs-lookup"><span data-stu-id="71d86-128">**Max. S2S connections**</span></span> | <span data-ttu-id="71d86-129">**1**</span><span class="sxs-lookup"><span data-stu-id="71d86-129">**1**</span></span>                       | <span data-ttu-id="71d86-130">Basic/standart: 10</span><span class="sxs-lookup"><span data-stu-id="71d86-130">Basic/Standard: 10</span></span><br> <span data-ttu-id="71d86-131">HighPerformance: 30</span><span class="sxs-lookup"><span data-stu-id="71d86-131">HighPerformance: 30</span></span> |
|                          |                             |                                          |

<span data-ttu-id="71d86-132">Merhaba özel IPSec/IKE ilkesiyle Azure rota tabanlı VPN ağ geçitleri toouse öneki tabanlı trafik Seçici seçeneği ile artık yapılandırabilirsiniz "**PolicyBasedTrafficSelectors**", tooconnect tooon içi ilke tabanlı VPN aygıtları.</span><span class="sxs-lookup"><span data-stu-id="71d86-132">With hello custom IPsec/IKE policy, you can now configure Azure route-based VPN gateways toouse prefix-based traffic selectors with option "**PolicyBasedTrafficSelectors**", tooconnect tooon-premises policy-based VPN devices.</span></span> <span data-ttu-id="71d86-133">Bu özellik bir Azure sanal ağdan tooconnect sağlar ve VPN ağ geçidi toomultiple ilke tabanlı VPN/güvenlik duvarı aygıtları hello tek bağlantı sınırı hello geçerli Azure ilke tabanlı VPN Gateway bileşenlerinden kaldırma, şirket içi.</span><span class="sxs-lookup"><span data-stu-id="71d86-133">This capability allows you tooconnect from an Azure virtual network and VPN gateway toomultiple on-premises policy-based VPN/firewall devices, removing hello single connection limit from hello current Azure policy-based VPN gateways.</span></span>

> [!IMPORTANT]
> 1. <span data-ttu-id="71d86-134">tooenable Bu bağlantı, şirket içi ilke tabanlı VPN aygıtları desteklemelidir **Ikev2** tooconnect toohello Azure yol tabanlı VPN ağ geçitleri.</span><span class="sxs-lookup"><span data-stu-id="71d86-134">tooenable this connectivity, your on-premises policy-based VPN devices must support **IKEv2** tooconnect toohello Azure route-based VPN gateways.</span></span> <span data-ttu-id="71d86-135">VPN aygıt belirtimlerine bakın.</span><span class="sxs-lookup"><span data-stu-id="71d86-135">Check your VPN device specifications.</span></span>
> 2. <span data-ttu-id="71d86-136">Merhaba şirket içi ağlar ile bu düzenek ilke tabanlı VPN aygıtları bağlanma yalnızca toohello Azure sanal ağı bağlanabilir; **tooother şirket içi ağlar transit olamaz veya aracılığıyla sanal ağlar aynı Azure VPN ağ geçidi hello**.</span><span class="sxs-lookup"><span data-stu-id="71d86-136">hello on-premises networks connecting through policy-based VPN devices with this mechanism can only connect toohello Azure virtual network; **they cannot transit tooother on-premises networks or virtual networks via hello same Azure VPN gateway**.</span></span>
> 3. <span data-ttu-id="71d86-137">Merhaba yapılandırma seçeneği hello özel IPSec/IKE bağlantı İlkesi bir parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="71d86-137">hello configuration option is part of hello custom IPsec/IKE connection policy.</span></span> <span data-ttu-id="71d86-138">Merhaba ilke tabanlı trafik Seçici seçeneği etkinleştirirseniz, hello tam İlkesi (IPSec/IKE şifreleme ve bütünlük algoritmalar, anahtar gücü ve SA yaşam süreleri) belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="71d86-138">If you enable hello policy-based traffic selector option, you must specify hello complete policy (IPsec/IKE encryption and integrity algorithms, key strengths, and SA lifetimes).</span></span>

<span data-ttu-id="71d86-139">Aşağıdaki diyagramda hello Azure VPN ağ geçidi transit yönlendirme hello ilke tabanlı seçeneğiyle neden çalışmıyor gösterir:</span><span class="sxs-lookup"><span data-stu-id="71d86-139">hello following diagram shows why transit routing via Azure VPN gateway doesn't work with hello policy-based option:</span></span>

![İlke tabanlı geçiş](./media/vpn-gateway-connect-multiple-policybased-rm-ps/policybasedtransit.png)

<span data-ttu-id="71d86-141">Hello diyagramda gösterildiği gibi hello Azure VPN ağ geçidi hello sanal ağ tooeach hello şirket içi ağ önekleri ancak hello arası bağlantı önekleri gelen trafik Seçici vardır.</span><span class="sxs-lookup"><span data-stu-id="71d86-141">As shown in hello diagram, hello Azure VPN gateway has traffic selectors from hello virtual network tooeach of hello on-premises network prefixes, but not hello cross-connection prefixes.</span></span> <span data-ttu-id="71d86-142">Örneğin, şirket içi site 2, 3 site ve site 4 her tooVNet1 sırasıyla iletişim kurabilir ancak hello Azure VPN ağ geçidi tooeach diğer bağlanamıyor.</span><span class="sxs-lookup"><span data-stu-id="71d86-142">For example, on-premises site 2, site 3, and site 4 can each communicate tooVNet1 respectively, but cannot connect via hello Azure VPN gateway tooeach other.</span></span> <span data-ttu-id="71d86-143">Merhaba diyagramda gösterilmektedir hello hello Azure VPN ağ geçidi bu yapılandırma bölümünde kullanılamayan trafiğini Seçici arası bağlanın.</span><span class="sxs-lookup"><span data-stu-id="71d86-143">hello diagram shows hello cross-connect traffic selectors that are not available in hello Azure VPN gateway under this configuration.</span></span>

## <a name="configure-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="71d86-144">İlke tabanlı trafik seçici bir bağlantıda yapılandırın</span><span class="sxs-lookup"><span data-stu-id="71d86-144">Configure policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="71d86-145">Merhaba bu makalede İzleme'ndaki yönergeleri aynı hello açıklandığı gibi örnek [S2S veya VNet-VNet bağlantıları için IPSec/IKE yapılandırma İlkesi](vpn-gateway-ipsecikepolicy-rm-powershell.md) tooestablish S2S VPN bağlantısı.</span><span class="sxs-lookup"><span data-stu-id="71d86-145">hello instructions in this article follow hello same example as described in [Configure IPsec/IKE policy for S2S or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) tooestablish a S2S VPN connection.</span></span> <span data-ttu-id="71d86-146">Bu diyagramda aşağıdaki hello gösterilir:</span><span class="sxs-lookup"><span data-stu-id="71d86-146">This is shown in hello following diagram:</span></span>

![s2s İlkesi](./media/vpn-gateway-connect-multiple-policybased-rm-ps/s2spolicypb.png)

<span data-ttu-id="71d86-148">İş akışı tooenable Bu bağlantı hello:</span><span class="sxs-lookup"><span data-stu-id="71d86-148">hello workflow tooenable this connectivity:</span></span>
1. <span data-ttu-id="71d86-149">Hello sanal ağ, VPN ağ geçidi ve yerel ağ geçidi, şirket içi bağlantı oluşturma</span><span class="sxs-lookup"><span data-stu-id="71d86-149">Create hello virtual network, VPN gateway, and local network gateway for your cross-premises connection</span></span>
2. <span data-ttu-id="71d86-150">Bir IPSec/IKE ilkesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="71d86-150">Create an IPsec/IKE policy</span></span>
3. <span data-ttu-id="71d86-151">S2S veya VNet-VNet bağlantısı oluşturduğunuzda hello ilkesi uygulamak ve **hello ilke tabanlı trafik Seçici etkinleştirmek** hello bağlantısı</span><span class="sxs-lookup"><span data-stu-id="71d86-151">Apply hello policy when you create a S2S or VNet-to-VNet connection, and **enable hello policy-based traffic selectors** on hello connection</span></span>
4. <span data-ttu-id="71d86-152">Merhaba bağlantıyı zaten oluşturduysanız, uygulama veya hello İlkesi tooan var olan bağlantıyı güncelleştir</span><span class="sxs-lookup"><span data-stu-id="71d86-152">If hello connection is already created, you can apply or update hello policy tooan existing connection</span></span>

## <a name="enable-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="71d86-153">İlke tabanlı trafik seçici bir bağlantısı etkinleştir</span><span class="sxs-lookup"><span data-stu-id="71d86-153">Enable policy-based traffic selectors on a connection</span></span>

<span data-ttu-id="71d86-154">Tamamladığınızdan emin olun [bölümü 3 hello IPSec/IKE yapılandırma İlkesi makalenin](vpn-gateway-ipsecikepolicy-rm-powershell.md) Bu bölüm için.</span><span class="sxs-lookup"><span data-stu-id="71d86-154">Make sure you have completed [Part 3 of hello Configure IPsec/IKE policy article](vpn-gateway-ipsecikepolicy-rm-powershell.md) for this section.</span></span> <span data-ttu-id="71d86-155">örnek kullanımları aşağıdaki hello aynı parametreleri ve adımları hello:</span><span class="sxs-lookup"><span data-stu-id="71d86-155">hello following example uses hello same parameters and steps:</span></span>

### <a name="step-1---create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="71d86-156">1. adım - hello sanal ağ, VPN ağ geçidi ve yerel ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="71d86-156">Step 1 - Create hello virtual network, VPN gateway, and local network gateway</span></span>

#### <a name="1-declare-your-variables--connect-tooyour-subscription"></a><span data-ttu-id="71d86-157">1. Değişkenlerinizi bildirme & tooyour. abonelik'e bağlanma</span><span class="sxs-lookup"><span data-stu-id="71d86-157">1. Declare your variables & connect tooyour subscription</span></span>
<span data-ttu-id="71d86-158">Bu alıştırmada, değişkenlerimizi bildirerek başlayın.</span><span class="sxs-lookup"><span data-stu-id="71d86-158">For this exercise, we start by declaring our variables.</span></span> <span data-ttu-id="71d86-159">Üretim için yapılandırma emin tooreplace hello değerleri kendi değerlerinizle olabilir.</span><span class="sxs-lookup"><span data-stu-id="71d86-159">Be sure tooreplace hello values with your own when configuring for production.</span></span>

```powershell
$Sub1          = "<YourSubscriptionName>"
$RG1           = "TestPolicyRG1"
$Location1     = "East US 2"
$VNetName1     = "TestVNet1"
$FESubName1    = "FrontEnd"
$BESubName1    = "Backend"
$GWSubName1    = "GatewaySubnet"
$VNetPrefix11  = "10.11.0.0/16"
$VNetPrefix12  = "10.12.0.0/16"
$FESubPrefix1  = "10.11.0.0/24"
$BESubPrefix1  = "10.12.0.0/24"
$GWSubPrefix1  = "10.12.255.0/27"
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GW1IPName1    = "VNet1GWIP1"
$GW1IPconf1    = "gw1ipconf1"
$Connection16  = "VNet1toSite6"

$LNGName6      = "Site6"
$LNGPrefix61   = "10.61.0.0/16"
$LNGPrefix62   = "10.62.0.0/16"
$LNGIP6        = "131.107.72.22"
```
<span data-ttu-id="71d86-160">toouse hello Resource Manager cmdlet'lerini tooPowerShell moduna geçtiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="71d86-160">toouse hello Resource Manager cmdlets, make sure you switch tooPowerShell mode.</span></span> <span data-ttu-id="71d86-161">Daha fazla bilgi için [Windows PowerShell’i Resource Manager ile kullanma](../powershell-azure-resource-manager.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="71d86-161">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="71d86-162">PowerShell Konsolunuzu açın ve tooyour hesap bağlanın.</span><span class="sxs-lookup"><span data-stu-id="71d86-162">Open your PowerShell console and connect tooyour account.</span></span> <span data-ttu-id="71d86-163">Bağlandığınız örnek toohelp aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="71d86-163">Use hello following sample toohelp you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="2-create-hello-virtual-network-vpn-gateway-and-local-network-gateway"></a><span data-ttu-id="71d86-164">2. Merhaba sanal ağ, VPN ağ geçidi ve yerel ağ geçidi oluşturma</span><span class="sxs-lookup"><span data-stu-id="71d86-164">2. Create hello virtual network, VPN gateway, and local network gateway</span></span>
<span data-ttu-id="71d86-165">Aşağıdaki örneğine hello hello sanal ağ, TestVNet1 üç alt ağları ve hello VPN ağ geçidi ile oluşturur.</span><span class="sxs-lookup"><span data-stu-id="71d86-165">hello following example creates hello virtual network, TestVNet1 with three subnets, and hello VPN gateway.</span></span> <span data-ttu-id="71d86-166">Değerleri değiştirerek, ağ geçidi alt ağınızı her zaman özellikle 'GatewaySubnet' adını önemlidir.</span><span class="sxs-lookup"><span data-stu-id="71d86-166">When substituting values, it's important that you always name your gateway subnet specifically 'GatewaySubnet'.</span></span> <span data-ttu-id="71d86-167">Başka bir ad kullanırsanız ağ geçidi oluşturma işleminiz başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="71d86-167">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

$gw1pip1    = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1      = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1    = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance

New-AzureRmLocalNetworkGateway -Name $LNGName6 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP6 -AddressPrefix $LNGPrefix61,$LNGPrefix62
```

### <a name="step-2---create-a-s2s-vpn-connection-with-an-ipsecike-policy"></a><span data-ttu-id="71d86-168">2. adım - bir IPSec/IKE İlkesi ile bir S2S VPN bağlantısı oluşturun</span><span class="sxs-lookup"><span data-stu-id="71d86-168">Step 2 - Create a S2S VPN connection with an IPsec/IKE policy</span></span>

#### <a name="1-create-an-ipsecike-policy"></a><span data-ttu-id="71d86-169">1. Bir IPSec/IKE ilkesi oluşturun</span><span class="sxs-lookup"><span data-stu-id="71d86-169">1. Create an IPsec/IKE policy</span></span>

> [!IMPORTANT]
> <span data-ttu-id="71d86-170">Toocreate sipariş tooenable "UsePolicyBasedTrafficSelectors" seçeneği hello bağlantı IPSec/IKE ilkesinde gerekir.</span><span class="sxs-lookup"><span data-stu-id="71d86-170">You need toocreate an IPsec/IKE policy in order tooenable "UsePolicyBasedTrafficSelectors" option on hello connection.</span></span>

<span data-ttu-id="71d86-171">Merhaba aşağıdaki örnekte bir IPSec/IKE İlkesi bu algoritmaları ve parametreleri oluşturur:</span><span class="sxs-lookup"><span data-stu-id="71d86-171">hello following example creates an IPsec/IKE policy with these algorithms and parameters:</span></span>
* <span data-ttu-id="71d86-172">Ikev2: AES256, SHA384 DHGroup24</span><span class="sxs-lookup"><span data-stu-id="71d86-172">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="71d86-173">IPSec: AES256, SHA256, PFS24, SA ömrü 3600 saniye & 2048KB</span><span class="sxs-lookup"><span data-stu-id="71d86-173">IPsec: AES256, SHA256, PFS24, SA Lifetime 3600 seconds & 2048KB</span></span>

```powershell
$ipsecpolicy6 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA256 -PfsGroup PFS24 -SALifeTimeSeconds 3600 -SADataSizeKilobytes 2048
```

#### <a name="2-create-hello-s2s-vpn-connection-with-policy-based-traffic-selectors-and-ipsecike-policy"></a><span data-ttu-id="71d86-174">2. İlke tabanlı trafik Seçici ve IPSec/IKE İlkesi ile Merhaba S2S VPN bağlantısı oluşturun</span><span class="sxs-lookup"><span data-stu-id="71d86-174">2. Create hello S2S VPN connection with policy-based traffic selectors and IPsec/IKE policy</span></span>
<span data-ttu-id="71d86-175">S2S VPN bağlantısı oluşturun ve hello önceki adımda oluşturduğunuz hello IPSec/IKE İlkesi uygulayın.</span><span class="sxs-lookup"><span data-stu-id="71d86-175">Create an S2S VPN connection and apply hello IPsec/IKE policy created in hello previous step.</span></span> <span data-ttu-id="71d86-176">Merhaba ek parametresinin unutmayın "-UsePolicyBasedTrafficSelectors $True" Merhaba bağlantıda ilke tabanlı trafik Seçici sağlar.</span><span class="sxs-lookup"><span data-stu-id="71d86-176">Be aware of hello additional parameter "-UsePolicyBasedTrafficSelectors $True"  which enables policy-based traffic selectors on hello connection.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng6 = Get-AzureRmLocalNetworkGateway  -Name $LNGName6 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng6 -Location $Location1 -ConnectionType IPsec -UsePolicyBasedTrafficSelectors $True -IpsecPolicies $ipsecpolicy6 -SharedKey 'AzureA1b2C3'
```

<span data-ttu-id="71d86-177">Hello adımları tamamladıktan sonra hello S2S VPN bağlantısı hello IPSec/IKE ilkesi tanımlı kullanın ve ilke tabanlı trafik Seçici hello bağlantıda etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="71d86-177">After completing hello steps, hello S2S VPN connection will use hello IPsec/IKE policy defined, and enable policy-based traffic selectors on hello connection.</span></span> <span data-ttu-id="71d86-178">Daha fazla bağlantıları tooadditional şirket içi ilke tabanlı VPN aygıtlardan aynı adımları tooadd hello yineleyebilirsiniz hello aynı Azure VPN ağ geçidi.</span><span class="sxs-lookup"><span data-stu-id="71d86-178">You can repeat hello same steps tooadd more connections tooadditional on-premises policy-based VPN devices from hello same Azure VPN gateway.</span></span>

## <a name="update-policy-based-traffic-selectors-for-a-connection"></a><span data-ttu-id="71d86-179">İlke tabanlı trafik Seçici bağlantı güncelleştir</span><span class="sxs-lookup"><span data-stu-id="71d86-179">Update policy-based traffic selectors for a connection</span></span>
<span data-ttu-id="71d86-180">Merhaba son Kısım nasıl var olan bir S2S VPN bağlantısı için tooupdate hello ilke tabanlı trafik Seçici seçeneği gösterir.</span><span class="sxs-lookup"><span data-stu-id="71d86-180">hello last section shows you how tooupdate hello policy-based traffic selectors option for an existing  S2S VPN connection.</span></span>

### <a name="1-get-hello-connection"></a><span data-ttu-id="71d86-181">1. Merhaba bağlantısını Al</span><span class="sxs-lookup"><span data-stu-id="71d86-181">1. Get hello connection</span></span>
<span data-ttu-id="71d86-182">Merhaba bağlantı kaynağı alın.</span><span class="sxs-lookup"><span data-stu-id="71d86-182">Get hello connection resource.</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1
```

### <a name="2-check-hello-policy-based-traffic-selectors-option"></a><span data-ttu-id="71d86-183">2. Merhaba ilke tabanlı trafik Seçici seçeneği işaretleyin.</span><span class="sxs-lookup"><span data-stu-id="71d86-183">2. Check hello policy-based traffic selectors option</span></span>
<span data-ttu-id="71d86-184">Merhaba aşağıdaki satırı hello ilke tabanlı trafik Seçici hello bağlantı için kullanılıp kullanılmadığını gösterir:</span><span class="sxs-lookup"><span data-stu-id="71d86-184">hello following line shows whether hello policy-based traffic selectors are used for hello connection:</span></span>

```powershell
$connection6.UsePolicyBasedTrafficSelectors
```

<span data-ttu-id="71d86-185">Merhaba satır döndürürse "**True**", ardından ilke tabanlı trafik Seçici hello bağlantısında yapılandırılmış; Aksi halde döndürür "**False**."</span><span class="sxs-lookup"><span data-stu-id="71d86-185">If hello line returns "**True**", then policy-based traffic selectors are configured on hello connection; otherwise it returns "**False**."</span></span>

### <a name="3-update-hello-policy-based-traffic-selectors-on-a-connection"></a><span data-ttu-id="71d86-186">3. Merhaba ilke tabanlı trafik seçici bir bağlantısı güncelleştir</span><span class="sxs-lookup"><span data-stu-id="71d86-186">3. Update hello policy-based traffic selectors on a connection</span></span>
<span data-ttu-id="71d86-187">Merhaba bağlantı kaynağı edindikten sonra etkinleştirebilir veya hello seçeneğini devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="71d86-187">Once you obtain hello connection resource, you can enable or disable hello option.</span></span>

#### <a name="disable-usepolicybasedtrafficselectors"></a><span data-ttu-id="71d86-188">UsePolicyBasedTrafficSelectors devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="71d86-188">Disable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="71d86-189">Merhaba aşağıdaki örnek hello ilke tabanlı trafik Seçici seçeneği devre dışı bırakır, ancak IPSec/IKE İlkesi değiştirmeden bırakır hello:</span><span class="sxs-lookup"><span data-stu-id="71d86-189">hello following example disables hello policy-based traffic selectors option, but leaves hello IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $False
```

#### <a name="enable-usepolicybasedtrafficselectors"></a><span data-ttu-id="71d86-190">UsePolicyBasedTrafficSelectors etkinleştir</span><span class="sxs-lookup"><span data-stu-id="71d86-190">Enable UsePolicyBasedTrafficSelectors</span></span>
<span data-ttu-id="71d86-191">Merhaba aşağıdaki örnek hello ilke tabanlı trafik Seçici seçeneği sağlar, ancak IPSec/IKE İlkesi değiştirmeden bırakır hello:</span><span class="sxs-lookup"><span data-stu-id="71d86-191">hello following example enables hello policy-based traffic selectors option, but leaves hello IPsec/IKE policy unchanged:</span></span>

```powershell
$RG1          = "TestPolicyRG1"
$Connection16 = "VNet1toSite6"
$connection6  = Get-AzureRmVirtualNetworkGatewayConnection -Name $Connection16 -ResourceGroupName $RG1

Set-AzureRmVirtualNetworkGatewayConnection -VirtualNetworkGatewayConnection $connection6 -UsePolicyBasedTrafficSelectors $True
```

## <a name="next-steps"></a><span data-ttu-id="71d86-192">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="71d86-192">Next steps</span></span>
<span data-ttu-id="71d86-193">Bağlantınız tamamlandıktan sonra sanal makineleri tooyour sanal ağları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="71d86-193">Once your connection is complete, you can add virtual machines tooyour virtual networks.</span></span> <span data-ttu-id="71d86-194">Adımlar için bkz. [Sanal Makine Oluşturma](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="71d86-194">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>

<span data-ttu-id="71d86-195">Ayrıca gözden [S2S VPN veya VNet-VNet bağlantıları için IPSec/IKE yapılandırma İlkesi](vpn-gateway-ipsecikepolicy-rm-powershell.md) özel IPSec/IKE ilkeleri hakkında daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="71d86-195">Also review [Configure IPsec/IKE policy for S2S VPN or VNet-to-VNet connections](vpn-gateway-ipsecikepolicy-rm-powershell.md) for more details on custom IPsec/IKE policies.</span></span>
