---
title: "aaaAnalytics - hello güçlü arama aracının Azure Application Insights | Microsoft Docs"
description: "Analytics, Application Insights hello güçlü tanılama arama aracının genel bakış. "
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 0a2f6011-5bcf-47b7-8450-40f284274b24
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: d2b41e2fff7cc786e11fa3dfe94fc46f1b86e9eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analytics-in-application-insights"></a>Application Insights analizleri
[Analytics](app-insights-analytics.md) hello güçlü arama özelliği [Application Insights](app-insights-overview.md). Bu sayfaları günlük analizi sorgu dili açıklanmaktadır. 

* **[Merhaba tanıtım videosunu izleyin](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.
* **[Benzetimli verilerimizi Analytics sürücüde test](https://analytics.applicationinsights.io/demo)**  uygulamanızı veri tooApplication Öngörüler henüz değil gönderiliyorsa.
* **[SQL-kullanıcıların kopya sayfası](https://aka.ms/sql-analytics)**  hello en yaygın deyimleri çevirir.
* **[Dil Başvurusu](app-insights-analytics-reference.md)**  nasıl toouse tüm hello hello günlük analizi sorgu dili güçlü özelliklerini öğrenin.


## <a name="queries-in-analytics"></a>Sorgularda Analytics
Tipik bir sorgu bir *kaynak* tablo izleyen bir dizi tarafından *işleçleri* ayırarak `|`. 

Örneğin, günlük hello kullanıcılarının Hyderabad, ne zaman web uygulamamız denemenin şimdi bulun. Ve var ki olsa da, hangi sonuç kodları tootheir HTTP isteklerini döndürülür görelim. 

```AIQL
requests
| where timestamp > ago(30d)
| summarize ClientCount = dcount(client_IP) by bin(timestamp, 1h), resultCode
| extend LocalTime = timestamp - 4h
| order by LocalTime desc
| render barchart
```

Biz, farklı istemci IP adresleri, hello saat hello tarafından hello son 7 gün gruplandırarak sayısı. 

> [!NOTE]
> Merhaba önceki 24h dışında tooget sonuçları 'timestamp' açıkça sorgunuzda yer ya da hello zaman aralığı açılan menüsünü kullanın.
>

Şimdi toostack hello sonuçları farklı yanıt kodları seçme grafik sunu çubuğu hello hello sonuçlarıyla görüntüle:

![Çubuk grafiği, x ve y eksenleri ardından kesimleme seçin](./media/app-insights-analytics/020.png)

Lunchtime ve Hyderabad yatak zamanında uygulamamıza en popüler olduğu gibi görünüyor. (Ve bu 500 kodlar araştırmanız gerekir.)

Güçlü istatistiksel işlemler vardır:

![İstatistiksel sorgu sonuçları](./media/app-insights-analytics/025.png)

Merhaba dil çok çekici özelliklere sahiptir:


* [Filtre](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html) ölçümleri ve özel özellikler de dahil olmak üzere herhangi bir sorgu tarafından ham uygulama telemetrinizi.
* [Katılma](https://docs.loganalytics.io/queryLanguage/query_language_joinoperator.html) birden çok tabloları – sayfa görünümleri, bağımlılık çağrıları, özel durumlar ve günlük izlemelerini ile ilişkilendirmek ister.
* Güçlü istatistiksel [toplamalar](https://docs.loganalytics.io/learn/tutorials/aggregations.html).
* Yalnızca, SQL kadar güçlü ve karmaşık sorgular için çok daha kolay: iç içe geçmiş deyimler yerine, bir başlangıç işlemi toohello hello verilerden sonraki kanal.
* Anında ve güçlü görselleştirmeler.
* [PIN grafikleri tooAzure panolar](app-insights-analytics-using.md#pin-to-dashboard).
* [Sorguları tooPower BI verme](app-insights-analytics-using.md#export-to-power-bi).
* Var olan bir [REST API](https://dev.applicationinsights.io/) toorun sorguları program aracılığıyla, örneğin Powershell'den kullanabileceğinizi.


## <a name="connect-tooyour-application-insights-data"></a>Tooyour uygulama istatistikleri verilerine bağlanma
Uygulamanızın analizi açmak [genel bakış dikey penceresinde](app-insights-dashboards.md) Application ınsights'ta: 

![Portal.Azure.com açın, Application Insights kaynağınıza açın ve analizi'ı tıklatın.](./media/app-insights-analytics/001.png)


## <a name="video"></a>Video

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 


[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]



## <a name="query-examples"></a>Sorgu örnekleri

Bu izlenecek yollar tooillustrate hello güç Analytics kullanmanın deneyin:

 *  [Otomatik tanılamayı ani ve adım istekleri süreleri atlar.](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Automatic%20diagnostics%20of%20sudden%20spikes%20or%20step%20jumps%20in%20requests%20duration&shared=true)
 *  [Zaman serisi analiz ile performans degradations analiz etme](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20performance%20degradations%20with%20time%20series%20analysis&shared=true)
 *  [Uygulama hataları autocluster ve diffpatterns analiz etme](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Analyzing%20application%20failures%20with%20autocluster%20and%20diffpatterns&shared=true)
 *  [Zaman serisi analiz ile Gelişmiş şekli algılama](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Advanced%20shape%20detection%20with%20time%20series%20analysis&shared=true)
 *  [(MAU/DAU vb. çalışırken) kayan pencere işlemleri tooanalyze uygulama kullanımı kullanma](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Using%20sliding%20window%20calculations%20to%20analyze%20usage%20metrics:%20rolling%20MAU~2FDAU%20and%20cohorts&shared=true)
 *  [Hizmet kesilmelerini algılanması tabanlı hata ayıklama günlüklerini analiz üzerinde](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Detection%20of%20service%20disruptions%20based%20on%20regression%20analysis%20of%20trace%20logs&shared=true) ve eşleşen bir blog gönderisini [burada](https://maximshklar.wordpress.com/2017/02/16/finding-trends-in-traces-with-smart-data-analytics).
 *  [Basit hata ayıklama günlüklerini kullanarak uygulamalarınızın performans profili oluşturma](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Profiling%20applications'%20performance%20with%20simple%20debug%20logs&shared=true) ve eşleşen bir blog gönderisini [burada](https://yossiattasblog.wordpress.com/2017/03/13/first-blog-post/)
 *  [Basit hata ayıklama günlüklerini kullanarak, kodu akışınızı her adımı için Hello süresini ölçme](https://analytics.applicationinsights.io/demo#/discover/query/main?title=Measuring%20the%20duration%20of%20each%20step%20in%20your%20code%20flow%20using%20simple%20debug%20logs&shared=true) ve eşleşen bir blog gönderisini [burada](https://yossiattasblog.wordpress.com/2017/03/14/measuring-the-duration-of-each-step-in-your-code-flow-using-simple-debug-logs/)
 *  [Çözümleme eşzamanlılık basit hata ayıklama günlüklerini kullanarak](https://analytics.applicationinsights.io/demo#/discover/query/results/chart?title=Analyzing%20concurrency%20with%20simple%20debug%20logs&shared=true) ve eşleşen bir blog gönderisini [burada](https://yossiattasblog.wordpress.com/2017/03/23/analyzing-concurrency-using-simple-debug-logs/)



## <a name="next-steps"></a>Sonraki adımlar
* Merhaba ile başlattığınız öneririz [dil Turu](app-insights-analytics-tour.md). 
* Hakkında daha fazla bilgi [analizi kullanarak](app-insights-analytics-using.md). 
* [Dil Başvurusu](app-insights-analytics-reference.md). 
