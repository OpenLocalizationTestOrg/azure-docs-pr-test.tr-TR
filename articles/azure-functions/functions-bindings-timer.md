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
# <a name="azure-functions-timer-trigger"></a><span data-ttu-id="eeac5-104">Azure işlevleri Zamanlayıcı tetikleyicisi</span><span class="sxs-lookup"><span data-stu-id="eeac5-104">Azure Functions timer trigger</span></span>

[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="eeac5-105">Bu makalede, Azure işlevlerinde nasıl tooconfigure ve kod Zamanlayıcı tetikler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="eeac5-105">This article explains how tooconfigure and code timer triggers in Azure Functions.</span></span> <span data-ttu-id="eeac5-106">Azure işlevleri tanımlanmış bir zamanlamaya göre işlevi kodunuzu çalıştırmak olanak sağlayan zamanlayıcı tetikleyicisi bağlama sahiptir.</span><span class="sxs-lookup"><span data-stu-id="eeac5-106">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> 

<span data-ttu-id="eeac5-107">çok örnekli genişleme Hello Zamanlayıcı tetikleyicisi destekler. Belirli Zamanlayıcı işlevi tek bir örneğini boyunca tüm örneklerde çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="eeac5-107">hello timer trigger supports multi-instance scale-out. A single instance of a particular timer function is run across all instances.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a id="trigger"></a>

## <a name="timer-trigger"></a><span data-ttu-id="eeac5-108">Zamanlayıcı tetikleyicisi</span><span class="sxs-lookup"><span data-stu-id="eeac5-108">Timer trigger</span></span>
<span data-ttu-id="eeac5-109">Merhaba Zamanlayıcı tetikleyicisi tooa işlevini kullanıyor hello JSON nesnesinde aşağıdaki hello `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="eeac5-109">hello timer trigger tooa function uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "schedule": "<CRON expression - see below>",
    "name": "<Name of trigger parameter in function signature>",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="eeac5-110">Merhaba değerini `schedule` olan bir [CRON ifade](http://en.wikipedia.org/wiki/Cron#CRON_expression) altı bu alanları içerir:</span><span class="sxs-lookup"><span data-stu-id="eeac5-110">hello value of `schedule` is a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that includes these six fields:</span></span> 

    {second} {minute} {hour} {day} {month} {day-of-week}
&nbsp;
>[!NOTE]   
><span data-ttu-id="eeac5-111">Birçok çevrimiçi Bul hello cron ifadelerin hello atlayın `{second}` alan.</span><span class="sxs-lookup"><span data-stu-id="eeac5-111">Many of hello cron expressions you find online omit hello `{second}` field.</span></span> <span data-ttu-id="eeac5-112">Bunlardan birini kopyalarsanız, hello fazladan tooadjust gerek `{second}` alan.</span><span class="sxs-lookup"><span data-stu-id="eeac5-112">If you copy from one of them, you need tooadjust for hello extra `{second}` field.</span></span> <span data-ttu-id="eeac5-113">Belirli örnekler için bkz: [zamanlama örnekler](#examples) aşağıda.</span><span class="sxs-lookup"><span data-stu-id="eeac5-113">For specific examples, see [Schedule examples](#examples) below.</span></span>

<span data-ttu-id="eeac5-114">Merhaba varsayılan saat dilimi hello CRON ifadelerle kullanılan Eşgüdümlü Evrensel Saat (UTC) alınır.</span><span class="sxs-lookup"><span data-stu-id="eeac5-114">hello default time zone used with hello CRON expressions is Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="eeac5-115">CRON İfadenizde bağlı başka bir saat dilimini temel toohave adlı işlev uygulamanız için yeni bir uygulama ayarı oluşturmak `WEBSITE_TIME_ZONE`.</span><span class="sxs-lookup"><span data-stu-id="eeac5-115">toohave your CRON expression based on another time zone, create a new app setting for your function app named `WEBSITE_TIME_ZONE`.</span></span> <span data-ttu-id="eeac5-116">Set hello değeri toohello hello adını istenen saat dilimi hello gösterildiği gibi [Microsoft saat dilimi dizin](https://msdn.microsoft.com/library/ms912391.aspx).</span><span class="sxs-lookup"><span data-stu-id="eeac5-116">Set hello value toohello name of hello desired time zone as shown in hello [Microsoft Time Zone Index](https://msdn.microsoft.com/library/ms912391.aspx).</span></span> 

<span data-ttu-id="eeac5-117">Örneğin, *Doğu Standart Saati* olan UTC-05:00.</span><span class="sxs-lookup"><span data-stu-id="eeac5-117">For example, *Eastern Standard Time* is UTC-05:00.</span></span> <span data-ttu-id="eeac5-118">toohave, Zamanlayıcı tetiklemek yangın 10:00 AM EST, her gün için UTC saat dilimi hesapları CRON ifade aşağıdaki kullanım hello adresindeki:</span><span class="sxs-lookup"><span data-stu-id="eeac5-118">toohave your timer trigger fire at 10:00 AM EST every day, use hello following CRON expression that accounts for UTC time zone:</span></span>

```json
"schedule": "0 0 15 * * *",
``` 

<span data-ttu-id="eeac5-119">Alternatif olarak, adlı işlev uygulamanız için yeni bir uygulama ayarı ekleyebilirsiniz `WEBSITE_TIME_ZONE` ve hello değeri çok**Doğu Standart Saati**.</span><span class="sxs-lookup"><span data-stu-id="eeac5-119">Alternatively, you could add a new app setting for your function app named `WEBSITE_TIME_ZONE` and set hello value too**Eastern Standard Time**.</span></span>  <span data-ttu-id="eeac5-120">Ardından CRON ifade aşağıdaki hello 10:00 AM EST için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="eeac5-120">Then hello following CRON expression could be used for 10:00 AM EST:</span></span> 

```json
"schedule": "0 0 10 * * *",
``` 


<a name="examples"></a>

## <a name="schedule-examples"></a><span data-ttu-id="eeac5-121">Zamanlama örnekleri</span><span class="sxs-lookup"><span data-stu-id="eeac5-121">Schedule examples</span></span>
<span data-ttu-id="eeac5-122">CRON ifadeleri hello için kullanabileceğiniz bazı örnekleri şunlardır `schedule` özelliği.</span><span class="sxs-lookup"><span data-stu-id="eeac5-122">Here are some samples of CRON expressions you can use for hello `schedule` property.</span></span> 

<span data-ttu-id="eeac5-123">her beş dakikada tootrigger:</span><span class="sxs-lookup"><span data-stu-id="eeac5-123">tootrigger once every five minutes:</span></span>

```json
"schedule": "0 */5 * * * *"
```

<span data-ttu-id="eeac5-124">tootrigger kez üstündeki hello her saat:</span><span class="sxs-lookup"><span data-stu-id="eeac5-124">tootrigger once at hello top of every hour:</span></span>

```json
"schedule": "0 0 * * * *",
```

<span data-ttu-id="eeac5-125">Her iki saatte tootrigger:</span><span class="sxs-lookup"><span data-stu-id="eeac5-125">tootrigger once every two hours:</span></span>

```json
"schedule": "0 0 */2 * * *",
```

<span data-ttu-id="eeac5-126">tootrigger saatte 09: 00 too5 gelen PM:</span><span class="sxs-lookup"><span data-stu-id="eeac5-126">tootrigger once every hour from 9 AM too5 PM:</span></span>

```json
"schedule": "0 0 9-17 * * *",
```

<span data-ttu-id="eeac5-127">tootrigger 9: 30'da her gün:</span><span class="sxs-lookup"><span data-stu-id="eeac5-127">tootrigger At 9:30 AM every day:</span></span>

```json
"schedule": "0 30 9 * * *",
```

<span data-ttu-id="eeac5-128">tootrigger 9: 30'da her hafta içi günü:</span><span class="sxs-lookup"><span data-stu-id="eeac5-128">tootrigger At 9:30 AM every weekday:</span></span>

```json
"schedule": "0 30 9 * * 1-5",
```

<a name="usage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="eeac5-129">Tetikleyici kullanımı</span><span class="sxs-lookup"><span data-stu-id="eeac5-129">Trigger usage</span></span>
<span data-ttu-id="eeac5-130">Bir zamanlayıcı tetikleyicisi işlevi çağrıldığında, hello [Zamanlayıcı nesne](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) hello işlevdeki geçirilir.</span><span class="sxs-lookup"><span data-stu-id="eeac5-130">When a timer trigger function is invoked, hello [timer object](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) is passed into hello function.</span></span> <span data-ttu-id="eeac5-131">Merhaba aşağıdaki JSON bir örnek hello Zamanlayıcı nesne gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="eeac5-131">hello following JSON is an example representation of hello timer object.</span></span> 

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

## <a name="trigger-sample"></a><span data-ttu-id="eeac5-132">Tetikleyici örnek</span><span class="sxs-lookup"><span data-stu-id="eeac5-132">Trigger sample</span></span>
<span data-ttu-id="eeac5-133">Merhaba Zamanlayıcı tetikleyicisi aşağıdaki hello olduğunu varsayalım `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="eeac5-133">Suppose you have hello following timer trigger in hello `bindings` array of function.json:</span></span>

```json
{
    "schedule": "0 */5 * * * *",
    "name": "myTimer",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="eeac5-134">Geç çalışıp çalışmadığını nesne toosee hello Zamanlayıcı okuyan hello dile özgü örneğine bakın.</span><span class="sxs-lookup"><span data-stu-id="eeac5-134">See hello language-specific sample that reads hello timer object toosee whether it's running late.</span></span>

* [<span data-ttu-id="eeac5-135">C#</span><span class="sxs-lookup"><span data-stu-id="eeac5-135">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="eeac5-136">F#</span><span class="sxs-lookup"><span data-stu-id="eeac5-136">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="eeac5-137">Node.js</span><span class="sxs-lookup"><span data-stu-id="eeac5-137">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="eeac5-138">Tetikleyici örnek C#</span><span class="sxs-lookup"><span data-stu-id="eeac5-138">Trigger sample in C#</span></span> #
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

### <a name="trigger-sample-in-f"></a><span data-ttu-id="eeac5-139">F # tetikleyici örnek</span><span class="sxs-lookup"><span data-stu-id="eeac5-139">Trigger sample in F#</span></span> #
```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter ) =
    if (myTimer.IsPastDue) then
        log.Info("F# function is running late.")
    let now = DateTime.Now.ToLongTimeString()
    log.Info(sprintf "F# function executed at %s!" now)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="eeac5-140">Node.js tetikleyici örnek</span><span class="sxs-lookup"><span data-stu-id="eeac5-140">Trigger sample in Node.js</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="eeac5-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="eeac5-141">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

