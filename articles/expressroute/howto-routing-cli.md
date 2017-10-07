---
title: "Nasıl tooconfigure bir Azure expressroute bağlantı hattı için yönlendirmeyi: CLI | Microsoft Docs"
description: "Bu makalede, oluşturma ve hello özel, genel ve Microsoft eşleme bir expressroute bağlantı hattı sağlama yardımcı olur. Bu makalede ayrıca nasıl toocheck hello durumu, güncelleştirme veya bağlantı hattınız için eşlemeleri silme gösterilmektedir."
documentationcenter: na
services: expressroute
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/31/2017
ms.author: anzaman,cherylmc
ms.openlocfilehash: 33130af050045527cdb316e77821c6d101b6a82a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-routing-for-an-expressroute-circuit-using-cli"></a>Oluşturma ve CLI kullanarak bir expressroute bağlantı hattı için yönlendirmeyi değiştirme

Bu makale, CLI kullanarak hello Resource Manager dağıtım modelinde bir expressroute bağlantı hattı için yönlendirme yapılandırması oluşturma ve yönetme yardımcı olur. Ayrıca, hello durumu, güncelleştirme veya silme denetleyin ve bir expressroute bağlantı hattı için eşlemeler sağlamayı sonlandırın. Bağlantı hattınız ile toouse farklı yöntem toowork istiyorsanız, bir makale listesi aşağıdaki hello seçin:

> [!div class="op_single_selector"]
> * [Azure portal](expressroute-howto-routing-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-routing-arm.md)
> * [Azure CLI](howto-routing-cli.md)
> * [Video - özel eşliği](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-private-peering-for-your-expressroute-circuit)
> * [Video - ortak eşleme](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-azure-public-peering-for-your-expressroute-circuit)
> * [Video - Microsoft eşlemesi](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-set-up-microsoft-peering-for-your-expressroute-circuit)
> * [PowerShell (klasik)](expressroute-howto-routing-classic.md)
> 

## <a name="configuration-prerequisites"></a>Yapılandırma önkoşulları

* Başlamadan önce hello hello CLI komutları (2.0 veya üstü) en son sürümünü yükleyin. Merhaba CLI komutları yükleme hakkında daha fazla bilgi için bkz: [Azure CLI 2.0 yükleme](/cli/azure/install-azure-cli).
* Merhaba gözden geçirdiğinizden emin olun [Önkoşullar](expressroute-prerequisites.md), [yönlendirme gereksinimleri](expressroute-routing.md), ve [iş akışı](expressroute-workflows.md) yapılandırmaya başlamadan önce sayfaları.
* Etkin bir ExpressRoute bağlantı hattınızın olması gerekir. Çok olarak Hello yönergeleri[bir expressroute bağlantı hattı oluşturma](howto-circuit-cli.md) ve devam etmeden önce bağlantı sağlayıcınız tarafından etkinleştirilen hello hattı sahip. Merhaba expressroute bağlantı hattı, bu makaledeki toobe mümkün toorun hello komutları için sağlanmış ve etkin durumda olması gerekir.

Bu yönergeler yalnızca Katman 2 bağlantı hizmetleri sunan hizmet sağlayıcıları ile oluşturulan toocircuits geçerlidir. Yönetilen sunan bir hizmet sağlayıcısı kullanıyorsanız, Katman 3 Hizmetleri (genellikle gibi bir IPVPN MPLS), bağlantı sağlayıcınız yapılandırmak ve yönetmek için yönlendirme.

Bir, iki veya üç eşlemenin tamamını (Azure özel, Azure genel ve Microsoft) bir expressroute bağlantı hattı için yapılandırabilirsiniz. Eşlemeleri seçtiğiniz herhangi bir sırayla yapılandırabilirsiniz. Bununla birlikte, her eşleme birer birer başlangıç yapılandırmasını tamamlayın emin olmanız gerekir.

## <a name="azure-private-peering"></a>Azure özel eşlemesi

Bu bölümde, oluşturma, alma, güncelleştirme ve hello bir expressroute bağlantı hattı için Azure özel eşleme yapılandırmasını silme yardımcı olur.

### <a name="toocreate-azure-private-peering"></a>Azure özel eşleme toocreate

1. Azure CLI Hello en son sürümünü yükleyin. Merhaba hello Azure komut satırı arabirimi (CLI) en son sürümünü kullanmanız gerekir. * gözden geçirme hello [Önkoşullar](expressroute-prerequisites.md) ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.

  ```azurecli
  az login
  ```

  Toocreate expressroute bağlantı hattı hello aboneliği seçin

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. ExpressRoute bağlantı hattı oluşturun. Merhaba yönergeleri toocreate izleyin bir [expressroute bağlantı hattı](howto-circuit-cli.md) ve hello bağlantı sağlayıcı tarafından sağlanan sahip.

  Bağlantı sağlayıcınız yönetilen Katman 3 Hizmetleri sunuyorsa, bağlantı sağlayıcısı tooenable Azure sizin için eşlemeyi özel isteyebilir. Bu durumda, hello sonraki bölümlerde listelenen toofollow yönergeleri gerekmez. Ancak, bağlantı sağlayıcınız yönlendirmeyi sizin için hattınızı oluşturduktan sonra yönetmiyorsa yapılandırmanızı hello sonraki adımları kullanarak devam edin.
3. Merhaba ExpressRoute bağlantı hattı toomake sağlanan ve ayrıca etkin olduğundan emin olun. Aşağıdaki örnek hello kullan:

  ```azurecli
  az network express-route show --resource-group ExpressRouteResourceGroup --name MyCircuit
  ```

  Merhaba yanıt benzer toohello örneği aşağıdaki gibidir:

  ```azurecli
  "allowClassicOperations": false,
  "authorizations": [],
  "circuitProvisioningState": "Enabled",
  "etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
  "gatewayManagerEtag": null,
  "id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
  "location": "westus",
  "name": "MyCircuit",
  "peerings": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
  "serviceProviderNotes": null,
  "serviceProviderProperties": {
  "bandwidthInMbps": 200,
  "peeringLocation": "Silicon Valley",
  "serviceProviderName": "Equinix"
  },
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. Merhaba bağlantı hattı için Azure özel eşlemesini yapılandırın. Merhaba sonraki adımlara devam etmeden önce aşağıdaki öğelerindeki hello sahip olduğunuzdan emin olun:

  * Bir/30 alt ağı hello birincil bağlantı için. Merhaba alt ağ, sanal ağlar için ayrılmış herhangi bir adres alanının parçası olmamalıdır.
  * Bir/30 alt ağı hello ikincil bağlantı için. Merhaba alt ağ, sanal ağlar için ayrılmış herhangi bir adres alanının parçası olmamalıdır.
  * Geçerli bir VLAN kimliği tooestablish bu eşlemenin. Hiçbir diğer eşliği emin hello devredeki aynı VLAN kimliğini kullanan hello
  * Eşleme için AS numarası. 2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz. Bu eşleme için özel bir AS numarası kullanabilirsiniz. 65515’i kullanmadığınızdan emin olun.
  * **İsteğe bağlı -** toouse birini seçerseniz bir MD5 karma değeri.

  Aşağıdaki örnek tooconfigure Azure hattınız için eşlemesini özel hello kullan:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering
  ```

  Bir MD5 karma değeri toouse seçerseniz, aşağıdaki örneğine hello kullan:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 10.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 10.0.0.4/30 --vlan-id 200 --peering-type AzurePrivatePeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > AS numaranızı müşteri ASN’si değil eşleme ASN’si olarak belirttiğinizden emin olun.
  > 
  > 

### <a name="tooview-azure-private-peering-details"></a>tooview Azure özel eşleme ayrıntıları

Aşağıdaki örnek hello kullanarak yapılandırma ayrıntılarını alabilirsiniz:

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

Merhaba, benzer toohello aşağıdaki örneğine çıktı:

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePrivatePeering",
  "ipv6PeeringConfig": null,
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePrivatePeering",
  "peerAsn": 7671,
  "peeringType": "AzurePrivatePeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-private-peering-configuration"></a>Azure özel eşleme yapılandırmasını tooupdate

Aşağıdaki örneğine hello kullanarak hello yapılandırmasını herhangi bir bölümünü güncelleştirebilirsiniz. Bu örnekte, hello hello hattının VLAN kimliği 100 too500 güncelleştiriliyor.

```azurecli
az network express-route peering update --vlan-id 500 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

### <a name="toodelete-azure-private-peering"></a>Azure özel eşleme toodelete

Aşağıdaki örnek hello çalıştırarak eşleme yapılandırmanızı kaldırabilirsiniz:

> [!WARNING]
> Bu örneği çalıştırmadan önce tüm sanal ağları expressroute bağlantı hattı hello bağlantısız olduğundan emin olmalısınız. 
> 
> 

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePrivatePeering
```

## <a name="azure-public-peering"></a>Azure ortak eşleme

Bu bölümde, oluşturma, alma, güncelleştirme ve hello bir expressroute bağlantı hattı için Azure ortak eşleme yapılandırmasını silme yardımcı olur.

### <a name="toocreate-azure-public-peering"></a>Azure ortak eşleme toocreate

1. Azure CLI Hello en son sürümünü yükleyin. Merhaba hello Azure komut satırı arabirimi (CLI) en son sürümünü kullanmanız gerekir. * gözden geçirme hello [Önkoşullar](expressroute-prerequisites.md) ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.

  ```azurecli
  az login
  ```

  Toocreate expressroute bağlantı hattı istediğiniz hello aboneliği seçin.

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. ExpressRoute bağlantı hattı oluşturun.  Merhaba yönergeleri toocreate izleyin bir [expressroute bağlantı hattı](howto-circuit-cli.md) ve hello bağlantı sağlayıcı tarafından sağlanan sahip.

  Bağlantı sağlayıcınız yönetilen Katman 3 Hizmetleri sunuyorsa, bağlantı sağlayıcınız özel sizin için Azure eşlemeyi sağlar isteyebilir. Bu durumda, hello sonraki bölümlerde listelenen toofollow yönergeleri gerekmez. Ancak, bağlantı sağlayıcınız yönlendirmeyi sizin için hattınızı oluşturduktan sonra yönetmiyorsa yapılandırmanızı hello sonraki adımları kullanarak devam edin.
3. Sağlanan ve ayrıca etkin hello ExpressRoute bağlantı hattı tooensure denetleyin. Aşağıdaki örnek hello kullan:

  ```azurecli
  az network express-route list
  ```

  Merhaba yanıt benzer toohello örneği aşağıdaki gibidir:

  ```azurecli
  "allowClassicOperations": false,
  "authorizations": [],
  "circuitProvisioningState": "Enabled",
  "etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
  "gatewayManagerEtag": null,
  "id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
  "location": "westus",
  "name": "MyCircuit",
  "peerings": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
  "serviceProviderNotes": null,
  "serviceProviderProperties": {
    "bandwidthInMbps": 200,
    "peeringLocation": "Silicon Valley",
    "serviceProviderName": "Equinix"
  },
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. Merhaba bağlantı hattı için Azure ortak eşlemesini yapılandırın. Devam etmeden önce aşağıdaki bilgilerle hello sahip olduğunuzdan emin olun.

  * Bir/30 alt ağı hello birincil bağlantı için. Bu geçerli bir ortak IPv4 öneki olmalıdır.
  * Bir/30 alt ağı hello ikincil bağlantı için. Bu geçerli bir ortak IPv4 öneki olmalıdır.
  * Geçerli bir VLAN kimliği tooestablish bu eşlemenin. Hiçbir diğer eşliği emin hello devredeki aynı VLAN kimliğini kullanan hello
  * Eşleme için AS numarası. 2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz.
  * **İsteğe bağlı -** toouse birini seçerseniz bir MD5 karma değeri.

  Aşağıdaki örnek tooconfigure Azure hattınız için eşlemesini genel hello çalıştırın:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering
  ```

  Bir MD5 karma değeri toouse seçerseniz, aşağıdaki örneğine hello kullan:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 12.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 12.0.0.4/30 --vlan-id 200 --peering-type AzurePublicPeering --SharedKey "A1B2C3D4"
  ```

  > [!IMPORTANT]
  > AS numaranızı müşteri ASN’si değil eşleme ASN’si olarak belirttiğinizden emin olun.

### <a name="tooview-azure-public-peering-details"></a>tooview Azure genel eşliği ayrıntıları

Aşağıdaki örnek hello kullanarak yapılandırma ayrıntılarını alabilirsiniz:

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

Merhaba, benzer toohello aşağıdaki örneğine çıktı:

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzurePublicPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": null,
  "name": "AzurePublicPeering",
  "peerAsn": 7671,
  "peeringType": "AzurePublicPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-azure-public-peering-configuration"></a>Azure ortak eşleme yapılandırmasını tooupdate

Aşağıdaki örneğine hello kullanarak hello yapılandırmasını herhangi bir bölümünü güncelleştirebilirsiniz. Bu örnekte, hello hello hattının VLAN kimliği 200 too600 güncelleştiriliyor.

```azurecli
az network express-route peering update --vlan-id 600 -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

### <a name="toodelete-azure-public-peering"></a>Azure ortak eşleme toodelete

Aşağıdaki örnek hello çalıştırarak eşleme yapılandırmanızı kaldırabilirsiniz:

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzurePublicPeering
```

## <a name="microsoft-peering"></a>Microsoft eşlemesi

Bu bölümde, oluşturma, alma, güncelleştirme ve bir expressroute bağlantı hattı için Microsoft eşleme yapılandırmasını hello silme yardımcı olur.

> [!IMPORTANT]
> Önceki tooAugust 1 yapılandırılmış olan ExpressRoute bağlantı hatları Microsoft eşliği, yol filtreleri tanımlanmamış olsa bile 2017 hello Microsoft eşleme aracılığıyla tanıtılan tüm hizmet ön eklerin sahip olur. Ve 1 Ağustos 2017 sonrasında yapılandırılmış ExpressRoute bağlantı hatları, Microsoft eşlemesi sahip olmaz tüm ön eklerin rota filtre bağlanana kadar tanıtılan toohello hattı. Daha fazla bilgi için bkz: [Microsoft eşliği için rota filtresini Yapılandır](how-to-routefilter-powershell.md).
> 
> 

### <a name="toocreate-microsoft-peering"></a>toocreate Microsoft eşlemesi

1. Azure CLI Hello en son sürümünü yükleyin. Merhaba en son sürümünü kullanın hello Azure komut satırı arabirimi (CLI). * gözden geçirme hello [Önkoşullar](expressroute-prerequisites.md) ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.

  ```azurecli
  az login
  ```

  Toocreate expressroute bağlantı hattı istediğiniz hello aboneliği seçin.

  ```azurecli
  az account set --subscription "<subscription ID>"
  ```
2. ExpressRoute bağlantı hattı oluşturun. Merhaba yönergeleri toocreate izleyin bir [expressroute bağlantı hattı](howto-circuit-cli.md) ve hello bağlantı sağlayıcı tarafından sağlanan sahip.

  Bağlantı sağlayıcınız yönetilen Katman 3 Hizmetleri sunuyorsa, bağlantı sağlayıcısı tooenable Azure sizin için eşlemeyi özel isteyebilir. Bu durumda, hello sonraki bölümlerde listelenen toofollow yönergeleri gerekmez. Ancak, bağlantı sağlayıcınız yönlendirmeyi sizin için hattınızı oluşturduktan sonra yönetmiyorsa yapılandırmanızı hello sonraki adımları kullanarak devam edin.

3. Merhaba ExpressRoute bağlantı hattı toomake sağlanan ve ayrıca etkin olduğundan emin olun. Aşağıdaki örnek hello kullan:

  ```azurecli
  az network express-route list
  ```

  Merhaba yanıt benzer toohello örneği aşağıdaki gibidir:

  ```azurecli
  "allowClassicOperations": false,
  "authorizations": [],
  "circuitProvisioningState": "Enabled",
  "etag": "W/\"1262c492-ffef-4a63-95a8-a6002736b8c4\"",
  "gatewayManagerEtag": null,
  "id": "/subscriptions/81ab786c-56eb-4a4d-bb5f-f60329772466/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit",
  "location": "westus",
  "name": "MyCircuit",
  "peerings": [],
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "serviceKey": "1d05cf70-1db5-419f-ad86-1ca62c3c125b",
  "serviceProviderNotes": null,
  "serviceProviderProperties": {
    "bandwidthInMbps": 200,
    "peeringLocation": "Silicon Valley",
    "serviceProviderName": "Equinix"
  },
  "serviceProviderProvisioningState": "Provisioned",
  "sku": {
    "family": "UnlimitedData",
    "name": "Standard_MeteredData",
    "tier": "Standard"
  },
  "tags": null,
  "type": "Microsoft.Network/expressRouteCircuits]
  ```

4. Microsoft Hello bağlantı hattı için eşlemesini yapılandırın. Devam etmeden önce bilgilerini aşağıdaki hello sahip olduğunuzdan emin olun.

  * Bir/30 alt ağı hello birincil bağlantı için. Bu size ait ve bir RIR / IRR içinde kayıtlı bir geçerli ortak IPv4 ön eki olmalıdır.
  * Bir/30 alt ağı hello ikincil bağlantı için. Bu size ait ve bir RIR / IRR içinde kayıtlı bir geçerli ortak IPv4 ön eki olmalıdır.
  * Geçerli bir VLAN kimliği tooestablish bu eşlemenin. Hiçbir diğer eşliği emin hello devredeki aynı VLAN kimliğini kullanan hello
  * Eşleme için AS numarası. 2 bayt ve 4 bayt AS numaralarını kullanabilirsiniz.
  * Tanıtılan önekler: listesini sağlamanız gerekir tüm ön eklerin hello BGP oturumu üzerinden tooadvertise planlayın. Yalnızca ortak IP adresi ön ekleri kabul edilir. Toosend ön ek kümesi planlıyorsanız, virgülle ayrılmış bir liste gönderebilirsiniz. Bu ön eklerin bir RIR içinde kayıtlı tooyou olmalıdır / IRR.
  * **İsteğe bağlı -** müşteri ASN'si: eşleme AS numarasına kayıtlı toohello olmayan önekler Tanıtıyorsanız, kayıtlı oldukları numara toowhich hello belirtebilirsiniz.
  * Yönlendirme kayıt defteri adı: Merhaba RIR belirtebilirsiniz / hangi hello karşı AS numarası ve önekleri IRR kayıtlı.
  * **İsteğe bağlı -** toouse birini seçerseniz bir MD5 karma değeri.

   Aşağıdaki örnek tooconfigure hattınız için Microsoft eşlemesini hello çalıştırın:

  ```azurecli
  az network express-route peering create --circuit-name MyCircuit --peer-asn 100 --primary-peer-subnet 123.0.0.0/30 -g ExpressRouteResourceGroup --secondary-peer-subnet 123.0.0.4/30 --vlan-id 300 --peering-type MicrosoftPeering --advertised-public-prefixes 123.1.0.0/24
  ```

### <a name="tooget-microsoft-peering-details"></a>tooget Microsoft eşleme ayrıntıları

Aşağıdaki örnek hello kullanarak yapılandırma ayrıntılarını alabilirsiniz:

```azurecli
az network express-route peering show -g ExpressRouteResourceGroup --circuit-name MyCircuit --name AzureMicrosoftPeering
```

Merhaba, benzer toohello aşağıdaki örneğine çıktı:

```azurecli
{
  "azureAsn": 12076,
  "etag": "W/\"2e97be83-a684-4f29-bf3c-96191e270666\"",
  "gatewayManagerEtag": "18",
  "id": "/subscriptions/9a0c2943-e0c2-4608-876c-e0ddffd1211b/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/MyCircuit/peerings/AzureMicrosoftPeering",
  "lastModifiedBy": "Customer",
  "microsoftPeeringConfig": {
    "advertisedPublicPrefixes": [
        ""
      ],
     "advertisedPublicPrefixesState": "",
     "customerASN": ,
     "routingRegistryName": ""
  }
  "name": "AzureMicrosoftPeering",
  "peerAsn": ,
  "peeringType": "AzureMicrosoftPeering",
  "primaryAzurePort": "",
  "primaryPeerAddressPrefix": "",
  "provisioningState": "Succeeded",
  "resourceGroup": "ExpressRouteResourceGroup",
  "routeFilter": null,
  "secondaryAzurePort": "",
  "secondaryPeerAddressPrefix": "",
  "sharedKey": null,
  "state": "Enabled",
  "stats": null,
  "vlanId": 100
}
```

### <a name="tooupdate-microsoft-peering-configuration"></a>tooupdate Microsoft eşleme yapılandırması

Merhaba yapılandırma herhangi bir bölümünü güncelleştirebilirsiniz. Hello öneklerini hello devrenin aşağıdaki örneğine hello içinde 123.1.0.0/24 too124.1.0.0/24 gelen güncelleştirilmekte olan tanıtılan:

```azurecli
az network express-route peering update --circuit-name MyCircuit -g ExpressRouteResourceGroup --peering-type MicrosoftPeering --advertised-public-prefixes 124.1.0.0/24
```

### <a name="toodelete-microsoft-peering"></a>toodelete Microsoft eşlemesi

Aşağıdaki örnek hello çalıştırarak eşleme yapılandırmanızı kaldırabilirsiniz:

```azurecli
az network express-route peering delete -g ExpressRouteResourceGroup --circuit-name MyCircuit --name MicrosoftPeering
```

## <a name="next-steps"></a>Sonraki adımlar

Sonraki adım, [VNet tooan expressroute bağlantı hattı bağlantı](howto-linkvnet-cli.md).

* ExpressRoute iş akışları hakkında daha fazla bilgi için bkz. [ExpressRoute iş akışları](expressroute-workflows.md).
* Bağlantı hattı eşlemesi hakkında daha fazla bilgi için bkz. [ExpressRoute bağlantı hattı ve yönlendirme etki alanları](expressroute-circuit-peerings.md).
* Sanal ağlarla çalışma hakkında daha fazla bilgi için bkz. [Sanal ağa genel bakış](../virtual-network/virtual-networks-overview.md).