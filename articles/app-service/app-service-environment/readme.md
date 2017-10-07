---
title: "aaaAzure uygulama hizmeti ortamı Benioku dosyası"
description: "Azure uygulama hizmeti ortamı açıklar hello belgelerine listeler"
services: app-service
documentationcenter: na
author: ccompy
manager: stefsch
ms.assetid: 77452413-5193-4762-8b3d-5fa8e4edf1ca
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: ccompy
ms.openlocfilehash: 6edc74804ded7497e70c31c9e08252257add4415
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="app-service-environment-documentation"></a>Uygulama hizmeti ortamı belgeleri
 Azure uygulama hizmeti ortamı App Service uygulamalarını yüksek ölçekte güvenli bir şekilde çalıştırmak için tam yalıtılmış ve ayrılmış bir ortam sağlayan bir Azure uygulama hizmeti özelliğidir. Bu özellik barındırabilir, [web uygulamaları][webapps], [mobil uygulamaları][mobileapps], [API uygulamaları][APIApps], ve [işlevleri][Functions].

Uygulama hizmeti ortamları (ASEs) gerektiren uygulama iş yükleri için idealdir:

* Çok büyük ölçekli.
* Yalıtım ve güvenli ağ erişimi.

Müşterilerin, tek bir Azure bölge içinde ve birden çok Azure bölgeleri arasında birden çok ASEs oluşturabilirsiniz. Bu çok yönlülük ASEs yatay olarak ölçekleme durum bilgisiz uygulama katmanları yüksek RPS iş yüklerini desteklemek için ideal hale getirir.

ASEs yalıtılmış toorunning yalnızca tek bir müşterinin uygulamalardır, her zaman bir Azure sanal ağı dağıtılır. Müşterilerin kullanarak uygulama gelen ve giden ağ trafiği üzerinde ayrıntılı denetim sahip [ağ güvenlik grupları][NSGs]. Uygulamalar, sanal ağlar tooon içi şirket kaynaklarına yüksek hızlı güvenli bağlantılar da oluşturabilirsiniz.

Uygulamaların sık iç veritabanları ve web Hizmetleri gibi tooaccess şirket kaynaklarına gerekir. ASEs üzerinde çalışan uygulamalar aracılığıyla kaynaklara erişebilir [siteden siteye] [ SiteToSite] VPN ve [Azure ExpressRoute] [ ExpressRoute] bağlantıları.

* [Uygulama hizmeti ortamı nedir?][Intro]
* [Uygulama hizmeti ortamı oluşturma][MakeExternalASE]
* [Bir iç yük dengeleyici uygulama hizmeti ortamı oluşturma][MakeILBASE]
* [Bir uygulama hizmeti ortamı'nı kullanma][UsingASE]
* [Ağ konuları ve hello uygulama hizmeti ortamı][ASENetwork]
* [Bir şablondan bir uygulama hizmeti ortamı oluşturma][MakeASEfromTemplate]


## <a name="videos"></a>Videolar
Ana Modern PaaS hello Azure uygulama hizmeti ile Kurumsal için
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2016/BRK3205/player]

Yüksek Oranda Ölçeklenebilir ve Güvenli Uygulamalar Dağıtma
>[!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON325/player]

Azure Uygulama Hizmeti’nde Kurumsal Web Uygulamaları ve Mobil Uygulamalar Çalıştırma
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3715/player]

## <a name="app-service-environment-v1"></a>App Service Ortamı v1 ##
Uygulama hizmeti ortamı iki sürümü vardır: ASEv1 ve ASEv2. ASEv1 hakkında daha fazla bilgi için bkz: [uygulama hizmeti ortamı v1 belgelerine][ASEv1README].


<!--Links-->
[Intro]: ./intro.md
[MakeExternalASE]: ./create-external-ase.md
[MakeASEfromTemplate]: ./create-from-template.md
[MakeILBASE]: ./create-ilb-ase.md
[ASENetwork]: ./network-info.md
[ASEReadme]: ./readme.md
[UsingASE]: ./using-an-ase.md
[UDRs]: ../../virtual-network/virtual-networks-udr-overview.md
[NSGs]: ../../virtual-network/virtual-networks-nsg.md
[ConfigureASEv1]: ../../app-service-web/app-service-web-configure-an-app-service-environment.md
[ASEv1Intro]: ../../app-service-web/app-service-app-service-environment-intro.md
[webapps]: ../../app-service-web/app-service-web-overview.md
[mobileapps]: ../../app-service-mobile/app-service-mobile-value-prop.md
[APIapps]: ../../app-service-api/app-service-api-apps-why-best-platform.md
[Functions]: ../../azure-functions/index.yml
[Pricing]: http://azure.microsoft.com/pricing/details/app-service/
[ARMOverview]: ../../azure-resource-manager/resource-group-overview.md
[ConfigureSSL]: ../../app-service-web/web-sites-purchase-ssl-web-site.md
[Kudu]: http://azure.microsoft.com/resources/videos/super-secret-kudu-debug-console-for-azure-web-sites/
[AppDeploy]: ../../app-service-web/web-sites-deploy.md
[ASEWAF]: ../../app-service-web/app-service-app-service-environment-web-application-firewall.md
[AppGW]: ../../application-gateway/application-gateway-web-application-firewall-overview.md
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[ASEv1README]: ../app-service-app-service-environments-readme.md
[SiteToSite]: ../../vpn-gateway/vpn-gateway-site-to-site-create.md
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
