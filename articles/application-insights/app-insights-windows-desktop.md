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
# <a name="monitoring-usage-and-performance-in-windows-desktop-apps"></a><span data-ttu-id="edcb7-103">Windows Masaüstü uygulamalarında kullanımı ve performansı izleme</span><span class="sxs-lookup"><span data-stu-id="edcb7-103">Monitoring usage and performance in Windows Desktop apps</span></span>


<span data-ttu-id="edcb7-104">[Azure Application Insights](app-insights-overview.md) ve [HockeyApp](https://hockeyapp.net), dağıttığınız uygulamanın kullanımını ve performansını izlemenize imkan tanır.</span><span class="sxs-lookup"><span data-stu-id="edcb7-104">[Azure Application Insights](app-insights-overview.md) and [HockeyApp](https://hockeyapp.net) let you monitor your deployed application for usage and performance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="edcb7-105">Öneririz [HockeyApp](https://hockeyapp.net) toodistribute ve İzleyici Masaüstü ve cihaz uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="edcb7-105">We recommend [HockeyApp](https://hockeyapp.net) toodistribute and monitor desktop and device apps.</span></span> <span data-ttu-id="edcb7-106">HockeyApp ile dağıtımı, canlı testleri ve kullanıcı geri bildirimini yönetmenin yanı sıra kullanımı ve kilitlenme raporlarını izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="edcb7-106">With HockeyApp, you can manage distribution, live testing, and user feedback, as well as monitor usage and crash reports.</span></span> <span data-ttu-id="edcb7-107">Ayrıca, [telemetrinizi dışarı aktarıp Analytics ile sorgulayabilirsiniz](app-insights-hockeyapp-bridge-app.md).</span><span class="sxs-lookup"><span data-stu-id="edcb7-107">You can also [export and query your telemetry with Analytics](app-insights-hockeyapp-bridge-app.md).</span></span>
> 
> <span data-ttu-id="edcb7-108">Bir masaüstü uygulamasından telemetri tooApplication Öngörüler gönderilip bu chiefly olsa da hata ayıklama ve Deneysel amaçları için yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="edcb7-108">Although telemetry can be sent tooApplication Insights from a desktop application, this is chiefly useful for debugging and experimental purposes.</span></span>
> 
> 

## <a name="toosend-telemetry-tooapplication-insights-from-a-windows-application"></a><span data-ttu-id="edcb7-109">bir Windows uygulamasında toosend telemetri tooApplication Öngörüler</span><span class="sxs-lookup"><span data-stu-id="edcb7-109">toosend telemetry tooApplication Insights from a Windows application</span></span>
1. <span data-ttu-id="edcb7-110">Merhaba, [Azure portal](https://portal.azure.com), [bir Application Insights kaynağı oluşturma](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="edcb7-110">In hello [Azure portal](https://portal.azure.com), [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="edcb7-111">Uygulama türü olarak ASP.NET uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="edcb7-111">For application type, choose ASP.NET app.</span></span>
2. <span data-ttu-id="edcb7-112">Merhaba izleme anahtarını bir kopyasını alın.</span><span class="sxs-lookup"><span data-stu-id="edcb7-112">Take a copy of hello Instrumentation Key.</span></span> <span data-ttu-id="edcb7-113">Başlangıç anahtarı Essentials hello yeni kaynak oluşturduğunuz aşağı açılan hello bulun.</span><span class="sxs-lookup"><span data-stu-id="edcb7-113">Find hello key in hello Essentials drop-down of hello new resource you just created.</span></span> 
3. <span data-ttu-id="edcb7-114">Visual Studio'da Uygulama projenizin hello NuGet paketlerini düzenleyin ve Microsoft.ApplicationInsights.WindowsServer ekleyin.</span><span class="sxs-lookup"><span data-stu-id="edcb7-114">In Visual Studio, edit hello NuGet packages of your app project, and add Microsoft.ApplicationInsights.WindowsServer.</span></span> <span data-ttu-id="edcb7-115">(Veya Microsoft.ApplicationInsights hello standart telemetri koleksiyonu modülleri olmadan tam API hello yalnızca istiyorsanız seçin.)</span><span class="sxs-lookup"><span data-stu-id="edcb7-115">(Or choose Microsoft.ApplicationInsights if you just want hello bare API, without hello standard telemetry collection modules.)</span></span>
4. <span data-ttu-id="edcb7-116">Merhaba izleme anahtarı ya da kodunuzu ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="edcb7-116">Set hello instrumentation key either in your code:</span></span>
   
    <span data-ttu-id="edcb7-117">`TelemetryConfiguration.Active.InstrumentationKey = "` *anahtarınız* `";`</span><span class="sxs-lookup"><span data-stu-id="edcb7-117">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
   
    <span data-ttu-id="edcb7-118">veya (Merhaba standart telemetri paketlerden birini yüklediyseniz) Applicationınsights.config:</span><span class="sxs-lookup"><span data-stu-id="edcb7-118">or in ApplicationInsights.config (if you installed one of hello standard telemetry packages):</span></span>
   
    <span data-ttu-id="edcb7-119">`<InstrumentationKey>`*anahtarınız*`</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="edcb7-119">`<InstrumentationKey>`*your key*`</InstrumentationKey>`</span></span> 
   
    <span data-ttu-id="edcb7-120">Applicationınsights.config kullanırsanız, Çözüm Gezgini'nde özelliklerini çok ayarlanmadığından emin olun**yapı eylemi içerik, kopya tooOutput dizin = kopyalama =**.</span><span class="sxs-lookup"><span data-stu-id="edcb7-120">If you use ApplicationInsights.config, make sure its properties in Solution Explorer are set too**Build Action = Content, Copy tooOutput Directory = Copy**.</span></span>
5. <span data-ttu-id="edcb7-121">[Merhaba API kullanan](app-insights-api-custom-events-metrics.md) toosend telemetri.</span><span class="sxs-lookup"><span data-stu-id="edcb7-121">[Use hello API](app-insights-api-custom-events-metrics.md) toosend telemetry.</span></span>
6. <span data-ttu-id="edcb7-122">Uygulamanızı çalıştırmak ve hello telemetri hello Azure portalında oluşturduğunuz hello kaynak görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="edcb7-122">Run your app, and see hello telemetry in hello resource you created in hello Azure Portal.</span></span>

## <span data-ttu-id="edcb7-123"><a name="telemetry"></a>Örnek kod</span><span class="sxs-lookup"><span data-stu-id="edcb7-123"><a name="telemetry"></a>Example code</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="edcb7-124">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="edcb7-124">Next steps</span></span>
* [<span data-ttu-id="edcb7-125">Pano oluşturma</span><span class="sxs-lookup"><span data-stu-id="edcb7-125">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="edcb7-126">Tanılama Araması</span><span class="sxs-lookup"><span data-stu-id="edcb7-126">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="edcb7-127">Ölçümleri keşfetme</span><span class="sxs-lookup"><span data-stu-id="edcb7-127">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="edcb7-128">Analytics sorguları yazma</span><span class="sxs-lookup"><span data-stu-id="edcb7-128">Write Analytics queries</span></span>](app-insights-analytics.md)

