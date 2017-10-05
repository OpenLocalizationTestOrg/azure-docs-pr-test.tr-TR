---
title: "Çok biçimlilik Reliable Actors Framework'te | Microsoft Docs"
description: "Hiyerarşileri .NET arabirimleri ve Reliable Actors framework türlerinde işlevselliği ve API tanımlarını yeniden oluşturun."
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
ms.openlocfilehash: 36a59a41b2261369a2062c76ef90aebf7e24a221
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="polymorphism-in-the-reliable-actors-framework"></a><span data-ttu-id="00ca1-103">Çok biçimlilik Reliable Actors Framework'te</span><span class="sxs-lookup"><span data-stu-id="00ca1-103">Polymorphism in the Reliable Actors framework</span></span>
<span data-ttu-id="00ca1-104">Reliable Actors framework birçok nesne yönelimli tasarımında kullanacağınız aynı teknikleri kullanarak aktörler oluşturmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="00ca1-104">The Reliable Actors framework allows you to build actors using many of the same techniques that you would use in object-oriented design.</span></span> <span data-ttu-id="00ca1-105">Bu teknikler biri türlerine izin verir ve'dan daha fazla devralmak için arabirimleri çok biçimlilik üst genelleştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="00ca1-105">One of those techniques is polymorphism, which allows types and interfaces to inherit from more generalized parents.</span></span> <span data-ttu-id="00ca1-106">Reliable Actors Framework'te devralma genellikle birkaç ek kısıtlamalar .NET modeliyle izler.</span><span class="sxs-lookup"><span data-stu-id="00ca1-106">Inheritance in the Reliable Actors framework generally follows the .NET model with a few additional constraints.</span></span> <span data-ttu-id="00ca1-107">Java/Linux durumunda, Java modelini izler.</span><span class="sxs-lookup"><span data-stu-id="00ca1-107">In case of Java/Linux, it follows the Java model.</span></span>

## <a name="interfaces"></a><span data-ttu-id="00ca1-108">Arabirimleri</span><span class="sxs-lookup"><span data-stu-id="00ca1-108">Interfaces</span></span>
<span data-ttu-id="00ca1-109">Reliable Actors framework aktör türüne göre uygulanacak en az bir arabirim tanımlamanızı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="00ca1-109">The Reliable Actors framework requires you to define at least one interface to be implemented by your actor type.</span></span> <span data-ttu-id="00ca1-110">Bu arabirim, istemciler tarafından aktörler ile iletişim kurmak için kullanılan bir proxy sınıfı oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="00ca1-110">This interface is used to generate a proxy class that can be used by clients to communicate with your actors.</span></span> <span data-ttu-id="00ca1-111">Aktör türü tarafından uygulanan her arabirimi ve tüm üst öğelerinden sonuçta türetilen sürece IActor(C#) veya Actor(Java) arabirimleri diğer arabirimlerinden devralabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00ca1-111">Interfaces can inherit from other interfaces as long as every interface that is implemented by an actor type and all of its parents ultimately derive from IActor(C#) or Actor(Java) .</span></span> <span data-ttu-id="00ca1-112">IActor(C#) ve Actor(Java) platform tarafından tanımlanan temel .NET ve Java çerçeveleri aktörler için sırasıyla arabirimlerdir.</span><span class="sxs-lookup"><span data-stu-id="00ca1-112">IActor(C#) and Actor(Java) are the platform-defined base interfaces for actors in the frameworks .NET and Java respectively.</span></span> <span data-ttu-id="00ca1-113">Bu nedenle, şekilleri kullanarak Klasik çok biçimlilik örnek şuna benzeyebilir:</span><span class="sxs-lookup"><span data-stu-id="00ca1-113">Thus, the classic polymorphism example using shapes might look something like this:</span></span>

![Hiyerarşi şekli aktörler için arabirim][shapes-interface-hierarchy]

## <a name="types"></a><span data-ttu-id="00ca1-115">Türler</span><span class="sxs-lookup"><span data-stu-id="00ca1-115">Types</span></span>
<span data-ttu-id="00ca1-116">Ayrıca, platform tarafından sağlanan temel aktör sınıfından türetilen aktör türlerinin hiyerarşisi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00ca1-116">You can also create a hierarchy of actor types, which are derived from the base Actor class that is provided by the platform.</span></span> <span data-ttu-id="00ca1-117">Şekiller söz konusu olduğunda, bir taban olabilir `Shape`(C#) veya `ShapeImpl`(Java) türü:</span><span class="sxs-lookup"><span data-stu-id="00ca1-117">In the case of shapes, you might have a base `Shape`(C#) or `ShapeImpl`(Java) type:</span></span>

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

<span data-ttu-id="00ca1-118">Subtypes `Shape`(C#) veya `ShapeImpl`(Java) taban yöntemleri geçersiz kılın.</span><span class="sxs-lookup"><span data-stu-id="00ca1-118">Subtypes of `Shape`(C#) or `ShapeImpl`(Java) can override methods from the base.</span></span>

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

<span data-ttu-id="00ca1-119">Not `ActorService` aktör türündeki özniteliği.</span><span class="sxs-lookup"><span data-stu-id="00ca1-119">Note the `ActorService` attribute on the actor type.</span></span> <span data-ttu-id="00ca1-120">Bu öznitelik güvenilir aktör framework aktörler bu tür barındırmak için bir hizmet otomatik olarak oluşturmasını söyler.</span><span class="sxs-lookup"><span data-stu-id="00ca1-120">This attribute tells the Reliable Actor framework that it should automatically create a service for hosting actors of this type.</span></span> <span data-ttu-id="00ca1-121">Bazı durumlarda, yalnızca işlevselliği alt türleri ile paylaşmak için tasarlanmıştır ve hiçbir zaman somut aktörler örneği oluşturmak için kullanılacak bir taban türü oluşturmak isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="00ca1-121">In some cases, you may wish to create a base type that is solely intended for sharing functionality with subtypes and will never be used to instantiate concrete actors.</span></span> <span data-ttu-id="00ca1-122">Bu durumda, kullanmanız gereken `abstract` hiçbir zaman bu türüne göre bir aktör oluşturacak göstermek için anahtar sözcüğü.</span><span class="sxs-lookup"><span data-stu-id="00ca1-122">In those cases, you should use the `abstract` keyword to indicate that you will never create an actor based on that type.</span></span>

## <a name="next-steps"></a><span data-ttu-id="00ca1-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="00ca1-123">Next steps</span></span>
* <span data-ttu-id="00ca1-124">Bkz: [nasıl Reliable Actors framework Service Fabric platformundan yararlanır](service-fabric-reliable-actors-platform.md) güvenilirlik, ölçeklenebilirlik ve tutarlı bir duruma sağlamak için.</span><span class="sxs-lookup"><span data-stu-id="00ca1-124">See [how the Reliable Actors framework leverages the Service Fabric platform](service-fabric-reliable-actors-platform.md) to provide reliability, scalability, and consistent state.</span></span>
* <span data-ttu-id="00ca1-125">Hakkında bilgi edinin [aktör yaşam döngüsü](service-fabric-reliable-actors-lifecycle.md).</span><span class="sxs-lookup"><span data-stu-id="00ca1-125">Learn about the [actor lifecycle](service-fabric-reliable-actors-lifecycle.md).</span></span>

<!-- Image references -->

[shapes-interface-hierarchy]: ./media/service-fabric-reliable-actors-polymorphism/Shapes-Interface-Hierarchy.png
