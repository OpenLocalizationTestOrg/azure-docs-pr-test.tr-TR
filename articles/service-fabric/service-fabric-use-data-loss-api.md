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
# <a name="how-to-invoke-data-loss-on-services"></a><span data-ttu-id="a8b11-103">Veri kaybı Hizmetleri çağırmak nasıl</span><span class="sxs-lookup"><span data-stu-id="a8b11-103">How to Invoke Data Loss on Services</span></span>
> [!WARNING]
> <span data-ttu-id="a8b11-104">Bu belge, Hizmetleri'nde veri kaybına neden açıklar ve dikkatli kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a8b11-104">This document describe how to cause data loss in your services, and should be used with care.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="a8b11-105">Giriş</span><span class="sxs-lookup"><span data-stu-id="a8b11-105">Introduction</span></span>
<span data-ttu-id="a8b11-106">Veri kaybı Service Fabric hizmetinizin arama StartPartitionDataLossAsync() tarafından bir bölüme çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a8b11-106">You can invoke data loss on a partition of your Service Fabric Service by calling StartPartitionDataLossAsync().</span></span>  <span data-ttu-id="a8b11-107">Bu API, veri kaybı koşullarını neden çalışmaya gerçekleştirmek için arıza ekleme ve analiz hizmeti kullanır.</span><span class="sxs-lookup"><span data-stu-id="a8b11-107">This api uses the Fault Injection and Analysis Service to perform the work to cause data loss conditions.</span></span>

## <a name="using-the-fault-injection-and-analysis-service"></a><span data-ttu-id="a8b11-108">Hata ekleme ve analiz hizmeti kullanılarak</span><span class="sxs-lookup"><span data-stu-id="a8b11-108">Using the Fault Injection and Analysis Service</span></span>
<span data-ttu-id="a8b11-109">Hata ekleme ve analiz hizmeti şu anda destekler aşağıdaki API'leri grafikte.</span><span class="sxs-lookup"><span data-stu-id="a8b11-109">The Fault Injection and Analysis Service currently supports the following APIs in the chart below.</span></span>  <span data-ttu-id="a8b11-110">Grafiğin sağ tarafında karşılık gelen PowerShell cmdlet'i gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a8b11-110">The right side of the chart shows the corresponding PowerShell cmdlet.</span></span>  <span data-ttu-id="a8b11-111">Her API her biri hakkında daha fazla bilgi için msdn belgelerine başvurun.</span><span class="sxs-lookup"><span data-stu-id="a8b11-111">Please refer to the msdn documentation on each API for more information on each one.</span></span>

| <span data-ttu-id="a8b11-112">C# API'Sİ</span><span class="sxs-lookup"><span data-stu-id="a8b11-112">C# API</span></span> | <span data-ttu-id="a8b11-113">PowerShell cmdlet'i</span><span class="sxs-lookup"><span data-stu-id="a8b11-113">PowerShell Cmdlet</span></span> |
| --- | ---:|
| <span data-ttu-id="a8b11-114">[StartPartitionDataLossAsync][dl]</span><span class="sxs-lookup"><span data-stu-id="a8b11-114">[StartPartitionDataLossAsync][dl]</span></span> |<span data-ttu-id="a8b11-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span><span class="sxs-lookup"><span data-stu-id="a8b11-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span></span> |
| <span data-ttu-id="a8b11-116">[StartPartitionQuorumLossAsync][ql]</span><span class="sxs-lookup"><span data-stu-id="a8b11-116">[StartPartitionQuorumLossAsync][ql]</span></span> |<span data-ttu-id="a8b11-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span><span class="sxs-lookup"><span data-stu-id="a8b11-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span></span> |
| <span data-ttu-id="a8b11-118">[StartPartitionRestartAsync][rp]</span><span class="sxs-lookup"><span data-stu-id="a8b11-118">[StartPartitionRestartAsync][rp]</span></span> |<span data-ttu-id="a8b11-119">[Start-ServiceFabricPartitionRestart][psrp]</span><span class="sxs-lookup"><span data-stu-id="a8b11-119">[Start-ServiceFabricPartitionRestart][psrp]</span></span> |

## <a name="conceptual-overview-of-running-a-command"></a><span data-ttu-id="a8b11-120">Bir komutu çalıştırmak kavramsal genel bakış</span><span class="sxs-lookup"><span data-stu-id="a8b11-120">Conceptual Overview of Running a Command</span></span>
<span data-ttu-id="a8b11-121">Hata ekleme ve analiz hizmeti kullanır, bu belgedeki "Başlat" API olarak adlandırılan bir API komutuyla başladığınız zaman uyumsuz bir model sonra sonlanma durumuna ulaştı kadar bir "GetProgress" API'sini kullanarak bu komut ilerlemesini denetler veya İptal kadar.</span><span class="sxs-lookup"><span data-stu-id="a8b11-121">The Fault Injection and Analysis Service uses an asynchronous model where you start the command with one API, referred to as the “Start” API in this document, then checks the progress of this command using a “GetProgress” API until it has reached a terminal state, or until you cancel it.</span></span>
<span data-ttu-id="a8b11-122">Bir komut başlatmak için karşılık gelen API için "Başlat" API çağrısı.</span><span class="sxs-lookup"><span data-stu-id="a8b11-122">To start a command, call the “Start” API for the corresponding API.</span></span>  <span data-ttu-id="a8b11-123">Bu API döndürdüğü hata ekleme ve analiz hizmet isteğini kabul.</span><span class="sxs-lookup"><span data-stu-id="a8b11-123">This API returns when the Fault Injection and Analysis Service has accepted the request.</span></span>  <span data-ttu-id="a8b11-124">Ancak, bunun ne kadar bir komut çalıştırıldı, göstermez veya henüz başlamamış olsa bile.</span><span class="sxs-lookup"><span data-stu-id="a8b11-124">However, it does not indicate how far a command has run, or even if it has started yet.</span></span>  <span data-ttu-id="a8b11-125">Bir komutun ilerleme durumunu denetlemek için "GetProgress" daha önce adı "Başlat" API karşılık gelen API çağrısı.</span><span class="sxs-lookup"><span data-stu-id="a8b11-125">In order to check progress of a command, call the “GetProgress” API that corresponds to the “Start” API previously called.</span></span>  <span data-ttu-id="a8b11-126">"GetProgress" API komutu, durum özelliğinin içinde geçerli durumunu gösteren bir nesne döndürür.</span><span class="sxs-lookup"><span data-stu-id="a8b11-126">The “GetProgress” API will return an object indicating the current status of the command inside its State property.</span></span>  <span data-ttu-id="a8b11-127">Süresiz olarak kadar bir komutu çalıştırır:</span><span class="sxs-lookup"><span data-stu-id="a8b11-127">A command runs indefinitely until:</span></span>

1. <span data-ttu-id="a8b11-128">Başarıyla tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="a8b11-128">It completes successfully.</span></span>  <span data-ttu-id="a8b11-129">"GetProgress" üzerinde bu durumda çağırırsanız, ilerleme nesnenin durumu tamamlanacaktır.</span><span class="sxs-lookup"><span data-stu-id="a8b11-129">If you call “GetProgress” on it in this case, the progress object’s State will be Completed.</span></span>
2. <span data-ttu-id="a8b11-130">Önemli bir hatayla karşılaşırsa.</span><span class="sxs-lookup"><span data-stu-id="a8b11-130">It encounters a fatal error.</span></span>  <span data-ttu-id="a8b11-131">"GetProgress" üzerinde bu durumda çağırırsanız, ilerleme nesnenin durumu hatalı</span><span class="sxs-lookup"><span data-stu-id="a8b11-131">If you call “GetProgress” on it in this case, the progress object’s State will be Faulted</span></span>
3. <span data-ttu-id="a8b11-132">Üzerinden iptal [CancelTestCommandAsync] [ cancel] API'sini veya [Stop-ServiceFabricTestCommand] [ cancelps] PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="a8b11-132">You cancel it through the [CancelTestCommandAsync][cancel] API, or [Stop-ServiceFabricTestCommand][cancelps] PowerShell cmdlet.</span></span>  <span data-ttu-id="a8b11-133">"GetProgress" üzerinde bu durumda çağırırsanız, öğe ilerleme nesnenin durumu bu API için bağımsız değişken bağlı olarak iptal edildi veya ForceCancelled, olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a8b11-133">If you call “GetProgress” on it in this case, the progress object’s State will be either Cancelled or ForceCancelled, depending on an argument to that API.</span></span>  <span data-ttu-id="a8b11-134">Belgelerine bakın [CancelTestCommandAsync] [ cancel] daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="a8b11-134">See the documentation for [CancelTestCommandAsync][cancel] for more details.</span></span>

## <a name="details-of-running-a-command"></a><span data-ttu-id="a8b11-135">Bir komut çalışan ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="a8b11-135">Details of Running a Command</span></span>
<span data-ttu-id="a8b11-136">Bir komut başlatmak için Başlat API beklenen bağımsız değişkenlerle çağırın.</span><span class="sxs-lookup"><span data-stu-id="a8b11-136">In order to start a command, call the Start API with the expected arguments.</span></span>  <span data-ttu-id="a8b11-137">Tüm Başlat API'leri Operationıd adlı bir GUID bağımsız değişkeni vardır.</span><span class="sxs-lookup"><span data-stu-id="a8b11-137">All Start APIs have a Guid argument named operationId.</span></span>  <span data-ttu-id="a8b11-138">Operationıd bağımsız değişkeni, bu komut ilerlemesini izlemek için kullanıldığından izlemek.</span><span class="sxs-lookup"><span data-stu-id="a8b11-138">You should keep track of the operationId argument, since it is used to track progress of this command.</span></span>  <span data-ttu-id="a8b11-139">Bu "GetProgress" API komut ilerlemesini izlemek için geçirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="a8b11-139">This must be passed into the “GetProgress” API in order to track progress of the command.</span></span>  <span data-ttu-id="a8b11-140">Operationıd benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a8b11-140">The operationId must be unique.</span></span>

<span data-ttu-id="a8b11-141">Başlangıç API başarıyla çağrıldıktan sonra döndürülen ilerleme nesnesinin State özelliği tamamlanana kadar GetProgress API bir döngüde çağrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a8b11-141">After successfully calling the Start API, the GetProgress API should be called in a loop until the returned progress object’s State property is Completed.</span></span>  <span data-ttu-id="a8b11-142">Tüm [FabricTransientException'ın] [ fte] ve OperationCanceledException'ın yeniden.</span><span class="sxs-lookup"><span data-stu-id="a8b11-142">All [FabricTransientException’s][fte] and OperationCanceledException’s should be retried.</span></span>
<span data-ttu-id="a8b11-143">Komutu (tamamlandı, Faulted veya iptal edildi) terminal durumuna ulaştı, döndürülen ilerleme nesnenin sonuç özelliği ek bilgi gerekir.</span><span class="sxs-lookup"><span data-stu-id="a8b11-143">When the command has reached a terminal state (Completed, Faulted, or Cancelled), the returned progress object’s Result property will have additional information.</span></span>  <span data-ttu-id="a8b11-144">Durum tamamlanmışsa Result.SelectedPartition.PartitionId seçilmedi bölüm kimliği içerir.</span><span class="sxs-lookup"><span data-stu-id="a8b11-144">If the state is Completed, Result.SelectedPartition.PartitionId will contain the partition id that was selected.</span></span>  <span data-ttu-id="a8b11-145">Result.Exception null olur.</span><span class="sxs-lookup"><span data-stu-id="a8b11-145">Result.Exception will be null.</span></span>  <span data-ttu-id="a8b11-146">Durumu hatalı Result.Exception hata ekleme neden olacaktır ve analiz hizmeti komutu hatalı.</span><span class="sxs-lookup"><span data-stu-id="a8b11-146">If the state is Faulted, Result.Exception will have the reason the Fault Injection and Analysis Service faulted the command.</span></span>  <span data-ttu-id="a8b11-147">Result.SelectedPartition.PartitionId seçilmedi bölüm kimliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="a8b11-147">Result.SelectedPartition.PartitionId will have the partition id that was selected.</span></span>  <span data-ttu-id="a8b11-148">Bazı durumlarda, komut yetecek kadar bir bölümü seçmek için proceeded değil.</span><span class="sxs-lookup"><span data-stu-id="a8b11-148">In some situations, the command may not have proceeded far enough to choose a partition.</span></span>  <span data-ttu-id="a8b11-149">Bu durumda, PartitionID 0 olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a8b11-149">In that case, the PartitionId will be 0.</span></span>  <span data-ttu-id="a8b11-150">Durumu iptal edilirse, Result.Exception null olur.</span><span class="sxs-lookup"><span data-stu-id="a8b11-150">If the state is Cancelled, Result.Exception will be null.</span></span>  <span data-ttu-id="a8b11-151">Faulted durum gibi Result.SelectedPartition.PartitionId seçildi bölüm kimliği vardır, ancak komut yetecek kadar bunu yapmak için proceeded değil, 0 olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a8b11-151">Like the Faulted case, Result.SelectedPartition.PartitionId will have the partition id that was chosen, but if the command has not proceeded far enough to do so, it will be 0.</span></span>  <span data-ttu-id="a8b11-152">Lütfen ayrıca aşağıdaki örneğe bakın.</span><span class="sxs-lookup"><span data-stu-id="a8b11-152">Please also refer to the sample below.</span></span>

<span data-ttu-id="a8b11-153">Aşağıdaki örnek kod, başlayın sonra belirli bir bölüme veri kaybına neden bir komutla ilgili ilerleme durumunu denetleme gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a8b11-153">The sample code below shows how to start then check progress on a command to cause data loss on a specific partition.</span></span>

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

<span data-ttu-id="a8b11-154">Aşağıdaki örnek belirtilen bir hizmeti rastgele bir bölümü seçmek için PartitionSelector kullanmayı gösterir:</span><span class="sxs-lookup"><span data-stu-id="a8b11-154">The sample below shows how to use the PartitionSelector to choose a random partition of a specified service:</span></span>

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

## <a name="history-and-truncation"></a><span data-ttu-id="a8b11-155">Geçmiş ve kesme</span><span class="sxs-lookup"><span data-stu-id="a8b11-155">History and Truncation</span></span>
<span data-ttu-id="a8b11-156">Bir komut terminal durumuna ulaştı sonra meta verilerini alanından tasarruf etmek için kaldırılacak önce belirli bir süre için arıza ekleme ve analiz hizmeti kalır.</span><span class="sxs-lookup"><span data-stu-id="a8b11-156">After a command has reached a terminal state, its metadata will remain in the Fault Injection and Analysis Service for a certain time, before it will be removed to save space.</span></span>  <span data-ttu-id="a8b11-157">"GetProgress" kaldırıldıktan sonra bir komut Operationıd kullanarak çağrılırsa, bir hata kodu KeyNotFound ile FabricException döndürür.</span><span class="sxs-lookup"><span data-stu-id="a8b11-157">If “GetProgress” is called using the operationId of a command after it has been removed, it will return a FabricException with an ErrorCode of KeyNotFound.</span></span>

[dl]: https://msdn.microsoft.com/library/azure/mt693569.aspx
[ql]: https://msdn.microsoft.com/library/azure/mt693558.aspx
[rp]: https://msdn.microsoft.com/library/azure/mt645056.aspx
[psdl]: https://msdn.microsoft.com/library/mt697573.aspx
[psql]: https://msdn.microsoft.com/library/mt697557.aspx
[psrp]: https://msdn.microsoft.com/library/mt697560.aspx
[cancel]: https://msdn.microsoft.com/library/azure/mt668910.aspx
[cancelps]: https://msdn.microsoft.com/library/mt697566.aspx
[fte]: https://msdn.microsoft.com/library/azure/system.fabric.fabrictransientexception.aspx
