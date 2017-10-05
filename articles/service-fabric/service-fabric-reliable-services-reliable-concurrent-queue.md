---
title: Azure Service Fabric ReliableConcurrentQueue
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
ms.openlocfilehash: 122cb48149477f295a65b8ee623c647b6db10a86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="introduction-to-reliableconcurrentqueue-in-azure-service-fabric"></a><span data-ttu-id="930b6-103">Azure Service Fabric ReliableConcurrentQueue giriş</span><span class="sxs-lookup"><span data-stu-id="930b6-103">Introduction to ReliableConcurrentQueue in Azure Service Fabric</span></span>
<span data-ttu-id="930b6-104">Güvenilir eşzamanlı sırası bir zaman uyumsuz işlem ve çoğaltılmış hangi özellikleri yüksek eşzamanlılık sıraya alma sıradır ve işlemleri dequeue.</span><span class="sxs-lookup"><span data-stu-id="930b6-104">Reliable Concurrent Queue is an asynchronous, transactional, and replicated queue which features high concurrency for enqueue and dequeue operations.</span></span> <span data-ttu-id="930b6-105">Tarafından sağlanan sıralama, katı FIFO gevşetme tarafından yüksek verimlilik ve düşük gecikme süresi sunacak şekilde tasarlanan [güvenilir sıra](https://msdn.microsoft.com/library/azure/dn971527.aspx) ve bunun yerine bir en yüksek çaba sıralama sağlar.</span><span class="sxs-lookup"><span data-stu-id="930b6-105">It is designed to deliver high throughput and low latency by relaxing the strict FIFO ordering provided by [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) and instead provides a best-effort ordering.</span></span>

## <a name="apis"></a><span data-ttu-id="930b6-106">API'ler</span><span class="sxs-lookup"><span data-stu-id="930b6-106">APIs</span></span>

|<span data-ttu-id="930b6-107">Eşzamanlı sırası</span><span class="sxs-lookup"><span data-stu-id="930b6-107">Concurrent Queue</span></span>                |<span data-ttu-id="930b6-108">Güvenilir eşzamanlı sırası</span><span class="sxs-lookup"><span data-stu-id="930b6-108">Reliable Concurrent Queue</span></span>                                         |
|--------------------------------|------------------------------------------------------------------|
| <span data-ttu-id="930b6-109">void Enqueue(T item)</span><span class="sxs-lookup"><span data-stu-id="930b6-109">void Enqueue(T item)</span></span>           | <span data-ttu-id="930b6-110">Görev EnqueueAsync (ITransaction tx, T öğe)</span><span class="sxs-lookup"><span data-stu-id="930b6-110">Task EnqueueAsync(ITransaction tx, T item)</span></span>                       |
| <span data-ttu-id="930b6-111">bool TryDequeue (out T sonuç)</span><span class="sxs-lookup"><span data-stu-id="930b6-111">bool TryDequeue(out T result)</span></span>  | <span data-ttu-id="930b6-112">Görev < ConditionalValue < T >> TryDequeueAsync (ITransaction tx)</span><span class="sxs-lookup"><span data-stu-id="930b6-112">Task< ConditionalValue < T > > TryDequeueAsync(ITransaction tx)</span></span>  |
| <span data-ttu-id="930b6-113">int Count()</span><span class="sxs-lookup"><span data-stu-id="930b6-113">int Count()</span></span>                    | <span data-ttu-id="930b6-114">uzun Count()</span><span class="sxs-lookup"><span data-stu-id="930b6-114">long Count()</span></span>                                                     |

## <a name="comparison-with-reliable-queuehttpsmsdnmicrosoftcomlibraryazuredn971527aspx"></a><span data-ttu-id="930b6-115">Karşılaştırma [güvenilir sırası](https://msdn.microsoft.com/library/azure/dn971527.aspx)</span><span class="sxs-lookup"><span data-stu-id="930b6-115">Comparison with [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx)</span></span>

<span data-ttu-id="930b6-116">Alternatif olarak güvenilir eşzamanlı sıra sunulan [güvenilir sıra](https://msdn.microsoft.com/library/azure/dn971527.aspx).</span><span class="sxs-lookup"><span data-stu-id="930b6-116">Reliable Concurrent Queue is offered as an alternative to [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx).</span></span> <span data-ttu-id="930b6-117">Burada katı FIFO sıralama gerekli değildir, durumlarda kullanılmalıdır olarak FIFO gerektiren bir kolaylığını eşzamanlılık ile güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="930b6-117">It should be used in cases where strict FIFO ordering is not required, as guaranteeing FIFO requires a tradeoff with concurrency.</span></span>  <span data-ttu-id="930b6-118">[Güvenilir sıra](https://msdn.microsoft.com/library/azure/dn971527.aspx) sıraya alma için izin verilen en fazla bir işlem ve aynı anda dequeue izin verilen en fazla bir işlem ile FIFO sıralama zorlamak için kilitler kullanır.</span><span class="sxs-lookup"><span data-stu-id="930b6-118">[Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) uses locks to enforce FIFO ordering, with at most one transaction allowed to enqueue and at most one transaction allowed to dequeue at a time.</span></span> <span data-ttu-id="930b6-119">Buna karşılık, güvenilir eşzamanlı sıra sıralama kısıtlaması rahatlatır ve bunların enqueue Interleave ve işlemleri dequeue sayı eşzamanlı işlemler sağlar.</span><span class="sxs-lookup"><span data-stu-id="930b6-119">In comparison, Reliable Concurrent Queue relaxes the ordering constraint and allows any number concurrent transactions to interleave their enqueue and dequeue operations.</span></span> <span data-ttu-id="930b6-120">En yüksek çaba sıralama ancak güvenilir eşzamanlı sıradaki iki değer göreli sıralamasını hiçbir zaman olabilir garanti sağlanmış.</span><span class="sxs-lookup"><span data-stu-id="930b6-120">Best-effort ordering is provided, however the relative ordering of two values in a Reliable Concurrent Queue can never be guaranteed.</span></span>

<span data-ttu-id="930b6-121">Güvenilir eşzamanlı sıra daha yüksek verimlilik ve daha düşük gecikme sağlar [güvenilir sıra](https://msdn.microsoft.com/library/azure/dn971527.aspx) enqueues gerçekleştirme birden çok eşzamanlı işlem olduğunda ve/veya dequeues.</span><span class="sxs-lookup"><span data-stu-id="930b6-121">Reliable Concurrent Queue provides higher throughput and lower latency than [Reliable Queue](https://msdn.microsoft.com/library/azure/dn971527.aspx) whenever there are multiple concurrent transactions performing enqueues and/or dequeues.</span></span>

<span data-ttu-id="930b6-122">Örnek Kullanım örneği ReliableConcurrentQueue için [Message Queue](https://en.wikipedia.org/wiki/Message_queue) senaryo.</span><span class="sxs-lookup"><span data-stu-id="930b6-122">A sample use case for the ReliableConcurrentQueue is the [Message Queue](https://en.wikipedia.org/wiki/Message_queue) scenario.</span></span> <span data-ttu-id="930b6-123">Bu senaryoda, bir veya daha fazla ileti üreticileri oluşturun ve öğeleri kuyruğa ekleyin ve bir veya daha fazla ileti tüketiciye sırasından ileti çekmek ve işlenecekleri.</span><span class="sxs-lookup"><span data-stu-id="930b6-123">In this scenario, one or more message producers create and add items to the queue, and one or more message consumers pull messages from the queue and process them.</span></span> <span data-ttu-id="930b6-124">Birden çok üreticileri ve tüketicileri sırasını işlemek için eş zamanlı işlemleri kullanarak bağımsız olarak çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="930b6-124">Multiple producers and consumers can work independently, using concurrent transactions in order to process the queue.</span></span>

## <a name="usage-guidelines"></a><span data-ttu-id="930b6-125">Kullanım yönergeleri</span><span class="sxs-lookup"><span data-stu-id="930b6-125">Usage Guidelines</span></span>
* <span data-ttu-id="930b6-126">Sıranın kuyruğundaki öğelerin düşük saklama dönemi olmasını bekliyor.</span><span class="sxs-lookup"><span data-stu-id="930b6-126">The queue expects that the items in the queue have a low retention period.</span></span> <span data-ttu-id="930b6-127">Diğer bir deyişle, öğeleri sıraya uzun bir süredir kalmak değil.</span><span class="sxs-lookup"><span data-stu-id="930b6-127">That is, the items would not stay in the queue for a long time.</span></span>
* <span data-ttu-id="930b6-128">Sıranın katı FIFO sıralama garanti etmez.</span><span class="sxs-lookup"><span data-stu-id="930b6-128">The queue does not guarantee strict FIFO ordering.</span></span>
* <span data-ttu-id="930b6-129">Sıranın kendi yazma okumaz.</span><span class="sxs-lookup"><span data-stu-id="930b6-129">The queue does not read its own writes.</span></span> <span data-ttu-id="930b6-130">Bir öğe sıraya alınan bir işlem içinde ise, aynı işlem içinde dequeuer için görünür olmaz.</span><span class="sxs-lookup"><span data-stu-id="930b6-130">If an item is enqueued within a transaction, it will not be visible to a dequeuer within the same transaction.</span></span>
* <span data-ttu-id="930b6-131">Dequeues birbirinden yalıtılmış değildir.</span><span class="sxs-lookup"><span data-stu-id="930b6-131">Dequeues are not isolated from each other.</span></span> <span data-ttu-id="930b6-132">Öğesi, *A* işlemde kuyruktan çıkarıldı *txnA*rağmen *txnA* öğe kaydedilmiş, değil *A* eşzamanlı bir işlem için görünür olmaz *txnB*.</span><span class="sxs-lookup"><span data-stu-id="930b6-132">If item *A* is dequeued in transaction *txnA*, even though *txnA* is not committed, item *A* would not be visible to a concurrent transaction *txnB*.</span></span>  <span data-ttu-id="930b6-133">Varsa *txnA* durdurur, *A* için görünür olacak *txnB* hemen.</span><span class="sxs-lookup"><span data-stu-id="930b6-133">If *txnA* aborts, *A* will become visible to *txnB* immediately.</span></span>
* <span data-ttu-id="930b6-134">*TryPeekAsync* davranışı kullanarak uygulanabilir bir *TryDequeueAsync* ve işlem iptal ediliyor.</span><span class="sxs-lookup"><span data-stu-id="930b6-134">*TryPeekAsync* behavior can be implemented by using a *TryDequeueAsync* and then aborting the transaction.</span></span> <span data-ttu-id="930b6-135">Buna örnek olarak programlama desenleri bölümünde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="930b6-135">An example of this can be found in the Programming Patterns section.</span></span>
* <span data-ttu-id="930b6-136">İşlem olmayan sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="930b6-136">Count is non-transactional.</span></span> <span data-ttu-id="930b6-137">Kuyrukta, öğelerin sayısı hakkında bir fikir edinmek için kullanılabilir, ancak bir nokta zaman temsil eder ve bağlı dayanıyordu olamaz.</span><span class="sxs-lookup"><span data-stu-id="930b6-137">It can be used to get an idea of the number of elements in the queue, but represents a point-in-time and cannot be relied upon.</span></span>
* <span data-ttu-id="930b6-138">İşlem bir performans etkisi sistemde olabilir uzun süre çalışan işlemleri önlemek için etkin durumdayken dequeued öğeleri üzerindeki pahalı işleme gerçekleştirilmemelidir.</span><span class="sxs-lookup"><span data-stu-id="930b6-138">Expensive processing on the dequeued items should not be performed while the transaction is active, to avoid long-running transactions which may have a performance impact on the system.</span></span>

## <a name="code-snippets"></a><span data-ttu-id="930b6-139">Kod parçacıkları</span><span class="sxs-lookup"><span data-stu-id="930b6-139">Code Snippets</span></span>
<span data-ttu-id="930b6-140">Bize birkaç kod parçacıkları ve bunların beklenen çıkış bakın.</span><span class="sxs-lookup"><span data-stu-id="930b6-140">Let us look at a few code snippets and their expected outputs.</span></span> <span data-ttu-id="930b6-141">Özel durum işleme, bu bölümde göz ardı edilir.</span><span class="sxs-lookup"><span data-stu-id="930b6-141">Exception handling is ignored in this section.</span></span>

### <a name="enqueueasync"></a><span data-ttu-id="930b6-142">EnqueueAsync</span><span class="sxs-lookup"><span data-stu-id="930b6-142">EnqueueAsync</span></span>
<span data-ttu-id="930b6-143">Burada, kendi beklenen çıktı tarafından takip EnqueueAsync kullanmak için bazı kod parçacıkları bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="930b6-143">Here are a few code snippets for using EnqueueAsync followed by their expected outputs.</span></span>

- <span data-ttu-id="930b6-144">*Durum 1: Tek bir Sıraya alma görevi*</span><span class="sxs-lookup"><span data-stu-id="930b6-144">*Case 1: Single Enqueue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="930b6-145">Görevi başarıyla tamamlandı ve o orada sıranın değiştirme eşzamanlı işlem olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="930b6-145">Assume that the task completed successfully, and that there were no concurrent transactions modifying the queue.</span></span> <span data-ttu-id="930b6-146">Kullanıcı öğelerinin herhangi birinde aşağıdaki siparişleri bulunduğu için kuyruğa bekleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="930b6-146">The user can expect the queue to contain the items in any of the following orders:</span></span>

> <span data-ttu-id="930b6-147">10, 20</span><span class="sxs-lookup"><span data-stu-id="930b6-147">10, 20</span></span>

> <span data-ttu-id="930b6-148">20, 10</span><span class="sxs-lookup"><span data-stu-id="930b6-148">20, 10</span></span>


- <span data-ttu-id="930b6-149">*Durum 2: Sıraya alma görev paralel*</span><span class="sxs-lookup"><span data-stu-id="930b6-149">*Case 2: Parallel Enqueue Task*</span></span>

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

<span data-ttu-id="930b6-150">Görevleri görevleri paralel olarak çalışan ve sıranın değiştirilmesi diğer eşzamanlı işlem vardı işleminin başarıyla tamamlandığını varsayalım.</span><span class="sxs-lookup"><span data-stu-id="930b6-150">Assume that the tasks completed successfully, that the tasks ran in parallel, and that there were no other concurrent transactions modifying the queue.</span></span> <span data-ttu-id="930b6-151">Hiçbir çıkarım kuyruğundaki öğelerin sırasını hakkında yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="930b6-151">No inference can be made about the order of items in the queue.</span></span> <span data-ttu-id="930b6-152">Bu kod parçacığını için öğeleri 4 hiçbirinde görünebilir!</span><span class="sxs-lookup"><span data-stu-id="930b6-152">For this code snippet, the items may appear in any of the 4!</span></span> <span data-ttu-id="930b6-153">olası sıralamalarını.</span><span class="sxs-lookup"><span data-stu-id="930b6-153">possible orderings.</span></span>  <span data-ttu-id="930b6-154">Sıranın özgün (sıradaki) sırayla öğeleri tutmak deneyecek, ancak bunları eşzamanlı işlem veya hataları nedeniyle yeniden sıralamak için zorlanabilir.</span><span class="sxs-lookup"><span data-stu-id="930b6-154">The queue will attempt to keep the items in the original (enqueued) order, but may be forced to reorder them due to concurrent operations or faults.</span></span>


### <a name="dequeueasync"></a><span data-ttu-id="930b6-155">DequeueAsync</span><span class="sxs-lookup"><span data-stu-id="930b6-155">DequeueAsync</span></span>
<span data-ttu-id="930b6-156">Burada, beklenen çıktı tarafından takip TryDequeueAsync kullanmak için bazı kod parçacıkları bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="930b6-156">Here are a few code snippets for using TryDequeueAsync followed by the expected outputs.</span></span> <span data-ttu-id="930b6-157">Sıranın sırasındaki aşağıdaki öğelerin ile önceden doldurulur varsayın:</span><span class="sxs-lookup"><span data-stu-id="930b6-157">Assume that the queue is already populated with the following items in the queue:</span></span>
> <span data-ttu-id="930b6-158">10, 20, 30, 40, 50, 60</span><span class="sxs-lookup"><span data-stu-id="930b6-158">10, 20, 30, 40, 50, 60</span></span>

- <span data-ttu-id="930b6-159">*Durum 1: Tek Dequeue görevi*</span><span class="sxs-lookup"><span data-stu-id="930b6-159">*Case 1: Single Dequeue Task*</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    await txn.CommitAsync();
}
```

<span data-ttu-id="930b6-160">Görevi başarıyla tamamlandı ve o orada sıranın değiştirme eşzamanlı işlem olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="930b6-160">Assume that the task completed successfully, and that there were no concurrent transactions modifying the queue.</span></span> <span data-ttu-id="930b6-161">Kuyruğundaki öğelerin sırasını hakkında hiçbir çıkarımı yapılan olduğundan, tüm üç öğe, herhangi bir sırada kuyruktan çıkarıldı.</span><span class="sxs-lookup"><span data-stu-id="930b6-161">Since no inference can be made about the order of the items in the queue, any three of the items may be dequeued, in any order.</span></span> <span data-ttu-id="930b6-162">Sıranın özgün (sıradaki) sırayla öğeleri tutmak deneyecek, ancak bunları eşzamanlı işlem veya hataları nedeniyle yeniden sıralamak için zorlanabilir.</span><span class="sxs-lookup"><span data-stu-id="930b6-162">The queue will attempt to keep the items in the original (enqueued) order, but may be forced to reorder them due to concurrent operations or faults.</span></span>  

- <span data-ttu-id="930b6-163">*Durum 2: Paralel görev Dequeue*</span><span class="sxs-lookup"><span data-stu-id="930b6-163">*Case 2: Parallel Dequeue Task*</span></span>

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

<span data-ttu-id="930b6-164">Görevleri görevleri paralel olarak çalışan ve sıranın değiştirilmesi diğer eşzamanlı işlem vardı işleminin başarıyla tamamlandığını varsayalım.</span><span class="sxs-lookup"><span data-stu-id="930b6-164">Assume that the tasks completed successfully, that the tasks ran in parallel, and that there were no other concurrent transactions modifying the queue.</span></span> <span data-ttu-id="930b6-165">Listeler kuyruğundaki öğelerin sırasını hakkında hiçbir çıkarımı yapılan bu yana *dequeue1* ve *dequeue2* her herhangi bir sırada iki tüm öğeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="930b6-165">Since no inference can be made about the order of the items in the queue, the lists *dequeue1* and *dequeue2* will each contain any two items, in any order.</span></span>

<span data-ttu-id="930b6-166">Aynı öğe *değil* hem listelerde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="930b6-166">The same item will *not* appear in both lists.</span></span> <span data-ttu-id="930b6-167">Bu nedenle, dequeue1 varsa *10*, *30*, dequeue2 olacaktır *20*, *40*.</span><span class="sxs-lookup"><span data-stu-id="930b6-167">Hence, if dequeue1 has *10*, *30*, then dequeue2 would have *20*, *40*.</span></span>

- <span data-ttu-id="930b6-168">*Durum 3: İşlem iptali ile sıralama Dequeue*</span><span class="sxs-lookup"><span data-stu-id="930b6-168">*Case 3: Dequeue Ordering With Transaction Abort*</span></span>

<span data-ttu-id="930b6-169">Yürütülen olan bir işlem durduruluyor sıranın head üzerinde öğeleri geri koyar dequeues.</span><span class="sxs-lookup"><span data-stu-id="930b6-169">Aborting a transaction with in-flight dequeues puts the items back on the head of the queue.</span></span> <span data-ttu-id="930b6-170">Hangi öğelerin sıra head üzerinde geri getirilme sırasını garanti edilmez.</span><span class="sxs-lookup"><span data-stu-id="930b6-170">The order in which the items are put back on the head of the queue is not guaranteed.</span></span> <span data-ttu-id="930b6-171">Bize aşağıdaki koda bakın:</span><span class="sxs-lookup"><span data-stu-id="930b6-171">Let us look at the following code:</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    // Abort the transaction
    await txn.AbortAsync();
}
```
<span data-ttu-id="930b6-172">Öğeleri aşağıdaki sırayla kuyruktan çıkarıldı varsayın:</span><span class="sxs-lookup"><span data-stu-id="930b6-172">Assume that the items were dequeued in the following order:</span></span>
> <span data-ttu-id="930b6-173">10, 20</span><span class="sxs-lookup"><span data-stu-id="930b6-173">10, 20</span></span>

<span data-ttu-id="930b6-174">Biz hareketi iptal, öğeleri aşağıdaki siparişleri hiçbirinde sırasının head dön eklenir:</span><span class="sxs-lookup"><span data-stu-id="930b6-174">When we abort the transaction, the items would be added back to the head of the queue in any of the following orders:</span></span>
> <span data-ttu-id="930b6-175">10, 20</span><span class="sxs-lookup"><span data-stu-id="930b6-175">10, 20</span></span>

> <span data-ttu-id="930b6-176">20, 10</span><span class="sxs-lookup"><span data-stu-id="930b6-176">20, 10</span></span>

<span data-ttu-id="930b6-177">Aynı işlem bulunduğu değil başarıyla tüm durumlarda geçerlidir *kabul edilen*.</span><span class="sxs-lookup"><span data-stu-id="930b6-177">The same is true for all cases where the transaction was not successfully *Committed*.</span></span>

## <a name="programming-patterns"></a><span data-ttu-id="930b6-178">Programlama desenleri</span><span class="sxs-lookup"><span data-stu-id="930b6-178">Programming Patterns</span></span>
<span data-ttu-id="930b6-179">Bu bölümde, bize en birkaç programlama ara desenleri ReliableConcurrentQueue kullanarak faydalı olabilir.</span><span class="sxs-lookup"><span data-stu-id="930b6-179">In this section, let us look at a few programming patterns that might be helpful in using ReliableConcurrentQueue.</span></span>

### <a name="batch-dequeues"></a><span data-ttu-id="930b6-180">Toplu Dequeues</span><span class="sxs-lookup"><span data-stu-id="930b6-180">Batch Dequeues</span></span>
<span data-ttu-id="930b6-181">A önerilir programlama düzeni toplu tüketici görevi için bir gerçekleştirmek yerine dequeues aynı anda dequeue.</span><span class="sxs-lookup"><span data-stu-id="930b6-181">A recommended programming pattern is for the consumer task to batch its dequeues instead of performing one dequeue at a time.</span></span> <span data-ttu-id="930b6-182">Kullanıcının her toplu iş veya toplu iş boyutu arasındaki gecikmelerini kısıtlama seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="930b6-182">The user can choose to throttle delays between every batch or the batch size.</span></span> <span data-ttu-id="930b6-183">Aşağıdaki kod parçacığını bu programlama modeli gösterir.</span><span class="sxs-lookup"><span data-stu-id="930b6-183">The following code snippet shows this programming model.</span></span>  <span data-ttu-id="930b6-184">Bu örnekte unutmayın, işlem kaydedildikten sonra bir arıza işlenirken meydana olsaydı, işlenmemiş öğeleri işlenmemiş olmadan kaybolacak işlem yapılmaz.</span><span class="sxs-lookup"><span data-stu-id="930b6-184">Note that in this example, the processing is done after the transaction is committed, so if a fault were to occur while processing, the unprocessed items will be lost without having been processed.</span></span>  <span data-ttu-id="930b6-185">Alternatif olarak, bu performansı üzerinde olumsuz bir etkisi olabilir ve önceden işlenmiş öğelerinin işleme gerektirir ancak işleme işlemdeki kapsamında yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="930b6-185">Alternatively, the processing can be done within the transaction's scope, however this may have a negative impact on performance and requires handling of the items already processed.</span></span>

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
                // If an item was dequeued, add to the buffer for processing
                processItems.Add(ret.Value);
            }
            else
            {
                // else break the for loop
                break;
            }
        }

        await txn.CommitAsync();
    }

    // Process the dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }

    int delayFactor = batchSize - processItems.Count;
    await Task.Delay(TimeSpan.FromMilliseconds(delayMs * delayFactor), cancellationToken);
}
```

### <a name="best-effort-notification-based-processing"></a><span data-ttu-id="930b6-186">En yüksek çaba bildirim tabanlı işleme</span><span class="sxs-lookup"><span data-stu-id="930b6-186">Best-Effort Notification-Based Processing</span></span>
<span data-ttu-id="930b6-187">Başka bir ilginç programlama modeli sayısı API kullanır.</span><span class="sxs-lookup"><span data-stu-id="930b6-187">Another interesting programming pattern uses the Count API.</span></span> <span data-ttu-id="930b6-188">Burada, size en yüksek çaba bildirim tabanlı sıra için işlem uygulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="930b6-188">Here, we can implement best-effort notification-based processing for the queue.</span></span> <span data-ttu-id="930b6-189">Sıra sayısı bir sıraya veya bir dequeue görev kısıtlama için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="930b6-189">The queue Count can be used to throttle an enqueue or a dequeue task.</span></span>  <span data-ttu-id="930b6-190">İşlem dışında işleneceğini beri işleme sırasında bir hata oluşursa, önceki örnekte olduğu gibi işlenmemiş öğeleri kayıp olabileceğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="930b6-190">Note that as in the previous example, since the processing occurs outside the transaction, unprocessed items may be lost if a fault occurs during processing.</span></span>

```
int threshold = 5;
long delayMs = 1000;

while(!cancellationToken.IsCancellationRequested)
{
    while (this.Queue.Count < threshold)
    {
        cancellationToken.ThrowIfCancellationRequested();

        // If the queue does not have the threshold number of items, delay the task and check again
        await Task.Delay(TimeSpan.FromMilliseconds(delayMs), cancellationToken);
    }

    // If there are approximately threshold number of items, try and process the queue

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
                // If an item was dequeued, add to the buffer for processing
                processItems.Add(ret.Value);
            }
        } while (processItems.Count < threshold && ret.HasValue);

        await txn.CommitAsync();
    }

    // Process the dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
}
```

### <a name="best-effort-drain"></a><span data-ttu-id="930b6-191">En yüksek çaba boşaltma</span><span class="sxs-lookup"><span data-stu-id="930b6-191">Best-Effort Drain</span></span>
<span data-ttu-id="930b6-192">Sıranın boşaltmayı veri yapısı eşzamanlı yapısı nedeniyle garanti edilemez.</span><span class="sxs-lookup"><span data-stu-id="930b6-192">A drain of the queue cannot be guaranteed due to the concurrent nature of the data structure.</span></span>  <span data-ttu-id="930b6-193">Bu olası TryDequeueAsync belirli bir çağrı, etkinliklerini sırada hiçbir kullanıcı işlemleri yürütülen olsa bile, sıraya alınan önceden olan bir öğeyi döndürmeyebilir ve kaydedilmiş olur.</span><span class="sxs-lookup"><span data-stu-id="930b6-193">It is possible that, even if no user operations on the queue are in-flight, a particular call to TryDequeueAsync may not return an item which was previously enqueued and committed.</span></span>  <span data-ttu-id="930b6-194">Sıraya alınan öğe garanti *sonunda* dequeue için bir bant dışı iletişim mekanizması bağımsız bir tüketici sıranın kararlı durum tüm üreticileri durduruldu ve hiç yeni sıraya alma işlemlerine izin verildiğinden olsa bile ulaştı ancak bilemezsiniz görünür hale gelmiştir.</span><span class="sxs-lookup"><span data-stu-id="930b6-194">The enqueued item is guaranteed to *eventually* become visible to dequeue, however without an out-of-band communication mechanism, an independent consumer cannot know that the queue has reached a steady-state even if all producers have been stopped and no new enqueue operations are allowed.</span></span> <span data-ttu-id="930b6-195">Bu nedenle, boşaltma en altına uygulandığı gibi yüksek çaba işlemdir.</span><span class="sxs-lookup"><span data-stu-id="930b6-195">Thus, the drain operation is best-effort as implemented below.</span></span>

<span data-ttu-id="930b6-196">Kullanıcı tüm başka üretici ve tüketici görevleri durdurmak ve tamamlanmaya veya iptal, sıranın boşaltmak denemeden önce yürütülen işlemler için beklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="930b6-196">The user should stop all further producer and consumer tasks, and wait for any in-flight transactions to commit or abort, before attempting to drain the queue.</span></span>  <span data-ttu-id="930b6-197">Kullanıcı beklenen kuyruğundaki öğelerin sayısı biliyorsa, bunlar tüm öğeleri kuyruktan çıkarıldı sinyalleri bir bildirim ayarlayalım ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="930b6-197">If the user knows the expected number of items in the queue, they can set up a notification which signals that all items have been dequeued.</span></span>

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
                // Buffer the dequeues
                processItems.Add(ret.Value);
            }
        } while (ret.HasValue && processItems.Count < batchSize);

        await txn.CommitAsync();
    }

    // Process the dequeues
    for (int i = 0; i < processItems.Count; ++i)
    {
        Console.WriteLine("Value : " + processItems[i]);
    }
} while (ret.HasValue);
```

### <a name="peek"></a><span data-ttu-id="930b6-198">Göz At</span><span class="sxs-lookup"><span data-stu-id="930b6-198">Peek</span></span>
<span data-ttu-id="930b6-199">ReliableConcurrentQueue sağlamaz *TryPeekAsync* API.</span><span class="sxs-lookup"><span data-stu-id="930b6-199">ReliableConcurrentQueue does not provide the *TryPeekAsync* api.</span></span> <span data-ttu-id="930b6-200">Kullanıcıların alabilirsiniz gözlem anlamsal kullanarak bir *TryDequeueAsync* ve işlem iptal ediliyor.</span><span class="sxs-lookup"><span data-stu-id="930b6-200">Users can get the peek semantic by using a *TryDequeueAsync* and then aborting the transaction.</span></span> <span data-ttu-id="930b6-201">Bu örnekte, dequeues yalnızca öğenin değeri büyükse işlenen *10*.</span><span class="sxs-lookup"><span data-stu-id="930b6-201">In this example, dequeues are processed only if the item's value is greater than *10*.</span></span>

```
using (var txn = this.StateManager.CreateTransaction())
{
    ConditionalValue ret = await this.Queue.TryDequeueAsync(txn, cancellationToken);
    bool valueProcessed = false;

    if (ret.HasValue)
    {
        if (ret.Value > 10)
        {
            // Process the item
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

## <a name="must-read"></a><span data-ttu-id="930b6-202">Okuma olmalıdır</span><span class="sxs-lookup"><span data-stu-id="930b6-202">Must Read</span></span>
* [<span data-ttu-id="930b6-203">Güvenilir hizmetler hızlı başlangıç</span><span class="sxs-lookup"><span data-stu-id="930b6-203">Reliable Services Quick Start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="930b6-204">Güvenilir Koleksiyonlar ile çalışma</span><span class="sxs-lookup"><span data-stu-id="930b6-204">Working with Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="930b6-205">Güvenilir hizmetler bildirimleri</span><span class="sxs-lookup"><span data-stu-id="930b6-205">Reliable Services notifications</span></span>](service-fabric-reliable-services-notifications.md)
* [<span data-ttu-id="930b6-206">Güvenilir hizmetler yedekleme ve geri yükleme (olağanüstü durum kurtarma)</span><span class="sxs-lookup"><span data-stu-id="930b6-206">Reliable Services Backup and Restore (Disaster Recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="930b6-207">Güvenilir durum Yöneticisi yapılandırması</span><span class="sxs-lookup"><span data-stu-id="930b6-207">Reliable State Manager Configuration</span></span>](service-fabric-reliable-services-configuration.md)
* [<span data-ttu-id="930b6-208">Service Fabric Web API Hizmetleri'ni kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="930b6-208">Getting Started with Service Fabric Web API Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="930b6-209">Gelişmiş kullanımını programlama modeli güvenilir hizmetler</span><span class="sxs-lookup"><span data-stu-id="930b6-209">Advanced Usage of the Reliable Services Programming Model</span></span>](service-fabric-reliable-services-advanced-usage.md)
* [<span data-ttu-id="930b6-210">Güvenilir koleksiyonlar için Geliştirici Başvurusu</span><span class="sxs-lookup"><span data-stu-id="930b6-210">Developer Reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
