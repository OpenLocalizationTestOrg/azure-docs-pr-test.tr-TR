---
title: "Azure Mobile Engagement iOS SDK tümleştirmesi | Microsoft Docs"
description: "En son güncelleştirmeler ve iOS için Azure Mobile Engagement SDK'sı için yordamlar"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 947ea44b-00c1-450f-9a3b-74437954dc56
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: objective-c
ms.topic: article
ms.date: 07/17/2017
ms.author: piyushjo
ms.openlocfilehash: 01fdbb43c21ac6932e8462f4a6507fc63e50542d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-integrate-engagement-on-ios"></a><span data-ttu-id="fb87f-103">Katılım tümleştirmek için iOS hakkında</span><span class="sxs-lookup"><span data-stu-id="fb87f-103">How to Integrate Engagement on iOS</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="fb87f-104">Windows Evrensel</span><span class="sxs-lookup"><span data-stu-id="fb87f-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="fb87f-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="fb87f-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="fb87f-106">iOS</span><span class="sxs-lookup"><span data-stu-id="fb87f-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="fb87f-107">Android</span><span class="sxs-lookup"><span data-stu-id="fb87f-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
>
>

<span data-ttu-id="fb87f-108">Bu yordam, Engagement analizi ve izleme işlevlerine iOS uygulamanızda etkinleştirmek için en basit yolu açıklar.</span><span class="sxs-lookup"><span data-stu-id="fb87f-108">This procedure describes the simplest way to activate Engagement's Analytics and Monitoring functions in your iOS application.</span></span>

<span data-ttu-id="fb87f-109">Engagement SDK'sı iOS7 + ve Xcode 8 + gerektirir: uygulamanızı dağıtım hedefi en az olmalıdır iOS 7.</span><span class="sxs-lookup"><span data-stu-id="fb87f-109">The Engagement SDK requires iOS7+ and Xcode 8+: the deployment target of your application must be at least iOS 7.</span></span>

> [!NOTE]
> <span data-ttu-id="fb87f-110">XCode 7'de gerçekten bağımlı sonra kullanabilirsiniz [iOS Engagement SDK'sı v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="fb87f-110">If you really depend on XCode 7 then you may use the [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="fb87f-111">Bir bilinen hata varsa bu önceki sürüm Reach modülünü 10 iOS aygıtları bakın çalıştırılırken [reach modülü tümleştirme](mobile-engagement-ios-integrate-engagement-reach.md) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="fb87f-111">There is a known bug on the Reach module of this previous version while running on iOS 10 devices see [the reach module integration](mobile-engagement-ios-integrate-engagement-reach.md) for more details.</span></span> <span data-ttu-id="fb87f-112">SDK v3.2.4 kullanın sonra yalnızca atlamak seçerseniz `UserNotifications.framework` sonraki adımda içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="fb87f-112">If you choose to use the SDK v3.2.4 then just skip the `UserNotifications.framework` import in the next step.</span></span>
>
>

<span data-ttu-id="fb87f-113">Aşağıdaki adım kullanıcıları, oturumlar, etkinlikleri, kilitlenme ve Technicals ilgili tüm istatistikleri işlem için gereken günlükleri rapor etkinleştirmek için yeterli değildir.</span><span class="sxs-lookup"><span data-stu-id="fb87f-113">The following steps are enough to activate the report of logs needed to compute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="fb87f-114">Olaylar, hatalar ve işleri gibi diğer istatistikleri işlem için gereken günlükleri rapor katılım API kullanarak el ile yapılması gerekir (bkz [iOS uygulamanızı API etiketleme Gelişmiş Mobile Engagement kullanmayı](mobile-engagement-ios-use-engagement-api.md) Bu istatistikler olduğundan uygulamaya bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="fb87f-114">The report of logs needed to compute other statistics like Events, Errors and Jobs must be done manually using the Engagement API  (see [How to use the advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-the-engagement-sdk-into-your-ios-project"></a><span data-ttu-id="fb87f-115">Engagement SDK'sı iOS projenize ekleme</span><span class="sxs-lookup"><span data-stu-id="fb87f-115">Embed the Engagement SDK into your iOS project</span></span>
* <span data-ttu-id="fb87f-116">İOS SDK'sı yükle gelen [burada](http://aka.ms/qk2rnj).</span><span class="sxs-lookup"><span data-stu-id="fb87f-116">Download the iOS SDK from [here](http://aka.ms/qk2rnj).</span></span>
* <span data-ttu-id="fb87f-117">Engagement SDK'sı iOS projenize ekleyin: Xcode'da, sağ, proje seçin tıklayın ve **"Ekle dosyaları..."** ve `EngagementSDK` klasör.</span><span class="sxs-lookup"><span data-stu-id="fb87f-117">Add the Engagement SDK to your iOS project: in Xcode, right click on your project and select **"Add files to ..."** and choose the `EngagementSDK` folder.</span></span>
* <span data-ttu-id="fb87f-118">Katılım çalışmak için ek çerçeveleri gerektirir: Proje Gezgini'nde proje bölmesini açın ve doğru hedef seçin.</span><span class="sxs-lookup"><span data-stu-id="fb87f-118">Engagement requires additional frameworks to work: in the project explorer, open your project pane and select the correct target.</span></span> <span data-ttu-id="fb87f-119">Ardından, açın **"Derleme aşamaları"** sekmesi ve **"Bağlantı ikiliyi kitaplıklara"** menüsünde bu çerçeveleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="fb87f-119">Then, open the **"Build phases"** tab and in the **"Link Binary With Libraries"** menu, add these frameworks:</span></span>

  * <span data-ttu-id="fb87f-120">`UserNotifications.framework`-bağlantı olarak ayarla`Optional`</span><span class="sxs-lookup"><span data-stu-id="fb87f-120">`UserNotifications.framework` - set the link as `Optional`</span></span>
  * <span data-ttu-id="fb87f-121">`AdSupport.framework`-bağlantı olarak ayarla`Optional`</span><span class="sxs-lookup"><span data-stu-id="fb87f-121">`AdSupport.framework` - set the link as `Optional`</span></span>
  * `SystemConfiguration.framework`
  * `CoreTelephony.framework`
  * `CFNetwork.framework`
  * `CoreLocation.framework`
  * `libxml2.dylib`

> [!NOTE]
> <span data-ttu-id="fb87f-122">AdSupport framework kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="fb87f-122">The AdSupport framework can be removed.</span></span> <span data-ttu-id="fb87f-123">Katılım IDFA toplamak için bu framework gerekir.</span><span class="sxs-lookup"><span data-stu-id="fb87f-123">Engagement needs this framework to collect the IDFA.</span></span> <span data-ttu-id="fb87f-124">Ancak, IDFA toplamayı devre \<ios-sdk-engagement-ıdfa\> bu kimliğiyle ilgili yeni Apple ilkesiyle uyum sağlamak için</span><span class="sxs-lookup"><span data-stu-id="fb87f-124">However, IDFA collection can be disabled \<ios-sdk-engagement-idfa\> to comply with the new Apple policy regarding this ID.</span></span>
>
>

## <a name="initialize-the-engagement-sdk"></a><span data-ttu-id="fb87f-125">Engagement SDK'yı başlatma</span><span class="sxs-lookup"><span data-stu-id="fb87f-125">Initialize the Engagement SDK</span></span>
<span data-ttu-id="fb87f-126">Uygulama temsilcinizi değiştirme gerekir:</span><span class="sxs-lookup"><span data-stu-id="fb87f-126">You need to modify your Application Delegate:</span></span>

* <span data-ttu-id="fb87f-127">Uygulama dosyanızı üst kısmında, katılım Aracısı'nı içeri aktarın:</span><span class="sxs-lookup"><span data-stu-id="fb87f-127">At the top of your implementation file, import the Engagement agent:</span></span>

      [...]
      #import "EngagementAgent.h"
* <span data-ttu-id="fb87f-128">Katılım Initialize yöntemi içinde '**applicationDidFinishLaunching:**'veya'**uygulama: didFinishLaunchingWithOptions:**':</span><span class="sxs-lookup"><span data-stu-id="fb87f-128">Initialize Engagement inside the method '**applicationDidFinishLaunching:**' or '**application:didFinishLaunchingWithOptions:**':</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
      {
        [...]
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
        [...]
      }

## <a name="basic-reporting"></a><span data-ttu-id="fb87f-129">Temel raporlama</span><span class="sxs-lookup"><span data-stu-id="fb87f-129">Basic reporting</span></span>
### <a name="recommended-method-overload-your-uiviewcontroller-classes"></a><span data-ttu-id="fb87f-130">Önerilen yöntem: aşırı yükleme, `UIViewController` sınıfları</span><span class="sxs-lookup"><span data-stu-id="fb87f-130">Recommended method: overload your `UIViewController` classes</span></span>
<span data-ttu-id="fb87f-131">Rapor kullanıcıları, oturumlar, etkinlikleri, kilitlenme ve teknik istatistikleri işlem katılım tarafından gerekli tüm günlüklerin etkinleştirmek için yalnızca tüm yapabilirsiniz, `UIViewController` alt sınıfları `EngagementViewController` sınıfları (aynı kural için`UITableViewController`  -\> `EngagementTableViewController`).</span><span class="sxs-lookup"><span data-stu-id="fb87f-131">In order to activate the report of all the logs required by Engagement to compute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `UIViewController` sub-classes inherit from the `EngagementViewController` classes (same rule for `UITableViewController` -\> `EngagementTableViewController`).</span></span>

<span data-ttu-id="fb87f-132">**Katılım:**</span><span class="sxs-lookup"><span data-stu-id="fb87f-132">**Without Engagement :**</span></span>

    #import <UIKit/UIKit.h>

    @interface Tab1ViewController : UIViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

<span data-ttu-id="fb87f-133">**Katılım ile:**</span><span class="sxs-lookup"><span data-stu-id="fb87f-133">**With Engagement :**</span></span>

    #import <UIKit/UIKit.h>
    #import "EngagementViewController.h"

    @interface Tab1ViewController : EngagementViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="fb87f-134">Alternatif yöntem: çağrı `startActivity()` el ile</span><span class="sxs-lookup"><span data-stu-id="fb87f-134">Alternate method: call `startActivity()` manually</span></span>
<span data-ttu-id="fb87f-135">Olamaz ya da tekrar etmek istiyor musunuz, `UIViewController` sınıfları, bunun yerine, çağırarak etkinliklerinizi başlatabilirsiniz `EngagementAgent`'s doğrudan yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="fb87f-135">If you cannot or do not want to overload your `UIViewController` classes, you can instead start your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fb87f-136">SDK otomatik olarak çağıran iOS `endActivity()` uygulama kapatıldığında yöntemi.</span><span class="sxs-lookup"><span data-stu-id="fb87f-136">The iOS SDK automatically calls the `endActivity()` method when the application is closed.</span></span> <span data-ttu-id="fb87f-137">Bu nedenle, olan *yüksek oranda* çağırmak için önerilen `startActivity` kullanıcı etkinliği değiştirdiğinizde, yöntemi ve *hiçbir zaman* çağrısı `endActivity` bu yöntemi çağırmadan geçerli zorlar beri yöntemi tamamlandı olarak oturumu.</span><span class="sxs-lookup"><span data-stu-id="fb87f-137">Thus, it is *HIGHLY* recommended to call the `startActivity` method whenever the activity of the user change, and to *NEVER* call the `endActivity` method, since calling this method forces the current session to be ended.</span></span>
>
>

## <a name="location-reporting"></a><span data-ttu-id="fb87f-138">Konum raporlama</span><span class="sxs-lookup"><span data-stu-id="fb87f-138">Location reporting</span></span>
<span data-ttu-id="fb87f-139">Hizmet Koşulları Apple uygulamaları konum yalnızca istatistikleri amaçla izleme kullanmaya izin vermez.</span><span class="sxs-lookup"><span data-stu-id="fb87f-139">Apple terms of service do not allow applications to use location tracking for statistics purpose only.</span></span> <span data-ttu-id="fb87f-140">Bu nedenle, yalnızca uygulamanız konumu başka bir nedenle izleme de kullanıyorsanız konumu raporları etkinleştirmek için önerilir.</span><span class="sxs-lookup"><span data-stu-id="fb87f-140">Thus, it is recommended to enable location reports only if your application also use the location tracking for another reason.</span></span>

<span data-ttu-id="fb87f-141">İOS 8 ile başlayarak, anahtar için bir dize ayarlayarak uygulamanızı konum hizmetleri nasıl kullandığı için bir açıklama sağlamalısınız [NSLocationWhenInUseUsageDescription] veya [NSLocationAlwaysUsageDescription]uygulamanızın Info.plist dosyasında.</span><span class="sxs-lookup"><span data-stu-id="fb87f-141">Starting with iOS 8, you must provide a description for how your app uses location services by setting a string for the key [NSLocationWhenInUseUsageDescription] or [NSLocationAlwaysUsageDescription] in your app's Info.plist file.</span></span> <span data-ttu-id="fb87f-142">Rapor konumu engagement arka planda istiyorsanız NSLocationAlwaysUsageDescription anahtarı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fb87f-142">If you want to report location in the background with Engagement, add the key NSLocationAlwaysUsageDescription.</span></span> <span data-ttu-id="fb87f-143">Diğer durumlarda, NSLocationWhenInUseUsageDescription anahtarı ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fb87f-143">In all other cases, add the key NSLocationWhenInUseUsageDescription.</span></span> <span data-ttu-id="fb87f-144">Rapor arka plan konumu iOS 11 NSLocationAlwaysAndWhenInUseUsageDescription ve NSLocationWhenInUseUsageDescription gerekir unutmayın.</span><span class="sxs-lookup"><span data-stu-id="fb87f-144">Note that you need both NSLocationAlwaysAndWhenInUseUsageDescription and NSLocationWhenInUseUsageDescription to report background location on iOS 11.</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="fb87f-145">Yavaş alan konumu raporlama</span><span class="sxs-lookup"><span data-stu-id="fb87f-145">Lazy area location reporting</span></span>
<span data-ttu-id="fb87f-146">Yavaş alan konumu raporlama ülke, bölgeye ve yere göre cihazlara ilişkili rapor oluşturmaya olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="fb87f-146">Lazy area location reporting allows to report the country, region and locality associated to devices.</span></span> <span data-ttu-id="fb87f-147">Bu tür konumu raporlama yalnızca ağ konumlarını (hücre kimliği veya WIFI göre) kullanır.</span><span class="sxs-lookup"><span data-stu-id="fb87f-147">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="fb87f-148">Aygıt alanına oturum başına en fazla bir kez bildirilir.</span><span class="sxs-lookup"><span data-stu-id="fb87f-148">The device area is reported at most once per session.</span></span> <span data-ttu-id="fb87f-149">GPS hiçbir zaman kullanılmaz ve bu nedenle bu konumu rapor çok az (no değil söylemeniz) türü pil üzerindeki etkisi.</span><span class="sxs-lookup"><span data-stu-id="fb87f-149">The GPS is never used, and thus this type of location report has very few (not to say no) impact on the battery.</span></span>

<span data-ttu-id="fb87f-150">Bildirilen alanları kullanıcıları, oturumlar, olayları ve hataları ile ilgili coğrafi istatistikleri hesaplamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fb87f-150">Reported areas are used to compute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="fb87f-151">Reach kampanyaları ölçütü olarak de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fb87f-151">They can also be used as criterion in Reach campaigns.</span></span> <span data-ttu-id="fb87f-152">Bir aygıt teşekkürler alınabilir için son bilinen alanı bildirilen [aygıt API].</span><span class="sxs-lookup"><span data-stu-id="fb87f-152">The last known area reported for a device can be retrieved thanks to the [Device API].</span></span>

<span data-ttu-id="fb87f-153">Yavaş alan konumu raporlama etkinleştirmek için katılım Aracısı'nı başlatma sonra aşağıdaki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="fb87f-153">To enable lazy area location reporting, add the following line after initializing the Engagement agent:</span></span>

    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
      [...]
      [[EngagementAgent shared] setLazyAreaLocationReport:YES];
      [...]
    }

### <a name="real-time-location-reporting"></a><span data-ttu-id="fb87f-154">Gerçek zamanlı konum raporlama</span><span class="sxs-lookup"><span data-stu-id="fb87f-154">Real time location reporting</span></span>
<span data-ttu-id="fb87f-155">Gerçek zamanlı konum raporlama enlem ve boylam cihazlara ilişkili rapor oluşturmaya olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="fb87f-155">Real time location reporting allows to report the latitude and longitude associated to devices.</span></span> <span data-ttu-id="fb87f-156">Varsayılan olarak, bu tür konumu raporlama yalnızca ağ konumlarını (hücre kimliği veya WIFI göre) kullanır ve uygulama ön planda (yani oturumu sırasında) çalıştığında raporlama yalnızca etkindir.</span><span class="sxs-lookup"><span data-stu-id="fb87f-156">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and the reporting is only active when the application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="fb87f-157">Gerçek zamanlı konumlarının *değil* istatistikleri hesaplamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="fb87f-157">Real time locations are *NOT* used to compute statistics.</span></span> <span data-ttu-id="fb87f-158">Gerçek zamanlı coğrafi yalıtma kullanımına izin vermek için kendi tek amacı olan \<Reach-İzleyici-bölge sınırlaması\> Reach kampanyaları ölçütü.</span><span class="sxs-lookup"><span data-stu-id="fb87f-158">Their only purpose is to allow the use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="fb87f-159">Gerçek zamanlı konum raporlama etkinleştirmek için katılım Aracısı'nı başlatma sonra aşağıdaki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="fb87f-159">To enable real time location reporting, add the following line after initializing the Engagement agent:</span></span>

    [[EngagementAgent shared] setRealtimeLocationReport:YES];

#### <a name="gps-based-reporting"></a><span data-ttu-id="fb87f-160">Raporlama GPS dayalı</span><span class="sxs-lookup"><span data-stu-id="fb87f-160">GPS based reporting</span></span>
<span data-ttu-id="fb87f-161">Varsayılan olarak, gerçek zamanlı konum raporlama ağ tabanlı konum yalnızca kullanır.</span><span class="sxs-lookup"><span data-stu-id="fb87f-161">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="fb87f-162">(Olan daha kesin) tabanlı GPS konumları kullanımını etkinleştirmek için ekleyin:</span><span class="sxs-lookup"><span data-stu-id="fb87f-162">To enable the use of GPS based locations (which are far more precise), add:</span></span>

    [[EngagementAgent shared] setFineRealtimeLocationReport:YES];

#### <a name="background-reporting"></a><span data-ttu-id="fb87f-163">Arka plan raporlama</span><span class="sxs-lookup"><span data-stu-id="fb87f-163">Background reporting</span></span>
<span data-ttu-id="fb87f-164">Uygulama ön planda (yani oturumu sırasında) çalıştırdığında, varsayılan olarak, gerçek zamanlı konum raporlama yalnızca etkindir.</span><span class="sxs-lookup"><span data-stu-id="fb87f-164">By default, real time location reporting is only active when the application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="fb87f-165">Aynı zamanda arka planda raporlamayı etkinleştirmek için ekleyin:</span><span class="sxs-lookup"><span data-stu-id="fb87f-165">To enable the reporting also in background, add:</span></span>

    [[EngagementAgent shared] setBackgroundRealtimeLocationReport:YES withLaunchOptions:launchOptions];

> [!NOTE]
> <span data-ttu-id="fb87f-166">Tabanlı ağ konumları yalnızca uygulama arka planda çalıştığında raporlanır, GPS etkin olsa bile.</span><span class="sxs-lookup"><span data-stu-id="fb87f-166">When the application runs in background, only network based locations are reported, even if you enabled the GPS.</span></span>
>
>

<span data-ttu-id="fb87f-167">Bu işlev uygulaması çağıracaktır [startMonitoringSignificantLocationChanges] uygulamanızın arka planda gittiğinde.</span><span class="sxs-lookup"><span data-stu-id="fb87f-167">Implementation of this function will call [startMonitoringSignificantLocationChanges] when your application goes into the background.</span></span> <span data-ttu-id="fb87f-168">Otomatik olarak yeni bir konum olay gelirse arka uygulamanıza yeniden başlatmak olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="fb87f-168">Be aware that it will automatically relaunch your application into the background if a new location event arrives.</span></span>

## <a name="advanced-reporting"></a><span data-ttu-id="fb87f-169">Gelişmiş raporlama</span><span class="sxs-lookup"><span data-stu-id="fb87f-169">Advanced reporting</span></span>
<span data-ttu-id="fb87f-170">Uygulama belirli olaylar, hatalar ve işleri rapor istiyorsanız, isteğe bağlı olarak, katılım API yöntemlerini kullanmanız gerekebilir `EngagementAgent` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="fb87f-170">Optionally, if you want to report application specific events, errors and jobs, you need to use the Engagement API through the methods of the `EngagementAgent` class.</span></span> <span data-ttu-id="fb87f-171">Bu sınıfın bir nesnesi çağırarak alınabilir `[EngagementAgent shared]` statik yöntemi.</span><span class="sxs-lookup"><span data-stu-id="fb87f-171">An object of this class can be retrieved by calling the `[EngagementAgent shared]` static method.</span></span>

<span data-ttu-id="fb87f-172">Katılım API tüm Engagement'ın gelişmiş özelliklerinden kullanacak şekilde sağlar ve nasıl ayrıntılı İos'ta katılım API kullanmak için (teknik belgeleri olarak yanı `EngagementAgent` sınıfı).</span><span class="sxs-lookup"><span data-stu-id="fb87f-172">The Engagement API allows to use all of Engagement's advanced capabilities and is detailed in the How to Use the Engagement API on iOS (as well as in the technical documentation of the `EngagementAgent` class).</span></span>

## <a name="disable-idfa-collection"></a><span data-ttu-id="fb87f-173">IDFA toplamayı devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="fb87f-173">Disable IDFA collection</span></span>
<span data-ttu-id="fb87f-174">Varsayılan olarak, katılım kullanacağı [IDFA] bir kullanıcıyı benzersiz şekilde tanımlamak için.</span><span class="sxs-lookup"><span data-stu-id="fb87f-174">By default, Engagement will use the [IDFA] to uniquely identify a user.</span></span> <span data-ttu-id="fb87f-175">Ancak başka bir uygulamada reklam kullanmıyorsanız, App Store gözden geçirme işlemi tarafından reddedilmiş.</span><span class="sxs-lookup"><span data-stu-id="fb87f-175">But if you’re not using advertising elsewhere in the app, you might be rejected by the App Store review process.</span></span> <span data-ttu-id="fb87f-176">IDFA toplamayı önişlemci makrosu ekleyerek devre dışı bırakılacak `ENGAGEMENT_DISABLE_IDFA` pch dosyanızdaki (veya `Build Settings` uygulamanızın).</span><span class="sxs-lookup"><span data-stu-id="fb87f-176">IDFA collection can be disabled by adding the preprocessor macro `ENGAGEMENT_DISABLE_IDFA` in your pch file (or in the `Build Settings` of your application).</span></span> <span data-ttu-id="fb87f-177">Bu başvuru olduğundan emin `ASIdentifierManager`, `advertisingIdentifier` veya `isAdvertisingTrackingEnabled` uygulama oluşturma.</span><span class="sxs-lookup"><span data-stu-id="fb87f-177">This will ensure that there is no references to `ASIdentifierManager`, `advertisingIdentifier` or `isAdvertisingTrackingEnabled` in the application build.</span></span>

<span data-ttu-id="fb87f-178">Tümleştirme sırasında **prefix.pch** dosyası:</span><span class="sxs-lookup"><span data-stu-id="fb87f-178">Integration in the **prefix.pch** file:</span></span>

    #define ENGAGEMENT_DISABLE_IDFA
    ...

<span data-ttu-id="fb87f-179">IDFA toplamayı düzgün uygulamanızda katılım test günlüklerinin denetleyerek devre dışı olduğunu doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fb87f-179">You can verify that the IDFA collection is properly disabled in your application by checking the Engagement test logs.</span></span> <span data-ttu-id="fb87f-180">Bkz: tümleştirme sınama\<ios-sdk-engagement-test-ıdfa\> daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="fb87f-180">See the Integration Test\<ios-sdk-engagement-test-idfa\> documentation for further information.</span></span>

## <a name="disable-log-reporting"></a><span data-ttu-id="fb87f-181">Günlük bildirimini devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="fb87f-181">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="fb87f-182">Yöntem çağrısı kullanma</span><span class="sxs-lookup"><span data-stu-id="fb87f-182">Using a method call</span></span>
<span data-ttu-id="fb87f-183">Engagement'ın günlükleri göndermek durdurmak istiyorsanız, çağırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fb87f-183">If you want Engagement to stop sending logs, you can call:</span></span>

    [[EngagementAgent shared] setEnabled:NO];

<span data-ttu-id="fb87f-184">Bu çağrı kalıcıdır: kullandığı `NSUserDefaults` bilgileri depolamak için.</span><span class="sxs-lookup"><span data-stu-id="fb87f-184">This call is persistent: it uses `NSUserDefaults` to store the information.</span></span>

<span data-ttu-id="fb87f-185">Yeniden ile aynı işlevini çağırarak raporlama günlüğü etkinleştirebilirsiniz `YES`.</span><span class="sxs-lookup"><span data-stu-id="fb87f-185">You can enable log reporting again by calling the same function with `YES`.</span></span>

### <a name="integration-in-your-settings-bundle"></a><span data-ttu-id="fb87f-186">Ayarlar paketi tümleştirme</span><span class="sxs-lookup"><span data-stu-id="fb87f-186">Integration in your settings bundle</span></span>
<span data-ttu-id="fb87f-187">Bu işlevi çağırmak yerine, ayrıca bu ayarı doğrudan var olan tümleştirebilirsiniz `Settings.bundle` dosya.</span><span class="sxs-lookup"><span data-stu-id="fb87f-187">Instead of calling this function, you can also integrate this setting directly in your existing `Settings.bundle` file.</span></span> <span data-ttu-id="fb87f-188">Dize `engagement_agent_enabled` olarak kullanılması gereken bir tercih tanımlayıcısı ve bir geçiş anahtara ilişkilendirilmiş olması gerekir (`PSToggleSwitchSpecifier`).</span><span class="sxs-lookup"><span data-stu-id="fb87f-188">The string `engagement_agent_enabled` must be used as a the preference identifier and it must be associated to a toggle switch(`PSToggleSwitchSpecifier`).</span></span>

<span data-ttu-id="fb87f-189">Aşağıdaki örnekte `Settings.bundle` uyguladıktan gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="fb87f-189">The following example of `Settings.bundle` shows how to implement it:</span></span>

    <dict>
        <key>PreferenceSpecifiers</key>
        <array>
            <dict>
                <key>DefaultValue</key>
                <true/>
                <key>Key</key>
                <string>engagement_agent_enabled</string>
                <key>Title</key>
                <string>Log reporting enabled</string>
                <key>Type</key>
                <string>PSToggleSwitchSpecifier</string>
            </dict>
        </array>
        <key>StringsTable</key>
        <string>Root</string>
    </dict>

<!-- URLs. -->
<span data-ttu-id="fb87f-190">[aygıt API]: http://go.microsoft.com/?linkid=9876094</span><span class="sxs-lookup"><span data-stu-id="fb87f-190">[Device API]: http://go.microsoft.com/?linkid=9876094</span></span>
<span data-ttu-id="fb87f-191">[NSLocationWhenInUseUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW26</span><span class="sxs-lookup"><span data-stu-id="fb87f-191">[NSLocationWhenInUseUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW26</span></span>
<span data-ttu-id="fb87f-192">[NSLocationAlwaysUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW18</span><span class="sxs-lookup"><span data-stu-id="fb87f-192">[NSLocationAlwaysUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW18</span></span>
<span data-ttu-id="fb87f-193">[startMonitoringSignificantLocationChanges]:http://developer.apple.com/library/IOs/#documentation/CoreLocation/Reference/CLLocationManager_Class/CLLocationManager/CLLocationManager.html#//apple_ref/occ/instm/CLLocationManager/startMonitoringSignificantLocationChanges</span><span class="sxs-lookup"><span data-stu-id="fb87f-193">[startMonitoringSignificantLocationChanges]:http://developer.apple.com/library/IOs/#documentation/CoreLocation/Reference/CLLocationManager_Class/CLLocationManager/CLLocationManager.html#//apple_ref/occ/instm/CLLocationManager/startMonitoringSignificantLocationChanges</span></span>
<span data-ttu-id="fb87f-194">[IDFA]:https://developer.apple.com/library/ios/documentation/AdSupport/Reference/ASIdentifierManager_Ref/ASIdentifierManager.html#//apple_ref/occ/instp/ASIdentifierManager/advertisingIdentifier</span><span class="sxs-lookup"><span data-stu-id="fb87f-194">[IDFA]:https://developer.apple.com/library/ios/documentation/AdSupport/Reference/ASIdentifierManager_Ref/ASIdentifierManager.html#//apple_ref/occ/instp/ASIdentifierManager/advertisingIdentifier</span></span>
