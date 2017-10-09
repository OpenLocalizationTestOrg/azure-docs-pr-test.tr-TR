---
title: "aaaSend platformlar arası bildirimleri toousers bildirim hub'ları (ASP.NET) ile"
description: "Bilgi nasıl tüm platformlar hedefleyen bir platform belirsiz bildirim tek bir istekte toouse bildirim hub'ları şablonları toosend."
services: notification-hubs
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 11d2131b-f683-47fd-a691-4cdfc696f62b
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: multiple
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: f105b871b809e739dd5c05ea819ad135e842ebb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="send-cross-platform-notifications-toousers-with-notification-hubs"></a>Platformlar arası bildirimleri toousers Notification Hubs ile gönderme
Merhaba önceki öğreticideki [Notification Hubs kullanıcılara bildirme], toopush bildirimleri tooall cihazların belirli kimliği doğrulanmış bir kullanıcı tarafından nasıl kayıtlı öğrendiniz. Bu öğreticide, birden çok istek gerekli toosend bildirim tooeach desteklenen istemci platformu yoktu. Bildirim hub'ları olanak veren şablonlarını destekler belirtin nasıl belirli bir aygıt tooreceive bildirimleri istemektedir. Bu, platformlar arası bildirimleri gönderme kolaylaştırır. Bu konuda gösterilir nasıl tek bir istekte, tüm platformlar hedefleyen bir platform belirsiz bildirim şablonları toosend tootake yararlanabilir. Şablonlar hakkında daha ayrıntılı bilgi için bkz: [Azure Notification Hubs'a genel bakış][Templates].
> [!IMPORTANT]
> Windows Phone projeleri 8.1 ve önceki Visual Studio 2017 kullanarak desteklenmez. Daha fazla bilgi için bkz. [Visual Studio 2017 Platform Desteği ve Uyumluluk](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).

> [!NOTE]
> Bildirim hub'ları sağlayan cihaz tooregister hello ile birden fazla şablon aynı etiketi. Bu durumda, her şablon için bir tane toohello aygıt etiketi içinde birden fazla bildirim sonuçları hedefleme gelen ileti teslim. Toodisplay hello gibi bir gösterge ve bir Windows mağazası uygulamasında bildirim olarak her ikisi birden çok görsel bildirimler aynı iletisinde bu sağlar.
> 
> 

Şablonları kullanarak toosend platformlar arası adımları bildirimleri aşağıdaki hello tamamlayın:

1. Merhaba Hello Visual Studio'da Çözüm Gezgini'nde, genişletin **denetleyicileri** klasörünü seçip açık hello RegisterController.cs dosya.
2. Hello Hello kod bloğunu bulun **Put** yeni bir kayıt oluşturur yöntemi Değiştir hello `switch` koddan hello ile içerik:
   
        switch (deviceUpdate.Platform)
        {
            case "mpns":
                var toastTemplate = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                    "<wp:Notification xmlns:wp=\"WPNotification\">" +
                       "<wp:Toast>" +
                            "<wp:Text1>$(message)</wp:Text1>" +
                       "</wp:Toast> " +
                    "</wp:Notification>";
                registration = new MpnsTemplateRegistrationDescription(deviceUpdate.Handle, toastTemplate);
                break;
            case "wns":
                toastTemplate = @"<toast><visual><binding template=""ToastText01""><text id=""1"">$(message)</text></binding></visual></toast>";
                registration = new WindowsTemplateRegistrationDescription(deviceUpdate.Handle, toastTemplate);
                break;
            case "apns":
                var alertTemplate = "{\"aps\":{\"alert\":\"$(message)\"}}";
                registration = new AppleTemplateRegistrationDescription(deviceUpdate.Handle, alertTemplate);
                break;
            case "gcm":
                var messageTemplate = "{\"data\":{\"message\":\"$(message)\"}}";
                registration = new GcmTemplateRegistrationDescription(deviceUpdate.Handle, messageTemplate);
                break;
            default:
                throw new HttpResponseException(HttpStatusCode.BadRequest);
        }
   
    Bu kod bir şablon kayıt yerel kaydını yerine hello platforma özgü yöntemi toocreate çağırır. Şablon kayıtlar yerel kayıtları türetilen olduğundan var olan kayıtlar değiştirilmedi.
3. Merhaba, **bildirimleri** denetleyicisi, Değiştir hello **sendNotification** koddan hello yöntemiyle:
   
        public async Task<HttpResponseMessage> Post()
        {
            var user = HttpContext.Current.User.Identity.Name;
            var userTag = "username:" + user;
   
            var notification = new Dictionary<string, string> { { "message", "Hello, " + user } };
            await Notifications.Instance.Hub.SendTemplateNotificationAsync(notification, userTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
    Bu kod tooall platformları bir bildirim gönderir, yerel bir yükü aynı zaman ve toospecify gerek kalmadan hello. Bildirim hub'ları derler ve sunar hello doğru yükü tooevery aygıt ile sağlanan hello *etiketi* kayıtlı hello şablonları belirtildiği gibi bir değer.
4. Webapı arka uç projeniz yeniden yayımlayın.
5. Merhaba istemci uygulamasını yeniden çalıştırın ve kayıt başarılı olduğunu doğrulayın.
6. (İsteğe bağlı) Merhaba istemci uygulaması tooa ikinci aygıt dağıtabilir, ardından hello uygulamayı çalıştırın.
   
    Bir bildirim her cihazda görüntülendiğine dikkat edin.

## <a name="next-steps"></a>Sonraki Adımlar
Bu öğreticiyi tamamladığınıza göre bildirim hub'ları ve bu konularda şablonları hakkında daha fazla bilgi:

* **[Bildirim hub'ları toosend son dakika haberleri kullanın]** <br/>Şablonları kullanarak başka bir senaryo gösterir
* **[Azure Notification Hubs'a genel bakış][Templates]**<br/>Genel Bakış konusunda daha ayrıntılı bilgiler şablonlarında.

<!-- Anchors. -->

<!-- Images. -->




<!-- URLs. -->
[Push toousers ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Push toousers Mobile Services]: /manage/services/notification-hubs/notify-users/
[Visual Studio 2012 Express for Windows 8]: http://go.microsoft.com/fwlink/?LinkId=257546

[Bildirim hub'ları toosend son dakika haberleri kullanın]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
[Azure Notification Hubs]: http://go.microsoft.com/fwlink/p/?LinkId=314257
[Notification Hubs kullanıcılara bildirme]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Templates]: http://go.microsoft.com/fwlink/p/?LinkId=317339
[Notification Hub How toofor Windows Store]: http://msdn.microsoft.com/library/windowsazure/jj927172.aspx
