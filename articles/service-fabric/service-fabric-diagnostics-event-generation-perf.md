---
title: Azure Service Fabric performans izleme | Microsoft Docs
description: "İzleme ve tanılama Azure Service Fabric kümeleri için performans sayaçları hakkında bilgi edinin."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 9d63148c182c705b6b49733c59ed8fdd13872d72
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="performance-metrics"></a><span data-ttu-id="64cad-103">Performans ölçümleri</span><span class="sxs-lookup"><span data-stu-id="64cad-103">Performance metrics</span></span>

<span data-ttu-id="64cad-104">Ölçümleri kümenizi ve bunun yanı sıra içinde çalışan uygulamaların performansını anlamak için toplanan.</span><span class="sxs-lookup"><span data-stu-id="64cad-104">Metrics should be collected to understand the performance of your cluster as well as the applications running in it.</span></span> <span data-ttu-id="64cad-105">Service Fabric kümeleri için aşağıdaki performans sayaçlarını toplama öneririz.</span><span class="sxs-lookup"><span data-stu-id="64cad-105">For Service Fabric clusters, we recommend collecting the following performance counters.</span></span>

## <a name="nodes"></a><span data-ttu-id="64cad-106">Düğümler</span><span class="sxs-lookup"><span data-stu-id="64cad-106">Nodes</span></span>

<span data-ttu-id="64cad-107">Kümenizdeki makineler için daha iyi her makinede yük anlamak ve uygun küme kararları ölçeklendirme yapmak için aşağıdaki performans sayaçlarını toplama göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="64cad-107">For the machines in your cluster, consider collecting the following performance counters to better understand the load on each machine and make appropriate cluster scaling decisions.</span></span>

| <span data-ttu-id="64cad-108">Sayacı kategorisi</span><span class="sxs-lookup"><span data-stu-id="64cad-108">Counter Category</span></span> | <span data-ttu-id="64cad-109">Sayaç adı</span><span class="sxs-lookup"><span data-stu-id="64cad-109">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="64cad-110">PhysicalDisk (her Disk için)</span><span class="sxs-lookup"><span data-stu-id="64cad-110">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="64cad-111">Ort.</span><span class="sxs-lookup"><span data-stu-id="64cad-111">Avg.</span></span> <span data-ttu-id="64cad-112">Disk okuma sırası uzunluğu</span><span class="sxs-lookup"><span data-stu-id="64cad-112">Disk Read Queue Length</span></span> |
| <span data-ttu-id="64cad-113">PhysicalDisk (her Disk için)</span><span class="sxs-lookup"><span data-stu-id="64cad-113">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="64cad-114">Ort.</span><span class="sxs-lookup"><span data-stu-id="64cad-114">Avg.</span></span> <span data-ttu-id="64cad-115">Disk yazma sırası uzunluğu</span><span class="sxs-lookup"><span data-stu-id="64cad-115">Disk Write Queue Length</span></span> |
| <span data-ttu-id="64cad-116">PhysicalDisk (her Disk için)</span><span class="sxs-lookup"><span data-stu-id="64cad-116">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="64cad-117">Ort.</span><span class="sxs-lookup"><span data-stu-id="64cad-117">Avg.</span></span> <span data-ttu-id="64cad-118">Disk sn/Okuma</span><span class="sxs-lookup"><span data-stu-id="64cad-118">Disk sec/Read</span></span> |
| <span data-ttu-id="64cad-119">PhysicalDisk (her Disk için)</span><span class="sxs-lookup"><span data-stu-id="64cad-119">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="64cad-120">Ort.</span><span class="sxs-lookup"><span data-stu-id="64cad-120">Avg.</span></span> <span data-ttu-id="64cad-121">Disk sn/yazma</span><span class="sxs-lookup"><span data-stu-id="64cad-121">Disk sec/Write</span></span> |
| <span data-ttu-id="64cad-122">PhysicalDisk (her Disk için)</span><span class="sxs-lookup"><span data-stu-id="64cad-122">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="64cad-123">Disk Okuma/sn</span><span class="sxs-lookup"><span data-stu-id="64cad-123">Disk Reads/sec</span></span> |
| <span data-ttu-id="64cad-124">PhysicalDisk (her Disk için)</span><span class="sxs-lookup"><span data-stu-id="64cad-124">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="64cad-125">Disk okuma bayt/sn</span><span class="sxs-lookup"><span data-stu-id="64cad-125">Disk Read Bytes/sec</span></span> |
| <span data-ttu-id="64cad-126">PhysicalDisk (her Disk için)</span><span class="sxs-lookup"><span data-stu-id="64cad-126">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="64cad-127">Disk Yazma/sn</span><span class="sxs-lookup"><span data-stu-id="64cad-127">Disk Writes/sec</span></span> |
| <span data-ttu-id="64cad-128">PhysicalDisk (her Disk için)</span><span class="sxs-lookup"><span data-stu-id="64cad-128">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="64cad-129">Disk Yazma Bayt/sn</span><span class="sxs-lookup"><span data-stu-id="64cad-129">Disk Write Bytes/sec</span></span> |
| <span data-ttu-id="64cad-130">Bellek</span><span class="sxs-lookup"><span data-stu-id="64cad-130">Memory</span></span> | <span data-ttu-id="64cad-131">Kullanılabilir MBayt</span><span class="sxs-lookup"><span data-stu-id="64cad-131">Available MBytes</span></span> |
| <span data-ttu-id="64cad-132">PagingFile</span><span class="sxs-lookup"><span data-stu-id="64cad-132">PagingFile</span></span> | <span data-ttu-id="64cad-133">% Kullanım</span><span class="sxs-lookup"><span data-stu-id="64cad-133">% Usage</span></span> |
| <span data-ttu-id="64cad-134">Process(Total)</span><span class="sxs-lookup"><span data-stu-id="64cad-134">Process(Total)</span></span> | <span data-ttu-id="64cad-135">% İşlemci zamanı</span><span class="sxs-lookup"><span data-stu-id="64cad-135">% Processor Time</span></span> |
| <span data-ttu-id="64cad-136">İşlem (her hizmeti)</span><span class="sxs-lookup"><span data-stu-id="64cad-136">Process (per service)</span></span> | <span data-ttu-id="64cad-137">% İşlemci zamanı</span><span class="sxs-lookup"><span data-stu-id="64cad-137">% Processor Time</span></span> |
| <span data-ttu-id="64cad-138">İşlem (her hizmeti)</span><span class="sxs-lookup"><span data-stu-id="64cad-138">Process (per service)</span></span> | <span data-ttu-id="64cad-139">İşlem kimliği</span><span class="sxs-lookup"><span data-stu-id="64cad-139">ID Process</span></span> |
| <span data-ttu-id="64cad-140">İşlem (her hizmeti)</span><span class="sxs-lookup"><span data-stu-id="64cad-140">Process (per service)</span></span> | <span data-ttu-id="64cad-141">Özel bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="64cad-141">Private Bytes</span></span> |
| <span data-ttu-id="64cad-142">İşlem (her hizmeti)</span><span class="sxs-lookup"><span data-stu-id="64cad-142">Process (per service)</span></span> | <span data-ttu-id="64cad-143">İş parçacığı sayısı</span><span class="sxs-lookup"><span data-stu-id="64cad-143">Thread Count</span></span> |
| <span data-ttu-id="64cad-144">İşlem (her hizmeti)</span><span class="sxs-lookup"><span data-stu-id="64cad-144">Process (per service)</span></span> | <span data-ttu-id="64cad-145">Sanal bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="64cad-145">Virtual Bytes</span></span> |
| <span data-ttu-id="64cad-146">İşlem (her hizmeti)</span><span class="sxs-lookup"><span data-stu-id="64cad-146">Process (per service)</span></span> | <span data-ttu-id="64cad-147">Çalışma kümesi</span><span class="sxs-lookup"><span data-stu-id="64cad-147">Working Set</span></span> |
| <span data-ttu-id="64cad-148">İşlem (her hizmeti)</span><span class="sxs-lookup"><span data-stu-id="64cad-148">Process (per service)</span></span> | <span data-ttu-id="64cad-149">Çalışma kümesi - özel</span><span class="sxs-lookup"><span data-stu-id="64cad-149">Working Set - Private</span></span> |

## <a name="net-applications-and-services"></a><span data-ttu-id="64cad-150">.NET uygulamaları ve Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="64cad-150">.NET applications and services</span></span>

<span data-ttu-id="64cad-151">.NET Hizmetleri kümenize dağıtıyorsanız aşağıdaki sayaçları toplayın.</span><span class="sxs-lookup"><span data-stu-id="64cad-151">Collect the following counters if you are deploying .NET services to your cluster.</span></span> 

| <span data-ttu-id="64cad-152">Sayacı kategorisi</span><span class="sxs-lookup"><span data-stu-id="64cad-152">Counter Category</span></span> | <span data-ttu-id="64cad-153">Sayaç adı</span><span class="sxs-lookup"><span data-stu-id="64cad-153">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="64cad-154">.NET CLR bellek (her hizmeti)</span><span class="sxs-lookup"><span data-stu-id="64cad-154">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="64cad-155">İşlem kimliği</span><span class="sxs-lookup"><span data-stu-id="64cad-155">Process ID</span></span> |
| <span data-ttu-id="64cad-156">.NET CLR bellek (her hizmeti)</span><span class="sxs-lookup"><span data-stu-id="64cad-156">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="64cad-157"># Toplam kaydedilmiş bayt</span><span class="sxs-lookup"><span data-stu-id="64cad-157"># Total committed Bytes</span></span> |
| <span data-ttu-id="64cad-158">.NET CLR bellek (her hizmeti)</span><span class="sxs-lookup"><span data-stu-id="64cad-158">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="64cad-159"># Toplam bayt ayrılmış</span><span class="sxs-lookup"><span data-stu-id="64cad-159"># Total reserved Bytes</span></span> |
| <span data-ttu-id="64cad-160">.NET CLR bellek (her hizmeti)</span><span class="sxs-lookup"><span data-stu-id="64cad-160">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="64cad-161"># Tüm yığınlardaki bayt</span><span class="sxs-lookup"><span data-stu-id="64cad-161"># Bytes in all Heaps</span></span> |
| <span data-ttu-id="64cad-162">.NET CLR bellek (her hizmeti)</span><span class="sxs-lookup"><span data-stu-id="64cad-162">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="64cad-163"># Gen 0 koleksiyonları</span><span class="sxs-lookup"><span data-stu-id="64cad-163"># Gen 0 Collections</span></span> |
| <span data-ttu-id="64cad-164">.NET CLR bellek (her hizmeti)</span><span class="sxs-lookup"><span data-stu-id="64cad-164">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="64cad-165"># Gen 1 koleksiyonları</span><span class="sxs-lookup"><span data-stu-id="64cad-165"># Gen 1 Collections</span></span> |
| <span data-ttu-id="64cad-166">.NET CLR bellek (her hizmeti)</span><span class="sxs-lookup"><span data-stu-id="64cad-166">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="64cad-167"># Gen 2 koleksiyonları</span><span class="sxs-lookup"><span data-stu-id="64cad-167"># Gen 2 Collections</span></span> |
| <span data-ttu-id="64cad-168">.NET CLR bellek (her hizmeti)</span><span class="sxs-lookup"><span data-stu-id="64cad-168">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="64cad-169">GC % zaman</span><span class="sxs-lookup"><span data-stu-id="64cad-169">% Time in GC</span></span> |

### <a name="service-fabrics-custom-performance-counters"></a><span data-ttu-id="64cad-170">Service Fabric'ın özel performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="64cad-170">Service Fabric's custom performance counters</span></span>

<span data-ttu-id="64cad-171">Service Fabric özel performans sayaçları önemli miktarda oluşturur.</span><span class="sxs-lookup"><span data-stu-id="64cad-171">Service Fabric generates a substantial amount of custom performance counters.</span></span> <span data-ttu-id="64cad-172">SDK yüklü değilse, Performans İzleyicisi uygulamanızda kapsamlı listesi Windows makinenizde görebilirsiniz (Başlat > Performans İzleyicisi).</span><span class="sxs-lookup"><span data-stu-id="64cad-172">If you have the SDK installed, you can see the comprehensive list on your Windows machine in your Performance Monitor application (Start > Performance Monitor).</span></span> 

<span data-ttu-id="64cad-173">Uygulamalarda Reliable Actors kullanıyorsanız, kümeniz için dağıtıyorsanız, gelen countes ekleme `Service Fabric Actor` ve `Service Fabric Actor Method` kategorileri (bkz [Service Fabric güvenilir aktörler tanılama](service-fabric-reliable-actors-diagnostics.md)).</span><span class="sxs-lookup"><span data-stu-id="64cad-173">In the applications you are deploying to your cluster, if you are using Reliable Actors, add countes from `Service Fabric Actor` and `Service Fabric Actor Method` categories (see [Service Fabric Reliable Actors Diagnostics](service-fabric-reliable-actors-diagnostics.md)).</span></span>

<span data-ttu-id="64cad-174">Güvenilir hizmetlerini kullanıyorsanız, benzer şekilde sahibiz `Service Fabric Service` ve `Service Fabric Service Method` toplamanız gerekir sayacı kategorileri sayaçları.</span><span class="sxs-lookup"><span data-stu-id="64cad-174">If you use Reliable Services, we similarly have `Service Fabric Service` and `Service Fabric Service Method` counter categories that you should collect counters from.</span></span> 

<span data-ttu-id="64cad-175">Güvenilir koleksiyonları kullanırsanız, eklemenizi öneririz `Avg. Transaction ms/Commit` gelen `Service Fabric Transactional Replicator` işlem ölçüm başına ortalama yürütme gecikmesi toplanacak.</span><span class="sxs-lookup"><span data-stu-id="64cad-175">If you use Reliable Collections, we recommend adding the `Avg. Transaction ms/Commit` from the `Service Fabric Transactional Replicator` to collect the average commit latency per transaction metric.</span></span>


## <a name="next-steps"></a><span data-ttu-id="64cad-176">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="64cad-176">Next steps</span></span>

* <span data-ttu-id="64cad-177">Daha fazla bilgi edinmek [olay oluşturma platform düzeyinde](service-fabric-diagnostics-event-generation-infra.md) Service Fabric içinde</span><span class="sxs-lookup"><span data-stu-id="64cad-177">Learn more about [event generation at the platform level](service-fabric-diagnostics-event-generation-infra.md) in Service Fabric</span></span>
* <span data-ttu-id="64cad-178">Aracılığıyla performans ölçümlerini derleme [Azure tanılama](service-fabric-diagnostics-event-aggregation-wad.md)</span><span class="sxs-lookup"><span data-stu-id="64cad-178">Collect performance metrics through [Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md)</span></span>
