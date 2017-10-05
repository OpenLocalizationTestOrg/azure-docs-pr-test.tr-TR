---
title: "Azure Search .NET uygulamasından kullanma | Microsoft Docs"
description: "Azure Search bir .NET uygulamasında kullanma"
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
ms.openlocfilehash: 552a7ab193e12d2e72da494166d774e974c85d47
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-search-from-a-net-application"></a><span data-ttu-id="dd5f7-103">Azure Search bir .NET uygulamasında kullanma</span><span class="sxs-lookup"><span data-stu-id="dd5f7-103">How to use Azure Search from a .NET Application</span></span>
<span data-ttu-id="dd5f7-104">Bu makale ile çalışır almak için bir kılavuz olan [Azure Search .NET SDK'sı](https://aka.ms/search-sdk).</span><span class="sxs-lookup"><span data-stu-id="dd5f7-104">This article is a walkthrough to get you up and running with the [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span> <span data-ttu-id="dd5f7-105">.NET SDK kullanarak Azure Search uygulamanızda zengin arama deneyimi uygulamak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-105">You can use the .NET SDK to implement a rich search experience in your application using Azure Search.</span></span>

## <a name="whats-in-the-azure-search-sdk"></a><span data-ttu-id="dd5f7-106">Azure nedir arama SDK</span><span class="sxs-lookup"><span data-stu-id="dd5f7-106">What's in the Azure Search SDK</span></span>
<span data-ttu-id="dd5f7-107">Bir istemci Kitaplığı'nın SDK oluşur `Microsoft.Azure.Search`.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-107">The SDK consists of a client library, `Microsoft.Azure.Search`.</span></span> <span data-ttu-id="dd5f7-108">Dizinleri, veri kaynakları ve dizin oluşturucular, yönetmek yanı sıra karşıya yükleme ve belgeleri yönetmek ve tüm HTTP ve JSON ayrıntıları ile mücadele etmek zorunda kalmadan sorgularını yürütmek sağlar.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-108">It enables you to manage your indexes, data sources, and indexers, as well as upload and manage documents, and execute queries, all without having to deal with the details of HTTP and JSON.</span></span>

<span data-ttu-id="dd5f7-109">İstemci Kitaplığı gibi sınıflarını tanımlayan `Index`, `Field`, ve `Document`, yanı sıra operations ister `Indexes.Create` ve `Documents.Search` üzerinde `SearchServiceClient` ve `SearchIndexClient` sınıfları.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-109">The client library defines classes like `Index`, `Field`, and `Document`, as well as operations like `Indexes.Create` and `Documents.Search` on the `SearchServiceClient` and `SearchIndexClient` classes.</span></span> <span data-ttu-id="dd5f7-110">Bu sınıfların şu ad alanlarından düzenlenmiştir:</span><span class="sxs-lookup"><span data-stu-id="dd5f7-110">These classes are organized into the following namespaces:</span></span>

* [<span data-ttu-id="dd5f7-111">Microsoft.Azure.Search</span><span class="sxs-lookup"><span data-stu-id="dd5f7-111">Microsoft.Azure.Search</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)
* [<span data-ttu-id="dd5f7-112">Microsoft.Azure.Search.Models</span><span class="sxs-lookup"><span data-stu-id="dd5f7-112">Microsoft.Azure.Search.Models</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models)

<span data-ttu-id="dd5f7-113">Geçerli sürümü Azure Search .NET SDK'sı, genellikle kullanıma sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-113">The current version of the Azure Search .NET SDK is now generally available.</span></span> <span data-ttu-id="dd5f7-114">Ziyaret için bir sonraki sürümde birleştirmek için bize geri bildirim sağlamak istiyorsanız, lütfen bizim [görüş sayfası](https://feedback.azure.com/forums/263029-azure-search/).</span><span class="sxs-lookup"><span data-stu-id="dd5f7-114">If you would like to provide feedback for us to incorporate in the next version, please visit our [feedback page](https://feedback.azure.com/forums/263029-azure-search/).</span></span>

<span data-ttu-id="dd5f7-115">.NET SDK'sı sürüm destekler `2016-09-01` , [Azure Search REST API'sini](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="dd5f7-115">The .NET SDK supports version `2016-09-01` of the [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span> <span data-ttu-id="dd5f7-116">Bu sürümü artık özel Çözümleyicileri ve Azure Blob ve Azure Table dizin oluşturucu desteği içerir.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-116">This version now includes support for custom analyzers and Azure Blob and Azure Table indexer support.</span></span> <span data-ttu-id="dd5f7-117">Önizleme özellikleri *değil* JSON ve CSV dosyalarını dizin oluşturma için destek gibi bu sürümü bir parçası olan [Önizleme](search-api-2015-02-28-preview.md) ve eski aracılığıyla kullanılabilen [.NET SDK'sı2.0-Önizlemesürümü](https://aka.ms/search-sdk-preview).</span><span class="sxs-lookup"><span data-stu-id="dd5f7-117">Preview features that are *not* part of this version, such as support for indexing JSON and CSV files, are in [preview](search-api-2015-02-28-preview.md) and available via the older [2.0-preview version of the .NET SDK](https://aka.ms/search-sdk-preview).</span></span>

<span data-ttu-id="dd5f7-118">Bu SDK desteklemediği [yönetim işlemlerini](https://docs.microsoft.com/rest/api/searchmanagement/) oluşturma ve arama hizmetleri ölçekleme ve API anahtarlarını yönetme gibi.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-118">This SDK does not support [Management Operations](https://docs.microsoft.com/rest/api/searchmanagement/) such as creating and scaling Search services and managing API keys.</span></span> <span data-ttu-id="dd5f7-119">Bir .NET uygulamasından arama kaynaklarınızı yönetmek gerekiyorsa, kullanabileceğiniz [Azure Search .NET Yönetim SDK](https://aka.ms/search-mgmt-sdk).</span><span class="sxs-lookup"><span data-stu-id="dd5f7-119">If you need to manage your Search resources from a .NET application, you can use the [Azure Search .NET Management SDK](https://aka.ms/search-mgmt-sdk).</span></span>

## <a name="upgrading-to-the-latest-version-of-the-sdk"></a><span data-ttu-id="dd5f7-120">SDK'ın en son sürüme yükseltme</span><span class="sxs-lookup"><span data-stu-id="dd5f7-120">Upgrading to the latest version of the SDK</span></span>
<span data-ttu-id="dd5f7-121">Azure Search .NET SDK'sı daha eski bir sürümü zaten kullanmakta olduğunuz ve genel olarak kullanılabilir yeni sürüme yükseltmek istiyorsanız [bu makalede](search-dotnet-sdk-migration.md) açıklar nasıl.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-121">If you're already using an older version of the Azure Search .NET SDK and you'd like to upgrade to the new generally available version, [this article](search-dotnet-sdk-migration.md) explains how.</span></span>

## <a name="requirements-for-the-sdk"></a><span data-ttu-id="dd5f7-122">SDK'sı gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="dd5f7-122">Requirements for the SDK</span></span>
1. <span data-ttu-id="dd5f7-123">Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-123">Visual Studio 2017.</span></span>
2. <span data-ttu-id="dd5f7-124">Kendi Azure Search hizmeti.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-124">Your own Azure Search service.</span></span> <span data-ttu-id="dd5f7-125">SDK'yı kullanmak için adını hizmetiniz ve bir veya daha fazla API anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-125">In order to use the SDK, you will need the name of your service and one or more API keys.</span></span> <span data-ttu-id="dd5f7-126">[Portalda bir hizmet oluşturma](search-create-service-portal.md) bu adımları uygularken size yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-126">[Create a service in the portal](search-create-service-portal.md) will help you through these steps.</span></span>
3. <span data-ttu-id="dd5f7-127">Azure Search .NET SDK'sını indirin [NuGet paketi](http://www.nuget.org/packages/Microsoft.Azure.Search) "NuGet paketlerini Yönet" Visual Studio kullanarak.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-127">Download the Azure Search .NET SDK [NuGet package](http://www.nuget.org/packages/Microsoft.Azure.Search) by using "Manage NuGet Packages" in Visual Studio.</span></span> <span data-ttu-id="dd5f7-128">Paket adı için yalnızca arama `Microsoft.Azure.Search` NuGet.org üzerinde.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-128">Just search for the package name `Microsoft.Azure.Search` on NuGet.org.</span></span>

<span data-ttu-id="dd5f7-129">Azure Search .NET SDK'sı .NET Framework 4.6 ve .NET Core hedefleme uygulamaları destekler.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-129">The Azure Search .NET SDK supports applications targeting the .NET Framework 4.6 and .NET Core.</span></span>

## <a name="core-scenarios"></a><span data-ttu-id="dd5f7-130">Temel senaryolar</span><span class="sxs-lookup"><span data-stu-id="dd5f7-130">Core scenarios</span></span>
<span data-ttu-id="dd5f7-131">Arama uygulamanızda yapmanız gerekir birkaç şey vardır.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-131">There are several things you'll need to do in your search application.</span></span> <span data-ttu-id="dd5f7-132">Bu öğreticide, bu temel senaryolar şu konulara değineceğiz:</span><span class="sxs-lookup"><span data-stu-id="dd5f7-132">In this tutorial, we'll cover these core scenarios:</span></span>

* <span data-ttu-id="dd5f7-133">Dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="dd5f7-133">Creating an index</span></span>
* <span data-ttu-id="dd5f7-134">Belgelerle dizin doldurma</span><span class="sxs-lookup"><span data-stu-id="dd5f7-134">Populating the index with documents</span></span>
* <span data-ttu-id="dd5f7-135">Tam metin araması ve filtreleri kullanarak belgeleri için arama</span><span class="sxs-lookup"><span data-stu-id="dd5f7-135">Searching for documents using full-text search and filters</span></span>

<span data-ttu-id="dd5f7-136">Aşağıdaki örnek kod her birinde göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-136">The sample code that follows illustrates each of these.</span></span> <span data-ttu-id="dd5f7-137">Kod parçacıkları, kendi uygulamanızda kullanmak üzere çekinmeyin.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-137">Feel free to use the code snippets in your own application.</span></span>

### <a name="overview"></a><span data-ttu-id="dd5f7-138">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="dd5f7-138">Overview</span></span>
<span data-ttu-id="dd5f7-139">Biz keşfetme örnek uygulamayı yeni bir oluşturur "hotels" adlı dizin birkaç belgelerle doldurur sonra bazı arama sorguları yürütür.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-139">The sample application we'll be exploring creates a new index named "hotels", populates it with a few documents, then executes some search queries.</span></span> <span data-ttu-id="dd5f7-140">Genel akış gösteren programın ana şöyledir:</span><span class="sxs-lookup"><span data-stu-id="dd5f7-140">Here is the main program, showing the overall flow:</span></span>

```csharp
// This sample shows how to delete, create, upload documents and query an index
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

    Console.WriteLine("{0}", "Complete.  Press any key to end application...\n");
    Console.ReadKey();
}
```

> [!NOTE]
> <span data-ttu-id="dd5f7-141">Bu kılavuzda kullanılan örnek uygulamanın tam kaynak kodunu [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo) üzerinde bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-141">You can find the full source code of the sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>
> 
>

<span data-ttu-id="dd5f7-142">Biz bu adım adım adım geçireceğiz.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-142">We'll walk through this step by step.</span></span> <span data-ttu-id="dd5f7-143">Önce yeni bir oluşturmak ihtiyacımız `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-143">First we need to create a new `SearchServiceClient`.</span></span> <span data-ttu-id="dd5f7-144">Bu nesne, dizinleri yönetmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-144">This object allows you to manage indexes.</span></span> <span data-ttu-id="dd5f7-145">Bir oluşturmak için bir yönetici API anahtarı yanı sıra Azure Search hizmet adı sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-145">In order to construct one, you need to provide your Azure Search service name as well as an admin API key.</span></span> <span data-ttu-id="dd5f7-146">Bu bilgileri girebilirsiniz `appsettings.json` dosyasının [örnek uygulama](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="dd5f7-146">You can enter this information in the `appsettings.json` file of the [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

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
> <span data-ttu-id="dd5f7-147">(Burada bir yönetici anahtarı gerekli Örneğin, bir sorgu anahtarı), yanlış bir tuşa sağlarsanız, `SearchServiceClient` özel durum oluşturacak bir `CloudException` şu hata ile bir işlemi yöntemi bunun üzerinde gibi ilk kez çağırdığınızda "Yasak" iletisi `Indexes.Create`.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-147">If you provide an incorrect key (for example, a query key where an admin key was required), the `SearchServiceClient` will throw a `CloudException` with the error message "Forbidden" the first time you call an operation method on it, such as `Indexes.Create`.</span></span> <span data-ttu-id="dd5f7-148">Bu, olanak olursa, bizim API anahtarı denetleyin.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-148">If this happens to you, double-check our API key.</span></span>
> 
> 

<span data-ttu-id="dd5f7-149">Sonraki birkaç satır "zaten varsa, ilk silme hotels" adlı bir dizin oluşturma yöntemlerini çağırın.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-149">The next few lines call methods to create an index named "hotels", deleting it first if it already exists.</span></span> <span data-ttu-id="dd5f7-150">Biz bu yöntemlerle biraz daha sonra yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-150">We will walk through these methods a little later.</span></span>

```csharp
Console.WriteLine("{0}", "Deleting index...\n");
DeleteHotelsIndexIfExists(serviceClient);

Console.WriteLine("{0}", "Creating index...\n");
CreateHotelsIndex(serviceClient);
```

<span data-ttu-id="dd5f7-151">Ardından, dizin doldurulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-151">Next, the index needs to be populated.</span></span> <span data-ttu-id="dd5f7-152">Bunu yapmak için ihtiyacımız bir `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-152">To do this, we will need a `SearchIndexClient`.</span></span> <span data-ttu-id="dd5f7-153">Abonelik sahibi olmak için iki yolu vardır: onu oluşturmak ya da çağırma `Indexes.GetClient` üzerinde `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-153">There are two ways to obtain one: by constructing it, or by calling `Indexes.GetClient` on the `SearchServiceClient`.</span></span> <span data-ttu-id="dd5f7-154">İkinci kolaylık sağlamak için kullanırız.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-154">We use the latter for convenience.</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="dd5f7-155">Genel bir arama uygulamasında, dizin yönetimi ve popülasyon, arama sorgularından ayrı bir bileşen tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-155">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="dd5f7-156">`Indexes.GetClient`, başka bir `SearchCredentials` sağlamanızı gerektirmediğinden, dizini doldurmak için uygundur.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-156">`Indexes.GetClient` is convenient for populating an index because it saves you the trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="dd5f7-157">Yeni `SearchIndexClient` için `SearchServiceClient` oluşturmak üzere kullandığınız yönetici anahtarını geçirerek bunu yapar.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-157">It does this by passing the admin key that you used to create the `SearchServiceClient` to the new `SearchIndexClient`.</span></span> <span data-ttu-id="dd5f7-158">Ancak uygulamanızın sorguları yürüten bölümünde, bir yönetici anahtarı yerine sorgu anahtarında geçirebilmeniz için doğrudan `SearchIndexClient` oluşturmak daha iyi olur.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-158">However, in the part of your application that executes queries, it is better to create the `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="dd5f7-159">Bu, en az ayrıcalık prensibi tutarlıdır ve uygulamanızı daha güvenli hale getirmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-159">This is consistent with the principle of least privilege and will help to make your application more secure.</span></span> <span data-ttu-id="dd5f7-160">Yönetici anahtarları ve sorgu anahtarları hakkında daha fazla bilgi için [burada](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span><span class="sxs-lookup"><span data-stu-id="dd5f7-160">You can find out more about admin keys and query keys [here](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span></span>
> 
> 

<span data-ttu-id="dd5f7-161">Biz sahip olduğunuza göre bir `SearchIndexClient`, biz dizin doldurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-161">Now that we have a `SearchIndexClient`, we can populate the index.</span></span> <span data-ttu-id="dd5f7-162">Bu size daha sonra size yol gösterir başka bir yöntem kullanarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-162">This is done by another method that we will walk through later.</span></span>

```csharp
Console.WriteLine("{0}", "Uploading documents...\n");
UploadDocuments(indexClient);
```

<span data-ttu-id="dd5f7-163">Son olarak, biz birkaç arama sorguları çalıştırmak ve sonuçları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-163">Finally, we execute a few search queries and display the results.</span></span> <span data-ttu-id="dd5f7-164">Bu süre kullanırız farklı bir `SearchIndexClient`:</span><span class="sxs-lookup"><span data-stu-id="dd5f7-164">This time we use a different `SearchIndexClient`:</span></span>

```csharp
ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

RunQueries(indexClientForQueries);
```

<span data-ttu-id="dd5f7-165">Biz yakından sürer `RunQueries` daha sonra yöntemi.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-165">We will take a closer look at the `RunQueries` method later.</span></span> <span data-ttu-id="dd5f7-166">Yeni oluşturmak için kodu işte `SearchIndexClient`:</span><span class="sxs-lookup"><span data-stu-id="dd5f7-166">Here is the code to create the new `SearchIndexClient`:</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="dd5f7-167">Bu süre dizine yazma erişimi gerekmez bu yana bir sorgu anahtarı kullanırız.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-167">This time we use a query key since we do not need write access to the index.</span></span> <span data-ttu-id="dd5f7-168">Bu bilgileri girebilirsiniz `appsettings.json` dosyasının [örnek uygulama](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="dd5f7-168">You can enter this information in the `appsettings.json` file of the [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

<span data-ttu-id="dd5f7-169">Bu uygulamayı geçerli bir hizmet adı ve API anahtarlarını çalıştırırsanız, çıktı aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="dd5f7-169">If you run this application with a valid service name and API keys, the output should look like this:</span></span>

    Deleting index...
    
    Creating index...
    
    Uploading documents...
    
    Waiting for documents to be indexed...
    
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
    
    Complete.  Press any key to end application...

<span data-ttu-id="dd5f7-170">Uygulamanın tam kaynak kodu, bu makalenin sonundaki sağlanır.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-170">The full source code of the application is provided at the end of this article.</span></span>

<span data-ttu-id="dd5f7-171">Ardından, biz tarafından çağrılır yöntemlerin her biri daha ayrıntılı bir bakış sürer `Main`.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-171">Next, we will take a closer look at each of the methods called by `Main`.</span></span>

### <a name="creating-an-index"></a><span data-ttu-id="dd5f7-172">Dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="dd5f7-172">Creating an index</span></span>
<span data-ttu-id="dd5f7-173">Oluşturduktan sonra bir `SearchServiceClient`, sonraki şey `Main` mu zaten varsa "hotels" dizininin olduğunda.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-173">After creating a `SearchServiceClient`, the next thing `Main` does is delete the "hotels" index if it already exists.</span></span> <span data-ttu-id="dd5f7-174">Aşağıdaki yöntemi tarafından gerçekleştirilir:</span><span class="sxs-lookup"><span data-stu-id="dd5f7-174">That is done by the following method:</span></span>

```csharp
private static void DeleteHotelsIndexIfExists(SearchServiceClient serviceClient)
{
    if (serviceClient.Indexes.Exists("hotels"))
    {
        serviceClient.Indexes.Delete("hotels");
    }
}
```

<span data-ttu-id="dd5f7-175">Bu yöntem verilen `SearchServiceClient` dizin varsa ve bu durumda denetlemek için onu silin.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-175">This method uses the given `SearchServiceClient` to check if the index exists, and if so, delete it.</span></span>

> [!NOTE]
> <span data-ttu-id="dd5f7-176">Bu makaledeki örnek kod, kolaylık amacıyla Azure Search .NET SDK'sının zaman uyumlu yöntemlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-176">The example code in this article uses the synchronous methods of the Azure Search .NET SDK for simplicity.</span></span> <span data-ttu-id="dd5f7-177">Kendi uygulamalarınızda zaman uyumsuz yöntemler kullanarak bunları ölçeklenebilir ve esnek tutmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-177">We recommend that you use the asynchronous methods in your own applications to keep them scalable and responsive.</span></span> <span data-ttu-id="dd5f7-178">Örneğin, yukarıdaki yöntemi kullanabilirsiniz `ExistsAsync` ve `DeleteAsync` yerine `Exists` ve `Delete`.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-178">For example, in the method above you could use `ExistsAsync` and `DeleteAsync` instead of `Exists` and `Delete`.</span></span>
> 
> 

<span data-ttu-id="dd5f7-179">Ardından, `Main` bu yöntemini çağırarak yeni bir "hotels" dizini oluşturur:</span><span class="sxs-lookup"><span data-stu-id="dd5f7-179">Next, `Main` creates a new "hotels" index by calling this method:</span></span>

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

<span data-ttu-id="dd5f7-180">Bu yöntem yeni bir oluşturur `Index` listesini nesnesiyle `Field` yeni bir dizin şemasını tanımlayan nesneleri.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-180">This method creates a new `Index` object with a list of `Field` objects that defines the schema of the new index.</span></span> <span data-ttu-id="dd5f7-181">Her alanın bir adı, veri türü ve arama davranışını tanımlamak birkaç öznitelik vardır.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-181">Each field has a name, data type, and several attributes that define its search behavior.</span></span> <span data-ttu-id="dd5f7-182">`FieldBuilder` Sınıfı listesini oluşturmak için yansıma kullanır `Field` nesneler genel özellikleri ve özniteliklerini inceleyerek tarafından dizini için belirtilen `Hotel` model sınıfı.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-182">The `FieldBuilder` class uses reflection to create a list of `Field` objects for the index by examining the public properties and attributes of the given `Hotel` model class.</span></span> <span data-ttu-id="dd5f7-183">Biz yakından gitmek `Hotel` daha sonra sınıfı.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-183">We'll take a closer look at the `Hotel` class later on.</span></span>

> [!NOTE]
> <span data-ttu-id="dd5f7-184">Her zaman listesi oluşturabilirsiniz `Field` kullanmak yerine doğrudan nesneleri `FieldBuilder` gerekiyorsa.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-184">You can always create the list of `Field` objects directly instead of using `FieldBuilder` if needed.</span></span> <span data-ttu-id="dd5f7-185">Örneğin, bir model sınıfı kullanmak istemeyebilirsiniz veya öznitelikleri ekleyerek değiştirmeye istemediğiniz varolan bir model sınıfı kullanmanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-185">For example, you may not want to use a model class or you may need to use an existing model class that you don't want to modify by adding attributes.</span></span>
>
> 

<span data-ttu-id="dd5f7-186">Alanlara ek olarak (bunlar kısaltma örnekten göz ardı edilir) dizine ayrıca Puanlama profilleri, ilgili veya CORS seçenekleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-186">In addition to fields, you can also add scoring profiles, suggesters, or CORS options to the Index (these are omitted from the sample for brevity).</span></span> <span data-ttu-id="dd5f7-187">Dizin nesnesi ve onun bağlı bölümlerinde hakkında daha fazla bilgi bulabilirsiniz [SDK başvurusu](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), ın yanı [Azure Search REST API Başvurusu](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="dd5f7-187">You can find more information about the Index object and its constituent parts in the [SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), as well as in the [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

### <a name="populating-the-index"></a><span data-ttu-id="dd5f7-188">Dizin doldurma</span><span class="sxs-lookup"><span data-stu-id="dd5f7-188">Populating the index</span></span>
<span data-ttu-id="dd5f7-189">Sonraki adım `Main` yeni oluşturulan dizinini doldurmak için.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-189">The next step in `Main` is to populate the newly-created index.</span></span> <span data-ttu-id="dd5f7-190">Bu aşağıdaki yönteminde gerçekleştirilir:</span><span class="sxs-lookup"><span data-stu-id="dd5f7-190">This is done in the following method:</span></span>

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
            Description = "Close to town hall and the river"
        }
    };

    var batch = IndexBatch.Upload(hotels);

    try
    {
        indexClient.Documents.Index(batch);
    }
    catch (IndexBatchException e)
    {
        // Sometimes when your Search service is under load, indexing will fail for some of the documents in
        // the batch. Depending on your application, you can take compensating actions like delaying and
        // retrying. For this simple demo, we just log the failed document keys and continue.
        Console.WriteLine(
            "Failed to index some of the documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

    Console.WriteLine("Waiting for documents to be indexed...\n");
    Thread.Sleep(2000);
}
```

<span data-ttu-id="dd5f7-191">Bu yöntem, dört bölümden oluşur.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-191">This method has four parts.</span></span> <span data-ttu-id="dd5f7-192">Bir dizi ilk oluşturur `Hotel` dizine karşıya yüklemek için giriş veri işlevi görecek nesneleri.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-192">The first creates an array of `Hotel` objects that will serve as our input data to upload to the index.</span></span> <span data-ttu-id="dd5f7-193">Bu veriler, kolaylık sağlamak için sabit kodlanmış ' dir.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-193">This data is hard-coded for simplicity.</span></span> <span data-ttu-id="dd5f7-194">Kendi uygulamanızda verilerinizi büyük olasılıkla bir SQL veritabanı gibi bir dış veri kaynağından gelecektir.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-194">In your own application, your data will likely come from an external data source such as a SQL database.</span></span>

<span data-ttu-id="dd5f7-195">İkinci bölümü oluşturur bir `IndexBatch` belgeleri içeren.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-195">The second part creates an `IndexBatch` containing the documents.</span></span> <span data-ttu-id="dd5f7-196">Oluşturduğunuz, bu durumda çağırarak zaman toplu uygulamak istediğiniz işlem belirtin `IndexBatch.Upload`.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-196">You specify the operation you want to apply to the batch at the time you create it, in this case by calling `IndexBatch.Upload`.</span></span> <span data-ttu-id="dd5f7-197">Toplu sonra Azure Search dizini tarafından yüklenen `Documents.Index` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-197">The batch is then uploaded to the Azure Search index by the `Documents.Index` method.</span></span>

> [!NOTE]
> <span data-ttu-id="dd5f7-198">Bu örnekte, biz yalnızca belgeleri karşıya yükleniyor.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-198">In this example, we are just uploading documents.</span></span> <span data-ttu-id="dd5f7-199">Varolan belgelere değişiklikleri birleştirmek veya belgeleri silmek istiyorsanız, çağırarak toplu işlemler oluşturabilirsiniz `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, veya `IndexBatch.Delete` yerine.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-199">If you wanted to merge changes into existing documents or delete documents, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete` instead.</span></span> <span data-ttu-id="dd5f7-200">Çağırarak farklı işlemlerini tek bir toplu işte karıştırabilirsiniz `IndexBatch.New`, bir koleksiyonunu alır `IndexAction` nesneleri, her biri bir belge üzerinde belirli bir işlemi gerçekleştirmek için Azure Search söyler.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-200">You can also mix different operations in a single batch by calling `IndexBatch.New`, which takes a collection of `IndexAction` objects, each of which tells Azure Search to perform a particular operation on a document.</span></span> <span data-ttu-id="dd5f7-201">Her oluşturabilirsiniz `IndexAction` gibi karşılık gelen yöntemini çağırarak kendi işlemi ile `IndexAction.Merge`, `IndexAction.Upload`ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-201">You can create each `IndexAction` with its own operation by calling the corresponding method such as `IndexAction.Merge`, `IndexAction.Upload`, and so on.</span></span>
> 
> 

<span data-ttu-id="dd5f7-202">Üçüncü bu yöntem dizin oluşturma için önemli bir hata durumunu işler bir catch bloğunun parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-202">The third part of this method is a catch block that handles an important error case for indexing.</span></span> <span data-ttu-id="dd5f7-203">Azure Search hizmetiniz toplu işlemdeki belgelerin bazılarına dizin oluşturmada başarısız olursa `Documents.Index` tarafından bir `IndexBatchException` oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-203">If your Azure Search service fails to index some of the documents in the batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="dd5f7-204">Bu durum, hizmetiniz ağır yük altındayken belgelere dizin oluşturuyorsanız oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-204">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="dd5f7-205">**Bu durumu, kodunuzda açık şekilde işlemenizi kesinlikle öneririz.**</span><span class="sxs-lookup"><span data-stu-id="dd5f7-205">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="dd5f7-206">Başarısız olan belgelere dizin oluşturmayı geciktirip sonra yeniden deneyebilir veya günlük tutup örneğin devam ettiği şekilde devam edebilir veya uygulamanızın veri tutarlılığı gereksinimlerine bağlı olarak başka bir şey yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-206">You can delay and then retry indexing the documents that failed, or you can log and continue like the sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

> [!NOTE]
> <span data-ttu-id="dd5f7-207">Kullanabileceğiniz `FindFailedActionsToRetry` yöntemi yalnızca bir önceki çağrılamadı eylemleri içeren yeni bir toplu iş oluşturmak için `Index`.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-207">You can use the `FindFailedActionsToRetry` method to construct a new batch containing only the actions that failed in a previous call to `Index`.</span></span> <span data-ttu-id="dd5f7-208">Yöntem belgelenen [burada](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) ve düzgün bir şekilde kullanma konusunda bir tartışma [StackOverflow üzerinde](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span><span class="sxs-lookup"><span data-stu-id="dd5f7-208">The method is documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) and there is a discussion of how to properly use it [on StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span></span>
>
>

<span data-ttu-id="dd5f7-209">Son olarak, `UploadDocuments` yöntemi gecikmeler iki saniye.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-209">Finally, the `UploadDocuments` method delays for two seconds.</span></span> <span data-ttu-id="dd5f7-210">Azure Search hizmetinizde dizin oluşturma uyumsuz şekilde meydana gelir; bu nedenle belgelerin aramada kullanılabilir olduğundan emin olmak için örnek uygulamanızın kısa bir süre beklemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-210">Indexing happens asynchronously in your Azure Search service, so the sample application needs to wait a short time to ensure that the documents are available for searching.</span></span> <span data-ttu-id="dd5f7-211">Bu gibi gecikmeler genellikle yalnızca gösterilerde, testlerde ve örnek uygulamalarda gereklidir.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-211">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

#### <a name="how-the-net-sdk-handles-documents"></a><span data-ttu-id="dd5f7-212">.NET SDK belgeleri nasıl işler?</span><span class="sxs-lookup"><span data-stu-id="dd5f7-212">How the .NET SDK handles documents</span></span>
<span data-ttu-id="dd5f7-213">Azure Search .NET SDK'sının `Hotel` gibi kullanıcı tanımlı bir sınıfın örneklerini dizine nasıl yükleyebildiğini merak ediyor olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-213">You may be wondering how the Azure Search .NET SDK is able to upload instances of a user-defined class like `Hotel` to the index.</span></span> <span data-ttu-id="dd5f7-214">Bu sorunun yanıtlanmasına yardımcı olmak için bakalım `Hotel` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="dd5f7-214">To help answer that question, let's look at the `Hotel` class:</span></span>

```csharp
using System;
using Microsoft.Azure.Search;
using Microsoft.Azure.Search.Models;
using Microsoft.Spatial;
using Newtonsoft.Json;

// The SerializePropertyNamesAsCamelCase attribute is defined in the Azure Search .NET SDK.
// It ensures that Pascal-case property names in the model class are mapped to camel-case
// field names in the index.
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

<span data-ttu-id="dd5f7-215">Fark edilecek ilk şey, `Hotel` öğesinin her bir genel özelliğinin dizin tanımındaki bir alana karşılık geldiği ancak çok önemli bir fark olduğudur: `Hotel` öğesinin her bir genel özelliğinin adı büyük harfle ("Pascal büyük/küçük harfi") başlarken her bir alanın adı küçük harfle ("ortası büyük harf") başlar.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-215">The first thing to notice is that each public property of `Hotel` corresponds to a field in the index definition, but with one crucial difference: The name of each field starts with a lower-case letter ("camel case"), while the name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="dd5f7-216">Bu durum, hedef şemanın uygulama geliştiricisinin denetimi dışında kaldığı bir veri bağlamayı gerçekleştiren .NET uygulamalarında ortak bir senaryodur.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-216">This is a common scenario in .NET applications that perform data-binding where the target schema is outside the control of the application developer.</span></span> <span data-ttu-id="dd5f7-217">Özellik adlarını ortası büyük harf yaparak .NET adlandırma yönergelerini bozmanın yerine, `[SerializePropertyNamesAsCamelCase]` özniteliğiyle SDK'nın özellik adlarını otomatik olarak ortası büyük harfle eşlenmesini söyleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-217">Rather than having to violate the .NET naming guidelines by making property names camel-case, you can tell the SDK to map the property names to camel-case automatically with the `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="dd5f7-218">Azure Search .NET SDK'sı, özel model nesnelerinizi JSON'a ve JSON'dan seri hale getirmek ve seri durumdan çıkarmak için [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) kitaplığını kullanır.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-218">The Azure Search .NET SDK uses the [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library to serialize and deserialize your custom model objects to and from JSON.</span></span> <span data-ttu-id="dd5f7-219">Gerekirse bu seri hale getirmeyi özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-219">You can customize this serialization if needed.</span></span> <span data-ttu-id="dd5f7-220">Daha fazla ayrıntı için bkz: [JSON.NET ile özel serileştirme](#JsonDotNet).</span><span class="sxs-lookup"><span data-stu-id="dd5f7-220">For more details, see [Custom Serialization with JSON.NET](#JsonDotNet).</span></span>
> 
> 

<span data-ttu-id="dd5f7-221">Fark edilecek ikinci şeydir öznitelikleri gibi `IsFilterable`, `IsSearchable`, `Key`, ve `Analyzer` her ortak özelliği tasarlamanız.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-221">The second thing to notice are the attributes such as `IsFilterable`, `IsSearchable`, `Key`, and `Analyzer` that decorate each public property.</span></span> <span data-ttu-id="dd5f7-222">Bu öznitelikler doğrudan eşleme [Azure Search dizini karşılık gelen özniteliklerini](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span><span class="sxs-lookup"><span data-stu-id="dd5f7-222">These attributes map directly to the [corresponding attributes of the Azure Search index](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span></span> <span data-ttu-id="dd5f7-223">`FieldBuilder` Sınıfı dizini için alan tanımlarını oluşturmak için bunları kullanır.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-223">The `FieldBuilder` class uses these to construct field definitions for the index.</span></span>

<span data-ttu-id="dd5f7-224">Üçüncü önemli şey hakkında `Hotel` sınıfı genel özelliklerin veri türleridir.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-224">The third important thing about the `Hotel` class are the data types of the public properties.</span></span> <span data-ttu-id="dd5f7-225">Bu özelliklerin .NET türleri dizin tanımında eşdeğer alan türleriyle eşlenir.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-225">The .NET types of  these properties map to their equivalent field types in the index definition.</span></span> <span data-ttu-id="dd5f7-226">Örneğin, `Category` dize özelliği `Edm.String` türündeki `category` alanına eşlenir.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-226">For example, the `Category` string property maps to the `category` field, which is of type `Edm.String`.</span></span> <span data-ttu-id="dd5f7-227">`bool?` ve `Edm.Boolean`, `DateTimeOffset?` ve `Edm.DateTimeOffset`, vb. arasında benzer türde eşlemeler bulunur. Tür eşlemesine yönelik belirli kurallar, [Azure Search .NET SDK başvurusundaki](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_) `Documents.Get` yönteminde belirtilmiştir.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-227">There are similar type mappings between `bool?` and `Edm.Boolean`, `DateTimeOffset?` and `Edm.DateTimeOffset`, etc. The specific rules for the type mapping are documented with the `Documents.Get` method in the [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span> <span data-ttu-id="dd5f7-228">`FieldBuilder` Sınıfı, bu eşlemeyi mvc'deki ancak hala serileştirme sorunları gidermek gerektiğinde anlamak yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-228">The `FieldBuilder` class takes care of this mapping for you, but it can still be helpful to understand in case you need to troubleshoot any serialization issues.</span></span>

<span data-ttu-id="dd5f7-229">Kendi sınıflarınızı belge olarak kullanabilme iki yönde de işe yarar; Ayrıca, arama sonuçları almak ve biz sonraki bölümde göreceğiniz gibi otomatik olarak onları tercih ettiğiniz bir türe seri durumdan SDK'sına sahip.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-229">This ability to use your own classes as documents works in both directions; You can also retrieve search results and have the SDK automatically deserialize them to a type of your choice, as we will see in the next section.</span></span>

> [!NOTE]
> <span data-ttu-id="dd5f7-230">Azure Search .NET SDK'sı, alan adlarını alan değerlerine bir anahtar/değer eşlemesi olan `Document` sınıfını kullanarak dinamik tür belirtilmiş belgeleri de destekler.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-230">The Azure Search .NET SDK also supports dynamically-typed documents using the `Document` class, which is a key/value mapping of field names to field values.</span></span> <span data-ttu-id="dd5f7-231">Bu durum, tasarım sırasında dizin şemasını bilmediğiniz veya belirli model sınıflarına bağlamanın kullanışlı olmayacağı senaryolarda kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-231">This is useful in scenarios where you don't know the index schema at design-time, or where it would be inconvenient to bind to specific model classes.</span></span> <span data-ttu-id="dd5f7-232">SDK'da belgelerle ilgili tüm yöntemler, `Document` sınıfıyla çalışan aşırı yüklerin yanı sıra genel türde bir parametre alan kesin tür belirtilmiş aşırı yüklere de sahiptir.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-232">All the methods in the SDK that deal with documents have overloads that work with the `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="dd5f7-233">Örnek kodda yalnızca ikinci Bu öğreticide kullanılır.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-233">Only the latter are used in the sample code in this tutorial.</span></span> <span data-ttu-id="dd5f7-234">`Document` Sınıfının devraldığı `Dictionary<string, object>`.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-234">The `Document` class inherits from `Dictionary<string, object>`.</span></span> <span data-ttu-id="dd5f7-235">Diğer ayrıntıları bulmak [burada](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span><span class="sxs-lookup"><span data-stu-id="dd5f7-235">You can find other details [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span></span>
> 
> 

<span data-ttu-id="dd5f7-236">**Neden boş değer atanabilir türleri kullanmalısınız?**</span><span class="sxs-lookup"><span data-stu-id="dd5f7-236">**Why you should use nullable data types**</span></span>

<span data-ttu-id="dd5f7-237">Bir Azure Search dizinine eşlemek için yeni model sınıflarınızı tasarlarken, `bool` ve `int` gibi değer türü özelliklerinin boş değer atanabilir (örneğin, `bool` yerine `bool?`) şeklinde bildirilmesini öneririz.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-237">When designing your own model classes to map to an Azure Search index, we recommend declaring properties of value types such as `bool` and `int` to be nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="dd5f7-238">Boş değer atanamayan bir özellik kullanırsanız buna karşılık gelen alan için dizininizdeki hiçbir belgenin boş bir değer içermediğini **garanti etmeniz** gerekir.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-238">If you use a non-nullable property, you have to **guarantee** that no documents in your index contain a null value for the corresponding field.</span></span> <span data-ttu-id="dd5f7-239">Bunu zorlamanıza ne SDK ne de Azure Search hizmeti yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-239">Neither the SDK nor the Azure Search service will help you to enforce this.</span></span>

<span data-ttu-id="dd5f7-240">Bu yalnızca kuramsal bir sorun değildir: Var olan `Edm.Int32` türünde bir dizine yeni bir alan eklediğiniz bir senaryoyu düşünün.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-240">This is not just a hypothetical concern: Imagine a scenario where you add a new field to an existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="dd5f7-241">Dizin tanımını güncelleştirdikten sonra, tüm belgelerin bu yeni alan için boş bir değeri olur (bunun nedeni, Azure Search'te tüm türlerin boş değer atanabilir olmasıdır).</span><span class="sxs-lookup"><span data-stu-id="dd5f7-241">After updating the index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="dd5f7-242">Ardından bu alan için boş değer atanamayan bir `int` özelliğiyle bir model sınıfı kullanırsanız belgeleri almaya çalışırken bunun gibi bir `JsonSerializationException` alırsınız:</span><span class="sxs-lookup"><span data-stu-id="dd5f7-242">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying to retrieve documents:</span></span>

    Error converting value {null} to type 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="dd5f7-243">Bu nedenle, en iyi uygulama olarak model sınıflarınızda boş değer atanabilir türler kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-243">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

<a name="JsonDotNet"></a>

#### <a name="custom-serialization-with-jsonnet"></a><span data-ttu-id="dd5f7-244">JSON.NET ile özel seri hale getirme</span><span class="sxs-lookup"><span data-stu-id="dd5f7-244">Custom Serialization with JSON.NET</span></span>
<span data-ttu-id="dd5f7-245">SDK'sı, seri hale getirme ve belgeleri seri durumdan çıkarmak için JSON.NET kullanır.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-245">The SDK uses JSON.NET for serializing and deserializing documents.</span></span> <span data-ttu-id="dd5f7-246">Seri hale getirme özelleştirebilir ve tanımlayarak, kendi gerekirse seri durumundan çıkarma `JsonConverter` veya `IContractResolver` (bkz [JSON.NET belgelerine](http://www.newtonsoft.com/json/help/html/Introduction.htm) daha fazla ayrıntı için).</span><span class="sxs-lookup"><span data-stu-id="dd5f7-246">You can customize serialization and deserialization if needed by defining your own `JsonConverter` or `IContractResolver` (see the [JSON.NET documentation](http://www.newtonsoft.com/json/help/html/Introduction.htm) for more details).</span></span> <span data-ttu-id="dd5f7-247">Uygulamanız Azure Search ve diğer daha Gelişmiş senaryolar ile kullanmak için mevcut bir model sınıfın uyum istediğinizde bu yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-247">This can be useful when you want to adapt an existing model class from your application for use with Azure Search, and other more advanced scenarios.</span></span> <span data-ttu-id="dd5f7-248">Örneğin, özel serileştirme ile şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="dd5f7-248">For example, with custom serialization you can:</span></span>

* <span data-ttu-id="dd5f7-249">İçerebilir veya belge alanlar olarak depolanan belirli özellikleri modeli sınıfınızın dışlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-249">Include or exclude certain properties of your model class from being stored as document fields.</span></span>
* <span data-ttu-id="dd5f7-250">Kodunuzda özellik adları ve alan adları, dizininizdeki arasında eşleyin.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-250">Map between property names in your code and field names in your index.</span></span>
* <span data-ttu-id="dd5f7-251">Belge alanları özellikleri eşlemek için kullanılan özel öznitelikler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-251">Create custom attributes that can be used for mapping properties to document fields.</span></span>

<span data-ttu-id="dd5f7-252">Github'daki Azure Search .NET SDK'sı için birim testleri özel serileştirme uygulamanın örnekleri bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-252">You can find examples of implementing custom serialization in the unit tests for the Azure Search .NET SDK on GitHub.</span></span> <span data-ttu-id="dd5f7-253">İyi bir başlangıç noktasıdır [bu klasör](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models).</span><span class="sxs-lookup"><span data-stu-id="dd5f7-253">A good starting point is [this folder](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models).</span></span> <span data-ttu-id="dd5f7-254">Özel serileştirme testleri tarafından kullanılan sınıfları içerir.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-254">It contains classes that are used by the custom serialization tests.</span></span>

### <a name="searching-for-documents-in-the-index"></a><span data-ttu-id="dd5f7-255">Dizin belgelerde arama</span><span class="sxs-lookup"><span data-stu-id="dd5f7-255">Searching for documents in the index</span></span>
<span data-ttu-id="dd5f7-256">Son örnek uygulama dizinindeki bazı belgeleri aramak için adımdır.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-256">The last step in the sample application is to search for some documents in the index.</span></span> <span data-ttu-id="dd5f7-257">Aşağıdaki yöntem bunu yapar:</span><span class="sxs-lookup"><span data-stu-id="dd5f7-257">The following method does this:</span></span>

```csharp
private static void RunQueries(ISearchIndexClient indexClient)
{
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
}
```

<span data-ttu-id="dd5f7-258">Her bir sorgu yürütülmeden, bu yöntem önce yeni bir oluşturur `SearchParameters` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-258">Each time it executes a query, this method first creates a new `SearchParameters` object.</span></span> <span data-ttu-id="dd5f7-259">Bu, sıralama, filtreleme, disk belleği ve olduğunu gibi bir sorgu için ek seçenekleri belirtmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-259">This is used to specify additional options for the query such as sorting, filtering, paging, and faceting.</span></span> <span data-ttu-id="dd5f7-260">Bu yöntemde, biz ayarladığınız `Filter`, `Select`, `OrderBy`, ve `Top` özelliği için farklı sorgular.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-260">In this method, we're setting the `Filter`, `Select`, `OrderBy`, and `Top` property for different queries.</span></span> <span data-ttu-id="dd5f7-261">Tüm `SearchParameters` özellikleri belgelenmiştir [burada](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span><span class="sxs-lookup"><span data-stu-id="dd5f7-261">All the `SearchParameters` properties are documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span></span>

<span data-ttu-id="dd5f7-262">Gerçekte arama sorguyu yürütmek için sonraki adımdır bakın.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-262">The next step is to actually execute the search query.</span></span> <span data-ttu-id="dd5f7-263">Bu yapılır kullanarak `Documents.Search` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-263">This is done using the `Documents.Search` method.</span></span> <span data-ttu-id="dd5f7-264">Her sorgu için size bir dize olarak kullanmak için arama metni geçirin (veya `"*"` arama metni ise), daha önce oluşturduğunuz arama parametrelerini artı.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-264">For each query, we pass the search text to use as a string (or `"*"` if there is no search text), plus the search parameters created earlier.</span></span> <span data-ttu-id="dd5f7-265">Biz de belirtmeniz `Hotel` türü parametre olarak `Documents.Search`, SDK'sını belgeleri arama sonuçlarında türündeki nesneleri seri durumdan söyler `Hotel`.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-265">We also specify `Hotel` as the type parameter for `Documents.Search`, which tells the SDK to deserialize documents in the search results into objects of type `Hotel`.</span></span>

> [!NOTE]
> <span data-ttu-id="dd5f7-266">Arama sorgu ifade sözdizimi hakkında daha fazla bilgi bulabilirsiniz [burada](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="dd5f7-266">You can find more information about the search query expression syntax [here](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span></span>
> 
> 

<span data-ttu-id="dd5f7-267">Son olarak, her sorgu sonra bu yöntem her belge konsola yazdırma tüm eşleşmeleri arama sonuçlarında dolaşır:</span><span class="sxs-lookup"><span data-stu-id="dd5f7-267">Finally, after each query this method iterates through all the matches in the search results, printing each document to the console:</span></span>

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

<span data-ttu-id="dd5f7-268">Buna karşılık her sorguları daha yakın bir göz atalım.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-268">Let's take a closer look at each of the queries in turn.</span></span> <span data-ttu-id="dd5f7-269">İlk sorguyu yürütmek için kod aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="dd5f7-269">Here is the code to execute the first query:</span></span>

```csharp
parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);
```

<span data-ttu-id="dd5f7-270">Bu durumda, "Bütçe" sözcüğü Eşleştir Oteller için arama yapıyorsanız ve yalnızca otel adlar, belirtilen şekilde geri dönmek istiyoruz `Select` parametresi.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-270">In this case, we're searching for hotels that match the word "budget", and we want to get back only the hotel names, as specified by the `Select` parameter.</span></span> <span data-ttu-id="dd5f7-271">Sonuçları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="dd5f7-271">Here are the results:</span></span>

    Name: Roach Motel

<span data-ttu-id="dd5f7-272">Ardından, değerinden 150 ABD dolarını gecelik oranı ile Oteller bulmak ve yalnızca otel kimliği ve açıklama dönmek istiyoruz:</span><span class="sxs-lookup"><span data-stu-id="dd5f7-272">Next, we want to find the hotels with a nightly rate of less than $150, and return only the hotel ID and description:</span></span>

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

<span data-ttu-id="dd5f7-273">Bu sorgu bir OData kullanan `$filter` ifadesi, `baseRate lt 150`, dizin belgelerde filtrelemek için.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-273">This query uses an OData `$filter` expression, `baseRate lt 150`, to filter the documents in the index.</span></span> <span data-ttu-id="dd5f7-274">Azure Search destekleyen OData söz dizimi hakkında daha fazla bilgi bulabilirsiniz [burada](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="dd5f7-274">You can find out more about the OData syntax that Azure Search supports [here](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span></span>

<span data-ttu-id="dd5f7-275">Sorgu sonuçlarını şunlardır:</span><span class="sxs-lookup"><span data-stu-id="dd5f7-275">Here are the results of the query:</span></span>

    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close to town hall and the river

<span data-ttu-id="dd5f7-276">Ardından, en son renovated üst iki Oteller bulmak ve Otel adı ve son Yenileme tarihi göstermek istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-276">Next, we want to find the top two hotels that have been most recently renovated, and show the hotel name and last renovation date.</span></span> <span data-ttu-id="dd5f7-277">Kod aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="dd5f7-277">Here is the code:</span></span> 

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

<span data-ttu-id="dd5f7-278">Bu durumda, yeniden OData sözdizimi belirtmek için kullanıyoruz `OrderBy` parametre olarak `lastRenovationDate desc`.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-278">In this case, we again use OData syntax to specify the `OrderBy` parameter as `lastRenovationDate desc`.</span></span> <span data-ttu-id="dd5f7-279">Ayrıca `Top` biz yalnızca get üstteki iki belgeleri emin olmak için 2.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-279">We also set `Top` to 2 to ensure we only get the top two documents.</span></span> <span data-ttu-id="dd5f7-280">Önce ayarlar gibi `Select` hangi alanların döndürülmesi gerektiğini belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-280">As before, we set `Select` to specify which fields should be returned.</span></span>

<span data-ttu-id="dd5f7-281">Sonuçları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="dd5f7-281">Here are the results:</span></span>

    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

<span data-ttu-id="dd5f7-282">Son olarak, biz "motel" word eşleşen tüm Oteller bulmak istediğiniz:</span><span class="sxs-lookup"><span data-stu-id="dd5f7-282">Finally, we want to find all hotels that match the word "motel":</span></span>

```csharp
parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

<span data-ttu-id="dd5f7-283">Ve biz belirtmemek olduğundan, tüm alanları içeren aşağıdaki sonuçları `Select` özelliği:</span><span class="sxs-lookup"><span data-stu-id="dd5f7-283">And here are the results, which include all fields since we did not specify the `Select` property:</span></span>

    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577

<span data-ttu-id="dd5f7-284">Öğreticinin Bu adım tamamlandıktan, ancak burada Durdur yok.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-284">This step completes the tutorial, but don't stop here.</span></span> <span data-ttu-id="dd5f7-285">**Sonraki adımlar** Azure Search hakkında daha fazla bilgi için ek kaynaklar sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-285">**Next steps** provides additional resources for learning more about Azure Search.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd5f7-286">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="dd5f7-286">Next steps</span></span>
* <span data-ttu-id="dd5f7-287">[.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) ve [REST API](https://docs.microsoft.com/rest/api/searchservice/) başvurularına göz atın.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-287">Browse the references for the [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
* <span data-ttu-id="dd5f7-288">Bilginiz aracılığıyla deepen [videolar ve diğer örnekler ve öğreticiler](search-video-demo-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="dd5f7-288">Deepen your knowledge through [videos and other samples and tutorials](search-video-demo-tutorial-list.md).</span></span>
* <span data-ttu-id="dd5f7-289">Gözden geçirme [adlandırma kuralları](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) çeşitli nesneleri adlandırma kurallarını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-289">Review [naming conventions](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) to learn the rules for naming various objects.</span></span>
* <span data-ttu-id="dd5f7-290">Gözden geçirme [desteklenen veri türleri](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) Azure Search'te.</span><span class="sxs-lookup"><span data-stu-id="dd5f7-290">Review [supported data types](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) in Azure Search.</span></span>
