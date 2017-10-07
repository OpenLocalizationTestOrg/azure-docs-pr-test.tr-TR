---
title: "aaaWindows Phone Silverlight Engagement SDK tümleştirmesi"
description: "Nasıl Azure Mobile Engagement Windows Phone Silverlight uygulamaları ile tooIntegrate"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 447fea8d-f4e3-4ad4-8ec0-8e3cf1ad3ab0
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: f65683a62e5256cea469a3a73d99ade4331cb6bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-phone-silverlight-engagement-sdk-integration"></a>Windows Phone Silverlight Engagement SDK tümleştirmesi
> [!div class="op_single_selector"]
> * [Windows Evrensel](mobile-engagement-windows-store-integrate-engagement.md) 
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [iOS](mobile-engagement-ios-integrate-engagement.md) 
> * [Android](mobile-engagement-android-integrate-engagement.md) 
> 
> 

Bu yordam, hello en basit yolu tooactivate Azure Mobile Engagement analizi ve izleme, Windows Phone Silverlight uygulamanızda işlevlerine açıklar.

Aşağıdaki adımları hello günlüklerinin yeterli tooactivate hello rapor kullanıcıları, oturumlar, etkinlikleri, kilitlenme ve Technicals ilgili tüm istatistikleri toocompute gerekli ' dir. Günlükler Hello rapor olaylar, hatalar ve işleri hello katılım API kullanarak el ile yapılmalıdır gibi bu toocompute diğer istatistiklerin gerekli (bkz [nasıl toouse hello Mobile Engagement Windows Phone Silverlight uygulamanızda API etiketleme Gelişmiş](mobile-engagement-windows-phone-use-engagement-api.md) Aşağıda) bu istatistikleri uygulama bağımlı olduğundan.

## <a name="supported-versions"></a>Desteklenen sürümler
Merhaba Windows Silverlight için Mobile Engagement SDK'sı yalnızca hedefleme uygulamalara tümleştirilebilir:

* Windows Phone 8.0
* Windows Phone 8.1 Silverlight

> [!NOTE]
> Windows Phone 8.1 (Silverlight olmayan) hedefliyorsanız sonra toohello başvuran [Windows Evrensel tümleştirme yordamı](mobile-engagement-windows-store-integrate-engagement.md).
> 
> 

## <a name="install-hello-mobile-engagement-silverlight-sdk"></a>Merhaba Mobile Engagement Silverlight SDK yükleme
Merhaba Windows Silverlight için Mobile Engagement SDK'sı olarak adlandırılan bir Nuget paketi olarak kullanılabilir *MicrosoftAzure.MobileEngagement*. Merhaba Visual Studio Nuget Paket Yöneticisi ' yükleyebilirsiniz. 

## <a name="add-hello-capabilities"></a>Merhaba yetenekleri ekleme
Merhaba Engagement SDK'sı hello Windows Phone Silverlight SDK sipariş toowork bazı özellikleri düzgün gerekir.

Açık, `WMAppManifest.xml` dosya ve yetenekleri aşağıdaki o hello hello bildirildiğinden emin `Capabilities` paneli:

* `ID_CAP_NETWORKING`
* `ID_CAP_IDENTITY_DEVICE`

## <a name="initialize-hello-engagement-sdk"></a>Merhaba Engagement SDK'yı başlatma
### <a name="engagement-configuration"></a>Katılım yapılandırma
Merhaba katılım yapılandırma hello Merkezi `Resources\EngagementConfiguration.xml` projenizin dosya.

Bu dosya toospecify düzenleyin:

* Uygulama bağlantı dizenizi etiketleri arasına `<connectionString>` ve `<\connectionString>`.

Çalışma zamanında, bunun yerine, çağırabilirsiniz hello aşağıdaki toospecify istiyorsanız yöntemi hello katılım aracı başlatmadan önce:

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(engagementConfiguration);

Merhaba bağlantı dizesi, uygulamanız için Klasik Azure portalı hello üzerinde görüntülenir.

### <a name="engagement-initialization"></a>Katılım başlatma
Yeni bir proje oluşturduğunuzda, bir `App.xaml.cs` dosyası oluşturulur. Bu sınıf devraldığı `Application` ve birçok önemli yöntemler içerir. Ayrıca, kullanılan tooinitialize hello Engagement SDK'sı de olur.

Merhaba değiştirme `App.xaml.cs`:

* Tooyour ekleme `using` deyimleri:
  
      using Microsoft.Azure.Engagement;
* INSERT `EngagementAgent.Instance.Init` hello içinde `Application_Launching` yöntemi:
  
      private void Application_Launching(object sender, LaunchingEventArgs e)
      {
        EngagementAgent.Instance.Init();
      }
* INSERT `EngagementAgent.Instance.OnActivated` hello içinde `Application_Activated` yöntemi:
  
      private void Application_Activated(object sender, ActivatedEventArgs e)
      {
         EngagementAgent.Instance.OnActivated(e);
      }

> [!WARNING]
> Biz, tooadd hello katılım başlatma, uygulamanızın başka bir yerde kesinlikle önerilmemektedir. Ancak, farkında olmanız bu hello `EngagementAgent.Instance.Init` yöntemi, adanmış bir iş parçacığı üzerinde ve hello kullanıcı Arabirimi iş parçacığı üzerinde çalışır.
> 
> 

## <a name="basic-reporting"></a>Temel raporlama
### <a name="recommended-method--overload-your-phoneapplicationpage-classes"></a>Önerilen yöntem: aşırı yükleme, `PhoneApplicationPage` sınıfları
Sipariş tooactivate hello raporunda katılım toocompute kullanıcıları, oturumlar, etkinlikleri, kilitlenme ve teknik istatistikleri gerekli tüm hello günlükler, yalnızca tüm yapabileceğiniz, `PhoneApplicationPage` alt sınıfları devral hello `EngagementPage` sınıfları.

Örneği nasıl toodo Bu, uygulamanızın bir sayfa için. Yapabileceğiniz Merhaba, uygulamanızın tüm sayfalar için aynı anlama.

#### <a name="c-source-file"></a>C# kaynak dosyası
Sayfanızı değiştirmek `.xaml.cs` dosyası:

* Tooyour ekleme `using` deyimleri:
  
      using Microsoft.Azure.Engagement;
* Değiştir `PhoneApplicationPage` ile `EngagementPage` :

**Katılım:**

        namespace Example
        {
          public partial class ExamplePage : PhoneApplicationPage
          {
            [...]
          }
        }

**Katılım ile:**

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!WARNING]
> Sayfanız hello devralıyorsa `OnNavigatedTo` yöntemi, dikkatli toolet hello olması `base.OnNavigatedTo(e)` çağırın. Aksi takdirde hello etkinlik raporlanmaz. Aslında, hello `EngagementPage` arayan `StartActivity` hello içinde `OnNavigatedTo` yöntemi.
> 
> 

#### <a name="xaml-file"></a>XAML dosyası
Sayfanızı değiştirmek `.xaml` dosyası:

* Tooyour ad alanları bildirimleri ekleyin:
  
      xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
* Değiştir `phone:PhoneApplicationPage` ile `engagement:EngagementPage` :

**Katılım:**

        <phone:PhoneApplicationPage>
            <!-- layout -->
        </phone:PhoneApplicationPage>

**Katılım ile:**

        <engagement:EngagementPage 
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP">

            <!-- layout -->
        </engagement:EngagementPage >

#### <a name="override-hello-default-behavior"></a>Merhaba varsayılan davranışı geçersiz kılma
Varsayılan olarak, hiçbir ek ile Merhaba etkinlik adı olarak hello sınıf adı hello sayfasının bildirilir. Merhaba sınıfı hello "Sayfa" soneki kullanıyorsa, katılım bunu de kaldırılır.

Merhaba adını toooverride hello varsayılan davranışı istiyorsanız, yalnızca bu tooyour kodu ekleyin:

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
           /* your code */
           return "new name";
        }

Etkinliği ile bazı ek bilgiler tooreport istiyorsanız, bu tooyour kodu ekleyebilirsiniz:

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
           /* your code */
           return extra;
        }

Bu yöntemler içinde hello denir `OnNavigatedTo` sayfanızın yöntemi.

### <a name="alternate-method-call-startactivity-manually"></a>Alternatif yöntem: çağrı `StartActivity()` el ile
Olamaz ya da toooverload istiyor musunuz, `PhoneApplicationPage` sınıfları, bunun yerine, çağırarak etkinliklerinizi başlatabilirsiniz `EngagementAgent` doğrudan yöntemleri.

Arama öneririz `StartActivity` içinde `OnNavigatedTo` , mainpage yöntemi.

        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
           base.OnNavigatedTo(e);
           EngagementAgent.Instance.StartActivity("MyPage");
        }

> [!IMPORTANT]
> Doğru oturumunuzu sonlandırmak emin olun.
> 
> Merhaba SDK otomatik olarak çağırır hello `EndActivity` hello uygulama kapatıldığında yöntemi. Bu nedenle, olan **yüksek oranda** toocall hello önerilen `StartActivity` hello kullanıcının hello etkinliği değiştirdiğinizde, yöntemi ve çok**hiçbir zaman** çağrısı hello `EndActivity` yöntemi. Bu yöntem hello geçerli kullanıcı Merhaba uygulaması ayrıldı ve bu tüm uygulama günlüklerini etkiler message toohello katılım Sunucusu'nun gönderir.
> 
> 

## <a name="advanced-reporting"></a>Gelişmiş raporlama
İsteğe bağlı olarak, böylece tooreport uygulama belirli olayları, hataları ve işleri, toodo isteyebilirsiniz, kullanım hello diğer yöntemleri bulunanlar hello `EngagementAgent` sınıfı. Merhaba katılım API toouse tüm Engagement'ın gelişmiş özelliklerinden sağlar.

Daha fazla bilgi için bkz: [nasıl toouse hello Mobile Engagement Windows Phone Silverlight uygulamanızda API etiketleme Gelişmiş](mobile-engagement-windows-phone-use-engagement-api.md).

## <a name="advanced-configuration"></a>Gelişmiş yapılandırma
### <a name="disable-automatic-crash-reporting"></a>Otomatik Kilitlenme bildirimini devre dışı bırak
Merhaba otomatik kilitlenme raporlama katılım özelliği devre dışı bırakabilirsiniz. Ardından, işlenmeyen bir özel durum meydana gelir, katılım hiçbir şey olmaz.

> [!WARNING]
> Bu özellik toodisable planlıyorsanız, uygulamanızda işlenmeyen bir kilitlenme meydana gelir, katılım hello kilitlenme göndermez unutmayın **ve** hello oturum ve işleri kapanmaz.
> 
> 

Raporlama toodisable otomatik kilitlenme yalnızca yapılandırmanıza bağlı olarak, bildirilen hello şekilde özelleştirin:

#### <a name="from-engagementconfigurationxml-file"></a>Gelen `EngagementConfiguration.xml` dosyası
Raporu çökme çok Ayarla`false` arasında `<reportCrash>` ve `</reportCrash>` etiketler.

#### <a name="from-engagementconfiguration-object-at-run-time"></a>Gelen `EngagementConfiguration` çalışma zamanında nesne
EngagementConfiguration nesnesini kullanarak rapor kilitlenme toofalse ayarlayın.

        /* Engagement configuration. */

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration(); engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";
        /\* Disable Engagement crash reporting. \*/ engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a>Veri bloğu modu
Varsayılan olarak, hello katılım hizmet raporları gerçek zamanlı olarak günlüğe kaydeder. Uygulamanızı günlükleri çok sık raporları, daha iyi toobuffer hello günlükleri ve tooreport varsa, bunları (Merhaba "veri bloğu modu" denir) tümünü bir defada bir normal zaman temel üzerinde.

toodo, bu nedenle, hello yöntemi çağırın:

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

Merhaba bağımsız değişkeni olarak bir değerdir **milisaniye**. Tooreactivate hello gerçek zamanlı günlük tutma istiyorsanız, herhangi bir zamanda hello yöntemini hello 0 değerine sahip veya herhangi bir parametre olmadan yalnızca çağırın.

Merhaba veri bloğu modu biraz artırmak hello pil ömrü ancak Engagement İzleyicisi Merhaba üzerinde bir etkisi vardır: tüm oturumları ve işleri süresi yuvarlak toohello veri bloğu eşiği (Bu nedenle, oturumlar ve işleri hello veri bloğu eşik görünmeyebilir daha kısa) olacaktır. Bu bir veri bloğu eşikten artık 30000 (30s) toouse önerilir. Toobe Günlükleri kaydedilen sınırlı too300 öğeleridir farkında olması. Gönderme çok uzunsa, bazı günlükleri kaybedebilir.

> [!WARNING]
> Merhaba veri bloğu eşik tooa süresi küçük yapılandırılamaz bir saniye daha. Toodo şekilde çalışırsanız, SDK izleme hello hatasıyla göstermek ve otomatik olarak hello toohello varsayılan değer, sıfırlama diğer bir deyişle, sıfır saniye. Bu hello SDK tooreport hello günlükler gerçek zamanlı tetikler.
> 
> 

