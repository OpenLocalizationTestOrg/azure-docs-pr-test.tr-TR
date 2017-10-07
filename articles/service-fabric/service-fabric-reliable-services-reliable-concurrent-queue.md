---
title: Azure Service Fabric aaaReliableConcurrentQueue
description: "ReliableConcurrentQueue paralel enqueues sağlar ve dequeues yüksek verimlilik sırasıdır."
services: service-fabric
documentationcenter: .net
author: sangarg
manager: timlt
editor: raja,tyadam,masnider,vturecek
ms.assetid: 62857523-604b-434e-bd1c-2141ea4b00d1
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 5/1/2017
ms.author: sangarg
ms.openlocfilehash: 78a9905996b9ab265c1288d2b49753638d7bc445
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooreliableconcurrentqueue-in-azure-service-fabric"></a><span data-ttu-id="ea319-103">Azure Service Fabric içinde giriş tooReliableConcurrentQueue</span><span class="sxs-lookup"><span data-stu-id="ea319-103">Introduction tooReliableConcurrentQueue in Azure Service Fabric</span></span>
<span data-ttu-id="ea319-104">Güvenilir eşzamanlı sırası bir zaman uyumsuz işlem ve çoğaltılmış hangi özellikleri yüksek eşzamanlılık sıraya alma sıradır ve işlemleri dequeue.</span><span class="sxs-lookup"><span data-stu-id="ea319-104">Reliable Concurrent Queue is an asynchronous, transactional, and replicated queue which features high concurrency for enqueue and dequeue operations.</span></span> <span data-ttu-id="ea319-105">Tasarlanmış toodeliver yüksek verimlilik ve sakin hello katı FIFO tarafından sağlanan sıralama ile düşük gecikme süresi olan [güvenilir sıra](https://msdn.microsoft.com/library/azure/dn971527.aspx) ve bunun yerine bir en yüksek çaba sıralama sağlar.</span><span class="sxs-lookup"><span data-stu-id="ea319-105">It is designed toodeliver high throughput and low latency by relaxing hello strict FIFO ordering provided by [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) and instead provides a best-effort ordering.</span></span>

## <a name="apis"></a><span data-ttu-id="ea319-106">API'ler</span><span class="sxs-lookup"><span data-stu-id="ea319-106">APIs</span></span>

|<span data-ttu-id="ea319-107">Eşzamanlı sırası</span><span class="sxs-lookup"><span data-stu-id="ea319-107">Concurrent Queue</span></span>                |<span data-ttu-id="ea319-108">Güvenilir eşzamanlı sırası</span><span class="sxs-lookup"><span data-stu-id="ea319-108">Reliable Concurrent Queue</span></span>                                         |
|--------------------------------|------------------------------------------------------------------|
| <span data-ttu-id="ea319-109">void Enqueue(T item)</span><span class="sxs-lookup"><span data-stu-id="ea319-109">void Enqueue(T item)</span></span>           | <span data-ttu-id="ea319-110">Görev EnqueueAsync (ITransaction tx, T öğe)</span><span class="sxs-lookup"><span data-stu-id="ea319-110">Task EnqueueAsync(ITransaction tx, T item)</span></span>                       |
| <span data-ttu-id="ea319-111">bool TryDequeue (out T sonuç)</span><span class="sxs-lookup"><span data-stu-id="ea319-111">bool TryDequeue(out T result)</span></span>  | <span data-ttu-id="ea319-112">Görev < ConditionalValue < T >> TryDequeueAsync (ITransaction tx)</span><span class="sxs-lookup"><span data-stu-id="ea319-112">Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)</span></span>  |
| <span data-ttu-id="ea319-113">int Count()</span><span class="sxs-lookup"><span data-stu-id="ea319-113">int Count()</span></span>                    | <span data-ttu-id="ea319-114">uzun Count()</span><span class="sxs-lookup"><span data-stu-id="ea319-114">long Count()</span></span>                                                     |

## <a name="comparison-with-reliable-queuehttpsmsdnmicrosoftcomlibraryazuredn971527aspx"></a><span data-ttu-id="ea319-115">Karşılaştırma [güvenilir sırası](https://msdn.microsoft.com/library/azure/dn971527.aspx)</span><span class="sxs-lookup"><span data-stu-id="ea319-115">Comparison with [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx)</span></span>

<span data-ttu-id="ea319-116">Güvenilir eşzamanlı sıra sunulur alternatif olarak çok[güvenilir sıra](https://msdn.microsoft.com/library/azure/dn971527.aspx).</span><span class="sxs-lookup"><span data-stu-id="ea319-116">Reliable Concurrent Queue is offered as an alternative too[Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx).</span></span> <span data-ttu-id="ea319-117">Burada katı FIFO sıralama gerekli değildir, durumlarda kullanılmalıdır olarak FIFO gerektiren bir kolaylığını eşzamanlılık ile güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="ea319-117">It should be used in cases where strict FIFO ordering is not required, as guaranteeing FIFO requires a tradeoff with concurrency.</span></span>  <span data-ttu-id="ea319-118">[Güvenilir sıra](https://msdn.microsoft.com/library/azure/dn971527.aspx) kullanan kilitleri tooenforce FIFO, tooenqueue izin verilen en fazla bir işlem ile ve aynı anda toodequeue izin çoğu bir işlem sırası.</span><span class="sxs-lookup"><span data-stu-id="ea319-118">[Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) uses locks tooenforce FIFO ordering, with at most one transaction allowed tooenqueue and at most one transaction allowed toodequeue at a time.</span></span> <span data-ttu-id="ea319-119">Buna karşılık, güvenilir eşzamanlı sıra kısıtlaması sıralama hello rahatlatır ve kendi enqueue herhangi sayı eşzamanlı işlemler toointerleave sağlar ve işlemleri dequeue.</span><span class="sxs-lookup"><span data-stu-id="ea319-119">In comparison, Reliable Concurrent Queue relaxes hello ordering constraint and allows any number concurrent transactions toointerleave their enqueue and dequeue operations.</span></span> <span data-ttu-id="ea319-120">En yüksek çaba sıralama ancak hello göreli bir güvenilir eşzamanlı kuyruğundaki iki değer sıralamasını hiçbir zaman olabilir garanti sağlanmış.</span><span class="sxs-lookup"><span data-stu-id="ea319-120">Best-effort ordering is provided, however hello relative ordering of two values in a Reliable Concurrent Queue can never be guaranteed.</span></span>

<span data-ttu-id="ea319-121">Güvenilir eşzamanlı sıra daha yüksek verimlilik ve daha düşük gecikme sağlar [güvenilir sıra](https://msdn.microsoft.com/library/azure/dn971527.aspx) enqueues gerçekleştirme birden çok eşzamanlı işlem olduğunda ve/veya dequeues.</span><span class="sxs-lookup"><span data-stu-id="ea319-121">Reliable Concurrent Queue provides higher throughput and lower latency than [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) whenever there are multiple concurrent transactions performing enqueues and/or dequeues.</span></span>

<span data-ttu-id="ea319-122">Merhaba ReliableConcurrentQueue hello için örnek kullanım örneği [Message Queue](https://en.wikipedia.org/wiki/Message_queue) senaryo.</span><span class="sxs-lookup"><span data-stu-id="ea319-122">A sample use case for hello ReliableConcurrentQueue is hello [Message Queue](https://en.wikipedia.org/wiki/Message_queue) scenario.</span></span> <span data-ttu-id="ea319-123">Bu senaryoda, bir veya daha fazla ileti üreticileri oluşturun ve öğeleri toohello sıra ekleyin ve bir veya daha fazla ileti tüketiciye hello sırasından ileti çekmek ve işlenecekleri.</span><span class="sxs-lookup"><span data-stu-id="ea319-123">In this scenario, one or more message producers create and add items toohello queue, and one or more message consumers pull messages from hello queue and process them.</span></span> <span data-ttu-id="ea319-124">Birden çok üreticileri ve tüketicileri eşzamanlı işlemleri içinde sırasını tooprocess hello kullanma bağımsız olarak çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="ea319-124">Multiple producers and consumers can work independently, using concurrent transactions in order tooprocess hello queue.</span></span>

## <a name="usage-guidelines"></a><span data-ttu-id="ea319-125">Kullanım yönergeleri</span><span class="sxs-lookup"><span data-stu-id="ea319-125">Usage Guidelines</span></span>
* <span data-ttu-id="ea319-126">Merhaba sıra hello sırasındaki hello öğelerin bir düşük bekletme süresine sahip bekliyor.</span><span class="sxs-lookup"><span data-stu-id="ea319-126">hello queue expects that hello items in hello queue have a low retention period.</span></span> <span data-ttu-id="ea319-127">Diğer bir deyişle, hello öğeleri hello sırada uzun bir süredir kalmak değil.</span><span class="sxs-lookup"><span data-stu-id="ea319-127">That is, hello items would not stay in hello queue for a long time.</span></span>
* <span data-ttu-id="ea319-128">Merhaba sıra katı FIFO sıralama garanti etmez.</span><span class="sxs-lookup"><span data-stu-id="ea319-128">hello queue does not guarantee strict FIFO ordering.</span></span>
* <span data-ttu-id="ea319-129">Merhaba sıra kendi yazma okumaz.</span><span class="sxs-lookup"><span data-stu-id="ea319-129">hello queue does not read its own writes.</span></span> <span data-ttu-id="ea319-130">Bir öğe sıraya alınan bir işlem içinde ise, hello içinde görünür tooa dequeuer olmaz aynı işlem.</span><span class="sxs-lookup"><span data-stu-id="ea319-130">If an item is enqueued within a transaction, it will not be visible tooa dequeuer within hello same transaction.</span></span>
* <span data-ttu-id="ea319-131">Dequeues birbirinden yalıtılmış değildir.</span><span class="sxs-lookup"><span data-stu-id="ea319-131">Dequeues are not isolated from each other.</span></span> <span data-ttu-id="ea319-132">Öğesi, *A* işlemde kuyruktan çıkarıldı *txnA*rağmen *txnA* öğe kaydedilmiş, değil *A* görünür tooa eşzamanlı olmaz işlem *txnB*.</span><span class="sxs-lookup"><span data-stu-id="ea319-132">If item *A* is dequeued in transaction *txnA*, even though *txnA* is not committed, item *A* would not be visible tooa concurrent transaction *txnB*.</span></span>  <span data-ttu-id="ea319-133">Varsa *txnA* durdurur, *A* çok görünür olacak*txnB* hemen.</span><span class="sxs-lookup"><span data-stu-id="ea319-133">If *txnA* aborts, *A* will become visible too*txnB* immediately.</span></span>
* <span data-ttu-id="ea319-134">*TryPeekAsync* davranışı kullanarak uygulanabilir bir *TryDequeueAsync* ve hello işlemi iptal ediliyor.</span><span class="sxs-lookup"><span data-stu-id="ea319-134">*TryPeekAsync* behavior can be implemented by using a *TryDequeueAsync* and then aborting hello transaction.</span></span> <span data-ttu-id="ea319-135">Bunun bir örneğini hello programlama desenleri bölümünde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="ea319-135">An example of this can be found in hello Programming Patterns section.</span></span>
* <span data-ttu-id="ea319-136">İşlem olmayan sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="ea319-136">Count is non-transactional.</span></span> <span data-ttu-id="ea319-137">Kullanılan tooget hello hello kuyruğundaki öğelerin sayısı hakkında bir fikir olabilir ancak bir nokta zaman temsil eder ve bağlı dayanıyordu olamaz.</span><span class="sxs-lookup"><span data-stu-id="ea319-137">It can be used tooget an idea of hello number of elements in hello queue, but represents a point-in-time and cannot be relied upon.</span></span>
* <span data-ttu-id="ea319-138">Merhaba işlem etkinken pahalı hello üzerinde işleme öğeleri kuyruktan çıkarıldı gerçekleştirilmemelidir hello sistemde bir performans etkisi olabilir tooavoid uzun süre çalışan işlemleri.</span><span class="sxs-lookup"><span data-stu-id="ea319-138">Expensive processing on hello dequeued items should not be performed while hello transaction is active, tooavoid long-running transactions which may have a performance impact on hello system.</span></span>

## <a name="code-snippets"></a><span data-ttu-id="ea319-139">Kod parçacıkları</span><span class="sxs-lookup"><span data-stu-id="ea319-139">Code Snippets</span></span>
<span data-ttu-id="ea319-140">Bize birkaç kod parçacıkları ve bunların beklenen çıkış bakın.</span><span class="sxs-lookup"><span data-stu-id="ea319-140">Let us look at a few code snippets and their expected outputs.</span></span> <span data-ttu-id="ea319-141">Özel durum işleme, bu bölümde göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="ea319-141">Exception handling is ignored in this section.</span></span>

### <a name="enqueueasync"></a><span data-ttu-id="ea319-142">EnqueueAsync</span><span class="sxs-lookup"><span data-stu-id="ea319-142">EnqueueAsync</span></span>
<span data-ttu-id="ea319-143">Burada, kendi beklenen çıktı tarafından takip EnqueueAsync kullanmak için bazı kod parçacıkları bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ea319-143">Here are a few code snippets for using EnqueueAsync followed by their expected outputs.</span></span>

- <span data-ttu-id="ea319-144">*Durum 1: Tek bir Sıraya alma görevi*</span><span class="sxs-lookup"><span data-stu-id="ea319-144">*Case 1: Single Enqueue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="ea319-145">Bu hello görevi başarıyla tamamlandı varsayar ve, hello sıra değiştirme eşzamanlı işlem vardı.</span><span class="sxs-lookup"><span data-stu-id="ea319-145">Assume that hello task completed successfully, and that there were no concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="ea319-146">Merhaba kullanıcı hello kuyruk toocontain hello öğeleri siparişleri aşağıdaki hello hiçbirinde bekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ea319-146">hello user can expect hello queue toocontain hello items in any of hello following orders:</span></span>

> <span data-ttu-id="ea319-147">10, 20</span><span class="sxs-lookup"><span data-stu-id="ea319-147">10, 20</span></span>

> <span data-ttu-id="ea319-148">20, 10</span><span class="sxs-lookup"><span data-stu-id="ea319-148">20, 10</span></span>


- <span data-ttu-id="ea319-149">*Durum 2: Sıraya alma görev paralel*</span><span class="sxs-lookup"><span data-stu-id="ea319-149">*Case 2: Parallel Enqueue Task*</span></span>

```
// Parallel Task 1
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}

// Parallel Task 2
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 30, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 40, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="ea319-150">Merhaba görevleri hello görevleri paralel olarak çalışan ve hello sıra değiştirerek diğer eşzamanlı işlem vardı işleminin başarıyla tamamlandığını varsayalım.</span><span class="sxs-lookup"><span data-stu-id="ea319-150">Assume that hello tasks completed successfully, that hello tasks ran in parallel, and that there were no other concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="ea319-151">Hiçbir çıkarım hello hello kuyruğundaki öğelerin sırasını hakkında yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="ea319-151">No inference can be made about hello order of items in hello queue.</span></span> <span data-ttu-id="ea319-152">Bu kod parçacığını için hello öğeleri hello 4 hiçbirinde görünebilir!</span><span class="sxs-lookup"><span data-stu-id="ea319-152">For this code snippet, hello items may appear in any of hello 4!</span></span> <span data-ttu-id="ea319-153">olası sıralamalarını.</span><span class="sxs-lookup"><span data-stu-id="ea319-153">possible orderings.</span></span>  <span data-ttu-id="ea319-154">Merhaba sıra tookeep hello öğeleri hello özgün (sıradaki) sırada deneyecek, ancak zorlanmış tooreorder olabilir tooconcurrent operations veya hataları nedeniyle bunları.</span><span class="sxs-lookup"><span data-stu-id="ea319-154">hello queue will attempt tookeep hello items in hello original (enqueued) order, but may be forced tooreorder them due tooconcurrent operations or faults.</span></span>


### <a name="dequeueasync"></a><span data-ttu-id="ea319-155">DequeueAsync</span><span class="sxs-lookup"><span data-stu-id="ea319-155">DequeueAsync</span></span>
<span data-ttu-id="ea319-156">Burada, beklenen hello çıkışlar tarafından izlenen TryDequeueAsync kullanmak için bazı kod parçacıkları bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ea319-156">Here are a few code snippets for using TryDequeueAsync followed by hello expected outputs.</span></span> <span data-ttu-id="ea319-157">Bu hello kuyruğa zaten hello kuyruğundaki öğelerin aşağıdaki hello doldurulur varsayın:</span><span class="sxs-lookup"><span data-stu-id="ea319-157">Assume that hello queue is already populated with hello following items in hello queue:</span></span>
> <span data-ttu-id="ea319-158">10, 20, 30, 40, 50, 60</span><span class="sxs-lookup"><span data-stu-id="ea319-158">10, 20, 30, 40, 50, 60</span></span>

- <span data-ttu-id="ea319-159">*Durum 1: Tek Dequeue görevi*</span><span class="sxs-lookup"><span data-stu-id="ea319-159">*Case 1: Single Dequeue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="ea319-160">Bu hello görevi başarıyla tamamlandı varsayar ve, hello sıra değiştirme eşzamanlı işlem vardı.</span><span class="sxs-lookup"><span data-stu-id="ea319-160">Assume that hello task completed successfully, and that there were no concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="ea319-161">Merhaba hello sırasındaki hello öğelerin sırasını hakkında hiçbir çıkarımı yapılan bu yana herhangi üç hello öğelerinin, herhangi bir sırada kuyruktan çıkarıldı.</span><span class="sxs-lookup"><span data-stu-id="ea319-161">Since no inference can be made about hello order of hello items in hello queue, any three of hello items may be dequeued, in any order.</span></span> <span data-ttu-id="ea319-162">Merhaba sıra tookeep hello öğeleri hello özgün (sıradaki) sırada deneyecek, ancak zorlanmış tooreorder olabilir tooconcurrent operations veya hataları nedeniyle bunları.</span><span class="sxs-lookup"><span data-stu-id="ea319-162">hello queue will attempt tookeep hello items in hello original (enqueued) order, but may be forced tooreorder them due tooconcurrent operations or faults.</span></span>  

- <span data-ttu-id="ea319-163">*Durum 2: Paralel görev Dequeue*</span><span class="sxs-lookup"><span data-stu-id="ea319-163">*Case 2: Parallel Dequeue Task*</span></span>

```
// Parallel Task 1
List<int> dequeue1;
using (var txn = this.StateManager.CreateTransaction())
{
    dequeue1.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;
    dequeue1.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;

    await txn.CommitAsync();
}

// Parallel Task 2
List<int> dequeue2;
using (var txn = this.StateManager.CreateTransaction())
{
    dequeue2.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;
    dequeue2.Add(await this.Queue.TryDequeueAsync(txn, cancellationToken)).val;

    await txn.CommitAsync();
}
```

<span data-ttu-id="ea319-164">Merhaba görevleri hello görevleri paralel olarak çalışan ve hello sıra değiştirerek diğer eşzamanlı işlem vardı işleminin başarıyla tamamlandığını varsayalım.</span><span class="sxs-lookup"><span data-stu-id="ea319-164">Assume that hello tasks completed successfully, that hello tasks ran in parallel, and that there were no other concurrent transactions modifying hello queue.</span></span> <span data-ttu-id="ea319-165">Merhaba hello sırasındaki hello öğelerin sırasını hakkında hiçbir çıkarımı yapılan beri hello listeleri *dequeue1* ve *dequeue2* her herhangi bir sırada iki tüm öğeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="ea319-165">Since no inference can be made about hello order of hello items in hello queue, hello lists *dequeue1* and *dequeue2* will each contain any two items, in any order.</span></span>

<span data-ttu-id="ea319-166">aynı öğe olacak hello *değil* hem listelerde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ea319-166">hello same item will *not* appear in both lists.</span></span> <span data-ttu-id="ea319-167">Bu nedenle, dequeue1 varsa *10*, *30*, dequeue2 olacaktır *20*, *40*.</span><span class="sxs-lookup"><span data-stu-id="ea319-167">Hence, if dequeue1 has *10*, *30*, then dequeue2 would have *20*, *40*.</span></span>

- <span data-ttu-id="ea319-168">*Durum 3: İşlem iptali ile sıralama Dequeue*</span><span class="sxs-lookup"><span data-stu-id="ea319-168">*Case 3: Dequeue Ordering With Transaction Abort*</span></span>

<span data-ttu-id="ea319-169">Yürütülen olan bir işlem durduruluyor hello sıra hello başındaki hello öğeleri geri koyar dequeues.</span><span class="sxs-lookup"><span data-stu-id="ea319-169">Aborting a transaction with in-flight dequeues puts hello items back on hello head of hello queue.</span></span> <span data-ttu-id="ea319-170">içinde hello öğeleri hello sıra hello başındaki geri yerleştirilir hello sipariş garanti edilmez.</span><span class="sxs-lookup"><span data-stu-id="ea319-170">hello order in which hello items are put back on hello head of hello queue is not guaranteed.</span></span> <span data-ttu-id="ea319-171">Bize koddan hello bakın:</span><span class="sxs-lookup"><span data-stu-id="ea319-171">Let us look at hello following code:</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    // Abort hello transaction
    await txn.AbortAsync();
}
```
<span data-ttu-id="ea319-172">Merhaba öğeleri sırasının hello kuyruktan çıkarıldı varsayın:</span><span class="sxs-lookup"><span data-stu-id="ea319-172">Assume that hello items were dequeued in hello following order:</span></span>
> <span data-ttu-id="ea319-173">10, 20</span><span class="sxs-lookup"><span data-stu-id="ea319-173">10, 20</span></span>

<span data-ttu-id="ea319-174">Biz hello hareketi iptal zaman hello öğeleri geri toohello head hello sırasının siparişleri aşağıdaki hello hiçbirinde eklenir:</span><span class="sxs-lookup"><span data-stu-id="ea319-174">When we abort hello transaction, hello items would be added back toohello head of hello queue in any of hello following orders:</span></span>
> <span data-ttu-id="ea319-175">10, 20</span><span class="sxs-lookup"><span data-stu-id="ea319-175">10, 20</span></span>

> <span data-ttu-id="ea319-176">20, 10</span><span class="sxs-lookup"><span data-stu-id="ea319-176">20, 10</span></span>

<span data-ttu-id="ea319-177">Merhaba aynı burada hello işlem değildi başarıyla tüm durumlarda için geçerlidir *kabul edilen*.</span><span class="sxs-lookup"><span data-stu-id="ea319-177">hello same is true for all cases where hello transaction was not successfully *Committed*.</span></span>

## <a name="programming-patterns"></a><span data-ttu-id="ea319-178">Programlama desenleri</span><span class="sxs-lookup"><span data-stu-id="ea319-178">Programming Patterns</span></span>
<span data-ttu-id="ea319-179">Bu bölümde, bize en birkaç programlama ara desenleri ReliableConcurrentQueue kullanarak faydalı olabilir.</span><span class="sxs-lookup"><span data-stu-id="ea319-179">In this section, let us look at a few programming patterns that might be helpful in using ReliableConcurrentQueue.</span></span>

### <a name="batch-dequeues"></a><span data-ttu-id="ea319-180">Toplu Dequeues</span><span class="sxs-lookup"><span data-stu-id="ea319-180">Batch Dequeues</span></span>
<span data-ttu-id="ea319-181">A önerilir programlama düzeni hello Tüketici Görev toobatch için kendi bir gerçekleştirmek yerine dequeues aynı anda dequeue.</span><span class="sxs-lookup"><span data-stu-id="ea319-181">A recommended programming pattern is for hello consumer task toobatch its dequeues instead of performing one dequeue at a time.</span></span> <span data-ttu-id="ea319-182">Merhaba kullanıcı her toplu iş veya hello toplu iş boyutu arasındaki toothrottle gecikmelerini seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea319-182">hello user can choose toothrottle delays between every batch or hello batch size.</span></span> <span data-ttu-id="ea319-183">Merhaba aşağıdaki kod parçacığını bu programlama modeli gösterir.</span><span class="sxs-lookup"><span data-stu-id="ea319-183">hello following code snippet shows this programming model.</span></span>  <span data-ttu-id="ea319-184">Merhaba işlem kaydedildikten sonra bir hata işleme sırasında toooccur olsaydı, hello işlenmemiş öğeleri işlenmemiş olmadan kaybolacak Bu örnekte, hello işleme yapıldığını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ea319-184">Note that in this example, hello processing is done after hello transaction is committed, so if a fault were toooccur while processing, hello unprocessed items will be lost without having been processed.</span></span>  <span data-ttu-id="ea319-185">Alternatif olarak, hello işlem tamamlandı ancak bu performansı üzerinde olumsuz bir etkisi olabilir ve zaten işleme hello öğelerinin gerektirir hello hareketin kapsamı içinde işlenir.</span><span class="sxs-lookup"><span data-stu-id="ea319-185">Alternatively, hello processing can be done within hello transaction's scope, however this may have a negative impact on performance and requires handling of hello items already processed.</span></span>

```
int batchSize = 5;
long delayMs = 100;

while(!cancellationToken.IsCancellationRequested)
{
    // Buffer for dequeued items
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        ConditionalValue<int> ret;

        for(int i = 0; i < batchSize; ++i)
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if (ret.HasValue)
            {
                // If an item was dequeued, add toohello buffer for processing
                processItems.Add(ret.Value);
            }
            else
            {
                // else break hello for loop
                break;
            }
        }

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }

    int delayFactor = batchSize - processItems.Count;
    await Task.Delay(TimeSpan.FromMilliseconds(delayMs * delayFactor), cancellationToken);
}
```

### <a name="best-effort-notification-based-processing"></a><span data-ttu-id="ea319-186">En yüksek çaba bildirim tabanlı işleme</span><span class="sxs-lookup"><span data-stu-id="ea319-186">Best-Effort Notification-Based Processing</span></span>
<span data-ttu-id="ea319-187">Başka bir ilginç programlama modeli hello sayısı API kullanır.</span><span class="sxs-lookup"><span data-stu-id="ea319-187">Another interesting programming pattern uses hello Count API.</span></span> <span data-ttu-id="ea319-188">Burada, size en yüksek çaba bildirim tabanlı işleme hello sıranın uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea319-188">Here, we can implement best-effort notification-based processing for hello queue.</span></span> <span data-ttu-id="ea319-189">Merhaba sıra sayısı, sıraya alma bir kullanılan toothrottle veya dequeue görev olabilir.</span><span class="sxs-lookup"><span data-stu-id="ea319-189">hello queue Count can be used toothrottle an enqueue or a dequeue task.</span></span>  <span data-ttu-id="ea319-190">Merhaba işlem dışında Hello işleneceğini beri işleme sırasında bir hata oluşursa, hello önceki örnekte olduğu gibi işlenmemiş öğeleri kayıp olabileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ea319-190">Note that as in hello previous example, since hello processing occurs outside hello transaction, unprocessed items may be lost if a fault occurs during processing.</span></span>

```
int threshold = 5;
long delayMs = 1000;

while(!cancellationToken.IsCancellationRequested)
{
    while (this.Queue.Count < threshold)
    {
        cancellationToken.ThrowIfCancellationRequested();

        // If hello queue does not have hello threshold number of items, delay hello task and check again
        await Task.Delay(TimeSpan.FromMilliseconds(delayMs), cancellationToken);
    }

    // If there are approximately threshold number of items, try and process hello queue

    // Buffer for dequeued items
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        ConditionalValue<int> ret;

        do
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if (ret.HasValue)
            {
                // If an item was dequeued, add toohello buffer for processing
                processItems.Add(ret.Value);
            }
        } while (processItems.Count < threshold && ret.HasValue);

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
}
```

### <a name="best-effort-drain"></a><span data-ttu-id="ea319-191">En yüksek çaba boşaltma</span><span class="sxs-lookup"><span data-stu-id="ea319-191">Best-Effort Drain</span></span>
<span data-ttu-id="ea319-192">Merhaba sıra boşaltmayı toohello eşzamanlı yapısını hello veri yapısı garanti edilemez.</span><span class="sxs-lookup"><span data-stu-id="ea319-192">A drain of hello queue cannot be guaranteed due toohello concurrent nature of hello data structure.</span></span>  <span data-ttu-id="ea319-193">Bu olası belirli çağrı tooTryDequeueAsync, etkinliklerini hiçbir kullanıcı işlemleri hello sırasına yürütülen olsa bile, sıraya alınan önceden olan bir öğeyi döndürmeyebilir ve kaydedilmiş olur.</span><span class="sxs-lookup"><span data-stu-id="ea319-193">It is possible that, even if no user operations on hello queue are in-flight, a particular call tooTryDequeueAsync may not return an item which was previously enqueued and committed.</span></span>  <span data-ttu-id="ea319-194">Merhaba sıraya alınan öğe çok garanti*sonunda* bir bant dışı iletişim mekanizması kararlı durum olsa bile bu hello sıraya ulaştı bağımsız bir tüketici bilemezsiniz ancak görünür toodequeue hale tüm üreticileri durdurulur ve yeni bir Sıraya alma işlemlerine izin verilir.</span><span class="sxs-lookup"><span data-stu-id="ea319-194">hello enqueued item is guaranteed too*eventually* become visible toodequeue, however without an out-of-band communication mechanism, an independent consumer cannot know that hello queue has reached a steady-state even if all producers have been stopped and no new enqueue operations are allowed.</span></span> <span data-ttu-id="ea319-195">Bu nedenle, hello boşaltma en altına uygulandığı gibi yüksek çaba işlemdir.</span><span class="sxs-lookup"><span data-stu-id="ea319-195">Thus, hello drain operation is best-effort as implemented below.</span></span>

<span data-ttu-id="ea319-196">Hello kullanıcı tüm başka üretici ve tüketici görevleri durdurmak ve herhangi bir yürütülen işlemler toocommit veya toodrain hello sırası çalışmadan önce iptal beklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ea319-196">hello user should stop all further producer and consumer tasks, and wait for any in-flight transactions toocommit or abort, before attempting toodrain hello queue.</span></span>  <span data-ttu-id="ea319-197">Merhaba kullanıcı hello kuyruğundaki öğelerin sayısı beklenen hello biliyorsa, bunlar tüm öğeleri kuyruktan çıkarıldı sinyalleri bir bildirim ayarlayalım ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ea319-197">If hello user knows hello expected number of items in hello queue, they can set up a notification which signals that all items have been dequeued.</span></span>

```
int numItemsDequeued;
int batchSize = 5;

ConditionalValue ret;

do
{
    List<int> processItems = new List<int>();

    using (var txn = this.StateManager.CreateTransaction())
    {
        do
        {
            ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);

            if(ret.HasValue)
            {
                // Buffer hello dequeues
                processItems.Add(ret.Value);
            }
        } while (ret.HasValue && processItems.Count < batchSize);

        await txn.CommitAsync();
    }

    // Process hello dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
} while (ret.HasValue);
```

### <a name="peek"></a><span data-ttu-id="ea319-198">Göz At</span><span class="sxs-lookup"><span data-stu-id="ea319-198">Peek</span></span>
<span data-ttu-id="ea319-199">ReliableConcurrentQueue hello sağlamaz *TryPeekAsync* API.</span><span class="sxs-lookup"><span data-stu-id="ea319-199">ReliableConcurrentQueue does not provide hello *TryPeekAsync* api.</span></span> <span data-ttu-id="ea319-200">Kullanıcıların alabilirsiniz hello gözlem anlamsal kullanarak bir *TryDequeueAsync* ve hello işlemi iptal ediliyor.</span><span class="sxs-lookup"><span data-stu-id="ea319-200">Users can get hello peek semantic by using a *TryDequeueAsync* and then aborting hello transaction.</span></span> <span data-ttu-id="ea319-201">Bu örnekte, dequeues yalnızca hello öğenin değeri büyükse işlenen *10*.</span><span class="sxs-lookup"><span data-stu-id="ea319-201">In this example, dequeues are processed only if hello item's value is greater than *10*.</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    ConditionalValue ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);
    bool valueProcessed = false;

    if (ret.HasValue)
    {
        if (ret.Value > 10)
        {
            // Process hello item
            Console.WriteLine("Value : " + ret.Value);
            valueProcessed = true;
        }
    }

    if (valueProcessed)
    {
        await txn.CommitAsync();    
    }
    else
    {
        await txn.AbortAsync();
    }
}
```

## <a name="must-read"></a><span data-ttu-id="ea319-202">Okuma olmalıdır</span><span class="sxs-lookup"><span data-stu-id="ea319-202">Must Read</span></span>
* [<span data-ttu-id="ea319-203">Güvenilir hizmetler hızlı başlangıç</span><span class="sxs-lookup"><span data-stu-id="ea319-203">Reliable Services Quick Start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="ea319-204">Güvenilir Koleksiyonlar ile çalışma</span><span class="sxs-lookup"><span data-stu-id="ea319-204">Working with Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="ea319-205">Güvenilir hizmetler bildirimleri</span><span class="sxs-lookup"><span data-stu-id="ea319-205">Reliable Services notifications</span></span>](service-fabric-reliable-services-notifications.md)
* [<span data-ttu-id="ea319-206">Güvenilir hizmetler yedekleme ve geri yükleme (olağanüstü durum kurtarma)</span><span class="sxs-lookup"><span data-stu-id="ea319-206">Reliable Services Backup and Restore (Disaster Recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="ea319-207">Güvenilir durum Yöneticisi yapılandırması</span><span class="sxs-lookup"><span data-stu-id="ea319-207">Reliable State Manager Configuration</span></span>](service-fabric-reliable-services-configuration.md)
* [<span data-ttu-id="ea319-208">Service Fabric Web API Hizmetleri'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="ea319-208">Getting Started with Service Fabric Web API Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="ea319-209">Gelişmiş kullanımını hello güvenilir Hizmetleri programlama modeli</span><span class="sxs-lookup"><span data-stu-id="ea319-209">Advanced Usage of hello Reliable Services Programming Model</span></span>](service-fabric-reliable-services-advanced-usage.md)
* [<span data-ttu-id="ea319-210">Güvenilir koleksiyonlar için Geliştirici Başvurusu</span><span class="sxs-lookup"><span data-stu-id="ea319-210">Developer Reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
