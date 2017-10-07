---
title: "aaaWindows Evrensel uygulamalar Reach SDK tümleştirmesi"
description: "Nasıl tooIntegrate Azure Mobile Engagement Reach ile Windows Evrensel uygulamaları"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: a31ca1d6-856f-4aec-898a-07969ae5f7ec
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: af311c65940014083333853875a00173b8d6783e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="windows-universal-apps-reach-sdk-integration"></a>Windows Evrensel uygulamaları Reach SDK tümleştirmesi
Merhaba tümleştirme hello yordamını izleyin [Windows Evrensel Engagement SDK tümleştirmesi](mobile-engagement-windows-store-integrate-engagement.md) bu kılavuz aşağıdaki önce.

## <a name="embed-hello-engagement-reach-sdk-into-your-windows-universal-project"></a>Windows Evrensel projenize Hello Engagement Reach SDK'sı ekleme
Herhangi bir şey yok tooadd. `EngagementReach`Projenizde başvuruları ve kaynak zaten var.

> [!TIP]
> Hello bulunan görüntüleri özelleştirebilirsiniz `Resources` klasörü projenizin, özellikle hello marka simgesini (Bu varsayılan toohello katılım simge). Evrensel uygulamaları hello de taşıyabilirsiniz `Resources` içeriği uygulamalar, ancak arasında olacaktır, paylaşılan bir proje tooshare klasöründe tookeep hello `Resources\EngagementConfiguration.xml` platform bağımlı olduğu gibi varsayılan konumuna dosya.
> 
> 

## <a name="enable-hello-windows-notification-service"></a>Merhaba Windows bildirim Hizmeti'ni etkinleştir
### <a name="windows-8x-and-windows-phone-81-only"></a>Windows 8.x ve Windows Phone 8.1 yalnızca
Sipariş toouse hello içinde **Windows bildirim hizmeti** (WNS adlandırılır) içinde `Package.appxmanifest` üzerinde dosya `Application UI` tıklayın `All Image Assets` hello sol bot kutusunda. Merhaba kutusunun sağında hello adresindeki `Notifications`, değiştirme `toast capable` gelen `(not set)` çok`(Yes)`.

### <a name="all-platforms"></a>Tüm platformlar
Uygulama tooyour Microsoft hesabı ve toohello katılım platformunuz toosynchronize gerekir. Bu toocreate bir hesap gerekir veya oturum açma [windows Geliştirme Merkezi](https://dev.windows.com). Sonra yeni bir uygulama oluşturun ve Bul SID'sini ve gizli anahtarını hello. Uygulama ayarınız Hello katılım ön uçta gidin `native push` ve kimlik bilgilerinizi yapıştırın. Bundan sonra projenize sağ üzerinde select tıklayın `store` ve `Associate App with hello Store...`. Tooselect Merhaba uygulaması yeterlidir, oluşturduğunuz toosynchronize önce onu.

## <a name="initialize-hello-engagement-reach-sdk"></a>Merhaba Engagement Reach SDK'sını başlatma
Merhaba değiştirme `App.xaml.cs`:

* INSERT `EngagementReach.Instance.Init` hemen sonra `EngagementAgent.Instance.Init` içinde `InitEngagement` yöntemi:
  
      private void InitEngagement(IActivatedEventArgs e)
      {
        EngagementAgent.Instance.Init(e);
        EngagementReach.Instance.Init(e);
      }
  
  Merhaba `EngagementReach.Instance.Init` adanmış bir iş parçacığı çalıştırır. Toodo sahip değil, kendiniz.

> [!NOTE]
> Anında iletme bildirimleri, uygulamanızda başka bir yerde kullanıyorsanız sonra çok sahip[itme kanalını paylaşan](#push-channel-sharing) Engagement Reach ile.
> 
> 

## <a name="integration"></a>Tümleştirme
Duyuruları ve yoklamaları uygulamanızda katılım sağlayan iki yolla tooadd hello ulaşma uygulama başlıkları ve Interstitial görünümleri: hello kaplama tümleştirme ve hello web görünümleri el ile tümleştirme. Her iki yaklaşım hello üzerinde birleştirmelisiniz değil aynı sayfa.

Bu şekilde hello iki tümleştirme arasında seçim Hello özetlenen:

* Sayfalarınızın zaten devralıyorsa hello Aracısı ' hello yer paylaşımlı tümleştirme seçebilirsiniz `EngagementPage`, onu değiştirme yalnızca bir konudur `EngagementPage` tarafından `EngagementPageOverlay` ve `xmlns:engagement="using:Microsoft.Azure.Engagement"` tarafından `xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"` sayfalarınızı içinde.
* Başka bir devralma düzeyi tooyour sayfaları içindeki sayfalarınızı tooprecisely yer hello UI erişmek isterseniz veya tooadd istemiyorsanız hello web görünümleri el ile tümleştirme'yı seçebilirsiniz. 

### <a name="overlay-integration"></a>Yer paylaşımlı tümleştirme
Merhaba katılım katmana hello kullanıcı Arabirimi öğeleri toodisplay Reach kampanyaları sayfanızda kullanılan dinamik olarak ekler. Merhaba katmana düzeninize uyacak değil, el ile tümleştirme hello web görünümleri yerine dikkate almalısınız.

.Xaml dosya değişikliği `EngagementPage` çok başvurusu`EngagementPageOverlay`

* Tooyour ad alanları bildirimleri ekleyin:
  
      xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"
* Değiştir `engagement:EngagementPage` ile `engagement:EngagementPageOverlay`:

**EngagementPage ile:**

        <engagement:EngagementPage 
            xmlns:engagement="using:Microsoft.Azure.Engagement">

            <!-- Your layout -->
        </engagement:EngagementPage>

**EngagementPageOverlay ile:**

        <engagement:EngagementPageOverlay 
            xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay">

            <!-- Your layout -->
        </engagement:EngagementPageOverlay>

Ardından .cs dosyanızda sayfanızda etiketi `EngagementPageOverlay` yerine `EngagementPage` ve içeri aktarma `Microsoft.Azure.Engagement.Overlay`.

            using Microsoft.Azure.Engagement.Overlay;

* Değiştir `EngagementPage` ile `EngagementPageOverlay`:

**EngagementPage ile:**

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPage
              {
                [...]
              }
            }

**EngagementPageOverlay ile:**

            using Microsoft.Azure.Engagement.Overlay;

            namespace Example
            {
              public sealed partial class ExamplePage : EngagementPageOverlay 
              {
                [...]
              }
            }


Merhaba katılım katmana ekler bir `Grid` öğesi, sayfanın en üstünde oluşur, Düzen ve hello iki `WebView` hello için öğeleri bir kapak sayfası ve hello Interstitial görünüm için başka bir hello.

Merhaba katmana öğelerinde doğrudan hello özelleştirebilirsiniz `EngagementPageOverlay.cs` dosya.

### <a name="web-views-manual-integration"></a>Web görünümleri el ile tümleştirme
Reach sayfalarınızın hello iki arama `WebView` öğeleri hello başlık ve hello Interstitial görünümü görüntülemek için sorumlu. yalnızca bir şey toodo sahip tooadd hello bu iki `WebView` öğeleri yere sayfalarınızda, örnek aşağıda verilmiştir:

    <Grid x:Name="engagementGrid">

      <!-- Your layout -->

      <WebView x:Name="engagement_notification_content" Visibility="Collapsed" Height="80" HorizontalAlignment="Stretch" VerticalAlignment="Top"/>
      <WebView x:Name="engagement_announcement_content" Visibility="Collapsed"  HorizontalAlignment="Stretch"  VerticalAlignment="Stretch"/>
    </Grid>


Bu örnek hello içinde `WebView` öğeler otomatik olarak onları ekran döndürme veya pencere boyutu değişikliği durumunda yeniden boyutlandırır kendi kapsayıcı esnetilen toofit olan.

> [!WARNING]
> Tookeep hello aynı adlandırma önemlidir `engagement_notification_content` ve `engagement_announcement_content` hello için `WebView` öğeleri. Reach bunları adına göre tanımlamak için kullanılır. 
> 
> 

## <a name="handle-datapush-optional"></a>Tanıtıcı datapush (isteğe bağlı)
Uygulama toobe mümkün tooreceive ulaşma veri gönderimleri isterseniz, iki olayları hello EngagementReach sınıfı tooimplement vardır:

App.xaml.cs hello App() oluşturucuda ekleyin:

            EngagementReach.Instance.DataPushStringReceived += (body) =>
            {
              Debug.WriteLine("String data push message received: " + body);
              return true;
            };

            EngagementReach.Instance.DataPushBase64Received += (decodedBody, encodedBody) =>
            {
              Debug.WriteLine("Base64 data push message received: " + encodedBody);
              // Do something useful with decodedBody like updating an image view
              return true;
            };

Her yöntem döndürür bir Boole değeri, bu hello geri çağırma görebilirsiniz. Katılım hello veri gönderimi gönderdikten sonra bir geri bildirim tooits arka uç gönderir. Merhaba geri çağırma false değeri döndürülürse, hello `exit` geri bildirim gönder olacaktır. Aksi durumda olur `action`. Geri arama yok hello olaylarını ayarlarsanız hello `drop` geri bildirim tooEngagement döndürülecek.

> [!WARNING]
> Katılım mümkün tooreceive katları geribildirimler veri gönderimi için değil. Bir olayda birçok işleyicileri tooset planlıyorsanız, hello geri bildirim sonuncu gönderilen toohello karşılık unutmayın. Bu durumda, tooalways öneririz hello kafa karıştırıcı geri bildirim hello ön uç sahip aynı değeri tooavoid döndürür.
> 
> 

## <a name="customize-ui-optional"></a>(İsteğe bağlı) kullanıcı arabirimini özelleştirme
### <a name="first-step"></a>İlk adım
Biz toocustomize hello ulaşma kullanıcı Arabirimi sağlar.

toodo bu nedenle, toocreate hello öğesinin bir alt kümesi olan `EngagementReachHandler` sınıfı.

**Örnek kod:**

            using Microsoft.Azure.Engagement;

            namespace Example
            {
              internal class ExampleReachHandler : EngagementReachHandler
              {
               // Override EngagementReachHandler methods depending on your needs
              }
            }

Sonra hello Merhaba içeriğine ayarlayın `EngagementReach.Instance.Handler` özel nesnesinde ile alan, `App.xaml.cs` hello sınıfında `App()` yöntemi.

**Örnek kod:**

            protected override void OnLaunched(LaunchActivatedEventArgs args)
            {
              // your app initialization 
              EngagementReach.Instance.Handler = new ExampleReachHandler();
              // Engagement Agent and Reach initialization
            }

> [!NOTE]
> Varsayılan olarak, kendi uyarlamasını katılım kullanır `EngagementReachHandler`.
> Toocreate yoksa, kendi ve bunu yaparsanız, her yöntemi toooverride yok. tooselect hello katılım temel nesne Hello varsayılan davranıştır.
> 
> 

### <a name="web-view"></a>Web görünümü
Varsayılan olarak, ulaşma hello DLL toodisplay hello bildirimleri ve sayfalarının katıştırılmış hello kaynakları kullanır.

tooprovide tam özelleştirme olanakları yalnızca kullanırız web görünümü. Doğrudan toocustomize düzenleri istiyorsanız hello kaynaklar dosyaları geçersiz kılma `EngagementAnnouncement.html` ve `EngagementNotification.html`. Katılım gereken tüm kodda `<body></body>` toorun doğru. Ancak, dış etiket ekleyebilirsiniz `engagement_webview_area`.

Ancak, kendi kaynaklarını toouse karar verebilirsiniz.

Geçersiz kılabilirsiniz `EngagementReachHandler` alt tootell katılım toouse yöntemleri, düzenler ancak dikkatli tooembedded hello katılım mekanizması alın:

**Örnek kod:**

            // In your subclass of EngagementReachHandler

            public override string GetAnnouncementHTML()
            {
              return base.GetAnnouncementHTML();
            }
            public override string GetAnnouncementName()
            {
              return base.GetAnnouncementName();
            }
            public override string GetNotfificationHTML()
            {
              return base.GetNotfificationHTML();
            }
            public override string GetNotfificationName()
            {
              return base.GetNotfificationName();
            }


Varsayılan olarak, AnnouncementHTML olan `ms-appx-web:///Resources/EngagementAnnouncement.html`. Anında iletme iletisi (metin Duyurusu, Web anoucement ve yoklama duyuru) Merhaba içeriğine tasarım hello html dosyası temsil eder. AnnouncementName olan `engagement_announcement_content`. Bunu hello hello webview xaml sayfası tasarımında adıdır.

NotfificationHTML olan `ms-appx-web:///Resources/EngagementNotification.html`. Anında iletme iletisi hello bildirim tasarım hello html dosyası temsil eder. NotfificationName olan `engagement_notification_content`. Bunu hello hello webview xaml sayfası tasarımında adıdır.

### <a name="customization"></a>Özelleştirme
Bildirim ve web görünümü, katılım nesne korumak istiyorsanız sahip duyuru özelleştirebilirsiniz. Dikkatli olun webview nesnesi üç kez açıklanan - Merhaba, xaml ilk kez ikinci hello "setwebview()" yönteminde .cs dosyanızdaki ve saat üçüncü hello html dosyasında zaman.

* Xaml içinde hello geçerli grafik düzenini webview bileşeni açıklanmaktadır.
* .Cs dosyanızda "Merhaba iki webview (bildirim, duyuru) hello boyutunu Ayarla setwebview()" tanımlayabilirsiniz. Merhaba uygulaması yeniden boyutlandırılırken çok etkili olur.
* Merhaba katılım html dosyasındaki hello webview içerik, tasarım açıklamakta ve birbirleri arasındaki öğeleri konum hello.

### <a name="launch-message"></a>İleti Başlatma
Bir kullanıcı bir sistem bildirimi (bildirim) tıkladığında, katılım Merhaba uygulaması başlatır, yük hello Merhaba içeriğine iletileri gönderme ve hello ilgili kampanya hello sayfayı görüntüleme.

Merhaba başlatma (bağlı olarak, ağ hızına hello) hello sayfasının hello uygulama ve hello görüntüsünün arasında bir gecikme yoktur.

bir şey yüklüyor tooindicate toohello kullanıcı, bir ilerleme çubuğu veya bir İlerleme göstergesi gibi görsel bir bilgi sağlamalıdır. Katılım kendisi, ancak sağladığı birkaç işleyicileri sizin için işleyemez.

"Genel App() {}" App.xaml.cs dosyasında tooimplement hello geri ekleyin:

            /* hello application has launched and hello content is loading.
             * You should display an indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageStarted += () => { [...] };

            /* hello application has finished loading hello content and hello page
             * is about toobe displayed.
             * You should hide hello indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageCompleted += () => { [...] };

            /* hello content has been loaded, but an error has occurred.
             * You can provide an information toohello user.
             * You should hide hello indicator here.
             */
            EngagementReach.Instance.RetrieveLaunchMessageFailed += () => { [...] };

Merhaba geri çağırma "Ortak App() {}" yönteminizi ayarlayabilirsiniz, `App.xaml.cs` dosya, tercihen hello önce `EngagementReach.Instance.Init()` çağırın.

> [!TIP]
> Her işleyici hello tarafından kullanıcı Arabirimi iş parçacığı denir. MessageBox veya bir şey UI ilgili kullanırken tooworry yok.
> 
> 

## <a id="push-channel-sharing"></a>Kanal paylaşımı gönderme
Ardından, uygulamanızda anında iletme bildirimleri başka bir amaç için kullanıyorsanız, hello Engagement SDK'sı özelliği paylaşımı toouse hello itme kanal sahip. Eksik tooavoid itme budur.

* Engagement Reach kendi itme kanal toohello başlatma sağlayabilir. Merhaba SDK yeni bir tane isteyen yerine kullanır.

Merhaba, anında iletme kanalda ile Merhaba Engagement Reach başlatma güncelleştirme `InitEngagement` hello yönteminden `App.xaml.cs` dosyası:

    /* Your own push channel logic... */
    var pushChannel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

    /*...Engagement initialization */
    EngagementAgent.Instance.Init(e);
    EngagementReach.Instance.Init(e,pushChannel);

* Alternatif olarak, yalnızca istiyorsanız tooconsume hello anında kanal hello ulaşma başlattıktan sonra hello SDK tarafından oluşturulduktan sonra bir geri çağırma Engagement Reach tooget hello itme kanalda ayarlayabilirsiniz.

Herhangi bir noktada, geri aramasını ayarlamasını **sonra** ulaşma başlatma hello:

    /* Set action on hello SDK push channel. */
    EngagementReach.Instance.SetActionOnPushChannel((PushNotificationChannel channel) => 
    {
      /* hello forwarded channel can be null if its creation fails for any reason. */
      if (channel != null)
      {
        /* Your own push channel logic... */
      });
    }

## <a name="custom-scheme-tip"></a>Özel şema İpucu
Özel şema kullanım sunuyoruz. Katılım uygulamanızda kullanılan katılım ön uç toobe öğesinden farklı türde bir URI gönderebilirsiniz. Varsayılan şema gibi `http, ftp, ...` olan yönetmek penceresi olacak Windows komut isteminde bir varsayılan uygulama cihazda yüklü olmaları durumunda. Ayrıca, uygulamanız için kendi özel şema oluşturabilirsiniz.

Merhaba basit yol tooset uygulamanızda özel bir düzeni olduğunu tooopen, `Package.appxmanifest` içinde gidin `Declarations` paneli. Seçin `Protocol` hello kullanılabilir bildirimleri Kaydırma kutusu ve ekleyin. Merhaba Düzenle `Name` yeni Protokolü alanıyla istenen adı.

Şimdi toouse bu protokolü düzenlemek, `App.xaml.cs` hello ile `OnActivated` yöntemi ve burada tooinitialize katılım de unutmayın:

            /// <summary>
            /// Enter point when app his called by another way than user click
            /// </summary>
            /// <param name="args">Activation args</param>
            protected override void OnActivated(IActivatedEventArgs args)
            {
              /* Init engagement like it was launch by a custom uri scheme */
              EngagementAgent.Instance.Init(args);
              EngagementReach.Instance.Init(args);

              //TODO design action toodo when app is launch

              #region Custom scheme use
              if (args.Kind == ActivationKind.Protocol)
              {
                ProtocolActivatedEventArgs myProtocol = (ProtocolActivatedEventArgs)args;

                if (myProtocol.Uri.Scheme.Equals("protocolName"))
                {
                  string path = myProtocol.Uri.AbsolutePath;
                }
              }
              #endregion

