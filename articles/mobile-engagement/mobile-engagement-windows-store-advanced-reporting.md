---
title: "aaaWindows Gelişmiş Evrensel raporlama MobileApps engagement"
description: "Nasıl Azure Mobile Engagement Windows Evrensel uygulamaları ile tooIntegrate"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ea5030bf-73ac-49b7-bc3e-c25fc10e945a
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-store
ms.devlang: dotnet
ms.topic: article
ms.date: 08/12/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: 20968f238ef7ae9dc0b8bb6dac3fb8bdb9bc3a10
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-reporting-with-hello-windows-universal-apps-engagement-sdk"></a>Merhaba Windows Evrensel uygulamaları Engagement SDK'sı ile Gelişmiş raporlama
> [!div class="op_single_selector"]
> * [Evrensel Windows](mobile-engagement-windows-store-advanced-reporting.md)
> * [Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md)
> * [iOS](mobile-engagement-ios-integrate-engagement.md)
> * [Android](mobile-engagement-android-advanced-reporting.md)
> 
> 

Bu konu Windows Evrensel uygulamanız ek raporlama senaryolarda açıklar. Bu senaryolar hello oluşturulan tooapply toohello uygulaması seçebileceği seçenekleriniz [Başlarken](mobile-engagement-windows-store-dotnet-get-started.md) Öğreticisi.

## <a name="prerequisites"></a>Ön koşullar
[!INCLUDE [Prereqs](../../includes/mobile-engagement-windows-store-prereqs.md)]

Bu öğreticiye başlamadan önce ilk hello tamamlamanız gereken [Başlarken](mobile-engagement-windows-store-dotnet-get-started.md) kasıtlı olarak doğrudan ve basit öğretici. Bu öğretici aralarından seçim yapabileceğiniz ek seçenekler ele alınmaktadır.

## <a name="specifying-engagement-configuration-at-runtime"></a>Çalışma zamanında katılım yapılandırmasını belirtme
Merhaba katılım yapılandırma hello Merkezi `Resources\EngagementConfiguration.xml` hello Burada belirtilmiş olan projenizin dosya [Başlarken](mobile-engagement-windows-store-dotnet-get-started.md) konu.

Ancak, ayrıca, çalışma zamanında belirtebilirsiniz: yöntemi hello katılım aracı başlatmadan önce aşağıdaki hello çağırabilirsiniz:

          /* Engagement configuration. */
          EngagementConfiguration engagementConfiguration = new EngagementConfiguration();

          /* Set hello Engagement connection string. */
          engagementConfiguration.Agent.ConnectionString = "Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}";

          /* Initialize Engagement angent with above configuration. */
          EngagementAgent.Instance.Init(e, engagementConfiguration);



## <a name="recommended-method-overload-your-page-classes"></a>Önerilen yöntem: aşırı yükleme, `Page` sınıfları
Katılım toocompute kullanıcıları, oturumlar, etkinlikleri, kilitlenme ve teknik istatistikleri, gerekli tüm hello günlüklerinin hello tooactivate raporlama tüm olun, `Page` alt sınıfları devral hello `EngagementPage` sınıfları.

Burada, uygulamanızın bir sayfa için bir örnek verilmiştir. Yapabileceğiniz Merhaba, uygulamanızın tüm sayfalar için aynı anlama.

### <a name="c-source-file"></a>C# kaynak dosyası
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
> Sayfanız hello kılıyorsa `OnNavigatedTo` yöntemi, emin toocall olması `base.OnNavigatedTo(e)`. Aksi takdirde hello etkinlik olması bildirilmedi (Merhaba `EngagementPage` çağrıları `StartActivity` içinde kendi `OnNavigatedTo` yöntemi).
> 
> 

### <a name="xaml-file"></a>XAML dosyası
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

### <a name="override-hello-default-behaviour"></a>Merhaba varsayılan davranışı geçersiz kılma
Varsayılan olarak, hiçbir ek ile Merhaba etkinlik adı olarak hello sınıf adı hello sayfasının bildirilir. Merhaba sınıfı hello "Sayfa" soneki kullanıyorsa, katılım kaldırır.

toooverride hello varsayılan davranışı hello adı için bu kodu ekleyin:

        // in hello .xaml.cs file
        protected override string GetEngagementPageName()
        {
          /* your code */
          return "new name";
        }

tooreport ek bilgilerle, etkinlik bu kodu ekleyin:

        // in hello .xaml.cs file
        protected override Dictionary<object,object> GetEngagementPageExtra()
        {
          /* your code */
          return extra;
        }

Bu yöntemler içinde hello denir `OnNavigatedTo` sayfanızın yöntemi.

### <a name="alternate-method-call-startactivity-manually"></a>Alternatif yöntem: çağrı `StartActivity()` el ile
Olamaz ya da toooverload istiyor musunuz, `Page` sınıfları, bunun yerine, çağırarak etkinliklerinizi başlatabilirsiniz `EngagementAgent` doğrudan yöntemleri.

Arama öneririz `StartActivity` içinde `OnNavigatedTo` sayfanızın yöntemi.

            protected override void OnNavigatedTo(NavigationEventArgs e)
            {
              base.OnNavigatedTo(e);
              EngagementAgent.Instance.StartActivity("MyPage");
            }

> [!IMPORTANT]
> Doğru oturumunuzu sonlandırmak emin olun.
> 
> Merhaba Windows Evrensel SDK otomatik olarak çağırır hello `EndActivity` hello uygulama kapatıldığında yöntemi. Bu nedenle, olan **yüksek oranda** toocall hello önerilen `StartActivity` hello kullanıcının hello etkinliği değiştirdiğinizde, yöntemi ve çok**hiçbir zaman** çağrısı hello `EndActivity` yöntemi. Bu yöntem hello geçerli kullanıcının tüm uygulama günlüklerini etkiler Merhaba uygulaması ayrıldı hello katılım sunucusuna bildirir.
> 
> 

## <a name="advanced-reporting"></a>Gelişmiş raporlama
İsteğe bağlı olarak, böylece tooreport uygulamaya özgü olaylar, hatalar ve işleri, toodo isteyebilirsiniz, kullanım hello diğer yöntemleri bulunanlar hello `EngagementAgent` sınıfı. Merhaba katılım API tüm Engagement'ın gelişmiş özelliklerini kullanılmasına izin verir.

Daha fazla bilgi için bkz: [nasıl toouse hello Mobile Engagement Windows Evrensel uygulamanız API etiketleme Gelişmiş](mobile-engagement-windows-store-use-engagement-api.md).

