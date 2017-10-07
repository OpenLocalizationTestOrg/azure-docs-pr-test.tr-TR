---
title: "aaa \"verileri (.NET - Azure Search) yükleme | Microsoft Docs\""
description: ".NET SDK kullanarak Azure Search tooupload veri tooan dizini hello nasıl öğrenin."
services: search
documentationcenter: 
author: brjohnstmsft
manager: jhubbard
editor: 
tags: 
ms.assetid: 0e0e7e7b-7178-4c26-95c6-2fd1e8015aca
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 01/13/2017
ms.author: brjohnst
ms.openlocfilehash: 78ddbefb522884d1f61cb275c25c091487aee639
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-tooazure-search-using-hello-net-sdk"></a>Karşıya veri tooAzure arama'yı kullanarak hello .NET SDK'sı
> [!div class="op_single_selector"]
> * [Genel Bakış](search-what-is-data-import.md)
> * [.NET](search-import-data-dotnet.md)
> * [REST](search-import-data-rest-api.md)
> 
> 

Bu makale size nasıl gösterir toouse hello [Azure Search .NET SDK'sı](https://aka.ms/search-sdk) tooimport verileri Azure Search dizini.

Bu kılavuza başlamadan önce bir [Azure Search dizini oluşturmuş](search-what-is-an-index.md) olmanız gerekir. Bu makalede, ayrıca, zaten oluşturduğunuzu varsayar bir `SearchServiceClient` gösterildiği gibi nesne [hello .NET SDK kullanarak Azure Search dizini oluşturma](search-create-index-dotnet.md#CreateSearchServiceClient).

> [!NOTE]
> Bu makaledeki örnek kodun tamamı C# dilinde yazılmıştır. Merhaba tam kaynak kodu bulabilirsiniz [github'da](http://aka.ms/search-dotnet-howto). Merhaba hakkında bilgi edinebilirsiniz [Azure Search .NET SDK'sı](search-howto-dotnet-sdk.md) daha ayrıntılı ilerlemesi hello örnek kod için.

Sipariş toopush belgelerde hello .NET SDK kullanarak dizininizi içine yapmanız gerekir:

1. Oluşturma bir `SearchIndexClient` nesne tooconnect tooyour arama dizini.
2. Oluşturma bir `IndexBatch` hello belgeleri toobe içeren eklenen değiştirilmiş veya silinmiş.
3. Merhaba çağrısı `Documents.Index` yöntemi, `SearchIndexClient` toosend hello `IndexBatch` tooyour arama dizini.

## <a name="create-an-instance-of-hello-searchindexclient-class"></a>Merhaba Searchındexclient sınıfının bir örneğini oluşturun
Azure Search .NET SDK kullanarak dizini içine tooimport veri Merhaba, toocreate hello örneği gerekir `SearchIndexClient` sınıfı. Zaten varsa, bu örneği kendiniz ancak, daha kolay oluşturabileceğiniz bir `SearchServiceClient` örneği toocall kendi `Indexes.GetClient` yöntemi. Örneğin, işte nasıl elde edebilirsiniz bir `SearchIndexClient` hello dizini "hotels" adlı bir `SearchServiceClient` adlı `serviceClient`:

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> Genel bir arama uygulamasında, dizin yönetimi ve popülasyon, arama sorgularından ayrı bir bileşen tarafından işlenir. `Indexes.GetClient`kaydettiğinden bir dizini doldurmada kullanışlıdır hello başka sağlama sorun `SearchCredentials`. Bunu Bu, kullanılan toocreate hello hello yönetici anahtarını geçirerek yapar `SearchServiceClient` toohello yeni `SearchIndexClient`. Ancak, uygulamanızın sorguları yürüten hello bölümünde daha iyi toocreate hello olmasından `SearchIndexClient` doğrudan böylece bir yönetici anahtarı yerine sorgu anahtarında geçirebilirsiniz. Bu hello ile tutarlıdır [en az ayrıcalık prensibi](https://en.wikipedia.org/wiki/Principle_of_least_privilege) ve uygulamanızı daha güvenli toomake yardımcı olur. Yönetici anahtarları ve hello sorgu anahtarları hakkında daha fazla bilgi için [Azure Search REST API Başvurusu](https://docs.microsoft.com/rest/api/searchservice/).
> 
> 

`SearchIndexClient`, `Documents` özelliğine sahiptir. Bu özellik tooadd, gereken tüm hello yöntemleri değiştirmek, silmek veya belgeleri dizininize sorgu sağlar.

## <a name="decide-which-indexing-action-toouse"></a>Hangi dizin oluşturma eylemini toouse karar verin
Merhaba .NET SDK kullanarak tooimport veri verilerinizi toopackage ihtiyacınız olacak bir `IndexBatch` nesnesi. Bir `IndexBatch` koleksiyonunu yalıtır `IndexAction` nesneleri, her biri içeren bir belge ve hangi eylemini tooperform belge (karşıya yükleme, birleştirme, silme, vb.) Azure Search söyleyen bir özellik. Seçtiğiniz Eylemler aşağıda hello bağlı olarak, yalnızca belirli alanlar her belge için dahil edilmelidir:

| Eylem | Açıklama | Her bir belge için gerekli alanlar | Notlar |
| --- | --- | --- | --- |
| `Upload` |Bir `Upload` benzer tooan "upsert" nerede hello belgenin yeni olması durumunda ekleneceği ve olması mevcut durumunda güncelleştirileceği/değiştirileceği bir eylemdir. |anahtar ve toodefine istediğiniz diğer alanlar |Güncelleştirme/var olan bir belgeyi değiştirirken, hello istekte belirtilen olmayan herhangi bir alan kendi alan çok kümesini sahip`null`. Bu durum, hatta hello alan tooa null olmayan değer önceden ayarlandı oluşur. |
| `Merge` |Varolan bir belge ile Merhaba güncelleştirmeleri alanları belirtilmiş. Merhaba belge hello dizininde mevcut değilse hello birleştirme işlemi başarısız olur. |anahtar ve toodefine istediğiniz diğer alanlar |Birleştirmede belirttiğiniz herhangi bir alan varolan bir alana hello hello belgedeki yerini alır. Buna `DataType.Collection(DataType.String)` türünde alanlar dahildir. Örneğin, hello belge bir alanı varsa, `tags` değerle `["budget"]` ve değeriyle bir birleştirme yürütme `["economy", "pool"]` için `tags`, hello hello son değerini `tags` alan `["economy", "pool"]`. `["budget", "economy", "pool"]` olmayacaktır. |
| `MergeOrUpload` |Bu eylem gibi davranır `Merge` anahtar zaten verilen hello belgeyle hello dizinde varsa. Merhaba belge mevcut değilse gibi davranır `Upload` yeni bir belgeyle. |anahtar ve toodefine istediğiniz diğer alanlar |- |
| `Delete` |Merhaba belirtilen belge hello dizinden kaldırır. |yalnızca anahtar |Merhaba anahtar alanı yoksayılacak dışında belirttiğiniz tüm alanlar. Bir belgeden tek bir alanı tooremove istiyorsanız kullanın `Merge` yerine ve basit şekilde hello alan açık olarak ayarlanıp toonull. |

Hangi eylemini toouse ile istediğiniz belirtebilirsiniz hello çeşitli statik yöntemlerini hello `IndexBatch` ve `IndexAction` hello sonraki bölümde gösterildiği gibi sınıflar.

## <a name="construct-your-indexbatch"></a>IndexBatch'inizi oluşturma
Belgelerinizde hangi eylemleri tooperform bildiğinize göre hazır tooconstruct hello olan `IndexBatch`. gösterir aşağıdaki örnekte nasıl hello toocreate birkaç farklı eylemler ile bir toplu iş. Bizim örneğimizde adlı özel bir sınıf kullandığına dikkat edin `Hotel` hello "hotels" dizininin tooa belgede eşler.

```csharp
var actions =
    new IndexAction<Hotel>[]
    {
        IndexAction.Upload(
            new Hotel()
            {
                HotelId = "1",
                BaseRate = 199.0,
                Description = "Best hotel in town",
                DescriptionFr = "Meilleur hôtel en ville",
                HotelName = "Fancy Stay",
                Category = "Luxury",
                Tags = new[] { "pool", "view", "wifi", "concierge" },
                ParkingIncluded = false,
                SmokingAllowed = false,
                LastRenovationDate = new DateTimeOffset(2010, 6, 27, 0, 0, 0, TimeSpan.Zero),
                Rating = 5,
                Location = GeographyPoint.Create(47.678581, -122.131577)
            }),
        IndexAction.Upload(
            new Hotel()
            {
                HotelId = "2",
                BaseRate = 79.99,
                Description = "Cheapest hotel in town",
                DescriptionFr = "Hôtel le moins cher en ville",
                HotelName = "Roach Motel",
                Category = "Budget",
                Tags = new[] { "motel", "budget" },
                ParkingIncluded = true,
                SmokingAllowed = true,
                LastRenovationDate = new DateTimeOffset(1982, 4, 28, 0, 0, 0, TimeSpan.Zero),
                Rating = 1,
                Location = GeographyPoint.Create(49.678581, -122.131577)
            }),
        IndexAction.MergeOrUpload(
            new Hotel()
            {
                HotelId = "3",
                BaseRate = 129.99,
                Description = "Close tootown hall and hello river"
            }),
        IndexAction.Delete(new Hotel() { HotelId = "6" })
    };

var batch = IndexBatch.New(actions);
```

Bu durumda, kullanıyoruz `Upload`, `MergeOrUpload`, ve `Delete` üzerinde hello adlı hello yöntemler tarafından belirtildiği gibi arama eylemlerimiz olarak `IndexAction` sınıfı.

Bu "hotels" dizini örneğinin, birçok belgeyle önceden doldurulduğunu varsayın. Nasıl biz toospecify tüm hello olası belge alanlarını kullanırken sahip değildi Not `MergeOrUpload` ve yalnızca hello belge anahtarını belirttiğimize (`HotelId`) kullanırken `Delete`.

Ayrıca, yalnızca tek bir dizin oluşturma isteğine too1000 belgelerde yukarı dahil edebileceğinizi unutmayın.

> [!NOTE]
> Bu örnekte, farklı eylemler toodifferent belgelerini uyguladığımız. İsterseniz tooperform hello aynı eylemleri çağırmak yerine hello toplu işteki tüm belgeler arasında `IndexBatch.New`, kullanabileceğinizi diğer statik yöntemlerini hello `IndexBatch`. Örneğin; `IndexBatch.Merge`, `IndexBatch.MergeOrUpload` ve `IndexBatch.Delete` çağırarak toplu işlemler oluşturabilirsiniz. Bu yöntemler, `IndexAction` nesneleri yerine bir belge koleksiyonu (bu örnekte `Hotel` türünde nesneler) alır.
> 
> 

## <a name="import-data-toohello-index"></a>İçeri aktarma veri toohello dizini
Başlatılan bir sahip olduğunuza `IndexBatch` nesne gönderebilirsiniz, toohello dizin çağırarak `Documents.Index` üzerinde `SearchIndexClient` nesnesi. örnekte gösterildiği nasıl aşağıdaki hello toocall `Index`, yanı sıra bazı ek adımlar tooperform gerekir:

```csharp
try
{
    indexClient.Documents.Index(batch);
}
catch (IndexBatchException e)
{
    // Sometimes when your Search service is under load, indexing will fail for some of hello documents in
    // hello batch. Depending on your application, you can take compensating actions like delaying and
    // retrying. For this simple demo, we just log hello failed document keys and continue.
    Console.WriteLine(
        "Failed tooindex some of hello documents: {0}",
        String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
}

Console.WriteLine("Waiting for documents toobe indexed...\n");
Thread.Sleep(2000);
```

Not hello `try` / `catch` hello çağrısı toohello çevreleyen `Index` yöntemi. Merhaba catch bloğu, dizin oluşturma için önemli bir hata durumunu işler. Azure Search hizmetinizin hello bazıları belgeleri hello toplu işlemde tooindex başarısız olursa bir `IndexBatchException` tarafından oluşturulan `Documents.Index`. Bu durum, hizmetiniz ağır yük altındayken belgelere dizin oluşturuyorsanız oluşabilir. **Bu durumu, kodunuzda açık şekilde işlemenizi kesinlikle öneririz.** Gecikme ve başarısız olan dizin hello belge yeniden deneyin veya oturum ve hello örnek vermez veya uygulamanızın veri tutarlılığı gereksinimlerine bağlı olarak başka bir şey yapabilirsiniz gibi devam edebilirsiniz.

Son olarak, yukarıdaki hello örnekteki kod iki saniye hello. Merhaba örnek uygulaması toowait hello belgelerin aramada kullanılabilir kısa bir süre tooensure gerekir böylece dizin oluşturma Azure Search hizmetinizin zaman uyumsuz olarak gerçekleşir. Bu gibi gecikmeler genellikle yalnızca gösterilerde, testlerde ve örnek uygulamalarda gereklidir.

<a name="HotelClass"></a>

### <a name="how-hello-net-sdk-handles-documents"></a>Merhaba .NET SDK belgeleri nasıl işler?
Size nasıl hello Azure Search .NET SDK'sı gibi kullanıcı tanımlı bir sınıf örneklerini mümkün tooupload merak ediyor olabilirsiniz `Hotel` toohello dizini. toohelp bu sorunun yanıtlanmasına, hello bakalım `Hotel` tanımlanan toohello dizin şemasını eşlemeleri sınıfı [hello .NET SDK kullanarak Azure Search dizini oluşturma](search-create-index-dotnet.md#DefineIndex):

```csharp
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [Key]
    [IsFilterable]
    public string HotelId { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public double? BaseRate { get; set; }

    [IsSearchable]
    public string Description { get; set; }

    [IsSearchable]
    [Analyzer(AnalyzerName.AsString.FrLucene)]
    [JsonProperty("description_fr")]
    public string DescriptionFr { get; set; }

    [IsSearchable, IsFilterable, IsSortable]
    public string HotelName { get; set; }

    [IsSearchable, IsFilterable, IsSortable, IsFacetable]
    public string Category { get; set; }

    [IsSearchable, IsFilterable, IsFacetable]
    public string[] Tags { get; set; }

    [IsFilterable, IsFacetable]
    public bool? ParkingIncluded { get; set; }

    [IsFilterable, IsFacetable]
    public bool? SmokingAllowed { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public DateTimeOffset? LastRenovationDate { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public int? Rating { get; set; }

    [IsFilterable, IsSortable]
    public GeographyPoint Location { get; set; }

    // ToString() method omitted for brevity...
}
```

Merhaba ilk şey toonotice her ortak özelliği olan `Hotel` tooa alan hello dizin tanımı, ancak çok önemli bir fark karşılık gelir: her alanı hello adını küçük harfle ("ortası büyük harf"), her ortak hello adını sırasında başlatır özelliği `Hotel` büyük harfle ("Pascal büyük") başlar. Bu, hello hedef şema hello uygulama geliştiricisi dış hello denetimin olduğu veri bağlamayı gerçekleştiren .NET uygulamalarında ortak bir senaryodur. Adlandırma yönergeleri özellik adlarını ortası büyük harf yaparak tooviolate hello .NET sahip olmak yerine hello SDK toomap hello özellik adları toocamel harf hello ile otomatik olarak anlayabilirsiniz `[SerializePropertyNamesAsCamelCase]` özniteliği.

> [!NOTE]
> Hello Azure Search .NET SDK'sını kullanır hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) kitaplığı tooserialize ve, özel model nesneleri tooand json'dan seri durumdan. Gerekirse bu seri hale getirmeyi özelleştirebilirsiniz. Daha fazla bilgi için bkz. [JSON.NET ile Özel Serileştirme](search-howto-dotnet-sdk.md#JsonDotNet). Bunun bir örneği olan hello hello kullanımını `[JsonProperty]` hello öznitelikte `DescriptionFr` yukarıdaki hello örnek kod bir özellik.
> 
> 

Merhaba hakkında ikinci önemli şey Hello `Hotel` sınıfı hello genel özelliklerin hello veri türleri bulunur. Bu özelliklerin Hello .NET türleri tootheir hello dizin tanımında eşdeğer alan türleriyle eşlenir. Örneğin, hello `Category` dize özelliği eşlemeleri toohello `category` türü alan `DataType.String`. `bool?` ve `DataType.Boolean`, `DateTimeOffset?` ve `DataType.DateTimeOffset`, vb. arasında benzer türde eşlemeler bulunur. Merhaba hello tür eşlemesi için belirli kurallar ile Merhaba belgelenmiştir `Documents.Get` hello yönteminde [Azure Search .NET SDK'sı başvurusu](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).

Bu özelliği toouse her iki yönde de kendi sınıflarınızı belge olarak çalışır; Ayrıca arama sonuçları almak ve sahip hello SDK otomatik olarak seri durumdan bunları tooa türü tercih ettiğiniz hello gösterildiği gibi [sonraki makalede](search-query-dotnet.md).

> [!NOTE]
> Hello Azure Search .NET SDK'sı hello kullanarak dinamik tür belirtilmiş belgeleri de destekler `Document` bir anahtar/değer eşlemesi alan adları toofield değerlerinin sınıfı. Bu tasarım zamanında hello dizin şemasını bilmediğiniz veya kullanışsız toobind toospecific modeli sınıfları olmayacağı senaryolarda kullanışlıdır. Merhaba SDK ilgili tüm hello yöntemler hello ile çalışan aşırı yüklerin `Document` sınıfı yanı sıra genel türde bir parametre alan kesin tür belirtilmiş aşırı. Yalnızca ikinci Merhaba, bu makaledeki örnek kod hello kullanılır.
> 
> 

**Neden boş değer atanabilir türleri kullanmalısınız?**

Kendi model sınıfları toomap tooan Azure Search dizininizi tasarlarken gibi özellikleri değer türlerini bildirme öneririz `bool` ve `int` toobe boş değer atanabilir (örneğin, `bool?` yerine `bool`). Atanamayan bir özellik kullanırsanız, çok sahip**garanti** hiçbir belgeleri dizininize hello karşılık gelen alan için bir null değer içeriyor. Merhaba SDK ne hello Azure Search hizmeti, tooenforce bu yardımcı olur.

Bu yalnızca kuramsal bir sorun değildir: türü olan yeni bir alan tooan mevcut dizin eklediğiniz bir senaryoyu düşünün `DataType.Int32`. (Tüm türleri Azure Search'te boş değer atanabilir olmasıdır) hello dizin tanımını güncelleştirdikten sonra bu yeni alan için bir null değer tüm belgeler olacaktır. Ardından bir model sınıfı bir null ile kullanırsanız `int` özelliği bu alan için elde edersiniz bir `JsonSerializationException` şöyle tooretrieve belgeleri çalışırken:

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

Bu nedenle, en iyi uygulama olarak model sınıflarınızda boş değer atanabilir türler kullanmanızı öneririz.

## <a name="next-steps"></a>Sonraki adımlar
Azure Search dizininizi doldurduktan sonra belgeler için sorguları toosearch veren hazır toostart olacaktır. Ayrıntılı bilgi için bkz. [Azure Search Dizininizi Sorgulama](search-query-overview.md).

