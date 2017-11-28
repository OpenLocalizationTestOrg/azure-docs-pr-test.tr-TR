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
# <a name="app-service-environment-documentation"></a><span data-ttu-id="45116-103">Uygulama hizmeti ortamı belgeleri</span><span class="sxs-lookup"><span data-stu-id="45116-103">App Service environment documentation</span></span>
 <span data-ttu-id="45116-104">Azure uygulama hizmeti ortamı App Service uygulamalarını yüksek ölçekte güvenli bir şekilde çalıştırmak için tam yalıtılmış ve ayrılmış bir ortam sağlayan bir Azure uygulama hizmeti özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="45116-104">Azure App Service Environment is an Azure App Service feature that provides a fully isolated and dedicated environment for securely running App Service apps at high scale.</span></span> <span data-ttu-id="45116-105">Bu özellik barındırabilir, [web uygulamaları][webapps], [mobil uygulamaları][mobileapps], [API uygulamaları][APIApps], ve [işlevleri][Functions].</span><span class="sxs-lookup"><span data-stu-id="45116-105">This capability can host your [web apps][webapps], [mobile apps][mobileapps], [API apps][APIApps], and [functions][Functions].</span></span>

<span data-ttu-id="45116-106">Uygulama hizmeti ortamları (ASEs) gerektiren uygulama iş yükleri için idealdir:</span><span class="sxs-lookup"><span data-stu-id="45116-106">App Service environments (ASEs) are ideal for application workloads that require:</span></span>

* <span data-ttu-id="45116-107">Çok büyük ölçekli.</span><span class="sxs-lookup"><span data-stu-id="45116-107">Very high scale.</span></span>
* <span data-ttu-id="45116-108">Yalıtım ve güvenli ağ erişimi.</span><span class="sxs-lookup"><span data-stu-id="45116-108">Isolation and secure network access.</span></span>

<span data-ttu-id="45116-109">Müşterilerin, tek bir Azure bölge içinde ve birden çok Azure bölgeleri arasında birden çok ASEs oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45116-109">Customers can create multiple ASEs within a single Azure region and across multiple Azure regions.</span></span> <span data-ttu-id="45116-110">Bu çok yönlülük ASEs yatay olarak ölçekleme durum bilgisiz uygulama katmanları yüksek RPS iş yüklerini desteklemek için ideal hale getirir.</span><span class="sxs-lookup"><span data-stu-id="45116-110">This versatility makes ASEs ideal for horizontally scaling stateless application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="45116-111">ASEs yalıtılmış toorunning yalnızca tek bir müşterinin uygulamalardır, her zaman bir Azure sanal ağı dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="45116-111">ASEs are isolated toorunning only a single customer's applications and are always deployed into an Azure virtual network.</span></span> <span data-ttu-id="45116-112">Müşterilerin kullanarak uygulama gelen ve giden ağ trafiği üzerinde ayrıntılı denetim sahip [ağ güvenlik grupları][NSGs].</span><span class="sxs-lookup"><span data-stu-id="45116-112">Customers have fine-grained control over inbound and outbound application network traffic by using [Network Security Groups][NSGs].</span></span> <span data-ttu-id="45116-113">Uygulamalar, sanal ağlar tooon içi şirket kaynaklarına yüksek hızlı güvenli bağlantılar da oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45116-113">Applications can also establish high-speed secure connections over virtual networks tooon-premises corporate resources.</span></span>

<span data-ttu-id="45116-114">Uygulamaların sık iç veritabanları ve web Hizmetleri gibi tooaccess şirket kaynaklarına gerekir.</span><span class="sxs-lookup"><span data-stu-id="45116-114">Apps frequently need tooaccess corporate resources, such as internal databases and web services.</span></span> <span data-ttu-id="45116-115">ASEs üzerinde çalışan uygulamalar aracılığıyla kaynaklara erişebilir [siteden siteye] [ SiteToSite] VPN ve [Azure ExpressRoute] [ ExpressRoute] bağlantıları.</span><span class="sxs-lookup"><span data-stu-id="45116-115">Apps that run on ASEs can access resources via [site-to-site][SiteToSite] VPN and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

* <span data-ttu-id="45116-116">[Uygulama hizmeti ortamı nedir?][Intro]</span><span class="sxs-lookup"><span data-stu-id="45116-116">[What is an App Service environment?][Intro]</span></span>
* <span data-ttu-id="45116-117">[Uygulama hizmeti ortamı oluşturma][MakeExternalASE]</span><span class="sxs-lookup"><span data-stu-id="45116-117">[Create an App Service environment][MakeExternalASE]</span></span>
* <span data-ttu-id="45116-118">[Bir iç yük dengeleyici uygulama hizmeti ortamı oluşturma][MakeILBASE]</span><span class="sxs-lookup"><span data-stu-id="45116-118">[Create an internal load balancer App Service environment][MakeILBASE]</span></span>
* <span data-ttu-id="45116-119">[Bir uygulama hizmeti ortamı'nı kullanma][UsingASE]</span><span class="sxs-lookup"><span data-stu-id="45116-119">[Use an App Service environment][UsingASE]</span></span>
* <span data-ttu-id="45116-120">[Ağ konuları ve hello uygulama hizmeti ortamı][ASENetwork]</span><span class="sxs-lookup"><span data-stu-id="45116-120">[Networking considerations and hello App Service environment][ASENetwork]</span></span>
* <span data-ttu-id="45116-121">[Bir şablondan bir uygulama hizmeti ortamı oluşturma][MakeASEfromTemplate]</span><span class="sxs-lookup"><span data-stu-id="45116-121">[Create an App Service environment from a template][MakeASEfromTemplate]</span></span>


## <a name="videos"></a><span data-ttu-id="45116-122">Videolar</span><span class="sxs-lookup"><span data-stu-id="45116-122">Videos</span></span>
<span data-ttu-id="45116-123">Ana Modern PaaS hello Azure uygulama hizmeti ile Kurumsal için</span><span class="sxs-lookup"><span data-stu-id="45116-123">Master Modern PaaS for hello Enterprise with Azure App Service</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2016/BRK3205/player]

<span data-ttu-id="45116-124">Yüksek Oranda Ölçeklenebilir ve Güvenli Uygulamalar Dağıtma</span><span class="sxs-lookup"><span data-stu-id="45116-124">Deploying Highly Scalable and Secure Apps</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON325/player]

<span data-ttu-id="45116-125">Azure Uygulama Hizmeti’nde Kurumsal Web Uygulamaları ve Mobil Uygulamalar Çalıştırma</span><span class="sxs-lookup"><span data-stu-id="45116-125">Running Enterprise Web and Mobile Apps on Azure App Service</span></span>
>[!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3715/player]

## <a name="app-service-environment-v1"></a><span data-ttu-id="45116-126">App Service Ortamı v1</span><span class="sxs-lookup"><span data-stu-id="45116-126">App Service Environment v1</span></span> ##
<span data-ttu-id="45116-127">Uygulama hizmeti ortamı iki sürümü vardır: ASEv1 ve ASEv2.</span><span class="sxs-lookup"><span data-stu-id="45116-127">There are two versions of App Service Environment: ASEv1 and ASEv2.</span></span> <span data-ttu-id="45116-128">ASEv1 hakkında daha fazla bilgi için bkz: [uygulama hizmeti ortamı v1 belgelerine][ASEv1README].</span><span class="sxs-lookup"><span data-stu-id="45116-128">For information on ASEv1, see [App Service Environment v1 documentation][ASEv1README].</span></span>


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
