---
title: "Aktör tabanlı Azure mikro olayları | Microsoft Docs"
description: "Service Fabric Reliable Actors olayları için giriş."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: aa01b0f7-8f88-403a-bfe1-5aba00312c24
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: amanbha
ms.openlocfilehash: d936670c548ff709fc2e935d3f28d94e4bde8a04
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="actor-events"></a><span data-ttu-id="74f56-103">Aktör olayları</span><span class="sxs-lookup"><span data-stu-id="74f56-103">Actor events</span></span>
<span data-ttu-id="74f56-104">Aktör olayları en yüksek çaba bildirim oyuncusu istemcilere göndermek için bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="74f56-104">Actor events provide a way to send best-effort notifications from the actor to the clients.</span></span> <span data-ttu-id="74f56-105">Aktör olayları aktör istemci iletişimi için tasarlanmıştır ve aktör aktör iletişimi için kullanılmaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="74f56-105">Actor events are designed for actor-to-client communication and should not be used for actor-to-actor communication.</span></span>

<span data-ttu-id="74f56-106">Aşağıdaki kod parçacıkları, uygulamanızda aktör olayları kullanmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="74f56-106">The following code snippets show how to use actor events in your application.</span></span>

<span data-ttu-id="74f56-107">Aktör tarafından yayımlanan olayları tanımlayan bir arabirim tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="74f56-107">Define an interface that describes the events published by the actor.</span></span> <span data-ttu-id="74f56-108">Bu arabirim öğesinden türetilmelidir `IActorEvents` arabirimi.</span><span class="sxs-lookup"><span data-stu-id="74f56-108">This interface must be derived from the `IActorEvents` interface.</span></span> <span data-ttu-id="74f56-109">Bağımsız değişkenler yöntemlerin olmalıdır [veri sözleşmesi seri hale getirilebilir](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="74f56-109">The arguments of the methods must be [data contract serializable](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span> <span data-ttu-id="74f56-110">Yöntemleri boş döndürmeleri gerektiği, bir yolu ve en iyi çaba bildirimleri olayı olarak olur.</span><span class="sxs-lookup"><span data-stu-id="74f56-110">The methods must return void, as event notifications are one way and best effort.</span></span>

```csharp
public interface IGameEvents : IActorEvents
{
    void GameScoreUpdated(Guid gameId, string currentScore);
}
```
```Java
public interface GameEvents implements ActorEvents
{
    void gameScoreUpdated(UUID gameId, String currentScore);
}
```
<span data-ttu-id="74f56-111">Aktör arabiriminde aktör tarafından yayımlanan olayları bildirme.</span><span class="sxs-lookup"><span data-stu-id="74f56-111">Declare the events published by the actor in the actor interface.</span></span>

```csharp
public interface IGameActor : IActor, IActorEventPublisher<IGameEvents>
{
    Task UpdateGameStatus(GameStatus status);

    Task<string> GetGameScore();
}
```
```Java
public interface GameActor extends Actor, ActorEventPublisherE<GameEvents>
{
    CompletableFuture<?> updateGameStatus(GameStatus status);

    CompletableFuture<String> getGameScore();
}
```
<span data-ttu-id="74f56-112">İstemci tarafında olay işleyicisi uygulayın.</span><span class="sxs-lookup"><span data-stu-id="74f56-112">On the client side, implement the event handler.</span></span>

```csharp
class GameEventsHandler : IGameEvents
{
    public void GameScoreUpdated(Guid gameId, string currentScore)
    {
        Console.WriteLine(@"Updates: Game: {0}, Score: {1}", gameId, currentScore);
    }
}
```

```Java
class GameEventsHandler implements GameEvents {
    public void gameScoreUpdated(UUID gameId, String currentScore)
    {
        System.out.println("Updates: Game: "+gameId+" ,Score: "+currentScore);
    }
}
```

<span data-ttu-id="74f56-113">İstemci üzerindeki olay yayımlar aktör proxy'sine oluşturun ve kendi olaylarına abone olma.</span><span class="sxs-lookup"><span data-stu-id="74f56-113">On the client, create a proxy to the actor that publishes the event and subscribe to its events.</span></span>

```csharp
var proxy = ActorProxy.Create<IGameActor>(
                    new ActorId(Guid.Parse(arg)), ApplicationName);

await proxy.SubscribeAsync<IGameEvents>(new GameEventsHandler());
```

```Java
GameActor actorProxy = ActorProxyBase.create<GameActor>(GameActor.class, new ActorId(UUID.fromString(args)));

return ActorProxyEventUtility.subscribeAsync(actorProxy, new GameEventsHandler());
```

<span data-ttu-id="74f56-114">Yük devretme durumunda aktör üzerinden farklı işlem ya da düğüm başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="74f56-114">In the event of failovers, the actor may fail over to a different process or node.</span></span> <span data-ttu-id="74f56-115">Aktör proxy etkin abonelikleri yönetir ve otomatik olarak yeniden abone.</span><span class="sxs-lookup"><span data-stu-id="74f56-115">The actor proxy manages the active subscriptions and automatically re-subscribes them.</span></span> <span data-ttu-id="74f56-116">Aracılığıyla yeniden abonelik aralığı kontrol edebilirsiniz `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API.</span><span class="sxs-lookup"><span data-stu-id="74f56-116">You can control the re-subscription interval through the `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API.</span></span> <span data-ttu-id="74f56-117">Aboneliğinizi iptal etmek için kullanmak `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.</span><span class="sxs-lookup"><span data-stu-id="74f56-117">To unsubscribe, use the `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.</span></span>

<span data-ttu-id="74f56-118">Sırada aktör üzerinde olayları yalnızca yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="74f56-118">On the actor, simply publish the events as they happen.</span></span> <span data-ttu-id="74f56-119">Aktör çalışma zamanı olay abonelere varsa, bunları bildirim gönderir.</span><span class="sxs-lookup"><span data-stu-id="74f56-119">If there are subscribers to the event, the Actors runtime will send them the notification.</span></span>

```csharp
var ev = GetEvent<IGameEvents>();
ev.GameScoreUpdated(Id.GetGuidId(), score);
```
```Java
GameEvents event = getEvent<GameEvents>(GameEvents.class);
event.gameScoreUpdated(Id.getUUIDId(), score);
```


## <a name="next-steps"></a><span data-ttu-id="74f56-120">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="74f56-120">Next steps</span></span>
* [<span data-ttu-id="74f56-121">Aktör yeniden giriş</span><span class="sxs-lookup"><span data-stu-id="74f56-121">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="74f56-122">Aktör tanılama ve performans izleme</span><span class="sxs-lookup"><span data-stu-id="74f56-122">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="74f56-123">Aktör API başvuru belgeleri</span><span class="sxs-lookup"><span data-stu-id="74f56-123">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="74f56-124">C# örnek kod</span><span class="sxs-lookup"><span data-stu-id="74f56-124">C# Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="74f56-125">C# .NET Core örnek kod</span><span class="sxs-lookup"><span data-stu-id="74f56-125">C# .NET Core Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started)
* [<span data-ttu-id="74f56-126">Java örnek kod</span><span class="sxs-lookup"><span data-stu-id="74f56-126">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)
