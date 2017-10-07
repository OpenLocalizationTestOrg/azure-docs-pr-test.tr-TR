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
# <a name="windows-universal-apps-sdk-content"></a><span data-ttu-id="2f57b-103">Windows Evrensel uygulamaları SDK içeriği</span><span class="sxs-lookup"><span data-stu-id="2f57b-103">Windows Universal Apps SDK content</span></span>
<span data-ttu-id="2f57b-104">Bu belge, listeler ve uygulamanızda hello SDK tarafından dağıtılan hello içeriği açıklar.</span><span class="sxs-lookup"><span data-stu-id="2f57b-104">This document lists and describes hello content deployed by hello SDK in your application.</span></span>

## <a name="hello-resources-folder"></a><span data-ttu-id="2f57b-105">Merhaba `/Resources` klasörü</span><span class="sxs-lookup"><span data-stu-id="2f57b-105">hello `/Resources` folder</span></span>
<span data-ttu-id="2f57b-106">Bu klasör, Mobile Engagement gereken tüm hello kaynakları içerir.</span><span class="sxs-lookup"><span data-stu-id="2f57b-106">This folder contains all hello resources that Mobile Engagement needs.</span></span> <span data-ttu-id="2f57b-107">Ayrıca bunları toofit özelleştirebilirsiniz uygulamanızı.</span><span class="sxs-lookup"><span data-stu-id="2f57b-107">You can also customize them toofit your app.</span></span>

* <span data-ttu-id="2f57b-108">`EngagementConfiguration.xml`: Mobile Engagement yapılandırma dosyası Merhaba, bunu burada, Mobile Engagement ayarları (Mobile Engagement bağlantı dizesi, rapor kilitlenme...) özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2f57b-108">`EngagementConfiguration.xml` : hello Mobile Engagement's configuration file, this is where you can customize Mobile Engagement settings (Mobile Engagement connection string, report crash...).</span></span>

### <a name="html-folder"></a><span data-ttu-id="2f57b-109">/HTML klasörü</span><span class="sxs-lookup"><span data-stu-id="2f57b-109">/html folder</span></span>
* <span data-ttu-id="2f57b-110">`EngagementNotification.html`: Merhaba `Notification` web görünümü html tasarımını uygulama başlıkları için.</span><span class="sxs-lookup"><span data-stu-id="2f57b-110">`EngagementNotification.html` : hello `Notification` web view html design for in-app banners.</span></span>
* <span data-ttu-id="2f57b-111">`EngagementAnnouncement.html`: Merhaba `Announcement` web görünümü html tasarımını uygulama Interstitial görünümler için.</span><span class="sxs-lookup"><span data-stu-id="2f57b-111">`EngagementAnnouncement.html` : hello `Announcement` web view html design for in-app interstitial views.</span></span>

### <a name="images-folder"></a><span data-ttu-id="2f57b-112">Resim klasörü</span><span class="sxs-lookup"><span data-stu-id="2f57b-112">/images folder</span></span>
* <span data-ttu-id="2f57b-113">`EngagementIconNotification.png`: hello marka simgesi hello sırasında görüntülenen bir bildirim sol, bunu, marka simgesiyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2f57b-113">`EngagementIconNotification.png` : hello brand icon displayed at hello left of a notification, replace this one by your brand icon.</span></span>
* <span data-ttu-id="2f57b-114">`EngagementIconOk.png`: Merhaba `Ok` hello ulaşma içerik sayfalarının hello eylem veya doğrulama düğmesi için simge.</span><span class="sxs-lookup"><span data-stu-id="2f57b-114">`EngagementIconOk.png` : hello `Ok` icon of hello reach content pages for hello action or validation button.</span></span>
* <span data-ttu-id="2f57b-115">`EngagementIconNOK.png`: Merhaba `NOK` hello ulaşma içerik sayfalarının hello doğrulama düğmesi devre dışı bırakıldığında kullanılan simge.</span><span class="sxs-lookup"><span data-stu-id="2f57b-115">`EngagementIconNOK.png` : hello `NOK` icon used when hello validation button of hello reach content pages is disabled.</span></span>
* <span data-ttu-id="2f57b-116">`EngagementIconClose.png`: Merhaba `Close` hello simgesini ulaşmasını bildirimleri ve hello için içerik düğmesi yok sayın.</span><span class="sxs-lookup"><span data-stu-id="2f57b-116">`EngagementIconClose.png` : hello `Close` icon of hello reach notifications and contents for hello dismiss button.</span></span>

### <a name="overlay-folder"></a><span data-ttu-id="2f57b-117">/overlay klasörü</span><span class="sxs-lookup"><span data-stu-id="2f57b-117">/overlay folder</span></span>
* <span data-ttu-id="2f57b-118">`EngagementPageOverlay.cs`: hello katmana sayfa Engagement reach uygulama kullanıcı Arabirimi tooits alt hello eklemek için sorumlu.</span><span class="sxs-lookup"><span data-stu-id="2f57b-118">`EngagementPageOverlay.cs` : hello overlay page responsible for adding hello Engagement reach in-app UI tooits child.</span></span>

