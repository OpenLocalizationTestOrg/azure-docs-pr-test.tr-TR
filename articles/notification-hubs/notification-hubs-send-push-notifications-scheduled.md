---
title: "aaaHow toosend zamanlanmış bildirimleri | Microsoft Docs"
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
ms.openlocfilehash: 9b3ba715dad6f5d824a615e83f2863b0db47b533
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-to-send-scheduled-notifications"></a><span data-ttu-id="49c0d-104">Nasıl yapılır: Zamanlanmış bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="49c0d-104">How To: Send scheduled notifications</span></span>
## <a name="overview"></a><span data-ttu-id="49c0d-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="49c0d-105">Overview</span></span>
<span data-ttu-id="49c0d-106">Toosend istediğiniz bir senaryo varsa bir bildirim bazı hello gelecekteki noktası ancak kolay bir yolu toowake, arka uç kodu toosend hello bildirimi gerekmez.</span><span class="sxs-lookup"><span data-stu-id="49c0d-106">If you have a scenario in which you want toosend a notification at some point in hello future, but do not have an easy way toowake up your back-end code toosend hello notification.</span></span> <span data-ttu-id="49c0d-107">Standart katmanı bildirim hub'ları hello gelecekteki too7 günde tooschedule bildirimleri sağlayan bir özellik destekler.</span><span class="sxs-lookup"><span data-stu-id="49c0d-107">Standard tier Notification Hubs supports a feature that enables you tooschedule notifications up too7 days in hello future.</span></span>

<span data-ttu-id="49c0d-108">Bir bildirim göndererek, yalnızca hello kullanın [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) hello aşağıdaki örnekte gösterildiği gibi hello Notification Hubs SDK'sı sınıfı:</span><span class="sxs-lookup"><span data-stu-id="49c0d-108">When sending a notification, simply use hello [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) class in hello Notification Hubs SDK as shown in hello following example:</span></span>

    Notification notification = new AppleNotification("{\"aps\":{\"alert\":\"Happy birthday!\"}}");
    var scheduled = await hub.ScheduleNotificationAsync(notification, new DateTime(2014, 7, 19, 0, 0, 0));

<span data-ttu-id="49c0d-109">Ayrıca, kendi notificationId kullanarak daha önce zamanlanmış bir bildirim iptal edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="49c0d-109">Also, you can cancel a previously scheduled notification using its notificationId:</span></span>

    await hub.CancelNotificationAsync(scheduled.ScheduledNotificationId);

<span data-ttu-id="49c0d-110">Zamanlanmış bildirim gönderebilirsiniz hello sayısı sınırı vardır.</span><span class="sxs-lookup"><span data-stu-id="49c0d-110">There are no limits on hello number of scheduled notifications you can send.</span></span>

