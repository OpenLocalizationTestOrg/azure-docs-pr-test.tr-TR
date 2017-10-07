---
title: "Windows Evrensel uygulamaları Azure Mobile Engagement ile aaaGet başlatıldı"
description: "Bilgi nasıl toouse Azure Mobile Engagement Windows Evrensel uygulamaları için analizler ve anında iletme bildirimleri ile."
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: 48103867-7f64-4646-b019-42bd797d38e2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 8224a6d3789cfe4784bbc9472005f9eddb94a8b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-universal-apps"></a>Windows Evrensel Uygulamaları için Azure Mobile Engagement kullanmaya başlama
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Bu konu, nasıl gösterir toouse Azure Mobile Engagement toounderstand uygulama kullanımı ve gönderme anında iletme bildirimleri toosegmented kullanıcılar Windows Evrensel uygulamasının.
Bu öğretici, Mobile Engagement kullanarak hello basit yayın senaryosunu gösterir. Temel uygulama kullanımı verilerini toplayan ve Windows Bildirim Hizmeti’ni (WNS) kullanarak anında iletme bildirimleri alan boş bir Windows Evrensel Uygulaması oluşturursunuz.

> [!NOTE]
> Hello Azure Mobile Engagement hizmet Mart 2018 kullanımdan kaldırılır ve şu anda yalnızca kullanılabilir tooexisting müşterileri içindir. Daha fazla bilgi için bkz. [Mobile Engagement nedir?](https://azure.microsoft.com/en-us/services/mobile-engagement/).

## <a name="prerequisites"></a>Ön koşullar
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

## <a name="set-up-mobile-engagement-for-your-windows-universal-app"></a>Windows Evrensel uygulamanız için Mobile Engagement kurma
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Uygulamanızın toohello Mobile Engagement arka ucuna bağlanmak
Bu öğretici "Merhaba en az gerekli toocollect veri kümesi ve bir anında iletme bildirimi gönderme bir temel tümleştirme" gösterilmektedir. Merhaba tümleştirme belgelerinin tamamı hello bulunabilir [Mobile Engagement Windows Evrensel SDK tümleştirmesi](mobile-engagement-windows-store-sdk-overview.md).

Visual Studio toodemonstrate hello Tümleştirmesi ile temel bir uygulama oluşturun.

### <a name="create-a-windows-universal-app-project"></a>Bir Windows Evrensel Uygulaması projesi oluşturma
Visual Studio'nun önceki sürümleri başlangıç adımları benzerdir olsa hello aşağıdaki adımlarda Visual Studio 2015 hello kullanımını varsayılmaktadır.

1. Visual Studio'yu başlatın ve hello **giriş** ekran, select **yeni proje**.
2. Merhaba açılır pencerede seçin **Windows** -> **Evrensel** -> **boş uygulama (Evrensel Windows)**. Merhaba doldurup **adı** ve **çözüm adı**ve ardından **Tamam**.

    ![][1]

Bir Windows Evrensel uygulama projesi sonraki hello Azure Mobile Engagement SDK'sını tümleştirmek oluşturdunuz.

### <a name="connect-your-app-toomobile-engagement-backend"></a>Uygulamanızın tooMobile Engagement arka ucuna bağlanmak
1. Merhaba yüklemek [MicrosoftAzure.MobileEngagement] Nuget paketini projenize. Windows ve Windows Phone platformlarının hedefliyorsanız, toodo bu iki projeleri için gerekir. Windows 8.x ve Windows Phone 8.1, hello aynı Nuget paketi yerler hello doğru platforma özgü ikili dosyalarını her projede.
2. Açık **Package.appxmanifest** ve yetenek aşağıdaki o hello var. eklendiğinden emin olun:

        Internet (Client)

    ![][2]
3. Şimdi daha önce Mobile Engagement uygulamanız için kopyaladığınız hello bağlantı dizesini kopyalayın ve hello Yapıştır `Resources\EngagementConfiguration.xml` hello arasında dosya `<connectionString>` ve `</connectionString>` etiketler:

    ![][3]

    > [!TIP]
    > Uygulamanız, Windows ve Windows Phone platformlarının ikisini de hedefliyorsa, desteklenen her platform için birer adet olmak üzere iki adet Mobile Engagement Uygulaması oluşturmanız gerekir. İki uygulama sahip hello hedef kitleyi segmentlere doğru oluşturabilirsiniz ve her platform için uygun şekilde hedefe yönelik bildirimler gönderebilirsiniz sağlar.

    > [!IMPORTANT]
    > NuGet Windows 10 UWP uygulamanızda hello SDK kaynakları otomatik olarak kopyalamaz. Bunu el ile Merhaba Nuget paketi yüklendiğinde (readme.txt) göster hello adımları izleyerek toodo sahip.  

1. Merhaba, `App.xaml.cs` dosyası:

    a. Merhaba eklemek `using` deyimi:

            using Microsoft.Azure.Engagement;

    b. Merhaba katılım başlatan bir yöntemi ekleyin:

           private void InitEngagement(IActivatedEventArgs e)
           {
             EngagementAgent.Instance.Init(e);

             //... rest of hello code
           }

    c. Merhaba Hello SDK başlatma **OnLaunched** yöntemi:

            protected override void OnLaunched(LaunchActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

    c. Merhaba aşağıdaki hello Ekle **OnActivated** yöntemi ve zaten mevcut değilse hello yöntemi ekleyin:

            protected override void OnActivated(IActivatedEventArgs e)
            {
              InitEngagement(e);

              //... rest of hello code
            }

## <a id="monitor"></a>Gerçek zamanlı izlemeyi etkinleştirme
verileri gönderilirken toostart ve hello kullanıcıların etkin olduğundan emin olmak, en az bir ekran (etkinlik) toohello Mobile Engagement arka göndermeniz gerekir.

1. Merhaba, **MainPage.xaml.cs**, hello aşağıdakileri ekleyin `using` deyimi:

    Microsoft.Azure.Engagement.Overlay’i kullanarak
2. Değiştirme hello temel sınıfını **MainPage** gelen **sayfa** çok**EngagementPageOverlay**:

        class MainPage : EngagementPageOverlay
3. Merhaba, `MainPage.xaml` dosyası:

    a. Tooyour ad alanları bildirimleri ekleyin:

        xmlns:engagement="using:Microsoft.Azure.Engagement.Overlay"

    b. Hello yerine **sayfa** hello XML etiket adı ile **engagement: EngagementPageOverlay**

> [!IMPORTANT]
> Sayfanız hello kılıyorsa `OnNavigatedTo` yöntemi, emin toocall olması `base.OnNavigatedTo(e)`. Aksi takdirde hello etkinlik bildirilmedi `EngagementPage` çağrıları `StartActivity` içinde kendi `OnNavigatedTo` yöntemi). Bu hello varsayılan şablonu sahip olduğu bir Windows Phone projesinde özellikle önemlidir bir `OnNavigatedTo` yöntemi.
>
> İçin **Windows 10 Universal uygulamalarının**, hello önerilen hello yöntemi kullanın "yöntemi önerilir: sayfa sınıflarınızı aşırı yükleme" kısmında [Gelişmiş raporlama hello Windows Evrensel uygulamaları Engagement SDK'sı ile](mobile-engagement-windows-store-advanced-reporting.md) , hello yerine bir bahsedilen üstünde.

## <a id="monitor"></a>Uygulamayı gerçek zamanlı izlemeyle bağlama
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Anında iletme bildirimlerini ve uygulama içi mesajlaşmayı etkinleştirme
Mobile Engagement toointeract sağlar ve kullanıcılarınızın anında iletme bildirimleri ve uygulama içi Mesajlaşma hello Kampanyalar bağlamında ulaşılırsa. Bu modül hello Mobile Engagement portalında REACH adı verilir.
Merhaba aşağıdaki bölümlerde, app tooreceive bunları ayarlayın.

### <a name="enable-your-app-tooreceive-wns-push-notifications"></a>Uygulama tooreceive WNS anında iletme bildirimlerini etkinleştirme
1. Merhaba, `Package.appxmanifest` dosyasında hello **uygulama** sekmesinde, altında **bildirimleri**ayarlayın **bildirim özellikli:** çok**Evet**

    ![][5]

### <a name="initialize-hello-reach-sdk"></a>Merhaba REACH SDK'yı başlatma
İçinde `App.xaml.cs`, çağrı **Initengagement** hello içinde **engagementreach.Instance.Init(e);** işlevi hello aracı başlatmadan hemen sonra:

        private void InitEngagement(IActivatedEventArgs e)
        {
           EngagementAgent.Instance.Init(e);
           EngagementReach.Instance.Init(e);
        }

Hazır toosend bir bildirim demektir. Şimdi bu temel tümleştirmeyi doğru bir şekilde gerçekleştirdiğinizi doğrulayacağız.

### <a name="grant-access-toomobile-engagement-toosend-notifications"></a>GRANT erişim tooMobile katılım toosend bildirimleri
1. Web tarayıcınızda [Windows Mağazası Geliştirme Merkezi]’ni açın, oturum açın ve gerekiyorsa bir hesap oluşturun.
2. Tıklatın **Pano** hello sağ üst köşe ve ardından **yeni uygulama oluştur** hello sol panel menüsünde.

    ![][9]
3. Adını ayırarak uygulamanızı oluşturun.

    ![][10]
4. Merhaba uygulama oluşturulduktan sonra çok gidin**Hizmetleri -> anında iletme bildirimleri** hello sol menüden.

    ![][11]
5. Bildirimler bölümü Hello itme, hello tıklatın **Live Services sitesi** bağlantı.

    ![][12]
6. Toohello gönderim kimlik bilgileri bölümüne gidin. Hello olduğundan emin olun **uygulama ayarları** bölümünde ve ardından kopyalama, **paket SID'si** ve **istemci parolası**

    ![][13]
7. Toohello gidin **ayarları** , Mobile Engagement portalının hello tıklatıp **yerel gönderim** hello soldaki bölüm. Merhaba ardından **Düzenle** düğmesini tooenter, **paket güvenlik tanımlayıcısı (SID)** ve **gizli anahtar** gösterildiği gibi:

    ![][6]
8. Son olarak, Visual Studio uygulamanızı hello uygulama Mağazası'nda oluşturulan bu uygulama ile ilişkilendirdiğinizden emin olun. Visual Studio’da **Uygulamayı Mağaza ile İlişkilendir**’e tıklayın.

    ![][7]

## <a id="send"></a>Bir bildirim tooyour uygulaması Gönder
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

Merhaba uygulama çalışıyorsa, bir uygulama içi bildirim görürsünüz. Aksi takdirde Hello uygulama kapalıysa, bir bildirim görürsünüz.
Bir uygulama bildirimi ancak bildirim bakın ve Visual Studio'da hata ayıklama modunda hello uygulama çalıştırıyorsanız, daha sonra deneyin **yaşam döngüsü olayları -> Askıya Al** hello araç tooensure bu hello uygulama askıya alınır. Merhaba uygulaması Visual Studio'da hata ayıklarken hello giriş düğmesine tıkladıysanız, ardından bu her zaman askıya alınmaz ve uygulama hello bildirim bakın, ancak bunu bir bildirim gösterilmesini.  

![][8]

<!-- URLs. -->
[Mobile Engagement Windows Universal SDK documentation]: ../mobile-engagement-windows-store-integrate-engagement/
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9864592
[Windows Mağazası Geliştirme Merkezi]: https://dev.windows.com
[Windows Universal Apps - Overlay integration]: ../mobile-engagement-windows-store-integrate-engagement-reach/#overlay-integration

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-store-dotnet-get-started/universal-app-creation.png
[2]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-capabilities.png
[3]: ./media/mobile-engagement-windows-store-dotnet-get-started/add-connection-info.png
[5]: ./media/mobile-engagement-windows-store-dotnet-get-started/manifest-toast.png
[6]: ./media/mobile-engagement-windows-store-dotnet-get-started/enter-credentials.png
[7]: ./media/mobile-engagement-windows-store-dotnet-get-started/associate-app-store.png
[8]: ./media/mobile-engagement-windows-store-dotnet-get-started/vs-suspend.png
[9]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_create_app.png
[10]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_app_name.png
[11]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push.png
[12]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_1.png
[13]: ./media/mobile-engagement-windows-store-dotnet-get-started/dashboard_services_push_creds.png
