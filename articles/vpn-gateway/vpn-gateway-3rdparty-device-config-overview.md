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
# <a name="overview-of-3rd-party-vpn-device-configurations"></a>3 taraf VPN cihaz yapılandırmalarını genel bakış
Bu makale Azure VPN ağ geçitleri için bağlamak için şirket içi VPN cihaz yapılandırmalarını genel bir bakış sağlar. Örnek Azure sanal ağ ve VPN ağ geçidi, şirket içi VPN aygıtları aynı parametrelere sahip bağlanmak için kullanılacak.

## <a name="device-requirements"></a>Cihaz gereksinimleri
Azure VPN ağ geçidi S2S VPN tünelleri için standart IPSec/IKE protokolü paketlerini kullanın. Başvurmak [VPN cihazları hakkında](vpn-gateway-about-vpn-devices.md) Azure VPN ağ geçitleri için varsayılan şifreleme algoritmaları ve ayrıntılı IPSec/IKE protokol parametreleri için. Bölümünde açıklandığı gibi isteğe bağlı olarak şifreleme algoritmaları ve anahtar gücü belirli bir bağlantı için tam birleşimini belirtebilirsiniz [şifreleme gereksinimleri hakkında](vpn-gateway-about-compliance-crypto.md).

## <a name ="singletunnel"></a>Tek VPN tüneli
Bir Azure VPN ağ geçidi ve şirket içi VPN cihazınız arasındaki tek S2S VPN tüneli, birinci topoloji oluşur. İsteğe bağlı olarak VPN tüneli üzerinden BGP yapılandırabilirsiniz.

![tek tünel](./media/vpn-gateway-3rdparty-device-config-overview/singletunnel.png)

Başvurmak [siteden siteye bağlantı yapılandırma](vpn-gateway-howto-site-to-site-resource-manager-portal.md) ayrıntılı, adım adım yönergeler için. Aşağıdaki bölümlerde parametreleri listelenmekte ve başlamanıza yardımcı olmak için bir PowerShell komut dosyası sağlar.

### <a name="network-and-vpn-gateway-information"></a>Ağ ve VPN ağ geçidi bilgileri
Bu bölümde yukarıdaki örnekler için parametreleri listeler.

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
[PowerShell kullanarak S2S VPN bağlantısı oluşturma](vpn-gateway-create-site-to-site-rm-powershell.md) ayrıntılı yönergeler içerir. Bu bölüm başlamanıza yardımcı olmak için bir örnek komut dosyası sağlar.

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

### <a name ="policybased"></a>[İsteğe bağlı] "UsePolicyBasedTrafficSelectors" özel IPSec/IKE ilkesiyle kullanın
VPN cihazlarınızı "any herhangi" trafiğini Seçici (rota tabanlı/VTI-tabanlı yapılandırması) desteklemez, özel bir IPSec/IKE İlkesi oluşturup "UsePolicyBasedTrafficSelectors" seçeneği açıklandığı şekilde yapılandırmak gerekir [bu makalede](vpn-gateway-connect-multiple-policybased-rm-ps.md).

> [!IMPORTANT]
> Bağlantı "UsePolicyBasedTrafficSelectors" seçeneğini etkinleştirmek için bir IPSec/IKE İlkesi oluşturmanız gerekir.

Aşağıdaki örnek komut dosyası için aşağıdaki algoritmaları ve parametrelerine sahip bir IPSec/IKE ilkesi oluşturur:
* Ikev2: AES256, SHA384 DHGroup24
* IPSec: AES256, SHA1, PFS24, SA ömrü 7200 saniye & 20480000KB (20GB)

Ardından, ilke uygulanır ve "UesPolicyBasedTrafficSelectors" bağlantısı sağlar.

```powershell
$ipsecpolicy5 = New-AzureRmIpsecPolicy -IkeEncryption AES256 -IkeIntegrity SHA384 -DhGroup DHGroup24 -IpsecEncryption AES256 -IpsecIntegrity SHA1 -PfsGroup PFS24 -SALifeTimeSeconds 7200 -SADataSizeKilobytes 20480000

$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $False -IpsecPolicies $ipsecpolicy5 -UsePolicyBasedTrafficSelectors $True
```

### <a name ="bgp"></a>[İsteğe bağlı] BGP S2S VPN bağlantısı kullan
BGP bağlantısı isteğe bağlı olarak kullanabilirsiniz. Bkz: [VPN ağ geçidi için BGP](vpn-gateway-bgp-resource-manager-ps.md). İki farklar vardır:

Şirket içi adres öneklerini şirket içi BGP eş IP adresini bir tek ana bilgisayar adresi olabilir:

```powershell
New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG1 -Location $Location1 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

Ayarlamanız gerekir "-EnableBGP" bağlantı oluştururken $True için:

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

## <a name="next-steps"></a>Sonraki adımlar
Etkin-etkin şirket içi ve dışı ile Sanal Ağdan Sanal Ağa bağlantıları yapılandırma adımları için bkz. [Şirket İçi ve Dışı ile Sanal Ağdan Sanal Ağa Bağlantılar için Etkin-Etkin VPN Gateways Yapılandırma](vpn-gateway-activeactive-rm-powershell.md).

