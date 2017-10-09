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
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="58a46-103">Bildirim hub'ları toosend son dakika haberleri kullanın</span><span class="sxs-lookup"><span data-stu-id="58a46-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="58a46-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="58a46-104">Overview</span></span>
<span data-ttu-id="58a46-105">Bu konu, nasıl gösterir toouse Azure Notification Hubs toobroadcast en son haberleri bildirimleri tooa Windows Phone 8.0/8.1 Silverlight uygulaması.</span><span class="sxs-lookup"><span data-stu-id="58a46-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooa Windows Phone 8.0/8.1 Silverlight app.</span></span> <span data-ttu-id="58a46-106">Windows mağazası veya Windows Phone 8.1 uygulama hedefliyorsanız Lütfen tootoohello bakın [Windows Evrensel](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) sürümü.</span><span class="sxs-lookup"><span data-stu-id="58a46-106">If you are targeting Windows Store or Windows Phone 8.1 app, please refer tootoohello [Windows Universal](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) version.</span></span> <span data-ttu-id="58a46-107">Tamamlandığında, ilgilendiğiniz haber kategorileri sonu için mümkün tooregister olmalı ve yalnızca bu kategorilerin anında iletme bildirimlerini almak.</span><span class="sxs-lookup"><span data-stu-id="58a46-107">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="58a46-108">Bu sayıda uygulama için genel bir desen bildirimleri gönderilen toobe toogroups daha önce bunları, örneğin, RSS Okuyucu, müzik fanlar, vb. için uygulamaları ilgi bildirilen kullanıcıların sahip olduğu bir senaryodur.</span><span class="sxs-lookup"><span data-stu-id="58a46-108">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="58a46-109">Yayın senaryoları etkin bir veya daha fazla dahil ederek *etiketleri* bir kayıt hello bildirim hub'oluştururken.</span><span class="sxs-lookup"><span data-stu-id="58a46-109">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="58a46-110">Bildirimleri tooa etiketi gönderildiğinde kayıtlı tüm aygıtları hello etiketi hello bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="58a46-110">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="58a46-111">Etiketleri yalnızca dizeleri olduğundan, önceden sağlanmış toobe gerekmez.</span><span class="sxs-lookup"><span data-stu-id="58a46-111">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="58a46-112">Etiketler hakkında daha fazla bilgi için çok başvuran[bildirim hub'ları Yönlendirme ve etiket ifadeleri](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="58a46-112">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58a46-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="58a46-113">Prerequisites</span></span>
<span data-ttu-id="58a46-114">Bu konu içinde oluşturduğunuz hello uygulama inşa edilmiştir [Notification Hubs ile çalışmaya başlama].</span><span class="sxs-lookup"><span data-stu-id="58a46-114">This topic builds on hello app you created in [Get started with Notification Hubs].</span></span> <span data-ttu-id="58a46-115">Bu öğreticiye başlamadan önce önce tamamlamış olmalıdır [Notification Hubs ile çalışmaya başlama].</span><span class="sxs-lookup"><span data-stu-id="58a46-115">Before starting this tutorial, you must have already completed [Get started with Notification Hubs].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="58a46-116">Kategori seçimi toohello uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="58a46-116">Add category selection toohello app</span></span>
<span data-ttu-id="58a46-117">Merhaba ilk adım, hello kullanıcı tooselect kategorileri tooregister etkinleştirmek tooadd hello kullanıcı Arabirimi öğeleri tooyour varolan ana sayfasıdır.</span><span class="sxs-lookup"><span data-stu-id="58a46-117">hello first step is tooadd hello UI elements tooyour existing main page that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="58a46-118">bir kullanıcı tarafından seçilen hello kategoriler hello aygıtta depolanır.</span><span class="sxs-lookup"><span data-stu-id="58a46-118">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="58a46-119">Merhaba uygulama başlatıldığında bir aygıt kaydı bildirim hub'ınıza seçili hello kategorileri etiketler oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="58a46-119">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="58a46-120">Merhaba MainPage.xaml proje dosyasını açın ve ardından hello yerine **kılavuz** adlı öğe `TitlePanel` ve `ContentPanel` koddan hello ile:</span><span class="sxs-lookup"><span data-stu-id="58a46-120">Open hello MainPage.xaml project file, then replace hello **Grid** elements named `TitlePanel` and `ContentPanel` with hello following code:</span></span>
   
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
2. <span data-ttu-id="58a46-121">Merhaba projesinde adlı yeni bir sınıf oluşturun **bildirimleri**, hello eklemek **ortak** değiştiricisi toohello sınıf tanımının sonra hello aşağıdakileri ekleyin **kullanarak** deyimleri toohello yeni kod dosyası:</span><span class="sxs-lookup"><span data-stu-id="58a46-121">In hello project, create a new class named **Notifications**, add hello **public** modifier toohello class definition, then add hello following **using** statements toohello new code file:</span></span>
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
        using System.IO.IsolatedStorage;
        using System.Windows;
3. <span data-ttu-id="58a46-122">Kopya hello aşağıdaki kod hello yeni **bildirimleri** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="58a46-122">Copy hello following code into hello new **Notifications** class:</span></span>
   
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

    <span data-ttu-id="58a46-123">Bu sınıf hello yalıtılmış depolama toostore hello kategorilerini bu aygıtın tooreceive olduğunu haber kullanır.</span><span class="sxs-lookup"><span data-stu-id="58a46-123">This class uses hello isolated storage toostore hello categories of news that this device is tooreceive.</span></span> <span data-ttu-id="58a46-124">Yöntemleri tooregister kullanarak bu kategorilerin de içeren bir [şablonu](notification-hubs-templates-cross-platform-push-messages.md) bildirimi kaydı.</span><span class="sxs-lookup"><span data-stu-id="58a46-124">It also contains methods tooregister for these categories using a [template](notification-hubs-templates-cross-platform-push-messages.md) notification registration.</span></span>


1. <span data-ttu-id="58a46-125">Özellik toohello aşağıdaki hello Hello App.xaml.cs proje dosyasında eklemek **uygulama** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="58a46-125">In hello App.xaml.cs project file, add hello following property toohello **App** class.</span></span> <span data-ttu-id="58a46-126">Hello yerine `<hub name>` ve `<connection string with listen access>` bildirim hub'ı adı ve hello için bağlantı dizenizi yer tutucularını *DefaultListenSharedAccessSignature* daha önce edindiğiniz.</span><span class="sxs-lookup"><span data-stu-id="58a46-126">Replace hello `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
   > [!NOTE]
   > <span data-ttu-id="58a46-127">Bir istemci uygulaması ile dağıtılmış kimlik bilgileri genellikle güvenli olmadığından, yalnızca hello anahtarını dinleme erişim için istemci uygulamanızı dağıtmak.</span><span class="sxs-lookup"><span data-stu-id="58a46-127">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="58a46-128">Bildirimler, ancak var olan kayıtlar için uygulama tooregister değiştirilemez erişimi etkinleştirir dinleyin ve bildirim gönderilemiyor.</span><span class="sxs-lookup"><span data-stu-id="58a46-128">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="58a46-129">Merhaba tam erişim tuşu bir güvenli arka uç hizmetinde bildirimleri gönderme ve var olan kayıtlar değiştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="58a46-129">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
2. <span data-ttu-id="58a46-130">MainPage.xaml.cs dosyasında hello aşağıdaki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="58a46-130">In your MainPage.xaml.cs, add hello following line:</span></span>
   
        using Windows.UI.Popups;
3. <span data-ttu-id="58a46-131">Merhaba MainPage.xaml.cs proje dosyasında yöntemi aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="58a46-131">In hello MainPage.xaml.cs project file, add hello following method:</span></span>
   
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
   
    <span data-ttu-id="58a46-132">Bu yöntem kategorileri ve kullandığı hello listesini oluşturur **bildirimleri** sınıf toostore hello hello yerel depolama listesinde ve bildirim hub'ınıza hello karşılık gelen etiketleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="58a46-132">This method creates a list of categories and uses hello **Notifications** class toostore hello list in hello local storage and register hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="58a46-133">Kategoriler değiştirildiğinde hello kayıt hello yeni kategorileri ile yeniden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="58a46-133">When categories are changed, hello registration is recreated with hello new categories.</span></span>

<span data-ttu-id="58a46-134">Uygulamanızı mümkün toostore kategorileri kümesi hello cihazda yerel depolama sunulmuştur ve kategorisi seçimine hello kullanıcı değişiklikleri hello her hello bildirim hub'ı ile kaydedin.</span><span class="sxs-lookup"><span data-stu-id="58a46-134">Your app is now able toostore a set of categories in local storage on hello device and register with hello notification hub whenever hello user changes hello selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="58a46-135">Bildirimler için kaydolun</span><span class="sxs-lookup"><span data-stu-id="58a46-135">Register for notifications</span></span>
<span data-ttu-id="58a46-136">Yerel depolamada depolanan hello kategorileri kullanarak başlangıçta hello bildirim hub'ı ile adımları kaydedin.</span><span class="sxs-lookup"><span data-stu-id="58a46-136">These steps register with hello notification hub on startup using hello categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="58a46-137">Merhaba kanal URI'sini hello Microsoft anında iletme bildirimi Hizmeti'ni (MPNS) tarafından atanan herhangi bir zamanda değiştiğinden bildirimleri için tooavoid bildirim hataları sık kaydetmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="58a46-137">Because hello channel URI assigned by hello Microsoft Push Notification Service (MPNS) can change at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="58a46-138">Bu hello uygulama her başlatıldığında bu örnek için bildirimleri kaydeder.</span><span class="sxs-lookup"><span data-stu-id="58a46-138">This example registers for notifications every time that hello app starts.</span></span> <span data-ttu-id="58a46-139">Bir günden az hello önceki kayıt itibaren aktarılırsa, sık çalıştırılan uygulamalar için günde bir kereden fazla, büyük olasılıkla kayıt toopreserve bant genişliği atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58a46-139">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
> 
> 

1. <span data-ttu-id="58a46-140">Merhaba App.xaml.cs dosyasını açın ve hello ekleyin **zaman uyumsuz** değiştiricisi çok**Application_Launching** eklediğiniz yöntemi ve Değiştir hello Notification Hubs kayıt kodu [Notification Hubs ile çalışmaya başlama] koddan hello ile:</span><span class="sxs-lookup"><span data-stu-id="58a46-140">Open hello App.xaml.cs file and add hello **async** modifier too**Application_Launching** method and replace hello Notification Hubs registration code that you added in [Get started with Notification Hubs] with hello following code:</span></span>
   
        private async void Application_Launching(object sender, LaunchingEventArgs e)
        {
            var result = await notifications.SubscribeToCategories();
   
            if (result != null)
                System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
                {
                    MessageBox.Show("Registration Id :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
                });
        }
   
    <span data-ttu-id="58a46-141">Bu hello uygulama her başlatıldığında hello kategorileri yerel depodan alır ve bu kategorileri için bir kayıt isteklerini emin olur.</span><span class="sxs-lookup"><span data-stu-id="58a46-141">This makes sure that every time hello app starts it retrieves hello categories from local storage and requests a registration for these categories.</span></span>
2. <span data-ttu-id="58a46-142">Merhaba MainPage.xaml.cs proje dosyasında hello uygulayan kod aşağıdaki hello eklemek **OnNavigatedTo** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="58a46-142">In hello MainPage.xaml.cs project file, add hello following code that implements hello **OnNavigatedTo** method:</span></span>
   
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
   
    <span data-ttu-id="58a46-143">Merhaba durumlarına önceden dayalı bu güncelleştirmeleri hello ana bir sayfayı kategorileri kaydedildi.</span><span class="sxs-lookup"><span data-stu-id="58a46-143">This updates hello main page based on hello status of previously saved categories.</span></span>

<span data-ttu-id="58a46-144">Merhaba uygulama tamamlanmıştır ve kategorisi seçimine hello kullanıcı değişiklikleri hello her kategori kümesini hello aygıt kullanılan yerel depolama tooregister hello bildirim hub'ı ile depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="58a46-144">hello app is now complete and can store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello user changes hello selection of categories.</span></span> <span data-ttu-id="58a46-145">Ardından, biz kategori bildirimleri toothis uygulamanın gönderebileceği bir arka uç tanımlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="58a46-145">Next, we will define a backend that can send category notifications toothis app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="58a46-146">Etiketli bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="58a46-146">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="58a46-147">Merhaba uygulamayı çalıştırın ve bildirimler oluşturma</span><span class="sxs-lookup"><span data-stu-id="58a46-147">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="58a46-148">Visual Studio'da F5 toocompile tuşuna basın ve hello uygulamayı başlatın.</span><span class="sxs-lookup"><span data-stu-id="58a46-148">In Visual Studio, press F5 toocompile and start hello app.</span></span>
   
    ![][1]
   
    <span data-ttu-id="58a46-149">Bir dizi kullanıcı Arabirimi sağlar bu hello uygulama değiştirir Not hello kategorileri toosubscribe seçmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="58a46-149">Note that hello app UI provides a set of toggles that lets you choose hello categories toosubscribe to.</span></span>
2. <span data-ttu-id="58a46-150">Bir veya daha fazla kategorileri değiştirir etkinleştirin ve ardından **abone ol**.</span><span class="sxs-lookup"><span data-stu-id="58a46-150">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="58a46-151">Merhaba uygulama seçili hello kategoriler etiketleri dönüştürür ve seçili hello etiketleri için yeni bir cihaz kaydı hello bildirim hub'ından ister.</span><span class="sxs-lookup"><span data-stu-id="58a46-151">hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span> <span data-ttu-id="58a46-152">Merhaba kayıtlı kategorileri döndürülen ve iletişim kutusunda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="58a46-152">hello registered categories are returned and displayed in a dialog.</span></span>
   
    ![][2]
3. <span data-ttu-id="58a46-153">Kategoriler tamamlandı aboneliği olan bir onay aldıktan sonra her kategori için hello konsol uygulama toosend bildirimleri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="58a46-153">After receiving a confirmation that your categories were subscription completed, run hello console app toosend notifications for each categories.</span></span> <span data-ttu-id="58a46-154">Yalnızca abone olduğunuz hello kategorileri için bir bildirim alırsınız emin olun.</span><span class="sxs-lookup"><span data-stu-id="58a46-154">Verify you only receive a notification for hello categories you have subscribed to.</span></span>
   
    ![][3]

<span data-ttu-id="58a46-155">Bu konuda tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="58a46-155">You have completed this topic.</span></span>

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

