---
title: "aaaBalance Azure Service Fabric kümesi | Microsoft Docs"
description: "Bir giriş toobalancing kümenizle hello Service Fabric kümesi Resource Manager."
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
ms.openlocfilehash: 5f7ad2f5cf4cfb3751a860f5293b03d2d5266d99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="balancing-your-service-fabric-cluster"></a><span data-ttu-id="5fac6-103">Service fabric kümesi Dengeleme</span><span class="sxs-lookup"><span data-stu-id="5fac6-103">Balancing your service fabric cluster</span></span>
<span data-ttu-id="5fac6-104">Merhaba Service Fabric kümesi Kaynak Yöneticisi, dinamik yük değişiklikleri, tanımlandığında tooadditions veya düğümler veya hizmetleri kaldırma işlemleri destekler.</span><span class="sxs-lookup"><span data-stu-id="5fac6-104">hello Service Fabric Cluster Resource Manager supports dynamic load changes, reacting tooadditions or removals of nodes or services.</span></span> <span data-ttu-id="5fac6-105">Bir kısıtlama ihlali de otomatik olarak düzeltir ve önceden hello küme yeniden dengeler.</span><span class="sxs-lookup"><span data-stu-id="5fac6-105">It also automatically corrects constraint violations, and proactively rebalances hello cluster.</span></span> <span data-ttu-id="5fac6-106">Ancak bu eylemler ne sıklıkta alınır ve bunları tetikleyen?</span><span class="sxs-lookup"><span data-stu-id="5fac6-106">But how often are these actions taken, and what triggers them?</span></span>

<span data-ttu-id="5fac6-107">Küme Kaynak Yöneticisi'ni gerçekleştirir bu hello iş üç farklı kategorisi vardır.</span><span class="sxs-lookup"><span data-stu-id="5fac6-107">There are three different categories of work that hello Cluster Resource Manager performs.</span></span> <span data-ttu-id="5fac6-108">Bunlar:</span><span class="sxs-lookup"><span data-stu-id="5fac6-108">They are:</span></span>

1. <span data-ttu-id="5fac6-109">Yerleştirme – bu aşamada herhangi bir durum bilgisi olan çoğaltmaları veya eksik olan durum bilgisiz örnekleri yerleştirme ile ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="5fac6-109">Placement – this stage deals with placing any stateful replicas or stateless instances that are missing.</span></span> <span data-ttu-id="5fac6-110">Yerleştirme, hem yeni hizmetleri hem de işleme durum bilgisi olan çoğaltmaları veya başarısız olan durum bilgisiz örnekleri içerir.</span><span class="sxs-lookup"><span data-stu-id="5fac6-110">Placement includes both new services and handling stateful replicas or stateless instances that have failed.</span></span> <span data-ttu-id="5fac6-111">Silme ve çoğaltmalar veya örnekleri bırakma burada ele alınır.</span><span class="sxs-lookup"><span data-stu-id="5fac6-111">Deleting and dropping replicas or instances are handled here.</span></span>
2. <span data-ttu-id="5fac6-112">Kısıtlama denetler – Bu aşama olup olmadığını denetler ve hello farklı yerleştirme kısıtlamaları (kurallar) hello sistem içinde ihlalleri düzeltir.</span><span class="sxs-lookup"><span data-stu-id="5fac6-112">Constraint Checks – this stage checks for and corrects violations of hello different placement constraints (rules) within hello system.</span></span> <span data-ttu-id="5fac6-113">Düğümler kapasite değildir ve bir hizmetin kısıtlamalarından karşılandığından emin olduktan gibi şeyler kuralları örnekleridir.</span><span class="sxs-lookup"><span data-stu-id="5fac6-113">Examples of rules are things like ensuring that nodes are not over capacity and that a service’s placement constraints are met.</span></span>
3. <span data-ttu-id="5fac6-114">Dengeleme – bu aşama dengelenmesi üzerinde yapılandırılmış hello dayalı gerekliyse toosee istenen farklı ölçümleri bakiyesini düzeyini denetler.</span><span class="sxs-lookup"><span data-stu-id="5fac6-114">Balancing – this stage checks toosee if rebalancing is necessary based on hello configured desired level of balance for different metrics.</span></span> <span data-ttu-id="5fac6-115">Öyleyse hello bir düzende küme diğer bir deyişle daha dengeli toofind çalışır.</span><span class="sxs-lookup"><span data-stu-id="5fac6-115">If so it attempts toofind an arrangement in hello cluster that is more balanced.</span></span>

## <a name="configuring-cluster-resource-manager-timers"></a><span data-ttu-id="5fac6-116">Küme Kaynak Yöneticisi zamanlayıcıları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="5fac6-116">Configuring Cluster Resource Manager Timers</span></span>
<span data-ttu-id="5fac6-117">Merhaba ilk Dengeleme geçici denetimleri kümesini zamanlayıcılar kümesidir.</span><span class="sxs-lookup"><span data-stu-id="5fac6-117">hello first set of controls around balancing are a set of timers.</span></span> <span data-ttu-id="5fac6-118">Bu zamanlayıcılar ne sıklıkta hello küme Resource Manager hello küme inceler ve düzeltici eylemleri gerçekleştirir yönetir.</span><span class="sxs-lookup"><span data-stu-id="5fac6-118">These timers govern how often hello Cluster Resource Manager examines hello cluster and takes corrective actions.</span></span>

<span data-ttu-id="5fac6-119">Küme Kaynak Yöneticisi yapabilir düzeltmeleri hello farklı bu türlerinin her biri kendi sıklığı yöneten farklı bir Zamanlayıcı tarafından denetlenir.</span><span class="sxs-lookup"><span data-stu-id="5fac6-119">Each of these different types of corrections hello Cluster Resource Manager can make is controlled by a different timer that governs its frequency.</span></span> <span data-ttu-id="5fac6-120">Her Zamanlayıcı başlatıldığında başlangıç görevi zamanlandı.</span><span class="sxs-lookup"><span data-stu-id="5fac6-120">When each timer fires, hello task is scheduled.</span></span> <span data-ttu-id="5fac6-121">Varsayılan olarak, Resource Manager hello:</span><span class="sxs-lookup"><span data-stu-id="5fac6-121">By default hello Resource Manager:</span></span>

* <span data-ttu-id="5fac6-122">durumu tarar ve güncelleştirmeleri (örneğin, bir düğümü çalışmıyor kayıt) uygular her 1/saniyede 10</span><span class="sxs-lookup"><span data-stu-id="5fac6-122">scans its state and applies updates (like recording that a node is down) every 1/10th of a second</span></span>
* <span data-ttu-id="5fac6-123">Merhaba yerleştirme onay bayrağını ayarlar</span><span class="sxs-lookup"><span data-stu-id="5fac6-123">sets hello placement check flag</span></span> 
* <span data-ttu-id="5fac6-124">saniyede Hello kısıtlaması onay bayrağını ayarlar</span><span class="sxs-lookup"><span data-stu-id="5fac6-124">sets hello constraint check flag every second</span></span>
* <span data-ttu-id="5fac6-125">beş saniyede bayrağı Dengeleme hello ayarlar.</span><span class="sxs-lookup"><span data-stu-id="5fac6-125">sets hello balancing flag every five seconds.</span></span>

<span data-ttu-id="5fac6-126">Aşağıda bu zamanlayıcılar yöneten hello yapılandırma örnekleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="5fac6-126">Examples of hello configuration governing these timers are below:</span></span>

<span data-ttu-id="5fac6-127">ClusterManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="5fac6-127">ClusterManifest.xml:</span></span>

``` xml
        <Section Name="PlacementAndLoadBalancing">
            <Parameter Name="PLBRefreshGap" Value="0.1" />
            <Parameter Name="MinPlacementInterval" Value="1.0" />
            <Parameter Name="MinConstraintCheckInterval" Value="1.0" />
            <Parameter Name="MinLoadBalancingInterval" Value="5.0" />
        </Section>
```

<span data-ttu-id="5fac6-128">tek başına dağıtımlarında ClusterConfig.json ya da Azure için Template.json aracılığıyla kümeleri barındırılan:</span><span class="sxs-lookup"><span data-stu-id="5fac6-128">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="5fac6-129">Bugün hello küme kaynak yöneticisi yalnızca bu eylemlerden biri, aynı anda sırayla gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="5fac6-129">Today hello Cluster Resource Manager only performs one of these actions at a time, sequentially.</span></span> <span data-ttu-id="5fac6-130">"En düşük aralıkları" olarak toothese zamanlayıcılar bakın ve hello zamanlayıcılar "ayarı bayrakları" devre dışı olduğunda gerçekleştirilecek eylemleri hello nedeni budur.</span><span class="sxs-lookup"><span data-stu-id="5fac6-130">This is why we refer toothese timers as “minimum intervals” and hello actions that get taken when hello timers go off as "setting flags".</span></span> <span data-ttu-id="5fac6-131">Örneğin, küme Resource Manager, bekleyen mvc'deki hello hello küme Dengeleme önce toocreate Hizmetleri ister.</span><span class="sxs-lookup"><span data-stu-id="5fac6-131">For example, hello Cluster Resource Manager takes care of pending requests toocreate services before balancing hello cluster.</span></span> <span data-ttu-id="5fac6-132">Belirtilen hello varsayılan zaman aralıklarıyla görebileceğiniz gibi hello küme kaynak yöneticisi için herhangi bir şey bu gereksinimlerini toodo sık tarar.</span><span class="sxs-lookup"><span data-stu-id="5fac6-132">As you can see by hello default time intervals specified, hello Cluster Resource Manager scans for anything it needs toodo frequently.</span></span> <span data-ttu-id="5fac6-133">Normalde bu her adımı sırasında yapılan değişiklikler hello kümesi küçük anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="5fac6-133">Normally this means that hello set of changes made during each step is small.</span></span> <span data-ttu-id="5fac6-134">Şeyler hello kümede gerçekleştiğinde sık olarak küçük değişiklikler hello küme Resource Manager toobe yanıt verir.</span><span class="sxs-lookup"><span data-stu-id="5fac6-134">Making small changes frequently allows hello Cluster Resource Manager toobe responsive when things happen in hello cluster.</span></span> <span data-ttu-id="5fac6-135">Merhaba varsayılan zamanlayıcılar bazı birçok hello itibaren aynı toplu işleme sağlamak olay türleri toooccur aynı anda eğilimi gösterir.</span><span class="sxs-lookup"><span data-stu-id="5fac6-135">hello default timers provide some batching since many of hello same types of events tend toooccur simultaneously.</span></span> 

<span data-ttu-id="5fac6-136">Örneğin, başarısız olduğunda düğümleri aynı anda kadar tüm hata etki alanlarını yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5fac6-136">For example, when nodes fail they can do so entire fault domains at a time.</span></span> <span data-ttu-id="5fac6-137">Tüm bu hatalar hello sonraki durum sırasında yakalanan güncelleştirme hello sonra *PLBRefreshGap*.</span><span class="sxs-lookup"><span data-stu-id="5fac6-137">All these failures are captured during hello next state update after hello *PLBRefreshGap*.</span></span> <span data-ttu-id="5fac6-138">Merhaba düzeltmeleri yerleştirme, kısıtlama denetimi aşağıdaki ve çalıştırmalarını Dengeleme hello sırasında belirlenir.</span><span class="sxs-lookup"><span data-stu-id="5fac6-138">hello corrections are determined during hello following placement, constraint check, and balancing runs.</span></span> <span data-ttu-id="5fac6-139">Varsayılan hello tarafından küme Resource Manager değil hello kümesindeki değişiklikleri saatlik aracılığıyla tarama ve tooaddress tüm değişiklikleri aynı anda çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="5fac6-139">By default hello Cluster Resource Manager is not scanning through hours of changes in hello cluster and trying tooaddress all changes at once.</span></span> <span data-ttu-id="5fac6-140">Bunun yapılması karmaşası toobursts sunulmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="5fac6-140">Doing so would lead toobursts of churn.</span></span>

<span data-ttu-id="5fac6-141">Merhaba küme hello Küme Kaynak Yöneticisi ayrıca bazı ek bilgiler toodetermine imbalanced gerekir.</span><span class="sxs-lookup"><span data-stu-id="5fac6-141">hello Cluster Resource Manager also needs some additional information toodetermine if hello cluster imbalanced.</span></span> <span data-ttu-id="5fac6-142">İçin sahip olduğumuz iki parça yapılandırma: *BalancingThresholds* ve *ActivityThresholds*.</span><span class="sxs-lookup"><span data-stu-id="5fac6-142">For that we have two other pieces of configuration: *BalancingThresholds* and *ActivityThresholds*.</span></span>

## <a name="balancing-thresholds"></a><span data-ttu-id="5fac6-143">Dengeleme eşikleri</span><span class="sxs-lookup"><span data-stu-id="5fac6-143">Balancing thresholds</span></span>
<span data-ttu-id="5fac6-144">Dengeleme eşik dengelenmesi tetiklemek hello ana denetimdir.</span><span class="sxs-lookup"><span data-stu-id="5fac6-144">A Balancing Threshold is hello main control for triggering rebalancing.</span></span> <span data-ttu-id="5fac6-145">Merhaba Dengeleme eşik bir ölçüm için ise bir _oranı_.</span><span class="sxs-lookup"><span data-stu-id="5fac6-145">hello Balancing Threshold for a metric is a _ratio_.</span></span> <span data-ttu-id="5fac6-146">Merhaba üzerinde bir ölçüm için Hello yükü en hello yük miktarı az yüklenen hello bölü düğümü yüklerse Bu ölçüm 's düğümü aşıyor *BalancingThreshold*, hello küme imbalanced olur.</span><span class="sxs-lookup"><span data-stu-id="5fac6-146">If hello load for a metric on hello most loaded node divided by hello amount of load on hello least loaded node exceeds that metric's *BalancingThreshold*, then hello cluster is imbalanced.</span></span> <span data-ttu-id="5fac6-147">Sonuç olarak Dengeleme küme Resource Manager denetler tetiklenen hello sonraki zaman hello olur.</span><span class="sxs-lookup"><span data-stu-id="5fac6-147">As a result balancing is triggered hello next time hello Cluster Resource Manager checks.</span></span> <span data-ttu-id="5fac6-148">Merhaba *MinLoadBalancingInterval* Zamanlayıcı tanımlar dengelenmesi gerekliyse, ne sıklıkta hello küme Resource Manager denetlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5fac6-148">hello *MinLoadBalancingInterval* timer defines how often hello Cluster Resource Manager should check if rebalancing is necessary.</span></span> <span data-ttu-id="5fac6-149">Denetimi, herhangi bir şey olur anlamına gelmez.</span><span class="sxs-lookup"><span data-stu-id="5fac6-149">Checking doesn't mean that anything happens.</span></span> 

<span data-ttu-id="5fac6-150">Dengeleme eşikleri hello küme tanımının bir parçası olarak ölçüm başına temelinde tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="5fac6-150">Balancing Thresholds are defined on a per-metric basis as a part of hello cluster definition.</span></span> <span data-ttu-id="5fac6-151">Ölçümler hakkında daha fazla bilgi için kullanıma [bu makalede](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="5fac6-151">For more information on metrics, check out [this article](service-fabric-cluster-resource-manager-metrics.md).</span></span>

<span data-ttu-id="5fac6-152">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="5fac6-152">ClusterManifest.xml</span></span>

```xml
    <Section Name="MetricBalancingThresholds">
      <Parameter Name="MetricName1" Value="2"/>
      <Parameter Name="MetricName2" Value="3.5"/>
    </Section>
```

<span data-ttu-id="5fac6-153">tek başına dağıtımlarında ClusterConfig.json ya da Azure için Template.json aracılığıyla kümeleri barındırılan:</span><span class="sxs-lookup"><span data-stu-id="5fac6-153">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="5fac6-154"><center>
![Eşik örnek Dengeleme][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="5fac6-154"><center>
![Balancing Threshold Example][Image1]
</center></span></span>

<span data-ttu-id="5fac6-155">Bu örnekte, her hizmetin bazı ölçüsünün bir birimi kullanıyor.</span><span class="sxs-lookup"><span data-stu-id="5fac6-155">In this example, each service is consuming one unit of some metric.</span></span> <span data-ttu-id="5fac6-156">Merhaba üst örnekte, bir düğümde en fazla yük hello beş ve hello en az iki.</span><span class="sxs-lookup"><span data-stu-id="5fac6-156">In hello top example, hello maximum load on a node is five and hello minimum is two.</span></span> <span data-ttu-id="5fac6-157">Bu ölçüm eşiği Dengeleme bu hello üç olduğunu düşünelim.</span><span class="sxs-lookup"><span data-stu-id="5fac6-157">Let’s say that hello balancing threshold for this metric is three.</span></span> <span data-ttu-id="5fac6-158">Merhaba oranı hello kümedeki 5/2 olduğundan 2.5 ve bu, üç, hello küme eşiğinin dengeleme dengeli hello belirtilenden azdır =.</span><span class="sxs-lookup"><span data-stu-id="5fac6-158">Since hello ratio in hello cluster is 5/2 = 2.5 and that is less than hello specified balancing threshold of three, hello cluster is balanced.</span></span> <span data-ttu-id="5fac6-159">Merhaba küme Resource Manager denetlediğinde dengelemesiz tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="5fac6-159">No balancing is triggered when hello Cluster Resource Manager checks.</span></span>

<span data-ttu-id="5fac6-160">Merhaba en az iki oranı beş içinde kaynaklanan ederken hello altındaki örnekte, bir düğümde en fazla yük hello 10 ' dur.</span><span class="sxs-lookup"><span data-stu-id="5fac6-160">In hello bottom example, hello maximum load on a node is 10, while hello minimum is two, resulting in a ratio of five.</span></span> <span data-ttu-id="5fac6-161">Beş hello belirlenen karşı eşiğinin Bu ölçüm için üç değerinden daha büyük.</span><span class="sxs-lookup"><span data-stu-id="5fac6-161">Five is greater than hello designated balancing threshold of three for that metric.</span></span> <span data-ttu-id="5fac6-162">Sonuç olarak, yeniden dengelenemiyor Çalıştır sonraki zamanlanan saat hello Zamanlayıcı ateşlenir Dengeleme olacaktır.</span><span class="sxs-lookup"><span data-stu-id="5fac6-162">As a result, a rebalancing run will be scheduled next time hello balancing timer fires.</span></span> <span data-ttu-id="5fac6-163">Böyle bir durumda bazı genellikle dağıtılmış tooNode3 yüktür.</span><span class="sxs-lookup"><span data-stu-id="5fac6-163">In a situation like this some load is usually distributed tooNode3.</span></span> <span data-ttu-id="5fac6-164">Merhaba Service Fabric kümesi Kaynak Yöneticisi doyumsuz bir yaklaşım kullanmadığı için bazı yükleme dağıtılmış tooNode2 de olabilir.</span><span class="sxs-lookup"><span data-stu-id="5fac6-164">Because hello Service Fabric Cluster Resource Manager doesn't use a greedy approach, some load could also be distributed tooNode2.</span></span> 

<span data-ttu-id="5fac6-165"><center>
![Eşik örnek Eylemler Dengeleme][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="5fac6-165"><center>
![Balancing Threshold Example Actions][Image2]
</center></span></span>

> [!NOTE]
> <span data-ttu-id="5fac6-166">"Dengeleme" Yük kümenizdeki yönetmek için iki farklı stratejileri işler.</span><span class="sxs-lookup"><span data-stu-id="5fac6-166">"Balancing" handles two different strategies for managing load in your cluster.</span></span> <span data-ttu-id="5fac6-167">Küme Kaynak Yöneticisi'ni kullanır hello hello varsayılan stratejisi toodistribute hello kümedeki hello düğümler arasında yüktür.</span><span class="sxs-lookup"><span data-stu-id="5fac6-167">hello default strategy that hello Cluster Resource Manager uses is toodistribute load across hello nodes in hello cluster.</span></span> <span data-ttu-id="5fac6-168">Merhaba diğer stratejidir [birleştirme](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="5fac6-168">hello other strategy is [defragmentation](service-fabric-cluster-resource-manager-defragmentation-metrics.md).</span></span> <span data-ttu-id="5fac6-169">Birleştirme sırasında hello gerçekleştirilen Dengeleme aynı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="5fac6-169">Defragmentation is performed during hello same balancing run.</span></span> <span data-ttu-id="5fac6-170">Merhaba Dengeleme ve birleştirme stratejilerini hello içinde farklı ölçümleri kullanılabilir aynı küme.</span><span class="sxs-lookup"><span data-stu-id="5fac6-170">hello balancing and defragmentation strategies can be used for different metrics within hello same cluster.</span></span> <span data-ttu-id="5fac6-171">Bir hizmetin Dengeleme ve birleştirme ölçümleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="5fac6-171">A service can have both balancing and defragmentation metrics.</span></span> <span data-ttu-id="5fac6-172">Birleştirme ölçümlerini hello hello oranını yükler olduğunda dengelenmesi hello küme Tetikleyicileri _aşağıda_ eşik Dengeleme hello.</span><span class="sxs-lookup"><span data-stu-id="5fac6-172">For defragmentation metrics, hello ratio of hello loads in hello cluster triggers rebalancing when it is _below_ hello balancing threshold.</span></span> 
>

<span data-ttu-id="5fac6-173">Eşik Dengeleme hello alma, açık bir hedef değil.</span><span class="sxs-lookup"><span data-stu-id="5fac6-173">Getting below hello balancing threshold is not an explicit goal.</span></span> <span data-ttu-id="5fac6-174">Dengeleme eşikleri olan yalnızca bir *tetikleyici*.</span><span class="sxs-lookup"><span data-stu-id="5fac6-174">Balancing Thresholds are just a *trigger*.</span></span> <span data-ttu-id="5fac6-175">Çalıştırır Dengeleme olduğunda hello küme Resource Manager bunu yapabilirsiniz, hangi iyileştirmeleri varsa belirler.</span><span class="sxs-lookup"><span data-stu-id="5fac6-175">When balancing runs, hello Cluster Resource Manager determines what improvements it can make, if any.</span></span> <span data-ttu-id="5fac6-176">Karşı arama yalnızca koparılan devre dışı olduğundan, hiçbir şey taşır anlamına gelmez.</span><span class="sxs-lookup"><span data-stu-id="5fac6-176">Just because a balancing search is kicked off doesn't mean anything moves.</span></span> <span data-ttu-id="5fac6-177">Bazen hello imbalanced ancak çok kısıtlanmış toocorrect kümedir.</span><span class="sxs-lookup"><span data-stu-id="5fac6-177">Sometimes hello cluster is imbalanced but too constrained toocorrect.</span></span> <span data-ttu-id="5fac6-178">Alternatif olarak, çok hareketleri hello geliştirmeleri gerektiren [pahalı](service-fabric-cluster-resource-manager-movement-cost.md)).</span><span class="sxs-lookup"><span data-stu-id="5fac6-178">Alternatively, hello improvements require movements that are too [costly](service-fabric-cluster-resource-manager-movement-cost.md)).</span></span>

## <a name="activity-thresholds"></a><span data-ttu-id="5fac6-179">Etkinlik eşikleri</span><span class="sxs-lookup"><span data-stu-id="5fac6-179">Activity thresholds</span></span>
<span data-ttu-id="5fac6-180">Düğümleri görece imbalanced olsa da, bazı durumlarda, hello *toplam* hello kümedeki yük miktarı düşük.</span><span class="sxs-lookup"><span data-stu-id="5fac6-180">Sometimes, although nodes are relatively imbalanced, hello *total* amount of load in hello cluster is low.</span></span> <span data-ttu-id="5fac6-181">Yük Hello eksikliği geçici DIP olabilir veya hello kümesi yeni ve yalnızca alma olduğundan önyükleme içinde.</span><span class="sxs-lookup"><span data-stu-id="5fac6-181">hello lack of load could be a transient dip, or because hello cluster is new and just getting bootstrapped.</span></span> <span data-ttu-id="5fac6-182">Her iki durumda da, elde edilen az toobe olduğundan Dengeleme hello kümesi toospend zaman istemeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5fac6-182">In either case, you may not want toospend time balancing hello cluster because there’s little toobe gained.</span></span> <span data-ttu-id="5fac6-183">Dengeleme Hello küme yapılan, ağ harcamanız ve her büyük yapmadan kaynakları toomove şeyler geçici işlem *mutlak* fark.</span><span class="sxs-lookup"><span data-stu-id="5fac6-183">If hello cluster underwent balancing, you’d spend network and compute resources toomove things around without making any large *absolute* difference.</span></span> <span data-ttu-id="5fac6-184">gereksiz tooavoid taşır, etkinlik eşikleri bilinen başka bir denetim yoktur.</span><span class="sxs-lookup"><span data-stu-id="5fac6-184">tooavoid unnecessary moves, there’s another control known as Activity Thresholds.</span></span> <span data-ttu-id="5fac6-185">Etkinlik eşikleri etkinliği için bazı mutlak alt sınır toospecify sağlar.</span><span class="sxs-lookup"><span data-stu-id="5fac6-185">Activity Thresholds allows you toospecify some absolute lower bound for activity.</span></span> <span data-ttu-id="5fac6-186">Hiçbir düğümü bu eşiğin üstünde ise, hello Dengeleme eşiğine olsa bile Dengeleme tetiklenen değil.</span><span class="sxs-lookup"><span data-stu-id="5fac6-186">If no node is over this threshold, balancing isn't triggered even if hello Balancing Threshold is met.</span></span>

<span data-ttu-id="5fac6-187">Biz bizim Dengeleme eşiğinin Bu ölçüm için üç korumak varsayalım.</span><span class="sxs-lookup"><span data-stu-id="5fac6-187">Let’s say that we retain our Balancing Threshold of three for this metric.</span></span> <span data-ttu-id="5fac6-188">Ayrıca 1536 etkinlik eşiğinin sahibiz varsayalım.</span><span class="sxs-lookup"><span data-stu-id="5fac6-188">Let's also say we have an Activity Threshold of 1536.</span></span> <span data-ttu-id="5fac6-189">Hello ilk durumda, hello küme hello imbalanced olsa eşik Dengeleme var. hiçbir düğüm karşılıyor bu etkinlik eşik, böylece hiçbir şey olmaz.</span><span class="sxs-lookup"><span data-stu-id="5fac6-189">In hello first case, while hello cluster is imbalanced per hello Balancing Threshold there's no node meets that Activity Threshold, so nothing happens.</span></span> <span data-ttu-id="5fac6-190">Merhaba altındaki örnekte Düğüm1 etkinlik eşik hello ' dir.</span><span class="sxs-lookup"><span data-stu-id="5fac6-190">In hello bottom example, Node1 is over hello Activity Threshold.</span></span> <span data-ttu-id="5fac6-191">Her ikisi de Dengeleme eşik hello hello ölçüm Merhaba etkinlik eşiği aşıldı yana Dengeleme zamanlanır.</span><span class="sxs-lookup"><span data-stu-id="5fac6-191">Since both hello Balancing Threshold and hello Activity Threshold for hello metric are exceeded, balancing is scheduled.</span></span> <span data-ttu-id="5fac6-192">Örnek olarak, diyagram aşağıdaki hello bakalım:</span><span class="sxs-lookup"><span data-stu-id="5fac6-192">As an example, let's look at hello following diagram:</span></span> 

<span data-ttu-id="5fac6-193"><center>
![Etkinlik eşik örneği][Image3]
</center></span><span class="sxs-lookup"><span data-stu-id="5fac6-193"><center>
![Activity Threshold Example][Image3]
</center></span></span>

<span data-ttu-id="5fac6-194">Yalnızca Dengeleme eşikleri gibi etkinlik eşikleri tanımlı başına Metrik hello Küme tanımı aracılığıyla şunlardır:</span><span class="sxs-lookup"><span data-stu-id="5fac6-194">Just like Balancing Thresholds, Activity Thresholds are defined per-metric via hello cluster definition:</span></span>

<span data-ttu-id="5fac6-195">ClusterManifest.xml</span><span class="sxs-lookup"><span data-stu-id="5fac6-195">ClusterManifest.xml</span></span>

``` xml
    <Section Name="MetricActivityThresholds">
      <Parameter Name="Memory" Value="1536"/>
    </Section>
```

<span data-ttu-id="5fac6-196">tek başına dağıtımlarında ClusterConfig.json ya da Azure için Template.json aracılığıyla kümeleri barındırılan:</span><span class="sxs-lookup"><span data-stu-id="5fac6-196">via ClusterConfig.json for Standalone deployments or Template.json for Azure hosted clusters:</span></span>

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

<span data-ttu-id="5fac6-197">Yük Dengeleme ve etkinlik eşiklere hem bağlı tooa belirli ölçüm Dengeleme - yalnızca her ikisi de Dengeleme eşik hello ve etkinlik eşiği Merhaba aşıldı tetiklenir aynı Ölçüm.</span><span class="sxs-lookup"><span data-stu-id="5fac6-197">Balancing and activity thresholds are both tied tooa specific metric - balancing is triggered only if both hello Balancing Threshold and Activity Threshold is exceeded for hello same metric.</span></span>

## <a name="balancing-services-together"></a><span data-ttu-id="5fac6-198">Hizmetleri birlikte Dengeleme</span><span class="sxs-lookup"><span data-stu-id="5fac6-198">Balancing services together</span></span>
<span data-ttu-id="5fac6-199">Merhaba küme imbalanced olup olmadığını küme çapında bir karardır.</span><span class="sxs-lookup"><span data-stu-id="5fac6-199">Whether hello cluster is imbalanced or not is a cluster-wide decision.</span></span> <span data-ttu-id="5fac6-200">Ancak, düzeltme hakkında Git hello şekilde bireysel hizmet çoğaltmaları ve geçici örnekleri taşımaktır.</span><span class="sxs-lookup"><span data-stu-id="5fac6-200">However, hello way we go about fixing it is moving individual service replicas and instances around.</span></span> <span data-ttu-id="5fac6-201">Bu doğru mantıklıdır?</span><span class="sxs-lookup"><span data-stu-id="5fac6-201">This makes sense, right?</span></span> <span data-ttu-id="5fac6-202">Bellek bir düğümde yığılmış, birden çok çoğaltmalar veya örnekleri tooit katılan.</span><span class="sxs-lookup"><span data-stu-id="5fac6-202">If memory is stacked up on one node, multiple replicas or instances could be contributing tooit.</span></span> <span data-ttu-id="5fac6-203">Giderilmesi hello dengesizliği herhangi hello durum bilgisi olan çoğaltmaları veya hello imbalanced ölçümün kullanmak durum bilgisiz örneklerinin hareketli gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="5fac6-203">Fixing hello imbalance could require moving any of hello stateful replicas or stateless instances that use hello imbalanced metric.</span></span>

<span data-ttu-id="5fac6-204">Bazen imbalanced kendisini değildi bir hizmet taşınmış ancak (yerel hello tartışma unutmayın ve daha önce genel ağırlık verir).</span><span class="sxs-lookup"><span data-stu-id="5fac6-204">Occasionally though, a service that wasn’t itself imbalanced gets moved (remember hello discussion of local and global weights earlier).</span></span> <span data-ttu-id="5fac6-205">Tüm bu hizmetin ölçümleri dengeli neden bir hizmet taşındığında?</span><span class="sxs-lookup"><span data-stu-id="5fac6-205">Why would a service get moved when all that service’s metrics were balanced?</span></span> <span data-ttu-id="5fac6-206">Bir örnek görelim:</span><span class="sxs-lookup"><span data-stu-id="5fac6-206">Let’s see an example:</span></span>

- <span data-ttu-id="5fac6-207">Dört Hizmetleri, Service1, Service2, Service3 ve Service4 varsayalım.</span><span class="sxs-lookup"><span data-stu-id="5fac6-207">Let's say there are four services, Service1, Service2, Service3, and Service4.</span></span> 
- <span data-ttu-id="5fac6-208">Service1 ölçümleri Metric1 ve Metric2 bildirir.</span><span class="sxs-lookup"><span data-stu-id="5fac6-208">Service1 reports metrics Metric1 and Metric2.</span></span> 
- <span data-ttu-id="5fac6-209">Service2 ölçümleri Metric2 ve Metric3 bildirir.</span><span class="sxs-lookup"><span data-stu-id="5fac6-209">Service2 reports metrics Metric2 and Metric3.</span></span> 
- <span data-ttu-id="5fac6-210">Service3 ölçümleri Metric3 ve Metric4 bildirir.</span><span class="sxs-lookup"><span data-stu-id="5fac6-210">Service3 reports metrics Metric3 and Metric4.</span></span>
- <span data-ttu-id="5fac6-211">Service4 ölçüm Metric99 bildirir.</span><span class="sxs-lookup"><span data-stu-id="5fac6-211">Service4 reports metric Metric99.</span></span> 

<span data-ttu-id="5fac6-212">Burada burada yapacağız kötülerinden görebilirsiniz: bir zinciri!</span><span class="sxs-lookup"><span data-stu-id="5fac6-212">Surely you can see where we’re going here: There's a chain!</span></span> <span data-ttu-id="5fac6-213">Biz gerçekten dört bağımsız Hizmetleri yoksa, ilişkili üç hizmeti ve kendi başına kapalıdır bir sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="5fac6-213">We don’t really have four independent services, we have three services that are related and one that is off on its own.</span></span>

<span data-ttu-id="5fac6-214"><center>
![Hizmetleri birlikte Dengeleme][Image4]
</center></span><span class="sxs-lookup"><span data-stu-id="5fac6-214"><center>
![Balancing Services Together][Image4]
</center></span></span>

<span data-ttu-id="5fac6-215">Bu zincir nedeniyle bir dengesizliği ölçümleri 1-4, çoğaltmalar veya örnekleri tooservices ait geçici 1-3 toomove neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="5fac6-215">Because of this chain, it's possible that an imbalance in metrics 1-4 can cause replicas or instances belonging tooservices 1-3 toomove around.</span></span> <span data-ttu-id="5fac6-216">Ölçümleri 1, 2 veya 3 içinde bir dengesizliği içinde Service4 hareketleri sebep olamaz biliyoruz.</span><span class="sxs-lookup"><span data-stu-id="5fac6-216">We also know that an imbalance in Metrics 1, 2, or 3 can't cause movements in Service4.</span></span> <span data-ttu-id="5fac6-217">Merhaba çoğaltmaları taşıyarak bu yana hiçbir noktası olacaktır veya can geçici tooService4 ait örnekleri kesinlikle hiçbir şey yapmak tooimpact hello Bakiye ölçümleri 1-3.</span><span class="sxs-lookup"><span data-stu-id="5fac6-217">There would be no point since moving hello replicas or instances belonging tooService4 around can do absolutely nothing tooimpact hello balance of Metrics 1-3.</span></span>

<span data-ttu-id="5fac6-218">Merhaba Küme Kaynak Yöneticisi'ni otomatik olarak hangi hizmetlerin ilgili rakamlar.</span><span class="sxs-lookup"><span data-stu-id="5fac6-218">hello Cluster Resource Manager automatically figures out what services are related.</span></span> <span data-ttu-id="5fac6-219">Ekleme, kaldırma veya hizmetleri için değişen hello ölçümleri ilişkilerini etkileyebilir.</span><span class="sxs-lookup"><span data-stu-id="5fac6-219">Adding, removing, or changing hello metrics for services can impact their relationships.</span></span> <span data-ttu-id="5fac6-220">Örneğin, güncelleştirilmiş tooremove Metric2 Service2 Dengeleme iki çalışmaları arasında olabilir.</span><span class="sxs-lookup"><span data-stu-id="5fac6-220">For example, between two runs of balancing Service2 may have been updated tooremove Metric2.</span></span> <span data-ttu-id="5fac6-221">Service1 Service2 arasındaki hello zinciri keser.</span><span class="sxs-lookup"><span data-stu-id="5fac6-221">This breaks hello chain between Service1 and Service2.</span></span> <span data-ttu-id="5fac6-222">Şimdi yerine iki grup ilgili hizmetlerin vardır üç:</span><span class="sxs-lookup"><span data-stu-id="5fac6-222">Now instead of two groups of related services, there are three:</span></span>

<span data-ttu-id="5fac6-223"><center>
![Hizmetleri birlikte Dengeleme][Image5]
</center></span><span class="sxs-lookup"><span data-stu-id="5fac6-223"><center>
![Balancing Services Together][Image5]
</center></span></span>

## <a name="next-steps"></a><span data-ttu-id="5fac6-224">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="5fac6-224">Next steps</span></span>
* <span data-ttu-id="5fac6-225">Kullanım ve kapasite hello kümedeki hello Service Fabric kümesi kaynak yöneticisi nasıl yönettiğini ölçümleridir.</span><span class="sxs-lookup"><span data-stu-id="5fac6-225">Metrics are how hello Service Fabric Cluster Resource Manger manages consumption and capacity in hello cluster.</span></span> <span data-ttu-id="5fac6-226">Ölçümler hakkında daha fazla toolearn ve nasıl tooconfigure bunları kullanıma [bu makalede](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="5fac6-226">toolearn more about metrics and how tooconfigure them, check out [this article](service-fabric-cluster-resource-manager-metrics.md)</span></span>
* <span data-ttu-id="5fac6-227">Taşıma maliyeti belirli hizmetleri diğerlerinden daha pahalı toomove olduğunu toohello küme Resource Manager sinyal bir yoludur.</span><span class="sxs-lookup"><span data-stu-id="5fac6-227">Movement Cost is one way of signaling toohello Cluster Resource Manager that certain services are more expensive toomove than others.</span></span> <span data-ttu-id="5fac6-228">Taşıma maliyeti hakkında daha fazla bilgi için çok başvuran[bu makalede](service-fabric-cluster-resource-manager-movement-cost.md)</span><span class="sxs-lookup"><span data-stu-id="5fac6-228">For more about movement cost, refer too[this article](service-fabric-cluster-resource-manager-movement-cost.md)</span></span>
* <span data-ttu-id="5fac6-229">Merhaba küme Resource Manager hello kümede karmaşası aşağı tooslow yapılandırabilirsiniz birkaç kısıtlamaları vardır.</span><span class="sxs-lookup"><span data-stu-id="5fac6-229">hello Cluster Resource Manager has several throttles that you can configure tooslow down churn in hello cluster.</span></span> <span data-ttu-id="5fac6-230">Bunlar normalde gerekli değildir, ancak bunlara ihtiyacınız varsa bunları hakkında bilgi edinebilirsiniz [burada](service-fabric-cluster-resource-manager-advanced-throttling.md)</span><span class="sxs-lookup"><span data-stu-id="5fac6-230">They're not normally necessary, but if you need them you can learn about them [here](service-fabric-cluster-resource-manager-advanced-throttling.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resrouce-manager-balancing-thresholds.png
[Image2]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-threshold-triggered-results.png
[Image3]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-activity-thresholds.png
[Image4]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together1.png
[Image5]:./media/service-fabric-cluster-resource-manager-balancing/cluster-resource-manager-balancing-services-together2.png
