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
ms.openlocfilehash: 5de07c259d1d327d0211338c2911804445dd6b60
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="service-movement-cost"></a><span data-ttu-id="ef837-103">Hizmet taşıma maliyeti</span><span class="sxs-lookup"><span data-stu-id="ef837-103">Service movement cost</span></span>
<span data-ttu-id="ef837-104">Service Fabric kümesi Kaynak Yöneticisi bir kümeye değişikliklerini ne belirlemeye çalışırken göz önünde bulundurur bir faktör bu değişiklikleri maliyetidir.</span><span class="sxs-lookup"><span data-stu-id="ef837-104">A factor that the Service Fabric Cluster Resource Manager considers when trying to determine what changes to make to a cluster is the cost of those changes.</span></span> <span data-ttu-id="ef837-105">"Maliyet" kavramı kapalı ne kadar küme karşı geliştirilebilir ticareti.</span><span class="sxs-lookup"><span data-stu-id="ef837-105">The notion of "cost" is traded off against how much the cluster can be improved.</span></span> <span data-ttu-id="ef837-106">Maliyet Dengeleme, birleştirme ve diğer gereksinimler için hizmetler taşırken hesaba katıldığında.</span><span class="sxs-lookup"><span data-stu-id="ef837-106">Cost is factored in when moving services for balancing, defragmentation, and other requirements.</span></span> <span data-ttu-id="ef837-107">En az kesintiye uğratan veya pahalı yolu gereksinimlerini karşılamak için belirtilir.</span><span class="sxs-lookup"><span data-stu-id="ef837-107">The goal is to meet the requirements in the least disruptive or expensive way.</span></span> 

<span data-ttu-id="ef837-108">Hizmetleri maliyetleri CPU süresi taşıma ve ağ bant genişliği en az.</span><span class="sxs-lookup"><span data-stu-id="ef837-108">Moving services costs CPU time and network bandwidth at a minimum.</span></span> <span data-ttu-id="ef837-109">Durum bilgisi olan hizmetler için ek bellek ve disk tüketen hizmetlerin durumu kopyalama gerektiriyor.</span><span class="sxs-lookup"><span data-stu-id="ef837-109">For stateful services, it requires copying the state of those services, consuming additional memory and disk.</span></span> <span data-ttu-id="ef837-110">Azure Service Fabric kümesi Resource Manager ile gelir çözümleri maliyetini en aza kümenin kaynakları gereksiz yere harcanan olmayan sağlamaya yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="ef837-110">Minimizing the cost of solutions that the Azure Service Fabric Cluster Resource Manager comes up with helps ensure that the cluster's resources aren't spent unnecessarily.</span></span> <span data-ttu-id="ef837-111">Ancak, aynı zamanda kümedeki kaynaklar ayırma önemli ölçüde artırmak çözümleri yoksay istemiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="ef837-111">However, you also don’t want to ignore solutions that would significantly improve the allocation of resources in the cluster.</span></span>

<span data-ttu-id="ef837-112">Küme Kaynak Yöneticisi'ni maliyetleri bilgi işlem ve kümeyi yönetmek denediğinde bunları sınırlama iki yolu vardır.</span><span class="sxs-lookup"><span data-stu-id="ef837-112">The Cluster Resource Manager has two ways of computing costs and limiting them while it tries to manage the cluster.</span></span> <span data-ttu-id="ef837-113">İlk mekanizma basit hale getirir her taşıma sayım.</span><span class="sxs-lookup"><span data-stu-id="ef837-113">The first mechanism is simply counting every move that it would make.</span></span> <span data-ttu-id="ef837-114">İki çözümleri ile aynı oluşturuluyorsa Bakiye (puan), en düşük maliyeti (taşır toplam sayısı) sahip bir küme Kaynak Yöneticisi'ni tercih sonra.</span><span class="sxs-lookup"><span data-stu-id="ef837-114">If two solutions are generated with about the same balance (score), then the Cluster Resource Manager prefers the one with the lowest cost (total number of moves).</span></span>

<span data-ttu-id="ef837-115">Bu strateji de çalışır.</span><span class="sxs-lookup"><span data-stu-id="ef837-115">This strategy works well.</span></span> <span data-ttu-id="ef837-116">Ancak varsayılan veya statik yükleri'te olduğu gibi tüm taşır eşit herhangi karmaşık sisteminde tahmin edilemez.</span><span class="sxs-lookup"><span data-stu-id="ef837-116">But as with default or static loads, it's unlikely in any complex system that all moves are equal.</span></span> <span data-ttu-id="ef837-117">Bazı çok daha pahalı olması muhtemeldir.</span><span class="sxs-lookup"><span data-stu-id="ef837-117">Some are likely to be much more expensive.</span></span>

## <a name="setting-move-costs"></a><span data-ttu-id="ef837-118">Ayar maliyetleri taşıyın</span><span class="sxs-lookup"><span data-stu-id="ef837-118">Setting Move Costs</span></span> 
<span data-ttu-id="ef837-119">Varsayılan taşıma maliyeti bir hizmet oluşturulduğunda belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ef837-119">You can specify the default move cost for a service when it is created:</span></span>

<span data-ttu-id="ef837-120">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ef837-120">PowerShell:</span></span>

```posh
New-ServiceFabricService -ApplicationName $applicationName -ServiceName $serviceName -ServiceTypeName $serviceTypeName –Stateful -MinReplicaSetSize 3 -TargetReplicaSetSize 3 -PartitionSchemeSingleton -DefaultMoveCost Medium
```

<span data-ttu-id="ef837-121">C# ' TA:</span><span class="sxs-lookup"><span data-stu-id="ef837-121">C#:</span></span> 

```csharp
FabricClient fabricClient = new FabricClient();
StatefulServiceDescription serviceDescription = new StatefulServiceDescription();
//set up the rest of the ServiceDescription
serviceDescription.DefaultMoveCost = MoveCost.Medium;
await fabricClient.ServiceManager.CreateServiceAsync(serviceDescription);
```

<span data-ttu-id="ef837-122">Ayrıca, belirtin veya hizmeti oluşturulduktan sonra MoveCost bir hizmet için dinamik olarak güncelleştir:</span><span class="sxs-lookup"><span data-stu-id="ef837-122">You can also specify or update MoveCost dynamically for a service after the service has been created:</span></span> 

<span data-ttu-id="ef837-123">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ef837-123">PowerShell:</span></span> 

```posh
Update-ServiceFabricService -Stateful -ServiceName "fabric:/AppName/ServiceName" -DefaultMoveCost High
```

<span data-ttu-id="ef837-124">C# ' TA:</span><span class="sxs-lookup"><span data-stu-id="ef837-124">C#:</span></span>

```csharp
StatefulServiceUpdateDescription updateDescription = new StatefulServiceUpdateDescription();
updateDescription.DefaultMoveCost = MoveCost.High;
await fabricClient.ServiceManager.UpdateServiceAsync(new Uri("fabric:/AppName/ServiceName"), updateDescription);
```

## <a name="dynamically-specifying-move-cost-on-a-per-replica-basis"></a><span data-ttu-id="ef837-125">Taşıma maliyeti yineleme başına temelinde dinamik olarak belirtme</span><span class="sxs-lookup"><span data-stu-id="ef837-125">Dynamically specifying move cost on a per-replica basis</span></span>

<span data-ttu-id="ef837-126">Önceki kod parçacıkları tüm hizmet dışında aynı anda tüm bir hizmetine MoveCost belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="ef837-126">The preceding snippets are all for specifying MoveCost for a whole service at once from outside the service itself.</span></span> <span data-ttu-id="ef837-127">Ancak, maliyeti en yararlı olduğu zaman taşımak, kullanım ömrü belirli hizmet nesnesi taşıma maliyeti değiştirir.</span><span class="sxs-lookup"><span data-stu-id="ef837-127">However, move cost is most useful is when the move cost of a specific service object changes over its lifespan.</span></span> <span data-ttu-id="ef837-128">Hizmetleri kendilerini büyük olasılıkla nasıl maliyetli belirli bir zaman taşımak için oldukları en iyi fikir sahip olduğundan, bir API Hizmetleri çalışma zamanı sırasında kendi tek taşıma maliyeti raporuna yoktur.</span><span class="sxs-lookup"><span data-stu-id="ef837-128">Since the services themselves probably have the best idea of how costly they are to move a given time, there's an API for services to report their own individual move cost during runtime.</span></span> 

<span data-ttu-id="ef837-129">C# ' TA:</span><span class="sxs-lookup"><span data-stu-id="ef837-129">C#:</span></span>

```csharp
this.Partition.ReportMoveCost(MoveCost.Medium);
```

## <a name="impact-of-move-cost"></a><span data-ttu-id="ef837-130">Taşıma maliyeti etkisi</span><span class="sxs-lookup"><span data-stu-id="ef837-130">Impact of move cost</span></span>
<span data-ttu-id="ef837-131">MoveCost dört düzeyi vardır: sıfır, düşük, Orta ve yüksek.</span><span class="sxs-lookup"><span data-stu-id="ef837-131">MoveCost has four levels: Zero, Low, Medium, and High.</span></span> <span data-ttu-id="ef837-132">MoveCosts birbirine göre dışında sıfırdır.</span><span class="sxs-lookup"><span data-stu-id="ef837-132">MoveCosts are relative to each other, except for Zero.</span></span> <span data-ttu-id="ef837-133">Sıfır taşıma maliyeti hareket ücretsizdir ve çözüm puan karşı saymak değil anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="ef837-133">Zero move cost means that movement is free and should not count against the score of the solution.</span></span> <span data-ttu-id="ef837-134">Yüksek mu için maliyet taşınma ayarı *değil* çoğaltma tek bir yerde kalır garanti edilemez.</span><span class="sxs-lookup"><span data-stu-id="ef837-134">Setting your move cost to High does *not* guarantee that the replica stays in one place.</span></span>

<span data-ttu-id="ef837-135"><center>
![Taşıma için çoğaltmalar seçerek bir etmen olarak taşıma maliyeti][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="ef837-135"><center>
![Move cost as a factor in selecting replicas for movement][Image1]
</center></span></span>

<span data-ttu-id="ef837-136">MoveCost genel en az kesintiye neden ve hala eşdeğer tarihe ulaşan çalışırken elde etmek kolay çözümler bulmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="ef837-136">MoveCost helps you find the solutions that cause the least disruption overall and are easiest to achieve while still arriving at equivalent balance.</span></span> <span data-ttu-id="ef837-137">Bir hizmetin maliyeti kavramı pek çok göreli olabilir.</span><span class="sxs-lookup"><span data-stu-id="ef837-137">A service’s notion of cost can be relative to many things.</span></span> <span data-ttu-id="ef837-138">Taşıma maliyeti hesaplama en yaygın unsurlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="ef837-138">The most common factors in calculating your move cost are:</span></span>

- <span data-ttu-id="ef837-139">Durum veya taşımak için hizmet olan verilerin miktarı.</span><span class="sxs-lookup"><span data-stu-id="ef837-139">The amount of state or data that the service has to move.</span></span>
- <span data-ttu-id="ef837-140">İstemci bağlantısının kesilmesi maliyeti.</span><span class="sxs-lookup"><span data-stu-id="ef837-140">The cost of disconnection of clients.</span></span> <span data-ttu-id="ef837-141">Birincil çoğaltma taşıma genellikle daha bir ikincil çoğaltma taşıma maliyeti daha pahalıdır.</span><span class="sxs-lookup"><span data-stu-id="ef837-141">Moving a primary replica is usually more costly than the cost of moving a secondary replica.</span></span>
- <span data-ttu-id="ef837-142">Yürütülen bir işlem kesintiye maliyeti.</span><span class="sxs-lookup"><span data-stu-id="ef837-142">The cost of interrupting an in-flight operation.</span></span> <span data-ttu-id="ef837-143">Bazı işlemler veri düzeyini depolamak veya yanıt olarak bir istemci çağrısı gerçekleştirilen işlemler maliyetlidir.</span><span class="sxs-lookup"><span data-stu-id="ef837-143">Some operations at the data store level or operations performed in response to a client call are costly.</span></span> <span data-ttu-id="ef837-144">Belirli bir bir noktadan sonra için yoksa sonlandırmasına istemezsiniz.</span><span class="sxs-lookup"><span data-stu-id="ef837-144">After a certain point, you don’t want to stop them if you don’t have to.</span></span> <span data-ttu-id="ef837-145">Bu nedenle işlemi sürerken taşıdığında olasılığını azaltmak için bu hizmeti nesnesinin taşıma maliyetini artırır.</span><span class="sxs-lookup"><span data-stu-id="ef837-145">So while the operation is going on, you increase the move cost of this service object to reduce the likelihood that it moves.</span></span> <span data-ttu-id="ef837-146">İşlemi bittiğinde, maliyet geri normal ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ef837-146">When the operation is done, you set the cost back to normal.</span></span>

## <a name="enabling-move-cost-in-your-cluster"></a><span data-ttu-id="ef837-147">Taşıma maliyeti kümenizdeki etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="ef837-147">Enabling move cost in your cluster</span></span>
<span data-ttu-id="ef837-148">Dikkate alınması daha ayrıntılı MoveCosts için sırayla MoveCost kümenizdeki etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ef837-148">In order for the more granular MoveCosts to be taken into account, MoveCost must be enabled in your cluster.</span></span> <span data-ttu-id="ef837-149">Bu ayar olmadan taşır sayım varsayılan mod MoveCost hesaplamak için kullanılır ve MoveCost raporları göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="ef837-149">Without this setting, the default mode of counting moves is used for calculating MoveCost, and MoveCost reports are ignored.</span></span>


<span data-ttu-id="ef837-150">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="ef837-150">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="UseMoveCostReports" Value="true" />
        </Section>
```

<span data-ttu-id="ef837-151">tek başına dağıtımlarında ClusterConfig.json ya da Azure için Template.json aracılığıyla kümeleri barındırılan:</span><span class="sxs-lookup"><span data-stu-id="ef837-151">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ef837-152">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ef837-152">Next steps</span></span>
- <span data-ttu-id="ef837-153">Service Fabric kümesi Kaynak Yöneticisi ölçümleri kullanım ve kapasite kümedeki yönetmek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="ef837-153">Service Fabric Cluster Resource Manger uses metrics to manage consumption and capacity in the cluster.</span></span> <span data-ttu-id="ef837-154">Ölçümleri ve bunların nasıl yapılandırılacağı hakkında daha fazla bilgi için kullanıma [yönetme kaynak tüketimini ve Service Fabric yük ölçümlerle](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="ef837-154">To learn more about metrics and how to configure them, check out [Managing resource consumption and load in Service Fabric with metrics](service-fabric-cluster-resource-manager-metrics.md).</span></span>
- <span data-ttu-id="ef837-155">Küme Kaynak Yöneticisi'ni nasıl yönetir ve yük devretme kümesinde dengeleyen hakkında bilgi almak için kullanıma [Dengeleme Service Fabric kümesi](service-fabric-cluster-resource-manager-balancing.md).</span><span class="sxs-lookup"><span data-stu-id="ef837-155">To learn about how the Cluster Resource Manager manages and balances load in the cluster, check out [Balancing your Service Fabric cluster](service-fabric-cluster-resource-manager-balancing.md).</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-movement-cost/service-most-cost-example.png
