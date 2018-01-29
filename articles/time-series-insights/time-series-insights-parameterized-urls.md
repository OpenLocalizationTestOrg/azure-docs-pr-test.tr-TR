---
title: "Parametreli URL'lerle Azure Time Series Insights özel görünümlerini paylaşma | Microsoft Docs"
description: "Bu makalede, özelleştirilmiş görünümün kolayca paylaşılabilmesi için Azure Time Series Insights'ta parametreli URL'lerin nasıl geliştirileceği açıklanır."
services: time-series-insights
ms.service: time-series-insights
author: MarkMcGeeAtAquent
ms.author: MarkMcGeeAtAquent
manager: jhubbard
editor: MicrosoftDocs/tsidocs
ms.reviewer: v-mamcge, jasonh, kfile, anshan
ms.devlang: rest-api
ms.topic: get-started-article
ms.workload: big-data
ms.date: 11/21/2017
ms.openlocfilehash: b7c58697323ec12ac08575916cb3ac5b38cc39c1
ms.sourcegitcommit: b5c6197f997aa6858f420302d375896360dd7ceb
ms.translationtype: HT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/21/2017
---
# <a name="share-a-custom-view-using-a-parameterized-url"></a>Parametreli URL'yi kullanarak özel görünümü paylaşma

Time Series Insights gezgininde özel bir görünümü paylaşmak için, programlama yoluyla özel görünümün parametreli bir URL'sini oluşturabilirsiniz.

Time Series Insights gezgini, doğrudan URL'den gerçekleştirilen bir deneyimde görünümleri belirtmek için URL sorgu parametrelerinin kullanımını destekler.  Örneğin, yalnızca URL'yi kullanarak hedef ortamı, arama koşulunu ve istenen zaman aralığını belirtebilirsiniz. Kullanıcı özelleştirilmiş URL'ye tıkladığında, arabirim Time Series Insights portalında doğrudan bu varlığın bağlantısını sağlar.  Veri erişimi ilkeleri uygulanır. 

## <a name="environment-id"></a>Ortam Kimliği

`environmentId=<guid>` parametresi hedef ortam kimliğini belirtir.  Bu, veri erişim FQDN'sinin bir bileşenidir ve bunu Azure Portal'da, ortama genel bakışın sağ üst köşesinde bulabilirsiniz.  `env.timeseries.azure.com` bölümünden önce gelen her şey, bu değeri oluşturur. Örnek bir ortam kimliği parametresi olarak `?environmentId=10000000-0000-0000-0000-100000000108` verilebilir.

## <a name="time"></a>Zaman

Parametreli URL ile mutlak veya göreli zaman değerleri belirtebilirsiniz.

### <a name="absolute-time-values"></a>Mutlak zaman değerleri

Mutlak zaman değerleri için, `from=<integer>` ve `to=<integer>` parametrelerini kullanın. 

`from=<integer>`, arama aralığının başlangıç zamanını gösteren JavaScript milisaniyesi cinsinden bir değerdir.

`to=<integer>`, arama aralığının bitiş zamanını gösteren JavaScript milisaniyesi cinsinden bir değerdir. 

Tarihe ilişkin JavaScript milisaniyesini belirlemek için bkz. [Epoch ve Unix Zaman Damgası Dönüştürücüsü](https://www.freeformatter.com/epoch-timestamp-to-date-converter.html).

### <a name="relative-time-values"></a>Göreli zaman değerleri

Göreli bir zaman değeri için `relativeMillis=<value>` kullanın; burada *değer*, arka uçtaki en son verilerden gelen JavaScript milisaniyesi cinsinden bir değerdir.

Örneğin, `&relativeMillis=3600000` en 60 dakikanın verilerini görüntüler.

Kabul edilen değerler, Time Series Insights gezgininin **kısa süre** menüsüne karşılık gelir ve şunları içerir:

- 1800000 (Son 30 Dakika)
- 3600000 (Son 60 Dakika)
- 10800000 (Son 3 Saat)
- 21600000 (Son 6 Saat)
- 43200000 (Son 12 Saat)
- 86400000 (Son 24 Saat)
- 604800000 (Son 7 Gün)
- 2592000000 (Son 30 Gün)

### <a name="optional-parameters"></a>İsteğe bağlı parametreler

`timeSeriesDefinitions=<collection of term objects>` parametresi Time Series Insights görünümünün dönemlerini belirtir; burada:

- `name=<string>`
  - *Dönem* adı.
- `splitBy=<string>`
  - *Bölme ölçütü* sütunun adı.
- `measureName=<string>`
  - *Ölçü* sütununun adı.
- `predicate=<string>`
  - Sunucu tarafı filtrelemesi için *where* yan tümcesi.

'multiChartStack=<true/false>' parametresi grafikte yığın oluşturmayı sağlar, 'multiChartSameScale=<true/false>' parametresi ise isteğe bağlı bir parametre içindeki terimler arasında aynı Y ekseni ölçeğini sağlar.  

- 'multiChartStack=false'
  - 'True' varsayılan olarak etkindir, bu nedenle yığına 'false' değerini geçirin.
- 'multiChartStack=false&multiChartSameScale=true' 
  - Terimler arasında aynı Y ekseni ölçeğini kullanmak için yığın oluşturmanın etkinleştirilmesi gerekir.  Varsayılan olarak 'false' olduğu için, 'true' değerinin geçirilmesi bu işlevi etkinleştirir.  
  
'timeBucketUnit=<Unit>&timeBucketSize=<integer>' parametresi, aralık kaydırıcısını daha ayrıntılı veya düz, daha toplu bir grafik görünümüne ayarlamanızı sağlar.  
- 'timeBucketUnit=<Unit>&timeBucketSize=<integer>'
  - Birimler = gün, saat, dakika, saniye, milisaniye.  Her zaman birimin ilk harfini büyük yapın.
  - timeBucketSize için istediğiniz tamsayıyı geçererek birim sayısını tanımlayın.  En fazla 7 güne kadar düzleştirebilirsiniz.  
  
'timezoneOffset=<integer>' parametresi, grafiğin UTC’ye uzaklık cinsinden görüntülenecek saat dilimini ayarlamanızı sağlar.  
  - 'timezoneOffset=-<integer>'
    - Bu tamsayı her zaman milisaniye cinsindendir.  
    - Bu işlevsellik, TSI gezgininde etkinleştirdiğimiz ve yerel (tarayıcı saati) ya da UTC saat dilimini seçmenize olanak tanıdığımız işlevden biraz farklıdır.  
 
### <a name="examples"></a>Örnekler

Örneğin, URL parametresi olarak zaman serisi tanımları eklemek için aşağıdakini kullanabilirsiniz:

```https
&timeSeriesDefinitions=[{"name":"F1PressureId","splitBy":"Id","measureName":"Pressure","predicate":"'Factory1'"},{"name":"F2TempStation","splitBy":"Station","measureName":"Temperature","predicate":"'Factory2'"},
{"name":"F3VibrationPL","splitBy":"ProductionLine","measureName":"Vibration","predicate":"'Factory3'"}]
```

Şunlara yönelik bu örnek zaman serisi tanımları 

- Ortam Kimliği
- Son 60 dakikalık veriler
- dönemler (F1PressureID, F2TempStation, and F3VibrationPL), isteğe bağlı parametreleri oluşturur
 
ve bunları kullanarak görünüm için aşağıdaki parametreli URL'yi oluşturabilirsiniz:

```https
https://insights.timeseries.azure.com/samples?environmentId=10000000-0000-0000-0000-100000000108&relativeMillis=3600000&timeSeriesDefinitions=[{"name":"F1PressureId","splitBy":"Id","measureName":"Pressure","predicate":"'Factory1'"},{"name":"F2TempStation","splitBy":"Station","measureName":"Temperature","predicate":"'Factory2'"},{"name":"F3VibrationPL","splitBy":"ProductionLine","measureName":"Vibration","predicate":"'Factory3'"}]
```

Önceki URL'de açıklanan görünümü oluşturmak için Time Series Insights gezginini kullansaydınız, şöyle görünürdü:

![Time Series Insights gezgini Dönemler](media/parameterized-url/url1.png)

Tam görünüm (grafik dahil) şöyle olurdu:

![Grafik görünümü](media/parameterized-url/url2.png)

## <a name="next-steps"></a>Sonraki adımlar
[C# kullanarak verileri sorgulama](time-series-insights-query-data-csharp.md)
