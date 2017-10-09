---
title: "Windows Phone üzerinde Azure Notification Hubs ile aaaSending anında iletme bildirimleri | Microsoft Docs"
description: "Bu öğreticide, nasıl toouse Azure Notification Hubs toopush bildirimleri tooa Windows Phone öğrenin 8 veya Windows Phone 8.1 Silverlight uygulaması."
services: notification-hubs
documentationcenter: windows
keywords: "anında iletme bildirimi,anında iletme bildirimi,windows phone anında iletme"
author: ysxu
manager: erikre
editor: erikre
ms.assetid: d872d8dc-4658-4d65-9e71-fa8e34fae96e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 10/03/2016
ms.author: yuaxu
ms.openlocfilehash: 1a0ad238fe7788ae2e4f47f02d113391af03dd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-on-windows-phone"></a><span data-ttu-id="a9644-104">Windows Phone'da Azure Notification Hubs ile anında iletme bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="a9644-104">Sending push notifications with Azure Notification Hubs on Windows Phone</span></span>
[!INCLUDE [notification-hubs-selector-get-started](../../includes/notification-hubs-selector-get-started.md)]

## <a name="overview"></a><span data-ttu-id="a9644-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="a9644-105">Overview</span></span>
> [!NOTE]
> <span data-ttu-id="a9644-106">toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a9644-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="a9644-107">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9644-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a9644-108">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).</span><span class="sxs-lookup"><span data-stu-id="a9644-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A0E0E5C02&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-windows-phone-get-started%2F).</span></span>
> 
> 

<span data-ttu-id="a9644-109">Bu öğretici nasıl toouse Azure Notification Hubs toosend anında bildirimler tooa Windows Phone 8 veya Windows Phone 8.1 Silverlight uygulamasına gösterir.</span><span class="sxs-lookup"><span data-stu-id="a9644-109">This tutorial shows you how toouse Azure Notification Hubs toosend push notifications tooa Windows Phone 8 or Windows Phone 8.1 Silverlight application.</span></span> <span data-ttu-id="a9644-110">Windows Phone 8.1 (Silverlight olmayan) hedefliyorsanız, toohello başvuran [Windows Evrensel](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) sürümü.</span><span class="sxs-lookup"><span data-stu-id="a9644-110">If you are targeting Windows Phone 8.1 (non-Silverlight), then refer toohello [Windows Universal](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) version.</span></span>
<span data-ttu-id="a9644-111">Bu öğreticide, hello Microsoft anında iletme bildirimi Hizmeti'ni (MPNS) kullanarak anında iletme bildirimleri alan boş bir Windows Phone 8 uygulaması oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="a9644-111">In this tutorial, you create a blank Windows Phone 8 app that receives push notifications by using hello Microsoft Push Notification Service (MPNS).</span></span> <span data-ttu-id="a9644-112">Mümkün toouse olacak tamamladığınızda, bildirim hub'ı toobroadcast uygulamanızı çalıştıran bildirimleri tooall hello cihazlar iletin.</span><span class="sxs-lookup"><span data-stu-id="a9644-112">When you're finished, you'll be able toouse your notification hub toobroadcast push notifications tooall hello devices running your app.</span></span>

> [!NOTE]
> <span data-ttu-id="a9644-113">Merhaba Notification Hubs Windows Phone SDK'sı hello Windows anında bildirim hizmeti (WNS) Windows Phone 8.1 Silverlight uygulamaları ile kullanmayı desteklemez.</span><span class="sxs-lookup"><span data-stu-id="a9644-113">hello Notification Hubs Windows Phone SDK does not support using hello Windows Push Notification Service (WNS) with Windows Phone 8.1 Silverlight apps.</span></span> <span data-ttu-id="a9644-114">toouse WNS'yi (MPNS) yerine Windows Phone 8.1 Silverlight uygulamaları ile izleyin hello [Notification Hubs - Windows Phone Silverlight Öğreticisi], REST API'lerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="a9644-114">toouse WNS (instead of MPNS) with Windows Phone 8.1 Silverlight apps, follow hello [Notification Hubs - Windows Phone Silverlight tutorial], which uses REST APIs.</span></span>
> 
> 

<span data-ttu-id="a9644-115">Merhaba öğretici Notification Hubs kullanımında hello basit yayın senaryosunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="a9644-115">hello tutorial demonstrates hello simple broadcast scenario in using Notification Hubs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9644-116">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a9644-116">Prerequisites</span></span>
<span data-ttu-id="a9644-117">Bu öğretici hello aşağıdakileri gerektirir:</span><span class="sxs-lookup"><span data-stu-id="a9644-117">This tutorial requires hello following:</span></span>

* <span data-ttu-id="a9644-118">[Windows Phone için Visual Studio 2012 Express] veya sonraki bir sürümü.</span><span class="sxs-lookup"><span data-stu-id="a9644-118">[Visual Studio 2012 Express for Windows Phone], or a later version.</span></span>

<span data-ttu-id="a9644-119">Bu öğreticiyi tamamlamak Windows Phone 8 uygulamalarına ilişkin diğer tüm Notification Hubs öğreticileri için önkoşuldur.</span><span class="sxs-lookup"><span data-stu-id="a9644-119">Completing this tutorial is a prerequisite for all other Notification Hubs tutorials for Windows Phone 8 apps.</span></span>

## <a name="create-your-notification-hub"></a><span data-ttu-id="a9644-120">Bildirim hub'ınızı oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9644-120">Create your notification hub</span></span>
[!INCLUDE [notification-hubs-portal-create-new-hub](../../includes/notification-hubs-portal-create-new-hub.md)]

<ol start="6">
<li><p><span data-ttu-id="a9644-121">Hello tıklatın <b>Bildirim Hizmetleri</b> bölümüne (içinde <i>ayarları</i>), tıklayın <b>Windows Phone (MPNS)</b> ve hello ardından <b>kimliği doğrulanmamış gönderimi etkinleştir </b> onay kutusu.</span><span class="sxs-lookup"><span data-stu-id="a9644-121">Click hello <b>Notification Services</b> section (within <i>Settings</i>), click on <b>Windows Phone (MPNS)</b> and then click hello <b>Enable unauthenticated push</b> check box.</span></span></p>
</li>
</ol>

&emsp;&emsp;![Azure Portal - Kimliği doğrulanmamış anında iletme bildirimlerini etkinleştirme](./media/notification-hubs-windows-phone-get-started/azure-portal-unauth.png)

<span data-ttu-id="a9644-123">Hub'ınız şimdi kimliği doğrulanmamış oluşturulan ve yapılandırılan toosend Windows Phone için bildirimidir.</span><span class="sxs-lookup"><span data-stu-id="a9644-123">Your hub is now created and configured toosend unauthenticated notification for Windows Phone.</span></span>

> [!NOTE]
> <span data-ttu-id="a9644-124">Bu öğretici, MPNS'yi kimlik doğrulamasız modda kullanır.</span><span class="sxs-lookup"><span data-stu-id="a9644-124">This tutorial uses MPNS in unauthenticated mode.</span></span> <span data-ttu-id="a9644-125">MPNS kimlik doğrulamasız modda tooeach kanal gönderebilirsiniz bildirimlerini sınırlamalarla birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="a9644-125">MPNS unauthenticated mode comes with restrictions on notifications that you can send tooeach channel.</span></span> <span data-ttu-id="a9644-126">Bildirim hub'ları destekler [MPNS kimlik doğrulamalı mod](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) tooupload sağlayarak sertifikanızı.</span><span class="sxs-lookup"><span data-stu-id="a9644-126">Notification Hubs supports [MPNS authenticated mode](http://msdn.microsoft.com/library/windowsphone/develop/ff941099.aspx) by allowing you tooupload your certificate.</span></span>
> 
> 

## <a name="connecting-your-app-toohello-notification-hub"></a><span data-ttu-id="a9644-127">Uygulama toohello bildirim hub'ınız bağlanma</span><span class="sxs-lookup"><span data-stu-id="a9644-127">Connecting your app toohello notification hub</span></span>
1. <span data-ttu-id="a9644-128">Visual Studio'da yeni bir Windows Phone 8 uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a9644-128">In Visual Studio, create a new Windows Phone 8 application.</span></span>
   
       ![Visual Studio - New Project - Windows Phone App][13]
   
    <span data-ttu-id="a9644-129">Visual Studio 2013 Güncelleştirme 2 veya sonrasında, bunun yerine Windows Phone Silverlight uygulaması oluşturursunuz.</span><span class="sxs-lookup"><span data-stu-id="a9644-129">In Visual Studio 2013 Update 2 or later, you instead create a Windows Phone Silverlight application.</span></span>
   
    ![Visual Studio - Yeni Proje - Boş Uygulama - Windows Phone Silverlight][11]
2. <span data-ttu-id="a9644-131">Visual Studio'da hello çözüme sağ tıklayın ve ardından **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="a9644-131">In Visual Studio, right-click hello solution, and then click **Manage NuGet Packages**.</span></span>
   
    <span data-ttu-id="a9644-132">Bu hello görüntüler **NuGet paketlerini Yönet** iletişim kutusu.</span><span class="sxs-lookup"><span data-stu-id="a9644-132">This displays hello **Manage NuGet Packages** dialog box.</span></span>
3. <span data-ttu-id="a9644-133">Arama `WindowsAzure.Messaging.Managed` tıklatıp **yükleme**ve hello kullanım koşullarını kabul edin.</span><span class="sxs-lookup"><span data-stu-id="a9644-133">Search for `WindowsAzure.Messaging.Managed` and click **Install**, and then accept hello terms of use.</span></span>
   
    ![Visual Studio - NuGet Paket Yöneticisi][20]
   
    <span data-ttu-id="a9644-135">Bu indirir, yükler ve bir başvuru toohello Azure Mesajlaşma kitaplığına için Windows hello kullanarak ekler <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet paketini</a>.</span><span class="sxs-lookup"><span data-stu-id="a9644-135">This downloads, installs, and adds a reference toohello Azure Messaging library for Windows by using hello <a href="http://nuget.org/packages/WindowsAzure.Messaging.Managed/">WindowsAzure.Messaging.Managed NuGet package</a>.</span></span>
4. <span data-ttu-id="a9644-136">Merhaba App.xaml.cs dosyasını açın ve hello aşağıdakileri ekleyin `using` deyimleri:</span><span class="sxs-lookup"><span data-stu-id="a9644-136">Open hello file App.xaml.cs and add hello following `using` statements:</span></span>
   
        using Microsoft.Phone.Notification;
        using Microsoft.WindowsAzure.Messaging;
5. <span data-ttu-id="a9644-137">Merhaba üst kısmındaki koddan hello eklemek **Application_Launching** App.xaml.cs yöntemi:</span><span class="sxs-lookup"><span data-stu-id="a9644-137">Add hello following code at hello top of **Application_Launching** method in App.xaml.cs:</span></span>
   
        var channel = HttpNotificationChannel.Find("MyPushChannel");
        if (channel == null)
        {
            channel = new HttpNotificationChannel("MyPushChannel");
            channel.Open();
            channel.BindToShellToast();
        }
   
        channel.ChannelUriUpdated += new EventHandler<NotificationChannelUriEventArgs>(async (o, args) =>
        {
            var hub = new NotificationHub("<hub name>", "<connection string>");
            var result = await hub.RegisterNativeAsync(args.ChannelUri.ToString());
   
            System.Windows.Deployment.Current.Dispatcher.BeginInvoke(() =>
            {
                MessageBox.Show("Registration :" + result.RegistrationId, "Registered", MessageBoxButton.OK);
            });
        });
   
   > [!NOTE]
   > <span data-ttu-id="a9644-138">Merhaba değeri **MyPushChannel** kullanılan toolookup hello içinde var olan bir kanalı olan bir dizini [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="a9644-138">hello value **MyPushChannel** is an index that is used toolookup an existing channel in hello [HttpNotificationChannel](https://msdn.microsoft.com/library/windows/apps/microsoft.phone.notification.httpnotificationchannel.aspx) collection.</span></span> <span data-ttu-id="a9644-139">Bu koleksiyonda bir tane bulunmuyorsa bu adla yeni bir giriş oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a9644-139">If there isn't one there, create a new entry with that name.</span></span>
   > 
   > 
   
    <span data-ttu-id="a9644-140">Hub ve hello bağlantı dizenizi tooinsert hello adı adlı emin olun **DefaultListenSharedAccessSignature** hello önceki bölümde edindiğiniz.</span><span class="sxs-lookup"><span data-stu-id="a9644-140">Make sure tooinsert hello name of your hub and hello connection string called **DefaultListenSharedAccessSignature** that you obtained in hello previous section.</span></span>
    <span data-ttu-id="a9644-141">Bu kod, MPNS'den hello uygulama hello kanal URI'sini alır ve ardından bu kanal URI'sini bildirim hub'ınıza kaydeder.</span><span class="sxs-lookup"><span data-stu-id="a9644-141">This code retrieves hello channel URI for hello app from MPNS, and then registers that channel URI with your notification hub.</span></span> <span data-ttu-id="a9644-142">Ayrıca her zaman Merhaba uygulaması başlatıldığında bildirim hub'ınıza URI kayıtlı hello kanal güvence altına alır.</span><span class="sxs-lookup"><span data-stu-id="a9644-142">It also guarantees that hello channel URI is registered in your notification hub each time hello application is launched.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a9644-143">Bu öğretici bir bildirim bildirim toohello aygıt gönderir.</span><span class="sxs-lookup"><span data-stu-id="a9644-143">This tutorial sends a toast notification toohello device.</span></span> <span data-ttu-id="a9644-144">Bunun yerine bir kutucuk bildirimi gönderdiğinizde, hello çağırmalısınız **BindToShellTile** hello kanalda yöntemi.</span><span class="sxs-lookup"><span data-stu-id="a9644-144">When you send a tile notification, you must instead call hello **BindToShellTile** method on hello channel.</span></span> <span data-ttu-id="a9644-145">toosupport bildirim ve kutucuk bildirimlerinin her ikisini de çağrısı **BindToShellTile** ve **BindToShellToast**.</span><span class="sxs-lookup"><span data-stu-id="a9644-145">toosupport both toast and tile notifications, call both **BindToShellTile** and  **BindToShellToast**.</span></span>
   > 
   > 
6. <span data-ttu-id="a9644-146">Çözüm Gezgini'nde genişletin **özellikleri**açın hello `WMAppManifest.xml` dosya, hello tıklatın **yetenekleri** sekmesinde ve o hello emin olun **ıd_cap_push_notıfıcatıon** Yetenek denetlenir.</span><span class="sxs-lookup"><span data-stu-id="a9644-146">In Solution Explorer, expand **Properties**, open hello `WMAppManifest.xml` file, click hello **Capabilities** tab, and make sure that hello **ID_CAP_PUSH_NOTIFICATION** capability is checked.</span></span>
   
       ![Visual Studio - Windows Phone App Capabilities][14]
   
       This ensures that your app can receive push notifications. Without it, any attempt toosend a push notification toohello app will fail.
7. <span data-ttu-id="a9644-147">Tuşuna hello `F5` anahtar toorun hello uygulama.</span><span class="sxs-lookup"><span data-stu-id="a9644-147">Press hello `F5` key toorun hello app.</span></span>
   
    <span data-ttu-id="a9644-148">Merhaba uygulamada bir kayıt iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="a9644-148">A registration message is displayed in hello app.</span></span>
8. <span data-ttu-id="a9644-149">Kapat hello uygulama.</span><span class="sxs-lookup"><span data-stu-id="a9644-149">Close hello app.</span></span>  
   
   > [!NOTE]
   > <span data-ttu-id="a9644-150">bildirim biçiminde bir anında iletme bildirimi tooreceive Merhaba uygulaması hello ön planda çalışmıyor olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="a9644-150">tooreceive a toast push notification, hello application must not be running in hello foreground.</span></span>
   > 
   > 

## <a name="send-push-notifications-from-your-backend"></a><span data-ttu-id="a9644-151">Arka ucunuzdan anında iletme bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="a9644-151">Send push notifications from your backend</span></span>
<span data-ttu-id="a9644-152">Bildirim hub'ları kullanarak hello ortak aracılığıyla herhangi bir arka uçtan anında iletme bildirimleri gönderebilirsiniz <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST arabirimini</a>.</span><span class="sxs-lookup"><span data-stu-id="a9644-152">You can send push notifications by using Notification Hubs from any backend via hello public <a href="http://msdn.microsoft.com/library/windowsazure/dn223264.aspx">REST interface</a>.</span></span> <span data-ttu-id="a9644-153">Bu öğreticide, bir .NET konsol uygulaması kullanarak anında iletme bildirimleri gönderirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9644-153">In this tutorial, you send push notifications using a .NET console application.</span></span> 

<span data-ttu-id="a9644-154">Nasıl toosend anında iletme bildirimleri Notification Hubs ile tümleştirilmiş bir ASP.NET Webapı arka ilişkin bir örnek için bkz: [Azure Notification Hubs kullanıcılara bildirme .NET arka ucu ile](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).</span><span class="sxs-lookup"><span data-stu-id="a9644-154">For an example of how toosend push notifications from an ASP.NET WebAPI backend that's integrated with Notification Hubs, see [Azure Notification Hubs Notify Users with .NET backend](notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md).</span></span>  

<span data-ttu-id="a9644-155">Bir örneği kullanarak toosend anında iletme bildirimleri nasıl hello [REST API'leri](https://msdn.microsoft.com/library/azure/dn223264.aspx), kullanıma [nasıl toouse Java'dan Notification Hubs](notification-hubs-java-push-notification-tutorial.md) ve [nasıl toouse php'den Notification Hubs](notification-hubs-php-push-notification-tutorial.md) .</span><span class="sxs-lookup"><span data-stu-id="a9644-155">For an example of how toosend push notifications by using hello [REST APIs](https://msdn.microsoft.com/library/azure/dn223264.aspx), check out [How toouse Notification Hubs from Java](notification-hubs-java-push-notification-tutorial.md) and [How toouse Notification Hubs from PHP](notification-hubs-php-push-notification-tutorial.md).</span></span>

1. <span data-ttu-id="a9644-156">Sağ hello çözüm, select **Ekle** ve **yeni proje...** ve ardından **Visual C#**, tıklatın **Windows** ve **konsol uygulaması**, tıklatıp **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="a9644-156">Right-click hello solution, select **Add** and **New Project...**, and then under **Visual C#**, click **Windows** and **Console Application**, and click **OK**.</span></span>
   
       ![Visual Studio - New Project - Console Application][6]
   
    <span data-ttu-id="a9644-157">Yeni Visual C# konsol uygulaması toohello çözümü ekler.</span><span class="sxs-lookup"><span data-stu-id="a9644-157">This adds a new Visual C# console application toohello solution.</span></span> <span data-ttu-id="a9644-158">Bunu ayrı bir çözümde de yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9644-158">You can also do this in a separate solution.</span></span>
2. <span data-ttu-id="a9644-159">**Araçlar**'a, **Kitaplık Paket Yöneticisi**'ne ve ardından **Paket Yöneticisi Konsolu**'na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="a9644-159">Click **Tools**, click **Library Package Manager**, and then click **Package Manager Console**.</span></span>
   
    <span data-ttu-id="a9644-160">Merhaba Paket Yöneticisi Konsolu'nu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="a9644-160">This displays hello Package Manager Console.</span></span>
3. <span data-ttu-id="a9644-161">Merhaba, **Paket Yöneticisi Konsolu** penceresinde, kümesi hello **varsayılan proje** tooyour yeni konsol uygulama projesi ve sonra hello konsol penceresinde hello aşağıdaki komutu yürütün:</span><span class="sxs-lookup"><span data-stu-id="a9644-161">In hello **Package Manager Console** window, set hello **Default project** tooyour new console application project, and then in hello console window, execute hello following command:</span></span>
   
       Install-Package Microsoft.Azure.NotificationHubs
   
   <span data-ttu-id="a9644-162">Bu başvuru toohello Azure Notification Hubs SDK'sı ekler hello kullanarak <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet paketini</a>.</span><span class="sxs-lookup"><span data-stu-id="a9644-162">This adds a reference toohello Azure Notification Hubs SDK using hello <a href="http://www.nuget.org/packages/Microsoft.Azure.NotificationHubs/">Microsoft.Azure.Notification Hubs NuGet package</a>.</span></span>
4. <span data-ttu-id="a9644-163">Açık hello `Program.cs` dosya ve hello aşağıdakileri ekleyin `using` deyimi:</span><span class="sxs-lookup"><span data-stu-id="a9644-163">Open hello `Program.cs` file and add hello following `using` statement:</span></span>
   
        using Microsoft.Azure.NotificationHubs;
5. <span data-ttu-id="a9644-164">Merhaba, `Program` sınıfı, yöntem aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="a9644-164">In hello `Program` class, add hello following method:</span></span>
   
        private static async void SendNotificationAsync()
        {
            NotificationHubClient hub = NotificationHubClient
                .CreateClientFromConnectionString("<connection string with full access>", "<hub name>");
            string toast = "<?xml version=\"1.0\" encoding=\"utf-8\"?>" +
                "<wp:Notification xmlns:wp=\"WPNotification\">" +
                   "<wp:Toast>" +
                        "<wp:Text1>Hello from a .NET App!</wp:Text1>" +
                   "</wp:Toast> " +
                "</wp:Notification>";
            await hub.SendMpnsNativeNotificationAsync(toast);
        }
   
    <span data-ttu-id="a9644-165">Tooreplace hello emin olun `<hub name>` yer tutucu hello Portalı'nda görüntülenen hello bildirim hub'ı hello adı.</span><span class="sxs-lookup"><span data-stu-id="a9644-165">Make sure tooreplace hello `<hub name>` placeholder with hello name of hello notification hub that appears in hello portal.</span></span> <span data-ttu-id="a9644-166">Ayrıca, hello bağlantı dizesi yer tutucusunu adlı hello bağlantı dizesi ile değiştirin **DefaultFullSharedAccessSignature** "bildirim hub'ınızı yapılandırma" Merhaba bölümünde edindiğiniz</span><span class="sxs-lookup"><span data-stu-id="a9644-166">Also, replace hello connection string placeholder with hello connection string called **DefaultFullSharedAccessSignature** that you obtained in hello section "Configure your notification hub."</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a9644-167">Merhaba bağlantı dizesiyle kullandığınızdan emin olun **tam** erişimi ile değil, **dinleme** erişim.</span><span class="sxs-lookup"><span data-stu-id="a9644-167">Make sure that you use hello connection string with **Full** access, not **Listen** access.</span></span> <span data-ttu-id="a9644-168">Merhaba dinleme erişimi dizesinin izinleri toosend anında iletme bildirimleri yok.</span><span class="sxs-lookup"><span data-stu-id="a9644-168">hello listen-access string does not have permissions toosend push notifications.</span></span>
   > 
   > 
6. <span data-ttu-id="a9644-169">Satırda aşağıdaki hello eklemek, `Main` yöntemi:</span><span class="sxs-lookup"><span data-stu-id="a9644-169">Add hello following line in your `Main` method:</span></span>
   
         SendNotificationAsync();
         Console.ReadLine();
7. <span data-ttu-id="a9644-170">Windows Phone ile çalışan öykünücüsü ve uygulama kapalı, ayarlanmış hello konsol uygulama projesi hello olarak varsayılan başlangıç projesi ve hello tuşuna basın `F5` anahtar toorun hello uygulama.</span><span class="sxs-lookup"><span data-stu-id="a9644-170">With your Windows Phone emulator running and your app closed, set hello console application project as hello default startup project, and then press hello `F5` key toorun hello app.</span></span>
   
    <span data-ttu-id="a9644-171">Bildirim biçiminde bir anında iletme bildirimi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="a9644-171">You will receive a toast push notification.</span></span> <span data-ttu-id="a9644-172">Merhaba bildirim başlığına dokunmak hello uygulamayı yükler.</span><span class="sxs-lookup"><span data-stu-id="a9644-172">Tapping hello toast banner loads hello app.</span></span>

<span data-ttu-id="a9644-173">Hello hello tüm olası yükleri bulabilirsiniz [bildirim Kataloğu] ve [kutucuk Kataloğu] MSDN'de Konular.</span><span class="sxs-lookup"><span data-stu-id="a9644-173">You can find all hello possible payloads in hello [toast catalog] and [tile catalog] topics on MSDN.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9644-174">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a9644-174">Next steps</span></span>
<span data-ttu-id="a9644-175">Bu basit örnekte, Windows Phone 8 aygıtları anında iletme bildirimleri tooall yayımladınız.</span><span class="sxs-lookup"><span data-stu-id="a9644-175">In this simple example, you broadcasted push notifications tooall your Windows Phone 8 devices.</span></span> 

<span data-ttu-id="a9644-176">Buna belirli kullanıcılara tootarget sipariş, toohello başvurmak [Notification Hubs kullanma toopush bildirimleri toousers] Öğreticisi.</span><span class="sxs-lookup"><span data-stu-id="a9644-176">In order tootarget specific users, refer toohello [Use Notification Hubs toopush notifications toousers] tutorial.</span></span> 

<span data-ttu-id="a9644-177">Toosegment kullanıcılarınızı ilgi alanı gruplarına göre isterseniz, okuyabilirsiniz [son dakika haberleri Notification Hubs kullanma toosend].</span><span class="sxs-lookup"><span data-stu-id="a9644-177">If you want toosegment your users by interest groups, you can read [Use Notification Hubs toosend breaking news].</span></span> 

<span data-ttu-id="a9644-178">Hakkında daha fazla bilgi toouse bildirim hub'ları [Notification Hubs Kılavuzu].</span><span class="sxs-lookup"><span data-stu-id="a9644-178">Learn more about how toouse Notification Hubs in [Notification Hubs Guidance].</span></span>

<!-- Images. -->
[6]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png
[7]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal.png
[8]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-from-portal2.png
[9]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal.png
[10]: ./media/notification-hubs-windows-phone-get-started/notification-hub-select-from-portal2.png
[11]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-silverlight-app.png
[12]: ./media/notification-hubs-windows-phone-get-started/notification-hub-connection-strings.png

[13]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-wp-app.png
[14]: ./media/notification-hubs-windows-phone-get-started/mobile-app-enable-push-wp8.png
[15]: ./media/notification-hubs-windows-phone-get-started/notification-hub-pushauth.png
[20]: ./media/notification-hubs-windows-phone-get-started/notification-hub-windows-universal-app-install-package.png
[213]: ./media/notification-hubs-windows-phone-get-started/notification-hub-create-console-app.png





<!-- URLs. -->
[Windows Phone için Visual Studio 2012 Express]: https://go.microsoft.com/fwLink/p/?LinkID=268374
[Notification Hubs Kılavuzu]: http://msdn.microsoft.com/library/jj927170.aspx
[MPNS authenticated mode]: http://msdn.microsoft.com/library/windowsphone/develop/ff941099(v=vs.105).aspx
[Notification Hubs kullanma toopush bildirimleri toousers]: notification-hubs-aspnet-backend-windows-dotnet-wns-notification.md
[son dakika haberleri Notification Hubs kullanma toosend]: notification-hubs-windows-phone-push-xplat-segmented-mpns-notification.md
[bildirim Kataloğu]: http://msdn.microsoft.com/library/windowsphone/develop/jj662938(v=vs.105).aspx
[kutucuk Kataloğu]: http://msdn.microsoft.com/library/windowsphone/develop/hh202948(v=vs.105).aspx
[Notification Hubs - Windows Phone Silverlight Öğreticisi]: https://github.com/Azure/azure-notificationhubs-samples/tree/master/PushToSLPhoneApp

