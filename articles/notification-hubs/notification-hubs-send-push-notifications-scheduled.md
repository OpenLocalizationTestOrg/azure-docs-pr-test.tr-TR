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
# <a name="how-to-send-scheduled-notifications"></a>Nasıl yapılır: Zamanlanmış bildirimleri gönderme
## <a name="overview"></a>Genel Bakış
Toosend istediğiniz bir senaryo varsa bir bildirim bazı hello gelecekteki noktası ancak kolay bir yolu toowake, arka uç kodu toosend hello bildirimi gerekmez. Standart katmanı bildirim hub'ları hello gelecekteki too7 günde tooschedule bildirimleri sağlayan bir özellik destekler.

Bir bildirim göndererek, yalnızca hello kullanın [ScheduledNotification](https://msdn.microsoft.com/library/microsoft.azure.notificationhubs.schedulednotification.aspx) hello aşağıdaki örnekte gösterildiği gibi hello Notification Hubs SDK'sı sınıfı:

    Notification notification = new AppleNotification("{\"aps\":{\"alert\":\"Happy birthday!\"}}");
    var scheduled = await hub.ScheduleNotificationAsync(notification, new DateTime(2014, 7, 19, 0, 0, 0));

Ayrıca, kendi notificationId kullanarak daha önce zamanlanmış bir bildirim iptal edebilirsiniz:

    await hub.CancelNotificationAsync(scheduled.ScheduledNotificationId);

Zamanlanmış bildirim gönderebilirsiniz hello sayısı sınırı vardır.

