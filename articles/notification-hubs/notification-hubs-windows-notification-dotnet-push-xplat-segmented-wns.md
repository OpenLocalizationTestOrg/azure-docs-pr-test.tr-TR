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
# <a name="use-notification-hubs-toosend-breaking-news"></a><span data-ttu-id="bf58d-103">Bildirim hub'ları toosend son dakika haberleri kullanın</span><span class="sxs-lookup"><span data-stu-id="bf58d-103">Use Notification Hubs toosend breaking news</span></span>
[!INCLUDE [notification-hubs-selector-breaking-news](../../includes/notification-hubs-selector-breaking-news.md)]

## <a name="overview"></a><span data-ttu-id="bf58d-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="bf58d-104">Overview</span></span>
<span data-ttu-id="bf58d-105">Bu konu, nasıl gösterir toouse Azure Notification Hubs toobroadcast haber bildirimleri tooa Windows mağazası veya Windows Phone 8.1 (Silverlight olmayan) uygulamasına kesiliyor.</span><span class="sxs-lookup"><span data-stu-id="bf58d-105">This topic shows you how toouse Azure Notification Hubs toobroadcast breaking news notifications tooa Windows Store or Windows Phone 8.1 (non-Silverlight) app.</span></span> <span data-ttu-id="bf58d-106">Windows Phone 8.1 Silverlight hedefliyorsanız Lütfen toohello bakın [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) sürümü.</span><span class="sxs-lookup"><span data-stu-id="bf58d-106">If you are targeting Windows Phone 8.1 Silverlight, please refer toohello [Windows Phone](notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md) version.</span></span> <span data-ttu-id="bf58d-107">Tamamlandığında, ilgilendiğiniz haber kategorileri sonu için mümkün tooregister olmalı ve yalnızca bu kategorilerin anında iletme bildirimlerini almak.</span><span class="sxs-lookup"><span data-stu-id="bf58d-107">When complete, you will be able tooregister for breaking news categories you are interested in, and receive only push notifications for those categories.</span></span> <span data-ttu-id="bf58d-108">Bu sayıda uygulama için genel bir desen bildirimleri gönderilen toobe toogroups daha önce bunları, örneğin RSS Okuyucu uygulamaları müzik fanları için ilgi derlendiğinden vb. kullanıcıların sahip olduğu bir senaryodur.</span><span class="sxs-lookup"><span data-stu-id="bf58d-108">This scenario is a common pattern for many apps where notifications have toobe sent toogroups of users that have previously declared interest in them, e.g. RSS reader, apps for music fans, and so on.</span></span> 

<span data-ttu-id="bf58d-109">Yayın senaryoları etkin bir veya daha fazla dahil ederek *etiketleri* bir kayıt hello bildirim hub'oluştururken.</span><span class="sxs-lookup"><span data-stu-id="bf58d-109">Broadcast scenarios are enabled by including one or more *tags* when creating a registration in hello notification hub.</span></span> <span data-ttu-id="bf58d-110">Bildirimleri tooa etiketi gönderildiğinde kayıtlı tüm aygıtları hello etiketi hello bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="bf58d-110">When notifications are sent tooa tag, all devices that have registered for hello tag will receive hello notification.</span></span> <span data-ttu-id="bf58d-111">Etiketleri yalnızca dizeleri olduğundan, önceden sağlanmış toobe gerekmez.</span><span class="sxs-lookup"><span data-stu-id="bf58d-111">Because tags are simply strings, they do not have toobe provisioned in advance.</span></span> <span data-ttu-id="bf58d-112">Etiketler hakkında daha fazla bilgi için çok başvuran[bildirim hub'ları Yönlendirme ve etiket ifadeleri](notification-hubs-tags-segment-push-message.md).</span><span class="sxs-lookup"><span data-stu-id="bf58d-112">For more information about tags, refer too[Notification Hubs Routing and Tag Expressions](notification-hubs-tags-segment-push-message.md).</span></span>

> [!NOTE]
> <span data-ttu-id="bf58d-113">Windows mağazası ve Windows Phone projeleri sürüm 8.1 ve önceki Visual Studio 2017 içinde desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="bf58d-113">Windows Store and Windows Phone projects version 8.1 and earlier are not supported in Visual Studio 2017.</span></span>  <span data-ttu-id="bf58d-114">Daha fazla bilgi için bkz. [Visual Studio 2017 Platform Desteği ve Uyumluluk](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span><span class="sxs-lookup"><span data-stu-id="bf58d-114">For more information, see [Visual Studio 2017 Platform Targeting and Compatibility](https://www.visualstudio.com/en-us/productinfo/vs2017-compatibility-vs).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="bf58d-115">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="bf58d-115">Prerequisites</span></span>
<span data-ttu-id="bf58d-116">Bu konu içinde oluşturduğunuz hello uygulama inşa edilmiştir [Notification Hubs ile çalışmaya başlama][get-started].</span><span class="sxs-lookup"><span data-stu-id="bf58d-116">This topic builds on hello app you created in [Get started with Notification Hubs][get-started].</span></span> <span data-ttu-id="bf58d-117">Bu öğreticiye başlamadan önce önce tamamlamış olmalıdır [Notification Hubs ile çalışmaya başlama][get-started].</span><span class="sxs-lookup"><span data-stu-id="bf58d-117">Before starting this tutorial, you must have already completed [Get started with Notification Hubs][get-started].</span></span>

## <a name="add-category-selection-toohello-app"></a><span data-ttu-id="bf58d-118">Kategori seçimi toohello uygulama Ekle</span><span class="sxs-lookup"><span data-stu-id="bf58d-118">Add category selection toohello app</span></span>
<span data-ttu-id="bf58d-119">Merhaba ilk adım, hello kullanıcı tooselect kategorileri tooregister etkinleştirmek tooadd hello kullanıcı Arabirimi öğeleri tooyour varolan ana sayfasıdır.</span><span class="sxs-lookup"><span data-stu-id="bf58d-119">hello first step is tooadd hello UI elements tooyour existing main page that enable hello user tooselect categories tooregister.</span></span> <span data-ttu-id="bf58d-120">bir kullanıcı tarafından seçilen hello kategoriler hello aygıtta depolanır.</span><span class="sxs-lookup"><span data-stu-id="bf58d-120">hello categories selected by a user are stored on hello device.</span></span> <span data-ttu-id="bf58d-121">Merhaba uygulama başlatıldığında bir aygıt kaydı bildirim hub'ınıza seçili hello kategorileri etiketler oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="bf58d-121">When hello app starts, a device registration is created in your notification hub with hello selected categories as tags.</span></span>

1. <span data-ttu-id="bf58d-122">Açık hello MainPage.xaml proje dosyası sonra kopyalama hello hello kodda aşağıdaki **kılavuz** öğe:</span><span class="sxs-lookup"><span data-stu-id="bf58d-122">Open hello MainPage.xaml project file, then copy hello following code in hello **Grid** element:</span></span>
   
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
2. <span data-ttu-id="bf58d-123">Merhaba sağ tıklayın **paylaşılan** proje ve adlı yeni bir sınıf ekleyin **bildirimleri**, hello eklemek **ortak** değiştiricisi toohello sınıf tanımının, ardından aşağıdaki hello ekleyin**kullanarak** deyimleri toohello yeni kod dosyası:</span><span class="sxs-lookup"><span data-stu-id="bf58d-123">Right click hello **Shared** project and add a new class named **Notifications**, add hello **public** modifier toohello class definition, then add hello following **using** statements toohello new code file:</span></span>
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.Storage;
        using System.Threading.Tasks;
3. <span data-ttu-id="bf58d-124">Kopya hello aşağıdaki kod hello yeni **bildirimleri** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="bf58d-124">Copy hello following code into hello new **Notifications** class:</span></span>
   
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
   
    <span data-ttu-id="bf58d-125">Bu sınıf hello yerel depolama toostore hello kategorilerini bu aygıtta tooreceive olduğunu haber kullanır.</span><span class="sxs-lookup"><span data-stu-id="bf58d-125">This class uses hello local storage toostore hello categories of news that this device has tooreceive.</span></span> <span data-ttu-id="bf58d-126">Arama hello yerine unutmayın *RegisterNativeAsync* diyoruz yöntemi *RegisterTemplateAsync* tooregister şablonu kayıt kullanarak hello kategorileri için.</span><span class="sxs-lookup"><span data-stu-id="bf58d-126">Note that instead of calling hello *RegisterNativeAsync* method we call *RegisterTemplateAsync* tooregister for hello categories using a template registration.</span></span> 
   
    <span data-ttu-id="bf58d-127">Biz de hello şablonu ("simpleWNSTemplateExample") için bir ad sağlayın, çünkü tooregister (örneğin biri bildirimleri) ve biri kutucuklar için birden fazla şablon istiyoruz ve tooname ihtiyacımız bunları toobe mümkün tooupdate sipariş veya silin.</span><span class="sxs-lookup"><span data-stu-id="bf58d-127">We also provide a name for hello template ("simpleWNSTemplateExample"), because we might want tooregister more than one template (for instance one for toast notifications and one for tiles) and we need tooname them in order toobe able tooupdate or delete them.</span></span>
   
    <span data-ttu-id="bf58d-128">Bir aygıt hello aynı etiketi sonuçlanır hedefleme gelen ileti etiketi ile birden fazla şablon kaydederse birden fazla bildirim toohello aygıt (her şablon için bir tane) teslim unutmayın.</span><span class="sxs-lookup"><span data-stu-id="bf58d-128">Note that if a device registers multiple templates with hello same tag, an incoming message targeting that tag will result in multiple notifications delivered toohello device (one for each template).</span></span> <span data-ttu-id="bf58d-129">Bu davranış, Hello aynı mantıksal ileti tooresult örneği için bir Windows mağazası uygulamasında bir gösterge ve bildirim gösteren birden çok görsel bildirimler sahip yararlıdır.</span><span class="sxs-lookup"><span data-stu-id="bf58d-129">This behavior is useful when hello same logical message has tooresult in multiple visual notifications, for instance showing both a badge and a toast in a Windows Store application.</span></span>
   
    <span data-ttu-id="bf58d-130">Şablonlar hakkında daha fazla bilgi için bkz: [şablonları](notification-hubs-templates-cross-platform-push-messages.md).</span><span class="sxs-lookup"><span data-stu-id="bf58d-130">For more information on templates, see [Templates](notification-hubs-templates-cross-platform-push-messages.md).</span></span>
4. <span data-ttu-id="bf58d-131">Özellik toohello aşağıdaki hello Hello App.xaml.cs proje dosyasında eklemek **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="bf58d-131">In hello App.xaml.cs project file, add hello following property toohello **App** class:</span></span>
   
        public Notifications notifications = new Notifications("<hub name>", "<connection string with listen access>");
   
    <span data-ttu-id="bf58d-132">Bu özellik kullanılan toocreate ve erişimi olan bir **bildirimleri** örneği.</span><span class="sxs-lookup"><span data-stu-id="bf58d-132">This property is used toocreate and access a **Notifications** instance.</span></span>
   
    <span data-ttu-id="bf58d-133">Kod yukarıda Hello hello yerine `<hub name>` ve `<connection string with listen access>` bildirim hub'ı adı ve hello için bağlantı dizenizi yer tutucularını *DefaultListenSharedAccessSignature* daha önce edindiğiniz.</span><span class="sxs-lookup"><span data-stu-id="bf58d-133">In hello above code, replace hello `<hub name>` and `<connection string with listen access>` placeholders with your notification hub name and hello connection string for *DefaultListenSharedAccessSignature* that you obtained earlier.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="bf58d-134">Bir istemci uygulaması ile dağıtılmış kimlik bilgileri genellikle güvenli olmadığından, yalnızca hello anahtarını dinleme erişim için istemci uygulamanızı dağıtmak.</span><span class="sxs-lookup"><span data-stu-id="bf58d-134">Because credentials that are distributed with a client app are not generally secure, you should only distribute hello key for listen access with your client app.</span></span> <span data-ttu-id="bf58d-135">Bildirimler, ancak var olan kayıtlar için uygulama tooregister değiştirilemez erişimi etkinleştirir dinleyin ve bildirim gönderilemiyor.</span><span class="sxs-lookup"><span data-stu-id="bf58d-135">Listen access enables your app tooregister for notifications, but existing registrations cannot be modified and notifications cannot be sent.</span></span> <span data-ttu-id="bf58d-136">Merhaba tam erişim tuşu bir güvenli arka uç hizmetinde bildirimleri gönderme ve var olan kayıtlar değiştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="bf58d-136">hello full access key is used in a secured backend service for sending notifications and changing existing registrations.</span></span>
   > 
   > 
5. <span data-ttu-id="bf58d-137">MainPage.xaml.cs dosyasında hello aşağıdaki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bf58d-137">In your MainPage.xaml.cs, add hello following line:</span></span>
   
        using Windows.UI.Popups;
6. <span data-ttu-id="bf58d-138">Merhaba MainPage.xaml.cs proje dosyasında yöntemi aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="bf58d-138">In hello MainPage.xaml.cs project file, add hello following method:</span></span>
   
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
   
    <span data-ttu-id="bf58d-139">Bu yöntem kategorileri ve kullandığı hello listesini oluşturur **bildirimleri** sınıf toostore hello hello yerel depolama listesinde ve bildirim hub'ınıza hello karşılık gelen etiketleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="bf58d-139">This method creates a list of categories and uses hello **Notifications** class toostore hello list in hello local storage and register hello corresponding tags with your notification hub.</span></span> <span data-ttu-id="bf58d-140">Kategoriler değiştirildiğinde hello kayıt hello yeni kategorileri ile yeniden oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="bf58d-140">When categories are changed, hello registration is recreated with hello new categories.</span></span>

<span data-ttu-id="bf58d-141">Uygulamanızı mümkün toostore kategorileri kümesi hello cihazda yerel depolama sunulmuştur ve kategorisi seçimine hello kullanıcı değişiklikleri hello her hello bildirim hub'ı ile kaydedin.</span><span class="sxs-lookup"><span data-stu-id="bf58d-141">Your app is now able toostore a set of categories in local storage on hello device and register with hello notification hub whenever hello user changes hello selection of categories.</span></span>

## <a name="register-for-notifications"></a><span data-ttu-id="bf58d-142">Bildirimler için kaydolun</span><span class="sxs-lookup"><span data-stu-id="bf58d-142">Register for notifications</span></span>
<span data-ttu-id="bf58d-143">Yerel depolamada depolanan hello kategorileri kullanarak başlangıçta hello bildirim hub'ı ile adımları kaydedin.</span><span class="sxs-lookup"><span data-stu-id="bf58d-143">These steps register with hello notification hub on startup using hello categories that have been stored in local storage.</span></span>

> [!NOTE]
> <span data-ttu-id="bf58d-144">Merhaba kanal URI'sini hello Windows bildirim Hizmeti'ni (WNS) tarafından atanan herhangi bir zamanda değiştiğinden bildirimleri için tooavoid bildirim hataları sık kaydetmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="bf58d-144">Because hello channel URI assigned by hello Windows Notification Service (WNS) can change at any time, you should register for notifications frequently tooavoid notification failures.</span></span> <span data-ttu-id="bf58d-145">Bu hello uygulama her başlatıldığında bu örnek bir bildirime kaydolur.</span><span class="sxs-lookup"><span data-stu-id="bf58d-145">This example registers for notification every time that hello app starts.</span></span> <span data-ttu-id="bf58d-146">Bir günden az hello önceki kayıt itibaren aktarılırsa, sık çalıştırılan uygulamalar için günde bir kereden fazla, büyük olasılıkla kayıt toopreserve bant genişliği atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf58d-146">For apps that are run frequently, more than once a day, you can probably skip registration toopreserve bandwidth if less than a day has passed since hello previous registration.</span></span>
> 
> 

1. <span data-ttu-id="bf58d-147">Açık hello App.xaml.cs dosyasını ve güncelleştirme hello **Initnotificationsasync** yöntemi toouse hello `notifications` sınıfı toosubscribe alarak kategorilere göre.</span><span class="sxs-lookup"><span data-stu-id="bf58d-147">Open hello App.xaml.cs file and update hello **InitNotificationsAsync** method toouse hello `notifications` class toosubscribe based on categories.</span></span>
   
        // *** Remove or comment out these lines *** 
        //var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
        //var hub = new NotificationHub("your hub name", "your listen connection string");
        //var result = await hub.RegisterNativeAsync(channel.Uri);
   
        var result = await notifications.SubscribeToCategories();
   
    <span data-ttu-id="bf58d-148">Bu hello uygulama her başlatıldığında hello kategorileri yerel depodan alır ve bu kategorilerin bir kayda istekleri emin olur.</span><span class="sxs-lookup"><span data-stu-id="bf58d-148">This makes sure that every time hello app starts it retrieves hello categories from local storage and requests a registeration for these categories.</span></span> <span data-ttu-id="bf58d-149">Merhaba **Initnotificationsasync** yöntemi hello bir parçası olarak oluşturulmuş [Notification Hubs ile çalışmaya başlama] [ get-started] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="bf58d-149">hello **InitNotificationsAsync** method was created as part of hello [Get started with Notification Hubs][get-started] tutorial.</span></span>
2. <span data-ttu-id="bf58d-150">Merhaba MainPage.xaml.cs proje dosyasında kodu toohello aşağıdaki hello eklemek *OnNavigatedTo* yöntemi:</span><span class="sxs-lookup"><span data-stu-id="bf58d-150">In hello MainPage.xaml.cs project file, add hello following code toohello *OnNavigatedTo* method:</span></span>
   
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
   
    <span data-ttu-id="bf58d-151">Merhaba durumlarına önceden dayalı bu güncelleştirmeleri hello ana bir sayfayı kategorileri kaydedildi.</span><span class="sxs-lookup"><span data-stu-id="bf58d-151">This updates hello main page based on hello status of previously saved categories.</span></span>

<span data-ttu-id="bf58d-152">Merhaba uygulama tamamlanmıştır ve kategorisi seçimine hello kullanıcı değişiklikleri hello her kategori kümesini hello aygıt kullanılan yerel depolama tooregister hello bildirim hub'ı ile depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bf58d-152">hello app is now complete and can store a set of categories in hello device local storage used tooregister with hello notification hub whenever hello user changes hello selection of categories.</span></span> <span data-ttu-id="bf58d-153">Ardından, biz kategori bildirimleri toothis uygulamanın gönderebileceği bir arka uç tanımlayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="bf58d-153">Next, we will define a backend that can send category notifications toothis app.</span></span>

## <a name="sending-tagged-notifications"></a><span data-ttu-id="bf58d-154">Etiketli bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="bf58d-154">Sending tagged notifications</span></span>
[!INCLUDE [notification-hubs-send-categories-template](../../includes/notification-hubs-send-categories-template.md)]

## <a name="run-hello-app-and-generate-notifications"></a><span data-ttu-id="bf58d-155">Merhaba uygulamayı çalıştırın ve bildirimler oluşturma</span><span class="sxs-lookup"><span data-stu-id="bf58d-155">Run hello app and generate notifications</span></span>
1. <span data-ttu-id="bf58d-156">Visual Studio'da F5 toocompile tuşuna basın ve hello uygulamayı başlatın.</span><span class="sxs-lookup"><span data-stu-id="bf58d-156">In Visual Studio, press F5 toocompile and start hello app.</span></span>
   
    ![][1]
   
    <span data-ttu-id="bf58d-157">Bir dizi kullanıcı Arabirimi sağlar bu hello uygulama değiştirir Not hello kategorileri toosubscribe seçmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="bf58d-157">Note that hello app UI provides a set of toggles that lets you choose hello categories toosubscribe to.</span></span>
2. <span data-ttu-id="bf58d-158">Bir veya daha fazla kategorileri değiştirir etkinleştirin ve ardından **abone ol**.</span><span class="sxs-lookup"><span data-stu-id="bf58d-158">Enable one or more categories toggles, then click **Subscribe**.</span></span>
   
    <span data-ttu-id="bf58d-159">Merhaba uygulama seçili hello kategoriler etiketleri dönüştürür ve seçili hello etiketleri için yeni bir cihaz kaydı hello bildirim hub'ından ister.</span><span class="sxs-lookup"><span data-stu-id="bf58d-159">hello app converts hello selected categories into tags and requests a new device registration for hello selected tags from hello notification hub.</span></span> <span data-ttu-id="bf58d-160">Merhaba kayıtlı kategorileri döndürülen ve iletişim kutusunda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="bf58d-160">hello registered categories are returned and displayed in a dialog.</span></span>
   
    ![][19]
3. <span data-ttu-id="bf58d-161">Merhaba arka yolları aşağıdaki hello birinde yeni bir bildirim gönder:</span><span class="sxs-lookup"><span data-stu-id="bf58d-161">Send a new notification from hello backend in one of hello following ways:</span></span>
   
   * <span data-ttu-id="bf58d-162">**Konsol uygulaması:** hello konsol uygulaması başlatın.</span><span class="sxs-lookup"><span data-stu-id="bf58d-162">**Console app:** start hello console app.</span></span>
   * <span data-ttu-id="bf58d-163">**Java/PHP:** uygulama/betiğini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bf58d-163">**Java/PHP:** run your app/script.</span></span>
     
     <span data-ttu-id="bf58d-164">Seçili hello kategorileri için bildirimler bildirimleri görünür.</span><span class="sxs-lookup"><span data-stu-id="bf58d-164">Notifications for hello selected categories appear as toast notifications.</span></span>
     
     ![][14]

## <a name="next-steps"></a><span data-ttu-id="bf58d-165">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bf58d-165">Next steps</span></span>
<span data-ttu-id="bf58d-166">Biz bu öğreticide öğrenilen nasıl kategoriye göre son dakika haberleri toobroadcast.</span><span class="sxs-lookup"><span data-stu-id="bf58d-166">In this tutorial we learned how toobroadcast breaking news by category.</span></span> <span data-ttu-id="bf58d-167">Diğer gelişmiş Notification Hubs senaryoları vurgulayın öğreticileri aşağıdaki hello birini Tamamlanıyor göz önünde bulundurun:</span><span class="sxs-lookup"><span data-stu-id="bf58d-167">Consider completing one of hello following tutorials that highlight other advanced Notification Hubs scenarios:</span></span>

* <span data-ttu-id="bf58d-168">[Bildirim hub'ları yerelleştirilmiş toobroadcast son dakika haberleri kullanın]</span><span class="sxs-lookup"><span data-stu-id="bf58d-168">[Use Notification Hubs toobroadcast localized breaking news]</span></span>
  
    <span data-ttu-id="bf58d-169">Haber uygulama tooenable göndermek çiğnemekten tooexpand hello bildirimleri nasıl yerelleştirilmiş öğrenin.</span><span class="sxs-lookup"><span data-stu-id="bf58d-169">Learn how tooexpand hello breaking news app tooenable sending localized notifications.</span></span>

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
