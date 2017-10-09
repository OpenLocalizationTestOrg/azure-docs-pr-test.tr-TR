---
title: aaaRouting ve etiket ifadeleri
description: "Bu konu Azure bildirim hub'ları için Yönlendirme ve etiket ifadeleri açıklar."
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: 0fffb3bb-8ed8-4e0f-89e8-0de24a47f644
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: c2c60500f7469f1cb1a73a5cf63c221a9ad6cbb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="routing-and-tag-expressions"></a><span data-ttu-id="6f093-103">Yönlendirme ve etiket ifadeleri</span><span class="sxs-lookup"><span data-stu-id="6f093-103">Routing and tag expressions</span></span>
## <a name="overview"></a><span data-ttu-id="6f093-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="6f093-104">Overview</span></span>
<span data-ttu-id="6f093-105">Etiket ifadeleri cihazlar ya da daha açık belirtmek gerekirse kayıtlar, belirli kümelerini tootarget, bildirim hub'ları üzerinden bir anında iletme bildirimi gönderirken etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="6f093-105">Tag expressions enable you tootarget specific sets of devices, or more specifically registrations, when sending a push notification through Notification Hubs.</span></span>

## <a name="targeting-specific-registrations"></a><span data-ttu-id="6f093-106">Belirli kayıtları hedefleme</span><span class="sxs-lookup"><span data-stu-id="6f093-106">Targeting specific registrations</span></span>
<span data-ttu-id="6f093-107">Merhaba kayıtlar bunları tooassociate etiketleriyle yalnızca yolu tootarget belirli bildirimini sonra hedef bu etiketler.</span><span class="sxs-lookup"><span data-stu-id="6f093-107">hello only way tootarget specific notification registrations is tooassociate tags with them, then target those tags.</span></span> <span data-ttu-id="6f093-108">' Da anlatıldığı gibi [kayıt yönetimi](notification-hubs-push-notification-registration-management.md), sipariş tooreceive anında bir bildirim hub'ına bir uygulamaya sahip tooregister bir aygıtı bildirimleri işlemek.</span><span class="sxs-lookup"><span data-stu-id="6f093-108">As discussed in [Registration Management](notification-hubs-push-notification-registration-management.md), in order tooreceive push notifications an app has tooregister a device handle on a notification hub.</span></span> <span data-ttu-id="6f093-109">Bir kaydı bir bildirim hub'ına oluşturulduktan sonra hello uygulama arka uç anında iletme bildirimleri tooit gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6f093-109">Once a registration is created on a notification hub, hello application backend can send push notifications tooit.</span></span>
<span data-ttu-id="6f093-110">Merhaba uygulama arka uç yolları aşağıdaki hello hello kayıtlar tootarget belirli bir bildirim seçebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6f093-110">hello application backend can choose hello registrations tootarget with a specific notification in hello following ways:</span></span>

1. <span data-ttu-id="6f093-111">**Yayın**: hello bildirim hub'ındaki tüm kayıtlar hello bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="6f093-111">**Broadcast**: all registrations in hello notification hub receive hello notification.</span></span>
2. <span data-ttu-id="6f093-112">**Etiket**: Belirtilen hello içeren tüm kayıtlar etiketi hello bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="6f093-112">**Tag**: all registrations that contain hello specified tag receive hello notification.</span></span>
3. <span data-ttu-id="6f093-113">**Etiket ifade**: etiketleri eşleşme olan kümesinin hello belirtilen ifade tüm kayıtlar hello bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="6f093-113">**Tag expression**: all registrations whose set of tags match hello specified expression receive hello notification.</span></span>

## <a name="tags"></a><span data-ttu-id="6f093-114">Etiketler</span><span class="sxs-lookup"><span data-stu-id="6f093-114">Tags</span></span>
<span data-ttu-id="6f093-115">Bir etiketi içeren too120 karakter yukarı herhangi bir dize alfasayısal olmalı ve alfasayısal olmayan karakter aşağıdaki hello: '_', ' @', '#', '. ',':', '-'.</span><span class="sxs-lookup"><span data-stu-id="6f093-115">A tag can be any string, up too120 characters, containing alphanumeric and hello following non-alphanumeric characters: ‘_’, ‘@’, ‘#’, ‘.’, ‘:’, ‘-’.</span></span> <span data-ttu-id="6f093-116">Merhaba aşağıdaki örnekte belirli müzik grupları hakkında bildirimleri alacak bir uygulamayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="6f093-116">hello following example shows an application from which you can receive toast notifications about specific music groups.</span></span> <span data-ttu-id="6f093-117">Bu senaryoda, bir basit yol tooroute bildirimleri toolabel kayıtlar resim aşağıdaki hello olduğu gibi hello farklı bantları temsil eden etiketlere sahip olur.</span><span class="sxs-lookup"><span data-stu-id="6f093-117">In this scenario, a simple way tooroute notifications is toolabel registrations with tags that represent hello different bands, as in hello following picture.</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags.png)

<span data-ttu-id="6f093-118">Bu resim, selamlama iletisine etiketli **Beatles** hello etiketiyle kayıtlı ulaştığında yalnızca hello tablet **Beatles**.</span><span class="sxs-lookup"><span data-stu-id="6f093-118">In this picture, hello message tagged **Beatles** reaches only hello tablet that registered with hello tag **Beatles**.</span></span>

<span data-ttu-id="6f093-119">Kayıtlar için etiketler oluşturma hakkında daha fazla bilgi için bkz: [kayıt yönetimi](notification-hubs-push-notification-registration-management.md).</span><span class="sxs-lookup"><span data-stu-id="6f093-119">For more information about creating registrations for tags, see [Registration Management](notification-hubs-push-notification-registration-management.md).</span></span>

<span data-ttu-id="6f093-120">Hello kullanarak bildirimleri tootags Gönder hello bildirimleri yöntemlerini gönderebilirsiniz `Microsoft.Azure.NotificationHubs.NotificationHubClient` hello sınıfında [Microsoft Azure bildirim hub'ları](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK.</span><span class="sxs-lookup"><span data-stu-id="6f093-120">You can send notifications tootags using hello send notifications methods of hello `Microsoft.Azure.NotificationHubs.NotificationHubClient` class in hello [Microsoft Azure Notification Hubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK.</span></span> <span data-ttu-id="6f093-121">Node.js kullanın veya anında iletme bildirimleri REST API'leri hello.</span><span class="sxs-lookup"><span data-stu-id="6f093-121">You can also use Node.js, or hello Push Notifications REST APIs.</span></span>  <span data-ttu-id="6f093-122">Merhaba SDK kullanarak örnek aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="6f093-122">Here's an example using hello SDK.</span></span>

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You requested a Beatles notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Beatles");

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You requested a Wailers notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Wailers");




<span data-ttu-id="6f093-123">Etiketlerin ön sağlamasının toobe sahip değil ve toomultiple uygulamaya özgü kavramları başvuruda bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="6f093-123">Tags do not have toobe pre-provisioned and can refer toomultiple app-specific concepts.</span></span> <span data-ttu-id="6f093-124">Örneğin, bu örnek uygulama kullanıcılarının bantlar üzerinde açıklama ve tooreceive bildirimleri, yalnızca kendi sık kullanılan bantlar üzerinde hello açıklamaları için aynı zamanda bunların yorum hello bant bağımsız olarak kullanıcıların arkadaşlarını tüm açıklamalar için istiyor.</span><span class="sxs-lookup"><span data-stu-id="6f093-124">For example, users of this example application can comment on bands and want tooreceive toasts, not only for hello comments on their favorite bands, but also for all comments from their friends, regardless of hello band on which they are commenting.</span></span> <span data-ttu-id="6f093-125">Resim aşağıdaki hello bu senaryo örneği gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="6f093-125">hello following picture shows an example of this scenario:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags2.png)

<span data-ttu-id="6f093-126">Bu resmi Alice hello Beatles güncelleştirmeleri ilgilendiği ve Bob hello Wailers güncelleştirmeleri ilgilendiği.</span><span class="sxs-lookup"><span data-stu-id="6f093-126">In this picture, Alice is interested in updates for hello Beatles, and Bob is interested in updates for hello Wailers.</span></span> <span data-ttu-id="6f093-127">Bob ayrıca Cahit'ın açıklamaları ilgilenen ve Cahit içinde hello Wailers ilgileniyor.</span><span class="sxs-lookup"><span data-stu-id="6f093-127">Bob is also interested in Charlie’s comments, and Charlie is in interested in hello Wailers.</span></span> <span data-ttu-id="6f093-128">Bir bildirim hello Beatles Cahit'ın açıklama gönderildiğinde, Alice ve Bob alırsınız.</span><span class="sxs-lookup"><span data-stu-id="6f093-128">When a notification is sent for Charlie’s comment on hello Beatles, both Alice and Bob receive it.</span></span>

<span data-ttu-id="6f093-129">Birden çok sorunları etiketleri (örneğin, "band_Beatles" veya "follows_Charlie") kodlamak olsa da, etiketleri basit dizeler ve özellikleri değerlerle ' dir.</span><span class="sxs-lookup"><span data-stu-id="6f093-129">While you can encode multiple concerns in tags (for example, “band_Beatles” or “follows_Charlie”), tags are simple strings and not properties with values.</span></span> <span data-ttu-id="6f093-130">Bir kayıt yalnızca hello varlığı veya yokluğuna göre belirli bir tag üzerinde eşleştirilir.</span><span class="sxs-lookup"><span data-stu-id="6f093-130">A registration is matched only on hello presence or absence of a specific tag.</span></span>

<span data-ttu-id="6f093-131">Toouse toointerest grupları göndermek için nasıl etiketler üzerinde tam adım adım öğretici için bkz [sonu haber](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span><span class="sxs-lookup"><span data-stu-id="6f093-131">For a full step-by-step tutorial on how toouse tags for sending toointerest groups, see [Breaking News](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).</span></span>

## <a name="using-tags-tootarget-users"></a><span data-ttu-id="6f093-132">Etiketler tootarget kullanıcılar kullanma</span><span class="sxs-lookup"><span data-stu-id="6f093-132">Using tags tootarget users</span></span>
<span data-ttu-id="6f093-133">Başka bir şekilde toouse etiketler tooidentify belirli bir kullanıcının tüm hello cihazlarda desteklenir.</span><span class="sxs-lookup"><span data-stu-id="6f093-133">Another way toouse tags is tooidentify all hello devices of a particular user.</span></span> <span data-ttu-id="6f093-134">Kayıtlar resim aşağıdaki hello gibi bir kullanıcı kimliği içeren bir etiketle etiketlenebilir:</span><span class="sxs-lookup"><span data-stu-id="6f093-134">Registrations can be tagged with a tag that contains a user id, as in hello following picture:</span></span>

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags3.png)

<span data-ttu-id="6f093-135">Bu resim, tüm kayıtlar etiketli uid:Alice hello etiketli ileti uid:Alice ulaştığında; Bu nedenle, tüm Alice'in cihazlarını.</span><span class="sxs-lookup"><span data-stu-id="6f093-135">In this picture, hello message tagged uid:Alice reaches all registrations tagged uid:Alice; hence, all of Alice’s devices.</span></span>

## <a name="tag-expressions"></a><span data-ttu-id="6f093-136">Etiket ifadeleri</span><span class="sxs-lookup"><span data-stu-id="6f093-136">Tag expressions</span></span>
<span data-ttu-id="6f093-137">Bir bildirim tootarget tek bir etiket tarafından değil, ancak etiketleri hakkında Boole ifadesi tarafından tanımlanan bir kayıt kümesine sahip olduğu durumlar vardır.</span><span class="sxs-lookup"><span data-stu-id="6f093-137">There are cases in which a notification has tootarget a set of registrations that is identified not by a single tag, but by a Boolean expression on tags.</span></span>

<span data-ttu-id="6f093-138">Oyun hello kırmızı Sox ve Cardinals arasında hakkında Boston anımsatıcı tooeveryone gönderir Spor uygulama göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="6f093-138">Consider a sports application that sends a reminder tooeveryone in Boston about a game between hello Red Sox and Cardinals.</span></span> <span data-ttu-id="6f093-139">Merhaba istemci uygulaması etiketler ekipleri ve konum ilgi hakkında kaydederse, hello bildirim hello kırmızı Sox veya hello Cardinals ilgilenmektedir Boston içinde hedeflenen tooeveryone olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="6f093-139">If hello client app registers tags about interest in teams and location, then hello notification should be targeted tooeveryone in Boston who is interested in either hello Red Sox or hello Cardinals.</span></span> <span data-ttu-id="6f093-140">Bu durum Boole ifadesi aşağıdaki hello ile ifade edilebilir:</span><span class="sxs-lookup"><span data-stu-id="6f093-140">This condition can be expressed with hello following Boolean expression:</span></span>

    (follows_RedSox || follows_Cardinals) && location_Boston


![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags4.png)

<span data-ttu-id="6f093-141">Etiket ifadeleri içerebilir tüm Boole işleçleri gibi ve (& &), ya da (|) ve (!).</span><span class="sxs-lookup"><span data-stu-id="6f093-141">Tag expressions can contain all Boolean operators, such as AND (&&), OR (||), and NOT (!).</span></span> <span data-ttu-id="6f093-142">Bunlar ayrıca parantez içerebilir.</span><span class="sxs-lookup"><span data-stu-id="6f093-142">They can also contain parentheses.</span></span> <span data-ttu-id="6f093-143">Yalnızca ORs içeriyorsa etiket ifadeleri sınırlı too20 etiketleridir; Aksi takdirde sınırlı too6 etiketleri oldukları.</span><span class="sxs-lookup"><span data-stu-id="6f093-143">Tag expressions are limited too20 tags if they contain only ORs; otherwise they are limited too6 tags.</span></span>

<span data-ttu-id="6f093-144">Etiket ifadeleri ile Merhaba SDK kullanarak bildirim göndermek için örnek aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="6f093-144">Here's an example for sending notifications with tag expressions using hello SDK.</span></span>

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    String userTag = "(location_Boston && !follows_Cardinals)";    

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You want info on hello Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You want info on hello Red Socks</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, userTag);
