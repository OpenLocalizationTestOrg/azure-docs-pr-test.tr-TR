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
# <a name="use-notification-hubs-toosend-localized-breaking-news"></a><span data-ttu-id="9aa00-103">Bildirim hub'ları yerelleştirilmiş toosend son dakika haberleri kullanın</span><span class="sxs-lookup"><span data-stu-id="9aa00-103">Use Notification Hubs toosend localized breaking news</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9aa00-104">Windows mağazası C#</span><span class="sxs-lookup"><span data-stu-id="9aa00-104">Windows Store C#</span></span>](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [<span data-ttu-id="9aa00-105">iOS</span><span class="sxs-lookup"><span data-stu-id="9aa00-105">iOS</span></span>](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="9aa00-106">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="9aa00-106">Overview</span></span>
<span data-ttu-id="9aa00-107">Bu konu, nasıl gösterir toouse hello **şablonu** dil ve cihaz tarafından yerelleştirilmiş haberi bildirimleri çiğnemekten Azure Notification Hubs toobroadcast özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="9aa00-107">This topic shows you how toouse hello **template** feature of Azure Notification Hubs toobroadcast breaking news notifications that have been localized by language and device.</span></span> <span data-ttu-id="9aa00-108">Bu öğreticide oluşturduğunuz hello Windows mağazası uygulaması ile başlamanız [son dakika haberleri Notification Hubs kullanma toosend].</span><span class="sxs-lookup"><span data-stu-id="9aa00-108">In this tutorial you start with hello Windows Store app created in [Use Notification Hubs toosend breaking news].</span></span> <span data-ttu-id="9aa00-109">Tamamlandığında, ilgilendiğiniz kategorileri için mümkün tooregister olacaktır, hangi tooreceive hello bildirimleri bir dil belirtin ve yalnızca anında iletme bildirimlerini seçili hello kategorileri için o dilde alırsınız.</span><span class="sxs-lookup"><span data-stu-id="9aa00-109">When complete, you will be able tooregister for categories you are interested in, specify a language in which tooreceive hello notifications, and receive only push notifications for hello selected categories in that language.</span></span>

<span data-ttu-id="9aa00-110">İki bölümden toothis senaryo vardır:</span><span class="sxs-lookup"><span data-stu-id="9aa00-110">There are two parts toothis scenario:</span></span>

* <span data-ttu-id="9aa00-111">Merhaba Windows mağazası uygulaması istemci cihazları toospecify bir dil ve haber kategorileri çiğnemekten toosubscribe toodifferent sağlar;</span><span class="sxs-lookup"><span data-stu-id="9aa00-111">hello Windows Store app allows client devices toospecify a language, and toosubscribe toodifferent breaking news categories;</span></span>
* <span data-ttu-id="9aa00-112">Merhaba arka uç yayınlar hello kullanarak hello bildirimleri **etiketi** ve **şablonu** Azure bildirim hub'larını feautres.</span><span class="sxs-lookup"><span data-stu-id="9aa00-112">hello back-end broadcasts hello notifications, using hello **tag** and **template** feautres of Azure Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9aa00-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9aa00-113">Prerequisites</span></span>
<span data-ttu-id="9aa00-114">Önceden hello tamamlamış olmalıdır [son dakika haberleri Notification Hubs kullanma toosend] öğretici ve bu öğreticinin bu kodu doğrudan derlemeler için kullanılabilir, hello koduna sahip.</span><span class="sxs-lookup"><span data-stu-id="9aa00-114">You must have already completed hello [Use Notification Hubs toosend breaking news] tutorial and have hello code available, because this tutorial builds directly upon that code.</span></span>

<span data-ttu-id="9aa00-115">Ayrıca Visual Studio 2012 veya üzeri gerekir.</span><span class="sxs-lookup"><span data-stu-id="9aa00-115">You also need Visual Studio 2012 or later.</span></span>

## <a name="template-concepts"></a><span data-ttu-id="9aa00-116">Şablon kavramları</span><span class="sxs-lookup"><span data-stu-id="9aa00-116">Template concepts</span></span>
<span data-ttu-id="9aa00-117">İçinde [son dakika haberleri Notification Hubs kullanma toosend] kullanılan bir uygulama yerleşik **etiketleri** toosubscribe toonotifications farklı haber kategorileri için.</span><span class="sxs-lookup"><span data-stu-id="9aa00-117">In [Use Notification Hubs toosend breaking news] you built an app that used **tags** toosubscribe toonotifications for different news categories.</span></span>
<span data-ttu-id="9aa00-118">Birçok uygulama, ancak, birden çok pazarda hedef ve yerelleştirme gerektirir.</span><span class="sxs-lookup"><span data-stu-id="9aa00-118">Many apps, however, target multiple markets and require localization.</span></span> <span data-ttu-id="9aa00-119">Bunun anlamı hello bildirimleri kendilerini Merhaba içeriğine sahip yerelleştirilmiş toobe ve teslim toohello cihaz kümesini düzeltin.</span><span class="sxs-lookup"><span data-stu-id="9aa00-119">This means that hello content of hello notifications themselves have toobe localized and delivered toohello correct set of devices.</span></span>
<span data-ttu-id="9aa00-120">Bu konudaki göstereceğiz nasıl toouse hello **şablonu** özellik bildirim hub'larını tooeasily teslim yerelleştirilmiş son dakika haberi bildirimleri.</span><span class="sxs-lookup"><span data-stu-id="9aa00-120">In this topic we will show how toouse hello **template** feature of Notification Hubs tooeasily deliver localized breaking news notifications.</span></span>

<span data-ttu-id="9aa00-121">Not: tek yönlü toosend yerelleştirilmiş bildirimleri toocreate her etiket birden çok sürümünün olduğu.</span><span class="sxs-lookup"><span data-stu-id="9aa00-121">Note: one way toosend localized notifications is toocreate multiple versions of each tag.</span></span> <span data-ttu-id="9aa00-122">Örneğin, toosupport İngilizce, Fransızca ve Mandarin, üç farklı etiketler world haberler için ihtiyacımız: "world_en", "world_fr" ve "world_ch".</span><span class="sxs-lookup"><span data-stu-id="9aa00-122">For instance, toosupport English, French, and Mandarin, we would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span></span> <span data-ttu-id="9aa00-123">Toosend sonra hello world haber tooeach bu etiketlerin yerelleştirilmiş bir sürümü gerekir.</span><span class="sxs-lookup"><span data-stu-id="9aa00-123">We would then have toosend a localized version of hello world news tooeach of these tags.</span></span> <span data-ttu-id="9aa00-124">Bu konudaki şablonları tooavoid hello artışı etiketleri ve birden fazla ileti gönderme hello gereksinimi kullanın.</span><span class="sxs-lookup"><span data-stu-id="9aa00-124">In this topic we use templates tooavoid hello proliferation of tags and hello requirement of sending multiple messages.</span></span>

<span data-ttu-id="9aa00-125">Yüksek bir düzeyde bir şekilde toospecify şablonlarıdır nasıl belirli bir aygıt bir bildirim almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9aa00-125">At a high level, templates are a way toospecify how a specific device should receive a notification.</span></span> <span data-ttu-id="9aa00-126">Merhaba şablon, uygulama arka ucu tarafından gönderilen Merhaba ileti parçası olan tooproperties bakarak hello tam yük biçimi belirtir.</span><span class="sxs-lookup"><span data-stu-id="9aa00-126">hello template specifies hello exact payload format by referring tooproperties that are part of hello message sent by your app back-end.</span></span> <span data-ttu-id="9aa00-127">Örneğimizde, biz tüm desteklenen diller içeren bir yerel ayar belirsiz ileti gönderir:</span><span class="sxs-lookup"><span data-stu-id="9aa00-127">In our case, we will send a locale-agnostic message containing all supported languages:</span></span>

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

<span data-ttu-id="9aa00-128">Ardından cihazlarını toohello doğru özellik başvuran bir şablonla kaydetmek sağlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="9aa00-128">Then we will ensure that devices register with a template that refers toohello correct property.</span></span> <span data-ttu-id="9aa00-129">Örneği için tooreceive isteyen bir Windows mağazası uygulaması şablonu ile ilgili tüm etiketleri aşağıdaki hello için basit bir bildirim iletisi kaydeder:</span><span class="sxs-lookup"><span data-stu-id="9aa00-129">For instance, a Windows Store app that wants tooreceive a simple toast message will register for hello following template with any corresponding tags:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">$(News_English)</text>
        </binding>
      </visual>
    </toast>



<span data-ttu-id="9aa00-130">Şablonlar, daha fazla bilgi bulabilir hakkında içinde çok güçlü bir özellik olan bizim [şablonları](notification-hubs-templates-cross-platform-push-messages.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="9aa00-130">Templates are a very powerful feature you can learn more about in our [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span></span> 

## <a name="hello-app-user-interface"></a><span data-ttu-id="9aa00-131">Merhaba uygulama kullanıcı arabirimi</span><span class="sxs-lookup"><span data-stu-id="9aa00-131">hello app user interface</span></span>
<span data-ttu-id="9aa00-132">Biz şimdi hello konuda oluşturulan hello çiğnemekten haber uygulama değiştirecek [son dakika haberleri Notification Hubs kullanma toosend] toosend yerelleştirilmiş şablonları kullanarak son dakika haberleri.</span><span class="sxs-lookup"><span data-stu-id="9aa00-132">We will now modify hello Breaking News app that you created in hello topic [Use Notification Hubs toosend breaking news] toosend localized breaking news using templates.</span></span>

<span data-ttu-id="9aa00-133">Windows mağazası uygulamanızı:</span><span class="sxs-lookup"><span data-stu-id="9aa00-133">In your Windows Store app:</span></span>

<span data-ttu-id="9aa00-134">MainPage.xaml tooinclude yerel ayar combobox değiştirin:</span><span class="sxs-lookup"><span data-stu-id="9aa00-134">Change your MainPage.xaml tooinclude a locale combobox:</span></span>

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

## <a name="building-hello-windows-store-client-app"></a><span data-ttu-id="9aa00-135">Merhaba Windows mağazası istemci uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="9aa00-135">Building hello Windows Store client app</span></span>
1. <span data-ttu-id="9aa00-136">Yerel ayar parametresi tooyour bildirimleri sınıfınıza ekleyin *StoreCategoriesAndSubscribe* ve *SubscribeToCateories* yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="9aa00-136">In your Notifications class, add a locale parameter tooyour  *StoreCategoriesAndSubscribe* and *SubscribeToCateories* methods.</span></span>
   
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
   
    <span data-ttu-id="9aa00-137">Arama hello yerine unutmayın *RegisterNativeAsync* diyoruz yöntemi *RegisterTemplateAsync*: biz hangi hello şablon hello bölgesel ayarına bağlıdır belirli bildirim biçimi kaydediliyor.</span><span class="sxs-lookup"><span data-stu-id="9aa00-137">Note that instead of calling hello *RegisterNativeAsync* method we call *RegisterTemplateAsync*: we are registering a specific notification format in which hello template depends on hello locale.</span></span> <span data-ttu-id="9aa00-138">Biz de hello şablonu ("localizedWNSTemplateExample") için bir ad sağlayın, çünkü tooregister (örneğin biri bildirimleri) ve biri kutucuklar için birden fazla şablon istiyoruz ve tooname ihtiyacımız bunları toobe mümkün tooupdate sipariş veya silin.</span><span class="sxs-lookup"><span data-stu-id="9aa00-138">We also provide a name for hello template ("localizedWNSTemplateExample"), because we might want tooregister more than one template (for instance one for toast notifications and one for tiles) and we need tooname them in order toobe able tooupdate or delete them.</span></span>
   
    <span data-ttu-id="9aa00-139">Bir aygıt hello aynı etiketi sonuçlanır hedefleme gelen ileti etiketi ile birden fazla şablon kaydederse birden fazla bildirim toohello aygıt (her şablon için bir tane) teslim unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9aa00-139">Note that if a device registers multiple templates with hello same tag, an incoming message targeting that tag will result in multiple notifications delivered toohello device (one for each template).</span></span> <span data-ttu-id="9aa00-140">Bu davranış, Hello aynı mantıksal ileti tooresult örneği için bir Windows mağazası uygulamasında bir gösterge ve bildirim gösteren birden çok görsel bildirimler sahip yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="9aa00-140">This behavior is useful when hello same logical message has tooresult in multiple visual notifications, for instance showing both a badge and a toast in a Windows Store application.</span></span>
2. <span data-ttu-id="9aa00-141">Yöntem tooretrieve hello depolanan yerel aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="9aa00-141">Add hello following method tooretrieve hello stored locale:</span></span>
   
        public string RetrieveLocale()
        {
            var locale = (string) ApplicationData.Current.LocalSettings.Values["locale"];
            return locale != null ? locale : "English";
        }
3. <span data-ttu-id="9aa00-142">MainPage.xaml.cs dosyasında, düğme güncelleştirme işleyicisi hello geçerli hello yerel açılan kutu değerini almak ve gösterildiği gibi toohello çağrısı toohello bildirimleri sınıfı, sağlayarak'ı tıklatın:</span><span class="sxs-lookup"><span data-stu-id="9aa00-142">In your MainPage.xaml.cs, update your button click handler by retrieving hello current value of hello Locale combo box and providing it toohello call toohello Notifications class, as shown:</span></span>
   
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
4. <span data-ttu-id="9aa00-143">Son olarak, App.xaml.cs dosyasında emin tooupdate olun, `InitNotificationsAsync` yöntemi tooretrieve hello yerel ayar ve abone olurken kullanın:</span><span class="sxs-lookup"><span data-stu-id="9aa00-143">Finally, in your App.xaml.cs file, make sure tooupdate your `InitNotificationsAsync` method tooretrieve hello locale and use it when subscribing:</span></span>
   
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

## <a name="send-localized-notifications-from-your-back-end"></a><span data-ttu-id="9aa00-144">Arka ucunuz yerelleştirilmiş bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="9aa00-144">Send localized notifications from your back-end</span></span>
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
