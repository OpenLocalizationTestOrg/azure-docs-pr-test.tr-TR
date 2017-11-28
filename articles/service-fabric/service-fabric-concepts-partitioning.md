---
title: aaaPartitioning Service Fabric Hizmetleri | Microsoft Docs
description: "Açıklar nasıl toopartition Service Fabric durum bilgisi olan hizmetler. Bölümler, veri ve işlem birlikte Genişletilebilir şekilde hello yerel makinede veri depolama sağlar."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 3b7248c8-ea92-4964-85e7-6f1291b5cc7b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: msfussell
ms.openlocfilehash: 6ead48716c08f4212535202ee69d169067d5c6d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="partition-service-fabric-reliable-services"></a><span data-ttu-id="6703f-104">Bölüm Service Fabric güvenilir hizmetler</span><span class="sxs-lookup"><span data-stu-id="6703f-104">Partition Service Fabric reliable services</span></span>
<span data-ttu-id="6703f-105">Bu makale, Azure Service Fabric güvenilir hizmetler bölümleme temel kavramları giriş toohello sağlar.</span><span class="sxs-lookup"><span data-stu-id="6703f-105">This article provides an introduction toohello basic concepts of partitioning Azure Service Fabric reliable services.</span></span> <span data-ttu-id="6703f-106">Merhaba hello makalede kullanılan kaynak kodunu da kullanılabilir [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span><span class="sxs-lookup"><span data-stu-id="6703f-106">hello source code used in hello article is also available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="partitioning"></a><span data-ttu-id="6703f-107">Bölümleme</span><span class="sxs-lookup"><span data-stu-id="6703f-107">Partitioning</span></span>
<span data-ttu-id="6703f-108">Bölümleme benzersiz tooService doku değil.</span><span class="sxs-lookup"><span data-stu-id="6703f-108">Partitioning is not unique tooService Fabric.</span></span> <span data-ttu-id="6703f-109">Aslında, ölçeklenebilir hizmetler oluşturmaya bir çekirdek desenini değil.</span><span class="sxs-lookup"><span data-stu-id="6703f-109">In fact, it is a core pattern of building scalable services.</span></span> <span data-ttu-id="6703f-110">Daha geniş anlamda, biz durumu (veri) ayırma kavram olarak bölümlendirme hakkında düşünün ve daha küçük erişilebilir birimleri tooimprove ölçeklenebilirlik ve performans işlem.</span><span class="sxs-lookup"><span data-stu-id="6703f-110">In a broader sense, we can think about partitioning as a concept of dividing state (data) and compute into smaller accessible units tooimprove scalability and performance.</span></span> <span data-ttu-id="6703f-111">Bölümlendirme, iyi bilinen bir form [veri bölümlendirme][wikipartition], parçalama olarak da bilinir.</span><span class="sxs-lookup"><span data-stu-id="6703f-111">A well-known form of partitioning is [data partitioning][wikipartition], also known as sharding.</span></span>

### <a name="partition-service-fabric-stateless-services"></a><span data-ttu-id="6703f-112">Bölüm Service Fabric durum bilgisi olmayan hizmetler</span><span class="sxs-lookup"><span data-stu-id="6703f-112">Partition Service Fabric stateless services</span></span>
<span data-ttu-id="6703f-113">Durum bilgisi olmayan hizmetler için bir hizmet bir veya daha fazla örneklerini içeren bir birimi olan bir bölüm hakkında düşünebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6703f-113">For stateless services, you can think about a partition being a logical unit that contains one or more instances of a service.</span></span> <span data-ttu-id="6703f-114">Şekil 1 bir durum bilgisi olmayan hizmetin bir bölüm kullanarak bir kümede dağıtılmış beş örneğiyle gösterir.</span><span class="sxs-lookup"><span data-stu-id="6703f-114">Figure 1 shows a stateless service with five instances distributed across a cluster using one partition.</span></span>

![Durum bilgisiz hizmeti](./media/service-fabric-concepts-partitioning/statelessinstances.png)

<span data-ttu-id="6703f-116">Gerçekten durum bilgisiz hizmet çözümlerine iki tür vardır.</span><span class="sxs-lookup"><span data-stu-id="6703f-116">There are really two types of stateless service solutions.</span></span> <span data-ttu-id="6703f-117">Merhaba ilk durumuna harici olarak örneğin (gibi hello oturum bilgilerini ve veri depolayan bir Web sitesi) bir Azure SQL veritabanında kalıcı bir hizmet biridir.</span><span class="sxs-lookup"><span data-stu-id="6703f-117">hello first one is a service that persists its state externally, for example in an Azure SQL database (like a website that stores hello session information and data).</span></span> <span data-ttu-id="6703f-118">Merhaba ikinci herhangi kalıcı durumunu yönetme değil yalnızca Hesaplama Hizmetleri (örneğin, bir hesap makinesi veya görüntü küçük resim oluşturma) olabilir.</span><span class="sxs-lookup"><span data-stu-id="6703f-118">hello second one is computation-only services (like a calculator or image thumbnailing) that do not manage any persistent state.</span></span>

<span data-ttu-id="6703f-119">İçinde bir durum bilgisi olmayan hizmetin bölümlendirme, çok nadir bir senaryo--ölçeklenebilirlik bir durumdur ve kullanılabilirlik normalde elde fazla örneğe ekleyerek.</span><span class="sxs-lookup"><span data-stu-id="6703f-119">In either case, partitioning a stateless service is a very rare scenario--scalability and availability are normally achieved by adding more instances.</span></span> <span data-ttu-id="6703f-120">Durum bilgisiz hizmet örnekleri için birden çok bölüm toomeet özel yönlendirme ihtiyacınız olduğunda tooconsider istediğiniz hello yalnızca zamanı ister.</span><span class="sxs-lookup"><span data-stu-id="6703f-120">hello only time you want tooconsider multiple partitions for stateless service instances is when you need toomeet special routing requests.</span></span>

<span data-ttu-id="6703f-121">Örnek olarak, burada belirli bir aralıkla kimlikleri kullanıcılar yalnızca belirli bir hizmet örneği tarafından sunulması bir durum düşünün.</span><span class="sxs-lookup"><span data-stu-id="6703f-121">As an example, consider a case where users with IDs in a certain range should only be served by a particular service instance.</span></span> <span data-ttu-id="6703f-122">Gerçekten bölümlenmiş arka uç (ör parçalı SQL veritabanı) sahip ve hangi hizmet örneğine toohello veritabanı parça--yazma veya diğer hazırlık işlemleri içinde gerçekleştirmesi toocontrol istediğinizde bir durum bilgisi olmayan hizmetin ne zaman bölüm, başka bir örnek verilmiştir Merhaba gerektiren durum bilgisiz hizmete hello aynı hello arka kullanılan bölümlenme bilgisi.</span><span class="sxs-lookup"><span data-stu-id="6703f-122">Another example of when you could partition a stateless service is when you have a truly partitioned backend (e.g. a sharded SQL database) and you want toocontrol which service instance should write toohello database shard--or perform other preparation work within hello stateless service that requires hello same partitioning information as is used in hello backend.</span></span> <span data-ttu-id="6703f-123">Bu senaryo türlerini farklı şekillerde çözülebilir ve hizmet bölümleme gerektirmeyebilecek.</span><span class="sxs-lookup"><span data-stu-id="6703f-123">Those types of scenarios can also be solved in different ways and do not necessarily require service partitioning.</span></span>

<span data-ttu-id="6703f-124">Bu kılavuzda Hello kalanı durum bilgisi olan hizmetler odaklanır.</span><span class="sxs-lookup"><span data-stu-id="6703f-124">hello remainder of this walkthrough focuses on stateful services.</span></span>

### <a name="partition-service-fabric-stateful-services"></a><span data-ttu-id="6703f-125">Bölüm Service Fabric durum bilgisi olan hizmetler</span><span class="sxs-lookup"><span data-stu-id="6703f-125">Partition Service Fabric stateful services</span></span>
<span data-ttu-id="6703f-126">Service Fabric kılar kolay toodevelop ölçeklenebilir durum bilgisi olan hizmetler birinci sınıf bir yöntem sunarak toopartition durumu (veri).</span><span class="sxs-lookup"><span data-stu-id="6703f-126">Service Fabric makes it easy toodevelop scalable stateful services by offering a first-class way toopartition state (data).</span></span> <span data-ttu-id="6703f-127">Üzerinden yüksek oranda güvenilir bir ölçek birimi olarak bir durum bilgisi olan hizmet bölüm hakkında kavramsal olarak, düşünebilirsiniz [çoğaltmaları](service-fabric-availability-services.md) , dağıtılmış ve bir kümede hello düğümleri arasında dengeli.</span><span class="sxs-lookup"><span data-stu-id="6703f-127">Conceptually, you can think about a partition of a stateful service as a scale unit that is highly reliable through [replicas](service-fabric-availability-services.md) that are distributed and balanced across hello nodes in a cluster.</span></span>

<span data-ttu-id="6703f-128">Service Fabric durum bilgisi olan hizmetler Hello bağlamında bölümleme toohello işleminin belirli bir hizmet bölümü hello tam hello hizmetinin durumunu bir kısmı için sorumlu olduğunu belirleme anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="6703f-128">Partitioning in hello context of Service Fabric stateful services refers toohello process of determining that a particular service partition is responsible for a portion of hello complete state of hello service.</span></span> <span data-ttu-id="6703f-129">(Önce belirtildiği gibi bir bölüm kümesidir [çoğaltmaları](service-fabric-availability-services.md)).</span><span class="sxs-lookup"><span data-stu-id="6703f-129">(As mentioned before, a partition is a set of [replicas](service-fabric-availability-services.md)).</span></span> <span data-ttu-id="6703f-130">Service Fabric hakkında önemli bir şey, bunu hello bölümleri farklı düğümlerde yerleştirir ' dir.</span><span class="sxs-lookup"><span data-stu-id="6703f-130">A great thing about Service Fabric is that it places hello partitions on different nodes.</span></span> <span data-ttu-id="6703f-131">Bu toogrow tooa düğümün kaynak sınırı sağlar.</span><span class="sxs-lookup"><span data-stu-id="6703f-131">This allows them toogrow tooa node's resource limit.</span></span> <span data-ttu-id="6703f-132">Merhaba veri büyüme gereksinimlerine göre bölümleri büyümesine ve Service Fabric bölümleri düğümleri arasında yeniden dengeler.</span><span class="sxs-lookup"><span data-stu-id="6703f-132">As hello data needs grow, partitions grow, and Service Fabric rebalances partitions across nodes.</span></span> <span data-ttu-id="6703f-133">Bu, hello devam donanım kaynaklarını verimli bir şekilde kullanılmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="6703f-133">This ensures hello continued efficient use of hardware resources.</span></span>

<span data-ttu-id="6703f-134">toogive bir örnek söylenebilir, 5 düğümlü bir küme ve yapılandırılmış toohave 10 bölümler ve üç çoğaltmaları hedefi bir hizmet ile başlar.</span><span class="sxs-lookup"><span data-stu-id="6703f-134">toogive you an example, say you start with a 5-node cluster and a service that is configured toohave 10 partitions and a target of three replicas.</span></span> <span data-ttu-id="6703f-135">Bu durumda, Service Fabric dengelemek ve hello çoğaltmalar Merhaba kümede--dağıtır ve iki birincil ile bitecek [çoğaltmaları](service-fabric-availability-services.md) düğüm başına.</span><span class="sxs-lookup"><span data-stu-id="6703f-135">In this case, Service Fabric would balance and distribute hello replicas across hello cluster--and you would end up with two primary [replicas](service-fabric-availability-services.md) per node.</span></span>
<span data-ttu-id="6703f-136">Merhaba küme too10 düğümleri kullanıma tooscale artık ihtiyacınız varsa, Service Fabric hello birincil yeniden dengelemeniz [çoğaltmaları](service-fabric-availability-services.md) tüm 10 düğümleri arasında.</span><span class="sxs-lookup"><span data-stu-id="6703f-136">If you now need tooscale out hello cluster too10 nodes, Service Fabric would rebalance hello primary [replicas](service-fabric-availability-services.md) across all 10 nodes.</span></span> <span data-ttu-id="6703f-137">Geri too5 düğümleri ölçeği, benzer şekilde, Service Fabric tüm hello çoğaltmalar Merhaba 5 düğümleri arasında yeniden dengelemeniz.</span><span class="sxs-lookup"><span data-stu-id="6703f-137">Likewise, if you scaled back too5 nodes, Service Fabric would rebalance all hello replicas across hello 5 nodes.</span></span>  

<span data-ttu-id="6703f-138">Şekil 2 önce ve sonra hello küme ölçeklendirme 10 bölümlerinin hello dağılımını gösterir.</span><span class="sxs-lookup"><span data-stu-id="6703f-138">Figure 2 shows hello distribution of 10 partitions before and after scaling hello cluster.</span></span>

![Durum bilgisi olan hizmet](./media/service-fabric-concepts-partitioning/partitions.png)

<span data-ttu-id="6703f-140">Sonuç olarak, hello genişleme istemcilerinden gelen istekleri bilgisayarlar arasında dağıtılır, hello uygulamasının genel performansı geliştirildi ve veri erişim toochunks üzerinde Çekişme sınırlı olduğundan elde edilir.</span><span class="sxs-lookup"><span data-stu-id="6703f-140">As a result, hello scale-out is achieved since requests from clients are distributed across computers, overall performance of hello application is improved, and contention on access toochunks of data is reduced.</span></span>

## <a name="plan-for-partitioning"></a><span data-ttu-id="6703f-141">Bölümleme planlama</span><span class="sxs-lookup"><span data-stu-id="6703f-141">Plan for partitioning</span></span>
<span data-ttu-id="6703f-142">Bir hizmet uygulamadan önce her zaman kullanıma gerekli tooscale stratejisi bölümleme hello düşünmelisiniz. Farklı yolu vardır, ancak bunların tümünün hangi Merhaba uygulaması tooachieve gereken odaklanın.</span><span class="sxs-lookup"><span data-stu-id="6703f-142">Before implementing a service, you should always consider hello partitioning strategy that is required tooscale out. There are different ways, but all of them focus on what hello application needs tooachieve.</span></span> <span data-ttu-id="6703f-143">Bu makalede Hello bağlamının şimdi hello bazıları daha önemli yönlerinden göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="6703f-143">For hello context of this article, let's consider some of hello more important aspects.</span></span>

<span data-ttu-id="6703f-144">Toothink hello yapısı, hello ilk adım olarak bölümlenmiş toobe gereken hello durumu hakkında bir iyi yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="6703f-144">A good approach is toothink about hello structure of hello state that needs toobe partitioned, as hello first step.</span></span>

<span data-ttu-id="6703f-145">Basit bir örnek atalım.</span><span class="sxs-lookup"><span data-stu-id="6703f-145">Let's take a simple example.</span></span> <span data-ttu-id="6703f-146">Toobuild countywide yoklama için bir hizmet olsaydı, her şehir için bir bölüm hello ilçe oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6703f-146">If you were toobuild a service for a countywide poll, you could create a partition for each city in hello county.</span></span> <span data-ttu-id="6703f-147">Ardından, toothat Şehir karşılık gelen hello bölümünde hello şehirde hello oyları her kişi için saklayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6703f-147">Then, you could store hello votes for every person in hello city in hello partition that corresponds toothat city.</span></span> <span data-ttu-id="6703f-148">Şekil 3'içinde bulundukları kişiler ve hello Şehir kümesi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="6703f-148">Figure 3 illustrates a set of people and hello city in which they reside.</span></span>

![Basit bölüm](./media/service-fabric-concepts-partitioning/cities.png)

<span data-ttu-id="6703f-150">Şehir Hello popülasyonunu yaygın değiştikçe, çok miktarda veri (örneğin, Seattle) içeren bazı bölümleri ve çok az durumu (örneğin Kirkland) ile diğer bölümleri ile bitirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6703f-150">As hello population of cities varies widely, you may end up with some partitions that contain a lot of data (e.g. Seattle) and other partitions with very little state (e.g. Kirkland).</span></span> <span data-ttu-id="6703f-151">Bu nedenle durumu eşit miktarda bölümlemeye sahip olmak hello etkisi nedir?</span><span class="sxs-lookup"><span data-stu-id="6703f-151">So what is hello impact of having partitions with uneven amounts of state?</span></span>

<span data-ttu-id="6703f-152">Merhaba örneği hakkında yeniden düşünüyorsanız, Seattle için hello oylarının tutan hello bölüm hello Kirkland bir değerinden daha fazla trafik alırsınız kolayca görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6703f-152">If you think about hello example again, you can easily see that hello partition that holds hello votes for Seattle will get more traffic than hello Kirkland one.</span></span> <span data-ttu-id="6703f-153">Varsayılan olarak, Service Fabric hello hakkında emin yapar birincil ve ikincil çoğaltmaları her düğümde aynı sayıda.</span><span class="sxs-lookup"><span data-stu-id="6703f-153">By default, Service Fabric makes sure that there is about hello same number of primary and secondary replicas on each node.</span></span> <span data-ttu-id="6703f-154">Bu nedenle, daha az trafik hizmet daha fazla trafik ve diğerleri hizmet çoğaltmaları tutun düğümleriyle bitirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6703f-154">So you may end up with nodes that hold replicas that serve more traffic and others that serve less traffic.</span></span> <span data-ttu-id="6703f-155">Soğuk noktalar bu bir kümede gibi ve, tercihen tooavoid etkin istersiniz.</span><span class="sxs-lookup"><span data-stu-id="6703f-155">You would preferably want tooavoid hot and cold spots like this in a cluster.</span></span>

<span data-ttu-id="6703f-156">İçinde tooavoid Bu sipariş, bir bölümleme açısından iki şey yapmanız:</span><span class="sxs-lookup"><span data-stu-id="6703f-156">In order tooavoid this, you should do two things, from a partitioning point of view:</span></span>

* <span data-ttu-id="6703f-157">Böylece tüm bölümleri arasında eşit olarak dağıtılır toopartition hello durumu deneyin.</span><span class="sxs-lookup"><span data-stu-id="6703f-157">Try toopartition hello state so that it is evenly distributed across all partitions.</span></span>
* <span data-ttu-id="6703f-158">Rapor yük hello hizmeti için hello çoğaltmaları her biri.</span><span class="sxs-lookup"><span data-stu-id="6703f-158">Report load from each of hello replicas for hello service.</span></span> <span data-ttu-id="6703f-159">(Bu makalede hakkında daha fazla bilgi için kontrol [ölçümleri ve yük](service-fabric-cluster-resource-manager-metrics.md)).</span><span class="sxs-lookup"><span data-stu-id="6703f-159">(For information on how, check out this article on [Metrics and Load](service-fabric-cluster-resource-manager-metrics.md)).</span></span> <span data-ttu-id="6703f-160">Service Fabric bellek miktarı veya kayıt sayısı gibi hizmetleri tarafından tüketilen hello yetenek tooreport yük sağlar.</span><span class="sxs-lookup"><span data-stu-id="6703f-160">Service Fabric provides hello capability tooreport load consumed by services, such as amount of memory or number of records.</span></span> <span data-ttu-id="6703f-161">Hiçbir düğümü genel aşırı için bildirilen hello ölçülerine bağlı olarak, Service Fabric bazı bölümleri diğerlerinden daha yüksek yüklerini hizmet veren ve hello küme taşıma çoğaltmaları toomore uygun düğümleri tarafından yeniden dengeler algılar.</span><span class="sxs-lookup"><span data-stu-id="6703f-161">Based on hello metrics reported, Service Fabric detects that some partitions are serving higher loads than others and rebalances hello cluster by moving replicas toomore suitable nodes, so that overall no node is overloaded.</span></span>

<span data-ttu-id="6703f-162">Bazı durumlarda, ne kadar veri belli bir bölüm olacak bilemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="6703f-162">Sometimes, you cannot know how much data will be in a given partition.</span></span> <span data-ttu-id="6703f-163">Genel bir öneri toodo hem--olacak şekilde ilk olarak, bölümleme stratejisine kabul ederek, hello veri eşit hello bölümler ve saniye raporlama yük tarafından yayar.</span><span class="sxs-lookup"><span data-stu-id="6703f-163">So a general recommendation is toodo both--first, by adopting a partitioning strategy that spreads hello data evenly across hello partitions and second, by reporting load.</span></span>  <span data-ttu-id="6703f-164">Merhaba ilk yöntem hello ikinci erişim ya da yük geçici farklılıkları düzgünleştirme zamanla tutarken örnek, oylama hello açıklanan durumlarda engeller.</span><span class="sxs-lookup"><span data-stu-id="6703f-164">hello first method prevents situations described in hello voting example, while hello second helps smooth out temporary differences in access or load over time.</span></span>

<span data-ttu-id="6703f-165">Bölüm planlamanın bir diğer unsuru toochoose hello doğru bölümleri toobegin ile sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="6703f-165">Another aspect of partition planning is toochoose hello correct number of partitions toobegin with.</span></span>
<span data-ttu-id="6703f-166">Service Fabric açısından bakıldığında, hiçbir şey yoktur senaryonuz için beklenenden daha yüksek bir bölüm sayısı ile başlıyor engeller.</span><span class="sxs-lookup"><span data-stu-id="6703f-166">From a Service Fabric perspective, there is nothing that prevents you from starting out with a higher number of partitions than anticipated for your scenario.</span></span>
<span data-ttu-id="6703f-167">Aslında, hello en çok bölüm sayısı varsayarak bir geçerli bir yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="6703f-167">In fact, assuming hello maximum number of partitions is a valid approach.</span></span>

<span data-ttu-id="6703f-168">Nadir durumlarda, ilk başta seçtiğiniz olandan daha fazla bölüm gerek yukarı bitebilir.</span><span class="sxs-lookup"><span data-stu-id="6703f-168">In rare cases, you may end up needing more partitions than you have initially chosen.</span></span> <span data-ttu-id="6703f-169">Merhaba olaydan sonra hello bölüm sayısı değiştirilemez gibi bazı gelişmiş bölüm yaklaşımlar tooapply gerekir, hello yeni bir hizmet örneğini oluşturma gibi aynı hizmeti türü.</span><span class="sxs-lookup"><span data-stu-id="6703f-169">As you cannot change hello partition count after hello fact, you would need tooapply some advanced partition approaches, such as creating a new service instance of hello same service type.</span></span> <span data-ttu-id="6703f-170">Merhaba yönlendirir bazı istemci-tarafı mantığı toohello doğru hizmet örneği, istemci kodunuzun korumalıdır istemci-tarafı bilgisini temel alarak istekleri tooimplement de gerekir.</span><span class="sxs-lookup"><span data-stu-id="6703f-170">You would also need tooimplement some client-side logic that routes hello requests toohello correct service instance, based on client-side knowledge that your client code must maintain.</span></span>

<span data-ttu-id="6703f-171">Planlama bölümleme için başka bir hello mevcut bilgisayar kaynaklarına noktadır.</span><span class="sxs-lookup"><span data-stu-id="6703f-171">Another consideration for partitioning planning is hello available computer resources.</span></span> <span data-ttu-id="6703f-172">Merhaba durumu erişilen ve depolanan toobe gerektiği ilişkili toofollow şunlardır:</span><span class="sxs-lookup"><span data-stu-id="6703f-172">As hello state needs toobe accessed and stored, you are bound toofollow:</span></span>

* <span data-ttu-id="6703f-173">Ağ bant genişliği sınırları</span><span class="sxs-lookup"><span data-stu-id="6703f-173">Network bandwidth limits</span></span>
* <span data-ttu-id="6703f-174">Sistem bellek sınırları</span><span class="sxs-lookup"><span data-stu-id="6703f-174">System memory limits</span></span>
* <span data-ttu-id="6703f-175">Disk depolama sınırları</span><span class="sxs-lookup"><span data-stu-id="6703f-175">Disk storage limits</span></span>

<span data-ttu-id="6703f-176">Bu nedenle çalıştıran bir kümedeki kaynak kısıtlamaları içine çalıştırırsanız ne olur? Merhaba yanıt hello küme tooaccommodate hello yeni gereksinimlerini yalnızca ölçeklendirebilirsiniz ' dir.</span><span class="sxs-lookup"><span data-stu-id="6703f-176">So what happens if you run into resource constraints in a running cluster? hello answer is that you can simply scale out hello cluster tooaccommodate hello new requirements.</span></span>

<span data-ttu-id="6703f-177">[Merhaba kapasite planlama Kılavuzu](service-fabric-capacity-planning.md) ilişkin yönergeler sunar toodetermine kaç düğümleri kümenizi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="6703f-177">[hello capacity planning guide](service-fabric-capacity-planning.md) offers guidance for how toodetermine how many nodes your cluster needs.</span></span>

## <a name="get-started-with-partitioning"></a><span data-ttu-id="6703f-178">Bölümlendirme ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="6703f-178">Get started with partitioning</span></span>
<span data-ttu-id="6703f-179">Bu bölüm, hizmetinizi bölümlendirme ile tooget nasıl başlatılacağını açıklar.</span><span class="sxs-lookup"><span data-stu-id="6703f-179">This section describes how tooget started with partitioning your service.</span></span>

<span data-ttu-id="6703f-180">Service Fabric üç bölümleme şeması seçeneği sunar:</span><span class="sxs-lookup"><span data-stu-id="6703f-180">Service Fabric offers a choice of three partition schemes:</span></span>

* <span data-ttu-id="6703f-181">(Uniformınt64partition da bilinir) bölümleme aralıklı.</span><span class="sxs-lookup"><span data-stu-id="6703f-181">Ranged partitioning (otherwise known as UniformInt64Partition).</span></span>
* <span data-ttu-id="6703f-182">Bölümleme adı.</span><span class="sxs-lookup"><span data-stu-id="6703f-182">Named partitioning.</span></span> <span data-ttu-id="6703f-183">Bu model genelde kullanan uygulamalar, sınırlı kümesinde bucketed veri içeriyor.</span><span class="sxs-lookup"><span data-stu-id="6703f-183">Applications using this model usually have data that can be bucketed, within a bounded set.</span></span> <span data-ttu-id="6703f-184">Adlandırılmış bölüm anahtarları olarak kullanılan veri alanlarının sık karşılaşılan örnekleri, bölge, posta kodları, müşteri grupları veya diğer iş sınırları olacaktır.</span><span class="sxs-lookup"><span data-stu-id="6703f-184">Some common examples of data fields used as named partition keys would be regions, postal codes, customer groups, or other business boundaries.</span></span>
* <span data-ttu-id="6703f-185">Tek bölümleme.</span><span class="sxs-lookup"><span data-stu-id="6703f-185">Singleton partitioning.</span></span> <span data-ttu-id="6703f-186">Merhaba hizmeti herhangi bir ek yönlendirme gerekmediğinde singleton bölümler genellikle kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6703f-186">Singleton partitions are typically used when hello service does not require any additional routing.</span></span> <span data-ttu-id="6703f-187">Örneğin, durum bilgisi olmayan hizmetler varsayılan olarak bu bölümleme düzenini kullanın.</span><span class="sxs-lookup"><span data-stu-id="6703f-187">For example, stateless services use this partitioning scheme by default.</span></span>

<span data-ttu-id="6703f-188">Adlandırılmış ve özel formları aralıklı bölümlerinin tek bölümleme şemaları geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="6703f-188">Named and Singleton partitioning schemes are special forms of ranged partitions.</span></span> <span data-ttu-id="6703f-189">Merhaba olduğu gibi varsayılan olarak, Service Fabric kullanmak için Visual Studio şablonları hello bölümlendirme, en yaygın ve kullanışlı bir aralıklı.</span><span class="sxs-lookup"><span data-stu-id="6703f-189">By default, hello Visual Studio templates for Service Fabric use ranged partitioning, as it is hello most common and useful one.</span></span> <span data-ttu-id="6703f-190">Bu makalenin sonraki bölümlerinde Hello hello aralıklı bölümleme düzeni odaklanır.</span><span class="sxs-lookup"><span data-stu-id="6703f-190">hello remainder of this article focuses on hello ranged partitioning scheme.</span></span>

### <a name="ranged-partitioning-scheme"></a><span data-ttu-id="6703f-191">Bölümleme düzeni aralıklı</span><span class="sxs-lookup"><span data-stu-id="6703f-191">Ranged partitioning scheme</span></span>
<span data-ttu-id="6703f-192">Kullanılan toospecify tamsayı budur (düşük anahtarı ve yüksek anahtar tarafından tanımlanır) aralığı ve bölüm (n) sayısı.</span><span class="sxs-lookup"><span data-stu-id="6703f-192">This is used toospecify an integer range (identified by a low key and high key) and a number of partitions (n).</span></span> <span data-ttu-id="6703f-193">N bölümler, her bir çakışmayan alt aralığı hello biri için sorumlu oluşturur genel anahtar aralığı'nı bölüm.</span><span class="sxs-lookup"><span data-stu-id="6703f-193">It creates n partitions, each responsible for a non-overlapping subrange of hello overall partition key range.</span></span> <span data-ttu-id="6703f-194">Örneğin, ranged bölümleme düzeni düşük anahtar 0 ile 99 yüksek anahtarı ve 4 sayısını dört bölüm, aşağıda gösterildiği gibi oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="6703f-194">For example, a ranged partitioning scheme with a low key of 0, a high key of 99, and a count of 4 would create four partitions, as shown below.</span></span>

![Bölümleme aralığı](./media/service-fabric-concepts-partitioning/range-partitioning.png)

<span data-ttu-id="6703f-196">Bir ortak toocreate hello veri kümesi içinde benzersiz bir anahtar göre bir karma bir yaklaşımdır.</span><span class="sxs-lookup"><span data-stu-id="6703f-196">A common approach is toocreate a hash based on a unique key within hello data set.</span></span> <span data-ttu-id="6703f-197">Bazı ortak anahtarları örnekleri bir araç kimlik numarası (Toplamıdır), bir çalışan kimliği veya benzersiz bir dize olabilir.</span><span class="sxs-lookup"><span data-stu-id="6703f-197">Some common examples of keys would be a vehicle identification number (VIN), an employee ID, or a unique string.</span></span> <span data-ttu-id="6703f-198">Bu benzersiz anahtarı kullanarak, daha sonra bir karma kod, modül hello anahtar aralığı, toouse, anahtar olarak oluşturur.</span><span class="sxs-lookup"><span data-stu-id="6703f-198">By using this unique key, you would then generate a hash code, modulus hello key range, toouse as your key.</span></span> <span data-ttu-id="6703f-199">Merhaba üst ve alt sınır anahtar aralığı izin verilen hello belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6703f-199">You can specify hello upper and lower bounds of hello allowed key range.</span></span>

### <a name="select-a-hash-algorithm"></a><span data-ttu-id="6703f-200">Bir karma algoritması seçin</span><span class="sxs-lookup"><span data-stu-id="6703f-200">Select a hash algorithm</span></span>
<span data-ttu-id="6703f-201">Karma önemli bir bölümü, karma algoritma seçme.</span><span class="sxs-lookup"><span data-stu-id="6703f-201">An important part of hashing is selecting your hash algorithm.</span></span> <span data-ttu-id="6703f-202">Merhaba hedef toogroup benzer anahtarları birbirine yakın (yere göre hassas karma)--olup bir husustur veya etkinlik kapsamlı tüm bölümler (dağıtım karma) dağıtılması, daha yaygın olduğu.</span><span class="sxs-lookup"><span data-stu-id="6703f-202">A consideration is whether hello goal is toogroup similar keys near each other (locality sensitive hashing)--or if activity should be distributed broadly across all partitions (distribution hashing), which is more common.</span></span>

<span data-ttu-id="6703f-203">iyi dağıtım karma algoritması Hello özellikleri şunlardır: kolay toocompute olan, birkaç çakışmaları olan ve hello anahtarları eşit dağıtır.</span><span class="sxs-lookup"><span data-stu-id="6703f-203">hello characteristics of a good distribution hashing algorithm are that it is easy toocompute, it has few collisions, and it distributes hello keys evenly.</span></span> <span data-ttu-id="6703f-204">İyi bir verimli karma algoritması hello bir örnektir [FNV-1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) karma algoritması.</span><span class="sxs-lookup"><span data-stu-id="6703f-204">A good example of an efficient hash algorithm is hello [FNV-1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) hash algorithm.</span></span>

<span data-ttu-id="6703f-205">Bir iyi genel karma kodu algoritması seçimler hello kaynaktır [karma işlevlerini Wikipedia sayfasında](http://en.wikipedia.org/wiki/Hash_function).</span><span class="sxs-lookup"><span data-stu-id="6703f-205">A good resource for general hash code algorithm choices is hello [Wikipedia page on hash functions](http://en.wikipedia.org/wiki/Hash_function).</span></span>

## <a name="build-a-stateful-service-with-multiple-partitions"></a><span data-ttu-id="6703f-206">Durum bilgisi olan bir hizmet birden çok bölüm ile derleme</span><span class="sxs-lookup"><span data-stu-id="6703f-206">Build a stateful service with multiple partitions</span></span>
<span data-ttu-id="6703f-207">İlk güvenilir durum bilgisi olan hizmet birden çok bölüm oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="6703f-207">Let's create your first reliable stateful service with multiple partitions.</span></span> <span data-ttu-id="6703f-208">Bu örnekte, aynı harf hello hello ile başlayan tüm soyadlarını toostore istediğiniz çok basit bir uygulama oluşturacaksınız aynı bölüm.</span><span class="sxs-lookup"><span data-stu-id="6703f-208">In this example, you will build a very simple application where you want toostore all last names that start with hello same letter in hello same partition.</span></span>

<span data-ttu-id="6703f-209">Kod yazmadan önce hello bölümleri ve bölüm anahtarlarını ilgili toothink gerekir.</span><span class="sxs-lookup"><span data-stu-id="6703f-209">Before you write any code, you need toothink about hello partitions and partition keys.</span></span> <span data-ttu-id="6703f-210">26 bölümleri (bir hello alfabe her harfin), ilgili gerekenler düşük ve yüksek anahtarlar hello?</span><span class="sxs-lookup"><span data-stu-id="6703f-210">You need 26 partitions (one for each letter in hello alphabet), but what about hello low and high keys?</span></span>
<span data-ttu-id="6703f-211">Tam anlamıyla toohave bir bölüm harf başına istiyoruz gibi kendi anahtarını her harfi olduğu gibi biz 0 hello düşük anahtar ve 25 hello yüksek anahtar olarak kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6703f-211">As we literally want toohave one partition per letter, we can use 0 as hello low key and 25 as hello high key, as each letter is its own key.</span></span>

> [!NOTE]
> <span data-ttu-id="6703f-212">Gerçekte hello dağıtım eşit olacak şekilde basitleştirilmiş bir senaryo budur.</span><span class="sxs-lookup"><span data-stu-id="6703f-212">This is a simplified scenario, as in reality hello distribution would be uneven.</span></span> <span data-ttu-id="6703f-213">"S" veya "M" "X" Merhaba olanları başlangıç değerinden daha yaygın hello harflerle başlayan son adları veya "Y".</span><span class="sxs-lookup"><span data-stu-id="6703f-213">Last names starting with hello letters "S" or "M" are more common than hello ones starting with "X" or "Y".</span></span>
> 
> 

1. <span data-ttu-id="6703f-214">Açık **Visual Studio** > **dosya** > **yeni** > **proje**.</span><span class="sxs-lookup"><span data-stu-id="6703f-214">Open **Visual Studio** > **File** > **New** > **Project**.</span></span>
2. <span data-ttu-id="6703f-215">Merhaba, **yeni proje** iletişim kutusunda, Merhaba Service Fabric uygulaması seçin.</span><span class="sxs-lookup"><span data-stu-id="6703f-215">In hello **New Project** dialog box, choose hello Service Fabric application.</span></span>
3. <span data-ttu-id="6703f-216">Merhaba proje "AlphabetPartitions" çağırın.</span><span class="sxs-lookup"><span data-stu-id="6703f-216">Call hello project "AlphabetPartitions".</span></span>
4. <span data-ttu-id="6703f-217">Merhaba, **bir hizmet oluşturma** iletişim kutusunda, seçin **durum bilgisi olan** hizmet ve "Alphabet.Processing" Merhaba resimde gösterildiği gibi çağırın.</span><span class="sxs-lookup"><span data-stu-id="6703f-217">In hello **Create a Service** dialog box, choose **Stateful** service and call it "Alphabet.Processing" as shown in hello image below.</span></span>
       <span data-ttu-id="6703f-218">![Visual Studio'da yeni hizmet iletişim kutusu][1]</span><span class="sxs-lookup"><span data-stu-id="6703f-218">![New service dialog in Visual Studio][1]</span></span>

  <!--  ![Stateful service screenshot](./media/service-fabric-concepts-partitioning/createstateful.png)-->

5. <span data-ttu-id="6703f-219">Bölümler Hello sayısını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="6703f-219">Set hello number of partitions.</span></span> <span data-ttu-id="6703f-220">Açık hello Applicationmanifest.xml dosya hello hello AlphabetPartitions proje ve güncelleştirme hello parametre aşağıda gösterildiği gibi Processing_PartitionCount too26 ApplicationPackageRoot klasöründe bulunan.</span><span class="sxs-lookup"><span data-stu-id="6703f-220">Open hello Applicationmanifest.xml file located in hello ApplicationPackageRoot folder of hello AlphabetPartitions project and update hello parameter Processing_PartitionCount too26 as shown below.</span></span>
   
    ```xml
    <Parameter Name="Processing_PartitionCount" DefaultValue="26" />
    ```
   
    <span data-ttu-id="6703f-221">Tooupdate hello LowKey ve hello StatefulService hello aşağıda gösterildiği gibi ApplicationManifest.xml öğesinde HighKey özelliklerini de gerekir.</span><span class="sxs-lookup"><span data-stu-id="6703f-221">You also need tooupdate hello LowKey and HighKey properties of hello StatefulService element in hello ApplicationManifest.xml as shown below.</span></span>
   
    ```xml
    <Service Name="Processing">
      <StatefulService ServiceTypeName="ProcessingType" TargetReplicaSetSize="[Processing_TargetReplicaSetSize]" MinReplicaSetSize="[Processing_MinReplicaSetSize]">
        <UniformInt64Partition PartitionCount="[Processing_PartitionCount]" LowKey="0" HighKey="25" />
      </StatefulService>
    </Service>
    ```
6. <span data-ttu-id="6703f-222">Bir uç nokta bağlantı noktası hello aşağıda gösterildiği gibi Alphabet.Processing hizmeti için (Merhaba PackageRoot klasöründe bulunur) ServiceManifest.xml hello uç nokta öğesi ekleyerek Hello hizmet toobe için erişilebilir, açın:</span><span class="sxs-lookup"><span data-stu-id="6703f-222">For hello service toobe accessible, open up an endpoint on a port by adding hello endpoint element of ServiceManifest.xml (located in hello PackageRoot folder) for hello Alphabet.Processing service as shown below:</span></span>
   
    ```xml
    <Endpoint Name="ProcessingServiceEndpoint" Port="8089" Protocol="http" Type="Internal" />
    ```
   
    <span data-ttu-id="6703f-223">Artık yapılandırılmış toolisten tooan 26 bölümleri olan dahili uç noktayı hello hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="6703f-223">Now hello service is configured toolisten tooan internal endpoint with 26 partitions.</span></span>
7. <span data-ttu-id="6703f-224">Ardından toooverride hello gerekir `CreateServiceReplicaListeners()` hello işleme sınıfının yöntemi.</span><span class="sxs-lookup"><span data-stu-id="6703f-224">Next, you need toooverride hello `CreateServiceReplicaListeners()` method of hello Processing class.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6703f-225">Bu örnek için basit bir HttpCommunicationListener kullandığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="6703f-225">For this sample, we assume that you are using a simple HttpCommunicationListener.</span></span> <span data-ttu-id="6703f-226">Güvenilir hizmet iletişimi hakkında daha fazla bilgi için bkz: [hello güvenilir hizmet iletişim modelini](service-fabric-reliable-services-communication.md).</span><span class="sxs-lookup"><span data-stu-id="6703f-226">For more information on reliable service communication, see [hello Reliable Service communication model](service-fabric-reliable-services-communication.md).</span></span>
   > 
   > 
8. <span data-ttu-id="6703f-227">Bir çoğaltma dinlediği hello URL için önerilen bir deseni biçimini izleyen hello olduğu: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.</span><span class="sxs-lookup"><span data-stu-id="6703f-227">A recommended pattern for hello URL that a replica listens on is hello following format: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.</span></span>
    <span data-ttu-id="6703f-228">Bu nedenle hello doğru uç noktalarda ve bu deseni ile iletişimi dinleyici toolisten tooconfigure istiyor.</span><span class="sxs-lookup"><span data-stu-id="6703f-228">So you want tooconfigure your communication listener toolisten on hello correct endpoints and with this pattern.</span></span>
   
    <span data-ttu-id="6703f-229">Bu hizmetin birden fazla çoğaltma hello üzerinde barındırılabilir aynı bilgisayara nedenle toobe benzersiz toohello çoğaltma bu adresi gerekir.</span><span class="sxs-lookup"><span data-stu-id="6703f-229">Multiple replicas of this service may be hosted on hello same computer, so this address needs toobe unique toohello replica.</span></span> <span data-ttu-id="6703f-230">Bölüm kimliği + çoğaltma kimliği hello URL'de olan nedeni budur.</span><span class="sxs-lookup"><span data-stu-id="6703f-230">This is why   partition ID + replica ID are in hello URL.</span></span> <span data-ttu-id="6703f-231">HttpListener birden çok adresi hello hello URL öneki benzersiz olduğu sürece aynı bağlantı noktası üzerinde dinleme.</span><span class="sxs-lookup"><span data-stu-id="6703f-231">HttpListener can listen on multiple addresses on hello same port as long as hello URL prefix    is unique.</span></span>
   
    <span data-ttu-id="6703f-232">Merhaba fazladan GUID burada ikincil çoğaltmaların salt okunur istekleri için de dinlemek Gelişmiş bir olay yok.</span><span class="sxs-lookup"><span data-stu-id="6703f-232">hello extra GUID is there for an advanced case where secondary replicas also listen for read-only requests.</span></span> <span data-ttu-id="6703f-233">Hello durum böyle olduğunda, birincil toosecondary tooforce istemcileri toore Çöz hello adresinden geçiş zaman yeni bir benzersiz adresi kullanıldığından emin toomake istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="6703f-233">When that's hello case, you want toomake sure that a new unique address is used when transitioning from primary toosecondary tooforce clients toore-resolve hello address.</span></span> <span data-ttu-id="6703f-234">'+' hello çoğaltma dinler tüm kullanılabilir konakları (IP, FQDM, localhost, vb.) hello üzerinde aşağıdaki kodu böylece buraya hello adresi bir örnekte gösterildiği gibi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6703f-234">'+' is used as hello address here so that hello replica listens on all available hosts (IP, FQDM, localhost, etc.) hello code below shows an example.</span></span>
   
    ```CSharp
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
         return new[] { new ServiceReplicaListener(context => this.CreateInternalListener(context))};
    }
    private ICommunicationListener CreateInternalListener(ServiceContext context)
    {
   
         EndpointResourceDescription internalEndpoint = context.CodePackageActivationContext.GetEndpoint("ProcessingServiceEndpoint");
         string uriPrefix = String.Format(
                "{0}://+:{1}/{2}/{3}-{4}/",
                internalEndpoint.Protocol,
                internalEndpoint.Port,
                context.PartitionId,
                context.ReplicaOrInstanceId,
                Guid.NewGuid());
   
         string nodeIP = FabricRuntime.GetNodeContext().IPAddressOrFQDN;
   
         string uriPublished = uriPrefix.Replace("+", nodeIP);
         return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInternalRequest);
    }
    ```
   
    <span data-ttu-id="6703f-235">Bu değer olan bu hello yayımlanan URL belirterek hello dinleme URL önekten biraz farklı.</span><span class="sxs-lookup"><span data-stu-id="6703f-235">It's also worth noting that hello published URL is slightly different from hello listening URL prefix.</span></span>
    <span data-ttu-id="6703f-236">Merhaba dinleme URL tooHttpListener verilir.</span><span class="sxs-lookup"><span data-stu-id="6703f-236">hello listening URL is given tooHttpListener.</span></span> <span data-ttu-id="6703f-237">Merhaba yayımlanan yayımlanan toohello Service Fabric adlandırma hizmet bulma için kullanılan hizmeti, olan hello URL'dir.</span><span class="sxs-lookup"><span data-stu-id="6703f-237">hello published URL is hello URL that is published toohello Service Fabric Naming Service, which is used for service discovery.</span></span> <span data-ttu-id="6703f-238">İstemciler, bu bulma hizmeti aracılığıyla bu adres için sorar.</span><span class="sxs-lookup"><span data-stu-id="6703f-238">Clients will ask for this address through that discovery service.</span></span> <span data-ttu-id="6703f-239">Merhaba adresi istemcileri sipariş tooconnect gereksinimlerini toohave hello gerçek IP veya FQDN hello düğümünün alın.</span><span class="sxs-lookup"><span data-stu-id="6703f-239">hello address that clients get needs toohave hello actual IP or FQDN of hello node in order tooconnect.</span></span> <span data-ttu-id="6703f-240">Bu nedenle tooreplace gerekir '+' ile düğümün IP veya FQDN yukarıda gösterildiği gibi hello.</span><span class="sxs-lookup"><span data-stu-id="6703f-240">So you need tooreplace '+' with hello node's IP or FQDN as shown above.</span></span>
9. <span data-ttu-id="6703f-241">Merhaba son tooadd hello işleme mantığı toohello hizmeti aşağıda gösterildiği gibi bir adımdır.</span><span class="sxs-lookup"><span data-stu-id="6703f-241">hello last step is tooadd hello processing logic toohello service as shown below.</span></span>
   
    ```CSharp
    private async Task ProcessInternalRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        string output = null;
        string user = context.Request.QueryString["lastname"].ToString();
   
        try
        {
            output = await this.AddUserAsync(user);
        }
        catch (Exception ex)
        {
            output = ex.Message;
        }
   
        using (HttpListenerResponse response = context.Response)
        {
            if (output != null)
            {
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    private async Task<string> AddUserAsync(string user)
    {
        IReliableDictionary<String, String> dictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<String, String>>("dictionary");
   
        using (ITransaction tx = this.StateManager.CreateTransaction())
        {
            bool addResult = await dictionary.TryAddAsync(tx, user.ToUpperInvariant(), user);
   
            await tx.CommitAsync();
   
            return String.Format(
                "User {0} {1}",
                user,
                addResult ? "sucessfully added" : "already exists");
        }
    }
    ```
   
    <span data-ttu-id="6703f-242">`ProcessInternalRequest`Okuma hello hello sorgu dizesi parametresi kullanılan toocall hello bölümü ve çağrıları değerlerini `AddUserAsync` tooadd hello lastname toohello güvenilir sözlük `dictionary`.</span><span class="sxs-lookup"><span data-stu-id="6703f-242">`ProcessInternalRequest` reads hello values of hello query string parameter used toocall hello partition and calls `AddUserAsync` tooadd hello lastname toohello reliable dictionary `dictionary`.</span></span>
10. <span data-ttu-id="6703f-243">Durum bilgisiz hizmet toohello proje toosee ekleyelim belirli bir bölüm nasıl çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6703f-243">Let's add a stateless service toohello project toosee how you can call a particular partition.</span></span>
    
    <span data-ttu-id="6703f-244">Bu hizmet hello lastname bir sorgu dizesi parametresi olarak kabul eder, hello bölüm anahtarı belirler ve toohello Alphabet.Processing hizmetini işleme gönderen basit bir web arabirimi olarak görev yapar.</span><span class="sxs-lookup"><span data-stu-id="6703f-244">This service serves as a simple web interface that accepts hello lastname as a query string parameter, determines hello partition key, and sends it toohello Alphabet.Processing service for processing.</span></span>
11. <span data-ttu-id="6703f-245">Merhaba, **bir hizmet oluşturma** iletişim kutusunda, seçin **Stateless** hizmet ve aşağıda gösterildiği gibi "Alphabet.Web" çağırın.</span><span class="sxs-lookup"><span data-stu-id="6703f-245">In hello **Create a Service** dialog box, choose **Stateless** service and call it "Alphabet.Web" as shown below.</span></span>
    
    ![Durum bilgisiz hizmet ekran görüntüsü](./media/service-fabric-concepts-partitioning/createnewstateless.png)<span data-ttu-id="6703f-247">.</span><span class="sxs-lookup"><span data-stu-id="6703f-247">.</span></span>
12. <span data-ttu-id="6703f-248">Merhaba Alphabet.WebApi hizmet tooopen aşağıda gösterildiği gibi bir bağlantı kurmak, hello ServiceManifest.xml Hello uç nokta bilgileri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="6703f-248">Update hello endpoint information in hello ServiceManifest.xml of hello Alphabet.WebApi service tooopen up a port as shown below.</span></span>
    
    ```xml
    <Endpoint Name="WebApiServiceEndpoint" Protocol="http" Port="8081"/>
    ```
13. <span data-ttu-id="6703f-249">Tooreturn koleksiyonunda hello sınıfı Web ServiceInstanceListeners gerekir.</span><span class="sxs-lookup"><span data-stu-id="6703f-249">You need tooreturn a collection of ServiceInstanceListeners in hello class Web.</span></span> <span data-ttu-id="6703f-250">Yeniden basit HttpCommunicationListener tooimplement seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6703f-250">Again, you can choose tooimplement a simple HttpCommunicationListener.</span></span>
    
    ```CSharp
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] {new ServiceInstanceListener(context => this.CreateInputListener(context))};
    }
    private ICommunicationListener CreateInputListener(ServiceContext context)
    {
        // Service instance's URL is hello node's IP & desired port
        EndpointResourceDescription inputEndpoint = context.CodePackageActivationContext.GetEndpoint("WebApiServiceEndpoint")
        string uriPrefix = String.Format("{0}://+:{1}/alphabetpartitions/", inputEndpoint.Protocol, inputEndpoint.Port);
        var uriPublished = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
        return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInputRequest);
    }
    ```
14. <span data-ttu-id="6703f-251">Şimdi tooimplement hello işleme mantığı gerekir.</span><span class="sxs-lookup"><span data-stu-id="6703f-251">Now you need tooimplement hello processing logic.</span></span> <span data-ttu-id="6703f-252">HttpCommunicationListener çağrıları hello `ProcessInputRequest` bir isteği ne zaman devreye girer.</span><span class="sxs-lookup"><span data-stu-id="6703f-252">hello HttpCommunicationListener calls `ProcessInputRequest` when a request comes in.</span></span> <span data-ttu-id="6703f-253">Bu nedenle devam edelim ve hello aşağıdaki kodu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6703f-253">So let's go ahead and add hello code below.</span></span>
    
    ```CSharp
    private async Task ProcessInputRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        String output = null;
        try
        {
            string lastname = context.Request.QueryString["lastname"];
            char firstLetterOfLastName = lastname.First();
            ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    
            ResolvedServicePartition partition = await this.servicePartitionResolver.ResolveAsync(alphabetServiceUri, partitionKey, cancelRequest);
            ResolvedServiceEndpoint ep = partition.GetEndpoint();
    
            JObject addresses = JObject.Parse(ep.Address);
            string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
            UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
            primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
            string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    
            output = String.Format(
                    "Result: {0}. <p>Partition key: '{1}' generated from hello first letter '{2}' of input value '{3}'. <br>Processing service partition ID: {4}. <br>Processing service replica address: {5}",
                    result,
                    partitionKey,
                    firstLetterOfLastName,
                    lastname,
                    partition.Info.Id,
                    primaryReplicaAddress);
        }
        catch (Exception ex) { output = ex.Message; }
    
        using (var response = context.Response)
        {
            if (output != null)
            {
                output = output + "added tooPartition: " + primaryReplicaAddress;
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    ```
    
    <span data-ttu-id="6703f-254">Şimdi arkasını adım adım yol gösterir.</span><span class="sxs-lookup"><span data-stu-id="6703f-254">Let's walk through it step by step.</span></span> <span data-ttu-id="6703f-255">Merhaba kod okur hello ilk harfi hello sorgu dizesi parametresinin `lastname` bir char içine.</span><span class="sxs-lookup"><span data-stu-id="6703f-255">hello code reads hello first letter of hello query string parameter `lastname` into a char.</span></span> <span data-ttu-id="6703f-256">Ardından, hello on altılık değeri çıkararak bu harfi için hello bölüm anahtarı belirler `A` hello son adları ilk harfi hello onaltılık değerinden.</span><span class="sxs-lookup"><span data-stu-id="6703f-256">Then, it determines hello partition key for this letter by subtracting hello hexadecimal value of `A` from hello hexadecimal value of hello last names' first letter.</span></span>
    
    ```CSharp
    string lastname = context.Request.QueryString["lastname"];
    char firstLetterOfLastName = lastname.First();
    ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    ```
    
    <span data-ttu-id="6703f-257">Bu örnekte, 26 bölümler bölüm başına tek bölüm anahtarına sahip kullanıyoruz unutmayın.</span><span class="sxs-lookup"><span data-stu-id="6703f-257">Remember, for this example, we are using 26 partitions with one partition key per partition.</span></span>
    <span data-ttu-id="6703f-258">Ardından, biz hello hizmet bölüm elde `partition` hello kullanarak bu anahtar için `ResolveAsync` hello yöntemi `servicePartitionResolver` nesnesi.</span><span class="sxs-lookup"><span data-stu-id="6703f-258">Next, we obtain hello service partition `partition` for this key by using hello `ResolveAsync` method on hello `servicePartitionResolver` object.</span></span> <span data-ttu-id="6703f-259">`servicePartitionResolver`olarak tanımlanır</span><span class="sxs-lookup"><span data-stu-id="6703f-259">`servicePartitionResolver` is defined as</span></span>
    
    ```CSharp
    private readonly ServicePartitionResolver servicePartitionResolver = ServicePartitionResolver.GetDefault();
    ```
    
    <span data-ttu-id="6703f-260">Merhaba `ResolveAsync` yöntemi alır hello hizmet URI'si, hello bölüm anahtarı ve parametre olarak bir iptal belirteci.</span><span class="sxs-lookup"><span data-stu-id="6703f-260">hello `ResolveAsync` method takes hello service URI, hello partition key, and a cancellation token as parameters.</span></span> <span data-ttu-id="6703f-261">Merhaba işleme hizmeti için hizmet URI'si hello `fabric:/AlphabetPartitions/Processing`.</span><span class="sxs-lookup"><span data-stu-id="6703f-261">hello service URI for hello processing service is `fabric:/AlphabetPartitions/Processing`.</span></span> <span data-ttu-id="6703f-262">Ardından, hello bölüm hello uç noktasını alın.</span><span class="sxs-lookup"><span data-stu-id="6703f-262">Next, we get hello endpoint of hello partition.</span></span>
    
    ```CSharp
    ResolvedServiceEndpoint ep = partition.GetEndpoint()
    ```
    
    <span data-ttu-id="6703f-263">Son olarak, biz hello uç nokta URL'si artı hello querystring yapı ve işleme hizmeti hello çağırın.</span><span class="sxs-lookup"><span data-stu-id="6703f-263">Finally, we build hello endpoint URL plus hello querystring and call hello processing service.</span></span>
    
    ```CSharp
    JObject addresses = JObject.Parse(ep.Address);
    string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
    UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
    primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
    string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    ```
    
    <span data-ttu-id="6703f-264">Merhaba işleme yaptıktan sonra biz hello çıkış geri yazma.</span><span class="sxs-lookup"><span data-stu-id="6703f-264">Once hello processing is done, we write hello output back.</span></span>
15. <span data-ttu-id="6703f-265">Merhaba son adımı tootest hello hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="6703f-265">hello last step is tootest hello service.</span></span> <span data-ttu-id="6703f-266">Visual Studio kullanan uygulama parametreleri, yerel ve bulut dağıtımı.</span><span class="sxs-lookup"><span data-stu-id="6703f-266">Visual Studio uses application parameters for local and cloud deployment.</span></span> <span data-ttu-id="6703f-267">tootest hello hizmeti yerel olarak 26 bölümlerle tooupdate hello ihtiyacınız `Local.xml` aşağıda gösterildiği gibi hello ApplicationParameters klasöründe hello AlphabetPartitions proje dosyası:</span><span class="sxs-lookup"><span data-stu-id="6703f-267">tootest hello service with 26 partitions locally, you need tooupdate hello `Local.xml` file in hello ApplicationParameters folder of hello AlphabetPartitions project as shown below:</span></span>
    
    ```xml
    <Parameters>
      <Parameter Name="Processing_PartitionCount" Value="26" />
      <Parameter Name="WebApi_InstanceCount" Value="1" />
    </Parameters>
    ```
16. <span data-ttu-id="6703f-268">Dağıtımını tamamladıktan sonra hello hizmeti ve tüm bölümleri hello Service Fabric Explorer'ın kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6703f-268">Once you finish deployment, you can check hello service and all of its partitions in hello Service Fabric Explorer.</span></span>
    
    ![Service Fabric Explorer ekran görüntüsü](./media/service-fabric-concepts-partitioning/sfxpartitions.png)
17. <span data-ttu-id="6703f-270">Bir tarayıcıda girerek mantığı bölümleme hello sınayabilirsiniz `http://localhost:8081/?lastname=somename`.</span><span class="sxs-lookup"><span data-stu-id="6703f-270">In a browser, you can test hello partitioning logic by entering `http://localhost:8081/?lastname=somename`.</span></span> <span data-ttu-id="6703f-271">Her son adı ile aynı harf hello depolanıyor hello başlayan olduğunu görürsünüz aynı bölüm.</span><span class="sxs-lookup"><span data-stu-id="6703f-271">You will see that each last name that starts with hello same letter is being stored in hello same partition.</span></span>
    
    ![Tarayıcı ekran görüntüsü](./media/service-fabric-concepts-partitioning/samplerunning.png)

<span data-ttu-id="6703f-273">Merhaba örnek Hello tüm kaynak kodunun edinilebilir [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span><span class="sxs-lookup"><span data-stu-id="6703f-273">hello entire source code of hello sample is available on [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6703f-274">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6703f-274">Next steps</span></span>
<span data-ttu-id="6703f-275">Service Fabric kavramları hakkında daha fazla bilgi için hello aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="6703f-275">For information on Service Fabric concepts, see hello following:</span></span>

* [<span data-ttu-id="6703f-276">Service Fabric hizmetlerin kullanılabilirliğini</span><span class="sxs-lookup"><span data-stu-id="6703f-276">Availability of Service Fabric services</span></span>](service-fabric-availability-services.md)
* [<span data-ttu-id="6703f-277">Service Fabric Hizmetleri ölçeklenebilirliği</span><span class="sxs-lookup"><span data-stu-id="6703f-277">Scalability of Service Fabric services</span></span>](service-fabric-concepts-scalability.md)
* [<span data-ttu-id="6703f-278">Kapasite planlama için Service Fabric uygulamaları</span><span class="sxs-lookup"><span data-stu-id="6703f-278">Capacity planning for Service Fabric applications</span></span>](service-fabric-capacity-planning.md)

[wikipartition]: https://en.wikipedia.org/wiki/Partition_(database)

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png