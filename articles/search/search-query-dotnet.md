---
title: Dizin sorgulama (.NET API - Azure Search) | Microsoft Docs
description: "Azure Search'te bir arama sorgusu oluşturun ve arama sonuçlarını filtrelemek ve sıralamak için arama parametrelerini kullanın."
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
ms.openlocfilehash: 52bd0fd4cf70401dcf881c7f28d5cd91397bb059
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="query-your-azure-search-index-using-the-net-sdk"></a><span data-ttu-id="69760-103">.NET SDK kullanarak Azure Search dizininizi sorgulama</span><span class="sxs-lookup"><span data-stu-id="69760-103">Query your Azure Search index using the .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="69760-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="69760-104">Overview</span></span>](search-query-overview.md)
> * [<span data-ttu-id="69760-105">Portal</span><span class="sxs-lookup"><span data-stu-id="69760-105">Portal</span></span>](search-explorer.md)
> * [<span data-ttu-id="69760-106">.NET</span><span class="sxs-lookup"><span data-stu-id="69760-106">.NET</span></span>](search-query-dotnet.md)
> * [<span data-ttu-id="69760-107">REST</span><span class="sxs-lookup"><span data-stu-id="69760-107">REST</span></span>](search-query-rest-api.md)
> 
> 

<span data-ttu-id="69760-108">Bu makale, [Azure Search .NET SDK](https://aka.ms/search-sdk)'sını kullanarak bir dizinin nasıl sorgulanacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="69760-108">This article will show you how to query an index using the [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span>

<span data-ttu-id="69760-109">Bu kılavuzda başlamadan önce, [Azure Search dizini oluşturmuş](search-what-is-an-index.md) ve [bunu verilerle doldurmuş](search-what-is-data-import.md) olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="69760-109">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md) and [populated it with data](search-what-is-data-import.md).</span></span>

> [!NOTE]
> <span data-ttu-id="69760-110">Bu makaledeki örnek kodun tamamı C# dilinde yazılmıştır.</span><span class="sxs-lookup"><span data-stu-id="69760-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="69760-111">Tam kaynak kodunu [GitHub](http://aka.ms/search-dotnet-howto)'da bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69760-111">You can find the full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="69760-112">Ayrıca, örnek kodla ilgili daha ayrıntılı yönergeler için [Azure Search .NET SDK’sı](search-howto-dotnet-sdk.md) hakkındaki yazıları da okuyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69760-112">You can also read about the [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of the sample code.</span></span>

## <a name="identify-your-azure-search-services-query-api-key"></a><span data-ttu-id="69760-113">Azure Search hizmet sorgunuzun api anahtarını tanımlama</span><span class="sxs-lookup"><span data-stu-id="69760-113">Identify your Azure Search service's query api-key</span></span>
<span data-ttu-id="69760-114">Artık bir Azure Search dizini oluşturduğunuza göre, .NET SDK kullanarak sorgu göndermeye neredeyse hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="69760-114">Now that you have created an Azure Search index, you are almost ready to issue queries using the .NET SDK.</span></span> <span data-ttu-id="69760-115">Öncelikle, sağladığınız arama hizmeti için oluşturulan sorgu api anahtarlarından birini edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="69760-115">First, you will need to obtain one of the query api-keys that was generated for the search service you provisioned.</span></span> <span data-ttu-id="69760-116">.NET SDK, hizmetinize yönelik her istek için bu api anahtarını gönderir.</span><span class="sxs-lookup"><span data-stu-id="69760-116">The .NET SDK will send this api-key on every request to your service.</span></span> <span data-ttu-id="69760-117">İstek başına geçerli bir anahtara sahip olmak, isteği gönderen uygulama ve bunu işleyen hizmet arasında güven oluşturur.</span><span class="sxs-lookup"><span data-stu-id="69760-117">Having a valid key establishes trust, on a per request basis, between the application sending the request and the service that handles it.</span></span>

1. <span data-ttu-id="69760-118">Hizmetinizin api anahtarlarını bulmak için [Azure portalında](https://portal.azure.com/) oturum açabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="69760-118">To find your service's api-keys you can sign in to the [Azure portal](https://portal.azure.com/)</span></span>
2. <span data-ttu-id="69760-119">Azure Search hizmetinizin dikey penceresine gidin</span><span class="sxs-lookup"><span data-stu-id="69760-119">Go to your Azure Search service's blade</span></span>
3. <span data-ttu-id="69760-120">"Anahtarlar" simgesine tıklayın</span><span class="sxs-lookup"><span data-stu-id="69760-120">Click on the "Keys" icon</span></span>

<span data-ttu-id="69760-121">Hizmetiniz, *yönetici anahtarlarına* ve *sorgu anahtarlarına* sahiptir.</span><span class="sxs-lookup"><span data-stu-id="69760-121">Your service will have *admin keys* and *query keys*.</span></span>

* <span data-ttu-id="69760-122">Birincil ve ikincil *yönetici anahtarlarınız*; hizmeti yönetme, dizinler, dizin oluşturucular ve veri kaynakları ekleme ve silme de dahil olmak üzere her türlü işlem için tüm hakları verir.</span><span class="sxs-lookup"><span data-stu-id="69760-122">Your primary and secondary *admin keys* grant full rights to all operations, including the ability to manage the service, create and delete indexes, indexers, and data sources.</span></span> <span data-ttu-id="69760-123">Birincil anahtarı yeniden oluşturmaya karar verirseniz ikincil anahtarı kullanmaya devam edebilmeniz ve tam tersini yapabilmeniz için iki anahtar vardır.</span><span class="sxs-lookup"><span data-stu-id="69760-123">There are two keys so that you can continue to use the secondary key if you decide to regenerate the primary key, and vice-versa.</span></span>
* <span data-ttu-id="69760-124">*Sorgu anahtarları*, dizinler ve belgeler için salt okunur erişim verir ve genellikle, arama istekleri gönderen istemci uygulamalarına dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="69760-124">Your *query keys* grant read-only access to indexes and documents, and are typically distributed to client applications that issue search requests.</span></span>

<span data-ttu-id="69760-125">Bir dizini sorgulama amacıyla, sorgu anahtarlarınızdan birini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="69760-125">For the purposes of querying an index, you can use one of your query keys.</span></span> <span data-ttu-id="69760-126">Yönetici anahtarlarınız da sorgular için kullanılabilir ancak uygulama kodunuzda bir sorgu anahtarı kullanmanız gerekir. Böylece [En az ayrıcalık prensibi](https://en.wikipedia.org/wiki/Principle_of_least_privilege) daha iyi takip edilmiş olur.</span><span class="sxs-lookup"><span data-stu-id="69760-126">Your admin keys can also be used for queries, but you should use a query key in your application code as this better follows the [Principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege).</span></span>

## <a name="create-an-instance-of-the-searchindexclient-class"></a><span data-ttu-id="69760-127">SearchIndexClient sınıfının bir örneğini oluşturma</span><span class="sxs-lookup"><span data-stu-id="69760-127">Create an instance of the SearchIndexClient class</span></span>
<span data-ttu-id="69760-128">Azure Search .NET SDK'sıyla sorgu yürütmek için `SearchIndexClient` sınıfının bir örneğini oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="69760-128">To issue queries with the Azure Search .NET SDK, you will need to create an instance of the `SearchIndexClient` class.</span></span> <span data-ttu-id="69760-129">Bu sınıfın birkaç oluşturucusu vardır.</span><span class="sxs-lookup"><span data-stu-id="69760-129">This class has several constructors.</span></span> <span data-ttu-id="69760-130">İstediğiniz oluşturucu, arama hizmeti adınızı, dizin adınızı ve `SearchCredentials` nesnesini parametre olarak alır.</span><span class="sxs-lookup"><span data-stu-id="69760-130">The one you want takes your search service name, index name, and a `SearchCredentials` object as parameters.</span></span> <span data-ttu-id="69760-131">`SearchCredentials`, api anahtarınızı sarmalar.</span><span class="sxs-lookup"><span data-stu-id="69760-131">`SearchCredentials` wraps your api-key.</span></span>

<span data-ttu-id="69760-132">Aşağıdaki kod, uygulamanın yapılandırma dosyasında ([örnek uygulama](http://aka.ms/search-dotnet-howto) olması durumunda `appsettings.json`) depolanan arama hizmeti adına ve API anahtarına ilişkin değerleri kullanarak "hotels" dizini ([.NET SDK kullanarak Azure Search dizini oluşturma](search-create-index-dotnet.md) bölümünde oluşturuldu) için yeni bir `SearchIndexClient` oluşturur:</span><span class="sxs-lookup"><span data-stu-id="69760-132">The code below creates a new `SearchIndexClient` for the "hotels" index (created in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md)) using values for the search service name and api-key that are stored in the application's config file (`appsettings.json` in the case of the [sample application](http://aka.ms/search-dotnet-howto)):</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="69760-133">`SearchIndexClient`, `Documents` özelliğine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="69760-133">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="69760-134">Bu özellik Azure Search dizinlerini sorgulamanız için gereken tüm yöntemleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="69760-134">This property provides all the methods you need to query Azure Search indexes.</span></span>

## <a name="query-your-index"></a><span data-ttu-id="69760-135">Dizininizi sorgulama</span><span class="sxs-lookup"><span data-stu-id="69760-135">Query your index</span></span>
<span data-ttu-id="69760-136">.NET SDK ile arama, `SearchIndexClient` öğenizde `Documents.Search` yöntemini çağırmak kadar kolaydır.</span><span class="sxs-lookup"><span data-stu-id="69760-136">Searching with the .NET SDK is as simple as calling the `Documents.Search` method on your `SearchIndexClient`.</span></span> <span data-ttu-id="69760-137">Bu yöntem, arama metni dahil olmak üzere sorguyu daha da ayrıntılandırmak için kullanılabilecek bir `SearchParameters` nesnesiyle birlikte birkaç parametre alır.</span><span class="sxs-lookup"><span data-stu-id="69760-137">This method takes a few parameters, including the search text, along with a `SearchParameters` object that can be used to further refine the query.</span></span>

#### <a name="types-of-queries"></a><span data-ttu-id="69760-138">Sorgu Türleri</span><span class="sxs-lookup"><span data-stu-id="69760-138">Types of Queries</span></span>
<span data-ttu-id="69760-139">Kullanacağınız iki ana [sorgu türü](search-query-overview.md#types-of-queries) `search` ve `filter` sorgularıdır.</span><span class="sxs-lookup"><span data-stu-id="69760-139">The two main [query types](search-query-overview.md#types-of-queries) you will use are `search` and `filter`.</span></span> <span data-ttu-id="69760-140">`search` sorgusu, dizininizdeki tüm *aranabilir* alanlarda bir veya daha çok terimi arar.</span><span class="sxs-lookup"><span data-stu-id="69760-140">A `search` query searches for one or more terms in all *searchable* fields in your index.</span></span> <span data-ttu-id="69760-141">`filter` sorgusu, bir dizindeki tüm *filtrelenebilir* alanlarda bir boole ifadesini değerlendirir.</span><span class="sxs-lookup"><span data-stu-id="69760-141">A `filter` query evaluates a boolean expression over all *filterable* fields in an index.</span></span>

<span data-ttu-id="69760-142">Arama ve filtrelerin her ikisi de `Documents.Search` yöntemi kullanılarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="69760-142">Both searches and filters are performed using the `Documents.Search` method.</span></span> <span data-ttu-id="69760-143">Bir arama sorgusu `searchText` parametresinde geçirilebilirken bir filtre ifadesi `SearchParameters` sınıfının `Filter` özelliğinden geçirilebilir.</span><span class="sxs-lookup"><span data-stu-id="69760-143">A search query can be passed in the `searchText` parameter, while a filter expression can be passed in the `Filter` property of the `SearchParameters` class.</span></span> <span data-ttu-id="69760-144">Arama yapmadan filtrelemek üzere `searchText` parametresi için `"*"` geçirmeniz yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="69760-144">To filter without searching, just pass `"*"` for the `searchText` parameter.</span></span> <span data-ttu-id="69760-145">Filtrelemeden arama yapmak için `Filter` özelliğini ayarlamadan bırakmanız veya bir `SearchParameters` örneği geçirmemeniz yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="69760-145">To search without filtering, just leave the `Filter` property unset, or do not pass in a `SearchParameters` instance at all.</span></span>

#### <a name="example-queries"></a><span data-ttu-id="69760-146">Örnek Sorgular</span><span class="sxs-lookup"><span data-stu-id="69760-146">Example Queries</span></span>
<span data-ttu-id="69760-147">Aşağıdaki örnek kod, [.NET SDK kullanarak Azure Search dizini oluşturma](search-create-index-dotnet.md#DefineIndex)'da tanımlanan "hotels" dizinini sorgulamanın birkaç farklı yolunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="69760-147">The following sample code shows a few different ways to query the "hotels" index defined in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md#DefineIndex).</span></span> <span data-ttu-id="69760-148">Arama sonuçlarıyla döndürülen belgelerin, [.NET SDK kullanarak Azure Search'te Veri İçeri Aktarma](search-import-data-dotnet.md#HotelClass)'da tanımlanan `Hotel` sınıfının örnekleri olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="69760-148">Note that the documents returned with the search results are instances of the `Hotel` class, which was defined in [Data Import in Azure Search using the .NET SDK](search-import-data-dotnet.md#HotelClass).</span></span> <span data-ttu-id="69760-149">Örnek kod, arama sonuçlarını konsola çıkarmak için bir `WriteDocuments` yöntemini kullanır.</span><span class="sxs-lookup"><span data-stu-id="69760-149">The sample code makes use of a `WriteDocuments` method to output the search results to the console.</span></span> <span data-ttu-id="69760-150">Bu yöntem bir sonraki bölümde açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="69760-150">This method is described in the next section.</span></span>

```csharp
SearchParameters parameters;
DocumentSearchResult<Hotel> results;

Console.WriteLine("Search the entire index for the term 'budget' and return only the hotelName field:\n");

parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);

Console.Write("Apply a filter to the index to find hotels cheaper than $150 per night, ");
Console.WriteLine("and return the hotelId and description:\n");

parameters =
    new SearchParameters()
    {
        Filter = "baseRate lt 150",
        Select = new[] { "hotelId", "description" }
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);

Console.Write("Search the entire index, order by a specific field (lastRenovationDate) ");
Console.Write("in descending order, take the top two results, and show only hotelName and ");
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

Console.WriteLine("Search the entire index for the term 'motel':\n");

parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

## <a name="handle-search-results"></a><span data-ttu-id="69760-151">Arama sonuçlarını işleme</span><span class="sxs-lookup"><span data-stu-id="69760-151">Handle search results</span></span>
<span data-ttu-id="69760-152">`Documents.Search` yöntemi, sorgunun sonuçlarını içeren bir `DocumentSearchResult` nesnesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="69760-152">The `Documents.Search` method returns a `DocumentSearchResult` object that contains the results of the query.</span></span> <span data-ttu-id="69760-153">Önceki bölümdeki örnek, arama sonuçlarını konsola çıkarmak için `WriteDocuments` adlı bir yöntemi kullanır:</span><span class="sxs-lookup"><span data-stu-id="69760-153">The example in the previous section used a method called `WriteDocuments` to output the search results to the console:</span></span>

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

<span data-ttu-id="69760-154">Önceki bölümdeki sorguların sonuçları, "hotels" dizininin, [.NET SDK kullanarak Azure Search'te Veri İçeri Aktarma](search-import-data-dotnet.md)'da verilen örnek verilerle doldurulduğu varsayıldığında şöyledir:</span><span class="sxs-lookup"><span data-stu-id="69760-154">Here is what the results look like for the queries in the previous section, assuming the "hotels" index is populated with the sample data in [Data Import in Azure Search using the .NET SDK](search-import-data-dotnet.md):</span></span>

```
Search the entire index for the term 'budget' and return only the hotelName field:

Name: Roach Motel

Apply a filter to the index to find hotels cheaper than $150 per night, and return the hotelId and description:

ID: 2   Description: Cheapest hotel in town
ID: 3   Description: Close to town hall and the river

Search the entire index, order by a specific field (lastRenovationDate) in descending order, take the top two results, and show only hotelName and lastRenovationDate:

Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

Search the entire index for the term 'motel':

ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577
```

<span data-ttu-id="69760-155">Yukarıdaki örnek kod, arama sonuçlarını çıkarmak için konsolu kullanır.</span><span class="sxs-lookup"><span data-stu-id="69760-155">The sample code above uses the console to output search results.</span></span> <span data-ttu-id="69760-156">Benzer şekilde, kendi uygulamanızda arama sonuçlarını göstermeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="69760-156">You will likewise need to display search results in your own application.</span></span> <span data-ttu-id="69760-157">ASP.NET MVC tabanlı bir web uygulamasında arama sonuçlarının nasıl işlendiğine bir örnek için [GitHub'daki bu örneğe](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) bakın.</span><span class="sxs-lookup"><span data-stu-id="69760-157">See [this sample on GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetSample) for an example of how to render search results in an ASP.NET MVC-based web application.</span></span>

