---
title: "Azure Uygulama Hizmetinde Mobile Apps Hakkında"
description: "App Service’in kurumsal mobil uygulamalarınıza sağladığı avantajları öğrenin."
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: yochayk
editor: 
ms.assetid: 4e96cb9d-a632-4cf6-8219-0810d8ade3f9
ms.service: app-service-mobile
ms.workload: na
ms.tgt_pltfrm: mobile-multiple
ms.devlang: na
ms.topic: hero-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: ac35ff9fe1c5f315c4de08de951f505627ec412b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <span data-ttu-id="e5f73-103"><a name="getting-started"> </a>Azure Uygulama Hizmetinde Mobile Apps Hakkında</span><span class="sxs-lookup"><span data-stu-id="e5f73-103"><a name="getting-started"> </a>About Mobile Apps in Azure App Service</span></span>
<span data-ttu-id="e5f73-104">Azure Uygulama Hizmeti, profesyonel geliştiricilere yönelik tam olarak yönetilen bir [hizmet olarak platform](https://azure.microsoft.com/overview/what-is-paas/) (PaaS) teklifidir.</span><span class="sxs-lookup"><span data-stu-id="e5f73-104">Azure App Service is a fully managed [platform as a service](https://azure.microsoft.com/overview/what-is-paas/) (PaaS) offering for professional developers.</span></span> <span data-ttu-id="e5f73-105">Bu hizmet, web, mobil ve tümleştirme senaryoları için zengin bir özellik kümesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="e5f73-105">The service brings a rich set of capabilities to web, mobile, and integration scenarios.</span></span> 

<span data-ttu-id="e5f73-106">Azure Uygulama Hizmeti’ndeki Mobile Apps özelliği, kurumsal geliştiriciler ve sistem entegratörleri için yüksek düzeyde ölçeklenebilir ve küresel olarak kullanılabilir bir platformdur.</span><span class="sxs-lookup"><span data-stu-id="e5f73-106">The Mobile Apps feature of Azure App Service gives enterprise developers and system integrators a mobile-application development platform that's highly scalable and globally available.</span></span>

![Mobile Apps özelliklerine görsel bir genel bakış](./media/app-service-mobile-value-prop/overview.png)

## <a name="why-mobile-apps"></a><span data-ttu-id="e5f73-108">Neden Mobile Apps?</span><span class="sxs-lookup"><span data-stu-id="e5f73-108">Why Mobile Apps?</span></span>
<span data-ttu-id="e5f73-109">Mobile Apps özelliği ile şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e5f73-109">With the Mobile Apps feature, you can:</span></span>

* <span data-ttu-id="e5f73-110">**Yerel ve platformlar arası uygulamaları oluşturma**: Hem yerel iOS, Android ve Windows uygulamaları hem de platformlar arası Xamarin veya Cordova (Phonegap) uygulamaları oluştururken yerel SDK'ları kullanarak App Service’in avantajlarından faydalanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5f73-110">**Build native and cross-platform apps**: Whether you're building native iOS, Android, and Windows apps or cross-platform Xamarin or Cordova (PhoneGap) apps, you can take advantage of App Service by using native SDKs.</span></span>
* <span data-ttu-id="e5f73-111">**Kuruluş sistemlerinizi bağlama**: Mobile Apps ile dakikalar için kurumsal oturum ekleyebilir ve kuruluşunuzu şirket içi ya da bulut kaynaklarına bağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5f73-111">**Connect to your enterprise systems**: With the Mobile Apps feature, you can add corporate sign-in in minutes, and connect to your enterprise on-premises or cloud resources.</span></span>
* <span data-ttu-id="e5f73-112">**Veri eşitleme ile çevrimdışı kullanılmaya hazır uygulamalar oluşturma**: Kurumsal veri kaynaklarınız ya da hizmet olarak yazılım (SaaS) API’leriniz ile bağlantı bulunduğunda arka planda verileri eşitlemek amacıyla çevrimdışı çalışan ve Mobile Apps kullanan uygulamalar oluşturarak mobil iş gücünüzü verimli kılın.</span><span class="sxs-lookup"><span data-stu-id="e5f73-112">**Build offline-ready apps with data sync**: Make your mobile workforce more productive by building apps that work offline, and use Mobile Apps to sync data in the background when connectivity is present with any of your enterprise data sources or software as a service (SaaS) APIs.</span></span>
* <span data-ttu-id="e5f73-113">**Milyonlarca kişiye Anında İletme Bildirimleri**: her cihazda, kendi ihtiyaçlarına özel ve doğru zamanda gönderilen anında iletme bildirimleriyle müşterilerinizle etkileşim kurun.</span><span class="sxs-lookup"><span data-stu-id="e5f73-113">**Push notifications to millions in seconds**: Engage your customers with instant push notifications on any device, personalized to their needs and sent when the time is right.</span></span>

## <a name="mobile-apps-features"></a><span data-ttu-id="e5f73-114">Mobile Apps özellikleri</span><span class="sxs-lookup"><span data-stu-id="e5f73-114">Mobile Apps features</span></span>
<span data-ttu-id="e5f73-115">Aşağıdaki özellikler, bulut etkin mobil geliştirme için önemlidir:</span><span class="sxs-lookup"><span data-stu-id="e5f73-115">The following features are important to cloud-enabled mobile development:</span></span>

* <span data-ttu-id="e5f73-116">**Kimlik doğrulama ve yetkilendirme**: Azure Active Directory dahil, sürekli büyüyen bir kurumsal kimlik sağlayıcısı listesinden ve Facebook, Google, Twitter ve Microsoft Hesabı gibi sosyal sağlayıcılardan seçim yapın.</span><span class="sxs-lookup"><span data-stu-id="e5f73-116">**Authentication and authorization**: Select from an ever-growing list of identity providers, including Azure Active Directory for enterprise authentication, plus social providers such as Facebook, Google, Twitter, and Microsoft accounts.</span></span> <span data-ttu-id="e5f73-117">Mobile Apps tüm sağlayıcılar için bir OAuth 2.0 hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="e5f73-117">Mobile Apps offers an OAuth 2.0 service for each provider.</span></span> <span data-ttu-id="e5f73-118">Ayrıca sağlayıcıya özel işlev için kimlik sağlayıcısına SDK tümleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5f73-118">You can also integrate the SDK for the identity provider for provider-specific functionality.</span></span>

    <span data-ttu-id="e5f73-119">[Kimlik doğrulama özelliklerimiz] hakkında daha fazlasını keşfedin.</span><span class="sxs-lookup"><span data-stu-id="e5f73-119">Discover more about our [authentication features].</span></span>

* <span data-ttu-id="e5f73-120">**Veri erişimi**: Azure Mobile Apps, Azure SQL Veritabanı’na ya da şirket içi bir SQL Sunucusu’na bağlı, mobil kullanıma uygun bir OData v3 veri kaynağı sağlar.</span><span class="sxs-lookup"><span data-stu-id="e5f73-120">**Data access**: Mobile Apps provides a mobile-friendly OData v3 data source that's linked to Azure SQL Database or an on-premises SQL server.</span></span> <span data-ttu-id="e5f73-121">Bu hizmet, [Azure Tablo depolama], MongoDB ve [Azure Cosmos DB]’nin yanı sıra Office 365 ve Salesforce.com gibi SaaS API’si sağlayıcıları dahil, diğer NoSQL ve SQL veri sağlayıcılarıyla kolayca tümleştirmenizi sağlayarak Entity Framework’ü temel alabilir.</span><span class="sxs-lookup"><span data-stu-id="e5f73-121">Because this service can be based on Entity Framework, you can easily integrate with other NoSQL and SQL data providers, including [Azure Table storage], MongoDB, [Azure Cosmos DB], and SaaS API providers such as Office 365 and Salesforce.com.</span></span>

* <span data-ttu-id="e5f73-122">**Çevrimdışı eşitleme**: İstemci SDK’miz çevrimdışı bir veri kümesi ile çalışan sağlam ve esnek mobil uygulamalar oluşturmanızı kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="e5f73-122">**Offline sync**: Our client SDKs make it easy to build robust and responsive mobile applications that operate with an offline dataset.</span></span> <span data-ttu-id="e5f73-123">Bu veri kümesini, çakışma çözümü desteği de dahil olmak üzere arka uç verileriyle otomatik olarak eşitleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5f73-123">You can sync this dataset automatically with the back-end data, including conflict-resolution support.</span></span>

  <span data-ttu-id="e5f73-124">[veri özellikleri] hakkında daha fazlasını keşfedin.</span><span class="sxs-lookup"><span data-stu-id="e5f73-124">Discover more about our [data features].</span></span>

* <span data-ttu-id="e5f73-125">**Anında İletme Bildirimleri**: İstemci SDK'mız, aynı anda milyonlarca kullanıcıya anında iletme bildirimleri göndermenizi sağlayarak, Azure Notification Hubs'ın kayıt özellikleriyle sorunsuz şekilde tümleşir.</span><span class="sxs-lookup"><span data-stu-id="e5f73-125">**Push notifications**: Our client SDKs integrate seamlessly with the registration capabilities of Azure Notification Hubs, so you can send push notifications to millions of users simultaneously.</span></span>

  <span data-ttu-id="e5f73-126">[anında iletme bildirimi özellikleri] hakkında daha fazlasını keşfedin.</span><span class="sxs-lookup"><span data-stu-id="e5f73-126">Discover more about our [push notification features].</span></span>

* <span data-ttu-id="e5f73-127">**İstemci SDK'ları**: Yerel geliştirmeyi ([iOS], [Android] ve [Windows]), platformlar arası geliştirmeyi ([Xamarin.iOS ve Xamarin.Android], [Xamarin.Forms]) ve karma uygulama geliştirmeyi ([Apache Cordova]) kapsayan SDK'ların eksiksiz bir kümesini sunuyoruz </span><span class="sxs-lookup"><span data-stu-id="e5f73-127">**Client SDKs**: We provide a complete set of client SDKs that cover native development ([iOS], [Android], and [Windows]), cross-platform development ([Xamarin.iOS and Xamarin.Android], [Xamarin.Forms]), and hybrid application development ([Apache Cordova]).</span></span> <span data-ttu-id="e5f73-128">Her istemci SDK’sı ile bir MIT lisansı ile birlikte sunulur ve açık kaynaklıdır.</span><span class="sxs-lookup"><span data-stu-id="e5f73-128">Each client SDK is available with an MIT license and is open source.</span></span>

## <a name="azure-app-service-features"></a><span data-ttu-id="e5f73-129">Azure Uygulama Hizmeti özellikleri</span><span class="sxs-lookup"><span data-stu-id="e5f73-129">Azure App Service features</span></span>
<span data-ttu-id="e5f73-130">Aşağıdaki platform özellikleri mobil üretim siteleri için yararlıdır:</span><span class="sxs-lookup"><span data-stu-id="e5f73-130">The following platform features are useful for mobile production sites:</span></span>

* <span data-ttu-id="e5f73-131">**Otomatik ölçeklendirme**: App Service’i kullanarak gelen müşteri yükünü işlemek için hızlı şekilde ölçeği artırabilir ya da genişletebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5f73-131">**Autoscaling**: With App Service, you can quickly scale up or scale out to handle any incoming customer load.</span></span> <span data-ttu-id="e5f73-132">Yük ya da zamanlama temelinden mobil uygulamanızın arka ucunu ölçeklendirmek için VM’nin sayısını ya da boyutunu el ile seçin ya da otomatik ölçeklendirmeyi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e5f73-132">Manually select the number and size of VMs, or set up autoscaling to scale your mobile-app back end based on load or schedule.</span></span>

  <span data-ttu-id="e5f73-133">[Otomatik ölçeklendirme] hakkında daha fazlasını keşfedin.</span><span class="sxs-lookup"><span data-stu-id="e5f73-133">Discover more about [autoscaling].</span></span>

* <span data-ttu-id="e5f73-134">**Hazırlık ortamları**: App Service, yeni arka ucun daha büyük bir DevOps planının parçası olarak test olan A/B testini ve yerinde hazırlanmasını gerçekleştirmenizi sağlayarak, sitenizin birden fazla sürümünü çalıştırabilir.</span><span class="sxs-lookup"><span data-stu-id="e5f73-134">**Staging environments**: App Service can run multiple versions of your site, so you can perform A/B testing, test in production as part of a larger DevOps plan, and do in-place staging of a new back end.</span></span>

  <span data-ttu-id="e5f73-135">[hazırlık ortamları] hakkında daha fazlasını keşfedin.</span><span class="sxs-lookup"><span data-stu-id="e5f73-135">Discover more about [staging environments].</span></span>

* <span data-ttu-id="e5f73-136">**Sürekli dağıtım**: App Service, SCM sisteminizin bir dalına ileterek arka ucunuzun yeni bir sürümü otomatik olarak oluşturmanızı sağlayarak, ortak tedarik zinciri yönetimi (SCM) sistemleriyle tümleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="e5f73-136">**Continuous deployment**: App Service can integrate with common supply chain management (SCM) systems, so you can automatically deploy a new version of your back end by pushing to a branch of your SCM system.</span></span>

  <span data-ttu-id="e5f73-137">[dağıtım seçenekleri] hakkında daha fazlasını keşfedin.</span><span class="sxs-lookup"><span data-stu-id="e5f73-137">Discover more about [deployment options].</span></span>

* <span data-ttu-id="e5f73-138">**Sanal Ağ**: App Service; sanal ağ, Azure ExpressRoute ya da karma bağlantılar kullanarak şirket içi kaynaklara bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="e5f73-138">**Virtual networking**: App Service can connect to on-premises resources by using virtual network, Azure ExpressRoute, or hybrid connections.</span></span>

  <span data-ttu-id="e5f73-139">[karma bağlantılar], [sanal ağlar], ve [ExpressRoute] hakkında daha fazlasını keşfedin.</span><span class="sxs-lookup"><span data-stu-id="e5f73-139">Discover more about [hybrid connections], [virtual networks], and [ExpressRoute].</span></span>

* <span data-ttu-id="e5f73-140">**Yalıtılmış ve ayrılmış ortamlar**: App Service, Azure Uygulama Hizmeti uygulamalarını yüksek ölçekte güvenli bir şekilde çalıştırılmaları için tam yalıtılmış ve ayrılmış bir ortamda çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="e5f73-140">**Isolated and dedicated environments**: You can run App Service in a fully isolated and dedicated environment for securely running Azure App Service apps at high scale.</span></span> <span data-ttu-id="e5f73-141">Bu ortam, büyük ölçekli, yalıtım veya güvenli ağ erişimi gerektiren uygulama iş yükleri için idealdir.</span><span class="sxs-lookup"><span data-stu-id="e5f73-141">This environment is ideal for application workloads that require high scale, isolation, or secure network access.</span></span>

  <span data-ttu-id="e5f73-142">[App Service ortamları] hakkında daha fazlasını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="e5f73-142">Discover more about [App Service environments].</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5f73-143">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e5f73-143">Next steps</span></span>

<span data-ttu-id="e5f73-144">Azure Uygulama Hizmeti'nde Mobile Apps kullanmaya başlamak için [başlarken] öğreticisini tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="e5f73-144">To get started with Mobile Apps in Azure App Service, complete the [getting started] tutorial.</span></span> <span data-ttu-id="e5f73-145">Bu öğretici, tercih ettiğiniz mobil arka ucu ve istemciyi oluşturma konusunda temel kavramları kapsar.</span><span class="sxs-lookup"><span data-stu-id="e5f73-145">The tutorial covers the basics of producing a mobile back end and client of your choice.</span></span> <span data-ttu-id="e5f73-146">Ayrıca kimlik doğrulama, çevrimdışı eşitleme ve anında iletme bildirimlerini tümleştirme konularını ele alır.</span><span class="sxs-lookup"><span data-stu-id="e5f73-146">It also covers integrating authentication, offline sync, and push notifications.</span></span> <span data-ttu-id="e5f73-147">Öğreticiyi her istemci uygulaması için birden çok kez tamamlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e5f73-147">You can complete the tutorial multiple times, once for each client application.</span></span>

<span data-ttu-id="e5f73-148">Mobile Apps hakkında daha fazla bilgi için [öğrenme haritamızı] gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="e5f73-148">For more information about Mobile Apps, review our [learning map].</span></span>
<span data-ttu-id="e5f73-149">Azure Uygulama Hizmeti platformu hakkında daha fazla bilgi için bkz. [Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="e5f73-149">For more information about the Azure App Service platform, see [Azure App Service].</span></span>

<!-- URLs. -->
[Migrate your mobile service to App Service]: app-service-mobile-migrating-from-mobile-services.md
[Azure App Service]: ../app-service/app-service-value-prop-what-is.md
[başlarken]: app-service-mobile-ios-get-started.md
[Azure Tablo depolama]:../cosmos-db/table-storage-how-to-use-dotnet.md
[Azure Cosmos DB]: ../cosmos-db/documentdb-get-started.md
[Kimlik doğrulama özelliklerimiz]: ./app-service-mobile-auth.md
[veri özellikleri]: ./app-service-mobile-offline-data-sync.md
[anında iletme bildirimi özellikleri]: ../notification-hubs/notification-hubs-push-notification-overview.md
[iOS]: ./app-service-mobile-ios-how-to-use-client-library.md
[Android]: ./app-service-mobile-android-how-to-use-client-library.md
[Windows]: ./app-service-mobile-dotnet-how-to-use-client-library.md
[Xamarin.iOS ve Xamarin.Android]: ./app-service-mobile-dotnet-how-to-use-client-library.md
[Xamarin.Forms]: ./app-service-mobile-xamarin-forms-get-started.md
[Apache Cordova]: ./app-service-mobile-cordova-how-to-use-client-library.md
[Otomatik ölçeklendirme]: ../app-service-web/web-sites-scale.md
[hazırlık ortamları]: ../app-service-web/web-sites-staged-publishing.md
[dağıtım seçenekleri]: ../app-service-web/web-sites-deploy.md
[karma bağlantılar]: ../app-service-web/web-sites-hybrid-connection-get-started.md
[sanal ağlar]: ../app-service-web/web-sites-integrate-with-vnet.md
[ExpressRoute]: ../app-service-web/app-service-app-service-environment-network-configuration-expressroute.md
[App Service ortamları]: ../app-service-web/app-service-app-service-environment-intro.md
[öğrenme haritamızı]: https://azure.microsoft.com/en-us/documentation/learning-paths/appservice-mobileapps/
