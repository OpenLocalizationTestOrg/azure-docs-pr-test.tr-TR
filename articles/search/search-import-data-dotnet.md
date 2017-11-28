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
# <a name="upload-data-tooazure-search-using-hello-net-sdk"></a><span data-ttu-id="9836a-103">Karşıya veri tooAzure arama'yı kullanarak hello .NET SDK'sı</span><span class="sxs-lookup"><span data-stu-id="9836a-103">Upload data tooAzure Search using hello .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9836a-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="9836a-104">Overview</span></span>](search-what-is-data-import.md)
> * [<span data-ttu-id="9836a-105">.NET</span><span class="sxs-lookup"><span data-stu-id="9836a-105">.NET</span></span>](search-import-data-dotnet.md)
> * [<span data-ttu-id="9836a-106">REST</span><span class="sxs-lookup"><span data-stu-id="9836a-106">REST</span></span>](search-import-data-rest-api.md)
> 
> 

<span data-ttu-id="9836a-107">Bu makale size nasıl gösterir toouse hello [Azure Search .NET SDK'sı](https://aka.ms/search-sdk) tooimport verileri Azure Search dizini.</span><span class="sxs-lookup"><span data-stu-id="9836a-107">This article will show you how toouse hello [Azure Search .NET SDK](https://aka.ms/search-sdk) tooimport data into an Azure Search index.</span></span>

<span data-ttu-id="9836a-108">Bu kılavuza başlamadan önce bir [Azure Search dizini oluşturmuş](search-what-is-an-index.md) olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9836a-108">Before beginning this walkthrough, you should already have [created an Azure Search index](search-what-is-an-index.md).</span></span> <span data-ttu-id="9836a-109">Bu makalede, ayrıca, zaten oluşturduğunuzu varsayar bir `SearchServiceClient` gösterildiği gibi nesne [hello .NET SDK kullanarak Azure Search dizini oluşturma](search-create-index-dotnet.md#CreateSearchServiceClient).</span><span class="sxs-lookup"><span data-stu-id="9836a-109">This article also assumes that you have already created a `SearchServiceClient` object, as shown in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md#CreateSearchServiceClient).</span></span>

> [!NOTE]
> <span data-ttu-id="9836a-110">Bu makaledeki örnek kodun tamamı C# dilinde yazılmıştır.</span><span class="sxs-lookup"><span data-stu-id="9836a-110">All sample code in this article is written in C#.</span></span> <span data-ttu-id="9836a-111">Merhaba tam kaynak kodu bulabilirsiniz [github'da](http://aka.ms/search-dotnet-howto).</span><span class="sxs-lookup"><span data-stu-id="9836a-111">You can find hello full source code [on GitHub](http://aka.ms/search-dotnet-howto).</span></span> <span data-ttu-id="9836a-112">Merhaba hakkında bilgi edinebilirsiniz [Azure Search .NET SDK'sı](search-howto-dotnet-sdk.md) daha ayrıntılı ilerlemesi hello örnek kod için.</span><span class="sxs-lookup"><span data-stu-id="9836a-112">You can also read about hello [Azure Search .NET SDK](search-howto-dotnet-sdk.md) for a more detailed walk through of hello sample code.</span></span>

<span data-ttu-id="9836a-113">Sipariş toopush belgelerde hello .NET SDK kullanarak dizininizi içine yapmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="9836a-113">In order toopush documents into your index using hello .NET SDK, you will need to:</span></span>

1. <span data-ttu-id="9836a-114">Oluşturma bir `SearchIndexClient` nesne tooconnect tooyour arama dizini.</span><span class="sxs-lookup"><span data-stu-id="9836a-114">Create a `SearchIndexClient` object tooconnect tooyour search index.</span></span>
2. <span data-ttu-id="9836a-115">Oluşturma bir `IndexBatch` hello belgeleri toobe içeren eklenen değiştirilmiş veya silinmiş.</span><span class="sxs-lookup"><span data-stu-id="9836a-115">Create an `IndexBatch` containing hello documents toobe added, modified, or deleted.</span></span>
3. <span data-ttu-id="9836a-116">Merhaba çağrısı `Documents.Index` yöntemi, `SearchIndexClient` toosend hello `IndexBatch` tooyour arama dizini.</span><span class="sxs-lookup"><span data-stu-id="9836a-116">Call hello `Documents.Index` method of your `SearchIndexClient` toosend hello `IndexBatch` tooyour search index.</span></span>

## <a name="create-an-instance-of-hello-searchindexclient-class"></a><span data-ttu-id="9836a-117">Merhaba Searchındexclient sınıfının bir örneğini oluşturun</span><span class="sxs-lookup"><span data-stu-id="9836a-117">Create an instance of hello SearchIndexClient class</span></span>
<span data-ttu-id="9836a-118">Azure Search .NET SDK kullanarak dizini içine tooimport veri Merhaba, toocreate hello örneği gerekir `SearchIndexClient` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="9836a-118">tooimport data into your index using hello Azure Search .NET SDK, you will need toocreate an instance of hello `SearchIndexClient` class.</span></span> <span data-ttu-id="9836a-119">Zaten varsa, bu örneği kendiniz ancak, daha kolay oluşturabileceğiniz bir `SearchServiceClient` örneği toocall kendi `Indexes.GetClient` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="9836a-119">You can construct this instance yourself, but it's easier if you already have a `SearchServiceClient` instance toocall its `Indexes.GetClient` method.</span></span> <span data-ttu-id="9836a-120">Örneğin, işte nasıl elde edebilirsiniz bir `SearchIndexClient` hello dizini "hotels" adlı bir `SearchServiceClient` adlı `serviceClient`:</span><span class="sxs-lookup"><span data-stu-id="9836a-120">For example, here is how you would obtain a `SearchIndexClient` for hello index named "hotels" from a `SearchServiceClient` named `serviceClient`:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="9836a-121">Genel bir arama uygulamasında, dizin yönetimi ve popülasyon, arama sorgularından ayrı bir bileşen tarafından işlenir.</span><span class="sxs-lookup"><span data-stu-id="9836a-121">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="9836a-122">`Indexes.GetClient`kaydettiğinden bir dizini doldurmada kullanışlıdır hello başka sağlama sorun `SearchCredentials`.</span><span class="sxs-lookup"><span data-stu-id="9836a-122">`Indexes.GetClient` is convenient for populating an index because it saves you hello trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="9836a-123">Bunu Bu, kullanılan toocreate hello hello yönetici anahtarını geçirerek yapar `SearchServiceClient` toohello yeni `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="9836a-123">It does this by passing hello admin key that you used toocreate hello `SearchServiceClient` toohello new `SearchIndexClient`.</span></span> <span data-ttu-id="9836a-124">Ancak, uygulamanızın sorguları yürüten hello bölümünde daha iyi toocreate hello olmasından `SearchIndexClient` doğrudan böylece bir yönetici anahtarı yerine sorgu anahtarında geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9836a-124">However, in hello part of your application that executes queries, it is better toocreate hello `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="9836a-125">Bu hello ile tutarlıdır [en az ayrıcalık prensibi](https://en.wikipedia.org/wiki/Principle_of_least_privilege) ve uygulamanızı daha güvenli toomake yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="9836a-125">This is consistent with hello [principle of least privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege) and will help toomake your application more secure.</span></span> <span data-ttu-id="9836a-126">Yönetici anahtarları ve hello sorgu anahtarları hakkında daha fazla bilgi için [Azure Search REST API Başvurusu](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="9836a-126">You can find out more about admin keys and query keys in hello [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
> 
> 

<span data-ttu-id="9836a-127">`SearchIndexClient`, `Documents` özelliğine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="9836a-127">`SearchIndexClient` has a `Documents` property.</span></span> <span data-ttu-id="9836a-128">Bu özellik tooadd, gereken tüm hello yöntemleri değiştirmek, silmek veya belgeleri dizininize sorgu sağlar.</span><span class="sxs-lookup"><span data-stu-id="9836a-128">This property provides all hello methods you need tooadd, modify, delete, or query documents in your index.</span></span>

## <a name="decide-which-indexing-action-toouse"></a><span data-ttu-id="9836a-129">Hangi dizin oluşturma eylemini toouse karar verin</span><span class="sxs-lookup"><span data-stu-id="9836a-129">Decide which indexing action toouse</span></span>
<span data-ttu-id="9836a-130">Merhaba .NET SDK kullanarak tooimport veri verilerinizi toopackage ihtiyacınız olacak bir `IndexBatch` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="9836a-130">tooimport data using hello .NET SDK, you will need toopackage up your data into an `IndexBatch` object.</span></span> <span data-ttu-id="9836a-131">Bir `IndexBatch` koleksiyonunu yalıtır `IndexAction` nesneleri, her biri içeren bir belge ve hangi eylemini tooperform belge (karşıya yükleme, birleştirme, silme, vb.) Azure Search söyleyen bir özellik.</span><span class="sxs-lookup"><span data-stu-id="9836a-131">An `IndexBatch` encapsulates a collection of `IndexAction` objects, each of which contains a document and a property that tells Azure Search what action tooperform on that document (upload, merge, delete, etc).</span></span> <span data-ttu-id="9836a-132">Seçtiğiniz Eylemler aşağıda hello bağlı olarak, yalnızca belirli alanlar her belge için dahil edilmelidir:</span><span class="sxs-lookup"><span data-stu-id="9836a-132">Depending on which of hello below actions you choose, only certain fields must be included for each document:</span></span>

| <span data-ttu-id="9836a-133">Eylem</span><span class="sxs-lookup"><span data-stu-id="9836a-133">Action</span></span> | <span data-ttu-id="9836a-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9836a-134">Description</span></span> | <span data-ttu-id="9836a-135">Her bir belge için gerekli alanlar</span><span class="sxs-lookup"><span data-stu-id="9836a-135">Necessary fields for each document</span></span> | <span data-ttu-id="9836a-136">Notlar</span><span class="sxs-lookup"><span data-stu-id="9836a-136">Notes</span></span> |
| --- | --- | --- | --- |
| `Upload` |<span data-ttu-id="9836a-137">Bir `Upload` benzer tooan "upsert" nerede hello belgenin yeni olması durumunda ekleneceği ve olması mevcut durumunda güncelleştirileceği/değiştirileceği bir eylemdir.</span><span class="sxs-lookup"><span data-stu-id="9836a-137">An `Upload` action is similar tooan "upsert" where hello document will be inserted if it is new and updated/replaced if it exists.</span></span> |<span data-ttu-id="9836a-138">anahtar ve toodefine istediğiniz diğer alanlar</span><span class="sxs-lookup"><span data-stu-id="9836a-138">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="9836a-139">Güncelleştirme/var olan bir belgeyi değiştirirken, hello istekte belirtilen olmayan herhangi bir alan kendi alan çok kümesini sahip`null`.</span><span class="sxs-lookup"><span data-stu-id="9836a-139">When updating/replacing an existing document, any field that is not specified in hello request will have its field set too`null`.</span></span> <span data-ttu-id="9836a-140">Bu durum, hatta hello alan tooa null olmayan değer önceden ayarlandı oluşur.</span><span class="sxs-lookup"><span data-stu-id="9836a-140">This occurs even when hello field was previously set tooa non-null value.</span></span> |
| `Merge` |<span data-ttu-id="9836a-141">Varolan bir belge ile Merhaba güncelleştirmeleri alanları belirtilmiş.</span><span class="sxs-lookup"><span data-stu-id="9836a-141">Updates an existing document with hello specified fields.</span></span> <span data-ttu-id="9836a-142">Merhaba belge hello dizininde mevcut değilse hello birleştirme işlemi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="9836a-142">If hello document does not exist in hello index, hello merge will fail.</span></span> |<span data-ttu-id="9836a-143">anahtar ve toodefine istediğiniz diğer alanlar</span><span class="sxs-lookup"><span data-stu-id="9836a-143">key, plus any other fields you wish toodefine</span></span> |<span data-ttu-id="9836a-144">Birleştirmede belirttiğiniz herhangi bir alan varolan bir alana hello hello belgedeki yerini alır.</span><span class="sxs-lookup"><span data-stu-id="9836a-144">Any field you specify in a merge will replace hello existing field in hello document.</span></span> <span data-ttu-id="9836a-145">Buna `DataType.Collection(DataType.String)` türünde alanlar dahildir.</span><span class="sxs-lookup"><span data-stu-id="9836a-145">This includes fields of type `DataType.Collection(DataType.String)`.</span></span> <span data-ttu-id="9836a-146">Örneğin, hello belge bir alanı varsa, `tags` değerle `["budget"]` ve değeriyle bir birleştirme yürütme `["economy", "pool"]` için `tags`, hello hello son değerini `tags` alan `["economy", "pool"]`.</span><span class="sxs-lookup"><span data-stu-id="9836a-146">For example, if hello document contains a field `tags` with value `["budget"]` and you execute a merge with value `["economy", "pool"]` for `tags`, hello final value of hello `tags` field will be `["economy", "pool"]`.</span></span> <span data-ttu-id="9836a-147">`["budget", "economy", "pool"]` olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="9836a-147">It will not be `["budget", "economy", "pool"]`.</span></span> |
| `MergeOrUpload` |<span data-ttu-id="9836a-148">Bu eylem gibi davranır `Merge` anahtar zaten verilen hello belgeyle hello dizinde varsa.</span><span class="sxs-lookup"><span data-stu-id="9836a-148">This action behaves like `Merge` if a document with hello given key already exists in hello index.</span></span> <span data-ttu-id="9836a-149">Merhaba belge mevcut değilse gibi davranır `Upload` yeni bir belgeyle.</span><span class="sxs-lookup"><span data-stu-id="9836a-149">If hello document does not exist, it behaves like `Upload` with a new document.</span></span> |<span data-ttu-id="9836a-150">anahtar ve toodefine istediğiniz diğer alanlar</span><span class="sxs-lookup"><span data-stu-id="9836a-150">key, plus any other fields you wish toodefine</span></span> |- |
| `Delete` |<span data-ttu-id="9836a-151">Merhaba belirtilen belge hello dizinden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="9836a-151">Removes hello specified document from hello index.</span></span> |<span data-ttu-id="9836a-152">yalnızca anahtar</span><span class="sxs-lookup"><span data-stu-id="9836a-152">key only</span></span> |<span data-ttu-id="9836a-153">Merhaba anahtar alanı yoksayılacak dışında belirttiğiniz tüm alanlar.</span><span class="sxs-lookup"><span data-stu-id="9836a-153">Any fields you specify other than hello key field will be ignored.</span></span> <span data-ttu-id="9836a-154">Bir belgeden tek bir alanı tooremove istiyorsanız kullanın `Merge` yerine ve basit şekilde hello alan açık olarak ayarlanıp toonull.</span><span class="sxs-lookup"><span data-stu-id="9836a-154">If you want tooremove an individual field from a document, use `Merge` instead and simply set hello field explicitly toonull.</span></span> |

<span data-ttu-id="9836a-155">Hangi eylemini toouse ile istediğiniz belirtebilirsiniz hello çeşitli statik yöntemlerini hello `IndexBatch` ve `IndexAction` hello sonraki bölümde gösterildiği gibi sınıflar.</span><span class="sxs-lookup"><span data-stu-id="9836a-155">You can specify what action you want toouse with hello various static methods of hello `IndexBatch` and `IndexAction` classes, as shown in hello next section.</span></span>

## <a name="construct-your-indexbatch"></a><span data-ttu-id="9836a-156">IndexBatch'inizi oluşturma</span><span class="sxs-lookup"><span data-stu-id="9836a-156">Construct your IndexBatch</span></span>
<span data-ttu-id="9836a-157">Belgelerinizde hangi eylemleri tooperform bildiğinize göre hazır tooconstruct hello olan `IndexBatch`.</span><span class="sxs-lookup"><span data-stu-id="9836a-157">Now that you know which actions tooperform on your documents, you are ready tooconstruct hello `IndexBatch`.</span></span> <span data-ttu-id="9836a-158">gösterir aşağıdaki örnekte nasıl hello toocreate birkaç farklı eylemler ile bir toplu iş.</span><span class="sxs-lookup"><span data-stu-id="9836a-158">hello example below shows how toocreate a batch with a few different actions.</span></span> <span data-ttu-id="9836a-159">Bizim örneğimizde adlı özel bir sınıf kullandığına dikkat edin `Hotel` hello "hotels" dizininin tooa belgede eşler.</span><span class="sxs-lookup"><span data-stu-id="9836a-159">Note that our example uses a custom class called `Hotel` that maps tooa document in hello "hotels" index.</span></span>

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

<span data-ttu-id="9836a-160">Bu durumda, kullanıyoruz `Upload`, `MergeOrUpload`, ve `Delete` üzerinde hello adlı hello yöntemler tarafından belirtildiği gibi arama eylemlerimiz olarak `IndexAction` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="9836a-160">In this case, we are using `Upload`, `MergeOrUpload`, and `Delete` as our search actions, as specified by hello methods called on hello `IndexAction` class.</span></span>

<span data-ttu-id="9836a-161">Bu "hotels" dizini örneğinin, birçok belgeyle önceden doldurulduğunu varsayın.</span><span class="sxs-lookup"><span data-stu-id="9836a-161">Assume that this example "hotels" index is already populated with a number of documents.</span></span> <span data-ttu-id="9836a-162">Nasıl biz toospecify tüm hello olası belge alanlarını kullanırken sahip değildi Not `MergeOrUpload` ve yalnızca hello belge anahtarını belirttiğimize (`HotelId`) kullanırken `Delete`.</span><span class="sxs-lookup"><span data-stu-id="9836a-162">Note how we did not have toospecify all hello possible document fields when using `MergeOrUpload` and how we only specified hello document key (`HotelId`) when using `Delete`.</span></span>

<span data-ttu-id="9836a-163">Ayrıca, yalnızca tek bir dizin oluşturma isteğine too1000 belgelerde yukarı dahil edebileceğinizi unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9836a-163">Also, note that you can only include up too1000 documents in a single indexing request.</span></span>

> [!NOTE]
> <span data-ttu-id="9836a-164">Bu örnekte, farklı eylemler toodifferent belgelerini uyguladığımız.</span><span class="sxs-lookup"><span data-stu-id="9836a-164">In this example, we are applying different actions toodifferent documents.</span></span> <span data-ttu-id="9836a-165">İsterseniz tooperform hello aynı eylemleri çağırmak yerine hello toplu işteki tüm belgeler arasında `IndexBatch.New`, kullanabileceğinizi diğer statik yöntemlerini hello `IndexBatch`.</span><span class="sxs-lookup"><span data-stu-id="9836a-165">If you wanted tooperform hello same actions across all documents in hello batch, instead of calling `IndexBatch.New`, you could use hello other static methods of `IndexBatch`.</span></span> <span data-ttu-id="9836a-166">Örneğin; `IndexBatch.Merge`, `IndexBatch.MergeOrUpload` ve `IndexBatch.Delete` çağırarak toplu işlemler oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9836a-166">For example, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete`.</span></span> <span data-ttu-id="9836a-167">Bu yöntemler, `IndexAction` nesneleri yerine bir belge koleksiyonu (bu örnekte `Hotel` türünde nesneler) alır.</span><span class="sxs-lookup"><span data-stu-id="9836a-167">These methods take a collection of documents (objects of type `Hotel` in this example) instead of `IndexAction` objects.</span></span>
> 
> 

## <a name="import-data-toohello-index"></a><span data-ttu-id="9836a-168">İçeri aktarma veri toohello dizini</span><span class="sxs-lookup"><span data-stu-id="9836a-168">Import data toohello index</span></span>
<span data-ttu-id="9836a-169">Başlatılan bir sahip olduğunuza `IndexBatch` nesne gönderebilirsiniz, toohello dizin çağırarak `Documents.Index` üzerinde `SearchIndexClient` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="9836a-169">Now that you have an initialized `IndexBatch` object, you can send it toohello index by calling `Documents.Index` on your `SearchIndexClient` object.</span></span> <span data-ttu-id="9836a-170">örnekte gösterildiği nasıl aşağıdaki hello toocall `Index`, yanı sıra bazı ek adımlar tooperform gerekir:</span><span class="sxs-lookup"><span data-stu-id="9836a-170">hello following example shows how toocall `Index`, as well as some extra steps you will need tooperform:</span></span>

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

<span data-ttu-id="9836a-171">Not hello `try` / `catch` hello çağrısı toohello çevreleyen `Index` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="9836a-171">Note hello `try`/`catch` surrounding hello call toohello `Index` method.</span></span> <span data-ttu-id="9836a-172">Merhaba catch bloğu, dizin oluşturma için önemli bir hata durumunu işler.</span><span class="sxs-lookup"><span data-stu-id="9836a-172">hello catch block handles an important error case for indexing.</span></span> <span data-ttu-id="9836a-173">Azure Search hizmetinizin hello bazıları belgeleri hello toplu işlemde tooindex başarısız olursa bir `IndexBatchException` tarafından oluşturulan `Documents.Index`.</span><span class="sxs-lookup"><span data-stu-id="9836a-173">If your Azure Search service fails tooindex some of hello documents in hello batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="9836a-174">Bu durum, hizmetiniz ağır yük altındayken belgelere dizin oluşturuyorsanız oluşabilir.</span><span class="sxs-lookup"><span data-stu-id="9836a-174">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="9836a-175">**Bu durumu, kodunuzda açık şekilde işlemenizi kesinlikle öneririz.**</span><span class="sxs-lookup"><span data-stu-id="9836a-175">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="9836a-176">Gecikme ve başarısız olan dizin hello belge yeniden deneyin veya oturum ve hello örnek vermez veya uygulamanızın veri tutarlılığı gereksinimlerine bağlı olarak başka bir şey yapabilirsiniz gibi devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9836a-176">You can delay and then retry indexing hello documents that failed, or you can log and continue like hello sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

<span data-ttu-id="9836a-177">Son olarak, yukarıdaki hello örnekteki kod iki saniye hello.</span><span class="sxs-lookup"><span data-stu-id="9836a-177">Finally, hello code in hello example above delays for two seconds.</span></span> <span data-ttu-id="9836a-178">Merhaba örnek uygulaması toowait hello belgelerin aramada kullanılabilir kısa bir süre tooensure gerekir böylece dizin oluşturma Azure Search hizmetinizin zaman uyumsuz olarak gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="9836a-178">Indexing happens asynchronously in your Azure Search service, so hello sample application needs toowait a short time tooensure that hello documents are available for searching.</span></span> <span data-ttu-id="9836a-179">Bu gibi gecikmeler genellikle yalnızca gösterilerde, testlerde ve örnek uygulamalarda gereklidir.</span><span class="sxs-lookup"><span data-stu-id="9836a-179">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

<a name="HotelClass"></a>

### <a name="how-hello-net-sdk-handles-documents"></a><span data-ttu-id="9836a-180">Merhaba .NET SDK belgeleri nasıl işler?</span><span class="sxs-lookup"><span data-stu-id="9836a-180">How hello .NET SDK handles documents</span></span>
<span data-ttu-id="9836a-181">Size nasıl hello Azure Search .NET SDK'sı gibi kullanıcı tanımlı bir sınıf örneklerini mümkün tooupload merak ediyor olabilirsiniz `Hotel` toohello dizini.</span><span class="sxs-lookup"><span data-stu-id="9836a-181">You may be wondering how hello Azure Search .NET SDK is able tooupload instances of a user-defined class like `Hotel` toohello index.</span></span> <span data-ttu-id="9836a-182">toohelp bu sorunun yanıtlanmasına, hello bakalım `Hotel` tanımlanan toohello dizin şemasını eşlemeleri sınıfı [hello .NET SDK kullanarak Azure Search dizini oluşturma](search-create-index-dotnet.md#DefineIndex):</span><span class="sxs-lookup"><span data-stu-id="9836a-182">toohelp answer that question, let's look at hello `Hotel` class, which maps toohello index schema defined in [Create an Azure Search index using hello .NET SDK](search-create-index-dotnet.md#DefineIndex):</span></span>

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

<span data-ttu-id="9836a-183">Merhaba ilk şey toonotice her ortak özelliği olan `Hotel` tooa alan hello dizin tanımı, ancak çok önemli bir fark karşılık gelir: her alanı hello adını küçük harfle ("ortası büyük harf"), her ortak hello adını sırasında başlatır özelliği `Hotel` büyük harfle ("Pascal büyük") başlar.</span><span class="sxs-lookup"><span data-stu-id="9836a-183">hello first thing toonotice is that each public property of `Hotel` corresponds tooa field in hello index definition, but with one crucial difference: hello name of each field starts with a lower-case letter ("camel case"), while hello name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="9836a-184">Bu, hello hedef şema hello uygulama geliştiricisi dış hello denetimin olduğu veri bağlamayı gerçekleştiren .NET uygulamalarında ortak bir senaryodur.</span><span class="sxs-lookup"><span data-stu-id="9836a-184">This is a common scenario in .NET applications that perform data-binding where hello target schema is outside hello control of hello application developer.</span></span> <span data-ttu-id="9836a-185">Adlandırma yönergeleri özellik adlarını ortası büyük harf yaparak tooviolate hello .NET sahip olmak yerine hello SDK toomap hello özellik adları toocamel harf hello ile otomatik olarak anlayabilirsiniz `[SerializePropertyNamesAsCamelCase]` özniteliği.</span><span class="sxs-lookup"><span data-stu-id="9836a-185">Rather than having tooviolate hello .NET naming guidelines by making property names camel-case, you can tell hello SDK toomap hello property names toocamel-case automatically with hello `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="9836a-186">Hello Azure Search .NET SDK'sını kullanır hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) kitaplığı tooserialize ve, özel model nesneleri tooand json'dan seri durumdan.</span><span class="sxs-lookup"><span data-stu-id="9836a-186">hello Azure Search .NET SDK uses hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library tooserialize and deserialize your custom model objects tooand from JSON.</span></span> <span data-ttu-id="9836a-187">Gerekirse bu seri hale getirmeyi özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9836a-187">You can customize this serialization if needed.</span></span> <span data-ttu-id="9836a-188">Daha fazla bilgi için bkz. [JSON.NET ile Özel Serileştirme](search-howto-dotnet-sdk.md#JsonDotNet).</span><span class="sxs-lookup"><span data-stu-id="9836a-188">You can find more details in [Custom Serialization with JSON.NET](search-howto-dotnet-sdk.md#JsonDotNet).</span></span> <span data-ttu-id="9836a-189">Bunun bir örneği olan hello hello kullanımını `[JsonProperty]` hello öznitelikte `DescriptionFr` yukarıdaki hello örnek kod bir özellik.</span><span class="sxs-lookup"><span data-stu-id="9836a-189">One example of this is hello use of hello `[JsonProperty]` attribute on hello `DescriptionFr` property in hello sample code above.</span></span>
> 
> 

<span data-ttu-id="9836a-190">Merhaba hakkında ikinci önemli şey Hello `Hotel` sınıfı hello genel özelliklerin hello veri türleri bulunur.</span><span class="sxs-lookup"><span data-stu-id="9836a-190">hello second important thing about hello `Hotel` class are hello data types of hello public properties.</span></span> <span data-ttu-id="9836a-191">Bu özelliklerin Hello .NET türleri tootheir hello dizin tanımında eşdeğer alan türleriyle eşlenir.</span><span class="sxs-lookup"><span data-stu-id="9836a-191">hello .NET types of these properties map tootheir equivalent field types in hello index definition.</span></span> <span data-ttu-id="9836a-192">Örneğin, hello `Category` dize özelliği eşlemeleri toohello `category` türü alan `DataType.String`.</span><span class="sxs-lookup"><span data-stu-id="9836a-192">For example, hello `Category` string property maps toohello `category` field, which is of type `DataType.String`.</span></span> <span data-ttu-id="9836a-193">`bool?` ve `DataType.Boolean`, `DateTimeOffset?` ve `DataType.DateTimeOffset`, vb. arasında benzer türde eşlemeler bulunur.</span><span class="sxs-lookup"><span data-stu-id="9836a-193">There are similar type mappings between `bool?` and `DataType.Boolean`, `DateTimeOffset?` and `DataType.DateTimeOffset`, and so forth.</span></span> <span data-ttu-id="9836a-194">Merhaba hello tür eşlemesi için belirli kurallar ile Merhaba belgelenmiştir `Documents.Get` hello yönteminde [Azure Search .NET SDK'sı başvurusu](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span><span class="sxs-lookup"><span data-stu-id="9836a-194">hello specific rules for hello type mapping are documented with hello `Documents.Get` method in hello [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span>

<span data-ttu-id="9836a-195">Bu özelliği toouse her iki yönde de kendi sınıflarınızı belge olarak çalışır; Ayrıca arama sonuçları almak ve sahip hello SDK otomatik olarak seri durumdan bunları tooa türü tercih ettiğiniz hello gösterildiği gibi [sonraki makalede](search-query-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="9836a-195">This ability toouse your own classes as documents works in both directions; You can also retrieve search results and have hello SDK automatically deserialize them tooa type of your choice, as shown in hello [next article](search-query-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9836a-196">Hello Azure Search .NET SDK'sı hello kullanarak dinamik tür belirtilmiş belgeleri de destekler `Document` bir anahtar/değer eşlemesi alan adları toofield değerlerinin sınıfı.</span><span class="sxs-lookup"><span data-stu-id="9836a-196">hello Azure Search .NET SDK also supports dynamically-typed documents using hello `Document` class, which is a key/value mapping of field names toofield values.</span></span> <span data-ttu-id="9836a-197">Bu tasarım zamanında hello dizin şemasını bilmediğiniz veya kullanışsız toobind toospecific modeli sınıfları olmayacağı senaryolarda kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="9836a-197">This is useful in scenarios where you don't know hello index schema at design-time, or where it would be inconvenient toobind toospecific model classes.</span></span> <span data-ttu-id="9836a-198">Merhaba SDK ilgili tüm hello yöntemler hello ile çalışan aşırı yüklerin `Document` sınıfı yanı sıra genel türde bir parametre alan kesin tür belirtilmiş aşırı.</span><span class="sxs-lookup"><span data-stu-id="9836a-198">All hello methods in hello SDK that deal with documents have overloads that work with hello `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="9836a-199">Yalnızca ikinci Merhaba, bu makaledeki örnek kod hello kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9836a-199">Only hello latter are used in hello sample code in this article.</span></span>
> 
> 

<span data-ttu-id="9836a-200">**Neden boş değer atanabilir türleri kullanmalısınız?**</span><span class="sxs-lookup"><span data-stu-id="9836a-200">**Why you should use nullable data types**</span></span>

<span data-ttu-id="9836a-201">Kendi model sınıfları toomap tooan Azure Search dizininizi tasarlarken gibi özellikleri değer türlerini bildirme öneririz `bool` ve `int` toobe boş değer atanabilir (örneğin, `bool?` yerine `bool`).</span><span class="sxs-lookup"><span data-stu-id="9836a-201">When designing your own model classes toomap tooan Azure Search index, we recommend declaring properties of value types such as `bool` and `int` toobe nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="9836a-202">Atanamayan bir özellik kullanırsanız, çok sahip**garanti** hiçbir belgeleri dizininize hello karşılık gelen alan için bir null değer içeriyor.</span><span class="sxs-lookup"><span data-stu-id="9836a-202">If you use a non-nullable property, you have too**guarantee** that no documents in your index contain a null value for hello corresponding field.</span></span> <span data-ttu-id="9836a-203">Merhaba SDK ne hello Azure Search hizmeti, tooenforce bu yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="9836a-203">Neither hello SDK nor hello Azure Search service will help you tooenforce this.</span></span>

<span data-ttu-id="9836a-204">Bu yalnızca kuramsal bir sorun değildir: türü olan yeni bir alan tooan mevcut dizin eklediğiniz bir senaryoyu düşünün `DataType.Int32`.</span><span class="sxs-lookup"><span data-stu-id="9836a-204">This is not just a hypothetical concern: Imagine a scenario where you add a new field tooan existing index that is of type `DataType.Int32`.</span></span> <span data-ttu-id="9836a-205">(Tüm türleri Azure Search'te boş değer atanabilir olmasıdır) hello dizin tanımını güncelleştirdikten sonra bu yeni alan için bir null değer tüm belgeler olacaktır.</span><span class="sxs-lookup"><span data-stu-id="9836a-205">After updating hello index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="9836a-206">Ardından bir model sınıfı bir null ile kullanırsanız `int` özelliği bu alan için elde edersiniz bir `JsonSerializationException` şöyle tooretrieve belgeleri çalışırken:</span><span class="sxs-lookup"><span data-stu-id="9836a-206">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying tooretrieve documents:</span></span>

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="9836a-207">Bu nedenle, en iyi uygulama olarak model sınıflarınızda boş değer atanabilir türler kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="9836a-207">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9836a-208">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9836a-208">Next steps</span></span>
<span data-ttu-id="9836a-209">Azure Search dizininizi doldurduktan sonra belgeler için sorguları toosearch veren hazır toostart olacaktır.</span><span class="sxs-lookup"><span data-stu-id="9836a-209">After populating your Azure Search index, you will be ready toostart issuing queries toosearch for documents.</span></span> <span data-ttu-id="9836a-210">Ayrıntılı bilgi için bkz. [Azure Search Dizininizi Sorgulama](search-query-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9836a-210">See [Query Your Azure Search Index](search-query-overview.md) for details.</span></span>

