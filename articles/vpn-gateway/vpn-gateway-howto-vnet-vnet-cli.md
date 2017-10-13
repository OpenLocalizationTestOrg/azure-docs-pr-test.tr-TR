---
title: "Bir sanal ağı başka bir sanal ağa bağlama: Azure CLI | Microsoft Docs"
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
ms.openlocfilehash: ff859bd9dbbf30c461cdba8409c77b04ff97b1f6
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/11/2017
---
# <a name="configure-a-vnet-to-vnet-vpn-gateway-connection-using-azure-cli"></a>Azure CLI kullanarak sanal ağlar arası VPN ağ geçidi bağlantısı yapılandırma

Bu makalede, sanal ağlar arasında VPN ağ geçidi bağlantısının nasıl oluşturulduğu gösterilir. Sanal ağlar aynı ya da farklı bölgelerde ve aynı ya da farklı aboneliklerde bulunuyor olabilirler. Farklı aboneliklerden sanal ağları bağlarken aboneliklerin aynı Active Directory kiracısıyla ilişkilendirilmiş olması gerekmez. 

Bu makaledeki adımlar Resource Manager dağıtım modeli için geçerlidir ve Azure CLI kullanılır. Ayrıca aşağıdaki listeden farklı bir seçenek belirtip farklı bir dağıtım aracı veya dağıtım modeli kullanarak da bu yapılandırmayı oluşturabilirsiniz:

> [!div class="op_single_selector"]
> * [Azure portal](vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)
> * [PowerShell](vpn-gateway-vnet-vnet-rm-ps.md)
> * [Azure CLI](vpn-gateway-howto-vnet-vnet-cli.md)
> * [Azure portal (klasik)](vpn-gateway-howto-vnet-vnet-portal-classic.md)
> * [Farklı dağıtım modellerini bağlama - Azure portalı](vpn-gateway-connect-different-deployment-models-portal.md)
> * [Farklı dağıtım modellerini bağlama - PowerShell](vpn-gateway-connect-different-deployment-models-powershell.md)
>
>

Bir sanal ağı başka bir sanal ağa bağlamak (VNet'ten VNet'e), bir VNet'i şirket içi site konumuna bağlamakla aynıdır. Her iki bağlantı türü de IPsec/IKE kullanarak güvenli bir tünel sunmak üzere bir VPN ağ geçidi kullanır. VNet’leriniz aynı bölgedeyse VNet Eşlemesi kullanarak bağlamayı düşünebilirsiniz. VNet eşlemesi VPN ağ geçidini kullanmaz. Daha fazla bilgi için bkz. [VNet eşlemesi](../virtual-network/virtual-network-peering-overview.md).

Hatta Sanal Ağdan Sanal Ağa iletişim çok siteli yapılandırmalarla bile birleştirilebilir. Bunun yapılması aşağıdaki diyagramda da görüldüğü gibi şirket içi ve şirket dışı bağlantıyla sanal ağ içi bağlantıyı birleştiren ağ topolojileri kurabilmenize olanak sağlar:

![Bağlantılar hakkında](./media/vpn-gateway-howto-vnet-vnet-cli/aboutconnections.png)

### <a name="why"></a>Sanal ağları neden bağlamalıyız?

Sanal ağları aşağıdaki sebeplerden dolayı bağlamak isteyebilirsiniz:

* **Çapraz bölge coğrafi artıklığı ve coğrafi-durum**

  * Kendi coğrafi çoğaltma veya eşitlemenizi, güvenli bağlantıyla İnternet’te uç noktalara gitmeden ayarlayabilirsiniz.
  * Azure Traffic Manager ve Load Balancer ile birçok Azure bölgesinde coğrafi yedeklilik imkanıyla yüksek oranda kullanılabilir iş yükü oluşturabilirsiniz. Buna önemli bir örnek olarak SQL Always On ile birden fazla Azure bölgesine yayılan Kullanılabilirlik Grupları’nı birlikte kurmak verilebilir.
* **Yalıtım veya yönetim sınır bölgesel çok katmanlı uygulamalar**

  * Yalıtım ve yönetim gereksinimlerinden dolayı aynı bölge içinde birbirlerine bağlı birden fazla sanal ağ ile çok katmanlı uygulamalar kurabilirsiniz.

Sanal ağlar arası bağlantılar hakkında daha fazla bilgi için bu makalenin sonunda yer alan [Sanal ağlar arası bağlantılar hakkında SSS](#faq) bölümünü inceleyin.

### <a name="which-set-of-steps-should-i-use"></a>Hangi adımları tamamlamalıyım? 

Bu makalede iki farklı adım kümesi görürsünüz. Bir adım kümesi [Aynı abonelikte bulunan sanal ağlar](#samesub), diğer adım kümesi ise [Farklı aboneliklerde bulunan sanal ağlar](#difsub) içindir.

## <a name="samesub"></a>Aynı abonelikte olan sanal ağları bağlanma

![v2v diyagramı](./media/vpn-gateway-howto-vnet-vnet-cli/v2vrmps.png)

### <a name="before-you-begin"></a>Başlamadan önce

Başlamadan önce, CLI komutlarının en son sürümünü (2.0 veya üzeri) yükleyin. CLI komutlarını yükleme hakkında bilgi için bkz. [Azure CLI 2.0’ı yükleme](/cli/azure/install-azure-cli).

### <a name="Plan"></a>IP adresi aralıklarınızı planlama

Aşağıdaki adımlarda kendi ağ geçidi alt ağları ve yapılandırmalarıyla birlikte iki sanal ağ oluşturulur. Daha sonra iki sanal ağ arasında bir VPN bağlantısı oluşturulur. Ağ yapılandırmanız için IP adres aralıklarını planlamanız önemlidir. Sanal ağ aralıklarınızın ya da yerel ağ aralıklarınızın hiçbir şekilde çakışmadığından emin olmalısınız. Bu örneklerde bir DNS sunucusu eklemiyoruz. Sanal ağlarınız için ad çözümlemesi istiyorsanız bkz. [Ad çözümlemesi](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).

Örneklerde aşağıdaki değerler kullanılmaktadır:

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


### <a name="Connect"></a>1. Adım: Aboneliğinize bağlanma

[!INCLUDE [CLI login](../../includes/vpn-gateway-cli-login-numbers-include.md)]

### <a name="TestVNet1"></a>Adım 2 - oluşturma ve TestVNet1 yapılandırma

1. Bir kaynak grubu oluşturun.

  ```azurecli
  az group create -n TestRG1  -l eastus
  ```
2. TestVNet1’i ve TestVNet1’in alt ağlarını oluşturun. Bu örnekte, TestVNet1 adlı bir sanal ağ ve FrontEnd adlı bir alt ağ oluşturulur.

  ```azurecli
  az network vnet create -n TestVNet1 -g TestRG1 --address-prefix 10.11.0.0/16 -l eastus --subnet-name FrontEnd --subnet-prefix 10.11.0.0/24
  ```
3. Arka uç alt ağı için ek bir adres alanı oluşturun. Bu adımda hem daha önce oluşturduğumuz adres alanını hem de eklemek istediğimiz ek etki alanını belirttiğimize dikkat edin. Bunun nedeni, [az network vnet update](https://docs.microsoft.com/cli/azure/network/vnet#az_network_vnet_update) komutunun önceki ayarların üzerine yazmasıdır. Bu komutu kullanırken tüm adres ön eklerini belirttiğinizden emin olun.

  ```azurecli
  az network vnet update -n TestVNet1 --address-prefixes 10.11.0.0/16 10.12.0.0/16 -g TestRG1
  ```
4. Arka uç alt ağını oluşturun.
  
  ```azurecli
  az network vnet subnet create --vnet-name TestVNet1 -n BackEnd -g TestRG1 --address-prefix 10.12.0.0/24 
  ```
5. Ağ geçidi alt ağını oluşturun. Ağ geçidi alt ağının 'GatewaySubnet' olarak adlandırıldığına dikkat edin. Bu ad gereklidir. Bu örnekte ağ geçidi alt ağı bir /27 kullanmaktadır. /29 kadar küçük bir ağ geçidi alt ağı oluşturmak mümkün olsa da en az /28 veya /27’yi seçerek daha fazla adres içeren büyük bir alt ağ oluşturmanızı öneririz. Bu, gelecekte isteyebileceğiniz ek yapılandırmaları da içerecek yeteri kadar adres sağlayacaktır.

  ```azurecli 
  az network vnet subnet create --vnet-name TestVNet1 -n GatewaySubnet -g TestRG1 --address-prefix 10.12.255.0/27
  ```
6. Sanal ağınız için oluşturacağınız ağ geçidine ayrılacak genel IP adresi isteyin. AllocationMethod değerinin Dinamik olduğuna dikkat edin. Kullanmak istediğiniz IP adresini belirtemezsiniz. IP adresi, ağ geçidinize dinamik olarak ayrılır.

  ```azurecli
  az network public-ip create -n VNet1GWIP -g TestRG1 --allocation-method Dynamic
  ```
7. TestVNet1 için sanal ağ geçidini oluşturun. Sanal Ağdan Sanal Ağa yapılandırmaları, RouteBased bir VPNType gerektirir. Bu komutu '--no-wait' parametresiyle çalıştırırsanız herhangi bir geri bildirim veya çıktı görmezsiniz. '--no-wait' parametresi, ağ geçidinin arka planda oluşturulmasına olanak tanır. VPN ağ geçidi oluşturma işleminin hemen tamamlandığı anlamına gelmez. Bir ağ geçidinin oluşturulması, kullandığınız ağ geçidi SKU’suna bağlı olarak 45 dakika veya daha uzun sürebilir.

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
4. Ağ geçidi alt ağını oluşturun.

  ```azurecli
   az network vnet subnet create --vnet-name TestVNet4 -n GatewaySubnet -g TestRG4 --address-prefix 10.42.255.0/27
  ```
5. Bir Genel IP adresi isteyin.

  ```azurecli
  az network public-ip create -n VNet4GWIP -g TestRG4 --allocation-method Dynamic
  ```
6. TestVNet4 sanal ağ geçidini oluşturun.

  ```azurecli
  az network vnet-gateway create -n VNet4GW -l westus --public-ip-address VNet4GWIP -g TestRG4 --vnet TestVNet4 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="createconnect"></a>4. Adım - Bağlantıları oluşturma

Artık VPN ağ geçitleri olan iki sanal ağınız var. Bir sonraki adım, sanal ağın ağ geçitleri arasındaki VPN ağ geçidi bağlantılarını oluşturmaya yöneliktir. Yukarıdaki örnekleri kullandıysanız, VNet ağ geçitleriniz farklı kaynak gruplarındadır. Ağ geçitleri farklı kaynak gruplarında olduğunda, bir bağlantı oluşturduğunuz sırada her ağ geçidinin kaynak kimliklerini tanımlamanız ve belirtmeniz gerekir. VNet’leriniz aynı kaynak grubundaysa, kaynak kimliklerini belirtmeniz gerekmeyeceğinden [ikinci yönerge kümesini](#samerg) kullanabilirsiniz.

### <a name="diffrg"></a>Farklı kaynak gruplarında bulunan VNet’leri bağlamak için

1. Aşağıdaki komutun çıktısından VNet1GW öğesinin Kaynak Kimliğini alın:

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  Çıktıda "id:" satırını bulun. Bir sonraki bölümde bağlantıyı oluşturmak için tırnak içindeki değerler gerekir. Bağlantınızı oluştururken kolayca yapıştırabilmek için bu değerleri Notepad gibi bir metin düzenleyicisine kopyalayın.

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

  **"id":** ifadesinden sonra gelen tırnak içindeki değerleri kopyalayın.

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
 ```

2. VNet4GW öğesinin Kaynak Kimliğini alın ve değerleri bir metin düzenleyicisine kopyalayın.

  ```azurecli
  az network vnet-gateway show -n VNet4GW -g TestRG4
  ```

3. TestVNet1 - TestVNet4 bağlantısını oluşturun. Bu adımda TestVNet1 - TestVNet4 arasında bağlantı oluşturursunuz. Örneklerde sözü geçen bir paylaşılan anahtar vardır. Paylaşılan anahtar için kendi değerlerinizi kullanabilirsiniz. Paylaşılan anahtarın her iki bağlantıyla da eşleşiyor olması önemlidir. Bağlantı oluşturma işleminin tamamlanması biraz zaman alır.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW 
  ```
4. TestVNet4 - TestVNet1 bağlantısı oluşturun. Bu adım, bağlantıyı TestVNet4’ten TestVNet1’e yönüne kuracak olmanız dışında yukarıdaki adımla aynıdır. Paylaşılan anahtarların eşleştiğinden emin olun. Bağlantının kurulması birkaç dakika sürer.

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG4 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG4/providers/Microsoft.Network/virtualNetworkGateways/VNet4GW -l westus --shared-key "aabbcc" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1G
  ```
5. Bağlantılarınızı doğrulayın. Bkz. [Bağlantınızı doğrulama](#verify).

### <a name="samerg"></a>Aynı kaynak grubunda bulunan VNet’leri bağlamak için

1. TestVNet1 - TestVNet4 bağlantısını oluşturun. Bu adımda TestVNet1 - TestVNet4 arasında bağlantı oluşturursunuz. Örneklerdeki kaynak gruplarının aynı olduğuna dikkat edin. Örneklerde paylaşılan bir anahtardan söz edildiğini de göreceksiniz. Paylaşılan anahtar için kendi değerlerinizi kullanabilirsiniz, ancak her iki bağlantı için de paylaşılan anahtarın eşleşmesi gerekir. Bağlantı oluşturma işleminin tamamlanması biraz zaman alır.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet4 -g TestRG1 --vnet-gateway1 VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet4GW
  ```
2. TestVNet4 - TestVNet1 bağlantısı oluşturun. Bu adım, bağlantıyı TestVNet4’ten TestVNet1’e yönüne kuracak olmanız dışında yukarıdaki adımla aynıdır. Paylaşılan anahtarların eşleştiğinden emin olun. Bağlantının kurulması birkaç dakika sürer.

  ```azurecli
  az network vpn-connection create -n VNet4ToVNet1 -g TestRG1 --vnet-gateway1 VNet4GW -l eastus --shared-key "eeffgg" --vnet-gateway2 VNet1GW
  ```
3. Bağlantılarınızı doğrulayın. Bkz. [Bağlantınızı doğrulama](#verify).

## <a name="difsub"></a>Farklı aboneliklerdeki VNet'leri bağlama

![v2v diyagramı](./media/vpn-gateway-howto-vnet-vnet-cli/v2vdiffsub.png)

Bu senaryoda TestVNet1 ve TestVNet5 bağlanır. VNet’ler farklı aboneliklerde yer alır. Aboneliklerin aynı Active Directory kiracısıyla ilişkilendirilmiş olması gerekmez. Bu yapılandırmanın adımları TestVNet1’i TestVNet5’e bağlamak için Sanal Ağdan Sanal Ağa bir bağlantı daha ekler.

### <a name="TestVNet1diff"></a>5. Adım - TestVNet1’i oluşturma ve yapılandırma

Bu yönergeler, önceki bölümlerde yer alan adımların devamıdır. TestVNet1 için TestVNet1 ve VPN ağ geçidini oluşturup yapılandırmak için [1. Adımı](#Connect) ve [2. Adımı](#TestVNet1) tamamlamalısınız.  Bu yapılandırma için önceki bölümdeki TestVNet4’ü oluşturmanız gerekmez, ancak oluşturursanız bu adımlarla çakışmaz. 1. ve 2. Adımı tamamladıktan sonra 6. Adıma (aşağıda) geçin.

### <a name="verifyranges"></a>6. Adım - IP adresi aralıklarını doğrulama

Ek bağlantılar oluşturulduğu sırada, yeni sanal ağın IP adresi alanının kendi Sanal Ağ aralıklarınız veya yerel ağ geçidi aralıkları ile çakışmadığını doğrulayın. Bu alıştırmada TestVNet5 için aşağıdaki değerleri kullanabilirsiniz:

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

Bu adım, yeni abonelik (5. Abonelik) bağlamında tamamlanmalıdır. Bu kısım, aboneliğin sahibi olan farklı bir kuruluşun yöneticisi tarafından tamamlanabilir. Abonelikler arasında geçiş yapmak için 'az account list --all' komutunu kullanarak hesabınızda kullanılabilen tüm abonelikleri listeleyin ve ardından 'az account set --subscription <subscriptionID>' komutuyla kullanmak istediğiniz aboneliğe geçin.

1. 5. Aboneliğe bağlı olduğunuzdan emin olun ve bir kaynak grubu oluşturun.

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

4. Ağ geçidi alt ağını ekleyin.

  ```azurecli
  az network vnet subnet create --vnet-name TestVNet5 -n GatewaySubnet -g TestRG5 --address-prefix 10.52.255.0/27
  ```

5. Genel bir IP adresi isteyin.

  ```azurecli
  az network public-ip create -n VNet5GWIP -g TestRG5 --allocation-method Dynamic
  ```
6. TestVNet5 ağ geçidini oluşturma

  ```azurecli
  az network vnet-gateway create -n VNet5GW -l japaneast --public-ip-address VNet5GWIP -g TestRG5 --vnet TestVNet5 --gateway-type Vpn --sku VpnGw1 --vpn-type RouteBased --no-wait
  ```

### <a name="connections5"></a>8. Adım - Bağlantıları oluşturma

Bu örnekteki ağ geçitleri farklı aboneliklerde olduğundan, bu adımı **[1. Abonelik]** ve **[5. Abonelik]** olarak işaretlenen iki CLI oturumuna ayırdık. Abonelikler arasında geçiş yapmak için 'az account list --all' komutunu kullanarak hesabınızda kullanılabilen tüm abonelikleri listeleyin ve ardından 'az account set --subscription <subscriptionID>' komutuyla kullanmak istediğiniz aboneliğe geçin.

1. **[1. Abonelik]** Oturum açın ve 1. Aboneliğe bağlanın. Çıktıdan Ağ Geçidinin adını ve kimliğini almak için şu komutu çalıştırın:

  ```azurecli
  az network vnet-gateway show -n VNet1GW -g TestRG1
  ```

  "id:" çıktısını kopyalayın. VNet ağ geçidinin (VNet1GW) kimliğini ve adını e-postayla veya başka bir yolla 5. Aboneliğin yöneticisine gönderin.

  Örnek çıktı:

  ```
  "id": "/subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW"
  ```

2. **[5. Abonelik]** Oturum açın ve 5. Aboneliğe bağlanın. Çıktıdan Ağ Geçidinin adını ve kimliğini almak için şu komutu çalıştırın:

  ```azurecli
  az network vnet-gateway show -n VNet5GW -g TestRG5
  ```

  "id:" çıktısını kopyalayın. VNet ağ geçidinin (VNet5GW) kimliğini ve adını e-postayla veya başka bir yolla 1. Aboneliğin yöneticisine gönderin.

3. **[1. Abonelik]** Bu adımda TestVNet1 ile TestVNet5 arasında bağlantı oluşturursunuz. Paylaşılan anahtar için kendi değerlerinizi kullanabilirsiniz, ancak her iki bağlantı için de paylaşılan anahtarın eşleşmesi gerekir. Bir bağlantı oluşturmak çok zaman almaz. 1 Abonelik’e bağlandığınızdan emin olun.

  ```azurecli
  az network vpn-connection create -n VNet1ToVNet5 -g TestRG1 --vnet-gateway1 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW -l eastus --shared-key "eeffgg" --vnet-gateway2 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW
  ```

4. **[5. Abonelik]** Bu adım, bağlantıyı TestVNet5’ten TestVNet1’e doğru kuracak olmanızın dışında yukarıdaki adımla aynıdır. Paylaşılan anahtarların eşleştiğinden ve 5. Aboneliğe bağlandığınızdan emin olun.

  ```azurecli
  az network vpn-connection create -n VNet5ToVNet1 -g TestRG5 --vnet-gateway1 /subscriptions/e7e33b39-fe28-4822-b65c-a4db8bbff7cb/resourceGroups/TestRG5/providers/Microsoft.Network/virtualNetworkGateways/VNet5GW -l japaneast --shared-key "eeffgg" --vnet-gateway2 /subscriptions/d6ff83d6-713d-41f6-a025-5eb76334fda9/resourceGroups/TestRG1/providers/Microsoft.Network/virtualNetworkGateways/VNet1GW
  ```

## <a name="verify"></a>Bağlantıları doğrulama
[!INCLUDE [vpn-gateway-no-nsg-include](../../includes/vpn-gateway-no-nsg-include.md)]

[!INCLUDE [verify connections v2v cli](../../includes/vpn-gateway-verify-connection-cli-rm-include.md)]

## <a name="faq"></a>Sanal ağlar arası bağlantılar hakkında SSS
[!INCLUDE [vpn-gateway-vnet-vnet-faq](../../includes/vpn-gateway-faq-vnet-vnet-include.md)]

## <a name="next-steps"></a>Sonraki adımlar

* Bağlantınız tamamlandıktan sonra sanal ağlarınıza sanal makineler ekleyebilirsiniz. Daha fazla bilgi edinmek için bkz. [Sanal Makineler ile ilgili belgeler](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).
* BGP hakkında bilgi edinmek için [BGP’ye Genel Bakış](vpn-gateway-bgp-overview.md) ve [BGP’yi yapılandırma](vpn-gateway-bgp-resource-manager-ps.md) makalelerine bakın.
