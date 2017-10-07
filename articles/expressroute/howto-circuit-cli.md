---
title: "Oluşturma ve bir Azure expressroute değiştirme: CLI | Microsoft Docs"
description: "Bu makalede nasıl toocreate, sağlama, doğrulayın, güncelleştirme, silme ve CLI kullanarak bir expressroute bağlantı hattı yetkisini kaldırma açıklanmaktadır."
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
ms.date: 07/25/2017
ms.author: anzaman;cherylmc
ms.openlocfilehash: 396e325658a59afadb209bb525cbb59ac775ae6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-cli"></a>Oluşturma ve CLI kullanarak bir expressroute bağlantı hattı değiştirme


Bu makalede nasıl toocreate kullanarak bir Azure expressroute bağlantı hattı hello komut satırı arabirimi (CLI) açıklanmaktadır. Bu makalede ayrıca, nasıl toocheck hello durumu, güncelleştirme veya silme ve bir bağlantı hattı yetkisini kaldırma gösterir. Toouse ExpressRoute bağlantı hatları ile farklı yöntem toowork istiyorsanız, liste aşağıdaki hello hello makale seçebilirsiniz:

> [!div class="op_single_selector"]
> * [Azure portal](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Azure CLI](howto-circuit-cli.md)
> * [Video - Azure portalı](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (klasik)](expressroute-howto-circuit-classic.md)
> 

## <a name="before-you-begin"></a>Başlamadan önce

* Başlamadan önce hello hello CLI komutları (2.0 veya üstü) en son sürümünü yükleyin. Merhaba CLI komutları yükleme hakkında daha fazla bilgi için bkz: [Azure CLI 2.0 yükleme](/cli/azure/install-azure-cli) ve [Azure CLI 2.0 ile çalışmaya başlama](/cli/azure/get-started-with-azure-cli).
* Gözden geçirme hello [Önkoşullar](expressroute-prerequisites.md) ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.

## <a name="create-and-provision-an-expressroute-circuit"></a>Oluşturma ve bir expressroute bağlantı hattı sağlama

### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a>1. Tooyour Azure hesabı oturum ve aboneliğinizi seçin

toobegin yapılandırmanıza, oturum açma tooyour Azure hesabı. Bağlandığınız örnekler toohelp aşağıdaki hello kullan:

```azurecli
az login
```

Merhaba hesabının Hello abonelikleri kontrol edin.

```azurecli
az account list
```

Bir expressroute bağlantı hattı toocreate istediğiniz hello aboneliği seçin.

```azurecli
az account set --subscription "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a>2. Desteklenen sağlayıcılar, konumları ve bant genişlikleri Hello listesini alma

Bir expressroute bağlantı hattı oluşturmadan önce desteklenen bağlantı sağlayıcıları, konumları ve bant genişliği seçenekleri hello listesi gerekir. Merhaba CLI komut 'az ağ hızlı rota listesi-service-providers', sonraki adımlarda kullanacağınız bu bilgiler verir:

```azurecli
az network express-route list-service-providers
```

Merhaba yanıt benzer toohello örneği aşağıdaki gibidir:

```azurecli
[
  {
    "bandwidthsOffered": [
      {
        "offerName": "50Mbps",
        "valueInMbps": 50
      },
      {
        "offerName": "100Mbps",
        "valueInMbps": 100
      },
      {
        "offerName": "200Mbps",
        "valueInMbps": 200
      },
      {
        "offerName": "500Mbps",
        "valueInMbps": 500
      },
      {
        "offerName": "1Gbps",
        "valueInMbps": 1000
      },
      {
        "offerName": "2Gbps",
        "valueInMbps": 2000
      },
      {
        "offerName": "5Gbps",
        "valueInMbps": 5000
      },
      {
        "offerName": "10Gbps",
        "valueInMbps": 10000
      }
    ],
    "id": "/subscriptions//resourceGroups//providers/Microsoft.Network/expressRouteServiceProviders/",
    "location": null,
    "name": "AARNet",
    "peeringLocations": [
      "Melbourne",
      "Sydney"
    ],
    "provisioningState": "Succeeded",
    "resourceGroup": "",
    "tags": null,
    "type": "Microsoft.Network/expressRouteServiceProviders"
  },
```

Bağlantı sağlayıcınız listeleniyorsa hello yanıt toosee denetleyin. Bir bağlantı hattı oluştururken ihtiyacınız olacak bilgileri, aşağıdaki hello not edin:

* Ad
* PeeringLocations
* BandwidthsOffered

Şimdi hazır toocreate bir expressroute bağlantı hattı olduğunuz.

### <a name="3-create-an-expressroute-circuit"></a>3. ExpressRoute bağlantı hattı oluşturma

> [!IMPORTANT]
> ExpressRoute bağlantı hattınız bir hizmet anahtarı verilen hello andan itibaren faturalandırılır. Merhaba bağlantı sağlayıcı hazır tooprovision hello hattı olduğunda bu işlemi gerçekleştirin.
> 
> 

Bir kaynak grubu zaten yoksa, expressroute bağlantı hattı oluşturmadan önce bir oluşturmanız gerekir. Bir kaynak grubu hello aşağıdaki komutu çalıştırarak oluşturabilirsiniz:

```azurecli
az group create -n ExpressRouteResourceGroup -l "West US"
```

Aşağıdaki örnek hello nasıl toocreate 200 MB/sn expressroute bağlantı hattı Silikon vadisi Equinix aracılığıyla gösterir. Farklı bir sağlayıcı ve farklı ayarlar kullanıyorsanız, bu bilgileri isteğiniz yaptığınızda değiştirin. 

Merhaba doğru SKU katmanı ve SKU ailesi belirttiğinizden emin olun:

* SKU katmanı, bir ExpressRoute standart ya da bir ExpressRoute premium Eklentisi etkin olup olmadığını belirler. 'Standart' tooget Merhaba standart SKU veya 'Premium' hello premium eklenti belirtebilirsiniz.
* SKU ailesi hello faturalama türü belirler. Ölçülen veri planı ve 'Unlimiteddata' için 'Metereddata' için bir sınırsız veri planı belirtebilirsiniz. 'Metereddata 'too'Unlimiteddata', ancak başlangıç türü 'Unlimiteddata' too'Metereddata değiştirilemez' hello fatura türünü değiştirebilirsiniz.


ExpressRoute bağlantı hattınız bir hizmet anahtarı verilen hello andan itibaren faturalandırılır. Yeni bir hizmet anahtarı için bir istek hello örneği aşağıdaki verilmiştir:

```azurecli
az network express-route create --bandwidth 200 -n MyCircuit --peering-location "Silicon Valley" -g ExpressRouteResourceGroup --provider "Equinix" -l "West US" --sku-family MeteredData --sku-tier Standard
```

Merhaba yanıt hello hizmet anahtarı içerir.

### <a name="4-list-all-expressroute-circuits"></a>4. Tüm ExpressRoute bağlantı hatları listesi

tooget, oluşturduğunuz tüm hello ExpressRoute bağlantı hatları listesini hello 'az ağ hızlı rota listesi' komutunu çalıştırın. Bu komutu kullanarak bu bilgileri dilediğiniz zaman alabilir. toolist tüm devreler hello parametresiz çağrısı yapın.

```azurecli
az network express-route list
```

Hizmet anahtarınız hello listelenen *ServiceKey* hello yanıtının alan.

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
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

Tüm hello parametrelerin ayrıntılı açıklamaları hello kullanarak çalışan hello komutu tarafından alabilirsiniz '-h' parametresi.

```azurecli
az network express-route list -h
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>5. Merhaba hizmet anahtar tooyour bağlantı sağlayıcı sağlamak için Gönder

'ServiceProviderProvisioningState' hello hizmet sağlayıcı tarafında sağlama hello geçerli durumu hakkında bilgi sağlar. Merhaba durum Microsoft yan hello üzerinde hello durumunu sağlar. Daha fazla bilgi için bkz: Merhaba [iş akışları makale](expressroute-workflows.md#expressroute-circuit-provisioning-states).

Yeni bir expressroute bağlantı hattı oluşturduğunuzda, hello devre durumunu izleyen hello oluşturulur.

```azurecli
"serviceProviderProvisioningState": "NotProvisioned"
"circuitProvisioningState": "Enabled"
```

Merhaba hattı hello bağlantı sağlayıcı için etkinleştirme işleminin hello olduğunda durumu aşağıdaki toohello değiştirir:

```azurecli
"serviceProviderProvisioningState": "Provisioning"
"circuitProvisioningState": "Enabled"
```

Toobe mümkün toouse için bir expressroute bağlantı hattı, durumu aşağıdaki hello olmalıdır:

```azurecli
"serviceProviderProvisioningState": "Provisioned"
"circuitProvisioningState": "Enabled
```

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>6. Merhaba durumunu ve hello hattı anahtar hello durumunu düzenli aralıklarla denetleyin

Merhaba durumu ve hello hattı anahtar hello durumunu denetleme, sağlayıcınız hattınız etkinleştirildiğinde bilmenizi sağlar. Merhaba hattı yapılandırıldıktan sonra 'ServiceProviderProvisioningState' 'Hazırlandı ' hello aşağıdaki örnekte gösterildiği gibi görünür:

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
"serviceProviderProvisioningState": "NotProvisioned",
"sku": {
  "family": "UnlimitedData",
  "name": "Standard_MeteredData",
  "tier": "Standard"
},
"tags": null,
"type": "Microsoft.Network/expressRouteCircuits]
```

### <a name="7-create-your-routing-configuration"></a>7. Yönlendirme yapılandırması oluşturma

Merhaba adım adım yönergeler için bkz: [expressroute bağlantı hattı yönlendirme yapılandırması](howto-routing-cli.md) makale toocreate ve hattı eşlemeler değiştirin.

> [!IMPORTANT]
> Bu yönergeler yalnızca Katman 2 bağlantı hizmetleri sunan hizmet sağlayıcıları ile oluşturulan toocircuits geçerlidir. Yönetilen sunan bir hizmet sağlayıcısı kullanıyorsanız, Katman 3 Hizmetleri (genellikle bir IP VPN, MPLS gibi), bağlantı sağlayıcınız yönlendirmeyi sizin için yönetir ve yapılandırır.
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a>8. Sanal ağ tooan expressroute bağlantı hattı bağlantı

Ardından, sanal ağ tooyour expressroute bağlantı hattı bağlayın. Kullanım hello [sanal bağlama ağları tooExpressRoute devreler](howto-linkvnet-cli.md) makalesi.

## <a name="modify"></a>Bir expressroute bağlantı hattı değiştirme

Bağlantı etkilemeden belirli bir expressroute bağlantı hattı özelliklerini değiştirebilirsiniz. Aşağıdaki değişiklikler kapalı kalma süresi olmadan hello yapabilirsiniz:

* Etkinleştirmek veya expressroute bağlantı hattı için ExpressRoute premium eklentisi devre dışı bırakın.
* Sağlanmış kapasite kullanılabilir hello bağlantı noktasında hello bant genişliği, expressroute bağlantı hattı artırabilir. Ancak, bir bağlantı hattının hello bant genişliği önceki sürüme indirme desteklenmiyor. 
* Ölçülen veri tooUnlimited veri hello ölçüm planı değiştirebilirsiniz. Ancak, veri desteklenmiyor sınırsız veri tooMetered planından ölçümü hello değiştirme.
* Etkinleştirme ve devre dışı *izin Klasik işlemleri*.

Merhaba sınırlar ve sınırlamalar hakkında daha fazla bilgi için bkz: [ExpressRoute SSS](expressroute-faqs.md).

### <a name="tooenable-hello-expressroute-premium-add-on"></a>tooenable hello ExpressRoute premium eklentisi

Hello aşağıdaki komutu kullanarak, varolan bağlantı hattınız için hello ExpressRoute premium eklentisi etkinleştirebilirsiniz:

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Premium
```

Merhaba hattı artık etkin hello ExpressRoute premium eklentisi özellikler sahiptir. Merhaba komutu başarıyla çalıştırıldı hemen için hello premium eklenti özelliğini faturalama başlayın.

### <a name="toodisable-hello-expressroute-premium-add-on"></a>toodisable hello ExpressRoute premium eklentisi

> [!IMPORTANT]
> Merhaba standart bağlantı hattı için izin daha büyük olan kaynaklar kullanıyorsanız, bu işlemi başarısız olabilir.
> 
> 

Merhaba ExpressRoute premium eklentisi'nı devre dışı bırakmadan önce aşağıdaki ölçütleri hello anlama:

* Premium toostandard düşürmek önce 10'dan az sanal ağlar bağlantılı toohello hattı sahip olduğunuzdan emin olmanız gerekir. Birden fazla 10 varsa, güncelleştirme isteği başarısız olur ve biz premium oranlarda fatura.
* Tüm sanal ağları diğer coğrafi bölgelerde bağlantısını gerekir. Tüm sanal ağları bağlantısını yok, güncelleştirme isteği başarısız olur ve biz premium oranlarda fatura.
* Yol tablosu özel eşleme için 4. 000'den az yolları olmalıdır. Rota tablosu boyutunuz 4.000 yolları büyükse, hello BGP oturumu bırakır. tanıtılan önekler Hello sayısı 4.000 kadar hello oturumu yeniden iler hale olmaz.

Aşağıdaki örneğine hello kullanarak hello ExpressRoute premium eklentisi hello varolan hattı için devre dışı bırakabilirsiniz:

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-tier Standard
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a>tooupdate hello ExpressRoute devresi bant genişliği

Merhaba denetimi sağlayıcınız için desteklenen hello bant genişliği seçenekleri için [ExpressRoute SSS](expressroute-faqs.md). Var olan bağlantı hattınız hello boyutundan büyük herhangi bir boyutta seçebilirsiniz.

> [!IMPORTANT]
> Merhaba varolan bağlantı noktasında yetersiz kapasite ise toorecreate hello expressroute bağlantı hattı olabilir. Varsa hiçbir ek kapasite kullanılabilir o konumda hello hattı yükseltemezsiniz.
>
> Bir expressroute bağlantı hattı kesintiye uğratmadan hello bant genişliği azaltma olamaz. Bant genişliği eski sürüme düşürmeyi, toodeprovision hello expressroute bağlantı hattı gerektirir ve yeni bir expressroute bağlantı hattı yeniden sağlayın.
>

Gereksinim duyduğunuz hello boyutu karar verdikten sonra komutu tooresize aşağıdaki hello hattınız kullanın:

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --bandwidth 1000
```

Bağlantı hattınız hello Microsoft tarafında boyutlandırılır. Ardından, bu değişikliği kendi yan toomatch, bağlantı sağlayıcısı tooupdate yapılandırmalarında başvurmanız gerekir. Bu bildirim yaptıktan sonra güncelleştirilmiş hello bant seçeneği için faturalama başlayın.

### <a name="toomove-hello-sku-from-metered-toounlimited"></a>ölçülen toounlimited gelen toomove hello SKU

Aşağıdaki örneğine hello kullanarak hello ExpressRoute devresi SKU'su değiştirebilirsiniz:

```azurecli
az network express-route update -n MyCircuit -g ExpressRouteResourceGroup --sku-family UnlimitedData
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a>toocontrol erişim toohello Klasik ve Resource Manager ortamları

Merhaba yönergeleri gözden [taşıma ExpressRoute bağlantı hatları hello Klasik toohello Resource Manager dağıtım modelinde](expressroute-howto-move-arm.md).

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Sağlamayı kaldırmayı ve bir expressroute bağlantı hattı silme

toodeprovision ve delete bir expressroute bağlantı hattı ölçütleri aşağıdaki hello anladığınızdan emin olun:

* Tüm sanal ağlardan hello expressroute bağlantı hattı bağlantısını gerekir. Bu işlem başarısız olursa, tüm sanal ağ olup olmadığını toosee toohello hattı bağlı denetleyin.
* Merhaba ExpressRoute bağlantı hattı Hizmet Sağlayıcısı sağlama durumu ise **sağlama** veya **hazırlandı**, kendi tarafında hizmet sağlayıcısı toodeprovision hello hattınız ile çalışmanız gerekir. Biz tooreserve kaynakları devam et ve hello hizmet sağlayıcısı sağlamayı hello hattı tamamlandıktan ve bize bildiren kadar sizi faturalandırmak.
* Merhaba hizmet sağlayıcısı hello hattı sağlaması kaldırılıyor. sağlaması hello hattı silebilirsiniz. Bir bağlantı hattı sağlaması kaldırılıyor. sağlaması durumlar hello Hizmet Sağlayıcısı sağlama durumu çok ayarlanır**sağlanmadı**. Merhaba hattı için fatura durdurur.

Hello aşağıdaki komutu çalıştırarak, expressroute bağlantı hattı silebilirsiniz:

```azurecli
az network express-route delete  -n MyCircuit -g ExpressRouteResourceGroup
```

## <a name="next-steps"></a>Sonraki adımlar

Bağlantı hattınız oluşturduktan sonra görevleri hello emin olun:

* [Oluşturma ve expressroute bağlantı hattı için yönlendirmeyi değiştirme](howto-routing-cli.md)
* [Sanal ağ tooyour expressroute bağlantı hattı bağlantı](howto-linkvnet-cli.md)
