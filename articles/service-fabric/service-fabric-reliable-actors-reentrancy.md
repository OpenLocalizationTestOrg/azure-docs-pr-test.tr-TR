---
title: "Aktör tabanlı Azure mikro yeniden girişi | Microsoft Docs"
description: "Service Fabric Reliable Actors yeniden giriş için giriş"
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: amanbha
ms.assetid: be23464a-0eea-4eca-ae5a-2e1b650d365e
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 00fcccb379bf1ba3875fbaba57a05b00fa228622
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="reliable-actors-reentrancy"></a><span data-ttu-id="c5864-103">Güvenilir aktörler yeniden giriş</span><span class="sxs-lookup"><span data-stu-id="c5864-103">Reliable Actors reentrancy</span></span>
<span data-ttu-id="c5864-104">Reliable Actors çalışma zamanı varsayılan olarak, mantıksal çağrısı Bağlam tabanlı yeniden giriş sağlar.</span><span class="sxs-lookup"><span data-stu-id="c5864-104">The Reliable Actors runtime, by default, allows logical call context-based reentrancy.</span></span> <span data-ttu-id="c5864-105">Bu aynı çağrı bağlam zincirinde olmaları durumunda desteklemeyeceğini olmasını aktörler sağlar.</span><span class="sxs-lookup"><span data-stu-id="c5864-105">This allows for actors to be reentrant if they are in the same call context chain.</span></span> <span data-ttu-id="c5864-106">Örneğin, A aktör aktör C'ye ileti gönderen aktör B'ye ileti gönderir Aktör C aktör A çağırırsa izin verecek şekilde ileti işleme bir parçası olarak desteklemeyeceğini, iletisidir.</span><span class="sxs-lookup"><span data-stu-id="c5864-106">For example, Actor A sends a message to Actor B, who sends a message to Actor C. As part of the message processing, if Actor C calls Actor A, the message is reentrant, so it will be allowed.</span></span> <span data-ttu-id="c5864-107">İşlem tamamlanana kadar farklı çağrı içeriği parçası olan diğer tüm iletileri aktör A engellenir.</span><span class="sxs-lookup"><span data-stu-id="c5864-107">Any other messages that are part of a different call context will be blocked on Actor A until it finishes processing.</span></span>

<span data-ttu-id="c5864-108">İki seçenek tanımlanan aktör yeniden giriş için kullanılabilir `ActorReentrancyMode` enum:</span><span class="sxs-lookup"><span data-stu-id="c5864-108">There are two options available for actor reentrancy defined in the `ActorReentrancyMode` enum:</span></span>

* <span data-ttu-id="c5864-109">`LogicalCallContext`(varsayılan davranış)</span><span class="sxs-lookup"><span data-stu-id="c5864-109">`LogicalCallContext` (default behavior)</span></span>
* <span data-ttu-id="c5864-110">`Disallowed`-yeniden giriş devre dışı bırakır</span><span class="sxs-lookup"><span data-stu-id="c5864-110">`Disallowed` - disables reentrancy</span></span>

```csharp
public enum ActorReentrancyMode
{
    LogicalCallContext = 1,
    Disallowed = 2
}
```
```Java
public enum ActorReentrancyMode
{
    LogicalCallContext(1),
    Disallowed(2)
}
```
<span data-ttu-id="c5864-111">Yeniden giriş yapılandırılabilir bir `ActorService`'s kayıt sırasında ayarları.</span><span class="sxs-lookup"><span data-stu-id="c5864-111">Reentrancy can be configured in an `ActorService`'s settings during registration.</span></span> <span data-ttu-id="c5864-112">Aktör hizmeti oluşturulan tüm aktör örnekleri ayar uygulanır.</span><span class="sxs-lookup"><span data-stu-id="c5864-112">The setting applies to all actor instances created in the actor service.</span></span>

<span data-ttu-id="c5864-113">Aşağıdaki örnek, yeniden giriş modunu ayarlar için bir aktör hizmeti gösterir `ActorReentrancyMode.Disallowed`.</span><span class="sxs-lookup"><span data-stu-id="c5864-113">The following example shows an actor service that sets the reentrancy mode to `ActorReentrancyMode.Disallowed`.</span></span> <span data-ttu-id="c5864-114">Bu durumda, bir aktör başka bir aktör, türünde bir özel durum desteklemeyeceğini iletisi gönderirse `FabricException` oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="c5864-114">In this case, if an actor sends a reentrant message to another actor, an exception of type `FabricException` will be thrown.</span></span>

```csharp
static class Program
{
    static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<Actor1>(
                (context, actorType) => new ActorService(
                    context,
                    actorType, () => new Actor1(),
                    settings: new ActorServiceSettings()
                    {
                        ActorConcurrencySettings = new ActorConcurrencySettings()
                        {
                            ReentrancyMode = ActorReentrancyMode.Disallowed
                        }
                    }))
                .GetAwaiter().GetResult();

            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ActorEventSource.Current.ActorHostInitializationFailed(e.ToString());
            throw;
        }
    }
}
```
```Java
static class Program
{
    static void Main()
    {
        try
        {
            ActorConcurrencySettings actorConcurrencySettings = new ActorConcurrencySettings();
            actorConcurrencySettings.setReentrancyMode(ActorReentrancyMode.Disallowed);

            ActorServiceSettings actorServiceSettings = new ActorServiceSettings();
            actorServiceSettings.setActorConcurrencySettings(actorConcurrencySettings);

            ActorRuntime.registerActorAsync(
                Actor1.getClass(),
                (context, actorType) -> new FabricActorService(
                    context,
                    actorType, () -> new Actor1(),
                    null,
                    stateProvider,
                    actorServiceSettings, timeout);

            Thread.sleep(Long.MAX_VALUE);
        }
        catch (Exception e)
        {
            throw e;
        }
    }
}
```


## <a name="next-steps"></a><span data-ttu-id="c5864-115">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c5864-115">Next steps</span></span>
* <span data-ttu-id="c5864-116">Yeniden girişi hakkında daha fazla bilgi [aktör API başvuru belgeleri](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span><span class="sxs-lookup"><span data-stu-id="c5864-116">Learn more about reentrancy in the [Actor API reference documentation](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span></span>
