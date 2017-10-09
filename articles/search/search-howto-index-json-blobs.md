---
title: "Azure Search blob dizin oluşturucu ile aaaIndexing JSON BLOB'ları"
description: "Dizin oluşturma JSON BLOB'ları ile Azure Search blob dizin oluşturucu"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 57e32e51-9286-46da-9d59-31884650ba99
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/10/2017
ms.author: eugenesh
ms.openlocfilehash: 269968714358cd40ea66863b4dbb97766e1d77e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-json-blobs-with-azure-search-blob-indexer"></a>Dizin oluşturma JSON BLOB'ları ile Azure Search blob dizin oluşturucu
Bu makale, JSON içeren BLOB'ları içerikten tooconfigure Azure Search blob dizin oluşturucu tooextract nasıl yapılandırılmış gösterir.

## <a name="scenarios"></a>Senaryolar
Varsayılan olarak, [Azure Search blob dizin oluşturucu](search-howto-indexing-azure-blob-storage.md) JSON BLOB'ları tek bir metin öbek ayrıştırır. Genellikle, JSON belgelerini toopreserve hello yapısı istiyorsunuz. Örneğin, hello JSON belgesi verilen

    {
        "article" : {
             "text" : "A hopefully useful article explaining how tooparse JSON blobs",
            "datePublished" : "2016-04-13"
            "tags" : [ "search", "storage", "howto" ]    
        }
    }

Azure Search içine belge "metin", "datePublished" ve "etiketler" alanları tooparse isteyebilirsiniz.

Alternatif olarak, ne zaman, BLOB'ları içeren bir **dizi JSON nesnesi**, her öğeye hello dizi toobecome ayrı bir Azure Search belge isteyebilirsiniz. Örneğin, bir blob bu JSON ile verilen:  

    [
        { "id" : "1", "text" : "example 1" },
        { "id" : "2", "text" : "example 2" },
        { "id" : "3", "text" : "example 3" }
    ]

Azure Search dizininizi üç ayrı belgelerle, her "id" ve "metin" alanları ile doldurabilirsiniz.

> [!IMPORTANT]
> işlevselliği ayrıştırma hello JSON dizisi şu anda önizlemede değil. Sürüm kullanarak yalnızca hello REST API kullanılabilir **2015-02-28-Önizleme**. Unutmayın, Önizleme API'leri sınama ve değerlendirme için tasarlanmıştır ve üretim ortamlarında kullanılmamalıdır.
>
>

## <a name="setting-up-json-indexing"></a>JSON dizin oluşturmayı ayarlama
JSON BLOB'ları dizin benzer toohello normal belge ayıklama olur. İlk olarak, tam olarak normal olarak hello veri kaynağı oluşturun: 

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "optional, my-folder" }
    }   

Zaten yoksa, hello hedef arama dizini oluşturun. 

Son olarak bir dizin oluşturucu oluşturup hello `parsingMode` parametresi çok`json` (tooindex her blob tek bir belgenin) veya `jsonArray` (bloblarınızın JSON dizileri içerir ve ayrı bir belge olarak kabul bir dizi toobe her öğeye ihtiyacınız varsa):

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-json-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "parameters" : { "configuration" : { "parsingMode" : "json" } }
    }

Gerekirse, kullanın **alan eşlemelerini** toopick hello sonraki bölümde gösterildiği gibi bu hello kaynak JSON kullanılan belge toopopulate özelliklerini hedef search dizininizi hello.

> [!IMPORTANT]
> Kullandığınızda `json` veya `jsonArray` modu ayrıştırma, Azure Search, veri kaynağındaki tüm BLOB'lar JSON içeren varsayar. Toosupport JSON bir karışımını gerekir ve JSON olmayan BLOB'hello aynı veri kaynağı, bize bilmeniz izin [UserVoice sitemizi](https://feedback.azure.com/forums/263029-azure-search).
>
>

## <a name="using-field-mappings-toobuild-search-documents"></a>Alan eşlemeleri toobuild arama belgeleri kullanma
Yalnızca ilkel veri türleri, dize dizileri ve GeoJSON noktaları desteklediğinden, şu anda, Azure Search rastgele JSON belgelerinin doğrudan dizin oluşturulamıyor. Ancak, kullanabileceğiniz **alan eşlemelerini** , JSON toopick bölümlerini belge ve "bunları hello arama belge üst düzey alanlarına Yükselt". alan eşlemeleri temel kavramlarıyla ilgili toolearn bkz [Azure Search dizin oluşturucu alan eşlemelerini köprü hello farklarını veri kaynakları ve arama dizinlerini](search-indexer-field-mappings.md).

Tooour örnek JSON belgesi gelmeye:

    {
        "article" : {
             "text" : "A hopefully useful article explaining how tooparse JSON blobs",
            "datePublished" : "2016-04-13"
            "tags" : [ "search", "storage", "howto" ]    
        }
    }

Alanları aşağıdaki hello ile arama dizini sahip varsayalım: `text` türü `Edm.String`, `date` türü `Edm.DateTimeOffset`, ve `tags` türü `Collection(Edm.String)`. toomap, JSON hello içinde istenen şekil, alan eşlemelerini aşağıdaki hello kullanın:

    "fieldMappings" : [
        { "sourceFieldName" : "/article/text", "targetFieldName" : "text" },
        { "sourceFieldName" : "/article/datePublished", "targetFieldName" : "date" },
        { "sourceFieldName" : "/article/tags", "targetFieldName" : "tags" }
      ]

Merhaba hello eşlemeleri kaynak alan adlarının hello kullanılarak belirtilir [JSON işaretçi](http://tools.ietf.org/html/rfc6901) gösterimi. JSON belgesinin kök eğik toorefer toohello ile başlayın, ardından İleri eğik ayrılmış yolu kullanılarak istenen hello özelliği (düzeyinde rasgele iç içe geçme) seçin.

Sıfır tabanlı dizini kullanılarak tooindividual dizi öğeleri de başvurabilir. Örneğin, toopick hello ilk öğesi hello "etiketler" Merhaba örnek, yukarıda diziden, böyle bir alan eşleme kullanın:

    { "sourceFieldName" : "/article/tags/0", "targetFieldName" : "firstTag" }

> [!NOTE]
> Bir kaynak alan adı bir alan eşleme yolunda JSON'de yok tooa özelliği başvuruyorsa, bu eşlemeyi hatasız atlanır. Bu, böylece (ortak kullanım örneği olan) farklı bir şema belgelerle destekliyoruz gerçekleştirilir. Hiçbir doğrulama olduğundan, alan eşleme belirtimi tootake dikkatli tooavoid hatalarını gerekir.
>
>

JSON belgeleri yalnızca basit en üst düzey özellikler içeriyorsa, alan eşlemelerini hiç gerekmeyebilir. Örneğin, JSON Bu, hello en üst düzey özellikleri "metin" gibi görünüyorsa, "datePublished" ve "etiketler" doğrudan eşler hello arama dizini karşılık gelen alanlara toohello:

    {
       "text" : "A hopefully useful article explaining how tooparse JSON blobs",
       "datePublished" : "2016-04-13"
       "tags" : [ "search", "storage", "howto" ]    
     }

Alan eşlemelerini içeren bir tam dizin oluşturucu yükü şöyledir:

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "my-json-indexer",
      "dataSourceName" : "my-blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "parameters" : { "configuration" : { "parsingMode" : "json" } },
      "fieldMappings" : [
        { "sourceFieldName" : "/article/text", "targetFieldName" : "text" },
        { "sourceFieldName" : "/article/datePublished", "targetFieldName" : "date" },
        { "sourceFieldName" : "/article/tags", "targetFieldName" : "tags" }
        ]
    }

## <a name="indexing-nested-json-arrays"></a>İç içe JSON diziler dizin oluşturma
Bir dizi JSON nesnesi, ancak bu diziyi tooindex ne istediğiniz yere hello belge içinde iç içe yerleştirilmiş? Hangi özelliği hello kullanarak hello dizi içerir çekme `documentRoot` Yapılandırma özelliği. Örneğin, BLOB'ları şöyle görünür:

    {
        "level1" : {
            "level2" : [
                { "id" : "1", "text" : "Use hello documentRoot property" },
                { "id" : "2", "text" : "toopluck hello array you want tooindex" },
                { "id" : "3", "text" : "even if it's nested inside hello document" }  
            ]
        }
    }

Hello bulunan bu yapılandırma tooindex hello dizisini kullanan `level2` özelliği:

    {
        "name" : "my-json-array-indexer",
        ... other indexer properties
        "parameters" : { "configuration" : { "parsingMode" : "jsonArray", "documentRoot" : "/level1/level2" } }
    }

## <a name="help-us-make-azure-search-better"></a>Azure Search iyileştirmemize yardımcı olun
Özellik istekleri veya fikir geliştirmeleri için varsa, üzerinde toous ulaşmak bizim [UserVoice sitesinde](https://feedback.azure.com/forums/263029-azure-search/).
