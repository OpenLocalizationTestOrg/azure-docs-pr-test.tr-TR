---
title: "aaaAzure Mobile Engagement iOS SDK sürüm notları | Microsoft Docs"
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
ms.openlocfilehash: ae29d200ebb1784357b29edbd1f66b71df0778cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-mobile-engagement-ios-sdk-release-notes"></a><span data-ttu-id="ad25f-103">Azure Mobile Engagement iOS SDK'sı sürüm notları</span><span class="sxs-lookup"><span data-stu-id="ad25f-103">Azure Mobile Engagement iOS SDK release notes</span></span>

## <a name="410-07172017"></a><span data-ttu-id="ad25f-104">4.1.0 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="ad25f-104">4.1.0 (07/17/2017)</span></span>
* <span data-ttu-id="ad25f-105">Sabit rozetleri arka planda temizlendi.</span><span class="sxs-lookup"><span data-stu-id="ad25f-105">Fixed badges cleared in background.</span></span>
* <span data-ttu-id="ad25f-106">Sabit uyarılar ana sırada adlı değil API'leri hakkında XCode 9.</span><span class="sxs-lookup"><span data-stu-id="ad25f-106">Fixed warnings on XCode 9 about APIs not called in main queue.</span></span>
* <span data-ttu-id="ad25f-107">Bellek sızıntısı ulaşma yoklamalarda sabit.</span><span class="sxs-lookup"><span data-stu-id="ad25f-107">Fixed a memory leak in Reach polls.</span></span>
* <span data-ttu-id="ad25f-108">İOS için destek bırakılan 6.X.</span><span class="sxs-lookup"><span data-stu-id="ad25f-108">Dropped support for iOS 6.X.</span></span> <span data-ttu-id="ad25f-109">Bu sürüm hello dağıtım hedefi, uygulamanızın başlangıç olmalıdır en az iOS 7.</span><span class="sxs-lookup"><span data-stu-id="ad25f-109">Starting from this version hello deployment target of your application must be at least iOS 7.</span></span>

## <a name="401-12132016"></a><span data-ttu-id="ad25f-110">4.0.1 (12/13/2016)</span><span class="sxs-lookup"><span data-stu-id="ad25f-110">4.0.1 (12/13/2016)</span></span>
* <span data-ttu-id="ad25f-111">Arka planda günlük teslim geliştirildi.</span><span class="sxs-lookup"><span data-stu-id="ad25f-111">Improved log delivery in background.</span></span>

## <a name="400-09122016"></a><span data-ttu-id="ad25f-112">4.0.0 (09/12/2016)</span><span class="sxs-lookup"><span data-stu-id="ad25f-112">4.0.0 (09/12/2016)</span></span>
* <span data-ttu-id="ad25f-113">İOS 10 cihazlarda değil işleme alınan sabit bildirimi.</span><span class="sxs-lookup"><span data-stu-id="ad25f-113">Fixed notification not actioned on iOS 10 devices.</span></span>
* <span data-ttu-id="ad25f-114">XCode 7 alanı onaylanamadı.</span><span class="sxs-lookup"><span data-stu-id="ad25f-114">Deprecate XCode 7.</span></span>

## <a name="324-06302016"></a><span data-ttu-id="ad25f-115">3.2.4 (06/30/2016)</span><span class="sxs-lookup"><span data-stu-id="ad25f-115">3.2.4 (06/30/2016)</span></span>
* <span data-ttu-id="ad25f-116">Sabit toplama teknik günlükleri ve diğer günlükler arasında.</span><span class="sxs-lookup"><span data-stu-id="ad25f-116">Fixed aggregation between technical logs and other logs.</span></span>

## <a name="323-06072016"></a><span data-ttu-id="ad25f-117">3.2.3 (06/07/2016)</span><span class="sxs-lookup"><span data-stu-id="ad25f-117">3.2.3 (06/07/2016)</span></span>
* <span data-ttu-id="ad25f-118">Sabit hello hata uygulama hello arka planda olduğunda burada teslim geri bildirilmedi.</span><span class="sxs-lookup"><span data-stu-id="ad25f-118">Fixed hello bug where delivery feedback is not reported when app is in hello background.</span></span>
* <span data-ttu-id="ad25f-119">En iyi duruma getirilmiş hello teknik günlükleri gönderme.</span><span class="sxs-lookup"><span data-stu-id="ad25f-119">Optimized hello sending of technical logs.</span></span>

## <a name="322-04072016"></a><span data-ttu-id="ad25f-120">3.2.2 (04/07/2016)</span><span class="sxs-lookup"><span data-stu-id="ad25f-120">3.2.2 (04/07/2016)</span></span>
* <span data-ttu-id="ad25f-121">Sabit hatanın bazen toocrash müşteri adayları, HTTP isteği iptal üzerinde.</span><span class="sxs-lookup"><span data-stu-id="ad25f-121">Fixed bug on HTTP request cancellation which sometimes leads toocrash.</span></span>

## <a name="321-12112015"></a><span data-ttu-id="ad25f-122">3.2.1 (12/11/2015)</span><span class="sxs-lookup"><span data-stu-id="ad25f-122">3.2.1 (12/11/2015)</span></span>
* <span data-ttu-id="ad25f-123">Yeni bir uygulama örneği ayrıntılı bağlantılar içeren bir bildirim tarafından tetiklendiğinde sabit hello gecikmesi</span><span class="sxs-lookup"><span data-stu-id="ad25f-123">Fixed hello delay when a new app instance is triggered by a notification with deep links</span></span>

## <a name="320-10082015"></a><span data-ttu-id="ad25f-124">3.2.0 (10/08/2015)</span><span class="sxs-lookup"><span data-stu-id="ad25f-124">3.2.0 (10/08/2015)</span></span>
* <span data-ttu-id="ad25f-125">İş ile Merhaba SDK toomake Bitcode'u etkin **Xcode 7**.</span><span class="sxs-lookup"><span data-stu-id="ad25f-125">Enabled Bitcode in hello SDK toomake it work with **Xcode 7**.</span></span>
* <span data-ttu-id="ad25f-126">Düzeltilen hatalar tooin uygulama bildirimleri ile ilgili.</span><span class="sxs-lookup"><span data-stu-id="ad25f-126">Fixed bugs related tooin-app notifications.</span></span>
* <span data-ttu-id="ad25f-127">Merhaba uygulama bildirimleri daha güvenilir düşük pil ve diğer tür senaryoların durumunda yapılan.</span><span class="sxs-lookup"><span data-stu-id="ad25f-127">Made hello in-app notifications more reliable in case of low battery and other such scenarios.</span></span>
* <span data-ttu-id="ad25f-128">3 taraf kitaplığı tarafından oluşturulan ek konsol günlükleri kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="ad25f-128">Removed extra console logs generated by 3rd party library.</span></span>

## <a name="310-08262015"></a><span data-ttu-id="ad25f-129">3.1.0 (08/26/2015)</span><span class="sxs-lookup"><span data-stu-id="ad25f-129">3.1.0 (08/26/2015)</span></span>
* <span data-ttu-id="ad25f-130">İOS 9 uyumluluk hata sahip bir üçüncü taraf kitaplık düzeltin.</span><span class="sxs-lookup"><span data-stu-id="ad25f-130">Fix iOS 9 compatibility bug with a third party library.</span></span> <span data-ttu-id="ad25f-131">Sonuçlar, uygulama bilgilerini veya ek veriler gönderme yoklar sırada kilitlenme neden olmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ad25f-131">It was causing crashes while sending polls results, application information or extra data.</span></span>

## <a name="300-06192015"></a><span data-ttu-id="ad25f-132">3.0.0 (06/19/2015)</span><span class="sxs-lookup"><span data-stu-id="ad25f-132">3.0.0 (06/19/2015)</span></span>
* <span data-ttu-id="ad25f-133">Mobile Engagement sessiz anında iletme bildirimleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="ad25f-133">Mobile Engagement uses Silent Push Notifications.</span></span>
* <span data-ttu-id="ad25f-134">İOS için destek bırakılan 4.X.</span><span class="sxs-lookup"><span data-stu-id="ad25f-134">Dropped support for iOS 4.X.</span></span> <span data-ttu-id="ad25f-135">Bu sürüm hello dağıtım hedefi, uygulamanızın başlangıç olmalıdır en az iOS 6.</span><span class="sxs-lookup"><span data-stu-id="ad25f-135">Starting from this version hello deployment target of your application must be at least iOS 6.</span></span>

## <a name="220-05212015"></a><span data-ttu-id="ad25f-136">2.2.0 (05/21/2015)</span><span class="sxs-lookup"><span data-stu-id="ad25f-136">2.2.0 (05/21/2015)</span></span>
* <span data-ttu-id="ad25f-137">Merhaba Mobile Engagement cihaz kimliği cihazlar için < iOS 6 yükleme sırasında oluşturulan GUID şimdi dayanır.</span><span class="sxs-lookup"><span data-stu-id="ad25f-137">hello Mobile Engagement device id for devices < iOS 6 is now based on a GUID generated at installation time.</span></span>

## <a name="210-04242015"></a><span data-ttu-id="ad25f-138">2.1.0 (04/24/2015)</span><span class="sxs-lookup"><span data-stu-id="ad25f-138">2.1.0 (04/24/2015)</span></span>
* <span data-ttu-id="ad25f-139">SWIFT uyumluluk eklendi.</span><span class="sxs-lookup"><span data-stu-id="ad25f-139">Added Swift compatibility.</span></span>
* <span data-ttu-id="ad25f-140">Hello uygulama açtıktan sonra bir bildirim tıklandığında, sağ URL sunulmuştur hello eylem yürütüldü.</span><span class="sxs-lookup"><span data-stu-id="ad25f-140">When clicking on a notification, hello action URL is now executed right after hello application is opened.</span></span>
* <span data-ttu-id="ad25f-141">Eklenen eksik üstbilgi dosyasında SDK paketi.</span><span class="sxs-lookup"><span data-stu-id="ad25f-141">Added missing header file in SDK package.</span></span>
* <span data-ttu-id="ad25f-142">Merhaba Mobile Engagement kilitlenme Raporlayıcı devre dışı bırakıldığında bir sorun düzeltilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ad25f-142">Fixed an issue when hello Mobile Engagement crash reporter was disabled.</span></span>

## <a name="200-02172015"></a><span data-ttu-id="ad25f-143">2.0.0 (02/17/2015)</span><span class="sxs-lookup"><span data-stu-id="ad25f-143">2.0.0 (02/17/2015)</span></span>
* <span data-ttu-id="ad25f-144">Azure Mobile Engagement ilk sürümünü</span><span class="sxs-lookup"><span data-stu-id="ad25f-144">Initial Release of Azure Mobile Engagement</span></span>
* <span data-ttu-id="ad25f-145">AppID/sdkKey yapılandırma bağlantı dizesini yapılandırma tarafından değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="ad25f-145">appId/sdkKey configuration is replaced by a connection string configuration.</span></span>
* <span data-ttu-id="ad25f-146">Rastgele XMPP varlıklardan rasgele XMPP ileti alıp API toosend kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="ad25f-146">Removed API toosend and receive arbitrary XMPP messages from arbitrary XMPP entities.</span></span>
* <span data-ttu-id="ad25f-147">Cihazlar arasında ileti alıp API toosend kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="ad25f-147">Removed API toosend and receive messages between devices.</span></span>
* <span data-ttu-id="ad25f-148">Güvenlik geliştirmeleri.</span><span class="sxs-lookup"><span data-stu-id="ad25f-148">Security improvements.</span></span>
* <span data-ttu-id="ad25f-149">SmartAd izleme kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="ad25f-149">SmartAd tracking removed.</span></span>
