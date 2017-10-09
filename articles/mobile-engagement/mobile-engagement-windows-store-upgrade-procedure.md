---
title: "aaaWindows Evrensel uygulamaları SDK yükseltme yordamları"
description: "Azure Mobile Engagement için Windows Evrensel uygulamaları SDK yükseltme yordamları"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 4c898175-2cd6-43db-b350-bb408332f24d
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 95aba5d55cd65d4190aad35737f872414b5ed443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-sdk-upgrade-procedures"></a>Windows Evrensel uygulamaları SDK yükseltme yordamları
Uygulamanıza katılım daha eski bir sürümü zaten bütünleştirdiyseniz noktaları hello SDK yükseltirken aşağıdaki tooconsider hello sahip.

Merhaba SDK çeşitli sürümleri eksik birkaç yordamları toofollow olabilir. 0.10.1 geçirirseniz örneğin hello izleyin toofirst sahip too0.11.0 "0.9.0'dan gelen too0.10.1" yordamı sonra hello "0.10.1 gelen too0.11.0" yordamı.

## <a name="from-330-too340"></a>3.3.0 gelen too3.4.0
### <a name="test-logs"></a>Test günlükleri
Konsol günlükleri Hello SDK tarafından üretilen artık etkin/devre dışı bırakılmış/filtrelenmiş olabilir. toocustomize Bu, güncelleştirme hello özellik `EngagementAgent.Instance.TestLogEnabled` tooone hello kullanılabilir hello değerinin `EngagementTestLogLevel` numaralandırma, örneğin:

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();

### <a name="resources"></a>Kaynaklar
Merhaba ulaşma katmana geliştirilmiştir. Merhaba SDK NuGet paketini kaynakları parçasıdır.

Merhaba SDK'ın yeni sürümü toohello yükseltirken tookeep istediğinizi varolan hello dosyalarınızdan kaynaklarınızın klasör veya kaplama seçebilirsiniz:

* Merhaba önceki katmana sizin yerinize çalıştığından veya hello tümleştirme `WebView` öğeleri el ile mevcut dosyalarınızı tookeep karar verebilirsiniz sonra çalışmaya devam edecektir. 
* Tooupdate toohello yeni katmana, yalnızca Değiştir hello tüm istiyorsanız `overlay` kaynaklarınızla hello SDK paketinden yeni bir hello klasöründen (UWP uygulamaları: hello yükseltmeden sonra % USERPROFILE % hello yeni katmana klasör alabilirsiniz\\. nuget\ packages\MicrosoftAzure.MobileEngagement\3.4.0\content\win81\Resources).

> [!WARNING]
> Merhaba yeni katmana kullanarak hello önceki sürümünde yapılan tüm özelleştirmeler üzerine yazar.
> 
> 

## <a name="from-320-too330"></a>3.2.0 gelen too3.3.0
### <a name="resources"></a>Kaynaklar
Bu adım yalnızca özelleştirilmiş kaynaklar ile ilgilidir. Toobackup sahip hello SDK (html, görüntüler, katmana) tarafından sağlanan hello kaynakları özelleştirdiyseniz, yükseltme ve yeniden Uygula önce bunları özelleştirmeyi üzerinde yükseltilmiş kaynakları.

## <a name="from-310-too320"></a>3.1.0 gelen too3.2.0
### <a name="resources"></a>Kaynaklar
Bu adım yalnızca özelleştirilmiş kaynaklar ile ilgilidir. Toobackup sahip hello SDK (html, görüntüler, katmana) tarafından sağlanan hello kaynakları özelleştirdiyseniz, yükseltme ve yeniden Uygula önce bunları özelleştirmeyi üzerinde yükseltilmiş kaynakları.

### <a name="webview-integration"></a>Web görünümü tümleştirme
Bazı geliştirmeler toomatch farklı cihaz form faktörleri'nın bu sürümünde sunulan. Merhaba webview, tümleştirilmesi hello aşağıdaki eşleştiğinden emin olun:

XAML sayfası () içinde:

            <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Right" VerticalAlignment="Top"/>
            <WebView x:Name="engagement_announcement_content" Visibility="Collapsed" HorizontalAlignment="Right" VerticalAlignment="Top"/> 

Ve ilişkili .cs dosyanızda:

    using Microsoft.Azure.Engagement;
    using System;
    using Windows.ApplicationModel.Core;
    using Windows.UI.ViewManagement;
    using Windows.UI.Xaml;
    using Windows.UI.Xaml.Navigation;

    namespace My.Namespace.Example
    {
            /// <summary>
            /// An empty page that can be used on its own or navigated toowithin a Frame.
            /// </summary>
            public sealed partial class ExampleEngagementReachPage : EngagementPage
            {
              public ExampleEngagementReachPage()
              {
                this.InitializeComponent();

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }

              #region tooimplement
              /* Attach events when page is navigated. */
              protected override void OnNavigatedTo(NavigationEventArgs e)
              {
                /* Update hello webview when hello app window is resized. */
                Window.Current.SizeChanged += DisplayProperties_OrientationChanged;

                /* Update hello webview when hello app/status bar is resized. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged += DisplayProperties_VisibleBoundsChanged; 
    #endif
                base.OnNavigatedTo(e);
              }

              /* When page is left ensure toodetach SizeChanged handler. */
              protected override void OnNavigatedFrom(NavigationEventArgs e)
              {
                Window.Current.SizeChanged -= DisplayProperties_OrientationChanged;
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
                ApplicationView.GetForCurrentView().VisibleBoundsChanged -= DisplayProperties_VisibleBoundsChanged;
    #endif
                base.OnNavigatedFrom(e);
              }

              /* "width" and "height" are hello current size of your application display. */
    #if WINDOWS_PHONE_APP || WINDOWS_UWP
              double width = ApplicationView.GetForCurrentView().VisibleBounds.Width;
              double height = ApplicationView.GetForCurrentView().VisibleBounds.Height;
    #else
              double width =  Window.Current.Bounds.Width;
              double height =  Window.Current.Bounds.Height;
    #endif

              /// <summary>
              /// Set your webview elements toohello correct size.
              /// </summary>
              /// <param name="width">hello width of your current display.</param>
              /// <param name="height">hello height of your current display.</param>
              private void SetWebView(double width, double height)
              {
                #pragma warning disable 4014
                CoreApplication.MainView.CoreWindow.Dispatcher.RunAsync(Windows.UI.Core.CoreDispatcherPriority.Normal,
                        () =>
                        {
                          this.engagement_notification_content.Width = width;
                          this.engagement_announcement_content.Width = width;
                          this.engagement_announcement_content.Height = height;
                        });
              }

              /// <summary>
              /// Handler that takes hello Windows.Current.SizeChanged and indicates that webviews have toobe resized.
              /// </summary>
              /// <param name="sender">Original event trigger.</param>
              /// <param name="e">Window Size Changed Event arguments.</param>
              private void DisplayProperties_OrientationChanged(object sender, Windows.UI.Core.WindowSizeChangedEventArgs e)
              {
                double width = e.Size.Width;
                double height = e.Size.Height;

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }

    #if WINDOWS_PHONE_APP || WINDOWS_UWP              
              /// <summary>
              /// Handler that takes hello ApplicationView.VisibleBoundsChanged and indicates that webviews have toobe resized
              /// </summary>
              /// <param name="sender">hello related application view.</param>
              /// <param name="e">Related event arguments.</param>
              private void DisplayProperties_VisibleBoundsChanged(ApplicationView sender, Object e)
              {
                double width = sender.VisibleBounds.Width;
                double height = sender.VisibleBounds.Height;

                /* Set your webview elements toohello correct size. */
                SetWebView(width, height);
              }
    #endif
              #endregion
            }
    }

## <a name="from-200-too300"></a>2.0.0 gelen too3.0.0
### <a name="resources"></a>Kaynaklar
Bu adım yalnızca özelleştirilmiş kaynaklar ile ilgilidir. Toobackup sahip hello SDK (html, görüntüler, katmana) tarafından sağlanan hello kaynakları özelleştirdiyseniz, yükseltme ve yeniden Uygula önce bunları özelleştirmeyi üzerinde yükseltilmiş kaynakları.

## <a name="from-111-too200"></a>1.1.1 gelen too2.0.0
Merhaba toomigrate'nın Azure Mobile Engagement tarafından desteklenen bir uygulamaya bir SDK tümleştirmesi hello Capptain hizmet gelen Capptain SAS tarafından nasıl sunulan açıklanmıştır. 

> [!IMPORTANT]
> Capptain ve Mobile Engagement olan değil hello aynı Hizmetleri ve yalnızca aşağıda verilen hello yordamı nasıl toomigrate hello istemci uygulamaları vurgular. Geçirme hello SDK hello uygulama hello Capptain sunucuları toohello Mobile Engagement sunuculardan veri geçişi YAPILMAZ
> 
> 

Önceki bir sürümünden geçiş yapıyorsanız, lütfen hello Capptain web sitesi toomigrate too1.1.1 ilk başvurun sonra hello aşağıdaki yordamı uygulayın

### <a name="nuget-package"></a>Nuget paketi
Değiştir **Capptain.WindowsPhone** tarafından **MicrosoftAzure.MobileEngagement** Nuget paketi.

### <a name="applying-mobile-engagement"></a>Mobil katılım uygulama
Merhaba SDK kullanan hello terim `Engagement`. Proje toomatch tooupdate gereken bu değişikliği.

Toouninstall, geçerli Capptain nuget paketi gerekir. Tüm değişikliklerinizi Capptain Kaynaklar klasörünü kaldırılacak göz önünde bulundurun. Tookeep istiyorsanız, bu dosyaların bir kopyasını sonra yapın.

Bundan sonra projenizde hello yeni Microsoft Azure katılım nuget paketini yükleyin. Doğrudan [nuget sitesinde] bulabilirsiniz. veya burada dizini. Tüm kaynak dosyaları katılım tarafından kullanılan ve hello yeni katılım DLL tooyour ekler bu eylem değiştirir başvuruları yansıtın.

Proje başvuruları Capptain DLL başvurularını silerek tooclean sahip. Bunu yapmazsanız Capptain hello sürümü çakışır ve hataları gerçekleşir.

Capptain kaynakları özelleştirdiyseniz, eski dosyaları içeriğinizi kopyalayın ve bunları hello yeni katılım dosyalarında yapıştırın. Xaml ve cs dosyaları güncelleştirilmiş toobe gerektiğini unutmayın.

Bu adımlar tamamlandığında tooreplace eski Capptain başvurular hello yeni katılım başvurular tarafından yeterlidir.

1. Tüm Capptain ad güncelleştirilmiş toobe sahip.
   
    Geçişten önce:
   
        using Capptain.Agent;
        using Capptain.Reach;
   
    Geçişten sonra:
   
        using Microsoft.Azure.Engagement;
2. "Capptain" içeren tüm Capptain sınıfları "Katılım" içermelidir.
   
    Geçişten önce:
   
        public sealed partial class MainPage : CapptainPage
        {
          protected override string GetCapptainPageName()
          {
            return "Capptain Demo";
          }
          ...
        }
   
    Geçişten sonra:
   
        public sealed partial class MainPage : EngagementPage
        {
          protected override string GetEngagementPageName()
          {
            return "Engagement Demo";
          }
          ...
        }
3. XAML dosyaları için de Capptain ad alanı ve özniteliklerini değiştirir.
   
    Geçişten önce:
   
        <capptain:CapptainPage
        ...
        xmlns:capptain="clr-namespace:Capptain.Agent;assembly=Capptain.Agent.WP"
        ...
        </capptain:CapptainPage>
   
    Geçişten sonra:
   
        <engagement:EngagementPage
        ...
        xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
        ...
        </engagement:EngagementPage>
4. Sayfa değiştirir
   
   > [!IMPORTANT]
   > Ayrıca değiştirir. Yeni ad `Microsoft.Azure.Engagement.Overlay`. Xaml ve cs dosyaları kullanılan toobe sahiptir. Üstelik `CapptainGrid` toobe adlı `EngagementGrid`, `capptain_notification_content` ve `capptain_announcement_content` adlandırıldığı `engagement_notification_content` ve `engagement_announcement_content`.
   > 
   > 
   
    Katmana için:
   
        <capptain:CapptainPageOverlay
          xmlns:capptain="using:Capptain.Overlay"
          ...
        </capptain:CapptainPageOverlay>
   
    Bu olur:
   
        <EngagementPageOverlay
          engagement="using:Microsoft.Azure.Engagement.Overlay"
          ...
        </engagement:EngagementPageOverlay>
5. Merhaba Capptain resimler ve HTML dosyaları gibi diğer kaynaklar lütfen unutmayın. bunlar da yeniden adlandırılmış toouse "Katılım" olmuştur.

### <a name="project-declaration"></a>Proje bildirimi
Package.appxmanifest üzerinde `File Type Associations` gelen güncelleştirildi:

* capptain\_ulaşmak\_içerik tooengagement\_ulaşmak\_içeriği
* capptain\_günlük\_tooengagement dosya\_günlük\_dosyası

### <a name="application-id--sdk-key"></a>Uygulama Kimliği / SDK anahtarı
Katılım bağlantı dizesini kullanır. Bir uygulama kimliği ve Mobile Engagement SDK'sı anahtarla toospecify yoksa, toospecify bir bağlantı dizesi yeterlidir. Bunu EngagementConfiguration dosyanızı ayarlayabilirsiniz.

Merhaba katılım yapılandırma ayarlanabilir, `Resources\EngagementConfiguration.xml` projenizin dosya.

Bu dosya toospecify düzenleyin:

* Uygulama bağlantı dizenizi etiketleri arasına `<connectionString>` ve `<\connectionString>`.

Çalışma zamanında, bunun yerine, çağırabilirsiniz hello aşağıdaki toospecify istiyorsanız yöntemi hello katılım aracı başlatmadan önce:

    /* Engagement configuration. */
    EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
    engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

    /* Initialize Engagement agent with above configuration. */
    EngagementAgent.Instance.Init(args, engagementConfiguration);

Merhaba bağlantı dizesi, uygulamanız için Klasik Azure portalı hello üzerinde görüntülenir.

### <a name="items-name-change"></a>Öğe adı değişikliği
Tüm öğeleri adlı *capptain* adlandırılmış *engagement*. Benzer şekilde *Capptain* çok*Engagement*.

Yaygın olarak kullanılan Capptain öğeleri örnekleri:

* Şimdi EngagementConfiguration adlı CapptainConfiguration
* Şimdi EngagementAgent adlı CapptainAgent
* Şimdi EngagementReach adlı CapptainReach
* Şimdi EngagementHttpConfig adlı CapptainHttpConfig
* Şimdi GetEngagementPageName adlı GetCapptainPageName

Ayrıca etkiler yeniden adlandırmak Not yöntemleri geçersiz kılındı.

