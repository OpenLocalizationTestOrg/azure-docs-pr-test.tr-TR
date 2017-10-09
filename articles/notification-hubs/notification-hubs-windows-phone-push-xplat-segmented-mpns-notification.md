---
title: "aaaUse bildirim hub'ları toosend son dakika haberleri (Windows Phone)"
description: "Azure Notification Hubs toouse etiketi haber tooa Windows Phone Uygulama yeni kayıtlar toosend içinde kullanın."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
ms.assetid: 42726bf5-cc82-438d-9eaa-238da3322d80
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 3519a8701105f88198afe288e59e9204420234db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-breaking-news"></a>Bildirim hub'ları toosend son dakika haberleri kullanın
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a>Genel Bakış
Bu konu, nasıl gösterir toouse Azure Notification Hubs toobroadcast en son haberleri bildirimleri tooa Windows Phone 8.0/8.1 Silverlight uygulaması. Windows mağazası veya Windows Phone 8.1 uygulama hedefliyorsanız Lütfen tootoohello bakın [Windows Evrensel](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) sürümü. Tamamlandığında, ilgilendiğiniz haber kategorileri sonu için mümkün tooregister olmalı ve yalnızca bu kategorilerin anında iletme bildirimlerini almak. Bu sayıda uygulama için genel bir desen bildirimleri gönderilen toobe toogroups daha önce bunları, örneğin, RSS Okuyucu, müzik fanlar, vb. için uygulamaları ilgi bildirilen kullanıcıların sahip olduğu bir senaryodur.

Yayın senaryoları etkin bir veya daha fazla dahil ederek *etiketleri* bir kayıt hello bildirim hub'oluştururken. Bildirimleri tooa etiketi gönderildiğinde kayıtlı tüm aygıtları hello etiketi hello bildirim alırsınız. Etiketleri yalnızca dizeleri olduğundan, önceden sağlanmış toobe gerekmez. Etiketler hakkında daha fazla bilgi için çok başvuran[bildirim hub'ları Yönlendirme ve etiket ifadeleri](notification-hubs-tags-segment-push-message.md).

## <a name="prerequisites"></a>Ön koşullar
Bu konu içinde oluşturduğunuz hello uygulama inşa edilmiştir [Notification Hubs ile çalışmaya başlama]. Bu öğreticiye başlamadan önce önce tamamlamış olmalıdır [Notification Hubs ile çalışmaya başlama].

## <a name="add-category-selection-toohello-app"></a>Kategori seçimi toohello uygulama Ekle
Merhaba ilk adım, hello kullanıcı tooselect kategorileri tooregister etkinleştirmek tooadd hello kullanıcı Arabirimi öğeleri tooyour varolan ana sayfasıdır. bir kullanıcı tarafından seçilen hello kategoriler hello aygıtta depolanır. Merhaba uygulama başlatıldığında bir aygıt kaydı bildirim hub'ınıza seçili hello kategorileri etiketler oluşturulur.

1. Merhaba MainPage.xaml proje dosyasını açın ve ardından hello yerine **kılavuz** adlı öğe `TitlePanel` ve `ContentPanel` koddan hello ile:
   
        <StackPanel x:Name="TitlePanel" Grid.Row="0" Margin="12,17,0,28">
            <TextBlock Text="Breaking News" Style="{StaticResource PhoneTextNormalStyle}" Margin="12,0"/>
            <TextBlock Text="Categories" Margin="9,-7,0,0" Style="{StaticResource PhoneTextTitle1Style}"/>
        </StackPanel>
   
        <Grid Name="ContentPanel" Grid.Row="1" Margin="12,0,12,0">
            <Grid.RowDefinitions>
                <RowDefinition Height="auto"/>
                <RowDefinition Height="auto" />
                <RowDefinition Height="auto" />
                <RowDefinition Height="auto" />
            </Grid.RowDefinitions>
            <Grid.ColumnDefinitions>
                <ColumnDefinition />
                <ColumnDefinition />
            </Grid.ColumnDefinitions>
            <CheckBox Name="WorldCheckBox" Grid.Row="0" Grid.Column="0">World</CheckBox>
            <CheckBox Name="PoliticsCheckBox" Grid.Row="1" Grid.Column="0">Politics</CheckBox>
            <CheckBox Name="BusinessCheckBox" Grid.Row="2" Grid.Column="0">Business</CheckBox>
            <CheckBox Name="TechnologyCheckBox" Grid.Row="0" Grid.Column="1">Technology</CheckBox>
            <CheckBox Name="ScienceCheckBox" Grid.Row="1" Grid.Column="1">Science</CheckBox>
            <CheckBox Name="SportsCheckBox" Grid.Row="2" Grid.Column="1">Sports</CheckBox>
            <Button Name="SubscribeButton" Content="Subscribe" HorizontalAlignment="Center" Grid.Row="3" Grid.Column="0" Grid.ColumnSpan="2" Click="SubscribeButton_Click" />
        </Grid>
2. Merhaba projesinde adlı yeni bir sınıf oluşturun **bildirimleri**, hello eklemek **ortak** değiştiricisi toohello sınıf tanımının sonra hello aşağıdakileri ekleyin **kullanarak** deyimleri toohello yeni kod dosyası:
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
        using System.IO.IsolatedStorage;
        using System.Windows;
3. Kopya hello aşağıdaki kod hello yeni **bildirimleri** sınıfı:
   
        private NotificationHub hub;
   
        // Registration task toocomplete registration in hello ChannelUriUpdated event handler
        private TaskCompletionSource<Registration> registrationTask;
   
        public Notifications(string hubName, string listenConnectionString)
        {
            hub = new NotificationHub(hubName, listenConnectionString);
        }
   
        public IEnumerable<string> RetrieveCategories()
        {
            var categories = (string)IsolatedStorageSettings.ApplicationSettings["categories"];
            return categories != null ? categories.Split(',') : new string[0];
        }
   
        public async Task<Registration> StoreCategoriesAndSubscribe(IEnumerable<string> categories)
        {
            var categoriesAsString = string.Join(",", categories);
            var settings = IsolatedStorageSettings.ApplicationSettings;
            if (!settings.Contains("categories"))
            {
                settings.Add("categories", categoriesAsString);
            }
            else
            {
                settings["categories"] = categoriesAsString;
            }
            settings.Save();
   
            return await SubscribeToCategories();
        }
   
        public async Task<Registration> SubscribeToCategories()
        {
            registrationTask = new TaskCompletionSource<Registration>();
   
            var channel = HttpNotificationChannel.Find("MyPushChannel");
   
            if (channel == null)
            {
                channel = new HttpNotificationChannel("MyPushChannel");
                channel.Open();
                channel.BindToShellToast();
                channel.ChannelUriUpdated += channel_ChannelUriUpdated;
   
                // This is optional, used tooreceive notifications while hello app is running.
                channel.ShellToastNotificationReceived += channel_ShellToastNotificationReceived;
            }
   
            // If channel.ChannelUri is not null, we will complete hello registrationTask here.  
            // If it is null, hello registrationTask will be completed in hello ChannelUriUpdated event handler.
            if (channel.ChannelUri != null)
            {
                await RegisterTemplate(channel.ChannelUri);
            }
   
            return await registrationTask.Task;
        }
   
        async void channel_ChannelUriUpdated(object sender, NotificationChannelUriEventArgs e)
        {
            await RegisterTemplate(e.ChannelUri);
        }
   
        async Task<Registration> RegisterTemplate(Uri channelUri)
        {
            // Using a template registration toosupport notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyMPNS = "<wp:Notification xmlns:wp=\"WPNotification\">" +
                                                "<wp:Toast>" +
                                                    "<wp:Text1>$(messageParam)</wp:Text1>" +
                                                "</wp:Toast>" +
                                            "</wp:Notification>";
   
            // hello stored categories tags are passed with hello template registration.
   
            registrationTask.SetResult(await hub.RegisterTemplateAsync(channelUri.ToString(), 
                templateBodyMPNS, "simpleMPNSTemplateExample", this.RetrieveCategories()));
   
            return await registrationTask.Task;
        }
   
        // This is optional. It is used tooreceive notifications while hello app is running.
        void channel_ShellToastNotificationReceived(object sender, NotificationEventArgs e)
        {
            StringBuilder message = new StringBuilder();
            string relativeUri = string.Empty;
   
            message.AppendFormat("Received Toast {0}:\n", DateTime.Now.ToShortTimeString());
   
            // Parse out hello information that was part of hello message.
            foreach (string key in e.Collection.Keys)
            {
                message.AppendFormat("{0}: {1}\n", key, e.Collection[key]);
   
                if (string.Compare(
                    key,
                    "wp:Param",
                    System.Globalization.CultureInfo.InvariantCulture,
                    System.Globalization.CompareOptions.IgnoreCase) == 0)
                {
                    relativeUri = e.Collection[key];
                }
            }
   
            // Display a dialog of all hello fields in hello toast.
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() => 
            { 
                MessageBox.Show(message.ToString()); 
            });
        }

    Bu sınıf hello yalıtılmış depolama toostore hello kategorilerini bu aygıtın tooreceive olduğunu haber kullanır. Yöntemleri tooregister kullanarak bu kategorilerin de içeren bir [şablonu](notification-hubs-templates-cross-platform-push-messages.md) bildirimi kaydı.


1. Özellik toohello aşağıdaki hello Hello App.xaml.cs proje dosyasında eklemek **uygulama** sınıfı. Hello yerine `<hub name>` ve `<connection string with listen access>` bildirim hub'ı adı ve hello için bağlantı dizenizi yer tutucularını *DefaultListenSharedAccessSignature* daha önce edindiğiniz.
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
   > [!NOTE]
   > Bir istemci uygulaması ile dağıtılmış kimlik bilgileri genellikle güvenli olmadığından, yalnızca hello anahtarını dinleme erişim için istemci uygulamanızı dağıtmak. Bildirimler, ancak var olan kayıtlar için uygulama tooregister değiştirilemez erişimi etkinleştirir dinleyin ve bildirim gönderilemiyor. Merhaba tam erişim tuşu bir güvenli arka uç hizmetinde bildirimleri gönderme ve var olan kayıtlar değiştirmek için kullanılır.
   > 
   > 
2. MainPage.xaml.cs dosyasında hello aşağıdaki satırı ekleyin:
   
        using Windows.UI.Popups;
3. Merhaba MainPage.xaml.cs proje dosyasında yöntemi aşağıdaki hello ekleyin:
   
        private async void SubscribeButton_Click(object sender, RoutedEventArgs e)
        {
          var categories = new HashSet<string>();
          if (WorldCheckBox.IsChecked == true) categories.Add("World");
          if (PoliticsCheckBox.IsChecked == true) categories.Add("Politics");
          if (BusinessCheckBox.IsChecked == true) categories.Add("Business");
          if (TechnologyCheckBox.IsChecked == true) categories.Add("Technology");
          if (ScienceCheckBox.IsChecked == true) categories.Add("Science");
          if (SportsCheckBox.IsChecked == true) categories.Add("Sports");
   
          var result = await ((App)Application.Current).notifications.StoreCategoriesAndSubscribe(categories);
   
          MessageBox.Show("Subscribed to: " + string.Join(",", categories) + " on registration id : " +
             result.RegistrationId);
        }
   
    Bu yöntem kategorileri ve kullandığı hello listesini oluşturur **bildirimleri** sınıf toostore hello hello yerel depolama listesinde ve bildirim hub'ınıza hello karşılık gelen etiketleri kaydedin. Kategoriler değiştirildiğinde hello kayıt hello yeni kategorileri ile yeniden oluşturulur.

Uygulamanızı mümkün toostore kategorileri kümesi hello cihazda yerel depolama sunulmuştur ve kategorisi seçimine hello kullanıcı değişiklikleri hello her hello bildirim hub'ı ile kaydedin.

## <a name="register-for-notifications"></a>Bildirimler için kaydolun
Yerel depolamada depolanan hello kategorileri kullanarak başlangıçta hello bildirim hub'ı ile adımları kaydedin.

> [!NOTE]
> Merhaba kanal URI'sini hello Microsoft anında iletme bildirimi Hizmeti'ni (MPNS) tarafından atanan herhangi bir zamanda değiştiğinden bildirimleri için tooavoid bildirim hataları sık kaydetmelisiniz. Bu hello uygulama her başlatıldığında bu örnek için bildirimleri kaydeder. Bir günden az hello önceki kayıt itibaren aktarılırsa, sık çalıştırılan uygulamalar için günde bir kereden fazla, büyük olasılıkla kayıt toopreserve bant genişliği atlayabilirsiniz.
> 
> 

1. Merhaba App.xaml.cs dosyasını açın ve hello ekleyin **zaman uyumsuz** değiştiricisi çok**Application_Launching** eklediğiniz yöntemi ve Değiştir hello Notification Hubs kayıt kodu [Notification Hubs ile çalışmaya başlama] koddan hello ile:
   
        private async void Application_Launching(object sender, LaunchingEventArgs e)
        {
            var result = await notifications.SubscribeToCategories();
   
            if (result != null)
                System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
                {
                    MessageBox.Show("Registration Id :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
                });
        }
   
    Bu hello uygulama her başlatıldığında hello kategorileri yerel depodan alır ve bu kategorileri için bir kayıt isteklerini emin olur.
2. Merhaba MainPage.xaml.cs proje dosyasında hello uygulayan kod aşağıdaki hello eklemek **OnNavigatedTo** yöntemi:
   
        protected override void OnNavigatedTo(NavigationEventArgs e)
        {
            var categories = ((App)Application.Current).notifications.RetrieveCategories();
   
            if (categories.Contains("World")) WorldCheckBox.IsChecked = true;
            if (categories.Contains("Politics")) PoliticsCheckBox.IsChecked = true;
            if (categories.Contains("Business")) BusinessCheckBox.IsChecked = true;
            if (categories.Contains("Technology")) TechnologyCheckBox.IsChecked = true;
            if (categories.Contains("Science")) ScienceCheckBox.IsChecked = true;
            if (categories.Contains("Sports")) SportsCheckBox.IsChecked = true;
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
   
    ![][2]
3. Kategoriler tamamlandı aboneliği olan bir onay aldıktan sonra her kategori için hello konsol uygulama toosend bildirimleri çalıştırın. Yalnızca abone olduğunuz hello kategorileri için bir bildirim alırsınız emin olun.
   
    ![][3]

Bu konuda tamamladınız.

<!--##Next steps

In this tutorial we learned how toobroadcast breaking news by category. Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:

+ [Use Notification Hubs toobroadcast localized breaking news]

    Learn how tooexpand hello breaking news app tooenable sending localized notifications.

+ [Notify users with Notification Hubs]

    Learn how toopush notifications toospecific authenticated users. This is a good solution for sending notifications only toospecific users.
-->

<!-- Anchors. -->
[Add category selection toohello app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run hello app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-breakingnews.png
[2]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-registration.png
[3]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-toast.png



<!-- URLs.-->
[Notification Hubs ile çalışmaya başlama]: /manage/services/notification-hubs/get-started-notification-hubs-wp8/
[Use Notification Hubs toobroadcast localized breaking news]: ../breakingnews-localized-wp8.md
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users/
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor Windows Phone]: ??

