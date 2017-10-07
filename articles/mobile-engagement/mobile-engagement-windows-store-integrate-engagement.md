---
title: "aaaWindows Evrensel uygulamalar Engagement SDK tümleştirmesi"
description: "Nasıl Azure Mobile Engagement Windows Evrensel uygulamaları ile tooIntegrate"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 71236b68-5ebd-44aa-8c82-c7ca8098ea05
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 18543798099c233dbe55cc387ba0216e369c8596
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-engagement-sdk-integration"></a>Windows Evrensel uygulamaları Engagement SDK tümleştirmesi
> [!div class="op_single_selector"]
> * [Evrensel Windows](mobile-engagement-windows-store-integrate-engagement.md) 
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md) 
> * [iOS](mobile-engagement-ios-integrate-engagement.md) 
> * [Android](mobile-engagement-android-integrate-engagement.md) 
> 
> 

Bu yordam, hello en basit yolu tooactivate Engagement analizi ve Windows Evrensel uygulamanız işlevlerde izleme açıklar.

Aşağıdaki adımları hello günlüklerinin yeterli tooactivate hello rapor kullanıcıları, oturumlar, etkinlikleri, kilitlenme ve Technicals ilgili tüm istatistikleri toocompute gerekli ' dir. Günlükler Hello rapor olaylar, hatalar ve işleri hello katılım API kullanarak el ile yapılmalıdır gibi bu toocompute diğer istatistiklerin gerekli (bkz [nasıl toouse hello Mobile Engagement Windows Evrensel uygulamanız API etiketleme Gelişmiş](mobile-engagement-windows-store-use-engagement-api.md) beri Bu istatistikler uygulamanın bağımlı olduğu.

## <a name="supported-versions"></a>Desteklenen sürümler
Merhaba Mobile Engagement SDK'sı Windows Evrensel uygulamaları için yalnızca Windows çalışma zamanı ve hedefleyen Evrensel Windows platformu uygulamaları tümleştirilebilir:

* Windows 8
* Windows 8.1
* Windows Phone 8.1
* Windows 10 (Masaüstü ve mobil aileleri)

> [!NOTE]
> Windows Phone Silverlight hedefleme sonra toohello başvuran [Windows Phone Silverlight tümleştirme yordamı](mobile-engagement-windows-phone-integrate-engagement.md).
> 
> 

## <a name="install-hello-mobile-engagement-universal-apps-sdk"></a>Merhaba Mobile Engagement Evrensel uygulamaları SDK yükleme
### <a name="all-platforms"></a>Tüm platformlar
Merhaba Mobile Engagement SDK'sı için Windows Evrensel uygulaması olarak adlandırılan bir Nuget paketi olarak kullanılabilir *MicrosoftAzure.MobileEngagement*. Merhaba Visual Studio Nuget Paket Yöneticisi ' yükleyebilirsiniz.

### <a name="windows-8x-and-windows-phone-81"></a>Windows 8.x ve Windows Phone 8.1
NuGet hello hello SDK kaynakları otomatik olarak dağıtan `Resources` uygulama projenizin hello kökünde klasör.

### <a name="windows-10-universal-windows-platform-applications"></a>Windows 10 Evrensel Windows platformu uygulamaları
NuGet UWP uygulaması henüz hello SDK kaynakları otomatik olarak dağıtmaz. El ile kaynakların dağıtımı kadar NuGet içinde yeniden girmesini toodo vardır:

1. Dosya Gezgini'ni açın.
2. Konum aşağıdaki toohello gidin (**x.x.x** yüklemekte katılım hello sürümüdür): *% USERPROFILE %\\.nuget\packages\MicrosoftAzure.MobileEngagement\\ * *x.x.x**\\content\win81*
3. Sürükle ve bırak hello **kaynakları** hello dosya Gezgini toohello kök Visual Studio, projenizin klasöründen.
4. Visual Studio projenizi seçin ve hello etkinleştirme **tüm dosyaları göster** simgesi hello üstünde **Çözüm Gezgini**.
5. Bazı dosyalar hello projeye dahil edilmez. bunları aynı anda sağ tıklayın hello üzerinde tooimport **kaynakları** klasörü, **projeden hariç** başka sağ tıklayın ardından hello üzerinde **kaynakları** klasörünü **Ekle Proje** toore-hello tüm klasör içerir. Merhaba tüm dosyaları **kaynakları** klasörü projenizde eklenmiştir.

## <a name="add-hello-capabilities"></a>Merhaba yetenekleri ekleme
Merhaba Engagement SDK'sı hello Windows SDK sipariş toowork bazı özellikleri düzgün gerekir.

Açık, `Package.appxmanifest` dosya ve yetenekleri aşağıdaki o hello bildirildiğinden emin olun:

* `Internet (Client)`

## <a name="initialize-hello-engagement-sdk"></a>Merhaba Engagement SDK'yı başlatma
### <a name="engagement-configuration"></a>Katılım yapılandırma
Merhaba katılım yapılandırma hello Merkezi `Resources\EngagementConfiguration.xml` projenizin dosya.

Bu dosya toospecify düzenleyin:

* Uygulama bağlantı dizenizi etiketleri arasına `<connectionString>` ve `<\connectionString>`.

Çalışma zamanında, bunun yerine, çağırabilirsiniz hello aşağıdaki toospecify istiyorsanız yöntemi hello katılım aracı başlatmadan önce:

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);

Merhaba bağlantı dizesi, uygulamanız için Klasik Azure portalı hello üzerinde görüntülenir.

### <a name="engagement-initialization"></a>Katılım başlatma
Yeni bir proje oluşturduğunuzda, bir `App.xaml.cs` dosyası oluşturulur. Bu sınıf devraldığı `Application` ve birçok önemli yöntemler içerir. Ayrıca, kullanılan tooinitialize hello Engagement SDK'sı de olur.

Merhaba değiştirme `App.xaml.cs`:

* Tooyour ekleme `using` deyimleri:
  
      using Microsoft.Azure.Engagement;
* Bir yöntem tooshare hello katılım başlatma tüm çağrıları için bir kez tanımlayın:
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
  
        // or
  
        EngagementAgent.Instance.Init(e, engagementConfiguration);
      }
* Çağrı `InitEngagement` hello içinde `OnLaunched` yöntemi:
  
      protected override void OnLaunched(LaunchActivatedEventArgs e)
      {
        InitEngagement(e);
      }
* Özel bir şema kullanarak uygulamanızı başlatıldığında, başka bir uygulama veya hello komut satırı sonra hello `OnActivated` yöntemi çağrılır. Uygulamanızı etkinleştirildiğinde tooinitiate hello Engagement SDK'sı da gerekir. toodo bu nedenle, geçersiz kılma `OnActivated` yöntemi:
  
      protected override void OnActivated(IActivatedEventArgs args)
      {
        InitEngagement(args);
      }

> [!IMPORTANT]
> Biz, tooadd hello katılım başlatma, uygulamanızın başka bir yerde kesinlikle önerilmemektedir.
> 
> 

## <a name="basic-reporting"></a>Temel raporlama
### <a name="recommended-method-overload-your-page-classes"></a>Önerilen yöntem: aşırı yükleme, `Page` sınıfları
Sipariş tooactivate hello raporunda katılım toocompute kullanıcıları, oturumlar, etkinlikleri, kilitlenme ve teknik istatistikleri gerekli tüm hello günlükler, yalnızca tüm yapabileceğiniz, `Page` alt sınıfları devral hello `EngagementPage` sınıfları.

Örneği nasıl toodo Bu, uygulamanızın bir sayfa için. Yapabileceğiniz Merhaba, uygulamanızın tüm sayfalar için aynı anlama.

#### <a name="c-source-file"></a>C# kaynak dosyası
Sayfanızı değiştirmek `.xaml.cs` dosyası:

* Tooyour ekleme `using` deyimleri:
  
      using Microsoft.Azure.Engagement;
* Değiştir `Page` ile `EngagementPage`:

**Katılım:**

        namespace Example
        {
          public sealed partial class ExamplePage : Page
          {
            [...]
          }
        }

**Katılım ile:**

        using Microsoft.Azure.Engagement;

        namespace Example
        {
          public sealed partial class ExamplePage : EngagementPage 
          {
            [...]
          }
        }

> [!IMPORTANT]
> Sayfanız hello kılıyorsa `OnNavigatedTo` yöntemi, emin toocall olması `base.OnNavigatedTo(e)`. Aksi takdirde hello etkinlik raporlanmayacak (Merhaba `EngagementPage` çağrıları `StartActivity` içinde kendi `OnNavigatedTo` yöntemi).
> 
> 

#### <a name="xaml-file"></a>XAML dosyası
Sayfanızı değiştirmek `.xaml` dosyası:

* Tooyour ad alanları bildirimleri ekleyin:
  
      xmlns:engagement="using:Microsoft.Azure.Engagement"
* Değiştir `Page` ile `engagement:EngagementPage`:

**Katılım:**

        <Page>
            <!-- layout -->
            ...
        </Page>

**Katılım ile:**

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">
            <!-- layout -->
            ...
        </engagement:EngagementPage >

#### <a name="override-hello-default-behaviour"></a>Merhaba varsayılan davranışı geçersiz kılma
Varsayılan olarak, hiçbir ek ile Merhaba etkinlik adı olarak hello sınıf adı hello sayfasının bildirilir. Merhaba sınıfı hello "Sayfa" soneki kullanıyorsa, katılım bunu de kaldırılır.

Merhaba adını toooverride hello varsayılan davranışa istiyorsanız, yalnızca bu tooyour kodu ekleyin:

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
Olamaz ya da toooverload istiyor musunuz, `Page` sınıfları, bunun yerine, çağırarak etkinliklerinizi başlatabilirsiniz `EngagementAgent` doğrudan yöntemleri.

Toocall öneririz `StartActivity` içinde `OnNavigatedTo` sayfanızın yöntemi.

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> Doğru oturumunuzu sonlandırmak emin olun.
> 
> Merhaba Windows Evrensel SDK otomatik olarak çağırır hello `EndActivity` hello uygulama kapatıldığında yöntemi. Bu nedenle, olan **yüksek oranda** toocall hello önerilen `StartActivity` hello kullanıcının hello etkinliği değiştirdiğinizde, yöntemi ve çok**hiçbir zaman** çağrısı hello `EndActivity` yöntemi, bu yöntem, tooEngagement gönderir Sunucu geçerli kullanıcının bırakın hello uygulama olduğundan, bu işlem tüm uygulama günlüklerini etkiler.
> 
> 

## <a name="advanced-reporting"></a>Gelişmiş raporlama
İsteğe bağlı olarak, böylece tooreport uygulama belirli olayları, hataları ve işleri, toodo isteyebilirsiniz, kullanım hello diğer yöntemleri bulunanlar hello `EngagementAgent` sınıfı. Merhaba katılım API toouse tüm Engagement'ın gelişmiş özelliklerinden sağlar.

Daha fazla bilgi için bkz: [nasıl toouse hello Mobile Engagement Windows Evrensel uygulamanız API etiketleme Gelişmiş](mobile-engagement-windows-store-use-engagement-api.md).

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
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

        /* Disable Engagement crash reporting. */
        engagementConfiguration.Agent.ReportCrash = false;

### <a name="burst-mode"></a>Veri bloğu modu
Varsayılan olarak, hello katılım hizmet raporları gerçek zamanlı olarak günlüğe kaydeder. Uygulamanızı günlükleri çok sık raporları, daha iyi toobuffer hello günlükleri ve tooreport varsa, bunları (Merhaba "veri bloğu modu" denir) tümünü bir defada bir normal zaman temel üzerinde.

toodo, bu nedenle, hello yöntemi çağırın:

        EngagementAgent.Instance.SetBurstThreshold(int everyMs);

Merhaba bağımsız değişkeni olarak bir değerdir **milisaniye**. Tooreactivate hello gerçek zamanlı günlük tutma istiyorsanız, herhangi bir zamanda hello yöntemini hello 0 değerine sahip veya herhangi bir parametre olmadan yalnızca çağırın.

Merhaba veri bloğu modu biraz artırmak hello pil ömrü ancak Engagement İzleyicisi Merhaba üzerinde bir etkisi vardır: tüm oturumları ve işleri süresi yuvarlak toohello veri bloğu eşiği (Bu nedenle, oturumlar ve işleri hello veri bloğu eşik görünmeyebilir daha kısa) olacaktır. Bu bir veri bloğu eşikten artık 30000 (30s) toouse önerilir. Toobe Günlükleri kaydedilen sınırlı too300 öğeleridir farkında olması. Gönderme çok uzunsa, bazı günlükleri kaybedebilir.

> [!WARNING]
> Merhaba veri bloğu eşik tooa dönemi 1'ler küçüktür yapılandırılamaz. Toodo şekilde çalışırsanız, SDK izleme hello hatasıyla göstermek ve otomatik olarak hello toohello varsayılan değer, yani, 0s sıfırlayın. Bu hello SDK tooreport hello günlükler gerçek zamanlı tetikler.
> 
> 

[here]:http://www.nuget.org/packages/Capptain.WindowsCS
[NuGet website]:http://docs.nuget.org/docs/start-here/overview

