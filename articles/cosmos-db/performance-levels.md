---
title: "DocumentDB API performans düzeyleri | Microsoft Docs"
description: "DocumentDB API performans düzeyleri, üretilen iş başına kapsayıcı olarak ayırmak nasıl etkinleştirme hakkında bilgi edinin."
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
ms.openlocfilehash: c8d4733e57eb760dbb8e8ca96f6ba55671d1742f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="retiring-the-s1-s2-and-s3-performance-levels"></a><span data-ttu-id="1267f-103">S1, S2 ve S3 performans düzeyleri devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="1267f-103">Retiring the S1, S2, and S3 performance levels</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="1267f-104">Bu makalede açıklanan S1, S2 ve S3 performans düzeyleri kullanımdan kaldırılacak ve artık yeni DocumentDB API hesapları için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1267f-104">The S1, S2, and S3 performance levels discussed in this article are being retired and are no longer available for new DocumentDB API accounts.</span></span>
>

<span data-ttu-id="1267f-105">Bu makalede, S1, S2 ve S3 performans düzeyleri genel bir bakış sağlar ve 1 Ağustos 2017 üzerinde nasıl bu performans düzeyleri kullanmak koleksiyonlar için tek bölüm koleksiyonları geçirilecek açıklanır.</span><span class="sxs-lookup"><span data-stu-id="1267f-105">This article provides an overview of S1, S2, and S3 performance levels, and discusses how the collections that use these performance levels will be migrated to single partition collections on August 1st, 2017.</span></span> <span data-ttu-id="1267f-106">Bu makaleyi okuduktan sonra aşağıdaki soruları yanıtlayın mümkün olacaktır:</span><span class="sxs-lookup"><span data-stu-id="1267f-106">After reading this article, you'll be able to answer the following questions:</span></span>

- [<span data-ttu-id="1267f-107">S1, S2 ve S3 performans neden olan kaldırılan düzeyleri?</span><span class="sxs-lookup"><span data-stu-id="1267f-107">Why are the S1, S2, and S3 performance levels being retired?</span></span>](#why-retired)
- [<span data-ttu-id="1267f-108">Nasıl tek bölüm koleksiyonları ve bölümlenmiş koleksiyonlar S1 için S2, S3 performans düzeyleri karşılaştırması nedir?</span><span class="sxs-lookup"><span data-stu-id="1267f-108">How do single partition collections and partitioned collections compare to the S1, S2, S3 performance levels?</span></span>](#compare)
- [<span data-ttu-id="1267f-109">Verilerimi kesintisiz erişim sağlamak için yapmanız gerekenler nelerdir?</span><span class="sxs-lookup"><span data-stu-id="1267f-109">What do I need to do to ensure uninterrupted access to my data?</span></span>](#uninterrupted-access)
- [<span data-ttu-id="1267f-110">Nasıl kendi koleksiyonuma geçişten sonra değişir mi?</span><span class="sxs-lookup"><span data-stu-id="1267f-110">How will my collection change after the migration?</span></span>](#collection-change)
- [<span data-ttu-id="1267f-111">Tek bölüm koleksiyonları geçişi sonra nasıl my faturalama değişir mi?</span><span class="sxs-lookup"><span data-stu-id="1267f-111">How will my billing change after I’m migrated to single partition collections?</span></span>](#billing-change)
- [<span data-ttu-id="1267f-112">Ne birden fazla 10 GB depolama alanı ihtiyacım var?</span><span class="sxs-lookup"><span data-stu-id="1267f-112">What if I need more than 10 GB of storage?</span></span>](#more-storage-needed)
- [<span data-ttu-id="1267f-113">S1, S2 ve S3 performans düzeyleri 1 Ağustos 2017 önce değiştirebilirim?</span><span class="sxs-lookup"><span data-stu-id="1267f-113">Can I change between the S1, S2, and S3 performance levels before August 1, 2017?</span></span>](#change-before)
- [<span data-ttu-id="1267f-114">Ne zaman kendi koleksiyonuma geçirildiğini nasıl anlarım?</span><span class="sxs-lookup"><span data-stu-id="1267f-114">How will I know when my collection has migrated?</span></span>](#when-migrated)
- [<span data-ttu-id="1267f-115">S3 performans düzeyleri üzerinde kendi tek bölüm koleksiyonları nasıl S1, S2, geçişini?</span><span class="sxs-lookup"><span data-stu-id="1267f-115">How do I migrate from the S1, S2, S3 performance levels to single partition collections on my own?</span></span>](#migrate-diy)
- [<span data-ttu-id="1267f-116">Nasıl bir EA müşteri ben varsa ı etkilenen?</span><span class="sxs-lookup"><span data-stu-id="1267f-116">How am I impacted if I'm an EA customer?</span></span>](#ea-customer)

<a name="why-retired"></a>

## <a name="why-are-the-s1-s2-and-s3-performance-levels-being-retired"></a><span data-ttu-id="1267f-117">S1, S2 ve S3 performans neden olan kaldırılan düzeyleri?</span><span class="sxs-lookup"><span data-stu-id="1267f-117">Why are the S1, S2, and S3 performance levels being retired?</span></span>

<span data-ttu-id="1267f-118">S1, S2 ve S3 performans düzeyleri DocumentDB API koleksiyonları sunar esnekliği sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="1267f-118">The S1, S2, and S3 performance levels do not offer the flexibility that DocumentDB API collections offers.</span></span> <span data-ttu-id="1267f-119">S1, S2, S3 performans düzeyleri ile üretilen iş ve depolama kapasitesini önceden ayarlanmış ve esneklik sunmadı.</span><span class="sxs-lookup"><span data-stu-id="1267f-119">With the S1, S2, S3 performance levels, both the throughput and storage capacity were pre-set and did not offer elasticity.</span></span> <span data-ttu-id="1267f-120">Azure Cosmos DB işleme ve depolama, özelleştirme yeteneği gereksinimleriniz değiştikçe ölçeklendirme yeteneğinizi çok daha fazla esneklik sunumu olarak sunar.</span><span class="sxs-lookup"><span data-stu-id="1267f-120">Azure Cosmos DB now offers the ability to customize your throughput and storage, offering you much more flexibility in your ability to scale as your needs change.</span></span>

<a name="compare"></a>

## <a name="how-do-single-partition-collections-and-partitioned-collections-compare-to-the-s1-s2-s3-performance-levels"></a><span data-ttu-id="1267f-121">Nasıl tek bölüm koleksiyonları ve bölümlenmiş koleksiyonlar S1 için S2, S3 performans düzeyleri karşılaştırması nedir?</span><span class="sxs-lookup"><span data-stu-id="1267f-121">How do single partition collections and partitioned collections compare to the S1, S2, S3 performance levels?</span></span>

<span data-ttu-id="1267f-122">Aşağıdaki tabloda tek bölüm koleksiyonları, bölümlenmiş koleksiyonlar ve S1, S2, S3 performans düzeyleri kullanılabilir işleme ve depolama seçenekleri karşılaştırılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="1267f-122">The following table compares the throughput and storage options available in single partition collections, partitioned collections, and S1, S2, S3 performance levels.</span></span> <span data-ttu-id="1267f-123">ABD Doğu 2 bölge için örnek aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1267f-123">Here is an example for US East 2 region:</span></span>

|   |<span data-ttu-id="1267f-124">Bölümlenmiş koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="1267f-124">Partitioned collection</span></span>|<span data-ttu-id="1267f-125">Tek bir bölüm koleksiyonu</span><span class="sxs-lookup"><span data-stu-id="1267f-125">Single partition collection</span></span>|<span data-ttu-id="1267f-126">S1</span><span class="sxs-lookup"><span data-stu-id="1267f-126">S1</span></span>|<span data-ttu-id="1267f-127">S2</span><span class="sxs-lookup"><span data-stu-id="1267f-127">S2</span></span>|<span data-ttu-id="1267f-128">S3</span><span class="sxs-lookup"><span data-stu-id="1267f-128">S3</span></span>|
|---|---|---|---|---|---|
|<span data-ttu-id="1267f-129">En yüksek verimlilik</span><span class="sxs-lookup"><span data-stu-id="1267f-129">Maximum throughput</span></span>|<span data-ttu-id="1267f-130">Sınırsız</span><span class="sxs-lookup"><span data-stu-id="1267f-130">Unlimited</span></span>|<span data-ttu-id="1267f-131">10 K RU/s</span><span class="sxs-lookup"><span data-stu-id="1267f-131">10K RU/s</span></span>|<span data-ttu-id="1267f-132">250 RU/s</span><span class="sxs-lookup"><span data-stu-id="1267f-132">250 RU/s</span></span>|<span data-ttu-id="1267f-133">1 K RU/s</span><span class="sxs-lookup"><span data-stu-id="1267f-133">1 K RU/s</span></span>|<span data-ttu-id="1267f-134">2.5 K RU/s</span><span class="sxs-lookup"><span data-stu-id="1267f-134">2.5 K RU/s</span></span>|
|<span data-ttu-id="1267f-135">En düşük işleme</span><span class="sxs-lookup"><span data-stu-id="1267f-135">Minimum throughput</span></span>|<span data-ttu-id="1267f-136">2.5 K RU/s</span><span class="sxs-lookup"><span data-stu-id="1267f-136">2.5K RU/s</span></span>|<span data-ttu-id="1267f-137">400 RU/s</span><span class="sxs-lookup"><span data-stu-id="1267f-137">400 RU/s</span></span>|<span data-ttu-id="1267f-138">250 RU/s</span><span class="sxs-lookup"><span data-stu-id="1267f-138">250 RU/s</span></span>|<span data-ttu-id="1267f-139">1 K RU/s</span><span class="sxs-lookup"><span data-stu-id="1267f-139">1 K RU/s</span></span>|<span data-ttu-id="1267f-140">2.5 K RU/s</span><span class="sxs-lookup"><span data-stu-id="1267f-140">2.5 K RU/s</span></span>|
|<span data-ttu-id="1267f-141">Maksimum depolama</span><span class="sxs-lookup"><span data-stu-id="1267f-141">Maximum storage</span></span>|<span data-ttu-id="1267f-142">Sınırsız</span><span class="sxs-lookup"><span data-stu-id="1267f-142">Unlimited</span></span>|<span data-ttu-id="1267f-143">10 GB</span><span class="sxs-lookup"><span data-stu-id="1267f-143">10 GB</span></span>|<span data-ttu-id="1267f-144">10 GB</span><span class="sxs-lookup"><span data-stu-id="1267f-144">10 GB</span></span>|<span data-ttu-id="1267f-145">10 GB</span><span class="sxs-lookup"><span data-stu-id="1267f-145">10 GB</span></span>|<span data-ttu-id="1267f-146">10 GB</span><span class="sxs-lookup"><span data-stu-id="1267f-146">10 GB</span></span>|
|<span data-ttu-id="1267f-147">Fiyat (ay)</span><span class="sxs-lookup"><span data-stu-id="1267f-147">Price (monthly)</span></span>|<span data-ttu-id="1267f-148">Verimlilik: $6 / 100 RU/s</span><span class="sxs-lookup"><span data-stu-id="1267f-148">Throughput: $6 / 100 RU/s</span></span><br><br><span data-ttu-id="1267f-149">Depolama: $ 0,25/GB</span><span class="sxs-lookup"><span data-stu-id="1267f-149">Storage: $0.25/GB</span></span>|<span data-ttu-id="1267f-150">Verimlilik: $6 / 100 RU/s</span><span class="sxs-lookup"><span data-stu-id="1267f-150">Throughput: $6 / 100 RU/s</span></span><br><br><span data-ttu-id="1267f-151">Depolama: $ 0,25/GB</span><span class="sxs-lookup"><span data-stu-id="1267f-151">Storage: $0.25/GB</span></span>|<span data-ttu-id="1267f-152">$25 ABD DOLARI</span><span class="sxs-lookup"><span data-stu-id="1267f-152">$25 USD</span></span>|<span data-ttu-id="1267f-153">$50 ABD DOLARI</span><span class="sxs-lookup"><span data-stu-id="1267f-153">$50 USD</span></span>|<span data-ttu-id="1267f-154">$100 ABD DOLARI</span><span class="sxs-lookup"><span data-stu-id="1267f-154">$100 USD</span></span>|

<span data-ttu-id="1267f-155">EA müşteri misiniz?</span><span class="sxs-lookup"><span data-stu-id="1267f-155">Are you an EA customer?</span></span> <span data-ttu-id="1267f-156">Aksi takdirde bkz [nasıl ı etkilenen EA müşteri ben varsa?](#ea-customer)</span><span class="sxs-lookup"><span data-stu-id="1267f-156">If so, see [How am I impacted if I'm an EA customer?](#ea-customer)</span></span>

<a name="uninterrupted-access"></a>

## <a name="what-do-i-need-to-do-to-ensure-uninterrupted-access-to-my-data"></a><span data-ttu-id="1267f-157">Verilerimi kesintisiz erişim sağlamak için yapmanız gerekenler nelerdir?</span><span class="sxs-lookup"><span data-stu-id="1267f-157">What do I need to do to ensure uninterrupted access to my data?</span></span>

<span data-ttu-id="1267f-158">Hiçbir şey Cosmos DB geçiş sizin için işler.</span><span class="sxs-lookup"><span data-stu-id="1267f-158">Nothing, Cosmos DB handles the migration for you.</span></span> <span data-ttu-id="1267f-159">S1, S2 ve S3 koleksiyonu varsa, geçerli koleksiyonunuzu 31 Temmuz 2017 üzerinde tek bölümlü bir koleksiyon geçirilir.</span><span class="sxs-lookup"><span data-stu-id="1267f-159">If you have an S1, S2, or S3 collection, your current collection will be migrated to a single partition collection on July 31, 2017.</span></span> 

<a name="collection-change"></a>

## <a name="how-will-my-collection-change-after-the-migration"></a><span data-ttu-id="1267f-160">Nasıl kendi koleksiyonuma geçişten sonra değişir mi?</span><span class="sxs-lookup"><span data-stu-id="1267f-160">How will my collection change after the migration?</span></span>

<span data-ttu-id="1267f-161">S1 koleksiyonu 400 RU/s üretilen iş ile bir tek bölümlü bir koleksiyon için bir geçişi yapılmaz.</span><span class="sxs-lookup"><span data-stu-id="1267f-161">If you have an S1 collection, you will be migrated to a single partition collection with 400 RU/s throughput.</span></span> <span data-ttu-id="1267f-162">Tek bölüm koleksiyonları ile kullanılabilen en düşük işleme 400 RU/s olur.</span><span class="sxs-lookup"><span data-stu-id="1267f-162">400 RU/s is the lowest throughput available with single partition collections.</span></span> <span data-ttu-id="1267f-163">Ancak, 400 RU/s maliyeti, çok 150 RU/s için kullanabileceğiniz ödeme yapıyorsanız olmayan şekilde S1 koleksiyonunuzu ve 250 RU/s – ödeme tek bölümlü bir koleksiyon yaklaşık aynıdır.</span><span class="sxs-lookup"><span data-stu-id="1267f-163">However, the cost for 400 RU/s in the a single partition collection is approximately the same as you were paying with your S1 collection and 250 RU/s – so you are not paying for the extra 150 RU/s available to you.</span></span>

<span data-ttu-id="1267f-164">S2 koleksiyonu 1 K RU/s ile bir tek bölümlü bir koleksiyon için bir geçişi yapılmaz.</span><span class="sxs-lookup"><span data-stu-id="1267f-164">If you have an S2 collection, you will be migrated to a single partition collection with 1 K RU/s.</span></span> <span data-ttu-id="1267f-165">Herhangi bir değişiklik, üretilen iş düzeyi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="1267f-165">You will see no change to your throughput level.</span></span>

<span data-ttu-id="1267f-166">S3 koleksiyonu 2,5 K RU/s ile bir tek bölümlü bir koleksiyon için bir geçişi yapılmaz.</span><span class="sxs-lookup"><span data-stu-id="1267f-166">If you have an S3 collection, you will be migrated to a single partition collection with 2.5 K RU/s.</span></span> <span data-ttu-id="1267f-167">Herhangi bir değişiklik, üretilen iş düzeyi görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="1267f-167">You will see no change to your throughput level.</span></span>

<span data-ttu-id="1267f-168">Koleksiyonunuz geçirildikten sonra her durumda, üretilen iş düzeyi özelleştirebilir ya da yukarı ve aşağı kullanıcılarınız için düşük gecikmeli erişim sağlamak için gerektiği şekilde ölçeklendirme kuramaz.</span><span class="sxs-lookup"><span data-stu-id="1267f-168">In each of these cases, after your collection is migrated, you will be able to customize your throughput level, or scale it up and down as needed to provide low-latency access to your users.</span></span> <span data-ttu-id="1267f-169">Koleksiyonunuz geçirildikten sonra işleme düzeyini değiştirmek için yalnızca Azure portalında Cosmos DB hesabınızı açın, Ölçek'ı tıklatın, koleksiyonunuzu seçin ve sonra aşağıdaki ekran görüntüsünde gösterildiği gibi üretilen iş düzeyi ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="1267f-169">To change the throughput level after your collection has migrated, simply open your Cosmos DB account in the Azure portal, click Scale, choose your collection, and then adjust the throughput level, as shown in the following screenshot:</span></span>

![Azure portalında üretilen iş ölçeklendirme](./media/performance-levels/portal-scale-throughput.png)

<a name="billing-change"></a>

## <a name="how-will-my-billing-change-after-im-migrated-to-the-single-partition-collections"></a><span data-ttu-id="1267f-171">Tek bölüm koleksiyonları geçişi sonra nasıl my faturalama değişir mi?</span><span class="sxs-lookup"><span data-stu-id="1267f-171">How will my billing change after I’m migrated to the single partition collections?</span></span>

<span data-ttu-id="1267f-172">Varsayılmıştır 10 S1 koleksiyonları, 1 GB depolama alanı BİZE Doğu bölgede her sahiptir ve 10 tek bölüm koleksiyonları 400 RU/sn (en düşük düzey), bu 10 S1 koleksiyonlarını geçirme.</span><span class="sxs-lookup"><span data-stu-id="1267f-172">Assuming you have 10 S1 collections, 1 GB of storage for each, in the US East region, and you migrate these 10 S1 collections to 10 single partition collections at 400 RU/sec (the minimum level).</span></span> <span data-ttu-id="1267f-173">Tam bir ay için 10 tek bölüm koleksiyonları tutarsanız faturanızı şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="1267f-173">Your bill will look as follows if you keep the 10 single partition collections for a full month:</span></span>

![Nasıl S1 10 koleksiyonlar için fiyatlandırma tek bölümlü bir koleksiyon için fiyatlandırma kullanarak 10 koleksiyonları karşılaştırır](./media/performance-levels/s1-vs-standard-pricing.png)

<a name="more-storage-needed"></a>

## <a name="what-if-i-need-more-than-10-gb-of-storage"></a><span data-ttu-id="1267f-175">Ne birden fazla 10 GB depolama alanı ihtiyacım var?</span><span class="sxs-lookup"><span data-stu-id="1267f-175">What if I need more than 10 GB of storage?</span></span>

<span data-ttu-id="1267f-176">S1, S2 ve S3 bir performans düzeyine sahip bir koleksiyona sahip, mı da 10 GB depolama alanı kullanılabilir Cosmos DB veri geçiş aracı verilerinizi ile bölümlenmiş bir koleksiyon neredeyse geçirmek için kullanabileceğiniz sahip tek bölümlü bir koleksiyon, sahip Sınırsız depolama.</span><span class="sxs-lookup"><span data-stu-id="1267f-176">Whether you have a collection with an S1, S2, or S3 performance level, or have a single partition collection, all of which have 10 GB of storage available, you can use the Cosmos DB Data Migration tool to migrate your data to a partitioned collection with virtually unlimited storage.</span></span> <span data-ttu-id="1267f-177">Bölümlendirilmiş bir koleksiyon avantajları hakkında daha fazla bilgi için bkz [bölümleme ve Azure Cosmos DB'de ölçeklendirme](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="1267f-177">For information about the benefits of a partitioned collection, see [Partitioning and scaling in Azure Cosmos DB](documentdb-partition-data.md).</span></span> <span data-ttu-id="1267f-178">S1, S2, S3 veya tek bölümlü bir koleksiyon için bölümlendirilmiş bir koleksiyon geçirme hakkında daha fazla bilgi için bkz: [tek bölümünden bölümlenmiş koleksiyonlar için geçiş](documentdb-partition-data.md#migrating-from-single-partition).</span><span class="sxs-lookup"><span data-stu-id="1267f-178">For information about how to migrate your S1, S2, S3, or single partition collection to a partitioned collection, see [Migrating from single-partition to partitioned collections](documentdb-partition-data.md#migrating-from-single-partition).</span></span> 

<a name="change-before"></a>

## <a name="can-i-change-between-the-s1-s2-and-s3-performance-levels-before-august-1-2017"></a><span data-ttu-id="1267f-179">S1, S2 ve S3 performans düzeyleri 1 Ağustos 2017 önce değiştirebilirim?</span><span class="sxs-lookup"><span data-stu-id="1267f-179">Can I change between the S1, S2, and S3 performance levels before August 1, 2017?</span></span>

<span data-ttu-id="1267f-180">Yalnızca var olan hesapları S1, S2 ve S3 performansı ile değiştirin ve performans düzeyi katmanları portalı üzerinden veya program aracılığıyla alter mümkün olacaktır.</span><span class="sxs-lookup"><span data-stu-id="1267f-180">Only existing accounts with S1, S2, and S3 performance will be able to change and alter performance level tiers through the portal or programmatically.</span></span> <span data-ttu-id="1267f-181">Ağustos 1 2017, S1, S2 ve S3 performans düzeyleri artık kullanılabilir olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="1267f-181">By August 1, 2017, the S1, S2, and S3 performance levels will no longer be available.</span></span> <span data-ttu-id="1267f-182">Tek bölümlü bir koleksiyon için S1, S3 veya S3 değiştirirseniz, S1, S2 ve S3 performans düzeyleri döndüremez.</span><span class="sxs-lookup"><span data-stu-id="1267f-182">If you change from S1, S3, or S3 to a single partition collection, you cannot return to the S1, S2, or S3 performance levels.</span></span>

<a name="when-migrated"></a>

## <a name="how-will-i-know-when-my-collection-has-migrated"></a><span data-ttu-id="1267f-183">Ne zaman kendi koleksiyonuma geçirildiğini nasıl anlarım?</span><span class="sxs-lookup"><span data-stu-id="1267f-183">How will I know when my collection has migrated?</span></span>

<span data-ttu-id="1267f-184">Geçiş 31 Temmuz 2017 üzerinde meydana gelir.</span><span class="sxs-lookup"><span data-stu-id="1267f-184">The migration will occur on July 31, 2017.</span></span> <span data-ttu-id="1267f-185">S1 kullanan bir koleksiyon varsa, geçiş gerçekleşmeden önce S2 veya S3 performans düzeyleri, Cosmos DB takım, e-posta ile başvurun.</span><span class="sxs-lookup"><span data-stu-id="1267f-185">If you have a collection that uses the S1, S2 or S3 performance levels, the Cosmos DB team will contact you by email before the migration takes place.</span></span> <span data-ttu-id="1267f-186">Geçiş 1 Ağustos 2017 üzerinde tamamlandığında, Azure portalında koleksiyonunuzu standart fiyatlandırma kullandığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="1267f-186">Once the migration is complete, on August 1, 2017, the Azure portal will show that your collection uses Standard pricing.</span></span>

![Fiyatlandırma katmanı standart koleksiyonunuzu onaylamak nasıl geçirildiğini](./media/performance-levels/portal-standard-pricing-applied.png)

<a name="migrate-diy"></a>

## <a name="how-do-i-migrate-from-the-s1-s2-s3-performance-levels-to-single-partition-collections-on-my-own"></a><span data-ttu-id="1267f-188">S3 performans düzeyleri üzerinde kendi tek bölüm koleksiyonları nasıl S1, S2, geçişini?</span><span class="sxs-lookup"><span data-stu-id="1267f-188">How do I migrate from the S1, S2, S3 performance levels to single partition collections on my own?</span></span>

<span data-ttu-id="1267f-189">Azure Portalı'nı kullanarak tek bölüm koleksiyonları S1, S2 ve S3 performans düzeylerinden geçirebileceğiniz veya program aracılığıyla.</span><span class="sxs-lookup"><span data-stu-id="1267f-189">You can migrate from the S1, S2, and S3 performance levels to single partition collections using the Azure portal or programmatically.</span></span> <span data-ttu-id="1267f-190">Kendinize ait olan tek bölüm koleksiyonları esnek işleme seçenekleri yararlanmasını 1 Ağustos önce bunu yapabilirsiniz veya koleksiyonlarınızı sizin için 31 Temmuz 2017 üzerinde geçirirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1267f-190">You can do this on your own before August 1 to benefit from the flexible throughput options available with single partition collections, or we will migrate your collections for you on July 31, 2017.</span></span>

<span data-ttu-id="1267f-191">**Azure Portalı'nı kullanarak tek bölüm koleksiyonları geçirmek için**</span><span class="sxs-lookup"><span data-stu-id="1267f-191">**To migrate to single partition collections using the Azure portal**</span></span>

1. <span data-ttu-id="1267f-192">İçinde [ **Azure portal**](https://portal.azure.com), tıklatın **Azure Cosmos DB**, sonra değiştirmek için Cosmos DB hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="1267f-192">In the [**Azure portal**](https://portal.azure.com), click **Azure Cosmos DB**, then select the Cosmos DB account to modify.</span></span> 
 
    <span data-ttu-id="1267f-193">Varsa **Azure Cosmos DB** olan atlama çubuğu değil üzerinde tıklayın >, kaydırın **veritabanları**seçin **Azure Cosmos DB**ve DocumentDB hesabı seçin.</span><span class="sxs-lookup"><span data-stu-id="1267f-193">If **Azure Cosmos DB** is not on the Jumpbar, click >, scroll to **Databases**, select **Azure Cosmos DB**, and then select the DocumentDB account.</span></span>  

2. <span data-ttu-id="1267f-194">Kaynak menüsünde altında **kapsayıcıları**, tıklatın **ölçek**, aşağı açılan listeden değiştirin ve ardından istediğiniz koleksiyonu seçmek **fiyatlandırma katmanı**.</span><span class="sxs-lookup"><span data-stu-id="1267f-194">On the resource menu, under **Containers**, click **Scale**, select the collection to modify from the drop-down list, and then click **Pricing Tier**.</span></span> <span data-ttu-id="1267f-195">Önceden tanımlanmış verimlilik kullanarak hesapları S1, S2 ve S3 fiyatlandırma katmanı vardır.</span><span class="sxs-lookup"><span data-stu-id="1267f-195">Accounts using pre-defined throughput have a pricing tier of S1, S2, or S3.</span></span>  <span data-ttu-id="1267f-196">İçinde **fiyatlandırma katmanınızı seçin** dikey penceresinde tıklatın **standart** kullanıcı tanımlı verimlilik değiştirin ve ardından **seçin** değişikliklerinizi kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="1267f-196">In the **Choose your pricing tier** blade, click **Standard** to change to user-defined throughput, and then click **Select** to save your change.</span></span>

    ![Üretilen iş değerini değiştirmek nereye gösteren ayarlar dikey penceresi ekran görüntüsü](./media/performance-levels/change-performance-set-thoughput.png)

3. <span data-ttu-id="1267f-198">Geri **ölçek** dikey penceresinde **fiyatlandırma katmanı** değiştirilir **standart** ve **üretilen işi (RU/s)** kutusu ile bir varsayılan görüntülenir 400 değeri.</span><span class="sxs-lookup"><span data-stu-id="1267f-198">Back in the **Scale** blade, the **Pricing Tier** is changed to **Standard** and the **Throughput (RU/s)** box is displayed with a default value of 400.</span></span> <span data-ttu-id="1267f-199">İşleme 400-10.000 arasında ayarlamak [istek birimleri](request-units.md)/second (RU/s).</span><span class="sxs-lookup"><span data-stu-id="1267f-199">Set the throughput between 400 and 10,000 [Request units](request-units.md)/second (RU/s).</span></span> <span data-ttu-id="1267f-200">**Tahmini aylık fatura** aylık maliyeti tahmini otomatik olarak sağlamak üzere Sayfa güncelleştirmelerini sonundaki.</span><span class="sxs-lookup"><span data-stu-id="1267f-200">The **Estimated Monthly Bill** at the bottom of the page updates automatically to provide an estimate of the monthly cost.</span></span> 

    >[!IMPORTANT] 
    > <span data-ttu-id="1267f-201">Yaptığınız değişiklikleri kaydedin ve fiyatlandırma katmanı standart taşıma sonra S1, S2 ve S3 performans düzeyleri için geri alamazsınız.</span><span class="sxs-lookup"><span data-stu-id="1267f-201">Once you save your changes and move to the Standard pricing tier, you cannot roll back to the S1, S2, or S3 performance levels.</span></span>

4. <span data-ttu-id="1267f-202">Tıklatın **kaydetmek** yaptığınız değişiklikleri kaydetmek için.</span><span class="sxs-lookup"><span data-stu-id="1267f-202">Click **Save** to save your changes.</span></span>

    <span data-ttu-id="1267f-203">Daha fazla verimlilik (10. 000'ru / s büyük) veya daha fazla depolama alanı (10 GB'den büyük) gerekli belirlerseniz, bölümlendirilmiş bir koleksiyon oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1267f-203">If you determine that you need more throughput (greater than 10,000 RU/s) or more storage (greater than 10GB) you can create a partitioned collection.</span></span> <span data-ttu-id="1267f-204">Tek bölümlü bir koleksiyon için bölümlendirilmiş bir koleksiyon geçirmek için bkz [tek bölümünden bölümlenmiş koleksiyonlar için geçiş](documentdb-partition-data.md#migrating-from-single-partition).</span><span class="sxs-lookup"><span data-stu-id="1267f-204">To migrate a single partition collection to a partitioned collection, see [Migrating from single-partition to partitioned collections](documentdb-partition-data.md#migrating-from-single-partition).</span></span>

    > [!NOTE]
    > <span data-ttu-id="1267f-205">Standart S1, S2 ve S3 değiştirme, 2 dakika kadar sürebilir.</span><span class="sxs-lookup"><span data-stu-id="1267f-205">Changing from S1, S2, or S3 to Standard may take up to 2 minutes.</span></span>
    > 
    > 

<span data-ttu-id="1267f-206">**.NET SDK kullanarak tek bölüm koleksiyonları geçirmek için**</span><span class="sxs-lookup"><span data-stu-id="1267f-206">**To migrate to single partition collections using the .NET SDK**</span></span>

<span data-ttu-id="1267f-207">Koleksiyonlarınızı performans düzeylerini değiştirmek için başka bir seçenek bizim SDK olur.</span><span class="sxs-lookup"><span data-stu-id="1267f-207">Another option for changing your collections' performance levels is through our SDKs.</span></span> <span data-ttu-id="1267f-208">Bu bölüm, yalnızca bir koleksiyona ait performansının değiştirilmesi kapsar kullanarak düzey bizim [DocumentDB .NET API](documentdb-sdk-dotnet.md), ancak bizim diğer SDK için benzer bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="1267f-208">This section only covers changing a collection's performance level using our [DocumentDB .NET API](documentdb-sdk-dotnet.md), but the process is similar for our other SDKs.</span></span>

<span data-ttu-id="1267f-209">Saniye başına 5.000 istek birimlerine koleksiyonu verimlilik değiştirmek için bir kod parçacığı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="1267f-209">Here is a code snippet for changing the collection throughput to 5,000 request units per second:</span></span>
    
```C#
    //Fetch the resource to be updated
    Offer offer = client.CreateOfferQuery()
                      .Where(r => r.ResourceLink == collection.SelfLink)    
                      .AsEnumerable()
                      .SingleOrDefault();

    // Set the throughput to 5000 request units per second
    offer = new OfferV2(offer, 5000);

    //Now persist these changes to the database by replacing the original resource
    await client.ReplaceOfferAsync(offer);
```

<span data-ttu-id="1267f-210">Ziyaret [MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx) ek örnekler görüntüleyip bizim teklif yöntemleri hakkında daha fazla bilgi için:</span><span class="sxs-lookup"><span data-stu-id="1267f-210">Visit [MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx) to view additional examples and learn more about our offer methods:</span></span>

* [<span data-ttu-id="1267f-211">**ReadOfferAsync**</span><span class="sxs-lookup"><span data-stu-id="1267f-211">**ReadOfferAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readofferasync.aspx)
* [<span data-ttu-id="1267f-212">**ReadOffersFeedAsync**</span><span class="sxs-lookup"><span data-stu-id="1267f-212">**ReadOffersFeedAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readoffersfeedasync.aspx)
* [<span data-ttu-id="1267f-213">**ReplaceOfferAsync**</span><span class="sxs-lookup"><span data-stu-id="1267f-213">**ReplaceOfferAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.replaceofferasync.aspx)
* [<span data-ttu-id="1267f-214">**CreateOfferQuery**</span><span class="sxs-lookup"><span data-stu-id="1267f-214">**CreateOfferQuery**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.linq.documentqueryable.createofferquery.aspx)

<a name="ea-customer"></a>

## <a name="how-am-i-impacted-if-im-an-ea-customer"></a><span data-ttu-id="1267f-215">Nasıl bir EA müşteri ben varsa ı etkilenen?</span><span class="sxs-lookup"><span data-stu-id="1267f-215">How am I impacted if I'm an EA customer?</span></span>

<span data-ttu-id="1267f-216">EA müşteriler kendi geçerli sözleşmenin sonuna kadar korumalı fiyat olacaktır.</span><span class="sxs-lookup"><span data-stu-id="1267f-216">EA customers will be price protected until the end of their current contract.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1267f-217">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1267f-217">Next steps</span></span>
<span data-ttu-id="1267f-218">Fiyatlandırma ve Azure Cosmos DB ile verileri yönetme hakkında daha fazla bilgi edinmek için şu kaynakları araştırın:</span><span class="sxs-lookup"><span data-stu-id="1267f-218">To learn more about pricing and managing data with Azure Cosmos DB, explore these resources:</span></span>

1.  <span data-ttu-id="1267f-219">[Cosmos DB'de veri bölümlendirme](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="1267f-219">[Partitioning data in Cosmos DB](documentdb-partition-data.md).</span></span> <span data-ttu-id="1267f-220">Tek bölümlü bir kapsayıcı ve bölümlenmiş kapsayıcıları yanı sıra, sorunsuz bir şekilde ölçeklendirmek için bölümleme stratejisine uygulama ipuçları arasındaki farkı anlama.</span><span class="sxs-lookup"><span data-stu-id="1267f-220">Understand the difference between single partition container and partitioned containers, as well as tips on implementing a partitioning strategy to scale seamlessly.</span></span>
2.  <span data-ttu-id="1267f-221">[Cosmos DB fiyatlandırma](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="1267f-221">[Cosmos DB pricing](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span> <span data-ttu-id="1267f-222">Üretilen iş sağlama ve depolama tüketme maliyeti hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="1267f-222">Learn about the cost of provisioning throughput and consuming storage.</span></span>
3.  <span data-ttu-id="1267f-223">[İstek birimleri](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="1267f-223">[Request units](request-units.md).</span></span> <span data-ttu-id="1267f-224">Farklı işlem türleri için örneğin okuma, yazma, sorgu işleme tüketiminin anlayın.</span><span class="sxs-lookup"><span data-stu-id="1267f-224">Understand the consumption of throughput for different operation types, for example Read, Write, Query.</span></span>
