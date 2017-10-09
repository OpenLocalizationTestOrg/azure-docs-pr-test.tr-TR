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
# <a name="send-sms-messages-from-azure-functions-using-hello-twilio-output-binding"></a>Azure işlevleri SMS iletileri göndermek hello kullanarak Twilio bağlama çıktı
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Bu makalede açıklanır nasıl Azure işlevleri tooconfigure ve kullanım Twilio bağlamalarla. 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Azure işlevlerini destekleyen işlevleri toosend SMS metin iletileri birkaç kod satırıyla, Twilio çıkış bağlamaları tooenable ve [Twilio](https://www.twilio.com/) hesabı. 

## <a name="functionjson-for-hello-twilio-output-binding"></a>bağlama Twilio Function.JSON hello için çıktı
Merhaba function.json dosyası aşağıdaki özelliklere hello sağlar:

* `name`: Merhaba Twilio SMS mesajı işlevi kod içinde kullanılan değişken adı.
* `type`: çok ayarlanmalıdır*"twilioSms"*.
* `accountSid`: Bu değer, Twilio hesabının SID tutan bir uygulama ayarı toohello adını ayarlamanız gerekir.
* `authToken`: Bu değer, Twilio kimlik doğrulaması belirtecine sahip bir uygulama ayarı toohello adını ayarlamanız gerekir.
* `to`: Bu değer hello SMS metni gönderilir toohello telefon numarası ayarlanır.
* `from`: Bu değer hello SMS metni gönderilen toohello telefon numarası ayarlanır.
* `direction`: çok ayarlanmalıdır*"out"*.
* `body`: Merhaba içinde dinamik olarak kod tooset işlevi için ihtiyaç duymuyorsanız bu değer kullanılan toohard kod hello SMS metin iletisi olabilir. 

Örnek function.json:

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


## <a name="example-c-queue-trigger-with-twilio-output-binding"></a>Örnek C# sıra tetikleyicisi Twilio ile bağlama çıktı
#### <a name="synchronous"></a>Zaman uyumlu
Bu zaman uyumlu örnek kod bir Azure depolama kuyruğu tetikleyicisi için yetersiz kullanan parametre toosend sipariş veren bir metin iletisi tooa müşteri.

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

#### <a name="asynchronous"></a>Zaman uyumsuz
Bir Azure depolama kuyruğu tetikleyicisi için bu zaman uyumsuz örnek kod bir sipariş veren bir metin iletisi tooa müşteri gönderir.

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

## <a name="example-nodejs-queue-trigger-with-twilio-output-binding"></a>Bağlama örnek Node.js sıra tetikleyicisi Twilio ile çıktı
Bu Node.js örnek sipariş veren bir metin iletisi tooa müşteri gönderir.

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

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

