---
title: "Zaten Java web uygulamaları için Application Insights Canlı"
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
ms.openlocfilehash: a2731e3e44f8f3d104d8abc7dbe71fe3a4c3a690
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="application-insights-for-java-web-apps-that-are-already-live"></a><span data-ttu-id="6b0cc-103">Zaten Java web uygulamaları için Application Insights Canlı</span><span class="sxs-lookup"><span data-stu-id="6b0cc-103">Application Insights for Java web apps that are already live</span></span>


<span data-ttu-id="6b0cc-104">J2EE sunucunuzda zaten çalışan bir web uygulamanız varsa, kendisiyle izlemeye başlamadan [Application Insights](app-insights-overview.md) gerekmeden kod değişiklikleri yapabilir veya projenizi yeniden derleyin.</span><span class="sxs-lookup"><span data-stu-id="6b0cc-104">If you have a web application that is already running on your J2EE server, you can start monitoring it with [Application Insights](app-insights-overview.md) without the need to make code changes or recompile your project.</span></span> <span data-ttu-id="6b0cc-105">Bu seçenek ile sunucu, İşlenmeyen özel durumları ve performans sayaçları için gönderilen HTTP istekleri hakkında bilgi alın.</span><span class="sxs-lookup"><span data-stu-id="6b0cc-105">With this option, you get information about HTTP requests sent to your server, unhandled exceptions, and performance counters.</span></span>

<span data-ttu-id="6b0cc-106">Size bir [Microsoft Azure](https://azure.com) aboneliği gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="6b0cc-106">You'll need a subscription to [Microsoft Azure](https://azure.com).</span></span>

> [!NOTE]
> <span data-ttu-id="6b0cc-107">Bu sayfada yordam, web uygulamanıza çalışma zamanında SDK ekler.</span><span class="sxs-lookup"><span data-stu-id="6b0cc-107">The procedure on this page adds the SDK to your web app at runtime.</span></span> <span data-ttu-id="6b0cc-108">Bu çalışma zamanı izleme, güncelleştirme veya kaynak kodu yeniden istemiyorsanız, yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="6b0cc-108">This runtime instrumentation is useful if you don't want to update or rebuild your source code.</span></span> <span data-ttu-id="6b0cc-109">Ancak yapabiliyorsanız, öneririz [kaynak koduna SDK'sı ekleme](app-insights-java-get-started.md) yerine.</span><span class="sxs-lookup"><span data-stu-id="6b0cc-109">But if you can, we recommend you [add the SDK to the source code](app-insights-java-get-started.md) instead.</span></span> <span data-ttu-id="6b0cc-110">Bu, kullanıcı etkinliğini izlemek için daha fazla seçenek kod yazma gibi sağlar.</span><span class="sxs-lookup"><span data-stu-id="6b0cc-110">That gives you more options such as writing code to track user activity.</span></span>
> 
> 

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="6b0cc-111">1. Application Insights izleme anahtarı edinme</span><span class="sxs-lookup"><span data-stu-id="6b0cc-111">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="6b0cc-112">Oturum [Microsoft Azure portalı](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="6b0cc-112">Sign in to the [Microsoft Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="6b0cc-113">Yeni bir Application Insights kaynağı oluşturma ve uygulama türünü Java web uygulaması olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="6b0cc-113">Create a new Application Insights resource and set the application type to Java web application.</span></span>
   
    ![Ad girme, Java web uygulaması seçme ve Oluştur’a tıklama](./media/app-insights-java-live/02-create.png)

    <span data-ttu-id="6b0cc-115">Kaynak birkaç saniye içinde oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="6b0cc-115">The resource is created in a few seconds.</span></span>

4. <span data-ttu-id="6b0cc-116">Yeni kaynak açın ve izleme anahtarı edinme.</span><span class="sxs-lookup"><span data-stu-id="6b0cc-116">Open the new resource and get its instrumentation key.</span></span> <span data-ttu-id="6b0cc-117">Bu anahtarı hemen kod projenize yapıştırmalısınız.</span><span class="sxs-lookup"><span data-stu-id="6b0cc-117">You'll need to paste this key into your code project shortly.</span></span>
   
    ![Yeni kaynağa genel bakışta, Özellikler'e tıklayıp izleme anahtarını kopyalama](./media/app-insights-java-live/03-key.png)

## <a name="2-download-the-sdk"></a><span data-ttu-id="6b0cc-119">2. SDK'sını indirin</span><span class="sxs-lookup"><span data-stu-id="6b0cc-119">2. Download the SDK</span></span>
1. <span data-ttu-id="6b0cc-120">[Java için Application Insights SDK’sı](https://aka.ms/aijavasdk) indirin.</span><span class="sxs-lookup"><span data-stu-id="6b0cc-120">Download the [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span> 
2. <span data-ttu-id="6b0cc-121">Sunucunuz üzerinde SDK içeriği proje ikili dosyaları yüklü olan dizine ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="6b0cc-121">On your server, extract the SDK contents to the directory from which your project binaries are loaded.</span></span> <span data-ttu-id="6b0cc-122">Tomcat kullanıyorsanız, bu dizin altında genelde olacaktır`webapps/<your_app_name>/WEB-INF/lib`</span><span class="sxs-lookup"><span data-stu-id="6b0cc-122">If you’re using Tomcat, this directory would typically be under `webapps/<your_app_name>/WEB-INF/lib`</span></span>

<span data-ttu-id="6b0cc-123">Bu her sunucu örneğindeki ve her uygulama için yineleyin gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="6b0cc-123">Note that you need to repeat this on each server instance, and for each app.</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="6b0cc-124">3. Application Insights xml dosyası Ekle</span><span class="sxs-lookup"><span data-stu-id="6b0cc-124">3. Add an Application Insights xml file</span></span>
<span data-ttu-id="6b0cc-125">Applicationınsights.XML SDK eklenen klasöründe oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6b0cc-125">Create ApplicationInsights.xml in the folder in which you added the SDK.</span></span> <span data-ttu-id="6b0cc-126">Aşağıdaki XML içine yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="6b0cc-126">Put into it the following XML.</span></span>

<span data-ttu-id="6b0cc-127">Azure portalından aldığınız izleme anahtarını bununla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6b0cc-127">Substitute the instrumentation key that you got from the Azure portal.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- The key from the portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data to each event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```

* <span data-ttu-id="6b0cc-128">İzleme anahtarı telemetrinin her öğesiyle birlikte gönderilir ve Application Insights’ın bunu kaynağınızda görüntülemesini isteyin.</span><span class="sxs-lookup"><span data-stu-id="6b0cc-128">The instrumentation key is sent along with every item of telemetry and tells Application Insights to display it in your resource.</span></span>
* <span data-ttu-id="6b0cc-129">HTTP isteği bileşeni isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="6b0cc-129">The HTTP Request component is optional.</span></span> <span data-ttu-id="6b0cc-130">İstek ve yanıt süreleri hakkında telemetriyi otomatik olarak portala gönderir.</span><span class="sxs-lookup"><span data-stu-id="6b0cc-130">It automatically sends telemetry about requests and response times to the portal.</span></span>
* <span data-ttu-id="6b0cc-131">Olay bağıntısı HTTP isteği bileşenine bir ektir.</span><span class="sxs-lookup"><span data-stu-id="6b0cc-131">Events correlation is an addition to the HTTP request component.</span></span> <span data-ttu-id="6b0cc-132">Sunucu tarafından alınan her istek için bir tanımlayıcı atar ve bu tanımlayıcıyı bir özellik olarak, telemetrinin her öğesine 'Operation.Id' özelliği olarak ekler.</span><span class="sxs-lookup"><span data-stu-id="6b0cc-132">It assigns an identifier to each request received by the server, and adds this identifier as a property to every item of telemetry as the property 'Operation.Id'.</span></span> <span data-ttu-id="6b0cc-133">Bir filtre ayarlayarak her istekle ilişkili telemetrinin bağıntısını kurmanızı sağlar [tanılama arama](app-insights-diagnostic-search.md).</span><span class="sxs-lookup"><span data-stu-id="6b0cc-133">It allows you to correlate the telemetry associated with each request by setting a filter in [diagnostic search](app-insights-diagnostic-search.md).</span></span>

## <a name="4-add-an-http-filter"></a><span data-ttu-id="6b0cc-134">4. HTTP filtresi ekleme</span><span class="sxs-lookup"><span data-stu-id="6b0cc-134">4. Add an HTTP filter</span></span>
<span data-ttu-id="6b0cc-135">Bulun ve projenizde web.xml dosyasını açın ve aşağıdaki uygulama filtrelerinizin yapılandırıldığı web uygulaması düğümü altında kod parçacığını birleştirin.</span><span class="sxs-lookup"><span data-stu-id="6b0cc-135">Locate and open the web.xml file in your project, and merge the following snippet of code under the web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="6b0cc-136">En doğru sonuçlar almak için önce filtrenin tüm diğer filtrelerle eşlenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="6b0cc-136">To get the most accurate results, the filter should be mapped before all other filters.</span></span>

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

## <a name="5-check-firewall-exceptions"></a><span data-ttu-id="6b0cc-137">5. Güvenlik Duvarı özel durumlarını denetleyin</span><span class="sxs-lookup"><span data-stu-id="6b0cc-137">5. Check firewall exceptions</span></span>
<span data-ttu-id="6b0cc-138">İçin gerekebilecek [ayarlamak giden veri göndermek için özel durumlar](app-insights-ip-addresses.md).</span><span class="sxs-lookup"><span data-stu-id="6b0cc-138">You might need to [set exceptions to send outgoing data](app-insights-ip-addresses.md).</span></span>

## <a name="6-restart-your-web-app"></a><span data-ttu-id="6b0cc-139">6. Web uygulamanızı yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="6b0cc-139">6. Restart your web app</span></span>
## <a name="7-view-your-telemetry-in-application-insights"></a><span data-ttu-id="6b0cc-140">7. Application Insights'da telemetrinizi görüntüleme</span><span class="sxs-lookup"><span data-stu-id="6b0cc-140">7. View your telemetry in Application Insights</span></span>
<span data-ttu-id="6b0cc-141">[Microsoft Azure portalında](https://portal.azure.com), Application Insights kaynağınıza dönün.</span><span class="sxs-lookup"><span data-stu-id="6b0cc-141">Return to your Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="6b0cc-142">HTTP istekleriyle ilgili telemetri genel bakış dikey penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="6b0cc-142">Telemetry about HTTP requests appears on the overview blade.</span></span> <span data-ttu-id="6b0cc-143">(Orada değilse, birkaç saniye bekleyip Yenile’ye tıklayın.)</span><span class="sxs-lookup"><span data-stu-id="6b0cc-143">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![örnek veri](./media/app-insights-java-live/5-results.png)

<span data-ttu-id="6b0cc-145">Daha ayrıntılı ölçümler görmek için herhangi bir grafiğe tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6b0cc-145">Click through any chart to see more detailed metrics.</span></span> 

![](./media/app-insights-java-live/6-barchart.png)

<span data-ttu-id="6b0cc-146">Ve istek özellikleri görüntülendiğinde, istekler ve özel durumlar gibi ilişkili telemetri olayları görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6b0cc-146">And when viewing the properties of a request, you can see the telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-live/7-instance.png)

[<span data-ttu-id="6b0cc-147">Ölçümler hakkında daha fazla bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="6b0cc-147">Learn more about metrics.</span></span>](app-insights-metrics-explorer.md)

## <a name="next-steps"></a><span data-ttu-id="6b0cc-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6b0cc-148">Next steps</span></span>
* <span data-ttu-id="6b0cc-149">[Web sayfalarınıza telemetri ekleyin](app-insights-javascript.md) İzleyici sayfa görünümleri ve kullanıcı ölçümlerini.</span><span class="sxs-lookup"><span data-stu-id="6b0cc-149">[Add telemetry to your web pages](app-insights-javascript.md) to monitor page views and user metrics.</span></span>
* <span data-ttu-id="6b0cc-150">[Web testleri oluşturma](app-insights-monitor-web-app-availability.md) canlı ve duyarlı uygulamanızı kaldığından emin olmak için.</span><span class="sxs-lookup"><span data-stu-id="6b0cc-150">[Set up web tests](app-insights-monitor-web-app-availability.md) to make sure your application stays live and responsive.</span></span>
* [<span data-ttu-id="6b0cc-151">Günlük izlemelerini yakalama</span><span class="sxs-lookup"><span data-stu-id="6b0cc-151">Capture log traces</span></span>](app-insights-java-trace-logs.md)
* <span data-ttu-id="6b0cc-152">[Olayları ve günlükleri arayın](app-insights-diagnostic-search.md) sorunların tanılanmasına yardımcı olmak için.</span><span class="sxs-lookup"><span data-stu-id="6b0cc-152">[Search events and logs](app-insights-diagnostic-search.md) to help diagnose problems.</span></span>

