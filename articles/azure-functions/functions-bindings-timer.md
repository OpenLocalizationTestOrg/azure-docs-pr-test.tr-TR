---
title: "Azure işlevleri Zamanlayıcı tetikleyicisi | Microsoft Docs"
description: "Azure işlevleri Zamanlayıcı Tetikleyicileri kullanmayı öğrenme."
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
ms.openlocfilehash: 6a97ab8508f889b77d064a5da70e3c726d62900c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-timer-trigger"></a><span data-ttu-id="d0e64-104">Azure işlevleri Zamanlayıcı tetikleyicisi</span><span class="sxs-lookup"><span data-stu-id="d0e64-104">Azure Functions timer trigger</span></span>

[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="d0e64-105">Bu makalede nasıl yapılandırılacağı ve kod Zamanlayıcı Tetikleyicileri Azure işlevleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d0e64-105">This article explains how to configure and code timer triggers in Azure Functions.</span></span> <span data-ttu-id="d0e64-106">Azure işlevleri tanımlanmış bir zamanlamaya göre işlevi kodunuzu çalıştırmak olanak sağlayan zamanlayıcı tetikleyicisi bağlama sahiptir.</span><span class="sxs-lookup"><span data-stu-id="d0e64-106">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> 

<span data-ttu-id="d0e64-107">Zamanlayıcı tetikleyicisi çok örnekli genişleme destekler. Belirli Zamanlayıcı işlevi tek bir örneğini boyunca tüm örneklerde çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="d0e64-107">The timer trigger supports multi-instance scale-out. A single instance of a particular timer function is run across all instances.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a id="trigger"></a>

## <a name="timer-trigger"></a><span data-ttu-id="d0e64-108">Zamanlayıcı tetikleyicisi</span><span class="sxs-lookup"><span data-stu-id="d0e64-108">Timer trigger</span></span>
<span data-ttu-id="d0e64-109">Aşağıdaki JSON nesnesinde bir işleve Zamanlayıcı tetikleyicisi kullanan `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="d0e64-109">The timer trigger to a function uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "schedule": "<CRON expression - see below>",
    "name": "<Name of trigger parameter in function signature>",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="d0e64-110">Değeri `schedule` olan bir [CRON ifade](http://en.wikipedia.org/wiki/Cron#CRON_expression) altı bu alanları içerir:</span><span class="sxs-lookup"><span data-stu-id="d0e64-110">The value of `schedule` is a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that includes these six fields:</span></span> 

    {second} {minute} {hour} {day} {month} {day-of-week}
&nbsp;
>[!NOTE]   
><span data-ttu-id="d0e64-111">Birçok çevrimiçi Bul cron ifadelerin atlayın `{second}` alan.</span><span class="sxs-lookup"><span data-stu-id="d0e64-111">Many of the cron expressions you find online omit the `{second}` field.</span></span> <span data-ttu-id="d0e64-112">Bunlardan birini kopyalarsanız, ek için ayarlamanız gereken `{second}` alan.</span><span class="sxs-lookup"><span data-stu-id="d0e64-112">If you copy from one of them, you need to adjust for the extra `{second}` field.</span></span> <span data-ttu-id="d0e64-113">Belirli örnekler için bkz: [zamanlama örnekler](#examples) aşağıda.</span><span class="sxs-lookup"><span data-stu-id="d0e64-113">For specific examples, see [Schedule examples](#examples) below.</span></span>

<span data-ttu-id="d0e64-114">CRON ifadelerle kullanılan varsayılan saat dilimini Eşgüdümlü Evrensel Saat (UTC) ' dir.</span><span class="sxs-lookup"><span data-stu-id="d0e64-114">The default time zone used with the CRON expressions is Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="d0e64-115">CRON İfadenizde başka bir saat dilimini temel olmasını adlı işlev uygulamanız için yeni bir uygulama ayarı oluşturmak `WEBSITE_TIME_ZONE`.</span><span class="sxs-lookup"><span data-stu-id="d0e64-115">To have your CRON expression based on another time zone, create a new app setting for your function app named `WEBSITE_TIME_ZONE`.</span></span> <span data-ttu-id="d0e64-116">İstenen saat dilimini adına gösterildiği gibi değeri [Microsoft saat dilimi dizin](https://msdn.microsoft.com/library/ms912391.aspx).</span><span class="sxs-lookup"><span data-stu-id="d0e64-116">Set the value to the name of the desired time zone as shown in the [Microsoft Time Zone Index](https://msdn.microsoft.com/library/ms912391.aspx).</span></span> 

<span data-ttu-id="d0e64-117">Örneğin, *Doğu Standart Saati* olan UTC-05:00.</span><span class="sxs-lookup"><span data-stu-id="d0e64-117">For example, *Eastern Standard Time* is UTC-05:00.</span></span> <span data-ttu-id="d0e64-118">10:00 AM EST her gün yangın tetikleyin, UTC saat dilimi hesapları aşağıdaki CRON deyimi kullanın, Zamanlayıcı sağlamak için:</span><span class="sxs-lookup"><span data-stu-id="d0e64-118">To have your timer trigger fire at 10:00 AM EST every day, use the following CRON expression that accounts for UTC time zone:</span></span>

```json
"schedule": "0 0 15 * * *",
``` 

<span data-ttu-id="d0e64-119">Alternatif olarak, adlı işlev uygulamanız için yeni bir uygulama ayarı ekleyebilirsiniz `WEBSITE_TIME_ZONE` ve değerine **Doğu Standart Saati**.</span><span class="sxs-lookup"><span data-stu-id="d0e64-119">Alternatively, you could add a new app setting for your function app named `WEBSITE_TIME_ZONE` and set the value to **Eastern Standard Time**.</span></span>  <span data-ttu-id="d0e64-120">Ardından aşağıdaki CRON ifade 10:00 AM EST için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="d0e64-120">Then the following CRON expression could be used for 10:00 AM EST:</span></span> 

```json
"schedule": "0 0 10 * * *",
``` 


<a name="examples"></a>

## <a name="schedule-examples"></a><span data-ttu-id="d0e64-121">Zamanlama örnekleri</span><span class="sxs-lookup"><span data-stu-id="d0e64-121">Schedule examples</span></span>
<span data-ttu-id="d0e64-122">CRON ifadeler için kullanabileceğiniz bazı örnekleri şunlardır `schedule` özelliği.</span><span class="sxs-lookup"><span data-stu-id="d0e64-122">Here are some samples of CRON expressions you can use for the `schedule` property.</span></span> 

<span data-ttu-id="d0e64-123">Her beş dakikada tetiklemek için:</span><span class="sxs-lookup"><span data-stu-id="d0e64-123">To trigger once every five minutes:</span></span>

```json
"schedule": "0 */5 * * * *"
```

<span data-ttu-id="d0e64-124">Bir kez saatte en üstte tetiklemek için:</span><span class="sxs-lookup"><span data-stu-id="d0e64-124">To trigger once at the top of every hour:</span></span>

```json
"schedule": "0 0 * * * *",
```

<span data-ttu-id="d0e64-125">Her iki saatte tetiklemek için:</span><span class="sxs-lookup"><span data-stu-id="d0e64-125">To trigger once every two hours:</span></span>

```json
"schedule": "0 0 */2 * * *",
```

<span data-ttu-id="d0e64-126">Saatte 09: 00'dan 18: 00 için tetiklemek için:</span><span class="sxs-lookup"><span data-stu-id="d0e64-126">To trigger once every hour from 9 AM to 5 PM:</span></span>

```json
"schedule": "0 0 9-17 * * *",
```

<span data-ttu-id="d0e64-127">09:30:00 her gün tetiklemek için:</span><span class="sxs-lookup"><span data-stu-id="d0e64-127">To trigger At 9:30 AM every day:</span></span>

```json
"schedule": "0 30 9 * * *",
```

<span data-ttu-id="d0e64-128">09:30:00 her hafta içi günü tetiklemek için:</span><span class="sxs-lookup"><span data-stu-id="d0e64-128">To trigger At 9:30 AM every weekday:</span></span>

```json
"schedule": "0 30 9 * * 1-5",
```

<a name="usage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="d0e64-129">Tetikleyici kullanımı</span><span class="sxs-lookup"><span data-stu-id="d0e64-129">Trigger usage</span></span>
<span data-ttu-id="d0e64-130">Bir zamanlayıcı tetikleyicisi işlevi çağrıldığında, [Zamanlayıcı nesne](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) işlevdeki geçirilir.</span><span class="sxs-lookup"><span data-stu-id="d0e64-130">When a timer trigger function is invoked, the [timer object](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) is passed into the function.</span></span> <span data-ttu-id="d0e64-131">Aşağıdaki JSON timer nesnesi bir örnek gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="d0e64-131">The following JSON is an example representation of the timer object.</span></span> 

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

## <a name="trigger-sample"></a><span data-ttu-id="d0e64-132">Tetikleyici örnek</span><span class="sxs-lookup"><span data-stu-id="d0e64-132">Trigger sample</span></span>
<span data-ttu-id="d0e64-133">Aşağıdaki Zamanlayıcı tetikleyicisi olduğunu varsayalım `bindings` function.json dizisi:</span><span class="sxs-lookup"><span data-stu-id="d0e64-133">Suppose you have the following timer trigger in the `bindings` array of function.json:</span></span>

```json
{
    "schedule": "0 */5 * * * *",
    "name": "myTimer",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="d0e64-134">Geç çalışıp çalışmadığını görmek için timer nesnesini okur dile özgü örneğe bakın.</span><span class="sxs-lookup"><span data-stu-id="d0e64-134">See the language-specific sample that reads the timer object to see whether it's running late.</span></span>

* [<span data-ttu-id="d0e64-135">C#</span><span class="sxs-lookup"><span data-stu-id="d0e64-135">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="d0e64-136">F#</span><span class="sxs-lookup"><span data-stu-id="d0e64-136">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="d0e64-137">Node.js</span><span class="sxs-lookup"><span data-stu-id="d0e64-137">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="d0e64-138">Tetikleyici örnek C#</span><span class="sxs-lookup"><span data-stu-id="d0e64-138">Trigger sample in C#</span></span> #
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

### <a name="trigger-sample-in-f"></a><span data-ttu-id="d0e64-139">F # tetikleyici örnek</span><span class="sxs-lookup"><span data-stu-id="d0e64-139">Trigger sample in F#</span></span> #
```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter ) =
    if (myTimer.IsPastDue) then
        log.Info("F# function is running late.")
    let now = DateTime.Now.ToLongTimeString()
    log.Info(sprintf "F# function executed at %s!" now)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="d0e64-140">Node.js tetikleyici örnek</span><span class="sxs-lookup"><span data-stu-id="d0e64-140">Trigger sample in Node.js</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="d0e64-141">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d0e64-141">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

