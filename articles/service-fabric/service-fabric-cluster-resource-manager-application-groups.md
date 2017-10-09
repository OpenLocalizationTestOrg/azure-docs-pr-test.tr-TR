---
title: "aaaService doku Küme Kaynak Yöneticisi - uygulama grupları | Microsoft Docs"
description: "Hello uygulama grubu işlevindeki hello Service Fabric kümesi Kaynak Yöneticisi'ne genel bakış"
services: service-fabric
documentationcenter: .net
author: masnider
manager: timlt
editor: 
ms.assetid: 4cae2370-77b3-49ce-bf40-030400c4260d
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: masnider
ms.openlocfilehash: b4f068862d962b53a0b3ea813b89bb13ee395681
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooapplication-groups"></a><span data-ttu-id="c6617-103">Giriş tooApplication grupları</span><span class="sxs-lookup"><span data-stu-id="c6617-103">Introduction tooApplication Groups</span></span>
<span data-ttu-id="c6617-104">Service Fabric'ın Küme Kaynağı Yöneticisi genellikle hello yük dengelemesini yaparak küme kaynaklarını yönetir (aracılığıyla temsil [ölçümleri](service-fabric-cluster-resource-manager-metrics.md)) hello kümesi boyunca eşit.</span><span class="sxs-lookup"><span data-stu-id="c6617-104">Service Fabric's Cluster Resource Manager typically manages cluster resources by spreading hello load (represented via [Metrics](service-fabric-cluster-resource-manager-metrics.md)) evenly throughout hello cluster.</span></span> <span data-ttu-id="c6617-105">Service Fabric yönetir hello ve hello kümede hello düğümler hello kapasitesini bir bütün olarak [kapasite](service-fabric-cluster-resource-manager-cluster-description.md).</span><span class="sxs-lookup"><span data-stu-id="c6617-105">Service Fabric manages hello capacity of hello nodes in hello cluster and hello cluster as a whole via [capacity](service-fabric-cluster-resource-manager-cluster-description.md).</span></span> <span data-ttu-id="c6617-106">Ölçümleri ve kapasite birçok iş yükü, ancak bazen ek gereksinimleri Getir yoğun olarak kullanılır farklı hizmet doku uygulama örnekleri desenleri harika çalışır.</span><span class="sxs-lookup"><span data-stu-id="c6617-106">Metrics and capacity work great for many workloads, but patterns that make heavy use of different Service Fabric Application Instances sometimes bring in additional requirements.</span></span> <span data-ttu-id="c6617-107">Örneğin, isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c6617-107">For example you may want to:</span></span>

- <span data-ttu-id="c6617-108">Yedek hello kümedeki hello düğümlere bazı kapasite bazı Adlandırılmış uygulama örneği içindeki hello hizmetler için</span><span class="sxs-lookup"><span data-stu-id="c6617-108">Reserve some capacity on hello nodes in hello cluster for hello services within some named application instance</span></span>
- <span data-ttu-id="c6617-109">(Bunları hello tüm küme yaymak) yerine adlandırılmış uygulama örneği içinde hello hizmetleri üzerinde çalışan düğümleri Hello toplam sayısını sınırla</span><span class="sxs-lookup"><span data-stu-id="c6617-109">Limit hello total number of nodes that hello services within a named application instance run on (instead of spreading them out over hello entire cluster)</span></span>
- <span data-ttu-id="c6617-110">Kapasiteleri hello adlandırılmış Uygulama örneğinin kendisinde toolimit hello hello Hizmetleri içindeki hizmetler veya toplam kaynak tüketimini sayısını tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="c6617-110">Define capacities on hello named application instance itself toolimit hello number of services or total resource consumption of hello services inside it</span></span>

<span data-ttu-id="c6617-111">Bu gereksinimleri hello Service Fabric kümesi Kaynak Yöneticisi toomeet uygulama grupları adlı bir özelliği destekler.</span><span class="sxs-lookup"><span data-stu-id="c6617-111">toomeet these requirements, hello Service Fabric Cluster Resource Manager supports a feature called Application Groups.</span></span>

## <a name="limiting-hello-maximum-number-of-nodes"></a><span data-ttu-id="c6617-112">Merhaba en fazla düğüm sayısını sınırlandırma</span><span class="sxs-lookup"><span data-stu-id="c6617-112">Limiting hello maximum number of nodes</span></span>
<span data-ttu-id="c6617-113">Uygulama örneğini gerektiğinde Merhaba basit kullanım uygulama kapasitesi toobe tooa belirli maksimum düğüm sayısı sınırlı bir durumdur.</span><span class="sxs-lookup"><span data-stu-id="c6617-113">hello simplest use case for Application capacity is when an application instance needs toobe limited tooa certain maximum number of nodes.</span></span> <span data-ttu-id="c6617-114">Bu uygulama örneği makine kümesi sayısı üzerine içindeki tüm hizmetler birleştirir.</span><span class="sxs-lookup"><span data-stu-id="c6617-114">This consolidates all services within that application instance onto a set number of machines.</span></span> <span data-ttu-id="c6617-115">Birleştirme toopredict çalıştığınız ya da bu adlandırılmış uygulama örneği içindeki hello hizmetler tarafından fiziksel kaynak kullanımını cap faydalıdır.</span><span class="sxs-lookup"><span data-stu-id="c6617-115">Consolidation is useful when you're trying toopredict or cap physical resource use by hello services within that named application instance.</span></span> 

<span data-ttu-id="c6617-116">Merhaba aşağıdaki resimde bir uygulama örneği ile ve tanımlanan düğüm sayısı üst sınırı olmadan gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="c6617-116">hello following image shows an application instance with and without a maximum number of nodes defined:</span></span>

<span data-ttu-id="c6617-117"><center>
![Uygulama örneği en fazla düğüm sayısını tanımlama][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="c6617-117"><center>
![Application Instance Defining Maximum Number of Nodes][Image1]
</center></span></span>

<span data-ttu-id="c6617-118">Merhaba sol örnekte hello uygulama tanımlı düğüm sayısı üst sınırı yok ve üç hizmeti vardır.</span><span class="sxs-lookup"><span data-stu-id="c6617-118">In hello left example, hello application doesn’t have a maximum number of nodes defined, and it has three services.</span></span> <span data-ttu-id="c6617-119">Hello küme Resource Manager altı kullanılabilir düğümler tooachieve hello iyi dengeyi hello kümedeki (Merhaba, varsayılan davranıştır) üzerinden tüm çoğaltmaları yayılır.</span><span class="sxs-lookup"><span data-stu-id="c6617-119">hello Cluster Resource Manager has spread out all replicas across six available nodes tooachieve hello best balance in hello cluster (hello default behavior).</span></span> <span data-ttu-id="c6617-120">Merhaba sağ örnekte, biz hello bkz aynı uygulama sınırlı toothree düğümleri.</span><span class="sxs-lookup"><span data-stu-id="c6617-120">In hello right example, we see hello same application limited toothree nodes.</span></span>

<span data-ttu-id="c6617-121">Bu davranışı denetler hello parametre en fazla düğüm adı verilir.</span><span class="sxs-lookup"><span data-stu-id="c6617-121">hello parameter that controls this behavior is called MaximumNodes.</span></span> <span data-ttu-id="c6617-122">Bu parametre uygulama oluşturma sırasında ayarlayın veya zaten çalışan bir uygulama örneği için güncelleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="c6617-122">This parameter can be set during application creation, or updated for an application instance that was already running.</span></span>

<span data-ttu-id="c6617-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6617-123">Powershell</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MaximumNodes 3
Update-ServiceFabricApplication –Name fabric:/AppName –MaximumNodes 5
```

<span data-ttu-id="c6617-124">C#</span><span class="sxs-lookup"><span data-stu-id="c6617-124">C#</span></span>

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MaximumNodes = 3;
await fc.ApplicationManager.CreateApplicationAsync(ad);

ApplicationUpdateDescription adUpdate = new ApplicationUpdateDescription(new Uri("fabric:/AppName"));
adUpdate.MaximumNodes = 5;
await fc.ApplicationManager.UpdateApplicationAsync(adUpdate);

```

<span data-ttu-id="c6617-125">Düğümleri Hello kümesinde hello Küme Kaynak Yöneticisi'ni hangi hizmet nesnelerin araya yerleştirilen veya hangi düğümlerin alışmanız garanti etmez.</span><span class="sxs-lookup"><span data-stu-id="c6617-125">Within hello set of nodes, hello Cluster Resource Manager doesn't guarantee which service objects get placed together or which nodes get used.</span></span>

## <a name="application-metrics-load-and-capacity"></a><span data-ttu-id="c6617-126">Uygulama ölçümleri, yükü ve kapasite</span><span class="sxs-lookup"><span data-stu-id="c6617-126">Application Metrics, Load, and Capacity</span></span>
<span data-ttu-id="c6617-127">Uygulama grupları ayrıca belirli adlandırılmış uygulama örneği ve bu ölçümleri için o uygulama örneğinin kapasitesi ile ilişkili toodefine ölçümleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="c6617-127">Application Groups also allow you toodefine metrics associated with a given named application instance, and that application instance's capacity for those metrics.</span></span> <span data-ttu-id="c6617-128">Uygulama ölçümleri tootrack, ayrılmış ve o uygulama örneğinin içine hello Hizmetleri sınırı hello kaynak tüketimini izin verir.</span><span class="sxs-lookup"><span data-stu-id="c6617-128">Application metrics allow you tootrack, reserve, and limit hello resource consumption of hello services inside that application instance.</span></span>

<span data-ttu-id="c6617-129">Her uygulama ölçümü için ayarlanabilir iki değer vardır:</span><span class="sxs-lookup"><span data-stu-id="c6617-129">For each application metric, there are two values that can be set:</span></span>

- <span data-ttu-id="c6617-130">**Toplam uygulama kapasitesinin** – Bu ayar hello hello uygulama belirli bir ölçüm için toplam kapasitesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="c6617-130">**Total Application Capacity** – This setting represents hello total capacity of hello application for a particular metric.</span></span> <span data-ttu-id="c6617-131">Merhaba Küme Kaynak Yöneticisi'ni yeni hizmetlerin toplam yük tooexceed bu değer neden olacağından bu uygulama örneği içinde hello oluşturulmasına izin vermez.</span><span class="sxs-lookup"><span data-stu-id="c6617-131">hello Cluster Resource Manager disallows hello creation of any new services within this application instance that would cause total load tooexceed this value.</span></span> <span data-ttu-id="c6617-132">Örneğin, hello uygulama örneği 10 kapasitesine sahip ve beş yükünü zaten varsayalım.</span><span class="sxs-lookup"><span data-stu-id="c6617-132">For example, let's say hello application instance had a capacity of 10 and already had load of five.</span></span> <span data-ttu-id="c6617-133">10 toplam varsayılan yükü olan bir hizmeti Hello oluşturulması izin verilmeyen.</span><span class="sxs-lookup"><span data-stu-id="c6617-133">hello creation of a service with a total default load of 10 would be disallowed.</span></span>
- <span data-ttu-id="c6617-134">**En fazla düğüm kapasitesi** – Bu ayar, tek bir düğümde hello uygulama için en fazla toplam yükleme hello belirtir.</span><span class="sxs-lookup"><span data-stu-id="c6617-134">**Maximum Node Capacity** – This setting specifies hello maximum total load for hello application on a single node.</span></span> <span data-ttu-id="c6617-135">Yük bu kapasite kalırsa, hello küme Resource Manager hello yükü azaldıktan çoğaltmaları tooother düğümleri taşır.</span><span class="sxs-lookup"><span data-stu-id="c6617-135">If load goes over this capacity, hello Cluster Resource Manager moves replicas tooother nodes so that hello load decreases.</span></span>


<span data-ttu-id="c6617-136">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c6617-136">Powershell:</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -Metrics @("MetricName:Metric1,MaximumNodeCapacity:100,MaximumApplicationCapacity:1000")
```

<span data-ttu-id="c6617-137">C# ' TA:</span><span class="sxs-lookup"><span data-stu-id="c6617-137">C#:</span></span>

``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.TotalApplicationCapacity = 1000;
appMetric.MaximumNodeCapacity = 100;
ad.Metrics.Add(appMetric);
await fc.ApplicationManager.CreateApplicationAsync(ad);
```

## <a name="reserving-capacity"></a><span data-ttu-id="c6617-138">Kapasite ayırma</span><span class="sxs-lookup"><span data-stu-id="c6617-138">Reserving Capacity</span></span>
<span data-ttu-id="c6617-139">Başka bir ortak için uygulama grupları içindeki kaynaklara küme hello tooensure verilen uygulama örneği için ayrılmış kullanılmasıdır.</span><span class="sxs-lookup"><span data-stu-id="c6617-139">Another common use for application groups is tooensure that resources within hello cluster are reserved for a given application instance.</span></span> <span data-ttu-id="c6617-140">Merhaba uygulama örneği oluşturulduğunda hello alanı her zaman ayrılır.</span><span class="sxs-lookup"><span data-stu-id="c6617-140">hello space is always reserved when hello application instance is created.</span></span>

<span data-ttu-id="c6617-141">Bile Merhaba uygulaması hemen gerçekleşir hello küme alanı ayırma:</span><span class="sxs-lookup"><span data-stu-id="c6617-141">Reserving space in hello cluster for hello application happens immediately even when:</span></span>
- <span data-ttu-id="c6617-142">Merhaba uygulama örneği oluşturulur ancak hizmetlerin içindeki henüz yok</span><span class="sxs-lookup"><span data-stu-id="c6617-142">hello application instance is created but doesn't have any services within it yet</span></span>
- <span data-ttu-id="c6617-143">Merhaba uygulama örneği değişiklikleri her zaman içindeki Hizmetler Hello sayısı</span><span class="sxs-lookup"><span data-stu-id="c6617-143">hello number of services within hello application instance changes every time</span></span> 
- <span data-ttu-id="c6617-144">Merhaba Hizmetleri var, ancak hello kaynakları tüketen değil</span><span class="sxs-lookup"><span data-stu-id="c6617-144">hello services exist but aren't consuming hello resources</span></span> 

<span data-ttu-id="c6617-145">İki ek parametreler belirtmek uygulama örneğini gerektirir kaynaklarını ayırma: *düğüm* ve *NodeReservationCapacity*</span><span class="sxs-lookup"><span data-stu-id="c6617-145">Reserving resources for an application instance requires specifying two additional parameters: *MinimumNodes* and *NodeReservationCapacity*</span></span>

- <span data-ttu-id="c6617-146">**En az düğüm** -hello minimum sayısını tanımlar uygulaması hello düğümlerinin örneği çalıştırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="c6617-146">**MinimumNodes** - Defines hello minimum number of nodes that hello application instance should run on.</span></span>  
- <span data-ttu-id="c6617-147">**NodeReservationCapacity** -Merhaba uygulaması için ölçüm başına Bu ayar değildir.</span><span class="sxs-lookup"><span data-stu-id="c6617-147">**NodeReservationCapacity** - This setting is per metric for hello application.</span></span> <span data-ttu-id="c6617-148">Merhaba, burada, hizmetleri çalıştırma Bu uygulamadaki hello herhangi bir düğümde Merhaba uygulaması için ayrılmış bu ölçüm, hello miktarını değerdir.</span><span class="sxs-lookup"><span data-stu-id="c6617-148">hello value is hello amount of that metric reserved for hello application on any node where that hello services in that application run.</span></span>

<span data-ttu-id="c6617-149">Birleştirme **düğüm** ve **NodeReservationCapacity** hello kümedeki hello uygulama için en düşük yük ayırma güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="c6617-149">Combining **MinimumNodes** and **NodeReservationCapacity** guarantees a minimum load reservation for hello application within hello cluster.</span></span> <span data-ttu-id="c6617-150">Daha az kalan varsa hello kapasite küme hello toplam rezervasyon gerekli, Merhaba uygulaması oluşturma başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="c6617-150">If there's less remaining capacity in hello cluster than hello total reservation required, creation of hello application fails.</span></span> 

<span data-ttu-id="c6617-151">Kapasite ayırma bir örneğe bakalım:</span><span class="sxs-lookup"><span data-stu-id="c6617-151">Let's look at an example of capacity reservation:</span></span>

<span data-ttu-id="c6617-152"><center>
![Uygulama örnekleri ayrılmış Kapasite tanımlama][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="c6617-152"><center>
![Application Instances Defining Reserved Capacity][Image2]
</center></span></span>

<span data-ttu-id="c6617-153">Merhaba sol örnekte, uygulamaları herhangi uygulama tanımlı kapasiteye sahip değil.</span><span class="sxs-lookup"><span data-stu-id="c6617-153">In hello left example, applications do not have any Application Capacity defined.</span></span> <span data-ttu-id="c6617-154">Merhaba Küme Kaynağı Yöneticisi her şeyi toonormal kurallarına göre dengeler.</span><span class="sxs-lookup"><span data-stu-id="c6617-154">hello Cluster Resource Manager balances everything according toonormal rules.</span></span>

<span data-ttu-id="c6617-155">Merhaba sağ üzerinde Hello örnekte Application1 ayarları aşağıdaki hello ile oluşturulmuş varsayalım:</span><span class="sxs-lookup"><span data-stu-id="c6617-155">In hello example on hello right, let's say that Application1 was created with hello following settings:</span></span>

- <span data-ttu-id="c6617-156">En az düğüm kümesi tootwo</span><span class="sxs-lookup"><span data-stu-id="c6617-156">MinimumNodes set tootwo</span></span>
- <span data-ttu-id="c6617-157">Bir uygulama ile tanımlanmış ölçümü</span><span class="sxs-lookup"><span data-stu-id="c6617-157">An application Metric defined with</span></span>
  - <span data-ttu-id="c6617-158">20 NodeReservationCapacity</span><span class="sxs-lookup"><span data-stu-id="c6617-158">NodeReservationCapacity of 20</span></span>

<span data-ttu-id="c6617-159">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c6617-159">Powershell</span></span>

 ``` posh
 New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MinimumNodes 2 -Metrics @("MetricName:Metric1,NodeReservationCapacity:20")
 ```

<span data-ttu-id="c6617-160">C#</span><span class="sxs-lookup"><span data-stu-id="c6617-160">C#</span></span>

 ``` csharp
ApplicationDescription ad = new ApplicationDescription();
ad.ApplicationName = new Uri("fabric:/AppName");
ad.ApplicationTypeName = "AppType1";
ad.ApplicationTypeVersion = "1.0.0.0";
ad.MinimumNodes = 2;

var appMetric = new ApplicationMetricDescription();
appMetric.Name = "Metric1";
appMetric.NodeReservationCapacity = 20;

ad.Metrics.Add(appMetric);

await fc.ApplicationManager.CreateApplicationAsync(ad);
```

<span data-ttu-id="c6617-161">Service Fabric Application1 için iki düğüm üzerinde kapasite ayırır ve olsa bile herhangi bir yük Application1 içinde hello Hizmetleri tarafından hello zamanında kullanılan Uygulama2 dizinlerini tooconsume Hizmetleri'nden kapasiteyi izin vermez.</span><span class="sxs-lookup"><span data-stu-id="c6617-161">Service Fabric reserves capacity on two nodes for Application1, and doesn't allow services from Application2 tooconsume that capacity even if there are no load is being consumed by hello services inside Application1 at hello time.</span></span> <span data-ttu-id="c6617-162">Bu ayrılmış uygulama kapasite tüketilen ve kapasite o düğümde ve hello kümedeki kalan hello düşülür değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="c6617-162">This reserved application capacity is considered consumed  and counts against hello remaining capacity on that node and within hello cluster.</span></span>  <span data-ttu-id="c6617-163">Merhaba ayırma küme kapasite hemen kalan hello çıkarılır, hello ayrılmış ancak yalnızca en az bir hizmet nesnesi üzerinde yerleştirildiğinde tüketim belirli bir düğümün hello kapasiteden çıkarılır.</span><span class="sxs-lookup"><span data-stu-id="c6617-163">hello reservation is deducted from hello remaining cluster capacity immediately, however hello reserved consumption is deducted from hello capacity of a specific node only when at least one service object is placed on it.</span></span> <span data-ttu-id="c6617-164">Kaynaklar yalnızca gerekli olduğunda düğümlerinde ayrılmış bu daha sonra bu ayırma esneklik ve daha iyi kaynak kullanımı için sağlar.</span><span class="sxs-lookup"><span data-stu-id="c6617-164">This later reservation allows for flexibility and better resource utilization since resources are only reserved on nodes when needed.</span></span>

## <a name="obtaining-hello-application-load-information"></a><span data-ttu-id="c6617-165">Merhaba uygulama yükleme bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="c6617-165">Obtaining hello application load information</span></span>
<span data-ttu-id="c6617-166">Bir uygulama için bir veya daha fazla ölçümleri tanımlanan kapasiteye sahip her bir uygulama için hello hizmetlerinin çoğaltmaları tarafından bildirilen hello birleşik yükleme hakkında bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c6617-166">For each application that has an Application Capacity defined for one or more metrics you can obtain hello information about hello aggregate load reported by replicas of its services.</span></span>

<span data-ttu-id="c6617-167">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c6617-167">Powershell:</span></span>

``` posh
Get-ServiceFabricApplicationLoad –ApplicationName fabric:/MyApplication1
```

<span data-ttu-id="c6617-168">C#</span><span class="sxs-lookup"><span data-stu-id="c6617-168">C#</span></span>

``` csharp
var v = await fc.QueryManager.GetApplicationLoadInformationAsync("fabric:/MyApplication1");
var metrics = v.ApplicationLoadMetricInformation;
foreach (ApplicationLoadMetricInformation metric in metrics)
{
    Console.WriteLine(metric.ApplicationCapacity);  //total capacity for this metric in this application instance
    Console.WriteLine(metric.ReservationCapacity);  //reserved capacity for this metric in this application instance
    Console.WriteLine(metric.ApplicationLoad);  //current load for this metric in this application instance
}
```

<span data-ttu-id="c6617-169">Merhaba ApplicationLoad sorgu hello hello uygulama için belirtilen uygulama kapasitesi hakkında temel bilgiler döndürür.</span><span class="sxs-lookup"><span data-stu-id="c6617-169">hello ApplicationLoad query returns hello basic information about Application Capacity that was specified for hello application.</span></span> <span data-ttu-id="c6617-170">Bu bilgiler hello Minimum düğümleri ve en fazla düğüm bilgileri ve hello uygulama şu anda kullandığı hello numarasını içerir.</span><span class="sxs-lookup"><span data-stu-id="c6617-170">This information includes hello Minimum Nodes and Maximum Nodes info, and hello number that hello application is currently occupying.</span></span> <span data-ttu-id="c6617-171">Ayrıca her uygulamayı yük ölçüm hakkında bilgi içerir dahil olmak üzere:</span><span class="sxs-lookup"><span data-stu-id="c6617-171">It also includes information about each application load metric, including:</span></span>

* <span data-ttu-id="c6617-172">Ölçüm adı: Hello ölçüm adıdır.</span><span class="sxs-lookup"><span data-stu-id="c6617-172">Metric Name: Name of hello metric.</span></span>
* <span data-ttu-id="c6617-173">Ayırma kapasitesi: hello kümede bu uygulama için ayrılmış küme kapasitesi.</span><span class="sxs-lookup"><span data-stu-id="c6617-173">Reservation Capacity: Cluster Capacity that is reserved in hello cluster for this Application.</span></span>
* <span data-ttu-id="c6617-174">Uygulama yük: Bu uygulamanın alt çoğaltmalarının toplam yük.</span><span class="sxs-lookup"><span data-stu-id="c6617-174">Application Load: Total Load of this Application’s child replicas.</span></span>
* <span data-ttu-id="c6617-175">Uygulama kapasitesi: İzin verilen en yüksek uygulama yük değeri.</span><span class="sxs-lookup"><span data-stu-id="c6617-175">Application Capacity: Maximum permitted value of Application Load.</span></span>

## <a name="removing-application-capacity"></a><span data-ttu-id="c6617-176">Uygulama kapasite kaldırma</span><span class="sxs-lookup"><span data-stu-id="c6617-176">Removing Application Capacity</span></span>
<span data-ttu-id="c6617-177">Merhaba uygulama kapasite parametreleri için bir uygulama ayarlandıktan sonra güncelleştirme uygulama API'leri veya PowerShell cmdlet'leri kullanılarak kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="c6617-177">Once hello Application Capacity parameters are set for an application, they can be removed using Update Application APIs or PowerShell cmdlets.</span></span> <span data-ttu-id="c6617-178">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="c6617-178">For example:</span></span>

``` posh
Update-ServiceFabricApplication –Name fabric:/MyApplication1 –RemoveApplicationCapacity

```

<span data-ttu-id="c6617-179">Bu komut tüm uygulama kapasite yönetim parametreleri hello uygulama örneğinden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="c6617-179">This command removes all Application capacity management parameters from hello application instance.</span></span> <span data-ttu-id="c6617-180">Bu düğüm, en fazla düğüm ve hello uygulamanın ölçümleri varsa içerir.</span><span class="sxs-lookup"><span data-stu-id="c6617-180">This includes MinimumNodes, MaximumNodes, and hello Application's metrics, if any.</span></span> <span data-ttu-id="c6617-181">Merhaba komutu Hello etkisini hemen uygulanır.</span><span class="sxs-lookup"><span data-stu-id="c6617-181">hello effect of hello command is immediate.</span></span> <span data-ttu-id="c6617-182">Bu komut tamamlandıktan sonra hello küme Resource Manager hello varsayılan davranışı uygulamaları yönetmek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="c6617-182">After this command completes, hello Cluster Resource Manager uses hello default behavior for managing applications.</span></span> <span data-ttu-id="c6617-183">Uygulama kapasite parametreleri belirtilebilir yeniden aracılığıyla `Update-ServiceFabricApplication` / `System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.</span><span class="sxs-lookup"><span data-stu-id="c6617-183">Application Capacity parameters can be specified again via `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.</span></span>

### <a name="restrictions-on-application-capacity"></a><span data-ttu-id="c6617-184">Uygulama kapasite kısıtlamalar</span><span class="sxs-lookup"><span data-stu-id="c6617-184">Restrictions on Application Capacity</span></span>
<span data-ttu-id="c6617-185">Dikkate alınması gereken uygulama kapasite parametreleri bazı kısıtlamalar vardır.</span><span class="sxs-lookup"><span data-stu-id="c6617-185">There are several restrictions on Application Capacity parameters that must be respected.</span></span> <span data-ttu-id="c6617-186">Doğrulama hatası varsa herhangi bir değişiklik gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="c6617-186">If there are validation errors no changes take place.</span></span>

- <span data-ttu-id="c6617-187">Tüm tamsayı parametreleri negatif olmayan sayı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="c6617-187">All integer parameters must be non-negative numbers.</span></span>
- <span data-ttu-id="c6617-188">En az düğüm asla en fazla düğüm büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c6617-188">MinimumNodes must never be greater than MaximumNodes.</span></span>
- <span data-ttu-id="c6617-189">Ardından bir yük ölçümü için kapasiteler tanımlanmışsa, bu kurallara uymalıdır:</span><span class="sxs-lookup"><span data-stu-id="c6617-189">If capacities for a load metric are defined, then they must follow these rules:</span></span>
  - <span data-ttu-id="c6617-190">Düğüm ayırma kapasitesi en fazla düğüm kapasitesi büyük olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="c6617-190">Node Reservation Capacity must not be greater than Maximum Node Capacity.</span></span> <span data-ttu-id="c6617-191">Örneğin, hello düğümü tootwo birimlerdeki hello ölçüm "CPU" Merhaba kapasiteyi sınırlamak ve her düğümde tooreserve üç birimleri deneyin.</span><span class="sxs-lookup"><span data-stu-id="c6617-191">For example, you cannot limit hello capacity for hello metric “CPU” on hello node tootwo units and try tooreserve three units on each node.</span></span>
  - <span data-ttu-id="c6617-192">En fazla düğüm belirtilirse, en fazla düğüm ve en fazla düğüm kapasitesi hello ürün toplam uygulama kapasiteden büyük olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="c6617-192">If MaximumNodes is specified, then hello product of MaximumNodes and Maximum Node Capacity must not be greater than Total Application Capacity.</span></span> <span data-ttu-id="c6617-193">Örneğin, "CPU" tooeight ayarlanır yük ölçümü için en fazla düğüm kapasitesi hello varsayalım.</span><span class="sxs-lookup"><span data-stu-id="c6617-193">For example, let's say hello Maximum Node Capacity for load metric “CPU” is set tooeight.</span></span> <span data-ttu-id="c6617-194">Ayrıca hello en fazla düğüm too10 ayarladığınızı varsayalım.</span><span class="sxs-lookup"><span data-stu-id="c6617-194">Let's also say you set hello Maximum Nodes too10.</span></span> <span data-ttu-id="c6617-195">Bu durumda, toplam uygulama kapasitesinin Bu yük ölçüm için 80'den büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c6617-195">In this case, Total Application Capacity must be greater than 80 for this load metric.</span></span>

<span data-ttu-id="c6617-196">Merhaba kısıtlamaları, hem uygulama oluşturma ve güncelleştirme sırasında zorlanır.</span><span class="sxs-lookup"><span data-stu-id="c6617-196">hello restrictions are enforced both during application creation and updates.</span></span>

## <a name="how-not-toouse-application-capacity"></a><span data-ttu-id="c6617-197">Değil toouse nasıl uygulama kapasite</span><span class="sxs-lookup"><span data-stu-id="c6617-197">How not toouse Application Capacity</span></span>
- <span data-ttu-id="c6617-198">Toouse hello uygulama grubu özellikleri tooconstrain hello uygulama tooa çalışmayın _belirli_ alt düğümleri kümesi.</span><span class="sxs-lookup"><span data-stu-id="c6617-198">Do not try toouse hello Application Group features tooconstrain hello application tooa _specific_ subset of nodes.</span></span> <span data-ttu-id="c6617-199">Diğer bir deyişle, hello uygulamanın en fazla beş düğümlerinde çalıştığını belirtebilirsiniz, ancak hello kümedeki belirli hangi beş düğümü.</span><span class="sxs-lookup"><span data-stu-id="c6617-199">In other words, you can specify that hello application runs on at most five nodes, but not which specific five nodes in hello cluster.</span></span> <span data-ttu-id="c6617-200">Bir uygulama toospecific sınırlama düğümleri kısıtlamalarından Hizmetleri kullanarak elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="c6617-200">Constraining an application toospecific nodes can be achieved using placement constraints for services.</span></span>
- <span data-ttu-id="c6617-201">Aynı uygulama üzerinde yerleştirilir hello iki Hizmetleri'nden aynı düğümlerine hello toouse hello uygulama kapasite tooensure çalışmayın.</span><span class="sxs-lookup"><span data-stu-id="c6617-201">Do not try toouse hello Application Capacity tooensure that two services from hello same application are placed on hello same nodes.</span></span> <span data-ttu-id="c6617-202">Bunun yerine kullanın [benzeşim](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) veya [kısıtlamalarından](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).</span><span class="sxs-lookup"><span data-stu-id="c6617-202">Instead use [affinity](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) or [placement constraints](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c6617-203">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c6617-203">Next steps</span></span>
- <span data-ttu-id="c6617-204">Hizmetleri yapılandırma hakkında daha fazla bilgi için [hizmetleri yapılandırma hakkında bilgi edinin](service-fabric-cluster-resource-manager-configure-services.md)</span><span class="sxs-lookup"><span data-stu-id="c6617-204">For more information on configuring services, [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)</span></span>
- <span data-ttu-id="c6617-205">toofind hello Küme Kaynak Yöneticisi yönetir ve dengeleyen hello kümedeki yük hakkında hello makalesine üzerinde kullanıma [Yük Dengeleme](service-fabric-cluster-resource-manager-balancing.md)</span><span class="sxs-lookup"><span data-stu-id="c6617-205">toofind out about how hello Cluster Resource Manager manages and balances load in hello cluster, check out hello article on [balancing load](service-fabric-cluster-resource-manager-balancing.md)</span></span>
- <span data-ttu-id="c6617-206">Merhaba baştan başlatın ve [giriş toohello Service Fabric kümesi Kaynak Yöneticisi Al](service-fabric-cluster-resource-manager-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="c6617-206">Start from hello beginning and [get an Introduction toohello Service Fabric Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)</span></span>
- <span data-ttu-id="c6617-207">Ölçümleri genellikle nasıl çalıştığı hakkında daha fazla bilgi için okumaya devam [Service Fabric yük ölçümleri](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="c6617-207">For more information on how metrics work generally, read up on [Service Fabric Load Metrics](service-fabric-cluster-resource-manager-metrics.md)</span></span>
- <span data-ttu-id="c6617-208">Merhaba küme Resource Manager hello küme açıklamak için birçok seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="c6617-208">hello Cluster Resource Manager has many options for describing hello cluster.</span></span> <span data-ttu-id="c6617-209">toofind bunlarla ilgili daha fazla bilgi, bu makalede denetleyin [açıklayan bir Service Fabric kümesi](service-fabric-cluster-resource-manager-cluster-description.md)</span><span class="sxs-lookup"><span data-stu-id="c6617-209">toofind out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-max-nodes.png
[Image2]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-reserved-capacity.png
