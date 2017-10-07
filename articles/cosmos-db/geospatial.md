---
title: "Azure Cosmos veritabanı Jeo-uzamsal verilerle aaaWorking | Microsoft Docs"
description: "Nasıl toocreate, dizin ve Azure Cosmos DB uzamsal nesneleriyle sorgulamak ve DocumentDB API hello anlayın."
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: 82ce2898-a9f9-4acf-af4d-8ca4ba9c7b8f
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/22/2017
ms.author: arramac
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a1e40b78cb4595631d845d46c21d07a30c8b972f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-geospatial-and-geojson-location-data-in-azure-cosmos-db"></a>Jeo-uzamsal ve Azure Cosmos veritabanı GeoJSON konum verileri ile çalışma
Bu makalede bir giriş toohello Jeo-uzamsal işlevindeki olan [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/). Bu okuduktan sonra aşağıdaki soruları mümkün tooanswer hello olacaktır:

* Azure Cosmos DB'de nasıl uzamsal veri depoluyor?
* Azure Cosmos DB'de SQL ve LINQ Jeo-uzamsal verileri nasıl sorgulama yapabilirsiniz?
* Nasıl etkinleştirmek veya Azure Cosmos DB'de uzamsal dizin oluşturmayı devre dışı?

Bu makalede nasıl toowork uzamsal verilerle ile Merhaba DocumentDB API gösterilmektedir. Lütfen bu bakın [GitHub proje](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Geospatial/Program.cs) kod örnekleri için.

## <a name="introduction-toospatial-data"></a>Giriş toospatial veri
Uzamsal veri hello konumu ve Şekil alanı nesnelerin açıklar. Çoğu uygulamada bu Merhaba Dünya, yani Jeo-uzamsal veriler üzerindeki tooobjects karşılık gelir. Uzamsal veriler, bir kişinin kullanılan toorepresent hello konum, ilgilendiğiniz bir yerde ya da bir şehir veya bir lake hello sınırını olabilir. Ortak kullanım durumları yakınlık sorguları, örneğin, "tüm kafeterya my geçerli konumu bulmak" için sıklıkla içerir. 

### <a name="geojson"></a>GeoJSON
Dizin oluşturma ve hello kullanarak temsil edilen Jeo-uzamsal noktası verileri Sorgulama Azure Cosmos DB destekler [GeoJSON belirtimi](https://tools.ietf.org/html/rfc7946). Böylece depolanabilir ve herhangi bir özel araçlar veya kitaplıkları Azure Cosmos DB kullanarak sorgulanan GeoJSON veri yapıları her zaman geçerli JSON, nesneleridir. Hello Azure Cosmos DB SDK'ları yardımcı sınıfları ve uzamsal verileri içeren kolay toowork olun yöntemleri sağlar. 

### <a name="points-linestrings-and-polygons"></a>Noktaları, MultiPoint ve çokgenler
A **noktası** alanı tek bir konumda gösterir. Jeo-uzamsal verileri bir noktası Market, bir bilgi noktası, bir otomobil veya bir şehir sokak adresi olabilir hello tam konumunu temsil eder.  Bir noktayı kendi koordinat kullanarak GeoJSON (ve Azure Cosmos DB) çifti veya boylam ve enlem temsil edilir. Bir noktası için JSON örnek aşağıda verilmiştir.

**Azure Cosmos DB noktaları**

```json
{
    "type":"Point",
    "coordinates":[ 31.9, -4.8 ]
}
```

> [!NOTE]
> Merhaba GeoJSON belirtimi belirtir boylam ilk ve enlem ikinci. Gibi diğer eşleme uygulamalarda boylam ve enlem açıları ve derece cinsinden temsil. Boylam değerleri Meridyeninden hello ölçülür ve -180 ve 180.0 derece ve enlem değerleri hello ekvatora ölçülür ve-90.0 arasında olan ve 90.0 derece. 
> 
> Azure Cosmos DB koordinatları hello WGS 84 başvuru sistemi belirtildiği şekilde yorumlar. Lütfen koordinat başvuru sistemleri hakkında daha fazla bilgi için aşağıya bakın.
> 
> 

Bu bir Azure Cosmos DB belgesinde konum verileri içeren bir kullanıcı profili bu örnekte gösterildiği gibi katıştırılabilen:

**Azure Cosmos DB içinde depolanan konumla profilini kullan**

```json
{
    "id":"documentdb-profile",
    "screen_name":"@CosmosDB",
    "city":"Redmond",
    "topics":[ "global", "distributed" ],
    "location":{
        "type":"Point",
        "coordinates":[ 31.9, -4.8 ]
    }
}
```

Ayrıca toopoints, GeoJSON MultiPoint ve çokgenler destekler. **MultiPoint** alanı iki veya daha fazla noktaları bir dizi temsil eder ve bunları bağlamak çizgi dilimleri hello. Jeo-uzamsal verinin, yaygın olarak kullanılan toorepresent Otoyollar veya rivers MultiPoint içindedir. A **Çokgen** kapalı LineString forms bir sınırı bağlı noktalarının. Çokgenler Göller gibi yaygın olarak kullanılan toorepresent doğal durum oluşumlarıyla veya şehir ve durumlar gibi siyasi daireleri markalarıdır. Burada, Azure Cosmos veritabanı çokgenin bir örnek verilmiştir. 

**GeoJSON'daki çokgenler**

```json
{
    "type":"Polygon",
    "coordinates":[
        [ 31.8, -5 ],
        [ 31.8, -4.7 ],
        [ 32, -4.7 ],
        [ 32, -5 ],
        [ 31.8, -5 ]
    ]
}
```

> [!NOTE]
> Merhaba geçerli çokgenler için hello sağlanan son koordinat çifti olması gerektiğini belirtilmesini gerektiriyor GeoJSON hello aynı hello ilk toocreate kapalı bir şekil.
> 
> Çokgen içindeki noktaları yönünün sırayla belirtilmelidir. Belirtilen saat yönünde sırayla Çokgen hello bölgesinde hello tersini temsil eder.
> 
> 

Ayrıca tooPoint, LineString ve Çokgen GeoJSON de nasıl hello gösterimi belirtir. toogroup yanı sıra birden çok Jeo-uzamsal konumları tooassociate rasgele coğrafi konuma özelliklerle bir **özelliği**. Bu nesneler geçerli JSON olduğundan, bunlar tüm depolanabilir ve Azure Cosmos DB'de işlenebilir. Ancak Azure Cosmos DB yalnızca noktalarının otomatik dizin oluşturma işlemi destekler.

### <a name="coordinate-reference-systems"></a>Koordinat başvuru sistemleri
Merhaba Dünya Hello şeklini düzensiz olduğundan Jeo-uzamsal veri koordinatlarını sistemlerindeki birçok koordinat başvurusu (CR), her biri kendi çerçeveler başvuru ve ölçü gösterilir. Örneğin, "Britanya Ulusal kılavuz" Merhaba başvuru sistemi çok doğru ise hello İngiltere, ancak değil dışında. 

Merhaba kullanımda en popüler CRS bugün hello World Geodetic sistem olan [WGS 84](http://earth-info.nga.mil/GandG/wgs84/). GPS aygıtları ve Google Haritalar ve Bing haritaları API'si dahil olmak üzere birçok eşleme Hizmetleri WGS 84 kullanın. Azure Cosmos DB dizin oluşturma ve Jeo-uzamsal verileri yalnızca WGS 84 CRS hello kullanarak sorgulama destekler. 

## <a name="creating-documents-with-spatial-data"></a>Uzamsal verilerle belgeleri oluşturma
GeoJSON değerleri içeren belgeleri oluşturduğunuzda, bunlar otomatik olarak uygun toohello dizin oluşturma ilkesi hello koleksiyonunun uzamsal dizine sahip dizine alınır. Bir Azure Cosmos DB SDK'sı ile Python veya Node.js gibi dinamik olarak yazılan bir dilde çalışıyorsanız, geçerli GeoJSON oluşturmanız gerekir.

**Node.js içinde Jeo-uzamsal verilerle belge oluşturma**

```json
var userProfileDocument = {
    "name":"documentdb",
    "location":{
        "type":"Point",
        "coordinates":[ -122.12, 47.66 ]
    }
};

client.createDocument(`dbs/${databaseName}/colls/${collectionName}`, userProfileDocument, (err, created) => {
    // additional code within hello callback
});
```

Merhaba DocumentDB API'leri ile çalışıyorsanız, hello kullanabilirsiniz `Point` ve `Polygon` hello sınıfları `Microsoft.Azure.Documents.Spatial` uygulama nesnelerinizi içindeki ad alanı tooembed konum bilgileri. Bu sınıfların hello seri hale getirme ve seri durumdan çıkarma uzamsal veri GeoJSON içine kolaylaştırmaya yardımcı.

**.NET Jeo-uzamsal verilerle belge oluşturma**

```json
using Microsoft.Azure.Documents.Spatial;

public class UserProfile
{
    [JsonProperty("name")]
    public string Name { get; set; }

    [JsonProperty("location")]
    public Point Location { get; set; }

    // More properties
}

await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "profiles"), 
    new UserProfile 
    { 
        Name = "documentdb", 
        Location = new Point (-122.12, 47.66) 
    });
```

Merhaba enlem ve boylam bilgilere sahip değilseniz, ancak hello fiziksel adreslerini veya şehir veya ülke gibi konum adı, Bing Haritalar REST Hizmetleri gibi bir coğrafi kodlama hizmet kullanarak hello gerçek koordinatları bakabilirsiniz. Bing Haritalar coğrafi kodlama hakkında daha fazla bilgi [burada](https://msdn.microsoft.com/library/ff701713.aspx).

## <a name="querying-spatial-types"></a>Uzamsal türler sorgulama
Biz nasıl göz ayırdıktan göre tooinsert Jeo-uzamsal veriler, nasıl bir göz atalım tooquery Azure Cosmos SQL ve LINQ kullanarak DB kullanarak bu verileri.

### <a name="spatial-sql-built-in-functions"></a>Uzamsal SQL yerleşik işlevler
Azure Cosmos DB Jeo-uzamsal sorgulamak için yerleşik işlevler açık Jeo-uzamsal Konsorsiyumu (OGC) aşağıdaki hello destekler. Merhaba eksiksiz hello SQL dil yerleşik işlevler hakkında daha fazla ayrıntı için lütfen çok başvurun[sorgu Azure Cosmos DB](documentdb-sql-query.md).

<table>
<tr>
  <td><strong>Kullanım</strong></td>
  <td><strong>Açıklama</strong></td>
</tr>
<tr>
  <td>St_dıstance (spatial_expr, spatial_expr)</td>
  <td>Merhaba iki GeoJSON noktası, çokgen veya LineString ifadeleri arasında Hello uzaklığını döndürür.</td>
</tr>
<tr>
  <td>ST_WITHIN (spatial_expr, spatial_expr)</td>
  <td>Merhaba ilk GeoJSON nesne (noktası, çokgen veya LineString) hello ikinci GeoJSON nesne içinde (noktası, çokgen veya LineString) olup olmadığını gösteren bir Boole ifadesi döndürür.</td>
</tr>
<tr>
  <td>ST_INTERSECTS (spatial_expr, spatial_expr)</td>
  <td>Merhaba iki belirtilen GeoJSON nesne (noktası, çokgen veya LineString) kesiştiği olup olmadığını gösteren bir Boole ifadesi döndürür.</td>
</tr>
<tr>
  <td>ST_ISVALID</td>
  <td>Merhaba GeoJSON noktası, çokgen veya LineString ifadesi geçerli belirtilen olup olmadığını gösteren bir Boole değeri döndürür.</td>
</tr>
<tr>
  <td>ST_ISVALIDDETAILED</td>
  <td>Merhaba GeoJSON noktası, çokgen veya LineString ifade belirtilmişse bir Boole değeri içeren bir JSON değeri geçerli değil ve geçersiz, ayrıca bir dize değeri olarak neden hello döndürür.</td>
</tr>
</table>

Uzamsal işlevleri kullanılan tooperform yakınlık sorguları uzamsal veri olabilir. Örneğin, tüm ailesi hello st_dıstance yerleşik işlevi belirtilen konum içinde 30 km hello birini kullanarak belgeleri döndüren bir sorgu aşağıdadır. 

**Sorgu**

    SELECT f.id 
    FROM Families f 
    WHERE ST_DISTANCE(f.location, {'type': 'Point', 'coordinates':[31.9, -4.8]}) < 30000

**Sonuçları**

    [{
      "id": "WakefieldFamily"
    }]

Dizin oluşturma ilkenizi uzamsal dizin oluşturma eklerseniz, "uzaklığı sorguları" verimli bir şekilde hello dizin sunulacak. Uzamsal dizin oluşturma hakkında daha fazla ayrıntı için lütfen hello bölümüne bakın. Bir uzamsal yoksa dizini hello için belirtilen yol, belirterek hala uzaysal sorgular gerçekleştirebilir `x-ms-documentdb-query-enable-scan` hello değerle istek üstbilgisi çok "true" ayarlayın. .NET içinde bu geçirme hello tarafından isteğe bağlı yapılabilir **FeedOptions** bağımsız değişkeni tooqueries ile [EnableScanInQuery](https://msdn.microsoft.com/library/microsoft.azure.documents.client.feedoptions.enablescaninquery.aspx#P:Microsoft.Azure.Documents.Client.FeedOptions.EnableScanInQuery) tootrue ayarlayın. 

Bir noktayı Çokgen içinde yer alıyorsa ST_WITHIN kullanılan toocheck olabilir. Yaygın olarak kullanılan toorepresent sınırları posta kodları, durumu sınırları veya doğal durum oluşumlarıyla gibi çokgenler değildir. Dizin oluşturma ilkenizi uzamsal dizin oluşturma eklerseniz, yeniden sonra "içindeki" sorguları verimli bir şekilde hello dizin sunulacak. 

Yalnızca tek bir halka ST_WITHIN Çokgen değişkenlerinde içerebilir, yani hello çokgenler bunlara boşluklar içermemelidir. 

**Sorgu**

    SELECT * 
    FROM Families f 
    WHERE ST_WITHIN(f.location, {
        'type':'Polygon', 
        'coordinates': [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
    })

**Sonuçları**

    [{
      "id": "WakefieldFamily",
    }]

> [!NOTE]
> Benzer eşleşmeyen toohow türleri çalışmadığını Azure Cosmos DB sorgu, hatalı biçimlendirilmiş veya geçersiz bağımsız değişken sonra çok değerlendirecek hello konum değeri belirtilen**tanımsız** ve hesaplanan hello belge toobe hello atlandı Sorgu sonuçları. Sorgunuz hiçbir sonuç döndürmezse neden hello spatail türü geçersiz ST_ISVALIDDETAILED toodebug çalıştırın.     
> 
> 

Ters sorgular gerçekleştirme Azure Cosmos DB de destekler, yani, çokgenler veya Azure Cosmos DB satırlarında dizin sonra belirtilen bir nokta içermesi için hello alanlar sorgu. Bu desen Lojistik tooidentify yaygın olarak kullanılan örneğin ne zaman bir kamyonu girer ya da belirlenen alan bırakır. 

**Sorgu**

    SELECT * 
    FROM Areas a 
    WHERE ST_WITHIN({'type': 'Point', 'coordinates':[31.9, -4.8]}, a.location)


**Sonuçları**

    [{
      "id": "MyDesignatedLocation",
      "location": {
        "type":"Polygon", 
        "coordinates": [[[31.8, -5], [32, -5], [32, -4.7], [31.8, -4.7], [31.8, -5]]]
      }
    }]

Uzamsal nesne geçerli ise ST_ISVALID ve ST_ISVALIDDETAILED kullanılan toocheck olabilir. Örneğin, sorgu aşağıdaki hello noktasının hello geçerlilik aralığı enlem değeri (-132.8) dışı ile denetler. ST_ISVALID yalnızca bir Boole değeri döndürür ve Boole ve neden geçersiz değerlendirilir hello neden içeren bir dize hello ST_ISVALIDDETAILED döndürür.

** Sorgu **

    SELECT ST_ISVALID({ "type": "Point", "coordinates": [31.9, -132.8] })

**Sonuçları**

    [{
      "$1": false
    }]

Bu işlevler de kullanılan toovalidate çokgenler olabilir. Örneğin, burada ST_ISVALIDDETAILED toovalidate kapalı bir Çokgen kullanırız. 

**Sorgu**

    SELECT ST_ISVALIDDETAILED({ "type": "Polygon", "coordinates": [[ 
        [ 31.8, -5 ], [ 31.8, -4.7 ], [ 32, -4.7 ], [ 32, -5 ] 
        ]]})

**Sonuçları**

    [{
       "$1": { 
            "valid": false, 
            "reason": "hello Polygon input is not valid because hello start and end points of hello ring number 1 are not hello same. Each ring of a Polygon must have hello same start and end points." 
          }
    }]

### <a name="linq-querying-in-hello-net-sdk"></a>LINQ sorgusu hello .NET SDK içinde
Merhaba DocumentDB .NET SDK'sı sağlayıcıları yöntemleri de saplama `Distance()` ve `Within()` LINQ ifadeleri içinde kullanmak için. Merhaba DocumentDB LINQ sağlayıcısı çevirir bu yöntem çağrıları toohello eşdeğer SQL yerleşik işlev çağrıları (st_dıstance ve ST_WITHIN sırasıyla). 

"Konum" değeri 30 km Merhaba, bir RADIUS içinde belirtilen hello Azure Cosmos DB koleksiyonunda tüm belgeleri bulur bir LINQ Sorgu örneği noktası LINQ kullanarak burada ait.

**LINQ sorgusu için uzaklık**

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(u => u.ProfileType == "Public" && a.Location.Distance(new Point(32.33, -4.66)) < 30000))
    {
        Console.WriteLine("\t" + user);
    }

Benzer şekilde, "Konum" Merhaba içinde olduğu tüm hello belgeleri kutusunu/Çokgen belirtilen bulmak için bir sorgu İşte. 

**İçinde LINQ sorgulamak için**

    Polygon rectangularArea = new Polygon(
        new[]
        {
            new LinearRing(new [] {
                new Position(31.8, -5),
                new Position(32, -5),
                new Position(32, -4.7),
                new Position(31.8, -4.7),
                new Position(31.8, -5)
            })
        });

    foreach (UserProfile user in client.CreateDocumentQuery<UserProfile>(UriFactory.CreateDocumentCollectionUri("db", "profiles"))
        .Where(a => a.Location.Within(rectangularArea)))
    {
        Console.WriteLine("\t" + user);
    }


Biz nasıl göz ayırdıktan göre LINQ ve SQL, kullanarak tooquery belgeleri nasıl bir göz atalım uzamsal dizin oluşturma için Azure Cosmos DB tooconfigure.

## <a name="indexing"></a>Dizinleme
Biz hello açıklandığı gibi [belirsiz şema dizin Azure Cosmos DB ile](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) kağıt, biz tasarlanmış Azure Cosmos veritabanı veritabanı altyapısı toobe gerçekten şema belirsiz ve JSON için birinci sınıf destek sağlar. Merhaba en iyi duruma getirilmiş yazma veritabanı motoruna Azure Cosmos DB yerel olarak hello GeoJSON standardında temsil uzamsal veriler (noktaları, çokgenler ve satırları) bilir.

Buna koysalar hello geometri 2B düzlemi üzerine geodetic koordinatları gelen öngörülen sonra aşamalı olarak kullanarak hücrelere bölünmüş bir **quadtree**. Bu hücreler hello hücrenin içinde hello konumuna bağlı olarak eşlenen too1D olan bir **Hilbert alanı doldurma eğri**, yerleşim yeri noktalarının korur. Konum verileri sıralandığında ayrıca olarak bilinen bir işlemle gidiyor **Mozaik döşeme**, yani bir konum kesiştiği tüm hello hücreleri tanımlanır ve anahtarları'hello Azure Cosmos DB dizini olarak depolanır. Sorgu zaman noktaları ve çokgenler grubun Mozaik tooextract gibi bağımsız değişkenler ilgili hücre kimliği aralıkları hello sonra tooretrieve veri hello dizinden kullanılan.

Uzamsal dizini içeren bir dizin oluşturma ilkesini belirtirseniz / * (tüm yolları) hello koleksiyonu içinde bulunan tüm noktalarını verimli uzamsal sorguları için (ST_WITHIN ve st_dıstance) dizine sonra. Uzamsal dizinler değil duyarlılık değeri vardır ve her zaman varsayılan duyarlılık değeri kullanın.

> [!NOTE]
> Azure Cosmos DB noktaları, çokgenler ve MultiPoint otomatik dizin oluşturma destekler
> 
> 

Merhaba aşağıdaki JSON parçacığı bir dizin oluşturma ilkesi etkin uzamsal dizin ile gösterir, yani uzamsal sorgulamak için belgeler içinde bulunan herhangi bir GeoJSON noktası dizini. Hello Azure Portal kullanarak ilke dizin hello değiştiriyorsanız hello İlkesi tooenable koleksiyonunuzu üzerinde dizin uzamsal dizin oluşturma işlemi için JSON aşağıdaki belirtebilirsiniz.

**Toplama dizin oluşturma ilkesi JSON noktaları ve çokgenler için etkin Spatial ile**

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "includedPaths":[
          {
             "path":"/*",
             "indexes":[
                {
                   "kind":"Range",
                   "dataType":"String",
                   "precision":-1
                },
                {
                   "kind":"Range",
                   "dataType":"Number",
                   "precision":-1
                },
                {
                   "kind":"Spatial",
                   "dataType":"Point"
                },
                {
                   "kind":"Spatial",
                   "dataType":"Polygon"
                }                
             ]
          }
       ],
       "excludedPaths":[
       ]
    }

Bir kod parçacığı aşağıda verilmiştir toocreate uzamsal dizin oluşturma ile bir koleksiyon nasıl noktaları içeren tüm yollar için açık gösterir .NET içinde. 

**Uzamsal dizin oluşturma ile bir koleksiyon oluşturma**

    DocumentCollection spatialData = new DocumentCollection()
    spatialData.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point)); //override tooturn spatial on by default
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), spatialData);

Burada da belgeler içinde depolanan noktaları üzerinden uzamsal dizin oluşturma Varolan koleksiyon tootake avantajı nasıl değiştirebilirsiniz.

**Var olan bir koleksiyon uzamsal dizin oluşturma ile değiştirme**

    Console.WriteLine("Updating collection with spatial indexing enabled in indexing policy...");
    collection.IndexingPolicy = new IndexingPolicy(new SpatialIndex(DataType.Point));
    await client.ReplaceDocumentCollectionAsync(collection);

    Console.WriteLine("Waiting for indexing toocomplete...");
    long indexTransformationProgress = 0;
    while (indexTransformationProgress < 100)
    {
        ResourceResponse<DocumentCollection> response = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));
        indexTransformationProgress = response.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromSeconds(1));
    }

> [!NOTE]
> Merhaba konumu GeoJSON değeri hello belge içinde hatalı biçimlendirilmiş veya geçersiz ise, ardından uzamsal sorgulamak için dizine değil. Konum değerleri ST_ISVALID ve ST_ISVALIDDETAILED kullanarak doğrulayabilirsiniz.
> 
> Koleksiyon tanımınızı bölüm anahtarı içeriyorsa, dönüşüm ilerleme dizin bildirilmedi. 
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
Learnt göre tooget Jeo-uzamsal desteği Azure Cosmos veritabanı ile çalışmaya nasıl hakkında şunları yapabilirsiniz:

* Merhaba ile kod yazmaya başlayın [Jeo-uzamsal .NET github'daki kod örnekleri](https://github.com/Azure/azure-documentdb-dotnet/blob/fcf23d134fc5019397dcf7ab97d8d6456cd94820/samples/code-samples/Geospatial/Program.cs)
* Hello Jeo-uzamsal sorgulama ile ele almak [Azure Cosmos DB Query Playground](http://www.documentdb.com/sql/demo#geospatial)
* Daha fazla bilgi edinmek [Azure Cosmos DB sorgusu](documentdb-sql-query.md)
* Daha fazla bilgi edinmek [Azure Cosmos DB dizin oluşturma ilkeleri](indexing-policies.md)

