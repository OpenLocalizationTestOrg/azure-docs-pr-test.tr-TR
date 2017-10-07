---
title: "aaaAzure işlevleri bildirim hub'ı bağlama | Microsoft Docs"
description: "Anlamak nasıl Azure işlevlerinde toouse Azure bildirim hub'ı bağlama."
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
keywords: "Azure işlevleri, İşlevler, olay işleme dinamik işlem sunucusuz mimarisi"
ms.assetid: 0ff0c949-20bf-430b-8dd5-d72b7b6ee6f7
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/27/2016
ms.author: glenga
ms.openlocfilehash: d192424a8ec701d02f8bcb4aa4c1d189b20537a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-notification-hub-output-binding"></a>Azure işlevleri bildirim hub'ı bağlama çıktı
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Bu makalede açıklanır nasıl Azure işlevlerinde tooconfigure ve kod Azure bildirim hub'ı bağlar. 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

İşlevlerinizi birkaç kod satırıyla, bir yapılandırılmış Azure bildirim hub'ı kullanarak anında iletme bildirimleri gönderebilirsiniz. Ancak, hello Azure bildirim hub'ı Platform Bildirim Hizmetleri (PNS) toouse istediğiniz hello için yapılandırılmış olması gerekir. Bir Azure bildirim hub'ı yapılandırma ve tooreceive bildirimleri kaydetmek istemci uygulamaları geliştirme hakkında daha fazla bilgi için bkz: [Notification Hubs ile çalışmaya başlama](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) ve hedef istemci platformunuzu hello adresindeki'ı tıklatın Sayfanın Üstü.

gönderdiğiniz hello bildirimleri yerel bildirimleri veya şablon bildirimleri olabilir. Yerel bildirimler hello yapılandırıldığı gibi belirli bildirim platform hedef `platform` hello özelliğinin çıkış bağlama. Bir şablon bildirim kullanılan tootarget birden çok platform olabilir.   

## <a name="notification-hub-output-binding-properties"></a>Bildirim hub'ı çıkış bağlama özellikleri
Merhaba function.json dosyası aşağıdaki özelliklere hello sağlar:

* `name`: İşlev kodu hello bildirim hub'ı iletisi için kullanılan değişken adı.
* `type`: çok ayarlanmalıdır*"notificationHub"*.
* `tagExpression`: Etiket ifadeleri hello etiketi ifadeyle eşleşecek tooreceive bildirimleri kaydolan cihazlar tooa kümesi bildirimleri teslim edilmesi toospecify izin verin.  Daha fazla bilgi için bkz: [Yönlendirme ve etiket ifadeleri](../notification-hubs/notification-hubs-tags-segment-push-message.md).
* `hubName`: Hello bildirim hub'ı kaynak hello Azure portal'ın adı.
* `connection`: Bu bağlantı dizesi olmalıdır bir **uygulama ayarı** bağlantı dizesini ayarlamak toohello *DefaultFullSharedAccessSignature* bildirim hub'ınız için değer.
* `direction`: çok ayarlanmalıdır*"out"*. 
* `platform`: hello platform özelliği hello bildirim platform bildirim hedeflerinizi gösterir. Değerleri aşağıdaki hello biri olmalıdır:
  * Merhaba platform özelliği bağlama, hello çıktısını atlanırsa, varsayılan olarak, herhangi bir platform hello Azure bildirim hub'ı üzerinde yapılandırılmış kullanılan tootarget şablon bildirimleri olabilir. Toosend platform bildirimleri ile Azure bildirim Hub'bir çapraz şablonları genel olarak kullanma hakkında daha fazla bilgi için bkz: [şablonları](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).
  * `apns`: Apple anında bildirim hizmeti. APNS için hello bildirim hub'ı yapılandırma ve bir istemci uygulamasında hello bildirim alma hakkında daha fazla bilgi için bkz: [Azure Notification Hubs ile anında iletme bildirimleri tooiOS gönderme](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md) 
  * `adm`: [Amazon Device Messaging](https://developer.amazon.com/device-messaging). ADM için hello bildirim hub'ı yapılandırma ve bir Kindle uygulaması hello bildirim alma hakkında daha fazla bilgi için bkz: [Kindle uygulamaları için Notification Hubs ile çalışmaya başlama](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md) 
  * `gcm`: [Google Cloud Messaging'i](https://developers.google.com/cloud-messaging/). Firebase bulut GCM hello yeni sürümü olan ileti, da desteklenir. GCM/FCM hello bildirim hub'ı yapılandırma ve bir Android istemci uygulamasını hello bildirim alma hakkında daha fazla bilgi için bkz: [Azure Notification Hubs ile anında iletme bildirimleri tooAndroid gönderme](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)
  * `wns`: [Windows anında bildirim Hizmetleri](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) Windows platformları hedefleme. Windows Phone 8.1 ve üzeri WNS tarafından da desteklenir. WNS için hello bildirim hub'ı yapılandırma ve bir evrensel Windows Platformu (UWP) uygulamasını hello bildirim alma hakkında daha fazla bilgi için bkz: [uygulamaları için Notification Hubs Windows Evrensel Platform ile çalışmaya başlama](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)
  * `mpns`: [Microsoft anında bildirim hizmeti](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx). Bu platform, Windows Phone 8 ve daha önceki Windows Phone platformlarını destekler. MPNS için hello bildirim hub'ı yapılandırma ve bir Windows Phone Uygulama hello bildirim alma hakkında daha fazla bilgi için bkz: [Windows Phone üzerinde Azure Notification Hubs ile anında iletme bildirimleri gönderme](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)

Örnek function.json:

```json
{
  "bindings": [
    {
      "name": "notification",
      "type": "notificationHub",
      "tagExpression": "",
      "hubName": "my-notification-hub",
      "connection": "MyHubConnectionString",
      "platform": "gcm",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

## <a name="notification-hub-connection-string-setup"></a>Bildirim hub'ı bağlantı dizesi kurulumu
bağlama toouse bir bildirim hub'ı çıktı, hello bağlantı dizesi hello hub için yapılandırmanız gerekir. Bu hello üzerinde yapılabilir *tümleştirme* , bildirim hub'ı seçerek veya yenisini oluşturarak sekmesi. 

Hello için bir bağlantı dizesi ekleyerek bir bağlantı dizesi olan bir hub'ınız için el ile de ekleyebilirsiniz *DefaultFullSharedAccessSignature* tooyour bildirim hub'ı. Bu bağlantı dizesi, işlevi erişim izni toosend bildirim iletilerini sağlar. Merhaba *DefaultFullSharedAccessSignature* hello bağlantı dizesi değeri erişilebilir **anahtarları** hello ana dikey penceresinde hello Azure portal, bildirim hub'ı kaynağın düğmesi. toomanually hub'ınız için aşağıdaki adımları kullanın hello bir bağlantı dizesi ekleyin: 

1. Merhaba üzerinde **işlev uygulaması** hello Azure portal dikey tıklayın **işlev uygulama ayarları > tooApp hizmeti ayarlarına Git**.
2. Merhaba, **ayarları** dikey penceresinde tıklatın **uygulama ayarları**.
3. Toohello aşağı **uygulama ayarları** bölüm ve bir adlandırılmış girişi ile eklemek *DefaultFullSharedAccessSignature* bildirim hub'ınız için değer.
4. Çıktı bağlamaları hello ayar dize adı uygulamanızı başvuru. Benzer çok**MyHubConnectionString** hello yukarıdaki örnekte kullanılan.

## <a name="apns-native-notifications-with-c-queue-triggers"></a>C# queue tetikleyicileri ile APNS yerel bildirimleri
Bu örnek nasıl toouse türleri hello tanımlanan gösterir [Microsoft Azure bildirim hub'ları Kitaplığı](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend yerel APNS bildirim. 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a new user toobe processed in hello form of a JSON string with 
    // a "name" value.
    //
    // hello JSON format for a native APNS notification is ...
    // { "aps": { "alert": "notification message" }}  

    log.Info($"Sending APNS notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string apnsNotificationPayload = "{\"aps\": {\"alert\": \"A new user wants toobe added (" + 
                                        user.name + ")\" }}";
    log.Info($"{apnsNotificationPayload}");
    await notification.AddAsync(new AppleNotification(apnsNotificationPayload));        
}
```

## <a name="gcm-native-notifications-with-c-queue-triggers"></a>C# queue tetikleyicileri ile GCM yerel bildirimleri
Bu örnek nasıl toouse türleri hello tanımlanan gösterir [Microsoft Azure bildirim hub'ları Kitaplığı](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend yerel GCM bildirim. 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a new user toobe processed in hello form of a JSON string with 
    // a "name" value.
    //
    // hello JSON format for a native GCM notification is ...
    // { "data": { "message": "notification message" }}  

    log.Info($"Sending GCM notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string gcmNotificationPayload = "{\"data\": {\"message\": \"A new user wants toobe added (" + 
                                        user.name + ")\" }}";
    log.Info($"{gcmNotificationPayload}");
    await notification.AddAsync(new GcmNotification(gcmNotificationPayload));        
}
```

## <a name="wns-native-notifications-with-c-queue-triggers"></a>C# queue tetikleyicileri ile WNS yerel bildirimleri
Bu örnek nasıl toouse türleri hello tanımlanan gösterir [Microsoft Azure bildirim hub'ları Kitaplığı](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend yerel WNS kutlayın bildirim. 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a new user toobe processed in hello form of a JSON string with 
    // a "name" value.
    //
    // hello XML format for a native WNS toast notification is ...
    // <?xml version="1.0" encoding="utf-8"?>
    // <toast>
    //      <visual>
    //     <binding template="ToastText01">
    //       <text id="1">notification message</text>
    //     </binding>
    //   </visual>
    // </toast>

    log.Info($"Sending WNS toast notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string wnsNotificationPayload = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                                    "<toast><visual><binding template=\"ToastText01\">" +
                                        "<text id=\"1\">" + 
                                            "A new user wants toobe added (" + user.name + ")" + 
                                        "</text>" +
                                    "</binding></visual></toast>";

    log.Info($"{wnsNotificationPayload}");
    await notification.AddAsync(new WindowsNotification(wnsNotificationPayload));        
}
```

## <a name="template-example-for-nodejs-timer-triggers"></a>Şablon örneği için Node.js Zamanlayıcı Tetikleyicileri
Bu örnek, bir bildirim gönderir bir [şablonu kayıt](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) içeren `location` ve `message`.

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    if(myTimer.isPastDue)
    {
        context.log('Node.js is running late!');
    }
    context.log('Node.js timer trigger function ran!', timeStamp);  
    context.bindings.notification = {
        location: "Redmond",
        message: "Hello from Node!"
    };
    context.done();
};
```

## <a name="template-example-for-f-timer-triggers"></a>F # Zamanlayıcı Tetikleyicileri şablon Örneğin
Bu örnek, bir bildirim gönderir bir [şablonu kayıt](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) içeren `location` ve `message`.

```fsharp
let Run(myTimer: TimerInfo, notification: byref<IDictionary<string, string>>) =
    notification = dict [("location", "Redmond"); ("message", "Hello from F#!")]
```

## <a name="template-example-using-an-out-parameter"></a>Out parametresi kullanılarak şablon örneği
Bu örnek, bir bildirim gönderir bir [şablonu kayıt](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) içeren bir `message` hello şablonunda yer tutucusu.

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static void Run(string myQueueItem,  out IDictionary<string, string> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = GetTemplateProperties(myQueueItem);
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["message"] = message;
    return templateProperties;
}
```

## <a name="template-example-with-asynchronous-function"></a>Şablon örneği ile zaman uyumsuz işlevi
Zaman uyumsuz kod kullanıyorsanız, out Parametreleri izin verilmiyor. Bu durumda kullanarak `IAsyncCollector` tooreturn, şablon bildirim. Merhaba aşağıdaki kodu zaman uyumsuz yukarıdaki hello kod örneğidir. 

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static async Task Run(string myQueueItem, IAsyncCollector<IDictionary<string,string>> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    log.Info($"Sending Template Notification tooNotification Hub");
    await notification.AddAsync(GetTemplateProperties(myQueueItem));    
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["user"] = "A new user wants toobe added : " + message;
    return templateProperties;
}
```

## <a name="template-example-using-json"></a>JSON kullanarak şablon örneği
Bu örnek, bir bildirim gönderir bir [şablonu kayıt](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) içeren bir `message` kullanarak geçerli bir JSON dizesi hello şablonunda yer tutucusu.

```cs
using System;

public static void Run(string myQueueItem,  out string notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = "{\"message\":\"Hello from C#. Processed a queue item!\"}";
}
```

## <a name="template-example-using-notification-hubs-library-types"></a>Şablon örneği bildirim hub'ları kitaplığı türleri kullanma
Bu örnek nasıl toouse türleri hello tanımlanan gösterir [Microsoft Azure bildirim hub'ları Kitaplığı](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/). 

```cs
#r "Microsoft.Azure.NotificationHubs"

using System;
using System.Threading.Tasks;
using Microsoft.Azure.NotificationHubs;

public static void Run(string myQueueItem,  out Notification notification, TraceWriter log)
{
   log.Info($"C# Queue trigger function processed: {myQueueItem}");
   notification = GetTemplateNotification(myQueueItem);
}

private static TemplateNotification GetTemplateNotification(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["message"] = message;
    return new TemplateNotification(templateProperties);
}
```

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

