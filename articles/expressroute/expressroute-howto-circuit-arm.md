---
title: "Oluşturma ve bir expressroute bağlantı hattı değiştirme: PowerShell: Azure Resource Manager | Microsoft Docs"
description: "Bu makalede nasıl toocreate, sağlama, doğrulayın, güncelleştirme, silme ve bir expressroute bağlantı hattı yetkisini kaldırma açıklanmaktadır."
documentationcenter: na
services: expressroute
author: ganesr
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f997182e-9b25-4a7a-b079-b004221dadcc
ms.service: expressroute
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 8d76c577a9cffdd393abac1b76cccc27d92e9e62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-modify-an-expressroute-circuit-using-powershell"></a>Oluşturma ve PowerShell kullanarak bir expressroute bağlantı hattı değiştirme
> [!div class="op_single_selector"]
> * [Azure portal](expressroute-howto-circuit-portal-resource-manager.md)
> * [PowerShell](expressroute-howto-circuit-arm.md)
> * [Azure CLI](howto-circuit-cli.md)
> * [Video - Azure portalı](http://azure.microsoft.com/documentation/videos/azure-expressroute-how-to-create-an-expressroute-circuit)
> * [PowerShell (klasik)](expressroute-howto-circuit-classic.md)
>

Bu makalede nasıl toocreate bir Azure expressroute bağlantı hattı PowerShell cmdlet'leri ve hello Azure Resource Manager dağıtım modelini kullanarak açıklanmaktadır. Bu makalede ayrıca, nasıl toocheck hello hello devrenin durumunu, güncelleştirme veya silme ve onu yetkisini kaldırma gösterir.

## <a name="before-you-begin"></a>Başlamadan önce
* Merhaba hello Azure Resource Manager PowerShell cmdlet'lerinin en son sürümünü yükleyin. Daha fazla bilgi için bkz: [Azure PowerShell genel bakış](/powershell/azure/overview).
* Gözden geçirme hello [Önkoşullar](expressroute-prerequisites.md) ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.


## <a name="create-and-provision-an-expressroute-circuit"></a>Oluşturma ve bir expressroute bağlantı hattı sağlama
### <a name="1-sign-in-tooyour-azure-account-and-select-your-subscription"></a>1. Tooyour Azure hesabı oturum ve aboneliğinizi seçin
toobegin yapılandırmanıza, oturum açma tooyour Azure hesabı. Bağlandığınız örnekler toohelp aşağıdaki hello kullan:

```powershell
Login-AzureRmAccount
```

Merhaba hesabının Hello abonelikleri kontrol edin:

```powershell
Get-AzureRmSubscription
```

Bir expressroute bağlantı hattı için toocreate istediğiniz hello aboneliği seçin:

```powershell
Select-AzureRmSubscription -SubscriptionId "<subscription ID>"
```

### <a name="2-get-hello-list-of-supported-providers-locations-and-bandwidths"></a>2. Desteklenen sağlayıcılar, konumları ve bant genişlikleri Hello listesini alma
Bir expressroute bağlantı hattı oluşturmadan önce desteklenen bağlantı sağlayıcıları, konumları ve bant genişliği seçenekleri hello listesi gerekir.

PowerShell cmdlet hello **Get-AzureRmExpressRouteServiceProvider** , sonraki adımlarda kullanacağınız bu bilgiler verir:

```powershell
Get-AzureRmExpressRouteServiceProvider
```

Bağlantı sağlayıcınız listelenip toosee kontrol edin. Aşağıdaki bilgilerle hello not edin. Bir bağlantı hattı oluşturduğunuzda, daha sonra gerekecektir.

* Ad
* PeeringLocations
* BandwidthsOffered

Şimdi hazır toocreate bir expressroute bağlantı hattı olduğunuz.   

### <a name="3-create-an-expressroute-circuit"></a>3. ExpressRoute bağlantı hattı oluşturma
Bir kaynak grubu zaten yoksa, expressroute bağlantı hattı oluşturmadan önce bir oluşturmanız gerekir. Merhaba aşağıdaki komutu çalıştırarak bunu yapabilirsiniz:

```powershell
New-AzureRmResourceGroup -Name "ExpressRouteResourceGroup" -Location "West US"
```


Aşağıdaki örnek hello nasıl toocreate 200 MB/sn expressroute bağlantı hattı Silikon vadisi Equinix aracılığıyla gösterir. Farklı bir sağlayıcı ve farklı ayarlar kullanıyorsanız, bu bilgileri isteğiniz yaptığınızda değiştirin. Merhaba, yeni bir hizmet anahtarı için bir örnek isteği aşağıdadır:

```powershell
New-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup" -Location "West US" -SkuTier Standard -SkuFamily MeteredData -ServiceProviderName "Equinix" -PeeringLocation "Silicon Valley" -BandwidthInMbps 200
```

Merhaba doğru SKU katmanı ve SKU ailesi belirttiğinizden emin olun:

* SKU katmanı, bir ExpressRoute standart ya da bir ExpressRoute premium Eklentisi etkin olup olmadığını belirler. Belirleyebileceğiniz *standart* tooget hello standart SKU veya *Premium* hello premium eklenti için.
* SKU ailesi hello faturalama türü belirler. Belirleyebileceğiniz *Metereddata* ölçülen veri planı için ve *Unlimiteddata* sınırsız veri planı için. Merhaba fatura türünden değiştirebileceğiniz *Metereddata* çok*Unlimiteddata*, ancak hello türünden değiştiremezsiniz *Unlimiteddata* çok*Metereddata* .

> [!IMPORTANT]
> ExpressRoute bağlantı hattınız bir hizmet anahtarı verilen hello andan itibaren Fatura edilecek. Merhaba bağlantı sağlayıcı hazır tooprovision hello hattı olduğunda bu işlemi gerçekleştirmek emin olun.
> 
> 

Merhaba yanıt hello hizmet anahtarı içerir. Merhaba aşağıdaki komutu çalıştırarak tüm hello parametrelerin ayrıntılı açıklamaları alabilirsiniz:

```powershell
get-help New-AzureRmExpressRouteCircuit -detailed
```


### <a name="4-list-all-expressroute-circuits"></a>4. Tüm ExpressRoute bağlantı hatları listesi
Tüm listesini Merhaba, oluşturduğunuz ExpressRoute bağlantı hatları tooget çalıştırmak hello **Get-AzureRmExpressRouteCircuit** komutu:

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```

Merhaba yanıt aşağıdaki örneğine benzer toohello görünür:

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                          }
    CircuitProvisioningState          : Enabled
    ServiceProviderProvisioningState  : NotProvisioned
    ServiceProviderNotes              :
    ServiceProviderProperties         : {
                                          "ServiceProviderName": "Equinix",
                                          "PeeringLocation": "Silicon Valley",
                                          "BandwidthInMbps": 200
                                        }
    ServiceKey                        : **************************************
    Peerings                          : []

Hello kullanarak herhangi bir zamanda bu bilgiler alabilirsiniz `Get-AzureRmExpressRouteCircuit` cmdlet'i. Merhaba parametresiz çağrısı yaparak tüm hello devreleri listeler. Hizmet anahtarınız hello listelenmez *ServiceKey* alan:

```powershell
Get-AzureRmExpressRouteCircuit
```


Merhaba yanıt aşağıdaki örneğine benzer toohello görünür:

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                          }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : NotProvisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


Merhaba aşağıdaki komutu çalıştırarak tüm hello parametrelerin ayrıntılı açıklamaları alabilirsiniz:

```powershell
get-help Get-AzureRmExpressRouteCircuit -detailed
```

### <a name="5-send-hello-service-key-tooyour-connectivity-provider-for-provisioning"></a>5. Merhaba hizmet anahtar tooyour bağlantı sağlayıcı sağlamak için Gönder
*ServiceProviderProvisioningState* hello hizmet sağlayıcı tarafında sağlama hello geçerli durumu hakkında bilgi sağlar. Durum Microsoft yan hello üzerinde hello durumunu sağlar. Merhaba hattı durumları sağlama hakkında daha fazla bilgi için bkz: [iş akışları](expressroute-workflows.md#expressroute-circuit-provisioning-states) makalesi.

Yeni bir expressroute bağlantı hattı oluşturduğunuzda, hello hattı durumu aşağıdaki hello olacaktır:

    ServiceProviderProvisioningState : NotProvisioned
    CircuitProvisioningState         : Enabled



Merhaba hattı hello bağlantı sağlayıcı için etkinleştirme işleminin hello olduğunda durumu aşağıdaki toohello değişir:

    ServiceProviderProvisioningState : Provisioning
    Status                           : Enabled

Toobe mümkün toouse için bir expressroute bağlantı hattı, durumu aşağıdaki hello olmalıdır:

    ServiceProviderProvisioningState : Provisioned
    CircuitProvisioningState         : Enabled

### <a name="6-periodically-check-hello-status-and-hello-state-of-hello-circuit-key"></a>6. Merhaba durumunu ve hello hattı anahtar hello durumunu düzenli aralıklarla denetleyin
Merhaba durumu ve hello hattı anahtar hello durumunu denetleme, sağlayıcınız hattınız etkinleştirildiğinde bilmenizi sağlar. Merhaba hattı yapılandırıldıktan sonra *ServiceProviderProvisioningState* olarak görünür *hazırlandı*hello aşağıdaki örnekte gösterildiği gibi:

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


Merhaba yanıt aşağıdaki örneğine benzer toohello görünür:

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                       }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                       }
    ServiceKey                       : **************************************
    Peerings                         : []

### <a name="7-create-your-routing-configuration"></a>7. Yönlendirme yapılandırması oluşturma
Merhaba adım adım yönergeler için bkz: [expressroute bağlantı hattı yönlendirme yapılandırması](expressroute-howto-routing-arm.md) makale toocreate ve hattı eşlemeler değiştirin.

> [!IMPORTANT]
> Bu yönergeler yalnızca Katman 2 bağlantı hizmetleri sunan hizmet sağlayıcıları ile oluşturulan toocircuits geçerlidir. Yönetilen sunan bir hizmet sağlayıcısı kullanıyorsanız, Katman 3 Hizmetleri (genellikle bir IP VPN, MPLS gibi), bağlantı sağlayıcınız yapılandırmak ve yönetmek için yönlendirme.
> 
> 

### <a name="8-link-a-virtual-network-tooan-expressroute-circuit"></a>8. Sanal ağ tooan expressroute bağlantı hattı bağlantı
Ardından, sanal ağ tooyour expressroute bağlantı hattı bağlayın. Kullanım hello [sanal bağlama ağları tooExpressRoute devreler](expressroute-howto-linkvnet-arm.md) hello Resource Manager dağıtım modeliyle çalışırken makalesi.

## <a name="getting-hello-status-of-an-expressroute-circuit"></a>Bir expressroute bağlantı hattı Hello durumunu alma
Hello kullanarak herhangi bir zamanda bu bilgiler alabilirsiniz **Get-AzureRmExpressRouteCircuit** cmdlet'i. Merhaba parametresiz çağrısı yaparak tüm hello devreleri listeler.

```powershell
Get-AzureRmExpressRouteCircuit
```


Merhaba yanıt aşağıdaki örneğine benzer toohello olacaktır:

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                         "Tier": "Standard",
                                         "Family": "MeteredData"
                                       }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                            "ServiceProviderName": "Equinix",
                                            "PeeringLocation": "Silicon Valley",
                                            "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


Merhaba kaynak grubu adı ve bağlantı hattı adı parametresi toohello araması olarak geçirerek belirli bir expressroute bağlantı hattı hakkında bilgi alabilirsiniz:

```powershell
Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"
```


Merhaba yanıt aşağıdaki örneğine benzer toohello görünür:

    Name                             : ExpressRouteARMCircuit
    ResourceGroupName                : ExpressRouteResourceGroup
    Location                         : westus
    Id                               : /subscriptions/***************************/resourceGroups/ExpressRouteResourceGroup/providers/Microsoft.Network/expressRouteCircuits/ExpressRouteARMCircuit
    Etag                             : W/"################################"
    ProvisioningState                : Succeeded
    Sku                              : {
                                         "Name": "Standard_MeteredData",
                                            "Tier": "Standard",
                                            "Family": "MeteredData"
                                          }
    CircuitProvisioningState         : Enabled
    ServiceProviderProvisioningState : Provisioned
    ServiceProviderNotes             :
    ServiceProviderProperties        : {
                                         "ServiceProviderName": "Equinix",
                                         "PeeringLocation": "Silicon Valley",
                                         "BandwidthInMbps": 200
                                          }
    ServiceKey                       : **************************************
    Peerings                         : []


Merhaba aşağıdaki komutu çalıştırarak tüm hello parametrelerin ayrıntılı açıklamaları alabilirsiniz:

```powershell
get-help get-azurededicatedcircuit -detailed
```

## <a name="modify"></a>Bir expressroute bağlantı hattı değiştirme
Bağlantı etkilemeden belirli bir expressroute bağlantı hattı özelliklerini değiştirebilirsiniz.

Yapabileceğiniz kapalı kalma süresi ile aşağıdaki hello:

* Etkinleştirmek veya devre dışı bir expressroute bağlantı hattı için ExpressRoute premium eklentisi.
* Artış hello bant genişliği, expressroute bağlantı hattı var. kapasite kullanılabilir hello bağlantı noktasında sağlanır. Bir bağlantı hattının Hello bant genişliği önceki sürüme indirme desteklenmiyor. 
* Ölçülen veri tooUnlimited veri planından ölçümü hello değiştirin. Sınırsız veri tooMetered veri desteklenmiyor planından ölçümü hello değiştirme.
* Etkinleştirme ve devre dışı *izin Klasik işlemleri*.

Toohello sınırlar ve sınırlamalar hakkında daha fazla bilgi için bkz [ExpressRoute SSS](expressroute-faqs.md).

### <a name="tooenable-hello-expressroute-premium-add-on"></a>tooenable hello ExpressRoute premium eklentisi
PowerShell parçacığını aşağıdaki hello kullanarak, varolan bağlantı hattınız için hello ExpressRoute premium eklentisi etkinleştirebilirsiniz:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Premium"
$ckt.sku.Name = "Premium_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

Merhaba hattı şimdi hello ExpressRoute premium eklentisi özellikleri etkin olacaktır. Merhaba komutu başarıyla çalıştırıldı hemen için hello premium eklenti özelliğini faturalama işlemini başlatacak.

### <a name="toodisable-hello-expressroute-premium-add-on"></a>toodisable hello ExpressRoute premium eklentisi
> [!IMPORTANT]
> Merhaba standart bağlantı hattı için izin daha büyük olan kaynaklar kullanıyorsanız, bu işlemi başarısız olabilir.
> 
> 

Merhaba aşağıdakileri göz önünde bulundurun:

* Premium toostandard düşürmek önce bağlı sanal ağlar hello sayıdaki emin olmalısınız toohello devre 10'dan oluşturulur. Bunu yapmazsanız, güncelleştirme isteği başarısız olur ve biz premium oranlarda faturalanacağı.
* Tüm sanal ağları diğer coğrafi bölgelerde bağlantısını gerekir. Bunu yapmazsanız, güncelleştirme isteği başarısız olur ve biz premium oranlarda faturalanacağı.
* Yol tablosu özel eşleme için 4. 000'den az yolları olmalıdır. Rota tablosu boyutunuz 4.000 yolları büyükse hello BGP oturumu bırakır ve 4.000 tanıtılan önekler hello sayısı gider kadar yeniden iler hale olmaz.

Merhaba ExpressRoute premium eklentisi hello varolan hattı için PowerShell cmdlet aşağıdaki hello kullanarak devre dışı bırakabilirsiniz:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Tier = "Standard"
$ckt.sku.Name = "Standard_MeteredData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="tooupdate-hello-expressroute-circuit-bandwidth"></a>tooupdate hello ExpressRoute devresi bant genişliği
Merhaba denetimi sağlayıcınız için desteklenen bant genişliği seçenekleri için [ExpressRoute SSS](expressroute-faqs.md). Var olan bağlantı hattınız hello boyutundan büyük herhangi bir boyutta seçebilirsiniz.

> [!IMPORTANT]
> Merhaba varolan bağlantı noktasında yetersiz kapasite ise toorecreate hello expressroute bağlantı hattı olabilir. Varsa hiçbir ek kapasite kullanılabilir o konumda hello hattı yükseltemezsiniz.
>
> Bir expressroute bağlantı hattı kesintiye uğratmadan hello bant genişliği azaltma olamaz. Bant genişliği eski sürüme düşürmeyi toodeprovision hello expressroute bağlantı hattı gerektirir ve yeni bir expressroute bağlantı hattı yeniden sağlayın.
> 

Gereksinim boyutu karar verdikten sonra komutu tooresize aşağıdaki hello hattınız kullanın:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.ServiceProviderProperties.BandwidthInMbps = 1000

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```


Bağlantı hattınız hello Microsoft tarafında boyutlandırılıp. Ardından bu değişikliği kendi yan toomatch, bağlantı sağlayıcısı tooupdate yapılandırmalarında başvurmanız gerekir. Bu bildirim yaptıktan sonra biz güncelleştirilmiş hello bant seçeneği için faturalama başlar.

### <a name="toomove-hello-sku-from-metered-toounlimited"></a>ölçülen toounlimited gelen toomove hello SKU
PowerShell parçacığını aşağıdaki hello kullanarak hello ExpressRoute devresi SKU'su değiştirebilirsiniz:

```powershell
$ckt = Get-AzureRmExpressRouteCircuit -Name "ExpressRouteARMCircuit" -ResourceGroupName "ExpressRouteResourceGroup"

$ckt.Sku.Family = "UnlimitedData"
$ckt.sku.Name = "Premium_UnlimitedData"

Set-AzureRmExpressRouteCircuit -ExpressRouteCircuit $ckt
```

### <a name="toocontrol-access-toohello-classic-and-resource-manager-environments"></a>toocontrol erişim toohello Klasik ve Resource Manager ortamları
Merhaba yönergeleri gözden [taşıma ExpressRoute bağlantı hatları hello Klasik toohello Resource Manager dağıtım modelinde](expressroute-howto-move-arm.md).  

## <a name="deprovisioning-and-deleting-an-expressroute-circuit"></a>Sağlamayı kaldırmayı ve bir expressroute bağlantı hattı silme
Merhaba aşağıdakileri göz önünde bulundurun:

* Tüm sanal ağlardan hello expressroute bağlantı hattı bağlantısını gerekir. Bu işlem başarısız olursa, tüm sanal ağ olup olmadığını toosee toohello hattı bağlı denetleyin.
* Merhaba ExpressRoute bağlantı hattı Hizmet Sağlayıcısı sağlama durumu ise **sağlama** veya **hazırlandı** kendi tarafında hizmet sağlayıcısı toodeprovision hello hattınız ile çalışmanız gerekir. Biz tooreserve kaynakları devam edecek ve hello hizmet sağlayıcısı sağlamayı hello hattı tamamlandıktan ve bize bildiren kadar sizi faturalandırmak.
* Merhaba hizmet sağlayıcısı hello hattı sağlaması kaldırılıyor. sağlaması değilse (Merhaba Hizmet Sağlayıcısı sağlama durumu çok ayarlamak**sağlanmadı**) hello hattı sonra silebilirsiniz. Bu hello hattı için fatura durdurur

Hello aşağıdaki komutu çalıştırarak, expressroute bağlantı hattı silebilirsiniz:

```powershell
Remove-AzureRmExpressRouteCircuit -ResourceGroupName "ExpressRouteResourceGroup" -Name "ExpressRouteARMCircuit"
```

## <a name="next-steps"></a>Sonraki adımlar

Bağlantı hattınız oluşturduktan sonra aşağıdaki hello emin olun:

* [Oluşturma ve expressroute bağlantı hattı için yönlendirmeyi değiştirme](expressroute-howto-routing-arm.md)
* [Sanal ağ tooyour expressroute bağlantı hattı bağlantı](expressroute-howto-linkvnet-arm.md)
