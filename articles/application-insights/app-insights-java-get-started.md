---
title: "Azure Application Insights ile Java web uygulaması analizi | Microsoft Docs"
description: "Application Insights ile Java web uygulamaları için Uygulama Performansı İzleme. "
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 051d4285-f38a-45d8-ad8a-45c3be828d91
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: a75815885d7ccd7cd56db3da2f3f92cae78fe033
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-application-insights-in-a-java-web-project"></a><span data-ttu-id="8773a-103">Java web projesinde Application Insights ile başlarken</span><span class="sxs-lookup"><span data-stu-id="8773a-103">Get started with Application Insights in a Java web project</span></span>


<span data-ttu-id="8773a-104">[Application Insights](https://azure.microsoft.com/services/application-insights/), web geliştiricileri için canlı uygulamanızın performansını ve kullanımını anlamanıza yardımcı olan genişletilebilir bir analiz hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="8773a-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) is an extensible analytics service for web developers that helps you understand the performance and usage of your live application.</span></span> <span data-ttu-id="8773a-105">[Performans sorunlarını ve özel durumlarını algılamak ve tanılamak](app-insights-detect-triage-diagnose.md) için bunu kullanın; uygulamanızla kullanıcıların ne yaptığını izlemek için de [kod yazın][api].</span><span class="sxs-lookup"><span data-stu-id="8773a-105">Use it to [detect and diagnose performance issues and exceptions](app-insights-detect-triage-diagnose.md), and [write code][api] to track what users do with your app.</span></span>

![örnek veri](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="8773a-107">Application Insights; Linux, Unix veya Windows üzerinde çalışan Java uygulamalarını destekler.</span><span class="sxs-lookup"><span data-stu-id="8773a-107">Application Insights supports Java apps running on Linux, Unix, or Windows.</span></span>

<span data-ttu-id="8773a-108">Gerekenler:</span><span class="sxs-lookup"><span data-stu-id="8773a-108">You need:</span></span>

* <span data-ttu-id="8773a-109">Oracle JRE 1.6 veya sonraki sürümleri ya da Zulu JRE 1.6 veya sonraki sürümleri</span><span class="sxs-lookup"><span data-stu-id="8773a-109">Oracle JRE 1.6 or later, or Zulu JRE 1.6 or later</span></span>
* <span data-ttu-id="8773a-110">Bir [Microsoft Azure](https://azure.microsoft.com/) aboneliği.</span><span class="sxs-lookup"><span data-stu-id="8773a-110">A subscription to [Microsoft Azure](https://azure.microsoft.com/).</span></span>

<span data-ttu-id="8773a-111">*Zaten canlı olan bir web uygulaması varsa, [web sunucusuna çalışma zamanında SDK eklemek](app-insights-java-live.md) için alternatif bir yordam izleyebilirsiniz. Bu alternatif yordam, kodun yeniden derlenmesini engellese de, kullanıcı etkinliğini izlemek için kod yazma seçeneğini elde etmezsiniz.*</span><span class="sxs-lookup"><span data-stu-id="8773a-111">*If you have a web app that's already live, you could follow the alternative procedure to [add the SDK at runtime in the web server](app-insights-java-live.md). That alternative avoids rebuilding the code, but you don't get the option to write code to track user activity.*</span></span>

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="8773a-112">1. Application Insights izleme anahtarı edinme</span><span class="sxs-lookup"><span data-stu-id="8773a-112">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="8773a-113">[Microsoft Azure portalında](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="8773a-113">Sign in to the [Microsoft Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="8773a-114">Bir Application Insights kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8773a-114">Create an Application Insights resource.</span></span> <span data-ttu-id="8773a-115">Uygulama türünü Java web uygulaması olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="8773a-115">Set the application type to Java web application.</span></span>

    ![Ad girme, Java web uygulaması seçme ve Oluştur’a tıklama](./media/app-insights-java-get-started/02-create.png)
3. <span data-ttu-id="8773a-117">Yeni kaynağın izleme anahtarını bulun.</span><span class="sxs-lookup"><span data-stu-id="8773a-117">Find the instrumentation key of the new resource.</span></span> <span data-ttu-id="8773a-118">Bu anahtarı hemen kod projenize yapıştırmalısınız.</span><span class="sxs-lookup"><span data-stu-id="8773a-118">You'll need to paste this key into your code project shortly.</span></span>

    ![Yeni kaynağa genel bakışta, Özellikler'e tıklayıp izleme anahtarını kopyalama](./media/app-insights-java-get-started/03-key.png)

## <a name="2-add-the-application-insights-sdk-for-java-to-your-project"></a><span data-ttu-id="8773a-120">2. Projenize Java için Application Insights SDK’sı ekleme</span><span class="sxs-lookup"><span data-stu-id="8773a-120">2. Add the Application Insights SDK for Java to your project</span></span>
<span data-ttu-id="8773a-121">*Projeniz için uygun yolu seçin.*</span><span class="sxs-lookup"><span data-stu-id="8773a-121">*Choose the appropriate way for your project.*</span></span>

#### <a name="if-youre-using-eclipse-to-create-a-maven-or-dynamic-web-project-"></a><span data-ttu-id="8773a-122">Maven veya Dinamik Web projesi oluşturmak için Eclipse kullanıyorsanız...</span><span class="sxs-lookup"><span data-stu-id="8773a-122">If you're using Eclipse to create a Maven or Dynamic Web project ...</span></span>
<span data-ttu-id="8773a-123">[Java eklentisi için Application Insights SDK'sı][eclipse] kullanın.</span><span class="sxs-lookup"><span data-stu-id="8773a-123">Use the [Application Insights SDK for Java plug-in][eclipse].</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="8773a-124">Maven kullanıyorsanız...</span><span class="sxs-lookup"><span data-stu-id="8773a-124">If you're using Maven...</span></span>
<span data-ttu-id="8773a-125">Projenizi derleme için zaten Maven kullanmak üzere ayarlanmışsa aşağıdaki kodu pom.xml dosyanızla birleştirin.</span><span class="sxs-lookup"><span data-stu-id="8773a-125">If your project is already set up to use Maven for build, merge the following code to your pom.xml file.</span></span>

<span data-ttu-id="8773a-126">Daha sonra, proje bağımlılıklarını ikili dosyaları indirmek için yenileyin.</span><span class="sxs-lookup"><span data-stu-id="8773a-126">Then, refresh the project dependencies to get the binaries downloaded.</span></span>

```XML

    <repositories>
       <repository>
          <id>central</id>
          <name>Central</name>
          <url>http://repo1.maven.org/maven2</url>
       </repository>
    </repositories>

    <dependencies>
      <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>applicationinsights-web</artifactId>
        <!-- or applicationinsights-core for bare API -->
        <version>[1.0,)</version>
      </dependency>
    </dependencies>
```

* <span data-ttu-id="8773a-127">*Derleme veya sağlama toplamı doğrulama hataları mı var?*</span><span class="sxs-lookup"><span data-stu-id="8773a-127">*Build or checksum validation errors?*</span></span> <span data-ttu-id="8773a-128">`<version>1.0.n</version>` gibi belirli bir sürümü kullanmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="8773a-128">Try using a specific version, such as: `<version>1.0.n</version>`.</span></span> <span data-ttu-id="8773a-129">En son sürümü [SDK sürüm notlarında](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) veya [Maven yapıtları](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights) sitemizde bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="8773a-129">You'll find the latest version in the [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) or in our [Maven artifacts](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span></span>
* <span data-ttu-id="8773a-130">*Yeni SDK’ye mi güncelleştirmeniz gerekiyor?*</span><span class="sxs-lookup"><span data-stu-id="8773a-130">*Need to update to a new SDK?*</span></span> <span data-ttu-id="8773a-131">Proje bağımlılıklarınızı yenileyin.</span><span class="sxs-lookup"><span data-stu-id="8773a-131">Refresh your project's dependencies.</span></span>

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="8773a-132">Gradle kullanıyorsanız...</span><span class="sxs-lookup"><span data-stu-id="8773a-132">If you're using Gradle...</span></span>
<span data-ttu-id="8773a-133">Projenizi derleme için zaten Gradle kullanmak üzere ayarlanmışsa aşağıdaki kodu build.gradle dosyanızla birleştirin.</span><span class="sxs-lookup"><span data-stu-id="8773a-133">If your project is already set up to use Gradle for build, merge the following code to your build.gradle file.</span></span>

<span data-ttu-id="8773a-134">Daha sonra, proje bağımlılıklarını ikili dosyaları indirmek için yenileyin.</span><span class="sxs-lookup"><span data-stu-id="8773a-134">Then refresh the project dependencies to get the binaries downloaded.</span></span>

```JSON

    repositories {
      mavenCentral()
    }

    dependencies {
      compile group: 'com.microsoft.azure', name: 'applicationinsights-web', version: '1.+'
      // or applicationinsights-core for bare API
    }
```

* <span data-ttu-id="8773a-135">*Derleme veya sağlama toplamı doğrulama hataları mı var? `version:'1.0.n'` gibi belirli bir sürümü kullanmayı deneyin*.</span><span class="sxs-lookup"><span data-stu-id="8773a-135">*Build or checksum validation errors? Try using a specific version, such as:* `version:'1.0.n'`.</span></span> <span data-ttu-id="8773a-136">*En son sürümü [SDK sürüm notlarında](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) bulabilirsiniz.*</span><span class="sxs-lookup"><span data-stu-id="8773a-136">*You'll find the latest version in the [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span></span>
* <span data-ttu-id="8773a-137">*Yeni SDK’ya güncelleştirmek için*</span><span class="sxs-lookup"><span data-stu-id="8773a-137">*To update to a new SDK*</span></span>
  * <span data-ttu-id="8773a-138">Proje bağımlılıklarınızı yenileyin.</span><span class="sxs-lookup"><span data-stu-id="8773a-138">Refresh your project's dependencies.</span></span>

#### <a name="otherwise-"></a><span data-ttu-id="8773a-139">Aksi taktirde...</span><span class="sxs-lookup"><span data-stu-id="8773a-139">Otherwise ...</span></span>
<span data-ttu-id="8773a-140">SDK'yi el ile ekleyin:</span><span class="sxs-lookup"><span data-stu-id="8773a-140">Manually add the SDK:</span></span>

1. <span data-ttu-id="8773a-141">[Java için Application Insights SDK’sı](https://aka.ms/aijavasdk) indirin.</span><span class="sxs-lookup"><span data-stu-id="8773a-141">Download the [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="8773a-142">İkili dosyaları zip dosyasından ayıklayıp projenize ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8773a-142">Extract the binaries from the zip file and add them to your project.</span></span>

### <a name="questions"></a><span data-ttu-id="8773a-143">Sorular...</span><span class="sxs-lookup"><span data-stu-id="8773a-143">Questions...</span></span>
* <span data-ttu-id="8773a-144">*Zip’teki `-core` ve `-web` bileşenleri arasındaki ilişki nedir?*</span><span class="sxs-lookup"><span data-stu-id="8773a-144">*What's the relationship between the `-core` and `-web` components in the zip?*</span></span>

  * <span data-ttu-id="8773a-145">`applicationinsights-core` size tam API sağlar.</span><span class="sxs-lookup"><span data-stu-id="8773a-145">`applicationinsights-core` gives you the bare API.</span></span> <span data-ttu-id="8773a-146">Bu bileşen her zaman gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="8773a-146">You always need this component.</span></span>
  * <span data-ttu-id="8773a-147">`applicationinsights-web`, HTTP istek sayısını ve yanıt sürelerini izleyen ölçümleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="8773a-147">`applicationinsights-web` gives you metrics that track HTTP request counts and response times.</span></span> <span data-ttu-id="8773a-148">Bu telemetrinin otomatik olarak toplanmasını istemiyorsanız, bu bileşeni atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8773a-148">You can omit this component if you don't want this telemetry automatically collected.</span></span> <span data-ttu-id="8773a-149">Örneğin, kendiniz yazmak istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="8773a-149">For example, if you want to write your own.</span></span>
* <span data-ttu-id="8773a-150">*Değişiklikleri yayımladığınızda SDK’yı güncelleştirmek için*</span><span class="sxs-lookup"><span data-stu-id="8773a-150">*To update the SDK when we publish changes*</span></span>

  * <span data-ttu-id="8773a-151">En son [Java için Application Insights SDK’si](https://aka.ms/qqkaq6)’ni indirin ve eskilerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="8773a-151">Download the latest [Application Insights SDK for Java](https://aka.ms/qqkaq6) and replace the old ones.</span></span>
  * <span data-ttu-id="8773a-152">Değişiklikler [SDK sürüm notlarında](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="8773a-152">Changes are described in the [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="8773a-153">3. Application Insights .xml dosyasını ekleme</span><span class="sxs-lookup"><span data-stu-id="8773a-153">3. Add an Application Insights .xml file</span></span>
<span data-ttu-id="8773a-154">Projenizin kaynaklar klasörüne ApplicationInsights.xml dosyasını ekleyin veya projenizin dağıtım sınıfı yoluna eklendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="8773a-154">Add ApplicationInsights.xml to the resources folder in your project, or make sure it is added to your project’s deployment class path.</span></span> <span data-ttu-id="8773a-155">Aşağıdaki XML dosyasını buraya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="8773a-155">Copy the following XML into it.</span></span>

<span data-ttu-id="8773a-156">Azure portalından aldığınız izleme anahtarını bununla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="8773a-156">Substitute the instrumentation key that you got from the Azure portal.</span></span>

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


* <span data-ttu-id="8773a-157">İzleme anahtarı telemetrinin her öğesiyle birlikte gönderilir ve Application Insights’ın bunu kaynağınızda görüntülemesini isteyin.</span><span class="sxs-lookup"><span data-stu-id="8773a-157">The instrumentation key is sent along with every item of telemetry and tells Application Insights to display it in your resource.</span></span>
* <span data-ttu-id="8773a-158">HTTP isteği bileşeni isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="8773a-158">The HTTP Request component is optional.</span></span> <span data-ttu-id="8773a-159">İstek ve yanıt süreleri hakkında telemetriyi otomatik olarak portala gönderir.</span><span class="sxs-lookup"><span data-stu-id="8773a-159">It automatically sends telemetry about requests and response times to the portal.</span></span>
* <span data-ttu-id="8773a-160">Olay bağıntısı HTTP isteği bileşenine bir ektir.</span><span class="sxs-lookup"><span data-stu-id="8773a-160">Events correlation is an addition to the HTTP request component.</span></span> <span data-ttu-id="8773a-161">Sunucu tarafından alınan her istek için bir tanımlayıcı atar ve bu tanımlayıcıyı bir özellik olarak, telemetrinin her öğesine 'Operation.Id' özelliği olarak ekler.</span><span class="sxs-lookup"><span data-stu-id="8773a-161">It assigns an identifier to each request received by the server, and adds this identifier as a property to every item of telemetry as the property 'Operation.Id'.</span></span> <span data-ttu-id="8773a-162">[Tanı aramaya][diagnostic] bir filtre ayarlayarak her istekle ilişkili telemetrinin bağıntısını kurmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="8773a-162">It allows you to correlate the telemetry associated with each request by setting a filter in [diagnostic search][diagnostic].</span></span>
* <span data-ttu-id="8773a-163">Application Insights anahtarı, Azure portalından bir sistem özelliği olarak dinamik şekilde geçirilebilir (-DAPPLICATION_INSIGHTS_IKEY=your_ikey).</span><span class="sxs-lookup"><span data-stu-id="8773a-163">The Application Insights key can be passed dynamically from the Azure portal as a system property (-DAPPLICATION_INSIGHTS_IKEY=your_ikey).</span></span> <span data-ttu-id="8773a-164">Tanımlı bir özellik yoksa, Azure Uygulama Ayarlarında ortam değişkeni (APPLICATION_INSIGHTS_IKEY) denetlenir.</span><span class="sxs-lookup"><span data-stu-id="8773a-164">If there is no property defined, it checks for environment variable (APPLICATION_INSIGHTS_IKEY) in Azure App Settings.</span></span> <span data-ttu-id="8773a-165">Her iki özellik de tanımlanmamışsa ApplicationInsights.xml dosyasındaki varsayılan InstrumentationKey kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8773a-165">If both the properties are undefined, the default InstrumentationKey is used from ApplicationInsights.xml.</span></span> <span data-ttu-id="8773a-166">Bu sıra farklı ortamlar için farklı InstrumentationKeys’i dinamik olarak yönetmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="8773a-166">This sequence helps you to manage different InstrumentationKeys for different environments dynamically.</span></span>

### <a name="alternative-ways-to-set-the-instrumentation-key"></a><span data-ttu-id="8773a-167">İzleme anahtarını ayarlamak için alternatif yollar</span><span class="sxs-lookup"><span data-stu-id="8773a-167">Alternative ways to set the instrumentation key</span></span>
<span data-ttu-id="8773a-168">Application Insights SDK’sı anahtarı şu sırayla arar:</span><span class="sxs-lookup"><span data-stu-id="8773a-168">Application Insights SDK looks for the key in this order:</span></span>

1. <span data-ttu-id="8773a-169">Sistem özelliği: -DAPPLICATION_INSIGHTS_IKEY=your_ikey</span><span class="sxs-lookup"><span data-stu-id="8773a-169">System property: -DAPPLICATION_INSIGHTS_IKEY=your_ikey</span></span>
2. <span data-ttu-id="8773a-170">Ortam değişkeni: APPLICATION_INSIGHTS_IKEY</span><span class="sxs-lookup"><span data-stu-id="8773a-170">Environment variable: APPLICATION_INSIGHTS_IKEY</span></span>
3. <span data-ttu-id="8773a-171">Yapılandırma dosyası: ApplicationInsights.xml</span><span class="sxs-lookup"><span data-stu-id="8773a-171">Configuration file: ApplicationInsights.xml</span></span>

<span data-ttu-id="8773a-172">Ayrıca [kod içinde ayarlayabilirsiniz](app-insights-api-custom-events-metrics.md#ikey):</span><span class="sxs-lookup"><span data-stu-id="8773a-172">You can also [set it in code](app-insights-api-custom-events-metrics.md#ikey):</span></span>

```Java

    telemetryClient.InstrumentationKey = "...";
```

## <a name="4-add-an-http-filter"></a><span data-ttu-id="8773a-173">4. HTTP filtresi ekleme</span><span class="sxs-lookup"><span data-stu-id="8773a-173">4. Add an HTTP filter</span></span>
<span data-ttu-id="8773a-174">Son yapılandırma adımı HTTP isteği bileşeninin her web isteğini kaydetmesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="8773a-174">The last configuration step allows the HTTP request component to log each web request.</span></span> <span data-ttu-id="8773a-175">(Yalnızca tam API istiyorsanız gerekmez.)</span><span class="sxs-lookup"><span data-stu-id="8773a-175">(Not required if you just want the bare API.)</span></span>

<span data-ttu-id="8773a-176">Projenizde web.xml dosyasını bulup açın ve uygulama filtrelerinizin yapılandırıldığı web uygulaması düğümü altında aşağıdaki kodu birleştirin.</span><span class="sxs-lookup"><span data-stu-id="8773a-176">Locate and open the web.xml file in your project, and merge the following code under the web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="8773a-177">En doğru sonuçlar almak için önce filtrenin tüm diğer filtrelerle eşlenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="8773a-177">To get the most accurate results, the filter should be mapped before all other filters.</span></span>

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

#### <a name="if-youre-using-spring-web-mvc-31-or-later"></a><span data-ttu-id="8773a-178">Spring Web MVC 3.1 veya sonraki sürümleri kullanıyorsanız</span><span class="sxs-lookup"><span data-stu-id="8773a-178">If you're using Spring Web MVC 3.1 or later</span></span>
<span data-ttu-id="8773a-179">Bu öğeleri *-servlet.xml içinde Application Insights paketini içerecek şekilde düzenleyin:</span><span class="sxs-lookup"><span data-stu-id="8773a-179">Edit these elements in *-servlet.xml to include the Application Insights package:</span></span>

```XML

    <context:component-scan base-package=" com.springapp.mvc, com.microsoft.applicationinsights.web.spring"/>

    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/**"/>
            <bean class="com.microsoft.applicationinsights.web.spring.RequestNameHandlerInterceptorAdapter" />
        </mvc:interceptor>
    </mvc:interceptors>
```

#### <a name="if-youre-using-struts-2"></a><span data-ttu-id="8773a-180">Struts 2 kullanıyorsanız</span><span class="sxs-lookup"><span data-stu-id="8773a-180">If you're using Struts 2</span></span>
<span data-ttu-id="8773a-181">Bu öğeyi Struts yapılandırma dosyasına ekleyin (genellikle struts.xml veya struts default.xml adıyla):</span><span class="sxs-lookup"><span data-stu-id="8773a-181">Add this item to the Struts configuration file (usually named struts.xml or struts-default.xml):</span></span>

```XML

     <interceptors>
       <interceptor name="ApplicationInsightsRequestNameInterceptor" class="com.microsoft.applicationinsights.web.struts.RequestNameInterceptor" />
     </interceptors>
     <default-interceptor-ref name="ApplicationInsightsRequestNameInterceptor" />
```

<span data-ttu-id="8773a-182">(Varsayılan yığında tanımlı dinleyiciler varsa, dinleyiciyi yalnızca o yığına eklenebilir.)</span><span class="sxs-lookup"><span data-stu-id="8773a-182">(If you have interceptors defined in a default stack, the interceptor can simply be added to that stack.)</span></span>

## <a name="5-run-your-application"></a><span data-ttu-id="8773a-183">5. Uygulamanızı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="8773a-183">5. Run your application</span></span>
<span data-ttu-id="8773a-184">Geliştirme makinenizde hata ayıklama modunda çalıştırın ya da sunucunuza yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="8773a-184">Either run it in debug mode on your development machine, or publish to your server.</span></span>

## <a name="6-view-your-telemetry-in-application-insights"></a><span data-ttu-id="8773a-185">6. Application Insights'da telemetrinizi görüntüleme</span><span class="sxs-lookup"><span data-stu-id="8773a-185">6. View your telemetry in Application Insights</span></span>
<span data-ttu-id="8773a-186">[Microsoft Azure portalında](https://portal.azure.com), Application Insights kaynağınıza dönün.</span><span class="sxs-lookup"><span data-stu-id="8773a-186">Return to your Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="8773a-187">HTTP isteklerine ilişkin veriler genel bakış dikey penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="8773a-187">HTTP requests data appears on the overview blade.</span></span> <span data-ttu-id="8773a-188">(Orada değilse, birkaç saniye bekleyip Yenile’ye tıklayın.)</span><span class="sxs-lookup"><span data-stu-id="8773a-188">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![örnek veri](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="8773a-190">[Ölçümler hakkında daha fazla bilgi edinin.][metrics]</span><span class="sxs-lookup"><span data-stu-id="8773a-190">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="8773a-191">Daha ayrıntılı derlenmiş ölçümler görmek için herhangi bir grafiğe tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8773a-191">Click through any chart to see more detailed aggregated metrics.</span></span>

![](./media/app-insights-java-get-started/6-barchart.png)

> <span data-ttu-id="8773a-192">Application Insights, MVC uygulamaları için HTTP isteklerinin biçiminin şu olduğunu varsayar: `VERB controller/action`.</span><span class="sxs-lookup"><span data-stu-id="8773a-192">Application Insights assumes the format of HTTP requests for MVC applications is: `VERB controller/action`.</span></span> <span data-ttu-id="8773a-193">Örneğin, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` ve `GET Home/Product/sdf96vws`; `GET Home/Product` içinde gruplandırılır.</span><span class="sxs-lookup"><span data-stu-id="8773a-193">For example, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` and `GET Home/Product/sdf96vws` are grouped into `GET Home/Product`.</span></span> <span data-ttu-id="8773a-194">Bu gruplandırma, istek sayısı veya isteklerin yürütülme süresi gibi anlamlı istek toplamalarını etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="8773a-194">This grouping enables meaningful aggregations of requests, such as number of requests and average execution time for requests.</span></span>
>
>

### <a name="instance-data"></a><span data-ttu-id="8773a-195">Örnek veriler</span><span class="sxs-lookup"><span data-stu-id="8773a-195">Instance data</span></span>
<span data-ttu-id="8773a-196">Ayrı ayrı örnekleri görmek için belirli bir istek türüne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8773a-196">Click through a specific request type to see individual instances.</span></span>

<span data-ttu-id="8773a-197">Application Insights’ta iki tür veri görüntülenir: ortalama, sayım ve toplam olarak depolanan birleşik veriler; HTTP isteklerinin tek tek raporu, özel durumlar, sayfa görünümleri veya özel olaylar olarak görüntülenen örnek veriler.</span><span class="sxs-lookup"><span data-stu-id="8773a-197">Two kinds of data are displayed in Application Insights: aggregated data, stored and displayed as averages, counts, and sums; and instance data - individual reports of HTTP requests, exceptions, page views, or custom events.</span></span>

<span data-ttu-id="8773a-198">İstek özellikleri görüntülendiğinde, istekler ve özel durumlar gibi bununla ilişkili telemetri olayları görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8773a-198">When viewing the properties of a request, you can see the telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-get-started/7-instance.png)

### <a name="analytics-powerful-query-language"></a><span data-ttu-id="8773a-199">Analiz: Güçlü sorgu dili</span><span class="sxs-lookup"><span data-stu-id="8773a-199">Analytics: Powerful query language</span></span>
<span data-ttu-id="8773a-200">Daha fazla veri birleştirdiğinizde hem veri toplama, hem de tek tek örneklerini bulmak için sorguları çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8773a-200">As you accumulate more data, you can run queries both to aggregate data and to find individual instances.</span></span>  <span data-ttu-id="8773a-201">[Analiz](app-insights-analytics.md) hem performans, hem de kullanım için olmasının yanı sıra tanılama için de güçlü bir araçtır.</span><span class="sxs-lookup"><span data-stu-id="8773a-201">[Analytics](app-insights-analytics.md) is a powerful tool for both for understanding performance and usage, and for diagnostic purposes.</span></span>

![Analizi örneği](./media/app-insights-java-get-started/025.png)

## <a name="7-install-your-app-on-the-server"></a><span data-ttu-id="8773a-203">7. Uygulamanızı sunucuya yükleme</span><span class="sxs-lookup"><span data-stu-id="8773a-203">7. Install your app on the server</span></span>
<span data-ttu-id="8773a-204">Artık uygulamanızı sunucuya yayımlayın, herkesin kullanmasını sağlayın ve portalda gösterilen telemetriye bakın.</span><span class="sxs-lookup"><span data-stu-id="8773a-204">Now publish your app to the server, let people use it, and watch the telemetry show up on the portal.</span></span>

* <span data-ttu-id="8773a-205">Güvenlik duvarınızın, uygulamanıza şu bağlantı noktalarına telemetri göndermesine izin verdiğinden emin olun:</span><span class="sxs-lookup"><span data-stu-id="8773a-205">Make sure your firewall allows your application to send telemetry to these ports:</span></span>

  * <span data-ttu-id="8773a-206">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="8773a-206">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="8773a-207">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="8773a-207">f5.services.visualstudio.com:443</span></span>

* <span data-ttu-id="8773a-208">Giden trafiğin güvenlik duvarından geçirilmesi gerekiyorsa, `http.proxyHost` ve `http.proxyPort` sistem özelliklerini tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="8773a-208">If outgoing traffic must be routed through a firewall, define system properties `http.proxyHost` and `http.proxyPort`.</span></span>

* <span data-ttu-id="8773a-209">Windows sunucularda yüklenecekler:</span><span class="sxs-lookup"><span data-stu-id="8773a-209">On Windows servers, install:</span></span>

  * [<span data-ttu-id="8773a-210">Microsoft Visual C++ Yeniden Dağıtılabilir</span><span class="sxs-lookup"><span data-stu-id="8773a-210">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="8773a-211">(Bu bileşen, performans sayaçlarını etkinleştirir.)</span><span class="sxs-lookup"><span data-stu-id="8773a-211">(This component enables performance counters.)</span></span>


## <a name="exceptions-and-request-failures"></a><span data-ttu-id="8773a-212">Özel durumlar ve istek hataları</span><span class="sxs-lookup"><span data-stu-id="8773a-212">Exceptions and request failures</span></span>
<span data-ttu-id="8773a-213">İşlenmeyen özel durumlar otomatik olarak toplanır:</span><span class="sxs-lookup"><span data-stu-id="8773a-213">Unhandled exceptions are automatically collected:</span></span>

![Ayarlar, Hatalar’ı açın](./media/app-insights-java-get-started/21-exceptions.png)

<span data-ttu-id="8773a-215">Diğer özel durumlar hakkında veri toplamak için iki seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="8773a-215">To collect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="8773a-216">[Kodunuzda trackException() çağrıları ekleme][apiexceptions].</span><span class="sxs-lookup"><span data-stu-id="8773a-216">[Insert calls to trackException() in your code][apiexceptions].</span></span>
* <span data-ttu-id="8773a-217">[Sunucunuza Java Agent yükleme](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="8773a-217">[Install the Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="8773a-218">İzlemek istediğiniz yöntemleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="8773a-218">You specify the methods you want to watch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="8773a-219">Yöntem çağrılarını ve dış bağımlılıkları izleme</span><span class="sxs-lookup"><span data-stu-id="8773a-219">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="8773a-220">Zamanlama verileriyle JDBC üzerinden yapılan belirli dahili yöntemleri ve çağrıları kaydetmek için [Java Agent yükleme](app-insights-java-agent.md) işlemini gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="8773a-220">[Install the Java Agent](app-insights-java-agent.md) to log specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="8773a-221">Performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="8773a-221">Performance counters</span></span>
<span data-ttu-id="8773a-222">Çeşitli performans sayaçlarını görmek için **Ayarlar**, **Sunucular**’ı açın.</span><span class="sxs-lookup"><span data-stu-id="8773a-222">Open **Settings**, **Servers**, to see a range of performance counters.</span></span>

![](./media/app-insights-java-get-started/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="8773a-223">Performans sayacı koleksiyonunu özelleştirme</span><span class="sxs-lookup"><span data-stu-id="8773a-223">Customize performance counter collection</span></span>
<span data-ttu-id="8773a-224">Standart performans sayaçları dizisinin koleksiyonunu devre dışı bırakmak için aşağıdaki kodu ApplicationInsights.xml dosyasının kök düğümü altına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="8773a-224">To disable collection of the standard set of performance counters, add the following code under the root node of the ApplicationInsights.xml file:</span></span>

```XML
    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="8773a-225">Ek performans sayaçlarını toplama</span><span class="sxs-lookup"><span data-stu-id="8773a-225">Collect additional performance counters</span></span>
<span data-ttu-id="8773a-226">Toplanacak ek performans sayaçları belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8773a-226">You can specify additional performance counters to be collected.</span></span>

#### <a name="jmx-counters-exposed-by-the-java-virtual-machine"></a><span data-ttu-id="8773a-227">JMX sayaçları (Java Sanal Makinesi tarafından gösterilen)</span><span class="sxs-lookup"><span data-stu-id="8773a-227">JMX counters (exposed by the Java Virtual Machine)</span></span>

```XML
    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="8773a-228">`displayName` – Application Insights portalında görüntülenen ad.</span><span class="sxs-lookup"><span data-stu-id="8773a-228">`displayName` – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="8773a-229">`objectName` – JMX nesne adı.</span><span class="sxs-lookup"><span data-stu-id="8773a-229">`objectName` – The JMX object name.</span></span>
* <span data-ttu-id="8773a-230">`attribute` – Getirilecek JMX nesne adının özniteliği</span><span class="sxs-lookup"><span data-stu-id="8773a-230">`attribute` – The attribute of the JMX object name to fetch</span></span>
* <span data-ttu-id="8773a-231">`type` (isteğe bağlı) - JMX nesnenin öznitelik türü:</span><span class="sxs-lookup"><span data-stu-id="8773a-231">`type` (optional) - The type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="8773a-232">Varsayılan: int veya long gibi basit bir tür.</span><span class="sxs-lookup"><span data-stu-id="8773a-232">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="8773a-233">`composite`: performans sayacı verileri 'Attribute.Data' biçimindedir</span><span class="sxs-lookup"><span data-stu-id="8773a-233">`composite`: the perf counter data is in the format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="8773a-234">`tabular`: performans sayacı verileri tablo satırı biçimindedir</span><span class="sxs-lookup"><span data-stu-id="8773a-234">`tabular`: the perf counter data is in the format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="8773a-235">Windows performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="8773a-235">Windows performance counters</span></span>
<span data-ttu-id="8773a-236">Her [Windows performans sayacı](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) bir kategorinin üyesidir (alanın bir sınıf üyesi olması gibi).</span><span class="sxs-lookup"><span data-stu-id="8773a-236">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in the same way that a field is a member of a class).</span></span> <span data-ttu-id="8773a-237">Kategoriler genel olabileceği gibi numaralı veya adlı örneklere de sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="8773a-237">Categories can either be global, or can have numbered or named instances.</span></span>

```XML
    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="8773a-238">displayName – Application Insights portalında görüntülenen ad.</span><span class="sxs-lookup"><span data-stu-id="8773a-238">displayName – The name displayed in the Application Insights portal.</span></span>
* <span data-ttu-id="8773a-239">categoryName – Bu performans sayacıyla ilişkili performans sayacı kategorisi (performans nesnesi).</span><span class="sxs-lookup"><span data-stu-id="8773a-239">categoryName – The performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="8773a-240">counterName – Performans sayacının adı.</span><span class="sxs-lookup"><span data-stu-id="8773a-240">counterName – The name of the performance counter.</span></span>
* <span data-ttu-id="8773a-241">instanceName – Performans sayacı kategorisi örneğinin adı veya kategoride tek örnek varsa boş bir dize ("").</span><span class="sxs-lookup"><span data-stu-id="8773a-241">instanceName – The name of the performance counter category instance, or an empty string (""), if the category contains a single instance.</span></span> <span data-ttu-id="8773a-242">categoryName adı Process olursa ve uygulamanızın çalıştığı geçerli JVM işleminden performans sayacını toplamak istiyorsanız `"__SELF__"` öğesini belirtin.</span><span class="sxs-lookup"><span data-stu-id="8773a-242">If the categoryName is Process, and the performance counter you'd like to collect is from the current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="8773a-243">Özel ölçümleriniz [Ölçüm Gezgini][metrics]'nde olduğundan performans sayaçlarınız görünürdür.</span><span class="sxs-lookup"><span data-stu-id="8773a-243">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-get-started/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="8773a-244">Unix Performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="8773a-244">Unix performance counters</span></span>
* <span data-ttu-id="8773a-245">Çok çeşitli sistem ve ağ verisi almak için [Application Insights eklentisiyle collectd yükleyin](app-insights-java-collectd.md).</span><span class="sxs-lookup"><span data-stu-id="8773a-245">[Install collectd with the Application Insights plugin](app-insights-java-collectd.md) to get a wide variety of system and network data.</span></span>

## <a name="get-user-and-session-data"></a><span data-ttu-id="8773a-246">Kullanıcı ve oturum verilerini alma</span><span class="sxs-lookup"><span data-stu-id="8773a-246">Get user and session data</span></span>
<span data-ttu-id="8773a-247">Tamam, web sunucunuzdan telemetri gönderiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="8773a-247">OK, you're sending telemetry from your web server.</span></span> <span data-ttu-id="8773a-248">Uygulamanızın 360 derecelik tam görünümünü almak için izlemeye katabileceğiniz birkaç şey daha vardır:</span><span class="sxs-lookup"><span data-stu-id="8773a-248">Now to get the full 360-degree view of your application, you can add more monitoring:</span></span>

* <span data-ttu-id="8773a-249">Sayfa görünümlerini ve kullanıcı ölçümlerini izlemek için [web sayfalarınıza telemetri ekleyin][usage].</span><span class="sxs-lookup"><span data-stu-id="8773a-249">[Add telemetry to your web pages][usage] to monitor page views and user metrics.</span></span>
* <span data-ttu-id="8773a-250">Uygulamanızın canlı ve duyarlı kaldığından emin olmak için [web testleri oluşturun][availability].</span><span class="sxs-lookup"><span data-stu-id="8773a-250">[Set up web tests][availability] to make sure your application stays live and responsive.</span></span>

## <a name="capture-log-traces"></a><span data-ttu-id="8773a-251">Günlük izlemelerini yakalama</span><span class="sxs-lookup"><span data-stu-id="8773a-251">Capture log traces</span></span>
<span data-ttu-id="8773a-252">Log4J, Logback veya diğer günlük altyapılarına ait günlükleri ayrıntılı incelemek için Application Insights’ı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8773a-252">You can use Application Insights to slice and dice logs from Log4J, Logback, or other logging frameworks.</span></span> <span data-ttu-id="8773a-253">Günlükleri HTTP istekleri ve başka telemetriyle ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8773a-253">You can correlate the logs with HTTP requests and other telemetry.</span></span> <span data-ttu-id="8773a-254">[Nasıl olduğunu öğrenin][javalogs].</span><span class="sxs-lookup"><span data-stu-id="8773a-254">[Learn how][javalogs].</span></span>

## <a name="send-your-own-telemetry"></a><span data-ttu-id="8773a-255">Kendi telemetrinizi gönderme</span><span class="sxs-lookup"><span data-stu-id="8773a-255">Send your own telemetry</span></span>
<span data-ttu-id="8773a-256">Artık SDK'yı da yüklediğinize göre, kendi telemetrinizi göndermek için API'yi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8773a-256">Now that you've installed the SDK, you can use the API to send your own telemetry.</span></span>

* <span data-ttu-id="8773a-257">Uygulamanızla kullanıcıların ne yaptıklarını öğrenmek için [Özel olayları ve ölçümleri izleyin][api].</span><span class="sxs-lookup"><span data-stu-id="8773a-257">[Track custom events and metrics][api] to learn what users are doing with your application.</span></span>
* <span data-ttu-id="8773a-258">Sorunların tanımlanması için [Olayları ve günlükleri arayın][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="8773a-258">[Search events and logs][diagnostic] to help diagnose problems.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="8773a-259">Kullanılabilirlik web testleri</span><span class="sxs-lookup"><span data-stu-id="8773a-259">Availability web tests</span></span>
<span data-ttu-id="8773a-260">Kullanıma hazır ve düzgün yanıt verdiğini denetlemek için Application Insights belirli aralıklarla web sitenizi test edebilir.</span><span class="sxs-lookup"><span data-stu-id="8773a-260">Application Insights can test your website at regular intervals to check that it's up and responding well.</span></span> <span data-ttu-id="8773a-261">[Ayarlamak için][availability], Web testleri'ne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8773a-261">[To set up][availability], click Web tests.</span></span>

![Web testleri’ne ve ardından Web testi ekle’ye tıklayın](./media/app-insights-java-get-started/31-config-web-test.png)

<span data-ttu-id="8773a-263">Yanıt süreleri grafiklerine ek olarak, siteniz devre dışı kalırsa e-posta bildirimleri de alacaksınız.</span><span class="sxs-lookup"><span data-stu-id="8773a-263">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Web testi örneği](./media/app-insights-java-get-started/appinsights-10webtestresult.png)

<span data-ttu-id="8773a-265">[Kullanılabilirlik web testleri hakkında daha fazla bilgi edinin.][availability]</span><span class="sxs-lookup"><span data-stu-id="8773a-265">[Learn more about availability web tests.][availability]</span></span>

## <a name="questions-problems"></a><span data-ttu-id="8773a-266">Sorularınız mı var?</span><span class="sxs-lookup"><span data-stu-id="8773a-266">Questions?</span></span> <span data-ttu-id="8773a-267">Sorunlarınız mı var?</span><span class="sxs-lookup"><span data-stu-id="8773a-267">Problems?</span></span>
[<span data-ttu-id="8773a-268">Java Sorun Giderme</span><span class="sxs-lookup"><span data-stu-id="8773a-268">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

## <a name="video"></a><span data-ttu-id="8773a-269">Video</span><span class="sxs-lookup"><span data-stu-id="8773a-269">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="8773a-270">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8773a-270">Next steps</span></span>
* [<span data-ttu-id="8773a-271">Bağımlılık çağrılarını izleme</span><span class="sxs-lookup"><span data-stu-id="8773a-271">Monitor dependency calls</span></span>](app-insights-java-agent.md)
* [<span data-ttu-id="8773a-272">Unix Performans sayaçlarını izleme</span><span class="sxs-lookup"><span data-stu-id="8773a-272">Monitor Unix performance counters</span></span>](app-insights-java-collectd.md)
* <span data-ttu-id="8773a-273">Sayfa yükleme sürelerini, AJAX çağrılarını ve tarayıcı özel durumlarını izlemek için [web sayfalarınıza izleme ekleyin](app-insights-javascript.md).</span><span class="sxs-lookup"><span data-stu-id="8773a-273">Add [monitoring to your web pages](app-insights-javascript.md) to monitor page load times, AJAX calls, browser exceptions.</span></span>
* <span data-ttu-id="8773a-274">Tarayıcıda veya sunucuda kullanımı izlemek için [özel telemetri](app-insights-api-custom-events-metrics.md) yazın.</span><span class="sxs-lookup"><span data-stu-id="8773a-274">Write [custom telemetry](app-insights-api-custom-events-metrics.md) to track usage in the browser or at the server.</span></span>
* <span data-ttu-id="8773a-275">Sisteminizi izlemek üzere anahtar grafikleri bir araya getirmek için [panolar](app-insights-dashboards.md) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8773a-275">Create [dashboards](app-insights-dashboards.md) to bring together the key charts for monitoring your system.</span></span>
* <span data-ttu-id="8773a-276">Uygulamanızdan telemetri üzerinde güçlü sorgular yapmak için [Analytics](app-insights-analytics.md)'i kullanın</span><span class="sxs-lookup"><span data-stu-id="8773a-276">Use  [Analytics](app-insights-analytics.md) for powerful queries over telemetry from your app</span></span>
* <span data-ttu-id="8773a-277">Daha fazla bilgi için bkz. [Java geliştiricileri için Azure](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="8773a-277">For more information, visit [Azure for Java developers](/java/azure).</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#trackexception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[usage]: app-insights-javascript.md
