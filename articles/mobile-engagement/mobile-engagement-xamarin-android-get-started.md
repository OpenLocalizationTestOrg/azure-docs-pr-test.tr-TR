---
title: "aaaGet Xamarin.Android için Azure Mobile Engagement ile başlatıldı"
description: "Bilgi nasıl toouse analizi ve Xamarin.Android uygulamaları için anında iletme bildirimleri ile Azure Mobile Engagement."
services: mobile-engagement
documentationcenter: xamarin
author: piyushjo
manager: erikre
editor: 
ms.assetid: fb68cf98-08a2-41b5-8e59-757469de3fe7
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-android
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/16/2016
ms.author: piyushjo
ms.openlocfilehash: 9d584fea8e8153d511258cf9b6f87f31dac6aeca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-xamarinandroid-apps"></a>Xamarin.Android Uygulamaları için Azure Mobile Engagement kullanmaya başlama
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Bu konu, nasıl gösterir toouse Azure Mobile Engagement toounderstand, uygulama kullanımınızı ve toosend bir Xamarin.Android uygulamasının bildirimleri toosegmented kullanıcılarına nasıl anında iletme.
Bu öğretici, Mobile Engagement kullanarak hello basit yayın senaryosunu gösterir. Öğreticide, temel bilgiler toplayan ve Google Cloud Messaging (GCM) kullanarak anında iletme bildirimleri gönderen, boş bir Xamarin.Android uygulaması oluşturursunuz.

> [!NOTE]
> Hello Azure Mobile Engagement hizmet Mart 2018 kullanımdan kaldırılır ve şu anda yalnızca kullanılabilir tooexisting müşterileri içindir. Daha fazla bilgi için bkz. [Mobile Engagement nedir?](https://azure.microsoft.com/en-us/services/mobile-engagement/).

Bu öğretici hello aşağıdakileri gerektirir:

* [Xamarin Studio](http://xamarin.com/studio). Xamarin ile Visual Studio’yu da kullanabilirsiniz, ancak bu öğretici Xamarin Studio'yu kullanır. Yükleme yönergeleri için bkz. [Visual Studio ve Xamarin için Kurulum ve Yükleme](https://msdn.microsoft.com/library/mt613162.aspx).
* [Mobile Engagement Xamarin SDK](https://www.nuget.org/packages/Microsoft.Azure.Engagement.Xamarin/)

> [!NOTE]
> toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-xamarin-android-get-started).
> 
> 

## <a id="setup-azme"></a>Android uygulamanız için Mobile Engagement kurma
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Uygulamanızın toohello Mobile Engagement arka ucuna bağlanmak
Bu öğreticide "Merhaba en az gerekli toocollect veri kümesi ve bir anında iletme bildirimi gönderme bir"temel tümleştirme"gösterilmektedir. 

Xamarin Studio toodemonstrate hello Tümleştirmesi ile temel bir uygulama oluşturacağız.

### <a name="create-a-new-xamarinandroid-project"></a>Yeni bir Xamarin.Android projesi oluşturma
1. Başlatma **Xamarin Studio** çok Git**dosya** -> **yeni** -> **çözümü** 
   
    ![][1]
2. Seçin **Android uygulaması** seçili hello dilin olduğundan emin olun **C#** tıklatıp **sonraki**.
   
    ![][2]
3. Hello dolgu **App Name** ve hello **kuruluş tanımlayıcı**. Emin toocheckmark olun **Google Play Hizmetleri** ve ardından **sonraki**. 
   
    ![][3]
4. Güncelleştirme hello **proje adı**, **çözüm adı** ve **konumu** gerekli ve tıklatırsanız **oluşturma**.
   
    ![][4]

Xamarin Studio biz Mobile Engagement tümleştirecek hello uygulaması oluşturacaksınız. 

### <a name="connect-your-app-toomobile-engagement-backend"></a>Uygulamanızın tooMobile Engagement arka ucuna bağlanmak
1. Merhaba sağ tıklayın **paketleri** seçip hello çözüm windows klasörü **paketleri Ekle...**
   
    ![][5]
2. Merhaba Ara **Microsoft Azure Mobile Engagement Xamarin SDK** ve tooyour çözüme ekleyin.  
   
    ![][6]
3. Açık **MainActivity.cs** ve hello aşağıdaki using deyimlerini:
   
        using Microsoft.Azure.Engagement;
        using Microsoft.Azure.Engagement.Activity;
4. Merhaba, `OnCreate` yöntemi, Mobile Engagement arka ucuyla tooinitialize hello bağlantıyı izleyerek hello ekleyin. Tooadd emin olun, **ConnectionString**. 
   
        EngagementConfiguration engagementConfiguration = new EngagementConfiguration();
        engagementConfiguration.ConnectionString = "YourConnectionStringFromAzurePortal";
        EngagementAgent.Init(engagementConfiguration);

### <a name="add-permissions-and-a-service-declaration"></a>İzinler ve bir hizmet bildirimi ekleme
1. Merhaba açın **Manifest.xml** dosya hello özellikleri klasörü altında. Kaynak sekmesini seçin, böylece hello XML kaynağını doğrudan güncelleştirin.
2. Bu izinleri toohello Manifest.xml ekleyin (Merhaba altında bulunabilir **özellikleri** klasörü) projenizin hemen önce veya sonra hello `<application>` etiketi:
   
        <uses-permission android:name="android.permission.INTERNET"/>
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION"/>
3. Merhaba arasında Hello aşağıdakileri ekleyin `<application>` ve `</application>` toodeclare hello Aracısı hizmeti etiketler:
   
        <service
             android:name="com.microsoft.azure.engagement.service.EngagementService"
             android:exported="false"
             android:label="<Your application name>"
             android:process=":Engagement"/>
4. Yapıştırdığınız hello kodla `"<Your application name>"` hello etiketi. Bu hello görüntülenir **ayarları** burada kullanıcılar görebilir hello cihazda çalışan hizmetleri menüsü. Örneğin bu etikete "Hizmet" Merhaba sözcüğünü ekleyebilirsiniz.

### <a name="send-a-screen-toomobile-engagement"></a>Ekran tooMobile katılım Gönder
Verileri gönderme ve hello kullanıcıların etkin olduğundan emin olmak sipariş toostart içinde en az bir ekran toohello Mobile Engagement arka göndermeniz gerekir. Bunu yapmak için-o hello olun `MainActivity` devraldığı `EngagementActivity` yerine `Activity`.

    public class MainActivity : EngagementActivity

Alternatif olarak, `EngagementActivity` konumundan devralamıyorsanız `.StartActivity` ve `.EndActivity` yöntemlerini sırasıyla `OnResume` ve `OnPause` içine eklemeniz gerekir.  

        protected override void OnResume()
            {
                EngagementAgent.StartActivity(EngagementAgentUtils.BuildEngagementActivityName(Java.Lang.Class.FromType(this.GetType())), null);
                base.OnResume();             
            }

            protected override void OnPause()
            {
                EngagementAgent.EndActivity();
                base.OnPause();            
            }

## <a id="monitor"></a>Uygulamayı gerçek zamanlı izlemeyle bağlama
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Anında iletme bildirimlerini ve uygulama içi mesajlaşmayı etkinleştirme
Mobile Engagement ile toointeract sağlar ve kullanıcılarınızın anında iletme bildirimleri ve uygulama içi Mesajlaşma hello Kampanyalar bağlamında ULAŞILIRSA. Bu modül hello Mobile Engagement portalında REACH adı verilir.
Aşağıdaki bölümlerde Merhaba, uygulama tooreceive bunları ayarlar.

[!INCLUDE [Enable Google Cloud Messaging](../../includes/mobile-engagement-enable-google-cloud-messaging.md)]

[!INCLUDE [Enable in-app messaging](../../includes/mobile-engagement-android-send-push.md)]

[!INCLUDE [Send notification from portal](../../includes/mobile-engagement-android-send-push-from-portal.md)]

<!-- Images -->
[1]: ./media/mobile-engagement-xamarin-android-get-started/1.png
[2]: ./media/mobile-engagement-xamarin-android-get-started/2.png
[3]: ./media/mobile-engagement-xamarin-android-get-started/3.png
[4]: ./media/mobile-engagement-xamarin-android-get-started/4.png
[5]: ./media/mobile-engagement-xamarin-android-get-started/5.png
[6]: ./media/mobile-engagement-xamarin-android-get-started/6.png
