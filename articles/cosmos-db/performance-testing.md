---
title: "Azure Cosmos DB ölçek ve performans testi | Microsoft Docs"
description: "Ölçek ve performans ile Azure Cosmos DB testi gerçekleştirmek öğrenin"
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
ms.openlocfilehash: b5a1edd08819e82437c5b22d8eb131665d7c9645
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="performance-and-scale-testing-with-azure-cosmos-db"></a><span data-ttu-id="63a17-104">Performansı ve ölçeği Azure Cosmos DB ile test etme</span><span class="sxs-lookup"><span data-stu-id="63a17-104">Performance and scale testing with Azure Cosmos DB</span></span>
<span data-ttu-id="63a17-105">Performans ve ölçek testi adımdır bir anahtar uygulama geliştirme.</span><span class="sxs-lookup"><span data-stu-id="63a17-105">Performance and scale testing is a key step in application development.</span></span> <span data-ttu-id="63a17-106">Birçok uygulama için veritabanı katmanı genel performans ve ölçeklenebilirlik üzerinde önemli bir etkisi vardır ve bu nedenle performans testi için kritik bir bileşen.</span><span class="sxs-lookup"><span data-stu-id="63a17-106">For many applications, the database tier has a significant impact on the overall performance and scalability, and is therefore a critical component of performance testing.</span></span> <span data-ttu-id="63a17-107">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) amaca esnek ölçek ve tahmin edilebilir performans ve bu nedenle yüksek performanslı veritabanı katmanı gereken uygulamalar için harika bir uygun değil.</span><span class="sxs-lookup"><span data-stu-id="63a17-107">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is purpose-built for elastic scale and predictable performance, and therefore a great fit for applications that need a high-performance database tier.</span></span> 

<span data-ttu-id="63a17-108">Bu makale, kendi Cosmos DB iş yükleri için performansı test paketleri uygulamadan veya yüksek performanslı uygulama senaryoları için Cosmos DB değerlendirme geliştiriciler için bir başvurudur.</span><span class="sxs-lookup"><span data-stu-id="63a17-108">This article is a reference for developers implementing performance test suites for their Cosmos DB workloads, or evaluating Cosmos DB for high-performance application scenarios.</span></span> <span data-ttu-id="63a17-109">Yalıtılmış performans veritabanını öncelikle sınama odaklanır, ancak aynı zamanda üretim uygulamaları için en iyi yöntemleri içerir.</span><span class="sxs-lookup"><span data-stu-id="63a17-109">It focuses primarily on isolated performance testing of the database, but also includes best practices for production applications.</span></span>

<span data-ttu-id="63a17-110">Bu makaleyi okuduktan sonra aşağıdaki soruları yanıtlayın mümkün olacaktır:</span><span class="sxs-lookup"><span data-stu-id="63a17-110">After reading this article, you will be able to answer the following questions:</span></span>   

* <span data-ttu-id="63a17-111">Cosmos DB performans testi için bir örnek .NET istemci uygulaması nereden bulabilirim?</span><span class="sxs-lookup"><span data-stu-id="63a17-111">Where can I find a sample .NET client application for performance testing of Cosmos DB?</span></span> 
* <span data-ttu-id="63a17-112">My istemci uygulamasından nasıl Cosmos DB ile yüksek işleme düzeyleri elde?</span><span class="sxs-lookup"><span data-stu-id="63a17-112">How do I achieve high throughput levels with Cosmos DB from my client application?</span></span>

<span data-ttu-id="63a17-113">Kodu ile çalışmaya başlamak için lütfen projeden indirin [Azure Cosmos DB performans testi örneği](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="63a17-113">To get started with code, please download the project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span></span> 

> [!NOTE]
> <span data-ttu-id="63a17-114">Bu uygulama amacı, az sayıda istemci makineleri ile daha iyi performans Cosmos DB dışında ayıklanacağı en iyi yöntemler göstermektir.</span><span class="sxs-lookup"><span data-stu-id="63a17-114">The goal of this application is to demonstrate best practices for extracting better performance out of Cosmos DB with a small number of client machines.</span></span> <span data-ttu-id="63a17-115">Bu genişlediğinden ölçeklendirebilirsiniz hizmet yoğun kapasitesini göstermek için yapılmadı.</span><span class="sxs-lookup"><span data-stu-id="63a17-115">This was not made to demonstrate the peak capacity of the service, which can scale limitlessly.</span></span>
> 
> 

<span data-ttu-id="63a17-116">Cosmos DB performansını artırmak istemci tarafı yapılandırma seçenekleri arıyorsanız bkz [Azure Cosmos DB performans ipuçları](performance-tips.md).</span><span class="sxs-lookup"><span data-stu-id="63a17-116">If you're looking for client-side configuration options to improve Cosmos DB performance, see [Azure Cosmos DB performance tips](performance-tips.md).</span></span>

## <a name="run-the-performance-testing-application"></a><span data-ttu-id="63a17-117">Performans uygulama testi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="63a17-117">Run the performance testing application</span></span>
<span data-ttu-id="63a17-118">Başlamak için en hızlı derlemek ve aşağıdaki adımları açıklandığı gibi .NET örnek aşağıda çalıştırmak için yoludur.</span><span class="sxs-lookup"><span data-stu-id="63a17-118">The quickest way to get started is to compile and run the .NET sample below, as described in the steps below.</span></span> <span data-ttu-id="63a17-119">Ayrıca, kaynak kodu gözden geçirin ve benzer yapılandırmaları için kendi istemci uygulamalarını uygulamak.</span><span class="sxs-lookup"><span data-stu-id="63a17-119">You can also review the source code and implement similar configurations to your own client applications.</span></span>

<span data-ttu-id="63a17-120">**1. adım:** projesinden indirmeniz [Azure Cosmos DB performans testi örneği](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), veya GitHub depoyu çatallaştırmanız.</span><span class="sxs-lookup"><span data-stu-id="63a17-120">**Step 1:** Download the project from [Azure Cosmos DB Performance Testing Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), or fork the GitHub repository.</span></span>

<span data-ttu-id="63a17-121">**2. adım:** EndpointUrl ve AuthorizationKey, CollectionThroughput ve DocumentTemplate (App.config dosyasında isteğe bağlı) ayarlarını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="63a17-121">**Step 2:** Modify the settings for EndpointUrl, AuthorizationKey, CollectionThroughput and DocumentTemplate (optional) in App.config.</span></span>

> [!NOTE]
> <span data-ttu-id="63a17-122">Yüksek verimlilik koleksiyonlarla sağlamadan önce lütfen [Fiyatlandırma sayfasında](https://azure.microsoft.com/pricing/details/cosmos-db/) koleksiyon başına maliyetleri tahmin etme.</span><span class="sxs-lookup"><span data-stu-id="63a17-122">Before provisioning collections with high throughput, please refer to the [Pricing Page](https://azure.microsoft.com/pricing/details/cosmos-db/) to estimate the costs per collection.</span></span> <span data-ttu-id="63a17-123">Azure Cosmos DB faturaları depolama ve işleme silerek veya test sonra Azure Cosmos DB koleksiyonlarınızı verimini azaltmayı maliyetleri kaydedebilmeniz için bağımsız olarak bir saatlik olarak.</span><span class="sxs-lookup"><span data-stu-id="63a17-123">Azure Cosmos DB bills storage and throughput independently on an hourly basis, so you can save costs by deleting or lowering the throughput of your Azure Cosmos DB collections after testing.</span></span>
> 
> 

<span data-ttu-id="63a17-124">**3. adım:** derleyin ve komut satırından konsol uygulamasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="63a17-124">**Step 3:** Compile and run the console app from the command line.</span></span> <span data-ttu-id="63a17-125">Aşağıdakine benzer bir çıktı görmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="63a17-125">You should see output like the following:</span></span>

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


<span data-ttu-id="63a17-126">**(Gerekiyorsa) 4. adım:** bildirilen üretilen işi (RU/s) aracından aynı olması gerekir ya da daha yüksek sağlanan işleme koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="63a17-126">**Step 4 (if necessary):** The throughput reported (RU/s) from the tool should be the same or higher than the provisioned throughput of the collection.</span></span> <span data-ttu-id="63a17-127">Aksi durumda, küçük artışlarla DegreeOfParallelism artırma sınırına ulaştığında yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="63a17-127">If not, increasing the DegreeOfParallelism in small increments may help you reach the limit.</span></span> <span data-ttu-id="63a17-128">İstemci uygulamanızı akışından plateaus, birden çok örneğini aynı veya farklı makinelerde uygulama başlatma, farklı örneklerinde sağlanan sınırına ulaştığında yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="63a17-128">If the throughput from your client app plateaus, launching multiple instances of the app on the same or different machines will help you reach the provisioned limit across the different instances.</span></span> <span data-ttu-id="63a17-129">Bu adım yardıma gereksinim duyarsanız, Lütfen bir e-posta yazma askcosmosdb@microsoft.com veya bir destek bileti gelen dosya [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="63a17-129">If you need help with this step, please, write an email to askcosmosdb@microsoft.com or file a support ticket from the [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="63a17-130">Uygulamayı oluşturduktan sonra farklı deneyebilirsiniz [ilkeleri dizin](indexing-policies.md) ve [tutarlılık düzeylerini](consistency-levels.md) üretilen iş ve gecikmeyi üzerindeki etkilerini anlamak için.</span><span class="sxs-lookup"><span data-stu-id="63a17-130">Once you have the app running, you can try different [Indexing policies](indexing-policies.md) and [Consistency levels](consistency-levels.md) to understand their impact on throughput and latency.</span></span> <span data-ttu-id="63a17-131">Kaynak kodu gözden geçirmek ve kendi test paketleri ya da üretim uygulamaları için benzer yapılandırmaları uygulamak.</span><span class="sxs-lookup"><span data-stu-id="63a17-131">You can also review the source code and implement similar configurations to your own test suites or production applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="63a17-132">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="63a17-132">Next steps</span></span>
<span data-ttu-id="63a17-133">Bu makalede, nasıl performansı ve ölçeği Cosmos DB bir .NET konsol uygulaması kullanarak test gerçekleştirebileceğiniz en arama.</span><span class="sxs-lookup"><span data-stu-id="63a17-133">In this article, we looked at how you can perform performance and scale testing with Cosmos DB using a .NET console app.</span></span> <span data-ttu-id="63a17-134">Lütfen Azure Cosmos DB ile çalışma hakkında ek bilgi için aşağıdaki bağlantılara bakın.</span><span class="sxs-lookup"><span data-stu-id="63a17-134">Please refer to the links below for additional information on working with Azure Cosmos DB.</span></span>

* [<span data-ttu-id="63a17-135">Azure Cosmos DB performans örnek testi</span><span class="sxs-lookup"><span data-stu-id="63a17-135">Azure Cosmos DB performance testing sample</span></span>](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)
* [<span data-ttu-id="63a17-136">Azure Cosmos DB performansını artırmak için istemci yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="63a17-136">Client configuration options to improve Azure Cosmos DB performance</span></span>](performance-tips.md)
* [<span data-ttu-id="63a17-137">Sunucu tarafı Azure Cosmos DB'de bölümlendirme</span><span class="sxs-lookup"><span data-stu-id="63a17-137">Server-side partitioning in Azure Cosmos DB</span></span>](partition-data.md)


