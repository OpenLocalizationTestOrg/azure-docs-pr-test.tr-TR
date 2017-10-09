---
title: "Arama hizmeti REST API sürümü 2015-02-28-Önizleme aaaAzure | Microsoft Docs"
description: "Azure Search Hizmeti REST API sürümü 2015-02-28-Önizleme doğal dil Çözümleyicileri ve moreLikeThis aramaları gibi Deneysel özellikler içerir."
services: search
documentationcenter: na
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 3dba3bf8-9c83-42f6-82bc-04727bd11037
ms.service: search
ms.devlang: rest-api
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: search
ms.date: 05/01/2017
ms.author: brjohnst
ms.openlocfilehash: 63cb30b7f43a42552c6744ea087afea947857224
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search-service-rest-api-version-2015-02-28-preview"></a>Azure Search Hizmeti REST API'si: Sürüm 2015-02-28-Önizleme
Bu makalede hello başvurusu için belgesidir `api-version=2015-02-28-Preview`. Bu önizleme hello geçerli genel olarak kullanılabilir sürümü, genişletir [api-version = 2015-02-28](https://msdn.microsoft.com/library/dn798935.aspx), Deneysel özellikleri aşağıdaki hello sağlayarak:

* `moreLikeThis`sorgu parametresi hello içinde [Search belgeleri](#SearchDocs) API. İlgili tooanother belirli belge olan diğer belgeleri bulur.

Merhaba birkaç ek bölümlerini `2015-02-28-Preview` REST API ayrı olarak belgelenmiştir. Bunlar:

* [Puanlama profili](search-api-scoring-profiles-2015-02-28-preview.md)
* [Dizin Oluşturucular](search-api-indexers-2015-02-28-preview.md)

Azure Search hizmeti birden çok sürümlerinde kullanılabilir. Lütfen çok başvurun[arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar için.

## <a name="apis-in-this-document"></a>Bu belgedeki API'leri
Azure Search Hizmeti API'si API işlemleri için iki URL sözdizimleri destekler: Basit ve OData (bkz [OData (Azure Search API) için destek](http://msdn.microsoft.com/library/azure/dn798932.aspx) Ayrıntılar için). Merhaba aşağıdaki listede hello basit sözdizimi gösterilmektedir.

[Dizin oluşturma](#CreateIndex)

    POST /indexes?api-version=2015-02-28-Preview

[Dizini Güncelleştir](#UpdateIndex)

    PUT /indexes/[index name]?api-version=2015-02-28-Preview

[Dizin Al](#GetIndex)

    GET /indexes/[index name]?api-version=2015-02-28-Preview

[Dizinleri listeleme](#ListIndexes)

    GET /indexes?api-version=2015-02-28-Preview

[Dizin istatistikleri Al](#GetIndexStats)

    GET /indexes/[index name]/stats?api-version=2015-02-28-Preview

[Testi Çözümleyicisi](#TestAnalyzer)

    POST /indexes/[index name]/analyze?api-version=2015-02-28-Preview

[Dizin silme](#DeleteIndex)

    DELETE /indexes/[index name]?api-version=2015-02-28-Preview

[Ekleme, silme ve dizin içindeki verileri güncelleştirme](#AddOrUpdateDocuments)

    POST /indexes/[index name]/docs/index?api-version=2015-02-28-Preview

[Belge ara](#SearchDocs)

    GET /indexes/[index name]/docs?[query parameters]
    POST /indexes/[index name]/docs/search?api-version=2015-02-28-Preview

[Arama belge](#LookupAPI)

     GET /indexes/[index name]/docs/[key]?[query parameters]

[Count belgeleri](#CountDocs)

    GET /indexes/[index name]/docs/$count?api-version=2015-02-28-Preview

[Öneriler](#Suggestions)

    GET /indexes/[index name]/docs/suggest?[query parameters]
    POST /indexes/[index name]/docs/suggest?api-version=2015-02-28-Preview

- - -
<a name="IndexOps"></a>

## <a name="index-operations"></a>Dizin işlemleri
Oluşturun ve Azure Search hizmeti belirtilen dizin kaynak basit HTTP isteklerini (POST, GET, PUT, DELETE) aracılığıyla dizinlerde yönetin. toocreate dizini bir ilk hello dizin şemasını tanımlayan bir JSON belgesi gönderin. Merhaba şema başlangıç dizini, kendi veri türleri ve nasıl (örneğin, tam metin araması, filtre, sıralama veya olduğunu) kullanılabilmesi için hello alanları tanımlar. Ayrıca, Puanlama profilleri, ilgili ve hello dizin diğer öznitelikleri tooconfigure hello davranışını tanımlar.

Merhaba aşağıdaki örnekte iki dillerde tanımlanan hello açıklama alanı ile otel bilgi aramak için kullanılan bir şema bir çizimi sağlar. Nasıl öznitelikleri hello alanın nasıl kullanıldığını kontrol dikkat edin. Örneğin hello `hotelId` hello belge anahtarı olarak kullanılan (`"key": true`) ve tam metin aramalardan dışlandı (`"searchable": false`).

    {
    "name": "hotels",  
    "fields": [
      {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
      {"name": "baseRate", "type": "Edm.Double"},
      {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
      {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
      {"name": "hotelName", "type": "Edm.String"},
      {"name": "category", "type": "Edm.String"},
      {"name": "tags", "type": "Collection(Edm.String)"},
      {"name": "parkingIncluded", "type": "Edm.Boolean"},
      {"name": "smokingAllowed", "type": "Edm.Boolean"},
      {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
      {"name": "rating", "type": "Edm.Int32"},
      {"name": "location", "type": "Edm.GeographyPoint"}
     ],
     "suggesters": [
      {
       "name": "sg",
       "searchMode": "analyzingInfixMatching",
       "sourceFields": ["hotelName"]
      }
     ]
    }

Merhaba dizin oluşturulduktan sonra başlangıç dizinini doldurmak belgeleri yükleyeceksiniz. Bkz: [ekleme veya güncelleştirme belgeler](#AddOrUpdateDocuments) bu sonraki adım için.

Azure Search'te bir video girişi tooindexing için hello bkz [kanal 9 bulut kapak bölüm Azure Search üzerinde](http://go.microsoft.com/fwlink/p/?LinkId=511509).

<a name="CreateIndex"></a>

## <a name="create-index"></a>Dizin Oluşturma
Bir dizin düzenleme ve belgeler Azure Search'te arama hello birincil anlamına gelir, veritabanındaki kayıtları benzer toohow tablo düzenler. Her dizin tüm toohello dizin şemasını (alan adları, veri türleri ve özellikleri) uygun ancak dizinler de diğer arama davranışları tanımlamak ek yapıları (ilgili, Puanlama profilleri ve CORS seçenekleri) belirtmeniz belgeleri koleksiyonu vardır.

Bir HTTP POST veya PUT İsteği kullanarak Azure Search hizmeti içinde yeni bir dizin oluşturabilirsiniz. Merhaba hello istek gövdesi başlangıç dizini ve yapılandırma bilgileri belirten bir JSON Şeması ' dir.

    POST https://[service name].search.windows.net/indexes?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Alternatif olarak, PUT kullanın ve URI hello üzerinde hello dizin adı belirtin. Merhaba dizin yoksa, oluşturulur.

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]

Dizin oluşturma depolanır ve arama işlemlerinin kullanılan hello belgelerinin hello yapısını belirler. Doldurma hello dizin ayrı bir işlemdir. Bu adım için kullanabileceğiniz bir [dizin oluşturucu](https://msdn.microsoft.com/library/azure/mt183328.aspx) (desteklenen veri kaynakları için kullanılabilir) veya bir [Ekle, güncelleştirme veya silme belgeleri](https://msdn.microsoft.com/library/azure/dn798930.aspx) işlemi. Merhaba belgeleri gönderilen ters hello dizin oluşturulur.

**Not**: hello dizinleri izin verilen maksimum sayısı değişir fiyatlandırma katmanı tarafından. Merhaba ücretsiz hizmet too3 dizinlerini sağlar. Standart hizmeti arama hizmeti başına 50 dizinleri sağlar. Bkz: [sınırları ve kısıtlamaları](http://msdn.microsoft.com/library/azure/dn798934.aspx) Ayrıntılar için.

**İstek**

HTTPS tüm hizmet istekleri için gereklidir. Merhaba **Create Index** isteği POST veya PUT yöntemini kullanan olacak oluşturulan. POST kullanırken hello dizin şeması tanımı birlikte hello istek gövdesinde bir dizin adı sağlamanız gerekir. PUT ile Merhaba dizin adı hello URL bir parçasıdır. Merhaba dizin yoksa, oluşturulur. Zaten varsa, güncelleştirilmiş toohello yeni tanımı var.

Merhaba dizin adı gerekir küçük olması, bir harf veya sayı ile başlamalı, hiçbir eğik çizgi veya nokta olan ve 128 karakterden kısa olmalıdır. Merhaba tire ardışık olmayan sürece hello dizin adı bir harf veya sayı ile başlattıktan sonra hello rest hello adının herhangi harf, sayı ve kısa çizgi, içerebilir.

Merhaba `api-version` gereklidir. Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) kullanılabilir sürümlerin listesi için.

**İstek üstbilgileri**

liste aşağıdaki hello hello gerekli ve isteğe bağlı istek üstbilgileri açıklar.

* `Content-Type`: Gerekli. Bu çok ayarlama`application/json`
* `api-key`: Gerekli. Merhaba `api-key` için kullanılır
* Merhaba isteği tooyour arama hizmeti kimlik doğrulaması. Bu bir dize değeri, benzersiz tooyour hizmeti olur. Merhaba **Create Index** isteği içermelidir bir `api-key` üstbilgi tooyour yönetici anahtarını (karşılıklı tooa sorgu anahtarı) olarak ayarlayın.

Merhaba hizmet adı tooconstruct hello istek URL'si de gerekir. Her iki hello hizmet adı alabilir ve `api-key` hizmeti Panonuzda hello Azure Portalı'ndan. Bkz: [hello portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.

<a name="RequestData"></a>
**İstek gövdesi sözdizimi**

veri türleri, öznitelikler yanı sıra, isteğe bağlı bir profilleri Puanlama listesi bu dizine beslenecek belgeleri içindeki veri alanlarını hello listesini içeren bir şema tanımı Hello hello istek gövdesini içeren, belgeleri eşleşen kullanılan tooscore Sorgu saati.

Bir POST isteği unutmayın, hello istek gövdesinde hello dizin adı belirtmeniz gerekir.

Yalnızca olabilir bir anahtar alanı hello dizininde. Bir dize alanı toobe içeriyor. Bu alan hello dizini içinde depolanan her belge için benzersiz tanımlayıcı hello temsil eder.

Merhaba ana dizin bölümlerini hello şunları içerir:

* `name`
* `fields`Bu ad, veri türü ve bu alan izin verilen eylemleri tanımlayan özellikleri dahil olmak üzere bu dizinine beslenecek.
* `suggesters`otomatik tamamlamayı veya yazarken tamamlanan sorgular için kullanılır.
* `scoringProfiles`Derecelendirme özel arama puanı için kullanılır. Bkz: [Puanlama profili Ekle](https://msdn.microsoft.com/library/azure/dn798928.aspx) Ayrıntılar için.
* `analyzers`, `charFilters`, `tokenizers`, `tokenFilters` nasıl belgeleri/sorgularınızı bozuk dizine ve arama yapılabilir belirteçlere toodefine kullanılır. Bkz: [analiz Azure Search'te](https://aka.ms//azsanalysis) Ayrıntılar için.
* `defaultScoringProfile`toooverwrite hello varsayılan davranışlar Puanlama kullanılır.
* `corsOptions`dizininizi tooallow çıkış noktaları arası sorguları.

Merhaba isteği yükü yapılandırılması hello söz dizimi aşağıdaki gibidir. Örnek istek, bu konuda daha üzerinde sağlanır.

    {
      "name": (optional on PUT; required on POST) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false,              
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }

**Dizin öznitelikleri**

Merhaba aşağıdaki öznitelikleri dizin oluşturulurken ayarlanabilir. Puanlama ve puanlama profilleri hakkında daha fazla bilgi için bkz [eklemek profilleri Puanlama](https://msdn.microsoft.com/library/azure/dn798928.aspx).

`name`-Ayarlar hello alanın adını hello.

`type`-Ayarlar hello alanın veri türünü hello.

`searchable`-Hello alan tam metin arama yapabilir işaretler. Başka bir deyişle, dizin oluşturma sırasında sözcük bölme gibi analiz yapılacaktır. Ayarlarsanız bir `searchable` alan tooa değeri "güneşli gün" gibi dahili olarak "güneşli" ve "gün" Merhaba tek tek belirteçlere bölme. Bu, bu koşulları için tam metin araması sağlar. Türünde alanlar `Edm.String` veya `Collection(Edm.String)` olan `searchable` varsayılan olarak. Diğer türleri alanlarının olamaz `searchable`.

* **Not**: `searchable` alanları Azure arama için tam metin araması hello alan değeri ek parçalanmış sürümünü depolayacak beri dizininizdeki ek boşluk kullanma. Toosave alanı istiyorsanız dizininizi ve aramaların içinde yer alan toobe gerekmez, Ayarla `searchable` çok`false`.

`filterable`-Başvurulan hello alan toobe sağlayan `$filter` sorgular. `filterable`farklı `searchable` dizeleri işlenme içinde. Türünde alanlar `Edm.String` veya `Collection(Edm.String)` olan `filterable` yalnızca tam eşleşme için karşılaştırmaları; bu nedenle Sözcük bölünmesi, uygulanabilecek değil. Örneğin, böyle bir alan ayarlarsanız `f` çok "güneşli gün", `$filter=f eq 'sunny'` herhangi bir eşleşme bulur ancak `$filter=f eq 'sunny day'` olur. Tüm alanlar `filterable` varsayılan olarak.

`sortable`-Varsayılan olarak hello sistem sonuçları puana göre sıralar, ancak birçok deneyimlerinde toosort hello belgelerde alanlara göre kullanıcılar isteyeceksiniz. Türünde alanlar `Collection(Edm.String)` olamaz `sortable`. Diğer tüm alanlar `sortable` varsayılan olarak.

`facetable`-Genellikle kategorisini (örneğin, dijital kamera ve bakın isabet marka tarafından megapiksel tarafından fiyat, vb. göre arayın.) tarafından isabet sayısı içeren sunu arama sonuçlarının kullanılır. Bu seçenek türü alanlarla kullanılamaz `Edm.GeographyPoint`. Diğer tüm alanlar `facetable` varsayılan olarak.

* **Not**: türünde alanlar `Edm.String` olan `filterable`, `sortable`, veya `facetable` 32 KB cinsinden uzunluğu en fazla olabilir. Bu tür alanları tek arama terimi olarak kabul edilir ve Azure Search'te bir terim hello en fazla 32 KB olduğundan budur. Bu tek bir dize alanda daha fazla metni toostore gerekiyorsa, tooexplicitly gerekir ayarlamak `filterable`, `sortable`, ve `facetable` çok`false` , dizin tanımında.
* **Not**: alan hello yukarıdaki hiçbiri sahipse özniteliklerini çok Ayarla`true` (`searchable`, `filterable`, `sortable`, veya`facetable`) hello alan ters hello dizinden etkili bir şekilde dışlandı. Bu seçenek, sorgularda kullanılmaz, ancak arama sonuçlarında gerekli alanlar için kullanışlıdır. Bu tür alanları hello dizinden hariç performansı artırır.

`key`-İşaretleri hello dizini içinde belgeleri için benzersiz tanımlayıcı içeren olarak alan hello. Hello yalnızca bir alanın seçilen `key` alanı ve türü olması gerektiği `Edm.String`. Anahtar alanları için kullanılan toolook belgeleri doğrudan hello aracılığıyla yukarı olabilir [arama API](#LookupAPI).

`retrievable`-Hello alan bir arama sonucunda döndürülebilecek olup olmadığını belirler.  Sıralama veya mekanizması Puanlama toouse alan (örneğin, kenar boşluğu) bir filtre olarak istiyor ancak hello alan toobe görünür toohello son kullanıcı istemiyorsanız bu yararlıdır. Bu öznitelik olmalıdır `true` için `key` alanları.

`analyzer`-Ayarlar hello Çözümleyicisi toouse adını hello alan için arama süresini ve dizin oluşturma zamanında hello. Değer kümesi izin Merhaba bkz [çözümleyiciler](https://msdn.microsoft.com/library/mt605304.aspx). Bu seçenek yalnızca kullanılabilir `searchable` alanları ve ayarlanamaz birlikte ya da `searchAnalyzer` veya `indexAnalyzer`.  Merhaba Çözümleyicisi seçilen sonra hello alanı değiştirilemez.

`searchAnalyzer`-Ayarlar hello Çözümleyicisi hello alan için arama zamanında kullanılan adını hello. Değer kümesi izin Merhaba bkz [çözümleyiciler](https://msdn.microsoft.com/library/mt605304.aspx). Bu seçenek yalnızca kullanılabilir `searchable` alanları. İle birlikte ayarlanmalıdır `indexAnalyzer` ve hello birlikte ayarlanamaz `analyzer` seçeneği. Bu çözümleyici varolan alan güncelleştirilebilir.

`indexAnalyzer`-Ayarlar hello Çözümleyicisi hello alan için dizin oluşturma zamanında kullanılan adını hello. Değer kümesi izin Merhaba bkz [çözümleyiciler](https://msdn.microsoft.com/library/mt605304.aspx). Bu seçenek yalnızca kullanılabilir `searchable` alanları. İle birlikte ayarlanmalıdır `searchAnalyzer` ve hello birlikte ayarlanamaz `analyzer` seçeneği. Merhaba Çözümleyicisi seçilen sonra hello alanı değiştirilemez.

`suggesters`-Ayarlar arama modu ve öneriler için Merhaba içeriğine hello kaynak alanlar hello. Bkz: [ilgili](#Suggesters) Ayrıntılar için.

`scoringProfiles`-Hangi öğelerin arama sonuçlarında daha yüksek görünür etkilemek sağlayan özel Puanlama davranışları tanımlar. Puanlama profili, alan ağırlığı ve işlevleri yapılır. Bkz: [eklemek profilleri Puanlama](https://msdn.microsoft.com/library/azure/dn798928.aspx) Puanlama profilinde kullanılan hello öznitelikleri hakkında daha fazla bilgi.

<!-- This is a standalone topic in MSDN -->
<a name="LanguageSupport"></a>
**Dil desteği**

Aranabilir alanlara analiz uygulanabilecek en sık Sözcük bölünmesi, metin normalleştirme ve koşulları filtreleme ilgilidir. Varsayılan olarak, Azure Search aranabilir alanlara hello analiz edilen [Apache Lucene standart Çözümleyicisi](http://lucene.apache.org/core/4_9_0/analyzers-common/index.html) aşağıdaki elemanlara metni keser["Unicode metin kesimleme"](http://unicode.org/reports/tr29/) kuralları. Ayrıca, tüm karakterleri tootheir küçük form hello standart Çözümleyicisi dönüştürür. Dizinlenmiş belgeleri ve arama terimlerini hello analiz dizin oluşturma ve sorgu işleme sırasında gidin.

Azure arama, çeşitli dillerde destekler. Her dil için belirli bir dil özellikleri hesapları bir standart metin Çözümleyicisi gerektirir. Azure arama çözümleyiciler iki tür sunar:

* 35 çözümleyiciler Lucene tarafından yedeklenir.
* Office ve Bing kullanılan teknoloji işleme özel Microsoft doğal dil desteğiyle 50 Çözümleyicileri.

Bazı geliştiriciler tercih edebilirsiniz hello Lucene daha tanıdık, basit, açık kaynaklı çözüm. Lucene çözümleyiciler hızlıdır, ancak hello Microsoft çözümleyiciler Gelişmiş lemmatization gibi özellikleri vardır, word (dillerde Almanca, Danca, Felemenkçe, İsveççe, Norveççe, Estonca, bitiş, Macarca, Slovakça gibi) decompounding ve varlık tanıma (URL'leri e-postalar, tarihler, sayılar). Mümkünse, hangisinin daha iyi bir uyum olan iki hello Microsoft ve Lucene çözümleyiciler toodecide karşılaştırmaları çalıştırmanız gerekir.

***Nasıl Karşılaştır***

İngilizce için Hello Lucene Çözümleyicisi hello standart Çözümleyicisi genişletir. ('S sondaki) iyelik sözcükleri kaldırır, göre kaynaklanan geçerlidir [bağlantısı kaynaklanan algoritması](http://tartarus.org/~martin/PorterStemmer/)ve İngilizce kaldırır [durdurma sözcükleri](http://en.wikipedia.org/wiki/Stop_words).

Buna karşılık, hello Microsoft Çözümleyicisi kaynaklanan yerine lemmatization gerçekleştirir. Bunu işleyebilir bükümlü ve düzensiz sözcük formlarını daha iyi ne daha ilgili arama sonuçlarında sonuçları anlamına gelir (izleme modülünü 7 [Azure arama MVA sunu](http://www.microsoftvirtualacademy.com/training-courses/adding-microsoft-azure-search-to-your-websites-and-apps) daha fazla ayrıntı için).

İle Microsoft çözümleyiciler dizin ortalama iki toothree Lucene eşdeğerlerine hello dil bağlı olarak daha yavaş katıdır. Arama performansını önemli ölçüde ortalama boyutu sorgularında etkilenmemesi gerekir.

***Yapılandırma***

Merhaba dizin tanımı'ndaki her bir alan için hello ayarlayabilirsiniz `analyzer` hangi dil ve satıcı belirtir özellik tooan Çözümleyicisi adı. Merhaba aynı Çözümleyicisi dizin oluşturma ve bu alan için arama uygulanır.
Örneğin, yana birimi hello içinde mevcut İngilizce, Fransızca ve İspanyolca otel açıklamaları için ayrı alanları olabilir aynı dizin. Kullanım hello ['searchFields' sorgu parametresi](#SearchQueryParameters) toospecify hangi dile özgü alan toosearch karşı sorgularınızı. Merhaba dahil sorgu örnekler gözden geçirebilirsiniz `analyzer` özelliğinde [Search belgeleri](#SearchDocs). 

***Çözümleyici listesi***

Merhaba Lucene ve Microsoft Çözümleyicisi adları ile birlikte desteklenen dillerin listesi aşağıdadır.

<table style="font-size:12">
    <tr>
        <th>Dil</th>
        <th>Microsoft Çözümleyicisi adı</th>
        <th>Lucene Çözümleyicisi adı</th>
    </tr>
    <tr>
        <td>Arapça</td>
        <td>ar.Microsoft</td>
        <td>ar.lucene</td>        
    </tr>
    <tr>
        <td>Ermenice</td>
        <td></td>
        <td>hy.lucene</td>
      </tr>
    <tr>
        <td>Bangla</td>
        <td>Bn.Microsoft</td>
        <td></td>
    </tr>
      <tr>
        <td>Bask dili</td>
        <td></td>
        <td>EU.lucene</td>
    </tr>
      <tr>
         <td>Bulgarca</td>
        <td>BG.Microsoft</td>
        <td>BG.lucene</td>
      </tr>
      <tr>
        <td>Katalanca</td>
        <td>CA.Microsoft</td>
        <td>CA.lucene</td>          
      </tr>
    <tr>
        <td>Basitleştirilmiş Çince</td>
        <td>zh-Hans.microsoft</td>
        <td>zh-Hans.lucene</td>        
    </tr>
    <tr>
        <td>Geleneksel Çince</td>
        <td>zh-Hant.microsoft</td>
        <td>zh-Hant.lucene</td>        
    <tr>
    <tr>
        <td>Hırvatça</td>
        <td>hr.Microsoft</td>
        <td/></td>
    </tr>
    <tr>
        <td>Çekçe</td>
        <td>cs.Microsoft</td>
        <td>cs.lucene</td>        
    </tr>    
    <tr>
        <td>Danca</td>
        <td>da.Microsoft</td>
        <td>da.lucene</td>        
    </tr>    
    <tr>
        <td>Hollanda dili</td>
        <td>NL.Microsoft</td>
        <td>NL.lucene</td>    
    </tr>    
    <tr>
        <td>Türkçe</td>        
        <td>en.Microsoft</td>
        <td>en.lucene</td>        
    </tr>
    <tr>
        <td>Estonca</td>
        <td>et.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Fince</td>
        <td>Fi.Microsoft</td>
        <td>Fi.lucene</td>        
    </tr>    
    <tr>
        <td>Fransızca</td>
        <td>fr.Microsoft</td>
        <td>fr.lucene</td>        
    </tr>
    <tr>
        <td>Galiçya lehçesi</td>
        <td></td>
        <td>GL.lucene</td>        
      </tr>
    <tr>
        <td>Almanca</td>
        <td>de.Microsoft</td>
        <td>de.lucene</td>        
    </tr>
    <tr>
        <td>Yunanca</td>
        <td>el.Microsoft</td>
        <td>el.lucene</td>        
    </tr>
    <tr>
        <td>Gucerat dili</td>
        <td>gu.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>İbranice</td>
        <td>He.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Hintçe</td>
        <td>Hi.Microsoft</td>
        <td>Hi.lucene</td>        
    </tr>
    <tr>
        <td>Macarca</td>        
        <td>hu.Microsoft</td>
        <td>hu.lucene</td>
    </tr>
    <tr>
        <td>İzlanda dili</td>
        <td>is.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Endonezya dili (Bahasa)</td>
        <td>id.Microsoft</td>
        <td>id.lucene</td>        
    </tr>
    <tr>
        <td>İrlanda dili</td>
        <td></td>
          <td>GA.lucene</td>
    </tr>
    <tr>
        <td>İtalyanca</td>
        <td>it.Microsoft</td>
        <td>it.lucene</td>        
    </tr>
    <tr>
        <td>Japonca</td>
        <td>ja.Microsoft</td>
        <td>ja.lucene</td>

    </tr>
    <tr>
        <td>Kannada dili</td>
        <td>Ka.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Kore dili</td>
        <td>Ko.Microsoft</td>
        <td>Ko.lucene</td>
    </tr>
    <tr>
        <td>Letonca</td>        
        <td>LV.Microsoft</td>
        <td>LV.lucene</td>    
    </tr>
    <tr>
        <td>Litvanca</td>
        <td>lt.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Malayalam dili</td>
        <td>ML.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Malay (Latin)</td>
        <td>MS.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Marathi</td>
        <td>Mr.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Norveççe</td>
        <td>NB.Microsoft</td>
        <td>No.lucene</td>        
    </tr>
      <tr>
        <td>Farsça</td>
        <td></td>
        <td>FA.lucene</td>        
      </tr>
    <tr>
        <td>Lehçe</td>
        <td>PL.Microsoft</td>
        <td>PL.lucene</td>        
    </tr>
    <tr>
        <td>Portekizce (Brezilya)</td>
        <td>PT Br.microsoft</td>
        <td>PT Br.lucene</td>        
    </tr>
    <tr>
        <td>Portekizce (Portekiz)</td>
        <td>PT Pt.microsoft</td>        
        <td>PT Pt.lucene</td>
    </tr>
    <tr>
        <td>Pencap dili</td>
        <td>Pa.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Rumence</td>
        <td>Ro.Microsoft</td>
        <td>Ro.lucene</td>
    </tr>
    <tr>
        <td>Rusça</td>
        <td>RU.Microsoft</td>
        <td>RU.lucene</td>    
    </tr>
    <tr>
        <td>Sırpça (Kiril)</td>
        <td>SR-cyrillic.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Sırpça (Latin)</td>
        <td>SR-latin.microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Slovakça</td>
        <td>SK.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Slovence</td>
        <td>SL.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>İspanyolca</td>
        <td>Es.Microsoft</td>
        <td>Es.lucene</td>
    </tr>
    <tr>
        <td>İsveç dili</td>
        <td>sv.Microsoft</td>
        <td>sv.lucene</td>
    </tr>

    <tr>
        <td>Tamil dili</td>
        <td>ta.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Telugu dili</td>
        <td>te.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Tay dili</td>
        <td>TH.Microsoft</td>
        <td>TH.lucene</td>
    </tr>
    <tr>
        <td>Türkçe</td>
        <td>tr.Microsoft</td>
        <td>tr.lucene</td>        
    </tr>
    <tr>
        <td>Ukrayna dili</td>
        <td>UK.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Urduca</td>
        <td>Your.Microsoft</td>
        <td></td>
    </tr>
    <tr>
        <td>Vietnam dili</td>
        <td>vi.Microsoft</td>
        <td></td>
    </tr>
    <td colspan="3">Ayrıca Azure Search dilden bağımsız çözümleyicisi yapılandırmalarını sağlar</td>
    <tr>
        <td>Standart ASCII Katlama</td>
        <td>standardasciifolding.lucene</td>
        <td>
        <ul>
            <li>Unicode metin kesimleme (standart belirteç Oluşturucu)</li>
            <li>ASCII kırılma filtresi - toohello ilk 127 ASCII karakter kümesi ASCII eşdeğerlerine ait olmayan Unicode karakterler dönüştürür. Bu, Aksan kaldırmak için kullanışlıdır.</li>
        </ul>
        </td>
    </tr>
</table>

İle ek açıklama adları olan tüm çözümleyiciler <i>lucene</i> tarafından sağlanmıştır [Apache Lucene'nın dil Çözümleyicileri](http://lucene.apache.org/core/4_9_0/analyzers-common/overview-summary.html). Filtre Katlama hello ASCII hakkında daha fazla bilgi bulunabilir [burada](http://lucene.apache.org/core/4_9_0/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html).

**Öneri araçları**

A `suggester` bir dizindeki hangi alanların kullanılan toosupport aramalarda otomatik tamamlama olduğunu tanımlar. Kısmi arama dizelerini toohello genellikle gönderilen [önerileri API](#Suggestions) hello kullanıcı bir arama sorgusu yazarak ve hello API önerilen tümcecikleri bir dizi döndürür. Merhaba dizinde tanımladığınız bir öneri aracı hangi alanların kullanılan toobuild hello yazarken tamamlanan arama terimleri olduğunu belirler. Bkz: [ilgili](#Suggesters) yapılandırma ayrıntıları için.

**Puanlama modelleri**

A `scoringProfile` hangi öğelerin görünür hello arama sonuçlarında daha yüksek etkilemek sağlayan özel Puanlama davranışları tanımlar. Puanlama profili, alan ağırlığı ve işlevleri yapılır. toouse bunları, hello sorgu dizesi adına göre bir profili belirttiğiniz.

Puanlama profili varsayılan sonuç kümesinde her öğe için bir arama puanı hello planda toocompute çalışır. Merhaba iç, adlandırılmamış Puanlama profili kullanabilirsiniz. Alternatif olarak, kümesinin `defaultScoringProfile` toouse özel bir profil hello varsayılan olarak özel bir profil hello sorgu dizesinde belirtilmediğinde çağrılır.

Bkz: [Ekle Puanlama profilleri tooa arama dizini (Azure Search Hizmeti REST API'si)](search-api-scoring-profiles-2015-02-28-preview.md) Ayrıntılar için.

**CORS seçenekleri**

Merhaba tarayıcı tüm çıkış noktaları arası istekleri engeller istemci tarafı Javascript herhangi API'leri varsayılan olarak çağrılamaz. CORS (çıkış noktaları arası kaynak paylaşımı) ayarı hello tarafından etkinleştirmek `corsOptions` öznitelik tooallow çıkış noktaları arası sorguları tooyour dizini. Yalnızca bu sorguyu güvenlik nedeniyle CORS desteğini API'leri unutmayın. Seçenekler aşağıdaki hello için CORS ayarlayabilirsiniz:

* `allowedOrigins`(gerekli): Bu bir erişim tooyour dizin verilecek çıkış noktaları listesidir. Bu, bu çıkış noktalarından sunulacak tüm Javascript kodlarının olacaktır anlamına gelir izin tooquery dizininizi (Merhaba doğru API anahtarını verdiği varsayılarak). Her bir çıkış noktası genellikle hello biçimidir `protocol://fully-qualified-domain-name:port` ancak başlangıç bağlantı noktası çoğunlukla yazılmaz. Bkz: [bu makalede](http://go.microsoft.com/fwlink/?LinkId=330822) daha fazla ayrıntı için.
  * Tooallow erişim tooall çıkış istiyorsanız ekleyin `*` hello içinde tek bir öğe olarak `allowedOrigins` dizi. Unutmayın **bu yöntem üretim arama hizmetleri için önerilmez.** Ancak, geliştirme veya hata ayıklama için yararlı olabilir.
* `maxAgeInSeconds`(isteğe bağlı): tarayıcılar bu değeri toodetermine hello süresi (saniye) toocache CORS denetim öncesi yanıtlarını kullanır. Bu, negatif olmayan bir tamsayı olmalıdır. Merhaba büyük hello daha iyi performans bu değer olur, ancak hello uzun CORS İlkesi değişiklikleri tootake için etkili. Ayarlanmazsa, varsayılan süre olan 5 dakika kullanılır.

<a name="CreateUpdateIndexExample"></a>
**İstek gövdesi örneği**

    {
      "name": "hotels",  
      "fields": [
        {"name": "hotelId", "type": "Edm.String", "key": true, "searchable": false},
        {"name": "baseRate", "type": "Edm.Double"},
        {"name": "description", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false},
        {"name": "description_fr", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "analyzer": "fr.lucene"},
        {"name": "hotelName", "type": "Edm.String"},
        {"name": "category", "type": "Edm.String"},
        {"name": "tags", "type": "Collection(Edm.String)"},
        {"name": "parkingIncluded", "type": "Edm.Boolean"},
        {"name": "smokingAllowed", "type": "Edm.Boolean"},
        {"name": "lastRenovationDate", "type": "Edm.DateTimeOffset"},
        {"name": "rating", "type": "Edm.Int32"},
        {"name": "location", "type": "Edm.GeographyPoint"}
      ],
      "suggesters": [
        {
          "name": "sg",
          "searchMode": "analyzingInfixMatching",
          "sourceFields": ["hotelName"]
        }
      ]
    }

**Yanıt**

Başarılı bir istek için: "201 oluşturuldu".

Varsayılan olarak oluşturulan hello dizin tanımı için JSON hello hello yanıt gövdesi içerir. Merhaba, `Prefer` istek üstbilgisi çok ayarlamak`return=minimal`hello yanıt gövdesi boş olacaktır ve hello başarı durum kodu olacaktır "204 İçerik" yerine "201 oluşturuldu". Bu, PUT veya POST kullanılan toocreate hello dizin olmasına bakılmaksızın geçerlidir.

**Açıklamalar**

Şu anda, sınırlı dizin şeması güncelleştirmelerini desteği yoktur. Alan türlerinin değiştirilmesi gibi yeniden dizinlemeyi gerektiren hiçbir şema güncelleştirmesi şu anda desteklenmiyor. Var olan alanları silinmiş veya değiştirilemez rağmen yeni alanlar herhangi bir zamanda tooan varolan bir dizini eklenebilir. Yeni bir alan eklediğinizde hello dizindeki tüm mevcut belgeleri otomatik olarak bu alan için bir null değer sahip olacaktır. Yeni belgeler toohello dizin ekleninceye kadar hiçbir ek depolama alanı tüketilebilir.

<a name="Suggesters"></a>

## <a name="suggesters"></a>Öneri Araçları
Merhaba önerileri özellik Azure Search, arama kutusuna girilen yanıt toopartial dize girdileri olası arama terimlerini listesini sağlayan yazarken tamamlanan veya otomatik tamamlama sorgusu yetenektir. Büyük olasılıkla Sorgu önerileri ticari web arama motorları kullanılırken fark: Bing içinde ".NET" yazarak üreten koşulları listesini ".NET 4.5", ".NET Framework 3,5", vb.. Merhaba arama hizmeti REST API kullanırken, özel bir Azure Search uygulamada önerileri uygulama hello aşağıdakileri gerektirir:

* Ekleyerek önerilerini etkinleştirmek bir **öneri aracı** hello adı, arama modu ve alanların listesi için yazarken tamamlanan vermiş dizininizdeki yapım çağrılır. Kısmi arama dizesi "Sea" yazarak bir kaynak alanı olarak "ŞehirAdı" "Seattle" sonuçlanır belirtirseniz, örneğin, "Sahil" ve "Seatac" (üçü gerçek Şehir adları) Sorgu önerileri toohello kullanıcı olarak sunulan.
* Öneriler tarafından arama hello çağırma [önerileri API](#Suggestions) , uygulama kodunuzda. Genellikle kısmi arama dizelerini hello kullanıcı bir arama sorgusu yazıyor ve bu API önerilen tümcecikleri kümesini döndürür toohello hizmet gönderilir.

Bu makalede açıklanır nasıl tooconfigure bir **öneri aracı**. Merhaba da gözden geçirmelisiniz [önerileri API](#Suggestions) bir öneri Aracı nasıl kullanıldığı hakkında bilgi.

**Kullanım**

`Suggesters`Merhaba dizinde oluşturulur ve kullanıldığında en iyi şekilde çalışır toosuggest özel belgeler gevşek terimleri veya tümcecikleri yerine. Merhaba en iyi adayı başlıklar, adları ve bir öğe tanımlayabilir diğer görece kısa tümceleri alanlardır. Kategoriler ve etiketler gibi yinelenen alanları veya çok uzun alanları açıklamaları veya açıklamalar alanları gibi daha az etkili olur.

Merhaba dizin tanımının bir parçası olarak, bir tek öneri aracı toohello ekleyebilirsiniz `suggesters` koleksiyonu. Bir öneri aracı tanımlayan özellikleri hello şunları içerir:

* `name`: hello hello öneri aracı adını. Merhaba çağırırken hello hello öneri aracı adını kullanmak `suggest` API.
* `searchMode`: aday tümcecikleri için kullanılan strateji toosearch hello. Merhaba şu anda desteklenen tek mod olan `analyzingInfixMatching`, hello başında veya tümcelerin hello ortasında esnek eşleştirilmesini gerçekleştirir.
* `sourceFields`: Merhaba kaynak önerileri için Merhaba içeriğine bir veya daha fazla alanlar bir listesi. Yalnızca türünde alanlar `Edm.String` ve `Collection(Edm.String)` kaynakları önerileri için olabilir. Ayarlama özel bir dil Çözümleyicisi sahip olmayan alanlar kullanılabilir.

**Öneri aracı örneği**

Bir öneri aracı hello dizini bir parçasıdır. Yalnızca bir öneri aracı hello mevcut `suggesters` hello yanında hello geçerli sürümü koleksiyonda koleksiyon alanları ve `scoringProfiles`.

        {
          "name": "hotels",
          "fields": [
             . . .
           ],
          "suggesters": [
            {
            "name": "sg",
            "searchMode": "analyzingInfixMatching",
            "sourceFields: ["hotelName", "category"]
            }
          ],
          "scoringProfiles": [
             . . .
          ]
        }

> [!NOTE]
> Azure Search hello genel Önizleme sürümü kullandıysanız `suggesters` daha eski bir boolean özelliği değiştirir (`"suggestions": false`), yalnızca desteklenen önek önerileri için kısa dizeleri (3-25 karakter). Kendi değiştirme `suggesters`, destekler infix hello başında veya hello ortasında yer alan içeriği, bir arama dizelerini hatalar için daha iyi tolerans ile eşleşen terimleri bulan eşleşen. Merhaba genel olarak kullanılabilir sürümünden başlayarak, bunu şimdi hello yalnızca hello önerileri API uygulamasıdır. Merhaba eski `suggestions` sunulmuştur özelliği `api-version=2014-07-31-Preview` toowork bu sürümde devam eder, ancak hello işlemsel değil `2015-02-28` veya Azure Search'ın sonraki sürümleri.
> 
> 

<a name="UpdateIndex"></a>

## <a name="update-index"></a>Dizini Güncelleştir
Bir HTTP PUT İsteği kullanarak Azure Search'te içinde varolan bir dizin güncelleştirebilirsiniz. Güncelleştirmeler CORS seçenekleri değiştirme ve puanlama profilleri değiştirme yeni alanları toohello varolan şema, ekleme içerebilir. Bkz: [eklemek profilleri Puanlama](https://msdn.microsoft.com/library/azure/dn798928.aspx) daha fazla bilgi için. Merhaba istek URI'SİNDEKİ hello dizin tooupdate hello adını belirtin:

    PUT https://[search service url]/indexes/[index name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

**Önemli:** dizin şeması güncelleştirmelerini desteğidir hello arama dizinini yeniden oluşturmayı gerektirmeyen sınırlı toooperations. Alan türlerinin değiştirilmesi gibi yeniden dizinlemeyi gerektiren hiçbir şema güncelleştirmesi şu anda desteklenmiyor. Var olan alanları değiştirilmiş veya silinemez ancak herhangi bir zamanda yeni alanlar eklenebilir. Merhaba aynı çok geçerlidir`suggesters`. Yeni alanlar eklenebilir, başlangıç saati hello alanlarındaki tooa öneri aracı eklenir, ancak alanları öğesinden kaldırılamaz `suggesters` ve var olan alanları çok eklenemez`suggesters`.

Yeni bir alan tooan dizin eklerken hello dizindeki tüm mevcut belgeleri otomatik olarak bu alan için bir null değer sahip olacaktır. Yeni belgeler toohello dizin ekleninceye kadar hiçbir ek depolama alanı tüketilebilir.

**İstek**

HTTPS tüm hizmet istekleri için gereklidir. Merhaba **güncelleştirme dizin** isteği HTTP PUT kullanarak oluşturulur. PUT ile Merhaba dizin adı hello URL bir parçasıdır. Merhaba dizin yoksa, oluşturulur. Merhaba dizini zaten varsa, güncelleştirilmiş toohello yeni tanımı var.

Merhaba dizin adı gerekir küçük olması, bir harf veya sayı ile başlamalı, hiçbir eğik çizgi veya nokta olan ve 128 karakterden kısa olmalıdır. Merhaba tire ardışık olmayan sürece hello dizin adı bir harf veya sayı ile başlattıktan sonra hello rest hello adının herhangi harf, sayı ve kısa çizgi, içerebilir.

`api-version=[string]`(gerekli). Merhaba Önizleme sürümü `api-version=2015-02-28-Preview`. Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri için.

**İstek üstbilgileri**

liste aşağıdaki hello hello gerekli ve isteğe bağlı istek üstbilgileri açıklar.

* `Content-Type`: Gerekli. Bu çok ayarlama`application/json`
* `api-key`: Gerekli. Merhaba `api-key` kullanılan tooauthenticate hello isteği tooyour arama hizmeti değil. Bu bir dize değeri, benzersiz tooyour hizmeti olur. Merhaba **güncelleştirme dizin** isteği içermelidir bir `api-key` üstbilgi tooyour yönetici anahtarını (karşılıklı tooa sorgu anahtarı) olarak ayarlayın.

Merhaba hizmet adı tooconstruct hello istek URL'si de gerekir. Merhaba hizmet adı alabilir ve `api-key` hizmeti Panonuzda hello Azure Portalı'ndan. Bkz: [hello portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.

**İstek gövdesi sözdizimi**

Varolan bir dizini güncelleştirirken hello gövde hello özgün şema tanımı içermelidir artı hello yanı sıra, eklemekte olduğunuz hello yeni alanlar varsa Puanlama profilleri, ilgili ve CORS seçenekleri değiştirdi. Merhaba Puanlama profilleri ve CORS seçenekleri değiştirme değil, başlangıç dizini oluşturulduğu gelen hello orijinal eklemeniz gerekir. Genel güncelleştirmeleri için en iyi düzeni toouse hello tooretrieve hello dizini GET tanımıdır, değiştirin ve sonra PUT ile güncelleştirin.

Merhaba şema sözdizimi dizin burada çoğaltılamaz toocreate kolaylık sağlamak için kullanılır. Bkz: [Create Index](#CreateIndex) daha fazla ayrıntı için.

    {
      "name": (optional) "name_of_index",
      "fields": [
        {
          "name": "name_of_field",
          "type": "Edm.String | Collection(Edm.String) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
          "searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
          "filterable": true (default) | false,
          "sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
          "facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
          "key": true | false (default, only Edm.String fields can be keys),
          "retrievable": true (default) | false, 
          "analyzer": "name of hello analyzer used for search and indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
          "searchAnalyzer": "name of hello search analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
          "indexAnalyzer": "name of hello indexing analyzer" (only if 'searchAnalyzer' is set and 'analyzer' is not set)
        }
      ],
      "suggesters": [
        {
          "name": "name of suggester",
          "searchMode": "analyzingInfixMatching" (other modes may be added in hello future),
          "sourceFields": ["field1", "field2", ...]
        }
      ],
      "scoringProfiles": [
        {
          "name": "name of scoring profile",
          "text": (optional, only applies toosearchable fields) {
            "weights": {
              "searchable_field_name": relative_weight_value (positive numbers),
              ...
            }
          },
          "functions": (optional) [
            {
              "type": "magnitude | freshness | distance | tag",
              "boost": # (positive number used as multiplier for raw score != 1),
              "fieldName": "...",
              "interpolation": "constant | linear (default) | quadratic | logarithmic",
              "magnitude": {
                "boostingRangeStart": #,
                "boostingRangeEnd": #,
                "constantBoostBeyondRange": true | false (default)
              },
              "freshness": {
                "boostingDuration": "..." (value representing timespan leading toonow over which boosting occurs)
              },
              "distance": {
                "referencePointParameter": "...", (parameter toobe passed in queries toouse as reference location, see "scoringParameter" for syntax details)
                "boostingDistance": # (hello distance in kilometers from hello reference location where hello boosting range ends)
              },
              "tag": {
                "tagsParameter": "..." (parameter toobe passed in queries toospecify list of tags toocompare against target field, see "scoringParameter" for syntax details)
              }
            }
          ],
          "functionAggregation": (optional, applies only when functions are specified)
            "sum (default) | average | minimum | maximum | firstMatching"
        }
      ],
      "analyzers":(optional)[ ... ],
      "charFilters":(optional)[ ... ],
      "tokenizers":(optional)[ ... ],
      "tokenFilters":(optional)[ ... ],
      "defaultScoringProfile": (optional) "...",
      "corsOptions": (optional) {
        "allowedOrigins": ["*"] | ["origin_1", "origin_2", ...],
        "maxAgeInSeconds": (optional) max_age_in_seconds (non-negative integer)
      }
    }


**Yanıt**

Başarılı bir istek için: "204 İçerik yok".

Varsayılan olarak hello yanıt gövdesi boş olur. Ancak, hello `Prefer` istek üstbilgisi çok ayarlamak`return=representation`, hello yanıt gövdesi Merhaba JSON güncelleştirildi hello dizin tanımını içerir. Bu durumda, hello başarı durum kodu olacak "200 Tamam".

**Dizin tanımı ile özel çözümleyiciler güncelleştiriliyor**

Bir analyzer, bir belirteç Oluşturucu, bir belirteç filtre veya char filtre tanımlandıktan sonra değiştirilemez. Yenilerini yalnızca hello varsa tooan varolan bir dizini eklenebilir `allowIndexDowntime` bayrağı hello dizin güncelleştirme isteğinde tootrue ayarlanır: 

`PUT https://[search service name].search.windows.net/indexes/[index name]?api-version=[api-version]&allowIndexDowntime=true`

Bu işlem en az birkaç saniye olarak, dizin oluşturma neden ve sorgu dizininizi çevrimdışı sokar Not toofail ister. Merhaba dizin performans ve yazma kullanılabilirliğini hello dizin güncelleştirildikten sonra birkaç dakika engelli ya da çok büyük dizinler için daha uzun olabilir.

<a name="ListIndexes"></a>

## <a name="list-indexes"></a>Liste dizinler
Merhaba **listesi dizinleri** işlemi listesi döndürülür hello dizinleri şu anda Azure Search hizmetinizin.

    GET https://[service name].search.windows.net/indexes?api-version=[api-version]
    api-key: [admin key]

**İstek**

HTTPS tüm hizmet istekleri için gereklidir. Merhaba **listesi dizinleri** isteği hello GET yöntemini kullanan olacak oluşturulan.

`api-version=[string]`(gerekli). Merhaba Önizleme sürümü `api-version=2015-02-28-Preview`. Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri için.

**İstek üstbilgileri**

liste aşağıdaki hello hello gerekli ve isteğe bağlı istek üstbilgileri açıklar.

* `api-key`: Gerekli. Merhaba `api-key` kullanılan tooauthenticate hello isteği tooyour arama hizmeti değil. Bu bir dize değeri, benzersiz tooyour hizmeti olur. Merhaba **listesi dizinler** isteği içermelidir bir `api-key` kümesi tooan yönetici anahtarı (karşılıklı tooa sorgu anahtarı).

Merhaba hizmet adı tooconstruct hello istek URL'si de gerekir. Merhaba hizmet adı alabilir ve `api-key` hizmeti Panonuzda hello Azure Portalı'ndan. Bkz: [hello portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.

**İstek gövdesi**

yok.

**Yanıt**

Durum kodu: 200 Tamam için başarılı bir yanıt döndürdü.

Bir örnek yanıt gövdesi şöyledir:

    {
      "value": [
        {
          "name": "Books",
          "fields": [
            {"name": "ISBN", ...},
            ...
          ]
        },
        {
          "name": "Games",
          ...
        },
        ...
      ]
    }

İlgilendiğiniz toojust hello özellikleri aşağı hello yanıt filtreleyebilirsiniz unutmayın. Örneğin, yalnızca dizin adlarının bir listesini istiyorsanız, hello OData kullanın `$select` sorgu seçeneği:

    GET /indexes?api-version=2015-02-28-Preview&$select=name

Bu durumda, yukarıdaki örnek hello hello yanıttan şu şekilde görünür:

    {
      "value": [
        {"name": "Books"},
        {"name": "Games"},
        ...
      ]
    }

Dizinleri çok arama hizmetiniz varsa yararlı yöntem toosave bant genişliği budur.

<a name="GetIndex"></a>

## <a name="get-index"></a>Dizin Al
Merhaba **alma dizin** işlemi Azure aramadan hello dizin tanımını alır.

    GET https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

**İstek**

HTTPS istekleri için gereklidir. Merhaba **alma dizin** isteği hello GET yöntemini kullanan olacak oluşturulan.

Merhaba [dizin adı] hello istek URI'SİNDEKİ hangi dizin tooreturn hello dizinleri koleksiyonundan belirtir.

`api-version=[string]`(gerekli). Merhaba Önizleme sürümü `api-version=2015-02-28-Preview`. Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri için.

**İstek üstbilgileri**

liste aşağıdaki hello hello gerekli ve isteğe bağlı istek üstbilgileri açıklar.

* `api-key`: Merhaba `api-key` kullanılan tooauthenticate hello isteği tooyour arama hizmeti değil. Bu bir dize değeri, benzersiz tooyour hizmeti olur. Merhaba **alma dizin** isteği içermelidir bir `api-key` kümesi tooan yönetici anahtarı (karşılıklı tooa sorgu anahtarı).

Merhaba hizmet adı tooconstruct hello istek URL'si de gerekir. Merhaba hizmet adı alabilir ve `api-key` hizmeti Panonuzda hello Azure Portalı'ndan. Bkz: [hello portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.

**İstek gövdesi**

yok.

**Yanıt**

Durum kodu: 200 Tamam için başarılı bir yanıt döndürdü.

Merhaba örnek JSON içinde [oluşturma ve bir dizin güncelleştirme](#CreateUpdateIndexExample) hello yanıt yükü ilişkin bir örnek.

<a name="DeleteIndex"></a>

## <a name="delete-index"></a>Dizin Sil
Merhaba **silmek dizin** işlemi, Azure Search hizmetinizin dizin ve ilişkili belgeleri kaldırır. Merhaba dizin adı hello hizmet hello Azure portal panosunda veya hello API alabilirsiniz. Bkz: [listesi dizinleri](#ListIndexes) Ayrıntılar için.

    DELETE https://[service name].search.windows.net/indexes/[index name]?api-version=[api-version]
    api-key: [admin key]

**İstek**

HTTPS istekleri için gereklidir. Merhaba **silmek dizin** isteği hello DELETE yöntemini kullanan olacak oluşturulan.

Merhaba [dizin adı] hello istek URI'SİNDEKİ hangi dizin toodelete hello dizinleri koleksiyonundan belirtir.

`api-version=[string]`(gerekli). Merhaba Önizleme sürümü `api-version=2015-02-28-Preview`. Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri için.

**İstek üstbilgileri**

liste aşağıdaki hello hello gerekli ve isteğe bağlı istek üstbilgileri açıklar.

* `api-key`: Gerekli. Merhaba `api-key` kullanılan tooauthenticate hello isteği tooyour arama hizmeti değil. Bir dize değeri, benzersiz tooyour hizmeti URL'si değil. Merhaba **silmek dizin** isteği içermelidir bir `api-key` üstbilgi tooyour yönetici anahtarını (karşılıklı tooa sorgu anahtarı) olarak ayarlayın.

Merhaba hizmet adı tooconstruct hello istek URL'si de gerekir. Merhaba hizmet adı alabilir ve `api-key` hizmeti Panonuzda hello Azure Portalı'ndan. Bkz: [hello portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.

**İstek gövdesi**

yok.

**Yanıt**

Durum kodu: 204 Hayır içerik için başarılı bir yanıt döndürülür.

<a name="GetIndexStats"></a>

## <a name="get-index-statistics"></a>Dizin istatistikleri Al
Merhaba **dizin istatistikleri almak** işlemi hello geçerli dizin yanı sıra, depolama alanı kullanımı için bir belge sayısı Azure aramadan döndürür.

    GET https://[service name].search.windows.net/indexes/[index name]/stats?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> Belge sayısını ve depolama boyutunu istatistiklerle değil gerçek zamanlı olarak birkaç dakikada toplanır. Bu nedenle, bu API tarafından döndürülen hello istatistikleri son dizin oluşturma işlemleri tarafından yapılan değişiklikler neden yansıtmayabilir.
> 
> 

**İstek**

HTTPS tüm hizmetleri istekler için gereklidir. Merhaba **dizin istatistikleri almak** isteği hello GET yöntemini kullanan olacak oluşturulan.

Merhaba [dizin adı] hello istek URI'SİNDEKİ hello hizmet tooreturn dizin istatistikleri hello belirtilen dizin için söyler.

`api-version=[string]`(gerekli). Merhaba Önizleme sürümü `api-version=2015-02-28-Preview`. Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri için.

**İstek üstbilgileri**

liste aşağıdaki hello hello gerekli ve isteğe bağlı istek üstbilgileri açıklar.

* `api-key`: Merhaba `api-key` kullanılan tooauthenticate hello isteği tooyour arama hizmeti değil. Bu bir dize değeri, benzersiz tooyour hizmeti olur. Merhaba **dizin istatistikleri almak** isteği içermelidir bir `api-key` kümesi tooan yönetici anahtarı (karşılıklı tooa sorgu anahtarı).

Merhaba hizmet adı tooconstruct hello istek URL'si de gerekir. Merhaba hizmet adı alabilir ve `api-key` hizmeti Panonuzda hello Azure Portalı'ndan. Bkz: [hello portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.

**İstek gövdesi**

yok.

**Yanıt**

Durum kodu: 200 Tamam için başarılı bir yanıt döndürdü.

Merhaba yanıt gövdesi hello biçimi aşağıdaki gibidir:

    {
      "documentCount": number,
      "storageSize": number (size of hello index in bytes)
    }

<a name="TestAnalyzer"></a>

## <a name="test-analyzer"></a>Testi Çözümleyicisi
Merhaba **analiz API** nasıl bir Çözümleyicisi belirteçlere metni keser. gösterir.

    POST https://[service name].search.windows.net/indexes/[index name]/analyze?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

**İstek**

HTTPS tüm hizmetleri istekler için gereklidir. Merhaba **analiz API** isteği hello POST yöntemini kullanan olacak oluşturulan.

`api-version=[string]`(gerekli). Merhaba Önizleme sürümü `api-version=2015-02-28-Preview`. Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri için.

**İstek üstbilgileri**

liste aşağıdaki hello hello gerekli ve isteğe bağlı istek üstbilgileri açıklar.

* `api-key`: Merhaba `api-key` kullanılan tooauthenticate hello isteği tooyour arama hizmeti değil. Bu bir dize değeri, benzersiz tooyour hizmeti olur. Merhaba **analiz API** isteği içermelidir bir `api-key` kümesi tooan yönetici anahtarı (karşılıklı tooa sorgu anahtarı).

Merhaba dizin adı ve hello hizmet adı tooconstruct hello istek URL'si de gerekir. Merhaba hizmet adı alabilir ve `api-key` hizmeti Panonuzda hello Azure Portalı'ndan. Bkz: [hello portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.

**İstek gövdesi**

    {
      "text": "Text tooanalyze",
      "analyzer": "analyzer_name"
    }

or

    {
      "text": "Text tooanalyze",
      "tokenizer": "tokenizer_name",
      "tokenFilters": (optional) [ "token_filter_name" ],
      "charFilters": (optional) [ "char_filter_name" ]
    }

Merhaba `analyzer_name`, `tokenizer_name`, `token_filter_name` ve `char_filter_name` hello dizini için önceden tanımlanmış veya özel çözümleyiciler, tokenizers, belirteç filtreleri ve char filtreleri geçerli adlarını toobe gerekir. sözcük analiz hello işlemi hakkında daha fazla toolearn [analiz Azure Search'te](https://aka.ms/azsanalysis).

**Yanıt**

Durum kodu: 200 Tamam için başarılı bir yanıt döndürdü.

Merhaba yanıt gövdesi hello biçimi aşağıdaki gibidir:

    {
      "tokens": [
        {
          "token": string (token),
          "startOffset": number (index of hello first character of hello token),
          "endOffset": number (index of hello last character of hello token),
          "position": number (position of hello token in hello input text)
        },
        ...
      ]
    }

**API örnek Çözümle**

**İstek**

    {
      "text": "Text tooanalyze",
      "analyzer": "standard"
    }

**Yanıt**

    {
      "tokens": [
        {
          "token": "text",
          "startOffset": 0,
          "endOffset": 4,
          "position": 0
        },
        {
          "token": "to",
          "startOffset": 5,
          "endOffset": 7,
          "position": 1
        },
        {
          "token": "analyze",
          "startOffset": 8,
          "endOffset": 15,
          "position": 2
        }
      ]
    }

- - -
<a name="DocOps"></a>

## <a name="document-operations"></a>Belge işlemleri
Azure Search'te bir dizine hello bulutta depolanan ve toohello hizmet karşıya JSON belgelerini kullanarak doldurulur. Karşıya yüklediğiniz tüm hello belgeleri hello gövde arama verilerinizin kapsar. Belgeleri karşıya gibi bazıları arama terimleri simgeleştirilmiş alanlar içerebilir. Merhaba `/docs` hello Azure Search API URL kesimi dizin belgelerde hello koleksiyonunu temsil eder. Karşıya yükleme gibi hello koleksiyon üzerinde gerçekleştirilen tüm işlemleri, birleştirme, silme veya belgeleri sorgulama sürer bunu hello URL'leri tek bir dizin Merhaba içeriğine yerinde bu işlemlerin her zaman ile başlar için `/indexes/[index name]/docs` için belirtilen dizin adı.

Uygulama kodunuz JSON belgeleri tooupload tooAzure arama ya da oluşturmanız gerekir veya kullanabileceğiniz bir [dizin oluşturucu](https://msdn.microsoft.com/library/dn946891.aspx) tooload belgeleri hello veri kaynağı Azure SQL Database veya Azure Cosmos DB ise. Genellikle, dizinleri sağlayan bir tek veri kümesinden doldurulur.

Toosearch istediğiniz her bir öğe için bir belge sahip planlamanız gerekir. Film kiralama uygulamasının film başına tek bir belgenin olabilir, bir mağaza uygulaması SKU başına tek bir belgenin olabilir, bir çevrimiçi eğitim malzemesi uygulamasının indirmelere başına tek bir belgenin olabilir, araştırma kesin bir belgeyi her akademik kağıt olabilir kendi Depo ve benzeri.

Belgeler bir veya daha fazla alan oluşur. Alanları Azure Search tarafından arama terimleri simgeleştirilmiş yanı sıra dışı simgeleştirilmiş metin veya filtreleri veya Puanlama profilleri kullanılabilir metin dışı değerleri içerebilir. Merhaba adları, veri türleri ve her bir alan için desteklenen arama özellikleri hello dizin şemasına göre belirlenir. Her dizin şemasında hello alanlardan biri bir kimliği olarak işaretlenmesi gerekir ve her bir belgenin bu belgede hello dizini benzersiz olarak tanıtan hello Kimliği alanı için bir değer olmalıdır. Diğer tüm belge alanlarını isteğe bağlıdır ve sol belirtilmezse varsayılan tooa null değer kullanılacak. Null değerler hello arama dizini yer almayan unutmayın.

Belgeleri yüklemeden önce başlangıç dizini hello hizmette oluşturmuş olmalısınız. Bkz: [Create Index](#CreateIndex) birinci adım hakkında ayrıntılı bilgi için.

<a name="AddOrUpdateDocuments"></a>

## <a name="add-update-or-delete-documents"></a>Ekleme, güncelleştirme, belgeleri veya silme
Karşıya yüklediğiniz, HTTP POST kullanılarak belirtilen bir dizinden birleştirme, birleştirme veya karşıya yükleme veya delete belgeleri. Güncelleştirmeler için çok sayıda (too1000 belgeleri toplu iş başına) veya toplu iş başına yaklaşık 16 MB belgelerin toplu işleme önerilir.

    POST https://[service name].search.windows.net/indexes/[index name]/docs/index?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

**İstek**

HTTPS tüm hizmet istekleri için gereklidir. Karşıya yüklediğiniz, HTTP POST kullanılarak belirtilen bir dizinden birleştirme, birleştirme veya karşıya yükleme veya delete belgeleri.

URI içerir [dizin adı] hello isteği hangi dizin toopost belgeler belirtme. Bu gibi durumlarda, belgeleri tooone dizin yalnızca aynı anda nakledebilirsiniz.

`api-version=[string]`(gerekli). Merhaba Önizleme sürümü `api-version=2015-02-28-Preview`. Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri için.

**İstek üstbilgileri**

liste aşağıdaki hello hello gerekli ve isteğe bağlı istek üstbilgileri açıklar.

* `Content-Type`: Gerekli. Bu çok ayarlama`application/json`
* `api-key`: Gerekli. Merhaba `api-key` kullanılan tooauthenticate hello isteği tooyour arama hizmeti değil. Bu bir dize değeri, benzersiz tooyour hizmeti olur. Merhaba **ekleme belgeleri** isteği içermelidir bir `api-key` üstbilgi tooyour yönetici anahtarını (karşılıklı tooa sorgu anahtarı) olarak ayarlayın.

Merhaba hizmet adı tooconstruct hello istek URL'si de gerekir. Merhaba hizmet adı alabilir ve `api-key` hizmeti Panonuzda hello Azure Portalı'ndan. Bkz: [hello portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.

**İstek gövdesi**

Daha fazla belgeleri toobe Hello hello istek gövdesi içeriyor veya dizini. Belgeler, benzersiz bir anahtar tarafından tanımlanır. Her bir eylem ile ilişkili bir belgedir: karşıya yükleme, birleştirme, mergeOrUpload veya Sil. Karşıya yükleme istekleri hello belge verileri içeren bir anahtar/değer çiftleri kümesi olarak olarak gerekir.

    {
      "value": [
        {
          "@search.action": "upload (default) | merge | mergeOrUpload | delete",
          "key_field_name": "unique_key_of_document", (key/value pair for key field from index schema)
          "field_name": field_value (key/value pairs matching index schema)
            ...
        },
        ...
      ]
    }

> [!NOTE]
> Belge anahtarları yalnızca harf, sayı, kısa çizgi içerebilir ("-"), alt çizgi ("_") ve eşittir işareti ("="). Daha fazla ayrıntı için bkz: [adlandırma kurallarını](https://msdn.microsoft.com/library/azure/dn857353.aspx).
> 
> 

**Belge eylemleri**

* `upload`: Bir karşıya yükleme benzer tooan "upsert" nerede hello belgenin yeni olması durumunda ekleneceği ve olması mevcut durumunda güncelleştirileceği/değiştirileceği bir eylemdir. Tüm alanlar hello güncelleştirme durumda yerini aldığını unutmayın.
* `merge`: Varolan bir belge ile hello birleştirme güncelleştirmeleri alanları belirtilmiş. Merhaba belge yoksa, hello birleştirme işlemi başarısız olur. Birleştirmede belirttiğiniz herhangi bir alan varolan bir alana hello hello belgedeki yerini alır. Buna `Collection(Edm.String)` türünde alanlar dahildir. Örneğin, hello belge "etiketler" değerine sahip bir alan varsa, `["budget"]` ve değeriyle bir birleştirme yürütme `["economy", "pool"]` "etiketleri için" Merhaba "etiketler" alanının son değeri hello olacaktır `["economy", "pool"]`. İçinde **değil** olması `["budget", "economy", "pool"]`.
* `mergeOrUpload`: gibi davranır `merge` anahtar zaten verilen hello belgeyle hello dizinde varsa. Merhaba belge mevcut değilse gibi davranır `upload` yeni bir belgeyle.
* `delete`: Delete hello belirtilen belge hello dizinden kaldırır. Belirttiğiniz tüm alanlar içinde olduğunu unutmayın bir `delete` işlemi hello anahtar alanı dışında yok sayılacak. Bir belgeden tek bir alanı tooremove istiyorsanız kullanın `merge` yerine ve basit şekilde hello alan açıkça çok kümesi`null`.

**Yanıt**

Durum kodu 200 (Tamam) tüm öğeleri başarıyla eklenmemiş anlamı başarılı bir yanıt için döndürülür. Bu hello tarafından belirtilir `status` tootrue tüm öğeleri yanı sıra hello için ayarlanan özelliği `statusCode` tooeither 201 (için yeni yüklenen belgeleri için) veya 200 (için birleştirilmiş veya Silinen Belge) ayarlanan özelliği:

    {
      "value": [
        {
          "key": "unique_key_of_new_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 201
        },
        {
          "key": "unique_key_of_merged_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        },
        {
          "key": "unique_key_of_deleted_document",
          "status": true,
          "errorMessage": null,
          "statusCode": 200
        }
      ]
    }  

En az bir öğenin dizine alınması başarısız olduğunda 207 (çok durumu) durum kodu döndürülür. Dizine öğeleri sahip hello `status` alanını toofalse ayarlayın. Merhaba `errorMessage` ve `statusCode` özellikleri hata dizin hello hello nedeni gösterir:

    {
      "value": [
        {
          "key": "unique_key_of_document_1",
          "status": false,
          "errorMessage": "hello search service is too busy tooprocess this document. Please try again later.",
          "statusCode": 503
        },
        {
          "key": "unique_key_of_document_2",
          "status": false,
          "errorMessage": "Document not found.",
          "statusCode": 404
        },
        {
          "key": "unique_key_of_document_3",
          "status": false,
          "errorMessage": "Index is temporarily unavailable because it was updated with hello 'allowIndexDowntime' flag set too'true'. Please try again later.",
          "statusCode": 422
        }
      ]
    }  

Aşağıdaki tablonun hello çeşitli hello yanıtta döndürülen durum kodları belge başına hello açıklanmaktadır. Başkalarının geçici hata koşulları belirtmek karşın bazı sorunları hello isteği kendisi ile olduğunu unutmayın. Merhaba ikinci bir gecikmeden sonra yeniden denemeniz gerekir.

<table style="font-size:12">
    <tr>
        <th>Durum kodu</th>
        <th>Anlamı</th>
        <th>Yeniden denenebilir</th>
        <th>Notlar</th>
    </tr>
    <tr>
        <td>200</td>
        <td>Belge başarıyla değiştirilmiş veya silinmiş.</td>
        <td>yok</td>
        <td>Silme işlemlerine olan <a href="https://en.wikipedia.org/wiki/Idempotence">ıdempotent</a>. Diğer bir deyişle, bir belge anahtarı hello dizininde mevcut değilse, bu anahtara sahip bir silme işlemini denemeden 200 durum koduna neden olur.</td>
    </tr>
    <tr>
        <td>201</td>
        <td>Belge başarıyla oluşturuldu.</td>
        <td>yok</td>
        <td></td>
    </tr>
    <tr>
        <td>400</td>
        <td>Merhaba belgedeki dizine alınmasını engelleyen bir hata vardı.</td>
        <td>Hayır</td>
        <td>Merhaba hata iletisi hello yanıt hello belgeyle nerede olduğunu belirtir.</td>
    </tr>
    <tr>
        <td>404</td>
        <td>anahtarı verilen hello hello dizininde mevcut olmadığından hello belge birleştirilemeyen.</td>
        <td>Hayır</td>
        <td>Bu hata yüklemeler için yeni belgeler oluşturma ve olduklarından silme işlemi için oluşmaz oluşmaz <a href="https://en.wikipedia.org/wiki/Idempotence">ıdempotent</a>.</td>
    </tr>
    <tr>
        <td>409</td>
        <td>Sürüm çakışması tooindex bir belge çalışırken algılandı.</td>
        <td>Evet</td>
        <td>Bu durum, aynı anda birden fazla kez belge tooindex hello çalıştığınız ortaya çıkar.</td>
    </tr>
    <tr>
        <td>422</td>
        <td>Merhaba 'allowIndexDowntime' bayrak kümesi too'true ile güncellendiğinden Merhaba dizin geçici olarak devre dışı '.</td>
        <td>Evet</td>
        <td></td>
    </tr>
    <tr>
        <td>503</td>
        <td>Arama hizmetinizi büyük olasılıkla tooheavy yük geçici olarak kullanılamıyor.</td>
        <td>Evet</td>
        <td>Kodunuzu bu durumda yeniden denemeden önce beklemesi gereken veya hello hizmet kullanılamazlık uzatma risk.</td>
    </tr>
</table> 

**Not**: istemci kodunuzun sık 207 yanıtı karşılaşırsa, olası bir nedeni hello sistem yük altında olmasıdır. Bu hello denetleyerek doğrulayabilirsiniz `statusCode` 503 özelliği. Öneririz bu hello durumda olup olmadığını, ***dizin oluşturma isteklerinin azaltma***. Aksi takdirde, dizin oluşturma trafiği subside değil, hello sistem 503 hataları olan tüm istekleri reddetme başlayabilirsiniz.

Durum kodu 429 hello dizin başına belge sayısı Kotanızı aştınız gösterir. Yeni bir dizin oluşturabilir veya için daha yüksek kapasite limitlerini yükseltin.

**Örnek:**

    {
      "value": [
        {
          "@search.action": "upload",
          "hotelId": "1",
          "baseRate": 199.0,
          "description": "Best hotel in town",
          "description_fr": "Meilleur hôtel en ville",
          "hotelName": "Fancy Stay",
          "category": "Luxury",
          "tags": ["pool", "view", "wifi", "concierge"],
          "parkingIncluded": false,
          "smokingAllowed": false,
          "lastRenovationDate": "2010-06-27T00:00:00Z",
          "rating": 5,
          "location": { "type": "Point", "coordinates": [-122.131577, 47.678581] }
        },
        {
          "@search.action": "upload",
          "hotelId": "2",
          "baseRate": 79.99,
          "description": "Cheapest hotel in town",
          "description_fr": "Hôtel le moins cher en ville",
          "hotelName": "Roach Motel",
          "category": "Budget",
          "tags": ["motel", "budget"],
          "parkingIncluded": true,
          "smokingAllowed": true,
          "lastRenovationDate": "1982-04-28T00:00:00Z",
          "rating": 1,
          "location": { "type": "Point", "coordinates": [-122.131577, 49.678581] }
        },
        {
          "@search.action": "merge",
          "hotelId": "3",
          "baseRate": 279.99,
          "description": "Surprisingly expensive",
          "lastRenovationDate": null
        },
        {
          "@search.action": "delete",
          "hotelId": "4"
        }
      ]
    }
- - -
<a name="SearchDocs"></a>

## <a name="search-documents"></a>Belge ara
A **arama** işlemi bir GET veya POST talebi olarak verilir ve eşleşen belgeleri seçmek için hello ölçütleri vermek parametreleri belirtir.

    GET https://[service name].search.windows.net/indexes/[index name]/docs?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/search?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

**Toouse yerine duyurduğumuzda Al**

HTTP GET toocall hello kullandığınızda **arama** API, toobe hello istek URL'si hello uzunluğu 8 KB'yi aşamaz kullanan gerekir. Çoğu uygulama için yeterince genellikle budur. Ancak, bazı uygulamalar çok büyük sorgular veya OData filtre ifadeleri üretir. Daha büyük filtreleri ve sorguları get'ten sağladığından bu uygulamalar için HTTP POST kullanılarak daha iyi bir seçimdir. POST, koşulları veya bir sorgu yan tümcelerinde hello sayısı ile hello faktörü, değil hello istek boyutu sınırını POST için yaklaşık 16 MB olduğundan hello ham sorgu hello boyutu sınırlama değil.

> [!NOTE]
> Merhaba POST isteği boyut sınırı çok büyük olsa bile arama sorguları ve filtre ifadeleri rasgele karmaşık olamaz. Bkz: [Lucene sorgu söz dizimi](https://msdn.microsoft.com/library/mt589323.aspx) ve [OData ifade sözdizimini](https://msdn.microsoft.com/library/dn798921.aspx) arama sorgusu ve filtre karmaşıklık sınırlamalar hakkında daha fazla bilgi.
> 
> 

**İstek**

HTTPS istekleri için gereklidir. Merhaba **arama** isteği hello GET veya POST yöntemleri kullanarak olacak oluşturulan.

Merhaba isteğin URI hello parametreleriyle eşleşen tüm belgeler için hangi dizin tooquery belirtir. Parametreleri hello sorgu dizesinde GET isteklerinin hello durumda belirtilir ve hello istekte hello durumunun POST gövdesinde ister.

GET isteklerini oluştururken en iyi uygulama, çok unutmayın[URL kodlama](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) çağrılırken parametreleri hello REST API doğrudan belirli sorgu. İçin **arama** bu işlemleri içerir:

* `$filter`
* `facet`
* `highlightPreTag`
* `highlightPostTag`
* `search`
* `moreLikeThis`

URL kodlaması sorgu parametreleri yukarıda hello üzerinde yalnızca önerilir. Tüm sorgu dizesi (her şeyi hello sonra?), yanlışlıkla URL kodlama Merhaba, istekleri çalışmamasına neden olur.

Ayrıca, URL kodlaması yalnızca REST API kullanarak doğrudan alma hello çağrılırken gereklidir. Hiçbir URL kodlaması çağrılırken gereklidir **arama** POST, kullanma ya da hello kullanırken [.NET istemci kitaplığını](https://msdn.microsoft.com/library/dn951165.aspx), sizin için URL kodlaması işler.

<a name="SearchQueryParameters"></a>
**Sorgu parametreleri**

**Arama** sorgu ölçütlerini sağlayan ve ayrıca arama davranışını belirtin birkaç parametre kabul eder. Bu parametreler hello URL'deki sorgu dizesi çağrılırken sağladığınız **arama** GET aracılığıyla ve JSON özellikleri çağrılırken hello istek gövdesi olarak **arama** POST ile. bazı parametreler için Hello sözdizimi GET ve POST arasında biraz farklıdır. Bu farklılıklar, geçerli aşağıda belirtilmiştir:

`search=[string]`(isteğe bağlı) - metin toosearch hello. Tüm `searchable` sürece alanları varsayılan olarak aranır `searchFields` belirtilir. Arama yaparken `searchable` alanları, hello arama metni kendisini simgeleştirilmiş, birden çok koşulları boşluk ile ayrılabilir şekilde (örneğin: `search=hello world`). Her terim toomatch kullanmak `*` (Boole filtresi sorgular için yararlı olabilir). Bu parametrenin atlanması sahip aynı efekt çok ayarı olarak hello`*`. Bkz: [Basit Sorgu söz dizimi](https://msdn.microsoft.com/library/dn798920.aspx) hello arama söz dizimi üzerinde özellikleri için.

* **Not**: hello sonuçları bazen olabilir şaşırtıcı üzerinden sorgulanırken `searchable` alanları. Merhaba belirteç Oluşturucu mantığı toohandle durumlarda ortak tooEnglish metin kesme, virgül gibi sayılar, vb. içerir. Örneğin, `search=123,456` virgül İngilizce büyük sayılar için bin ayırıcı olarak kullanıldığından hello tek tek 123 ve terimleri 456, yerine tek bir terim 123,456 ile eşleşir. Bu nedenle, noktalama tooseparate koşullarını yerine boşluk hello kullanılmasını öneririz `search` parametresi.

`searchMode=any|all`(isteğe bağlı, çok varsayılanları`any`) - olup hello arama terimleri bir bölümünü veya tamamını sipariş toocount hello belgede bir eşleşme olarak eşlenmesi gerekir.

`searchFields=[string]`(isteğe bağlı) - hello için virgülle ayrılmış bir alan adları toosearch hello listesini Belirtilen metni. Hedef alan işaretli, olarak `searchable`.

`queryType=simple|full`(isteğe bağlı, çok varsayılanları`simple`) - kümesi "Basit" çok arama metni simgelerini gibi sağlayan bir basit sorgu dili kullanarak değerlendirdiğinde +, * ve "". Sorguları, tüm aranabilir alanları değerlendirilir (veya alanlarını belirtilen `searchFields`) varsayılan olarak her belgedeki. Merhaba sorgu türü ayarlandığında çok`full` arama metni alana özgü ve ağırlıklı aramaları sağlayan hello Lucene sorgu dili kullanarak yorumlanır. Bkz: [Basit Sorgu söz dizimi](https://msdn.microsoft.com/library/dn798920.aspx) ve [Lucene sorgu söz dizimi](https://msdn.microsoft.com/library/mt589323.aspx) hello arama sözdizimleri üzerinde özellikleri için. 

> [!NOTE]
> Merhaba Lucene sorgu dili benzer işlevselliği sunan $filter lehinde desteklenmiyor aramada aralığı.
> 
> 

`moreLikeThis=[key]`(isteğe bağlı) **Önemli:** bu özellik yalnızca kullanılabilir `2015-02-28-Preview`. Bu seçenek hello metin arama parametre içeren bir sorguda kullanılamaz `search=[string]`. Merhaba `moreLikeThis` parametresi hello belge anahtarı ile belirtilen benzer toohello belge olan belgeleri bulur. Ne zaman bir arama isteği yapıldığında ile `moreLikeThis`, arama terimleri listesini hello sıklığı ve rarity hello kaynak belgedeki koşulları temel alınarak oluşturulur. Kullanılan toomake hello sonra isteği bu terimler. Varsayılan olarak, tüm içeriğini hello `searchable` sürece alanlar olarak kabul `searchFields` hangi alanları aranır kullanılan toorestrict değil.  

`$skip=#`(isteğe bağlı) - hello sayısı arama sonuçları tooskip; 100. 000 ' büyük olamaz. Dizisi tooscan belgelerde gerekiyor ancak kullanamazsınız `$skip` toothis sınırlaması nedeniyle kullanmayı `$orderby` tamamen sıralı anahtar ve `$filter` bir aralık sorgu yerine.

> [!NOTE]
> Çağrılırken **arama** POST kullanarak, bu parametre adlı `skip` yerine `$skip`.
> 
> 

`$top=#`(isteğe bağlı) - arama hello sayısı tooretrieve sonuçlanır. Bu ile birlikte kullanılabilir `$skip` tooimplement istemci-tarafı sayfalama arama sonuçları.

> [!NOTE]
> Çağrılırken **arama** POST kullanarak, bu parametre adlı `top` yerine `$top`.
> 
> 

`$count=true|false`(isteğe bağlı, çok varsayılanları`false`)-toofetch sonuçları toplam hata sayısı hello olup olmadığını belirtir. Bu hello eşleşen tüm belgelerin hello sayısıdır `search` ve `$filter` yoksayılıyor parametreleri `$top` ve `$skip`. Bu değeri çok ayarı`true` bir performans etkisi olabilir. Döndürülen hello sayısı yaklaşık olduğuna dikkat edin.

> [!NOTE]
> Çağrılırken **arama** POST kullanarak, bu parametre adlı `count` yerine `$count`.
> 
> 

`$orderby=[string]`(isteğe bağlı) - virgülle ayrılmış ifadeler toosort hello sonuçlarına göre listesi. Her bir ifadenin bir alan adı veya bir çağrı toohello olabilir `geo.distance()` işlevi. Her deyim tarafından izlenebilir `asc` artan, tooindicated ve `desc` azalan tooindicate. Merhaba varsayılan, artan. TIES tarafından belgelerin hello eşleşmiyor puan ayrılmış olarak gösterilir. Öyle değilse `$orderby` belirtilirse, belge eşleşmiyor puan göre azalan hello varsayılan sıralama düzeni. Bir sınır için 32 yan `$orderby`.

> [!NOTE]
> Çağrılırken **arama** POST kullanarak, bu parametre adlı `orderby` yerine `$orderby`.
> 
> 

`$select=[string]`(isteğe bağlı) - virgülle ayrılmış alanlar tooretrieve listesi. Belirtilmezse, hello şemasında alınabilir olarak işaretlenmiş tüm alanlar dahil edilir. Bu parametre çok ayarlayarak da açıkça tüm alanlar isteyebilir`*`.

> [!NOTE]
> Çağrılırken **arama** POST kullanarak, bu parametre adlı `select` yerine `$select`.
> 
> 

`facet=[string]`(sıfır veya daha fazla) - bir alan toofacet tarafından. Merhaba dizesi parametreleri toocustomize hello olduğunu virgülle ayrılmış olarak ifade edilen isteğe bağlı olarak içerebilir `name:value` çiftleri. Geçerli Parametreler şunlardır:

* `count`(en fazla sayıda modeli şartı; varsayılan değer 10). Maksimum yok yoktur, ancak özellikle çok sayıda benzersiz koşulları hello modellenmiş alan içeriyorsa, daha yüksek değerleri karşılık gelen bir performans cezasına sebep.
  * Örneğin: `facet=category,count:5` hello modeli sonuçlarında iyi beş kategorileri alır.  
  * **Not**: hello varsa `count` parametre benzersiz koşulları hello sayısından daha az ve hello sonuçları doğru olmayabilir. Son olduğunu sorgular parça dağıtılan toohello yolu budur. Artan `count` genellikle artar doğruluğu hello terim sayıları, ancak performans maliyeti hello.
* `sort`(birini `count` toosort *azalan* sayıma göre `-count` toosort *artan* sayıma göre `value` toosort *artan* değer veya `-value` toosort *azalan* değeriyle)
  * Örneğin: `facet=category,count:3,sort:count` alır, her şehir adı belgelerle hello sayısına göre azalan sırada modeli sonuçlarında üst üç kategoride hello. Örneğin, bütçe, Motel ve lüks, hello üst üç kategorileri şunlardır ve bütçe 5 isabet, 6 Motel sahip ve lüks 4 varsa, ardından hello demet hello sırayla olacaktır Motel, bütçe, lüks.
  * Örneğin: `facet=rating,sort:-value` değerine göre azalan sırada tüm olası derecelendirmeler aralıklarını üretir. Merhaba derecelendirmeleri 1 too5 varsa, örneğin, hello demet sıralanır 5, 4, 3, 2, kaç tane belgeleri her derecelendirme eşleşen yedeklemiş 1.
* `values`(kanal ayrılmış sayısal veya `Edm.DateTimeOffset` değerleri model girdi değerleri dinamik bir dizi belirtme)
  * Örneğin: `facet=baseRate,values:10|20` üç demet oluşturur: biri temel oranını 0 toobut 10, 10 toobut 20 ve 20 veya daha yüksek bir dahil değil yedeklemek için bir tane dahil edilmez.
  * Örneğin: `facet=lastRenovationDate,values:2010-02-01T00:00:00Z` iki demet oluşturur: biri Şubat 2010'dan önce renovated Oteller ve Otel için bir renovated Şubat 2010 veya üzeri 1.
* `interval`(sayı, 0'dan büyük tamsayı aralığı veya `minute`, `hour`, `day`, `week`, `month`, `quarter`, `year` tarih saat değerleri için)
  * Örneğin: `facet=baseRate,interval:100` demet boyutu 100 temel oranı aralıklarını temel alarak oluşturur. Örneğin, temel oranları tüm $60 ve $600 arasında varsa, olacaktır 0-100, 100-200, 200-300, 400 300, 400-500 ve 500-600 aralıklarını.
  * Örneğin: `facet=lastRenovationDate,interval:year` bir demet zaman Oteller renovated her yıl üretir.
* `timeoffset`([+-] hh: mm, [+-] ssdd, veya [+-] hh) `timeoffset` isteğe bağlıdır. Yalnızca hello ile birleştirilebilir `interval` seçeneği ve yalnızca türünde uygulanan tooa alan `Edm.DateTimeOffset`. Merhaba değeri, zaman sınırları ayarı hello UTC saati için uzaklık tooaccount belirtir.
  * Örneğin: `facet=lastRenovationDate,interval:day,timeoffset:-01:00` kullandığı hello 01:00:00 UTC (Merhaba hedef saat diliminde gece yarısı) başlar günlük sınır
* **Not**: `count` ve `sort` hello aynı birleştirilebilir ile modeli belirtimi, ancak bunlar ilişkilendirilemez `interval` veya `values`, ve `interval` ve `values` birlikte birleştirilemez.
* **Not**: tarih saat aralığı nedeni modellerinin hesaplanan UTC saat tabanlı `timeoffset` belirtilmedi. Örneğin: için `facet=lastRenovationDate,interval:day`, hello günlük sınır 00:00:00 UTC başlatır. 

> [!NOTE]
> Çağrılırken **arama** POST kullanarak, bu parametre adlı `facets` yerine `facet`. Ayrıca, bunu burada her ayrı modeli ifade dizesidir dizeleri bir JSON dizisi olarak belirtin.
> 
> 

`$filter=[string]`(isteğe bağlı) - standart OData sözdiziminde yapılandırılmış arama ifadesi.

> [!NOTE]
> Çağrılırken **arama** POST kullanarak, bu parametre adlı `filter` yerine `$filter`.
> 
> 

`highlight=[string]`(isteğe bağlı) - virgülle ayrılmış bir alan adları isabet için kullanılan bir dizi vurgular. Yalnızca `searchable` alanları isabet vurgulama için kullanılabilir.

`highlightPreTag=[string]`(isteğe bağlı, çok varsayılanları`<em>`) - bir dize toohit vurgular başına etiketi. İle ayarlanmalıdır `highlightPostTag`.

> [!NOTE]
> Çağrılırken **arama** GET kullanarak, ayrılmış karakter hello URL (örneğin, % &#23; yerine) yüzde olarak kodlanmış olmalıdır.
> 
> 

`highlightPostTag=[string]`(isteğe bağlı, çok varsayılanları`</em>`)-toohit vurgular ekler bir dize etiketi. İle ayarlanmalıdır `highlightPreTag`.

> [!NOTE]
> Çağrılırken **arama** GET kullanarak, ayrılmış karakter hello URL (örneğin, % &#23; yerine) yüzde olarak kodlanmış olmalıdır.
> 
> 

`scoringProfile=[string]`(isteğe bağlı) - hello Puanlama profili tooevaluate adıyla aynı düzeni toosort hello sonuçları eşleşen belgelerde puanlarını.

`scoringParameter=[string]`(sıfır veya daha fazla) - bir Puanlama işlevi tanımlanan her parametre için hello değerleri gösterir (örneğin, `referencePointParameter`) hello biçimini kullanarak `name-value1,value2,...`.

* Örneğin, hello profil Puanlama işlevi ile tanımlıyorsa "mylocation" Merhaba sorgu dizesi seçeneği adlı bir parametre olması `&scoringParameter=mylocation--122.2,44.8`. Merhaba ikinci tire hello ilk değer (Bu örnekte boylam) bir parçası olsa hello ilk tire hello adını hello değer listesinden ayırır.
* Puanlama parametrelerini etiketi, artırmanın virgüller, içerebilir gibi tek tırnak kullanılarak hello listedeki tür değerleri kaçış. Merhaba değer kendilerini tek tırnak içermiyorsa, katlama tarafından kaçış
  * Örneğin, "Hello, O'Brien" ve "Smith", hello sorgu "mytag" adlı bir parametreye artırmanın bir etiketi varsa ve hello etiketinde tooboost istediğiniz değerleri dize seçenek olacaktır `&scoringParameter=mytag-'Hello, O''Brien',Smith`. Tırnak işaretleri yalnızca olduğuna dikkat edin virgül içeren değerler için gereklidir.

> [!NOTE]
> Çağrılırken **arama** POST kullanarak, bu parametre adlı `scoringParameters` yerine `scoringParameter`. Bir JSON dizisini ayrı bir olduğu her bir dize belirttiğiniz ayrıca `name-values` çifti.
> 
> 

`minimumCoverage`(isteğe bağlı, varsayılan olarak too100) - 0 ile Merhaba sorgu toobe sırada bir arama sorgusu tarafından ele alınması gereken hello dizin hello yüzdesini gösteren 100 arasında bir sayı başarı bildirdi. Varsayılan olarak, tüm dizin hello kullanılabilir olmalıdır veya `Search` 503 HTTP durum kodunu döndürür. Ayarlarsanız `minimumCoverage` ve `Search` başarılı, HTTP 200 dönün ve içeren bir `@search.coverage` hello yanıt hello sorguda eklenmiştir hello dizin hello yüzdesini belirten değer.

> [!NOTE]
> Bu parametre tooa değerin 100 Hizmetleri ile yalnızca bir çoğaltma için bile arama kullanılabilirlik sağlamak için yararlı olabilir. daha düşük ayarlanması. Ancak, tüm eşleşen belgeleri toobe hello arama sonuçlarında mevcut sağlanır. Arama geri çağırma olduğu daha önemli tooyour uygulamadan kullanılabilirlik daha sonra en iyi tooleave olan `minimumCoverage` zaman, varsayılan değer 100.
> 
> 

`api-version=[string]`(gerekli). Merhaba Önizleme sürümü `api-version=2015-02-28-Preview`. Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri için.

Not: Bu işlem için hello `api-version` olup, çağrı bağımsız olarak hello URL'deki sorgu parametresi olarak belirtilen **arama** GET veya POST ile.

**İstek üstbilgileri**

liste aşağıdaki hello hello gerekli ve isteğe bağlı istek üstbilgileri açıklar.

* `api-key`: Merhaba `api-key` kullanılan tooauthenticate hello isteği tooyour arama hizmeti değil. Bir dize değeri, benzersiz tooyour hizmeti URL'si değil. Merhaba **arama** isteği, bir yönetici anahtarını veya sorgu anahtarı belirtebilirsiniz `api-key`.

Merhaba hizmet adı tooconstruct hello istek URL'si de gerekir. Merhaba hizmet adı alabilir ve `api-key` hizmeti Panonuzda hello Azure Portalı'ndan. Bkz: [hello portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.

**İstek gövdesi**

GET için: yok.

POST için:

    {
      "count": true | false (default),
      "facets": [ "facet_expression_1", "facet_expression_2", ... ],
      "filter": "odata_filter_expression",
      "highlight": "highlight_field_1, highlight_field_2, ...",
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 100),
      "moreLikeThis": "document_key" (mutually exclusive with "search" parameter),
      "orderby": "orderby_expression",
      "scoringParameters": [ "scoring_parameter_1", "scoring_parameter_2", ... ],
      "scoringProfile": "scoring_profile_name",
      "search": "simple_query_expression",
      "searchFields": "field_name_1, field_name_2, ...",
      "searchMode": "any" (default) | "all",
      "select": "field_name_1, field_name_2, ...",
      "skip": # (default 0),
      "top": #
    }

**Kısmi arama yanıtları devamlılığı**

Bazen Azure Search tüm tek bir arama yanıt istenen sonuçları hello döndüremez. Bu durum hello sorgu çok fazla belgeleri değil belirterek isteğinde bulunduğunda gibi farklı nedenlerle oluşabilir `$top` veya için bir değer belirterek `$top` , çok büyük. Böyle durumlarda, Azure Search hello içerecektir `@odata.nextLink` hello yanıt gövdesi içinde ek açıklama ve ayrıca `@search.nextPageParameters` bir POST isteği ise. Bu ek açıklamaları tooformulate hello değerlerini başka bir arama isteği tooget hello sonraki bölümü hello arama yanıtı kullanabilirsiniz. Bu adlı bir ***devamlılık*** hello özgün arama isteği ve hello ek açıklamaları genellikle denir ***devamlılık belirteçleri***. Bkz: [aşağıdaki hello örnek](#SearchResponse) hello sözdizimi, bu ek açıklamaların ve hello yanıt gövdesi içinde nerede göründüklerinden hakkında bilgi. 

Azure Search devamlılık belirteçleri neden döndürebilir hello uygulamaya özel ve konu toochange nedenleridir. Sağlam istemcileri her zaman burada beklenenden daha az belgeler döndürülür ve devamlılık belirteci belgelerini almak dahil toocontinue hazır toohandle durumda olması gerekir. Ayrıca aynı HTTP yöntemi sipariş toocontinue özgün isteğinde hello olarak hello kullanmanız gerektiğini unutmayın. Bir GET isteği gönderirse, örneğin, gönderdiğiniz herhangi bir devamlılık isteğini de GET kullanmanız gerekir (ve sonrası için benzer şekilde).

<a name="SearchResponse"></a>
**Yanıt**

Durum kodu: 200 Tamam için başarılı bir yanıt döndürdü.

    {
      "@odata.count": # (if $count=true was provided in hello query),
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "@search.facets": { (if faceting was specified in hello query)
        "facet_field": [
          {
            "value": facet_entry_value (for non-range facets),
            "from": facet_entry_value (for range facets),
            "to": facet_entry_value (for range facets),
            "count": number_of_documents
          }
        ],
        ...
      },
      "@search.nextPageParameters": { (request body toofetch hello next page of results if not all results could be returned in this response and Search was called with POST)
        "count": ... (value from request body if present),
        "facets": ... (value from request body if present),
        "filter": ... (value from request body if present),
        "highlight": ... (value from request body if present),
        "highlightPreTag": ... (value from request body if present),
        "highlightPostTag": ... (value from request body if present),
        "minimumCoverage": ... (value from request body if present),
        "moreLikeThis": ... (value from request body if present),
        "orderby": ... (value from request body if present),
        "scoringParameters": ... (value from request body if present),
        "scoringProfile": ... (value from request body if present),
        "search": ... (value from request body if present),
        "searchFields": ... (value from request body if present),
        "searchMode": ... (value from request body if present),
        "select": ... (value from request body if present),
        "skip": ... (page size plus value from request body if present),
        "top": ... (value from request body if present minus page size),
      },
      "value": [
        {
          "@search.score": document_score (if a text query was provided),
          "@search.highlights": {
            field_name: [ subset of text, ... ],
            ...
          },
          key_field_name: document_key,
          field_name: field_value (retrievable fields or specified projection),
          ...
        },
        ...
      ],
      "@odata.nextLink": (URL toofetch hello next page of results if not all results could be returned in this response; Applies tooboth GET and POST)
    }

**Örnekler:**

Ek örnekler üzerinde hello bulabilirsiniz [OData ifade sözdizimini Azure arama için](https://msdn.microsoft.com/library/azure/dn798921.aspx) sayfası.

1)    Arama hello dizin tarihe göre azalan sırada sıralanır.

    GET /indexes/hotels/docs? arama = * & $orderby lastRenovationDate desc & api-version = 2015-02-28-Önizleme =

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "*", "orderby": "lastRenovationDate desc"}

2)    Modellenmiş bir arama hello dizinini aramak ve modelleri için kategoriler, derecelendirme, etiketleri yanı sıra belirli aralıklara baseRate öğeleriyle almak:

    GET /indexes/hotels/docs? arama = test & modeli = kategori & modeli = derecelendirme & modeli etiketleri & modeli = baseRate, değerleri: 80 = | 150 | 220 & API sürümü 2015-02-28-Önizleme =

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "test", "modelleri": ["kategorisi", "Derecelendirme", "etiketler", "baseRate, değerleri: 80 | 150 | 220"]}

3)    Bir filtre kullanarak daraltmak hello önceki modellenmiş sorgu sonuçları üzerinde hello kullanıcı tıklattıktan sonra 3 ve kategori "Motel" derecelendirme:

    GET /indexes/hotels/docs? arama = test & modeli etiketleri & modeli = baseRate, değerleri: 80 = | 150 | 220 & $filter & derecelendirme eq 3 ve kategori eq 'Motel' api-version = 2015-02-28-Önizleme =

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "test", "modelleri": ["etiketleri", "baseRate, değerleri: 80 | 150 | 220"], "filtre": "Derecelendirme eq 3 ve kategori eq 'Motel'"}

4) Modellenmiş bir aramada bir sorgudan döndürülen benzersiz koşulları bir üst sınır ayarlayın. Merhaba varsayılan değer 10 ancak artırabilir ya da hello kullanarak bu değeri azaltmak `count` hello parametresini `facet` özniteliği:

    GET /indexes/hotels/docs? arama = test & modeli Şehir, sayısı: 5 & api-version = 2015-02-28-Önizleme =

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "test", "modelleri": ["Şehir, sayısı: 5"]}

5)    Belirli alanları içinde arama hello dizin; Dile özgü alanı:

    GET /indexes/hotels/docs? arama hôtel & searchFields = description_fr & api-version = 2015-02-28-Önizleme =

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "hôtel", "searchFields": "description_fr"}

6) Birden çok alan arasında arama başlangıç dizini. Örneğin, depolayabileceğiniz ve tüm içinde birden fazla dilde sorgu aranabilir alanları aynı dizin hello.  İngilizce ve Fransızca açıklamaları hello aynı birlikte varsa belge, sorgu sonuçları tüm içinde hello döndürebilirsiniz:

    GET /indexes/hotels/docs? arama otel & searchFields = açıklama, description_fr & api-version = 2015-02-28-Önizleme =

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "otel", "searchFields": "açıklama, description_fr"}

Aynı anda yalnızca bir dizin sorgulanabilir unutmayın. Aynı anda tooquery bir planlamıyorsanız her dil için birden çok dizin oluşturmayın.

7)    Disk belleği - Get hello 1 öğe sayfasının (sayfa boyutu Dur 10):

    GET /indexes/hotels/docs? arama = * & $skip = 0 & $top = 10 & api-version = 2015-02-28-Önizleme

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "*", "Atla": 0, "üst": 10}

8)    Disk belleği - Get hello 2 öğe sayfasının (sayfa boyutu Dur 10):

    GET /indexes/hotels/docs? arama = * & $skip = 10 & $top = 10 & api-version = 2015-02-28-Önizleme

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "*", "Atla": "üst" 10: 10}

9)    Belirli bir alan kümesi Al:

    GET /indexes/hotels/docs? arama = * & $select hotelName, açıklama ve api-version = 2015-02-28-Önizleme =

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "*", "Seç": "hotelName, açıklaması"}

10)  Bir özel filtre ifadesi eşleşen belgeler Al:

    GET /indexes/hotels/docs? $filter = (baseRate ge 60 ve baseRate lt 300) veya hotelName eq 'Süslü kalmak' & api-version = 2015-02-28-Önizleme

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"filtre": "(baseRate ge 60 ve baseRate lt 300) veya hotelName eq 'Süslü Kal'"}

11) Arama başlangıç dizini ve isabet vurgular dönüş parçaları

    GET /indexes/hotels/docs? arama bir şey = & vurgulayın açıklama & api-version = 2015-02-28-Önizleme =

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "bir şey", "highlight": "Açıklama"}

12) Arama başlangıç dizini ve bir başvuru konumu çıktığınızda daha yakından toofarther gelen sıralanmış dönüş belgeleri

    GET /indexes/hotels/docs? arama bir şey = & $orderby=geo.distance (konum, geography'POINT(-122.12315 47.88121)') & api-version = 2015-02-28-Önizleme

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "bir şey", "orderby": "geo.distance (konum, geography'POINT(-122.12315 47.88121)')"}

13) Dizin hello arama olmadığı varsayılarak "coğrafi" adlı bir Puanlama profili ile iki uzaklık Puanlama işlevleri, bir parametre tanımlama "currentLocation" ve "lastLocation" adlı bir parametreyi tanımlayan bir adlı

    GET /indexes/hotels/docs? arama bir şey = & scoringProfile = coğrafi & scoringParameter currentLocation--122.123,44.77233 & scoringParameter = lastLocation--121.499,44.2113 & api-version = 2015-02-28-Önizleme =

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "bir şey", "scoringProfile": "coğrafi", "scoringParameters": ["currentLocation--122.123,44.77233", "lastLocation--121.499,44.2113"]}

14) Dizin hello kullanarak bulmanın [Basit Sorgu söz dizimi](https://msdn.microsoft.com/library/dn798920.aspx). Bu sorgu burada hello koşulları "rahatlık" ve "Konum" ancak değil "motel" aranabilir alanları içeren Oteller döndürür:

    GET /indexes/hotels/docs? arama = rahatlık + konumu-motel & searchMode = all & api-version = 2015-02-28-Önizleme

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "rahatlık + konumu-motel", "searchMode": "tümü"}

Not hello `searchMode=all` üstünde. Bu parametreyi dahil olmak üzere hello varsayılan değerini geçersiz kılar `searchMode=any`, sağlama, `-motel` "Ve değil" yerine "Veya değil" anlamına gelir. Olmadan `searchMode=all`"Veya, arama sonuçları kısıtlayan yerine genişletir değil" alın ve bu counter-intuitive toosome kullanıcılar olabilir.

15) Dizin hello kullanarak bulmanın [lucene sorgu söz dizimi](https://msdn.microsoft.com/library/mt589323.aspx). Bu sorgu hello terimi "Bütçe" ve "son renovated" Merhaba ifadesini içeren tüm aranabilir alanları hello kategori alanı, içerdiği Oteller döndürür. "En son renovated" Merhaba tümcecik içeren belgeleri yüksek hello terim artırma değeri (3) sonucunda derecelendirilir.

    GET /indexes/hotels/docs? arama Kategori: Bütçe = ve \"son renovated\"^ 3 & searchMode = all & api-version = 2015-02-28-Önizleme & querytype tam =

    POST /indexes/hotels/docs/search? api-version = 2015-02-28-Önizleme {"Ara": "Kategori: Bütçe ve \"son renovated\"^ 3", "queryType": "tam", "searchMode": "tümü"}

<a name="LookupAPI"></a>

## <a name="lookup-document"></a>Arama belge
Merhaba **arama belge** işlemi Azure aramadan belge alır. Bu, bir kullanıcı belirli arama sonucu tıklar ve bu belge hakkında belirli ayrıntıları toolook istediğinizde kullanışlıdır.

    GET https://[service name].search.windows.net/indexes/[index name]/docs/[key]?[query parameters]
    api-key: [admin or query key]

**İstek**

HTTPS istekleri için gereklidir. Merhaba **arama belge** isteği oluşturulmasını gibi.

    GET /indexes/[index name]/docs/key?[query parameters]

Alternatif olarak, anahtar aramasını hello geleneksel OData sözdizimini kullanabilirsiniz:

    GET /indexes('[index name]')/docs('[key]')?[query parameters]

Merhaba istek URI içeren bir [dizin adı] ve [Temel], hangi belge tooretrieve hangi dizinden belirtme. Ayrıca, aynı anda yalnızca bir belge alabilir. Kullanım **arama** tooget tek bir istekte birden çok belge.

**Sorgu parametreleri**

`$select=[string]`(isteğe bağlı) - virgülle ayrılmış alanlar tooretrieve listesi. Belirtilmemiş veya çok ayarlarsanız`*`, hello şemada alınabilir olarak işaretlenmiş tüm alanlar hello projeksiyon dahil edilir.

`api-version=[string]`(gerekli). Merhaba Önizleme sürümü `api-version=2015-02-28-Preview`. Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri için.

Not: Bu işlem için hello `api-version` sorgu parametresi olarak belirtilir.

**İstek üstbilgileri**

liste aşağıdaki hello hello gerekli ve isteğe bağlı istek üstbilgileri açıklar.

* `api-key`: Merhaba `api-key` kullanılan tooauthenticate hello isteği tooyour arama hizmeti değil. Bir dize değeri, benzersiz tooyour hizmeti URL'si değil. Merhaba **arama belge** isteği, bir yönetici anahtarını veya sorgu anahtarı belirtebilirsiniz `api-key`.

Merhaba hizmet adı tooconstruct hello istek URL'si de gerekir. Merhaba hizmet adı alabilir ve `api-key` hizmeti Panonuzda hello Azure Portalı'ndan. Bkz: [hello portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.

**İstek gövdesi**

yok.

**Yanıt**

Durum kodu: 200 Tamam için başarılı bir yanıt döndürdü.

    {
      field_name: field_value (fields matching hello default or specified projection)
    }

**Örnek**

'2' anahtar içeriyor arama hello belge

    GET /indexes/hotels/docs/2?api-version=2015-02-28-Preview

'OData sözdizimini kullanarak 3' anahtarına sahip arama hello belge:

    GET /indexes('hotels')/docs('3')?api-version=2015-02-28-Preview

<a name="CountDocs"></a>

## <a name="count-documents"></a>Count belgeleri
Merhaba **sayısı belgeleri** işlemi arama dizini belgelerde hello sayısı sayısını alır. Merhaba `$count` sözdizimi hello OData protokolü bir parçasıdır.

    GET https://[service name].search.windows.net/indexes/[index name]/docs/$count?api-version=[api-version]
    Accept: text/plain
    api-key: [admin or query key]

**İstek**

HTTPS istekleri için gereklidir. Merhaba **sayısı belgeleri** isteği hello GET yöntemini kullanan olacak oluşturulan.

Merhaba [dizin adı] hello istek URI'SİNDEKİ hello hizmet tooreturn tüm öğelerin sayısını hello belgeleri koleksiyonundaki hello belirtilen dizin söyler.

`api-version=[string]`(gerekli). Merhaba Önizleme sürümü `api-version=2015-02-28-Preview`. Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri için.

**İstek üstbilgileri**

liste aşağıdaki hello hello gerekli ve isteğe bağlı istek üstbilgileri açıklar.

* `Accept`: Bu değeri çok ayarlanmalıdır`text/plain`.
* `api-key`: Merhaba `api-key` kullanılan tooauthenticate hello isteği tooyour arama hizmeti değil. Bir dize değeri, benzersiz tooyour hizmeti URL'si değil. Merhaba **sayısı belgeleri** isteği, bir yönetici anahtarını veya sorgu anahtarı belirtebilirsiniz `api-key`.

Merhaba hizmet adı tooconstruct hello istek URL'si de gerekir. Merhaba hizmet adı alabilir ve `api-key` hizmeti Panonuzda hello Azure Portalı'ndan. Bkz: [hello portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.

**İstek gövdesi**

yok.

**Yanıt**

Durum kodu: 200 Tamam için başarılı bir yanıt döndürdü.

Merhaba yanıt gövdesi, düz metin olarak biçimlendirilmiş bir tamsayı olarak hello sayısı değeri içerir.

<a name="Suggestions"></a>

## <a name="suggestions"></a>Öneriler
Merhaba **önerileri** işlemi kısmi arama girişinize göre önerileri alır. Kullanıcıların arama terimi girerek gibi genellikle arama kutuları tooprovide yazarken tamamlanan önerilerine kullanılır.

Öneri istekleri hedef belgeler öneren adresindeki hedeflenir, birden çok adayı belgeleri hello eşleşiyorsa metin yinelenebilir hello önerilen şekilde aynı giriş arayın. Kullanabileceğiniz `$select` tooretrieve diğer belge (Merhaba belge anahtar dahil) alanları böylece hangi belge hello her öneri kaynağıdır anlayabilirsiniz.

A **önerileri** işlem bir GET veya POST isteği verildi.

    GET https://[service name].search.windows.net/indexes/[index name]/docs/suggest?[query parameters]
    api-key: [admin or query key]

    POST https://[service name].search.windows.net/indexes/[index name]/docs/suggest?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin or query key]

**Toouse yerine duyurduğumuzda Al**

HTTP GET toocall hello kullandığınızda **önerileri** API, toobe hello istek URL'si hello uzunluğu 8 KB'yi aşamaz kullanan gerekir. Çoğu uygulama için yeterince genellikle budur. Ancak, bazı uygulamalar çok büyük sorgular, özellikle OData filtre ifadeleri üretir. GET daha büyük filtreleri sağladığından bu uygulamalar için HTTP POST kullanılarak daha iyi bir seçimdir. POST, ile birlikte bir filtre yan tümcelerinde hello sayısı hello sınırlama faktörü, POST için hello isteği boyut sınırı yaklaşık 16 MB olduğundan hello ham filtre dizesi boyutunu hello değil.

> [!NOTE]
> Merhaba POST isteği boyut sınırı çok büyük olsa da, filtre ifadeleri rasgele karmaşık olamaz. Bkz: [OData ifade sözdizimini](https://msdn.microsoft.com/library/dn798921.aspx) filtre karmaşıklık sınırlamalar hakkında daha fazla bilgi.
> 
> 

**İstek**

HTTPS istekleri için gereklidir. Merhaba **önerileri** isteği hello GET veya POST yöntemleri kullanarak olacak oluşturulan.

Merhaba isteğin URI hello dizin tooquery hello adını belirtir. Merhaba kısmen giriş arama terimi gibi parametreleri hello sorgu dizesinde GET isteklerinin hello durumda belirtilir ve hello istekte hello durumunun POST gövdesinde ister.

GET isteklerini oluştururken en iyi uygulama, çok unutmayın[URL kodlama](https://msdn.microsoft.com/library/system.uri.escapedatastring.aspx) çağrılırken parametreleri hello REST API doğrudan belirli sorgu. İçin **önerileri** bu işlemleri içerir:

* `$filter`
* `highlightPreTag`
* `highlightPostTag`
* `search`

URL kodlaması sorgu parametreleri yukarıda hello üzerinde yalnızca önerilir. Tüm sorgu dizesi (her şeyi hello sonra?), yanlışlıkla URL kodlama Merhaba, istekleri çalışmamasına neden olur.

Ayrıca, URL kodlaması yalnızca REST API kullanarak doğrudan alma hello çağrılırken gereklidir. Hiçbir URL kodlaması çağrılırken gereklidir **önerileri** POST, kullanma ya da hello kullanırken [.NET istemci kitaplığını](https://msdn.microsoft.com/library/dn951165.aspx), sizin için URL kodlaması işler.

**Sorgu parametreleri**

**Öneriler** sorgu ölçütlerini sağlayan ve ayrıca arama davranışını belirtin birkaç parametre kabul eder. Bu parametreler hello URL'deki sorgu dizesi çağrılırken sağladığınız **önerileri** GET aracılığıyla ve JSON özellikleri çağrılırken hello istek gövdesi olarak **önerileri** POST ile. bazı parametreler için Hello sözdizimi GET ve POST arasında biraz farklıdır. Bu farklılıklar, geçerli aşağıda belirtilmiştir:

`search=[string]`-arama metni toouse toosuggest sorguları hello. En az 1 karakter ve en fazla 100 karakter olmalıdır.

`highlightPreTag=[string]`(isteğe bağlı) - toosearch isabet başına bir dize etiketi. İle ayarlanmalıdır `highlightPostTag`.

> [!NOTE]
> Çağrılırken **önerileri** GET kullanarak, ayrılmış karakter hello URL (örneğin, % &#23; yerine) yüzde olarak kodlanmış olmalıdır.
> 
> 

`highlightPostTag=[string]`(isteğe bağlı) - toosearch isabet ekler bir dize etiketi. İle ayarlanmalıdır `highlightPreTag`.

> [!NOTE]
> Çağrılırken **önerileri** GET kullanarak, ayrılmış karakter hello URL (örneğin, % &#23; yerine) yüzde olarak kodlanmış olmalıdır.
> 
> 

`suggesterName=[string]`-Belirtilen hello olarak hello öneri aracı adını hello `suggesters` hello dizin tanımının bir parçası olan koleksiyonu. A `suggester` hangi alanlar için önerilen sorgu terimlerinin taranır belirler. Bkz: [ilgili](#Suggesters) Ayrıntılar için.

`fuzzy=[boolean]`(isteğe bağlı, varsayılan = false)-tootrue bu ayarlandığında olsa bile bir yedek veya eksik karakter hello arama metnini API öneriler bulacaksınız. Bu bazı senaryolarda daha iyi bir deneyim sağlarken benzer bir öneri aramalar daha yavaş ve daha fazla kaynak tüketmesine maliyeti performanslarının gelir.

`searchFields=[string]`(isteğe bağlı) - hello için virgülle ayrılmış bir alan adları toosearch hello listesi belirtilen arama metni. Hedef alan önerileri için etkinleştirilmesi gerekir.

`$top=#`(isteğe bağlı, varsayılan = 5)-hello önerileri tooretrieve sayısı. 1 ile 100 arasında bir sayı olmalıdır.

> [!NOTE]
> Çağrılırken **önerileri** POST kullanarak, bu parametre adlı `top` yerine `$top`.
> 
> 

`$filter=[string]`(isteğe bağlı) - hello belgeleri filtreleyen bir ifade için öneriler kabul edilir.

> [!NOTE]
> Çağrılırken **önerileri** POST kullanarak, bu parametre adlı `filter` yerine `$filter`.
> 
> 

`$orderby=[string]`(isteğe bağlı) - virgülle ayrılmış ifadeler toosort hello sonuçlarına göre listesi. Her bir ifadenin bir alan adı veya bir çağrı toohello olabilir `geo.distance()` işlevi. Her deyim tarafından izlenebilir `asc` artan, tooindicated ve `desc` azalan tooindicate. Merhaba varsayılan, artan. Bir sınır için 32 yan `$orderby`.

> [!NOTE]
> Çağrılırken **önerileri** POST kullanarak, bu parametre adlı `orderby` yerine `$orderby`.
> 
> 

`$select=[string]`(isteğe bağlı) - virgülle ayrılmış alanlar tooretrieve listesi. Belirtilmezse, yalnızca belge anahtarını hello ve öneri metni döndürülür. Bu parametre çok ayarlayarak tüm alanları açıkça isteyebilir`*`.

> [!NOTE]
> Çağrılırken **önerileri** POST kullanarak, bu parametre adlı `select` yerine `$select`.
> 
> 

`minimumCoverage`(isteğe bağlı, varsayılan olarak too80) - 0 ve öneriler sorgu hello sorgu toobe sırada tarafından ele alınması gereken hello dizin hello yüzdesini gösteren 100 arasında bir sayı başarı bildirdi. Varsayılan olarak, en az % 80 hello dizini kullanılabilir olmalıdır veya `Suggest` 503 HTTP durum kodunu döndürür. Ayarlarsanız `minimumCoverage` ve `Suggest` başarılı, HTTP 200 dönün ve içeren bir `@search.coverage` hello yanıt hello sorguda eklenmiştir hello dizin hello yüzdesini belirten değer.

> [!NOTE]
> Bu parametre tooa değerin 100 Hizmetleri ile yalnızca bir çoğaltma için bile arama kullanılabilirlik sağlamak için yararlı olabilir. daha düşük ayarlanması. Ancak, tüm eşleşen öneri toobe hello sonuçlarında mevcut sağlanır. Geri çağırma kullanılabilirlik sonra onun değil toolower en iyi daha fazla önemli tooyour uygulama ise `minimumCoverage` varsayılan değerini 80 aşağıda.
> 
> 

`api-version=[string]`(gerekli). Merhaba Önizleme sürümü `api-version=2015-02-28-Preview`. Bkz: [arama hizmet sürümü oluşturma](http://msdn.microsoft.com/library/azure/dn864560.aspx) Ayrıntılar ve diğer sürümleri için.

Not: Bu işlem için hello `api-version` olup, çağrı bağımsız olarak hello URL'deki sorgu parametresi olarak belirtilen **önerileri** GET veya POST ile.

**İstek üstbilgileri**

liste aşağıdaki hello hello gerekli ve isteğe bağlı istek üstbilgileri açıklar

* `api-key`: Merhaba `api-key` kullanılan tooauthenticate hello isteği tooyour arama hizmeti değil. Bir dize değeri, benzersiz tooyour hizmeti URL'si değil. Merhaba **önerileri** isteği hello bir yönetici anahtarını veya sorgu anahtarını belirtebilirsiniz `api-key`.

Merhaba hizmet adı tooconstruct hello istek URL'si de gerekir. Merhaba hizmet adı alabilir ve `api-key` hizmeti Panonuzda hello Azure Portalı'ndan. Bkz: [hello portalda Azure Search hizmeti oluşturma](search-create-service-portal.md) sayfa gezinti Yardım.

**İstek gövdesi**

GET için: yok.

POST için:

    {
      "filter": "odata_filter_expression",
      "fuzzy": true | false (default),
      "highlightPreTag": "pre_tag",
      "highlightPostTag": "post_tag",
      "minimumCoverage": # (% of index that must be covered toodeclare query successful; default 80),
      "orderby": "orderby_expression",
      "search": "partial_search_input",
      "searchFields": "field_name_1, field_name_2, ...",
      "select": "field_name_1, field_name_2, ...",
      "suggesterName": "suggester_name",
      "top": # (default 5)
    }

**Yanıt**

Durum kodu: 200 Tamam için başarılı bir yanıt döndürdü.

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
        },
        ...
      ]
    }

Merhaba projeksiyon seçeneği hello dizinin her bir öğesinde bulunan kullanılan tooretrieve alanları ise:

    {
      "@search.coverage": # (if minimumCoverage was provided in hello query),
      "value": [
        {
          "@search.text": "...",
          "<key field>": "..."
          <other projected data fields>
        },
        ...
      ]
    }

**Örnek**

Merhaba kısmi arama giriş 'lux' olduğu 5 önerileri Al

    GET /indexes/hotels/docs/suggest?search=lux&$top=5&suggesterName=sg&api-version=2015-02-28-Preview

    POST /indexes/hotels/docs/suggest?api-version=2015-02-28-Preview
    {
      "search": "lux",
      "top": 5,
      "suggesterName": "sg"
    }
