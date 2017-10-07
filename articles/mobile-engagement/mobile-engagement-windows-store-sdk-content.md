---
title: "aaaWindows Evrensel uygulamaları SDK içeriği"
description: "Azure Mobile Engagement için hello Windows Evrensel uygulamaları SDK Merhaba içeriğine hakkında bilgi edinin"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8fa1b701-1c2b-4aec-940c-06c974ef5405
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: a8013d2433c0be62d737c8bc6e8360ed79bbe532
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-sdk-content"></a>Windows Evrensel uygulamaları SDK içeriği
Bu belge, listeler ve uygulamanızda hello SDK tarafından dağıtılan hello içeriği açıklar.

## <a name="hello-resources-folder"></a>Merhaba `/Resources` klasörü
Bu klasör, Mobile Engagement gereken tüm hello kaynakları içerir. Ayrıca bunları toofit özelleştirebilirsiniz uygulamanızı.

* `EngagementConfiguration.xml`: Mobile Engagement yapılandırma dosyası Merhaba, bunu burada, Mobile Engagement ayarları (Mobile Engagement bağlantı dizesi, rapor kilitlenme...) özelleştirebilirsiniz.

### <a name="html-folder"></a>/HTML klasörü
* `EngagementNotification.html`: Merhaba `Notification` web görünümü html tasarımını uygulama başlıkları için.
* `EngagementAnnouncement.html`: Merhaba `Announcement` web görünümü html tasarımını uygulama Interstitial görünümler için.

### <a name="images-folder"></a>Resim klasörü
* `EngagementIconNotification.png`: hello marka simgesi hello sırasında görüntülenen bir bildirim sol, bunu, marka simgesiyle değiştirin.
* `EngagementIconOk.png`: Merhaba `Ok` hello ulaşma içerik sayfalarının hello eylem veya doğrulama düğmesi için simge.
* `EngagementIconNOK.png`: Merhaba `NOK` hello ulaşma içerik sayfalarının hello doğrulama düğmesi devre dışı bırakıldığında kullanılan simge.
* `EngagementIconClose.png`: Merhaba `Close` hello simgesini ulaşmasını bildirimleri ve hello için içerik düğmesi yok sayın.

### <a name="overlay-folder"></a>/overlay klasörü
* `EngagementPageOverlay.cs`: hello katmana sayfa Engagement reach uygulama kullanıcı Arabirimi tooits alt hello eklemek için sorumlu.

