---
title: "Azure Service Fabric kümesi Bakiye | Microsoft Docs"
description: "Service Fabric kümesi Resource Manager ile kümenizi Dengeleme giriş bilgileri."
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 030b1465-6616-4c0b-8bc7-24ed47d054c0
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: 34eacb29f324025c1d2803c9690600227d3ec457
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="balancing-your-service-fabric-cluster"></a><span data-ttu-id="d1373-103">Service fabric kümesi Dengeleme</span><span class="sxs-lookup"><span data-stu-id="d1373-103">Balancing your service fabric cluster</span></span>
<span data-ttu-id="d1373-104">Service Fabric kümesi kaynak yöneticisi ekleme veya kaldırma işlemleri düğümleri veya hizmetlerin tepki dinamik yük değişiklikleri destekler.</span><span class="sxs-lookup"><span data-stu-id="d1373-104">The Service Fabric Cluster Resource Manager supports dynamic load changes, reacting to additions or removals of nodes or services.</span></span> <span data-ttu-id="d1373-105">Bir kısıtlama ihlali de otomatik olarak düzeltir ve proaktif olarak küme yeniden dengeler.</span><span class="sxs-lookup"><span data-stu-id="d1373-105">It also automatically corrects constraint violations, and proactively rebalances the cluster.</span></span> <span data-ttu-id="d1373-106">Ancak bu eylemler ne sıklıkta alınır ve bunları tetikleyen?</span><span class="sxs-lookup"><span data-stu-id="d1373-106">But how often are these actions taken, and what triggers them?</span></span>

<span data-ttu-id="d1373-107">Küme Kaynak Yöneticisi'ni gerçekleştiren iş üç farklı kategorisi vardır.</span><span class="sxs-lookup"><span data-stu-id="d1373-107">There are three different categories of work that the Cluster Resource Manager performs.</span></span> <span data-ttu-id="d1373-108">Bunlar:</span><span class="sxs-lookup"><span data-stu-id="d1373-108">They are:</span></span>

1. <span data-ttu-id="d1373-109">Yerleştirme – bu aşamada herhangi bir durum bilgisi olan çoğaltmaları veya eksik olan durum bilgisiz örnekleri yerleştirme ile ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="d1373-109">Placement – this stage deals with placing any stateful replicas or stateless instances that are missing.</span></span> <span data-ttu-id="d1373-110">Yerleştirme, hem yeni hizmetleri hem de işleme durum bilgisi olan çoğaltmaları veya başarısız olan durum bilgisiz örnekleri içerir.</span><span class="sxs-lookup"><span data-stu-id="d1373-110">Placement includes both new services and handling stateful replicas or stateless instances that have failed.</span></span> <span data-ttu-id="d1373-111">Silme ve çoğaltmalar veya örnekleri bırakma burada ele alınır.</span><span class="sxs-lookup"><span data-stu-id="d1373-111">Deleting and dropping replicas or instances are handled here.</span></span>
2. <span data-ttu-id="d1373-112">Kısıtlama denetler – Bu aşama olup olmadığını denetler ve farklı kısıtlamalarından (kurallar) sistemi içinde ihlalleri düzeltir.</span><span class="sxs-lookup"><span data-stu-id="d1373-112">Constraint Checks – this stage checks for and corrects violations of the different placement constraints (rules) within the system.</span></span> <span data-ttu-id="d1373-113">Düğümler kapasite değildir ve bir hizmetin kısıtlamalarından karşılandığından emin olduktan gibi şeyler kuralları örnekleridir.</span><span class="sxs-lookup"><span data-stu-id="d1373-113">Examples of rules are things like ensuring that nodes are not over capacity and that a service’s placement constraints are met.</span></span>
3. <span data-ttu-id="d1373-114">– Bu aşama denetler dengelenmesi farklı ölçümleri bakiyesini yapılandırılmış istenilen düzeyine göre gerekli olup olmadığını görmek için Dengeleme.</span><span class="sxs-lookup"><span data-stu-id="d1373-114">Balancing – this stage checks to see if rebalancing is necessary based on the configured desired level of balance for different metrics.</span></span> <span data-ttu-id="d1373-115">Bu durumda daha dengeli kümede düzenleme bulmaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="d1373-115">If so it attempts to find an arrangement in the cluster that is more balanced.</span></span>

## <a name="configuring-cluster-resource-manager-timers"></a><span data-ttu-id="d1373-116">Küme Kaynak Yöneticisi zamanlayıcıları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d1373-116">Configuring Cluster Resource Manager Timers</span></span>
<span data-ttu-id="d1373-117">İlk Dengeleme geçici denetimleri kümesini zamanlayıcılar kümesidir.</span><span class="sxs-lookup"><span data-stu-id="d1373-117">The first set of controls around balancing are a set of timers.</span></span> <span data-ttu-id="d1373-118">Bu zamanlayıcılar ne sıklıkta Küme Kaynak Yöneticisi'ni küme inceler ve düzeltici eylemleri gerçekleştirir yönetir.</span><span class="sxs-lookup"><span data-stu-id="d1373-118">These timers govern how often the Cluster Resource Manager examines the cluster and takes corrective actions.</span></span>

<span data-ttu-id="d1373-119">Küme Kaynak Yöneticisi yapabilir düzeltmeleri farklı bu türlerinin her biri kendi sıklığı yöneten farklı bir Zamanlayıcı tarafından denetlenir.</span><span class="sxs-lookup"><span data-stu-id="d1373-119">Each of these different types of corrections the Cluster Resource Manager can make is controlled by a different timer that governs its frequency.</span></span> <span data-ttu-id="d1373-120">Her Zamanlayıcı başlatıldığında görevi zamanlandı.</span><span class="sxs-lookup"><span data-stu-id="d1373-120">When each timer fires, the task is scheduled.</span></span> <span data-ttu-id="d1373-121">Resource Manager varsayılan olarak:</span><span class="sxs-lookup"><span data-stu-id="d1373-121">By default the Resource Manager:</span></span>

* <span data-ttu-id="d1373-122">durumu tarar ve güncelleştirmeleri (örneğin, bir düğümü çalışmıyor kayıt) uygular her 1/saniyede 10</span><span class="sxs-lookup"><span data-stu-id="d1373-122">scans its state and applies updates (like recording that a node is down) every 1/10th of a second</span></span>
* <span data-ttu-id="d1373-123">yerleştirme denetim bayrağını ayarlar</span><span class="sxs-lookup"><span data-stu-id="d1373-123">sets the placement check flag</span></span> 
* <span data-ttu-id="d1373-124">saniyede kısıtlaması onay bayrağını ayarlar</span><span class="sxs-lookup"><span data-stu-id="d1373-124">sets the constraint check flag every second</span></span>
* <span data-ttu-id="d1373-125">beş saniyede karşı bayrağını ayarlar.</span><span class="sxs-lookup"><span data-stu-id="d1373-125">sets the balancing flag every five seconds.</span></span>

<span data-ttu-id="d1373-126">Aşağıda bu zamanlayıcılar yöneten yapılandırma örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d1373-126">Examples of the configuration governing these timers are below:</span></span>

<span data-ttu-id="d1373-127">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="d1373-127">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PLBRefreshGap" Value="0.1" />
            <Parameter Name="MinPlacementInterval" Value="1.0" />
            <Parameter Name="MinConstraintCheckInterval" Value="1.0" />
            <Parameter Name="MinLoadBalancingInterval" Value="5.0" />
        </Section>
```

<span data-ttu-id="d1373-128">tek başına dağıtımlarında ClusterConfig.json ya da Azure için Template.json aracılığıyla kümeleri barındırılan:</span><span class="sxs-lookup"><span data-stu-id="d1373-128">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "PlacementAndLoadBalancing",
    "parameters": [
      {
          "name": "PLBRefreshGap",
          "value": "0.10"
      },
      {
          "name": "MinPlacementInterval",
          "value": "1.0"
      },
      {
          "name": "MinConstraintCheckInterval",
          "value": "1.0"
      },
      {
          "name": "MinLoadBalancingInterval",
          "value": "5.0"
      }
    ]
  }
]
```

<span data-ttu-id="d1373-129">Bugün Küme Kaynak Yöneticisi'ni yalnızca bu eylemlerden biri, bir kerede sırayla gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="d1373-129">Today the Cluster Resource Manager only performs one of these actions at a time, sequentially.</span></span> <span data-ttu-id="d1373-130">Biz "minimum aralıkları" ve zamanlayıcılar "ayarı bayrakları" devre dışı olduğunda gerçekleştirilecek eylemleri olarak bu zamanlayıcılar başvurmak nedeni budur.</span><span class="sxs-lookup"><span data-stu-id="d1373-130">This is why we refer to these timers as “minimum intervals” and the actions that get taken when the timers go off as "setting flags".</span></span> <span data-ttu-id="d1373-131">Örneğin, Küme Kaynak Yöneticisi'ni Dengeleme kümesi önce hizmetleri oluşturmak üzere bekleyen istekleri ilgilenir.</span><span class="sxs-lookup"><span data-stu-id="d1373-131">For example, the Cluster Resource Manager takes care of pending requests to create services before balancing the cluster.</span></span> <span data-ttu-id="d1373-132">Belirtilen varsayılan zaman aralıklarına göre gördüğünüz gibi Küme Kaynak Yöneticisi'ni sık yapması gereken her şey için tarar.</span><span class="sxs-lookup"><span data-stu-id="d1373-132">As you can see by the default time intervals specified, the Cluster Resource Manager scans for anything it needs to do frequently.</span></span> <span data-ttu-id="d1373-133">Normalde bu her adımı sırasında yapılan değişiklikler kümesi küçük olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="d1373-133">Normally this means that the set of changes made during each step is small.</span></span> <span data-ttu-id="d1373-134">Sık olarak küçük değişiklikler Küme Kaynağı Yöneticisi'nin şeyler kümede gerçekleştiğinde esnek olmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="d1373-134">Making small changes frequently allows the Cluster Resource Manager to be responsive when things happen in the cluster.</span></span> <span data-ttu-id="d1373-135">Varsayılan zamanlayıcılar olayları aynı türde çoğunu aynı anda ortaya eğilimindedir bu yana bazı yığınlama sağlar.</span><span class="sxs-lookup"><span data-stu-id="d1373-135">The default timers provide some batching since many of the same types of events tend to occur simultaneously.</span></span> 

<span data-ttu-id="d1373-136">Örneğin, başarısız olduğunda düğümleri aynı anda kadar tüm hata etki alanlarını yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1373-136">For example, when nodes fail they can do so entire fault domains at a time.</span></span> <span data-ttu-id="d1373-137">Tüm bu hatalar sonraki durum sırasında yakalanan güncelleştirme sonra *PLBRefreshGap*.</span><span class="sxs-lookup"><span data-stu-id="d1373-137">All these failures are captured during the next state update after the *PLBRefreshGap*.</span></span> <span data-ttu-id="d1373-138">Düzeltmeleri, kısıtlama denetimi gibi aşağıdaki yerleştirme sırasında belirlenir ve Dengeleme çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="d1373-138">The corrections are determined during the following placement, constraint check, and balancing runs.</span></span> <span data-ttu-id="d1373-139">Varsayılan olarak Küme Kaynak Yöneticisi'ni değil kümesindeki değişiklikleri saatlik aracılığıyla tarama ve adresi aynı anda tüm değişiklikleri çalışılıyor.</span><span class="sxs-lookup"><span data-stu-id="d1373-139">By default the Cluster Resource Manager is not scanning through hours of changes in the cluster and trying to address all changes at once.</span></span> <span data-ttu-id="d1373-140">Bunun yapılması karmaşası WINS'e için yol açar.</span><span class="sxs-lookup"><span data-stu-id="d1373-140">Doing so would lead to bursts of churn.</span></span>

<span data-ttu-id="d1373-141">Küme Kaynak Yöneticisi'ni de belirlemek için bazı ek bilgiler gerekir imbalanced küme.</span><span class="sxs-lookup"><span data-stu-id="d1373-141">The Cluster Resource Manager also needs some additional information to determine if the cluster imbalanced.</span></span> <span data-ttu-id="d1373-142">İçin sahip olduğumuz iki parça yapılandırma: *BalancingThresholds* ve *ActivityThresholds*.</span><span class="sxs-lookup"><span data-stu-id="d1373-142">For that we have two other pieces of configuration: *BalancingThresholds* and *ActivityThresholds*.</span></span>

## <a name="balancing-thresholds"></a><span data-ttu-id="d1373-143">Dengeleme eşikleri</span><span class="sxs-lookup"><span data-stu-id="d1373-143">Balancing thresholds</span></span>
<span data-ttu-id="d1373-144">Dengeleme eşik dengelenmesi tetiklemek ana denetimdir.</span><span class="sxs-lookup"><span data-stu-id="d1373-144">A Balancing Threshold is the main control for triggering rebalancing.</span></span> <span data-ttu-id="d1373-145">Ölçüm için Dengeleme eşik bir _oranı_.</span><span class="sxs-lookup"><span data-stu-id="d1373-145">The Balancing Threshold for a metric is a _ratio_.</span></span> <span data-ttu-id="d1373-146">Bu ölçüm ait bir ölçüm yük miktarı az yüklenen düğümde bölü en yüklenen düğümde yük aşarsa, *BalancingThreshold*, küme imbalanced olur.</span><span class="sxs-lookup"><span data-stu-id="d1373-146">If the load for a metric on the most loaded node divided by the amount of load on the least loaded node exceeds that metric's *BalancingThreshold*, then the cluster is imbalanced.</span></span> <span data-ttu-id="d1373-147">Sonuç olarak Dengeleme Küme Kaynak Yöneticisi'ni denetlediğinde tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="d1373-147">As a result balancing is triggered the next time the Cluster Resource Manager checks.</span></span> <span data-ttu-id="d1373-148">*MinLoadBalancingInterval* Zamanlayıcı tanımlar dengelenmesi gerekliyse, Küme Kaynak Yöneticisi ' ne sıklıkta denetlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d1373-148">The *MinLoadBalancingInterval* timer defines how often the Cluster Resource Manager should check if rebalancing is necessary.</span></span> <span data-ttu-id="d1373-149">Denetimi, herhangi bir şey olur anlamına gelmez.</span><span class="sxs-lookup"><span data-stu-id="d1373-149">Checking doesn't mean that anything happens.</span></span> 

<span data-ttu-id="d1373-150">Dengeleme eşikleri küme tanımının bir parçası olarak ölçüm başına temelinde tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="d1373-150">Balancing Thresholds are defined on a per-metric basis as a part of the cluster definition.</span></span> <span data-ttu-id="d1373-151">Ölçümler hakkında daha fazla bilgi için kullanıma [bu makalede](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="d1373-151">For more information on metrics, check out [this article](service-fabric-cluster-resource-manager-metrics.md).</span></span>

<span data-ttu-id="d1373-152">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="d1373-152">ClusterManifest.xml</span></span>

```xml
    <Section Name="MetricBalancingThresholds">
      <Parameter Name="MetricName1" Value="2"/>
      <Parameter Name="MetricName2" Value="3.5"/>
    </Section>
```

<span data-ttu-id="d1373-153">tek başına dağıtımlarında ClusterConfig.json ya da Azure için Template.json aracılığıyla kümeleri barındırılan:</span><span class="sxs-lookup"><span data-stu-id="d1373-153">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "MetricBalancingThresholds",
    "parameters": [
      {
          "name": "MetricName1",
          "value": "2"
      },
      {
          "name": "MetricName2",
          "value": "3.5"
      }
    ]
  }
]
```

<span data-ttu-id="d1373-154"><center>
![Eşik örnek Dengeleme][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="d1373-154"><center>
![Balancing Threshold Example][Image1]
</center></span></span>

<span data-ttu-id="d1373-155">Bu örnekte, her hizmetin bazı ölçüsünün bir birimi kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="d1373-155">In this example, each service is consuming one unit of some metric.</span></span> <span data-ttu-id="d1373-156">Üst örnekte, bir düğümde en fazla yük beştir ve iki en düşük gereksinimdir.</span><span class="sxs-lookup"><span data-stu-id="d1373-156">In the top example, the maximum load on a node is five and the minimum is two.</span></span> <span data-ttu-id="d1373-157">Bu ölçüm karşı eşiği üç olduğunu düşünelim.</span><span class="sxs-lookup"><span data-stu-id="d1373-157">Let’s say that the balancing threshold for this metric is three.</span></span> <span data-ttu-id="d1373-158">Kümedeki oranı 5/2 olduğundan 2.5 ve diğer bir deyişle belirtilenden daha az = üç eşiğinin Dengeleme, küme dengelenir.</span><span class="sxs-lookup"><span data-stu-id="d1373-158">Since the ratio in the cluster is 5/2 = 2.5 and that is less than the specified balancing threshold of three, the cluster is balanced.</span></span> <span data-ttu-id="d1373-159">Küme Kaynak Yöneticisi'ni denetlediğinde dengelemesiz tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="d1373-159">No balancing is triggered when the Cluster Resource Manager checks.</span></span>

<span data-ttu-id="d1373-160">En az iki oranı beş içinde kaynaklanan olsa da alt örnekte bir düğümde en fazla yük 10 ' dur.</span><span class="sxs-lookup"><span data-stu-id="d1373-160">In the bottom example, the maximum load on a node is 10, while the minimum is two, resulting in a ratio of five.</span></span> <span data-ttu-id="d1373-161">Beş üç bu ölçümü için belirlenen karşı eşiği değerinden daha büyük.</span><span class="sxs-lookup"><span data-stu-id="d1373-161">Five is greater than the designated balancing threshold of three for that metric.</span></span> <span data-ttu-id="d1373-162">Sonuç olarak, bir çalıştırma dengelenmesi karşı Zamanlayıcı harekete zamanlanan sonraki sefer olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d1373-162">As a result, a rebalancing run will be scheduled next time the balancing timer fires.</span></span> <span data-ttu-id="d1373-163">Böyle bir durumda bazı yük Düğüm3 için genellikle dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="d1373-163">In a situation like this some load is usually distributed to Node3.</span></span> <span data-ttu-id="d1373-164">Service Fabric kümesi Kaynak Yöneticisi doyumsuz bir yaklaşım kullanmadığı için bazı yükleme Düğüm2 için de dağıtılmış.</span><span class="sxs-lookup"><span data-stu-id="d1373-164">Because the Service Fabric Cluster Resource Manager doesn't use a greedy approach, some load could also be distributed to Node2.</span></span> 

<span data-ttu-id="d1373-165"><center>
![Eşik örnek Eylemler Dengeleme][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="d1373-165"><center>
![Balancing Threshold Example Actions][Image2]
</center></span></span>

> [!NOTE]
> <span data-ttu-id="d1373-166">"Dengeleme" Yük kümenizdeki yönetmek için iki farklı stratejileri işler.</span><span class="sxs-lookup"><span data-stu-id="d1373-166">"Balancing" handles two different strategies for managing load in your cluster.</span></span> <span data-ttu-id="d1373-167">Küme Kaynak Yöneticisi'ni kullanan varsayılan strateji, kümedeki düğümler arasında yük dağıtmaktır.</span><span class="sxs-lookup"><span data-stu-id="d1373-167">The default strategy that the Cluster Resource Manager uses is to distribute load across the nodes in the cluster.</span></span> <span data-ttu-id="d1373-168">Diğer strateji [birleştirme](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="d1373-168">The other strategy is [defragmentation](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span></span> <span data-ttu-id="d1373-169">Birleştirme aynı Dengeleme çalışması sırasında gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="d1373-169">Defragmentation is performed during the same balancing run.</span></span> <span data-ttu-id="d1373-170">Yük Dengeleme ve birleştirme stratejilerini aynı kümedeki farklı ölçümleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="d1373-170">The balancing and defragmentation strategies can be used for different metrics within the same cluster.</span></span> <span data-ttu-id="d1373-171">Bir hizmetin Dengeleme ve birleştirme ölçümleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="d1373-171">A service can have both balancing and defragmentation metrics.</span></span> <span data-ttu-id="d1373-172">Birleştirme ölçümleri için kümedeki yükleri oranını tetikler olduğunda dengelenmesi _aşağıda_ karşı eşiği.</span><span class="sxs-lookup"><span data-stu-id="d1373-172">For defragmentation metrics, the ratio of the loads in the cluster triggers rebalancing when it is _below_ the balancing threshold.</span></span> 
>

<span data-ttu-id="d1373-173">Dengeleme eşiğin altına alma, açık bir hedef değil.</span><span class="sxs-lookup"><span data-stu-id="d1373-173">Getting below the balancing threshold is not an explicit goal.</span></span> <span data-ttu-id="d1373-174">Dengeleme eşikleri olan yalnızca bir *tetikleyici*.</span><span class="sxs-lookup"><span data-stu-id="d1373-174">Balancing Thresholds are just a *trigger*.</span></span> <span data-ttu-id="d1373-175">Çalıştırır Dengeleme olduğunda Küme Kaynak Yöneticisi'ni varsa bunu yapabilirsiniz, hangi iyileştirmeleri belirler.</span><span class="sxs-lookup"><span data-stu-id="d1373-175">When balancing runs, the Cluster Resource Manager determines what improvements it can make, if any.</span></span> <span data-ttu-id="d1373-176">Karşı arama yalnızca koparılan devre dışı olduğundan, hiçbir şey taşır anlamına gelmez.</span><span class="sxs-lookup"><span data-stu-id="d1373-176">Just because a balancing search is kicked off doesn't mean anything moves.</span></span> <span data-ttu-id="d1373-177">Bazen küme imbalanced ancak düzeltmek için çok kısıtlanmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="d1373-177">Sometimes the cluster is imbalanced but too constrained to correct.</span></span> <span data-ttu-id="d1373-178">Alternatif olarak, çok hareketleri geliştirmeleri gerektiren [pahalı](service-fabric-cluster-resource-manager-movement-cost.md)).</span><span class="sxs-lookup"><span data-stu-id="d1373-178">Alternatively, the improvements require movements that are too [costly](service-fabric-cluster-resource-manager-movement-cost.md)).</span></span>

## <a name="activity-thresholds"></a><span data-ttu-id="d1373-179">Etkinlik eşikleri</span><span class="sxs-lookup"><span data-stu-id="d1373-179">Activity thresholds</span></span>
<span data-ttu-id="d1373-180">Bazen, düğümleri görece imbalanced olmasına rağmen *toplam* yük devretme kümesinde miktarı düşük.</span><span class="sxs-lookup"><span data-stu-id="d1373-180">Sometimes, although nodes are relatively imbalanced, the *total* amount of load in the cluster is low.</span></span> <span data-ttu-id="d1373-181">Yük eksikliği geçici DIP olabilir ya da küme yeni yalnızca alma olduğundan ve önyükleme içinde.</span><span class="sxs-lookup"><span data-stu-id="d1373-181">The lack of load could be a transient dip, or because the cluster is new and just getting bootstrapped.</span></span> <span data-ttu-id="d1373-182">Her iki durumda da olduğundan biraz kazanılacak Dengeleme kümesi süre beklemesini istemeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1373-182">In either case, you may not want to spend time balancing the cluster because there’s little to be gained.</span></span> <span data-ttu-id="d1373-183">Küme Dengeleme yapılan, ağ harcamanız ve işlem kaynaklarını daha büyük yapmadan şeyler hareket etmek için *mutlak* fark.</span><span class="sxs-lookup"><span data-stu-id="d1373-183">If the cluster underwent balancing, you’d spend network and compute resources to move things around without making any large *absolute* difference.</span></span> <span data-ttu-id="d1373-184">Önlemek için gereksiz taşır, etkinlik eşikleri bilinen başka bir denetim yoktur.</span><span class="sxs-lookup"><span data-stu-id="d1373-184">To avoid unnecessary moves, there’s another control known as Activity Thresholds.</span></span> <span data-ttu-id="d1373-185">Etkinlik eşikleri bazı mutlak alt bağımlı etkinliğinin belirtmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d1373-185">Activity Thresholds allows you to specify some absolute lower bound for activity.</span></span> <span data-ttu-id="d1373-186">Hiçbir düğümü bu eşiğin üstünde ise, Dengeleme eşiğine olsa bile Dengeleme tetiklenen değil.</span><span class="sxs-lookup"><span data-stu-id="d1373-186">If no node is over this threshold, balancing isn't triggered even if the Balancing Threshold is met.</span></span>

<span data-ttu-id="d1373-187">Biz bizim Dengeleme eşiğinin Bu ölçüm için üç korumak varsayalım.</span><span class="sxs-lookup"><span data-stu-id="d1373-187">Let’s say that we retain our Balancing Threshold of three for this metric.</span></span> <span data-ttu-id="d1373-188">Ayrıca 1536 etkinlik eşiğinin sahibiz varsayalım.</span><span class="sxs-lookup"><span data-stu-id="d1373-188">Let's also say we have an Activity Threshold of 1536.</span></span> <span data-ttu-id="d1373-189">Küme Dengeleme var. eşik imbalanced olsa ilk durumda, bu etkinlik eşik hiçbir düğümü hiçbir şey olmaz şekilde karşılar.</span><span class="sxs-lookup"><span data-stu-id="d1373-189">In the first case, while the cluster is imbalanced per the Balancing Threshold there's no node meets that Activity Threshold, so nothing happens.</span></span> <span data-ttu-id="d1373-190">Alt örnekte Düğüm1 etkinliği eşiğin üstünde ' dir.</span><span class="sxs-lookup"><span data-stu-id="d1373-190">In the bottom example, Node1 is over the Activity Threshold.</span></span> <span data-ttu-id="d1373-191">Dengeleme eşik ve ölçüm etkinlik eşiği aştığından, Dengeleme zamanlanır.</span><span class="sxs-lookup"><span data-stu-id="d1373-191">Since both the Balancing Threshold and the Activity Threshold for the metric are exceeded, balancing is scheduled.</span></span> <span data-ttu-id="d1373-192">Örnek olarak, aşağıdaki diyagramda bakalım:</span><span class="sxs-lookup"><span data-stu-id="d1373-192">As an example, let's look at the following diagram:</span></span> 

<span data-ttu-id="d1373-193"><center>
![Etkinlik eşik örneği][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="d1373-193"><center>
![Activity Threshold Example][Image3]
</center></span></span>

<span data-ttu-id="d1373-194">Yalnızca Dengeleme eşikleri gibi etkinlik eşikleri tanımlı başına Metrik Küme tanımı aracılığıyla şunlardır:</span><span class="sxs-lookup"><span data-stu-id="d1373-194">Just like Balancing Thresholds, Activity Thresholds are defined per-metric via the cluster definition:</span></span>

<span data-ttu-id="d1373-195">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="d1373-195">ClusterManifest.xml</span></span>

``` xml
    <Section Name="MetricActivityThresholds">
      <Parameter Name="Memory" Value="1536"/>
    </Section>
```

<span data-ttu-id="d1373-196">tek başına dağıtımlarında ClusterConfig.json ya da Azure için Template.json aracılığıyla kümeleri barındırılan:</span><span class="sxs-lookup"><span data-stu-id="d1373-196">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

```json
"fabricSettings": [
  {
    "name": "MetricActivityThresholds",
    "parameters": [
      {
          "name": "Memory",
          "value": "1536"
      }
    ]
  }
]
```

<span data-ttu-id="d1373-197">Yük Dengeleme ve etkinlik hem Dengeleme belirli bir ölçüm için - bağlı tetiklenir yalnızca Dengeleme eşik ve etkinlik eşiği aşıldı varsa aynı ölçümü eşiklere.</span><span class="sxs-lookup"><span data-stu-id="d1373-197">Balancing and activity thresholds are both tied to a specific metric - balancing is triggered only if both the Balancing Threshold and Activity Threshold is exceeded for the same metric.</span></span>

## <a name="balancing-services-together"></a><span data-ttu-id="d1373-198">Hizmetleri birlikte Dengeleme</span><span class="sxs-lookup"><span data-stu-id="d1373-198">Balancing services together</span></span>
<span data-ttu-id="d1373-199">Küme imbalanced olup olmamasına küme çapında bir karardır.</span><span class="sxs-lookup"><span data-stu-id="d1373-199">Whether the cluster is imbalanced or not is a cluster-wide decision.</span></span> <span data-ttu-id="d1373-200">Ancak, düzeltme hakkında Git şekilde bireysel hizmet çoğaltmaları ve geçici örnekleri taşımaktır.</span><span class="sxs-lookup"><span data-stu-id="d1373-200">However, the way we go about fixing it is moving individual service replicas and instances around.</span></span> <span data-ttu-id="d1373-201">Bu doğru mantıklıdır?</span><span class="sxs-lookup"><span data-stu-id="d1373-201">This makes sense, right?</span></span> <span data-ttu-id="d1373-202">Bellek bir düğümde yığılmış, birden çok çoğaltmalar veya örnekleri için katkıda bulunan.</span><span class="sxs-lookup"><span data-stu-id="d1373-202">If memory is stacked up on one node, multiple replicas or instances could be contributing to it.</span></span> <span data-ttu-id="d1373-203">Dengesizliği düzelttikten herhangi bir durum bilgisi olan çoğaltmaları veya imbalanced ölçümün kullanmak durum bilgisiz örneklerinin hareketli gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="d1373-203">Fixing the imbalance could require moving any of the stateful replicas or stateless instances that use the imbalanced metric.</span></span>

<span data-ttu-id="d1373-204">Bazen imbalanced kendisini değildi bir hizmet taşınmış ancak (yerel tartışma unutmayın ve daha önce genel ağırlık verir).</span><span class="sxs-lookup"><span data-stu-id="d1373-204">Occasionally though, a service that wasn’t itself imbalanced gets moved (remember the discussion of local and global weights earlier).</span></span> <span data-ttu-id="d1373-205">Tüm bu hizmetin ölçümleri dengeli neden bir hizmet taşındığında?</span><span class="sxs-lookup"><span data-stu-id="d1373-205">Why would a service get moved when all that service’s metrics were balanced?</span></span> <span data-ttu-id="d1373-206">Bir örnek görelim:</span><span class="sxs-lookup"><span data-stu-id="d1373-206">Let’s see an example:</span></span>

- <span data-ttu-id="d1373-207">Dört Hizmetleri, Service1, Service2, Service3 ve Service4 varsayalım.</span><span class="sxs-lookup"><span data-stu-id="d1373-207">Let's say there are four services, Service1, Service2, Service3, and Service4.</span></span> 
- <span data-ttu-id="d1373-208">Service1 ölçümleri Metric1 ve Metric2 bildirir.</span><span class="sxs-lookup"><span data-stu-id="d1373-208">Service1 reports metrics Metric1 and Metric2.</span></span> 
- <span data-ttu-id="d1373-209">Service2 ölçümleri Metric2 ve Metric3 bildirir.</span><span class="sxs-lookup"><span data-stu-id="d1373-209">Service2 reports metrics Metric2 and Metric3.</span></span> 
- <span data-ttu-id="d1373-210">Service3 ölçümleri Metric3 ve Metric4 bildirir.</span><span class="sxs-lookup"><span data-stu-id="d1373-210">Service3 reports metrics Metric3 and Metric4.</span></span>
- <span data-ttu-id="d1373-211">Service4 ölçüm Metric99 bildirir.</span><span class="sxs-lookup"><span data-stu-id="d1373-211">Service4 reports metric Metric99.</span></span> 

<span data-ttu-id="d1373-212">Burada burada yapacağız kötülerinden görebilirsiniz: bir zinciri!</span><span class="sxs-lookup"><span data-stu-id="d1373-212">Surely you can see where we’re going here: There's a chain!</span></span> <span data-ttu-id="d1373-213">Biz gerçekten dört bağımsız Hizmetleri yoksa, ilişkili üç hizmeti ve kendi başına kapalıdır bir sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="d1373-213">We don’t really have four independent services, we have three services that are related and one that is off on its own.</span></span>

<span data-ttu-id="d1373-214"><center>
![Hizmetleri birlikte Dengeleme][Image4]
</center></span><span class="sxs-lookup"><span data-stu-id="d1373-214"><center>
![Balancing Services Together][Image4]
</center></span></span>

<span data-ttu-id="d1373-215">Bu zincir nedeniyle bir dengesizliği ölçümleri 1-4, çoğaltmaları veya hizmetleri hareket etmek için 1-3 ait örnekleri neden olabilir. mümkündür.</span><span class="sxs-lookup"><span data-stu-id="d1373-215">Because of this chain, it's possible that an imbalance in metrics 1-4 can cause replicas or instances belonging to services 1-3 to move around.</span></span> <span data-ttu-id="d1373-216">Ölçümleri 1, 2 veya 3 içinde bir dengesizliği içinde Service4 hareketleri sebep olamaz biliyoruz.</span><span class="sxs-lookup"><span data-stu-id="d1373-216">We also know that an imbalance in Metrics 1, 2, or 3 can't cause movements in Service4.</span></span> <span data-ttu-id="d1373-217">Çoğaltmaları taşıyarak bu yana hiçbir noktası olacaktır veya Service4 ait örnekleri ölçümleri 1-3 bakiyesini etkilemeye kesinlikle hiçbir şey yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d1373-217">There would be no point since moving the replicas or instances belonging to Service4 around can do absolutely nothing to impact the balance of Metrics 1-3.</span></span>

<span data-ttu-id="d1373-218">Küme Kaynak Yöneticisi'ni otomatik olarak hangi hizmetlerin ilgili rakamlar.</span><span class="sxs-lookup"><span data-stu-id="d1373-218">The Cluster Resource Manager automatically figures out what services are related.</span></span> <span data-ttu-id="d1373-219">Ekleme, kaldırma veya hizmetleri için ölçümler değiştirme ilişkilerini etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="d1373-219">Adding, removing, or changing the metrics for services can impact their relationships.</span></span> <span data-ttu-id="d1373-220">Örneğin, Service2 Dengeleme iki çalışmaları arasında Metric2 kaldırmak için güncelleştirilmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="d1373-220">For example, between two runs of balancing Service2 may have been updated to remove Metric2.</span></span> <span data-ttu-id="d1373-221">Service1 Service2 arasındaki zinciri keser.</span><span class="sxs-lookup"><span data-stu-id="d1373-221">This breaks the chain between Service1 and Service2.</span></span> <span data-ttu-id="d1373-222">Şimdi yerine iki grup ilgili hizmetlerin vardır üç:</span><span class="sxs-lookup"><span data-stu-id="d1373-222">Now instead of two groups of related services, there are three:</span></span>

<span data-ttu-id="d1373-223"><center>
![Hizmetleri birlikte Dengeleme][Image5]
</center></span><span class="sxs-lookup"><span data-stu-id="d1373-223"><center>
![Balancing Services Together][Image5]
</center></span></span>

## <a name="next-steps"></a><span data-ttu-id="d1373-224">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d1373-224">Next steps</span></span>
* <span data-ttu-id="d1373-225">Service Fabric kümesi Kaynak Yöneticisi, kullanım ve kapasite kümedeki nasıl yönettiğini ölçümleridir.</span><span class="sxs-lookup"><span data-stu-id="d1373-225">Metrics are how the Service Fabric Cluster Resource Manger manages consumption and capacity in the cluster.</span></span> <span data-ttu-id="d1373-226">Ölçümleri ve bunların nasıl yapılandırılacağı hakkında daha fazla bilgi için kullanıma [bu makalede](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="d1373-226">To learn more about metrics and how to configure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>
* <span data-ttu-id="d1373-227">Taşıma maliyeti için Küme Kaynak Yöneticisi'ni, belirli hizmetleri diğerlerinden taşımak daha pahalı sinyal bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="d1373-227">Movement Cost is one way of signaling to the Cluster Resource Manager that certain services are more expensive to move than others.</span></span> <span data-ttu-id="d1373-228">Taşıma maliyeti hakkında daha fazla bilgi için başvurmak [bu makalede](service-fabric-cluster-resource-manager-movement-cost.md)</span><span class="sxs-lookup"><span data-stu-id="d1373-228">For more about movement cost, refer to [this article](service-fabric-cluster-resource-manager-movement-cost.md)</span></span>
* <span data-ttu-id="d1373-229">Küme Kaynak Yöneticisi'ni kümedeki karmaşası aşağı yavaş yapılandırdığınız birkaç kısıtlamaları vardır.</span><span class="sxs-lookup"><span data-stu-id="d1373-229">The Cluster Resource Manager has several throttles that you can configure to slow down churn in the cluster.</span></span> <span data-ttu-id="d1373-230">Bunlar normalde gerekli değildir, ancak bunlara ihtiyacınız varsa bunları hakkında bilgi edinebilirsiniz [burada](service-fabric-cluster-resource-manager-advanced-throttling.md)</span><span class="sxs-lookup"><span data-stu-id="d1373-230">They're not normally necessary, but if you need them you can learn about them [here](service-fabric-cluster-resource-manager-advanced-throttling.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resrouce-manager-balancing-thresholds.png
[Image2]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-threshold-triggered-results.png
[Image3]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-activity-thresholds.png
[Image4]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together1.png
[Image5]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together2.png
