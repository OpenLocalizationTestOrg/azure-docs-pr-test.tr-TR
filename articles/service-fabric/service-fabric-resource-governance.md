---
title: "Azure Service Fabric kaynak İdaresi kapsayıcıları ve hizmetler için | Microsoft Docs"
description: "Azure Service Fabric iç veya dış kapsayıcıları çalışan hizmetler için kaynak sınırları belirtmenize olanak tanır."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 88d44953ad83f9e7401fd087a39842e4a3790124
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="resource-governance"></a><span data-ttu-id="6340c-103">Kaynak İdaresi</span><span class="sxs-lookup"><span data-stu-id="6340c-103">Resource governance</span></span> 

<span data-ttu-id="6340c-104">Birden fazla hizmet aynı düğümü veya küme üzerinde çalışırken, bir hizmetin diğer hizmetlere starving daha fazla kaynak tüketebilir mümkündür.</span><span class="sxs-lookup"><span data-stu-id="6340c-104">When running multiple services on the same node or cluster, it is possible that one service might consume more resources starving other services.</span></span> <span data-ttu-id="6340c-105">Bu sorunu gürültülü komşu sorun olarak adlandırılır.</span><span class="sxs-lookup"><span data-stu-id="6340c-105">This problem is referred to as the noisy-neighbor problem.</span></span> <span data-ttu-id="6340c-106">Service Fabric ayırmaları ve her kaynakları garanti ve ayrıca kaynak kullanımını sınırlamak için hizmet sınırları belirtmek Geliştirici sağlar.</span><span class="sxs-lookup"><span data-stu-id="6340c-106">Service Fabric allows the developer to specify reservations and limits per service to guarantee resources and also limit its resource usage.</span></span> 

## <a name="resource-governance-metrics"></a><span data-ttu-id="6340c-107">Kaynak İdaresi ölçümleri</span><span class="sxs-lookup"><span data-stu-id="6340c-107">Resource governance metrics</span></span> 

<span data-ttu-id="6340c-108">Kaynak İdaresi Service Fabric desteklenir [hizmet paketi](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="6340c-108">Resource governance is supported in Service Fabric per [Service Package](service-fabric-application-model.md).</span></span> <span data-ttu-id="6340c-109">Hizmet Paketi için atanmış olan kaynakları daha fazla kod paketler arasında bölünebilir.</span><span class="sxs-lookup"><span data-stu-id="6340c-109">The resources that are assigned to Service Package can be further divided between code packages.</span></span> <span data-ttu-id="6340c-110">Belirtilen kaynak sınırları ayrıca kaynakları ayırma anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="6340c-110">The resource limits specified also mean the reservation of the resources.</span></span> <span data-ttu-id="6340c-111">Service Fabric destekler CPU ve bellek iki yerleşik kullanarak hizmet paketi belirtme [ölçümleri](service-fabric-cluster-resource-manager-metrics.md):</span><span class="sxs-lookup"><span data-stu-id="6340c-111">Service Fabric supports specifying CPU and Memory per service package, using two built-in [metrics](service-fabric-cluster-resource-manager-metrics.md):</span></span>

* <span data-ttu-id="6340c-112">CPU (ölçüm adı `ServiceFabric:/_CpuCores`): bir çekirdek ana makinede kullanılabilir mantıksal bir çekirdek olduğundan ve tüm çekirdek tüm düğümler arasında ağırlıklı aynı.</span><span class="sxs-lookup"><span data-stu-id="6340c-112">CPU (metric name `ServiceFabric:/_CpuCores`): A core is a logical core that is available on the host machine, and all cores across all nodes are weighted the same.</span></span>
* <span data-ttu-id="6340c-113">Bellek (ölçüm adı `ServiceFabric:/_MemoryInMB`): bellek megabayt cinsinden ifade edilir ve makinede kullanılabilir fiziksel bellek eşler.</span><span class="sxs-lookup"><span data-stu-id="6340c-113">Memory (metric name `ServiceFabric:/_MemoryInMB`): Memory is expressed in megabytes, and it maps to physical memory that is available on the machine.</span></span>

<span data-ttu-id="6340c-114">Yeni hizmet paketleri kullanılabilir kaynakları aştı açılmasını çalışma zamanı reddeder - yalnızca geçici ayırma garantileri sağlanır.</span><span class="sxs-lookup"><span data-stu-id="6340c-114">Only soft reservation guarantees are provided - the runtime rejects opening of new service packages available resources are exceeded.</span></span> <span data-ttu-id="6340c-115">Ancak, başka bir yürütülebilir dosya veya kapsayıcı düğümde yerleştirdiyseniz, özgün ayırma garantileri ihlal.</span><span class="sxs-lookup"><span data-stu-id="6340c-115">However, if another executable or container is placed on the node, that may violate the original reservation guarantees.</span></span>

<span data-ttu-id="6340c-116">Bu iki ölçümler için [küme Resource Manager](service-fabric-cluster-resource-manager-cluster-description.md) toplam küme kapasite, kümedeki her düğümde yük izler ve küme kaynaklarında kaldı.</span><span class="sxs-lookup"><span data-stu-id="6340c-116">For these two metrics, the [Cluster Resource Manager](service-fabric-cluster-resource-manager-cluster-description.md) tracks total cluster capacity, the load on each node in the cluster, and, remaining resources in the cluster.</span></span> <span data-ttu-id="6340c-117">Bu iki ölçümleri herhangi bir diğer kullanıcı veya özel bir ölçü eşdeğerdir ve varolan tüm özellikler bunlarla kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="6340c-117">These two metrics are equivalent to any other user or custom metric and all existing features can be used with them:</span></span>
* <span data-ttu-id="6340c-118">Küme olabilir [dengeli](service-fabric-cluster-resource-manager-balancing.md) göre bu iki ölçümleri (varsayılan davranıştır).</span><span class="sxs-lookup"><span data-stu-id="6340c-118">Cluster can be [balanced](service-fabric-cluster-resource-manager-balancing.md) according to these two metrics (default behavior).</span></span>
* <span data-ttu-id="6340c-119">Küme olabilir [birleştirilmiş](service-fabric-cluster-resource-manager-defragmentation-metrics.md) bu iki ölçümleri göre.</span><span class="sxs-lookup"><span data-stu-id="6340c-119">Cluster can be [defragmented](service-fabric-cluster-resource-manager-defragmentation-metrics.md) according to these two metrics.</span></span>
* <span data-ttu-id="6340c-120">Zaman [bir küme açıklayan](service-fabric-cluster-resource-manager-cluster-description.md), arabelleğe alınan kapasite iki bu ölçümleri ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="6340c-120">When [describing a cluster](service-fabric-cluster-resource-manager-cluster-description.md), buffered capacity can be set for these two metrics.</span></span>

<span data-ttu-id="6340c-121">[Dinamik yük raporlama](service-fabric-cluster-resource-manager-metrics.md) bu ölçümleri desteklenmiyor ve bu ölçümleri oluşturma zamanında tanımlanır için yükler.</span><span class="sxs-lookup"><span data-stu-id="6340c-121">[Dynamic load reporting](service-fabric-cluster-resource-manager-metrics.md) is not supported for these metrics, and loads for these metrics are defined at creation time.</span></span>

## <a name="cluster-set-up-for-enabling-resource-governance"></a><span data-ttu-id="6340c-122">Küme kümesi kaynak İdaresi etkinleştirmek için</span><span class="sxs-lookup"><span data-stu-id="6340c-122">Cluster set up for enabling resource governance</span></span>

<span data-ttu-id="6340c-123">Kapasite el ile kümedeki her düğüm türü şu şekilde tanımlanması:</span><span class="sxs-lookup"><span data-stu-id="6340c-123">Capacity should be defined manually in each node type in the cluster as follows:</span></span>

```xml
    <NodeType Name="MyNodeType">
      <Capacities>
        <Capacity Name="ServiceFabric:/_CpuCores" Value="4"/>
        <Capacity Name="ServiceFabric:/_MemoryInMB" Value="2048"/>
      </Capacities>
    </NodeType>
```
 
<span data-ttu-id="6340c-124">Kaynak İdaresi yalnızca kullanıcı Hizmetleri ve sistem hizmetleri üzerinde izin verilir.</span><span class="sxs-lookup"><span data-stu-id="6340c-124">Resource governance is allowed only on user services and not on any system services.</span></span> <span data-ttu-id="6340c-125">Kapasite, bazı çekirdek ve bellek belirtirken sol sistem hizmetleri için ayrılmamış gerekir.</span><span class="sxs-lookup"><span data-stu-id="6340c-125">When specifying capacity, some cores and memory must be left unallocated for system services.</span></span> <span data-ttu-id="6340c-126">En iyi performans için aşağıdaki ayar da küme bildiriminde açık olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="6340c-126">For optimal performance, the following setting should also be turned on in the cluster manifest:</span></span> 

```xml
<Section Name="PlacementAndLoadBalancing">
    <Parameter Name="PreventTransientOvercommit" Value="true" /> 
    <Parameter Name="AllowConstraintCheckFixesDuringApplicationUpgrade" Value="true" />
</Section>
```


## <a name="specifying-resource-governance"></a><span data-ttu-id="6340c-127">Kaynak İdaresi belirtme</span><span class="sxs-lookup"><span data-stu-id="6340c-127">Specifying resource governance</span></span> 

<span data-ttu-id="6340c-128">Kaynak İdaresi sınırları uygulama bildirimi (ServiceManifestImport bölümüne) aşağıdaki örnekte gösterildiği gibi belirtilir:</span><span class="sxs-lookup"><span data-stu-id="6340c-128">Resource governance limits are specified in the application manifest (ServiceManifestImport section) as shown in the following example:</span></span>

```xml
<?xml version='1.0' encoding='UTF-8'?>
<ApplicationManifest ApplicationTypeName='TestAppTC1' ApplicationTypeVersion='vTC1' xsi:schemaLocation='http://schemas.microsoft.com/2011/01/fabric ServiceFabricServiceModel.xsd' xmlns='http://schemas.microsoft.com/2011/01/fabric' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance'>
  <Parameters>
  </Parameters>
  <!--
  ServicePackageA has the number of CPU cores defined, but doesn't have the MemoryInMB defined.
  In this case, Service Fabric will sum the limits on code packages and uses the sum as 
  the overall ServicePackage limit.
  -->
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName='ServicePackageA' ServiceManifestVersion='v1'/>
    <Policies>
      <ServicePackageResourceGovernancePolicy CpuCores="1"/>
      <ResourceGovernancePolicy CodePackageRef="CodeA1" CpuShares="512" MemoryInMB="1000" />
      <ResourceGovernancePolicy CodePackageRef="CodeA2" CpuShares="256" MemoryInMB="1000" />
    </Policies>
  </ServiceManifestImport>
```
  
<span data-ttu-id="6340c-129">Bu örnekte, hizmet paketi ServicePackageA nereye yerleştirileceğini düğümlerinde bir temel alır.</span><span class="sxs-lookup"><span data-stu-id="6340c-129">In this example, service package ServicePackageA gets one core on the nodes where it is placed.</span></span> <span data-ttu-id="6340c-130">Bu hizmet paketi iki kod paket (CodeA1 ve CodeA2) içerir ve her ikisini de belirtin `CpuShares` parametresi.</span><span class="sxs-lookup"><span data-stu-id="6340c-130">This service package contains two code packages (CodeA1 and CodeA2), and both specify the `CpuShares` parameter.</span></span> <span data-ttu-id="6340c-131">CpuShares 512:256 oranını çekirdek iki kod paket arasında böler.</span><span class="sxs-lookup"><span data-stu-id="6340c-131">The proportion of CpuShares 512:256  divides the core across the two code packages.</span></span> <span data-ttu-id="6340c-132">Bu nedenle, bu örnekte, bir çekirdek iki üç CodeA1 alır ve CodeA2 üçte bir çekirdek (ve aynı yazılım garantisi ayırma) alır.</span><span class="sxs-lookup"><span data-stu-id="6340c-132">Thus, in this example, CodeA1 gets two-thirds of a core, and  CodeA2 gets one-third of a core (and a soft-guarantee reservation of the same).</span></span> <span data-ttu-id="6340c-133">Ne zaman CpuShares kod paketler için belirtilmeyen durumunda, Service Fabric çekirdek bunları arasında eşit olarak böler.</span><span class="sxs-lookup"><span data-stu-id="6340c-133">In case when CpuShares are not specified for code packages, Service Fabric divides the cores equally among them.</span></span>

<span data-ttu-id="6340c-134">Her iki kod paketi için 1024 MB bellek (ve aynı yazılım garantisi ayırma) sınırlı olacak şekilde bellek sınırları kesin.</span><span class="sxs-lookup"><span data-stu-id="6340c-134">Memory limits are absolute, so both code packages are limited to 1024 MB of memory (and a soft-guarantee reservation of the same).</span></span> <span data-ttu-id="6340c-135">Kod paketleri (kapsayıcılar veya işlemler) bu sınırı aşan miktarda bellek ayıramazlar ve bunu denediklerinde yetersiz bellek özel durumu ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="6340c-135">Code packages (containers or processes) are not able to allocate more memory than this limit, and attempting to do so results in an out-of-memory exception.</span></span> <span data-ttu-id="6340c-136">Kaynak sınırı zorlamasının çalışması için, hizmet paketi içindeki tüm kod paketlerinin bellek sınırlarının belirtilmiş olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6340c-136">For resource limit enforcement to work, all code packages within a service package should have memory limits specified.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6340c-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6340c-137">Next steps</span></span>
* <span data-ttu-id="6340c-138">Küme Kaynak Yöneticisi hakkında daha fazla bilgi için bu okuma [makale](service-fabric-cluster-resource-manager-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="6340c-138">To learn more about Cluster Resource Manager, read this [article](service-fabric-cluster-resource-manager-introduction.md).</span></span>
* <span data-ttu-id="6340c-139">Uygulama modeli hakkında daha fazla bilgi için hizmet paketleri, kod paketleri ve nasıl çoğaltmaları için eşleştirebilirsiniz bu okuma [makale](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="6340c-139">To learn more about application model, service packages, code packages and how replicas map to them read this [article](service-fabric-application-model.md).</span></span>
