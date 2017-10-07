---
title: "aaaDocumentDB API performans düzeyleri | Microsoft Docs"
description: "Nasıl DocumentDB API performans düzeyleri, kapsayıcı başına temelinde tooreserve verimlilik etkinleştirme hakkında bilgi edinin."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 7dc21c71-47e2-4e06-aa21-e84af52866f4
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 716bc11ae238dbb0feebf004ed8d5f8a7515ec6f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="retiring-hello-s1-s2-and-s3-performance-levels"></a><span data-ttu-id="500cf-103">Merhaba S1, S2 ve S3 performans düzeyleri devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="500cf-103">Retiring hello S1, S2, and S3 performance levels</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="500cf-104">Bu makalede açıklanan hello S1, S2 ve S3 performans düzeyleri kullanımdan kaldırılacak ve artık yeni DocumentDB API hesapları için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="500cf-104">hello S1, S2, and S3 performance levels discussed in this article are being retired and are no longer available for new DocumentDB API accounts.</span></span>
>

<span data-ttu-id="500cf-105">Bu makalede, S1, S2 ve S3 performans düzeyleri genel bir bakış sağlar ve bu performans düzeyleri kullanmak hello koleksiyonları 1 Ağustos 2017 geçirilen toosingle bölüm koleksiyonları nasıl olacaktır açıklanır.</span><span class="sxs-lookup"><span data-stu-id="500cf-105">This article provides an overview of S1, S2, and S3 performance levels, and discusses how hello collections that use these performance levels will be migrated toosingle partition collections on August 1st, 2017.</span></span> <span data-ttu-id="500cf-106">Bu makaleyi okuduktan sonra aşağıdaki soruları mümkün tooanswer hello olması:</span><span class="sxs-lookup"><span data-stu-id="500cf-106">After reading this article, you'll be able tooanswer hello following questions:</span></span>

- [<span data-ttu-id="500cf-107">Merhaba S1, S2 ve S3 performans neden olan kaldırılan düzeyleri?</span><span class="sxs-lookup"><span data-stu-id="500cf-107">Why are hello S1, S2, and S3 performance levels being retired?</span></span>](#why-retired)
- [<span data-ttu-id="500cf-108">Nasıl tek bölüm koleksiyonları ve bölümlenmiş koleksiyonlar toohello S1, S2, S3 performans düzeyleri karşılaştırması nedir?</span><span class="sxs-lookup"><span data-stu-id="500cf-108">How do single partition collections and partitioned collections compare toohello S1, S2, S3 performance levels?</span></span>](#compare)
- [<span data-ttu-id="500cf-109">I ne toodo tooensure kesintisiz toomy veri erişim?</span><span class="sxs-lookup"><span data-stu-id="500cf-109">What do I need toodo tooensure uninterrupted access toomy data?</span></span>](#uninterrupted-access)
- [<span data-ttu-id="500cf-110">Nasıl kendi koleksiyonuma hello geçişten sonra değişir mi?</span><span class="sxs-lookup"><span data-stu-id="500cf-110">How will my collection change after hello migration?</span></span>](#collection-change)
- [<span data-ttu-id="500cf-111">Geçirilen toosingle bölüm koleksiyonları ben sonra my faturalama nasıl değiştirilir?</span><span class="sxs-lookup"><span data-stu-id="500cf-111">How will my billing change after I’m migrated toosingle partition collections?</span></span>](#billing-change)
- [<span data-ttu-id="500cf-112">Ne birden fazla 10 GB depolama alanı ihtiyacım var?</span><span class="sxs-lookup"><span data-stu-id="500cf-112">What if I need more than 10 GB of storage?</span></span>](#more-storage-needed)
- [<span data-ttu-id="500cf-113">1 Ağustos 2017 önce hello S1, S2 ve S3 performans düzeyleri arasında değiştirebilir miyim?</span><span class="sxs-lookup"><span data-stu-id="500cf-113">Can I change between hello S1, S2, and S3 performance levels before August 1, 2017?</span></span>](#change-before)
- [<span data-ttu-id="500cf-114">Ne zaman kendi koleksiyonuma geçirildiğini nasıl anlarım?</span><span class="sxs-lookup"><span data-stu-id="500cf-114">How will I know when my collection has migrated?</span></span>](#when-migrated)
- [<span data-ttu-id="500cf-115">Merhaba S1, S2, S3 performans düzeyleri toosingle bölüm koleksiyonlar üzerinde kendi gelen nasıl geçişini?</span><span class="sxs-lookup"><span data-stu-id="500cf-115">How do I migrate from hello S1, S2, S3 performance levels toosingle partition collections on my own?</span></span>](#migrate-diy)
- [<span data-ttu-id="500cf-116">Nasıl bir EA müşteri ben varsa ı etkilenen?</span><span class="sxs-lookup"><span data-stu-id="500cf-116">How am I impacted if I'm an EA customer?</span></span>](#ea-customer)

<a name="why-retired"></a>

## <a name="why-are-hello-s1-s2-and-s3-performance-levels-being-retired"></a><span data-ttu-id="500cf-117">Merhaba S1, S2 ve S3 performans neden olan kaldırılan düzeyleri?</span><span class="sxs-lookup"><span data-stu-id="500cf-117">Why are hello S1, S2, and S3 performance levels being retired?</span></span>

<span data-ttu-id="500cf-118">Merhaba S1, S2 ve S3 performans düzeyleri değil DocumentDB API koleksiyonları sunar teklif hello esneklik yapın.</span><span class="sxs-lookup"><span data-stu-id="500cf-118">hello S1, S2, and S3 performance levels do not offer hello flexibility that DocumentDB API collections offers.</span></span> <span data-ttu-id="500cf-119">Merhaba S1, S2, S3 performans düzeyleri, her iki hello işleme ve depolama kapasitesini önceden ayarlanmış ve esneklik sunmadı.</span><span class="sxs-lookup"><span data-stu-id="500cf-119">With hello S1, S2, S3 performance levels, both hello throughput and storage capacity were pre-set and did not offer elasticity.</span></span> <span data-ttu-id="500cf-120">Azure Cosmos DB artık hello özelliği toocustomize üretilen iş ve depolama yeteneği tooscale gereksinimleriniz değiştikçe çok daha fazla esneklik sunumu sunar.</span><span class="sxs-lookup"><span data-stu-id="500cf-120">Azure Cosmos DB now offers hello ability toocustomize your throughput and storage, offering you much more flexibility in your ability tooscale as your needs change.</span></span>

<a name="compare"></a>

## <a name="how-do-single-partition-collections-and-partitioned-collections-compare-toohello-s1-s2-s3-performance-levels"></a><span data-ttu-id="500cf-121">Nasıl tek bölüm koleksiyonları ve bölümlenmiş koleksiyonlar toohello S1, S2, S3 performans düzeyleri karşılaştırması nedir?</span><span class="sxs-lookup"><span data-stu-id="500cf-121">How do single partition collections and partitioned collections compare toohello S1, S2, S3 performance levels?</span></span>

<span data-ttu-id="500cf-122">Aşağıdaki tablonun hello hello işleme ve depolama seçenekleri tek bölüm koleksiyonları, bölümlenmiş koleksiyonlar ve S1, S2, S3 performans düzeyleri karşılaştırır.</span><span class="sxs-lookup"><span data-stu-id="500cf-122">hello following table compares hello throughput and storage options available in single partition collections, partitioned collections, and S1, S2, S3 performance levels.</span></span> <span data-ttu-id="500cf-123">ABD Doğu 2 bölge için örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="500cf-123">Here is an example for US East 2 region:</span></span>

|   |<span data-ttu-id="500cf-124">Bölümlenmiş koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="500cf-124">Partitioned collection</span></span>|<span data-ttu-id="500cf-125">Tek bir bölüm koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="500cf-125">Single partition collection</span></span>|<span data-ttu-id="500cf-126">S1</span><span class="sxs-lookup"><span data-stu-id="500cf-126">S1</span></span>|<span data-ttu-id="500cf-127">S2</span><span class="sxs-lookup"><span data-stu-id="500cf-127">S2</span></span>|<span data-ttu-id="500cf-128">S3</span><span class="sxs-lookup"><span data-stu-id="500cf-128">S3</span></span>|
|---|---|---|---|---|---|
|<span data-ttu-id="500cf-129">En yüksek verimlilik</span><span class="sxs-lookup"><span data-stu-id="500cf-129">Maximum throughput</span></span>|<span data-ttu-id="500cf-130">Sınırsız</span><span class="sxs-lookup"><span data-stu-id="500cf-130">Unlimited</span></span>|<span data-ttu-id="500cf-131">10 K RU/s</span><span class="sxs-lookup"><span data-stu-id="500cf-131">10K RU/s</span></span>|<span data-ttu-id="500cf-132">250 RU/s</span><span class="sxs-lookup"><span data-stu-id="500cf-132">250 RU/s</span></span>|<span data-ttu-id="500cf-133">1 K RU/s</span><span class="sxs-lookup"><span data-stu-id="500cf-133">1 K RU/s</span></span>|<span data-ttu-id="500cf-134">2.5 K RU/s</span><span class="sxs-lookup"><span data-stu-id="500cf-134">2.5 K RU/s</span></span>|
|<span data-ttu-id="500cf-135">En düşük işleme</span><span class="sxs-lookup"><span data-stu-id="500cf-135">Minimum throughput</span></span>|<span data-ttu-id="500cf-136">2.5 K RU/s</span><span class="sxs-lookup"><span data-stu-id="500cf-136">2.5K RU/s</span></span>|<span data-ttu-id="500cf-137">400 RU/s</span><span class="sxs-lookup"><span data-stu-id="500cf-137">400 RU/s</span></span>|<span data-ttu-id="500cf-138">250 RU/s</span><span class="sxs-lookup"><span data-stu-id="500cf-138">250 RU/s</span></span>|<span data-ttu-id="500cf-139">1 K RU/s</span><span class="sxs-lookup"><span data-stu-id="500cf-139">1 K RU/s</span></span>|<span data-ttu-id="500cf-140">2.5 K RU/s</span><span class="sxs-lookup"><span data-stu-id="500cf-140">2.5 K RU/s</span></span>|
|<span data-ttu-id="500cf-141">Maksimum depolama</span><span class="sxs-lookup"><span data-stu-id="500cf-141">Maximum storage</span></span>|<span data-ttu-id="500cf-142">Sınırsız</span><span class="sxs-lookup"><span data-stu-id="500cf-142">Unlimited</span></span>|<span data-ttu-id="500cf-143">10 GB</span><span class="sxs-lookup"><span data-stu-id="500cf-143">10 GB</span></span>|<span data-ttu-id="500cf-144">10 GB</span><span class="sxs-lookup"><span data-stu-id="500cf-144">10 GB</span></span>|<span data-ttu-id="500cf-145">10 GB</span><span class="sxs-lookup"><span data-stu-id="500cf-145">10 GB</span></span>|<span data-ttu-id="500cf-146">10 GB</span><span class="sxs-lookup"><span data-stu-id="500cf-146">10 GB</span></span>|
|<span data-ttu-id="500cf-147">Fiyat (ay)</span><span class="sxs-lookup"><span data-stu-id="500cf-147">Price (monthly)</span></span>|<span data-ttu-id="500cf-148">Verimlilik: $6 / 100 RU/s</span><span class="sxs-lookup"><span data-stu-id="500cf-148">Throughput: $6 / 100 RU/s</span></span><br><br><span data-ttu-id="500cf-149">Depolama: $ 0,25/GB</span><span class="sxs-lookup"><span data-stu-id="500cf-149">Storage: $0.25/GB</span></span>|<span data-ttu-id="500cf-150">Verimlilik: $6 / 100 RU/s</span><span class="sxs-lookup"><span data-stu-id="500cf-150">Throughput: $6 / 100 RU/s</span></span><br><br><span data-ttu-id="500cf-151">Depolama: $ 0,25/GB</span><span class="sxs-lookup"><span data-stu-id="500cf-151">Storage: $0.25/GB</span></span>|<span data-ttu-id="500cf-152">$25 ABD DOLARI</span><span class="sxs-lookup"><span data-stu-id="500cf-152">$25 USD</span></span>|<span data-ttu-id="500cf-153">$50 ABD DOLARI</span><span class="sxs-lookup"><span data-stu-id="500cf-153">$50 USD</span></span>|<span data-ttu-id="500cf-154">$100 ABD DOLARI</span><span class="sxs-lookup"><span data-stu-id="500cf-154">$100 USD</span></span>|

<span data-ttu-id="500cf-155">EA müşteri misiniz?</span><span class="sxs-lookup"><span data-stu-id="500cf-155">Are you an EA customer?</span></span> <span data-ttu-id="500cf-156">Aksi takdirde bkz [nasıl ı etkilenen EA müşteri ben varsa?](#ea-customer)</span><span class="sxs-lookup"><span data-stu-id="500cf-156">If so, see [How am I impacted if I'm an EA customer?](#ea-customer)</span></span>

<a name="uninterrupted-access"></a>

## <a name="what-do-i-need-toodo-tooensure-uninterrupted-access-toomy-data"></a><span data-ttu-id="500cf-157">I ne toodo tooensure kesintisiz toomy veri erişim?</span><span class="sxs-lookup"><span data-stu-id="500cf-157">What do I need toodo tooensure uninterrupted access toomy data?</span></span>

<span data-ttu-id="500cf-158">Hiçbir şey Cosmos DB hello geçiş sizin için işler.</span><span class="sxs-lookup"><span data-stu-id="500cf-158">Nothing, Cosmos DB handles hello migration for you.</span></span> <span data-ttu-id="500cf-159">S1, S2 ve S3 koleksiyonu varsa, geçerli koleksiyonunuzu 31 Temmuz 2017 geçirilen tooa tek bölüm koleksiyonu olacaktır.</span><span class="sxs-lookup"><span data-stu-id="500cf-159">If you have an S1, S2, or S3 collection, your current collection will be migrated tooa single partition collection on July 31, 2017.</span></span> 

<a name="collection-change"></a>

## <a name="how-will-my-collection-change-after-hello-migration"></a><span data-ttu-id="500cf-160">Nasıl kendi koleksiyonuma hello geçişten sonra değişir mi?</span><span class="sxs-lookup"><span data-stu-id="500cf-160">How will my collection change after hello migration?</span></span>

<span data-ttu-id="500cf-161">S1 koleksiyonu varsa, 400 RU/s üretilen iş ile geçirilen tooa tek bölümlü bir koleksiyon olacaktır.</span><span class="sxs-lookup"><span data-stu-id="500cf-161">If you have an S1 collection, you will be migrated tooa single partition collection with 400 RU/s throughput.</span></span> <span data-ttu-id="500cf-162">400 RU/s hello en düşük işleme sahip tek bölüm koleksiyonları kullanılabilir olur.</span><span class="sxs-lookup"><span data-stu-id="500cf-162">400 RU/s is hello lowest throughput available with single partition collections.</span></span> <span data-ttu-id="500cf-163">Ancak, tek bölüm koleksiyonudur yaklaşık S1 koleksiyonunuzu aynı ödeme hello hello 400 RU/s ve 250 RU/sizin için ödeme yapıyorsanız olmayan şekilde s – hello maliyeti çok 150 RU/s kullanılabilir tooyou hello.</span><span class="sxs-lookup"><span data-stu-id="500cf-163">However, hello cost for 400 RU/s in hello a single partition collection is approximately hello same as you were paying with your S1 collection and 250 RU/s – so you are not paying for hello extra 150 RU/s available tooyou.</span></span>

<span data-ttu-id="500cf-164">S2 koleksiyonu varsa, geçirilen tooa tek bölüm 1 K RU/s koleksiyonuyla olacaktır.</span><span class="sxs-lookup"><span data-stu-id="500cf-164">If you have an S2 collection, you will be migrated tooa single partition collection with 1 K RU/s.</span></span> <span data-ttu-id="500cf-165">Hiçbir değişiklik tooyour üretilen iş düzeyi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="500cf-165">You will see no change tooyour throughput level.</span></span>

<span data-ttu-id="500cf-166">S3 koleksiyonu varsa, geçirilen tooa tek bölümlü bir koleksiyon 2,5 K RU/s ile olacaktır.</span><span class="sxs-lookup"><span data-stu-id="500cf-166">If you have an S3 collection, you will be migrated tooa single partition collection with 2.5 K RU/s.</span></span> <span data-ttu-id="500cf-167">Hiçbir değişiklik tooyour üretilen iş düzeyi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="500cf-167">You will see no change tooyour throughput level.</span></span>

<span data-ttu-id="500cf-168">Her durumda, koleksiyonunuzu geçirildikten sonra üretilen iş düzeyi mümkün toocustomize olması, veya kaldıracak ölçeklemek yukarı ve aşağı gerekli tooprovide düşük gecikmeli erişim tooyour kullanıcılar olarak.</span><span class="sxs-lookup"><span data-stu-id="500cf-168">In each of these cases, after your collection is migrated, you will be able toocustomize your throughput level, or scale it up and down as needed tooprovide low-latency access tooyour users.</span></span> <span data-ttu-id="500cf-169">koleksiyonunuz geçirildikten sonra toochange hello üretilen iş düzeyi Cosmos DB hesabınızı hello Azure portal açmanız yeterlidir, Ölçek'ı tıklatın, koleksiyonunuzu seçin ve sonra hello üretilen iş düzeyi hello ekran aşağıdaki gösterildiği gibi ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="500cf-169">toochange hello throughput level after your collection has migrated, simply open your Cosmos DB account in hello Azure portal, click Scale, choose your collection, and then adjust hello throughput level, as shown in hello following screenshot:</span></span>

![Nasıl tooscale performansı hello Azure portalı](./media/performance-levels/portal-scale-throughput.png)

<a name="billing-change"></a>

## <a name="how-will-my-billing-change-after-im-migrated-toohello-single-partition-collections"></a><span data-ttu-id="500cf-171">Geçirilen toohello tek bölüm koleksiyonları ben sonra my faturalama nasıl değiştirilir?</span><span class="sxs-lookup"><span data-stu-id="500cf-171">How will my billing change after I’m migrated toohello single partition collections?</span></span>

<span data-ttu-id="500cf-172">Varsayılmıştır 10 S1 koleksiyonları, 1 GB depolama alanı hello BİZE Doğu bölgede her sahiptir ve bu 10 S1 koleksiyonları too10 tek bölüm koleksiyonları 400 RU/sn (en düşük düzey hello) konumunda geçirme.</span><span class="sxs-lookup"><span data-stu-id="500cf-172">Assuming you have 10 S1 collections, 1 GB of storage for each, in hello US East region, and you migrate these 10 S1 collections too10 single partition collections at 400 RU/sec (hello minimum level).</span></span> <span data-ttu-id="500cf-173">Tam bir ay için hello 10 tek bölüm koleksiyonları tutarsanız faturanızı şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="500cf-173">Your bill will look as follows if you keep hello 10 single partition collections for a full month:</span></span>

![S1 10 koleksiyonlar için fiyatlandırma too10 koleksiyonları nasıl karşılaştırır tek bölümlü bir koleksiyon için fiyatlandırma kullanma](./media/performance-levels/s1-vs-standard-pricing.png)

<a name="more-storage-needed"></a>

## <a name="what-if-i-need-more-than-10-gb-of-storage"></a><span data-ttu-id="500cf-175">Ne birden fazla 10 GB depolama alanı ihtiyacım var?</span><span class="sxs-lookup"><span data-stu-id="500cf-175">What if I need more than 10 GB of storage?</span></span>

<span data-ttu-id="500cf-176">S1, S2 ve S3 bir performans düzeyine sahip bir koleksiyona sahip ya da 10 GB kullanılabilir depolama alanı olan bir tek bölümlü bir koleksiyona sahip olup olmadığını, verileri tooa koleksiyonuyla neredeyse bölümlenmiş hello Cosmos DB veri geçiş aracı toomigrate kullanabilirsiniz Sınırsız depolama.</span><span class="sxs-lookup"><span data-stu-id="500cf-176">Whether you have a collection with an S1, S2, or S3 performance level, or have a single partition collection, all of which have 10 GB of storage available, you can use hello Cosmos DB Data Migration tool toomigrate your data tooa partitioned collection with virtually unlimited storage.</span></span> <span data-ttu-id="500cf-177">Bölümlendirilmiş bir koleksiyon hello avantajları hakkında daha fazla bilgi için bkz: [bölümleme ve Azure Cosmos DB'de ölçeklendirme](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="500cf-177">For information about hello benefits of a partitioned collection, see [Partitioning and scaling in Azure Cosmos DB](documentdb-partition-data.md).</span></span> <span data-ttu-id="500cf-178">Hakkında bilgi için toomigrate S1, S2, S3 veya tek bölümlü bir koleksiyon bölümlenmiş tooa koleksiyonu, bkz: [tek bölümlü toopartitioned koleksiyonlarından geçiş](documentdb-partition-data.md#migrating-from-single-partition).</span><span class="sxs-lookup"><span data-stu-id="500cf-178">For information about how toomigrate your S1, S2, S3, or single partition collection tooa partitioned collection, see [Migrating from single-partition toopartitioned collections](documentdb-partition-data.md#migrating-from-single-partition).</span></span> 

<a name="change-before"></a>

## <a name="can-i-change-between-hello-s1-s2-and-s3-performance-levels-before-august-1-2017"></a><span data-ttu-id="500cf-179">1 Ağustos 2017 önce hello S1, S2 ve S3 performans düzeyleri arasında değiştirebilir miyim?</span><span class="sxs-lookup"><span data-stu-id="500cf-179">Can I change between hello S1, S2, and S3 performance levels before August 1, 2017?</span></span>

<span data-ttu-id="500cf-180">S1, S2 ve S3 performans yalnızca var olan hesapları mümkün toochange olması ve performans düzeyi katmanları hello portalı üzerinden veya program aracılığıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="500cf-180">Only existing accounts with S1, S2, and S3 performance will be able toochange and alter performance level tiers through hello portal or programmatically.</span></span> <span data-ttu-id="500cf-181">1 Ağustos 2017 S1, S2, hello ve S3 performans düzeyleri artık kullanılabilir olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="500cf-181">By August 1, 2017, hello S1, S2, and S3 performance levels will no longer be available.</span></span> <span data-ttu-id="500cf-182">S1, S3 veya S3 tooa tek bölüm koleksiyonundan değiştirirseniz, S1, S2 ve S3 performans düzeyleri toohello döndüremez.</span><span class="sxs-lookup"><span data-stu-id="500cf-182">If you change from S1, S3, or S3 tooa single partition collection, you cannot return toohello S1, S2, or S3 performance levels.</span></span>

<a name="when-migrated"></a>

## <a name="how-will-i-know-when-my-collection-has-migrated"></a><span data-ttu-id="500cf-183">Ne zaman kendi koleksiyonuma geçirildiğini nasıl anlarım?</span><span class="sxs-lookup"><span data-stu-id="500cf-183">How will I know when my collection has migrated?</span></span>

<span data-ttu-id="500cf-184">Merhaba geçiş 31 Temmuz 2017 üzerinde meydana gelir.</span><span class="sxs-lookup"><span data-stu-id="500cf-184">hello migration will occur on July 31, 2017.</span></span> <span data-ttu-id="500cf-185">Bir koleksiyon varsa hello S1, S2 kullanan veya S3 performans düzeyleri, hello Cosmos DB takım hello geçiş gerçekleşmeden önce e-posta ile bağlantı kurar.</span><span class="sxs-lookup"><span data-stu-id="500cf-185">If you have a collection that uses hello S1, S2 or S3 performance levels, hello Cosmos DB team will contact you by email before hello migration takes place.</span></span> <span data-ttu-id="500cf-186">Hello geçiş 1 Ağustos 2017 üzerinde tamamlandıktan sonra hello Azure portal, koleksiyonunuzu standart fiyatlandırma kullandığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="500cf-186">Once hello migration is complete, on August 1, 2017, hello Azure portal will show that your collection uses Standard pricing.</span></span>

![Koleksiyonunuz tooconfirm nasıl sahip toohello standart fiyatlandırma katmanı geçişi](./media/performance-levels/portal-standard-pricing-applied.png)

<a name="migrate-diy"></a>

## <a name="how-do-i-migrate-from-hello-s1-s2-s3-performance-levels-toosingle-partition-collections-on-my-own"></a><span data-ttu-id="500cf-188">Merhaba S1, S2, S3 performans düzeyleri toosingle bölüm koleksiyonlar üzerinde kendi gelen nasıl geçişini?</span><span class="sxs-lookup"><span data-stu-id="500cf-188">How do I migrate from hello S1, S2, S3 performance levels toosingle partition collections on my own?</span></span>

<span data-ttu-id="500cf-189">Merhaba S1, S2, geçirebileceğiniz ve S3 performans hello Azure portal kullanarak toosingle bölüm koleksiyonları Düzeyler veya program aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="500cf-189">You can migrate from hello S1, S2, and S3 performance levels toosingle partition collections using hello Azure portal or programmatically.</span></span> <span data-ttu-id="500cf-190">1 Ağustos önce kendi toobenefit üzerinde hello esnek işleme seçenekleri ile tek bölüm koleksiyonları kullanılabilir bunu yapabilirsiniz veya koleksiyonlarınızı sizin için 31 Temmuz 2017 üzerinde geçirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="500cf-190">You can do this on your own before August 1 toobenefit from hello flexible throughput options available with single partition collections, or we will migrate your collections for you on July 31, 2017.</span></span>

<span data-ttu-id="500cf-191">**Hello Azure portal kullanarak toomigrate toosingle bölüm koleksiyonları**</span><span class="sxs-lookup"><span data-stu-id="500cf-191">**toomigrate toosingle partition collections using hello Azure portal**</span></span>

1. <span data-ttu-id="500cf-192">Merhaba, [ **Azure portal**](https://portal.azure.com), tıklatın **Azure Cosmos DB**, hello Cosmos DB hesap toomodify seçin.</span><span class="sxs-lookup"><span data-stu-id="500cf-192">In hello [**Azure portal**](https://portal.azure.com), click **Azure Cosmos DB**, then select hello Cosmos DB account toomodify.</span></span> 
 
    <span data-ttu-id="500cf-193">Varsa **Azure Cosmos DB** üzerinde atlama çubuğu Merhaba, tıklatın değil >, çok kaydırma**veritabanları**seçin **Azure Cosmos DB**ve ardından hello DocumentDB hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="500cf-193">If **Azure Cosmos DB** is not on hello Jumpbar, click >, scroll too**Databases**, select **Azure Cosmos DB**, and then select hello DocumentDB account.</span></span>  

2. <span data-ttu-id="500cf-194">Merhaba kaynak menüsünde altında **kapsayıcıları**, tıklatın **ölçek**hello koleksiyonu toomodify hello aşağı açılan listeden seçin ve ardından **fiyatlandırma katmanı**.</span><span class="sxs-lookup"><span data-stu-id="500cf-194">On hello resource menu, under **Containers**, click **Scale**, select hello collection toomodify from hello drop-down list, and then click **Pricing Tier**.</span></span> <span data-ttu-id="500cf-195">Önceden tanımlanmış verimlilik kullanarak hesapları S1, S2 ve S3 fiyatlandırma katmanı vardır.</span><span class="sxs-lookup"><span data-stu-id="500cf-195">Accounts using pre-defined throughput have a pricing tier of S1, S2, or S3.</span></span>  <span data-ttu-id="500cf-196">Merhaba, **fiyatlandırma katmanınızı seçin** dikey penceresinde tıklatın **standart** toochange toouser tanımlı verimlilik ve ardından **seçin** toosave değişikliğinizin.</span><span class="sxs-lookup"><span data-stu-id="500cf-196">In hello **Choose your pricing tier** blade, click **Standard** toochange toouser-defined throughput, and then click **Select** toosave your change.</span></span>

    ![Burada toochange hello verimlilik değeri gösteren hello ayarları dikey penceresi ekran görüntüsü](./media/performance-levels/change-performance-set-thoughput.png)

3. <span data-ttu-id="500cf-198">Merhaba edilene **ölçek** dikey penceresinde, hello **fiyatlandırma katmanı** çok değiştirilir**standart** ve hello **üretilen işi (RU/s)** kutusu ile görüntülenir bir 400 varsayılan değeri.</span><span class="sxs-lookup"><span data-stu-id="500cf-198">Back in hello **Scale** blade, hello **Pricing Tier** is changed too**Standard** and hello **Throughput (RU/s)** box is displayed with a default value of 400.</span></span> <span data-ttu-id="500cf-199">Set hello işleme 400-10.000 arasında [istek birimleri](request-units.md)/second (RU/s).</span><span class="sxs-lookup"><span data-stu-id="500cf-199">Set hello throughput between 400 and 10,000 [Request units](request-units.md)/second (RU/s).</span></span> <span data-ttu-id="500cf-200">Merhaba **tahmini aylık fatura** hello hello sonunda sayfa tooprovide aylık maliyeti hello tahmini otomatik olarak güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="500cf-200">hello **Estimated Monthly Bill** at hello bottom of hello page updates automatically tooprovide an estimate of hello monthly cost.</span></span> 

    >[!IMPORTANT] 
    > <span data-ttu-id="500cf-201">Yaptığınız değişiklikleri kaydedin ve toohello standart fiyatlandırma katmanını taşımak sonra toohello S1, S2 ve S3 performans düzeyleri geri alamazsınız.</span><span class="sxs-lookup"><span data-stu-id="500cf-201">Once you save your changes and move toohello Standard pricing tier, you cannot roll back toohello S1, S2, or S3 performance levels.</span></span>

4. <span data-ttu-id="500cf-202">Tıklatın **kaydetmek** toosave değişikliklerinizi.</span><span class="sxs-lookup"><span data-stu-id="500cf-202">Click **Save** toosave your changes.</span></span>

    <span data-ttu-id="500cf-203">Daha fazla verimlilik (10. 000'ru / s büyük) veya daha fazla depolama alanı (10 GB'den büyük) gerekli belirlerseniz, bölümlendirilmiş bir koleksiyon oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="500cf-203">If you determine that you need more throughput (greater than 10,000 RU/s) or more storage (greater than 10GB) you can create a partitioned collection.</span></span> <span data-ttu-id="500cf-204">toomigrate tek bölümlü bir koleksiyon bölümlenmiş tooa koleksiyonu bkz [tek bölümlü toopartitioned koleksiyonlarından geçiş](documentdb-partition-data.md#migrating-from-single-partition).</span><span class="sxs-lookup"><span data-stu-id="500cf-204">toomigrate a single partition collection tooa partitioned collection, see [Migrating from single-partition toopartitioned collections](documentdb-partition-data.md#migrating-from-single-partition).</span></span>

    > [!NOTE]
    > <span data-ttu-id="500cf-205">S1, S2 ve S3 tooStandard değiştirme too2 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="500cf-205">Changing from S1, S2, or S3 tooStandard may take up too2 minutes.</span></span>
    > 
    > 

<span data-ttu-id="500cf-206">**Merhaba .NET SDK kullanarak toomigrate toosingle bölüm koleksiyonları**</span><span class="sxs-lookup"><span data-stu-id="500cf-206">**toomigrate toosingle partition collections using hello .NET SDK**</span></span>

<span data-ttu-id="500cf-207">Koleksiyonlarınızı performans düzeylerini değiştirmek için başka bir seçenek bizim SDK olur.</span><span class="sxs-lookup"><span data-stu-id="500cf-207">Another option for changing your collections' performance levels is through our SDKs.</span></span> <span data-ttu-id="500cf-208">Bu bölüm, yalnızca bir koleksiyona ait performansının değiştirilmesi kapsar kullanarak düzey bizim [DocumentDB .NET API](documentdb-sdk-dotnet.md), ancak bizim diğer SDK için hello işlemi benzerdir.</span><span class="sxs-lookup"><span data-stu-id="500cf-208">This section only covers changing a collection's performance level using our [DocumentDB .NET API](documentdb-sdk-dotnet.md), but hello process is similar for our other SDKs.</span></span>

<span data-ttu-id="500cf-209">Saniye başına 000 isteği birim hello koleksiyonu verimlilik too5 değiştirmek için bir kod parçacığı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="500cf-209">Here is a code snippet for changing hello collection throughput too5,000 request units per second:</span></span>
    
```C#
    //Fetch hello resource toobe updated
    Offer offer = client.CreateOfferQuery()
                      .Where(r => r.ResourceLink == collection.SelfLink)    
                      .AsEnumerable()
                      .SingleOrDefault();

    // Set hello throughput too5000 request units per second
    offer = new OfferV2(offer, 5000);

    //Now persist these changes toohello database by replacing hello original resource
    await client.ReplaceOfferAsync(offer);
```

<span data-ttu-id="500cf-210">Ziyaret [MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx) tooview ek örnekler ve bizim teklif yöntemleri hakkında daha fazla bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="500cf-210">Visit [MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx) tooview additional examples and learn more about our offer methods:</span></span>

* [<span data-ttu-id="500cf-211">**ReadOfferAsync**</span><span class="sxs-lookup"><span data-stu-id="500cf-211">**ReadOfferAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readofferasync.aspx)
* [<span data-ttu-id="500cf-212">**ReadOffersFeedAsync**</span><span class="sxs-lookup"><span data-stu-id="500cf-212">**ReadOffersFeedAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readoffersfeedasync.aspx)
* [<span data-ttu-id="500cf-213">**ReplaceOfferAsync**</span><span class="sxs-lookup"><span data-stu-id="500cf-213">**ReplaceOfferAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.replaceofferasync.aspx)
* [<span data-ttu-id="500cf-214">**CreateOfferQuery**</span><span class="sxs-lookup"><span data-stu-id="500cf-214">**CreateOfferQuery**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.linq.documentqueryable.createofferquery.aspx)

<a name="ea-customer"></a>

## <a name="how-am-i-impacted-if-im-an-ea-customer"></a><span data-ttu-id="500cf-215">Nasıl bir EA müşteri ben varsa ı etkilenen?</span><span class="sxs-lookup"><span data-stu-id="500cf-215">How am I impacted if I'm an EA customer?</span></span>

<span data-ttu-id="500cf-216">EA müşteriler kendi geçerli sözleşmenin hello sonuna kadar korumalı fiyat olacaktır.</span><span class="sxs-lookup"><span data-stu-id="500cf-216">EA customers will be price protected until hello end of their current contract.</span></span>

## <a name="next-steps"></a><span data-ttu-id="500cf-217">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="500cf-217">Next steps</span></span>
<span data-ttu-id="500cf-218">Fiyatlandırma ve Azure Cosmos DB ile verileri yönetme hakkında daha fazla toolearn şu kaynakları araştırın:</span><span class="sxs-lookup"><span data-stu-id="500cf-218">toolearn more about pricing and managing data with Azure Cosmos DB, explore these resources:</span></span>

1.  <span data-ttu-id="500cf-219">[Cosmos DB'de veri bölümlendirme](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="500cf-219">[Partitioning data in Cosmos DB](documentdb-partition-data.md).</span></span> <span data-ttu-id="500cf-220">Merhaba birbirinden bölümleme stratejisi tooscale sorunsuz bir şekilde uygulama ipuçları yanı sıra tek bölümlü bir kapsayıcı ve bölümlenmiş kapsayıcıları anlayın.</span><span class="sxs-lookup"><span data-stu-id="500cf-220">Understand hello difference between single partition container and partitioned containers, as well as tips on implementing a partitioning strategy tooscale seamlessly.</span></span>
2.  <span data-ttu-id="500cf-221">[Cosmos DB fiyatlandırma](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="500cf-221">[Cosmos DB pricing](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span> <span data-ttu-id="500cf-222">Üretilen iş sağlama ve depolama tüketme hello maliyeti hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="500cf-222">Learn about hello cost of provisioning throughput and consuming storage.</span></span>
3.  <span data-ttu-id="500cf-223">[İstek birimleri](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="500cf-223">[Request units](request-units.md).</span></span> <span data-ttu-id="500cf-224">Farklı işlem türleri için örneğin okuma, yazma, sorgu işleme Hello tüketimini anlayın.</span><span class="sxs-lookup"><span data-stu-id="500cf-224">Understand hello consumption of throughput for different operation types, for example Read, Write, Query.</span></span>
