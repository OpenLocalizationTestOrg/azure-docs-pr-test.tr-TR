---
title: "aaaGet Azure uygulamaları için Notification Hubs Windows Evrensel Platform ile başlatılan | Microsoft Docs"
description: "Bu öğreticide, bilgi nasıl toouse Azure Notification Hubs toopush bildirimleri tooa Evrensel Windows Platform uygulaması."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: erikre
ms.assetid: cf307cf3-8c58-4628-9c63-8751e6a0ef43
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 11056842d205522ed493dc61c76ecf78ebb5a363
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-notification-hubs-for-windows-universal-platform-apps"></a>Windows Evrensel Platform Uygulamaları için Notification Hubs'ı kullanmaya başlama
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a>Genel Bakış
Bu öğretici nasıl toouse Azure Notification Hubs toosend anında bildirimler tooa Evrensel Windows Platformu (UWP) uygulamasını gösterir.

Bu öğreticide, hello Windows anında bildirim Hizmeti'ni (WNS) kullanarak anında iletme bildirimleri alan boş bir Windows mağazası uygulaması oluşturursunuz. Mümkün toouse olacak tamamladığınızda, bildirim hub'ı toobroadcast uygulamanızı çalıştıran bildirimleri tooall hello cihazlar iletin.

## <a name="before-you-begin"></a>Başlamadan önce
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

Bu öğreticinin hello tamamlanan kodu Github'da bulunabilir [burada](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).

## <a name="prerequisites"></a>Ön koşullar
Bu öğretici hello aşağıdakileri gerektirir:

* [Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) veya üstü
* [Evrensel Windows Uygulama Geliştirme Araçları'nın yüklü olması](https://msdn.microsoft.com/windows/uwp/get-started/get-set-up)
* Etkin bir Azure hesabı <br/>Hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz. Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).
* Etkin bir Windows Mağazası hesabı

Bu öğreticinin tamamlanması Windows Evrensel Platform uygulamalarına ilişkin diğer tüm Notification Hubs öğreticileri için önkoşuldur.

## <a name="register-your-app-for-hello-windows-store"></a>Merhaba Windows mağazası için uygulamanızı kaydetme
toosend anında iletme bildirimleri tooUWP uygulamalar, uygulama toohello Windows mağazası ilişkilendirmeniz gerekir. Ardından, bildirim hub'ı toointegrate WNS ile yapılandırmanız gerekir.

1. Uygulamanızı zaten kaydolmadıysanız toohello gidin [Windows Geliştirme Merkezi](https://dev.windows.com/overview), Microsoft hesabınızla oturum açın ve ardından **yeni uygulama oluştur**.

2. Uygulamanız için bir ad yazın ve **Uygulama adını ayır**'a tıklayın. Bu, uygulamanız için yeni bir Windows Mağazası kaydı oluşturur.

3. Windows Evrensel hello kullanarak Visual Studio'da yeni bir Visual C# mağaza uygulamaları projesi oluşturma **boş uygulama** şablonu ve tıklatın **Tamam**.

4. Merhaba hedef ve minimum platform sürümleri için Hello Varsayılanları kabul edin.

5. Çözüm Gezgini'nde, hello Windows mağazası uygulama projesine sağ tıklayın, tıklatın **deposu**ve ardından **uygulamayı hello mağaza ile ilişkilendir...** . hello **uygulamanızı hello Windows mağazası ile ilişkilendirin** Sihirbazı görünür.

6. Başlangıç Sihirbazı'nda, Microsoft hesabınızla oturum açın.

7. 2. adımda kaydettiğiniz hello uygulama tıklatın, **sonraki**ve ardından **ilişkilendirmek**. Bu gerekli hello Windows mağazası kayıt bilgilerini toohello uygulama bildirimi ekler.

8. Merhaba üzerinde geri [Windows Geliştirme Merkezi](http://dev.windows.com/overview) sayfasında yeni uygulamanız için **Hizmetleri**, tıklatın **anında iletme bildirimleri**ve ardından **WNS/MPNS**.

9. **Yeni Bildirim**’e tıklayın.

10. **Boş (Bildirim)** şablonuna ve sonra **Tamam**’a tıklayın.

11. Bildirim için bir **Ad** ve Görsel **Bağlam** iletisi girin. Ardından **Taslak olarak kaydet**'e tıklayın.

12. Toohello gidin [uygulama kayıt portalı](http://apps.dev.microsoft.com) ve oturum açın.

13. Uygulamanızın adına tıklayın. Merhaba Not **uygulama gizli anahtarı** parola ve hello **paket güvenlik tanımlayıcısı (SID)** hello bulunan **Windows mağazası** platforma ayarlar.

     > [AZURE.WARNING]
    Merhaba uygulama gizli anahtarı ve paket SID'si önemli güvenlik kimlik bilgileridir. Bu değerleri kimseyle paylaşmayın veya uygulamanızla birlikte dağıtmayın.

## <a name="configure-your-notification-hub"></a>Bildirim hub'ınızı yapılandırma
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p>Select hello <b>Bildirim Hizmetleri</b> seçeneği ve hello <b>Windows (WNS)</b> seçeneği. Merhaba enter <b>uygulama gizli anahtarı</b> hello Parolada <b>güvenlik anahtarı</b> alan. Girin, <b>paket SID'si</b> WNS hello önceki bölümdeki alınan ve ardından değeri <b>kaydetmek</b>.</p>
</li>
</ol>

&emsp;&emsp;![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-configure-wns.png)

Bildirim hub'ınız şimdi WNS ile yapılandırılmış toowork olan ve hello bağlantı dizeleri tooregister uygulamanızı çalıştırdıktan ve bildirimleri göndermek.

## <a name="connect-your-app-toohello-notification-hub"></a>Uygulama toohello bildirim hub'ınıza bağlanın
1. Visual Studio'da hello çözüme sağ tıklayın ve ardından **NuGet paketlerini Yönet**.
   
    Bu hello görüntüler **NuGet paketlerini Yönet** iletişim kutusu.
2. Arama `WindowsAzure.Messaging.Managed` tıklatıp **yükleme**ve hello kullanım koşullarını kabul edin.
   
    ![][20]
   
    Bu indirir, yükler ve bir başvuru toohello Azure Mesajlaşma kitaplığına için Windows hello kullanarak ekler <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet paketini</a>.
3. Merhaba App.xaml.cs dosyasını açın ve hello aşağıdakileri ekleyin `using` deyimleri. 
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.UI.Popups;
4. Ayrıca App.xaml.cs dosyasında hello aşağıdakileri ekleyin **Initnotificationsasync** yöntemi tanımı toohello **uygulama** sınıfı:
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("< your hub name>", "<Your DefaultListenSharedAccessSignature connection string>");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
   
        }
   
    Bu kod, WNS'den hello uygulama hello kanal URI'sini alır ve ardından bu kanal URI'sini bildirim hub'ınıza kaydeder.
   
   > [!NOTE]
   > "Hub name" yer tutucusunu hello Azure Portal görünür hello bildirim hub'hello adı ile Merhaba emin tooreplace olun. Ayrıca hello bağlantı dizesi yer tutucusunu hello ile değiştirin **DefaultListenSharedAccessSignature** hello elde edilen bağlantı dizesi **erişim ilkeleri** bildirim Hub'ınıza sayfasının bir önceki bölümde.
   > 
   > 
5. Merhaba hello üstündeki **OnLaunched** App.xaml.cs dosyasındaki olay işleyicisi ekleme çağrısı toohello yeni aşağıdaki hello **Initnotificationsasync** yöntemi:
   
        InitNotificationsAsync();
   
    Bu URI her zaman Merhaba uygulaması başlatıldığında bildirim hub'ınıza kayıtlı hello kanal güvence altına alır.
6. Tuşuna hello **F5** anahtar toorun hello uygulama. Merhaba kayıt anahtarını içeren bir açılır iletişim kutusu görüntülenir.

Uygulamanızı hazır tooreceive bildirimleri sunulmuştur.

## <a name="send-notifications"></a>Bildirim gönderme
Hello bildirimleri göndererek uygulamanızda bildirim alma hızlı bir şekilde test edebilirsiniz [Azure Portal](https://portal.azure.com/) hello kullanarak **Test gönderimi** ekranda hello aşağıda gösterildiği gibi hello bildirim hub'ına, düğme.

![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-test-send-wns.png)

Anında iletme bildirimleri normalde, uyumlu bir kitaplık kullanılarak Mobile Services veya ASP.NET gibi bir arka uç hizmetinde gönderilir. Bir kitaplık arka ucunuz için kullanılabilir değilse toosend bildirim iletilerini doğrudan hello REST API de kullanabilirsiniz. 

Bu öğreticide, biz basit tutmak ve yalnızca arka uç hizmeti yerine bir konsol uygulamasındaki bildirim hub'ları için hello .NET SDK kullanarak bildirim göndererek istemci uygulamanızı test etme gösterin. Merhaba öneririz [Notification Hubs kullanma toopush bildirimleri toousers] hello bir ASP.NET arka ucundan bildirim göndermek için sonraki adım olarak Öğreticisi. Ancak, aşağıdaki yaklaşımlardan hello bildirim göndermek için kullanılabilir:

* **REST arabirimi**: hello kullanarak herhangi bir arka uç platform bildirim destekleyebilir [REST arabirimini](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).
* **Microsoft Azure Notification Hubs .NET SDK'sı**: hello Visual Studio için Nuget Paket Yöneticisi, çalışması [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).
* **Node.js** : [nasıl toouse node.js'den Notification Hubs](notification-hubs-nodejs-push-notification-tutorial.md).
* **Azure Mobile Apps**: bir örneği için Notification Hubs ile tümleştirilmiş bir Azure mobil uygulaması toosend bildirimleri bkz [Mobile Apps için anında iletme bildirimleri ekleme](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).
* **Java / PHP**: REST API'lerini kullanarak toosend bildirim nasıl hello ilişkin bir örnek için bkz: "nasıl toouse Java/php'den Notification Hubs" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).

## <a name="optional-send-notifications-from-a-console-app"></a>(İsteğe bağlı) Konsol uygulamasından bildirim gönderme
bir .NET konsol uygulaması kullanarak toosend bildirim aşağıdaki adımları izleyin. 

1. Sağ hello çözüm, select **Ekle** ve **yeni proje...** ve ardından **Visual C#**, tıklatın **Windows** ve **konsol uygulaması**, tıklatıp **Tamam**.
   
    Yeni Visual C# konsol uygulaması toohello çözümü ekler. Bunu ayrı bir çözümde de yapabilirsiniz.

2. Visual Studio'da **Araçlar**'a, **NuGet Paket Yöneticisi**'ne ve ardından **Paket Yöneticisi Konsolu**'na tıklayın.
   
    Bu, Visual Studio'da Paket Yöneticisi konsolu hello görüntüler.
3. Hello Paket Yöneticisi konsolu penceresinde, hello ayarlamak **varsayılan proje** tooyour yeni konsol uygulama projesi ve sonra hello konsol penceresinde hello aşağıdaki komutu yürütün:
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    Bu başvuru toohello Azure Notification Hubs SDK'sı ekler hello kullanarak <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet paketini</a>.
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. Merhaba Program.cs dosyasını açın ve hello aşağıdakileri ekleyin `using` deyimi:
   
        using Microsoft.Azure.NotificationHubs;
5. Merhaba, **Program** sınıfı, yöntem aşağıdaki hello ekleyin:
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
            await hub.SendWindowsNativeNotificationAsync(toast);
        }
   
       Make sure tooreplace hello "hub name" placeholder with hello name of hello notification hub that as it appears in hello Azure Portal. Also, replace hello connection string placeholder with hello **DefaultFullSharedAccessSignature** connection string that you obtained from hello **Access Policies** page of your Notification Hub in hello section called "Configure your notification hub."
   
   > [!NOTE]
   > Sahip hello bağlantı dizesini kullandığınızdan emin olun **tam** erişimi ile değil, **dinleme** erişim. Merhaba dinleme erişimi dizesinin izinleri toosend bildirimleri yok.
   > 
   > 
6. Merhaba satırlarında aşağıdaki hello eklemek **ana** yöntemi:
   
         SendNotificationAsync();
         Console.ReadLine();
7. Visual Studio'da Hello konsol uygulama projesi sağ tıklayın ve **başlangıç projesi olarak ayarla** tooset hello başlangıç projesi olarak. Merhaba tuşuna **F5** anahtar toorun Merhaba uygulaması.
   
    Tüm kayıtlı cihazlarda bildirim alırsınız. Tıklatmak veya dokunarak hello bildirim başlığına hello uygulamayı yükler.

Hello tüm hello desteklenen yükleri bulabilirsiniz [bildirim Kataloğu], [kutucuk Kataloğu], ve [göstergeye genel bakış] MSDN'de Konular.

## <a name="next-steps"></a>Sonraki adımlar
Bu basit örnekte hello portalı veya bir konsol uygulaması kullanarak Windows cihazlarınıza yayın bildirimleri tooall gönderdi. Merhaba öneririz [Notification Hubs kullanma toopush bildirimleri toousers] hello sonraki adım olarak Öğreticisi. Bunu nasıl kullanarak bir ASP.NET arka uç toosend bildirimleri etiketler tootarget belirli kullanıcılara gösterilir.

Kullanıcılarınızı ilgi alanı gruplarına göre toosegment istiyorsanız, bkz: [son dakika haberleri Notification Hubs kullanma toosend]. 

toolearn Notification Hubs hakkında daha fazla genel bilgi [Notification Hubs Kılavuzu](notification-hubs-push-notification-overview.md).

<!-- Images. -->
[13]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-create-console-app.png
[14]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-toast.png
[19]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-reg.png
[20]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-universal-app-install-package.png

<!-- URLs. -->

[Notification Hubs kullanma toopush bildirimleri toousers]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[son dakika haberleri Notification Hubs kullanma toosend]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md

[bildirim Kataloğu]: http://msdn.microsoft.com/library/windows/apps/hh761494.aspx
[kutucuk Kataloğu]: http://msdn.microsoft.com/library/windows/apps/hh761491.aspx
[göstergeye genel bakış]: http://msdn.microsoft.com/library/windows/apps/hh779719.aspx
