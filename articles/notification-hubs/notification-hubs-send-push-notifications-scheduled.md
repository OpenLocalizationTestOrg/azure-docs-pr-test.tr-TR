---
title: "Zamanlanmış bildirimleri göndermek nasıl | Microsoft Docs"
description: "Bu konuda, Azure Notification Hubs ile zamanlanmış bildirimleri kullanmayı açıklar."
services: notification-hubs
documentationcenter: .net
keywords: "anında iletme bildirimleri, anında iletme bildirimi, anında iletme bildirimleri planlama"
author: ysxu
manager: erikre
editor: 
ms.assetid: 6b718c75-75dd-4c99-aee3-db1288235c1a
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: efac6e1ecc00359f1622d380333140bc055c83e0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-send-scheduled-notifications"></a><span data-ttu-id="0926c-104">Nasıl yapılır: Zamanlanmış bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="0926c-104">How To: Send scheduled notifications</span></span>
## <a name="overview"></a><span data-ttu-id="0926c-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="0926c-105">Overview</span></span>
<span data-ttu-id="0926c-106">Bir senaryo, belirli bir noktada gelecekte bir bildirim göndermek istiyor ancak uyandırmak için kolay bir yol arka uç kodunuzun bildirim göndermek için yoksa varsa.</span><span class="sxs-lookup"><span data-stu-id="0926c-106">If you have a scenario in which you want to send a notification at some point in the future, but do not have an easy way to wake up your back-end code to send the notification.</span></span> <span data-ttu-id="0926c-107">Standart katmanı bildirim hub'ları bildirimleri gelecekte 7 gün için zamanlamanıza olanak sağlayan bir özellik destekler.</span><span class="sxs-lookup"><span data-stu-id="0926c-107">Standard tier Notification Hubs supports a feature that enables you to schedule notifications up to 7 days in the future.</span></span>

<span data-ttu-id="0926c-108">Bir bildirim göndererek, yalnızca kullanın [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) aşağıdaki örnekte gösterildiği gibi bildirim hub'ları SDK'da sınıfı:</span><span class="sxs-lookup"><span data-stu-id="0926c-108">When sending a notification, simply use the [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) class in the Notification Hubs SDK as shown in the following example:</span></span>

    Notification notification = new AppleNotification("{\"aps\":{\"alert\":\"Happy birthday!\"}}");
    var scheduled = await hub.ScheduleNotificationAsync(notification, new DateTime(2014, 7, 19, 0, 0, 0));

<span data-ttu-id="0926c-109">Ayrıca, kendi notificationId kullanarak daha önce zamanlanmış bir bildirim iptal edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="0926c-109">Also, you can cancel a previously scheduled notification using its notificationId:</span></span>

    await hub.CancelNotificationAsync(scheduled.ScheduledNotificationId);

<span data-ttu-id="0926c-110">Zamanlanmış bildirim gönderebilirsiniz sayısı sınırı vardır.</span><span class="sxs-lookup"><span data-stu-id="0926c-110">There are no limits on the number of scheduled notifications you can send.</span></span>

