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
# <a name="introduction-tooapp-service-environment-v1"></a><span data-ttu-id="7bbf5-103">Giriş tooApp hizmeti ortamı v1</span><span class="sxs-lookup"><span data-stu-id="7bbf5-103">Introduction tooApp Service Environment v1</span></span>

> [!NOTE]
> <span data-ttu-id="7bbf5-104">Uygulama hizmeti ortamı v1 hello hakkında makaledir.</span><span class="sxs-lookup"><span data-stu-id="7bbf5-104">This article is about hello App Service Environment v1.</span></span>  <span data-ttu-id="7bbf5-105">Merhaba, daha kolay toouse ve daha güçlü altyapısı üzerinde çalışan uygulama hizmeti ortamı'nın daha yeni bir sürümü var.</span><span class="sxs-lookup"><span data-stu-id="7bbf5-105">There is a newer version of hello App Service Environment that is easier  toouse and runs on more powerful infrastructure.</span></span> <span data-ttu-id="7bbf5-106">Merhaba yeni sürümü hakkında daha fazla ile Merhaba Başlat toolearn [giriş toohello uygulama hizmeti ortamı](../app-service/app-service-environment/intro.md).</span><span class="sxs-lookup"><span data-stu-id="7bbf5-106">toolearn more about hello new version start with hello [Introduction toohello App  Service Environment](../app-service/app-service-environment/intro.md).</span></span>
> 

## <a name="overview"></a><span data-ttu-id="7bbf5-107">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="7bbf5-107">Overview</span></span>
<span data-ttu-id="7bbf5-108">Bir uygulama hizmeti ortamını bir [Premium] [ PremiumTier] hizmet Azure App Service uygulamalarını yüksek ölçekte güvenli bir şekilde çalıştırmak için tam yalıtılmış ve ayrılmış bir ortam sağlayan bir Azure uygulama hizmeti planı seçeneği de dahil olmak üzere [Web Apps][WebApps], [Mobile Apps][MobileApps], ve [API uygulamaları][APIApps].</span><span class="sxs-lookup"><span data-stu-id="7bbf5-108">An App Service Environment is a [Premium][PremiumTier] service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps at high scale, including [Web Apps][WebApps], [Mobile Apps][MobileApps], and [API Apps][APIApps].</span></span>  

<span data-ttu-id="7bbf5-109">Uygulama hizmeti ortamları gerektiren uygulama iş yükleri için idealdir:</span><span class="sxs-lookup"><span data-stu-id="7bbf5-109">App Service Environments are ideal for application workloads requiring:</span></span>

* <span data-ttu-id="7bbf5-110">Çok yüksek düzeyde ölçekleme</span><span class="sxs-lookup"><span data-stu-id="7bbf5-110">Very high scale</span></span>
* <span data-ttu-id="7bbf5-111">Yalıtım ve güvenli ağ erişimi</span><span class="sxs-lookup"><span data-stu-id="7bbf5-111">Isolation and secure network access</span></span>

<span data-ttu-id="7bbf5-112">Müşterilerin, tek bir Azure bölge içinde ve aynı zamanda birden çok Azure bölgeler arasında birden fazla App Service ortamları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7bbf5-112">Customers can create multiple App Service Environments within a single Azure region, as well as across multiple Azure regions.</span></span>  <span data-ttu-id="7bbf5-113">Bu uygulama hizmeti ortamları yatay olarak ölçekleme durumu daha az uygulama katmanları yüksek RPS iş yüklerini desteklemek için ideal hale getirir.</span><span class="sxs-lookup"><span data-stu-id="7bbf5-113">This makes App Service Environments ideal for horizontally scaling state-less application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="7bbf5-114">Uygulama hizmeti ortamları yalıtılmış toorunning yalnızca tek bir müşterinin uygulamalardır, her zaman bir sanal ağ içinde dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="7bbf5-114">App Service Environments are isolated toorunning only a single customer's applications, and are always deployed into a virtual network.</span></span>  <span data-ttu-id="7bbf5-115">Her iki uygulama gelen ve giden ağ trafiği üzerinde ayrıntılı denetim müşteriler sahip ve uygulamaları sanal ağlar tooon içi şirket kaynaklarına yüksek hızlı güvenli bağlantı kurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7bbf5-115">Customers have fine-grained control over both inbound and outbound application network traffic, and applications can establish high-speed secure connections over virtual networks tooon-premises corporate resources.</span></span>

<span data-ttu-id="7bbf5-116">Tüm makaleler ve nasıl-hakkında kullanıcının hello App Service ortamları kullanılabilir [uygulama hizmeti ortamları için Benioku](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="7bbf5-116">All articles and How-To's about App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="7bbf5-117">App Service ortamları nasıl yüksek ölçekli etkinleştirmek ve güvenli bir genel bakış için ağ erişimi, hello bkz [AzureCon derinlemesine] [ AzureConDeepDive] App Service ortamları üzerinde!</span><span class="sxs-lookup"><span data-stu-id="7bbf5-117">For an overview of how App Service Environments enable high scale and secure network access, see hello [AzureCon Deep Dive][AzureConDeepDive] on App Service Environments!</span></span>

<span data-ttu-id="7bbf5-118">Birden fazla App Service ortamları kullanarak yatay olarak ölçekleme üzerinde bir derin Dalış için nasıl hello makalesine bakın toosetup bir [coğrafi olarak dağıtılan uygulama ayak izini][GeodistributedAppFootprint].</span><span class="sxs-lookup"><span data-stu-id="7bbf5-118">For a deep-dive on horizontally scaling using multiple App Service Environments see hello article on how toosetup a [geo-distributed app footprint][GeodistributedAppFootprint].</span></span>

<span data-ttu-id="7bbf5-119">toosee nasıl hello AzureCon derinlemesine gösterilen hello güvenlik mimarisi yapılandırılmışsa, uygulama üzerinde hello makaleye bakın bir [güvenlik mimarisine katmanlı](app-service-app-service-environment-layered-security.md) App Service ortamları ile.</span><span class="sxs-lookup"><span data-stu-id="7bbf5-119">toosee how hello security architecture shown in hello AzureCon Deep Dive was configured, see hello article on implementing a [layered security architecture](app-service-app-service-environment-layered-security.md) with App Service Environments.</span></span>

<span data-ttu-id="7bbf5-120">Uygulama hizmeti ortamları üzerinde çalışan uygulamalar, web uygulaması Güvenlik Duvarı (WAF) gibi Yukarı Akış cihazlar tarafından geçişli erişimleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="7bbf5-120">Apps running on App Service Environments can have their access gated by upstream devices such as web application firewalls (WAF).</span></span>  <span data-ttu-id="7bbf5-121">Merhaba makale üzerinde [App Service ortamları için bir WAF yapılandırma](app-service-app-service-environment-web-application-firewall.md) bu senaryo, kapsar.</span><span class="sxs-lookup"><span data-stu-id="7bbf5-121">hello article on [configuring a WAF for App Service Environments](app-service-app-service-environment-web-application-firewall.md) covers this scenario.</span></span> 

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="dedicated-compute-resources"></a><span data-ttu-id="7bbf5-122">Adanmış bir işlem kaynakları</span><span class="sxs-lookup"><span data-stu-id="7bbf5-122">Dedicated Compute Resources</span></span>
<span data-ttu-id="7bbf5-123">Tüm uygulama hizmeti ortamı'nda kaynaklar hello işlem özel olarak tooa tek bir abonelik ayrılmış ve bir uygulama hizmeti ortamı toofifty (50) işlem kaynakları özel kullanım için tek bir uygulama tarafından yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="7bbf5-123">All of hello compute resources in an App Service Environment are dedicated exclusively tooa single subscription, and an App Service Environment can be configured with up toofifty (50) compute resources for exclusive use by a single application.</span></span>

<span data-ttu-id="7bbf5-124">Bir uygulama hizmeti ortamı bir ön uç işlem kaynak havuzu, hem de bir toothree çalışan işlem kaynak havuzları oluşur.</span><span class="sxs-lookup"><span data-stu-id="7bbf5-124">An App Service Environment is composed of a front-end compute resource pool, as well as one toothree worker compute resource pools.</span></span> 

<span data-ttu-id="7bbf5-125">Merhaba ön uç havuzu, bir uygulama hizmeti ortamı içindeki uygulama isteklerinin iyi Otomatik Yük Dengeleme olarak SSL sonlandırma sorumlu işlem kaynaklarını içerir.</span><span class="sxs-lookup"><span data-stu-id="7bbf5-125">hello front-end pool contains compute resources responsible for SSL termination as well automatic load balancing of app requests within an App Service Environment.</span></span> 

<span data-ttu-id="7bbf5-126">Her bir çalışan havuzu çok ayrılan işlem kaynaklarını içeren[App Service planları][AppServicePlan], bir veya daha fazla Azure App Service uygulama sırayla içerir.</span><span class="sxs-lookup"><span data-stu-id="7bbf5-126">Each worker pool contains compute resources allocated too[App Service Plans][AppServicePlan], which in turn contain one or more Azure App Service apps.</span></span>  <span data-ttu-id="7bbf5-127">Uygulama hizmeti ortamı'nda toothree farklı çalışan havuzları olabilir olduğundan, her bir çalışan havuzu için hello esneklik toochoose farklı işlem kaynakları sahip.</span><span class="sxs-lookup"><span data-stu-id="7bbf5-127">Since there can be up toothree different worker pools in an App Service Environment, you have hello flexibility toochoose different compute resources for each worker pool.</span></span>  

<span data-ttu-id="7bbf5-128">Örneğin, bu, daha az güçlü işlem kaynağı toocreate bir çalışan havuzu geliştirme veya test uygulamaları için hedeflenen App Service planları sağlar.</span><span class="sxs-lookup"><span data-stu-id="7bbf5-128">For example, this allows you toocreate one worker pool with less powerful compute resources for App Service Plans intended for development or test apps.</span></span>  <span data-ttu-id="7bbf5-129">İkinci (veya hatta üçüncü) çalışan havuzunda App Service planları çalışan üretim uygulamalar için hedeflenen daha güçlü işlem kaynakları kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="7bbf5-129">A second (or even third) worker pool could use more powerful compute resources intended for App Service Plans running production apps.</span></span>

<span data-ttu-id="7bbf5-130">Merhaba miktarı işlem kaynakları kullanılabilir toohello ön uç ve çalışan havuzları hakkında daha fazla bilgi için bkz: [nasıl tooConfigure bir uygulama hizmeti ortamı][HowToConfigureanAppServiceEnvironment].</span><span class="sxs-lookup"><span data-stu-id="7bbf5-130">For more details on hello quantity of compute resources available toohello front-end and worker pools, see [How tooConfigure an App Service Environment][HowToConfigureanAppServiceEnvironment].</span></span>  

<span data-ttu-id="7bbf5-131">Uygulama hizmeti ortamı'nda desteklenen kaynak boyutlarını hello kullanılabilir ilgili ayrıntılar işlem için hello başvurun [App Service fiyatlandırması] [ AppServicePricing] sayfasında ve hello App Service ortamları için kullanılabilir seçenekleri gözden geçir içinde Hello Premium fiyatlandırma katmanı.</span><span class="sxs-lookup"><span data-stu-id="7bbf5-131">For details on hello available compute resource sizes supported in an App Service Environment, consult hello [App Service Pricing][AppServicePricing] page and review hello available options for App Service Environments in hello Premium pricing tier.</span></span>

## <a name="virtual-network-support"></a><span data-ttu-id="7bbf5-132">Sanal ağ desteği</span><span class="sxs-lookup"><span data-stu-id="7bbf5-132">Virtual Network Support</span></span>
<span data-ttu-id="7bbf5-133">Bir uygulama hizmeti ortamı oluşturulabilir **ya da** bir Azure Resource Manager sanal ağ **veya** Klasik dağıtım modeli sanal ağı ([sanal ağlarhakkındadahafazlabilgi] [MoreInfoOnVirtualNetworks]).</span><span class="sxs-lookup"><span data-stu-id="7bbf5-133">An App Service Environment can be created in **either** an Azure Resource Manager virtual network, **or** a classic deployment model virtual network ([more info on virtual networks][MoreInfoOnVirtualNetworks]).</span></span>  <span data-ttu-id="7bbf5-134">Bir uygulama hizmeti ortamı her zaman bir sanal ağ ve daha hassas bir şekilde bir sanal ağ alt ağı mevcut olmadığından, hem gelen ve giden ağ iletişimlerinin sanal ağlar toocontrol hello güvenlik özelliklerinden yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7bbf5-134">Since an App Service Environment always exists in a virtual network, and more precisely within a subnet of a virtual network, you can leverage hello security features of virtual networks toocontrol both inbound and outbound network communications.</span></span>  

<span data-ttu-id="7bbf5-135">Uygulama hizmeti ortamı'ortak bir IP adresiyle veya iç yalnızca bir Azure iç yük dengeleyici (ILB) adresi ile karşılıklı ya da Internet'e olabilir.</span><span class="sxs-lookup"><span data-stu-id="7bbf5-135">An App Service Environment can be either Internet facing with a public IP address, or internal facing with only an Azure Internal Load Balancer (ILB) address.</span></span>

<span data-ttu-id="7bbf5-136">Kullanabileceğiniz [ağ güvenlik grubu] [ NetworkSecurityGroups] toorestrict gelen ağ iletişimi toohello bir uygulama hizmeti ortamı bulunduğu alt ağı.</span><span class="sxs-lookup"><span data-stu-id="7bbf5-136">You can use [network security groups][NetworkSecurityGroups] toorestrict inbound network communications toohello subnet where an App Service Environment resides.</span></span>  <span data-ttu-id="7bbf5-137">Bu, Yukarı Akış aygıtlar ve web uygulaması güvenlik duvarı ve ağ SaaS sağlayıcıları gibi hizmetler arkasında toorun uygulamaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="7bbf5-137">This allows you toorun apps behind upstream devices and services such as web application firewalls, and network SaaS providers.</span></span>

<span data-ttu-id="7bbf5-138">Uygulamalar da sıklıkla iç veritabanları ve web Hizmetleri gibi şirket kaynaklarına tooaccess gerekir.</span><span class="sxs-lookup"><span data-stu-id="7bbf5-138">Apps also frequently need tooaccess corporate resources such as internal databases and web services.</span></span>  <span data-ttu-id="7bbf5-139">Ortak bir yaklaşım toomake bir Azure sanal ağı içinde akan Bu uç noktaları kullanılabilir yalnızca toointernal ağ trafiğidir.</span><span class="sxs-lookup"><span data-stu-id="7bbf5-139">A common approach is toomake these endpoints available only toointernal network traffic flowing within an Azure virtual network.</span></span>  <span data-ttu-id="7bbf5-140">Bir uygulama hizmeti ortamı birleştirilmiş toohello olduğunda hello iç Hizmetleri, uygulamaları hello ortamında çalışan aynı sanal ağ üzerinden erişilebilir uç noktalar dahil onlara erişebilirsiniz [siteden siteye] [ SiteToSite]ve [Azure ExpressRoute] [ ExpressRoute] bağlantıları.</span><span class="sxs-lookup"><span data-stu-id="7bbf5-140">Once an App Service Environment is joined toohello same virtual network as hello internal services, apps running in hello environment can access them, including endpoints reachable via [Site-to-Site][SiteToSite] and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

<span data-ttu-id="7bbf5-141">Uygulama hizmeti ortamları sanal ağlar ve şirket içi ağlar ile nasıl çalıştığı hakkında daha fazla bilgi makaleleri aşağıdaki hello başvurun [ağ mimarisi][NetworkArchitectureOverview], [denetleme gelen Trafik][ControllingInboundTraffic], ve [güvenli bir şekilde bağlanma tooBackends][SecurelyConnectingToBackends].</span><span class="sxs-lookup"><span data-stu-id="7bbf5-141">For more details on how App Service Environments work with virtual networks and on-premises networks consult hello following articles on [Network Architecture][NetworkArchitectureOverview], [Controlling Inbound Traffic][ControllingInboundTraffic], and [Securely Connecting tooBackends][SecurelyConnectingToBackends].</span></span> 

## <a name="getting-started"></a><span data-ttu-id="7bbf5-142">Başlarken</span><span class="sxs-lookup"><span data-stu-id="7bbf5-142">Getting started</span></span>
<span data-ttu-id="7bbf5-143">Uygulama hizmeti ortamları ile çalışmaya tooget bakın [nasıl tooCreate bir uygulama hizmeti ortamı][HowToCreateAnAppServiceEnvironment]</span><span class="sxs-lookup"><span data-stu-id="7bbf5-143">tooget started with App Service Environments, see [How tooCreate An App Service Environment][HowToCreateAnAppServiceEnvironment]</span></span>

<span data-ttu-id="7bbf5-144">Tüm makaleler ve nasıl-için uygulama hizmeti ortamları hello kullanılabilir için kullanıcının [uygulama hizmeti ortamları için Benioku](../app-service/app-service-app-service-environments-readme.md).</span><span class="sxs-lookup"><span data-stu-id="7bbf5-144">All articles and How-To's for App Service Environments are available in hello [README for Application Service Environments](../app-service/app-service-app-service-environments-readme.md).</span></span>

<span data-ttu-id="7bbf5-145">Hello Azure App Service platformu hakkında daha fazla bilgi için bkz: [Azure App Service][AzureAppService].</span><span class="sxs-lookup"><span data-stu-id="7bbf5-145">For more information about hello Azure App Service platform, see [Azure App Service][AzureAppService].</span></span>

<span data-ttu-id="7bbf5-146">Merhaba hello uygulama hizmeti ortamı ağ mimarisi genel bakış için bkz: [ağ mimarisine genel bakış] [ NetworkArchitectureOverview] makalesi.</span><span class="sxs-lookup"><span data-stu-id="7bbf5-146">For an overview of hello App Service Environment network architecture, see hello [Network Architecture Overview][NetworkArchitectureOverview] article.</span></span>

<span data-ttu-id="7bbf5-147">ExpressRoute ile bir uygulama hizmeti ortamı kullanma hakkında ayrıntılar için bkz: aşağıdaki makaleye bakın hello [hızlı rota ve App Service ortamları][NetworkConfigDetailsForExpressRoute].</span><span class="sxs-lookup"><span data-stu-id="7bbf5-147">For details on using an App Service Environment with ExpressRoute, see hello following article on [Express Route and App Service Environments][NetworkConfigDetailsForExpressRoute].</span></span>

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


