---
title: "Azure Cosmos DB aaaExpire verileri toolive süresiyle | Microsoft Docs"
description: "TTL ile Microsoft Azure Cosmos DB hello sistemden bir süre sonra otomatik olarak temizlenir hello özelliği toohave belgeleri sağlar."
services: cosmos-db
documentationcenter: 
keywords: zaman toolive
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
ms.openlocfilehash: 51d8ec46add72c9624457316a4ccd1e23fb83ad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="expire-data-in-azure-cosmos-db-collections-automatically-with-time-toolive"></a><span data-ttu-id="ba43b-104">Zaman toolive ile otomatik olarak Azure Cosmos DB koleksiyonlarda verileri süresi dolacak</span><span class="sxs-lookup"><span data-stu-id="ba43b-104">Expire data in Azure Cosmos DB collections automatically with time toolive</span></span>
<span data-ttu-id="ba43b-105">Uygulamalar oluşturmak ve çok büyük miktarda veri depolayın.</span><span class="sxs-lookup"><span data-stu-id="ba43b-105">Applications can produce and store vast amounts of data.</span></span> <span data-ttu-id="ba43b-106">Bu veriler, bazı bilgiler yalnızca sınırlı bir süre için yararlıdır oluşturulan makine olay verileri, günlükler ve kullanıcı oturumu ister.</span><span class="sxs-lookup"><span data-stu-id="ba43b-106">Some of this data, like machine generated event data, logs, and user session information is only useful for a finite period of time.</span></span> <span data-ttu-id="ba43b-107">Merhaba uygulaması fazlalık toohello ihtiyaçlarını Hello veri olduktan sonra bu verileri güvenli toopurge olduğundan ve bir uygulamanın hello depolama gereksinimlerini azaltmak.</span><span class="sxs-lookup"><span data-stu-id="ba43b-107">Once hello data becomes surplus toohello needs of hello application it is safe toopurge this data and reduce hello storage needs of an application.</span></span>

<span data-ttu-id="ba43b-108">"Zaman toolive" veya TTL ile Microsoft Azure Cosmos DB hello veritabanından bir süre sonra otomatik olarak temizlenir hello özelliği toohave belgeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="ba43b-108">With "time toolive" or TTL, Microsoft Azure Cosmos DB provides hello ability toohave documents automatically purged from hello database after a period of time.</span></span> <span data-ttu-id="ba43b-109">Merhaba varsayılan süre toolive hello koleksiyon düzeyinde ayarlamak ve bir belge başına temelinde geçersiz kılındı.</span><span class="sxs-lookup"><span data-stu-id="ba43b-109">hello default time toolive can be set at hello collection level, and overridden on a per-document basis.</span></span> <span data-ttu-id="ba43b-110">Bir koleksiyonu varsayılan olarak veya bir belge düzeyinde TTL ayarlandıktan sonra Cosmos DB son değiştirildiği olduğundan, bu süre, saniye sonra mevcut belgeleri otomatik olarak kaldırır.</span><span class="sxs-lookup"><span data-stu-id="ba43b-110">Once TTL is set, either as a collection default or at a document level, Cosmos DB will automatically remove documents that exist after that period of time, in seconds, since they were last modified.</span></span>

<span data-ttu-id="ba43b-111">Hello belgenin en son değiştirildiği zamanı Cosmos DB'de toolive karşı bir uzaklık kullanır.</span><span class="sxs-lookup"><span data-stu-id="ba43b-111">Time toolive in Cosmos DB uses an offset against when hello document was last modified.</span></span> <span data-ttu-id="ba43b-112">toodo bu hello kullanan `_ts` her belge üzerinde var olan alan.</span><span class="sxs-lookup"><span data-stu-id="ba43b-112">toodo this it uses hello `_ts` field which exists on every document.</span></span> <span data-ttu-id="ba43b-113">Merhaba _ts UNIX stili dönem zaman damgası temsil eden hello tarih ve saat alanıdır.</span><span class="sxs-lookup"><span data-stu-id="ba43b-113">hello _ts field is a unix-style epoch timestamp representing hello date and time.</span></span> <span data-ttu-id="ba43b-114">Merhaba `_ts` alanı her zaman bir belge değiştirildiğinde güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="ba43b-114">hello `_ts` field is updated every time a document is modified.</span></span> 

## <a name="ttl-behavior"></a><span data-ttu-id="ba43b-115">TTL davranışı</span><span class="sxs-lookup"><span data-stu-id="ba43b-115">TTL behavior</span></span>
<span data-ttu-id="ba43b-116">Merhaba TTL özelliği, iki düzeyde - hello koleksiyon düzeyinde ve hello belge düzeyinde TTL özellikleri tarafından denetlenir.</span><span class="sxs-lookup"><span data-stu-id="ba43b-116">hello TTL feature is controlled by TTL properties at two levels - hello collection level and hello document level.</span></span> <span data-ttu-id="ba43b-117">Hello değerleri saniye olarak ayarlamak ve hello delta olarak davranılır `_ts` hello belge en son değiştirildiği.</span><span class="sxs-lookup"><span data-stu-id="ba43b-117">hello values are set in seconds and are treated as a delta from hello `_ts` that hello document was last modified at.</span></span>

1. <span data-ttu-id="ba43b-118">DefaultTTL hello koleksiyon için</span><span class="sxs-lookup"><span data-stu-id="ba43b-118">DefaultTTL for hello collection</span></span>
   
   * <span data-ttu-id="ba43b-119">Eksik (veya set toonull), belgeler, otomatik olarak silinmez.</span><span class="sxs-lookup"><span data-stu-id="ba43b-119">If missing (or set toonull), documents are not deleted automatically.</span></span>
   * <span data-ttu-id="ba43b-120">Varsa ve hello değerdir "-1" = sonsuz – belgeleri varsayılan olarak süresi yok</span><span class="sxs-lookup"><span data-stu-id="ba43b-120">If present and hello value is "-1" = infinite – documents don’t expire by default</span></span>
   * <span data-ttu-id="ba43b-121">Varsa ve hello değerdir bir numara ("n") – belgelerin süresi dolsun "n" saniye son değişikliğinden sonra</span><span class="sxs-lookup"><span data-stu-id="ba43b-121">If present and hello value is some number ("n") – documents expire "n” seconds after last modification</span></span>
2. <span data-ttu-id="ba43b-122">TTL hello belgeler için:</span><span class="sxs-lookup"><span data-stu-id="ba43b-122">TTL for hello documents:</span></span> 
   
   * <span data-ttu-id="ba43b-123">Özelliği, yalnızca DefaultTTL hello üst koleksiyonu için mevcut olduğunda geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="ba43b-123">Property is applicable only if DefaultTTL is present for hello parent collection.</span></span>
   * <span data-ttu-id="ba43b-124">Merhaba üst koleksiyon için Hello DefaultTTL değerini geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="ba43b-124">Overrides hello DefaultTTL value for hello parent collection.</span></span>

<span data-ttu-id="ba43b-125">Merhaba belge süresi doldu hemen (`ttl`  +  `_ts` > geçerli sunucu zamanı =), "süresi dolmuş olarak" Merhaba belge olarak işaretlendi.</span><span class="sxs-lookup"><span data-stu-id="ba43b-125">As soon as hello document has expired (`ttl` + `_ts` >= current server time), hello document is marked as "expired”.</span></span> <span data-ttu-id="ba43b-126">Bu tarihten sonra bu belgeler üzerinde hiçbir işlem izin verilecek ve hello gerçekleştirilen herhangi bir sorgu sonuçlarından bırakılır.</span><span class="sxs-lookup"><span data-stu-id="ba43b-126">No operation will be allowed on these documents after this time and they will be excluded from hello results of any queries performed.</span></span> <span data-ttu-id="ba43b-127">Merhaba belgeleri hello sistemde fiziksel olarak silinir ve hello arka planda mümkün daha sonra silinir.</span><span class="sxs-lookup"><span data-stu-id="ba43b-127">hello documents are physically deleted in hello system, and are deleted in hello background opportunistically at a later time.</span></span> <span data-ttu-id="ba43b-128">Bu kullanılmasına neden değil [istek birimlerine (RUs)](request-units.md) hello koleksiyonu bütçesi.</span><span class="sxs-lookup"><span data-stu-id="ba43b-128">This does not consume any [Request Units (RUs)](request-units.md) from hello collection budget.</span></span>

<span data-ttu-id="ba43b-129">Merhaba mantığı yukarıda matris aşağıdaki hello gösterilebilir:</span><span class="sxs-lookup"><span data-stu-id="ba43b-129">hello above logic can be shown in hello following matrix:</span></span>

|  | <span data-ttu-id="ba43b-130">DefaultTTL eksik değil hello koleksiyonunda ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ba43b-130">DefaultTTL missing/not set on hello collection</span></span> | <span data-ttu-id="ba43b-131">DefaultTTL = -1 koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="ba43b-131">DefaultTTL = -1 on collection</span></span> | <span data-ttu-id="ba43b-132">DefaultTTL koleksiyonunda "n" =</span><span class="sxs-lookup"><span data-stu-id="ba43b-132">DefaultTTL = "n" on collection</span></span> |
| --- |:--- |:--- |:--- |
| <span data-ttu-id="ba43b-133">TTL eksik belgesi</span><span class="sxs-lookup"><span data-stu-id="ba43b-133">TTL Missing on document</span></span> |<span data-ttu-id="ba43b-134">Hiçbir şey hello belge ve koleksiyon TTL kavramına sahip olduğundan belge düzeyinde toooverride.</span><span class="sxs-lookup"><span data-stu-id="ba43b-134">Nothing toooverride at document level since both hello document and collection have no concept of TTL.</span></span> |<span data-ttu-id="ba43b-135">Bu koleksiyonun hiç belgelerde sona erecek.</span><span class="sxs-lookup"><span data-stu-id="ba43b-135">No documents in this collection will expire.</span></span> |<span data-ttu-id="ba43b-136">Bu koleksiyonda hello belgeleri aralığı n sona erdiğinde sona erecek.</span><span class="sxs-lookup"><span data-stu-id="ba43b-136">hello documents in this collection will expire when interval n elapses.</span></span> |
| <span data-ttu-id="ba43b-137">TTL belgesinde -1 =</span><span class="sxs-lookup"><span data-stu-id="ba43b-137">TTL = -1 on document</span></span> |<span data-ttu-id="ba43b-138">Hiçbir şey toooverride hello koleksiyonu tanımlamıyor beri hello belge düzeyinde hello belge kılabilirsiniz DefaultTTL özelliği.</span><span class="sxs-lookup"><span data-stu-id="ba43b-138">Nothing toooverride at hello document level since hello collection doesn’t define hello DefaultTTL property that a document can override.</span></span> <span data-ttu-id="ba43b-139">TTL belgesinde hello sistem tarafından yorumlanan atanmamış.</span><span class="sxs-lookup"><span data-stu-id="ba43b-139">TTL on a document is un-interpreted by hello system.</span></span> |<span data-ttu-id="ba43b-140">Bu koleksiyonun hiç belgelerde sona erecek.</span><span class="sxs-lookup"><span data-stu-id="ba43b-140">No documents in this collection will expire.</span></span> |<span data-ttu-id="ba43b-141">TTL =-1'de bu koleksiyonun Hello belgeyle asla sona erecek.</span><span class="sxs-lookup"><span data-stu-id="ba43b-141">hello document with TTL=-1 in this collection will never expire.</span></span> <span data-ttu-id="ba43b-142">Diğer tüm belgeler "n" aralığından sonra sona erecek.</span><span class="sxs-lookup"><span data-stu-id="ba43b-142">All other documents will expire after "n" interval.</span></span> |
| <span data-ttu-id="ba43b-143">TTL belgesinde n =</span><span class="sxs-lookup"><span data-stu-id="ba43b-143">TTL = n on document</span></span> |<span data-ttu-id="ba43b-144">Hiçbir şey hello belge düzeyinde toooverride.</span><span class="sxs-lookup"><span data-stu-id="ba43b-144">Nothing toooverride at hello document level.</span></span> <span data-ttu-id="ba43b-145">Bir belge üzerinde TTL hello sistem tarafından yorumlanan kaydetmeyin.</span><span class="sxs-lookup"><span data-stu-id="ba43b-145">TTL on a document in un-interpreted by hello system.</span></span> |<span data-ttu-id="ba43b-146">TTL Hello belgeyle = n saniye cinsinden aralık n sonra dolacak.</span><span class="sxs-lookup"><span data-stu-id="ba43b-146">hello document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="ba43b-147">Diğer belgeleri -1 aralığı devralır ve süresi dolmayacak.</span><span class="sxs-lookup"><span data-stu-id="ba43b-147">Other documents will inherit interval of -1 and never expire.</span></span> |<span data-ttu-id="ba43b-148">TTL Hello belgeyle = n saniye cinsinden aralık n sonra dolacak.</span><span class="sxs-lookup"><span data-stu-id="ba43b-148">hello document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="ba43b-149">Diğer belgeler "n" aralığı hello koleksiyonundan devralır.</span><span class="sxs-lookup"><span data-stu-id="ba43b-149">Other documents will inherit "n" interval from hello collection.</span></span> |

## <a name="configuring-ttl"></a><span data-ttu-id="ba43b-150">TTL yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ba43b-150">Configuring TTL</span></span>
<span data-ttu-id="ba43b-151">Varsayılan olarak, varsayılan olarak tüm Cosmos DB koleksiyonlarında ve tüm belgeleri zaman toolive devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="ba43b-151">By default, time toolive is disabled by default in all Cosmos DB collections and on all documents.</span></span>

## <a name="enabling-ttl"></a><span data-ttu-id="ba43b-152">TTL etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="ba43b-152">Enabling TTL</span></span>
<span data-ttu-id="ba43b-153">TTL tooenable bir koleksiyon ya da bir koleksiyon içinde hello belgelerine koleksiyonu tooeither -1 veya sıfır olmayan pozitif bir sayı tooset hello DefaultTTL özelliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="ba43b-153">tooenable TTL on a collection, or hello documents within a collection, you need tooset hello DefaultTTL property of a collection tooeither -1 or a non-zero positive number.</span></span> <span data-ttu-id="ba43b-154">Varsayılan olarak hello koleksiyonundaki tüm belgeleri sonsuza kadar Canlı ancak hello Cosmos DB hizmeti bu koleksiyon, bu varsayılanı geçersiz belgeler için izlemelidir hello DefaultTTL çok 1 anlamına gelir ayarlama.</span><span class="sxs-lookup"><span data-stu-id="ba43b-154">Setting hello DefaultTTL too-1 means that by default all documents in hello collection will live forever but hello Cosmos DB service should monitor this collection for documents that have overridden this default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive =-1; //never expire by default

    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(databaseName),
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });

## <a name="configuring-default-ttl-on-a-collection"></a><span data-ttu-id="ba43b-155">Bir koleksiyonda varsayılan TTL yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ba43b-155">Configuring default TTL on a collection</span></span>
<span data-ttu-id="ba43b-156">Bir koleksiyon düzeyinde toolive bir varsayılan saati mümkün tooconfigure arasındadır.</span><span class="sxs-lookup"><span data-stu-id="ba43b-156">You are able tooconfigure a default time toolive at a collection level.</span></span> <span data-ttu-id="ba43b-157">tooset hello TTL hello zaman damgası hello belgenin son değiştirilme sonra bir koleksiyon üzerinde tooprovide hello süre, saniye cinsinden tooexpire gösteren sıfır olmayan pozitif bir sayı hello koleksiyonundaki tüm belgeleri gereken (`_ts`).</span><span class="sxs-lookup"><span data-stu-id="ba43b-157">tooset hello TTL on a collection, you need tooprovide a non-zero positive number that indicates hello period, in seconds, tooexpire all documents in hello collection after hello last modified timestamp of hello document (`_ts`).</span></span> <span data-ttu-id="ba43b-158">Veya hello varsayılan çok-toohello koleksiyonunda eklenen tüm belgeleri süresiz olarak varsayılan olarak dinamik gelir 1 ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ba43b-158">Or, you can set hello default too-1, which implies that all documents inserted in toohello collection will live indefinitely by default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive = 90 * 60 * 60 * 24; // expire all documents after 90 days
    
    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        "/dbs/salesdb",
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });


## <a name="setting-ttl-on-a-document"></a><span data-ttu-id="ba43b-159">Bir belge TTL ayarı</span><span class="sxs-lookup"><span data-stu-id="ba43b-159">Setting TTL on a document</span></span>
<span data-ttu-id="ba43b-160">Ayrıca toosetting varsayılan TTL bir koleksiyonda belirli TTL belge düzeyinde ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ba43b-160">In addition toosetting a default TTL on a collection you can set specific TTL at a document level.</span></span> <span data-ttu-id="ba43b-161">Bunun yapılması hello varsayılan hello koleksiyonunun geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="ba43b-161">Doing this will override hello default of hello collection.</span></span>

* <span data-ttu-id="ba43b-162">tooset hello TTL bir belge üzerinde gösteren sıfır olmayan pozitif bir sayı hello dönem hello zaman damgası hello belgenin son değiştirilme sonra tooexpire hello belge saniye cinsinden tooprovide gerekir (`_ts`).</span><span class="sxs-lookup"><span data-stu-id="ba43b-162">tooset hello TTL on a document, you need tooprovide a non-zero positive number which indicates hello period, in seconds, tooexpire hello document after hello last modified timestamp of hello document (`_ts`).</span></span>
* <span data-ttu-id="ba43b-163">Bir belgenin hello koleksiyonunun varsayılan hello hiçbir TTL alan varsa uygulanır.</span><span class="sxs-lookup"><span data-stu-id="ba43b-163">If a document has no TTL field, then hello default of hello collection will apply.</span></span>
* <span data-ttu-id="ba43b-164">TTL hello koleksiyon düzeyinde devre dışıysa, TTL hello koleksiyonunda yeniden etkinleştirilene kadar hello belgesindeki hello TTL alanında yoksayılacak.</span><span class="sxs-lookup"><span data-stu-id="ba43b-164">If TTL is disabled at hello collection level, hello TTL field on hello document will be ignored until TTL is enabled again on hello collection.</span></span>

<span data-ttu-id="ba43b-165">Nasıl tooset hello belge TTL bitiş tarihini gösteren bir parçacığı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="ba43b-165">Here's a snippet showing how tooset hello TTL expiration on a document:</span></span>

    // Include a property that serializes too"ttl" in JSON
    public class SalesOrder
    {
        [JsonProperty(PropertyName = "id")]
        public string Id { get; set; }
        
        [JsonProperty(PropertyName="cid")]
        public string CustomerId { get; set; }
        
        // used tooset expiration policy
        [JsonProperty(PropertyName = "ttl", NullValueHandling = NullValueHandling.Ignore)]
        public int? TimeToLive { get; set; }
        
        //...
    }
    
    // Set hello value toohello expiration in seconds
    SalesOrder salesOrder = new SalesOrder
    {
        Id = "SO05",
        CustomerId = "CO18009186470",
        TimeToLive = 60 * 60 * 24 * 30;  // Expire sales orders in 30 days 
    };


## <a name="extending-ttl-on-an-existing-document"></a><span data-ttu-id="ba43b-166">Var olan bir belgeyi TTL genişletme</span><span class="sxs-lookup"><span data-stu-id="ba43b-166">Extending TTL on an existing document</span></span>
<span data-ttu-id="ba43b-167">Merhaba belge üzerinde herhangi bir yazma işlemi yaparak hello TTL belgesinde sıfırlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ba43b-167">You can reset hello TTL on a document by doing any write operation on hello document.</span></span> <span data-ttu-id="ba43b-168">Bunun yapılması hello ayarlayacak `_ts` toohello geçerli saati ve hello geri sayım toohello hello tarafından belirlenen süre sonu, belge `ttl`, yeniden başlar.</span><span class="sxs-lookup"><span data-stu-id="ba43b-168">Doing this will set hello `_ts` toohello current time, and hello countdown toohello document expiry, as set by hello `ttl`, will begin again.</span></span> <span data-ttu-id="ba43b-169">Toochange hello istiyorsanız `ttl` bir belgenin diğer ayarlanabilir alan yaptığınız gibi hello alanı güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ba43b-169">If you wish toochange hello `ttl` of a document, you can update hello field as you can do with any other settable field.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = 60 * 30 * 30; // update time toolive
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="removing-ttl-from-a-document"></a><span data-ttu-id="ba43b-170">Bir belgeden TTL kaldırma</span><span class="sxs-lookup"><span data-stu-id="ba43b-170">Removing TTL from a document</span></span>
<span data-ttu-id="ba43b-171">TTL bir belgeyi ayarlama ve artık bu belgeyi tooexpire istiyorsanız, ardından hello belge alabilir, hello TTL alanı kaldırmak ve hello sunucusundaki hello belgeden değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ba43b-171">If a TTL has been set on a document and you no longer want that document tooexpire, then you can retrieve hello document, remove hello TTL field and replace hello document on hello server.</span></span> <span data-ttu-id="ba43b-172">Merhaba TTL alanı hello belgeden kaldırıldığında, hello varsayılan hello koleksiyonunun uygulanır.</span><span class="sxs-lookup"><span data-stu-id="ba43b-172">When hello TTL field is removed from hello document, hello default of hello collection will be applied.</span></span> <span data-ttu-id="ba43b-173">toostop bir belgeden süresinin dolmasını ve hello koleksiyonundan devralmayan tooset hello TTL değeri çok-1 yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ba43b-173">toostop a document from expiring and not inherit from hello collection then you need tooset hello TTL value too-1.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = null; // inherit hello default TTL of hello collection
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="disabling-ttl"></a><span data-ttu-id="ba43b-174">TTL devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="ba43b-174">Disabling TTL</span></span>
<span data-ttu-id="ba43b-175">toodisable TTL tamamen, bir koleksiyon ve durdurma hello arka plan işleme hello DefaultTTL özelliği hello koleksiyonunda silinmeli süresi dolan belgeleri için aranıyor.</span><span class="sxs-lookup"><span data-stu-id="ba43b-175">toodisable TTL entirely on a collection and stop hello background process from looking for expired documents hello DefaultTTL property on hello collection should be deleted.</span></span> <span data-ttu-id="ba43b-176">Bu özellik silme çok 1 ayarından farklıdır.</span><span class="sxs-lookup"><span data-stu-id="ba43b-176">Deleting this property is different from setting it too-1.</span></span> <span data-ttu-id="ba43b-177">Yeni belgeleri çok 1 anlamına gelir ayarlama toohello koleksiyonu sonsuza kadar Canlı ancak, bu belirli belgeleri hello koleksiyonundaki kılabilirsiniz eklendi.</span><span class="sxs-lookup"><span data-stu-id="ba43b-177">Setting too-1 means new documents added toohello collection will live forever but you can override this on specific documents in hello collection.</span></span> <span data-ttu-id="ba43b-178">Önceki bir varsayılan açıkça silmiş belgeleri olsa bile bu özellik tamamen hello koleksiyonundan kaldırılması hiçbir belge dolacağını anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="ba43b-178">Removing this property entirely from hello collection means that no documents will expire, even if there are documents that have explicitly overridden a previous default.</span></span>

    DocumentCollection collection = await client.ReadDocumentCollectionAsync("/dbs/salesdb/colls/orders");
    
    // Disable TTL
    collection.DefaultTimeToLive = null;
    
    await client.ReplaceDocumentCollectionAsync(collection);


## <a name="faq"></a><span data-ttu-id="ba43b-179">SSS</span><span class="sxs-lookup"><span data-stu-id="ba43b-179">FAQ</span></span>
<span data-ttu-id="ba43b-180">**Ne TTL bana maliyeti ne olacak?**</span><span class="sxs-lookup"><span data-stu-id="ba43b-180">**What will TTL cost me?**</span></span>

<span data-ttu-id="ba43b-181">Hiçbir ek maliyet toosetting TTL belgesinde yoktur.</span><span class="sxs-lookup"><span data-stu-id="ba43b-181">There is no additional cost toosetting a TTL on a document.</span></span>

<span data-ttu-id="ba43b-182">**Ne kadar süreyle Hello TTL yukarı olduğunda, my belge toodelete sürer?**</span><span class="sxs-lookup"><span data-stu-id="ba43b-182">**How long will it take toodelete my document once hello TTL is up?**</span></span>

<span data-ttu-id="ba43b-183">hemen hello TTL çalışır durumda ve CRUD veya sorgu API'leri yoluyla erişilemeyecek hello belgeleri süresi dolmuş.</span><span class="sxs-lookup"><span data-stu-id="ba43b-183">hello documents are expired immediately once hello TTL is up, and will not be accessible via CRUD or query APIs.</span></span> 

<span data-ttu-id="ba43b-184">**TTL belgesinde herhangi RU giderler etkileyecek?**</span><span class="sxs-lookup"><span data-stu-id="ba43b-184">**Will TTL on a document have any impact on RU charges?**</span></span>

<span data-ttu-id="ba43b-185">Hayır, hiçbir etkisi olacaktır RU masrafları Cosmos DB'de TTL aracılığıyla süresi dolan belgelerin silme işlemleri için.</span><span class="sxs-lookup"><span data-stu-id="ba43b-185">No, there will be no impact on RU charges for deletions of expired documents via TTL in Cosmos DB.</span></span>

<span data-ttu-id="ba43b-186">**Hello TTL özelliği yalnızca tooentire belgeleri geçerli veya bireysel belge özellik değerlerini süresinin dolmasını sağlayabilir mi?**</span><span class="sxs-lookup"><span data-stu-id="ba43b-186">**Does hello TTL feature only apply tooentire documents, or can I expire individual document property values?**</span></span>

<span data-ttu-id="ba43b-187">TTL toohello belgenin tamamına uygulanır.</span><span class="sxs-lookup"><span data-stu-id="ba43b-187">TTL applies toohello entire document.</span></span> <span data-ttu-id="ba43b-188">Tooexpire isterseniz yeni bir belge ve ardından bir kısmı tooa ayrı "bağlı" belgedeki hello ana belgeden hello bölümü ayıklayın ve ardından TTL ayıklanan belge kullanmak önerilir.</span><span class="sxs-lookup"><span data-stu-id="ba43b-188">If you would like tooexpire just a portion of a document, then it is recommended that you extract hello portion from hello main document in tooa separate "linked” document and then use TTL on that extracted document.</span></span>

<span data-ttu-id="ba43b-189">**Merhaba TTL özellik belirli bir dizin oluşturma gereksinimleri var mı?**</span><span class="sxs-lookup"><span data-stu-id="ba43b-189">**Does hello TTL feature have any specific indexing requirements?**</span></span>

<span data-ttu-id="ba43b-190">Evet.</span><span class="sxs-lookup"><span data-stu-id="ba43b-190">Yes.</span></span> <span data-ttu-id="ba43b-191">Merhaba koleksiyonu olmalıdır [ilke kümesi dizin](indexing-policies.md) tooeither CONSISTENT veya Lazy.</span><span class="sxs-lookup"><span data-stu-id="ba43b-191">hello collection must have [indexing policy set](indexing-policies.md) tooeither Consistent or Lazy.</span></span> <span data-ttu-id="ba43b-192">Önceden ayarlanmış bir DefaultTTL sahip bir koleksiyonun üzerinde dizin oluşturmayı devre dışı çalışırken tooturn olarak tooset DefaultTTL kümesi tooNone dizin ile bir koleksiyon üzerinde çalışırken bir hatayla sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="ba43b-192">Trying tooset DefaultTTL on a collection with indexing set tooNone will result in an error, as will trying tooturn off indexing on a collection that has a DefaultTTL already set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba43b-193">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ba43b-193">Next steps</span></span>
<span data-ttu-id="ba43b-194">Azure Cosmos DB hakkında daha fazla toolearn başvuran toohello hizmet [ *belgelerine* ](https://azure.microsoft.com/documentation/services/cosmos-db/) sayfası.</span><span class="sxs-lookup"><span data-stu-id="ba43b-194">toolearn more about Azure Cosmos DB, refer toohello service [*documentation*](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span>

