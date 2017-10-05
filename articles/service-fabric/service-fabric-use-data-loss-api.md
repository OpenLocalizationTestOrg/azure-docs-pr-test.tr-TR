---
title: "Veri kaybı doku hizmetini çağırmak nasıl | Microsoft Docs"
description: "Veri kaybı kullanmayı açıklar API"
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
ms.openlocfilehash: 0c4791e56f84d0df38783a13c8d8c564fd25f55f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-invoke-data-loss-on-services"></a>Veri kaybı Hizmetleri çağırmak nasıl
> [!WARNING]
> Bu belge, Hizmetleri'nde veri kaybına neden açıklar ve dikkatli kullanılmalıdır.
> 
> 

## <a name="introduction"></a>Giriş
Veri kaybı Service Fabric hizmetinizin arama StartPartitionDataLossAsync() tarafından bir bölüme çağırabilirsiniz.  Bu API, veri kaybı koşullarını neden çalışmaya gerçekleştirmek için arıza ekleme ve analiz hizmeti kullanır.

## <a name="using-the-fault-injection-and-analysis-service"></a>Hata ekleme ve analiz hizmeti kullanılarak
Hata ekleme ve analiz hizmeti şu anda destekler aşağıdaki API'leri grafikte.  Grafiğin sağ tarafında karşılık gelen PowerShell cmdlet'i gösterilmektedir.  Her API her biri hakkında daha fazla bilgi için msdn belgelerine başvurun.

| C# API'Sİ | PowerShell cmdlet'i |
| --- | ---:|
| [StartPartitionDataLossAsync][dl] |[Start-ServiceFabricPartitionDataLoss][psdl] |
| [StartPartitionQuorumLossAsync][ql] |[Start-ServiceFabricPartitionQuorumLoss][psql] |
| [StartPartitionRestartAsync][rp] |[Start-ServiceFabricPartitionRestart][psrp] |

## <a name="conceptual-overview-of-running-a-command"></a>Bir komutu çalıştırmak kavramsal genel bakış
Hata ekleme ve analiz hizmeti kullanır, bu belgedeki "Başlat" API olarak adlandırılan bir API komutuyla başladığınız zaman uyumsuz bir model sonra sonlanma durumuna ulaştı kadar bir "GetProgress" API'sini kullanarak bu komut ilerlemesini denetler veya İptal kadar.
Bir komut başlatmak için karşılık gelen API için "Başlat" API çağrısı.  Bu API döndürdüğü hata ekleme ve analiz hizmet isteğini kabul.  Ancak, bunun ne kadar bir komut çalıştırıldı, göstermez veya henüz başlamamış olsa bile.  Bir komutun ilerleme durumunu denetlemek için "GetProgress" daha önce adı "Başlat" API karşılık gelen API çağrısı.  "GetProgress" API komutu, durum özelliğinin içinde geçerli durumunu gösteren bir nesne döndürür.  Süresiz olarak kadar bir komutu çalıştırır:

1. Başarıyla tamamlanır.  "GetProgress" üzerinde bu durumda çağırırsanız, ilerleme nesnenin durumu tamamlanacaktır.
2. Önemli bir hatayla karşılaşırsa.  "GetProgress" üzerinde bu durumda çağırırsanız, ilerleme nesnenin durumu hatalı
3. Üzerinden iptal [CancelTestCommandAsync] [ cancel] API'sini veya [Stop-ServiceFabricTestCommand] [ cancelps] PowerShell cmdlet'i.  "GetProgress" üzerinde bu durumda çağırırsanız, öğe ilerleme nesnenin durumu bu API için bağımsız değişken bağlı olarak iptal edildi veya ForceCancelled, olacaktır.  Belgelerine bakın [CancelTestCommandAsync] [ cancel] daha fazla ayrıntı için.

## <a name="details-of-running-a-command"></a>Bir komut çalışan ayrıntıları
Bir komut başlatmak için Başlat API beklenen bağımsız değişkenlerle çağırın.  Tüm Başlat API'leri Operationıd adlı bir GUID bağımsız değişkeni vardır.  Operationıd bağımsız değişkeni, bu komut ilerlemesini izlemek için kullanıldığından izlemek.  Bu "GetProgress" API komut ilerlemesini izlemek için geçirilmelidir.  Operationıd benzersiz olması gerekir.

Başlangıç API başarıyla çağrıldıktan sonra döndürülen ilerleme nesnesinin State özelliği tamamlanana kadar GetProgress API bir döngüde çağrılmalıdır.  Tüm [FabricTransientException'ın] [ fte] ve OperationCanceledException'ın yeniden.
Komutu (tamamlandı, Faulted veya iptal edildi) terminal durumuna ulaştı, döndürülen ilerleme nesnenin sonuç özelliği ek bilgi gerekir.  Durum tamamlanmışsa Result.SelectedPartition.PartitionId seçilmedi bölüm kimliği içerir.  Result.Exception null olur.  Durumu hatalı Result.Exception hata ekleme neden olacaktır ve analiz hizmeti komutu hatalı.  Result.SelectedPartition.PartitionId seçilmedi bölüm kimliği gerekir.  Bazı durumlarda, komut yetecek kadar bir bölümü seçmek için proceeded değil.  Bu durumda, PartitionID 0 olacaktır.  Durumu iptal edilirse, Result.Exception null olur.  Faulted durum gibi Result.SelectedPartition.PartitionId seçildi bölüm kimliği vardır, ancak komut yetecek kadar bunu yapmak için proceeded değil, 0 olacaktır.  Lütfen ayrıca aşağıdaki örneğe bakın.

Aşağıdaki örnek kod, başlayın sonra belirli bir bölüme veri kaybına neden bir komutla ilgili ilerleme durumunu denetleme gösterilmektedir.

```csharp
    static async Task PerformDataLossSample()
    {
        // Create a unique operation id for the command below
        Guid operationId = Guid.NewGuid();

        // Note: Use the appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // The name of the target service
        Uri targetServiceName = new Uri("fabric:/MyService");

        // The id of the target partition inside the target service
        Guid targetPartitionId = new Guid("00000000-0000-0000-0000-000002233445");

        PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(targetServiceName, targetPartitionId);

        // Start the command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means the Fault Injection and Analysis Service has saved the intent to perform this work.  It does not say anything about the progress
        // of the command.
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

        // Poll the progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // the command won't be cancelled.        

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

                // In a terminal state .Result.SelectedPartition.PartitionId will have the chosen partition
                Console.WriteLine("  Printing selected partition='{0}'", progress.Result.SelectedPartition.PartitionId);
                break;
            }
            else if (progress.State == TestCommandProgressState.Faulted)
            {
                // If State is Faulted, the progress object's Result property's Exception property will have the reason why.
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

Aşağıdaki örnek belirtilen bir hizmeti rastgele bir bölümü seçmek için PartitionSelector kullanmayı gösterir:

```csharp
    static async Task PerformDataLossUseSelectorSample()
    {
        // Create a unique operation id for the command below
        Guid operationId = Guid.NewGuid();

        // Note: Use the appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // The name of the target service
        Uri targetServiceName = new Uri("fabric:/SampleService ");

        // Use a PartitionSelector that will have the Fault Injection and Analysis Service choose a random partition of “targetServiceName”
        PartitionSelector partitionSelector = PartitionSelector.RandomOf(targetServiceName);

        // Start the command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means the Fault Injection and Analysis Service has saved the intent to perform this work.  It does not say anything about the progress
        // of the command.
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

        // Poll the progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // the command won't be cancelled.

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
                // If State is Faulted, the progress object's Result property's Exception property will have the reason why.
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
Bir komut terminal durumuna ulaştı sonra meta verilerini alanından tasarruf etmek için kaldırılacak önce belirli bir süre için arıza ekleme ve analiz hizmeti kalır.  "GetProgress" kaldırıldıktan sonra bir komut Operationıd kullanarak çağrılırsa, bir hata kodu KeyNotFound ile FabricException döndürür.

[dl]: https://msdn.microsoft.com/library/azure/mt693569.aspx
[ql]: https://msdn.microsoft.com/library/azure/mt693558.aspx
[rp]: https://msdn.microsoft.com/library/azure/mt645056.aspx
[psdl]: https://msdn.microsoft.com/library/mt697573.aspx
[psql]: https://msdn.microsoft.com/library/mt697557.aspx
[psrp]: https://msdn.microsoft.com/library/mt697560.aspx
[cancel]: https://msdn.microsoft.com/library/azure/mt668910.aspx
[cancelps]: https://msdn.microsoft.com/library/mt697566.aspx
[fte]: https://msdn.microsoft.com/library/azure/system.fabric.fabrictransientexception.aspx
