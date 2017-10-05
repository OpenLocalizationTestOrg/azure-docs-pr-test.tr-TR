---
title: "(Windows Phone) son dakika haberleri göndermek için Notification Hubs'ı kullanma"
description: "Azure Notification Hubs etiketi kayıtları bir Windows Phone uygulamasına son dakika haberleri göndermek için kullanın."
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
ms.openlocfilehash: 3a6a69bf555c7267d3fbeb03ff6c03054991960f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-notification-hubs-to-send-breaking-news"></a><span data-ttu-id="b9357-103">Son dakika haberleri göndermek için Notification Hubs kullanma</span><span class="sxs-lookup"><span data-stu-id="b9357-103">Use Notification Hubs to send breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="b9357-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="b9357-104">Overview</span></span>
<span data-ttu-id="b9357-105">Bu konu Azure Notification Hubs son dakika haberi bildirimleri bir Windows Phone 8.0/8.1 Silverlight uygulamasına yayını için nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="b9357-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to a Windows Phone 8.0/8.1 Silverlight app.</span></span> <span data-ttu-id="b9357-106">Windows mağazası veya Windows Phone 8.1 uygulama hedefliyorsanız, için lütfen [Windows Evrensel](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) sürümü.</span><span class="sxs-lookup"><span data-stu-id="b9357-106">If you are targeting Windows Store or Windows Phone 8.1 app, please refer to to the [Windows Universal](notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md) version.</span></span> <span data-ttu-id="b9357-107">Tamamlandığında, ilgilendiğiniz haber kategorileri dökümü için kaydedilecek olması ve yalnızca bu kategorilerin anında iletme bildirimlerini almak.</span><span class="sxs-lookup"><span data-stu-id="b9357-107">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="b9357-108">Bu sayıda uygulama için genel bir desen bildirimleri daha önce bunları, örneğin, RSS Okuyucu, müzik fanlar, vb. için uygulamaları ilgi derlendiğinden kullanıcı gruplarını gönderilmesini sahip olduğu bir senaryodur.</span><span class="sxs-lookup"><span data-stu-id="b9357-108">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, etc.</span></span>

<span data-ttu-id="b9357-109">Yayın senaryoları etkin bir veya daha fazla dahil ederek *etiketleri* bir kayıt bildirim hub'ı oluştururken.</span><span class="sxs-lookup"><span data-stu-id="b9357-109">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="b9357-110">Bildirimler için bir etiket gönderildiğinde, kaydettiğiniz tüm etiket cihazlarda bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="b9357-110">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span></span> <span data-ttu-id="b9357-111">Etiketleri yalnızca dizeleri olduğundan, bunlar önceden hazırlanması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="b9357-111">Because tags are simply strings, they do not have to be provisioned in advance.</span></span> <span data-ttu-id="b9357-112">Etiketler hakkında daha fazla bilgi için başvurmak [bildirim hub'ları Yönlendirme ve etiket ifadeleri](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="b9357-112">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9357-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b9357-113">Prerequisites</span></span>
<span data-ttu-id="b9357-114">Bu konu, oluşturduğunuz uygulama inşa edilmiştir [Notification Hubs ile çalışmaya başlama].</span><span class="sxs-lookup"><span data-stu-id="b9357-114">This topic builds on the app you created in [Get started with Notification Hubs].</span></span> <span data-ttu-id="b9357-115">Bu öğreticiye başlamadan önce önce tamamlamış olmalıdır [Notification Hubs ile çalışmaya başlama].</span><span class="sxs-lookup"><span data-stu-id="b9357-115">Before starting this tutorial, you must have already completed [Get started with Notification Hubs].</span></span>

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="b9357-116">Kategori seçimi için uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="b9357-116">Add category selection to the app</span></span>
<span data-ttu-id="b9357-117">İlk adım, kullanıcı Arabirimi öğeleri kaydetmek için kategoriler seçmesini sağlayan varolan ana sayfanıza eklemektir.</span><span class="sxs-lookup"><span data-stu-id="b9357-117">The first step is to add the UI elements to your existing main page that enable the user to select categories to register.</span></span> <span data-ttu-id="b9357-118">Bir kullanıcı tarafından seçilen kategoriler cihazda depolanır.</span><span class="sxs-lookup"><span data-stu-id="b9357-118">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="b9357-119">Uygulama başlatıldığında bir aygıt kaydı bildirim hub'ınıza seçili kategorileri etiketler oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b9357-119">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="b9357-120">MainPage.xaml proje dosyasını açın ve sonra değiştirmek **kılavuz** adlı öğe `TitlePanel` ve `ContentPanel` aşağıdaki kod ile:</span><span class="sxs-lookup"><span data-stu-id="b9357-120">Open the MainPage.xaml project file, then replace the **Grid** elements named `TitlePanel` and `ContentPanel` with the following code:</span></span>
   
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
2. <span data-ttu-id="b9357-121">Projede adlı yeni bir sınıf oluşturun **bildirimleri**, ekleme **ortak** değiştiricisi sınıf tanımına sonra aşağıdakileri ekleyin **kullanarak** deyimleri için yeni kod dosyası:</span><span class="sxs-lookup"><span data-stu-id="b9357-121">In the project, create a new class named **Notifications**, add the **public** modifier to the class definition, then add the following **using** statements to the new code file:</span></span>
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
        using System.IO.IsolatedStorage;
        using System.Windows;
3. <span data-ttu-id="b9357-122">Aşağıdaki kodu yeni dosyaya kopyalayın **bildirimleri** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="b9357-122">Copy the following code into the new **Notifications** class:</span></span>
   
        private NotificationHub hub;
   
        // Registration task to complete registration in the ChannelUriUpdated event handler
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
   
                // This is optional, used to receive notifications while the app is running.
                channel.ShellToastNotificationReceived += channel_ShellToastNotificationReceived;
            }
   
            // If channel.ChannelUri is not null, we will complete the registrationTask here.  
            // If it is null, the registrationTask will be completed in the ChannelUriUpdated event handler.
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
            // Using a template registration to support notifications across platforms.
            // Any template notifications that contain messageParam and a corresponding tag expression
            // will be delivered for this registration.
   
            const string templateBodyMPNS = "<wp:Notification xmlns:wp=\"WPNotification\">" +
                                                "<wp:Toast>" +
                                                    "<wp:Text1>$(messageParam)</wp:Text1>" +
                                                "</wp:Toast>" +
                                            "</wp:Notification>";
   
            // The stored categories tags are passed with the template registration.
   
            registrationTask.SetResult(await hub.RegisterTemplateAsync(channelUri.ToString(), 
                templateBodyMPNS, "simpleMPNSTemplateExample", this.RetrieveCategories()));
   
            return await registrationTask.Task;
        }
   
        // This is optional. It is used to receive notifications while the app is running.
        void channel_ShellToastNotificationReceived(object sender, NotificationEventArgs e)
        {
            StringBuilder message = new StringBuilder();
            string relativeUri = string.Empty;
   
            message.AppendFormat("Received Toast {0}:\n", DateTime.Now.ToShortTimeString());
   
            // Parse out the information that was part of the message.
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
   
            // Display a dialog of all the fields in the toast.
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() => 
            { 
                MessageBox.Show(message.ToString()); 
            });
        }

    <span data-ttu-id="b9357-123">Bu sınıf yalıtılmış depolama almak için bu cihazı mı haber kategorilerini depolamak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="b9357-123">This class uses the isolated storage to store the categories of news that this device is to receive.</span></span> <span data-ttu-id="b9357-124">Kullanarak bu kategorileri için kaydetmeye yönelik yöntemler de içeren bir [şablonu](notification-hubs-templates-cross-platform-push-messages.md) bildirimi kaydı.</span><span class="sxs-lookup"><span data-stu-id="b9357-124">It also contains methods to register for these categories using a [template](notification-hubs-templates-cross-platform-push-messages.md) notification registration.</span></span>


1. <span data-ttu-id="b9357-125">App.xaml.cs proje dosyasında aşağıdaki özellik eklemek **uygulama** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="b9357-125">In the App.xaml.cs project file, add the following property to the **App** class.</span></span> <span data-ttu-id="b9357-126">Değiştir `<hub name>` ve `<connection string with listen access>` , bildirim hub'ı adı ve bağlantı dizesinde yer tutucularını *DefaultListenSharedAccessSignature* daha önce edindiğiniz.</span><span class="sxs-lookup"><span data-stu-id="b9357-126">Replace the `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
   > [!NOTE]
   > <span data-ttu-id="b9357-127">Bir istemci uygulaması ile dağıtılmış kimlik bilgileri genellikle güvenli olmadığı için istemci uygulamanızı dinleme erişim için anahtar yalnızca dağıtmanız.</span><span class="sxs-lookup"><span data-stu-id="b9357-127">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="b9357-128">Bildirimler, ancak var olan kayıtlar için kaydetmek için uygulamanızın değiştirilemez erişimi etkinleştirir dinleyin ve bildirim gönderilemiyor.</span><span class="sxs-lookup"><span data-stu-id="b9357-128">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="b9357-129">Tam erişim anahtarı, bir güvenli arka uç hizmetinde bildirimleri gönderme ve var olan kayıtlar değiştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b9357-129">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
2. <span data-ttu-id="b9357-130">MainPage.xaml.cs dosyasında aşağıdaki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b9357-130">In your MainPage.xaml.cs, add the following line:</span></span>
   
        using Windows.UI.Popups;
3. <span data-ttu-id="b9357-131">MainPage.xaml.cs proje dosyasında aşağıdaki yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="b9357-131">In the MainPage.xaml.cs project file, add the following method:</span></span>
   
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
   
    <span data-ttu-id="b9357-132">Bu yöntem kategorileri ve kullandığı bir liste oluşturur **bildirimleri** listesi yerel depolama alanına depolar ve karşılık gelen kaydetmek için sınıfı, bildirim hub'ınıza etiketler.</span><span class="sxs-lookup"><span data-stu-id="b9357-132">This method creates a list of categories and uses the **Notifications** class to store the list in the local storage and register the corresponding tags with your notification hub.</span></span> <span data-ttu-id="b9357-133">Kategoriler değiştirildiğinde kaydı yeni kategoriler yeniden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="b9357-133">When categories are changed, the registration is recreated with the new categories.</span></span>

<span data-ttu-id="b9357-134">Uygulamanızı kategorileri kümesi cihazın yerel depolama depolamak ve kullanıcı kategorisi seçimine değiştiğinde bildirim hub'ınızla kaydolmak için sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="b9357-134">Your app is now able to store a set of categories in local storage on the device and register with the notification hub whenever the user changes the selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="b9357-135">Bildirimler için kaydolun</span><span class="sxs-lookup"><span data-stu-id="b9357-135">Register for notifications</span></span>
<span data-ttu-id="b9357-136">Yerel depolamada depolanan kategorileri kullanarak başlangıçtaki bildirim hub'ı ile adımları kaydedin.</span><span class="sxs-lookup"><span data-stu-id="b9357-136">These steps register with the notification hub on startup using the categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="b9357-137">Microsoft anında iletme bildirimi Hizmeti'ni (MPNS) tarafından atanan URI kanal herhangi bir zamanda değiştiğinden bildirimlerinin sık bildirim hataları önlemek için kayıt olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b9357-137">Because the channel URI assigned by the Microsoft Push Notification Service (MPNS) can change at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="b9357-138">Bu örnek uygulama başladıktan her zaman için bildirimleri kaydeder.</span><span class="sxs-lookup"><span data-stu-id="b9357-138">This example registers for notifications every time that the app starts.</span></span> <span data-ttu-id="b9357-139">Sık çalıştırılan uygulamalar için günde bir kereden fazla, büyük olasılıkla bir günden az itibaren önceki kayıt aktarılırsa bant genişliğinden tasarruf etmek kayıt atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9357-139">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
> 
> 

1. <span data-ttu-id="b9357-140">App.xaml.cs dosyasını açın ve eklemek **zaman uyumsuz** değiştiriciyi **Application_Launching** yöntemi ve bildirim hub'ları kayıt, eklenen kod Değiştir [Notification Hubs ile çalışmaya başlama] aşağıdaki kod ile:</span><span class="sxs-lookup"><span data-stu-id="b9357-140">Open the App.xaml.cs file and add the **async** modifier to **Application_Launching** method and replace the Notification Hubs registration code that you added in [Get started with Notification Hubs] with the following code:</span></span>
   
        private async void Application_Launching(object sender, LaunchingEventArgs e)
        {
            var result = await notifications.SubscribeToCategories();
   
            if (result != null)
                System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
                {
                    MessageBox.Show("Registration Id :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
                });
        }
   
    <span data-ttu-id="b9357-141">Bu uygulama her başlatıldığında kategorileri yerel depodan alır ve bu kategorileri için bir kayıt isteklerini emin olur.</span><span class="sxs-lookup"><span data-stu-id="b9357-141">This makes sure that every time the app starts it retrieves the categories from local storage and requests a registration for these categories.</span></span>
2. <span data-ttu-id="b9357-142">MainPage.xaml.cs proje dosyasında uygulayan aşağıdaki kodu ekleyin **OnNavigatedTo** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="b9357-142">In the MainPage.xaml.cs project file, add the following code that implements the **OnNavigatedTo** method:</span></span>
   
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
   
    <span data-ttu-id="b9357-143">Bu, önceden kaydedilmiş kategorileri durumlarına dayalı ana sayfa güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="b9357-143">This updates the main page based on the status of previously saved categories.</span></span>

<span data-ttu-id="b9357-144">Uygulama tamamlanmıştır ve kategorileri kümesi kullanıcı kategorisi seçimine değiştiğinde bildirim hub'ınızla kaydolmak için kullanılan aygıt yerel depoda depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b9357-144">The app is now complete and can store a set of categories in the device local storage used to register with the notification hub whenever the user changes the selection of categories.</span></span> <span data-ttu-id="b9357-145">Ardından, biz bu uygulamaya kategori bildirimleri gönderebilir bir arka uç tanımlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="b9357-145">Next, we will define a backend that can send category notifications to this app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="b9357-146">Etiketli bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="b9357-146">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="b9357-147">Uygulamayı çalıştırın ve bildirimler oluşturma</span><span class="sxs-lookup"><span data-stu-id="b9357-147">Run the app and generate notifications</span></span>
1. <span data-ttu-id="b9357-148">Visual Studio'da derleme ve uygulamayı başlatmak için F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="b9357-148">In Visual Studio, press F5 to compile and start the app.</span></span>
   
    ![][1]
   
    <span data-ttu-id="b9357-149">Uygulama kullanıcı Arabirimi sağlayan bir dizi değiştirir sağlar Not abone olmak için kategorilerini seçin.</span><span class="sxs-lookup"><span data-stu-id="b9357-149">Note that the app UI provides a set of toggles that lets you choose the categories to subscribe to.</span></span>
2. <span data-ttu-id="b9357-150">Bir veya daha fazla kategorileri değiştirir etkinleştirin ve ardından **abone ol**.</span><span class="sxs-lookup"><span data-stu-id="b9357-150">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="b9357-151">Uygulama seçili kategorileri etiketlerine dönüştürür ve bildirim hub'ından seçili etiketleri için yeni bir cihaz kaydı ister.</span><span class="sxs-lookup"><span data-stu-id="b9357-151">The app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span> <span data-ttu-id="b9357-152">Kayıtlı kategorileri döndürülen ve iletişim kutusunda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b9357-152">The registered categories are returned and displayed in a dialog.</span></span>
   
    ![][2]
3. <span data-ttu-id="b9357-153">Kategoriler tamamlandı aboneliği olan bir onay aldıktan sonra her kategori için bildirimleri göndermek için konsol uygulamasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b9357-153">After receiving a confirmation that your categories were subscription completed, run the console app to send notifications for each categories.</span></span> <span data-ttu-id="b9357-154">Yalnızca abone olduğunuz kategorileri için bir bildirim alırsınız emin olun.</span><span class="sxs-lookup"><span data-stu-id="b9357-154">Verify you only receive a notification for the categories you have subscribed to.</span></span>
   
    ![][3]

<span data-ttu-id="b9357-155">Bu konuda tamamladınız.</span><span class="sxs-lookup"><span data-stu-id="b9357-155">You have completed this topic.</span></span>

<!--##Next steps

In this tutorial we learned how to broadcast breaking news by category. Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:

+ [Use Notification Hubs to broadcast localized breaking news]

    Learn how to expand the breaking news app to enable sending localized notifications.

+ [Notify users with Notification Hubs]

    Learn how to push notifications to specific authenticated users. This is a good solution for sending notifications only to specific users.
-->

<!-- Anchors. -->
[Add category selection to the app]: #adding-categories
[Register for notifications]: #register
[Send notifications from your back-end]: #send
[Run the app and generate notifications]: #test-app
[Next Steps]: #next-steps

<!-- Images. -->
[1]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-breakingnews.png
[2]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-registration.png
[3]: ./media/notification-hubs-windows-phone-send-breaking-news/notification-hub-toast.png



<!-- URLs.-->
<span data-ttu-id="b9357-156">[Notification Hubs ile çalışmaya başlama]: /manage/services/notification-hubs/get-started-notification-hubs-wp8/</span><span class="sxs-lookup"><span data-stu-id="b9357-156">[Get started with Notification Hubs]: /manage/services/notification-hubs/get-started-notification-hubs-wp8/</span></span>
[Use Notification Hubs to broadcast localized breaking news]: ../breakingnews-localized-wp8.md
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users/
[Mobile Service]: /develop/mobile/tutorials/get-started
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for Windows Phone]: ??

