---
title: "aaaAzure Mobile Engagement iOS SDK tümleştirmesi | Microsoft Docs"
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
ms.openlocfilehash: 66ce34efabede7d882caa8a91431a8df71e4fb59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toointegrate-engagement-on-ios"></a><span data-ttu-id="6bd6a-103">Nasıl tooIntegrate Engagement iOS</span><span class="sxs-lookup"><span data-stu-id="6bd6a-103">How tooIntegrate Engagement on iOS</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6bd6a-104">Windows Evrensel</span><span class="sxs-lookup"><span data-stu-id="6bd6a-104">Windows Universal</span></span>](mobile-engagement-windows-store-integrate-engagement.md)
> * [<span data-ttu-id="6bd6a-105">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="6bd6a-105">Windows Phone Silverlight</span></span>](mobile-engagement-windows-phone-integrate-engagement.md)
> * [<span data-ttu-id="6bd6a-106">iOS</span><span class="sxs-lookup"><span data-stu-id="6bd6a-106">iOS</span></span>](mobile-engagement-ios-integrate-engagement.md)
> * [<span data-ttu-id="6bd6a-107">Android</span><span class="sxs-lookup"><span data-stu-id="6bd6a-107">Android</span></span>](mobile-engagement-android-integrate-engagement.md)
>
>

<span data-ttu-id="6bd6a-108">Bu yordam, hello en basit yolu tooactivate Engagement analizi ve izleme işlevlerine iOS uygulamanızda açıklar.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-108">This procedure describes hello simplest way tooactivate Engagement's Analytics and Monitoring functions in your iOS application.</span></span>

<span data-ttu-id="6bd6a-109">Merhaba Engagement SDK'sı iOS7 + ve Xcode 8 + gerektirir: hello dağıtım hedef uygulamanızın en az olmalıdır iOS 7.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-109">hello Engagement SDK requires iOS7+ and Xcode 8+: hello deployment target of your application must be at least iOS 7.</span></span>

> [!NOTE]
> <span data-ttu-id="6bd6a-110">XCode 7'de gerçekten bağımlı sonra hello kullanabilir [iOS Engagement SDK'sı v3.2.4](https://aka.ms/r6oouh).</span><span class="sxs-lookup"><span data-stu-id="6bd6a-110">If you really depend on XCode 7 then you may use hello [iOS Engagement SDK v3.2.4](https://aka.ms/r6oouh).</span></span> <span data-ttu-id="6bd6a-111">Bir bilinen hata varsa bu önceki sürümünü Reach modülünü hello 10 iOS aygıtları bakın çalıştırılırken [hello reach modülü tümleştirme](mobile-engagement-ios-integrate-engagement-reach.md) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-111">There is a known bug on hello Reach module of this previous version while running on iOS 10 devices see [hello reach module integration](mobile-engagement-ios-integrate-engagement-reach.md) for more details.</span></span> <span data-ttu-id="6bd6a-112">Toouse hello SDK v3.2.4 belirtin, sonra yalnızca hello Atla varsa `UserNotifications.framework` hello sonraki adımda içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-112">If you choose toouse hello SDK v3.2.4 then just skip hello `UserNotifications.framework` import in hello next step.</span></span>
>
>

<span data-ttu-id="6bd6a-113">Aşağıdaki adımları hello günlüklerinin yeterli tooactivate hello rapor kullanıcıları, oturumlar, etkinlikleri, kilitlenme ve Technicals ilgili tüm istatistikleri toocompute gerekli ' dir.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-113">hello following steps are enough tooactivate hello report of logs needed toocompute all statistics regarding Users, Sessions, Activities, Crashes and Technicals.</span></span> <span data-ttu-id="6bd6a-114">Günlükler Hello rapor olaylar, hatalar ve işleri hello katılım API kullanarak el ile yapılmalıdır gibi bu toocompute diğer istatistiklerin gerekli (bkz [nasıl toouse hello Mobile Engagement iOS uygulamanızı API etiketleme Gelişmiş](mobile-engagement-ios-use-engagement-api.md) Bu istatistikler itibaren Uygulama bağımlıdır.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-114">hello report of logs needed toocompute other statistics like Events, Errors and Jobs must be done manually using hello Engagement API  (see [How toouse hello advanced Mobile Engagement tagging API in your iOS app](mobile-engagement-ios-use-engagement-api.md) since these statistics are application dependent.</span></span>

## <a name="embed-hello-engagement-sdk-into-your-ios-project"></a><span data-ttu-id="6bd6a-115">Merhaba Engagement SDK'sı iOS projenize ekleme</span><span class="sxs-lookup"><span data-stu-id="6bd6a-115">Embed hello Engagement SDK into your iOS project</span></span>
* <span data-ttu-id="6bd6a-116">Merhaba iOS SDK'sı yükle gelen [burada](http://aka.ms/qk2rnj).</span><span class="sxs-lookup"><span data-stu-id="6bd6a-116">Download hello iOS SDK from [here](http://aka.ms/qk2rnj).</span></span>
* <span data-ttu-id="6bd6a-117">Ekle hello Engagement SDK'sı tooyour iOS projesi: Xcode'da, sağ, proje seçin tıklayın ve **"çok dosyaları Ekle..."** ve hello seçin `EngagementSDK` klasör.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-117">Add hello Engagement SDK tooyour iOS project: in Xcode, right click on your project and select **"Add files too..."** and choose hello `EngagementSDK` folder.</span></span>
* <span data-ttu-id="6bd6a-118">Katılım ek çerçeveler toowork gerektirir: hello proje Gezgini'nde, proje bölmesini açın ve doğru hedef hello seçin.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-118">Engagement requires additional frameworks toowork: in hello project explorer, open your project pane and select hello correct target.</span></span> <span data-ttu-id="6bd6a-119">Merhaba açın **"Derleme aşamaları"** sekmesi ve hello **"Bağlantı ikiliyi kitaplıklara"** menüsünde bu çerçeveleri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6bd6a-119">Then, open hello **"Build phases"** tab and in hello **"Link Binary With Libraries"** menu, add these frameworks:</span></span>

  * <span data-ttu-id="6bd6a-120">`UserNotifications.framework`-kümesi hello bağlantı olarak`Optional`</span><span class="sxs-lookup"><span data-stu-id="6bd6a-120">`UserNotifications.framework` - set hello link as `Optional`</span></span>
  * <span data-ttu-id="6bd6a-121">`AdSupport.framework`-kümesi hello bağlantı olarak`Optional`</span><span class="sxs-lookup"><span data-stu-id="6bd6a-121">`AdSupport.framework` - set hello link as `Optional`</span></span>
  * `SystemConfiguration.framework`
  * `CoreTelephony.framework`
  * `CFNetwork.framework`
  * `CoreLocation.framework`
  * `libxml2.dylib`

> [!NOTE]
> <span data-ttu-id="6bd6a-122">Merhaba AdSupport framework kaldırılabilir.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-122">hello AdSupport framework can be removed.</span></span> <span data-ttu-id="6bd6a-123">Katılım bu framework toocollect hello IDFA gerekir.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-123">Engagement needs this framework toocollect hello IDFA.</span></span> <span data-ttu-id="6bd6a-124">Ancak, IDFA toplamayı devre \<ios-sdk-engagement-ıdfa\> toocomply bu kimliğiyle ilgili yeni Apple politikasını hello ile</span><span class="sxs-lookup"><span data-stu-id="6bd6a-124">However, IDFA collection can be disabled \<ios-sdk-engagement-idfa\> toocomply with hello new Apple policy regarding this ID.</span></span>
>
>

## <a name="initialize-hello-engagement-sdk"></a><span data-ttu-id="6bd6a-125">Merhaba Engagement SDK'yı başlatma</span><span class="sxs-lookup"><span data-stu-id="6bd6a-125">Initialize hello Engagement SDK</span></span>
<span data-ttu-id="6bd6a-126">Uygulama temsilcinizi toomodify gerekir:</span><span class="sxs-lookup"><span data-stu-id="6bd6a-126">You need toomodify your Application Delegate:</span></span>

* <span data-ttu-id="6bd6a-127">Uygulama dosyanızı Hello üstünde hello katılım Aracısı içeri aktarın:</span><span class="sxs-lookup"><span data-stu-id="6bd6a-127">At hello top of your implementation file, import hello Engagement agent:</span></span>

      [...]
      #import "EngagementAgent.h"
* <span data-ttu-id="6bd6a-128">Katılım Initialize hello yöntemi içinde '**applicationDidFinishLaunching:**'veya'**uygulama: didFinishLaunchingWithOptions:**':</span><span class="sxs-lookup"><span data-stu-id="6bd6a-128">Initialize Engagement inside hello method '**applicationDidFinishLaunching:**' or '**application:didFinishLaunchingWithOptions:**':</span></span>

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
      {
        [...]
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
        [...]
      }

## <a name="basic-reporting"></a><span data-ttu-id="6bd6a-129">Temel raporlama</span><span class="sxs-lookup"><span data-stu-id="6bd6a-129">Basic reporting</span></span>
### <a name="recommended-method-overload-your-uiviewcontroller-classes"></a><span data-ttu-id="6bd6a-130">Önerilen yöntem: aşırı yükleme, `UIViewController` sınıfları</span><span class="sxs-lookup"><span data-stu-id="6bd6a-130">Recommended method: overload your `UIViewController` classes</span></span>
<span data-ttu-id="6bd6a-131">Sipariş tooactivate hello raporunda katılım toocompute kullanıcıları, oturumlar, etkinlikleri, kilitlenme ve teknik istatistikleri gerekli tüm hello günlükler, yalnızca tüm yapabileceğiniz, `UIViewController` alt sınıfları devral hello `EngagementViewController` sınıfları (aynı kural için `UITableViewController`  - \> `EngagementTableViewController`).</span><span class="sxs-lookup"><span data-stu-id="6bd6a-131">In order tooactivate hello report of all hello logs required by Engagement toocompute Users, Sessions, Activities, Crashes and Technical statistics, you can simply make all your `UIViewController` sub-classes inherit from hello `EngagementViewController` classes (same rule for `UITableViewController` -\> `EngagementTableViewController`).</span></span>

<span data-ttu-id="6bd6a-132">**Katılım:**</span><span class="sxs-lookup"><span data-stu-id="6bd6a-132">**Without Engagement :**</span></span>

    #import <UIKit/UIKit.h>

    @interface Tab1ViewController : UIViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

<span data-ttu-id="6bd6a-133">**Katılım ile:**</span><span class="sxs-lookup"><span data-stu-id="6bd6a-133">**With Engagement :**</span></span>

    #import <UIKit/UIKit.h>
    #import "EngagementViewController.h"

    @interface Tab1ViewController : EngagementViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

### <a name="alternate-method-call-startactivity-manually"></a><span data-ttu-id="6bd6a-134">Alternatif yöntem: çağrı `startActivity()` el ile</span><span class="sxs-lookup"><span data-stu-id="6bd6a-134">Alternate method: call `startActivity()` manually</span></span>
<span data-ttu-id="6bd6a-135">Olamaz ya da toooverload istiyor musunuz, `UIViewController` sınıfları, bunun yerine, çağırarak etkinliklerinizi başlatabilirsiniz `EngagementAgent`'s doğrudan yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-135">If you cannot or do not want toooverload your `UIViewController` classes, you can instead start your activities by calling `EngagementAgent`'s methods directly.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6bd6a-136">Merhaba iOS SDK'sı otomatik olarak çağırır hello `endActivity()` hello uygulama kapatıldığında yöntemi.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-136">hello iOS SDK automatically calls hello `endActivity()` method when hello application is closed.</span></span> <span data-ttu-id="6bd6a-137">Bu nedenle, olan *yüksek oranda* toocall hello önerilen `startActivity` hello kullanıcının hello etkinliği değiştirdiğinizde, yöntemi ve çok*hiçbir zaman* çağrısı hello `endActivity` bu yöntem zorlar arama itibaren yöntemi Merhaba geçerli oturum toobe sona erdi.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-137">Thus, it is *HIGHLY* recommended toocall hello `startActivity` method whenever hello activity of hello user change, and too*NEVER* call hello `endActivity` method, since calling this method forces hello current session toobe ended.</span></span>
>
>

## <a name="location-reporting"></a><span data-ttu-id="6bd6a-138">Konum raporlama</span><span class="sxs-lookup"><span data-stu-id="6bd6a-138">Location reporting</span></span>
<span data-ttu-id="6bd6a-139">Hizmet Koşulları Apple uygulamaları toouse konum yalnızca istatistikleri amaçla izleme izin vermez.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-139">Apple terms of service do not allow applications toouse location tracking for statistics purpose only.</span></span> <span data-ttu-id="6bd6a-140">Bu nedenle, yalnızca uygulamanız hello konumu başka bir nedenle izleme de kullanıyorsanız tooenable konumu raporları önerilir.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-140">Thus, it is recommended tooenable location reports only if your application also use hello location tracking for another reason.</span></span>

<span data-ttu-id="6bd6a-141">İOS 8 ile başlayarak, uygulamanızı hello anahtarı için bir dize ayarlayarak konum hizmetleri nasıl kullandığı için bir açıklama sağlamalısınız [NSLocationWhenInUseUsageDescription] veya [NSLocationAlwaysUsageDescription]uygulamanızın Info.plist dosyasında.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-141">Starting with iOS 8, you must provide a description for how your app uses location services by setting a string for hello key [NSLocationWhenInUseUsageDescription] or [NSLocationAlwaysUsageDescription] in your app's Info.plist file.</span></span> <span data-ttu-id="6bd6a-142">Engagement hello arka planda tooreport konumu istiyorsanız hello anahtar NSLocationAlwaysUsageDescription ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-142">If you want tooreport location in hello background with Engagement, add hello key NSLocationAlwaysUsageDescription.</span></span> <span data-ttu-id="6bd6a-143">Diğer durumlarda, başlangıç anahtarı NSLocationWhenInUseUsageDescription ekleyin.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-143">In all other cases, add hello key NSLocationWhenInUseUsageDescription.</span></span> <span data-ttu-id="6bd6a-144">İOS 11 NSLocationAlwaysAndWhenInUseUsageDescription ve NSLocationWhenInUseUsageDescription tooreport arka plan konumu gerektiğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-144">Note that you need both NSLocationAlwaysAndWhenInUseUsageDescription and NSLocationWhenInUseUsageDescription tooreport background location on iOS 11.</span></span>

### <a name="lazy-area-location-reporting"></a><span data-ttu-id="6bd6a-145">Yavaş alan konumu raporlama</span><span class="sxs-lookup"><span data-stu-id="6bd6a-145">Lazy area location reporting</span></span>
<span data-ttu-id="6bd6a-146">Yavaş alan konumu raporlama sağlar tooreport hello ülke, bölgeye ve yere göre ilişkili toodevices.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-146">Lazy area location reporting allows tooreport hello country, region and locality associated toodevices.</span></span> <span data-ttu-id="6bd6a-147">Bu tür konumu raporlama yalnızca ağ konumlarını (hücre kimliği veya WIFI göre) kullanır.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-147">This type of location reporting only uses network locations (based on Cell ID or WIFI).</span></span> <span data-ttu-id="6bd6a-148">Merhaba aygıt alanına oturum başına en fazla bir kez bildirilir.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-148">hello device area is reported at most once per session.</span></span> <span data-ttu-id="6bd6a-149">Merhaba GPS hiçbir zaman kullanılmaz ve bu nedenle bu konumu rapor çok az türü (değil toosay yok) hello pil üzerindeki etkisi.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-149">hello GPS is never used, and thus this type of location report has very few (not toosay no) impact on hello battery.</span></span>

<span data-ttu-id="6bd6a-150">Kullanıcılar, oturumlar, olayları ve hataları ile ilgili kullanılan toocompute coğrafi istatistikleri bildirilen alanlarıdır.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-150">Reported areas are used toocompute geographic statistics about users, sessions, events and errors.</span></span> <span data-ttu-id="6bd6a-151">Reach kampanyaları ölçütü olarak de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-151">They can also be used as criterion in Reach campaigns.</span></span> <span data-ttu-id="6bd6a-152">bir aygıtı alınırsa teşekkürler toohello olabilir raporlanan alanı bilinen son hello [aygıt API].</span><span class="sxs-lookup"><span data-stu-id="6bd6a-152">hello last known area reported for a device can be retrieved thanks toohello [Device API].</span></span>

<span data-ttu-id="6bd6a-153">tooenable yavaş alan konumu raporlama satır hello katılım Aracısı başlatma sonra aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6bd6a-153">tooenable lazy area location reporting, add hello following line after initializing hello Engagement agent:</span></span>

    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
      [...]
      [[EngagementAgent shared] setLazyAreaLocationReport:YES];
      [...]
    }

### <a name="real-time-location-reporting"></a><span data-ttu-id="6bd6a-154">Gerçek zamanlı konum raporlama</span><span class="sxs-lookup"><span data-stu-id="6bd6a-154">Real time location reporting</span></span>
<span data-ttu-id="6bd6a-155">Gerçek zamanlı konum raporlama sağlar tooreport hello enlem ve boylam ilişkili toodevices.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-155">Real time location reporting allows tooreport hello latitude and longitude associated toodevices.</span></span> <span data-ttu-id="6bd6a-156">Varsayılan olarak, bu tür konumu raporlama yalnızca ağ konumlarını (hücre kimliği veya WIFI göre) kullanır ve hello uygulama ön planda (yani oturumu sırasında) çalıştığında hello raporlama yalnızca etkindir.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-156">By default, this type of location reporting only uses network locations (based on Cell ID or WIFI), and hello reporting is only active when hello application runs in foreground (i.e. during a session).</span></span>

<span data-ttu-id="6bd6a-157">Gerçek zamanlı konumlarının *değil* toocompute istatistikleri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-157">Real time locations are *NOT* used toocompute statistics.</span></span> <span data-ttu-id="6bd6a-158">Yalnızca amaçlarına tooallow hello gerçek zamanlı coğrafi yalıtma kullanımıdır \<Reach-İzleyici-bölge sınırlaması\> Reach kampanyaları ölçütü.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-158">Their only purpose is tooallow hello use of real time geo-fencing \<Reach-Audience-geofencing\> criterion in Reach campaigns.</span></span>

<span data-ttu-id="6bd6a-159">tooenable gerçek zamanlı konum raporlama satır hello katılım Aracısı başlatma sonra aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6bd6a-159">tooenable real time location reporting, add hello following line after initializing hello Engagement agent:</span></span>

    [[EngagementAgent shared] setRealtimeLocationReport:YES];

#### <a name="gps-based-reporting"></a><span data-ttu-id="6bd6a-160">Raporlama GPS dayalı</span><span class="sxs-lookup"><span data-stu-id="6bd6a-160">GPS based reporting</span></span>
<span data-ttu-id="6bd6a-161">Varsayılan olarak, gerçek zamanlı konum raporlama ağ tabanlı konum yalnızca kullanır.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-161">By default, real time location reporting only uses network based locations.</span></span> <span data-ttu-id="6bd6a-162">GPS tooenable hello kullanımı (olan daha kesin) konumları tabanlı, ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6bd6a-162">tooenable hello use of GPS based locations (which are far more precise), add:</span></span>

    [[EngagementAgent shared] setFineRealtimeLocationReport:YES];

#### <a name="background-reporting"></a><span data-ttu-id="6bd6a-163">Arka plan raporlama</span><span class="sxs-lookup"><span data-stu-id="6bd6a-163">Background reporting</span></span>
<span data-ttu-id="6bd6a-164">Merhaba uygulama ön planda (yani oturumu sırasında) çalıştırdığında, varsayılan olarak, gerçek zamanlı konum raporlama yalnızca etkindir.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-164">By default, real time location reporting is only active when hello application runs in foreground (i.e. during a session).</span></span> <span data-ttu-id="6bd6a-165">aynı zamanda arka planda raporlama tooenable hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="6bd6a-165">tooenable hello reporting also in background, add:</span></span>

    [[EngagementAgent shared] setBackgroundRealtimeLocationReport:YES withLaunchOptions:launchOptions];

> [!NOTE]
> <span data-ttu-id="6bd6a-166">Merhaba uygulaması arka planda çalıştığında, ağ tabanlı konumlar sadece bildirilir, etkinleştirilmiş olsa bile GPS hello.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-166">When hello application runs in background, only network based locations are reported, even if you enabled hello GPS.</span></span>
>
>

<span data-ttu-id="6bd6a-167">Bu işlev uygulaması çağıracaktır [startMonitoringSignificantLocationChanges] uygulamanızı hello arka plana gittiğinde.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-167">Implementation of this function will call [startMonitoringSignificantLocationChanges] when your application goes into hello background.</span></span> <span data-ttu-id="6bd6a-168">Otomatik olarak yeni bir konum olay gelirse hello arka plan uygulamanıza yeniden başlatmak olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-168">Be aware that it will automatically relaunch your application into hello background if a new location event arrives.</span></span>

## <a name="advanced-reporting"></a><span data-ttu-id="6bd6a-169">Gelişmiş raporlama</span><span class="sxs-lookup"><span data-stu-id="6bd6a-169">Advanced reporting</span></span>
<span data-ttu-id="6bd6a-170">Tooreport uygulama belirli olaylar, hatalar ve işleri istiyorsanız, isteğe bağlı olarak, hello hello yöntemleri aracılığıyla toouse hello katılım API gerekir `EngagementAgent` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-170">Optionally, if you want tooreport application specific events, errors and jobs, you need toouse hello Engagement API through hello methods of hello `EngagementAgent` class.</span></span> <span data-ttu-id="6bd6a-171">Bu sınıfın bir nesnesi tarafından arama hello alınabilir `[EngagementAgent shared]` statik yöntemi.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-171">An object of this class can be retrieved by calling hello `[EngagementAgent shared]` static method.</span></span>

<span data-ttu-id="6bd6a-172">Merhaba katılım API toouse tüm Engagement'ın gelişmiş özelliklerinden sağlar ve hello nasıl ayrıntılı tooUse iOS katılım API (Merhaba teknik belgelerine hello gibi yanı `EngagementAgent` sınıfı).</span><span class="sxs-lookup"><span data-stu-id="6bd6a-172">hello Engagement API allows toouse all of Engagement's advanced capabilities and is detailed in hello How tooUse the Engagement API on iOS (as well as in hello technical documentation of hello `EngagementAgent` class).</span></span>

## <a name="disable-idfa-collection"></a><span data-ttu-id="6bd6a-173">IDFA toplamayı devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="6bd6a-173">Disable IDFA collection</span></span>
<span data-ttu-id="6bd6a-174">Varsayılan olarak, katılım hello kullanacağı [IDFA] toouniquely kullanıcı tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-174">By default, Engagement will use hello [IDFA] toouniquely identify a user.</span></span> <span data-ttu-id="6bd6a-175">Ancak başka bir yerde hello uygulamada reklam kullanmıyorsanız hello App Store gözden geçirme işlemi tarafından reddedilmiş.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-175">But if you’re not using advertising elsewhere in hello app, you might be rejected by hello App Store review process.</span></span> <span data-ttu-id="6bd6a-176">IDFA toplamayı hello önişlemci makrosu ekleyerek devre dışı bırakılacak `ENGAGEMENT_DISABLE_IDFA` pch dosyanızdaki (veya hello `Build Settings` uygulamanızın).</span><span class="sxs-lookup"><span data-stu-id="6bd6a-176">IDFA collection can be disabled by adding hello preprocessor macro `ENGAGEMENT_DISABLE_IDFA` in your pch file (or in hello `Build Settings` of your application).</span></span> <span data-ttu-id="6bd6a-177">Bu olduğunu başvuru çok sağlayacak`ASIdentifierManager`, `advertisingIdentifier` veya `isAdvertisingTrackingEnabled` hello uygulama derlemede.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-177">This will ensure that there is no references too`ASIdentifierManager`, `advertisingIdentifier` or `isAdvertisingTrackingEnabled` in hello application build.</span></span>

<span data-ttu-id="6bd6a-178">Merhaba tümleştirme **prefix.pch** dosyası:</span><span class="sxs-lookup"><span data-stu-id="6bd6a-178">Integration in hello **prefix.pch** file:</span></span>

    #define ENGAGEMENT_DISABLE_IDFA
    ...

<span data-ttu-id="6bd6a-179">Merhaba IDFA toplamayı düzgün uygulamanızda hello katılım test günlüklerinin denetleyerek devre dışı olduğunu doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-179">You can verify that hello IDFA collection is properly disabled in your application by checking hello Engagement test logs.</span></span> <span data-ttu-id="6bd6a-180">Merhaba tümleştirme Test bkz\<ios-sdk-engagement-test-ıdfa\> daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-180">See hello Integration Test\<ios-sdk-engagement-test-idfa\> documentation for further information.</span></span>

## <a name="disable-log-reporting"></a><span data-ttu-id="6bd6a-181">Günlük bildirimini devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="6bd6a-181">Disable log reporting</span></span>
### <a name="using-a-method-call"></a><span data-ttu-id="6bd6a-182">Yöntem çağrısı kullanma</span><span class="sxs-lookup"><span data-stu-id="6bd6a-182">Using a method call</span></span>
<span data-ttu-id="6bd6a-183">Katılım toostop günlükleri göndermek istiyorsanız, çağırabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6bd6a-183">If you want Engagement toostop sending logs, you can call:</span></span>

    [[EngagementAgent shared] setEnabled:NO];

<span data-ttu-id="6bd6a-184">Bu çağrı kalıcıdır: kullandığı `NSUserDefaults` toostore hello bilgi.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-184">This call is persistent: it uses `NSUserDefaults` toostore hello information.</span></span>

<span data-ttu-id="6bd6a-185">Aynı işlevi ile Merhaba çağırarak yeniden raporlama günlüğü etkinleştirebilirsiniz `YES`.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-185">You can enable log reporting again by calling hello same function with `YES`.</span></span>

### <a name="integration-in-your-settings-bundle"></a><span data-ttu-id="6bd6a-186">Ayarlar paketi tümleştirme</span><span class="sxs-lookup"><span data-stu-id="6bd6a-186">Integration in your settings bundle</span></span>
<span data-ttu-id="6bd6a-187">Bu işlevi çağırmak yerine, ayrıca bu ayarı doğrudan var olan tümleştirebilirsiniz `Settings.bundle` dosya.</span><span class="sxs-lookup"><span data-stu-id="6bd6a-187">Instead of calling this function, you can also integrate this setting directly in your existing `Settings.bundle` file.</span></span> <span data-ttu-id="6bd6a-188">Merhaba dize `engagement_agent_enabled` ilişkili tooa geçiş anahtar hello tercih tanımlayıcısı ve olarak kullanılmalıdır (`PSToggleSwitchSpecifier`).</span><span class="sxs-lookup"><span data-stu-id="6bd6a-188">hello string `engagement_agent_enabled` must be used as a hello preference identifier and it must be associated tooa toggle switch(`PSToggleSwitchSpecifier`).</span></span>

<span data-ttu-id="6bd6a-189">Merhaba örneği `Settings.bundle` gösterir nasıl tooimplement onu:</span><span class="sxs-lookup"><span data-stu-id="6bd6a-189">hello following example of `Settings.bundle` shows how tooimplement it:</span></span>

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
[aygıt API]: http://go.microsoft.com/?linkid=9876094
[NSLocationWhenInUseUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW26
[NSLocationAlwaysUsageDescription]:https://developer.apple.com/library/prerelease/ios/documentation/General/Reference/InfoPlistKeyReference/Articles/CocoaKeys.html#//apple_ref/doc/uid/TP40009251-SW18
[startMonitoringSignificantLocationChanges]:http://developer.apple.com/library/IOs/#documentation/CoreLocation/Reference/CLLocationManager_Class/CLLocationManager/CLLocationManager.html#//apple_ref/occ/instm/CLLocationManager/startMonitoringSignificantLocationChanges
[IDFA]:https://developer.apple.com/library/ios/documentation/AdSupport/Reference/ASIdentifierManager_Ref/ASIdentifierManager.html#//apple_ref/occ/instp/ASIdentifierManager/advertisingIdentifier
