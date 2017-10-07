---
title: "aaaMonitoring kullanım ve Windows Masaüstü uygulamaları için performansı"
description: "HockeyApp ve Application Insights ile Windows masaüstü uygulamanızın kullanımını ve performansını analiz edin."
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: 19040746-3315-47e7-8c60-4b3000d2ddc4
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/26/2016
ms.author: bwren
ms.openlocfilehash: 73806885a6f0ed3896c0e43308c90ba087007887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-usage-and-performance-in-windows-desktop-apps"></a>Windows Masaüstü uygulamalarında kullanımı ve performansı izleme


[Azure Application Insights](app-insights-overview.md) ve [HockeyApp](https://hockeyapp.net), dağıttığınız uygulamanın kullanımını ve performansını izlemenize imkan tanır.

> [!IMPORTANT]
> Öneririz [HockeyApp](https://hockeyapp.net) toodistribute ve İzleyici Masaüstü ve cihaz uygulamalar. HockeyApp ile dağıtımı, canlı testleri ve kullanıcı geri bildirimini yönetmenin yanı sıra kullanımı ve kilitlenme raporlarını izleyebilirsiniz. Ayrıca, [telemetrinizi dışarı aktarıp Analytics ile sorgulayabilirsiniz](app-insights-hockeyapp-bridge-app.md).
> 
> Bir masaüstü uygulamasından telemetri tooApplication Öngörüler gönderilip bu chiefly olsa da hata ayıklama ve Deneysel amaçları için yararlıdır.
> 
> 

## <a name="toosend-telemetry-tooapplication-insights-from-a-windows-application"></a>bir Windows uygulamasında toosend telemetri tooApplication Öngörüler
1. Merhaba, [Azure portal](https://portal.azure.com), [bir Application Insights kaynağı oluşturma](app-insights-create-new-resource.md). Uygulama türü olarak ASP.NET uygulamasını seçin.
2. Merhaba izleme anahtarını bir kopyasını alın. Başlangıç anahtarı Essentials hello yeni kaynak oluşturduğunuz aşağı açılan hello bulun. 
3. Visual Studio'da Uygulama projenizin hello NuGet paketlerini düzenleyin ve Microsoft.ApplicationInsights.WindowsServer ekleyin. (Veya Microsoft.ApplicationInsights hello standart telemetri koleksiyonu modülleri olmadan tam API hello yalnızca istiyorsanız seçin.)
4. Merhaba izleme anahtarı ya da kodunuzu ayarlayın:
   
    `TelemetryConfiguration.Active.InstrumentationKey = "` *anahtarınız* `";` 
   
    veya (Merhaba standart telemetri paketlerden birini yüklediyseniz) Applicationınsights.config:
   
    `<InstrumentationKey>`*anahtarınız*`</InstrumentationKey>` 
   
    Applicationınsights.config kullanırsanız, Çözüm Gezgini'nde özelliklerini çok ayarlanmadığından emin olun**yapı eylemi içerik, kopya tooOutput dizin = kopyalama =**.
5. [Merhaba API kullanan](app-insights-api-custom-events-metrics.md) toosend telemetri.
6. Uygulamanızı çalıştırmak ve hello telemetri hello Azure portalında oluşturduğunuz hello kaynak görebilirsiniz.

## <a name="telemetry"></a>Örnek kod
```C#

    public partial class Form1 : Form
    {
        private TelemetryClient tc = new TelemetryClient();
        ...
        private void Form1_Load(object sender, EventArgs e)
        {
            // Alternative toosetting ikey in config file:
            tc.InstrumentationKey = "key copied from portal";

            // Set session data:
            tc.Context.User.Id = Environment.UserName;
            tc.Context.Session.Id = Guid.NewGuid().ToString();
            tc.Context.Device.OperatingSystem = Environment.OSVersion.ToString();

            // Log a page view:
            tc.TrackPageView("Form1");
            ...
        }

        protected override void OnClosing(CancelEventArgs e)
        {
            stop = true;
            if (tc != null)
            {
                tc.Flush(); // only for desktop apps

                // Allow time for flushing:
                System.Threading.Thread.Sleep(1000);
            }
            base.OnClosing(e);
        }

```

## <a name="next-steps"></a>Sonraki adımlar
* [Pano oluşturma](app-insights-dashboards.md)
* [Tanılama Araması](app-insights-diagnostic-search.md)
* [Ölçümleri keşfetme](app-insights-metrics-explorer.md)
* [Analytics sorguları yazma](app-insights-analytics.md)

