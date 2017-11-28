---
title: "Service Fabric kaynak İdaresi kapsayıcıları ve hizmetler için aaaAzure | Microsoft Docs"
description: "Azure Service Fabric toospecify kaynak sınırları içinde veya dışında kapsayıcıları çalışan hizmetleri sağlar."
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
ms.openlocfilehash: 34e368211d98ff6b5b294c9c8b3af5ca30eeb20c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-governance"></a><span data-ttu-id="0dc50-103">Kaynak İdaresi</span><span class="sxs-lookup"><span data-stu-id="0dc50-103">Resource governance</span></span> 

<span data-ttu-id="0dc50-104">Birden çok hizmet üzerinde çalışan Merhaba, aynı düğüm veya kümenin bir hizmetin diğer hizmetlere starving daha fazla kaynak tüketebilir mümkündür.</span><span class="sxs-lookup"><span data-stu-id="0dc50-104">When running multiple services on hello same node or cluster, it is possible that one service might consume more resources starving other services.</span></span> <span data-ttu-id="0dc50-105">Bu sorunu başvurulan tooas hello gürültülü komşu sorunudur.</span><span class="sxs-lookup"><span data-stu-id="0dc50-105">This problem is referred tooas hello noisy-neighbor problem.</span></span> <span data-ttu-id="0dc50-106">Service Fabric hello Geliştirici toospecify ayırmaları ve hizmet tooguarantee kaynakları başına sınırları sağlar ve ayrıca kaynak kullanımını sınırlama.</span><span class="sxs-lookup"><span data-stu-id="0dc50-106">Service Fabric allows hello developer toospecify reservations and limits per service tooguarantee resources and also limit its resource usage.</span></span> 

## <a name="resource-governance-metrics"></a><span data-ttu-id="0dc50-107">Kaynak İdaresi ölçümleri</span><span class="sxs-lookup"><span data-stu-id="0dc50-107">Resource governance metrics</span></span> 

<span data-ttu-id="0dc50-108">Kaynak İdaresi Service Fabric desteklenir [hizmet paketi](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="0dc50-108">Resource governance is supported in Service Fabric per [Service Package](service-fabric-application-model.md).</span></span> <span data-ttu-id="0dc50-109">tooService paket atanan hello kaynakları daha fazla kod paketler arasında bölünebilir.</span><span class="sxs-lookup"><span data-stu-id="0dc50-109">hello resources that are assigned tooService Package can be further divided between code packages.</span></span> <span data-ttu-id="0dc50-110">Belirtilen hello kaynak sınırları ayrıca hello ayırma hello kaynakların anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="0dc50-110">hello resource limits specified also mean hello reservation of hello resources.</span></span> <span data-ttu-id="0dc50-111">Service Fabric destekler CPU ve bellek iki yerleşik kullanarak hizmet paketi belirtme [ölçümleri](service-fabric-cluster-resource-manager-metrics.md):</span><span class="sxs-lookup"><span data-stu-id="0dc50-111">Service Fabric supports specifying CPU and Memory per service package, using two built-in [metrics](service-fabric-cluster-resource-manager-metrics.md):</span></span>

* <span data-ttu-id="0dc50-112">CPU (ölçüm adı `ServiceFabric:/_CpuCores`): bir çekirdek hello ana makinede kullanılabilir mantıksal bir çekirdek olduğundan ve tüm çekirdek tüm düğümler arasında ağırlıklı aynı hello.</span><span class="sxs-lookup"><span data-stu-id="0dc50-112">CPU (metric name `ServiceFabric:/_CpuCores`): A core is a logical core that is available on hello host machine, and all cores across all nodes are weighted hello same.</span></span>
* <span data-ttu-id="0dc50-113">Bellek (ölçüm adı `ServiceFabric:/_MemoryInMB`): bellek megabayt cinsinden ifade edilir ve hello makinede kullanılabilir toophysical bellek eşler.</span><span class="sxs-lookup"><span data-stu-id="0dc50-113">Memory (metric name `ServiceFabric:/_MemoryInMB`): Memory is expressed in megabytes, and it maps toophysical memory that is available on hello machine.</span></span>

<span data-ttu-id="0dc50-114">Yeni hizmet paketleri kullanılabilir kaynakları aştı açılmasını Hello çalışma zamanı reddeder - yalnızca geçici ayırma garantileri sağlanır.</span><span class="sxs-lookup"><span data-stu-id="0dc50-114">Only soft reservation guarantees are provided - hello runtime rejects opening of new service packages available resources are exceeded.</span></span> <span data-ttu-id="0dc50-115">Ancak, başka bir yürütülebilir dosya veya kapsayıcı hello düğümde yerleştirdiyseniz, hello özgün ayırma garantileri ihlal.</span><span class="sxs-lookup"><span data-stu-id="0dc50-115">However, if another executable or container is placed on hello node, that may violate hello original reservation guarantees.</span></span>

<span data-ttu-id="0dc50-116">Bu iki ölçümleri hello [küme Resource Manager](service-fabric-cluster-resource-manager-cluster-description.md) toplam küme kapasite, hello yük hello kümedeki her düğümde izler ve hello küme kaynaklarında kaldı.</span><span class="sxs-lookup"><span data-stu-id="0dc50-116">For these two metrics, hello [Cluster Resource Manager](service-fabric-cluster-resource-manager-cluster-description.md) tracks total cluster capacity, hello load on each node in hello cluster, and, remaining resources in hello cluster.</span></span> <span data-ttu-id="0dc50-117">Bu iki ölçümleri eşdeğer tooany diğer kullanıcı veya özel bir ölçü ve varolan tüm özellikler bunlarla kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="0dc50-117">These two metrics are equivalent tooany other user or custom metric and all existing features can be used with them:</span></span>
* <span data-ttu-id="0dc50-118">Küme olabilir [dengeli](service-fabric-cluster-resource-manager-balancing.md) toothese iki ölçümleri (varsayılan davranış) göre.</span><span class="sxs-lookup"><span data-stu-id="0dc50-118">Cluster can be [balanced](service-fabric-cluster-resource-manager-balancing.md) according toothese two metrics (default behavior).</span></span>
* <span data-ttu-id="0dc50-119">Küme olabilir [birleştirilmiş](service-fabric-cluster-resource-manager-defragmentation-metrics.md) toothese iki ölçümleri göre.</span><span class="sxs-lookup"><span data-stu-id="0dc50-119">Cluster can be [defragmented](service-fabric-cluster-resource-manager-defragmentation-metrics.md) according toothese two metrics.</span></span>
* <span data-ttu-id="0dc50-120">Zaman [bir küme açıklayan](service-fabric-cluster-resource-manager-cluster-description.md), arabelleğe alınan kapasite iki bu ölçümleri ayarlanabilir.</span><span class="sxs-lookup"><span data-stu-id="0dc50-120">When [describing a cluster](service-fabric-cluster-resource-manager-cluster-description.md), buffered capacity can be set for these two metrics.</span></span>

<span data-ttu-id="0dc50-121">[Dinamik yük raporlama](service-fabric-cluster-resource-manager-metrics.md) bu ölçümleri desteklenmiyor ve bu ölçümleri oluşturma zamanında tanımlanır için yükler.</span><span class="sxs-lookup"><span data-stu-id="0dc50-121">[Dynamic load reporting](service-fabric-cluster-resource-manager-metrics.md) is not supported for these metrics, and loads for these metrics are defined at creation time.</span></span>

## <a name="cluster-set-up-for-enabling-resource-governance"></a><span data-ttu-id="0dc50-122">Küme kümesi kaynak İdaresi etkinleştirmek için</span><span class="sxs-lookup"><span data-stu-id="0dc50-122">Cluster set up for enabling resource governance</span></span>

<span data-ttu-id="0dc50-123">Kapasite el ile Merhaba kümedeki her düğüm türü şu şekilde tanımlanması:</span><span class="sxs-lookup"><span data-stu-id="0dc50-123">Capacity should be defined manually in each node type in hello cluster as follows:</span></span>

```xml
    <NodeType Name="MyNodeType">
      <Capacities>
        <Capacity Name="ServiceFabric:/_CpuCores" Value="4"/>
        <Capacity Name="ServiceFabric:/_MemoryInMB" Value="2048"/>
      </Capacities>
    </NodeType>
```
 
<span data-ttu-id="0dc50-124">Kaynak İdaresi yalnızca kullanıcı Hizmetleri ve sistem hizmetleri üzerinde izin verilir.</span><span class="sxs-lookup"><span data-stu-id="0dc50-124">Resource governance is allowed only on user services and not on any system services.</span></span> <span data-ttu-id="0dc50-125">Kapasite, bazı çekirdek ve bellek belirtirken sol sistem hizmetleri için ayrılmamış gerekir.</span><span class="sxs-lookup"><span data-stu-id="0dc50-125">When specifying capacity, some cores and memory must be left unallocated for system services.</span></span> <span data-ttu-id="0dc50-126">En iyi performans için aşağıdaki ayar hello ayrıca hello küme bildiriminde açık olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="0dc50-126">For optimal performance, hello following setting should also be turned on in hello cluster manifest:</span></span> 

```xml
<Section Name="PlacementAndLoadBalancing">
    <Parameter Name="PreventTransientOvercommit" Value="true" /> 
    <Parameter Name="AllowConstraintCheckFixesDuringApplicationUpgrade" Value="true" />
</Section>
```


## <a name="specifying-resource-governance"></a><span data-ttu-id="0dc50-127">Kaynak İdaresi belirtme</span><span class="sxs-lookup"><span data-stu-id="0dc50-127">Specifying resource governance</span></span> 

<span data-ttu-id="0dc50-128">Kaynak İdaresi sınırları hello uygulama bildirimi (ServiceManifestImport bölümüne) hello aşağıdaki örnekte gösterildiği gibi belirtilir:</span><span class="sxs-lookup"><span data-stu-id="0dc50-128">Resource governance limits are specified in hello application manifest (ServiceManifestImport section) as shown in hello following example:</span></span>

```xml
<?xml version='1.0' encoding='UTF-8'?>
<ApplicationManifest ApplicationTypeName='TestAppTC1' ApplicationTypeVersion='vTC1' xsi:schemaLocation='http://schemas.microsoft.com/2011/01/fabric ServiceFabricServiceModel.xsd' xmlns='http://schemas.microsoft.com/2011/01/fabric' xmlns:xsi='http://www.w3.org/2001/XMLSchema-instance'>
  <Parameters>
  </Parameters>
  <!--
  ServicePackageA has hello number of CPU cores defined, but doesn't have hello MemoryInMB defined.
  In this case, Service Fabric will sum hello limits on code packages and uses hello sum as 
  hello overall ServicePackage limit.
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
  
<span data-ttu-id="0dc50-129">Bu örnekte, hizmet paketi ServicePackageA nereye yerleştirileceğini hello düğümlerinde bir temel alır.</span><span class="sxs-lookup"><span data-stu-id="0dc50-129">In this example, service package ServicePackageA gets one core on hello nodes where it is placed.</span></span> <span data-ttu-id="0dc50-130">Bu hizmet paketi iki kod paket (CodeA1 ve CodeA2) içerir ve her ikisi de hello belirtin `CpuShares` parametresi.</span><span class="sxs-lookup"><span data-stu-id="0dc50-130">This service package contains two code packages (CodeA1 and CodeA2), and both specify hello `CpuShares` parameter.</span></span> <span data-ttu-id="0dc50-131">CpuShares 512:256 Hello oranını hello çekirdek hello iki kod paketler arasında böler.</span><span class="sxs-lookup"><span data-stu-id="0dc50-131">hello proportion of CpuShares 512:256  divides hello core across hello two code packages.</span></span> <span data-ttu-id="0dc50-132">Bu nedenle, bu örnekte, bir çekirdek iki üç CodeA1 alır ve çekirdek üçte CodeA2 alır (ve yazılım garantisi rezervasyonu hello aynı).</span><span class="sxs-lookup"><span data-stu-id="0dc50-132">Thus, in this example, CodeA1 gets two-thirds of a core, and  CodeA2 gets one-third of a core (and a soft-guarantee reservation of hello same).</span></span> <span data-ttu-id="0dc50-133">CpuShares kod paketler için belirtilmediğinde Service Fabric hello çekirdek bunları arasında eşit olarak böler durumda.</span><span class="sxs-lookup"><span data-stu-id="0dc50-133">In case when CpuShares are not specified for code packages, Service Fabric divides hello cores equally among them.</span></span>

<span data-ttu-id="0dc50-134">Her iki kod paketi sınırlı too1024; bu nedenle bellek sınırları absolute MB bellek (ve aynı hello yumuşak garantisi rezervasyonu).</span><span class="sxs-lookup"><span data-stu-id="0dc50-134">Memory limits are absolute, so both code packages are limited too1024 MB of memory (and a soft-guarantee reservation of hello same).</span></span> <span data-ttu-id="0dc50-135">Kod paketler (kapsayıcıları veya işlemler) Bu sınır ve toodo çalışırken daha fazla bellek böylece bir bellek yetersiz özel durum sonuçları mümkün tooallocate yok.</span><span class="sxs-lookup"><span data-stu-id="0dc50-135">Code packages (containers or processes) are not able tooallocate more memory than this limit, and attempting toodo so results in an out-of-memory exception.</span></span> <span data-ttu-id="0dc50-136">Kaynak sınırı zorlaması toowork için bir hizmet paketi içindeki tüm kod paketleri belirtilen bellek sınırlarını olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0dc50-136">For resource limit enforcement toowork, all code packages within a service package should have memory limits specified.</span></span>


## <a name="next-steps"></a><span data-ttu-id="0dc50-137">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0dc50-137">Next steps</span></span>
* <span data-ttu-id="0dc50-138">toolearn daha hakkında Küme Kaynak Yöneticisi, bu okuma [makale](service-fabric-cluster-resource-manager-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="0dc50-138">toolearn more about Cluster Resource Manager, read this [article](service-fabric-cluster-resource-manager-introduction.md).</span></span>
* <span data-ttu-id="0dc50-139">uygulama modeli, hizmet paketleri, kod paketleri ve çoğaltmaları toothem nasıl eşleme hakkında daha fazla toolearn okuma bu [makale](service-fabric-application-model.md).</span><span class="sxs-lookup"><span data-stu-id="0dc50-139">toolearn more about application model, service packages, code packages and how replicas map toothem read this [article](service-fabric-application-model.md).</span></span>
