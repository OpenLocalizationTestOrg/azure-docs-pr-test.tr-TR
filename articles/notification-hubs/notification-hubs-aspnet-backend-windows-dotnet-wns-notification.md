---
title: ".NET arka ucu ile aaaAzure Notification Hubs kullanıcılara bildirme"
description: "Nasıl toosend güvenli anında iletme bildirimleri ile Azure öğrenin. Merhaba .NET API kullanarak C# içinde yazılan kod örnekleri."
documentationcenter: windows
author: ysxu
manager: erikre
services: notification-hubs
editor: 
ms.assetid: 012529f2-fdbc-43c4-8634-2698164b5880
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: a366181faa81e78adf4de61435ef2790c3aa29d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-notify-users-with-net-backend"></a>Azure Notification Hubs kullanıcılara bildirme .NET arka ucu ile
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a>Genel Bakış
Azure'da anında iletme bildirimi destek tooaccess kullanımı kolay, multiplatform ve Mobile Tüketiciler, kurumsal uygulamalar için anında iletme bildirimleri hello uyarlamasını büyük ölçüde basitleştirir ölçeklendirilmiş gönderim altyapısı sağlar Platform. Bu öğretici nasıl toouse Azure Notification Hubs toosend anında iletme bildirimleri tooa belirli uygulama kullanıcısı belirli bir cihazda gösterir. Bir ASP.NET Webapı arka kullanılan tooauthenticate istemcileri kullanılır. Merhaba kullanılarak istemci kullanıcı kimlik doğrulaması ve etiket hello arka uç toonotification kayıt tarafından otomatik olarak eklenir. Bu etiket hello arka uç toogenerate bildirimleri için belirli bir kullanıcı tarafından kullanılan toosend olacaktır. Uygulama arka ucu kullanarak bildirimleri için kaydediliyor daha fazla bilgi için Başlangıç Kılavuzu konusuna [uygulama arka ucunuzdan kaydetme](http://msdn.microsoft.com/library/dn743807.aspx). Bu öğretici hello bildirim hub'ı ve hello oluşturulan proje derlemeler [Notification Hubs ile çalışmaya başlama] Öğreticisi.

Bu öğretici aynı zamanda hello önkoşul toohello olan [güvenli anında] Öğreticisi. Bu öğreticide hello adımlarını tamamladıktan sonra toohello geçebilmeniz [güvenli anında] nasıl toomodify hello kod Bu öğretici toosend bir anında iletme bildirimi güvenli bir şekilde gösteren öğretici.

## <a name="before-you-begin"></a>Başlamadan önce
Geri bildiriminizi ciddiye alacağız. Bu konu veya bu içeriğin geliştirilmesi için öneriler Tamamlanıyor bir güçlükle karşılaşırsanız hello sayfanın hello sonundaki görüşlerinize değer veriyoruz.

Bu öğreticinin hello tamamlanan kodu Github'da bulunabilir [burada](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers). 

## <a name="prerequisites"></a>Ön koşullar
Bu öğretici başlamadan önce zaten bu Mobile Services öğreticileri tamamlamış olmanız gerekir:

* [Notification Hubs ile çalışmaya başlama]<br/>Merhaba uygulama adı ayrılmaya bildirim hub'ınızı oluşturması ve Bu öğreticide tooreceive bildirimleri kaydedin. Bu öğreticide adımları önceden tamamlamış varsayar. Aksi durumda, lütfen hello adımları [bildirim hub'ları (Windows mağazası) ile çalışmaya başlama](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); özellikle, hello bölümleri [hello Windows mağazası için uygulamanızı kaydetme](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) ve [Yapılandır Bildirim Hub'ınızı](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub). Özellikle, hello girdiğinizden emin olun **paket SID'si** ve **gizli** hello portalında hello değerleri **yapılandırma** bildirim hub'ınız için sekmesi. Bu yapılandırma yordamı hello bölümünde açıklanan [bildirim hub'ınızı yapılandırma](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub). Bu önemli bir adımdır: hello portal hello kimlik bilgisi belirtilen hello uygulama adı için seçtiğiniz eşleşmiyorsa, hello anında iletme bildirimi başarısız olur.

> [!NOTE]
> Merhaba, arka uç hizmeti olarak Azure App Service'de Mobile Apps kullanıyorsanız, bkz: [Mobile Apps sürüm](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) Bu öğreticinin.
> 
> 

&nbsp;

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="update-hello-code-for-hello-client-project"></a>Merhaba istemci projesi için Hello kodunu güncelleştirin
Bu bölümde, Merhaba tamamlandı hello projesindeki hello kod güncelleştirme [Notification Hubs ile çalışmaya başlama] Öğreticisi. Merhaba zaten hello deposuyla ilişkili ve gerekir bildirim hub'ınız için yapılandırılmış. Bu bölümde, kod toocall hello yeni Webapı arka ekleyin ve kaydetme ve bildirimleri göndermek için kullanın.

1. Merhaba oluşturduğunuz hello hello çözümü Visual Studio'da açın [Notification Hubs ile çalışmaya başlama] Öğreticisi.
2. Çözüm Gezgini'nde hello sağ **(Windows 8.1)** proje ve ardından **NuGet paketlerini Yönet**.
3. Merhaba sol taraftaki tıklatın **çevrimiçi**.
4. Merhaba, **arama** kutusuna **Http istemcisi**.
5. Merhaba sonuçlar listesinde tıklayın **Microsoft HTTP istemci kitaplıkları**ve ardından **yükleme**. Merhaba yüklemeyi tamamlayın.
6. Merhaba NuGet edilene **arama** kutusuna **Json.net**. Merhaba yüklemek **Json.NET** paket ve ardından Kapat hello NuGet Paket Yöneticisi penceresi.
7. Merhaba yukarıdaki Hello adımları yineleyin **(Windows Phone 8.1)** proje tooinstall hello **JSON.NET** hello Windows Phone projesi için NuGet paketi.
8. Çözüm Gezgini'nde, hello **(Windows 8.1)** projesi, çift **MainPage.xaml** tooopen onu hello Visual Studio düzenleyicisinde.
9. Merhaba, **MainPage.xaml** XML kodunu değiştir hello `<Grid>` koddan hello bölümle. Bu kod, kullanıcı hello bir kullanıcı adı ve parola textbox ile kimlik doğrulaması ekler. Ayrıca, hello bildirim iletisi ve hello bildirimi alması gereken hello kullanıcı adı etiketi için metin kutuları ekler:
   
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition Height="Auto"/>
                <RowDefinition Height="*"/>
            </Grid.RowDefinitions>
   
            <TextBlock Grid.Row="0" Text="Notify Users" HorizontalAlignment="Center" FontSize="48"/>
   
            <StackPanel Grid.Row="1" VerticalAlignment="Center">
                <Grid>
                    <Grid.RowDefinitions>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                    </Grid.RowDefinitions>
                    <Grid.ColumnDefinitions>
                        <ColumnDefinition></ColumnDefinition>
                        <ColumnDefinition></ColumnDefinition>
                        <ColumnDefinition></ColumnDefinition>
                    </Grid.ColumnDefinitions>
                    <TextBlock Grid.Row="0" Grid.ColumnSpan="3" Text="Username" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="UsernameTextBox" Grid.Row="1" Grid.ColumnSpan="3" Margin="20,0,20,0"/>
                    <TextBlock Grid.Row="2" Grid.ColumnSpan="3" Text="Password" FontSize="24" Margin="20,0,20,0" />
                    <PasswordBox Name="PasswordTextBox" Grid.Row="3" Grid.ColumnSpan="3" Margin="20,0,20,0"/>
   
                    <Button Grid.Row="4" Grid.ColumnSpan="3" HorizontalAlignment="Center" VerticalAlignment="Center"
                                Content="1. Login and register" Click="LoginAndRegisterClick" Margin="0,0,0,20"/>
   
                    <ToggleButton Name="toggleWNS" Grid.Row="5" Grid.Column="0" HorizontalAlignment="Right" Content="WNS" IsChecked="True" />
                    <ToggleButton Name="toggleGCM" Grid.Row="5" Grid.Column="1" HorizontalAlignment="Center" Content="GCM" />
                    <ToggleButton Name="toggleAPNS" Grid.Row="5" Grid.Column="2" HorizontalAlignment="Left" Content="APNS" />
   
                    <TextBlock Grid.Row="6" Grid.ColumnSpan="3" Text="Username Tag tooSend To" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="ToUserTagTextBox" Grid.Row="7" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <TextBlock Grid.Row="8" Grid.ColumnSpan="3" Text="Enter Notification Message" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="NotificationMessageTextBox" Grid.Row="9" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <Button Grid.Row="10" Grid.ColumnSpan="3" HorizontalAlignment="Center" Content="2. Send push" Click="PushClick" Name="SendPushButton" />
                </Grid>
            </StackPanel>
        </Grid>
10. Çözüm Gezgini'nde, hello **(Windows Phone 8.1)** proje, açık **MainPage.xaml** ve Windows Phone 8.1 hello Değiştir `<Grid>` yukarıdaki aynı kodu ile bölüm. Merhaba arabirimi aşağıda gösterilen benzer toowhats görünmelidir.
    
    ![][13]
11. Çözüm Gezgini'nde hello açın **MainPage.xaml.cs** hello dosyası **(Windows 8.1)** ve **(Windows Phone 8.1)** projeleri. Merhaba aşağıdakileri ekleyin `using` deyimleri hello üst dosyalar:
    
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Windows.Networking.PushNotifications;
        using Windows.UI.Popups;
        using System.Threading.Tasks;
12. İçinde **MainPage.xaml.cs** hello için **(Windows 8.1)** ve **(Windows Phone 8.1)** projeler eklemek üye toohello aşağıdaki hello `MainPage` sınıfı. Emin tooreplace olması `<Enter Your Backend Endpoint>` hello ile gerçek arka uç noktanızı elde daha önce. Örneğin, `http://mybackend.azurewebsites.net`.
    
        private static string BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";
13. Merhaba toohello MainPage sınıfında aşağıdaki kodu ekleyin **MainPage.xaml.cs** hello için **(Windows 8.1)** ve **(Windows Phone 8.1)** projeleri.
    
    Merhaba `PushClick` yöntemdir hello hello için işleyicisi'ı tıklatın **Gönder anında** düğmesi. Merhaba eşleşen bir kullanıcı adı etiketi ile cihazları hello arka uç tootrigger bildirim tooall çağırır `to_tag` parametresi. Merhaba bildirim iletisi hello istek gövdesinde JSON içeriği olarak gönderilir.
    
    Merhaba `LoginAndRegisterClick` yöntemdir hello hello için işleyicisi'ı tıklatın **oturum açma ve kaydetme** düğmesi. Merhaba basic depolar (Bu, kimlik doğrulama şemasını kullanan herhangi bir belirteci temsil ettiğini unutmayın), Yerel Depodaki kimlik doğrulama belirteci sonra kullanır `RegisterClient` tooregister hello arka uç kullanarak bildirimleri için.

        private async void PushClick(object sender, RoutedEventArgs e)
        {
            if (toggleWNS.IsChecked.Value)
            {
                await sendPush("wns", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);
            }
            if (toggleGCM.IsChecked.Value)
            {
                await sendPush("gcm", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);
            }
            if (toggleAPNS.IsChecked.Value)
            {
                await sendPush("apns", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);

            }
        }

        private async Task sendPush(string pns, string userTag, string message)
        {
            var POST_URL = BACKEND_ENDPOINT + "/api/notifications?pns=" +
                pns + "&to_tag=" + userTag;

            using (var httpClient = new HttpClient())
            {
                var settings = ApplicationData.Current.LocalSettings.Values;
                httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);

                try
                {
                    await httpClient.PostAsync(POST_URL, new StringContent("\"" + message + "\"",
                        System.Text.Encoding.UTF8, "application/json"));
                }
                catch (Exception ex)
                {
                    MessageDialog alert = new MessageDialog(ex.Message, "Failed toosend " + pns + " message");
                    alert.ShowAsync();
                }
            }
        }

        private async void LoginAndRegisterClick(object sender, RoutedEventArgs e)
        {
            SetAuthenticationTokenInLocalStorage();

            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

            // hello "username:<user name>" tag gets automatically added by hello message handler in hello backend.
            // hello tag passed here can be whatever other tags you may want toouse.
            try
            {
                // hello device handle used will be different depending on hello device and PNS. 
                // Windows devices use hello channel uri as hello PNS handle.
                await new RegisterClient(BACKEND_ENDPOINT).RegisterAsync(channel.Uri, new string[] { "myTag" });

                var dialog = new MessageDialog("Registered as: " + UsernameTextBox.Text);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
                SendPushButton.IsEnabled = true;
            }
            catch (Exception ex)
            {
                MessageDialog alert = new MessageDialog(ex.Message, "Failed tooregister with RegisterClient");
                alert.ShowAsync();
            }
        }

        private void SetAuthenticationTokenInLocalStorage()
        {
            string username = UsernameTextBox.Text;
            string password = PasswordTextBox.Password;

            var token = Convert.ToBase64String(System.Text.Encoding.UTF8.GetBytes(username + ":" + password));
            ApplicationData.Current.LocalSettings.Values["AuthenticationToken"] = token;
        }



1. Çözüm Gezgini'nde, hello altında **paylaşılan** proje, açık hello **App.xaml.cs** dosya. Merhaba görüşmesi çok bulma`InitNotificationsAsync()` hello içinde `OnLaunched()` olay işleyicisi. Out yorum yapmak veya hello çağrısı çok silme`InitNotificationsAsync()`. yukarıda eklediğiniz hello düğme işleyicisi bildirim kayıtlar başlatacak.

        protected override void OnLaunched(LaunchActivatedEventArgs e)
        {
            //InitNotificationsAsync();


1. Çözüm Gezgini'nde hello sağ **paylaşılan** proje ve ardından **Ekle**ve ardından **sınıfı**. Ad hello sınıfı **RegisterClient.cs**, ardından **Tamam** toogenerate hello sınıfı.
   
   Bu sınıf, anında iletme bildirimleri için sipariş tooregister hello REST çağrılarını gerekli toocontact hello uygulama arka ucu, kaydırılır. Merhaba da yerel olarak depoladığı *registrationIds* bildirim hub'ı ayrıntılı biçimde açıklandığı gibi hello tarafından oluşturulan [uygulama arka ucunuzdan kaydetme](http://msdn.microsoft.com/library/dn743807.aspx). Merhaba tıklattığınızda yerel depolamada depolanan bir yetki belirteci kullandığına dikkat edin **oturum açma ve kaydetme** düğmesi.
2. Merhaba aşağıdakileri ekleyin `using` deyimleri hello dosyanın üst kısmındaki hello RegisterClient.cs:
   
       using Windows.Storage;
       using System.Net;
       using System.Net.Http;
       using System.Net.Http.Headers;
       using Newtonsoft.Json;
       using System.Threading.Tasks;
       using System.Linq;
3. Merhaba içindeki kodu aşağıdaki hello eklemek `RegisterClient` sınıf tanımının.
   
       private string POST_URL;
   
       private class DeviceRegistration
       {
           public string Platform { get; set; }
           public string Handle { get; set; }
           public string[] Tags { get; set; }
       }
   
       public RegisterClient(string backendEndpoint)
       {
           POST_URL = backendEndpoint + "/api/register";
       }
   
       public async Task RegisterAsync(string handle, IEnumerable<string> tags)
       {
           var regId = await RetrieveRegistrationIdOrRequestNewOneAsync();
   
           var deviceRegistration = new DeviceRegistration
           {
               Platform = "wns",
               Handle = handle,
               Tags = tags.ToArray<string>()
           };
   
           var statusCode = await UpdateRegistrationAsync(regId, deviceRegistration);
   
           if (statusCode == HttpStatusCode.Gone)
           {
               // regId is expired, deleting from local storage & recreating
               var settings = ApplicationData.Current.LocalSettings.Values;
               settings.Remove("__NHRegistrationId");
               regId = await RetrieveRegistrationIdOrRequestNewOneAsync();
               statusCode = await UpdateRegistrationAsync(regId, deviceRegistration);
           }
   
           if (statusCode != HttpStatusCode.Accepted)
           {
               // log or throw
               throw new System.Net.WebException(statusCode.ToString());
           }
       }
   
       private async Task<HttpStatusCode> UpdateRegistrationAsync(string regId, DeviceRegistration deviceRegistration)
       {
           using (var httpClient = new HttpClient())
           {
               var settings = ApplicationData.Current.LocalSettings.Values;
               httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string) settings["AuthenticationToken"]);
   
               var putUri = POST_URL + "/" + regId;
   
               string json = JsonConvert.SerializeObject(deviceRegistration);
                               var response = await httpClient.PutAsync(putUri, new StringContent(json, Encoding.UTF8, "application/json"));
               return response.StatusCode;
           }
       }
   
       private async Task<string> RetrieveRegistrationIdOrRequestNewOneAsync()
       {
           var settings = ApplicationData.Current.LocalSettings.Values;
           if (!settings.ContainsKey("__NHRegistrationId"))
           {
               using (var httpClient = new HttpClient())
               {
                   httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                   var response = await httpClient.PostAsync(POST_URL, new StringContent(""));
                   if (response.IsSuccessStatusCode)
                   {
                       string regId = await response.Content.ReadAsStringAsync();
                       regId = regId.Substring(1, regId.Length - 2);
                       settings.Add("__NHRegistrationId", regId);
                   }
                   else
                   {
                       throw new System.Net.WebException(response.StatusCode.ToString());
                   }
               }
           }
           return (string)settings["__NHRegistrationId"];
   
       }
4. Yaptığınız tüm değişiklikleri kaydedin.

## <a name="testing-hello-application"></a>Merhaba uygulamayı test etme
1. Windows 8.1 ve Windows Phone 8.1 Merhaba uygulaması başlatın. Windows Phone 8.1 için hello öykünücü veya gerçek bir cihaza hello örneği çalıştırabilirsiniz.
2. Merhaba uygulama Hello Windows 8.1 örneğinde girin bir **kullanıcıadı** ve **parola** ekranda hello aşağıda gösterildiği gibi. Merhaba kullanıcı adı ve parola Windows Phone üzerinde farklı olmalıdır.
3. Tıklatın **oturum açma ve kaydetme** ve bir iletişim kutusu gösterir oturum olduğunu doğrulayın. Bu da hello etkinleştirir **Gönder anında** düğmesi.
   
    ![][14]
4. Merhaba Windows Phone 8.1 örneği, bir kullanıcı adı dizesi hem hello girin **kullanıcıadı** ve **parola** alanları ardından **oturum açma ve kaydetme**.
5. Merhaba sonra **alıcı kullanıcı adı etiketi** alanında, Windows 8.1 kayıtlı hello kullanıcı adı girin. Bir bildirim iletisi girin ve tıklayın **Gönder anında**.
   
    ![][16]
6. Merhaba eşleşen kullanıcı adı etiketi ile kaydettiğiniz hello cihazların Merhaba bildirim iletisi alırsınız.
   
    ![][15]

## <a name="next-steps"></a>Sonraki Adımlar
* Kullanıcılarınızı ilgi alanı gruplarına göre toosegment istiyorsanız, bkz: [son dakika haberleri Notification Hubs kullanma toosend].
* toouse bildirim hub'ları, toolearn nasıl hakkında daha fazla bilgi görmek [Notification Hubs Kılavuzu].

[9]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push9.png
[10]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push10.png
[11]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push11.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-ui.png
[14]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-windows-instance-username.png
[15]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-notification-received.png
[16]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-send-message.png



<!-- URLs. -->
[Notification Hubs ile çalışmaya başlama]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[güvenli anında]: notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md
[son dakika haberleri Notification Hubs kullanma toosend]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
[Notification Hubs Kılavuzu]: http://msdn.microsoft.com/library/jj927170.aspx
