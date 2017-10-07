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
# <a name="azure-functions-notification-hub-output-binding"></a><span data-ttu-id="aad3a-104">Azure işlevleri bildirim hub'ı bağlama çıktı</span><span class="sxs-lookup"><span data-stu-id="aad3a-104">Azure Functions Notification Hub output binding</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="aad3a-105">Bu makalede açıklanır nasıl Azure işlevlerinde tooconfigure ve kod Azure bildirim hub'ı bağlar.</span><span class="sxs-lookup"><span data-stu-id="aad3a-105">This article explains how tooconfigure and code Azure Notification Hub bindings in Azure Functions.</span></span> 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="aad3a-106">İşlevlerinizi birkaç kod satırıyla, bir yapılandırılmış Azure bildirim hub'ı kullanarak anında iletme bildirimleri gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aad3a-106">Your functions can send push notifications using a configured Azure Notification Hub with a few lines of code.</span></span> <span data-ttu-id="aad3a-107">Ancak, hello Azure bildirim hub'ı Platform Bildirim Hizmetleri (PNS) toouse istediğiniz hello için yapılandırılmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="aad3a-107">However, hello Azure Notification Hub must be configured for hello Platform Notifications Services (PNS) you want toouse.</span></span> <span data-ttu-id="aad3a-108">Bir Azure bildirim hub'ı yapılandırma ve tooreceive bildirimleri kaydetmek istemci uygulamaları geliştirme hakkında daha fazla bilgi için bkz: [Notification Hubs ile çalışmaya başlama](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) ve hedef istemci platformunuzu hello adresindeki'ı tıklatın Sayfanın Üstü.</span><span class="sxs-lookup"><span data-stu-id="aad3a-108">For more information on configuring an Azure Notification Hub and developing a client applications that register tooreceive notifications, see [Getting started with Notification Hubs](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) and click your target client platform at hello top.</span></span>

<span data-ttu-id="aad3a-109">gönderdiğiniz hello bildirimleri yerel bildirimleri veya şablon bildirimleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="aad3a-109">hello notifications you send can be native notifications or template notifications.</span></span> <span data-ttu-id="aad3a-110">Yerel bildirimler hello yapılandırıldığı gibi belirli bildirim platform hedef `platform` hello özelliğinin çıkış bağlama.</span><span class="sxs-lookup"><span data-stu-id="aad3a-110">Native notifications target a specific notification platform as configured in hello `platform` property of hello output binding.</span></span> <span data-ttu-id="aad3a-111">Bir şablon bildirim kullanılan tootarget birden çok platform olabilir.</span><span class="sxs-lookup"><span data-stu-id="aad3a-111">A template notification can be used tootarget multiple platforms.</span></span>   

## <a name="notification-hub-output-binding-properties"></a><span data-ttu-id="aad3a-112">Bildirim hub'ı çıkış bağlama özellikleri</span><span class="sxs-lookup"><span data-stu-id="aad3a-112">Notification hub output binding properties</span></span>
<span data-ttu-id="aad3a-113">Merhaba function.json dosyası aşağıdaki özelliklere hello sağlar:</span><span class="sxs-lookup"><span data-stu-id="aad3a-113">hello function.json file provides hello following properties:</span></span>

* <span data-ttu-id="aad3a-114">`name`: İşlev kodu hello bildirim hub'ı iletisi için kullanılan değişken adı.</span><span class="sxs-lookup"><span data-stu-id="aad3a-114">`name` : Variable name used in function code for hello notification hub message.</span></span>
* <span data-ttu-id="aad3a-115">`type`: çok ayarlanmalıdır*"notificationHub"*.</span><span class="sxs-lookup"><span data-stu-id="aad3a-115">`type` : must be set too*"notificationHub"*.</span></span>
* <span data-ttu-id="aad3a-116">`tagExpression`: Etiket ifadeleri hello etiketi ifadeyle eşleşecek tooreceive bildirimleri kaydolan cihazlar tooa kümesi bildirimleri teslim edilmesi toospecify izin verin.</span><span class="sxs-lookup"><span data-stu-id="aad3a-116">`tagExpression` : Tag expressions allow you toospecify that notifications be delivered tooa set of devices who have registered tooreceive notifications that match hello tag expression.</span></span>  <span data-ttu-id="aad3a-117">Daha fazla bilgi için bkz: [Yönlendirme ve etiket ifadeleri](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="aad3a-117">For more information, see [Routing and tag expressions](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span></span>
* <span data-ttu-id="aad3a-118">`hubName`: Hello bildirim hub'ı kaynak hello Azure portal'ın adı.</span><span class="sxs-lookup"><span data-stu-id="aad3a-118">`hubName` : Name of hello notification hub resource in hello Azure portal.</span></span>
* <span data-ttu-id="aad3a-119">`connection`: Bu bağlantı dizesi olmalıdır bir **uygulama ayarı** bağlantı dizesini ayarlamak toohello *DefaultFullSharedAccessSignature* bildirim hub'ınız için değer.</span><span class="sxs-lookup"><span data-stu-id="aad3a-119">`connection` : This connection string must be an **Application Setting** connection string set toohello *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
* <span data-ttu-id="aad3a-120">`direction`: çok ayarlanmalıdır*"out"*.</span><span class="sxs-lookup"><span data-stu-id="aad3a-120">`direction` : must be set too*"out"*.</span></span> 
* <span data-ttu-id="aad3a-121">`platform`: hello platform özelliği hello bildirim platform bildirim hedeflerinizi gösterir.</span><span class="sxs-lookup"><span data-stu-id="aad3a-121">`platform` : hello platform property indicates hello notification platform your notification targets.</span></span> <span data-ttu-id="aad3a-122">Değerleri aşağıdaki hello biri olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="aad3a-122">Must be one of hello following values:</span></span>
  * <span data-ttu-id="aad3a-123">Merhaba platform özelliği bağlama, hello çıktısını atlanırsa, varsayılan olarak, herhangi bir platform hello Azure bildirim hub'ı üzerinde yapılandırılmış kullanılan tootarget şablon bildirimleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="aad3a-123">By default, if hello platform property is omitted from hello output binding, template notifications can be used tootarget any platform configured on hello Azure Notification Hub.</span></span> <span data-ttu-id="aad3a-124">Toosend platform bildirimleri ile Azure bildirim Hub'bir çapraz şablonları genel olarak kullanma hakkında daha fazla bilgi için bkz: [şablonları](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="aad3a-124">For more information on using templates in general toosend cross platform notifications with an Azure Notification Hub, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>
  * <span data-ttu-id="aad3a-125">`apns`: Apple anında bildirim hizmeti.</span><span class="sxs-lookup"><span data-stu-id="aad3a-125">`apns` : Apple Push Notification Service.</span></span> <span data-ttu-id="aad3a-126">APNS için hello bildirim hub'ı yapılandırma ve bir istemci uygulamasında hello bildirim alma hakkında daha fazla bilgi için bkz: [Azure Notification Hubs ile anında iletme bildirimleri tooiOS gönderme](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="aad3a-126">For more information on configuring hello notification hub for APNS and receiving hello notification in a client app, see [Sending push notifications tooiOS with Azure Notification Hubs](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span></span> 
  * <span data-ttu-id="aad3a-127">`adm`: [Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span><span class="sxs-lookup"><span data-stu-id="aad3a-127">`adm` : [Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span></span> <span data-ttu-id="aad3a-128">ADM için hello bildirim hub'ı yapılandırma ve bir Kindle uygulaması hello bildirim alma hakkında daha fazla bilgi için bkz: [Kindle uygulamaları için Notification Hubs ile çalışmaya başlama](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span><span class="sxs-lookup"><span data-stu-id="aad3a-128">For more information on configuring hello notification hub for ADM and receiving hello notification in a Kindle app, see [Getting Started with Notification Hubs for Kindle apps](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span></span> 
  * <span data-ttu-id="aad3a-129">`gcm`: [Google Cloud Messaging'i](https://developers.google.com/cloud-messaging/).</span><span class="sxs-lookup"><span data-stu-id="aad3a-129">`gcm` : [Google Cloud Messaging](https://developers.google.com/cloud-messaging/).</span></span> <span data-ttu-id="aad3a-130">Firebase bulut GCM hello yeni sürümü olan ileti, da desteklenir.</span><span class="sxs-lookup"><span data-stu-id="aad3a-130">Firebase Cloud Messaging, which is hello new version of GCM, is also supported.</span></span> <span data-ttu-id="aad3a-131">GCM/FCM hello bildirim hub'ı yapılandırma ve bir Android istemci uygulamasını hello bildirim alma hakkında daha fazla bilgi için bkz: [Azure Notification Hubs ile anında iletme bildirimleri tooAndroid gönderme](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="aad3a-131">For more information on configuring hello notification hub for GCM/FCM and receiving hello notification in an Android client app, see [Sending push notifications tooAndroid with Azure Notification Hubs](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span></span>
  * <span data-ttu-id="aad3a-132">`wns`: [Windows anında bildirim Hizmetleri](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) Windows platformları hedefleme.</span><span class="sxs-lookup"><span data-stu-id="aad3a-132">`wns` : [Windows Push Notification Services](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) targeting Windows platforms.</span></span> <span data-ttu-id="aad3a-133">Windows Phone 8.1 ve üzeri WNS tarafından da desteklenir.</span><span class="sxs-lookup"><span data-stu-id="aad3a-133">Windows Phone 8.1 and later is also supported by WNS.</span></span> <span data-ttu-id="aad3a-134">WNS için hello bildirim hub'ı yapılandırma ve bir evrensel Windows Platformu (UWP) uygulamasını hello bildirim alma hakkında daha fazla bilgi için bkz: [uygulamaları için Notification Hubs Windows Evrensel Platform ile çalışmaya başlama](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span><span class="sxs-lookup"><span data-stu-id="aad3a-134">For more information on configuring hello notification hub for WNS and receiving hello notification in a Universal Windows Platform (UWP) app, see [Getting started with Notification Hubs for Windows Universal Platform Apps](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span></span>
  * <span data-ttu-id="aad3a-135">`mpns`: [Microsoft anında bildirim hizmeti](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span><span class="sxs-lookup"><span data-stu-id="aad3a-135">`mpns` : [Microsoft Push Notification Service](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span></span> <span data-ttu-id="aad3a-136">Bu platform, Windows Phone 8 ve daha önceki Windows Phone platformlarını destekler.</span><span class="sxs-lookup"><span data-stu-id="aad3a-136">This platform supports Windows Phone 8 and earlier Windows Phone platforms.</span></span> <span data-ttu-id="aad3a-137">MPNS için hello bildirim hub'ı yapılandırma ve bir Windows Phone Uygulama hello bildirim alma hakkında daha fazla bilgi için bkz: [Windows Phone üzerinde Azure Notification Hubs ile anında iletme bildirimleri gönderme](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span><span class="sxs-lookup"><span data-stu-id="aad3a-137">For more information on configuring hello notification hub for MPNS and receiving hello notification in a Windows Phone app, see [Sending push notifications with Azure Notification Hubs on Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span></span>

<span data-ttu-id="aad3a-138">Örnek function.json:</span><span class="sxs-lookup"><span data-stu-id="aad3a-138">Example function.json:</span></span>

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

## <a name="notification-hub-connection-string-setup"></a><span data-ttu-id="aad3a-139">Bildirim hub'ı bağlantı dizesi kurulumu</span><span class="sxs-lookup"><span data-stu-id="aad3a-139">Notification hub connection string setup</span></span>
<span data-ttu-id="aad3a-140">bağlama toouse bir bildirim hub'ı çıktı, hello bağlantı dizesi hello hub için yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="aad3a-140">toouse a Notification hub output binding, you must configure hello connection string for hello hub.</span></span> <span data-ttu-id="aad3a-141">Bu hello üzerinde yapılabilir *tümleştirme* , bildirim hub'ı seçerek veya yenisini oluşturarak sekmesi.</span><span class="sxs-lookup"><span data-stu-id="aad3a-141">This can be done on hello *Integrate* tab by selecting your notification hub or creating a new one.</span></span> 

<span data-ttu-id="aad3a-142">Hello için bir bağlantı dizesi ekleyerek bir bağlantı dizesi olan bir hub'ınız için el ile de ekleyebilirsiniz *DefaultFullSharedAccessSignature* tooyour bildirim hub'ı.</span><span class="sxs-lookup"><span data-stu-id="aad3a-142">You can also manually add a connection string for an existing hub by adding a connection string for hello *DefaultFullSharedAccessSignature* tooyour notification hub.</span></span> <span data-ttu-id="aad3a-143">Bu bağlantı dizesi, işlevi erişim izni toosend bildirim iletilerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="aad3a-143">This connection string provides your function access permission toosend notification messages.</span></span> <span data-ttu-id="aad3a-144">Merhaba *DefaultFullSharedAccessSignature* hello bağlantı dizesi değeri erişilebilir **anahtarları** hello ana dikey penceresinde hello Azure portal, bildirim hub'ı kaynağın düğmesi.</span><span class="sxs-lookup"><span data-stu-id="aad3a-144">hello *DefaultFullSharedAccessSignature* connection string value can be accessed from hello **keys** button in hello main blade of your notification hub resource in hello Azure portal.</span></span> <span data-ttu-id="aad3a-145">toomanually hub'ınız için aşağıdaki adımları kullanın hello bir bağlantı dizesi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="aad3a-145">toomanually add a connection string for your hub, use hello following steps:</span></span> 

1. <span data-ttu-id="aad3a-146">Merhaba üzerinde **işlev uygulaması** hello Azure portal dikey tıklayın **işlev uygulama ayarları > tooApp hizmeti ayarlarına Git**.</span><span class="sxs-lookup"><span data-stu-id="aad3a-146">On hello **Function app** blade of hello Azure portal, click **Function App Settings > Go tooApp Service settings**.</span></span>
2. <span data-ttu-id="aad3a-147">Merhaba, **ayarları** dikey penceresinde tıklatın **uygulama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="aad3a-147">In hello **Settings** blade, click **Application Settings**.</span></span>
3. <span data-ttu-id="aad3a-148">Toohello aşağı **uygulama ayarları** bölüm ve bir adlandırılmış girişi ile eklemek *DefaultFullSharedAccessSignature* bildirim hub'ınız için değer.</span><span class="sxs-lookup"><span data-stu-id="aad3a-148">Scroll down toohello **App settings** section, and add a named entry for *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
4. <span data-ttu-id="aad3a-149">Çıktı bağlamaları hello ayar dize adı uygulamanızı başvuru.</span><span class="sxs-lookup"><span data-stu-id="aad3a-149">Reference your App setting string name in hello output bindings.</span></span> <span data-ttu-id="aad3a-150">Benzer çok**MyHubConnectionString** hello yukarıdaki örnekte kullanılan.</span><span class="sxs-lookup"><span data-stu-id="aad3a-150">Similar too**MyHubConnectionString** used in hello example above.</span></span>

## <a name="apns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="aad3a-151">C# queue tetikleyicileri ile APNS yerel bildirimleri</span><span class="sxs-lookup"><span data-stu-id="aad3a-151">APNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="aad3a-152">Bu örnek nasıl toouse türleri hello tanımlanan gösterir [Microsoft Azure bildirim hub'ları Kitaplığı](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend yerel APNS bildirim.</span><span class="sxs-lookup"><span data-stu-id="aad3a-152">This example shows how toouse types defined in hello [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend a native APNS notification.</span></span> 

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

## <a name="gcm-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="aad3a-153">C# queue tetikleyicileri ile GCM yerel bildirimleri</span><span class="sxs-lookup"><span data-stu-id="aad3a-153">GCM native notifications with C# queue triggers</span></span>
<span data-ttu-id="aad3a-154">Bu örnek nasıl toouse türleri hello tanımlanan gösterir [Microsoft Azure bildirim hub'ları Kitaplığı](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend yerel GCM bildirim.</span><span class="sxs-lookup"><span data-stu-id="aad3a-154">This example shows how toouse types defined in hello [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend a native GCM notification.</span></span> 

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

## <a name="wns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="aad3a-155">C# queue tetikleyicileri ile WNS yerel bildirimleri</span><span class="sxs-lookup"><span data-stu-id="aad3a-155">WNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="aad3a-156">Bu örnek nasıl toouse türleri hello tanımlanan gösterir [Microsoft Azure bildirim hub'ları Kitaplığı](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend yerel WNS kutlayın bildirim.</span><span class="sxs-lookup"><span data-stu-id="aad3a-156">This example shows how toouse types defined in hello [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) toosend a native WNS toast notification.</span></span> 

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

## <a name="template-example-for-nodejs-timer-triggers"></a><span data-ttu-id="aad3a-157">Şablon örneği için Node.js Zamanlayıcı Tetikleyicileri</span><span class="sxs-lookup"><span data-stu-id="aad3a-157">Template example for Node.js timer triggers</span></span>
<span data-ttu-id="aad3a-158">Bu örnek, bir bildirim gönderir bir [şablonu kayıt](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) içeren `location` ve `message`.</span><span class="sxs-lookup"><span data-stu-id="aad3a-158">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

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

## <a name="template-example-for-f-timer-triggers"></a><span data-ttu-id="aad3a-159">F # Zamanlayıcı Tetikleyicileri şablon Örneğin</span><span class="sxs-lookup"><span data-stu-id="aad3a-159">Template example for F# timer triggers</span></span>
<span data-ttu-id="aad3a-160">Bu örnek, bir bildirim gönderir bir [şablonu kayıt](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) içeren `location` ve `message`.</span><span class="sxs-lookup"><span data-stu-id="aad3a-160">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

```fsharp
let Run(myTimer: TimerInfo, notification: byref<IDictionary<string, string>>) =
    notification = dict [("location", "Redmond"); ("message", "Hello from F#!")]
```

## <a name="template-example-using-an-out-parameter"></a><span data-ttu-id="aad3a-161">Out parametresi kullanılarak şablon örneği</span><span class="sxs-lookup"><span data-stu-id="aad3a-161">Template example using an out parameter</span></span>
<span data-ttu-id="aad3a-162">Bu örnek, bir bildirim gönderir bir [şablonu kayıt](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) içeren bir `message` hello şablonunda yer tutucusu.</span><span class="sxs-lookup"><span data-stu-id="aad3a-162">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in hello template.</span></span>

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

## <a name="template-example-with-asynchronous-function"></a><span data-ttu-id="aad3a-163">Şablon örneği ile zaman uyumsuz işlevi</span><span class="sxs-lookup"><span data-stu-id="aad3a-163">Template example with asynchronous function</span></span>
<span data-ttu-id="aad3a-164">Zaman uyumsuz kod kullanıyorsanız, out Parametreleri izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="aad3a-164">If you are using asynchronous code, out parameters are not allowed.</span></span> <span data-ttu-id="aad3a-165">Bu durumda kullanarak `IAsyncCollector` tooreturn, şablon bildirim.</span><span class="sxs-lookup"><span data-stu-id="aad3a-165">In this case use `IAsyncCollector` tooreturn your template notification.</span></span> <span data-ttu-id="aad3a-166">Merhaba aşağıdaki kodu zaman uyumsuz yukarıdaki hello kod örneğidir.</span><span class="sxs-lookup"><span data-stu-id="aad3a-166">hello following code is an asynchronous example of hello code above.</span></span> 

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

## <a name="template-example-using-json"></a><span data-ttu-id="aad3a-167">JSON kullanarak şablon örneği</span><span class="sxs-lookup"><span data-stu-id="aad3a-167">Template example using JSON</span></span>
<span data-ttu-id="aad3a-168">Bu örnek, bir bildirim gönderir bir [şablonu kayıt](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) içeren bir `message` kullanarak geçerli bir JSON dizesi hello şablonunda yer tutucusu.</span><span class="sxs-lookup"><span data-stu-id="aad3a-168">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in hello template using a valid JSON string.</span></span>

```cs
using System;

public static void Run(string myQueueItem,  out string notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = "{\"message\":\"Hello from C#. Processed a queue item!\"}";
}
```

## <a name="template-example-using-notification-hubs-library-types"></a><span data-ttu-id="aad3a-169">Şablon örneği bildirim hub'ları kitaplığı türleri kullanma</span><span class="sxs-lookup"><span data-stu-id="aad3a-169">Template example using Notification Hubs library types</span></span>
<span data-ttu-id="aad3a-170">Bu örnek nasıl toouse türleri hello tanımlanan gösterir [Microsoft Azure bildirim hub'ları Kitaplığı](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="aad3a-170">This example shows how toouse types defined in hello [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="aad3a-171">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="aad3a-171">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

