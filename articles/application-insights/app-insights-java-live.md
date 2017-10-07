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
# <a name="application-insights-for-java-web-apps-that-are-already-live"></a>Zaten Java web uygulamaları için Application Insights Canlı


J2EE sunucunuzda zaten çalışan bir web uygulamanız varsa, kendisiyle izlemeye başlamadan [Application Insights](app-insights-overview.md) hello ihtiyaç toomake kod değişiklikleri veya projenizi yeniden derleyin. Bu seçenek ile tooyour server, İşlenmeyen özel durumları ve performans sayaçları gönderilen HTTP istekleri hakkında bilgi alın.

Bir abonelik çok gerekir[Microsoft Azure](https://azure.com).

> [!NOTE]
> Bu sayfada Hello yordam, çalışma zamanında hello SDK tooyour web uygulaması ekler. Bu çalışma zamanı araçları tooupdate istediğiniz yok veya kaynak kodu yeniden yararlıdır. Ancak yapabiliyorsanız, öneririz [hello SDK toohello kaynak kodunu ekleyin](app-insights-java-get-started.md) yerine. Bu kod tootrack kullanıcı etkinliği yazma gibi daha fazla seçenek verir.
> 
> 

## <a name="1-get-an-application-insights-instrumentation-key"></a>1. Application Insights izleme anahtarı edinme
1. İçinde toohello oturum [Microsoft Azure portalı](https://portal.azure.com)
2. Yeni bir Application Insights kaynağı oluşturun ve hello uygulama türü tooJava web uygulaması ayarlayın.
   
    ![Ad girme, Java web uygulaması seçme ve Oluştur’a tıklama](./media/app-insights-java-live/02-create.png)

    Merhaba kaynak birkaç saniye içinde oluşturulur.

4. Merhaba yeni kaynak açın ve izleme anahtarı edinme. Toopaste bu anahtar kod projenize kısa bir süre sonra ihtiyacınız vardır.
   
    ![Merhaba yeni kaynağa genel bakışta, Özellikler'i tıklatın ve hello izleme anahtarını kopyalama](./media/app-insights-java-live/03-key.png)

## <a name="2-download-hello-sdk"></a>2. Merhaba SDK yükle
1. Merhaba karşıdan [Java için Application Insights SDK](https://aka.ms/aijavasdk). 
2. Sunucunuzda, proje ikili dosyaları yüklü olan hello SDK içeriği toohello dizine ayıklayın. Tomcat kullanıyorsanız, bu dizin altında genelde olacaktır`webapps/<your_app_name>/WEB-INF/lib`

Toorepeat bu her sunucu örneğindeki ve her uygulama için gereksinim duyduğunuz olduğunu unutmayın.

## <a name="3-add-an-application-insights-xml-file"></a>3. Application Insights xml dosyası Ekle
Applicationınsights.XML hello SDK eklenen hello klasöründe oluşturun. İçine yerleştirin hello XML.

Hello Azure portal ' aldığınız hello izleme anahtarını Bununla değiştirin.

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

* Merhaba izleme anahtarı telemetrinin her öğesiyle birlikte gönderilir ve Application Insights toodisplay söyler kaynağınız içinde.
* Merhaba HTTP isteği bileşeni isteğe bağlıdır. İstek ve yanıt sürelerini toohello portal hakkında telemetriyi otomatik olarak gönderir.
* Olay bağıntısı bir toplama toohello HTTP isteği bileşendir. Merhaba sunucu tarafından alınan bir tanımlayıcı tooeach isteği atar ve bu tanımlayıcı telemetri bir özellik tooevery öğesi olarak 'Operation.Id' hello özelliği olarak ekler. Bir filtre ayarlayarak her istekle ilişkili toocorrelate hello telemetri tanır [tanılama arama](app-insights-diagnostic-search.md).

## <a name="4-add-an-http-filter"></a>4. HTTP filtresi ekleme
Bulup, proje ve uygulama filtrelerinizin yapılandırıldığı hello web uygulaması düğümü altında kod parçacığını aşağıdaki birleştirme hello hello web.xml dosyasını açın.

tooget hello en doğru sonuçlar, hello filtre önce tüm diğer filtrelerle eşlenmesi gerekir.

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

## <a name="5-check-firewall-exceptions"></a>5. Güvenlik Duvarı özel durumlarını denetleyin
Çok gerekebilecek[özel durumları toosend giden veri kümesi](app-insights-ip-addresses.md).

## <a name="6-restart-your-web-app"></a>6. Web uygulamanızı yeniden başlatın
## <a name="7-view-your-telemetry-in-application-insights"></a>7. Application Insights'da telemetrinizi görüntüleme
Tooyour Application Insights kaynağını dönmek [Microsoft Azure portal](https://portal.azure.com).

HTTP istekleriyle ilgili telemetri hello genel bakış dikey penceresinde görüntülenir. (Orada değilse, birkaç saniye bekleyip Yenile’ye tıklayın.)

![örnek veri](./media/app-insights-java-live/5-results.png)

Tıklatın herhangi grafik toosee ayrıntılı ölçümler. 

![](./media/app-insights-java-live/6-barchart.png)

Ve istek hello özellikleri görüntülendiğinde, istekler ve özel durumlar gibi ilişkili hello telemetri olayları görebilirsiniz.

![](./media/app-insights-java-live/7-instance.png)

[Ölçümler hakkında daha fazla bilgi edinin.](app-insights-metrics-explorer.md)

## <a name="next-steps"></a>Sonraki adımlar
* [Telemetri tooyour web sayfaları eklemek](app-insights-javascript.md) toomonitor sayfa görünümlerini ve kullanıcı ölçümlerini.
* [Web testleri oluşturma](app-insights-monitor-web-app-availability.md) toomake uygulamanızın canlı ve duyarlı kaldığından emin.
* [Günlük izlemelerini yakalama](app-insights-java-trace-logs.md)
* [Olayları ve günlükleri arayın](app-insights-diagnostic-search.md) toohelp sorunları tanılayın.

