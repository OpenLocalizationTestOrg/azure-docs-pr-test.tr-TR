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
# <a name="how-toointegrate-engagement-on-ios"></a>Nasıl tooIntegrate Engagement iOS
> [!div class="op_single_selector"]
> * [Windows Evrensel](mobile-engagement-windows-store-integrate-engagement.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-integrate-engagement.md)
>
>

Bu yordam, hello en basit yolu tooactivate Engagement analizi ve izleme işlevlerine iOS uygulamanızda açıklar.

Merhaba Engagement SDK'sı iOS7 + ve Xcode 8 + gerektirir: hello dağıtım hedef uygulamanızın en az olmalıdır iOS 7.

> [!NOTE]
> XCode 7'de gerçekten bağımlı sonra hello kullanabilir [iOS Engagement SDK'sı v3.2.4](https://aka.ms/r6oouh). Bir bilinen hata varsa bu önceki sürümünü Reach modülünü hello 10 iOS aygıtları bakın çalıştırılırken [hello reach modülü tümleştirme](mobile-engagement-ios-integrate-engagement-reach.md) daha fazla ayrıntı için. Toouse hello SDK v3.2.4 belirtin, sonra yalnızca hello Atla varsa `UserNotifications.framework` hello sonraki adımda içeri aktarın.
>
>

Aşağıdaki adımları hello günlüklerinin yeterli tooactivate hello rapor kullanıcıları, oturumlar, etkinlikleri, kilitlenme ve Technicals ilgili tüm istatistikleri toocompute gerekli ' dir. Günlükler Hello rapor olaylar, hatalar ve işleri hello katılım API kullanarak el ile yapılmalıdır gibi bu toocompute diğer istatistiklerin gerekli (bkz [nasıl toouse hello Mobile Engagement iOS uygulamanızı API etiketleme Gelişmiş](mobile-engagement-ios-use-engagement-api.md) Bu istatistikler itibaren Uygulama bağımlıdır.

## <a name="embed-hello-engagement-sdk-into-your-ios-project"></a>Merhaba Engagement SDK'sı iOS projenize ekleme
* Merhaba iOS SDK'sı yükle gelen [burada](http://aka.ms/qk2rnj).
* Ekle hello Engagement SDK'sı tooyour iOS projesi: Xcode'da, sağ, proje seçin tıklayın ve **"çok dosyaları Ekle..."** ve hello seçin `EngagementSDK` klasör.
* Katılım ek çerçeveler toowork gerektirir: hello proje Gezgini'nde, proje bölmesini açın ve doğru hedef hello seçin. Merhaba açın **"Derleme aşamaları"** sekmesi ve hello **"Bağlantı ikiliyi kitaplıklara"** menüsünde bu çerçeveleri ekleyin:

  * `UserNotifications.framework`-kümesi hello bağlantı olarak`Optional`
  * `AdSupport.framework`-kümesi hello bağlantı olarak`Optional`
  * `SystemConfiguration.framework`
  * `CoreTelephony.framework`
  * `CFNetwork.framework`
  * `CoreLocation.framework`
  * `libxml2.dylib`

> [!NOTE]
> Merhaba AdSupport framework kaldırılabilir. Katılım bu framework toocollect hello IDFA gerekir. Ancak, IDFA toplamayı devre \<ios-sdk-engagement-ıdfa\> toocomply bu kimliğiyle ilgili yeni Apple politikasını hello ile
>
>

## <a name="initialize-hello-engagement-sdk"></a>Merhaba Engagement SDK'yı başlatma
Uygulama temsilcinizi toomodify gerekir:

* Uygulama dosyanızı Hello üstünde hello katılım Aracısı içeri aktarın:

      [...]
      #import "EngagementAgent.h"
* Katılım Initialize hello yöntemi içinde '**applicationDidFinishLaunching:**'veya'**uygulama: didFinishLaunchingWithOptions:**':

      - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
      {
        [...]
        [EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];
        [...]
      }

## <a name="basic-reporting"></a>Temel raporlama
### <a name="recommended-method-overload-your-uiviewcontroller-classes"></a>Önerilen yöntem: aşırı yükleme, `UIViewController` sınıfları
Sipariş tooactivate hello raporunda katılım toocompute kullanıcıları, oturumlar, etkinlikleri, kilitlenme ve teknik istatistikleri gerekli tüm hello günlükler, yalnızca tüm yapabileceğiniz, `UIViewController` alt sınıfları devral hello `EngagementViewController` sınıfları (aynı kural için `UITableViewController`  - \> `EngagementTableViewController`).

**Katılım:**

    #import <UIKit/UIKit.h>

    @interface Tab1ViewController : UIViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

**Katılım ile:**

    #import <UIKit/UIKit.h>
    #import "EngagementViewController.h"

    @interface Tab1ViewController : EngagementViewController<UITextFieldDelegate> {
      UITextField* myTextField1;
      UITextField* myTextField2;
    }

    @property (nonatomic, retain) IBOutlet UITextField* myTextField1;
    @property (nonatomic, retain) IBOutlet UITextField* myTextField2;

### <a name="alternate-method-call-startactivity-manually"></a>Alternatif yöntem: çağrı `startActivity()` el ile
Olamaz ya da toooverload istiyor musunuz, `UIViewController` sınıfları, bunun yerine, çağırarak etkinliklerinizi başlatabilirsiniz `EngagementAgent`'s doğrudan yöntemleri.

> [!IMPORTANT]
> Merhaba iOS SDK'sı otomatik olarak çağırır hello `endActivity()` hello uygulama kapatıldığında yöntemi. Bu nedenle, olan *yüksek oranda* toocall hello önerilen `startActivity` hello kullanıcının hello etkinliği değiştirdiğinizde, yöntemi ve çok*hiçbir zaman* çağrısı hello `endActivity` bu yöntem zorlar arama itibaren yöntemi Merhaba geçerli oturum toobe sona erdi.
>
>

## <a name="location-reporting"></a>Konum raporlama
Hizmet Koşulları Apple uygulamaları toouse konum yalnızca istatistikleri amaçla izleme izin vermez. Bu nedenle, yalnızca uygulamanız hello konumu başka bir nedenle izleme de kullanıyorsanız tooenable konumu raporları önerilir.

İOS 8 ile başlayarak, uygulamanızı hello anahtarı için bir dize ayarlayarak konum hizmetleri nasıl kullandığı için bir açıklama sağlamalısınız [NSLocationWhenInUseUsageDescription] veya [NSLocationAlwaysUsageDescription]uygulamanızın Info.plist dosyasında. Engagement hello arka planda tooreport konumu istiyorsanız hello anahtar NSLocationAlwaysUsageDescription ekleyin. Diğer durumlarda, başlangıç anahtarı NSLocationWhenInUseUsageDescription ekleyin. İOS 11 NSLocationAlwaysAndWhenInUseUsageDescription ve NSLocationWhenInUseUsageDescription tooreport arka plan konumu gerektiğini unutmayın.

### <a name="lazy-area-location-reporting"></a>Yavaş alan konumu raporlama
Yavaş alan konumu raporlama sağlar tooreport hello ülke, bölgeye ve yere göre ilişkili toodevices. Bu tür konumu raporlama yalnızca ağ konumlarını (hücre kimliği veya WIFI göre) kullanır. Merhaba aygıt alanına oturum başına en fazla bir kez bildirilir. Merhaba GPS hiçbir zaman kullanılmaz ve bu nedenle bu konumu rapor çok az türü (değil toosay yok) hello pil üzerindeki etkisi.

Kullanıcılar, oturumlar, olayları ve hataları ile ilgili kullanılan toocompute coğrafi istatistikleri bildirilen alanlarıdır. Reach kampanyaları ölçütü olarak de kullanılabilir. bir aygıtı alınırsa teşekkürler toohello olabilir raporlanan alanı bilinen son hello [aygıt API].

tooenable yavaş alan konumu raporlama satır hello katılım Aracısı başlatma sonra aşağıdaki hello ekleyin:

    - (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
    {
      [...]
      [[EngagementAgent shared] setLazyAreaLocationReport:YES];
      [...]
    }

### <a name="real-time-location-reporting"></a>Gerçek zamanlı konum raporlama
Gerçek zamanlı konum raporlama sağlar tooreport hello enlem ve boylam ilişkili toodevices. Varsayılan olarak, bu tür konumu raporlama yalnızca ağ konumlarını (hücre kimliği veya WIFI göre) kullanır ve hello uygulama ön planda (yani oturumu sırasında) çalıştığında hello raporlama yalnızca etkindir.

Gerçek zamanlı konumlarının *değil* toocompute istatistikleri kullanılır. Yalnızca amaçlarına tooallow hello gerçek zamanlı coğrafi yalıtma kullanımıdır \<Reach-İzleyici-bölge sınırlaması\> Reach kampanyaları ölçütü.

tooenable gerçek zamanlı konum raporlama satır hello katılım Aracısı başlatma sonra aşağıdaki hello ekleyin:

    [[EngagementAgent shared] setRealtimeLocationReport:YES];

#### <a name="gps-based-reporting"></a>Raporlama GPS dayalı
Varsayılan olarak, gerçek zamanlı konum raporlama ağ tabanlı konum yalnızca kullanır. GPS tooenable hello kullanımı (olan daha kesin) konumları tabanlı, ekleyin:

    [[EngagementAgent shared] setFineRealtimeLocationReport:YES];

#### <a name="background-reporting"></a>Arka plan raporlama
Merhaba uygulama ön planda (yani oturumu sırasında) çalıştırdığında, varsayılan olarak, gerçek zamanlı konum raporlama yalnızca etkindir. aynı zamanda arka planda raporlama tooenable hello ekleyin:

    [[EngagementAgent shared] setBackgroundRealtimeLocationReport:YES withLaunchOptions:launchOptions];

> [!NOTE]
> Merhaba uygulaması arka planda çalıştığında, ağ tabanlı konumlar sadece bildirilir, etkinleştirilmiş olsa bile GPS hello.
>
>

Bu işlev uygulaması çağıracaktır [startMonitoringSignificantLocationChanges] uygulamanızı hello arka plana gittiğinde. Otomatik olarak yeni bir konum olay gelirse hello arka plan uygulamanıza yeniden başlatmak olduğunu unutmayın.

## <a name="advanced-reporting"></a>Gelişmiş raporlama
Tooreport uygulama belirli olaylar, hatalar ve işleri istiyorsanız, isteğe bağlı olarak, hello hello yöntemleri aracılığıyla toouse hello katılım API gerekir `EngagementAgent` sınıfı. Bu sınıfın bir nesnesi tarafından arama hello alınabilir `[EngagementAgent shared]` statik yöntemi.

Merhaba katılım API toouse tüm Engagement'ın gelişmiş özelliklerinden sağlar ve hello nasıl ayrıntılı tooUse iOS katılım API (Merhaba teknik belgelerine hello gibi yanı `EngagementAgent` sınıfı).

## <a name="disable-idfa-collection"></a>IDFA toplamayı devre dışı bırak
Varsayılan olarak, katılım hello kullanacağı [IDFA] toouniquely kullanıcı tanımlayın. Ancak başka bir yerde hello uygulamada reklam kullanmıyorsanız hello App Store gözden geçirme işlemi tarafından reddedilmiş. IDFA toplamayı hello önişlemci makrosu ekleyerek devre dışı bırakılacak `ENGAGEMENT_DISABLE_IDFA` pch dosyanızdaki (veya hello `Build Settings` uygulamanızın). Bu olduğunu başvuru çok sağlayacak`ASIdentifierManager`, `advertisingIdentifier` veya `isAdvertisingTrackingEnabled` hello uygulama derlemede.

Merhaba tümleştirme **prefix.pch** dosyası:

    #define ENGAGEMENT_DISABLE_IDFA
    ...

Merhaba IDFA toplamayı düzgün uygulamanızda hello katılım test günlüklerinin denetleyerek devre dışı olduğunu doğrulayabilirsiniz. Merhaba tümleştirme Test bkz\<ios-sdk-engagement-test-ıdfa\> daha fazla bilgi için.

## <a name="disable-log-reporting"></a>Günlük bildirimini devre dışı bırak
### <a name="using-a-method-call"></a>Yöntem çağrısı kullanma
Katılım toostop günlükleri göndermek istiyorsanız, çağırabilirsiniz:

    [[EngagementAgent shared] setEnabled:NO];

Bu çağrı kalıcıdır: kullandığı `NSUserDefaults` toostore hello bilgi.

Aynı işlevi ile Merhaba çağırarak yeniden raporlama günlüğü etkinleştirebilirsiniz `YES`.

### <a name="integration-in-your-settings-bundle"></a>Ayarlar paketi tümleştirme
Bu işlevi çağırmak yerine, ayrıca bu ayarı doğrudan var olan tümleştirebilirsiniz `Settings.bundle` dosya. Merhaba dize `engagement_agent_enabled` ilişkili tooa geçiş anahtar hello tercih tanımlayıcısı ve olarak kullanılmalıdır (`PSToggleSwitchSpecifier`).

Merhaba örneği `Settings.bundle` gösterir nasıl tooimplement onu:

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
