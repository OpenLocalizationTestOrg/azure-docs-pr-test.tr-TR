---
title: "Ayrıca \"bir dizin (.NET API - Azure Search) sorgu | Microsoft Docs\""
description: "Azure Search'te bir arama sorgusu oluşturun ve arama parametrelerini toofilter ve sıralama arama sonuçlarını kullanın."
services: search
manager: jhubbard
documentationcenter: 
author: brjohnstmsft
ms.assetid: 12c3efba-ea99-4187-9d2d-f63b5ec7040d
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/19/2017
ms.author: brjohnst
ms.openlocfilehash: 8b3ba1cd1270aad038fb48d9053fcff35d243e13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="query-your-azure-search-index-using-hello-net-sdk"></a>Merhaba .NET SDK kullanarak Azure Search dizininizi sorgulama
> [!div class="op_single_selector"]
> * [Genel Bakış](search-query-overview.md)
> * [Portal](search-explorer.md)
> * [.NET](search-query-dotnet.md)
> * [REST](search-query-rest-api.md)
> 
> 

Bu makale tooquery kullanarak bir dizinin nasıl hello gösterir [Azure Search .NET SDK'sı](https://aka.ms/search-sdk).

Bu kılavuzda başlamadan önce, [Azure Search dizini oluşturmuş](search-what-is-an-index.md) ve [bunu verilerle doldurmuş](search-what-is-data-import.md) olmanız gerekir.

> [!NOTE]
> Bu makaledeki örnek kodun tamamı C# dilinde yazılmıştır. Merhaba tam kaynak kodu bulabilirsiniz [github'da](http://aka.ms/search-dotnet-howto). Merhaba hakkında bilgi edinebilirsiniz [Azure Search .NET SDK'sı](search-howto-dotnet-sdk.md) daha ayrıntılı ilerlemesi hello örnek kod için.

## <a name="identify-your-azure-search-services-query-api-key"></a>Azure Search hizmet sorgunuzun api anahtarını tanımlama
Azure Search dizini oluşturduğunuza göre hello .NET SDK kullanarak neredeyse hazır tooissue sorguları demektir. Öncelikle, sağladığınız hello arama hizmeti için tooobtain hello sorgu API oluşturulmasının anahtarlarından biri gerekir. Merhaba .NET SDK'sı her isteği tooyour hizmette bu api anahtarını gönderir. Geçerli bir anahtar sahip istek başına temelinde, hello isteği gönderiliyor hello uygulama ve bunu işleyen hello hizmeti arasında güven oluşturur.

1. toofind hizmetinizin api toohello oturum açabilir anahtarlarından [Azure portalı](https://portal.azure.com/)
2. Tooyour Azure Search hizmet dikey penceresine gidin
3. Merhaba üzerinde "Anahtarlar" simgesine tıklayın

Hizmetiniz, *yönetici anahtarlarına* ve *sorgu anahtarlarına* sahiptir.

* Birincil ve ikincil *yönetici anahtarları* tooall operations hello özelliği toomanage hello hizmeti dahil olmak üzere, tam haklar, oluşturun ve dizinler, dizin oluşturucular ve veri kaynaklarını silin. Tooregenerate hello birincil anahtar ve tam tersini karar verirseniz toouse hello ikincil anahtar devam edebilmesi için bu iki anahtar vardır.
* *Sorgu anahtarları* salt okunur erişim tooindexes ve belgeleri verin ve arama istekleri gönderen genellikle dağıtılmış tooclient uygulamalardır.

Bir dizini sorgulama hello amacıyla, sorgu anahtarlarınızdan birini kullanabilirsiniz. Yönetici anahtarlarınız da sorgular için kullanılabilir, ancak bu daha iyi hello aşağıdaki gibi uygulama kodunuzda bir sorgu anahtarı kullanmanız gerekir [en az ayrıcalık prensibi](https://en.wikipedia.org/wiki/Principle_of_least_privilege).

## <a name="create-an-instance-of-hello-searchindexclient-class"></a>Merhaba Searchındexclient sınıfının bir örneğini oluşturun
tooissue sorguları'hello Azure Search .NET SDK'sı ile toocreate hello örneği gerekir `SearchIndexClient` sınıfı. Bu sınıfın birkaç oluşturucusu vardır. Arama hizmeti adınızı, dizin adı Hello istediğinizi alır ve bir `SearchCredentials` nesnesini parametre olarak. `SearchCredentials`, api anahtarınızı sarmalar.

Aşağıdaki Hello kodu oluşturur Yeni bir `SearchIndexClient` hello "hotels" dizini için (oluşturulan [hello .NET SDK kullanarak Azure Search dizini oluşturma](search-create-index-dotnet.md)) hello arama hizmeti adı ve hello uygulamanın yapılandırma dosyasında depolanan api anahtarı için değerleri kullanarak dosya (`appsettings.json` hello hello durumda [örnek uygulama](http://aka.ms/search-dotnet-howto)):

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

`SearchIndexClient`, `Documents` özelliğine sahiptir. Bu özellik, tüm hello tooquery Azure Search dizinlerini gereken yöntemleri sağlar.

## <a name="query-your-index"></a>Dizininizi sorgulama
Merhaba .NET SDK ile arama arama hello basit `Documents.Search` yöntemi, `SearchIndexClient`. Bu yöntem ile birlikte hello arama metni dahil olmak üzere birkaç parametre alır bir `SearchParameters` kullanılan toofurther İyileştir hello sorgu olabilir nesnesi.

#### <a name="types-of-queries"></a>Sorgu Türleri
Merhaba iki ana [sorgu türü](search-query-overview.md#types-of-queries) kullanacağınız olan `search` ve `filter`. `search` sorgusu, dizininizdeki tüm *aranabilir* alanlarda bir veya daha çok terimi arar. `filter` sorgusu, bir dizindeki tüm *filtrelenebilir* alanlarda bir boole ifadesini değerlendirir.

Arama ve filtrelerin hello kullanılarak gerçekleştirilir `Documents.Search` yöntemi. Bir arama sorgusu hello geçirilebilir `searchText` bir filtre ifadesi hello geçirilebilirken parametresi `Filter` hello özelliğinin `SearchParameters` sınıfı. Arama, olmadan toofilter geçirmeniz yeterlidir `"*"` hello için `searchText` parametresi. filtreleme, olmadan toosearch yalnızca hello bırakın `Filter` özelliği ayarlanmadan veya içinde geçmeyin bir `SearchParameters` örneği.

#### <a name="example-queries"></a>Örnek Sorgular
Aşağıdaki örnek kod hello gösterir birkaç farklı şekilde "dizin tanımlı tooquery hello hotels" [hello .NET SDK kullanarak Azure Search dizini oluşturma](search-create-index-dotnet.md#DefineIndex). Merhaba Arama sonuçlarıyla döndürülen hello belgeleri hello örnekleri olduğuna dikkat edin `Hotel` tanımlanan sınıfı [Veri Al'ı kullanarak Azure Search .NET SDK'sı hello](search-import-data-dotnet.md#HotelClass). Merhaba örnek kod kullanır bir `WriteDocuments` yöntemi toooutput hello arama sonuçları toohello konsol. Bu yöntem hello sonraki bölümde açıklanmıştır.

```csharp
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
```

## <a name="handle-search-results"></a>Arama sonuçlarını işleme
Merhaba `Documents.Search` yöntemi döndürür bir `DocumentSearchResult` hello hello sorgunun sonuçlarını içeren nesne. Merhaba önceki bölümde Hello örnekte kullanılan adlı bir yöntem `WriteDocuments` toooutput hello arama sonuçları toohello konsolu:

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

İşte hello önceki bölümdeki hello sorgularında olduğunu varsayarak hello "hotels" dizininin hello örnek verilerle doldurulur gibi ne hello sonuçlar görünür [Veri Al'ı kullanarak Azure Search .NET SDK'sı hello](search-import-data-dotnet.md):

```
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
```

Yukarıdaki örnek kod Hello hello konsol toooutput arama sonuçları kullanır. Bu gibi durumlarda, toodisplay arama sonuçlarında benzer şekilde, kendi uygulamanızda gerekir. Bkz: [github'daki bu örneğe](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) nasıl bir ASP.NET MVC tabanlı web uygulamasında toorender arama sonuçları bir örnek için.

