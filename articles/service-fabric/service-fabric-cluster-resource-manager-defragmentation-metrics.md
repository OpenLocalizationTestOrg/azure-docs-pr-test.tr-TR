---
title: "Azure Service Fabric ölçümlerini aaaDefragmentation | Microsoft Docs"
description: "Birleştirme kullanarak veya Service Fabric ölçümlerini için bir strateji olarak sevk bir genel bakış"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: e5ebfae5-c8f7-4d6c-9173-3e22a9730552
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: d09045a6cf196d2771f1a0794637f4579d3eb96b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="defragmentation-of-metrics-and-load-in-service-fabric"></a><span data-ttu-id="5a4da-103">Ölçümleri ve Service Fabric yük birleştirme</span><span class="sxs-lookup"><span data-stu-id="5a4da-103">Defragmentation of metrics and load in Service Fabric</span></span>
<span data-ttu-id="5a4da-104">Yük ölçüm hello kümedeki yönetmek için hello Service Fabric kümesi kaynak yöneticisinin varsayılan toodistribute hello yük stratejidir.</span><span class="sxs-lookup"><span data-stu-id="5a4da-104">hello Service Fabric Cluster Resource Manager's default strategy for managing load metrics in hello cluster is toodistribute hello load.</span></span> <span data-ttu-id="5a4da-105">Düğümleri eşit olarak kullanıldığını sağlama tooboth Çekişme ve harcanan kaynakları sağlama sıcak ve soğuk noktalar önler.</span><span class="sxs-lookup"><span data-stu-id="5a4da-105">Ensuring that nodes are evenly utilized avoids hot and cold spots that lead tooboth contention and wasted resources.</span></span> <span data-ttu-id="5a4da-106">Merhaba küme iş yüklerini dağıtma hello hata belirli bir iş yükü büyük bir yüzdesini almaz sağlar beri hataları sürdüren açısından güvenli olur.</span><span class="sxs-lookup"><span data-stu-id="5a4da-106">Distributing workloads in hello cluster is also hello safest in terms of surviving failures since it ensures that a failure doesn’t take out a large percentage of a given workload.</span></span> 

<span data-ttu-id="5a4da-107">Merhaba Service Fabric kümesi Kaynak Yöneticisi, birleştirme olan yük yönetmek için farklı bir strateji desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="5a4da-107">hello Service Fabric Cluster Resource Manager does support a different strategy for managing load, which is defragmentation.</span></span> <span data-ttu-id="5a4da-108">Birleştirme toodistribute hello kullanım ölçüm Merhaba kümede çalışırken yerine onu birleştirilir olduğunu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="5a4da-108">Defragmentation means that instead of trying toodistribute hello utilization of a metric across hello cluster, it is consolidated.</span></span> <span data-ttu-id="5a4da-109">Birleştirme yalnızca bir ters çevirmeyi hello ortalama standart sapmasını ölçüm yükü en aza yerine stratejisi – Dengeleme hello varsayılan, hello Küme Kaynak Yöneticisi'ni çalışır tooincrease onu.</span><span class="sxs-lookup"><span data-stu-id="5a4da-109">Consolidation is just an inversion of hello default balancing strategy – instead of minimizing hello average standard deviation of metric load, hello Cluster Resource Manager tries tooincrease it.</span></span>

## <a name="when-toouse-defragmentation"></a><span data-ttu-id="5a4da-110">Zaman toouse birleştirme</span><span class="sxs-lookup"><span data-stu-id="5a4da-110">When toouse defragmentation</span></span>
<span data-ttu-id="5a4da-111">Merhaba kümedeki yük dağıtma, bazı hello kaynaklara her düğümde tüketir.</span><span class="sxs-lookup"><span data-stu-id="5a4da-111">Distributing load in hello cluster consumes some of hello resources on each node.</span></span> <span data-ttu-id="5a4da-112">Bazı iş yükleri olağanüstü büyük ve çoğu veya hepsi bir düğümün tüketen Hizmetleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5a4da-112">Some workloads create services that are exceptionally large and consume most or all of a node.</span></span> <span data-ttu-id="5a4da-113">Bu durumda olduğunda büyük yeterli hiç oluşturulan iş yükleri bunları herhangi düğümü toorun boşluk mümkündür.</span><span class="sxs-lookup"><span data-stu-id="5a4da-113">In these cases, it's possible that when there are large workloads getting created that there isn't enough space on any node toorun them.</span></span> <span data-ttu-id="5a4da-114">Büyük iş yüklerini Service Fabric bir sorun değildir; Bu durumlarda hello tooreorganize hello küme toomake yer büyük bu iş yükü için ihtiyaç duyduğu Küme Kaynak Yöneticisi'ni belirler.</span><span class="sxs-lookup"><span data-stu-id="5a4da-114">Large workloads aren't a problem in Service Fabric; in these cases hello Cluster Resource Manager determines that it needs tooreorganize hello cluster toomake room for this large workload.</span></span> <span data-ttu-id="5a4da-115">Ancak, hello hello kümede zamanlanmış toowait toobe sırada iş yükü vardır.</span><span class="sxs-lookup"><span data-stu-id="5a4da-115">However, in hello meantime that workload has toowait toobe scheduled in hello cluster.</span></span>

<span data-ttu-id="5a4da-116">Daha sonra birçok Hizmetleri ve geçici bir çözüm durumu toomove varsa hello kümede yerleştirilen hello büyük iş yükü toobe uzun bir süredir ele geçirebilir.</span><span class="sxs-lookup"><span data-stu-id="5a4da-116">If there are many services and state toomove around, then it could take a long time for hello large workload toobe placed in hello cluster.</span></span> <span data-ttu-id="5a4da-117">Merhaba kümedeki diğer iş yükleri de büyük varsa ve bu nedenle uzun tooreorganize ele daha yüksektir.</span><span class="sxs-lookup"><span data-stu-id="5a4da-117">This is more likely if other workloads in hello cluster are also large and so take longer tooreorganize.</span></span> <span data-ttu-id="5a4da-118">Merhaba Service Fabric ekip oluşturma zamanları ile bu senaryonun benzetimleri ölçülür.</span><span class="sxs-lookup"><span data-stu-id="5a4da-118">hello Service Fabric team measured creation times in simulations of this scenario.</span></span> <span data-ttu-id="5a4da-119">%30 ve % 50 arasında yukarıdaki Küme kullanımı var hemen büyük hizmetleri oluşturma çok uzun sürdüğü bulduk.</span><span class="sxs-lookup"><span data-stu-id="5a4da-119">We found that creating large services took much longer as soon as cluster utilization got above between 30% and 50%.</span></span> <span data-ttu-id="5a4da-120">toohandle bu senaryo, biz birleştirme karşı bir strateji olarak sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="5a4da-120">toohandle this scenario, we introduced defragmentation as a balancing strategy.</span></span> <span data-ttu-id="5a4da-121">Büyük iş yükleri için özellikle olanları oluşturulma zamanı birleştirme gerçekten bu yeni iş yüklerine Yardım önemli olduğu hello kümede zamanlanmış bulduk.</span><span class="sxs-lookup"><span data-stu-id="5a4da-121">We found that for large workloads, especially ones where creation time was important, defragmentation really helped those new workloads get scheduled in hello cluster.</span></span>

<span data-ttu-id="5a4da-122">Daha az düğümlerin içine birleştirme ölçümleri toohave hello küme Resource Manager tooproactively try toocondense hello yük hello Hizmetleri yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a4da-122">You can configure defragmentation metrics toohave hello Cluster Resource Manager tooproactively try toocondense hello load of hello services into fewer nodes.</span></span> <span data-ttu-id="5a4da-123">Bu, olduğunu neredeyse her zaman hello küme yeniden düzenleme olmadan büyük Hizmetleri için yeriniz sağlamaya yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="5a4da-123">This helps ensure that there is almost always room for large services without reorganizing hello cluster.</span></span> <span data-ttu-id="5a4da-124">Tooreorganize hello küme olmamasından büyük iş yüklerini hızlı oluşturma sağlar.</span><span class="sxs-lookup"><span data-stu-id="5a4da-124">Not having tooreorganize hello cluster allows creating large workloads quickly.</span></span>

<span data-ttu-id="5a4da-125">Çoğu kişi birleştirme gerek yoktur.</span><span class="sxs-lookup"><span data-stu-id="5a4da-125">Most people don’t need defragmentation.</span></span> <span data-ttu-id="5a4da-126">Hizmetleri olan genellikle küçük, sabit toofind odada onlar için hello küme olmadığı için.</span><span class="sxs-lookup"><span data-stu-id="5a4da-126">Services are usually be small, so it’s not hard toofind room for them in hello cluster.</span></span> <span data-ttu-id="5a4da-127">Düzenlenmesi mümkün olduğunda, çünkü çoğu Hizmetleri küçük ve hızlı bir şekilde ve paralel taşınabilir öğeyi hızlı bir şekilde, yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="5a4da-127">When reorganization is possible, it goes quickly, again because most services are small and can be moved quickly and in parallel.</span></span> <span data-ttu-id="5a4da-128">Hizmetleri, büyük ve bunları hızlı bir şekilde oluşturulan gereksinim ardından hello ancak birleştirme stratejisi sizin için olur.</span><span class="sxs-lookup"><span data-stu-id="5a4da-128">However, if you have large services and need them created quickly then hello defragmentation strategy is for you.</span></span> <span data-ttu-id="5a4da-129">Biz birleştirme sonraki kullanmanın hello bileşim ele alacağız.</span><span class="sxs-lookup"><span data-stu-id="5a4da-129">We'll discuss hello tradeoffs of using defragmentation next.</span></span> 

## <a name="defragmentation-tradeoffs"></a><span data-ttu-id="5a4da-130">Birleştirme bileşim</span><span class="sxs-lookup"><span data-stu-id="5a4da-130">Defragmentation tradeoffs</span></span>
<span data-ttu-id="5a4da-131">Daha fazla hizmet başarısız düğümleri üzerinde çalışan bu yana birleştirme hataları, impactfulness artırabilir.</span><span class="sxs-lookup"><span data-stu-id="5a4da-131">Defragmentation can increase impactfulness of failures, since more services are running on nodes that fail.</span></span> <span data-ttu-id="5a4da-132">Merhaba küme kaynaklarında büyük iş yüklerini hello oluşturulması için bekleyen ayırma tutulması gereken beri birleştirme maliyetleri de artırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5a4da-132">Defragmentation can also increase costs, since resources in hello cluster must be held in reserve, waiting for hello creation of large workloads.</span></span>

<span data-ttu-id="5a4da-133">Hello Aşağıdaki diyagramda iki küme görsel gösterimi, birleştirilmiş diğeri olmayan sağlar.</span><span class="sxs-lookup"><span data-stu-id="5a4da-133">hello following diagram gives a visual representation of two clusters, one that is defragmented and one that is not.</span></span> 

<span data-ttu-id="5a4da-134"><center>
![Karşılaştırma ve dengeli kümeleri birleştirilmiş][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="5a4da-134"><center>
![Comparing Balanced and Defragmented Clusters][Image1]
</center></span></span>

<span data-ttu-id="5a4da-135">Dengeli hello durumda gerekli tooplace hello en büyük hizmet nesnelerden biri olacak hareketleri hello sayısını göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="5a4da-135">In hello balanced case, consider hello number of movements that would be necessary tooplace one of hello largest service objects.</span></span> <span data-ttu-id="5a4da-136">Merhaba birleştirilmiş kümede hello büyük iş yükü diğer hizmetler toomove toowait gerek kalmadan dört veya beş düğümlerinde yerleştirilemedi.</span><span class="sxs-lookup"><span data-stu-id="5a4da-136">In hello defragmented cluster, hello large workload could be placed on nodes four or five without having toowait for any other services toomove.</span></span>

## <a name="defragmentation-pros-and-cons"></a><span data-ttu-id="5a4da-137">Birleştirme Artıları ve eksileri</span><span class="sxs-lookup"><span data-stu-id="5a4da-137">Defragmentation pros and cons</span></span>
<span data-ttu-id="5a4da-138">Bu nedenle bu diğer kavramsal bileşim nelerdir?</span><span class="sxs-lookup"><span data-stu-id="5a4da-138">So what are those other conceptual tradeoffs?</span></span> <span data-ttu-id="5a4da-139">Hakkında hızlı bir şeyler toothink tablosu aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="5a4da-139">Here’s a quick table of things toothink about:</span></span>

| <span data-ttu-id="5a4da-140">Birleştirme uzmanları</span><span class="sxs-lookup"><span data-stu-id="5a4da-140">Defragmentation Pros</span></span> | <span data-ttu-id="5a4da-141">Birleştirme simgeler</span><span class="sxs-lookup"><span data-stu-id="5a4da-141">Defragmentation Cons</span></span> |
| --- | --- |
| <span data-ttu-id="5a4da-142">Büyük Hizmetleri daha hızlı oluşturulmasını sağlar</span><span class="sxs-lookup"><span data-stu-id="5a4da-142">Allows faster creation of large services</span></span> |<span data-ttu-id="5a4da-143">Concentrates Çekişme artırma daha az düğümü yükleme</span><span class="sxs-lookup"><span data-stu-id="5a4da-143">Concentrates load onto fewer nodes, increasing contention</span></span> |
| <span data-ttu-id="5a4da-144">Etkinleştirir veri taşıma oluşturma sırasında düşürün.</span><span class="sxs-lookup"><span data-stu-id="5a4da-144">Enables lower data movement during creation</span></span> |<span data-ttu-id="5a4da-145">Hataları daha fazla hizmet etkileyebilir ve daha fazla karmaşası neden</span><span class="sxs-lookup"><span data-stu-id="5a4da-145">Failures can impact more services and cause more churn</span></span> |
| <span data-ttu-id="5a4da-146">Alan geri kazanma ve gereksinimleri zengin açıklaması sağlar</span><span class="sxs-lookup"><span data-stu-id="5a4da-146">Allows rich description of requirements and reclamation of space</span></span> |<span data-ttu-id="5a4da-147">Daha karmaşık genel kaynak yönetimi yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5a4da-147">More complex overall Resource Management configuration</span></span> |

<span data-ttu-id="5a4da-148">Birleştirilmiş karıştırabilirsiniz ve aynı küme normal ölçümlerini hello.</span><span class="sxs-lookup"><span data-stu-id="5a4da-148">You can mix defragmented and normal metrics in hello same cluster.</span></span> <span data-ttu-id="5a4da-149">Merhaba Küme Kaynak Yöneticisi'ni çalışır tooconsolidate hello birleştirme ölçümleri yaymak sırasında mümkün olduğunca başkalarının hello.</span><span class="sxs-lookup"><span data-stu-id="5a4da-149">hello Cluster Resource Manager tries tooconsolidate hello defragmentation metrics as much as possible while spreading out hello others.</span></span> <span data-ttu-id="5a4da-150">Birleştirme karıştırma ve stratejileri Dengeleme hello sonuçları dahil olmak üzere çeşitli etkenlere bağlıdır:</span><span class="sxs-lookup"><span data-stu-id="5a4da-150">hello results of mixing defragmentation and balancing strategies depends on several factors, including:</span></span>
  - <span data-ttu-id="5a4da-151">Birleştirme ölçümleri hello sayısı ve ölçümleri Dengeleme hello sayısı</span><span class="sxs-lookup"><span data-stu-id="5a4da-151">hello number of balancing metrics vs. hello number of defragmentation metrics</span></span>
  - <span data-ttu-id="5a4da-152">Herhangi bir hizmet ölçümleri her iki tür kullanıp kullanmadığını</span><span class="sxs-lookup"><span data-stu-id="5a4da-152">Whether any service uses both types of metrics</span></span> 
  - <span data-ttu-id="5a4da-153">Merhaba ölçüm ağırlığı</span><span class="sxs-lookup"><span data-stu-id="5a4da-153">hello metric weights</span></span>
  - <span data-ttu-id="5a4da-154">Geçerli ölçüm yükler</span><span class="sxs-lookup"><span data-stu-id="5a4da-154">current metric loads</span></span>
  
<span data-ttu-id="5a4da-155">Deneme gerekli toodetermine hello tam gerekli yapılandırmadır.</span><span class="sxs-lookup"><span data-stu-id="5a4da-155">Experimentation is required toodetermine hello exact configuration necessary.</span></span> <span data-ttu-id="5a4da-156">Birleştirme ölçümleri üretimde etkinleştirmeden önce iş yüklerinin kapsamlı ölçüm öneririz.</span><span class="sxs-lookup"><span data-stu-id="5a4da-156">We recommend thorough measurement of your workloads before you enable defragmentation metrics in production.</span></span> <span data-ttu-id="5a4da-157">Bu birleştirme ve dengeli ölçümleri hello içinde karıştırılması durumlarda özellikle geçerlidir aynı hizmet.</span><span class="sxs-lookup"><span data-stu-id="5a4da-157">This is especially true when mixing defragmentation and balanced metrics within hello same service.</span></span> 

## <a name="configuring-defragmentation-metrics"></a><span data-ttu-id="5a4da-158">Birleştirme ölçümleri yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5a4da-158">Configuring defragmentation metrics</span></span>
<span data-ttu-id="5a4da-159">Birleştirme ölçümleri yapılandırma bir genel hello kümedeki bir karardır ve tek tek ölçümleri birleştirme için seçilebilir.</span><span class="sxs-lookup"><span data-stu-id="5a4da-159">Configuring defragmentation metrics is a global decision in hello cluster, and individual metrics can be selected for defragmentation.</span></span> <span data-ttu-id="5a4da-160">config parçacıkları aşağıdaki hello nasıl tooconfigure ölçümlerini birleştirme gösterir.</span><span class="sxs-lookup"><span data-stu-id="5a4da-160">hello following config snippets show how tooconfigure metrics for defragmentation.</span></span> <span data-ttu-id="5a4da-161">Bu durumda, "Metric2" normalde dengeli toobe devam ederken "Metric1" bir birleştirme ölçü olarak yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="5a4da-161">In this case, "Metric1" is configured as a defragmentation metric, while "Metric2" will continue toobe balanced normally.</span></span> 

<span data-ttu-id="5a4da-162">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="5a4da-162">ClusterManifest.xml:</span></span>

```xml
<Section Name="DefragmentationMetrics">
    <Parameter Name="Metric1" Value="true" />
    <Parameter Name="Metric2" Value="false" />
</Section>
```

<span data-ttu-id="5a4da-163">tek başına dağıtımlarında ClusterConfig.json ya da Azure için Template.json aracılığıyla kümeleri barındırılan:</span><span class="sxs-lookup"><span data-stu-id="5a4da-163">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "DefragmentationMetrics",
    "parameters": [
      {
          "name": "Metric1",
          "value": "true"
      },
      {
          "name": "Metric2",
          "value": "false"
      }
    ]
  }
]
```


## <a name="next-steps"></a><span data-ttu-id="5a4da-164">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5a4da-164">Next steps</span></span>
- <span data-ttu-id="5a4da-165">Merhaba küme Resource Manager hello küme açıklamak için adam seçenekleri vardır.</span><span class="sxs-lookup"><span data-stu-id="5a4da-165">hello Cluster Resource Manager has man options for describing hello cluster.</span></span> <span data-ttu-id="5a4da-166">toofind bunlarla ilgili daha fazla bilgi, bu makalede denetleyin [açıklayan bir Service Fabric kümesi](service-fabric-cluster-resource-manager-cluster-description.md)</span><span class="sxs-lookup"><span data-stu-id="5a4da-166">toofind out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>
- <span data-ttu-id="5a4da-167">Kullanım ve kapasite hello kümedeki hello Service Fabric kümesi kaynak yöneticisi nasıl yönettiğini ölçümleridir.</span><span class="sxs-lookup"><span data-stu-id="5a4da-167">Metrics are how hello Service Fabric Cluster Resource Manger manages consumption and capacity in hello cluster.</span></span> <span data-ttu-id="5a4da-168">Ölçümler hakkında daha fazla toolearn ve nasıl tooconfigure bunları kullanıma [bu makalede](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="5a4da-168">toolearn more about metrics and how tooconfigure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-defragmentation-metrics/balancing-defrag-compared.png
