---
title: "aaaHow toouse bir .NET uygulamasından Azure Search | Microsoft Docs"
description: "Bir .NET uygulamasından Azure toouse arama nasıl"
services: search
documentationcenter: 
author: brjohnstmsft
manager: jlembicz
editor: 
ms.assetid: 93653341-c05f-4cfd-be45-bb877f964fcb
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/22/2017
ms.author: brjohnst
ms.openlocfilehash: 8e13fbe5549547d65941b856ce5a90611261388f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-search-from-a-net-application"></a>Bir .NET uygulamasından Azure toouse arama nasıl
Bu makalede bir gözden geçirme tooget olduğundan, hello ile çalışır [Azure Search .NET SDK'sı](https://aka.ms/search-sdk). Bir zengin hello .NET SDK'sı tooimplement kullanabileceğiniz Azure arama'yı kullanarak, uygulamanızda arama deneyimini.

## <a name="whats-in-hello-azure-search-sdk"></a>Azure Search SDK hello nedir
Merhaba SDK oluşan bir istemci Kitaplığı'nın `Microsoft.Azure.Search`. Bu, toomanage dizinleri, veri kaynakları ve dizin oluşturucular, sağlar yanı sıra karşıya yükleme ve belgeleri yönetmek ve tüm HTTP ve JSON hello ayrıntılarla toodeal kalmadan sorgular yürütün.

Merhaba istemci kitaplığı gibi sınıflara tanımlar `Index`, `Field`, ve `Document`, yanı sıra operations ister `Indexes.Create` ve `Documents.Search` hello üzerinde `SearchServiceClient` ve `SearchIndexClient` sınıfları. Bu sınıfların ad alanları aşağıdaki hello düzenlenmiştir:

* [Microsoft.Azure.Search](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)
* [Microsoft.Azure.Search.Models](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models)

Merhaba geçerli sürümü hello Azure Search .NET SDK'sı, genellikle kullanıma sunulmuştur. Tooprovide geri bildirim isterseniz bize tooincorporate hello sonraki sürümünde, lütfen şu adresi ziyaret bizim [görüş sayfası](https://feedback.azure.com/forums/263029-azure-search/).

Merhaba .NET SDK sürüm destekleyen `2016-09-01` Merhaba, [Azure Search REST API'sini](https://docs.microsoft.com/rest/api/searchservice/). Bu sürümü artık özel Çözümleyicileri ve Azure Blob ve Azure Table dizin oluşturucu desteği içerir. Önizleme özellikleri *değil* JSON ve CSV dosyalarını dizin oluşturma için destek gibi bu sürümü bir parçası olan [Önizleme](search-api-2015-02-28-preview.md) ve hello eski aracılığıyla kullanılabilen [hello .NET SDK 2.0-Önizleme sürümü ](https://aka.ms/search-sdk-preview).

Bu SDK desteklemediği [yönetim işlemlerini](https://docs.microsoft.com/rest/api/searchmanagement/) oluşturma ve arama hizmetleri ölçekleme ve API anahtarlarını yönetme gibi. .NET uygulaması arama kaynaklarınızdan toomanage gerekirse hello kullanabilirsiniz [Azure Search .NET Yönetim SDK](https://aka.ms/search-mgmt-sdk).

## <a name="upgrading-toohello-latest-version-of-hello-sdk"></a>Merhaba SDK toohello en son sürümüne yükseltme
Hello Azure Search .NET SDK'sı daha eski bir sürümü zaten kullanıyorsanız ve tooupgrade toohello yeni genel olarak kullanılabilir sürüm, istediğiniz [bu makalede](search-dotnet-sdk-migration.md) açıklar nasıl.

## <a name="requirements-for-hello-sdk"></a>Merhaba SDK gereksinimleri
1. Visual Studio 2017.
2. Kendi Azure Search hizmeti. Sipariş toouse hello SDK, hizmetinize hello adını ve bir veya daha fazla API anahtarı gerekir. [Merhaba Portalı'nda bir hizmet oluşturma](search-create-service-portal.md) bu adımları uygularken size yardımcı olur.
3. Hello Azure Search .NET SDK'sını indirin [NuGet paketi](http://www.nuget.org/packages/Microsoft.Azure.Search) "NuGet paketlerini Yönet" Visual Studio kullanarak. Merhaba paket adı için yalnızca arama `Microsoft.Azure.Search` NuGet.org üzerinde.

Hello Azure Search .NET SDK'sı hello .NET Framework 4.6 ve .NET Core hedefleyen uygulamaları destekler.

## <a name="core-scenarios"></a>Temel senaryolar
Arama uygulamanızda toodo gerekir birkaç şey vardır. Bu öğreticide, bu temel senaryolar şu konulara değineceğiz:

* Dizin oluşturma
* Belgelerle Hello dizin doldurma
* Tam metin araması ve filtreleri kullanarak belgeleri için arama

Aşağıdaki örnek kod hello her birinde gösterilmektedir. Ücretsiz toouse hello kod parçacıkları, kendi uygulamanızda eşitleyerek.

### <a name="overview"></a>Genel Bakış
Merhaba biz keşfetme örnek uygulamayı yeni bir oluşturur "hotels" adlı dizin birkaç belgelerle doldurur sonra bazı arama sorguları yürütür. Gösteren hello ana program İşte hello genel akış:

```csharp
// This sample shows how toodelete, create, upload documents and query an index
static void Main(string[] args)
{
    IConfigurationBuilder builder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
    IConfigurationRoot configuration = builder.Build();

    SearchServiceClient serviceClient = CreateSearchServiceClient(configuration);

    Console.WriteLine("{0}", "Deleting index...\n");
    DeleteHotelsIndexIfExists(serviceClient);

    Console.WriteLine("{0}", "Creating index...\n");
    CreateHotelsIndex(serviceClient);

    ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

    Console.WriteLine("{0}", "Uploading documents...\n");
    UploadDocuments(indexClient);

    ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

    RunQueries(indexClientForQueries);

    Console.WriteLine("{0}", "Complete.  Press any key tooend application...\n");
    Console.ReadKey();
}
```

> [!NOTE]
> Merhaba örnek uygulaması bu ilerlemesi üzerinde kullanılan hello tam kaynak kodunu bulabilirsiniz [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).
> 
>

Biz bu adım adım adım geçireceğiz. Yeni bir toocreate ilk ihtiyacımız `SearchServiceClient`. Bu nesne toomanage dizinleri sağlar. Sipariş tooconstruct içinde biri, bir yönetici API anahtarı yanı sıra Azure Search hizmet adınızı tooprovide gerekir. Bu bilgiler hello girebilirsiniz `appsettings.json` hello dosyasının [örnek uygulama](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).

```csharp
private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string adminApiKey = configuration["SearchServiceAdminApiKey"];

    SearchServiceClient serviceClient = new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
    return serviceClient;
}
```

> [!NOTE]
> Yanlış bir anahtar (burada bir yönetici anahtarı gerekli Örneğin, bir sorgu anahtarı) sağlarsanız, hello `SearchServiceClient` özel durum oluşturacak bir `CloudException` hello hata iletisi "Yasak" Merhaba ile ilk kez, bir işlemi yöntemi üzerinde aşağıdaki gibi çağrısından `Indexes.Create`. Bu tooyou olursa, bizim API anahtarı denetleyin.
> 
> 

Merhaba sonraki birkaç satır yöntemleri toocreate "hotels" zaten varsa, ilk silme, adında bir dizini arayın. Biz bu yöntemlerle biraz daha sonra yol gösterir.

```csharp
Console.WriteLine("{0}", "Deleting index...\n");
DeleteHotelsIndexIfExists(serviceClient);

Console.WriteLine("{0}", "Creating index...\n");
CreateHotelsIndex(serviceClient);
```

Ardından, başlangıç dizini doldurulmuş toobe gerekir. toodo bunu ihtiyacımız bir `SearchIndexClient`. İki yolu tooobtain biri vardır: onu oluşturmak ya da çağırma `Indexes.GetClient` hello üzerinde `SearchServiceClient`. Merhaba ikinci kolaylık sağlamak için kullanırız.

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> Genel bir arama uygulamasında, dizin yönetimi ve popülasyon, arama sorgularından ayrı bir bileşen tarafından işlenir. `Indexes.GetClient`kaydettiğinden bir dizini doldurmada kullanışlıdır hello başka sağlama sorun `SearchCredentials`. Bunu Bu, kullanılan toocreate hello hello yönetici anahtarını geçirerek yapar `SearchServiceClient` toohello yeni `SearchIndexClient`. Ancak, uygulamanızın sorguları yürüten hello bölümünde daha iyi toocreate hello olmasından `SearchIndexClient` doğrudan böylece bir yönetici anahtarı yerine sorgu anahtarında geçirebilirsiniz. Bu en az ayrıcalık prensibi hello ile tutarlı ve uygulamanızı daha güvenli toomake yardımcı olur. Yönetici anahtarları ve sorgu anahtarları hakkında daha fazla bilgi için [burada](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).
> 
> 

Biz sahip olduğunuza göre bir `SearchIndexClient`, biz hello dizin doldurabilirsiniz. Bu size daha sonra size yol gösterir başka bir yöntem kullanarak gerçekleştirilir.

```csharp
Console.WriteLine("{0}", "Uploading documents...\n");
UploadDocuments(indexClient);
```

Son olarak, biz birkaç arama sorguları yürütmek ve hello sonuçları görüntüleyin. Bu süre kullanırız farklı bir `SearchIndexClient`:

```csharp
ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

RunQueries(indexClientForQueries);
```

Biz hello yakından sürer `RunQueries` daha sonra yöntemi. Yeni hello kod toocreate hello işte `SearchIndexClient`:

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

Bu süre yazma erişimi toohello dizin gerekmez bu yana bir sorgu anahtarı kullanırız. Bu bilgiler hello girebilirsiniz `appsettings.json` hello dosyasının [örnek uygulama](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).

Bu uygulamayı geçerli bir hizmet adı ve API anahtarlarını çalıştırırsanız hello çıktı aşağıdaki gibi görünmelidir:

    Deleting index...
    
    Creating index...
    
    Uploading documents...
    
    Waiting for documents toobe indexed...
    
    Search hello entire index for hello term 'budget' and return only hello hotelName field:
    
    Name: Roach Motel
    
    Apply a filter toohello index toofind hotels cheaper than $150 per night, and return hello hotelId and description:
    
    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close tootown hall and hello river
    
    Search hello entire index, order by a specific field (lastRenovationDate) in descending order, take hello top two results, and show only hotelName and lastRenovationDate:
    
    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00
    
    Search hello entire index for hello term 'motel':
    
    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577
    
    Complete.  Press any key tooend application...

Merhaba uygulaması Hello tam kaynak kodunu hello bu makalenin sonundaki sağlanır.

Ardından, biz tarafından çağrılır hello yöntemlerin her biri daha ayrıntılı bir bakış sürer `Main`.

### <a name="creating-an-index"></a>Dizin oluşturma
Oluşturduktan sonra bir `SearchServiceClient`, hello sonraki şey `Main` mu zaten delete hello "hotels" dizininin ise. Bu yöntemi aşağıdaki hello tarafından gerçekleştirilir:

```csharp
private static void DeleteHotelsIndexIfExists(SearchServiceClient serviceClient)
{
    if (serviceClient.Indexes.Exists("hotels"))
    {
        serviceClient.Indexes.Delete("hotels");
    }
}
```

Bu yöntem verilen hello kullanır `SearchServiceClient` toocheck hello dizin varsa ve bu durumda, silin.

> [!NOTE]
> Bu makaledeki örnek kod Hello hello Azure Search .NET SDK'sı zaman uyumlu yöntemleri hello kolaylık sağlamak için kullanır. Kendi uygulamaları tookeep hello zaman uyumsuz yöntemleri kullanmanızı öneririz bunları ölçeklenebilir ve esnek. Örneğin, yukarıdaki yöntemi hello kullanabilirsiniz `ExistsAsync` ve `DeleteAsync` yerine `Exists` ve `Delete`.
> 
> 

Ardından, `Main` bu yöntemini çağırarak yeni bir "hotels" dizini oluşturur:

```csharp
private static void CreateHotelsIndex(SearchServiceClient serviceClient)
{
    var definition = new Index()
    {
        Name = "hotels",
        Fields = FieldBuilder.BuildForType<Hotel>()
    };

    serviceClient.Indexes.Create(definition);
}
```

Bu yöntem yeni bir oluşturur `Index` listesini nesnesiyle `Field` hello yeni dizin hello şemasını tanımlayan nesneleri. Her alanın bir adı, veri türü ve arama davranışını tanımlamak birkaç öznitelik vardır. Merhaba `FieldBuilder` sınıfını kullanır yansıma toocreate listesini `Field` nesneleri inceleniyor tarafından hello dizin için genel özellikleri ve verilen hello özniteliklerini hello `Hotel` model sınıfı. Biz hello yakından gitmek `Hotel` daha sonra sınıfı.

> [!NOTE]
> Merhaba listesini her zaman oluşturabilirsiniz `Field` kullanmak yerine doğrudan nesneleri `FieldBuilder` gerekiyorsa. Örneğin, bir model sınıfı toouse istemeyebilirsiniz veya toouse toomodify öznitelikleri ekleyerek istemediğiniz varolan bir model sınıfı gerekebilir.
>
> 

Ayrıca toofields, ayrıca Puanlama profilleri, ilgili veya CORS seçenekleri toohello (bunlar kısaltma hello örnekten göz ardı edilir) dizini ekleyebilirsiniz. Hello hello dizin nesnesi ve onun bağlı bölümleri hakkında daha fazla bilgi bulabilirsiniz [SDK başvurusu](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), hello gibi yanı [Azure Search REST API Başvurusu](https://docs.microsoft.com/rest/api/searchservice/).

### <a name="populating-hello-index"></a>Merhaba dizin doldurma
Merhaba sonraki adımda `Main` toopopulate hello yeni oluşturulan dizinidir. Bu yöntemi aşağıdaki hello gerçekleştirilir:

```csharp
private static void UploadDocuments(ISearchIndexClient indexClient)
{
    var hotels = new Hotel[]
    {
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
        },
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
        },
        new Hotel() 
        { 
            HotelId = "3", 
            BaseRate = 129.99,
            Description = "Close tootown hall and hello river"
        }
    };

    var batch = IndexBatch.Upload(hotels);

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
}
```

Bu yöntem, dört bölümden oluşur. Merhaba ilk olarak bir dizi oluşturur `Hotel` giriş verisi tooupload toohello dizinimizi hizmet verecektir nesneleri. Bu veriler, kolaylık sağlamak için sabit kodlanmış ' dir. Kendi uygulamanızda verilerinizi büyük olasılıkla bir SQL veritabanı gibi bir dış veri kaynağından gelecektir.

Merhaba ikinci bölümü oluşturur bir `IndexBatch` hello belgeleri içeren. Oluşturduğunuz, bu durumda çağırarak hello zamanında tooapply toohello toplu istediğiniz hello işlemi belirttiğiniz `IndexBatch.Upload`. Karşıya yüklenen toohello Azure Search dizini tarafından hello hello toplu olduğundan `Documents.Index` yöntemi.

> [!NOTE]
> Bu örnekte, biz yalnızca belgeleri karşıya yükleniyor. Toomerge değişiklikler mevcut belgeleri veya delete belgeleri istediyseniz, çağırarak toplu işlemler oluşturabilirsiniz `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, veya `IndexBatch.Delete` yerine. Çağırarak farklı işlemlerini tek bir toplu işte karıştırabilirsiniz `IndexBatch.New`, bir koleksiyonunu alır `IndexAction` nesneleri, bir belge üzerinde belirli bir işlemi her biri söyler Azure Search tooperform. Her oluşturabilirsiniz `IndexAction` gibi hello karşılık gelen yöntemini çağırarak kendi işlemi ile `IndexAction.Merge`, `IndexAction.Upload`ve benzeri.
> 
> 

Merhaba üçüncü bu yöntem dizin oluşturma için önemli bir hata durumunu işler bir catch bloğunun parçasıdır. Azure Search hizmetinizin hello bazıları belgeleri hello toplu işlemde tooindex başarısız olursa bir `IndexBatchException` tarafından oluşturulan `Documents.Index`. Bu durum, hizmetiniz ağır yük altındayken belgelere dizin oluşturuyorsanız oluşabilir. **Bu durumu, kodunuzda açık şekilde işlemenizi kesinlikle öneririz.** Gecikme ve başarısız olan dizin hello belge yeniden deneyin veya oturum ve hello örnek vermez veya uygulamanızın veri tutarlılığı gereksinimlerine bağlı olarak başka bir şey yapabilirsiniz gibi devam edebilirsiniz.

> [!NOTE]
> Merhaba kullanabilirsiniz `FindFailedActionsToRetry` içeren yeni bir toplu yöntemi tooconstruct yalnızca önceki çağrıda çok başarısız Eylemler hello`Index`. Merhaba yöntemi belgelenmiştir [burada](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) ve nasıl tooproperly kullanır, tartışma [StackOverflow üzerinde](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).
>
>

Son olarak, hello `UploadDocuments` yöntemi gecikmeler iki saniye. Merhaba örnek uygulaması toowait hello belgelerin aramada kullanılabilir kısa bir süre tooensure gerekir böylece dizin oluşturma Azure Search hizmetinizin zaman uyumsuz olarak gerçekleşir. Bu gibi gecikmeler genellikle yalnızca gösterilerde, testlerde ve örnek uygulamalarda gereklidir.

#### <a name="how-hello-net-sdk-handles-documents"></a>Merhaba .NET SDK belgeleri nasıl işler?
Size nasıl hello Azure Search .NET SDK'sı gibi kullanıcı tanımlı bir sınıf örneklerini mümkün tooupload merak ediyor olabilirsiniz `Hotel` toohello dizini. toohelp bu sorunun yanıtlanmasına, hello bakalım `Hotel` sınıfı:

```csharp
using System;
using Microsoft.Azure.Search;
using Microsoft.Azure.Search.Models;
using Microsoft.Spatial;
using Newtonsoft.Json;

// hello SerializePropertyNamesAsCamelCase attribute is defined in hello Azure Search .NET SDK.
// It ensures that Pascal-case property names in hello model class are mapped toocamel-case
// field names in hello index.
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [System.ComponentModel.DataAnnotations.Key]
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
}
```

Merhaba ilk şey toonotice her ortak özelliği olan `Hotel` tooa alan hello dizin tanımı, ancak çok önemli bir fark karşılık gelir: her alanı hello adını küçük harfle ("ortası büyük harf"), her ortak hello adını sırasında başlatır özelliği `Hotel` büyük harfle ("Pascal büyük") başlar. Bu, hello hedef şema hello uygulama geliştiricisi dış hello denetimin olduğu veri bağlamayı gerçekleştiren .NET uygulamalarında ortak bir senaryodur. Adlandırma yönergeleri özellik adlarını ortası büyük harf yaparak tooviolate hello .NET sahip olmak yerine hello SDK toomap hello özellik adları toocamel harf hello ile otomatik olarak anlayabilirsiniz `[SerializePropertyNamesAsCamelCase]` özniteliği.

> [!NOTE]
> Hello Azure Search .NET SDK'sını kullanır hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) kitaplığı tooserialize ve, özel model nesneleri tooand json'dan seri durumdan. Gerekirse bu seri hale getirmeyi özelleştirebilirsiniz. Daha fazla ayrıntı için bkz: [JSON.NET ile özel serileştirme](#JsonDotNet).
> 
> 

Merhaba ikinci şey toonotice olan hello öznitelikleri gibi `IsFilterable`, `IsSearchable`, `Key`, ve `Analyzer` her ortak özelliği tasarlamanız. Bu öznitelikler toohello doğrudan eşleme [hello Azure Search dizini karşılık gelen özniteliklerini](https://docs.microsoft.com/rest/api/searchservice/create-index#request). Merhaba `FieldBuilder` sınıfı hello dizini için bu tooconstruct alan tanımları kullanır.

Merhaba üçüncü önemli şey hello hakkında `Hotel` sınıfı hello genel özelliklerin hello veri türleri bulunur. Bu özelliklerin Hello .NET türleri tootheir hello dizin tanımında eşdeğer alan türleriyle eşlenir. Örneğin, hello `Category` dize özelliği eşlemeleri toohello `category` türü alan `Edm.String`. Arasında benzer türde eşlemeler bulunur `bool?` ve `Edm.Boolean`, `DateTimeOffset?` ve `Edm.DateTimeOffset`, vb. hello hello tür eşlemesi için belirli kurallar ile Merhaba belgelenmiştir `Documents.Get` hello yönteminde [Azure Search .NET SDK'sı başvuru](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_). Merhaba `FieldBuilder` sınıfı, bu eşlemeyi mvc'deki ancak serileştirme sorunları tootroubleshoot gerektiğinde yine yararlı toounderstand olabilir.

Bu özelliği toouse her iki yönde de kendi sınıflarınızı belge olarak çalışır; Ayrıca arama sonuçları almak ve sahip hello SDK otomatik olarak seri durumdan bunları tooa türü tercih ettiğiniz biz hello sonraki bölümde göreceğiniz gibi.

> [!NOTE]
> Hello Azure Search .NET SDK'sı hello kullanarak dinamik tür belirtilmiş belgeleri de destekler `Document` bir anahtar/değer eşlemesi alan adları toofield değerlerinin sınıfı. Bu tasarım zamanında hello dizin şemasını bilmediğiniz veya kullanışsız toobind toospecific modeli sınıfları olmayacağı senaryolarda kullanışlıdır. Merhaba SDK ilgili tüm hello yöntemler hello ile çalışan aşırı yüklerin `Document` sınıfı yanı sıra genel türde bir parametre alan kesin tür belirtilmiş aşırı. Yalnızca ikinci Merhaba, hello örnek kodda Bu öğreticide kullanılır. Merhaba `Document` sınıfının devraldığı `Dictionary<string, object>`. Diğer ayrıntıları bulmak [burada](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).
> 
> 

**Neden boş değer atanabilir türleri kullanmalısınız?**

Kendi model sınıfları toomap tooan Azure Search dizininizi tasarlarken gibi özellikleri değer türlerini bildirme öneririz `bool` ve `int` toobe boş değer atanabilir (örneğin, `bool?` yerine `bool`). Atanamayan bir özellik kullanırsanız, çok sahip**garanti** hiçbir belgeleri dizininize hello karşılık gelen alan için bir null değer içeriyor. Merhaba SDK ne hello Azure Search hizmeti, tooenforce bu yardımcı olur.

Bu yalnızca kuramsal bir sorun değildir: türü olan yeni bir alan tooan mevcut dizin eklediğiniz bir senaryoyu düşünün `Edm.Int32`. (Tüm türleri Azure Search'te boş değer atanabilir olmasıdır) hello dizin tanımını güncelleştirdikten sonra bu yeni alan için bir null değer tüm belgeler olacaktır. Ardından bir model sınıfı bir null ile kullanırsanız `int` özelliği bu alan için elde edersiniz bir `JsonSerializationException` şöyle tooretrieve belgeleri çalışırken:

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

Bu nedenle, en iyi uygulama olarak model sınıflarınızda boş değer atanabilir türler kullanmanızı öneririz.

<a name="JsonDotNet"></a>

#### <a name="custom-serialization-with-jsonnet"></a>JSON.NET ile özel seri hale getirme
Merhaba SDK JSON.NET seri hale getirme ve belgeleri seri durumdan çıkarmak için kullanır. Seri hale getirme özelleştirebilir ve tanımlayarak, kendi gerekirse seri durumundan çıkarma `JsonConverter` veya `IContractResolver` (Merhaba bkz [JSON.NET belgelerine](http://www.newtonsoft.com/json/help/html/Introduction.htm) daha fazla ayrıntı için). Azure Search ve diğer daha Gelişmiş senaryolar ile kullanılmak üzere uygulamanızdan tooadapt varolan bir model sınıfı istediğinizde bu yararlı olabilir. Örneğin, özel serileştirme ile şunları yapabilirsiniz:

* İçerebilir veya belge alanlar olarak depolanan belirli özellikleri modeli sınıfınızın dışlayabilirsiniz.
* Kodunuzda özellik adları ve alan adları, dizininizdeki arasında eşleyin.
* Özellikler toodocument alanlarını eşleme için kullanılan özel öznitelikler oluşturun.

Merhaba birim testlerinde hello Azure Search .NET SDK github'da için özel serileştirme uygulamanın örnekleri bulabilirsiniz. İyi bir başlangıç noktasıdır [bu klasör](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models). Merhaba özel serileştirme testleri tarafından kullanılan sınıfları içerir.

### <a name="searching-for-documents-in-hello-index"></a>Merhaba dizin belgelerde arama
Merhaba son Merhaba örnek uygulaması hello dizin bazı belgelerde toosearch adımdır. yöntemini aşağıdaki hello bunu yapar:

```csharp
private static void RunQueries(ISearchIndexClient indexClient)
{
    SearchParameters parameters;
    DocumentSearchResult<Hotel> results;

    Console.WriteLine("Search hello entire index for hello term 'budget' and return only hello hotelName field:\n");

    parameters =
        new SearchParameters()
        {
            Select = new[] { "hotelName" }
        };

    results = indexClient.Documents.Search<Hotel>("budget", parameters);

    WriteDocuments(results);

    Console.Write("Apply a filter toohello index toofind hotels cheaper than $150 per night, ");
    Console.WriteLine("and return hello hotelId and description:\n");

    parameters =
        new SearchParameters()
        {
            Filter = "baseRate lt 150",
            Select = new[] { "hotelId", "description" }
        };

    results = indexClient.Documents.Search<Hotel>("*", parameters);

    WriteDocuments(results);

    Console.Write("Search hello entire index, order by a specific field (lastRenovationDate) ");
    Console.Write("in descending order, take hello top two results, and show only hotelName and ");
    Console.WriteLine("lastRenovationDate:\n");

    parameters =
        new SearchParameters()
        {
            OrderBy = new[] { "lastRenovationDate desc" },
            Select = new[] { "hotelName", "lastRenovationDate" },
            Top = 2
        };

    results = indexClient.Documents.Search<Hotel>("*", parameters);

    WriteDocuments(results);

    Console.WriteLine("Search hello entire index for hello term 'motel':\n");

    parameters = new SearchParameters();
    results = indexClient.Documents.Search<Hotel>("motel", parameters);

    WriteDocuments(results);
}
```

Her bir sorgu yürütülmeden, bu yöntem önce yeni bir oluşturur `SearchParameters` nesnesi. Sıralama, filtreleme, disk belleği ve olduğunu gibi hello sorgu için kullanılan toospecify ek seçenekler budur. Bu yöntemde, biz hello ayarladığınız `Filter`, `Select`, `OrderBy`, ve `Top` özelliği için farklı sorgular. Tüm hello `SearchParameters` özellikleri belgelenmiştir [burada](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).

Merhaba sonraki adımdır tooactually hello arama sorgu yürütün. Bu yapılır hello kullanarak `Documents.Search` yöntemi. Her sorgu için biz hello arama metni toouse bir dize olarak geçirin (veya `"*"` arama metni ise), artı daha önce oluşturduğunuz parametreleri arama hello. Biz de belirtmeniz `Hotel` hello türü parametre olarak `Documents.Search`, söyleyen hello SDK toodeserialize belgeleri hello arama sonuçlarında türündeki nesneleri `Hotel`.

> [!NOTE]
> Merhaba arama sorgu ifade sözdizimi hakkında daha fazla bilgi bulabilirsiniz [burada](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).
> 
> 

Son olarak, her sorgu sonra bu yöntem her bir belge toohello konsol yazdırma tüm hello eşleşmeleri hello arama sonuçlarında yinelenir:

```csharp
private static void WriteDocuments(DocumentSearchResult<Hotel> searchResults)
{
    foreach (SearchResult<Hotel> result in searchResults.Results)
    {
        Console.WriteLine(result.Document);
    }

    Console.WriteLine();
}
```

Buna karşılık her hello sorguları daha yakın bir göz atalım. Merhaba kod tooexecute hello ilk sorgu şöyledir:

```csharp
parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);
```

Bu durumda, "Bütçe" Merhaba word eşleşen Oteller için arama yapıyorsanız ve tooget geri yalnızca hello otel adları, hello tarafından belirtilen istiyoruz `Select` parametresi. Merhaba sonuçları şunlardır:

    Name: Roach Motel

Ardından, biz toofind hello Oteller değerinden 150 ABD dolarını gecelik oranı ile istediğiniz ve yalnızca hello otel kimliği ve açıklama döndürür:

```csharp
parameters =
    new SearchParameters()
    {
        Filter = "baseRate lt 150",
        Select = new[] { "hotelId", "description" }
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);
```

Bu sorgu bir OData kullanan `$filter` ifadesi, `baseRate lt 150`, hello dizindeki toofilter hello belgeler. Hello Azure Search destekleyen OData sözdizimi hakkında daha fazla bilgi için [burada](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).

Merhaba hello sorgunun sonuçlarını şunlardır:

    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close tootown hall and hello river

Ardından, en son renovated ve hello otel adını ve son Yenileme tarihi toofind hello üst iki Oteller istiyoruz. Merhaba kod aşağıdadır: 

```csharp
parameters =
    new SearchParameters()
    {
        OrderBy = new[] { "lastRenovationDate desc" },
        Select = new[] { "hotelName", "lastRenovationDate" },
        Top = 2
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);
```

OData sözdizimi toospecify hello yeniden bu durumda, kullandığımız `OrderBy` parametre olarak `lastRenovationDate desc`. Ayrıca `Top` too2 tooensure biz yalnızca get hello üstteki iki belgeleri. Önce ayarlar gibi `Select` hangi alanların döndürülmesi toospecify.

Merhaba sonuçları şunlardır:

    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

Son olarak, toofind hello word "motel" eşleşen tüm Oteller istiyoruz:

```csharp
parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

Ve hello belirtmedi olduğundan, tüm alanları içeren hello sonuçları işte `Select` özelliği:

    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577

Başlangıç Öğreticisi Bu adım tamamlandıktan, ancak burada Durdur yok. **Sonraki adımlar** Azure Search hakkında daha fazla bilgi için ek kaynaklar sağlanmıştır.

## <a name="next-steps"></a>Sonraki adımlar
* Hello için Hello başvuruları Gözat [.NET SDK'sı](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) ve [REST API](https://docs.microsoft.com/rest/api/searchservice/).
* Bilginiz aracılığıyla deepen [videolar ve diğer örnekler ve öğreticiler](search-video-demo-tutorial-list.md).
* Gözden geçirme [adlandırma kuralları](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) çeşitli nesneleri adlandırma toolearn hello kuralları.
* Gözden geçirme [desteklenen veri türleri](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) Azure Search'te.
