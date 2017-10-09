---
title: "aaaGet Baidu kullanarak Azure Notification Hubs ile çalışmaya | Microsoft Docs"
description: "Bu öğreticide, bilgi nasıl Baidu kullanarak toouse Azure Notification Hubs toopush bildirimleri tooAndroid cihazları."
services: notification-hubs
documentationcenter: android
author: ysxu
manager: erikre
editor: 
ms.assetid: 23bde1ea-f978-43b2-9eeb-bfd7b9edc4c1
ms.service: notification-hubs
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: mobile-baidu
ms.workload: mobile
ms.date: 08/19/2016
ms.author: yuaxu
ms.openlocfilehash: 2767fdd3bb04674e7a531634237cc05cd8c21cb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-notification-hubs-using-baidu"></a>Baidu kullanarak Azure Notification Hubs ile çalışmaya başlama
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Genel Bakış
Baidu bulut anında iletme toosend anında iletme bildirimleri toomobile aygıtları kullanabileceğiniz bir Çin bulut hizmetidir. Bu hizmet, burada tooAndroid hello varlığını farklı uygulama mağazalarının ve anında iletme nedeniyle karmaşıktır anında iletme bildirimleri teslim hizmetleri, ayrıca genellikle bağlı tooGCM (Google olmayan Android cihazları toohello kullanılabilirliğini Çin'de yararlıdır Mesajlaşma bulut).

## <a name="prerequisites"></a>Ön koşullar
Bu öğretici için aşağıdakiler gereklidir:

* Hello karşıdan yükleyebileceğiniz, (varsayıyoruz Eclipse kullanın) android SDK <a href="http://go.microsoft.com/fwlink/?LinkId=389797">Android sitesi</a>
* [Mobile Services Android SDK'sı]
* [Baidu anında iletme Android SDK]

> [!NOTE]
> toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-baidu-get-started%2F).
> 
> 

## <a name="create-a-baidu-account"></a>Bir Baidu hesabı oluşturma
Baidu toouse, bir Baidu hesabınızın olması gerekir. Zaten varsa, toohello içinde oturum [Baidu portalında] ve toohello bir sonraki adımı atlayın. Aksi takdirde hakkında yönergeleri izleyerek hello bkz toocreate bir Baidu hesabı.  

1. Toohello Git [Baidu portalında] hello tıklatıp**登录**(**oturum açma**) bağlantı. Tıklatın**立即注册**toostart hello hesap kayıt işlemi.
   
   ![][1]
2. Merhaba gerekli ayrıntıları girin: telefon/e-posta adresi, parola ve doğrulama kodu — tıklatıp **kaydolma**.
   
   ![][2]
3. Bir e-posta toohello e-posta adresine gönderilecek bir bağlantı tooactivate ile Baidu hesabınızı girilen.
   
   ![][3]
4. Tooyour e-posta hesabında oturum, hello Baidu etkinleştirme posta açın ve Baidu hesabınızı hello etkinleştirme bağlantı tooactivate tıklatın.
   
   ![][4]

Baidu hesabınızı etkinleştirdikten sonra toohello içinde oturum [Baidu portalında].

## <a name="register-as-a-baidu-developer"></a>Bir Baidu geliştiricisi olarak kaydolma
1. İçinde toohello oturum açtıktan sonra [Baidu portalında], tıklatın**更多 >>** (**daha fazla**).
   
      ![][5]
2. Aşağı kaydırın hello**站长与开发者服务 (yayımlanması ve geliştirici Hizmetleri)** 'ye tıklayın**百度开放云平台**(**Baidu bulut platformu açmak**).
   
      ![][6]
3. Merhaba sonraki sayfasında, tıklatın**开发者服务**(**Geliştirici Hizmetleri**) hello sağ üst köşede.
   
      ![][7]
4. Merhaba sonraki sayfasında, tıklatın**注册开发者**(**kayıtlı geliştiriciler**) hello sağ üst köşesinde hello menüsünden.
   
      ![][8]
5. Bir doğrulama kısa mesajı almak için adınızı, açıklamayı ve cep telefonu numarasını girin ve ardından **送验证码** (**Doğrulama Kodu Gönder**) öğesine tıklayın. Uluslararası telefon numaraları için parantez içinde tooenclose hello ülke kodu gerekir. Örneğin, bir Amerika Birleşik Devletleri numarası için bu **(1) 1234567890** şeklinde olacaktır.
   
      ![][9]
6. Ardından hello aşağıdaki örnekte gösterildiği gibi bir doğrulama numarasına sahip bir kısa mesaj almalısınız:
   
      ![][10]
7. Merhaba iletisi Hello doğrulama numarasını girin**验证码**(**onay kodu**).
8. Son olarak, hello Geliştirici kayıt hello Baidu anlaşmayı kabul eden ve'ı tıklatarak tamamlayın**提交**(**gönderme**). Kayıt başarılı şekilde tamamlandığını sayfasında aşağıdaki hello görürsünüz:
   
      ![][11]

## <a name="create-a-baidu-cloud-push-project"></a>Bir Baidu bulut anında iletme projesi oluşturma
Bir Baidu bulut anında iletme projesi oluşturduğunuzda, uygulama kimliğinizi, API anahtarınızı ve gizli anahtarınızı alırsınız.

1. İçinde toohello oturum açtıktan sonra [Baidu portalında], tıklatın**更多 >>** (**daha fazla**).
   
      ![][5]
2. Aşağı kaydırın hello**站长与开发者服务**(**yayımlanması ve geliştirici Hizmetleri**) bölümünde ve tıklatın**百度开放云平台**(**Baidu bulut platformu açmak**).
   
      ![][6]
3. Merhaba sonraki sayfasında, tıklatın**开发者服务**(**Geliştirici Hizmetleri**) hello sağ üst köşede.
   
      ![][7]
4. Merhaba sonraki sayfasında, tıklatın**云推送**(**bulut itme**) hello gelen**云服务**(**bulut Hizmetleri**) bölümü.
   
      ![][12]
5. Kayıtlı bir geliştirici olduktan sonra gördüğünüz**管理控制台**(**Yönetim Konsolu**) hello üst menüsünde. **开发者服务管理** (**Geliştirici Hizmeti Yönetimi**) öğesine tıklayın.
   
      ![][13]
6. Merhaba sonraki sayfasında, tıklatın**创建工程**(**proje oluştur**).
   
      ![][14]
7. Bir uygulama adı girin ve **创建** (**Oluştur**) öğesine tıklayın.
   
      ![][15]
8. Bir Baidu bulut anında iletme projesi başarılı bir şekilde oluşturulduktan sonra, **Uygulama Kimliği**, **API Anahtarı** ve **Gizli Anahtar** değerlerini içeren bir sayfa görürsünüz. Merhaba API anahtarı ve daha sonra kullanacağımız gizli anahtarı not edin.
   
      ![][16]
9. Tıklayarak Hello projesi anında iletme bildirimleri için yapılandırma**云推送**(**bulut anında iletme**) hello sol bölmedeki.
   
      ![][31]
10. Merhaba Hello sonraki sayfasında, tıklatın**推送设置**(**ayarları göndermek**) düğmesi.
    
    ![][32]  
11. Merhaba Android projenizde kullanacağınız hello paket adı Hello yapılandırma sayfasında, eklemek**应用包名**(**uygulama paketi**) alan ve ardından**保存设置**() **Kaydetmek**).  
    
    ![][33]

Merhaba gördüğünüz**保存成功!** (**Başarıyla kaydedildi!**) iletisini görürsünüz.

## <a name="configure-your-notification-hub"></a>Bildirim hub'ınızı yapılandırma
1. İçinde toohello oturum [Klasik Azure portalı]ve ardından **+ yeni** Merhaba ekranında hello sonundaki.
2. **Uygulama Hizmetleri**'ne tıklayın, **Service Bus**'a tıklayın, **Notification Hub**'a tıklayın ve ardından **Hızlı Oluştur**'a tıklayın.
3. İçin bir ad, **bildirim hub'ı**seçin hello **bölge** ve hello **Namespace** burada bu bildirim hub'ı oluşturulur ve ardından  **Yeni bir Notification Hub Oluştur**.  
   
      ![][17]
4. Bildirim hub'ınızı oluşturduğunuz hello ad alanına tıklayın ve ardından **bildirim hub'ları** hello üstünde.
   
      ![][18]
5. Oluşturulan ve ardından select hello bildirim hub'ı **yapılandırma** hello üst menüsünde.
   
      ![][19]
6. Toohello aşağı **baidu bildirim ayarları** bölümünde ve hello Baidu konsolundan Baidu bulut anında iletme projeniz için daha önce edindiğiniz gizli anahtar ve hello API anahtarını girin. **Kaydet** düğmesine tıklayın.
   
      ![][20]
7. Merhaba tıklatın **Pano** sekmesinde hello üst hello bildirim hub'ı ve ardından **bağlantı dizesini görüntüle**.
   
      ![][21]
8. Merhaba Not **DefaultListenSharedAccessSignature** ve **DefaultFullSharedAccessSignature** hello gelen **erişim bağlantısı bilgileri** penceresi.
   
    ![][22]

## <a name="connect-your-app-toohello-notification-hub"></a>Uygulama toohello bildirim hub'ınıza bağlanın
1. Eclipse ADT'de yeni bir Android projesi (**Dosya** > **Yeni** > **Android Uygulama Projesi**) oluşturun.
   
    ![][23]
2. Girin bir **uygulama adı** ve o hello olun **gereken Minimum SDK** sürümü çok Ayarla**API 16: Android 4.1**.
   
    ![][24]
3. Tıklatın **sonraki** ve hello kadar hello Sihirbazı aşağıdaki devam **etkinlik Oluştur** penceresi görüntülenir. Olduğundan emin olun **boş etkinlik** seçili ve son olarak select **son** toocreate yeni bir Android uygulaması.
   
    ![][25]
4. Bu hello emin olun **proje derleme hedefi** doğru olarak ayarlanmış.
   
    ![][26]
5. Hello Hello notification-hubs-0.4.jar dosyasını indirin **dosyaları** hello sekmesinde [Notification-Hubs-Android-SDK Bintray'deki üzerinde](https://bintray.com/microsoftazuremobile/SDK/Notification-Hubs-Android-SDK/0.4). Merhaba dosya toohello ekleme **kitaplıklar** klasörü Eclipse projenizin ve yenileme hello *kitaplıklar* klasör.
6. İndirip hello sıkıştırmasını [Baidu anında iletme Android SDK]açın hello **kitaplıklar** klasörünü ve ardından kopyalama hello **libs-x.y.z** jar dosyasını ve hello **pushservice**  &  **MIPS** hello klasörlerde **kitaplıklar** Android uygulamanızın klasör.
7. Açık hello **AndroidManifest.xml** dosya Android projesi ve Baidu SDK hello tarafından gerekli olan hello izinleri ekleyin.
   
        <uses-permission android:name="android.permission.INTERNET" />
        <uses-permission android:name="android.permission.READ_PHONE_STATE" />
        <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
        <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
        <uses-permission android:name="android.permission.WRITE_SETTINGS" />
        <uses-permission android:name="android.permission.VIBRATE" />
        <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
        <uses-permission android:name="android.permission.DISABLE_KEYGUARD" />
        <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
        <uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
        <uses-permission android:name="android.permission.ACCESS_DOWNLOAD_MANAGER" />
        <uses-permission android:name="android.permission.DOWNLOAD_WITHOUT_NOTIFICATION" />
8. Merhaba eklemek **android: name** özelliği tooyour **uygulama** öğesinde **AndroidManifest.xml**değiştirerek *yourprojectname* (için Örneğin, **com.example.BaiduTest**). Bu proje adı hello Baidu konsolunda yapılandırdığınız hello bir eşleştiğinden emin olun.
   
        <application android:name="yourprojectname.DemoApplication"
9. Merhaba hello sonra yapılandırmasını hello uygulama öğesi içinde aşağıdaki ekleme **. MainActivity** etkinlik öğesinden değiştirme *yourprojectname* (örneğin, **com.example.BaiduTest**):
   
        <receiver android:name="yourprojectname.MyPushMessageReceiver">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.MESSAGE" />
                <action android:name="com.baidu.android.pushservice.action.RECEIVE" />
                <action android:name="com.baidu.android.pushservice.action.notification.CLICK" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.PushServiceReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="android.intent.action.BOOT_COMPLETED" />
                <action android:name="android.net.conn.CONNECTIVITY_CHANGE" />
                <action android:name="com.baidu.android.pushservice.action.notification.SHOW" />
            </intent-filter>
        </receiver>
   
        <receiver android:name="com.baidu.android.pushservice.RegistrationReceiver"
            android:process=":bdservice_v1">
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.METHOD" />
                <action android:name="com.baidu.android.pushservice.action.BIND_SYNC" />
            </intent-filter>
            <intent-filter>
                <action android:name="android.intent.action.PACKAGE_REMOVED"/>
                <data android:scheme="package" />
            </intent-filter>
        </receiver>
   
        <service
            android:name="com.baidu.android.pushservice.PushService"
            android:exported="true"
            android:process=":bdservice_v1"  >
            <intent-filter>
                <action android:name="com.baidu.android.pushservice.action.PUSH_SERVICE" />
            </intent-filter>
        </service>
10. Adlı yeni bir sınıf ekleyin **ConfigurationSettings.java** toohello projesi.
    
     ![][28]
    
     ![][29]
11. Aşağıdaki kod tooit hello ekleyin:
    
        public class ConfigurationSettings {
                public static String API_KEY = "...";
                public static String NotificationHubName = "...";
                public static String NotificationHubConnectionString = "...";
            }
    
    Merhaba değeri olarak ayarlayın **apı_key** ne hello Baidu bulut projesinden daha önce alınan ile **NotificationHubName** hello Klasik Azure Portalı'ndan bildirim hub'ı adıyla ve  **NotificationHubConnectionString** defaultlistensharedaccesssignature hello Klasik Azure portalı ile.
12. Adlı yeni bir sınıf ekleyin **DemoApplication.java**ve kod tooit aşağıdaki hello ekleyin:
    
        import com.baidu.frontia.FrontiaApplication;
    
        public class DemoApplication extends FrontiaApplication {
            @Override
            public void onCreate() {
                super.onCreate();
            }
        }
13. Adlı başka bir yeni sınıf ekleyin **MyPushMessageReceiver.java**ve kod tooit aşağıdaki hello ekleyin. Merhaba Baidu anında iletme sunucusundan alınan anında iletme bildirimleri tanıtıcıları hello hello sınıfı var.
    
        import java.util.List;
        import android.content.Context;
        import android.os.AsyncTask;
        import android.util.Log;
        import com.baidu.frontia.api.FrontiaPushMessageReceiver;
        import com.microsoft.windowsazure.messaging.NotificationHub;
    
        public class MyPushMessageReceiver extends FrontiaPushMessageReceiver {
            /** TAG tooLog */
            public static NotificationHub hub = null;
            public static String mChannelId, mUserId;
            public static final String TAG = MyPushMessageReceiver.class
                    .getSimpleName();
    
            @Override
            public void onBind(Context context, int errorCode, String appid,
                    String userId, String channelId, String requestId) {
                String responseString = "onBind errorCode=" + errorCode + " appid="
                        + appid + " userId=" + userId + " channelId=" + channelId
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
                mChannelId = channelId;
                mUserId = userId;
    
                try {
                    if (hub == null) {
                        hub = new NotificationHub(
                                ConfigurationSettings.NotificationHubName,
                                ConfigurationSettings.NotificationHubConnectionString,
                                context);
                        Log.i(TAG, "Notification hub initialized");
                    }
                } catch (Exception e) {
                   Log.e(TAG, e.getMessage());
                }
    
                registerWithNotificationHubs();
            }
    
            private void registerWithNotificationHubs() {
               new AsyncTask<Void, Void, Void>() {
                  @Override
                  protected Void doInBackground(Void... params) {
                     try {
                         hub.registerBaidu(mUserId, mChannelId);
                         Log.i(TAG, "Registered with Notification Hub - '"
                                 + ConfigurationSettings.NotificationHubName + "'"
                                 + " with UserId - '"
                                 + mUserId + "' and Channel Id - '"
                                 + mChannelId + "'");
                     } catch (Exception e) {
                         Log.e(TAG, e.getMessage());
                     }
                     return null;
                 }
               }.execute(null, null, null);
            }
    
            @Override
            public void onSetTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onSetTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onDelTags(Context context, int errorCode,
                    List<String> sucessTags, List<String> failTags, String requestId) {
                String responseString = "onDelTags errorCode=" + errorCode
                        + " sucessTags=" + sucessTags + " failTags=" + failTags
                        + " requestId=" + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onListTags(Context context, int errorCode, List<String> tags,
                    String requestId) {
                String responseString = "onListTags errorCode=" + errorCode + " tags="
                        + tags;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onUnbind(Context context, int errorCode, String requestId) {
                String responseString = "onUnbind errorCode=" + errorCode
                        + " requestId = " + requestId;
                Log.d(TAG, responseString);
            }
    
            @Override
            public void onNotificationClicked(Context context, String title,
                    String description, String customContentString) {
                String notifyString = "title=\"" + title + "\" description=\""
                        + description + "\" customContent=" + customContentString;
                Log.d(TAG, notifyString);
            }
    
            @Override
            public void onMessage(Context context, String message,
                    String customContentString) {
                String messageString = "message=\"" + message + "\" customContentString=" + customContentString;
                Log.d(TAG, messageString);
            }
        }
14. Açık **MainActivity.java**ve toohello aşağıdaki hello ekleyin **onCreate** yöntemi:
    
            PushManager.startWork(getApplicationContext(),
                    PushConstants.LOGIN_TYPE_API_KEY, ConfigurationSettings.API_KEY);
15. İçeri aktarma deyimlerini hello üstünde aşağıdaki hello açın:
    
            import com.baidu.android.pushservice.PushConstants;
            import com.baidu.android.pushservice.PushManager;

## <a name="send-notifications-tooyour-app"></a>Bildirimleri tooyour uygulama Gönder
Hello bildirimleri göndererek uygulamanızda bildirim alma hızlı bir şekilde test edebilirsiniz [Azure portal](https://portal.azure.com/) hello kullanarak **Gönder** hello ekran aşağıdaki gösterildiği gibi hello bildirim hub'ı üzerinde düğmesi:

![](./media/notification-hubs-baidu-get-started/notification-hub-test-send-baidu.png)

Anında iletme bildirimleri normalde, uyumlu bir kitaplık kullanılarak Mobile Services veya ASP.NET gibi bir arka uç hizmetinde gönderilir. Bir kitaplık arka ucunuz için kullanılabilir durumda değilse, hello REST API'sini kullanabilirsiniz doğrudan toosend bildirim iletileri.

Bu öğreticide, basit tutmak ve yalnızca arka uç hizmeti yerine bir konsol uygulamasındaki bildirim hub'ları için hello .NET SDK kullanarak bildirim göndererek istemci uygulamanızı test etme gösterme. Merhaba öneririz [Notification Hubs kullanma toopush bildirimleri toousers](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) hello bir ASP.NET arka ucundan bildirim göndermek için sonraki adım olarak Öğreticisi. Ancak, aşağıdaki yaklaşımlardan hello bildirim göndermek için kullanılabilir:

* **REST arabirimi**: hello kullanarak herhangi bir arka uç platform bildirim destekleyebilir [REST arabirimini](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).
* **Microsoft Azure Notification Hubs .NET SDK'sı**: hello Visual Studio için Nuget Paket Yöneticisi, çalışması [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).
* **Node.js**: [nasıl toouse node.js'den Notification Hubs](notification-hubs-nodejs-push-notification-tutorial.md).
* **Mobile Apps**: bir örneği için Notification Hubs ile tümleştirilmiş Azure App Service Mobile Apps arka uç toosend bildirimleri bkz [Ekle anında iletme bildirimleri tooyour mobil uygulama](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).
* **Java / PHP**: REST API'lerini kullanarak toosend bildirim nasıl hello ilişkin bir örnek için bkz: "nasıl toouse Java/php'den Notification Hubs" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).

## <a name="optional-send-notifications-from-a-net-console-app"></a>(İsteğe bağlı) Bir .NET konsol uygulamasından bildirim gönderme
Bu bölümde, bir .NET konsol uygulaması kullanarak bildirim göndermeyi göstereceğiz.

1. Yeni bir Visual C# konsol uygulaması oluşturun:
   
    ![][30]
2. Hello Paket Yöneticisi konsolu penceresinde, hello ayarlamak **varsayılan proje** tooyour yeni konsol uygulama projesi ve sonra hello konsol penceresinde hello aşağıdaki komutu yürütün:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Bu yönerge başvuru toohello Azure Notification Hubs SDK'sı ekler hello kullanarak <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet paketini</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
3. Açık hello dosya **Program.cs** ve hello aşağıdakileri ekleyin deyimi kullanarak:
   
        using Microsoft.Azure.NotificationHubs;
4. İçinde `Program` sınıfı, yöntem aşağıdaki hello ekleyebilir ve *DefaultFullSharedAccessSignatureSASConnectionString* ve *NotificationHubName* elinizde hello değerlere sahip.
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("DefaultFullSharedAccessSignatureSASConnectionString", "NotificationHubName");
            string message = "{\"title\":\"((Notification title))\",\"description\":\"Hello from Azure\"}";
            var result = await hub.SendBaiduNativeNotificationAsync(message);
        }
5. Hello aşağıdaki satırları ekleyin, **ana** yöntemi:
   
         SendNotificationAsync();
         Console.ReadLine();

## <a name="test-your-app"></a>Uygulamanızı test etme
Bu uygulama, yalnızca gerçek bir telefonla connect tootest bir USB kablosu kullanarak telefon tooyour bilgisayar hello. Bu eylem uygulamanız iliştirilmiş hello telefon yükler.

Merhaba öykünücüsünde hello Eclipse üst araç çubuğunda, bu uygulamayla tootest tıklatın **çalıştırmak**ve ardından uygulamanızı seçin: hello öykünücüsü, yüklendiğinde başlatır ve çalıştırmalarını hello uygulama.

Merhaba uygulama Baidu anında bildirim hizmeti hello hello UserID' ve 'Channelıd' alır ve hello bildirim hub'ı ile kaydeder.

bir test bildirimi toosend hello Klasik Azure portalı hello hata ayıklama sekmesini kullanabilirsiniz. Merhaba .NET konsol uygulaması Visual Studio için oluşturulduysa, yalnızca Visual Studio toorun hello uygulamada hello F5 tuşuna basın. Merhaba uygulaması hello üst bildirim alanında cihaz veya öykünücü görünür bir bildirim gönderir.

<!-- Images. -->
[1]: ./media/notification-hubs-baidu-get-started/BaiduRegistration.png
[2]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationInput.png
[3]: ./media/notification-hubs-baidu-get-started/BaiduConfirmation.png
[4]: ./media/notification-hubs-baidu-get-started/BaiduActivationEmail.png
[5]: ./media/notification-hubs-baidu-get-started/BaiduRegistrationMore.png
[6]: ./media/notification-hubs-baidu-get-started/BaiduOpenCloudPlatform.png
[7]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperServices.png
[8]: ./media/notification-hubs-baidu-get-started/BaiduDeveloperRegistration.png
[9]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationInput.png
[10]: ./media/notification-hubs-baidu-get-started/BaiduDevRegistrationConfirmation.png
[11]: ./media/notification-hubs-baidu-get-started/BaiduDevConfirmationFinal.png
[12]: ./media/notification-hubs-baidu-get-started/BaiduCloudPush.png
[13]: ./media/notification-hubs-baidu-get-started/BaiduDevSvcMgmt.png
[14]: ./media/notification-hubs-baidu-get-started/BaiduCreateProject.png
[15]: ./media/notification-hubs-baidu-get-started/BaiduCreateProjectInput.png
[16]: ./media/notification-hubs-baidu-get-started/BaiduProjectKeys.png
[17]: ./media/notification-hubs-baidu-get-started/AzureNHCreation.png
[18]: ./media/notification-hubs-baidu-get-started/NotificationHubs.png
[19]: ./media/notification-hubs-baidu-get-started/NotificationHubsConfigure.png
[20]: ./media/notification-hubs-baidu-get-started/NotificationHubBaiduConfigure.png
[21]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionStringView.png
[22]: ./media/notification-hubs-baidu-get-started/NotificationHubsConnectionString.png
[23]: ./media/notification-hubs-baidu-get-started/EclipseNewProject.png
[24]: ./media/notification-hubs-baidu-get-started/EclipseProjectCreation.png
[25]: ./media/notification-hubs-baidu-get-started/EclipseBlankActivity.png
[26]: ./media/notification-hubs-baidu-get-started/EclipseProjectBuildProperty.png
[27]: ./media/notification-hubs-baidu-get-started/EclipseBaiduReferences.png
[28]: ./media/notification-hubs-baidu-get-started/EclipseNewClass.png
[29]: ./media/notification-hubs-baidu-get-started/EclipseConfigSettingsClass.png
[30]: ./media/notification-hubs-baidu-get-started/ConsoleProject.png
[31]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig1.png
[32]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig2.png
[33]: ./media/notification-hubs-baidu-get-started/BaiduPushConfig3.png

<!-- URLs. -->
[Mobile Services Android SDK'sı]: https://go.microsoft.com/fwLink/?LinkID=280126&clcid=0x409
[Baidu anında iletme Android SDK]: http://developer.baidu.com/wiki/index.php?title=docs/cplat/push/sdk/clientsdk
[Klasik Azure portalı]: https://manage.windowsazure.com/
[Baidu portalında]: http://www.baidu.com/
