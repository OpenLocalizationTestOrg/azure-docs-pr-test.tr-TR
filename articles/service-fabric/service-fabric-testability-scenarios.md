---
title: "Azure mikro için aaaCreate chaos ve yük devretme testleri | Microsoft Docs"
description: "Merhaba Service Fabric chaos test ve yük devretme kullanarak senaryoları tooinduce hataları test etmek ve hizmetlerinizi hello güvenilirliğini doğrulayın."
services: service-fabric
documentationcenter: .net
author: motanv
manager: rsinha
editor: toddabel
ms.assetid: 8eee7e89-404a-4605-8f00-7e4d4fb17553
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: motanv
ms.openlocfilehash: 1cac4f9e0e4a6c8416d5220d1537b5110decd1f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="testability-scenarios"></a><span data-ttu-id="7c7a6-103">Test Edilebilirlik senaryoları</span><span class="sxs-lookup"><span data-stu-id="7c7a6-103">Testability scenarios</span></span>
<span data-ttu-id="7c7a6-104">Bulut altyapılarının doğası gereği güvenilir gibi büyük dağıtılan sistemlerde.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-104">Large distributed systems like cloud infrastructures are inherently unreliable.</span></span> <span data-ttu-id="7c7a6-105">Azure Service Fabric verir geliştiriciler hello özelliği toowrite Hizmetleri toorun güvenilmez altyapılar üstünde.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-105">Azure Service Fabric gives developers hello ability toowrite services toorun on top of unreliable infrastructures.</span></span> <span data-ttu-id="7c7a6-106">Sipariş toowrite yüksek kaliteli Hizmetleri'nde geliştiricilerin kendi Hizmetleri gibi güvenilmeyen altyapı tootest hello kararlılığını toobe mümkün tooinduce gerekir.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-106">In order toowrite high-quality services, developers need toobe able tooinduce such unreliable infrastructure tootest hello stability of their services.</span></span>

<span data-ttu-id="7c7a6-107">Merhaba hata analizi hizmeti geliştiricilere hataları hello bulunması hello özelliği tooinduce hata eylemleri tootest hizmetleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-107">hello Fault Analysis Service gives developers hello ability tooinduce fault actions tootest services in hello presence of failures.</span></span> <span data-ttu-id="7c7a6-108">Ancak, hedeflenen benzetimli hataları yalnızca o ana kadarki alırsınız.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-108">However, targeted simulated faults will get you only so far.</span></span> <span data-ttu-id="7c7a6-109">Ayrıca, sınama tootake hello Service Fabric hello test senaryoları kullanabilirsiniz: chaos test ve bir yük devretme testi.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-109">tootake hello testing further, you can use hello test scenarios in Service Fabric: a chaos test and a failover test.</span></span> <span data-ttu-id="7c7a6-110">Bu senaryolar, normal ve durunda hello küme üzerinden uzun süre boyunca sürekli araya eklemeli hataları benzetimi.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-110">These scenarios simulate continuous interleaved faults, both graceful and ungraceful, throughout hello cluster over extended periods of time.</span></span> <span data-ttu-id="7c7a6-111">Bir test hello oranı ve hataları tür ile yapılandırıldıktan sonra ya da C# API'leri veya PowerShell, hello kümedeki toogenerate hataları ve hizmet başlatılabilir.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-111">Once a test is configured with hello rate and kind of faults, it can be started through either C# APIs or PowerShell, toogenerate faults in hello cluster and your service.</span></span>

> [!WARNING]
> <span data-ttu-id="7c7a6-112">ChaosTestScenario daha esnektir, hizmet tabanlı Chaos tarafından değiştirilmektedir.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-112">ChaosTestScenario is being replaced by a more resilient, service-based Chaos.</span></span> <span data-ttu-id="7c7a6-113">Lütfen toohello yeni makale başvurun [denetlenen Chaos](service-fabric-controlled-chaos.md) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-113">Please refer toohello new article [Controlled Chaos](service-fabric-controlled-chaos.md) for more details.</span></span>
> 
> 

## <a name="chaos-test"></a><span data-ttu-id="7c7a6-114">Chaos test</span><span class="sxs-lookup"><span data-stu-id="7c7a6-114">Chaos test</span></span>
<span data-ttu-id="7c7a6-115">Merhaba chaos senaryo hello tüm Service Fabric kümesi arasında hataları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-115">hello chaos scenario generates faults across hello entire Service Fabric cluster.</span></span> <span data-ttu-id="7c7a6-116">Merhaba senaryo genellikle birkaç saat ay veya yıl tooa görülen hataları sıkıştırır.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-116">hello scenario compresses faults generally seen in months or years tooa few hours.</span></span> <span data-ttu-id="7c7a6-117">Merhaba yüksek hata oranı araya eklemeli hataları Hello birleşimi aksi eksik köşe durumları bulur.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-117">hello combination of interleaved faults with hello high fault rate finds corner cases that are otherwise missed.</span></span> <span data-ttu-id="7c7a6-118">Bu tooa önemli iyileştirme hello kod hello hizmet kalitesi yol açar.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-118">This leads tooa significant improvement in hello code quality of hello service.</span></span>

### <a name="faults-simulated-in-hello-chaos-test"></a><span data-ttu-id="7c7a6-119">Merhaba chaos testinde benzetimli hataları</span><span class="sxs-lookup"><span data-stu-id="7c7a6-119">Faults simulated in hello chaos test</span></span>
* <span data-ttu-id="7c7a6-120">Bir düğümü yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="7c7a6-120">Restart a node</span></span>
* <span data-ttu-id="7c7a6-121">Dağıtılmış kod paketi yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="7c7a6-121">Restart a deployed code package</span></span>
* <span data-ttu-id="7c7a6-122">Bir yineleme kaldırma</span><span class="sxs-lookup"><span data-stu-id="7c7a6-122">Remove a replica</span></span>
* <span data-ttu-id="7c7a6-123">Bir çoğaltmayı yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="7c7a6-123">Restart a replica</span></span>
* <span data-ttu-id="7c7a6-124">(İsteğe bağlı) birincil kopya taşıma</span><span class="sxs-lookup"><span data-stu-id="7c7a6-124">Move a primary replica (optional)</span></span>
* <span data-ttu-id="7c7a6-125">(İsteğe bağlı) bir ikincil çoğaltma taşıma</span><span class="sxs-lookup"><span data-stu-id="7c7a6-125">Move a secondary replica (optional)</span></span>

<span data-ttu-id="7c7a6-126">Hello chaos test hataları birden çok kez çalışır ve küme doğrulama hello için belirtilen süre.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-126">hello chaos test runs multiple iterations of faults and cluster validations for hello specified period of time.</span></span> <span data-ttu-id="7c7a6-127">Merhaba küme toostabilize ve doğrulama toosucceed hello zamanın de yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-127">hello time spent for hello cluster toostabilize and for validation toosucceed is also configurable.</span></span> <span data-ttu-id="7c7a6-128">tek bir küme doğrulama hatasına isabet hello senaryo başarısız oluyor.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-128">hello scenario fails when you hit a single failure in cluster validation.</span></span>

<span data-ttu-id="7c7a6-129">Örneğin, bir saat en fazla üç eşzamanlı hataları toorun bir test kümesi göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-129">For example, consider a test set toorun for one hour with a maximum of three concurrent faults.</span></span> <span data-ttu-id="7c7a6-130">Merhaba test üç hataları anlamına ve hello küme durumunu doğrulamak.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-130">hello test will induce three faults, and then validate hello cluster health.</span></span> <span data-ttu-id="7c7a6-131">Merhaba test hello önceki adıma hello küme bozulur veya bir saat geçirir kadar yineleme.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-131">hello test will iterate through hello previous step till hello cluster becomes unhealthy or one hour passes.</span></span> <span data-ttu-id="7c7a6-132">Merhaba küme her yinelemede bozulursa, yani, yapılandırılan süre içinde Sabitle değil, hello test bir özel durum ile başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-132">If hello cluster becomes unhealthy in any iteration, i.e. it does not stabilize within a configured time, hello test will fail with an exception.</span></span> <span data-ttu-id="7c7a6-133">Bu durum, bir şeyler yanlış geçti ve daha fazla araştırma gerekiyor gösterir.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-133">This exception indicates that something has gone wrong and needs further investigation.</span></span>

<span data-ttu-id="7c7a6-134">Mevcut haliyle hello hataya nesil hello chaos test altyapısında yalnızca güvenli hataları uygulanmasını.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-134">In its current form, hello fault generation engine in hello chaos test induces only safe faults.</span></span> <span data-ttu-id="7c7a6-135">Başka bir deyişle, dış hatalarının hello olmaması durumunda, bir çekirdek veya veri kaybı asla meydana gelmez.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-135">This means that in hello absence of external faults, a quorum or data loss will never occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="7c7a6-136">Önemli yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="7c7a6-136">Important configuration options</span></span>
* <span data-ttu-id="7c7a6-137">**TimeToRun**: toplam süre hello test çalışacağı ile başarılı tamamlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-137">**TimeToRun**: Total time that hello test will run before finishing with success.</span></span> <span data-ttu-id="7c7a6-138">Merhaba test daha önce bir doğrulama hatası yerine bitirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-138">hello test can finish earlier in lieu of a validation failure.</span></span>
* <span data-ttu-id="7c7a6-139">**MaxClusterStabilizationTimeout**: saat toowait hello küme toobecome hello test başarısız olmadan önce sağlıklı için en fazla miktarı.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-139">**MaxClusterStabilizationTimeout**: Maximum amount of time toowait for hello cluster toobecome healthy before failing hello test.</span></span> <span data-ttu-id="7c7a6-140">Merhaba gerçekleştirilen denetimlerinin küme durumu Tamam olup olduğundan, hizmet durumu Tamam olduğunu, hello hedef çoğaltma kümesi boyutu hello hizmet bölüm için elde edilir ve hiçbir Inbuild çoğaltmaların mevcut.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-140">hello checks performed are whether cluster health is OK, service health is OK, hello target replica set size is achieved for hello service partition, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="7c7a6-141">**MaxConcurrentFaults**: en fazla eş zamanlı hatalarının sayısı her yinelemede kopyaladığınızda.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-141">**MaxConcurrentFaults**: Maximum number of concurrent faults induced in each iteration.</span></span> <span data-ttu-id="7c7a6-142">daha yüksek hello sayı Merhaba, bu nedenle daha karmaşık yük devretme ve geçiş birleşimleri kaynaklanan daha agresif hello test hello.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-142">hello higher hello number, hello more aggressive hello test, hence resulting in more complex failovers and transition combinations.</span></span> <span data-ttu-id="7c7a6-143">Merhaba test dış hataları olmaması durumunda olmayacaktır, bu yapılandırmanın nasıl yüksek olan yedeklemiş çekirdek veya veri kaybı güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-143">hello test guarantees that in absence of external faults there will not be a quorum or data loss, irrespective of how high this configuration is.</span></span>
* <span data-ttu-id="7c7a6-144">**EnableMoveReplicaFaults**: etkinleştirir ya da birincil veya ikincil çoğaltmaları hello hello taşınmasına neden olan hello hataları devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-144">**EnableMoveReplicaFaults**: Enables or disables hello faults that are causing hello move of hello primary or secondary replicas.</span></span> <span data-ttu-id="7c7a6-145">Bu hataları varsayılan olarak devre dışıdır.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-145">These faults are disabled by default.</span></span>
* <span data-ttu-id="7c7a6-146">**WaitTimeBetweenIterations**: gidiş hataları ve karşılık gelen doğrulama sonra yani yinelemeleri arasındaki zaman toowait miktarı.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-146">**WaitTimeBetweenIterations**: Amount of time toowait between iterations, i.e. after a round of faults and corresponding validation.</span></span>

### <a name="how-toorun-hello-chaos-test"></a><span data-ttu-id="7c7a6-147">Test nasıl toorun hello chaos</span><span class="sxs-lookup"><span data-stu-id="7c7a6-147">How toorun hello chaos test</span></span>
<span data-ttu-id="7c7a6-148">C# örneği</span><span class="sxs-lookup"><span data-stu-id="7c7a6-148">C# sample</span></span>

```csharp
using System;
using System.Fabric;
using System.Fabric.Testability.Scenario;
using System.Threading;
using System.Threading.Tasks;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";

        Console.WriteLine("Starting Chaos Test Scenario...");
        try
        {
            RunChaosTestScenarioAsync(clusterConnection).Wait();
        }
        catch (AggregateException ae)
        {
            Console.WriteLine("Chaos Test Scenario did not complete: ");
            foreach (Exception ex in ae.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("Chaos Test Scenario completed.");
        return 0;
    }

    static async Task RunChaosTestScenarioAsync(string clusterConnection)
    {
        TimeSpan maxClusterStabilizationTimeout = TimeSpan.FromSeconds(180);
        uint maxConcurrentFaults = 3;
        bool enableMoveReplicaFaults = true;

        // Create FabricClient with connection and security information here.
        FabricClient fabricClient = new FabricClient(clusterConnection);

        // hello chaos test scenario should run at least 60 minutes or until it fails.
        TimeSpan timeToRun = TimeSpan.FromMinutes(60);
        ChaosTestScenarioParameters scenarioParameters = new ChaosTestScenarioParameters(
          maxClusterStabilizationTimeout,
          maxConcurrentFaults,
          enableMoveReplicaFaults,
          timeToRun);

        // Other related parameters:
        // Pause between two iterations for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenIterations = TimeSpan.FromSeconds(30);
        // Pause between concurrent actions for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenFaults = TimeSpan.FromSeconds(10);

        // Create hello scenario class and execute it asynchronously.
        ChaosTestScenario chaosScenario = new ChaosTestScenario(fabricClient, scenarioParameters);

        try
        {
            await chaosScenario.ExecuteAsync(CancellationToken.None);
        }
        catch (AggregateException ae)
        {
            throw ae.InnerException;
        }
    }
}
```

<span data-ttu-id="7c7a6-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7c7a6-149">PowerShell</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```


## <a name="failover-test"></a><span data-ttu-id="7c7a6-150">Yük devretme testi</span><span class="sxs-lookup"><span data-stu-id="7c7a6-150">Failover test</span></span>
<span data-ttu-id="7c7a6-151">Merhaba yük devretme testi senaryosu, belirli hizmet bölüm hedefler hello chaos testi senaryosu sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-151">hello failover test scenario is a version of hello chaos test scenario that targets a specific service partition.</span></span> <span data-ttu-id="7c7a6-152">Yük devretme hello etkisini belirli hizmet bölümdeki hello diğer hizmetler etkilenmemesini bırakarak sınar.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-152">It tests hello effect of failover on a specific service partition while leaving hello other services unaffected.</span></span> <span data-ttu-id="7c7a6-153">Merhaba hedef bölüm bilgileri ve diğer parametreler ile yapılandırıldıktan sonra hizmet bölüm için C# API'leri veya PowerShell toogenerate hataları kullanan bir istemci-tarafı araç olarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-153">Once it's configured with hello target partition information and other parameters, it runs as a client-side tool that uses either C# APIs or PowerShell toogenerate faults for a service partition.</span></span> <span data-ttu-id="7c7a6-154">İş mantığınızın bir iş yükü hello yan tooprovide üzerinde çalışırken hello senaryo bir dizi benzetimli hataları ve hizmet doğrulama yineler.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-154">hello scenario iterates through a sequence of simulated faults and service validation while your business logic runs on hello side tooprovide a workload.</span></span> <span data-ttu-id="7c7a6-155">Bir hizmet doğrulama hatası daha fazla araştırma gereken bir sorun olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-155">A failure in service validation indicates an issue that needs further investigation.</span></span>

### <a name="faults-simulated-in-hello-failover-test"></a><span data-ttu-id="7c7a6-156">Merhaba yük devretme testi benzetimli hataları</span><span class="sxs-lookup"><span data-stu-id="7c7a6-156">Faults simulated in hello failover test</span></span>
* <span data-ttu-id="7c7a6-157">Merhaba bölüm barındırıldığı dağıtılmış kod paketi yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="7c7a6-157">Restart a deployed code package where hello partition is hosted</span></span>
* <span data-ttu-id="7c7a6-158">Bir birincil/ikincil çoğaltma veya durum bilgisiz örneğini Kaldır</span><span class="sxs-lookup"><span data-stu-id="7c7a6-158">Remove a primary/secondary replica or stateless instance</span></span>
* <span data-ttu-id="7c7a6-159">Birincil ve ikincil bir çoğaltma (bir kalıcı hizmeti) yeniden Başlat</span><span class="sxs-lookup"><span data-stu-id="7c7a6-159">Restart a primary secondary replica (if a persisted service)</span></span>
* <span data-ttu-id="7c7a6-160">Birincil çoğaltma taşıma</span><span class="sxs-lookup"><span data-stu-id="7c7a6-160">Move a primary replica</span></span>
* <span data-ttu-id="7c7a6-161">Bir ikincil çoğaltma taşıma</span><span class="sxs-lookup"><span data-stu-id="7c7a6-161">Move a secondary replica</span></span>
* <span data-ttu-id="7c7a6-162">Merhaba bölümü yeniden başlatın</span><span class="sxs-lookup"><span data-stu-id="7c7a6-162">Restart hello partition</span></span>

<span data-ttu-id="7c7a6-163">Merhaba yük devretme testi seçilen hataya uygulanmasını ve ardından doğrulama hello hizmet tooensure üzerinde kendi kararlılık çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-163">hello failover test induces a chosen fault and then runs validation on hello service tooensure its stability.</span></span> <span data-ttu-id="7c7a6-164">birden çok hataları hello chaos test zaman, karşılıklı olarak toopossible sırasında bir hata yalnızca hello yük devretme testi uygulanmasını.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-164">hello failover test induces only one fault at a time, as opposed toopossible multiple faults in hello chaos test.</span></span> <span data-ttu-id="7c7a6-165">Merhaba hizmet bölüm sonra her hata hello yapılandırılmış zaman aşımı süresi içinde Sabitle değil hello sınama başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-165">If hello service partition does not stabilize within hello configured timeout after each fault, hello test fails.</span></span> <span data-ttu-id="7c7a6-166">Merhaba test yalnızca güvenli hataları uygulanmasını.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-166">hello test induces only safe faults.</span></span> <span data-ttu-id="7c7a6-167">Başka bir deyişle, dış hataları olmaması durumunda, bir çekirdek veya veri kaybı değil ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-167">This means that in absence of external failures, a quorum or data loss will not occur.</span></span>

### <a name="important-configuration-options"></a><span data-ttu-id="7c7a6-168">Önemli yapılandırma seçenekleri</span><span class="sxs-lookup"><span data-stu-id="7c7a6-168">Important configuration options</span></span>
* <span data-ttu-id="7c7a6-169">**PartitionSelector**: hedeflenen toobe gereken hello bölümü belirtir Seçici nesnesi.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-169">**PartitionSelector**: Selector object that specifies hello partition that needs toobe targeted.</span></span>
* <span data-ttu-id="7c7a6-170">**TimeToRun**: toplam süre hello test çalışacağı tamamlamadan önce.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-170">**TimeToRun**: Total time that hello test will run before finishing.</span></span>
* <span data-ttu-id="7c7a6-171">**MaxServiceStabilizationTimeout**: saat toowait hello küme toobecome hello test başarısız olmadan önce sağlıklı için en fazla miktarı.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-171">**MaxServiceStabilizationTimeout**: Maximum amount of time toowait for hello cluster toobecome healthy before failing hello test.</span></span> <span data-ttu-id="7c7a6-172">Merhaba gerçekleştirilen denetimlerinin hizmet durumu Tamam olup olduğundan, hello hedef çoğaltma kümesi boyutu tüm bölümler için elde edilir ve hiçbir Inbuild çoğaltmaların mevcut.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-172">hello checks performed are whether service health is OK, hello target replica set size is achieved for all partitions, and no InBuild replicas exist.</span></span>
* <span data-ttu-id="7c7a6-173">**WaitTimeBetweenFaults**: her arıza ve doğrulama döngüsü arasındaki süre toowait miktarı.</span><span class="sxs-lookup"><span data-stu-id="7c7a6-173">**WaitTimeBetweenFaults**: Amount of time toowait between every fault and validation cycle.</span></span>

### <a name="how-toorun-hello-failover-test"></a><span data-ttu-id="7c7a6-174">Nasıl toorun hello yük devretmeyi sınama</span><span class="sxs-lookup"><span data-stu-id="7c7a6-174">How toorun hello failover test</span></span>
<span data-ttu-id="7c7a6-175">**C#**</span><span class="sxs-lookup"><span data-stu-id="7c7a6-175">**C#**</span></span>

```csharp
using System;
using System.Fabric;
using System.Fabric.Testability.Scenario;
using System.Threading;
using System.Threading.Tasks;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");

        Console.WriteLine("Starting Chaos Test Scenario...");
        try
        {
            RunFailoverTestScenarioAsync(clusterConnection, serviceName).Wait();
        }
        catch (AggregateException ae)
        {
            Console.WriteLine("Chaos Test Scenario did not complete: ");
            foreach (Exception ex in ae.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("Chaos Test Scenario completed.");
        return 0;
    }

    static async Task RunFailoverTestScenarioAsync(string clusterConnection, Uri serviceName)
    {
        TimeSpan maxServiceStabilizationTimeout = TimeSpan.FromSeconds(180);
        PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);

        // Create FabricClient with connection and security information here.
        FabricClient fabricClient = new FabricClient(clusterConnection);

        // hello chaos test scenario should run at least 60 minutes or until it fails.
        TimeSpan timeToRun = TimeSpan.FromMinutes(60);
        FailoverTestScenarioParameters scenarioParameters = new FailoverTestScenarioParameters(
          randomPartitionSelector,
          timeToRun,
          maxServiceStabilizationTimeout);

        // Other related parameters:
        // Pause between two iterations for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenIterations = TimeSpan.FromSeconds(30);
        // Pause between concurrent actions for a random duration bound by this value.
        // scenarioParameters.WaitTimeBetweenFaults = TimeSpan.FromSeconds(10);

        // Create hello scenario class and execute it asynchronously.
        FailoverTestScenario failoverScenario = new FailoverTestScenario(fabricClient, scenarioParameters);

        try
        {
            await failoverScenario.ExecuteAsync(CancellationToken.None);
        }
        catch (AggregateException ae)
        {
            throw ae.InnerException;
        }
    }
}
```


<span data-ttu-id="7c7a6-176">**PowerShell**</span><span class="sxs-lookup"><span data-stu-id="7c7a6-176">**PowerShell**</span></span>

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/SampleApp/SampleService"

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindSingleton
```
