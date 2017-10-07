---
title: "aaaReliable aktörler zamanlayıcılar ve anımsatıcıları | Microsoft Docs"
description: "Giriş tootimers ve Service Fabric güvenilir aktörler için anımsatıcılar."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: 00c48716-569e-4a64-bd6c-25234c85ff4f
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: c5116ec1923014e131130b9f4e86dd1e133bbf7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="actor-timers-and-reminders"></a><span data-ttu-id="cdb6c-103">Aktör zamanlayıcılar ve anımsatıcıları</span><span class="sxs-lookup"><span data-stu-id="cdb6c-103">Actor timers and reminders</span></span>
<span data-ttu-id="cdb6c-104">Aktör zamanlayıcılar veya anımsatıcıları kaydederek kendilerini düzenli çalışma zamanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cdb6c-104">Actors can schedule periodic work on themselves by registering either timers or reminders.</span></span> <span data-ttu-id="cdb6c-105">Bu makalede gösterilmektedir nasıl toouse zamanlayıcılar ve anımsatıcıları ve aralarındaki hello farkları açıklamaktadır.</span><span class="sxs-lookup"><span data-stu-id="cdb6c-105">This article shows how toouse timers and reminders and explains hello differences between them.</span></span>

## <a name="actor-timers"></a><span data-ttu-id="cdb6c-106">Aktör zamanlayıcılar</span><span class="sxs-lookup"><span data-stu-id="cdb6c-106">Actor timers</span></span>
<span data-ttu-id="cdb6c-107">Aktör zamanlayıcılar hello geri arama yöntemleri çalışma zamanı sağlar aktörler hello hello Aç tabanlı eşzamanlılık garanti saygı .NET veya Java Zamanlayıcı tooensure çevresinde basit bir sarmalayıcı sağlar.</span><span class="sxs-lookup"><span data-stu-id="cdb6c-107">Actor timers provide a simple wrapper around a .NET or Java timer tooensure that hello callback methods respect hello turn-based concurrency guarantees that hello Actors runtime provides.</span></span>

<span data-ttu-id="cdb6c-108">Aktör hello kullanabilir `RegisterTimer`(C#) veya `registerTimer`(Java) ve `UnregisterTimer`(C#) veya `unregisterTimer`kendi tabanında (Java) yöntemleri sınıfı tooregister ve bunların zamanlayıcılar kaldırılamadı.</span><span class="sxs-lookup"><span data-stu-id="cdb6c-108">Actors can use hello `RegisterTimer`(C#) or `registerTimer`(Java)  and `UnregisterTimer`(C#) or `unregisterTimer`(Java) methods on their base class tooregister and unregister their timers.</span></span> <span data-ttu-id="cdb6c-109">Aşağıdaki örnek Hello süreölçer API'lerini hello kullanımını göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="cdb6c-109">hello example below shows hello use of timer APIs.</span></span> <span data-ttu-id="cdb6c-110">Merhaba API'leri: çok benzer toohello .NET Zamanlayıcı veya Java Zamanlayıcı.</span><span class="sxs-lookup"><span data-stu-id="cdb6c-110">hello APIs are very similar toohello .NET timer or Java timer.</span></span> <span data-ttu-id="cdb6c-111">Merhaba Zamanlayıcı zamanı geldiğinde bu örnekte, hello hello aktörler çalışma zamanı arama `MoveObject`(C#) veya `moveObject`(Java) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="cdb6c-111">In this example, when hello timer is due, hello Actors runtime will call hello `MoveObject`(C#) or `moveObject`(Java) method.</span></span> <span data-ttu-id="cdb6c-112">Merhaba yöntemi toorespect hello Aç tabanlı eşzamanlılık garanti edilmez.</span><span class="sxs-lookup"><span data-stu-id="cdb6c-112">hello method is guaranteed toorespect hello turn-based concurrency.</span></span> <span data-ttu-id="cdb6c-113">Bu yürütme bu geri çağırma işlemi tamamlanana kadar başka bir aktör yöntemin veya Zamanlayıcı/anımsatıcı geri aramalar ediyor olacağı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="cdb6c-113">This means that no other actor methods or timer/reminder callbacks will be in progress until this callback completes execution.</span></span>

```csharp
class VisualObjectActor : Actor, IVisualObject
{
    private IActorTimer _updateTimer;

    public VisualObjectActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    protected override Task OnActivateAsync()
    {
        ...

        _updateTimer = RegisterTimer(
            MoveObject,                     // Callback method
            null,                           // Parameter toopass toohello callback method
            TimeSpan.FromMilliseconds(15),  // Amount of time toodelay before hello callback is invoked
            TimeSpan.FromMilliseconds(15)); // Time interval between invocations of hello callback method

        return base.OnActivateAsync();
    }

    protected override Task OnDeactivateAsync()
    {
        if (_updateTimer != null)
        {
            UnregisterTimer(_updateTimer);
        }

        return base.OnDeactivateAsync();
    }

    private Task MoveObject(object state)
    {
        ...
        return Task.FromResult(true);
    }
}
```
```Java
public class VisualObjectActorImpl extends FabricActor implements VisualObjectActor
{
    private ActorTimer updateTimer;

    public VisualObjectActorImpl(FabricActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    @Override
    protected CompletableFuture onActivateAsync()
    {
        ...

        return this.stateManager()
                .getOrAddStateAsync(
                        stateName,
                        VisualObject.createRandom(
                                this.getId().toString(),
                                new Random(this.getId().toString().hashCode())))
                .thenApply((r) -> {
                    this.registerTimer(
                            (o) -> this.moveObject(o),                        // Callback method
                            "moveObject",
                            null,                                             // Parameter toopass toohello callback method
                            Duration.ofMillis(10),                            // Amount of time toodelay before hello callback is invoked
                            Duration.ofMillis(timerIntervalInMilliSeconds));  // Time interval between invocations of hello callback method
                    return null;
                });
    }

    @Override
    protected CompletableFuture onDeactivateAsync()
    {
        if (updateTimer != null)
        {
            unregisterTimer(updateTimer);
        }

        return super.onDeactivateAsync();
    }

    private CompletableFuture moveObject(Object state)
    {
        ...
        return this.stateManager().getStateAsync(this.stateName).thenCompose(v -> {
            VisualObject v1 = (VisualObject)v;
            v1.move();
            return (CompletableFuture<?>)this.stateManager().setStateAsync(stateName, v1).
                    thenApply(r -> {
                      ...
                      return null;});
        });
    }
}
```

<span data-ttu-id="cdb6c-114">yürütme Hello geri çağırma tamamlandıktan sonra hello sonraki süreyi hello süreölçer başlatır.</span><span class="sxs-lookup"><span data-stu-id="cdb6c-114">hello next period of hello timer starts after hello callback completes execution.</span></span> <span data-ttu-id="cdb6c-115">Bu, hello geri arama yürütüyor ve hello geri araması bitirdiğinde kullanmaya çalışırken bu hello Zamanlayıcı durdurulduğunda anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="cdb6c-115">This implies that hello timer is stopped while hello callback is executing and is started when hello callback finishes.</span></span>

<span data-ttu-id="cdb6c-116">Merhaba aktörler çalışma zamanı hello geri araması bitirdiğinde toohello aktör'ın durum Yöneticisi yapılan değişiklikleri kaydeder.</span><span class="sxs-lookup"><span data-stu-id="cdb6c-116">hello Actors runtime saves changes made toohello actor's State Manager when hello callback finishes.</span></span> <span data-ttu-id="cdb6c-117">Merhaba durum kaydetme işleminde bir hata meydana gelirse, söz konusu aktör nesne devre dışı bırakılır ve yeni bir örneğini etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="cdb6c-117">If an error occurs in saving hello state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="cdb6c-118">Çöp toplama bir parçası olarak Hello aktör devre dışı bırakıldığında tüm zamanlayıcılar durdurulur.</span><span class="sxs-lookup"><span data-stu-id="cdb6c-118">All timers are stopped when hello actor is deactivated as part of garbage collection.</span></span> <span data-ttu-id="cdb6c-119">Bir zamanlayıcı geri aramalar bundan sonra çağrılır.</span><span class="sxs-lookup"><span data-stu-id="cdb6c-119">No timer callbacks are invoked after that.</span></span> <span data-ttu-id="cdb6c-120">Ayrıca, hello aktörler çalışma zamanı devre dışı bırakma önce çalışmakta olan hello zamanlayıcılar hakkında hiçbir bilgi sürdürmez.</span><span class="sxs-lookup"><span data-stu-id="cdb6c-120">Also, hello Actors runtime does not retain any information about hello timers that were running before deactivation.</span></span> <span data-ttu-id="cdb6c-121">Bu toohello aktör tooregister hello gelecekteki etkinleştirildiğinde, gereken tüm zamanlayıcılar olur.</span><span class="sxs-lookup"><span data-stu-id="cdb6c-121">It is up toohello actor tooregister any timers that it needs when it is reactivated in hello future.</span></span> <span data-ttu-id="cdb6c-122">Daha fazla bilgi için üzerinde hello bölümüne bakın. [aktör çöp toplama](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="cdb6c-122">For more information, see hello section on [actor garbage collection](service-fabric-reliable-actors-lifecycle.md).</span></span>

## <a name="actor-reminders"></a><span data-ttu-id="cdb6c-123">Aktör anımsatıcıları</span><span class="sxs-lookup"><span data-stu-id="cdb6c-123">Actor reminders</span></span>
<span data-ttu-id="cdb6c-124">Anımsatıcıları olan bir mekanizma tootrigger bir aktör üzerinde kalıcı geri aramalar kez belirtildi.</span><span class="sxs-lookup"><span data-stu-id="cdb6c-124">Reminders are a mechanism tootrigger persistent callbacks on an actor at specified times.</span></span> <span data-ttu-id="cdb6c-125">İşlevlerine benzer tootimers ' dir.</span><span class="sxs-lookup"><span data-stu-id="cdb6c-125">Their functionality is similar tootimers.</span></span> <span data-ttu-id="cdb6c-126">Ancak zamanlayıcılar anımsatıcıları tüm koşullar altında hello aktör açıkça bunları kaydını siler veya hello aktör açıkça silinene kadar tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="cdb6c-126">But unlike timers, reminders are triggered under all circumstances until hello actor explicitly unregisters them or hello actor is explicitly deleted.</span></span> <span data-ttu-id="cdb6c-127">Özellikle, Hello aktörler çalışma zamanı hello aktör'ın anımsatıcıları hakkında bilgi devam ederse çünkü anımsatıcıları aktör deactivations ve yük devretme işlemlerini arasında tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="cdb6c-127">Specifically, reminders are triggered across actor deactivations and failovers because hello Actors runtime persists information about hello actor's reminders.</span></span>

<span data-ttu-id="cdb6c-128">tooregister anımsatıcısı, bir aktör çağırır hello `RegisterReminderAsync` hello aşağıdaki örnekte gösterildiği gibi hello temel sınıf üzerinde sağlanan yöntemi:</span><span class="sxs-lookup"><span data-stu-id="cdb6c-128">tooregister a reminder, an actor calls hello `RegisterReminderAsync` method provided on hello base class, as shown in hello following example:</span></span>

```csharp
protected override async Task OnActivateAsync()
{
    string reminderName = "Pay cell phone bill";
    int amountInDollars = 100;

    IActorReminder reminderRegistration = await this.RegisterReminderAsync(
        reminderName,
        BitConverter.GetBytes(amountInDollars),
        TimeSpan.FromDays(3),
        TimeSpan.FromDays(1));
}
```

```Java
@Override
protected CompletableFuture onActivateAsync()
{
    String reminderName = "Pay cell phone bill";
    int amountInDollars = 100;

    ActorReminder reminderRegistration = this.registerReminderAsync(
            reminderName,
            state,
            dueTime,    //hello amount of time toodelay before firing hello reminder
            period);    //hello time interval between firing of reminders
}
```

<span data-ttu-id="cdb6c-129">Bu örnekte, `"Pay cell phone bill"` hello anımsatıcı adıdır.</span><span class="sxs-lookup"><span data-stu-id="cdb6c-129">In this example, `"Pay cell phone bill"` is hello reminder name.</span></span> <span data-ttu-id="cdb6c-130">Aktör kullanır hello bir dize budur toouniquely anımsatıcısı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="cdb6c-130">This is a string that hello actor uses toouniquely identify a reminder.</span></span> <span data-ttu-id="cdb6c-131">`BitConverter.GetBytes(amountInDollars)`(C#) hello anımsatıcı'yla ilişkili hello bağlamdır.</span><span class="sxs-lookup"><span data-stu-id="cdb6c-131">`BitConverter.GetBytes(amountInDollars)`(C#) is hello context that is associated with hello reminder.</span></span> <span data-ttu-id="cdb6c-132">Bu geri toohello Aktör bir bağımsız değişken toohello anımsatıcı geri çağırma, yani geçirilir `IRemindable.ReceiveReminderAsync`(C#) veya `Remindable.receiveReminderAsync`(Java).</span><span class="sxs-lookup"><span data-stu-id="cdb6c-132">It will be passed back toohello actor as an argument toohello reminder callback, i.e. `IRemindable.ReceiveReminderAsync`(C#) or `Remindable.receiveReminderAsync`(Java).</span></span>

<span data-ttu-id="cdb6c-133">Anımsatıcıları kullanmak aktörler hello uygulanmalı `IRemindable` hello aşağıdaki örnekte gösterildiği gibi arabirim.</span><span class="sxs-lookup"><span data-stu-id="cdb6c-133">Actors that use reminders must implement hello `IRemindable` interface, as shown in hello example below.</span></span>

```csharp
public class ToDoListActor : Actor, IToDoListActor, IRemindable
{
    public ToDoListActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task ReceiveReminderAsync(string reminderName, byte[] context, TimeSpan dueTime, TimeSpan period)
    {
        if (reminderName.Equals("Pay cell phone bill"))
        {
            int amountToPay = BitConverter.ToInt32(context, 0);
            System.Console.WriteLine("Please pay your cell phone bill of ${0}!", amountToPay);
        }
        return Task.FromResult(true);
    }
}
```
```Java
public class ToDoListActorImpl extends FabricActor implements ToDoListActor, Remindable
{
    public ToDoListActor(FabricActorService actorService, ActorId actorId)
    {
        super(actorService, actorId);
    }

    public CompletableFuture receiveReminderAsync(String reminderName, byte[] context, Duration dueTime, Duration period)
    {
        if (reminderName.equals("Pay cell phone bill"))
        {
            int amountToPay = ByteBuffer.wrap(context).getInt();
            System.out.println("Please pay your cell phone bill of " + amountToPay);
        }
        return CompletableFuture.completedFuture(true);
    }

```

<span data-ttu-id="cdb6c-134">Bir anımsatıcı tetiklendiğinde hello Reliable Actors çalışma zamanı hello çağıracağı `ReceiveReminderAsync`(C#) veya `receiveReminderAsync`hello aktör yöntemi (Java).</span><span class="sxs-lookup"><span data-stu-id="cdb6c-134">When a reminder is triggered, hello Reliable Actors runtime will invoke hello  `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method on hello Actor.</span></span> <span data-ttu-id="cdb6c-135">Bir aktör birden çok anımsatıcıları kaydetmek ve hello `ReceiveReminderAsync`(C#) veya `receiveReminderAsync`(Java) yöntem çağrıldığında bu anımsatıcılar birini ne zaman tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="cdb6c-135">An actor can register multiple reminders, and hello `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method is invoked when any of those reminders is triggered.</span></span> <span data-ttu-id="cdb6c-136">Merhaba aktör toohello içinde geçirilen hello anımsatıcı adı kullanabilir `ReceiveReminderAsync`(C#) veya `receiveReminderAsync`(Java) yöntemi toofigure hangi anımsatıcı tetiklendi.</span><span class="sxs-lookup"><span data-stu-id="cdb6c-136">hello actor can use hello reminder name that is passed in toohello `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method toofigure out which reminder was triggered.</span></span>

<span data-ttu-id="cdb6c-137">Merhaba aktörler çalışma zamanı kaydeder hello aktör'ın durumdayken hello `ReceiveReminderAsync`(C#) veya `receiveReminderAsync`(Java) çağrı tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="cdb6c-137">hello Actors runtime saves hello actor's state when hello `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) call finishes.</span></span> <span data-ttu-id="cdb6c-138">Merhaba durum kaydetme işleminde bir hata meydana gelirse, söz konusu aktör nesne devre dışı bırakılır ve yeni bir örneğini etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="cdb6c-138">If an error occurs in saving hello state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="cdb6c-139">toounregister anımsatıcısı, bir aktör çağırır hello `UnregisterReminderAsync`(C#) veya `unregisterReminderAsync`(Java) yöntemini hello aşağıdaki örnekte gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="cdb6c-139">toounregister a reminder, an actor calls hello `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method, as shown in hello examples below.</span></span>

```csharp
IActorReminder reminder = GetReminder("Pay cell phone bill");
Task reminderUnregistration = UnregisterReminderAsync(reminder);
```
```Java
ActorReminder reminder = getReminder("Pay cell phone bill");
CompletableFuture reminderUnregistration = unregisterReminderAsync(reminder);
```

<span data-ttu-id="cdb6c-140">Yukarıda gösterildiği gibi hello `UnregisterReminderAsync`(C#) veya `unregisterReminderAsync`(Java) yöntemi kabul eden bir `IActorReminder`(C#) veya `ActorReminder`(Java) arabirimi.</span><span class="sxs-lookup"><span data-stu-id="cdb6c-140">As shown above, hello `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method accepts an `IActorReminder`(C#) or `ActorReminder`(Java) interface.</span></span> <span data-ttu-id="cdb6c-141">Merhaba aktör temel sınıf destekleyen bir `GetReminder`(C#) veya `getReminder`kullanılan tooretrieve hello olabilir (Java) yöntemi `IActorReminder`(C#) veya `ActorReminder`hello anımsatıcı adı geçirerek (Java) arabirimi.</span><span class="sxs-lookup"><span data-stu-id="cdb6c-141">hello actor base class supports a `GetReminder`(C#) or `getReminder`(Java) method that can be used tooretrieve hello `IActorReminder`(C#) or `ActorReminder`(Java) interface by passing in hello reminder name.</span></span> <span data-ttu-id="cdb6c-142">Merhaba aktör toopersist hello gereksinimi olmadığından bu uygundur `IActorReminder`(C#) veya `ActorReminder`hello döndürülen (Java) arabirimi `RegisterReminder`(C#) veya `registerReminder`(Java) yöntem çağrısı.</span><span class="sxs-lookup"><span data-stu-id="cdb6c-142">This is convenient because hello actor does not need toopersist hello `IActorReminder`(C#) or `ActorReminder`(Java) interface that was returned from hello `RegisterReminder`(C#) or `registerReminder`(Java) method call.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cdb6c-143">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="cdb6c-143">Next Steps</span></span>
<span data-ttu-id="cdb6c-144">Güvenilir aktör olayları ve yeniden giriş hakkında bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="cdb6c-144">Learn about Reliable Actor events and reentrancy:</span></span>
* [<span data-ttu-id="cdb6c-145">Aktör olayları</span><span class="sxs-lookup"><span data-stu-id="cdb6c-145">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="cdb6c-146">Aktör yeniden giriş</span><span class="sxs-lookup"><span data-stu-id="cdb6c-146">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
