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
# <a name="reliable-actors-reentrancy"></a>Güvenilir aktörler yeniden giriş
Merhaba Reliable Actors çalışma zamanı, varsayılan olarak, mantıksal çağrısı Bağlam tabanlı yeniden giriş sağlar. Hello olmaları durumunda aktörler toobe yeniden girme için böylece aynı çağrı bağlam zinciri. Örneğin, ileti tooActor C. gönderen bir ileti tooActor B, A aktör gönderir Aktör C aktör A çağırırsa izin verecek şekilde hello ileti işleme bir parçası olarak hello desteklemeyeceğini, iletisidir. İşlem tamamlanana kadar farklı çağrı içeriği parçası olan diğer tüm iletileri aktör A engellenir.

İki seçenek hello tanımlanan aktör yeniden giriş için kullanılabilir `ActorReentrancyMode` enum:

* `LogicalCallContext`(varsayılan davranış)
* `Disallowed`-yeniden giriş devre dışı bırakır

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
Yeniden giriş yapılandırılabilir bir `ActorService`'s kayıt sırasında ayarları. Merhaba ayar hello aktör hizmetinde oluşturulan tooall aktör örnekleri uygulanır.

Merhaba aşağıdaki örnekte gösterilir hello yeniden giriş modu çok ayarlar bir aktör hizmeti`ActorReentrancyMode.Disallowed`. Bu durumda, bir aktör desteklemeyeceğini ileti tooanother aktör, türünde bir özel durum gönderirse `FabricException` oluşturulur.

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


## <a name="next-steps"></a>Sonraki adımlar
* Merhaba yeniden girişi hakkında daha fazla bilgi [aktör API başvuru belgeleri](https://msdn.microsoft.com/library/azure/dn971626.aspx)
