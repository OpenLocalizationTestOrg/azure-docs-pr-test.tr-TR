---
title: "Azure Mobile Engagement Android SDK tümleştirmesi"
description: "En son güncelleştirmeler ve yordamlar için Azure Mobile Engagement Android SDK"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 585341f9-3f39-459a-af42-864e400a0128
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: c179c39a43da0aa35e945acceacbf27fe8e328f3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="release-notes"></a><span data-ttu-id="2415f-103">Sürüm notları</span><span class="sxs-lookup"><span data-stu-id="2415f-103">Release notes</span></span>

## <a name="431-07172017"></a><span data-ttu-id="2415f-104">4.3.1 (07/17/2017)</span><span class="sxs-lookup"><span data-stu-id="2415f-104">4.3.1 (07/17/2017)</span></span>
* <span data-ttu-id="2415f-105">Çağrılırken nadiren bir kilitlenme düzeltme `EngagementAgentUtils.isInDedicatedEngagementProcess`, ayrıca kullanılan tarafından `EngagementApplication` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="2415f-105">Fix a crash that could rarely happen when calling `EngagementAgentUtils.isInDedicatedEngagementProcess`, which is also used by the `EngagementApplication` class.</span></span>

## <a name="430-06272017"></a><span data-ttu-id="2415f-106">4.3.0 (06/27/2017)</span><span class="sxs-lookup"><span data-stu-id="2415f-106">4.3.0 (06/27/2017)</span></span>
* <span data-ttu-id="2415f-107">Android 8 desteği (SDK'ın önceki sürümleri üzerinde Android 8 çalışmaz).</span><span class="sxs-lookup"><span data-stu-id="2415f-107">Android 8 support (previous versions of the SDK will not work on Android 8).</span></span>
* <span data-ttu-id="2415f-108">Daha fazla hiçbir bağımlılık destek kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="2415f-108">No more dependency on support library.</span></span>
* <span data-ttu-id="2415f-109">Kaldırma `EngagementFragmentActivity` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="2415f-109">Remove `EngagementFragmentActivity` class.</span></span>
* <span data-ttu-id="2415f-110">Nedeniyle [arka plan yürütme sınırları](https://developer.android.com/preview/features/background.html) arka planda günlükleri Android 8'de kullanıcı aygıt ile etkileşim kadar gecikebilir, bu bir itme kampanya etkileyecek **teslim edildi** ve **sistem bildirimi görüntülenir** Aygıt uyku durumunda erteleniyor istatistikleri (bildirim görüntülenmeye devam eder, halka ve gerçek zamanlı sorun olmadan Titret).</span><span class="sxs-lookup"><span data-stu-id="2415f-110">Due to [Background Execution Limits](https://developer.android.com/preview/features/background.html) on Android 8, logs in background might be delayed until the user interacts with the device, this will have an impact on Push Campaign **Delivered** and **System notification displayed** statistics being delayed if the device was sleeping (the notification will still be displayed, will ring and vibrate in real time without issues).</span></span>
* <span data-ttu-id="2415f-111">Nedeniyle [arka plan konum sınırları](https://developer.android.com/preview/features/background-location-limits.html), arka plan konumda güncelleştirilmeyecek sık üzerinde Android 8 gerçek zamanlı.</span><span class="sxs-lookup"><span data-stu-id="2415f-111">Due to [Background Location Limits](https://developer.android.com/preview/features/background-location-limits.html), the real time location in background will not be updated frequently on Android 8.</span></span>

## <a name="424-03302017"></a><span data-ttu-id="2415f-112">4.2.4 (03/30/2017)</span><span class="sxs-lookup"><span data-stu-id="2415f-112">4.2.4 (03/30/2017)</span></span>
* <span data-ttu-id="2415f-113">Uygulama içi bildirim metin renkleri Android 7 eski Android sürümleri ile aynı olacak şekilde düzeltin.</span><span class="sxs-lookup"><span data-stu-id="2415f-113">Fix in-app notification text colors on Android 7 to be the same as older Android versions.</span></span>

## <a name="423-08102016"></a><span data-ttu-id="2415f-114">4.2.3 (08/10/2016)</span><span class="sxs-lookup"><span data-stu-id="2415f-114">4.2.3 (08/10/2016)</span></span>
* <span data-ttu-id="2415f-115">Daha fazla WIFI kilit yok.</span><span class="sxs-lookup"><span data-stu-id="2415f-115">No more WIFI lock.</span></span>
* <span data-ttu-id="2415f-116">Init (hata 4.2.0 içinde sunulan) önce getDeviceId çağrılırken bir kilitlenme düzeltin.</span><span class="sxs-lookup"><span data-stu-id="2415f-116">Fix a deadlock when calling getDeviceId before init (bug introduced in 4.2.0).</span></span>

## <a name="422-05172016"></a><span data-ttu-id="2415f-117">4.2.2 (05/17/2016)</span><span class="sxs-lookup"><span data-stu-id="2415f-117">4.2.2 (05/17/2016)</span></span>
* <span data-ttu-id="2415f-118">İstikrara yönelik iyileştirmeler.</span><span class="sxs-lookup"><span data-stu-id="2415f-118">Stability improvements.</span></span>

## <a name="421-05102016"></a><span data-ttu-id="2415f-119">4.2.1 (05/10/2016)</span><span class="sxs-lookup"><span data-stu-id="2415f-119">4.2.1 (05/10/2016)</span></span>
* <span data-ttu-id="2415f-120">Güvenlik: web görünümü yerel dosya erişimini devre dışı bırakın.</span><span class="sxs-lookup"><span data-stu-id="2415f-120">Security: disable web view local file access.</span></span>
* <span data-ttu-id="2415f-121">Güvenliği: kaldırma `EngagementPreferenceActivity` artık kullanılmayan ve güvenli olmayan genişleten sınıf `PreferenceActivity` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="2415f-121">Security: remove `EngagementPreferenceActivity` class that extends obsolete and unsecure `PreferenceActivity` class.</span></span>
* <span data-ttu-id="2415f-122">Güvenlik: etkinlikleri kullanmak için şimdi belgelenmiştir ulaşma `exported="false"`, bu bayrak, önceki SDK sürümlerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2415f-122">Security: reach activities are now documented to use `exported="false"`, this flag can also be used in previous SDK versions.</span></span>

## <a name="420-03112016"></a><span data-ttu-id="2415f-123">4.2.0 (03/11/2016)</span><span class="sxs-lookup"><span data-stu-id="2415f-123">4.2.0 (03/11/2016)</span></span>
* <span data-ttu-id="2415f-124">SDK şimdi MIT altında lisanslanmıştır.</span><span class="sxs-lookup"><span data-stu-id="2415f-124">The SDK is now licensed under MIT.</span></span>
* <span data-ttu-id="2415f-125">Bir özel cihaz tanımlayıcısı SDK başlatma zamanında belirtmeye izin.</span><span class="sxs-lookup"><span data-stu-id="2415f-125">Allow specifying a custom device identifier at SDK initialization time.</span></span>

## <a name="415-02012016"></a><span data-ttu-id="2415f-126">4.1.5 (02/01/2016)</span><span class="sxs-lookup"><span data-stu-id="2415f-126">4.1.5 (02/01/2016)</span></span>
* <span data-ttu-id="2415f-127">İstikrara yönelik iyileştirmeler.</span><span class="sxs-lookup"><span data-stu-id="2415f-127">Stability improvements.</span></span>

## <a name="414-01262016"></a><span data-ttu-id="2415f-128">4.1.4 (01/26/2016)</span><span class="sxs-lookup"><span data-stu-id="2415f-128">4.1.4 (01/26/2016)</span></span>
* <span data-ttu-id="2415f-129">İstikrara yönelik iyileştirmeler.</span><span class="sxs-lookup"><span data-stu-id="2415f-129">Stability improvements.</span></span>

## <a name="413-1292015"></a><span data-ttu-id="2415f-130">4.1.3 (12/9/2015)</span><span class="sxs-lookup"><span data-stu-id="2415f-130">4.1.3 (12/9/2015)</span></span>
* <span data-ttu-id="2415f-131">İstikrara yönelik iyileştirmeler.</span><span class="sxs-lookup"><span data-stu-id="2415f-131">Stability improvements.</span></span>

## <a name="412-11252015"></a><span data-ttu-id="2415f-132">4.1.2 (11/25/2015)</span><span class="sxs-lookup"><span data-stu-id="2415f-132">4.1.2 (11/25/2015)</span></span>
* <span data-ttu-id="2415f-133">İstikrara yönelik iyileştirmeler.</span><span class="sxs-lookup"><span data-stu-id="2415f-133">Stability improvements.</span></span>

## <a name="411-11042015"></a><span data-ttu-id="2415f-134">4.1.1 (11/04/2015)</span><span class="sxs-lookup"><span data-stu-id="2415f-134">4.1.1 (11/04/2015)</span></span>
* <span data-ttu-id="2415f-135">İstikrara yönelik iyileştirmeler.</span><span class="sxs-lookup"><span data-stu-id="2415f-135">Stability improvements.</span></span>

## <a name="410-08252015"></a><span data-ttu-id="2415f-136">4.1.0 (08/25/2015)</span><span class="sxs-lookup"><span data-stu-id="2415f-136">4.1.0 (08/25/2015)</span></span>
* <span data-ttu-id="2415f-137">Yeni izni modeli için Android M işleyin.</span><span class="sxs-lookup"><span data-stu-id="2415f-137">Handle new permission model for Android M.</span></span>
* <span data-ttu-id="2415f-138">Yerine çalışma zamanında konumu özellikleri artık yapılandırabilirsiniz `AndroidManifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="2415f-138">Can now configure location features at runtime instead of using  `AndroidManifest.xml`.</span></span>
* <span data-ttu-id="2415f-139">Bir izin hatayı düzeltmek: kullanırsanız `ACCESS_FINE_LOCATION`, ardından `ACCESS_COARSE_LOCATION` artık gerekli değildir.</span><span class="sxs-lookup"><span data-stu-id="2415f-139">Fix a permission bug: if you use `ACCESS_FINE_LOCATION`, then `ACCESS_COARSE_LOCATION` is not needed anymore.</span></span>
* <span data-ttu-id="2415f-140">İstikrara yönelik iyileştirmeler.</span><span class="sxs-lookup"><span data-stu-id="2415f-140">Stability improvements.</span></span>

## <a name="400-07062015"></a><span data-ttu-id="2415f-141">4.0.0 (07/06/2015)</span><span class="sxs-lookup"><span data-stu-id="2415f-141">4.0.0 (07/06/2015)</span></span>
* <span data-ttu-id="2415f-142">Analizler ve anında iletme daha güvenilir sağlamak için iç protokol değişiklikleri.</span><span class="sxs-lookup"><span data-stu-id="2415f-142">Internal protocol changes to make analytics and push more reliable.</span></span>
* <span data-ttu-id="2415f-143">İtme kampanya herhangi bir türde yerel gönderim kimlik bilgilerini yapılandırmak için yerel gönderim (GCM/ADM) şimdi de için uygulama içi Bildirimlerde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2415f-143">Native push (GCM/ADM) is now also used for in app notifications so you must configure the native push credentials for any type of push campaign.</span></span>
* <span data-ttu-id="2415f-144">Büyük resim bildirim düzeltin: gönderilen sonra görüntülenen yalnızca 10'luk oldukları.</span><span class="sxs-lookup"><span data-stu-id="2415f-144">Fix big picture notification: they were displayed only 10s after being pushed.</span></span>
* <span data-ttu-id="2415f-145">Web görünümünde bir hatayı düzeltmek: bir bağlantıyı tıklatmak olduğu da yürütülürken varsayılan eylem URL'si.</span><span class="sxs-lookup"><span data-stu-id="2415f-145">Fix a bug in web view: clicking on a link was also executing the default action URL.</span></span>
* <span data-ttu-id="2415f-146">Yerel depolama yönetimiyle ilgili nadir bir kilitlenme düzeltin.</span><span class="sxs-lookup"><span data-stu-id="2415f-146">Fix a rare crash related to local storage management.</span></span>
* <span data-ttu-id="2415f-147">Dinamik yapılandırma dizesi yönetim düzeltin.</span><span class="sxs-lookup"><span data-stu-id="2415f-147">Fix dynamic configuration string management.</span></span>
* <span data-ttu-id="2415f-148">EULA güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="2415f-148">Update EULA.</span></span>

## <a name="300-02172015"></a><span data-ttu-id="2415f-149">3.0.0 (02/17/2015)</span><span class="sxs-lookup"><span data-stu-id="2415f-149">3.0.0 (02/17/2015)</span></span>
* <span data-ttu-id="2415f-150">Azure Mobile Engagement ilk sürümünü</span><span class="sxs-lookup"><span data-stu-id="2415f-150">Initial Release of Azure Mobile Engagement</span></span>
* <span data-ttu-id="2415f-151">AppID yapılandırma bağlantı dizesini yapılandırma tarafından değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="2415f-151">appId configuration is replaced by a connection string configuration.</span></span>
* <span data-ttu-id="2415f-152">Rastgele XMPP varlıklardan rasgele XMPP ileti alıp göndermek için API kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="2415f-152">Removed API to send and receive arbitrary XMPP messages from arbitrary XMPP entities.</span></span>
* <span data-ttu-id="2415f-153">Cihazlar arasında ileti gönderme ve alma için API kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="2415f-153">Removed API to send and receive messages between devices.</span></span>
* <span data-ttu-id="2415f-154">Güvenlik geliştirmeleri.</span><span class="sxs-lookup"><span data-stu-id="2415f-154">Security improvements.</span></span>
* <span data-ttu-id="2415f-155">Google Play ve SmartAd izleme kaldırıldı.</span><span class="sxs-lookup"><span data-stu-id="2415f-155">Google Play and SmartAd tracking removed.</span></span>

