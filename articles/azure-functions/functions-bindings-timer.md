---
title: "aaaAzure işlevleri Zamanlayıcı tetikleyicisi | Microsoft Docs"
description: "Toouse Zamanlayıcı Azure işlevlerinde nasıl tetikler anlayın."
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: "Azure işlevleri, İşlevler, olay işleme dinamik işlem sunucusuz mimarisi"
ms.assetid: d2f013d1-f458-42ae-baf8-1810138118ac
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/27/2017
ms.author: glenga
ms.custom: 
ms.openlocfilehash: 17fca22372dbc55d4684c8c099cc97923a7d3cf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-timer-trigger"></a>Azure işlevleri Zamanlayıcı tetikleyicisi

[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Bu makalede, Azure işlevlerinde nasıl tooconfigure ve kod Zamanlayıcı tetikler açıklanmaktadır. Azure işlevleri tanımlanmış bir zamanlamaya göre işlevi kodunuzu çalıştırmak olanak sağlayan zamanlayıcı tetikleyicisi bağlama sahiptir. 

çok örnekli genişleme Hello Zamanlayıcı tetikleyicisi destekler. Belirli Zamanlayıcı işlevi tek bir örneğini boyunca tüm örneklerde çalıştırılır.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a id="trigger"></a>

## <a name="timer-trigger"></a>Zamanlayıcı tetikleyicisi
Merhaba Zamanlayıcı tetikleyicisi tooa işlevini kullanıyor hello JSON nesnesinde aşağıdaki hello `bindings` function.json dizisi:

```json
{
    "schedule": "<CRON expression - see below>",
    "name": "<Name of trigger parameter in function signature>",
    "type": "timerTrigger",
    "direction": "in"
}
```

Merhaba değerini `schedule` olan bir [CRON ifade](http://en.wikipedia.org/wiki/Cron#CRON_expression) altı bu alanları içerir: 

    {second} {minute} {hour} {day} {month} {day-of-week}
&nbsp;
>[!NOTE]   
>Birçok çevrimiçi Bul hello cron ifadelerin hello atlayın `{second}` alan. Bunlardan birini kopyalarsanız, hello fazladan tooadjust gerek `{second}` alan. Belirli örnekler için bkz: [zamanlama örnekler](#examples) aşağıda.

Merhaba varsayılan saat dilimi hello CRON ifadelerle kullanılan Eşgüdümlü Evrensel Saat (UTC) alınır. CRON İfadenizde bağlı başka bir saat dilimini temel toohave adlı işlev uygulamanız için yeni bir uygulama ayarı oluşturmak `WEBSITE_TIME_ZONE`. Set hello değeri toohello hello adını istenen saat dilimi hello gösterildiği gibi [Microsoft saat dilimi dizin](https://msdn.microsoft.com/library/ms912391.aspx). 

Örneğin, *Doğu Standart Saati* olan UTC-05:00. toohave, Zamanlayıcı tetiklemek yangın 10:00 AM EST, her gün için UTC saat dilimi hesapları CRON ifade aşağıdaki kullanım hello adresindeki:

```json
"schedule": "0 0 15 * * *",
``` 

Alternatif olarak, adlı işlev uygulamanız için yeni bir uygulama ayarı ekleyebilirsiniz `WEBSITE_TIME_ZONE` ve hello değeri çok**Doğu Standart Saati**.  Ardından CRON ifade aşağıdaki hello 10:00 AM EST için kullanılabilir: 

```json
"schedule": "0 0 10 * * *",
``` 


<a name="examples"></a>

## <a name="schedule-examples"></a>Zamanlama örnekleri
CRON ifadeleri hello için kullanabileceğiniz bazı örnekleri şunlardır `schedule` özelliği. 

her beş dakikada tootrigger:

```json
"schedule": "0 */5 * * * *"
```

tootrigger kez üstündeki hello her saat:

```json
"schedule": "0 0 * * * *",
```

Her iki saatte tootrigger:

```json
"schedule": "0 0 */2 * * *",
```

tootrigger saatte 09: 00 too5 gelen PM:

```json
"schedule": "0 0 9-17 * * *",
```

tootrigger 9: 30'da her gün:

```json
"schedule": "0 30 9 * * *",
```

tootrigger 9: 30'da her hafta içi günü:

```json
"schedule": "0 30 9 * * 1-5",
```

<a name="usage"></a>

## <a name="trigger-usage"></a>Tetikleyici kullanımı
Bir zamanlayıcı tetikleyicisi işlevi çağrıldığında, hello [Zamanlayıcı nesne](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) hello işlevdeki geçirilir. Merhaba aşağıdaki JSON bir örnek hello Zamanlayıcı nesne gösterimidir. 

```json
{
    "Schedule":{
    },
    "ScheduleStatus": {
        "Last":"2016-10-04T10:15:00.012699+00:00",
        "Next":"2016-10-04T10:20:00+00:00"
    },
    "IsPastDue":false
}
```

<a name="sample"></a>

## <a name="trigger-sample"></a>Tetikleyici örnek
Merhaba Zamanlayıcı tetikleyicisi aşağıdaki hello olduğunu varsayalım `bindings` function.json dizisi:

```json
{
    "schedule": "0 */5 * * * *",
    "name": "myTimer",
    "type": "timerTrigger",
    "direction": "in"
}
```

Geç çalışıp çalışmadığını nesne toosee hello Zamanlayıcı okuyan hello dile özgü örneğine bakın.

* [C#](#triggercsharp)
* [F#](#triggerfsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>Tetikleyici örnek C# #
```csharp
public static void Run(TimerInfo myTimer, TraceWriter log)
{
    if(myTimer.IsPastDue)
    {
        log.Info("Timer is running late!");
    }
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}" );  
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a>F # tetikleyici örnek #
```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter ) =
    if (myTimer.IsPastDue) then
        log.Info("F# function is running late.")
    let now = DateTime.Now.ToLongTimeString()
    log.Info(sprintf "F# function executed at %s!" now)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Node.js tetikleyici örnek
```JavaScript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    if(myTimer.isPastDue)
    {
        context.log('Node.js is running late!');
    }
    context.log('Node.js timer trigger function ran!', timeStamp);   

    context.done();
};
```

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

