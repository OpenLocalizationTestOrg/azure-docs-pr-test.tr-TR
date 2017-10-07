---
title: "Merhaba değişiklikle aaaWorking akışı destek Azure Cosmos DB'de | Microsoft Docs"
description: "Kullanım Azure Cosmos DB akış destek tootrack değişiklik belgelerde ve tetikleyiciler gibi olay tabanlı işleme ve önbellekleri ve analizi sistemleri güncel tutma gerçekleştirin."
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
ms.openlocfilehash: a4dcf4ceb476e3e08266dbcdcbee1d75e1d1eed4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-hello-change-feed-support-in-azure-cosmos-db"></a><span data-ttu-id="92046-104">Merhaba değişiklik akış desteği Azure Cosmos DB ile çalışma</span><span class="sxs-lookup"><span data-stu-id="92046-104">Working with hello change feed support in Azure Cosmos DB</span></span>
<span data-ttu-id="92046-105">[Azure Cosmos DB](../cosmos-db/introduction.md) bir hızlı ve esnek genel olarak, yazma ve okuma için tahmin edilebilir tek basamaklı milisaniyelik gecikme süresine sahip yüksek hacimli işlem ve işletimsel verileri depolamak için kullanılan veritabanı hizmeti çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="92046-105">[Azure Cosmos DB](../cosmos-db/introduction.md) is a fast and flexible globally replicated database service that is used for storing high-volume transactional and operational data with predictable single-digit millisecond latency for reads and writes.</span></span> <span data-ttu-id="92046-106">Bu, oldukça uygun perakende, oyun, IOT ve işlem günlüğü uygulamaları için kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="92046-106">This makes it well-suited for IoT, gaming, retail, and operational logging applications.</span></span> <span data-ttu-id="92046-107">Bu uygulamalar ortak tasarım modelinde tootrack değişiklikleri tooAzure Cosmos DB verilerde yapılan ve gerçekleştirilmiş görünümlere güncelleştirme, bu değişikliklere dayalı belirli olaylar üzerinde gerçek zamanlı analytics, arşiv verileri toocold depolama ve bildirimlerini tetiklemesini gerçekleştirmek olur.</span><span class="sxs-lookup"><span data-stu-id="92046-107">A common design pattern in these applications is tootrack changes made tooAzure Cosmos DB data, and update materialized views, perform real-time analytics, archive data toocold storage, and trigger notifications on certain events based on these changes.</span></span> <span data-ttu-id="92046-108">Merhaba **değişiklik akışı Destek** Azure Cosmos DB'de toobuild verimli ve ölçeklenebilir çözümler her bu düzenleri için sağlar.</span><span class="sxs-lookup"><span data-stu-id="92046-108">hello **change feed support** in Azure Cosmos DB enables you toobuild efficient and scalable solutions for each of these patterns.</span></span>

<span data-ttu-id="92046-109">Destek akış değişiklikle Azure Cosmos DB hello sırada değiştirilmiş bir Azure Cosmos DB koleksiyonundaki belgelerin sıralanmış bir listesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="92046-109">With change feed support, Azure Cosmos DB provides a sorted list of documents within an Azure Cosmos DB collection in hello order in which they were modified.</span></span> <span data-ttu-id="92046-110">Bu akışın gibi eylemleri gerçekleştirmek ve değişiklikleri toodata hello koleksiyonundaki için kullanılan toolisten olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="92046-110">This feed can be used toolisten for modifications toodata within hello collection and perform actions such as:</span></span>

* <span data-ttu-id="92046-111">Bir belge eklendiğinde veya çağrı tooan API Tetikle</span><span class="sxs-lookup"><span data-stu-id="92046-111">Trigger a call tooan API when a document is inserted or modified</span></span>
* <span data-ttu-id="92046-112">Gerçek zamanlı (akış) yönlendirilmeden güncelleştirmeleri</span><span class="sxs-lookup"><span data-stu-id="92046-112">Perform real-time (stream) processing on updates</span></span>
* <span data-ttu-id="92046-113">Önbellek, arama motoru veya veri ambarı veri eşitleme</span><span class="sxs-lookup"><span data-stu-id="92046-113">Synchronize data with a cache, search engine, or data warehouse</span></span>

<span data-ttu-id="92046-114">Azure Cosmos DB değişiklikler kalıcı zaman uyumsuz olarak işlenir ve Paralel işleme için bir veya daha fazla tüketiciye dağıtılmış.</span><span class="sxs-lookup"><span data-stu-id="92046-114">Changes in Azure Cosmos DB are persisted and can be processed asynchronously, and distributed across one or more consumers for parallel processing.</span></span> <span data-ttu-id="92046-115">Merhaba API'leri değişiklik akış ve nasıl toobuild ölçeklenebilir gerçek zamanlı uygulamaları kullanabilmeniz için bakalım.</span><span class="sxs-lookup"><span data-stu-id="92046-115">Let's look at hello APIs for change feed and how you can use them toobuild scalable real-time applications.</span></span> <span data-ttu-id="92046-116">Bu makalede, Azure Cosmos DB ile toowork nasıl değiştiğini akış ve hello DocumentDB API gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="92046-116">This article shows how toowork with Azure Cosmos DB change feed and hello DocumentDB API.</span></span> 

![Akış toopower gerçek zamanlı analiz ve bilgi işlem senaryolarına olay denetimli Azure Cosmos DB Değiştir kullanma](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> <span data-ttu-id="92046-118">Destek akış değişiklik, yalnızca şu anda DocumentDB API hello için sağlanır; Merhaba grafik API'si ve tablo API şu anda desteklenmemektedir.</span><span class="sxs-lookup"><span data-stu-id="92046-118">Change feed support is only provided for hello DocumentDB API at this time; hello Graph API and Table API are not currently supported.</span></span>

## <a name="use-cases-and-scenarios"></a><span data-ttu-id="92046-119">Kullanım örnekleri ve senaryoları</span><span class="sxs-lookup"><span data-stu-id="92046-119">Use cases and scenarios</span></span>
<span data-ttu-id="92046-120">Değişiklik akış yüksek hacimli yazma ile büyük veri verimli işlemeye olanak sağlar ve bir alternatif tooquerying tüm veri kümeleri tooidentify nelerin değiştiğini sunar.</span><span class="sxs-lookup"><span data-stu-id="92046-120">Change feed allows for efficient processing of large datasets with a high volume of writes, and offers an alternative tooquerying entire datasets tooidentify what has changed.</span></span> <span data-ttu-id="92046-121">Örneğin, görevleri verimli bir şekilde aşağıdaki hello gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="92046-121">For example, you can perform hello following tasks efficiently:</span></span>

* <span data-ttu-id="92046-122">Bir önbellek, arama dizini ya da bir veri ambarı Azure Cosmos DB içinde depolanan veriler ile güncelleştirecek.</span><span class="sxs-lookup"><span data-stu-id="92046-122">Update a cache, search index, or a data warehouse with data stored in Azure Cosmos DB.</span></span>
* <span data-ttu-id="92046-123">Uygulama düzeyi verileri katmanlama ve arşivleme uygulamak, diğer bir deyişle, Azure Cosmos DB'de "etkin verileri" depolamak ve "soğuk veri çıkış" çok geçerlilik süresi[Azure Blob Storage](../storage/common/storage-introduction.md) veya [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="92046-123">Implement application-level data tiering and archival, that is, store "hot data" in Azure Cosmos DB, and age out "cold data" too[Azure Blob Storage](../storage/common/storage-introduction.md) or [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span></span>
* <span data-ttu-id="92046-124">Verileri kullanarak toplu analizi uygulamak [Apache Hadoop](run-hadoop-with-hdinsight.md).</span><span class="sxs-lookup"><span data-stu-id="92046-124">Implement batch analytics on data using [Apache Hadoop](run-hadoop-with-hdinsight.md).</span></span>
* <span data-ttu-id="92046-125">Uygulama [lambda işlem hatları Azure üzerinde](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) Azure Cosmos DB ile.</span><span class="sxs-lookup"><span data-stu-id="92046-125">Implement [lambda pipelines on Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) with Azure Cosmos DB.</span></span> <span data-ttu-id="92046-126">Azure Cosmos DB alımı ve sorgu işleyen ve düşük ile lambda mimariyi uygulayan ölçeklenebilir veritabanı çözümü sağlar.</span><span class="sxs-lookup"><span data-stu-id="92046-126">Azure Cosmos DB provides a scalable database solution that can handle both ingestion and query, and implement lambda architectures with low TCO.</span></span> 
* <span data-ttu-id="92046-127">Sıfır kapalı kalma süresi geçişler tooanother farklı bir bölümleme düzeni Azure Cosmos DB hesabıyla gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="92046-127">Perform zero down-time migrations tooanother Azure Cosmos DB account with a different partitioning scheme.</span></span>

<span data-ttu-id="92046-128">**Azure Cosmos DB alımı ve sorgu için sahip lambda ardışık düzenler:**</span><span class="sxs-lookup"><span data-stu-id="92046-128">**Lambda Pipelines with Azure Cosmos DB for ingestion and query:**</span></span>

![Azure Cosmos DB lambda ardışık düzeni alımı ve sorgu için temel](./media/change-feed/lambda.png)

<span data-ttu-id="92046-130">Azure Cosmos DB tooreceive kullanın ve cihazlar, algılayıcılar, altyapı ve uygulamaları olay verileri depolamak ve bu olayları işlem ile gerçek zamanlı [Azure akış analizi](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), veya [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="92046-130">You can use Azure Cosmos DB tooreceive and store event data from devices, sensors, infrastructure, and applications, and process these events in real-time with [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/hdinsight-storm-overview.md), or [Apache Spark](../hdinsight/hdinsight-apache-spark-overview.md).</span></span> 

<span data-ttu-id="92046-131">İçinde [sunucusuz](http://azure.com/serverless) web ve mobil uygulamaları, anında iletme bildirimleri tootheir aygıtlarını kullanarakgöndermegibibelirlieylemlerideğişiklikleritooyourMüşteri'ninprofili,tercihlerineveyakonumutootriggergibiizlemeolaylarıiçin[Azure işlevleri](../azure-functions/functions-bindings-documentdb.md) veya [uygulama hizmetleri](https://azure.microsoft.com/services/app-service/).</span><span class="sxs-lookup"><span data-stu-id="92046-131">Within your [serverless](http://azure.com/serverless) web and mobile apps, you can track events such as changes tooyour customer's profile, preferences, or location tootrigger certain actions like sending push notifications tootheir devices using [Azure Functions](../azure-functions/functions-bindings-documentdb.md) or [App Services](https://azure.microsoft.com/services/app-service/).</span></span> <span data-ttu-id="92046-132">Örneğin, Azure Cosmos DB toobuild oyun kullanıyorsanız, değişiklik akış tooimplement gerçek zamanlı liderlik tamamlanmış oyunlar gelen puanları temel kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="92046-132">If you're using Azure Cosmos DB toobuild a game, you can, for example, use change feed tooimplement real-time leaderboards based on scores from completed games.</span></span>

## <a name="how-change-feed-works-in-azure-cosmos-db"></a><span data-ttu-id="92046-133">Değişiklik akış Azure Cosmos DB'de nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="92046-133">How change feed works in Azure Cosmos DB</span></span>
<span data-ttu-id="92046-134">Azure Cosmos DB hello özelliği tooincrementally yapılan güncelleştirmeler tooan Azure Cosmos DB koleksiyonu okuma sağlar.</span><span class="sxs-lookup"><span data-stu-id="92046-134">Azure Cosmos DB provides hello ability tooincrementally read updates made tooan Azure Cosmos DB collection.</span></span> <span data-ttu-id="92046-135">Bu değişiklik akışın hello aşağıdaki özelliklere sahiptir:</span><span class="sxs-lookup"><span data-stu-id="92046-135">This change feed has hello following properties:</span></span>

* <span data-ttu-id="92046-136">Değişiklikler Azure Cosmos DB'de kalıcı ve zaman uyumsuz olarak işlenir.</span><span class="sxs-lookup"><span data-stu-id="92046-136">Changes are persistent in Azure Cosmos DB and can be processed asynchronously.</span></span>
* <span data-ttu-id="92046-137">Bir koleksiyon içinde değişiklikleri toodocuments hemen hello değişiklik akışta kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="92046-137">Changes toodocuments within a collection are available immediately in hello change feed.</span></span>
* <span data-ttu-id="92046-138">Her değişiklik tooa belge hello değişiklik akışta tam olarak bir kez görünür ve kendi denetim noktası oluşturma mantığı istemcilerini yönetme.</span><span class="sxs-lookup"><span data-stu-id="92046-138">Each change tooa document appears exactly once in hello change feed, and clients manage their checkpointing logic.</span></span> <span data-ttu-id="92046-139">Merhaba değişiklik akış işlemci kitaplığı otomatik denetim noktası oluşturma ve "en az bir kez" semantiği sağlar.</span><span class="sxs-lookup"><span data-stu-id="92046-139">hello change feed processor library provides automatic checkpointing and "at least once" semantics.</span></span>
* <span data-ttu-id="92046-140">Belirli bir belge için yalnızca hello en son değişiklik hello değişiklik günlüğünde yer alır.</span><span class="sxs-lookup"><span data-stu-id="92046-140">Only hello most recent change for a given document is included in hello change log.</span></span> <span data-ttu-id="92046-141">Ara değişikliklerin kullanılamayabilir.</span><span class="sxs-lookup"><span data-stu-id="92046-141">Intermediate changes may not be available.</span></span>
* <span data-ttu-id="92046-142">Merhaba değişiklik akışı, her bölüm anahtarı değerini içinde değişiklik sırasına göre sıralanır.</span><span class="sxs-lookup"><span data-stu-id="92046-142">hello change feed is sorted by order of modification within each partition key value.</span></span> <span data-ttu-id="92046-143">Bölüm anahtarı değerleri arasında hiçbir garanti edilen sipariş yoktur.</span><span class="sxs-lookup"><span data-stu-id="92046-143">There is no guaranteed order across partition-key values.</span></span>
* <span data-ttu-id="92046-144">Değişiklikleri herhangi noktası zaman eşitlenebilir, diğer bir deyişle, değişiklikler kullanılabilir hiçbir sabit veri saklama süresi vardır.</span><span class="sxs-lookup"><span data-stu-id="92046-144">Changes can be synchronized from any point-in-time, that is, there is no fixed data retention period for which changes are available.</span></span>
* <span data-ttu-id="92046-145">Değişiklikler bölüm anahtar aralıklarına yığınlar halinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="92046-145">Changes are available in chunks of partition key ranges.</span></span> <span data-ttu-id="92046-146">Bu özellik paralel olarak birden çok tüketiciye/sunucuları tarafından işlenen büyük topluluklara toobe değişikliklerden sağlar.</span><span class="sxs-lookup"><span data-stu-id="92046-146">This capability allows changes from large collections toobe processed in parallel by multiple consumers/servers.</span></span>
* <span data-ttu-id="92046-147">Uygulamaları birden çok değişikliği aynı anda hello üzerinde aynı akışları için isteyebileceği koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="92046-147">Applications can request for multiple change feeds simultaneously on hello same collection.</span></span>

<span data-ttu-id="92046-148">Azure Cosmos veritabanı değişikliği akış tüm hesapları için varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="92046-148">Azure Cosmos DB's change feed is enabled by default for all accounts.</span></span> <span data-ttu-id="92046-149">Kullanabilirsiniz, [sağlanan işleme](request-units.md) yazma bölgenize veya herhangi [bölge okuma](distribute-data-globally.md) hello gelen tooread akışı, başka bir işlem Azure Cosmos DB'den gibi değiştirin.</span><span class="sxs-lookup"><span data-stu-id="92046-149">You can use your [provisioned throughput](request-units.md) in your write region or any [read region](distribute-data-globally.md) tooread from hello change feed, just like any other operation from Azure Cosmos DB.</span></span> <span data-ttu-id="92046-150">Merhaba değişiklik akış ekler ve toodocuments hello koleksiyonundaki yapılan güncelleştirme işlemlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="92046-150">hello change feed includes inserts and update operations made toodocuments within hello collection.</span></span> <span data-ttu-id="92046-151">Siler yakalayabilirsiniz belgelerinizi siler yerine içinde "soft-Sil" bayrağını ayarlayarak.</span><span class="sxs-lookup"><span data-stu-id="92046-151">You can capture deletes by setting a "soft-delete" flag within your documents in place of deletes.</span></span> <span data-ttu-id="92046-152">Alternatif olarak, sınırlı bir süre hello aracılığıyla belgeleriniz için ayarlayabileceğiniz [TTL yetenek](time-to-live.md), örneğin, 24 saat ve kullanım değeri hello için bu özelliği toocapture siler.</span><span class="sxs-lookup"><span data-stu-id="92046-152">Alternatively, you can set a finite expiration period for your documents via hello [TTL capability](time-to-live.md), for example, 24 hours and use hello value of that property toocapture deletes.</span></span> <span data-ttu-id="92046-153">Bu çözüm ile Merhaba TTL sona erme süresinden daha kısa bir zaman aralığındaki tooprocess değişiklikleri sahip.</span><span class="sxs-lookup"><span data-stu-id="92046-153">With this solution, you have tooprocess changes within a shorter time interval than hello TTL expiration period.</span></span> <span data-ttu-id="92046-154">Hello değişiklik akışı her bölüm anahtarı aralığının hello belge koleksiyonundaki için kullanılabilir ve bu nedenle bir veya daha fazla tüketiciye paralel işleme üzerinden dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="92046-154">hello change feed is available for each partition key range within hello document collection, and thus can be distributed across one or more consumers for parallel processing.</span></span> 

![Azure Cosmos DB değişimin dağıtılmış işlem akışı](./media/change-feed/changefeedvisual.png)

<span data-ttu-id="92046-156">İstemci kodunuzda akışı bir değişiklik nasıl uygulayacağınıza, birkaç seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="92046-156">You have a few options in how you implement a change feed in your client code.</span></span> <span data-ttu-id="92046-157">İzleme açıklamak hemen nasıl tooimplement hello Azure Cosmos DB REST API'sini kullanarak değişiklik akış hello ve DocumentDB SDK'ları hello Merhaba, bölümler.</span><span class="sxs-lookup"><span data-stu-id="92046-157">hello sections that immediately follow describe how tooimplement hello change feed using hello Azure Cosmos DB REST API and hello DocumentDB SDKs.</span></span> <span data-ttu-id="92046-158">Ancak, .NET uygulamaları için hello yeni kullanmanızı öneririz [değişiklik akış işlemci Kitaplığı](#change-feed-processor) okuma değişiklikleri bölümler basitleştirir ve birden çok iş parçacığı üzerinde çalışırken etkinleştirir hello işleme olaylarından akış değiştirin Paralel.</span><span class="sxs-lookup"><span data-stu-id="92046-158">However, for .NET applications, we recommend using hello new [Change feed processor library](#change-feed-processor) for processing events from hello change feed as it simplifies reading changes across partitions and enables multiple threads working in parallel.</span></span> 

## <span data-ttu-id="92046-159"><a id="rest-apis"></a>REST API ve DocumentDB SDK'ları Hello ile çalışma</span><span class="sxs-lookup"><span data-stu-id="92046-159"><a id="rest-apis"></a>Working with hello REST API and DocumentDB SDKs</span></span>
<span data-ttu-id="92046-160">Azure Cosmos DB sağlar, depolama ve işleme adlı esnek kapsayıcıları **koleksiyonları**.</span><span class="sxs-lookup"><span data-stu-id="92046-160">Azure Cosmos DB provides elastic containers of storage and throughput called **collections**.</span></span> <span data-ttu-id="92046-161">Veri koleksiyonları içinde mantıksal olarak gruplandırılmış kullanarak [bölüm anahtarlarını](partition-data.md) ölçeklenebilirlik ve performans.</span><span class="sxs-lookup"><span data-stu-id="92046-161">Data within collections is logically grouped using [partition keys](partition-data.md) for scalability and performance.</span></span> <span data-ttu-id="92046-162">Azure Cosmos DB arama kimliği (okuma/Get), sorgu ve okuma beslemelerini (taramalar) dahil olmak üzere bu verilerine erişmek için çeşitli API'ler sağlar.</span><span class="sxs-lookup"><span data-stu-id="92046-162">Azure Cosmos DB provides various APIs for accessing this data, including lookup by ID (Read/Get), query, and read-feeds (scans).</span></span> <span data-ttu-id="92046-163">Merhaba değişiklik akışı iki yeni istek üstbilgileri toohello DocumentDB doldurarak elde edilebilir `ReadDocumentFeed` API'sini ve bölüm anahtarlarını aralıklar paralel olarak işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="92046-163">hello change feed can be obtained by populating two new request headers toohello DocumentDB `ReadDocumentFeed` API, and can be processed in parallel across ranges of partition keys.</span></span>

### <a name="readdocumentfeed-api"></a><span data-ttu-id="92046-164">ReadDocumentFeed API</span><span class="sxs-lookup"><span data-stu-id="92046-164">ReadDocumentFeed API</span></span>
<span data-ttu-id="92046-165">ReadDocumentFeed nasıl çalıştığı bir kısa bakalım.</span><span class="sxs-lookup"><span data-stu-id="92046-165">Let's take a brief look at how ReadDocumentFeed works.</span></span> <span data-ttu-id="92046-166">Azure Cosmos DB destekleyen bir akış hello aracılığıyla bir koleksiyon içinde belgelerin okuma `ReadDocumentFeed` API.</span><span class="sxs-lookup"><span data-stu-id="92046-166">Azure Cosmos DB supports reading a feed of documents within a collection via hello `ReadDocumentFeed` API.</span></span> <span data-ttu-id="92046-167">Örneğin, hello aşağıdaki isteği belgeleri hello içinde bir sayfa döndürür `serverlogs` koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="92046-167">For example, hello following request returns a page of documents inside hello `serverlogs` collection.</span></span> 

    GET https://mydocumentdb.documents.azure.com/dbs/smalldb/colls/serverlogs HTTP/1.1
    x-ms-date: Tue, 22 Nov 2016 17:05:14 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dgo7JEogZDn6ritWhwc5hX%2fNTV4wwM1u9V2Is1H4%2bDRg%3d
    Cache-Control: no-cache
    x-ms-consistency-level: Strong
    User-Agent: Microsoft.Azure.Documents.Client/1.10.27.5
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: mydocumentdb.documents.azure.com

<span data-ttu-id="92046-168">Sonuçları hello kullanarak bunlarla sınırlı `x-ms-max-item-count` üstbilgi ve okuma sürdürüldü hello isteğini yeniden göndermeden bir `x-ms-continuation` üstbilgi hello önceki yanıtta döndürülen.</span><span class="sxs-lookup"><span data-stu-id="92046-168">Results can be limited by using hello `x-ms-max-item-count` header, and reads can be resumed by resubmitting hello request with a `x-ms-continuation` header returned in hello previous response.</span></span> <span data-ttu-id="92046-169">Tek bir istemciden gerçekleştirildiğinde `ReadDocumentFeed` seri olarak bölümler sonuçları arasında yineler.</span><span class="sxs-lookup"><span data-stu-id="92046-169">When performed from a single client, `ReadDocumentFeed` iterates through results across partitions serially.</span></span> 

<span data-ttu-id="92046-170">**Seri belge akışı okuma**</span><span class="sxs-lookup"><span data-stu-id="92046-170">**Serial read document feed**</span></span>

<span data-ttu-id="92046-171">Desteklenen hello birini kullanarak belgelerin hello akışı da alabilir [Azure Cosmos DB SDK'ları](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="92046-171">You can also retrieve hello feed of documents using one of hello supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="92046-172">Örneğin, kod parçacığında gösterildiği nasıl aşağıdaki hello toouse hello [ReadDocumentFeedAsync yöntemi](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) .NET içinde.</span><span class="sxs-lookup"><span data-stu-id="92046-172">For example, hello following snippet shows how toouse hello [ReadDocumentFeedAsync method](/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentfeedasync?view=azure-dotnet) in .NET.</span></span>

```csharp
FeedResponse<dynamic> feedResponse = null;
do
{
    feedResponse = await client.ReadDocumentFeedAsync(collection, new FeedOptions { MaxItemCount = -1 });
}
while (feedResponse.ResponseContinuation != null);
```

### <a name="distributed-execution-of-readdocumentfeed"></a><span data-ttu-id="92046-173">ReadDocumentFeed dağıtılmış yürütülmesi</span><span class="sxs-lookup"><span data-stu-id="92046-173">Distributed execution of ReadDocumentFeed</span></span>
<span data-ttu-id="92046-174">Veri ya da daha fazla terabayt içeren veya büyük miktarda güncelleştirme alma koleksiyonlar için tek istemci makineye okuma akıştan seri yürütülmesi pratik olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="92046-174">For collections that contain terabytes of data or more, or ingest a large volume of updates, serial execution of read feed from a single client machine might not be practical.</span></span> <span data-ttu-id="92046-175">Sipariş toosupport Azure Cosmos DB bu büyük veri senaryolarını sağlar API'leri toodistribute `ReadDocumentFeed` çağrıları saydam birden çok istemci okuyucular/tüketicileri arasında.</span><span class="sxs-lookup"><span data-stu-id="92046-175">In order toosupport these big data scenarios, Azure Cosmos DB provides APIs toodistribute `ReadDocumentFeed` calls transparently across multiple client readers/consumers.</span></span> 

<span data-ttu-id="92046-176">**Dağıtılmış okuma belge besleme**</span><span class="sxs-lookup"><span data-stu-id="92046-176">**Distributed Read Document Feed**</span></span>

<span data-ttu-id="92046-177">bölüm anahtarlarını aralıklarını temel alarak API Hello değişiklik akış için artımlı değişiklikler, Azure Cosmos DB ölçeklenebilir işlenmesini tooprovide genişleme modelini destekler.</span><span class="sxs-lookup"><span data-stu-id="92046-177">tooprovide scalable processing of incremental changes, Azure Cosmos DB supports a scale-out model for hello change feed API based on ranges of partition keys.</span></span>

* <span data-ttu-id="92046-178">Bir koleksiyon gerçekleştirmek için anahtar aralıklarına bölüm listesini elde edebilirsiniz bir `ReadPartitionKeyRanges` çağırın.</span><span class="sxs-lookup"><span data-stu-id="92046-178">You can obtain a list of partition key ranges for a collection performing a `ReadPartitionKeyRanges` call.</span></span> 
* <span data-ttu-id="92046-179">Her bölüm anahtarı aralığının gerçekleştirdiğiniz bir `ReadDocumentFeed` bu aralıkta bölüm anahtarlarını tooread belgeler.</span><span class="sxs-lookup"><span data-stu-id="92046-179">For each partition key range, you can perform a `ReadDocumentFeed` tooread documents with partition keys within that range.</span></span>

### <a name="retrieving-partition-key-ranges-for-a-collection"></a><span data-ttu-id="92046-180">Bir koleksiyon için bölüm anahtarı aralıkları alma</span><span class="sxs-lookup"><span data-stu-id="92046-180">Retrieving partition key ranges for a collection</span></span>
<span data-ttu-id="92046-181">Hello bölüm anahtar aralıklarına göre isteyen hello alabilir `pkranges` bir koleksiyon içindeki kaynak.</span><span class="sxs-lookup"><span data-stu-id="92046-181">You can retrieve hello partition key ranges by requesting hello `pkranges` resource within a collection.</span></span> <span data-ttu-id="92046-182">Örneğin hello aşağıdaki isteği hello listesini hello için bölüm anahtarı aralıkları alır `serverlogs` koleksiyonu:</span><span class="sxs-lookup"><span data-stu-id="92046-182">For example hello following request retrieves hello list of partition key ranges for hello `serverlogs` collection:</span></span>

    GET https://querydemo.documents.azure.com/dbs/bigdb/colls/serverlogs/pkranges HTTP/1.1
    x-ms-date: Tue, 15 Nov 2016 07:26:51 GMT
    authorization: type%3dmaster%26ver%3d1.0%26sig%3dEConYmRgDExu6q%2bZ8GjfUGOH0AcOx%2behkancw3LsGQ8%3d
    x-ms-consistency-level: Session
    x-ms-version: 2016-07-11
    Accept: application/json
    Host: querydemo.documents.azure.com

<span data-ttu-id="92046-183">Bu istek hello bölüm anahtar aralıklarına hakkındaki meta verileri içeren bir yanıtı aşağıdaki hello döndürür:</span><span class="sxs-lookup"><span data-stu-id="92046-183">This request returns hello following response containing metadata about hello partition key ranges:</span></span>

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


<span data-ttu-id="92046-184">**Bölüm anahtarı aralığının özellikleri**: her bölüm anahtarı aralığının aşağıdaki tablonun hello hello meta veri özelliklerini içerir:</span><span class="sxs-lookup"><span data-stu-id="92046-184">**Partition key range properties**: Each partition key range includes hello metadata properties in hello following table:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="92046-185">Üstbilgi adı</span><span class="sxs-lookup"><span data-stu-id="92046-185">Header name</span></span></th>
        <th><span data-ttu-id="92046-186">Açıklama</span><span class="sxs-lookup"><span data-stu-id="92046-186">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="92046-187">id</span><span class="sxs-lookup"><span data-stu-id="92046-187">id</span></span></td>
        <td>
            <p><span data-ttu-id="92046-188">Merhaba bölüm anahtarı aralığının Hello kimliği.</span><span class="sxs-lookup"><span data-stu-id="92046-188">hello ID for hello partition key range.</span></span> <span data-ttu-id="92046-189">Her bir koleksiyonun içindeki kararlı ve benzersiz bir kimliği budur.</span><span class="sxs-lookup"><span data-stu-id="92046-189">This is a stable and unique ID within each collection.</span></span></p>
            <p><span data-ttu-id="92046-190">Aşağıdaki çağrı tooread değişiklikler hello bölüm anahtarı aralığının tarafından kullanılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="92046-190">Must be used in hello following call tooread changes by partition key range.</span></span></p>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="92046-191">maxExclusive</span><span class="sxs-lookup"><span data-stu-id="92046-191">maxExclusive</span></span></td>
        <td><span data-ttu-id="92046-192">Merhaba bölüm anahtarı aralığının için Hello en fazla bölüm anahtarı karma değer.</span><span class="sxs-lookup"><span data-stu-id="92046-192">hello maximum partition key hash value for hello partition key range.</span></span> <span data-ttu-id="92046-193">İç kullanım için.</span><span class="sxs-lookup"><span data-stu-id="92046-193">For internal use.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="92046-194">minInclusive</span><span class="sxs-lookup"><span data-stu-id="92046-194">minInclusive</span></span></td>
        <td><span data-ttu-id="92046-195">Merhaba bölüm anahtarı aralığının için Hello en az bölüm anahtarı karma değer.</span><span class="sxs-lookup"><span data-stu-id="92046-195">hello minimum partition key hash value for hello partition key range.</span></span> <span data-ttu-id="92046-196">İç kullanım için.</span><span class="sxs-lookup"><span data-stu-id="92046-196">For internal use.</span></span></td>
    </tr>       
</table>

<span data-ttu-id="92046-197">Desteklenen hello birini kullanarak bunu yapabilirsiniz [Azure Cosmos DB SDK'ları](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="92046-197">You can do this using one of hello supported [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="92046-198">Örneğin, hello aşağıdaki kod parçacığında nasıl tooretrieve bölüm anahtarı .NET aralıkları hello kullanarak gösterir [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="92046-198">For example, hello following snippet shows how tooretrieve partition key ranges in .NET using hello [ReadPartitionKeyRangeFeedAsync](/dotnet/api/microsoft.azure.documents.client.documentclient.readpartitionkeyrangefeedasync?view=azure-dotnet) method.</span></span>

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

<span data-ttu-id="92046-199">Azure Cosmos DB ayarı hello tarafından isteğe bağlı bölüm anahtarı aralığının başına belge alınmasını destekler `x-ms-documentdb-partitionkeyrangeid` üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="92046-199">Azure Cosmos DB supports retrieval of documents per partition key range by setting hello optional `x-ms-documentdb-partitionkeyrangeid` header.</span></span> 

### <a name="performing-an-incremental-readdocumentfeed"></a><span data-ttu-id="92046-200">Bir artımlı ReadDocumentFeed gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="92046-200">Performing an incremental ReadDocumentFeed</span></span>
<span data-ttu-id="92046-201">ReadDocumentFeed senaryoları/görevler değişiklikleri Azure Cosmos DB koleksiyonlarda artımlı işleme için aşağıdaki hello destekler:</span><span class="sxs-lookup"><span data-stu-id="92046-201">ReadDocumentFeed supports hello following scenarios/tasks for incremental processing of changes in Azure Cosmos DB collections:</span></span>

* <span data-ttu-id="92046-202">Tüm okuma hello başından toodocuments diğer bir deyişle, koleksiyon oluşturulması değiştirir.</span><span class="sxs-lookup"><span data-stu-id="92046-202">Read all changes toodocuments from hello beginning, that is, from collection creation.</span></span>
* <span data-ttu-id="92046-203">Tüm okuma toofuture güncelleştirmeleri toodocuments kullanıcı tarafından belirtilen bir tarihten geçerli saati veya herhangi bir değişiklik değiştirir.</span><span class="sxs-lookup"><span data-stu-id="92046-203">Read all changes toofuture updates toodocuments from current time, or any changes since a user-specified time.</span></span>
* <span data-ttu-id="92046-204">Tüm değişiklikleri toodocuments hello koleksiyonu (ETag) mantıksal bir sürümünden okuyun.</span><span class="sxs-lookup"><span data-stu-id="92046-204">Read all changes toodocuments from a logical version of hello collection (ETag).</span></span> <span data-ttu-id="92046-205">Denetim noktası artımlı okuma akışı isteklerinden ETag döndürülen hello tüketicileriniz dayalı olabilir.</span><span class="sxs-lookup"><span data-stu-id="92046-205">You can checkpoint your consumers based on hello returned ETag from incremental read-feed requests.</span></span>

<span data-ttu-id="92046-206">Merhaba değişiklikler ekler ve güncelleştirmeleri toodocuments içerir.</span><span class="sxs-lookup"><span data-stu-id="92046-206">hello changes include inserts and updates toodocuments.</span></span> <span data-ttu-id="92046-207">toocapture siler, belgeler içinde "geçici silme" özelliğini kullanın veya hello kullan [yerleşik TTL özelliği](time-to-live.md) toosignal hello bekleyen bir değişikliği akış değiştirin.</span><span class="sxs-lookup"><span data-stu-id="92046-207">toocapture deletes, you must use a "soft delete" property within your documents, or use hello [built-in TTL property](time-to-live.md) toosignal a pending deletion in hello change feed.</span></span>

<span data-ttu-id="92046-208">Tablo listeleri hello Hello [isteği](/rest/api/documentdb/common-documentdb-rest-request-headers.md) ve [yanıt üstbilgilerini](/rest/api/documentdb/common-documentdb-rest-response-headers.md) ReadDocumentFeed işlemleri için.</span><span class="sxs-lookup"><span data-stu-id="92046-208">hello following table lists hello [request](/rest/api/documentdb/common-documentdb-rest-request-headers.md) and [response headers](/rest/api/documentdb/common-documentdb-rest-response-headers.md) for ReadDocumentFeed operations.</span></span>

<span data-ttu-id="92046-209">**İstek üstbilgileri için artımlı ReadDocumentFeed**:</span><span class="sxs-lookup"><span data-stu-id="92046-209">**Request headers for incremental ReadDocumentFeed**:</span></span>

<table>
    <tr>
        <th><span data-ttu-id="92046-210">Üstbilgi adı</span><span class="sxs-lookup"><span data-stu-id="92046-210">Header name</span></span></th>
        <th><span data-ttu-id="92046-211">Açıklama</span><span class="sxs-lookup"><span data-stu-id="92046-211">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="92046-212">BİR IM</span><span class="sxs-lookup"><span data-stu-id="92046-212">A-IM</span></span></td>
        <td><span data-ttu-id="92046-213">Çok "Artımlı akış" olarak ayarlanması gerekir ya da aksi takdirde atlanmış</span><span class="sxs-lookup"><span data-stu-id="92046-213">Must be set too"Incremental feed", or omitted otherwise</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="92046-214">If-None-Match</span><span class="sxs-lookup"><span data-stu-id="92046-214">If-None-Match</span></span></td>
        <td>
            <p><span data-ttu-id="92046-215">Başlık: (oluşturma koleksiyonu) itibaren hello tüm değişiklikleri döndürür</span><span class="sxs-lookup"><span data-stu-id="92046-215">No header: returns all changes from hello beginning (collection creation)</span></span></p>
            <p><span data-ttu-id="92046-216">"*": hello koleksiyonundaki tüm yeni değişiklikleri toodata döndürür</span><span class="sxs-lookup"><span data-stu-id="92046-216">"*": returns all new changes toodata within hello collection</span></span></p>         
            <p><span data-ttu-id="92046-217">&lt;ETag&gt;: varsa tooa koleksiyonu ETag, mantıksal zaman damgası itibaren yapılan tüm değişiklikler döndürür</span><span class="sxs-lookup"><span data-stu-id="92046-217">&lt;etag&gt;: If set tooa collection ETag, returns all changes made since that logical timestamp</span></span></p>
        </td>
    </tr>
    <tr>    
        <td><span data-ttu-id="92046-218">If-Modified-Since</span><span class="sxs-lookup"><span data-stu-id="92046-218">If-Modified-Since</span></span></td> 
        <td><span data-ttu-id="92046-219">RFC 1123 saat biçimi; If-None-Match belirtilmişse göz ardı</span><span class="sxs-lookup"><span data-stu-id="92046-219">RFC 1123 time format; ignored if If-None-Match is specified</span></span></td> 
    </tr> 
    <tr>
        <td><span data-ttu-id="92046-220">x-ms-documentdb-partitionkeyrangeid</span><span class="sxs-lookup"><span data-stu-id="92046-220">x-ms-documentdb-partitionkeyrangeid</span></span></td>
        <td><span data-ttu-id="92046-221">verilerin okunması için hello bölüm anahtarı aralığının kimliği.</span><span class="sxs-lookup"><span data-stu-id="92046-221">hello partition key range ID for reading data.</span></span></td>
    </tr>
</table>

<span data-ttu-id="92046-222">**Yanıt üstbilgileri için artımlı ReadDocumentFeed**:</span><span class="sxs-lookup"><span data-stu-id="92046-222">**Response headers for incremental ReadDocumentFeed**:</span></span>

<table> <tr>
        <th><span data-ttu-id="92046-223">Üstbilgi adı</span><span class="sxs-lookup"><span data-stu-id="92046-223">Header name</span></span></th>
        <th><span data-ttu-id="92046-224">Açıklama</span><span class="sxs-lookup"><span data-stu-id="92046-224">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="92046-225">ETag</span><span class="sxs-lookup"><span data-stu-id="92046-225">etag</span></span></td>
        <td>
            <p><span data-ttu-id="92046-226">Merhaba yanıtında son belgenin Hello mantıksal sıra numarası (LSN).</span><span class="sxs-lookup"><span data-stu-id="92046-226">hello logical sequence number (LSN) of last document returned in hello response.</span></span></p>
            <p><span data-ttu-id="92046-227">Artımlı ReadDocumentFeed If-None-Match bu değeri yeniden göndermeden ettirilebilir.</span><span class="sxs-lookup"><span data-stu-id="92046-227">Incremental ReadDocumentFeed can be resumed by resubmitting this value in If-None-Match.</span></span></p>
        </td>
    </tr>
</table>

<span data-ttu-id="92046-228">Örnek istek tooreturn İşte hello mantıksal sürüm/ETag koleksiyonda tüm artımlı değişiklikler `28535` ve bölüm anahtarı aralığının = `16`:</span><span class="sxs-lookup"><span data-stu-id="92046-228">Here's a sample request tooreturn all incremental changes in collection from hello logical version/ETag `28535` and partition key range = `16`:</span></span>

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

<span data-ttu-id="92046-229">Değişiklikleri süre içinde hello bölüm anahtarı aralığının her bölüm anahtarı değerine göre sıralanır.</span><span class="sxs-lookup"><span data-stu-id="92046-229">Changes are ordered by time within each partition key value within hello partition key range.</span></span> <span data-ttu-id="92046-230">Bölüm anahtarı değerleri arasında hiçbir garanti edilen sipariş yoktur.</span><span class="sxs-lookup"><span data-stu-id="92046-230">There is no guaranteed order across partition-key values.</span></span> <span data-ttu-id="92046-231">Tek bir sayfayla sığmayacak daha fazla sonuç yoksa hello hello isteğini yeniden göndermeden hello sonraki sonuç sayfasını okuyabilirsiniz `If-None-Match` değer eşit toohello üstbilgiyle `etag` hello önceki yanıt gelen.</span><span class="sxs-lookup"><span data-stu-id="92046-231">If there are more results than can fit in a single page, you can read hello next page of results by resubmitting hello request with hello `If-None-Match` header with value equal toohello `etag` from hello previous response.</span></span> <span data-ttu-id="92046-232">Birden çok belge eklendi veya işlemsel olarak bir saklı yordam veya tetikleyici içinde güncelleştirildi, bunlar tüm hello içinde aynı döndürülecek yanıt sayfası.</span><span class="sxs-lookup"><span data-stu-id="92046-232">If multiple documents were inserted or updated transactionally within a stored procedure or trigger, they will all be returned within hello same response page.</span></span>

> [!NOTE]
> <span data-ttu-id="92046-233">Değişiklik akış ile daha fazla öğe bir sayfa içinde belirtilenden döndürülen alabilirsiniz `x-ms-max-item-count` hello durumda eklenir veya güncelleştirilir saklı yordamların içinde birden fazla belge veya tetikler.</span><span class="sxs-lookup"><span data-stu-id="92046-233">With change feed, you might get more items returned in a page than specified in `x-ms-max-item-count` in hello case of multiple documents inserted or updated inside a stored procedures or triggers.</span></span> 

<span data-ttu-id="92046-234">Merhaba .NET SDK'sı (1.17.0) kullanırken, hello alan kümesi `StartTime` içinde `ChangeFeedOptions` beri değiştirilen toodirectly dönüş belgeleri `StartTime` çağrılırken `CreateDocumentChangeFeedQuery`.</span><span class="sxs-lookup"><span data-stu-id="92046-234">When using hello .NET SDK (1.17.0), set hello field `StartTime` in `ChangeFeedOptions` toodirectly return changed documents since `StartTime` when calling  `CreateDocumentChangeFeedQuery`.</span></span> <span data-ttu-id="92046-235">Belirterek `If-Modified-Since` hello REST API kullanarak, isteğiniz hello belgeleri değil kendilerini ancak bunun yerine hello devamlılık belirteci döndürür veya `etag` hello yanıt üstbilgisi içinde.</span><span class="sxs-lookup"><span data-stu-id="92046-235">By specifying `If-Modified-Since` using hello REST API, your request will return not hello documents themselves, but rather hello continuation token or `etag` in hello response header.</span></span> <span data-ttu-id="92046-236">Değiştirilen hello belirtilen süre, hello devamlılık belirteci tooreturn hello belgelerin `etag` sonra hello sonraki istekle kullanılmalıdır `If-None-Match` tooreturn hello gerçek belgeleri.</span><span class="sxs-lookup"><span data-stu-id="92046-236">tooreturn hello documents modified hello specified time, hello continuation token `etag` must then be used in hello next request with `If-None-Match` tooreturn hello actual documents.</span></span> 

<span data-ttu-id="92046-237">Merhaba .NET SDK'sı sağlar hello [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) ve [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) yardımcı sınıfları tooaccess değişikliklerinin tooa koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="92046-237">hello .NET SDK provides hello [CreateDocumentChangeFeedQuery](/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentchangefeedquery?view=azure-dotnet) and [ChangeFeedOptions](/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) helper classes tooaccess changes made tooa collection.</span></span> <span data-ttu-id="92046-238">Merhaba aşağıdaki kod parçacığında tooretrieve tüm tek bir istemciden gelen hello .NET SDK kullanarak hello başından nasıl değiştiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="92046-238">hello following snippet shows how tooretrieve all changes from hello beginning using hello .NET SDK from a single client.</span></span>

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
<span data-ttu-id="92046-239">Ve hello aşağıdaki kod parçacığında nasıl tooprocess gerçek zamanlı olarak değiştiğini gösterir hello değişiklik kullanarak Azure Cosmos DB ile destek akışı ve işlev önceki hello.</span><span class="sxs-lookup"><span data-stu-id="92046-239">And hello following snippet shows how tooprocess changes in real-time with Azure Cosmos DB by using hello change feed support and hello preceding function.</span></span> <span data-ttu-id="92046-240">Hello ilk çağrıda hello koleksiyonundaki tüm hello belgeleri döndürür ve hello ikinci yalnızca hello hello son denetim noktasının bu yana oluşturulan oluşturulan iki belgeler döndürür.</span><span class="sxs-lookup"><span data-stu-id="92046-240">hello first call returns all hello documents in hello collection, and hello second only returns hello two documents created that were created since hello last checkpoint.</span></span>

```csharp
// Returns all documents in hello collection.
Dictionary<string, string> checkpoints = await GetChanges(client, collection, new Dictionary<string, string>());

await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-201", MetricType = "Temperature", Unit = "Celsius", MetricValue = 1000 });
await client.CreateDocumentAsync(collection, new DeviceReading { DeviceId = "xsensr-212", MetricType = "Pressure", Unit = "psi", MetricValue = 1000 });

// Returns only hello two documents created above.
checkpoints = await GetChanges(client, collection, checkpoints);
```

<span data-ttu-id="92046-241">İstemci tarafı mantığı tooselectively işlem olayları kullanarak hello değişiklik akış de filtre uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="92046-241">You can also filter hello change feed using client side logic tooselectively process events.</span></span> <span data-ttu-id="92046-242">Örneğin, istemci tarafı LINQ tooprocess aygıt algılayıcılar olayları sıcaklık değiştirmek yalnızca kullanan bir parçacığı aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="92046-242">For example, here's a snippet that uses client side LINQ tooprocess only temperature change events from device sensors.</span></span>

```csharp
FeedResponse<DeviceReading> readChangesResponse = query.ExecuteNextAsync<DeviceReading>().Result;

foreach (DeviceReading changedDocument in 
    readChangesResponse.AsEnumerable().Where(d => d.MetricType == "Temperature" && d.MetricValue > 1000L))
{
    // trigger an action, like call an API
}
```

## <span data-ttu-id="92046-243"><a id="change-feed-processor"></a>Değişiklik işlemci akışı kitaplığı</span><span class="sxs-lookup"><span data-stu-id="92046-243"><a id="change-feed-processor"></a>Change Feed Processor library</span></span>
<span data-ttu-id="92046-244">Başka bir seçenektir toouse hello [Azure Cosmos DB değiştirmek akış işlemci Kitaplığı](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), hangi yardımcı olabilir, olay arasında birden çok tüketiciye akışı bir değişiklik gelen işleme kolayca dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="92046-244">Another option is toouse hello [Azure Cosmos DB Change Feed Processor library](https://docs.microsoft.com/azure/cosmos-db/documentdb-sdk-dotnet-changefeed), which can help you easily distribute event processing from a change feed across multiple consumers.</span></span> <span data-ttu-id="92046-245">Merhaba kitaplığı hello .NET platformu üzerinde okuyucular akış değişiklik oluşturmak için mükemmeldir.</span><span class="sxs-lookup"><span data-stu-id="92046-245">hello library is great for building change feed readers on hello .NET platform.</span></span> <span data-ttu-id="92046-246">Hello dahil hello yöntemleri üzerinden hello değişiklik akış işlemci kitaplığı kullanılarak Basitleştirilmiş bazı iş akışları diğer Cosmos DB SDK aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="92046-246">Some workflows that would be simplified by using hello Change Feed Processor library over hello methods included in hello other Cosmos DB SDKs include:</span></span> 

* <span data-ttu-id="92046-247">Birden çok bölüm arasında veri depolandığında değişiklik çekilmesini güncelleştirmelerini akışı</span><span class="sxs-lookup"><span data-stu-id="92046-247">Pulling updates from change feed when data is stored across multiple partitions</span></span>
* <span data-ttu-id="92046-248">Taşıma veya bir koleksiyon tooanother veri çoğaltma</span><span class="sxs-lookup"><span data-stu-id="92046-248">Moving or replicating data from one collection tooanother</span></span>
* <span data-ttu-id="92046-249">Paralel yürütme güncelleştirmeleri toodata tarafından tetiklenen eylemler ve akış Değiştir</span><span class="sxs-lookup"><span data-stu-id="92046-249">Parallel execution of actions triggered by updates toodata and change feed</span></span> 

<span data-ttu-id="92046-250">Merhaba Cosmos SDK'ları Hello API'lerini kullanarak kesin erişim toochange güncelleştirmeleri her bölüm akış sağlarken hello değişiklik akış işlemci kitaplığını kullanarak bölümler ve paralel çalışan birden çok iş parçacığı üzerinde okuma değişiklikleri basitleştirir.</span><span class="sxs-lookup"><span data-stu-id="92046-250">While using hello APIs in hello Cosmos SDKs provides precise access toochange feed updates in each partition, using hello Change Feed Processor library simplifies reading changes across partitions and multiple threads working in parallel.</span></span> <span data-ttu-id="92046-251">El ile değişiklikleri her kapsayıcıdan okuma ve kaydetme her bölüm için devamlılık belirteci yerine hello değişiklik akış işlemci okuma değişiklikleri bir kiralama mekanizması kullanarak bölümleri arasında otomatik olarak yönetir.</span><span class="sxs-lookup"><span data-stu-id="92046-251">Instead of manually reading changes from each container and saving a continuation token for each partition, hello Change Feed Processor automatically manages reading changes across partitions using a lease mechanism.</span></span>

<span data-ttu-id="92046-252">Merhaba kitaplığı NuGet paketi olarak kullanılabilir: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) ve bir Github olarak kaynak koddan [örnek](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor).</span><span class="sxs-lookup"><span data-stu-id="92046-252">hello library is available as a NuGet Package: [Microsoft.Azure.Documents.ChangeFeedProcessor](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) and from source code as a Github [sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor).</span></span> 

### <a name="understanding-change-feed-processor-library"></a><span data-ttu-id="92046-253">Anlama değişiklik akış işlemci kitaplığı</span><span class="sxs-lookup"><span data-stu-id="92046-253">Understanding Change Feed Processor library</span></span> 

<span data-ttu-id="92046-254">Merhaba değişiklik akış işlemci gerçekleştirilmesinin dört ana bileşen mevcuttur: hello izlenen koleksiyonu, hello kira koleksiyonu, hello işleyicisi konağı ve hello tüketicileri.</span><span class="sxs-lookup"><span data-stu-id="92046-254">There are four main components of implementing hello Change Feed Processor: hello monitored collection, hello lease collection, hello processor host, and hello consumers.</span></span> 

<span data-ttu-id="92046-255">**İzlenen koleksiyonu:** izlenen hello koleksiyonudur hello veri hangi hello değişiklik akış oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="92046-255">**Monitored Collection:** hello monitored collection is hello data from which hello change feed is generated.</span></span> <span data-ttu-id="92046-256">Herhangi bir eklemeleri ve değişiklikleri izlenen toohello koleksiyonu hello koleksiyonunun değişiklik akışta hello yansıtılır.</span><span class="sxs-lookup"><span data-stu-id="92046-256">Any inserts and changes toohello monitored collection are reflected in hello change feed of hello collection.</span></span> 

<span data-ttu-id="92046-257">**Kira koleksiyonu:** hello değişiklik arasında birden çok Worker akış işleme kira koleksiyonu koordinatları hello.</span><span class="sxs-lookup"><span data-stu-id="92046-257">**Lease Collection:** hello lease collection coordinates processing hello change feed across multiple workers.</span></span> <span data-ttu-id="92046-258">Ayrı bir kira bölüm başına ile kullanılan toostore hello kiraları koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="92046-258">A separate collection is used toostore hello leases with one lease per partition.</span></span> <span data-ttu-id="92046-259">Bu kira koleksiyonu hello ile farklı bir hesap üzerinde değişiklik akış işlemci çalıştıran bölge daha yakından toowhere hello yazmak avantajlı toostore olur.</span><span class="sxs-lookup"><span data-stu-id="92046-259">It is advantageous toostore this lease collection on a different account with hello write region closer toowhere hello Change Feed Processor is running.</span></span> <span data-ttu-id="92046-260">Bir kira nesnesi öznitelikleri aşağıdaki hello içerir:</span><span class="sxs-lookup"><span data-stu-id="92046-260">A lease object contains hello following attributes:</span></span> 
* <span data-ttu-id="92046-261">Sahibi: hello kira sahibi hello konak belirtir</span><span class="sxs-lookup"><span data-stu-id="92046-261">Owner: Specifies hello host that owns hello lease</span></span>
* <span data-ttu-id="92046-262">Devamlılık: hello konumu (devamlılık belirteci) için belirli bir bölüm akış hello değişikliği belirtir.</span><span class="sxs-lookup"><span data-stu-id="92046-262">Continuation: Specifies hello position (continuation token) in hello change feed for a particular partition</span></span>
* <span data-ttu-id="92046-263">Zaman damgası: kira güncelleştirildi; son zamanı Merhaba kira süresi dolmuş olarak kabul edilir olup olmadığını Hello zaman damgası kullanılan toocheck olabilir</span><span class="sxs-lookup"><span data-stu-id="92046-263">Timestamp: Last time lease was updated; hello timestamp can be used toocheck whether hello lease is considered expired</span></span> 

<span data-ttu-id="92046-264">**İşlemci ana bilgisayarı:** kaç bölümleri tooprocess etkin kiralamaları kaç ana örneklerini olmadığına göre her bir ana bilgisayar belirler.</span><span class="sxs-lookup"><span data-stu-id="92046-264">**Processor Host:** Each host determines how many partitions tooprocess based on how many other instances of hosts have active leases.</span></span> 
1.  <span data-ttu-id="92046-265">Bir ana bilgisayar başlatıldığında tüm ana bilgisayarlar arasında kiraları toobalance hello iş yükünü devralır.</span><span class="sxs-lookup"><span data-stu-id="92046-265">When a host starts up, it acquires leases toobalance hello workload across all hosts.</span></span> <span data-ttu-id="92046-266">Kira etkin şekilde bir ana bilgisayar kiralama, düzenli aralıklarla yeniler.</span><span class="sxs-lookup"><span data-stu-id="92046-266">A host periodically renews leases, so leases remain active.</span></span> 
2.  <span data-ttu-id="92046-267">Bir ana bilgisayar kontrol noktaları hello son devamlılık belirteci tooits kira her okuyun.</span><span class="sxs-lookup"><span data-stu-id="92046-267">A host checkpoints hello last continuation token tooits lease for each read.</span></span> <span data-ttu-id="92046-268">tooensure eşzamanlılık güvenliği, bir konak hello ETag her bir kira güncelleştirme denetler.</span><span class="sxs-lookup"><span data-stu-id="92046-268">tooensure concurrency safety, a host checks hello ETag for each lease update.</span></span> <span data-ttu-id="92046-269">Diğer denetim noktası stratejileri de desteklenir.</span><span class="sxs-lookup"><span data-stu-id="92046-269">Other checkpoint strategies are also supported.</span></span>  
3.  <span data-ttu-id="92046-270">Kapatma, bağlı bir ana bilgisayar tüm kira serbest ancak daha sonra okuma hello saklı kontrol noktasından devam edebilmek için tutar devamlılık bilgi hello.</span><span class="sxs-lookup"><span data-stu-id="92046-270">Upon shutdown, a host releases all leases but keeps hello continuation information, so it can resume reading from hello stored checkpoint later.</span></span> 

<span data-ttu-id="92046-271">Şu anda ana bilgisayar hello sayısı hello bölümleri (kiraları) sayısından büyük olamaz.</span><span class="sxs-lookup"><span data-stu-id="92046-271">At this time hello number of hosts cannot be greater than hello number of partitions (leases).</span></span>

<span data-ttu-id="92046-272">**Tüketiciler:** tüketici veya çalışanları olan her konak tarafından başlatılan işlem akışı hello değişikliği gerçekleştiren iş parçacığı.</span><span class="sxs-lookup"><span data-stu-id="92046-272">**Consumers:** Consumers, or workers, are threads that perform hello change feed processing initiated by each host.</span></span> <span data-ttu-id="92046-273">Her işlemci ana bilgisayarın birden çok tüketiciye sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="92046-273">Each processor host can have multiple consumers.</span></span> <span data-ttu-id="92046-274">Her bir tüketici okur hello değişiklik akış hello tooand atandı bölüm değişiklikleri ana bilgisayar bildirir ve kira süresi doldu.</span><span class="sxs-lookup"><span data-stu-id="92046-274">Each consumer reads hello change feed from hello partition it is assigned tooand notifies its host of changes and expired leases.</span></span>

<span data-ttu-id="92046-275">toofurther değişiklik akış işlemci dört bu unsuru birlikte nasıl çalıştığını anlamak, diyagram aşağıdaki hello içinde bir örneğe bakalım.</span><span class="sxs-lookup"><span data-stu-id="92046-275">toofurther understand how these four elements of Change Feed Processor work together, let's look at an example in hello following diagram.</span></span> <span data-ttu-id="92046-276">Merhaba koleksiyonu depoları belgeleri izlenen ve hello "Şehir" Merhaba bölüm anahtarı olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="92046-276">hello monitored collection stores documents and uses hello "city" as hello partition key.</span></span> <span data-ttu-id="92046-277">Merhaba mavi bölüm "A-E" hello "Şehir" alanını belgeler vb. içerdiğini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="92046-277">We see that hello blue partition contains documents with hello "city" field from "A-E" and so on.</span></span> <span data-ttu-id="92046-278">Her iki tüketicileri hello dört bölümü paralel okuma ile iki ana vardır.</span><span class="sxs-lookup"><span data-stu-id="92046-278">There are two hosts, each with two consumers reading from hello four partitions in parallel.</span></span> <span data-ttu-id="92046-279">Merhaba oklar, akış hello belirli bir noktada okuma hello tüketicileri değiştirmek gösterir.</span><span class="sxs-lookup"><span data-stu-id="92046-279">hello arrows show hello consumers reading from a specific spot in hello change feed.</span></span> <span data-ttu-id="92046-280">Merhaba mavi zaten hello değişiklik akış değişiklikleri okuma hello temsil ederken hello ilk bölümünde hello Koyu mavi okunmamış değişiklikler temsil eder.</span><span class="sxs-lookup"><span data-stu-id="92046-280">In hello first partition, hello darker blue represents unread changes while hello light blue represents hello already read changes on hello change feed.</span></span> <span data-ttu-id="92046-281">Merhaba konakları hello kira koleksiyonu toostore hello her tüketici konumunu okuma geçerli "devamlılık" değeri tookeep izini kullanın.</span><span class="sxs-lookup"><span data-stu-id="92046-281">hello hosts use hello lease collection toostore a "continuation" value tookeep track of hello current reading position for each consumer.</span></span> 

![Hello Azure Cosmos DB değişikliği kullanarak akış işlemcisi konağı](./media/change-feed/changefeedprocessornew.png)

### <a name="using-change-feed-processor-library"></a><span data-ttu-id="92046-283">Değişiklik kullanarak akış işlemci kitaplığı</span><span class="sxs-lookup"><span data-stu-id="92046-283">Using Change Feed Processor Library</span></span> 
<span data-ttu-id="92046-284">bölümden hello nasıl toouse hello kaynak koleksiyonu tooa hedef koleksiyondan değişiklikleri çoğaltmaya hello bağlamı değişiklik akış işlemci kitaplıkta açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="92046-284">hello following section explains how toouse hello Change Feed Processor library in hello context of replicating changes from a source collection tooa destination collection.</span></span> <span data-ttu-id="92046-285">Burada, hello kaynak koleksiyonu izlenen hello değişiklik akış işlemcide koleksiyonudur.</span><span class="sxs-lookup"><span data-stu-id="92046-285">Here, hello source collection is hello monitored collection in Change Feed Processor.</span></span> 

<span data-ttu-id="92046-286">**Yükleme ve hello değişiklik akış işlemci NuGet paketini ekleyin**</span><span class="sxs-lookup"><span data-stu-id="92046-286">**Install and include hello Change Feed Processor NuGet package**</span></span> 

<span data-ttu-id="92046-287">Değişiklik akış işlemci NuGet paketini yüklemeden önce ilk yükleyin:</span><span class="sxs-lookup"><span data-stu-id="92046-287">Before installing Change Feed Processor NuGet Package, first install:</span></span> 
* <span data-ttu-id="92046-288">Microsoft.Azure.DocumentDB, sürüm 1.13.1 veya üstü</span><span class="sxs-lookup"><span data-stu-id="92046-288">Microsoft.Azure.DocumentDB, version 1.13.1 or above</span></span> 
* <span data-ttu-id="92046-289">Newtonsoft.Json, sürüm 9.0.1 veya yükleme yukarıda `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` ve bir başvuru olarak dahil edin.</span><span class="sxs-lookup"><span data-stu-id="92046-289">Newtonsoft.Json, version 9.0.1 or above Install `Microsoft.Azure.DocumentDB.ChangeFeedProcessor` and include it as a reference.</span></span>

<span data-ttu-id="92046-290">**İzlenen, kiralama ve hedef koleksiyon oluşturma**</span><span class="sxs-lookup"><span data-stu-id="92046-290">**Create a monitored, lease and destination collection**</span></span> 

<span data-ttu-id="92046-291">Sipariş toouse hello değişiklik akış işlemci kitaplığı, hello kira koleksiyonu hello işlemci boşaltıyor çalıştırmadan önce oluşturulan toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="92046-291">In order toouse hello Change Feed Processor Library, hello lease collection needs toobe created before running hello processor host(s).</span></span> <span data-ttu-id="92046-292">Yeniden değişikliği akış işlemci çalıştıran farklı bir hesap üzerinde yazma bölge daha yakından toowhere hello ile bir kira koleksiyon depolamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="92046-292">Again, we recommend storing a lease collection on a different account with a write region closer toowhere hello Change Feed Processor is running.</span></span> <span data-ttu-id="92046-293">Bu veri taşıma örnekte hello değişiklik akış işleyicisi konağı çalıştırmadan önce toocreate hello hedef koleksiyonu gerekir.</span><span class="sxs-lookup"><span data-stu-id="92046-293">In this data movement example, we need toocreate hello destination collection before running hello Change Feed Processor host.</span></span> <span data-ttu-id="92046-294">İzlenen bir yardımcı yöntem toocreate Merhaba diyoruz Hello örnek kodda kiralık ve zaten mevcut değilse hedef koleksiyonları.</span><span class="sxs-lookup"><span data-stu-id="92046-294">In hello sample code we call a helper method toocreate hello monitored, leased, and destination collections if they do not already exist.</span></span> 

> [!WARNING]
> <span data-ttu-id="92046-295">Üretilen iş ile Azure Cosmos DB hello uygulama toocommunicate için ayırma gibi bir koleksiyon oluşturma, fiyatlandırmaya vardır.</span><span class="sxs-lookup"><span data-stu-id="92046-295">Creating a collection has pricing implications, as you are reserving throughput for hello application toocommunicate with Azure Cosmos DB.</span></span> <span data-ttu-id="92046-296">Daha fazla ayrıntı için lütfen başlangıç adresini ziyaret edin [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/cosmos-db/)</span><span class="sxs-lookup"><span data-stu-id="92046-296">For more details, please visit hello [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

<span data-ttu-id="92046-297">*İşlemci konak oluşturma*</span><span class="sxs-lookup"><span data-stu-id="92046-297">*Creating a processor host*</span></span>

<span data-ttu-id="92046-298">Merhaba `ChangeFeedProcessorHost` sınıfı, olay işlemcisi uygulamaları için aynı zamanda denetim noktası oluşturma ve bölüm kiralama Yönetimi sağlayan bir iş parçacığı, çok işlemli, güvenli çalışma zamanı ortamı sağlar.</span><span class="sxs-lookup"><span data-stu-id="92046-298">hello `ChangeFeedProcessorHost` class provides a thread-safe, multi-process, safe runtime environment for event processor implementations that also provides checkpointing and partition lease management.</span></span> <span data-ttu-id="92046-299">toouse hello `ChangeFeedProcessorHost` sınıfı, uygulayabilirsiniz `IChangeFeedObserver`.</span><span class="sxs-lookup"><span data-stu-id="92046-299">toouse hello `ChangeFeedProcessorHost` class, you can implement `IChangeFeedObserver`.</span></span> <span data-ttu-id="92046-300">Bu arabirim üç yöntem içerir:</span><span class="sxs-lookup"><span data-stu-id="92046-300">This interface contains three methods:</span></span>

* <span data-ttu-id="92046-301">`OpenAsync`: Bu işlev, değişiklik akış gözlemci açıldığında çağrılır.</span><span class="sxs-lookup"><span data-stu-id="92046-301">`OpenAsync`: This function is called when change feed observer is opened.</span></span> <span data-ttu-id="92046-302">Tüketici/gözlemci açıldığında değiştirilmiş tooperform belirli bir eylemi olabilir.</span><span class="sxs-lookup"><span data-stu-id="92046-302">It can be modified tooperform a specific action when consumer/observer is opened.</span></span>  
* <span data-ttu-id="92046-303">`CloseAsync`: Değişiklik akış gözlemci sonlandırıldığında bu işlev çağrılır.</span><span class="sxs-lookup"><span data-stu-id="92046-303">`CloseAsync`: This function is called when change feed observer is terminated.</span></span> <span data-ttu-id="92046-304">Tüketici/gözlemci kapatıldığında değiştirilmiş tooperform belirli bir eylemi olabilir.</span><span class="sxs-lookup"><span data-stu-id="92046-304">It can be modified tooperform a specific action when consumer/observer is closed.</span></span>  
* <span data-ttu-id="92046-305">`ProcessChangesAsync`: Belge yeni değişiklikleri değişiklik Besleme üzerindeki kullanılabilir olduğunda bu işlev çağrılır.</span><span class="sxs-lookup"><span data-stu-id="92046-305">`ProcessChangesAsync`: This function is called when document new changes are available on change feed.</span></span> <span data-ttu-id="92046-306">Değiştirilen tooperform her akış değişiklik güncelleştirme sırasında belirli bir eylemi olabilir.</span><span class="sxs-lookup"><span data-stu-id="92046-306">It can be modified tooperform a specific action upon every change feed update.</span></span>  

<span data-ttu-id="92046-307">Bizim örneğimizde, biz hello arabirimini uygulayan `IChangeFeedObserver` hello aracılığıyla `DocumentFeedObserver` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="92046-307">In our example, we implement hello interface `IChangeFeedObserver` through hello `DocumentFeedObserver` class.</span></span> <span data-ttu-id="92046-308">Burada, hello `ProcessChangesAsync` işlev değişikliği belgeden akış hello hedef koleksiyona upserts (güncelleştirmeler).</span><span class="sxs-lookup"><span data-stu-id="92046-308">Here, hello `ProcessChangesAsync` function upserts (updates) a document from change feed into hello destination collection.</span></span> <span data-ttu-id="92046-309">Bu örnek, bir koleksiyon tooanother sipariş toochange hello bölüm anahtarı, bir veri kümesinin veri taşıma için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="92046-309">This example is useful for moving data from one collection tooanother in order toochange hello partition key of a data set.</span></span> 

<span data-ttu-id="92046-310">*Çalışan hello işlemcisi konağı*</span><span class="sxs-lookup"><span data-stu-id="92046-310">*Running hello Processor Host*</span></span>

<span data-ttu-id="92046-311">Olay işleme başlamadan önce her ikisi de akış seçeneklerini değiştirin ve akış konak seçeneklerini değiştirme özelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="92046-311">Before beginning event processing, both change feed options and change feed host options can be customized.</span></span> 
```csharp
    // Customizable change feed option and host options 
    ChangeFeedOptions feedOptions = new ChangeFeedOptions();

    // ie customize StartFromBeginning so change feed reads from beginning
    // can customize MaxItemCount, PartitonKeyRangeId, RequestContinuation, SessionToken and StartFromBeginning
    feedOptions.StartFromBeginning = true;

    ChangeFeedHostOptions feedHostOptions = new ChangeFeedHostOptions();

    // ie. customizing lease renewal interval too15 seconds
    // can customize LeaseRenewInterval, LeaseAcquireInterval, LeaseExpirationInterval, FeedPollDelay 
    feedHostOptions.LeaseRenewInterval = TimeSpan.FromSeconds(15);

```
<span data-ttu-id="92046-312">özelleştirilebilir hello belirli alanlar tabloları aşağıdaki hello özetlenir.</span><span class="sxs-lookup"><span data-stu-id="92046-312">hello specific fields that can be customized are summarized in hello following tables.</span></span> 

<span data-ttu-id="92046-313">**Akış seçeneklerini değiştirme**:</span><span class="sxs-lookup"><span data-stu-id="92046-313">**Change Feed Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="92046-314">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="92046-314">Property Name</span></span></th>
        <th><span data-ttu-id="92046-315">Açıklama</span><span class="sxs-lookup"><span data-stu-id="92046-315">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="92046-316">MaxItemCount</span><span class="sxs-lookup"><span data-stu-id="92046-316">MaxItemCount</span></span></td>
        <td><span data-ttu-id="92046-317">Alır veya hello Azure Cosmos DB veritabanı hizmeti hello numaralandırma işlemi döndürdü öğeleri toobe hello sayısını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="92046-317">Gets or sets hello maximum number of items toobe returned in hello enumeration operation in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="92046-318">PartitionKeyRangeId</span><span class="sxs-lookup"><span data-stu-id="92046-318">PartitionKeyRangeId</span></span></td>
        <td><span data-ttu-id="92046-319">Alır veya hello Azure Cosmos DB veritabanı hizmetinin hello bölüm anahtarı aralığının kimliği hello geçerli istek için ayarlar.</span><span class="sxs-lookup"><span data-stu-id="92046-319">Gets or sets hello partition key range id for hello current request in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="92046-320">RequestContinuation</span><span class="sxs-lookup"><span data-stu-id="92046-320">RequestContinuation</span></span></td>
        <td><span data-ttu-id="92046-321">Alır veya hello Azure Cosmos DB veritabanı hizmetinin hello isteği devamlılık belirteci ayarlar.</span><span class="sxs-lookup"><span data-stu-id="92046-321">Gets or sets hello request continuation token in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="92046-322">SessionToken</span><span class="sxs-lookup"><span data-stu-id="92046-322">SessionToken</span></span></td>
        <td><span data-ttu-id="92046-323">Alır veya oturum tutarlılığı hello Azure Cosmos DB veritabanı hizmeti ile Merhaba Oturum belirteci kullanmak için ayarlar.</span><span class="sxs-lookup"><span data-stu-id="92046-323">Gets or sets hello session token for use with session consistency in hello Azure Cosmos DB database service.</span></span></td>
    </tr>
        <tr>
        <td><span data-ttu-id="92046-324">StartFromBeginning</span><span class="sxs-lookup"><span data-stu-id="92046-324">StartFromBeginning</span></span></td>
        <td><span data-ttu-id="92046-325">Alır veya değişiklik hello Azure Cosmos DB veritabanı hizmetinin akış (true) itibaren hello ya da geçerli (false) başlamalıdır olup olmadığını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="92046-325">Gets or sets whether change feed in hello Azure Cosmos DB database service should start from hello beginning (true) or from current (false).</span></span> <span data-ttu-id="92046-326">Varsayılan olarak, geçerli (false) başlar.</span><span class="sxs-lookup"><span data-stu-id="92046-326">By default, it starts from current (false).</span></span></td>
    </tr>
</table>

<span data-ttu-id="92046-327">**Akış konak seçeneklerini değiştirme**:</span><span class="sxs-lookup"><span data-stu-id="92046-327">**Change Feed Host Options**:</span></span>
<table>
    <tr>
        <th><span data-ttu-id="92046-328">Özellik adı</span><span class="sxs-lookup"><span data-stu-id="92046-328">Property Name</span></span></th>
        <th><span data-ttu-id="92046-329">Tür</span><span class="sxs-lookup"><span data-stu-id="92046-329">Type</span></span></th>
        <th><span data-ttu-id="92046-330">Açıklama</span><span class="sxs-lookup"><span data-stu-id="92046-330">Description</span></span></th>
    </tr>
    <tr>
        <td><span data-ttu-id="92046-331">LeaseRenewInterval</span><span class="sxs-lookup"><span data-stu-id="92046-331">LeaseRenewInterval</span></span></td>
        <td><span data-ttu-id="92046-332">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="92046-332">TimeSpan</span></span></td>
        <td><span data-ttu-id="92046-333">şu anda hello ChangeFeedEventHost örneği tarafından tutulan bölümler için tüm kiraları Hello aralığı.</span><span class="sxs-lookup"><span data-stu-id="92046-333">hello interval for all leases for partitions currently held by hello ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="92046-334">LeaseAcquireInterval</span><span class="sxs-lookup"><span data-stu-id="92046-334">LeaseAcquireInterval</span></span></td>
        <td><span data-ttu-id="92046-335">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="92046-335">TimeSpan</span></span></td>
        <td><span data-ttu-id="92046-336">bölümler dağılımla bilinen konak örnekler arasında olup olmadığını aralığı tookick görev toocompute kapalı hello.</span><span class="sxs-lookup"><span data-stu-id="92046-336">hello interval tookick off a task toocompute whether partitions are distributed evenly among known host instances.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="92046-337">LeaseExpirationInterval</span><span class="sxs-lookup"><span data-stu-id="92046-337">LeaseExpirationInterval</span></span></td>
        <td><span data-ttu-id="92046-338">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="92046-338">TimeSpan</span></span></td>
        <td><span data-ttu-id="92046-339">Merhaba aralığı için hangi hello kira bir bölüm temsil eden bir kira alınır.</span><span class="sxs-lookup"><span data-stu-id="92046-339">hello interval for which hello lease is taken on a lease representing a partition.</span></span> <span data-ttu-id="92046-340">Merhaba kira bu aralıkta yenilenmezse, süresi doldu ve tooanother ChangeFeedEventHost örneği hello bölüm sahipliğini taşır.</span><span class="sxs-lookup"><span data-stu-id="92046-340">If hello lease is not renewed within this interval, it is expired and ownership of hello partition moves tooanother ChangeFeedEventHost instance.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="92046-341">FeedPollDelay</span><span class="sxs-lookup"><span data-stu-id="92046-341">FeedPollDelay</span></span></td>
        <td><span data-ttu-id="92046-342">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="92046-342">TimeSpan</span></span></td>
        <td><span data-ttu-id="92046-343">Tüm geçerli değişiklikleri boşaltmış sonra bir bölüm hello yeni değişiklikleri için yoklama arasındaki hello gecikme akış.</span><span class="sxs-lookup"><span data-stu-id="92046-343">hello delay between polling a partition for new changes on hello feed, after all current changes are drained.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="92046-344">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="92046-344">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="92046-345">CheckpointFrequency</span><span class="sxs-lookup"><span data-stu-id="92046-345">CheckpointFrequency</span></span></td>
        <td><span data-ttu-id="92046-346">Merhaba sıklığı toocheckpoint kiralar.</span><span class="sxs-lookup"><span data-stu-id="92046-346">hello frequency toocheckpoint leases.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="92046-347">MinPartitionCount</span><span class="sxs-lookup"><span data-stu-id="92046-347">MinPartitionCount</span></span></td>
        <td><span data-ttu-id="92046-348">Int</span><span class="sxs-lookup"><span data-stu-id="92046-348">Int</span></span></td>
        <td><span data-ttu-id="92046-349">Merhaba ana Hello en düşük bölüm sayısı.</span><span class="sxs-lookup"><span data-stu-id="92046-349">hello minimum partition count for hello host.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="92046-350">MaxPartitionCount</span><span class="sxs-lookup"><span data-stu-id="92046-350">MaxPartitionCount</span></span></td>
        <td><span data-ttu-id="92046-351">Int</span><span class="sxs-lookup"><span data-stu-id="92046-351">Int</span></span></td>
        <td><span data-ttu-id="92046-352">bölümler hello konak Hello sayısının hizmet verebilir.</span><span class="sxs-lookup"><span data-stu-id="92046-352">hello maximum number of partitions hello host can serve.</span></span></td>
    </tr>
    <tr>
        <td><span data-ttu-id="92046-353">DiscardExistingLeases</span><span class="sxs-lookup"><span data-stu-id="92046-353">DiscardExistingLeases</span></span></td>
        <td><span data-ttu-id="92046-354">bool</span><span class="sxs-lookup"><span data-stu-id="92046-354">Bool</span></span></td>
        <td><span data-ttu-id="92046-355">Merhaba tüm mevcut kiraları hello ana bilgisayarın Başlat olup olmadığını silineceğini ve hello konak baştan başlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="92046-355">Whether on hello start of hello host all existing leases should be deleted and hello host should start from scratch.</span></span></td>
    </tr>
</table>


<span data-ttu-id="92046-356">toostart olay işleme, örneği `ChangeFeedProcessorHost`, Azure Cosmos DB koleksiyonunuz için hello uygun parametreleri sağlayarak.</span><span class="sxs-lookup"><span data-stu-id="92046-356">toostart event processing, instantiate `ChangeFeedProcessorHost`, providing hello appropriate parameters for your Azure Cosmos DB collection.</span></span> <span data-ttu-id="92046-357">Ardından, çağıran `RegisterObserverAsync` tooregister, `IChangeFeedObserver` hello çalışma zamanı (Bu örnekte DocumentFeedObserver) uygulaması.</span><span class="sxs-lookup"><span data-stu-id="92046-357">Then, call `RegisterObserverAsync` tooregister your `IChangeFeedObserver` (DocumentFeedObserver in this example) implementation with hello runtime.</span></span> <span data-ttu-id="92046-358">Bu noktada, hello konak tooacquire her bölüm anahtarı aralığının "Hızlı" algoritma kullanarak hello Azure Cosmos DB koleksiyonunda üzerinde bir kira çalışır.</span><span class="sxs-lookup"><span data-stu-id="92046-358">At this point, hello host attempts tooacquire a lease on every partition key range in hello Azure Cosmos DB collection using a "greedy" algorithm.</span></span> <span data-ttu-id="92046-359">Bu kiralar belirli bir zaman çerçevesi için en son ve sonrasında yenilenmelidir.</span><span class="sxs-lookup"><span data-stu-id="92046-359">These leases last for a given timeframe and must then be renewed.</span></span> <span data-ttu-id="92046-360">Yeni düğüm olarak çalışan örnekleri, bu durumda, çevrimiçi olması, kiralama ayırmaları yapar ve her konak tooacquire daha fazla kira girişimleri olarak zaman içinde hello yük düğümler arasında kayar..</span><span class="sxs-lookup"><span data-stu-id="92046-360">As new nodes, worker instances, in this case, come online, they place lease reservations and over time hello load shifts between nodes as each host attempts tooacquire more leases.</span></span> 

<span data-ttu-id="92046-361">Merhaba örnek kodda bir fabrika sınıfı (DocumentFeedObserverFactory.cs) toocreate bir gözlemci ve hello kullanırız `RegistObserverFactoryAsync` tooregister hello gözlemci.</span><span class="sxs-lookup"><span data-stu-id="92046-361">In hello sample code, we use a factory class (DocumentFeedObserverFactory.cs) toocreate an observer and hello `RegistObserverFactoryAsync` tooregister hello observer.</span></span> 

```csharp
using (DocumentClient destClient = new DocumentClient(destCollInfo.Uri, destCollInfo.MasterKey))
    {
        DocumentFeedObserverFactory docObserverFactory = new DocumentFeedObserverFactory(destClient, destCollInfo);
        ChangeFeedEventHost host = new ChangeFeedEventHost(hostName, documentCollectionLocation, leaseCollectionLocation, feedOptions, feedHostOptions);

        await host.RegisterObserverFactoryAsync(docObserverFactory);

        Console.WriteLine("Running... Press enter toostop.");
        Console.ReadLine();

        await host.UnregisterObserversAsync();
    }
```
<span data-ttu-id="92046-362">Zaman içerisinde bir denge sağlanır.</span><span class="sxs-lookup"><span data-stu-id="92046-362">Over time, an equilibrium is established.</span></span> <span data-ttu-id="92046-363">Bu dinamik özellik CPU tabanlı otomatik ölçeklendirme uygulanan toobe tooconsumers ölçek büyütme ve ölçek azaltma için etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="92046-363">This dynamic capability enables CPU-based auto-scaling toobe applied tooconsumers for both scale-up and scale-down.</span></span> <span data-ttu-id="92046-364">Değişiklikler Azure Cosmos DB'de tüketicilerin işleyebileceğinden daha hızlı bir oranda kullanılabilir hello tüketiciler üzerindeki CPU artışı çalışan örnek sayısı üzerinde otomatik ölçeklendirmeye kullanılan toocause olabilir.</span><span class="sxs-lookup"><span data-stu-id="92046-364">If changes are available in Azure Cosmos DB at a faster rate than consumers can process, hello CPU increase on consumers can be used toocause an auto-scale on worker instance count.</span></span>

## <a name="next-steps"></a><span data-ttu-id="92046-365">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="92046-365">Next steps</span></span>
* <span data-ttu-id="92046-366">Merhaba deneyin [Github'da Azure Cosmos DB Değiştir Akış kod örnekleri](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span><span class="sxs-lookup"><span data-stu-id="92046-366">Try hello [Azure Cosmos DB Change feed code samples on GitHub](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed)</span></span>
* <span data-ttu-id="92046-367">Kodlama Hello ile çalışmaya başlama [Azure Cosmos DB SDK'ları](documentdb-sdk-dotnet.md) veya hello [REST API](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="92046-367">Get started coding with hello [Azure Cosmos DB SDKs](documentdb-sdk-dotnet.md) or hello [REST API](/rest/api/documentdb/).</span></span>
