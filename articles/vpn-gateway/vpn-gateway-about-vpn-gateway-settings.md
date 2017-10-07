---
title: "Şirket içi Azure bağlantıları için ağ geçidi ayarlarını aaaVPN | Microsoft Docs"
description: "Azure sanal ağ geçitleri için VPN ağ geçidi ayarları hakkında bilgi edinin."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: ae665bc5-0089-45d0-a0d5-bc0ab4e79899
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/26/2017
ms.author: cherylmc
ms.openlocfilehash: 01229d99fa37e30e00aa00f939f488d631b5593c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="about-vpn-gateway-configuration-settings"></a>VPN ağ geçidi yapılandırma ayarları hakkında

Bir VPN ağ geçidi, sanal ağınızı ve şirket içi konumunuz arasındaki şifrelenmiş trafik ortak bir bağlantı üzerinden gönderir sanal ağ geçidi türüdür. Hello Azure omurga üzerinden sanal ağlar arasında bir VPN ağ geçidi toosend trafiği de kullanabilirsiniz.

Bir VPN gateway bağlantısı her biri yapılandırılabilir ayarları içeren hello yapılandırmasına göre birden fazla kaynak kullanır. Bu makalede Hello bölümlerde hello kaynakları ve Resource Manager dağıtım modelinde oluşturulmuş bir sanal ağ için tooa VPN ağ geçidi ile ilgili ayarları açıklanmaktadır. Merhaba her bağlantı çözümünüz için açıklamaları ve topoloji diyagramları bulabilirsiniz [VPN Gateway hakkında](vpn-gateway-about-vpngateways.md) makalesi.

## <a name="gwtype"></a>Ağ geçidi türleri

Her sanal ağ, yalnızca bir sanal ağ geçidi her tür olabilir. Bir sanal ağ geçidi oluştururken, hello ağ geçidi türü yapılandırmanız için doğru olduğundan emin olmanız gerekir.

-GatewayType için Hello kullanılabilir değerler şunlardır:

* VPN
* ExpressRoute

Bir VPN ağ geçidi hello gerektirir `-GatewayType` *Vpn*.

Örnek:

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased
```

## <a name="gwsku"></a>Ağ Geçidi SKU'ları

[!INCLUDE [vpn-gateway-gwsku-include](../../includes/vpn-gateway-gwsku-include.md)]

### <a name="configure-hello-gateway-sku"></a>Merhaba ağ geçidi SKU'su yapılandırın

#### <a name="azure-portal"></a>Azure portalına

Hello Azure portal toocreate bir Resource Manager sanal ağ geçidi kullanırsanız, hello açılan listeyi kullanarak hello ağ geçidi SKU'su seçebilirsiniz. ile sunulan başlangıç seçenekleri toohello ağ geçidi türü ve seçtiğiniz VPN türü karşılık gelir.

#### <a name="powershell"></a>PowerShell

Merhaba aşağıdaki PowerShell örnek belirtir hello `-GatewaySku` VpnGw1 olarak.

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewaySku VpnGw1 `
-GatewayType Vpn -VpnType RouteBased
```

#### <a name="resize"></a>Değişiklik (boyutlandırma) bir ağ geçidi SKU'su

Ağ geçidi SKU'su tooa tooupgrade istiyorsanız, daha güçlü SKU hello kullanabileceğiniz `Resize-AzureRmVirtualNetworkGateway` PowerShell cmdlet'i. Ayrıca bu cmdlet kullanılarak hello ağ geçidi SKU boyutunu düşürmek.

Aşağıdaki PowerShell örneğine hello olan ağ geçidi SKU'su tooVpnGw2 yeniden boyutlandırılabilir gösterir.

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
Resize-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -GatewaySku VpnGw2
```

## <a name="connectiontype"></a>Bağlantı türleri

Merhaba Resource Manager dağıtım modelinde, her yapılandırma belirli sanal ağ geçidi bağlantı türü gerektirir. Merhaba kullanılabilir Resource Manager PowerShell değerleri `-ConnectionType` şunlardır:

* IPsec
* Vnet2Vnet
* ExpressRoute
* VPNClient

Aşağıdaki PowerShell örneğine hello hello bağlantı türü gerektiren bir S2S bağlantı oluşturuyoruz *IPSec*.

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name localtovon -ResourceGroupName testrg `
-Location 'West US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
-ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
```

## <a name="vpntype"></a>VPN türleri

Merhaba sanal ağ geçidi için VPN ağ geçidi yapılandırması oluşturduğunuzda, bir VPN türü belirtmeniz gerekir. Merhaba seçtiğiniz VPN türü toocreate istediğiniz hello bağlantı topolojiye bağlıdır. Örneğin, P2S bağlantısı RouteBased VPN türü gerektirir. Bir VPN türü ayrıca kullanmakta olduğunuz hello donanımına bağlı olabilir. S2S yapılandırmaları bir VPN cihazı gerektirir. Bazı VPN cihazlarının yalnızca belirli bir VPN türü destekler.

Merhaba seçtiğiniz VPN türü toocreate istediğiniz hello çözüm için tüm hello bağlantı gereksinimleri karşılaması gerekir. Örneğin, toocreate istiyorsanız bir S2S VPN gateway bağlantısı ve P2S VPN ağ geçidi bağlantısı için Merhaba aynı sanal ağ, VPN türü kullanırsınız *RouteBased* çünkü P2S RouteBased VPN türü gerektirir. Ayrıca, VPN cihazınızın RouteBased VPN bağlantısı desteklenen tooverify gerekir. 

Bir sanal ağ geçidi oluşturulduktan sonra hello VPN türü değiştirilemez. Sanal ağ geçidi hello ve yeni bir tane oluşturun toodelete sahip. İki VPN türü vardır:

[!INCLUDE [vpn-gateway-vpntype](../../includes/vpn-gateway-vpntype-include.md)]

Merhaba aşağıdaki PowerShell örnek belirtir hello `-VpnType` olarak *RouteBased*. Bir ağ geçidi oluştururken, o hello emin olmalısınız - VpnType öğesinin yapılandırmanız için doğru.

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig `
-GatewayType Vpn -VpnType RouteBased
```

## <a name="requirements"></a>Ağ geçidi gereksinimleri

[!INCLUDE [vpn-gateway-table-requirements](../../includes/vpn-gateway-table-requirements-include.md)]

## <a name="gwsub"></a>Ağ geçidi alt ağı

Bir VPN ağ geçidi oluşturmadan önce bir ağ geçidi alt ağı oluşturmanız gerekir. Hello ağ geçidi alt ağı bu hello sanal ağ geçidi VMs hello IP adreslerini içeren ve Hizmetleri kullanın. Sanal ağ geçidinizi oluşturduğunuzda, ağ geçidi VMs dağıtılan toohello ağ geçidi alt ağı olan ve gerekli hello VPN ağ geçidi ayarları ile yapılandırılmış. Hiçbir zaman başka herhangi bir şey (örneğin, ek VM'ler) toohello ağ geçidi alt ağı dağıtmanız gerekir. Merhaba ağ geçidi alt ağı 'GatewaySubnet' toowork düzgün olarak adlandırılmalıdır. Merhaba ağ geçidi alt ağına 'GatewaySubnet' sağlar adlandırma Azure bilmeniz bu hello alt toodeploy hello sanal ağ ağ geçidi sanal makineleri ve Hizmetleri için.

Merhaba ağ geçidi alt ağı oluşturduğunuzda, alt ağ hello IP adreslerinin sayısı hello içerdiğini belirtin. hello ağ geçidi alt ağı Hello IP adresleri ayrılmış toohello ağ geçidi sanal makineleri ve ağ geçidi hizmetleri verilebilir. Bazı yapılandırmalar diğerlerinden daha fazla IP adresi gerektirir. Merhaba yönergeler toocreate istediğiniz ve toocreate istediğiniz bu hello ağ geçidi alt ağı bu gereksinimleri karşıladığını doğrulayın hello yapılandırması için bakın. Ayrıca, ağ geçidi alt ağı yeterli IP adreslerini tooaccommodate olası gelecekteki ek yapılandırmalar içerdiğinden emin toomake isteyebilirsiniz. Bir ağ geçidi alt ağı/29 kadar küçük oluşturabilirsiniz, ancak 28 ya da daha büyük bir ağ geçidi alt ağı oluşturmanızı öneririz (/ 28, / 27, /26 vs.). Merhaba gelecekteki işlevselliğini eklerseniz bu şekilde, olmaz tootear, ağ geçidine sahip sonra silin ve hello ağ geçidi alt ağı tooallow daha fazla IP adresi oluşturun.

Merhaba aşağıdaki Resource Manager PowerShell örnek GatewaySubnet adlı bir ağ geçidi alt ağı gösterir. Şu anda mevcut çoğu yapılandırma için yeterli IP adresine izin veren bir/27 hello CIDR gösteriminde belirtir görebilirsiniz.

```powershell
Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.0.3.0/27
```

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

## <a name="lng"></a>Yerel ağ geçitleri

Bir VPN ağ geçidi yapılandırması oluştururken hello yerel ağ geçidi genellikle şirket içi konumunuzu temsil eder. Merhaba Klasik dağıtım modelinde hello yerel ağ geçidi başvurulan tooas bir yerel Site oluştu. 

Merhaba yerel ağ geçidi bir ad verin, hello şirket içi VPN cihazının genel IP adresi hello ve hello şirket içi konumunda yer hello adres öneklerini belirtirsiniz. Azure ağ trafiği için hello hedef adres öneklerine bakar, yerel ağ geçidiniz için belirttiğiniz hello yapılandırma bakar ve paketleri buna uygun şekilde yönlendirir. Ayrıca, VPN ağ geçidi bağlantısı kullanma VNet-VNet yapılandırmaları için yerel ağ geçitleri de belirtin.

Aşağıdaki PowerShell örneğine hello yeni bir yerel ağ geçidi oluşturur:

```powershell
New-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg `
-Location 'West US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.5.51.0/24'
```

Bazen toomodify hello yerel ağ geçidi ayarlarını gerekir. Örneğin, eklediğinizde veya hello adres aralığını değiştirmek veya hello VPN cihazının IP adresi hello değişip değişmediğini. Klasik bir VNet için hello yerel ağlar sayfasında hello Klasik portalda bu ayarları değiştirebilirsiniz. Kaynak Yöneticisi için bkz: [PowerShell kullanarak yerel ağ geçidi ayarlarını değiştirmek](vpn-gateway-modify-local-network-gateway.md).

## <a name="resources"></a>REST API ve PowerShell cmdlet'leri

Ek teknik kaynaklar ve REST API'leri, PowerShell cmdlet'lerini veya Azure CLI için VPN ağ geçidi yapılandırmaları kullanırken belirli sözdizimi gereksinimleri için sayfalar aşağıdaki hello bakın:

| **Klasik** | **Resource Manager** |
| --- | --- |
| [PowerShell](/powershell/module/azure#networking) |[PowerShell](/powershell/module/azurerm.network#vpn) |
| [REST API](https://msdn.microsoft.com/library/jj154113) |[REST API](/rest/api/network/virtualnetworkgateways) |
| Desteklenmiyor | [Azure CLI](/cli/azure/network/vnet-gateway)|

## <a name="next-steps"></a>Sonraki adımlar

Bir bağlantı yapılandırmaları hakkında daha fazla bilgi için bkz: [VPN Gateway hakkında](vpn-gateway-about-vpngateways.md).