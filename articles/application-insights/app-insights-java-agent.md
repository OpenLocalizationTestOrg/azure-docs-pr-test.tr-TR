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
# <a name="monitor-dependencies-exceptions-and-execution-times-in-java-web-apps"></a>Bağımlılıklar, özel durumlar ve yürütme sürelerini Java web uygulamalarını izleme


Varsa [Java web uygulamanıza Application Insights ile işaretlenir][java], hello Java Agent tooget daha ayrıntılı Öngörüler, kod değişiklikleri olmadan kullanabilirsiniz:

* **Bağımlılıklar:** tooother bileşenleri de dahil olmak üzere, uygulamanızın yaptığı çağrıları hakkında veriler:
  * **REST çağrılarını** HttpClient, OkHttp ve RestTemplate (yay) yapılır.
  * **Redis** hello Jedis istemci yapılan çağrıları. Merhaba çağrısı 10'luk uzun sürerse, hello aracı ayrıca hello çağrı bağımsız getirir.
  * **[JDBC çağrıları](http://docs.oracle.com/javase/7/docs/technotes/guides/jdbc/)**  -MySQL, SQL Server, PostgreSQL, SQLite, Oracle DB veya Apache Derby DB. "executeBatch" çağrıları desteklenir. Merhaba çağrısı 10'luk uzun sürerse, MySQL ve PostgreSQL için hello Aracısı hello sorgu planı bildirir.
* **Özel durum yakalandı:** kodunuz tarafından işlenen özel durumlar hakkında veri.
* **Yöntem yürütme süresi:** hello hakkındaki verileri alır tooexecute belirli yöntemler seferlik.

toouse hello Java agent, sunucunuza yükleyin. Web uygulamalarınızı hello ile işaretlenir gerekir [Application Insights Java SDK'sı][java]. 

## <a name="install-hello-application-insights-agent-for-java"></a>Java için Application Insights Aracısı Hello yükleyin
1. Java sunucunuz Hello makine üzerinde çalışan [hello Aracısı'nı indirme](https://aka.ms/aijavasdk).
2. Merhaba uygulama sunucusu başlangıç komut dosyasını düzenleyin ve JVM aşağıdaki hello ekleyin:
   
    `javaagent:`*tam yol toohello Aracısı JAR dosyasını*
   
    Örneğin, Tomcat'te bir Linux makinesinde:
   
    `export JAVA_OPTS="$JAVA_OPTS -javaagent:<full path tooagent JAR file>"`
3. Uygulama sunucunuzu yeniden başlatın.

## <a name="configure-hello-agent"></a>Merhaba Aracısı'nı yapılandırma
Adlı bir dosya oluşturun `AI-Agent.xml` ve hello yerleştirin hello Aracısı JAR dosyasını aynı klasöre.

Merhaba xml dosyası Merhaba içeriğine ayarlayın. Aşağıdaki örnek tooinclude hello düzenleyin veya hello özellikleri atlayın.

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

Tooenable raporları özel durumu ve tek tek yöntemleri için yöntemi zamanlama var.

Varsayılan olarak, `reportExecutionTime` geçerlidir ve `reportCaughtExceptions` false olur.

## <a name="view-hello-data"></a>Merhaba verileri görüntüleme
Hello Application Insights kaynağı, toplanan uzak bağımlılık ve yöntemi yürütme sürelerinin görünür [performans hello altında döşeme][metrics].

bağımlılık, özel durum ve yöntemi raporları, tek tek örneklerini toosearch açmak [arama][diagnostic].

[Tanılama bağımlılık sorunları - daha fazla bilgi](app-insights-asp-net-dependencies.md#diagnosis).

## <a name="questions-problems"></a>Sorularınız mı var? Sorunlarınız mı var?
* Veri yok mu? [Set güvenlik duvarı özel durumlar](app-insights-ip-addresses.md)
* [Java Sorun Giderme](app-insights-java-troubleshoot.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#track-exception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
