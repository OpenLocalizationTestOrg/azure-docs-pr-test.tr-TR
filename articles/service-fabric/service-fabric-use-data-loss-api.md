---
title: "aaaHow tooInvoke Service Fabric Hizmetleri veri kaybı | Microsoft Docs"
description: "Nasıl toouse hello veri kaybı açıklar API"
services: service-fabric
documentationcenter: .net
author: LMWF
manager: rsinha
editor: 
ms.assetid: f4e70f6f-cad9-4a3e-9655-009b4db09c6d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 09/19/2016
ms.author: lemai
redirect_url: /azure/service-fabric/service-fabric-testability-overview
ms.openlocfilehash: 014c7ebfd2c42d79a5fe1802ecc3fa0c1f26f9d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinvoke-data-loss-on-services"></a>Nasıl tooInvoke Hizmetleri veri kaybı
> [!WARNING]
> Bu belgeyi açıklayan nasıl hizmetlerinizi, toocause veri kaybına ve dikkatli kullanılmalıdır.
> 
> 

## <a name="introduction"></a>Giriş
Veri kaybı Service Fabric hizmetinizin arama StartPartitionDataLossAsync() tarafından bir bölüme çağırabilirsiniz.  Bu API hello hata ekleme ve analiz hizmeti tooperform hello iş toocause veri kaybı koşullarını kullanır.

## <a name="using-hello-fault-injection-and-analysis-service"></a>Merhaba hata ekleme ve analiz hizmeti kullanılarak
Merhaba hata ekleme ve analiz hizmeti aşağıdaki hello grafik API'leri aşağıdaki hello şu anda destekler.  Merhaba grafik Hello sağ tarafındaki hello karşılık gelen PowerShell cmdlet'ini gösterir.  Her biri hakkında daha fazla bilgi için lütfen her API toohello msdn belgelerine başvurun.

| C# API'Sİ | PowerShell cmdlet'i |
| --- | ---:|
| [StartPartitionDataLossAsync][dl] |[Start-ServiceFabricPartitionDataLoss][psdl] |
| [StartPartitionQuorumLossAsync][ql] |[Start-ServiceFabricPartitionQuorumLoss][psql] |
| [StartPartitionRestartAsync][rp] |[Start-ServiceFabricPartitionRestart][psrp] |

## <a name="conceptual-overview-of-running-a-command"></a>Bir komutu çalıştırmak kavramsal genel bakış
Merhaba başladığınız zaman uyumsuz bir model tooas hello "Başlat" API sonra denetimleri hello ilerlemesini terminal ulaştı kadar "GetProgress" API'sini kullanarak bu komut, bu belgedeki başvurulan bir API ile komutu Hata ekleme ve analiz hizmeti kullanan hello durum, ya da size kadar iptal edin.
toostart bir komut hello karşılık gelen API için hello "Başlat" API çağrısı.  Bu API hello hata ekleme ve analiz hizmeti hello isteği kabul döndürür.  Ancak, bunun ne kadar bir komut çalıştırıldı, göstermez veya henüz başlamamış olsa bile.  Sipariş toocheck ediyor komut, hello "GetProgress" toohello "Başlat" API önceden adlı karşılık gelen API çağrısı.  Merhaba "GetProgress" API hello hello komutu, durum özelliğinin içinde geçerli durumunu gösteren bir nesne döndürür.  Süresiz olarak kadar bir komutu çalıştırır:

1. Başarıyla tamamlanır.  "GetProgress" üzerinde bu durumda çağırırsanız, hello ilerleme nesnenin durumu tamamlanacaktır.
2. Önemli bir hatayla karşılaşırsa.  "GetProgress" üzerinde bu durumda çağırırsanız, hello ilerleme nesnenin durumu hatalı
3. Merhaba iptal [CancelTestCommandAsync] [ cancel] API, veya [Stop-ServiceFabricTestCommand] [ cancelps] PowerShell cmdlet'i.  "GetProgress" üzerinde bu durumda çağırırsanız, hello ilerleme nesnenin durumu iptal edildi veya ForceCancelled, bir bağımsız değişken toothat API bağlı olacaktır.  Merhaba belgelerine bakın [CancelTestCommandAsync] [ cancel] daha fazla ayrıntı için.

## <a name="details-of-running-a-command"></a>Bir komut çalışan ayrıntıları
Sipariş toostart bir komutu, beklenen hello bağımsız değişkenlerle hello Başlat API çağırın.  Tüm Başlat API'leri Operationıd adlı bir GUID bağımsız değişkeni vardır.  Merhaba Operationıd bağımsız değişkeni, kullanıldığından kaydını tutabilirsiniz tootrack ilerleme durumunu bu komutu.  Merhaba hello komutunun sipariş tootrack Sürüyor "GetProgress" API uygulamasına geçirilmelidir.  Merhaba Operationıd benzersiz olması gerekir.

Başarılı bir şekilde hello API, başlatma ilerleme hello döndürülen kadar bir döngüde GetProgress API çağrılmalıdır hello çağrıldıktan sonra nesnesinin State özelliği tamamlandı.  Tüm [FabricTransientException'ın] [ fte] ve OperationCanceledException'ın yeniden.
Merhaba komutu (tamamlandı, Faulted veya iptal edildi) terminal durumuna ulaştı, ilerleme nesnenin sonuç özelliği ek bilgi gerekir hello döndürdü.  Merhaba durumu tamamlanmışsa Result.SelectedPartition.PartitionId seçilmedi hello bölüm kimliği içerir.  Result.Exception null olur.  Merhaba durumu hatalı, Result.Exception hello neden hello hata ekleme ve analiz hatalı hizmet hello komutu yüklemeniz gerekir.  Result.SelectedPartition.PartitionId seçilmedi hello bölüm kimliği gerekir.  Bazı durumlarda, hello komutu şu ana kadar yeterli toochoose bir bölüm proceeded değil.  Bu durumda, hello PartitionID 0 olacaktır.  Merhaba durumu iptal edilirse, Result.Exception null olur.  Hello Faulted çalışması gibi Result.SelectedPartition.PartitionId seçildi hello bölüm kimliği vardır, ancak hello komutu şu ana kadar yeterli toodo şekilde proceeded değil, 0 olacaktır.  Lütfen aşağıdaki toohello örneği de bakın.

Aşağıdaki Hello örnek kodu nasıl toostart sonra Denetle komutu toocause veri kaybı belirli bir bölüme ilerlemesini gösterir.

```csharp
    static async Task PerformDataLossSample()
    {
        // Create a unique operation id for hello command below
        Guid operationId = Guid.NewGuid();

        // Note: Use hello appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // hello name of hello target service
        Uri targetServiceName = new Uri("fabric:/MyService");

        // hello id of hello target partition inside hello target service
        Guid targetPartitionId = new Guid("00000000-0000-0000-0000-000002233445");

        PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(targetServiceName, targetPartitionId);

        // Start hello command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means hello Fault Injection and Analysis Service has saved hello intent tooperform this work.  It does not say anything about hello progress
        // of hello command.
        while (true)
        {
            try
            {
                await fabricClient.TestManager.StartPartitionDataLossAsync(operationId, partitionSelector, DataLossMode.FullDataLoss).ConfigureAwait(false);
                break;
            }
            catch (OperationCanceledException)
            {
            }
            catch (FabricTransientException)
            {
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }

        PartitionDataLossProgress progress = null;

        // Poll hello progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // hello command won't be cancelled.        

        while (true)
        {
            try
            {
                progress = await fabricClient.TestManager.GetPartitionDataLossProgressAsync(operationId).ConfigureAwait(false);
            }
            catch (OperationCanceledException)
            {
                continue;
            }
            catch (FabricTransientException)
            {
                continue;
            }

            if (progress.State == TestCommandProgressState.Completed)
            {
                Console.WriteLine("Command '{0}' completed successfully", operationId);

                // In a terminal state .Result.SelectedPartition.PartitionId will have hello chosen partition
                Console.WriteLine("  Printing selected partition='{0}'", progress.Result.SelectedPartition.PartitionId);
                break;
            }
            else if (progress.State == TestCommandProgressState.Faulted)
            {
                // If State is Faulted, hello progress object's Result property's Exception property will have hello reason why.
                Console.WriteLine("Command '{0}' failed with '{1}'", operationId, progress.Result.Exception);
                break;
            }
            else
            {
                Console.WriteLine("Command '{0}' is currently Running", operationId);
            }

            await Task.Delay(TimeSpan.FromSeconds(5.0d)).ConfigureAwait(false);
        }
    }
```

Aşağıdaki Hello örneği nasıl toouse hello PartitionSelector toochoose belirtilen bir hizmeti rastgele bir bölümünü gösterir:

```csharp
    static async Task PerformDataLossUseSelectorSample()
    {
        // Create a unique operation id for hello command below
        Guid operationId = Guid.NewGuid();

        // Note: Use hello appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // hello name of hello target service
        Uri targetServiceName = new Uri("fabric:/SampleService ");

        // Use a PartitionSelector that will have hello Fault Injection and Analysis Service choose a random partition of “targetServiceName”
        PartitionSelector partitionSelector = PartitionSelector.RandomOf(targetServiceName);

        // Start hello command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means hello Fault Injection and Analysis Service has saved hello intent tooperform this work.  It does not say anything about hello progress
        // of hello command.
        while (true)
        {
            try
            {
                await fabricClient.TestManager.StartPartitionDataLossAsync(operationId, partitionSelector, DataLossMode.FullDataLoss).ConfigureAwait(false);
                break;
            }
            catch (OperationCanceledException)
            {
            }
            catch (FabricTransientException)
            {
            }
            catch (Exception e)
            {
                Console.WriteLine("Unexpected exception '{0}'", e);
                throw;
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }

        PartitionDataLossProgress progress = null;

        // Poll hello progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // hello command won't be cancelled.

        while (true)
        {
            try
            {
                progress = await fabricClient.TestManager.GetPartitionDataLossProgressAsync(operationId).ConfigureAwait(false);
            }
            catch (OperationCanceledException)
            {
                continue;
            }
            catch (FabricTransientException)
            {
                continue;
            }

            if (progress.State == TestCommandProgressState.Completed)
            {
                Console.WriteLine("Command '{0}' completed successfully", operationId);

                Console.WriteLine("Printing progress.Result:");
                Console.WriteLine("  Printing selected partition='{0}'", progress.Result.SelectedPartition.PartitionId);

                break;
            }
            else if (progress.State == TestCommandProgressState.Faulted)
            {
                // If State is Faulted, hello progress object's Result property's Exception property will have hello reason why.
                Console.WriteLine("Command '{0}' failed with '{1}', SelectedPartition {2}", operationId, progress.Result.Exception, progress.Result.SelectedPartition);
                break;
            }
            else
            {
                Console.WriteLine("Command '{0}' is currently Running", operationId);
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }
    }
```

## <a name="history-and-truncation"></a>Geçmiş ve kesme
Bir komut terminal durumuna ulaştı sonra meta verilerini hello hata ekleme kalır ve toosave alanı olacak önce belirli bir süre için analiz hizmetlerini kaldırıldı.  "GetProgress" Merhaba Operationıd komut kaldırıldıktan sonra kullanarak çağrılırsa, bir hata kodu KeyNotFound ile FabricException döndürür.

[dl]: https://msdn.microsoft.com/library/azure/mt693569.aspx
[ql]: https://msdn.microsoft.com/library/azure/mt693558.aspx
[rp]: https://msdn.microsoft.com/library/azure/mt645056.aspx
[psdl]: https://msdn.microsoft.com/library/mt697573.aspx
[psql]: https://msdn.microsoft.com/library/mt697557.aspx
[psrp]: https://msdn.microsoft.com/library/mt697560.aspx
[cancel]: https://msdn.microsoft.com/library/azure/mt668910.aspx
[cancelps]: https://msdn.microsoft.com/library/mt697566.aspx
[fte]: https://msdn.microsoft.com/library/azure/system.fabric.fabrictransientexception.aspx
