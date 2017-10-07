---
title: "aaaIntroduction tooApp hizmeti ortamı v1"
description: "Tüm uygulamalarınızın çalıştırmak için güvenli, VNet katılmış, ayrılmış ölçek birimleri sağlayan hello uygulama hizmeti ortamı v1 özelliği hakkında bilgi edinin."
services: app-service
documentationcenter: 
author: stefsch
manager: erikre
editor: 
ms.assetid: 78e6d4f5-da46-4eb5-a632-b5fdc17d2394
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: ccompy
ms.openlocfilehash: 6e3cd1909b241887b5ec19412b9f7884d870cc3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapp-service-environment-v1"></a>Giriş tooApp hizmeti ortamı v1

> [!NOTE]
> Uygulama hizmeti ortamı v1 hello hakkında makaledir.  Merhaba, daha kolay toouse ve daha güçlü altyapısı üzerinde çalışan uygulama hizmeti ortamı'nın daha yeni bir sürümü var. Merhaba yeni sürümü hakkında daha fazla ile Merhaba Başlat toolearn [giriş toohello uygulama hizmeti ortamı](../app-service/app-service-environment/intro.md).
> 

## <a name="overview"></a>Genel Bakış
Bir uygulama hizmeti ortamını bir [Premium] [ PremiumTier] hizmet Azure App Service uygulamalarını yüksek ölçekte güvenli bir şekilde çalıştırmak için tam yalıtılmış ve ayrılmış bir ortam sağlayan bir Azure uygulama hizmeti planı seçeneği de dahil olmak üzere [Web Apps][WebApps], [Mobile Apps][MobileApps], ve [API uygulamaları][APIApps].  

Uygulama hizmeti ortamları gerektiren uygulama iş yükleri için idealdir:

* Çok yüksek düzeyde ölçekleme
* Yalıtım ve güvenli ağ erişimi

Müşterilerin, tek bir Azure bölge içinde ve aynı zamanda birden çok Azure bölgeler arasında birden fazla App Service ortamları oluşturabilirsiniz.  Bu uygulama hizmeti ortamları yatay olarak ölçekleme durumu daha az uygulama katmanları yüksek RPS iş yüklerini desteklemek için ideal hale getirir.

Uygulama hizmeti ortamları yalıtılmış toorunning yalnızca tek bir müşterinin uygulamalardır, her zaman bir sanal ağ içinde dağıtılır.  Her iki uygulama gelen ve giden ağ trafiği üzerinde ayrıntılı denetim müşteriler sahip ve uygulamaları sanal ağlar tooon içi şirket kaynaklarına yüksek hızlı güvenli bağlantı kurabilirsiniz.

Tüm makaleler ve nasıl-hakkında kullanıcının hello App Service ortamları kullanılabilir [uygulama hizmeti ortamları için Benioku](../app-service/app-service-app-service-environments-readme.md).

App Service ortamları nasıl yüksek ölçekli etkinleştirmek ve güvenli bir genel bakış için ağ erişimi, hello bkz [AzureCon derinlemesine] [ AzureConDeepDive] App Service ortamları üzerinde!

Birden fazla App Service ortamları kullanarak yatay olarak ölçekleme üzerinde bir derin Dalış için nasıl hello makalesine bakın toosetup bir [coğrafi olarak dağıtılan uygulama ayak izini][GeodistributedAppFootprint].

toosee nasıl hello AzureCon derinlemesine gösterilen hello güvenlik mimarisi yapılandırılmışsa, uygulama üzerinde hello makaleye bakın bir [güvenlik mimarisine katmanlı](app-service-app-service-environment-layered-security.md) App Service ortamları ile.

Uygulama hizmeti ortamları üzerinde çalışan uygulamalar, web uygulaması Güvenlik Duvarı (WAF) gibi Yukarı Akış cihazlar tarafından geçişli erişimleri olabilir.  Merhaba makale üzerinde [App Service ortamları için bir WAF yapılandırma](app-service-app-service-environment-web-application-firewall.md) bu senaryo, kapsar. 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="dedicated-compute-resources"></a>Adanmış bir işlem kaynakları
Tüm uygulama hizmeti ortamı'nda kaynaklar hello işlem özel olarak tooa tek bir abonelik ayrılmış ve bir uygulama hizmeti ortamı toofifty (50) işlem kaynakları özel kullanım için tek bir uygulama tarafından yapılandırılabilir.

Bir uygulama hizmeti ortamı bir ön uç işlem kaynak havuzu, hem de bir toothree çalışan işlem kaynak havuzları oluşur. 

Merhaba ön uç havuzu, bir uygulama hizmeti ortamı içindeki uygulama isteklerinin iyi Otomatik Yük Dengeleme olarak SSL sonlandırma sorumlu işlem kaynaklarını içerir. 

Her bir çalışan havuzu çok ayrılan işlem kaynaklarını içeren[App Service planları][AppServicePlan], bir veya daha fazla Azure App Service uygulama sırayla içerir.  Uygulama hizmeti ortamı'nda toothree farklı çalışan havuzları olabilir olduğundan, her bir çalışan havuzu için hello esneklik toochoose farklı işlem kaynakları sahip.  

Örneğin, bu, daha az güçlü işlem kaynağı toocreate bir çalışan havuzu geliştirme veya test uygulamaları için hedeflenen App Service planları sağlar.  İkinci (veya hatta üçüncü) çalışan havuzunda App Service planları çalışan üretim uygulamalar için hedeflenen daha güçlü işlem kaynakları kullanabilir.

Merhaba miktarı işlem kaynakları kullanılabilir toohello ön uç ve çalışan havuzları hakkında daha fazla bilgi için bkz: [nasıl tooConfigure bir uygulama hizmeti ortamı][HowToConfigureanAppServiceEnvironment].  

Uygulama hizmeti ortamı'nda desteklenen kaynak boyutlarını hello kullanılabilir ilgili ayrıntılar işlem için hello başvurun [App Service fiyatlandırması] [ AppServicePricing] sayfasında ve hello App Service ortamları için kullanılabilir seçenekleri gözden geçir içinde Hello Premium fiyatlandırma katmanı.

## <a name="virtual-network-support"></a>Sanal ağ desteği
Bir uygulama hizmeti ortamı oluşturulabilir **ya da** bir Azure Resource Manager sanal ağ **veya** Klasik dağıtım modeli sanal ağı ([sanal ağlarhakkındadahafazlabilgi] [MoreInfoOnVirtualNetworks]).  Bir uygulama hizmeti ortamı her zaman bir sanal ağ ve daha hassas bir şekilde bir sanal ağ alt ağı mevcut olmadığından, hem gelen ve giden ağ iletişimlerinin sanal ağlar toocontrol hello güvenlik özelliklerinden yararlanabilirsiniz.  

Uygulama hizmeti ortamı'ortak bir IP adresiyle veya iç yalnızca bir Azure iç yük dengeleyici (ILB) adresi ile karşılıklı ya da Internet'e olabilir.

Kullanabileceğiniz [ağ güvenlik grubu] [ NetworkSecurityGroups] toorestrict gelen ağ iletişimi toohello bir uygulama hizmeti ortamı bulunduğu alt ağı.  Bu, Yukarı Akış aygıtlar ve web uygulaması güvenlik duvarı ve ağ SaaS sağlayıcıları gibi hizmetler arkasında toorun uygulamaları sağlar.

Uygulamalar da sıklıkla iç veritabanları ve web Hizmetleri gibi şirket kaynaklarına tooaccess gerekir.  Ortak bir yaklaşım toomake bir Azure sanal ağı içinde akan Bu uç noktaları kullanılabilir yalnızca toointernal ağ trafiğidir.  Bir uygulama hizmeti ortamı birleştirilmiş toohello olduğunda hello iç Hizmetleri, uygulamaları hello ortamında çalışan aynı sanal ağ üzerinden erişilebilir uç noktalar dahil onlara erişebilirsiniz [siteden siteye] [ SiteToSite]ve [Azure ExpressRoute] [ ExpressRoute] bağlantıları.

Uygulama hizmeti ortamları sanal ağlar ve şirket içi ağlar ile nasıl çalıştığı hakkında daha fazla bilgi makaleleri aşağıdaki hello başvurun [ağ mimarisi][NetworkArchitectureOverview], [denetleme gelen Trafik][ControllingInboundTraffic], ve [güvenli bir şekilde bağlanma tooBackends][SecurelyConnectingToBackends]. 

## <a name="getting-started"></a>Başlarken
Uygulama hizmeti ortamları ile çalışmaya tooget bakın [nasıl tooCreate bir uygulama hizmeti ortamı][HowToCreateAnAppServiceEnvironment]

Tüm makaleler ve nasıl-için uygulama hizmeti ortamları hello kullanılabilir için kullanıcının [uygulama hizmeti ortamları için Benioku](../app-service/app-service-app-service-environments-readme.md).

Hello Azure App Service platformu hakkında daha fazla bilgi için bkz: [Azure App Service][AzureAppService].

Merhaba hello uygulama hizmeti ortamı ağ mimarisi genel bakış için bkz: [ağ mimarisine genel bakış] [ NetworkArchitectureOverview] makalesi.

ExpressRoute ile bir uygulama hizmeti ortamı kullanma hakkında ayrıntılar için bkz: aşağıdaki makaleye bakın hello [hızlı rota ve App Service ortamları][NetworkConfigDetailsForExpressRoute].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!-- LINKS -->
[PremiumTier]: http://azure.microsoft.com/pricing/details/app-service/
[MoreInfoOnVirtualNetworks]: https://azure.microsoft.com/documentation/articles/virtual-networks-faq/
[AppServicePlan]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[HowToCreateAnAppServiceEnvironment]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[WebApps]: http://azure.microsoft.com/documentation/articles/app-service-web-overview/
[MobileApps]: http://azure.microsoft.com/documentation/articles/app-service-mobile-value-prop-preview/
[APIApps]: http://azure.microsoft.com/documentation/articles/app-service-api-apps-why-best-platform/
[LogicApps]: http://azure.microsoft.com/documentation/articles/app-service-logic-what-are-logic-apps/
[AzureConDeepDive]:  https://azure.microsoft.com/documentation/videos/azurecon-2015-deploying-highly-scalable-and-secure-web-and-mobile-apps/
[GeodistributedAppFootprint]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-geo-distributed-scale/
[NetworkSecurityGroups]: https://azure.microsoft.com/documentation/articles/virtual-networks-nsg/
[SiteToSite]: https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create/
[ExpressRoute]: http://azure.microsoft.com/services/expressroute/
[HowToConfigureanAppServiceEnvironment]:  http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[ControllingInboundTraffic]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-control-inbound-traffic/
[SecurelyConnectingToBackends]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-securely-connecting-to-backend-resources/
[NetworkArchitectureOverview]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-architecture-overview/
[NetworkConfigDetailsForExpressRoute]:  https://azure.microsoft.com/documentation/articles/app-service-app-service-environment-network-configuration-expressroute/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 

<!-- IMAGES -->


