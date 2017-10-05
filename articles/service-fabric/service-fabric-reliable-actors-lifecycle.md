---
title: "Aktör tabanlı Azure mikro yaşam döngüsüne genel bakış | Microsoft Docs"
description: "Service Fabric güvenilir aktör yaşam döngüsü, atık toplama ve aktörler ve durumlarına el ile silinmesi açıklanmaktadır"
services: service-fabric
documentationcenter: .net
author: amanbha
manager: timlt
editor: vturecek
ms.assetid: b91384cc-804c-49d6-a6cb-f3f3d7d65a8e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: amanbha
ms.openlocfilehash: 75b7b77a0bef2051599a4f61183109cfb2ffff3b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="actor-lifecycle-automatic-garbage-collection-and-manual-delete"></a><span data-ttu-id="1aab2-103">Aktör yaşam döngüsü, otomatik çöp toplama ve el ile silme</span><span class="sxs-lookup"><span data-stu-id="1aab2-103">Actor lifecycle, automatic garbage collection, and manual delete</span></span>
<span data-ttu-id="1aab2-104">Bir oyuncu yöntemlerinden herhangi biri için bir çağrı yapılır ilk kez etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="1aab2-104">An actor is activated the first time a call is made to any of its methods.</span></span> <span data-ttu-id="1aab2-105">Bir oyuncu devre dışı bırakılmış (Çöp aktörler çalışma zamanı tarafından toplanan) ise yapılandırılabilir bir süre için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="1aab2-105">An actor is deactivated (garbage collected by the Actors runtime) if it is not used for a configurable period of time.</span></span> <span data-ttu-id="1aab2-106">Bir aktör ve durumu da el ile herhangi bir zamanda silinebilir.</span><span class="sxs-lookup"><span data-stu-id="1aab2-106">An actor and its state can also be deleted manually at any time.</span></span>

## <a name="actor-activation"></a><span data-ttu-id="1aab2-107">Aktör etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="1aab2-107">Actor activation</span></span>
<span data-ttu-id="1aab2-108">Bir oyuncu etkinleştirildiğinde, aşağıdakiler gerçekleşir:</span><span class="sxs-lookup"><span data-stu-id="1aab2-108">When an actor is activated, the following occurs:</span></span>

* <span data-ttu-id="1aab2-109">Bir oyuncu için bir çağrı gelir ve bir etkin değilse, yeni aktör oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="1aab2-109">When a call comes for an actor and one is not already active, a new actor is created.</span></span>
* <span data-ttu-id="1aab2-110">Durum koruma aktör'in durumu yüklenir.</span><span class="sxs-lookup"><span data-stu-id="1aab2-110">The actor's state is loaded if it's maintaining state.</span></span>
* <span data-ttu-id="1aab2-111">`OnActivateAsync` (C#) veya `onActivateAsync` (hangi aktör uygulamasında kılınabilir) (Java) yöntemi çağrılır.</span><span class="sxs-lookup"><span data-stu-id="1aab2-111">The `OnActivateAsync` (C#) or `onActivateAsync` (Java) method (which can be overridden in the actor implementation) is called.</span></span>
* <span data-ttu-id="1aab2-112">Aktör şimdi etkin olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="1aab2-112">The actor is now considered active.</span></span>

## <a name="actor-deactivation"></a><span data-ttu-id="1aab2-113">Aktör devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="1aab2-113">Actor deactivation</span></span>
<span data-ttu-id="1aab2-114">Bir oyuncu devre dışı bırakıldığında, aşağıdakiler gerçekleşir:</span><span class="sxs-lookup"><span data-stu-id="1aab2-114">When an actor is deactivated, the following occurs:</span></span>

* <span data-ttu-id="1aab2-115">Belirli bir süre için bir aktör kullanılmadığı zaman etkin aktörler tablosundan kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="1aab2-115">When an actor is not used for some period of time, it is removed from the Active Actors table.</span></span>
* <span data-ttu-id="1aab2-116">`OnDeactivateAsync` (C#) veya `onDeactivateAsync` (hangi aktör uygulamasında kılınabilir) (Java) yöntemi çağrılır.</span><span class="sxs-lookup"><span data-stu-id="1aab2-116">The `OnDeactivateAsync` (C#) or `onDeactivateAsync` (Java) method (which can be overridden in the actor implementation) is called.</span></span> <span data-ttu-id="1aab2-117">Aktör için tüm zamanlayıcılar temizler.</span><span class="sxs-lookup"><span data-stu-id="1aab2-117">This clears all the timers for the actor.</span></span> <span data-ttu-id="1aab2-118">Aktör işlemleri değişiklikler bu yönteminden çağrılmamalıdır durumu ister.</span><span class="sxs-lookup"><span data-stu-id="1aab2-118">Actor operations like state changes should not be called from this method.</span></span>

> [!TIP]
> <span data-ttu-id="1aab2-119">Fabric aktör çalışma zamanı bazı yayar [olayları ilgili aktör etkinleştirme ve devre dışı bırakma](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters).</span><span class="sxs-lookup"><span data-stu-id="1aab2-119">The Fabric Actors runtime emits some [events related to actor activation and deactivation](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters).</span></span> <span data-ttu-id="1aab2-120">Bunlar, tanılama ve performans izlemesi kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="1aab2-120">They are useful in diagnostics and performance monitoring.</span></span>
>
>

### <a name="actor-garbage-collection"></a><span data-ttu-id="1aab2-121">Aktör çöp toplama</span><span class="sxs-lookup"><span data-stu-id="1aab2-121">Actor garbage collection</span></span>
<span data-ttu-id="1aab2-122">Bir oyuncu devre dışı bırakıldığında aktör nesne başvuruları yayımlanan ve normalde ortak dil çalışma zamanı (CLR) veya java sanal makinesi (JVM) atık toplayıcı tarafından toplanacak olabilir.</span><span class="sxs-lookup"><span data-stu-id="1aab2-122">When an actor is deactivated, references to the actor object are released and it can be garbage collected normally by the common language runtime (CLR) or java virtual machine (JVM) garbage collector.</span></span> <span data-ttu-id="1aab2-123">Çöp toplama yalnızca aktör nesnesini temizler; Mevcut **değil** aktör ait durum Yöneticisi'nde depolanan durumunu kaldırın.</span><span class="sxs-lookup"><span data-stu-id="1aab2-123">Garbage collection only cleans up the actor object; it does **not** remove state stored in the actor's State Manager.</span></span> <span data-ttu-id="1aab2-124">Aktör etkinleştirilir, sonraki açışınızda yeni bir aktör nesnesi oluşturulur ve durumu geri.</span><span class="sxs-lookup"><span data-stu-id="1aab2-124">The next time the actor is activated, a new actor object is created and its state is restored.</span></span>

<span data-ttu-id="1aab2-125">Ne "devre dışı bırakma ve atık toplama amacıyla kullanılan olarak" sayar?</span><span class="sxs-lookup"><span data-stu-id="1aab2-125">What counts as “being used” for the purpose of deactivation and garbage collection?</span></span>

* <span data-ttu-id="1aab2-126">Çağrı Alma</span><span class="sxs-lookup"><span data-stu-id="1aab2-126">Receiving a call</span></span>
* <span data-ttu-id="1aab2-127">`IRemindable.ReceiveReminderAsync`(yalnızca aktör anımsatıcıları kullanıyorsa geçerlidir) çağrılan yöntemi</span><span class="sxs-lookup"><span data-stu-id="1aab2-127">`IRemindable.ReceiveReminderAsync` method being invoked (applicable only if the actor uses reminders)</span></span>

> [!NOTE]
> <span data-ttu-id="1aab2-128">Aktör zamanlayıcılar kullanıyorsa ve Zamanlayıcı geri çağırma çağrılır, mevcut **değil** "kullanılan" olarak sayısı.</span><span class="sxs-lookup"><span data-stu-id="1aab2-128">if the actor uses timers and its timer callback is invoked, it does **not** count as "being used".</span></span>
>
>

<span data-ttu-id="1aab2-129">Biz devre dışı bırakma ayrıntıları geçmeden önce aşağıdaki koşulları tanımlamak önemlidir:</span><span class="sxs-lookup"><span data-stu-id="1aab2-129">Before we go into the details of deactivation, it is important to define the following terms:</span></span>

* <span data-ttu-id="1aab2-130">*Tarama aralığı*.</span><span class="sxs-lookup"><span data-stu-id="1aab2-130">*Scan interval*.</span></span> <span data-ttu-id="1aab2-131">Withintext aktörler çalışma zamanı, etkin aktörler tablosunu devre dışı bırakılabilir aktörler için tarar ve atık toplanan aralığını budur.</span><span class="sxs-lookup"><span data-stu-id="1aab2-131">This is the interval at which the Actors runtime scans its Active Actors table for actors that can be deactivated and garbage collected.</span></span> <span data-ttu-id="1aab2-132">Bu varsayılan değeri 1 dakikadır.</span><span class="sxs-lookup"><span data-stu-id="1aab2-132">The default value for this is 1 minute.</span></span>
* <span data-ttu-id="1aab2-133">*Boşta kalma zaman aşımı*.</span><span class="sxs-lookup"><span data-stu-id="1aab2-133">*Idle timeout*.</span></span> <span data-ttu-id="1aab2-134">Bu bir aktör kullanılmayan kalması gereken süreyi belirtir (boş) devre dışı bırakılabilir ve atık toplanan önce.</span><span class="sxs-lookup"><span data-stu-id="1aab2-134">This is the amount of time that an actor needs to remain unused (idle) before it can be deactivated and garbage collected.</span></span> <span data-ttu-id="1aab2-135">Bunun için varsayılan değer 60 dakikadır.</span><span class="sxs-lookup"><span data-stu-id="1aab2-135">The default value for this is 60 minutes.</span></span>

<span data-ttu-id="1aab2-136">Genellikle, bu varsayılan değişiklik gerekmez.</span><span class="sxs-lookup"><span data-stu-id="1aab2-136">Typically, you do not need to change these defaults.</span></span> <span data-ttu-id="1aab2-137">Ancak, gerekirse, bu aralıklar üzerinden değiştirilebilir `ActorServiceSettings` kaydederken, [aktör hizmeti](service-fabric-reliable-actors-platform.md):</span><span class="sxs-lookup"><span data-stu-id="1aab2-137">However, if necessary, these intervals can be changed through `ActorServiceSettings` when registering your [Actor Service](service-fabric-reliable-actors-platform.md):</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        ActorRuntime.RegisterActorAsync<MyActor>((context, actorType) =>
                new ActorService(context, actorType,
                    settings:
                        new ActorServiceSettings()
                        {
                            ActorGarbageCollectionSettings =
                                new ActorGarbageCollectionSettings(10, 2)
                        }))
            .GetAwaiter()
            .GetResult();
    }
}
```

```Java
public class Program
{
    public static void main(String[] args)
    {
        ActorRuntime.registerActorAsync(
                MyActor.class,
                (context, actorTypeInfo) -> new FabricActorService(context, actorTypeInfo),
                timeout);
    }
}
```
<span data-ttu-id="1aab2-138">Her etkin aktör aktör çalışma zamanı, (yani kullanılır) boşta olduğu süre miktarını izler.</span><span class="sxs-lookup"><span data-stu-id="1aab2-138">For each active actor, the actor runtime keeps track of the amount of time that it has been idle (i.e. not used).</span></span> <span data-ttu-id="1aab2-139">Aktör çalışma zamanı her aktörler denetler her `ScanIntervalInSeconds` , çöp toplanır ve boşta olması durumunda topladığı olup olmadığını görmek için `IdleTimeoutInSeconds`.</span><span class="sxs-lookup"><span data-stu-id="1aab2-139">The actor runtime checks each of the actors every `ScanIntervalInSeconds` to see if it can be garbage collected and collects it if it has been idle for `IdleTimeoutInSeconds`.</span></span>

<span data-ttu-id="1aab2-140">Bir oyuncu kullanılan zaman boşta kalma süresini 0 olarak sıfırlanır.</span><span class="sxs-lookup"><span data-stu-id="1aab2-140">Anytime an actor is used, its idle time is reset to 0.</span></span> <span data-ttu-id="1aab2-141">Bundan sonra yalnızca onu yeniden boşta kalırsa toplanacak aktör olabilir `IdleTimeoutInSeconds`.</span><span class="sxs-lookup"><span data-stu-id="1aab2-141">After this, the actor can be garbage collected only if it again remains idle for `IdleTimeoutInSeconds`.</span></span> <span data-ttu-id="1aab2-142">Bir oyuncu aktör arabirim yöntemi veya aktör anımsatıcı geri çağırma yürütülürse kullanılan değerlendirilir çağırma.</span><span class="sxs-lookup"><span data-stu-id="1aab2-142">Recall that an actor is considered to have been used if either an actor interface method or an actor reminder callback is executed.</span></span> <span data-ttu-id="1aab2-143">Bir oyuncu olan **değil** Zamanlayıcı geri çağırma çalıştırıldığında kullanılan düşünülür.</span><span class="sxs-lookup"><span data-stu-id="1aab2-143">An actor is **not** considered to have been used if its timer callback is executed.</span></span>

<span data-ttu-id="1aab2-144">Aşağıdaki diyagramda bu kavramları göstermek için tek bir aktör yaşam döngüsü gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="1aab2-144">The following diagram shows the lifecycle of a single actor to illustrate these concepts.</span></span>

![Boşta kalma süresi örneği][1]

<span data-ttu-id="1aab2-146">Örnek bu aktör lifetime öğesine aktör yöntem çağrıları, anımsatıcı ve zamanlayıcılar etkisini gösterir.</span><span class="sxs-lookup"><span data-stu-id="1aab2-146">The example shows the impact of actor method calls, reminders, and timers on the lifetime of this actor.</span></span> <span data-ttu-id="1aab2-147">Aşağıdaki noktaları örnek hakkında tümleştirilmediği şunlardır:</span><span class="sxs-lookup"><span data-stu-id="1aab2-147">The following points about the example are worth mentioning:</span></span>

* <span data-ttu-id="1aab2-148">ScanInterval ve IdleTimeout 5 ve 10 sırasıyla ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="1aab2-148">ScanInterval and IdleTimeout are set to 5 and 10 respectively.</span></span> <span data-ttu-id="1aab2-149">(Yalnızca kavramı göstermek için bu konudaki Hedefimiz olduğundan birimleri burada önemli değildir.)</span><span class="sxs-lookup"><span data-stu-id="1aab2-149">(Units do not matter here, since our purpose is only to illustrate the concept.)</span></span>
* <span data-ttu-id="1aab2-150">Toplanacak aktörler için tarama T = 0, 5, 10, 15, 20, 25 5 tarama aralığı tarafından tanımlandığı şekilde gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="1aab2-150">The scan for actors to be garbage collected happens at T=0,5,10,15,20,25, as defined by the scan interval of 5.</span></span>
* <span data-ttu-id="1aab2-151">T = konumundaki 4, 8, 12, 16, 20, 24, düzenli bir süreölçeri başlatılır ve kendi geri çağırmayı yürütür.</span><span class="sxs-lookup"><span data-stu-id="1aab2-151">A periodic timer fires at T=4,8,12,16,20,24, and its callback executes.</span></span> <span data-ttu-id="1aab2-152">Aktör boşta kalma süresi etkilemez.</span><span class="sxs-lookup"><span data-stu-id="1aab2-152">It does not impact the idle time of the actor.</span></span>
* <span data-ttu-id="1aab2-153">Aktör yöntem çağrısı T = 7, boşta kalma süresi 0 olarak sıfırlar ve aktör çöp koleksiyonu geciktirir.</span><span class="sxs-lookup"><span data-stu-id="1aab2-153">An actor method call at T=7 resets the idle time to 0 and delays the garbage collection of the actor.</span></span>
* <span data-ttu-id="1aab2-154">Aktör anımsatıcı geri çağırma T = 14 yürütür ve daha fazla aktör çöp koleksiyonu geciktirir.</span><span class="sxs-lookup"><span data-stu-id="1aab2-154">An actor reminder callback executes at T=14 and further delays the garbage collection of the actor.</span></span>
* <span data-ttu-id="1aab2-155">Çöp toplama tarama T = 25 adresindeki sırasında aktör'ın boşta kalma süresi son 10 boşta kalma zaman aşımı aşıyor ve aktör toplanacak olan.</span><span class="sxs-lookup"><span data-stu-id="1aab2-155">During the garbage collection scan at T=25, the actor's idle time finally exceeds the idle timeout of 10, and the actor is garbage collected.</span></span>

<span data-ttu-id="1aab2-156">Bir oyuncu hiçbir zaman bu yöntemin yürütülmesi için ne kadar süre olsun yöntemlerinden birini yürütülürken toplanacak olmaz.</span><span class="sxs-lookup"><span data-stu-id="1aab2-156">An actor will never be garbage collected while it is executing one of its methods, no matter how much time is spent in executing that method.</span></span> <span data-ttu-id="1aab2-157">Daha önce belirtildiği gibi aktör arabirim yöntemleri ve anımsatıcı geri aramalar yürütülmesini aktör'ın boşta kalma süresi 0 olarak sıfırlayarak çöp toplama engeller.</span><span class="sxs-lookup"><span data-stu-id="1aab2-157">As mentioned earlier, the execution of actor interface methods and reminder callbacks prevents garbage collection by resetting the actor's idle time to 0.</span></span> <span data-ttu-id="1aab2-158">Zamanlayıcı geri aramalar yürütülmesi boşta kalma süresi 0 olarak sıfırlamaz.</span><span class="sxs-lookup"><span data-stu-id="1aab2-158">The execution of timer callbacks does not reset the idle time to 0.</span></span> <span data-ttu-id="1aab2-159">Ancak, aktör çöp koleksiyonu Zamanlayıcı geri yürütme tamamlanana kadar ertelenir.</span><span class="sxs-lookup"><span data-stu-id="1aab2-159">However, the garbage collection of the actor is deferred until the timer callback has completed execution.</span></span>

## <a name="deleting-actors-and-their-state"></a><span data-ttu-id="1aab2-160">Aktör ve durumlarına silme</span><span class="sxs-lookup"><span data-stu-id="1aab2-160">Deleting actors and their state</span></span>
<span data-ttu-id="1aab2-161">Çöp toplama devre dışı bırakılan aktör yalnızca aktör nesnesini temizler, ancak bir aktör ait durum Yöneticisi'nde depolanan verileri kaldırmaz.</span><span class="sxs-lookup"><span data-stu-id="1aab2-161">Garbage collection of deactivated actors only cleans up the actor object, but it does not remove data that is stored in an actor's State Manager.</span></span> <span data-ttu-id="1aab2-162">Bir aktör yeniden etkinleştirildiğinde, verileri yeniden durum Yöneticisi aracılığıyla için kullanılabilir hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="1aab2-162">When an actor is re-activated, its data is again made available to it through the State Manager.</span></span> <span data-ttu-id="1aab2-163">Burada aktörler durum Yöneticisi'nde veri depolamak ve devre dışı ancak hiçbir zaman yeniden etkinleştirilmiş durumda, kendi verilerini temizle gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="1aab2-163">In cases where actors store data in State Manager and are deactivated but never re-activated, it may be necessary to clean up their data.</span></span>

<span data-ttu-id="1aab2-164">[Aktör hizmeti](service-fabric-reliable-actors-platform.md) aktörler uzak çağrıyı yapandan silmek için bir işlev sağlar:</span><span class="sxs-lookup"><span data-stu-id="1aab2-164">The [Actor Service](service-fabric-reliable-actors-platform.md) provides a function for deleting actors from a remote caller:</span></span>

```csharp
ActorId actorToDelete = new ActorId(id);

IActorService myActorServiceProxy = ActorServiceProxy.Create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

await myActorServiceProxy.DeleteActorAsync(actorToDelete, cancellationToken)
```
```Java
ActorId actorToDelete = new ActorId(id);

ActorService myActorServiceProxy = ActorServiceProxy.create(
    new Uri("fabric:/MyApp/MyService"), actorToDelete);

myActorServiceProxy.deleteActorAsync(actorToDelete);
```

<span data-ttu-id="1aab2-165">Bir oyuncu silme aktör şu anda etkin olan olup olmadığına bağlı olarak aşağıdaki etkileri gösterir:</span><span class="sxs-lookup"><span data-stu-id="1aab2-165">Deleting an actor has the following effects depending on whether or not the actor is currently active:</span></span>

* <span data-ttu-id="1aab2-166">**Etkin aktör**</span><span class="sxs-lookup"><span data-stu-id="1aab2-166">**Active Actor**</span></span>
  * <span data-ttu-id="1aab2-167">Aktör etkin aktörler listesinden kaldırılır ve devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="1aab2-167">Actor is removed from active actors list and is deactivated.</span></span>
  * <span data-ttu-id="1aab2-168">Durumu kalıcı olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="1aab2-168">Its state is deleted permanently.</span></span>
* <span data-ttu-id="1aab2-169">**Etkin olmayan aktör**</span><span class="sxs-lookup"><span data-stu-id="1aab2-169">**Inactive Actor**</span></span>
  * <span data-ttu-id="1aab2-170">Durumu kalıcı olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="1aab2-170">Its state is deleted permanently.</span></span>

<span data-ttu-id="1aab2-171">Bir oyuncu çağrılamıyor Not Sil aktör yöntemlerinden birini kendisinden aktör çalışma zamanı tek iş parçacıklı erişim uygulamaya aktör çağrısı geçici bir kilidi elde bir aktör çağrısı bağlamı içinde yürütülürken silinemez çünkü.</span><span class="sxs-lookup"><span data-stu-id="1aab2-171">Note that an actor cannot call delete on itself from one of its actor methods because the actor cannot be deleted while executing within an actor call context, in which the runtime has obtained a lock around the actor call to enforce single-threaded access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1aab2-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1aab2-172">Next steps</span></span>
* [<span data-ttu-id="1aab2-173">Aktör zamanlayıcılar ve anımsatıcıları</span><span class="sxs-lookup"><span data-stu-id="1aab2-173">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="1aab2-174">Aktör olayları</span><span class="sxs-lookup"><span data-stu-id="1aab2-174">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="1aab2-175">Aktör yeniden giriş</span><span class="sxs-lookup"><span data-stu-id="1aab2-175">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="1aab2-176">Aktör tanılama ve performans izleme</span><span class="sxs-lookup"><span data-stu-id="1aab2-176">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="1aab2-177">Aktör API başvuru belgeleri</span><span class="sxs-lookup"><span data-stu-id="1aab2-177">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="1aab2-178">C# örnek kod</span><span class="sxs-lookup"><span data-stu-id="1aab2-178">C# Sample code</span></span>](https://github.com/Azure/servicefabric-samples)
* [<span data-ttu-id="1aab2-179">Java örnek kod</span><span class="sxs-lookup"><span data-stu-id="1aab2-179">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-lifecycle/garbage-collection.png
