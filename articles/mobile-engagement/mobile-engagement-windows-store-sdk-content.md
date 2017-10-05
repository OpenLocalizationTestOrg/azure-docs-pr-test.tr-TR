---
title: "Windows Evrensel uygulamaları SDK içeriği"
description: "Azure Mobile Engagement Windows Evrensel uygulamaları SDK içeriği hakkında bilgi edinin"
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
ms.openlocfilehash: b28d525ab16487b963772e23fdecd11f94dcabd1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="windows-universal-apps-sdk-content"></a><span data-ttu-id="55473-103">Windows Evrensel uygulamaları SDK içeriği</span><span class="sxs-lookup"><span data-stu-id="55473-103">Windows Universal Apps SDK content</span></span>
<span data-ttu-id="55473-104">Bu belge listeler ve uygulamanızda SDK'sı tarafından dağıtılan içeriği açıklar.</span><span class="sxs-lookup"><span data-stu-id="55473-104">This document lists and describes the content deployed by the SDK in your application.</span></span>

## <a name="the-resources-folder"></a><span data-ttu-id="55473-105">`/Resources` Klasörü</span><span class="sxs-lookup"><span data-stu-id="55473-105">The `/Resources` folder</span></span>
<span data-ttu-id="55473-106">Bu klasör, Mobile Engagement gereken tüm kaynakları içerir.</span><span class="sxs-lookup"><span data-stu-id="55473-106">This folder contains all the resources that Mobile Engagement needs.</span></span> <span data-ttu-id="55473-107">Ayrıca bunları uygulamanızı uyacak şekilde özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="55473-107">You can also customize them to fit your app.</span></span>

* <span data-ttu-id="55473-108">`EngagementConfiguration.xml`: Mobile Engagement'ın yapılandırma dosyası, Mobile Engagement ayarlarını (Mobile Engagement bağlantı dizesi, rapor kilitlenme...) burada özelleştirebilirsiniz budur.</span><span class="sxs-lookup"><span data-stu-id="55473-108">`EngagementConfiguration.xml` : The Mobile Engagement's configuration file, this is where you can customize Mobile Engagement settings (Mobile Engagement connection string, report crash...).</span></span>

### <a name="html-folder"></a><span data-ttu-id="55473-109">/HTML klasörü</span><span class="sxs-lookup"><span data-stu-id="55473-109">/html folder</span></span>
* <span data-ttu-id="55473-110">`EngagementNotification.html``Notification` Web görünümü html tasarımını uygulama başlıkları için.</span><span class="sxs-lookup"><span data-stu-id="55473-110">`EngagementNotification.html` : The `Notification` web view html design for in-app banners.</span></span>
* <span data-ttu-id="55473-111">`EngagementAnnouncement.html``Announcement` Web görünümü html tasarımını uygulama Interstitial görünümler için.</span><span class="sxs-lookup"><span data-stu-id="55473-111">`EngagementAnnouncement.html` : The `Announcement` web view html design for in-app interstitial views.</span></span>

### <a name="images-folder"></a><span data-ttu-id="55473-112">Resim klasörü</span><span class="sxs-lookup"><span data-stu-id="55473-112">/images folder</span></span>
* <span data-ttu-id="55473-113">`EngagementIconNotification.png`: Bir bildirim sol tarafında görüntülenen marka simge bunu, marka simgesiyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="55473-113">`EngagementIconNotification.png` : The brand icon displayed at the left of a notification, replace this one by your brand icon.</span></span>
* <span data-ttu-id="55473-114">`EngagementIconOk.png``Ok` Reach içerik sayfalarının eylem veya doğrulama düğmesi için simge.</span><span class="sxs-lookup"><span data-stu-id="55473-114">`EngagementIconOk.png` : The `Ok` icon of the reach content pages for the action or validation button.</span></span>
* <span data-ttu-id="55473-115">`EngagementIconNOK.png``NOK` Reach içerik sayfalarının doğrulama düğmesi devre dışı bırakıldığında kullanılan simge.</span><span class="sxs-lookup"><span data-stu-id="55473-115">`EngagementIconNOK.png` : The `NOK` icon used when the validation button of the reach content pages is disabled.</span></span>
* <span data-ttu-id="55473-116">`EngagementIconClose.png``Close` Ulaşma bildirim ve içerikleri Atla düğmesi için simge.</span><span class="sxs-lookup"><span data-stu-id="55473-116">`EngagementIconClose.png` : The `Close` icon of the reach notifications and contents for the dismiss button.</span></span>

### <a name="overlay-folder"></a><span data-ttu-id="55473-117">/overlay klasörü</span><span class="sxs-lookup"><span data-stu-id="55473-117">/overlay folder</span></span>
* <span data-ttu-id="55473-118">`EngagementPageOverlay.cs`: Katılım eklemek için sorumlu katmana sayfa alt uygulama UI ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="55473-118">`EngagementPageOverlay.cs` : The overlay page responsible for adding the Engagement reach in-app UI to its child.</span></span>

