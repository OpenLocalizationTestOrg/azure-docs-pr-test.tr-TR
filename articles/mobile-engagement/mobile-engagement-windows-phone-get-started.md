---
title: "Windows Phone Silverlight için Azure Mobile Engagement uygulamalarla aaaGet başlatıldı"
description: "Bilgi nasıl Windows Phone Silverlight uygulamaları için analizler ve anında iletme bildirimleri ile Azure Mobile Engagement toouse."
services: mobile-engagement
documentationcenter: windows
author: piyushjo
manager: erikre
editor: 
ms.assetid: aa34692f-87f7-47c6-a20c-a1972750bc25
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b39a838ab03217b2dc845cbf59d7bf8b094dac1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-windows-phone-silverlight-apps"></a>Windows Phone Silverlight uygulamaları için Azure Mobile Engagement kullanmaya başlama
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Bu konu, nasıl gösterir toouse Azure Mobile Engagement toounderstand uygulama kullanımı ve gönderme anında iletme bildirimleri toosegmented kullanıcılar Windows Phone Silverlight uygulaması.
Bu öğretici, Mobile Engagement kullanarak hello basit yayın senaryosunu gösterir. Temel verileri toplayan ve Microsoft Anında İletme Bildirimi Hizmeti’ni (MPNS) kullanarak anında iletme bildirimleri alan boş bir Windows Phone Silverlight uygulaması oluşturursunuz.

> [!NOTE]
> Hello Azure Mobile Engagement hizmet Mart 2018 kullanımdan kaldırılır ve şu anda yalnızca kullanılabilir tooexisting müşterileri içindir. Daha fazla bilgi için bkz. [Mobile Engagement nedir?](https://azure.microsoft.com/en-us/services/mobile-engagement/).

> [!NOTE]
> Windows Phone 8.1 ve önceki sürümlerde oluşturulmuş projeler Visual Studio 2017’de desteklenmez.  Daha fazla bilgi için bkz. [Visual Studio 2017 Platform Desteği ve Uyumluluk](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).

> [!NOTE]
> Windows Phone 8.1 (Silverlight olmayan) hedefliyorsanız, toohello başvuran [Windows Evrensel Öğreticisine](mobile-engagement-windows-store-dotnet-get-started.md).
> 
> 

Bu öğretici hello aşağıdakileri gerektirir:

* Visual Studio 2013
* [MicrosoftAzure.MobileEngagement] Nuget paketi

> [!NOTE]
> toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-windows-phone-get-started).
> 
> 

## <a id="setup-azme"></a>Windows Phone uygulamanıza Mobile Engagement’i kurma
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Uygulamanızın toohello Mobile Engagement arka ucuna bağlanmak
Bu öğreticide "Merhaba en az gerekli toocollect veri kümesi ve bir anında iletme bildirimi gönderme bir"temel tümleştirme"gösterilmektedir. Merhaba tümleştirme belgelerinin tamamı hello bulunabilir [Mobile Engagement Windows Phone SDK tümleştirmesi](mobile-engagement-windows-phone-sdk-overview.md)

Visual Studio toodemonstrate hello Tümleştirmesi ile temel bir uygulama oluşturacağız.

### <a name="create-a-new-windows-phone-silverlight-project"></a>Yeni bir Windows Phone Silverlight projesi oluşturma
Visual Studio'nun önceki sürümleri başlangıç adımları benzerdir olsa hello aşağıdaki adımlarda Visual Studio 2015 hello kullanımını varsayılmaktadır. 

1. Visual Studio'yu başlatın ve hello **giriş** ekran, select **yeni proje**.
2. Merhaba açılır pencerede seçin **Windows 8** -> **Windows Phone** -> **boş uygulama (Windows Phone Silverlight)**. Merhaba doldurup **adı** ve **çözüm adı**ve ardından **Tamam**.
   
    ![][1]
3. Tootarget ya da seçebilirsiniz **Windows Phone 8.0** veya **Windows Phone 8.1**.

İçine biz hello Azure Mobile Engagement SDK'sı tümleştirecek yeni bir Windows Phone Silverlight uygulaması oluşturdunuz.

### <a name="connect-your-app-toohello-mobile-engagement-backend"></a>Uygulamanızın toohello Mobile Engagement arka ucuna bağlanmak
1. Merhaba yüklemek [MicrosoftAzure.MobileEngagement] nuget paketini projenize.
2. Açık `WMAppManifest.xml` (Merhaba özellikler klasörünün altında) ve hello aşağıdakilerin bildirildiğinden emin olun (bunları değillerse ekleyin) hello içinde `<Capabilities />` etiketi:
   
        <Capability Name="ID_CAP_NETWORKING" />
        <Capability Name="ID_CAP_IDENTITY_DEVICE" />
   
    ![][2]
3. Şimdi daha önce Mobile Engagement uygulamanız için kopyaladığınız hello bağlantı dizesini yapıştırın ve hello Yapıştır `Resources\EngagementConfiguration.xml` hello arasında dosya `<connectionString>` ve `</connectionString>` etiketler:
   
    ![][3]
4. Merhaba, `App.xaml.cs` dosyası:
   
    a. Merhaba eklemek `using` deyimi:
   
            using Microsoft.Azure.Engagement;
   
    b. Merhaba Hello SDK başlatma `Application_Launching` yöntemi:
   
            private void Application_Launching(object sender, LaunchingEventArgs e)
            {
              EngagementAgent.Instance.Init();
            }
   
    c. Merhaba aşağıdaki hello Ekle `Application_Activated`:
   
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
               EngagementAgent.Instance.OnActivated(e);
            }

## <a id="monitor"></a>Gerçek zamanlı izlemeyi etkinleştirme
Verileri gönderme ve hello kullanıcıların etkin olduğundan emin olmak sipariş toostart içinde en az bir ekran (etkinlik) toohello Mobile Engagement arka göndermeniz gerekir.

1. Hello MainPage.xaml.cs, hello eklemek `using` deyimi:
   
        using Microsoft.Azure.Engagement;
2. Merhaba temel sınıfını değiştirme **MainPage**, önce olduğu **mainpage**, ile **EngagementPage**.
   
        class MainPage : EngagementPage 
3. `MainPage.xml` dosyanızda:
   
    a. Tooyour ad alanları bildirimleri ekleyin:
   
            xmlns:engagement="clr-namespace:Microsoft.Azure.Engagement;assembly=Microsoft.Azure.Engagement.EngagementAgent.WP"
   
    b. Değiştir `phone:PhoneApplicationPage` hello XML etiket adı ile `engagement:EngagementPage`.

## <a id="monitor"></a>Uygulamayı gerçek zamanlı izlemeyle bağlama
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Anında iletme bildirimlerini ve uygulama içi mesajlaşmayı etkinleştirme
Mobile Engagement toointeract sağlar ve anında iletme bildirimleri ve uygulama içi Mesajlaşma Kampanyalar hello bağlamda Kullanıcılarınızla ulaşılırsa. Bu modül hello Mobile Engagement portalında REACH adı verilir.
Merhaba aşağıdaki bölümlerde, app tooreceive bunları ayarlayın.

### <a name="enable-your-app-tooreceive-mpns-push-notifications"></a>Uygulama tooreceive MPNS anında iletme bildirimlerini etkinleştirme
Yeni özellikleri tooyour ekleme `WMAppManifest.xml` dosyası:

        ID_CAP_PUSH_NOTIFICATION
        ID_CAP_WEBBROWSERCOMPONENT

   ![][5]

### <a name="initialize-hello-reach-sdk"></a>Merhaba REACH SDK'yı başlatma
1. İçinde `App.xaml.cs`, çağrı `EngagementReach.Instance.Init();` hello içinde **Application_Launching** hello aracı başlatmadan hemen sonra işlevi:
   
        private void Application_Launching(object sender, LaunchingEventArgs e)
        {
           EngagementAgent.Instance.Init();
           EngagementReach.Instance.Init();
        }
2. İçinde `App.xaml.cs`, çağrı `EngagementReach.Instance.OnActivated(e);` hello içinde **Application_Activated** hello aracı başlatmadan hemen sonra işlevi:
   
        private void Application_Activated(object sender, ActivatedEventArgs e)
        {
           EngagementAgent.Instance.OnActivated(e);
           EngagementReach.Instance.OnActivated(e);
        }

İşinizi tamamlandı. Şimdi bu temel tümleştirmeyi doğru bir şekilde gerçekleştirdiğinizi onaylayacağız.

## <a id="send"></a>Bir bildirim tooyour uygulaması Gönder
[!INCLUDE [Create Windows Push campaign](../../includes/mobile-engagement-windows-push-campaign.md)]

Hello uygulama, aksi takdirde bildirim hello aşağıdaki gibi açıksa şimdi bir bildirim gösterilir, Cihazınızda bir uygulama içi bildirim olarak görmeniz gerekir: 

![][6]

<!-- URLs. -->
[MicrosoftAzure.MobileEngagement]: http://go.microsoft.com/?linkid=9874664
[Mobile Engagement Windows Phone SDK documentation]: ../mobile-engagement-windows-phone-integrate-engagement/

<!-- Images. -->
[1]: ./media/mobile-engagement-windows-phone-get-started/project-properties.png
[2]: ./media/mobile-engagement-windows-phone-get-started/wmappmanifest-capabilities.png
[3]: ./media/mobile-engagement-windows-phone-get-started/add-connection-string.png
[5]: ./media/mobile-engagement-windows-phone-get-started/reach-capabilities.png
[6]: ./media/mobile-engagement-windows-phone-get-started/push-screenshot.png
