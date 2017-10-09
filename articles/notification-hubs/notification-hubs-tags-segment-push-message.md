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
# <a name="routing-and-tag-expressions"></a>Yönlendirme ve etiket ifadeleri
## <a name="overview"></a>Genel Bakış
Etiket ifadeleri cihazlar ya da daha açık belirtmek gerekirse kayıtlar, belirli kümelerini tootarget, bildirim hub'ları üzerinden bir anında iletme bildirimi gönderirken etkinleştirin.

## <a name="targeting-specific-registrations"></a>Belirli kayıtları hedefleme
Merhaba kayıtlar bunları tooassociate etiketleriyle yalnızca yolu tootarget belirli bildirimini sonra hedef bu etiketler. ' Da anlatıldığı gibi [kayıt yönetimi](notification-hubs-push-notification-registration-management.md), sipariş tooreceive anında bir bildirim hub'ına bir uygulamaya sahip tooregister bir aygıtı bildirimleri işlemek. Bir kaydı bir bildirim hub'ına oluşturulduktan sonra hello uygulama arka uç anında iletme bildirimleri tooit gönderebilirsiniz.
Merhaba uygulama arka uç yolları aşağıdaki hello hello kayıtlar tootarget belirli bir bildirim seçebilirsiniz:

1. **Yayın**: hello bildirim hub'ındaki tüm kayıtlar hello bildirim alırsınız.
2. **Etiket**: Belirtilen hello içeren tüm kayıtlar etiketi hello bildirim alırsınız.
3. **Etiket ifade**: etiketleri eşleşme olan kümesinin hello belirtilen ifade tüm kayıtlar hello bildirim alırsınız.

## <a name="tags"></a>Etiketler
Bir etiketi içeren too120 karakter yukarı herhangi bir dize alfasayısal olmalı ve alfasayısal olmayan karakter aşağıdaki hello: '_', ' @', '#', '. ',':', '-'. Merhaba aşağıdaki örnekte belirli müzik grupları hakkında bildirimleri alacak bir uygulamayı gösterir. Bu senaryoda, bir basit yol tooroute bildirimleri toolabel kayıtlar resim aşağıdaki hello olduğu gibi hello farklı bantları temsil eden etiketlere sahip olur.

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags.png)

Bu resim, selamlama iletisine etiketli **Beatles** hello etiketiyle kayıtlı ulaştığında yalnızca hello tablet **Beatles**.

Kayıtlar için etiketler oluşturma hakkında daha fazla bilgi için bkz: [kayıt yönetimi](notification-hubs-push-notification-registration-management.md).

Hello kullanarak bildirimleri tootags Gönder hello bildirimleri yöntemlerini gönderebilirsiniz `Microsoft.Azure.NotificationHubs.NotificationHubClient` hello sınıfında [Microsoft Azure bildirim hub'ları](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/) SDK. Node.js kullanın veya anında iletme bildirimleri REST API'leri hello.  Merhaba SDK kullanarak örnek aşağıda verilmiştir.

    Microsoft.Azure.NotificationHubs.NotificationOutcome outcome = null;

    // Windows 8.1 / Windows Phone 8.1
    var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">" +
    "You requested a Beatles notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Beatles");

    // Windows 10
    toast = @"<toast><visual><binding template=""ToastGeneric""><text id=""1"">" +
    "You requested a Wailers notification</text></binding></visual></toast>";
    outcome = await Notifications.Instance.Hub.SendWindowsNativeNotificationAsync(toast, "Wailers");




Etiketlerin ön sağlamasının toobe sahip değil ve toomultiple uygulamaya özgü kavramları başvuruda bulunabilir. Örneğin, bu örnek uygulama kullanıcılarının bantlar üzerinde açıklama ve tooreceive bildirimleri, yalnızca kendi sık kullanılan bantlar üzerinde hello açıklamaları için aynı zamanda bunların yorum hello bant bağımsız olarak kullanıcıların arkadaşlarını tüm açıklamalar için istiyor. Resim aşağıdaki hello bu senaryo örneği gösterilmektedir:

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags2.png)

Bu resmi Alice hello Beatles güncelleştirmeleri ilgilendiği ve Bob hello Wailers güncelleştirmeleri ilgilendiği. Bob ayrıca Cahit'ın açıklamaları ilgilenen ve Cahit içinde hello Wailers ilgileniyor. Bir bildirim hello Beatles Cahit'ın açıklama gönderildiğinde, Alice ve Bob alırsınız.

Birden çok sorunları etiketleri (örneğin, "band_Beatles" veya "follows_Charlie") kodlamak olsa da, etiketleri basit dizeler ve özellikleri değerlerle ' dir. Bir kayıt yalnızca hello varlığı veya yokluğuna göre belirli bir tag üzerinde eşleştirilir.

Toouse toointerest grupları göndermek için nasıl etiketler üzerinde tam adım adım öğretici için bkz [sonu haber](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md).

## <a name="using-tags-tootarget-users"></a>Etiketler tootarget kullanıcılar kullanma
Başka bir şekilde toouse etiketler tooidentify belirli bir kullanıcının tüm hello cihazlarda desteklenir. Kayıtlar resim aşağıdaki hello gibi bir kullanıcı kimliği içeren bir etiketle etiketlenebilir:

![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags3.png)

Bu resim, tüm kayıtlar etiketli uid:Alice hello etiketli ileti uid:Alice ulaştığında; Bu nedenle, tüm Alice'in cihazlarını.

## <a name="tag-expressions"></a>Etiket ifadeleri
Bir bildirim tootarget tek bir etiket tarafından değil, ancak etiketleri hakkında Boole ifadesi tarafından tanımlanan bir kayıt kümesine sahip olduğu durumlar vardır.

Oyun hello kırmızı Sox ve Cardinals arasında hakkında Boston anımsatıcı tooeveryone gönderir Spor uygulama göz önünde bulundurun. Merhaba istemci uygulaması etiketler ekipleri ve konum ilgi hakkında kaydederse, hello bildirim hello kırmızı Sox veya hello Cardinals ilgilenmektedir Boston içinde hedeflenen tooeveryone olması gerekir. Bu durum Boole ifadesi aşağıdaki hello ile ifade edilebilir:

    (follows_RedSox || follows_Cardinals) && location_Boston


![](./media/notification-hubs-routing-tag-expressions/notification-hubs-tags4.png)

Etiket ifadeleri içerebilir tüm Boole işleçleri gibi ve (& &), ya da (|) ve (!). Bunlar ayrıca parantez içerebilir. Yalnızca ORs içeriyorsa etiket ifadeleri sınırlı too20 etiketleridir; Aksi takdirde sınırlı too6 etiketleri oldukları.

Etiket ifadeleri ile Merhaba SDK kullanarak bildirim göndermek için örnek aşağıda verilmiştir.

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
