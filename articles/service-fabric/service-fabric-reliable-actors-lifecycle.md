---
title: "Aktör tabanlı Azure mikro yaşam döngüsünün aaaOverview | Microsoft Docs"
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
ms.openlocfilehash: a7926e372449048f0a579c2c58573754a4a82363
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="actor-lifecycle-automatic-garbage-collection-and-manual-delete"></a><span data-ttu-id="a6732-103">Aktör yaşam döngüsü, otomatik çöp toplama ve el ile silme</span><span class="sxs-lookup"><span data-stu-id="a6732-103">Actor lifecycle, automatic garbage collection, and manual delete</span></span>
<span data-ttu-id="a6732-104">Bir oyuncu etkinleştirilir hello ilk kez yöntemlerinden tooany bir çağrı yapılır.</span><span class="sxs-lookup"><span data-stu-id="a6732-104">An actor is activated hello first time a call is made tooany of its methods.</span></span> <span data-ttu-id="a6732-105">Bir oyuncu devre dışı bırakılmış (Çöp hello aktörler çalışma zamanı tarafından toplanan) ise yapılandırılabilir bir süre için kullanılmaz.</span><span class="sxs-lookup"><span data-stu-id="a6732-105">An actor is deactivated (garbage collected by hello Actors runtime) if it is not used for a configurable period of time.</span></span> <span data-ttu-id="a6732-106">Bir aktör ve durumu da el ile herhangi bir zamanda silinebilir.</span><span class="sxs-lookup"><span data-stu-id="a6732-106">An actor and its state can also be deleted manually at any time.</span></span>

## <a name="actor-activation"></a><span data-ttu-id="a6732-107">Aktör etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="a6732-107">Actor activation</span></span>
<span data-ttu-id="a6732-108">Bir oyuncu etkinleştirildiğinde hello şunlar olur:</span><span class="sxs-lookup"><span data-stu-id="a6732-108">When an actor is activated, hello following occurs:</span></span>

* <span data-ttu-id="a6732-109">Bir oyuncu için bir çağrı gelir ve bir etkin değilse, yeni aktör oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="a6732-109">When a call comes for an actor and one is not already active, a new actor is created.</span></span>
* <span data-ttu-id="a6732-110">Durum koruma hello aktör'ın durumunu yüklenir.</span><span class="sxs-lookup"><span data-stu-id="a6732-110">hello actor's state is loaded if it's maintaining state.</span></span>
* <span data-ttu-id="a6732-111">Merhaba `OnActivateAsync` (C#) veya `onActivateAsync` (hangi hello aktör uygulamasında kılınabilir) (Java) yöntemi çağrılır.</span><span class="sxs-lookup"><span data-stu-id="a6732-111">hello `OnActivateAsync` (C#) or `onActivateAsync` (Java) method (which can be overridden in hello actor implementation) is called.</span></span>
* <span data-ttu-id="a6732-112">Merhaba aktör şimdi etkin olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="a6732-112">hello actor is now considered active.</span></span>

## <a name="actor-deactivation"></a><span data-ttu-id="a6732-113">Aktör devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="a6732-113">Actor deactivation</span></span>
<span data-ttu-id="a6732-114">Bir oyuncu devre dışı bırakıldığında hello şunlar olur:</span><span class="sxs-lookup"><span data-stu-id="a6732-114">When an actor is deactivated, hello following occurs:</span></span>

* <span data-ttu-id="a6732-115">Belirli bir süre için bir aktör kullanılmadığı zaman hello etkin aktörler tablosundan kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="a6732-115">When an actor is not used for some period of time, it is removed from hello Active Actors table.</span></span>
* <span data-ttu-id="a6732-116">Merhaba `OnDeactivateAsync` (C#) veya `onDeactivateAsync` (hangi hello aktör uygulamasında kılınabilir) (Java) yöntemi çağrılır.</span><span class="sxs-lookup"><span data-stu-id="a6732-116">hello `OnDeactivateAsync` (C#) or `onDeactivateAsync` (Java) method (which can be overridden in hello actor implementation) is called.</span></span> <span data-ttu-id="a6732-117">Merhaba aktör tüm hello zamanlayıcılarını temizler.</span><span class="sxs-lookup"><span data-stu-id="a6732-117">This clears all hello timers for hello actor.</span></span> <span data-ttu-id="a6732-118">Aktör işlemleri değişiklikler bu yönteminden çağrılmamalıdır durumu ister.</span><span class="sxs-lookup"><span data-stu-id="a6732-118">Actor operations like state changes should not be called from this method.</span></span>

> [!TIP]
> <span data-ttu-id="a6732-119">Merhaba Fabric aktör çalışma zamanı bazı yayar [olayları ilgili tooactor etkinleştirme ve devre dışı bırakma](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters).</span><span class="sxs-lookup"><span data-stu-id="a6732-119">hello Fabric Actors runtime emits some [events related tooactor activation and deactivation](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters).</span></span> <span data-ttu-id="a6732-120">Bunlar, tanılama ve performans izlemesi kullanışlıdır.</span><span class="sxs-lookup"><span data-stu-id="a6732-120">They are useful in diagnostics and performance monitoring.</span></span>
>
>

### <a name="actor-garbage-collection"></a><span data-ttu-id="a6732-121">Aktör çöp toplama</span><span class="sxs-lookup"><span data-stu-id="a6732-121">Actor garbage collection</span></span>
<span data-ttu-id="a6732-122">Bir aktör devre dışı bırakıldığında başvuruları toohello aktör nesne yayımlandığında ve normal şekilde Merhaba ortak dil çalışma zamanı (CLR) veya java sanal makinesi (JVM) atık toplayıcı tarafından toplanacak olabilir.</span><span class="sxs-lookup"><span data-stu-id="a6732-122">When an actor is deactivated, references toohello actor object are released and it can be garbage collected normally by hello common language runtime (CLR) or java virtual machine (JVM) garbage collector.</span></span> <span data-ttu-id="a6732-123">Çöp toplama yalnızca hello aktör nesnesini temizler; Mevcut **değil** hello aktör'ın durum Yöneticisi'nde depolanan durumunu kaldırın.</span><span class="sxs-lookup"><span data-stu-id="a6732-123">Garbage collection only cleans up hello actor object; it does **not** remove state stored in hello actor's State Manager.</span></span> <span data-ttu-id="a6732-124">Hello sonraki zaman hello aktör etkinleştirilir, yeni bir aktör nesnesi oluşturulur ve durumuna geri yüklenir.</span><span class="sxs-lookup"><span data-stu-id="a6732-124">hello next time hello actor is activated, a new actor object is created and its state is restored.</span></span>

<span data-ttu-id="a6732-125">"Hello amacı devre dışı bırakma ve atık toplama için kullanılan olarak" ne sayar?</span><span class="sxs-lookup"><span data-stu-id="a6732-125">What counts as “being used” for hello purpose of deactivation and garbage collection?</span></span>

* <span data-ttu-id="a6732-126">Çağrı Alma</span><span class="sxs-lookup"><span data-stu-id="a6732-126">Receiving a call</span></span>
* <span data-ttu-id="a6732-127">`IRemindable.ReceiveReminderAsync`(yalnızca hello aktör anımsatıcıları kullanıyorsa geçerlidir) çağrılan yöntemi</span><span class="sxs-lookup"><span data-stu-id="a6732-127">`IRemindable.ReceiveReminderAsync` method being invoked (applicable only if hello actor uses reminders)</span></span>

> [!NOTE]
> <span data-ttu-id="a6732-128">Merhaba aktör zamanlayıcılar kullanıyorsa ve Zamanlayıcı geri çağırma çağrılır, mevcut **değil** "kullanılan" olarak sayısı.</span><span class="sxs-lookup"><span data-stu-id="a6732-128">if hello actor uses timers and its timer callback is invoked, it does **not** count as "being used".</span></span>
>
>

<span data-ttu-id="a6732-129">Biz devre dışı bırakma hello ayrıntılarını geçmeden önce önemli toodefine hello koşulları aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="a6732-129">Before we go into hello details of deactivation, it is important toodefine hello following terms:</span></span>

* <span data-ttu-id="a6732-130">*Tarama aralığı*.</span><span class="sxs-lookup"><span data-stu-id="a6732-130">*Scan interval*.</span></span> <span data-ttu-id="a6732-131">Bu başlangıç aralığı aktörler hangi hello çalışma zamanı, etkin aktörler tablosunu devre dışı bırakılabilir aktörler için tarar ve atık toplanan.</span><span class="sxs-lookup"><span data-stu-id="a6732-131">This is hello interval at which hello Actors runtime scans its Active Actors table for actors that can be deactivated and garbage collected.</span></span> <span data-ttu-id="a6732-132">Bu Hello varsayılan değeri 1 dakikadır.</span><span class="sxs-lookup"><span data-stu-id="a6732-132">hello default value for this is 1 minute.</span></span>
* <span data-ttu-id="a6732-133">*Boşta kalma zaman aşımı*.</span><span class="sxs-lookup"><span data-stu-id="a6732-133">*Idle timeout*.</span></span> <span data-ttu-id="a6732-134">Bu hello bir aktör tooremain kullanılmayan gerektiğini zaman miktarıdır (boş) devre dışı bırakılabilir ve atık toplanan önce.</span><span class="sxs-lookup"><span data-stu-id="a6732-134">This is hello amount of time that an actor needs tooremain unused (idle) before it can be deactivated and garbage collected.</span></span> <span data-ttu-id="a6732-135">Bunun için Hello varsayılan değer 60 dakikadır.</span><span class="sxs-lookup"><span data-stu-id="a6732-135">hello default value for this is 60 minutes.</span></span>

<span data-ttu-id="a6732-136">Genellikle, bu varsayılan toochange gerekmez.</span><span class="sxs-lookup"><span data-stu-id="a6732-136">Typically, you do not need toochange these defaults.</span></span> <span data-ttu-id="a6732-137">Ancak, gerekirse, bu aralıklar üzerinden değiştirilebilir `ActorServiceSettings` kaydederken, [aktör hizmeti](service-fabric-reliable-actors-platform.md):</span><span class="sxs-lookup"><span data-stu-id="a6732-137">However, if necessary, these intervals can be changed through `ActorServiceSettings` when registering your [Actor Service](service-fabric-reliable-actors-platform.md):</span></span>

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
<span data-ttu-id="a6732-138">Her etkin aktör hello aktör çalışma zamanı, (yani kullanılır) boşta zaman hello miktarını izler.</span><span class="sxs-lookup"><span data-stu-id="a6732-138">For each active actor, hello actor runtime keeps track of hello amount of time that it has been idle (i.e. not used).</span></span> <span data-ttu-id="a6732-139">Merhaba aktör çalışma zamanı denetler her hello aktörler her `ScanIntervalInSeconds` çöp olabiliyorsa toosee toplanır ve boşta olması durumunda topladığı `IdleTimeoutInSeconds`.</span><span class="sxs-lookup"><span data-stu-id="a6732-139">hello actor runtime checks each of hello actors every `ScanIntervalInSeconds` toosee if it can be garbage collected and collects it if it has been idle for `IdleTimeoutInSeconds`.</span></span>

<span data-ttu-id="a6732-140">Bir oyuncu kullanılan zaman boşta kalma süresini sıfırlama too0 ' dir.</span><span class="sxs-lookup"><span data-stu-id="a6732-140">Anytime an actor is used, its idle time is reset too0.</span></span> <span data-ttu-id="a6732-141">Bundan sonra yalnızca onu yeniden boşta kalırsa toplanacak hello aktör olabilir `IdleTimeoutInSeconds`.</span><span class="sxs-lookup"><span data-stu-id="a6732-141">After this, hello actor can be garbage collected only if it again remains idle for `IdleTimeoutInSeconds`.</span></span> <span data-ttu-id="a6732-142">Bir aktör toohave değerlendirilir geri çağırma edilmiş bir aktör arabirim yöntemini veya aktör anımsatıcı geri çağırma yürütülürse kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a6732-142">Recall that an actor is considered toohave been used if either an actor interface method or an actor reminder callback is executed.</span></span> <span data-ttu-id="a6732-143">Bir aktör olan **değil** toohave olarak kabul edilen Zamanlayıcı geri çağırma çalıştırıldığında kullanılan.</span><span class="sxs-lookup"><span data-stu-id="a6732-143">An actor is **not** considered toohave been used if its timer callback is executed.</span></span>

<span data-ttu-id="a6732-144">Merhaba Aşağıdaki diyagramda tek aktör tooillustrate hello yaşam döngüsü Bu kavramlar gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a6732-144">hello following diagram shows hello lifecycle of a single actor tooillustrate these concepts.</span></span>

![Boşta kalma süresi örneği][1]

<span data-ttu-id="a6732-146">Merhaba örnek hello etkisini aktör yöntem çağrıları, anımsatıcı ve zamanlayıcılar bu aktör hello ömrü gösterir.</span><span class="sxs-lookup"><span data-stu-id="a6732-146">hello example shows hello impact of actor method calls, reminders, and timers on hello lifetime of this actor.</span></span> <span data-ttu-id="a6732-147">Başlangıç noktaları hello örnek hakkında aşağıdaki tümleştirilmediği şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a6732-147">hello following points about hello example are worth mentioning:</span></span>

* <span data-ttu-id="a6732-148">ScanInterval ve IdleTimeout too5 ve 10 sırasıyla ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="a6732-148">ScanInterval and IdleTimeout are set too5 and 10 respectively.</span></span> <span data-ttu-id="a6732-149">(Bu konudaki Hedefimiz yalnızca tooillustrate hello kavram olduğundan birimleri burada önemli değildir.)</span><span class="sxs-lookup"><span data-stu-id="a6732-149">(Units do not matter here, since our purpose is only tooillustrate hello concept.)</span></span>
* <span data-ttu-id="a6732-150">Merhaba tarama teşkil eden kişilerin toobe çöp toplama T = 0, 5, 10, 15, 20, 25 ' hello tarama aralığı 5 tarafından tanımlandığı şekilde gerçekleşir.</span><span class="sxs-lookup"><span data-stu-id="a6732-150">hello scan for actors toobe garbage collected happens at T=0,5,10,15,20,25, as defined by hello scan interval of 5.</span></span>
* <span data-ttu-id="a6732-151">T = konumundaki 4, 8, 12, 16, 20, 24, düzenli bir süreölçeri başlatılır ve kendi geri çağırmayı yürütür.</span><span class="sxs-lookup"><span data-stu-id="a6732-151">A periodic timer fires at T=4,8,12,16,20,24, and its callback executes.</span></span> <span data-ttu-id="a6732-152">Boşta kalma süresi hello aktör hello etkilemez.</span><span class="sxs-lookup"><span data-stu-id="a6732-152">It does not impact hello idle time of hello actor.</span></span>
* <span data-ttu-id="a6732-153">T = 7 konumundaki bir aktör yöntemi çağrısı hello boşta kalma süresi too0 sıfırlar ve hello aktör hello çöp koleksiyonu geciktirir.</span><span class="sxs-lookup"><span data-stu-id="a6732-153">An actor method call at T=7 resets hello idle time too0 and delays hello garbage collection of hello actor.</span></span>
* <span data-ttu-id="a6732-154">T = 14 aktör anımsatıcı geri çağırmayı yürütür ve daha fazla gecikmeler hello aktör çöp koleksiyonu hello.</span><span class="sxs-lookup"><span data-stu-id="a6732-154">An actor reminder callback executes at T=14 and further delays hello garbage collection of hello actor.</span></span>
* <span data-ttu-id="a6732-155">Merhaba atık toplama taramada T = 25, sırasında hello aktör'ın boşta kalma süresi son 10 hello boşta kalma zaman aşımı aşıyor ve hello aktör toplanacak olan.</span><span class="sxs-lookup"><span data-stu-id="a6732-155">During hello garbage collection scan at T=25, hello actor's idle time finally exceeds hello idle timeout of 10, and hello actor is garbage collected.</span></span>

<span data-ttu-id="a6732-156">Bir oyuncu hiçbir zaman bu yöntemin yürütülmesi için ne kadar süre olsun yöntemlerinden birini yürütülürken toplanacak olmaz.</span><span class="sxs-lookup"><span data-stu-id="a6732-156">An actor will never be garbage collected while it is executing one of its methods, no matter how much time is spent in executing that method.</span></span> <span data-ttu-id="a6732-157">Daha önce belirtildiği gibi hello yürütülmesini aktör arabirim yöntemleri ve anımsatıcı geri aramalar hello aktör'ın boşta kalma süresi too0 sıfırlayarak çöp toplama engeller.</span><span class="sxs-lookup"><span data-stu-id="a6732-157">As mentioned earlier, hello execution of actor interface methods and reminder callbacks prevents garbage collection by resetting hello actor's idle time too0.</span></span> <span data-ttu-id="a6732-158">Zamanlayıcı geri aramalar Hello yürütülmesi hello boşta kalma süresi too0 sıfırlamaz.</span><span class="sxs-lookup"><span data-stu-id="a6732-158">hello execution of timer callbacks does not reset hello idle time too0.</span></span> <span data-ttu-id="a6732-159">Ancak, hello aktör hello çöp koleksiyonu Hello Zamanlayıcı geri yürütme tamamlanana kadar ertelenir.</span><span class="sxs-lookup"><span data-stu-id="a6732-159">However, hello garbage collection of hello actor is deferred until hello timer callback has completed execution.</span></span>

## <a name="deleting-actors-and-their-state"></a><span data-ttu-id="a6732-160">Aktör ve durumlarına silme</span><span class="sxs-lookup"><span data-stu-id="a6732-160">Deleting actors and their state</span></span>
<span data-ttu-id="a6732-161">Çöp toplama devre dışı bırakılan aktör yalnızca hello aktör nesnesini temizler, ancak bir aktör ait durum Yöneticisi'nde depolanan verileri kaldırmaz.</span><span class="sxs-lookup"><span data-stu-id="a6732-161">Garbage collection of deactivated actors only cleans up hello actor object, but it does not remove data that is stored in an actor's State Manager.</span></span> <span data-ttu-id="a6732-162">Bir aktör yeniden etkinleştirildiğinde, verileri yeniden kullanılabilir tooit hello durum Yöneticisi aracılığıyla yapılır.</span><span class="sxs-lookup"><span data-stu-id="a6732-162">When an actor is re-activated, its data is again made available tooit through hello State Manager.</span></span> <span data-ttu-id="a6732-163">Burada aktörler durum Yöneticisi'nde veri depolamak ve devre dışı ancak hiçbir zaman yeniden etkinleştirilmiş durumda, kendi verilerini gerekli tooclean olabilir.</span><span class="sxs-lookup"><span data-stu-id="a6732-163">In cases where actors store data in State Manager and are deactivated but never re-activated, it may be necessary tooclean up their data.</span></span>

<span data-ttu-id="a6732-164">Merhaba [aktör hizmeti](service-fabric-reliable-actors-platform.md) aktörler uzak çağrıyı yapandan silmek için bir işlev sağlar:</span><span class="sxs-lookup"><span data-stu-id="a6732-164">hello [Actor Service](service-fabric-reliable-actors-platform.md) provides a function for deleting actors from a remote caller:</span></span>

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

<span data-ttu-id="a6732-165">Bir oyuncu silme etkileri hello aktör şu anda etkin olan olup olmadığına bağlı olarak aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="a6732-165">Deleting an actor has hello following effects depending on whether or not hello actor is currently active:</span></span>

* <span data-ttu-id="a6732-166">**Etkin aktör**</span><span class="sxs-lookup"><span data-stu-id="a6732-166">**Active Actor**</span></span>
  * <span data-ttu-id="a6732-167">Aktör etkin aktörler listesinden kaldırılır ve devre dışı bırakılır.</span><span class="sxs-lookup"><span data-stu-id="a6732-167">Actor is removed from active actors list and is deactivated.</span></span>
  * <span data-ttu-id="a6732-168">Durumu kalıcı olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="a6732-168">Its state is deleted permanently.</span></span>
* <span data-ttu-id="a6732-169">**Etkin olmayan aktör**</span><span class="sxs-lookup"><span data-stu-id="a6732-169">**Inactive Actor**</span></span>
  * <span data-ttu-id="a6732-170">Durumu kalıcı olarak silinir.</span><span class="sxs-lookup"><span data-stu-id="a6732-170">Its state is deleted permanently.</span></span>

<span data-ttu-id="a6732-171">Bir oyuncu çağrılamıyor Not Sil aktör yöntemlerinden birini kendisinden hangi hello çalışma zamanı hello aktör çağrısı tooenforce tek iş parçacıklı erişimine geçici bir kilidi elde bir aktör çağrısı bağlamı içinde yürütülürken hello aktör silinemez çünkü.</span><span class="sxs-lookup"><span data-stu-id="a6732-171">Note that an actor cannot call delete on itself from one of its actor methods because hello actor cannot be deleted while executing within an actor call context, in which hello runtime has obtained a lock around hello actor call tooenforce single-threaded access.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6732-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a6732-172">Next steps</span></span>
* [<span data-ttu-id="a6732-173">Aktör zamanlayıcılar ve anımsatıcıları</span><span class="sxs-lookup"><span data-stu-id="a6732-173">Actor timers and reminders</span></span>](service-fabric-reliable-actors-timers-reminders.md)
* [<span data-ttu-id="a6732-174">Aktör olayları</span><span class="sxs-lookup"><span data-stu-id="a6732-174">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="a6732-175">Aktör yeniden giriş</span><span class="sxs-lookup"><span data-stu-id="a6732-175">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="a6732-176">Aktör tanılama ve performans izleme</span><span class="sxs-lookup"><span data-stu-id="a6732-176">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="a6732-177">Aktör API başvuru belgeleri</span><span class="sxs-lookup"><span data-stu-id="a6732-177">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="a6732-178">C# örnek kod</span><span class="sxs-lookup"><span data-stu-id="a6732-178">C# Sample code</span></span>](https://github.com/Azure/servicefabric-samples)
* [<span data-ttu-id="a6732-179">Java örnek kod</span><span class="sxs-lookup"><span data-stu-id="a6732-179">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-lifecycle/garbage-collection.png
