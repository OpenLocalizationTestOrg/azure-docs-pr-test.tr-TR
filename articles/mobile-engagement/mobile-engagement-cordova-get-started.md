---
title: "aaaGet Cordova/Phonegap için Azure Mobile Engagement ile başlatıldı"
description: "Bilgi nasıl toouse analizler ve anında iletme bildirimleri ile Azure Mobile Engagement Cordova/Phonegap uygulamaları için."
services: mobile-engagement
documentationcenter: Mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 54fe9113-e239-4ed7-9fd1-a502d7ac7f47
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-phonegap
ms.devlang: js
ms.topic: hero-article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: e67dabbdf7886802bb058f38964e558d5ae6854c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-mobile-engagement-for-cordovaphonegap"></a>Cordova/Phonegap için Azure Mobile Engagement Kullanmaya Başlama
[!INCLUDE [Hero tutorial switcher](../../includes/mobile-engagement-hero-tutorial-switcher.md)]

Bu konu, nasıl gösterir, uygulama kullanımı ve gönderme anında iletme bildirimleri toosegmented kullanıcılarınızın bir mobil uygulama için Cordova ile geliştirilen toouse Azure Mobile Engagement toounderstand.

Bu öğreticide, Mac kullanarak boş bir Cordova uygulaması oluşturup Mobile Engagement SDK ile tümleştireceğiz. Uygulama, temel analiz verileri toplar, iOS için Apple Anında İletilen Bildirim Sistemi (APNS) ve Android için Google Cloud Messaging (GCM) kullanarak anında iletme bildirimlerini alır. Bu tooan iOS veya Android cihazında Test dağıtımını yapacaksınız. 

> [!NOTE]
> toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fmobile-engagement-cordova-get-started).
> 
> 

Bu öğretici hello aşağıdakileri gerektirir:

* Mac uygulama Mağazası'ndan (tooiOS dağıtmak için) yükleyebileceğiniz XCode
* [Android SDK ve öykünücüsü](http://developer.android.com/sdk/installing/index.html) (dağıtmayla tooAndroid)
* APNS için Apple Dev Center'dan edinebileceğiniz anında iletme bildirimi sertifikası (.p12)
* GCM için Google Developer Console’unuzdan edinebileceğiniz GCM Proje numarası
* [Mobile Engagement Cordova eklentisi](https://www.npmjs.com/package/cordova-plugin-ms-azure-mobile-engagement)

> [!NOTE]
> Merhaba kaynak kodu bulun ve üzerinde hello Cordova eklentisi için Benioku hello [GitHub](https://github.com/Azure/azure-mobile-engagement-cordova)
> 
> 

## <a id="setup-azme"></a>Cordova uygulamanız için Mobile Engagement kurma
[!INCLUDE [Create Mobile Engagement App in Portal](../../includes/mobile-engagement-create-app-in-portal-new.md)]

## <a id="connecting-app"></a>Uygulamanızın toohello Mobile Engagement arka ucuna bağlama
Bu öğreticide hello en az gerekli toocollect veri kümesi ve bir anında iletme bildirimi gönderme bir "temel tümleştirme" gösterilmektedir. 

Cordova toodemonstrate hello tümleştirme ile temel bir uygulama oluşturacağız:

### <a name="create-a-new-cordova-project"></a>Yeni bir Cordova projesi oluşturma
1. Başlatma *Terminal* hangi hello varsayılan şablondan yeni bir Cordova projesi oluşturacak aşağıdaki, Mac makine ve türü hello penceresinde. Hello yayımlama, sonunda kullanım toodeploy profil olduğundan emin olun, iOS uygulamanızın uygulama kimliği hello olarak 'com.mycompany.myapp' kullanıyor 
   
        $ cordova create azme-cordova com.mycompany.myapp
        $ cd azme-cordova
2. Projeniz için tooconfigure aşağıdaki hello yürütme **iOS** ve hello iOS simülatörü çalıştırın:
   
        $ cordova platform add ios 
        $ cordova run ios
3. Projeniz için tooconfigure aşağıdaki hello yürütme **Android** ve hello Android öykünücüsünde çalıştırın. Android SDK öykünücüsü ayarlarınızı hedef olarak Google API'leri (Google Inc.) ile Merhaba CPU olduğundan emin olun / ABI olarak Google API'ler ARM'si.  
   
        $ cordova platform add android
        $ cordova run android
4. Merhaba Cordova Konsolu eklentisini ekleyin. 

    ```
    $ cordova plugin add cordova-plugin-console
    ``` 

### <a name="connect-your-app-toomobile-engagement-backend"></a>Uygulamanızın tooMobile Engagement arka ucuna bağlanmak
1. Merhaba değişken değerleri tooconfigure hello eklentisi sağlarken Hello Azure Mobile Engagement Cordova eklentisini yükleyin:
   
        cordova plugin add cordova-plugin-ms-azure-mobile-engagement    
             --variable AZME_IOS_CONNECTION_STRING=<iOS Connection String> 
            --variable AZME_IOS_REACH_ICON=... (icon name WITH extension) 
            --variable AZME_ANDROID_CONNECTION_STRING=<Android Connection String> 
            --variable AZME_ANDROID_REACH_ICON=... (icon name WITHOUT extension)       
            --variable AZME_ANDROID_GOOGLE_PROJECT_NUMBER=... (From your Google Cloud console for sending push notifications) 
            --variable AZME_ACTION_URL =... (URL scheme which triggers hello app for deep linking)
            --variable AZME_ENABLE_NATIVE_LOG=true|false
            --variable AZME_ENABLE_PLUGIN_LOG=true|false

*Android Reach simgesi* : hello kaynağı herhangi bir uzantı veya drawable ön eki olmadan hello adı olması gerekir (örn: mynotificationicon), ve android projenize (platformları/android/res/drawable) hello simge dosyası kopyalanır

*iOS Reach simgesi* : hello kaynak uzantısı hello adı olması gerekir (örn: mynotificationicon.png), ve hello simge dosyası eklenir (Merhaba Ekle dosyaları menüsünü kullanarak) XCode ile iOS projenize gerekir

## <a id="monitor"></a>Gerçek zamanlı izlemeyi etkinleştirme
1. Merhaba Cordova projesinde **www/js/index.js** tooMobile katılım toodeclare yeni bir etkinlik bir kez hello tooadd hello çağrısı *deviceReady* olayı alındığında.
   
         onDeviceReady: function() {
                Engagement.startActivity("myPage",{});
            }
2. Merhaba uygulamayı çalıştırın:
   
   * **iOS için**
     
       İçinde `Terminal` penceresinde hello aşağıdakini yürüterek uygulamanızı yeni bir Simulator örneğinde başlatın:
     
           cordova run ios
   * **Android için**
     
       İçinde `Terminal` penceresinde hello aşağıdakini yürüterek uygulamanızı yeni bir öykünücü örneğinde başlatın:
     
           cordova run android
3. Merhaba konsol günlüklerine hello aşağıdakileri görebilirsiniz:
   
        [Engagement] Agent: Session started
        [Engagement] Agent: Activity 'myPage' started
        [Engagement] Connection: Established
        [Engagement] Connection: Sent: appInfo
        [Engagement] Connection: Sent: startSession
        [Engagement] Connection: Sent: activity name='myPage'

## <a id="monitor"></a>Uygulamayı gerçek zamanlı izlemeyle bağlama
[!INCLUDE [Connect app with real-time monitoring](../../includes/mobile-engagement-connect-app-with-monitor.md)]

## <a id="integrate-push"></a>Anında İletme Bildirimlerini ve uygulama içi mesajlaşmayı etkinleştirme
Mobile Engagement anında iletme bildirimleri ve uygulama içi hello Kampanyalar bağlamında Mesajlaşma aracılığıyla kullanıcılarınız ile toointeract sağlar. Bu modül hello Mobile Engagement portalında REACH adı verilir.
Merhaba aşağıdaki bölümlerde, app tooreceive Kurulum bunları.

### <a name="configure-push-credentials-for-mobile-engagement"></a>Mobile Engagement için Gönderim kimlik bilgilerini yapılandırma
sizin adınıza tooallow Mobile Engagement toosend anında iletme bildirimleri, erişim tooyour Apple iOS sertifikanıza veya GCM Server API anahtarını toogrant gerekir. 

1. Tooyour Mobile Engagement portalına gidin. Bu proje için kullanmakta olduğunuz ve üzerinde hello ardından hello uygulamasında olduğunuz sağlamak **Katıl** hello altındaki düğmesi:
   
    ![][1]
2. Engagement Portal'ınızdaki hello ayarları sayfasına gideceksiniz. Merhaba orada tıklayın **yerel gönderim** bölümü:
   
    ![][2]
3. iOS Sertifikasını/GCM Server API Anahtarını yapılandırın
   
    **[iOS]**
   
    a. .p12 sertifikanızı seçin, bunu yükleyip parolanızı yazın:
   
    ![][3]
   
    **[Android]**
   
    a. Merhaba Düzenle simgesine önüne **API anahtarı** hello GCM ayarları bölümünde ve gösteren yukarı hello açılan'de, hello GCM Server anahtarını yapıştırın ve tıklayın **Tamam**. 
   
    ![][4]

### <a name="enable-push-notifications-in-hello-cordova-app"></a>Merhaba Cordova uygulamasında anında iletme bildirimlerini etkinleştirin
Düzen **www/js/index.js** tooadd hello çağrısı tooMobile katılım toorequest anında iletme bildirimleri ve bir işleyici bildirin:

     onDeviceReady: function() {
           Engagement.initializeReach(  
                 // on OpenUrl  
                 function(_url) {   
                 alert(_url);   
                 });  
            Engagement.startActivity("myPage",{});  
        }

### <a name="run-hello-app"></a>Merhaba uygulamayı çalıştırma
**[iOS]**

1. Biz XCode toobuild kullanabilir ve iOS anında iletme bildirimleri tooan gerçek cihaz yalnızca olanak tanıdığından hello aygıt tootest anında iletme bildirimleri hello uygulamasını dağıtabilirsiniz. Cordova projenizin oluşturulduğu toohello konumuna gidin ve çok gidin**...\platforms\ios** konumu. Xcode'da hello yerel .xcodeproj dosyasını açın. 
2. Derleme ve sağlama profili toohello Mobile Engagement portalına ve hello hello oluşturulurken sağlanan eşleşen bir uygulama kimliği yalnızca karşıya hello sertifikayı içeren hello olan hello hesabı kullanarak hello Cordova uygulaması toohello iOS cihazı dağıtma Merhaba Cordova uygulaması. Merhaba denetleyebilirsiniz *paket tanımlayıcısı* içinde **kaynakları\*-info.plist** yukarı dosya XCode toomatch. 
3. Bu hello uygulama belirten aygıtınızda hello standart iOS açılır penceresini izni toosend bildirimleri istekleri görürsünüz. Merhaba izni verin. 

**[Android]**

GCM bildirimleri hello Android öykünücüsünde desteklenen gibi hello öykünücüsü toorun hello Android uygulaması yalnızca kullanabilirsiniz. 

    cordova run android

## <a id="send"></a>Bir bildirim tooyour uygulaması Gönder
Şimdi hello cihazda çalışan bir itme tooyour uygulama gönderecek basit bir anında iletme bildirimi kampanyası oluşturacağız:

1. Toohello gidin **ulaşmak** Mobile Engagement portalınızın sekmesi
2. Tıklatın **Yeni duyuru** toocreate anında iletme kampanyanızı
   
    ![][6]
3. Kampanyanızı girişleri toocreate sağlamak **[Android]**
   
   * Kampanyanıza bir **Ad** verin. 
   * Select hello **teslimat türü** olarak *sistem bildirimi* *basit*
   * Select hello **teslim saati** olarak *"Her zaman"*
   * Sağlayan bir **başlık** hello itme hello ilk satırı olacak bildiriminizin için.
   * Sağlayan bir **ileti** hello ileti gövdesi görevini görecek olan, bildirimi. 
     
     ![][11]
4. Kampanyanızı girişleri toocreate sağlamak **[iOS]**
   
   * Kampanyanıza bir **Ad** verin. 
   * Select hello **teslim saati** olarak *"dışında yalnızca uygulama"*
   * Sağlayan bir **başlık** hello itme hello ilk satırı olacak bildiriminizin için.
   * Sağlayan bir **ileti** hello ileti gövdesi görevini görecek olan, bildirimi. 
     
     ![][12]
5. Aşağı kaydırın ve içerik bölümü hello seçin **yalnızca bildirim**
   
    ![][8]
6. [İsteğe bağlı] Bir Eylem URL'si de sağlayabilirsiniz. Merhaba yapılandırılırken sağlanan bir URL şemasını kullandığından emin olun **AZME\_yeniden yönlendirme\_URL** değişkeni örneğin *myapp://test*.  
7. Ayar hello en temel kampanya olası bitirdiniz. Şimdi kaydırarak yeniden aşağı gidin ve hello tıklatın **oluşturma** toosave kampanyanızı düğmesine tıklayın.
8. Son olarak **Etkinleştir** düğmesine tıklayarak kampanyanızı etkinleştirin
   
    ![][10]
9. Şimdi cihazınızda veya öykünücünüzde bu kampanyanın bir parçası olan bir anında iletme bildirimi görmelisiniz. 

## <a id="next-steps"></a>Sonraki Adımlar
[Cordova Mobile Engagement SDK ile kullanılabilen tüm metotlara genel bakış](https://github.com/Azure/azure-mobile-engagement-cordova)

<!-- Images. -->

[1]: ./media/mobile-engagement-cordova-get-started/engage-button.png
[2]: ./media/mobile-engagement-cordova-get-started/engagement-portal.png
[3]: ./media/mobile-engagement-cordova-get-started/native-push-settings.png
[4]: ./media/mobile-engagement-cordova-get-started/api-key.png
[6]: ./media/mobile-engagement-cordova-get-started/new-announcement.png
[8]: ./media/mobile-engagement-cordova-get-started/campaign-content.png
[10]: ./media/mobile-engagement-cordova-get-started/campaign-activate.png
[11]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-android.png
[12]: ./media/mobile-engagement-cordova-get-started/campaign-first-params-ios.png

