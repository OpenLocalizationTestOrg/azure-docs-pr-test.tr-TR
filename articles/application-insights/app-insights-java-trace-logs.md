---
title: "Azure Application Insights'ta aaaExplore Java izleme günlükleri | Microsoft Docs"
description: Application Insights arama Log4J veya Logback izlemeleri
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: fc0a9e2f-3beb-4f47-a9fe-3f86cd29d97a
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/12/2016
ms.author: bwren
ms.openlocfilehash: e5f8e8c67e57753ba7574b97aa96dbb41db00ce1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-java-trace-logs-in-application-insights"></a><span data-ttu-id="7dfab-103">Application Insights izleme günlüklerini Java keşfedin</span><span class="sxs-lookup"><span data-stu-id="7dfab-103">Explore Java trace logs in Application Insights</span></span>
<span data-ttu-id="7dfab-104">Logback veya Log4J kullanıyorsanız (1.2 sürümü veya v2.0) izleme için otomatik olarak tooApplication burada keşfedin ve bunlar üzerinde arama Öngörüler gönderilen, izleme günlükleri sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="7dfab-104">If you're using Logback or Log4J (v1.2 or v2.0) for tracing, you can have your trace logs sent automatically tooApplication Insights where you can explore and search on them.</span></span>

## <a name="install-hello-java-sdk"></a><span data-ttu-id="7dfab-105">Merhaba Java SDK'sını yükleyin</span><span class="sxs-lookup"><span data-stu-id="7dfab-105">Install hello Java SDK</span></span>

<span data-ttu-id="7dfab-106">Yükleme [Java için Application Insights SDK][java], size, bu işlemi yapmadıysanız.</span><span class="sxs-lookup"><span data-stu-id="7dfab-106">Install [Application Insights SDK for Java][java], if you haven't already done that.</span></span>

<span data-ttu-id="7dfab-107">(Tootrack HTTP isteklerini istemiyorsanız, hello .xml yapılandırma dosyası çoğunu atlayabilirsiniz, ancak en az hello içermelidir `InstrumentationKey` öğesi.</span><span class="sxs-lookup"><span data-stu-id="7dfab-107">(If you don't want tootrack HTTP requests, you can omit most of hello .xml configuration file, but you must at least include hello `InstrumentationKey` element.</span></span> <span data-ttu-id="7dfab-108">Ayrıca çağırmalıdır `new TelemetryClient()` tooinitialize hello SDK.)</span><span class="sxs-lookup"><span data-stu-id="7dfab-108">You should also call `new TelemetryClient()` tooinitialize hello SDK.)</span></span>


## <a name="add-logging-libraries-tooyour-project"></a><span data-ttu-id="7dfab-109">Günlüğe kaydetme kitaplıkları tooyour proje ekleyin</span><span class="sxs-lookup"><span data-stu-id="7dfab-109">Add logging libraries tooyour project</span></span>
<span data-ttu-id="7dfab-110">*Projeniz için uygun şekilde Hello seçin.*</span><span class="sxs-lookup"><span data-stu-id="7dfab-110">*Choose hello appropriate way for your project.*</span></span>

#### <a name="if-youre-using-maven"></a><span data-ttu-id="7dfab-111">Maven kullanıyorsanız...</span><span class="sxs-lookup"><span data-stu-id="7dfab-111">If you're using Maven...</span></span>
<span data-ttu-id="7dfab-112">Projeniz zaten toouse Maven derleme için ayarladıysanız, kod parçacıkları pom.xml dosyanıza aşağıdaki hello birini birleştirin.</span><span class="sxs-lookup"><span data-stu-id="7dfab-112">If your project is already set up toouse Maven for build, merge one of hello following snippets of code into your pom.xml file.</span></span>

<span data-ttu-id="7dfab-113">Ardından hello proje bağımlılıklarını, indirilen tooget hello ikili yenileyin.</span><span class="sxs-lookup"><span data-stu-id="7dfab-113">Then refresh hello project dependencies, tooget hello binaries downloaded.</span></span>

<span data-ttu-id="7dfab-114">*Logback*</span><span class="sxs-lookup"><span data-stu-id="7dfab-114">*Logback*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-logback</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="7dfab-115">*Log4J v2.0*</span><span class="sxs-lookup"><span data-stu-id="7dfab-115">*Log4J v2.0*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

<span data-ttu-id="7dfab-116">*Log4J 1.2 sürümü*</span><span class="sxs-lookup"><span data-stu-id="7dfab-116">*Log4J v1.2*</span></span>

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j1_2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

#### <a name="if-youre-using-gradle"></a><span data-ttu-id="7dfab-117">Gradle kullanıyorsanız...</span><span class="sxs-lookup"><span data-stu-id="7dfab-117">If you're using Gradle...</span></span>
<span data-ttu-id="7dfab-118">Projeniz zaten toouse Gradle derleme için ayarladıysanız, aşağıdaki satırları toohello hello birini ekleyin `dependencies` build.gradle dosyanızla grubu:</span><span class="sxs-lookup"><span data-stu-id="7dfab-118">If your project is already set up toouse Gradle for build, add one of hello following lines toohello `dependencies` group in your build.gradle file:</span></span>

<span data-ttu-id="7dfab-119">Ardından hello proje bağımlılıklarını, indirilen tooget hello ikili yenileyin.</span><span class="sxs-lookup"><span data-stu-id="7dfab-119">Then refresh hello project dependencies, tooget hello binaries downloaded.</span></span>

<span data-ttu-id="7dfab-120">**Logback**</span><span class="sxs-lookup"><span data-stu-id="7dfab-120">**Logback**</span></span>

```

    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-logback', version: '1.0.+'
```

<span data-ttu-id="7dfab-121">**Log4J v2.0**</span><span class="sxs-lookup"><span data-stu-id="7dfab-121">**Log4J v2.0**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j2', version: '1.0.+'
```

<span data-ttu-id="7dfab-122">**Log4J 1.2 sürümü**</span><span class="sxs-lookup"><span data-stu-id="7dfab-122">**Log4J v1.2**</span></span>

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j1_2', version: '1.0.+'
```

#### <a name="otherwise-"></a><span data-ttu-id="7dfab-123">Aksi taktirde...</span><span class="sxs-lookup"><span data-stu-id="7dfab-123">Otherwise ...</span></span>
<span data-ttu-id="7dfab-124">Karşıdan yükleyin ve hello uygun appender ayıklayın ve sonra hello uygun kitaplığı tooyour projesini ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7dfab-124">Download and extract hello appropriate appender, then add hello appropriate library tooyour project:</span></span>

| <span data-ttu-id="7dfab-125">Günlükçü</span><span class="sxs-lookup"><span data-stu-id="7dfab-125">Logger</span></span> | <span data-ttu-id="7dfab-126">İndir</span><span class="sxs-lookup"><span data-stu-id="7dfab-126">Download</span></span> | <span data-ttu-id="7dfab-127">Kitaplık</span><span class="sxs-lookup"><span data-stu-id="7dfab-127">Library</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7dfab-128">Logback</span><span class="sxs-lookup"><span data-stu-id="7dfab-128">Logback</span></span> |[<span data-ttu-id="7dfab-129">SDK Logback appender ile</span><span class="sxs-lookup"><span data-stu-id="7dfab-129">SDK with Logback appender</span></span>](https://aka.ms/xt62a4) |<span data-ttu-id="7dfab-130">applicationınsights günlük logback</span><span class="sxs-lookup"><span data-stu-id="7dfab-130">applicationinsights-logging-logback</span></span> |
| <span data-ttu-id="7dfab-131">Log4J v2.0</span><span class="sxs-lookup"><span data-stu-id="7dfab-131">Log4J v2.0</span></span> |[<span data-ttu-id="7dfab-132">Log4J v2 appender SDK'sı</span><span class="sxs-lookup"><span data-stu-id="7dfab-132">SDK with Log4J v2 appender</span></span>](https://aka.ms/qypznq) |<span data-ttu-id="7dfab-133">applicationınsights günlük log4j2</span><span class="sxs-lookup"><span data-stu-id="7dfab-133">applicationinsights-logging-log4j2</span></span> |
| <span data-ttu-id="7dfab-134">Log4j 1.2 sürümü</span><span class="sxs-lookup"><span data-stu-id="7dfab-134">Log4j v1.2</span></span> |[<span data-ttu-id="7dfab-135">Log4J 1.2 sürümü appender SDK'sı</span><span class="sxs-lookup"><span data-stu-id="7dfab-135">SDK with Log4J v1.2 appender</span></span>](https://aka.ms/ky9cbo) |<span data-ttu-id="7dfab-136">applicationınsights günlük log4j1_2</span><span class="sxs-lookup"><span data-stu-id="7dfab-136">applicationinsights-logging-log4j1_2</span></span> |

## <a name="add-hello-appender-tooyour-logging-framework"></a><span data-ttu-id="7dfab-137">Merhaba appender tooyour günlüğü framework ekleme</span><span class="sxs-lookup"><span data-stu-id="7dfab-137">Add hello appender tooyour logging framework</span></span>
<span data-ttu-id="7dfab-138">Başlarken izlemeleri, birleştirme hello ilgili parçacığını kod toohello Log4J veya Logback yapılandırma dosyası toostart:</span><span class="sxs-lookup"><span data-stu-id="7dfab-138">toostart getting traces, merge hello relevant snippet of code toohello Log4J or Logback configuration file:</span></span> 

<span data-ttu-id="7dfab-139">*Logback*</span><span class="sxs-lookup"><span data-stu-id="7dfab-139">*Logback*</span></span>

```XML

    <appender name="aiAppender" 
      class="com.microsoft.applicationinsights.logback.ApplicationInsightsAppender">
    </appender>
    <root level="trace">
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="7dfab-140">*Log4J v2.0*</span><span class="sxs-lookup"><span data-stu-id="7dfab-140">*Log4J v2.0*</span></span>

```XML

    <Configuration packages="com.microsoft.applicationinsights.Log4j">
      <Appenders>
        <ApplicationInsightsAppender name="aiAppender" />
      </Appenders>
      <Loggers>
        <Root level="trace">
          <AppenderRef ref="aiAppender"/>
        </Root>
      </Loggers>
    </Configuration>
```

<span data-ttu-id="7dfab-141">*Log4J 1.2 sürümü*</span><span class="sxs-lookup"><span data-stu-id="7dfab-141">*Log4J v1.2*</span></span>

```XML

    <appender name="aiAppender" 
         class="com.microsoft.applicationinsights.log4j.v1_2.ApplicationInsightsAppender">
    </appender>
    <root>
      <priority value ="trace" />
      <appender-ref ref="aiAppender" />
    </root>
```

<span data-ttu-id="7dfab-142">Merhaba Application Insights appenders (Merhaba kod örnekleri yukarıda gösterildiği gibi) yapılandırılmış tüm Günlükçü ve mutlaka hello kök Günlükçü tarafından başvurulabilir.</span><span class="sxs-lookup"><span data-stu-id="7dfab-142">hello Application Insights appenders can be referenced by any configured logger, and not necessarily by hello root logger (as shown in hello code samples above).</span></span>

## <a name="explore-your-traces-in-hello-application-insights-portal"></a><span data-ttu-id="7dfab-143">Merhaba Application Insights portalında, izlemeleri keşfedin</span><span class="sxs-lookup"><span data-stu-id="7dfab-143">Explore your traces in hello Application Insights portal</span></span>
<span data-ttu-id="7dfab-144">Yapılandırdığınız göre proje toosend tooApplication Öngörüler izler, görüntüleyin ve bu izlemelerin hello de hello Application Insights portalında arama [arama] [ diagnostic] dikey.</span><span class="sxs-lookup"><span data-stu-id="7dfab-144">Now that you've configured your project toosend traces tooApplication Insights, you can view and search these traces in hello Application Insights portal, in hello [Search][diagnostic] blade.</span></span>

![Arama Hello Application Insights portalında açın](./media/app-insights-java-trace-logs/10-diagnostics.png)

## <a name="next-steps"></a><span data-ttu-id="7dfab-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7dfab-146">Next steps</span></span>
<span data-ttu-id="7dfab-147">[Tanılama arama][diagnostic]</span><span class="sxs-lookup"><span data-stu-id="7dfab-147">[Diagnostic search][diagnostic]</span></span>

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md


