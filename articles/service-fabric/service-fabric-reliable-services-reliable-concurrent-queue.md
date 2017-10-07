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
# <a name="introduction-tooreliableconcurrentqueue-in-azure-service-fabric"></a>Azure Service Fabric içinde giriş tooReliableConcurrentQueue
Güvenilir eşzamanlı sırası bir zaman uyumsuz işlem ve çoğaltılmış hangi özellikleri yüksek eşzamanlılık sıraya alma sıradır ve işlemleri dequeue. Tasarlanmış toodeliver yüksek verimlilik ve sakin hello katı FIFO tarafından sağlanan sıralama ile düşük gecikme süresi olan [güvenilir sıra](https://msdn.microsoft.com/library/azure/dn971527.aspx) ve bunun yerine bir en yüksek çaba sıralama sağlar.

## <a name="apis"></a>API'ler

|Eşzamanlı sırası                |Güvenilir eşzamanlı sırası                                         |
|--------------------------------|------------------------------------------------------------------|
| void Enqueue(T item)           | Görev EnqueueAsync (ITransaction tx, T öğe)                       |
| bool TryDequeue (out T sonuç)  | Görev < ConditionalValue < T >> TryDequeueAsync (ITransaction tx)  |
| int Count()                    | uzun Count()                                                     |

## <a name="comparison-with-reliable-queuehttpsmsdnmicrosoftcomlibraryazuredn971527aspx"></a>Karşılaştırma [güvenilir sırası](https://msdn.microsoft.com/library/azure/dn971527.aspx)

Güvenilir eşzamanlı sıra sunulur alternatif olarak çok[güvenilir sıra](https://msdn.microsoft.com/library/azure/dn971527.aspx). Burada katı FIFO sıralama gerekli değildir, durumlarda kullanılmalıdır olarak FIFO gerektiren bir kolaylığını eşzamanlılık ile güvence altına alır.  [Güvenilir sıra](https://msdn.microsoft.com/library/azure/dn971527.aspx) kullanan kilitleri tooenforce FIFO, tooenqueue izin verilen en fazla bir işlem ile ve aynı anda toodequeue izin çoğu bir işlem sırası. Buna karşılık, güvenilir eşzamanlı sıra kısıtlaması sıralama hello rahatlatır ve kendi enqueue herhangi sayı eşzamanlı işlemler toointerleave sağlar ve işlemleri dequeue. En yüksek çaba sıralama ancak hello göreli bir güvenilir eşzamanlı kuyruğundaki iki değer sıralamasını hiçbir zaman olabilir garanti sağlanmış.

Güvenilir eşzamanlı sıra daha yüksek verimlilik ve daha düşük gecikme sağlar [güvenilir sıra](https://msdn.microsoft.com/library/azure/dn971527.aspx) enqueues gerçekleştirme birden çok eşzamanlı işlem olduğunda ve/veya dequeues.

Merhaba ReliableConcurrentQueue hello için örnek kullanım örneği [Message Queue](https://en.wikipedia.org/wiki/Message_queue) senaryo. Bu senaryoda, bir veya daha fazla ileti üreticileri oluşturun ve öğeleri toohello sıra ekleyin ve bir veya daha fazla ileti tüketiciye hello sırasından ileti çekmek ve işlenecekleri. Birden çok üreticileri ve tüketicileri eşzamanlı işlemleri içinde sırasını tooprocess hello kullanma bağımsız olarak çalışabilir.

## <a name="usage-guidelines"></a>Kullanım yönergeleri
* Merhaba sıra hello sırasındaki hello öğelerin bir düşük bekletme süresine sahip bekliyor. Diğer bir deyişle, hello öğeleri hello sırada uzun bir süredir kalmak değil.
* Merhaba sıra katı FIFO sıralama garanti etmez.
* Merhaba sıra kendi yazma okumaz. Bir öğe sıraya alınan bir işlem içinde ise, hello içinde görünür tooa dequeuer olmaz aynı işlem.
* Dequeues birbirinden yalıtılmış değildir. Öğesi, *A* işlemde kuyruktan çıkarıldı *txnA*rağmen *txnA* öğe kaydedilmiş, değil *A* görünür tooa eşzamanlı olmaz işlem *txnB*.  Varsa *txnA* durdurur, *A* çok görünür olacak*txnB* hemen.
* *TryPeekAsync* davranışı kullanarak uygulanabilir bir *TryDequeueAsync* ve hello işlemi iptal ediliyor. Bunun bir örneğini hello programlama desenleri bölümünde bulunabilir.
* İşlem olmayan sayısıdır. Kullanılan tooget hello hello kuyruğundaki öğelerin sayısı hakkında bir fikir olabilir ancak bir nokta zaman temsil eder ve bağlı dayanıyordu olamaz.
* Merhaba işlem etkinken pahalı hello üzerinde işleme öğeleri kuyruktan çıkarıldı gerçekleştirilmemelidir hello sistemde bir performans etkisi olabilir tooavoid uzun süre çalışan işlemleri.

## <a name="code-snippets"></a>Kod parçacıkları
Bize birkaç kod parçacıkları ve bunların beklenen çıkış bakın. Özel durum işleme, bu bölümde göz ardı edilir.

### <a name="enqueueasync"></a>EnqueueAsync
Burada, kendi beklenen çıktı tarafından takip EnqueueAsync kullanmak için bazı kod parçacıkları bulunmaktadır.

- *Durum 1: Tek bir Sıraya alma görevi*

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.EnqueueAsync(txn, 10, cancellationToken);
    await this.Queue.EnqueueAsync(txn, 20, cancellationToken);

    await txn.CommitAsync();
}
```

Bu hello görevi başarıyla tamamlandı varsayar ve, hello sıra değiştirme eşzamanlı işlem vardı. Merhaba kullanıcı hello kuyruk toocontain hello öğeleri siparişleri aşağıdaki hello hiçbirinde bekleyebilirsiniz:

> 10, 20

> 20, 10


- *Durum 2: Sıraya alma görev paralel*

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

Merhaba görevleri hello görevleri paralel olarak çalışan ve hello sıra değiştirerek diğer eşzamanlı işlem vardı işleminin başarıyla tamamlandığını varsayalım. Hiçbir çıkarım hello hello kuyruğundaki öğelerin sırasını hakkında yapılabilir. Bu kod parçacığını için hello öğeleri hello 4 hiçbirinde görünebilir! olası sıralamalarını.  Merhaba sıra tookeep hello öğeleri hello özgün (sıradaki) sırada deneyecek, ancak zorlanmış tooreorder olabilir tooconcurrent operations veya hataları nedeniyle bunları.


### <a name="dequeueasync"></a>DequeueAsync
Burada, beklenen hello çıkışlar tarafından izlenen TryDequeueAsync kullanmak için bazı kod parçacıkları bulunmaktadır. Bu hello kuyruğa zaten hello kuyruğundaki öğelerin aşağıdaki hello doldurulur varsayın:
> 10, 20, 30, 40, 50, 60

- *Durum 1: Tek Dequeue görevi*

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    await txn.CommitAsync();
}
```

Bu hello görevi başarıyla tamamlandı varsayar ve, hello sıra değiştirme eşzamanlı işlem vardı. Merhaba hello sırasındaki hello öğelerin sırasını hakkında hiçbir çıkarımı yapılan bu yana herhangi üç hello öğelerinin, herhangi bir sırada kuyruktan çıkarıldı. Merhaba sıra tookeep hello öğeleri hello özgün (sıradaki) sırada deneyecek, ancak zorlanmış tooreorder olabilir tooconcurrent operations veya hataları nedeniyle bunları.  

- *Durum 2: Paralel görev Dequeue*

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

Merhaba görevleri hello görevleri paralel olarak çalışan ve hello sıra değiştirerek diğer eşzamanlı işlem vardı işleminin başarıyla tamamlandığını varsayalım. Merhaba hello sırasındaki hello öğelerin sırasını hakkında hiçbir çıkarımı yapılan beri hello listeleri *dequeue1* ve *dequeue2* her herhangi bir sırada iki tüm öğeleri içerir.

aynı öğe olacak hello *değil* hem listelerde görüntülenir. Bu nedenle, dequeue1 varsa *10*, *30*, dequeue2 olacaktır *20*, *40*.

- *Durum 3: İşlem iptali ile sıralama Dequeue*

Yürütülen olan bir işlem durduruluyor hello sıra hello başındaki hello öğeleri geri koyar dequeues. içinde hello öğeleri hello sıra hello başındaki geri yerleştirilir hello sipariş garanti edilmez. Bize koddan hello bakın:

```
using (var txn = this.StateManager.CreateTransaction())
{
    await this.Queue.TryDequeueAsync(txn, cancellationToken);
    await this.Queue.TryDequeueAsync(txn, cancellationToken);

    // Abort hello transaction
    await txn.AbortAsync();
}
```
Merhaba öğeleri sırasının hello kuyruktan çıkarıldı varsayın:
> 10, 20

Biz hello hareketi iptal zaman hello öğeleri geri toohello head hello sırasının siparişleri aşağıdaki hello hiçbirinde eklenir:
> 10, 20

> 20, 10

Merhaba aynı burada hello işlem değildi başarıyla tüm durumlarda için geçerlidir *kabul edilen*.

## <a name="programming-patterns"></a>Programlama desenleri
Bu bölümde, bize en birkaç programlama ara desenleri ReliableConcurrentQueue kullanarak faydalı olabilir.

### <a name="batch-dequeues"></a>Toplu Dequeues
A önerilir programlama düzeni hello Tüketici Görev toobatch için kendi bir gerçekleştirmek yerine dequeues aynı anda dequeue. Merhaba kullanıcı her toplu iş veya hello toplu iş boyutu arasındaki toothrottle gecikmelerini seçebilirsiniz. Merhaba aşağıdaki kod parçacığını bu programlama modeli gösterir.  Merhaba işlem kaydedildikten sonra bir hata işleme sırasında toooccur olsaydı, hello işlenmemiş öğeleri işlenmemiş olmadan kaybolacak Bu örnekte, hello işleme yapıldığını unutmayın.  Alternatif olarak, hello işlem tamamlandı ancak bu performansı üzerinde olumsuz bir etkisi olabilir ve zaten işleme hello öğelerinin gerektirir hello hareketin kapsamı içinde işlenir.

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

### <a name="best-effort-notification-based-processing"></a>En yüksek çaba bildirim tabanlı işleme
Başka bir ilginç programlama modeli hello sayısı API kullanır. Burada, size en yüksek çaba bildirim tabanlı işleme hello sıranın uygulayabilirsiniz. Merhaba sıra sayısı, sıraya alma bir kullanılan toothrottle veya dequeue görev olabilir.  Merhaba işlem dışında Hello işleneceğini beri işleme sırasında bir hata oluşursa, hello önceki örnekte olduğu gibi işlenmemiş öğeleri kayıp olabileceğini unutmayın.

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

### <a name="best-effort-drain"></a>En yüksek çaba boşaltma
Merhaba sıra boşaltmayı toohello eşzamanlı yapısını hello veri yapısı garanti edilemez.  Bu olası belirli çağrı tooTryDequeueAsync, etkinliklerini hiçbir kullanıcı işlemleri hello sırasına yürütülen olsa bile, sıraya alınan önceden olan bir öğeyi döndürmeyebilir ve kaydedilmiş olur.  Merhaba sıraya alınan öğe çok garanti*sonunda* bir bant dışı iletişim mekanizması kararlı durum olsa bile bu hello sıraya ulaştı bağımsız bir tüketici bilemezsiniz ancak görünür toodequeue hale tüm üreticileri durdurulur ve yeni bir Sıraya alma işlemlerine izin verilir. Bu nedenle, hello boşaltma en altına uygulandığı gibi yüksek çaba işlemdir.

Hello kullanıcı tüm başka üretici ve tüketici görevleri durdurmak ve herhangi bir yürütülen işlemler toocommit veya toodrain hello sırası çalışmadan önce iptal beklemeniz gerekir.  Merhaba kullanıcı hello kuyruğundaki öğelerin sayısı beklenen hello biliyorsa, bunlar tüm öğeleri kuyruktan çıkarıldı sinyalleri bir bildirim ayarlayalım ayarlayabilirsiniz.

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

### <a name="peek"></a>Göz At
ReliableConcurrentQueue hello sağlamaz *TryPeekAsync* API. Kullanıcıların alabilirsiniz hello gözlem anlamsal kullanarak bir *TryDequeueAsync* ve hello işlemi iptal ediliyor. Bu örnekte, dequeues yalnızca hello öğenin değeri büyükse işlenen *10*.

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

## <a name="must-read"></a>Okuma olmalıdır
* [Güvenilir hizmetler hızlı başlangıç](service-fabric-reliable-services-quick-start.md)
* [Güvenilir Koleksiyonlar ile çalışma](service-fabric-work-with-reliable-collections.md)
* [Güvenilir hizmetler bildirimleri](service-fabric-reliable-services-notifications.md)
* [Güvenilir hizmetler yedekleme ve geri yükleme (olağanüstü durum kurtarma)](service-fabric-reliable-services-backup-restore.md)
* [Güvenilir durum Yöneticisi yapılandırması](service-fabric-reliable-services-configuration.md)
* [Service Fabric Web API Hizmetleri'ni kullanmaya başlama](service-fabric-reliable-services-communication-webapi.md)
* [Gelişmiş kullanımını hello güvenilir Hizmetleri programlama modeli](service-fabric-reliable-services-advanced-usage.md)
* [Güvenilir koleksiyonlar için Geliştirici Başvurusu](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)
