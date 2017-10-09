---
title: "Azure Application Insights'ta aaaSending kullanıcı bağlamı tooenable kullanımı deneyimleri | Microsoft Docs"
description: "Bunların her biri benzersiz, kalıcı bir kimlik dizesi Application ınsights'ta atadıktan sonra kullanıcıların hizmeti aracılığıyla nasıl hareket izler."
services: application-insights
documentationcenter: 
author: abgreg
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: csharp
ms.topic: article
ms.date: 08/02/2017
ms.author: bwren
ms.openlocfilehash: 0e6c2348f53a3ea970060334179b0dd070925e82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
#  <a name="sending-user-context-tooenable-usage-experiences-in-azure-application-insights"></a><span data-ttu-id="440fd-103">Azure Application Insights'ta gönderen kullanıcı bağlamı tooenable kullanımı deneyimleri</span><span class="sxs-lookup"><span data-stu-id="440fd-103">Sending user context tooenable usage experiences in Azure Application Insights</span></span>

## <a name="tracking-users"></a><span data-ttu-id="440fd-104">Kullanıcıları izleme</span><span class="sxs-lookup"><span data-stu-id="440fd-104">Tracking users</span></span>

<span data-ttu-id="440fd-105">Application Insights, toomonitor sağlar ve kullanıcılarınızın ürün kullanım araçlar aracılığıyla izleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="440fd-105">Application Insights enables you toomonitor and track your users through a set of product usage tools:</span></span> 
* [<span data-ttu-id="440fd-106">Kullanıcılar, Oturumlar, Etkinlikler</span><span class="sxs-lookup"><span data-stu-id="440fd-106">Users, Sessions, Events</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-segmentation)
* [<span data-ttu-id="440fd-107">Huniler</span><span class="sxs-lookup"><span data-stu-id="440fd-107">Funnels</span></span>](https://docs.microsoft.com/azure/application-insights/usage-funnels)
* [<span data-ttu-id="440fd-108">Bekletme</span><span class="sxs-lookup"><span data-stu-id="440fd-108">Retention</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-retention)
* <span data-ttu-id="440fd-109">Cohorts</span><span class="sxs-lookup"><span data-stu-id="440fd-109">Cohorts</span></span>
* [<span data-ttu-id="440fd-110">Çalışma kitapları</span><span class="sxs-lookup"><span data-stu-id="440fd-110">Workbooks</span></span>](https://docs.microsoft.com/azure/application-insights/app-insights-usage-workbooks)

<span data-ttu-id="440fd-111">Zaman içinde ne bir kullanıcı mu sipariş tootrack içinde Application Insights her kullanıcı veya oturum kimliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="440fd-111">In order tootrack what a user does over time, Application Insights needs an ID for each user or session.</span></span> <span data-ttu-id="440fd-112">Bu kimlikleri her özel olay veya sayfa görünümünde içerir.</span><span class="sxs-lookup"><span data-stu-id="440fd-112">Include these IDs in every custom event or page view.</span></span>
- <span data-ttu-id="440fd-113">Kullanıcılar, Funnels, bekletme ve Cohorts: kullanıcı kimliğini de ekleyin.</span><span class="sxs-lookup"><span data-stu-id="440fd-113">Users, Funnels, Retention, and Cohorts: Include user ID.</span></span>
- <span data-ttu-id="440fd-114">Oturumlar: oturum kimliğini de ekleyin.</span><span class="sxs-lookup"><span data-stu-id="440fd-114">Sessions: Include session ID.</span></span>

<span data-ttu-id="440fd-115">Uygulamanız ile Merhaba bütünleştirdiyseniz [JavaScript SDK'sı](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), kullanıcı Kimliğini otomatik olarak izlenir.</span><span class="sxs-lookup"><span data-stu-id="440fd-115">If your app is integrated with hello [JavaScript SDK](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), user ID is tracked automatically.</span></span>

## <a name="choosing-user-ids"></a><span data-ttu-id="440fd-116">Kullanıcı kimliklerini seçme</span><span class="sxs-lookup"><span data-stu-id="440fd-116">Choosing user IDs</span></span>

<span data-ttu-id="440fd-117">Kullanıcı kimlikleri, kullanıcıların zaman içinde nasıl davranacağını kullanıcı oturumları tootrack arasında kalıcı.</span><span class="sxs-lookup"><span data-stu-id="440fd-117">User IDs should persist across user sessions tootrack how users behave over time.</span></span> <span data-ttu-id="440fd-118">Kalıcı hello kimliği için çeşitli yaklaşım vardır</span><span class="sxs-lookup"><span data-stu-id="440fd-118">There are various approaches for persisting hello ID.</span></span>
- <span data-ttu-id="440fd-119">Hizmetinizi zaten bir kullanıcı tanımı.</span><span class="sxs-lookup"><span data-stu-id="440fd-119">A definition of a user that you already have in your service.</span></span>
- <span data-ttu-id="440fd-120">Merhaba hizmet tooa tarayıcı erişimi varsa, onu hello tarayıcı bir Kimliğe sahip bir tanımlama bilgisi içinde geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="440fd-120">If hello service has access tooa browser, it can pass hello browser a cookie with an ID in it.</span></span> <span data-ttu-id="440fd-121">Merhaba tanımlama bilgisi hello kullanıcının tarayıcısında kaldığı sürece hello kimliği için korunur.</span><span class="sxs-lookup"><span data-stu-id="440fd-121">hello ID will persist for as long as hello cookie remains in hello user's browser.</span></span>
- <span data-ttu-id="440fd-122">Gerekirse, yeni bir kimliği her oturum kullanabilirsiniz, ancak kullanıcılar hakkında hello sonuçları sınırlı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="440fd-122">If necessary, you can use a new ID each session, but hello results about users will be limited.</span></span> <span data-ttu-id="440fd-123">Örneğin, bir kullanıcının davranışına zamanla nasıl değiştiğini mümkün toosee olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="440fd-123">For example, you won't be able toosee how a user's behavior changes over time.</span></span>

<span data-ttu-id="440fd-124">Merhaba kimliği bir GUID olmalıdır veya başka bir dize yeterince karmaşık tooidentify her kullanıcının benzersiz olarak.</span><span class="sxs-lookup"><span data-stu-id="440fd-124">hello ID should be a Guid or another string complex enough tooidentify each user uniquely.</span></span> <span data-ttu-id="440fd-125">Örneğin, uzun rastgele bir sayı olabilir.</span><span class="sxs-lookup"><span data-stu-id="440fd-125">For example, it could be a long random number.</span></span>

<span data-ttu-id="440fd-126">Merhaba kimliği hello kullanıcıyla ilgili kişisel tanımlama bilgileri içeriyorsa, bunu uygun değere toosend tooApplication Öngörüler bir kullanıcı kimliği değil</span><span class="sxs-lookup"><span data-stu-id="440fd-126">If hello ID contains personally identifying information about hello user, it is not an appropriate value toosend tooApplication Insights as a user ID.</span></span> <span data-ttu-id="440fd-127">Böyle bir kimlik olarak gönderdiğiniz bir [kimliği doğrulanmış kullanıcı kimliği](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), ancak kullanım senaryoları için hello kullanıcı kimliği gereksinimi yerine getirmiyor.</span><span class="sxs-lookup"><span data-stu-id="440fd-127">You can send such an ID as an [authenticated user ID](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), but it does not fulfill hello user ID requirement for usage scenarios.</span></span>

## <a name="aspnet-apps-set-user-context-in-an-itelemetryinitializer"></a><span data-ttu-id="440fd-128">ASP.NET uygulamaları: kullanıcı bağlamı bir ITelemetryInitializer ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="440fd-128">ASP.NET Apps: Set user context in an ITelemetryInitializer</span></span>

<span data-ttu-id="440fd-129">Ayrıntılı olarak açıklandığı gibi bir telemetri Başlatıcı oluşturun [burada](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer), Context.User.Id hello ve Context.Session.Id hello ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="440fd-129">Create a telemetry initializer, as described in detail [here](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer), and set hello Context.User.Id and hello Context.Session.Id.</span></span>

<span data-ttu-id="440fd-130">Bu örnek süresi hello oturumun ardından dolar hello kullanıcı kimliği tooan tanımlayıcısı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="440fd-130">This example sets hello user ID tooan identifier that expires after hello session.</span></span> <span data-ttu-id="440fd-131">Mümkünse, oturumlar arasında devam eden bir kullanıcı kimliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="440fd-131">If possible, use a user ID that persists across sessions.</span></span>

<span data-ttu-id="440fd-132">*C#*</span><span class="sxs-lookup"><span data-stu-id="440fd-132">*C#*</span></span>

```C#

    using System;
    using System.Web;
    using Microsoft.ApplicationInsights.Channel;
    using Microsoft.ApplicationInsights.Extensibility;

    namespace MvcWebRole.Telemetry
    {
      /*
       * Custom TelemetryInitializer that sets hello user ID.
       *
       */
      public class MyTelemetryInitializer : ITelemetryInitializer
      {
        public void Initialize(ITelemetry telemetry)
        {
            // For a full experience, track each user across sessions. For an incomplete view of user 
            // behavior within a session, store user ID on hello HttpContext Session.
            // Set hello user ID if we haven't done so yet.
            if (HttpContext.Current.Session["UserId"] == null)
            {
                HttpContext.Current.Session["UserId"] = Guid.NewGuid();
            }

            // Set hello user id on hello Application Insights telemetry item.
            telemetry.Context.User.Id = (string)HttpContext.Current.Session["UserId"];

            // Set hello session id on hello Application Insights telemetry item.
            telemetry.Context.Session.Id = HttpContext.Current.Session.SessionID;
        }
      }
    }
```

## <a name="next-steps"></a><span data-ttu-id="440fd-133">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="440fd-133">Next steps</span></span>
- <span data-ttu-id="440fd-134">tooenable kullanımı deneyimleri, göndermeye Başla [özel olaylar](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) veya [sayfa görünümleri](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span><span class="sxs-lookup"><span data-stu-id="440fd-134">tooenable usage experiences, start sending [custom events](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) or [page views](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).</span></span>
- <span data-ttu-id="440fd-135">Özel olaylar ya da sayfa görünümleri keşfedin hello kullanım araçları toolearn zaten gönderirseniz kullanıcılar hizmetinizi kullanma.</span><span class="sxs-lookup"><span data-stu-id="440fd-135">If you already send custom events or page views, explore hello Usage tools toolearn how users use your service.</span></span>
    * [<span data-ttu-id="440fd-136">Kullanıma genel bakış</span><span class="sxs-lookup"><span data-stu-id="440fd-136">Usage overview</span></span>](app-insights-usage-overview.md)
    * [<span data-ttu-id="440fd-137">Kullanıcıları, oturumlar ve olaylar</span><span class="sxs-lookup"><span data-stu-id="440fd-137">Users, Sessions, and Events</span></span>](app-insights-usage-segmentation.md)
    * [<span data-ttu-id="440fd-138">Huniler</span><span class="sxs-lookup"><span data-stu-id="440fd-138">Funnels</span></span>](usage-funnels.md)
    * [<span data-ttu-id="440fd-139">Bekletme</span><span class="sxs-lookup"><span data-stu-id="440fd-139">Retention</span></span>](app-insights-usage-retention.md)
    * [<span data-ttu-id="440fd-140">Çalışma kitapları</span><span class="sxs-lookup"><span data-stu-id="440fd-140">Workbooks</span></span>](app-insights-usage-workbooks.md)
