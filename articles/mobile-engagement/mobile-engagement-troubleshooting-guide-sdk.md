---
title: "aaaAzure Mobile Engagement sorun giderme kılavuzu - SDK"
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
ms.openlocfilehash: 1c082b81d898f4bdb47b8efe6cfbacfd83fe9279
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-sdk-integration-issues"></a><span data-ttu-id="d4c9e-103">SDK tümleştirme sorunları için sorun giderme kılavuzu</span><span class="sxs-lookup"><span data-stu-id="d4c9e-103">Troubleshooting guide for SDK integration issues</span></span>
<span data-ttu-id="d4c9e-104">Merhaba, nasıl Azure Mobile Engagement uygulamanıza ile tümleşir karşılaşabileceğiniz olası sorunlar şunlardır.</span><span class="sxs-lookup"><span data-stu-id="d4c9e-104">hello following are possible issues you may encounter with how Azure Mobile Engagement integrates into your application.</span></span>

## <a name="sdk-issues-discovered-by-a-failure-in-another-area-of-your-application"></a><span data-ttu-id="d4c9e-105">Bir hata, uygulamanızın başka bir alan keşfedilen SDK sorunları</span><span class="sxs-lookup"><span data-stu-id="d4c9e-105">SDK issues discovered by a failure in another area of your application</span></span>
### <a name="issue"></a><span data-ttu-id="d4c9e-106">Sorun</span><span class="sxs-lookup"><span data-stu-id="d4c9e-106">Issue</span></span>
* <span data-ttu-id="d4c9e-107">UI veri toplama hatası (Analytics, izleme, Segment veya panolar).</span><span class="sxs-lookup"><span data-stu-id="d4c9e-107">UI data collection failure (in Analytics, Monitoring, Segmentation, or Dashboards).</span></span>
* <span data-ttu-id="d4c9e-108">Hataları gönderme (uygulama ya da her ikisini de dışında uygulamasında iter çalışmıyor).</span><span class="sxs-lookup"><span data-stu-id="d4c9e-108">Push Failures (Pushes don't work in app, out of app, or both).</span></span>
* <span data-ttu-id="d4c9e-109">Özellik hataları (izleme, coğrafi konuma veya belirli iter çalışmıyor platform) Gelişmiş.</span><span class="sxs-lookup"><span data-stu-id="d4c9e-109">Advanced Feature Failures (Tracking, Geolocation, or platform specific Pushes don’t work).</span></span>
* <span data-ttu-id="d4c9e-110">API hataları (API'leri başarısız genellikle hata iletileri olmadan sessizce).</span><span class="sxs-lookup"><span data-stu-id="d4c9e-110">API Failures (APIs fail often silently without error messages).</span></span>
* <span data-ttu-id="d4c9e-111">Hizmet hataları (hiçbiri Azure Mobile Engagement uygulamanız için çalışır).</span><span class="sxs-lookup"><span data-stu-id="d4c9e-111">Service Failures (none of Azure Mobile Engagement works for your application).</span></span>

### <a name="causes"></a><span data-ttu-id="d4c9e-112">Neden olur.</span><span class="sxs-lookup"><span data-stu-id="d4c9e-112">Causes</span></span>
* <span data-ttu-id="d4c9e-113">Hello Azure Mobile Engagement SDK'sı ile çözümlenen toobe gereken çoğu sorunlar uygulamanız (örneğin, bir kullanıcı Arabirimi veri toplama hatası, gönderme hatası, gelişmiş özellik hatası, API hatası, uygulama kilitlenmelerine veya görünen hizmet bir hata bulunan Kesinti).</span><span class="sxs-lookup"><span data-stu-id="d4c9e-113">Most issues that need toobe resolved with hello Azure Mobile Engagement SDK will be discovered by a failure in your application (such as a UI data collection failure, push failure, advanced feature failure, API failure, Application crashes, or apparent service outage).</span></span>  
* <span data-ttu-id="d4c9e-114">Azure Mobile Engagement, belirli bir özellik, hiçbir zaman uygulamanızda önce çalıştıysa toocomplete hello tümleştirme gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4c9e-114">If a particular feature of Azure Mobile Engagement has never worked in your app before, you will need toocomplete hello integration.</span></span> 
* <span data-ttu-id="d4c9e-115">Azure Mobile Engagement, belirli bir özellik çalıştığı ve durdurulmuş, tooupgrade toohello son sürümü hello Azure Mobile Engagement SDK'sı ile gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="d4c9e-115">If a particular feature of Azure Mobile Engagement was working and stopped, you may need tooupgrade toohello last version with hello Azure Mobile Engagement SDK.</span></span> <span data-ttu-id="d4c9e-116">Hello Azure Mobile Engagement SDK'sı (Android, iOS, Windows ve Windows Phone) Azure Mobile Engagement tarafından desteklenen her platform için farklı bir sürümü olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d4c9e-116">Remember that there is a different version of hello Azure Mobile Engagement SDK for each platform supported by Azure Mobile Engagement (Android, iOS, Windows, and Windows Phone).</span></span>

#### <a name="sdk-integration"></a><span data-ttu-id="d4c9e-117">SDK Tümleştirmesi</span><span class="sxs-lookup"><span data-stu-id="d4c9e-117">SDK Integration</span></span>
* <span data-ttu-id="d4c9e-118">Azure Mobile Engagement SDK'yı (Analytics) doğru biçimde tümleşik.</span><span class="sxs-lookup"><span data-stu-id="d4c9e-118">Azure Mobile Engagement not correctly integrated in SDK (Analytics).</span></span>
* <span data-ttu-id="d4c9e-119">SDK (uygulama içinde ve dışında uygulama iter) doğru biçimde tümleşik ulaşabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4c9e-119">Reach not correctly integrated in SDK (In App and Out of App Pushes).</span></span>
* <span data-ttu-id="d4c9e-120">Süresi dolmuş veya hatalı ürün vs sertifika. Geliştirme (yalnızca iOS).</span><span class="sxs-lookup"><span data-stu-id="d4c9e-120">Certificate expired or incorrect PROD vs. DEV (iOS only).</span></span>
* <span data-ttu-id="d4c9e-121">GCM veya ADM SDK'da tümleşik doğru biçimde (Android yalnızca - hizmet belirli iter).</span><span class="sxs-lookup"><span data-stu-id="d4c9e-121">GCM or ADM not correctly integrated in SDK (Android only - Service Specific Pushes).</span></span>
* <span data-ttu-id="d4c9e-122">Doğru biçimde izleme SDK (yükleme deposu izleme) tümleşiktir.</span><span class="sxs-lookup"><span data-stu-id="d4c9e-122">Tracking not correctly integrated in SDK (Install store tracking).</span></span>
* <span data-ttu-id="d4c9e-123">Yavaş veya GPS yerleşimine SDK (hedefleme coğrafi konuma göre) doğru biçimde tümleşik.</span><span class="sxs-lookup"><span data-stu-id="d4c9e-123">Lazy Location or GPS Location not correctly integrated in SDK (Targeting by geo-location).</span></span>

<span data-ttu-id="d4c9e-124">**Ayrıca bkz.:**</span><span class="sxs-lookup"><span data-stu-id="d4c9e-124">**See also:**</span></span>

* <span data-ttu-id="d4c9e-125">[SDK Belgeleri - tümleştirme kılavuzları][Link 5]</span><span class="sxs-lookup"><span data-stu-id="d4c9e-125">[SDK Documentation - Integration Guides][Link 5]</span></span> 
* <span data-ttu-id="d4c9e-126">[Sorun giderme kılavuzu - gönderme][Link 23]</span><span class="sxs-lookup"><span data-stu-id="d4c9e-126">[Troubleshooting Guide - Push][Link 23]</span></span>

#### <a name="sdk-upgrade"></a><span data-ttu-id="d4c9e-127">SDK yükseltme</span><span class="sxs-lookup"><span data-stu-id="d4c9e-127">SDK Upgrade</span></span>
* <span data-ttu-id="d4c9e-128">Tooupgrade SDK tooresolve sorunlarının hello SDK'sı (Merhaba aygıt işletim sistemi sürümleri genellikle ilgili toonewer) daha eski sürümleriyle gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4c9e-128">Need tooupgrade SDK tooresolve issues with older versions of hello SDK (often related toonewer versions of hello device OS).</span></span>
* <span data-ttu-id="d4c9e-129">Aygıtınızdan uygulamanızı önceki tüm sürümlerini kaldırın ve hello uygulamanızı en yeni sürümünü yükleyin, hello hello Azure Mobile Engagement UI tooconfirm Cihazınızı hello en yeni sürümü, uygulamanızın kullanıyor, cihaz kimliği yeniden kaydedin.</span><span class="sxs-lookup"><span data-stu-id="d4c9e-129">Uninstall all previous versions of your app from your device and reinstall hello newest version of your app, hello re-register your Device ID from hello Azure Mobile Engagement UI tooconfirm that your device is using hello newest version of your app.</span></span>

<span data-ttu-id="d4c9e-130">**Ayrıca bkz.:**</span><span class="sxs-lookup"><span data-stu-id="d4c9e-130">**See also:**</span></span>

* [<span data-ttu-id="d4c9e-131">SDK Belgeleri - sürüm notları</span><span class="sxs-lookup"><span data-stu-id="d4c9e-131">SDK Documentation - Release Notes</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554) 
* [<span data-ttu-id="d4c9e-132">SDK Belgeleri - yükseltme kılavuzları</span><span class="sxs-lookup"><span data-stu-id="d4c9e-132">SDK Documentation - Upgrade Guides</span></span>](http://go.microsoft.com/fwlink/?LinkId= 525554)

#### <a name="sdk-other"></a><span data-ttu-id="d4c9e-133">SDK diğer</span><span class="sxs-lookup"><span data-stu-id="d4c9e-133">SDK Other</span></span>
* <span data-ttu-id="d4c9e-134">Azure Mobile Engagement uygulama bildirimi "AndroidManifest.xml" hatalara neden olabilir toowork (yalnızca Android).</span><span class="sxs-lookup"><span data-stu-id="d4c9e-134">Errors in Application Manifest "AndroidManifest.xml" can cause Azure Mobile Engagement not toowork (Android only).</span></span>
* <span data-ttu-id="d4c9e-135">SDK tümleştirmesi ve API kullanımı ile yaygın bir sorun tooconfuse hello SDK anahtarı olan ve API anahtarını hello.</span><span class="sxs-lookup"><span data-stu-id="d4c9e-135">A common issue with SDK integration and API usage is tooconfuse hello SDK Key and hello API Key.</span></span>

<span data-ttu-id="d4c9e-136">**Ayrıca bkz.:**</span><span class="sxs-lookup"><span data-stu-id="d4c9e-136">**See also:**</span></span>

* <span data-ttu-id="d4c9e-137">[Kavramlar - sözlüğü][Link 6]</span><span class="sxs-lookup"><span data-stu-id="d4c9e-137">[Concepts - Glossary][Link 6]</span></span>

## <a name="advanced-coding-issues"></a><span data-ttu-id="d4c9e-138">Sorunları kodlama Gelişmiş</span><span class="sxs-lookup"><span data-stu-id="d4c9e-138">Advanced coding issues</span></span>
### <a name="issue"></a><span data-ttu-id="d4c9e-139">Sorun</span><span class="sxs-lookup"><span data-stu-id="d4c9e-139">Issue</span></span>
* <span data-ttu-id="d4c9e-140">Platform özel kod doğrudan Mobile Engagement, iOS, Android ve Windows Phone sorunlara neden olabilir tooAzure ilgili.</span><span class="sxs-lookup"><span data-stu-id="d4c9e-140">Platform specific code not directly related tooAzure Mobile Engagement can cause issues on iOS, Android, and Windows Phone.</span></span>

### <a name="causes"></a><span data-ttu-id="d4c9e-141">Neden olur.</span><span class="sxs-lookup"><span data-stu-id="d4c9e-141">Causes</span></span>
* <span data-ttu-id="d4c9e-142">Birçok Azure Mobile Engagement kodlama sorunları Gelişmiş nedeni yanlış yazılan platformu tarafından belirli bir kod tooAzure Mobile Engagement doğrudan ilgili.</span><span class="sxs-lookup"><span data-stu-id="d4c9e-142">Many advanced coding issues with Azure Mobile Engagement are caused by improperly written platform specific code not directly related tooAzure Mobile Engagement.</span></span> <span data-ttu-id="d4c9e-143">Tooconsult belgeleri belirli toohello platform için ayrıca tooAzure Mobile Engagement belgeleri (Android, iOS, Web, Windows ve Windows Phone) geliştirdiğinize gerekir.</span><span class="sxs-lookup"><span data-stu-id="d4c9e-143">You will need tooconsult documentation specific toohello platform you are developing for in addition tooAzure Mobile Engagement documentation (Android, iOS, Web, Windows, and Windows Phone).</span></span>
* <span data-ttu-id="d4c9e-144">Doğru biçimde "Kategoriler" yapılandırma, bir bildirim tooanother konumdan içinde veya dışında hello uygulaması (yalnızca Android) bağlama engeller.</span><span class="sxs-lookup"><span data-stu-id="d4c9e-144">Not correctly configuring "categories", prevents linking from a notification tooanother location either inside or outside of hello app (Android only).</span></span> 
* <span data-ttu-id="d4c9e-145">"UIKit.framework" çok "isteğe bağlı" "simgesi bulunamadı hatası" gösterir, iOS kodunuzda ayarı bulunamadı ve/veya eski iOS cihazlarda (yalnızca iOS) çöküyor.</span><span class="sxs-lookup"><span data-stu-id="d4c9e-145">Not setting "UIKit.framework" too"optional" in your iOS code, shows a "Symbol not found error" and/or crashes on older iOS devices (iOS only).</span></span>
* <span data-ttu-id="d4c9e-146">Süresi dolan sertifikaları veya doğru biçimde hello geliştirme veya üretim hello cert sürümünü kullanarak, nedenleri itme (yalnızca iOS) verir.</span><span class="sxs-lookup"><span data-stu-id="d4c9e-146">Expired certificates or not correctly using hello DEV or Prod version of hello cert, causes push issues (iOS only).</span></span>
* <span data-ttu-id="d4c9e-147">(Merhaba system center için uygulamanın oturumunu işleyişi Android ve iOS iter gibi), Azure Mobile Engagement denetleyemezsiniz bazı sınırlamalar devralınan tooa platformu vardır.</span><span class="sxs-lookup"><span data-stu-id="d4c9e-147">There are some limitations inherent tooa platform that Azure Mobile Engagement can't control (like how hello system center works for out of app pushes in Android and iOS).</span></span>
* <span data-ttu-id="d4c9e-148">Azure Mobile Engagement tam başvuru için iOS ve Android için Azure Mobile Engagement tarafından kullanılan hello iç paketlerin listesini yayımlar.</span><span class="sxs-lookup"><span data-stu-id="d4c9e-148">Azure Mobile Engagement publishes a full list of hello internal packages used by Azure Mobile Engagement for iOS and Android for reference.</span></span> <span data-ttu-id="d4c9e-149">Azure Mobile Engagement özelliklerinden bazıları belirli toohello platform (Android, iOS, Web, Windows ve Windows Phone) olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="d4c9e-149">Keep in mind that some features of Azure Mobile Engagement are specific toohello platform (Android, iOS, Web, Windows, and Windows Phone).</span></span>

### <a name="see-also"></a><span data-ttu-id="d4c9e-150">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="d4c9e-150">See also</span></span>
* <span data-ttu-id="d4c9e-151">[Sorun giderme kılavuzu - gönderme][Link 23]</span><span class="sxs-lookup"><span data-stu-id="d4c9e-151">[Troubleshooting Guide - Push][Link 23]</span></span> 
* <span data-ttu-id="d4c9e-152">[SDK Belgeleri - sürüm notları][Link 5]</span><span class="sxs-lookup"><span data-stu-id="d4c9e-152">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="d4c9e-153">[SDK Belgeleri - yükseltme kılavuzları][Link 5]</span><span class="sxs-lookup"><span data-stu-id="d4c9e-153">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="application-crashes"></a><span data-ttu-id="d4c9e-154">Uygulama çökme (Crash)</span><span class="sxs-lookup"><span data-stu-id="d4c9e-154">Application crashes</span></span>
### <a name="issue"></a><span data-ttu-id="d4c9e-155">Sorun</span><span class="sxs-lookup"><span data-stu-id="d4c9e-155">Issue</span></span>
* <span data-ttu-id="d4c9e-156">Uygulamanızı hello son kullanıcıların cihazda çöküyor.</span><span class="sxs-lookup"><span data-stu-id="d4c9e-156">Your application crashes on hello end users' device.</span></span>

### <a name="causes"></a><span data-ttu-id="d4c9e-157">Neden olur.</span><span class="sxs-lookup"><span data-stu-id="d4c9e-157">Causes</span></span>
* <span data-ttu-id="d4c9e-158">Kilitlenme bilgi hello görüntülenebilir *Analytics UI* veya hello *Analytics API*</span><span class="sxs-lookup"><span data-stu-id="d4c9e-158">Crash information can be viewed in hello *Analytics UI* or hello *Analytics API*</span></span>
* <span data-ttu-id="d4c9e-159">Cihaz kimliği test aygıtınızın hello ve hello ele bulabilir bir son kullanıcı toohelp için uygulama toocrash neden aynı eylemi, kilitlenme hello nedenini tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="d4c9e-159">You can find hello Device ID of your test device and take hello same action that caused your application toocrash for an end user toohelp identify hello cause of your crash.</span></span>
* <span data-ttu-id="d4c9e-160">Uygulamaları toocrash neden ile ilgili bilinen sorunlar hello Azure Mobile Engagement SDK'sı bazen toohello hello SDK en son sürümüne yükseltme tarafından çözümlenir.</span><span class="sxs-lookup"><span data-stu-id="d4c9e-160">Known issues with hello Azure Mobile Engagement SDK that cause applications toocrash are sometimes resolved by upgrading toohello latest version of hello SDK.</span></span> <span data-ttu-id="d4c9e-161">Platformunuz hakkında emin toocheck hello sürüm notları, kilitlenme araştırırken olun.</span><span class="sxs-lookup"><span data-stu-id="d4c9e-161">Make sure toocheck hello release notes about your platform when investigating crashes.</span></span>

### <a name="see-also"></a><span data-ttu-id="d4c9e-162">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="d4c9e-162">See also</span></span>
* <span data-ttu-id="d4c9e-163">[SDK Belgeleri - sürüm notları][Link 5]</span><span class="sxs-lookup"><span data-stu-id="d4c9e-163">[SDK Documentation - Release Notes][Link 5]</span></span>
* <span data-ttu-id="d4c9e-164">[SDK Belgeleri - yükseltme kılavuzları][Link 5]</span><span class="sxs-lookup"><span data-stu-id="d4c9e-164">[SDK Documentation - Upgrade Guides][Link 5]</span></span>

## <a name="app-store-upload-failures"></a><span data-ttu-id="d4c9e-165">Uygulama mağazası karşıya yükleme hataları</span><span class="sxs-lookup"><span data-stu-id="d4c9e-165">App store upload failures</span></span>
### <a name="issue"></a><span data-ttu-id="d4c9e-166">Sorun</span><span class="sxs-lookup"><span data-stu-id="d4c9e-166">Issue</span></span>
* <span data-ttu-id="d4c9e-167">Toouploading hello en son sürümünü uygulama tooApple, Google veya hello Windows uygulama mağazası ilgili hatalarla ilgili.</span><span class="sxs-lookup"><span data-stu-id="d4c9e-167">Errors related toouploading hello latest version of your app tooApple, Google, or hello Windows App store.</span></span>

### <a name="causes"></a><span data-ttu-id="d4c9e-168">Neden olur.</span><span class="sxs-lookup"><span data-stu-id="d4c9e-168">Causes</span></span>
* <span data-ttu-id="d4c9e-169">Uygulama mağazaları bazen belirli özellikleri etkin blok uygulamalar (örneğin hello Apple Store hello kullanımında IDFV hello Mağazası'ndaki uygulamaların ve hello GooglePlay deposu engeller uygulamalar arasında uygulama bilgilerinin hello paylaşımı).</span><span class="sxs-lookup"><span data-stu-id="d4c9e-169">App stores sometimes block apps with certain features enabled (e.g. hello Apple Store prevents hello use of IDFV in apps in hello store and hello GooglePlay store prevents hello sharing of application information between apps).</span></span> 
* <span data-ttu-id="d4c9e-170">Bir uygulama toohello deposu karşıya güçlük çekiyorsanız hello sürüm notları platform ve hello SDK geçerli sürümü hakkında denetlediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="d4c9e-170">Make sure that you check hello release notes about your platform and current version of hello SDK if you have difficulty uploading an app toohello store.</span></span>

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

