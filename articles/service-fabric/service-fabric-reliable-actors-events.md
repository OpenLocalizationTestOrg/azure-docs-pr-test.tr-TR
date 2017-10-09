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
# <a name="actor-events"></a>Aktör olayları
Aktör olayları bir şekilde toosend en yüksek çaba bildirimleri hello aktör toohello istemcilerden sağlar. Aktör olayları aktör istemci iletişimi için tasarlanmıştır ve aktör aktör iletişimi için kullanılmaması gerekir.

Merhaba aşağıdaki kod parçacıkları Göster nasıl toouse aktör olayları uygulamanızda.

Merhaba aktör tarafından yayımlanan hello olayları tanımlayan bir arabirim tanımlayın. Bu arabirim hello türetilmelidir `IActorEvents` arabirimi. Merhaba yöntemleri Hello bağımsız olmalıdır [veri sözleşmesi seri hale getirilebilir](service-fabric-reliable-actors-notes-on-actor-type-serialization.md). Merhaba yöntemleri boş döndürmeleri gerektiği, bir yolu ve en iyi çaba bildirimleri olayı olarak olur.

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
Merhaba aktör hello aktör arabiriminde tarafından yayımlanan hello olayları bildirme.

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
Merhaba istemci tarafında hello olay işleyicisi uygulayın.

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

Merhaba istemcide hello olay yayımlayan bir proxy toohello aktör oluşturun ve tooits olayları abone olun.

```csharp
var proxy = ActorProxy.Create<IGameActor>(
                    new ActorId(Guid.Parse(arg)), ApplicationName);

await proxy.SubscribeAsync<IGameEvents>(new GameEventsHandler());
```

```Java
GameActor actorProxy = ActorProxyBase.create<GameActor>(GameActor.class, new ActorId(UUID.fromString(args)));

return ActorProxyEventUtility.subscribeAsync(actorProxy, new GameEventsHandler());
```

Yük devretme işlemlerini Hello olayda hello aktör tooa farklı bir işlem veya düğüm üzerinde başarısız olabilir. Merhaba aktör proxy hello etkin abonelikleri yönetir ve otomatik olarak yeniden abone. Merhaba yeniden abonelik aralığı hello aracılığıyla kontrol edebilirsiniz `ActorProxyEventExtensions.SubscribeAsync<TEvent>` API. toounsubscribe, kullanım hello `ActorProxyEventExtensions.UnsubscribeAsync<TEvent>` API.

Bunlar gerçekleşecek şekilde hello aktör üzerinde hello olayları yalnızca yayımlayın. Merhaba aktörler çalışma zamanı aboneleri toohello olay varsa, bunları hello bildirim gönderir.

```csharp
var ev = GetEvent<IGameEvents>();
ev.GameScoreUpdated(Id.GetGuidId(), score);
```
```Java
GameEvents event = getEvent<GameEvents>(GameEvents.class);
event.gameScoreUpdated(Id.getUUIDId(), score);
```


## <a name="next-steps"></a>Sonraki adımlar
* [Aktör yeniden giriş](service-fabric-reliable-actors-reentrancy.md)
* [Aktör tanılama ve performans izleme](service-fabric-reliable-actors-diagnostics.md)
* [Aktör API başvuru belgeleri](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [C# örnek kod](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [C# .NET Core örnek kod](https://github.com/Azure-Samples/service-fabric-dotnet-core-getting-started)
* [Java örnek kod](http://github.com/Azure-Samples/service-fabric-java-getting-started)
