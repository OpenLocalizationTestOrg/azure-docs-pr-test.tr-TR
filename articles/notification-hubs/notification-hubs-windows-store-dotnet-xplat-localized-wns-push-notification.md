---
title: "aaaNotification Hubs yerelleştirilmiş çiğnemekten haber Öğreticisi"
description: "Son dakika haberi bildirimleri toouse Azure Notification Hubs toosend nasıl yerelleştirilmiş öğrenin."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: 
ms.assetid: c454f5a3-a06b-45ac-91c7-f91210889b25
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: d273a6b384df311dea7b76ca83ccd94d9a989c4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-notification-hubs-toosend-localized-breaking-news"></a>Bildirim hub'ları yerelleştirilmiş toosend son dakika haberleri kullanın
> [!div class="op_single_selector"]
> * [Windows mağazası C#](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [iOS](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a>Genel Bakış
Bu konu, nasıl gösterir toouse hello **şablonu** dil ve cihaz tarafından yerelleştirilmiş haberi bildirimleri çiğnemekten Azure Notification Hubs toobroadcast özelliğidir. Bu öğreticide oluşturduğunuz hello Windows mağazası uygulaması ile başlamanız [son dakika haberleri Notification Hubs kullanma toosend]. Tamamlandığında, ilgilendiğiniz kategorileri için mümkün tooregister olacaktır, hangi tooreceive hello bildirimleri bir dil belirtin ve yalnızca anında iletme bildirimlerini seçili hello kategorileri için o dilde alırsınız.

İki bölümden toothis senaryo vardır:

* Merhaba Windows mağazası uygulaması istemci cihazları toospecify bir dil ve haber kategorileri çiğnemekten toosubscribe toodifferent sağlar;
* Merhaba arka uç yayınlar hello kullanarak hello bildirimleri **etiketi** ve **şablonu** Azure bildirim hub'larını feautres.

## <a name="prerequisites"></a>Ön koşullar
Önceden hello tamamlamış olmalıdır [son dakika haberleri Notification Hubs kullanma toosend] öğretici ve bu öğreticinin bu kodu doğrudan derlemeler için kullanılabilir, hello koduna sahip.

Ayrıca Visual Studio 2012 veya üzeri gerekir.

## <a name="template-concepts"></a>Şablon kavramları
İçinde [son dakika haberleri Notification Hubs kullanma toosend] kullanılan bir uygulama yerleşik **etiketleri** toosubscribe toonotifications farklı haber kategorileri için.
Birçok uygulama, ancak, birden çok pazarda hedef ve yerelleştirme gerektirir. Bunun anlamı hello bildirimleri kendilerini Merhaba içeriğine sahip yerelleştirilmiş toobe ve teslim toohello cihaz kümesini düzeltin.
Bu konudaki göstereceğiz nasıl toouse hello **şablonu** özellik bildirim hub'larını tooeasily teslim yerelleştirilmiş son dakika haberi bildirimleri.

Not: tek yönlü toosend yerelleştirilmiş bildirimleri toocreate her etiket birden çok sürümünün olduğu. Örneğin, toosupport İngilizce, Fransızca ve Mandarin, üç farklı etiketler world haberler için ihtiyacımız: "world_en", "world_fr" ve "world_ch". Toosend sonra hello world haber tooeach bu etiketlerin yerelleştirilmiş bir sürümü gerekir. Bu konudaki şablonları tooavoid hello artışı etiketleri ve birden fazla ileti gönderme hello gereksinimi kullanın.

Yüksek bir düzeyde bir şekilde toospecify şablonlarıdır nasıl belirli bir aygıt bir bildirim almanız gerekir. Merhaba şablon, uygulama arka ucu tarafından gönderilen Merhaba ileti parçası olan tooproperties bakarak hello tam yük biçimi belirtir. Örneğimizde, biz tüm desteklenen diller içeren bir yerel ayar belirsiz ileti gönderir:

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

Ardından cihazlarını toohello doğru özellik başvuran bir şablonla kaydetmek sağlayacaktır. Örneği için tooreceive isteyen bir Windows mağazası uygulaması şablonu ile ilgili tüm etiketleri aşağıdaki hello için basit bir bildirim iletisi kaydeder:

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">$(News_English)</text>
        </binding>
      </visual>
    </toast>



Şablonlar, daha fazla bilgi bulabilir hakkında içinde çok güçlü bir özellik olan bizim [şablonları](notification-hubs-templates-cross-platform-push-messages.md) makalesi. 

## <a name="hello-app-user-interface"></a>Merhaba uygulama kullanıcı arabirimi
Biz şimdi hello konuda oluşturulan hello çiğnemekten haber uygulama değiştirecek [son dakika haberleri Notification Hubs kullanma toosend] toosend yerelleştirilmiş şablonları kullanarak son dakika haberleri.

Windows mağazası uygulamanızı:

MainPage.xaml tooinclude yerel ayar combobox değiştirin:

    <Grid Margin="120, 58, 120, 80"  
            Background="{StaticResource ApplicationPageBackgroundThemeBrush}">
        <Grid.RowDefinitions>
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
            <RowDefinition />
        </Grid.RowDefinitions>
        <Grid.ColumnDefinitions>
            <ColumnDefinition />
            <ColumnDefinition />
        </Grid.ColumnDefinitions>
        <TextBlock Grid.Row="0" Grid.Column="0" Grid.ColumnSpan="2"  TextWrapping="Wrap" Text="Breaking News" FontSize="42" VerticalAlignment="Top"/>
        <ComboBox Name="Locale" HorizontalAlignment="Left" VerticalAlignment="Center" Width="200" Grid.Row="1" Grid.Column="0">
            <x:String>English</x:String>
            <x:String>French</x:String>
            <x:String>Mandarin</x:String>
        </ComboBox>
        <ToggleSwitch Header="World" Name="WorldToggle" Grid.Row="2" Grid.Column="0"/>
        <ToggleSwitch Header="Politics" Name="PoliticsToggle" Grid.Row="3" Grid.Column="0"/>
        <ToggleSwitch Header="Business" Name="BusinessToggle" Grid.Row="4" Grid.Column="0"/>
        <ToggleSwitch Header="Technology" Name="TechnologyToggle" Grid.Row="2" Grid.Column="1"/>
        <ToggleSwitch Header="Science" Name="ScienceToggle" Grid.Row="3" Grid.Column="1"/>
        <ToggleSwitch Header="Sports" Name="SportsToggle" Grid.Row="4" Grid.Column="1"/>
        <Button Content="Subscribe" HorizontalAlignment="Center" Grid.Row="5" Grid.Column="0" Grid.ColumnSpan="2" Click="SubscribeButton_Click" />
    </Grid>

## <a name="building-hello-windows-store-client-app"></a>Merhaba Windows mağazası istemci uygulaması oluşturma
1. Yerel ayar parametresi tooyour bildirimleri sınıfınıza ekleyin *StoreCategoriesAndSubscribe* ve *SubscribeToCateories* yöntemleri.
   
        public async Task<Registration> StoreCategoriesAndSubscribe(string locale, IEnumerable<string> categories)
        {
            ApplicationData.Current.LocalSettings.Values["categories"] = string.Join(",", categories);
            ApplicationData.Current.LocalSettings.Values["locale"] = locale;
            return await SubscribeToCategories(categories);
        }
   
        public async Task<Registration> SubscribeToCategories(string locale, IEnumerable<string> categories = null)
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            if (categories == null)
            {
                categories = RetrieveCategories();
            }
   
            // Using a template registration. This makes supporting notifications across other platforms much easier.
            // Using hello localized tags based on locale selected.
            string templateBodyWNS = String.Format("<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(News_{0})</text></binding></visual></toast>", locale);
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "localizedWNSTemplateExample", categories);
        }
   
    Arama hello yerine unutmayın *RegisterNativeAsync* diyoruz yöntemi *RegisterTemplateAsync*: biz hangi hello şablon hello bölgesel ayarına bağlıdır belirli bildirim biçimi kaydediliyor. Biz de hello şablonu ("localizedWNSTemplateExample") için bir ad sağlayın, çünkü tooregister (örneğin biri bildirimleri) ve biri kutucuklar için birden fazla şablon istiyoruz ve tooname ihtiyacımız bunları toobe mümkün tooupdate sipariş veya silin.
   
    Bir aygıt hello aynı etiketi sonuçlanır hedefleme gelen ileti etiketi ile birden fazla şablon kaydederse birden fazla bildirim toohello aygıt (her şablon için bir tane) teslim unutmayın. Bu davranış, Hello aynı mantıksal ileti tooresult örneği için bir Windows mağazası uygulamasında bir gösterge ve bildirim gösteren birden çok görsel bildirimler sahip yararlıdır.
2. Yöntem tooretrieve hello depolanan yerel aşağıdaki hello ekleyin:
   
        public string RetrieveLocale()
        {
            var locale = (string) ApplicationData.Current.LocalSettings.Values["locale"];
            return locale != null ? locale : "English";
        }
3. MainPage.xaml.cs dosyasında, düğme güncelleştirme işleyicisi hello geçerli hello yerel açılan kutu değerini almak ve gösterildiği gibi toohello çağrısı toohello bildirimleri sınıfı, sağlayarak'ı tıklatın:
   
        private async void SubscribeButton_Click(object sender, RoutedEventArgs e)
        {
            var locale = (string)Locale.SelectedItem;
   
            var categories = new HashSet<string>();
            if (WorldToggle.IsOn) categories.Add("World");
            if (PoliticsToggle.IsOn) categories.Add("Politics");
            if (BusinessToggle.IsOn) categories.Add("Business");
            if (TechnologyToggle.IsOn) categories.Add("Technology");
            if (ScienceToggle.IsOn) categories.Add("Science");
            if (SportsToggle.IsOn) categories.Add("Sports");
   
            var result = await ((App)Application.Current).notifications.StoreCategoriesAndSubscribe(locale,
                 categories);
   
            var dialog = new MessageDialog("Locale: " + locale + " Subscribed to: " + 
                string.Join(",", categories) + " on registration Id: " + result.RegistrationId);
            dialog.Commands.Add(new UICommand("OK"));
            await dialog.ShowAsync();
        }
4. Son olarak, App.xaml.cs dosyasında emin tooupdate olun, `InitNotificationsAsync` yöntemi tooretrieve hello yerel ayar ve abone olurken kullanın:
   
        private async void InitNotificationsAsync()
        {
            var result = await notifications.SubscribeToCategories(notifications.RetrieveLocale());
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

## <a name="send-localized-notifications-from-your-back-end"></a>Arka ucunuz yerelleştirilmiş bildirimleri gönderme
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

<!-- Anchors. -->
[Template concepts]: #concepts
[hello app user interface]: #ui
[Building hello Windows Store client app]: #building-client
[Send notifications from your back-end]: #send
[Next Steps]:#next-steps

<!-- Images. -->

<!-- URLs. -->
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Notify users with Notification Hubs: Mobile Services]: /manage/services/notification-hubs/notify-users
[son dakika haberleri Notification Hubs kullanma toosend]: /manage/services/notification-hubs/breaking-news-dotnet

[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-dotnet
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-dotnet
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-dotnet
[Push notifications tooapp users]: /develop/mobile/tutorials/push-notifications-to-app-users-dotnet
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-dotnet
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-toofor iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[Notification Hubs How-toofor Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
