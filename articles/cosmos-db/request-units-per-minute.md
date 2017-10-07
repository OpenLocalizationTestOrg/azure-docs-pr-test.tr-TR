---
title: "Azure CosmosDB: İstek birimleri (RU/m) dakikada | Microsoft Docs"
description: "Nasıl aynı kullanarak tooreduce maliyet istek birimleri dakikada öğrenin."
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
ms.openlocfilehash: fcc3a92b9788750a2bfba361c3a9cebdb56eee05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="request-units-per-minute-in-azure-cosmos-db"></a><span data-ttu-id="1d4ae-103">İstek birimleri dakikada Azure Cosmos veritabanı</span><span class="sxs-lookup"><span data-stu-id="1d4ae-103">Request units per minute in Azure Cosmos DB</span></span>

<span data-ttu-id="1d4ae-104">Azure Cosmos DB hızlı ve tahmin edilebilir performans ve ölçek uygulamanızın büyüme birlikte sorunsuz bir şekilde elde tasarlanmış toohelp ' dir.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-104">Azure Cosmos DB is designed toohelp you achieve a fast, predictable performance and scale seamlessly along with your application’s growth.</span></span> <span data-ttu-id="1d4ae-105">Her iki saniyede ve dakika başına (RU/m) ayrıntı Cosmos DB kapsayıcısı üzerinde üretilen işi sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-105">You can provision throughput on a Cosmos DB container at both, per-second and at per-minute (RU/m) granularities.</span></span> <span data-ttu-id="1d4ae-106">Merhaba dakika başına ayrıntı düzeyi, sağlanan işleme olduğu kullanılan toomanage saniyede bazda gerçekleşen hello iş yükü içindeki beklenmeyen ani.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-106">hello provisioned throughput at per-minute granularity is used toomanage unexpected spikes in hello workload occurring at a per-second granularity.</span></span> 

<span data-ttu-id="1d4ae-107">Bu makalede hello istek birimi (RU/m) dakikada sağlanmasını nasıl çalıştığını genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-107">This article provides an overview of how hello provisioning of Request Unit per Minute (RU/m) works.</span></span> <span data-ttu-id="1d4ae-108">Merhaba RU/m sağlama ile aklınızda tooprovide öngörülebilir bir performans (özellikle toorun analytics işletimsel verilerinizi en üstünde gerekiyorsa) öngörülemeyen gereksinimlerini ve spiky iş yükleri çevresinde hedeftir.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-108">hello goal in mind with provisioning of RU/m is tooprovide a predictable performance around unpredictable needs (especially if you need toorun analytics on top of your operational data) and spiky workloads.</span></span> <span data-ttu-id="1d4ae-109">Toohave müşterilerimizin içiniz rahat ile hızlı bir şekilde ölçeklendirebilirsiniz şekilde sağladıkları daha fazla hello verimlilik kullanmak istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-109">We want toohave our customers consume more hello throughput they provision so they can scale quickly with peace of mind.</span></span>

<span data-ttu-id="1d4ae-110">Bu makaleyi okuduktan sonra aşağıdaki soruları mümkün tooanswer hello olacaktır:</span><span class="sxs-lookup"><span data-stu-id="1d4ae-110">After reading this article, you will be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="1d4ae-111">Bir istek birimi dakikada nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="1d4ae-111">How does a Request Unit per Minute work?</span></span>
* <span data-ttu-id="1d4ae-112">Merhaba istek birimi / dakika ve saniye başına istek birimi arasındaki fark nedir?</span><span class="sxs-lookup"><span data-stu-id="1d4ae-112">What is hello difference between Request Unit per Minute and Request Unit per Second?</span></span>
* <span data-ttu-id="1d4ae-113">Nasıl tooprovision RU/m?</span><span class="sxs-lookup"><span data-stu-id="1d4ae-113">How tooprovision RU/m?</span></span>
* <span data-ttu-id="1d4ae-114">Hangi senaryosunda ı istek birimi dakikada sağlama düşünün?</span><span class="sxs-lookup"><span data-stu-id="1d4ae-114">Under which scenario shall I consider provisioning Request Unit per Minute?</span></span>
* <span data-ttu-id="1d4ae-115">Nasıl toouse hello portal ölçümleri toooptimize my maliyet ve performansı?</span><span class="sxs-lookup"><span data-stu-id="1d4ae-115">How toouse hello portal metrics toooptimize my cost and performance?</span></span>
* <span data-ttu-id="1d4ae-116">İstek türü RU/m bütçenizi tüketebileceği tanımla</span><span class="sxs-lookup"><span data-stu-id="1d4ae-116">Define which type of request can consume your RU/m budget?</span></span>

## <a name="provisioning-request-units-per-minute-rum"></a><span data-ttu-id="1d4ae-117">İstek birimleri (RU/m) dakikada sağlama</span><span class="sxs-lookup"><span data-stu-id="1d4ae-117">Provisioning request units per minute (RU/m)</span></span>

<span data-ttu-id="1d4ae-118">Azure Cosmos DB hello ikinci bazda (RU/s) sağlarken, üretilen iş o saniye içinde sağlanan hello kapasite aştı değil, düşük gecikme isteğiniz başarılı hello garantisi alın.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-118">When you provision Azure Cosmos DB at hello second granularity (RU/s), you get hello guarantee that your request succeeds at a low latency if your throughput has not exceeded hello capacity provisioned within that second.</span></span> <span data-ttu-id="1d4ae-119">RU/m ile bu dakika içinde isteğiniz başarılı hello garantisi hello MINUTE hello ayrıntı düzeyi altındadır.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-119">With RU/m, hello granularity is at hello minute with hello guarantee that your request succeeds within that minute.</span></span> <span data-ttu-id="1d4ae-120">Toobursting sistemleri, biz hello performans elde tahmin edilebilir olduğundan ve ona planlayabilirsiniz emin olun.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-120">Compared toobursting systems, we make sure that hello performance you get is predictable and you can plan on it.</span></span>

<span data-ttu-id="1d4ae-121">Merhaba şekilde works sağlama dakikada basittir:</span><span class="sxs-lookup"><span data-stu-id="1d4ae-121">hello way per minute provisioning works is simple:</span></span>

* <span data-ttu-id="1d4ae-122">RU/m saatlik ve ayrıca tooRU/s faturalandırılır.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-122">RU/m is billed hourly and in addition tooRU/s.</span></span> <span data-ttu-id="1d4ae-123">Daha fazla ayrıntı için lütfen Azure Cosmos DB ziyaret [fiyatlandırma sayfası](https://aka.ms/acdbpricing).</span><span class="sxs-lookup"><span data-stu-id="1d4ae-123">For more details, please visit Azure Cosmos DB [pricing page](https://aka.ms/acdbpricing).</span></span>
* <span data-ttu-id="1d4ae-124">Koleksiyon düzeyinde RU/m etkinleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-124">RU/m can be enabled at collection level.</span></span> <span data-ttu-id="1d4ae-125">Bu yapılabilir hello SDK (Node.js, Java ya da .net) veya hello portal üzerinden (aynı zamanda MongoDB API iş yükleri içerir)</span><span class="sxs-lookup"><span data-stu-id="1d4ae-125">That can be done through hello SDKs (Node.js, Java, or .Net) or through hello portal (also include MongoDB API workloads)</span></span>
* <span data-ttu-id="1d4ae-126">RU/m etkinleştirildiğinde her 100 RU/hazırlandı s için sağlanan 1.000 RU/m ayrıca Al (Merhaba orandır 10 x)</span><span class="sxs-lookup"><span data-stu-id="1d4ae-126">When RU/m is enabled, for every 100 RU/s provisioned, you also get 1,000 RU/m provisioned (hello ratio is 10x)</span></span>
* <span data-ttu-id="1d4ae-127">Yalnızca aştınız varsa, RU/m sağlama sırasında belirtilen ikinci bir, bir istek birimi kullanır, bu saniye içinde ikinci sağlama başına</span><span class="sxs-lookup"><span data-stu-id="1d4ae-127">At a given second, a request unit consumes your RU/m provisioning only if you have exceeded your per second provisioning within that second</span></span>
* <span data-ttu-id="1d4ae-128">Bir kez 60 saniye süre (UTC) uçları Merhaba, dakika sağlama başına hello refilled</span><span class="sxs-lookup"><span data-stu-id="1d4ae-128">Once hello 60-second period (UTC) ends, hello per minute provisioning is refilled</span></span>
* <span data-ttu-id="1d4ae-129">RU/m, yalnızca bir en fazla 5000 RU/s bölüm başına sağlama koleksiyonlar için etkinleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-129">RU/m can be enabled only for collections with a maximum provisioning of 5,000 RU/s per partition.</span></span> <span data-ttu-id="1d4ae-130">Üretilen iş gereksinimlerinize ölçeği ve bölüm başına sağlama böyle bir yüksek düzeyde varsa, bir uyarı iletisi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-130">If you scale your throughput needs and have such a high level of provisioning per partition, you will get a warning message</span></span>

<span data-ttu-id="1d4ae-131">Aşağıda bir müşteri 10kRU/s 100kRU/m ile sağlayabilirsiniz somut bir örnek %73 90 saniyelik süre 10.000 sahip bir koleksiyonun üzerinde aracılığıyla (50kRU/sn) en yoğun RU/s ve sağlanan 100.000 RU/m sağlama karşı Maliyet: kaydediliyor.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-131">Below is a concrete example, in which a customer can provision 10kRU/s with 100kRU/m, saving 73% in cost against provisioning for peak (at 50kRU/sec) through a 90-second period on a collection that has 10,000 RU/s and 100,000 RU/m provisioned:</span></span>

* <span data-ttu-id="1d4ae-132">1 saniye: hello RU/m bütçe 100.000 ayarlayın</span><span class="sxs-lookup"><span data-stu-id="1d4ae-132">1st second: hello RU/m budget is set at 100,000</span></span>
* <span data-ttu-id="1d4ae-133">3 ikinci: Bu ikinci hello sırasında istek birimi tüketimini edildi 11,010 RUs, hello RU/s sağlama yukarıda 1,010 RUs.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-133">3rd second: During that second hello consumption of Request Unit was 11,010 RUs, 1,010 RUs above hello RU/s provisioning.</span></span> <span data-ttu-id="1d4ae-134">Bu nedenle, 1,010 RUs hello RU/m bütçeden azaltılır.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-134">Therefore, 1,010 RUs are deducted from hello RU/m budget.</span></span> <span data-ttu-id="1d4ae-135">98,990 RUs sonraki 57 saniye cinsinden hello RU/m bütçe hello için kullanılabilir</span><span class="sxs-lookup"><span data-stu-id="1d4ae-135">98,990 RUs are available for hello next 57 seconds in hello RU/m budget</span></span>
* <span data-ttu-id="1d4ae-136">29 ikinci: Bu saniye boyunca büyük bir aşırı oldu (> 4 x saniyede sağlama daha yüksek) ve istek birimi hello tüketimini 46,920 RUs.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-136">29th second: During that second, a large spike happened (>4x higher than provisioning per second) and hello consumption of Request Unit was 46,920 RUs.</span></span> <span data-ttu-id="1d4ae-137">403 RUs (29 saniye) 92,323 RUs (28 saniye) too55 bırakılan hello RU/m bütçesi 36,920 RUs kesinti</span><span class="sxs-lookup"><span data-stu-id="1d4ae-137">36,920 RUs are deducted from hello RU/m budget that dropped from 92,323 RUs (28th second) too55,403 RUs (29th second)</span></span>
* <span data-ttu-id="1d4ae-138">61st ikinci: RU/m bütçe too100, 000 RUs geri ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-138">61st second: RU/m budget is set back too100,000 RUs.</span></span>
 
![Merhaba tüketimini gösteren ve Azure Cosmos DB sağlama grafiği](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute.png)

## <a name="specifying-request-unit-capacity-with-rum"></a><span data-ttu-id="1d4ae-140">İstek birimi kapasite RU/m ile belirtme</span><span class="sxs-lookup"><span data-stu-id="1d4ae-140">Specifying request unit capacity with RU/m</span></span>

<span data-ttu-id="1d4ae-141">Bir Azure Cosmos DB koleksiyonunu oluştururken hello numarası belirtin (RU saniye başına) saniyede istek birimlerinin hello koleksiyonu için ayrılmış istiyor.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-141">When creating an Azure Cosmos DB collection, you specify hello number of request units per second (RU per second) you want reserved for hello collection.</span></span> <span data-ttu-id="1d4ae-142">Dakika başına tooadd RU isteyip istemediğinizi de karar verebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-142">You can also decide if you want tooadd RU per minute.</span></span> <span data-ttu-id="1d4ae-143">Bu hello portalı veya hello SDK aracılığıyla yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-143">This can be done through hello Portal or hello SDK.</span></span> 

### <a name="through-hello-portal"></a><span data-ttu-id="1d4ae-144">Merhaba Portal</span><span class="sxs-lookup"><span data-stu-id="1d4ae-144">Through hello Portal</span></span>

<span data-ttu-id="1d4ae-145">Yalnızca etkinleştirme veya dakikada RU devre dışı bırakma bir koleksiyonu sağlamada gerektirir.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-145">Enabling or disabling RU per minute simply requires a click when provisioning a collection.</span></span> 

 ![Gösteren ekran görüntüsü nasıl hello Azure portal'ın tooset RU/m](./media/request-units-per-minute/azure-cosmos-db-request-unit-per-minute-portal.png)

### <a name="through-hello-sdk"></a><span data-ttu-id="1d4ae-147">Merhaba SDK</span><span class="sxs-lookup"><span data-stu-id="1d4ae-147">Through hello SDK</span></span>
<span data-ttu-id="1d4ae-148">İlk olarak, bu önemli toonote RU/m yalnızca SDK'ları aşağıdaki hello için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-148">First, this is important toonote that RU/m is only available for hello following SDKs:</span></span>

* <span data-ttu-id="1d4ae-149">.NET 1.14.0</span><span class="sxs-lookup"><span data-stu-id="1d4ae-149">.Net 1.14.0</span></span>
* <span data-ttu-id="1d4ae-150">Java 1.11.0</span><span class="sxs-lookup"><span data-stu-id="1d4ae-150">Java 1.11.0</span></span>
* <span data-ttu-id="1d4ae-151">Node.js 1.12.0</span><span class="sxs-lookup"><span data-stu-id="1d4ae-151">Node.js 1.12.0</span></span>
* <span data-ttu-id="1d4ae-152">Python 2.2.0</span><span class="sxs-lookup"><span data-stu-id="1d4ae-152">Python 2.2.0</span></span>

<span data-ttu-id="1d4ae-153">Merhaba .NET SDK kullanarak dakika başına ikinci ve 30.000 isteği birim başına 3000 isteği birim içeren bir koleksiyon oluşturmak için bir kod parçacığı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1d4ae-153">Here is a code snippet for creating a collection with 3,000 request units per second and 30,000 request units per minute using hello .NET SDK:</span></span>

```csharp
// Create a collection with RU/m enabled
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

// Set hello throughput too3,000 request units per second which will give you 30,000 request units per minute as hello RU/m budget
await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 3000, OfferEnableRUPerMinuteThroughput = true });
```

<span data-ttu-id="1d4ae-154">Bir koleksiyon too5 hello verimini değiştirmek için bir kod parçacığı aşağıda verilmiştir, .NET SDK'sı dakika kullanarak başına RU sağlama olmadan saniyede 000 istek birimleri hello:</span><span class="sxs-lookup"><span data-stu-id="1d4ae-154">Here is a code snippet for changing hello throughput of a collection too5,000 request units per second without provisioning RU per minute using hello .NET SDK:</span></span>

```csharp
// Get hello current offer
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set hello throughput too5000 request units per second without RU/m enabled (hello last parameter tooOfferV2 constructor below)
OfferV2 offerV2 = new OfferV2(offer, 5000, false);

// Now persist these changes toohello database by replacing hello original resource
await client.ReplaceOfferAsync(offerV2);
```

## <a name="good-fit-scenarios"></a><span data-ttu-id="1d4ae-155">İyi senaryoları Sığdır</span><span class="sxs-lookup"><span data-stu-id="1d4ae-155">Good fit scenarios</span></span>

<span data-ttu-id="1d4ae-156">Bu bölümde, dakika başına istek birimleri etkinleştirmek için iyi bir tercihtir senaryoların genel bir bakış sağlar.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-156">In this section, we provide an overview of scenarios that are a good fit for enabling request units per minute.</span></span>

<span data-ttu-id="1d4ae-157">**Geliştirme ve Test Ortamı:** iyi sığacak şekilde.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-157">**Dev/Test environment:** Good fit.</span></span> <span data-ttu-id="1d4ae-158">Farklı iş yükleri ile uygulamanızı test ediyorsanız bu aşamada hello geliştirme aşamasında RU/m hello esneklik sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-158">During hello development stage, if you are testing your application with different workloads, RU/m can provide hello flexibility at this stage.</span></span> <span data-ttu-id="1d4ae-159">Merhaba sırasında [öykünücüsü](local-emulator.md) harika ücretsiz aracı tootest Azure Cosmos DB değil.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-159">While hello [emulator](local-emulator.md) is a great free tool tootest Azure Cosmos DB.</span></span> <span data-ttu-id="1d4ae-160">Ancak, bir bulut ortamında toostart istiyorsanız, geçici performans gereksinimlerinizi RU/m ile büyük bir esneklik gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-160">However if you want toostart in a cloud environment, you will have a great flexibility with RU/m for your adhoc performance needs.</span></span> <span data-ttu-id="1d4ae-161">Geliştirme, daha az düşünmeye ilk performans gereksinimleri hakkında daha fazla süre beklemesini.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-161">You will spend more time developing, less worrying about performance needs at first.</span></span> <span data-ttu-id="1d4ae-162">Biz hello minimum RU/s sağlama ile başlamanızı öneririz ve RU/m etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-162">We recommend starting with hello minimum RU/s provisioning and enable RU/m.</span></span>

<span data-ttu-id="1d4ae-163">**Öngörülemeyen, spiky, dakika ayrıntı düzeyi gerekiyor:** iyi sığacak – tasarrufları: % 25 75.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-163">**Unpredictable, spiky, minute granularity needs:** Good fit – Savings: 25-75%.</span></span> <span data-ttu-id="1d4ae-164">Biz RU/m ve çoğu üretim senaryoları büyük geliştirme olan bu gruba gördünüz.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-164">We have seen large improvement from RU/m and most production scenarios are into that group.</span></span> <span data-ttu-id="1d4ae-165">Sorguları çalıştırma varsa birkaç kez bir dakika içinde depo olan bir IOT iş yükü varsa, sisteminizi zaman yapar toplu aynı hello Ekle zaman, handeling spiky gereken için ek kapasite gerekir.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-165">If you have an IoT workload that has spike a few times in a minute, if you have queries running when your system makes mass insert at hello same time, you will need extra capacity for handeling spiky needs.</span></span> <span data-ttu-id="1d4ae-166">Adım adım yaklaşımımız aşağıdaki uygulayarak kaynak gereksinimlerinizi en iyi duruma getirme öneririz.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-166">We recommend optimizing your resource needs by applying our step by step approach below.</span></span>

 ![5 dakikalık ayrıntı isteği tüketimini gösteren grafik](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-consumption.png)
 
 <span data-ttu-id="1d4ae-168">*Şekil - RU tüketim Kıyaslama*</span><span class="sxs-lookup"><span data-stu-id="1d4ae-168">*Figure - RU consumption benchmark*</span></span>

<span data-ttu-id="1d4ae-169">**İçiniz rahat:** iyi sığacak – tasarrufları: % 10-20.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-169">**Peace of mind:** Good fit – Savings: 10-20%.</span></span> <span data-ttu-id="1d4ae-170">Bazı durumlarda, yalnızca toohave içiniz rahat istiyor ve olası yükselmeleri ve azaltma hakkında endişelenmeniz değil.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-170">Sometimes, you just want toohave peace of mind and not worry about potential peaks and throttling.</span></span> <span data-ttu-id="1d4ae-171">Sizin için hello sağa bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-171">This feature is hello right one for you.</span></span> <span data-ttu-id="1d4ae-172">Bu durumda, RU/m etkinleştirme öneririz ve biraz daha düşük, ikinci sağlama başına.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-172">In that case, we recommend enabling RU/m and slightly lower your per second provisioning.</span></span> <span data-ttu-id="1d4ae-173">Bu durumda hello öğesinden farklı aynıdır titizlikle, sağlama toooptimize denemez.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-173">This case is different from hello above as you will not try toooptimize aggressively your provisioning.</span></span> <span data-ttu-id="1d4ae-174">Daha fazla olan bir "Sıfır azaltma" bakış budur.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-174">This is more of a “Zero Throttling” mindset you are in.</span></span>

<span data-ttu-id="1d4ae-175">Adhoc gereksinimleri olan kritik işlemler: bazen tooonly izin RU/m bütçe hello bütçe açılmıyor şekilde erişim tüketen geçici veya önemli işlemleri daha az kritik işlemler öneririz.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-175">Critical operations with adhoc needs: We sometimes recommend tooonly let critical operations access RU/m budget so hello budget doesn’t get consume by adhoc or less important operations.</span></span> <span data-ttu-id="1d4ae-176">Merhaba aşağıdaki bölümde, kolayca tanımlanabilir.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-176">That can be easily defined in hello section below.</span></span>

## <a name="using-hello-portal-metrics-toooptimize-cost-and-performance"></a><span data-ttu-id="1d4ae-177">Merhaba portal ölçümleri toooptimize maliyet ve performansı kullanma</span><span class="sxs-lookup"><span data-stu-id="1d4ae-177">Using hello portal metrics toooptimize cost and performance</span></span>

<span data-ttu-id="1d4ae-178">**Merhaba önümüzdeki haftalarda biz, üretilen iş gereken RUs dakika tüketim toooptimize izleme geçici hello içerik daha fazla geliştireceksiniz.**</span><span class="sxs-lookup"><span data-stu-id="1d4ae-178">**In hello coming weeks, we will further develop hello content around monitoring RUs minute consumption toooptimize your throughput needs.**</span></span>

<span data-ttu-id="1d4ae-179">Merhaba portal ölçümleri karşı RU tüketen normal RU saniye ne kadarının dakika görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-179">Through hello portal metrics, you can see how much of regular RU seconds you consume versus RU minutes.</span></span> <span data-ttu-id="1d4ae-180">Bu ölçümleri izleme, sağlama en iyi hale getirmenize yardımcı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-180">Monitoring these metrics should help you optimize your provisioning.</span></span> 

<span data-ttu-id="1d4ae-181">Adım adım bir yaklaşım nasıl öneririz toouse RU/m tooyour avantajı.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-181">We recommend a step by step approach on how toouse RU/m tooyour advantage.</span></span> <span data-ttu-id="1d4ae-182">Her adımı için (Bu olabilir saat, gün, veya hatta hafta), iş yükü tam döngüsünün temsil eden hello RU tüketim genel bir bakış olmalıdır ve ne sağlamak, hello kullanımı Öngörüler alın.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-182">For each step, you should have an overview of hello RU consumption representing a full cycle of your workload (it could be hours, days, or even weeks) and get insights on hello utilization of what you provision.</span></span>

<span data-ttu-id="1d4ae-183">Merhaba bu yaklaşım arkasında olarak, işleme sağlama kapatın, performans ölçütlerle eşleşen noktası sağlama olası tooa toomake ilkesidir.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-183">hello principle behind this approach is toomake your throughput provisioning as close as possible tooa provisioning point that matches your performance criteria below.</span></span> 

![5 dakikalık ayrıntı isteği tüketimini gösteren grafik](./media/request-units-per-minute/azure-cosmos-db-request-units-per-minute-adjust-provisioning.png)
 
<span data-ttu-id="1d4ae-185">toounderstand hello en iyi sağlama noktası iş yükü, toounderstand gerekir:</span><span class="sxs-lookup"><span data-stu-id="1d4ae-185">toounderstand hello optimal provisioning point for your workload, you need toounderstand:</span></span>

* <span data-ttu-id="1d4ae-186">Tüketim desenleri: Hayır, kesintili veya sürekli ani?</span><span class="sxs-lookup"><span data-stu-id="1d4ae-186">Consumption patterns: no, infrequent or sustained spikes?</span></span> <span data-ttu-id="1d4ae-187">(2 x ortalama) küçük, Orta veya büyük (> 10 x ortalama) ani?</span><span class="sxs-lookup"><span data-stu-id="1d4ae-187">Small (2x average), medium, or large (>10x average) spikes?</span></span>
* <span data-ttu-id="1d4ae-188">Daraltılmış istekleri yüzdesi: hızlandırma biraz varsa rahat düşündüğünüz musunuz?</span><span class="sxs-lookup"><span data-stu-id="1d4ae-188">Percent of throttled requests: do you feel comfortable if you have a bit of throttling?</span></span> <span data-ttu-id="1d4ae-189">Öyleyse, ne kadar?</span><span class="sxs-lookup"><span data-stu-id="1d4ae-189">If so, by how much?</span></span> 

<span data-ttu-id="1d4ae-190">Hedefleriniz nelerdir belirledikten sonra mümkün tooget daha yakından toohello en iyi sağlama olacaktır.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-190">Once you have identified what your goals are, you will be able tooget closer toohello optimal provisioning.</span></span>

<span data-ttu-id="1d4ae-191">tooassist tooprovide nasıl, RU/m tüketime, sağlama toooptimize dayanarak bir genel yönergeler, istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-191">tooassist you, we want tooprovide an overall guidance on how toooptimize your provisioning based on your RU/m consumption.</span></span> <span data-ttu-id="1d4ae-192">Bu kılavuz tooall türdeki iş yüklerini uygulanmaz ancak hello özel Önizleme bilgisini temel alarak.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-192">This guidance doesn’t apply tooall kind of workloads but is based on hello private preview knowledge.</span></span> <span data-ttu-id="1d4ae-193">Biz bu tür temelleri değişebilir olarak size daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="1d4ae-193">We might change such baselines as we learn more:</span></span>

|<span data-ttu-id="1d4ae-194">RU/m % kullanımı</span><span class="sxs-lookup"><span data-stu-id="1d4ae-194">RU/m % utilization</span></span>|<span data-ttu-id="1d4ae-195">RU/m kullanımını derecesini</span><span class="sxs-lookup"><span data-stu-id="1d4ae-195">Degree of utilization of RU/m</span></span>|<span data-ttu-id="1d4ae-196">Sağlama için Önerilen Eylemler</span><span class="sxs-lookup"><span data-stu-id="1d4ae-196">Recommended actions for provisioning</span></span>|
|---|---|---|
|<span data-ttu-id="1d4ae-197">0-1%</span><span class="sxs-lookup"><span data-stu-id="1d4ae-197">0-1%</span></span>|<span data-ttu-id="1d4ae-198">Kullanımı altında</span><span class="sxs-lookup"><span data-stu-id="1d4ae-198">Under utilization</span></span>|<span data-ttu-id="1d4ae-199">Daha fazla RU/m RU/s tooconsume alt</span><span class="sxs-lookup"><span data-stu-id="1d4ae-199">Lower RU/s tooconsume more RU/m</span></span>|
|<span data-ttu-id="1d4ae-200">1-10%</span><span class="sxs-lookup"><span data-stu-id="1d4ae-200">1-10%</span></span>|<span data-ttu-id="1d4ae-201">Sağlıklı kullanın</span><span class="sxs-lookup"><span data-stu-id="1d4ae-201">Healthy use</span></span>|<span data-ttu-id="1d4ae-202">Merhaba aynı düzeyi sağlamaya devam</span><span class="sxs-lookup"><span data-stu-id="1d4ae-202">Keep hello same provisioning level</span></span>|
|<span data-ttu-id="1d4ae-203">Yukarıdaki % 10</span><span class="sxs-lookup"><span data-stu-id="1d4ae-203">Above 10%</span></span>|<span data-ttu-id="1d4ae-204">Kullanımı</span><span class="sxs-lookup"><span data-stu-id="1d4ae-204">Over utilization</span></span>|<span data-ttu-id="1d4ae-205">Toorely RU/s RU/m üzerinde daha az artırın</span><span class="sxs-lookup"><span data-stu-id="1d4ae-205">Increase RU/s toorely less on RU/m</span></span>|

## <a name="select-which-operations-can-consume-hello-rum-budget"></a><span data-ttu-id="1d4ae-206">Hangi işlemleri hello RU/m bütçe tüketebileceği seçin</span><span class="sxs-lookup"><span data-stu-id="1d4ae-206">Select which operations can consume hello RU/m budget</span></span>

<span data-ttu-id="1d4ae-207">İsteği düzeyinde, ayrıca etkinleştirebilir/RU/m bütçe tooserve hello isteğini işlem türü ne olursa olsun devre dışı bırakabilir.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-207">At request level, you can also enable/disable RU/m budget tooserve hello request irrespective of operation type.</span></span> <span data-ttu-id="1d4ae-208">Sağlanan normal RUs/sn bütçe tüketilen ve hello isteği hello RU/m bütçe kullanamayacaklarını, bu istek kısıtlanacak.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-208">If regular provisioned RUs/sec budget is consumed and hello request cannot consume hello RU/m budget, this request will be throttled.</span></span> <span data-ttu-id="1d4ae-209">RU/m verimlilik bütçe etkinleştirilmişse varsayılan olarak, herhangi bir istek RU/m bütçe tarafından sunulur.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-209">By default, any request is served by RU/m budget if RU/m throughput budget is activated.</span></span> 

<span data-ttu-id="1d4ae-210">CRUD ve sorgu işlemleri için hello DocumentDB API kullanarak RU/m bütçe devre dışı bırakmak için bir kod parçacığı aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-210">Here is a code snippet for disabling RU/m budget using hello DocumentDB API for CRUD and query operations.</span></span>

```csharp
// In order toodisable any CRUD request for RU/m, set DisableRUPerMinuteUsage tootrue in RequestOptions
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    new Document { Id = "Cosmos DB" },
    new RequestOptions { DisableRUPerMinuteUsage = true });
// In order toodisable any query request for RU/m, set DisableRUPerMinuteOnRequest tootrue in RequestOptions
FeedOptions feedOptions = new FeedOptions();
feedOptions.DisableRUPerMinuteUsage = true;
var query = client.CreateDocumentQuery<Book>(
    UriFactory.CreateDocumentCollectionUri("db", "container"),
    "select * from c",feedOptions).AsDocumentQuery();
```

## <a name="next-steps"></a><span data-ttu-id="1d4ae-211">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1d4ae-211">Next steps</span></span>

<span data-ttu-id="1d4ae-212">Bu makalede, biz Azure Cosmos DB nasıl bölümleme çalışır, bölümlenmiş koleksiyonlar nasıl oluşturulur ve uygulamanız için iyi bir bölüm anahtarı nasıl seçim yapabilirsiniz açıklanan.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-212">In this article, we've described how partitioning works in Azure Cosmos DB, how you can create partitioned collections, and how you can pick a good partition key for your application.</span></span>

* <span data-ttu-id="1d4ae-213">Ölçek ve performans ile Azure Cosmos DB testi gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-213">Perform scale and performance testing with Azure Cosmos DB.</span></span> <span data-ttu-id="1d4ae-214">Bkz: [performans ve ölçek testi Azure Cosmos DB ile](performance-testing.md) bir örnek için.</span><span class="sxs-lookup"><span data-stu-id="1d4ae-214">See [Performance and Scale Testing with Azure Cosmos DB](performance-testing.md) for a sample.</span></span>
* <span data-ttu-id="1d4ae-215">Kodlama Hello ile çalışmaya başlama [SDK'ları](documentdb-sdk-dotnet.md) veya hello [REST API](/rest/api/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="1d4ae-215">Get started coding with hello [SDKs](documentdb-sdk-dotnet.md) or hello [REST API](/rest/api/documentdb/).</span></span>
* <span data-ttu-id="1d4ae-216">Hakkında bilgi edinin [sağlanan işleme](request-units.md) Azure Cosmos veritabanı</span><span class="sxs-lookup"><span data-stu-id="1d4ae-216">Learn about [provisioned throughput](request-units.md) in Azure Cosmos DB</span></span> 

