---
title: "Azure VPN ağ geçitleri için bağlanmak için 3 taraf VPN cihazını yapılandırma hakkında | Microsoft Docs"
description: "Bu makale Azure VPN ağ geçitleri için bağlamak için 3 taraf VPN cihaz yapılandırmalarını genel bir bakış sağlar."
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
ms.openlocfilehash: 72dab85bb882b05d72cef26bef70437695b70416
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="overview-of-3rd-party-vpn-device-configurations"></a><span data-ttu-id="39181-103">3 taraf VPN cihaz yapılandırmalarını genel bakış</span><span class="sxs-lookup"><span data-stu-id="39181-103">Overview of 3rd party VPN device configurations</span></span>
<span data-ttu-id="39181-104">Bu makale Azure VPN ağ geçitleri için bağlamak için şirket içi VPN cihaz yapılandırmalarını genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="39181-104">This article provides an overview of on-premises VPN device configurations for connecting to Azure VPN gateways.</span></span> <span data-ttu-id="39181-105">Örnek Azure sanal ağ ve VPN ağ geçidi, şirket içi VPN aygıtları aynı parametrelere sahip bağlanmak için kullanılacak.</span><span class="sxs-lookup"><span data-stu-id="39181-105">The sample Azure virtual network and VPN gateway setup will be used to connect to different on-premises VPN devices with the same parameters.</span></span>

## <a name="device-requirements"></a><span data-ttu-id="39181-106">Cihaz gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="39181-106">Device requirements</span></span>
<span data-ttu-id="39181-107">Azure VPN ağ geçidi S2S VPN tünelleri için standart IPSec/IKE protokolü paketlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="39181-107">Azure VPN gateways use standard IPsec/IKE protocol suites for S2S VPN tunnels.</span></span> <span data-ttu-id="39181-108">Başvurmak [VPN cihazları hakkında](vpn-gateway-about-vpn-devices.md) Azure VPN ağ geçitleri için varsayılan şifreleme algoritmaları ve ayrıntılı IPSec/IKE protokol parametreleri için.</span><span class="sxs-lookup"><span data-stu-id="39181-108">Refer to [About VPN devices](vpn-gateway-about-vpn-devices.md) for the detailed IPsec/IKE protocol parameters and default cryptographic algorithms for Azure VPN gateways.</span></span> <span data-ttu-id="39181-109">Bölümünde açıklandığı gibi isteğe bağlı olarak şifreleme algoritmaları ve anahtar gücü belirli bir bağlantı için tam birleşimini belirtebilirsiniz [şifreleme gereksinimleri hakkında](vpn-gateway-about-compliance-crypto.md).</span><span class="sxs-lookup"><span data-stu-id="39181-109">You can optionally specify the exact combination of cryptographic algorithms and key strengths for a specific connection as described in [About cryptographic requirements](vpn-gateway-about-compliance-crypto.md).</span></span>

## <span data-ttu-id="39181-110"><a name ="singletunnel"></a>Tek VPN tüneli</span><span class="sxs-lookup"><span data-stu-id="39181-110"><a name ="singletunnel"></a>Single VPN tunnel</span></span>
<span data-ttu-id="39181-111">Bir Azure VPN ağ geçidi ve şirket içi VPN cihazınız arasındaki tek S2S VPN tüneli, birinci topoloji oluşur.</span><span class="sxs-lookup"><span data-stu-id="39181-111">The first topology consists of a single S2S VPN tunnel between an Azure VPN gateway and your on-premises VPN device.</span></span> <span data-ttu-id="39181-112">İsteğe bağlı olarak VPN tüneli üzerinden BGP yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="39181-112">You can optionally configure BGP across the VPN tunnel.</span></span>

![tek tünel](./media/vpn-gateway-3rdparty-device-config-overview/singletunnel.png)

<span data-ttu-id="39181-114">Başvurmak [siteden siteye bağlantı yapılandırma](vpn-gateway-howto-site-to-site-resource-manager-portal.md) ayrıntılı, adım adım yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="39181-114">Refer to [Configure site-to-site connection](vpn-gateway-howto-site-to-site-resource-manager-portal.md) for detailed, step-by-step guidance.</span></span> <span data-ttu-id="39181-115">Aşağıdaki bölümlerde parametreleri listelenmekte ve başlamanıza yardımcı olmak için bir PowerShell komut dosyası sağlar.</span><span class="sxs-lookup"><span data-stu-id="39181-115">The following sections list the parameters and provide a sample PowerShell script to help you get started.</span></span>

### <a name="network-and-vpn-gateway-information"></a><span data-ttu-id="39181-116">Ağ ve VPN ağ geçidi bilgileri</span><span class="sxs-lookup"><span data-stu-id="39181-116">Network and VPN gateway information</span></span>
<span data-ttu-id="39181-117">Bu bölümde yukarıdaki örnekler için parametreleri listeler.</span><span class="sxs-lookup"><span data-stu-id="39181-117">This section list the parameters for the examples above.</span></span>

| <span data-ttu-id="39181-118">**Parametre**</span><span class="sxs-lookup"><span data-stu-id="39181-118">**Parameter**</span></span>                | <span data-ttu-id="39181-119">**Değer**</span><span class="sxs-lookup"><span data-stu-id="39181-119">**Value**</span></span>                    |
| ---                          | ---                          |
| <span data-ttu-id="39181-120">VNet adres önekleri</span><span class="sxs-lookup"><span data-stu-id="39181-120">VNet address prefixes</span></span>        | <span data-ttu-id="39181-121">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="39181-121">10.11.0.0/16</span></span><br><span data-ttu-id="39181-122">10.12.0.0/16</span><span class="sxs-lookup"><span data-stu-id="39181-122">10.12.0.0/16</span></span> |
| <span data-ttu-id="39181-123">Azure VPN ağ geçidi IP</span><span class="sxs-lookup"><span data-stu-id="39181-123">Azure VPN gateway IP</span></span>         | <span data-ttu-id="39181-124">Azure VPN ağ geçidi IP</span><span class="sxs-lookup"><span data-stu-id="39181-124">Azure VPN Gateway IP</span></span>         |
| <span data-ttu-id="39181-125">Şirket içi adres önekleri</span><span class="sxs-lookup"><span data-stu-id="39181-125">On-premises address prefixes</span></span> | <span data-ttu-id="39181-126">10.51.0.0/16</span><span class="sxs-lookup"><span data-stu-id="39181-126">10.51.0.0/16</span></span><br><span data-ttu-id="39181-127">10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="39181-127">10.52.0.0/16</span></span> |
| <span data-ttu-id="39181-128">Şirket içi VPN cihazının IP</span><span class="sxs-lookup"><span data-stu-id="39181-128">On-premises VPN device IP</span></span>    | <span data-ttu-id="39181-129">Şirket içi VPN cihazının IP</span><span class="sxs-lookup"><span data-stu-id="39181-129">On-premises VPN device IP</span></span>    |
| <span data-ttu-id="39181-130">* VNet BGP ASN</span><span class="sxs-lookup"><span data-stu-id="39181-130">*VNet BGP ASN</span></span>                | <span data-ttu-id="39181-131">65010</span><span class="sxs-lookup"><span data-stu-id="39181-131">65010</span></span>                        |
| <span data-ttu-id="39181-132">* Azure BGP eşdeğer IP</span><span class="sxs-lookup"><span data-stu-id="39181-132">*Azure BGP peer IP</span></span>           | <span data-ttu-id="39181-133">10.12.255.30</span><span class="sxs-lookup"><span data-stu-id="39181-133">10.12.255.30</span></span>                 |
| <span data-ttu-id="39181-134">* Şirket içi BGP ASN</span><span class="sxs-lookup"><span data-stu-id="39181-134">*On-premises BGP ASN</span></span>         | <span data-ttu-id="39181-135">65050</span><span class="sxs-lookup"><span data-stu-id="39181-135">65050</span></span>                        |
| <span data-ttu-id="39181-136">* Şirket içi BGP eşdeğer IP</span><span class="sxs-lookup"><span data-stu-id="39181-136">*On-premises BGP peer IP</span></span>     | <span data-ttu-id="39181-137">10.52.255.254</span><span class="sxs-lookup"><span data-stu-id="39181-137">10.52.255.254</span></span>                |

* <span data-ttu-id="39181-138">(*) Yalnızca BGP için isteğe bağlı parametreleri</span><span class="sxs-lookup"><span data-stu-id="39181-138">(*) Optional parameters for BGP only</span></span>

### <a name="sample-powershell-script"></a><span data-ttu-id="39181-139">Örnek PowerShell komut dosyası</span><span class="sxs-lookup"><span data-stu-id="39181-139">Sample PowerShell script</span></span>
<span data-ttu-id="39181-140">[PowerShell kullanarak S2S VPN bağlantısı oluşturma](vpn-gateway-create-site-to-site-rm-powershell.md) ayrıntılı yönergeler içerir.</span><span class="sxs-lookup"><span data-stu-id="39181-140">[Create a S2S VPN connection using PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md) has the detailed instructions.</span></span> <span data-ttu-id="39181-141">Bu bölüm başlamanıza yardımcı olmak için bir örnek komut dosyası sağlar.</span><span class="sxs-lookup"><span data-stu-id="39181-141">This section provides a sample script to get you started.</span></span>

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

# Connect to your subscription and create a new resource group

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

# Create the S2S VPN connection

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False
```

### <span data-ttu-id="39181-142"><a name ="policybased"></a>[İsteğe bağlı] "UsePolicyBasedTrafficSelectors" özel IPSec/IKE ilkesiyle kullanın</span><span class="sxs-lookup"><span data-stu-id="39181-142"><a name ="policybased"></a> [Optional] Use custom IPsec/IKE policy with "UsePolicyBasedTrafficSelectors"</span></span>
<span data-ttu-id="39181-143">VPN cihazlarınızı "any herhangi" trafiğini Seçici (rota tabanlı/VTI-tabanlı yapılandırması) desteklemez, özel bir IPSec/IKE İlkesi oluşturup "UsePolicyBasedTrafficSelectors" seçeneği açıklandığı şekilde yapılandırmak gerekir [bu makalede](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="39181-143">If your VPN devices do not support "any-to-any" traffic selectors (route-based/VTI-based configuration), you will need to create a custom IPsec/IKE policy and configure "UsePolicyBasedTrafficSelectors" option as described in [this article](vpn-gateway-connect-multiple-policybased-rm-ps.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="39181-144">Bağlantı "UsePolicyBasedTrafficSelectors" seçeneğini etkinleştirmek için bir IPSec/IKE İlkesi oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="39181-144">You need to create an IPsec/IKE policy in order to enable "UsePolicyBasedTrafficSelectors" option on the connection.</span></span>

<span data-ttu-id="39181-145">Aşağıdaki örnek komut dosyası için aşağıdaki algoritmaları ve parametrelerine sahip bir IPSec/IKE ilkesi oluşturur:</span><span class="sxs-lookup"><span data-stu-id="39181-145">The sample script below creates an IPsec/IKE policy with the following algorithms and parameters:</span></span>
* <span data-ttu-id="39181-146">Ikev2: AES256, SHA384 DHGroup24</span><span class="sxs-lookup"><span data-stu-id="39181-146">IKEv2: AES256, SHA384, DHGroup24</span></span>
* <span data-ttu-id="39181-147">IPSec: AES256, SHA1, PFS24, SA ömrü 7200 saniye & 20480000KB (20GB)</span><span class="sxs-lookup"><span data-stu-id="39181-147">IPsec: AES256, SHA1, PFS24, SA Lifetime 7200 seconds & 20480000KB (20GB)</span></span>

<span data-ttu-id="39181-148">Ardından, ilke uygulanır ve "UesPolicyBasedTrafficSelectors" bağlantısı sağlar.</span><span class="sxs-lookup"><span data-stu-id="39181-148">It then applies the policy and enables "UesPolicyBasedTrafficSelectors" on the connection.</span></span>

```powershell
$ipsecpolicy5 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA1 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 20480000

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False -IpsecPolicies $ipsecpolicy5 -UsePolicyBasedTrafficSelectors $True
```

### <span data-ttu-id="39181-149"><a name ="bgp"></a>[İsteğe bağlı] BGP S2S VPN bağlantısı kullan</span><span class="sxs-lookup"><span data-stu-id="39181-149"><a name ="bgp"></a>[Optional] Use BGP on S2S VPN connection</span></span>
<span data-ttu-id="39181-150">BGP bağlantısı isteğe bağlı olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="39181-150">You can optionally use BGP on the connection.</span></span> <span data-ttu-id="39181-151">Bkz: [VPN ağ geçidi için BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="39181-151">See [BGP for VPN gateway](vpn-gateway-bgp-resource-manager-ps.md).</span></span> <span data-ttu-id="39181-152">İki farklar vardır:</span><span class="sxs-lookup"><span data-stu-id="39181-152">There are two differences:</span></span>

<span data-ttu-id="39181-153">Şirket içi adres öneklerini şirket içi BGP eş IP adresini bir tek ana bilgisayar adresi olabilir:</span><span class="sxs-lookup"><span data-stu-id="39181-153">The on-premises address prefixes can be a single host address, the on-premises BGP peer IP address:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

<span data-ttu-id="39181-154">Ayarlamanız gerekir "-EnableBGP" bağlantı oluştururken $True için:</span><span class="sxs-lookup"><span data-stu-id="39181-154">You must set "-EnableBGP" to $True when creating the connection:</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

## <a name="next-steps"></a><span data-ttu-id="39181-155">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="39181-155">Next steps</span></span>
<span data-ttu-id="39181-156">Etkin-etkin şirket içi ve dışı ile Sanal Ağdan Sanal Ağa bağlantıları yapılandırma adımları için bkz. [Şirket İçi ve Dışı ile Sanal Ağdan Sanal Ağa Bağlantılar için Etkin-Etkin VPN Gateways Yapılandırma](vpn-gateway-activeactive-rm-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="39181-156">See [Configuring Active-Active VPN Gateways for Cross-Premises and VNet-to-VNet Connections](vpn-gateway-activeactive-rm-powershell.md) for steps to configure active-active cross-premises and VNet-to-VNet connections.</span></span>

