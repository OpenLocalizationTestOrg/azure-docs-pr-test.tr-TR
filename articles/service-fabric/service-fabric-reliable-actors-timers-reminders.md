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
# <a name="actor-timers-and-reminders"></a>Aktör zamanlayıcılar ve anımsatıcıları
Aktör zamanlayıcılar veya anımsatıcıları kaydederek kendilerini düzenli çalışma zamanlayabilirsiniz. Bu makalede gösterilmektedir nasıl toouse zamanlayıcılar ve anımsatıcıları ve aralarındaki hello farkları açıklamaktadır.

## <a name="actor-timers"></a>Aktör zamanlayıcılar
Aktör zamanlayıcılar hello geri arama yöntemleri çalışma zamanı sağlar aktörler hello hello Aç tabanlı eşzamanlılık garanti saygı .NET veya Java Zamanlayıcı tooensure çevresinde basit bir sarmalayıcı sağlar.

Aktör hello kullanabilir `RegisterTimer`(C#) veya `registerTimer`(Java) ve `UnregisterTimer`(C#) veya `unregisterTimer`kendi tabanında (Java) yöntemleri sınıfı tooregister ve bunların zamanlayıcılar kaldırılamadı. Aşağıdaki örnek Hello süreölçer API'lerini hello kullanımını göstermektedir. Merhaba API'leri: çok benzer toohello .NET Zamanlayıcı veya Java Zamanlayıcı. Merhaba Zamanlayıcı zamanı geldiğinde bu örnekte, hello hello aktörler çalışma zamanı arama `MoveObject`(C#) veya `moveObject`(Java) yöntemi. Merhaba yöntemi toorespect hello Aç tabanlı eşzamanlılık garanti edilmez. Bu yürütme bu geri çağırma işlemi tamamlanana kadar başka bir aktör yöntemin veya Zamanlayıcı/anımsatıcı geri aramalar ediyor olacağı anlamına gelir.

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

yürütme Hello geri çağırma tamamlandıktan sonra hello sonraki süreyi hello süreölçer başlatır. Bu, hello geri arama yürütüyor ve hello geri araması bitirdiğinde kullanmaya çalışırken bu hello Zamanlayıcı durdurulduğunda anlamına gelir.

Merhaba aktörler çalışma zamanı hello geri araması bitirdiğinde toohello aktör'ın durum Yöneticisi yapılan değişiklikleri kaydeder. Merhaba durum kaydetme işleminde bir hata meydana gelirse, söz konusu aktör nesne devre dışı bırakılır ve yeni bir örneğini etkinleştirilir.

Çöp toplama bir parçası olarak Hello aktör devre dışı bırakıldığında tüm zamanlayıcılar durdurulur. Bir zamanlayıcı geri aramalar bundan sonra çağrılır. Ayrıca, hello aktörler çalışma zamanı devre dışı bırakma önce çalışmakta olan hello zamanlayıcılar hakkında hiçbir bilgi sürdürmez. Bu toohello aktör tooregister hello gelecekteki etkinleştirildiğinde, gereken tüm zamanlayıcılar olur. Daha fazla bilgi için üzerinde hello bölümüne bakın. [aktör çöp toplama](service-fabric-reliable-actors-lifecycle.md).

## <a name="actor-reminders"></a>Aktör anımsatıcıları
Anımsatıcıları olan bir mekanizma tootrigger bir aktör üzerinde kalıcı geri aramalar kez belirtildi. İşlevlerine benzer tootimers ' dir. Ancak zamanlayıcılar anımsatıcıları tüm koşullar altında hello aktör açıkça bunları kaydını siler veya hello aktör açıkça silinene kadar tetiklenir. Özellikle, Hello aktörler çalışma zamanı hello aktör'ın anımsatıcıları hakkında bilgi devam ederse çünkü anımsatıcıları aktör deactivations ve yük devretme işlemlerini arasında tetiklenir.

tooregister anımsatıcısı, bir aktör çağırır hello `RegisterReminderAsync` hello aşağıdaki örnekte gösterildiği gibi hello temel sınıf üzerinde sağlanan yöntemi:

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

Bu örnekte, `"Pay cell phone bill"` hello anımsatıcı adıdır. Aktör kullanır hello bir dize budur toouniquely anımsatıcısı tanımlayın. `BitConverter.GetBytes(amountInDollars)`(C#) hello anımsatıcı'yla ilişkili hello bağlamdır. Bu geri toohello Aktör bir bağımsız değişken toohello anımsatıcı geri çağırma, yani geçirilir `IRemindable.ReceiveReminderAsync`(C#) veya `Remindable.receiveReminderAsync`(Java).

Anımsatıcıları kullanmak aktörler hello uygulanmalı `IRemindable` hello aşağıdaki örnekte gösterildiği gibi arabirim.

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

Bir anımsatıcı tetiklendiğinde hello Reliable Actors çalışma zamanı hello çağıracağı `ReceiveReminderAsync`(C#) veya `receiveReminderAsync`hello aktör yöntemi (Java). Bir aktör birden çok anımsatıcıları kaydetmek ve hello `ReceiveReminderAsync`(C#) veya `receiveReminderAsync`(Java) yöntem çağrıldığında bu anımsatıcılar birini ne zaman tetiklenir. Merhaba aktör toohello içinde geçirilen hello anımsatıcı adı kullanabilir `ReceiveReminderAsync`(C#) veya `receiveReminderAsync`(Java) yöntemi toofigure hangi anımsatıcı tetiklendi.

Merhaba aktörler çalışma zamanı kaydeder hello aktör'ın durumdayken hello `ReceiveReminderAsync`(C#) veya `receiveReminderAsync`(Java) çağrı tamamlanır. Merhaba durum kaydetme işleminde bir hata meydana gelirse, söz konusu aktör nesne devre dışı bırakılır ve yeni bir örneğini etkinleştirilir.

toounregister anımsatıcısı, bir aktör çağırır hello `UnregisterReminderAsync`(C#) veya `unregisterReminderAsync`(Java) yöntemini hello aşağıdaki örnekte gösterildiği gibi.

```csharp
IActorReminder reminder = GetReminder("Pay cell phone bill");
Task reminderUnregistration = UnregisterReminderAsync(reminder);
```
```Java
ActorReminder reminder = getReminder("Pay cell phone bill");
CompletableFuture reminderUnregistration = unregisterReminderAsync(reminder);
```

Yukarıda gösterildiği gibi hello `UnregisterReminderAsync`(C#) veya `unregisterReminderAsync`(Java) yöntemi kabul eden bir `IActorReminder`(C#) veya `ActorReminder`(Java) arabirimi. Merhaba aktör temel sınıf destekleyen bir `GetReminder`(C#) veya `getReminder`kullanılan tooretrieve hello olabilir (Java) yöntemi `IActorReminder`(C#) veya `ActorReminder`hello anımsatıcı adı geçirerek (Java) arabirimi. Merhaba aktör toopersist hello gereksinimi olmadığından bu uygundur `IActorReminder`(C#) veya `ActorReminder`hello döndürülen (Java) arabirimi `RegisterReminder`(C#) veya `registerReminder`(Java) yöntem çağrısı.

## <a name="next-steps"></a>Sonraki Adımlar
Güvenilir aktör olayları ve yeniden giriş hakkında bilgi edinin:
* [Aktör olayları](service-fabric-reliable-actors-events.md)
* [Aktör yeniden giriş](service-fabric-reliable-actors-reentrancy.md)
