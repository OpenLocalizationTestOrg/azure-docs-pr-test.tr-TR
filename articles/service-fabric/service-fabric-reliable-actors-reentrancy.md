---
title: "Aktör tabanlı Azure mikro aaaReentrancy | Microsoft Docs"
description: "Service Fabric güvenilir aktörler için giriş tooreentrancy"
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
ms.openlocfilehash: 61c69bcf0f100e075d19ba155954c05789b71761
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="reliable-actors-reentrancy"></a><span data-ttu-id="16ba7-103">Güvenilir aktörler yeniden giriş</span><span class="sxs-lookup"><span data-stu-id="16ba7-103">Reliable Actors reentrancy</span></span>
<span data-ttu-id="16ba7-104">Merhaba Reliable Actors çalışma zamanı, varsayılan olarak, mantıksal çağrısı Bağlam tabanlı yeniden giriş sağlar.</span><span class="sxs-lookup"><span data-stu-id="16ba7-104">hello Reliable Actors runtime, by default, allows logical call context-based reentrancy.</span></span> <span data-ttu-id="16ba7-105">Hello olmaları durumunda aktörler toobe yeniden girme için böylece aynı çağrı bağlam zinciri.</span><span class="sxs-lookup"><span data-stu-id="16ba7-105">This allows for actors toobe reentrant if they are in hello same call context chain.</span></span> <span data-ttu-id="16ba7-106">Örneğin, ileti tooActor C. gönderen bir ileti tooActor B, A aktör gönderir Aktör C aktör A çağırırsa izin verecek şekilde hello ileti işleme bir parçası olarak hello desteklemeyeceğini, iletisidir.</span><span class="sxs-lookup"><span data-stu-id="16ba7-106">For example, Actor A sends a message tooActor B, who sends a message tooActor C. As part of hello message processing, if Actor C calls Actor A, hello message is reentrant, so it will be allowed.</span></span> <span data-ttu-id="16ba7-107">İşlem tamamlanana kadar farklı çağrı içeriği parçası olan diğer tüm iletileri aktör A engellenir.</span><span class="sxs-lookup"><span data-stu-id="16ba7-107">Any other messages that are part of a different call context will be blocked on Actor A until it finishes processing.</span></span>

<span data-ttu-id="16ba7-108">İki seçenek hello tanımlanan aktör yeniden giriş için kullanılabilir `ActorReentrancyMode` enum:</span><span class="sxs-lookup"><span data-stu-id="16ba7-108">There are two options available for actor reentrancy defined in hello `ActorReentrancyMode` enum:</span></span>

* <span data-ttu-id="16ba7-109">`LogicalCallContext`(varsayılan davranış)</span><span class="sxs-lookup"><span data-stu-id="16ba7-109">`LogicalCallContext` (default behavior)</span></span>
* <span data-ttu-id="16ba7-110">`Disallowed`-yeniden giriş devre dışı bırakır</span><span class="sxs-lookup"><span data-stu-id="16ba7-110">`Disallowed` - disables reentrancy</span></span>

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
<span data-ttu-id="16ba7-111">Yeniden giriş yapılandırılabilir bir `ActorService`'s kayıt sırasında ayarları.</span><span class="sxs-lookup"><span data-stu-id="16ba7-111">Reentrancy can be configured in an `ActorService`'s settings during registration.</span></span> <span data-ttu-id="16ba7-112">Merhaba ayar hello aktör hizmetinde oluşturulan tooall aktör örnekleri uygulanır.</span><span class="sxs-lookup"><span data-stu-id="16ba7-112">hello setting applies tooall actor instances created in hello actor service.</span></span>

<span data-ttu-id="16ba7-113">Merhaba aşağıdaki örnekte gösterilir hello yeniden giriş modu çok ayarlar bir aktör hizmeti`ActorReentrancyMode.Disallowed`.</span><span class="sxs-lookup"><span data-stu-id="16ba7-113">hello following example shows an actor service that sets hello reentrancy mode too`ActorReentrancyMode.Disallowed`.</span></span> <span data-ttu-id="16ba7-114">Bu durumda, bir aktör desteklemeyeceğini ileti tooanother aktör, türünde bir özel durum gönderirse `FabricException` oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="16ba7-114">In this case, if an actor sends a reentrant message tooanother actor, an exception of type `FabricException` will be thrown.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="16ba7-115">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="16ba7-115">Next steps</span></span>
* <span data-ttu-id="16ba7-116">Merhaba yeniden girişi hakkında daha fazla bilgi [aktör API başvuru belgeleri](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span><span class="sxs-lookup"><span data-stu-id="16ba7-116">Learn more about reentrancy in hello [Actor API reference documentation](https://msdn.microsoft.com/library/azure/dn971626.aspx)</span></span>
