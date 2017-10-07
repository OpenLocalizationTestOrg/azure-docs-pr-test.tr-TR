---
title: "Azure Application Insights ile aaaJava web uygulaması analizi | Microsoft Docs"
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
ms.openlocfilehash: 6555ee53a44f937350e4fa296080f7dce4f45226
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-in-a-java-web-project"></a><span data-ttu-id="b3718-103">Java web projesinde Application Insights ile başlarken</span><span class="sxs-lookup"><span data-stu-id="b3718-103">Get started with Application Insights in a Java web project</span></span>


<span data-ttu-id="b3718-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) yardımcı olan web geliştiricileri hello performansını ve canlı uygulamanızın kullanımını anlamak için bir genişletilebilir bir analiz hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="b3718-104">[Application Insights](https://azure.microsoft.com/services/application-insights/) is an extensible analytics service for web developers that helps you understand hello performance and usage of your live application.</span></span> <span data-ttu-id="b3718-105">Çok kullanmak[performans sorunlarını ve özel durumlarını saptayıp tanılamanıza](app-insights-detect-triage-diagnose.md), ve [kod yazmayı] [ api] tootrack hangi kullanıcıların uygulamanızı yapın.</span><span class="sxs-lookup"><span data-stu-id="b3718-105">Use it too[detect and diagnose performance issues and exceptions](app-insights-detect-triage-diagnose.md), and [write code][api] tootrack what users do with your app.</span></span>

![örnek veri](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="b3718-107">Application Insights; Linux, Unix veya Windows üzerinde çalışan Java uygulamalarını destekler.</span><span class="sxs-lookup"><span data-stu-id="b3718-107">Application Insights supports Java apps running on Linux, Unix, or Windows.</span></span>

<span data-ttu-id="b3718-108">Gerekenler:</span><span class="sxs-lookup"><span data-stu-id="b3718-108">You need:</span></span>

* <span data-ttu-id="b3718-109">Oracle JRE 1.6 veya sonraki sürümleri ya da Zulu JRE 1.6 veya sonraki sürümleri</span><span class="sxs-lookup"><span data-stu-id="b3718-109">Oracle JRE 1.6 or later, or Zulu JRE 1.6 or later</span></span>
* <span data-ttu-id="b3718-110">Bir abonelik çok[Microsoft Azure](https://azure.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="b3718-110">A subscription too[Microsoft Azure](https://azure.microsoft.com/).</span></span>

<span data-ttu-id="b3718-111">*Zaten Canlı olan bir web uygulaması varsa, hello alternatif yordam çok izleyebilirsiniz[hello SDK hello web sunucusunda çalışma zamanında ekleme](app-insights-java-live.md). Bu alternatif hello kodun yeniden engellese de, hello seçeneği toowrite kod tootrack kullanıcı etkinliği elde etmezsiniz.*</span><span class="sxs-lookup"><span data-stu-id="b3718-111">*If you have a web app that's already live, you could follow hello alternative procedure too[add hello SDK at runtime in hello web server](app-insights-java-live.md). That alternative avoids rebuilding hello code, but you don't get hello option toowrite code tootrack user activity.*</span></span>

## <a name="1-get-an-application-insights-instrumentation-key"></a><span data-ttu-id="b3718-112">1. Application Insights izleme anahtarı edinme</span><span class="sxs-lookup"><span data-stu-id="b3718-112">1. Get an Application Insights instrumentation key</span></span>
1. <span data-ttu-id="b3718-113">İçinde toohello oturum [Microsoft Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b3718-113">Sign in toohello [Microsoft Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b3718-114">Bir Application Insights kaynağı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="b3718-114">Create an Application Insights resource.</span></span> <span data-ttu-id="b3718-115">Merhaba uygulama türü tooJava web uygulaması ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="b3718-115">Set hello application type tooJava web application.</span></span>

    ![Ad girme, Java web uygulaması seçme ve Oluştur’a tıklama](./media/app-insights-java-get-started/02-create.png)
3. <span data-ttu-id="b3718-117">Hello hello yeni kaynağın izleme anahtarını bulun.</span><span class="sxs-lookup"><span data-stu-id="b3718-117">Find hello instrumentation key of hello new resource.</span></span> <span data-ttu-id="b3718-118">Toopaste bu anahtar kod projenize kısa bir süre sonra ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="b3718-118">You'll need toopaste this key into your code project shortly.</span></span>

    ![Merhaba yeni kaynağa genel bakışta, Özellikler'i tıklatın ve hello izleme anahtarını kopyalama](./media/app-insights-java-get-started/03-key.png)

## <a name="2-add-hello-application-insights-sdk-for-java-tooyour-project"></a><span data-ttu-id="b3718-120">2. Java tooyour projesi için Hello Application Insights SDK ekleme</span><span class="sxs-lookup"><span data-stu-id="b3718-120">2. Add hello Application Insights SDK for Java tooyour project</span></span>
<span data-ttu-id="b3718-121">*Projeniz için uygun şekilde Hello seçin.*</span><span class="sxs-lookup"><span data-stu-id="b3718-121">*Choose hello appropriate way for your project.*</span></span>

#### <a name="if-youre-using-eclipse-toocreate-a-maven-or-dynamic-web-project-"></a><span data-ttu-id="b3718-122">Kullanıyorsanız, toocreate Maven veya dinamik Web projesi Tutulma...</span><span class="sxs-lookup"><span data-stu-id="b3718-122">If you're using Eclipse toocreate a Maven or Dynamic Web project ...</span></span>
<span data-ttu-id="b3718-123">Kullanım hello [Java eklentisi için Application Insights SDK][eclipse].</span><span class="sxs-lookup"><span data-stu-id="b3718-123">Use hello [Application Insights SDK for Java plug-in][eclipse].</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="b3718-124">Maven kullanıyorsanız...</span><span class="sxs-lookup"><span data-stu-id="b3718-124">If you're using Maven...</span></span>
<span data-ttu-id="b3718-125">Projeniz zaten toouse Maven derleme için ayarladıysanız, aşağıdaki kodu tooyour pom.xml dosyasına hello birleştirin.</span><span class="sxs-lookup"><span data-stu-id="b3718-125">If your project is already set up toouse Maven for build, merge hello following code tooyour pom.xml file.</span></span>

<span data-ttu-id="b3718-126">Ardından, yenileme hello proje bağımlılıkları tooget hello ikili dosyaları indirilir.</span><span class="sxs-lookup"><span data-stu-id="b3718-126">Then, refresh hello project dependencies tooget hello binaries downloaded.</span></span>

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

* <span data-ttu-id="b3718-127">*Derleme veya sağlama toplamı doğrulama hataları mı var?*</span><span class="sxs-lookup"><span data-stu-id="b3718-127">*Build or checksum validation errors?*</span></span> <span data-ttu-id="b3718-128">`<version>1.0.n</version>` gibi belirli bir sürümü kullanmayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="b3718-128">Try using a specific version, such as: `<version>1.0.n</version>`.</span></span> <span data-ttu-id="b3718-129">Hello hello en son sürümünü bulacaksınız [SDK sürüm notlarında](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) veya bizim [Maven yapıtları](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span><span class="sxs-lookup"><span data-stu-id="b3718-129">You'll find hello latest version in hello [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) or in our [Maven artifacts](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights).</span></span>
* <span data-ttu-id="b3718-130">*Tooupdate tooa gereken yeni SDK?*</span><span class="sxs-lookup"><span data-stu-id="b3718-130">*Need tooupdate tooa new SDK?*</span></span> <span data-ttu-id="b3718-131">Proje bağımlılıklarınızı yenileyin.</span><span class="sxs-lookup"><span data-stu-id="b3718-131">Refresh your project's dependencies.</span></span>

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="b3718-132">Gradle kullanıyorsanız...</span><span class="sxs-lookup"><span data-stu-id="b3718-132">If you're using Gradle...</span></span>
<span data-ttu-id="b3718-133">Projeniz zaten toouse Gradle derleme için ayarladıysanız, aşağıdaki kodu tooyour build.gradle dosyasına hello birleştirin.</span><span class="sxs-lookup"><span data-stu-id="b3718-133">If your project is already set up toouse Gradle for build, merge hello following code tooyour build.gradle file.</span></span>

<span data-ttu-id="b3718-134">Ardından yenileme hello proje bağımlılıkları tooget hello ikili dosyaları indirilir.</span><span class="sxs-lookup"><span data-stu-id="b3718-134">Then refresh hello project dependencies tooget hello binaries downloaded.</span></span>

```JSON

    repositories {
      mavenCentral()
    }

    dependencies {
      compile group: 'com.microsoft.azure', name: 'applicationinsights-web', version: '1.+'
      // or applicationinsights-core for bare API
    }
```

* <span data-ttu-id="b3718-135">*Derleme veya sağlama toplamı doğrulama hataları mı var? `version:'1.0.n'` gibi belirli bir sürümü kullanmayı deneyin*.</span><span class="sxs-lookup"><span data-stu-id="b3718-135">*Build or checksum validation errors? Try using a specific version, such as:* `version:'1.0.n'`.</span></span> <span data-ttu-id="b3718-136">*Hello hello en son sürümünü bulacaksınız [SDK sürüm notlarında](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span><span class="sxs-lookup"><span data-stu-id="b3718-136">*You'll find hello latest version in hello [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).*</span></span>
* <span data-ttu-id="b3718-137">*tooupdate tooa yeni SDK'sı*</span><span class="sxs-lookup"><span data-stu-id="b3718-137">*tooupdate tooa new SDK*</span></span>
  * <span data-ttu-id="b3718-138">Proje bağımlılıklarınızı yenileyin.</span><span class="sxs-lookup"><span data-stu-id="b3718-138">Refresh your project's dependencies.</span></span>

#### <a name="otherwise-"></a><span data-ttu-id="b3718-139">Aksi taktirde...</span><span class="sxs-lookup"><span data-stu-id="b3718-139">Otherwise ...</span></span>
<span data-ttu-id="b3718-140">El ile Merhaba SDK ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b3718-140">Manually add hello SDK:</span></span>

1. <span data-ttu-id="b3718-141">Merhaba karşıdan [Java için Application Insights SDK](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="b3718-141">Download hello [Application Insights SDK for Java](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="b3718-142">Hello ikili dosyaları hello zip dosyasından ayıklayıp tooyour proje ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b3718-142">Extract hello binaries from hello zip file and add them tooyour project.</span></span>

### <a name="questions"></a><span data-ttu-id="b3718-143">Sorular...</span><span class="sxs-lookup"><span data-stu-id="b3718-143">Questions...</span></span>
* <span data-ttu-id="b3718-144">*Merhaba hello arasındaki ilişki nedir `-core` ve `-web` hello zip bileşenlerinde?*</span><span class="sxs-lookup"><span data-stu-id="b3718-144">*What's hello relationship between hello `-core` and `-web` components in hello zip?*</span></span>

  * <span data-ttu-id="b3718-145">`applicationinsights-core`tam API hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="b3718-145">`applicationinsights-core` gives you hello bare API.</span></span> <span data-ttu-id="b3718-146">Bu bileşen her zaman gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="b3718-146">You always need this component.</span></span>
  * <span data-ttu-id="b3718-147">`applicationinsights-web`, HTTP istek sayısını ve yanıt sürelerini izleyen ölçümleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="b3718-147">`applicationinsights-web` gives you metrics that track HTTP request counts and response times.</span></span> <span data-ttu-id="b3718-148">Bu telemetrinin otomatik olarak toplanmasını istemiyorsanız, bu bileşeni atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3718-148">You can omit this component if you don't want this telemetry automatically collected.</span></span> <span data-ttu-id="b3718-149">Örneğin, toowrite kendi istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="b3718-149">For example, if you want toowrite your own.</span></span>
* <span data-ttu-id="b3718-150">*tooupdate hello değişiklikleri yayımladığınızda SDK*</span><span class="sxs-lookup"><span data-stu-id="b3718-150">*tooupdate hello SDK when we publish changes*</span></span>

  * <span data-ttu-id="b3718-151">Merhaba son karşıdan [Java için Application Insights SDK](https://aka.ms/qqkaq6) ve eskilerle hello Değiştir.</span><span class="sxs-lookup"><span data-stu-id="b3718-151">Download hello latest [Application Insights SDK for Java](https://aka.ms/qqkaq6) and replace hello old ones.</span></span>
  * <span data-ttu-id="b3718-152">Değişiklikleri hello açıklanan [SDK sürüm notlarında](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span><span class="sxs-lookup"><span data-stu-id="b3718-152">Changes are described in hello [SDK release notes](https://github.com/Microsoft/ApplicationInsights-Java#release-notes).</span></span>

## <a name="3-add-an-application-insights-xml-file"></a><span data-ttu-id="b3718-153">3. Application Insights .xml dosyasını ekleme</span><span class="sxs-lookup"><span data-stu-id="b3718-153">3. Add an Application Insights .xml file</span></span>
<span data-ttu-id="b3718-154">Projenizde toohello kaynaklar klasörüne applicationınsights.xml dosyasını ekleyin veya tooyour projenin dağıtım sınıfı yoluna eklendiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="b3718-154">Add ApplicationInsights.xml toohello resources folder in your project, or make sure it is added tooyour project’s deployment class path.</span></span> <span data-ttu-id="b3718-155">XML içine aşağıdaki hello kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="b3718-155">Copy hello following XML into it.</span></span>

<span data-ttu-id="b3718-156">Hello Azure portal ' aldığınız hello izleme anahtarını Bununla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b3718-156">Substitute hello instrumentation key that you got from hello Azure portal.</span></span>

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


* <span data-ttu-id="b3718-157">Merhaba izleme anahtarı telemetrinin her öğesiyle birlikte gönderilir ve Application Insights toodisplay söyler kaynağınız içinde.</span><span class="sxs-lookup"><span data-stu-id="b3718-157">hello instrumentation key is sent along with every item of telemetry and tells Application Insights toodisplay it in your resource.</span></span>
* <span data-ttu-id="b3718-158">Merhaba HTTP isteği bileşeni isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="b3718-158">hello HTTP Request component is optional.</span></span> <span data-ttu-id="b3718-159">İstek ve yanıt sürelerini toohello portal hakkında telemetriyi otomatik olarak gönderir.</span><span class="sxs-lookup"><span data-stu-id="b3718-159">It automatically sends telemetry about requests and response times toohello portal.</span></span>
* <span data-ttu-id="b3718-160">Olay bağıntısı bir toplama toohello HTTP isteği bileşendir.</span><span class="sxs-lookup"><span data-stu-id="b3718-160">Events correlation is an addition toohello HTTP request component.</span></span> <span data-ttu-id="b3718-161">Merhaba sunucu tarafından alınan bir tanımlayıcı tooeach isteği atar ve bu tanımlayıcı telemetri bir özellik tooevery öğesi olarak 'Operation.Id' hello özelliği olarak ekler.</span><span class="sxs-lookup"><span data-stu-id="b3718-161">It assigns an identifier tooeach request received by hello server, and adds this identifier as a property tooevery item of telemetry as hello property 'Operation.Id'.</span></span> <span data-ttu-id="b3718-162">Bir filtre ayarlayarak her istekle ilişkili toocorrelate hello telemetri tanır [tanılama arama][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="b3718-162">It allows you toocorrelate hello telemetry associated with each request by setting a filter in [diagnostic search][diagnostic].</span></span>
* <span data-ttu-id="b3718-163">Merhaba Application Insights anahtar geçirilebilir dinamik olarak hello Azure portalında bir sistem özelliği olarak (-DAPPLICATION_INSIGHTS_IKEY your_ikey =).</span><span class="sxs-lookup"><span data-stu-id="b3718-163">hello Application Insights key can be passed dynamically from hello Azure portal as a system property (-DAPPLICATION_INSIGHTS_IKEY=your_ikey).</span></span> <span data-ttu-id="b3718-164">Tanımlı bir özellik yoksa, Azure Uygulama Ayarlarında ortam değişkeni (APPLICATION_INSIGHTS_IKEY) denetlenir.</span><span class="sxs-lookup"><span data-stu-id="b3718-164">If there is no property defined, it checks for environment variable (APPLICATION_INSIGHTS_IKEY) in Azure App Settings.</span></span> <span data-ttu-id="b3718-165">Her iki hello özellikleri tanımsızdır hello varsayılan InstrumentationKey Applicationınsights.xml kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b3718-165">If both hello properties are undefined, hello default InstrumentationKey is used from ApplicationInsights.xml.</span></span> <span data-ttu-id="b3718-166">Bu sıra toomanage yardımcı olan farklı ortamlar için farklı InstrumentationKeys dinamik olarak.</span><span class="sxs-lookup"><span data-stu-id="b3718-166">This sequence helps you toomanage different InstrumentationKeys for different environments dynamically.</span></span>

### <a name="alternative-ways-tooset-hello-instrumentation-key"></a><span data-ttu-id="b3718-167">Alternatif yolu tooset hello izleme anahtarı</span><span class="sxs-lookup"><span data-stu-id="b3718-167">Alternative ways tooset hello instrumentation key</span></span>
<span data-ttu-id="b3718-168">Application Insights SDK'sı hello anahtarı bu sırayla arar:</span><span class="sxs-lookup"><span data-stu-id="b3718-168">Application Insights SDK looks for hello key in this order:</span></span>

1. <span data-ttu-id="b3718-169">Sistem özelliği: -DAPPLICATION_INSIGHTS_IKEY=your_ikey</span><span class="sxs-lookup"><span data-stu-id="b3718-169">System property: -DAPPLICATION_INSIGHTS_IKEY=your_ikey</span></span>
2. <span data-ttu-id="b3718-170">Ortam değişkeni: APPLICATION_INSIGHTS_IKEY</span><span class="sxs-lookup"><span data-stu-id="b3718-170">Environment variable: APPLICATION_INSIGHTS_IKEY</span></span>
3. <span data-ttu-id="b3718-171">Yapılandırma dosyası: ApplicationInsights.xml</span><span class="sxs-lookup"><span data-stu-id="b3718-171">Configuration file: ApplicationInsights.xml</span></span>

<span data-ttu-id="b3718-172">Ayrıca [kod içinde ayarlayabilirsiniz](app-insights-api-custom-events-metrics.md#ikey):</span><span class="sxs-lookup"><span data-stu-id="b3718-172">You can also [set it in code](app-insights-api-custom-events-metrics.md#ikey):</span></span>

```Java

    telemetryClient.InstrumentationKey = "...";
```

## <a name="4-add-an-http-filter"></a><span data-ttu-id="b3718-173">4. HTTP filtresi ekleme</span><span class="sxs-lookup"><span data-stu-id="b3718-173">4. Add an HTTP filter</span></span>
<span data-ttu-id="b3718-174">Merhaba son yapılandırma adımı, her web isteğini hello HTTP isteği bileşeni toolog sağlar.</span><span class="sxs-lookup"><span data-stu-id="b3718-174">hello last configuration step allows hello HTTP request component toolog each web request.</span></span> <span data-ttu-id="b3718-175">(Yalnızca hello tam API istiyorsanız gerekmez.)</span><span class="sxs-lookup"><span data-stu-id="b3718-175">(Not required if you just want hello bare API.)</span></span>

<span data-ttu-id="b3718-176">Bulup, proje ve uygulama filtrelerinizin yapılandırıldığı koddan hello web uygulaması düğümü altında birleştirme hello hello web.xml dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="b3718-176">Locate and open hello web.xml file in your project, and merge hello following code under hello web-app node, where your application filters are configured.</span></span>

<span data-ttu-id="b3718-177">tooget hello en doğru sonuçlar, hello filtre önce tüm diğer filtrelerle eşlenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="b3718-177">tooget hello most accurate results, hello filter should be mapped before all other filters.</span></span>

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

#### <a name="if-youre-using-spring-web-mvc-31-or-later"></a><span data-ttu-id="b3718-178">Spring Web MVC 3.1 veya sonraki sürümleri kullanıyorsanız</span><span class="sxs-lookup"><span data-stu-id="b3718-178">If you're using Spring Web MVC 3.1 or later</span></span>
<span data-ttu-id="b3718-179">Bu öğeleri Düzenle *-servlet.xml tooinclude hello Application Insights paketi:</span><span class="sxs-lookup"><span data-stu-id="b3718-179">Edit these elements in *-servlet.xml tooinclude hello Application Insights package:</span></span>

```XML

    <context:component-scan base-package=" com.springapp.mvc, com.microsoft.applicationinsights.web.spring"/>

    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/**"/>
            <bean class="com.microsoft.applicationinsights.web.spring.RequestNameHandlerInterceptorAdapter" />
        </mvc:interceptor>
    </mvc:interceptors>
```

#### <a name="if-youre-using-struts-2"></a><span data-ttu-id="b3718-180">Struts 2 kullanıyorsanız</span><span class="sxs-lookup"><span data-stu-id="b3718-180">If you're using Struts 2</span></span>
<span data-ttu-id="b3718-181">Bu öğe toohello Struts yapılandırma dosyasına (genellikle adlandırılmış struts.xml veya struts default.xml) ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b3718-181">Add this item toohello Struts configuration file (usually named struts.xml or struts-default.xml):</span></span>

```XML

     <interceptors>
       <interceptor name="ApplicationInsightsRequestNameInterceptor" class="com.microsoft.applicationinsights.web.struts.RequestNameInterceptor" />
     </interceptors>
     <default-interceptor-ref name="ApplicationInsightsRequestNameInterceptor" />
```

<span data-ttu-id="b3718-182">(Varsayılan yığında tanımlı dinleyiciler varsa hello dinleyiciyi yalnızca toothat yığın eklenebilir.)</span><span class="sxs-lookup"><span data-stu-id="b3718-182">(If you have interceptors defined in a default stack, hello interceptor can simply be added toothat stack.)</span></span>

## <a name="5-run-your-application"></a><span data-ttu-id="b3718-183">5. Uygulamanızı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="b3718-183">5. Run your application</span></span>
<span data-ttu-id="b3718-184">Geliştirme makinenizde hata ayıklama modunda çalıştırın ya da tooyour server yayımlama.</span><span class="sxs-lookup"><span data-stu-id="b3718-184">Either run it in debug mode on your development machine, or publish tooyour server.</span></span>

## <a name="6-view-your-telemetry-in-application-insights"></a><span data-ttu-id="b3718-185">6. Application Insights'da telemetrinizi görüntüleme</span><span class="sxs-lookup"><span data-stu-id="b3718-185">6. View your telemetry in Application Insights</span></span>
<span data-ttu-id="b3718-186">Tooyour Application Insights kaynağını dönmek [Microsoft Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b3718-186">Return tooyour Application Insights resource in [Microsoft Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="b3718-187">HTTP istekleri verileri hello genel bakış dikey penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b3718-187">HTTP requests data appears on hello overview blade.</span></span> <span data-ttu-id="b3718-188">(Orada değilse, birkaç saniye bekleyip Yenile’ye tıklayın.)</span><span class="sxs-lookup"><span data-stu-id="b3718-188">(If it isn't there, wait a few seconds and then click Refresh.)</span></span>

![örnek veri](./media/app-insights-java-get-started/5-results.png)

<span data-ttu-id="b3718-190">[Ölçümler hakkında daha fazla bilgi edinin.][metrics]</span><span class="sxs-lookup"><span data-stu-id="b3718-190">[Learn more about metrics.][metrics]</span></span>

<span data-ttu-id="b3718-191">Daha ayrıntılı herhangi grafik toosee geçişli tıklatma ölçümleri birleştirilir.</span><span class="sxs-lookup"><span data-stu-id="b3718-191">Click through any chart toosee more detailed aggregated metrics.</span></span>

![](./media/app-insights-java-get-started/6-barchart.png)

> <span data-ttu-id="b3718-192">Application Insights varsayar MVC uygulamaları için HTTP isteklerini hello biçimi: `VERB controller/action`.</span><span class="sxs-lookup"><span data-stu-id="b3718-192">Application Insights assumes hello format of HTTP requests for MVC applications is: `VERB controller/action`.</span></span> <span data-ttu-id="b3718-193">Örneğin, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` ve `GET Home/Product/sdf96vws`; `GET Home/Product` içinde gruplandırılır.</span><span class="sxs-lookup"><span data-stu-id="b3718-193">For example, `GET Home/Product/f9anuh81`, `GET Home/Product/2dffwrf5` and `GET Home/Product/sdf96vws` are grouped into `GET Home/Product`.</span></span> <span data-ttu-id="b3718-194">Bu gruplandırma, istek sayısı veya isteklerin yürütülme süresi gibi anlamlı istek toplamalarını etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="b3718-194">This grouping enables meaningful aggregations of requests, such as number of requests and average execution time for requests.</span></span>
>
>

### <a name="instance-data"></a><span data-ttu-id="b3718-195">Örnek veriler</span><span class="sxs-lookup"><span data-stu-id="b3718-195">Instance data</span></span>
<span data-ttu-id="b3718-196">Belirli bir istek geçişli tıklatma toosee tek tek örneklerini yazın.</span><span class="sxs-lookup"><span data-stu-id="b3718-196">Click through a specific request type toosee individual instances.</span></span>

<span data-ttu-id="b3718-197">Application Insights’ta iki tür veri görüntülenir: ortalama, sayım ve toplam olarak depolanan birleşik veriler; HTTP isteklerinin tek tek raporu, özel durumlar, sayfa görünümleri veya özel olaylar olarak görüntülenen örnek veriler.</span><span class="sxs-lookup"><span data-stu-id="b3718-197">Two kinds of data are displayed in Application Insights: aggregated data, stored and displayed as averages, counts, and sums; and instance data - individual reports of HTTP requests, exceptions, page views, or custom events.</span></span>

<span data-ttu-id="b3718-198">İstek Hello özellikleri görüntülendiğinde, istekler ve özel durumlar gibi ilişkili hello telemetri olayları görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3718-198">When viewing hello properties of a request, you can see hello telemetry events associated with it such as requests and exceptions.</span></span>

![](./media/app-insights-java-get-started/7-instance.png)

### <a name="analytics-powerful-query-language"></a><span data-ttu-id="b3718-199">Analiz: Güçlü sorgu dili</span><span class="sxs-lookup"><span data-stu-id="b3718-199">Analytics: Powerful query language</span></span>
<span data-ttu-id="b3718-200">Daha fazla veri birleştirdiğinizde hem tooaggregate veri ve toofind ayrı ayrı örnekleri sorguları çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3718-200">As you accumulate more data, you can run queries both tooaggregate data and toofind individual instances.</span></span>  <span data-ttu-id="b3718-201">[Analiz](app-insights-analytics.md) hem performans, hem de kullanım için olmasının yanı sıra tanılama için de güçlü bir araçtır.</span><span class="sxs-lookup"><span data-stu-id="b3718-201">[Analytics](app-insights-analytics.md) is a powerful tool for both for understanding performance and usage, and for diagnostic purposes.</span></span>

![Analizi örneği](./media/app-insights-java-get-started/025.png)

## <a name="7-install-your-app-on-hello-server"></a><span data-ttu-id="b3718-203">7. Uygulamanızı hello sunucusuna yükleyin</span><span class="sxs-lookup"><span data-stu-id="b3718-203">7. Install your app on hello server</span></span>
<span data-ttu-id="b3718-204">Artık uygulama toohello sunucunuza yayımlayın, kullanmak ve hello portalda hello telemetri izleyin, kullanıcıların izin verir.</span><span class="sxs-lookup"><span data-stu-id="b3718-204">Now publish your app toohello server, let people use it, and watch hello telemetry show up on hello portal.</span></span>

* <span data-ttu-id="b3718-205">Güvenlik duvarınızın, uygulama toosend telemetri toothese bağlantı noktaları verdiğinden emin olun:</span><span class="sxs-lookup"><span data-stu-id="b3718-205">Make sure your firewall allows your application toosend telemetry toothese ports:</span></span>

  * <span data-ttu-id="b3718-206">dc.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="b3718-206">dc.services.visualstudio.com:443</span></span>
  * <span data-ttu-id="b3718-207">f5.services.visualstudio.com:443</span><span class="sxs-lookup"><span data-stu-id="b3718-207">f5.services.visualstudio.com:443</span></span>

* <span data-ttu-id="b3718-208">Giden trafiğin güvenlik duvarından geçirilmesi gerekiyorsa, `http.proxyHost` ve `http.proxyPort` sistem özelliklerini tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="b3718-208">If outgoing traffic must be routed through a firewall, define system properties `http.proxyHost` and `http.proxyPort`.</span></span>

* <span data-ttu-id="b3718-209">Windows sunucularda yüklenecekler:</span><span class="sxs-lookup"><span data-stu-id="b3718-209">On Windows servers, install:</span></span>

  * [<span data-ttu-id="b3718-210">Microsoft Visual C++ Yeniden Dağıtılabilir</span><span class="sxs-lookup"><span data-stu-id="b3718-210">Microsoft Visual C++ Redistributable</span></span>](http://www.microsoft.com/download/details.aspx?id=40784)

    <span data-ttu-id="b3718-211">(Bu bileşen, performans sayaçlarını etkinleştirir.)</span><span class="sxs-lookup"><span data-stu-id="b3718-211">(This component enables performance counters.)</span></span>


## <a name="exceptions-and-request-failures"></a><span data-ttu-id="b3718-212">Özel durumlar ve istek hataları</span><span class="sxs-lookup"><span data-stu-id="b3718-212">Exceptions and request failures</span></span>
<span data-ttu-id="b3718-213">İşlenmeyen özel durumlar otomatik olarak toplanır:</span><span class="sxs-lookup"><span data-stu-id="b3718-213">Unhandled exceptions are automatically collected:</span></span>

![Ayarlar, Hatalar’ı açın](./media/app-insights-java-get-started/21-exceptions.png)

<span data-ttu-id="b3718-215">diğer özel durumlar toocollect verileri, iki seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="b3718-215">toocollect data on other exceptions, you have two options:</span></span>

* <span data-ttu-id="b3718-216">[INSERT çağırır tootrackException() kodunuzda][apiexceptions].</span><span class="sxs-lookup"><span data-stu-id="b3718-216">[Insert calls tootrackException() in your code][apiexceptions].</span></span>
* <span data-ttu-id="b3718-217">[Sunucunuza Hello Java Agent Yükleme](app-insights-java-agent.md).</span><span class="sxs-lookup"><span data-stu-id="b3718-217">[Install hello Java Agent on your server](app-insights-java-agent.md).</span></span> <span data-ttu-id="b3718-218">Toowatch istediğiniz hello yöntemleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="b3718-218">You specify hello methods you want toowatch.</span></span>

## <a name="monitor-method-calls-and-external-dependencies"></a><span data-ttu-id="b3718-219">Yöntem çağrılarını ve dış bağımlılıkları izleme</span><span class="sxs-lookup"><span data-stu-id="b3718-219">Monitor method calls and external dependencies</span></span>
<span data-ttu-id="b3718-220">[Merhaba Java Agent Yükleme](app-insights-java-agent.md) toolog belirtilen dahili yöntemleri ve zamanlama verileriyle JDBC yapılan çağrıları.</span><span class="sxs-lookup"><span data-stu-id="b3718-220">[Install hello Java Agent](app-insights-java-agent.md) toolog specified internal methods and calls made through JDBC, with timing data.</span></span>

## <a name="performance-counters"></a><span data-ttu-id="b3718-221">Performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="b3718-221">Performance counters</span></span>
<span data-ttu-id="b3718-222">Açık **ayarları**, **sunucuları**, toosee bir dizi performans sayacı.</span><span class="sxs-lookup"><span data-stu-id="b3718-222">Open **Settings**, **Servers**, toosee a range of performance counters.</span></span>

![](./media/app-insights-java-get-started/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a><span data-ttu-id="b3718-223">Performans sayacı koleksiyonunu özelleştirme</span><span class="sxs-lookup"><span data-stu-id="b3718-223">Customize performance counter collection</span></span>
<span data-ttu-id="b3718-224">performans sayaçları, standart kümesi hello toodisable koleksiyonu hello hello Applicationınsights.XML dosyasının kök düğümü altında koddan hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b3718-224">toodisable collection of hello standard set of performance counters, add hello following code under hello root node of hello ApplicationInsights.xml file:</span></span>

```XML
    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a><span data-ttu-id="b3718-225">Ek performans sayaçlarını toplama</span><span class="sxs-lookup"><span data-stu-id="b3718-225">Collect additional performance counters</span></span>
<span data-ttu-id="b3718-226">Ek performans sayaçları toobe toplanan belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3718-226">You can specify additional performance counters toobe collected.</span></span>

#### <a name="jmx-counters-exposed-by-hello-java-virtual-machine"></a><span data-ttu-id="b3718-227">JMX sayaçları (Java sanal makinesi hello tarafından gösterilen)</span><span class="sxs-lookup"><span data-stu-id="b3718-227">JMX counters (exposed by hello Java Virtual Machine)</span></span>

```XML
    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* <span data-ttu-id="b3718-228">`displayName`– hello Application Insights portalında görüntülenen hello adı.</span><span class="sxs-lookup"><span data-stu-id="b3718-228">`displayName` – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="b3718-229">`objectName`– hello JMX nesne adı.</span><span class="sxs-lookup"><span data-stu-id="b3718-229">`objectName` – hello JMX object name.</span></span>
* <span data-ttu-id="b3718-230">`attribute`– hello JMX nesne adı toofetch hello özniteliği</span><span class="sxs-lookup"><span data-stu-id="b3718-230">`attribute` – hello attribute of hello JMX object name toofetch</span></span>
* <span data-ttu-id="b3718-231">`type`(isteğe bağlı) - JMX nesnenin öznitelik türü hello:</span><span class="sxs-lookup"><span data-stu-id="b3718-231">`type` (optional) - hello type of JMX object’s attribute:</span></span>
  * <span data-ttu-id="b3718-232">Varsayılan: int veya long gibi basit bir tür.</span><span class="sxs-lookup"><span data-stu-id="b3718-232">Default: a simple type such as int or long.</span></span>
  * <span data-ttu-id="b3718-233">`composite`: hello performans sayacı verileri 'Attribute.Data' hello biçiminde değil</span><span class="sxs-lookup"><span data-stu-id="b3718-233">`composite`: hello perf counter data is in hello format of 'Attribute.Data'</span></span>
  * <span data-ttu-id="b3718-234">`tabular`: hello performans sayacı verileri tablo satırı hello biçiminde değil</span><span class="sxs-lookup"><span data-stu-id="b3718-234">`tabular`: hello perf counter data is in hello format of a table row</span></span>

#### <a name="windows-performance-counters"></a><span data-ttu-id="b3718-235">Windows performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="b3718-235">Windows performance counters</span></span>
<span data-ttu-id="b3718-236">Her [Windows performans sayacı](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) bir kategorinin üyesidir (Merhaba, bir alanın bir sınıf üyesi olduğunu aynı şekilde).</span><span class="sxs-lookup"><span data-stu-id="b3718-236">Each [Windows performance counter](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx) is a member of a category (in hello same way that a field is a member of a class).</span></span> <span data-ttu-id="b3718-237">Kategoriler genel olabileceği gibi numaralı veya adlı örneklere de sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="b3718-237">Categories can either be global, or can have numbered or named instances.</span></span>

```XML
    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* <span data-ttu-id="b3718-238">displayName – hello Application Insights portalında görüntülenen hello adı.</span><span class="sxs-lookup"><span data-stu-id="b3718-238">displayName – hello name displayed in hello Application Insights portal.</span></span>
* <span data-ttu-id="b3718-239">categoryName – bu performans sayacı ilişkilendirildiği hello performans sayacı kategorisi (performans nesnesi).</span><span class="sxs-lookup"><span data-stu-id="b3718-239">categoryName – hello performance counter category (performance object) with which this performance counter is associated.</span></span>
* <span data-ttu-id="b3718-240">counterName – hello hello performans sayacının adını.</span><span class="sxs-lookup"><span data-stu-id="b3718-240">counterName – hello name of hello performance counter.</span></span>
* <span data-ttu-id="b3718-241">instanceName – hello hello performans sayacı kategorisi örneğinin adını ya da boş bir dize (""), tek bir örnek hello kategorisi içerir.</span><span class="sxs-lookup"><span data-stu-id="b3718-241">instanceName – hello name of hello performance counter category instance, or an empty string (""), if hello category contains a single instance.</span></span> <span data-ttu-id="b3718-242">Merhaba categoryName işlem toocollect istediğinizi hello performans sayacı olduğundan hello geçerli JVM işleminden ise, uygulamanızı çalıştıran, belirtin `"__SELF__"`.</span><span class="sxs-lookup"><span data-stu-id="b3718-242">If hello categoryName is Process, and hello performance counter you'd like toocollect is from hello current JVM process on which your app is running, specify `"__SELF__"`.</span></span>

<span data-ttu-id="b3718-243">Özel ölçümleriniz [Ölçüm Gezgini][metrics]'nde olduğundan performans sayaçlarınız görünürdür.</span><span class="sxs-lookup"><span data-stu-id="b3718-243">Your performance counters are visible as custom metrics in [Metrics Explorer][metrics].</span></span>

![](./media/app-insights-java-get-started/12-custom-perfs.png)

### <a name="unix-performance-counters"></a><span data-ttu-id="b3718-244">Unix Performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="b3718-244">Unix performance counters</span></span>
* <span data-ttu-id="b3718-245">[Merhaba Application Insights eklentisiyle collectd yükleyin](app-insights-java-collectd.md) tooget çok çeşitli sistem ve ağ verileri.</span><span class="sxs-lookup"><span data-stu-id="b3718-245">[Install collectd with hello Application Insights plugin](app-insights-java-collectd.md) tooget a wide variety of system and network data.</span></span>

## <a name="get-user-and-session-data"></a><span data-ttu-id="b3718-246">Kullanıcı ve oturum verilerini alma</span><span class="sxs-lookup"><span data-stu-id="b3718-246">Get user and session data</span></span>
<span data-ttu-id="b3718-247">Tamam, web sunucunuzdan telemetri gönderiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="b3718-247">OK, you're sending telemetry from your web server.</span></span> <span data-ttu-id="b3718-248">Şimdi tooget Merhaba, uygulamanızın 360 derecelik tam görünümünü daha izleme ekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="b3718-248">Now tooget hello full 360-degree view of your application, you can add more monitoring:</span></span>

* <span data-ttu-id="b3718-249">[Telemetri tooyour web sayfaları eklemek] [ usage] toomonitor sayfa görünümlerini ve kullanıcı ölçümlerini.</span><span class="sxs-lookup"><span data-stu-id="b3718-249">[Add telemetry tooyour web pages][usage] toomonitor page views and user metrics.</span></span>
* <span data-ttu-id="b3718-250">[Web testleri oluşturma] [ availability] toomake uygulamanızın canlı ve duyarlı kaldığından emin.</span><span class="sxs-lookup"><span data-stu-id="b3718-250">[Set up web tests][availability] toomake sure your application stays live and responsive.</span></span>

## <a name="capture-log-traces"></a><span data-ttu-id="b3718-251">Günlük izlemelerini yakalama</span><span class="sxs-lookup"><span data-stu-id="b3718-251">Capture log traces</span></span>
<span data-ttu-id="b3718-252">Log4J, Logback veya başka günlük altyapılarına günlüklerinden inin ve Application Insights tooslice kullanın.</span><span class="sxs-lookup"><span data-stu-id="b3718-252">You can use Application Insights tooslice and dice logs from Log4J, Logback, or other logging frameworks.</span></span> <span data-ttu-id="b3718-253">Merhaba günlükleri HTTP istekleri ve başka telemetriyle ilişkilendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3718-253">You can correlate hello logs with HTTP requests and other telemetry.</span></span> <span data-ttu-id="b3718-254">[Nasıl olduğunu öğrenin][javalogs].</span><span class="sxs-lookup"><span data-stu-id="b3718-254">[Learn how][javalogs].</span></span>

## <a name="send-your-own-telemetry"></a><span data-ttu-id="b3718-255">Kendi telemetrinizi gönderme</span><span class="sxs-lookup"><span data-stu-id="b3718-255">Send your own telemetry</span></span>
<span data-ttu-id="b3718-256">Merhaba SDK yüklediniz, kendi telemetrinizi hello API toosend kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3718-256">Now that you've installed hello SDK, you can use hello API toosend your own telemetry.</span></span>

* <span data-ttu-id="b3718-257">[Özel olayları ve ölçümleri izleme] [ api] hangi kullanıcıların uygulamanızla yaptıkları toolearn.</span><span class="sxs-lookup"><span data-stu-id="b3718-257">[Track custom events and metrics][api] toolearn what users are doing with your application.</span></span>
* <span data-ttu-id="b3718-258">[Olayları ve günlükleri arayın] [ diagnostic] toohelp sorunları tanılayın.</span><span class="sxs-lookup"><span data-stu-id="b3718-258">[Search events and logs][diagnostic] toohelp diagnose problems.</span></span>

## <a name="availability-web-tests"></a><span data-ttu-id="b3718-259">Kullanılabilirlik web testleri</span><span class="sxs-lookup"><span data-stu-id="b3718-259">Availability web tests</span></span>
<span data-ttu-id="b3718-260">Application Insights olan yukarı düzenli aralıklarla toocheck ve düzgün yanıt Web sitenizi test edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b3718-260">Application Insights can test your website at regular intervals toocheck that it's up and responding well.</span></span> <span data-ttu-id="b3718-261">[Yukarı tooset][availability], Web testleri'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="b3718-261">[tooset up][availability], click Web tests.</span></span>

![Web testleri’ne ve ardından Web testi ekle’ye tıklayın](./media/app-insights-java-get-started/31-config-web-test.png)

<span data-ttu-id="b3718-263">Yanıt süreleri grafiklerine ek olarak, siteniz devre dışı kalırsa e-posta bildirimleri de alacaksınız.</span><span class="sxs-lookup"><span data-stu-id="b3718-263">You'll get charts of response times, plus email notifications if your site goes down.</span></span>

![Web testi örneği](./media/app-insights-java-get-started/appinsights-10webtestresult.png)

<span data-ttu-id="b3718-265">[Kullanılabilirlik web testleri hakkında daha fazla bilgi edinin.][availability]</span><span class="sxs-lookup"><span data-stu-id="b3718-265">[Learn more about availability web tests.][availability]</span></span>

## <a name="questions-problems"></a><span data-ttu-id="b3718-266">Sorularınız mı var?</span><span class="sxs-lookup"><span data-stu-id="b3718-266">Questions?</span></span> <span data-ttu-id="b3718-267">Sorunlarınız mı var?</span><span class="sxs-lookup"><span data-stu-id="b3718-267">Problems?</span></span>
[<span data-ttu-id="b3718-268">Java Sorun Giderme</span><span class="sxs-lookup"><span data-stu-id="b3718-268">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

## <a name="video"></a><span data-ttu-id="b3718-269">Video</span><span class="sxs-lookup"><span data-stu-id="b3718-269">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a><span data-ttu-id="b3718-270">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b3718-270">Next steps</span></span>
* [<span data-ttu-id="b3718-271">Bağımlılık çağrılarını izleme</span><span class="sxs-lookup"><span data-stu-id="b3718-271">Monitor dependency calls</span></span>](app-insights-java-agent.md)
* [<span data-ttu-id="b3718-272">Unix Performans sayaçlarını izleme</span><span class="sxs-lookup"><span data-stu-id="b3718-272">Monitor Unix performance counters</span></span>](app-insights-java-collectd.md)
* <span data-ttu-id="b3718-273">Ekleme [tooyour web sayfalarını izleme](app-insights-javascript.md) toomonitor sayfa yükleme süresi, AJAX çağrıları, tarayıcı özel durumları.</span><span class="sxs-lookup"><span data-stu-id="b3718-273">Add [monitoring tooyour web pages](app-insights-javascript.md) toomonitor page load times, AJAX calls, browser exceptions.</span></span>
* <span data-ttu-id="b3718-274">Yazma [özel telemetri](app-insights-api-custom-events-metrics.md) tootrack kullanım hello tarayıcıda veya hello sunucusu.</span><span class="sxs-lookup"><span data-stu-id="b3718-274">Write [custom telemetry](app-insights-api-custom-events-metrics.md) tootrack usage in hello browser or at hello server.</span></span>
* <span data-ttu-id="b3718-275">Oluşturma [panolar](app-insights-dashboards.md) sisteminizi izleme toobring birlikte hello anahtar grafikleri.</span><span class="sxs-lookup"><span data-stu-id="b3718-275">Create [dashboards](app-insights-dashboards.md) toobring together hello key charts for monitoring your system.</span></span>
* <span data-ttu-id="b3718-276">Uygulamanızdan telemetri üzerinde güçlü sorgular yapmak için [Analytics](app-insights-analytics.md)'i kullanın</span><span class="sxs-lookup"><span data-stu-id="b3718-276">Use  [Analytics](app-insights-analytics.md) for powerful queries over telemetry from your app</span></span>
* <span data-ttu-id="b3718-277">Daha fazla bilgi için bkz. [Java geliştiricileri için Azure](/java/azure).</span><span class="sxs-lookup"><span data-stu-id="b3718-277">For more information, visit [Azure for Java developers](/java/azure).</span></span>

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#trackexception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[usage]: app-insights-javascript.md
