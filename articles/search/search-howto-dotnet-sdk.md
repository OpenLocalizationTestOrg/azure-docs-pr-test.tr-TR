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
# <a name="how-toouse-azure-search-from-a-net-application"></a><span data-ttu-id="f02ff-103">Bir .NET uygulamasından Azure toouse arama nasıl</span><span class="sxs-lookup"><span data-stu-id="f02ff-103">How toouse Azure Search from a .NET Application</span></span>
<span data-ttu-id="f02ff-104">Bu makalede bir gözden geçirme tooget olduğundan, hello ile çalışır [Azure Search .NET SDK'sı](https://aka.ms/search-sdk).</span><span class="sxs-lookup"><span data-stu-id="f02ff-104">This article is a walkthrough tooget you up and running with hello [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span> <span data-ttu-id="f02ff-105">Bir zengin hello .NET SDK'sı tooimplement kullanabileceğiniz Azure arama'yı kullanarak, uygulamanızda arama deneyimini.</span><span class="sxs-lookup"><span data-stu-id="f02ff-105">You can use hello .NET SDK tooimplement a rich search experience in your application using Azure Search.</span></span>

## <a name="whats-in-hello-azure-search-sdk"></a><span data-ttu-id="f02ff-106">Azure Search SDK hello nedir</span><span class="sxs-lookup"><span data-stu-id="f02ff-106">What's in hello Azure Search SDK</span></span>
<span data-ttu-id="f02ff-107">Merhaba SDK oluşan bir istemci Kitaplığı'nın `Microsoft.Azure.Search`.</span><span class="sxs-lookup"><span data-stu-id="f02ff-107">hello SDK consists of a client library, `Microsoft.Azure.Search`.</span></span> <span data-ttu-id="f02ff-108">Bu, toomanage dizinleri, veri kaynakları ve dizin oluşturucular, sağlar yanı sıra karşıya yükleme ve belgeleri yönetmek ve tüm HTTP ve JSON hello ayrıntılarla toodeal kalmadan sorgular yürütün.</span><span class="sxs-lookup"><span data-stu-id="f02ff-108">It enables you toomanage your indexes, data sources, and indexers, as well as upload and manage documents, and execute queries, all without having toodeal with hello details of HTTP and JSON.</span></span>

<span data-ttu-id="f02ff-109">Merhaba istemci kitaplığı gibi sınıflara tanımlar `Index`, `Field`, ve `Document`, yanı sıra operations ister `Indexes.Create` ve `Documents.Search` hello üzerinde `SearchServiceClient` ve `SearchIndexClient` sınıfları.</span><span class="sxs-lookup"><span data-stu-id="f02ff-109">hello client library defines classes like `Index`, `Field`, and `Document`, as well as operations like `Indexes.Create` and `Documents.Search` on hello `SearchServiceClient` and `SearchIndexClient` classes.</span></span> <span data-ttu-id="f02ff-110">Bu sınıfların ad alanları aşağıdaki hello düzenlenmiştir:</span><span class="sxs-lookup"><span data-stu-id="f02ff-110">These classes are organized into hello following namespaces:</span></span>

* [<span data-ttu-id="f02ff-111">Microsoft.Azure.Search</span><span class="sxs-lookup"><span data-stu-id="f02ff-111">Microsoft.Azure.Search</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)
* [<span data-ttu-id="f02ff-112">Microsoft.Azure.Search.Models</span><span class="sxs-lookup"><span data-stu-id="f02ff-112">Microsoft.Azure.Search.Models</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models)

<span data-ttu-id="f02ff-113">Merhaba geçerli sürümü hello Azure Search .NET SDK'sı, genellikle kullanıma sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="f02ff-113">hello current version of hello Azure Search .NET SDK is now generally available.</span></span> <span data-ttu-id="f02ff-114">Tooprovide geri bildirim isterseniz bize tooincorporate hello sonraki sürümünde, lütfen şu adresi ziyaret bizim [görüş sayfası](https://feedback.azure.com/forums/263029-azure-search/).</span><span class="sxs-lookup"><span data-stu-id="f02ff-114">If you would like tooprovide feedback for us tooincorporate in hello next version, please visit our [feedback page](https://feedback.azure.com/forums/263029-azure-search/).</span></span>

<span data-ttu-id="f02ff-115">Merhaba .NET SDK sürüm destekleyen `2016-09-01` Merhaba, [Azure Search REST API'sini](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="f02ff-115">hello .NET SDK supports version `2016-09-01` of hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span> <span data-ttu-id="f02ff-116">Bu sürümü artık özel Çözümleyicileri ve Azure Blob ve Azure Table dizin oluşturucu desteği içerir.</span><span class="sxs-lookup"><span data-stu-id="f02ff-116">This version now includes support for custom analyzers and Azure Blob and Azure Table indexer support.</span></span> <span data-ttu-id="f02ff-117">Önizleme özellikleri *değil* JSON ve CSV dosyalarını dizin oluşturma için destek gibi bu sürümü bir parçası olan [Önizleme](search-api-2015-02-28-preview.md) ve hello eski aracılığıyla kullanılabilen [hello .NET SDK 2.0-Önizleme sürümü ](https://aka.ms/search-sdk-preview).</span><span class="sxs-lookup"><span data-stu-id="f02ff-117">Preview features that are *not* part of this version, such as support for indexing JSON and CSV files, are in [preview](search-api-2015-02-28-preview.md) and available via hello older [2.0-preview version of hello .NET SDK](https://aka.ms/search-sdk-preview).</span></span>

<span data-ttu-id="f02ff-118">Bu SDK desteklemediği [yönetim işlemlerini](https://docs.microsoft.com/rest/api/searchmanagement/) oluşturma ve arama hizmetleri ölçekleme ve API anahtarlarını yönetme gibi.</span><span class="sxs-lookup"><span data-stu-id="f02ff-118">This SDK does not support [Management Operations](https://docs.microsoft.com/rest/api/searchmanagement/) such as creating and scaling Search services and managing API keys.</span></span> <span data-ttu-id="f02ff-119">.NET uygulaması arama kaynaklarınızdan toomanage gerekirse hello kullanabilirsiniz [Azure Search .NET Yönetim SDK](https://aka.ms/search-mgmt-sdk).</span><span class="sxs-lookup"><span data-stu-id="f02ff-119">If you need toomanage your Search resources from a .NET application, you can use hello [Azure Search .NET Management SDK](https://aka.ms/search-mgmt-sdk).</span></span>

## <a name="upgrading-toohello-latest-version-of-hello-sdk"></a><span data-ttu-id="f02ff-120">Merhaba SDK toohello en son sürümüne yükseltme</span><span class="sxs-lookup"><span data-stu-id="f02ff-120">Upgrading toohello latest version of hello SDK</span></span>
<span data-ttu-id="f02ff-121">Hello Azure Search .NET SDK'sı daha eski bir sürümü zaten kullanıyorsanız ve tooupgrade toohello yeni genel olarak kullanılabilir sürüm, istediğiniz [bu makalede](search-dotnet-sdk-migration.md) açıklar nasıl.</span><span class="sxs-lookup"><span data-stu-id="f02ff-121">If you're already using an older version of hello Azure Search .NET SDK and you'd like tooupgrade toohello new generally available version, [this article](search-dotnet-sdk-migration.md) explains how.</span></span>

## <a name="requirements-for-hello-sdk"></a><span data-ttu-id="f02ff-122">Merhaba SDK gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="f02ff-122">Requirements for hello SDK</span></span>
1. <span data-ttu-id="f02ff-123">Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="f02ff-123">Visual Studio 2017.</span></span>
2. <span data-ttu-id="f02ff-124">Kendi Azure Search hizmeti.</span><span class="sxs-lookup"><span data-stu-id="f02ff-124">Your own Azure Search service.</span></span> <span data-ttu-id="f02ff-125">Sipariş toouse hello SDK, hizmetinize hello adını ve bir veya daha fazla API anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="f02ff-125">In order toouse hello SDK, you will need hello name of your service and one or more API keys.</span></span> <span data-ttu-id="f02ff-126">[Merhaba Portalı'nda bir hizmet oluşturma](search-create-service-portal.md) bu adımları uygularken size yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="f02ff-126">[Create a service in hello portal](search-create-service-portal.md) will help you through these steps.</span></span>
3. <span data-ttu-id="f02ff-127">Hello Azure Search .NET SDK'sını indirin [NuGet paketi](http://www.nuget.org/packages/Microsoft.Azure.Search) "NuGet paketlerini Yönet" Visual Studio kullanarak.</span><span class="sxs-lookup"><span data-stu-id="f02ff-127">Download hello Azure Search .NET SDK [NuGet package](http://www.nuget.org/packages/Microsoft.Azure.Search) by using "Manage NuGet Packages" in Visual Studio.</span></span> <span data-ttu-id="f02ff-128">Merhaba paket adı için yalnızca arama `Microsoft.Azure.Search` NuGet.org üzerinde.</span><span class="sxs-lookup"><span data-stu-id="f02ff-128">Just search for hello package name `Microsoft.Azure.Search` on NuGet.org.</span></span>

<span data-ttu-id="f02ff-129">Hello Azure Search .NET SDK'sı hello .NET Framework 4.6 ve .NET Core hedefleyen uygulamaları destekler.</span><span class="sxs-lookup"><span data-stu-id="f02ff-129">hello Azure Search .NET SDK supports applications targeting hello .NET Framework 4.6 and .NET Core.</span></span>

## <a name="core-scenarios"></a><span data-ttu-id="f02ff-130">Temel senaryolar</span><span class="sxs-lookup"><span data-stu-id="f02ff-130">Core scenarios</span></span>
<span data-ttu-id="f02ff-131">Arama uygulamanızda toodo gerekir birkaç şey vardır.</span><span class="sxs-lookup"><span data-stu-id="f02ff-131">There are several things you'll need toodo in your search application.</span></span> <span data-ttu-id="f02ff-132">Bu öğreticide, bu temel senaryolar şu konulara değineceğiz:</span><span class="sxs-lookup"><span data-stu-id="f02ff-132">In this tutorial, we'll cover these core scenarios:</span></span>

* <span data-ttu-id="f02ff-133">Dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="f02ff-133">Creating an index</span></span>
* <span data-ttu-id="f02ff-134">Belgelerle Hello dizin doldurma</span><span class="sxs-lookup"><span data-stu-id="f02ff-134">Populating hello index with documents</span></span>
* <span data-ttu-id="f02ff-135">Tam metin araması ve filtreleri kullanarak belgeleri için arama</span><span class="sxs-lookup"><span data-stu-id="f02ff-135">Searching for documents using full-text search and filters</span></span>

<span data-ttu-id="f02ff-136">Aşağıdaki örnek kod hello her birinde gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f02ff-136">hello sample code that follows illustrates each of these.</span></span> <span data-ttu-id="f02ff-137">Ücretsiz toouse hello kod parçacıkları, kendi uygulamanızda eşitleyerek.</span><span class="sxs-lookup"><span data-stu-id="f02ff-137">Feel free toouse hello code snippets in your own application.</span></span>

### <a name="overview"></a><span data-ttu-id="f02ff-138">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="f02ff-138">Overview</span></span>
<span data-ttu-id="f02ff-139">Merhaba biz keşfetme örnek uygulamayı yeni bir oluşturur "hotels" adlı dizin birkaç belgelerle doldurur sonra bazı arama sorguları yürütür.</span><span class="sxs-lookup"><span data-stu-id="f02ff-139">hello sample application we'll be exploring creates a new index named "hotels", populates it with a few documents, then executes some search queries.</span></span> <span data-ttu-id="f02ff-140">Gösteren hello ana program İşte hello genel akış:</span><span class="sxs-lookup"><span data-stu-id="f02ff-140">Here is hello main program, showing hello overall flow:</span></span>

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
> <span data-ttu-id="f02ff-141">Merhaba örnek uygulaması bu ilerlemesi üzerinde kullanılan hello tam kaynak kodunu bulabilirsiniz [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="f02ff-141">You can find hello full source code of hello sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>
> 
>

<span data-ttu-id="f02ff-142">Biz bu adım adım adım geçireceğiz.</span><span class="sxs-lookup"><span data-stu-id="f02ff-142">We'll walk through this step by step.</span></span> <span data-ttu-id="f02ff-143">Yeni bir toocreate ilk ihtiyacımız `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="f02ff-143">First we need toocreate a new `SearchServiceClient`.</span></span> <span data-ttu-id="f02ff-144">Bu nesne toomanage dizinleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="f02ff-144">This object allows you toomanage indexes.</span></span> <span data-ttu-id="f02ff-145">Sipariş tooconstruct içinde biri, bir yönetici API anahtarı yanı sıra Azure Search hizmet adınızı tooprovide gerekir.</span><span class="sxs-lookup"><span data-stu-id="f02ff-145">In order tooconstruct one, you need tooprovide your Azure Search service name as well as an admin API key.</span></span> <span data-ttu-id="f02ff-146">Bu bilgiler hello girebilirsiniz `appsettings.json` hello dosyasının [örnek uygulama](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="f02ff-146">You can enter this information in hello `appsettings.json` file of hello [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

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
> <span data-ttu-id="f02ff-147">Yanlış bir anahtar (burada bir yönetici anahtarı gerekli Örneğin, bir sorgu anahtarı) sağlarsanız, hello `SearchServiceClient` özel durum oluşturacak bir `CloudException` hello hata iletisi "Yasak" Merhaba ile ilk kez, bir işlemi yöntemi üzerinde aşağıdaki gibi çağrısından `Indexes.Create`.</span><span class="sxs-lookup"><span data-stu-id="f02ff-147">If you provide an incorrect key (for example, a query key where an admin key was required), hello `SearchServiceClient` will throw a `CloudException` with hello error message "Forbidden" hello first time you call an operation method on it, such as `Indexes.Create`.</span></span> <span data-ttu-id="f02ff-148">Bu tooyou olursa, bizim API anahtarı denetleyin.</span><span class="sxs-lookup"><span data-stu-id="f02ff-148">If this happens tooyou, double-check our API key.</span></span>
> 
> 

<span data-ttu-id="f02ff-149">Merhaba sonraki birkaç satır yöntemleri toocreate "hotels" zaten varsa, ilk silme, adında bir dizini arayın.</span><span class="sxs-lookup"><span data-stu-id="f02ff-149">hello next few lines call methods toocreate an index named "hotels", deleting it first if it already exists.</span></span> <span data-ttu-id="f02ff-150">Biz bu yöntemlerle biraz daha sonra yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="f02ff-150">We will walk through these methods a little later.</span></span>

```csharp
Console.WriteLine("{0}", "Deleting index...\n");
DeleteHotelsIndexIfExists(serviceClient);

Console.WriteLine("{0}", "Creating index...\n");
CreateHotelsIndex(serviceClient);
```

<span data-ttu-id="f02ff-151">Ardından, başlangıç dizini doldurulmuş toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="f02ff-151">Next, hello index needs toobe populated.</span></span> <span data-ttu-id="f02ff-152">toodo bunu ihtiyacımız bir `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="f02ff-152">toodo this, we will need a `SearchIndexClient`.</span></span> <span data-ttu-id="f02ff-153">İki yolu tooobtain biri vardır: onu oluşturmak ya da çağırma `Indexes.GetClient` hello üzerinde `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="f02ff-153">There are two ways tooobtain one: by constructing it, or by calling `Indexes.GetClient` on hello `SearchServiceClient`.</span></span> <span data-ttu-id="f02ff-154">Merhaba ikinci kolaylık sağlamak için kullanırız.</span><span class="sxs-lookup"><span data-stu-id="f02ff-154">We use hello latter for convenience.</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="f02ff-155">Genel bir arama uygulamasında, dizin yönetimi ve popülasyon, arama sorgularından ayrı bir bileşen tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="f02ff-155">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="f02ff-156">`Indexes.GetClient`kaydettiğinden bir dizini doldurmada kullanışlıdır hello başka sağlama sorun `SearchCredentials`.</span><span class="sxs-lookup"><span data-stu-id="f02ff-156">`Indexes.GetClient` is convenient for populating an index because it saves you hello trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="f02ff-157">Bunu Bu, kullanılan toocreate hello hello yönetici anahtarını geçirerek yapar `SearchServiceClient` toohello yeni `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="f02ff-157">It does this by passing hello admin key that you used toocreate hello `SearchServiceClient` toohello new `SearchIndexClient`.</span></span> <span data-ttu-id="f02ff-158">Ancak, uygulamanızın sorguları yürüten hello bölümünde daha iyi toocreate hello olmasından `SearchIndexClient` doğrudan böylece bir yönetici anahtarı yerine sorgu anahtarında geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f02ff-158">However, in hello part of your application that executes queries, it is better toocreate hello `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="f02ff-159">Bu en az ayrıcalık prensibi hello ile tutarlı ve uygulamanızı daha güvenli toomake yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="f02ff-159">This is consistent with hello principle of least privilege and will help toomake your application more secure.</span></span> <span data-ttu-id="f02ff-160">Yönetici anahtarları ve sorgu anahtarları hakkında daha fazla bilgi için [burada](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span><span class="sxs-lookup"><span data-stu-id="f02ff-160">You can find out more about admin keys and query keys [here](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span></span>
> 
> 

<span data-ttu-id="f02ff-161">Biz sahip olduğunuza göre bir `SearchIndexClient`, biz hello dizin doldurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f02ff-161">Now that we have a `SearchIndexClient`, we can populate hello index.</span></span> <span data-ttu-id="f02ff-162">Bu size daha sonra size yol gösterir başka bir yöntem kullanarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="f02ff-162">This is done by another method that we will walk through later.</span></span>

```csharp
Console.WriteLine("{0}", "Uploading documents...\n");
UploadDocuments(indexClient);
```

<span data-ttu-id="f02ff-163">Son olarak, biz birkaç arama sorguları yürütmek ve hello sonuçları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="f02ff-163">Finally, we execute a few search queries and display hello results.</span></span> <span data-ttu-id="f02ff-164">Bu süre kullanırız farklı bir `SearchIndexClient`:</span><span class="sxs-lookup"><span data-stu-id="f02ff-164">This time we use a different `SearchIndexClient`:</span></span>

```csharp
ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

RunQueries(indexClientForQueries);
```

<span data-ttu-id="f02ff-165">Biz hello yakından sürer `RunQueries` daha sonra yöntemi.</span><span class="sxs-lookup"><span data-stu-id="f02ff-165">We will take a closer look at hello `RunQueries` method later.</span></span> <span data-ttu-id="f02ff-166">Yeni hello kod toocreate hello işte `SearchIndexClient`:</span><span class="sxs-lookup"><span data-stu-id="f02ff-166">Here is hello code toocreate hello new `SearchIndexClient`:</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="f02ff-167">Bu süre yazma erişimi toohello dizin gerekmez bu yana bir sorgu anahtarı kullanırız.</span><span class="sxs-lookup"><span data-stu-id="f02ff-167">This time we use a query key since we do not need write access toohello index.</span></span> <span data-ttu-id="f02ff-168">Bu bilgiler hello girebilirsiniz `appsettings.json` hello dosyasının [örnek uygulama](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="f02ff-168">You can enter this information in hello `appsettings.json` file of hello [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

<span data-ttu-id="f02ff-169">Bu uygulamayı geçerli bir hizmet adı ve API anahtarlarını çalıştırırsanız hello çıktı aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="f02ff-169">If you run this application with a valid service name and API keys, hello output should look like this:</span></span>

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

<span data-ttu-id="f02ff-170">Merhaba uygulaması Hello tam kaynak kodunu hello bu makalenin sonundaki sağlanır.</span><span class="sxs-lookup"><span data-stu-id="f02ff-170">hello full source code of hello application is provided at hello end of this article.</span></span>

<span data-ttu-id="f02ff-171">Ardından, biz tarafından çağrılır hello yöntemlerin her biri daha ayrıntılı bir bakış sürer `Main`.</span><span class="sxs-lookup"><span data-stu-id="f02ff-171">Next, we will take a closer look at each of hello methods called by `Main`.</span></span>

### <a name="creating-an-index"></a><span data-ttu-id="f02ff-172">Dizin oluşturma</span><span class="sxs-lookup"><span data-stu-id="f02ff-172">Creating an index</span></span>
<span data-ttu-id="f02ff-173">Oluşturduktan sonra bir `SearchServiceClient`, hello sonraki şey `Main` mu zaten delete hello "hotels" dizininin ise.</span><span class="sxs-lookup"><span data-stu-id="f02ff-173">After creating a `SearchServiceClient`, hello next thing `Main` does is delete hello "hotels" index if it already exists.</span></span> <span data-ttu-id="f02ff-174">Bu yöntemi aşağıdaki hello tarafından gerçekleştirilir:</span><span class="sxs-lookup"><span data-stu-id="f02ff-174">That is done by hello following method:</span></span>

```csharp
private static void DeleteHotelsIndexIfExists(SearchServiceClient serviceClient)
{
    if (serviceClient.Indexes.Exists("hotels"))
    {
        serviceClient.Indexes.Delete("hotels");
    }
}
```

<span data-ttu-id="f02ff-175">Bu yöntem verilen hello kullanır `SearchServiceClient` toocheck hello dizin varsa ve bu durumda, silin.</span><span class="sxs-lookup"><span data-stu-id="f02ff-175">This method uses hello given `SearchServiceClient` toocheck if hello index exists, and if so, delete it.</span></span>

> [!NOTE]
> <span data-ttu-id="f02ff-176">Bu makaledeki örnek kod Hello hello Azure Search .NET SDK'sı zaman uyumlu yöntemleri hello kolaylık sağlamak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="f02ff-176">hello example code in this article uses hello synchronous methods of hello Azure Search .NET SDK for simplicity.</span></span> <span data-ttu-id="f02ff-177">Kendi uygulamaları tookeep hello zaman uyumsuz yöntemleri kullanmanızı öneririz bunları ölçeklenebilir ve esnek.</span><span class="sxs-lookup"><span data-stu-id="f02ff-177">We recommend that you use hello asynchronous methods in your own applications tookeep them scalable and responsive.</span></span> <span data-ttu-id="f02ff-178">Örneğin, yukarıdaki yöntemi hello kullanabilirsiniz `ExistsAsync` ve `DeleteAsync` yerine `Exists` ve `Delete`.</span><span class="sxs-lookup"><span data-stu-id="f02ff-178">For example, in hello method above you could use `ExistsAsync` and `DeleteAsync` instead of `Exists` and `Delete`.</span></span>
> 
> 

<span data-ttu-id="f02ff-179">Ardından, `Main` bu yöntemini çağırarak yeni bir "hotels" dizini oluşturur:</span><span class="sxs-lookup"><span data-stu-id="f02ff-179">Next, `Main` creates a new "hotels" index by calling this method:</span></span>

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

<span data-ttu-id="f02ff-180">Bu yöntem yeni bir oluşturur `Index` listesini nesnesiyle `Field` hello yeni dizin hello şemasını tanımlayan nesneleri.</span><span class="sxs-lookup"><span data-stu-id="f02ff-180">This method creates a new `Index` object with a list of `Field` objects that defines hello schema of hello new index.</span></span> <span data-ttu-id="f02ff-181">Her alanın bir adı, veri türü ve arama davranışını tanımlamak birkaç öznitelik vardır.</span><span class="sxs-lookup"><span data-stu-id="f02ff-181">Each field has a name, data type, and several attributes that define its search behavior.</span></span> <span data-ttu-id="f02ff-182">Merhaba `FieldBuilder` sınıfını kullanır yansıma toocreate listesini `Field` nesneleri inceleniyor tarafından hello dizin için genel özellikleri ve verilen hello özniteliklerini hello `Hotel` model sınıfı.</span><span class="sxs-lookup"><span data-stu-id="f02ff-182">hello `FieldBuilder` class uses reflection toocreate a list of `Field` objects for hello index by examining hello public properties and attributes of hello given `Hotel` model class.</span></span> <span data-ttu-id="f02ff-183">Biz hello yakından gitmek `Hotel` daha sonra sınıfı.</span><span class="sxs-lookup"><span data-stu-id="f02ff-183">We'll take a closer look at hello `Hotel` class later on.</span></span>

> [!NOTE]
> <span data-ttu-id="f02ff-184">Merhaba listesini her zaman oluşturabilirsiniz `Field` kullanmak yerine doğrudan nesneleri `FieldBuilder` gerekiyorsa.</span><span class="sxs-lookup"><span data-stu-id="f02ff-184">You can always create hello list of `Field` objects directly instead of using `FieldBuilder` if needed.</span></span> <span data-ttu-id="f02ff-185">Örneğin, bir model sınıfı toouse istemeyebilirsiniz veya toouse toomodify öznitelikleri ekleyerek istemediğiniz varolan bir model sınıfı gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="f02ff-185">For example, you may not want toouse a model class or you may need toouse an existing model class that you don't want toomodify by adding attributes.</span></span>
>
> 

<span data-ttu-id="f02ff-186">Ayrıca toofields, ayrıca Puanlama profilleri, ilgili veya CORS seçenekleri toohello (bunlar kısaltma hello örnekten göz ardı edilir) dizini ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f02ff-186">In addition toofields, you can also add scoring profiles, suggesters, or CORS options toohello Index (these are omitted from hello sample for brevity).</span></span> <span data-ttu-id="f02ff-187">Hello hello dizin nesnesi ve onun bağlı bölümleri hakkında daha fazla bilgi bulabilirsiniz [SDK başvurusu](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), hello gibi yanı [Azure Search REST API Başvurusu](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="f02ff-187">You can find more information about hello Index object and its constituent parts in hello [SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), as well as in hello [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

### <a name="populating-hello-index"></a><span data-ttu-id="f02ff-188">Merhaba dizin doldurma</span><span class="sxs-lookup"><span data-stu-id="f02ff-188">Populating hello index</span></span>
<span data-ttu-id="f02ff-189">Merhaba sonraki adımda `Main` toopopulate hello yeni oluşturulan dizinidir.</span><span class="sxs-lookup"><span data-stu-id="f02ff-189">hello next step in `Main` is toopopulate hello newly-created index.</span></span> <span data-ttu-id="f02ff-190">Bu yöntemi aşağıdaki hello gerçekleştirilir:</span><span class="sxs-lookup"><span data-stu-id="f02ff-190">This is done in hello following method:</span></span>

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

<span data-ttu-id="f02ff-191">Bu yöntem, dört bölümden oluşur.</span><span class="sxs-lookup"><span data-stu-id="f02ff-191">This method has four parts.</span></span> <span data-ttu-id="f02ff-192">Merhaba ilk olarak bir dizi oluşturur `Hotel` giriş verisi tooupload toohello dizinimizi hizmet verecektir nesneleri.</span><span class="sxs-lookup"><span data-stu-id="f02ff-192">hello first creates an array of `Hotel` objects that will serve as our input data tooupload toohello index.</span></span> <span data-ttu-id="f02ff-193">Bu veriler, kolaylık sağlamak için sabit kodlanmış ' dir.</span><span class="sxs-lookup"><span data-stu-id="f02ff-193">This data is hard-coded for simplicity.</span></span> <span data-ttu-id="f02ff-194">Kendi uygulamanızda verilerinizi büyük olasılıkla bir SQL veritabanı gibi bir dış veri kaynağından gelecektir.</span><span class="sxs-lookup"><span data-stu-id="f02ff-194">In your own application, your data will likely come from an external data source such as a SQL database.</span></span>

<span data-ttu-id="f02ff-195">Merhaba ikinci bölümü oluşturur bir `IndexBatch` hello belgeleri içeren.</span><span class="sxs-lookup"><span data-stu-id="f02ff-195">hello second part creates an `IndexBatch` containing hello documents.</span></span> <span data-ttu-id="f02ff-196">Oluşturduğunuz, bu durumda çağırarak hello zamanında tooapply toohello toplu istediğiniz hello işlemi belirttiğiniz `IndexBatch.Upload`.</span><span class="sxs-lookup"><span data-stu-id="f02ff-196">You specify hello operation you want tooapply toohello batch at hello time you create it, in this case by calling `IndexBatch.Upload`.</span></span> <span data-ttu-id="f02ff-197">Karşıya yüklenen toohello Azure Search dizini tarafından hello hello toplu olduğundan `Documents.Index` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="f02ff-197">hello batch is then uploaded toohello Azure Search index by hello `Documents.Index` method.</span></span>

> [!NOTE]
> <span data-ttu-id="f02ff-198">Bu örnekte, biz yalnızca belgeleri karşıya yükleniyor.</span><span class="sxs-lookup"><span data-stu-id="f02ff-198">In this example, we are just uploading documents.</span></span> <span data-ttu-id="f02ff-199">Toomerge değişiklikler mevcut belgeleri veya delete belgeleri istediyseniz, çağırarak toplu işlemler oluşturabilirsiniz `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, veya `IndexBatch.Delete` yerine.</span><span class="sxs-lookup"><span data-stu-id="f02ff-199">If you wanted toomerge changes into existing documents or delete documents, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete` instead.</span></span> <span data-ttu-id="f02ff-200">Çağırarak farklı işlemlerini tek bir toplu işte karıştırabilirsiniz `IndexBatch.New`, bir koleksiyonunu alır `IndexAction` nesneleri, bir belge üzerinde belirli bir işlemi her biri söyler Azure Search tooperform.</span><span class="sxs-lookup"><span data-stu-id="f02ff-200">You can also mix different operations in a single batch by calling `IndexBatch.New`, which takes a collection of `IndexAction` objects, each of which tells Azure Search tooperform a particular operation on a document.</span></span> <span data-ttu-id="f02ff-201">Her oluşturabilirsiniz `IndexAction` gibi hello karşılık gelen yöntemini çağırarak kendi işlemi ile `IndexAction.Merge`, `IndexAction.Upload`ve benzeri.</span><span class="sxs-lookup"><span data-stu-id="f02ff-201">You can create each `IndexAction` with its own operation by calling hello corresponding method such as `IndexAction.Merge`, `IndexAction.Upload`, and so on.</span></span>
> 
> 

<span data-ttu-id="f02ff-202">Merhaba üçüncü bu yöntem dizin oluşturma için önemli bir hata durumunu işler bir catch bloğunun parçasıdır.</span><span class="sxs-lookup"><span data-stu-id="f02ff-202">hello third part of this method is a catch block that handles an important error case for indexing.</span></span> <span data-ttu-id="f02ff-203">Azure Search hizmetinizin hello bazıları belgeleri hello toplu işlemde tooindex başarısız olursa bir `IndexBatchException` tarafından oluşturulan `Documents.Index`.</span><span class="sxs-lookup"><span data-stu-id="f02ff-203">If your Azure Search service fails tooindex some of hello documents in hello batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="f02ff-204">Bu durum, hizmetiniz ağır yük altındayken belgelere dizin oluşturuyorsanız oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="f02ff-204">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="f02ff-205">**Bu durumu, kodunuzda açık şekilde işlemenizi kesinlikle öneririz.**</span><span class="sxs-lookup"><span data-stu-id="f02ff-205">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="f02ff-206">Gecikme ve başarısız olan dizin hello belge yeniden deneyin veya oturum ve hello örnek vermez veya uygulamanızın veri tutarlılığı gereksinimlerine bağlı olarak başka bir şey yapabilirsiniz gibi devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f02ff-206">You can delay and then retry indexing hello documents that failed, or you can log and continue like hello sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

> [!NOTE]
> <span data-ttu-id="f02ff-207">Merhaba kullanabilirsiniz `FindFailedActionsToRetry` içeren yeni bir toplu yöntemi tooconstruct yalnızca önceki çağrıda çok başarısız Eylemler hello`Index`.</span><span class="sxs-lookup"><span data-stu-id="f02ff-207">You can use hello `FindFailedActionsToRetry` method tooconstruct a new batch containing only hello actions that failed in a previous call too`Index`.</span></span> <span data-ttu-id="f02ff-208">Merhaba yöntemi belgelenmiştir [burada](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) ve nasıl tooproperly kullanır, tartışma [StackOverflow üzerinde](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span><span class="sxs-lookup"><span data-stu-id="f02ff-208">hello method is documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) and there is a discussion of how tooproperly use it [on StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span></span>
>
>

<span data-ttu-id="f02ff-209">Son olarak, hello `UploadDocuments` yöntemi gecikmeler iki saniye.</span><span class="sxs-lookup"><span data-stu-id="f02ff-209">Finally, hello `UploadDocuments` method delays for two seconds.</span></span> <span data-ttu-id="f02ff-210">Merhaba örnek uygulaması toowait hello belgelerin aramada kullanılabilir kısa bir süre tooensure gerekir böylece dizin oluşturma Azure Search hizmetinizin zaman uyumsuz olarak gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="f02ff-210">Indexing happens asynchronously in your Azure Search service, so hello sample application needs toowait a short time tooensure that hello documents are available for searching.</span></span> <span data-ttu-id="f02ff-211">Bu gibi gecikmeler genellikle yalnızca gösterilerde, testlerde ve örnek uygulamalarda gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f02ff-211">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

#### <a name="how-hello-net-sdk-handles-documents"></a><span data-ttu-id="f02ff-212">Merhaba .NET SDK belgeleri nasıl işler?</span><span class="sxs-lookup"><span data-stu-id="f02ff-212">How hello .NET SDK handles documents</span></span>
<span data-ttu-id="f02ff-213">Size nasıl hello Azure Search .NET SDK'sı gibi kullanıcı tanımlı bir sınıf örneklerini mümkün tooupload merak ediyor olabilirsiniz `Hotel` toohello dizini.</span><span class="sxs-lookup"><span data-stu-id="f02ff-213">You may be wondering how hello Azure Search .NET SDK is able tooupload instances of a user-defined class like `Hotel` toohello index.</span></span> <span data-ttu-id="f02ff-214">toohelp bu sorunun yanıtlanmasına, hello bakalım `Hotel` sınıfı:</span><span class="sxs-lookup"><span data-stu-id="f02ff-214">toohelp answer that question, let's look at hello `Hotel` class:</span></span>

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

<span data-ttu-id="f02ff-215">Merhaba ilk şey toonotice her ortak özelliği olan `Hotel` tooa alan hello dizin tanımı, ancak çok önemli bir fark karşılık gelir: her alanı hello adını küçük harfle ("ortası büyük harf"), her ortak hello adını sırasında başlatır özelliği `Hotel` büyük harfle ("Pascal büyük") başlar.</span><span class="sxs-lookup"><span data-stu-id="f02ff-215">hello first thing toonotice is that each public property of `Hotel` corresponds tooa field in hello index definition, but with one crucial difference: hello name of each field starts with a lower-case letter ("camel case"), while hello name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="f02ff-216">Bu, hello hedef şema hello uygulama geliştiricisi dış hello denetimin olduğu veri bağlamayı gerçekleştiren .NET uygulamalarında ortak bir senaryodur.</span><span class="sxs-lookup"><span data-stu-id="f02ff-216">This is a common scenario in .NET applications that perform data-binding where hello target schema is outside hello control of hello application developer.</span></span> <span data-ttu-id="f02ff-217">Adlandırma yönergeleri özellik adlarını ortası büyük harf yaparak tooviolate hello .NET sahip olmak yerine hello SDK toomap hello özellik adları toocamel harf hello ile otomatik olarak anlayabilirsiniz `[SerializePropertyNamesAsCamelCase]` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="f02ff-217">Rather than having tooviolate hello .NET naming guidelines by making property names camel-case, you can tell hello SDK toomap hello property names toocamel-case automatically with hello `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="f02ff-218">Hello Azure Search .NET SDK'sını kullanır hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) kitaplığı tooserialize ve, özel model nesneleri tooand json'dan seri durumdan.</span><span class="sxs-lookup"><span data-stu-id="f02ff-218">hello Azure Search .NET SDK uses hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library tooserialize and deserialize your custom model objects tooand from JSON.</span></span> <span data-ttu-id="f02ff-219">Gerekirse bu seri hale getirmeyi özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f02ff-219">You can customize this serialization if needed.</span></span> <span data-ttu-id="f02ff-220">Daha fazla ayrıntı için bkz: [JSON.NET ile özel serileştirme](#JsonDotNet).</span><span class="sxs-lookup"><span data-stu-id="f02ff-220">For more details, see [Custom Serialization with JSON.NET](#JsonDotNet).</span></span>
> 
> 

<span data-ttu-id="f02ff-221">Merhaba ikinci şey toonotice olan hello öznitelikleri gibi `IsFilterable`, `IsSearchable`, `Key`, ve `Analyzer` her ortak özelliği tasarlamanız.</span><span class="sxs-lookup"><span data-stu-id="f02ff-221">hello second thing toonotice are hello attributes such as `IsFilterable`, `IsSearchable`, `Key`, and `Analyzer` that decorate each public property.</span></span> <span data-ttu-id="f02ff-222">Bu öznitelikler toohello doğrudan eşleme [hello Azure Search dizini karşılık gelen özniteliklerini](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span><span class="sxs-lookup"><span data-stu-id="f02ff-222">These attributes map directly toohello [corresponding attributes of hello Azure Search index](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span></span> <span data-ttu-id="f02ff-223">Merhaba `FieldBuilder` sınıfı hello dizini için bu tooconstruct alan tanımları kullanır.</span><span class="sxs-lookup"><span data-stu-id="f02ff-223">hello `FieldBuilder` class uses these tooconstruct field definitions for hello index.</span></span>

<span data-ttu-id="f02ff-224">Merhaba üçüncü önemli şey hello hakkında `Hotel` sınıfı hello genel özelliklerin hello veri türleri bulunur.</span><span class="sxs-lookup"><span data-stu-id="f02ff-224">hello third important thing about hello `Hotel` class are hello data types of hello public properties.</span></span> <span data-ttu-id="f02ff-225">Bu özelliklerin Hello .NET türleri tootheir hello dizin tanımında eşdeğer alan türleriyle eşlenir.</span><span class="sxs-lookup"><span data-stu-id="f02ff-225">hello .NET types of  these properties map tootheir equivalent field types in hello index definition.</span></span> <span data-ttu-id="f02ff-226">Örneğin, hello `Category` dize özelliği eşlemeleri toohello `category` türü alan `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="f02ff-226">For example, hello `Category` string property maps toohello `category` field, which is of type `Edm.String`.</span></span> <span data-ttu-id="f02ff-227">Arasında benzer türde eşlemeler bulunur `bool?` ve `Edm.Boolean`, `DateTimeOffset?` ve `Edm.DateTimeOffset`, vb. hello hello tür eşlemesi için belirli kurallar ile Merhaba belgelenmiştir `Documents.Get` hello yönteminde [Azure Search .NET SDK'sı başvuru](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span><span class="sxs-lookup"><span data-stu-id="f02ff-227">There are similar type mappings between `bool?` and `Edm.Boolean`, `DateTimeOffset?` and `Edm.DateTimeOffset`, etc. hello specific rules for hello type mapping are documented with hello `Documents.Get` method in hello [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span> <span data-ttu-id="f02ff-228">Merhaba `FieldBuilder` sınıfı, bu eşlemeyi mvc'deki ancak serileştirme sorunları tootroubleshoot gerektiğinde yine yararlı toounderstand olabilir.</span><span class="sxs-lookup"><span data-stu-id="f02ff-228">hello `FieldBuilder` class takes care of this mapping for you, but it can still be helpful toounderstand in case you need tootroubleshoot any serialization issues.</span></span>

<span data-ttu-id="f02ff-229">Bu özelliği toouse her iki yönde de kendi sınıflarınızı belge olarak çalışır; Ayrıca arama sonuçları almak ve sahip hello SDK otomatik olarak seri durumdan bunları tooa türü tercih ettiğiniz biz hello sonraki bölümde göreceğiniz gibi.</span><span class="sxs-lookup"><span data-stu-id="f02ff-229">This ability toouse your own classes as documents works in both directions; You can also retrieve search results and have hello SDK automatically deserialize them tooa type of your choice, as we will see in hello next section.</span></span>

> [!NOTE]
> <span data-ttu-id="f02ff-230">Hello Azure Search .NET SDK'sı hello kullanarak dinamik tür belirtilmiş belgeleri de destekler `Document` bir anahtar/değer eşlemesi alan adları toofield değerlerinin sınıfı.</span><span class="sxs-lookup"><span data-stu-id="f02ff-230">hello Azure Search .NET SDK also supports dynamically-typed documents using hello `Document` class, which is a key/value mapping of field names toofield values.</span></span> <span data-ttu-id="f02ff-231">Bu tasarım zamanında hello dizin şemasını bilmediğiniz veya kullanışsız toobind toospecific modeli sınıfları olmayacağı senaryolarda kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="f02ff-231">This is useful in scenarios where you don't know hello index schema at design-time, or where it would be inconvenient toobind toospecific model classes.</span></span> <span data-ttu-id="f02ff-232">Merhaba SDK ilgili tüm hello yöntemler hello ile çalışan aşırı yüklerin `Document` sınıfı yanı sıra genel türde bir parametre alan kesin tür belirtilmiş aşırı.</span><span class="sxs-lookup"><span data-stu-id="f02ff-232">All hello methods in hello SDK that deal with documents have overloads that work with hello `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="f02ff-233">Yalnızca ikinci Merhaba, hello örnek kodda Bu öğreticide kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f02ff-233">Only hello latter are used in hello sample code in this tutorial.</span></span> <span data-ttu-id="f02ff-234">Merhaba `Document` sınıfının devraldığı `Dictionary<string, object>`.</span><span class="sxs-lookup"><span data-stu-id="f02ff-234">hello `Document` class inherits from `Dictionary<string, object>`.</span></span> <span data-ttu-id="f02ff-235">Diğer ayrıntıları bulmak [burada](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span><span class="sxs-lookup"><span data-stu-id="f02ff-235">You can find other details [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span></span>
> 
> 

<span data-ttu-id="f02ff-236">**Neden boş değer atanabilir türleri kullanmalısınız?**</span><span class="sxs-lookup"><span data-stu-id="f02ff-236">**Why you should use nullable data types**</span></span>

<span data-ttu-id="f02ff-237">Kendi model sınıfları toomap tooan Azure Search dizininizi tasarlarken gibi özellikleri değer türlerini bildirme öneririz `bool` ve `int` toobe boş değer atanabilir (örneğin, `bool?` yerine `bool`).</span><span class="sxs-lookup"><span data-stu-id="f02ff-237">When designing your own model classes toomap tooan Azure Search index, we recommend declaring properties of value types such as `bool` and `int` toobe nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="f02ff-238">Atanamayan bir özellik kullanırsanız, çok sahip**garanti** hiçbir belgeleri dizininize hello karşılık gelen alan için bir null değer içeriyor.</span><span class="sxs-lookup"><span data-stu-id="f02ff-238">If you use a non-nullable property, you have too**guarantee** that no documents in your index contain a null value for hello corresponding field.</span></span> <span data-ttu-id="f02ff-239">Merhaba SDK ne hello Azure Search hizmeti, tooenforce bu yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="f02ff-239">Neither hello SDK nor hello Azure Search service will help you tooenforce this.</span></span>

<span data-ttu-id="f02ff-240">Bu yalnızca kuramsal bir sorun değildir: türü olan yeni bir alan tooan mevcut dizin eklediğiniz bir senaryoyu düşünün `Edm.Int32`.</span><span class="sxs-lookup"><span data-stu-id="f02ff-240">This is not just a hypothetical concern: Imagine a scenario where you add a new field tooan existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="f02ff-241">(Tüm türleri Azure Search'te boş değer atanabilir olmasıdır) hello dizin tanımını güncelleştirdikten sonra bu yeni alan için bir null değer tüm belgeler olacaktır.</span><span class="sxs-lookup"><span data-stu-id="f02ff-241">After updating hello index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="f02ff-242">Ardından bir model sınıfı bir null ile kullanırsanız `int` özelliği bu alan için elde edersiniz bir `JsonSerializationException` şöyle tooretrieve belgeleri çalışırken:</span><span class="sxs-lookup"><span data-stu-id="f02ff-242">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying tooretrieve documents:</span></span>

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="f02ff-243">Bu nedenle, en iyi uygulama olarak model sınıflarınızda boş değer atanabilir türler kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="f02ff-243">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

<a name="JsonDotNet"></a>

#### <a name="custom-serialization-with-jsonnet"></a><span data-ttu-id="f02ff-244">JSON.NET ile özel seri hale getirme</span><span class="sxs-lookup"><span data-stu-id="f02ff-244">Custom Serialization with JSON.NET</span></span>
<span data-ttu-id="f02ff-245">Merhaba SDK JSON.NET seri hale getirme ve belgeleri seri durumdan çıkarmak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="f02ff-245">hello SDK uses JSON.NET for serializing and deserializing documents.</span></span> <span data-ttu-id="f02ff-246">Seri hale getirme özelleştirebilir ve tanımlayarak, kendi gerekirse seri durumundan çıkarma `JsonConverter` veya `IContractResolver` (Merhaba bkz [JSON.NET belgelerine](http://www.newtonsoft.com/json/help/html/Introduction.htm) daha fazla ayrıntı için).</span><span class="sxs-lookup"><span data-stu-id="f02ff-246">You can customize serialization and deserialization if needed by defining your own `JsonConverter` or `IContractResolver` (see hello [JSON.NET documentation](http://www.newtonsoft.com/json/help/html/Introduction.htm) for more details).</span></span> <span data-ttu-id="f02ff-247">Azure Search ve diğer daha Gelişmiş senaryolar ile kullanılmak üzere uygulamanızdan tooadapt varolan bir model sınıfı istediğinizde bu yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="f02ff-247">This can be useful when you want tooadapt an existing model class from your application for use with Azure Search, and other more advanced scenarios.</span></span> <span data-ttu-id="f02ff-248">Örneğin, özel serileştirme ile şunları yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f02ff-248">For example, with custom serialization you can:</span></span>

* <span data-ttu-id="f02ff-249">İçerebilir veya belge alanlar olarak depolanan belirli özellikleri modeli sınıfınızın dışlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f02ff-249">Include or exclude certain properties of your model class from being stored as document fields.</span></span>
* <span data-ttu-id="f02ff-250">Kodunuzda özellik adları ve alan adları, dizininizdeki arasında eşleyin.</span><span class="sxs-lookup"><span data-stu-id="f02ff-250">Map between property names in your code and field names in your index.</span></span>
* <span data-ttu-id="f02ff-251">Özellikler toodocument alanlarını eşleme için kullanılan özel öznitelikler oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f02ff-251">Create custom attributes that can be used for mapping properties toodocument fields.</span></span>

<span data-ttu-id="f02ff-252">Merhaba birim testlerinde hello Azure Search .NET SDK github'da için özel serileştirme uygulamanın örnekleri bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f02ff-252">You can find examples of implementing custom serialization in hello unit tests for hello Azure Search .NET SDK on GitHub.</span></span> <span data-ttu-id="f02ff-253">İyi bir başlangıç noktasıdır [bu klasör](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models).</span><span class="sxs-lookup"><span data-stu-id="f02ff-253">A good starting point is [this folder](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models).</span></span> <span data-ttu-id="f02ff-254">Merhaba özel serileştirme testleri tarafından kullanılan sınıfları içerir.</span><span class="sxs-lookup"><span data-stu-id="f02ff-254">It contains classes that are used by hello custom serialization tests.</span></span>

### <a name="searching-for-documents-in-hello-index"></a><span data-ttu-id="f02ff-255">Merhaba dizin belgelerde arama</span><span class="sxs-lookup"><span data-stu-id="f02ff-255">Searching for documents in hello index</span></span>
<span data-ttu-id="f02ff-256">Merhaba son Merhaba örnek uygulaması hello dizin bazı belgelerde toosearch adımdır.</span><span class="sxs-lookup"><span data-stu-id="f02ff-256">hello last step in hello sample application is toosearch for some documents in hello index.</span></span> <span data-ttu-id="f02ff-257">yöntemini aşağıdaki hello bunu yapar:</span><span class="sxs-lookup"><span data-stu-id="f02ff-257">hello following method does this:</span></span>

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

<span data-ttu-id="f02ff-258">Her bir sorgu yürütülmeden, bu yöntem önce yeni bir oluşturur `SearchParameters` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="f02ff-258">Each time it executes a query, this method first creates a new `SearchParameters` object.</span></span> <span data-ttu-id="f02ff-259">Sıralama, filtreleme, disk belleği ve olduğunu gibi hello sorgu için kullanılan toospecify ek seçenekler budur.</span><span class="sxs-lookup"><span data-stu-id="f02ff-259">This is used toospecify additional options for hello query such as sorting, filtering, paging, and faceting.</span></span> <span data-ttu-id="f02ff-260">Bu yöntemde, biz hello ayarladığınız `Filter`, `Select`, `OrderBy`, ve `Top` özelliği için farklı sorgular.</span><span class="sxs-lookup"><span data-stu-id="f02ff-260">In this method, we're setting hello `Filter`, `Select`, `OrderBy`, and `Top` property for different queries.</span></span> <span data-ttu-id="f02ff-261">Tüm hello `SearchParameters` özellikleri belgelenmiştir [burada](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span><span class="sxs-lookup"><span data-stu-id="f02ff-261">All hello `SearchParameters` properties are documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span></span>

<span data-ttu-id="f02ff-262">Merhaba sonraki adımdır tooactually hello arama sorgu yürütün.</span><span class="sxs-lookup"><span data-stu-id="f02ff-262">hello next step is tooactually execute hello search query.</span></span> <span data-ttu-id="f02ff-263">Bu yapılır hello kullanarak `Documents.Search` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="f02ff-263">This is done using hello `Documents.Search` method.</span></span> <span data-ttu-id="f02ff-264">Her sorgu için biz hello arama metni toouse bir dize olarak geçirin (veya `"*"` arama metni ise), artı daha önce oluşturduğunuz parametreleri arama hello.</span><span class="sxs-lookup"><span data-stu-id="f02ff-264">For each query, we pass hello search text toouse as a string (or `"*"` if there is no search text), plus hello search parameters created earlier.</span></span> <span data-ttu-id="f02ff-265">Biz de belirtmeniz `Hotel` hello türü parametre olarak `Documents.Search`, söyleyen hello SDK toodeserialize belgeleri hello arama sonuçlarında türündeki nesneleri `Hotel`.</span><span class="sxs-lookup"><span data-stu-id="f02ff-265">We also specify `Hotel` as hello type parameter for `Documents.Search`, which tells hello SDK toodeserialize documents in hello search results into objects of type `Hotel`.</span></span>

> [!NOTE]
> <span data-ttu-id="f02ff-266">Merhaba arama sorgu ifade sözdizimi hakkında daha fazla bilgi bulabilirsiniz [burada](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="f02ff-266">You can find more information about hello search query expression syntax [here](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span></span>
> 
> 

<span data-ttu-id="f02ff-267">Son olarak, her sorgu sonra bu yöntem her bir belge toohello konsol yazdırma tüm hello eşleşmeleri hello arama sonuçlarında yinelenir:</span><span class="sxs-lookup"><span data-stu-id="f02ff-267">Finally, after each query this method iterates through all hello matches in hello search results, printing each document toohello console:</span></span>

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

<span data-ttu-id="f02ff-268">Buna karşılık her hello sorguları daha yakın bir göz atalım.</span><span class="sxs-lookup"><span data-stu-id="f02ff-268">Let's take a closer look at each of hello queries in turn.</span></span> <span data-ttu-id="f02ff-269">Merhaba kod tooexecute hello ilk sorgu şöyledir:</span><span class="sxs-lookup"><span data-stu-id="f02ff-269">Here is hello code tooexecute hello first query:</span></span>

```csharp
parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);
```

<span data-ttu-id="f02ff-270">Bu durumda, "Bütçe" Merhaba word eşleşen Oteller için arama yapıyorsanız ve tooget geri yalnızca hello otel adları, hello tarafından belirtilen istiyoruz `Select` parametresi.</span><span class="sxs-lookup"><span data-stu-id="f02ff-270">In this case, we're searching for hotels that match hello word "budget", and we want tooget back only hello hotel names, as specified by hello `Select` parameter.</span></span> <span data-ttu-id="f02ff-271">Merhaba sonuçları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f02ff-271">Here are hello results:</span></span>

    Name: Roach Motel

<span data-ttu-id="f02ff-272">Ardından, biz toofind hello Oteller değerinden 150 ABD dolarını gecelik oranı ile istediğiniz ve yalnızca hello otel kimliği ve açıklama döndürür:</span><span class="sxs-lookup"><span data-stu-id="f02ff-272">Next, we want toofind hello hotels with a nightly rate of less than $150, and return only hello hotel ID and description:</span></span>

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

<span data-ttu-id="f02ff-273">Bu sorgu bir OData kullanan `$filter` ifadesi, `baseRate lt 150`, hello dizindeki toofilter hello belgeler.</span><span class="sxs-lookup"><span data-stu-id="f02ff-273">This query uses an OData `$filter` expression, `baseRate lt 150`, toofilter hello documents in hello index.</span></span> <span data-ttu-id="f02ff-274">Hello Azure Search destekleyen OData sözdizimi hakkında daha fazla bilgi için [burada](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="f02ff-274">You can find out more about hello OData syntax that Azure Search supports [here](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span></span>

<span data-ttu-id="f02ff-275">Merhaba hello sorgunun sonuçlarını şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f02ff-275">Here are hello results of hello query:</span></span>

    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close tootown hall and hello river

<span data-ttu-id="f02ff-276">Ardından, en son renovated ve hello otel adını ve son Yenileme tarihi toofind hello üst iki Oteller istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="f02ff-276">Next, we want toofind hello top two hotels that have been most recently renovated, and show hello hotel name and last renovation date.</span></span> <span data-ttu-id="f02ff-277">Merhaba kod aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="f02ff-277">Here is hello code:</span></span> 

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

<span data-ttu-id="f02ff-278">OData sözdizimi toospecify hello yeniden bu durumda, kullandığımız `OrderBy` parametre olarak `lastRenovationDate desc`.</span><span class="sxs-lookup"><span data-stu-id="f02ff-278">In this case, we again use OData syntax toospecify hello `OrderBy` parameter as `lastRenovationDate desc`.</span></span> <span data-ttu-id="f02ff-279">Ayrıca `Top` too2 tooensure biz yalnızca get hello üstteki iki belgeleri.</span><span class="sxs-lookup"><span data-stu-id="f02ff-279">We also set `Top` too2 tooensure we only get hello top two documents.</span></span> <span data-ttu-id="f02ff-280">Önce ayarlar gibi `Select` hangi alanların döndürülmesi toospecify.</span><span class="sxs-lookup"><span data-stu-id="f02ff-280">As before, we set `Select` toospecify which fields should be returned.</span></span>

<span data-ttu-id="f02ff-281">Merhaba sonuçları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f02ff-281">Here are hello results:</span></span>

    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

<span data-ttu-id="f02ff-282">Son olarak, toofind hello word "motel" eşleşen tüm Oteller istiyoruz:</span><span class="sxs-lookup"><span data-stu-id="f02ff-282">Finally, we want toofind all hotels that match hello word "motel":</span></span>

```csharp
parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

<span data-ttu-id="f02ff-283">Ve hello belirtmedi olduğundan, tüm alanları içeren hello sonuçları işte `Select` özelliği:</span><span class="sxs-lookup"><span data-stu-id="f02ff-283">And here are hello results, which include all fields since we did not specify hello `Select` property:</span></span>

    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577

<span data-ttu-id="f02ff-284">Başlangıç Öğreticisi Bu adım tamamlandıktan, ancak burada Durdur yok.</span><span class="sxs-lookup"><span data-stu-id="f02ff-284">This step completes hello tutorial, but don't stop here.</span></span> <span data-ttu-id="f02ff-285">**Sonraki adımlar** Azure Search hakkında daha fazla bilgi için ek kaynaklar sağlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="f02ff-285">**Next steps** provides additional resources for learning more about Azure Search.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f02ff-286">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f02ff-286">Next steps</span></span>
* <span data-ttu-id="f02ff-287">Hello için Hello başvuruları Gözat [.NET SDK'sı](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) ve [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="f02ff-287">Browse hello references for hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
* <span data-ttu-id="f02ff-288">Bilginiz aracılığıyla deepen [videolar ve diğer örnekler ve öğreticiler](search-video-demo-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="f02ff-288">Deepen your knowledge through [videos and other samples and tutorials](search-video-demo-tutorial-list.md).</span></span>
* <span data-ttu-id="f02ff-289">Gözden geçirme [adlandırma kuralları](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) çeşitli nesneleri adlandırma toolearn hello kuralları.</span><span class="sxs-lookup"><span data-stu-id="f02ff-289">Review [naming conventions](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) toolearn hello rules for naming various objects.</span></span>
* <span data-ttu-id="f02ff-290">Gözden geçirme [desteklenen veri türleri](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) Azure Search'te.</span><span class="sxs-lookup"><span data-stu-id="f02ff-290">Review [supported data types](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) in Azure Search.</span></span>
