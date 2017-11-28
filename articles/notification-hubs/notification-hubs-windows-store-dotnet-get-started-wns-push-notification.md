---
title: "aaaGet Azure uygulamaları için Notification Hubs Windows Evrensel Platform ile başlatılan | Microsoft Docs"
description: "Bu öğreticide, bilgi nasıl toouse Azure Notification Hubs toopush bildirimleri tooa Evrensel Windows Platform uygulaması."
services: notification-hubs
documentationcenter: windows
author: ysxu
manager: erikre
editor: erikre
ms.assetid: cf307cf3-8c58-4628-9c63-8751e6a0ef43
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 11056842d205522ed493dc61c76ecf78ebb5a363
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-notification-hubs-for-windows-universal-platform-apps"></a><span data-ttu-id="84f38-103">Windows Evrensel Platform Uygulamaları için Notification Hubs'ı kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="84f38-103">Getting started with Notification Hubs for Windows Universal Platform Apps</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="84f38-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="84f38-104">Overview</span></span>
<span data-ttu-id="84f38-105">Bu öğretici nasıl toouse Azure Notification Hubs toosend anında bildirimler tooa Evrensel Windows Platformu (UWP) uygulamasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="84f38-105">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Universal Windows Platform (UWP) app.</span></span>

<span data-ttu-id="84f38-106">Bu öğreticide, hello Windows anında bildirim Hizmeti'ni (WNS) kullanarak anında iletme bildirimleri alan boş bir Windows mağazası uygulaması oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="84f38-106">In this tutorial, you create a blank Windows Store app that receives push notifications by using hello Windows Push Notification Service (WNS).</span></span> <span data-ttu-id="84f38-107">Mümkün toouse olacak tamamladığınızda, bildirim hub'ı toobroadcast uygulamanızı çalıştıran bildirimleri tooall hello cihazlar iletin.</span><span class="sxs-lookup"><span data-stu-id="84f38-107">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="84f38-108">Başlamadan önce</span><span class="sxs-lookup"><span data-stu-id="84f38-108">Before you begin</span></span>
[!INCLUDE [notification-hubs-hero-slug](../../includes/notification-hubs-hero-slug.md)]

<span data-ttu-id="84f38-109">Bu öğreticinin hello tamamlanan kodu Github'da bulunabilir [burada](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).</span><span class="sxs-lookup"><span data-stu-id="84f38-109">hello completed code for this tutorial can be found on GitHub [here](https://github.com/Azure/azure-notificationhubs-samples/tree/master/dotnet/GetStartedWindowsUniversal).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84f38-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="84f38-110">Prerequisites</span></span>
<span data-ttu-id="84f38-111">Bu öğretici hello aşağıdakileri gerektirir:</span><span class="sxs-lookup"><span data-stu-id="84f38-111">This tutorial requires hello following:</span></span>

* <span data-ttu-id="84f38-112">[Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) veya üstü</span><span class="sxs-lookup"><span data-stu-id="84f38-112">[Microsoft Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs) or later</span></span>
* [<span data-ttu-id="84f38-113">Evrensel Windows Uygulama Geliştirme Araçları'nın yüklü olması</span><span class="sxs-lookup"><span data-stu-id="84f38-113">Universal Windows App Development Tools installed</span></span>](https://msdn.microsoft.com/windows/uwp/get-started/get-set-up)
* <span data-ttu-id="84f38-114">Etkin bir Azure hesabı</span><span class="sxs-lookup"><span data-stu-id="84f38-114">An active Azure account</span></span> <br/><span data-ttu-id="84f38-115">Hesabınız yoksa yalnızca birkaç dakika içinde ücretsiz bir deneme sürümü hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84f38-115">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="84f38-116">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="84f38-116">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-store-dotnet-get-started%2F).</span></span>
* <span data-ttu-id="84f38-117">Etkin bir Windows Mağazası hesabı</span><span class="sxs-lookup"><span data-stu-id="84f38-117">An active Windows Store account</span></span>

<span data-ttu-id="84f38-118">Bu öğreticinin tamamlanması Windows Evrensel Platform uygulamalarına ilişkin diğer tüm Notification Hubs öğreticileri için önkoşuldur.</span><span class="sxs-lookup"><span data-stu-id="84f38-118">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Universal Platform apps.</span></span>

## <a name="register-your-app-for-hello-windows-store"></a><span data-ttu-id="84f38-119">Merhaba Windows mağazası için uygulamanızı kaydetme</span><span class="sxs-lookup"><span data-stu-id="84f38-119">Register your app for hello Windows Store</span></span>
<span data-ttu-id="84f38-120">toosend anında iletme bildirimleri tooUWP uygulamalar, uygulama toohello Windows mağazası ilişkilendirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="84f38-120">toosend push notifications tooUWP apps, you must associate your app toohello Windows Store.</span></span> <span data-ttu-id="84f38-121">Ardından, bildirim hub'ı toointegrate WNS ile yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="84f38-121">You must then configure your notification hub toointegrate with WNS.</span></span>

1. <span data-ttu-id="84f38-122">Uygulamanızı zaten kaydolmadıysanız toohello gidin [Windows Geliştirme Merkezi](https://dev.windows.com/overview), Microsoft hesabınızla oturum açın ve ardından **yeni uygulama oluştur**.</span><span class="sxs-lookup"><span data-stu-id="84f38-122">If you have not already registered your app, navigate toohello [Windows Dev Center](https://dev.windows.com/overview), sign in with your Microsoft account, and then click **Create a new app**.</span></span>

2. <span data-ttu-id="84f38-123">Uygulamanız için bir ad yazın ve **Uygulama adını ayır**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="84f38-123">Type a name for your app and click **Reserve app name**.</span></span> <span data-ttu-id="84f38-124">Bu, uygulamanız için yeni bir Windows Mağazası kaydı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="84f38-124">This creates a new Windows Store registration for your app.</span></span>

3. <span data-ttu-id="84f38-125">Windows Evrensel hello kullanarak Visual Studio'da yeni bir Visual C# mağaza uygulamaları projesi oluşturma **boş uygulama** şablonu ve tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="84f38-125">In Visual Studio, create a new Visual C# Store Apps project by using hello Windows Universal **Blank App** template and click **OK**.</span></span>

4. <span data-ttu-id="84f38-126">Merhaba hedef ve minimum platform sürümleri için Hello Varsayılanları kabul edin.</span><span class="sxs-lookup"><span data-stu-id="84f38-126">Accept hello defaults for hello target and minimum platform versions.</span></span>

5. <span data-ttu-id="84f38-127">Çözüm Gezgini'nde, hello Windows mağazası uygulama projesine sağ tıklayın, tıklatın **deposu**ve ardından **uygulamayı hello mağaza ile ilişkilendir...** . hello **uygulamanızı hello Windows mağazası ile ilişkilendirin** Sihirbazı görünür.</span><span class="sxs-lookup"><span data-stu-id="84f38-127">In Solution Explorer, right-click hello Windows Store app project, click **Store**, and then click **Associate App with hello Store...**. hello **Associate Your App with hello Windows Store** wizard appears.</span></span>

6. <span data-ttu-id="84f38-128">Başlangıç Sihirbazı'nda, Microsoft hesabınızla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="84f38-128">In hello wizard, sign in with your Microsoft account.</span></span>

7. <span data-ttu-id="84f38-129">2. adımda kaydettiğiniz hello uygulama tıklatın, **sonraki**ve ardından **ilişkilendirmek**.</span><span class="sxs-lookup"><span data-stu-id="84f38-129">Click hello app that you registered in step 2, click **Next**, and then click **Associate**.</span></span> <span data-ttu-id="84f38-130">Bu gerekli hello Windows mağazası kayıt bilgilerini toohello uygulama bildirimi ekler.</span><span class="sxs-lookup"><span data-stu-id="84f38-130">This adds hello required Windows Store registration information toohello application manifest.</span></span>

8. <span data-ttu-id="84f38-131">Merhaba üzerinde geri [Windows Geliştirme Merkezi](http://dev.windows.com/overview) sayfasında yeni uygulamanız için **Hizmetleri**, tıklatın **anında iletme bildirimleri**ve ardından **WNS/MPNS**.</span><span class="sxs-lookup"><span data-stu-id="84f38-131">Back on hello [Windows Dev Center](http://dev.windows.com/overview) page for your new app, click **Services**, click **Push notifications**, and then click **WNS/MPNS**.</span></span>

9. <span data-ttu-id="84f38-132">**Yeni Bildirim**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="84f38-132">Click **New Notification**.</span></span>

10. <span data-ttu-id="84f38-133">**Boş (Bildirim)** şablonuna ve sonra **Tamam**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="84f38-133">Click **Blank (Toast)** template and then click **OK**.</span></span>

11. <span data-ttu-id="84f38-134">Bildirim için bir **Ad** ve Görsel **Bağlam** iletisi girin.</span><span class="sxs-lookup"><span data-stu-id="84f38-134">Enter a notification **Name** and Visual **Context** message.</span></span> <span data-ttu-id="84f38-135">Ardından **Taslak olarak kaydet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="84f38-135">Then click **Save as draft**.</span></span>

12. <span data-ttu-id="84f38-136">Toohello gidin [uygulama kayıt portalı](http://apps.dev.microsoft.com) ve oturum açın.</span><span class="sxs-lookup"><span data-stu-id="84f38-136">Navigate toohello [Application Registration Portal](http://apps.dev.microsoft.com) and log in.</span></span>

13. <span data-ttu-id="84f38-137">Uygulamanızın adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="84f38-137">Click on your application name.</span></span> <span data-ttu-id="84f38-138">Merhaba Not **uygulama gizli anahtarı** parola ve hello **paket güvenlik tanımlayıcısı (SID)** hello bulunan **Windows mağazası** platforma ayarlar.</span><span class="sxs-lookup"><span data-stu-id="84f38-138">Make a note of hello **Application Secret** password and hello **Package security identifier (SID)** located in hello **Windows Store** platform settings.</span></span>

     > [AZURE.WARNING]
    <span data-ttu-id="84f38-139">Merhaba uygulama gizli anahtarı ve paket SID'si önemli güvenlik kimlik bilgileridir.</span><span class="sxs-lookup"><span data-stu-id="84f38-139">hello application secret and package SID are important security credentials.</span></span> <span data-ttu-id="84f38-140">Bu değerleri kimseyle paylaşmayın veya uygulamanızla birlikte dağıtmayın.</span><span class="sxs-lookup"><span data-stu-id="84f38-140">Do not share these values with anyone or distribute them with your app.</span></span>

## <a name="configure-your-notification-hub"></a><span data-ttu-id="84f38-141">Bildirim hub'ınızı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="84f38-141">Configure your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p><span data-ttu-id="84f38-142">Select hello <b>Bildirim Hizmetleri</b> seçeneği ve hello <b>Windows (WNS)</b> seçeneği.</span><span class="sxs-lookup"><span data-stu-id="84f38-142">Select hello <b>Notification Services</b> option and hello <b>Windows (WNS)</b> option.</span></span> <span data-ttu-id="84f38-143">Merhaba enter <b>uygulama gizli anahtarı</b> hello Parolada <b>güvenlik anahtarı</b> alan.</span><span class="sxs-lookup"><span data-stu-id="84f38-143">Then enter hello <b>Application secret</b> password in hello <b>Security Key</b> field.</span></span> <span data-ttu-id="84f38-144">Girin, <b>paket SID'si</b> WNS hello önceki bölümdeki alınan ve ardından değeri <b>kaydetmek</b>.</span><span class="sxs-lookup"><span data-stu-id="84f38-144">Enter your <b>Package SID</b> value that you obtained from WNS in hello previous section, and then click <b>Save</b>.</span></span></p>
</li>
</ol>

&emsp;&emsp;![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-configure-wns.png)

<span data-ttu-id="84f38-145">Bildirim hub'ınız şimdi WNS ile yapılandırılmış toowork olan ve hello bağlantı dizeleri tooregister uygulamanızı çalıştırdıktan ve bildirimleri göndermek.</span><span class="sxs-lookup"><span data-stu-id="84f38-145">Your notification hub is now configured toowork with WNS, and you have hello connection strings tooregister your app and send notifications.</span></span>

## <a name="connect-your-app-toohello-notification-hub"></a><span data-ttu-id="84f38-146">Uygulama toohello bildirim hub'ınıza bağlanın</span><span class="sxs-lookup"><span data-stu-id="84f38-146">Connect your app toohello notification hub</span></span>
1. <span data-ttu-id="84f38-147">Visual Studio'da hello çözüme sağ tıklayın ve ardından **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="84f38-147">In Visual Studio, right-click hello solution, and then click **Manage NuGet Packages**.</span></span>
   
    <span data-ttu-id="84f38-148">Bu hello görüntüler **NuGet paketlerini Yönet** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="84f38-148">This displays hello **Manage NuGet Packages** dialog box.</span></span>
2. <span data-ttu-id="84f38-149">Arama `WindowsAzure.Messaging.Managed` tıklatıp **yükleme**ve hello kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="84f38-149">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and accept hello terms of use.</span></span>
   
    ![][20]
   
    <span data-ttu-id="84f38-150">Bu indirir, yükler ve bir başvuru toohello Azure Mesajlaşma kitaplığına için Windows hello kullanarak ekler <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet paketini</a>.</span><span class="sxs-lookup"><span data-stu-id="84f38-150">This downloads, installs, and adds a reference toohello Azure Messaging library for Windows by using hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span></span>
3. <span data-ttu-id="84f38-151">Merhaba App.xaml.cs dosyasını açın ve hello aşağıdakileri ekleyin `using` deyimleri.</span><span class="sxs-lookup"><span data-stu-id="84f38-151">Open hello App.xaml.cs project file and add hello following `using` statements.</span></span> 
   
        using Windows.Networking.PushNotifications;
        using Microsoft.WindowsAzure.Messaging;
        using Windows.UI.Popups;
4. <span data-ttu-id="84f38-152">Ayrıca App.xaml.cs dosyasında hello aşağıdakileri ekleyin **Initnotificationsasync** yöntemi tanımı toohello **uygulama** sınıfı:</span><span class="sxs-lookup"><span data-stu-id="84f38-152">Also in App.xaml.cs, add hello following **InitNotificationsAsync** method definition toohello **App** class:</span></span>
   
        private async void InitNotificationsAsync()
        {
            var channel = await PushNotificationChannelManager.CreatePushNotificationChannelForApplicationAsync();
   
            var hub = new NotificationHub("< your hub name>", "<Your DefaultListenSharedAccessSignature connection string>");
            var result = await hub.RegisterNativeAsync(channel.Uri);
   
            // Displays hello registration ID so you know it was successful
            if (result.RegistrationId != null)
            {
                var dialog = new MessageDialog("Registration successful: " + result.RegistrationId);
                dialog.Commands.Add(new UICommand("OK"));
                await dialog.ShowAsync();
            }
   
        }
   
    <span data-ttu-id="84f38-153">Bu kod, WNS'den hello uygulama hello kanal URI'sini alır ve ardından bu kanal URI'sini bildirim hub'ınıza kaydeder.</span><span class="sxs-lookup"><span data-stu-id="84f38-153">This code retrieves hello channel URI for hello app from WNS, and then registers that channel URI with your notification hub.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="84f38-154">"Hub name" yer tutucusunu hello Azure Portal görünür hello bildirim hub'hello adı ile Merhaba emin tooreplace olun.</span><span class="sxs-lookup"><span data-stu-id="84f38-154">Make sure tooreplace hello "your hub name" placeholder with hello name of hello notification hub that appears in hello Azure Portal.</span></span> <span data-ttu-id="84f38-155">Ayrıca hello bağlantı dizesi yer tutucusunu hello ile değiştirin **DefaultListenSharedAccessSignature** hello elde edilen bağlantı dizesi **erişim ilkeleri** bildirim Hub'ınıza sayfasının bir önceki bölümde.</span><span class="sxs-lookup"><span data-stu-id="84f38-155">Also replace hello connection string placeholder with hello **DefaultListenSharedAccessSignature** connection string that you obtained from hello **Access Polices** page of your Notification Hub in a previous section.</span></span>
   > 
   > 
5. <span data-ttu-id="84f38-156">Merhaba hello üstündeki **OnLaunched** App.xaml.cs dosyasındaki olay işleyicisi ekleme çağrısı toohello yeni aşağıdaki hello **Initnotificationsasync** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="84f38-156">At hello top of hello **OnLaunched** event handler in App.xaml.cs, add hello following call toohello new **InitNotificationsAsync** method:</span></span>
   
        InitNotificationsAsync();
   
    <span data-ttu-id="84f38-157">Bu URI her zaman Merhaba uygulaması başlatıldığında bildirim hub'ınıza kayıtlı hello kanal güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="84f38-157">This guarantees that hello channel URI is registered in your notification hub each time hello application is launched.</span></span>
6. <span data-ttu-id="84f38-158">Tuşuna hello **F5** anahtar toorun hello uygulama.</span><span class="sxs-lookup"><span data-stu-id="84f38-158">Press hello **F5** key toorun hello app.</span></span> <span data-ttu-id="84f38-159">Merhaba kayıt anahtarını içeren bir açılır iletişim kutusu görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="84f38-159">A pop-up dialog that contains hello registration key is displayed.</span></span>

<span data-ttu-id="84f38-160">Uygulamanızı hazır tooreceive bildirimleri sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="84f38-160">Your app is now ready tooreceive toast notifications.</span></span>

## <a name="send-notifications"></a><span data-ttu-id="84f38-161">Bildirim gönderme</span><span class="sxs-lookup"><span data-stu-id="84f38-161">Send notifications</span></span>
<span data-ttu-id="84f38-162">Hello bildirimleri göndererek uygulamanızda bildirim alma hızlı bir şekilde test edebilirsiniz [Azure Portal](https://portal.azure.com/) hello kullanarak **Test gönderimi** ekranda hello aşağıda gösterildiği gibi hello bildirim hub'ına, düğme.</span><span class="sxs-lookup"><span data-stu-id="84f38-162">You can quickly test receiving notifications in your app by sending notifications in hello [Azure Portal](https://portal.azure.com/) using hello **Test Send** button on hello notification hub, as shown in hello screen below.</span></span>

![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-test-send-wns.png)

<span data-ttu-id="84f38-163">Anında iletme bildirimleri normalde, uyumlu bir kitaplık kullanılarak Mobile Services veya ASP.NET gibi bir arka uç hizmetinde gönderilir.</span><span class="sxs-lookup"><span data-stu-id="84f38-163">Push notifications are normally sent in a back-end service like Mobile Services or ASP.NET using a compatible library.</span></span> <span data-ttu-id="84f38-164">Bir kitaplık arka ucunuz için kullanılabilir değilse toosend bildirim iletilerini doğrudan hello REST API de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84f38-164">You can also use hello REST API directly toosend notification messages if a library is not available for your back-end.</span></span> 

<span data-ttu-id="84f38-165">Bu öğreticide, biz basit tutmak ve yalnızca arka uç hizmeti yerine bir konsol uygulamasındaki bildirim hub'ları için hello .NET SDK kullanarak bildirim göndererek istemci uygulamanızı test etme gösterin.</span><span class="sxs-lookup"><span data-stu-id="84f38-165">In this tutorial, we will keep it simple and just demonstrate testing your client app by sending notifications using hello .NET SDK for notification hubs in a console application instead of a backend service.</span></span> <span data-ttu-id="84f38-166">Merhaba öneririz [Notification Hubs kullanma toopush bildirimleri toousers] hello bir ASP.NET arka ucundan bildirim göndermek için sonraki adım olarak Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="84f38-166">We recommend hello [Use Notification Hubs toopush notifications toousers] tutorial as hello next step for sending notifications from an ASP.NET backend.</span></span> <span data-ttu-id="84f38-167">Ancak, aşağıdaki yaklaşımlardan hello bildirim göndermek için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="84f38-167">However, hello following approaches can be used for sending notifications:</span></span>

* <span data-ttu-id="84f38-168">**REST arabirimi**: hello kullanarak herhangi bir arka uç platform bildirim destekleyebilir [REST arabirimini](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span><span class="sxs-lookup"><span data-stu-id="84f38-168">**REST Interface**:  You can support notification on any backend platform using  hello [REST interface](http://msdn.microsoft.com/library/windowsazure/dn223264.aspx).</span></span>
* <span data-ttu-id="84f38-169">**Microsoft Azure Notification Hubs .NET SDK'sı**: hello Visual Studio için Nuget Paket Yöneticisi, çalışması [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span><span class="sxs-lookup"><span data-stu-id="84f38-169">**Microsoft Azure Notification Hubs .NET SDK**: In hello Nuget Package Manager for Visual Studio, run [Install-Package Microsoft.Azure.NotificationHubs](https://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/).</span></span>
* <span data-ttu-id="84f38-170">**Node.js** : [nasıl toouse node.js'den Notification Hubs](notification-hubs-nodejs-push-notification-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="84f38-170">**Node.js** : [How toouse Notification Hubs from Node.js](notification-hubs-nodejs-push-notification-tutorial.md).</span></span>
* <span data-ttu-id="84f38-171">**Azure Mobile Apps**: bir örneği için Notification Hubs ile tümleştirilmiş bir Azure mobil uygulaması toosend bildirimleri bkz [Mobile Apps için anında iletme bildirimleri ekleme](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span><span class="sxs-lookup"><span data-stu-id="84f38-171">**Azure Mobile Apps**: For an example of how toosend notifications from an Azure Mobile App that's integrated with Notification Hubs, see [Add push notifications for Mobile Apps](../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-push.md).</span></span>
* <span data-ttu-id="84f38-172">**Java / PHP**: REST API'lerini kullanarak toosend bildirim nasıl hello ilişkin bir örnek için bkz: "nasıl toouse Java/php'den Notification Hubs" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span><span class="sxs-lookup"><span data-stu-id="84f38-172">**Java / PHP**: For an example of how toosend notifications by using hello REST APIs, see "How toouse Notification Hubs from Java/PHP" ([Java](notification-hubs-java-push-notification-tutorial.md) | [PHP](notification-hubs-php-push-notification-tutorial.md)).</span></span>

## <a name="optional-send-notifications-from-a-console-app"></a><span data-ttu-id="84f38-173">(İsteğe bağlı) Konsol uygulamasından bildirim gönderme</span><span class="sxs-lookup"><span data-stu-id="84f38-173">(Optional) Send notifications from a console app</span></span>
<span data-ttu-id="84f38-174">bir .NET konsol uygulaması kullanarak toosend bildirim aşağıdaki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="84f38-174">toosend notifications by using a .NET console application follow these steps.</span></span> 

1. <span data-ttu-id="84f38-175">Sağ hello çözüm, select **Ekle** ve **yeni proje...** ve ardından **Visual C#**, tıklatın **Windows** ve **konsol uygulaması**, tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="84f38-175">Right-click hello solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span></span>
   
    <span data-ttu-id="84f38-176">Yeni Visual C# konsol uygulaması toohello çözümü ekler.</span><span class="sxs-lookup"><span data-stu-id="84f38-176">This adds a new Visual C# console application toohello solution.</span></span> <span data-ttu-id="84f38-177">Bunu ayrı bir çözümde de yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84f38-177">You can also do this in a separate solution.</span></span>

2. <span data-ttu-id="84f38-178">Visual Studio'da **Araçlar**'a, **NuGet Paket Yöneticisi**'ne ve ardından **Paket Yöneticisi Konsolu**'na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="84f38-178">In Visual Studio, click **Tools**, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="84f38-179">Bu, Visual Studio'da Paket Yöneticisi konsolu hello görüntüler.</span><span class="sxs-lookup"><span data-stu-id="84f38-179">This displays hello Package Manager Console in Visual Studio.</span></span>
3. <span data-ttu-id="84f38-180">Hello Paket Yöneticisi konsolu penceresinde, hello ayarlamak **varsayılan proje** tooyour yeni konsol uygulama projesi ve sonra hello konsol penceresinde hello aşağıdaki komutu yürütün:</span><span class="sxs-lookup"><span data-stu-id="84f38-180">In hello Package Manager Console window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
        Install-Package Microsoft.Azure.NotificationHubs
   
    <span data-ttu-id="84f38-181">Bu başvuru toohello Azure Notification Hubs SDK'sı ekler hello kullanarak <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet paketini</a>.</span><span class="sxs-lookup"><span data-stu-id="84f38-181">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
   
    ![](./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-package-manager.png)
4. <span data-ttu-id="84f38-182">Merhaba Program.cs dosyasını açın ve hello aşağıdakileri ekleyin `using` deyimi:</span><span class="sxs-lookup"><span data-stu-id="84f38-182">Open hello Program.cs file and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="84f38-183">Merhaba, **Program** sınıfı, yöntem aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="84f38-183">In hello **Program** class, add hello following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            var toast = @"<toast><visual><binding template=""ToastText01""><text id=""1"">Hello from a .NET App!</text></binding></visual></toast>";
            await hub.SendWindowsNativeNotificationAsync(toast);
        }
   
       Make sure tooreplace hello "hub name" placeholder with hello name of hello notification hub that as it appears in hello Azure Portal. Also, replace hello connection string placeholder with hello **DefaultFullSharedAccessSignature** connection string that you obtained from hello **Access Policies** page of your Notification Hub in hello section called "Configure your notification hub."
   
   > [!NOTE]
   > <span data-ttu-id="84f38-184">Sahip hello bağlantı dizesini kullandığınızdan emin olun **tam** erişimi ile değil, **dinleme** erişim.</span><span class="sxs-lookup"><span data-stu-id="84f38-184">Make sure that you use hello connection string that has **Full** access, not **Listen** access.</span></span> <span data-ttu-id="84f38-185">Merhaba dinleme erişimi dizesinin izinleri toosend bildirimleri yok.</span><span class="sxs-lookup"><span data-stu-id="84f38-185">hello listen-access string does not have permissions toosend notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="84f38-186">Merhaba satırlarında aşağıdaki hello eklemek **ana** yöntemi:</span><span class="sxs-lookup"><span data-stu-id="84f38-186">Add hello following lines in hello **Main** method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="84f38-187">Visual Studio'da Hello konsol uygulama projesi sağ tıklayın ve **başlangıç projesi olarak ayarla** tooset hello başlangıç projesi olarak.</span><span class="sxs-lookup"><span data-stu-id="84f38-187">Right-click hello console application project in Visual Studio, and click **Set as StartUp Project** tooset it as hello startup project.</span></span> <span data-ttu-id="84f38-188">Merhaba tuşuna **F5** anahtar toorun Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="84f38-188">Then press hello **F5** key toorun hello application.</span></span>
   
    <span data-ttu-id="84f38-189">Tüm kayıtlı cihazlarda bildirim alırsınız.</span><span class="sxs-lookup"><span data-stu-id="84f38-189">You will receive a toast notification on all registered devices.</span></span> <span data-ttu-id="84f38-190">Tıklatmak veya dokunarak hello bildirim başlığına hello uygulamayı yükler.</span><span class="sxs-lookup"><span data-stu-id="84f38-190">Clicking or tapping hello toast banner loads hello app.</span></span>

<span data-ttu-id="84f38-191">Hello tüm hello desteklenen yükleri bulabilirsiniz [bildirim Kataloğu], [kutucuk Kataloğu], ve [göstergeye genel bakış] MSDN'de Konular.</span><span class="sxs-lookup"><span data-stu-id="84f38-191">You can find all hello supported payloads in hello [toast catalog], [tile catalog], and [badge overview] topics on MSDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="84f38-192">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="84f38-192">Next steps</span></span>
<span data-ttu-id="84f38-193">Bu basit örnekte hello portalı veya bir konsol uygulaması kullanarak Windows cihazlarınıza yayın bildirimleri tooall gönderdi.</span><span class="sxs-lookup"><span data-stu-id="84f38-193">In this simple example, you sent broadcast notifications tooall your Windows devices using hello portal or a console app.</span></span> <span data-ttu-id="84f38-194">Merhaba öneririz [Notification Hubs kullanma toopush bildirimleri toousers] hello sonraki adım olarak Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="84f38-194">We recommend hello [Use Notification Hubs toopush notifications toousers] tutorial as hello next step.</span></span> <span data-ttu-id="84f38-195">Bunu nasıl kullanarak bir ASP.NET arka uç toosend bildirimleri etiketler tootarget belirli kullanıcılara gösterilir.</span><span class="sxs-lookup"><span data-stu-id="84f38-195">It will show you how toosend notifications from an ASP.NET backend using tags tootarget specific users.</span></span>

<span data-ttu-id="84f38-196">Kullanıcılarınızı ilgi alanı gruplarına göre toosegment istiyorsanız, bkz: [son dakika haberleri Notification Hubs kullanma toosend].</span><span class="sxs-lookup"><span data-stu-id="84f38-196">If you want toosegment your users by interest groups, see [Use Notification Hubs toosend breaking news].</span></span> 

<span data-ttu-id="84f38-197">toolearn Notification Hubs hakkında daha fazla genel bilgi [Notification Hubs Kılavuzu](notification-hubs-push-notification-overview.md).</span><span class="sxs-lookup"><span data-stu-id="84f38-197">toolearn more general information about Notification Hubs, see [Notification Hubs Guidance](notification-hubs-push-notification-overview.md).</span></span>

<!-- Images. -->
[13]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-create-console-app.png
[14]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-toast.png
[19]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-reg.png
[20]: ./media/notification-hubs-windows-store-dotnet-get-started/notification-hub-windows-universal-app-install-package.png

<!-- URLs. -->

[Notification Hubs kullanma toopush bildirimleri toousers]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[son dakika haberleri Notification Hubs kullanma toosend]: notification-hubs-windows-notification-dotnet-push-xplat-segmented-wns.md

[bildirim Kataloğu]: http://msdn.microsoft.com/library/windows/apps/hh761494.aspx
[kutucuk Kataloğu]: http://msdn.microsoft.com/library/windows/apps/hh761491.aspx
[göstergeye genel bakış]: http://msdn.microsoft.com/library/windows/apps/hh779719.aspx
