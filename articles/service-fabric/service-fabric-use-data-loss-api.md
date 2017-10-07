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
# <a name="how-tooinvoke-data-loss-on-services"></a><span data-ttu-id="8508c-103">Nasıl tooInvoke Hizmetleri veri kaybı</span><span class="sxs-lookup"><span data-stu-id="8508c-103">How tooInvoke Data Loss on Services</span></span>
> [!WARNING]
> <span data-ttu-id="8508c-104">Bu belgeyi açıklayan nasıl hizmetlerinizi, toocause veri kaybına ve dikkatli kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8508c-104">This document describe how toocause data loss in your services, and should be used with care.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="8508c-105">Giriş</span><span class="sxs-lookup"><span data-stu-id="8508c-105">Introduction</span></span>
<span data-ttu-id="8508c-106">Veri kaybı Service Fabric hizmetinizin arama StartPartitionDataLossAsync() tarafından bir bölüme çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8508c-106">You can invoke data loss on a partition of your Service Fabric Service by calling StartPartitionDataLossAsync().</span></span>  <span data-ttu-id="8508c-107">Bu API hello hata ekleme ve analiz hizmeti tooperform hello iş toocause veri kaybı koşullarını kullanır.</span><span class="sxs-lookup"><span data-stu-id="8508c-107">This api uses hello Fault Injection and Analysis Service tooperform hello work toocause data loss conditions.</span></span>

## <a name="using-hello-fault-injection-and-analysis-service"></a><span data-ttu-id="8508c-108">Merhaba hata ekleme ve analiz hizmeti kullanılarak</span><span class="sxs-lookup"><span data-stu-id="8508c-108">Using hello Fault Injection and Analysis Service</span></span>
<span data-ttu-id="8508c-109">Merhaba hata ekleme ve analiz hizmeti aşağıdaki hello grafik API'leri aşağıdaki hello şu anda destekler.</span><span class="sxs-lookup"><span data-stu-id="8508c-109">hello Fault Injection and Analysis Service currently supports hello following APIs in hello chart below.</span></span>  <span data-ttu-id="8508c-110">Merhaba grafik Hello sağ tarafındaki hello karşılık gelen PowerShell cmdlet'ini gösterir.</span><span class="sxs-lookup"><span data-stu-id="8508c-110">hello right side of hello chart shows hello corresponding PowerShell cmdlet.</span></span>  <span data-ttu-id="8508c-111">Her biri hakkında daha fazla bilgi için lütfen her API toohello msdn belgelerine başvurun.</span><span class="sxs-lookup"><span data-stu-id="8508c-111">Please refer toohello msdn documentation on each API for more information on each one.</span></span>

| <span data-ttu-id="8508c-112">C# API'Sİ</span><span class="sxs-lookup"><span data-stu-id="8508c-112">C# API</span></span> | <span data-ttu-id="8508c-113">PowerShell cmdlet'i</span><span class="sxs-lookup"><span data-stu-id="8508c-113">PowerShell Cmdlet</span></span> |
| --- | ---:|
| <span data-ttu-id="8508c-114">[StartPartitionDataLossAsync][dl]</span><span class="sxs-lookup"><span data-stu-id="8508c-114">[StartPartitionDataLossAsync][dl]</span></span> |<span data-ttu-id="8508c-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span><span class="sxs-lookup"><span data-stu-id="8508c-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span></span> |
| <span data-ttu-id="8508c-116">[StartPartitionQuorumLossAsync][ql]</span><span class="sxs-lookup"><span data-stu-id="8508c-116">[StartPartitionQuorumLossAsync][ql]</span></span> |<span data-ttu-id="8508c-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span><span class="sxs-lookup"><span data-stu-id="8508c-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span></span> |
| <span data-ttu-id="8508c-118">[StartPartitionRestartAsync][rp]</span><span class="sxs-lookup"><span data-stu-id="8508c-118">[StartPartitionRestartAsync][rp]</span></span> |<span data-ttu-id="8508c-119">[Start-ServiceFabricPartitionRestart][psrp]</span><span class="sxs-lookup"><span data-stu-id="8508c-119">[Start-ServiceFabricPartitionRestart][psrp]</span></span> |

## <a name="conceptual-overview-of-running-a-command"></a><span data-ttu-id="8508c-120">Bir komutu çalıştırmak kavramsal genel bakış</span><span class="sxs-lookup"><span data-stu-id="8508c-120">Conceptual Overview of Running a Command</span></span>
<span data-ttu-id="8508c-121">Merhaba başladığınız zaman uyumsuz bir model tooas hello "Başlat" API sonra denetimleri hello ilerlemesini terminal ulaştı kadar "GetProgress" API'sini kullanarak bu komut, bu belgedeki başvurulan bir API ile komutu Hata ekleme ve analiz hizmeti kullanan hello durum, ya da size kadar iptal edin.</span><span class="sxs-lookup"><span data-stu-id="8508c-121">hello Fault Injection and Analysis Service uses an asynchronous model where you start hello command with one API, referred tooas hello “Start” API in this document, then checks hello progress of this command using a “GetProgress” API until it has reached a terminal state, or until you cancel it.</span></span>
<span data-ttu-id="8508c-122">toostart bir komut hello karşılık gelen API için hello "Başlat" API çağrısı.</span><span class="sxs-lookup"><span data-stu-id="8508c-122">toostart a command, call hello “Start” API for hello corresponding API.</span></span>  <span data-ttu-id="8508c-123">Bu API hello hata ekleme ve analiz hizmeti hello isteği kabul döndürür.</span><span class="sxs-lookup"><span data-stu-id="8508c-123">This API returns when hello Fault Injection and Analysis Service has accepted hello request.</span></span>  <span data-ttu-id="8508c-124">Ancak, bunun ne kadar bir komut çalıştırıldı, göstermez veya henüz başlamamış olsa bile.</span><span class="sxs-lookup"><span data-stu-id="8508c-124">However, it does not indicate how far a command has run, or even if it has started yet.</span></span>  <span data-ttu-id="8508c-125">Sipariş toocheck ediyor komut, hello "GetProgress" toohello "Başlat" API önceden adlı karşılık gelen API çağrısı.</span><span class="sxs-lookup"><span data-stu-id="8508c-125">In order toocheck progress of a command, call hello “GetProgress” API that corresponds toohello “Start” API previously called.</span></span>  <span data-ttu-id="8508c-126">Merhaba "GetProgress" API hello hello komutu, durum özelliğinin içinde geçerli durumunu gösteren bir nesne döndürür.</span><span class="sxs-lookup"><span data-stu-id="8508c-126">hello “GetProgress” API will return an object indicating hello current status of hello command inside its State property.</span></span>  <span data-ttu-id="8508c-127">Süresiz olarak kadar bir komutu çalıştırır:</span><span class="sxs-lookup"><span data-stu-id="8508c-127">A command runs indefinitely until:</span></span>

1. <span data-ttu-id="8508c-128">Başarıyla tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="8508c-128">It completes successfully.</span></span>  <span data-ttu-id="8508c-129">"GetProgress" üzerinde bu durumda çağırırsanız, hello ilerleme nesnenin durumu tamamlanacaktır.</span><span class="sxs-lookup"><span data-stu-id="8508c-129">If you call “GetProgress” on it in this case, hello progress object’s State will be Completed.</span></span>
2. <span data-ttu-id="8508c-130">Önemli bir hatayla karşılaşırsa.</span><span class="sxs-lookup"><span data-stu-id="8508c-130">It encounters a fatal error.</span></span>  <span data-ttu-id="8508c-131">"GetProgress" üzerinde bu durumda çağırırsanız, hello ilerleme nesnenin durumu hatalı</span><span class="sxs-lookup"><span data-stu-id="8508c-131">If you call “GetProgress” on it in this case, hello progress object’s State will be Faulted</span></span>
3. <span data-ttu-id="8508c-132">Merhaba iptal [CancelTestCommandAsync] [ cancel] API, veya [Stop-ServiceFabricTestCommand] [ cancelps] PowerShell cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="8508c-132">You cancel it through hello [CancelTestCommandAsync][cancel] API, or [Stop-ServiceFabricTestCommand][cancelps] PowerShell cmdlet.</span></span>  <span data-ttu-id="8508c-133">"GetProgress" üzerinde bu durumda çağırırsanız, hello ilerleme nesnenin durumu iptal edildi veya ForceCancelled, bir bağımsız değişken toothat API bağlı olacaktır.</span><span class="sxs-lookup"><span data-stu-id="8508c-133">If you call “GetProgress” on it in this case, hello progress object’s State will be either Cancelled or ForceCancelled, depending on an argument toothat API.</span></span>  <span data-ttu-id="8508c-134">Merhaba belgelerine bakın [CancelTestCommandAsync] [ cancel] daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="8508c-134">See hello documentation for [CancelTestCommandAsync][cancel] for more details.</span></span>

## <a name="details-of-running-a-command"></a><span data-ttu-id="8508c-135">Bir komut çalışan ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="8508c-135">Details of Running a Command</span></span>
<span data-ttu-id="8508c-136">Sipariş toostart bir komutu, beklenen hello bağımsız değişkenlerle hello Başlat API çağırın.</span><span class="sxs-lookup"><span data-stu-id="8508c-136">In order toostart a command, call hello Start API with hello expected arguments.</span></span>  <span data-ttu-id="8508c-137">Tüm Başlat API'leri Operationıd adlı bir GUID bağımsız değişkeni vardır.</span><span class="sxs-lookup"><span data-stu-id="8508c-137">All Start APIs have a Guid argument named operationId.</span></span>  <span data-ttu-id="8508c-138">Merhaba Operationıd bağımsız değişkeni, kullanıldığından kaydını tutabilirsiniz tootrack ilerleme durumunu bu komutu.</span><span class="sxs-lookup"><span data-stu-id="8508c-138">You should keep track of hello operationId argument, since it is used tootrack progress of this command.</span></span>  <span data-ttu-id="8508c-139">Merhaba hello komutunun sipariş tootrack Sürüyor "GetProgress" API uygulamasına geçirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="8508c-139">This must be passed into hello “GetProgress” API in order tootrack progress of hello command.</span></span>  <span data-ttu-id="8508c-140">Merhaba Operationıd benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="8508c-140">hello operationId must be unique.</span></span>

<span data-ttu-id="8508c-141">Başarılı bir şekilde hello API, başlatma ilerleme hello döndürülen kadar bir döngüde GetProgress API çağrılmalıdır hello çağrıldıktan sonra nesnesinin State özelliği tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="8508c-141">After successfully calling hello Start API, hello GetProgress API should be called in a loop until hello returned progress object’s State property is Completed.</span></span>  <span data-ttu-id="8508c-142">Tüm [FabricTransientException'ın] [ fte] ve OperationCanceledException'ın yeniden.</span><span class="sxs-lookup"><span data-stu-id="8508c-142">All [FabricTransientException’s][fte] and OperationCanceledException’s should be retried.</span></span>
<span data-ttu-id="8508c-143">Merhaba komutu (tamamlandı, Faulted veya iptal edildi) terminal durumuna ulaştı, ilerleme nesnenin sonuç özelliği ek bilgi gerekir hello döndürdü.</span><span class="sxs-lookup"><span data-stu-id="8508c-143">When hello command has reached a terminal state (Completed, Faulted, or Cancelled), hello returned progress object’s Result property will have additional information.</span></span>  <span data-ttu-id="8508c-144">Merhaba durumu tamamlanmışsa Result.SelectedPartition.PartitionId seçilmedi hello bölüm kimliği içerir.</span><span class="sxs-lookup"><span data-stu-id="8508c-144">If hello state is Completed, Result.SelectedPartition.PartitionId will contain hello partition id that was selected.</span></span>  <span data-ttu-id="8508c-145">Result.Exception null olur.</span><span class="sxs-lookup"><span data-stu-id="8508c-145">Result.Exception will be null.</span></span>  <span data-ttu-id="8508c-146">Merhaba durumu hatalı, Result.Exception hello neden hello hata ekleme ve analiz hatalı hizmet hello komutu yüklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8508c-146">If hello state is Faulted, Result.Exception will have hello reason hello Fault Injection and Analysis Service faulted hello command.</span></span>  <span data-ttu-id="8508c-147">Result.SelectedPartition.PartitionId seçilmedi hello bölüm kimliği gerekir.</span><span class="sxs-lookup"><span data-stu-id="8508c-147">Result.SelectedPartition.PartitionId will have hello partition id that was selected.</span></span>  <span data-ttu-id="8508c-148">Bazı durumlarda, hello komutu şu ana kadar yeterli toochoose bir bölüm proceeded değil.</span><span class="sxs-lookup"><span data-stu-id="8508c-148">In some situations, hello command may not have proceeded far enough toochoose a partition.</span></span>  <span data-ttu-id="8508c-149">Bu durumda, hello PartitionID 0 olacaktır.</span><span class="sxs-lookup"><span data-stu-id="8508c-149">In that case, hello PartitionId will be 0.</span></span>  <span data-ttu-id="8508c-150">Merhaba durumu iptal edilirse, Result.Exception null olur.</span><span class="sxs-lookup"><span data-stu-id="8508c-150">If hello state is Cancelled, Result.Exception will be null.</span></span>  <span data-ttu-id="8508c-151">Hello Faulted çalışması gibi Result.SelectedPartition.PartitionId seçildi hello bölüm kimliği vardır, ancak hello komutu şu ana kadar yeterli toodo şekilde proceeded değil, 0 olacaktır.</span><span class="sxs-lookup"><span data-stu-id="8508c-151">Like hello Faulted case, Result.SelectedPartition.PartitionId will have hello partition id that was chosen, but if hello command has not proceeded far enough toodo so, it will be 0.</span></span>  <span data-ttu-id="8508c-152">Lütfen aşağıdaki toohello örneği de bakın.</span><span class="sxs-lookup"><span data-stu-id="8508c-152">Please also refer toohello sample below.</span></span>

<span data-ttu-id="8508c-153">Aşağıdaki Hello örnek kodu nasıl toostart sonra Denetle komutu toocause veri kaybı belirli bir bölüme ilerlemesini gösterir.</span><span class="sxs-lookup"><span data-stu-id="8508c-153">hello sample code below shows how toostart then check progress on a command toocause data loss on a specific partition.</span></span>

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

<span data-ttu-id="8508c-154">Aşağıdaki Hello örneği nasıl toouse hello PartitionSelector toochoose belirtilen bir hizmeti rastgele bir bölümünü gösterir:</span><span class="sxs-lookup"><span data-stu-id="8508c-154">hello sample below shows how toouse hello PartitionSelector toochoose a random partition of a specified service:</span></span>

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

## <a name="history-and-truncation"></a><span data-ttu-id="8508c-155">Geçmiş ve kesme</span><span class="sxs-lookup"><span data-stu-id="8508c-155">History and Truncation</span></span>
<span data-ttu-id="8508c-156">Bir komut terminal durumuna ulaştı sonra meta verilerini hello hata ekleme kalır ve toosave alanı olacak önce belirli bir süre için analiz hizmetlerini kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="8508c-156">After a command has reached a terminal state, its metadata will remain in hello Fault Injection and Analysis Service for a certain time, before it will be removed toosave space.</span></span>  <span data-ttu-id="8508c-157">"GetProgress" Merhaba Operationıd komut kaldırıldıktan sonra kullanarak çağrılırsa, bir hata kodu KeyNotFound ile FabricException döndürür.</span><span class="sxs-lookup"><span data-stu-id="8508c-157">If “GetProgress” is called using hello operationId of a command after it has been removed, it will return a FabricException with an ErrorCode of KeyNotFound.</span></span>

[dl]: https://msdn.microsoft.com/library/azure/mt693569.aspx
[ql]: https://msdn.microsoft.com/library/azure/mt693558.aspx
[rp]: https://msdn.microsoft.com/library/azure/mt645056.aspx
[psdl]: https://msdn.microsoft.com/library/mt697573.aspx
[psql]: https://msdn.microsoft.com/library/mt697557.aspx
[psrp]: https://msdn.microsoft.com/library/mt697560.aspx
[cancel]: https://msdn.microsoft.com/library/azure/mt668910.aspx
[cancelps]: https://msdn.microsoft.com/library/mt697566.aspx
[fte]: https://msdn.microsoft.com/library/azure/system.fabric.fabrictransientexception.aspx
