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
# <a name="reliable-services-notifications"></a><span data-ttu-id="1e958-103">Güvenilir hizmetler bildirimleri</span><span class="sxs-lookup"><span data-stu-id="1e958-103">Reliable Services notifications</span></span>
<span data-ttu-id="1e958-104">Bildirimleri istemcileri ilginizi tooan nesne yapılan tootrack hello değişiklikler sağlar.</span><span class="sxs-lookup"><span data-stu-id="1e958-104">Notifications allow clients tootrack hello changes that are being made tooan object that they're interested in.</span></span> <span data-ttu-id="1e958-105">İki nesne türünün destek bildirimleri: *güvenilir durum Yöneticisi* ve *güvenilir sözlük*.</span><span class="sxs-lookup"><span data-stu-id="1e958-105">Two types of objects support notifications: *Reliable State Manager* and *Reliable Dictionary*.</span></span>

<span data-ttu-id="1e958-106">Bildirimleri kullanmak için yaygın nedenler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1e958-106">Common reasons for using notifications are:</span></span>

* <span data-ttu-id="1e958-107">Yapı ikincil dizinler gibi görünümlerde gerçekleştirilip veya filtrelenmiş görünümleri hello yinelemenin durumunun bir araya getirilir.</span><span class="sxs-lookup"><span data-stu-id="1e958-107">Building materialized views, such as secondary indexes or aggregated filtered views of hello replica's state.</span></span> <span data-ttu-id="1e958-108">Bir örnek, güvenilir sözlükteki tüm anahtarları sıralanmış bir dizindir.</span><span class="sxs-lookup"><span data-stu-id="1e958-108">An example is a sorted index of all keys in Reliable Dictionary.</span></span>
* <span data-ttu-id="1e958-109">Gönderen izleme gibi verileri hello hello son bir saat eklenen kullanıcıların sayısı.</span><span class="sxs-lookup"><span data-stu-id="1e958-109">Sending monitoring data, such as hello number of users added in hello last hour.</span></span>

<span data-ttu-id="1e958-110">Bildirimleri işlemleri uygulama bir parçası olarak tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="1e958-110">Notifications are fired as part of applying operations.</span></span> <span data-ttu-id="1e958-111">Bu yüzden, olası ve zaman uyumlu olaylar pahalı işlemleri eklememelisiniz kadar hızlı bildirimleri yapılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="1e958-111">Because of that, notifications should be handled as fast as possible, and synchronous events shouldn't include any expensive operations.</span></span>

## <a name="reliable-state-manager-notifications"></a><span data-ttu-id="1e958-112">Güvenilir durum Yöneticisi bildirimleri</span><span class="sxs-lookup"><span data-stu-id="1e958-112">Reliable State Manager notifications</span></span>
<span data-ttu-id="1e958-113">Güvenilir durumu Yöneticisi olayları aşağıdaki hello için bildirimleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="1e958-113">Reliable State Manager provides notifications for hello following events:</span></span>

* <span data-ttu-id="1e958-114">İşlem</span><span class="sxs-lookup"><span data-stu-id="1e958-114">Transaction</span></span>
  * <span data-ttu-id="1e958-115">İşleme</span><span class="sxs-lookup"><span data-stu-id="1e958-115">Commit</span></span>
* <span data-ttu-id="1e958-116">Durum Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="1e958-116">State manager</span></span>
  * <span data-ttu-id="1e958-117">Yeniden oluşturma</span><span class="sxs-lookup"><span data-stu-id="1e958-117">Rebuild</span></span>
  * <span data-ttu-id="1e958-118">Güvenilir bir duruma eklenmesi</span><span class="sxs-lookup"><span data-stu-id="1e958-118">Addition of a reliable state</span></span>
  * <span data-ttu-id="1e958-119">Güvenilir durumunun kaldırma</span><span class="sxs-lookup"><span data-stu-id="1e958-119">Removal of a reliable state</span></span>

<span data-ttu-id="1e958-120">Güvenilir durum Yöneticisi hello geçerli inflight işlemleri izler.</span><span class="sxs-lookup"><span data-stu-id="1e958-120">Reliable State Manager tracks hello current inflight transactions.</span></span> <span data-ttu-id="1e958-121">harekete bir bildirim toobe neden olan işlem durumunda Hello yalnızca değişiklik yürütme bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="1e958-121">hello only change in transaction state that causes a notification toobe fired is a transaction being committed.</span></span>

<span data-ttu-id="1e958-122">Güvenilir durum Yöneticisi güvenilir sözlük ve güvenilir sırası gibi güvenilir durumları koleksiyonu tutar.</span><span class="sxs-lookup"><span data-stu-id="1e958-122">Reliable State Manager maintains a collection of reliable states like Reliable Dictionary and Reliable Queue.</span></span> <span data-ttu-id="1e958-123">Güvenilir durum Yöneticisi bu koleksiyon değiştiğinde bildirim ateşlenir: güvenilir durumu eklendiğinde veya kaldırıldığında ya da hello tüm koleksiyon yeniden.</span><span class="sxs-lookup"><span data-stu-id="1e958-123">Reliable State Manager fires notifications when this collection changes: a reliable state is added or removed, or hello entire collection is rebuilt.</span></span>
<span data-ttu-id="1e958-124">Merhaba güvenilir durum Yöneticisi koleksiyonu üç durumda yeniden oluşturulur:</span><span class="sxs-lookup"><span data-stu-id="1e958-124">hello Reliable State Manager collection is rebuilt in three cases:</span></span>

* <span data-ttu-id="1e958-125">Kurtarma: bir çoğaltma başladığında, önceki durumuna hello diskten kurtarır.</span><span class="sxs-lookup"><span data-stu-id="1e958-125">Recovery: When a replica starts, it recovers its previous state from hello disk.</span></span> <span data-ttu-id="1e958-126">Kurtarma Hello sonunda kullandığı **NotifyStateManagerChangedEventArgs** toofire kurtarılan güvenilir durumları hello kümesini içeren bir olay.</span><span class="sxs-lookup"><span data-stu-id="1e958-126">At hello end of recovery, it uses **NotifyStateManagerChangedEventArgs** toofire an event that contains hello set of recovered reliable states.</span></span>
* <span data-ttu-id="1e958-127">Tam kopyalama: bir çoğaltma hello yapılandırma kümesi katılabilmesi için önce yerleşik toobe sahiptir.</span><span class="sxs-lookup"><span data-stu-id="1e958-127">Full copy: Before a replica can join hello configuration set, it has toobe built.</span></span> <span data-ttu-id="1e958-128">Bazı durumlarda, bu hello birincil çoğaltma toobe uygulanan toohello boşta ikincil çoğaltma güvenilir durum yöneticisinin durumundan tam bir kopyasını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="1e958-128">Sometimes, this requires a full copy of Reliable State Manager's state from hello primary replica toobe applied toohello idle secondary replica.</span></span> <span data-ttu-id="1e958-129">Merhaba ikincil çoğaltma kullanan güvenilir durumu Yöneticisi **NotifyStateManagerChangedEventArgs** toofire hello birincil çoğaltmadan edinilen güvenilir durumları hello kümesini içeren bir olay.</span><span class="sxs-lookup"><span data-stu-id="1e958-129">Reliable State Manager on hello secondary replica uses **NotifyStateManagerChangedEventArgs** toofire an event that contains hello set of reliable states that it acquired from hello primary replica.</span></span>
* <span data-ttu-id="1e958-130">Geri yükleme: olağanüstü durum kurtarma senaryolarında hello yinelemenin durumu bir yedekten geri yüklenebilir **RestoreAsync**.</span><span class="sxs-lookup"><span data-stu-id="1e958-130">Restore: In disaster recovery scenarios, hello replica's state can be restored from a backup via **RestoreAsync**.</span></span> <span data-ttu-id="1e958-131">Böyle durumlarda, güvenilir durum Yöneticisi hello birincil çoğaltmadaki kullanan **NotifyStateManagerChangedEventArgs** toofire hello yedekten geri güvenilir durumları hello kümesini içeren bir olay.</span><span class="sxs-lookup"><span data-stu-id="1e958-131">In such cases, Reliable State Manager on hello primary replica uses **NotifyStateManagerChangedEventArgs** toofire an event that contains hello set of reliable states that it restored from hello backup.</span></span>

<span data-ttu-id="1e958-132">tooregister işlem bildirimleri ve/veya durum Yöneticisi bildirimleri için gereksinim duyduğunuz hello ile tooregister **TransactionChanged** veya **StateManagerChanged** güvenilir durumu Yöneticisi olayları.</span><span class="sxs-lookup"><span data-stu-id="1e958-132">tooregister for transaction notifications and/or state manager notifications, you need tooregister with hello **TransactionChanged** or **StateManagerChanged** events on Reliable State Manager.</span></span> <span data-ttu-id="1e958-133">Ortak bir yerde tooregister bu olay işleyicileri ile olan durum bilgisi olan hizmetinizin hello Oluşturucusu.</span><span class="sxs-lookup"><span data-stu-id="1e958-133">A common place tooregister with these event handlers is hello constructor of your stateful service.</span></span> <span data-ttu-id="1e958-134">Merhaba Oluşturucu kaydederken hello ömrü sırasında bir değişiklik nedeniyle herhangi bir bildirim kaçırılması olmaz **IReliableStateManager**.</span><span class="sxs-lookup"><span data-stu-id="1e958-134">When you register on hello constructor, you won't miss any notification that's caused by a change during hello lifetime of **IReliableStateManager**.</span></span>

```C#
public MyService(StatefulServiceContext context)
    : base(MyService.EndpointName, context, CreateReliableStateManager(context))
{
    this.StateManager.TransactionChanged += this.OnTransactionChangedHandler;
    this.StateManager.StateManagerChanged += this.OnStateManagerChangedHandler;
}
```

<span data-ttu-id="1e958-135">Merhaba **TransactionChanged** olay işleyicisi kullanan **NotifyTransactionChangedEventArgs** tooprovide hello Olay Ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="1e958-135">hello **TransactionChanged** event handler uses **NotifyTransactionChangedEventArgs** tooprovide details about hello event.</span></span> <span data-ttu-id="1e958-136">Merhaba eylem özelliği içerir (örneğin, **NotifyTransactionChangedAction.Commit**) değişikliğin hello türünü belirtir.</span><span class="sxs-lookup"><span data-stu-id="1e958-136">It contains hello action property (for example, **NotifyTransactionChangedAction.Commit**) that specifies hello type of change.</span></span> <span data-ttu-id="1e958-137">Ayrıca, değiştirilmiş bir başvuru toohello işlem sağlar hello TRANSACTION özelliği içerir.</span><span class="sxs-lookup"><span data-stu-id="1e958-137">It also contains hello transaction property that provides a reference toohello transaction that changed.</span></span>

> [!NOTE]
> <span data-ttu-id="1e958-138">Bugün, **TransactionChanged** yalnızca hello hareket tamamlanırsa olayları ortaya çıkar.</span><span class="sxs-lookup"><span data-stu-id="1e958-138">Today, **TransactionChanged** events are raised only if hello transaction is committed.</span></span> <span data-ttu-id="1e958-139">Merhaba eylem sonra çok eşittir**NotifyTransactionChangedAction.Commit**.</span><span class="sxs-lookup"><span data-stu-id="1e958-139">hello action is then equal too**NotifyTransactionChangedAction.Commit**.</span></span> <span data-ttu-id="1e958-140">Ancak işlem durumu değişiklikleri diğer türleri için olayları hello gelecekteki, yükseltilmiş.</span><span class="sxs-lookup"><span data-stu-id="1e958-140">But in hello future, events might be raised for other types of transaction state changes.</span></span> <span data-ttu-id="1e958-141">Merhaba eylem denetleme ve yalnızca bu beklediğiniz ise hello olayı işleme öneririz.</span><span class="sxs-lookup"><span data-stu-id="1e958-141">We recommend checking hello action and processing hello event only if it's one that you expect.</span></span>
> 
> 

<span data-ttu-id="1e958-142">Aşağıda bir örnek verilmiştir **TransactionChanged** olay işleyicisi.</span><span class="sxs-lookup"><span data-stu-id="1e958-142">Following is an example **TransactionChanged** event handler.</span></span>

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

<span data-ttu-id="1e958-143">Merhaba **StateManagerChanged** olay işleyicisi kullanan **NotifyStateManagerChangedEventArgs** tooprovide hello Olay Ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="1e958-143">hello **StateManagerChanged** event handler uses **NotifyStateManagerChangedEventArgs** tooprovide details about hello event.</span></span>
<span data-ttu-id="1e958-144">**NotifyStateManagerChangedEventArgs** iki alt sınıfları olmayan: **NotifyStateManagerRebuildEventArgs** ve **NotifyStateManagerSingleEntityChangedEventArgs**.</span><span class="sxs-lookup"><span data-stu-id="1e958-144">**NotifyStateManagerChangedEventArgs** has two subclasses: **NotifyStateManagerRebuildEventArgs** and **NotifyStateManagerSingleEntityChangedEventArgs**.</span></span>
<span data-ttu-id="1e958-145">Merhaba eylem özelliğinde kullanmak **NotifyStateManagerChangedEventArgs** toocast **NotifyStateManagerChangedEventArgs** toohello doğru alt:</span><span class="sxs-lookup"><span data-stu-id="1e958-145">You use hello action property in **NotifyStateManagerChangedEventArgs** toocast **NotifyStateManagerChangedEventArgs** toohello correct subclass:</span></span>

* <span data-ttu-id="1e958-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="1e958-146">**NotifyStateManagerChangedAction.Rebuild**: **NotifyStateManagerRebuildEventArgs**</span></span>
* <span data-ttu-id="1e958-147">**NotifyStateManagerChangedAction.Add** ve **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="1e958-147">**NotifyStateManagerChangedAction.Add** and **NotifyStateManagerChangedAction.Remove**: **NotifyStateManagerSingleEntityChangedEventArgs**</span></span>

<span data-ttu-id="1e958-148">Aşağıda bir örnek verilmiştir **StateManagerChanged** bildirim işleyici.</span><span class="sxs-lookup"><span data-stu-id="1e958-148">Following is an example **StateManagerChanged** notification handler.</span></span>

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

## <a name="reliable-dictionary-notifications"></a><span data-ttu-id="1e958-149">Güvenilir sözlük bildirimleri</span><span class="sxs-lookup"><span data-stu-id="1e958-149">Reliable Dictionary notifications</span></span>
<span data-ttu-id="1e958-150">Güvenilir sözlük olayları aşağıdaki hello için bildirimleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="1e958-150">Reliable Dictionary provides notifications for hello following events:</span></span>

* <span data-ttu-id="1e958-151">Yeniden oluşturma: çağrılır **ReliableDictionary** durumuna kurtarılan ya da kopyalanmış yerel durumu ya da yedekleme kurtarıldı.</span><span class="sxs-lookup"><span data-stu-id="1e958-151">Rebuild: Called when **ReliableDictionary** has recovered its state from a recovered or copied local state or backup.</span></span>
* <span data-ttu-id="1e958-152">Clear: çağrılır hello durumunu **ReliableDictionary** hello temizlenmiş **ClearAsync** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="1e958-152">Clear: Called when hello state of **ReliableDictionary** has been cleared through hello **ClearAsync** method.</span></span>
* <span data-ttu-id="1e958-153">Ekleyin: adlı bir öğe çok eklendiğinde**ReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="1e958-153">Add: Called when an item has been added too**ReliableDictionary**.</span></span>
* <span data-ttu-id="1e958-154">Güncelleştirme: bir öğe olarak adlandırılan **IReliableDictionary** güncelleştirildi.</span><span class="sxs-lookup"><span data-stu-id="1e958-154">Update: Called when an item in **IReliableDictionary** has been updated.</span></span>
* <span data-ttu-id="1e958-155">Kaldır: bir öğe adlı **IReliableDictionary** silinmiş olabilir.</span><span class="sxs-lookup"><span data-stu-id="1e958-155">Remove: Called when an item in **IReliableDictionary** has been deleted.</span></span>

<span data-ttu-id="1e958-156">tooget güvenilir sözlük bildirimleri, gereksinim duyduğunuz hello ile tooregister **DictionaryChanged** olay işleyicisini **IReliableDictionary**.</span><span class="sxs-lookup"><span data-stu-id="1e958-156">tooget Reliable Dictionary notifications, you need tooregister with hello **DictionaryChanged** event handler on **IReliableDictionary**.</span></span> <span data-ttu-id="1e958-157">Ortak bir yerde tooregister bu olay işleyicileri ile olan hello **ReliableStateManager.StateManagerChanged** bildirim ekleyin.</span><span class="sxs-lookup"><span data-stu-id="1e958-157">A common place tooregister with these event handlers is in hello **ReliableStateManager.StateManagerChanged** add notification.</span></span>
<span data-ttu-id="1e958-158">Ne zaman kaydetme **IReliableDictionary** çok eklenen**IReliableStateManager** herhangi bir bildirim kaçırılması olmaz sağlar.</span><span class="sxs-lookup"><span data-stu-id="1e958-158">Registering when **IReliableDictionary** is added too**IReliableStateManager** ensures that you won't miss any notifications.</span></span>

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
> <span data-ttu-id="1e958-159">**ProcessStateManagerSingleEntityNotification** hello örnek yöntemidir önceki bu hello **OnStateManagerChangedHandler** örnek çağrıları.</span><span class="sxs-lookup"><span data-stu-id="1e958-159">**ProcessStateManagerSingleEntityNotification** is hello sample method that hello preceding **OnStateManagerChangedHandler** example calls.</span></span>
> 
> 

<span data-ttu-id="1e958-160">Merhaba önceki kod ayarlar hello **IReliableNotificationAsyncCallback** , bunların ile arabirim **DictionaryChanged**.</span><span class="sxs-lookup"><span data-stu-id="1e958-160">hello preceding code sets hello **IReliableNotificationAsyncCallback** interface, along with **DictionaryChanged**.</span></span> <span data-ttu-id="1e958-161">Çünkü **NotifyDictionaryRebuildEventArgs** içeren bir **IAsyncEnumerable** arabirimi--, zaman uyumsuz olarak--numaralandırılan toobe gereken yeniden bildirimleri aracılığıyla harekete  **RebuildNotificationAsyncCallback** yerine **OnDictionaryChangedHandler**.</span><span class="sxs-lookup"><span data-stu-id="1e958-161">Because **NotifyDictionaryRebuildEventArgs** contains an **IAsyncEnumerable** interface--which needs toobe enumerated asynchronously--rebuild notifications are fired through **RebuildNotificationAsyncCallback** instead of **OnDictionaryChangedHandler**.</span></span>

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
> <span data-ttu-id="1e958-162">İşleme hello yeniden bildirimi, bir parçası olarak kod, önceki hello ilk hello toplanmış durumu temizlenir tutulur.</span><span class="sxs-lookup"><span data-stu-id="1e958-162">In hello preceding code, as part of processing hello rebuild notification, first hello maintained aggregated state is cleared.</span></span> <span data-ttu-id="1e958-163">Merhaba güvenilir koleksiyonu ile yeni bir durum yeniden olduğundan, tüm önceki bildirimler önemli değildir.</span><span class="sxs-lookup"><span data-stu-id="1e958-163">Because hello reliable collection is being rebuilt with a new state, all previous notifications are irrelevant.</span></span>
> 
> 

<span data-ttu-id="1e958-164">Merhaba **DictionaryChanged** olay işleyicisi kullanan **NotifyDictionaryChangedEventArgs** tooprovide hello Olay Ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="1e958-164">hello **DictionaryChanged** event handler uses **NotifyDictionaryChangedEventArgs** tooprovide details about hello event.</span></span>
<span data-ttu-id="1e958-165">**NotifyDictionaryChangedEventArgs** beş alt sınıfların sahiptir.</span><span class="sxs-lookup"><span data-stu-id="1e958-165">**NotifyDictionaryChangedEventArgs** has five subclasses.</span></span> <span data-ttu-id="1e958-166">Merhaba eylem özelliğini **NotifyDictionaryChangedEventArgs** toocast **NotifyDictionaryChangedEventArgs** toohello doğru alt:</span><span class="sxs-lookup"><span data-stu-id="1e958-166">Use hello action property in **NotifyDictionaryChangedEventArgs** toocast **NotifyDictionaryChangedEventArgs** toohello correct subclass:</span></span>

* <span data-ttu-id="1e958-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span><span class="sxs-lookup"><span data-stu-id="1e958-167">**NotifyDictionaryChangedAction.Rebuild**: **NotifyDictionaryRebuildEventArgs**</span></span>
* <span data-ttu-id="1e958-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span><span class="sxs-lookup"><span data-stu-id="1e958-168">**NotifyDictionaryChangedAction.Clear**: **NotifyDictionaryClearEventArgs**</span></span>
* <span data-ttu-id="1e958-169">**NotifyDictionaryChangedAction.Add** ve **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="1e958-169">**NotifyDictionaryChangedAction.Add** and **NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemAddedEventArgs**</span></span>
* <span data-ttu-id="1e958-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="1e958-170">**NotifyDictionaryChangedAction.Update**: **NotifyDictionaryItemUpdatedEventArgs**</span></span>
* <span data-ttu-id="1e958-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span><span class="sxs-lookup"><span data-stu-id="1e958-171">**NotifyDictionaryChangedAction.Remove**: **NotifyDictionaryItemRemovedEventArgs**</span></span>

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

## <a name="recommendations"></a><span data-ttu-id="1e958-172">Öneriler</span><span class="sxs-lookup"><span data-stu-id="1e958-172">Recommendations</span></span>
* <span data-ttu-id="1e958-173">*Yapmak* bildirim olayları mümkün olduğunca hızlı tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="1e958-173">*Do* complete notification events as fast as possible.</span></span>
* <span data-ttu-id="1e958-174">*Sağlamadığı* pahalı işlemleri (örneğin, g/ç işlemleri) zaman uyumlu olaylar bir parçası olarak çalıştırmak.</span><span class="sxs-lookup"><span data-stu-id="1e958-174">*Do not* execute any expensive operations (for example, I/O operations) as part of synchronous events.</span></span>
* <span data-ttu-id="1e958-175">*Yapmak* hello olay işlemeden önce hello eylem türünü denetleyin.</span><span class="sxs-lookup"><span data-stu-id="1e958-175">*Do* check hello action type before you process hello event.</span></span> <span data-ttu-id="1e958-176">Yeni Eylem türleri hello gelecekteki eklenebilir.</span><span class="sxs-lookup"><span data-stu-id="1e958-176">New action types might be added in hello future.</span></span>

<span data-ttu-id="1e958-177">Göz önünde bazı şeyleri tookeep şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1e958-177">Here are some things tookeep in mind:</span></span>

* <span data-ttu-id="1e958-178">Bildirimleri hello yürütme bir işlemin bir parçası olarak tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="1e958-178">Notifications are fired as part of hello execution of an operation.</span></span> <span data-ttu-id="1e958-179">Örneğin, bir geri bildirim hello bir geri yükleme işleminin son adımı tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="1e958-179">For example, a restore notification is fired as hello last step of a restore operation.</span></span> <span data-ttu-id="1e958-180">Bir geri yükleme Hello bildirim olayı işlenen kadar tamamlanmaz.</span><span class="sxs-lookup"><span data-stu-id="1e958-180">A restore will not finish until hello notification event is processed.</span></span>
* <span data-ttu-id="1e958-181">Bildirimleri işlemleri uygulama hello bir parçası olarak başlatıldığından istemciler yalnızca yerel olarak kaydedilmiş işlemleri için bildirim bakın.</span><span class="sxs-lookup"><span data-stu-id="1e958-181">Because notifications are fired as part of hello applying operations, clients see only notifications for locally committed operations.</span></span> <span data-ttu-id="1e958-182">Ve işlemleri yalnızca yerel olarak kaydedilmiş toobe garanti (diğer bir deyişle, oturum açmış), olabilir veya hello gelecekteki geri değil.</span><span class="sxs-lookup"><span data-stu-id="1e958-182">And because operations are guaranteed only toobe locally committed (in other words, logged), they might or might not be undone in hello future.</span></span>
* <span data-ttu-id="1e958-183">Merhaba Yinele yolda uygulanan her işlem için tek bir bildirim tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="1e958-183">On hello redo path, a single notification is fired for each applied operation.</span></span> <span data-ttu-id="1e958-184">Bu işlem T1 Create(X), Delete(X) ve Create(X) içeriyorsa, bir bildirim X hello oluşturulmasını, bir hello silinmek ve yeniden hello oluşturma için bir sırada elde edersiniz olduğunu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="1e958-184">This means that if transaction T1 includes Create(X), Delete(X), and Create(X), you'll get one notification for hello creation of X, one for hello deletion, and one for hello creation again, in that order.</span></span>
* <span data-ttu-id="1e958-185">Birden çok işlemleri içeren işlemleri için işlemleri, bunlar hello kullanıcı birincil çoğaltmadan hello alınan hello sırayla uygulanır.</span><span class="sxs-lookup"><span data-stu-id="1e958-185">For transactions that contain multiple operations, operations are applied in hello order in which they were received on hello primary replica from hello user.</span></span>
* <span data-ttu-id="1e958-186">False ilerleme durumu işlenirken bir parçası olarak, bazı işlemler geri olabilir.</span><span class="sxs-lookup"><span data-stu-id="1e958-186">As part of processing false progress, some operations might be undone.</span></span> <span data-ttu-id="1e958-187">Bildirimleri hello çoğaltma geri tooa kararlı noktasının hello durumu alınıyor, bu tür geri alma işlemleri için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1e958-187">Notifications are raised for such undo operations, rolling hello state of hello replica back tooa stable point.</span></span> <span data-ttu-id="1e958-188">Önemli bir fark geri bildirimler, yinelenen anahtarlar olayları toplanır ' dir.</span><span class="sxs-lookup"><span data-stu-id="1e958-188">One important difference of undo notifications is that events that have duplicate keys are aggregated.</span></span> <span data-ttu-id="1e958-189">Örneğin, T1 işlem geri alınamaz, tek bildirim tooDelete(X) görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="1e958-189">For example, if transaction T1 is being undone, you'll see a single notification tooDelete(X).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1e958-190">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1e958-190">Next steps</span></span>
* [<span data-ttu-id="1e958-191">Güvenilir Koleksiyonlar</span><span class="sxs-lookup"><span data-stu-id="1e958-191">Reliable Collections</span></span>](service-fabric-work-with-reliable-collections.md)
* [<span data-ttu-id="1e958-192">Güvenilir hizmetler hızlı başlangıç</span><span class="sxs-lookup"><span data-stu-id="1e958-192">Reliable Services quick start</span></span>](service-fabric-reliable-services-quick-start.md)
* [<span data-ttu-id="1e958-193">Güvenilir hizmetler yedekleme ve geri yükleme (olağanüstü durum kurtarma)</span><span class="sxs-lookup"><span data-stu-id="1e958-193">Reliable Services backup and restore (disaster recovery)</span></span>](service-fabric-reliable-services-backup-restore.md)
* [<span data-ttu-id="1e958-194">Güvenilir koleksiyonlar için Geliştirici Başvurusu</span><span class="sxs-lookup"><span data-stu-id="1e958-194">Developer reference for Reliable Collections</span></span>](https://msdn.microsoft.com/library/azure/microsoft.servicefabric.data.collections.aspx)

