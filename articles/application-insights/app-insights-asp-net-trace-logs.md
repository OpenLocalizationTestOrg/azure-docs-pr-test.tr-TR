---
title: "Application Insights'ta aaaExplore .NET izleme günlükleri"
description: "İzleme, NLog veya Log4Net ile oluşturulan günlükleri arayın."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 0c2a084f-6e71-467b-a6aa-4ab222f17153
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 6bfcd9e5751c3656236d7eb2fc09321740171a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-net-trace-logs-in-application-insights"></a>.NET izleme günlükleri Application ınsights'ta keşfedin
NLog, log4Net veya System.Diagnostics.Trace, ASP.NET uygulamanızda Tanılama izleme için kullanırsanız, çok gönderilen günlüklerinizi olabilir[Azure Application Insights][start], burada keşfedin aramak ve bunları. Günlüklerinizi hello ile diğer birleştirilecek tanımlayabilirsiniz böylece, uygulamadan gelen telemetri hello her kullanıcı isteği hizmeti ile ilişkilendirilmiş izlemeleri ve diğer olayları ve özel durum raporları ile ilişkilendirilmesi.

> [!NOTE]
> Merhaba günlük yakalama modülü gerekiyor mu? 3. taraf günlükçüleri için yararlı bir bağdaştırıcı olduğundan, ancak NLog kullanmıyorsanız, log4Net veya System.Diagnostics.Trace, göz önünde bulundurun yalnızca arama [uygulama Öngörüler TrackTrace()](app-insights-api-custom-events-metrics.md#tracktrace) doğrudan.
>
>

## <a name="install-logging-on-your-app"></a>Uygulamanıza oturum yükleyin
Seçilen günlük framework projenize yükleyin. Bu app.config veya web.config bir girişe neden.

System.Diagnostics.Trace kullanıyorsanız, tooadd bir giriş tooweb.config gerekir:

```XML

    <configuration>
     <system.diagnostics>
       <trace autoflush="false" indentsize="4">
         <listeners>
           <add name="myListener"
             type="System.Diagnostics.TextWriterTraceListener"
             initializeData="TextWriterOutput.log" />
           <remove name="Default" />
         </listeners>
       </trace>
     </system.diagnostics>
   </configuration>
```
## <a name="configure-application-insights-toocollect-logs"></a>Application Insights toocollect günlüklerini yapılandırma
**[Application Insights tooyour projesi eklemek](app-insights-asp-net.md)**  bunu, henüz yapmadıysanız. Bir seçenek tooinclude hello günlük Toplayıcı görürsünüz.

Veya **yapılandırma Application Insights** Çözüm Gezgini'nde projenize sağ tarafından. Çok olarak Hello seçeneğini**izleme koleksiyonu yapılandırma**.

*Application Insights menüsü veya günlük Toplayıcı seçeneği yok?* Deneyin [sorun giderme](#troubleshooting).

## <a name="manual-installation"></a>El ile yükleme
Proje türü hello Application Insights Yükleyici (örneğin Windows Masaüstü projesi) tarafından desteklenmiyor, bu yöntemi kullanın.

1. Toouse log4Net veya NLog düşünüyorsanız, projenize yükleyin.
2. Çözüm Gezgini'nde, projenize sağ tıklayın ve seçin **NuGet paketlerini Yönet**.
3. "Application Insights" araması yapın
4. Merhaba uygun paket - aşağıdakilerden birini seçin:

   * Microsoft.ApplicationInsights.TraceListener (toocapture System.Diagnostics.Trace çağrı)
   * Microsoft.ApplicationInsights.EventSourceListener (toocapture EventSource olaylarını)
   * Microsoft.ApplicationInsights.EtwListener (toocapture ETW olayları)
   * Microsoft.ApplicationInsights.NLogTarget
   * Microsoft.ApplicationInsights.Log4NetAppender

Merhaba NuGet paketi hello gerekli derlemeleri yükler ve ayrıca web.config veya app.config değiştirir.

## <a name="insert-diagnostic-log-calls"></a>Tanılama günlük çağrıları Ekle
System.Diagnostics.Trace kullanırsanız, tipik bir çağrı olacaktır:

    System.Diagnostics.Trace.TraceWarning("Slow response - database01");

Log4net veya NLog isterseniz:

    logger.Warn("Slow response - database01");

## <a name="using-eventsource-events"></a>EventSource olaylarını kullanma
Yapılandırabileceğiniz [System.Diagnostics.Tracing.EventSource](https://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource.aspx) olayları gönderilen toobe tooApplication Öngörüler izlemeleri olarak. İlk olarak, hello yükleyin `Microsoft.ApplicationInsights.EventSourceListener` NuGet paketi. Daha sonra Düzenle `TelemetryModules` hello bölümünü [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md) dosya.

```xml
    <Add Type="Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule, Microsoft.ApplicationInsights.EventSourceListener">
      <Sources>
        <Add Name="MyCompany" Level="Verbose" />
      </Sources>
    </Add>
```

Her bir kaynağı için şu parametreler hello ayarlayabilirsiniz:
 * `Name`Merhaba EventSource toocollect Hello adını belirtir.
 * `Level`günlüğe kaydetme düzeyi toocollect hello belirtir. Aşağıdakilerden biri olabilir `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.
 * `Keywords`(İsteğe bağlı) anahtar sözcükleri birleşimleri toouse hello tamsayı değerini belirtir.

## <a name="using-diagnosticsource-events"></a>DiagnosticSource olaylarını kullanma
Yapılandırabileceğiniz [System.Diagnostics.DiagnosticSource](https://github.com/dotnet/corefx/blob/master/src/System.Diagnostics.DiagnosticSource/src/DiagnosticSourceUsersGuide.md) olayları gönderilen toobe tooApplication Öngörüler izlemeleri olarak. İlk olarak, hello yükleyin [ `Microsoft.ApplicationInsights.DiagnosticSourceListener` ](https://www.nuget.org/packages/Microsoft.ApplicationInsights.DiagnosticSourceListener) NuGet paketi. Merhaba Düzenle `TelemetryModules` hello bölümünü [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md) dosya.

```xml
    <Add Type="Microsoft.ApplicationInsights.DiagnsoticSourceListener.DiagnosticSourceTelemetryModule, Microsoft.ApplicationInsights.DiagnosticSourceListener">
      <Sources>
        <Add Name="MyDiagnosticSourceName" />
      </Sources>
    </Add>
```

Tootrace, istediğiniz her DiagnosticSource için hello olan bir giriş eklemek `Name` özniteliği, DiagnosticSource toohello adını ayarlayın.

## <a name="using-etw-events"></a>ETW olayları kullanma
ETW olayları toobe tooApplication Öngörüler izlemeleri gönderilen yapılandırabilirsiniz. İlk olarak, hello yükleyin `Microsoft.ApplicationInsights.EtwCollector` NuGet paketi. Daha sonra Düzenle `TelemetryModules` hello bölümünü [Applicationınsights.config](app-insights-configuration-with-applicationinsights-config.md) dosya.

> [!NOTE] 
> Merhaba işlem barındırma hello SDK'sı, "Performans günlüğü kullanıcıları" veya yöneticileri üyesi olan bir kimlik altında çalışıyorsa, ETW olayları yalnızca toplanabilir.

```xml
    <Add Type="Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule, Microsoft.ApplicationInsights.EtwCollector">
      <Sources>
        <Add ProviderName="MyCompanyEventSourceName" Level="Verbose" />
      </Sources>
    </Add>
```

Her bir kaynağı için şu parametreler hello ayarlayabilirsiniz:
 * `ProviderName`Merhaba ETW sağlayıcı toocollect Hello adıdır.
 * `ProviderGuid`Merhaba hello ETW sağlayıcı toocollect GUİD'si belirtir yerine kullanılabilir `ProviderName`.
 * `Level`günlüğe kaydetme düzeyi toocollect hello ayarlar. Aşağıdakilerden biri olabilir `Critical`, `Error`, `Informational`, `LogAlways`, `Verbose`, `Warning`.
 * `Keywords`(İsteğe bağlı) kümeleri anahtar sözcüğü birleşimleri toouse tamsayı değerini hello.

## <a name="using-hello-trace-api-directly"></a>Merhaba izleme API kullanarak doğrudan
Merhaba Application Insights izleme API doğrudan çağırabilir. Merhaba günlük bağdaştırıcıları bu API'yi kullanın.

Örneğin:

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow response - database01");

TrackTrace avantajı hello iletisinde oldukça uzun veri koyabilirsiniz ' dir. Örneğin, gönderme verisi kodlayın.

Ayrıca, bir önem düzeyi tooyour ileti ekleyebilirsiniz. Ve diğer telemetri gibi toohelp filtre veya arama izlemeleri farklı kümeleri için kullanabileceğiniz özellik değerlerini ekleyebilirsiniz. Örneğin:

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

Bu, içinde sağlayacağı [arama][diagnostic], tooeasily filtre tooa belirli veritabanı ile ilgili belirli bir önemde tüm hello iletilerinin çıkışı.

## <a name="explore-your-logs"></a>Günlüklerinizi keşfedin
Uygulamanızı, ya da hata ayıklama modunda çalıştırmak veya dinamik dağıtın.

Uygulamanızın genel bakış dikey penceresinde de [hello Application Insights portalındaki][portal], seçin [arama][diagnostic].

![Application Insights'ta arama seçin](./media/app-insights-asp-net-trace-logs/020-diagnostic-search.png)

![Arama](./media/app-insights-asp-net-trace-logs/10-diagnostics.png)

Örneğin yapabilecekleriniz:

* Günlük izlemelerini veya belirli özelliklere sahip öğeleri Filtrele
* Belirli bir öğeyi ayrıntılı inceleyin.
* Toohello ilgili diğer telemetriyi Bul aynı kullanıcı isteği (diğer bir deyişle, ile aynı hello Operationıd)
* Bu sayfanın Hello yapılandırma sık kullanılan olarak Kaydet

> [!NOTE]
> **Örnekleme.** Uygulamanız çok miktarda veri gönderir ve hello Application Insights SDK'sı ASP.NET sürüm 2.0.0-beta3 veya üzeri kullanıyorsanız, hello Uyarlamalı örnekleme özelliği çalışır ve yalnızca telemetrinizi yüzdesi gönderin. [Örnekleme hakkında daha fazla bilgi edinin.](app-insights-sampling.md)
>
>

## <a name="next-steps"></a>Sonraki adımlar
[Hataları ve ASP.NET özel durumları tanılama][exceptions]

[Arama hakkında daha fazla bilgi][diagnostic].

## <a name="troubleshooting"></a>Sorun giderme
### <a name="how-do-i-do-this-for-java"></a>Bunu nasıl yapabilirim Java için?
Kullanım hello [Java günlük bağdaştırıcıları](app-insights-java-trace-logs.md).

### <a name="theres-no-application-insights-option-on-hello-project-context-menu"></a>Merhaba proje bağlam menüsünde Application Insights seçeneği yoktur
* Application Insights araçları bu geliştirme makinede yüklü denetleyin. Visual Studio menü Araçlar, uzantılar ve güncelleştirmeler, için Application Insights araçları arayın. Merhaba yüklü sekmesinde değilse, çevrimiçi hello sekmesini açın ve yükleyin.
* Bu proje Application Insights araçları tarafından desteklenmeyen bir türde olabilir. Kullanım [el ile yükleme](#manual-installation).

### <a name="no-log-adapter-option-in-hello-configuration-tool"></a>Merhaba Yapılandırma aracında günlük bağdaştırıcısı seçeneği
* Tooinstall hello günlük önce gerekir.
* System.Diagnostics.Trace kullanıyorsanız, emin [içinde yapılandırılmış `web.config` ](https://msdn.microsoft.com/library/system.diagnostics.eventlogtracelistener.aspx).
* Application Insights en son sürümünü hello var mı? Visual Studio'da **Araçları** menüsünde seçin **Uzantılar ve güncelleştirmeler**ve açık hello **güncelleştirmeleri** sekmesi. Geliştirici analiz araçları vardır, tooupdate'yı tıklatın.

### <a name="emptykey"></a>"İzleme anahtarını boş olamaz" hata alıyorum
Application Insights yüklemeden bağdaştırıcısı Nuget paketi günlüğü hello yüklü gibi görünüyor.

Çözüm Gezgini'nde sağ `ApplicationInsights.config` ve **güncelleştirme Application Insights**. Toosign, başvurulmasını bir iletişim kutusu içinde tooAzure elde edersiniz ve ya da bir Application Insights kaynağı oluşturun veya var olan bir yeniden kullanın. Bu sorununu çözer.

### <a name="i-can-see-traces-in-diagnostic-search-but-not-hello-other-events"></a>I tanılama arama içindeki görebilir, ancak diğer olayları hello değil
Bu, bazen hello ardışık düzeninden tüm hello olayları ve istekleri tooget için biraz zaman alabilir.

### <a name="limits"></a>Ne kadar veri tutulur?
Pek çok etken hello korunur veri miktarını etkileyebilir. Merhaba bkz [sınırları](app-insights-api-custom-events-metrics.md#limits) sayfasının bölümünde hello müşteri olay ölçümleri daha fazla bilgi için. 

### <a name="im-not-seeing-some-of-hello-log-entries-that-i-expect"></a>Bazı t beklediğiniz hello günlük girdileri görüyorum değil
Uygulamanız çok miktarda veri gönderir ve hello Application Insights SDK'sı ASP.NET sürüm 2.0.0-beta3 veya üzeri kullanıyorsanız, hello Uyarlamalı örnekleme özelliği çalışır ve yalnızca telemetrinizi yüzdesi gönderin. [Örnekleme hakkında daha fazla bilgi edinin.](app-insights-sampling.md)

## <a name="add"></a>Sonraki adımlar
* [Kullanılabilirlik ve yanıt hızını testleri ayarlama][availability]
* [Sorun giderme][qna]

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[portal]: https://portal.azure.com/
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
