---
title: "Sorun giderme kılavuzu - SDK'sı azure Mobile Engagement"
description: "Azure Mobile Engagement SDK tümleştirmesi sorunlarını giderme"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: de265cf1-2f88-43ef-8616-156ada5be7b6
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4d9d6165deb4bd0c65f1841aa7c457363a1f2865
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-for-sdk-integration-issues"></a><span data-ttu-id="949ad-103">SDK tümleştirme sorunları için sorun giderme kılavuzu</span><span class="sxs-lookup"><span data-stu-id="949ad-103">Troubleshooting guide for SDK integration issues</span></span>
<span data-ttu-id="949ad-104">Azure Mobile Engagement'ın uygulamanıza nasıl tümleştirilir karşılaşabileceğiniz olası sorunlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="949ad-104">The following are possible issues you may encounter with how Azure Mobile Engagement integrates into your application.</span></span>

## <a name="sdk-issues-discovered-by-a-failure-in-another-area-of-your-application"></a><span data-ttu-id="949ad-105">Bir hata, uygulamanızın başka bir alan keşfedilen SDK sorunları</span><span class="sxs-lookup"><span data-stu-id="949ad-105">SDK issues discovered by a failure in another area of your application</span></span>
### <a name="issue"></a><span data-ttu-id="949ad-106">Sorun</span><span class="sxs-lookup"><span data-stu-id="949ad-106">Issue</span></span>
* <span data-ttu-id="949ad-107">UI veri toplama hatası (Analytics, izleme, Segment veya panolar).</span><span class="sxs-lookup"><span data-stu-id="949ad-107">UI data collection failure (in Analytics, Monitoring, Segmentation, or Dashboards).</span></span>
* <span data-ttu-id="949ad-108">Hataları gönderme (uygulama ya da her ikisini de dışında uygulamasında iter çalışmıyor).</span><span class="sxs-lookup"><span data-stu-id="949ad-108">Push Failures (Pushes don't work in app, out of app, or both).</span></span>
* <span data-ttu-id="949ad-109">Özellik hataları (izleme, coğrafi konuma veya belirli iter çalışmıyor platform) Gelişmiş.</span><span class="sxs-lookup"><span data-stu-id="949ad-109">Advanced Feature Failures (Tracking, Geolocation, or platform specific Pushes don’t work).</span></span>
* <span data-ttu-id="949ad-110">API hataları (API'leri başarısız genellikle hata iletileri olmadan sessizce).</span><span class="sxs-lookup"><span data-stu-id="949ad-110">API Failures (APIs fail often silently without error messages).</span></span>
* <span data-ttu-id="949ad-111">Hizmet hataları (hiçbiri Azure Mobile Engagement uygulamanız için çalışır).</span><span class="sxs-lookup"><span data-stu-id="949ad-111">Service Failures (none of Azure Mobile Engagement works for your application).</span></span>

### <a name="causes"></a><span data-ttu-id="949ad-112">Neden olur.</span><span class="sxs-lookup"><span data-stu-id="949ad-112">Causes</span></span>
* <span data-ttu-id="949ad-113">Uygulamanız (örneğin, bir kullanıcı Arabirimi veri toplama hatası, gönderme hatası, gelişmiş özellik hatası, API hatası, uygulama kilitlenmelerine veya görünen hizmet kesintisi) bir hata ile Azure Mobile Engagement SDK'sı çözülmesi gereken çoğu sorunları bulunacaktır.</span><span class="sxs-lookup"><span data-stu-id="949ad-113">Most issues that need to be resolved with the Azure Mobile Engagement SDK will be discovered by a failure in your application (such as a UI data collection failure, push failure, advanced feature failure, API failure, Application crashes, or apparent service outage).</span></span>  
* <span data-ttu-id="949ad-114">Azure Mobile Engagement, belirli bir özellik, hiçbir zaman uygulamanızda önce çalıştıysa tümleştirme tamamlanması gerekir.</span><span class="sxs-lookup"><span data-stu-id="949ad-114">If a particular feature of Azure Mobile Engagement has never worked in your app before, you will need to complete the integration.</span></span> 
* <span data-ttu-id="949ad-115">Azure Mobile Engagement, belirli bir özellik çalıştığı ve durdurulmuş, en son Azure Mobile Engagement SDK'sı sürüm yükseltmeniz gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="949ad-115">If a particular feature of Azure Mobile Engagement was working and stopped, you may need to upgrade to the last version with the Azure Mobile Engagement SDK.</span></span> <span data-ttu-id="949ad-116">Azure Mobile Engagement (Android, iOS, Windows ve Windows Phone) tarafından desteklenen her platform için Azure Mobile Engagement SDK'sı farklı bir sürümü olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="949ad-116">Remember that there is a different version of the Azure Mobile Engagement SDK for each platform supported by Azure Mobile Engagement (Android, iOS, Windows, and Windows Phone).</span></span>

#### <a name="sdk-integration"></a><span data-ttu-id="949ad-117">SDK Tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="949ad-117">SDK Integration</span></span>
* <span data-ttu-id="949ad-118">Azure Mobile Engagement SDK'yı (Analytics) doğru biçimde tümleşik.</span><span class="sxs-lookup"><span data-stu-id="949ad-118">Azure Mobile Engagement not correctly integrated in SDK (Analytics).</span></span>
* <span data-ttu-id="949ad-119">SDK (uygulama içinde ve dışında uygulama iter) doğru biçimde tümleşik ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="949ad-119">Reach not correctly integrated in SDK (In App and Out of App Pushes).</span></span>
* <span data-ttu-id="949ad-120">Süresi dolmuş veya hatalı ürün vs sertifika. Geliştirme (yalnızca iOS).</span><span class="sxs-lookup"><span data-stu-id="949ad-120">Certificate expired or incorrect PROD vs. DEV (iOS only).</span></span>
* <span data-ttu-id="949ad-121">GCM veya ADM SDK'da tümleşik doğru biçimde (Android yalnızca - hizmet belirli iter).</span><span class="sxs-lookup"><span data-stu-id="949ad-121">GCM or ADM not correctly integrated in SDK (Android only - Service Specific Pushes).</span></span>
* <span data-ttu-id="949ad-122">Doğru biçimde izleme SDK (yükleme deposu izleme) tümleşiktir.</span><span class="sxs-lookup"><span data-stu-id="949ad-122">Tracking not correctly integrated in SDK (Install store tracking).</span></span>
* <span data-ttu-id="949ad-123">Yavaş veya GPS yerleşimine SDK (hedefleme coğrafi konuma göre) doğru biçimde tümleşik.</span><span class="sxs-lookup"><span data-stu-id="949ad-123">Lazy Location or GPS Location not correctly integrated in SDK (Targeting by geo-location).</span></span>

<span data-ttu-id="949ad-124">**Ayrıca bkz.:**</span><span class="sxs-lookup"><span data-stu-id="949ad-124">**See also:**</span></span>

* <span data-ttu-id="949ad-125">[SDK Belgeleri - tümleştirme kılavuzları][Link 5]</span><span class="sxs-lookup"><span data-stu-id="949ad-125">[SDK Documentation - Integration Guides][Link 5]</span></span> 
* <span data-ttu-id="949ad-126">[Sorun giderme kılavuzu - gönderme][Link 23]</span><span class="sxs-lookup"><span data-stu-id="949ad-126">[Troubleshooting Guide - Push][Link 23]</span></span>

#### <a name="sdk-upgrade"></a><span data-ttu-id="949ad-127">SDK yükseltme</span><span class="sxs-lookup"><span data-stu-id="949ad-127">SDK Upgrade</span></span>
* <span data-ttu-id="949ad-128">SDK'sını (genellikle daha yeni sürümleri aygıt işletim sistemi için ilgili) SDK'ın eski sürümleri ile ilgili sorunları gidermek yükseltme yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="949ad-128">Need to upgrade SDK to resolve issues with older versions of the SDK (often related to newer versions of the device OS).</span></span>
* <span data-ttu-id="949ad-129">Cihazınızı uygulamanızı önceki tüm sürümlerini kaldırın ve en yeni sürümü, uygulamanızın, yeniden kaydettirin Cihazınızı uygulamanızı en yeni sürümünü kullandığını doğrulamak için Azure Mobile Engagement UI, cihaz kimliği yükleyin.</span><span class="sxs-lookup"><span data-stu-id="949ad-129">Uninstall all previous versions of your app from your device and reinstall the newest version of your app, the re-register your Device ID from the Azure Mobile Engagement UI to confirm that your device is using the newest version of your app.</span></span>

<span data-ttu-id="949ad-130">**Ayrıca bkz.:**</span><span class="sxs-lookup"><span data-stu-id="949ad-130">**See also:**</span></span>

* [<span data-ttu-id="949ad-131">SDK Belgeleri - sürüm notları</span><span class="sxs-lookup"><span data-stu-id="949ad-131">SDK Documentation - Release Notes</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554) 
* [<span data-ttu-id="949ad-132">SDK Belgeleri - yükseltme kılavuzları</span><span class="sxs-lookup"><span data-stu-id="949ad-132">SDK Documentation - Upgrade Guides</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554)

#### <a name="sdk-other"></a><span data-ttu-id="949ad-133">SDK diğer</span><span class="sxs-lookup"><span data-stu-id="949ad-133">SDK Other</span></span>
* <span data-ttu-id="949ad-134">Uygulama bildirimi "AndroidManifest.xml" hataları Azure Mobile Engagement'ı (yalnızca Android) çalışmamasına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="949ad-134">Errors in Application Manifest "AndroidManifest.xml" can cause Azure Mobile Engagement not to work (Android only).</span></span>
* <span data-ttu-id="949ad-135">SDK anahtarı ve API anahtarını karmaşık hale getirmeye SDK tümleştirmesi ve API kullanımı ile yaygın bir sorun var.</span><span class="sxs-lookup"><span data-stu-id="949ad-135">A common issue with SDK integration and API usage is to confuse the SDK Key and the API Key.</span></span>

<span data-ttu-id="949ad-136">**Ayrıca bkz.:**</span><span class="sxs-lookup"><span data-stu-id="949ad-136">**See also:**</span></span>

* <span data-ttu-id="949ad-137">[Kavramlar - sözlüğü][Link 6]</span><span class="sxs-lookup"><span data-stu-id="949ad-137">[Concepts - Glossary][Link 6]</span></span>

## <a name="advanced-coding-issues"></a><span data-ttu-id="949ad-138">Sorunları kodlama Gelişmiş</span><span class="sxs-lookup"><span data-stu-id="949ad-138">Advanced coding issues</span></span>
### <a name="issue"></a><span data-ttu-id="949ad-139">Sorun</span><span class="sxs-lookup"><span data-stu-id="949ad-139">Issue</span></span>
* <span data-ttu-id="949ad-140">İOS, Android ve Windows Phone platform belirli kodu doğrudan Azure Mobile Engagement için ilgili sorunlara neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="949ad-140">Platform specific code not directly related to Azure Mobile Engagement can cause issues on iOS, Android, and Windows Phone.</span></span>

### <a name="causes"></a><span data-ttu-id="949ad-141">Neden olur.</span><span class="sxs-lookup"><span data-stu-id="949ad-141">Causes</span></span>
* <span data-ttu-id="949ad-142">Birçok Azure Mobile Engagement kodlama sorunları Gelişmiş nedeni yanlış yazılmış platform belirli kodu Azure Mobile Engagement için doğrudan ilgili değildir.</span><span class="sxs-lookup"><span data-stu-id="949ad-142">Many advanced coding issues with Azure Mobile Engagement are caused by improperly written platform specific code not directly related to Azure Mobile Engagement.</span></span> <span data-ttu-id="949ad-143">Azure Mobile Engagement belgeleri (Android, iOS, Web, Windows ve Windows Phone) yanı sıra için geliştirdiğiniz platformu belirli belgelere gerekecektir.</span><span class="sxs-lookup"><span data-stu-id="949ad-143">You will need to consult documentation specific to the platform you are developing for in addition to Azure Mobile Engagement documentation (Android, iOS, Web, Windows, and Windows Phone).</span></span>
* <span data-ttu-id="949ad-144">Doğru biçimde "Kategoriler" yapılandırma, başka bir konum içinde veya dışında (yalnızca Android) uygulama bildirimden bağlanma engeller.</span><span class="sxs-lookup"><span data-stu-id="949ad-144">Not correctly configuring "categories", prevents linking from a notification to another location either inside or outside of the app (Android only).</span></span> 
* <span data-ttu-id="949ad-145">"UIKit.framework" "isteğe bağlı" "simgesi bulunamadı hatası" gösterir, iOS kodunuzun ayarını değil ve/veya eski iOS cihazlarda (yalnızca iOS) çöküyor.</span><span class="sxs-lookup"><span data-stu-id="949ad-145">Not setting "UIKit.framework" to "optional" in your iOS code, shows a "Symbol not found error" and/or crashes on older iOS devices (iOS only).</span></span>
* <span data-ttu-id="949ad-146">Süresi dolan sertifikaları veya doğru biçimde nedenler cert geliştirme veya üretim sürümünü kullanarak anında iletme (yalnızca iOS) verir.</span><span class="sxs-lookup"><span data-stu-id="949ad-146">Expired certificates or not correctly using the DEV or Prod version of the cert, causes push issues (iOS only).</span></span>
* <span data-ttu-id="949ad-147">Devralınan (system center için uygulamanın oturumunu işleyişi Android ve iOS iter gibi), Azure Mobile Engagement denetleyemezsiniz bir platform için bazı sınırlamalar vardır.</span><span class="sxs-lookup"><span data-stu-id="949ad-147">There are some limitations inherent to a platform that Azure Mobile Engagement can't control (like how the system center works for out of app pushes in Android and iOS).</span></span>
* <span data-ttu-id="949ad-148">Azure Mobile Engagement tam başvuru için iOS ve Android için Azure Mobile Engagement tarafından kullanılan iç paketlerin listesini yayımlar.</span><span class="sxs-lookup"><span data-stu-id="949ad-148">Azure Mobile Engagement publishes a full list of the internal packages used by Azure Mobile Engagement for iOS and Android for reference.</span></span> <span data-ttu-id="949ad-149">Azure Mobile Engagement özelliklerinden bazıları (Android, iOS, Web, Windows ve Windows Phone) platforma özgü aklınızda bulundurun.</span><span class="sxs-lookup"><span data-stu-id="949ad-149">Keep in mind that some features of Azure Mobile Engagement are specific to the platform (Android, iOS, Web, Windows, and Windows Phone).</span></span>

### <a name="see-also"></a><span data-ttu-id="949ad-150">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="949ad-150">See also</span></span>
* <span data-ttu-id="949ad-151">[Sorun giderme kılavuzu - gönderme][Link 23]</span><span class="sxs-lookup"><span data-stu-id="949ad-151">[Troubleshooting Guide - Push][Link 23]</span></span> 
* <span data-ttu-id="949ad-152">[SDK Belgeleri - sürüm notları][Link 5]</span><span class="sxs-lookup"><span data-stu-id="949ad-152">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="949ad-153">[SDK Belgeleri - yükseltme kılavuzları][Link 5]</span><span class="sxs-lookup"><span data-stu-id="949ad-153">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="application-crashes"></a><span data-ttu-id="949ad-154">Uygulama çökme (Crash)</span><span class="sxs-lookup"><span data-stu-id="949ad-154">Application crashes</span></span>
### <a name="issue"></a><span data-ttu-id="949ad-155">Sorun</span><span class="sxs-lookup"><span data-stu-id="949ad-155">Issue</span></span>
* <span data-ttu-id="949ad-156">Uygulamanız son kullanıcıların cihazda çöküyor.</span><span class="sxs-lookup"><span data-stu-id="949ad-156">Your application crashes on the end users' device.</span></span>

### <a name="causes"></a><span data-ttu-id="949ad-157">Neden olur.</span><span class="sxs-lookup"><span data-stu-id="949ad-157">Causes</span></span>
* <span data-ttu-id="949ad-158">Kilitlenme bilgi görüntülenebilir *Analytics UI* veya *Analytics API*</span><span class="sxs-lookup"><span data-stu-id="949ad-158">Crash information can be viewed in the *Analytics UI* or the *Analytics API*</span></span>
* <span data-ttu-id="949ad-159">Test Cihazınızı cihaz Kimliğini bulun ve kilitlenme uygulamanıza, kilitlenme nedenini belirlemeye yardımcı olmak bir son kullanıcı için neden aynı adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="949ad-159">You can find the Device ID of your test device and take the same action that caused your application to crash for an end user to help identify the cause of your crash.</span></span>
* <span data-ttu-id="949ad-160">Azure Mobile Engagement SDK'sı uygulamaların kilitlenmesine neden bilinen sorunlar bazen SDK'ın en son sürüme yükseltme tarafından çözümlenir.</span><span class="sxs-lookup"><span data-stu-id="949ad-160">Known issues with the Azure Mobile Engagement SDK that cause applications to crash are sometimes resolved by upgrading to the latest version of the SDK.</span></span> <span data-ttu-id="949ad-161">Sürüm Notları platformunuz hakkında kilitlenme araştırırken olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="949ad-161">Make sure to check the release notes about your platform when investigating crashes.</span></span>

### <a name="see-also"></a><span data-ttu-id="949ad-162">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="949ad-162">See also</span></span>
* <span data-ttu-id="949ad-163">[SDK Belgeleri - sürüm notları][Link 5]</span><span class="sxs-lookup"><span data-stu-id="949ad-163">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="949ad-164">[SDK Belgeleri - yükseltme kılavuzları][Link 5]</span><span class="sxs-lookup"><span data-stu-id="949ad-164">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="app-store-upload-failures"></a><span data-ttu-id="949ad-165">Uygulama mağazası karşıya yükleme hataları</span><span class="sxs-lookup"><span data-stu-id="949ad-165">App store upload failures</span></span>
### <a name="issue"></a><span data-ttu-id="949ad-166">Sorun</span><span class="sxs-lookup"><span data-stu-id="949ad-166">Issue</span></span>
* <span data-ttu-id="949ad-167">Apple, Google veya Windows uygulama mağazası uygulamanızı en son sürümünü yükleme için ilgili hatalar.</span><span class="sxs-lookup"><span data-stu-id="949ad-167">Errors related to uploading the latest version of your app to Apple, Google, or the Windows App store.</span></span>

### <a name="causes"></a><span data-ttu-id="949ad-168">Neden olur.</span><span class="sxs-lookup"><span data-stu-id="949ad-168">Causes</span></span>
* <span data-ttu-id="949ad-169">Uygulama mağazaları bazen belirli özellikleri etkin blok uygulamalar (örneğin Apple Store Mağazası'ndaki uygulamaların IDFV kullanımda ve uygulamalar arasında uygulama bilgi paylaşımı GooglePlay deposu engeller).</span><span class="sxs-lookup"><span data-stu-id="949ad-169">App stores sometimes block apps with certain features enabled (e.g. the Apple Store prevents the use of IDFV in apps in the store and the GooglePlay store prevents the sharing of application information between apps).</span></span> 
* <span data-ttu-id="949ad-170">Depoya bir uygulama karşıya güçlük çekiyorsanız, platform ve SDK'ın geçerli sürümü ile ilgili sürüm notları denetlediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="949ad-170">Make sure that you check the release notes about your platform and current version of the SDK if you have difficulty uploading an app to the store.</span></span>

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/en-us/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/en-us/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/en-us/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

