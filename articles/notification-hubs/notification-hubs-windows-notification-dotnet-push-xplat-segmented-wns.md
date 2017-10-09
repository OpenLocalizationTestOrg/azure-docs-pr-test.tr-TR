---
title: "aaaUse bildirim hub'ları toosend son dakika haberleri (Evrensel Windows)"
description: "Azure Notification Hubs haber tooa Evrensel Windows uygulaması çiğnemekten hello kayıt toosend etiketleri kullanın."
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
ms.openlocfilehash: f102d286d2c7bd387fcfa2c7eab2ba31a0298517
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a>Bildirim hub'ları toosend son dakika haberleri kullanın
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>Genel Bakış
Bu konu, nasıl gösterir toouse Azure Notification Hubs toobroadcast haber bildirimleri tooa Windows mağazası veya Windows Phone 8.1 (Silverlight olmayan) uygulamasına kesiliyor. Windows Phone 8.1 Silverlight hedefliyorsanız Lütfen toohello bakın [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) sürümü. Tamamlandığında, ilgilendiğiniz haber kategorileri sonu için mümkün tooregister olmalı ve yalnızca bu kategorilerin anında iletme bildirimlerini almak. Bu sayıda uygulama için genel bir desen bildirimleri gönderilen toobe toogroups daha önce bunları, örneğin RSS Okuyucu uygulamaları müzik fanları için ilgi derlendiğinden vb. kullanıcıların sahip olduğu bir senaryodur. 

Yayın senaryoları etkin bir veya daha fazla dahil ederek *etiketleri* bir kayıt hello bildirim hub'oluştururken. Bildirimleri tooa etiketi gönderildiğinde kayıtlı tüm aygıtları hello etiketi hello bildirim alırsınız. Etiketleri yalnızca dizeleri olduğundan, önceden sağlanmış toobe gerekmez. Etiketler hakkında daha fazla bilgi için çok başvuran[bildirim hub'ları Yönlendirme ve etiket ifadeleri](notification-hubs-tags-segment-push-message.md).

> [!NOTE]
> Windows mağazası ve Windows Phone projeleri sürüm 8.1 ve önceki Visual Studio 2017 içinde desteklenmez.  Daha fazla bilgi için bkz. [Visual Studio 2017 Platform Desteği ve Uyumluluk](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs). 

## <a name="prerequisites"></a>Ön koşullar
Bu konu içinde oluşturduğunuz hello uygulama inşa edilmiştir [Notification Hubs ile çalışmaya başlama][get-started]. Bu öğreticiye başlamadan önce önce tamamlamış olmalıdır [Notification Hubs ile çalışmaya başlama][get-started].

## <a name="add-category-selection-toohello-app"></a>Kategori seçimi toohello uygulama Ekle
Merhaba ilk adım, hello kullanıcı tooselect kategorileri tooregister etkinleştirmek tooadd hello kullanıcı Arabirimi öğeleri tooyour varolan ana sayfasıdır. bir kullanıcı tarafından seçilen hello kategoriler hello aygıtta depolanır. Merhaba uygulama başlatıldığında bir aygıt kaydı bildirim hub'ınıza seçili hello kategorileri etiketler oluşturulur.

1. Açık hello MainPage.xaml proje dosyası sonra kopyalama hello hello kodda aşağıdaki **kılavuz** öğe:
   
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
2. Merhaba sağ tıklayın **paylaşılan** proje ve adlı yeni bir sınıf ekleyin **bildirimleri**, hello eklemek **ortak** değiştiricisi toohello sınıf tanımının, ardından aşağıdaki hello ekleyin**kullanarak** deyimleri toohello yeni kod dosyası:
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.Storage;
        using System.Threading.Tasks;
3. Kopya hello aşağıdaki kod hello yeni **bildirimleri** sınıfı:
   
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
   
            // Using a template registration toosupport notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyWNS = "<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(messageParam)</text></binding></visual></toast>";
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "simpleWNSTemplateExample",
                    categories);
        }
   
    Bu sınıf hello yerel depolama toostore hello kategorilerini bu aygıtta tooreceive olduğunu haber kullanır. Arama hello yerine unutmayın *RegisterNativeAsync* diyoruz yöntemi *RegisterTemplateAsync* tooregister şablonu kayıt kullanarak hello kategorileri için. 
   
    Biz de hello şablonu ("simpleWNSTemplateExample") için bir ad sağlayın, çünkü tooregister (örneğin biri bildirimleri) ve biri kutucuklar için birden fazla şablon istiyoruz ve tooname ihtiyacımız bunları toobe mümkün tooupdate sipariş veya silin.
   
    Bir aygıt hello aynı etiketi sonuçlanır hedefleme gelen ileti etiketi ile birden fazla şablon kaydederse birden fazla bildirim toohello aygıt (her şablon için bir tane) teslim unutmayın. Bu davranış, Hello aynı mantıksal ileti tooresult örneği için bir Windows mağazası uygulamasında bir gösterge ve bildirim gösteren birden çok görsel bildirimler sahip yararlıdır.
   
    Şablonlar hakkında daha fazla bilgi için bkz: [şablonları](notification-hubs-templates-cross-platform-push-messages.md).
4. Özellik toohello aşağıdaki hello Hello App.xaml.cs proje dosyasında eklemek **uygulama** sınıfı:
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
    Bu özellik kullanılan toocreate ve erişimi olan bir **bildirimleri** örneği.
   
    Kod yukarıda Hello hello yerine `<hub name>` ve `<connection string with listen access>` bildirim hub'ı adı ve hello için bağlantı dizenizi yer tutucularını *DefaultListenSharedAccessSignature* daha önce edindiğiniz.
   
   > [!NOTE]
   > Bir istemci uygulaması ile dağıtılmış kimlik bilgileri genellikle güvenli olmadığından, yalnızca hello anahtarını dinleme erişim için istemci uygulamanızı dağıtmak. Bildirimler, ancak var olan kayıtlar için uygulama tooregister değiştirilemez erişimi etkinleştirir dinleyin ve bildirim gönderilemiyor. Merhaba tam erişim tuşu bir güvenli arka uç hizmetinde bildirimleri gönderme ve var olan kayıtlar değiştirmek için kullanılır.
   > 
   > 
5. MainPage.xaml.cs dosyasında hello aşağıdaki satırı ekleyin:
   
        using Windows.UI.Popups;
6. Merhaba MainPage.xaml.cs proje dosyasında yöntemi aşağıdaki hello ekleyin:
   
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
   
    Bu yöntem kategorileri ve kullandığı hello listesini oluşturur **bildirimleri** sınıf toostore hello hello yerel depolama listesinde ve bildirim hub'ınıza hello karşılık gelen etiketleri kaydedin. Kategoriler değiştirildiğinde hello kayıt hello yeni kategorileri ile yeniden oluşturulur.

Uygulamanızı mümkün toostore kategorileri kümesi hello cihazda yerel depolama sunulmuştur ve kategorisi seçimine hello kullanıcı değişiklikleri hello her hello bildirim hub'ı ile kaydedin.

## <a name="register-for-notifications"></a>Bildirimler için kaydolun
Yerel depolamada depolanan hello kategorileri kullanarak başlangıçta hello bildirim hub'ı ile adımları kaydedin.

> [!NOTE]
> Merhaba kanal URI'sini hello Windows bildirim Hizmeti'ni (WNS) tarafından atanan herhangi bir zamanda değiştiğinden bildirimleri için tooavoid bildirim hataları sık kaydetmelisiniz. Bu hello uygulama her başlatıldığında bu örnek bir bildirime kaydolur. Bir günden az hello önceki kayıt itibaren aktarılırsa, sık çalıştırılan uygulamalar için günde bir kereden fazla, büyük olasılıkla kayıt toopreserve bant genişliği atlayabilirsiniz.
> 
> 

1. Açık hello App.xaml.cs dosyasını ve güncelleştirme hello **Initnotificationsasync** yöntemi toouse hello `notifications` sınıfı toosubscribe alarak kategorilere göre.
   
        // *** Remove or comment out these lines *** 
        //var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
        //var hub = new NotificationHub("your hub name", "your listen connection string");
        //var result = await hub.RegisterNativeAsync(channel.Uri);
   
        var result = await notifications.SubscribeToCategories();
   
    Bu hello uygulama her başlatıldığında hello kategorileri yerel depodan alır ve bu kategorilerin bir kayda istekleri emin olur. Merhaba **Initnotificationsasync** yöntemi hello bir parçası olarak oluşturulmuş [Notification Hubs ile çalışmaya başlama] [ get-started] Öğreticisi.
2. Merhaba MainPage.xaml.cs proje dosyasında kodu toohello aşağıdaki hello eklemek *OnNavigatedTo* yöntemi:
   
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
   
    Merhaba durumlarına önceden dayalı bu güncelleştirmeleri hello ana bir sayfayı kategorileri kaydedildi.

Merhaba uygulama tamamlanmıştır ve kategorisi seçimine hello kullanıcı değişiklikleri hello her kategori kümesini hello aygıt kullanılan yerel depolama tooregister hello bildirim hub'ı ile depolayabilirsiniz. Ardından, biz kategori bildirimleri toothis uygulamanın gönderebileceği bir arka uç tanımlayacaksınız.

## <a name="sending-tagged-notifications"></a>Etiketli bildirimleri gönderme
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a>Merhaba uygulamayı çalıştırın ve bildirimler oluşturma
1. Visual Studio'da F5 toocompile tuşuna basın ve hello uygulamayı başlatın.
   
    ![][1]
   
    Bir dizi kullanıcı Arabirimi sağlar bu hello uygulama değiştirir Not hello kategorileri toosubscribe seçmenize olanak sağlar.
2. Bir veya daha fazla kategorileri değiştirir etkinleştirin ve ardından **abone ol**.
   
    Merhaba uygulama seçili hello kategoriler etiketleri dönüştürür ve seçili hello etiketleri için yeni bir cihaz kaydı hello bildirim hub'ından ister. Merhaba kayıtlı kategorileri döndürülen ve iletişim kutusunda görüntülenir.
   
    ![][19]
3. Merhaba arka yolları aşağıdaki hello birinde yeni bir bildirim gönder:
   
   * **Konsol uygulaması:** hello konsol uygulaması başlatın.
   * **Java/PHP:** uygulama/betiğini çalıştırın.
     
     Seçili hello kategorileri için bildirimler bildirimleri görünür.
     
     ![][14]

## <a name="next-steps"></a>Sonraki adımlar
Biz bu öğreticide öğrenilen nasıl kategoriye göre son dakika haberleri toobroadcast. Diğer gelişmiş Notification Hubs senaryoları vurgulayın öğreticileri aşağıdaki hello birini Tamamlanıyor göz önünde bulundurun:

* [Bildirim hub'ları yerelleştirilmiş toobroadcast son dakika haberleri kullanın]
  
    Haber uygulama tooenable göndermek çiğnemekten tooexpand hello bildirimleri nasıl yerelleştirilmiş öğrenin.

<!-- Anchors. -->
[Add category selection toohello app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run hello app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-breakingnews-win1.png

[14]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-toast-2.png


[19]: ./media/notification-hubs-windows-store-dotnet-send-breaking-news/notification-hub-windows-reg-2.png

<!-- URLs.-->
[get-started]: /manage/services/notification-hubs/getting-started-windows-dotnet/
[Bildirim hub'ları yerelleştirilmiş toobroadcast son dakika haberleri kullanın]: /manage/services/notification-hubs/breaking-news-localized-dotnet/
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
