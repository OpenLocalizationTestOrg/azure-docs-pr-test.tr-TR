---
title: "Service Fabric kümesi Kaynak Yöneticisi: taşıma maliyeti | Microsoft Docs"
description: "Taşıma maliyeti Service Fabric Hizmetleri için genel bakış"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: f022f258-7bc0-4db4-aa85-8c6c8344da32
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 65d4ac73efffcf7b25b1e95da6f9012a9238cb75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="service-movement-cost"></a><span data-ttu-id="c532d-103">Hizmet taşıma maliyeti</span><span class="sxs-lookup"><span data-stu-id="c532d-103">Service movement cost</span></span>
<span data-ttu-id="c532d-104">Service Fabric kümesi Kaynak Yöneticisi hello bir faktör toodetermine hangi değişiklikleri toomake tooa küme hello bu değişiklikleri maliyetidir çalışırken göz önünde bulundurur.</span><span class="sxs-lookup"><span data-stu-id="c532d-104">A factor that hello Service Fabric Cluster Resource Manager considers when trying toodetermine what changes toomake tooa cluster is hello cost of those changes.</span></span> <span data-ttu-id="c532d-105">"Maliyet" Merhaba kavramı kapalı ne kadar hello küme karşı geliştirilebilir ticareti.</span><span class="sxs-lookup"><span data-stu-id="c532d-105">hello notion of "cost" is traded off against how much hello cluster can be improved.</span></span> <span data-ttu-id="c532d-106">Maliyet Dengeleme, birleştirme ve diğer gereksinimler için hizmetler taşırken hesaba katıldığında.</span><span class="sxs-lookup"><span data-stu-id="c532d-106">Cost is factored in when moving services for balancing, defragmentation, and other requirements.</span></span> <span data-ttu-id="c532d-107">Merhaba hedeftir hello toomeet hello gereksinimleri en az kesintiye uğratan veya pahalı yolu.</span><span class="sxs-lookup"><span data-stu-id="c532d-107">hello goal is toomeet hello requirements in hello least disruptive or expensive way.</span></span> 

<span data-ttu-id="c532d-108">Hizmetleri maliyetleri CPU süresi taşıma ve ağ bant genişliği en az.</span><span class="sxs-lookup"><span data-stu-id="c532d-108">Moving services costs CPU time and network bandwidth at a minimum.</span></span> <span data-ttu-id="c532d-109">Durum bilgisi olan hizmetler için ek bellek ve disk tüketen hizmetlerin hello durumunu kopyalama gerektiriyor.</span><span class="sxs-lookup"><span data-stu-id="c532d-109">For stateful services, it requires copying hello state of those services, consuming additional memory and disk.</span></span> <span data-ttu-id="c532d-110">Azure Service Fabric kümesi Resource Manager ile gelir bu hello çözümleri Hello maliyetini en aza indirme hello kümenin kaynakları gereksiz yere harcanan olmayan sağlamaya yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="c532d-110">Minimizing hello cost of solutions that hello Azure Service Fabric Cluster Resource Manager comes up with helps ensure that hello cluster's resources aren't spent unnecessarily.</span></span> <span data-ttu-id="c532d-111">Ancak, hello küme kaynaklarında hello ayrılması önemli ölçüde artırmak tooignore çözümleri istemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="c532d-111">However, you also don’t want tooignore solutions that would significantly improve hello allocation of resources in hello cluster.</span></span>

<span data-ttu-id="c532d-112">Merhaba küme Resource Manager maliyetleri bilgi işlem ve toomanage hello küme denediğinde bunları sınırlama iki yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="c532d-112">hello Cluster Resource Manager has two ways of computing costs and limiting them while it tries toomanage hello cluster.</span></span> <span data-ttu-id="c532d-113">Merhaba ilk mekanizması yalnızca onu yapacağınız her taşıma sayım.</span><span class="sxs-lookup"><span data-stu-id="c532d-113">hello first mechanism is simply counting every move that it would make.</span></span> <span data-ttu-id="c532d-114">İki çözümleri ile hello oluşturuluyorsa hello Küme Kaynak Yöneticisi'ni (taşır toplam sayısı) en düşük maliyeti hello ile hello birini tercih sonra aynı (puan) dengeleyin.</span><span class="sxs-lookup"><span data-stu-id="c532d-114">If two solutions are generated with about hello same balance (score), then hello Cluster Resource Manager prefers hello one with hello lowest cost (total number of moves).</span></span>

<span data-ttu-id="c532d-115">Bu strateji de çalışır.</span><span class="sxs-lookup"><span data-stu-id="c532d-115">This strategy works well.</span></span> <span data-ttu-id="c532d-116">Ancak varsayılan veya statik yükleri'te olduğu gibi tüm taşır eşit herhangi karmaşık sisteminde tahmin edilemez.</span><span class="sxs-lookup"><span data-stu-id="c532d-116">But as with default or static loads, it's unlikely in any complex system that all moves are equal.</span></span> <span data-ttu-id="c532d-117">Büyük olasılıkla toobe çok daha pahalı bazılarıdır.</span><span class="sxs-lookup"><span data-stu-id="c532d-117">Some are likely toobe much more expensive.</span></span>

## <a name="setting-move-costs"></a><span data-ttu-id="c532d-118">Ayar maliyetleri taşıyın</span><span class="sxs-lookup"><span data-stu-id="c532d-118">Setting Move Costs</span></span> 
<span data-ttu-id="c532d-119">Oluşturulduğunda hello varsayılan taşıma maliyeti bir hizmet için belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c532d-119">You can specify hello default move cost for a service when it is created:</span></span>

<span data-ttu-id="c532d-120">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c532d-120">PowerShell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -DefaultMoveCost Medium
```

<span data-ttu-id="c532d-121">C# ' TA:</span><span class="sxs-lookup"><span data-stu-id="c532d-121">C#:</span></span> 

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
//set up hello rest of hello ServiceDescription
serviceDescription.DefaultMoveCost = MoveCost.Medium;
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

<span data-ttu-id="c532d-122">Ayrıca, belirtin veya hello hizmeti oluşturulduktan sonra MoveCost bir hizmet için dinamik olarak güncelleştir:</span><span class="sxs-lookup"><span data-stu-id="c532d-122">You can also specify or update MoveCost dynamically for a service after hello service has been created:</span></span> 

<span data-ttu-id="c532d-123">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c532d-123">PowerShell:</span></span> 

```posh
Update-ServiceFabricService -Stateful -ServiceName "fabric:/AppName/ServiceName" -DefaultMoveCost High
```

<span data-ttu-id="c532d-124">C# ' TA:</span><span class="sxs-lookup"><span data-stu-id="c532d-124">C#:</span></span>

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.DefaultMoveCost = MoveCost.High;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/AppName/ServiceName"), updateDescription);
```

## <a name="dynamically-specifying-move-cost-on-a-per-replica-basis"></a><span data-ttu-id="c532d-125">Taşıma maliyeti yineleme başına temelinde dinamik olarak belirtme</span><span class="sxs-lookup"><span data-stu-id="c532d-125">Dynamically specifying move cost on a per-replica basis</span></span>

<span data-ttu-id="c532d-126">Merhaba önceki kod parçacıkları tüm bir tüm hizmetine aynı anda dış hello hizmetin kendisini MoveCost belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="c532d-126">hello preceding snippets are all for specifying MoveCost for a whole service at once from outside hello service itself.</span></span> <span data-ttu-id="c532d-127">Ancak, maliyeti en yararlı olduğu zaman taşımak hello taşıma maliyeti belirli hizmeti nesnesi, kullanım ömrü değiştirir.</span><span class="sxs-lookup"><span data-stu-id="c532d-127">However, move cost is most useful is when hello move cost of a specific service object changes over its lifespan.</span></span> <span data-ttu-id="c532d-128">Merhaba kendilerini büyük olasılıkla Hizmetleri bu yana nasıl maliyetli toomove belirli bir zaman oldukları hello en iyi fikir vardır, hizmetleri tooreport çalışma zamanı sırasında tek tek kendi taşıma maliyeti için bir API yoktur.</span><span class="sxs-lookup"><span data-stu-id="c532d-128">Since hello services themselves probably have hello best idea of how costly they are toomove a given time, there's an API for services tooreport their own individual move cost during runtime.</span></span> 

<span data-ttu-id="c532d-129">C# ' TA:</span><span class="sxs-lookup"><span data-stu-id="c532d-129">C#:</span></span>

```csharp
this.Partition.ReportMoveCost(MoveCost.Medium);
```

## <a name="impact-of-move-cost"></a><span data-ttu-id="c532d-130">Taşıma maliyeti etkisi</span><span class="sxs-lookup"><span data-stu-id="c532d-130">Impact of move cost</span></span>
<span data-ttu-id="c532d-131">MoveCost dört düzeyi vardır: sıfır, düşük, Orta ve yüksek.</span><span class="sxs-lookup"><span data-stu-id="c532d-131">MoveCost has four levels: Zero, Low, Medium, and High.</span></span> <span data-ttu-id="c532d-132">MoveCosts sıfır dışında diğer, göreli tooeach ' dir.</span><span class="sxs-lookup"><span data-stu-id="c532d-132">MoveCosts are relative tooeach other, except for Zero.</span></span> <span data-ttu-id="c532d-133">Sıfır taşıma maliyeti hareket ücretsizdir ve hello çözüm hello puan karşı saymak değil anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="c532d-133">Zero move cost means that movement is free and should not count against hello score of hello solution.</span></span> <span data-ttu-id="c532d-134">TooHigh maliyet taşınma mu ayarı *değil* garanti bu hello çoğaltma tek bir yerde kalır.</span><span class="sxs-lookup"><span data-stu-id="c532d-134">Setting your move cost tooHigh does *not* guarantee that hello replica stays in one place.</span></span>

<span data-ttu-id="c532d-135"><center>
![Taşıma için çoğaltmalar seçerek bir etmen olarak taşıma maliyeti][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="c532d-135"><center>
![Move cost as a factor in selecting replicas for movement][Image1]
</center></span></span>

<span data-ttu-id="c532d-136">MoveCost neden az kesintiye genel hello ve hala eşdeğer tarihe ulaşan sırasında kolay tooachieve olan hello çözümler bulmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="c532d-136">MoveCost helps you find hello solutions that cause hello least disruption overall and are easiest tooachieve while still arriving at equivalent balance.</span></span> <span data-ttu-id="c532d-137">Bir hizmetin maliyeti kavramı göreli toomany şey olabilir.</span><span class="sxs-lookup"><span data-stu-id="c532d-137">A service’s notion of cost can be relative toomany things.</span></span> <span data-ttu-id="c532d-138">Merhaba, taşıma maliyeti hesaplama en yaygın unsurlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c532d-138">hello most common factors in calculating your move cost are:</span></span>

- <span data-ttu-id="c532d-139">Durum veya hello hizmet toomove gereken veri miktarı Hello.</span><span class="sxs-lookup"><span data-stu-id="c532d-139">hello amount of state or data that hello service has toomove.</span></span>
- <span data-ttu-id="c532d-140">istemci bağlantısının kesilmesi Hello maliyeti.</span><span class="sxs-lookup"><span data-stu-id="c532d-140">hello cost of disconnection of clients.</span></span> <span data-ttu-id="c532d-141">Birincil çoğaltma taşıma genellikle daha bir ikincil çoğaltma taşıma hello maliyeti daha pahalıdır.</span><span class="sxs-lookup"><span data-stu-id="c532d-141">Moving a primary replica is usually more costly than hello cost of moving a secondary replica.</span></span>
- <span data-ttu-id="c532d-142">yürütülen bir işlem kesintiye hello maliyeti.</span><span class="sxs-lookup"><span data-stu-id="c532d-142">hello cost of interrupting an in-flight operation.</span></span> <span data-ttu-id="c532d-143">Bazı işlemler hello veri düzeyini depolamak veya yanıt tooa istemci çağrısında gerçekleştirilen işlemler maliyetlidir.</span><span class="sxs-lookup"><span data-stu-id="c532d-143">Some operations at hello data store level or operations performed in response tooa client call are costly.</span></span> <span data-ttu-id="c532d-144">Toostop istemediğiniz belirli bir noktadan sonra bunları için yoksa.</span><span class="sxs-lookup"><span data-stu-id="c532d-144">After a certain point, you don’t want toostop them if you don’t have to.</span></span> <span data-ttu-id="c532d-145">Bu nedenle Hello işlemi sürerken taşıdığında bu hizmet nesnesi tooreduce hello olasılığını hello taşıma maliyeti artırın.</span><span class="sxs-lookup"><span data-stu-id="c532d-145">So while hello operation is going on, you increase hello move cost of this service object tooreduce hello likelihood that it moves.</span></span> <span data-ttu-id="c532d-146">Merhaba işlemi yapıldığında hello maliyeti arka toonormal ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c532d-146">When hello operation is done, you set hello cost back toonormal.</span></span>

## <a name="enabling-move-cost-in-your-cluster"></a><span data-ttu-id="c532d-147">Taşıma maliyeti kümenizdeki etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="c532d-147">Enabling move cost in your cluster</span></span>
<span data-ttu-id="c532d-148">Sırayla hesaba daha ayrıntılı MoveCosts toobe Merhaba, MoveCost kümenizdeki etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c532d-148">In order for hello more granular MoveCosts toobe taken into account, MoveCost must be enabled in your cluster.</span></span> <span data-ttu-id="c532d-149">Bu ayar olmadan taşır sayım hello varsayılan mod MoveCost hesaplamak için kullanılır ve MoveCost raporları göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="c532d-149">Without this setting, hello default mode of counting moves is used for calculating MoveCost, and MoveCost reports are ignored.</span></span>


<span data-ttu-id="c532d-150">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="c532d-150">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="UseMoveCostReports" Value="true" />
        </Section>
```

<span data-ttu-id="c532d-151">tek başına dağıtımlarında ClusterConfig.json ya da Azure için Template.json aracılığıyla kümeleri barındırılan:</span><span class="sxs-lookup"><span data-stu-id="c532d-151">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "UseMoveCostReports",
          "value": "true"
      }
    ]
  }
]
```

## <a name="next-steps"></a><span data-ttu-id="c532d-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c532d-152">Next steps</span></span>
- <span data-ttu-id="c532d-153">Service Fabric kümesi Kaynak Yöneticisi ölçümleri toomanage kullanım ve kapasite hello kümede kullanır.</span><span class="sxs-lookup"><span data-stu-id="c532d-153">Service Fabric Cluster Resource Manger uses metrics toomanage consumption and capacity in hello cluster.</span></span> <span data-ttu-id="c532d-154">Ölçümler hakkında daha fazla toolearn ve nasıl tooconfigure bunları kullanıma [yönetme kaynak tüketimini ve Service Fabric yük ölçümlerle](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="c532d-154">toolearn more about metrics and how tooconfigure them, check out [Managing resource consumption and load in Service Fabric with metrics](service-fabric-cluster-resource-manager-metrics.md).</span></span>
- <span data-ttu-id="c532d-155">toolearn nasıl hello Küme Kaynak Yöneticisi yönetir ve dengeleyen hello kümedeki yük hakkında kullanıma [Dengeleme Service Fabric kümesi](service-fabric-cluster-resource-manager-balancing.md).</span><span class="sxs-lookup"><span data-stu-id="c532d-155">toolearn about how hello Cluster Resource Manager manages and balances load in hello cluster, check out [Balancing your Service Fabric cluster](service-fabric-cluster-resource-manager-balancing.md).</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-movement-cost/service-most-cost-example.png
