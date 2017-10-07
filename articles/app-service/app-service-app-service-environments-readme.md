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
# <a name="app-service-environment-documentation"></a><span data-ttu-id="13313-105">Uygulama hizmeti ortamı belgeleri</span><span class="sxs-lookup"><span data-stu-id="13313-105">App Service Environment Documentation</span></span>
<span data-ttu-id="13313-106">Bir uygulama hizmeti ortamını bir [Premium] [ PremiumTier] hizmet Azure App Service uygulamalarını yüksek ölçekte güvenli bir şekilde çalıştırmak için tam yalıtılmış ve ayrılmış bir ortam sağlayan bir Azure uygulama hizmeti planı seçeneği de dahil olmak üzere [Web Apps][WebApps], [Mobile Apps][MobileApps], ve [API uygulamaları][APIApps].</span><span class="sxs-lookup"><span data-stu-id="13313-106">An App Service Environment is a [Premium][PremiumTier] service plan option of Azure App Service that provides a fully isolated and dedicated environment for securely running Azure App Service apps at high scale, including [Web Apps][WebApps], [Mobile Apps][MobileApps], and [API Apps][APIApps].</span></span>  

<span data-ttu-id="13313-107">Uygulama hizmeti ortamları gerektiren uygulama iş yükleri için idealdir:</span><span class="sxs-lookup"><span data-stu-id="13313-107">App Service Environments are ideal for application workloads requiring:</span></span>

* <span data-ttu-id="13313-108">Çok yüksek düzeyde ölçekleme</span><span class="sxs-lookup"><span data-stu-id="13313-108">Very high scale</span></span>
* <span data-ttu-id="13313-109">Yalıtım ve güvenli ağ erişimi</span><span class="sxs-lookup"><span data-stu-id="13313-109">Isolation and secure network access</span></span>

<span data-ttu-id="13313-110">Müşterilerin, tek bir Azure bölge içinde ve aynı zamanda birden çok Azure bölgeler arasında birden fazla App Service ortamları oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13313-110">Customers can create multiple App Service Environments within a single Azure region, as well as across multiple Azure regions.</span></span>  <span data-ttu-id="13313-111">Bu uygulama hizmeti ortamları yatay olarak ölçekleme durumu daha az uygulama katmanları yüksek RPS iş yüklerini desteklemek için ideal hale getirir.</span><span class="sxs-lookup"><span data-stu-id="13313-111">This makes App Service Environments ideal for horizontally scaling state-less application tiers in support of high RPS workloads.</span></span>

<span data-ttu-id="13313-112">Uygulama hizmeti ortamları yalıtılmış toorunning yalnızca tek bir müşterinin uygulamalardır, her zaman bir sanal ağ içinde dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="13313-112">App Service Environments are isolated toorunning only a single customer's applications, and are always deployed into a virtual network.</span></span>  <span data-ttu-id="13313-113">Müşterilerin sahip hem uygulama gelen ve giden ağ trafiği kullanarak üzerinde ayrıntılı denetim [ağ güvenlik grubu][NetworkSecurityGroups].</span><span class="sxs-lookup"><span data-stu-id="13313-113">Customers have fine-grained control over both inbound and outbound application network traffic using [network security groups][NetworkSecurityGroups].</span></span>  <span data-ttu-id="13313-114">Uygulamalar, sanal ağlar tooon içi şirket kaynaklarına yüksek hızlı güvenli bağlantılar da oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="13313-114">Applications can also establish high-speed secure connections over virtual networks tooon-premises corporate resources.</span></span>

<span data-ttu-id="13313-115">Uygulamaların sık iç veritabanları ve web Hizmetleri gibi şirket kaynaklarına tooaccess gerekir.</span><span class="sxs-lookup"><span data-stu-id="13313-115">Apps frequently need tooaccess corporate resources such as internal databases and web services.</span></span>  <span data-ttu-id="13313-116">Uygulama hizmeti ortamları üzerinde çalışan uygulamalar aracılığıyla erişilebilen kaynaklara erişebilir [siteden siteye] [ SiteToSite] VPN ve [Azure ExpressRoute] [ ExpressRoute] bağlantıları.</span><span class="sxs-lookup"><span data-stu-id="13313-116">Apps running on App Service Environments can access resources reachable via [Site-to-Site][SiteToSite] VPN and [Azure ExpressRoute][ExpressRoute] connections.</span></span>

* [<span data-ttu-id="13313-117">App Service Ortamı nedir?</span><span class="sxs-lookup"><span data-stu-id="13313-117">What is an App Service Environment?</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
* [<span data-ttu-id="13313-118">App Service Ortamı oluşturma</span><span class="sxs-lookup"><span data-stu-id="13313-118">Creating an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="13313-119">App Service Ortamında Uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="13313-119">Creating Apps in an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md)
* [<span data-ttu-id="13313-120">Oluşturma ve bir iç yük dengeleyici ile uygulama hizmeti ortamları kullanma</span><span class="sxs-lookup"><span data-stu-id="13313-120">Creating and Using an Internal Load Balancer with App Service Environments</span></span>](../app-service-web/app-service-environment-with-internal-load-balancer.md)
* [<span data-ttu-id="13313-121">App Service Ortamını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="13313-121">Configuring an App Service Environment</span></span>](../app-service-web/app-service-web-configure-an-app-service-environment.md) 
* [<span data-ttu-id="13313-122">App Service Ortamında Uygulamaları Ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="13313-122">Scaling Apps in an App Service Environment</span></span>](../app-service-web/app-service-web-scale-a-web-app-in-an-app-service-environment.md)
* [<span data-ttu-id="13313-123">Ağ Güvenliği ve Mimarisi</span><span class="sxs-lookup"><span data-stu-id="13313-123">Network Security and Architecture</span></span>](../app-service-web/app-service-app-service-environment-network-architecture-overview.md)

## <a name="how-tos"></a><span data-ttu-id="13313-124">Nasıl yapılır 's</span><span class="sxs-lookup"><span data-stu-id="13313-124">How To's</span></span>
[!INCLUDE [app-service-blueprint-app-service-environment](../../includes/app-service-blueprint-app-service-environment.md)]

## <a name="videos"></a><span data-ttu-id="13313-125">Videolar</span><span class="sxs-lookup"><span data-stu-id="13313-125">Videos</span></span>
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
