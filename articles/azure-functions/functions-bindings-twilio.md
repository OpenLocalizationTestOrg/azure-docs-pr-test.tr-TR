---
title: "aaaAzure işlevleri Twilio bağlama | Microsoft Docs"
description: "Anlamak nasıl toouse Twilio Azure işlevleri bağlamalarla."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "Azure işlevleri, İşlevler, olay işleme dinamik işlem sunucusuz mimarisi"
ms.assetid: a60263aa-3de9-4e1b-a2bb-0b52e70d559b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/20/2016
ms.author: wesmc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 882853947850e7d6795ca5b2f3fb6b9a83ede182
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="send-sms-messages-from-azure-functions-using-hello-twilio-output-binding"></a><span data-ttu-id="65d5e-104">Azure işlevleri SMS iletileri göndermek hello kullanarak Twilio bağlama çıktı</span><span class="sxs-lookup"><span data-stu-id="65d5e-104">Send SMS messages from Azure Functions using hello Twilio output binding</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="65d5e-105">Bu makalede açıklanır nasıl Azure işlevleri tooconfigure ve kullanım Twilio bağlamalarla.</span><span class="sxs-lookup"><span data-stu-id="65d5e-105">This article explains how tooconfigure and use Twilio bindings with Azure Functions.</span></span> 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="65d5e-106">Azure işlevlerini destekleyen işlevleri toosend SMS metin iletileri birkaç kod satırıyla, Twilio çıkış bağlamaları tooenable ve [Twilio](https://www.twilio.com/) hesabı.</span><span class="sxs-lookup"><span data-stu-id="65d5e-106">Azure Functions supports Twilio output bindings tooenable your functions toosend SMS text messages with a few lines of code and a [Twilio](https://www.twilio.com/) account.</span></span> 

## <a name="functionjson-for-hello-twilio-output-binding"></a><span data-ttu-id="65d5e-107">bağlama Twilio Function.JSON hello için çıktı</span><span class="sxs-lookup"><span data-stu-id="65d5e-107">function.json for hello Twilio output binding</span></span>
<span data-ttu-id="65d5e-108">Merhaba function.json dosyası aşağıdaki özelliklere hello sağlar:</span><span class="sxs-lookup"><span data-stu-id="65d5e-108">hello function.json file provides hello following properties:</span></span>

* <span data-ttu-id="65d5e-109">`name`: Merhaba Twilio SMS mesajı işlevi kod içinde kullanılan değişken adı.</span><span class="sxs-lookup"><span data-stu-id="65d5e-109">`name` : Variable name used in function code for hello Twilio SMS text message.</span></span>
* <span data-ttu-id="65d5e-110">`type`: çok ayarlanmalıdır*"twilioSms"*.</span><span class="sxs-lookup"><span data-stu-id="65d5e-110">`type` : must be set too*"twilioSms"*.</span></span>
* <span data-ttu-id="65d5e-111">`accountSid`: Bu değer, Twilio hesabının SID tutan bir uygulama ayarı toohello adını ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="65d5e-111">`accountSid` : This value must be set toohello name of an App Setting that holds your Twilio Account Sid.</span></span>
* <span data-ttu-id="65d5e-112">`authToken`: Bu değer, Twilio kimlik doğrulaması belirtecine sahip bir uygulama ayarı toohello adını ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="65d5e-112">`authToken` : This value must be set toohello name of an App Setting that holds your Twilio authentication token.</span></span>
* <span data-ttu-id="65d5e-113">`to`: Bu değer hello SMS metni gönderilir toohello telefon numarası ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="65d5e-113">`to` : This value is set toohello phone number that hello SMS text is sent to.</span></span>
* <span data-ttu-id="65d5e-114">`from`: Bu değer hello SMS metni gönderilen toohello telefon numarası ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="65d5e-114">`from` : This value is set toohello phone number that hello SMS text is sent from.</span></span>
* <span data-ttu-id="65d5e-115">`direction`: çok ayarlanmalıdır*"out"*.</span><span class="sxs-lookup"><span data-stu-id="65d5e-115">`direction` : must be set too*"out"*.</span></span>
* <span data-ttu-id="65d5e-116">`body`: Merhaba içinde dinamik olarak kod tooset işlevi için ihtiyaç duymuyorsanız bu değer kullanılan toohard kod hello SMS metin iletisi olabilir.</span><span class="sxs-lookup"><span data-stu-id="65d5e-116">`body` : This value can be used toohard code hello SMS text message if you don't need tooset it dynamically in hello code for your function.</span></span> 

<span data-ttu-id="65d5e-117">Örnek function.json:</span><span class="sxs-lookup"><span data-stu-id="65d5e-117">Example function.json:</span></span>

```json
{
  "type": "twilioSms",
  "name": "message",
  "accountSid": "TwilioAccountSid",
  "authToken": "TwilioAuthToken",
  "to": "+1704XXXXXXX",
  "from": "+1425XXXXXXX",
  "direction": "out",
  "body": "Azure Functions Testing"
}
```


## <a name="example-c-queue-trigger-with-twilio-output-binding"></a><span data-ttu-id="65d5e-118">Örnek C# sıra tetikleyicisi Twilio ile bağlama çıktı</span><span class="sxs-lookup"><span data-stu-id="65d5e-118">Example C# queue trigger with Twilio output binding</span></span>
#### <a name="synchronous"></a><span data-ttu-id="65d5e-119">Zaman uyumlu</span><span class="sxs-lookup"><span data-stu-id="65d5e-119">Synchronous</span></span>
<span data-ttu-id="65d5e-120">Bu zaman uyumlu örnek kod bir Azure depolama kuyruğu tetikleyicisi için yetersiz kullanan parametre toosend sipariş veren bir metin iletisi tooa müşteri.</span><span class="sxs-lookup"><span data-stu-id="65d5e-120">This synchronous example code for an Azure Storage queue trigger uses an out parameter toosend a text message tooa customer who placed an order.</span></span>

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static void Run(string myQueueItem, out SMSMessage message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a JSON string representing an order that contains hello name of a 
    // customer and a mobile number toosend text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want toouse a hard coded message and number in hello binding, you must at least 
    // initialize hello SMSMessage variable.
    message = new SMSMessage();

    // A dynamic message can be set instead of hello body in hello output binding. In this example, we use 
    // hello order information toopersonalize a text message toohello mobile number provided for
    // order status updates.
    message.Body = msg;
    message.too= order.mobileNumber;
}
```

#### <a name="asynchronous"></a><span data-ttu-id="65d5e-121">Zaman uyumsuz</span><span class="sxs-lookup"><span data-stu-id="65d5e-121">Asynchronous</span></span>
<span data-ttu-id="65d5e-122">Bir Azure depolama kuyruğu tetikleyicisi için bu zaman uyumsuz örnek kod bir sipariş veren bir metin iletisi tooa müşteri gönderir.</span><span class="sxs-lookup"><span data-stu-id="65d5e-122">This asynchronous example code for an Azure Storage queue trigger sends a text message tooa customer who placed an order.</span></span>

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static async Task Run(string myQueueItem, IAsyncCollector<SMSMessage> message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a JSON string representing an order that contains hello name of a 
    // customer and a mobile number toosend text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want toouse a hard coded message and number in hello binding, you must at least 
    // initialize hello SMSMessage variable.
    SMSMessage smsText = new SMSMessage();

    // A dynamic message can be set instead of hello body in hello output binding. In this example, we use 
    // hello order information toopersonalize a text message toohello mobile number provided for
    // order status updates.
    smsText.Body = msg;
    smsText.too= order.mobileNumber;

    await message.AddAsync(smsText);
}
```

## <a name="example-nodejs-queue-trigger-with-twilio-output-binding"></a><span data-ttu-id="65d5e-123">Bağlama örnek Node.js sıra tetikleyicisi Twilio ile çıktı</span><span class="sxs-lookup"><span data-stu-id="65d5e-123">Example Node.js queue trigger with Twilio output binding</span></span>
<span data-ttu-id="65d5e-124">Bu Node.js örnek sipariş veren bir metin iletisi tooa müşteri gönderir.</span><span class="sxs-lookup"><span data-stu-id="65d5e-124">This Node.js example sends a text message tooa customer who placed an order.</span></span>

```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);

    // In this example hello queue item is a JSON string representing an order that contains hello name of a 
    // customer and a mobile number toosend text updates to.
    var msg = "Hello " + myQueueItem.name + ", thank you for your order.";

    // Even if you want toouse a hard coded message and number in hello binding, you must at least 
    // initialize hello message binding.
    context.bindings.message = {};

    // A dynamic message can be set instead of hello body in hello output binding. In this example, we use 
    // hello order information toopersonalize a text message toohello mobile number provided for
    // order status updates.
    context.bindings.message = {
        body : msg,
        too: myQueueItem.mobileNumber
    };

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="65d5e-125">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="65d5e-125">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

