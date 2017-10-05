---
title: "Yaşam süresi Azure Cosmos veritabanı verileriyle sona | Microsoft Docs"
description: "TTL ile Microsoft Azure Cosmos DB sistemden bir süre sonra otomatik olarak temizlenir dosyalarınız olanağı sağlar."
services: cosmos-db
documentationcenter: 
keywords: "yaşam süresi"
author: arramac
manager: jhubbard
editor: 
ms.assetid: 25fcbbda-71f7-414a-bf57-d8671358ca3f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: arramac
ms.openlocfilehash: 6f1c43ca0113dc7579b0fc3743d3314c16ce78a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="expire-data-in-azure-cosmos-db-collections-automatically-with-time-to-live"></a><span data-ttu-id="1b1e5-104">Otomatik olarak süresi ile Azure Cosmos DB koleksiyonlarda verileri süresi dolacak</span><span class="sxs-lookup"><span data-stu-id="1b1e5-104">Expire data in Azure Cosmos DB collections automatically with time to live</span></span>
<span data-ttu-id="1b1e5-105">Uygulamalar oluşturmak ve çok büyük miktarda veri depolayın.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-105">Applications can produce and store vast amounts of data.</span></span> <span data-ttu-id="1b1e5-106">Bu veriler, bazı bilgiler yalnızca sınırlı bir süre için yararlıdır oluşturulan makine olay verileri, günlükler ve kullanıcı oturumu ister.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-106">Some of this data, like machine generated event data, logs, and user session information is only useful for a finite period of time.</span></span> <span data-ttu-id="1b1e5-107">Veri olduktan sonra uygulamanızın gereksinimlerine fazlalık, bu verileri temizlemek ve bir uygulamanın depolama gereksinimlerini azaltmak güvenlidir.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-107">Once the data becomes surplus to the needs of the application it is safe to purge this data and reduce the storage needs of an application.</span></span>

<span data-ttu-id="1b1e5-108">"Yaşam süresi" veya TTL ile Microsoft Azure Cosmos DB veritabanından bir süre sonra otomatik olarak temizlenir dosyalarınız olanağı sağlar.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-108">With "time to live" or TTL, Microsoft Azure Cosmos DB provides the ability to have documents automatically purged from the database after a period of time.</span></span> <span data-ttu-id="1b1e5-109">Varsayılan yaşam süresi koleksiyon düzeyinde ayarlamak ve bir belge başına temelinde geçersiz kılındı.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-109">The default time to live can be set at the collection level, and overridden on a per-document basis.</span></span> <span data-ttu-id="1b1e5-110">Bir koleksiyonu varsayılan olarak veya bir belge düzeyinde TTL ayarlandıktan sonra Cosmos DB son değiştirildiği olduğundan, bu süre, saniye sonra mevcut belgeleri otomatik olarak kaldırır.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-110">Once TTL is set, either as a collection default or at a document level, Cosmos DB will automatically remove documents that exist after that period of time, in seconds, since they were last modified.</span></span>

<span data-ttu-id="1b1e5-111">Cosmos DB'de yaşam süresi belgenin en son değiştirildiği bir uzaklık karşı kullanır.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-111">Time to live in Cosmos DB uses an offset against when the document was last modified.</span></span> <span data-ttu-id="1b1e5-112">Bunu kullandığı yapmak için `_ts` her belge üzerinde var olan alan.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-112">To do this it uses the `_ts` field which exists on every document.</span></span> <span data-ttu-id="1b1e5-113">Tarih ve saatini temsil eden bir UNIX stili dönem zaman damgası _ts alanıdır.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-113">The _ts field is a unix-style epoch timestamp representing the date and time.</span></span> <span data-ttu-id="1b1e5-114">`_ts` Alanı her zaman bir belge değiştirildiğinde güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-114">The `_ts` field is updated every time a document is modified.</span></span> 

## <a name="ttl-behavior"></a><span data-ttu-id="1b1e5-115">TTL davranışı</span><span class="sxs-lookup"><span data-stu-id="1b1e5-115">TTL behavior</span></span>
<span data-ttu-id="1b1e5-116">TTL özelliği, iki düzeyde - koleksiyon düzeyinde ve belge düzeyi TTL özellikleri tarafından denetlenir.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-116">The TTL feature is controlled by TTL properties at two levels - the collection level and the document level.</span></span> <span data-ttu-id="1b1e5-117">Saniye cinsinden ayarlanır ve bir delta olarak kabul edilir. değerler `_ts` belgeyi son değiştirilme saati.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-117">The values are set in seconds and are treated as a delta from the `_ts` that the document was last modified at.</span></span>

1. <span data-ttu-id="1b1e5-118">Koleksiyon için DefaultTTL</span><span class="sxs-lookup"><span data-stu-id="1b1e5-118">DefaultTTL for the collection</span></span>
   
   * <span data-ttu-id="1b1e5-119">Eksikse (veya null olarak ayarlanır) belgeleri otomatik olarak silinmez.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-119">If missing (or set to null), documents are not deleted automatically.</span></span>
   * <span data-ttu-id="1b1e5-120">Mevcut değer ise "-1" sonsuz – = belgeleri varsayılan olarak süresi yok</span><span class="sxs-lookup"><span data-stu-id="1b1e5-120">If present and the value is "-1" = infinite – documents don’t expire by default</span></span>
   * <span data-ttu-id="1b1e5-121">Mevcut ve değeri bir numara ("n") – belgelerin süresi dolsun varsa "n" son değişikliğinden sonra saniye</span><span class="sxs-lookup"><span data-stu-id="1b1e5-121">If present and the value is some number ("n") – documents expire "n” seconds after last modification</span></span>
2. <span data-ttu-id="1b1e5-122">TTL belgeler için:</span><span class="sxs-lookup"><span data-stu-id="1b1e5-122">TTL for the documents:</span></span> 
   
   * <span data-ttu-id="1b1e5-123">Özelliği, yalnızca DefaultTTL üst koleksiyonu için mevcut olduğunda geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-123">Property is applicable only if DefaultTTL is present for the parent collection.</span></span>
   * <span data-ttu-id="1b1e5-124">Üst koleksiyonun DefaultTTL değerini geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-124">Overrides the DefaultTTL value for the parent collection.</span></span>

<span data-ttu-id="1b1e5-125">Belgenin süresi doldu hemen (`ttl`  +  `_ts` > geçerli sunucu zamanı =), belgenin "süresi"olarak işaretlenmiş.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-125">As soon as the document has expired (`ttl` + `_ts` >= current server time), the document is marked as "expired”.</span></span> <span data-ttu-id="1b1e5-126">Bu tarihten sonra bu belgeler üzerinde hiçbir işlem izin verilecek ve gerçekleştirilen herhangi bir sorgu sonuçlarından bırakılır.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-126">No operation will be allowed on these documents after this time and they will be excluded from the results of any queries performed.</span></span> <span data-ttu-id="1b1e5-127">Belgeleri sistemde fiziksel olarak silinir ve arka planda mümkün daha sonra silinir.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-127">The documents are physically deleted in the system, and are deleted in the background opportunistically at a later time.</span></span> <span data-ttu-id="1b1e5-128">Bu kullanılmasına neden değil [istek birimlerine (RUs)](request-units.md) koleksiyonu bütçeden.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-128">This does not consume any [Request Units (RUs)](request-units.md) from the collection budget.</span></span>

<span data-ttu-id="1b1e5-129">Yukarıdaki mantığı aşağıdaki matrisinde gösterilebilir:</span><span class="sxs-lookup"><span data-stu-id="1b1e5-129">The above logic can be shown in the following matrix:</span></span>

|  | <span data-ttu-id="1b1e5-130">DefaultTTL eksik değil koleksiyonda ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-130">DefaultTTL missing/not set on the collection</span></span> | <span data-ttu-id="1b1e5-131">DefaultTTL = -1 koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="1b1e5-131">DefaultTTL = -1 on collection</span></span> | <span data-ttu-id="1b1e5-132">DefaultTTL koleksiyonunda "n" =</span><span class="sxs-lookup"><span data-stu-id="1b1e5-132">DefaultTTL = "n" on collection</span></span> |
| --- |:--- |:--- |:--- |
| <span data-ttu-id="1b1e5-133">TTL eksik belgesi</span><span class="sxs-lookup"><span data-stu-id="1b1e5-133">TTL Missing on document</span></span> |<span data-ttu-id="1b1e5-134">Belge ve koleksiyon TTL kavramına sahip olduğundan belge düzeyinde geçersiz kılmak için bir şey yok.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-134">Nothing to override at document level since both the document and collection have no concept of TTL.</span></span> |<span data-ttu-id="1b1e5-135">Bu koleksiyonun hiç belgelerde sona erecek.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-135">No documents in this collection will expire.</span></span> |<span data-ttu-id="1b1e5-136">Bu koleksiyon belgelerde aralığı n sona erdiğinde sona erecek.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-136">The documents in this collection will expire when interval n elapses.</span></span> |
| <span data-ttu-id="1b1e5-137">TTL belgesinde -1 =</span><span class="sxs-lookup"><span data-stu-id="1b1e5-137">TTL = -1 on document</span></span> |<span data-ttu-id="1b1e5-138">Belge düzeyinde toplamadan beri geçersiz kılmak için hiçbir şey bir belge kılabilirsiniz DefaultTTL özelliği tanımlamıyor.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-138">Nothing to override at the document level since the collection doesn’t define the DefaultTTL property that a document can override.</span></span> <span data-ttu-id="1b1e5-139">TTL belgesinde sistem tarafından yorumlanan kaydetmeyin.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-139">TTL on a document is un-interpreted by the system.</span></span> |<span data-ttu-id="1b1e5-140">Bu koleksiyonun hiç belgelerde sona erecek.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-140">No documents in this collection will expire.</span></span> |<span data-ttu-id="1b1e5-141">TTL =-1'de bu koleksiyonun belgeyle asla sona erecek.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-141">The document with TTL=-1 in this collection will never expire.</span></span> <span data-ttu-id="1b1e5-142">Diğer tüm belgeler "n" aralığından sonra sona erecek.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-142">All other documents will expire after "n" interval.</span></span> |
| <span data-ttu-id="1b1e5-143">TTL belgesinde n =</span><span class="sxs-lookup"><span data-stu-id="1b1e5-143">TTL = n on document</span></span> |<span data-ttu-id="1b1e5-144">Belge düzeyinde geçersiz kılmak için bir şey yok.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-144">Nothing to override at the document level.</span></span> <span data-ttu-id="1b1e5-145">Bir belge üzerinde TTL sistem tarafından yorumlanan kaydetmeyin.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-145">TTL on a document in un-interpreted by the system.</span></span> |<span data-ttu-id="1b1e5-146">TTL belgeyle = n saniye cinsinden aralık n sonra dolacak.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-146">The document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="1b1e5-147">Diğer belgeleri -1 aralığı devralır ve süresi dolmayacak.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-147">Other documents will inherit interval of -1 and never expire.</span></span> |<span data-ttu-id="1b1e5-148">TTL belgeyle = n saniye cinsinden aralık n sonra dolacak.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-148">The document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="1b1e5-149">Diğer belgeler "n" aralığı koleksiyondan devralır.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-149">Other documents will inherit "n" interval from the collection.</span></span> |

## <a name="configuring-ttl"></a><span data-ttu-id="1b1e5-150">TTL yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1b1e5-150">Configuring TTL</span></span>
<span data-ttu-id="1b1e5-151">Varsayılan olarak, yaşam süresi tüm Cosmos DB koleksiyonlarında ve tüm belgeler üzerinde varsayılan olarak devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-151">By default, time to live is disabled by default in all Cosmos DB collections and on all documents.</span></span>

## <a name="enabling-ttl"></a><span data-ttu-id="1b1e5-152">TTL etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="1b1e5-152">Enabling TTL</span></span>
<span data-ttu-id="1b1e5-153">Bir koleksiyon veya bir koleksiyon içindeki belgelerde TTL etkinleştirmek için bir koleksiyonun DefaultTTL özelliğini -1 veya sıfır olmayan pozitif bir sayı için ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-153">To enable TTL on a collection, or the documents within a collection, you need to set the DefaultTTL property of a collection to either -1 or a non-zero positive number.</span></span> <span data-ttu-id="1b1e5-154">DefaultTTL-1 koleksiyondaki tüm belgeleri sonsuza kadar Canlı varsayılan ancak Cosmos DB hizmeti tarafından olarak ayarlandığında bu koleksiyon, bu varsayılanı geçersiz belgeler için izlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-154">Setting the DefaultTTL to -1 means that by default all documents in the collection will live forever but the Cosmos DB service should monitor this collection for documents that have overridden this default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive =-1; //never expire by default

    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(databaseName),
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });

## <a name="configuring-default-ttl-on-a-collection"></a><span data-ttu-id="1b1e5-155">Bir koleksiyonda varsayılan TTL yapılandırma</span><span class="sxs-lookup"><span data-stu-id="1b1e5-155">Configuring default TTL on a collection</span></span>
<span data-ttu-id="1b1e5-156">Bir varsayılan koleksiyon düzeyinde yaşam süresi yapılandırmadı.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-156">You are able to configure a default time to live at a collection level.</span></span> <span data-ttu-id="1b1e5-157">Bir koleksiyonda TTL ayarlamak için zaman damgası belgenin son değiştiren sonra koleksiyondaki tüm belgeleri süresi dolacak şekilde saniye cinsinden süre gösteren sıfır olmayan pozitif bir sayı sağlamanız gerekir (`_ts`).</span><span class="sxs-lookup"><span data-stu-id="1b1e5-157">To set the TTL on a collection, you need to provide a non-zero positive number that indicates the period, in seconds, to expire all documents in the collection after the last modified timestamp of the document (`_ts`).</span></span> <span data-ttu-id="1b1e5-158">Veya, koleksiyona eklenen tüm belgeleri süresiz olarak varsayılan olarak dinamik gelir-1 varsayılan ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-158">Or, you can set the default to -1, which implies that all documents inserted in to the collection will live indefinitely by default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive = 90 * 60 * 60 * 24; // expire all documents after 90 days
    
    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        "/dbs/salesdb",
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });


## <a name="setting-ttl-on-a-document"></a><span data-ttu-id="1b1e5-159">Bir belge TTL ayarı</span><span class="sxs-lookup"><span data-stu-id="1b1e5-159">Setting TTL on a document</span></span>
<span data-ttu-id="1b1e5-160">Bir koleksiyonda varsayılan TTL ayarlanmasına ek olarak, bir belge düzeyinde belirli TTL ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-160">In addition to setting a default TTL on a collection you can set specific TTL at a document level.</span></span> <span data-ttu-id="1b1e5-161">Bunun yapılması varsayılan koleksiyon değerini geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-161">Doing this will override the default of the collection.</span></span>

* <span data-ttu-id="1b1e5-162">Bir belgeyi TTL ayarlamak için zaman damgası belgenin son değiştiren sonra belgenin süresi dolacak şekilde saniye cinsinden süre gösteren sıfır olmayan pozitif bir sayı sağlamanız gerekir (`_ts`).</span><span class="sxs-lookup"><span data-stu-id="1b1e5-162">To set the TTL on a document, you need to provide a non-zero positive number which indicates the period, in seconds, to expire the document after the last modified timestamp of the document (`_ts`).</span></span>
* <span data-ttu-id="1b1e5-163">Bir belge TTL alanı varsa, varsayılan koleksiyon uygulanır.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-163">If a document has no TTL field, then the default of the collection will apply.</span></span>
* <span data-ttu-id="1b1e5-164">TTL koleksiyon düzeyinde devre dışıysa, TTL koleksiyonda yeniden etkinleştirilene kadar belgeyi TTL alanı yoksayılacak.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-164">If TTL is disabled at the collection level, the TTL field on the document will be ignored until TTL is enabled again on the collection.</span></span>

<span data-ttu-id="1b1e5-165">TTL sona erme bir belgeyi ayarlama gösteren bir parçacığı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1b1e5-165">Here's a snippet showing how to set the TTL expiration on a document:</span></span>

    // Include a property that serializes to "ttl" in JSON
    public class SalesOrder
    {
        [JsonProperty(PropertyName = "id")]
        public string Id { get; set; }
        
        [JsonProperty(PropertyName="cid")]
        public string CustomerId { get; set; }
        
        // used to set expiration policy
        [JsonProperty(PropertyName = "ttl", NullValueHandling = NullValueHandling.Ignore)]
        public int? TimeToLive { get; set; }
        
        //...
    }
    
    // Set the value to the expiration in seconds
    SalesOrder salesOrder = new SalesOrder
    {
        Id = "SO05",
        CustomerId = "CO18009186470",
        TimeToLive = 60 * 60 * 24 * 30;  // Expire sales orders in 30 days 
    };


## <a name="extending-ttl-on-an-existing-document"></a><span data-ttu-id="1b1e5-166">Var olan bir belgeyi TTL genişletme</span><span class="sxs-lookup"><span data-stu-id="1b1e5-166">Extending TTL on an existing document</span></span>
<span data-ttu-id="1b1e5-167">Belge üzerinde herhangi bir yazma işlemi yaparak belgesinde TTL sıfırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-167">You can reset the TTL on a document by doing any write operation on the document.</span></span> <span data-ttu-id="1b1e5-168">Bunu yaptığınızda bu ayarlayacak `_ts` geçerli saati ve belirlediği belge süre sonu için geri sayım `ttl`, yeniden başlar.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-168">Doing this will set the `_ts` to the current time, and the countdown to the document expiry, as set by the `ttl`, will begin again.</span></span> <span data-ttu-id="1b1e5-169">Değiştirmek istiyorsanız `ttl` bir belgenin diğer ayarlanabilir alan yaptığınız gibi alanı güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-169">If you wish to change the `ttl` of a document, you can update the field as you can do with any other settable field.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = 60 * 30 * 30; // update time to live
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="removing-ttl-from-a-document"></a><span data-ttu-id="1b1e5-170">Bir belgeden TTL kaldırma</span><span class="sxs-lookup"><span data-stu-id="1b1e5-170">Removing TTL from a document</span></span>
<span data-ttu-id="1b1e5-171">TTL bir belgeyi ayarlama ve süresi dolacak şekilde bu belgeyi artık istiyorsanız sonra belgeyi almak, TTL alanı kaldırabileceğiniz ve sunucuda belge değiştirin.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-171">If a TTL has been set on a document and you no longer want that document to expire, then you can retrieve the document, remove the TTL field and replace the document on the server.</span></span> <span data-ttu-id="1b1e5-172">TTL alanı belgeden kaldırıldığında, koleksiyon varsayılan uygulanır.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-172">When the TTL field is removed from the document, the default of the collection will be applied.</span></span> <span data-ttu-id="1b1e5-173">Bir belgeden zaman aşımına uğramak durdurup koleksiyondan devralmayan sonra TTL değeri -1 olarak ayarlandığında gerekir.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-173">To stop a document from expiring and not inherit from the collection then you need to set the TTL value to -1.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = null; // inherit the default TTL of the collection
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="disabling-ttl"></a><span data-ttu-id="1b1e5-174">TTL devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="1b1e5-174">Disabling TTL</span></span>
<span data-ttu-id="1b1e5-175">TTL bir koleksiyonda tamamen devre dışı bırakın ve koleksiyon DefaultTTL özellikte süresi dolan belgeleri mi arıyorsunuz gelen arka plan işlemi durdurmak için silinmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-175">To disable TTL entirely on a collection and stop the background process from looking for expired documents the DefaultTTL property on the collection should be deleted.</span></span> <span data-ttu-id="1b1e5-176">Bu özellik silme -1 olarak ayarından farklıdır.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-176">Deleting this property is different from setting it to -1.</span></span> <span data-ttu-id="1b1e5-177">Koleksiyona eklenen yeni belgeler-1 anlamına gelir ayarına sonsuza kadar Canlı ancak, bu koleksiyondaki belirli belgeleri kılabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-177">Setting to -1 means new documents added to the collection will live forever but you can override this on specific documents in the collection.</span></span> <span data-ttu-id="1b1e5-178">Önceki bir varsayılan açıkça silmiş belgeleri olsa bile bu özellik tamamen koleksiyonundan kaldırılması hiçbir belge dolacağını anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-178">Removing this property entirely from the collection means that no documents will expire, even if there are documents that have explicitly overridden a previous default.</span></span>

    DocumentCollection collection = await client.ReadDocumentCollectionAsync("/dbs/salesdb/colls/orders");
    
    // Disable TTL
    collection.DefaultTimeToLive = null;
    
    await client.ReplaceDocumentCollectionAsync(collection);


## <a name="faq"></a><span data-ttu-id="1b1e5-179">SSS</span><span class="sxs-lookup"><span data-stu-id="1b1e5-179">FAQ</span></span>
<span data-ttu-id="1b1e5-180">**Ne TTL bana maliyeti ne olacak?**</span><span class="sxs-lookup"><span data-stu-id="1b1e5-180">**What will TTL cost me?**</span></span>

<span data-ttu-id="1b1e5-181">Bir belge üzerinde bir TTL ayarına ek bir maliyet yoktur.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-181">There is no additional cost to setting a TTL on a document.</span></span>

<span data-ttu-id="1b1e5-182">**Ne kadar TTL yukarı olduğunda my belge silmek için sürer?**</span><span class="sxs-lookup"><span data-stu-id="1b1e5-182">**How long will it take to delete my document once the TTL is up?**</span></span>

<span data-ttu-id="1b1e5-183">Hemen TTL çalışır durumda ve CRUD veya sorgu API'leri yoluyla erişilemeyecek belgeleri süresi dolmuş.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-183">The documents are expired immediately once the TTL is up, and will not be accessible via CRUD or query APIs.</span></span> 

<span data-ttu-id="1b1e5-184">**TTL belgesinde herhangi RU giderler etkileyecek?**</span><span class="sxs-lookup"><span data-stu-id="1b1e5-184">**Will TTL on a document have any impact on RU charges?**</span></span>

<span data-ttu-id="1b1e5-185">Hayır, hiçbir etkisi olacaktır RU masrafları Cosmos DB'de TTL aracılığıyla süresi dolan belgelerin silme işlemleri için.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-185">No, there will be no impact on RU charges for deletions of expired documents via TTL in Cosmos DB.</span></span>

<span data-ttu-id="1b1e5-186">**TTL özelliği yalnızca tüm belgeler için geçerli veya belgenin özellik değerlerini süresinin dolmasını sağlayabilir mi?**</span><span class="sxs-lookup"><span data-stu-id="1b1e5-186">**Does the TTL feature only apply to entire documents, or can I expire individual document property values?**</span></span>

<span data-ttu-id="1b1e5-187">TTL belgenin tamamına uygulanır.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-187">TTL applies to the entire document.</span></span> <span data-ttu-id="1b1e5-188">Ardından bir belgeyi yalnızca bir kısmı süresi dolacak şekilde isterseniz, bölümü ana belge için ayrı bir "bağlı" Belge ayıklayın ve ardından TTL ayıklanan bu belgeyi kullanmak önerilir.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-188">If you would like to expire just a portion of a document, then it is recommended that you extract the portion from the main document in to a separate "linked” document and then use TTL on that extracted document.</span></span>

<span data-ttu-id="1b1e5-189">**TTL özelliği, belirli bir dizin oluşturma gereksinimleri var mı?**</span><span class="sxs-lookup"><span data-stu-id="1b1e5-189">**Does the TTL feature have any specific indexing requirements?**</span></span>

<span data-ttu-id="1b1e5-190">Evet.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-190">Yes.</span></span> <span data-ttu-id="1b1e5-191">Koleksiyon olmalıdır [ilke kümesi dizin](indexing-policies.md) CONSISTENT veya Lazy.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-191">The collection must have [indexing policy set](indexing-policies.md) to either Consistent or Lazy.</span></span> <span data-ttu-id="1b1e5-192">None olarak ayarlanmış dizin ile bir koleksiyonda DefaultTTL ayarlanmaya çalışılırken bir hata, önceden ayarlanmış bir DefaultTTL sahip bir koleksiyonun üzerinde dizin oluşturmayı devre dışı bırakma çalışılırken olarak neden olur.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-192">Trying to set DefaultTTL on a collection with indexing set to None will result in an error, as will trying to turn off indexing on a collection that has a DefaultTTL already set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b1e5-193">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1b1e5-193">Next steps</span></span>
<span data-ttu-id="1b1e5-194">Azure Cosmos DB hakkında daha fazla bilgi için hizmete bakın [ *belgelerine* ](https://azure.microsoft.com/documentation/services/cosmos-db/) sayfası.</span><span class="sxs-lookup"><span data-stu-id="1b1e5-194">To learn more about Azure Cosmos DB, refer to the service [*documentation*](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span>

