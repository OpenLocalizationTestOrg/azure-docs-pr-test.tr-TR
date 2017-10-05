---
title: "Verileri karşıya yükleme (.NET - Azure Search) | Microsoft Docs"
description: ".NET SDK kullanarak Azure Search'te bir dizine nasıl veri yükleneceğini öğrenin."
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
ms.openlocfilehash: bdd952869143c6ca6374bb9264db5bcba1f32b50
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="upload-data-to-azure-search-using-the-net-sdk"></a><span data-ttu-id="bb54b-103">.NET SDK kullanarak Azure Search'e veri yükleme</span><span class="sxs-lookup"><span data-stu-id="bb54b-103">Upload data to Azure Search using the .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="bb54b-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="bb54b-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="bb54b-105">.NET</span><span class="sxs-lookup"><span data-stu-id="bb54b-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="bb54b-106">REST</span><span class="sxs-lookup"><span data-stu-id="bb54b-106">REST</span></span>](search-import-data-rest-api.md)
> 
> 

<span data-ttu-id="bb54b-107">Bu makalede, bir Azure Search dizinine veri aktarmak için [Azure Search .NET SDK](https://aka.ms/search-sdk)'sının nasıl kullanılacağı gösterilir.</span><span class="sxs-lookup"><span data-stu-id="bb54b-107">This article will show you how to use the [Azure Search .NET SDK](https://aka.ms/search-sdk) to import data into an Azure Search index.</span></span>

<span data-ttu-id="bb54b-108">Bu kılavuza başlamadan önce bir [Azure Search dizini oluşturmuş](search-what-is-an-index.md) olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bb54b-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span> <span data-ttu-id="bb54b-109">Ayrıca, bu makale [.NET SDK kullanarak Azure Search dizini oluşturma](search-create-index-dotnet.md#CreateSearchServiceClient) başlığı altında gösterildiği şekilde önceden bir `SearchServiceClient` nesnesi oluşturduğunuzu varsayar.</span><span class="sxs-lookup"><span data-stu-id="bb54b-109">This article also assumes that you have already created a `SearchServiceClient` object, as shown in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md#CreateSearchServiceClient).</span></span>

> [!NOTE]
> <span data-ttu-id="bb54b-110">Bu makaledeki örnek kodun tamamı C# dilinde yazılmıştır.</span><span class="sxs-lookup"><span data-stu-id="bb54b-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="bb54b-111">Tam kaynak kodunu [GitHub](http://aka.ms/search-dotnet-howto)'da bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb54b-111">You can find the full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="bb54b-112">Ayrıca, örnek kodla ilgili daha ayrıntılı yönergeler için [Azure Search .NET SDK’sı](search-howto-dotnet-sdk.md) hakkındaki yazıları da okuyabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb54b-112">You can also read about the [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of the sample code.</span></span>

<span data-ttu-id="bb54b-113">.NET SDK kullanarak dizininize belge göndermek için şunu yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="bb54b-113">In order to push documents into your index using the .NET SDK, you will need to:</span></span>

1. <span data-ttu-id="bb54b-114">Arama dizininize bağlamak için bir `SearchIndexClient` nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bb54b-114">Create a `SearchIndexClient` object to connect to your search index.</span></span>
2. <span data-ttu-id="bb54b-115">Eklenecek, değiştirilecek veya silinecek belgeleri içeren bir `IndexBatch` oluşturun.</span><span class="sxs-lookup"><span data-stu-id="bb54b-115">Create an `IndexBatch` containing the documents to be added, modified, or deleted.</span></span>
3. <span data-ttu-id="bb54b-116">Arama dizininize `IndexBatch` göndermek için `SearchIndexClient` öğenizin `Documents.Index` yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="bb54b-116">Call the `Documents.Index` method of your `SearchIndexClient` to send the `IndexBatch` to your search index.</span></span>

## <a name="create-an-instance-of-the-searchindexclient-class"></a><span data-ttu-id="bb54b-117">SearchIndexClient sınıfının bir örneğini oluşturma</span><span class="sxs-lookup"><span data-stu-id="bb54b-117">Create an instance of the SearchIndexClient class</span></span>
<span data-ttu-id="bb54b-118">Azure Search .NET SDK'sını kullanarak dizininize veri aktarmak için `SearchIndexClient` sınıfının bir örneğini oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="bb54b-118">To import data into your index using the Azure Search .NET SDK, you will need to create an instance of the `SearchIndexClient` class.</span></span> <span data-ttu-id="bb54b-119">Bu örneği kendiniz oluşturulabilirsiniz ancak bunun `Indexes.GetClient` yöntemini çağırmak için bir `SearchServiceClient` örneğine zaten sahipseniz daha kolay olur.</span><span class="sxs-lookup"><span data-stu-id="bb54b-119">You can construct this instance yourself, but it's easier if you already have a `SearchServiceClient` instance to call its `Indexes.GetClient` method.</span></span> <span data-ttu-id="bb54b-120">Örneğin, `serviceClient` adlı bir `SearchServiceClient` öğesinden "hotels" adlı bir dizin için şu şekilde bir `SearchIndexClient` elde edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="bb54b-120">For example, here is how you would obtain a `SearchIndexClient` for the index named "hotels" from a `SearchServiceClient` named `serviceClient`:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="bb54b-121">Genel bir arama uygulamasında, dizin yönetimi ve popülasyon, arama sorgularından ayrı bir bileşen tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="bb54b-121">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="bb54b-122">`Indexes.GetClient`, başka bir `SearchCredentials` sağlamanızı gerektirmediğinden, dizini doldurmak için uygundur.</span><span class="sxs-lookup"><span data-stu-id="bb54b-122">`Indexes.GetClient` is convenient for populating an index because it saves you the trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="bb54b-123">Yeni `SearchIndexClient` için `SearchServiceClient` oluşturmak üzere kullandığınız yönetici anahtarını geçirerek bunu yapar.</span><span class="sxs-lookup"><span data-stu-id="bb54b-123">It does this by passing the admin key that you used to create the `SearchServiceClient` to the new `SearchIndexClient`.</span></span> <span data-ttu-id="bb54b-124">Ancak uygulamanızın sorguları yürüten bölümünde, bir yönetici anahtarı yerine sorgu anahtarında geçirebilmeniz için doğrudan `SearchIndexClient` oluşturmak daha iyi olur.</span><span class="sxs-lookup"><span data-stu-id="bb54b-124">However, in the part of your application that executes queries, it is better to create the `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="bb54b-125">Bu, [en az ayrıcalık ilkesiyle](https://en.wikipedia.org/wiki/Principle_of_least_privilege) tutarlıdır ve uygulamanızı daha güvenli hale getirmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="bb54b-125">This is consistent with the [principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege) and will help to make your application more secure.</span></span> <span data-ttu-id="bb54b-126">[Azure Search REST API'si başvurusunda](https://docs.microsoft.com/rest/api/searchservice/) yönetici anahtarları ve sorgu anahtarları hakkında daha fazla bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb54b-126">You can find out more about admin keys and query keys in the [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
> 
> 

<span data-ttu-id="bb54b-127">`SearchIndexClient`, `Documents` özelliğine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="bb54b-127">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="bb54b-128">Bu özellik, belgeleri dizininize eklemek, bunları değiştirmek, silmek veya sorgulamak için ihtiyacınız olan tüm yöntemleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="bb54b-128">This property provides all the methods you need to add, modify, delete, or query documents in your index.</span></span>

## <a name="decide-which-indexing-action-to-use"></a><span data-ttu-id="bb54b-129">Hangi dizin oluşturma eyleminin kullanılacağına karar verme</span><span class="sxs-lookup"><span data-stu-id="bb54b-129">Decide which indexing action to use</span></span>
<span data-ttu-id="bb54b-130">.NET SDK kullanarak veri içeri aktarmak için verilerinizi bir `IndexBatch` nesnesine paketlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="bb54b-130">To import data using the .NET SDK, you will need to package up your data into an `IndexBatch` object.</span></span> <span data-ttu-id="bb54b-131">Bir `IndexBatch`, her birinde bir belge ve söz konusu belgede hangi eylemin (karşıya yükleme, birleştirme, silme, vb.) gerçekleştirileceğini Azure Search'e söyleyen bir özellik bulunan `IndexAction` nesneleri koleksiyonunu kapsar.</span><span class="sxs-lookup"><span data-stu-id="bb54b-131">An `IndexBatch` encapsulates a collection of `IndexAction` objects, each of which contains a document and a property that tells Azure Search what action to perform on that document (upload, merge, delete, etc).</span></span> <span data-ttu-id="bb54b-132">Yukarıdaki eylemlerden hangisini seçtiğinize bağlı olarak, her bir belgeye yalnızca belirli alanlar dahil edilmelidir:</span><span class="sxs-lookup"><span data-stu-id="bb54b-132">Depending on which of the below actions you choose, only certain fields must be included for each document:</span></span>

| <span data-ttu-id="bb54b-133">Eylem</span><span class="sxs-lookup"><span data-stu-id="bb54b-133">Action</span></span> | <span data-ttu-id="bb54b-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="bb54b-134">Description</span></span> | <span data-ttu-id="bb54b-135">Her bir belge için gerekli alanlar</span><span class="sxs-lookup"><span data-stu-id="bb54b-135">Necessary fields for each document</span></span> | <span data-ttu-id="bb54b-136">Notlar</span><span class="sxs-lookup"><span data-stu-id="bb54b-136">Notes</span></span> |
| --- | --- | --- | --- |
| `Upload` |<span data-ttu-id="bb54b-137">Bir `Upload` eylemi, belgenin yeni olması durumunda ekleneceği ve var olması durumunda güncelleştirileceği/değiştirileceği bir "upsert" ile benzerlik gösterir.</span><span class="sxs-lookup"><span data-stu-id="bb54b-137">An `Upload` action is similar to an "upsert" where the document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="bb54b-138">anahtar ve tanımlamak istediğiniz diğer alanlar</span><span class="sxs-lookup"><span data-stu-id="bb54b-138">key, plus any other fields you wish to define</span></span> |<span data-ttu-id="bb54b-139">Var olan bir belgeyi güncelleştirirken/değiştirirken istekte belirtilmeyen herhangi bir alan `null` olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="bb54b-139">When updating/replacing an existing document, any field that is not specified in the request will have its field set to `null`.</span></span> <span data-ttu-id="bb54b-140">Bu durum, alan daha önce değersiz olmayan bir değere ayarlanmış olsa dahi gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="bb54b-140">This occurs even when the field was previously set to a non-null value.</span></span> |
| `Merge` |<span data-ttu-id="bb54b-141">Var olan belgeyi belirtilen alanlarla güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="bb54b-141">Updates an existing document with the specified fields.</span></span> <span data-ttu-id="bb54b-142">Belge dizinde mevcut değilse birleştirme işlemi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="bb54b-142">If the document does not exist in the index, the merge will fail.</span></span> |<span data-ttu-id="bb54b-143">anahtar ve tanımlamak istediğiniz diğer alanlar</span><span class="sxs-lookup"><span data-stu-id="bb54b-143">key, plus any other fields you wish to define</span></span> |<span data-ttu-id="bb54b-144">Birleştirmede belirttiğiniz herhangi bir alan belgede var olan alanın yerini alır.</span><span class="sxs-lookup"><span data-stu-id="bb54b-144">Any field you specify in a merge will replace the existing field in the document.</span></span> <span data-ttu-id="bb54b-145">Buna `DataType.Collection(DataType.String)` türünde alanlar dahildir.</span><span class="sxs-lookup"><span data-stu-id="bb54b-145">This includes fields of type `DataType.Collection(DataType.String)`.</span></span> <span data-ttu-id="bb54b-146">Örneğin, belge `["budget"]` değerine sahip bir `tags` alanını içeriyorsa ve `tags` için `["economy", "pool"]` değeriyle bir birleştirme yürütürseniz `tags` alanının son değeri `["economy", "pool"]` olur.</span><span class="sxs-lookup"><span data-stu-id="bb54b-146">For example, if the document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, the final value of the `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="bb54b-147">`["budget", "economy", "pool"]` olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="bb54b-147">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `MergeOrUpload` |<span data-ttu-id="bb54b-148">Belirtilen anahtara sahip bir belge dizinde zaten mevcutsa bu eylem `Merge` gibi davranır.</span><span class="sxs-lookup"><span data-stu-id="bb54b-148">This action behaves like `Merge` if a document with the given key already exists in the index.</span></span> <span data-ttu-id="bb54b-149">Belge mevcut değilse yeni bir belgeyle `Upload` gibi davranır.</span><span class="sxs-lookup"><span data-stu-id="bb54b-149">If the document does not exist, it behaves like `Upload` with a new document.</span></span> |<span data-ttu-id="bb54b-150">anahtar ve tanımlamak istediğiniz diğer alanlar</span><span class="sxs-lookup"><span data-stu-id="bb54b-150">key, plus any other fields you wish to define</span></span> |- |
| `Delete` |<span data-ttu-id="bb54b-151">Belirtilen belgeyi dizinden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="bb54b-151">Removes the specified document from the index.</span></span> |<span data-ttu-id="bb54b-152">yalnızca anahtar</span><span class="sxs-lookup"><span data-stu-id="bb54b-152">key only</span></span> |<span data-ttu-id="bb54b-153">Anahtar alanı dışında belirttiğiniz tüm alanlar yoksayılır.</span><span class="sxs-lookup"><span data-stu-id="bb54b-153">Any fields you specify other than the key field will be ignored.</span></span> <span data-ttu-id="bb54b-154">Bir belgeden tek bir alanı kaldırmak istiyorsanız bunun yerine `Merge` kullanıp alanı açık bir şekilde null olarak ayarlamanız yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="bb54b-154">If you want to remove an individual field from a document, use `Merge` instead and simply set the field explicitly to null.</span></span> |

<span data-ttu-id="bb54b-155">Bir sonraki bölümde gösterildiği üzere, `IndexBatch` ve `IndexAction` sınıflarının çeşitli statik yöntemleriyle hangi eylemi kullanmak istediğinizi belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb54b-155">You can specify what action you want to use with the various static methods of the `IndexBatch` and `IndexAction` classes, as shown in the next section.</span></span>

## <a name="construct-your-indexbatch"></a><span data-ttu-id="bb54b-156">IndexBatch'inizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="bb54b-156">Construct your IndexBatch</span></span>
<span data-ttu-id="bb54b-157">Artık belgelerinizde hangi eylemleri gerçekleştireceğinizi bildiğinize göre, `IndexBatch` oluşturmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="bb54b-157">Now that you know which actions to perform on your documents, you are ready to construct the `IndexBatch`.</span></span> <span data-ttu-id="bb54b-158">Aşağıdaki örnek, bir toplu işlemin birkaç farklı eylemle nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="bb54b-158">The example below shows how to create a batch with a few different actions.</span></span> <span data-ttu-id="bb54b-159">Örneğimizde "hotels" dizinindeki bir belgeyle eşlenen `Hotel` adlı özel bir sınıf kullandığımıza dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="bb54b-159">Note that our example uses a custom class called `Hotel` that maps to a document in the "hotels" index.</span></span>

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
                Description = "Close to town hall and the river"
            }),
        IndexAction.Delete(new Hotel() { HotelId = "6" })
    };

var batch = IndexBatch.New(actions);
```

<span data-ttu-id="bb54b-160">Bu durumda, `IndexAction` sınıfında çağrılan yöntemler tarafından belirtildiği üzere, arama eylemlerimiz olarak `Upload`, `MergeOrUpload` ve `Delete` kullanıyoruz.</span><span class="sxs-lookup"><span data-stu-id="bb54b-160">In this case, we are using `Upload`, `MergeOrUpload`, and `Delete` as our search actions, as specified by the methods called on the `IndexAction` class.</span></span>

<span data-ttu-id="bb54b-161">Bu "hotels" dizini örneğinin, birçok belgeyle önceden doldurulduğunu varsayın.</span><span class="sxs-lookup"><span data-stu-id="bb54b-161">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="bb54b-162">`MergeOrUpload` kullanırken olası tüm belge alanlarını belirtmek zorunda kalmadığımıza ve `Delete` kullanırken yalnızca belge anahtarını (`HotelId`) belirttiğimize dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="bb54b-162">Note how we did not have to specify all the possible document fields when using `MergeOrUpload` and how we only specified the document key (`HotelId`) when using `Delete`.</span></span>

<span data-ttu-id="bb54b-163">Ayrıca, tek bir dizin oluşturma isteğine yalnızca en fazla 1000 belge dahil edebileceğinizi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="bb54b-163">Also, note that you can only include up to 1000 documents in a single indexing request.</span></span>

> [!NOTE]
> <span data-ttu-id="bb54b-164">Bu örnekte, farklı belgelere farklı eylemler uyguluyoruz.</span><span class="sxs-lookup"><span data-stu-id="bb54b-164">In this example, we are applying different actions to different documents.</span></span> <span data-ttu-id="bb54b-165">Toplu işlemdeki tüm belgelerde aynı eylemleri gerçekleştirmek istiyorsanız `IndexBatch.New` çağırmak yerine `IndexBatch` öğesinin diğer statik yöntemlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb54b-165">If you wanted to perform the same actions across all documents in the batch, instead of calling `IndexBatch.New`, you could use the other static methods of `IndexBatch`.</span></span> <span data-ttu-id="bb54b-166">Örneğin; `IndexBatch.Merge`, `IndexBatch.MergeOrUpload` ve `IndexBatch.Delete` çağırarak toplu işlemler oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb54b-166">For example, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete`.</span></span> <span data-ttu-id="bb54b-167">Bu yöntemler, `IndexAction` nesneleri yerine bir belge koleksiyonu (bu örnekte `Hotel` türünde nesneler) alır.</span><span class="sxs-lookup"><span data-stu-id="bb54b-167">These methods take a collection of documents (objects of type `Hotel` in this example) instead of `IndexAction` objects.</span></span>
> 
> 

## <a name="import-data-to-the-index"></a><span data-ttu-id="bb54b-168">Dizine veri aktarma</span><span class="sxs-lookup"><span data-stu-id="bb54b-168">Import data to the index</span></span>
<span data-ttu-id="bb54b-169">Artık başlatılan bir `IndexBatch` nesneniz olduğuna göre `SearchIndexClient` nesneniz üzerinden `Documents.Index` çağrısı yaparak bunu dizininize gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb54b-169">Now that you have an initialized `IndexBatch` object, you can send it to the index by calling `Documents.Index` on your `SearchIndexClient` object.</span></span> <span data-ttu-id="bb54b-170">Aşağıdaki örnekte, nasıl `Index` çağrılacağının yanı sıra gerçekleştirmeniz gereken bazı ek adımlar gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="bb54b-170">The following example shows how to call `Index`, as well as some extra steps you will need to perform:</span></span>

```csharp
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
```

<span data-ttu-id="bb54b-171">`try`/`catch` öğesinin, `Index` yöntemine yönelik çağrıyı çevrelediğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="bb54b-171">Note the `try`/`catch` surrounding the call to the `Index` method.</span></span> <span data-ttu-id="bb54b-172">Catch bloğu, dizin oluşturma için önemli bir hata durumunu işler.</span><span class="sxs-lookup"><span data-stu-id="bb54b-172">The catch block handles an important error case for indexing.</span></span> <span data-ttu-id="bb54b-173">Azure Search hizmetiniz toplu işlemdeki belgelerin bazılarına dizin oluşturmada başarısız olursa `Documents.Index` tarafından bir `IndexBatchException` oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="bb54b-173">If your Azure Search service fails to index some of the documents in the batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="bb54b-174">Bu durum, hizmetiniz ağır yük altındayken belgelere dizin oluşturuyorsanız oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="bb54b-174">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="bb54b-175">**Bu durumu, kodunuzda açık şekilde işlemenizi kesinlikle öneririz.**</span><span class="sxs-lookup"><span data-stu-id="bb54b-175">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="bb54b-176">Başarısız olan belgelere dizin oluşturmayı geciktirip sonra yeniden deneyebilir veya günlük tutup örneğin devam ettiği şekilde devam edebilir veya uygulamanızın veri tutarlılığı gereksinimlerine bağlı olarak başka bir şey yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb54b-176">You can delay and then retry indexing the documents that failed, or you can log and continue like the sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

<span data-ttu-id="bb54b-177">Son olarak, yukarıdaki örnekteki kod iki saniye gecikir.</span><span class="sxs-lookup"><span data-stu-id="bb54b-177">Finally, the code in the example above delays for two seconds.</span></span> <span data-ttu-id="bb54b-178">Azure Search hizmetinizde dizin oluşturma uyumsuz şekilde meydana gelir; bu nedenle belgelerin aramada kullanılabilir olduğundan emin olmak için örnek uygulamanızın kısa bir süre beklemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="bb54b-178">Indexing happens asynchronously in your Azure Search service, so the sample application needs to wait a short time to ensure that the documents are available for searching.</span></span> <span data-ttu-id="bb54b-179">Bu gibi gecikmeler genellikle yalnızca gösterilerde, testlerde ve örnek uygulamalarda gereklidir.</span><span class="sxs-lookup"><span data-stu-id="bb54b-179">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

<a name="HotelClass"></a>

### <a name="how-the-net-sdk-handles-documents"></a><span data-ttu-id="bb54b-180">.NET SDK belgeleri nasıl işler?</span><span class="sxs-lookup"><span data-stu-id="bb54b-180">How the .NET SDK handles documents</span></span>
<span data-ttu-id="bb54b-181">Azure Search .NET SDK'sının `Hotel` gibi kullanıcı tanımlı bir sınıfın örneklerini dizine nasıl yükleyebildiğini merak ediyor olabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb54b-181">You may be wondering how the Azure Search .NET SDK is able to upload instances of a user-defined class like `Hotel` to the index.</span></span> <span data-ttu-id="bb54b-182">Bu sorunun yanıtlanmasına yardımcı olmak için [.NET SDK kullanarak Azure Search dizini oluşturma](search-create-index-dotnet.md#DefineIndex)'da tanımlanan dizin şemasıyla eşlenen `Hotel` sınıfına bakalım:</span><span class="sxs-lookup"><span data-stu-id="bb54b-182">To help answer that question, let's look at the `Hotel` class, which maps to the index schema defined in [Create an Azure Search index using the .NET SDK](search-create-index-dotnet.md#DefineIndex):</span></span>

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

<span data-ttu-id="bb54b-183">Fark edilecek ilk şey, `Hotel` öğesinin her bir genel özelliğinin dizin tanımındaki bir alana karşılık geldiği ancak çok önemli bir fark olduğudur: `Hotel` öğesinin her bir genel özelliğinin adı büyük harfle ("Pascal büyük/küçük harfi") başlarken her bir alanın adı küçük harfle ("ortası büyük harf") başlar.</span><span class="sxs-lookup"><span data-stu-id="bb54b-183">The first thing to notice is that each public property of `Hotel` corresponds to a field in the index definition, but with one crucial difference: The name of each field starts with a lower-case letter ("camel case"), while the name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="bb54b-184">Bu durum, hedef şemanın uygulama geliştiricisinin denetimi dışında kaldığı bir veri bağlamayı gerçekleştiren .NET uygulamalarında ortak bir senaryodur.</span><span class="sxs-lookup"><span data-stu-id="bb54b-184">This is a common scenario in .NET applications that perform data-binding where the target schema is outside the control of the application developer.</span></span> <span data-ttu-id="bb54b-185">Özellik adlarını ortası büyük harf yaparak .NET adlandırma yönergelerini bozmanın yerine, `[SerializePropertyNamesAsCamelCase]` özniteliğiyle SDK'nın özellik adlarını otomatik olarak ortası büyük harfle eşlenmesini söyleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb54b-185">Rather than having to violate the .NET naming guidelines by making property names camel-case, you can tell the SDK to map the property names to camel-case automatically with the `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="bb54b-186">Azure Search .NET SDK'sı, özel model nesnelerinizi JSON'a ve JSON'dan seri hale getirmek ve seri durumdan çıkarmak için [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) kitaplığını kullanır.</span><span class="sxs-lookup"><span data-stu-id="bb54b-186">The Azure Search .NET SDK uses the [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library to serialize and deserialize your custom model objects to and from JSON.</span></span> <span data-ttu-id="bb54b-187">Gerekirse bu seri hale getirmeyi özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb54b-187">You can customize this serialization if needed.</span></span> <span data-ttu-id="bb54b-188">Daha fazla bilgi için bkz. [JSON.NET ile Özel Serileştirme](search-howto-dotnet-sdk.md#JsonDotNet).</span><span class="sxs-lookup"><span data-stu-id="bb54b-188">You can find more details in [Custom Serialization with JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet).</span></span> <span data-ttu-id="bb54b-189">Bunun bir örneği, yukarıdaki örnek kodda `DescriptionFr` özelliğinde `[JsonProperty]` özniteliğinin kullanılmasıdır.</span><span class="sxs-lookup"><span data-stu-id="bb54b-189">One example of this is the use of the `[JsonProperty]` attribute on the `DescriptionFr` property in the sample code above.</span></span>
> 
> 

<span data-ttu-id="bb54b-190">`Hotel` sınıfı hakkında ikinci önemli şey, genel özelliklerin veri türleridir.</span><span class="sxs-lookup"><span data-stu-id="bb54b-190">The second important thing about the `Hotel` class are the data types of the public properties.</span></span> <span data-ttu-id="bb54b-191">Bu özelliklerin .NET türleri, dizin tanımında eşdeğer alan türleriyle eşlenir.</span><span class="sxs-lookup"><span data-stu-id="bb54b-191">The .NET types of these properties map to their equivalent field types in the index definition.</span></span> <span data-ttu-id="bb54b-192">Örneğin, `Category` dize özelliği `DataType.String` türündeki `category` alanına eşlenir.</span><span class="sxs-lookup"><span data-stu-id="bb54b-192">For example, the `Category` string property maps to the `category` field, which is of type `DataType.String`.</span></span> <span data-ttu-id="bb54b-193">`bool?` ve `DataType.Boolean`, `DateTimeOffset?` ve `DataType.DateTimeOffset`, vb. arasında benzer türde eşlemeler bulunur.</span><span class="sxs-lookup"><span data-stu-id="bb54b-193">There are similar type mappings between `bool?` and `DataType.Boolean`, `DateTimeOffset?` and `DataType.DateTimeOffset`, and so forth.</span></span> <span data-ttu-id="bb54b-194">Tür eşlemesine yönelik belirli kurallar, [Azure Search .NET SDK başvurusundaki](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_) `Documents.Get` yönteminde belirtilmiştir.</span><span class="sxs-lookup"><span data-stu-id="bb54b-194">The specific rules for the type mapping are documented with the `Documents.Get` method in the [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span>

<span data-ttu-id="bb54b-195">Kendi sınıflarınızı belge olarak kullanabilme iki yönde de işe yarar: [Sonraki makalede](search-query-dotnet.md) gösterildiği üzere, arama sonuçlarını da alabilir ve SDK'nın bunları otomatik olarak istediğiniz bir türe seri durumdan çıkarmasını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bb54b-195">This ability to use your own classes as documents works in both directions; You can also retrieve search results and have the SDK automatically deserialize them to a type of your choice, as shown in the [next article](search-query-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="bb54b-196">Azure Search .NET SDK'sı, alan adlarını alan değerlerine bir anahtar/değer eşlemesi olan `Document` sınıfını kullanarak dinamik tür belirtilmiş belgeleri de destekler.</span><span class="sxs-lookup"><span data-stu-id="bb54b-196">The Azure Search .NET SDK also supports dynamically-typed documents using the `Document` class, which is a key/value mapping of field names to field values.</span></span> <span data-ttu-id="bb54b-197">Bu durum, tasarım sırasında dizin şemasını bilmediğiniz veya belirli model sınıflarına bağlamanın kullanışlı olmayacağı senaryolarda kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="bb54b-197">This is useful in scenarios where you don't know the index schema at design-time, or where it would be inconvenient to bind to specific model classes.</span></span> <span data-ttu-id="bb54b-198">SDK'da belgelerle ilgili tüm yöntemler, `Document` sınıfıyla çalışan aşırı yüklerin yanı sıra genel türde bir parametre alan kesin tür belirtilmiş aşırı yüklere de sahiptir.</span><span class="sxs-lookup"><span data-stu-id="bb54b-198">All the methods in the SDK that deal with documents have overloads that work with the `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="bb54b-199">Bu makaledeki örnek kodda yalnızca ikinci durum kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bb54b-199">Only the latter are used in the sample code in this article.</span></span>
> 
> 

<span data-ttu-id="bb54b-200">**Neden boş değer atanabilir türleri kullanmalısınız?**</span><span class="sxs-lookup"><span data-stu-id="bb54b-200">**Why you should use nullable data types**</span></span>

<span data-ttu-id="bb54b-201">Bir Azure Search dizinine eşlemek için yeni model sınıflarınızı tasarlarken, `bool` ve `int` gibi değer türü özelliklerinin boş değer atanabilir (örneğin, `bool` yerine `bool?`) şeklinde bildirilmesini öneririz.</span><span class="sxs-lookup"><span data-stu-id="bb54b-201">When designing your own model classes to map to an Azure Search index, we recommend declaring properties of value types such as `bool` and `int` to be nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="bb54b-202">Boş değer atanamayan bir özellik kullanırsanız buna karşılık gelen alan için dizininizdeki hiçbir belgenin boş bir değer içermediğini **garanti etmeniz** gerekir.</span><span class="sxs-lookup"><span data-stu-id="bb54b-202">If you use a non-nullable property, you have to **guarantee** that no documents in your index contain a null value for the corresponding field.</span></span> <span data-ttu-id="bb54b-203">Bunu zorlamanıza ne SDK ne de Azure Search hizmeti yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="bb54b-203">Neither the SDK nor the Azure Search service will help you to enforce this.</span></span>

<span data-ttu-id="bb54b-204">Bu yalnızca kuramsal bir sorun değildir: Var olan `DataType.Int32` türünde bir dizine yeni bir alan eklediğiniz bir senaryoyu düşünün.</span><span class="sxs-lookup"><span data-stu-id="bb54b-204">This is not just a hypothetical concern: Imagine a scenario where you add a new field to an existing index that is of type `DataType.Int32`.</span></span> <span data-ttu-id="bb54b-205">Dizin tanımını güncelleştirdikten sonra, tüm belgelerin bu yeni alan için boş bir değeri olur (bunun nedeni, Azure Search'te tüm türlerin boş değer atanabilir olmasıdır).</span><span class="sxs-lookup"><span data-stu-id="bb54b-205">After updating the index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="bb54b-206">Ardından bu alan için boş değer atanamayan bir `int` özelliğiyle bir model sınıfı kullanırsanız belgeleri almaya çalışırken bunun gibi bir `JsonSerializationException` alırsınız:</span><span class="sxs-lookup"><span data-stu-id="bb54b-206">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying to retrieve documents:</span></span>

    Error converting value {null} to type 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="bb54b-207">Bu nedenle, en iyi uygulama olarak model sınıflarınızda boş değer atanabilir türler kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="bb54b-207">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb54b-208">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bb54b-208">Next steps</span></span>
<span data-ttu-id="bb54b-209">Azure Search dizininizi doldurduktan sonra, belgeleri aramak için sorgu göndermeye başlamaya hazır olursunuz.</span><span class="sxs-lookup"><span data-stu-id="bb54b-209">After populating your Azure Search index, you will be ready to start issuing queries to search for documents.</span></span> <span data-ttu-id="bb54b-210">Ayrıntılı bilgi için bkz. [Azure Search Dizininizi Sorgulama](search-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bb54b-210">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>

