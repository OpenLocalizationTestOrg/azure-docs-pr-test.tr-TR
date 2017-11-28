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
# <a name="query-your-azure-search-index-using-hello-net-sdk"></a><span data-ttu-id="f9888-103">Merhaba .NET SDK kullanarak Azure Search dizininizi sorgulama</span><span class="sxs-lookup"><span data-stu-id="f9888-103">Query your Azure Search index using hello .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f9888-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="f9888-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="f9888-105">Portal</span><span class="sxs-lookup"><span data-stu-id="f9888-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="f9888-106">.NET</span><span class="sxs-lookup"><span data-stu-id="f9888-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="f9888-107">REST</span><span class="sxs-lookup"><span data-stu-id="f9888-107">REST</span></span>](search-query-rest-api.md)
> 
> 

<span data-ttu-id="f9888-108">Bu makale tooquery kullanarak bir dizinin nasıl hello gösterir [Azure Search .NET SDK'sı](https://aka.ms/search-sdk).</span><span class="sxs-lookup"><span data-stu-id="f9888-108">This article will show you how tooquery an index using hello [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span>

<span data-ttu-id="f9888-109">Bu kılavuzda başlamadan önce, [Azure Search dizini oluşturmuş](search-what-is-an-index.md) ve [bunu verilerle doldurmuş](search-what-is-data-import.md) olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f9888-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f9888-110">Bu makaledeki örnek kodun tamamı C# dilinde yazılmıştır.</span><span class="sxs-lookup"><span data-stu-id="f9888-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="f9888-111">Merhaba tam kaynak kodu bulabilirsiniz [github'da](http://aka.ms/search-dotnet-howto).</span><span class="sxs-lookup"><span data-stu-id="f9888-111">You can find hello full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="f9888-112">Merhaba hakkında bilgi edinebilirsiniz [Azure Search .NET SDK'sı](search-howto-dotnet-sdk.md) daha ayrıntılı ilerlemesi hello örnek kod için.</span><span class="sxs-lookup"><span data-stu-id="f9888-112">You can also read about hello [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of hello sample code.</span></span>

## <a name="identify-your-azure-search-services-query-api-key"></a><span data-ttu-id="f9888-113">Azure Search hizmet sorgunuzun api anahtarını tanımlama</span><span class="sxs-lookup"><span data-stu-id="f9888-113">Identify your Azure Search service's query api-key</span></span>
<span data-ttu-id="f9888-114">Azure Search dizini oluşturduğunuza göre hello .NET SDK kullanarak neredeyse hazır tooissue sorguları demektir.</span><span class="sxs-lookup"><span data-stu-id="f9888-114">Now that you have created an Azure Search index, you are almost ready tooissue queries using hello .NET SDK.</span></span> <span data-ttu-id="f9888-115">Öncelikle, sağladığınız hello arama hizmeti için tooobtain hello sorgu API oluşturulmasının anahtarlarından biri gerekir.</span><span class="sxs-lookup"><span data-stu-id="f9888-115">First, you will need tooobtain one of hello query api-keys that was generated for hello search service you provisioned.</span></span> <span data-ttu-id="f9888-116">Merhaba .NET SDK'sı her isteği tooyour hizmette bu api anahtarını gönderir.</span><span class="sxs-lookup"><span data-stu-id="f9888-116">hello .NET SDK will send this api-key on every request tooyour service.</span></span> <span data-ttu-id="f9888-117">Geçerli bir anahtar sahip istek başına temelinde, hello isteği gönderiliyor hello uygulama ve bunu işleyen hello hizmeti arasında güven oluşturur.</span><span class="sxs-lookup"><span data-stu-id="f9888-117">Having a valid key establishes trust, on a per request basis, between hello application sending hello request and hello service that handles it.</span></span>

1. <span data-ttu-id="f9888-118">toofind hizmetinizin api toohello oturum açabilir anahtarlarından [Azure portalı](https://portal.azure.com/)</span><span class="sxs-lookup"><span data-stu-id="f9888-118">toofind your service's api-keys you can sign in toohello [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="f9888-119">Tooyour Azure Search hizmet dikey penceresine gidin</span><span class="sxs-lookup"><span data-stu-id="f9888-119">Go tooyour Azure Search service's blade</span></span>
3. <span data-ttu-id="f9888-120">Merhaba üzerinde "Anahtarlar" simgesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="f9888-120">Click on hello "Keys" icon</span></span>

<span data-ttu-id="f9888-121">Hizmetiniz, *yönetici anahtarlarına* ve *sorgu anahtarlarına* sahiptir.</span><span class="sxs-lookup"><span data-stu-id="f9888-121">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="f9888-122">Birincil ve ikincil *yönetici anahtarları* tooall operations hello özelliği toomanage hello hizmeti dahil olmak üzere, tam haklar, oluşturun ve dizinler, dizin oluşturucular ve veri kaynaklarını silin.</span><span class="sxs-lookup"><span data-stu-id="f9888-122">Your primary and secondary *admin keys* grant full rights tooall operations, including hello ability toomanage hello service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="f9888-123">Tooregenerate hello birincil anahtar ve tam tersini karar verirseniz toouse hello ikincil anahtar devam edebilmesi için bu iki anahtar vardır.</span><span class="sxs-lookup"><span data-stu-id="f9888-123">There are two keys so that you can continue toouse hello secondary key if you decide tooregenerate hello primary key, and vice-versa.</span></span>
* <span data-ttu-id="f9888-124">*Sorgu anahtarları* salt okunur erişim tooindexes ve belgeleri verin ve arama istekleri gönderen genellikle dağıtılmış tooclient uygulamalardır.</span><span class="sxs-lookup"><span data-stu-id="f9888-124">Your *query keys* grant read-only access tooindexes and documents, and are typically distributed tooclient applications that issue search requests.</span></span>

<span data-ttu-id="f9888-125">Bir dizini sorgulama hello amacıyla, sorgu anahtarlarınızdan birini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9888-125">For hello purposes of querying an index, you can use one of your query keys.</span></span> <span data-ttu-id="f9888-126">Yönetici anahtarlarınız da sorgular için kullanılabilir, ancak bu daha iyi hello aşağıdaki gibi uygulama kodunuzda bir sorgu anahtarı kullanmanız gerekir [en az ayrıcalık prensibi](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span><span class="sxs-lookup"><span data-stu-id="f9888-126">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows hello [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span></span>

## <a name="create-an-instance-of-hello-searchindexclient-class"></a><span data-ttu-id="f9888-127">Merhaba Searchındexclient sınıfının bir örneğini oluşturun</span><span class="sxs-lookup"><span data-stu-id="f9888-127">Create an instance of hello SearchIndexClient class</span></span>
<span data-ttu-id="f9888-128">tooissue sorguları'hello Azure Search .NET SDK'sı ile toocreate hello örneği gerekir `SearchIndexClient` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="f9888-128">tooissue queries with hello Azure Search .NET SDK, you will need toocreate an instance of hello `SearchIndexClient` class.</span></span> <span data-ttu-id="f9888-129">Bu sınıfın birkaç oluşturucusu vardır.</span><span class="sxs-lookup"><span data-stu-id="f9888-129">This class has several constructors.</span></span> <span data-ttu-id="f9888-130">Arama hizmeti adınızı, dizin adı Hello istediğinizi alır ve bir `SearchCredentials` nesnesini parametre olarak.</span><span class="sxs-lookup"><span data-stu-id="f9888-130">hello one you want takes your search service name, index name, and a `SearchCredentials` object as parameters.</span></span> <span data-ttu-id="f9888-131">`SearchCredentials`, api anahtarınızı sarmalar.</span><span class="sxs-lookup"><span data-stu-id="f9888-131">`SearchCredentials` wraps your api-key.</span></span>

<span data-ttu-id="f9888-132">Aşağıdaki Hello kodu oluşturur Yeni bir `SearchIndexClient` hello "hotels" dizini için (oluşturulan [hello .NET SDK kullanarak Azure Search dizini oluşturma](search-create-index-dotnet.md)) hello arama hizmeti adı ve hello uygulamanın yapılandırma dosyasında depolanan api anahtarı için değerleri kullanarak dosya (`appsettings.json` hello hello durumda [örnek uygulama](http://aka.ms/search-dotnet-howto)):</span><span class="sxs-lookup"><span data-stu-id="f9888-132">hello code below creates a new `SearchIndexClient` for hello "hotels" index (created in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md)) using values for hello search service name and api-key that are stored in hello application's config file (`appsettings.json` in hello case of hello [sample application](http://aka.ms/search-dotnet-howto)):</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="f9888-133">`SearchIndexClient`, `Documents` özelliğine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="f9888-133">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="f9888-134">Bu özellik, tüm hello tooquery Azure Search dizinlerini gereken yöntemleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="f9888-134">This property provides all hello methods you need tooquery Azure Search indexes.</span></span>

## <a name="query-your-index"></a><span data-ttu-id="f9888-135">Dizininizi sorgulama</span><span class="sxs-lookup"><span data-stu-id="f9888-135">Query your index</span></span>
<span data-ttu-id="f9888-136">Merhaba .NET SDK ile arama arama hello basit `Documents.Search` yöntemi, `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="f9888-136">Searching with hello .NET SDK is as simple as calling hello `Documents.Search` method on your `SearchIndexClient`.</span></span> <span data-ttu-id="f9888-137">Bu yöntem ile birlikte hello arama metni dahil olmak üzere birkaç parametre alır bir `SearchParameters` kullanılan toofurther İyileştir hello sorgu olabilir nesnesi.</span><span class="sxs-lookup"><span data-stu-id="f9888-137">This method takes a few parameters, including hello search text, along with a `SearchParameters` object that can be used toofurther refine hello query.</span></span>

#### <a name="types-of-queries"></a><span data-ttu-id="f9888-138">Sorgu Türleri</span><span class="sxs-lookup"><span data-stu-id="f9888-138">Types of Queries</span></span>
<span data-ttu-id="f9888-139">Merhaba iki ana [sorgu türü](search-query-overview.md#types-of-queries) kullanacağınız olan `search` ve `filter`.</span><span class="sxs-lookup"><span data-stu-id="f9888-139">hello two main [query types](search-query-overview.md#types-of-queries) you will use are `search` and `filter`.</span></span> <span data-ttu-id="f9888-140">`search` sorgusu, dizininizdeki tüm *aranabilir* alanlarda bir veya daha çok terimi arar.</span><span class="sxs-lookup"><span data-stu-id="f9888-140">A `search` query searches for one or more terms in all *searchable* fields in your index.</span></span> <span data-ttu-id="f9888-141">`filter` sorgusu, bir dizindeki tüm *filtrelenebilir* alanlarda bir boole ifadesini değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="f9888-141">A `filter` query evaluates a boolean expression over all *filterable* fields in an index.</span></span>

<span data-ttu-id="f9888-142">Arama ve filtrelerin hello kullanılarak gerçekleştirilir `Documents.Search` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="f9888-142">Both searches and filters are performed using hello `Documents.Search` method.</span></span> <span data-ttu-id="f9888-143">Bir arama sorgusu hello geçirilebilir `searchText` bir filtre ifadesi hello geçirilebilirken parametresi `Filter` hello özelliğinin `SearchParameters` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="f9888-143">A search query can be passed in hello `searchText` parameter, while a filter expression can be passed in hello `Filter` property of hello `SearchParameters` class.</span></span> <span data-ttu-id="f9888-144">Arama, olmadan toofilter geçirmeniz yeterlidir `"*"` hello için `searchText` parametresi.</span><span class="sxs-lookup"><span data-stu-id="f9888-144">toofilter without searching, just pass `"*"` for hello `searchText` parameter.</span></span> <span data-ttu-id="f9888-145">filtreleme, olmadan toosearch yalnızca hello bırakın `Filter` özelliği ayarlanmadan veya içinde geçmeyin bir `SearchParameters` örneği.</span><span class="sxs-lookup"><span data-stu-id="f9888-145">toosearch without filtering, just leave hello `Filter` property unset, or do not pass in a `SearchParameters` instance at all.</span></span>

#### <a name="example-queries"></a><span data-ttu-id="f9888-146">Örnek Sorgular</span><span class="sxs-lookup"><span data-stu-id="f9888-146">Example Queries</span></span>
<span data-ttu-id="f9888-147">Aşağıdaki örnek kod hello gösterir birkaç farklı şekilde "dizin tanımlı tooquery hello hotels" [hello .NET SDK kullanarak Azure Search dizini oluşturma](search-create-index-dotnet.md#DefineIndex).</span><span class="sxs-lookup"><span data-stu-id="f9888-147">hello following sample code shows a few different ways tooquery hello "hotels" index defined in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md#DefineIndex).</span></span> <span data-ttu-id="f9888-148">Merhaba Arama sonuçlarıyla döndürülen hello belgeleri hello örnekleri olduğuna dikkat edin `Hotel` tanımlanan sınıfı [Veri Al'ı kullanarak Azure Search .NET SDK'sı hello](search-import-data-dotnet.md#HotelClass).</span><span class="sxs-lookup"><span data-stu-id="f9888-148">Note that hello documents returned with hello search results are instances of hello `Hotel` class, which was defined in [Data Import in Azure Search using hello .NET SDK](search-import-data-dotnet.md#HotelClass).</span></span> <span data-ttu-id="f9888-149">Merhaba örnek kod kullanır bir `WriteDocuments` yöntemi toooutput hello arama sonuçları toohello konsol.</span><span class="sxs-lookup"><span data-stu-id="f9888-149">hello sample code makes use of a `WriteDocuments` method toooutput hello search results toohello console.</span></span> <span data-ttu-id="f9888-150">Bu yöntem hello sonraki bölümde açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="f9888-150">This method is described in hello next section.</span></span>

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

## <a name="handle-search-results"></a><span data-ttu-id="f9888-151">Arama sonuçlarını işleme</span><span class="sxs-lookup"><span data-stu-id="f9888-151">Handle search results</span></span>
<span data-ttu-id="f9888-152">Merhaba `Documents.Search` yöntemi döndürür bir `DocumentSearchResult` hello hello sorgunun sonuçlarını içeren nesne.</span><span class="sxs-lookup"><span data-stu-id="f9888-152">hello `Documents.Search` method returns a `DocumentSearchResult` object that contains hello results of hello query.</span></span> <span data-ttu-id="f9888-153">Merhaba önceki bölümde Hello örnekte kullanılan adlı bir yöntem `WriteDocuments` toooutput hello arama sonuçları toohello konsolu:</span><span class="sxs-lookup"><span data-stu-id="f9888-153">hello example in hello previous section used a method called `WriteDocuments` toooutput hello search results toohello console:</span></span>

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

<span data-ttu-id="f9888-154">İşte hello önceki bölümdeki hello sorgularında olduğunu varsayarak hello "hotels" dizininin hello örnek verilerle doldurulur gibi ne hello sonuçlar görünür [Veri Al'ı kullanarak Azure Search .NET SDK'sı hello](search-import-data-dotnet.md):</span><span class="sxs-lookup"><span data-stu-id="f9888-154">Here is what hello results look like for hello queries in hello previous section, assuming hello "hotels" index is populated with hello sample data in [Data Import in Azure Search using hello .NET SDK](search-import-data-dotnet.md):</span></span>

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

<span data-ttu-id="f9888-155">Yukarıdaki örnek kod Hello hello konsol toooutput arama sonuçları kullanır.</span><span class="sxs-lookup"><span data-stu-id="f9888-155">hello sample code above uses hello console toooutput search results.</span></span> <span data-ttu-id="f9888-156">Bu gibi durumlarda, toodisplay arama sonuçlarında benzer şekilde, kendi uygulamanızda gerekir.</span><span class="sxs-lookup"><span data-stu-id="f9888-156">You will likewise need toodisplay search results in your own application.</span></span> <span data-ttu-id="f9888-157">Bkz: [github'daki bu örneğe](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) nasıl bir ASP.NET MVC tabanlı web uygulamasında toorender arama sonuçları bir örnek için.</span><span class="sxs-lookup"><span data-stu-id="f9888-157">See [this sample on GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) for an example of how toorender search results in an ASP.NET MVC-based web application.</span></span>

