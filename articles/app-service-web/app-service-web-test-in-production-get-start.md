---
title: "Web Apps ile üretim testine başlayın"
description: "Azure App Service Web Apps üretim (TIP) özelliğinde testi hakkında bilgi edinin."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 4623468d-886e-4203-8012-8f86deb2790b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: cephalin
ms.openlocfilehash: 9f38b635140cacf0513c75385bce3c110a930969
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-test-in-production-for-web-apps"></a><span data-ttu-id="c3f02-103">Web Apps ile üretim testine başlayın</span><span class="sxs-lookup"><span data-stu-id="c3f02-103">Get started with test in production for Web Apps</span></span>
<span data-ttu-id="c3f02-104">Üretimde test ya da canlı web uygulamanızı gerçek müşteri trafiğinden kullanarak sınama olan uygulama geliştiriciler giderek kolay bir şekilde entegre bir test stratejisi kendi [Çevik Geliştirme](https://en.wikipedia.org/wiki/Agile_software_development) Metodoloji.</span><span class="sxs-lookup"><span data-stu-id="c3f02-104">Testing in production, or live-testing your web app using live customer traffic, is a test strategy that app developers increasingly integrate into their [agile development](https://en.wikipedia.org/wiki/Agile_software_development) methodology.</span></span> <span data-ttu-id="c3f02-105">Bir test ortamında birleştirilen verileri aksine, üretim ortamında test uygulamalarınızı dinamik kullanıcı trafiği ile kalitesi sağlar.</span><span class="sxs-lookup"><span data-stu-id="c3f02-105">It enables you to test the quality of your apps with live user traffic in your production environment, as opposed to synthesized data in a test environment.</span></span> <span data-ttu-id="c3f02-106">Yeni uygulamanızı gerçek kullanıcılara göstererek dağıtıldıktan sonra uygulamanızı karşılaşabilecekleri gerçek sorunlar hakkında haberdar olmak.</span><span class="sxs-lookup"><span data-stu-id="c3f02-106">By exposing your new app to real users, you can be informed on the real problems your app may face once it is deployed.</span></span> <span data-ttu-id="c3f02-107">İşlevselliği, performans ve uygulama güncelleştirmelerinizi birim, hız ve hiçbir zaman bir sınama ortamında yaklaşık gerçek kullanıcı trafiği çeşitli karşı değerini doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3f02-107">You can verify the functionality, performance, and value of your app updates against the volume, velocity, and variety of real user traffic, which you can never approximate in a test environment.</span></span>

## <a name="traffic-routing-in-app-service-web-apps"></a><span data-ttu-id="c3f02-108">App Service Web Apps yönlendirme trafiği</span><span class="sxs-lookup"><span data-stu-id="c3f02-108">Traffic Routing in App Service Web Apps</span></span>
<span data-ttu-id="c3f02-109">Trafik yönlendirme özelliğindeki [Azure uygulama hizmeti](http://go.microsoft.com/fwlink/?LinkId=529714), bir veya daha fazla dinamik kullanıcı trafiğinin bir kısmı yönlendirebilirsiniz [dağıtım yuvaları](web-sites-staged-publishing.md)ve uygulamanızı ile analiz etmek [Azure Application Insights](/services/application-insights/) veya [Azure Hdınsight](/services/hdinsight/), veya bir üçüncü taraf aracı [New Relic](/marketplace/partners/newrelic/newrelic/) değişikliğinizin doğrulamak için.</span><span class="sxs-lookup"><span data-stu-id="c3f02-109">With the Traffic Routing feature in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), you can direct a portion of live user traffic to one or more [deployment slots](web-sites-staged-publishing.md), and then analyze your app with [Azure Application Insights](/services/application-insights/) or [Azure HDInsight](/services/hdinsight/), or a third-party tool like [New Relic](/marketplace/partners/newrelic/newrelic/) to validate your change.</span></span> <span data-ttu-id="c3f02-110">Örneğin, App Service ile aşağıdaki senaryolar uygulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c3f02-110">For example, you can implement the following scenarios with App Service:</span></span>

* <span data-ttu-id="c3f02-111">İşlev hataları bulmaya veya performans sorunları, güncelleştirmelerinin site genelinde dağıtımdan sabitleme</span><span class="sxs-lookup"><span data-stu-id="c3f02-111">Discover functional bugs or pinpoint performance bottlenecks in your updates prior to site-wide deployment</span></span>
* <span data-ttu-id="c3f02-112">Değişikliklerinizi "denetimli test uçuşlar" beta uygulama kullanılabilirlik ölçümleri ölçerek gerçekleştirin</span><span class="sxs-lookup"><span data-stu-id="c3f02-112">Perform "controlled test flights" of your changes by measuring usability metrics on the beta app</span></span>
* <span data-ttu-id="c3f02-113">Aşamalı olarak yeni bir güncelleştirme kadar artırmalarını ve bir hata oluşursa düzgün biçimde geçerli sürüme geri</span><span class="sxs-lookup"><span data-stu-id="c3f02-113">Gradually ramp up to a new update, and gracefully back down to the current version if an error occurs</span></span> 
* <span data-ttu-id="c3f02-114">Çalıştırarak, uygulamanızın iş sonuçları en iyi duruma getirme [A / B testler](https://en.wikipedia.org/wiki/A/B_testing) veya [multivariate testleri](https://en.wikipedia.org/wiki/Multivariate_testing_in_marketing) içinde birden çok dağıtım yuvası</span><span class="sxs-lookup"><span data-stu-id="c3f02-114">Optimize your app's business results by running [A/B tests](https://en.wikipedia.org/wiki/A/B_testing) or [multivariate tests](https://en.wikipedia.org/wiki/Multivariate_testing_in_marketing) in multiple deployment slots</span></span>

### <a name="requirements-for-using-traffic-routing-in-web-apps"></a><span data-ttu-id="c3f02-115">Trafik yönlendirme Web uygulamalarında kullanma gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="c3f02-115">Requirements for using Traffic Routing in Web Apps</span></span>
* <span data-ttu-id="c3f02-116">Web uygulamanızı çalıştırmak gerekir **standart** veya **Premium** birden çok dağıtım yuvası için gerekli olduğundan, katmanı.</span><span class="sxs-lookup"><span data-stu-id="c3f02-116">Your web app must run in **Standard** or **Premium** tier, as it is required for multiple deployment slots.</span></span>
* <span data-ttu-id="c3f02-117">Düzgün çalışması için kullanıcıların tarayıcıda etkinleştirilmesi için tanımlama bilgileri trafik yönlendirme gerektirir.</span><span class="sxs-lookup"><span data-stu-id="c3f02-117">In order to work properly, Traffic Routing requires cookies to be enabled in the users' browser.</span></span> <span data-ttu-id="c3f02-118">Trafik yönlendirme, bir dağıtım yuvası ömrü istemci tarayıcısına istemci oturumu sabitlemek için tanımlama bilgilerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="c3f02-118">Traffic Routing uses cookies to pin a client browser to a deployment slot for the life the client session.</span></span>
* <span data-ttu-id="c3f02-119">Trafik yönlendirme Azure PowerShell cmdlet'leri aracılığıyla Gelişmiş ipucu senaryolarını destekler.</span><span class="sxs-lookup"><span data-stu-id="c3f02-119">Traffic Routing supports advanced TiP scenarios through Azure PowerShell cmdlets.</span></span>

## <a name="route-traffic-segment-to-a-deployment-slot"></a><span data-ttu-id="c3f02-120">Rota trafiği kesimine bir dağıtım yuvası</span><span class="sxs-lookup"><span data-stu-id="c3f02-120">Route traffic segment to a deployment slot</span></span>
<span data-ttu-id="c3f02-121">Her ipucu senaryosu temel düzeyde, bir üretim dışı dağıtım yuvası Canlı trafiğinizi önceden tanımlanmış yüzdesi rota.</span><span class="sxs-lookup"><span data-stu-id="c3f02-121">At the basic level in every TiP scenario, you route a predefined percentage of your live traffic to a non-production deployment slot.</span></span> <span data-ttu-id="c3f02-122">Bunu yapmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="c3f02-122">To do this, follow the steps below:</span></span>

> [!NOTE]
> <span data-ttu-id="c3f02-123">Adımlar burada varsayar sahip olduğunuz bir [üretim dışı dağıtım yuvası](web-sites-staged-publishing.md) ve istenen web uygulama içeriğini zaten olan [dağıtılan](web-sites-deploy.md) ona.</span><span class="sxs-lookup"><span data-stu-id="c3f02-123">The steps here assumes that you already have a [non-production deployment slot](web-sites-staged-publishing.md) and that the desired web app content is already [deployed](web-sites-deploy.md) to it.</span></span>
> 
> 

1. <span data-ttu-id="c3f02-124">İçine oturum [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c3f02-124">Log into the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="c3f02-125">Web uygulamanızın dikey penceresinde tıklayın **ayarları** > **trafik yönlendirme**.</span><span class="sxs-lookup"><span data-stu-id="c3f02-125">In your web app's blade, click **Settings** > **Traffic Routing**.</span></span>
   ![](./media/app-service-web-test-in-production/01-traffic-routing.png)
3. <span data-ttu-id="c3f02-126">Trafiği için ve işlemleriniz ve'ı tıklatın toplam trafiğin yüzde yönlendirmek istediğiniz yuvası seçin **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="c3f02-126">Select the slot that you want to route traffic to and the percentage of the total traffic you desire, then click **Save**.</span></span>
   
    ![](./media/app-service-web-test-in-production/02-select-slot.png)
4. <span data-ttu-id="c3f02-127">Dağıtım yuvanın dikey penceresine gidin.</span><span class="sxs-lookup"><span data-stu-id="c3f02-127">Go to the deployment slot's blade.</span></span> <span data-ttu-id="c3f02-128">Dinamik trafik için yönlendirilen görmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="c3f02-128">You should now see live traffic being routed to it.</span></span>
   
    ![](./media/app-service-web-test-in-production/03-traffic-routed.png)

<span data-ttu-id="c3f02-129">Trafik yönlendirme yapılandırıldıktan sonra istemciler belirtilen yüzdesi, üretim dışı yuvasına rastgele yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="c3f02-129">Once Traffic Routing is configured, the specified percentage of clients will be randomly routed to your non-production slot.</span></span> <span data-ttu-id="c3f02-130">Ancak, istemci otomatik olarak belirli bir yuva yönlendirilir sonra bunu "için bu istemci oturumu için o yuva sabitlenir olduğunu" dikkate almak önemlidir.</span><span class="sxs-lookup"><span data-stu-id="c3f02-130">However, it is important to note that once a client is automatically routed to a specific slot, it will be "pinned" to that slot for the life of that client session.</span></span> <span data-ttu-id="c3f02-131">Bu yapılan kullanıcı oturumunu sabitlemek için bir tanımlama bilgisi kullanarak.</span><span class="sxs-lookup"><span data-stu-id="c3f02-131">This done using a cookie to pin the user session.</span></span> <span data-ttu-id="c3f02-132">HTTP isteklerini inceleyin, bulacaksınız bir `TipMix` sonraki her istekte tanımlama bilgisi.</span><span class="sxs-lookup"><span data-stu-id="c3f02-132">If you inspect the HTTP requests, you will find a `TipMix` cookie in every subsequent request.</span></span>

![](./media/app-service-web-test-in-production/04-tip-cookie.png)

## <a name="force-client-requests-to-a-specific-slot"></a><span data-ttu-id="c3f02-133">İstemci isteklerini belirli bir yuva zorla</span><span class="sxs-lookup"><span data-stu-id="c3f02-133">Force client requests to a specific slot</span></span>
<span data-ttu-id="c3f02-134">Otomatik trafik yönlendirme ek olarak, uygulama hizmeti rota isteklerini belirli bir yuva için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3f02-134">In addition to automatic traffic routing, App Service is able to route requests to a specific slot.</span></span> <span data-ttu-id="c3f02-135">Kullanıcılarınızı opt içine yapılamıyor veya geri çevirin, beta uygulamanızın olarak istediğinizde kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="c3f02-135">This is useful when you want your users to be able to opt-into or opt-out of your beta app.</span></span> <span data-ttu-id="c3f02-136">Bunu yapmak için kullandığınız `x-ms-routing-name` sorgu parametresi.</span><span class="sxs-lookup"><span data-stu-id="c3f02-136">To do this, you use the `x-ms-routing-name` query parameter.</span></span>

<span data-ttu-id="c3f02-137">Belirli yuvası kullanarak kullanıcıların bildirmeksizin `x-ms-routing-name`, yuva trafik yönlendirme listesine zaten eklenmiş olduğundan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c3f02-137">To reroute users to a specific slot using `x-ms-routing-name`, you must make sure that the slot is already added to the Traffic Routing list.</span></span> <span data-ttu-id="c3f02-138">Bir yuva açıkça yönlendirmek istediğiniz olduğundan, ayarladığınız gerçek yönlendirme yüzdesi önemli değildir.</span><span class="sxs-lookup"><span data-stu-id="c3f02-138">Since you want to route to a slot explicitly, the actual routing percentage you set doesn't matter.</span></span> <span data-ttu-id="c3f02-139">İsterseniz, "beta uygulamaya erişmek için tıklatabileceği bir beta bağlantı" hazırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3f02-139">If you want, you can craft a "beta link" that users can click to access the beta app.</span></span>

![](./media/app-service-web-test-in-production/06-enable-x-ms-routing-name.png)

### <a name="opt-users-out-of-beta-app"></a><span data-ttu-id="c3f02-140">Kullanıcılar beta uygulama dışında iptal et</span><span class="sxs-lookup"><span data-stu-id="c3f02-140">Opt users out of beta app</span></span>
<span data-ttu-id="c3f02-141">Beta uygulamanızı dışında opt kullanıcılar izin vermek için örneğin, bu bağlantıyı web sayfanıza koyabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c3f02-141">To let users opt out of your beta app, for example, you can put this link in your web page:</span></span>

    <a href="<webappname>.azurewebsites.net/?x-ms-routing-name=self">Go back to production app</a>

<span data-ttu-id="c3f02-142">Dize `x-ms-routing-name=self` üretim yuvasına belirtir.</span><span class="sxs-lookup"><span data-stu-id="c3f02-142">The string `x-ms-routing-name=self` specifies the production slot.</span></span> <span data-ttu-id="c3f02-143">İstemci tarayıcısı erişim sonra bağlantı, yalnızca üretim yuvasına yönlendirilir, ancak sonraki her istek içerecek `x-ms-routing-name=self` üretim yuvasına oturumuna sabitler tanımlama bilgisi.</span><span class="sxs-lookup"><span data-stu-id="c3f02-143">Once the client browser access the link, not only is it redirected to the production slot, but every subsequent request will contain the `x-ms-routing-name=self` cookie that pins the session to the production slot.</span></span>

![](./media/app-service-web-test-in-production/05-access-production-slot.png)

### <a name="opt-users-in-to-beta-app"></a><span data-ttu-id="c3f02-144">Kullanıcılar beta uygulamasına iptal et</span><span class="sxs-lookup"><span data-stu-id="c3f02-144">Opt users in to beta app</span></span>
<span data-ttu-id="c3f02-145">Beta uygulamanıza kabul kullanıcıların izin vermek için aynı sorgu parametresi örneğin üretim dışı yuva adını ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="c3f02-145">To let users opt in to your beta app, set the same query parameter to the name of the non-production slot, for example:</span></span>

        <webappname>.azurewebsites.net/?x-ms-routing-name=staging

## <a name="more-resources"></a><span data-ttu-id="c3f02-146">Diğer kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c3f02-146">More resources</span></span>
* [<span data-ttu-id="c3f02-147">Hazırlık ortamları için Azure App Service'te web uygulamalarını ayarlama</span><span class="sxs-lookup"><span data-stu-id="c3f02-147">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)
* [<span data-ttu-id="c3f02-148">Azure'nın beklendiği karmaşık bir uygulama dağıtma</span><span class="sxs-lookup"><span data-stu-id="c3f02-148">Deploy a complex application predictably in Azure</span></span>](app-service-deploy-complex-application-predictably.md)
* [<span data-ttu-id="c3f02-149">Azure App Service ile Çevik Yazılım Geliştirme</span><span class="sxs-lookup"><span data-stu-id="c3f02-149">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)
* [<span data-ttu-id="c3f02-150">DevOps ortamları etkili bir şekilde web uygulamaları için kullanın</span><span class="sxs-lookup"><span data-stu-id="c3f02-150">Use DevOps environments effectively for your web apps</span></span>](app-service-web-staged-publishing-realworld-scenarios.md)

