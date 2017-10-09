---
title: "aaaAbout 3 taraf VPN cihazı yapılandırma tooconnect tooAzure VPN ağ geçitleri | Microsoft Docs"
description: "Bu makalede tooAzure VPN ağ geçitlerini bağlama için 3 taraf VPN cihaz yapılandırmalarını genel bir bakış sağlar."
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: 
tags: 
ms.assetid: a8bfc955-de49-4172-95ac-5257e262d7ea
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/20/2017
ms.author: yushwang
ms.openlocfilehash: 3bb4fc94bc625386c2d0a02e1dcbdeb38ee0665e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-3rd-party-vpn-device-configurations"></a><span data-ttu-id="158aa-103">3 taraf VPN cihaz yapılandırmalarını genel bakış</span><span class="sxs-lookup"><span data-stu-id="158aa-103">Overview of 3rd party VPN device configurations</span></span>
<span data-ttu-id="158aa-104">Bu makalede, şirket içi VPN cihaz yapılandırmalarını tooAzure VPN ağ geçitlerini bağlama için genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="158aa-104">This article provides an overview of on-premises VPN device configurations for connecting tooAzure VPN gateways.</span></span> <span data-ttu-id="158aa-105">Merhaba örnek Azure sanal ağı ve kullanılan tooconnect toodifferent şirket içi VPN aygıtları hello ile aynı parametre olması VPN ağ geçidi Kurulum olacaktır.</span><span class="sxs-lookup"><span data-stu-id="158aa-105">hello sample Azure virtual network and VPN gateway setup will be used tooconnect toodifferent on-premises VPN devices with hello same parameters.</span></span>

## <a name="device-requirements"></a><span data-ttu-id="158aa-106">Cihaz gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="158aa-106">Device requirements</span></span>
<span data-ttu-id="158aa-107">Azure VPN ağ geçidi S2S VPN tünelleri için standart IPSec/IKE protokolü paketlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="158aa-107">Azure VPN gateways use standard IPsec/IKE protocol suites for S2S VPN tunnels.</span></span> <span data-ttu-id="158aa-108">Çok başvuran[VPN cihazları hakkında](vpn-gateway-about-vpn-devices.md) Merhaba IPSec/IKE protokolü parametreleri ve Azure VPN ağ geçitleri için varsayılan şifreleme algoritmalarının ayrıntılı.</span><span class="sxs-lookup"><span data-stu-id="158aa-108">Refer too[About VPN devices](vpn-gateway-about-vpn-devices.md) for hello detailed IPsec/IKE protocol parameters and default cryptographic algorithms for Azure VPN gateways.</span></span> <span data-ttu-id="158aa-109">Bölümünde açıklandığı gibi hello tam birleşimini şifreleme algoritmaları ve anahtar gücü belirli bir bağlantı için isteğe bağlı olarak belirtebilirsiniz [şifreleme gereksinimleri hakkında](vpn-gateway-about-compliance-crypto.md).</span><span class="sxs-lookup"><span data-stu-id="158aa-109">You can optionally specify hello exact combination of cryptographic algorithms and key strengths for a specific connection as described in [About cryptographic requirements](vpn-gateway-about-compliance-crypto.md).</span></span>

## <span data-ttu-id="158aa-110"><a name ="singletunnel"></a>Tek VPN tüneli</span><span class="sxs-lookup"><span data-stu-id="158aa-110"><a name ="singletunnel"></a>Single VPN tunnel</span></span>
<span data-ttu-id="158aa-111">bir Azure VPN ağ geçidi ve şirket içi VPN cihazınız arasındaki tek S2S VPN tüneli Hello ilk topoloji oluşur.</span><span class="sxs-lookup"><span data-stu-id="158aa-111">hello first topology consists of a single S2S VPN tunnel between an Azure VPN gateway and your on-premises VPN device.</span></span> <span data-ttu-id="158aa-112">BGP hello VPN tüneli üzerinden isteğe bağlı olarak yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="158aa-112">You can optionally configure BGP across hello VPN tunnel.</span></span>

![tek tünel](./media/vpn-gateway-3rdparty-device-config-overview/singletunnel.png)

<span data-ttu-id="158aa-114">Çok başvuran[siteden siteye bağlantı yapılandırma](vpn-gateway-howto-site-to-site-resource-manager-portal.md) ayrıntılı, adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="158aa-114">Refer too[Configure site-to-site connection](vpn-gateway-howto-site-to-site-resource-manager-portal.md) for detailed, step-by-step guidance.</span></span> <span data-ttu-id="158aa-115">Merhaba aşağıdaki bölümlerde hello parametreleri listelenmekte ve kullanmaya başlama örnek PowerShell komut dosyası toohelp sağlayın.</span><span class="sxs-lookup"><span data-stu-id="158aa-115">hello following sections list hello parameters and provide a sample PowerShell script toohelp you get started.</span></span>

### <a name="network-and-vpn-gateway-information"></a><span data-ttu-id="158aa-116">Ağ ve VPN ağ geçidi bilgileri</span><span class="sxs-lookup"><span data-stu-id="158aa-116">Network and VPN gateway information</span></span>
<span data-ttu-id="158aa-117">Bu bölümde yukarıdaki hello örnekler için hello parametreleri listeler.</span><span class="sxs-lookup"><span data-stu-id="158aa-117">This section list hello parameters for hello examples above.</span></span>

| <span data-ttu-id="158aa-118">**Parametre**</span><span class="sxs-lookup"><span data-stu-id="158aa-118">**Parameter**</span></span>                | <span data-ttu-id="158aa-119">**Değer**</span><span class="sxs-lookup"><span data-stu-id="158aa-119">**Value**</span></span>                    |
| ---                          | ---                          |
| <span data-ttu-id="158aa-120">VNet adres önekleri</span><span class="sxs-lookup"><span data-stu-id="158aa-120">VNet address prefixes</span></span>        | <span data-ttu-id="158aa-121">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="158aa-121">10.11.0.0/16</span></span><br><span data-ttu-id="158aa-122">10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="158aa-122">10.12.0.0/16</span></span> |
| <span data-ttu-id="158aa-123">Azure VPN ağ geçidi IP</span><span class="sxs-lookup"><span data-stu-id="158aa-123">Azure VPN gateway IP</span></span>         | <span data-ttu-id="158aa-124">Azure VPN ağ geçidi IP</span><span class="sxs-lookup"><span data-stu-id="158aa-124">Azure VPN Gateway IP</span></span>         |
| <span data-ttu-id="158aa-125">Şirket içi adres önekleri</span><span class="sxs-lookup"><span data-stu-id="158aa-125">On-premises address prefixes</span></span> | <span data-ttu-id="158aa-126">10.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="158aa-126">10.51.0.0/16</span></span><br><span data-ttu-id="158aa-127">10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="158aa-127">10.52.0.0/16</span></span> |
| <span data-ttu-id="158aa-128">Şirket içi VPN cihazının IP</span><span class="sxs-lookup"><span data-stu-id="158aa-128">On-premises VPN device IP</span></span>    | <span data-ttu-id="158aa-129">Şirket içi VPN cihazının IP</span><span class="sxs-lookup"><span data-stu-id="158aa-129">On-premises VPN device IP</span></span>    |
| <span data-ttu-id="158aa-130">* VNet BGP ASN</span><span class="sxs-lookup"><span data-stu-id="158aa-130">*VNet BGP ASN</span></span>                | <span data-ttu-id="158aa-131">65010</span><span class="sxs-lookup"><span data-stu-id="158aa-131">65010</span></span>                        |
| <span data-ttu-id="158aa-132">* Azure BGP eşdeğer IP</span><span class="sxs-lookup"><span data-stu-id="158aa-132">*Azure BGP peer IP</span></span>           | <span data-ttu-id="158aa-133">10.12.255.30</span><span class="sxs-lookup"><span data-stu-id="158aa-133">10.12.255.30</span></span>                 |
| <span data-ttu-id="158aa-134">* Şirket içi BGP ASN</span><span class="sxs-lookup"><span data-stu-id="158aa-134">*On-premises BGP ASN</span></span>         | <span data-ttu-id="158aa-135">65050</span><span class="sxs-lookup"><span data-stu-id="158aa-135">65050</span></span>                        |
| <span data-ttu-id="158aa-136">* Şirket içi BGP eşdeğer IP</span><span class="sxs-lookup"><span data-stu-id="158aa-136">*On-premises BGP peer IP</span></span>     | <span data-ttu-id="158aa-137">10.52.255.254</span><span class="sxs-lookup"><span data-stu-id="158aa-137">10.52.255.254</span></span>                |

* <span data-ttu-id="158aa-138">(*) Yalnızca BGP için isteğe bağlı parametreleri</span><span class="sxs-lookup"><span data-stu-id="158aa-138">(*) Optional parameters for BGP only</span></span>

### <a name="sample-powershell-script"></a><span data-ttu-id="158aa-139">Örnek PowerShell komut dosyası</span><span class="sxs-lookup"><span data-stu-id="158aa-139">Sample PowerShell script</span></span>
<span data-ttu-id="158aa-140">[PowerShell kullanarak S2S VPN bağlantısı oluşturma](vpn-gateway-create-site-to-site-rm-powershell.md) hello ayrıntılı yönergeler.</span><span class="sxs-lookup"><span data-stu-id="158aa-140">[Create a S2S VPN connection using PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) has hello detailed instructions.</span></span> <span data-ttu-id="158aa-141">Bu bölüm, başlattığınız bir örnek komut dosyası tooget sağlar.</span><span class="sxs-lookup"><span data-stu-id="158aa-141">This section provides a sample script tooget you started.</span></span>

```powershell
# Declare your variables

$Sub1          = "Replace_With_Your_Subcription_Name"
$RG1           = "TestRG1"
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
$VNet1ASN      = 65010
$DNS1          = "8.8.8.8"
$GWName1       = "VNet1GW"
$GWIPName1     = "VNet1GWIP"
$GWIPconfName1 = "gwipconf1"
$Connection15  = "VNet1toSite5"
$LNGName5      = "Site5"
$LNGPrefix50   = "10.52.255.254/32"
$LNGPrefix51   = "10.51.0.0/16"
$LNGPrefix52   = "10.52.0.0/16"
$LNGIP5        = "Your_VPN_Device_IP"
$LNGASN5       = 65050
$BGPPeerIP5    = "10.52.255.254"

# Connect tooyour subscription and create a new resource group

Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1

# Create virtual network

$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1

# Create VPN gateway

$gwpip1    = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$vnet1     = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1

New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN

# Create local network gateway

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix51,$LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5

# Create hello S2S VPN connection

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False
```

### <span data-ttu-id="158aa-142"><a name ="policybased"></a>[İsteğe bağlı] "UsePolicyBasedTrafficSelectors" özel IPSec/IKE ilkesiyle kullanın</span><span class="sxs-lookup"><span data-stu-id="158aa-142"><a name ="policybased"></a> [Optional] Use custom IPsec/IKE policy with "UsePolicyBasedTrafficSelectors"</span></span>
<span data-ttu-id="158aa-143">VPN cihazlarınızı "any herhangi" trafiğini Seçici (rota tabanlı/VTI-tabanlı yapılandırması) desteklemez varsa toocreate özel bir IPSec/IKE ilke ihtiyacınız ve "UsePolicyBasedTrafficSelectors" seçeneği açıklandığı gibi yapılandırın [bu makalede ](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="158aa-143">If your VPN devices do not support "any-to-any" traffic selectors (route-based/VTI-based configuration), you will need toocreate a custom IPsec/IKE policy and configure "UsePolicyBasedTrafficSelectors" option as described in [this article](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="158aa-144">Toocreate sipariş tooenable "UsePolicyBasedTrafficSelectors" seçeneği hello bağlantı IPSec/IKE ilkesinde gerekir.</span><span class="sxs-lookup"><span data-stu-id="158aa-144">You need toocreate an IPsec/IKE policy in order tooenable "UsePolicyBasedTrafficSelectors" option on hello connection.</span></span>

<span data-ttu-id="158aa-145">Merhaba örnek komut dosyası aşağıdaki hello ile IPSec/IKE ilkesi oluşturur algoritmaları ve parametreleri aşağıdaki:</span><span class="sxs-lookup"><span data-stu-id="158aa-145">hello sample script below creates an IPsec/IKE policy with hello following algorithms and parameters:</span></span>
* <span data-ttu-id="158aa-146">Ikev2: AES256, SHA384 DHGroup24</span><span class="sxs-lookup"><span data-stu-id="158aa-146">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="158aa-147">IPSec: AES256, SHA1, PFS24, SA ömrü 7200 saniye & 20480000KB (20GB)</span><span class="sxs-lookup"><span data-stu-id="158aa-147">IPsec: AES256, SHA1, PFS24, SA Lifetime 7200 seconds & 20480000KB (20GB)</span></span>

<span data-ttu-id="158aa-148">Merhaba ilke uygulanır ve "UesPolicyBasedTrafficSelectors" Merhaba bağlantıda sağlar.</span><span class="sxs-lookup"><span data-stu-id="158aa-148">It then applies hello policy and enables "UesPolicyBasedTrafficSelectors" on hello connection.</span></span>

```powershell
$ipsecpolicy5 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA1 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 20480000

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False -IpsecPolicies $ipsecpolicy5 -UsePolicyBasedTrafficSelectors $True
```

### <span data-ttu-id="158aa-149"><a name ="bgp"></a>[İsteğe bağlı] BGP S2S VPN bağlantısı kullan</span><span class="sxs-lookup"><span data-stu-id="158aa-149"><a name ="bgp"></a>[Optional] Use BGP on S2S VPN connection</span></span>
<span data-ttu-id="158aa-150">BGP hello bağlantıda isteğe bağlı olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="158aa-150">You can optionally use BGP on hello connection.</span></span> <span data-ttu-id="158aa-151">Bkz: [VPN ağ geçidi için BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="158aa-151">See [BGP for VPN gateway](vpn-gateway-bgp-resource-manager-ps.md).</span></span> <span data-ttu-id="158aa-152">İki farklar vardır:</span><span class="sxs-lookup"><span data-stu-id="158aa-152">There are two differences:</span></span>

<span data-ttu-id="158aa-153">Merhaba şirket içi adres öneklerini, tek bir ana bilgisayara adresi, hello şirket içi BGP eş IP adresi olabilir:</span><span class="sxs-lookup"><span data-stu-id="158aa-153">hello on-premises address prefixes can be a single host address, hello on-premises BGP peer IP address:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

<span data-ttu-id="158aa-154">Ayarlamanız gerekir "-EnableBGP" $ çok True hello bağlantı oluştururken:</span><span class="sxs-lookup"><span data-stu-id="158aa-154">You must set "-EnableBGP" too$True when creating hello connection:</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

## <a name="next-steps"></a><span data-ttu-id="158aa-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="158aa-155">Next steps</span></span>
<span data-ttu-id="158aa-156">Bkz: [yapılandırma etkin-etkin VPN ağ geçitleri için şirket içi ve VNet-VNet bağlantıları](vpn-gateway-activeactive-rm-powershell.md) adımları tooconfigure etkin-etkin şirket içi ve VNet-VNet bağlantıları için.</span><span class="sxs-lookup"><span data-stu-id="158aa-156">See [Configuring Active-Active VPN Gateways for Cross-Premises and VNet-to-VNet Connections](vpn-gateway-activeactive-rm-powershell.md) for steps tooconfigure active-active cross-premises and VNet-to-VNet connections.</span></span>

