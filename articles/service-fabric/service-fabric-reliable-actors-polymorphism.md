---
title: Merhaba Reliable Actors Framework'te aaaPolymorphism | Microsoft Docs
description: ".NET arabirimleri ve hello Reliable Actors framework tooreuse işlevselliği türlerinde ve API tanımlarını hiyerarşiler"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: vturecek
ms.assetid: ef0eeff6-32b7-410d-ac69-87cba8b8fd46
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ed9ec442595bd9a5e48c9af1f6aac003439b81f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="polymorphism-in-hello-reliable-actors-framework"></a>Çok biçimlilik hello Reliable Actors Framework'te
Merhaba Reliable Actors framework birçok kullanarak toobuild aktörler sağlar, nesne yönelimli tasarımında kullanacağınız aynı teknikleri hello. Bu teknikler biri türlerine izin verir ve fazla tooinherit arabirimleri çok biçimlilik üst genelleştirilmiş. Devralma hello Reliable Actors Framework'te genellikle birkaç ek kısıtlamalar hello .NET modeliyle izler. Java/Linux durumunda hello Java modelini izler.

## <a name="interfaces"></a>Arabirimleri
Merhaba Reliable Actors framework gerektirir, toodefine aktör türü tarafından uygulanan en az bir arabirim toobe. Kullanılan toogenerate, aktörler ile istemcileri toocommunicate tarafından kullanılan bir proxy sınıfı arabirimidir. Aktör türü tarafından uygulanan her arabirimi ve tüm üst öğelerinden sonuçta türetilen sürece IActor(C#) veya Actor(Java) arabirimleri diğer arabirimlerinden devralabilirsiniz. IActor(C#) ve Actor(Java) hello platform tarafından tanımlanan temel hello çerçeveleri .NET ve Java aktörler için sırasıyla arabirimlerdir. Bu nedenle, şekilleri kullanarak hello Klasik çok biçimlilik örnek şuna benzeyebilir:

![Hiyerarşi şekli aktörler için arabirim][shapes-interface-hierarchy]

## <a name="types"></a>Türler
Bir hiyerarşi hello platform tarafından sağlanan hello temel aktör sınıfından türetilen aktör türlerinin de oluşturabilirsiniz. Temel şekillerin Hello durumda olabilir `Shape`(C#) veya `ShapeImpl`(Java) türü:

```csharp
public abstract class Shape : Actor, IShape
{
    public abstract Task<int> GetVerticeCount();

    public abstract Task<double> GetAreaAsync();
}
```
```Java
public abstract class ShapeImpl extends FabricActor implements Shape
{
    public abstract CompletableFuture<int> getVerticeCount();

    public abstract CompletableFuture<double> getAreaAsync();
}
```

Subtypes `Shape`(C#) veya `ShapeImpl`(Java) hello taban yöntemleri geçersiz kılın.

```csharp
[ActorService(Name = "Circle")]
[StatePersistence(StatePersistence.Persisted)]
public class Circle : Shape, ICircle
{
    public override Task<int> GetVerticeCount()
    {
        return Task.FromResult(0);
    }

    public override async Task<double> GetAreaAsync()
    {
        CircleState state = await this.StateManager.GetStateAsync<CircleState>("circle");

        return Math.PI *
            state.Radius *
            state.Radius;
    }
}
```
```Java
@ActorServiceAttribute(name = "Circle")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class Circle extends ShapeImpl implements Circle
{
    @Override
    public CompletableFuture<Integer> getVerticeCount()
    {
        return CompletableFuture.completedFuture(0);
    }

    @Override
    public CompletableFuture<Double> getAreaAsync()
    {
        return (this.stateManager().getStateAsync<CircleState>("circle").thenApply(state->{
          return Math.PI * state.radius * state.radius;
        }));
    }
}
```

Not hello `ActorService` hello aktör türündeki özniteliği. Bu öznitelik hello güvenilir aktör framework aktörler bu tür barındırmak için bir hizmet otomatik olarak oluşturmasını söyler. Bazı durumlarda, toocreate yalnızca işlevselliği alt türleri ile paylaşmak için amaçlanan bir taban türü isteyebilir ve kullanılan tooinstantiate somut aktörler hiçbir zaman olmaz. Bu gibi durumlarda hello kullanması gereken `abstract` hiçbir zaman bu türüne göre bir aktör oluşturacak anahtar sözcüğü tooindicate.

## <a name="next-steps"></a>Sonraki adımlar
* Bkz: [nasıl hello Reliable Actors framework hello Service Fabric platformundan yararlanır](service-fabric-reliable-actors-platform.md) tooprovide güvenilirlik, ölçeklenebilirlik ve tutarlı bir duruma.
* Merhaba hakkında bilgi edinin [aktör yaşam döngüsü](service-fabric-reliable-actors-lifecycle.md).

<!-- Image references -->

[shapes-interface-hierarchy]: ./media/service-fabric-reliable-actors-polymorphism/Shapes-Interface-Hierarchy.png
