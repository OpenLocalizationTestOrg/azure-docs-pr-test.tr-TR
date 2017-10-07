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
# <a name="induce-controlled-chaos-in-service-fabric-clusters"></a>Service Fabric kümelerinde denetimli Chaos anlamına
Bulut altyapılarının doğası gereği güvenilir gibi büyük ölçekli dağıtılmış sistemler. Azure Service Fabric geliştiriciler toowrite güvenilir dağıtılmış hizmet güvenilir olmayan bir altyapının en üstünde sağlar. toowrite sağlam dağıtılmış hizmetlerini güvenilir olmayan bir altyapının en üstünde, geliştiricilerin gerekir toobe mümkün tootest hello hizmetlerini kararlılığını güvenilmez altyapısını temel hello karmaşık durumu geçişleri giderek sırada son toofaults.

Merhaba [hata ekleme ve küme analiz hizmeti](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-testability-overview) (olarak da bilinen hata analizi hizmeti hello) imkanı geliştiriciler hello tooinduce hizmetlerini tootest hataları. Bunlar hedeflenen gibi hataları, benzetimli [bir bölümü yeniden](https://docs.microsoft.com/en-us/powershell/module/servicefabric/start-servicefabricpartitionrestart?view=azureservicefabricps), hello en yaygın durumu geçişleri çalışma yardımcı olabilir. Ancak hedeflenen benzetimli hataları tanımına göre ağırlıklı ve böylece kaçırabilir gösteren yedekleme yalnızca sabit tahmin, uzun ve karmaşık sırası durumu geçişleri içinde hataları. Bir taraflı olmayan test etmek için Chaos kullanabilirsiniz.

Chaos uzun süreler boyunca hello küme boyunca düzenli, araya eklemeli hataları (normal ve durunda) benzetimini yapar. Merhaba oranı ve hataları hello tür Chaos yapılandırdıktan sonra hataları hello küme ve hizmetlerinizi oluşturma C# veya Powershell API'si toostart aracılığıyla Chaos başlatabilirsiniz. Daha sonra durdurur Chaos otomatik olarak, belirli bir süre için (örneğin, bir saat), Chaos toorun yapılandırabilir ya da StopChaos API (C# veya Powershell) toostop çağırabilirsiniz, dilediğiniz zaman.

> [!NOTE]
> Mevcut haliyle Chaos yalnızca güvenli hataları, dış hataları hello olmaması durumunda bir çekirdek kayıp veya veri kaybı hiçbir zaman oluştuğunu gelir uygulanmasını.
>

Chaos çalışırken hello şu anda çalıştırmak hello hello durumunu yakalama farklı olayları üretir. Örneğin, bir ExecutingFaultsEvent Chaos bu yineleme tooexecute karar verdiği tüm hello hataları içerir. Bir ValidationFailedEvent hello küme hello doğrulama sırasında bulundu bir doğrulama hatası (sistem durumu veya kararlılık sorunları) hello ayrıntılarını içerir. Merhaba GetChaosReport API (C# veya Powershell) tooget hello rapor Chaos çalıştırılan çağırabilirsiniz. Bu olaylar kalıcı bir [güvenilir sözlük](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-reliable-services-reliable-collections), iki yapılandırmaları tarafından dikte kesilmesi ilkesi vardır: **MaxStoredChaosEventCount** (varsayılan değer olan 25000) ve **StoredActionCleanupIntervalInSeconds** (varsayılan değer olan 3600). Her *StoredActionCleanupIntervalInSeconds* Chaos denetler ve tüm ancak hello en son *MaxStoredChaosEventCount* olayları hello güvenilir sözlükten temizlendi.

## <a name="faults-induced-in-chaos"></a>İçinde Chaos kopyaladığınızda hataları
Chaos hello tüm Service Fabric kümesi arasında hataları oluşturur ve ay veya yıl birkaç saat görülür hataları sıkıştırır. Merhaba yüksek hata oranı araya eklemeli hataları Hello birleşimi aksi atlanabilir köşe durumları bulur. Bu alıştırmada karmaşık dünyada tooa önemli iyileştirme hello kod hello hizmet kalitesi yol açar.

Chaos hataları kategorileri aşağıdaki hello gelen uygulanmasını:

* Bir düğümü yeniden başlatın
* Dağıtılmış kod paketi yeniden başlatın
* Bir yineleme kaldırma
* Bir çoğaltmayı yeniden başlatın
* Bir birincil çoğaltmayı (yapılandırılabilir) taşıma
* Bir ikincil çoğaltma (yapılandırılabilir) taşıma

Chaos içinde birden çok kez çalışır. Her bir yineleme hataları oluşur ve hello için küme doğrulama period belirtildi. Merhaba küme toostabilize ve doğrulama toosucceed hello zamanın yapılandırabilirsiniz. Küme doğrulama hata bulunursa, Chaos oluşturur ve ValidationFailedEvent hello UTC zaman damgası ve hello hata ayrıntıları ile devam ettirir. Örneğin, bir saat en fazla üç eşzamanlı hataları için ayarlanmış bir toorun karmaşık dünyada örneği göz önünde bulundurun. Chaos üç hataları uygulanmasını ve hello küme durumu doğrular. Merhaba önceki açıkça hello StopChaosAsync API aracılığıyla durdurulmuş veya bir saatlik olana kadar adım geçirir yineler. Her yinelemede Hello küme bozulursa (diğer bir deyişle, bu MaxClusterStabilizationTimeout içinde geçirilen hello içinde Sabitle değil), Chaos bir ValidationFailedEvent oluşturur. Bu olay, bir şeyler yanlış geçti ve daha fazla araştırma gerekebilir gösterir.

kopyaladığınızda Chaos hataları tooget GetChaosReport API (powershell veya C#) kullanabilirsiniz. Merhaba API hello sonraki kesimini hello Chaos raporunun hello geçilen devamlılık belirteci veya hello geçen zaman aralığı temel alır. ContinuationToken tooget hello sonraki kesimin hello Chaos rapor hello veya StartTimeUtc ve EndTimeUtc aracılığıyla hello zaman aralığını belirtebilirsiniz, ancak hello hello ContinuationToken ve hello zaman aralığı belirtemezsiniz ya da belirtebilirsiniz aynı çağrısı. 100'den fazla Chaos olayları olduğunda hello Chaos rapor, en fazla 100 Chaos olay kesimi içerdiği segmentlerinde döndürülür.

## <a name="important-configuration-options"></a>Önemli yapılandırma seçenekleri
* **TimeToRun**: toplam saat Chaos çalıştıran ile başarılı tamamlanmadan önce. Merhaba StopChaos API hello TimeToRun boyunca çalıştıktan önce Chaos durdurabilirsiniz.

* **MaxClusterStabilizationTimeout**: hello maksimum hello küme toobecome bir ValidationFailedEvent oluşturan önce sağlıklı zaman toowait miktarı. Bu kurtarma sırasında bu bekleme tooreduce hello hello kümede yüktür. gerçekleştirilen hello denetimleri şunlardır:
  * Merhaba küme durumu Tamam ise
  * Merhaba hizmet durumu Tamam ise
  * Merhaba hedef çoğaltma kümesi boyutu, hello hizmet bölüm için elde edilir
  * Hiçbir Inbuild çoğaltmaların var
* **MaxConcurrentFaults**: Merhaba her yinelemede kopyaladığınızda eşzamanlı hataları maksimum sayısı. Merhaba yüksek hello sayı, hello daha agresif Chaos olduğundan ve küme hello hello yük devretme ve hello durumu geçişi birleşimler geçtiği ayrıca daha karmaşıktır. 

> [!NOTE]
> Ne olursa olsun nasıl yüksek bir değer *MaxConcurrentFaults* varsa, Chaos - dış hataları - hello olmaması durumunda çekirdek kayıp veya veri kaybı yoktur güvence altına alır.
>

* **EnableMoveReplicaFaults**: etkinleştirir veya hello birincil veya ikincil çoğaltmaları toomove neden hello hataları devre dışı bırakır. Bu hataları varsayılan olarak devre dışıdır.
* **WaitTimeBetweenIterations**: yinelemeleri arasındaki zaman toowait hello miktarı. Diğer bir deyişle, Chaos gidiş hataları ve hello karşılık gelen hello küme hello durumunu doğrulanması tamamlandı yürütüldükten sonra duraklatma süreyi hello. Merhaba hello değer arttıkça hello daha düşük olan hello ortalama hata ekleme oranı.
* **WaitTimeBetweenFaults**: tek bir yineleme iki ardışık hataları arasında zaman toowait hello miktarı. Merhaba daha yüksek hello değeri, daha düşük hello eşzamanlılığı hello (veya hello arasında örtüşme) hataları.
* **ClusterHealthPolicy**: küme sistem durumu ilkesi kullanılan toovalidate hello Chaos yineleme Between hello küme durumunu olduğunu. Merhaba küme sistem durumu hatası veya hataya yürütme sırasında beklenmeyen bir özel durum oluşursa, Chaos hello sonraki sistem durumu denetimi - bazı zaman toorecuperate tooprovide hello kümeyle önce 30 dakika bekler.
* **Bağlam**: (dize, dize) koleksiyonunu anahtar-değer çiftlerini yazın. Merhaba eşlemesi kullanılan toorecord hello Chaos çalıştırma hakkında bilgi olabilir. Bu tür çiftleri 100'den fazla olamaz ve her bir dize (anahtar veya değer) en fazla 4095 karakterden uzun olamaz. Bu haritada hello çalıştırmak Chaos toooptionally deposu hello bağlamının hello belirli çalıştırma hakkında hello başlatıcı tarafından ayarlanır.

## <a name="how-toorun-chaos"></a>Nasıl toorun Chaos

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
