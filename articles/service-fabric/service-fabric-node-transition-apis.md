---
title: "aaaStart ve durdurma küme düğümleri tootest Azure mikro | Microsoft Docs"
description: "Nasıl toouse arıza ekleme tootest Service Fabric uygulaması başlatma ve küme düğümleri durdurma öğrenin."
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
ms.date: 6/12/2017
ms.author: lemai
ms.openlocfilehash: 7d3f5147328e6233a67533fbfb2a525aa5fc060e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="replacing-hello-start-node-and-stop-node-apis-with-hello-node-transition-api"></a>Hello düğümü Başlat ve Durdur düğüm API'leri hello düğümü geçiş API ile değiştirme

## <a name="what-do-hello-stop-node-and-start-node-apis-do"></a>Durdur düğümü hello ve başlangıç düğümü API'leri yapın?

Merhaba Durdur düğümü API (yönetilen: [StopNodeAsync()][stopnode], PowerShell: [Stop-ServiceFabricNode][stopnodeps]) bir Service Fabric düğümü durdurur.  Service Fabric düğümü işlemi, VM veya makine değil – hello VM veya makine hala çalıştırırsınız.  Merhaba belge Hello kalanı için Service Fabric düğümü "düğümü" anlamına gelir.  Bir düğümü durdurma, koyar içine bir *durduruldu* burada hello kümesinin bir üyesi değil ve Hizmetleri, bu nedenle benzetimi barındıramaz durumu bir *aşağı* düğümü.  Bu, hataları hello sistem tootest uygulamanızı injecting için kullanışlıdır.  Merhaba başlangıç düğümü API (yönetilen: [StartNodeAsync()][startnode], PowerShell: [başlangıç ServiceFabricNode][startnodeps]]) çevirmelerinin hello düğümü API, Durdur  hangi hello düğüm geri tooa normal durumu getirir.

## <a name="why-are-we-replacing-these"></a>Neden Biz bu değiştirdiğiniz?

Daha önce açıklandığı gibi bir *durduruldu* Service Fabric düğümdür bilerek hello Durdur düğümü API kullanarak hedeflenen bir düğüm.  A *aşağı* (örneğin hello VM veya makine kapalıdır) herhangi bir nedenle çalışmıyor bir düğüm düğümdür.  Merhaba Durdur düğümü API arasında bilgi toodifferentiate hello sistem kullanıma sunmuyor *durduruldu* düğümleri ve *aşağı* düğümleri.

Ayrıca, bu API'ları tarafından döndürülen bazı hatalar olması olabilir olarak tanımlayıcı değildir.  Örneğin, çağırma hello Durdur düğümü API üzerinde zaten bir *durduruldu* düğümü hello hata döndürecektir *InvalidAddress*.  Bu deneyim geliştirilmiş.

Ayrıca, bir düğüm için durduruldu hello süresi başlangıç düğümü API çağrılan hello kadar "sonsuz" olur.  Biz bu sorunlara neden olabilir ve hataya yatkın olabilir buldunuz.  Örneğin, burada bir kullanıcı bir düğümde hello Durdur düğümü API çağrılır ve hakkında mı unuttunuz sorunları gördük.  Daha sonra hello düğüm varsa belirsiz *aşağı* veya *durduruldu*.


## <a name="introducing-hello-node-transition-apis"></a>Merhaba düğümü geçiş API'leri Tanıtımı

Biz, yeni bir API kümesi yukarıda bu sorunları ele aldık.  Merhaba yeni düğümü geçiş API (yönetilen: [StartNodeTransitionAsync()][snt]) kullanılan tootransition Service Fabric düğümü tooa olabilir *durduruldu* durum veya tootransition, gelen bir *durduruldu* durumu tooa durumunu normal.  Lütfen bu hello "Başlat" Merhaba API hello adını toostarting bir düğüm başvurmuyor unutmayın.  Toobeginning hello sistem tootransition hello düğümü tooeither yürütecek zaman uyumsuz bir işlem başvurduğu *durduruldu* veya durumu başlatıldı.

**Kullanım**

Merhaba düğümü geçiş API çağrıldığında bir özel durum oluşturmadığını, ardından hello sistem hello zaman uyumsuz işlemi kabul etti ve yürütülmez.  Başarılı bir çağrı hello işlemi henüz tamamlandı göstermez.  Merhaba işlemi, düğüm geçiş ilerleme API çağrısı hello hello geçerli durumu hakkında bilgi tooget (yönetilen: [GetNodeTransitionProgressAsync()][gntp]) düğüm çağrılırken kullanılan hello GUID ile Bu işlem için geçiş API.  Merhaba düğümü geçiş ilerleme API NodeTransitionProgress nesneyi döndürür.  Bu nesnenin durumu özelliği hello hello işlemi geçerli durumunu belirtir.  Merhaba durumu "çalışıyorsa," Merhaba işlemi yürütüyor.  Tamamlandığında, hatasız hello işlemi tamamlandı.  Bu hatayla, hello işlem yürütülürken bir sorun oluştu.  özellik hangi hello sorun gösterecektir hello sonuç özelliğin özel durum.  Https://docs.microsoft.com/dotnet/api/System.fabric.testcommandprogressstate hello State özelliği ve kod örnekleri için aşağıdaki hello "Örnek kullanım" bölümüne hakkında daha fazla bilgi için bkz.


**Durdurulmuş bir düğümü ve bir aşağı düğümü arasında ayrım yapma** bir düğümü ise *durduruldu* kullanarak hello düğümü geçiş API, bir düğümü sorgusu hello çıktısını (yönetilen: [GetNodeListAsync()] [ nodequery], PowerShell: [Get-ServiceFabricNode][nodequeryps]) bu düğüm olduğunu gösterecek bir *IsStopped* özellik değerinin true.  Bu hello hello değerinden farklı Not *NodeStatus* yazacaktır özelliği *aşağı*.  Merhaba, *NodeStatus* özellik değerine sahip *aşağı*, ancak *IsStopped* hello düğümü hello düğümü geçiş API kullanarak durdurulmadı sonra yanlış olduğundan ve  *Aşağı* başka bir nedenle son.  Merhaba, *IsStopped* özelliktir true ve hello *NodeStatus* özelliği *aşağı*, hello düğümü geçiş API kullanarak durduruldu sonra.

Başlangıç bir *durduruldu* hello düğümü geçiş API kullanarak düğümüne döndürür, toofunction normal hello küme üyesi olarak yeniden.  Merhaba hello düğümü sorgusu API çıktısını gösterir *IsStopped* false olarak ve *NodeStatus* aşağı (örneğin yukarı) olmayan bir şey olarak.


**Sınırlı bir süre** hello düğümü geçiş API toostop bir düğüm kullanırken hello birini parametreleri, gerekli *stopNodeDurationInSeconds*, temsil hello süreyi saniye tookeep hello düğümünde  *durdurulmuş*.  Bu değer izin verilen 600 en az ve en fazla 14400 sahip aralık hello olmalıdır.  Bu süre dolduktan sonra hello düğüm kendi içine durumunu otomatik olarak yeniden başlatılır.  Kullanım örneği için tooSample 1 aşağıya bakın.

> [!WARNING]
> Düğüm geçiş API'leri karıştırma önlemek ve düğüm durdurmak ve başlatmak düğümü API'leri hello.  Merhaba çok başlangıç düğümü geçiş API yalnızca kullanılması önerilir.  > Bir düğüm olup zaten yapıldıysa hello Durdur düğümü API kullanarak durduruldu, onu hello başlangıç düğümü API ilk hello kullanmadan önce kullanılarak başlatılmaması gerekir > düğümü geçiş API'leri.

> [!WARNING]
> Birden çok düğüm geçiş API çağrıları üzerinde yapılamaz aynı düğümde paralel hello.  Merhaba düğümü geçiş API böyle bir durumda olacak > NodeTransitionInProgress ErrorCode özellik değeri olan bir FabricException atar.  Belirli bir düğümde bir düğüm geçiş sonra > edilmiş hello işlemi başlamadan önce bir terminal durumu (tamamlandı, Faulted veya ForceCancelled) ulaşana kadar başlatıldı, beklemeniz gerekir bir > Yeni hello üzerinde aynı geçiş düğümü.  Paralel düğümü geçiş çağrıları farklı düğümlerde izin verilir.


#### <a name="sample-usage"></a>Örnek Kullanım


**Örnek 1** -örnek kullandığı aşağıdaki hello hello düğümü geçiş API toostop bir düğüm.

```csharp
        // Helper function tooget information about a node
        static Node GetNodeInfo(FabricClient fc, string node)
        {
            NodeList n = null;
            while (n == null)
            {
                n = fc.QueryManager.GetNodeListAsync(node).GetAwaiter().GetResult();
                Task.Delay(TimeSpan.FromSeconds(1)).GetAwaiter();
            };

            return n.FirstOrDefault();
        }

        static async Task WaitForStateAsync(FabricClient fc, Guid operationId, TestCommandProgressState targetState)
        {
            NodeTransitionProgress progress = null;

            do
            {
                bool exceptionObserved = false;
                try
                {
                    progress = await fc.TestManager.GetNodeTransitionProgressAsync(operationId, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                    exceptionObserved = true;
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                    exceptionObserved = true;
                }

                if (!exceptionObserved)
                {
                    Console.WriteLine("Current state of operation '{0}': {1}", operationId, progress.State);

                    if (progress.State == TestCommandProgressState.Faulted)
                    {
                        // Inspect hello progress object's Result.Exception.HResult tooget hello error code.
                        Console.WriteLine("'{0}' failed with: {1}, HResult: {2}", operationId, progress.Result.Exception, progress.Result.Exception.HResult);

                        // ...additional logic as required
                    }

                    if (progress.State == targetState)
                    {
                        Console.WriteLine("Target state '{0}' has been reached", targetState);
                        break;
                    }
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);
            }
            while (true);
        }

        static async Task StopNodeAsync(FabricClient fc, string nodeName, int durationInSeconds)
        {
            // Uses hello GetNodeListAsync() API tooget information about hello target node
            Node n = GetNodeInfo(fc, nodeName);

            // Create a Guid
            Guid guid = Guid.NewGuid();

            // Create a NodeStopDescription object, which will be used as a parameter into StartNodeTransition
            NodeStopDescription description = new NodeStopDescription(guid, n.NodeName, n.NodeInstanceId, durationInSeconds);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with hello NodeStopDescription from above, which will stop hello target node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    // This is retryable
                }
                catch (FabricTransientException fte)
                {
                    // This is retryable
                }

                // Backoff
                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);
            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hte desired state is reached.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Completed).ConfigureAwait(false);
        }
```

**Örnek 2** - hello örnek başlatır izleyen bir *durduruldu* düğümü.  Bazı yardımcı yöntemler hello ilk örnekten kullanır.

```csharp
        static async Task StartNodeAsync(FabricClient fc, string nodeName)
        {
            // Uses hello GetNodeListAsync() API tooget information about hello target node
            Node n = GetNodeInfo(fc, nodeName);

            Guid guid = Guid.NewGuid();
            BigInteger nodeInstanceId = n.NodeInstanceId;

            // Create a NodeStartDescription object, which will be used as a parameter into StartNodeTransition
            NodeStartDescription description = new NodeStartDescription(guid, n.NodeName, nodeInstanceId);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with hello NodeStartDescription from above, which will start hello target stopped node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);

            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hte desired state is reached.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Completed).ConfigureAwait(false);
        }
```

**Örnek 3** - hello aşağıdaki örnek, yanlış kullanımı gösterir.  Bu kullanım yanlış olduğundan hello *stopDurationInSeconds* sağladığı izin verilen aralığın başlangıç daha büyük.  StartNodeTransitionAsync() önemli bir hata ile başarısız olur bu yana hello işlemi kabul ve hello ilerleme API çağrılmamalı.  Bu örnek hello ilk örnekten bazı yardımcı yöntemler kullanır.

```csharp
        static async Task StopNodeWithOutOfRangeDurationAsync(FabricClient fc, string nodeName)
        {
            Node n = GetNodeInfo(fc, nodeName);

            Guid guid = Guid.NewGuid();

            // Use an out of range value for stopDurationInSeconds toodemonstrate error
            NodeStopDescription description = new NodeStopDescription(guid, n.NodeName, n.NodeInstanceId, 99999);

            try
            {
                await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
            }

            catch (FabricException e)
            {
                Console.WriteLine("Caught {0}", e);
                Console.WriteLine("ErrorCode {0}", e.ErrorCode);
                // Output:
                // Caught System.Fabric.FabricException: System.Runtime.InteropServices.COMException (-2147017629)
                // StopDurationInSeconds is out of range ---> System.Runtime.InteropServices.COMException: Exception from HRESULT: 0x80071C63
                // << Parts of exception omitted>>
                //
                // ErrorCode InvalidDuration
            }
        }
```

**Örnek 4** - hello aşağıdaki örnek, başlangıç düğümü, geçiş ilerleme hello düğümü geçiş API tarafından başlatılan hello işlemi kabul edilir, ancak daha sonra yürütülürken başarısız olduğunda API sunucudan döndürülen hello hata bilgilerini gösterir.  Merhaba düğümü geçiş API toostart var olmayan bir düğüm çalıştığı hello durumda başarısız olur.  Bu örnek hello ilk örnekten bazı yardımcı yöntemler kullanır.

```csharp
        static async Task StartNodeWithNonexistentNodeAsync(FabricClient fc)
        {
            Guid guid = Guid.NewGuid();
            BigInteger nodeInstanceId = 12345;

            // Intentionally use a nonexistent node
            NodeStartDescription description = new NodeStartDescription(guid, "NonexistentNode", nodeInstanceId);

            bool wasSuccessful = false;

            do
            {
                try
                {
                    // Invoke StartNodeTransitionAsync with hello NodeStartDescription from above, which will start hello target stopped node.  Retry transient errors.
                    await fc.TestManager.StartNodeTransitionAsync(description, TimeSpan.FromMinutes(1), CancellationToken.None).ConfigureAwait(false);
                    wasSuccessful = true;
                }
                catch (OperationCanceledException oce)
                {
                    Console.WriteLine("Caught exception '{0}'", oce);
                }
                catch (FabricTransientException fte)
                {
                    Console.WriteLine("Caught exception '{0}'", fte);
                }

                await Task.Delay(TimeSpan.FromSeconds(5)).ConfigureAwait(false);

            }
            while (!wasSuccessful);

            // Now call StartNodeTransitionProgressAsync() until hello desired state is reached.  In this case, it will end up in hello Faulted state since hello node does not exist.
            // When StartNodeTransitionProgressAsync()'s returned progress object has a State if Faulted, inspect hello progress object's Result.Exception.HResult tooget hello error code.
            // In this case, it will be NodeNotFound.
            await WaitForStateAsync(fc, guid, TestCommandProgressState.Faulted).ConfigureAwait(false);
        }
```

[stopnode]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.faultmanagementclient?redirectedfrom=MSDN#System_Fabric_FabricClient_FaultManagementClient_StopNodeAsync_System_String_System_Numerics_BigInteger_System_Fabric_CompletionMode_
[stopnodeps]: https://msdn.microsoft.com/library/mt125982.aspx
[startnode]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.faultmanagementclient?redirectedfrom=MSDN#System_Fabric_FabricClient_FaultManagementClient_StartNodeAsync_System_String_System_Numerics_BigInteger_System_String_System_Int32_System_Fabric_CompletionMode_System_Threading_CancellationToken_
[startnodeps]: https://msdn.microsoft.com/library/mt163520.aspx
[nodequery]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.queryclient#System_Fabric_FabricClient_QueryClient_GetNodeListAsync_System_String_
[nodequeryps]: https://docs.microsoft.com/powershell/servicefabric/vlatest/Get-ServiceFabricNode?redirectedfrom=msdn
[snt]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.testmanagementclient#System_Fabric_FabricClient_TestManagementClient_StartNodeTransitionAsync_System_Fabric_Description_NodeTransitionDescription_System_TimeSpan_System_Threading_CancellationToken_
[gntp]: https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient.testmanagementclient#System_Fabric_FabricClient_TestManagementClient_GetNodeTransitionProgressAsync_System_Guid_System_TimeSpan_System_Threading_CancellationToken_
