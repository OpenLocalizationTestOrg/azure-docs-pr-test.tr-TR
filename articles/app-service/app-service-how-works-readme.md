---
title: "aaaHow Azure App Service nasıl çalışır"
description: "App Service’in nasıl çalıştığını öğrenin"
keywords: "app service, azure app service, ölçek, ölçeklenebilir, app service planı, app service maliyeti"
services: app-service
documentationcenter: 
author: yochay
manager: erikre
editor: 
ms.assetid: ae74fc32-969e-4580-8d61-02c922f1f184
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 02/23/2017
ms.author: yochayk
ms.openlocfilehash: b20733ec8844773d063e2b6918605c4a48db1f5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-app-service-works"></a><span data-ttu-id="8fd87-104">App Service nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="8fd87-104">How App Service works</span></span>
<span data-ttu-id="8fd87-105">Azure uygulama hizmeti mühendisleri Günümüzde karşılaştığınız tasarlanmış toosolve hello pratik sorunları olan bir bulut hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="8fd87-105">Azure App Service is a cloud service that's designed toosolve hello practical problems that engineers face today.</span></span>
<span data-ttu-id="8fd87-106">Uygulama hizmeti odaklar üzerinde hello ödün vermeden üstün Geliştirici verimliliği sağlama üzerinde bulut ölçeğinde toodeliver uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="8fd87-106">App Service focuses on providing superior developer productivity without compromising on hello need toodeliver applications at cloud scale.</span></span> 

<span data-ttu-id="8fd87-107">App Service ayrıca hello özellik ve kurumsal iş kolu satır uygulamaları oluşturmak için gerekli olan çerçeve sağlar.</span><span class="sxs-lookup"><span data-stu-id="8fd87-107">App Service also provides hello features and frameworks that are necessary for creating enterprise line-of-business applications.</span></span> <span data-ttu-id="8fd87-108">App Service Java, PHP, Node.js, Python ve hello Microsoft .NET diller de dahil olmak üzere, en popüler geliştirme dilleri uygulamalar geliştirmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="8fd87-108">App Service lets you develop apps in most popular development languages, including Java, PHP, Node.js, Python, and hello Microsoft .NET languages.</span></span> <span data-ttu-id="8fd87-109">App Service ile yapabilecekleriniz:</span><span class="sxs-lookup"><span data-stu-id="8fd87-109">With App Service, you can:</span></span>

* <span data-ttu-id="8fd87-110">Yüksek oranda ölçeklenebilir web uygulamaları oluşturma.</span><span class="sxs-lookup"><span data-stu-id="8fd87-110">Build highly scalable web apps.</span></span>
* <span data-ttu-id="8fd87-111">Veri arka uçları, kullanıcı kimlik doğrulaması ve anında iletme bildirimleri gibi kullanımı kolay mobil özellik gruplarıyla hızlı şekilde Mobile Apps arka uçları oluşturma.</span><span class="sxs-lookup"><span data-stu-id="8fd87-111">Quickly build Mobile Apps back ends with a set of easy-to-use mobile capabilities such as data back ends, user authentication, and push notifications.</span></span>
* <span data-ttu-id="8fd87-112">API Apps ile API’leri uygulama, dağıtma ve yayımlama.</span><span class="sxs-lookup"><span data-stu-id="8fd87-112">Implement, deploy, and publish APIs with API Apps.</span></span>
* <span data-ttu-id="8fd87-113">İş uygulamalarını iş akışlarında birbirine bağlayın ve Logic Apps ile verileri dönüştürün.</span><span class="sxs-lookup"><span data-stu-id="8fd87-113">Tie business applications together into workflows and transform data with Logic Apps.</span></span>

> [!INCLUDE [app-service-linux](../../includes/app-service-linux.md)]
> 
> 

<span data-ttu-id="8fd87-114">En iyi duruma getirilmiş tam yaşam deneyimi uygulama tasarım tooapp bakım geliştiriciler toohave sağlayan hello ölçeklenebilir ve esnek Web Apps platform, tüm uygulama türleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="8fd87-114">All app types rely on hello scalable and flexible Web Apps platform, which enables developers toohave an optimized full lifecycle experience from app design tooapp maintenance.</span></span> <span data-ttu-id="8fd87-115">Merhaba yaşam döngüsü özellikleri hello aşağıdakileri sağlar:</span><span class="sxs-lookup"><span data-stu-id="8fd87-115">hello lifecycle capabilities enable hello following:</span></span>

* <span data-ttu-id="8fd87-116">**Hızlı Uygulama oluşturma**.</span><span class="sxs-lookup"><span data-stu-id="8fd87-116">**Quick app creation**.</span></span> <span data-ttu-id="8fd87-117">Baştan başlayabilir veya hello Azure Marketi işlemdeki destek sistem (OSS) paketinden seçin.</span><span class="sxs-lookup"><span data-stu-id="8fd87-117">Start from scratch or pick an operational support system (OSS) package from hello Azure Marketplace.</span></span>
* <span data-ttu-id="8fd87-118">**Sürekli dağıtım**.</span><span class="sxs-lookup"><span data-stu-id="8fd87-118">**Continuous deployment**.</span></span> <span data-ttu-id="8fd87-119">TFS, GitHub ve Bitbucket gibi popüler kaynak denetimlerinden otomatik olarak yeni kod dağıtın ve OneDrive ve Dropbox gibi çevrimiçi depolama hizmetlerinde içerik eşitleyin.</span><span class="sxs-lookup"><span data-stu-id="8fd87-119">Automatically deploy new code from popular source control solutions such as TFS, GitHub, and Bitbucket, and sync content from online storage services such as OneDrive and Dropbox.</span></span>
* <span data-ttu-id="8fd87-120">**Üretim ortamında test**.</span><span class="sxs-lookup"><span data-stu-id="8fd87-120">**Test in production**.</span></span> <span data-ttu-id="8fd87-121">Sorunsuz üretim öncesi ortamlar oluşturun ve toothem giden trafik miktarı hello yönetin.</span><span class="sxs-lookup"><span data-stu-id="8fd87-121">Smoothly create pre-production environments and manage hello amount of traffic that's going toothem.</span></span> <span data-ttu-id="8fd87-122">Gerektiğinde Merhaba bulutta hata ayıklayın ve sorunları bulunduğunda geri alma.</span><span class="sxs-lookup"><span data-stu-id="8fd87-122">Debug in hello cloud when needed, and roll back when issues are found.</span></span>
* <span data-ttu-id="8fd87-123">**Zaman uyumsuz görevler ve toplu işler çalıştırma**.</span><span class="sxs-lookup"><span data-stu-id="8fd87-123">**Running asynchronous tasks and batch jobs**.</span></span> <span data-ttu-id="8fd87-124">Arka planda kod çalıştırın ya da kodunuzu olaylar (örneğin, Azure Storage kuyruğuna gelen iletiler) zamanlanan süreleri (CRON) temel alarak etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="8fd87-124">Run code in a background process or activate your code based on events (such as messages landing in an Azure Storage queue) and scheduled times (CRON).</span></span>
* <span data-ttu-id="8fd87-125">**Ölçeklendirme hello uygulama**.</span><span class="sxs-lookup"><span data-stu-id="8fd87-125">**Scaling hello app**.</span></span> <span data-ttu-id="8fd87-126">Yatay ve dikey olarak trafik ve kaynak kullanımı temelinde hizmetinizi birçok seçenekleri tooautomatically ölçek birini kullanın.</span><span class="sxs-lookup"><span data-stu-id="8fd87-126">Use one of many options tooautomatically scale your service horizontally and vertically based on traffic and resource utilization.</span></span> <span data-ttu-id="8fd87-127">Ayrılmış tooyour uygulamaları özel ortamları yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="8fd87-127">Configure private environments that are dedicated tooyour apps.</span></span>   
* <span data-ttu-id="8fd87-128">**Bakımı hello uygulama**.</span><span class="sxs-lookup"><span data-stu-id="8fd87-128">**Maintaining hello app**.</span></span> <span data-ttu-id="8fd87-129">Tanılama özellikleri toostay sorunları ve tooefficiently öncesinde gerçek zamanlı (özelliklerle otomatik düzeltme ve dinamik hata ayıklama gibi) ya da çözümleyin veya günlükleri ve bellek çözümleme tarafından hello olgu sonra dökümleri ve birçok hello hata ayıklama kullanın.</span><span class="sxs-lookup"><span data-stu-id="8fd87-129">Use many of hello debugging and diagnostics features toostay ahead of problems and tooefficiently resolve them either in real time (with features such as auto-healing and live debugging) or after hello fact by analyzing logs and memory dumps.</span></span>

<span data-ttu-id="8fd87-130">Bir bütün olarak App Service özelliklerini kendi kodunda geliştiriciler toofocus etkinleştirin ve kararlı ve yüksek düzeyde ölçeklenebilir üretim durumuna hızlı şekilde ulaşmasını.</span><span class="sxs-lookup"><span data-stu-id="8fd87-130">As a whole, App Service capabilities enable developers toofocus on their code and quickly reach a stable and highly scalable production state.</span></span> <span data-ttu-id="8fd87-131">Merhaba API Apps ve Logic Apps özelliklerini, geliştiriciler iş çözümleri ve şirket içi toocloud tümleştirme arasındaki engeller için köprü gerçek kurumsal uygulamalar oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="8fd87-131">With hello API Apps and Logic Apps features, developers can build real-world enterprise applications that bridge barriers between business solutions and on-premises toocloud integration.</span></span> 

## <a name="videos"></a><span data-ttu-id="8fd87-132">Videolar</span><span class="sxs-lookup"><span data-stu-id="8fd87-132">Videos</span></span>
* [<span data-ttu-id="8fd87-133">Azure Uygulama Hizmeti Mimarisi</span><span class="sxs-lookup"><span data-stu-id="8fd87-133">Azure App Service Architecture</span></span>](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/)

## <a name="next-steps"></a><span data-ttu-id="8fd87-134">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8fd87-134">Next steps</span></span>

<span data-ttu-id="8fd87-135">Aşağıdaki konularda hello uygulama hizmeti hakkında daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="8fd87-135">Learn more about App Service in one of hello following topics:</span></span>

* [<span data-ttu-id="8fd87-136">Azure Uygulama Hizmeti nedir?</span><span class="sxs-lookup"><span data-stu-id="8fd87-136">What is Azure App Service?</span></span>](app-service-value-prop-what-is.md)
  * [<span data-ttu-id="8fd87-137">Web Uygulaması</span><span class="sxs-lookup"><span data-stu-id="8fd87-137">Web App</span></span>](../app-service-web/app-service-web-overview.md)
  * [<span data-ttu-id="8fd87-138">Mobil uygulama</span><span class="sxs-lookup"><span data-stu-id="8fd87-138">Mobile App</span></span>](../app-service-mobile/app-service-mobile-value-prop.md)
  * [<span data-ttu-id="8fd87-139">API Uygulaması</span><span class="sxs-lookup"><span data-stu-id="8fd87-139">API App</span></span>](../app-service-api/app-service-api-apps-why-best-platform.md)
* [<span data-ttu-id="8fd87-140">Azure Uygulama Hizmeti Mimarisi (sunu)</span><span class="sxs-lookup"><span data-stu-id="8fd87-140">Azure App Service Architecture (presentation)</span></span>](http://www.slideshare.net/maartenba/windows-azure-web-sites-things-they-dont-teach-kids-in-school-comunity-day-2013)
* [<span data-ttu-id="8fd87-141">Azure Uygulama Hizmeti, Cloud Services ve Sanal Makineler karşılaştırması</span><span class="sxs-lookup"><span data-stu-id="8fd87-141">Azure App Service, Cloud Services, and Virtual Machines comparison</span></span>](../app-service-web/choose-web-site-cloud-service-vm.md)
* [<span data-ttu-id="8fd87-142">App Service Planları’nı anlama</span><span class="sxs-lookup"><span data-stu-id="8fd87-142">Understanding App Service Plans</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
* [<span data-ttu-id="8fd87-143">Giriş tooApp hizmeti ortamı</span><span class="sxs-lookup"><span data-stu-id="8fd87-143">Introduction tooApp Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
  * [<span data-ttu-id="8fd87-144">Alıştırma: App Service Ortamı oluşturma</span><span class="sxs-lookup"><span data-stu-id="8fd87-144">Exercise: Create an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="8fd87-145">Azure Uygulama Hizmeti Geliştirme Yığınları Desteği</span><span class="sxs-lookup"><span data-stu-id="8fd87-145">Azure App Service Development Stacks Support</span></span>](https://azure.microsoft.com/blog/windows-azure-websites-development-stacks-support/)



