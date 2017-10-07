---
title: "aaaAzure Cosmos DB ölçek ve performans testi | Microsoft Docs"
description: "Nasıl tooperform ölçekleme ve performans Azure Cosmos DB ile test etme öğrenin"
keywords: Performans testi
services: cosmos-db
author: arramac
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: f4c96ebd-f53c-427d-a500-3f28fe7b11d0
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: arramac
ms.openlocfilehash: 46d1217e11a39ee970a868de9a5c5dfcf52cedf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-and-scale-testing-with-azure-cosmos-db"></a><span data-ttu-id="7a2e1-104">Performansı ve ölçeği Azure Cosmos DB ile test etme</span><span class="sxs-lookup"><span data-stu-id="7a2e1-104">Performance and scale testing with Azure Cosmos DB</span></span>
<span data-ttu-id="7a2e1-105">Performans ve ölçek testi adımdır bir anahtar uygulama geliştirme.</span><span class="sxs-lookup"><span data-stu-id="7a2e1-105">Performance and scale testing is a key step in application development.</span></span> <span data-ttu-id="7a2e1-106">Birçok uygulama için hello veritabanı katmanı önemli bir etkisi vardır genel performans ve ölçeklenebilirlik hello ve bu nedenle önemli bir bileşeni performansını sınamak.</span><span class="sxs-lookup"><span data-stu-id="7a2e1-106">For many applications, hello database tier has a significant impact on hello overall performance and scalability, and is therefore a critical component of performance testing.</span></span> <span data-ttu-id="7a2e1-107">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) amaca esnek ölçek ve tahmin edilebilir performans ve bu nedenle yüksek performanslı veritabanı katmanı gereken uygulamalar için harika bir uygun değil.</span><span class="sxs-lookup"><span data-stu-id="7a2e1-107">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is purpose-built for elastic scale and predictable performance, and therefore a great fit for applications that need a high-performance database tier.</span></span> 

<span data-ttu-id="7a2e1-108">Bu makale, kendi Cosmos DB iş yükleri için performansı test paketleri uygulamadan veya yüksek performanslı uygulama senaryoları için Cosmos DB değerlendirme geliştiriciler için bir başvurudur.</span><span class="sxs-lookup"><span data-stu-id="7a2e1-108">This article is a reference for developers implementing performance test suites for their Cosmos DB workloads, or evaluating Cosmos DB for high-performance application scenarios.</span></span> <span data-ttu-id="7a2e1-109">Yalıtılmış performans hello veritabanını öncelikle sınama odaklanır, ancak aynı zamanda üretim uygulamaları için en iyi yöntemleri içerir.</span><span class="sxs-lookup"><span data-stu-id="7a2e1-109">It focuses primarily on isolated performance testing of hello database, but also includes best practices for production applications.</span></span>

<span data-ttu-id="7a2e1-110">Bu makaleyi okuduktan sonra aşağıdaki soruları mümkün tooanswer hello olacaktır:</span><span class="sxs-lookup"><span data-stu-id="7a2e1-110">After reading this article, you will be able tooanswer hello following questions:</span></span>   

* <span data-ttu-id="7a2e1-111">Cosmos DB performans testi için bir örnek .NET istemci uygulaması nereden bulabilirim?</span><span class="sxs-lookup"><span data-stu-id="7a2e1-111">Where can I find a sample .NET client application for performance testing of Cosmos DB?</span></span> 
* <span data-ttu-id="7a2e1-112">My istemci uygulamasından nasıl Cosmos DB ile yüksek işleme düzeyleri elde?</span><span class="sxs-lookup"><span data-stu-id="7a2e1-112">How do I achieve high throughput levels with Cosmos DB from my client application?</span></span>

<span data-ttu-id="7a2e1-113">tooget kodu ile başlatıldı, lütfen hello projeden indirin [Azure Cosmos DB performans testi örneği](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="7a2e1-113">tooget started with code, please download hello project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span></span> 

> [!NOTE]
> <span data-ttu-id="7a2e1-114">Merhaba, bu uygulamanın istemci makineleri az sayıda ile daha iyi performans Cosmos DB dışında ayıklanacağı toodemonstrate en iyi yöntemler hedeftir.</span><span class="sxs-lookup"><span data-stu-id="7a2e1-114">hello goal of this application is toodemonstrate best practices for extracting better performance out of Cosmos DB with a small number of client machines.</span></span> <span data-ttu-id="7a2e1-115">Bu toodemonstrate hello yoğun genişlediğinden ölçeklendirebilirsiniz hello hizmet kapasitesini yapılmadı.</span><span class="sxs-lookup"><span data-stu-id="7a2e1-115">This was not made toodemonstrate hello peak capacity of hello service, which can scale limitlessly.</span></span>
> 
> 

<span data-ttu-id="7a2e1-116">İstemci tarafı yapılandırma seçenekleri tooimprove Cosmos DB performans arıyorsanız bkz [Azure Cosmos DB performans ipuçları](performance-tips.md).</span><span class="sxs-lookup"><span data-stu-id="7a2e1-116">If you're looking for client-side configuration options tooimprove Cosmos DB performance, see [Azure Cosmos DB performance tips](performance-tips.md).</span></span>

## <a name="run-hello-performance-testing-application"></a><span data-ttu-id="7a2e1-117">Merhaba performans uygulama testi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="7a2e1-117">Run hello performance testing application</span></span>
<span data-ttu-id="7a2e1-118">hızlı şekilde tooget hello başlatılan toocompile çalışma hello .NET örnek aşağıda hello aşağıdaki adımlarda açıklandığı gibi ise.</span><span class="sxs-lookup"><span data-stu-id="7a2e1-118">hello quickest way tooget started is toocompile and run hello .NET sample below, as described in hello steps below.</span></span> <span data-ttu-id="7a2e1-119">Ayrıca, hello kaynak kodu gözden geçirin ve benzer yapılandırmaları tooyour kendi istemci uygulamalarını uygulamak.</span><span class="sxs-lookup"><span data-stu-id="7a2e1-119">You can also review hello source code and implement similar configurations tooyour own client applications.</span></span>

<span data-ttu-id="7a2e1-120">**1. adım:** indirme hello projeden [Azure Cosmos DB performans testi örneği](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), veya çatalı hello GitHub depo.</span><span class="sxs-lookup"><span data-stu-id="7a2e1-120">**Step 1:** Download hello project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), or fork hello GitHub repository.</span></span>

<span data-ttu-id="7a2e1-121">**2. adım:** EndpointUrl ve AuthorizationKey, CollectionThroughput ve DocumentTemplate (App.config dosyasında isteğe bağlı) hello ayarlarını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7a2e1-121">**Step 2:** Modify hello settings for EndpointUrl, AuthorizationKey, CollectionThroughput and DocumentTemplate (optional) in App.config.</span></span>

> [!NOTE]
> <span data-ttu-id="7a2e1-122">Yüksek verimlilik koleksiyonlarla sağlamadan önce lütfen toohello bakın [Fiyatlandırma sayfasında](https://azure.microsoft.com/pricing/details/cosmos-db/) tooestimate hello maliyetleri koleksiyon başına.</span><span class="sxs-lookup"><span data-stu-id="7a2e1-122">Before provisioning collections with high throughput, please refer toohello [Pricing Page](https://azure.microsoft.com/pricing/details/cosmos-db/) tooestimate hello costs per collection.</span></span> <span data-ttu-id="7a2e1-123">Azure Cosmos DB faturaları depolama ve işleme silerek veya test sonra Azure Cosmos DB koleksiyonlarınızı hello verimini azaltmayı maliyetleri kaydedebilmeniz için bağımsız olarak bir saatlik olarak.</span><span class="sxs-lookup"><span data-stu-id="7a2e1-123">Azure Cosmos DB bills storage and throughput independently on an hourly basis, so you can save costs by deleting or lowering hello throughput of your Azure Cosmos DB collections after testing.</span></span>
> 
> 

<span data-ttu-id="7a2e1-124">**3. adım:** derleyip hello komut satırından hello konsol uygulamasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7a2e1-124">**Step 3:** Compile and run hello console app from hello command line.</span></span> <span data-ttu-id="7a2e1-125">Merhaba aşağıdaki gibi bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="7a2e1-125">You should see output like hello following:</span></span>

    Summary:
    ---------------------------------------------------------------------
    Endpoint: https://docdb-scale-demo.documents.azure.com:443/
    Collection : db.testdata at 50000 request units per second
    Document Template*: Player.json
    Degree of parallelism*: 500
    ---------------------------------------------------------------------

    DocumentDBBenchmark starting...
    Creating database db
    Creating collection testdata
    Creating metric collection metrics
    Retrying after sleeping for 00:03:34.1720000
    Starting Inserts with 500 tasks
    Inserted 661 docs @ 656 writes/s, 6860 RU/s (18B max monthly 1KB reads)
    Inserted 6505 docs @ 2668 writes/s, 27962 RU/s (72B max monthly 1KB reads)
    Inserted 11756 docs @ 3240 writes/s, 33957 RU/s (88B max monthly 1KB reads)
    Inserted 17076 docs @ 3590 writes/s, 37627 RU/s (98B max monthly 1KB reads)
    Inserted 22106 docs @ 3748 writes/s, 39281 RU/s (102B max monthly 1KB reads)
    Inserted 28430 docs @ 3902 writes/s, 40897 RU/s (106B max monthly 1KB reads)
    Inserted 33492 docs @ 3928 writes/s, 41168 RU/s (107B max monthly 1KB reads)
    Inserted 38392 docs @ 3963 writes/s, 41528 RU/s (108B max monthly 1KB reads)
    Inserted 43371 docs @ 4012 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 48477 docs @ 4035 writes/s, 42282 RU/s (110B max monthly 1KB reads)
    Inserted 53845 docs @ 4088 writes/s, 42845 RU/s (111B max monthly 1KB reads)
    Inserted 59267 docs @ 4138 writes/s, 43364 RU/s (112B max monthly 1KB reads)
    Inserted 64703 docs @ 4197 writes/s, 43981 RU/s (114B max monthly 1KB reads)
    Inserted 70428 docs @ 4216 writes/s, 44181 RU/s (115B max monthly 1KB reads)
    Inserted 75868 docs @ 4247 writes/s, 44505 RU/s (115B max monthly 1KB reads)
    Inserted 81571 docs @ 4280 writes/s, 44852 RU/s (116B max monthly 1KB reads)
    Inserted 86271 docs @ 4273 writes/s, 44783 RU/s (116B max monthly 1KB reads)
    Inserted 91993 docs @ 4299 writes/s, 45056 RU/s (117B max monthly 1KB reads)
    Inserted 97469 docs @ 4292 writes/s, 44984 RU/s (117B max monthly 1KB reads)
    Inserted 99736 docs @ 4192 writes/s, 43930 RU/s (114B max monthly 1KB reads)
    Inserted 99997 docs @ 4013 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 100000 docs @ 3846 writes/s, 40304 RU/s (104B max monthly 1KB reads)

    Summary:
    ---------------------------------------------------------------------
    Inserted 100000 docs @ 3834 writes/s, 40180 RU/s (104B max monthly 1KB reads)
    ---------------------------------------------------------------------
    DocumentDBBenchmark completed successfully.


<span data-ttu-id="7a2e1-126">**(Gerekiyorsa) 4. adım:** bildirilen hello işleme (RU/s) hello aracından hello aynı ya da hello sağlanan işleme hello koleksiyonunun daha yüksek olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7a2e1-126">**Step 4 (if necessary):** hello throughput reported (RU/s) from hello tool should be hello same or higher than hello provisioned throughput of hello collection.</span></span> <span data-ttu-id="7a2e1-127">Aksi durumda, artan hello DegreeOfParallelism küçük artışlarla hello sınırına ulaştığında yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="7a2e1-127">If not, increasing hello DegreeOfParallelism in small increments may help you reach hello limit.</span></span> <span data-ttu-id="7a2e1-128">İstemci uygulamanızı Hello akışından plateaus, üzerinde birden çok örneğini hello uygulama başlatma aynı hello veya farklı makinelerde sağlanan hello sınırı farklı örnekleri arasında hello ulaşmak yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="7a2e1-128">If hello throughput from your client app plateaus, launching multiple instances of hello app on hello same or different machines will help you reach hello provisioned limit across hello different instances.</span></span> <span data-ttu-id="7a2e1-129">Bu adım yardıma gereksinim duyarsanız, Lütfen bir e-posta yazma tooaskcosmosdb@microsoft.com veya bir destek bileti hello gelen dosya [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7a2e1-129">If you need help with this step, please, write an email tooaskcosmosdb@microsoft.com or file a support ticket from hello [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="7a2e1-130">Çalışan hello uygulama olduktan sonra farklı deneyebilirsiniz [ilkeleri dizin](indexing-policies.md) ve [tutarlılık düzeylerini](consistency-levels.md) toounderstand üretilen iş ve gecikmeyi üzerindeki etkilerini.</span><span class="sxs-lookup"><span data-stu-id="7a2e1-130">Once you have hello app running, you can try different [Indexing policies](indexing-policies.md) and [Consistency levels](consistency-levels.md) toounderstand their impact on throughput and latency.</span></span> <span data-ttu-id="7a2e1-131">Ayrıca hello kaynak kodu gözden geçirin ve benzer yapılandırmaları tooyour kendi test paketleri ya da üretim uygulamaları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="7a2e1-131">You can also review hello source code and implement similar configurations tooyour own test suites or production applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a2e1-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7a2e1-132">Next steps</span></span>
<span data-ttu-id="7a2e1-133">Bu makalede, nasıl performansı ve ölçeği Cosmos DB bir .NET konsol uygulaması kullanarak test gerçekleştirebileceğiniz en arama.</span><span class="sxs-lookup"><span data-stu-id="7a2e1-133">In this article, we looked at how you can perform performance and scale testing with Cosmos DB using a .NET console app.</span></span> <span data-ttu-id="7a2e1-134">Azure Cosmos DB ile çalışma hakkında ek bilgi için lütfen aşağıdaki toohello bağlantılara bakın.</span><span class="sxs-lookup"><span data-stu-id="7a2e1-134">Please refer toohello links below for additional information on working with Azure Cosmos DB.</span></span>

* [<span data-ttu-id="7a2e1-135">Azure Cosmos DB performans örnek testi</span><span class="sxs-lookup"><span data-stu-id="7a2e1-135">Azure Cosmos DB performance testing sample</span></span>](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)
* [<span data-ttu-id="7a2e1-136">İstemci yapılandırma seçenekleri tooimprove Azure Cosmos DB performansı</span><span class="sxs-lookup"><span data-stu-id="7a2e1-136">Client configuration options tooimprove Azure Cosmos DB performance</span></span>](performance-tips.md)
* [<span data-ttu-id="7a2e1-137">Sunucu tarafı Azure Cosmos DB'de bölümlendirme</span><span class="sxs-lookup"><span data-stu-id="7a2e1-137">Server-side partitioning in Azure Cosmos DB</span></span>](partition-data.md)


