---
title: ".NET arka ucu ile aaaAzure Notification Hubs kullanıcılara bildirme"
description: "Nasıl toosend güvenli anında iletme bildirimleri ile Azure öğrenin. Merhaba .NET API kullanarak C# içinde yazılan kod örnekleri."
documentationcenter: windows
author: ysxu
manager: erikre
services: notification-hubs
editor: 
ms.assetid: 012529f2-fdbc-43c4-8634-2698164b5880
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: a366181faa81e78adf4de61435ef2790c3aa29d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-notification-hubs-notify-users-with-net-backend"></a><span data-ttu-id="90e16-104">Azure Notification Hubs kullanıcılara bildirme .NET arka ucu ile</span><span class="sxs-lookup"><span data-stu-id="90e16-104">Azure Notification Hubs Notify Users with .NET backend</span></span>
[!INCLUDE [notification-hubs-selector-aspnet-backend-notify-users](../../includes/notification-hubs-selector-aspnet-backend-notify-users.md)]

## <a name="overview"></a><span data-ttu-id="90e16-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="90e16-105">Overview</span></span>
<span data-ttu-id="90e16-106">Azure'da anında iletme bildirimi destek tooaccess kullanımı kolay, multiplatform ve Mobile Tüketiciler, kurumsal uygulamalar için anında iletme bildirimleri hello uyarlamasını büyük ölçüde basitleştirir ölçeklendirilmiş gönderim altyapısı sağlar Platform.</span><span class="sxs-lookup"><span data-stu-id="90e16-106">Push notification support in Azure enables you tooaccess an easy-to-use, multiplatform, and scaled-out push infrastructure, which greatly simplifies hello implementation of push notifications for both consumer and enterprise applications for mobile platforms.</span></span> <span data-ttu-id="90e16-107">Bu öğretici nasıl toouse Azure Notification Hubs toosend anında iletme bildirimleri tooa belirli uygulama kullanıcısı belirli bir cihazda gösterir.</span><span class="sxs-lookup"><span data-stu-id="90e16-107">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa specific app user on a specific device.</span></span> <span data-ttu-id="90e16-108">Bir ASP.NET Webapı arka kullanılan tooauthenticate istemcileri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="90e16-108">An ASP.NET WebAPI backend is used tooauthenticate clients.</span></span> <span data-ttu-id="90e16-109">Merhaba kullanılarak istemci kullanıcı kimlik doğrulaması ve etiket hello arka uç toonotification kayıt tarafından otomatik olarak eklenir.</span><span class="sxs-lookup"><span data-stu-id="90e16-109">Using hello authenticated client user, and tag will be automatically added by hello backend toonotification registration.</span></span> <span data-ttu-id="90e16-110">Bu etiket hello arka uç toogenerate bildirimleri için belirli bir kullanıcı tarafından kullanılan toosend olacaktır.</span><span class="sxs-lookup"><span data-stu-id="90e16-110">This tag will be used toosend by hello backend toogenerate notifications for a specific user.</span></span> <span data-ttu-id="90e16-111">Uygulama arka ucu kullanarak bildirimleri için kaydediliyor daha fazla bilgi için Başlangıç Kılavuzu konusuna [uygulama arka ucunuzdan kaydetme](http://msdn.microsoft.com/library/dn743807.aspx).</span><span class="sxs-lookup"><span data-stu-id="90e16-111">For more information on registering for notifications using an app backend, see hello guidance topic [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="90e16-112">Bu öğretici hello bildirim hub'ı ve hello oluşturulan proje derlemeler [Notification Hubs ile çalışmaya başlama] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="90e16-112">This tutorial builds on hello notification hub and project that you created in hello [Get started with Notification Hubs] tutorial.</span></span>

<span data-ttu-id="90e16-113">Bu öğretici aynı zamanda hello önkoşul toohello olan [güvenli anında] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="90e16-113">This tutorial is also hello prerequisite toohello [Secure Push] tutorial.</span></span> <span data-ttu-id="90e16-114">Bu öğreticide hello adımlarını tamamladıktan sonra toohello geçebilmeniz [güvenli anında] nasıl toomodify hello kod Bu öğretici toosend bir anında iletme bildirimi güvenli bir şekilde gösteren öğretici.</span><span class="sxs-lookup"><span data-stu-id="90e16-114">After you have completed hello steps in this tutorial, you can proceed toohello [Secure Push] tutorial, which shows how toomodify hello code in this tutorial toosend a push notification securely.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="90e16-115">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="90e16-115">Before you begin</span></span>
<span data-ttu-id="90e16-116">Geri bildiriminizi ciddiye alacağız.</span><span class="sxs-lookup"><span data-stu-id="90e16-116">We do take your feedback seriously.</span></span> <span data-ttu-id="90e16-117">Bu konu veya bu içeriğin geliştirilmesi için öneriler Tamamlanıyor bir güçlükle karşılaşırsanız hello sayfanın hello sonundaki görüşlerinize değer veriyoruz.</span><span class="sxs-lookup"><span data-stu-id="90e16-117">If you have any difficulties completing this topic, or recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span>

<span data-ttu-id="90e16-118">Bu öğreticinin hello tamamlanan kodu Github'da bulunabilir [burada](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span><span class="sxs-lookup"><span data-stu-id="90e16-118">hello completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/NotifyUsers).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="90e16-119">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="90e16-119">Prerequisites</span></span>
<span data-ttu-id="90e16-120">Bu öğretici başlamadan önce zaten bu Mobile Services öğreticileri tamamlamış olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="90e16-120">Before you start this tutorial, you must have already completed these Mobile Services tutorials:</span></span>

* <span data-ttu-id="90e16-121">[Notification Hubs ile çalışmaya başlama]</span><span class="sxs-lookup"><span data-stu-id="90e16-121">[Get started with Notification Hubs]</span></span><br/><span data-ttu-id="90e16-122">Merhaba uygulama adı ayrılmaya bildirim hub'ınızı oluşturması ve Bu öğreticide tooreceive bildirimleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="90e16-122">You create your notification hub and reserve hello app name and register tooreceive notifications in this tutorial.</span></span> <span data-ttu-id="90e16-123">Bu öğreticide adımları önceden tamamlamış varsayar.</span><span class="sxs-lookup"><span data-stu-id="90e16-123">This tutorial assumes you have already completed these steps.</span></span> <span data-ttu-id="90e16-124">Aksi durumda, lütfen hello adımları [bildirim hub'ları (Windows mağazası) ile çalışmaya başlama](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); özellikle, hello bölümleri [hello Windows mağazası için uygulamanızı kaydetme](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) ve [Yapılandır Bildirim Hub'ınızı](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span><span class="sxs-lookup"><span data-stu-id="90e16-124">If not, please follow hello steps in [Getting Started with Notification Hubs (Windows Store)](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md); specifically, hello sections [Register your app for hello Windows Store](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#register-your-app-for-the-windows-store) and [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="90e16-125">Özellikle, hello girdiğinizden emin olun **paket SID'si** ve **gizli** hello portalında hello değerleri **yapılandırma** bildirim hub'ınız için sekmesi.</span><span class="sxs-lookup"><span data-stu-id="90e16-125">In particular, make sure that you have entered hello **Package SID** and **Client Secret** values in hello portal, in hello **Configure** tab for your notification hub.</span></span> <span data-ttu-id="90e16-126">Bu yapılandırma yordamı hello bölümünde açıklanan [bildirim hub'ınızı yapılandırma](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span><span class="sxs-lookup"><span data-stu-id="90e16-126">This configuration procedure is described in hello section [Configure your Notification Hub](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md#configure-your-notification-hub).</span></span> <span data-ttu-id="90e16-127">Bu önemli bir adımdır: hello portal hello kimlik bilgisi belirtilen hello uygulama adı için seçtiğiniz eşleşmiyorsa, hello anında iletme bildirimi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="90e16-127">This is an important step: if hello credentials on hello portal do not match those specified for hello app name you choose, hello push notification will not succeed.</span></span>

> [!NOTE]
> <span data-ttu-id="90e16-128">Merhaba, arka uç hizmeti olarak Azure App Service'de Mobile Apps kullanıyorsanız, bkz: [Mobile Apps sürüm](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) Bu öğreticinin.</span><span class="sxs-lookup"><span data-stu-id="90e16-128">If you are using Mobile Apps in Azure App Service as your backend service, see hello [Mobile Apps version](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md) of this tutorial.</span></span>
> 
> 

&nbsp;

[!INCLUDE [notification-hubs-aspnet-backend-notifyusers](../../includes/notification-hubs-aspnet-backend-notifyusers.md)]

## <a name="update-hello-code-for-hello-client-project"></a><span data-ttu-id="90e16-129">Merhaba istemci projesi için Hello kodunu güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="90e16-129">Update hello code for hello client project</span></span>
<span data-ttu-id="90e16-130">Bu bölümde, Merhaba tamamlandı hello projesindeki hello kod güncelleştirme [Notification Hubs ile çalışmaya başlama] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="90e16-130">In this section, you update hello code in hello project you completed for hello [Get started with Notification Hubs] tutorial.</span></span> <span data-ttu-id="90e16-131">Merhaba zaten hello deposuyla ilişkili ve gerekir bildirim hub'ınız için yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="90e16-131">hello should already be associated with hello store and configured for your notification hub.</span></span> <span data-ttu-id="90e16-132">Bu bölümde, kod toocall hello yeni Webapı arka ekleyin ve kaydetme ve bildirimleri göndermek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="90e16-132">In this section, you will add code toocall hello new WebAPI backend and use it for registering and sending notifications.</span></span>

1. <span data-ttu-id="90e16-133">Merhaba oluşturduğunuz hello hello çözümü Visual Studio'da açın [Notification Hubs ile çalışmaya başlama] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="90e16-133">In Visual Studio, open hello hello solution you created for hello [Get started with Notification Hubs] tutorial.</span></span>
2. <span data-ttu-id="90e16-134">Çözüm Gezgini'nde hello sağ **(Windows 8.1)** proje ve ardından **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="90e16-134">In Solution Explorer, right-click hello **(Windows 8.1)** project and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="90e16-135">Merhaba sol taraftaki tıklatın **çevrimiçi**.</span><span class="sxs-lookup"><span data-stu-id="90e16-135">On hello left-hand side, click **Online**.</span></span>
4. <span data-ttu-id="90e16-136">Merhaba, **arama** kutusuna **Http istemcisi**.</span><span class="sxs-lookup"><span data-stu-id="90e16-136">In hello **Search** box, type **Http Client**.</span></span>
5. <span data-ttu-id="90e16-137">Merhaba sonuçlar listesinde tıklayın **Microsoft HTTP istemci kitaplıkları**ve ardından **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="90e16-137">In hello results list, click **Microsoft HTTP Client Libraries**, and then click **Install**.</span></span> <span data-ttu-id="90e16-138">Merhaba yüklemeyi tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="90e16-138">Complete hello installation.</span></span>
6. <span data-ttu-id="90e16-139">Merhaba NuGet edilene **arama** kutusuna **Json.net**.</span><span class="sxs-lookup"><span data-stu-id="90e16-139">Back in hello NuGet **Search** box, type **Json.net**.</span></span> <span data-ttu-id="90e16-140">Merhaba yüklemek **Json.NET** paket ve ardından Kapat hello NuGet Paket Yöneticisi penceresi.</span><span class="sxs-lookup"><span data-stu-id="90e16-140">Install hello **Json.NET** package, and then close hello NuGet Package Manager window.</span></span>
7. <span data-ttu-id="90e16-141">Merhaba yukarıdaki Hello adımları yineleyin **(Windows Phone 8.1)** proje tooinstall hello **JSON.NET** hello Windows Phone projesi için NuGet paketi.</span><span class="sxs-lookup"><span data-stu-id="90e16-141">Repeat hello steps above for hello **(Windows Phone 8.1)** project tooinstall hello **JSON.NET** NuGet package for hello Windows Phone project.</span></span>
8. <span data-ttu-id="90e16-142">Çözüm Gezgini'nde, hello **(Windows 8.1)** projesi, çift **MainPage.xaml** tooopen onu hello Visual Studio düzenleyicisinde.</span><span class="sxs-lookup"><span data-stu-id="90e16-142">In Solution Explorer, in hello **(Windows 8.1)** project, double-click **MainPage.xaml** tooopen it in hello Visual Studio editor.</span></span>
9. <span data-ttu-id="90e16-143">Merhaba, **MainPage.xaml** XML kodunu değiştir hello `<Grid>` koddan hello bölümle.</span><span class="sxs-lookup"><span data-stu-id="90e16-143">In hello **MainPage.xaml** XML code, replace hello `<Grid>` section with hello following code.</span></span> <span data-ttu-id="90e16-144">Bu kod, kullanıcı hello bir kullanıcı adı ve parola textbox ile kimlik doğrulaması ekler.</span><span class="sxs-lookup"><span data-stu-id="90e16-144">This code adds a username and password textbox that hello user will authenticate with.</span></span> <span data-ttu-id="90e16-145">Ayrıca, hello bildirim iletisi ve hello bildirimi alması gereken hello kullanıcı adı etiketi için metin kutuları ekler:</span><span class="sxs-lookup"><span data-stu-id="90e16-145">It also adds textboxes for hello notification message and hello username tag that should receive hello notification:</span></span>
   
        <Grid>
            <Grid.RowDefinitions>
                <RowDefinition Height="Auto"/>
                <RowDefinition Height="*"/>
            </Grid.RowDefinitions>
   
            <TextBlock Grid.Row="0" Text="Notify Users" HorizontalAlignment="Center" FontSize="48"/>
   
            <StackPanel Grid.Row="1" VerticalAlignment="Center">
                <Grid>
                    <Grid.RowDefinitions>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                        <RowDefinition Height="Auto"/>
                    </Grid.RowDefinitions>
                    <Grid.ColumnDefinitions>
                        <ColumnDefinition></ColumnDefinition>
                        <ColumnDefinition></ColumnDefinition>
                        <ColumnDefinition></ColumnDefinition>
                    </Grid.ColumnDefinitions>
                    <TextBlock Grid.Row="0" Grid.ColumnSpan="3" Text="Username" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="UsernameTextBox" Grid.Row="1" Grid.ColumnSpan="3" Margin="20,0,20,0"/>
                    <TextBlock Grid.Row="2" Grid.ColumnSpan="3" Text="Password" FontSize="24" Margin="20,0,20,0" />
                    <PasswordBox Name="PasswordTextBox" Grid.Row="3" Grid.ColumnSpan="3" Margin="20,0,20,0"/>
   
                    <Button Grid.Row="4" Grid.ColumnSpan="3" HorizontalAlignment="Center" VerticalAlignment="Center"
                                Content="1. Login and register" Click="LoginAndRegisterClick" Margin="0,0,0,20"/>
   
                    <ToggleButton Name="toggleWNS" Grid.Row="5" Grid.Column="0" HorizontalAlignment="Right" Content="WNS" IsChecked="True" />
                    <ToggleButton Name="toggleGCM" Grid.Row="5" Grid.Column="1" HorizontalAlignment="Center" Content="GCM" />
                    <ToggleButton Name="toggleAPNS" Grid.Row="5" Grid.Column="2" HorizontalAlignment="Left" Content="APNS" />
   
                    <TextBlock Grid.Row="6" Grid.ColumnSpan="3" Text="Username Tag tooSend To" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="ToUserTagTextBox" Grid.Row="7" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <TextBlock Grid.Row="8" Grid.ColumnSpan="3" Text="Enter Notification Message" FontSize="24" Margin="20,0,20,0"/>
                    <TextBox Name="NotificationMessageTextBox" Grid.Row="9" Grid.ColumnSpan="3" Margin="20,0,20,0" TextWrapping="Wrap" />
                    <Button Grid.Row="10" Grid.ColumnSpan="3" HorizontalAlignment="Center" Content="2. Send push" Click="PushClick" Name="SendPushButton" />
                </Grid>
            </StackPanel>
        </Grid>
10. <span data-ttu-id="90e16-146">Çözüm Gezgini'nde, hello **(Windows Phone 8.1)** proje, açık **MainPage.xaml** ve Windows Phone 8.1 hello Değiştir `<Grid>` yukarıdaki aynı kodu ile bölüm.</span><span class="sxs-lookup"><span data-stu-id="90e16-146">In Solution Explorer, in hello **(Windows Phone 8.1)** project, open **MainPage.xaml** and replace hello Windows Phone 8.1 `<Grid>` section with that same code above.</span></span> <span data-ttu-id="90e16-147">Merhaba arabirimi aşağıda gösterilen benzer toowhats görünmelidir.</span><span class="sxs-lookup"><span data-stu-id="90e16-147">hello interface should look similar toowhats shown below.</span></span>
    
    ![][13]
11. <span data-ttu-id="90e16-148">Çözüm Gezgini'nde hello açın **MainPage.xaml.cs** hello dosyası **(Windows 8.1)** ve **(Windows Phone 8.1)** projeleri.</span><span class="sxs-lookup"><span data-stu-id="90e16-148">In Solution Explorer, open hello **MainPage.xaml.cs** file for hello **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span> <span data-ttu-id="90e16-149">Merhaba aşağıdakileri ekleyin `using` deyimleri hello üst dosyalar:</span><span class="sxs-lookup"><span data-stu-id="90e16-149">Add hello following `using` statements at hello top of both files:</span></span>
    
        using System.Net.Http;
        using Windows.Storage;
        using System.Net.Http.Headers;
        using Windows.Networking.PushNotifications;
        using Windows.UI.Popups;
        using System.Threading.Tasks;
12. <span data-ttu-id="90e16-150">İçinde **MainPage.xaml.cs** hello için **(Windows 8.1)** ve **(Windows Phone 8.1)** projeler eklemek üye toohello aşağıdaki hello `MainPage` sınıfı.</span><span class="sxs-lookup"><span data-stu-id="90e16-150">In **MainPage.xaml.cs** for hello **(Windows 8.1)** and **(Windows Phone 8.1)** projects, add hello following member toohello `MainPage` class.</span></span> <span data-ttu-id="90e16-151">Emin tooreplace olması `<Enter Your Backend Endpoint>` hello ile gerçek arka uç noktanızı elde daha önce.</span><span class="sxs-lookup"><span data-stu-id="90e16-151">Be sure tooreplace `<Enter Your Backend Endpoint>` with hello your actual backend endpoint obtained previously.</span></span> <span data-ttu-id="90e16-152">Örneğin, `http://mybackend.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="90e16-152">For example, `http://mybackend.azurewebsites.net`.</span></span>
    
        private static string BACKEND_ENDPOINT = "<Enter Your Backend Endpoint>";
13. <span data-ttu-id="90e16-153">Merhaba toohello MainPage sınıfında aşağıdaki kodu ekleyin **MainPage.xaml.cs** hello için **(Windows 8.1)** ve **(Windows Phone 8.1)** projeleri.</span><span class="sxs-lookup"><span data-stu-id="90e16-153">Add hello code below toohello MainPage class in **MainPage.xaml.cs** for hello **(Windows 8.1)** and **(Windows Phone 8.1)** projects.</span></span>
    
    <span data-ttu-id="90e16-154">Merhaba `PushClick` yöntemdir hello hello için işleyicisi'ı tıklatın **Gönder anında** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="90e16-154">hello `PushClick` method is hello click handler for hello **Send Push** button.</span></span> <span data-ttu-id="90e16-155">Merhaba eşleşen bir kullanıcı adı etiketi ile cihazları hello arka uç tootrigger bildirim tooall çağırır `to_tag` parametresi.</span><span class="sxs-lookup"><span data-stu-id="90e16-155">It calls hello backend tootrigger a notification tooall devices with a username tag that matches hello `to_tag` parameter.</span></span> <span data-ttu-id="90e16-156">Merhaba bildirim iletisi hello istek gövdesinde JSON içeriği olarak gönderilir.</span><span class="sxs-lookup"><span data-stu-id="90e16-156">hello notification message is sent as JSON content in hello request body.</span></span>
    
    <span data-ttu-id="90e16-157">Merhaba `LoginAndRegisterClick` yöntemdir hello hello için işleyicisi'ı tıklatın **oturum açma ve kaydetme** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="90e16-157">hello `LoginAndRegisterClick` method is hello click handler for hello **Log in and register** button.</span></span> <span data-ttu-id="90e16-158">Merhaba basic depolar (Bu, kimlik doğrulama şemasını kullanan herhangi bir belirteci temsil ettiğini unutmayın), Yerel Depodaki kimlik doğrulama belirteci sonra kullanır `RegisterClient` tooregister hello arka uç kullanarak bildirimleri için.</span><span class="sxs-lookup"><span data-stu-id="90e16-158">It stores hello basic authentication token in local storage (note that this represents any token your authentication scheme uses), then uses `RegisterClient` tooregister for notifications using hello backend.</span></span>

        private async void PushClick(object sender, RoutedEventArgs e)
        {
            if (toggleWNS.IsChecked.Value)
            {
                await sendPush("wns", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);
            }
            if (toggleGCM.IsChecked.Value)
            {
                await sendPush("gcm", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);
            }
            if (toggleAPNS.IsChecked.Value)
            {
                await sendPush("apns", ToUserTagTextBox.Text, this.NotificationMessageTextBox.Text);

            }
        }

        private async Task sendPush(string pns, string userTag, string message)
        {
            var POST_URL = BACKEND_ENDPOINT + "/api/notifications?pns=" +
                pns + "&to_tag=" + userTag;

            using (var httpClient = new HttpClient())
            {
                var settings = ApplicationData.Current.LocalSettings.Values;
                httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);

                try
                {
                    await httpClient.PostAsync(POST_URL, new StringContent("\"" + message + "\"",
                        System.Text.Encoding.UTF8, "application/json"));
                }
                catch (Exception ex)
                {
                    MessageDialog alert = new MessageDialog(ex.Message, "Failed toosend " + pns + " message");
                    alert.ShowAsync();
                }
            }
        }

        private async void LoginAndRegisterClick(object sender, RoutedEventArgs e)
        {
            SetAuthenticationTokenInLocalStorage();

            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();

            // hello "username:<user name>" tag gets automatically added by hello message handler in hello backend.
            // hello tag passed here can be whatever other tags you may want toouse.
            try
            {
                // hello device handle used will be different depending on hello device and PNS. 
                // Windows devices use hello channel uri as hello PNS handle.
                await new RegisterClient(BACKEND_ENDPOINT).RegisterAsync(channel.Uri, new string[] { "myTag" });

                var dialog = new MessageDialog("Registered as: " + UsernameTextBox.Text);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
                SendPushButton.IsEnabled = true;
            }
            catch (Exception ex)
            {
                MessageDialog alert = new MessageDialog(ex.Message, "Failed tooregister with RegisterClient");
                alert.ShowAsync();
            }
        }

        private void SetAuthenticationTokenInLocalStorage()
        {
            string username = UsernameTextBox.Text;
            string password = PasswordTextBox.Password;

            var token = Convert.ToBase64String(System.Text.Encoding.UTF8.GetBytes(username + ":" + password));
            ApplicationData.Current.LocalSettings.Values["AuthenticationToken"] = token;
        }



1. <span data-ttu-id="90e16-159">Çözüm Gezgini'nde, hello altında **paylaşılan** proje, açık hello **App.xaml.cs** dosya.</span><span class="sxs-lookup"><span data-stu-id="90e16-159">In Solution Explorer, under hello **Shared** project, open hello **App.xaml.cs** file.</span></span> <span data-ttu-id="90e16-160">Merhaba görüşmesi çok bulma`InitNotificationsAsync()` hello içinde `OnLaunched()` olay işleyicisi.</span><span class="sxs-lookup"><span data-stu-id="90e16-160">Find hello call too`InitNotificationsAsync()` in hello `OnLaunched()` event handler.</span></span> <span data-ttu-id="90e16-161">Out yorum yapmak veya hello çağrısı çok silme`InitNotificationsAsync()`.</span><span class="sxs-lookup"><span data-stu-id="90e16-161">Comment out or delete hello call too`InitNotificationsAsync()`.</span></span> <span data-ttu-id="90e16-162">yukarıda eklediğiniz hello düğme işleyicisi bildirim kayıtlar başlatacak.</span><span class="sxs-lookup"><span data-stu-id="90e16-162">hello button handler added above will initialize notification registrations.</span></span>

        protected override void OnLaunched(LaunchActivatedEventArgs e)
        {
            //InitNotificationsAsync();


1. <span data-ttu-id="90e16-163">Çözüm Gezgini'nde hello sağ **paylaşılan** proje ve ardından **Ekle**ve ardından **sınıfı**.</span><span class="sxs-lookup"><span data-stu-id="90e16-163">In Solution Explorer, right-click hello **Shared** project, then click **Add**, and then click **Class**.</span></span> <span data-ttu-id="90e16-164">Ad hello sınıfı **RegisterClient.cs**, ardından **Tamam** toogenerate hello sınıfı.</span><span class="sxs-lookup"><span data-stu-id="90e16-164">Name hello class **RegisterClient.cs**, then click **OK** toogenerate hello class.</span></span>
   
   <span data-ttu-id="90e16-165">Bu sınıf, anında iletme bildirimleri için sipariş tooregister hello REST çağrılarını gerekli toocontact hello uygulama arka ucu, kaydırılır.</span><span class="sxs-lookup"><span data-stu-id="90e16-165">This class will wrap hello REST calls required toocontact hello app backend, in order tooregister for push notifications.</span></span> <span data-ttu-id="90e16-166">Merhaba da yerel olarak depoladığı *registrationIds* bildirim hub'ı ayrıntılı biçimde açıklandığı gibi hello tarafından oluşturulan [uygulama arka ucunuzdan kaydetme](http://msdn.microsoft.com/library/dn743807.aspx).</span><span class="sxs-lookup"><span data-stu-id="90e16-166">It also locally stores hello *registrationIds* created by hello Notification Hub as detailed in [Registering from your app backend](http://msdn.microsoft.com/library/dn743807.aspx).</span></span> <span data-ttu-id="90e16-167">Merhaba tıklattığınızda yerel depolamada depolanan bir yetki belirteci kullandığına dikkat edin **oturum açma ve kaydetme** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="90e16-167">Note that it uses an authorization token stored in local storage when you click hello **Log in and register** button.</span></span>
2. <span data-ttu-id="90e16-168">Merhaba aşağıdakileri ekleyin `using` deyimleri hello dosyanın üst kısmındaki hello RegisterClient.cs:</span><span class="sxs-lookup"><span data-stu-id="90e16-168">Add hello following `using` statements at hello top of hello RegisterClient.cs file:</span></span>
   
       using Windows.Storage;
       using System.Net;
       using System.Net.Http;
       using System.Net.Http.Headers;
       using Newtonsoft.Json;
       using System.Threading.Tasks;
       using System.Linq;
3. <span data-ttu-id="90e16-169">Merhaba içindeki kodu aşağıdaki hello eklemek `RegisterClient` sınıf tanımının.</span><span class="sxs-lookup"><span data-stu-id="90e16-169">Add hello following code inside hello `RegisterClient` class definition.</span></span>
   
       private string POST_URL;
   
       private class DeviceRegistration
       {
           public string Platform { get; set; }
           public string Handle { get; set; }
           public string[] Tags { get; set; }
       }
   
       public RegisterClient(string backendEndpoint)
       {
           POST_URL = backendEndpoint + "/api/register";
       }
   
       public async Task RegisterAsync(string handle, IEnumerable<string> tags)
       {
           var regId = await RetrieveRegistrationIdOrRequestNewOneAsync();
   
           var deviceRegistration = new DeviceRegistration
           {
               Platform = "wns",
               Handle = handle,
               Tags = tags.ToArray<string>()
           };
   
           var statusCode = await UpdateRegistrationAsync(regId, deviceRegistration);
   
           if (statusCode == HttpStatusCode.Gone)
           {
               // regId is expired, deleting from local storage & recreating
               var settings = ApplicationData.Current.LocalSettings.Values;
               settings.Remove("__NHRegistrationId");
               regId = await RetrieveRegistrationIdOrRequestNewOneAsync();
               statusCode = await UpdateRegistrationAsync(regId, deviceRegistration);
           }
   
           if (statusCode != HttpStatusCode.Accepted)
           {
               // log or throw
               throw new System.Net.WebException(statusCode.ToString());
           }
       }
   
       private async Task<HttpStatusCode> UpdateRegistrationAsync(string regId, DeviceRegistration deviceRegistration)
       {
           using (var httpClient = new HttpClient())
           {
               var settings = ApplicationData.Current.LocalSettings.Values;
               httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string) settings["AuthenticationToken"]);
   
               var putUri = POST_URL + "/" + regId;
   
               string json = JsonConvert.SerializeObject(deviceRegistration);
                               var response = await httpClient.PutAsync(putUri, new StringContent(json, Encoding.UTF8, "application/json"));
               return response.StatusCode;
           }
       }
   
       private async Task<string> RetrieveRegistrationIdOrRequestNewOneAsync()
       {
           var settings = ApplicationData.Current.LocalSettings.Values;
           if (!settings.ContainsKey("__NHRegistrationId"))
           {
               using (var httpClient = new HttpClient())
               {
                   httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Basic", (string)settings["AuthenticationToken"]);
   
                   var response = await httpClient.PostAsync(POST_URL, new StringContent(""));
                   if (response.IsSuccessStatusCode)
                   {
                       string regId = await response.Content.ReadAsStringAsync();
                       regId = regId.Substring(1, regId.Length - 2);
                       settings.Add("__NHRegistrationId", regId);
                   }
                   else
                   {
                       throw new System.Net.WebException(response.StatusCode.ToString());
                   }
               }
           }
           return (string)settings["__NHRegistrationId"];
   
       }
4. <span data-ttu-id="90e16-170">Yaptığınız tüm değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="90e16-170">Save all your changes.</span></span>

## <a name="testing-hello-application"></a><span data-ttu-id="90e16-171">Merhaba uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="90e16-171">Testing hello Application</span></span>
1. <span data-ttu-id="90e16-172">Windows 8.1 ve Windows Phone 8.1 Merhaba uygulaması başlatın.</span><span class="sxs-lookup"><span data-stu-id="90e16-172">Launch hello application on both Windows 8.1 and Windows Phone 8.1.</span></span> <span data-ttu-id="90e16-173">Windows Phone 8.1 için hello öykünücü veya gerçek bir cihaza hello örneği çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90e16-173">For Windows Phone 8.1 you can run hello instance in hello emulator or an actual device.</span></span>
2. <span data-ttu-id="90e16-174">Merhaba uygulama Hello Windows 8.1 örneğinde girin bir **kullanıcıadı** ve **parola** ekranda hello aşağıda gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="90e16-174">In hello Windows 8.1 instance of hello app, enter a **Username** and **Password** as shown in hello screen below.</span></span> <span data-ttu-id="90e16-175">Merhaba kullanıcı adı ve parola Windows Phone üzerinde farklı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="90e16-175">It should differ from hello user name and password you enter on Windows Phone.</span></span>
3. <span data-ttu-id="90e16-176">Tıklatın **oturum açma ve kaydetme** ve bir iletişim kutusu gösterir oturum olduğunu doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="90e16-176">Click **Log in and register** and verify a dialog shows that you have logged in.</span></span> <span data-ttu-id="90e16-177">Bu da hello etkinleştirir **Gönder anında** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="90e16-177">This will also enable hello **Send Push** button.</span></span>
   
    ![][14]
4. <span data-ttu-id="90e16-178">Merhaba Windows Phone 8.1 örneği, bir kullanıcı adı dizesi hem hello girin **kullanıcıadı** ve **parola** alanları ardından **oturum açma ve kaydetme**.</span><span class="sxs-lookup"><span data-stu-id="90e16-178">On hello Windows Phone 8.1 instance, enter a user name string in both hello **Username** and **Password** fields then click **Login and register**.</span></span>
5. <span data-ttu-id="90e16-179">Merhaba sonra **alıcı kullanıcı adı etiketi** alanında, Windows 8.1 kayıtlı hello kullanıcı adı girin.</span><span class="sxs-lookup"><span data-stu-id="90e16-179">Then in hello **Recipient Username Tag** field, enter hello user name registered on Windows 8.1.</span></span> <span data-ttu-id="90e16-180">Bir bildirim iletisi girin ve tıklayın **Gönder anında**.</span><span class="sxs-lookup"><span data-stu-id="90e16-180">Enter a notification message and click **Send Push**.</span></span>
   
    ![][16]
6. <span data-ttu-id="90e16-181">Merhaba eşleşen kullanıcı adı etiketi ile kaydettiğiniz hello cihazların Merhaba bildirim iletisi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="90e16-181">Only hello devices that have registered with hello matching username tag receive hello notification message.</span></span>
   
    ![][15]

## <a name="next-steps"></a><span data-ttu-id="90e16-182">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="90e16-182">Next Steps</span></span>
* <span data-ttu-id="90e16-183">Kullanıcılarınızı ilgi alanı gruplarına göre toosegment istiyorsanız, bkz: [son dakika haberleri Notification Hubs kullanma toosend].</span><span class="sxs-lookup"><span data-stu-id="90e16-183">If you want toosegment your users by interest groups, see [Use Notification Hubs toosend breaking news].</span></span>
* <span data-ttu-id="90e16-184">toouse bildirim hub'ları, toolearn nasıl hakkında daha fazla bilgi görmek [Notification Hubs Kılavuzu].</span><span class="sxs-lookup"><span data-stu-id="90e16-184">toolearn more about how toouse Notification Hubs, see [Notification Hubs Guidance].</span></span>

[9]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push9.png
[10]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push10.png
[11]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push11.png
[12]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-secure-push12.png
[13]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-ui.png
[14]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-windows-instance-username.png
[15]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-notification-received.png
[16]: ./media/notification-hubs-aspnet-backend-windows-dotnet-notify-users/notification-hubs-wp-send-message.png



<!-- URLs. -->
[Notification Hubs ile çalışmaya başlama]: notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md
[güvenli anında]: notification-hubs-aspnet-backend-windows-dotnet-wns-secure-push-notification.md
[son dakika haberleri Notification Hubs kullanma toosend]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md
[Notification Hubs Kılavuzu]: http://msdn.microsoft.com/library/jj927170.aspx
