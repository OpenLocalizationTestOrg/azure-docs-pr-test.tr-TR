---
title: "Şirket içi ağ tooan Azure sanal ağı bağlanın: siteden siteye VPN: CLI | Microsoft Docs"
description: "Şirket içi bir IPSec bağlantısı üzerinden tooan Azure sanal ağı ağ adımları toocreate genel Internet hello. Bu adımlar CLI kullanarak Siteden Siteye şirket içi ve dışı karışık VPN Gateway bağlantısı oluşturmanıza yardımcı olur."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/09/2017
ms.author: cherylmc
ms.openlocfilehash: c652cf2caf3928cdeb19d7dc329f6db101e5ed90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-with-a-site-to-site-vpn-connection-using-cli"></a>CLI kullanarak Siteden Siteye VPN bağlantısı olan bir sanal ağ oluşturma

Bu makale size nasıl toouse hello Azure CLI toocreate, şirket içi ağ toohello VNet bir siteden siteye VPN ağ geçidi bağlantısını gösterir. Bu makaledeki adımları Hello toohello Resource Manager dağıtım modeli uygulayın. Liste aşağıdaki hello farklı bir seçeneği seçerek farklı dağıtım aracını veya dağıtım modelini kullanarak bu yapılandırma ayrıca oluşturabilirsiniz:<br>

> [!div class="op_single_selector"]
> * [Azure portal](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [CLI](vpn-gateway-howto-site-to-site-resource-manager-cli.md)
> * [Azure portal (klasik)](vpn-gateway-howto-site-to-site-classic-portal.md)
> 
>


![Siteden Siteye şirket içi ve dışı karışık VPN Gateway bağlantısı diyagramı](./media/vpn-gateway-howto-site-to-site-resource-manager-cli/site-to-site-diagram.png)

Kullanılan tooconnect bir siteden siteye VPN gateway bağlantısı olan bir IPSec/IKE (Ikev1 veya Ikev2) VPN tüneli üzerinden tooan Azure sanal ağı şirket içi ağ. Bağlantı bu tür bir VPN cihazı bulunan dışarıya dönük bir genel IP adresi atanmış tooit olan şirket içi gerektirir. VPN ağ geçitleri hakkında daha fazla bilgi için bkz. [VPN ağ geçidi hakkında](vpn-gateway-about-vpngateways.md).

## <a name="before-you-begin"></a>Başlamadan önce

Ölçüt yapılandırmaya başlamadan önce aşağıdaki hello karşıladığınızı doğrulayın:

* Uyumlu bir VPN cihazı ve mümkün tooconfigure olan birisi olduğundan emin olun. Uyumlu VPN cihazları ve cihaz yapılandırması hakkında daha fazla bilgi için bkz.[VPN Cihazları Hakkında](vpn-gateway-about-vpn-devices.md).
* VPN cihazınız için dışarıya dönük genel bir IPv4 adresi olduğunu doğrulayın. Bu IP adresi bir NAT’nin arkasında olamaz.
* Bulunan hello IP adresi aralıklarıyla ilgili bilginiz yoksa, şirket içi ağ, bu ayrıntıları sizin için sağlayabilecek biriyle toocoordinate gerekir. Bu yapılandırma oluşturduğunuzda, Azure tooyour şirket içi konumu yönlendirilecek hello IP adresi aralığı önekleri belirtmeniz gerekir. Şirket içi ağınıza hello ağların hiçbiri diz tooconnect için istediğiniz hello sanal ağ alt ağı üzerinden olabilir.
* Merhaba CLI komutları (2.0 veya üstü) en son sürümünü yüklediğinizden emin olun. Merhaba CLI komutları yükleme hakkında daha fazla bilgi için bkz: [Azure CLI 2.0 yükleme](/cli/azure/install-azure-cli) ve [Azure CLI 2.0 ile çalışmaya başlama](/cli/azure/get-started-with-azure-cli).

### <a name="example"></a>Örnek değerler

Aşağıdaki değerleri toocreate bir test ortamı hello kullanın veya toothese değerleri bkz toobetter anlamak bu makaledeki hello örnekler:

```
#Example values

VnetName                = TestVNet1 
ResourceGroup           = TestRG1 
Location                = eastus 
AddressSpace            = 10.11.0.0/16 
SubnetName              = Subnet1 
Subnet                  = 10.11.0.0/24 
GatewaySubnet           = 10.11.255.0/27 
LocalNetworkGatewayName = Site2 
LNG Public IP           = <VPN device IP address>
LocalAddrPrefix1        = 10.0.0.0/24
LocalAddrPrefix2        = 20.0.0.0/24   
GatewayName             = VNet1GW 
PublicIP                = VNet1GWIP 
VPNType                 = RouteBased 
GatewayType             = Vpn 
ConnectionName          = VNet1toSite2
```

## <a name="Login"></a>1. Tooyour. abonelik'e bağlanma

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-include.md)]

## <a name="rg"></a>2. Kaynak grubu oluşturma

Merhaba aşağıdaki örnek hello 'eastus' konum ' TestRG1' adlı bir kaynak grubu oluşturur. Sanal ağınızı toocreate istediğiniz hello bölgede bir kaynak grubu zaten varsa, bunun yerine bir kullanabilirsiniz.

```azurecli
az group create --name TestRG1 --location eastus
```

## <a name="VNet"></a>3. Sanal ağ oluşturma

Bir sanal ağ zaten yoksa oluşturmak hello kullanarak [az ağ vnet oluşturma](/cli/azure/network/vnet#create) komutu. Bir sanal ağ oluştururken, belirttiğiniz hello adres alanlarının, şirket içi ağınızda sahip hello adres alanları çakışmadığından emin olun.

Merhaba aşağıdaki örnek 'TestVNet1' ve bir alt ağı, 'Subnet1' adlı bir sanal ağ oluşturur.

```azurecli
az network vnet create --name TestVNet1 --resource-group TestRG1 --address-prefix 10.11.0.0/16 --location eastus --subnet-name Subnet1 --subnet-prefix 10.11.0.0/24
```

## 4. <a name="gwsub"></a>Merhaba ağ geçidi alt ağı oluşturun

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

Bu yapılandırma için, bir ağ geçidi alt ağına da ihtiyacınız olacaktır. Merhaba sanal ağ geçidi hello VPN ağ geçidi Hizmetleri tarafından kullanılan hello IP adreslerini içeren bir ağ geçidi alt ağı kullanır. Ağ geçidi alt ağını oluşturduğunuzda, bu alt ağ 'GatewaySubnet' olarak adlandırılmalıdır. Başka bir ad kullanırsanız alt ağ oluşturulur ancak Azure bunu bir ağ geçidi alt ağı olarak değerlendirmez.

Merhaba, belirttiğiniz hello ağ geçidi alt ağı boyutunu toocreate istediğiniz hello VPN ağ geçidi yapılandırmasına bağlıdır. Olası toocreate ağ geçidi alt ağı /29 küçük olmakla birlikte, / 27 veya /28 seçerek daha fazla adreslerini içeren daha büyük bir alt ağı oluşturmanızı öneririz. Daha büyük bir ağ geçidi alt ağı kullanmak yeterli IP adreslerini tooaccommodate olası gelecekteki yapılandırmaları için sağlar.

Kullanım hello [az ağ sanal alt oluşturmak](/cli/azure/network/vnet/subnet#create) komutu toocreate hello ağ geçidi alt ağı.

```azurecli
az network vnet subnet create --address-prefix 10.11.255.0/27 --name GatewaySubnet --resource-group TestRG1 --vnet-name TestVNet1
```

## <a name="localnet"></a>5. Merhaba yerel ağ geçidi oluşturma

Merhaba yerel ağ geçidi genellikle tooyour içi konumunuz anlamına gelir. Merhaba site olarak Azure tooit bakın, sonra kullanabilirsiniz hello IP adresi belirtin bir ad verin hello şirket içi VPN aygıtının toowhich bir bağlantı oluşturur. Ayrıca, hello VPN ağ geçidi toohello VPN cihazı yönlendirilecek hello IP adresi öneklerini belirtin. Belirttiğiniz hello adres öneklerini hello öneklerini şirket içi ağınızda yer alan var. Şirket içi ağınıza değişirse hello öneklerini kolayca güncelleştirebilirsiniz.

Hello aşağıdaki değerleri kullanın:

* Merhaba *--ağ geçidi IP adresi* şirket içi VPN aygıtınızın hello IP adresidir. VPN cihazınız bir NAT’nin arkasında olamaz.
* Merhaba *--yerel adres öneklerini* şirket içi adres alanlarının olduğundan.

Kullanım hello [az ağ yerel-ağ geçidi oluşturmak](/cli/azure/network/local-gateway#create) komutu tooadd birden çok adres öneklerini sahip bir yerel ağ geçidi:

```azurecli
az network local-gateway create --gateway-ip-address 23.99.221.164 --name Site2 --resource-group TestRG1 --local-address-prefixes 10.0.0.0/24 20.0.0.0/24
```

## <a name="PublicIP"></a>6. Genel IP adresi isteme

Bir VPN ağ geçidinin genel bir IP adresi olmalıdır. Başlangıç IP adresi kaynağı ilk isteği ve ardından sanal ağ geçidinizi oluştururken tooit bakın. Başlangıç IP adresi toohello kaynak Hello VPN ağ geçidi oluşturulup dinamik olarak atanır. VPN Gateway hizmeti şu anda yalnızca *Dinamik* Genel IP adresi ayırmayı desteklemektedir. Statik bir Genel IP adresi ataması isteğinde bulunamazsınız. Ancak, bu tooyour VPN ağ geçidi atandıktan sonra hello IP adresini değiştirse anlamına gelmez. ağ geçidi Hello genel IP adresi değişiklikleri hello zaman hello yalnızca zaman silinmiş ve yeniden oluşturulmalıdır. VPN ağ geçidiniz üzerinde gerçekleştirilen yeniden boyutlandırma, sıfırlama veya diğer iç bakım/yükseltme işlemleri sırasında değişmez.

Kullanım hello [az ağ genel IP oluşturun](/cli/azure/network/public-ip#create) komutu toorequest dinamik genel IP adresi.

```azurecli
az network public-ip create --name VNet1GWIP --resource-group TestRG1 --allocation-method Dynamic
```

## <a name="CreateGateway"></a>7. Merhaba VPN ağ geçidi oluşturma

Merhaba sanal ağ VPN ağ geçidi oluşturun. Bir VPN ağ geçidi oluşturma too45 dakika veya daha fazla toocomplete alabilir.

Hello aşağıdaki değerleri kullanın:

* Merhaba *--ağ geçidi türü* bir Site siteye için yapılandırmadır *Vpn*. Merhaba ağ geçidi türü her zaman, uygulamakta olduğunuz belirli toohello yapılandırmadır. Daha fazla bilgi için bkz. [Ağ geçidi türleri](vpn-gateway-about-vpn-gateway-settings.md#gwtype).
* Merhaba *--vpn türü* olabilir *RouteBased* (bazı belgelerde dinamik ağ geçidi tooas denir) veya *PolicyBased* (tooas statik bir ağ geçidi bazı olarak adlandırılır belgeler). Merhaba, bağlandığınız hello aygıtının belirli toorequirements ayardır. VPN ağ geçidi türleri hakkında daha fazla bilgi için bkz. [VPN Gateway yapılandırma ayarları hakkında](vpn-gateway-about-vpn-gateway-settings.md#vpntype).
* Merhaba ağ geçidi SKU'su toouse istediğinizi seçin. Bazı SKU’larda yapılandırma sınırlamaları vardır. Daha fazla bilgi için bkz. [Ağ geçidi SKU'ları](vpn-gateway-about-vpn-gateway-settings.md#gwsku).

Hello kullanarak hello VPN ağ geçidi oluşturmak [az ağ sanal ağ geçidi oluşturma](/cli/azure/network/vnet-gateway#create) komutu. 'Wait--yok-' parametresi hello kullanarak bu komutu çalıştırırsanız, herhangi bir geri bildirim veya çıkış görmüyorum. Bu parametre hello ağ geçidi toocreate hello arka planda sağlar. Bir ağ geçidi toocreate yaklaşık 45 dakika sürer.

```azurecli
az network vnet-gateway create --name VNet1GW --public-ip-address VNet1GWIP --resource-group TestRG1 --vnet TestVNet1 --gateway-type Vpn --vpn-type RouteBased --sku VpnGw1 --no-wait 
```

## <a name="VPNDevice"></a>8. VPN cihazınızı yapılandırma

Siteden siteye bağlantıları tooan şirket içi ağ bir VPN cihazı gerektirir. Bu adımda VPN cihazınızı yapılandıracaksınız. VPN Cihazınızı yapılandırırken hello aşağıdaki gerekir:

- Paylaşılan bir anahtar. Bu olduğu hello aynı paylaşılan siteden siteye VPN bağlantınızı oluştururken belirttiğiniz anahtarı. Bu örneklerde temel bir paylaşılan anahtar kullanılır. Daha karmaşık bir anahtar toouse oluşturmak öneririz.
- Merhaba sanal ağ geçidinizin genel IP adresi. Hello Azure portal, PowerShell veya CLI kullanarak hello ortak IP adresini görüntüleyebilirsiniz. sanal ağ geçidinizi kullanın hello toofind hello genel IP adresi [az ağ ortak IP listesi](/cli/azure/network/public-ip#list) komutu. Kolay okuma için hello çıkış biçimlendirilmiş toodisplay hello genel IP'ler, tablo biçiminde listesidir.

  ```azurecli
  az network public-ip list --resource-group TestRG1 --output table
  ```


[!INCLUDE [Configure VPN device](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]


## <a name="CreateConnection"></a>9. Merhaba VPN bağlantısı oluşturun

Sanal ağ geçidiniz ve şirket içi VPN aygıtınızın arasında Hello siteden siteye VPN bağlantısı oluşturun. Yapılandırılmış hello eşleşmelidir ödeme özellikle dikkat toohello paylaşılan anahtar değeri, VPN cihazınız için anahtar değeri paylaşılan.

Hello kullanarak hello bağlantısı oluşturma [az ağ vpn bağlantısı oluşturmak](/cli/azure/network/vpn-connection#create) komutu.

```azurecli
az network vpn-connection create --name VNet1toSite2 -resource-group TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key abc123 --local-gateway2 Site2
```

Kısa bir süre, hello bağlantı kurulur.

## <a name="toverify"></a>10. Merhaba VPN bağlantısını doğrulama

[!INCLUDE [verify connection](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

Başka bir yöntem tooverify toouse istiyorsanız, bağlantınızı bkz [bir VPN ağ geçidi bağlantısını doğrulama](vpn-gateway-verify-connection-resource-manager.md).

## <a name="connectVM"></a>tooconnect tooa sanal makine

[!INCLUDE [Connect tooa VM](../../includes/vpn-gateway-connect-vm-s2s-include.md)]

## <a name="tasks"></a>Genel görevler

Bu bölüm, siteden siteye yapılandırmalarla çalışırken yararlı olan genel komutları içerir. Merhaba tam CLI ağ komutların listesi için bkz: [Azure CLI - ağ](/cli/azure/network).

[!INCLUDE [local network gateway common tasks](../../includes/vpn-gateway-common-tasks-cli-include.md)]

## <a name="next-steps"></a>Sonraki adımlar

* Bağlantınız tamamlandıktan sonra sanal makineleri tooyour sanal ağları ekleyebilirsiniz. Daha fazla bilgi için bkz. [Sanal Makineler](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).
* BGP hakkında daha fazla bilgi için bkz: Merhaba [BGP genel bakış](vpn-gateway-bgp-overview.md) ve [nasıl tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
* Zorlamalı Tünel Oluşturma hakkında bilgi için bkz. [Zorlamalı Tünel Oluşturma Hakkında](vpn-gateway-forced-tunneling-rm.md).
* Yüksek Oranda Kullanılabilir Etkin-Etkin bağlantılar hakkında bilgi için bkz. [Yüksek Oranda Kullanılabilir Şirket İçi ve Dışı ile Sanal Ağdan Sanal Ağa Bağlantı](vpn-gateway-highlyavailable.md).
* Ağ Azure CLI komutlarının listesi için bkz. [Azure CLI](https://docs.microsoft.com/cli/azure/network).