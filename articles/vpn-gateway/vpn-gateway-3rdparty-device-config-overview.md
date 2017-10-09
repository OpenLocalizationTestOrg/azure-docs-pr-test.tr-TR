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
# <a name="overview-of-3rd-party-vpn-device-configurations"></a>3 taraf VPN cihaz yapılandırmalarını genel bakış
Bu makalede, şirket içi VPN cihaz yapılandırmalarını tooAzure VPN ağ geçitlerini bağlama için genel bir bakış sağlar. Merhaba örnek Azure sanal ağı ve kullanılan tooconnect toodifferent şirket içi VPN aygıtları hello ile aynı parametre olması VPN ağ geçidi Kurulum olacaktır.

## <a name="device-requirements"></a>Cihaz gereksinimleri
Azure VPN ağ geçidi S2S VPN tünelleri için standart IPSec/IKE protokolü paketlerini kullanın. Çok başvuran[VPN cihazları hakkında](vpn-gateway-about-vpn-devices.md) Merhaba IPSec/IKE protokolü parametreleri ve Azure VPN ağ geçitleri için varsayılan şifreleme algoritmalarının ayrıntılı. Bölümünde açıklandığı gibi hello tam birleşimini şifreleme algoritmaları ve anahtar gücü belirli bir bağlantı için isteğe bağlı olarak belirtebilirsiniz [şifreleme gereksinimleri hakkında](vpn-gateway-about-compliance-crypto.md).

## <a name ="singletunnel"></a>Tek VPN tüneli
bir Azure VPN ağ geçidi ve şirket içi VPN cihazınız arasındaki tek S2S VPN tüneli Hello ilk topoloji oluşur. BGP hello VPN tüneli üzerinden isteğe bağlı olarak yapılandırabilirsiniz.

![tek tünel](./media/vpn-gateway-3rdparty-device-config-overview/singletunnel.png)

Çok başvuran[siteden siteye bağlantı yapılandırma](vpn-gateway-howto-site-to-site-resource-manager-portal.md) ayrıntılı, adım adım yönergeler için. Merhaba aşağıdaki bölümlerde hello parametreleri listelenmekte ve kullanmaya başlama örnek PowerShell komut dosyası toohelp sağlayın.

### <a name="network-and-vpn-gateway-information"></a>Ağ ve VPN ağ geçidi bilgileri
Bu bölümde yukarıdaki hello örnekler için hello parametreleri listeler.

| **Parametre**                | **Değer**                    |
| ---                          | ---                          |
| VNet adres önekleri        | 10.11.0.0/16<br>10.12.0.0/16 |
| Azure VPN ağ geçidi IP         | Azure VPN ağ geçidi IP         |
| Şirket içi adres önekleri | 10.51.0.0/16<br>10.52.0.0/16 |
| Şirket içi VPN cihazının IP    | Şirket içi VPN cihazının IP    |
| * VNet BGP ASN                | 65010                        |
| * Azure BGP eşdeğer IP           | 10.12.255.30                 |
| * Şirket içi BGP ASN         | 65050                        |
| * Şirket içi BGP eşdeğer IP     | 10.52.255.254                |

* (*) Yalnızca BGP için isteğe bağlı parametreleri

### <a name="sample-powershell-script"></a>Örnek PowerShell komut dosyası
[PowerShell kullanarak S2S VPN bağlantısı oluşturma](vpn-gateway-create-site-to-site-rm-powershell.md) hello ayrıntılı yönergeler. Bu bölüm, başlattığınız bir örnek komut dosyası tooget sağlar.

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

### <a name ="policybased"></a>[İsteğe bağlı] "UsePolicyBasedTrafficSelectors" özel IPSec/IKE ilkesiyle kullanın
VPN cihazlarınızı "any herhangi" trafiğini Seçici (rota tabanlı/VTI-tabanlı yapılandırması) desteklemez varsa toocreate özel bir IPSec/IKE ilke ihtiyacınız ve "UsePolicyBasedTrafficSelectors" seçeneği açıklandığı gibi yapılandırın [bu makalede ](vpn-gateway-connect-multiple-policybased-rm-ps.md).

> [!IMPORTANT]
> Toocreate sipariş tooenable "UsePolicyBasedTrafficSelectors" seçeneği hello bağlantı IPSec/IKE ilkesinde gerekir.

Merhaba örnek komut dosyası aşağıdaki hello ile IPSec/IKE ilkesi oluşturur algoritmaları ve parametreleri aşağıdaki:
* Ikev2: AES256, SHA384 DHGroup24
* IPSec: AES256, SHA1, PFS24, SA ömrü 7200 saniye & 20480000KB (20GB)

Merhaba ilke uygulanır ve "UesPolicyBasedTrafficSelectors" Merhaba bağlantıda sağlar.

```powershell
$ipsecpolicy5 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA1 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 20480000

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False -IpsecPolicies $ipsecpolicy5 -UsePolicyBasedTrafficSelectors $True
```

### <a name ="bgp"></a>[İsteğe bağlı] BGP S2S VPN bağlantısı kullan
BGP hello bağlantıda isteğe bağlı olarak kullanabilirsiniz. Bkz: [VPN ağ geçidi için BGP](vpn-gateway-bgp-resource-manager-ps.md). İki farklar vardır:

Merhaba şirket içi adres öneklerini, tek bir ana bilgisayara adresi, hello şirket içi BGP eş IP adresi olabilir:

```powershell
New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

Ayarlamanız gerekir "-EnableBGP" $ çok True hello bağlantı oluştururken:

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

## <a name="next-steps"></a>Sonraki adımlar
Bkz: [yapılandırma etkin-etkin VPN ağ geçitleri için şirket içi ve VNet-VNet bağlantıları](vpn-gateway-activeactive-rm-powershell.md) adımları tooconfigure etkin-etkin şirket içi ve VNet-VNet bağlantıları için.

