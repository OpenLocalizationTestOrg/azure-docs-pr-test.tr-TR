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
# <a name="explore-java-trace-logs-in-application-insights"></a>Application Insights izleme günlüklerini Java keşfedin
Logback veya Log4J kullanıyorsanız (1.2 sürümü veya v2.0) izleme için otomatik olarak tooApplication burada keşfedin ve bunlar üzerinde arama Öngörüler gönderilen, izleme günlükleri sahip olabilir.

## <a name="install-hello-java-sdk"></a>Merhaba Java SDK'sını yükleyin

Yükleme [Java için Application Insights SDK][java], size, bu işlemi yapmadıysanız.

(Tootrack HTTP isteklerini istemiyorsanız, hello .xml yapılandırma dosyası çoğunu atlayabilirsiniz, ancak en az hello içermelidir `InstrumentationKey` öğesi. Ayrıca çağırmalıdır `new TelemetryClient()` tooinitialize hello SDK.)


## <a name="add-logging-libraries-tooyour-project"></a>Günlüğe kaydetme kitaplıkları tooyour proje ekleyin
*Projeniz için uygun şekilde Hello seçin.*

#### <a name="if-youre-using-maven"></a>Maven kullanıyorsanız...
Projeniz zaten toouse Maven derleme için ayarladıysanız, kod parçacıkları pom.xml dosyanıza aşağıdaki hello birini birleştirin.

Ardından hello proje bağımlılıklarını, indirilen tooget hello ikili yenileyin.

*Logback*

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-logback</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

*Log4J v2.0*

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

*Log4J 1.2 sürümü*

```XML

    <dependencies>
       <dependency>
          <groupId>com.microsoft.azure</groupId>
          <artifactId>applicationinsights-logging-log4j1_2</artifactId>
          <version>[1.0,)</version>
       </dependency>
    </dependencies>
```

#### <a name="if-youre-using-gradle"></a>Gradle kullanıyorsanız...
Projeniz zaten toouse Gradle derleme için ayarladıysanız, aşağıdaki satırları toohello hello birini ekleyin `dependencies` build.gradle dosyanızla grubu:

Ardından hello proje bağımlılıklarını, indirilen tooget hello ikili yenileyin.

**Logback**

```

    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-logback', version: '1.0.+'
```

**Log4J v2.0**

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j2', version: '1.0.+'
```

**Log4J 1.2 sürümü**

```
    compile group: 'com.microsoft.azure', name: 'applicationinsights-logging-log4j1_2', version: '1.0.+'
```

#### <a name="otherwise-"></a>Aksi taktirde...
Karşıdan yükleyin ve hello uygun appender ayıklayın ve sonra hello uygun kitaplığı tooyour projesini ekleyin:

| Günlükçü | İndir | Kitaplık |
| --- | --- | --- |
| Logback |[SDK Logback appender ile](https://aka.ms/xt62a4) |applicationınsights günlük logback |
| Log4J v2.0 |[Log4J v2 appender SDK'sı](https://aka.ms/qypznq) |applicationınsights günlük log4j2 |
| Log4j 1.2 sürümü |[Log4J 1.2 sürümü appender SDK'sı](https://aka.ms/ky9cbo) |applicationınsights günlük log4j1_2 |

## <a name="add-hello-appender-tooyour-logging-framework"></a>Merhaba appender tooyour günlüğü framework ekleme
Başlarken izlemeleri, birleştirme hello ilgili parçacığını kod toohello Log4J veya Logback yapılandırma dosyası toostart: 

*Logback*

```XML

    <appender name="aiAppender" 
      class="com.microsoft.applicationinsights.logback.ApplicationInsightsAppender">
    </appender>
    <root level="trace">
      <appender-ref ref="aiAppender" />
    </root>
```

*Log4J v2.0*

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

*Log4J 1.2 sürümü*

```XML

    <appender name="aiAppender" 
         class="com.microsoft.applicationinsights.log4j.v1_2.ApplicationInsightsAppender">
    </appender>
    <root>
      <priority value ="trace" />
      <appender-ref ref="aiAppender" />
    </root>
```

Merhaba Application Insights appenders (Merhaba kod örnekleri yukarıda gösterildiği gibi) yapılandırılmış tüm Günlükçü ve mutlaka hello kök Günlükçü tarafından başvurulabilir.

## <a name="explore-your-traces-in-hello-application-insights-portal"></a>Merhaba Application Insights portalında, izlemeleri keşfedin
Yapılandırdığınız göre proje toosend tooApplication Öngörüler izler, görüntüleyin ve bu izlemelerin hello de hello Application Insights portalında arama [arama] [ diagnostic] dikey.

![Arama Hello Application Insights portalında açın](./media/app-insights-java-trace-logs/10-diagnostics.png)

## <a name="next-steps"></a>Sonraki adımlar
[Tanılama arama][diagnostic]

<!--Link references-->

[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md


