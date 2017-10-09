---
title: "Windows Phone üzerinde Azure Notification Hubs ile aaaSending anında iletme bildirimleri | Microsoft Docs"
description: "Bu öğreticide, nasıl toouse Azure Notification Hubs toopush bildirimleri tooa Windows Phone öğrenin 8 veya Windows Phone 8.1 Silverlight uygulaması."
services: notification-hubs
documentationcenter: windows
keywords: "anında iletme bildirimi,anında iletme bildirimi,windows phone anında iletme"
author: ysxu
manager: erikre
editor: erikre
ms.assetid: d872d8dc-4658-4d65-9e71-fa8e34fae96e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 1a0ad238fe7788ae2e4f47f02d113391af03dd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-on-windows-phone"></a>Windows Phone'da Azure Notification Hubs ile anında iletme bildirimleri gönderme
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Genel Bakış
> [!NOTE]
> toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir. Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).
> 
> 

Bu öğretici nasıl toouse Azure Notification Hubs toosend anında bildirimler tooa Windows Phone 8 veya Windows Phone 8.1 Silverlight uygulamasına gösterir. Windows Phone 8.1 (Silverlight olmayan) hedefliyorsanız, toohello başvuran [Windows Evrensel](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) sürümü.
Bu öğreticide, hello Microsoft anında iletme bildirimi Hizmeti'ni (MPNS) kullanarak anında iletme bildirimleri alan boş bir Windows Phone 8 uygulaması oluşturursunuz. Mümkün toouse olacak tamamladığınızda, bildirim hub'ı toobroadcast uygulamanızı çalıştıran bildirimleri tooall hello cihazlar iletin.

> [!NOTE]
> Merhaba Notification Hubs Windows Phone SDK'sı hello Windows anında bildirim hizmeti (WNS) Windows Phone 8.1 Silverlight uygulamaları ile kullanmayı desteklemez. toouse WNS'yi (MPNS) yerine Windows Phone 8.1 Silverlight uygulamaları ile izleyin hello [Notification Hubs - Windows Phone Silverlight Öğreticisi], REST API'lerini kullanır.
> 
> 

Merhaba öğretici Notification Hubs kullanımında hello basit yayın senaryosunu gösterir.

## <a name="prerequisites"></a>Ön koşullar
Bu öğretici hello aşağıdakileri gerektirir:

* [Windows Phone için Visual Studio 2012 Express] veya sonraki bir sürümü.

Bu öğreticiyi tamamlamak Windows Phone 8 uygulamalarına ilişkin diğer tüm Notification Hubs öğreticileri için önkoşuldur.

## <a name="create-your-notification-hub"></a>Bildirim hub'ınızı oluşturma
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p>Hello tıklatın <b>Bildirim Hizmetleri</b> bölümüne (içinde <i>ayarları</i>), tıklayın <b>Windows Phone (MPNS)</b> ve hello ardından <b>kimliği doğrulanmamış gönderimi etkinleştir </b> onay kutusu.</p>
</li>
</ol>

&emsp;&emsp;![Azure Portal - Kimliği doğrulanmamış anında iletme bildirimlerini etkinleştirme](./media/notification-hubs-windows-phone-get-started/azure-portal-unauth.png)

Hub'ınız şimdi kimliği doğrulanmamış oluşturulan ve yapılandırılan toosend Windows Phone için bildirimidir.

> [!NOTE]
> Bu öğretici, MPNS'yi kimlik doğrulamasız modda kullanır. MPNS kimlik doğrulamasız modda tooeach kanal gönderebilirsiniz bildirimlerini sınırlamalarla birlikte gelir. Bildirim hub'ları destekler [MPNS kimlik doğrulamalı mod](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) tooupload sağlayarak sertifikanızı.
> 
> 

## <a name="connecting-your-app-toohello-notification-hub"></a>Uygulama toohello bildirim hub'ınız bağlanma
1. Visual Studio'da yeni bir Windows Phone 8 uygulaması oluşturun.
   
       ![Visual Studio - New Project - Windows Phone App][13]
   
    Visual Studio 2013 Güncelleştirme 2 veya sonrasında, bunun yerine Windows Phone Silverlight uygulaması oluşturursunuz.
   
    ![Visual Studio - Yeni Proje - Boş Uygulama - Windows Phone Silverlight][11]
2. Visual Studio'da hello çözüme sağ tıklayın ve ardından **NuGet paketlerini Yönet**.
   
    Bu hello görüntüler **NuGet paketlerini Yönet** iletişim kutusu.
3. Arama `WindowsAzure.Messaging.Managed` tıklatıp **yükleme**ve hello kullanım koşullarını kabul edin.
   
    ![Visual Studio - NuGet Paket Yöneticisi][20]
   
    Bu indirir, yükler ve bir başvuru toohello Azure Mesajlaşma kitaplığına için Windows hello kullanarak ekler <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet paketini</a>.
4. Merhaba App.xaml.cs dosyasını açın ve hello aşağıdakileri ekleyin `using` deyimleri:
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
5. Merhaba üst kısmındaki koddan hello eklemek **Application_Launching** App.xaml.cs yöntemi:
   
        var channel = HttpNotificationChannel.Find("MyPushChannel");
        if (channel == null)
        {
            channel = new HttpNotificationChannel("MyPushChannel");
            channel.Open();
            channel.BindToShellToast();
        }
   
        channel.ChannelUriUpdated += new EventHandler<NotificationChannelUriEventArgs>(async (o, args) =>
        {
            var hub = new NotificationHub("<hub name>", "<connection string>");
            var result = await hub.RegisterNativeAsync(args.ChannelUri.ToString());
   
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
            {
                MessageBox.Show("Registration :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
            });
        });
   
   > [!NOTE]
   > Merhaba değeri **MyPushChannel** kullanılan toolookup hello içinde var olan bir kanalı olan bir dizini [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) koleksiyonu. Bu koleksiyonda bir tane bulunmuyorsa bu adla yeni bir giriş oluşturun.
   > 
   > 
   
    Hub ve hello bağlantı dizenizi tooinsert hello adı adlı emin olun **DefaultListenSharedAccessSignature** hello önceki bölümde edindiğiniz.
    Bu kod, MPNS'den hello uygulama hello kanal URI'sini alır ve ardından bu kanal URI'sini bildirim hub'ınıza kaydeder. Ayrıca her zaman Merhaba uygulaması başlatıldığında bildirim hub'ınıza URI kayıtlı hello kanal güvence altına alır.
   
   > [!NOTE]
   > Bu öğretici bir bildirim bildirim toohello aygıt gönderir. Bunun yerine bir kutucuk bildirimi gönderdiğinizde, hello çağırmalısınız **BindToShellTile** hello kanalda yöntemi. toosupport bildirim ve kutucuk bildirimlerinin her ikisini de çağrısı **BindToShellTile** ve **BindToShellToast**.
   > 
   > 
6. Çözüm Gezgini'nde genişletin **özellikleri**açın hello `WMAppManifest.xml` dosya, hello tıklatın **yetenekleri** sekmesinde ve o hello emin olun **ıd_cap_push_notıfıcatıon** Yetenek denetlenir.
   
       ![Visual Studio - Windows Phone App Capabilities][14]
   
       This ensures that your app can receive push notifications. Without it, any attempt toosend a push notification toohello app will fail.
7. Tuşuna hello `F5` anahtar toorun hello uygulama.
   
    Merhaba uygulamada bir kayıt iletisi görüntülenir.
8. Kapat hello uygulama.  
   
   > [!NOTE]
   > bildirim biçiminde bir anında iletme bildirimi tooreceive Merhaba uygulaması hello ön planda çalışmıyor olması gerekir.
   > 
   > 

## <a name="send-push-notifications-from-your-backend"></a>Arka ucunuzdan anında iletme bildirimleri gönderme
Bildirim hub'ları kullanarak hello ortak aracılığıyla herhangi bir arka uçtan anında iletme bildirimleri gönderebilirsiniz <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST arabirimini</a>. Bu öğreticide, bir .NET konsol uygulaması kullanarak anında iletme bildirimleri gönderirsiniz. 

Nasıl toosend anında iletme bildirimleri Notification Hubs ile tümleştirilmiş bir ASP.NET Webapı arka ilişkin bir örnek için bkz: [Azure Notification Hubs kullanıcılara bildirme .NET arka ucu ile](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).  

Bir örneği kullanarak toosend anında iletme bildirimleri nasıl hello [REST API'leri](https://msdn.microsoft.com/library/azure/dn223264.aspx), kullanıma [nasıl toouse Java'dan Notification Hubs](notification-hubs-java-push-notification-tutorial.md) ve [nasıl toouse php'den Notification Hubs](notification-hubs-php-push-notification-tutorial.md) .

1. Sağ hello çözüm, select **Ekle** ve **yeni proje...** ve ardından **Visual C#**, tıklatın **Windows** ve **konsol uygulaması**, tıklatıp **Tamam**.
   
       ![Visual Studio - New Project - Console Application][6]
   
    Yeni Visual C# konsol uygulaması toohello çözümü ekler. Bunu ayrı bir çözümde de yapabilirsiniz.
2. **Araçlar**'a, **Kitaplık Paket Yöneticisi**'ne ve ardından **Paket Yöneticisi Konsolu**'na tıklayın.
   
    Merhaba Paket Yöneticisi Konsolu'nu görüntüler.
3. Merhaba, **Paket Yöneticisi Konsolu** penceresinde, kümesi hello **varsayılan proje** tooyour yeni konsol uygulama projesi ve sonra hello konsol penceresinde hello aşağıdaki komutu yürütün:
   
       Install-Package Microsoft.Azure.NotificationHubs
   
   Bu başvuru toohello Azure Notification Hubs SDK'sı ekler hello kullanarak <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet paketini</a>.
4. Açık hello `Program.cs` dosya ve hello aşağıdakileri ekleyin `using` deyimi:
   
        using Microsoft.Azure.NotificationHubs;
5. Merhaba, `Program` sınıfı, yöntem aşağıdaki hello ekleyin:
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            string toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                "<wp:Notification xmlns:wp=\"WPNotification\">" +
                   "<wp:Toast>" +
                        "<wp:Text1>Hello from a .NET App!</wp:Text1>" +
                   "</wp:Toast> " +
                "</wp:Notification>";
            await hub.SendMpnsNativeNotificationAsync(toast);
        }
   
    Tooreplace hello emin olun `<hub name>` yer tutucu hello Portalı'nda görüntülenen hello bildirim hub'ı hello adı. Ayrıca, hello bağlantı dizesi yer tutucusunu adlı hello bağlantı dizesi ile değiştirin **DefaultFullSharedAccessSignature** "bildirim hub'ınızı yapılandırma" Merhaba bölümünde edindiğiniz
   
   > [!NOTE]
   > Merhaba bağlantı dizesiyle kullandığınızdan emin olun **tam** erişimi ile değil, **dinleme** erişim. Merhaba dinleme erişimi dizesinin izinleri toosend anında iletme bildirimleri yok.
   > 
   > 
6. Satırda aşağıdaki hello eklemek, `Main` yöntemi:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Windows Phone ile çalışan öykünücüsü ve uygulama kapalı, ayarlanmış hello konsol uygulama projesi hello olarak varsayılan başlangıç projesi ve hello tuşuna basın `F5` anahtar toorun hello uygulama.
   
    Bildirim biçiminde bir anında iletme bildirimi alırsınız. Merhaba bildirim başlığına dokunmak hello uygulamayı yükler.

Hello hello tüm olası yükleri bulabilirsiniz [bildirim Kataloğu] ve [kutucuk Kataloğu] MSDN'de Konular.

## <a name="next-steps"></a>Sonraki adımlar
Bu basit örnekte, Windows Phone 8 aygıtları anında iletme bildirimleri tooall yayımladınız. 

Buna belirli kullanıcılara tootarget sipariş, toohello başvurmak [Notification Hubs kullanma toopush bildirimleri toousers] Öğreticisi. 

Toosegment kullanıcılarınızı ilgi alanı gruplarına göre isterseniz, okuyabilirsiniz [son dakika haberleri Notification Hubs kullanma toosend]. 

Hakkında daha fazla bilgi toouse bildirim hub'ları [Notification Hubs Kılavuzu].

<!-- Images. -->
[6]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png
[7]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal.png
[8]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal2.png
[9]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal.png
[10]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal2.png
[11]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-silverlight-app.png
[12]: ./media/notification-hubs-windows-phone-get-started/notification-hub-connection-strings.png

[13]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-app.png
[14]: ./media/notification-hubs-windows-phone-get-started/mobile-app-enable-push-wp8.png
[15]: ./media/notification-hubs-windows-phone-get-started/notification-hub-pushauth.png
[20]: ./media/notification-hubs-windows-phone-get-started/notification-hub-windows-universal-app-install-package.png
[213]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png





<!-- URLs. -->
[Windows Phone için Visual Studio 2012 Express]: https://go.microsoft.com/fwLink/p/?LinkID=268374
[Notification Hubs Kılavuzu]: http://msdn.microsoft.com/library/jj927170.aspx
[MPNS authenticated mode]: http://msdn.microsoft.com/library/windowsphone/develop/ff941099(v=vs.105).aspx
[Notification Hubs kullanma toopush bildirimleri toousers]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[son dakika haberleri Notification Hubs kullanma toosend]: notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md
[bildirim Kataloğu]: http://msdn.microsoft.com/library/windowsphone/develop/jj662938(v=vs.105).aspx
[kutucuk Kataloğu]: http://msdn.microsoft.com/library/windowsphone/develop/hh202948(v=vs.105).aspx
[Notification Hubs - Windows Phone Silverlight Öğreticisi]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSLPhoneApp

