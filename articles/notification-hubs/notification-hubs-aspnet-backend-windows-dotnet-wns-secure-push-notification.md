---
title: "aaaAzure güvenli hub bildirim gönderme"
description: "Nasıl toosend güvenli anında iletme bildirimleri ile Azure öğrenin. Merhaba .NET API kullanarak C# içinde yazılan kod örnekleri."
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
services: notification-hubs
ms.assetid: 5aef50f4-80b3-460e-a9a7-7435001273bd
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: b6fe16c96d28d75ff698278409fb012472ba6396
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-secure-push"></a>Azure Notification Hubs güvenli bildirme
> [!div class="op_single_selector"]
> * [Windows Evrensel](notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md)
> * [iOS](notification-hubs-aspnet-backend-ios-push-apple-apns-secure-notification.md)
> * [Android](notification-hubs-aspnet-backend-android-secure-google-gcm-push-notification.md)
> 
> 

## <a name="overview"></a>Genel Bakış
Microsoft Azure anında iletme bildirimi desteği tooaccess Mobile Tüketiciler, kurumsal uygulamalar için anında iletme bildirimleri hello uyarlamasını büyük ölçüde basitleştirir bir kullanımı kolay, çok platformlu, ölçeği gönderim altyapısı sağlar Platform.

Tooregulatory veya güvenlik kısıtlamaları, bazen bir uygulama bir şey hello standart anında iletme bildirimi altyapısı iletilen hello bildirim tooinclude isteyebilirsiniz. Bu öğretici nasıl tooachieve hello aynı deneyimi hello istemci aygıt hello uygulama arka ucu arasında güvenli, kimliği doğrulanmış bir bağlantı üzerinden hassas bilgileri göndererek açıklar.

Yüksek bir düzeyde hello akışı aşağıdaki gibidir:

1. Merhaba uygulama arka ucu:
   * Arka uç veritabanı güvenli yükünde depolar.
   * Merhaba (güvenli hiçbir bilgi gönderilmez) Bu bildirim toohello aygıtın Kimliğini gönderir.
2. Merhaba cihaza hello bildirim alırken Hello uygulamanın:
   * Merhaba cihaz hello arka uç isteyen hello güvenli yükü bağlanır.
   * Merhaba uygulama hello yükü hello aygıt bildirim olarak gösterebilir.

Merhaba kullanıcı oturum açtığında sonra akışı önceki hello (ve Bu öğreticide), biz hello aygıt varsayın toonote kimlik doğrulama belirtecini yerel depolama biriminde, depolar. önemlidir. Merhaba aygıt hello bildirim'ın güvenli yükü bu belirteci kullanarak alabilir gibi tamamen sorunsuz bir deneyim daha güvence altına alır. Uygulamanızın kimlik doğrulama belirteçleri hello aygıtta depolamaz veya bu belirteçleri süresi, hello hello bildirim alma sırasında cihaz uygulaması hello kullanıcı toolaunch hello uygulama isteyen genel bir bildirim görüntülemelidir. Merhaba uygulama hello kullanıcının kimliğini doğrular ve hello bildirim yükü gösterir.

Bu güvenli itme öğreticide gösterilmiştir nasıl toosend bir anında iletme bildirimi güvenli bir şekilde. Merhaba öğretici derlemeler üzerinde hello [kullanıcılara bildirme](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md) önce bu öğreticide hello adımlar tamamlanmalıdır şekilde öğretici.

> [!NOTE]
> Bu öğreticide oluşturduğunuz ve bildirim hub'ınızı açıklandığı şekilde yapılandırılmış varsayar [bildirim hub'ları (Windows mağazası) ile çalışmaya başlama](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md).
> Ayrıca, Windows Phone 8.1 (Windows Phone değil) Windows kimlik bilgileri gerektirir ve arka plan görevleri Windows Phone 8.0 veya Silverlight 8.1 çalışmaz unutmayın. Windows mağazası uygulamaları için yalnızca hello uygulama ekran kilitleme etkin ise bir arka plan görevi aracılığıyla bildirimleri alabilirsiniz (Merhaba Appmanifest hello onay kutusu tıklayın).
> 
> 

[!INCLUDE [notification-hubs-aspnet-backend-securepush](../../includes/notification-hubs-aspnet-backend-securepush.md)]

## <a name="modify-hello-windows-phone-project"></a>Windows Phone proje Hello değiştirme
1. Merhaba, **NotifyUserWindowsPhone** projesi, kod tooApp.xaml.cs tooregister hello itme arka plan görevi aşağıdaki hello ekleyin. Aşağıdaki kod hello hello sonunda hello eklemek `OnLaunched()` yöntemi:
   
        RegisterBackgroundTask();
2. Hala App.xaml.cs dosyasında koddan hemen sonra hello hello eklemek `OnLaunched()` yöntemi:
   
        private async void RegisterBackgroundTask()
        {
            if (!Windows.ApplicationModel.Background.BackgroundTaskRegistration.AllTasks.Any(i => i.Value.Name == "PushBackgroundTask"))
            {
                var result = await BackgroundExecutionManager.RequestAccessAsync();
                var builder = new BackgroundTaskBuilder();
   
                builder.Name = "PushBackgroundTask";
                builder.TaskEntryPoint = typeof(PushBackgroundComponent.PushBackgroundTask).FullName;
                builder.SetTrigger(new Windows.ApplicationModel.Background.PushNotificationTrigger());
                BackgroundTaskRegistration task = builder.Register();
            }
        }
3. Merhaba aşağıdakileri ekleyin `using` deyimleri hello App.xaml.cs dosyasını hello üstündeki:
   
        using Windows.Networking.PushNotifications;
        using Windows.ApplicationModel.Background;
4. Merhaba gelen **dosya** Visual Studio'da menüsünü **Tümünü Kaydet**.

## <a name="create-hello-push-background-component"></a>Merhaba itme arka plan bileşeni oluşturma
Merhaba sonraki adıma toocreate hello itme arka plan bileşendir.

1. Çözüm Gezgini'nde hello çözümün hello en üst düzey düğüme sağ tıklayın (**çözüm SecurePush** bu durumda), ardından **Ekle**, ardından **yeni proje**.
2. Genişletme **mağazası uygulamaları**, ardından **Windows Phone uygulamaları**, ardından **Windows çalışma zamanı bileşeni (Windows Phone)**. Ad hello proje **PushBackgroundComponent**ve ardından **Tamam** toocreate hello projesi.
   
    ![][12]
3. Çözüm Gezgini'nde hello sağ **PushBackgroundComponent (Windows Phone 8.1)** proje ve ardından **Ekle**, ardından **sınıfı**. Ad hello yeni sınıf **PushBackgroundTask.cs**. Tıklatın **Ekle** toogenerate hello sınıfı.
4. Merhaba Hello tüm içeriğini değiştirin **PushBackgroundComponent** ad alanı tanımını aşağıdaki kod, hello yer tutucu değiştirerek hello ile `{back-end endpoint}` dağıtırken elde hello arka uç uç noktası ile arka uç:
   
        public sealed class Notification
            {
                public int Id { get; set; }
                public string Payload { get; set; }
                public bool Read { get; set; }
            }
   
            public sealed class PushBackgroundTask : IBackgroundTask
            {
                private string GET_URL = "{back-end endpoint}/api/notifications/";
   
                async void IBackgroundTask.Run(IBackgroundTaskInstance taskInstance)
                {
                    // Store hello content received from hello notification so it can be retrieved from hello UI.
                    RawNotification raw = (RawNotification)taskInstance.TriggerDetails;
                    var notificationId = raw.Content;
   
                    // retrieve content
                    BackgroundTaskDeferral deferral = taskInstance.GetDeferral();
                    var httpClient = new HttpClient();
                    var settings = ApplicationData.Current.LocalSettings.Values;
                    httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                    var notificationString = await httpClient.GetStringAsync(GET_URL + notificationId);
   
                    var notification = JsonConvert.DeserializeObject<Notification>(notificationString);
   
                    ShowToast(notification);
   
                    deferral.Complete();
                }
   
                private void ShowToast(Notification notification)
                {
                    ToastTemplateType toastTemplate = ToastTemplateType.ToastText01;
                    XmlDocument toastXml = ToastNotificationManager.GetTemplateContent(toastTemplate);
                    XmlNodeList toastTextElements = toastXml.GetElementsByTagName("text");
                    toastTextElements[0].AppendChild(toastXml.CreateTextNode(notification.Payload));
                    ToastNotification toast = new ToastNotification(toastXml);
                    ToastNotificationManager.CreateToastNotifier().Show(toast);
                }
            }
5. Çözüm Gezgini'nde hello sağ **PushBackgroundComponent (Windows Phone 8.1)** proje ve ardından **NuGet paketlerini Yönet**.
6. Merhaba sol taraftaki tıklatın **çevrimiçi**.
7. Merhaba, **arama** kutusuna **Http istemcisi**.
8. Merhaba sonuçlar listesinde tıklayın **Microsoft HTTP istemci kitaplıkları**ve ardından **yükleme**. Merhaba yüklemeyi tamamlayın.
9. Merhaba NuGet edilene **arama** kutusuna **Json.net**. Merhaba yüklemek **Json.NET** paket sonra Kapat hello NuGet Paket Yöneticisi penceresi.
10. Merhaba aşağıdakileri ekleyin `using` deyimleri hello hello üstündeki **PushBackgroundTask.cs** dosyası:
    
        using Windows.ApplicationModel.Background;
        using Windows.Networking.PushNotifications;
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Newtonsoft.Json;
        using Windows.UI.Notifications;
        using Windows.Data.Xml.Dom;
11. Çözüm Gezgini'nde, hello **NotifyUserWindowsPhone (Windows Phone 8.1)** projesinde **başvuruları**, ardından **Başvuru Ekle...** . Merhaba başvuru Yöneticisi iletişim kutusunda, hello sonraki çok onay kutusunu**PushBackgroundComponent**ve ardından **Tamam**.
12. Çözüm Gezgini'nde çift tıklayarak **Package.appxmanifest** hello içinde **NotifyUserWindowsPhone (Windows Phone 8.1)** projesi. Altında **bildirimleri**ayarlayın **bildirim özellikli** çok**Evet**.
    
    ![][3]
13. Hala **Package.appxmanifest**, hello tıklatın **bildirimleri** menü hello üstüne yakın. Merhaba, **kullanılabilir bildirimleri** açılan listesinde, tıklatın **arka plan görevleri**ve ardından **Ekle**.
14. İçinde **Package.appxmanifest**altında **özellikleri**, denetleme **anında bildirim**.
15. İçinde **Package.appxmanifest**altında **uygulama ayarları**, türü **PushBackgroundComponent.PushBackgroundTask** hello içinde **giriş noktası** alan.
    
    ![][13]
16. Merhaba gelen **dosya** menüsünde tıklatın **Tümünü Kaydet**.

## <a name="run-hello-application"></a>Merhaba uygulama çalıştırın
toorun Merhaba uygulama, aşağıdaki hello:

1. Visual Studio'da hello çalıştırmak **AppBackend** Web API uygulaması. Bir ASP.NET web sayfası görüntülenir.
2. Visual Studio'da hello çalıştırmak **NotifyUserWindowsPhone (Windows Phone 8.1)** Windows Phone Uygulama. Merhaba Windows Phone öykünücüsü çalışır ve hello uygulamayı otomatik olarak yükler.
3. Merhaba, **NotifyUserWindowsPhone** uygulama kullanıcı Arabirimi, bir kullanıcı adı ve parola girin. Bunlar herhangi bir dize olabilir, ancak bunlar olmalıdır hello aynı değeri.
4. Merhaba, **NotifyUserWindowsPhone** uygulama kullanıcı Arabirimi, tıklatın **oturum açma ve kaydetme**. Ardından **Gönder itme**.

[3]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push3.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-secure-push/notification-hubs-secure-push13.png
