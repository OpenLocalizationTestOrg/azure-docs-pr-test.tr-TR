---
title: "Android uygulamaları Azure Mobile Engagement ile aaaGet başlatıldı"
description: "Bilgi nasıl Android uygulamaları için analizler ve anında iletme bildirimleri ile Azure Mobile Engagement toouse."
services: mobile-engagement
documentationcenter: android
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3c286c6d-cfef-4e3e-9b2c-715429fe82db
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: Java
ms.topic: hero-article
ms.date: 08/10/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: e8c92607691104750cdf1c4f7639a041d8a7bcd5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-android-apps"></a>Android uygulamaları için Azure Mobile Engagement kullanmaya başlama
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Bu konu, nasıl gösterir toouse Azure Mobile Engagement toounderstand, uygulama kullanımınızı ve toosend bir Android uygulamasının bildirimleri toosegmented kullanıcılarına nasıl anında iletme.
Bu öğretici, Mobile Engagement kullanarak hello basit yayın senaryosunu gösterir. Öğreticide, temel bilgiler toplayan ve Google Cloud Messaging (GCM) kullanarak anında iletme bildirimleri alan, boş bir Android uygulaması oluşturursunuz.

## <a name="prerequisites"></a>Ön koşullar
Bu öğreticiyi tamamlamak gerektirir hello [Android Geliştirici Araçları](https://developer.android.com/sdk/index.html), hello Android Studio tümleşik geliştirme ortamını ve en son Android platformunu hello içerir.

Ayrıca hello gerektirir [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).

> [!IMPORTANT]
> toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-android-get-started).
>
>

## <a name="set-up-mobile-engagement-for-your-android-app"></a>Android uygulamanız için Mobile Engagement kurma
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a name="connect-your-app-toohello-mobile-engagement-backend"></a>Uygulamanızın toohello Mobile Engagement arka ucuna bağlanmak
Bu öğreticide "Merhaba en az gerekli toocollect veri kümesi ve bir anında iletme bildirimi gönderme bir"temel tümleştirme"gösterilmektedir. Android Studio toodemonstrate hello Tümleştirmesi ile temel bir uygulama oluşturun.

Merhaba tümleştirme belgelerinin tamamı hello bulunabilir [Mobile Engagement Android SDK tümleştirmesi](mobile-engagement-android-sdk-overview.md).

### <a name="create-an-android-project"></a>Android projesi oluşturma
1. Başlat **Android Studio**, hello açılır pencerede seçip **yeni bir Android Studio projesi Başlat**.

    ![][1]
2. Uygulama adı ve şirket etki alanı belirtin. Girdiğiniz bilgileri daha sonra kullanmanız gerekeceğinden bunları not edin. **İleri**’ye tıklayın.

    ![][2]
3. Merhaba hedef form faktörünü ve API düzeyini seçin ve tıklayın **sonraki**.

   > [!NOTE]
   > Mobile Engagement, en az API düzey 10 (Android 2.3.3) gerektirir.
   >
   >

    ![][3]
4. Seçin **boş etkinlik** hello yalnızca ekran bu uygulama ve tıklatın burada **sonraki**.

    ![][4]
5. Son olarak, olan ve'ı tıklatın hello Varsayılanları bırakabilir **son**.

    ![][5]

Android Studio şimdi içine biz Mobile Engagement tümleştirmek hello tanıtım uygulamasını oluşturur.

### <a name="include-hello-sdk-library-in-your-project"></a>Merhaba SDK kitaplığını projenize ekleme
1. Merhaba karşıdan [Mobile Engagement Android SDK](https://aka.ms/vq9mfn).
2. Bilgisayarınızdaki Hello arşiv dosyasını tooa klasöre ayıklayın.
3. Bu SDK'ın geçerli sürümü hello Hello .jar kitaplığını belirleyin ve toohello panoya kopyalayın.

      ![][6]
4. Toohello gidin **proje** bölümünde (1) ve hello .jar (2) hello libs klasörüne yapıştırın.

      ![][7]
5. tooload hello kitaplığı, Merhaba projeyi Eşitle.

      ![][8]

### <a name="connect-your-app-toomobile-engagement-backend-with-hello-connection-string"></a>Bağlantı dizesi hello ile uygulamanızın tooMobile Engagement arka ucuna bağlanmak
1. (Yalnızca tek bir yerde genellikle hello Ana faaliyet, uygulamanızın yapılmalıdır) hello etkinlik oluşturma içine kod satırı aşağıdaki hello kopyalayın. Bu örnek uygulama için src altında MainActivity hello açın main -> java klasörü ve hello aşağıdakileri ekleyin:

        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.setConnectionString("Endpoint={appCollection}.{domain};AppId={appId};SdkKey={sdkKey}");
        EngagementAgent.getInstance(this).init(engagementConfiguration);
2. Alt + Enter tuşuna basarak veya içeri aktarma deyimlerini aşağıdaki hello ekleyerek Hello başvuruları çözümlenemedi:

        import com.microsoft.azure.engagement.EngagementAgent;
        import com.microsoft.azure.engagement.EngagementConfiguration;
3. Toohello Azure Klasik Portalı'nda, uygulamanızın dön **bağlantı bilgisi** sayfası ve kopyalama hello **bağlantı dizesi**.

      ![][9]
4. Merhaba yapıştırma `setConnectionString` hello tüm dizeyi koddan hello gösterilen değiştirme parametresi:

        engagementConfiguration.setConnectionString("Endpoint=my-company-name.device.mobileengagement.windows.net;SdkKey=********************;AppId=*********");

### <a name="add-permissions-and-a-service-declaration"></a>İzinler ve bir hizmet bildirimi ekleme
1. Bu izinleri toohello projenizin manifest.xml dosyasında hemen önce veya sonra hello eklemek `<application>` etiketi:

        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
2. toodeclare Merhaba Aracısı hizmeti, bu kod hello arasında eklemek `<application>` ve `</application>` etiketler:

        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
3. Yapıştırdığınız hello kodla `"<Your application name>"` hello etiketinde görüntülendiği hello **ayarları** burada görebilirsiniz hello cihazda çalışan hizmetleri menüsü. Örneğin bu etikete "Hizmet" Merhaba sözcüğünü ekleyebilirsiniz.

### <a name="send-a-screen-toomobile-engagement"></a>Ekran tooMobile katılım Gönder
verileri gönderme toostart ve olun hello kullanıcıların etkin olduğundan, en az bir ekran (etkinlik) toohello Mobile Engagement arka göndermeniz gerekir.

Çok Git**MainActivity.java** ve tooreplace hello temel sınıfını aşağıdaki hello ekleyin **MainActivity** çok**EngagementActivity**:

    public class MainActivity extends EngagementActivity {

> [!NOTE]
> Temel sınıfınız değilse *etkinlik*, başvurun [Gelişmiş Android raporlama](mobile-engagement-android-advanced-reporting.md) nasıl tooinherit farklı sınıflardan.
>
>

Bu basit Örnek senaryo için satır aşağıdaki hello çıkışı Açıklama:

    // setSupportActionBar(toolbar);

Tookeep hello istiyorsanız `ActionBar` , uygulamanızda bkz [Gelişmiş Android raporlama](mobile-engagement-android-advanced-reporting.md).

## <a name="connect-app-with-real-time-monitoring"></a>Uygulamayı gerçek zamanlı izlemeyle bağlama
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a name="enable-push-notifications-and-in-app-messaging"></a>Anında iletme bildirimlerini ve uygulama içi mesajlaşmayı etkinleştirme
Mobile Engagement, bir kampanya sırasında anında iletme bildirimleri ve uygulama içi mesajlaşma ile kullanıcılarınızla etkileşim kurmanızı ve REACH ile kullanıcılarınıza ulaşmanızı sağlar. Bu modül hello Mobile Engagement portalında REACH adı verilir.
bölümden Merhaba, uygulama tooreceive bunları ayarlar.

### <a name="copy-sdk-resources-in-your-project"></a>SDK kaynaklarını projenize kopyalama
1. İçerik ve kopyalama geri tooyour SDK yükleme hello gidin **res** klasör.

    ![][10]
2. TooAndroid Studio, select hello dön **ana** proje dosyalarınıza dizin ve tooadd hello kaynakları tooyour proje yapıştırın.

    ![][11]

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

## <a name="next-steps"></a>Sonraki adımlar
Çok Git[Android SDK](mobile-engagement-android-sdk-overview.md) tooget ayrıntılı hello SDK tümleştirmesi hakkında bilgi.

<!-- Images. -->
[1]: ./media/mobile-engagement-android-get-started/android-studio-new-project.png
[2]: ./media/mobile-engagement-android-get-started/android-studio-project-props.png
[3]: ./media/mobile-engagement-android-get-started/android-studio-project-props2.png
[4]: ./media/mobile-engagement-android-get-started/android-studio-add-activity.png
[5]: ./media/mobile-engagement-android-get-started/android-studio-activity-name.png
[6]: ./media/mobile-engagement-android-get-started/sdk-content.png
[7]: ./media/mobile-engagement-android-get-started/paste-jar.png
[8]: ./media/mobile-engagement-android-get-started/sync-project.png
[9]: ./media/mobile-engagement-android-get-started/app-connection-info-page.png
[10]: ./media/mobile-engagement-android-get-started/copy-resources.png
[11]: ./media/mobile-engagement-android-get-started/paste-resources.png
