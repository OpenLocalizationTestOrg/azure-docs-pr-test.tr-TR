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
# <a name="polymorphism-in-hello-reliable-actors-framework"></a><span data-ttu-id="ae13c-103">Çok biçimlilik hello Reliable Actors Framework'te</span><span class="sxs-lookup"><span data-stu-id="ae13c-103">Polymorphism in hello Reliable Actors framework</span></span>
<span data-ttu-id="ae13c-104">Merhaba Reliable Actors framework birçok kullanarak toobuild aktörler sağlar, nesne yönelimli tasarımında kullanacağınız aynı teknikleri hello.</span><span class="sxs-lookup"><span data-stu-id="ae13c-104">hello Reliable Actors framework allows you toobuild actors using many of hello same techniques that you would use in object-oriented design.</span></span> <span data-ttu-id="ae13c-105">Bu teknikler biri türlerine izin verir ve fazla tooinherit arabirimleri çok biçimlilik üst genelleştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="ae13c-105">One of those techniques is polymorphism, which allows types and interfaces tooinherit from more generalized parents.</span></span> <span data-ttu-id="ae13c-106">Devralma hello Reliable Actors Framework'te genellikle birkaç ek kısıtlamalar hello .NET modeliyle izler.</span><span class="sxs-lookup"><span data-stu-id="ae13c-106">Inheritance in hello Reliable Actors framework generally follows hello .NET model with a few additional constraints.</span></span> <span data-ttu-id="ae13c-107">Java/Linux durumunda hello Java modelini izler.</span><span class="sxs-lookup"><span data-stu-id="ae13c-107">In case of Java/Linux, it follows hello Java model.</span></span>

## <a name="interfaces"></a><span data-ttu-id="ae13c-108">Arabirimleri</span><span class="sxs-lookup"><span data-stu-id="ae13c-108">Interfaces</span></span>
<span data-ttu-id="ae13c-109">Merhaba Reliable Actors framework gerektirir, toodefine aktör türü tarafından uygulanan en az bir arabirim toobe.</span><span class="sxs-lookup"><span data-stu-id="ae13c-109">hello Reliable Actors framework requires you toodefine at least one interface toobe implemented by your actor type.</span></span> <span data-ttu-id="ae13c-110">Kullanılan toogenerate, aktörler ile istemcileri toocommunicate tarafından kullanılan bir proxy sınıfı arabirimidir.</span><span class="sxs-lookup"><span data-stu-id="ae13c-110">This interface is used toogenerate a proxy class that can be used by clients toocommunicate with your actors.</span></span> <span data-ttu-id="ae13c-111">Aktör türü tarafından uygulanan her arabirimi ve tüm üst öğelerinden sonuçta türetilen sürece IActor(C#) veya Actor(Java) arabirimleri diğer arabirimlerinden devralabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ae13c-111">Interfaces can inherit from other interfaces as long as every interface that is implemented by an actor type and all of its parents ultimately derive from IActor(C#) or Actor(Java) .</span></span> <span data-ttu-id="ae13c-112">IActor(C#) ve Actor(Java) hello platform tarafından tanımlanan temel hello çerçeveleri .NET ve Java aktörler için sırasıyla arabirimlerdir.</span><span class="sxs-lookup"><span data-stu-id="ae13c-112">IActor(C#) and Actor(Java) are hello platform-defined base interfaces for actors in hello frameworks .NET and Java respectively.</span></span> <span data-ttu-id="ae13c-113">Bu nedenle, şekilleri kullanarak hello Klasik çok biçimlilik örnek şuna benzeyebilir:</span><span class="sxs-lookup"><span data-stu-id="ae13c-113">Thus, hello classic polymorphism example using shapes might look something like this:</span></span>

![Hiyerarşi şekli aktörler için arabirim][shapes-interface-hierarchy]

## <a name="types"></a><span data-ttu-id="ae13c-115">Türler</span><span class="sxs-lookup"><span data-stu-id="ae13c-115">Types</span></span>
<span data-ttu-id="ae13c-116">Bir hiyerarşi hello platform tarafından sağlanan hello temel aktör sınıfından türetilen aktör türlerinin de oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ae13c-116">You can also create a hierarchy of actor types, which are derived from hello base Actor class that is provided by hello platform.</span></span> <span data-ttu-id="ae13c-117">Temel şekillerin Hello durumda olabilir `Shape`(C#) veya `ShapeImpl`(Java) türü:</span><span class="sxs-lookup"><span data-stu-id="ae13c-117">In hello case of shapes, you might have a base `Shape`(C#) or `ShapeImpl`(Java) type:</span></span>

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

<span data-ttu-id="ae13c-118">Subtypes `Shape`(C#) veya `ShapeImpl`(Java) hello taban yöntemleri geçersiz kılın.</span><span class="sxs-lookup"><span data-stu-id="ae13c-118">Subtypes of `Shape`(C#) or `ShapeImpl`(Java) can override methods from hello base.</span></span>

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

<span data-ttu-id="ae13c-119">Not hello `ActorService` hello aktör türündeki özniteliği.</span><span class="sxs-lookup"><span data-stu-id="ae13c-119">Note hello `ActorService` attribute on hello actor type.</span></span> <span data-ttu-id="ae13c-120">Bu öznitelik hello güvenilir aktör framework aktörler bu tür barındırmak için bir hizmet otomatik olarak oluşturmasını söyler.</span><span class="sxs-lookup"><span data-stu-id="ae13c-120">This attribute tells hello Reliable Actor framework that it should automatically create a service for hosting actors of this type.</span></span> <span data-ttu-id="ae13c-121">Bazı durumlarda, toocreate yalnızca işlevselliği alt türleri ile paylaşmak için amaçlanan bir taban türü isteyebilir ve kullanılan tooinstantiate somut aktörler hiçbir zaman olmaz.</span><span class="sxs-lookup"><span data-stu-id="ae13c-121">In some cases, you may wish toocreate a base type that is solely intended for sharing functionality with subtypes and will never be used tooinstantiate concrete actors.</span></span> <span data-ttu-id="ae13c-122">Bu gibi durumlarda hello kullanması gereken `abstract` hiçbir zaman bu türüne göre bir aktör oluşturacak anahtar sözcüğü tooindicate.</span><span class="sxs-lookup"><span data-stu-id="ae13c-122">In those cases, you should use hello `abstract` keyword tooindicate that you will never create an actor based on that type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae13c-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ae13c-123">Next steps</span></span>
* <span data-ttu-id="ae13c-124">Bkz: [nasıl hello Reliable Actors framework hello Service Fabric platformundan yararlanır](service-fabric-reliable-actors-platform.md) tooprovide güvenilirlik, ölçeklenebilirlik ve tutarlı bir duruma.</span><span class="sxs-lookup"><span data-stu-id="ae13c-124">See [how hello Reliable Actors framework leverages hello Service Fabric platform](service-fabric-reliable-actors-platform.md) tooprovide reliability, scalability, and consistent state.</span></span>
* <span data-ttu-id="ae13c-125">Merhaba hakkında bilgi edinin [aktör yaşam döngüsü](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="ae13c-125">Learn about hello [actor lifecycle](service-fabric-reliable-actors-lifecycle.md).</span></span>

<!-- Image references -->

[shapes-interface-hierarchy]: ./media/service-fabric-reliable-actors-polymorphism/Shapes-Interface-Hierarchy.png
