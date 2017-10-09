---
title: aaaReliable Hizmetleri bildirimleri | Microsoft Docs
description: "Service Fabric Reliable Services bildirimler için kavramsal belgeler"
services: service-fabric
documentationcenter: .net
author: mcoskun
manager: timlt
editor: masnider,vturecek
ms.assetid: cdc918dd-5e81-49c8-a03d-7ddcd12a9a76
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 6/29/2017
ms.author: mcoskun
ms.openlocfilehash: 8c43190d31dbe82d1dc7fa1c228128bdcc3684f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-services-notifications"></a>Güvenilir hizmetler bildirimleri
Bildirimleri istemcileri ilginizi tooan nesne yapılan tootrack hello değişiklikler sağlar. İki nesne türünün destek bildirimleri: *güvenilir durum Yöneticisi* ve *güvenilir sözlük*.

Bildirimleri kullanmak için yaygın nedenler şunlardır:

* Yapı ikincil dizinler gibi görünümlerde gerçekleştirilip veya filtrelenmiş görünümleri hello yinelemenin durumunun bir araya getirilir. Bir örnek, güvenilir sözlükteki tüm anahtarları sıralanmış bir dizindir.
* Gönderen izleme gibi verileri hello hello son bir saat eklenen kullanıcıların sayısı.

Bildirimleri işlemleri uygulama bir parçası olarak tetiklenir. Bu yüzden, olası ve zaman uyumlu olaylar pahalı işlemleri eklememelisiniz kadar hızlı bildirimleri yapılmalıdır.

## <a name="reliable-state-manager-notifications"></a>Güvenilir durum Yöneticisi bildirimleri
Güvenilir durumu Yöneticisi olayları aşağıdaki hello için bildirimleri sağlar:

* İşlem
  * İşleme
* Durum Yöneticisi
  * Yeniden oluşturma
  * Güvenilir bir duruma eklenmesi
  * Güvenilir durumunun kaldırma

Güvenilir durum Yöneticisi hello geçerli inflight işlemleri izler. harekete bir bildirim toobe neden olan işlem durumunda Hello yalnızca değişiklik yürütme bir işlemdir.

Güvenilir durum Yöneticisi güvenilir sözlük ve güvenilir sırası gibi güvenilir durumları koleksiyonu tutar. Güvenilir durum Yöneticisi bu koleksiyon değiştiğinde bildirim ateşlenir: güvenilir durumu eklendiğinde veya kaldırıldığında ya da hello tüm koleksiyon yeniden.
Merhaba güvenilir durum Yöneticisi koleksiyonu üç durumda yeniden oluşturulur:

* Kurtarma: bir çoğaltma başladığında, önceki durumuna hello diskten kurtarır. Kurtarma Hello sonunda kullandığı **NotifyStateManagerChangedEventArgs** toofire kurtarılan güvenilir durumları hello kümesini içeren bir olay.
* Tam kopyalama: bir çoğaltma hello yapılandırma kümesi katılabilmesi için önce yerleşik toobe sahiptir. Bazı durumlarda, bu hello birincil çoğaltma toobe uygulanan toohello boşta ikincil çoğaltma güvenilir durum yöneticisinin durumundan tam bir kopyasını gerektirir. Merhaba ikincil çoğaltma kullanan güvenilir durumu Yöneticisi **NotifyStateManagerChangedEventArgs** toofire hello birincil çoğaltmadan edinilen güvenilir durumları hello kümesini içeren bir olay.
* Geri yükleme: olağanüstü durum kurtarma senaryolarında hello yinelemenin durumu bir yedekten geri yüklenebilir **RestoreAsync**. Böyle durumlarda, güvenilir durum Yöneticisi hello birincil çoğaltmadaki kullanan **NotifyStateManagerChangedEventArgs** toofire hello yedekten geri güvenilir durumları hello kümesini içeren bir olay.

tooregister işlem bildirimleri ve/veya durum Yöneticisi bildirimleri için gereksinim duyduğunuz hello ile tooregister **TransactionChanged** veya **StateManagerChanged** güvenilir durumu Yöneticisi olayları. Ortak bir yerde tooregister bu olay işleyicileri ile olan durum bilgisi olan hizmetinizin hello Oluşturucusu. Merhaba Oluşturucu kaydederken hello ömrü sırasında bir değişiklik nedeniyle herhangi bir bildirim kaçırılması olmaz **IReliableStateManager**.

```C#
public MyService(StatefulServiceContext context)
    : base(MyService.EndpointName, context, CreateReliableStateManager(context))
{
    this.StateManager.TransactionChanged += this.OnTransactionChangedHandler;
    this.StateManager.StateManagerChanged += this.OnStateManagerChangedHandler;
}
```

Merhaba **TransactionChanged** olay işleyicisi kullanan **NotifyTransactionChangedEventArgs** tooprovide hello Olay Ayrıntıları. Merhaba eylem özelliği içerir (örneğin, **NotifyTransactionChangedAction.Commit**) değişikliğin hello türünü belirtir. Ayrıca, değiştirilmiş bir başvuru toohello işlem sağlar hello TRANSACTION özelliği içerir.

> [!NOTE]
> Bugün, **TransactionChanged** yalnızca hello hareket tamamlanırsa olayları ortaya çıkar. Merhaba eylem sonra çok eşittir**NotifyTransactionChangedAction.Commit**. Ancak işlem durumu değişiklikleri diğer türleri için olayları hello gelecekteki, yükseltilmiş. Merhaba eylem denetleme ve yalnızca bu beklediğiniz ise hello olayı işleme öneririz.
> 
> 

Aşağıda bir örnek verilmiştir **TransactionChanged** olay işleyicisi.

```C#
private void OnTransactionChangedHandler(object sender, NotifyTransactionChangedEventArgs e)
{
    if (e.Action == NotifyTransactionChangedAction.Commit)
    {
        this.lastCommitLsn = e.Transaction.CommitSequenceNumber;
        this.lastTransactionId = e.Transaction.TransactionId;

        this.lastCommittedTransactionList.Add(e.Transaction.TransactionId);
    }
}
```

Merhaba **StateManagerChanged** olay işleyicisi kullanan **NotifyStateManagerChangedEventArgs** tooprovide hello Olay Ayrıntıları.
**NotifyStateManagerChangedEventArgs** iki alt sınıfları olmayan: **NotifyStateManagerRebuildEventArgs** ve **NotifyStateManagerSingleEntityChangedEventArgs**.
Merhaba eylem özelliğinde kullanmak **NotifyStateManagerChangedEventArgs** toocast **NotifyStateManagerChangedEventArgs** toohello doğru alt:

* **NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**
* **NotifyStateManagerChangedAction.Add** ve **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**

Aşağıda bir örnek verilmiştir **StateManagerChanged** bildirim işleyici.

```C#
public void OnStateManagerChangedHandler(object sender, NotifyStateManagerChangedEventArgs e)
{
    if (e.Action == NotifyStateManagerChangedAction.Rebuild)
    {
        this.ProcessStataManagerRebuildNotification(e);

        return;
    }

    this.ProcessStateManagerSingleEntityNotification(e);
}
```

## <a name="reliable-dictionary-notifications"></a>Güvenilir sözlük bildirimleri
Güvenilir sözlük olayları aşağıdaki hello için bildirimleri sağlar:

* Yeniden oluşturma: çağrılır **ReliableDictionary** durumuna kurtarılan ya da kopyalanmış yerel durumu ya da yedekleme kurtarıldı.
* Clear: çağrılır hello durumunu **ReliableDictionary** hello temizlenmiş **ClearAsync** yöntemi.
* Ekleyin: adlı bir öğe çok eklendiğinde**ReliableDictionary**.
* Güncelleştirme: bir öğe olarak adlandırılan **IReliableDictionary** güncelleştirildi.
* Kaldır: bir öğe adlı **IReliableDictionary** silinmiş olabilir.

tooget güvenilir sözlük bildirimleri, gereksinim duyduğunuz hello ile tooregister **DictionaryChanged** olay işleyicisini **IReliableDictionary**. Ortak bir yerde tooregister bu olay işleyicileri ile olan hello **ReliableStateManager.StateManagerChanged** bildirim ekleyin.
Ne zaman kaydetme **IReliableDictionary** çok eklenen**IReliableStateManager** herhangi bir bildirim kaçırılması olmaz sağlar.

```C#
private void ProcessStateManagerSingleEntityNotification(NotifyStateManagerChangedEventArgs e)
{
    var operation = e as NotifyStateManagerSingleEntityChangedEventArgs;

    if (operation.Action == NotifyStateManagerChangedAction.Add)
    {
        if (operation.ReliableState is IReliableDictionary<TKey, TValue>)
        {
            var dictionary = (IReliableDictionary<TKey, TValue>)operation.ReliableState;
            dictionary.RebuildNotificationAsyncCallback = this.OnDictionaryRebuildNotificationHandlerAsync;
            dictionary.DictionaryChanged += this.OnDictionaryChangedHandler;
            }
        }
    }
}
```

> [!NOTE]
> **ProcessStateManagerSingleEntityNotification** hello örnek yöntemidir önceki bu hello **OnStateManagerChangedHandler** örnek çağrıları.
> 
> 

Merhaba önceki kod ayarlar hello **IReliableNotificationAsyncCallback** , bunların ile arabirim **DictionaryChanged**. Çünkü **NotifyDictionaryRebuildEventArgs** içeren bir **IAsyncEnumerable** arabirimi--, zaman uyumsuz olarak--numaralandırılan toobe gereken yeniden bildirimleri aracılığıyla harekete  **RebuildNotificationAsyncCallback** yerine **OnDictionaryChangedHandler**.

```C#
public async Task OnDictionaryRebuildNotificationHandlerAsync(
    IReliableDictionary<TKey, TValue> origin,
    NotifyDictionaryRebuildEventArgs<TKey, TValue> rebuildNotification)
{
    this.secondaryIndex.Clear();

    var enumerator = e.State.GetAsyncEnumerator();
    while (await enumerator.MoveNextAsync(CancellationToken.None))
    {
        this.secondaryIndex.Add(enumerator.Current.Key, enumerator.Current.Value);
    }
}
```

> [!NOTE]
> İşleme hello yeniden bildirimi, bir parçası olarak kod, önceki hello ilk hello toplanmış durumu temizlenir tutulur. Merhaba güvenilir koleksiyonu ile yeni bir durum yeniden olduğundan, tüm önceki bildirimler önemli değildir.
> 
> 

Merhaba **DictionaryChanged** olay işleyicisi kullanan **NotifyDictionaryChangedEventArgs** tooprovide hello Olay Ayrıntıları.
**NotifyDictionaryChangedEventArgs** beş alt sınıfların sahiptir. Merhaba eylem özelliğini **NotifyDictionaryChangedEventArgs** toocast **NotifyDictionaryChangedEventArgs** toohello doğru alt:

* **NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**
* **NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**
* **NotifyDictionaryChangedAction.Add** ve **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**
* **NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**
* **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**

```C#
public void OnDictionaryChangedHandler(object sender, NotifyDictionaryChangedEventArgs<TKey, TValue> e)
{
    switch (e.Action)
    {
        case NotifyDictionaryChangedAction.Clear:
            var clearEvent = e as NotifyDictionaryClearEventArgs<TKey, TValue>;
            this.ProcessClearNotification(clearEvent);
            return;

        case NotifyDictionaryChangedAction.Add:
            var addEvent = e as NotifyDictionaryItemAddedEventArgs<TKey, TValue>;
            this.ProcessAddNotification(addEvent);
            return;

        case NotifyDictionaryChangedAction.Update:
            var updateEvent = e as NotifyDictionaryItemUpdatedEventArgs<TKey, TValue>;
            this.ProcessUpdateNotification(updateEvent);
            return;

        case NotifyDictionaryChangedAction.Remove:
            var deleteEvent = e as NotifyDictionaryItemRemovedEventArgs<TKey, TValue>;
            this.ProcessRemoveNotification(deleteEvent);
            return;

        default:
            break;
    }
}
```

## <a name="recommendations"></a>Öneriler
* *Yapmak* bildirim olayları mümkün olduğunca hızlı tamamlayın.
* *Sağlamadığı* pahalı işlemleri (örneğin, g/ç işlemleri) zaman uyumlu olaylar bir parçası olarak çalıştırmak.
* *Yapmak* hello olay işlemeden önce hello eylem türünü denetleyin. Yeni Eylem türleri hello gelecekteki eklenebilir.

Göz önünde bazı şeyleri tookeep şunlardır:

* Bildirimleri hello yürütme bir işlemin bir parçası olarak tetiklenir. Örneğin, bir geri bildirim hello bir geri yükleme işleminin son adımı tetiklenir. Bir geri yükleme Hello bildirim olayı işlenen kadar tamamlanmaz.
* Bildirimleri işlemleri uygulama hello bir parçası olarak başlatıldığından istemciler yalnızca yerel olarak kaydedilmiş işlemleri için bildirim bakın. Ve işlemleri yalnızca yerel olarak kaydedilmiş toobe garanti (diğer bir deyişle, oturum açmış), olabilir veya hello gelecekteki geri değil.
* Merhaba Yinele yolda uygulanan her işlem için tek bir bildirim tetiklenir. Bu işlem T1 Create(X), Delete(X) ve Create(X) içeriyorsa, bir bildirim X hello oluşturulmasını, bir hello silinmek ve yeniden hello oluşturma için bir sırada elde edersiniz olduğunu anlamına gelir.
* Birden çok işlemleri içeren işlemleri için işlemleri, bunlar hello kullanıcı birincil çoğaltmadan hello alınan hello sırayla uygulanır.
* False ilerleme durumu işlenirken bir parçası olarak, bazı işlemler geri olabilir. Bildirimleri hello çoğaltma geri tooa kararlı noktasının hello durumu alınıyor, bu tür geri alma işlemleri için oluşturulur. Önemli bir fark geri bildirimler, yinelenen anahtarlar olayları toplanır ' dir. Örneğin, T1 işlem geri alınamaz, tek bildirim tooDelete(X) görürsünüz.

## <a name="next-steps"></a>Sonraki adımlar
* [Güvenilir Koleksiyonlar](service-fabric-work-with-reliable-collections.md)
* [Güvenilir hizmetler hızlı başlangıç](service-fabric-reliable-services-quick-start.md)
* [Güvenilir hizmetler yedekleme ve geri yükleme (olağanüstü durum kurtarma)](service-fabric-reliable-services-backup-restore.md)
* [Güvenilir koleksiyonlar için Geliştirici Başvurusu](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

