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
#  <a name="sending-user-context-tooenable-usage-experiences-in-azure-application-insights"></a>Azure Application Insights'ta gönderen kullanıcı bağlamı tooenable kullanımı deneyimleri

## <a name="tracking-users"></a>Kullanıcıları izleme

Application Insights, toomonitor sağlar ve kullanıcılarınızın ürün kullanım araçlar aracılığıyla izleyebilirsiniz: 
* [Kullanıcılar, Oturumlar, Etkinlikler](https://docs.microsoft.com/azure/application-insights/app-insights-usage-segmentation)
* [Huniler](https://docs.microsoft.com/azure/application-insights/usage-funnels)
* [Bekletme](https://docs.microsoft.com/azure/application-insights/app-insights-usage-retention)
* Cohorts
* [Çalışma kitapları](https://docs.microsoft.com/azure/application-insights/app-insights-usage-workbooks)

Zaman içinde ne bir kullanıcı mu sipariş tootrack içinde Application Insights her kullanıcı veya oturum kimliği gerekir. Bu kimlikleri her özel olay veya sayfa görünümünde içerir.
- Kullanıcılar, Funnels, bekletme ve Cohorts: kullanıcı kimliğini de ekleyin.
- Oturumlar: oturum kimliğini de ekleyin.

Uygulamanız ile Merhaba bütünleştirdiyseniz [JavaScript SDK'sı](https://docs.microsoft.com/azure/application-insights/app-insights-javascript#set-up-application-insights-for-your-web-page), kullanıcı Kimliğini otomatik olarak izlenir.

## <a name="choosing-user-ids"></a>Kullanıcı kimliklerini seçme

Kullanıcı kimlikleri, kullanıcıların zaman içinde nasıl davranacağını kullanıcı oturumları tootrack arasında kalıcı. Kalıcı hello kimliği için çeşitli yaklaşım vardır
- Hizmetinizi zaten bir kullanıcı tanımı.
- Merhaba hizmet tooa tarayıcı erişimi varsa, onu hello tarayıcı bir Kimliğe sahip bir tanımlama bilgisi içinde geçirebilirsiniz. Merhaba tanımlama bilgisi hello kullanıcının tarayıcısında kaldığı sürece hello kimliği için korunur.
- Gerekirse, yeni bir kimliği her oturum kullanabilirsiniz, ancak kullanıcılar hakkında hello sonuçları sınırlı olacaktır. Örneğin, bir kullanıcının davranışına zamanla nasıl değiştiğini mümkün toosee olmayacaktır.

Merhaba kimliği bir GUID olmalıdır veya başka bir dize yeterince karmaşık tooidentify her kullanıcının benzersiz olarak. Örneğin, uzun rastgele bir sayı olabilir.

Merhaba kimliği hello kullanıcıyla ilgili kişisel tanımlama bilgileri içeriyorsa, bunu uygun değere toosend tooApplication Öngörüler bir kullanıcı kimliği değil Böyle bir kimlik olarak gönderdiğiniz bir [kimliği doğrulanmış kullanıcı kimliği](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#authenticated-users), ancak kullanım senaryoları için hello kullanıcı kimliği gereksinimi yerine getirmiyor.

## <a name="aspnet-apps-set-user-context-in-an-itelemetryinitializer"></a>ASP.NET uygulamaları: kullanıcı bağlamı bir ITelemetryInitializer ayarlayın.

Ayrıntılı olarak açıklandığı gibi bir telemetri Başlatıcı oluşturun [burada](https://docs.microsoft.com/azure/application-insights/app-insights-api-filtering-sampling#add-properties-itelemetryinitializer), Context.User.Id hello ve Context.Session.Id hello ayarlanır.

Bu örnek süresi hello oturumun ardından dolar hello kullanıcı kimliği tooan tanımlayıcısı ayarlar. Mümkünse, oturumlar arasında devam eden bir kullanıcı kimliği kullanın.

*C#*

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

## <a name="next-steps"></a>Sonraki adımlar
- tooenable kullanımı deneyimleri, göndermeye Başla [özel olaylar](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) veya [sayfa görünümleri](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).
- Özel olaylar ya da sayfa görünümleri keşfedin hello kullanım araçları toolearn zaten gönderirseniz kullanıcılar hizmetinizi kullanma.
    * [Kullanıma genel bakış](app-insights-usage-overview.md)
    * [Kullanıcıları, oturumlar ve olaylar](app-insights-usage-segmentation.md)
    * [Huniler](usage-funnels.md)
    * [Bekletme](app-insights-usage-retention.md)
    * [Çalışma kitapları](app-insights-usage-workbooks.md)
