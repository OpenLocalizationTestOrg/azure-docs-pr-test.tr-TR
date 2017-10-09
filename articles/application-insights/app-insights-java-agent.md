---
title: "Azure Application Insights Java web uygulamalarının aaaPerformance izleme | Microsoft Docs"
description: "Genişletilmiş performans ve Application Insights ile Java Web sitenizin kullanım izleme."
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 84017a48-1cb3-40c8-aab1-ff68d65e2128
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: bwren
ms.openlocfilehash: bf3983e3b4a16e72bc606b6468a757288d05ebaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-dependencies-exceptions-and-execution-times-in-java-web-apps"></a><span data-ttu-id="9c8ee-103">Bağımlılıklar, özel durumlar ve yürütme sürelerini Java web uygulamalarını izleme</span><span class="sxs-lookup"><span data-stu-id="9c8ee-103">Monitor dependencies, exceptions and execution times in Java web apps</span></span>


<span data-ttu-id="9c8ee-104">Varsa [Java web uygulamanıza Application Insights ile işaretlenir][java], hello Java Agent tooget daha ayrıntılı Öngörüler, kod değişiklikleri olmadan kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9c8ee-104">If you have [instrumented your Java web app with Application Insights][java], you can use hello Java Agent tooget deeper insights, without any code changes:</span></span>

* <span data-ttu-id="9c8ee-105">**Bağımlılıklar:** tooother bileşenleri de dahil olmak üzere, uygulamanızın yaptığı çağrıları hakkında veriler:</span><span class="sxs-lookup"><span data-stu-id="9c8ee-105">**Dependencies:** Data about calls that your application makes tooother components, including:</span></span>
  * <span data-ttu-id="9c8ee-106">**REST çağrılarını** HttpClient, OkHttp ve RestTemplate (yay) yapılır.</span><span class="sxs-lookup"><span data-stu-id="9c8ee-106">**REST calls** made via HttpClient, OkHttp, and RestTemplate (Spring).</span></span>
  * <span data-ttu-id="9c8ee-107">**Redis** hello Jedis istemci yapılan çağrıları.</span><span class="sxs-lookup"><span data-stu-id="9c8ee-107">**Redis** calls made via hello Jedis client.</span></span> <span data-ttu-id="9c8ee-108">Merhaba çağrısı 10'luk uzun sürerse, hello aracı ayrıca hello çağrı bağımsız getirir.</span><span class="sxs-lookup"><span data-stu-id="9c8ee-108">If hello call takes longer than 10s, hello agent also fetches hello call arguments.</span></span>
  * <span data-ttu-id="9c8ee-109">**[JDBC çağrıları](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)**  -MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB veya Apache Derby DB.</span><span class="sxs-lookup"><span data-stu-id="9c8ee-109">**[JDBC calls](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** - MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB or Apache Derby DB.</span></span> <span data-ttu-id="9c8ee-110">"executeBatch" çağrıları desteklenir.</span><span class="sxs-lookup"><span data-stu-id="9c8ee-110">"executeBatch" calls are supported.</span></span> <span data-ttu-id="9c8ee-111">Merhaba çağrısı 10'luk uzun sürerse, MySQL ve PostgreSQL için hello Aracısı hello sorgu planı bildirir.</span><span class="sxs-lookup"><span data-stu-id="9c8ee-111">For MySQL and PostgreSQL, if hello call takes longer than 10s, hello agent reports hello query plan.</span></span>
* <span data-ttu-id="9c8ee-112">**Özel durum yakalandı:** kodunuz tarafından işlenen özel durumlar hakkında veri.</span><span class="sxs-lookup"><span data-stu-id="9c8ee-112">**Caught exceptions:** Data about exceptions that are handled by your code.</span></span>
* <span data-ttu-id="9c8ee-113">**Yöntem yürütme süresi:** hello hakkındaki verileri alır tooexecute belirli yöntemler seferlik.</span><span class="sxs-lookup"><span data-stu-id="9c8ee-113">**Method execution time:** Data about hello time it takes tooexecute specific methods.</span></span>

<span data-ttu-id="9c8ee-114">toouse hello Java agent, sunucunuza yükleyin.</span><span class="sxs-lookup"><span data-stu-id="9c8ee-114">toouse hello Java agent, you install it on your server.</span></span> <span data-ttu-id="9c8ee-115">Web uygulamalarınızı hello ile işaretlenir gerekir [Application Insights Java SDK'sı][java].</span><span class="sxs-lookup"><span data-stu-id="9c8ee-115">Your web apps must be instrumented with hello [Application Insights Java SDK][java].</span></span> 

## <a name="install-hello-application-insights-agent-for-java"></a><span data-ttu-id="9c8ee-116">Java için Application Insights Aracısı Hello yükleyin</span><span class="sxs-lookup"><span data-stu-id="9c8ee-116">Install hello Application Insights agent for Java</span></span>
1. <span data-ttu-id="9c8ee-117">Java sunucunuz Hello makine üzerinde çalışan [hello Aracısı'nı indirme](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="9c8ee-117">On hello machine running your Java server, [download hello agent](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="9c8ee-118">Merhaba uygulama sunucusu başlangıç komut dosyasını düzenleyin ve JVM aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9c8ee-118">Edit hello application server startup script, and add hello following JVM:</span></span>
   
    <span data-ttu-id="9c8ee-119">`javaagent:`*tam yol toohello Aracısı JAR dosyasını*</span><span class="sxs-lookup"><span data-stu-id="9c8ee-119">`javaagent:`*full path toohello agent JAR file*</span></span>
   
    <span data-ttu-id="9c8ee-120">Örneğin, Tomcat'te bir Linux makinesinde:</span><span class="sxs-lookup"><span data-stu-id="9c8ee-120">For example, in Tomcat on a Linux machine:</span></span>
   
    `export JAVA_OPTS="$JAVA_OPTS -javaagent:<full path tooagent JAR file>"`
3. <span data-ttu-id="9c8ee-121">Uygulama sunucunuzu yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="9c8ee-121">Restart your application server.</span></span>

## <a name="configure-hello-agent"></a><span data-ttu-id="9c8ee-122">Merhaba Aracısı'nı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="9c8ee-122">Configure hello agent</span></span>
<span data-ttu-id="9c8ee-123">Adlı bir dosya oluşturun `AI-Agent.xml` ve hello yerleştirin hello Aracısı JAR dosyasını aynı klasöre.</span><span class="sxs-lookup"><span data-stu-id="9c8ee-123">Create a file named `AI-Agent.xml` and place it in hello same folder as hello agent JAR file.</span></span>

<span data-ttu-id="9c8ee-124">Merhaba xml dosyası Merhaba içeriğine ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="9c8ee-124">Set hello content of hello xml file.</span></span> <span data-ttu-id="9c8ee-125">Aşağıdaki örnek tooinclude hello düzenleyin veya hello özellikleri atlayın.</span><span class="sxs-lookup"><span data-stu-id="9c8ee-125">Edit hello following example tooinclude or omit hello features you want.</span></span>

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsightsAgent>
      <Instrumentation>

        <!-- Collect remote dependency data -->
        <BuiltIn enabled="true">
           <!-- Disable Redis or alter threshold call duration above which arguments are sent.
               Defaults: enabled, 10000 ms -->
           <Jedis enabled="true" thresholdInMS="1000"/>

           <!-- Set SQL query duration above which query plan is reported (MySQL, PostgreSQL). Default is 10000 ms. -->
           <MaxStatementQueryLimitInMS>1000</MaxStatementQueryLimitInMS>
        </BuiltIn>

        <!-- Collect data about caught exceptions
             and method execution times -->

        <Class name="com.myCompany.MyClass">
           <Method name="methodOne"
               reportCaughtExceptions="true"
               reportExecutionTime="true"
               />

           <!-- Report on hello particular signature
                void methodTwo(String, int) -->
           <Method name="methodTwo"
              reportExecutionTime="true"
              signature="(Ljava/lang/String;I)V" />
        </Class>

      </Instrumentation>
    </ApplicationInsightsAgent>

```

<span data-ttu-id="9c8ee-126">Tooenable raporları özel durumu ve tek tek yöntemleri için yöntemi zamanlama var.</span><span class="sxs-lookup"><span data-stu-id="9c8ee-126">You have tooenable reports exception and method timing for individual methods.</span></span>

<span data-ttu-id="9c8ee-127">Varsayılan olarak, `reportExecutionTime` geçerlidir ve `reportCaughtExceptions` false olur.</span><span class="sxs-lookup"><span data-stu-id="9c8ee-127">By default, `reportExecutionTime` is true and `reportCaughtExceptions` is false.</span></span>

## <a name="view-hello-data"></a><span data-ttu-id="9c8ee-128">Merhaba verileri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="9c8ee-128">View hello data</span></span>
<span data-ttu-id="9c8ee-129">Hello Application Insights kaynağı, toplanan uzak bağımlılık ve yöntemi yürütme sürelerinin görünür [performans hello altında döşeme][metrics].</span><span class="sxs-lookup"><span data-stu-id="9c8ee-129">In hello Application Insights resource, aggregated remote dependency and method execution times appears [under hello Performance tile][metrics].</span></span>

<span data-ttu-id="9c8ee-130">bağımlılık, özel durum ve yöntemi raporları, tek tek örneklerini toosearch açmak [arama][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="9c8ee-130">toosearch for individual instances of dependency, exception, and method reports, open [Search][diagnostic].</span></span>

<span data-ttu-id="9c8ee-131">[Tanılama bağımlılık sorunları - daha fazla bilgi](app-insights-asp-net-dependencies.md#diagnosis).</span><span class="sxs-lookup"><span data-stu-id="9c8ee-131">[Diagnosing dependency issues - learn more](app-insights-asp-net-dependencies.md#diagnosis).</span></span>

## <a name="questions-problems"></a><span data-ttu-id="9c8ee-132">Sorularınız mı var?</span><span class="sxs-lookup"><span data-stu-id="9c8ee-132">Questions?</span></span> <span data-ttu-id="9c8ee-133">Sorunlarınız mı var?</span><span class="sxs-lookup"><span data-stu-id="9c8ee-133">Problems?</span></span>
* <span data-ttu-id="9c8ee-134">Veri yok mu?</span><span class="sxs-lookup"><span data-stu-id="9c8ee-134">No data?</span></span> [<span data-ttu-id="9c8ee-135">Set güvenlik duvarı özel durumlar</span><span class="sxs-lookup"><span data-stu-id="9c8ee-135">Set firewall exceptions</span></span>](app-insights-ip-addresses.md)
* [<span data-ttu-id="9c8ee-136">Java Sorun Giderme</span><span class="sxs-lookup"><span data-stu-id="9c8ee-136">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
