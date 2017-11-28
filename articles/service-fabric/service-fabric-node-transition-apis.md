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
# <a name="replacing-hello-start-node-and-stop-node-apis-with-hello-node-transition-api"></a><span data-ttu-id="8b70d-103">Hello düğümü Başlat ve Durdur düğüm API'leri hello düğümü geçiş API ile değiştirme</span><span class="sxs-lookup"><span data-stu-id="8b70d-103">Replacing hello Start Node and Stop node APIs with hello Node Transition API</span></span>

## <a name="what-do-hello-stop-node-and-start-node-apis-do"></a><span data-ttu-id="8b70d-104">Durdur düğümü hello ve başlangıç düğümü API'leri yapın?</span><span class="sxs-lookup"><span data-stu-id="8b70d-104">What do hello Stop Node and Start Node APIs do?</span></span>

<span data-ttu-id="8b70d-105">Merhaba Durdur düğümü API (yönetilen: [StopNodeAsync()][stopnode], PowerShell: [Stop-ServiceFabricNode][stopnodeps]) bir Service Fabric düğümü durdurur.</span><span class="sxs-lookup"><span data-stu-id="8b70d-105">hello Stop Node API (managed: [StopNodeAsync()][stopnode], PowerShell: [Stop-ServiceFabricNode][stopnodeps]) stops a Service Fabric node.</span></span>  <span data-ttu-id="8b70d-106">Service Fabric düğümü işlemi, VM veya makine değil – hello VM veya makine hala çalıştırırsınız.</span><span class="sxs-lookup"><span data-stu-id="8b70d-106">A Service Fabric node is process, not a VM or machine – hello VM or machine will still be running.</span></span>  <span data-ttu-id="8b70d-107">Merhaba belge Hello kalanı için Service Fabric düğümü "düğümü" anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="8b70d-107">For hello rest of hello document "node" will mean Service Fabric node.</span></span>  <span data-ttu-id="8b70d-108">Bir düğümü durdurma, koyar içine bir *durduruldu* burada hello kümesinin bir üyesi değil ve Hizmetleri, bu nedenle benzetimi barındıramaz durumu bir *aşağı* düğümü.</span><span class="sxs-lookup"><span data-stu-id="8b70d-108">Stopping a node puts it into a *stopped* state where it is not a member of hello cluster and cannot host services, thus simulating a *down* node.</span></span>  <span data-ttu-id="8b70d-109">Bu, hataları hello sistem tootest uygulamanızı injecting için kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="8b70d-109">This is useful for injecting faults into hello system tootest your application.</span></span>  <span data-ttu-id="8b70d-110">Merhaba başlangıç düğümü API (yönetilen: [StartNodeAsync()][startnode], PowerShell: [başlangıç ServiceFabricNode][startnodeps]]) çevirmelerinin hello düğümü API, Durdur  hangi hello düğüm geri tooa normal durumu getirir.</span><span class="sxs-lookup"><span data-stu-id="8b70d-110">hello Start Node API (managed: [StartNodeAsync()][startnode], PowerShell: [Start-ServiceFabricNode][startnodeps]]) reverses hello Stop Node API,  which brings hello node back tooa normal state.</span></span>

## <a name="why-are-we-replacing-these"></a><span data-ttu-id="8b70d-111">Neden Biz bu değiştirdiğiniz?</span><span class="sxs-lookup"><span data-stu-id="8b70d-111">Why are we replacing these?</span></span>

<span data-ttu-id="8b70d-112">Daha önce açıklandığı gibi bir *durduruldu* Service Fabric düğümdür bilerek hello Durdur düğümü API kullanarak hedeflenen bir düğüm.</span><span class="sxs-lookup"><span data-stu-id="8b70d-112">As described earlier, a *stopped* Service Fabric node is a node intentionally targeted using hello Stop Node API.</span></span>  <span data-ttu-id="8b70d-113">A *aşağı* (örneğin hello VM veya makine kapalıdır) herhangi bir nedenle çalışmıyor bir düğüm düğümdür.</span><span class="sxs-lookup"><span data-stu-id="8b70d-113">A *down* node is a node that is down for any other reason (e.g. hello VM or machine is off).</span></span>  <span data-ttu-id="8b70d-114">Merhaba Durdur düğümü API arasında bilgi toodifferentiate hello sistem kullanıma sunmuyor *durduruldu* düğümleri ve *aşağı* düğümleri.</span><span class="sxs-lookup"><span data-stu-id="8b70d-114">With hello Stop Node API, hello system does not expose information toodifferentiate between *stopped* nodes and *down* nodes.</span></span>

<span data-ttu-id="8b70d-115">Ayrıca, bu API'ları tarafından döndürülen bazı hatalar olması olabilir olarak tanımlayıcı değildir.</span><span class="sxs-lookup"><span data-stu-id="8b70d-115">In addition, some errors returned by these APIs are not as descriptive as they could be.</span></span>  <span data-ttu-id="8b70d-116">Örneğin, çağırma hello Durdur düğümü API üzerinde zaten bir *durduruldu* düğümü hello hata döndürecektir *InvalidAddress*.</span><span class="sxs-lookup"><span data-stu-id="8b70d-116">For example, invoking hello Stop Node API on an already *stopped* node will return hello error *InvalidAddress*.</span></span>  <span data-ttu-id="8b70d-117">Bu deneyim geliştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="8b70d-117">This experience could be improved.</span></span>

<span data-ttu-id="8b70d-118">Ayrıca, bir düğüm için durduruldu hello süresi başlangıç düğümü API çağrılan hello kadar "sonsuz" olur.</span><span class="sxs-lookup"><span data-stu-id="8b70d-118">Also, hello duration a node is stopped for is “infinite” until hello Start Node API is invoked.</span></span>  <span data-ttu-id="8b70d-119">Biz bu sorunlara neden olabilir ve hataya yatkın olabilir buldunuz.</span><span class="sxs-lookup"><span data-stu-id="8b70d-119">We’ve found this can cause problems and may be error-prone.</span></span>  <span data-ttu-id="8b70d-120">Örneğin, burada bir kullanıcı bir düğümde hello Durdur düğümü API çağrılır ve hakkında mı unuttunuz sorunları gördük.</span><span class="sxs-lookup"><span data-stu-id="8b70d-120">For example, we’ve seen problems where a user invoked hello Stop Node API on a node and then forgot about it.</span></span>  <span data-ttu-id="8b70d-121">Daha sonra hello düğüm varsa belirsiz *aşağı* veya *durduruldu*.</span><span class="sxs-lookup"><span data-stu-id="8b70d-121">Later, it was unclear if hello node was *down* or *stopped*.</span></span>


## <a name="introducing-hello-node-transition-apis"></a><span data-ttu-id="8b70d-122">Merhaba düğümü geçiş API'leri Tanıtımı</span><span class="sxs-lookup"><span data-stu-id="8b70d-122">Introducing hello Node Transition APIs</span></span>

<span data-ttu-id="8b70d-123">Biz, yeni bir API kümesi yukarıda bu sorunları ele aldık.</span><span class="sxs-lookup"><span data-stu-id="8b70d-123">We’ve addressed these issues above in a new set of APIs.</span></span>  <span data-ttu-id="8b70d-124">Merhaba yeni düğümü geçiş API (yönetilen: [StartNodeTransitionAsync()][snt]) kullanılan tootransition Service Fabric düğümü tooa olabilir *durduruldu* durum veya tootransition, gelen bir *durduruldu* durumu tooa durumunu normal.</span><span class="sxs-lookup"><span data-stu-id="8b70d-124">hello new Node Transition API (managed: [StartNodeTransitionAsync()][snt]) may be used tootransition a Service Fabric node tooa *stopped* state, or tootransition it from a *stopped* state tooa normal up state.</span></span>  <span data-ttu-id="8b70d-125">Lütfen bu hello "Başlat" Merhaba API hello adını toostarting bir düğüm başvurmuyor unutmayın.</span><span class="sxs-lookup"><span data-stu-id="8b70d-125">Please note that hello “Start” in hello name of hello API does not refer toostarting a node.</span></span>  <span data-ttu-id="8b70d-126">Toobeginning hello sistem tootransition hello düğümü tooeither yürütecek zaman uyumsuz bir işlem başvurduğu *durduruldu* veya durumu başlatıldı.</span><span class="sxs-lookup"><span data-stu-id="8b70d-126">It refers toobeginning an asynchronous operation that hello system will execute tootransition hello node tooeither *stopped* or started state.</span></span>

<span data-ttu-id="8b70d-127">**Kullanım**</span><span class="sxs-lookup"><span data-stu-id="8b70d-127">**Usage**</span></span>

<span data-ttu-id="8b70d-128">Merhaba düğümü geçiş API çağrıldığında bir özel durum oluşturmadığını, ardından hello sistem hello zaman uyumsuz işlemi kabul etti ve yürütülmez.</span><span class="sxs-lookup"><span data-stu-id="8b70d-128">If hello Node Transition API does not throw an exception when invoked, then hello system has accepted hello asynchronous operation, and will execute it.</span></span>  <span data-ttu-id="8b70d-129">Başarılı bir çağrı hello işlemi henüz tamamlandı göstermez.</span><span class="sxs-lookup"><span data-stu-id="8b70d-129">A successful call does not imply hello operation is finished yet.</span></span>  <span data-ttu-id="8b70d-130">Merhaba işlemi, düğüm geçiş ilerleme API çağrısı hello hello geçerli durumu hakkında bilgi tooget (yönetilen: [GetNodeTransitionProgressAsync()][gntp]) düğüm çağrılırken kullanılan hello GUID ile Bu işlem için geçiş API.</span><span class="sxs-lookup"><span data-stu-id="8b70d-130">tooget information about hello current state of hello operation, call hello Node Transition Progress API (managed: [GetNodeTransitionProgressAsync()][gntp]) with hello guid used when invoking Node Transition API for this operation.</span></span>  <span data-ttu-id="8b70d-131">Merhaba düğümü geçiş ilerleme API NodeTransitionProgress nesneyi döndürür.</span><span class="sxs-lookup"><span data-stu-id="8b70d-131">hello Node Transition Progress API returns an NodeTransitionProgress object.</span></span>  <span data-ttu-id="8b70d-132">Bu nesnenin durumu özelliği hello hello işlemi geçerli durumunu belirtir.</span><span class="sxs-lookup"><span data-stu-id="8b70d-132">This object’s State property specifies hello current state of hello operation.</span></span>  <span data-ttu-id="8b70d-133">Merhaba durumu "çalışıyorsa," Merhaba işlemi yürütüyor.</span><span class="sxs-lookup"><span data-stu-id="8b70d-133">If hello state is “Running” then hello operation is executing.</span></span>  <span data-ttu-id="8b70d-134">Tamamlandığında, hatasız hello işlemi tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="8b70d-134">If it is Completed, hello operation finished without error.</span></span>  <span data-ttu-id="8b70d-135">Bu hatayla, hello işlem yürütülürken bir sorun oluştu.</span><span class="sxs-lookup"><span data-stu-id="8b70d-135">If it is Faulted, there was a problem executing hello operation.</span></span>  <span data-ttu-id="8b70d-136">özellik hangi hello sorun gösterecektir hello sonuç özelliğin özel durum.</span><span class="sxs-lookup"><span data-stu-id="8b70d-136">hello Result property’s Exception property will indicate what hello issue was.</span></span>  <span data-ttu-id="8b70d-137">Https://docs.microsoft.com/dotnet/api/System.fabric.testcommandprogressstate hello State özelliği ve kod örnekleri için aşağıdaki hello "Örnek kullanım" bölümüne hakkında daha fazla bilgi için bkz.</span><span class="sxs-lookup"><span data-stu-id="8b70d-137">See https://docs.microsoft.com/dotnet/api/system.fabric.testcommandprogressstate for more information about hello State property, and hello “Sample Usage” section below for code examples.</span></span>


<span data-ttu-id="8b70d-138">**Durdurulmuş bir düğümü ve bir aşağı düğümü arasında ayrım yapma** bir düğümü ise *durduruldu* kullanarak hello düğümü geçiş API, bir düğümü sorgusu hello çıktısını (yönetilen: [GetNodeListAsync()] [ nodequery], PowerShell: [Get-ServiceFabricNode][nodequeryps]) bu düğüm olduğunu gösterecek bir *IsStopped* özellik değerinin true.</span><span class="sxs-lookup"><span data-stu-id="8b70d-138">**Differentiating between a stopped node and a down node** If a node is *stopped* using hello Node Transition API, hello output of a node query (managed: [GetNodeListAsync()][nodequery], PowerShell: [Get-ServiceFabricNode][nodequeryps]) will show that this node has an *IsStopped* property value of true.</span></span>  <span data-ttu-id="8b70d-139">Bu hello hello değerinden farklı Not *NodeStatus* yazacaktır özelliği *aşağı*.</span><span class="sxs-lookup"><span data-stu-id="8b70d-139">Note this is different from hello value of hello *NodeStatus* property, which will say *Down*.</span></span>  <span data-ttu-id="8b70d-140">Merhaba, *NodeStatus* özellik değerine sahip *aşağı*, ancak *IsStopped* hello düğümü hello düğümü geçiş API kullanarak durdurulmadı sonra yanlış olduğundan ve  *Aşağı* başka bir nedenle son.</span><span class="sxs-lookup"><span data-stu-id="8b70d-140">If hello *NodeStatus* property has a value of *Down*, but *IsStopped* is false, then hello node was not stopped using hello Node Transition API, and is *Down* due some other reason.</span></span>  <span data-ttu-id="8b70d-141">Merhaba, *IsStopped* özelliktir true ve hello *NodeStatus* özelliği *aşağı*, hello düğümü geçiş API kullanarak durduruldu sonra.</span><span class="sxs-lookup"><span data-stu-id="8b70d-141">If hello *IsStopped* property is true, and hello *NodeStatus* property is *Down*, then it was stopped using hello Node Transition API.</span></span>

<span data-ttu-id="8b70d-142">Başlangıç bir *durduruldu* hello düğümü geçiş API kullanarak düğümüne döndürür, toofunction normal hello küme üyesi olarak yeniden.</span><span class="sxs-lookup"><span data-stu-id="8b70d-142">Starting a *stopped* node using hello Node Transition API will return it toofunction as a normal member of hello cluster again.</span></span>  <span data-ttu-id="8b70d-143">Merhaba hello düğümü sorgusu API çıktısını gösterir *IsStopped* false olarak ve *NodeStatus* aşağı (örneğin yukarı) olmayan bir şey olarak.</span><span class="sxs-lookup"><span data-stu-id="8b70d-143">hello output of hello node query API will show *IsStopped* as false, and *NodeStatus* as something that is not Down (e.g. Up).</span></span>


<span data-ttu-id="8b70d-144">**Sınırlı bir süre** hello düğümü geçiş API toostop bir düğüm kullanırken hello birini parametreleri, gerekli *stopNodeDurationInSeconds*, temsil hello süreyi saniye tookeep hello düğümünde  *durdurulmuş*.</span><span class="sxs-lookup"><span data-stu-id="8b70d-144">**Limited Duration** When using hello Node Transition API toostop a node, one of hello required parameters, *stopNodeDurationInSeconds*, represents hello amount of time in seconds tookeep hello node *stopped*.</span></span>  <span data-ttu-id="8b70d-145">Bu değer izin verilen 600 en az ve en fazla 14400 sahip aralık hello olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8b70d-145">This value must be in hello allowed range, which has a minimum of 600, and a maximum of 14400.</span></span>  <span data-ttu-id="8b70d-146">Bu süre dolduktan sonra hello düğüm kendi içine durumunu otomatik olarak yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="8b70d-146">After this time expires, hello node will restart itself into Up state automatically.</span></span>  <span data-ttu-id="8b70d-147">Kullanım örneği için tooSample 1 aşağıya bakın.</span><span class="sxs-lookup"><span data-stu-id="8b70d-147">Refer tooSample 1 below for an example of usage.</span></span>

> [!WARNING]
> <span data-ttu-id="8b70d-148">Düğüm geçiş API'leri karıştırma önlemek ve düğüm durdurmak ve başlatmak düğümü API'leri hello.</span><span class="sxs-lookup"><span data-stu-id="8b70d-148">Avoid mixing Node Transition APIs and hello Stop Node and Start Node APIs.</span></span>  <span data-ttu-id="8b70d-149">Merhaba çok başlangıç düğümü geçiş API yalnızca kullanılması önerilir.</span><span class="sxs-lookup"><span data-stu-id="8b70d-149">hello recommendation is too use hello Node Transition API only.</span></span>  <span data-ttu-id="8b70d-150">> Bir düğüm olup zaten yapıldıysa hello Durdur düğümü API kullanarak durduruldu, onu hello başlangıç düğümü API ilk hello kullanmadan önce kullanılarak başlatılmaması gerekir > düğümü geçiş API'leri.</span><span class="sxs-lookup"><span data-stu-id="8b70d-150">> If a node has been already been stopped using hello Stop Node API, it should be started using hello Start Node API first before using hello > Node Transition APIs.</span></span>

> [!WARNING]
> <span data-ttu-id="8b70d-151">Birden çok düğüm geçiş API çağrıları üzerinde yapılamaz aynı düğümde paralel hello.</span><span class="sxs-lookup"><span data-stu-id="8b70d-151">Multiple Node Transition APIs calls cannot be made on hello same node in parallel.</span></span>  <span data-ttu-id="8b70d-152">Merhaba düğümü geçiş API böyle bir durumda olacak > NodeTransitionInProgress ErrorCode özellik değeri olan bir FabricException atar.</span><span class="sxs-lookup"><span data-stu-id="8b70d-152">In such a situation, hello Node Transition API will    > throw a FabricException with an ErrorCode property value of NodeTransitionInProgress.</span></span>  <span data-ttu-id="8b70d-153">Belirli bir düğümde bir düğüm geçiş sonra > edilmiş hello işlemi başlamadan önce bir terminal durumu (tamamlandı, Faulted veya ForceCancelled) ulaşana kadar başlatıldı, beklemeniz gerekir bir > Yeni hello üzerinde aynı geçiş düğümü.</span><span class="sxs-lookup"><span data-stu-id="8b70d-153">Once a node transition on a specific node has  > been started, you should wait until hello operation reaches a terminal state (Completed, Faulted, or ForceCancelled) before starting a  > new transition on hello same node.</span></span>  <span data-ttu-id="8b70d-154">Paralel düğümü geçiş çağrıları farklı düğümlerde izin verilir.</span><span class="sxs-lookup"><span data-stu-id="8b70d-154">Parallel node transition calls on different nodes are allowed.</span></span>


#### <a name="sample-usage"></a><span data-ttu-id="8b70d-155">Örnek Kullanım</span><span class="sxs-lookup"><span data-stu-id="8b70d-155">Sample Usage</span></span>


<span data-ttu-id="8b70d-156">**Örnek 1** -örnek kullandığı aşağıdaki hello hello düğümü geçiş API toostop bir düğüm.</span><span class="sxs-lookup"><span data-stu-id="8b70d-156">**Sample 1** - hello following sample uses hello Node Transition API toostop a node.</span></span>

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

<span data-ttu-id="8b70d-157">**Örnek 2** - hello örnek başlatır izleyen bir *durduruldu* düğümü.</span><span class="sxs-lookup"><span data-stu-id="8b70d-157">**Sample 2** - hello following sample starts a *stopped* node.</span></span>  <span data-ttu-id="8b70d-158">Bazı yardımcı yöntemler hello ilk örnekten kullanır.</span><span class="sxs-lookup"><span data-stu-id="8b70d-158">It uses some helper methods from hello first sample.</span></span>

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

<span data-ttu-id="8b70d-159">**Örnek 3** - hello aşağıdaki örnek, yanlış kullanımı gösterir.</span><span class="sxs-lookup"><span data-stu-id="8b70d-159">**Sample 3** - hello following sample shows incorrect usage.</span></span>  <span data-ttu-id="8b70d-160">Bu kullanım yanlış olduğundan hello *stopDurationInSeconds* sağladığı izin verilen aralığın başlangıç daha büyük.</span><span class="sxs-lookup"><span data-stu-id="8b70d-160">This usage is incorrect because hello *stopDurationInSeconds* it provides is greater than hello allowed range.</span></span>  <span data-ttu-id="8b70d-161">StartNodeTransitionAsync() önemli bir hata ile başarısız olur bu yana hello işlemi kabul ve hello ilerleme API çağrılmamalı.</span><span class="sxs-lookup"><span data-stu-id="8b70d-161">Since StartNodeTransitionAsync() will fail with a fatal error, hello operation was not accepted, and hello progress API should not be called.</span></span>  <span data-ttu-id="8b70d-162">Bu örnek hello ilk örnekten bazı yardımcı yöntemler kullanır.</span><span class="sxs-lookup"><span data-stu-id="8b70d-162">This sample uses some helper methods from hello first sample.</span></span>

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

<span data-ttu-id="8b70d-163">**Örnek 4** - hello aşağıdaki örnek, başlangıç düğümü, geçiş ilerleme hello düğümü geçiş API tarafından başlatılan hello işlemi kabul edilir, ancak daha sonra yürütülürken başarısız olduğunda API sunucudan döndürülen hello hata bilgilerini gösterir.</span><span class="sxs-lookup"><span data-stu-id="8b70d-163">**Sample 4** - hello following sample shows hello error information that will be returned from hello Node Transition Progress API when hello operation initiated by hello Node Transition API is accepted, but fails later while executing.</span></span>  <span data-ttu-id="8b70d-164">Merhaba düğümü geçiş API toostart var olmayan bir düğüm çalıştığı hello durumda başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="8b70d-164">In hello case, it fails because hello Node Transition API attempts toostart a node that does not exist.</span></span>  <span data-ttu-id="8b70d-165">Bu örnek hello ilk örnekten bazı yardımcı yöntemler kullanır.</span><span class="sxs-lookup"><span data-stu-id="8b70d-165">This sample uses some helper methods from hello first sample.</span></span>

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
