---
title: "Sanal ağ tooanother VNet bağlanın: Azure CLI | Microsoft Docs"
description: "Bu makalede, Azure Resource Manager ve Azure CLI kullanarak sanal ağları birbirine bağlama konusu incelenmektedir."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 0683c664-9c03-40a4-b198-a6529bf1ce8b
ms.service: vpn-gateway
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/02/2017
ms.author: cherylmc
ms.openlocfilehash: 70113914bcae03c80f9ad133ff081d1cf37fc309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-azure-cli"></a>Azure CLI kullanarak sanal ağlar arası VPN ağ geçidi bağlantısı yapılandırma

Bu makale size nasıl gösterir toocreate sanal ağlar arasında bir VPN ağ geçidi bağlantısı. Merhaba sanal ağları olabilir hello aynı ya da farklı bölgelerde ve gelen aynı hello ya da farklı Aboneliklerde. Bağlanan sanal ağlar farklı aboneliklerden hello abonelikleri ile ilişkili toobe gerekmediğinde aynı Active Directory Kiracı hello. 

Bu makaledeki adımları Hello toohello Resource Manager dağıtım modeli uygulayın ve Azure CLI kullanın. Liste aşağıdaki hello farklı bir seçeneği seçerek farklı dağıtım aracını veya dağıtım modelini kullanarak bu yapılandırma ayrıca oluşturabilirsiniz:

> [!div class="op_single_selector"]
> * [Azure portal](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [Azure CLI](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Azure portal (klasik)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Farklı dağıtım modellerini bağlama - Azure portalı](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Farklı dağıtım modellerini bağlama - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

Sanal ağ tooanother sanal ağ (VNet-VNet) bağlanma benzer tooconnecting bir VNet tooan şirket içi site konumu değil. Her iki bağlantı türü bir VPN ağ geçidi tooprovide IPSec/IKE kullanarak güvenli bir tünel kullanın. Sanal ağlar hello varsa aynı bölgede VNet eşlemesi kullanarak bunları bağlanma tooconsider isteyebilir. VNet eşlemesi VPN ağ geçidini kullanmaz. Daha fazla bilgi için bkz. [VNet eşlemesi](../virtual-network/virtual-network-peering-overview.md).

Hatta Sanal Ağdan Sanal Ağa iletişim çok siteli yapılandırmalarla bile birleştirilebilir. Hello Aşağıdaki diyagramda gösterildiği gibi arası sanal ağ bağlantısı ile şirket içi bağlantılar birleştiren ağ topolojileri kurabilmenize olanak sağlar:

![Bağlantılar hakkında](./media/vpn-gateway-howto-vnet-vnet-cli/aboutconnections.png)

### <a name="why"></a>Sanal ağları neden bağlamalıyız?

Aşağıdaki nedenlerden Merhaba tooconnect sanal ağlar isteyebilirsiniz:

* **Çapraz bölge coğrafi artıklığı ve coğrafi-durum**

  * Kendi coğrafi çoğaltma veya eşitlemenizi, güvenli bağlantıyla İnternet’te uç noktalara gitmeden ayarlayabilirsiniz.
  * Azure Traffic Manager ve Load Balancer ile birçok Azure bölgesinde coğrafi yedeklilik imkanıyla yüksek oranda kullanılabilir iş yükü oluşturabilirsiniz. Bir önemli SQL Always On kullanılabilirlik grupları: birden fazla Azure bölgesine yayılan ile yukarı tooset örnektir.
* **Yalıtım veya yönetim sınır bölgesel çok katmanlı uygulamalar**

  * İçinde hello aynı bölge tooisolation ya da yönetim gereksinimleri birbirlerine bağlı birden çok sanal ağ ile çok katmanlı uygulamalar ayarlayabilirsiniz.

VNet-VNet bağlantıları hakkında daha fazla bilgi için bkz: Merhaba [VNet-VNet ile ilgili SSS](#faq) hello bu makalenin sonunda.

### <a name="which-set-of-steps-should-i-use"></a>Hangi adımları tamamlamalıyım? 

Bu makalede iki farklı adım kümesi görürsünüz. Adımlar için bir dizi [içinde bulunan sanal ağlar aynı abonelik hello](#samesub), diğeri [farklı Aboneliklerde bulunan sanal ağlar](#difsub).

## <a name="samesub"></a>Hello olan sanal ağlara bağlantı aynı abonelik

![v2v diyagramı](./media/vpn-gateway-howto-vnet-vnet-cli/v2vrmps.png)

### <a name="before-you-begin"></a>Başlamadan önce

Başlamadan önce hello hello CLI komutları (2.0 veya üstü) en son sürümünü yükleyin. Merhaba CLI komutları yükleme hakkında daha fazla bilgi için bkz: [Azure CLI 2.0 yükleme](/cli/azure/install-azure-cli).

### <a name="Plan"></a>IP adresi aralıklarınızı planlama

Aşağıdaki adımları hello, kullanıcıların kendi ağ geçidi alt ağları ve yapılandırmalarıyla birlikte iki sanal ağ oluşturun. Ardından hello arasında bir VPN bağlantısı iki Vnet oluşturuyoruz. Önemli tooplan başlangıç IP adresi aralıklarını ağ yapılandırmanızı olur. Sanal ağ aralıklarınızın ya da yerel ağ aralıklarınızın hiçbir şekilde çakışmadığından emin olmalısınız. Bu örneklerde bir DNS sunucusu eklemiyoruz. Sanal ağlarınız için ad çözümlemesi istiyorsanız bkz. [Ad çözümlemesi](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

Merhaba örnekleri değerleri aşağıdaki hello kullanırız:

**Değerler TestVNet1 için:**

* VNet Name: TestVNet1
* Resource Group: TestRG1
* Location: East US
* TestVNet1: 10.11.0.0/16 & 10.12.0.0/16
* FrontEnd: 10.11.0.0/24
* BackEnd: 10.12.0.0/24
* GatewaySubnet: 10.12.255.0/27
* GatewayName: VNet1GW
* Public IP: VNet1GWIP
* VPNType: RouteBased
* Connection(1to4): VNet1toVNet4
* Connection(1to5): VNet1toVNet5
* ConnectionType: VNet2VNet

**Değerler TestVNet4 için:**

* VNet Name: TestVNet4
* TestVNet2: 10.41.0.0/16 & 10.42.0.0/16
* FrontEnd: 10.41.0.0/24
* BackEnd: 10.42.0.0/24
* GatewaySubnet: 10.42.255.0/27
* Resource Group: TestRG4
* Location: West US
* GatewayName: VNet4GW
* Public IP: VNet4GWIP
* VPNType: RouteBased
* Connection: VNet4toVNet1
* ConnectionType: VNet2VNet


### <a name="Connect"></a>1. adım - tooyour. abonelik'e bağlanma

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-numbers-include.md)]

### <a name="TestVNet1"></a>Adım 2 - oluşturma ve TestVNet1 yapılandırma

1. Bir kaynak grubu oluşturun.

  ```azurecli
  az group create -n TestRG1  -l eastus
  ```
2. TestVNet1 için TestVNet1 ve hello alt ağlar oluşturun. Bu örnekte, TestVNet1 adlı bir sanal ağ ve FrontEnd adlı bir alt ağ oluşturulur.

  ```azurecli
  az network vnet create -n TestVNet1 -g TestRG1 --address-prefix 10.11.0.0/16 -l eastus --subnet-name FrontEnd --subnet-prefix 10.11.0.0/24
  ```
3. Merhaba arka uç alt ağ için ek adres alanı oluşturun. Bu adımda, biz daha önce oluşturduğumuz iki hello adres alanını belirtin ve ek adres alanı tooadd istiyoruz Merhaba, dikkat edin. Bunun nedeni, hello [az ağ vnet güncelleştirmesi](https://docs.microsoft.com/cli/azure/network/vnet#update) komutu hello önceki ayarların üzerine yazar. Emin toospecify tüm hello adres öneklerinin bu komutunu kullanırken olun.

  ```azurecli
  az network vnet update -n TestVNet1 --address-prefixes 10.11.0.0/16 10.12.0.0/16 -g TestRG1
  ```
4. Merhaba arka uç alt ağ oluşturun.
  
  ```azurecli
  az network vnet subnet create --vnet-name TestVNet1 -n BackEnd -g TestRG1 --address-prefix 10.12.0.0/24 
  ```
5. Merhaba ağ geçidi alt ağı oluşturun. Bu hello ağ geçidi alt ağı 'GatewaySubnet' adlı dikkat edin. Bu ad gereklidir. Bu örnekte, hello ağ geçidi alt ağı/27 kullanmaktadır. Olası toocreate ağ geçidi alt ağı /29 küçük olmakla birlikte, en az/28 veya /27 seçerek daha fazla adreslerini içeren daha büyük bir alt ağı oluşturmanızı öneririz. Bu, gelecekteki hello isteyebileceğiniz yeterli adresleri tooaccommodate olası ek yapılandırmalar için izin verir.

  ```azurecli 
  az network vnet subnet create --vnet-name TestVNet1 -n GatewaySubnet -g TestRG1 --address-prefix 10.12.255.0/27
  ```
6. Ağınız için oluşturacağınız bir ortak IP adresi toobe ayrılmış toohello ağ geçidi isteği. Bu hello AllocationMethod dinamik olduğuna dikkat edin. Başlangıç IP adresi toouse istediğiniz belirtemezsiniz. Dinamik olarak ayrılan tooyour geçididir.

  ```azurecli
  az network public-ip create -n VNet1GWIP -g TestRG1 --allocation-method Dynamic
  ```
7. TestVNet1 için Hello sanal ağ geçidi oluşturun. Sanal Ağdan Sanal Ağa yapılandırmaları, RouteBased bir VPNType gerektirir. 'Wait--yok-' parametresi hello kullanarak bu komutu çalıştırırsanız, herhangi bir geri bildirim veya çıkış görmüyorum. Merhaba 'wait--yok-' parametresi hello ağ geçidi toocreate hello arka planda izin verir. Bu hello VPN ağ geçidi hemen oluşturmayı tamamladığında anlamına gelmez. Bir ağ geçidi oluşturma 45 dakika veya daha fazla hello ağ geçidi kullandığınız SKU bağlı olarak genellikle alabilir.

  ```azurecli
  az network vnet-gateway create -n VNet1GW -l eastus --public-ip-address VNet1GWIP -g TestRG1 --vnet TestVNet1 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="TestVNet4"></a>3. Adım - TestVNet4’ü oluşturma ve yapılandırma

1. Bir kaynak grubu oluşturun.

  ```azurecli
  az group create -n TestRG4  -l westus
  ```
2. TestVNet4’ü oluşturun.

  ```azurecli
  az network vnet create -n TestVNet4 -g TestRG4 --address-prefix 10.41.0.0/16 -l westus --subnet-name FrontEnd --subnet-prefix 10.41.0.0/24
  ```

3. TestVNet4 için ek alt ağlar oluşturun.

  ```azurecli
  az network vnet update -n TestVNet4 --address-prefixes 10.41.0.0/16 10.42.0.0/16 -g TestRG4 
  az network vnet subnet create --vnet-name TestVNet4 -n BackEnd -g TestRG4 --address-prefix 10.42.0.0/24 
  ```
4. Merhaba ağ geçidi alt ağı oluşturun.

  ```azurecli
   az network vnet subnet create --vnet-name TestVNet4 -n GatewaySubnet -g TestRG4 --address-prefix 10.42.255.0/27
  ```
5. Bir Genel IP adresi isteyin.

  ```azurecli
  az network public-ip create -n VNet4GWIP -g TestRG4 --allocation-method Dynamic
  ```
6. Merhaba TestVNet4 sanal ağ geçidi oluşturun.

  ```azurecli
  az network vnet-gateway create -n VNet4GW -l westus --public-ip-address VNet4GWIP -g TestRG4 --vnet TestVNet4 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="createconnect"></a>4. adım - hello bağlantıları oluşturma

Artık VPN ağ geçitleri olan iki sanal ağınız var. Merhaba sonraki hello sanal ağ geçitleri arasında toocreate VPN ağ geçidi bağlantıları adımdır. Merhaba örnekler yukarıdaki kullandıysanız, VNet ağ geçitleri farklı kaynak gruplarında olduğunda. Ağ geçitleri farklı kaynak gruplarında olduğunda tooidentify gerekir ve her ağ geçidi için hello kaynak kimlikleri bağlantı kurarken belirtin. Sanal ağlar hello varsa aynı kaynak grubu, hello kullanabilirsiniz [yönergeleri ikinci kümesi](#samerg) toospecify hello kaynak kimlikleri gerektiğinden yok.

### <a name="diffrg"></a>tooconnect farklı kaynak gruplarında bulunan sanal ağlar

1. Merhaba, kaynak kimliği VNet1GW komutu aşağıdaki hello hello çıktısından alın:

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  Hello çıktısında hello Bul "kimliği:" satır. Merhaba hello tırnak işareti içinde gerekli toocreate hello bağlantı hello sonraki bölümde değerlerdir. Böylece, kolayca bunları bağlantınızı oluştururken yapıştırabilirsiniz bu değerleri tooa metin düzenleyici, Not Defteri gibi kopyalayın.

  Örnek çıktı:

  ```
  "activeActive": false, 
  "bgpSettings": { 
    "asn": 65515, 
    "bgpPeeringAddress": "10.12.255.30", 
    "peerWeight": 0 
   }, 
  "enableBgp": false, 
  "etag": "W/\"ecb42bc5-c176-44e1-802f-b0ce2962ac04\"", 
  "gatewayDefaultSite": null, 
  "gatewayType": "Vpn", 
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW", 
  "ipConfigurations":
  ```

  Sonra Hello değerleri kopyalamak **"id":** hello tırnak işareti içinde.

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
 ```

2. Merhaba, kaynak kimliği VNet4GW ve kopyalama hello değerleri tooa metin düzenleyicisi alın.

  ```azurecli
  az network vnet-gateway show -n VNet4GW -g TestRG4
  ```

3. Merhaba TestVNet1 tooTestVNet4 bağlantı oluşturun. Bu adımda TestVNet1 tooTestVNet4 hello bağlantı oluşturun. Merhaba örneklerde paylaşılan bir anahtarı yok. Merhaba paylaşılan anahtar için kendi değerlerinizi kullanabilirsiniz. Merhaba hello paylaşılan anahtara şeydir önemli hem bağlantılarında eşleşmesi gerekir. Bağlantı oluşturma toocomplete sırasında kısa sürer.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW 
  ```
4. Merhaba TestVNet4 tooTestVNet1 bağlantı oluşturun. TestVNet4 tooTestVNet1 hello bağlantı oluşturma dışında bu benzer toohello yukarıdaki bir adımdır. Merhaba paylaşılan anahtarların eşleştiğinden emin olun. Tooestablish hello bağlantı birkaç dakika sürer.

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG4 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW -l westus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1G
  ```
5. Bağlantılarınızı doğrulayın. Bkz. [Bağlantınızı doğrulama](#verify).

### <a name="samerg"></a>tooconnect hello aynı bulunan sanal ağlar kaynak grubu

1. Merhaba TestVNet1 tooTestVNet4 bağlantı oluşturun. Bu adımda TestVNet1 tooTestVNet4 hello bağlantı oluşturun. Bildirim hello kaynak grupları olan hello hello örneklerde aynı. Merhaba örneklerde paylaşılan bir anahtar de görebilirsiniz. Merhaba paylaşılan anahtar için kendi değerlerinizi kullanabilirsiniz, ancak hello paylaşılan anahtar için her iki bağlantı eşleşmelidir. Bağlantı oluşturma toocomplete sırasında kısa sürer.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet4GW
  ```
2. Merhaba TestVNet4 tooTestVNet1 bağlantı oluşturun. TestVNet4 tooTestVNet1 hello bağlantı oluşturma dışında bu benzer toohello yukarıdaki bir adımdır. Merhaba paylaşılan anahtarların eşleştiğinden emin olun. Tooestablish hello bağlantı birkaç dakika sürer.

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG1 --vnet-gateway1 VNet4GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet1GW
  ```
3. Bağlantılarınızı doğrulayın. Bkz. [Bağlantınızı doğrulama](#verify).

## <a name="difsub"></a>Farklı aboneliklerdeki VNet'leri bağlama

![v2v diyagramı](./media/vpn-gateway-howto-vnet-vnet-cli/v2vdiffsub.png)

Bu senaryoda TestVNet1 ve TestVNet5 bağlanır. Merhaba sanal ağlar farklı Aboneliklerde bulunur. Merhaba abonelikleri hello ile ilişkili toobe gerek yoktur aynı Active Directory kiracısı. Bu yapılandırma için Hello adımları sipariş tooconnect TestVNet1 tooTestVNet5 ek bir VNet-VNet bağlantı ekleyin.

### <a name="TestVNet1diff"></a>5. Adım - TestVNet1’i oluşturma ve yapılandırma

Bu yönergeleri, önceki bölümlerde hello hello adımlardan devam edin. Tamamlamanız gereken [1. adım](#Connect) ve [2. adım](#TestVNet1) toocreate TestVNet1 yapılandırmak ve VPN ağ geçidi için TestVNet1 hello. Oluşturursanız, bu adımlara devam çakışmamasını rağmen bu yapılandırma için gerekli toocreate TestVNet4 hello önceki bölümden değildir. 1. ve 2. Adımı tamamladıktan sonra 6. Adıma (aşağıda) geçin.

### <a name="verifyranges"></a>6. adım - başlangıç IP adresi aralıklarını doğrulama

Ek bağlantılar oluştururken, başlangıç IP adresi alanı hello yeni sanal ağın hiçbirini diğer aralıklarınız veya yerel ağ geçidi aralıkları ile çakışmaması önemli tooverify bağlıdır. Bu alıştırmada, hello TestVNet5 için değerler aşağıdaki hello kullanabilirsiniz:

**Değerler TestVNet5 için:**

* VNet Name: TestVNet5
* Resource Group: TestRG5
* Location: Japan East
* TestVNet5: 10.51.0.0/16 & 10.52.0.0/16
* FrontEnd: 10.51.0.0/24
* BackEnd: 10.52.0.0/24
* GatewaySubnet: 10.52.255.0.0/27
* GatewayName: VNet5GW
* Public IP: VNet5GWIP
* VPNType: RouteBased
* Connection: VNet5toVNet1
* ConnectionType: VNet2VNet

### <a name="TestVNet5"></a>7. Adım - TestVNet5’i oluşturma ve yapılandırma

Bu adım hello hello yeni abonelik, 5. abonelik bağlamında yapılmalıdır. Bu bölümü hello aboneliğin sahibi olan farklı bir kuruluşta hello Yöneticisi tarafından gerçekleştirilebilir. Abonelikleri kullanımı arasındaki tooswitch ' az hesabı listesi--tüm ' toolist hello abonelikleri kullanılabilir tooyour hesabı sonra kullanın ' az hesabı kümesi--abonelik <subscriptionID>' toouse istediğiniz tooswitch toohello abonelik.

1. Bağlı tooSubscription 5 olan, sonra bir kaynak grubu oluşturmak emin olun.

  ```azurecli
  az group create -n TestRG5  -l japaneast
  ```
2. TestVNet5’i oluşturun.

  ```azurecli
  az network vnet create -n TestVNet5 -g TestRG5 --address-prefix 10.51.0.0/16 -l japaneast --subnet-name FrontEnd --subnet-prefix 10.51.0.0/24
  ```

3. Alt ağlar ekleyin.

  ```azurecli
  az network vnet update -n TestVNet5 --address-prefixes 10.51.0.0/16 10.52.0.0/16 -g TestRG5
  az network vnet subnet create --vnet-name TestVNet5 -n BackEnd -g TestRG5 --address-prefix 10.52.0.0/24
  ```

4. Merhaba ağ geçidi alt ağı ekleyin.

  ```azurecli
  az network vnet subnet create --vnet-name TestVNet5 -n GatewaySubnet -g TestRG5 --address-prefix 10.52.255.0/27
  ```

5. Genel bir IP adresi isteyin.

  ```azurecli
  az network public-ip create -n VNet5GWIP -g TestRG5 --allocation-method Dynamic
  ```
6. Merhaba TestVNet5 ağ geçidini oluşturma

  ```azurecli
  az network vnet-gateway create -n VNet5GW -l japaneast --public-ip-address VNet5GWIP -g TestRG5 --vnet TestVNet5 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="connections5"></a>8. adım - hello bağlantıları oluşturma

Biz bu adımla olarak işaretlenmiş iki CLI oturumları bölme **[abonelik 1]**, ve **[5. abonelik]** hello ağ geçitleri hello farklı Aboneliklerde olduğundan. Abonelikleri kullanımı arasındaki tooswitch ' az hesabı listesi--tüm ' toolist hello abonelikleri kullanılabilir tooyour hesabı sonra kullanın ' az hesabı kümesi--abonelik <subscriptionID>' toouse istediğiniz tooswitch toohello abonelik.

1. **[1. abonelik]**  Oturum açın ve tooSubscription 1 bağlanın. Çalışma hello aşağıdaki tooget hello adını ve Kimliğini hello hello çıktısından ağ geçidi komutu:

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  Merhaba çıktısını Kopyala "kimliği:". Hello kimliği ve hello hello VNet ağ geçidi (VNet1GW) toohello yöneticinin adı 5. aboneliğin e-posta veya başka bir yöntemle gönderin.

  Örnek çıktı:

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
  ```

2. **[5. abonelik]**  Oturum açın ve tooSubscription 5 bağlanın. Çalışma hello aşağıdaki tooget hello adını ve Kimliğini hello hello çıktısından ağ geçidi komutu:

  ```azurecli
  az network vnet-gateway show -n VNet5GW -g TestRG5
  ```

  Merhaba çıktısını Kopyala "kimliği:". Hello kimliği ve hello hello VNet ağ geçidi (vnet5gw'un) toohello yöneticisinin adını abonelik 1 e-posta veya başka bir yöntemle gönderin.

3. **[1. abonelik]**  Bu adımda TestVNet1 tooTestVNet5 hello bağlantı oluşturun. Merhaba paylaşılan anahtar için kendi değerlerinizi kullanabilirsiniz, ancak hello paylaşılan anahtar için her iki bağlantı eşleşmelidir. Bağlantı oluşturma toocomplete sırasında kısa sürebilir. TooSubscription 1 bağlandığınızdan emin olun.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet5 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```

4. **[5. abonelik]**  TestVNet5 tooTestVNet1 hello bağlantı oluşturma dışında bu benzer toohello yukarıdaki bir adımdır. Bu hello paylaşılan anahtarlar eşleşme ve tooSubscription 5 bağlanmak emin olun.

  ```azurecli
  az network vpn-connection create -n VNet5ToVNet1 -g TestRG5 --vnet-gateway1 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW -l japaneast --shared-key "eeffgg" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```

## <a name="verify"></a>Merhaba bağlantılarını doğrulama
[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections v2v cli](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

## <a name="faq"></a>Sanal ağlar arası bağlantılar hakkında SSS
[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-vnet-vnet-faq-include.md)]

## <a name="next-steps"></a>Sonraki adımlar

* Bağlantınız tamamlandıktan sonra sanal makineleri tooyour sanal ağları ekleyebilirsiniz. Daha fazla bilgi için bkz: Merhaba [Virtual Machines belgeleri](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).
* BGP hakkında daha fazla bilgi için bkz: Merhaba [BGP genel bakış](vpn-gateway-bgp-overview.md) ve [nasıl tooconfigure BGP](vpn-gateway-bgp-resource-manager-ps.md).
