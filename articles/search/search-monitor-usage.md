---
title: "aaaMonitor kullanım ve Azure Search hizmeti istatistikleri | Microsoft Docs"
description: "Azure arama, Microsoft Azure üzerinde barındırılan bulut arama hizmeti için kaynak kullanım ve dizin boyutu izler."
services: search
documentationcenter: 
author: bernitorres
manager: jlembicz
editor: 
tags: azure-portal
ms.assetid: 122948de-d29a-426e-88b4-58cbcee4bc23
ms.service: search
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 05/01/2017
ms.author: betorres
ms.openlocfilehash: f38eabb5d04a410e11eaaff22157da8aba9e4845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-an-azure-search-service"></a>Azure Search Hizmeti izleme

Azure arama, kullanım ve arama hizmetleri performansını izleme için çeşitli kaynaklar sunar. Size verir erişim toometrics, günlükleri, dizin istatistikleri ve Power BI üzerinde genişletilmiş izleme yetenekleri. Bu makalede nasıl tooenable hello farklı izleme stratejileri ve nasıl toointerpret hello sonuç verileri açıklanmaktadır.

## <a name="azure-search-metrics"></a>Azure arama ölçütleri
Ölçümleri arama hizmetinizi gerçek zamanlı görünürlük yakın verin ve hiçbir ek ayar ile her hizmet için kullanılabilir. Bunlar, hizmetiniz için too30 günlerini hello performansını izlemenize olanak tanır.

Azure arama için üç farklı ölçüm verilerini toplar:

* Arama gecikme süresi: zaman hello arama hizmeti tooprocess arama sorguları, dakikada bir araya getirilir.
* Arama sorguları (QPS) saniyede: arama sayısını saniye başına alınan sorguları dakikada bir araya getirilir.
* Daraltılmış arama sorguları yüzdesi: kısıtlanan arama sorguları yüzdesi dakikada bir araya getirilir.

![Ekran görüntüsü, QPS etkinliği][1]

### <a name="set-up-alerts"></a>Uyarıları ayarlayın
Ölçüm tanımladığınız bir eşik kestiği hello ölçüm ayrıntı sayfasından uyarıları tootrigger bir e-posta bildirimi veya otomatik bir eylemi yapılandırabilirsiniz.

Ölçümler hakkında daha fazla bilgi için Azure monitörde hello tam belgelerine bakın.  

## <a name="how-tootrack-resource-usage"></a>Nasıl tootrack kaynak kullanımı
Merhaba büyümesi dizinler ve belge boyutu izleme proaktif olarak hello üst sınırı hizmetiniz için belirlediğinize göre basarsa önce kapasite ayarlamanıza yardımcı olabilir. Merhaba portalı veya program aracılığıyla hello REST API kullanarak bunu yapabilirsiniz.

### <a name="using-hello-portal"></a>Merhaba portal kullanma

toomonitor kaynak kullanımı, hello hello sayısı ve hizmetiniz için istatistikleri görüntüleyin [portal](https://portal.azure.com).

1. İçinde toohello oturum [portal](https://portal.azure.com).
2. Hello Azure Search hizmetinizin hizmet panosunu açın. Merhaba hizmet döşeme hello giriş sayfasında bulunabilir veya Gözat toohello hizmetinden hello atlama çubuğu üzerinde göz atabilirsiniz.

Hello kullanımı bölümü hangi kullanılabilir kaynakları bölümündedir şu anda kullanımda söyleyen bir ölçüm içerir. Dizinleri, belgeler ve depolama için başına hizmet sınırları hakkında daha fazla bilgi için bkz: [hizmet sınırları](search-limits-quotas-capacity.md).

  ![Kullanımı kutucuğu][2]

> [!NOTE]
> Yukarıdaki Hello ekran görüntüsü bir çoğaltma maksimum vardır ve her bölüm ve yalnızca konak 3 dizinleri, 10.000 belgeler veya veri 50 MB hello ücretsiz hizmeti için hangisi önce gelirse. Bir temel veya standart katmanını oluşturulan hizmetlerine çok daha büyük hizmet sınırları vardır. Bir katmanı seçme özelliği hakkında daha fazla bilgi için bkz: [bir katmanı SKU seçin veya](search-sku-tier.md).
>
>

### <a name="using-hello-rest-api"></a>Merhaba REST API kullanma
Hello Azure Search REST API'sini ve hello .NET SDK'sı programlı erişim tooservice ölçümleri sağlar.  Kullanıyorsanız [dizin oluşturucular](https://msdn.microsoft.com/library/azure/dn946891.aspx) tooload Azure SQL Database veya Azure Cosmos DB dizinden bir ek bir API olan kullanılabilir tooget hello numaraları gerektirir.

* [Dizin istatistikleri Al](/rest/api/searchservice/get-index-statistics)
* [Count belgeleri](/rest/api/searchservice/count-documents)
* [Dizin Oluşturucu durumunu Al](/rest/api/searchservice/get-indexer-status)

## <a name="how-tooexport-logs-and-metrics"></a>Nasıl tooexport ve ölçümleri

Hizmeti ve hello ham verileri hello önceki bölümde açıklanan hello ölçümünün hello işlem günlükleri dışarı aktarabilirsiniz. İşlem günlükleri size izin hello hizmetinin nasıl kullanıldığını ve veriler olduğunda Power BI'dan tüketilebilir tooa depolama hesabına kopyalanır. Azure arama bu amaç için bir izleme Power BI içerik paketi sağlar.


### <a name="enabling-monitoring"></a>İzlemeyi etkinleştirme
Azure Search Hizmeti hello [Azure portal](http://portal.azure.com) hello izlemesini etkinleştir seçeneği altında.

Merhaba veri seçin tooexport istediğiniz: günlükleri, ölçümleri veya her ikisi de. Tooa depolama hesabı kopyalama, tooan olay hub'ı göndermek veya tooLog Analytics verebilirsiniz.

![Nasıl tooenable hello Portalı'nda izleme][3]

PowerShell veya hello Azure CLI kullanarak tooenable hello belgelerine bakın [burada](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs#how-to-enable-collection-of-diagnostic-logs).

### <a name="logs-and-metrics-schemas"></a>Günlükleri ve ölçümleri şemaları
Merhaba veri kopyalanan tooa depolama olduğunda hesap, hello veri iki kapsayıcı JSON ve onun yerine olarak biçimlendirilmiş:

* Öngörüler günlükleri operationlogs: arama trafiği günlükleri
* Öngörüler ölçümleri pt1m: ölçümler için

Kapsayıcı başına saat başına bir blob yok.

Örnek yolu:`resourceId=/subscriptions/<subscriptionID>/resourcegroups/<resourceGroupName>/providers/microsoft.search/searchservices/<searchServiceName>/y=2015/m=12/d=25/h=01/m=00/name=PT1H.json`

#### <a name="log-schema"></a>Günlüğü şeması
Arama hizmeti trafik günlüklerinizi Hello günlükleri BLOB'ları içerir.
Her bir blob olarak adlandırılan bir kök nesnesi vardır **kayıtları** günlük nesnelerinin bir dizisi içerir.
Her bir blob hello sırasında gerçekleşen tüm hello işlemi üzerinde kayıtları sahip aynı saat.

| Ad | Tür | Örnek | Notlar |
| --- | --- | --- | --- |
| time |Tarih saat |"2015-12-07T00:00:43.6872559Z" |Merhaba işleminin zaman damgası |
| resourceId |Dize |"/ SUBSCRIPTIONS/11111111-1111-1111-1111-111111111111 /<br/>VARSAYILAN/RESOURCEGROUPS/SAĞLAYICILARI /<br/> MICROSOFT. ARAMA/SEARCHSERVICES/SEARCHSERVICE" |ResourceId |
| operationName |Dize |"Query.Search" |Merhaba işlemin Hello adı |
| operationVersion |Dize |"2015-02-28" |Merhaba API kullanılan sürüm |
| category |Dize |"OperationLogs" |sabiti |
| resultType |Dize |"Başarılı" |Olası değerler: başarı veya başarısızlık |
| resultSignature |Int |200 |HTTP Sonuç kodu |
| durationMS |Int |50 |Milisaniye cinsinden hello işlemi süresi |
| properties |Nesne |Aşağıdaki tablonun hello bakın |İşlemi özgü verileri içeren nesnesi |

**Özellik şeması**
| Ad | Tür | Örnek | Notlar |
| --- | --- | --- | --- |
| Açıklama |Dize |"/İndexes('content')/docs Al" |Merhaba işlemin uç noktası |
| Sorgu |Dize |"? arama = AzureSearch & $count = true & api-version = 2015-02-28" |Merhaba sorgu parametreleri |
| Belgeler |Int |42 |İşlenen belge sayısı |
| indexName |Dize |"testindex" |Merhaba işlemle ilişkili hello dizinin adı |

#### <a name="metrics-schema"></a>Ölçümleri şeması
| Ad | Tür | Örnek | Notlar |
| --- | --- | --- | --- |
| resourceId |Dize |"/ SUBSCRIPTIONS/11111111-1111-1111-1111-111111111111 /<br/>VARSAYILAN/RESOURCEGROUPS/SAĞLAYICILARI /<br/>MICROSOFT. ARAMA/SEARCHSERVICES/SEARCHSERVICE" |Kaynak Kimliği |
| metricName |Dize |"Gecikme" |Merhaba ölçüm Hello adı |
| time |Tarih saat |"2015-12-07T00:00:43.6872559Z" |Merhaba işlemin zaman damgası |
| Ortalama |Int |64 |Merhaba ortalama değer hello ölçüm zaman aralığında hello ham örnekleri |
| en az |Int |37 |Merhaba en düşük değer hello ölçüm zaman aralığında hello ham örnekleri |
| Maksimum |Int |78 |Merhaba en büyük değer hello ölçüm zaman aralığında hello ham örnekleri |
| Toplam |Int |258 |Merhaba toplam değeri hello ölçüm zaman aralığında hello ham örnekleri |
| Sayısı |Int |4 |Ham örnek Hello sayısı toogenerate hello metriği kullanılan |
| timegrain |Dize |"PT1M" |ISO 8601 hello ölçüsünün Hello zaman birimi |

Tüm ölçümlerini bir dakikalık aralıklarla raporlanır. Her ölçüm dakikada en az, en fazla ve ortalama değerleri gösterir.

Merhaba SearchQueriesPerSecond için en az bu dakikada kaydedildiği saniye başına arama sorguları için en düşük değer hello ölçümüdür. Merhaba aynı toohello en büyük değer geçerlidir. Merhaba toplama hello tüm üzerinde ortalama, dakikadır.
Bir dakika sırasında bu senaryoyu düşünün: iş yükünün hello SearchQueriesPerSecond için en yüksek olan yüksek bir saniye ardından 58 saniye ortalama iş yükünün ve son olarak yalnızca bir sorgu ile bir saniye olduğu hello en düşük.

ThrottledSearchQueriesPercentage için minimum, maksimum, ortalama ve toplam, tüm sahip hello aynı değeri: Merhaba, arama sorguları bir dakikada toplam sayıda hello kısıtlanan arama sorguları yüzdesi.

## <a name="analyzing-your-data-with-power-bi"></a>Power BI ile verilerinizi analiz etme

Kullanmanızı öneririz [Power BI](https://powerbi.microsoft.com) tooexplore ve verilerinizi görselleştirmenize. Kolayca tooyour Azure depolama hesabı bağlayın ve hızlı bir şekilde verilerinizi çözümlemeye başlayın.

Azure arama sağlayan bir [Power BI içerik paketi](https://app.powerbi.com/getdata/services/azure-search) toomonitor sağlar ve önceden tanımlanmış grafikler ve tablolar ile arama trafiğinizi anlama. Otomatik olarak tooyour veri bağlanmak ve arama hizmetinizi hakkında visual bilgiler Power BI raporları kümesi içerir. Daha fazla bilgi için bkz: Merhaba [içerik paketi Yardım sayfası](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-search/).

![Azure arama için Power BI Panosu][4]

## <a name="next-steps"></a>Sonraki adımlar
Gözden geçirme [ölçeklendirme çoğaltmaları ve bölümleri](search-limits-quotas-capacity.md) nasıl toobalance hello bölümler ve çoğaltmalar var olan bir hizmet için ayrılması konusunda yönergeler için.

Ziyaret [Microsoft azure'da Search hizmetinizi yönetme](search-manage.md) Hizmeti Yönetimi hakkında daha fazla bilgi için veya [performans ve en iyi duruma getirme](search-performance-optimization.md) Kılavuzu ayarlama.

Harika raporları oluşturma hakkında daha fazla bilgi edinin. Bkz: [Power BI Desktop ile çalışmaya başlama](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/) Ayrıntılar için

<!--Image references-->
[1]: ./media/search-monitor-usage/AzSearch-Monitor-BarChart.PNG
[2]: ./media/search-monitor-usage/AzureSearch-Monitor1.PNG
[3]: ./media/search-monitor-usage/AzureSearch-Enable-Monitoring.PNG
[4]: ./media/search-monitor-usage/AzureSearch-PowerBI-Dashboard.png
