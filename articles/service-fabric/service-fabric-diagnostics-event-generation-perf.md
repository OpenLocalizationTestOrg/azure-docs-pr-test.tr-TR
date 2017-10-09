---
title: "aaaAzure Service Fabric performansını izleme | Microsoft Docs"
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
ms.openlocfilehash: 54d4c62b7250a1f70b0898ba07ae5a37716f4cf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-metrics"></a><span data-ttu-id="8d23a-103">Performans ölçümleri</span><span class="sxs-lookup"><span data-stu-id="8d23a-103">Performance metrics</span></span>

<span data-ttu-id="8d23a-104">Ölçümleri toplanan toounderstand hello performans kümenizin yanı sıra içinde çalışan hello uygulamaları gerekir.</span><span class="sxs-lookup"><span data-stu-id="8d23a-104">Metrics should be collected toounderstand hello performance of your cluster as well as hello applications running in it.</span></span> <span data-ttu-id="8d23a-105">Service Fabric kümeleri için performans sayaçlarını izleyerek hello toplama öneririz.</span><span class="sxs-lookup"><span data-stu-id="8d23a-105">For Service Fabric clusters, we recommend collecting hello following performance counters.</span></span>

## <a name="nodes"></a><span data-ttu-id="8d23a-106">Düğümler</span><span class="sxs-lookup"><span data-stu-id="8d23a-106">Nodes</span></span>

<span data-ttu-id="8d23a-107">Kümenizdeki Hello makineler için aşağıdaki performans sayaçları toobetter anlamak her makinede yük hello ve kararları ölçeklendirme uygun küme olun hello toplama göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="8d23a-107">For hello machines in your cluster, consider collecting hello following performance counters toobetter understand hello load on each machine and make appropriate cluster scaling decisions.</span></span>

| <span data-ttu-id="8d23a-108">Sayacı kategorisi</span><span class="sxs-lookup"><span data-stu-id="8d23a-108">Counter Category</span></span> | <span data-ttu-id="8d23a-109">Sayaç adı</span><span class="sxs-lookup"><span data-stu-id="8d23a-109">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="8d23a-110">PhysicalDisk (her Disk için)</span><span class="sxs-lookup"><span data-stu-id="8d23a-110">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="8d23a-111">Ort. Disk okuma sırası uzunluğu</span><span class="sxs-lookup"><span data-stu-id="8d23a-111">Avg. Disk Read Queue Length</span></span> |
| <span data-ttu-id="8d23a-112">PhysicalDisk (her Disk için)</span><span class="sxs-lookup"><span data-stu-id="8d23a-112">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="8d23a-113">Ort. Disk yazma sırası uzunluğu</span><span class="sxs-lookup"><span data-stu-id="8d23a-113">Avg. Disk Write Queue Length</span></span> |
| <span data-ttu-id="8d23a-114">PhysicalDisk (her Disk için)</span><span class="sxs-lookup"><span data-stu-id="8d23a-114">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="8d23a-115">Ort. Disk sn/Okuma</span><span class="sxs-lookup"><span data-stu-id="8d23a-115">Avg. Disk sec/Read</span></span> |
| <span data-ttu-id="8d23a-116">PhysicalDisk (her Disk için)</span><span class="sxs-lookup"><span data-stu-id="8d23a-116">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="8d23a-117">Ort. Disk sn/yazma</span><span class="sxs-lookup"><span data-stu-id="8d23a-117">Avg. Disk sec/Write</span></span> |
| <span data-ttu-id="8d23a-118">PhysicalDisk (her Disk için)</span><span class="sxs-lookup"><span data-stu-id="8d23a-118">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="8d23a-119">Disk Okuma/sn</span><span class="sxs-lookup"><span data-stu-id="8d23a-119">Disk Reads/sec</span></span> |
| <span data-ttu-id="8d23a-120">PhysicalDisk (her Disk için)</span><span class="sxs-lookup"><span data-stu-id="8d23a-120">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="8d23a-121">Disk okuma bayt/sn</span><span class="sxs-lookup"><span data-stu-id="8d23a-121">Disk Read Bytes/sec</span></span> |
| <span data-ttu-id="8d23a-122">PhysicalDisk (her Disk için)</span><span class="sxs-lookup"><span data-stu-id="8d23a-122">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="8d23a-123">Disk Yazma/sn</span><span class="sxs-lookup"><span data-stu-id="8d23a-123">Disk Writes/sec</span></span> |
| <span data-ttu-id="8d23a-124">PhysicalDisk (her Disk için)</span><span class="sxs-lookup"><span data-stu-id="8d23a-124">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="8d23a-125">Disk Yazma Bayt/sn</span><span class="sxs-lookup"><span data-stu-id="8d23a-125">Disk Write Bytes/sec</span></span> |
| <span data-ttu-id="8d23a-126">Bellek</span><span class="sxs-lookup"><span data-stu-id="8d23a-126">Memory</span></span> | <span data-ttu-id="8d23a-127">Kullanılabilir MBayt</span><span class="sxs-lookup"><span data-stu-id="8d23a-127">Available MBytes</span></span> |
| <span data-ttu-id="8d23a-128">PagingFile</span><span class="sxs-lookup"><span data-stu-id="8d23a-128">PagingFile</span></span> | <span data-ttu-id="8d23a-129">% Kullanım</span><span class="sxs-lookup"><span data-stu-id="8d23a-129">% Usage</span></span> |
| <span data-ttu-id="8d23a-130">Process(Total)</span><span class="sxs-lookup"><span data-stu-id="8d23a-130">Process(Total)</span></span> | <span data-ttu-id="8d23a-131">% İşlemci zamanı</span><span class="sxs-lookup"><span data-stu-id="8d23a-131">% Processor Time</span></span> |
| <span data-ttu-id="8d23a-132">İşlem (her hizmeti)</span><span class="sxs-lookup"><span data-stu-id="8d23a-132">Process (per service)</span></span> | <span data-ttu-id="8d23a-133">% İşlemci zamanı</span><span class="sxs-lookup"><span data-stu-id="8d23a-133">% Processor Time</span></span> |
| <span data-ttu-id="8d23a-134">İşlem (her hizmeti)</span><span class="sxs-lookup"><span data-stu-id="8d23a-134">Process (per service)</span></span> | <span data-ttu-id="8d23a-135">İşlem kimliği</span><span class="sxs-lookup"><span data-stu-id="8d23a-135">ID Process</span></span> |
| <span data-ttu-id="8d23a-136">İşlem (her hizmeti)</span><span class="sxs-lookup"><span data-stu-id="8d23a-136">Process (per service)</span></span> | <span data-ttu-id="8d23a-137">Özel bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="8d23a-137">Private Bytes</span></span> |
| <span data-ttu-id="8d23a-138">İşlem (her hizmeti)</span><span class="sxs-lookup"><span data-stu-id="8d23a-138">Process (per service)</span></span> | <span data-ttu-id="8d23a-139">İş parçacığı sayısı</span><span class="sxs-lookup"><span data-stu-id="8d23a-139">Thread Count</span></span> |
| <span data-ttu-id="8d23a-140">İşlem (her hizmeti)</span><span class="sxs-lookup"><span data-stu-id="8d23a-140">Process (per service)</span></span> | <span data-ttu-id="8d23a-141">Sanal bayt sayısı</span><span class="sxs-lookup"><span data-stu-id="8d23a-141">Virtual Bytes</span></span> |
| <span data-ttu-id="8d23a-142">İşlem (her hizmeti)</span><span class="sxs-lookup"><span data-stu-id="8d23a-142">Process (per service)</span></span> | <span data-ttu-id="8d23a-143">Çalışma kümesi</span><span class="sxs-lookup"><span data-stu-id="8d23a-143">Working Set</span></span> |
| <span data-ttu-id="8d23a-144">İşlem (her hizmeti)</span><span class="sxs-lookup"><span data-stu-id="8d23a-144">Process (per service)</span></span> | <span data-ttu-id="8d23a-145">Çalışma kümesi - özel</span><span class="sxs-lookup"><span data-stu-id="8d23a-145">Working Set - Private</span></span> |

## <a name="net-applications-and-services"></a><span data-ttu-id="8d23a-146">.NET uygulamaları ve Hizmetleri</span><span class="sxs-lookup"><span data-stu-id="8d23a-146">.NET applications and services</span></span>

<span data-ttu-id="8d23a-147">.NET Hizmetleri tooyour küme dağıtıyorsanız sayaçları aşağıdaki hello toplayın.</span><span class="sxs-lookup"><span data-stu-id="8d23a-147">Collect hello following counters if you are deploying .NET services tooyour cluster.</span></span> 

| <span data-ttu-id="8d23a-148">Sayacı kategorisi</span><span class="sxs-lookup"><span data-stu-id="8d23a-148">Counter Category</span></span> | <span data-ttu-id="8d23a-149">Sayaç adı</span><span class="sxs-lookup"><span data-stu-id="8d23a-149">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="8d23a-150">.NET CLR bellek (her hizmeti)</span><span class="sxs-lookup"><span data-stu-id="8d23a-150">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="8d23a-151">İşlem kimliği</span><span class="sxs-lookup"><span data-stu-id="8d23a-151">Process ID</span></span> |
| <span data-ttu-id="8d23a-152">.NET CLR bellek (her hizmeti)</span><span class="sxs-lookup"><span data-stu-id="8d23a-152">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="8d23a-153"># Toplam kaydedilmiş bayt</span><span class="sxs-lookup"><span data-stu-id="8d23a-153"># Total committed Bytes</span></span> |
| <span data-ttu-id="8d23a-154">.NET CLR bellek (her hizmeti)</span><span class="sxs-lookup"><span data-stu-id="8d23a-154">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="8d23a-155"># Toplam bayt ayrılmış</span><span class="sxs-lookup"><span data-stu-id="8d23a-155"># Total reserved Bytes</span></span> |
| <span data-ttu-id="8d23a-156">.NET CLR bellek (her hizmeti)</span><span class="sxs-lookup"><span data-stu-id="8d23a-156">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="8d23a-157"># Tüm yığınlardaki bayt</span><span class="sxs-lookup"><span data-stu-id="8d23a-157"># Bytes in all Heaps</span></span> |
| <span data-ttu-id="8d23a-158">.NET CLR bellek (her hizmeti)</span><span class="sxs-lookup"><span data-stu-id="8d23a-158">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="8d23a-159"># Gen 0 koleksiyonları</span><span class="sxs-lookup"><span data-stu-id="8d23a-159"># Gen 0 Collections</span></span> |
| <span data-ttu-id="8d23a-160">.NET CLR bellek (her hizmeti)</span><span class="sxs-lookup"><span data-stu-id="8d23a-160">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="8d23a-161"># Gen 1 koleksiyonları</span><span class="sxs-lookup"><span data-stu-id="8d23a-161"># Gen 1 Collections</span></span> |
| <span data-ttu-id="8d23a-162">.NET CLR bellek (her hizmeti)</span><span class="sxs-lookup"><span data-stu-id="8d23a-162">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="8d23a-163"># Gen 2 koleksiyonları</span><span class="sxs-lookup"><span data-stu-id="8d23a-163"># Gen 2 Collections</span></span> |
| <span data-ttu-id="8d23a-164">.NET CLR bellek (her hizmeti)</span><span class="sxs-lookup"><span data-stu-id="8d23a-164">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="8d23a-165">GC % zaman</span><span class="sxs-lookup"><span data-stu-id="8d23a-165">% Time in GC</span></span> |

### <a name="service-fabrics-custom-performance-counters"></a><span data-ttu-id="8d23a-166">Service Fabric'ın özel performans sayaçları</span><span class="sxs-lookup"><span data-stu-id="8d23a-166">Service Fabric's custom performance counters</span></span>

<span data-ttu-id="8d23a-167">Service Fabric özel performans sayaçları önemli miktarda oluşturur.</span><span class="sxs-lookup"><span data-stu-id="8d23a-167">Service Fabric generates a substantial amount of custom performance counters.</span></span> <span data-ttu-id="8d23a-168">Merhaba yüklü SDK varsa, Performans İzleyicisi uygulamanızda hello kapsamlı listesi Windows makinenizde görebilirsiniz (Başlat > Performans İzleyicisi).</span><span class="sxs-lookup"><span data-stu-id="8d23a-168">If you have hello SDK installed, you can see hello comprehensive list on your Windows machine in your Performance Monitor application (Start > Performance Monitor).</span></span> 

<span data-ttu-id="8d23a-169">Merhaba uygulamalarda tooyour küme dağıtıyorsanız, Reliable Actors kullanıyorsanız, gelen countes ekleyin `Service Fabric Actor` ve `Service Fabric Actor Method` kategorileri (bkz [Service Fabric güvenilir aktörler tanılama](service-fabric-reliable-actors-diagnostics.md)).</span><span class="sxs-lookup"><span data-stu-id="8d23a-169">In hello applications you are deploying tooyour cluster, if you are using Reliable Actors, add countes from `Service Fabric Actor` and `Service Fabric Actor Method` categories (see [Service Fabric Reliable Actors Diagnostics](service-fabric-reliable-actors-diagnostics.md)).</span></span>

<span data-ttu-id="8d23a-170">Güvenilir hizmetlerini kullanıyorsanız, benzer şekilde sahibiz `Service Fabric Service` ve `Service Fabric Service Method` toplamanız gerekir sayacı kategorileri sayaçları.</span><span class="sxs-lookup"><span data-stu-id="8d23a-170">If you use Reliable Services, we similarly have `Service Fabric Service` and `Service Fabric Service Method` counter categories that you should collect counters from.</span></span> 

<span data-ttu-id="8d23a-171">Güvenilir koleksiyonları kullanırsanız, hello eklemenizi öneririz `Avg. Transaction ms/Commit` hello gelen `Service Fabric Transactional Replicator` toocollect hello ortalama yürütme gecikmesi işlem ölçüm başına.</span><span class="sxs-lookup"><span data-stu-id="8d23a-171">If you use Reliable Collections, we recommend adding hello `Avg. Transaction ms/Commit` from hello `Service Fabric Transactional Replicator` toocollect hello average commit latency per transaction metric.</span></span>


## <a name="next-steps"></a><span data-ttu-id="8d23a-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="8d23a-172">Next steps</span></span>

* <span data-ttu-id="8d23a-173">Daha fazla bilgi edinmek [olay oluşturma hello platform düzeyinde](service-fabric-diagnostics-event-generation-infra.md) Service Fabric içinde</span><span class="sxs-lookup"><span data-stu-id="8d23a-173">Learn more about [event generation at hello platform level](service-fabric-diagnostics-event-generation-infra.md) in Service Fabric</span></span>
* <span data-ttu-id="8d23a-174">Aracılığıyla performans ölçümlerini derleme [Azure tanılama](service-fabric-diagnostics-event-aggregation-wad.md)</span><span class="sxs-lookup"><span data-stu-id="8d23a-174">Collect performance metrics through [Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md)</span></span>
