---
title: "Azure ExpressRoute Microsoft eşliği için rota filtrelerini yapılandırın: portalı | Microsoft Docs"
description: "Bu makalede Microsoft Peering kullanma tooconfigure yol filtreleri Azure portalına nasıl hello açıklanır"
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
ms.date: 08/25/2017
ms.author: ganesr;cherylmc
ms.openlocfilehash: 2a47d465ec5f175d9510cef94606f70f036f0862
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-route-filters-for-microsoft-peering"></a>Microsoft eşlemesi için rota filtreleri yapılandırma

Yol filtreleri şekilde tooconsume bir alt kümesini Microsoft eşleme yoluyla desteklenen hizmetler şunlardır. Bu makale Yardım yapılandırmak ve ExpressRoute bağlantı hatları için yol filtreleri yönetmek Hello adımları.

Dynamics 365 Hizmetleri ve işletme için Office 365 Hizmetleri Exchange Online, SharePoint Online ve Skype gibi hello Microsoft eşleme aracılığıyla erişilebilir. Microsoft eşlemesi bir expressroute bağlantı hattı yapılandırıldığında, tüm ön eklerin ilgili toothese Hizmetleri oluşturulmuş hello BGP oturumları bildirilir. BGP topluluk değeri hello önek sunulan ekli tooevery önek tooidentify hello hizmetidir. Merhaba BGP topluluk değerlerini ve eşlemek için hello Hizmetleri listesi için bkz: [BGP toplulukları](expressroute-routing.md#bgp).

Bağlantı tooall Hizmetleri gerektiriyorsa, çok sayıda önekleri BGP bildirilir. Bu, ağınızdaki yönlendiricileri tarafından tutulan hello yol tablolarını hello boyutunu önemli ölçüde artırır. Yalnızca bir alt kümesini Hizmetleri Microsoft eşliği ile sunulan tooconsume planlıyorsanız, yol tablolarınız iki yolla hello boyutunu azaltabilirsiniz. Şunları yapabilirsiniz:

- İstenmeyen önekleri BGP toplulukları yol filtreleri uygulayarak filtreleyin. Bu standart bir ağ uygulaması ve birçok ağ içinde yaygın olarak kullanılır.

- Rota filtrelerini tanımlayın ve bunları tooyour expressroute bağlantı hattı uygulayabilirsiniz. Bir rota filtre hello listesi sağlar hizmetlerini, yeni bir kaynak Microsoft eşleme yoluyla tooconsume planlamaktır. ExpressRoute yönlendiriciler yalnızca hello rota filtrede tanımlanan toohello Hizmetleri ait önekleri hello listesi gönderir.

### <a name="about"></a>Rota filtreler hakkında

Microsoft eşlemesi, expressroute bağlantı hattı üzerinde yapılandırıldığında, hello Microsoft sınır yönlendiricileri hello sınır yönlendiricileri (sizin ya da bağlantı sağlayıcınızın) BGP oturumları çifti oluşturun. Yol yok tanıtılan tooyour ağ tabanlıdır. tooenable yol tanıtımları tooyour ağ, bir rota filtre ilişkilendirmeniz gerekir.

Bir rota filtre expressroute bağlantı hattı 's Microsoft eşleme yoluyla tooconsume istediğiniz hizmetleri tanımlamanıza olanak sağlar. Tüm hello BGP topluluk değerlerini temelde beyaz listesi var. Bir rota filtre kaynağı tanımlandı ve tooan expressroute bağlantı hattı bağlı sonra toohello BGP topluluk değerlerini eşlemek tüm ön eklerin tanıtılan tooyour ağ tabanlıdır.

Office 365 Hizmetleri bunlardaki ile toobe mümkün tooattach yol filtreleri, yetkilendirme tooconsume Office 365 Hizmetleri ExpressRoute aracılığıyla olması gerekir. ExpressRoute aracılığıyla yetkili tooconsume Office 365 Hizmetleri olmayan hello işlemi tooattach yol filtreleri başarısız olur. Merhaba Yetkilendirme işlemi hakkında daha fazla bilgi için bkz: [Office 365 için Azure ExpressRoute](https://support.office.com/article/Azure-ExpressRoute-for-Office-365-6d2534a2-c19c-4a99-be5e-33a0cee5d3bd). Bağlantı tooDynamics 365 Hizmetleri, önceki tüm yetkilendirme gerektirmez.

> [!IMPORTANT]
> Önceki tooAugust 1 yapılandırılmış olan ExpressRoute bağlantı hatları Microsoft eşliği, yol filtreleri tanımlanmamış olsa bile 2017 Microsoft eşleme aracılığıyla tanıtılan tüm hizmet ön eklerin sahip olur. Ve 1 Ağustos 2017 sonrasında yapılandırılmış ExpressRoute bağlantı hatları, Microsoft eşlemesi sahip olmaz tüm ön eklerin rota filtre bağlanana kadar tanıtılan toohello hattı.
> 
> 

### <a name="workflow"></a>İş akışı

Microsoft eşleme aracılığıyla toobe mümkün toosuccessfully tooservices bağlanma, hello aşağıdaki yapılandırma adımları tamamlamanız gerekir:

- Microsoft sağlanan eşlemesini sahip etkin bir expressroute olması gerekir. Bu görevleri yönergeleri tooaccomplish aşağıdaki hello kullanabilirsiniz:
  - [Bir expressroute bağlantı hattı oluşturma](expressroute-howto-circuit-portal-resource-manager.md) ve devam etmeden önce bağlantı sağlayıcınız tarafından etkinleştirilen hello hattı sahip. Hello expressroute bağlantı hattının sağlanmış ve etkin durumda olması gerekir.
  - [Microsoft eşlemesi oluşturmak](expressroute-howto-routing-portal-resource-manager.md) doğrudan hello BGP oturumu yönetiyorsanız. Veya, bağlantı sağlayıcınız hattınız için eşlemesini Microsoft sağlamak.

-  Oluşturma ve bir rota filtre yapılandırmanız gerekir.
    - Tanımlamak hello Microsoft eşleme yoluyla tooconsume ile Hizmetleri
    - Merhaba BGP topluluk değerlerini hello servisleri ile ilişkili olan listesini belirlemesini
    - Bir kural tooallow hello önek listesi eşleşen hello BGP topluluk değerlerini oluşturun

-  Merhaba rota filtre toohello expressroute bağlantı hattı ilişkilendirmeniz gerekir.

## <a name="before-you-begin"></a>Başlamadan önce

Yapılandırmaya başlamadan önce aşağıdaki ölçütleri hello karşıladığından emin olun:

 - Gözden geçirme hello [Önkoşullar](expressroute-prerequisites.md) ve [iş akışları](expressroute-workflows.md) yapılandırmaya başlamadan önce.

 - Etkin bir ExpressRoute bağlantı hattınızın olması gerekir. Çok olarak Hello yönergeleri[bir expressroute bağlantı hattı oluşturma](expressroute-howto-circuit-portal-resource-manager.md) ve devam etmeden önce bağlantı sağlayıcınız tarafından etkinleştirilen hello hattı sahip. Hello expressroute bağlantı hattının sağlanmış ve etkin durumda olması gerekir.

 - Etkin bir Microsoft eşlemesi olması gerekir. Bölümündeki yönergeleri izleyin [oluşturma ve eşleme yapılandırmasını değiştirme](expressroute-howto-routing-portal-resource-manager.md)


## <a name="prefixes"></a>1. adım. Önekleri ve BGP topluluk değerlerini listesini alma

### <a name="1-get-a-list-of-bgp-community-values"></a>1. BGP topluluk değerlerini listesini al

Microsoft eşleme aracılığıyla erişilebilir hizmetleriyle ilişkili BGP topluluk değerlerini hello kullanılabilir [ExpressRoute yönlendirme gereksinimleri](expressroute-routing.md) sayfası.

### <a name="2-make-a-list-of-hello-values-that-you-want-toouse"></a>2. Merhaba değerler listesini toouse istiyor olun

BGP topluluk değerlerini istediğiniz listesini toouse hello rota filtrede olun. Örnek olarak, hello Dynamics 365 Hizmetleri için BGP topluluk değeri 12076:5040 ' dir.

## <a name="filter"></a>2. adım. Bir rota filtre ve bir filtre kuralı oluşturma

Bir rota filtre yalnızca bir kuralınız olabilir ve hello kural 'İzin ver' türünde olmalıdır. Bu kural, kendisiyle ilişkilendirilmiş BGP topluluk değerlerini listesini olabilir.

### <a name="1-create-a-route-filter"></a>1. Bir rota filtresi oluşturma
Yeni bir kaynak hello seçeneği toocreate seçerek bir rota filtre oluşturabilirsiniz. Tıklatın **yeni** > **ağ** > **RouteFilter**hello görüntü aşağıdaki gösterildiği gibi:

![Bir rota filtresi oluşturma](.\media\how-to-routefilter-portal\CreateRouteFilter1.png)

Bir kaynak grubunda hello rota filtre yerleştirmeniz gerekir. 

![Bir rota filtresi oluşturma](.\media\how-to-routefilter-portal\CreateRouteFilter.png)

### <a name="2-create-a-filter-rule"></a>2. Bir filtre kuralı oluşturma

Ekleyebilir ve kural sekmesi rota filtreniz için hello seçerek güncelleştirme kurallarını yönetin.

![Bir rota filtresi oluşturma](.\media\how-to-routefilter-portal\ManageRouteFilter.png)


Tooconnect toofrom hello istediğiniz hizmetleri açılan liste ve bittiğinde hello kuralını kaydetmek hello seçebilirsiniz.

![Bir rota filtresi oluşturma](.\media\how-to-routefilter-portal\AddRouteFilterRule.png)


## <a name="attach"></a>3. adım. Merhaba rota filtre tooan expressroute bağlantı hattı ekleme

Merhaba "Hattı Ekle" düğmesini seçerek ve hello expressroute bağlantı hattı hello açılır listeden seçerek hello rota filtre tooa devresi ekleyebilirsiniz.

![Bir rota filtresi oluşturma](.\media\how-to-routefilter-portal\AddCktToRouteFilter.png)

## <a name="getproperties"></a>bir rota filtre tooget hello özellikleri

Merhaba Portalı'nda hello kaynak açtığınızda, bir rota filtre özelliklerini görüntüleyebilirsiniz.

![Bir rota filtresi oluşturma](.\media\how-to-routefilter-portal\ViewRouteFilter.png)


## <a name="updateproperties"></a>bir rota filtre tooupdate hello özellikleri

Merhaba "kuralı Yönet" düğmesini seçerek BGP topluluk değerlerini ekli tooa hattı hello listesini güncelleştirebilirsiniz.


![Bir rota filtresi oluşturma](.\media\how-to-routefilter-portal\ManageRouteFilter.png)

![Bir rota filtresi oluşturma](.\media\how-to-routefilter-portal\AddRouteFilterRule.png) 


## <a name="detach"></a>toodetach bir expressroute bağlantı hattı rota filtresi

toodetach hello rota filtre hattından hello hattındaki sağ tıklayın ve "ilişkisini üzerinde"'ı tıklatın.

![Bir rota filtresi oluşturma](.\media\how-to-routefilter-portal\DetachRouteFilter.png) 


## <a name="delete"></a>bir rota filtre toodelete

Bir rota filtre hello Sil düğmesini seçerek silebilirsiniz. 

![Bir rota filtresi oluşturma](.\media\how-to-routefilter-portal\DeleteRouteFilter.png) 

## <a name="next-steps"></a>Sonraki adımlar

ExpressRoute hakkında daha fazla bilgi için bkz: Merhaba [ExpressRoute SSS](expressroute-faqs.md).
