---
title: "Azure CosmosDB: İstek birimleri (RU/m) dakikada | Microsoft Docs"
description: "Dakika başına istek birimleri yararlanarak maliyetini azaltmak öğrenin."
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 72d60d5656ad664e42a848fc9b372cb09e49b888
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="request-units-per-minute-in-azure-cosmos-db"></a><span data-ttu-id="e05fd-103">İstek birimleri dakikada Azure Cosmos veritabanı</span><span class="sxs-lookup"><span data-stu-id="e05fd-103">Request units per minute in Azure Cosmos DB</span></span>

<span data-ttu-id="e05fd-104">Azure Cosmos DB hızlı ve tahmin edilebilir performansı ve ölçeği uygulamanızın büyüme sorunsuz bir şekilde birlikte yardımcı olmak için tasarlanmıştır.</span><span class="sxs-lookup"><span data-stu-id="e05fd-104">Azure Cosmos DB is designed to help you achieve a fast, predictable performance and scale seamlessly along with your application’s growth.</span></span> <span data-ttu-id="e05fd-105">Her iki saniyede ve dakika başına (RU/m) ayrıntı Cosmos DB kapsayıcısı üzerinde üretilen işi sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e05fd-105">You can provision throughput on a Cosmos DB container at both, per-second and at per-minute (RU/m) granularities.</span></span> <span data-ttu-id="e05fd-106">Dakika başına ayrıntı düzeyinde sağlanan aktarım hızı, saniye başına ayrıntı düzeyinde iş yükünde oluşan beklenmedik artışları yönetmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e05fd-106">The provisioned throughput at per-minute granularity is used to manage unexpected spikes in the workload occurring at a per-second granularity.</span></span> 

<span data-ttu-id="e05fd-107">Bu makalede, istek birimi (RU/m) dakikada sağlama nasıl çalıştığını genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="e05fd-107">This article provides an overview of how the provisioning of Request Unit per Minute (RU/m) works.</span></span> <span data-ttu-id="e05fd-108">Hedef RU/m sağlama ile aklınızda öngörülebilir bir performans (özellikle işletimsel verilerinizi en üstünde analytics çalıştırmanız gerekiyorsa) öngörülemeyen gereksinimlerini ve spiky iş yükleri çevresinde sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="e05fd-108">The goal in mind with provisioning of RU/m is to provide a predictable performance around unpredictable needs (especially if you need to run analytics on top of your operational data) and spiky workloads.</span></span> <span data-ttu-id="e05fd-109">Gönül rahatlığı ile hızlı bir şekilde ölçeklendirebilirsiniz şekilde sağladıkları daha fazla verimlilik tüketen müşterilerimizin olmasını istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="e05fd-109">We want to have our customers consume more the throughput they provision so they can scale quickly with peace of mind.</span></span>

<span data-ttu-id="e05fd-110">Bu makaleyi okuduktan sonra aşağıdaki soruları yanıtlayın mümkün olacaktır:</span><span class="sxs-lookup"><span data-stu-id="e05fd-110">After reading this article, you will be able to answer the following questions:</span></span>

* <span data-ttu-id="e05fd-111">Bir istek birimi dakikada nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="e05fd-111">How does a Request Unit per Minute work?</span></span>
* <span data-ttu-id="e05fd-112">İstek birimi / dakika ve saniye başına istek birimi arasındaki fark nedir?</span><span class="sxs-lookup"><span data-stu-id="e05fd-112">What is the difference between Request Unit per Minute and Request Unit per Second?</span></span>
* <span data-ttu-id="e05fd-113">RU/m sağlamak nasıl?</span><span class="sxs-lookup"><span data-stu-id="e05fd-113">How to provision RU/m?</span></span>
* <span data-ttu-id="e05fd-114">Hangi senaryosunda ı istek birimi dakikada sağlama düşünün?</span><span class="sxs-lookup"><span data-stu-id="e05fd-114">Under which scenario shall I consider provisioning Request Unit per Minute?</span></span>
* <span data-ttu-id="e05fd-115">Portal ölçümleri my maliyet ve performansı iyileştirmek için nasıl kullanılacağını?</span><span class="sxs-lookup"><span data-stu-id="e05fd-115">How to use the portal metrics to optimize my cost and performance?</span></span>
* <span data-ttu-id="e05fd-116">İstek türü RU/m bütçenizi tüketebileceği tanımla</span><span class="sxs-lookup"><span data-stu-id="e05fd-116">Define which type of request can consume your RU/m budget?</span></span>

## <a name="provisioning-request-units-per-minute-rum"></a><span data-ttu-id="e05fd-117">İstek birimleri (RU/m) dakikada sağlama</span><span class="sxs-lookup"><span data-stu-id="e05fd-117">Provisioning request units per minute (RU/m)</span></span>

<span data-ttu-id="e05fd-118">İkinci bazda (RU/s) Azure Cosmos DB sağladığınızda, üretilen iş o saniye içinde sağlanan kapasite aştı değil, düşük gecikme isteğiniz başarılı garantisi alın.</span><span class="sxs-lookup"><span data-stu-id="e05fd-118">When you provision Azure Cosmos DB at the second granularity (RU/s), you get the guarantee that your request succeeds at a low latency if your throughput has not exceeded the capacity provisioned within that second.</span></span> <span data-ttu-id="e05fd-119">RU/m ile bu dakika içinde isteğiniz başarılı garantisi MINUTE ayrıntı altındadır.</span><span class="sxs-lookup"><span data-stu-id="e05fd-119">With RU/m, the granularity is at the minute with the guarantee that your request succeeds within that minute.</span></span> <span data-ttu-id="e05fd-120">Sistemleri emniyeti için ile karşılaştırıldığında, biz elde performans tahmin edilebilir ve üzerinde planlayabilirsiniz emin olun.</span><span class="sxs-lookup"><span data-stu-id="e05fd-120">Compared to bursting systems, we make sure that the performance you get is predictable and you can plan on it.</span></span>

<span data-ttu-id="e05fd-121">Basit works sağlama dakikada yoludur:</span><span class="sxs-lookup"><span data-stu-id="e05fd-121">The way per minute provisioning works is simple:</span></span>

* <span data-ttu-id="e05fd-122">RU/m saatlik ve RU/s ek olarak faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="e05fd-122">RU/m is billed hourly and in addition to RU/s.</span></span> <span data-ttu-id="e05fd-123">Daha fazla ayrıntı için lütfen Azure Cosmos DB ziyaret [fiyatlandırma sayfası](https://aka.ms/acdbpricing).</span><span class="sxs-lookup"><span data-stu-id="e05fd-123">For more details, please visit Azure Cosmos DB [pricing page](https://aka.ms/acdbpricing).</span></span>
* <span data-ttu-id="e05fd-124">Koleksiyon düzeyinde RU/m etkinleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="e05fd-124">RU/m can be enabled at collection level.</span></span> <span data-ttu-id="e05fd-125">Bu yapılabilir SDK'ları (Node.js, Java ya da .net) veya portal üzerinden (aynı zamanda MongoDB API iş yükleri içerir)</span><span class="sxs-lookup"><span data-stu-id="e05fd-125">That can be done through the SDKs (Node.js, Java, or .Net) or through the portal (also include MongoDB API workloads)</span></span>
* <span data-ttu-id="e05fd-126">RU/m etkinleştirildiğinde her 100 RU/hazırlandı s için sağlanan 1.000 RU/m ayrıca Al (10 x orandır)</span><span class="sxs-lookup"><span data-stu-id="e05fd-126">When RU/m is enabled, for every 100 RU/s provisioned, you also get 1,000 RU/m provisioned (the ratio is 10x)</span></span>
* <span data-ttu-id="e05fd-127">Yalnızca aştınız varsa, RU/m sağlama sırasında belirtilen ikinci bir, bir istek birimi kullanır, bu saniye içinde ikinci sağlama başına</span><span class="sxs-lookup"><span data-stu-id="e05fd-127">At a given second, a request unit consumes your RU/m provisioning only if you have exceeded your per second provisioning within that second</span></span>
* <span data-ttu-id="e05fd-128">(UTC) 60 saniye dönemi sona erince sağlama dakika başına refilled</span><span class="sxs-lookup"><span data-stu-id="e05fd-128">Once the 60-second period (UTC) ends, the per minute provisioning is refilled</span></span>
* <span data-ttu-id="e05fd-129">RU/m, yalnızca bir en fazla 5000 RU/s bölüm başına sağlama koleksiyonlar için etkinleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="e05fd-129">RU/m can be enabled only for collections with a maximum provisioning of 5,000 RU/s per partition.</span></span> <span data-ttu-id="e05fd-130">Üretilen iş gereksinimlerinize ölçeği ve bölüm başına sağlama böyle bir yüksek düzeyde varsa, bir uyarı iletisi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="e05fd-130">If you scale your throughput needs and have such a high level of provisioning per partition, you will get a warning message</span></span>

<span data-ttu-id="e05fd-131">Aşağıda bir müşteri 10kRU/s 100kRU/m ile sağlayabilirsiniz somut bir örnek %73 90 saniyelik süre 10.000 sahip bir koleksiyonun üzerinde aracılığıyla (50kRU/sn) en yoğun RU/s ve sağlanan 100.000 RU/m sağlama karşı Maliyet: kaydediliyor.</span><span class="sxs-lookup"><span data-stu-id="e05fd-131">Below is a concrete example, in which a customer can provision 10kRU/s with 100kRU/m, saving 73% in cost against provisioning for peak (at 50kRU/sec) through a 90-second period on a collection that has 10,000 RU/s and 100,000 RU/m provisioned:</span></span>

* <span data-ttu-id="e05fd-132">1 saniye: RU/m bütçe 100.000 sırasında ayarlanır</span><span class="sxs-lookup"><span data-stu-id="e05fd-132">1st second: The RU/m budget is set at 100,000</span></span>
* <span data-ttu-id="e05fd-133">3 ikinci: Bu saniye boyunca istek birimi tüketiminin edildi 11,010 RUs, RU/s sağlama yukarıda 1,010 RUs.</span><span class="sxs-lookup"><span data-stu-id="e05fd-133">3rd second: During that second the consumption of Request Unit was 11,010 RUs, 1,010 RUs above the RU/s provisioning.</span></span> <span data-ttu-id="e05fd-134">Bu nedenle, 1,010 RUs RU/m bütçeden azaltılır.</span><span class="sxs-lookup"><span data-stu-id="e05fd-134">Therefore, 1,010 RUs are deducted from the RU/m budget.</span></span> <span data-ttu-id="e05fd-135">Sonraki 57 saniye cinsinden RU/m bütçe 98,990 RUs mevcuttur</span><span class="sxs-lookup"><span data-stu-id="e05fd-135">98,990 RUs are available for the next 57 seconds in the RU/m budget</span></span>
* <span data-ttu-id="e05fd-136">29 ikinci: Bu saniye boyunca büyük bir aşırı oldu (> 4 x saniyede sağlama daha yüksek) ve istek birimi tüketiminin 46,920 RUs.</span><span class="sxs-lookup"><span data-stu-id="e05fd-136">29th second: During that second, a large spike happened (>4x higher than provisioning per second) and the consumption of Request Unit was 46,920 RUs.</span></span> <span data-ttu-id="e05fd-137">36,920 RUs 92,323 RUs (28 saniye) 55,403 RUs (29 saniye) bırakılan RU/m bütçesi kesinti</span><span class="sxs-lookup"><span data-stu-id="e05fd-137">36,920 RUs are deducted from the RU/m budget that dropped from 92,323 RUs (28th second) to 55,403 RUs (29th second)</span></span>
* <span data-ttu-id="e05fd-138">61st ikinci: RU/m bütçe 100.000 RUs geri ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="e05fd-138">61st second: RU/m budget is set back to 100,000 RUs.</span></span>
 
![Azure Cosmos DB sağlama ve tüketimini gösteren grafik](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute.png)

## <a name="specifying-request-unit-capacity-with-rum"></a><span data-ttu-id="e05fd-140">İstek birimi kapasite RU/m ile belirtme</span><span class="sxs-lookup"><span data-stu-id="e05fd-140">Specifying request unit capacity with RU/m</span></span>

<span data-ttu-id="e05fd-141">Bir Azure Cosmos DB koleksiyonunu oluştururken numarası belirtin (RU saniye başına) saniyede istek birimlerinin koleksiyon için ayrılmış istiyor.</span><span class="sxs-lookup"><span data-stu-id="e05fd-141">When creating an Azure Cosmos DB collection, you specify the number of request units per second (RU per second) you want reserved for the collection.</span></span> <span data-ttu-id="e05fd-142">Dakika başına RU eklemek isteyip istemediğinizi de karar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e05fd-142">You can also decide if you want to add RU per minute.</span></span> <span data-ttu-id="e05fd-143">Bu, Portal veya SDK yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="e05fd-143">This can be done through the Portal or the SDK.</span></span> 

### <a name="through-the-portal"></a><span data-ttu-id="e05fd-144">Portalı aracılığıyla</span><span class="sxs-lookup"><span data-stu-id="e05fd-144">Through the Portal</span></span>

<span data-ttu-id="e05fd-145">Yalnızca etkinleştirme veya dakikada RU devre dışı bırakma bir koleksiyonu sağlamada gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e05fd-145">Enabling or disabling RU per minute simply requires a click when provisioning a collection.</span></span> 

 ![Azure portalında RU/m ayarlama gösteren ekran görüntüsü](./media/request-units-per-minute/azure-cosmos-db-request-unit-per-minute-portal.png)

### <a name="through-the-sdk"></a><span data-ttu-id="e05fd-147">SDK aracılığıyla</span><span class="sxs-lookup"><span data-stu-id="e05fd-147">Through the SDK</span></span>
<span data-ttu-id="e05fd-148">İlk olarak, bu RU/m yalnızca aşağıdaki SDK'ları için kullanılabilir olduğunu dikkate almak önemlidir:</span><span class="sxs-lookup"><span data-stu-id="e05fd-148">First, this is important to note that RU/m is only available for the following SDKs:</span></span>

* <span data-ttu-id="e05fd-149">.NET 1.14.0</span><span class="sxs-lookup"><span data-stu-id="e05fd-149">.Net 1.14.0</span></span>
* <span data-ttu-id="e05fd-150">Java 1.11.0</span><span class="sxs-lookup"><span data-stu-id="e05fd-150">Java 1.11.0</span></span>
* <span data-ttu-id="e05fd-151">Node.js 1.12.0</span><span class="sxs-lookup"><span data-stu-id="e05fd-151">Node.js 1.12.0</span></span>
* <span data-ttu-id="e05fd-152">Python 2.2.0</span><span class="sxs-lookup"><span data-stu-id="e05fd-152">Python 2.2.0</span></span>

<span data-ttu-id="e05fd-153">.NET SDK kullanarak dakika başına ikinci ve 30.000 isteği birim başına 3000 isteği birim içeren bir koleksiyon oluşturmak için bir kod parçacığı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="e05fd-153">Here is a code snippet for creating a collection with 3,000 request units per second and 30,000 request units per minute using the .NET SDK:</span></span>

```csharp
// Create a collection with RU/m enabled
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

// Set the throughput to 3,000 request units per second which will give you 30,000 request units per minute as the RU/m budget
await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000, OfferEnableRUPerMinuteThroughput = true });
```

<span data-ttu-id="e05fd-154">.NET SDK kullanarak dakikada sağlama RU olmadan saniye başına 5.000 isteği birim için bir koleksiyon verimini değiştirmek için bir kod parçacığı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="e05fd-154">Here is a code snippet for changing the throughput of a collection to 5,000 request units per second without provisioning RU per minute using the .NET SDK:</span></span>

```csharp
// Get the current offer
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set the throughput to 5000 request units per second without RU/m enabled (the last parameter to OfferV2 constructor below)
OfferV2 offerV2 = new OfferV2(offer, 5000, false);

// Now persist these changes to the database by replacing the original resource
await client.ReplaceOfferAsync(offerV2);
```

## <a name="good-fit-scenarios"></a><span data-ttu-id="e05fd-155">İyi senaryoları Sığdır</span><span class="sxs-lookup"><span data-stu-id="e05fd-155">Good fit scenarios</span></span>

<span data-ttu-id="e05fd-156">Bu bölümde, dakika başına istek birimleri etkinleştirmek için iyi bir tercihtir senaryoların genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="e05fd-156">In this section, we provide an overview of scenarios that are a good fit for enabling request units per minute.</span></span>

<span data-ttu-id="e05fd-157">**Geliştirme ve Test Ortamı:** iyi sığacak şekilde.</span><span class="sxs-lookup"><span data-stu-id="e05fd-157">**Dev/Test environment:** Good fit.</span></span> <span data-ttu-id="e05fd-158">Farklı iş yükleri ile uygulamanızı test ediyorsanız bu aşamada geliştirme aşamasında RU/m esneklik sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="e05fd-158">During the development stage, if you are testing your application with different workloads, RU/m can provide the flexibility at this stage.</span></span> <span data-ttu-id="e05fd-159">Sırada [öykünücüsü](local-emulator.md) Azure Cosmos DB test etmek için harika ücretsiz bir araçtır.</span><span class="sxs-lookup"><span data-stu-id="e05fd-159">While the [emulator](local-emulator.md) is a great free tool to test Azure Cosmos DB.</span></span> <span data-ttu-id="e05fd-160">Ancak bulut ortamında başlatmak istiyorsanız, geçici performans gereksinimlerinizi RU/m ile büyük bir esneklik gerekir.</span><span class="sxs-lookup"><span data-stu-id="e05fd-160">However if you want to start in a cloud environment, you will have a great flexibility with RU/m for your adhoc performance needs.</span></span> <span data-ttu-id="e05fd-161">Geliştirme, daha az düşünmeye ilk performans gereksinimleri hakkında daha fazla süre beklemesini.</span><span class="sxs-lookup"><span data-stu-id="e05fd-161">You will spend more time developing, less worrying about performance needs at first.</span></span> <span data-ttu-id="e05fd-162">Biz minimum sağlama RU/s ile başlamanızı öneririz ve RU/m etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e05fd-162">We recommend starting with the minimum RU/s provisioning and enable RU/m.</span></span>

<span data-ttu-id="e05fd-163">**Öngörülemeyen, spiky, dakika ayrıntı düzeyi gerekiyor:** iyi sığacak – tasarrufları: % 25 75.</span><span class="sxs-lookup"><span data-stu-id="e05fd-163">**Unpredictable, spiky, minute granularity needs:** Good fit – Savings: 25-75%.</span></span> <span data-ttu-id="e05fd-164">Biz RU/m ve çoğu üretim senaryoları büyük geliştirme olan bu gruba gördünüz.</span><span class="sxs-lookup"><span data-stu-id="e05fd-164">We have seen large improvement from RU/m and most production scenarios are into that group.</span></span> <span data-ttu-id="e05fd-165">Sisteminiz aynı anda toplu ekleme yaptığında, çalışmakta olan sorgulara varsa birkaç kez bir dakika içinde depo olan bir IOT iş yükü varsa handeling spiky ihtiyaçları için ek kapasite gerekir.</span><span class="sxs-lookup"><span data-stu-id="e05fd-165">If you have an IoT workload that has spike a few times in a minute, if you have queries running when your system makes mass insert at the same time, you will need extra capacity for handeling spiky needs.</span></span> <span data-ttu-id="e05fd-166">Adım adım yaklaşımımız aşağıdaki uygulayarak kaynak gereksinimlerinizi en iyi duruma getirme öneririz.</span><span class="sxs-lookup"><span data-stu-id="e05fd-166">We recommend optimizing your resource needs by applying our step by step approach below.</span></span>

 ![5 dakikalık ayrıntı isteği tüketimini gösteren grafik](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-consumption.png)
 
 <span data-ttu-id="e05fd-168">*Şekil - RU tüketim Kıyaslama*</span><span class="sxs-lookup"><span data-stu-id="e05fd-168">*Figure - RU consumption benchmark*</span></span>

<span data-ttu-id="e05fd-169">**İçiniz rahat:** iyi sığacak – tasarrufları: % 10-20.</span><span class="sxs-lookup"><span data-stu-id="e05fd-169">**Peace of mind:** Good fit – Savings: 10-20%.</span></span> <span data-ttu-id="e05fd-170">Bazı durumlarda, yalnızca içiniz rahat olmasını istediğiniz ve olası yükselmeleri ve azaltma hakkında endişelenmeniz değil.</span><span class="sxs-lookup"><span data-stu-id="e05fd-170">Sometimes, you just want to have peace of mind and not worry about potential peaks and throttling.</span></span> <span data-ttu-id="e05fd-171">Sizin için doğru bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="e05fd-171">This feature is the right one for you.</span></span> <span data-ttu-id="e05fd-172">Bu durumda, RU/m etkinleştirme öneririz ve biraz daha düşük, ikinci sağlama başına.</span><span class="sxs-lookup"><span data-stu-id="e05fd-172">In that case, we recommend enabling RU/m and slightly lower your per second provisioning.</span></span> <span data-ttu-id="e05fd-173">Bu durumda yukarıdaki farklı olarak titizlikle, sağlama iyileştirmek denemez.</span><span class="sxs-lookup"><span data-stu-id="e05fd-173">This case is different from the above as you will not try to optimize aggressively your provisioning.</span></span> <span data-ttu-id="e05fd-174">Daha fazla olan bir "Sıfır azaltma" bakış budur.</span><span class="sxs-lookup"><span data-stu-id="e05fd-174">This is more of a “Zero Throttling” mindset you are in.</span></span>

<span data-ttu-id="e05fd-175">Adhoc gereksinimleri olan kritik işlemler: Bazı durumlarda yalnızca kritik işlemler RU/m bütçe bütçe açılmıyor şekilde erişim tüketen geçici veya önemli işlemleri daha az izin vermek için öneririz.</span><span class="sxs-lookup"><span data-stu-id="e05fd-175">Critical operations with adhoc needs: We sometimes recommend to only let critical operations access RU/m budget so the budget doesn’t get consume by adhoc or less important operations.</span></span> <span data-ttu-id="e05fd-176">Aşağıdaki bölümde, kolayca tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="e05fd-176">That can be easily defined in the section below.</span></span>

## <a name="using-the-portal-metrics-to-optimize-cost-and-performance"></a><span data-ttu-id="e05fd-177">Maliyet ve performansı en iyi duruma getirmek için portal ölçümleri kullanma</span><span class="sxs-lookup"><span data-stu-id="e05fd-177">Using the portal metrics to optimize cost and performance</span></span>

<span data-ttu-id="e05fd-178">**Önümüzdeki haftalarda size daha fazla üretilen iş gereksinimlerinizi en iyi duruma getirme RUs dakika tüketim izleme geçici içerik geliştireceksiniz.**</span><span class="sxs-lookup"><span data-stu-id="e05fd-178">**In the coming weeks, we will further develop the content around monitoring RUs minute consumption to optimize your throughput needs.**</span></span>

<span data-ttu-id="e05fd-179">Portal ölçümleri karşı RU tüketen normal RU saniye ne kadarının dakika görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e05fd-179">Through the portal metrics, you can see how much of regular RU seconds you consume versus RU minutes.</span></span> <span data-ttu-id="e05fd-180">Bu ölçümleri izleme, sağlama en iyi hale getirmenize yardımcı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e05fd-180">Monitoring these metrics should help you optimize your provisioning.</span></span> 

<span data-ttu-id="e05fd-181">Kendi yararınıza RU/m kullanma hakkında adım adım bir yaklaşım öneririz.</span><span class="sxs-lookup"><span data-stu-id="e05fd-181">We recommend a step by step approach on how to use RU/m to your advantage.</span></span> <span data-ttu-id="e05fd-182">Her adımı için bir genel bakış (bunu olabilir saat, gün, veya hatta hafta), iş yükü tam döngüsünün temsil eden RU tüketiminin olmalıdır ve ne sağlamak kullanımı hakkında Öngörüler alın.</span><span class="sxs-lookup"><span data-stu-id="e05fd-182">For each step, you should have an overview of the RU consumption representing a full cycle of your workload (it could be hours, days, or even weeks) and get insights on the utilization of what you provision.</span></span>

<span data-ttu-id="e05fd-183">Bu yaklaşım arkasında ilkesini, işleme, performans ölçütlerle eşleşen bir sağlama noktasına olabildiğince yakın gibi sağlama olmasını sağlamaktır.</span><span class="sxs-lookup"><span data-stu-id="e05fd-183">The principle behind this approach is to make your throughput provisioning as close as possible to a provisioning point that matches your performance criteria below.</span></span> 

![5 dakikalık ayrıntı isteği tüketimini gösteren grafik](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-adjust-provisioning.png)
 
<span data-ttu-id="e05fd-185">İş yükü için en iyi sağlama noktası anlamak için anlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e05fd-185">To understand the optimal provisioning point for your workload, you need to understand:</span></span>

* <span data-ttu-id="e05fd-186">Tüketim desenleri: Hayır, kesintili veya sürekli ani?</span><span class="sxs-lookup"><span data-stu-id="e05fd-186">Consumption patterns: no, infrequent or sustained spikes?</span></span> <span data-ttu-id="e05fd-187">(2 x ortalama) küçük, Orta veya büyük (> 10 x ortalama) ani?</span><span class="sxs-lookup"><span data-stu-id="e05fd-187">Small (2x average), medium, or large (>10x average) spikes?</span></span>
* <span data-ttu-id="e05fd-188">Daraltılmış istekleri yüzdesi: hızlandırma biraz varsa rahat düşündüğünüz musunuz?</span><span class="sxs-lookup"><span data-stu-id="e05fd-188">Percent of throttled requests: do you feel comfortable if you have a bit of throttling?</span></span> <span data-ttu-id="e05fd-189">Öyleyse, ne kadar?</span><span class="sxs-lookup"><span data-stu-id="e05fd-189">If so, by how much?</span></span> 

<span data-ttu-id="e05fd-190">Hedefleriniz nelerdir belirledikten sonra en iyi sağlamak için daha yakından almak mümkün olacaktır.</span><span class="sxs-lookup"><span data-stu-id="e05fd-190">Once you have identified what your goals are, you will be able to get closer to the optimal provisioning.</span></span>

<span data-ttu-id="e05fd-191">Size yardımcı olmak üzere, sağlama, RU/m tüketime dayanarak en iyi duruma getirme hakkında genel bir kılavuz sağlamak istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="e05fd-191">To assist you, we want to provide an overall guidance on how to optimize your provisioning based on your RU/m consumption.</span></span> <span data-ttu-id="e05fd-192">Bu kılavuz, tüm türdeki iş yüklerini uygulanmaz ancak özel Önizleme bilgisini temel alarak.</span><span class="sxs-lookup"><span data-stu-id="e05fd-192">This guidance doesn’t apply to all kind of workloads but is based on the private preview knowledge.</span></span> <span data-ttu-id="e05fd-193">Biz bu tür temelleri değişebilir olarak size daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="e05fd-193">We might change such baselines as we learn more:</span></span>

|<span data-ttu-id="e05fd-194">RU/m % kullanımı</span><span class="sxs-lookup"><span data-stu-id="e05fd-194">RU/m % utilization</span></span>|<span data-ttu-id="e05fd-195">RU/m kullanımını derecesini</span><span class="sxs-lookup"><span data-stu-id="e05fd-195">Degree of utilization of RU/m</span></span>|<span data-ttu-id="e05fd-196">Sağlama için Önerilen Eylemler</span><span class="sxs-lookup"><span data-stu-id="e05fd-196">Recommended actions for provisioning</span></span>|
|---|---|---|
|<span data-ttu-id="e05fd-197">0-1%</span><span class="sxs-lookup"><span data-stu-id="e05fd-197">0-1%</span></span>|<span data-ttu-id="e05fd-198">Kullanımı altında</span><span class="sxs-lookup"><span data-stu-id="e05fd-198">Under utilization</span></span>|<span data-ttu-id="e05fd-199">Daha fazla RU/m tüketmeye alt RU/s</span><span class="sxs-lookup"><span data-stu-id="e05fd-199">Lower RU/s to consume more RU/m</span></span>|
|<span data-ttu-id="e05fd-200">1-10%</span><span class="sxs-lookup"><span data-stu-id="e05fd-200">1-10%</span></span>|<span data-ttu-id="e05fd-201">Sağlıklı kullanın</span><span class="sxs-lookup"><span data-stu-id="e05fd-201">Healthy use</span></span>|<span data-ttu-id="e05fd-202">Aynı sağlama düzeyini koruyun</span><span class="sxs-lookup"><span data-stu-id="e05fd-202">Keep the same provisioning level</span></span>|
|<span data-ttu-id="e05fd-203">Yukarıdaki % 10</span><span class="sxs-lookup"><span data-stu-id="e05fd-203">Above 10%</span></span>|<span data-ttu-id="e05fd-204">Kullanımı</span><span class="sxs-lookup"><span data-stu-id="e05fd-204">Over utilization</span></span>|<span data-ttu-id="e05fd-205">Üzerinde daha az RU/m yararlanmayı RU/s artırın</span><span class="sxs-lookup"><span data-stu-id="e05fd-205">Increase RU/s to rely less on RU/m</span></span>|

## <a name="select-which-operations-can-consume-the-rum-budget"></a><span data-ttu-id="e05fd-206">Hangi işlemleri RU/m bütçe tüketebileceği seçin</span><span class="sxs-lookup"><span data-stu-id="e05fd-206">Select which operations can consume the RU/m budget</span></span>

<span data-ttu-id="e05fd-207">İsteği düzeyinde, ayrıca etkinleştirebilir/RU/m bütçe işlem türü ne olursa olsun isteğe hizmet devre dışı bırakabilir.</span><span class="sxs-lookup"><span data-stu-id="e05fd-207">At request level, you can also enable/disable RU/m budget to serve the request irrespective of operation type.</span></span> <span data-ttu-id="e05fd-208">Sağlanan normal RUs/sn bütçe tüketilen ve istek RU/m bütçe kullanamayacaklarını, bu istek kısıtlanacak.</span><span class="sxs-lookup"><span data-stu-id="e05fd-208">If regular provisioned RUs/sec budget is consumed and the request cannot consume the RU/m budget, this request will be throttled.</span></span> <span data-ttu-id="e05fd-209">RU/m verimlilik bütçe etkinleştirilmişse varsayılan olarak, herhangi bir istek RU/m bütçe tarafından sunulur.</span><span class="sxs-lookup"><span data-stu-id="e05fd-209">By default, any request is served by RU/m budget if RU/m throughput budget is activated.</span></span> 

<span data-ttu-id="e05fd-210">CRUD ve sorgu işlemleri için DocumentDB API kullanarak RU/m bütçe devre dışı bırakmak için bir kod parçacığı aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e05fd-210">Here is a code snippet for disabling RU/m budget using the DocumentDB API for CRUD and query operations.</span></span>

```csharp
// In order to disable any CRUD request for RU/m, set DisableRUPerMinuteUsage to true in RequestOptions
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    new Document { Id = "Cosmos DB" },
    new RequestOptions { DisableRUPerMinuteUsage = true });
// In order to disable any query request for RU/m, set DisableRUPerMinuteOnRequest to true in RequestOptions
FeedOptions feedOptions = new FeedOptions();
feedOptions.DisableRUPerMinuteUsage = true;
var query = client.CreateDocumentQuery<Book>(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    "select * from c",feedOptions).AsDocumentQuery();
```

## <a name="next-steps"></a><span data-ttu-id="e05fd-211">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e05fd-211">Next steps</span></span>

<span data-ttu-id="e05fd-212">Bu makalede, biz Azure Cosmos DB nasıl bölümleme çalışır, bölümlenmiş koleksiyonlar nasıl oluşturulur ve uygulamanız için iyi bir bölüm anahtarı nasıl seçim yapabilirsiniz açıklanan.</span><span class="sxs-lookup"><span data-stu-id="e05fd-212">In this article, we've described how partitioning works in Azure Cosmos DB, how you can create partitioned collections, and how you can pick a good partition key for your application.</span></span>

* <span data-ttu-id="e05fd-213">Ölçek ve performans ile Azure Cosmos DB testi gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="e05fd-213">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="e05fd-214">Bkz: [performans ve ölçek testi Azure Cosmos DB ile](performance-testing.md) bir örnek için.</span><span class="sxs-lookup"><span data-stu-id="e05fd-214">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="e05fd-215">Kodlama ile çalışmaya başlama [SDK'ları](documentdb-sdk-dotnet.md) veya [REST API](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="e05fd-215">Get started coding with the [SDKs](documentdb-sdk-dotnet.md) or the [REST API](/rest/api/documentdb/).</span></span>
* <span data-ttu-id="e05fd-216">Hakkında bilgi edinin [sağlanan işleme](request-units.md) Azure Cosmos veritabanı</span><span class="sxs-lookup"><span data-stu-id="e05fd-216">Learn about [provisioned throughput](request-units.md) in Azure Cosmos DB</span></span> 

