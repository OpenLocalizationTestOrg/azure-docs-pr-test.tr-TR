---
title: "SQL sorgu ölçümleri Azure Cosmos DB DocumentDB API'si | Microsoft Docs"
description: "İzleme ve Azure Cosmos DB istekleri SQL sorgu performansını hata ayıklama hakkında bilgi edinin."
keywords: "SQL söz dizimi, sql sorgusu, sql sorguları, json sorgu dili, veritabanı kavramlarını ve sql sorguları, toplama işlevleri"
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: b2fa8e8f-7291-45a3-9bd1-7284ed9077f8
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: d928113e809e5ad43901e79dc256a8a39c210181
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="tuning-query-performance-with-azure-cosmos-db"></a><span data-ttu-id="23c0e-104">Sorgu performans Azure Cosmos DB ile ayarlama</span><span class="sxs-lookup"><span data-stu-id="23c0e-104">Tuning query performance with Azure Cosmos DB</span></span>
<span data-ttu-id="23c0e-105">Azure Cosmos DB sağlayan bir [SQL veri sorgulama için API](documentdb-sql-query.md), şema veya ikincil dizinler gerektirmeden.</span><span class="sxs-lookup"><span data-stu-id="23c0e-105">Azure Cosmos DB provides a [SQL API for querying data](documentdb-sql-query.md), without requiring schema or secondary indexes.</span></span> <span data-ttu-id="23c0e-106">Bu makalede, geliştiriciler için aşağıdaki bilgileri sağlar:</span><span class="sxs-lookup"><span data-stu-id="23c0e-106">This article provides the following information for developers:</span></span>

* <span data-ttu-id="23c0e-107">Azure Cosmos veritabanı SQL sorgu yürütme nasıl çalıştığı hakkında üst düzey ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="23c0e-107">High-level details on how Azure Cosmos DB's SQL query execution works</span></span>
* <span data-ttu-id="23c0e-108">Sorgu istek ve yanıt üstbilgileri ve istemci SDK seçenekleri hakkında ayrıntılar</span><span class="sxs-lookup"><span data-stu-id="23c0e-108">Details on query request and response headers, and client SDK options</span></span>
* <span data-ttu-id="23c0e-109">İpuçları ve sorgu performansı için en iyi yöntemler</span><span class="sxs-lookup"><span data-stu-id="23c0e-109">Tips and best practices for query performance</span></span>
* <span data-ttu-id="23c0e-110">Sorgu performansı hata ayıklamak için SQL yürütme istatistikleri kullanmaya nasıl örnekleri</span><span class="sxs-lookup"><span data-stu-id="23c0e-110">Examples of how to utilize SQL execution statistics to debug query performance</span></span>

## <a name="about-sql-query-execution"></a><span data-ttu-id="23c0e-111">SQL sorgu yürütme hakkında</span><span class="sxs-lookup"><span data-stu-id="23c0e-111">About SQL query execution</span></span>

<span data-ttu-id="23c0e-112">Azure Cosmos DB'de herhangi büyüyebilir kapsayıcıları veri deposundaki [depolama boyutu veya istek işleme](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="23c0e-112">In Azure Cosmos DB, you store data in containers, which can grow to any [storage size or request throughput](partition-data.md).</span></span> <span data-ttu-id="23c0e-113">Azure Cosmos DB verileri veri artışını işlemek veya sağlanan performansı artırmak için kapsar altında fiziksel bölümleri arasında sorunsuz bir şekilde ölçeklendirir.</span><span class="sxs-lookup"><span data-stu-id="23c0e-113">Azure Cosmos DB seamlessly scales data across physical partitions under the covers to handle data growth or increase in provisioned throughput.</span></span> <span data-ttu-id="23c0e-114">REST API veya desteklenen birini kullanarak herhangi bir kapsayıcıya SQL sorguları verebilir [DocumentDB SDK'ları](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="23c0e-114">You can issue SQL queries to any container using the REST API or one of the supported [DocumentDB SDKs](documentdb-sdk-dotnet.md).</span></span>

<span data-ttu-id="23c0e-115">Bölümlendirme, kısa bir genel bakış: veri fiziksel bölümleri arasında nasıl bölünür belirler "Şehir" gibi bir bölüm anahtarı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="23c0e-115">A brief overview of partitioning: you define a partition key like "city", which determines how data is split across physical partitions.</span></span> <span data-ttu-id="23c0e-116">Tek bir bölüm anahtarına ait veri (örneğin, "Şehir" "Seattle" ==) fiziksel bir bölüm içinde depolanır ancak genellikle tek bir fiziksel bölüm birden çok bölüm anahtarlarını sahiptir.</span><span class="sxs-lookup"><span data-stu-id="23c0e-116">Data belonging to a single partition key (for example, "city" == "Seattle") is stored within a physical partition, but typically a single physical partition has multiple partition keys.</span></span> <span data-ttu-id="23c0e-117">Bir bölümü depolama boyutuna ulaştığında, hizmet sorunsuz bir şekilde bölüm iki yeni bölümlere ayırır ve bu bölümler bölüm anahtarı tam olarak böler.</span><span class="sxs-lookup"><span data-stu-id="23c0e-117">When a partition reaches its storage size, the service seamlessly splits the partition into two new partitions, and divides the partition key evenly across these partitions.</span></span> <span data-ttu-id="23c0e-118">Bölümler geçici olduğundan, "Bölüm anahtarı karmaları aralıklarına gösterir bir bölüm anahtarı aralığı" için bir Özet API'leri kullanın.</span><span class="sxs-lookup"><span data-stu-id="23c0e-118">Since partitions are transient, the APIs use an abstraction of a "partition key range", which denotes the ranges of partition key hashes.</span></span> 

<span data-ttu-id="23c0e-119">Bir sorgu için Azure Cosmos DB verdiğinizde, SDK mantıksal adımları gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="23c0e-119">When you issue a query to Azure Cosmos DB, the SDK performs these logical steps:</span></span>

* <span data-ttu-id="23c0e-120">Sorgu yürütme planı belirlemek için SQL sorgu ayrıştırılamadı.</span><span class="sxs-lookup"><span data-stu-id="23c0e-120">Parse the SQL query to determine the query execution plan.</span></span> 
* <span data-ttu-id="23c0e-121">Sorgu, bir filtre bölüm anahtarı karşı içeriyorsa, ister `SELECT * FROM c WHERE c.city = "Seattle"`, tek bir bölüm yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="23c0e-121">If the query includes a filter against the partition key, like `SELECT * FROM c WHERE c.city = "Seattle"`, it is routed to a single partition.</span></span> <span data-ttu-id="23c0e-122">Sorgu bölüm anahtarı üzerinde bir filtre yok sonra içindeki tüm bölümlerin yürütülür ve sonuçları birleştirilir istemci tarafı.</span><span class="sxs-lookup"><span data-stu-id="23c0e-122">If the query does not have a filter on partition key, then it is executed in all partitions, and results are merged client side.</span></span>
* <span data-ttu-id="23c0e-123">Sorgu her bölümü seri içinde yürütülen veya paralel, istemci yapılandırmasına bağlı olarak.</span><span class="sxs-lookup"><span data-stu-id="23c0e-123">The query is executed within each partition in series or parallel, based on client configuration.</span></span> <span data-ttu-id="23c0e-124">Her bölüm içinde sorgu birini yapabilir veya sorgu karmaşıklığına bağlı olarak daha fazla gidiş dönüş sayfa boyutu yapılandırılmış ve koleksiyon verimini sağlandı.</span><span class="sxs-lookup"><span data-stu-id="23c0e-124">Within each partition, the query might make one or more round trips depending on the query complexity, configured page size, and provisioned throughput of the collection.</span></span> <span data-ttu-id="23c0e-125">Her yürütme sayısını döndürür [istek birimleri](request-units.md) sorgu yürütme ve isteğe bağlı olarak, sorgu yürütme istatistikleri tüketilen.</span><span class="sxs-lookup"><span data-stu-id="23c0e-125">Each execution returns the number of [request units](request-units.md) consumed by query execution, and optionally, query execution statistics.</span></span> 
* <span data-ttu-id="23c0e-126">SDK, bölümler sorgu sonuçlarının bir özetini gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="23c0e-126">The SDK performs a summarization of the query results across partitions.</span></span> <span data-ttu-id="23c0e-127">Sorgu bir ORDER BY bölümler içeriyorsa, örneğin, daha sonra bireysel bölümleri sonuçlarından birleştirme-sıralanmış genel olarak sıralanmış olarak sonuçları döndürmek için.</span><span class="sxs-lookup"><span data-stu-id="23c0e-127">For example, if the query involves an ORDER BY across partitions, then results from individual partitions are merge-sorted to return results in globally sorted order.</span></span> <span data-ttu-id="23c0e-128">Sorgu gibi bir toplama ise `COUNT`, tek tek bölümlerden birinden sayıları genel sayısı üretmek için toplanır.</span><span class="sxs-lookup"><span data-stu-id="23c0e-128">If the query is an aggregation like `COUNT`, the counts from individual partitions are summed to produce the overall count.</span></span>

<span data-ttu-id="23c0e-129">SDK'ları sorgu yürütmesi için çeşitli seçenekler sağlar.</span><span class="sxs-lookup"><span data-stu-id="23c0e-129">The SDKs provide various options for query execution.</span></span> <span data-ttu-id="23c0e-130">Örneğin, .NET içinde bu seçenekleri mevcuttur `FeedOptions` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="23c0e-130">For example, in .NET these options are available in the `FeedOptions` class.</span></span> <span data-ttu-id="23c0e-131">Aşağıdaki tabloda, bu seçenekler ve bunların nasıl sorgusu yürütme süresi etkisi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="23c0e-131">The following table describes these options and how they impact query execution time.</span></span> 

| <span data-ttu-id="23c0e-132">Seçenek</span><span class="sxs-lookup"><span data-stu-id="23c0e-132">Option</span></span> | <span data-ttu-id="23c0e-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="23c0e-133">Description</span></span> |
| ------ | ----------- |
| `EnableCrossPartitionQuery` | <span data-ttu-id="23c0e-134">Ayarlanmalıdır herhangi bir sorgu için true gerektirir arasında birden fazla bölüm yürütülecek.</span><span class="sxs-lookup"><span data-stu-id="23c0e-134">Must be set to true for any query that requires to be executed across more than one partition.</span></span> <span data-ttu-id="23c0e-135">Geliştirme zamanı boyunca bilinçli performans bileşim olmanızı sağlamak için bir açık bayrağı budur.</span><span class="sxs-lookup"><span data-stu-id="23c0e-135">This is an explicit flag to enable you to make conscious performance tradeoffs during development time.</span></span> |
| `EnableScanInQuery` | <span data-ttu-id="23c0e-136">Dizin oluşturma dışında seçtiyseniz true, ancak yine de sorgu bir tarama çalıştırmak istediğiniz ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="23c0e-136">Must be set to true if you have opted out of indexing, but want to run the query via a scan anyway.</span></span> <span data-ttu-id="23c0e-137">Yalnızca geçerli istenen filtre yolu için dizin oluşturma devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="23c0e-137">Only applicable if indexing for the requested filter path is disabled.</span></span> | 
| `MaxItemCount` | <span data-ttu-id="23c0e-138">Sunucuya gidiş dönüş döndürülecek öğe maksimum sayısı.</span><span class="sxs-lookup"><span data-stu-id="23c0e-138">The maximum number of items to return per round trip to the server.</span></span> <span data-ttu-id="23c0e-139">-1 ayarıyla sunucu öğe sayısını yönetme izin verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="23c0e-139">By setting to -1, you can let the server manage the number of items.</span></span> <span data-ttu-id="23c0e-140">Veya yalnızca az sayıda gidiş dönüş başına öğe almak için bu değeri düşürebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="23c0e-140">Or, you can lower this value to retrieve only a small number of items per round trip.</span></span> 
| `MaxBufferedItemCount` | <span data-ttu-id="23c0e-141">Bu istemci-tarafı seçenek ve çapraz bölüm ORDER BY gerçekleştirirken bellek tüketimini sınırlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="23c0e-141">This is a client-side option, and used to limit the memory consumption when performing cross-partition ORDER BY.</span></span> <span data-ttu-id="23c0e-142">Daha yüksek bir değer çapraz bölüm sıralama gecikme süresi azaltılmasına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="23c0e-142">A higher value helps reduce the latency of cross-partition sorting.</span></span> |
| `MaxDegreeOfParallelism` | <span data-ttu-id="23c0e-143">Alır veya Azure DocumentDB veritabanı hizmeti paralel sorgu yürütme sırasında istemci tarafı çalıştırmak eşzamanlı işlem sayısını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="23c0e-143">Gets or sets the number of concurrent operations run client side during parallel query execution in the Azure DocumentDB database service.</span></span> <span data-ttu-id="23c0e-144">Pozitif özellik değerini ayarla değerine eşzamanlı işlem sayısını sınırlar.</span><span class="sxs-lookup"><span data-stu-id="23c0e-144">A positive property value limits the number of concurrent operations to the set value.</span></span> <span data-ttu-id="23c0e-145">0'dan düşük bir değere ayarlanırsa, sistem otomatik olarak çalıştırmak için eşzamanlı işlem sayısını karar verir.</span><span class="sxs-lookup"><span data-stu-id="23c0e-145">If it is set to less than 0, the system automatically decides the number of concurrent operations to run.</span></span> |
| `PopulateQueryMetrics` | <span data-ttu-id="23c0e-146">Yükleme zamanı süre istatistiklerin ayrıntılı günlük sorgu yürütme derleme süresi, dizin döngü süresi ve belge gibi çeşitli aşamaları harcadığı etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="23c0e-146">Enables detailed logging of statistics of time spent in various phases of query execution like compilation time, index loop time, and document load time.</span></span> <span data-ttu-id="23c0e-147">Sorgu istatistiklerini çıktısı sorgu performans sorunları tanılamak için Azure desteği ile paylaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="23c0e-147">You can share output from query statistics with Azure Support to diagnose query performance issues.</span></span> |
| `RequestContinuation` | <span data-ttu-id="23c0e-148">Herhangi bir sorgu tarafından döndürülen donuk devamlılık belirteci geçirerek sorgu yürütme devam edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="23c0e-148">You can resume query execution by passing in the opaque continuation token returned by any query.</span></span> <span data-ttu-id="23c0e-149">Devamlılık belirteci sorgu yürütme için gerekli tüm durum yalıtır.</span><span class="sxs-lookup"><span data-stu-id="23c0e-149">The continuation token encapsulates all state required for query execution.</span></span> |
| `ResponseContinuationTokenLimitInKb` | <span data-ttu-id="23c0e-150">Sunucu tarafından döndürülen devam belirtecini en büyük boyutunu sınırlandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="23c0e-150">You can limit the maximum size of the continuation token returned by the server.</span></span> <span data-ttu-id="23c0e-151">Uygulama ana bilgisayarı yanıt üstbilgi boyutu sınırları varsa bu ayarlamanız gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="23c0e-151">You might need to set this if your application host has limits on response header size.</span></span> <span data-ttu-id="23c0e-152">Bu ayar, toplam süre ve sorgu için kullanılan RUs artırabilir.</span><span class="sxs-lookup"><span data-stu-id="23c0e-152">Setting this may increase the overall duration and RUs consumed for the query.</span></span>  |

<span data-ttu-id="23c0e-153">Örneğin, örnek bir sorgu ile bir koleksiyon üzerinde istenen bölüm anahtarı atalım `/city` bölüm anahtarı ve sn'ye 100.000 RU/s ile sağlanan olarak.</span><span class="sxs-lookup"><span data-stu-id="23c0e-153">For example, let's take an example query on partition key requested on a collection with `/city` as the partition key and provisioned with 100,000 RU/s of throughput.</span></span> <span data-ttu-id="23c0e-154">Bu sorgu kullanarak isteği `CreateDocumentQuery<T>` aşağıdaki gibi .NET içinde:</span><span class="sxs-lookup"><span data-stu-id="23c0e-154">You request this query using `CreateDocumentQuery<T>` in .NET like the following:</span></span>

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        PopulateQueryMetrics = true, 
        MaxItemCount = -1, 
        MaxDegreeOfParallelism = -1, 
        EnableCrossPartitionQuery = true 
    }).AsDocumentQuery();

FeedResponse<dynamic> result = await query.ExecuteNextAsync();
```

<span data-ttu-id="23c0e-155">Yukarıda gösterilen SDK kod parçacığını aşağıdaki REST API isteğine karşılık gelir:</span><span class="sxs-lookup"><span data-stu-id="23c0e-155">The SDK snippet shown above, corresponds to the following REST API request:</span></span>

```
POST https://arramacquerymetrics-westus.documents.azure.com/dbs/db/colls/sample/docs HTTP/1.1
x-ms-continuation: 
x-ms-documentdb-isquery: True
x-ms-max-item-count: -1
x-ms-documentdb-query-enablecrosspartition: True
x-ms-documentdb-query-parallelizecrosspartitionquery: True
x-ms-documentdb-query-iscontinuationexpected: True
x-ms-documentdb-populatequerymetrics: True
x-ms-date: Tue, 27 Jun 2017 21:52:18 GMT
authorization: type%3dmaster%26ver%3d1.0%26sig%3drp1Hi83Y8aVV5V6LzZ6xhtQVXRAMz0WNMnUuvriUv%2b4%3d
x-ms-session-token: 7:8,6:2008,5:8,4:2008,3:8,2:2008,1:8,0:8,9:8,8:4008
Cache-Control: no-cache
x-ms-consistency-level: Session
User-Agent: documentdb-dotnet-sdk/1.14.1 Host/32-bit MicrosoftWindowsNT/6.2.9200.0
x-ms-version: 2017-02-22
Accept: application/json
Content-Type: application/query+json
Host: arramacquerymetrics-westus.documents.azure.com
Content-Length: 52
Expect: 100-continue

{"query":"SELECT * FROM c WHERE c.city = 'Seattle'"}
```

<span data-ttu-id="23c0e-156">Her sorgu yürütme sayfası bir REST API için karşılık gelen `POST` ile `Accept: application/query+json` üstbilgi ve gövde SQL sorgusu.</span><span class="sxs-lookup"><span data-stu-id="23c0e-156">Each query execution page corresponds to a REST API `POST` with the `Accept: application/query+json` header, and the SQL query in the body.</span></span> <span data-ttu-id="23c0e-157">Her sorgu bir yapar ya da daha fazla ile sunucuya yuvarlak `x-ms-continuation` belirteci echoed yürütme devam etmek için istemci ile sunucu arasında.</span><span class="sxs-lookup"><span data-stu-id="23c0e-157">Each query makes one or more round trips to the server with the `x-ms-continuation` token echoed between the client and server to resume execution.</span></span> <span data-ttu-id="23c0e-158">FeedOptions yapılandırma seçeneklerinde istek üstbilgileri biçiminde sunucuya geçirilir.</span><span class="sxs-lookup"><span data-stu-id="23c0e-158">The configuration options in FeedOptions are passed to the server in the form of request headers.</span></span> <span data-ttu-id="23c0e-159">Örneğin, `MaxItemCount` karşılık gelen `x-ms-max-item-count`.</span><span class="sxs-lookup"><span data-stu-id="23c0e-159">For example, `MaxItemCount` corresponds to `x-ms-max-item-count`.</span></span> 

<span data-ttu-id="23c0e-160">İstek aşağıdaki (okunabilirlik için kesilmiş) yanıtı döndürür:</span><span class="sxs-lookup"><span data-stu-id="23c0e-160">The request returns the following (truncated for readability) response:</span></span>

```
HTTP/1.1 200 Ok
Cache-Control: no-store, no-cache
Pragma: no-cache
Transfer-Encoding: chunked
Content-Type: application/json
Server: Microsoft-HTTPAPI/2.0
Strict-Transport-Security: max-age=31536000
x-ms-last-state-change-utc: Tue, 27 Jun 2017 21:01:57.561 GMT
x-ms-resource-quota: documentSize=10240;documentsSize=10485760;documentsCount=-1;collectionSize=10485760;
x-ms-resource-usage: documentSize=1;documentsSize=884;documentsCount=2000;collectionSize=1408;
x-ms-item-count: 2000
x-ms-schemaversion: 1.3
x-ms-alt-content-path: dbs/db/colls/sample
x-ms-content-path: +9kEANVq0wA=
x-ms-xp-role: 1
x-ms-documentdb-query-metrics: totalExecutionTimeInMs=33.67;queryCompileTimeInMs=0.06;queryLogicalPlanBuildTimeInMs=0.02;queryPhysicalPlanBuildTimeInMs=0.10;queryOptimizationTimeInMs=0.00;VMExecutionTimeInMs=32.56;indexLookupTimeInMs=0.36;documentLoadTimeInMs=9.58;systemFunctionExecuteTimeInMs=0.00;userFunctionExecuteTimeInMs=0.00;retrievedDocumentCount=2000;retrievedDocumentSize=1125600;outputDocumentCount=2000;writeOutputTimeInMs=18.10;indexUtilizationRatio=1.00
x-ms-request-charge: 604.42
x-ms-serviceversion: version=1.14.34.4
x-ms-activity-id: 0df8b5f6-83b9-4493-abda-cce6d0f91486
x-ms-session-token: 2:2008
x-ms-gatewayversion: version=1.14.33.2
Date: Tue, 27 Jun 2017 21:59:49 GMT
```

<span data-ttu-id="23c0e-161">Sorgudan döndürülen anahtar yanıt üstbilgilerini aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="23c0e-161">The key response headers returned from the query include the following:</span></span>

| <span data-ttu-id="23c0e-162">Seçenek</span><span class="sxs-lookup"><span data-stu-id="23c0e-162">Option</span></span> | <span data-ttu-id="23c0e-163">Açıklama</span><span class="sxs-lookup"><span data-stu-id="23c0e-163">Description</span></span> |
| ------ | ----------- |
| `x-ms-item-count` | <span data-ttu-id="23c0e-164">Yanıtta döndürülen öğe sayısı.</span><span class="sxs-lookup"><span data-stu-id="23c0e-164">The number of items returned in the response.</span></span> <span data-ttu-id="23c0e-165">Bu sağlanan üzerinde bağımlı `x-ms-max-item-count`, en büyük yanıt yükü boyutu, sağlanan işleme ve sorgu yürütme süresi içinde sığabilecek öğe sayısı.</span><span class="sxs-lookup"><span data-stu-id="23c0e-165">This is dependent on the supplied `x-ms-max-item-count`, the number of items that can be fit within the maximum response payload size, the provisioned throughput, and query execution time.</span></span> |  
| `x-ms-continuation:` | <span data-ttu-id="23c0e-166">Ek sonuçlar mevcutsa, sorgunun yürütülmesi, devam etmek için devamlılık belirteci.</span><span class="sxs-lookup"><span data-stu-id="23c0e-166">The continuation token to resume execution of the query, if additional results are available.</span></span> | 
| `x-ms-documentdb-query-metrics` | <span data-ttu-id="23c0e-167">Sorgu istatistiklerini yürütme.</span><span class="sxs-lookup"><span data-stu-id="23c0e-167">The query statistics for the execution.</span></span> <span data-ttu-id="23c0e-168">Bu, sorgu yürütme çeşitli aşamalarında harcanan zamanın istatistikleri içeren sınırlandırılmış bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="23c0e-168">This is a delimited string containing statistics of time spent in the various phases of query execution.</span></span> <span data-ttu-id="23c0e-169">Döndürülen IF `x-ms-documentdb-populatequerymetrics` ayarlanır `True`.</span><span class="sxs-lookup"><span data-stu-id="23c0e-169">Returned if `x-ms-documentdb-populatequerymetrics` is set to `True`.</span></span> | 
| `x-ms-request-charge` | <span data-ttu-id="23c0e-170">Sayısı [istek birimleri](request-units.md) sorgu tarafından tüketilen.</span><span class="sxs-lookup"><span data-stu-id="23c0e-170">The number of [request units](request-units.md) consumed by the query.</span></span> | 

<span data-ttu-id="23c0e-171">REST API isteği üstbilgileri ve seçenekleri hakkında daha fazla bilgi için bkz: [DocumentDB REST API kullanarak kaynak sorgulaması](https://docs.microsoft.com/rest/api/documentdb/querying-documentdb-resources-using-the-rest-api).</span><span class="sxs-lookup"><span data-stu-id="23c0e-171">For details on the REST API request headers and options, see [Querying resources using the DocumentDB REST API](https://docs.microsoft.com/rest/api/documentdb/querying-documentdb-resources-using-the-rest-api).</span></span>

## <a name="best-practices-for-query-performance"></a><span data-ttu-id="23c0e-172">Sorgu performansı için en iyi yöntemler</span><span class="sxs-lookup"><span data-stu-id="23c0e-172">Best practices for query performance</span></span>
<span data-ttu-id="23c0e-173">Aşağıdaki Azure Cosmos DB sorgu performansı etkileyen en yaygın faktörlerdir.</span><span class="sxs-lookup"><span data-stu-id="23c0e-173">The following are the most common factors that impact Azure Cosmos DB query performance.</span></span> <span data-ttu-id="23c0e-174">Bu makalede bu konuların her derinlere.</span><span class="sxs-lookup"><span data-stu-id="23c0e-174">We dig deeper into each of these topics in this article.</span></span>

| <span data-ttu-id="23c0e-175">Faktörü</span><span class="sxs-lookup"><span data-stu-id="23c0e-175">Factor</span></span> | <span data-ttu-id="23c0e-176">İpucu</span><span class="sxs-lookup"><span data-stu-id="23c0e-176">Tip</span></span> | 
| ------ | -----| 
| <span data-ttu-id="23c0e-177">Sağlanan aktarım hızı</span><span class="sxs-lookup"><span data-stu-id="23c0e-177">Provisioned throughput</span></span> | <span data-ttu-id="23c0e-178">Sorgu RU ölçmek ve sorgularınızı gerekli sağlanan işleme sahip olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="23c0e-178">Measure RU per query, and ensure that you have the required provisioned throughput for your queries.</span></span> | 
| <span data-ttu-id="23c0e-179">Bölümleme ve bölüm anahtarları</span><span class="sxs-lookup"><span data-stu-id="23c0e-179">Partitioning and partition keys</span></span> | <span data-ttu-id="23c0e-180">Sorguları ayrıcalık tanıma ile düşük gecikme süresi filtre yan tümcesi bölüm anahtar değeri.</span><span class="sxs-lookup"><span data-stu-id="23c0e-180">Favor queries with the partition key value in the filter clause for low latency.</span></span> |
| <span data-ttu-id="23c0e-181">SDK ve sorgu seçenekleri</span><span class="sxs-lookup"><span data-stu-id="23c0e-181">SDK and query options</span></span> | <span data-ttu-id="23c0e-182">Doğrudan bağlantı gibi SDK en iyi uygulamaları izleyin ve istemci tarafı sorgu yürütme seçeneklerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="23c0e-182">Follow SDK best practices like direct connectivity, and tune client-side query execution options.</span></span> |
| <span data-ttu-id="23c0e-183">Ağ gecikmesi</span><span class="sxs-lookup"><span data-stu-id="23c0e-183">Network latency</span></span> | <span data-ttu-id="23c0e-184">Ağ Yükü ölçüm için hesap ve yakın bölgesinden okumak için çok girişli API'leri kullanın.</span><span class="sxs-lookup"><span data-stu-id="23c0e-184">Account for network overhead in measurement, and use multi-homing APIs to read from the nearest region.</span></span> |
| <span data-ttu-id="23c0e-185">Dizin oluşturma ilkesi</span><span class="sxs-lookup"><span data-stu-id="23c0e-185">Indexing Policy</span></span> | <span data-ttu-id="23c0e-186">Gerekli dizin yolları/ilke sorgu için olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="23c0e-186">Ensure that you have the required indexing paths/policy for the query.</span></span> |
| <span data-ttu-id="23c0e-187">Sorgu yürütme ölçümleri</span><span class="sxs-lookup"><span data-stu-id="23c0e-187">Query execution metrics</span></span> | <span data-ttu-id="23c0e-188">Sorgu ve veri şekilleri, olası yeniden yazdırmaya tanımlamak için sorgu yürütme ölçümleri analiz edin.</span><span class="sxs-lookup"><span data-stu-id="23c0e-188">Analyze the query execution metrics to identify potential rewrites of query and data shapes.</span></span>  |

### <a name="provisioned-throughput"></a><span data-ttu-id="23c0e-189">Sağlanan aktarım hızı</span><span class="sxs-lookup"><span data-stu-id="23c0e-189">Provisioned throughput</span></span>
<span data-ttu-id="23c0e-190">Cosmos DB'de her istek birimleri (RU) Saniyedeki cinsinden ifade edilen ayrılmış işleme ile veri kapsayıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="23c0e-190">In Cosmos DB, you create containers of data, each with reserved throughput expressed in request units (RU) per-second.</span></span> <span data-ttu-id="23c0e-191">1 KB belgenin okuma 1. RU ve (sorguları da dahil) her işlemi bunun kapsamına bağlı RUs sabit sayıda normalleştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="23c0e-191">A read of a 1-KB document is 1 RU, and every operation (including queries) is normalized to a fixed number of RUs based on its complexity.</span></span> <span data-ttu-id="23c0e-192">Örneğin, 1000 varsa RU/s kapsayıcısı için sağlanan ve gibi bir sorguya sahip `SELECT * FROM c WHERE c.city = 'Seattle'` 5 RUs kullanır ve ardından (1000 RU/s) gerçekleştirebilirsiniz / (5 RU/sorgu) sorgularını saniyede = 200 sorgu/s.</span><span class="sxs-lookup"><span data-stu-id="23c0e-192">For example, if you have 1000 RU/s provisioned for your container, and you have a query like `SELECT * FROM c WHERE c.city = 'Seattle'` that consumes 5 RUs, then you can perform (1000 RU/s) / (5 RU/query) = 200 query/s such queries per second.</span></span> 

<span data-ttu-id="23c0e-193">200'den fazla saniye başına sorgusu gönderirseniz, hız sınırlaması gelen istekleri 200/s yukarıda hizmetini başlatır.</span><span class="sxs-lookup"><span data-stu-id="23c0e-193">If you submit more than 200 queries/sec, the service starts rate-limiting incoming requests above 200/s.</span></span> <span data-ttu-id="23c0e-194">Bu durumda otomatik olarak işleme geri Çekilme/yeniden deneme gerçekleştirerek SDK'lar, bu nedenle bu sorgular için daha yüksek gecikme fark edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="23c0e-194">The SDKs automatically handle this case by performing a backoff/retry, therefore you might notice a higher latency for these queries.</span></span> <span data-ttu-id="23c0e-195">Gerekli değere sağlanan işleme artırma sorgu gecikme süresi ve verimlilik artırır.</span><span class="sxs-lookup"><span data-stu-id="23c0e-195">Increasing the provisioned throughput to the required value improves your query latency and throughput.</span></span> 

<span data-ttu-id="23c0e-196">İstek birimleri hakkında daha fazla bilgi için bkz: [istek birimleri](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="23c0e-196">To learn more about request units, see [Request units](request-units.md).</span></span>

### <a name="partitioning-and-partition-keys"></a><span data-ttu-id="23c0e-197">Bölümleme ve bölüm anahtarları</span><span class="sxs-lookup"><span data-stu-id="23c0e-197">Partitioning and partition keys</span></span>
<span data-ttu-id="23c0e-198">Azure Cosmos DB ile sorguları aşağıdaki sırayla hızlı/en verimli gelen yavaş/daha az verimli için genellikle gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="23c0e-198">With Azure Cosmos DB, typically queries perform in the following order from fastest/most efficient to slower/less efficient.</span></span> 

* <span data-ttu-id="23c0e-199">Bir tek bölüm anahtarı ve öğe anahtarı alma</span><span class="sxs-lookup"><span data-stu-id="23c0e-199">GET on a single partition key and item key</span></span>
* <span data-ttu-id="23c0e-200">Tek bölüm anahtarı bir filtre yan tümcesi içeren sorgu</span><span class="sxs-lookup"><span data-stu-id="23c0e-200">Query with a filter clause on a single partition key</span></span>
* <span data-ttu-id="23c0e-201">Bir eşitlik veya aralık filtre yan tümcesi herhangi bir özellikte olmadan sorgulama</span><span class="sxs-lookup"><span data-stu-id="23c0e-201">Query without an equality or range filter clause on any property</span></span>
* <span data-ttu-id="23c0e-202">Filtre sorgulama</span><span class="sxs-lookup"><span data-stu-id="23c0e-202">Query without filters</span></span>

<span data-ttu-id="23c0e-203">Tüm bölümleri danışmanız gerekir sorguları daha yüksek gecikme gerekir ve daha yüksek RUs kullanmasını sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="23c0e-203">Queries that need to consult all partitions need higher latency, and can consume higher RUs.</span></span> <span data-ttu-id="23c0e-204">Her bölüm karşı tüm özellikleri otomatik dizin oluşturma işlemi olduğundan, sorgu verimli bir şekilde dizinden bu durumda hizmet verilebilir.</span><span class="sxs-lookup"><span data-stu-id="23c0e-204">Since each partition has automatic indexing against all properties, the query can be served efficiently from the index in this case.</span></span> <span data-ttu-id="23c0e-205">Bölümler paralellik seçenekleri kullanarak daha hızlı yayılma sorgular yapabilir.</span><span class="sxs-lookup"><span data-stu-id="23c0e-205">You can make queries that span partitions faster by using the parallelism options.</span></span>

<span data-ttu-id="23c0e-206">Bölümlendirme ve bölüm anahtarları hakkında daha fazla bilgi için bkz: [Azure Cosmos DB'de bölümleme](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="23c0e-206">To learn more about partitioning and partition keys, see [Partitioning in Azure Cosmos DB](partition-data.md).</span></span>

### <a name="sdk-and-query-options"></a><span data-ttu-id="23c0e-207">SDK ve sorgu seçenekleri</span><span class="sxs-lookup"><span data-stu-id="23c0e-207">SDK and query options</span></span>
<span data-ttu-id="23c0e-208">Bkz: [performans ipuçları](performance-tips.md) ve [performans testi](performance-testing.md) için en iyi istemci tarafında performans Azure Cosmos DB'den alma.</span><span class="sxs-lookup"><span data-stu-id="23c0e-208">See [Performance Tips](performance-tips.md) and [Performance testing](performance-testing.md) for how to get the best client-side performance from Azure Cosmos DB.</span></span> <span data-ttu-id="23c0e-209">Bu, son SDK'ları kullanarak, platforma özgü yapılandırmaları bağlantıları, atık toplama sıklığını varsayılan sayısı gibi yapılandırma ve doğrudan/TCP gibi basit bağlantı seçenekleri kullanarak içerir.</span><span class="sxs-lookup"><span data-stu-id="23c0e-209">This includes using the latest SDKs, configuring platform-specific configurations like default number of connections, frequency of garbage collection, and using lightweight connectivity options like Direct/TCP.</span></span> 


#### <a name="max-item-count"></a><span data-ttu-id="23c0e-210">En fazla öğe sayısı</span><span class="sxs-lookup"><span data-stu-id="23c0e-210">Max Item Count</span></span>
<span data-ttu-id="23c0e-211">Sorgular, değeri için `MaxItemCount` uçtan uca sorgu zamanında önemli bir etkisi olabilir.</span><span class="sxs-lookup"><span data-stu-id="23c0e-211">For queries, the value of `MaxItemCount` can have a significant impact on end-to-end query time.</span></span> <span data-ttu-id="23c0e-212">Her sunucuya gidiş dönüş öğelerin sayısı en fazla döndürülecek `MaxItemCount` (100 öğelerinin varsayılan).</span><span class="sxs-lookup"><span data-stu-id="23c0e-212">Each round trip to the server will return no more than the number of items in `MaxItemCount` (Default of 100 items).</span></span> <span data-ttu-id="23c0e-213">Bu daha yüksek bir değere ayarlamak (-1, en fazla ve önerilen), sorgu süresi genel sorgular büyük sonuç kümeleri ile için özellikle istemci ve sunucu arasındaki gidiş dönüş sayısı sınırlayarak geliştirecektir.</span><span class="sxs-lookup"><span data-stu-id="23c0e-213">Setting this to a higher value (-1 is maximum, and recommended) will improve your query duration overall by limiting the number of round trips between server and client, especially for queries with large result sets.</span></span>

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        MaxItemCount = -1, 
    }).AsDocumentQuery();
```

#### <a name="max-degree-of-parallelism"></a><span data-ttu-id="23c0e-214">Maksimum paralellik derecesi</span><span class="sxs-lookup"><span data-stu-id="23c0e-214">Max Degree of Parallelism</span></span>
<span data-ttu-id="23c0e-215">Sorguları için ayarlama `MaxDegreeOfParallelism` özellikle çapraz bölüm sorgular (olmadan bir filtre bölüm anahtarı değeri) gerçekleştirirseniz, uygulamanız için en iyi yapılandırmaları tanımlamak için.</span><span class="sxs-lookup"><span data-stu-id="23c0e-215">For queries, tune the `MaxDegreeOfParallelism` to identify the best configurations for your application, especially if you perform cross-partition queries (without a filter on the partition-key value).</span></span> <span data-ttu-id="23c0e-216">`MaxDegreeOfParallelism`en fazla sayısını Paralel Görevler, yani, en fazla paralel olarak ziyaret etme bölüm denetler.</span><span class="sxs-lookup"><span data-stu-id="23c0e-216">`MaxDegreeOfParallelism`  controls the maximum number of parallel tasks, i.e., the maximum of partitions to be visited in parallel.</span></span> 

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        MaxDegreeOfParallelism = -1, 
        EnableCrossPartitionQuery = true 
    }).AsDocumentQuery();
```

<span data-ttu-id="23c0e-217">Varsayalım</span><span class="sxs-lookup"><span data-stu-id="23c0e-217">Let’s assume that</span></span>
* <span data-ttu-id="23c0e-218">D = (istemci makine işlemcide toplam sayısı =) Paralel Görevler varsayılan maksimum sayısı</span><span class="sxs-lookup"><span data-stu-id="23c0e-218">D = Default Maximum number of parallel tasks (= total number of processor in the client machine)</span></span>
* <span data-ttu-id="23c0e-219">P = Paralel Görevler maksimum sayısı kullanıcı tanımlı</span><span class="sxs-lookup"><span data-stu-id="23c0e-219">P = User-specified maximum number of parallel tasks</span></span>
* <span data-ttu-id="23c0e-220">N sorgu yanıtlama ziyaret gerekiyor bölüm sayısı =</span><span class="sxs-lookup"><span data-stu-id="23c0e-220">N = Number of partitions that needs  to be visited for answering a query</span></span>

<span data-ttu-id="23c0e-221">Paralel sorgular P. farklı değerler için nasıl davranacaktır etkileri verilmiştir</span><span class="sxs-lookup"><span data-stu-id="23c0e-221">Following are implications of how the parallel queries would behave for different values of P.</span></span>
* <span data-ttu-id="23c0e-222">(P == 0) = > seri modu</span><span class="sxs-lookup"><span data-stu-id="23c0e-222">(P == 0) => Serial Mode</span></span>
* <span data-ttu-id="23c0e-223">(P == 1) = > bir görevin maksimum</span><span class="sxs-lookup"><span data-stu-id="23c0e-223">(P == 1) => Maximum of one task</span></span>
* <span data-ttu-id="23c0e-224">(P > 1) = > Min (P, N) Paralel Görevler</span><span class="sxs-lookup"><span data-stu-id="23c0e-224">(P > 1) => Min (P, N) parallel tasks</span></span> 
* <span data-ttu-id="23c0e-225">(P < 1) = > Min (N, D) Paralel Görevler</span><span class="sxs-lookup"><span data-stu-id="23c0e-225">(P < 1) => Min (N, D) parallel tasks</span></span>

<span data-ttu-id="23c0e-226">SDK sürüm notlarında ve uygulanan sınıflar ve yöntemler ayrıntıları görmek için [DocumentDB SDK'ları](documentdb-sdk-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="23c0e-226">For SDK release notes, and details on implemented classes and methods see [DocumentDB SDKs](documentdb-sdk-dotnet.md)</span></span>

### <a name="network-latency"></a><span data-ttu-id="23c0e-227">Ağ gecikmesi</span><span class="sxs-lookup"><span data-stu-id="23c0e-227">Network latency</span></span>
<span data-ttu-id="23c0e-228">Bkz: [Azure Cosmos DB genel dağıtım](tutorial-global-distribution-documentdb.md) genel dağıtımları ayarlar ve en yakın bölgeyi bağlanma hakkında.</span><span class="sxs-lookup"><span data-stu-id="23c0e-228">See [Azure Cosmos DB global distribution](tutorial-global-distribution-documentdb.md) for how to set up global distribution, and connect to the closest region.</span></span> <span data-ttu-id="23c0e-229">Birden çok gidiş dönüş yapmak veya sorgudan ayarlamak büyük bir sonuç almak gerektiğinde ağ gecikmesi sorgu performansına önemli bir etkisi vardır.</span><span class="sxs-lookup"><span data-stu-id="23c0e-229">Network latency has a significant impact on query performance when you need to make multiple round-trips or retrieve a large result set from the query.</span></span> 

<span data-ttu-id="23c0e-230">Sorgu yürütme ölçümleri bölümüne sorgularda sunucusu yürütme süresi almak açıklanmaktadır ( `totalExecutionTimeInMs`), böylece sorgu yürütme harcanan süre ve ağ yolda harcadığı zamanı arasında ayırt edebilir.</span><span class="sxs-lookup"><span data-stu-id="23c0e-230">The section on query execution metrics explains how to retrieve the server execution time of queries ( `totalExecutionTimeInMs`), so that you can differentiate between time spent in query execution and time spent in network transit.</span></span>

### <a name="indexing-policy"></a><span data-ttu-id="23c0e-231">Dizin oluşturma ilkesi</span><span class="sxs-lookup"><span data-stu-id="23c0e-231">Indexing policy</span></span>
<span data-ttu-id="23c0e-232">Bkz: [dizin oluşturma ilkesini yapılandırma](indexing-policies.md) yolları, tür ve modları ve bunlar sorgu yürütme nasıl etkiler dizin oluşturma için.</span><span class="sxs-lookup"><span data-stu-id="23c0e-232">See [Configuring indexing policy](indexing-policies.md) for indexing paths, kinds, and modes, and how they impact query execution.</span></span> <span data-ttu-id="23c0e-233">Varsayılan olarak, dizin oluşturma ilkesini karma dizeleri için dizin oluşturma kullanır etkin olduğu yönelik eşitlik sorguları, ancak aralığı sorguları/order sorgular tarafından için değil.</span><span class="sxs-lookup"><span data-stu-id="23c0e-233">By default, the indexing policy uses Hash indexing for strings, which is effective for equality queries, but not for range queries/order by queries.</span></span> <span data-ttu-id="23c0e-234">Aralık sorgu dizeleri için ihtiyacınız varsa, tüm dizeleri aralığı dizin türü belirtilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="23c0e-234">If you need range queries for strings, we recommend specifying the Range index type for all strings.</span></span> 

## <a name="query-execution-metrics"></a><span data-ttu-id="23c0e-235">Sorgu yürütme ölçümleri</span><span class="sxs-lookup"><span data-stu-id="23c0e-235">Query execution metrics</span></span>
<span data-ttu-id="23c0e-236">İsteğe bağlı geçirerek sorgu yürütme üzerinde ayrıntılı ölçümler edinebilirsiniz `x-ms-documentdb-populatequerymetrics` üstbilgi (`FeedOptions.PopulateQueryMetrics` .NET SDK'sındaki).</span><span class="sxs-lookup"><span data-stu-id="23c0e-236">You can obtain detailed metrics on query execution by passing in the optional `x-ms-documentdb-populatequerymetrics` header (`FeedOptions.PopulateQueryMetrics` in the .NET SDK).</span></span> <span data-ttu-id="23c0e-237">Döndürülen değerin `x-ms-documentdb-query-metrics` Gelişmiş sorgu yürütme işlemi sorun giderme yönelik aşağıdaki anahtar-değer çiftleri sahiptir.</span><span class="sxs-lookup"><span data-stu-id="23c0e-237">The value returned in `x-ms-documentdb-query-metrics` has the following key-value pairs meant for advanced troubleshooting of query execution.</span></span> 

```cs
IDocumentQuery<dynamic> query = client.CreateDocumentQuery(
    UriFactory.CreateDocumentCollectionUri(DatabaseName, CollectionName), 
    "SELECT * FROM c WHERE c.city = 'Seattle'", 
    new FeedOptions 
    { 
        PopulateQueryMetrics = true, 
    }).AsDocumentQuery();

FeedResponse<dynamic> result = await query.ExecuteNextAsync();

// Returns metrics by partition key range Id
IReadOnlyDictionary<string, QueryMetrics> metrics = result.QueryMetrics;

```

| <span data-ttu-id="23c0e-238">Ölçüm</span><span class="sxs-lookup"><span data-stu-id="23c0e-238">Metric</span></span> | <span data-ttu-id="23c0e-239">Birim</span><span class="sxs-lookup"><span data-stu-id="23c0e-239">Unit</span></span> | <span data-ttu-id="23c0e-240">Açıklama</span><span class="sxs-lookup"><span data-stu-id="23c0e-240">Description</span></span> | 
| ------ | -----| ----------- |
| `totalExecutionTimeInMs` | <span data-ttu-id="23c0e-241">milisaniye</span><span class="sxs-lookup"><span data-stu-id="23c0e-241">milliseconds</span></span> | <span data-ttu-id="23c0e-242">Sorgu yürütme süresi</span><span class="sxs-lookup"><span data-stu-id="23c0e-242">Query execution time</span></span> | 
| `queryCompileTimeInMs` | <span data-ttu-id="23c0e-243">milisaniye</span><span class="sxs-lookup"><span data-stu-id="23c0e-243">milliseconds</span></span> | <span data-ttu-id="23c0e-244">Sorgu derleme süresi</span><span class="sxs-lookup"><span data-stu-id="23c0e-244">Query compile time</span></span>  | 
| `queryLogicalPlanBuildTimeInMs` | <span data-ttu-id="23c0e-245">milisaniye</span><span class="sxs-lookup"><span data-stu-id="23c0e-245">milliseconds</span></span> | <span data-ttu-id="23c0e-246">Mantıksal sorgu planı oluşturmak için zaman</span><span class="sxs-lookup"><span data-stu-id="23c0e-246">Time to build logical query plan</span></span> | 
| `queryPhysicalPlanBuildTimeInMs` | <span data-ttu-id="23c0e-247">milisaniye</span><span class="sxs-lookup"><span data-stu-id="23c0e-247">milliseconds</span></span> | <span data-ttu-id="23c0e-248">Fiziksel sorgu planı oluşturmak için zaman</span><span class="sxs-lookup"><span data-stu-id="23c0e-248">Time to build physical query plan</span></span> | 
| `queryOptimizationTimeInMs` | <span data-ttu-id="23c0e-249">milisaniye</span><span class="sxs-lookup"><span data-stu-id="23c0e-249">milliseconds</span></span> | <span data-ttu-id="23c0e-250">Sorgu en iyi duruma getirme için harcanan süre</span><span class="sxs-lookup"><span data-stu-id="23c0e-250">Time spent in optimizing query</span></span> | 
| `VMExecutionTimeInMs` | <span data-ttu-id="23c0e-251">milisaniye</span><span class="sxs-lookup"><span data-stu-id="23c0e-251">milliseconds</span></span> | <span data-ttu-id="23c0e-252">Sorgu çalışma zamanında harcanan süre</span><span class="sxs-lookup"><span data-stu-id="23c0e-252">Time spent in query runtime</span></span> | 
| `indexLookupTimeInMs` | <span data-ttu-id="23c0e-253">milisaniye</span><span class="sxs-lookup"><span data-stu-id="23c0e-253">milliseconds</span></span> | <span data-ttu-id="23c0e-254">Fiziksel dizini katmanda harcanan süre</span><span class="sxs-lookup"><span data-stu-id="23c0e-254">Time spent in physical index layer</span></span> | 
| `documentLoadTimeInMs` | <span data-ttu-id="23c0e-255">milisaniye</span><span class="sxs-lookup"><span data-stu-id="23c0e-255">milliseconds</span></span> | <span data-ttu-id="23c0e-256">Belgeleri yüklenirken harcanan süre</span><span class="sxs-lookup"><span data-stu-id="23c0e-256">Time spent in loading documents</span></span>  | 
| `systemFunctionExecuteTimeInMs` | <span data-ttu-id="23c0e-257">milisaniye</span><span class="sxs-lookup"><span data-stu-id="23c0e-257">milliseconds</span></span> | <span data-ttu-id="23c0e-258">Yürütülen sistem (yerleşik) işlevleri milisaniye cinsinden toplam süre</span><span class="sxs-lookup"><span data-stu-id="23c0e-258">Total time spent executing system (built-in) functions in milliseconds</span></span>  | 
| `userFunctionExecuteTimeInMs` | <span data-ttu-id="23c0e-259">milisaniye</span><span class="sxs-lookup"><span data-stu-id="23c0e-259">milliseconds</span></span> | <span data-ttu-id="23c0e-260">Milisaniye cinsinden yürütme kullanıcı tanımlı işlevler için harcanan toplam süre</span><span class="sxs-lookup"><span data-stu-id="23c0e-260">Total time spent executing user-defined functions in milliseconds</span></span> | 
| `retrievedDocumentCount` | <span data-ttu-id="23c0e-261">milisaniye</span><span class="sxs-lookup"><span data-stu-id="23c0e-261">milliseconds</span></span> | <span data-ttu-id="23c0e-262">Toplam alınan belge sayısı</span><span class="sxs-lookup"><span data-stu-id="23c0e-262">Total number of retrieved documents</span></span>  | 
| `retrievedDocumentSize` | <span data-ttu-id="23c0e-263">Bayt</span><span class="sxs-lookup"><span data-stu-id="23c0e-263">bytes</span></span> | <span data-ttu-id="23c0e-264">Alınan belgeleri bayt olarak toplam boyutu</span><span class="sxs-lookup"><span data-stu-id="23c0e-264">Total size of retrieved documents in bytes</span></span>  | 
| `outputDocumentCount` | <span data-ttu-id="23c0e-265">Sayısı</span><span class="sxs-lookup"><span data-stu-id="23c0e-265">count</span></span> | <span data-ttu-id="23c0e-266">Çıktı belge sayısı</span><span class="sxs-lookup"><span data-stu-id="23c0e-266">Number of output documents</span></span> | 
| `writeOutputTimeInMs` | <span data-ttu-id="23c0e-267">milisaniye</span><span class="sxs-lookup"><span data-stu-id="23c0e-267">milliseconds</span></span> | <span data-ttu-id="23c0e-268">Milisaniye cinsinden sorgu yürütme süresi</span><span class="sxs-lookup"><span data-stu-id="23c0e-268">Query execution time in milliseconds</span></span> | 
| `indexUtilizationRatio` | <span data-ttu-id="23c0e-269">oranı (< = 1)</span><span class="sxs-lookup"><span data-stu-id="23c0e-269">ratio (<=1)</span></span> | <span data-ttu-id="23c0e-270">Filtre tarafından yüklenen belgelere sayısıyla eşleşen belge sayısı oranı</span><span class="sxs-lookup"><span data-stu-id="23c0e-270">Ratio of number of documents matched by the filter to the number of documents loaded</span></span>  | 

<span data-ttu-id="23c0e-271">İstemci SDK'ları dahili olarak sorgu her bölüm içinde hizmet vermek için birden çok sorgu işlemleri kalmasına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="23c0e-271">The client SDKs may internally make multiple query operations to serve the query within each partition.</span></span> <span data-ttu-id="23c0e-272">İstemci başına toplam sonuç aşarsanız bölümü birden fazla çağrı yaptığında `x-ms-max-item-count`, sorgu bölüm için sağlanan işleme aşarsa veya sorgu yükü sayfa başına en fazla boyutu ulaşırsa veya sorgu ayrılmış sistem ulaşırsa zaman aşımı sınırı.</span><span class="sxs-lookup"><span data-stu-id="23c0e-272">The client makes more than one call per-partition if the total results exceed `x-ms-max-item-count`, if the query exceeds the provisioned throughput for the partition, or if the query payload reaches the maximum size per page, or if the query reaches the system allocated timeout limit.</span></span> <span data-ttu-id="23c0e-273">Her kısmi sorgu yürütme döndüren bir `x-ms-documentdb-query-metrics` bu sayfa için.</span><span class="sxs-lookup"><span data-stu-id="23c0e-273">Each partial query execution returns a `x-ms-documentdb-query-metrics` for that page.</span></span> 

<span data-ttu-id="23c0e-274">Bazı örnek sorgular şunlardır ve sorgu yürütülmesini ölçümleri bazıları yorumlama döndürdü:</span><span class="sxs-lookup"><span data-stu-id="23c0e-274">Here are some sample queries, and how to interpret some of the metrics returned from query execution:</span></span> 

| <span data-ttu-id="23c0e-275">Sorgu</span><span class="sxs-lookup"><span data-stu-id="23c0e-275">Query</span></span> | <span data-ttu-id="23c0e-276">Örnek ölçümü</span><span class="sxs-lookup"><span data-stu-id="23c0e-276">Sample Metric</span></span> | <span data-ttu-id="23c0e-277">Açıklama</span><span class="sxs-lookup"><span data-stu-id="23c0e-277">Description</span></span> | 
| ------ | -----| ----------- |
| `SELECT TOP 100 * FROM c` | `"RetrievedDocumentCount": 101` | <span data-ttu-id="23c0e-278">Alınan belge sayısı üst yan tümce eşleşecek şekilde 100 + 1'dir.</span><span class="sxs-lookup"><span data-stu-id="23c0e-278">The number of documents retrieved is 100+1 to match the TOP clause.</span></span> <span data-ttu-id="23c0e-279">Sorgu zaman harcanan çoğunlukla `WriteOutputTime` ve `DocumentLoadTime` tarama olduğundan.</span><span class="sxs-lookup"><span data-stu-id="23c0e-279">Query time is mostly spent in `WriteOutputTime` and `DocumentLoadTime` since it is a scan.</span></span> | 
| `SELECT TOP 500 * FROM c` | `"RetrievedDocumentCount": 501` | <span data-ttu-id="23c0e-280">RetrievedDocumentCount (TOP yan tümcesi eşleştirmek için daha yüksek 500 + 1) sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="23c0e-280">RetrievedDocumentCount is now higher (500+1 to match the TOP clause).</span></span> | 
| `SELECT * FROM c WHERE c.N = 55` | `"IndexLookupTime": "00:00:00.0009500"` | <span data-ttu-id="23c0e-281">Dizin arama olmasından dolayı hakkında 0,9 ms için anahtar bir arama, IndexLookupTime içinde harcanan `/N/?`.</span><span class="sxs-lookup"><span data-stu-id="23c0e-281">About 0.9 ms is spent in IndexLookupTime for a key lookup, because it's an index lookup on `/N/?`.</span></span> | 
| `SELECT * FROM c WHERE c.N > 55` | `"IndexLookupTime": "00:00:00.0017700"` | <span data-ttu-id="23c0e-282">Biraz daha fazla (1,7 ms) için harcanan süre içinde IndexLookupTime aralığı tarama bir dizin arama olmasından dolayı `/N/?`.</span><span class="sxs-lookup"><span data-stu-id="23c0e-282">Slightly more time (1.7 ms) spent in IndexLookupTime over a range scan, because it's an index lookup on `/N/?`.</span></span> | 
| `SELECT TOP 500 c.N FROM c` | `"IndexLookupTime": "00:00:00.0017700"` | <span data-ttu-id="23c0e-283">Aynı anda harcanan `DocumentLoadTime` önceki sorgular, ancak daha düşük `WriteOutputTime` yalnızca tek bir özellik yansıtma olduğundan.</span><span class="sxs-lookup"><span data-stu-id="23c0e-283">Same time spent on `DocumentLoadTime` as previous queries, but lower `WriteOutputTime` because we're projecting only one property.</span></span> | 
| `SELECT TOP 500 udf.toPercent(c.N) FROM c` | `"UserDefinedFunctionExecutionTime": "00:00:00.2136500"` | <span data-ttu-id="23c0e-284">Yaklaşık 213 ms, geçen `UserDefinedFunctionExecutionTime` UDF her değeri üzerinde yürütme `c.N`.</span><span class="sxs-lookup"><span data-stu-id="23c0e-284">About 213 ms is spent in `UserDefinedFunctionExecutionTime` executing the UDF on each value of `c.N`.</span></span> |
| `SELECT TOP 500 c.Name FROM c WHERE STARTSWITH(c.Name, 'Den')` | `"IndexLookupTime": "00:00:00.0006400", "SystemFunctionExecutionTime": "00:00:00.0074100"` | <span data-ttu-id="23c0e-285">Yaklaşık 0,6 ms, geçen `IndexLookupTime` üzerinde `/Name/?`.</span><span class="sxs-lookup"><span data-stu-id="23c0e-285">About 0.6 ms is spent in `IndexLookupTime` on `/Name/?`.</span></span> <span data-ttu-id="23c0e-286">İçinde sorgu yürütme süresi (~ 7 ms) çoğu `SystemFunctionExecutionTime`.</span><span class="sxs-lookup"><span data-stu-id="23c0e-286">Most of the query execution time (~7 ms) in `SystemFunctionExecutionTime`.</span></span> |
| `SELECT TOP 500 c.Name FROM c WHERE STARTSWITH(LOWER(c.Name), 'den')` | `"IndexLookupTime": "00:00:00", "RetrievedDocumentCount": 2491,  "OutputDocumentCount": 500` | <span data-ttu-id="23c0e-287">Sorgu, bir tarama gerçekleştirilir, kullandığından `LOWER`, ve 500 2491 alınan belgeleri dışında döndürülür.</span><span class="sxs-lookup"><span data-stu-id="23c0e-287">Query is performed as a scan because it uses `LOWER`, and 500 out of 2491 retrieved documents are returned.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="23c0e-288">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="23c0e-288">Next steps</span></span>
* <span data-ttu-id="23c0e-289">Desteklenen SQL sorgu işleçleri ve anahtar sözcükler hakkında bilgi edinmek için bkz: [SQL sorgusu](documentdb-sql-query.md).</span><span class="sxs-lookup"><span data-stu-id="23c0e-289">To learn about the supported SQL query operators and keywords, see [SQL query](documentdb-sql-query.md).</span></span> 
* <span data-ttu-id="23c0e-290">İstek birimleri hakkında bilgi edinmek için [istek birimleri](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="23c0e-290">To learn about request units, see [request units](request-units.md).</span></span>
* <span data-ttu-id="23c0e-291">Dizin oluşturma ilkesi hakkında bilgi edinmek için [İlkesi dizin oluşturma](indexing-policies.md)</span><span class="sxs-lookup"><span data-stu-id="23c0e-291">To learn about indexing policy, see [indexing policy](indexing-policies.md)</span></span> 


