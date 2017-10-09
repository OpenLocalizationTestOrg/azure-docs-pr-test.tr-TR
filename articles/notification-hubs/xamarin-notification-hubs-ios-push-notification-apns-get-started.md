---
title: "Xamarin uygulamaları için Notification Hubs ile anında iletme bildirimleri aaaiOS | Microsoft Docs"
description: "Bu öğreticide, nasıl toouse Azure Notification Hubs toosend anında bildirimleri tooa Xamarin iOS uygulaması öğrenin."
services: notification-hubs
keywords: "ios anında iletme bildirimleri,anında iletme iletileri,anında iletme bildirimleri,anında iletme iletisi"
documentationcenter: xamarin
author: ysxu
manager: erikre
editor: 
ms.assetid: 4d4dfd42-c5a5-4360-9d70-7812f96924d2
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-xamarin-ios
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 8db60338047dd53074b4d3d4bb127aa6d9f13a25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="ios-push-notifications-with-notification-hubs-for-xamarin-apps"></a>Xamarin uygulamaları için Notification Hubs ile iOS Anında İletme Bildirimleri
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Genel Bakış
> [!IMPORTANT]
> toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fpartner-xamarin-notification-hubs-ios-get-started).
> 
> 

Bu öğretici nasıl toouse Azure Notification Hubs toosend anında bildirimleri tooan iOS uygulaması gösterir.
Hello kullanarak anında iletme bildirimleri alan boş bir Xamarin.iOS uygulaması oluşturacaksınız [Apple anında iletilen bildirim servisi (APNs)](https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/APNSOverview.html). Mümkün toouse olacak tamamladığınızda, bildirim hub'ı toobroadcast uygulamanızı çalıştıran bildirimleri tooall hello cihazlar iletin. Merhaba tamamlanmış kod hello kullanılabilir [NotificationHubs uygulaması] [ GitHub] örnek.

Bu öğretici Notification Hubs ile Merhaba basit anında iletme iletisi yayımlama senaryosunu gösterir.

## <a name="prerequisites"></a>Ön koşullar
Bu öğretici hello aşağıdakileri gerektirir:

* [Xcode 6.0][Install Xcode]
* iOS 7.0 (veya sonraki bir sürümü) uyumlu bir cihaz
* iOS Developer Program üyeliği
* [Xamarin Studio]
  
  > [!NOTE]
  > İOS anında iletme bildirimlerinin yapılandırma gereksinimleri nedeniyle dağıtın ve hello benzetici yerine bir fiziksel iOS cihazında (iPhone veya iPad) hello örnek uygulamayı test.
  > 
  > 

Bu öğreticiyi tamamlamak Xamarin iOS uygulamalarına ilişkin diğer tüm Notification Hubs öğreticileri için önkoşuldur.

[!INCLUDE [Notification Hubs Enable Apple Push Notifications](../../includes/notification-hubs-enable-apple-push-notifications.md)]

## <a name="configure-your-notification-hub"></a>Bildirim hub'ınızı yapılandırma
Bu bölümde, yeni bir bildirim hub'ı oluşturma ve hello kullanarak APNS ile kimlik doğrulaması yapılandırma açıklanmaktadır **.p12** oluşturduğunuz bildirim sertifikası. Önceden oluşturduğunuz bir bildirim hub'ı toouse istiyorsanız, toostep 5 atlayabilirsiniz.

[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="7">

<li>

<p>Notification Hub ayarlarınızı, istediğimizden tıklatın hello Azure Portal'ın tooconfigure hello APNS bağlantısını istiyoruz gibi açmak <b>Bildirim Hizmetleri</b>ve ardından hello <b>Apple (APNS)</b> hello listedeki öğesi. Bunu yaptıktan sonra tıklayın <b>sertifikasını karşıya yükle</b> ve select hello <b>.p12</b> hello hello sertifikanın parolasını yanı sıra daha önce verilen sertifika.</p>

<p>Emin tooselect olun <b>korumalı alan</b> itme göndereceğinizden modu geliştirme ortamında iletileri. Yalnızca hello kullan <b>üretim</b> zaten uygulamanızı hello mağazadan satın alan toosend anında iletme bildirimleri toousers isterseniz ayarı.</p>
</li>
</ol>
&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-apns.png)

&emsp;&emsp;![](./media/notification-hubs-ios-get-started/notification-hubs-sandbox.png)

Bildirim hub'ınız şimdi APNS ile yapılandırılmış toowork olan ve hello bağlantı dizeleri tooregister uygulamanızı çalıştırdıktan ve anında iletme bildirimleri göndermek.

## <a name="connect-your-app-toohello-notification-hub"></a>Uygulama toohello bildirim hub'ınıza bağlanın
#### <a name="create-a-new-project"></a>Yeni bir proje oluşturma
1. Xamarin Studio'da yeni bir iOS projesi oluşturun ve seçin hello **Unified API** > **tek görünüm uygulaması** şablonu.
   
     ![Xamarin Studio - Uygulama Türünü Seçme][31]
2. Bir başvuru toohello Azure Mesajlaşma bileşeni ekleyin. Merhaba Hello çözüm görünümü, sağ **bileşenleri** projeniz için klasör ve seçin **daha almak bileşenleri**. Merhaba Ara **Azure Mesajlaşma** bileşeni ve hello bileşen tooyour projeye ekleyin.
3. İçinde **AppDelegate.cs**, hello aşağıdaki ekleme deyimini kullanarak:
   
        using WindowsAzure.Messaging;
4. Bir **SBNotificationHub** örneği bildirin:
   
        private SBNotificationHub Hub { get; set; }
5. Oluşturma bir **Constants.cs** değişkenleri aşağıdaki hello sınıfıyla:
   
        // Azure app-specific connection string and hub path
        public const string ConnectionString = "<Azure connection string>";
        public const string NotificationHubPath = "<Azure hub path>";
6. İçinde **AppDelegate.cs**, güncelleştirme **FinishedLaunching()** toomatch hello aşağıdaki:
   
        public override bool FinishedLaunching(UIApplication application, NSDictionary launchOptions)
        {
            if (UIDevice.CurrentDevice.CheckSystemVersion (8, 0)) {
                var pushSettings = UIUserNotificationSettings.GetSettingsForTypes (
                       UIUserNotificationType.Alert | UIUserNotificationType.Badge | UIUserNotificationType.Sound,
                       new NSSet ());
   
                UIApplication.SharedApplication.RegisterUserNotificationSettings (pushSettings);
                UIApplication.SharedApplication.RegisterForRemoteNotifications ();
            } else {
                UIRemoteNotificationType notificationTypes = UIRemoteNotificationType.Alert | UIRemoteNotificationType.Badge | UIRemoteNotificationType.Sound;
                UIApplication.SharedApplication.RegisterForRemoteNotificationTypes (notificationTypes);
            }
   
            return true;
        }
7. Merhaba geçersiz kılma **Appledelegate.cs** yönteminde **AppDelegate.cs**:
   
        public override void RegisteredForRemoteNotifications(UIApplication application, NSData deviceToken)
        {
            Hub = new SBNotificationHub(Constants.ConnectionString, Constants.NotificationHubPath);
   
            Hub.UnregisterAllAsync (deviceToken, (error) => {
                if (error != null)
                {
                    Console.WriteLine("Error calling Unregister: {0}", error.ToString());
                    return;
                }
   
                NSSet tags = null; // create tags if you want
                Hub.RegisterNativeAsync(deviceToken, tags, (errorCallback) => {
                    if (errorCallback != null)
                        Console.WriteLine("RegisterNativeAsync error: " + errorCallback.ToString());
                });
            });
        }
8. Merhaba geçersiz kılma **Appledelegate.cs** yönteminde **AppDelegate.cs**:
   
        public override void ReceivedRemoteNotification(UIApplication application, NSDictionary userInfo)
        {
            ProcessNotification(userInfo, false);
        }
9. Merhaba aşağıdaki oluşturma **Appledelegate.cs** yönteminde **AppDelegate.cs**:
   
        void ProcessNotification(NSDictionary options, bool fromFinishedLaunching)
        {
            // Check toosee if hello dictionary has hello aps key.  This is hello notification payload you would have sent
            if (null != options && options.ContainsKey(new NSString("aps")))
            {
                //Get hello aps dictionary
                NSDictionary aps = options.ObjectForKey(new NSString("aps")) as NSDictionary;
   
                string alert = string.Empty;
   
                //Extract hello alert text
                // NOTE: If you're using hello simple alert by just specifying
                // "  aps:{alert:"alert msg here"}  ", this will work fine.
                // But if you're using a complex alert with Localization keys, etc.,
                // your "alert" object from hello aps dictionary will be another NSDictionary.
                // Basically hello JSON gets dumped right into a NSDictionary,
                // so keep that in mind.
                if (aps.ContainsKey(new NSString("alert")))
                    alert = (aps [new NSString("alert")] as NSString).ToString();
   
                //If this came from hello ReceivedRemoteNotification while hello app was running,
                // we of course need toomanually process things like hello sound, badge, and alert.
                if (!fromFinishedLaunching)
                {
                    //Manually show an alert
                    if (!string.IsNullOrEmpty(alert))
                    {
                        UIAlertView avAlert = new UIAlertView("Notification", alert, null, "OK", null);
                        avAlert.Show();
                    }
                }
            }
        }
   
   > [!NOTE]
   > Toooverride seçebilirsiniz **FailedToRegisterForRemoteNotifications()** toohandle durumlar gibi ağ bağlantısı yok. Bu burada hello kullanıcı uygulamanızı çevrimdışı modda (örneğin, uçak) başlayabilir ve toohandle itme senaryolarında belirli tooyour uygulama içi mesajlaşmayı istediğiniz özellikle önemlidir.
   > 
   > 
10. Merhaba uygulama Cihazınızda çalıştırın.

## <a name="sending-push-notifications"></a>Anında İletme Bildirimleri Gönderme
Hello bildirimleri göndererek uygulamanızda anında iletme bildirimleri almayı test edebilirsiniz [Azure Portal] hello aracılığıyla **Test gönderimi** hello özelliği **sorun giderme** araç takımı, sağda ekranda hello aşağıda gösterildiği gibi hello bildirim hub'ı sayfasında.

![](./media/notification-hubs-ios-get-started/notification-hubs-test-send.png)

Anında iletme bildirimleri normalde, uyumlu bir kitaplık kullanılarak Mobile Services veya ASP.NET gibi bir arka uç hizmeti aracılığıyla gönderilir. Bir kitaplık senaryonuzda kullanılabilir değilse, toosend anında iletme iletileri doğrudan hello REST API de kullanabilirsiniz. 

Bu öğreticide, biz basit tutmak ve yalnızca arka uç hizmeti yerine bir konsol uygulamasındaki bildirim hub'ları için hello .NET SDK kullanarak bildirim göndererek istemci uygulamanızı test etme gösterin. Merhaba öneririz [Notification Hubs kullanma toopush bildirimleri toousers](notification-hubs-aspnet-backend-ios-apple-apns-notification.md) hello bir ASP.NET arka ucundan bildirim göndermek için sonraki adım olarak Öğreticisi. Ancak, aşağıdaki yaklaşımlardan hello bildirim göndermek için kullanılabilir:

* **REST arabirimi**: hello kullanarak herhangi bir arka uç platformunda anında iletme bildirimi destekleyebilir [REST arabirimini](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).
* **Microsoft Azure Notification Hubs .NET SDK'sı**: hello Visual Studio için Nuget Paket Yöneticisi, çalışması [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).
* **Node.js** : [nasıl toouse node.js'den Notification Hubs](notification-hubs-nodejs-push-notification-tutorial.md).

**Mobile Apps**: bir örneği için Notification Hubs ile tümleştirilmiş Azure App Service Mobile Apps arka uç toosend bildirimleri bkz [Ekle anında iletme bildirimleri tooyour mobil uygulama](../app-service-mobile/app-service-mobile-ios-get-started-push.md).

* **Java / PHP**: REST API'lerini kullanarak toosend anında iletme bildirimleri nasıl hello ilişkin bir örnek için bkz: "nasıl toouse Java/php'den Notification Hubs" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).

#### <a name="optional-send-push-notifications-from-a-net-console-app"></a>(İsteğe bağlı) .NET Konsol Uygulamasından Anında İletme Bildirimleri Gönderme
Bu bölümde, basit bir .NET konsol uygulaması kullanarak anında iletme bildirimleri göndereceğiz. Bu örnek Hello amaçları doğrultusunda, biz Visual Studio'nun zaten yüklü olduğu tooa Windows geliştirme ortamına geçiş yapar.

1. Visual Studio'da yeni bir Visual C# konsol uygulaması oluşturun:
   
       ![Visual Studio - Create a new console application][213]
2. Visual Studio'da **Araçlar**'a, **NuGet Paket Yöneticisi**'ne ve ardından **Paket Yöneticisi Konsolu**'na tıklayın.
   
    Merhaba Paket Yöneticisi konsolu, Visual Studio çalışma alanınızın yerleşik toohello alt görüntülenmesi gerekir.
3. Hello Paket Yöneticisi konsolu penceresinde, hello ayarlamak **varsayılan proje** tooyour yeni konsol uygulama projesi ve sonra hello konsol penceresinde hello aşağıdaki komutu yürütün:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Bu başvuru toohello Azure Notification Hubs SDK'sı ekler hello kullanarak <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet paketini</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. Açık hello `Program.cs` dosya ve hello aşağıdakileri ekleyin `using` deyimi, size Azure sınıflarını ve işlevlerini ana sınıfınız içindeki kullanabilirsiniz sağlama:
   
        using Microsoft.Azure.NotificationHubs;
5. İçinde `Program` sınıfı, yöntem aşağıdaki hello ekleyin (tooreplace hello unutmayın **bağlantı dizesi** ve **hub adı**):
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient.CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var alert = "{\"aps\":{\"alert\":\"Hello from .NET!\"}}";
            await hub.SendAppleNativeNotificationAsync(alert);
        }
6. Hello aşağıdaki satırları ekleyin, `Main` yöntemi:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Merhaba F5 anahtar toorun hello uygulama tuşuna basın. Saniyeler içinde, cihazınızda bir anında iletme bildirimi görüntülendiğini görmeniz gerekir. Wi-Fi veya hücresel veri ağı kullanmanızdan bağımsız hello cihazda etkin bir Internet bağlantısı olduğundan emin olun.

Merhaba Apple hello tüm olası yükleri bulabilirsiniz [yerel ve anında iletilen bildirim Programlama Kılavuzu].

#### <a name="optional-send-notifications-from-a-mobile-service"></a>(İsteğe bağlı) Mobil Hizmetten Bildirim Gönderme
Bu bölümde, bir node betiği aracılığıyla mobil hizmet kullanarak anında iletme bildirimleri göndereceğiz.

bir mobil hizmet kullanarak bildirim toosend izleyin [Mobile Services'i kullanmaya başlama]ve ardından:

1. İçinde toohello oturum [Klasik Azure portalı]ve mobil hizmetinizi seçin.
2. Select hello **Zamanlayıcı** hello üst sekmesinde.
   
       ![Azure Classic Portal - Scheduler][215]
3. Yeni bir zamanlanan iş oluşturun, ad ekleyin ve **İsteğe bağlı**'yı seçin.
   
       ![Azure Classic Portal - Create new job][216]
4. Merhaba iş oluşturulduğunda hello iş adına tıklayın. Merhaba ardından **betik** hello üst çubuğu sekmesinde.
5. Komut dosyası Zamanlayıcı işlevinizin içine aşağıdaki hello ekleyin. Bildirim hub'ı adı ve hello için bağlantı dizenizi emin tooreplace hello yer tutucularını olun *DefaultFullSharedAccessSignature* daha önce edindiğiniz. **Kaydet** düğmesine tıklayın.
   
        var azure = require('azure');
        var notificationHubService = azure.createNotificationHubService('<Hubname>', '<SAS Full access >');
        notificationHubService.apns.send(
            null,
            {"aps":
                {
                  "alert": "Hello from Mobile Services!"
                }
            },
            function (error)
            {
                if (!error) {
                    console.warn("Notification successful");
                }
            }
        );
6. Tıklatın **bir kez çalıştır** hello alt çubuğunda. Cihazınızda bir uyarı almanız gerekir.

## <a name="next-steps"></a>Sonraki adımlar
Bu basit örnekte, iOS cihazlarınıza anında iletme bildirimleri tooall yayımladınız. Buna belirli kullanıcılara tootarget sipariş, toohello öğretici başvurun [Notification Hubs kullanma toopush bildirimleri toousers]. Toosegment kullanıcılarınızı ilgi alanı gruplarına göre isterseniz, okuyabilirsiniz [son dakika haberleri Notification Hubs kullanma toosend]. Hakkında daha fazla bilgi toouse bildirim hub'ları [Notification Hubs Kılavuzu] ve hello [bildirim hub'ları nasıl-toofor iOS].

<!-- Images. -->

[213]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-console-app.png

[215]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler1.png
[216]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-scheduler2.png


[31]: ./media/partner-xamarin-notification-hubs-ios-get-started/notification-hub-create-ios-app.png




<!-- URLs. -->
[Mobile Services iOS SDK]: http://go.microsoft.com/fwLink/?LinkID=266533
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[Mobile Services'i kullanmaya başlama]: /develop/mobile/tutorials/get-started-xamarin-ios
[Klasik Azure portalı]: https://manage.windowsazure.com/
[Notification Hubs Kılavuzu]: http://msdn.microsoft.com/library/jj927170.aspx
[bildirim hub'ları nasıl-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[Install Xcode]: https://go.microsoft.com/fwLink/p/?LinkID=266532
[iOS Provisioning Portal]: http://go.microsoft.com/fwlink/p/?LinkId=272456

[Notification Hubs kullanma toopush bildirimleri toousers]: /manage/services/notification-hubs/notify-users-aspnet
[son dakika haberleri Notification Hubs kullanma toosend]: /manage/services/notification-hubs/breaking-news-dotnet

[yerel ve anında iletilen bildirim Programlama Kılavuzu]:https://developer.apple.com/library/content/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/HandlingRemoteNotifications.html#//apple_ref/doc/uid/TP40008194-CH6-SW1
[Apple Push Notification Service]: http://go.microsoft.com/fwlink/p/?LinkId=272584

[Azure Mobile Services Component]: http://components.xamarin.com/view/azure-mobile-services/
[GitHub]: http://go.microsoft.com/fwlink/p/?LinkId=331329
[Xamarin Studio]: http://xamarin.com/download
[WindowsAzure.Messaging]: https://github.com/infosupport/WindowsAzure.Messaging.iOS
[Azure Portal]: https://portal.azure.com
