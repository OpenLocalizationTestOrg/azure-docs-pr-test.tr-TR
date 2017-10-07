---
title: "aaaApp hizmeti ortamı | Microsoft Docs"
description: "Azure uygulama hizmeti ortamı nedir? Giriş tooApp hizmeti ortamı."
keywords: "Azure uygulama hizmeti ortamı, sanal ağ, güvenli ağ oluşturma"
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 1db5c057-3c56-4537-b580-cdd21fe3f3a7
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: stefsch
ms.openlocfilehash: 1b59fed4e5a72d4c4805e1dca203747e07e77103
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-environment-documentation"></a>Uygulama hizmeti ortamı belgeleri
Bir uygulama hizmeti ortamını bir [Premium] [ PremiumTier] hizmet Azure App Service uygulamalarını yüksek ölçekte güvenli bir şekilde çalıştırmak için tam yalıtılmış ve ayrılmış bir ortam sağlayan bir Azure uygulama hizmeti planı seçeneği de dahil olmak üzere [Web Apps][WebApps], [Mobile Apps][MobileApps], ve [API uygulamaları][APIApps].  

Uygulama hizmeti ortamları gerektiren uygulama iş yükleri için idealdir:

* Çok yüksek düzeyde ölçekleme
* Yalıtım ve güvenli ağ erişimi

Müşterilerin, tek bir Azure bölge içinde ve aynı zamanda birden çok Azure bölgeler arasında birden fazla App Service ortamları oluşturabilirsiniz.  Bu uygulama hizmeti ortamları yatay olarak ölçekleme durumu daha az uygulama katmanları yüksek RPS iş yüklerini desteklemek için ideal hale getirir.

Uygulama hizmeti ortamları yalıtılmış toorunning yalnızca tek bir müşterinin uygulamalardır, her zaman bir sanal ağ içinde dağıtılır.  Müşterilerin sahip hem uygulama gelen ve giden ağ trafiği kullanarak üzerinde ayrıntılı denetim [ağ güvenlik grubu][NetworkSecurityGroups].  Uygulamalar, sanal ağlar tooon içi şirket kaynaklarına yüksek hızlı güvenli bağlantılar da oluşturabilirsiniz.

Uygulamaların sık iç veritabanları ve web Hizmetleri gibi şirket kaynaklarına tooaccess gerekir.  Uygulama hizmeti ortamları üzerinde çalışan uygulamalar aracılığıyla erişilebilen kaynaklara erişebilir [siteden siteye] [ SiteToSite] VPN ve [Azure ExpressRoute] [ ExpressRoute] bağlantıları.

* [App Service Ortamı nedir?](../app-service-web/app-service-app-service-environment-intro.md)
* [App Service Ortamı oluşturma](../app-service-web/app-service-web-how-to-create-an-app-service-environment.md)
* [App Service Ortamında Uygulama oluşturma](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [Oluşturma ve bir iç yük dengeleyici ile uygulama hizmeti ortamları kullanma](../app-service-web/app-service-environment-with-internal-load-balancer.md)
* [App Service Ortamını yapılandırma](../app-service-web/app-service-web-configure-an-app-service-environment.md) 
* [App Service Ortamında Uygulamaları Ölçeklendirme](../app-service-web/app-service-web-scale-a-web-app-in-an-app-service-environment.md)
* [Ağ Güvenliği ve Mimarisi](../app-service-web/app-service-app-service-environment-network-architecture-overview.md)

## <a name="how-tos"></a>Nasıl yapılır 's
[!INCLUDE [app-service-blueprint-app-service-environment](../../includes/app-service-blueprint-app-service-environment.md)]

## <a name="videos"></a>Videolar
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2016/BRK3205/player]

>[!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON325/player]

>[!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3715/player]



<!-- LINKS -->
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[WebApps]: http://azure.microsoft.com/documentation/articles/app-service-web-overview/
[MobileApps]: http://azure.microsoft.com/documentation/articles/app-service-mobile-value-prop-preview/
[APIApps]: http://azure.microsoft.com/documentation/articles/app-service-api-apps-why-best-platform/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
