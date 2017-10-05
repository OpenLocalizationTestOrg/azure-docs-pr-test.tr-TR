---
title: "Azure Application ınsights'ta Java web uygulamaları için performans izleme | Microsoft Docs"
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
ms.openlocfilehash: 4e56998382610ad3d7224e6a8de5aee5419ebe43
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-dependencies-exceptions-and-execution-times-in-java-web-apps"></a><span data-ttu-id="638aa-103">Bağımlılıklar, özel durumlar ve yürütme sürelerini Java web uygulamalarını izleme</span><span class="sxs-lookup"><span data-stu-id="638aa-103">Monitor dependencies, exceptions and execution times in Java web apps</span></span>


<span data-ttu-id="638aa-104">Varsa [Java web uygulamanıza Application Insights ile işaretlenir][java], kod değişiklikleri olmadan daha ayrıntılı Öngörüler almak için Java Agent kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="638aa-104">If you have [instrumented your Java web app with Application Insights][java], you can use the Java Agent to get deeper insights, without any code changes:</span></span>

* <span data-ttu-id="638aa-105">**Bağımlılıklar:** verileri de dahil olmak üzere diğer bileşenler için uygulamanızın yaptığı çağrıları hakkında:</span><span class="sxs-lookup"><span data-stu-id="638aa-105">**Dependencies:** Data about calls that your application makes to other components, including:</span></span>
  * <span data-ttu-id="638aa-106">**REST çağrılarını** HttpClient, OkHttp ve RestTemplate (yay) yapılır.</span><span class="sxs-lookup"><span data-stu-id="638aa-106">**REST calls** made via HttpClient, OkHttp, and RestTemplate (Spring).</span></span>
  * <span data-ttu-id="638aa-107">**Redis** Jedis istemcisi üzerinden yapılan çağrıları.</span><span class="sxs-lookup"><span data-stu-id="638aa-107">**Redis** calls made via the Jedis client.</span></span> <span data-ttu-id="638aa-108">Çağrı 10'luk uzun sürerse, aracı ayrıca çağrı bağımsız getirir.</span><span class="sxs-lookup"><span data-stu-id="638aa-108">If the call takes longer than 10s, the agent also fetches the call arguments.</span></span>
  * <span data-ttu-id="638aa-109">**[JDBC çağrıları](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)**  -MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB veya Apache Derby DB.</span><span class="sxs-lookup"><span data-stu-id="638aa-109">**[JDBC calls](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)** - MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB or Apache Derby DB.</span></span> <span data-ttu-id="638aa-110">"executeBatch" çağrıları desteklenir.</span><span class="sxs-lookup"><span data-stu-id="638aa-110">"executeBatch" calls are supported.</span></span> <span data-ttu-id="638aa-111">Çağrı 10'luk uzun sürerse, MySQL ve PostgreSQL için aracı sorgu planı bildirir.</span><span class="sxs-lookup"><span data-stu-id="638aa-111">For MySQL and PostgreSQL, if the call takes longer than 10s, the agent reports the query plan.</span></span>
* <span data-ttu-id="638aa-112">**Özel durum yakalandı:** kodunuz tarafından işlenen özel durumlar hakkında veri.</span><span class="sxs-lookup"><span data-stu-id="638aa-112">**Caught exceptions:** Data about exceptions that are handled by your code.</span></span>
* <span data-ttu-id="638aa-113">**Yöntem yürütme süresi:** belirli yöntemleri yürütme süresini hakkındaki verileri.</span><span class="sxs-lookup"><span data-stu-id="638aa-113">**Method execution time:** Data about the time it takes to execute specific methods.</span></span>

<span data-ttu-id="638aa-114">Java Aracısı'nı kullanmak için sunucunuzda yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="638aa-114">To use the Java agent, you install it on your server.</span></span> <span data-ttu-id="638aa-115">Web uygulamalarınızı ile işaretlenir gerekir [Application Insights Java SDK'sı][java].</span><span class="sxs-lookup"><span data-stu-id="638aa-115">Your web apps must be instrumented with the [Application Insights Java SDK][java].</span></span> 

## <a name="install-the-application-insights-agent-for-java"></a><span data-ttu-id="638aa-116">Java için Application Insights aracısı yükleyin</span><span class="sxs-lookup"><span data-stu-id="638aa-116">Install the Application Insights agent for Java</span></span>
1. <span data-ttu-id="638aa-117">Java sunucunuz makinede çalışan [Aracısı'nı indirme](https://aka.ms/aijavasdk).</span><span class="sxs-lookup"><span data-stu-id="638aa-117">On the machine running your Java server, [download the agent](https://aka.ms/aijavasdk).</span></span>
2. <span data-ttu-id="638aa-118">Uygulama sunucusu başlangıç komut dosyasını düzenleyin ve aşağıdaki JVM ekleyin:</span><span class="sxs-lookup"><span data-stu-id="638aa-118">Edit the application server startup script, and add the following JVM:</span></span>
   
    <span data-ttu-id="638aa-119">`javaagent:`*Aracı JAR dosyasının tam yolu*</span><span class="sxs-lookup"><span data-stu-id="638aa-119">`javaagent:`*full path to the agent JAR file*</span></span>
   
    <span data-ttu-id="638aa-120">Örneğin, Tomcat'te bir Linux makinesinde:</span><span class="sxs-lookup"><span data-stu-id="638aa-120">For example, in Tomcat on a Linux machine:</span></span>
   
    `export JAVA_OPTS="$JAVA_OPTS -javaagent:<full path to agent JAR file>"`
3. <span data-ttu-id="638aa-121">Uygulama sunucunuzu yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="638aa-121">Restart your application server.</span></span>

## <a name="configure-the-agent"></a><span data-ttu-id="638aa-122">Aracısı'nı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="638aa-122">Configure the agent</span></span>
<span data-ttu-id="638aa-123">Adlı bir dosya oluşturun `AI-Agent.xml` ve aracı JAR dosyasını aynı klasöre yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="638aa-123">Create a file named `AI-Agent.xml` and place it in the same folder as the agent JAR file.</span></span>

<span data-ttu-id="638aa-124">Xml dosyasının içeriğini ayarlarsınız.</span><span class="sxs-lookup"><span data-stu-id="638aa-124">Set the content of the xml file.</span></span> <span data-ttu-id="638aa-125">İstediğiniz dahil etmek veya özellikleri atlamak için aşağıdaki örnek düzenleyin.</span><span class="sxs-lookup"><span data-stu-id="638aa-125">Edit the following example to include or omit the features you want.</span></span>

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

           <!-- Report on the particular signature
                void methodTwo(String, int) -->
           <Method name="methodTwo"
              reportExecutionTime="true"
              signature="(Ljava/lang/String;I)V" />
        </Class>

      </Instrumentation>
    </ApplicationInsightsAgent>

```

<span data-ttu-id="638aa-126">Raporları özel durumu ve yöntemi zamanlama tek tek yöntemleri için etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="638aa-126">You have to enable reports exception and method timing for individual methods.</span></span>

<span data-ttu-id="638aa-127">Varsayılan olarak, `reportExecutionTime` geçerlidir ve `reportCaughtExceptions` false olur.</span><span class="sxs-lookup"><span data-stu-id="638aa-127">By default, `reportExecutionTime` is true and `reportCaughtExceptions` is false.</span></span>

## <a name="view-the-data"></a><span data-ttu-id="638aa-128">Verileri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="638aa-128">View the data</span></span>
<span data-ttu-id="638aa-129">Application Insights kaynağını toplanmış uzak bağımlılık ve yöntemi yürütme sürelerinin görünür [performans bölmesi altında][metrics].</span><span class="sxs-lookup"><span data-stu-id="638aa-129">In the Application Insights resource, aggregated remote dependency and method execution times appears [under the Performance tile][metrics].</span></span>

<span data-ttu-id="638aa-130">Bağımlılık, özel durum ve yöntemi raporları tek tek örneklerini aramak için açık [arama][diagnostic].</span><span class="sxs-lookup"><span data-stu-id="638aa-130">To search for individual instances of dependency, exception, and method reports, open [Search][diagnostic].</span></span>

<span data-ttu-id="638aa-131">[Tanılama bağımlılık sorunları - daha fazla bilgi](app-insights-asp-net-dependencies.md#diagnosis).</span><span class="sxs-lookup"><span data-stu-id="638aa-131">[Diagnosing dependency issues - learn more](app-insights-asp-net-dependencies.md#diagnosis).</span></span>

## <a name="questions-problems"></a><span data-ttu-id="638aa-132">Sorularınız mı var?</span><span class="sxs-lookup"><span data-stu-id="638aa-132">Questions?</span></span> <span data-ttu-id="638aa-133">Sorunlarınız mı var?</span><span class="sxs-lookup"><span data-stu-id="638aa-133">Problems?</span></span>
* <span data-ttu-id="638aa-134">Veri yok mu?</span><span class="sxs-lookup"><span data-stu-id="638aa-134">No data?</span></span> [<span data-ttu-id="638aa-135">Set güvenlik duvarı özel durumlar</span><span class="sxs-lookup"><span data-stu-id="638aa-135">Set firewall exceptions</span></span>](app-insights-ip-addresses.md)
* [<span data-ttu-id="638aa-136">Java Sorun Giderme</span><span class="sxs-lookup"><span data-stu-id="638aa-136">Troubleshooting Java</span></span>](app-insights-java-troubleshoot.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
