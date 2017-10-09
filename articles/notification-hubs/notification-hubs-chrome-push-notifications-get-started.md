---
title: "Azure Notification Hubs ile aaaSend anında iletme bildirimleri tooChrome uygulamaları | Microsoft Docs"
description: "Nasıl toouse Azure Notification Hubs toosend anında bildirimler tooa Chrome uygulaması hakkında bilgi edinin."
services: notification-hubs
keywords: "mobil anında iletme bildirimleri,anında iletme bildirimleri,anında iletme bildirimi,chrome anında iletme bildirimleri"
documentationcenter: 
author: ysxu
manager: erikre
editor: 
ms.assetid: 75d4ff59-d04a-455f-bd44-0130a68e641f
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-chrome
ms.devlang: JavaScript
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 7dec8ab02622563bc3730a2e96820da8932d22f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="send-push-notifications-toochrome-apps-with-azure-notification-hubs"></a>Anında iletme bildirimleri tooChrome uygulamaları Azure Notification Hubs ile gönderme
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

Bu konuda nasıl toouse Azure Notification Hubs toosend anında bildirimler tooa hello hello Google Chrome tarayıcısı bağlamında görüntülenen Chrome uygulaması gösterilmektedir. Bu öğreticide, [Google Cloud Messaging (GCM)](https://developers.google.com/cloud-messaging/) kullanarak anında iletme bildirimleri alan bir Chrome uygulaması oluşturacağız. 

> [!NOTE]
> toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%notification-hubs-chrome-get-started%2F).
> 
> 

Merhaba öğreticide şu temel adımlarda tooenable anında iletme bildirimleri açıklanmaktadır:

* [Google Cloud Messaging'i etkinleştirme](#register)
* [Bildirim hub'ınızı yapılandırma](#configure-hub)
* [Chrome uygulaması toohello bildirim hub'ınıza bağlanın](#connect-app)
* [Anında iletme bildirimi tooyour Chrome uygulaması Gönder](#send)
* [Ek işlevler ve özellikler](#next-steps)

> [!NOTE]
> Chrome uygulaması anında iletme bildirimleri genel tarayıcı içi bildirimler olmayan - belirli toohello tarayıcı genişletilebilirlik modeli vardır (bkz [Chrome uygulamalarına genel bakış] Ayrıntılar için). Ayrıca Chrome uygulamaları toohello Masaüstü tarayıcısı, Apache Cordova aracılığıyla mobil (Android ve iOS) çalıştırın. Bkz: [mobil cihazlarda Chrome uygulamaları] toolearn daha fazla.
> 
> 

GCM ve Azure Notification Hubs yapılandırma olan Android için aynı tooconfiguring beri [Google Cloud Messaging for Chrome] kullanım dışı bırakıldı ve aynı GCM hello artık Android cihazları hem Chrome örneklerini destekler.

## <a id="register"></a>Google Cloud Messaging'i etkinleştirme
1. Toohello gidin [Google Cloud Console] Web sitesi, Google hesabı kimlik bilgilerinizle oturum açın ve hello ardından **proje oluştur** düğmesi. Uygun bir sağlamak **proje adı**ve ardından hello **oluşturma** düğmesi.
   
       ![Google Cloud Console - Create Project][1]
2. Merhaba Not **proje numarası** hello üzerinde **projeleri** oluşturduğunuz hello projesi için sayfa. Bu hello kullanacağınız **GCM Gönderen Kimliği** hello Chrome uygulaması tooregister GCM ile içinde.
   
       ![Google Cloud Console - Project Number][2]
3. Merhaba sol bölmede **API'leri & auth**ve ardından aşağı kaydırın ve hello geçiş tooenable tıklatın **Google Cloud Messaging for Android**. Tooenable yok **Google Cloud Messaging for Chrome**.
   
       ![Google Cloud Console - Server Key][3]
4. Merhaba sol bölmede **kimlik bilgileri** > **yeni anahtarı oluştur** > **sunucu anahtarı** > **oluşturma**.
   
       ![Google Cloud Console - Credentials][4]
5. Merhaba sunucu Not **API anahtarı**. Bu, bildirim hub'ı İleri tooenable yapılandırır, toosend anında iletme bildirimleri tooGCM.
   
       ![Google Cloud Console - API Key][5]

## <a id="configure-hub"></a>Bildirim hub'ınızı yapılandırma
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

&emsp;&emsp;6.   Merhaba, **ayarları** dikey penceresinde, select **Bildirim Hizmetleri** ve ardından **Google (GCM)**. Merhaba API anahtarını girin ve kaydedin.

&emsp;&emsp;![Azure Notification Hubs - Google (GCM)](./media/notification-hubs-android-get-started/notification-hubs-gcm-api.png)

## <a id="connect-app"></a>Chrome uygulaması toohello bildirim hub'ınıza bağlanın
Bildirim hub'ınız şimdi GCM ile yapılandırılmış toowork olduğu ve uygulama tooboth anında iletme bildirimleri göndermenizi ve hello bağlantı dizeleri tooregister sahip. LK

### <a name="create-a-new-chrome-app"></a>Yeni bir Chrome Uygulaması oluşturma
Aşağıdaki Hello örneği üzerinde hello temel [Chrome uygulaması GCM örneği] ve kullandığı hello bir Chrome uygulaması şekilde toocreate önerilir. Biz hello adımları özellikle ilgili tooAzure bildirim hub'ları vurgular. 

> [!NOTE]
> Bu Chrome uygulamasının hello kaynak karşıdan öneririz [Chrome uygulaması bildirim hub'ı örneği].
> 
> 

Merhaba Chrome uygulaması JavaScript aracılığıyla oluşturulur ve oluşturmak için tercih edilen sözcük düzenleyicisini birini kullanabilirsiniz. Aşağıda, bu Chrome Uygulamasının nasıl görüneceği gösterilmektedir.

![Google Chrome Uygulaması][15]

1. Bir klasör oluşturun ve `ChromePushApp` olarak adlandırın. Elbette, hello rastgele bir addır - farklı bir ad kullanırsanız hello hello gerekli kod kesimlerinde yolu değiştirdiğinizden emin olun.
2. Merhaba karşıdan [crypto-js Kitaplığı] hello ikinci adımda oluşturduğunuz hello klasöründeki. Bu kitaplık klasörü iki alt klasör içerir: `components` ve `rollups`.
3. Bir `manifest.json` dosyası oluşturun. Tüm Chrome uygulamaları hello uygulama meta verilerini ve en içeren bir bildirim dosyası tarafından yedeklenen hello kullanıcı yüklediğinde toohello uygulama verilen önemlisi, tüm izinleri.
   
        {
          "name": "NH-GCM Notifications",
          "description": "Chrome platform app.",
          "manifest_version": 2,
          "version": "0.1",
          "app": {
            "background": {
              "scripts": ["background.js"]
            }
          },
          "permissions": ["gcm", "storage", "notifications", "https://*.servicebus.windows.net/*"],
          "icons": { "128": "gcm_128.png" }
        }
   
    Bildirim hello `permissions` bu Chrome uygulaması GCM mümkün tooreceive anında iletme bildirimleri olacağını belirten öğesi. Ayrıca hello Azure bildirim hub'ları hello Chrome uygulaması REST çağrısı tooregister burada yapacak URI belirtmeniz gerekir.
    Bizim örnek uygulamamız da bir simge dosyası kullanan `gcm_128.png`, hello özgün GCM örneğinden yeniden kullanılan hello kaynaktaki bulacaksınız. Merhaba uygun herhangi bir görüntü için alternatif [simge ölçütleri](https://developer.chrome.com/apps/manifest/icons).
4. Adlı bir dosya oluşturun `background.js` koddan hello ile:
   
        // Returns a new notification ID used in hello notification.
        function getNotificationId() {
          var id = Math.floor(Math.random() * 9007199254740992) + 1;
          return id.toString();
        }
   
        function messageReceived(message) {
          // A message is an object with a data property that
          // consists of key-value pairs.
   
          // Concatenate all key-value pairs tooform a display string.
          var messageString = "";
          for (var key in message.data) {
            if (messageString != "")
              messageString += ", "
            messageString += key + ":" + message.data[key];
          }
          console.log("Message received: " + messageString);
   
          // Pop up a notification tooshow hello GCM message.
          chrome.notifications.create(getNotificationId(), {
            title: 'GCM Message',
            iconUrl: 'gcm_128.png',
            type: 'basic',
            message: messageString
          }, function() {});
        }
   
        var registerWindowCreated = false;
   
        function firstTimeRegistration() {
          chrome.storage.local.get("registered", function(result) {
   
            registerWindowCreated = true;
            chrome.app.window.create(
              "register.html",
              {  width: 520,
                 height: 500,
                 frame: 'chrome'
              },
              function(appWin) {}
            );
          });
        }
   
        // Set up a listener for GCM message event.
        chrome.gcm.onMessage.addListener(messageReceived);
   
        // Set up listeners tootrigger hello first-time registration.
        chrome.runtime.onInstalled.addListener(firstTimeRegistration);
        chrome.runtime.onStartup.addListener(firstTimeRegistration);
   
    Bu, hello Chrome uygulama penceresi HTML'sini hello dosyasıdır (**register.html**) ve ayrıca hello işleyicisini tanımlar **messageReceived** toohandle hello gelen anında iletme bildirimi.
5. Adlı bir dosya oluşturun `register.html` -bu hello hello Chrome uygulamasının kullanıcı arabirimini tanımlar. 
   
   > [!NOTE]
   > Bu örnekte **CryptoJS v3.1.2** kullanılır. Merhaba kitaplığının başka bir sürümünü yüklediyseniz, hello hello sürümünde düzgün şekilde değiştirdiğinizden emin olun `src` yolu.
   > 
   > 
   
        <html>
   
        <head>
        <title>GCM Registration</title>
        <script src="register.js"></script>
        <script src="CryptoJS v3.1.2/rollups/hmac-sha256.js"></script>
        <script src="CryptoJS v3.1.2/components/enc-base64-min.js"></script>
        </head>
   
        <body>
   
        Sender ID:<br/><input id="senderId" type="TEXT" size="20"><br/>
        <button id="registerWithGCM">Register with GCM</button>
        <br/>
        <br/>
        <br/>
   
        Notification Hub Name:<br/><input id="hubName" type="TEXT" style="width:400px"><br/><br/>
        Connection String:<br/><textarea id="connectionString" type="TEXT" style="width:400px;height:60px"></textarea>
   
        <br/>
   
        <button id="registerWithNH" disabled="true">Register with Azure Notification Hubs</button>
   
        <br/>
        <br/>
   
        <textarea id="console" type="TEXT" readonly style="width:500px;height:200px;background-color:#e5e5e5;padding:5px"></textarea>
   
        </body>
   
        </html>
6. Adlı bir dosya oluşturun `register.js` hello kodu aşağıdaki ile. Bu dosyanın arkasındaki hello betiği belirtir `register.html`. Toocreate Arabiriminiz için ayrı bir destek betiği alacak şekilde chrome uygulamaları satır içi yürütmeye izin vermez.
   
        var registrationId = "";
        var hubName        = "", connectionString = "";
        var originalUri    = "", targetUri = "", endpoint = "", sasKeyName = "", sasKeyValue = "", sasToken = "";
   
        window.onload = function() {
           document.getElementById("registerWithGCM").onclick = registerWithGCM;  
           document.getElementById("registerWithNH").onclick = registerWithNH;
           updateLog("You have not registered yet. Please provider sender ID and register with GCM and then with  Notification Hubs.");
        }
   
        function updateLog(status) {
          currentStatus = document.getElementById("console").innerHTML;
          if (currentStatus != "") {
            currentStatus = currentStatus + "\n\n";
          }
   
          document.getElementById("console").innerHTML = currentStatus  + status;
        }
   
        function registerWithGCM() {
          var senderId = document.getElementById("senderId").value.trim();
          chrome.gcm.register([senderId], registerCallback);
   
          // Prevent register button from being clicked again before hello registration finishes.
          document.getElementById("registerWithGCM").disabled = true;
        }
   
        function registerCallback(regId) {
          registrationId = regId;
          document.getElementById("registerWithGCM").disabled = false;
   
          if (chrome.runtime.lastError) {
            // When hello registration fails, handle hello error and retry the
            // registration later.
            updateLog("Registration failed: " + chrome.runtime.lastError.message);
            return;
          }
   
          updateLog("Registration with GCM succeeded.");
          document.getElementById("registerWithNH").disabled = false;
   
          // Mark that hello first-time registration is done.
          chrome.storage.local.set({registered: true});
        }
   
        function registerWithNH() {
          hubName = document.getElementById("hubName").value.trim();
          connectionString = document.getElementById("connectionString").value.trim();
          splitConnectionString();
          generateSaSToken();
          sendNHRegistrationRequest();
        }
   
        // From http://msdn.microsoft.com/library/dn495627.aspx
        function splitConnectionString()
        {
          var parts = connectionString.split(';');
          if (parts.length != 3)
          throw "Error parsing connection string";
   
          parts.forEach(function(part) {
            if (part.indexOf('Endpoint') == 0) {
            endpoint = 'https' + part.substring(11);
            } else if (part.indexOf('SharedAccessKeyName') == 0) {
            sasKeyName = part.substring(20);
            } else if (part.indexOf('SharedAccessKey') == 0) {
            sasKeyValue = part.substring(16);
            }
          });
   
          originalUri = endpoint + hubName;
        }
   
        function generateSaSToken()
        {
          targetUri = encodeURIComponent(originalUri.toLowerCase()).toLowerCase();
          var expiresInMins = 10; // 10 minute expiration
   
          // Set expiration in seconds.
          var expireOnDate = new Date();
          expireOnDate.setMinutes(expireOnDate.getMinutes() + expiresInMins);
          var expires = Date.UTC(expireOnDate.getUTCFullYear(), expireOnDate
            .getUTCMonth(), expireOnDate.getUTCDate(), expireOnDate
            .getUTCHours(), expireOnDate.getUTCMinutes(), expireOnDate
            .getUTCSeconds()) / 1000;
          var tosign = targetUri + '\n' + expires;
   
          // Using CryptoJS.
          var signature = CryptoJS.HmacSHA256(tosign, sasKeyValue);
          var base64signature = signature.toString(CryptoJS.enc.Base64);
          var base64UriEncoded = encodeURIComponent(base64signature);
   
          // Construct authorization string.
          sasToken = "SharedAccessSignature sr=" + targetUri + "&sig="
                          + base64UriEncoded + "&se=" + expires + "&skn=" + sasKeyName;
        }
   
        function sendNHRegistrationRequest()
        {
          var registrationPayload =
          "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
          "<entry xmlns=\"http://www.w3.org/2005/Atom\">" +
              "<content type=\"application/xml\">" +
                  "<GcmRegistrationDescription xmlns:i=\"http://www.w3.org/2001/XMLSchema-instance\" xmlns=\"http://schemas.microsoft.com/netservices/2010/10/servicebus/connect\">" +
                      "<GcmRegistrationId>{GCMRegistrationId}</GcmRegistrationId>" +
                  "</GcmRegistrationDescription>" +
              "</content>" +
          "</entry>";
   
          // Update hello payload with hello registration ID obtained earlier.
          registrationPayload = registrationPayload.replace("{GCMRegistrationId}", registrationId);
   
          var url = originalUri + "/registrations/?api-version=2014-09";
          var client = new XMLHttpRequest();
   
          client.onload = function () {
            if (client.readyState == 4) {
              if (client.status == 200) {
                updateLog("Notification Hub Registration succesful!");
                updateLog(client.responseText);
              } else {
                updateLog("Notification Hub Registration did not succeed!");
                updateLog("HTTP Status: " + client.status + " : " + client.statusText);
                updateLog("HTTP Response: " + "\n" + client.responseText);
              }
            }
          };
   
          client.onerror = function () {
                updateLog("ERROR - Notification Hub Registration did not succeed!");
          }
   
          client.open("POST", url, true);
          client.setRequestHeader("Content-Type", "application/atom+xml;type=entry;charset=utf-8");
          client.setRequestHeader("Authorization", sasToken);
          client.setRequestHeader("x-ms-version", "2014-09");
   
          try {
              client.send(registrationPayload);
          }
          catch(err) {
              updateLog(err.message);
          }
        }
   
    betik yukarıdaki Hello anahtar parametreleri aşağıdaki hello sahiptir:
   
   * **Window.onLoad** UI hello üzerinde hello iki düğmelerinin hello düğme tıklama olaylarını tanımlar. Biri GCM'ye kaydedilir ve diğer hello Azure Notification Hubs ile GCM tooregister kaydı sonra döndürülen hello kayıt Kimliğini kullanır.
   * **updateLog** toohandle basit günlüğe kaydetme özelliklerini tanır hello işlevdir.
   * **registerWithGCM** hello kılan hello ilk düğme tıklama işleyicisidir `chrome.gcm.register` çağrısı tooGCM tooregister hello geçerli Chrome uygulaması örneğini.
   * **registerCallback** hello GCM kayıt çağrısı döndürüldüğünde çağrılan hello geri çağırma işlevi.
   * **registerWithNH** , Notification hubs'a hello ikinci düğme tıklama işleyicisidir. Alır `hubName` ve `connectionString` (Merhaba kullanıcının belirttiği) ve el becerisi gerektiren işler hello Notification Hubs kayıt REST API çağrısı.
   * **splitConnectionString** ve **generateSaSToken** hello tüm REST API çağrılarında kullanılan bir SaS belirteci oluşturma işleminin JavaScript uygulamasını temsil eden yardımcılardır. Daha fazla bilgi için bkz. [Ortak Kavramlar](http://msdn.microsoft.com/library/dn495627.aspx).
   * **sendNHRegistrationRequest** HTTP REST yapar hello işlevi çağırmak tooAzure bildirim hub'ları.
   * **registrationPayload** hello kayıt XML yükünü tanımlar. Daha fazla bilgi için bkz. [Kayıt NH REST API’si oluşturma]. Ne GCM'den aldık ile Merhaba kayıt Kimliğini güncelleştiriyoruz.
   * **İstemci** örneği **XMLHttpRequest** toomake hello HTTP POST isteği kullanırız. Merhaba güncelleştiriyoruz Not `Authorization` üstbilgiyle `sasToken`. Bu çağrının başarıyla tamamlanması, bu Chrome Uygulaması örneğinin Azure Notification Hubs'a kaydedilmesini sağlar.

Merhaba bu proje için genel klasör yapısı şuna benzemelidir: ![Google Chrome uygulaması - klasör yapısı][21]

### <a name="set-up-and-test-your-chrome-app"></a>Chrome Uygulamanızı ayarlama ve test etme
1. Chrome tarayıcınızı açın. **Chrome uzantıları**'nı açın ve **Geliştirici modunu** etkinleştirin.
   
       ![Google Chrome - Enable Developer Mode][16]
2. Tıklatın **paketi açılmış uzantı Yükle** ve hello dosyaları oluşturulduğu toohello klasörüne gidin. Merhaba Ayrıca isteğe bağlı olarak kullanabileceğiniz **Chrome Apps & Extensions Developer aracı**. Bu araç kendi (Merhaba Chrome Web Mağazası ' yüklenir) içinde bir Chrome uygulaması ve Chrome uygulaması geliştirmeniz için Gelişmiş hata ayıklama özellikleri sağlar.
   
       ![Google Chrome - Load Unpacked Extension][17]
3. Ardından Hello Chrome uygulaması hatasız oluşturduysanız görünmesini Chrome uygulamanızı görürsünüz.
   
       ![Google Chrome - Chrome App Display][18]
4. Hello girin **proje numarası** daha önce hello aldığınız **Google Cloud Console** tıklatın ve hello Gönderen Kimliği olarak **GCM ile kayıt**. Selamlama iletisine görmesi gereken **başarılı GCM ile kayıt.**
   
       ![Google Chrome - Chrome App Customization][19]
5. Girin, **bildirim hub'ı adı** ve hello **DefaultListenSharedAccessSignature** önceki hello portal ve tıklatın Elde **Azure Notification Hubkaydetme**. Selamlama iletisine görmesi gereken **bildirim hub'ı kaydı başarılı!** ve hello hello Azure Notification Hubs kayıt içeren hello kayıt yanıtının ayrıntılarını kimliği
   
       ![Google Chrome - Specify Notification Hub Details][20]  

## <a name="send"></a>Bildirim tooyour Chrome uygulaması Gönder
Test amacıyla, bir .NET konsol uygulaması kullanarak size Chrome anında iletme bildirimleri göndereceğiz. 

> [!NOTE]
> Notification Hubs ile Ortak <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST arabirimimizi</a> kullanarak herhangi bir arka uçtan anında iletme bildirimleri gönderebilirsiniz. Daha fazla platformlar arası örnek için [belge portalımıza](https://azure.microsoft.com/documentation/services/notification-hubs/) göz atın.
> 
> 

1. Merhaba gelen Visual Studio **dosya** menüsünde, select **yeni** ve ardından **proje**. **Visual C#** altında, **Windows** ve **Konsol Uygulaması**'na, ardından **Tamam**'a tıklayın.  Bu, yeni bir konsol uygulama projesi oluşturur.
2. Merhaba gelen **Araçları** menüsünde tıklatın **kitaplık Paket Yöneticisi** ve ardından **Paket Yöneticisi Konsolu**. Merhaba Paket Yöneticisi Konsolu'nu görüntüler.
3. Merhaba konsol penceresinde hello aşağıdaki komutu yürütün:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
       This adds a reference toohello Azure Service Bus SDK with hello <a href="http://nuget.org/packages/  WindowsAzure.ServiceBus/">WindowsAzure.ServiceBus NuGet package</a>.
4. Açık `Program.cs` ve hello aşağıdakileri ekleyin `using` deyimi:
   
        using Microsoft.Azure.NotificationHubs;
5. Merhaba, `Program` sınıfı, yöntem aşağıdaki hello ekleyin:
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            String message = "{\"data\":{\"message\":\"Hello Chrome from Azure Notification Hubs\"}}";
            await hub.SendGcmNativeNotificationAsync(message);
        }
   
       Make sure tooreplace hello `<hub name>` placeholder with hello name of hello notification hub that appears in hello [portal](https://portal.azure.com) in your Notification Hub blade. Also, replace hello connection string placeholder with hello connection string called `DefaultFullSharedAccessSignature` that you obtained in hello notification hub configuration section.
   
   > [!NOTE]
   > Merhaba bağlantı dizesiyle kullandığınızdan emin olun **tam** erişimi ile değil, **dinleme** erişim. Merhaba **dinleme** erişim bağlantı dizesi toosend anında iletme bildirimleri izinleri vermez.
   > 
   > 
6. Merhaba aşağıdaki çağırır hello eklemek `Main` yöntemi:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Chrome'un çalıştığından emin olun ve hello konsol uygulamasını çalıştırın.
8. Merhaba aşağıdaki görmelisiniz bildirim masaüstünüzde açılır.
   
       ![Google Chrome - Notification][13]
9. Hello Chrome Bildirimler penceresinde hello görev çubuğunda (Windows'ta) kullanarak da tüm bildirimlerinizi görebilirsiniz Chrome çalışırken.
   
       ![Google Chrome - Notifications List][14]

> [!NOTE]
> (Merhaba Chrome tarayıcısının çalışıyor olması gerekir rağmen) çalışan veya hello tarayıcıda aç toohave hello Chrome uygulaması gerekmez. Ayrıca tüm bildirimlerinizi birleştirilmiş bir görünüm hello Chrome Bildirimler penceresinde elde edersiniz.
> 
> 

## <a name="next-steps"> </a>Sonraki adımlar
[Notification Hubs'a Genel Bakış]'ta Notification Hubs hakkında daha fazla bilgi edinin.

tootarget belirli kullanıcılar, başvuran toohello [Azure Notification Hubs kullanıcılara bildirme] Öğreticisi. 

Kullanıcılarınızı ilgi alanı gruplarına göre toosegment istiyorsanız hello izleyebilirsiniz [Azure Notification Hubs son dakika haberleri] Öğreticisi.

<!-- Images. -->
[1]: ./media/notification-hubs-chrome-get-started/GoogleConsoleCreateProject.PNG
[2]: ./media/notification-hubs-chrome-get-started/GoogleProjectNumber.png
[3]: ./media/notification-hubs-chrome-get-started/EnableGCM.png
[4]: ./media/notification-hubs-chrome-get-started/CreateServerKey.png
[5]: ./media/notification-hubs-chrome-get-started/ServerKey.png
[6]: ./media/notification-hubs-chrome-get-started/CreateNH.png
[7]: ./media/notification-hubs-chrome-get-started/NHNamespace.png
[8]: ./media/notification-hubs-chrome-get-started/NamespaceConfigure.png
[9]: ./media/notification-hubs-chrome-get-started/NHConfigure.png
[10]: ./media/notification-hubs-chrome-get-started/NHConfigureGCM.png
[11]: ./media/notification-hubs-chrome-get-started/NHDashboard.png
[12]: ./media/notification-hubs-chrome-get-started/NHConnString.png
[13]: ./media/notification-hubs-chrome-get-started/ChromeNotification.png
[14]: ./media/notification-hubs-chrome-get-started/ChromeNotificationWindow.png
[15]: ./media/notification-hubs-chrome-get-started/ChromeApp.png
[16]: ./media/notification-hubs-chrome-get-started/ChromeExtensions.png
[17]: ./media/notification-hubs-chrome-get-started/ChromeLoadExtension.png
[18]: ./media/notification-hubs-chrome-get-started/ChromeAppLoaded.png
[19]: ./media/notification-hubs-chrome-get-started/ChromeAppGCM.png
[20]: ./media/notification-hubs-chrome-get-started/ChromeAppNH.png
[21]: ./media/notification-hubs-chrome-get-started/FinalFolderView.png

<!-- URLs. -->
[Chrome uygulaması bildirim hub'ı örneği]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToChromeApps
[Google Cloud Console]: http://cloud.google.com/console
[Azure Classic Portal]: https://manage.windowsazure.com/
[Notification Hubs'a Genel Bakış]: notification-hubs-push-notification-overview.md
[Chrome uygulamalarına genel bakış]: https://developer.chrome.com/apps/about_apps
[Chrome uygulaması GCM örneği]: https://github.com/GoogleChrome/chrome-app-samples/tree/master/samples/gcm-notifications
[Installable Web Apps]: https://developers.google.com/chrome/apps/docs/
[mobil cihazlarda Chrome uygulamaları]: https://developer.chrome.com/apps/chrome_apps_on_mobile
[Kayıt NH REST API’si oluşturma]: http://msdn.microsoft.com/library/azure/dn223265.aspx
[crypto-js Kitaplığı]: http://code.google.com/p/crypto-js/
[GCM with Chrome Apps]: https://developer.chrome.com/apps/cloudMessaging
[Google Cloud Messaging for Chrome]: https://developer.chrome.com/apps/cloudMessagingV1
[Azure Notification Hubs kullanıcılara bildirme]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[Azure Notification Hubs son dakika haberleri]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
