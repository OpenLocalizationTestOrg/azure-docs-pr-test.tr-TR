---
title: "Notification Hubs son dakika haberleri öğretici yerelleştirilmiş"
description: "Yerelleştirilmiş son dakika haberi bildirimleri göndermek için Azure Notification Hubs kullanmayı öğrenin."
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
ms.openlocfilehash: e864e832b4c50644bf4062dee29d34ff9fe2774e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-localized-breaking-news"></a><span data-ttu-id="74fd7-103">Yerelleştirilmiş son dakika haberleri göndermek için Notification Hubs kullanma</span><span class="sxs-lookup"><span data-stu-id="74fd7-103">Use Notification Hubs to send localized breaking news</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="74fd7-104">Windows mağazası C#</span><span class="sxs-lookup"><span data-stu-id="74fd7-104">Windows Store C#</span></span>](notification-hubs-windows-store-dotnet-xplat-localized-wns-push-notification.md)
> * [<span data-ttu-id="74fd7-105">iOS</span><span class="sxs-lookup"><span data-stu-id="74fd7-105">iOS</span></span>](notification-hubs-ios-xplat-localized-apns-push-notification.md)
> 
> 

## <a name="overview"></a><span data-ttu-id="74fd7-106">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="74fd7-106">Overview</span></span>
<span data-ttu-id="74fd7-107">Bu konuda nasıl kullanılacağını gösterir **şablonu** dil ve cihaz tarafından yerelleştirilmiş son dakika haberi bildirimleri yayınlamak için Azure Notification Hubs özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="74fd7-107">This topic shows you how to use the **template** feature of Azure Notification Hubs to broadcast breaking news notifications that have been localized by language and device.</span></span> <span data-ttu-id="74fd7-108">Bu öğreticide oluşturduğunuz Windows mağazası uygulaması ile başlayın [son dakika haberleri göndermek için Notification Hubs kullanma].</span><span class="sxs-lookup"><span data-stu-id="74fd7-108">In this tutorial you start with the Windows Store app created in [Use Notification Hubs to send breaking news].</span></span> <span data-ttu-id="74fd7-109">Tamamlandığında, ilgilendiğiniz kategorileri için kaydetme, hangi bildirimleri almak ve o dilde yalnızca seçili kategorileri için anında iletme bildirimleri almak bir dil belirtin mümkün olacaktır.</span><span class="sxs-lookup"><span data-stu-id="74fd7-109">When complete, you will be able to register for categories you are interested in, specify a language in which to receive the notifications, and receive only push notifications for the selected categories in that language.</span></span>

<span data-ttu-id="74fd7-110">Bu senaryo iki bölümü vardır:</span><span class="sxs-lookup"><span data-stu-id="74fd7-110">There are two parts to this scenario:</span></span>

* <span data-ttu-id="74fd7-111">Windows mağazası uygulaması istemci aygıtlar bir dil belirtin ve farklı son dakika haberleri kategorilere abone olmak için sağlar;</span><span class="sxs-lookup"><span data-stu-id="74fd7-111">the Windows Store app allows client devices to specify a language, and to subscribe to different breaking news categories;</span></span>
* <span data-ttu-id="74fd7-112">arka uç kullanarak bildirimleri yayınlar **etiketi** ve **şablonu** Azure bildirim hub'larını feautres.</span><span class="sxs-lookup"><span data-stu-id="74fd7-112">the back-end broadcasts the notifications, using the **tag** and **template** feautres of Azure Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="74fd7-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="74fd7-113">Prerequisites</span></span>
<span data-ttu-id="74fd7-114">Önceden tamamlamış olmalıdır [son dakika haberleri göndermek için Notification Hubs kullanma] öğretici ve bu öğreticinin bu kodu doğrudan derlemeler için kullanılabilir, koda sahip.</span><span class="sxs-lookup"><span data-stu-id="74fd7-114">You must have already completed the [Use Notification Hubs to send breaking news] tutorial and have the code available, because this tutorial builds directly upon that code.</span></span>

<span data-ttu-id="74fd7-115">Ayrıca Visual Studio 2012 veya üzeri gerekir.</span><span class="sxs-lookup"><span data-stu-id="74fd7-115">You also need Visual Studio 2012 or later.</span></span>

## <a name="template-concepts"></a><span data-ttu-id="74fd7-116">Şablon kavramları</span><span class="sxs-lookup"><span data-stu-id="74fd7-116">Template concepts</span></span>
<span data-ttu-id="74fd7-117">İçinde [son dakika haberleri göndermek için Notification Hubs kullanma] kullanılan bir uygulama yerleşik **etiketleri** farklı haber kategorileri için Bildirimlere abone olma.</span><span class="sxs-lookup"><span data-stu-id="74fd7-117">In [Use Notification Hubs to send breaking news] you built an app that used **tags** to subscribe to notifications for different news categories.</span></span>
<span data-ttu-id="74fd7-118">Birçok uygulama, ancak, birden çok pazarda hedef ve yerelleştirme gerektirir.</span><span class="sxs-lookup"><span data-stu-id="74fd7-118">Many apps, however, target multiple markets and require localization.</span></span> <span data-ttu-id="74fd7-119">Bildirimler içeriğe sahip yerelleştirilmiş ve aygıtların doğru kümesine teslim anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="74fd7-119">This means that the content of the notifications themselves have to be localized and delivered to the correct set of devices.</span></span>
<span data-ttu-id="74fd7-120">Bu konudaki nasıl kullanılacağını göstereceğiz **şablonu** kolayca yerelleştirilmiş son dakika haberi bildirimleri göndermek için Notification Hubs özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="74fd7-120">In this topic we will show how to use the **template** feature of Notification Hubs to easily deliver localized breaking news notifications.</span></span>

<span data-ttu-id="74fd7-121">Not: yerelleştirilmiş bildirimleri göndermek için bir yol her etiket birden fazla sürümünü oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="74fd7-121">Note: one way to send localized notifications is to create multiple versions of each tag.</span></span> <span data-ttu-id="74fd7-122">Örneğin, İngilizce, Fransızca ve Mandarin desteklemek için üç farklı etiketler world haberler için ihtiyacımız: "world_en", "world_fr" ve "world_ch".</span><span class="sxs-lookup"><span data-stu-id="74fd7-122">For instance, to support English, French, and Mandarin, we would need three different tags for world news: "world_en", "world_fr", and "world_ch".</span></span> <span data-ttu-id="74fd7-123">Biz sonra world haber yerelleştirilmiş bir sürümünde bu etiketlerin her biri için göndermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="74fd7-123">We would then have to send a localized version of the world news to each of these tags.</span></span> <span data-ttu-id="74fd7-124">Bu konudaki etiketleri artışı ve birden fazla ileti gönderme gereksinimi önlemek için şablonlar kullanın.</span><span class="sxs-lookup"><span data-stu-id="74fd7-124">In this topic we use templates to avoid the proliferation of tags and the requirement of sending multiple messages.</span></span>

<span data-ttu-id="74fd7-125">Yüksek bir düzeyde şablonları belirli bir aygıt bir bildirim nasıl alacağını belirtmek için bir yoldur.</span><span class="sxs-lookup"><span data-stu-id="74fd7-125">At a high level, templates are a way to specify how a specific device should receive a notification.</span></span> <span data-ttu-id="74fd7-126">Şablon, uygulama arka ucu tarafından gönderilen ileti parçası olan özellikler için bakarak tam yük biçimi belirtir.</span><span class="sxs-lookup"><span data-stu-id="74fd7-126">The template specifies the exact payload format by referring to properties that are part of the message sent by your app back-end.</span></span> <span data-ttu-id="74fd7-127">Örneğimizde, biz tüm desteklenen diller içeren bir yerel ayar belirsiz ileti gönderir:</span><span class="sxs-lookup"><span data-stu-id="74fd7-127">In our case, we will send a locale-agnostic message containing all supported languages:</span></span>

    {
        "News_English": "...",
        "News_French": "...",
        "News_Mandarin": "..."
    }

<span data-ttu-id="74fd7-128">Ardından aygıtları doğru özelliğine başvuran bir şablon ile kaydetmeye sağlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="74fd7-128">Then we will ensure that devices register with a template that refers to the correct property.</span></span> <span data-ttu-id="74fd7-129">Örneği için bir basit bildirim iletisi almak istediği bir Windows mağazası uygulaması, aşağıdaki şablonu ile ilgili herhangi bir etiket için kaydeder:</span><span class="sxs-lookup"><span data-stu-id="74fd7-129">For instance, a Windows Store app that wants to receive a simple toast message will register for the following template with any corresponding tags:</span></span>

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">$(News_English)</text>
        </binding>
      </visual>
    </toast>



<span data-ttu-id="74fd7-130">Şablonlar, daha fazla bilgi bulabilir hakkında içinde çok güçlü bir özellik olan bizim [şablonları](notification-hubs-templates-cross-platform-push-messages.md) makalesi.</span><span class="sxs-lookup"><span data-stu-id="74fd7-130">Templates are a very powerful feature you can learn more about in our [Templates](notification-hubs-templates-cross-platform-push-messages.md) article.</span></span> 

## <a name="the-app-user-interface"></a><span data-ttu-id="74fd7-131">Uygulama kullanıcı arabirimi</span><span class="sxs-lookup"><span data-stu-id="74fd7-131">The app user interface</span></span>
<span data-ttu-id="74fd7-132">Biz şimdi konu başlığı altında oluşturulan yeni haber uygulama değiştirecek [son dakika haberleri göndermek için Notification Hubs kullanma] son dakika haberleri şablonları kullanarak göndermek için yerelleştirilmiş.</span><span class="sxs-lookup"><span data-stu-id="74fd7-132">We will now modify the Breaking News app that you created in the topic [Use Notification Hubs to send breaking news] to send localized breaking news using templates.</span></span>

<span data-ttu-id="74fd7-133">Windows mağazası uygulamanızı:</span><span class="sxs-lookup"><span data-stu-id="74fd7-133">In your Windows Store app:</span></span>

<span data-ttu-id="74fd7-134">Yerel ayar combobox dahil etmek için MainPage.xaml değiştirin:</span><span class="sxs-lookup"><span data-stu-id="74fd7-134">Change your MainPage.xaml to include a locale combobox:</span></span>

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

## <a name="building-the-windows-store-client-app"></a><span data-ttu-id="74fd7-135">Windows mağazası istemci uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="74fd7-135">Building the Windows Store client app</span></span>
1. <span data-ttu-id="74fd7-136">Yerel ayar parametresi bildirimleri sınıfınıza ekleyin, *StoreCategoriesAndSubscribe* ve *SubscribeToCateories* yöntemleri.</span><span class="sxs-lookup"><span data-stu-id="74fd7-136">In your Notifications class, add a locale parameter to your  *StoreCategoriesAndSubscribe* and *SubscribeToCateories* methods.</span></span>
   
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
            // Using the localized tags based on locale selected.
            string templateBodyWNS = String.Format("<toast><visual><binding template=\"ToastText01\"><text id=\"1\">$(News_{0})</text></binding></visual></toast>", locale);
   
            return await hub.RegisterTemplateAsync(channel.Uri, templateBodyWNS, "localizedWNSTemplateExample", categories);
        }
   
    <span data-ttu-id="74fd7-137">Arama yerine unutmayın *RegisterNativeAsync* diyoruz yöntemi *RegisterTemplateAsync*: biz şablon bölgesel ayarına bağlıdır belirli bildirim biçimi kaydediliyor.</span><span class="sxs-lookup"><span data-stu-id="74fd7-137">Note that instead of calling the *RegisterNativeAsync* method we call *RegisterTemplateAsync*: we are registering a specific notification format in which the template depends on the locale.</span></span> <span data-ttu-id="74fd7-138">Ayrıca ("localizedWNSTemplateExample"), şablon için bir ad (örneğin bir bildirimleri için) ve biri döşeme için birden fazla şablon kaydetmek istiyoruz ve bunları güncelleştirmek veya bunları silmek için ad ihtiyacımız çünkü sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="74fd7-138">We also provide a name for the template ("localizedWNSTemplateExample"), because we might want to register more than one template (for instance one for toast notifications and one for tiles) and we need to name them in order to be able to update or delete them.</span></span>
   
    <span data-ttu-id="74fd7-139">Bir aygıt ile aynı etiketi birden fazla şablon kaydederse, bir gelen ileti etiketi içinde birden fazla bildirim sonuçlanacak hedefleme aygıt (her şablon için bir tane) teslim olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="74fd7-139">Note that if a device registers multiple templates with the same tag, an incoming message targeting that tag will result in multiple notifications delivered to the device (one for each template).</span></span> <span data-ttu-id="74fd7-140">Bu davranış, aynı mantıksal ileti örneği için bir Windows mağazası uygulamasında bir gösterge ve bildirim gösteren birden çok görsel bildirimler neden olduğunda yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="74fd7-140">This behavior is useful when the same logical message has to result in multiple visual notifications, for instance showing both a badge and a toast in a Windows Store application.</span></span>
2. <span data-ttu-id="74fd7-141">Depolanan yerel almak için aşağıdaki yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="74fd7-141">Add the following method to retrieve the stored locale:</span></span>
   
        public string RetrieveLocale()
        {
            var locale = (string) ApplicationData.Current.LocalSettings.Values["locale"];
            return locale != null ? locale : "English";
        }
3. <span data-ttu-id="74fd7-142">MainPage.xaml.cs dosyasında Güncelleştir, düğmesi gösterildiği gibi yerel açılan kutu geçerli değerini almak ve bildirimleri sınıfı çağrısına sağlayarak işleyici tıklayın:</span><span class="sxs-lookup"><span data-stu-id="74fd7-142">In your MainPage.xaml.cs, update your button click handler by retrieving the current value of the Locale combo box and providing it to the call to the Notifications class, as shown:</span></span>
   
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
4. <span data-ttu-id="74fd7-143">Son olarak, App.xaml.cs dosyasında güncelleştirdiğinizden emin olun, `InitNotificationsAsync` yöntemi yerel almak ve abone olurken kullanın:</span><span class="sxs-lookup"><span data-stu-id="74fd7-143">Finally, in your App.xaml.cs file, make sure to update your `InitNotificationsAsync` method to retrieve the locale and use it when subscribing:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var result = await notifications.SubscribeToCategories(notifications.RetrieveLocale());
   
            // Displays the registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
        }

## <a name="send-localized-notifications-from-your-back-end"></a><span data-ttu-id="74fd7-144">Arka ucunuz yerelleştirilmiş bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="74fd7-144">Send localized notifications from your back-end</span></span>
[!INCLUDE [notification-hubs-localized-back-end](../../includes/notification-hubs-localized-back-end.md)]

<!-- Anchors. -->
[Template concepts]: #concepts
[The app user interface]: #ui
[Building the Windows Store client app]: #building-client
[Send notifications from your back-end]: #send
[Next Steps]:#next-steps

<!-- Images. -->

<!-- URLs. -->
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notify users with Notification Hubs: ASP.NET]: /manage/services/notification-hubs/notify-users-aspnet
[Notify users with Notification Hubs: Mobile Services]: /manage/services/notification-hubs/notify-users
<span data-ttu-id="74fd7-145">[son dakika haberleri göndermek için Notification Hubs kullanma]: /manage/services/notification-hubs/breaking-news-dotnet</span><span class="sxs-lookup"><span data-stu-id="74fd7-145">[Use Notification Hubs to send breaking news]: /manage/services/notification-hubs/breaking-news-dotnet</span></span>

[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253
[Get started with Mobile Services]: /develop/mobile/tutorials/get-started/#create-new-service
[Get started with data]: /develop/mobile/tutorials/get-started-with-data-dotnet
[Get started with authentication]: /develop/mobile/tutorials/get-started-with-users-dotnet
[Get started with push notifications]: /develop/mobile/tutorials/get-started-with-push-dotnet
[Push notifications to app users]: /develop/mobile/tutorials/push-notifications-to-app-users-dotnet
[Authorize users with scripts]: /develop/mobile/tutorials/authorize-users-in-scripts-dotnet
[JavaScript and HTML]: /develop/mobile/tutorials/get-started-with-push-js

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for iOS]: http://msdn.microsoft.com/library/jj927168.aspx
[Notification Hubs How-To for Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
