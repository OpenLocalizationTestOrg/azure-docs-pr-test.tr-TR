---
title: "aaaMoving ExpressRoute bağlantı hattına Klasik tooResource Manager | Microsoft Docs"
description: "Bu sayfayı gerekenler genel bir bakış sağlar hello Klasik ve Resource Manager dağıtım modellerinde hello köprü oluşturma hakkında tooknow."
documentationcenter: na
services: expressroute
author: ganesr
manager: carmonm
editor: 
ms.assetid: bdf01217-1a98-4ec0-a08e-d84fd37f78af
ms.service: expressroute
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/02/2017
ms.author: ganesr
ms.openlocfilehash: c901d2cda01aec409b528d29fc937ac6afaea511
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="moving-expressroute-circuits-from-hello-classic-toohello-resource-manager-deployment-model"></a>ExpressRoute bağlantı hatları hello Klasik toohello Resource Manager dağıtım modeli taşıma
Bu makale bir Azure expressroute bağlantı hattı hello Klasik toohello Azure Resource Manager dağıtım modeli toomove ne anlama geldiğini genel bir bakış sağlar.

Hem Klasik hello ve hello Resource Manager dağıtım modellerinde dağıtılan bir tek ExpressRoute bağlantı hattı tooconnect toovirtual ağları kullanabilirsiniz. Nasıl oluşturulduğunu, bağımsız olarak bir expressroute bağlantı hattı her iki dağıtım modeli üzerinden şimdi toovirtual ağlara bağlayabilirsiniz.

![Her iki dağıtım modeli üzerinden toovirtual ağlara bağlanan bir expressroute bağlantı hattı](./media/expressroute-move/expressroute-move-1.png)

## <a name="expressroute-circuits-that-are-created-in-hello-classic-deployment-model"></a>Merhaba Klasik dağıtım modelinde oluşturulmuş ExpressRoute bağlantı hatları
Merhaba Klasik dağıtım modelinde oluşturulmuş ExpressRoute bağlantı hatları taşınmış toobe toohello Resource Manager dağıtım modeli ilk tooenable bağlantı tooboth hello Klasik ve hello Resource Manager dağıtım modellerinde gerekir. Bir bağlantı taşınırken bağlantı kaybı veya kesintisi olmaz. Merhaba Klasik dağıtım modelinde tüm hattı sanal ağ bağlantıları (içinde hello aynı abonelik ve çapraz abonelik) korunur.

Hello taşıma sonra başarıyla tamamlandı hello expressroute bağlantı hattı görünür, gerçekleştirir ve tam olarak hello Resource Manager dağıtım modelinde oluşturulmuş expressroute bağlantı hattı gibi hissettirir. Artık hello Resource Manager dağıtım modelinde toovirtual ağlara bağlantılar oluşturabilirsiniz.

Bir expressroute bağlantı hattı taşınan toohello Resource Manager dağıtım modeli alındıktan sonra yalnızca hello Resource Manager dağıtım modeli kullanarak hello expressroute bağlantı hattı hello yaşam döngüsünü yönetebilirsiniz. Bu, (örneğin, bant genişliği, SKU ve faturalama türü) hattı özelliklerini güncelleştirme ve yalnızca hello Resource Manager dağıtım modelinde bağlantı hatları silme eşlemeleri, ekleme/güncelleştirme/silme gibi işlemleri gerçekleştirebileceğiniz anlamına gelir. Aşağıdaki erişim tooboth dağıtım modellerini nasıl yönetebileceğiniz hakkında daha ayrıntılı bilgi için hello Resource Manager dağıtım modelinde oluşturulan bağlantı hatları toohello bölüme bakın.

Bağlantı sağlayıcı tooperform hello taşıma tooinvolve sahip değilsiniz.

## <a name="expressroute-circuits-that-are-created-in-hello-resource-manager-deployment-model"></a>Merhaba Resource Manager dağıtım modelinde oluşturulmuş ExpressRoute bağlantı hatları
Merhaba Resource Manager dağıtım modeli toobe içinde her iki dağıtım modelinden erişilebilir oluşturulmuş ExpressRoute bağlantı hatları etkinleştirebilirsiniz. Aboneliğinizdeki tüm expressroute bağlantı hattı her iki dağıtım modelinden erişilebilir etkin toobe olabilir.

* Merhaba Resource Manager dağıtım modelinde oluşturulmuş ExpressRoute bağlantı hatlarının varsayılan olarak erişim toohello Klasik dağıtım modeli yok.
* Merhaba Klasik dağıtım modeli toohello Resource manager dağıtım modelinden taşınmış ExpressRoute bağlantı hatlarının varsayılan olarak her iki dağıtım modelinden erişilebilir.
* Bir expressroute bağlantı hattı her zaman olup hello Resource Manager veya Klasik dağıtım modeli oluşturulduğu bağımsız olarak erişim toohello Resource Manager dağıtım modeli vardır. Oluşturulan toovirtual ağlarının bağlantılar oluşturabilirsiniz Bunun anlamı üzerinde yönergeleri Resource Manager dağıtım modeli hello [nasıl toolink sanal ağlar](expressroute-howto-linkvnet-arm.md).
* Erişim toohello Klasik dağıtım modeli hello tarafından denetlenen **allowClassicOperations** hello expressroute bağlantı hattı parametresi.

> [!IMPORTANT]
> Merhaba üzerinde belgelenen tüm kotalar [hizmet sınırları](../azure-subscription-service-limits.md) sayfayı uygulayın. Örnek olarak, standart bir bağlantı hattı Klasik hello ve hello Resource Manager dağıtım modelleri arasında en fazla 10 sanal ağ bağlantıları/bağlantılar olabilir.
> 
> 

## <a name="controlling-access-toohello-classic-deployment-model"></a>Erişim toohello Klasik dağıtım modeli denetleme
Bir tek ExpressRoute bağlantı hattı toolink toovirtual ağlarda her iki dağıtım modeli tarafından hello ayarını etkinleştirebilirsiniz **allowClassicOperations** hello expressroute bağlantı hattı parametresi.

Ayarı **allowClassicOperations** tooTRUE, her iki dağıtım modelleri toohello expressroute bağlantı hattı sanal ağlardan toolink sağlar. Üzerinde Kılavuzu izleyerek hello Klasik dağıtım modelinde toovirtual ağlara bağlayabilirsiniz [nasıl toolink sanal ağlarda Klasik dağıtım modeli hello](expressroute-howto-linkvnet-classic.md). Üzerinde Kılavuzu izleyerek hello Resource Manager dağıtım modeli toovirtual ağlara bağlayabilirsiniz [nasıl toolink sanal ağlarda Resource Manager dağıtım modeli hello](expressroute-howto-linkvnet-arm.md).

Ayarı **allowClassicOperations** tooFALSE erişimi toohello hattı hello Klasik dağıtım modelinden. Ancak, hello Klasik dağıtım modelinde tüm sanal ağ bağlantıları korunur. Bu durumda, expressroute bağlantı hattı hello hello Klasik dağıtım modelinde görünür değil.

## <a name="supported-operations-in-hello-classic-deployment-model"></a>Operations hello Klasik dağıtım modelinde desteklenen
Klasik işlemleri aşağıdaki hello bir expressroute bağlantı hattı üzerinde desteklenen zaman hattı **allowClassicOperations** tooTRUE ayarlayın:

* ExpressRoute bağlantı hattı bilgilerini alma
* Tooclassic sanal ağlar oluşturma/güncelleştirme/alma/silme sanal ağ bağlantıları
* çapraz abonelik bağlantısı için sanal ağ bağlantı yetkilerini oluşturma/güncelleştirme/alma/silme

Hello şu Klasik işlemleri gerçekleştiremezsiniz zaman **allowClassicOperations** tooTRUE ayarlayın:

* Azure özel, Azure genel ve Microsoft eşlemeleri için Sınır Ağ Geçidi Protokolü (BGP) eşlemeleri oluşturma/güncelleştirme/alma/silme
* ExpressRoute bağlantı hatlarını silme

## <a name="communication-between-hello-classic-and-hello-resource-manager-deployment-models"></a>Merhaba Klasik hello Resource Manager dağıtım modelleri arasında iletişimi
Merhaba expressroute bağlantı hattı Klasik hello ve hello Resource Manager dağıtım modelleri arasında köprü gibi davranır. Trafiği arasındaki hello Klasik dağıtım modelinde sanal ağlardaki hem de sanal ağlarda hello Resource Manager dağıtım modeli akışları ExpressRoute aracılığıyla her iki sanal ağ bağlantılı toohello varsa aynı expressroute bağlantı hattı.

Toplam verimlilik hello işleme kapasitesi hello sanal ağ geçidi ile sınırlıdır. Trafik bu gibi durumlarda hello bağlantı sağlayıcısı ve sizin ağlarınıza girmez. Merhaba sanal ağlar arasındaki trafik akışını tam olarak hello Microsoft ağı içerisinde yer alır.

## <a name="access-tooazure-public-and-microsoft-peering-resources"></a>Erişim tooAzure genel ve Microsoft eşleme kaynaklarına
Azure ortak eşleme ve kesintisiz Microsoft eşleme aracılığıyla normalde erişilebilen tooaccess kaynakları devam edebilirsiniz.  

## <a name="whats-supported"></a>Desteklenen durumlar
Bu bölümde ExpressRoute bağlantı hatları için desteklenen durumlar açıklanmaktadır:

* Merhaba Klasik ve hello Resource Manager dağıtım modellerinde dağıtılan bir tek ExpressRoute bağlantı hattı tooaccess sanal ağlar kullanabilirsiniz.
* Hello Klasik toohello Resource Manager dağıtım modeli bir expressroute bağlantı hattını taşıyabilirsiniz. Taşındıktan sonra hello expressroute bağlantı hattı görünür, hissettirir ve hello Resource Manager dağıtım modelinde oluşturulan herhangi bir expressroute bağlantı hattı gibi gerçekleştirir.
* Yalnızca hello expressroute bağlantı hattını taşıyabilirsiniz. Bağlantı hattı bağlantıları, ağ geçitleri ve VPN ağ geçitleri bu işlem aracılığıyla taşınamaz.
* Bir expressroute bağlantı hattı taşınan toohello Resource Manager dağıtım modeli alındıktan sonra yalnızca hello Resource Manager dağıtım modeli kullanarak hello expressroute bağlantı hattı hello yaşam döngüsünü yönetebilirsiniz. Bu, (örneğin, bant genişliği, SKU ve faturalama türü) hattı özelliklerini güncelleştirme ve yalnızca hello Resource Manager dağıtım modelinde bağlantı hatları silme eşlemeleri, ekleme/güncelleştirme/silme gibi işlemleri gerçekleştirebileceğiniz anlamına gelir.
* Merhaba expressroute bağlantı hattı Klasik hello ve hello Resource Manager dağıtım modelleri arasında köprü gibi davranır. Trafiği arasındaki hello Klasik dağıtım modelinde sanal ağlardaki hem de sanal ağlarda hello Resource Manager dağıtım modeli akışları ExpressRoute aracılığıyla her iki sanal ağ bağlantılı toohello varsa aynı expressroute bağlantı hattı.
* Çapraz abonelik bağlantısı hem Klasik Merhaba hem de hello Resource Manager dağıtım modellerinde desteklenir.
* Merhaba Klasik modeli toohello Azure Resource Manager modelinden bir expressroute bağlantı hattı taşıdıktan sonra şunları yapabilirsiniz [hello sanal ağlar bağlantılı toohello expressroute bağlantı hattı geçirmek](expressroute-migration-classic-resource-manager.md).

## <a name="whats-not-supported"></a>Desteklenmeyen durumlar
Bu bölümde ExpressRoute bağlantı hatları için desteklenmeyen durumlar açıklanmaktadır:

* Merhaba Klasik dağıtım modelinden bir expressroute bağlantı hattı Hello yaşam döngüsünü yönetme.
* Merhaba Klasik dağıtım modeli için rol tabanlı erişim denetimi (RBAC) desteği. RBAC denetimleri tooa hattı hello Klasik dağıtım modelinde gerçekleştiremezsiniz. Hello aboneliğin tüm yönetici/Abonelikteki sanal ağlar toohello hattı bağlantısını veya bağlantı.

## <a name="configuration"></a>Yapılandırma
Açıklanan hello yönergeleri izleyerek [hello Klasik toohello Resource Manager dağıtım modelinden bir expressroute bağlantı hattı taşıma](expressroute-howto-move-arm.md).

## <a name="next-steps"></a>Sonraki adımlar
* [Merhaba sanal ağlar bağlantılı toohello expressroute bağlantı hattı hello Klasik modeli toohello Azure Resource Manager modelden geçirme](expressroute-migration-classic-resource-manager.md)
* İş akışı bilgileri için bkz. [ExpressRoute bağlantı hattı sağlama iş akışları ve devre durumları](expressroute-workflows.md).
* tooconfigure expressroute'unuzu:
  
  * [ExpressRoute bağlantı hattı oluşturma](expressroute-howto-circuit-arm.md)
  * [Yönlendirmeyi yapılandırma](expressroute-howto-routing-arm.md)
  * [Sanal ağ tooan expressroute bağlantı hattı bağlantı](expressroute-howto-linkvnet-arm.md)

