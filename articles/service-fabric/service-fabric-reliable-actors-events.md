---
title: "Aktör tabanlı Azure mikro aaaEvents | Microsoft Docs"
description: "Service Fabric Reliable Actors giriş tooevents."
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
ms.openlocfilehash: a51e41c35441a5fea508138968b36a35f0ba6699
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="actor-events"></a><span data-ttu-id="fff18-103">Aktör olayları</span><span class="sxs-lookup"><span data-stu-id="fff18-103">Actor events</span></span>
<span data-ttu-id="fff18-104">Aktör olayları bir şekilde toosend en yüksek çaba bildirimleri hello aktör toohello istemcilerden sağlar.</span><span class="sxs-lookup"><span data-stu-id="fff18-104">Actor events provide a way toosend best-effort notifications from hello actor toohello clients.</span></span> <span data-ttu-id="fff18-105">Aktör olayları aktör istemci iletişimi için tasarlanmıştır ve aktör aktör iletişimi için kullanılmaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="fff18-105">Actor events are designed for actor-to-client communication and should not be used for actor-to-actor communication.</span></span>

<span data-ttu-id="fff18-106">Merhaba aşağıdaki kod parçacıkları Göster nasıl toouse aktör olayları uygulamanızda.</span><span class="sxs-lookup"><span data-stu-id="fff18-106">hello following code snippets show how toouse actor events in your application.</span></span>

<span data-ttu-id="fff18-107">Merhaba aktör tarafından yayımlanan hello olayları tanımlayan bir arabirim tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="fff18-107">Define an interface that describes hello events published by hello actor.</span></span> <span data-ttu-id="fff18-108">Bu arabirim hello türetilmelidir `IActorEvents` arabirimi.</span><span class="sxs-lookup"><span data-stu-id="fff18-108">This interface must be derived from hello `IActorEvents` interface.</span></span> <span data-ttu-id="fff18-109">Merhaba yöntemleri Hello bağımsız olmalıdır [veri sözleşmesi seri hale getirilebilir](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span><span class="sxs-lookup"><span data-stu-id="fff18-109">hello arguments of hello methods must be [data contract serializable](service-fabric-reliable-actors-notes-on-actor-type-serialization.md).</span></span> <span data-ttu-id="fff18-110">Merhaba yöntemleri boş döndürmeleri gerektiği, bir yolu ve en iyi çaba bildirimleri olayı olarak olur.</span><span class="sxs-lookup"><span data-stu-id="fff18-110">hello methods must return void, as event notifications are one way and best effort.</span></span>

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
<span data-ttu-id="fff18-111">Merhaba aktör hello aktör arabiriminde tarafından yayımlanan hello olayları bildirme.</span><span class="sxs-lookup"><span data-stu-id="fff18-111">Declare hello events published by hello actor in hello actor interface.</span></span>

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
<span data-ttu-id="fff18-112">Merhaba istemci tarafında hello olay işleyicisi uygulayın.</span><span class="sxs-lookup"><span data-stu-id="fff18-112">On hello client side, implement hello event handler.</span></span>

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

<span data-ttu-id="fff18-113">Merhaba istemcide hello olay yayımlayan bir proxy toohello aktör oluşturun ve tooits olayları abone olun.</span><span class="sxs-lookup"><span data-stu-id="fff18-113">On hello client, create a proxy toohello actor that publishes hello event and subscribe tooits events.</span></span>

```csharp
var proxy = ActorProxy.Create<IGameActor>(
                    new ActorId(Guid.Parse(arg)), ApplicationName);

await proxy.SubscribeAsync<IGameEvents>(new GameEventsHandler());
```

```Java
GameActor actorProxy = ActorProxyBase.create<GameActor>(GameActor.class, new ActorId(UUID.fromString(args)));

return ActorProxyEventUtility.subscribeAsync(actorProxy, new GameEventsHandler());
```

<span data-ttu-id="fff18-114">Yük devretme işlemlerini Hello olayda hello aktör tooa farklı bir işlem veya düğüm üzerinde başarısız olabilir.</span><span class="sxs-lookup"><span data-stu-id="fff18-114">In hello event of failovers, hello actor may fail over tooa different process or node.</span></span> <span data-ttu-id="fff18-115">Merhaba aktör proxy hello etkin abonelikleri yönetir ve otomatik olarak yeniden abone.</span><span class="sxs-lookup"><span data-stu-id="fff18-115">hello actor proxy manages hello active subscriptions and automatically re-subscribes them.</span></span> <span data-ttu-id="fff18-116">Merhaba yeniden abonelik aralığı hello aracılığıyla kontrol edebilirsiniz `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API.</span><span class="sxs-lookup"><span data-stu-id="fff18-116">You can control hello re-subscription interval through hello `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API.</span></span> <span data-ttu-id="fff18-117">toounsubscribe, kullanım hello `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.</span><span class="sxs-lookup"><span data-stu-id="fff18-117">toounsubscribe, use hello `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.</span></span>

<span data-ttu-id="fff18-118">Bunlar gerçekleşecek şekilde hello aktör üzerinde hello olayları yalnızca yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="fff18-118">On hello actor, simply publish hello events as they happen.</span></span> <span data-ttu-id="fff18-119">Merhaba aktörler çalışma zamanı aboneleri toohello olay varsa, bunları hello bildirim gönderir.</span><span class="sxs-lookup"><span data-stu-id="fff18-119">If there are subscribers toohello event, hello Actors runtime will send them hello notification.</span></span>

```csharp
var ev = GetEvent<IGameEvents>();
ev.GameScoreUpdated(Id.GetGuidId(), score);
```
```Java
GameEvents event = getEvent<GameEvents>(GameEvents.class);
event.gameScoreUpdated(Id.getUUIDId(), score);
```


## <a name="next-steps"></a><span data-ttu-id="fff18-120">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fff18-120">Next steps</span></span>
* [<span data-ttu-id="fff18-121">Aktör yeniden giriş</span><span class="sxs-lookup"><span data-stu-id="fff18-121">Actor reentrancy</span></span>](service-fabric-reliable-actors-reentrancy.md)
* [<span data-ttu-id="fff18-122">Aktör tanılama ve performans izleme</span><span class="sxs-lookup"><span data-stu-id="fff18-122">Actor diagnostics and performance monitoring</span></span>](service-fabric-reliable-actors-diagnostics.md)
* [<span data-ttu-id="fff18-123">Aktör API başvuru belgeleri</span><span class="sxs-lookup"><span data-stu-id="fff18-123">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="fff18-124">C# örnek kod</span><span class="sxs-lookup"><span data-stu-id="fff18-124">C# Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [<span data-ttu-id="fff18-125">C# .NET Core örnek kod</span><span class="sxs-lookup"><span data-stu-id="fff18-125">C# .NET Core Sample code</span></span>](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started)
* [<span data-ttu-id="fff18-126">Java örnek kod</span><span class="sxs-lookup"><span data-stu-id="fff18-126">Java Sample code</span></span>](http://github.com/Azure-Samples/service-fabric-java-getting-started)
