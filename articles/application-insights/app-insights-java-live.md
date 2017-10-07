---
title: "aaaApplication zaten Canlı olan uygulamalar için Java Insights web"
description: "Sunucunuzda zaten çalışan bir web uygulaması İzlemeyi Başlat"
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 12f3dbb9-915f-4087-87c9-807286030b0b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/10/2016
ms.author: bwren
ms.openlocfilehash: 2b01cd61657522ccf1d2d97b2a29cdeb08ec9a18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-java-web-apps-that-are-already-live"></a><span data-ttu-id="e6aab-103">Zaten Java web uygulamaları için Application Insights Canlı</span><span class="sxs-lookup"><span data-stu-id="e6aab-103">Application Insights for Java web apps that are already live</span></span>


<span data-ttu-id="e6aab-104">J2EE sunucunuzda zaten çalışan bir web uygulamanız varsa, kendisiyle izlemeye başlamadan [Application Insights](app-insights-overview.md) hello ihtiyaç toomake kod değişiklikleri veya projenizi yeniden derleyin.</span><span class="sxs-lookup"><span data-stu-id="e6aab-104">If you have a web application that is already running on your J2EE server, you can start monitoring it with [Application Insights](app-insights-overview.md) without hello need toomake code changes or recompile your project.</span></span> <span data-ttu-id="e6aab-105">Bu seçenek ile tooyour server, İşlenmeyen özel durumları ve performans sayaçları gönderilen HTTP istekleri hakkında bilgi alın.</span><span class="sxs-lookup"><span data-stu-id="e6aab-105">With this option, you get information about HTTP requests sent tooyour server, unhandled exceptions, and performance counters.</span></span>

<span data-ttu-id="e6aab-106">Bir abonelik çok gerekir[Microsoft Azure](https://azure.com).</span><span class="sxs-lookup"><span data-stu-id="e6aab-106">You'll need a subscription too[Microsoft Azure](https://azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="e6aab-107">Bu sayfada Hello yordam, çalışma zamanında hello SDK tooyour web uygulaması ekler.</span><span class="sxs-lookup"><span data-stu-id="e6aab-107">hello procedure on this page adds hello SDK tooyour web app at runtime.</span></span> <span data-ttu-id="e6aab-108">Bu çalışma zamanı araçları tooupdate istediğiniz yok veya kaynak kodu yeniden yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="e6aab-108">This runtime instrumentation is useful if you don't want tooupdate or rebuild your source code.</span></span> <span data-ttu-id="e6aab-109">Ancak yapabiliyorsanız, öneririz [hello SDK toohello kaynak kodunu ekleyin](app-insights-java-get-started.md) yerine.</span><span class="sxs-lookup"><span data-stu-id="e6aab-109">But if you can, we recommend you [add hello SDK toohello source code](app-insights-java-get-started.md) instead.</span></span> <span data-ttu-id="e6aab-110">Bu kod tootrack kullanıcı etkinliği yazma gibi daha fazla seçenek verir.</span><span class="sxs-lookup"><span data-stu-id="e6aab-110">That gives you more options such as writing code tootrack user activity.</span></span>
> 
> 

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="e6aab-111">1. Application Insights izleme anahtarı edinme</span><span class="sxs-lookup"><span data-stu-id="e6aab-111">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="e6aab-112">İçinde toohello oturum [Microsoft Azure portalı](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="e6aab-112">Sign in toohello [Microsoft Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="e6aab-113">Yeni bir Application Insights kaynağı oluşturun ve hello uygulama türü tooJava web uygulaması ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e6aab-113">Create a new Application Insights resource and set hello application type tooJava web application.</span></span>
   
    ![Ad girme, Java web uygulaması seçme ve Oluştur’a tıklama](./media/app-insights-java-live/02-create.png)

    <span data-ttu-id="e6aab-115">Merhaba kaynak birkaç saniye içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="e6aab-115">hello resource is created in a few seconds.</span></span>

4. <span data-ttu-id="e6aab-116">Merhaba yeni kaynak açın ve izleme anahtarı edinme.</span><span class="sxs-lookup"><span data-stu-id="e6aab-116">Open hello new resource and get its instrumentation key.</span></span> <span data-ttu-id="e6aab-117">Toopaste bu anahtar kod projenize kısa bir süre sonra ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="e6aab-117">You'll need toopaste this key into your code project shortly.</span></span>
   
    ![Merhaba yeni kaynağa genel bakışta, Özellikler'i tıklatın ve hello izleme anahtarını kopyalama](./media/app-insights-java-live/03-key.png)

## <a name="2-download-hello-sdk"></a><span data-ttu-id="e6aab-119">2. Merhaba SDK yükle</span><span class="sxs-lookup"><span data-stu-id="e6aab-119">2. Download hello SDK</span></span>
1. <span data-ttu-id="e6aab-120">Merhaba karşıdan [Java için Application Insights SDK](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="e6aab-120">Download hello [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span> 
2. <span data-ttu-id="e6aab-121">Sunucunuzda, proje ikili dosyaları yüklü olan hello SDK içeriği toohello dizine ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="e6aab-121">On your server, extract hello SDK contents toohello directory from which your project binaries are loaded.</span></span> <span data-ttu-id="e6aab-122">Tomcat kullanıyorsanız, bu dizin altında genelde olacaktır`webapps/<your_app_name>/WEB-INF/lib`</span><span class="sxs-lookup"><span data-stu-id="e6aab-122">If you’re using Tomcat, this directory would typically be under `webapps/<your_app_name>/WEB-INF/lib`</span></span>

<span data-ttu-id="e6aab-123">Toorepeat bu her sunucu örneğindeki ve her uygulama için gereksinim duyduğunuz olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="e6aab-123">Note that you need toorepeat this on each server instance, and for each app.</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="e6aab-124">3. Application Insights xml dosyası Ekle</span><span class="sxs-lookup"><span data-stu-id="e6aab-124">3. Add an Application Insights xml file</span></span>
<span data-ttu-id="e6aab-125">Applicationınsights.XML hello SDK eklenen hello klasöründe oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e6aab-125">Create ApplicationInsights.xml in hello folder in which you added hello SDK.</span></span> <span data-ttu-id="e6aab-126">İçine yerleştirin hello XML.</span><span class="sxs-lookup"><span data-stu-id="e6aab-126">Put into it hello following XML.</span></span>

<span data-ttu-id="e6aab-127">Hello Azure portal ' aldığınız hello izleme anahtarını Bununla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="e6aab-127">Substitute hello instrumentation key that you got from hello Azure portal.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- hello key from hello portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data tooeach event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```

* <span data-ttu-id="e6aab-128">Merhaba izleme anahtarı telemetrinin her öğesiyle birlikte gönderilir ve Application Insights toodisplay söyler kaynağınız içinde.</span><span class="sxs-lookup"><span data-stu-id="e6aab-128">hello instrumentation key is sent along with every item of telemetry and tells Application Insights toodisplay it in your resource.</span></span>
* <span data-ttu-id="e6aab-129">Merhaba HTTP isteği bileşeni isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="e6aab-129">hello HTTP Request component is optional.</span></span> <span data-ttu-id="e6aab-130">İstek ve yanıt sürelerini toohello portal hakkında telemetriyi otomatik olarak gönderir.</span><span class="sxs-lookup"><span data-stu-id="e6aab-130">It automatically sends telemetry about requests and response times toohello portal.</span></span>
* <span data-ttu-id="e6aab-131">Olay bağıntısı bir toplama toohello HTTP isteği bileşendir.</span><span class="sxs-lookup"><span data-stu-id="e6aab-131">Events correlation is an addition toohello HTTP request component.</span></span> <span data-ttu-id="e6aab-132">Merhaba sunucu tarafından alınan bir tanımlayıcı tooeach isteği atar ve bu tanımlayıcı telemetri bir özellik tooevery öğesi olarak 'Operation.Id' hello özelliği olarak ekler.</span><span class="sxs-lookup"><span data-stu-id="e6aab-132">It assigns an identifier tooeach request received by hello server, and adds this identifier as a property tooevery item of telemetry as hello property 'Operation.Id'.</span></span> <span data-ttu-id="e6aab-133">Bir filtre ayarlayarak her istekle ilişkili toocorrelate hello telemetri tanır [tanılama arama](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="e6aab-133">It allows you toocorrelate hello telemetry associated with each request by setting a filter in [diagnostic search](app-insights-diagnostic-search.md).</span></span>

## <a name="4-add-an-http-filter"></a><span data-ttu-id="e6aab-134">4. HTTP filtresi ekleme</span><span class="sxs-lookup"><span data-stu-id="e6aab-134">4. Add an HTTP filter</span></span>
<span data-ttu-id="e6aab-135">Bulup, proje ve uygulama filtrelerinizin yapılandırıldığı hello web uygulaması düğümü altında kod parçacığını aşağıdaki birleştirme hello hello web.xml dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="e6aab-135">Locate and open hello web.xml file in your project, and merge hello following snippet of code under hello web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="e6aab-136">tooget hello en doğru sonuçlar, hello filtre önce tüm diğer filtrelerle eşlenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="e6aab-136">tooget hello most accurate results, hello filter should be mapped before all other filters.</span></span>

```XML

    <filter>
      <filter-name>ApplicationInsightsWebFilter</filter-name>
      <filter-class>
        com.microsoft.applicationinsights.web.internal.WebRequestTrackingFilter
      </filter-class>
    </filter>
    <filter-mapping>
       <filter-name>ApplicationInsightsWebFilter</filter-name>
       <url-pattern>/*</url-pattern>
    </filter-mapping>
```

## <a name="5-check-firewall-exceptions"></a><span data-ttu-id="e6aab-137">5. Güvenlik Duvarı özel durumlarını denetleyin</span><span class="sxs-lookup"><span data-stu-id="e6aab-137">5. Check firewall exceptions</span></span>
<span data-ttu-id="e6aab-138">Çok gerekebilecek[özel durumları toosend giden veri kümesi](app-insights-ip-addresses.md).</span><span class="sxs-lookup"><span data-stu-id="e6aab-138">You might need too[set exceptions toosend outgoing data](app-insights-ip-addresses.md).</span></span>

## <a name="6-restart-your-web-app"></a><span data-ttu-id="e6aab-139">6. Web uygulamanızı yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="e6aab-139">6. Restart your web app</span></span>
## <a name="7-view-your-telemetry-in-application-insights"></a><span data-ttu-id="e6aab-140">7. Application Insights'da telemetrinizi görüntüleme</span><span class="sxs-lookup"><span data-stu-id="e6aab-140">7. View your telemetry in Application Insights</span></span>
<span data-ttu-id="e6aab-141">Tooyour Application Insights kaynağını dönmek [Microsoft Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e6aab-141">Return tooyour Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="e6aab-142">HTTP istekleriyle ilgili telemetri hello genel bakış dikey penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="e6aab-142">Telemetry about HTTP requests appears on hello overview blade.</span></span> <span data-ttu-id="e6aab-143">(Orada değilse, birkaç saniye bekleyip Yenile’ye tıklayın.)</span><span class="sxs-lookup"><span data-stu-id="e6aab-143">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![örnek veri](./media/app-insights-java-live/5-results.png)

<span data-ttu-id="e6aab-145">Tıklatın herhangi grafik toosee ayrıntılı ölçümler.</span><span class="sxs-lookup"><span data-stu-id="e6aab-145">Click through any chart toosee more detailed metrics.</span></span> 

![](./media/app-insights-java-live/6-barchart.png)

<span data-ttu-id="e6aab-146">Ve istek hello özellikleri görüntülendiğinde, istekler ve özel durumlar gibi ilişkili hello telemetri olayları görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6aab-146">And when viewing hello properties of a request, you can see hello telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-live/7-instance.png)

[<span data-ttu-id="e6aab-147">Ölçümler hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="e6aab-147">Learn more about metrics.</span></span>](app-insights-metrics-explorer.md)

## <a name="next-steps"></a><span data-ttu-id="e6aab-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e6aab-148">Next steps</span></span>
* <span data-ttu-id="e6aab-149">[Telemetri tooyour web sayfaları eklemek](app-insights-javascript.md) toomonitor sayfa görünümlerini ve kullanıcı ölçümlerini.</span><span class="sxs-lookup"><span data-stu-id="e6aab-149">[Add telemetry tooyour web pages](app-insights-javascript.md) toomonitor page views and user metrics.</span></span>
* <span data-ttu-id="e6aab-150">[Web testleri oluşturma](app-insights-monitor-web-app-availability.md) toomake uygulamanızın canlı ve duyarlı kaldığından emin.</span><span class="sxs-lookup"><span data-stu-id="e6aab-150">[Set up web tests](app-insights-monitor-web-app-availability.md) toomake sure your application stays live and responsive.</span></span>
* [<span data-ttu-id="e6aab-151">Günlük izlemelerini yakalama</span><span class="sxs-lookup"><span data-stu-id="e6aab-151">Capture log traces</span></span>](app-insights-java-trace-logs.md)
* <span data-ttu-id="e6aab-152">[Olayları ve günlükleri arayın](app-insights-diagnostic-search.md) toohelp sorunları tanılayın.</span><span class="sxs-lookup"><span data-stu-id="e6aab-152">[Search events and logs](app-insights-diagnostic-search.md) toohelp diagnose problems.</span></span>

