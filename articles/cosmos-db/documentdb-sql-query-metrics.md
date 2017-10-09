---
title: "Azure Cosmos DB DocumentDB API için aaaSQL sorgu ölçümleri | Microsoft Docs"
description: "Nasıl tooinstrument ve hata ayıklama SQL sorgu performansını Azure Cosmos DB isteklerinin hello hakkında bilgi edinin."
keywords: "SQL söz dizimi, sql sorgusu, sql sorguları, json sorgu dili, veritabanı kavramlarını ve sql sorguları, toplama işlevleri"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: b2fa8e8f-7291-45a3-9bd1-7284ed9077f8
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: 2fee3786b7d48d254162699471943e316764b003
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tuning-query-performance-with-azure-cosmos-db"></a>Sorgu performans Azure Cosmos DB ile ayarlama
Azure Cosmos DB sağlayan bir [SQL veri sorgulama için API](documentdb-sql-query.md), şema veya ikincil dizinler gerektirmeden. Bu makalede, geliştiriciler için bilgi aşağıdaki hello sağlar:

* Azure Cosmos veritabanı SQL sorgu yürütme nasıl çalıştığı hakkında üst düzey ayrıntıları
* Sorgu istek ve yanıt üstbilgileri ve istemci SDK seçenekleri hakkında ayrıntılar
* İpuçları ve sorgu performansı için en iyi yöntemler
* Nasıl tooutilize SQL yürütme istatistikleri toodebug sorgu performansı örnekleri

## <a name="about-sql-query-execution"></a>SQL sorgu yürütme hakkında

Azure Cosmos DB'de tooany büyüyebilir kapsayıcıları veri deposundaki [depolama boyutu veya istek işleme](partition-data.md). Azure Cosmos DB veri hello kapsar toohandle veri büyüme veya sağlanan işleme artış altında fiziksel bölümleri arasında sorunsuz bir şekilde ölçeklendirir. SQL sorguları tooany kapsayıcı hello REST API veya desteklenen hello birini kullanarak sorunu [DocumentDB SDK'ları](documentdb-sdk-dotnet.md).

Bölümlendirme, kısa bir genel bakış: veri fiziksel bölümleri arasında nasıl bölünür belirler "Şehir" gibi bir bölüm anahtarı tanımlayın. Veri ait tooa tek bölüm anahtarı (örneğin, "Şehir" "Seattle" ==) fiziksel bir bölüm içinde depolanır ancak genellikle tek bir fiziksel bölüm birden çok bölüm anahtarlarını sahiptir. Bir bölümü depolama boyutuna ulaştığında hello hizmet sorunsuz bir şekilde hello bölüm iki yeni bölümlere ayırır ve hello bölüm anahtarı bu bölümleri arasında eşit olarak böler. Bölümler geçici olduğundan, hello API'leri "Bölüm anahtarı karmaları hello aralıklarını gösterir bir bölüm anahtarı aralığı" için bir Özet kullanın. 

Sorgu tooAzure Cosmos DB verdiğinizde, hello SDK mantıksal adımları gerçekleştirir:

* Merhaba SQL sorgu toodetermine hello sorgu yürütme planı ayrıştırılamıyor. 
* Merhaba sorgu hello bölüm anahtarı karşı bir filtre içeriyorsa, ister `SELECT * FROM c WHERE c.city = "Seattle"`, yönlendirilmiş tooa olan tek bir bölüm. Merhaba sorgu bölüm anahtarı üzerinde bir filtre yok sonra içindeki tüm bölümlerin yürütülür ve sonuçları birleştirilir istemci tarafı.
* Merhaba sorgu her bölümü seri içinde yürütülen veya paralel, istemci yapılandırmasına bağlı olarak. Her bölüm içinde hello sorgu birini yapabilir veya hello sorgu karmaşıklık bağlı olarak daha fazla gidiş dönüş sayfa boyutu yapılandırılmış ve hello koleksiyonu verimini sağlandı. Her yürütme hello sayısını döndürür [istek birimleri](request-units.md) sorgu yürütme ve isteğe bağlı olarak, sorgu yürütme istatistikleri tüketilen. 
* Merhaba SDK hello sorgu sonuçlarının bir özetini bölümler gerçekleştirir. Hello sorgu bir ORDER BY bölümler içeriyorsa, örneğin, daha sonra bireysel bölümleri sonuçlarından birleştirme sıralanmış tooreturn sonuçlar genel olarak sıralanmış olarak olur. Merhaba sorgu gibi bir toplama ise `COUNT`, tek tek bölümlerden birinden hello sayı olan toplanan tooproduce hello toplam sayısı.

Merhaba SDK'ları sorgu yürütmesi için çeşitli seçenekler sağlar. Örneğin, .NET içinde bu seçenekler hello kullanılabilir `FeedOptions` sınıfı. Merhaba aşağıdaki tabloda bu seçenekler ve bunların nasıl sorgusu yürütme süresi etkisi açıklanmaktadır. 

| Seçenek | Açıklama |
| ------ | ----------- |
| `EnableCrossPartitionQuery` | Tootrue arasında birden fazla bölüm yürütülen toobe gerektiren herhangi bir sorgu için ayarlamanız gerekir. Bu bir açık bayrağı tooenable olduğundan, geliştirme zamanı sırasında toomake bilinçli performans dengelerin. |
| `EnableScanInQuery` | Dizin oluşturma dışında çevirdiniz ancak toorun hello sorgu bir tarama aracılığıyla yine de istiyorsanız tootrue ayarlamanız gerekir. Yalnızca hello için dizin oluşturma geçerli filtre yol devre dışı istedi. | 
| `MaxItemCount` | Merhaba en fazla gidiş dönüş toohello sunucu başına öğeleri tooreturn sayısı. Çok-1 ayarlayarak hello sunucu hello öğe sayısını yönetme izin verebilirsiniz. Ya da bu değer tooretrieve yalnızca az sayıda gidiş dönüş başına öğe düşürebilirsiniz. 
| `MaxBufferedItemCount` | Bu istemci-tarafı bir seçenektir ve çapraz bölüm ORDER BY gerçekleştirirken toolimit hello bellek tüketimi kullanılan. Daha yüksek bir değer çapraz bölüm sıralama hello gecikme süresi azaltılmasına yardımcı olur. |
| `MaxDegreeOfParallelism` | Alır veya hello hello Azure DocumentDB veritabanı hizmeti paralel sorgu yürütme sırasında istemci tarafı çalıştırmak eşzamanlı işlem sayısını ayarlar. Pozitif özellik değerini eşzamanlı işlem toohello kümesi değeri hello sayısını sınırlar. 0'dan tooless ayarlanırsa hello sistem eşzamanlı işlem toorun hello sayısı otomatik olarak karar verir. |
| `PopulateQueryMetrics` | Yükleme zamanı süre istatistiklerin ayrıntılı günlük sorgu yürütme derleme süresi, dizin döngü süresi ve belge gibi çeşitli aşamaları harcadığı etkinleştirir. Sorgu istatistiklerini çıktısını Azure toodiagnose sorgu performans sorunlarıyla paylaşabilirsiniz. |
| `RequestContinuation` | Herhangi bir sorgu tarafından döndürülen hello donuk devamlılık belirteci geçirerek sorgu yürütme devam edebilirsiniz. Merhaba devamlılık belirteci sorgu yürütme için gerekli tüm durum yalıtır. |
| `ResponseContinuationTokenLimitInKb` | Merhaba hello devamlılık belirteci hello sunucu tarafından döndürülen en büyük boyutunu sınırlandırabilirsiniz. Uygulama ana bilgisayarı yanıt üstbilgi boyutu sınırları varsa bu tooset gerekebilir. Bu ayarı hello artırabileceği toplam süre ve hello sorgu için kullanılan RUs.  |

Örneğin, örnek bir sorgu ile bir koleksiyon üzerinde istenen bölüm anahtarı atalım `/city` hello bölüm anahtarı ve sn'ye 100.000 RU/s ile sağlanan olarak. Bu sorgu kullanarak isteği `CreateDocumentQuery<T>` hello aşağıdaki gibi .NET içinde:

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        PopulateQueryMetrics = true, 
        MaxItemCount = -1, 
        MaxDegreeOfParallelism = -1, 
        EnableCrossPartitionQuery = true 
    }).AsDocumentQuery();

FeedResponse<dynamic> result = await query.ExecuteNextAsync();
```

Yukarıda gösterilen SDK parçacığı Merhaba, REST API isteği aşağıdaki toohello karşılık gelir:

```
POST https://arramacquerymetrics-westus.documents.azure.com/dbs/db/colls/sample/docs HTTP/1.1
x-ms-continuation: 
x-ms-documentdb-isquery: True
x-ms-max-item-count: -1
x-ms-documentdb-query-enablecrosspartition: True
x-ms-documentdb-query-parallelizecrosspartitionquery: True
x-ms-documentdb-query-iscontinuationexpected: True
x-ms-documentdb-populatequerymetrics: True
x-ms-date: Tue, 27 Jun 2017 21:52:18 GMT
authorization: type%3dmaster%26ver%3d1.0%26sig%3drp1Hi83Y8aVV5V6LzZ6xhtQVXRAMz0WNMnUuvriUv%2b4%3d
x-ms-session-token: 7:8,6:2008,5:8,4:2008,3:8,2:2008,1:8,0:8,9:8,8:4008
Cache-Control: no-cache
x-ms-consistency-level: Session
User-Agent: documentdb-dotnet-sdk/1.14.1 Host/32-bit MicrosoftWindowsNT/6.2.9200.0
x-ms-version: 2017-02-22
Accept: application/json
Content-Type: application/query+json
Host: arramacquerymetrics-westus.documents.azure.com
Content-Length: 52
Expect: 100-continue

{"query":"SELECT * FROM c WHERE c.city = 'Seattle'"}
```

Her bir sorgu yürütme sayfa tooa REST API karşılık gelen `POST` hello ile `Accept: application/query+json` üstbilgi ve hello gövdesindeki hello SQL sorgusu. Her sorgu bir yapan veya daha fazla dönüşleri toohello hello sunucusuyla yuvarlak `x-ms-continuation` belirteci echoed hello istemci ve sunucu tooresume yürütme arasında. Merhaba yapılandırma seçenekleri FeedOptions toohello sunucusuna istek üstbilgilerinin hello biçiminde geçirilir. Örneğin, `MaxItemCount` çok karşılık gelen`x-ms-max-item-count`. 

Merhaba isteği döndürür (okunabilirlik için kesilmiş) hello aşağıdaki yanıtı:

```
HTTP/1.1 200 Ok
Cache-Control: no-store, no-cache
Pragma: no-cache
Transfer-Encoding: chunked
Content-Type: application/json
Server: Microsoft-HTTPAPI/2.0
Strict-Transport-Security: max-age=31536000
x-ms-last-state-change-utc: Tue, 27 Jun 2017 21:01:57.561 GMT
x-ms-resource-quota: documentSize=10240;documentsSize=10485760;documentsCount=-1;collectionSize=10485760;
x-ms-resource-usage: documentSize=1;documentsSize=884;documentsCount=2000;collectionSize=1408;
x-ms-item-count: 2000
x-ms-schemaversion: 1.3
x-ms-alt-content-path: dbs/db/colls/sample
x-ms-content-path: +9kEANVq0wA=
x-ms-xp-role: 1
x-ms-documentdb-query-metrics: totalExecutionTimeInMs=33.67;queryCompileTimeInMs=0.06;queryLogicalPlanBuildTimeInMs=0.02;queryPhysicalPlanBuildTimeInMs=0.10;queryOptimizationTimeInMs=0.00;VMExecutionTimeInMs=32.56;indexLookupTimeInMs=0.36;documentLoadTimeInMs=9.58;systemFunctionExecuteTimeInMs=0.00;userFunctionExecuteTimeInMs=0.00;retrievedDocumentCount=2000;retrievedDocumentSize=1125600;outputDocumentCount=2000;writeOutputTimeInMs=18.10;indexUtilizationRatio=1.00
x-ms-request-charge: 604.42
x-ms-serviceversion: version=1.14.34.4
x-ms-activity-id: 0df8b5f6-83b9-4493-abda-cce6d0f91486
x-ms-session-token: 2:2008
x-ms-gatewayversion: version=1.14.33.2
Date: Tue, 27 Jun 2017 21:59:49 GMT
```

Merhaba sorgusundan döndürülen hello anahtar yanıt üstbilgilerini hello şunları içerir:

| Seçenek | Açıklama |
| ------ | ----------- |
| `x-ms-item-count` | Merhaba hello yanıtta döndürülen öğe sayısı. Bu sağlanan hello üzerinde bağımlı `x-ms-max-item-count`, hello hello en büyük yanıt yükü boyutu, hello sağlanan işleme ve sorgu yürütme süresi içinde sığabilecek öğe sayısı. |  
| `x-ms-continuation:` | Merhaba devamlılık belirteci tooresume yürütme hello sorgusunun ek sonuçlar varsa. | 
| `x-ms-documentdb-query-metrics` | Merhaba yürütme Hello sorgu istatistikleri. Bu, sorgu yürütme çeşitli aşamaları hello harcanan zamanın istatistikleri içeren sınırlandırılmış bir dizedir. Döndürülen IF `x-ms-documentdb-populatequerymetrics` çok ayarlanır`True`. | 
| `x-ms-request-charge` | Merhaba sayısı [istek birimleri](request-units.md) hello sorgu tarafından tüketilen. | 

Merhaba REST API isteği üstbilgileri ve seçenekleri hakkında daha fazla bilgi için bkz: [hello DocumentDB REST API kullanarak kaynak sorgulaması](https://docs.microsoft.com/rest/api/documentdb/querying-documentdb-resources-using-the-rest-api).

## <a name="best-practices-for-query-performance"></a>Sorgu performansı için en iyi yöntemler
Merhaba aşağıdaki Azure Cosmos DB sorgu performansı etkileyen hello en yaygın faktörlerdir. Bu makalede bu konuların her derinlere.

| Faktörü | İpucu | 
| ------ | -----| 
| Sağlanan aktarım hızı | Sorgu RU ölçmek ve sorgularınızı hello gerekli sağlanan işleme sahip olduğundan emin olun. | 
| Bölümleme ve bölüm anahtarları | Sorguları ayrıcalık tanıma düşük gecikme süresi hello filtre yan tümcesi içinde hello bölüm anahtarı değerine sahip. |
| SDK ve sorgu seçenekleri | Doğrudan bağlantı gibi SDK en iyi uygulamaları izleyin ve istemci tarafı sorgu yürütme seçeneklerini ayarlayın. |
| Ağ gecikmesi | Ağ Yükü ölçüm için hesap ve en yakın bölgeyi hello gelen çok girişli API'leri tooread kullanın. |
| Dizin oluşturma ilkesi | Gerekli hello dizin yolları/İlkesi hello sorgu için olduğundan emin olun. |
| Sorgu yürütme ölçümleri | Merhaba sorgu yürütme ölçümleri tooidentify olası yeniden yazdırmaya sorgu ve veri şekilleri, analiz edin.  |

### <a name="provisioned-throughput"></a>Sağlanan aktarım hızı
Cosmos DB'de her istek birimleri (RU) Saniyedeki cinsinden ifade edilen ayrılmış işleme ile veri kapsayıcı oluşturun. 1 KB belgenin okuma 1. RU, (sorguları da dahil) her işlemi ise bunun kapsamına bağlı RUs sayısı sabit normalleştirilmiş tooa. Örneğin, 1000 varsa RU/s kapsayıcısı için sağlanan ve gibi bir sorguya sahip `SELECT * FROM c WHERE c.city = 'Seattle'` 5 RUs kullanır ve ardından (1000 RU/s) gerçekleştirebilirsiniz / (5 RU/sorgu) sorgularını saniyede = 200 sorgu/s. 

200'den fazla saniye başına sorgusu gönderirseniz, hız sınırlaması gelen istekleri 200/s yukarıda hello hizmetini başlatır. Merhaba SDK'ları otomatik olarak geri Çekilme/yeniden deneme gerçekleştirerek bu durumda işler, bu nedenle bu sorgular için daha yüksek gecikme fark edebilirsiniz. Sağlanan hello verimlilik toohello artırma değeri sorgu gecikme süresi ve verimliliği artırır gereklidir. 

İstek birimleri hakkında daha fazla toolearn bkz [istek birimleri](request-units.md).

### <a name="partitioning-and-partition-keys"></a>Bölümleme ve bölüm anahtarları
Azure Cosmos DB ile sorguları genellikle siparişi hızlı/en verimli tooslower/daha az verimli aşağıdaki hello gerçekleştirin. 

* Bir tek bölüm anahtarı ve öğe anahtarı alma
* Tek bölüm anahtarı bir filtre yan tümcesi içeren sorgu
* Bir eşitlik veya aralık filtre yan tümcesi herhangi bir özellikte olmadan sorgulama
* Filtre sorgulama

Bu gereksinim tooconsult tüm bölümleri gereksinimini daha yüksek gecikme sorgular ve daha yüksek RUs kullanmasını sağlayabilirsiniz. Her bölüm karşı tüm özellikleri otomatik dizin oluşturma işlemi olduğundan, hello sorgu verimli bir şekilde hello dizinden bu durumda hizmet verilebilir. Merhaba paralellik seçenekleri kullanarak bölümleri daha hızlı yayılma sorgular yapabilir.

bölümlendirme ve bölüm anahtarları hakkında daha fazla toolearn bkz [Azure Cosmos DB'de bölümleme](partition-data.md).

### <a name="sdk-and-query-options"></a>SDK ve sorgu seçenekleri
Bkz: [performans ipuçları](performance-tips.md) ve [performans testi](performance-testing.md) nasıl tooget hello en iyi istemci tarafında performans Azure Cosmos DB'den için. Bu kullanarak içerir platforma özgü yapılandırmaları bağlantıları, atık toplama sıklığını varsayılan sayısı gibi yapılandırma ve doğrudan/TCP gibi basit bağlantı seçenekleri kullanarak en son SDK hello. 


#### <a name="max-item-count"></a>En fazla öğe sayısı
Sorgular için değeri hello `MaxItemCount` uçtan uca sorgu zamanında önemli bir etkisi olabilir. Her gidiş dönüş toohello sunucu hello öğelerin sayısı en fazla döndürülecek `MaxItemCount` (100 öğelerinin varsayılan). Bu tooa daha yüksek değer ayarlama (-1, en fazla ve önerilen), sorgu süresi genel hello özellikle büyük sonuç kümeleri ile sorgular için istemci ve sunucu arasındaki gidiş dönüş sayısı sınırlayarak geliştirecektir.

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        MaxItemCount = -1, 
    }).AsDocumentQuery();
```

#### <a name="max-degree-of-parallelism"></a>Maksimum paralellik derecesi
Merhaba sorguları için ayarlama `MaxDegreeOfParallelism` tooidentify hello özellikle çapraz bölüm sorgular (olmadan bir filtre hello bölüm anahtarı değerini) gerçekleştirirseniz, uygulamanız için en iyi yapılandırmaları. `MaxDegreeOfParallelism`Merhaba sayısını Paralel Görevler, yani, paralel olarak ziyaret bölümleri toobe hello maksimum denetler. 

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        MaxDegreeOfParallelism = -1, 
        EnableCrossPartitionQuery = true 
    }).AsDocumentQuery();
```

Varsayalım
* D = (Merhaba istemci makine işlemcide toplam sayısı =) Paralel Görevler varsayılan maksimum sayısı
* P = Paralel Görevler maksimum sayısı kullanıcı tanımlı
* N ziyaret toobe bir sorgu yanıtlama için gereken bölüm sayısı =

Merhaba paralel sorgular P. farklı değerler için nasıl davranacaktır etkileri verilmiştir
* (P == 0) = > seri modu
* (P == 1) = > bir görevin maksimum
* (P > 1) = > Min (P, N) Paralel Görevler 
* (P < 1) = > Min (N, D) Paralel Görevler

SDK sürüm notlarında ve uygulanan sınıflar ve yöntemler ayrıntıları görmek için [DocumentDB SDK'ları](documentdb-sdk-dotnet.md)

### <a name="network-latency"></a>Ağ gecikmesi
Bkz: [Azure Cosmos DB genel dağıtım](tutorial-global-distribution-documentdb.md) nasıl tooset yukarı genel dağıtım ve toohello en yakın bölgeyi bağlanmak için. Büyük sonuç hello sorgudan kümesi almak veya birden çok gidiş dönüş toomake gerek duyduğunuzda ağ gecikmesi sorgu performansına önemli bir etkisi vardır. 

Merhaba sorgu yürütme ölçümleri bölümüne nasıl tooretrieve hello sorgularda sunucusu yürütme süresi açıklar ( `totalExecutionTimeInMs`), böylece sorgu yürütme harcanan süre ve ağ yolda harcadığı zamanı arasında ayırt edebilir.

### <a name="indexing-policy"></a>Dizin oluşturma ilkesi
Bkz: [dizin oluşturma ilkesini yapılandırma](indexing-policies.md) yolları, tür ve modları ve bunlar sorgu yürütme nasıl etkiler dizin oluşturma için. Varsayılan olarak, dizin oluşturma ilkesi hello karma dizeleri için dizin oluşturma kullanır etkin olduğu yönelik eşitlik sorguları, ancak aralığı sorguları/order sorgular tarafından için değil. Aralık sorgu dizeleri için gerekiyorsa, hello tüm dizeleri aralığı dizin türü belirtilmesi önerilir. 

## <a name="query-execution-metrics"></a>Sorgu yürütme ölçümleri
İsteğe bağlı hello geçirerek sorgu yürütme üzerinde ayrıntılı ölçümler edinebilirsiniz `x-ms-documentdb-populatequerymetrics` üstbilgi (`FeedOptions.PopulateQueryMetrics` hello .NET SDK içinde). Merhaba, döndürülen değer `x-ms-documentdb-query-metrics` amacı, Gelişmiş sorgu yürütme işlemi sorun giderme için anahtar-değer çiftleri aşağıdaki hello sahiptir. 

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        PopulateQueryMetrics = true, 
    }).AsDocumentQuery();

FeedResponse<dynamic> result = await query.ExecuteNextAsync();

// Returns metrics by partition key range Id
IReadOnlyDictionary<string, QueryMetrics> metrics = result.QueryMetrics;

```

| Ölçüm | Birim | Açıklama | 
| ------ | -----| ----------- |
| `totalExecutionTimeInMs` | milisaniye | Sorgu yürütme süresi | 
| `queryCompileTimeInMs` | milisaniye | Sorgu derleme süresi  | 
| `queryLogicalPlanBuildTimeInMs` | milisaniye | Zaman toobuild mantıksal sorgu planı | 
| `queryPhysicalPlanBuildTimeInMs` | milisaniye | Zaman toobuild fiziksel sorgu planı | 
| `queryOptimizationTimeInMs` | milisaniye | Sorgu en iyi duruma getirme için harcanan süre | 
| `VMExecutionTimeInMs` | milisaniye | Sorgu çalışma zamanında harcanan süre | 
| `indexLookupTimeInMs` | milisaniye | Fiziksel dizini katmanda harcanan süre | 
| `documentLoadTimeInMs` | milisaniye | Belgeleri yüklenirken harcanan süre  | 
| `systemFunctionExecuteTimeInMs` | milisaniye | Yürütülen sistem (yerleşik) işlevleri milisaniye cinsinden toplam süre  | 
| `userFunctionExecuteTimeInMs` | milisaniye | Milisaniye cinsinden yürütme kullanıcı tanımlı işlevler için harcanan toplam süre | 
| `retrievedDocumentCount` | milisaniye | Toplam alınan belge sayısı  | 
| `retrievedDocumentSize` | Bayt | Alınan belgeleri bayt olarak toplam boyutu  | 
| `outputDocumentCount` | Sayısı | Çıktı belge sayısı | 
| `writeOutputTimeInMs` | milisaniye | Milisaniye cinsinden sorgu yürütme süresi | 
| `indexUtilizationRatio` | oranı (< = 1) | Merhaba filtre toohello yüklenen belge sayısı ile eşleşen belge sayısı oranı  | 

Merhaba istemci SDK'ları dahili olarak birden çok sorgu işlemleri tooserve hello sorgusu her bölüm içinde kalmasına neden olabilir. Merhaba istemci başına hello toplam sonuçları aşarsanız bölümü birden fazla çağrı yaptığında `x-ms-max-item-count`hello sorgu aşıyor hello bölümü için sağlanan işleme hello Merhaba, sorgu yükünü sayfa başına hello maksimum boyuta ulaşana veya Merhaba, sorgu hello ulaştığında, Sistem zaman aşımı sınırı ayrılmış. Her kısmi sorgu yürütme döndüren bir `x-ms-documentdb-query-metrics` bu sayfa için. 

Bazı örnek sorgular şunlardır ve nasıl hello ölçümleri bazıları döndürülen sorgu yürütülmesini toointerpret: 

| Sorgu | Örnek ölçümü | Açıklama | 
| ------ | -----| ----------- |
| `SELECT TOP 100 * FROM c` | `"RetrievedDocumentCount": 101` | Merhaba alınan belge sayısı 100 + 1 toomatch hello TOP yan tümcesi. Sorgu zaman harcanan çoğunlukla `WriteOutputTime` ve `DocumentLoadTime` tarama olduğundan. | 
| `SELECT TOP 500 * FROM c` | `"RetrievedDocumentCount": 501` | RetrievedDocumentCount daha yüksek (500 + 1 toomatch hello TOP yan tümcesi) sunulmuştur. | 
| `SELECT * FROM c WHERE c.N = 55` | `"IndexLookupTime": "00:00:00.0009500"` | Dizin arama olmasından dolayı hakkında 0,9 ms için anahtar bir arama, IndexLookupTime içinde harcanan `/N/?`. | 
| `SELECT * FROM c WHERE c.N > 55` | `"IndexLookupTime": "00:00:00.0017700"` | Biraz daha fazla (1,7 ms) için harcanan süre içinde IndexLookupTime aralığı tarama bir dizin arama olmasından dolayı `/N/?`. | 
| `SELECT TOP 500 c.N FROM c` | `"IndexLookupTime": "00:00:00.0017700"` | Aynı anda harcanan `DocumentLoadTime` önceki sorgular, ancak daha düşük `WriteOutputTime` yalnızca tek bir özellik yansıtma olduğundan. | 
| `SELECT TOP 500 udf.toPercent(c.N) FROM c` | `"UserDefinedFunctionExecutionTime": "00:00:00.2136500"` | Yaklaşık 213 ms, geçen `UserDefinedFunctionExecutionTime` her değerine göre hello UDF yürütme `c.N`. |
| `SELECT TOP 500 c.Name FROM c WHERE STARTSWITH(c.Name, 'Den')` | `"IndexLookupTime": "00:00:00.0006400", "SystemFunctionExecutionTime": "00:00:00.0074100"` | Yaklaşık 0,6 ms, geçen `IndexLookupTime` üzerinde `/Name/?`. Merhaba çoğunu sorgusunu yürütme süresi (~ 7 ms) `SystemFunctionExecutionTime`. |
| `SELECT TOP 500 c.Name FROM c WHERE STARTSWITH(LOWER(c.Name), 'den')` | `"IndexLookupTime": "00:00:00", "RetrievedDocumentCount": 2491,  "OutputDocumentCount": 500` | Sorgu, bir tarama gerçekleştirilir, kullandığından `LOWER`, ve 500 2491 alınan belgeleri dışında döndürülür. |


## <a name="next-steps"></a>Sonraki adımlar
* toolearn desteklenen hello SQL sorgu işleçleri ve anahtar sözcükler hakkında bkz [SQL sorgusu](documentdb-sql-query.md). 
* İstek birimleri hakkında toolearn bkz [istek birimleri](request-units.md).
* Dizin oluşturma ilkesi hakkında toolearn bakın [İlkesi dizin oluşturma](indexing-policies.md) 


