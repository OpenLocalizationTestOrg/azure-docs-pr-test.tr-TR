---
title: "Application Insights aaaPerformance sayaçları | Microsoft Docs"
description: "Sistem ve Application Insights özel .NET performans sayaçları izleyin."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 5b816f4c-a77a-4674-ae36-802ee3a2f56d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/11/2016
ms.author: bwren
ms.openlocfilehash: 0a51c225f1d1124c9e7fe89f34e747cb26a3589e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="system-performance-counters-in-application-insights"></a>Application Insights sistem performans sayaçları
Windows, çok çeşitli sağlar [performans sayaçları](http://www.codeproject.com/Articles/8590/An-Introduction-To-Performance-Counters) CPU doluluğu, bellek, disk ve ağ kullanımı gibi. Ayrıca kendi tanımlayabilirsiniz. [Application Insights](app-insights-overview.md) uygulamanız IIS altında bir şirket içi ana bilgisayar veya sanal makine toowhich, çalışıyorsa, bu performans sayaçlarını yönetimsel erişime sahip gösterebilir. Merhaba grafikleri hello kaynakları kullanılabilir tooyour dinamik uygulama belirtmek ve sunucu örnekleri arasında tooidentify dengesiz yük yardımcı olabilir.

Performans sayaçları, bu kesimleri sunucu örneği tarafından bir tablo içeren hello sunucuları dikey penceresinde görünür.

![Application Insights'ta bildirilen performans sayaçları](./media/app-insights-performance-counters/counters-by-server-instance.png)

(Performans sayaçlarını Azure Web uygulamaları için kullanılabilir değil. Ancak [Azure tanılama tooApplication Öngörüler Gönder](app-insights-azure-diagnostics.md).)

## <a name="view-counters"></a>Sayaçları görüntüleyin
Merhaba sunucuları dikey varsayılan bir performans sayaçlarını gösterir. 

toosee diğer sayaçları hello sunucuları dikey penceresinde hello grafikleri düzenleyebilir veya yeni bir [ölçüm Gezgini](app-insights-metrics-explorer.md) dikey ve yeni grafikler ekleyin. 

bir grafiği düzenlediğinizde hello kullanılabilir sayaçlar ölçümleri listelenir.

![Application Insights'ta bildirilen performans sayaçları](./media/app-insights-performance-counters/choose-performance-counters.png)

tek bir yerde tüm en yararlı grafikler toosee oluşturma bir [Pano](app-insights-dashboards.md) ve tooit sabitleyin.

## <a name="add-counters"></a>Sayaç ekleme
İstediğiniz hello performans sayacı hello ölçümleri listesinde gösterilen değil, hello Application Insights SDK'sı web sunucunuz toplama değil çünkü olmasıdır. Toodo şekilde yapılandırabilirsiniz.

1. Hangi sayaçları hello sunucuda bu PowerShell komutunu kullanarak sunucunuzun kullanılabilir olduğunu bulabilirsiniz:
   
    `Get-Counter -ListSet *`
   
    (Bkz [ `Get-Counter` ](https://technet.microsoft.com/library/hh849685.aspx).)
2. Applicationınsights.config açın.
   
   * Application Insights tooyour uygulama geliştirme sırasında eklediyseniz, projenizde Applicationınsights.config düzenleyin ve yeniden dağıtın tooyour sunucuları.
   * Çalışma zamanında Durum İzleyicisi tooinstrument bir web uygulaması kullandıysanız, IIS'de hello uygulamasının hello kök dizininde Applicationınsights.config bulun. Var. her sunucu örneğinde güncelleştirin.
3. Merhaba performans Toplayıcı yönergesi düzenleyin:
   
```XML
   
    <Add Type="Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule, Microsoft.AI.PerfCounterCollector">
      <Counters>
        <Add PerformanceCounter="\Objects\Processes"/>
        <Add PerformanceCounter="\Sales(photo)\# Items Sold" ReportAs="Photo sales"/>
      </Counters>
    </Add>

```

Standart sayaçları hem olanlar kendiniz uyguladık yakalayabilirsiniz. `\Objects\Processes`Standart bir sayaç örneği tüm Windows sistemlerinde kullanılabilir. `\Sales(photo)\# Items Sold`bir web hizmeti uygulanan özel bir sayaç örneğidir. 

Merhaba biçimi `\Category(instance)\Counter"`, veya örnekleri yok kategoriler, sadece `\Category\Counter`.

`ReportAs`Eşleşmeyen sayaç adları için gerekli olan `[a-zA-Z()/-_ \.]+` -diğer bir deyişle, ayarlar aşağıdaki hello karakterler içerir: harfler, köşeli ayraçlar, eğik çizgi, tire, alt çizgi, boşluk, yuvarlak nokta.

Bir örnek belirtirseniz, bir boyut "CounterInstanceName" hello, ölçüm raporlanan toplanacaktır.

### <a name="collecting-performance-counters-in-code"></a>Kodda performans sayaçlarını toplama
toocollect sistem performans sayaçları ve tooApplication Öngörüler göndermek, aşağıdaki hello parçacığı uyum sağlayabilir:


``` C#

    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\.NET CLR Memory([replace-with-application-process-name])\# GC Handles", "GC Handles")));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

Veya yapabileceğiniz Merhaba, oluşturduğunuz özel ölçümleri ile aynı anlama:

``` C#
    var perfCollectorModule = new PerformanceCollectorModule();
    perfCollectorModule.Counters.Add(new PerformanceCounterCollectionRequest(
      @"\Sales(photo)\# Items Sold", "Photo sales"));
    perfCollectorModule.Initialize(TelemetryConfiguration.Active);
```

## <a name="performance-counters-in-analytics"></a>Analytics performans sayaçları
Arama ve performans sayacı raporlarda görüntüleme [Analytics](app-insights-analytics.md).

Merhaba **performanceCounters** şeması sunan hello `category`, `counter` adı ve `instance` her performans sayacı adı.  Telemetri Hello her uygulama için yalnızca bu uygulama için hello sayaçları görürsünüz. Örneğin, toosee hangi sayaçları kullanılabilir: 

![Application Insights analytics performans sayaçları](./media/app-insights-performance-counters/analytics-performance-counters.png)

('Instance' burada toohello performans sayacı örneği başvuruyor, rol veya sunucu makine örneğini hello değil. Merhaba performans sayacı örneği adı genellikle sayaçları işlemci zamanı gibi hello işlem veya uygulama tarafından hello adı kesim.)

bir grafik hello son dönemde üzerinden kullanılabilir belleğin tooget: 

![Application Insights analytics'te bellek timechart](./media/app-insights-performance-counters/analytics-available-memory.png)

Gibi diğer telemetri **performanceCounters** de bir sütuna sahip `cloud_RoleInstance` uygulamanızı çalıştıran hello ana bilgisayar sunucu örneğinin hello kimliğini gösterir. Örneğin, toocompare hello uygulamanızın performansı ile Merhaba farklı makinelerde: 

![Performans rol örneğinde Application Insights tarafından analiz bölümlenmiş.](./media/app-insights-performance-counters/analytics-metrics-role-instance.png)

## <a name="aspnet-and-application-insights-counts"></a>ASP.NET ve Application Insights sayılar
*Hello hello özel durum oranı ve özel durumları ölçümleri arasındaki fark nedir?*

* *Özel durum oranı* bir sistem performans sayacı. Merhaba CLR tüm işlenmiş hello ve oluşturulan ve hello toplam bir örnekleme aralığı içinde hello aralığı hello uzunluğu ile böler işlenmeyen özel durumları sayar. Merhaba Application Insights SDK'sı bu sonucu toplar ve toohello portal gönderir.
* *Özel durumlar* hello hello portal hello grafik hello örnekleme aralığı içinde tarafından alınan TrackException raporları sayısıdır. Burada TrackException kodunuzda çağırır ve tüm içermeyen yazmıştır özel durumlar Hello işlenmiş yalnızca içerir [işlenmeyen özel durumlar](app-insights-asp-net-exceptions.md). 

## <a name="alerts"></a>Uyarılar
Diğer ölçümleri gibi yapabilecekleriniz [bir uyarı ayarlamak](app-insights-alerts.md) bir performans sayacı, bir sınır dışında kalırsa belirttiğiniz toowarn. Merhaba uyarıları dikey penceresini açın ve eklemek uyarı'ı tıklatın.

## <a name="next"></a>Sonraki adımlar
* [Bağımlılık izleme](app-insights-asp-net-dependencies.md)
* [Özel durum izleme](app-insights-asp-net-exceptions.md)

