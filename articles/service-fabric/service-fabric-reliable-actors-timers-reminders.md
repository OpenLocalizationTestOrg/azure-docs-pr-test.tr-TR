---
title: "Güvenilir aktörler zamanlayıcılar ve anımsatıcıları | Microsoft Docs"
description: "Service Fabric Reliable Actors zamanlayıcılar ve anımsatıcıları için giriş."
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
ms.openlocfilehash: 06b026ce06e0f16a77ac238de0af2263f272933c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="actor-timers-and-reminders"></a><span data-ttu-id="33853-103">Aktör zamanlayıcılar ve anımsatıcıları</span><span class="sxs-lookup"><span data-stu-id="33853-103">Actor timers and reminders</span></span>
<span data-ttu-id="33853-104">Aktör zamanlayıcılar veya anımsatıcıları kaydederek kendilerini düzenli çalışma zamanlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="33853-104">Actors can schedule periodic work on themselves by registering either timers or reminders.</span></span> <span data-ttu-id="33853-105">Bu makalede zamanlayıcılar ve anımsatıcıları nasıl kullanılacağını gösterir ve bunları arasındaki farklar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="33853-105">This article shows how to use timers and reminders and explains the differences between them.</span></span>

## <a name="actor-timers"></a><span data-ttu-id="33853-106">Aktör zamanlayıcılar</span><span class="sxs-lookup"><span data-stu-id="33853-106">Actor timers</span></span>
<span data-ttu-id="33853-107">Aktör zamanlayıcılar aktörler çalışma zamanı sağladığını geri arama yöntemleri Aç tabanlı eşzamanlılık saygı emin olmak için .NET veya Java bir zamanlayıcı çevresinde basit bir sarmalayıcı garanti sağlar.</span><span class="sxs-lookup"><span data-stu-id="33853-107">Actor timers provide a simple wrapper around a .NET or Java timer to ensure that the callback methods respect the turn-based concurrency guarantees that the Actors runtime provides.</span></span>

<span data-ttu-id="33853-108">Aktör kullanabileceğiniz `RegisterTimer`(C#) veya `registerTimer`(Java) ve `UnregisterTimer`(C#) veya `unregisterTimer`(Java) yöntemlere kaydetmek ve bunların zamanlayıcılar kaydı için temel sınıf.</span><span class="sxs-lookup"><span data-stu-id="33853-108">Actors can use the `RegisterTimer`(C#) or `registerTimer`(Java)  and `UnregisterTimer`(C#) or `unregisterTimer`(Java) methods on their base class to register and unregister their timers.</span></span> <span data-ttu-id="33853-109">Aşağıdaki örnek, süreölçer API'lerini kullanımını gösterir.</span><span class="sxs-lookup"><span data-stu-id="33853-109">The example below shows the use of timer APIs.</span></span> <span data-ttu-id="33853-110">API'ler .NET Zamanlayıcı veya Java Zamanlayıcı çok benzer.</span><span class="sxs-lookup"><span data-stu-id="33853-110">The APIs are very similar to the .NET timer or Java timer.</span></span> <span data-ttu-id="33853-111">Bu örnekte, Zamanlayıcı zamanı geldiğinde aktörler çalışma zamanı çağıracak `MoveObject`(C#) veya `moveObject`(Java) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="33853-111">In this example, when the timer is due, the Actors runtime will call the `MoveObject`(C#) or `moveObject`(Java) method.</span></span> <span data-ttu-id="33853-112">Yöntemi, dönüş tabanlı eşzamanlılık cevaben sağlanır.</span><span class="sxs-lookup"><span data-stu-id="33853-112">The method is guaranteed to respect the turn-based concurrency.</span></span> <span data-ttu-id="33853-113">Bu yürütme bu geri çağırma işlemi tamamlanana kadar başka bir aktör yöntemin veya Zamanlayıcı/anımsatıcı geri aramalar ediyor olacağı anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="33853-113">This means that no other actor methods or timer/reminder callbacks will be in progress until this callback completes execution.</span></span>

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
            null,                           // Parameter to pass to the callback method
            TimeSpan.FromMilliseconds(15),  // Amount of time to delay before the callback is invoked
            TimeSpan.FromMilliseconds(15)); // Time interval between invocations of the callback method

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
                            null,                                             // Parameter to pass to the callback method
                            Duration.ofMillis(10),                            // Amount of time to delay before the callback is invoked
                            Duration.ofMillis(timerIntervalInMilliSeconds));  // Time interval between invocations of the callback method
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

<span data-ttu-id="33853-114">Geri çağırma yürütme tamamlandıktan sonra sonraki süreyi süreölçer başlatır.</span><span class="sxs-lookup"><span data-stu-id="33853-114">The next period of the timer starts after the callback completes execution.</span></span> <span data-ttu-id="33853-115">Bu geri arama yürütüyor ve geri arama tamamlandığında başlatılan Zamanlayıcı durdurulduğunda anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="33853-115">This implies that the timer is stopped while the callback is executing and is started when the callback finishes.</span></span>

<span data-ttu-id="33853-116">Aktörler çalışma zamanı geri araması bitirdiğinde aktör ait durum Yöneticisi için yapılan değişiklikleri kaydeder.</span><span class="sxs-lookup"><span data-stu-id="33853-116">The Actors runtime saves changes made to the actor's State Manager when the callback finishes.</span></span> <span data-ttu-id="33853-117">Durum kaydetme işleminde bir hata meydana gelirse, söz konusu aktör nesne devre dışı bırakılır ve yeni bir örneğini etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="33853-117">If an error occurs in saving the state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="33853-118">Aktör çöp toplama bir parçası olarak devre dışı bırakıldığında tüm zamanlayıcılar durdurulur.</span><span class="sxs-lookup"><span data-stu-id="33853-118">All timers are stopped when the actor is deactivated as part of garbage collection.</span></span> <span data-ttu-id="33853-119">Bir zamanlayıcı geri aramalar bundan sonra çağrılır.</span><span class="sxs-lookup"><span data-stu-id="33853-119">No timer callbacks are invoked after that.</span></span> <span data-ttu-id="33853-120">Ayrıca, aktörler çalışma zamanı devre dışı bırakma önce çalışmakta olan zamanlayıcılar hakkında hiçbir bilgi sürdürmez.</span><span class="sxs-lookup"><span data-stu-id="33853-120">Also, the Actors runtime does not retain any information about the timers that were running before deactivation.</span></span> <span data-ttu-id="33853-121">Gelecekte etkinleştirildiğinde, gereken tüm zamanlayıcılar kaydetmek için aktör kadar olur.</span><span class="sxs-lookup"><span data-stu-id="33853-121">It is up to the actor to register any timers that it needs when it is reactivated in the future.</span></span> <span data-ttu-id="33853-122">Daha fazla bilgi için bölümüne bakarak [aktör çöp toplama](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="33853-122">For more information, see the section on [actor garbage collection](service-fabric-reliable-actors-lifecycle.md).</span></span>

## <a name="actor-reminders"></a><span data-ttu-id="33853-123">Aktör anımsatıcıları</span><span class="sxs-lookup"><span data-stu-id="33853-123">Actor reminders</span></span>
<span data-ttu-id="33853-124">Anımsatıcıları olan bir aktör üzerinde kalıcı geri aramalar tetiklemek için bir mekanizma kez belirtilebilir.</span><span class="sxs-lookup"><span data-stu-id="33853-124">Reminders are a mechanism to trigger persistent callbacks on an actor at specified times.</span></span> <span data-ttu-id="33853-125">İşlevleri için zamanlayıcılar benzer.</span><span class="sxs-lookup"><span data-stu-id="33853-125">Their functionality is similar to timers.</span></span> <span data-ttu-id="33853-126">Ancak zamanlayıcılar anımsatıcıları tüm koşullar altında aktör açıkça bunları kaydını siler veya aktör açıkça silinene kadar tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="33853-126">But unlike timers, reminders are triggered under all circumstances until the actor explicitly unregisters them or the actor is explicitly deleted.</span></span> <span data-ttu-id="33853-127">Özellikle, aktörler çalışma zamanı aktör'ın anımsatıcıları hakkında bilgi devam ederse çünkü anımsatıcıları aktör deactivations ve yük devretme işlemlerini arasında tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="33853-127">Specifically, reminders are triggered across actor deactivations and failovers because the Actors runtime persists information about the actor's reminders.</span></span>

<span data-ttu-id="33853-128">Bir anımsatıcı kaydetmek için bir aktör çağırır `RegisterReminderAsync` temel sınıf üzerinde aşağıdaki örnekte gösterildiği gibi sağlanan yöntemi:</span><span class="sxs-lookup"><span data-stu-id="33853-128">To register a reminder, an actor calls the `RegisterReminderAsync` method provided on the base class, as shown in the following example:</span></span>

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
            dueTime,    //The amount of time to delay before firing the reminder
            period);    //The time interval between firing of reminders
}
```

<span data-ttu-id="33853-129">Bu örnekte, `"Pay cell phone bill"` anımsatıcı adıdır.</span><span class="sxs-lookup"><span data-stu-id="33853-129">In this example, `"Pay cell phone bill"` is the reminder name.</span></span> <span data-ttu-id="33853-130">Bu aktör anımsatıcısı benzersiz şekilde tanımlamak için kullandığı bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="33853-130">This is a string that the actor uses to uniquely identify a reminder.</span></span> <span data-ttu-id="33853-131">`BitConverter.GetBytes(amountInDollars)`(C#) olduğundan anımsatıcı'yla ilişkili bağlam.</span><span class="sxs-lookup"><span data-stu-id="33853-131">`BitConverter.GetBytes(amountInDollars)`(C#) is the context that is associated with the reminder.</span></span> <span data-ttu-id="33853-132">Bu geri aktör anımsatıcı geri çağırma bağımsız değişken olarak yani geçirilir `IRemindable.ReceiveReminderAsync`(C#) veya `Remindable.receiveReminderAsync`(Java).</span><span class="sxs-lookup"><span data-stu-id="33853-132">It will be passed back to the actor as an argument to the reminder callback, i.e. `IRemindable.ReceiveReminderAsync`(C#) or `Remindable.receiveReminderAsync`(Java).</span></span>

<span data-ttu-id="33853-133">Anımsatıcıları kullanmak aktörler uygulanmalı `IRemindable` , aşağıdaki örnekte gösterildiği gibi arabirim.</span><span class="sxs-lookup"><span data-stu-id="33853-133">Actors that use reminders must implement the `IRemindable` interface, as shown in the example below.</span></span>

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

<span data-ttu-id="33853-134">Bir anımsatıcı tetiklendiğinde Reliable Actors çalışma zamanı çağıracağı `ReceiveReminderAsync`(C#) veya `receiveReminderAsync`aktör yöntemi (Java).</span><span class="sxs-lookup"><span data-stu-id="33853-134">When a reminder is triggered, the Reliable Actors runtime will invoke the  `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method on the Actor.</span></span> <span data-ttu-id="33853-135">Bir oyuncu birden çok anımsatıcıları kaydedebilirsiniz ve `ReceiveReminderAsync`(C#) veya `receiveReminderAsync`(Java) yöntem çağrıldığında bu anımsatıcılar birini ne zaman tetiklenir.</span><span class="sxs-lookup"><span data-stu-id="33853-135">An actor can register multiple reminders, and the `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method is invoked when any of those reminders is triggered.</span></span> <span data-ttu-id="33853-136">Aktör için geçirilen anımsatıcı adı kullanabilirsiniz `ReceiveReminderAsync`(C#) veya `receiveReminderAsync`hangi anımsatıcı tetiklendi şekilde yöntemi (Java).</span><span class="sxs-lookup"><span data-stu-id="33853-136">The actor can use the reminder name that is passed in to the `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) method to figure out which reminder was triggered.</span></span>

<span data-ttu-id="33853-137">Çalışma zamanı kaydeder aktör 's aktörler duruma `ReceiveReminderAsync`(C#) veya `receiveReminderAsync`(Java) çağrı tamamlanır.</span><span class="sxs-lookup"><span data-stu-id="33853-137">The Actors runtime saves the actor's state when the `ReceiveReminderAsync`(C#) or `receiveReminderAsync`(Java) call finishes.</span></span> <span data-ttu-id="33853-138">Durum kaydetme işleminde bir hata meydana gelirse, söz konusu aktör nesne devre dışı bırakılır ve yeni bir örneğini etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="33853-138">If an error occurs in saving the state, that actor object will be deactivated and a new instance will be activated.</span></span>

<span data-ttu-id="33853-139">Bir aktör anımsatıcısı kaydı çağrılar `UnregisterReminderAsync`(C#) veya `unregisterReminderAsync`(Java) yöntemi, aşağıdaki örneklerde gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="33853-139">To unregister a reminder, an actor calls the `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method, as shown in the examples below.</span></span>

```csharp
IActorReminder reminder = GetReminder("Pay cell phone bill");
Task reminderUnregistration = UnregisterReminderAsync(reminder);
```
```Java
ActorReminder reminder = getReminder("Pay cell phone bill");
CompletableFuture reminderUnregistration = unregisterReminderAsync(reminder);
```

<span data-ttu-id="33853-140">Yukarıda gösterildiği gibi `UnregisterReminderAsync`(C#) veya `unregisterReminderAsync`(Java) yöntemi kabul eden bir `IActorReminder`(C#) veya `ActorReminder`(Java) arabirimi.</span><span class="sxs-lookup"><span data-stu-id="33853-140">As shown above, the `UnregisterReminderAsync`(C#) or `unregisterReminderAsync`(Java) method accepts an `IActorReminder`(C#) or `ActorReminder`(Java) interface.</span></span> <span data-ttu-id="33853-141">Aktör temel sınıf destekleyen bir `GetReminder`(C#) veya `getReminder`almak için kullanılır (Java) yöntemi `IActorReminder`(C#) veya `ActorReminder`anımsatıcı adı geçirerek (Java) arabirimi.</span><span class="sxs-lookup"><span data-stu-id="33853-141">The actor base class supports a `GetReminder`(C#) or `getReminder`(Java) method that can be used to retrieve the `IActorReminder`(C#) or `ActorReminder`(Java) interface by passing in the reminder name.</span></span> <span data-ttu-id="33853-142">Aktör kalıcı gerek yoktur çünkü bu uygundur `IActorReminder`(C#) veya `ActorReminder`döndürüldü (Java) arabirimi `RegisterReminder`(C#) veya `registerReminder`(Java) yöntem çağrısı.</span><span class="sxs-lookup"><span data-stu-id="33853-142">This is convenient because the actor does not need to persist the `IActorReminder`(C#) or `ActorReminder`(Java) interface that was returned from the `RegisterReminder`(C#) or `registerReminder`(Java) method call.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33853-143">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="33853-143">Next Steps</span></span>
<span data-ttu-id="33853-144">Güvenilir aktör olayları ve yeniden giriş hakkında bilgi edinin:</span><span class="sxs-lookup"><span data-stu-id="33853-144">Learn about Reliable Actor events and reentrancy:</span></span>
* [<span data-ttu-id="33853-145">Aktör olayları</span><span class="sxs-lookup"><span data-stu-id="33853-145">Actor events</span></span>](service-fabric-reliable-actors-events.md)
* [<span data-ttu-id="33853-146">Aktör yeniden giriş</span><span class="sxs-lookup"><span data-stu-id="33853-146">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
