---
title: "Azure Mobile Engagement iOS SDK sürüm notları | Microsoft Docs"
description: "En son güncelleştirmeler ve iOS için Azure Mobile Engagement SDK'sı için yordamlar"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a43ff0f6-90d5-4b3c-8d7a-a1db21bc776b
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 9bdaa57f9902373ccf796ff109332b64c66bf9e7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-mobile-engagement-ios-sdk-release-notes"></a><span data-ttu-id="66a44-103">Azure Mobile Engagement iOS SDK'sı sürüm notları</span><span class="sxs-lookup"><span data-stu-id="66a44-103">Azure Mobile Engagement iOS SDK release notes</span></span>

## <a name="410-07172017"></a><span data-ttu-id="66a44-104">4.1.0 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="66a44-104">4.1.0 (07/17/2017)</span></span>
* <span data-ttu-id="66a44-105">Sabit rozetleri arka planda temizlendi.</span><span class="sxs-lookup"><span data-stu-id="66a44-105">Fixed badges cleared in background.</span></span>
* <span data-ttu-id="66a44-106">Sabit uyarılar ana sırada adlı değil API'leri hakkında XCode 9.</span><span class="sxs-lookup"><span data-stu-id="66a44-106">Fixed warnings on XCode 9 about APIs not called in main queue.</span></span>
* <span data-ttu-id="66a44-107">Bellek sızıntısı ulaşma yoklamalarda sabit.</span><span class="sxs-lookup"><span data-stu-id="66a44-107">Fixed a memory leak in Reach polls.</span></span>
* <span data-ttu-id="66a44-108">İOS için destek bırakılan 6.X.</span><span class="sxs-lookup"><span data-stu-id="66a44-108">Dropped support for iOS 6.X.</span></span> <span data-ttu-id="66a44-109">Uygulamanızın dağıtım hedef bu sürümünden başlayarak olmalıdır en az iOS 7.</span><span class="sxs-lookup"><span data-stu-id="66a44-109">Starting from this version the deployment target of your application must be at least iOS 7.</span></span>

## <a name="401-12132016"></a><span data-ttu-id="66a44-110">4.0.1 (12/13/2016)</span><span class="sxs-lookup"><span data-stu-id="66a44-110">4.0.1 (12/13/2016)</span></span>
* <span data-ttu-id="66a44-111">Arka planda günlük teslim geliştirildi.</span><span class="sxs-lookup"><span data-stu-id="66a44-111">Improved log delivery in background.</span></span>

## <a name="400-09122016"></a><span data-ttu-id="66a44-112">4.0.0 (09/12/2016)</span><span class="sxs-lookup"><span data-stu-id="66a44-112">4.0.0 (09/12/2016)</span></span>
* <span data-ttu-id="66a44-113">İOS 10 cihazlarda değil işleme alınan sabit bildirimi.</span><span class="sxs-lookup"><span data-stu-id="66a44-113">Fixed notification not actioned on iOS 10 devices.</span></span>
* <span data-ttu-id="66a44-114">XCode 7 alanı onaylanamadı.</span><span class="sxs-lookup"><span data-stu-id="66a44-114">Deprecate XCode 7.</span></span>

## <a name="324-06302016"></a><span data-ttu-id="66a44-115">3.2.4 (06/30/2016)</span><span class="sxs-lookup"><span data-stu-id="66a44-115">3.2.4 (06/30/2016)</span></span>
* <span data-ttu-id="66a44-116">Sabit toplama teknik günlükleri ve diğer günlükler arasında.</span><span class="sxs-lookup"><span data-stu-id="66a44-116">Fixed aggregation between technical logs and other logs.</span></span>

## <a name="323-06072016"></a><span data-ttu-id="66a44-117">3.2.3 (06/07/2016)</span><span class="sxs-lookup"><span data-stu-id="66a44-117">3.2.3 (06/07/2016)</span></span>
* <span data-ttu-id="66a44-118">Hata, uygulama arka planda olduğunda burada teslim geri bildirilmedi sabit.</span><span class="sxs-lookup"><span data-stu-id="66a44-118">Fixed the bug where delivery feedback is not reported when app is in the background.</span></span>
* <span data-ttu-id="66a44-119">Teknik günlükleri gönderme en iyi duruma getirilmiş.</span><span class="sxs-lookup"><span data-stu-id="66a44-119">Optimized the sending of technical logs.</span></span>

## <a name="322-04072016"></a><span data-ttu-id="66a44-120">3.2.2 (04/07/2016)</span><span class="sxs-lookup"><span data-stu-id="66a44-120">3.2.2 (04/07/2016)</span></span>
* <span data-ttu-id="66a44-121">Sabit hatanın bazen çökmesine müşteri adayları, HTTP isteği iptal üzerinde.</span><span class="sxs-lookup"><span data-stu-id="66a44-121">Fixed bug on HTTP request cancellation which sometimes leads to crash.</span></span>

## <a name="321-12112015"></a><span data-ttu-id="66a44-122">3.2.1 (12/11/2015)</span><span class="sxs-lookup"><span data-stu-id="66a44-122">3.2.1 (12/11/2015)</span></span>
* <span data-ttu-id="66a44-123">Yeni bir uygulama örneği ayrıntılı bağlantılar içeren bir bildirim tarafından tetiklendiğinde gecikme sabit</span><span class="sxs-lookup"><span data-stu-id="66a44-123">Fixed the delay when a new app instance is triggered by a notification with deep links</span></span>

## <a name="320-10082015"></a><span data-ttu-id="66a44-124">3.2.0 (10/08/2015)</span><span class="sxs-lookup"><span data-stu-id="66a44-124">3.2.0 (10/08/2015)</span></span>
* <span data-ttu-id="66a44-125">SDK'sı ile çalışması için Bitcode'u etkin **Xcode 7**.</span><span class="sxs-lookup"><span data-stu-id="66a44-125">Enabled Bitcode in the SDK to make it work with **Xcode 7**.</span></span>
* <span data-ttu-id="66a44-126">Düzeltilen hatalar için uygulama bildirimleri ile ilgili.</span><span class="sxs-lookup"><span data-stu-id="66a44-126">Fixed bugs related to in-app notifications.</span></span>
* <span data-ttu-id="66a44-127">Uygulama bildirimleri daha güvenilir düşük pil ve diğer tür senaryoların durumunda yapılan.</span><span class="sxs-lookup"><span data-stu-id="66a44-127">Made the in-app notifications more reliable in case of low battery and other such scenarios.</span></span>
* <span data-ttu-id="66a44-128">3 taraf kitaplığı tarafından oluşturulan ek konsol günlükleri kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="66a44-128">Removed extra console logs generated by 3rd party library.</span></span>

## <a name="310-08262015"></a><span data-ttu-id="66a44-129">3.1.0 (08/26/2015)</span><span class="sxs-lookup"><span data-stu-id="66a44-129">3.1.0 (08/26/2015)</span></span>
* <span data-ttu-id="66a44-130">İOS 9 uyumluluk hata sahip bir üçüncü taraf kitaplık düzeltin.</span><span class="sxs-lookup"><span data-stu-id="66a44-130">Fix iOS 9 compatibility bug with a third party library.</span></span> <span data-ttu-id="66a44-131">Sonuçlar, uygulama bilgilerini veya ek veriler gönderme yoklar sırada kilitlenme neden olmaktadır.</span><span class="sxs-lookup"><span data-stu-id="66a44-131">It was causing crashes while sending polls results, application information or extra data.</span></span>

## <a name="300-06192015"></a><span data-ttu-id="66a44-132">3.0.0 (06/19/2015)</span><span class="sxs-lookup"><span data-stu-id="66a44-132">3.0.0 (06/19/2015)</span></span>
* <span data-ttu-id="66a44-133">Mobile Engagement sessiz anında iletme bildirimleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="66a44-133">Mobile Engagement uses Silent Push Notifications.</span></span>
* <span data-ttu-id="66a44-134">İOS için destek bırakılan 4.X.</span><span class="sxs-lookup"><span data-stu-id="66a44-134">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="66a44-135">Uygulamanızın dağıtım hedef bu sürümünden başlayarak olmalıdır en az iOS 6.</span><span class="sxs-lookup"><span data-stu-id="66a44-135">Starting from this version the deployment target of your application must be at least iOS 6.</span></span>

## <a name="220-05212015"></a><span data-ttu-id="66a44-136">2.2.0 (05/21/2015)</span><span class="sxs-lookup"><span data-stu-id="66a44-136">2.2.0 (05/21/2015)</span></span>
* <span data-ttu-id="66a44-137">Cihazlar için Mobile Engagement cihaz kimliğini < iOS 6 yükleme sırasında oluşturulan GUID şimdi dayanır.</span><span class="sxs-lookup"><span data-stu-id="66a44-137">The Mobile Engagement device id for devices < iOS 6 is now based on a GUID generated at installation time.</span></span>

## <a name="210-04242015"></a><span data-ttu-id="66a44-138">2.1.0 (04/24/2015)</span><span class="sxs-lookup"><span data-stu-id="66a44-138">2.1.0 (04/24/2015)</span></span>
* <span data-ttu-id="66a44-139">SWIFT uyumluluk eklendi.</span><span class="sxs-lookup"><span data-stu-id="66a44-139">Added Swift compatibility.</span></span>
* <span data-ttu-id="66a44-140">Uygulama açtıktan sonra bir bildirim tıklandığında, eylem URL'si artık sağ yürütüldü.</span><span class="sxs-lookup"><span data-stu-id="66a44-140">When clicking on a notification, the action URL is now executed right after the application is opened.</span></span>
* <span data-ttu-id="66a44-141">Eklenen eksik üstbilgi dosyasında SDK paketi.</span><span class="sxs-lookup"><span data-stu-id="66a44-141">Added missing header file in SDK package.</span></span>
* <span data-ttu-id="66a44-142">Mobile Engagement kilitlenme Raporlayıcı devre dışı bırakıldığında bir sorun düzeltilmiştir.</span><span class="sxs-lookup"><span data-stu-id="66a44-142">Fixed an issue when the Mobile Engagement crash reporter was disabled.</span></span>

## <a name="200-02172015"></a><span data-ttu-id="66a44-143">2.0.0 (02/17/2015)</span><span class="sxs-lookup"><span data-stu-id="66a44-143">2.0.0 (02/17/2015)</span></span>
* <span data-ttu-id="66a44-144">Azure Mobile Engagement ilk sürümünü</span><span class="sxs-lookup"><span data-stu-id="66a44-144">Initial Release of Azure Mobile Engagement</span></span>
* <span data-ttu-id="66a44-145">AppID/sdkKey yapılandırma bağlantı dizesini yapılandırma tarafından değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="66a44-145">appId/sdkKey configuration is replaced by a connection string configuration.</span></span>
* <span data-ttu-id="66a44-146">Rastgele XMPP varlıklardan rasgele XMPP ileti alıp göndermek için API kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="66a44-146">Removed API to send and receive arbitrary XMPP messages from arbitrary XMPP entities.</span></span>
* <span data-ttu-id="66a44-147">Cihazlar arasında ileti gönderme ve alma için API kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="66a44-147">Removed API to send and receive messages between devices.</span></span>
* <span data-ttu-id="66a44-148">Güvenlik geliştirmeleri.</span><span class="sxs-lookup"><span data-stu-id="66a44-148">Security improvements.</span></span>
* <span data-ttu-id="66a44-149">SmartAd izleme kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="66a44-149">SmartAd tracking removed.</span></span>
