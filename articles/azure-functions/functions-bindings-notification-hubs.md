---
title: "Azure işlevleri bildirim hub'ı bağlama | Microsoft Docs"
description: "Azure bildirim hub'ı bağlama Azure işlevlerini kullanmak nasıl anlayın."
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
ms.openlocfilehash: fa3d37b963c1bb6b58127b9180cd657d7b1dabcc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-notification-hub-output-binding"></a><span data-ttu-id="a7ce8-104">Azure işlevleri bildirim hub'ı bağlama çıktı</span><span class="sxs-lookup"><span data-stu-id="a7ce8-104">Azure Functions Notification Hub output binding</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="a7ce8-105">Bu makalede nasıl yapılandırılacağı ve kod Azure bildirim hub'ı bağlamaları Azure işlevlerinde açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-105">This article explains how to configure and code Azure Notification Hub bindings in Azure Functions.</span></span> 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="a7ce8-106">İşlevlerinizi birkaç kod satırıyla, bir yapılandırılmış Azure bildirim hub'ı kullanarak anında iletme bildirimleri gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-106">Your functions can send push notifications using a configured Azure Notification Hub with a few lines of code.</span></span> <span data-ttu-id="a7ce8-107">Ancak, Azure bildirim hub'ı Platform Bildirim Hizmetleri (kullanmak istediğiniz PNS için) yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-107">However, the Azure Notification Hub must be configured for the Platform Notifications Services (PNS) you want to use.</span></span> <span data-ttu-id="a7ce8-108">Bir Azure bildirim hub'ı yapılandırma ve bildirimleri almak için kaydolun istemci uygulamaları geliştirme hakkında daha fazla bilgi için bkz: [Notification Hubs ile çalışmaya başlama](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) ve hedef istemci platformunuzu üst'ı tıklatın .</span><span class="sxs-lookup"><span data-stu-id="a7ce8-108">For more information on configuring an Azure Notification Hub and developing a client applications that register to receive notifications, see [Getting started with Notification Hubs](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) and click your target client platform at the top.</span></span>

<span data-ttu-id="a7ce8-109">Gönderdiğiniz bildirimleri yerel bildirimleri veya şablon bildirimleri olabilir.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-109">The notifications you send can be native notifications or template notifications.</span></span> <span data-ttu-id="a7ce8-110">Yerel bildirimler yapılandırılan belirli bildirim platform hedef `platform` çıkış bağlama özelliği.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-110">Native notifications target a specific notification platform as configured in the `platform` property of the output binding.</span></span> <span data-ttu-id="a7ce8-111">Bir şablon bildirim hedef birden çok platform için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-111">A template notification can be used to target multiple platforms.</span></span>   

## <a name="notification-hub-output-binding-properties"></a><span data-ttu-id="a7ce8-112">Bildirim hub'ı çıkış bağlama özellikleri</span><span class="sxs-lookup"><span data-stu-id="a7ce8-112">Notification hub output binding properties</span></span>
<span data-ttu-id="a7ce8-113">Function.json dosyası aşağıdaki özellikleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="a7ce8-113">The function.json file provides the following properties:</span></span>

* <span data-ttu-id="a7ce8-114">`name`: Bildirim hub'ı ileti için işlevi kod içinde kullanılan değişken adı.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-114">`name` : Variable name used in function code for the notification hub message.</span></span>
* <span data-ttu-id="a7ce8-115">`type`: ayarlanmalıdır *"notificationHub"*.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-115">`type` : must be set to *"notificationHub"*.</span></span>
* <span data-ttu-id="a7ce8-116">`tagExpression`: Etiket ifadeleri bildirimleri etiketi ifadeyle eşleşecek bildirimleri almak için kayıtlı cihazları kümesine teslim edilmesi belirtmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-116">`tagExpression` : Tag expressions allow you to specify that notifications be delivered to a set of devices who have registered to receive notifications that match the tag expression.</span></span>  <span data-ttu-id="a7ce8-117">Daha fazla bilgi için bkz: [Yönlendirme ve etiket ifadeleri](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="a7ce8-117">For more information, see [Routing and tag expressions](../notification-hubs/notification-hubs-tags-segment-push-message.md).</span></span>
* <span data-ttu-id="a7ce8-118">`hubName`: Azure Portalı'ndaki bildirim hub'ı kaynağının adı.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-118">`hubName` : Name of the notification hub resource in the Azure portal.</span></span>
* <span data-ttu-id="a7ce8-119">`connection`: Bu bağlantı dizesi olmalıdır bir **uygulama ayarı** bağlantı dizesini ayarlamak *DefaultFullSharedAccessSignature* bildirim hub'ınız için değer.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-119">`connection` : This connection string must be an **Application Setting** connection string set to the *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
* <span data-ttu-id="a7ce8-120">`direction`: ayarlanmalıdır *"out"*.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-120">`direction` : must be set to *"out"*.</span></span> 
* <span data-ttu-id="a7ce8-121">`platform`: Platform özelliği bildirim platform bildirim hedeflerinizi gösterir.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-121">`platform` : The platform property indicates the notification platform your notification targets.</span></span> <span data-ttu-id="a7ce8-122">Aşağıdaki değerlerden biri olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="a7ce8-122">Must be one of the following values:</span></span>
  * <span data-ttu-id="a7ce8-123">Platform özellik çıkış bağlamanın dışında atlanırsa varsayılan olarak, şablon bildirim Azure bildirim hub'ına yapılandırılmış herhangi bir platform hedeflemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-123">By default, if the platform property is omitted from the output binding, template notifications can be used to target any platform configured on the Azure Notification Hub.</span></span> <span data-ttu-id="a7ce8-124">Çapraz bir Azure bildirim hub'ı ile platform bildirimleri göndermek için genel şablonları kullanma hakkında daha fazla bilgi için bkz: [şablonları](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="a7ce8-124">For more information on using templates in general to send cross platform notifications with an Azure Notification Hub, see [Templates](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md).</span></span>
  * <span data-ttu-id="a7ce8-125">`apns`: Apple anında bildirim hizmeti.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-125">`apns` : Apple Push Notification Service.</span></span> <span data-ttu-id="a7ce8-126">APNS için bildirim hub'ı yapılandırma ve bir istemci uygulamasında bildirim alma hakkında daha fazla bilgi için bkz: [Azure Notification Hubs ile ios'a gönderme anında iletme bildirimleri](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="a7ce8-126">For more information on configuring the notification hub for APNS and receiving the notification in a client app, see [Sending push notifications to iOS with Azure Notification Hubs](../notification-hubs/notification-hubs-ios-apple-push-notification-apns-get-started.md)</span></span> 
  * <span data-ttu-id="a7ce8-127">`adm`: [Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span><span class="sxs-lookup"><span data-stu-id="a7ce8-127">`adm` : [Amazon Device Messaging](https://developer.amazon.com/device-messaging).</span></span> <span data-ttu-id="a7ce8-128">ADM için bildirim hub'ı yapılandırma ve bir Kindle uygulaması bildirim alma hakkında daha fazla bilgi için bkz: [Kindle uygulamaları için Notification Hubs ile çalışmaya başlama](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span><span class="sxs-lookup"><span data-stu-id="a7ce8-128">For more information on configuring the notification hub for ADM and receiving the notification in a Kindle app, see [Getting Started with Notification Hubs for Kindle apps](../notification-hubs/notification-hubs-kindle-amazon-adm-push-notification.md)</span></span> 
  * <span data-ttu-id="a7ce8-129">`gcm`: [Google Cloud Messaging'i](https://developers.google.com/cloud-messaging/).</span><span class="sxs-lookup"><span data-stu-id="a7ce8-129">`gcm` : [Google Cloud Messaging](https://developers.google.com/cloud-messaging/).</span></span> <span data-ttu-id="a7ce8-130">Firebase bulut GCM yeni sürümü olan ileti, da desteklenir.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-130">Firebase Cloud Messaging, which is the new version of GCM, is also supported.</span></span> <span data-ttu-id="a7ce8-131">GCM/FCM için bildirim hub'ı yapılandırma ve bir Android istemci uygulamasını bildirim alma hakkında daha fazla bilgi için bkz: [Azure Notification Hubs ile android'e gönderme anında iletme bildirimleri](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="a7ce8-131">For more information on configuring the notification hub for GCM/FCM and receiving the notification in an Android client app, see [Sending push notifications to Android with Azure Notification Hubs](../notification-hubs/notification-hubs-android-push-notification-google-fcm-get-started.md)</span></span>
  * <span data-ttu-id="a7ce8-132">`wns`: [Windows anında bildirim Hizmetleri](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) Windows platformları hedefleme.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-132">`wns` : [Windows Push Notification Services](https://msdn.microsoft.com/en-us/windows/uwp/controls-and-patterns/tiles-and-notifications-windows-push-notification-services--wns--overview) targeting Windows platforms.</span></span> <span data-ttu-id="a7ce8-133">Windows Phone 8.1 ve üzeri WNS tarafından da desteklenir.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-133">Windows Phone 8.1 and later is also supported by WNS.</span></span> <span data-ttu-id="a7ce8-134">WNS için bildirim hub'ı yapılandırma ve bir evrensel Windows Platformu (UWP) uygulamasını bildirim alma hakkında daha fazla bilgi için bkz: [uygulamaları için Notification Hubs Windows Evrensel Platform ile çalışmaya başlama](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span><span class="sxs-lookup"><span data-stu-id="a7ce8-134">For more information on configuring the notification hub for WNS and receiving the notification in a Universal Windows Platform (UWP) app, see [Getting started with Notification Hubs for Windows Universal Platform Apps](../notification-hubs/notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md)</span></span>
  * <span data-ttu-id="a7ce8-135">`mpns`: [Microsoft anında bildirim hizmeti](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span><span class="sxs-lookup"><span data-stu-id="a7ce8-135">`mpns` : [Microsoft Push Notification Service](https://msdn.microsoft.com/en-us/library/windows/apps/ff402558.aspx).</span></span> <span data-ttu-id="a7ce8-136">Bu platform, Windows Phone 8 ve daha önceki Windows Phone platformlarını destekler.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-136">This platform supports Windows Phone 8 and earlier Windows Phone platforms.</span></span> <span data-ttu-id="a7ce8-137">MPNS için bildirim hub'ı yapılandırma ve bir Windows Phone uygulama bildirim alma hakkında daha fazla bilgi için bkz: [Windows Phone üzerinde Azure Notification Hubs ile anında iletme bildirimleri gönderme](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span><span class="sxs-lookup"><span data-stu-id="a7ce8-137">For more information on configuring the notification hub for MPNS and receiving the notification in a Windows Phone app, see [Sending push notifications with Azure Notification Hubs on Windows Phone](../notification-hubs/notification-hubs-windows-mobile-push-notifications-mpns.md)</span></span>

<span data-ttu-id="a7ce8-138">Örnek function.json:</span><span class="sxs-lookup"><span data-stu-id="a7ce8-138">Example function.json:</span></span>

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

## <a name="notification-hub-connection-string-setup"></a><span data-ttu-id="a7ce8-139">Bildirim hub'ı bağlantı dizesi kurulumu</span><span class="sxs-lookup"><span data-stu-id="a7ce8-139">Notification hub connection string setup</span></span>
<span data-ttu-id="a7ce8-140">Bağlama bildirim hub'ı çıkışı kullanmak için bağlantı dizesi hub için yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-140">To use a Notification hub output binding, you must configure the connection string for the hub.</span></span> <span data-ttu-id="a7ce8-141">Bu, üzerinde yapılabilir *tümleştirme* , bildirim hub'ı seçerek veya yenisini oluşturarak sekmesi.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-141">This can be done on the *Integrate* tab by selecting your notification hub or creating a new one.</span></span> 

<span data-ttu-id="a7ce8-142">Var olan bir hub için bir bağlantı dizesi için bir bağlantı dizesi ekleyerek el ile de ekleyebilirsiniz *DefaultFullSharedAccessSignature* bildirim hub'ınıza.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-142">You can also manually add a connection string for an existing hub by adding a connection string for the *DefaultFullSharedAccessSignature* to your notification hub.</span></span> <span data-ttu-id="a7ce8-143">Bu bağlantı dizesi, bildirim iletilerini göndermek için işlevi erişim izniniz sağlar.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-143">This connection string provides your function access permission to send notification messages.</span></span> <span data-ttu-id="a7ce8-144">*DefaultFullSharedAccessSignature* bağlantı dizesi değeri, gelen erişilebilir **anahtarları** bildirim hub'ı kaynağınız Azure Portalı'ndaki ana dikey düğmesini.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-144">The *DefaultFullSharedAccessSignature* connection string value can be accessed from the **keys** button in the main blade of your notification hub resource in the Azure portal.</span></span> <span data-ttu-id="a7ce8-145">El ile hub'ınız için bir bağlantı dizesi eklemek için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="a7ce8-145">To manually add a connection string for your hub, use the following steps:</span></span> 

1. <span data-ttu-id="a7ce8-146">Üzerinde **işlev uygulaması** Azure portalı dikey tıklayın **işlev uygulama ayarları > uygulama hizmeti ayarlarına Git**.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-146">On the **Function app** blade of the Azure portal, click **Function App Settings > Go to App Service settings**.</span></span>
2. <span data-ttu-id="a7ce8-147">İçinde **ayarları** dikey penceresinde tıklatın **uygulama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-147">In the **Settings** blade, click **Application Settings**.</span></span>
3. <span data-ttu-id="a7ce8-148">Ekranı aşağı kaydırarak **uygulama ayarları** bölüm ve bir adlandırılmış girişi ile eklemek *DefaultFullSharedAccessSignature* bildirim hub'ınız için değer.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-148">Scroll down to the **App settings** section, and add a named entry for *DefaultFullSharedAccessSignature* value for your notification hub.</span></span>
4. <span data-ttu-id="a7ce8-149">Uygulama ayarı dize adınızı çıkış bağlamaları başvuru.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-149">Reference your App setting string name in the output bindings.</span></span> <span data-ttu-id="a7ce8-150">Benzer şekilde **MyHubConnectionString** yukarıdaki örnekte kullanılan.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-150">Similar to **MyHubConnectionString** used in the example above.</span></span>

## <a name="apns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="a7ce8-151">C# queue tetikleyicileri ile APNS yerel bildirimleri</span><span class="sxs-lookup"><span data-stu-id="a7ce8-151">APNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="a7ce8-152">Bu örnek tanımlanan türleri kullanmayı gösterir [Microsoft Azure bildirim hub'ları Kitaplığı](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) yerel APNS bildirim göndermek için.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-152">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native APNS notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The JSON format for a native APNS notification is ...
    // { "aps": { "alert": "notification message" }}  

    log.Info($"Sending APNS notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string apnsNotificationPayload = "{\"aps\": {\"alert\": \"A new user wants to be added (" + 
                                        user.name + ")\" }}";
    log.Info($"{apnsNotificationPayload}");
    await notification.AddAsync(new AppleNotification(apnsNotificationPayload));        
}
```

## <a name="gcm-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="a7ce8-153">C# queue tetikleyicileri ile GCM yerel bildirimleri</span><span class="sxs-lookup"><span data-stu-id="a7ce8-153">GCM native notifications with C# queue triggers</span></span>
<span data-ttu-id="a7ce8-154">Bu örnek tanımlanan türleri kullanmayı gösterir [Microsoft Azure bildirim hub'ları Kitaplığı](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) yerel GCM bildirim göndermek için.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-154">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native GCM notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The JSON format for a native GCM notification is ...
    // { "data": { "message": "notification message" }}  

    log.Info($"Sending GCM notification of a new user");    
    dynamic user = JsonConvert.DeserializeObject(myQueueItem);    
    string gcmNotificationPayload = "{\"data\": {\"message\": \"A new user wants to be added (" + 
                                        user.name + ")\" }}";
    log.Info($"{gcmNotificationPayload}");
    await notification.AddAsync(new GcmNotification(gcmNotificationPayload));        
}
```

## <a name="wns-native-notifications-with-c-queue-triggers"></a><span data-ttu-id="a7ce8-155">C# queue tetikleyicileri ile WNS yerel bildirimleri</span><span class="sxs-lookup"><span data-stu-id="a7ce8-155">WNS native notifications with C# queue triggers</span></span>
<span data-ttu-id="a7ce8-156">Bu örnek tanımlanan türleri kullanmayı gösterir [Microsoft Azure bildirim hub'ları Kitaplığı](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) yerel WNS bildirim göndermek için.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-156">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) to send a native WNS toast notification.</span></span> 

```cs
#r "Microsoft.Azure.NotificationHubs"
#r "Newtonsoft.Json"

using System;
using Microsoft.Azure.NotificationHubs;
using Newtonsoft.Json;

public static async Task Run(string myQueueItem, IAsyncCollector<Notification> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a new user to be processed in the form of a JSON string with 
    // a "name" value.
    //
    // The XML format for a native WNS toast notification is ...
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
                                            "A new user wants to be added (" + user.name + ")" + 
                                        "</text>" +
                                    "</binding></visual></toast>";

    log.Info($"{wnsNotificationPayload}");
    await notification.AddAsync(new WindowsNotification(wnsNotificationPayload));        
}
```

## <a name="template-example-for-nodejs-timer-triggers"></a><span data-ttu-id="a7ce8-157">Şablon örneği için Node.js Zamanlayıcı Tetikleyicileri</span><span class="sxs-lookup"><span data-stu-id="a7ce8-157">Template example for Node.js timer triggers</span></span>
<span data-ttu-id="a7ce8-158">Bu örnek, bir bildirim gönderir bir [şablonu kayıt](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) içeren `location` ve `message`.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-158">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

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

## <a name="template-example-for-f-timer-triggers"></a><span data-ttu-id="a7ce8-159">F # Zamanlayıcı Tetikleyicileri şablon Örneğin</span><span class="sxs-lookup"><span data-stu-id="a7ce8-159">Template example for F# timer triggers</span></span>
<span data-ttu-id="a7ce8-160">Bu örnek, bir bildirim gönderir bir [şablonu kayıt](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) içeren `location` ve `message`.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-160">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains `location` and `message`.</span></span>

```fsharp
let Run(myTimer: TimerInfo, notification: byref<IDictionary<string, string>>) =
    notification = dict [("location", "Redmond"); ("message", "Hello from F#!")]
```

## <a name="template-example-using-an-out-parameter"></a><span data-ttu-id="a7ce8-161">Out parametresi kullanılarak şablon örneği</span><span class="sxs-lookup"><span data-stu-id="a7ce8-161">Template example using an out parameter</span></span>
<span data-ttu-id="a7ce8-162">Bu örnek, bir bildirim gönderir bir [şablonu kayıt](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) içeren bir `message` şablonunda yer tutucusu.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-162">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in the template.</span></span>

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

## <a name="template-example-with-asynchronous-function"></a><span data-ttu-id="a7ce8-163">Şablon örneği ile zaman uyumsuz işlevi</span><span class="sxs-lookup"><span data-stu-id="a7ce8-163">Template example with asynchronous function</span></span>
<span data-ttu-id="a7ce8-164">Zaman uyumsuz kod kullanıyorsanız, out Parametreleri izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-164">If you are using asynchronous code, out parameters are not allowed.</span></span> <span data-ttu-id="a7ce8-165">Bu durumda kullanarak `IAsyncCollector` , şablon bildirim dönün.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-165">In this case use `IAsyncCollector` to return your template notification.</span></span> <span data-ttu-id="a7ce8-166">Aşağıdaki kod, yukarıdaki kod zaman uyumsuz bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-166">The following code is an asynchronous example of the code above.</span></span> 

```cs
using System;
using System.Threading.Tasks;
using System.Collections.Generic;

public static async Task Run(string myQueueItem, IAsyncCollector<IDictionary<string,string>> notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    log.Info($"Sending Template Notification to Notification Hub");
    await notification.AddAsync(GetTemplateProperties(myQueueItem));    
}

private static IDictionary<string, string> GetTemplateProperties(string message)
{
    Dictionary<string, string> templateProperties = new Dictionary<string, string>();
    templateProperties["user"] = "A new user wants to be added : " + message;
    return templateProperties;
}
```

## <a name="template-example-using-json"></a><span data-ttu-id="a7ce8-167">JSON kullanarak şablon örneği</span><span class="sxs-lookup"><span data-stu-id="a7ce8-167">Template example using JSON</span></span>
<span data-ttu-id="a7ce8-168">Bu örnek, bir bildirim gönderir bir [şablonu kayıt](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) içeren bir `message` kullanarak geçerli bir JSON dizesi şablonunda yer tutucusu.</span><span class="sxs-lookup"><span data-stu-id="a7ce8-168">This example sends a notification for a [template registration](../notification-hubs/notification-hubs-templates-cross-platform-push-messages.md) that contains a `message` place holder in the template using a valid JSON string.</span></span>

```cs
using System;

public static void Run(string myQueueItem,  out string notification, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    notification = "{\"message\":\"Hello from C#. Processed a queue item!\"}";
}
```

## <a name="template-example-using-notification-hubs-library-types"></a><span data-ttu-id="a7ce8-169">Şablon örneği bildirim hub'ları kitaplığı türleri kullanma</span><span class="sxs-lookup"><span data-stu-id="a7ce8-169">Template example using Notification Hubs library types</span></span>
<span data-ttu-id="a7ce8-170">Bu örnek tanımlanan türleri kullanmayı gösterir [Microsoft Azure bildirim hub'ları Kitaplığı](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="a7ce8-170">This example shows how to use types defined in the [Microsoft Azure Notification Hubs Library](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span> 

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

## <a name="next-steps"></a><span data-ttu-id="a7ce8-171">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a7ce8-171">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

