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
# <a name="actor-lifecycle-automatic-garbage-collection-and-manual-delete"></a>Aktör yaşam döngüsü, otomatik çöp toplama ve el ile silme
Bir oyuncu etkinleştirilir hello ilk kez yöntemlerinden tooany bir çağrı yapılır. Bir oyuncu devre dışı bırakılmış (Çöp hello aktörler çalışma zamanı tarafından toplanan) ise yapılandırılabilir bir süre için kullanılmaz. Bir aktör ve durumu da el ile herhangi bir zamanda silinebilir.

## <a name="actor-activation"></a>Aktör etkinleştirme
Bir oyuncu etkinleştirildiğinde hello şunlar olur:

* Bir oyuncu için bir çağrı gelir ve bir etkin değilse, yeni aktör oluşturulur.
* Durum koruma hello aktör'ın durumunu yüklenir.
* Merhaba `OnActivateAsync` (C#) veya `onActivateAsync` (hangi hello aktör uygulamasında kılınabilir) (Java) yöntemi çağrılır.
* Merhaba aktör şimdi etkin olarak kabul edilir.

## <a name="actor-deactivation"></a>Aktör devre dışı bırakma
Bir oyuncu devre dışı bırakıldığında hello şunlar olur:

* Belirli bir süre için bir aktör kullanılmadığı zaman hello etkin aktörler tablosundan kaldırılır.
* Merhaba `OnDeactivateAsync` (C#) veya `onDeactivateAsync` (hangi hello aktör uygulamasında kılınabilir) (Java) yöntemi çağrılır. Merhaba aktör tüm hello zamanlayıcılarını temizler. Aktör işlemleri değişiklikler bu yönteminden çağrılmamalıdır durumu ister.

> [!TIP]
> Merhaba Fabric aktör çalışma zamanı bazı yayar [olayları ilgili tooactor etkinleştirme ve devre dışı bırakma](service-fabric-reliable-actors-diagnostics.md#list-of-events-and-performance-counters). Bunlar, tanılama ve performans izlemesi kullanışlıdır.
>
>

### <a name="actor-garbage-collection"></a>Aktör çöp toplama
Bir aktör devre dışı bırakıldığında başvuruları toohello aktör nesne yayımlandığında ve normal şekilde Merhaba ortak dil çalışma zamanı (CLR) veya java sanal makinesi (JVM) atık toplayıcı tarafından toplanacak olabilir. Çöp toplama yalnızca hello aktör nesnesini temizler; Mevcut **değil** hello aktör'ın durum Yöneticisi'nde depolanan durumunu kaldırın. Hello sonraki zaman hello aktör etkinleştirilir, yeni bir aktör nesnesi oluşturulur ve durumuna geri yüklenir.

"Hello amacı devre dışı bırakma ve atık toplama için kullanılan olarak" ne sayar?

* Çağrı Alma
* `IRemindable.ReceiveReminderAsync`(yalnızca hello aktör anımsatıcıları kullanıyorsa geçerlidir) çağrılan yöntemi

> [!NOTE]
> Merhaba aktör zamanlayıcılar kullanıyorsa ve Zamanlayıcı geri çağırma çağrılır, mevcut **değil** "kullanılan" olarak sayısı.
>
>

Biz devre dışı bırakma hello ayrıntılarını geçmeden önce önemli toodefine hello koşulları aşağıdaki gibidir:

* *Tarama aralığı*. Bu başlangıç aralığı aktörler hangi hello çalışma zamanı, etkin aktörler tablosunu devre dışı bırakılabilir aktörler için tarar ve atık toplanan. Bu Hello varsayılan değeri 1 dakikadır.
* *Boşta kalma zaman aşımı*. Bu hello bir aktör tooremain kullanılmayan gerektiğini zaman miktarıdır (boş) devre dışı bırakılabilir ve atık toplanan önce. Bunun için Hello varsayılan değer 60 dakikadır.

Genellikle, bu varsayılan toochange gerekmez. Ancak, gerekirse, bu aralıklar üzerinden değiştirilebilir `ActorServiceSettings` kaydederken, [aktör hizmeti](service-fabric-reliable-actors-platform.md):

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
Her etkin aktör hello aktör çalışma zamanı, (yani kullanılır) boşta zaman hello miktarını izler. Merhaba aktör çalışma zamanı denetler her hello aktörler her `ScanIntervalInSeconds` çöp olabiliyorsa toosee toplanır ve boşta olması durumunda topladığı `IdleTimeoutInSeconds`.

Bir oyuncu kullanılan zaman boşta kalma süresini sıfırlama too0 ' dir. Bundan sonra yalnızca onu yeniden boşta kalırsa toplanacak hello aktör olabilir `IdleTimeoutInSeconds`. Bir aktör toohave değerlendirilir geri çağırma edilmiş bir aktör arabirim yöntemini veya aktör anımsatıcı geri çağırma yürütülürse kullanılır. Bir aktör olan **değil** toohave olarak kabul edilen Zamanlayıcı geri çağırma çalıştırıldığında kullanılan.

Merhaba Aşağıdaki diyagramda tek aktör tooillustrate hello yaşam döngüsü Bu kavramlar gösterilmektedir.

![Boşta kalma süresi örneği][1]

Merhaba örnek hello etkisini aktör yöntem çağrıları, anımsatıcı ve zamanlayıcılar bu aktör hello ömrü gösterir. Başlangıç noktaları hello örnek hakkında aşağıdaki tümleştirilmediği şunlardır:

* ScanInterval ve IdleTimeout too5 ve 10 sırasıyla ayarlanır. (Bu konudaki Hedefimiz yalnızca tooillustrate hello kavram olduğundan birimleri burada önemli değildir.)
* Merhaba tarama teşkil eden kişilerin toobe çöp toplama T = 0, 5, 10, 15, 20, 25 ' hello tarama aralığı 5 tarafından tanımlandığı şekilde gerçekleşir.
* T = konumundaki 4, 8, 12, 16, 20, 24, düzenli bir süreölçeri başlatılır ve kendi geri çağırmayı yürütür. Boşta kalma süresi hello aktör hello etkilemez.
* T = 7 konumundaki bir aktör yöntemi çağrısı hello boşta kalma süresi too0 sıfırlar ve hello aktör hello çöp koleksiyonu geciktirir.
* T = 14 aktör anımsatıcı geri çağırmayı yürütür ve daha fazla gecikmeler hello aktör çöp koleksiyonu hello.
* Merhaba atık toplama taramada T = 25, sırasında hello aktör'ın boşta kalma süresi son 10 hello boşta kalma zaman aşımı aşıyor ve hello aktör toplanacak olan.

Bir oyuncu hiçbir zaman bu yöntemin yürütülmesi için ne kadar süre olsun yöntemlerinden birini yürütülürken toplanacak olmaz. Daha önce belirtildiği gibi hello yürütülmesini aktör arabirim yöntemleri ve anımsatıcı geri aramalar hello aktör'ın boşta kalma süresi too0 sıfırlayarak çöp toplama engeller. Zamanlayıcı geri aramalar Hello yürütülmesi hello boşta kalma süresi too0 sıfırlamaz. Ancak, hello aktör hello çöp koleksiyonu Hello Zamanlayıcı geri yürütme tamamlanana kadar ertelenir.

## <a name="deleting-actors-and-their-state"></a>Aktör ve durumlarına silme
Çöp toplama devre dışı bırakılan aktör yalnızca hello aktör nesnesini temizler, ancak bir aktör ait durum Yöneticisi'nde depolanan verileri kaldırmaz. Bir aktör yeniden etkinleştirildiğinde, verileri yeniden kullanılabilir tooit hello durum Yöneticisi aracılığıyla yapılır. Burada aktörler durum Yöneticisi'nde veri depolamak ve devre dışı ancak hiçbir zaman yeniden etkinleştirilmiş durumda, kendi verilerini gerekli tooclean olabilir.

Merhaba [aktör hizmeti](service-fabric-reliable-actors-platform.md) aktörler uzak çağrıyı yapandan silmek için bir işlev sağlar:

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

Bir oyuncu silme etkileri hello aktör şu anda etkin olan olup olmadığına bağlı olarak aşağıdaki hello sahiptir:

* **Etkin aktör**
  * Aktör etkin aktörler listesinden kaldırılır ve devre dışı bırakılır.
  * Durumu kalıcı olarak silinir.
* **Etkin olmayan aktör**
  * Durumu kalıcı olarak silinir.

Bir oyuncu çağrılamıyor Not Sil aktör yöntemlerinden birini kendisinden hangi hello çalışma zamanı hello aktör çağrısı tooenforce tek iş parçacıklı erişimine geçici bir kilidi elde bir aktör çağrısı bağlamı içinde yürütülürken hello aktör silinemez çünkü.

## <a name="next-steps"></a>Sonraki adımlar
* [Aktör zamanlayıcılar ve anımsatıcıları](service-fabric-reliable-actors-timers-reminders.md)
* [Aktör olayları](service-fabric-reliable-actors-events.md)
* [Aktör yeniden giriş](service-fabric-reliable-actors-reentrancy.md)
* [Aktör tanılama ve performans izleme](service-fabric-reliable-actors-diagnostics.md)
* [Aktör API başvuru belgeleri](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [C# örnek kod](https://github.com/Azure/servicefabric-samples)
* [Java örnek kod](http://github.com/Azure-Samples/service-fabric-java-getting-started)

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-lifecycle/garbage-collection.png
