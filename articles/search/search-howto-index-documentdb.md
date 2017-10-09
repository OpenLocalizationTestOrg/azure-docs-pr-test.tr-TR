---
title: "aaaIndexing Cosmos DB veri kaynağı Azure arama için | Microsoft Docs"
description: "Bu makale size nasıl gösterir toocreate Cosmos DB veri kaynağı olarak sahip bir Azure Search dizin oluşturucu."
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 
ms.service: search
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: search
ms.date: 08/10/2017
ms.author: eugenesh
ms.openlocfilehash: 195c9bc026ee1591679dc425ef083a32a3c86be6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="connecting-cosmos-db-with-azure-search-using-indexers"></a>Azure Search'te dizin oluşturucular kullanma Cosmos DB bağlanma

Cosmos DB verilerinizi harika bir arama deneyimi tooimplement istiyorsanız, bir Azure Search dizinine bir Azure Search dizin oluşturucu toopull veri kullanabilirsiniz. Bu makalede, nasıl gösteriyoruz hiçbir kod toomaintain dizin altyapı toowrite kalmadan Azure Cosmos DB Azure Search toointegrate.

tooset Cosmos DB dizin oluşturucu yukarı olmalıdır bir [Azure Search Hizmeti](search-create-service-portal.md), bir dizin, veri kaynağı ve son olarak hello dizin oluşturucu oluşturabilirsiniz. Hello kullanarak bu nesneleri oluşturabilirsiniz [portal](search-import-data-portal.md), [.NET SDK'sı](/dotnet/api/microsoft.azure.search), veya [REST API](/rest/api/searchservice/) tüm .NET olmayan diller için. 

Merhaba portal için seçerseniz, hello [verilerini İçeri Aktar Sihirbazı](search-import-data-portal.md) , tüm bu kaynaklar hello oluşturulmasını size yol gösterir.

> [!NOTE]
> Cosmos DB hello DocumentDB gelecek nesil ' dir. Merhaba ürün adı değiştirilmiş olsa da, söz dizimi olan hello aynı önceki gibi. Lütfen toospecify devam `documentdb` bu dizin oluşturucu makalede yönergelerine uygun olarak. 

> [!TIP]
> Merhaba başlatabilirsiniz **veri içeri aktarma** gelen hello Cosmos DB Pano toosimplify bu veri kaynağı için Dizin Oluşturma Sihirbazı. Sol gezinti bölmesinde, çok Git**koleksiyonları** > **Azure arama Ekle** tooget başlatıldı.

<a name="Concepts"></a>
## <a name="azure-search-indexer-concepts"></a>Azure Search dizin oluşturucu kavramları
Azure arama destekler hello oluşturulması ve yönetimi, veri kaynaklarının (Cosmos DB dahil) ve dizin oluşturucular, bu veri kaynaklarına karşı çalışır.

A **veri kaynağı** hello veri tooindex, kimlik bilgileri ve (örneğin, değiştirilen veya silinen belgeleri koleksiyonunuzu içinde) hello verilerde yapılan değişiklikler tanımlamak için ilkeleri belirtir. Böylece birden çok dizin oluşturucular tarafından kullanılabilir hello veri kaynağı bağımsız bir kaynak olarak tanımlanır.

Bir **dizin oluşturucu** hello veri kaynağınızdan verileri bir hedef search dizinine nasıl akacağını açıklar. Bir dizin oluşturucu için kullanılabilir:

* Merhaba veri toopopulate dizin tek seferlik bir kopyasını gerçekleştirin.
* Dizin hello veri kaynağında bir zamanlamaya göre değişiklikler ile eşitleyin. Merhaba zamanlaması hello dizin oluşturucu tanımının bir parçası değildir.
* Gerektiğinde isteğe bağlı güncelleştirmeler tooan dizin çağırır.

<a name="CreateDataSource"></a>
## <a name="step-1-create-a-data-source"></a>1. adım: bir veri kaynağı oluşturma
toocreate bir veri kaynağı bir POST yapın:

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
        "name": "mydocdbdatasource",
        "type": "documentdb",
        "credentials": {
            "connectionString": "AccountEndpoint=https://myDocDbEndpoint.documents.azure.com;AccountKey=myDocDbAuthKey;Database=myDocDbDatabaseId"
        },
        "container": { "name": "myDocDbCollectionId", "query": null },
        "dataChangeDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName": "_ts"
        }
    }

Merhaba hello istek gövdesi alanları izleyen hello içermelidir hello veri kaynağı tanımını içerir:

* **ad**: Cosmos DB veritabanı adı toorepresent belirleyin.
* **tür**: olmalıdır `documentdb`.
* **kimlik bilgileri**:
  
  * **connectionString**: gerekli. Merhaba bağlantı bilgisi tooyour Azure Cosmos DB veritabanı biçimi aşağıdaki hello belirtin:`AccountEndpoint=<Cosmos DB endpoint url>;AccountKey=<Cosmos DB auth key>;Database=<Cosmos DB database id>`
* **kapsayıcı**:
  
  * **ad**: gerekli. Merhaba Cosmos DB koleksiyonu toobe dizine Hello kimliğini belirtin.
  * **Sorgu**: isteğe bağlı. Azure Search dizin düz bir şemaya sorgu tooflatten rasgele bir JSON belgesi belirtebilirsiniz.
* **dataChangeDetectionPolicy**: önerilir. Bkz: [dizin değiştirilmiş belgeleri](#DataChangeDetectionPolicy) bölümü.
* **dataDeletionDetectionPolicy**: isteğe bağlı. Bkz: [silinen belgeler dizin](#DataDeletionDetectionPolicy) bölümü.

### <a name="using-queries-tooshape-indexed-data"></a>Dizine veri sorguları tooshape kullanma
Cosmos DB sorgu tooflatten özelliklerini iç içe geçmiş veya dizileri, JSON özellikleri proje ve dizine hello veri toobe filtre belirtebilirsiniz. 

Örneğin belge:

    {
        "userId": 10001,
        "contact": {
            "firstName": "andy",
            "lastName": "hoh"
        },
        "company": "microsoft",
        "tags": ["azure", "documentdb", "search"]
    }

Filtre sorgusu:

    SELECT * FROM c WHERE c.company = "microsoft" and c._ts >= @HighWaterMark ORDER BY c._ts

Düzleştirme sorgusu:

    SELECT c.id, c.userId, c.contact.firstName, c.contact.lastName, c.company, c._ts FROM c WHERE c._ts >= @HighWaterMark ORDER BY c._ts
    
    
Projeksiyon sorgusu:

    SELECT VALUE { "id":c.id, "Name":c.contact.firstName, "Company":c.company, "_ts":c._ts } FROM c WHERE c._ts >= @HighWaterMark ORDER BY c._ts


Düzleştirme sorgu dizisi:

    SELECT c.id, c.userId, tag, c._ts FROM c JOIN tag IN c.tags WHERE c._ts >= @HighWaterMark ORDER BY c._ts

<a name="CreateIndex"></a>
## <a name="step-2-create-an-index"></a>2. adım: bir dizin oluşturun
Zaten yoksa, bir hedef Azure Search dizini oluşturma. Hello kullanarak bir dizin oluşturabilirsiniz [Azure portal UI](search-create-index-portal.md), hello [oluşturma dizini REST API](/rest/api/searchservice/create-index) veya [dizin sınıfı](/dotnet/api/microsoft.azure.search.models.index).

Aşağıdaki örnek hello bir kimlik ve açıklama alanı ile bir dizin oluşturur:

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
       "name": "mysearchindex",
       "fields": [{
         "name": "id",
         "type": "Edm.String",
         "key": true,
         "searchable": false
       }, {
         "name": "description",
         "type": "Edm.String",
         "filterable": false,
         "sortable": false,
         "facetable": false,
         "suggestions": true
       }]
     }

Bu hello emin olun, hedef dizin şemasını hello kaynak JSON belgelerinin hello şemasını veya özel sorgu projeksiyon hello çıktısını ile uyumlu.

> [!NOTE]
> Bölümlenmiş koleksiyonlar için hello varsayılan belge Cosmos veritabanı anahtarıdır `_rid` çok yeniden adlandırılmış özelliği`rid` Azure Search'te. Ayrıca, Cosmos veritabanı `_rid` değerleri Azure Search anahtarlarında geçersiz karakterler içeriyor. Bu nedenle, hello `_rid` Base64 ile kodlanmış değerlerdir.
> 
> 

### <a name="mapping-between-json-data-types-and-azure-search-data-types"></a>JSON veri türleri ve Azure Search'te veri türleri arasında eşleme
| JSON VERİ TÜRÜ | UYUMLU HEDEF DİZİN ALAN TÜRLERİ |
| --- | --- |
| bool |Edm.Boolean, Edm.String |
| Tamsayıları gibi ara numaraları |EDM.Int32, EDM.Int64, Edm.String |
| Bu görünümlü kayan nokta sayıları |Edm.Double, Edm.String |
| Dize |Edm.String |
| ["A", "b", "c"] örneğin ilkel türlerin dizileri |Collection(Edm.String) |
| Tarihleri gibi görünen dizeleri |Edm.DateTimeOffset, Edm.String |
| GeoJSON nesneleri, örneğin {"tür": "Point", "coordinates": [uzun lat]} |Edm.GeographyPoint |
| Diğer JSON nesneleri |Yok |

<a name="CreateIndexer"></a>
## <a name="step-3-create-an-indexer"></a>3. adım: bir dizin oluşturucu yapın

Başlangıç dizini ve veri kaynağı oluşturulduktan sonra hazır toocreate hello dizin oluşturucu olduğunuz:

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "mydocdbindexer",
      "dataSourceName" : "mydocdbdatasource",
      "targetIndexName" : "mysearchindex",
      "schedule" : { "interval" : "PT2H" }
    }

Bu dizin oluşturucu iki saatte bir çalışır (zamanlama aralığı çok Ayarla "PT2H"). bir dizin oluşturucu toorun 30 dakikada hello aralığı çok ayarlamak "PT30M". Merhaba kısa desteklenen aralığı 5 dakikadır. Merhaba zamanlama atlanırsa, isteğe bağlı -, yalnızca zaman bir kez oluşturulduktan sonra bir dizin oluşturucu çalıştırır. Ancak, bir dizin oluşturucu isteğe bağlı herhangi bir zamanda çalıştırabilirsiniz.   

Merhaba dizin oluşturucu API oluşturma hakkında daha fazla ayrıntı için kullanıma [oluşturma dizin oluşturucu](https://docs.microsoft.com/rest/api/searchservice/create-indexer).

<a id="RunIndexer"></a>
### <a name="running-indexer-on-demand"></a>Dizin Oluşturucu isteğe bağlı çalıştırma
Düzenli bir zamanlamaya göre ek toorunning içinde bir dizin oluşturucu isteğe bağlı olarak çağrılabilir:

    POST https://[service name].search.windows.net/indexers/[indexer name]/run?api-version=2016-09-01
    api-key: [Search service admin key]

> [!NOTE]
> Çalıştırma API başarıyla geri döndüğünde, hello dizin oluşturucu çağırma zamanlanmış ancak hello gerçek işlemini zaman uyumsuz olarak gerçekleşir. 

Merhaba portalında veya hello alma dizin oluşturucu durumu sonraki tanımlayan API'sini kullanarak hello dizin oluşturucu durumunu izleyebilirsiniz. 

<a name="GetIndexerStatus"></a>
### <a name="getting-indexer-status"></a>Dizin Oluşturucu durumunu alma
Bir dizin oluşturucu hello durumunu ve yürütme geçmişini alabilirsiniz:

    GET https://[service name].search.windows.net/indexers/[indexer name]/status?api-version=2016-09-01
    api-key: [Search service admin key]

Merhaba yanıt genel dizin oluşturucu durumu, hello son (veya devam eden) dizin oluşturucu çağırma ve son dizin oluşturucu çağrılarını hello geçmişini içerir.

    {
        "status":"running",
        "lastResult": {
            "status":"success",
            "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
         },
        "executionHistory":[ {
            "status":"success",
             "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
        }]
    }

Yukarı (Merhaba son yürütme hello yanıtta önce geliyorsa şekilde), ters kronolojik sırada sıralanır toohello 50 en son tamamlanan yürütmeleri, yürütme geçmişini içerir.

<a name="DataChangeDetectionPolicy"></a>
## <a name="indexing-changed-documents"></a>Değiştirilmiş belgeleri dizin oluşturma
bir veri Hello amacı değiştirme algılama İlkesi olduğunu tooefficiently tanımlamak değiştirilen veri öğeleri. Şu anda, yalnızca desteklenen hello hello ilkedir `High Water Mark` hello kullanarak İlkesi `_ts` (zaman damgası) özelliğini aşağıdaki gibi belirtilen Cosmos DB tarafından sağlanan:

    {
        "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
        "highWaterMarkColumnName" : "_ts"
    }

Bu ilkeyi kullanarak tooensure iyi dizin oluşturucu performans kullanmamanız önerilir. 

Özel bir sorgu kullanıyorsanız, bu hello emin olun `_ts` özelliği hello sorgu tarafından öngörülen.

<a name="IncrementalProgress"></a>
### <a name="incremental-progress-and-custom-queries"></a>Artımlı ilerleme ve özel sorgular
Dizin Oluşturucu yürütme geçici hataları veya yürütme süresi sınırını kesintiye uğrarsa, hello dizin oluşturucu, sonraki çalışılmayan toore dizin hello tüm koleksiyon sıfırdan sahip olmak yerine çalıştığında, kaldığı yukarı seçebilirsiniz, dizin oluşturma sırasında artımlı ilerleme sağlar. Bu büyük topluluklara dizin oluştururken özellikle önemlidir. 

özel bir sorgu kullanırken tooenable artımlı ilerleme olun sorgunuzu hello tarafından hello sonuçlarını sıralar `_ts` sütun. Bu, Dönemsel onay Azure Search hataları hello bulunması tooprovide artımlı ilerleme kullandığını gösteren sağlar.   

Bazı durumlarda, sorgunuzu içeriyor olsa bile bir `ORDER BY [collection alias]._ts` yan tümcesi, Azure Search değil Infer hello sorgulayan hello tarafından sıralanan `_ts`. Azure arama sonuçları hello kullanarak sıralanır anlayabilirsiniz `assumeOrderByHighWaterMarkColumn` Yapılandırma özelliği. toospecify bu ipucu oluşturun veya aşağıdaki gibi dizin güncelleştirin: 

    {
     ... other indexer definition properties
     "parameters" : {
            "configuration" : { "assumeOrderByHighWaterMarkColumn" : true } }
    } 

<a name="DataDeletionDetectionPolicy"></a>
## <a name="indexing-deleted-documents"></a>Dizin oluşturma belgeleri silindi
Merhaba koleksiyondan silinen satır, normalde toodelete hello arama dizini de bu satırları istediğinizde. bir veri silme algılama İlkesi Hello amacı tooefficiently silinen veri öğeleri tanımlayın. Şu anda, yalnızca desteklenen hello hello ilkedir `Soft Delete` İlkesi (silme bazı sıralama bayrağıyla işaretlenmiş), olduğu gibi belirtildi:

    {
        "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
        "softDeleteColumnName" : "hello property that specifies whether a document was deleted",
        "softDeleteMarkerValue" : "hello value that identifies a document as deleted"
    }

Özel bir sorgu kullanıyorsanız, bu hello özelliği tarafından başvurulan emin olun `softDeleteColumnName` hello sorgu tarafından yansıtılır.

Aşağıdaki örneğine hello bir veri kaynağı ile bir geçici silme ilkesi oluşturur:

    POST https://[Search service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [Search service admin key]

    {
        "name": "mydocdbdatasource",
        "type": "documentdb",
        "credentials": {
            "connectionString": "AccountEndpoint=https://myDocDbEndpoint.documents.azure.com;AccountKey=myDocDbAuthKey;Database=myDocDbDatabaseId"
        },
        "container": { "name": "myDocDbCollectionId" },
        "dataChangeDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName": "_ts"
        },
        "dataDeletionDetectionPolicy": {
            "@odata.type": "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
            "softDeleteColumnName": "isDeleted",
            "softDeleteMarkerValue": "true"
        }
    }

## <a name="NextSteps"></a>Sonraki adımlar
Tebrikler! Nasıl kullanarak Azure Search ile Azure Cosmos DB toointegrate hello dizin oluşturucu için Cosmos DB öğrendiniz.

* Azure Cosmos DB hakkında daha fazla nasıl toolearn bakın hello [Cosmos DB hizmeti sayfası](https://azure.microsoft.com/services/documentdb/).
* Azure Search hakkında daha fazla nasıl toolearn bakın hello [arama hizmeti sayfası](https://azure.microsoft.com/services/search/).
