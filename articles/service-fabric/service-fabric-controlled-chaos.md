---
title: "Service Fabric Chaos aaaInduce kümeleri | Microsoft Docs"
description: "Hata ekleme ve küme analiz hizmeti API'leri toomanage Chaos hello kümedeki kullanma."
services: service-fabric
documentationcenter: .net
author: motanv
manager: anmola
editor: motanv
ms.assetid: 2bd13443-3478-4382-9a5a-1f6c6b32bfc9
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: motanv
ms.openlocfilehash: 7e87cae22645fc4ba52e258471d8f3a4ffdb1cce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="induce-controlled-chaos-in-service-fabric-clusters"></a><span data-ttu-id="66c95-103">Service Fabric kümelerinde denetimli Chaos anlamına</span><span class="sxs-lookup"><span data-stu-id="66c95-103">Induce controlled Chaos in Service Fabric clusters</span></span>
<span data-ttu-id="66c95-104">Bulut altyapılarının doğası gereği güvenilir gibi büyük ölçekli dağıtılmış sistemler.</span><span class="sxs-lookup"><span data-stu-id="66c95-104">Large-scale distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="66c95-105">Azure Service Fabric geliştiriciler toowrite güvenilir dağıtılmış hizmet güvenilir olmayan bir altyapının en üstünde sağlar.</span><span class="sxs-lookup"><span data-stu-id="66c95-105">Azure Service Fabric enables developers toowrite reliable distributed services on top of an unreliable infrastructure.</span></span> <span data-ttu-id="66c95-106">toowrite sağlam dağıtılmış hizmetlerini güvenilir olmayan bir altyapının en üstünde, geliştiricilerin gerekir toobe mümkün tootest hello hizmetlerini kararlılığını güvenilmez altyapısını temel hello karmaşık durumu geçişleri giderek sırada son toofaults.</span><span class="sxs-lookup"><span data-stu-id="66c95-106">toowrite robust distributed services on top of an unreliable infrastructure, developers need toobe able tootest hello stability of their services while hello underlying unreliable infrastructure is going through complicated state transitions due toofaults.</span></span>

<span data-ttu-id="66c95-107">Merhaba [hata ekleme ve küme analiz hizmeti](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (olarak da bilinen hata analizi hizmeti hello) imkanı geliştiriciler hello tooinduce hizmetlerini tootest hataları.</span><span class="sxs-lookup"><span data-stu-id="66c95-107">hello [Fault Injection and Cluster Analysis Service](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (also known as hello Fault Analysis Service) gives developers hello ability tooinduce faults tootest their services.</span></span> <span data-ttu-id="66c95-108">Bunlar hedeflenen gibi hataları, benzetimli [bir bölümü yeniden](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), hello en yaygın durumu geçişleri çalışma yardımcı olabilir.</span><span class="sxs-lookup"><span data-stu-id="66c95-108">These targeted simulated faults, like [restarting a partition](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), can help exercise hello most common state transitions.</span></span> <span data-ttu-id="66c95-109">Ancak hedeflenen benzetimli hataları tanımına göre ağırlıklı ve böylece kaçırabilir gösteren yedekleme yalnızca sabit tahmin, uzun ve karmaşık sırası durumu geçişleri içinde hataları.</span><span class="sxs-lookup"><span data-stu-id="66c95-109">However targeted simulated faults are biased by definition and thus may miss bugs that show up only in hard-to-predict, long and complicated sequence of state transitions.</span></span> <span data-ttu-id="66c95-110">Bir taraflı olmayan test etmek için Chaos kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66c95-110">For an unbiased testing, you can use Chaos.</span></span>

<span data-ttu-id="66c95-111">Chaos uzun süreler boyunca hello küme boyunca düzenli, araya eklemeli hataları (normal ve durunda) benzetimini yapar.</span><span class="sxs-lookup"><span data-stu-id="66c95-111">Chaos simulates periodic, interleaved faults (both graceful and ungraceful) throughout hello cluster over extended periods of time.</span></span> <span data-ttu-id="66c95-112">Merhaba oranı ve hataları hello tür Chaos yapılandırdıktan sonra hataları hello küme ve hizmetlerinizi oluşturma C# veya Powershell API'si toostart aracılığıyla Chaos başlatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66c95-112">Once you have configured Chaos with hello rate and hello kind of faults, you can start Chaos through C# or Powershell API toostart generating faults in hello cluster and in your services.</span></span> <span data-ttu-id="66c95-113">Daha sonra durdurur Chaos otomatik olarak, belirli bir süre için (örneğin, bir saat), Chaos toorun yapılandırabilir ya da StopChaos API (C# veya Powershell) toostop çağırabilirsiniz, dilediğiniz zaman.</span><span class="sxs-lookup"><span data-stu-id="66c95-113">You can configure Chaos toorun for a specified time period (for example, for one hour), after which Chaos stops automatically, or you can call StopChaos API (C# or Powershell) toostop it at any time.</span></span>

> [!NOTE]
> <span data-ttu-id="66c95-114">Mevcut haliyle Chaos yalnızca güvenli hataları, dış hataları hello olmaması durumunda bir çekirdek kayıp veya veri kaybı hiçbir zaman oluştuğunu gelir uygulanmasını.</span><span class="sxs-lookup"><span data-stu-id="66c95-114">In its current form, Chaos induces only safe faults, which implies that in hello absence of external faults a quorum loss, or data loss never occurs.</span></span>
>

<span data-ttu-id="66c95-115">Chaos çalışırken hello şu anda çalıştırmak hello hello durumunu yakalama farklı olayları üretir.</span><span class="sxs-lookup"><span data-stu-id="66c95-115">While Chaos is running, it produces different events that capture hello state of hello run at hello moment.</span></span> <span data-ttu-id="66c95-116">Örneğin, bir ExecutingFaultsEvent Chaos bu yineleme tooexecute karar verdiği tüm hello hataları içerir.</span><span class="sxs-lookup"><span data-stu-id="66c95-116">For example, an ExecutingFaultsEvent contains all hello faults that Chaos has decided tooexecute in that iteration.</span></span> <span data-ttu-id="66c95-117">Bir ValidationFailedEvent hello küme hello doğrulama sırasında bulundu bir doğrulama hatası (sistem durumu veya kararlılık sorunları) hello ayrıntılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="66c95-117">A ValidationFailedEvent contains hello details of a validation failure (health or stability issues) that was found during hello validation of hello cluster.</span></span> <span data-ttu-id="66c95-118">Merhaba GetChaosReport API (C# veya Powershell) tooget hello rapor Chaos çalıştırılan çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66c95-118">You can invoke hello GetChaosReport API (C# or Powershell) tooget hello report of Chaos runs.</span></span> <span data-ttu-id="66c95-119">Bu olaylar kalıcı bir [güvenilir sözlük](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), iki yapılandırmaları tarafından dikte kesilmesi ilkesi vardır: **MaxStoredChaosEventCount** (varsayılan değer olan 25000) ve **StoredActionCleanupIntervalInSeconds** (varsayılan değer olan 3600).</span><span class="sxs-lookup"><span data-stu-id="66c95-119">These events get persisted in a [reliable dictionary](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), which has a truncation policy dictated by two configurations: **MaxStoredChaosEventCount** (default value is 25000) and **StoredActionCleanupIntervalInSeconds** (default value is 3600).</span></span> <span data-ttu-id="66c95-120">Her *StoredActionCleanupIntervalInSeconds* Chaos denetler ve tüm ancak hello en son *MaxStoredChaosEventCount* olayları hello güvenilir sözlükten temizlendi.</span><span class="sxs-lookup"><span data-stu-id="66c95-120">Every *StoredActionCleanupIntervalInSeconds* Chaos checks and all but hello most recent *MaxStoredChaosEventCount* events, are purged from hello reliable dictionary.</span></span>

## <a name="faults-induced-in-chaos"></a><span data-ttu-id="66c95-121">İçinde Chaos kopyaladığınızda hataları</span><span class="sxs-lookup"><span data-stu-id="66c95-121">Faults induced in Chaos</span></span>
<span data-ttu-id="66c95-122">Chaos hello tüm Service Fabric kümesi arasında hataları oluşturur ve ay veya yıl birkaç saat görülür hataları sıkıştırır.</span><span class="sxs-lookup"><span data-stu-id="66c95-122">Chaos generates faults across hello entire Service Fabric cluster and compresses faults that are seen in months or years into a few hours.</span></span> <span data-ttu-id="66c95-123">Merhaba yüksek hata oranı araya eklemeli hataları Hello birleşimi aksi atlanabilir köşe durumları bulur.</span><span class="sxs-lookup"><span data-stu-id="66c95-123">hello combination of interleaved faults with hello high fault rate finds corner cases that may otherwise be missed.</span></span> <span data-ttu-id="66c95-124">Bu alıştırmada karmaşık dünyada tooa önemli iyileştirme hello kod hello hizmet kalitesi yol açar.</span><span class="sxs-lookup"><span data-stu-id="66c95-124">This exercise of Chaos leads tooa significant improvement in hello code quality of hello service.</span></span>

<span data-ttu-id="66c95-125">Chaos hataları kategorileri aşağıdaki hello gelen uygulanmasını:</span><span class="sxs-lookup"><span data-stu-id="66c95-125">Chaos induces faults from hello following categories:</span></span>

* <span data-ttu-id="66c95-126">Bir düğümü yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="66c95-126">Restart a node</span></span>
* <span data-ttu-id="66c95-127">Dağıtılmış kod paketi yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="66c95-127">Restart a deployed code package</span></span>
* <span data-ttu-id="66c95-128">Bir yineleme kaldırma</span><span class="sxs-lookup"><span data-stu-id="66c95-128">Remove a replica</span></span>
* <span data-ttu-id="66c95-129">Bir çoğaltmayı yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="66c95-129">Restart a replica</span></span>
* <span data-ttu-id="66c95-130">Bir birincil çoğaltmayı (yapılandırılabilir) taşıma</span><span class="sxs-lookup"><span data-stu-id="66c95-130">Move a primary replica (configurable)</span></span>
* <span data-ttu-id="66c95-131">Bir ikincil çoğaltma (yapılandırılabilir) taşıma</span><span class="sxs-lookup"><span data-stu-id="66c95-131">Move a secondary replica (configurable)</span></span>

<span data-ttu-id="66c95-132">Chaos içinde birden çok kez çalışır.</span><span class="sxs-lookup"><span data-stu-id="66c95-132">Chaos runs in multiple iterations.</span></span> <span data-ttu-id="66c95-133">Her bir yineleme hataları oluşur ve hello için küme doğrulama period belirtildi.</span><span class="sxs-lookup"><span data-stu-id="66c95-133">Each iteration consists of faults and cluster validation for hello specified period.</span></span> <span data-ttu-id="66c95-134">Merhaba küme toostabilize ve doğrulama toosucceed hello zamanın yapılandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66c95-134">You can configure hello time spent for hello cluster toostabilize and for validation toosucceed.</span></span> <span data-ttu-id="66c95-135">Küme doğrulama hata bulunursa, Chaos oluşturur ve ValidationFailedEvent hello UTC zaman damgası ve hello hata ayrıntıları ile devam ettirir.</span><span class="sxs-lookup"><span data-stu-id="66c95-135">If a failure is found in cluster validation, Chaos generates and persists a ValidationFailedEvent with hello UTC timestamp and hello failure details.</span></span> <span data-ttu-id="66c95-136">Örneğin, bir saat en fazla üç eşzamanlı hataları için ayarlanmış bir toorun karmaşık dünyada örneği göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="66c95-136">For example, consider an instance of Chaos that is set toorun for an hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="66c95-137">Chaos üç hataları uygulanmasını ve hello küme durumu doğrular.</span><span class="sxs-lookup"><span data-stu-id="66c95-137">Chaos induces three faults, and then validates hello cluster health.</span></span> <span data-ttu-id="66c95-138">Merhaba önceki açıkça hello StopChaosAsync API aracılığıyla durdurulmuş veya bir saatlik olana kadar adım geçirir yineler.</span><span class="sxs-lookup"><span data-stu-id="66c95-138">It iterates through hello previous step until it is explicitly stopped through hello StopChaosAsync API or one-hour passes.</span></span> <span data-ttu-id="66c95-139">Her yinelemede Hello küme bozulursa (diğer bir deyişle, bu MaxClusterStabilizationTimeout içinde geçirilen hello içinde Sabitle değil), Chaos bir ValidationFailedEvent oluşturur.</span><span class="sxs-lookup"><span data-stu-id="66c95-139">If hello cluster becomes unhealthy in any iteration (that is, it does not stabilize within hello passed-in MaxClusterStabilizationTimeout), Chaos generates a ValidationFailedEvent.</span></span> <span data-ttu-id="66c95-140">Bu olay, bir şeyler yanlış geçti ve daha fazla araştırma gerekebilir gösterir.</span><span class="sxs-lookup"><span data-stu-id="66c95-140">This event indicates that something has gone wrong and might need further investigation.</span></span>

<span data-ttu-id="66c95-141">kopyaladığınızda Chaos hataları tooget GetChaosReport API (powershell veya C#) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66c95-141">tooget which faults Chaos induced, you can use GetChaosReport API (powershell or C#).</span></span> <span data-ttu-id="66c95-142">Merhaba API hello sonraki kesimini hello Chaos raporunun hello geçilen devamlılık belirteci veya hello geçen zaman aralığı temel alır.</span><span class="sxs-lookup"><span data-stu-id="66c95-142">hello API gets hello next segment of hello Chaos report based on hello passed-in continuation token or hello passed-in time-range.</span></span> <span data-ttu-id="66c95-143">ContinuationToken tooget hello sonraki kesimin hello Chaos rapor hello veya StartTimeUtc ve EndTimeUtc aracılığıyla hello zaman aralığını belirtebilirsiniz, ancak hello hello ContinuationToken ve hello zaman aralığı belirtemezsiniz ya da belirtebilirsiniz aynı çağrısı.</span><span class="sxs-lookup"><span data-stu-id="66c95-143">You can either specify hello ContinuationToken tooget hello next segment of hello Chaos report or you can specify hello time-range through StartTimeUtc and EndTimeUtc, but you cannot specify both hello ContinuationToken and hello time-range in hello same call.</span></span> <span data-ttu-id="66c95-144">100'den fazla Chaos olayları olduğunda hello Chaos rapor, en fazla 100 Chaos olay kesimi içerdiği segmentlerinde döndürülür.</span><span class="sxs-lookup"><span data-stu-id="66c95-144">When there are more than 100 Chaos events, hello Chaos report is returned in segments where a segment contains no more than 100 Chaos events.</span></span>

## <a name="important-configuration-options"></a><span data-ttu-id="66c95-145">Önemli yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="66c95-145">Important configuration options</span></span>
* <span data-ttu-id="66c95-146">**TimeToRun**: toplam saat Chaos çalıştıran ile başarılı tamamlanmadan önce.</span><span class="sxs-lookup"><span data-stu-id="66c95-146">**TimeToRun**: Total time that Chaos runs before it finishes with success.</span></span> <span data-ttu-id="66c95-147">Merhaba StopChaos API hello TimeToRun boyunca çalıştıktan önce Chaos durdurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="66c95-147">You can stop Chaos before it has run for hello TimeToRun period through hello StopChaos API.</span></span>

* <span data-ttu-id="66c95-148">**MaxClusterStabilizationTimeout**: hello maksimum hello küme toobecome bir ValidationFailedEvent oluşturan önce sağlıklı zaman toowait miktarı.</span><span class="sxs-lookup"><span data-stu-id="66c95-148">**MaxClusterStabilizationTimeout**: hello maximum amount of time toowait for hello cluster toobecome healthy before producing a ValidationFailedEvent.</span></span> <span data-ttu-id="66c95-149">Bu kurtarma sırasında bu bekleme tooreduce hello hello kümede yüktür.</span><span class="sxs-lookup"><span data-stu-id="66c95-149">This wait is tooreduce hello load on hello cluster while it is recovering.</span></span> <span data-ttu-id="66c95-150">gerçekleştirilen hello denetimleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="66c95-150">hello checks performed are:</span></span>
  * <span data-ttu-id="66c95-151">Merhaba küme durumu Tamam ise</span><span class="sxs-lookup"><span data-stu-id="66c95-151">If hello cluster health is OK</span></span>
  * <span data-ttu-id="66c95-152">Merhaba hizmet durumu Tamam ise</span><span class="sxs-lookup"><span data-stu-id="66c95-152">If hello service health is OK</span></span>
  * <span data-ttu-id="66c95-153">Merhaba hedef çoğaltma kümesi boyutu, hello hizmet bölüm için elde edilir</span><span class="sxs-lookup"><span data-stu-id="66c95-153">If hello target replica set size is achieved for hello service partition</span></span>
  * <span data-ttu-id="66c95-154">Hiçbir Inbuild çoğaltmaların var</span><span class="sxs-lookup"><span data-stu-id="66c95-154">That no InBuild replicas exist</span></span>
* <span data-ttu-id="66c95-155">**MaxConcurrentFaults**: Merhaba her yinelemede kopyaladığınızda eşzamanlı hataları maksimum sayısı.</span><span class="sxs-lookup"><span data-stu-id="66c95-155">**MaxConcurrentFaults**: hello maximum number of concurrent faults that are induced in each iteration.</span></span> <span data-ttu-id="66c95-156">Merhaba yüksek hello sayı, hello daha agresif Chaos olduğundan ve küme hello hello yük devretme ve hello durumu geçişi birleşimler geçtiği ayrıca daha karmaşıktır.</span><span class="sxs-lookup"><span data-stu-id="66c95-156">hello higher hello number, hello more aggressive Chaos is and hello failovers and hello state transition combinations that hello cluster goes through are also more complex.</span></span> 

> [!NOTE]
> <span data-ttu-id="66c95-157">Ne olursa olsun nasıl yüksek bir değer *MaxConcurrentFaults* varsa, Chaos - dış hataları - hello olmaması durumunda çekirdek kayıp veya veri kaybı yoktur güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="66c95-157">Regardless how high a value *MaxConcurrentFaults* has, Chaos guarantees - in hello absence of external faults - there is no quorum loss or data loss.</span></span>
>

* <span data-ttu-id="66c95-158">**EnableMoveReplicaFaults**: etkinleştirir veya hello birincil veya ikincil çoğaltmaları toomove neden hello hataları devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="66c95-158">**EnableMoveReplicaFaults**: Enables or disables hello faults that cause hello primary or secondary replicas toomove.</span></span> <span data-ttu-id="66c95-159">Bu hataları varsayılan olarak devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="66c95-159">These faults are disabled by default.</span></span>
* <span data-ttu-id="66c95-160">**WaitTimeBetweenIterations**: yinelemeleri arasındaki zaman toowait hello miktarı.</span><span class="sxs-lookup"><span data-stu-id="66c95-160">**WaitTimeBetweenIterations**: hello amount of time toowait between iterations.</span></span> <span data-ttu-id="66c95-161">Diğer bir deyişle, Chaos gidiş hataları ve hello karşılık gelen hello küme hello durumunu doğrulanması tamamlandı yürütüldükten sonra duraklatma süreyi hello.</span><span class="sxs-lookup"><span data-stu-id="66c95-161">That is, hello amount of time Chaos will pause after having executed a round of faults and having finished hello corresponding validation of hello health of hello cluster.</span></span> <span data-ttu-id="66c95-162">Merhaba hello değer arttıkça hello daha düşük olan hello ortalama hata ekleme oranı.</span><span class="sxs-lookup"><span data-stu-id="66c95-162">hello higher hello value, hello lower is hello average fault injection rate.</span></span>
* <span data-ttu-id="66c95-163">**WaitTimeBetweenFaults**: tek bir yineleme iki ardışık hataları arasında zaman toowait hello miktarı.</span><span class="sxs-lookup"><span data-stu-id="66c95-163">**WaitTimeBetweenFaults**: hello amount of time toowait between two consecutive faults in a single iteration.</span></span> <span data-ttu-id="66c95-164">Merhaba daha yüksek hello değeri, daha düşük hello eşzamanlılığı hello (veya hello arasında örtüşme) hataları.</span><span class="sxs-lookup"><span data-stu-id="66c95-164">hello higher hello value, hello lower hello concurrency of (or hello overlap between) faults.</span></span>
* <span data-ttu-id="66c95-165">**ClusterHealthPolicy**: küme sistem durumu ilkesi kullanılan toovalidate hello Chaos yineleme Between hello küme durumunu olduğunu.</span><span class="sxs-lookup"><span data-stu-id="66c95-165">**ClusterHealthPolicy**: Cluster health policy is used toovalidate hello health of hello cluster in between Chaos iterations.</span></span> <span data-ttu-id="66c95-166">Merhaba küme sistem durumu hatası veya hataya yürütme sırasında beklenmeyen bir özel durum oluşursa, Chaos hello sonraki sistem durumu denetimi - bazı zaman toorecuperate tooprovide hello kümeyle önce 30 dakika bekler.</span><span class="sxs-lookup"><span data-stu-id="66c95-166">If hello cluster health is in error or if an unexpected exception happens during fault execution, Chaos will wait for 30 minutes before hello next health-check - tooprovide hello cluster with some time toorecuperate.</span></span>
* <span data-ttu-id="66c95-167">**Bağlam**: (dize, dize) koleksiyonunu anahtar-değer çiftlerini yazın.</span><span class="sxs-lookup"><span data-stu-id="66c95-167">**Context**: A collection of (string, string) type key-value pairs.</span></span> <span data-ttu-id="66c95-168">Merhaba eşlemesi kullanılan toorecord hello Chaos çalıştırma hakkında bilgi olabilir.</span><span class="sxs-lookup"><span data-stu-id="66c95-168">hello map can be used toorecord information about hello Chaos run.</span></span> <span data-ttu-id="66c95-169">Bu tür çiftleri 100'den fazla olamaz ve her bir dize (anahtar veya değer) en fazla 4095 karakterden uzun olamaz.</span><span class="sxs-lookup"><span data-stu-id="66c95-169">There cannot be more than 100 such pairs and each string (key or value) can be at most 4095 characters long.</span></span> <span data-ttu-id="66c95-170">Bu haritada hello çalıştırmak Chaos toooptionally deposu hello bağlamının hello belirli çalıştırma hakkında hello başlatıcı tarafından ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="66c95-170">This map is set by hello starter of hello Chaos run toooptionally store hello context about hello specific run.</span></span>

## <a name="how-toorun-chaos"></a><span data-ttu-id="66c95-171">Nasıl toorun Chaos</span><span class="sxs-lookup"><span data-stu-id="66c95-171">How toorun Chaos</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using System.Fabric;

using System.Diagnostics;
using System.Fabric.Chaos.DataStructures;

class Program
{
    private class ChaosEventComparer : IEqualityComparer<ChaosEvent>
    {
        public bool Equals(ChaosEvent x, ChaosEvent y)
        {
            return x.TimeStampUtc.Equals(y.TimeStampUtc);
        }

        public int GetHashCode(ChaosEvent obj)
        {
            return obj.TimeStampUtc.GetHashCode();
        }
    }

    static void Main(string[] args)
    {
        var clusterConnectionString = "localhost:19000";
        using (var client = new FabricClient(clusterConnectionString))
        {
            var startTimeUtc = DateTime.UtcNow;
            var stabilizationTimeout = TimeSpan.FromSeconds(30.0);
            var timeToRun = TimeSpan.FromMinutes(60.0);
            var maxConcurrentFaults = 3;

            var parameters = new ChaosParameters(
                stabilizationTimeout,
                maxConcurrentFaults,
                true, /* EnableMoveReplicaFault */
                timeToRun);

            try
            {
                client.TestManager.StartChaosAsync(parameters).GetAwaiter().GetResult();
            }
            catch (FabricChaosAlreadyRunningException)
            {
                Console.WriteLine("An instance of Chaos is already running in hello cluster.");
            }

            var filter = new ChaosReportFilter(startTimeUtc, DateTime.MaxValue);

            var eventSet = new HashSet<ChaosEvent>(new ChaosEventComparer());

            while (true)
            {
                var report = client.TestManager.GetChaosReportAsync(filter).GetAwaiter().GetResult();

                foreach (var chaosEvent in report.History)
                {
                    if (eventSet.Add(chaosEvent))
                    {
                        Console.WriteLine(chaosEvent);
                    }
                }

                // When Chaos stops, a StoppedEvent is created.
                // If a StoppedEvent is found, exit hello loop.
                var lastEvent = report.History.LastOrDefault();

                if (lastEvent is StoppedEvent)
                {
                    break;
                }

                Task.Delay(TimeSpan.FromSeconds(1.0)).GetAwaiter().GetResult();
            }
        }
    }
}
```

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

$events = @{}
$now = [System.DateTime]::UtcNow

Start-ServiceFabricChaos -TimeToRunMinute $timeToRun -MaxConcurrentFaults $concurrentFaults -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec

while($true)
{
    $stopped = $false
    $report = Get-ServiceFabricChaosReport -StartTimeUtc $now -EndTimeUtc ([System.DateTime]::MaxValue)

    foreach ($e in $report.History) {

        if(-Not ($events.Contains($e.TimeStampUtc.Ticks)))
        {
            $events.Add($e.TimeStampUtc.Ticks, $e)
            if($e -is [System.Fabric.Chaos.DataStructures.ValidationFailedEvent])
            {
                Write-Host -BackgroundColor White -ForegroundColor Red $e
            }
            else
            {
                if($e -is [System.Fabric.Chaos.DataStructures.StoppedEvent])
                {
                    $stopped = $true
                }

                Write-Host $e
            }
        }
    }

    if($stopped -eq $true)
    {
        break
    }

    Start-Sleep -Seconds 1
}

Stop-ServiceFabricChaos
```
