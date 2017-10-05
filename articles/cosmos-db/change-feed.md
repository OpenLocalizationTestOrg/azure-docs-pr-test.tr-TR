---
title: "Değişiklik çalışmak akışı destek Azure Cosmos DB'de | Microsoft Docs"
description: "Belgelerdeki değişiklikleri izlemek ve tetikleyiciler gibi olay tabanlı işleme ve önbellekleri ve analizi sistemleri güncel tutma gerçekleştirmek için Azure Cosmos DB Değiştir Akış desteği kullanın."
keywords: "Akış Değiştir"
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 2d7798db-857f-431a-b10f-3ccbc7d93b50
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: rest-api
ms.topic: article
ms.date: 08/15/2017
ms.author: arramac
ms.openlocfilehash: 160fbc98e0f3dcc7d17cbe0c7f7425811596a896
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="working-with-the-change-feed-support-in-azure-cosmos-db"></a><span data-ttu-id="44851-104">Destek Azure Cosmos DB'de akış değişiklik ile çalışma</span><span class="sxs-lookup"><span data-stu-id="44851-104">Working with the change feed support in Azure Cosmos DB</span></span>
<span data-ttu-id="44851-105">[Azure Cosmos DB](../cosmos-db/introduction.md) bir hızlı ve esnek genel olarak, yazma ve okuma için tahmin edilebilir tek basamaklı milisaniyelik gecikme süresine sahip yüksek hacimli işlem ve işletimsel verileri depolamak için kullanılan veritabanı hizmeti çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="44851-105">[Azure Cosmos DB](../cosmos-db/introduction.md) is a fast and flexible globally replicated database service that is used for storing high-volume transactional and operational data with predictable single-digit millisecond latency for reads and writes.</span></span> <span data-ttu-id="44851-106">Bu, oldukça uygun perakende, oyun, IOT ve işlem günlüğü uygulamaları için kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="44851-106">This makes it well-suited for IoT, gaming, retail, and operational logging applications.</span></span> <span data-ttu-id="44851-107">Bu uygulamalar ortak tasarım modelinde olan Azure Cosmos DB verilerde yapılan değişiklikleri izlemek ve gerçekleştirilmiş görünümlere güncelleştirmek, gerçek zamanlı analiz gerçekleştirmek, verileri soğuk depolama ve bu değişikliklere dayalı belirli olayları bildirimlerini tetiklemesini arşivlemek için.</span><span class="sxs-lookup"><span data-stu-id="44851-107">A common design pattern in these applications is to track changes made to Azure Cosmos DB data, and update materialized views, perform real-time analytics, archive data to cold storage, and trigger notifications on certain events based on these changes.</span></span> <span data-ttu-id="44851-108">**Değişiklik akışı Destek** Azure Cosmos DB'de, verimli ve ölçeklenebilir çözümler her bu düzenlerin oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="44851-108">The **change feed support** in Azure Cosmos DB enables you to build efficient and scalable solutions for each of these patterns.</span></span>

<span data-ttu-id="44851-109">Destek akış değişiklikle Azure Cosmos DB belgelerinin Azure Cosmos DB koleksiyonu değiştirilmiş sırada içindeki sıralanmış bir listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="44851-109">With change feed support, Azure Cosmos DB provides a sorted list of documents within an Azure Cosmos DB collection in the order in which they were modified.</span></span> <span data-ttu-id="44851-110">Bu akışın koleksiyonundaki veri değişiklikleri dinler ve gibi eylemleri gerçekleştirmek için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="44851-110">This feed can be used to listen for modifications to data within the collection and perform actions such as:</span></span>

* <span data-ttu-id="44851-111">Bir belge eklendiğinde veya değiştiren bir API çağrısı Tetikle</span><span class="sxs-lookup"><span data-stu-id="44851-111">Trigger a call to an API when a document is inserted or modified</span></span>
* <span data-ttu-id="44851-112">Gerçek zamanlı (akış) yönlendirilmeden güncelleştirmeleri</span><span class="sxs-lookup"><span data-stu-id="44851-112">Perform real-time (stream) processing on updates</span></span>
* <span data-ttu-id="44851-113">Önbellek, arama motoru veya veri ambarı veri eşitleme</span><span class="sxs-lookup"><span data-stu-id="44851-113">Synchronize data with a cache, search engine, or data warehouse</span></span>

<span data-ttu-id="44851-114">Azure Cosmos DB değişiklikler kalıcı zaman uyumsuz olarak işlenir ve Paralel işleme için bir veya daha fazla tüketiciye dağıtılmış.</span><span class="sxs-lookup"><span data-stu-id="44851-114">Changes in Azure Cosmos DB are persisted and can be processed asynchronously, and distributed across one or more consumers for parallel processing.</span></span> <span data-ttu-id="44851-115">Değişiklik akış ve gerçek zamanlı ölçeklenebilir uygulamalar oluşturmak için bunları nasıl kullanabileceğiniz API'ler bakalım.</span><span class="sxs-lookup"><span data-stu-id="44851-115">Let's look at the APIs for change feed and how you can use them to build scalable real-time applications.</span></span> <span data-ttu-id="44851-116">Bu makalede Azure Cosmos DB Değiştir Akış ve DocumentDB API ile nasıl çalışılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="44851-116">This article shows how to work with Azure Cosmos DB change feed and the DocumentDB API.</span></span> 

![Akış güç gerçek zamanlı analiz ve bilgi işlem senaryolarına olay denetimli için Azure Cosmos DB Değiştir kullanma](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> <span data-ttu-id="44851-118">Destek akış değişiklik, yalnızca şu anda DocumentDB API'si için sağlanır; Tablo API ve grafik API'si şu anda desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="44851-118">Change feed support is only provided for the DocumentDB API at this time; the Graph API and Table API are not currently supported.</span></span>

## <a name="use-cases-and-scenarios"></a><span data-ttu-id="44851-119">Kullanım örnekleri ve senaryoları</span><span class="sxs-lookup"><span data-stu-id="44851-119">Use cases and scenarios</span></span>
<span data-ttu-id="44851-120">Değişiklik akış yüksek hacimli yazma ile büyük veri verimli işlemeye olanak sağlar ve nelerin değiştiğini belirlemek için tüm veri kümeleri sorgulama için bir alternatif sunar.</span><span class="sxs-lookup"><span data-stu-id="44851-120">Change feed allows for efficient processing of large datasets with a high volume of writes, and offers an alternative to querying entire datasets to identify what has changed.</span></span> <span data-ttu-id="44851-121">Örneğin, aşağıdaki görevleri etkin şekilde gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="44851-121">For example, you can perform the following tasks efficiently:</span></span>

* <span data-ttu-id="44851-122">Bir önbellek, arama dizini ya da bir veri ambarı Azure Cosmos DB içinde depolanan veriler ile güncelleştirecek.</span><span class="sxs-lookup"><span data-stu-id="44851-122">Update a cache, search index, or a data warehouse with data stored in Azure Cosmos DB.</span></span>
* <span data-ttu-id="44851-123">Uygulama düzeyi verileri katmanlama ve arşivleme uygulamak, diğer bir deyişle, Azure Cosmos DB'de "etkin verileri" depolamak ve "soğuk veri çıkış" geçerlilik süresi [Azure Blob Storage](../storage/common/storage-introduction.md) veya [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="44851-123">Implement application-level data tiering and archival, that is, store "hot data" in Azure Cosmos DB, and age out "cold data" to [Azure Blob Storage](../storage/common/storage-introduction.md) or [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span></span>
* <span data-ttu-id="44851-124">Verileri kullanarak toplu analizi uygulamak [Apache Hadoop](run-hadoop-with-hdinsight.md).</span><span class="sxs-lookup"><span data-stu-id="44851-124">Implement batch analytics on data using [Apache Hadoop](run-hadoop-with-hdinsight.md).</span></span>
* <span data-ttu-id="44851-125">Uygulama [lambda işlem hatları Azure üzerinde](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) Azure Cosmos DB ile.</span><span class="sxs-lookup"><span data-stu-id="44851-125">Implement [lambda pipelines on Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) with Azure Cosmos DB.</span></span> <span data-ttu-id="44851-126">Azure Cosmos DB alımı ve sorgu işleyen ve düşük ile lambda mimariyi uygulayan ölçeklenebilir veritabanı çözümü sağlar.</span><span class="sxs-lookup"><span data-stu-id="44851-126">Azure Cosmos DB provides a scalable database solution that can handle both ingestion and query, and implement lambda architectures with low TCO.</span></span> 
* <span data-ttu-id="44851-127">Farklı bir bölümleme düzeni ile başka bir Azure Cosmos DB hesabına sıfır kapalı kalma süresi geçişler gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="44851-127">Perform zero down-time migrations to another Azure Cosmos DB account with a different partitioning scheme.</span></span>

<span data-ttu-id="44851-128">**Azure Cosmos DB alımı ve sorgu için sahip lambda ardışık düzenler:**</span><span class="sxs-lookup"><span data-stu-id="44851-128">**Lambda Pipelines with Azure Cosmos DB for ingestion and query:**</span></span>

![Azure Cosmos DB lambda ardışık düzeni alımı ve sorgu için temel](./media/change-feed/lambda.png)

<span data-ttu-id="44851-130">Cihazlar, algılayıcılar, altyapı ve uygulamalardan olay veri depolamak ve almak için Azure Cosmos DB kullanın ve bu olayları işleme ile gerçek zamanlı [Azure akış analizi](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), veya [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="44851-130">You can use Azure Cosmos DB to receive and store event data from devices, sensors, infrastructure, and applications, and process these events in real-time with [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), or [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span></span> 

<span data-ttu-id="44851-131">İçinde [sunucusuz](http://azure.com/serverless) web ve mobil uygulamaları, yapabilecekleriniz müşterinizin profili, tercihlerine veya konumu kullanarak cihazlarını anında iletme bildirimleri gönderme gibi belirli eylemleri tetiklemek için değişiklik izleme olaylarına [ Azure işlevleri](../azure-functions/functions-bindings-documentdb.md) veya [uygulama hizmetleri](https://azure.microsoft.com/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="44851-131">Within your [serverless](http://azure.com/serverless) web and mobile apps, you can track events such as changes to your customer's profile, preferences, or location to trigger certain actions like sending push notifications to their devices using [Azure Functions](../azure-functions/functions-bindings-documentdb.md) or [App Services](https://azure.microsoft.com/services/app-service/).</span></span> <span data-ttu-id="44851-132">Oyun oluşturmak için Azure Cosmos DB kullanıyorsanız, şunları yapabilirsiniz, örneğin, kullanım tamamlanmış oyunlar gelen puanları göre gerçek zamanlı liderlik uygulamak için akış değiştirin.</span><span class="sxs-lookup"><span data-stu-id="44851-132">If you're using Azure Cosmos DB to build a game, you can, for example, use change feed to implement real-time leaderboards based on scores from completed games.</span></span>

## <a name="how-change-feed-works-in-azure-cosmos-db"></a><span data-ttu-id="44851-133">Değişiklik akış Azure Cosmos DB'de nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="44851-133">How change feed works in Azure Cosmos DB</span></span>
<span data-ttu-id="44851-134">Azure Cosmos DB artımlı olarak bir Azure Cosmos DB koleksiyona yapılan güncelleştirmeler okuma özelliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="44851-134">Azure Cosmos DB provides the ability to incrementally read updates made to an Azure Cosmos DB collection.</span></span> <span data-ttu-id="44851-135">Bu değişiklik akışın aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="44851-135">This change feed has the following properties:</span></span>

* <span data-ttu-id="44851-136">Değişiklikler Azure Cosmos DB'de kalıcı ve zaman uyumsuz olarak işlenir.</span><span class="sxs-lookup"><span data-stu-id="44851-136">Changes are persistent in Azure Cosmos DB and can be processed asynchronously.</span></span>
* <span data-ttu-id="44851-137">Bir koleksiyon içindeki belgelerde yapılan değişiklikler, akış değişikliği hemen kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="44851-137">Changes to documents within a collection are available immediately in the change feed.</span></span>
* <span data-ttu-id="44851-138">Bir belgeyi her değişiklik akış değişikliği tam olarak bir kez görünür ve bunların denetim noktası oluşturma mantığı istemcileri yönetmek.</span><span class="sxs-lookup"><span data-stu-id="44851-138">Each change to a document appears exactly once in the change feed, and clients manage their checkpointing logic.</span></span> <span data-ttu-id="44851-139">Değişiklik akış işlemci kitaplığı otomatik denetim noktası oluşturma ve "en az bir kez" semantiği sağlar.</span><span class="sxs-lookup"><span data-stu-id="44851-139">The change feed processor library provides automatic checkpointing and "at least once" semantics.</span></span>
* <span data-ttu-id="44851-140">Yalnızca en son değişiklik belirli bir belge için değişiklik günlüğünde yer alır.</span><span class="sxs-lookup"><span data-stu-id="44851-140">Only the most recent change for a given document is included in the change log.</span></span> <span data-ttu-id="44851-141">Ara değişikliklerin kullanılamayabilir.</span><span class="sxs-lookup"><span data-stu-id="44851-141">Intermediate changes may not be available.</span></span>
* <span data-ttu-id="44851-142">Değişiklik akışı, her bölüm anahtarı değerini içinde değişiklik sırasına göre sıralanır.</span><span class="sxs-lookup"><span data-stu-id="44851-142">The change feed is sorted by order of modification within each partition key value.</span></span> <span data-ttu-id="44851-143">Bölüm anahtarı değerleri arasında hiçbir garanti edilen sipariş yoktur.</span><span class="sxs-lookup"><span data-stu-id="44851-143">There is no guaranteed order across partition-key values.</span></span>
* <span data-ttu-id="44851-144">Değişiklikleri herhangi noktası zaman eşitlenebilir, diğer bir deyişle, değişiklikler kullanılabilir hiçbir sabit veri saklama süresi vardır.</span><span class="sxs-lookup"><span data-stu-id="44851-144">Changes can be synchronized from any point-in-time, that is, there is no fixed data retention period for which changes are available.</span></span>
* <span data-ttu-id="44851-145">Değişiklikler bölüm anahtar aralıklarına yığınlar halinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="44851-145">Changes are available in chunks of partition key ranges.</span></span> <span data-ttu-id="44851-146">Bu özellik paralel olarak birden çok tüketiciye/sunucuları tarafından işlenmek üzere büyük topluluklara değişikliklerden sağlar.</span><span class="sxs-lookup"><span data-stu-id="44851-146">This capability allows changes from large collections to be processed in parallel by multiple consumers/servers.</span></span>
* <span data-ttu-id="44851-147">Uygulamalar için aynı koleksiyon üzerinde eşzamanlı olarak birden çok değişikliği akışları isteyebilir.</span><span class="sxs-lookup"><span data-stu-id="44851-147">Applications can request for multiple change feeds simultaneously on the same collection.</span></span>

<span data-ttu-id="44851-148">Azure Cosmos veritabanı değişikliği akış tüm hesapları için varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="44851-148">Azure Cosmos DB's change feed is enabled by default for all accounts.</span></span> <span data-ttu-id="44851-149">Kullanabilirsiniz, [sağlanan işleme](request-units.md) yazma bölgenize veya herhangi bir [bölge okuma](distribute-data-globally.md) akış değişikliği okumak için olduğu gibi Azure Cosmos DB'den başka bir işlem.</span><span class="sxs-lookup"><span data-stu-id="44851-149">You can use your [provisioned throughput](request-units.md) in your write region or any [read region](distribute-data-globally.md) to read from the change feed, just like any other operation from Azure Cosmos DB.</span></span> <span data-ttu-id="44851-150">Değişiklik akış ekler ve koleksiyon içindeki belgelerde yapılan güncelleştirme işlemlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="44851-150">The change feed includes inserts and update operations made to documents within the collection.</span></span> <span data-ttu-id="44851-151">Siler yakalayabilirsiniz belgelerinizi siler yerine içinde "soft-Sil" bayrağını ayarlayarak.</span><span class="sxs-lookup"><span data-stu-id="44851-151">You can capture deletes by setting a "soft-delete" flag within your documents in place of deletes.</span></span> <span data-ttu-id="44851-152">Alternatif olarak, sınırlı bir süre belgeleriniz için ayarlayabileceğiniz [TTL yetenek](time-to-live.md), örneğin, 24 saat ve siler yakalamak için o özelliğin değerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="44851-152">Alternatively, you can set a finite expiration period for your documents via the [TTL capability](time-to-live.md), for example, 24 hours and use the value of that property to capture deletes.</span></span> <span data-ttu-id="44851-153">Bu çözüm ile TTL sona erme süresinden daha kısa bir zaman aralığındaki değişiklikleri işlemeye sahip.</span><span class="sxs-lookup"><span data-stu-id="44851-153">With this solution, you have to process changes within a shorter time interval than the TTL expiration period.</span></span> <span data-ttu-id="44851-154">Değişiklik akışı her bölüm anahtarı aralığının belge koleksiyonundaki için kullanılabilir ve bu nedenle bir veya daha fazla tüketiciye paralel işleme üzerinden dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="44851-154">The change feed is available for each partition key range within the document collection, and thus can be distributed across one or more consumers for parallel processing.</span></span> 

![Azure Cosmos DB değişimin dağıtılmış işlem akışı](./media/change-feed/changefeedvisual.png)

<span data-ttu-id="44851-156">İstemci kodunuzda akışı bir değişiklik nasıl uygulayacağınıza, birkaç seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="44851-156">You have a few options in how you implement a change feed in your client code.</span></span> <span data-ttu-id="44851-157">Hemen bölümlerde Azure Cosmos DB REST API ve DocumentDB SDK'ları kullanarak akış değişikliği uygulamak nasıl açıklar.</span><span class="sxs-lookup"><span data-stu-id="44851-157">The sections that immediately follow describe how to implement the change feed using the Azure Cosmos DB REST API and the DocumentDB SDKs.</span></span> <span data-ttu-id="44851-158">Ancak, .NET uygulamaları için yeni kullanmanızı öneririz [değişiklik akış işlemci Kitaplığı](#change-feed-processor) değişikliği olayları işlemek için akış olarak bölümler okuma değişiklikleri basitleştirir ve birden çok iş parçacığı üzerinde çalışırken sağlar Paralel.</span><span class="sxs-lookup"><span data-stu-id="44851-158">However, for .NET applications, we recommend using the new [Change feed processor library](#change-feed-processor) for processing events from the change feed as it simplifies reading changes across partitions and enables multiple threads working in parallel.</span></span> 

## <span data-ttu-id="44851-159"><a id="rest-apis"></a>REST API ve DocumentDB SDK'ları ile çalışma</span><span class="sxs-lookup"><span data-stu-id="44851-159"><a id="rest-apis"></a>Working with the REST API and DocumentDB SDKs</span></span>
<span data-ttu-id="44851-160">Azure Cosmos DB sağlar, depolama ve işleme adlı esnek kapsayıcıları **koleksiyonları**.</span><span class="sxs-lookup"><span data-stu-id="44851-160">Azure Cosmos DB provides elastic containers of storage and throughput called **collections**.</span></span> <span data-ttu-id="44851-161">Veri koleksiyonları içinde mantıksal olarak gruplandırılmış kullanarak [bölüm anahtarlarını](partition-data.md) ölçeklenebilirlik ve performans.</span><span class="sxs-lookup"><span data-stu-id="44851-161">Data within collections is logically grouped using [partition keys](partition-data.md) for scalability and performance.</span></span> <span data-ttu-id="44851-162">Azure Cosmos DB arama kimliği (okuma/Get), sorgu ve okuma beslemelerini (taramalar) dahil olmak üzere bu verilerine erişmek için çeşitli API'ler sağlar.</span><span class="sxs-lookup"><span data-stu-id="44851-162">Azure Cosmos DB provides various APIs for accessing this data, including lookup by ID (Read/Get), query, and read-feeds (scans).</span></span> <span data-ttu-id="44851-163">DocumentDB için iki yeni istek üstbilgileri doldurarak değişiklik akış alınabilir `ReadDocumentFeed` API'sini ve bölüm anahtarlarını aralıklar paralel olarak işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="44851-163">The change feed can be obtained by populating two new request headers to the DocumentDB `ReadDocumentFeed` API, and can be processed in parallel across ranges of partition keys.</span></span>

### <a name="readdocumentfeed-api"></a><span data-ttu-id="44851-164">ReadDocumentFeed API</span><span class="sxs-lookup"><span data-stu-id="44851-164">ReadDocumentFeed API</span></span>
<span data-ttu-id="44851-165">ReadDocumentFeed nasıl çalıştığı bir kısa bakalım.</span><span class="sxs-lookup"><span data-stu-id="44851-165">Let's take a brief look at how ReadDocumentFeed works.</span></span> <span data-ttu-id="44851-166">Azure Cosmos DB destekleyen bir akış bir koleksiyon içinde belgelerin okuma `ReadDocumentFeed` API.</span><span class="sxs-lookup"><span data-stu-id="44851-166">Azure Cosmos DB supports reading a feed of documents within a collection via the `ReadDocumentFeed` API.</span></span> <span data-ttu-id="44851-167">Örneğin, aşağıdaki isteği belgeleri içinde bir sayfasını döndürür `serverlogs` koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="44851-167">For example, the following request returns a page of documents inside the `serverlogs` collection.</span></span> 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

<span data-ttu-id="44851-168">Sonuçları kullanarak bunlarla sınırlı `x-ms-max-item-count` üstbilgi ve okuma sürdürüldü istekle yeniden göndermeden bir `x-ms-continuation` üstbilgi önceki yanıtta döndürülen.</span><span class="sxs-lookup"><span data-stu-id="44851-168">Results can be limited by using the `x-ms-max-item-count` header, and reads can be resumed by resubmitting the request with a `x-ms-continuation` header returned in the previous response.</span></span> <span data-ttu-id="44851-169">Tek bir istemciden gerçekleştirildiğinde `ReadDocumentFeed` seri olarak bölümler sonuçları arasında yineler.</span><span class="sxs-lookup"><span data-stu-id="44851-169">When performed from a single client, `ReadDocumentFeed` iterates through results across partitions serially.</span></span> 

<span data-ttu-id="44851-170">**Seri belge akışı okuma**</span><span class="sxs-lookup"><span data-stu-id="44851-170">**Serial read document feed**</span></span>

<span data-ttu-id="44851-171">Desteklenen birini kullanarak belgelerin akış de alabilirsiniz [Azure Cosmos DB SDK'ları](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="44851-171">You can also retrieve the feed of documents using one of the supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="44851-172">Örneğin, aşağıdaki kod parçacığını nasıl kullanılacağını gösterir [ReadDocumentFeedAsync yöntemi](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) .NET içinde.</span><span class="sxs-lookup"><span data-stu-id="44851-172">For example, the following snippet shows how to use the [ReadDocumentFeedAsync method](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) in .NET.</span></span>

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a><span data-ttu-id="44851-173">ReadDocumentFeed dağıtılmış yürütülmesi</span><span class="sxs-lookup"><span data-stu-id="44851-173">Distributed execution of ReadDocumentFeed</span></span>
<span data-ttu-id="44851-174">Veri ya da daha fazla terabayt içeren veya büyük miktarda güncelleştirme alma koleksiyonlar için tek istemci makineye okuma akıştan seri yürütülmesi pratik olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="44851-174">For collections that contain terabytes of data or more, or ingest a large volume of updates, serial execution of read feed from a single client machine might not be practical.</span></span> <span data-ttu-id="44851-175">Bu büyük veri senaryolarını desteklemek için Azure Cosmos DB dağıtmak için API'ler sağlar `ReadDocumentFeed` çağrıları saydam birden çok istemci okuyucular/tüketicileri arasında.</span><span class="sxs-lookup"><span data-stu-id="44851-175">In order to support these big data scenarios, Azure Cosmos DB provides APIs to distribute `ReadDocumentFeed` calls transparently across multiple client readers/consumers.</span></span> 

<span data-ttu-id="44851-176">**Dağıtılmış okuma belge besleme**</span><span class="sxs-lookup"><span data-stu-id="44851-176">**Distributed Read Document Feed**</span></span>

<span data-ttu-id="44851-177">Sağlamak için ölçeklenebilir artımlı değişiklikler, işleme Azure Cosmos DB genişleme modeli için bölüm anahtarlarını aralıklarını temel alarak API akış değişiklik destekler.</span><span class="sxs-lookup"><span data-stu-id="44851-177">To provide scalable processing of incremental changes, Azure Cosmos DB supports a scale-out model for the change feed API based on ranges of partition keys.</span></span>

* <span data-ttu-id="44851-178">Bir koleksiyon gerçekleştirmek için anahtar aralıklarına bölüm listesini elde edebilirsiniz bir `ReadPartitionKeyRanges` çağırın.</span><span class="sxs-lookup"><span data-stu-id="44851-178">You can obtain a list of partition key ranges for a collection performing a `ReadPartitionKeyRanges` call.</span></span> 
* <span data-ttu-id="44851-179">Her bölüm anahtarı aralığının gerçekleştirdiğiniz bir `ReadDocumentFeed` bu aralıkta bölüm anahtarlarla belgeleri okumak için.</span><span class="sxs-lookup"><span data-stu-id="44851-179">For each partition key range, you can perform a `ReadDocumentFeed` to read documents with partition keys within that range.</span></span>

### <a name="retrieving-partition-key-ranges-for-a-collection"></a><span data-ttu-id="44851-180">Bir koleksiyon için bölüm anahtarı aralıkları alma</span><span class="sxs-lookup"><span data-stu-id="44851-180">Retrieving partition key ranges for a collection</span></span>
<span data-ttu-id="44851-181">Bölüm anahtarı aralıkları isteyerek alabilir `pkranges` bir koleksiyon içindeki kaynak.</span><span class="sxs-lookup"><span data-stu-id="44851-181">You can retrieve the partition key ranges by requesting the `pkranges` resource within a collection.</span></span> <span data-ttu-id="44851-182">Örneğin aşağıdaki isteği bölüm anahtarı aralıklarını listesini alır `serverlogs` koleksiyonu:</span><span class="sxs-lookup"><span data-stu-id="44851-182">For example the following request retrieves the list of partition key ranges for the `serverlogs` collection:</span></span>

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

<span data-ttu-id="44851-183">Bu istek bölüm anahtar aralıklarına hakkındaki meta verileri içeren aşağıdaki yanıtı döndürür:</span><span class="sxs-lookup"><span data-stu-id="44851-183">This request returns the following response containing metadata about the partition key ranges:</span></span>

    HTTP/1.1 200 Ok
    Content-Type: application/json
    x-ms-item-count: 25
    x-ms-schemaversion: 1.1
    Date: Tue, 15 Nov 2016 07:26:51 GMT

    {
       "_rid":"qYcAAPEvJBQ=",
       "PartitionKeyRanges":[
          {
             "_rid":"qYcAAPEvJBQCAAAAAAAAUA==",
             "id":"0",
             "_etag":"\"00002800-0000-0000-0000-580ac4ea0000\"",
             "minInclusive":"",
             "maxExclusive":"05C1CFFFFFFFF8",
             "_self":"dbs\/qYcAAA==\/colls\/qYcAAPEvJBQ=\/pkranges\/qYcAAPEvJBQCAAAAAAAAUA==\/",
             "_ts":1477100776
          },
          ...
       ],
       "_count": 25
    }


<span data-ttu-id="44851-184">**Bölüm anahtarı aralığının özellikleri**: her bölüm anahtarı aralığının aşağıdaki tabloda meta veri özelliklerini içerir:</span><span class="sxs-lookup"><span data-stu-id="44851-184">**Partition key range properties**: Each partition key range includes the metadata properties in the following table:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="44851-185">Üstbilgi adı</span><span class="sxs-lookup"><span data-stu-id="44851-185">Header name</span></span></th>
        <th><span data-ttu-id="44851-186">Açıklama</span><span class="sxs-lookup"><span data-stu-id="44851-186">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="44851-187">id</span><span class="sxs-lookup"><span data-stu-id="44851-187">id</span></span></td>
        <td>
            <p><span data-ttu-id="44851-188">Bölüm anahtarı aralığının kimliği.</span><span class="sxs-lookup"><span data-stu-id="44851-188">The ID for the partition key range.</span></span> <span data-ttu-id="44851-189">Her bir koleksiyonun içindeki kararlı ve benzersiz bir kimliği budur.</span><span class="sxs-lookup"><span data-stu-id="44851-189">This is a stable and unique ID within each collection.</span></span></p>
            <p><span data-ttu-id="44851-190">Aşağıdaki çağrısında değişiklikleri okumak için bölüm anahtarı aralığının tarafından kullanılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="44851-190">Must be used in the following call to read changes by partition key range.</span></span></p>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="44851-191">maxExclusive</span><span class="sxs-lookup"><span data-stu-id="44851-191">maxExclusive</span></span></td>
        <td><span data-ttu-id="44851-192">Bölüm anahtarı aralığının en fazla bölüm anahtar karma değeri.</span><span class="sxs-lookup"><span data-stu-id="44851-192">The maximum partition key hash value for the partition key range.</span></span> <span data-ttu-id="44851-193">İç kullanım için.</span><span class="sxs-lookup"><span data-stu-id="44851-193">For internal use.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="44851-194">minInclusive</span><span class="sxs-lookup"><span data-stu-id="44851-194">minInclusive</span></span></td>
        <td><span data-ttu-id="44851-195">Bölüm anahtarı aralığının en düşük bölüm anahtar karma değeri.</span><span class="sxs-lookup"><span data-stu-id="44851-195">The minimum partition key hash value for the partition key range.</span></span> <span data-ttu-id="44851-196">İç kullanım için.</span><span class="sxs-lookup"><span data-stu-id="44851-196">For internal use.</span></span></td>
    </tr>       
</table>

<span data-ttu-id="44851-197">Desteklenen birini kullanarak bunu yapabilirsiniz [Azure Cosmos DB SDK'ları](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="44851-197">You can do this using one of the supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="44851-198">Örneğin, aşağıdaki kod parçacığında bölüm anahtar aralıklarına .NET kullanarak almak gösterilmiştir [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="44851-198">For example, the following snippet shows how to retrieve partition key ranges in .NET using the [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) method.</span></span>

```csharp
string pkRangesResponseContinuation = null;
List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

do
{
    FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
        collectionUri, 
        new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

    partitionKeyRanges.AddRange(pkRangesResponse);
    pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
}
while (pkRangesResponseContinuation != null);
```

<span data-ttu-id="44851-199">Azure Cosmos DB isteğe bağlı ayarlayarak bölüm anahtarı aralığının başına belge alınmasını destekler `x-ms-documentdb-partitionkeyrangeid` üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="44851-199">Azure Cosmos DB supports retrieval of documents per partition key range by setting the optional `x-ms-documentdb-partitionkeyrangeid` header.</span></span> 

### <a name="performing-an-incremental-readdocumentfeed"></a><span data-ttu-id="44851-200">Bir artımlı ReadDocumentFeed gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="44851-200">Performing an incremental ReadDocumentFeed</span></span>
<span data-ttu-id="44851-201">ReadDocumentFeed değişiklikleri Azure Cosmos DB koleksiyonlarda artımlı işleme için aşağıdaki senaryoları/görevleri destekler:</span><span class="sxs-lookup"><span data-stu-id="44851-201">ReadDocumentFeed supports the following scenarios/tasks for incremental processing of changes in Azure Cosmos DB collections:</span></span>

* <span data-ttu-id="44851-202">Başlangıçtan itibaren belgelere tüm değişiklikler, diğer bir deyişle, koleksiyon oluşturulması okuyun.</span><span class="sxs-lookup"><span data-stu-id="44851-202">Read all changes to documents from the beginning, that is, from collection creation.</span></span>
* <span data-ttu-id="44851-203">Geçerli zamandan ilerideki güncelleştirmeler belgeleri için yapılan tüm değişiklikler veya bir kullanıcı tarafından belirtilen zaman bu yana değişiklikler okuyun.</span><span class="sxs-lookup"><span data-stu-id="44851-203">Read all changes to future updates to documents from current time, or any changes since a user-specified time.</span></span>
* <span data-ttu-id="44851-204">Tüm değişiklikleri (ETag) koleksiyon mantıksal bir sürümünden belgeleri okuyun.</span><span class="sxs-lookup"><span data-stu-id="44851-204">Read all changes to documents from a logical version of the collection (ETag).</span></span> <span data-ttu-id="44851-205">Denetim noktası artımlı okuma akışı isteklerinden döndürülen ETag göre tüketicileriniz olabilir.</span><span class="sxs-lookup"><span data-stu-id="44851-205">You can checkpoint your consumers based on the returned ETag from incremental read-feed requests.</span></span>

<span data-ttu-id="44851-206">Değişiklikleri ekler içeren ve belge güncelleştirmeleri.</span><span class="sxs-lookup"><span data-stu-id="44851-206">The changes include inserts and updates to documents.</span></span> <span data-ttu-id="44851-207">Siler yakalamak için bir "geçici silme" özelliği, belgeler içinde veya kullanmanız gerekir, kullanmak [yerleşik TTL özelliği](time-to-live.md) akış değişiklik bekleyen bir değişikliği göstermek için.</span><span class="sxs-lookup"><span data-stu-id="44851-207">To capture deletes, you must use a "soft delete" property within your documents, or use the [built-in TTL property](time-to-live.md) to signal a pending deletion in the change feed.</span></span>

<span data-ttu-id="44851-208">Aşağıdaki tabloda [isteği](/rest/api/documentdb/common-documentdb-rest-request-headers.md) ve [yanıt üstbilgilerini](/rest/api/documentdb/common-documentdb-rest-response-headers.md) ReadDocumentFeed işlemleri için.</span><span class="sxs-lookup"><span data-stu-id="44851-208">The following table lists the [request](/rest/api/documentdb/common-documentdb-rest-request-headers.md) and [response headers](/rest/api/documentdb/common-documentdb-rest-response-headers.md) for ReadDocumentFeed operations.</span></span>

<span data-ttu-id="44851-209">**İstek üstbilgileri için artımlı ReadDocumentFeed**:</span><span class="sxs-lookup"><span data-stu-id="44851-209">**Request headers for incremental ReadDocumentFeed**:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="44851-210">Üstbilgi adı</span><span class="sxs-lookup"><span data-stu-id="44851-210">Header name</span></span></th>
        <th><span data-ttu-id="44851-211">Açıklama</span><span class="sxs-lookup"><span data-stu-id="44851-211">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="44851-212">BİR IM</span><span class="sxs-lookup"><span data-stu-id="44851-212">A-IM</span></span></td>
        <td><span data-ttu-id="44851-213">"Artımlı akışına" ayarlayın veya gerekir aksi takdirde atlanmış</span><span class="sxs-lookup"><span data-stu-id="44851-213">Must be set to "Incremental feed", or omitted otherwise</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="44851-214">If-None-Match</span><span class="sxs-lookup"><span data-stu-id="44851-214">If-None-Match</span></span></td>
        <td>
            <p><span data-ttu-id="44851-215">Başlık: tüm değişiklikleri (oluşturma koleksiyonu) baştan döndürür</span><span class="sxs-lookup"><span data-stu-id="44851-215">No header: returns all changes from the beginning (collection creation)</span></span></p>
            <p><span data-ttu-id="44851-216">"*": tüm yeni değişiklikleri veri koleksiyonundaki döndürür</span><span class="sxs-lookup"><span data-stu-id="44851-216">"*": returns all new changes to data within the collection</span></span></p>           
            <p><span data-ttu-id="44851-217">&lt;ETag&gt;: ETag, koleksiyon kümesine döndürürse mantıksal zaman damgası itibaren yapılan tüm değişiklikler</span><span class="sxs-lookup"><span data-stu-id="44851-217">&lt;etag&gt;: If set to a collection ETag, returns all changes made since that logical timestamp</span></span></p>
        </td>
    </tr>
    <tr>    
        <td><span data-ttu-id="44851-218">If-Modified-Since</span><span class="sxs-lookup"><span data-stu-id="44851-218">If-Modified-Since</span></span></td> 
        <td><span data-ttu-id="44851-219">RFC 1123 saat biçimi; If-None-Match belirtilmişse göz ardı</span><span class="sxs-lookup"><span data-stu-id="44851-219">RFC 1123 time format; ignored if If-None-Match is specified</span></span></td> 
    </tr> 
    <tr>
        <td><span data-ttu-id="44851-220">x-ms-documentdb-partitionkeyrangeid</span><span class="sxs-lookup"><span data-stu-id="44851-220">x-ms-documentdb-partitionkeyrangeid</span></span></td>
        <td><span data-ttu-id="44851-221">Verilerin okunması için bölüm anahtarı aralığının kimliği.</span><span class="sxs-lookup"><span data-stu-id="44851-221">The partition key range ID for reading data.</span></span></td>
    </tr>
</table>

<span data-ttu-id="44851-222">**Yanıt üstbilgileri için artımlı ReadDocumentFeed**:</span><span class="sxs-lookup"><span data-stu-id="44851-222">**Response headers for incremental ReadDocumentFeed**:</span></span>

<table> <tr>
        <th><span data-ttu-id="44851-223">Üstbilgi adı</span><span class="sxs-lookup"><span data-stu-id="44851-223">Header name</span></span></th>
        <th><span data-ttu-id="44851-224">Açıklama</span><span class="sxs-lookup"><span data-stu-id="44851-224">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="44851-225">ETag</span><span class="sxs-lookup"><span data-stu-id="44851-225">etag</span></span></td>
        <td>
            <p><span data-ttu-id="44851-226">Yanıtta döndürülen son belgenin mantıksal sıra numarası (LSN).</span><span class="sxs-lookup"><span data-stu-id="44851-226">The logical sequence number (LSN) of last document returned in the response.</span></span></p>
            <p><span data-ttu-id="44851-227">Artımlı ReadDocumentFeed If-None-Match bu değeri yeniden göndermeden ettirilebilir.</span><span class="sxs-lookup"><span data-stu-id="44851-227">Incremental ReadDocumentFeed can be resumed by resubmitting this value in If-None-Match.</span></span></p>
        </td>
    </tr>
</table>

<span data-ttu-id="44851-228">Mantıksal sürüm/Etag'den koleksiyonundaki tüm artımlı değişiklikler döndürülecek bir örnek istek işte `28535` ve bölüm anahtarı aralığının = `16`:</span><span class="sxs-lookup"><span data-stu-id="44851-228">Here's a sample request to return all incremental changes in collection from the logical version/ETag `28535` and partition key range = `16`:</span></span>

    GET https://mydocumentdb.documents.azure.com/dbs/bigdb/colls/bigcoll/docs HTTP/1.1
    x-ms-max-item-count: 1
    If-None-Match: "28535"
    A-IM: Incremental feed
    x-ms-documentdb-partitionkeyrangeid: 16
    x-ms-date: Tue, 22 Nov 2016 20:43:01 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dzdpL2QQ8TCfiNbW%2fEcT88JHNvWeCgDA8gWeRZ%2btfN5o%3d
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

<span data-ttu-id="44851-229">Değişiklikleri süre içinde bölüm anahtarı aralığının her bölüm anahtarı değerine göre sıralanır.</span><span class="sxs-lookup"><span data-stu-id="44851-229">Changes are ordered by time within each partition key value within the partition key range.</span></span> <span data-ttu-id="44851-230">Bölüm anahtarı değerleri arasında hiçbir garanti edilen sipariş yoktur.</span><span class="sxs-lookup"><span data-stu-id="44851-230">There is no guaranteed order across partition-key values.</span></span> <span data-ttu-id="44851-231">Tek bir sayfayla sığmayacak daha fazla sonuç yoksa istekle yeniden göndermeden sonraki sonuç sayfasını okuyabilirsiniz `If-None-Match` değerine eşit bir değer üstbilgiyle `etag` önceki yanıt gelen.</span><span class="sxs-lookup"><span data-stu-id="44851-231">If there are more results than can fit in a single page, you can read the next page of results by resubmitting the request with the `If-None-Match` header with value equal to the `etag` from the previous response.</span></span> <span data-ttu-id="44851-232">Birden çok belge eklendi veya işlemsel olarak bir saklı yordam veya tetikleyici içinde güncelleştirildi, bunların tümü aynı yanıt sayfa içinde döndürülür.</span><span class="sxs-lookup"><span data-stu-id="44851-232">If multiple documents were inserted or updated transactionally within a stored procedure or trigger, they will all be returned within the same response page.</span></span>

> [!NOTE]
> <span data-ttu-id="44851-233">Değişiklik akış ile daha fazla öğe bir sayfa içinde belirtilenden döndürülen alabilirsiniz `x-ms-max-item-count` eklenir veya güncelleştirilir saklı yordamların içinde birden çok belge durumunda veya tetikler.</span><span class="sxs-lookup"><span data-stu-id="44851-233">With change feed, you might get more items returned in a page than specified in `x-ms-max-item-count` in the case of multiple documents inserted or updated inside a stored procedures or triggers.</span></span> 

<span data-ttu-id="44851-234">.NET SDK'sı (1.17.0) kullanırken, alan kümesi `StartTime` içinde `ChangeFeedOptions` bu yana değişen belgeleri doğrudan döndürülecek `StartTime` çağrılırken `CreateDocumentChangeFeedQuery`.</span><span class="sxs-lookup"><span data-stu-id="44851-234">When using the .NET SDK (1.17.0), set the field `StartTime` in `ChangeFeedOptions` to directly return changed documents since `StartTime` when calling  `CreateDocumentChangeFeedQuery`.</span></span> <span data-ttu-id="44851-235">Belirterek `If-Modified-Since` REST API kullanarak, isteğiniz belgelerin değil kendilerini ancak bunun yerine devamlılık belirteci döndürür veya `etag` yanıt üstbilgisi içinde.</span><span class="sxs-lookup"><span data-stu-id="44851-235">By specifying `If-Modified-Since` using the REST API, your request will return not the documents themselves, but rather the continuation token or `etag` in the response header.</span></span> <span data-ttu-id="44851-236">Belgeleri değiştiren devamlılık belirteci belirtilen zaman döndürülecek `etag` ardından sonraki istekle kullanılmalıdır `If-None-Match` gerçek belgeleri döndürülecek.</span><span class="sxs-lookup"><span data-stu-id="44851-236">To return the documents modified the specified time, the continuation token `etag` must then be used in the next request with `If-None-Match` to return the actual documents.</span></span> 

<span data-ttu-id="44851-237">.NET SDK'sı sağlar [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) ve [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) bir koleksiyona yapılan değişiklikler erişmek için yardımcı sınıfları.</span><span class="sxs-lookup"><span data-stu-id="44851-237">The .NET SDK provides the [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) and [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) helper classes to access changes made to a collection.</span></span> <span data-ttu-id="44851-238">Aşağıdaki kod parçacığında, tek bir istemciden gelen .NET SDK kullanarak başından tüm değişiklikleri almak gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="44851-238">The following snippet shows how to retrieve all changes from the beginning using the .NET SDK from a single client.</span></span>

```csharp
private async Task<Dictionary<string, string>> GetChanges(
    DocumentClient client,
    string collection,
    Dictionary<string, string> checkpoints)
{
    string pkRangesResponseContinuation = null;
    List<PartitionKeyRange> partitionKeyRanges = new List<PartitionKeyRange>();

    do
    {
        FeedResponse<PartitionKeyRange> pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
            collectionUri, 
            new FeedOptions { RequestContinuation = pkRangesResponseContinuation });

        partitionKeyRanges.AddRange(pkRangesResponse);
        pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
    }
    while (pkRangesResponseContinuation != null);

    foreach (PartitionKeyRange pkRange in partitionKeyRanges)
    {
        string continuation = null;
        checkpoints.TryGetValue(pkRange.Id, out continuation);

        IDocumentQuery<Document> query = client.CreateDocumentChangeFeedQuery(
            collection,
            new ChangeFeedOptions
            {
                PartitionKeyRangeId = pkRange.Id,
                StartFromBeginning = true,
                RequestContinuation = continuation,
                MaxItemCount = 1
            });

        while (query.HasMoreResults)
        {
            FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

            foreach (DeviceReading changedDocument in readChangesResponse)
            {
                Console.WriteLine(changedDocument.Id);
            }

            checkpoints[pkRange.Id] = readChangesResponse.ResponseContinuation;
        }
    }

    return checkpoints;
}
```
<span data-ttu-id="44851-239">Ve aşağıdaki kod parçacığında, değişiklikleri işlemeye gösterilmiştir kullanarak Azure Cosmos DB ile gerçek zamanlı değişikliği desteği ve önceki işlevi akış.</span><span class="sxs-lookup"><span data-stu-id="44851-239">And the following snippet shows how to process changes in real-time with Azure Cosmos DB by using the change feed support and the preceding function.</span></span> <span data-ttu-id="44851-240">İlk çağrıda koleksiyondaki tüm belgeleri döndürür ve ikinci yalnızca en son kontrol bu yana oluşturulan iki belge oluşturulan döndürür.</span><span class="sxs-lookup"><span data-stu-id="44851-240">The first call returns all the documents in the collection, and the second only returns the two documents created that were created since the last checkpoint.</span></span>

```csharp
// Returns all documents in the collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only the two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

<span data-ttu-id="44851-241">Seçmeli olarak olayları işlemek için istemci tarafı mantığı kullanarak akış değişiklik de filtre uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44851-241">You can also filter the change feed using client side logic to selectively process events.</span></span> <span data-ttu-id="44851-242">Örneğin, aygıt algılayıcılar yalnızca sıcaklık değişikliği olayları işlemek için istemci tarafı LINQ kullanan bir parçacığı aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="44851-242">For example, here's a snippet that uses client side LINQ to process only temperature change events from device sensors.</span></span>

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <span data-ttu-id="44851-243"><a id="change-feed-processor"></a>Değişiklik işlemci akışı kitaplığı</span><span class="sxs-lookup"><span data-stu-id="44851-243"><a id="change-feed-processor"></a>Change Feed Processor library</span></span>
<span data-ttu-id="44851-244">Başka bir seçenek kullanmaktır [Azure Cosmos DB değiştirmek akış işlemci Kitaplığı](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), hangi yardımcı olabilir, olay arasında birden çok tüketiciye akışı bir değişiklik gelen işleme kolayca dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44851-244">Another option is to use the [Azure Cosmos DB Change Feed Processor library](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), which can help you easily distribute event processing from a change feed across multiple consumers.</span></span> <span data-ttu-id="44851-245">Kitaplığı, .NET platformu üzerinde okuyucular akış değişiklik oluşturmak için mükemmeldir.</span><span class="sxs-lookup"><span data-stu-id="44851-245">The library is great for building change feed readers on the .NET platform.</span></span> <span data-ttu-id="44851-246">Diğer Cosmos DB SDK içinde bulunan yöntemleri üzerinde değişiklik akış işlemci kitaplığı kullanılarak Basitleştirilmiş bazı iş akışları içerir:</span><span class="sxs-lookup"><span data-stu-id="44851-246">Some workflows that would be simplified by using the Change Feed Processor library over the methods included in the other Cosmos DB SDKs include:</span></span> 

* <span data-ttu-id="44851-247">Birden çok bölüm arasında veri depolandığında değişiklik çekilmesini güncelleştirmelerini akışı</span><span class="sxs-lookup"><span data-stu-id="44851-247">Pulling updates from change feed when data is stored across multiple partitions</span></span>
* <span data-ttu-id="44851-248">Taşıma veya verileri bir koleksiyondan çoğaltma</span><span class="sxs-lookup"><span data-stu-id="44851-248">Moving or replicating data from one collection to another</span></span>
* <span data-ttu-id="44851-249">Veri ve akış değişiklik güncelleştirmelerini tarafından tetiklenen eylemlerin Paralel yürütme</span><span class="sxs-lookup"><span data-stu-id="44851-249">Parallel execution of actions triggered by updates to data and change feed</span></span> 

<span data-ttu-id="44851-250">Cosmos SDK API'leri kullanarak her bölüm akış güncelleştirmelerinde değiştirmek için kesin erişim sağlarken, akış işlemci değiştirmek kitaplığını kullanarak bölümler ve paralel çalışan birden çok iş parçacığı üzerinde okuma değişiklikleri basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="44851-250">While using the APIs in the Cosmos SDKs provides precise access to change feed updates in each partition, using the Change Feed Processor library simplifies reading changes across partitions and multiple threads working in parallel.</span></span> <span data-ttu-id="44851-251">El ile değişiklikleri her kapsayıcıdan okuma ve kaydetme her bölüm için devamlılık belirteci yerine akış değişiklik işlemci okuma değişiklikleri bir kiralama mekanizması kullanarak bölümleri arasında otomatik olarak yönetir.</span><span class="sxs-lookup"><span data-stu-id="44851-251">Instead of manually reading changes from each container and saving a continuation token for each partition, the Change Feed Processor automatically manages reading changes across partitions using a lease mechanism.</span></span>

<span data-ttu-id="44851-252">Bir NuGet paketi olarak kullanılabilir bir kitaplığıdır: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) ve bir Github olarak kaynak koddan [örnek](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor).</span><span class="sxs-lookup"><span data-stu-id="44851-252">The library is available as a NuGet Package: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) and from source code as a Github [sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor).</span></span> 

### <a name="understanding-change-feed-processor-library"></a><span data-ttu-id="44851-253">Anlama değişiklik akış işlemci kitaplığı</span><span class="sxs-lookup"><span data-stu-id="44851-253">Understanding Change Feed Processor library</span></span> 

<span data-ttu-id="44851-254">Akış değişiklik işlemci gerçekleştirilmesinin dört ana bileşen mevcuttur: izlenen koleksiyonu, kira koleksiyonu, işlemci ana bilgisayar ve tüketicilerin.</span><span class="sxs-lookup"><span data-stu-id="44851-254">There are four main components of implementing the Change Feed Processor: the monitored collection, the lease collection, the processor host, and the consumers.</span></span> 

<span data-ttu-id="44851-255">**İzlenen koleksiyonu:** değişiklik akış oluşturulan verileri izlenen koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="44851-255">**Monitored Collection:** The monitored collection is the data from which the change feed is generated.</span></span> <span data-ttu-id="44851-256">Tüm eklemeleri ve değişiklikleri izlenen koleksiyonu için koleksiyon değişiklik akışta yansıtılır.</span><span class="sxs-lookup"><span data-stu-id="44851-256">Any inserts and changes to the monitored collection are reflected in the change feed of the collection.</span></span> 

<span data-ttu-id="44851-257">**Kira koleksiyonu:** arasında birden çok Worker akış değişiklik işleme kira koleksiyonu koordinatları.</span><span class="sxs-lookup"><span data-stu-id="44851-257">**Lease Collection:** The lease collection coordinates processing the change feed across multiple workers.</span></span> <span data-ttu-id="44851-258">Ayrı bir koleksiyon, bölüm başına bir kiralama ile kiraları depolamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="44851-258">A separate collection is used to store the leases with one lease per partition.</span></span> <span data-ttu-id="44851-259">Akış değişiklik işlemci çalıştığı yazma bölgeyi daha yakın olan farklı bir hesap üzerinde bu kira koleksiyon depolamak için avantajlıdır.</span><span class="sxs-lookup"><span data-stu-id="44851-259">It is advantageous to store this lease collection on a different account with the write region closer to where the Change Feed Processor is running.</span></span> <span data-ttu-id="44851-260">Bir kira nesnesi aşağıdaki öznitelikleri içerir:</span><span class="sxs-lookup"><span data-stu-id="44851-260">A lease object contains the following attributes:</span></span> 
* <span data-ttu-id="44851-261">Sahibi: kira sahibi olan konak belirtir</span><span class="sxs-lookup"><span data-stu-id="44851-261">Owner: Specifies the host that owns the lease</span></span>
* <span data-ttu-id="44851-262">Devamlılık: belirli bir bölüm için akış değişiklik (devamlılık belirteci) konumu belirtir</span><span class="sxs-lookup"><span data-stu-id="44851-262">Continuation: Specifies the position (continuation token) in the change feed for a particular partition</span></span>
* <span data-ttu-id="44851-263">Zaman damgası: kira güncelleştirildi; son zamanı zaman damgası, kira süresi dolmuş olarak kabul edilip edilmediğini kontrol etmek için kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="44851-263">Timestamp: Last time lease was updated; the timestamp can be used to check whether the lease is considered expired</span></span> 

<span data-ttu-id="44851-264">**İşlemci ana bilgisayarı:** etkin kiralamaları kaç ana örneklerini olmadığına göre işlem kaç bölümler her konak belirler.</span><span class="sxs-lookup"><span data-stu-id="44851-264">**Processor Host:** Each host determines how many partitions to process based on how many other instances of hosts have active leases.</span></span> 
1.  <span data-ttu-id="44851-265">Bir ana bilgisayar başlatıldığında tüm ana bilgisayarlar arasında iş yükünü dengelemek için kiraları alır.</span><span class="sxs-lookup"><span data-stu-id="44851-265">When a host starts up, it acquires leases to balance the workload across all hosts.</span></span> <span data-ttu-id="44851-266">Kira etkin şekilde bir ana bilgisayar kiralama, düzenli aralıklarla yeniler.</span><span class="sxs-lookup"><span data-stu-id="44851-266">A host periodically renews leases, so leases remain active.</span></span> 
2.  <span data-ttu-id="44851-267">Bir ana bilgisayar kontrol noktaları da son kirasını her devamlılık belirteci okuyun.</span><span class="sxs-lookup"><span data-stu-id="44851-267">A host checkpoints the last continuation token to its lease for each read.</span></span> <span data-ttu-id="44851-268">Eşzamanlılık güvenliği sağlamak için her bir kira güncelleştirme ETag bir ana bilgisayar denetler.</span><span class="sxs-lookup"><span data-stu-id="44851-268">To ensure concurrency safety, a host checks the ETag for each lease update.</span></span> <span data-ttu-id="44851-269">Diğer denetim noktası stratejileri de desteklenir.</span><span class="sxs-lookup"><span data-stu-id="44851-269">Other checkpoint strategies are also supported.</span></span>  
3.  <span data-ttu-id="44851-270">Kapatma, bağlı bir konak tüm kira serbest bırakır, ancak depolanan denetim noktası dosyasından okuma daha sonra devam edebilmek için devamlılık bilgileri tutar.</span><span class="sxs-lookup"><span data-stu-id="44851-270">Upon shutdown, a host releases all leases but keeps the continuation information, so it can resume reading from the stored checkpoint later.</span></span> 

<span data-ttu-id="44851-271">Şu anda konakların sayısı bölümleri (kiraları) sayısından büyük olamaz.</span><span class="sxs-lookup"><span data-stu-id="44851-271">At this time the number of hosts cannot be greater than the number of partitions (leases).</span></span>

<span data-ttu-id="44851-272">**Tüketiciler:** tüketici veya çalışanları olan her konak tarafından başlatılan akış değişiklik yönlendirilmeden iş parçacığı.</span><span class="sxs-lookup"><span data-stu-id="44851-272">**Consumers:** Consumers, or workers, are threads that perform the change feed processing initiated by each host.</span></span> <span data-ttu-id="44851-273">Her işlemci ana bilgisayarın birden çok tüketiciye sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="44851-273">Each processor host can have multiple consumers.</span></span> <span data-ttu-id="44851-274">Her bir tüketici değişikliği atandığı bölümünden akış ve değişiklikleri ana bilgisayar bildirir ve kira süresi okur.</span><span class="sxs-lookup"><span data-stu-id="44851-274">Each consumer reads the change feed from the partition it is assigned to and notifies its host of changes and expired leases.</span></span>

<span data-ttu-id="44851-275">Daha fazla değişiklik akış işlemci dört bu unsuru birlikte nasıl çalıştığını anlamak için aşağıdaki diyagramda bir örnekte bakalım.</span><span class="sxs-lookup"><span data-stu-id="44851-275">To further understand how these four elements of Change Feed Processor work together, let's look at an example in the following diagram.</span></span> <span data-ttu-id="44851-276">İzlenen koleksiyonu belgeleri depolar ve "Şehir" Bölüm anahtarı olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="44851-276">The monitored collection stores documents and uses the "city" as the partition key.</span></span> <span data-ttu-id="44851-277">Mavi bölüm "Şehir" alanını "A-E" belgeler vb. içerdiğini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="44851-277">We see that the blue partition contains documents with the "city" field from "A-E" and so on.</span></span> <span data-ttu-id="44851-278">Her iki tüketicileri paralel dört bölümden okuma ile iki ana vardır.</span><span class="sxs-lookup"><span data-stu-id="44851-278">There are two hosts, each with two consumers reading from the four partitions in parallel.</span></span> <span data-ttu-id="44851-279">Oklar, belirli bir nokta akış değişikliği okuma tüketicileri gösterir.</span><span class="sxs-lookup"><span data-stu-id="44851-279">The arrows show the consumers reading from a specific spot in the change feed.</span></span> <span data-ttu-id="44851-280">Mavi akış değişiklik zaten okuma değişiklikleri temsil ederken, ilk bölümü Koyu mavi okunmamış değişiklikler temsil eder.</span><span class="sxs-lookup"><span data-stu-id="44851-280">In the first partition, the darker blue represents unread changes while the light blue represents the already read changes on the change feed.</span></span> <span data-ttu-id="44851-281">Ana bilgisayarlar, her tüketici geçerli okuma konumunu izlemek için bir "devamlılık" değeri depolamak için kira koleksiyonunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="44851-281">The hosts use the lease collection to store a "continuation" value to keep track of the current reading position for each consumer.</span></span> 

![Azure Cosmos DB değişikliği kullanarak akış işlemcisi konağı](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a><span data-ttu-id="44851-283">Değişiklik kullanarak akış işlemci kitaplığı</span><span class="sxs-lookup"><span data-stu-id="44851-283">Using Change Feed Processor Library</span></span> 
<span data-ttu-id="44851-284">Aşağıdaki bölümde, bir hedef koleksiyona kaynak koleksiyondan değişiklikleri çoğaltmaya bağlamı değişiklik akış işlemci kitaplıkta kullanımı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="44851-284">The following section explains how to use the Change Feed Processor library in the context of replicating changes from a source collection to a destination collection.</span></span> <span data-ttu-id="44851-285">Burada, kaynak koleksiyonu değişiklik akış işlemcide izlenen koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="44851-285">Here, the source collection is the monitored collection in Change Feed Processor.</span></span> 

<span data-ttu-id="44851-286">**Yükleme ve değişiklik akış işlemci NuGet paketini ekleyin**</span><span class="sxs-lookup"><span data-stu-id="44851-286">**Install and include the Change Feed Processor NuGet package**</span></span> 

<span data-ttu-id="44851-287">Değişiklik akış işlemci NuGet paketini yüklemeden önce ilk yükleyin:</span><span class="sxs-lookup"><span data-stu-id="44851-287">Before installing Change Feed Processor NuGet Package, first install:</span></span> 
* <span data-ttu-id="44851-288">Microsoft.Azure.DocumentDB, sürüm 1.13.1 veya üstü</span><span class="sxs-lookup"><span data-stu-id="44851-288">Microsoft.Azure.DocumentDB, version 1.13.1 or above</span></span> 
* <span data-ttu-id="44851-289">Newtonsoft.Json, sürüm 9.0.1 veya yükleme yukarıda `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` ve bir başvuru olarak dahil edin.</span><span class="sxs-lookup"><span data-stu-id="44851-289">Newtonsoft.Json, version 9.0.1 or above Install `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` and include it as a reference.</span></span>

<span data-ttu-id="44851-290">**İzlenen, kiralama ve hedef koleksiyon oluşturma**</span><span class="sxs-lookup"><span data-stu-id="44851-290">**Create a monitored, lease and destination collection**</span></span> 

<span data-ttu-id="44851-291">Değişiklik akış işlemci kitaplığı kullanmak için kira koleksiyonu işlemci boşaltıyor çalıştırmadan önce oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="44851-291">In order to use the Change Feed Processor Library, the lease collection needs to be created before running the processor host(s).</span></span> <span data-ttu-id="44851-292">Yeniden bölgesiyle akış değişiklik işlemci çalıştığı için yazma yakın farklı bir hesap üzerinde bir kira koleksiyon depolamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="44851-292">Again, we recommend storing a lease collection on a different account with a write region closer to where the Change Feed Processor is running.</span></span> <span data-ttu-id="44851-293">Bu veri taşıma örneği oluşturmamız değişiklik akış işleyicisi konağı çalıştırmadan önce hedef koleksiyonu gerekir.</span><span class="sxs-lookup"><span data-stu-id="44851-293">In this data movement example, we need to create the destination collection before running the Change Feed Processor host.</span></span> <span data-ttu-id="44851-294">Kiralanmış, izlenen, oluşturmak için yardımcı yöntem diyoruz örnek kod ve zaten mevcut değilse hedef koleksiyonları.</span><span class="sxs-lookup"><span data-stu-id="44851-294">In the sample code we call a helper method to create the monitored, leased, and destination collections if they do not already exist.</span></span> 

> [!WARNING]
> <span data-ttu-id="44851-295">Uygulamanın Azure Cosmos DB ile iletişim kurmak işleme ayırma gibi bir koleksiyon oluşturma, fiyatlandırmaya vardır.</span><span class="sxs-lookup"><span data-stu-id="44851-295">Creating a collection has pricing implications, as you are reserving throughput for the application to communicate with Azure Cosmos DB.</span></span> <span data-ttu-id="44851-296">Daha fazla ayrıntı için lütfen ziyaret [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/cosmos-db/)</span><span class="sxs-lookup"><span data-stu-id="44851-296">For more details, please visit the [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

<span data-ttu-id="44851-297">*İşlemci konak oluşturma*</span><span class="sxs-lookup"><span data-stu-id="44851-297">*Creating a processor host*</span></span>

<span data-ttu-id="44851-298">`ChangeFeedProcessorHost` Sınıfı, olay işlemcisi uygulamaları için aynı zamanda denetim noktası oluşturma ve bölüm kiralama Yönetimi sağlayan bir iş parçacığı, çok işlemli, güvenli çalışma zamanı ortamı sağlar.</span><span class="sxs-lookup"><span data-stu-id="44851-298">The `ChangeFeedProcessorHost` class provides a thread-safe, multi-process, safe runtime environment for event processor implementations that also provides checkpointing and partition lease management.</span></span> <span data-ttu-id="44851-299">Kullanılacak `ChangeFeedProcessorHost` sınıfı, uygulayabilirsiniz `IChangeFeedObserver`.</span><span class="sxs-lookup"><span data-stu-id="44851-299">To use the `ChangeFeedProcessorHost` class, you can implement `IChangeFeedObserver`.</span></span> <span data-ttu-id="44851-300">Bu arabirim üç yöntem içerir:</span><span class="sxs-lookup"><span data-stu-id="44851-300">This interface contains three methods:</span></span>

* <span data-ttu-id="44851-301">`OpenAsync`: Bu işlev, değişiklik akış gözlemci açıldığında çağrılır.</span><span class="sxs-lookup"><span data-stu-id="44851-301">`OpenAsync`: This function is called when change feed observer is opened.</span></span> <span data-ttu-id="44851-302">Tüketici/gözlemci açıldığında, belirli bir eylemi gerçekleştirmek için değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="44851-302">It can be modified to perform a specific action when consumer/observer is opened.</span></span>  
* <span data-ttu-id="44851-303">`CloseAsync`: Değişiklik akış gözlemci sonlandırıldığında bu işlev çağrılır.</span><span class="sxs-lookup"><span data-stu-id="44851-303">`CloseAsync`: This function is called when change feed observer is terminated.</span></span> <span data-ttu-id="44851-304">Tüketici/gözlemci kapatıldığında belirli bir eylemi gerçekleştirmek için değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="44851-304">It can be modified to perform a specific action when consumer/observer is closed.</span></span>  
* <span data-ttu-id="44851-305">`ProcessChangesAsync`: Belge yeni değişiklikleri değişiklik Besleme üzerindeki kullanılabilir olduğunda bu işlev çağrılır.</span><span class="sxs-lookup"><span data-stu-id="44851-305">`ProcessChangesAsync`: This function is called when document new changes are available on change feed.</span></span> <span data-ttu-id="44851-306">Güncelleştirme akışı her değişiklik sırasında belirli bir eylemi gerçekleştirmek için değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="44851-306">It can be modified to perform a specific action upon every change feed update.</span></span>  

<span data-ttu-id="44851-307">Bizim örneğimizde, biz arabirimini uygulayan `IChangeFeedObserver` aracılığıyla `DocumentFeedObserver` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="44851-307">In our example, we implement the interface `IChangeFeedObserver` through the `DocumentFeedObserver` class.</span></span> <span data-ttu-id="44851-308">Burada, `ProcessChangesAsync` işlev değişikliği belgeden akışı hedef koleksiyona upserts (güncelleştirmeler).</span><span class="sxs-lookup"><span data-stu-id="44851-308">Here, the `ProcessChangesAsync` function upserts (updates) a document from change feed into the destination collection.</span></span> <span data-ttu-id="44851-309">Bu örnek veri bir koleksiyondan başka bir veri kümesinin bölüm anahtarı değiştirmek için taşıma için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="44851-309">This example is useful for moving data from one collection to another in order to change the partition key of a data set.</span></span> 

<span data-ttu-id="44851-310">*İşlemci ana çalışan*</span><span class="sxs-lookup"><span data-stu-id="44851-310">*Running the Processor Host*</span></span>

<span data-ttu-id="44851-311">Olay işleme başlamadan önce her ikisi de akış seçeneklerini değiştirin ve akış konak seçeneklerini değiştirme özelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="44851-311">Before beginning event processing, both change feed options and change feed host options can be customized.</span></span> 
```csharp
    // Customizable change feed option and host options 
    ChangeFeedOptions feedOptions = new ChangeFeedOptions();

    // ie customize StartFromBeginning so change feed reads from beginning
    // can customize MaxItemCount, PartitonKeyRangeId, RequestContinuation, SessionToken and StartFromBeginning
    feedOptions.StartFromBeginning = true;

    ChangeFeedHostOptions feedHostOptions = new ChangeFeedHostOptions();

    // ie. customizing lease renewal interval to 15 seconds
    // can customize LeaseRenewInterval, LeaseAcquireInterval, LeaseExpirationInterval, FeedPollDelay 
    feedHostOptions.LeaseRenewInterval = TimeSpan.FromSeconds(15);

```
<span data-ttu-id="44851-312">Özelleştirilebilir belirli alanları aşağıdaki tabloda özetlenmiştir.</span><span class="sxs-lookup"><span data-stu-id="44851-312">The specific fields that can be customized are summarized in the following tables.</span></span> 

<span data-ttu-id="44851-313">**Akış seçeneklerini değiştirme**:</span><span class="sxs-lookup"><span data-stu-id="44851-313">**Change Feed Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="44851-314">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="44851-314">Property Name</span></span></th>
        <th><span data-ttu-id="44851-315">Açıklama</span><span class="sxs-lookup"><span data-stu-id="44851-315">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="44851-316">MaxItemCount</span><span class="sxs-lookup"><span data-stu-id="44851-316">MaxItemCount</span></span></td>
        <td><span data-ttu-id="44851-317">Alır veya numaralandırma işlemi Azure Cosmos DB veritabanı Hizmet döndürülecek öğe sayısının üst sınırını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="44851-317">Gets or sets the maximum number of items to be returned in the enumeration operation in the Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="44851-318">PartitionKeyRangeId</span><span class="sxs-lookup"><span data-stu-id="44851-318">PartitionKeyRangeId</span></span></td>
        <td><span data-ttu-id="44851-319">Kimliğini alır veya bölüm anahtarı aralığının geçerli istek için Azure Cosmos DB veritabanı hizmetinin ayarlar.</span><span class="sxs-lookup"><span data-stu-id="44851-319">Gets or sets the partition key range id for the current request in the Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="44851-320">RequestContinuation</span><span class="sxs-lookup"><span data-stu-id="44851-320">RequestContinuation</span></span></td>
        <td><span data-ttu-id="44851-321">Alır veya Azure Cosmos DB veritabanı hizmeti isteği devamlılık belirteci ayarlar.</span><span class="sxs-lookup"><span data-stu-id="44851-321">Gets or sets the request continuation token in the Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="44851-322">SessionToken</span><span class="sxs-lookup"><span data-stu-id="44851-322">SessionToken</span></span></td>
        <td><span data-ttu-id="44851-323">Alır veya Azure Cosmos DB veritabanı hizmetinde oturum tutarlılığı ile kullanmak için oturum belirteci ayarlar.</span><span class="sxs-lookup"><span data-stu-id="44851-323">Gets or sets the session token for use with session consistency in the Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="44851-324">StartFromBeginning</span><span class="sxs-lookup"><span data-stu-id="44851-324">StartFromBeginning</span></span></td>
        <td><span data-ttu-id="44851-325">Alır veya Azure Cosmos DB veritabanı hizmetinin akış değişiklik başına (true) ya da geçerli (false) başlamalıdır olup olmadığını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="44851-325">Gets or sets whether change feed in the Azure Cosmos DB database service should start from the beginning (true) or from current (false).</span></span> <span data-ttu-id="44851-326">Varsayılan olarak, geçerli (false) başlar.</span><span class="sxs-lookup"><span data-stu-id="44851-326">By default, it starts from current (false).</span></span></td>
    </tr>
</table>

<span data-ttu-id="44851-327">**Akış konak seçeneklerini değiştirme**:</span><span class="sxs-lookup"><span data-stu-id="44851-327">**Change Feed Host Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="44851-328">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="44851-328">Property Name</span></span></th>
        <th><span data-ttu-id="44851-329">Tür</span><span class="sxs-lookup"><span data-stu-id="44851-329">Type</span></span></th>
        <th><span data-ttu-id="44851-330">Açıklama</span><span class="sxs-lookup"><span data-stu-id="44851-330">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="44851-331">LeaseRenewInterval</span><span class="sxs-lookup"><span data-stu-id="44851-331">LeaseRenewInterval</span></span></td>
        <td><span data-ttu-id="44851-332">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="44851-332">TimeSpan</span></span></td>
        <td><span data-ttu-id="44851-333">Şu anda ChangeFeedEventHost örneği tarafından tutulan bölümler için seçtiğiniz aralık tüm kiraları için.</span><span class="sxs-lookup"><span data-stu-id="44851-333">The interval for all leases for partitions currently held by the ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="44851-334">LeaseAcquireInterval</span><span class="sxs-lookup"><span data-stu-id="44851-334">LeaseAcquireInterval</span></span></td>
        <td><span data-ttu-id="44851-335">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="44851-335">TimeSpan</span></span></td>
        <td><span data-ttu-id="44851-336">Bölümler bilinen konak örnekler arasında eşit şekilde dağıtılıp dağıtılmadığını işlem için bir görevi devre dışı kazandırın aralığı.</span><span class="sxs-lookup"><span data-stu-id="44851-336">The interval to kick off a task to compute whether partitions are distributed evenly among known host instances.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="44851-337">LeaseExpirationInterval</span><span class="sxs-lookup"><span data-stu-id="44851-337">LeaseExpirationInterval</span></span></td>
        <td><span data-ttu-id="44851-338">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="44851-338">TimeSpan</span></span></td>
        <td><span data-ttu-id="44851-339">Kira bir bölüm temsil eden bir kira alınır aralığı.</span><span class="sxs-lookup"><span data-stu-id="44851-339">The interval for which the lease is taken on a lease representing a partition.</span></span> <span data-ttu-id="44851-340">Kira bu aralıkta yenilenmezse, süresi doldu ve bölüm sahipliğini başka bir ChangeFeedEventHost örneğine taşır.</span><span class="sxs-lookup"><span data-stu-id="44851-340">If the lease is not renewed within this interval, it is expired and ownership of the partition moves to another ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="44851-341">FeedPollDelay</span><span class="sxs-lookup"><span data-stu-id="44851-341">FeedPollDelay</span></span></td>
        <td><span data-ttu-id="44851-342">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="44851-342">TimeSpan</span></span></td>
        <td><span data-ttu-id="44851-343">Akış, geçerli sonra tüm değişiklikler yeni değişiklikleri boşaltmış için bir bölüm yoklama arasındaki gecikme.</span><span class="sxs-lookup"><span data-stu-id="44851-343">The delay between polling a partition for new changes on the feed, after all current changes are drained.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="44851-344">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="44851-344">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="44851-345">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="44851-345">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="44851-346">Denetim noktası kiraları için sıklığı.</span><span class="sxs-lookup"><span data-stu-id="44851-346">The frequency to checkpoint leases.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="44851-347">MinPartitionCount</span><span class="sxs-lookup"><span data-stu-id="44851-347">MinPartitionCount</span></span></td>
        <td><span data-ttu-id="44851-348">Int</span><span class="sxs-lookup"><span data-stu-id="44851-348">Int</span></span></td>
        <td><span data-ttu-id="44851-349">Ana bilgisayar için en düşük bölüm sayısı.</span><span class="sxs-lookup"><span data-stu-id="44851-349">The minimum partition count for the host.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="44851-350">MaxPartitionCount</span><span class="sxs-lookup"><span data-stu-id="44851-350">MaxPartitionCount</span></span></td>
        <td><span data-ttu-id="44851-351">Int</span><span class="sxs-lookup"><span data-stu-id="44851-351">Int</span></span></td>
        <td><span data-ttu-id="44851-352">Ana bilgisayar hizmet verebilir bölüm maksimum sayısı.</span><span class="sxs-lookup"><span data-stu-id="44851-352">The maximum number of partitions the host can serve.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="44851-353">DiscardExistingLeases</span><span class="sxs-lookup"><span data-stu-id="44851-353">DiscardExistingLeases</span></span></td>
        <td><span data-ttu-id="44851-354">bool</span><span class="sxs-lookup"><span data-stu-id="44851-354">Bool</span></span></td>
        <td><span data-ttu-id="44851-355">Olup tüm mevcut kiraları konak başlangıcını silinmesi gerekir ve konak baştan başlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="44851-355">Whether on the start of the host all existing leases should be deleted and the host should start from scratch.</span></span></td>
    </tr>
</table>


<span data-ttu-id="44851-356">Olay işlemeyi başlatmak için örneği `ChangeFeedProcessorHost`, Azure Cosmos DB koleksiyonunuz için uygun parametreleri sağlayarak.</span><span class="sxs-lookup"><span data-stu-id="44851-356">To start event processing, instantiate `ChangeFeedProcessorHost`, providing the appropriate parameters for your Azure Cosmos DB collection.</span></span> <span data-ttu-id="44851-357">Ardından, çağıran `RegisterObserverAsync` kaydetmek için `IChangeFeedObserver` (Bu örnekte DocumentFeedObserver) uygulama çalışma zamanı ile.</span><span class="sxs-lookup"><span data-stu-id="44851-357">Then, call `RegisterObserverAsync` to register your `IChangeFeedObserver` (DocumentFeedObserver in this example) implementation with the runtime.</span></span> <span data-ttu-id="44851-358">Bu noktada, ana bilgisayar "Hızlı" algoritma kullanarak Azure Cosmos DB koleksiyondaki her bölüm anahtarı aralığının üzerinde bir kira almaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="44851-358">At this point, the host attempts to acquire a lease on every partition key range in the Azure Cosmos DB collection using a "greedy" algorithm.</span></span> <span data-ttu-id="44851-359">Bu kiralar belirli bir zaman çerçevesi için en son ve sonrasında yenilenmelidir.</span><span class="sxs-lookup"><span data-stu-id="44851-359">These leases last for a given timeframe and must then be renewed.</span></span> <span data-ttu-id="44851-360">Yeni düğüm olarak çalışan örnekleri, bu durumda, çevrimiçi olması, kiralama ayırmaları yapar ve her bir ana bilgisayar daha fazla kira elde etmeye çalışır olarak zaman içinde yük düğümler arasında kayar..</span><span class="sxs-lookup"><span data-stu-id="44851-360">As new nodes, worker instances, in this case, come online, they place lease reservations and over time the load shifts between nodes as each host attempts to acquire more leases.</span></span> 

<span data-ttu-id="44851-361">Örnek kodda bir fabrika sınıfı (DocumentFeedObserverFactory.cs) bir gözlemci oluşturmak için kullanırız ve `RegistObserverFactoryAsync` gözlemci kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="44851-361">In the sample code, we use a factory class (DocumentFeedObserverFactory.cs) to create an observer and the `RegistObserverFactoryAsync` to register the observer.</span></span> 

```csharp
using (DocumentClient destClient = new DocumentClient(destCollInfo.Uri, destCollInfo.MasterKey))
    {
        DocumentFeedObserverFactory docObserverFactory = new DocumentFeedObserverFactory(destClient, destCollInfo);
        ChangeFeedEventHost host = new ChangeFeedEventHost(hostName, documentCollectionLocation, leaseCollectionLocation, feedOptions, feedHostOptions);

        await host.RegisterObserverFactoryAsync(docObserverFactory);

        Console.WriteLine("Running... Press enter to stop.");
        Console.ReadLine();

        await host.UnregisterObserversAsync();
    }
```
<span data-ttu-id="44851-362">Zaman içerisinde bir denge sağlanır.</span><span class="sxs-lookup"><span data-stu-id="44851-362">Over time, an equilibrium is established.</span></span> <span data-ttu-id="44851-363">Bu dinamik özellik CPU tabanlı ölçek büyütme ve ölçek azaltma için tüketicilere uygulanması için otomatik ölçeklendirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="44851-363">This dynamic capability enables CPU-based auto-scaling to be applied to consumers for both scale-up and scale-down.</span></span> <span data-ttu-id="44851-364">Değişiklikler Azure Cosmos DB'de tüketicilerin işleyebileceğinden daha hızlı bir oranda kullanılabilir, tüketiciler üzerindeki CPU artışı çalışan örnek sayısı üzerinde otomatik ölçeklendirmeye neden için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="44851-364">If changes are available in Azure Cosmos DB at a faster rate than consumers can process, the CPU increase on consumers can be used to cause an auto-scale on worker instance count.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44851-365">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="44851-365">Next steps</span></span>
* <span data-ttu-id="44851-366">Deneyin [Github'da Azure Cosmos DB Değiştir Akış kod örnekleri](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span><span class="sxs-lookup"><span data-stu-id="44851-366">Try the [Azure Cosmos DB Change feed code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span></span>
* <span data-ttu-id="44851-367">Kodlama ile çalışmaya başlama [Azure Cosmos DB SDK'ları](documentdb-sdk-dotnet.md) veya [REST API](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="44851-367">Get started coding with the [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md) or the [REST API](/rest/api/documentdb/).</span></span>
