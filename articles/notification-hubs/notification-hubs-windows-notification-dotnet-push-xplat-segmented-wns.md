---
title: "(Windows Evrensel) son dakika haberleri göndermek için Notification Hubs'ı kullanma"
description: "Bir evrensel Windows uygulaması için son dakika haberleri göndermek için Azure Notification Hubs kayıt etiketleri kullanın."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
ms.assetid: 994d2eed-f62e-433c-bf65-4afebf1c0561
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 0e945b5626a08fcb428131f2abb465c2c141011a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="use-notification-hubs-to-send-breaking-news"></a>Son dakika haberleri göndermek için Notification Hubs kullanma
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>Genel Bakış
Bu konu Azure Notification Hubs son dakika haberi bildirimleri Windows mağazası veya Windows Phone 8.1 (Silverlight olmayan) uygulamasına yayını için nasıl kullanılacağını gösterir. Windows Phone 8.1 Silverlight'ı hedefliyorsanız lütfen [Windows Evrensel](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) sürümüne bakın. Tamamlandığında, ilgilendiğiniz haber kategorileri dökümü için kaydedilecek olması ve yalnızca bu kategorilerin anında iletme bildirimlerini almak. Bu sayıda uygulama için genel bir desen bildirimleri daha önce bunları, örneğin RSS Okuyucu uygulamaları müzik fanları için ilgi derlendiğinden vb. kullanıcı gruplarının gönderilmesi sahip olduğu bir senaryodur. 

Yayın senaryoları etkin bir veya daha fazla dahil ederek *etiketleri* bir kayıt bildirim hub'ı oluştururken. Bildirimler için bir etiket gönderildiğinde, kaydettiğiniz tüm etiket cihazlarda bildirim alırsınız. Etiketleri yalnızca dizeleri olduğundan, bunlar önceden hazırlanması gerekmez. Etiketler hakkında daha fazla bilgi için başvurmak [bildirim hub'ları Yönlendirme ve etiket ifadeleri](notification-hubs-tags-segment-push-message.md).

> [!NOTE]
> Windows mağazası ve Windows Phone projeleri sürüm 8.1 ve önceki Visual Studio 2017 içinde desteklenmez.  Daha fazla bilgi için bkz. [Visual Studio 2017 Platform Desteği ve Uyumluluk](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs). 

## <a name="prerequisites"></a>Ön koşullar
Bu konu, oluşturduğunuz uygulama inşa edilmiştir [Notification Hubs ile çalışmaya başlama][get-started]. Bu öğreticiye başlamadan önce önce tamamlamış olmalıdır [Notification Hubs ile çalışmaya başlama][get-started].

## <a name="add-category-selection-to-the-app"></a>Kategori seçimi için uygulama ekleme
İlk adım, kullanıcı Arabirimi öğeleri kaydetmek için kategoriler seçmesini sağlayan varolan ana sayfanıza eklemektir. Bir kullanıcı tarafından seçilen kategoriler cihazda depolanır. Uygulama başlatıldığında bir aygıt kaydı bildirim hub'ınıza seçili kategorileri etiketler oluşturulur.

1. MainPage.xaml proje dosyasını açın, sonra aşağıdaki kodu kopyalayın **kılavuz** öğe:
   
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
                <RowDefinition/>
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition/>
                <ColumnDefinition/>
            </Grid.ColumnDefinitions>
            <TextBlock Grid.Row="0" Grid.Column="0" Grid.ColumnSpan="2"  TextWrapping="Wrap" Text="Breaking News" FontSize="42" VerticalAlignment="Top" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="World" Name="WorldToggle" Grid.Row="1" Grid.Column="0" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Politics" Name="PoliticsToggle" Grid.Row="2" Grid.Column="0" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Business" Name="BusinessToggle" Grid.Row="3" Grid.Column="0" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Technology" Name="TechnologyToggle" Grid.Row="1" Grid.Column="1" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Science" Name="ScienceToggle" Grid.Row="2" Grid.Column="1" HorizontalAlignment="Center"/>
            <ToggleSwitch Header="Sports" Name="SportsToggle" Grid.Row="3" Grid.Column="1" HorizontalAlignment="Center"/>
            <Button Name="SubscribeButton" Content="Subscribe" HorizontalAlignment="Center" Grid.Row="4" Grid.Column="0" Grid.ColumnSpan="2" Click="SubscribeButton_Click"/>
        </Grid>
2. Sağ tıklayın **paylaşılan** proje ve adlı yeni bir sınıf ekleyin **bildirimleri**, ekleme **ortak** değiştiricisi sınıf tanımına sonra aşağıdakileri ekleyin  **kullanarak** deyimleri için yeni kod dosyası:
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.Storage;
        using System.Threading.Tasks;
3. Aşağıdaki kodu yeni dosyaya kopyalayın **bildirimleri** sınıfı:
   
        private NotificationHub hub;
   
        public Notifications(string hubName, string listenConnectionString)
        {
            hub = new NotificationHub(hubName, listenConnectionString);
        }
   
        public async Task<Registration> StoreCategoriesAndSubscribe(IEnumerable<string> categories)
        {
            ApplicationData.Current.LocalSettings.Values["categories"] = string.Join(",", categories);
            return await SubscribeToCategories(categories);
        }
   
        public IEnumerable<string> RetrieveCategories()
        {
            var categories = (string) ApplicationData.Current.LocalSettings.Values["categories"];
            return categories != null ? categories.Split(','): new string[0];
        }
   
        public async Task<Registration> SubscribeToCategories(IEnumerable<string> categories = null)
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            if (categories == null)
            {
                categories = RetrieveCategories();
            }
   
            // Using a template registration to support notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyWNS = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(messageParam)</text></binding></visual></toast>";
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "simpleWNSTemplateExample",
                    categories);
        }
   
    Bu sınıf yerel depolama almak için bu aygıtın haber kategorilerini depolamak için kullanır. Arama yerine unutmayın *RegisterNativeAsync* diyoruz yöntemi *RegisterTemplateAsync* şablonu kayıt kullanarak kategorileri için kaydedilecek. 
   
    Ayrıca ("simpleWNSTemplateExample"), şablon için bir ad (örneğin bir bildirimleri için) ve biri döşeme için birden fazla şablon kaydetmek istiyoruz ve bunları güncelleştirmek veya bunları silmek için ad ihtiyacımız çünkü sunuyoruz.
   
    Bir aygıt ile aynı etiketi birden fazla şablon kaydederse, bir gelen ileti etiketi içinde birden fazla bildirim sonuçlanacak hedefleme aygıt (her şablon için bir tane) teslim olduğunu unutmayın. Bu davranış, aynı mantıksal ileti örneği için bir Windows mağazası uygulamasında bir gösterge ve bildirim gösteren birden çok görsel bildirimler neden olduğunda yararlıdır.
   
    Şablonlar hakkında daha fazla bilgi için bkz: [şablonları](notification-hubs-templates-cross-platform-push-messages.md).
4. App.xaml.cs proje dosyasında aşağıdaki özellik eklemek **uygulama** sınıfı:
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
    Bu özellik oluşturmak ve erişmek için kullanılan bir **bildirimleri** örneği.
   
    Yukarıdaki kodla `<hub name>` ve `<connection string with listen access>` , bildirim hub'ı adı ve bağlantı dizesinde yer tutucularını *DefaultListenSharedAccessSignature* daha önce edindiğiniz.
   
   > [!NOTE]
   > Bir istemci uygulaması ile dağıtılmış kimlik bilgileri genellikle güvenli olmadığı için istemci uygulamanızı dinleme erişim için anahtar yalnızca dağıtmanız. Bildirimler, ancak var olan kayıtlar için kaydetmek için uygulamanızın değiştirilemez erişimi etkinleştirir dinleyin ve bildirim gönderilemiyor. Tam erişim anahtarı, bir güvenli arka uç hizmetinde bildirimleri gönderme ve var olan kayıtlar değiştirmek için kullanılır.
   > 
   > 
5. MainPage.xaml.cs dosyasında aşağıdaki satırı ekleyin:
   
        using Windows.UI.Popups;
6. MainPage.xaml.cs proje dosyasında aşağıdaki yöntemi ekleyin:
   
        private async void SubscribeButton_Click(object sender, RoutedEventArgs e)
        {
            var categories = new HashSet<string>();
            if (WorldToggle.IsOn) categories.Add("World");
            if (PoliticsToggle.IsOn) categories.Add("Politics");
            if (BusinessToggle.IsOn) categories.Add("Business");
            if (TechnologyToggle.IsOn) categories.Add("Technology");
            if (ScienceToggle.IsOn) categories.Add("Science");
            if (SportsToggle.IsOn) categories.Add("Sports");
   
            var result = await ((App)Application.Current).notifications.StoreCategoriesAndSubscribe(categories);
   
            var dialog = new MessageDialog("Subscribed to: " + string.Join(",", categories) + " on registration Id: " + result.RegistrationId);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
   
    Bu yöntem kategorileri ve kullandığı bir liste oluşturur **bildirimleri** listesi yerel depolama alanına depolar ve karşılık gelen kaydetmek için sınıfı, bildirim hub'ınıza etiketler. Kategoriler değiştirildiğinde kaydı yeni kategoriler yeniden oluşturulur.

Uygulamanızı kategorileri kümesi cihazın yerel depolama depolamak ve kullanıcı kategorisi seçimine değiştiğinde bildirim hub'ınızla kaydolmak için sunulmuştur.

## <a name="register-for-notifications"></a>Bildirimler için kaydolun
Yerel depolamada depolanan kategorileri kullanarak başlangıçtaki bildirim hub'ı ile adımları kaydedin.

> [!NOTE]
> Windows bildirim Hizmeti'ni (WNS) tarafından atanan URI kanal herhangi bir zamanda değiştiğinden bildirimlerinin sık bildirim hataları önlemek için kayıt olmalıdır. Bu örnek uygulama başladıktan her zaman bir bildirime kaydolur. Sık çalıştırılan uygulamalar için günde bir kereden fazla, büyük olasılıkla bir günden az itibaren önceki kayıt aktarılırsa bant genişliğinden tasarruf etmek kayıt atlayabilirsiniz.
> 
> 

1. App.xaml.cs dosyasını açıp güncelleştirme **Initnotificationsasync** yöntemini kullanmak üzere `notifications` abone olmak için sınıf tabanlı kategorilerindeki.
   
        // *** Remove or comment out these lines *** 
        //var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
        //var hub = new NotificationHub("your hub name", "your listen connection string");
        //var result = await hub.RegisterNativeAsync(channel.Uri);
   
        var result = await notifications.SubscribeToCategories();
   
    Bu uygulama her başlatıldığında kategorileri yerel depodan alır ve bu kategorilerin bir kayda istekleri emin olur. **Initnotificationsasync** yöntemi, bir parçası olarak oluşturulmuş [Notification Hubs ile çalışmaya başlama] [ get-started] Öğreticisi.
2. MainPage.xaml.cs proje dosyasına aşağıdaki kodu ekleyin *OnNavigatedTo* yöntemi:
   
        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
            var categories = ((App)Application.Current).notifications.RetrieveCategories();
   
            if (categories.Contains("World")) WorldToggle.IsOn = true;
            if (categories.Contains("Politics")) PoliticsToggle.IsOn = true;
            if (categories.Contains("Business")) BusinessToggle.IsOn = true;
            if (categories.Contains("Technology")) TechnologyToggle.IsOn = true;
            if (categories.Contains("Science")) ScienceToggle.IsOn = true;
            if (categories.Contains("Sports")) SportsToggle.IsOn = true;
        }
   
    Bu, önceden kaydedilmiş kategorileri durumlarına dayalı ana sayfa güncelleştirir.

Uygulama tamamlanmıştır ve kategorileri kümesi kullanıcı kategorisi seçimine değiştiğinde bildirim hub'ınızla kaydolmak için kullanılan aygıt yerel depoda depolayabilirsiniz. Ardından, biz bu uygulamaya kategori bildirimleri gönderebilir bir arka uç tanımlayacaksınız.

## <a name="sending-tagged-notifications"></a>Etiketli bildirimleri gönderme
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-the-app-and-generate-notifications"></a>Uygulamayı çalıştırın ve bildirimler oluşturma
1. Visual Studio'da derleme ve uygulamayı başlatmak için F5 tuşuna basın.
   
    ![][1]
   
    Uygulama kullanıcı Arabirimi sağlayan bir dizi değiştirir sağlar Not abone olmak için kategorilerini seçin.
2. Bir veya daha fazla kategorileri değiştirir etkinleştirin ve ardından **abone ol**.
   
    Uygulama seçili kategorileri etiketlerine dönüştürür ve bildirim hub'ından seçili etiketleri için yeni bir cihaz kaydı ister. Kayıtlı kategorileri döndürülen ve iletişim kutusunda görüntülenir.
   
    ![][19]
3. Yeni bir bildirim arka ucundan aşağıdaki yollardan biriyle gönder:
   
   * **Konsol uygulaması:** konsol uygulaması başlatın.
   * **Java/PHP:** uygulama/betiğini çalıştırın.
     
     Seçili kategorileri için bildirimleri bildirimleri görünür.
     
     ![][14]

## <a name="next-steps"></a>Sonraki adımlar
Bu öğreticide biz kategoriye göre son dakika haberleri yayın öğrendiniz. Diğer gelişmiş Notification Hubs senaryoları vurgulayın aşağıdaki öğreticiler birini Tamamlanıyor göz önünde bulundurun:

* [Yerelleştirilmiş son dakika haberleri yayınlamak için Notification Hubs'ı kullanma]
  
    Gönderen yerelleştirilmiş bildirimlerini etkinleştirmek için en son haberleri uygulama genişletin öğrenin.

<!-- Anchors. -->
[Add category selection to the app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run the app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-breakingnews-win1.png

[14]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-toast-2.png


[19]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-reg-2.png

<!-- URLs.-->
[get-started]: /manage/services/notification-hubs/getting-started-windows-dotnet/
[Yerelleştirilmiş son dakika haberleri yayınlamak için Notification Hubs'ı kullanma]: /manage/services/notification-hubs/breaking-news-localized-dotnet/
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
