---
title: "Şirket içi ağ tooan Azure sanal ağı bağlanın: siteden siteye VPN: PowerShell | Microsoft Docs"
description: "Şirket içi bir IPSec bağlantısı üzerinden tooan Azure sanal ağı ağ adımları toocreate genel Internet hello. Bu adımlar PowerShell kullanarak Siteden Siteye şirket içi ve dışı karışık VPN Gateway bağlantısı oluşturmanıza yardımcı olur."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: fcc2fda5-4493-4c15-9436-84d35adbda8e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: cb8db1dab3a5488816a7f7e8e63908a4c02f55db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vnet-with-a-site-to-site-vpn-connection-using-powershell"></a>PowerShell kullanarak Siteden Siteye VPN bağlantısı ile sanal ağ oluşturma

Bu makale size nasıl toouse PowerShell toocreate bir Site siteye VPN ağ geçidi bağlantısını şirket içi ağ toohello VNet gösterir. Bu makaledeki adımları Hello toohello Resource Manager dağıtım modeli uygulayın. Liste aşağıdaki hello farklı bir seçeneği seçerek farklı dağıtım aracını veya dağıtım modelini kullanarak bu yapılandırma ayrıca oluşturabilirsiniz:

> [!div class="op_single_selector"]
> * [Azure portal](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [CLI](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Azure portal (klasik)](vpn-gateway-howto-site-to-site-classic-portal.md)
> * [Klasik portal (klasik)](vpn-gateway-site-to-site-create.md)
> 
>


Kullanılan tooconnect bir siteden siteye VPN gateway bağlantısı olan bir IPSec/IKE (Ikev1 veya Ikev2) VPN tüneli üzerinden tooan Azure sanal ağı şirket içi ağ. Bağlantı bu tür bir VPN cihazı bulunan dışarıya dönük bir genel IP adresi atanmış tooit olan şirket içi gerektirir. VPN ağ geçitleri hakkında daha fazla bilgi için bkz. [VPN ağ geçidi hakkında](vpn-gateway-about-vpngateways.md).

![Siteden Siteye şirket içi ve dışı karışık VPN Gateway bağlantısı diyagramı](./media/vpn-gateway-create-site-to-site-rm-powershell/site-to-site-diagram.png)

## <a name="before"></a>Başlamadan önce

Ölçüt yapılandırmanıza başlamadan önce aşağıdaki hello karşıladığınızı doğrulayın:

* Uyumlu bir VPN cihazı ve mümkün tooconfigure olan birisi olduğundan emin olun. Uyumlu VPN cihazları ve cihaz yapılandırması hakkında daha fazla bilgi için bkz.[VPN Cihazları Hakkında](vpn-gateway-about-vpn-devices.md).
* VPN cihazınız için dışarıya dönük genel bir IPv4 adresi olduğunu doğrulayın. Bu IP adresi bir NAT’nin arkasında olamaz.
* Bulunan hello IP adresi aralıklarıyla ilgili bilginiz yoksa, şirket içi ağ, bu ayrıntıları sizin için sağlayabilecek biriyle toocoordinate gerekir. Bu yapılandırma oluşturduğunuzda, Azure tooyour şirket içi konumu yönlendirilecek hello IP adresi aralığı önekleri belirtmeniz gerekir. Şirket içi ağınıza hello ağların hiçbiri diz tooconnect için istediğiniz hello sanal ağ alt ağı üzerinden olabilir.
* Merhaba hello Azure Resource Manager PowerShell cmdlet'lerinin en son sürümünü yükleyin. PowerShell cmdlet'leri sık sık güncelleştirilir ve genellikle, PowerShell cmdlet'leri tooget hello son özellik işlevinin tooupdate gerekir. PowerShell cmdlet'leri güncelleştirmezseniz belirtilen hello değerleri başarısız olabilir. Bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview) karşıdan yükleme ve PowerShell cmdlet'leri hakkında daha fazla bilgi.

### <a name="example"></a>Örnek değerler

Bu makaledeki örneklerde Hello değerleri aşağıdaki hello kullanın. Bu değerleri toocreate bir test ortamı kullanın veya toothem başvurun toobetter anlamak bu makaledeki hello örnekler.

```
#Example values

VnetName                = TestVNet1
ResourceGroup           = TestRG1
Location                = East US 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.1.0/28 
GatewaySubnet           = 10.11.0.0/27
LocalNetworkGatewayName = Site2
LNG Public IP           = <VPN device IP address> 
Local Address Prefixes  = 10.0.0.0/24, 20.0.0.0/24
Gateway Name            = VNet1GW
PublicIP                = VNet1GWIP
Gateway IP Config       = gwipconfig1 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2

```


## <a name="Login"></a>1. Tooyour. abonelik'e bağlanma

[!INCLUDE [PowerShell login](../../includes/vpn-gateway-ps-login-include.md)]

## <a name="VNet"></a>2. Sanal ağ ve ağ geçidi alt ağı oluşturma

Sanal ağınız yoksa bir sanal ağ oluşturun. Bir sanal ağ oluştururken, belirttiğiniz hello adres alanlarının, şirket içi ağınızda sahip hello adres alanları çakışmadığından emin olun.

[!INCLUDE [About gateway subnets](../../includes/vpn-gateway-about-gwsubnet-include.md)]

[!INCLUDE [No NSG warning](../../includes/vpn-gateway-no-nsg-include.md)]

### <a name="vnet"></a>toocreate sanal ağ ve bir ağ geçidi alt ağı

Bu örnekte, sanal ağ ve ağ geçidi alt ağı oluşturulur. Tooadd görmek için bir ağ geçidi alt ağı gereken sanal ağ zaten varsa [tooadd önceden oluşturulmuş bir ağ geçidi alt ağı tooa sanal ağ](#gatewaysubnet).

Kaynak grubu oluşturun:

```powershell
New-AzureRmResourceGroup -Name TestRG1 -Location 'East US'
```

Sanal ağınızı oluşturun.

1. Merhaba değişkenleri ayarlayın.

  ```powershell
  $subnet1 = New-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27
  $subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name 'Subnet1' -AddressPrefix 10.11.1.0/28
  ```
2. Merhaba VNet oluşturun.

  ```powershell
  New-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1 `
  -Location 'East US' -AddressPrefix 10.11.0.0/16 -Subnet $subnet1, $subnet2
  ```

### <a name="gatewaysubnet"></a>tooadd önceden oluşturduğunuz bir ağ geçidi alt ağı tooa sanal ağ

1. Merhaba değişkenleri ayarlayın.

  ```powershell
  $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG1 -Name TestVet1
  ```
2. Merhaba ağ geçidi alt ağı oluşturun.

  ```powershell
  Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.11.0.0/27 -VirtualNetwork $vnet
  ```
3. Merhaba yapılandırmasını ayarlayın.

  ```powershell
  Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
  ```

## 3. <a name="localnet"></a>Merhaba yerel ağ geçidi oluşturma

Merhaba yerel ağ geçidi genellikle tooyour içi konumunuz anlamına gelir. Merhaba site olarak Azure tooit bakın, sonra kullanabilirsiniz hello IP adresi belirtin bir ad verin hello şirket içi VPN aygıtının toowhich bir bağlantı oluşturur. Ayrıca, hello VPN ağ geçidi toohello VPN cihazı yönlendirilecek hello IP adresi öneklerini belirtin. Belirttiğiniz hello adres öneklerini hello öneklerini şirket içi ağınızda yer alan var. Şirket içi ağınıza değişirse hello öneklerini kolayca güncelleştirebilirsiniz.

Hello aşağıdaki değerleri kullanın:

* Merhaba *Gatewayıpaddress* şirket içi VPN aygıtınızın hello IP adresidir. VPN cihazınız bir NAT’nin arkasında olamaz.
* Merhaba *AddressPrefix* şirket içi adres alanınızdır.

tooadd tek adres ön ekine sahip bir yerel ağ geçidi:

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.0.0.0/24'
  ```

tooadd birden çok adres öneklerini sahip bir yerel ağ geçidi:

  ```powershell
  New-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1 `
  -Location 'East US' -GatewayIpAddress '23.99.221.164' -AddressPrefix @('10.0.0.0/24','20.0.0.0/24')
  ```

yerel ağ geçidinizin IP adresi öneklerini toomodify:<br>
Bazen yerel ağ geçidi ön ekleriniz değişir. Merhaba adımlar önekleri olup, bir VPN ağ geçidi bağlantısı oluşturup oluşturmadığınıza bağlıdır IP adresiniz toomodify uygulayın. Merhaba bkz [bir yerel ağ geçidi değiştirme IP adresi ön eklerini](#modify) bu makalenin.

## <a name="PublicIP"></a>4. Genel IP adresi isteme

Bir VPN ağ geçidinin genel bir IP adresi olmalıdır. Başlangıç IP adresi kaynağı ilk isteği ve ardından sanal ağ geçidinizi oluştururken tooit bakın. Başlangıç IP adresi toohello kaynak Hello VPN ağ geçidi oluşturulup dinamik olarak atanır. VPN Gateway hizmeti şu anda yalnızca *Dinamik* Genel IP adresi ayırmayı desteklemektedir. Statik bir Genel IP adresi ataması isteğinde bulunamazsınız. Ancak, bu tooyour VPN ağ geçidi atandıktan sonra hello IP adresini değiştirse anlamına gelmez. ağ geçidi Hello genel IP adresi değişiklikleri hello zaman hello yalnızca zaman silinmiş ve yeniden oluşturulmalıdır. VPN ağ geçidiniz üzerinde gerçekleştirilen yeniden boyutlandırma, sıfırlama veya diğer iç bakım/yükseltme işlemleri sırasında değişmez.

Tooyour sanal ağ VPN ağ geçidi atanmış bir genel IP adresi isteyin.

```powershell
$gwpip= New-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName TestRG1 -Location 'East US' -AllocationMethod Dynamic
```

## <a name="GatewayIPConfig"></a>5. Merhaba ağ geçidi IP adresleme yapılandırmasını oluşturma

Merhaba ağ geçidi yapılandırmasını hello alt ağı ve hello ortak IP adresi toouse tanımlar. Aşağıdaki örnek toocreate hello ağ geçidi yapılandırmanızı kullanın:

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name TestVNet1 -ResourceGroupName TestRG1
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name gwipconfig1 -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
```

## <a name="CreateGateway"></a>6. Merhaba VPN ağ geçidi oluşturma

Merhaba sanal ağ VPN ağ geçidi oluşturun. Bir VPN ağ geçidi oluşturma too45 dakika veya daha fazla toocomplete alabilir.

Hello aşağıdaki değerleri kullanın:

* Merhaba *- GatewayType* bir Site siteye için yapılandırmadır *Vpn*. Merhaba ağ geçidi türü her zaman, uygulamakta olduğunuz belirli toohello yapılandırmadır. Örneğin, başka ağ geçidi yapılandırmalarında -GatewayType değerinin ExpressRoute olması gerekebilir.
* Merhaba *- VpnType* olabilir *RouteBased* (bazı belgelerde dinamik ağ geçidi tooas denir) veya *PolicyBased* (bazı belgelerde statik ağ geçidi tooas adlandırılır ). VPN ağ geçidi türleri hakkında daha fazla bilgi için bkz. [VPN Gateway Hakkında](vpn-gateway-about-vpngateways.md).
* Merhaba ağ geçidi SKU'su toouse istediğinizi seçin. Bazı SKU’larda yapılandırma sınırlamaları vardır. Daha fazla bilgi için bkz. [Ağ geçidi SKU'ları](vpn-gateway-about-vpn-gateway-settings.md#gwsku). Hello ilgili hello VPN ağ geçidi oluştururken bir hata alırsanız - GatewaySku, doğrulayın hello PowerShell cmdlet'lerinin en yeni sürümünü hello yüklü.

```powershell
New-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1 `
-Location 'East US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased -GatewaySku VpnGw1
```

## <a name="ConfigureVPNDevice"></a>7. VPN cihazınızı yapılandırma

Siteden siteye bağlantıları tooan şirket içi ağ bir VPN cihazı gerektirir. Bu adımda VPN cihazınızı yapılandıracaksınız. VPN Cihazınızı yapılandırırken hello aşağıdaki gerekir:

- Paylaşılan bir anahtar. Bu olduğu hello aynı paylaşılan siteden siteye VPN bağlantınızı oluştururken belirttiğiniz anahtarı. Bu örneklerde temel bir paylaşılan anahtar kullanılır. Daha karmaşık bir anahtar toouse oluşturmak öneririz.
- Merhaba sanal ağ geçidinizin genel IP adresi. Hello Azure portal, PowerShell veya CLI kullanarak hello ortak IP adresini görüntüleyebilirsiniz. toofind hello PowerShell, aşağıdaki örneğine kullanım hello kullanarak sanal ağ geçidinizin genel IP adresi:

  ```powershell
  Get-AzureRmPublicIpAddress -Name GW1PublicIP -ResourceGroupName TestRG1
  ```

[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <a name="CreateConnection"></a>8. Merhaba VPN bağlantısı oluşturun

Ardından, sanal ağ geçidiniz ile VPN cihazınız arasındaki hello siteden siteye VPN bağlantısı oluşturun. Emin tooreplace hello değerleri kendi değerlerinizle olabilir. Merhaba paylaşılan anahtar, VPN cihazınızın yapılandırması için kullanılan hello değerle eşleşmelidir. Bu hello fark '-ConnectionType' siteden siteye için *IPSec*.

1. Merhaba değişkenleri ayarlayın.
  ```powershell
  $gateway1 = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroupName TestRG1
  $local = Get-AzureRmLocalNetworkGateway -Name Site2 -ResourceGroupName TestRG1
  ```

2. Merhaba bağlantı oluşturun.
  ```powershell
  New-AzureRmVirtualNetworkGatewayConnection -Name VNet1toSite2 -ResourceGroupName TestRG1 `
  -Location 'East US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
  -ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
  ```

Kısa bir süre, hello bağlantı kurulur.

## <a name="toverify"></a>9. Merhaba VPN bağlantısını doğrulama

VPN bağlantınızı birkaç farklı şekilde tooverify vardır.

[!INCLUDE [Verify connection](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="connectVM"></a>tooconnect tooa sanal makine

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]


## <a name="modify"></a>Yerel bir ağ geçidinin IP adresi ön eklerini değiştirme

Tooyour şirket içi konumunuz yönlendirilmiş istediğiniz başlangıç IP adresi öneklerini değiştirirseniz, hello yerel ağ geçidi değiştirebilirsiniz. İki ayrı yönerge grubu sunulmuştur. Seçtiğiniz hello yönergeleri olup, zaten, ağ geçidi bağlantısı oluşturup oluşturmadığınıza bağlıdır.

[!INCLUDE [Modify prefixes](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <a name="modifygwipaddress"></a>Bir yerel ağ geçidi Hello ağ geçidi IP adresini değiştirme

[!INCLUDE [Modify gateway IP address](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a>Sonraki adımlar

*  Bağlantınız tamamlandıktan sonra sanal makineleri tooyour sanal ağları ekleyebilirsiniz. Daha fazla bilgi için bkz. [Sanal Makineler](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).
* BGP hakkında daha fazla bilgi için bkz: Merhaba [BGP genel bakış](vpn-gateway-bgp-overview.md) ve [nasıl tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
