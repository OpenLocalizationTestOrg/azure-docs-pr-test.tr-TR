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
# <a name="use-notification-hubs-to-send-breaking-news"></a><span data-ttu-id="04626-103">Son dakika haberleri göndermek için Notification Hubs kullanma</span><span class="sxs-lookup"><span data-stu-id="04626-103">Use Notification Hubs to send breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="04626-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="04626-104">Overview</span></span>
<span data-ttu-id="04626-105">Bu konu Azure Notification Hubs son dakika haberi bildirimleri Windows mağazası veya Windows Phone 8.1 (Silverlight olmayan) uygulamasına yayını için nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="04626-105">This topic shows you how to use Azure Notification Hubs to broadcast breaking news notifications to a Windows Store or Windows Phone 8.1 (non-Silverlight) app.</span></span> <span data-ttu-id="04626-106">Windows Phone 8.1 Silverlight'ı hedefliyorsanız lütfen [Windows Evrensel](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) sürümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="04626-106">If you are targeting Windows Phone 8.1 Silverlight, please refer to the [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) version.</span></span> <span data-ttu-id="04626-107">Tamamlandığında, ilgilendiğiniz haber kategorileri dökümü için kaydedilecek olması ve yalnızca bu kategorilerin anında iletme bildirimlerini almak.</span><span class="sxs-lookup"><span data-stu-id="04626-107">When complete, you will be able to register for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="04626-108">Bu sayıda uygulama için genel bir desen bildirimleri daha önce bunları, örneğin RSS Okuyucu uygulamaları müzik fanları için ilgi derlendiğinden vb. kullanıcı gruplarının gönderilmesi sahip olduğu bir senaryodur.</span><span class="sxs-lookup"><span data-stu-id="04626-108">This scenario is a common pattern for many apps where notifications have to be sent to groups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, and so on.</span></span> 

<span data-ttu-id="04626-109">Yayın senaryoları etkin bir veya daha fazla dahil ederek *etiketleri* bir kayıt bildirim hub'ı oluştururken.</span><span class="sxs-lookup"><span data-stu-id="04626-109">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in the notification hub.</span></span> <span data-ttu-id="04626-110">Bildirimler için bir etiket gönderildiğinde, kaydettiğiniz tüm etiket cihazlarda bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="04626-110">When notifications are sent to a tag, all devices that have registered for the tag will receive the notification.</span></span> <span data-ttu-id="04626-111">Etiketleri yalnızca dizeleri olduğundan, bunlar önceden hazırlanması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="04626-111">Because tags are simply strings, they do not have to be provisioned in advance.</span></span> <span data-ttu-id="04626-112">Etiketler hakkında daha fazla bilgi için başvurmak [bildirim hub'ları Yönlendirme ve etiket ifadeleri](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="04626-112">For more information about tags, refer to [Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

> [!NOTE]
> <span data-ttu-id="04626-113">Windows mağazası ve Windows Phone projeleri sürüm 8.1 ve önceki Visual Studio 2017 içinde desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="04626-113">Windows Store and Windows Phone projects version 8.1 and earlier are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="04626-114">Daha fazla bilgi için bkz. [Visual Studio 2017 Platform Desteği ve Uyumluluk](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="04626-114">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="04626-115">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="04626-115">Prerequisites</span></span>
<span data-ttu-id="04626-116">Bu konu, oluşturduğunuz uygulama inşa edilmiştir [Notification Hubs ile çalışmaya başlama][get-started].</span><span class="sxs-lookup"><span data-stu-id="04626-116">This topic builds on the app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="04626-117">Bu öğreticiye başlamadan önce önce tamamlamış olmalıdır [Notification Hubs ile çalışmaya başlama][get-started].</span><span class="sxs-lookup"><span data-stu-id="04626-117">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-to-the-app"></a><span data-ttu-id="04626-118">Kategori seçimi için uygulama ekleme</span><span class="sxs-lookup"><span data-stu-id="04626-118">Add category selection to the app</span></span>
<span data-ttu-id="04626-119">İlk adım, kullanıcı Arabirimi öğeleri kaydetmek için kategoriler seçmesini sağlayan varolan ana sayfanıza eklemektir.</span><span class="sxs-lookup"><span data-stu-id="04626-119">The first step is to add the UI elements to your existing main page that enable the user to select categories to register.</span></span> <span data-ttu-id="04626-120">Bir kullanıcı tarafından seçilen kategoriler cihazda depolanır.</span><span class="sxs-lookup"><span data-stu-id="04626-120">The categories selected by a user are stored on the device.</span></span> <span data-ttu-id="04626-121">Uygulama başlatıldığında bir aygıt kaydı bildirim hub'ınıza seçili kategorileri etiketler oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="04626-121">When the app starts, a device registration is created in your notification hub with the selected categories as tags.</span></span>

1. <span data-ttu-id="04626-122">MainPage.xaml proje dosyasını açın, sonra aşağıdaki kodu kopyalayın **kılavuz** öğe:</span><span class="sxs-lookup"><span data-stu-id="04626-122">Open the MainPage.xaml project file, then copy the following code in the **Grid** element:</span></span>
   
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
2. <span data-ttu-id="04626-123">Sağ tıklayın **paylaşılan** proje ve adlı yeni bir sınıf ekleyin **bildirimleri**, ekleme **ortak** değiştiricisi sınıf tanımına sonra aşağıdakileri ekleyin  **kullanarak** deyimleri için yeni kod dosyası:</span><span class="sxs-lookup"><span data-stu-id="04626-123">Right click the **Shared** project and add a new class named **Notifications**, add the **public** modifier to the class definition, then add the following **using** statements to the new code file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.Storage;
        using System.Threading.Tasks;
3. <span data-ttu-id="04626-124">Aşağıdaki kodu yeni dosyaya kopyalayın **bildirimleri** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="04626-124">Copy the following code into the new **Notifications** class:</span></span>
   
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
   
    <span data-ttu-id="04626-125">Bu sınıf yerel depolama almak için bu aygıtın haber kategorilerini depolamak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="04626-125">This class uses the local storage to store the categories of news that this device has to receive.</span></span> <span data-ttu-id="04626-126">Arama yerine unutmayın *RegisterNativeAsync* diyoruz yöntemi *RegisterTemplateAsync* şablonu kayıt kullanarak kategorileri için kaydedilecek.</span><span class="sxs-lookup"><span data-stu-id="04626-126">Note that instead of calling the *RegisterNativeAsync* method we call *RegisterTemplateAsync* to register for the categories using a template registration.</span></span> 
   
    <span data-ttu-id="04626-127">Ayrıca ("simpleWNSTemplateExample"), şablon için bir ad (örneğin bir bildirimleri için) ve biri döşeme için birden fazla şablon kaydetmek istiyoruz ve bunları güncelleştirmek veya bunları silmek için ad ihtiyacımız çünkü sunuyoruz.</span><span class="sxs-lookup"><span data-stu-id="04626-127">We also provide a name for the template ("simpleWNSTemplateExample"), because we might want to register more than one template (for instance one for toast notifications and one for tiles) and we need to name them in order to be able to update or delete them.</span></span>
   
    <span data-ttu-id="04626-128">Bir aygıt ile aynı etiketi birden fazla şablon kaydederse, bir gelen ileti etiketi içinde birden fazla bildirim sonuçlanacak hedefleme aygıt (her şablon için bir tane) teslim olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="04626-128">Note that if a device registers multiple templates with the same tag, an incoming message targeting that tag will result in multiple notifications delivered to the device (one for each template).</span></span> <span data-ttu-id="04626-129">Bu davranış, aynı mantıksal ileti örneği için bir Windows mağazası uygulamasında bir gösterge ve bildirim gösteren birden çok görsel bildirimler neden olduğunda yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="04626-129">This behavior is useful when the same logical message has to result in multiple visual notifications, for instance showing both a badge and a toast in a Windows Store application.</span></span>
   
    <span data-ttu-id="04626-130">Şablonlar hakkında daha fazla bilgi için bkz: [şablonları](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="04626-130">For more information on templates, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>
4. <span data-ttu-id="04626-131">App.xaml.cs proje dosyasında aşağıdaki özellik eklemek **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="04626-131">In the App.xaml.cs project file, add the following property to the **App** class:</span></span>
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
    <span data-ttu-id="04626-132">Bu özellik oluşturmak ve erişmek için kullanılan bir **bildirimleri** örneği.</span><span class="sxs-lookup"><span data-stu-id="04626-132">This property is used to create and access a **Notifications** instance.</span></span>
   
    <span data-ttu-id="04626-133">Yukarıdaki kodla `<hub name>` ve `<connection string with listen access>` , bildirim hub'ı adı ve bağlantı dizesinde yer tutucularını *DefaultListenSharedAccessSignature* daha önce edindiğiniz.</span><span class="sxs-lookup"><span data-stu-id="04626-133">In the above code, replace the `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and the connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="04626-134">Bir istemci uygulaması ile dağıtılmış kimlik bilgileri genellikle güvenli olmadığı için istemci uygulamanızı dinleme erişim için anahtar yalnızca dağıtmanız.</span><span class="sxs-lookup"><span data-stu-id="04626-134">Because credentials that are distributed with a client app are not generally secure, you should only distribute the key for listen access with your client app.</span></span> <span data-ttu-id="04626-135">Bildirimler, ancak var olan kayıtlar için kaydetmek için uygulamanızın değiştirilemez erişimi etkinleştirir dinleyin ve bildirim gönderilemiyor.</span><span class="sxs-lookup"><span data-stu-id="04626-135">Listen access enables your app to register for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="04626-136">Tam erişim anahtarı, bir güvenli arka uç hizmetinde bildirimleri gönderme ve var olan kayıtlar değiştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="04626-136">The full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
5. <span data-ttu-id="04626-137">MainPage.xaml.cs dosyasında aşağıdaki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="04626-137">In your MainPage.xaml.cs, add the following line:</span></span>
   
        using Windows.UI.Popups;
6. <span data-ttu-id="04626-138">MainPage.xaml.cs proje dosyasında aşağıdaki yöntemi ekleyin:</span><span class="sxs-lookup"><span data-stu-id="04626-138">In the MainPage.xaml.cs project file, add the following method:</span></span>
   
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
   
    <span data-ttu-id="04626-139">Bu yöntem kategorileri ve kullandığı bir liste oluşturur **bildirimleri** listesi yerel depolama alanına depolar ve karşılık gelen kaydetmek için sınıfı, bildirim hub'ınıza etiketler.</span><span class="sxs-lookup"><span data-stu-id="04626-139">This method creates a list of categories and uses the **Notifications** class to store the list in the local storage and register the corresponding tags with your notification hub.</span></span> <span data-ttu-id="04626-140">Kategoriler değiştirildiğinde kaydı yeni kategoriler yeniden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="04626-140">When categories are changed, the registration is recreated with the new categories.</span></span>

<span data-ttu-id="04626-141">Uygulamanızı kategorileri kümesi cihazın yerel depolama depolamak ve kullanıcı kategorisi seçimine değiştiğinde bildirim hub'ınızla kaydolmak için sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="04626-141">Your app is now able to store a set of categories in local storage on the device and register with the notification hub whenever the user changes the selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="04626-142">Bildirimler için kaydolun</span><span class="sxs-lookup"><span data-stu-id="04626-142">Register for notifications</span></span>
<span data-ttu-id="04626-143">Yerel depolamada depolanan kategorileri kullanarak başlangıçtaki bildirim hub'ı ile adımları kaydedin.</span><span class="sxs-lookup"><span data-stu-id="04626-143">These steps register with the notification hub on startup using the categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="04626-144">Windows bildirim Hizmeti'ni (WNS) tarafından atanan URI kanal herhangi bir zamanda değiştiğinden bildirimlerinin sık bildirim hataları önlemek için kayıt olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="04626-144">Because the channel URI assigned by the Windows Notification Service (WNS) can change at any time, you should register for notifications frequently to avoid notification failures.</span></span> <span data-ttu-id="04626-145">Bu örnek uygulama başladıktan her zaman bir bildirime kaydolur.</span><span class="sxs-lookup"><span data-stu-id="04626-145">This example registers for notification every time that the app starts.</span></span> <span data-ttu-id="04626-146">Sık çalıştırılan uygulamalar için günde bir kereden fazla, büyük olasılıkla bir günden az itibaren önceki kayıt aktarılırsa bant genişliğinden tasarruf etmek kayıt atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04626-146">For apps that are run frequently, more than once a day, you can probably skip registration to preserve bandwidth if less than a day has passed since the previous registration.</span></span>
> 
> 

1. <span data-ttu-id="04626-147">App.xaml.cs dosyasını açıp güncelleştirme **Initnotificationsasync** yöntemini kullanmak üzere `notifications` abone olmak için sınıf tabanlı kategorilerindeki.</span><span class="sxs-lookup"><span data-stu-id="04626-147">Open the App.xaml.cs file and update the **InitNotificationsAsync** method to use the `notifications` class to subscribe based on categories.</span></span>
   
        // *** Remove or comment out these lines *** 
        //var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
        //var hub = new NotificationHub("your hub name", "your listen connection string");
        //var result = await hub.RegisterNativeAsync(channel.Uri);
   
        var result = await notifications.SubscribeToCategories();
   
    <span data-ttu-id="04626-148">Bu uygulama her başlatıldığında kategorileri yerel depodan alır ve bu kategorilerin bir kayda istekleri emin olur.</span><span class="sxs-lookup"><span data-stu-id="04626-148">This makes sure that every time the app starts it retrieves the categories from local storage and requests a registeration for these categories.</span></span> <span data-ttu-id="04626-149">**Initnotificationsasync** yöntemi, bir parçası olarak oluşturulmuş [Notification Hubs ile çalışmaya başlama] [ get-started] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="04626-149">The **InitNotificationsAsync** method was created as part of the [Get started with Notification Hubs][get-started] tutorial.</span></span>
2. <span data-ttu-id="04626-150">MainPage.xaml.cs proje dosyasına aşağıdaki kodu ekleyin *OnNavigatedTo* yöntemi:</span><span class="sxs-lookup"><span data-stu-id="04626-150">In the MainPage.xaml.cs project file, add the following code to the *OnNavigatedTo* method:</span></span>
   
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
   
    <span data-ttu-id="04626-151">Bu, önceden kaydedilmiş kategorileri durumlarına dayalı ana sayfa güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="04626-151">This updates the main page based on the status of previously saved categories.</span></span>

<span data-ttu-id="04626-152">Uygulama tamamlanmıştır ve kategorileri kümesi kullanıcı kategorisi seçimine değiştiğinde bildirim hub'ınızla kaydolmak için kullanılan aygıt yerel depoda depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04626-152">The app is now complete and can store a set of categories in the device local storage used to register with the notification hub whenever the user changes the selection of categories.</span></span> <span data-ttu-id="04626-153">Ardından, biz bu uygulamaya kategori bildirimleri gönderebilir bir arka uç tanımlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="04626-153">Next, we will define a backend that can send category notifications to this app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="04626-154">Etiketli bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="04626-154">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-the-app-and-generate-notifications"></a><span data-ttu-id="04626-155">Uygulamayı çalıştırın ve bildirimler oluşturma</span><span class="sxs-lookup"><span data-stu-id="04626-155">Run the app and generate notifications</span></span>
1. <span data-ttu-id="04626-156">Visual Studio'da derleme ve uygulamayı başlatmak için F5 tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="04626-156">In Visual Studio, press F5 to compile and start the app.</span></span>
   
    ![][1]
   
    <span data-ttu-id="04626-157">Uygulama kullanıcı Arabirimi sağlayan bir dizi değiştirir sağlar Not abone olmak için kategorilerini seçin.</span><span class="sxs-lookup"><span data-stu-id="04626-157">Note that the app UI provides a set of toggles that lets you choose the categories to subscribe to.</span></span>
2. <span data-ttu-id="04626-158">Bir veya daha fazla kategorileri değiştirir etkinleştirin ve ardından **abone ol**.</span><span class="sxs-lookup"><span data-stu-id="04626-158">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="04626-159">Uygulama seçili kategorileri etiketlerine dönüştürür ve bildirim hub'ından seçili etiketleri için yeni bir cihaz kaydı ister.</span><span class="sxs-lookup"><span data-stu-id="04626-159">The app converts the selected categories into tags and requests a new device registration for the selected tags from the notification hub.</span></span> <span data-ttu-id="04626-160">Kayıtlı kategorileri döndürülen ve iletişim kutusunda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="04626-160">The registered categories are returned and displayed in a dialog.</span></span>
   
    ![][19]
3. <span data-ttu-id="04626-161">Yeni bir bildirim arka ucundan aşağıdaki yollardan biriyle gönder:</span><span class="sxs-lookup"><span data-stu-id="04626-161">Send a new notification from the backend in one of the following ways:</span></span>
   
   * <span data-ttu-id="04626-162">**Konsol uygulaması:** konsol uygulaması başlatın.</span><span class="sxs-lookup"><span data-stu-id="04626-162">**Console app:** start the console app.</span></span>
   * <span data-ttu-id="04626-163">**Java/PHP:** uygulama/betiğini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="04626-163">**Java/PHP:** run your app/script.</span></span>
     
     <span data-ttu-id="04626-164">Seçili kategorileri için bildirimleri bildirimleri görünür.</span><span class="sxs-lookup"><span data-stu-id="04626-164">Notifications for the selected categories appear as toast notifications.</span></span>
     
     ![][14]

## <a name="next-steps"></a><span data-ttu-id="04626-165">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="04626-165">Next steps</span></span>
<span data-ttu-id="04626-166">Bu öğreticide biz kategoriye göre son dakika haberleri yayın öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="04626-166">In this tutorial we learned how to broadcast breaking news by category.</span></span> <span data-ttu-id="04626-167">Diğer gelişmiş Notification Hubs senaryoları vurgulayın aşağıdaki öğreticiler birini Tamamlanıyor göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="04626-167">Consider completing one of the following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="04626-168">[Yerelleştirilmiş son dakika haberleri yayınlamak için Notification Hubs'ı kullanma]</span><span class="sxs-lookup"><span data-stu-id="04626-168">[Use Notification Hubs to broadcast localized breaking news]</span></span>
  
    <span data-ttu-id="04626-169">Gönderen yerelleştirilmiş bildirimlerini etkinleştirmek için en son haberleri uygulama genişletin öğrenin.</span><span class="sxs-lookup"><span data-stu-id="04626-169">Learn how to expand the breaking news app to enable sending localized notifications.</span></span>

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
<span data-ttu-id="04626-170">[Yerelleştirilmiş son dakika haberleri yayınlamak için Notification Hubs'ı kullanma]: /manage/services/notification-hubs/breaking-news-localized-dotnet/</span><span class="sxs-lookup"><span data-stu-id="04626-170">[Use Notification Hubs to broadcast localized breaking news]: /manage/services/notification-hubs/breaking-news-localized-dotnet/</span></span>
[Notify users with Notification Hubs]: /manage/services/notification-hubs/notify-users
[Mobile Service]: /develop/mobile/tutorials/get-started/
[Notification Hubs Guidance]: http://msdn.microsoft.com/library/jj927170.aspx
[Notification Hubs How-To for Windows Store]: http://msdn.microsoft.com/library/jj927172.aspx
[Submit an app page]: http://go.microsoft.com/fwlink/p/?LinkID=266582
[My Applications]: http://go.microsoft.com/fwlink/p/?LinkId=262039
[Live SDK for Windows]: http://go.microsoft.com/fwlink/p/?LinkId=262253

[wns object]: http://go.microsoft.com/fwlink/p/?LinkId=260591
