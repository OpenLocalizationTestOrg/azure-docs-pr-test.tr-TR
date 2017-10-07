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
# <a name="testability-scenarios"></a>Test Edilebilirlik senaryoları
Bulut altyapılarının doğası gereği güvenilir gibi büyük dağıtılan sistemlerde. Azure Service Fabric verir geliştiriciler hello özelliği toowrite Hizmetleri toorun güvenilmez altyapılar üstünde. Sipariş toowrite yüksek kaliteli Hizmetleri'nde geliştiricilerin kendi Hizmetleri gibi güvenilmeyen altyapı tootest hello kararlılığını toobe mümkün tooinduce gerekir.

Merhaba hata analizi hizmeti geliştiricilere hataları hello bulunması hello özelliği tooinduce hata eylemleri tootest hizmetleri sağlar. Ancak, hedeflenen benzetimli hataları yalnızca o ana kadarki alırsınız. Ayrıca, sınama tootake hello Service Fabric hello test senaryoları kullanabilirsiniz: chaos test ve bir yük devretme testi. Bu senaryolar, normal ve durunda hello küme üzerinden uzun süre boyunca sürekli araya eklemeli hataları benzetimi. Bir test hello oranı ve hataları tür ile yapılandırıldıktan sonra ya da C# API'leri veya PowerShell, hello kümedeki toogenerate hataları ve hizmet başlatılabilir.

> [!WARNING]
> ChaosTestScenario daha esnektir, hizmet tabanlı Chaos tarafından değiştirilmektedir. Lütfen toohello yeni makale başvurun [denetlenen Chaos](service-fabric-controlled-chaos.md) daha fazla ayrıntı için.
> 
> 

## <a name="chaos-test"></a>Chaos test
Merhaba chaos senaryo hello tüm Service Fabric kümesi arasında hataları oluşturur. Merhaba senaryo genellikle birkaç saat ay veya yıl tooa görülen hataları sıkıştırır. Merhaba yüksek hata oranı araya eklemeli hataları Hello birleşimi aksi eksik köşe durumları bulur. Bu tooa önemli iyileştirme hello kod hello hizmet kalitesi yol açar.

### <a name="faults-simulated-in-hello-chaos-test"></a>Merhaba chaos testinde benzetimli hataları
* Bir düğümü yeniden başlatın
* Dağıtılmış kod paketi yeniden başlatın
* Bir yineleme kaldırma
* Bir çoğaltmayı yeniden başlatın
* (İsteğe bağlı) birincil kopya taşıma
* (İsteğe bağlı) bir ikincil çoğaltma taşıma

Hello chaos test hataları birden çok kez çalışır ve küme doğrulama hello için belirtilen süre. Merhaba küme toostabilize ve doğrulama toosucceed hello zamanın de yapılandırılabilir. tek bir küme doğrulama hatasına isabet hello senaryo başarısız oluyor.

Örneğin, bir saat en fazla üç eşzamanlı hataları toorun bir test kümesi göz önünde bulundurun. Merhaba test üç hataları anlamına ve hello küme durumunu doğrulamak. Merhaba test hello önceki adıma hello küme bozulur veya bir saat geçirir kadar yineleme. Merhaba küme her yinelemede bozulursa, yani, yapılandırılan süre içinde Sabitle değil, hello test bir özel durum ile başarısız olur. Bu durum, bir şeyler yanlış geçti ve daha fazla araştırma gerekiyor gösterir.

Mevcut haliyle hello hataya nesil hello chaos test altyapısında yalnızca güvenli hataları uygulanmasını. Başka bir deyişle, dış hatalarının hello olmaması durumunda, bir çekirdek veya veri kaybı asla meydana gelmez.

### <a name="important-configuration-options"></a>Önemli yapılandırma seçenekleri
* **TimeToRun**: toplam süre hello test çalışacağı ile başarılı tamamlamadan önce. Merhaba test daha önce bir doğrulama hatası yerine bitirebilirsiniz.
* **MaxClusterStabilizationTimeout**: saat toowait hello küme toobecome hello test başarısız olmadan önce sağlıklı için en fazla miktarı. Merhaba gerçekleştirilen denetimlerinin küme durumu Tamam olup olduğundan, hizmet durumu Tamam olduğunu, hello hedef çoğaltma kümesi boyutu hello hizmet bölüm için elde edilir ve hiçbir Inbuild çoğaltmaların mevcut.
* **MaxConcurrentFaults**: en fazla eş zamanlı hatalarının sayısı her yinelemede kopyaladığınızda. daha yüksek hello sayı Merhaba, bu nedenle daha karmaşık yük devretme ve geçiş birleşimleri kaynaklanan daha agresif hello test hello. Merhaba test dış hataları olmaması durumunda olmayacaktır, bu yapılandırmanın nasıl yüksek olan yedeklemiş çekirdek veya veri kaybı güvence altına alır.
* **EnableMoveReplicaFaults**: etkinleştirir ya da birincil veya ikincil çoğaltmaları hello hello taşınmasına neden olan hello hataları devre dışı bırakır. Bu hataları varsayılan olarak devre dışıdır.
* **WaitTimeBetweenIterations**: gidiş hataları ve karşılık gelen doğrulama sonra yani yinelemeleri arasındaki zaman toowait miktarı.

### <a name="how-toorun-hello-chaos-test"></a>Test nasıl toorun hello chaos
C# örneği

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

PowerShell

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```


## <a name="failover-test"></a>Yük devretme testi
Merhaba yük devretme testi senaryosu, belirli hizmet bölüm hedefler hello chaos testi senaryosu sürümüdür. Yük devretme hello etkisini belirli hizmet bölümdeki hello diğer hizmetler etkilenmemesini bırakarak sınar. Merhaba hedef bölüm bilgileri ve diğer parametreler ile yapılandırıldıktan sonra hizmet bölüm için C# API'leri veya PowerShell toogenerate hataları kullanan bir istemci-tarafı araç olarak çalışır. İş mantığınızın bir iş yükü hello yan tooprovide üzerinde çalışırken hello senaryo bir dizi benzetimli hataları ve hizmet doğrulama yineler. Bir hizmet doğrulama hatası daha fazla araştırma gereken bir sorun olduğunu gösterir.

### <a name="faults-simulated-in-hello-failover-test"></a>Merhaba yük devretme testi benzetimli hataları
* Merhaba bölüm barındırıldığı dağıtılmış kod paketi yeniden başlatın
* Bir birincil/ikincil çoğaltma veya durum bilgisiz örneğini Kaldır
* Birincil ve ikincil bir çoğaltma (bir kalıcı hizmeti) yeniden Başlat
* Birincil çoğaltma taşıma
* Bir ikincil çoğaltma taşıma
* Merhaba bölümü yeniden başlatın

Merhaba yük devretme testi seçilen hataya uygulanmasını ve ardından doğrulama hello hizmet tooensure üzerinde kendi kararlılık çalıştırır. birden çok hataları hello chaos test zaman, karşılıklı olarak toopossible sırasında bir hata yalnızca hello yük devretme testi uygulanmasını. Merhaba hizmet bölüm sonra her hata hello yapılandırılmış zaman aşımı süresi içinde Sabitle değil hello sınama başarısız olur. Merhaba test yalnızca güvenli hataları uygulanmasını. Başka bir deyişle, dış hataları olmaması durumunda, bir çekirdek veya veri kaybı değil ortaya çıkar.

### <a name="important-configuration-options"></a>Önemli yapılandırma seçenekleri
* **PartitionSelector**: hedeflenen toobe gereken hello bölümü belirtir Seçici nesnesi.
* **TimeToRun**: toplam süre hello test çalışacağı tamamlamadan önce.
* **MaxServiceStabilizationTimeout**: saat toowait hello küme toobecome hello test başarısız olmadan önce sağlıklı için en fazla miktarı. Merhaba gerçekleştirilen denetimlerinin hizmet durumu Tamam olup olduğundan, hello hedef çoğaltma kümesi boyutu tüm bölümler için elde edilir ve hiçbir Inbuild çoğaltmaların mevcut.
* **WaitTimeBetweenFaults**: her arıza ve doğrulama döngüsü arasındaki süre toowait miktarı.

### <a name="how-toorun-hello-failover-test"></a>Nasıl toorun hello yük devretmeyi sınama
**C#**

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


**PowerShell**

```powershell
$connection = "localhost:19000"
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/SampleApp/SampleService"

Connect-ServiceFabricCluster $connection

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindSingleton
```
