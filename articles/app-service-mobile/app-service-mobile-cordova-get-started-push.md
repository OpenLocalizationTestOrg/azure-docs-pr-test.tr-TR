---
title: "aaaAdd anında iletme bildirimleri tooApache Azure Mobile Apps ile Cordova uygulaması | Microsoft Docs"
description: "Nasıl toouse Azure Mobile Apps toosend anında bildirimler tooyour Apache Cordova uygulaması hakkında bilgi edinin."
services: app-service\mobile
documentationcenter: javascript
manager: syntaxc4
editor: 
author: ggailey777
ms.assetid: 92c596a9-875c-4840-b0e1-69198817576f
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-html
ms.devlang: javascript
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 8e1b23d6145b446b6f01599337b677e2f2b31d7e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="add-push-notifications-tooyour-apache-cordova-app"></a>Anında iletme bildirimleri tooyour Apache Cordova uygulaması ekleyin
[!INCLUDE [app-service-mobile-selector-get-started-push](../../includes/app-service-mobile-selector-get-started-push.md)]

## <a name="overview"></a>Genel Bakış
Bu öğreticide, böylece bir kayda eklenen her zaman bir anında iletme bildirimi toohello aygıt gönderilen anında iletme bildirimleri toohello [Apache Cordova Hızlı Başlangıç] projeye ekleyin.

Kullanmıyorsanız, hızlı başlangıç sunucu projesi hello indirilen, anında iletme bildirimi uzantısı paketi hello. Daha fazla bilgi için bkz: [hello .NET arka uç sunucusu SDK ile Azure Mobile Apps için iş][1].

## <a name="prerequisites"></a>Önkoşullar
Bu öğretici hello Google Android öykünücüsü, bir Android cihazında, bir Windows aygıtı ve bir iOS aygıtı üzerinde çalışan Visual Studio 2015 ile geliştirilen bir Apache Cordova uygulaması kapsar.

toocomplete Bu öğretici, gerekir:

* Bir bilgisayarla [Visual Studio Community 2015] [ 2] veya sonraki sürümler.
* [Apache Cordova için Visual Studio Araçları][4].
* Bir [etkin Azure hesabı][3].
* Bir tamamlanmış [Apache Cordova Hızlı Başlangıç] [ 5] projesi.
* (Android) A [Google hesabı] [ 6] doğrulanmış e-posta adresine sahip.
* (iOS) Bir [Apple Developer Program üyeliği] [ 7] ve bir iOS cihazı (iOS simülatörü itme desteklemez).
* (Windows) A [Windows mağazası Geliştirici hesabınızla] [ 8] ve Windows 10 cihaz.

## <a name="configure-hub"></a>Bildirim hub'ı yapılandırma
[!INCLUDE [app-service-mobile-configure-notification-hub](../../includes/app-service-mobile-configure-notification-hub.md)]

[Bu bölümdeki adımları gösteren bir videoyu izleyin][9]

## <a name="update-hello-server-project"></a>Güncelleştirme hello sunucu projesi
[!INCLUDE [app-service-mobile-update-server-project-for-push-template](../../includes/app-service-mobile-update-server-project-for-push-template.md)]

## <a name="add-push-to-app"></a>Cordova uygulamanızı değiştirme
Apache Cordova uygulaması projenize hazır toohandle anında iletme bildirimleri yükleme hello Cordova itme eklentisi artı hiçbir platforma özgü anında hizmet tarafından olduğundan emin olun.

#### <a name="update-hello-cordova-version-in-your-project"></a>Projenizdeki Hello Cordova sürümünü güncelleştirin.
Projenizi Apache Cordova v6.1.1'den önceki bir sürümünü kullanıyorsa, hello istemci projesi güncelleştirin. tooupdate hello proje:

* Sağ `config.xml` tooopen hello yapılandırma Tasarımcısı.
* Merhaba platformları sekmesini seçin.
* Hello 6.1.1 seçin **Cordova CLI** metin kutusu.
* Seçin **yapı**, ardından **yapı çözümü** tooupdate hello projesi.

#### <a name="install-hello-push-plugin"></a>Merhaba itme eklentisini yükleme
Apache Cordova uygulamaları aygıt ya da ağ yetenekleri yerel işleyemez.  Bu özellikler tarafından sağlanan olan eklentileri üzerinde ya da yayımlanan [npm] [ 10] veya github'da.  Merhaba `phonegap-plugin-push` eklentidir kullanılan toohandle ağ anında iletme bildirimleri.

Merhaba itme eklentisi şu yollardan biriyle yükleyebilirsiniz:

**Merhaba-komut dosyasından:**

Merhaba aşağıdaki komutu yürütün:

    cordova plugin add phonegap-plugin-push

**Gelen Visual Studio içinde:**

1. Çözüm Gezgini'nde hello açın `config.xml` dosyası **eklentileri** > **özel**seçin **Git** yükleme kaynağı olarak enter`https://github.com/phonegap/phonegap-plugin-push`hello kaynağı olarak.

   ![][img1]

2. Merhaba ok sonraki toohello yükleme kaynağı'ı tıklatın.
3. İçinde **SENDER_ID**, sayısal proje kimliği hello Google Developer konsol projesi için zaten varsa, bunu burada ekleyebilirsiniz. Aksi takdirde, 777777 gibi bir yer tutucu değerini girin.  Android hedefliyorsanız, bu değeri daha sonra config.xml güncelleştirebilirsiniz.
4. **Ekle**'ye tıklayın.

Merhaba itme eklentisi artık yüklüdür.

#### <a name="install-hello-device-plugin"></a>Merhaba aygıt eklentisini yükleme
İzleme hello aynı yordamı tooinstall hello itme eklentisi kullanılır.  Merhaba çekirdek eklentiler listesinden Hello aygıt eklenti ekleme (tıklatın **eklentileri** > **çekirdek** toofind onu). Bu eklenti tooobtain hello platform adı gerekir.

#### <a name="register-your-device-on-application-start-up"></a>Uygulama başlatma aygıtınızda kaydetme
Başlangıçta, biz bazı çok az kod Android için içerir. Daha sonra iOS veya Windows 10 hello uygulama toorun değiştirin.

1. Çağrı çok ekleyin**registerForPushNotifications** hello oturum açma işlemi için ya da hello hello sonundaki hello geri çağırma sırasında **onDeviceReady** yöntemi:

        // Login toohello service.
        client.login('google')
            .then(function () {
                // Create a table reference
                todoItemTable = client.getTable('todoitem');

                // Refresh hello todoItems
                refreshDisplay();

                // Wire up hello UI Event Handler for hello Add Item
                $('#add-item').submit(addItemHandler);
                $('#refresh').on('click', refreshDisplay);

                    // Added tooregister for push notifications.
                registerForPushNotifications();

            }, handleError);

    Bu örnek, arama gösterir **registerForPushNotifications** kimlik doğrulaması başarılı olduktan sonra.  Çağırabilirsiniz `registerForPushNotifications()` gereklidir sıklıkta.

2. Merhaba yeni Ekle **registerForPushNotifications** yöntemini aşağıdaki şekilde:

        // Register for Push Notifications. Requires that phonegap-plugin-push be installed.
        var pushRegistration = null;
        function registerForPushNotifications() {
          pushRegistration = PushNotification.init({
              android: { senderID: 'Your_Project_ID' },
              ios: { alert: 'true', badge: 'true', sound: 'true' },
              wns: {}
          });

        // Handle hello registration event.
        pushRegistration.on('registration', function (data) {
          // Get hello native platform of hello device.
          var platform = device.platform;
          // Get hello handle returned during registration.
          var handle = data.registrationId;
          // Set hello device-specific message template.
          if (platform == 'android' || platform == 'Android') {
              // Register for GCM notifications.
              client.push.register('gcm', handle, {
                  mytemplate: { body: { data: { message: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'iOS') {
              // Register for notifications.
              client.push.register('apns', handle, {
                  mytemplate: { body: { aps: { alert: "{$(messageParam)}" } } }
              });
          } else if (device.platform === 'windows') {
              // Register for WNS notifications.
              client.push.register('wns', handle, {
                  myTemplate: {
                      body: '<toast><visual><binding template="ToastText01"><text id="1">$(messageParam)</text></binding></visual></toast>',
                      headers: { 'X-WNS-Type': 'wns/toast' } }
              });
          }
        });

        pushRegistration.on('notification', function (data, d2) {
          alert('Push Received: ' + data.message);
        });

        pushRegistration.on('error', handleError);
        }
3. (Android) Kod önceki hello yerine `Your_Project_ID` uygulamanızdan için kimliği ile Merhaba sayısal proje [Google Developer konsolunda][18].

## <a name="optional-configure-and-run-hello-app-on-android"></a>(İsteğe bağlı) Yapılandırma ve hello uygulama Android'de çalıştırma
Bu bölümde tooenable anında iletme bildirimleri Android tamamlayın.

#### <a name="enable-gcm"></a>Firebase etkinleştirmek bulut Mesajlaşma
Google Android platformu hello başlangıçta hedefleme bu yana Firebase Cloud Messaging etkinleştirmeniz gerekir.

[!INCLUDE [notification-hubs-enable-firebase-cloud-messaging](../../includes/notification-hubs-enable-firebase-cloud-messaging.md)]

#### <a name="configure-backend"></a>Merhaba mobil uygulama arka uç toosend gönderme istekleri FCM kullanarak yapılandırma
[!INCLUDE [app-service-mobile-android-configure-push](../../includes/app-service-mobile-android-configure-push.md)]

#### <a name="configure-your-cordova-app-for-android"></a>Android için Cordova uygulamanızı yapılandırma
Cordova uygulamanızı config.xml açın ve değiştirmek `Your_Project_ID` hello uygulamanızdan için kimliği ile Merhaba sayısal proje [Google Developer konsolunda][18].

        <plugin name="phonegap-plugin-push" version="1.7.1" src="https://github.com/phonegap/phonegap-plugin-push.git">
            <variable name="SENDER_ID" value="Your_Project_ID" />
        </plugin>

İndex.js açın ve sayısal proje kimliğinizi hello kod toouse güncelleştir

        pushRegistration = PushNotification.init({
            android: { senderID: 'Your_Project_ID' },
            ios: { alert: 'true', badge: 'true', sound: 'true' },
            wns: {}
        });

#### <a name="configure-device"></a>USB hata ayıklama için Android Cihazınızı yapılandırın
Uygulama tooyour Android cihazı dağıtmadan önce tooenable USB hata ayıklama gerekir.  Android telefonunuzda aşağıdaki adımları gerçekleştirin:

1. Çok Git**ayarları** > **telefon hakkında**, hello dokunun **yapı numarası** geliştirici modunu (yaklaşık yedi defa) etkinleştirilene kadar.
2. Geri **ayarları** > **Geliştirici seçenekleri** etkinleştirmek **USB hata ayıklama**, ardından Android telefonunuzu tooyour geliştirme bilgisayarınıza bir USB kablosu ile bağlanın.

Bu Android 6.0 (Marshmallow) çalıştıran bir Google Nexus 5 X aygıtı kullanarak test.  Ancak, tüm modern Android sürüm arasında hello teknikleri yaygındır.

#### <a name="install-google-play-services"></a>Google Play hizmetlerini yükleyin
Merhaba itme eklentisi Android Google Play Hizmetleri'nin anında iletme bildirimleri için kullanır.

1. Visual Studio'da sırasıyla **Araçları** > **Android** > **Android SDK Manager**, hello genişletin **ek özellikler** klasör ve onay hello kutusunu toomake her SDK'ları aşağıdaki hello yüklendiğinden emin olun.

   * Android 2.3 veya daha yüksek
   * Google depo düzeltme 27 veya daha yüksek
   * Google Play hizmetlerini 9.0.2 veya üzeri

2. Tıklatın **yükleme paketleri** ve hello yükleme toocomplete için bekleyin.

Merhaba geçerli kitaplıkları hello listelenen gerekli [phonegap eklentiyi itme yükleme belgelerini][19].

#### <a name="test-push-notifications-in-hello-app-on-android"></a>Merhaba uygulamasında android'de test anında iletme bildirimleri
Uygulama ve hello Todoıtem tablosu ekleme öğelerde çalıştırarak test anında iletme bildirimleri hello artık kullanabilirsiniz. Test edebilirsiniz hello aynı cihaz veya kullanmakta olduğunuz sürece ikinci bir aygıttan aynı hello arka uç. Cordova uygulamanızı hello Android platformunda yolları aşağıdaki hello birinde test edin:

* **Bir fiziksel cihaz üzerindeki:** Android cihaz tooyour geliştirme bilgisayarınıza bir USB kablosu ile ekleyin.  Yerine **Google Android öykünücüsü**seçin **aygıt**. Visual Studio hello uygulama toohello aygıt dağıtır ve ardından Merhaba uygulaması çalıştırır.  Hello aygıtta hello uygulama ile etkileşim kurabilirsiniz.

  Geliştirme deneyiminizi iyileştirebilir.  Ekran uygulamaları gibi paylaşımı [Mobizen] [ 20] Android uygulama geliştirmede yardımcı olabilir.  Mobizen Android ekran tooa web tarayıcınızı bilgisayarınıza projeleri.

* **Android öykünücüsünde üzerinde:** bir öykünücü üzerinde çalışırken gereken ek yapılandırma adımları vardır.

    Google API'leri hello hedef olarak ayarlanmış hello Android sanal cihazı (AVD) Yöneticisi'nde gösterildiği gibi tooa sanal cihaza dağıttığınız emin olun.

    ![](./media/app-service-mobile-cordova-get-started-push/google-apis-avd-settings.png)

    Daha hızlı x86 toouse istiyorsanız öykünücüsü, [hello HAXM sürücüyü yüklemek] [ 11] ve hello öykünücüsü toouse yapılandırmak.

    Bir Google hesabı toohello Android cihazı tıklayarak ekleyin **uygulamaları** > **ayarları** > **hesabı eklemek**, hello istemleri izleyin.

    ![](./media/app-service-mobile-cordova-get-started-push/add-google-account.png)

    Önce Hello Yapılacaklar listesi uygulaması gibi çalıştırabilir ve yeni bir Yapılacaklar öğesi ekleyin. Bu süre, hello bildirim alanında bir bildirim simgesi görüntülenir. Merhaba bildirim çekmecesini tooview hello tam metin hello bildirim açabilirsiniz.

    ![](./media/app-service-mobile-cordova-get-started-push/android-notifications.png)

## <a name="optional-configure-and-run-on-ios"></a>(İsteğe bağlı) Yapılandırma ve İos'ta çalıştırma
Bu bölümde, iOS cihazlarda hello Cordova projesi çalıştırmaya yöneliktir. İOS cihazlarıyla çalışmıyorsanız, bu bölümü atlayabilirsiniz.

#### <a name="install-and-run-hello-ios-remote-build-agent-on-a-mac-or-cloud-service"></a>Yükleme ve çalıştırma hello iOS uzak aracı bir Mac veya Bulut hizmetinde derleme
Visual Studio kullanarak iOS Cordova uygulaması çalıştırmadan önce hello hello içinde adımlarını [iOS kurulum kılavuzunu] [ 12] tooinstall ve uzak çalışma hello derleme aracısı.

İOS için başlangıç uygulaması oluşturduğunuzdan emin olun. Merhaba hello Kurulum Kılavuzu'nda Visual Studio'dan iOS için gerekli toobuild adımlardır. Mac yoksa hello uzak derleme aracısı MacInCloud gibi bir hizmet kullanarak iOS için oluşturabilirsiniz. Daha fazla bilgi için bkz: [hello bulutta iOS uygulamanızı çalıştırma][21].

> [!NOTE]
> XCode 7 veya daha fazla gerekli toouse hello itme iOS eklentidir.

#### <a name="find-hello-id-toouse-as-your-app-id"></a>Merhaba kimliği toouse uygulama Kimliğiniz Bul
Anında iletme bildirimleri için uygulamanızı kaydetme önce config.xml Cordova uygulamanızı açın, hello Bul `id` öznitelik değeri hello pencere öğesinde ve daha sonra kullanmak üzere kopyalayın. XML aşağıdaki hello hello kimliğidir `io.cordova.myapp7777777`.

        <widget defaultlocale="en-US" id="io.cordova.myapp7777777"
          version="1.0.0" windows-packageVersion="1.1.0.0" xmlns="http://www.w3.org/ns/widgets"
            xmlns:cdv="http://cordova.apache.org/ns/1.0" xmlns:vs="http://schemas.microsoft.com/appx/2014/htmlapps">

Apple Geliştirici Portalı üzerinde bir uygulama kimliği oluşturduğunuzda, daha sonra bu tanımlayıcı kullanın. Farklı bir uygulama kimliği hello Geliştirici portalında oluşturursanız, daha sonra Bu öğreticide birkaç ek adımlar atmanız gerekir. Pencere öğesinde Hello kimliği hello uygulama kimliği hello Geliştirici portalındaki eşleşmelidir.

#### <a name="register-hello-app-for-push-notifications-on-apples-developer-portal"></a>Apple Geliştirici portalındaki anında iletme bildirimleri için Hello uygulamasını Kaydet
[!INCLUDE [Enable Apple Push Notifications](../../includes/enable-apple-push-notifications.md)]

[Benzer adımları gösteren bir video izleyin](https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-5-Set-up-apns-for-push)

#### <a name="configure-azure-toosend-push-notifications"></a>Azure toosend anında iletme bildirimleri yapılandırma
[!INCLUDE [app-service-mobile-apns-configure-push](../../includes/app-service-mobile-apns-configure-push.md)]

#### <a name="verify-that-your-app-id-matches-your-cordova-app"></a>Uygulama Kimliğiniz Cordova uygulamanızı eşleştiğini doğrulayın
Merhaba Apple Geliştirici hesabınızda zaten oluşturulmuş uygulama kimliği config.xml hello pencere öğesinde hello Kimliğini eşleşiyorsa, bu adımı atlayabilirsiniz. Ancak, Hello kimlikler eşleşmezse, hello aşağıdaki adımları gerçekleştirin:

1. Merhaba platformları klasörü projenizden silin.
2. Merhaba eklentileri klasörü projenizden silin.
3. Merhaba node_modules klasörü projenizden silin.
4. Güncelleştirme hello ID özniteliği hello pencere öğesinde config.xml toouse hello Apple Geliştirici hesabınızda oluşturduğunuz uygulama kimliği.
5. Projenizi yeniden derleyin.

##### <a name="test-push-notifications-in-your-ios-app"></a>İOS uygulamanızı test anında iletme bildirimleri
1. Visual Studio'da olduğundan emin olun **iOS** hello dağıtım hedefi olarak seçilir ve ardından **aygıt** toorun bağlı iOS Cihazınızda.

    Bir iOS aygıtı bağlı tooyour PC çalıştırabilirsiniz iTunes kullanma. Merhaba iOS simülatörü anında iletme bildirimlerini desteklemiyor.

2. Tuşuna hello **çalıştırmak** düğmesini veya **F5** Visual Studio toobuild hello proje ve başlangıç hello bir iOS aygıtı uygulamada ve ardından tıklayın **Tamam** tooaccept anında iletme bildirimleri.

   > [!NOTE]
   > Merhaba uygulaması ilk çalıştırma hello sırasında anında iletme bildirimleri için onay ister.

3. Merhaba uygulamada, bir görev yazın ve hello artı (+) ardından simge.
4. Bir bildirim alındı ve ardından Tamam toodismiss hello bildirim doğrulayın.

## <a name="optional-configure-and-run-on-windows"></a>(İsteğe bağlı) Yapılandırma ve Windows'ta çalıştırma
Bu bölümde, Windows 10 cihazlarda (Merhaba PhoneGap itme eklentisi üzerinde Windows 10 desteklenir) hello Apache Cordova uygulaması projesi çalıştırmaya yöneliktir. Windows cihazlarıyla çalışmıyorsanız, bu bölümü atlayabilirsiniz.

#### <a name="register-your-windows-app-for-push-notifications-with-wns"></a>Windows uygulamanızı anında iletme bildirimleri için WNS ile kaydetme
Visual Studio'da toouse hello depolama seçenekleri Windows hedef gibi hello çözüm platformları listeden seçin **Windows x64** veya **Windows x86** (kaçının **Windows AnyCPU** için anında iletme bildirimleri).

[!INCLUDE [app-service-mobile-register-wns](../../includes/app-service-mobile-register-wns.md)]

[Benzer adımları gösteren bir videoyu izleyin][13]

#### <a name="configure-hello-notification-hub-for-wns"></a>WNS için Hello bildirim hub'ı yapılandırma
[!INCLUDE [app-service-mobile-configure-wns](../../includes/app-service-mobile-configure-wns.md)]

#### <a name="configure-your-cordova-app-toosupport-windows-push-notifications"></a>Cordova uygulaması toosupport Windows anında iletme bildirimleri yapılandırma
Açık hello yapılandırma Tasarımcısı (sağ tıklatın ve config.xml **Görünüm Tasarımcısı**), select hello **Windows** sekmesini tıklatın ve seçin **Windows 10** altında**Windows hedef sürüm**.

Açık build.json dosya toosupport anında iletme bildirimleri için varsayılan (hata ayıklama) oluşturur. "Yayın" yapılandırma tooyour hata ayıklama yapılandırması kopyalayın.

        "windows": {
            "release": {
                "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
                "publisherId": "CN=yourpublisherID"
            }
        }

Merhaba güncelleştirmeden sonra hello build.json koddan hello içermelidir:

    "windows": {
        "release": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            },
        "debug": {
            "packageCertificateKeyFile": "res\\native\\windows\\CordovaApp.pfx",
            "publisherId": "CN=yourpublisherID"
            }
        }

Merhaba uygulaması oluşturma ve hiçbir hata sahip olduğunuzu doğrulayın. İstemci uygulamanızı hello mobil uygulama arka ucu hello bildirimleri için şimdi kaydetmelisiniz. Bu bölümde, çözümünüz içinde her Windows projesi için tekrarlayın.

#### <a name="test-push-notifications-in-your-windows-app"></a>Windows uygulamanızı test anında iletme bildirimleri
Visual Studio'da Windows platformu aşağıdaki gibi hello dağıtım hedefi olarak seçildiğinden emin olun **Windows x64** veya **Windows x86**. Visual Studio, barındırma Windows 10 PC'de toorun hello uygulamayı seçin **yerel makine**.

Tuşuna hello düğmesi toobuild Merhaba projeyi çalıştırın ve hello uygulamayı başlatın.

Merhaba uygulamasında yeni bir todoıtem için bir ad yazın ve hello artı (+) ardından simge tooadd onu.

Merhaba öğesi eklendiğinde, bir bildirim alındığında doğrulayın.

## <a name="next-steps"></a>Sonraki Adımlar
* Hakkında bilgi edinin [bildirim hub'ları] [ 17] toolearn anında iletme bildirimleri hakkında.
* Zaten yapmadıysanız, hello Öğreticisi tarafından devam [Authentication ekleme] [ 14] tooyour Apache Cordova uygulaması.

Nasıl toouse hello SDK'ları hakkında bilgi edinin.

* [Apache Cordova SDK'sı][15]
* [ASP.NET sunucusu SDK][1]
* [Node.js sunucusu SDK][16]

<!-- Images -->
[img1]: ./media/app-service-mobile-cordova-get-started-push/add-push-plugin.png

<!-- URLs -->
[1]: app-service-mobile-dotnet-backend-how-to-use-server-sdk.md
[2]: http://www.visualstudio.com/
[3]: https://azure.microsoft.com/pricing/free-trial/
[4]: https://www.visualstudio.com/en-us/features/cordova-vs.aspx
[5]: app-service-mobile-cordova-get-started.md
[6]: http://go.microsoft.com/fwlink/p/?LinkId=268302
[7]: https://developer.apple.com/programs/
[8]: https://developer.microsoft.com/en-us/store/register
[9]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-3-Create-azure-notification-hub
[10]: https://www.npmjs.com/
[11]: https://taco.visualstudio.com/en-us/docs/run-app-apache/#HAXM
[12]: http://taco.visualstudio.com/en-us/docs/ios-guide/
[13]: https://channel9.msdn.com/series/Azure-connected-services-with-Cordova/Azure-connected-services-task-6-Set-up-wns-for-push
[14]: app-service-mobile-cordova-get-started-users.md
[15]: app-service-mobile-cordova-how-to-use-client-library.md
[16]: app-service-mobile-node-backend-how-to-use-server-sdk.md
[17]: ../notification-hubs/notification-hubs-push-notification-overview.md
[18]: https://console.developers.google.com/home/dashboard
[19]: https://github.com/phonegap/phonegap-plugin-push/blob/master/docs/INSTALLATION.md
[20]: https://www.mobizen.com/
[21]: http://taco.visualstudio.com/en-us/docs/build_ios_cloud/
