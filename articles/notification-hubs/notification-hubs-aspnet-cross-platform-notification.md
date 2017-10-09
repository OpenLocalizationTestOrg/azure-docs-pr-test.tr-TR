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
# <a name="send-cross-platform-notifications-toousers-with-notification-hubs"></a><span data-ttu-id="6167b-103">Platformlar arası bildirimleri toousers Notification Hubs ile gönderme</span><span class="sxs-lookup"><span data-stu-id="6167b-103">Send cross-platform notifications toousers with Notification Hubs</span></span>
<span data-ttu-id="6167b-104">Merhaba önceki öğreticideki [Notification Hubs kullanıcılara bildirme], toopush bildirimleri tooall cihazların belirli kimliği doğrulanmış bir kullanıcı tarafından nasıl kayıtlı öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="6167b-104">In hello previous tutorial [Notify users with Notification Hubs], you learned how toopush notifications tooall devices registered by a specific authenticated user.</span></span> <span data-ttu-id="6167b-105">Bu öğreticide, birden çok istek gerekli toosend bildirim tooeach desteklenen istemci platformu yoktu.</span><span class="sxs-lookup"><span data-stu-id="6167b-105">In that tutorial, multiple requests were required toosend a notification tooeach supported client platform.</span></span> <span data-ttu-id="6167b-106">Bildirim hub'ları olanak veren şablonlarını destekler belirtin nasıl belirli bir aygıt tooreceive bildirimleri istemektedir.</span><span class="sxs-lookup"><span data-stu-id="6167b-106">Notification Hubs supports templates, which let you specify how a specific device wants tooreceive notifications.</span></span> <span data-ttu-id="6167b-107">Bu, platformlar arası bildirimleri gönderme kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="6167b-107">This simplifies sending cross-platform notifications.</span></span> <span data-ttu-id="6167b-108">Bu konuda gösterilir nasıl tek bir istekte, tüm platformlar hedefleyen bir platform belirsiz bildirim şablonları toosend tootake yararlanabilir.</span><span class="sxs-lookup"><span data-stu-id="6167b-108">This topic demonstrates how tootake advantage of templates toosend, in a single request, a platform-agnostic notification that targets all platforms.</span></span> <span data-ttu-id="6167b-109">Şablonlar hakkında daha ayrıntılı bilgi için bkz: [Azure Notification Hubs'a genel bakış][Templates].</span><span class="sxs-lookup"><span data-stu-id="6167b-109">For more detailed information about templates, see [Azure Notification Hubs Overview][Templates].</span></span>
> [!IMPORTANT]
> <span data-ttu-id="6167b-110">Windows Phone projeleri 8.1 ve önceki Visual Studio 2017 kullanarak desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="6167b-110">Windows Phone projects 8.1 and earlier are not supported using Visual Studio 2017.</span></span> <span data-ttu-id="6167b-111">Daha fazla bilgi için bkz. [Visual Studio 2017 Platform Desteği ve Uyumluluk](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="6167b-111">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span>

> [!NOTE]
> <span data-ttu-id="6167b-112">Bildirim hub'ları sağlayan cihaz tooregister hello ile birden fazla şablon aynı etiketi.</span><span class="sxs-lookup"><span data-stu-id="6167b-112">Notification Hubs allows a device tooregister multiple templates with hello same tag.</span></span> <span data-ttu-id="6167b-113">Bu durumda, her şablon için bir tane toohello aygıt etiketi içinde birden fazla bildirim sonuçları hedefleme gelen ileti teslim.</span><span class="sxs-lookup"><span data-stu-id="6167b-113">In this case, an incoming message targeting that tag results in multiple notifications delivered toohello device, one for each template.</span></span> <span data-ttu-id="6167b-114">Toodisplay hello gibi bir gösterge ve bir Windows mağazası uygulamasında bildirim olarak her ikisi birden çok görsel bildirimler aynı iletisinde bu sağlar.</span><span class="sxs-lookup"><span data-stu-id="6167b-114">This enables you toodisplay hello same message in multiple visual notifications, such as both as a badge and as a toast notification in a Windows Store app.</span></span>
> 
> 

<span data-ttu-id="6167b-115">Şablonları kullanarak toosend platformlar arası adımları bildirimleri aşağıdaki hello tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="6167b-115">Complete hello following steps toosend cross-platform notifications using templates:</span></span>

1. <span data-ttu-id="6167b-116">Merhaba Hello Visual Studio'da Çözüm Gezgini'nde, genişletin **denetleyicileri** klasörünü seçip açık hello RegisterController.cs dosya.</span><span class="sxs-lookup"><span data-stu-id="6167b-116">In hello Solution Explorer in Visual Studio, expand hello **Controllers** folder, then open hello RegisterController.cs file.</span></span>
2. <span data-ttu-id="6167b-117">Hello Hello kod bloğunu bulun **Put** yeni bir kayıt oluşturur yöntemi Değiştir hello `switch` koddan hello ile içerik:</span><span class="sxs-lookup"><span data-stu-id="6167b-117">Locate hello block of code in hello **Put** method that creates a new registration replace hello `switch` content with hello following code:</span></span>
   
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
   
    <span data-ttu-id="6167b-118">Bu kod bir şablon kayıt yerel kaydını yerine hello platforma özgü yöntemi toocreate çağırır.</span><span class="sxs-lookup"><span data-stu-id="6167b-118">This code calls hello platform-specific method toocreate a template registration instead of a native registration.</span></span> <span data-ttu-id="6167b-119">Şablon kayıtlar yerel kayıtları türetilen olduğundan var olan kayıtlar değiştirilmedi.</span><span class="sxs-lookup"><span data-stu-id="6167b-119">Existing registrations need not be modified because template registrations derive from native registrations.</span></span>
3. <span data-ttu-id="6167b-120">Merhaba, **bildirimleri** denetleyicisi, Değiştir hello **sendNotification** koddan hello yöntemiyle:</span><span class="sxs-lookup"><span data-stu-id="6167b-120">In hello **Notifications** controller, replace hello **sendNotification** method with hello following code:</span></span>
   
        public async Task<HttpResponseMessage> Post()
        {
            var user = HttpContext.Current.User.Identity.Name;
            var userTag = "username:" + user;
   
            var notification = new Dictionary<string, string> { { "message", "Hello, " + user } };
            await Notifications.Instance.Hub.SendTemplateNotificationAsync(notification, userTag);
   
            return Request.CreateResponse(HttpStatusCode.OK);
        }
   
    <span data-ttu-id="6167b-121">Bu kod tooall platformları bir bildirim gönderir, yerel bir yükü aynı zaman ve toospecify gerek kalmadan hello.</span><span class="sxs-lookup"><span data-stu-id="6167b-121">This code sends a notification tooall platforms at hello same time and without having toospecify a native payload.</span></span> <span data-ttu-id="6167b-122">Bildirim hub'ları derler ve sunar hello doğru yükü tooevery aygıt ile sağlanan hello *etiketi* kayıtlı hello şablonları belirtildiği gibi bir değer.</span><span class="sxs-lookup"><span data-stu-id="6167b-122">Notification Hubs builds and delivers hello correct payload tooevery device with hello provided *tag* value, as specified in hello registered templates.</span></span>
4. <span data-ttu-id="6167b-123">Webapı arka uç projeniz yeniden yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="6167b-123">Re-publish your WebApi back-end project.</span></span>
5. <span data-ttu-id="6167b-124">Merhaba istemci uygulamasını yeniden çalıştırın ve kayıt başarılı olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="6167b-124">Run hello client app again and verify that registration succeeds.</span></span>
6. <span data-ttu-id="6167b-125">(İsteğe bağlı) Merhaba istemci uygulaması tooa ikinci aygıt dağıtabilir, ardından hello uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6167b-125">(Optional) Deploy hello client app tooa second device, then run hello app.</span></span>
   
    <span data-ttu-id="6167b-126">Bir bildirim her cihazda görüntülendiğine dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="6167b-126">Note that a notification is displayed on each device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6167b-127">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="6167b-127">Next Steps</span></span>
<span data-ttu-id="6167b-128">Bu öğreticiyi tamamladığınıza göre bildirim hub'ları ve bu konularda şablonları hakkında daha fazla bilgi:</span><span class="sxs-lookup"><span data-stu-id="6167b-128">Now that you have completed this tutorial, find out more about Notification Hubs and templates in these topics:</span></span>

* <span data-ttu-id="6167b-129">**[Bildirim hub'ları toosend son dakika haberleri kullanın]**</span><span class="sxs-lookup"><span data-stu-id="6167b-129">**[Use Notification Hubs toosend breaking news]**</span></span> <br/><span data-ttu-id="6167b-130">Şablonları kullanarak başka bir senaryo gösterir</span><span class="sxs-lookup"><span data-stu-id="6167b-130">Demonstrates another scenario for using templates</span></span>
* <span data-ttu-id="6167b-131">**[Azure Notification Hubs'a genel bakış][Templates]**</span><span class="sxs-lookup"><span data-stu-id="6167b-131">**[Azure Notification Hubs Overview][Templates]**</span></span><br/><span data-ttu-id="6167b-132">Genel Bakış konusunda daha ayrıntılı bilgiler şablonlarında.</span><span class="sxs-lookup"><span data-stu-id="6167b-132">Overview topic has more detailed information on templates.</span></span>

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
