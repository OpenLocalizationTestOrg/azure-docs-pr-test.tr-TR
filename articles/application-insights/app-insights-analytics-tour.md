---
title: "Azure Application Insights Analytics üzerinden aaaA tur | Microsoft Docs"
description: "Tüm hello ana sorgularda Analytics, Application Insights hello güçlü arama aracının kısa örnekleri."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: bddf4a6d-ea8d-4607-8531-1fe197cc57ad
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/06/2017
ms.author: bwren
ms.openlocfilehash: c268e26c6bf93ac2ee2a9d5e83613150dcf90b04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="a-tour-of-analytics-in-application-insights"></a>Application ınsights'ta Analytics turu
[Analytics](app-insights-analytics.md) hello güçlü arama özelliği [Application Insights](app-insights-overview.md). Bu sayfaları günlük analizi sorgu dili açıklanmaktadır.

* **[Merhaba tanıtım videosunu izleyin](https://applicationanalytics-media.azureedge.net/home_page_video.mp4)**.
* **[Benzetimli verilerimizi Analytics sürücüde test](https://analytics.applicationinsights.io/demo)**  uygulamanızı veri tooApplication Öngörüler henüz değil gönderiliyorsa.
* **[SQL-kullanıcıların kopya sayfası](https://aka.ms/sql-analytics)**  hello en yaygın deyimleri çevirir.

Başlattığınız bazı temel sorguları tooget aracılığıyla ilerlemesi atalım.

## <a name="connect-tooyour-application-insights-data"></a>Tooyour uygulama istatistikleri verilerine bağlanma
Uygulamanızın analizi açmak [genel bakış dikey penceresinde](app-insights-dashboards.md) Application ınsights'ta:

![Portal.Azure.com açın, Application Insights kaynağınıza açın ve analizi'ı tıklatın.](./media/app-insights-analytics-tour/001.png)

## <a name="takehttpsdocsloganalyticsioquerylanguagequerylanguagetakeoperatorhtml-show-me-n-rows"></a>[Ele](https://docs.loganalytics.io/queryLanguage/query_language_takeoperator.html): n satırları göster
Kullanıcı işlemleri (web uygulamanız tarafından alınan genellikle HTTP isteklerini) oturum veri noktaları denilen bir tabloda depolanır `requests`. Her satır, uygulamanıza Application Insights SDK'sı hello alınan telemetri bir veri noktasıdır.

Merhaba tablonun birkaç örnek satırlarını inceleyerek başlayalım:

![sonuçlar](./media/app-insights-analytics-tour/010.png)

> [!NOTE]
> Git tıklamadan önce hello imleç hello deyiminde yere yerleştirin. Bir deyim birden fazla hattından bölebilirsiniz ancak boş satırlar bir deyimde koymayın. Boş satırlar olan uygun şekilde tookeep birkaç ayrı hello penceresinde sorgular.
>
>

Sütunları seçin, bunları sütunlara göre Gruplandır sürükleyin ve filtre:

![Sütun Seçimi sonuçlarının üst sağ tıklatın](./media/app-insights-analytics-tour/030.png)

Hiçbir öğe toosee hello ayrıntı genişletin:

![Tablo seçin ve yapılandırma sütunları kullanın](./media/app-insights-analytics-tour/040.png)

> [!NOTE]
> Bir sütun toore düzeni hello sonuçları hello web tarayıcısında kullanılabilir Hello başı'ı tıklatın. Ancak büyük sonuç kümesi için satır indirilen toohello tarayıcı hello sayısı sınırlı olduğunu unutmayın. Bu şekilde sıralama, her zaman en yüksek gerçek hello veya en düşük öğeleri göstermez. toosort öğelerini güvenilir bir şekilde, hello kullanma `top` veya `sort` işleci.
>
>

## <a name="tophttpsdocsloganalyticsioquerylanguagequerylanguagetopoperatorhtml-and-sorthttpsdocsloganalyticsioquerylanguagequerylanguagesortoperatorhtml"></a>[Üst](https://docs.loganalytics.io/queryLanguage/query_language_topoperator.html) ve [sıralama](https://docs.loganalytics.io/queryLanguage/query_language_sortoperator.html)
`take`yararlı tooget bir sonuç hızlı örneğidir ancak hello tablodaki belirli bir sırada gösterir. tooget sıralı bir görünümü kullanmak `top` (için bir örnek) veya `sort` (üzerinden hello tüm tablo).

Belirli bir sütuna göre sıralanmış hello ilk n satırları göster:

```AIQL

    requests | top 10 by timestamp desc
```

* *Sözdizimi:* çoğu işleçleri gibi anahtar sözcüğü parametrelere sahip `by`.
* `desc`azalan düzende = `asc` artan =.

![](./media/app-insights-analytics-tour/260.png)

`top...`Daha fazla kullanıcı bildiren yoludur `sort ... | take...`. Biz yazılı:

```AIQL

    requests | sort by timestamp desc | take 10
```

Merhaba sonuç aynı Merhaba, ancak biraz daha yavaş çalışır olacaktır. (Ayrıca yazabilirsiniz `order`, bir diğer ad olduğu `sort`.)

Merhaba Tablo görünümünde Hello sütun üst bilgileri de Merhaba ekranında kullanılan toosort hello sonuçları olabilir. Ancak, kullandıysanız Kuşkusuz `take` veya `top` tooretrieve yalnızca bir tablonun parçası, alınan yalnızca yeniden sıralamak hello kayıtları gerekir.

## <a name="wherehttpsdocsloganalyticsioquerylanguagequerylanguagewhereoperatorhtml-filtering-on-a-condition"></a>[Burada](https://docs.loganalytics.io/queryLanguage/query_language_whereoperator.html): bir koşula göre filtreleme

Belirli Sonuç kodu döndürdü yalnızca istekleri görelim:

```AIQL

    requests
    | where resultCode  == "404"
    | take 10
```

![](./media/app-insights-analytics-tour/250.png)

Merhaba `where` işleci bir Boole ifadesi alır. Bunlarla ilgili bazı önemli noktalar şunlardır:

* `and`, `or`: Boole işleçleri
* `==`, `<>`, `!=` : eşit ve eşit değil
* `=~`, `!~` : büyük küçük harf duyarlı dize eşit ve eşit değil. Daha fazla dize karşılaştırma işleçleri çok vardır.

<!---Read all about [scalar expressions]().--->

### <a name="getting-hello-right-type"></a>Merhaba sağ türü alınıyor
Başarısız istekleri Bul:

```AIQL

    requests
    | where isnotempty(resultCode) and toint(resultCode) >= 400
```
<!---
`resultCode` has type string, so we must cast it app-insights-analytics-reference.md#casts for a numeric comparison.
--->

## <a name="time"></a>Zaman

Varsayılan olarak, sorgularınızı kısıtlı toohello son 24 saat etkilenir. Ancak bu aralığı değiştirebilirsiniz:

![](./media/app-insights-analytics-tour/change-time-range.png)

İlgili herhangi bir sorgu yazarak Hello zaman aralığını geçersiz kılma `timestamp` where yan tümcesinde. Örneğin:

```AIQL

    // What were hello slowest requests over hello past 3 days?
    requests
    | where timestamp > ago(3d)  // Override hello time range
    | top 5 by duration
```

Merhaba zaman aralığı eşdeğer tooa 'where' yan tümcesi hello kaynak tabloları birinin her Bahsetme sonra eklenen bir özelliktir.

`ago(3d)`'üç gün önce' anlamına gelir. Diğer birimleri süreyi saat dahil et (`2h`, `2.5h`), dakika (`25m`) ve saniye (`10s`).

Diğer örnekler:

```AIQL

    // Last calendar week:
    requests
    | where timestamp > startofweek(now()-7d)
        and timestamp < startofweek(now())
    | top 5 by duration

    // First hour of every day in past seven days:
    requests
    | where timestamp > ago(7d) and timestamp % 1d < 1h
    | top 5 by duration

    // Specific dates:
    requests
    | where timestamp > datetime(2016-11-19) and timestamp < datetime(2016-11-21)
    | top 5 by duration

```

[Tarihler ve saatlere başvuru](https://docs.loganalytics.io/concepts/concepts_datatypes_datetime.html).


## <a name="projecthttpsdocsloganalyticsioquerylanguagequerylanguageprojectoperatorhtml-select-rename-and-compute-columns"></a>[Proje](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html): sütunları işlem seçin ve yeniden adlandırma
Kullanım [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) toopick istediğiniz hello sütun çıkışı:

```AIQL

    requests | top 10 by timestamp desc
             | project timestamp, name, resultCode
```

![](./media/app-insights-analytics-tour/240.png)

Sütunları yeniden adlandırın ve yenilerini tanımlayın:

```AIQL

    requests
    | top 10 by timestamp desc
    | project  
            name,
            response = resultCode,
            timestamp,
            ['time of day'] = floor(timestamp % 1d, 1s)
```

![Sonuç](./media/app-insights-analytics-tour/270.png)

* Sütun adları, boşluk içerebilir veya bunlar köşeli parantez içindeki, simgeler şöyle: `['...']` veya`["..."]`
* `%`Merhaba modulo işleci normal ' dir.
* `1d`(bir basamak biri olan sonra bir 'D ') bir timespan değişmez değer bir gün anlamına gelir. Daha fazla bazı timespan değişmez değerler şunlardır: `12h`, `30m`, `10s`, `0.01s`.
* `floor`(diğer ad `bin`) bir değer birden çok sağladığınız hello taban değeri en yakın toohello aşağı yuvarlar. Bu nedenle `floor(aTime, 1s)` birer ikinci en yakın toohello aşağı yuvarlar.

İfadeler, tüm hello normal işleçleri içerebilir (`+`, `-`,...), ve bir dizi kullanışlı işlevi yoktur.

## <a name="extend"></a>Genişletme
Yalnızca var olanları tooadd sütunları toohello istiyorsanız, kullanmak [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html):

```AIQL

    requests
    | top 10 by timestamp desc
    | extend timeOfDay = floor(timestamp % 1d, 1s)
```

Kullanarak [ `extend` ](https://docs.loganalytics.io/queryLanguage/query_language_extendoperator.html) daha az ayrıntılıdır [ `project` ](https://docs.loganalytics.io/queryLanguage/query_language_projectoperator.html) tookeep istiyorsanız tüm var olan sütunlar hello.

### <a name="convert-toolocal-time"></a>Toolocal zaman Dönüştür

Zaman damgaları her zaman UTC biçimindedir. Bu nedenle hello BİZE Pasifik Yakası üzerinde olduğunuz ve Kış ise, bu istediğiniz:

```AIQL

    requests
    | top 10 by timestamp desc
    | extend localTime = timestamp - 8h
```


## <a name="summarizehttpsdocsloganalyticsioquerylanguagequerylanguagesummarizeoperatorhtml-aggregate-groups-of-rows"></a>[Özetlemek](https://docs.loganalytics.io/queryLanguage/query_language_summarizeoperator.html): toplam satır grupları
`Summarize`Belirtilen bir geçerlidir *toplama işlevi* satır grupları üzerinden.

Örneğin, web uygulamanızı toorespond tooa isteği hello süresini hello alanında bildirilir `duration`. Görelim hello ortalama yanıt süresi tooall istekleri:

![](./media/app-insights-analytics-tour/410.png)

Veya biz hello sonuç farklı adlar istekleri ayrı:

![](./media/app-insights-analytics-tour/420.png)

`Summarize`toplar hangi hello için gruplar halinde veri noktaları hello akışında hello `by` yan tümcesi eşit olarak değerlendirir. Merhaba yer alan her değerin `by` ifade - her işlem adı örnek yukarıda hello - hello sonuç tablosunda bir satırı sonuçlanıyor.

Veya sonuçları günün saatini göre gruplandırabilirsiniz:

![](./media/app-insights-analytics-tour/430.png)

Biz hello nasıl kullanmakta olduğunuz fark `bin` işlevi (diğer adıyla `floor`). Yalnızca kullansaydık `by timestamp`, kendi az grubunda her giriş satır yapmış olursunuz. Sürekli bir skaler için LIKE kez veya numaraları toobreak hello sürekli aralığına ayrık değerler yönetilebilir bir dizi sunuyoruz. `bin`-yalnızca hello tanıdık yuvarlama aşağı olduğu `floor` işlev - hello en kolay yolu toodo olduğundan.

Biz kullanabilirsiniz hello dizeleri aynı teknik tooreduce aralığı:

![](./media/app-insights-analytics-tour/440.png)

Kullanabileceğiniz bildirimi `name=` hello toplama ifadeleri veya hello tarafından yan tümcesi bir sonuç sütunu tooset hello adı.

## <a name="counting-sampled-data"></a>Sayım örneklenen verileri
`sum(itemCount)`Merhaba toocount olaylarını toplama önerilen olur. Çoğu durumda, ItemCount hello işlevi yalnızca hello hello Grup satır sayısı yukarı sayar şekilde == 1. Ancak zaman [örnekleme](app-insights-sampling.md) olan işleminde, yalnızca bir kesir hello özgün olayların korunur Application ınsights'ta veri noktaları olarak gördüğünüz her veri noktası için vardır; böylece `itemCount` olaylar.

Örnekleme %75 hello özgün olayları, daha sonra ItemCount atar, örneğin, == 4 korunur hello kayıtlarında - diğer bir deyişle, tutulan her kayıt için vardı dört özgün kaydeder.

Uyarlamalı örnekleme ItemCount toobe uygulamanızı ağırlıklı olarak ne zaman kullanıldığını dönemlerde yüksek neden olur.

ItemCount birleşimi, bu nedenle hello özgün olay sayısı için iyi bir gösterge sağlar.

![](./media/app-insights-analytics-tour/510.png)

Ayrıca bir `count()` toplama (ve sayısı işlemi) durumlarda gerçekten istediğiniz toocount hello bir grup satır sayısı.

Bir dizi var. [toplama işlevleri](https://docs.loganalytics.io/learn/tutorials/aggregations.html).

## <a name="charting-hello-results"></a>Grafik hello sonuçları
```AIQL

    exceptions
       | summarize count=sum(itemCount)  
         by bin(timestamp, 1h)
```

Varsayılan olarak bir tablo olarak sonuçları görüntülenir:

![](./media/app-insights-analytics-tour/225.png)

Merhaba Tablo görünümü daha iyi yapabileceğimiz. Merhaba Grafik görünümünde hello sonuçlarını hello dikey çubuk seçeneğiyle bakalım:

![Grafiği tıklatın ardından dikey çubuk grafiği seçin ve ata x ve y eksenleri](./media/app-insights-analytics-tour/230.png)

Ancak dikkat edin (Merhaba Tablo görünümünde görebileceğiniz gibi) zamanına göre hello sonuçları biz sıralamak alamadık, hello grafik görüntüleme her zaman doğru sırayla tarih/saat gösterilir.


## <a name="timecharts"></a>Timecharts
Kaç tane var. her saat olaylardır göster:

```AIQL

    requests
      | summarize event_count=sum(itemCount)
        by bin(timestamp, 1h)
```

Merhaba grafik görüntüleme seçeneği belirleyin:

![timechart](./media/app-insights-analytics-tour/080.png)

## <a name="multiple-series"></a>Birden fazla seri
Birden çok ifadelerinde hello `summarize` yan tümcesi birden çok sütun oluşturur.

Birden çok ifadelerinde hello `by` yan tümcesi her değer birleşimlerinde birden çok satır oluşturur.

```AIQL

    requests
    | summarize count_=sum(itemCount), avg(duration)
      by bin(timestamp, 1h), client_StateOrProvince, client_City
    | order by timestamp asc, client_StateOrProvince, client_City
```

![Saat ve konuma göre istekleri tablosu](./media/app-insights-analytics-tour/090.png)

### <a name="segment-a-chart-by-dimensions"></a>Bir grafik boyutlara göre bölme
Bir dize sütunu ve hello dize sayısal bir sütun içeren bir tablo grafik kullanılan toosplit hello sayısal veri noktalarını ayrı bir dizi olabiliyorsa. Birden çok dize sütunu ise, hangi sütunun toouse hello ayrıştırıcı seçebilirsiniz.

![Bir analiz grafik segment](./media/app-insights-analytics-tour/100.png)

#### <a name="bounce-rate"></a>Oranı sıçrama

Boolean tooa dize toouse Dönüştür bir Ayrıştırıcıyı olarak:

```AIQL

    // Bounce rate: sessions with only one page view
    requests
    | where notempty(session_Id)
    | where tostring(operation_SyntheticSource) == "" // real users
    | summarize pagesInSession=sum(itemCount), sessionEnd=max(timestamp)
               by session_Id
    | extend isbounce= pagesInSession == 1
    | summarize count()
               by tostring(isbounce), bin (sessionEnd, 1h)
    | render timechart
```

### <a name="display-multiple-metrics"></a>Birden çok ölçümleri görüntüleme
Birden fazla sayısal sütun eklenmesi toohello zaman damgasına sahip bir tablo grafik herhangi bir bileşimini görüntüleyebilirsiniz.

![Bir analiz grafik segment](./media/app-insights-analytics-tour/110.png)

Seçmelisiniz **yok bölünmüş** birden çok sayısal sütunlar seçebilmeniz için önce. Bir dize sütunu hello tarafından aynı bölünemez birden fazla sayısal sütun görüntüleme olarak zaman.

## <a name="daily-average-cycle"></a>Günlük ortalama döngüsü
Kullanım ortalama bir günün hello nasıl değişiyor?

Saate binned sayısı istekler, bir gün modulo hello zamana göre:

```AIQL

    requests
    | where timestamp > ago(30d)  // Override "Last 24h"
    | where tostring(operation_SyntheticSource) == "" // real users
    | extend hour = bin(timestamp % 1d , 1h)
          + datetime("2016-01-01") // Allow render on line chart
    | summarize event_count=sum(itemCount) by hour
```

![Saat cinsinden ortalama bir günün çizgi grafiği](./media/app-insights-analytics-tour/120.png)

> [!NOTE]
> Biz şu anda tooconvert zaman süreleri toodatetimes sipariş toodisplay üzerinde bir çizgi grafiği özen gösterin.
>
>

## <a name="compare-multiple-daily-series"></a>Birden fazla günlük seri Karşılaştır
Nasıl kullanım günü hello zaman içinde farklı ülkelerde değişiyor mu?

```AIQL

     requests  
     | where timestamp > ago(30d)  // Override "Last 24h"
     | where tostring(operation_SyntheticSource) == "" // real users
     | extend hour= floor( timestamp % 1d , 1h)
           + datetime("2001-01-01")
     | summarize event_count=sum(itemCount)
       by hour, client_CountryOrRegion
     | render timechart
```

![Bölünmüş tarafından client_CountryOrRegion](./media/app-insights-analytics-tour/130.png)

## <a name="plot-a-distribution"></a>Bir dağıtım Çiz
Kaç tane oturumları vardır, farklı uzunlukta?

```AIQL

    requests
    | where timestamp > ago(30d) // override "Last 24h"
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id
    | extend sessionDuration = max_timestamp - min_timestamp
    | where sessionDuration > 1s and sessionDuration < 3m
    | summarize count() by floor(sessionDuration, 3s)
    | project d = sessionDuration + datetime("2016-01-01"), count_
```

Merhaba son gerekli tooconvert toodatetime satırdır. Şu anda yalnızca bir datetime ise bir grafiğin hello x ekseninin skaler görüntülenir.

Merhaba `where` yan tümcesi dışlar tek adımda oturumları (sessionDuration == 0) ve ayarlar hello hello x ekseni uzunluğu.

![](./media/app-insights-analytics-tour/290.png)

## <a name="percentileshttpsdocsloganalyticsioquerylanguagequerylanguagepercentilesaggfunctionhtml"></a>[Yüzdebirlik değeri](https://docs.loganalytics.io/queryLanguage/query_language_percentiles_aggfunction.html)
Hangi süreleri aralıklarına oturumları farklı yüzdelerini kapak?

Sorgu yukarıda Hello kullanır, ancak hello son satırı değiştirin:

```AIQL

    requests
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id
    | extend sesh = max_timestamp - min_timestamp
    | where sesh > 1s
    | summarize count() by floor(sesh, 3s)
    | summarize percentiles(sesh, 5, 20, 50, 80, 95)
```

Biz de hello üst sınırı burada tümcesinde sipariş tooget düzeltmek birden fazla isteği ile tüm oturumları dahil olmak üzere rakamları hello kaldırıldı:

![Sonuç](./media/app-insights-analytics-tour/180.png)

İçinden biz görebilirsiniz:

* %5 oturumlarının 3 dakikadan 34s daha kısa bir süre; yine de sahip istiyor musunuz?
* Son 36 dakikadan az %50 oturumlarının;
* 7 günden fazla %5 oturumlarının son

tooget her ülke için ayrı bir çözümleme, biz yalnızca toobring hello client_CountryOrRegion sütunu işleçleri özetlemek ayrı ayrı her ikisi de aracılığıyla vardır:

```AIQL

    requests
    | where isnotnull(session_Id) and isnotempty(session_Id)
    | summarize min(timestamp), max(timestamp)
      by session_Id, client_CountryOrRegion
    | extend sesh = max_timestamp - min_timestamp
    | where sesh > 1s
    | summarize count() by floor(sesh, 3s), client_CountryOrRegion
    | summarize percentiles(sesh, 5, 20, 50, 80, 95)
      by client_CountryOrRegion
```

![](./media/app-insights-analytics-tour/190.png)

## <a name="join"></a>Birleştir
Erişim tooseveral tabloları, istekler ve özel durumlar dahil olmak üzere sunuyoruz.

hata yanıtını döndürülen toofind hello özel durumlar ilgili tooa isteği, biz katılmayı hello tabloları `session_Id`:

```AIQL

    requests
    | where toint(resultCode) >= 500
    | join (exceptions) on operation_Id
    | take 30
```


İyi bir uygulama toouse olan `project` ihtiyacımız gerçekleştirmeden önce tooselect yalnızca hello sütunları hello birleştirme.
Merhaba, aynı yan tümceleri, biz hello zaman damgası sütunu yeniden adlandırın.

## <a name="lethttpsdocsloganalyticsioquerylanguagequerylanguageletstatementhtml-assign-a-result-tooa-variable"></a>[Let](https://docs.loganalytics.io/queryLanguage/query_language_letstatement.html): sonuç tooa değişkeni atayın

Kullanım `let` tooseparate hello önceki ifade hello bölümlerini çıkışı. Merhaba sonuçları aynıdır:

```AIQL

    let bad_requests =
      requests
        | where  toint(resultCode) >= 500  ;
    bad_requests
    | join (exceptions) on session_Id
    | take 30
```

> [!Tip] 
> Merhaba Analytics istemcisinde hello hello sorgunun bölümlerini arasında boş satırlar koymayın. Emin tooexecute tamamını yapın.
>

Kullanım `toscalar` tooconvert tek tablo hücre tooa değeri:

```AIQL
let topCities =  toscalar (
   requests
   | summarize count() by client_City 
   | top n by count_ 
   | summarize makeset(client_City));
requests
| where client_City in (topCities(3)) 
| summarize count() by client_City;
```


### <a name="functions"></a>İşlevler

Kullanım *izin* toodefine bir işlev:

```AIQL

    let usdate = (t:datetime)
    {
      strcat(getmonth(t), "/", dayofmonth(t),"/", getyear(t), " ",
      bin((t-1h)%12h+1h,1s), iff(t%24h<12h, "AM", "PM"))
    };
    requests  
    | extend PST = usdate(timestamp-8h)
```

## <a name="accessing-nested-objects"></a>İç içe geçmiş nesnelere erişme
İç içe geçmiş nesnelerde kolayca erişilebilir. Örneğin, hello özel durumlar akışında yapılandırılmış nesneleri bu gibi görebilirsiniz:

![Sonuç](./media/app-insights-analytics-tour/520.png)

İlgilendiğiniz hello özellikleri seçerek düzleştirmek:

```AIQL

    exceptions | take 10
    | extend method1 = tostring(details[0].parsedStack[1].method)
```

Toocast hello sonuç toohello uygun türü gerektiğini unutmayın.


## <a name="custom-properties-and-measurements"></a>Özel özellikler ve ölçümler
Uygulamanızı bağlanıyorsa [özel boyutları (Özellikler) ve özel ölçümleri](app-insights-api-custom-events-metrics.md#properties) tooevents, ardından görürsünüz: bunları hello `customDimensions` ve `customMeasurements` nesneleri.

Örneğin, uygulamanızın içeriyorsa:

```C#

    var dimensions = new Dictionary<string, string>
                     {{"p1", "v1"},{"p2", "v2"}};
    var measurements = new Dictionary<string, double>
                     {{"m1", 42.0}, {"m2", 43.2}};
    telemetryClient.TrackEvent("myEvent", dimensions, measurements);
```

tooextract Analytics bu değerleri:

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      m1 = todouble(customMeasurements.m1) // cast tooexpected type

```

tooverify Özel boyut belirli bir tür olup:

```AIQL

    customEvents
    | extend p1 = customDimensions.p1,
      iff(notnull(todouble(customMeasurements.m1)), ...
```

## <a name="dashboards"></a>Panolar
Sonuçları tooa Panonuzda sipariş toobring birlikte, en önemli grafikler ve tablolar sabitleyebilirsiniz.

* [Azure paylaşılan Pano](app-insights-dashboards.md#share-dashboards): hello PIN simgesine tıklayın. Bunu, bir paylaşılan Pano sahip olmanız gerekir. Hello Azure portal, açın veya bir pano oluşturun ve Paylaşım'ı tıklatın.
* [Power BI panosuna](app-insights-export-power-bi.md): tıklatın verme, Power BI sorgu. Bu alternatif bir avantajı, çok çeşitli diğer sonuçlarından kaynakları yanında sorgunuzu görüntüleyebilirsiniz ' dir.

## <a name="combine-with-imported-data"></a>İçeri aktarılan verilerle birleştirin

Analytics Raporları hello Panoda harika bakın, ancak bazen daha fazla digestible form tootranslate hello veri tooa istiyor. Örneğin, bir diğer ad tarafından tanımlanan, kimliği doğrulanmış kullanıcılar hello telemetri varsayalım. Sonuç olarak, gerçek adlarını tooshow ister. toodo bunu hello diğer adlar toohello gerçek adlarını eşleyen bir CSV dosyası gerekir.

Bir veri dosyasını içeri aktarın ve gibi hello standart tablolardan (istekleri, özel durumlar ve benzeri) herhangi birini kullanın. Bu, kendi sorgulamak ya da diğer tablolarla katılın. Örneğin, usermap adlı bir tablo varsa ve sütunları içeren `realName` ve `userId`, tootranslate hello kullanmayı `user_AuthenticatedId` hello isteği telemetri alanındaki:

```AIQL

    requests
    | where notempty(user_AuthenticatedId)
    | project userId = user_AuthenticatedId
      // get hello realName field from hello usermap table:
    | join kind=leftouter ( usermap ) on userId
      // count transactions by name:
    | summarize count() by realName
```

tooimport hello şema dikey penceresinde, bir tablo altında **diğer veri kaynakları**, örnek verileriniz yükleyerek hello yönergeleri tooadd yeni bir veri kaynağı izleyin. Ardından bu tanımı tooupload tabloları kullanabilir.

"Diğer veri kaynakları." altında "bize başvurun" Bağlantı başlangıçta göreceğiniz şekilde hello içe aktar özelliği şu anda önizlemede, değil Merhaba bağlantı sonra bir "yeni veri kaynağı Ekle" düğmesi tarafından değiştirilir ve bu toosign toohello Önizleme programı kullanın.


## <a name="tables"></a>Tablolar
Merhaba, uygulamanızdan alınan telemetri çeşitli tablolara erişilebilir akışıdır. Her tablo için kullanılabilen özellikleri Hello şeması hello penceresinde hello sol tarafında görünür olur.

### <a name="requests-table"></a>İstekler tablosu
Count HTTP istekleri tooyour web app ve kesim tarafından sayfa adı:

![Ada göre kesimli sayısı istekleri](./media/app-insights-analytics-tour/analytics-count-requests.png)

Çoğu başarısız hello istekleri Bul:

![Ada göre kesimli sayısı istekleri](./media/app-insights-analytics-tour/analytics-failed-requests.png)

### <a name="custom-events-table"></a>Özel olaylar tablo
Kullanırsanız [TrackEvent()](app-insights-api-custom-events-metrics.md#trackevent) toosend kendi olayları bu tablodan okuyabilirsiniz.

Bu satırlar, uygulama kodunuzun içerdiği bir örnek atalım:

```C#

    telemetry.TrackEvent("Query",
       new Dictionary<string,string> {{"query", sqlCmd}},
       new Dictionary<string,double> {
           {"retry", retryCount},
           {"querytime", totalTime}})
```

Bu olaylar Hello sıklığını görüntüle:

![Özel olaylar görüntü oranı](./media/app-insights-analytics-tour/analytics-custom-events-rate.png)

Ölçüleri ve boyutları hello olaylarından ayıklayın:

![Özel olaylar görüntü oranı](./media/app-insights-analytics-tour/analytics-custom-events-dimensions.png)

### <a name="custom-metrics-table"></a>Özel ölçümleri tablosu
Kullanıyorsanız [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) toosend ölçüm kendi değerlerinizi hello sonuçlarını bulacaksınız **customMetrics** akış. Örneğin:  

![Application Insights analytics'te özel ölçümleri](./media/app-insights-analytics-tour/analytics-custom-metrics.png)

> [!NOTE]
> İçinde [ölçüm Gezgini](app-insights-metrics-explorer.md), ekli tooany türüne telemetri görünür birlikte hello ölçümleri dikey kullanılarak gönderilen ölçümleri yanı sıra tüm özel ölçümleri `TrackMetric()`. Ancak, analizleri özel ölçümleri hala bunlar taşınan - olayları veya istekleri vb. - TrackMetric tarafından gönderilen ölçümleri kendi akışında görünürken telemetri toowhichever türü bağlı.
>
>

### <a name="performance-counters-table"></a>Performans sayaçları tablosu
[Performans sayaçları](app-insights-performance-counters.md) ve ağ kullanımı gibi CPU, bellek, uygulamanız için temel sistem ölçümleri gösterilmektedir. Kendi özel sayaçlar dahil hello SDK toosend ek sayaçları, yapılandırabilirsiniz.

Merhaba **performanceCounters** şeması sunan hello `category`, `counter` adı ve `instance` her performans sayacı adı. Sayaç örneği adları yalnızca geçerli toosome performans sayaçları ve genellikle hello işlem toowhich hello sayısı hello adını ilişkili gösterir. Telemetri Hello her uygulama için yalnızca bu uygulama için hello sayaçları görürsünüz. Örneğin, toosee hangi sayaçları kullanılabilir:

![Application Insights analytics performans sayaçları](./media/app-insights-analytics-tour/analytics-performance-counters.png)

Seçilen dönemi tooget hello üzerinden kullanılabilir belleğin bir grafik:

![Application Insights analytics'te bellek timechart](./media/app-insights-analytics-tour/analytics-available-memory.png)

Gibi diğer telemetri **performanceCounters** de bir sütuna sahip `cloud_RoleInstance` hello uygulamanızı çalıştıran hello ana bilgisayar makine kimliğini gösterir. Örneğin, toocompare hello uygulamanızın performansı ile Merhaba farklı makinelerde:

![Performans rol örneğinde Application Insights tarafından analiz bölümlenmiş.](./media/app-insights-analytics-tour/analytics-metrics-role-instance.png)

### <a name="exceptions-table"></a>Özel durumlar tablosu
[Özel durumlar, uygulamanız tarafından bildirilen](app-insights-asp-net-exceptions.md) bu tabloda kullanılabilir.

toofind hello özel durumu oluştu, uygulamanızın işleme HTTP isteği Merhaba, üzerinde operation_Id Katıl:

![Özel durumlar isteklerle operation_Id üzerinde katılma](./media/app-insights-analytics-tour/analytics-exception-request.png)

### <a name="browser-timings-table"></a>Tarayıcı zamanlamaları tablosu
`browserTimings`Kullanıcılarınızın tarayıcılarda toplanan sayfa yükleme verileri gösterir.

[İstemci tarafı telemetri için uygulamanızı ayarlayın](app-insights-javascript.md) içinde bu ölçümleri toosee sipariş.

Merhaba şeması içerir [hello uzunlukları hello sayfa yükleme işlemi farklı aşaması gösteren ölçümleri](app-insights-javascript.md#page-load-performance). (Bunlar hello süreyi kullanıcılarınızın bir sayfa okuma göstermediği.)  

Merhaba popularities farklı sayfaların göstermek ve her bir sayfa için zamanları yük:

![Sayfa yükleme sürelerinin analytics'te](./media/app-insights-analytics-tour/analytics-page-load.png)

### <a name="availability-results-table"></a>Kullanılabilirlik sonuçları tablosu
`availabilityResults`Merhaba sonuçlarını gösterir, [web testleri](app-insights-monitor-web-app-availability.md). Her çalışma testlerinizin her test konumdan ayrı olarak bildirilir.

![Sayfa yükleme sürelerinin analytics'te](./media/app-insights-analytics-tour/analytics-availability.png)

### <a name="dependencies-table"></a>Bağımlılıklar tablosu
Arama sonuçlarını içeren uygulamanızı toodatabases ve REST API'leri ve diğer yapar tooTrackDependency() çağırır. Ayrıca hello tarayıcıdan oluşturulan AJAX çağrıları içerir.

AJAX çağrıları hello tarayıcısından:

```AIQL

    dependencies | where client_Type == "Browser"
    | take 10
```

Bağımlılık çağrıları hello sunucusundan:

```AIQL

    dependencies | where client_Type == "PC"
    | take 10
```

Sunucu tarafı bağımlılık sonuçları her zaman göster `success==False` Merhaba, Application Insights aracısı yüklü değil. Ancak, hello diğer verileri doğru değildir.

### <a name="traces-table"></a>İzlemeler tablosu
Merhaba telemetri TrackTrace(), kullanma, uygulamanız tarafından gönderilen içerir veya [başka günlük altyapılarına](app-insights-asp-net-trace-logs.md).

## <a name="video"></a>Video 

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/123/player] 

Gelişmiş sorgular:

> [!VIDEO https://channel9.msdn.com/Events/Build/2016/P591/player]


## <a name="next-steps"></a>Sonraki adımlar
* [Analytics dil başvurusu](app-insights-analytics-reference.md)
* [SQL-kullanıcıların kopya sayfası](https://aka.ms/sql-analytics) hello en yaygın deyimleri çevirir.

[!INCLUDE [app-insights-analytics-footer](../../includes/app-insights-analytics-footer.md)]
