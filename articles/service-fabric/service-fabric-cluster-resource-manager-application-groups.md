---
title: "Service Fabric kümesi Kaynak Yöneticisi - uygulama grupları | Microsoft Docs"
description: "Service Fabric kümesi Kaynak Yöneticisi'nde uygulama grubu işlevlerine genel bakış"
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
ms.openlocfilehash: 7fc61731c8df2a0c3dc5b77ae718b41c240f9233
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="introduction-to-application-groups"></a><span data-ttu-id="14671-103">Uygulama grupları giriş</span><span class="sxs-lookup"><span data-stu-id="14671-103">Introduction to Application Groups</span></span>
<span data-ttu-id="14671-104">Service Fabric'ın Küme Kaynağı Yöneticisi genellikle yük dengelemesini yaparak küme kaynaklarını yönetir (aracılığıyla temsil [ölçümleri](service-fabric-cluster-resource-manager-metrics.md)) kümesi boyunca eşit.</span><span class="sxs-lookup"><span data-stu-id="14671-104">Service Fabric's Cluster Resource Manager typically manages cluster resources by spreading the load (represented via [Metrics](service-fabric-cluster-resource-manager-metrics.md)) evenly throughout the cluster.</span></span> <span data-ttu-id="14671-105">Service Fabric yönetir ve kümesindeki düğümlerin kapasite bir bütün olarak [kapasite](service-fabric-cluster-resource-manager-cluster-description.md).</span><span class="sxs-lookup"><span data-stu-id="14671-105">Service Fabric manages the capacity of the nodes in the cluster and the cluster as a whole via [capacity](service-fabric-cluster-resource-manager-cluster-description.md).</span></span> <span data-ttu-id="14671-106">Ölçümleri ve kapasite birçok iş yükü, ancak bazen ek gereksinimleri Getir yoğun olarak kullanılır farklı hizmet doku uygulama örnekleri desenleri harika çalışır.</span><span class="sxs-lookup"><span data-stu-id="14671-106">Metrics and capacity work great for many workloads, but patterns that make heavy use of different Service Fabric Application Instances sometimes bring in additional requirements.</span></span> <span data-ttu-id="14671-107">Örneğin, isteyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="14671-107">For example you may want to:</span></span>

- <span data-ttu-id="14671-108">Yedek kümedeki düğümlere bazı kapasite bazı Adlandırılmış uygulama örneği içindeki hizmetler için</span><span class="sxs-lookup"><span data-stu-id="14671-108">Reserve some capacity on the nodes in the cluster for the services within some named application instance</span></span>
- <span data-ttu-id="14671-109">(Bunları tüm küme yaymak) yerine adlandırılmış uygulama örneği içindeki hizmetler üzerinde çalışan düğümleri toplam sayısını sınırla</span><span class="sxs-lookup"><span data-stu-id="14671-109">Limit the total number of nodes that the services within a named application instance run on (instead of spreading them out over the entire cluster)</span></span>
- <span data-ttu-id="14671-110">Örneğindeki adlandırılmış uygulama kendisini hizmetlerin veya Hizmetleri içindeki toplam kaynak tüketimini sınırlamak için kapasiteleri tanımlayın</span><span class="sxs-lookup"><span data-stu-id="14671-110">Define capacities on the named application instance itself to limit the number of services or total resource consumption of the services inside it</span></span>

<span data-ttu-id="14671-111">Bu gereksinimleri karşılamak için Service Fabric kümesi Kaynak Yöneticisi uygulama grupları adlı bir özelliği destekler.</span><span class="sxs-lookup"><span data-stu-id="14671-111">To meet these requirements, the Service Fabric Cluster Resource Manager supports a feature called Application Groups.</span></span>

## <a name="limiting-the-maximum-number-of-nodes"></a><span data-ttu-id="14671-112">En fazla düğüm sayısını sınırlandırma</span><span class="sxs-lookup"><span data-stu-id="14671-112">Limiting the maximum number of nodes</span></span>
<span data-ttu-id="14671-113">Uygulama örneğini bir belirli en fazla düğüm sayısını için sınırlı olması gereken basit kullanım uygulama kapasite durumdur.</span><span class="sxs-lookup"><span data-stu-id="14671-113">The simplest use case for Application capacity is when an application instance needs to be limited to a certain maximum number of nodes.</span></span> <span data-ttu-id="14671-114">Bu uygulama örneği makine kümesi sayısı üzerine içindeki tüm hizmetler birleştirir.</span><span class="sxs-lookup"><span data-stu-id="14671-114">This consolidates all services within that application instance onto a set number of machines.</span></span> <span data-ttu-id="14671-115">Birleştirme, tahmin etmek ya da bu adlandırılmış uygulama örneği içindeki hizmetler tarafından fiziksel kaynak kullanımını cap çalıştığınız yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="14671-115">Consolidation is useful when you're trying to predict or cap physical resource use by the services within that named application instance.</span></span> 

<span data-ttu-id="14671-116">Aşağıdaki resimde bir uygulama örneği ile ve tanımlanan düğüm sayısı üst sınırı olmadan gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="14671-116">The following image shows an application instance with and without a maximum number of nodes defined:</span></span>

<span data-ttu-id="14671-117"><center>
![Uygulama örneği en fazla düğüm sayısını tanımlama][Image1]
</center></span><span class="sxs-lookup"><span data-stu-id="14671-117"><center>
![Application Instance Defining Maximum Number of Nodes][Image1]
</center></span></span>

<span data-ttu-id="14671-118">Sol örnekte, uygulama tanımlı düğüm sayısı üst sınırı yok ve üç hizmeti vardır.</span><span class="sxs-lookup"><span data-stu-id="14671-118">In the left example, the application doesn’t have a maximum number of nodes defined, and it has three services.</span></span> <span data-ttu-id="14671-119">Küme Kaynak Yöneticisi'ni tüm çoğaltmaları (varsayılan davranış) kümedeki en iyi dengeyi elde etmek için altı kullanılabilir düğümleri arasında yayılır.</span><span class="sxs-lookup"><span data-stu-id="14671-119">The Cluster Resource Manager has spread out all replicas across six available nodes to achieve the best balance in the cluster (the default behavior).</span></span> <span data-ttu-id="14671-120">Şu örnekte, üç düğümlerine sınırlı aynı uygulama bakın.</span><span class="sxs-lookup"><span data-stu-id="14671-120">In the right example, we see the same application limited to three nodes.</span></span>

<span data-ttu-id="14671-121">Bu davranışı denetler parametre en fazla düğüm adı verilir.</span><span class="sxs-lookup"><span data-stu-id="14671-121">The parameter that controls this behavior is called MaximumNodes.</span></span> <span data-ttu-id="14671-122">Bu parametre uygulama oluşturma sırasında ayarlayın veya zaten çalışan bir uygulama örneği için güncelleştirilmiştir.</span><span class="sxs-lookup"><span data-stu-id="14671-122">This parameter can be set during application creation, or updated for an application instance that was already running.</span></span>

<span data-ttu-id="14671-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="14671-123">Powershell</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MaximumNodes 3
Update-ServiceFabricApplication –Name fabric:/AppName –MaximumNodes 5
```

<span data-ttu-id="14671-124">C#</span><span class="sxs-lookup"><span data-stu-id="14671-124">C#</span></span>

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

<span data-ttu-id="14671-125">Düğümleri kümesi içinde Küme Kaynak Yöneticisi'ni hangi hizmet nesnelerin araya yerleştirilen veya hangi düğümlerin alışmanız garanti etmez.</span><span class="sxs-lookup"><span data-stu-id="14671-125">Within the set of nodes, the Cluster Resource Manager doesn't guarantee which service objects get placed together or which nodes get used.</span></span>

## <a name="application-metrics-load-and-capacity"></a><span data-ttu-id="14671-126">Uygulama ölçümleri, yükü ve kapasite</span><span class="sxs-lookup"><span data-stu-id="14671-126">Application Metrics, Load, and Capacity</span></span>
<span data-ttu-id="14671-127">Uygulama grupları verilen adlandırılmış uygulama örneği ve bu ölçümleri için o uygulama örneğinin kapasitesi ile ilişkili ölçümleri tanımlamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="14671-127">Application Groups also allow you to define metrics associated with a given named application instance, and that application instance's capacity for those metrics.</span></span> <span data-ttu-id="14671-128">Uygulama ölçümleri, izlemek, ayırmak ve Hizmetleri, uygulama örneği içinde kaynak tüketimini sınırlamak izin verir.</span><span class="sxs-lookup"><span data-stu-id="14671-128">Application metrics allow you to track, reserve, and limit the resource consumption of the services inside that application instance.</span></span>

<span data-ttu-id="14671-129">Her uygulama ölçümü için ayarlanabilir iki değer vardır:</span><span class="sxs-lookup"><span data-stu-id="14671-129">For each application metric, there are two values that can be set:</span></span>

- <span data-ttu-id="14671-130">**Toplam uygulama kapasitesinin** – Bu ayar uygulama için belirli bir ölçüm toplam kapasitesini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="14671-130">**Total Application Capacity** – This setting represents the total capacity of the application for a particular metric.</span></span> <span data-ttu-id="14671-131">Küme Kaynak Yöneticisi'ni yeni hizmetlerin bu değeri aşacak toplam yük neden olacağından bu uygulama örneği içinde oluşturulmasına izin vermez.</span><span class="sxs-lookup"><span data-stu-id="14671-131">The Cluster Resource Manager disallows the creation of any new services within this application instance that would cause total load to exceed this value.</span></span> <span data-ttu-id="14671-132">Örneğin, uygulama örneği 10 kapasitesine sahip ve beş yükünü zaten varsayalım.</span><span class="sxs-lookup"><span data-stu-id="14671-132">For example, let's say the application instance had a capacity of 10 and already had load of five.</span></span> <span data-ttu-id="14671-133">Bir hizmet oluşturma 10 toplam varsayılan yükü ile izin verilmeyen.</span><span class="sxs-lookup"><span data-stu-id="14671-133">The creation of a service with a total default load of 10 would be disallowed.</span></span>
- <span data-ttu-id="14671-134">**En fazla düğüm kapasitesi** – Bu ayar, tek bir düğümünde uygulama için en fazla toplam yükleme belirtir.</span><span class="sxs-lookup"><span data-stu-id="14671-134">**Maximum Node Capacity** – This setting specifies the maximum total load for the application on a single node.</span></span> <span data-ttu-id="14671-135">Yük bu kapasite kalırsa, yükü azaldıktan Küme Kaynak Yöneticisi'ni çoğaltmaları diğer düğümlere taşır.</span><span class="sxs-lookup"><span data-stu-id="14671-135">If load goes over this capacity, the Cluster Resource Manager moves replicas to other nodes so that the load decreases.</span></span>


<span data-ttu-id="14671-136">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="14671-136">Powershell:</span></span>

``` posh
New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -Metrics @("MetricName:Metric1,MaximumNodeCapacity:100,MaximumApplicationCapacity:1000")
```

<span data-ttu-id="14671-137">C# ' TA:</span><span class="sxs-lookup"><span data-stu-id="14671-137">C#:</span></span>

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

## <a name="reserving-capacity"></a><span data-ttu-id="14671-138">Kapasite ayırma</span><span class="sxs-lookup"><span data-stu-id="14671-138">Reserving Capacity</span></span>
<span data-ttu-id="14671-139">Uygulama grupları için başka bir yaygın kullanım kümedeki kaynaklar için belirli uygulama örneği ayrıldığından emin olmaktır.</span><span class="sxs-lookup"><span data-stu-id="14671-139">Another common use for application groups is to ensure that resources within the cluster are reserved for a given application instance.</span></span> <span data-ttu-id="14671-140">Uygulama örneği oluşturulduğunda, alan her zaman ayrılır.</span><span class="sxs-lookup"><span data-stu-id="14671-140">The space is always reserved when the application instance is created.</span></span>

<span data-ttu-id="14671-141">Bile uygulama hemen gerçekleştiğinden için kümedeki alanı ayırma:</span><span class="sxs-lookup"><span data-stu-id="14671-141">Reserving space in the cluster for the application happens immediately even when:</span></span>
- <span data-ttu-id="14671-142">Uygulama örneği oluşturulur ancak hizmetlerin içindeki henüz yok</span><span class="sxs-lookup"><span data-stu-id="14671-142">the application instance is created but doesn't have any services within it yet</span></span>
- <span data-ttu-id="14671-143">Uygulama örneği değişiklikleri her zaman içindeki Hizmetler sayısı</span><span class="sxs-lookup"><span data-stu-id="14671-143">the number of services within the application instance changes every time</span></span> 
- <span data-ttu-id="14671-144">Hizmetler var, ancak kaynak tüketmeye değil</span><span class="sxs-lookup"><span data-stu-id="14671-144">the services exist but aren't consuming the resources</span></span> 

<span data-ttu-id="14671-145">İki ek parametreler belirtmek uygulama örneğini gerektirir kaynaklarını ayırma: *düğüm* ve *NodeReservationCapacity*</span><span class="sxs-lookup"><span data-stu-id="14671-145">Reserving resources for an application instance requires specifying two additional parameters: *MinimumNodes* and *NodeReservationCapacity*</span></span>

- <span data-ttu-id="14671-146">**En az düğüm** -Uygulama örneğinin çalışması gereken düğüm sayısı alt sınırı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="14671-146">**MinimumNodes** - Defines the minimum number of nodes that the application instance should run on.</span></span>  
- <span data-ttu-id="14671-147">**NodeReservationCapacity** -bu uygulama için ölçüm başına ayardır.</span><span class="sxs-lookup"><span data-stu-id="14671-147">**NodeReservationCapacity** - This setting is per metric for the application.</span></span> <span data-ttu-id="14671-148">Değer herhangi bir düğümde uygulama için ayrılmış, ölçüm miktarıdır. Burada, o uygulama hizmetlerini çalıştırmak.</span><span class="sxs-lookup"><span data-stu-id="14671-148">The value is the amount of that metric reserved for the application on any node where that the services in that application run.</span></span>

<span data-ttu-id="14671-149">Birleştirme **düğüm** ve **NodeReservationCapacity** küme içindeki uygulama için en düşük yük ayırma güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="14671-149">Combining **MinimumNodes** and **NodeReservationCapacity** guarantees a minimum load reservation for the application within the cluster.</span></span> <span data-ttu-id="14671-150">Kalan kapasite kümedeki toplam ayırma daha az var. gerekli uygulamanın oluşturma başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="14671-150">If there's less remaining capacity in the cluster than the total reservation required, creation of the application fails.</span></span> 

<span data-ttu-id="14671-151">Kapasite ayırma bir örneğe bakalım:</span><span class="sxs-lookup"><span data-stu-id="14671-151">Let's look at an example of capacity reservation:</span></span>

<span data-ttu-id="14671-152"><center>
![Uygulama örnekleri ayrılmış Kapasite tanımlama][Image2]
</center></span><span class="sxs-lookup"><span data-stu-id="14671-152"><center>
![Application Instances Defining Reserved Capacity][Image2]
</center></span></span>

<span data-ttu-id="14671-153">Sol örnekte, uygulamaları herhangi uygulama tanımlı kapasiteye sahip değil.</span><span class="sxs-lookup"><span data-stu-id="14671-153">In the left example, applications do not have any Application Capacity defined.</span></span> <span data-ttu-id="14671-154">Küme Kaynak Yöneticisi'ni normal kurallarına göre her şeyi dengeler.</span><span class="sxs-lookup"><span data-stu-id="14671-154">The Cluster Resource Manager balances everything according to normal rules.</span></span>

<span data-ttu-id="14671-155">Sağdaki örnekte Application1 aşağıdaki ayarlarla oluşturuldu varsayalım:</span><span class="sxs-lookup"><span data-stu-id="14671-155">In the example on the right, let's say that Application1 was created with the following settings:</span></span>

- <span data-ttu-id="14671-156">İki düğüm ayarlama</span><span class="sxs-lookup"><span data-stu-id="14671-156">MinimumNodes set to two</span></span>
- <span data-ttu-id="14671-157">Bir uygulama ile tanımlanmış ölçümü</span><span class="sxs-lookup"><span data-stu-id="14671-157">An application Metric defined with</span></span>
  - <span data-ttu-id="14671-158">20 NodeReservationCapacity</span><span class="sxs-lookup"><span data-stu-id="14671-158">NodeReservationCapacity of 20</span></span>

<span data-ttu-id="14671-159">PowerShell</span><span class="sxs-lookup"><span data-stu-id="14671-159">Powershell</span></span>

 ``` posh
 New-ServiceFabricApplication -ApplicationName fabric:/AppName -ApplicationTypeName AppType1 -ApplicationTypeVersion 1.0.0.0 -MinimumNodes 2 -Metrics @("MetricName:Metric1,NodeReservationCapacity:20")
 ```

<span data-ttu-id="14671-160">C#</span><span class="sxs-lookup"><span data-stu-id="14671-160">C#</span></span>

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

<span data-ttu-id="14671-161">Service Fabric Application1 için iki düğüm üzerinde kapasite ayırır ve Hizmetleri Uygulama2 dizinlerini olsa bile herhangi bir yük tarafından Application1 içinde Hizmetleri zaman mı tüketiliyor kapasiteyi kullanmasına izin vermez.</span><span class="sxs-lookup"><span data-stu-id="14671-161">Service Fabric reserves capacity on two nodes for Application1, and doesn't allow services from Application2 to consume that capacity even if there are no load is being consumed by the services inside Application1 at the time.</span></span> <span data-ttu-id="14671-162">Bu ayrılmış uygulama kapasite tüketilen ve o düğümde ve kümedeki kalan kapasite karşı sayılarını değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="14671-162">This reserved application capacity is considered consumed  and counts against the remaining capacity on that node and within the cluster.</span></span>  <span data-ttu-id="14671-163">Ancak, yalnızca en az bir hizmet nesnesi üzerinde yerleştirildiğinde ayrılmış tüketim belirli bir düğümün kapasiteden çıkarılır ayırma kalan küme kapasiteden hemen çıkarılır.</span><span class="sxs-lookup"><span data-stu-id="14671-163">The reservation is deducted from the remaining cluster capacity immediately, however the reserved consumption is deducted from the capacity of a specific node only when at least one service object is placed on it.</span></span> <span data-ttu-id="14671-164">Kaynaklar yalnızca gerekli olduğunda düğümlerinde ayrılmış bu daha sonra bu ayırma esneklik ve daha iyi kaynak kullanımı için sağlar.</span><span class="sxs-lookup"><span data-stu-id="14671-164">This later reservation allows for flexibility and better resource utilization since resources are only reserved on nodes when needed.</span></span>

## <a name="obtaining-the-application-load-information"></a><span data-ttu-id="14671-165">Uygulama yükleme bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="14671-165">Obtaining the application load information</span></span>
<span data-ttu-id="14671-166">Her uygulama için bir veya daha fazla ölçümleri hizmetlerinin çoğaltmaları tarafından bildirilen toplam yükleme hakkında bilgi edinmek için tanımlanan bir uygulama kapasitesine sahiptir.</span><span class="sxs-lookup"><span data-stu-id="14671-166">For each application that has an Application Capacity defined for one or more metrics you can obtain the information about the aggregate load reported by replicas of its services.</span></span>

<span data-ttu-id="14671-167">PowerShell:</span><span class="sxs-lookup"><span data-stu-id="14671-167">Powershell:</span></span>

``` posh
Get-ServiceFabricApplicationLoad –ApplicationName fabric:/MyApplication1
```

<span data-ttu-id="14671-168">C#</span><span class="sxs-lookup"><span data-stu-id="14671-168">C#</span></span>

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

<span data-ttu-id="14671-169">ApplicationLoad sorgu uygulama için belirtilen uygulama kapasite hakkındaki temel bilgileri döndürür.</span><span class="sxs-lookup"><span data-stu-id="14671-169">The ApplicationLoad query returns the basic information about Application Capacity that was specified for the application.</span></span> <span data-ttu-id="14671-170">Bu bilgiler, Minimum düğümleri ve en fazla düğüm bilgileri ve uygulama şu anda kullandığı numarasını içerir.</span><span class="sxs-lookup"><span data-stu-id="14671-170">This information includes the Minimum Nodes and Maximum Nodes info, and the number that the application is currently occupying.</span></span> <span data-ttu-id="14671-171">Ayrıca her uygulamayı yük ölçüm hakkında bilgi içerir dahil olmak üzere:</span><span class="sxs-lookup"><span data-stu-id="14671-171">It also includes information about each application load metric, including:</span></span>

* <span data-ttu-id="14671-172">Ölçüm adı: Ölçüm adı.</span><span class="sxs-lookup"><span data-stu-id="14671-172">Metric Name: Name of the metric.</span></span>
* <span data-ttu-id="14671-173">Ayırma kapasitesi: kümede bu uygulama için ayrılmış küme kapasitesi.</span><span class="sxs-lookup"><span data-stu-id="14671-173">Reservation Capacity: Cluster Capacity that is reserved in the cluster for this Application.</span></span>
* <span data-ttu-id="14671-174">Uygulama yük: Bu uygulamanın alt çoğaltmalarının toplam yük.</span><span class="sxs-lookup"><span data-stu-id="14671-174">Application Load: Total Load of this Application’s child replicas.</span></span>
* <span data-ttu-id="14671-175">Uygulama kapasitesi: İzin verilen en yüksek uygulama yük değeri.</span><span class="sxs-lookup"><span data-stu-id="14671-175">Application Capacity: Maximum permitted value of Application Load.</span></span>

## <a name="removing-application-capacity"></a><span data-ttu-id="14671-176">Uygulama kapasite kaldırma</span><span class="sxs-lookup"><span data-stu-id="14671-176">Removing Application Capacity</span></span>
<span data-ttu-id="14671-177">Bir uygulama için uygulama kapasite parametreleri ayarlandıktan sonra güncelleştirme uygulama API'leri veya PowerShell cmdlet'leri kullanılarak kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="14671-177">Once the Application Capacity parameters are set for an application, they can be removed using Update Application APIs or PowerShell cmdlets.</span></span> <span data-ttu-id="14671-178">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="14671-178">For example:</span></span>

``` posh
Update-ServiceFabricApplication –Name fabric:/MyApplication1 –RemoveApplicationCapacity

```

<span data-ttu-id="14671-179">Bu komut tüm uygulama kapasite yönetim parametreleri uygulama örneğinden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="14671-179">This command removes all Application capacity management parameters from the application instance.</span></span> <span data-ttu-id="14671-180">Bu düğüm, en fazla düğüm ve uygulamanın ölçümleri varsa içerir.</span><span class="sxs-lookup"><span data-stu-id="14671-180">This includes MinimumNodes, MaximumNodes, and the Application's metrics, if any.</span></span> <span data-ttu-id="14671-181">Komutun etkisini hemen uygulanır.</span><span class="sxs-lookup"><span data-stu-id="14671-181">The effect of the command is immediate.</span></span> <span data-ttu-id="14671-182">Bu komut tamamlandıktan sonra Küme Kaynak Yöneticisi'ni varsayılan davranışı uygulamaları yönetmek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="14671-182">After this command completes, the Cluster Resource Manager uses the default behavior for managing applications.</span></span> <span data-ttu-id="14671-183">Uygulama kapasite parametreleri belirtilebilir yeniden aracılığıyla `Update-ServiceFabricApplication` / `System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.</span><span class="sxs-lookup"><span data-stu-id="14671-183">Application Capacity parameters can be specified again via `Update-ServiceFabricApplication`/`System.Fabric.FabricClient.ApplicationManagementClient.UpdateApplicationAsync()`.</span></span>

### <a name="restrictions-on-application-capacity"></a><span data-ttu-id="14671-184">Uygulama kapasite kısıtlamalar</span><span class="sxs-lookup"><span data-stu-id="14671-184">Restrictions on Application Capacity</span></span>
<span data-ttu-id="14671-185">Dikkate alınması gereken uygulama kapasite parametreleri bazı kısıtlamalar vardır.</span><span class="sxs-lookup"><span data-stu-id="14671-185">There are several restrictions on Application Capacity parameters that must be respected.</span></span> <span data-ttu-id="14671-186">Doğrulama hatası varsa herhangi bir değişiklik gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="14671-186">If there are validation errors no changes take place.</span></span>

- <span data-ttu-id="14671-187">Tüm tamsayı parametreleri negatif olmayan sayı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="14671-187">All integer parameters must be non-negative numbers.</span></span>
- <span data-ttu-id="14671-188">En az düğüm asla en fazla düğüm büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="14671-188">MinimumNodes must never be greater than MaximumNodes.</span></span>
- <span data-ttu-id="14671-189">Ardından bir yük ölçümü için kapasiteler tanımlanmışsa, bu kurallara uymalıdır:</span><span class="sxs-lookup"><span data-stu-id="14671-189">If capacities for a load metric are defined, then they must follow these rules:</span></span>
  - <span data-ttu-id="14671-190">Düğüm ayırma kapasitesi en fazla düğüm kapasitesi büyük olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="14671-190">Node Reservation Capacity must not be greater than Maximum Node Capacity.</span></span> <span data-ttu-id="14671-191">Örneğin, iki birimlerine düğümde "CPU" ölçüm için kapasite sınırlamak ve üç birimleri her düğümde ayrılacak deneyin.</span><span class="sxs-lookup"><span data-stu-id="14671-191">For example, you cannot limit the capacity for the metric “CPU” on the node to two units and try to reserve three units on each node.</span></span>
  - <span data-ttu-id="14671-192">En fazla düğüm belirtilirse, en fazla düğüm ve en fazla düğüm kapasitesi çarpımı toplam uygulama kapasiteden büyük olmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="14671-192">If MaximumNodes is specified, then the product of MaximumNodes and Maximum Node Capacity must not be greater than Total Application Capacity.</span></span> <span data-ttu-id="14671-193">Örneğin, "CPU" sekiz için ayarlanmış yük ölçümü için en fazla düğüm kapasitesi varsayalım.</span><span class="sxs-lookup"><span data-stu-id="14671-193">For example, let's say the Maximum Node Capacity for load metric “CPU” is set to eight.</span></span> <span data-ttu-id="14671-194">Ayrıca en fazla düğüm sayısı 10'a ayarladığınızı varsayalım.</span><span class="sxs-lookup"><span data-stu-id="14671-194">Let's also say you set the Maximum Nodes to 10.</span></span> <span data-ttu-id="14671-195">Bu durumda, toplam uygulama kapasitesinin Bu yük ölçüm için 80'den büyük olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="14671-195">In this case, Total Application Capacity must be greater than 80 for this load metric.</span></span>

<span data-ttu-id="14671-196">Kısıtlamaları, hem uygulama oluşturma ve güncelleştirme sırasında zorlanır.</span><span class="sxs-lookup"><span data-stu-id="14671-196">The restrictions are enforced both during application creation and updates.</span></span>

## <a name="how-not-to-use-application-capacity"></a><span data-ttu-id="14671-197">Uygulama kapasite kullanma değil</span><span class="sxs-lookup"><span data-stu-id="14671-197">How not to use Application Capacity</span></span>
- <span data-ttu-id="14671-198">Uygulamaya sınırlamak için uygulama grubu özelliklerini kullanmaya çalışmayın bir _belirli_ alt düğümleri kümesi.</span><span class="sxs-lookup"><span data-stu-id="14671-198">Do not try to use the Application Group features to constrain the application to a _specific_ subset of nodes.</span></span> <span data-ttu-id="14671-199">Diğer bir deyişle, uygulamanın en fazla beş düğümlerinde çalıştığını belirtebilirsiniz, ancak küme içindeki belirli hangi beş düğümü.</span><span class="sxs-lookup"><span data-stu-id="14671-199">In other words, you can specify that the application runs on at most five nodes, but not which specific five nodes in the cluster.</span></span> <span data-ttu-id="14671-200">Belirli düğümler uygulamaya kısıtlamadır yerleşim kısıtlaması Hizmetleri kullanarak elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="14671-200">Constraining an application to specific nodes can be achieved using placement constraints for services.</span></span>
- <span data-ttu-id="14671-201">İki Hizmetleri'nden aynı uygulama aynı düğümlerinde yerleştirilir emin olmak için uygulama kapasite kullanmaya çalışmayın.</span><span class="sxs-lookup"><span data-stu-id="14671-201">Do not try to use the Application Capacity to ensure that two services from the same application are placed on the same nodes.</span></span> <span data-ttu-id="14671-202">Bunun yerine kullanın [benzeşim](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) veya [kısıtlamalarından](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).</span><span class="sxs-lookup"><span data-stu-id="14671-202">Instead use [affinity](service-fabric-cluster-resource-manager-advanced-placement-rules-affinity.md) or [placement constraints](service-fabric-cluster-resource-manager-cluster-description.md#node-properties-and-placement-constraints).</span></span>

## <a name="next-steps"></a><span data-ttu-id="14671-203">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="14671-203">Next steps</span></span>
- <span data-ttu-id="14671-204">Hizmetleri yapılandırma hakkında daha fazla bilgi için [hizmetleri yapılandırma hakkında bilgi edinin](service-fabric-cluster-resource-manager-configure-services.md)</span><span class="sxs-lookup"><span data-stu-id="14671-204">For more information on configuring services, [Learn about configuring Services](service-fabric-cluster-resource-manager-configure-services.md)</span></span>
- <span data-ttu-id="14671-205">Küme Kaynak Yöneticisi'ni yönetir ve yük devretme kümesinde dengeleyen hakkında bilgi almak için makalesine kontrol [Yük Dengeleme](service-fabric-cluster-resource-manager-balancing.md)</span><span class="sxs-lookup"><span data-stu-id="14671-205">To find out about how the Cluster Resource Manager manages and balances load in the cluster, check out the article on [balancing load](service-fabric-cluster-resource-manager-balancing.md)</span></span>
- <span data-ttu-id="14671-206">En baştan başlatın ve [bir giriş için Service Fabric kümesi Resource Manager Al](service-fabric-cluster-resource-manager-introduction.md)</span><span class="sxs-lookup"><span data-stu-id="14671-206">Start from the beginning and [get an Introduction to the Service Fabric Cluster Resource Manager](service-fabric-cluster-resource-manager-introduction.md)</span></span>
- <span data-ttu-id="14671-207">Ölçümleri genellikle nasıl çalıştığı hakkında daha fazla bilgi için okumaya devam [Service Fabric yük ölçümleri](service-fabric-cluster-resource-manager-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="14671-207">For more information on how metrics work generally, read up on [Service Fabric Load Metrics](service-fabric-cluster-resource-manager-metrics.md)</span></span>
- <span data-ttu-id="14671-208">Küme Kaynak Yöneticisi'ni küme açıklamak için birçok seçeneğiniz vardır.</span><span class="sxs-lookup"><span data-stu-id="14671-208">The Cluster Resource Manager has many options for describing the cluster.</span></span> <span data-ttu-id="14671-209">Bunları hakkında daha fazla bilgi için bu makalede kontrol [açıklayan bir Service Fabric kümesi](service-fabric-cluster-resource-manager-cluster-description.md)</span><span class="sxs-lookup"><span data-stu-id="14671-209">To find out more about them, check out this article on [describing a Service Fabric cluster](service-fabric-cluster-resource-manager-cluster-description.md)</span></span>

[Image1]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-max-nodes.png
[Image2]:./media/service-fabric-cluster-resource-manager-application-groups/application-groups-reserved-capacity.png
