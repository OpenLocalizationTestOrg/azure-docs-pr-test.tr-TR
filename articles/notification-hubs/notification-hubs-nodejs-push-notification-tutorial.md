---
title: "Azure bildirim hub'ları ve Node.js ile anında iletme bildirimleri gönderme"
description: "Bir Node.js uygulamasından anında iletme bildirimleri göndermek için bildirim hub'ları kullanmayı öğrenin."
keywords: "anında iletme bildirimi, anında iletme notifications,node.js itme ios anında iletme"
services: notification-hubs
documentationcenter: nodejs
author: ysxu
manager: erikre
editor: 
ms.assetid: ded4749c-6c39-4ff8-b2cf-1927b3e92f93
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 10/25/2016
ms.author: yuaxu
ms.openlocfilehash: dc4987b16b2e930641c6c90eff8b65c1bf8d573c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-and-nodejs"></a><span data-ttu-id="3f012-104">Azure bildirim hub'ları ve Node.js ile anında iletme bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="3f012-104">Sending push notifications with Azure Notification Hubs and Node.js</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

## <a name="overview"></a><span data-ttu-id="3f012-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="3f012-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="3f012-106">Bu öğreticiyi tamamlamak için etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3f012-106">To complete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="3f012-107">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3f012-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="3f012-108">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).</span><span class="sxs-lookup"><span data-stu-id="3f012-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).</span></span>
> 
> 

<span data-ttu-id="3f012-109">Bu kılavuz bir Node.js uygulamasından doğrudan Azure Notification Hubs Yardım ile anında iletme bildirimleri göndermek nasıl yapacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="3f012-109">This guide will show you how to send push notifications with the help of Azure Notification Hubs directly from a Node.js application.</span></span> 

<span data-ttu-id="3f012-110">Aşağıdaki platformlarda uygulamalarına anında iletme bildirimleri gönderme kapsamdaki senaryolar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="3f012-110">The scenarios covered include sending push notifications to applications on the following platforms:</span></span>

* <span data-ttu-id="3f012-111">Android</span><span class="sxs-lookup"><span data-stu-id="3f012-111">Android</span></span>
* <span data-ttu-id="3f012-112">iOS</span><span class="sxs-lookup"><span data-stu-id="3f012-112">iOS</span></span>
* <span data-ttu-id="3f012-113">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="3f012-113">Windows Phone</span></span>
* <span data-ttu-id="3f012-114">Evrensel Windows platformu</span><span class="sxs-lookup"><span data-stu-id="3f012-114">Universal Windows Platform</span></span> 

<span data-ttu-id="3f012-115">Bildirim hub'ları hakkında daha fazla bilgi için bkz: [sonraki adımlar](#next) bölümü.</span><span class="sxs-lookup"><span data-stu-id="3f012-115">For more information on notification hubs, see the [Next Steps](#next) section.</span></span>

## <a name="what-are-notification-hubs"></a><span data-ttu-id="3f012-116">Bildirim Hub'ları nedir?</span><span class="sxs-lookup"><span data-stu-id="3f012-116">What are Notification Hubs?</span></span>
<span data-ttu-id="3f012-117">Azure bildirim hub'ları, mobil cihazlara anında iletme bildirimleri göndermek için kullanımı kolay, çok platformlu, ölçeklenebilir bir altyapı sunar.</span><span class="sxs-lookup"><span data-stu-id="3f012-117">Azure Notification Hubs provide an easy-to-use, multi-platform, scalable infrastructure for sending push notifications to mobile devices.</span></span> <span data-ttu-id="3f012-118">Hizmet altyapısı hakkında daha fazla bilgi için bkz: [Azure Notification Hubs](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) sayfası.</span><span class="sxs-lookup"><span data-stu-id="3f012-118">For details on the service infrastructure, see the [Azure Notification Hubs](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) page.</span></span>

## <a name="create-a-nodejs-application"></a><span data-ttu-id="3f012-119">Bir Node.js uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="3f012-119">Create a Node.js Application</span></span>
<span data-ttu-id="3f012-120">Bu öğreticinin ilk adımı, yeni ve boş bir Node.js uygulaması oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="3f012-120">The first step in this tutorial is creating a new blank Node.js application.</span></span> <span data-ttu-id="3f012-121">Bir Node.js uygulaması oluşturma ile ilgili yönergeler için bkz: [oluşturma ve bir Node.js uygulamasını Azure Web sitesini dağıtmak][nodejswebsite], [Node.js bulut hizmeti] [ Node.js Cloud Service] Windows PowerShell kullanarak veya [Web sitesini WebMatrix ile].</span><span class="sxs-lookup"><span data-stu-id="3f012-121">For instructions on creating a Node.js application, see [Create and deploy a Node.js application to Azure Web Site][nodejswebsite], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or [Web Site with WebMatrix].</span></span>

## <a name="configure-your-application-to-use-notification-hubs"></a><span data-ttu-id="3f012-122">Uygulamanızı bildirim hub'ları kullanacak şekilde yapılandırma</span><span class="sxs-lookup"><span data-stu-id="3f012-122">Configure Your Application to Use Notification Hubs</span></span>
<span data-ttu-id="3f012-123">Azure bildirim hub'ları kullanmak için karşıdan yükleme ve Node.js kullanma gerekir [azure paketi](https://www.npmjs.com/package/azure), anında iletme bildirimi REST Hizmetleri ile iletişim yardımcı kitaplıklar yerleşik bir kümesini içerir.</span><span class="sxs-lookup"><span data-stu-id="3f012-123">To use Azure Notification Hubs, you need to download and use the Node.js [azure package](https://www.npmjs.com/package/azure), which includes a built-in set of helper libraries that communicate with the push notification REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="3f012-124">Paket elde etmek için düğüm paketi Yöneticisi (NPM) kullanın</span><span class="sxs-lookup"><span data-stu-id="3f012-124">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="3f012-125">Bir komut satırı arabirimi gibi kullandığınız **PowerShell** (Windows), **Terminal** (Mac) veya **Bash** (Linux) ve boş uygulamanızı oluşturduğunuz klasöre gidin.</span><span class="sxs-lookup"><span data-stu-id="3f012-125">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Linux) and navigate to the folder where you created your blank application.</span></span>
2. <span data-ttu-id="3f012-126">Tür **npm yükleme azure sb** komut penceresinde.</span><span class="sxs-lookup"><span data-stu-id="3f012-126">Type **npm install azure-sb** in the command window.</span></span>
3. <span data-ttu-id="3f012-127">El ile çalıştırabilirsiniz **ls** veya **dir** doğrulamak için komutu bir **düğümü\_modülleri** klasörü oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="3f012-127">You can manually run the **ls** or **dir** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="3f012-128">Bu klasör içinde bulma **azure** bildirim hub'ı erişmek için gereken kitaplıklar içeren paket.</span><span class="sxs-lookup"><span data-stu-id="3f012-128">Inside that folder, find the **azure** package, which contains the libraries you need to access the Notification Hub.</span></span>

> [!NOTE]
> <span data-ttu-id="3f012-129">Üzerinde resmi NPM yükleme hakkında daha fazla bilgiyi [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm).</span><span class="sxs-lookup"><span data-stu-id="3f012-129">You can learn more about installing NPM on the official [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm).</span></span> 
> 
> 

### <a name="import-the-module"></a><span data-ttu-id="3f012-130">Modülünü içeri aktarın</span><span class="sxs-lookup"><span data-stu-id="3f012-130">Import the module</span></span>
<span data-ttu-id="3f012-131">Bir metin düzenleyicisi kullanarak, en üstüne aşağıdakileri ekleyin **server.js** uygulamanın dosya:</span><span class="sxs-lookup"><span data-stu-id="3f012-131">Using a text editor, add the following to the top of the **server.js** file of the application:</span></span>

    var azure = require('azure');

### <a name="setup-an-azure-notification-hub-connection"></a><span data-ttu-id="3f012-132">Azure bildirim hub'ı bağlantısı kurma</span><span class="sxs-lookup"><span data-stu-id="3f012-132">Setup an Azure Notification Hub connection</span></span>
<span data-ttu-id="3f012-133">**NotificationHubService** nesne notification hubs ile çalışmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="3f012-133">The **NotificationHubService** object lets you work with notification hubs.</span></span> <span data-ttu-id="3f012-134">Aşağıdaki kod oluşturur bir **NotificationHubService** adlı nofication hub'ına yönelik nesne **hubname**.</span><span class="sxs-lookup"><span data-stu-id="3f012-134">The following code creates a **NotificationHubService** object for the nofication hub named **hubname**.</span></span> <span data-ttu-id="3f012-135">Üst kısmına ekleyin **server.js** azure modülü içeri aktarmak için deyimi sonra dosyayı:</span><span class="sxs-lookup"><span data-stu-id="3f012-135">Add it near the top of the **server.js** file, after the statement to import the azure module:</span></span>

    var notificationHubService = azure.createNotificationHubService('hubname','connectionstring');

<span data-ttu-id="3f012-136">Bağlantı **connectionstring** değeri elde edilebilir gelen [Azure Portal] aşağıdaki adımları gerçekleştirerek:</span><span class="sxs-lookup"><span data-stu-id="3f012-136">The connection **connectionstring** value can be obtained from the [Azure Portal] by performing the following steps:</span></span>

1. <span data-ttu-id="3f012-137">Sol gezinti bölmesinde **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="3f012-137">In the left navigation pane, click **Browse**.</span></span>
2. <span data-ttu-id="3f012-138">Seçin **bildirim hub'ları**, örnek için kullanmak istediğiniz hub'ı bulun.</span><span class="sxs-lookup"><span data-stu-id="3f012-138">Select **Notification Hubs**, and then find the hub you wish to use for the sample.</span></span> <span data-ttu-id="3f012-139">Başvurabilirsiniz [Windows mağazası Başlarken Öğreticisi](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) yeni bir bildirim hub'ı oluşturma yardıma gereksinim duyarsanız.</span><span class="sxs-lookup"><span data-stu-id="3f012-139">You can refer to the [Windows Store Getting Started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) if you need help creating a new Notification Hub.</span></span>
3. <span data-ttu-id="3f012-140">Seçin **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="3f012-140">Select **Settings**.</span></span>
4. <span data-ttu-id="3f012-141">Tıklayın **erişim ilkeleri**.</span><span class="sxs-lookup"><span data-stu-id="3f012-141">Click on **Access Policies**.</span></span> <span data-ttu-id="3f012-142">Her iki paylaşılan ve tam erişim bağlantı dizeleri görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="3f012-142">You will see both shared and full access connection strings.</span></span>

![Azure Portal - bildirim hub'ları](./media/notification-hubs-nodejs-how-to-use-notification-hubs/notification-hubs-portal.png)

> [!NOTE]
> <span data-ttu-id="3f012-144">Kullanarak bağlantı dizenizi alabilirsiniz **Get-AzureSbNamespace** tarafından sağlanan cmdlet [Azure PowerShell](/powershell/azureps-cmdlets-docs) veya **azure sb ad alanı göster** komutunu [Azure komut satırı arabirimi (Azure CLI)](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="3f012-144">You can also retrieve the connection string using the **Get-AzureSbNamespace** cmdlet provided by [Azure PowerShell](/powershell/azureps-cmdlets-docs) or the **azure sb namespace show** command with the [Azure Command-Line Interface (Azure CLI)](../cli-install-nodejs.md).</span></span>
> 
> 

## <a name="general-architecture"></a><span data-ttu-id="3f012-145">Genel mimari</span><span class="sxs-lookup"><span data-stu-id="3f012-145">General architecture</span></span>
<span data-ttu-id="3f012-146">**NotificationHubService** nesneyi kullanıma sunan belirli cihazlar ve uygulamalar için anında iletme bildirimleri göndermek için aşağıdaki nesne örnekleri:</span><span class="sxs-lookup"><span data-stu-id="3f012-146">The **NotificationHubService** object exposes the following object instances for sending push notifications to specific devices and applications:</span></span>

* <span data-ttu-id="3f012-147">**Android** -kullanmak **GcmService** şu adresten edinilebilir nesne **notificationHubService.gcm**</span><span class="sxs-lookup"><span data-stu-id="3f012-147">**Android** - use the **GcmService** object, which is available at **notificationHubService.gcm**</span></span>
* <span data-ttu-id="3f012-148">**iOS** -kullanmak **ApnsService** adresindeki erişilebilir olan nesne, **notificationHubService.apns**</span><span class="sxs-lookup"><span data-stu-id="3f012-148">**iOS** - use the **ApnsService** object, which is accessible at **notificationHubService.apns**</span></span>
* <span data-ttu-id="3f012-149">**Windows Phone** -kullanmak **MpnsService** şu adresten edinilebilir nesne **notificationHubService.mpns**</span><span class="sxs-lookup"><span data-stu-id="3f012-149">**Windows Phone** - use the **MpnsService** object, which is available at **notificationHubService.mpns**</span></span>
* <span data-ttu-id="3f012-150">**Evrensel Windows platformu** -kullanmak **WnsService** şu adresten edinilebilir nesne **notificationHubService.wns**</span><span class="sxs-lookup"><span data-stu-id="3f012-150">**Universal Windows Platform** - use the **WnsService** object, which is available at **notificationHubService.wns**</span></span>

### <a name="how-to-send-push-notifications-to-android-applications"></a><span data-ttu-id="3f012-151">Nasıl yapılır: Android uygulamalarına anında iletme bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="3f012-151">How to: Send push notifications to Android applications</span></span>
<span data-ttu-id="3f012-152">**GcmService** nesne sağlayan bir **Gönder** Android uygulamalarına anında iletme bildirimleri göndermek için kullanılan yöntem.</span><span class="sxs-lookup"><span data-stu-id="3f012-152">The **GcmService** object provides a **send** method that can be used to send push notifications to Android applications.</span></span> <span data-ttu-id="3f012-153">**Gönder** yöntemi aşağıdaki parametreleri kabul eder:</span><span class="sxs-lookup"><span data-stu-id="3f012-153">The **send** method accepts the following parameters:</span></span>

* <span data-ttu-id="3f012-154">**Etiketler** -etiketi tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="3f012-154">**Tags** - the tag identifier.</span></span> <span data-ttu-id="3f012-155">Hiçbir etiketi sağlanırsa, tüm istemcilere bildirim gönderilir.</span><span class="sxs-lookup"><span data-stu-id="3f012-155">If no tag is provided, the notification will be sent to all clients.</span></span>
* <span data-ttu-id="3f012-156">**Yükü** -ileti JSON veya ham dize yükü.</span><span class="sxs-lookup"><span data-stu-id="3f012-156">**Payload** - the message's JSON or raw string payload.</span></span>
* <span data-ttu-id="3f012-157">**Geri çağırma** -geri çağırma işlevi.</span><span class="sxs-lookup"><span data-stu-id="3f012-157">**Callback** - the callback function.</span></span>

<span data-ttu-id="3f012-158">Yük biçimi hakkında daha fazla bilgi için bkz: **yükü** bölümünü [uygulama GCM Server](http://developer.android.com/google/gcm/server.html#payload) belge.</span><span class="sxs-lookup"><span data-stu-id="3f012-158">For more information on the payload format, see the **Payload** section of the [Implementing GCM Server](http://developer.android.com/google/gcm/server.html#payload) document.</span></span>

<span data-ttu-id="3f012-159">Aşağıdaki kod **GcmService** örneği kullanıma sunulan **NotificationHubService** tüm kayıtlı istemcilere anında iletme bildirimi göndermek için.</span><span class="sxs-lookup"><span data-stu-id="3f012-159">The following code uses the **GcmService** instance exposed by the **NotificationHubService** to send a push notification to all registered clients.</span></span>

    var payload = {
      data: {
        message: 'Hello!'
      }
    };
    notificationHubService.gcm.send(null, payload, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-to-ios-applications"></a><span data-ttu-id="3f012-160">Nasıl yapılır: iOS uygulamalarına anında iletme bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="3f012-160">How to: Send push notifications to iOS applications</span></span>
<span data-ttu-id="3f012-161">Yukarıda açıklanan Android uygulamaları ile aynı **ApnsService** nesnesi sağlar bir **Gönder** iOS uygulamalarına anında iletme bildirimleri göndermek için kullanılan yöntem.</span><span class="sxs-lookup"><span data-stu-id="3f012-161">Same as with Android applications described above, the **ApnsService** object provides a **send** method that can be used to send push notifications to iOS applications.</span></span> <span data-ttu-id="3f012-162">**Gönder** yöntemi aşağıdaki parametreleri kabul eder:</span><span class="sxs-lookup"><span data-stu-id="3f012-162">The **send** method accepts the following parameters:</span></span>

* <span data-ttu-id="3f012-163">**Etiketler** -etiketi tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="3f012-163">**Tags** - the tag identifier.</span></span> <span data-ttu-id="3f012-164">Hiçbir etiketi sağlanırsa, tüm istemcilere bildirim gönderilir.</span><span class="sxs-lookup"><span data-stu-id="3f012-164">If no tag is provided, the notification will be sent to all clients.</span></span>
* <span data-ttu-id="3f012-165">**Yükü** -ileti JSON veya dize yükü.</span><span class="sxs-lookup"><span data-stu-id="3f012-165">**Payload** - the message's JSON or string payload.</span></span>
* <span data-ttu-id="3f012-166">**Geri çağırma** -geri çağırma işlevi.</span><span class="sxs-lookup"><span data-stu-id="3f012-166">**Callback** - the callback function.</span></span>

<span data-ttu-id="3f012-167">Yük biçimi daha fazla bilgi için bkz: **bildirim yükü** bölümünü [yerel ve anında iletilen bildirim Programlama Kılavuzu](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) belge.</span><span class="sxs-lookup"><span data-stu-id="3f012-167">For more information the payload format, see The **Notification Payload** section of the [Local and Push Notification Programming Guide](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) document.</span></span>

<span data-ttu-id="3f012-168">Aşağıdaki kod **ApnsService** örneği kullanıma sunulan **NotificationHubService** tüm istemciler için bir uyarı iletisi göndermek için:</span><span class="sxs-lookup"><span data-stu-id="3f012-168">The following code uses the **ApnsService** instance exposed by the **NotificationHubService** to send an alert message to all clients:</span></span>

    var payload={
        alert: 'Hello!'
      };
    notificationHubService.apns.send(null, payload, function(error){
      if(!error){
         // notification sent
      }
    });

### <a name="how-to-send-push-notifications-to-windows-phone-applications"></a><span data-ttu-id="3f012-169">Nasıl yapılır: Windows Phone uygulamalarına anında iletme bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="3f012-169">How to: Send push notifications to Windows Phone applications</span></span>
<span data-ttu-id="3f012-170">**MpnsService** nesne sağlayan bir **Gönder** Windows Phone uygulamalarına anında iletme bildirimleri göndermek için kullanılan yöntem.</span><span class="sxs-lookup"><span data-stu-id="3f012-170">The **MpnsService** object provides a **send** method that can be used to send push notifications to Windows Phone applications.</span></span> <span data-ttu-id="3f012-171">**Gönder** yöntemi aşağıdaki parametreleri kabul eder:</span><span class="sxs-lookup"><span data-stu-id="3f012-171">The **send** method accepts the following parameters:</span></span>

* <span data-ttu-id="3f012-172">**Etiketler** -etiketi tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="3f012-172">**Tags** - the tag identifier.</span></span> <span data-ttu-id="3f012-173">Hiçbir etiketi sağlanırsa, tüm istemcilere bildirim gönderilir.</span><span class="sxs-lookup"><span data-stu-id="3f012-173">If no tag is provided, the notification will be sent to all clients.</span></span>
* <span data-ttu-id="3f012-174">**Yükü** -ileti XML yükü.</span><span class="sxs-lookup"><span data-stu-id="3f012-174">**Payload** - the message's XML payload.</span></span>
* <span data-ttu-id="3f012-175">**TargetName**  -  `toast` bildirimleri için.</span><span class="sxs-lookup"><span data-stu-id="3f012-175">**TargetName** - `toast` for toast notifications.</span></span> <span data-ttu-id="3f012-176">`token`Döşeme bildirimleri için.</span><span class="sxs-lookup"><span data-stu-id="3f012-176">`token` for tile notifications.</span></span>
* <span data-ttu-id="3f012-177">**NotificationClass** -bildirim önceliğini.</span><span class="sxs-lookup"><span data-stu-id="3f012-177">**NotificationClass** - The priority of the notification.</span></span> <span data-ttu-id="3f012-178">Bkz: **HTTP üstbilgi öğelerini** bölümünü [anında iletme bildirimleri bir sunucudan](http://msdn.microsoft.com/library/hh221551.aspx) belge için geçerli değerler.</span><span class="sxs-lookup"><span data-stu-id="3f012-178">See the **HTTP Header Elements** section of the [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) document for valid values.</span></span>
* <span data-ttu-id="3f012-179">**Seçenekler** - isteğe bağlı istek üstbilgileri.</span><span class="sxs-lookup"><span data-stu-id="3f012-179">**Options** - optional request headers.</span></span>
* <span data-ttu-id="3f012-180">**Geri çağırma** -geri çağırma işlevi.</span><span class="sxs-lookup"><span data-stu-id="3f012-180">**Callback** - the callback function.</span></span>

<span data-ttu-id="3f012-181">Geçerli bir listesi için **TargetName**, **NotificationClass** ve üst bilgi seçeneklerini kullanıma [anında iletme bildirimleri bir sunucudan](http://msdn.microsoft.com/library/hh221551.aspx) sayfası.</span><span class="sxs-lookup"><span data-stu-id="3f012-181">For a list of valid **TargetName**, **NotificationClass** and header options, check out the [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) page.</span></span>

<span data-ttu-id="3f012-182">Aşağıdaki örnek kod kullanır **MpnsService** örneği kullanıma sunulan **NotificationHubService** anında bildirim göndermek için:</span><span class="sxs-lookup"><span data-stu-id="3f012-182">The following sample code uses the **MpnsService** instance exposed by the **NotificationHubService** to send a toast push notification:</span></span>

    var payload = '<?xml version="1.0" encoding="utf-8"?><wp:Notification xmlns:wp="WPNotification"><wp:Toast><wp:Text1>string</wp:Text1><wp:Text2>string</wp:Text2></wp:Toast></wp:Notification>';
    notificationHubService.mpns.send(null, payload, 'toast', 22, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-to-universal-windows-platform-uwp-applications"></a><span data-ttu-id="3f012-183">Nasıl yapılır: Evrensel Windows Platformu (UWP) uygulamaları için anında iletme bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="3f012-183">How to: Send push notifications to Universal Windows Platform (UWP) applications</span></span>
<span data-ttu-id="3f012-184">**WnsService** nesne sağlayan bir **Gönder** Evrensel Windows platformu uygulamalarına anında iletme bildirimleri göndermek için kullanılan yöntem.</span><span class="sxs-lookup"><span data-stu-id="3f012-184">The **WnsService** object provides a **send** method that can be used to send push notifications to Universal Windows Platform applications.</span></span>  <span data-ttu-id="3f012-185">**Gönder** yöntemi aşağıdaki parametreleri kabul eder:</span><span class="sxs-lookup"><span data-stu-id="3f012-185">The **send** method accepts the following parameters:</span></span>

* <span data-ttu-id="3f012-186">**Etiketler** -etiketi tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="3f012-186">**Tags** - the tag identifier.</span></span> <span data-ttu-id="3f012-187">Hiçbir etiketi sağlanırsa, tüm kayıtlı istemcilere bildirim gönderilir.</span><span class="sxs-lookup"><span data-stu-id="3f012-187">If no tag is provided, the notification will be sent to all registered clients.</span></span>
* <span data-ttu-id="3f012-188">**Yükü** -XML ileti yükü.</span><span class="sxs-lookup"><span data-stu-id="3f012-188">**Payload** - the XML message payload.</span></span>
* <span data-ttu-id="3f012-189">**Tür** -bildirim türü.</span><span class="sxs-lookup"><span data-stu-id="3f012-189">**Type** - the notification type.</span></span>
* <span data-ttu-id="3f012-190">**Seçenekler** - isteğe bağlı istek üstbilgileri.</span><span class="sxs-lookup"><span data-stu-id="3f012-190">**Options** - optional request headers.</span></span>
* <span data-ttu-id="3f012-191">**Geri çağırma** -geri çağırma işlevi.</span><span class="sxs-lookup"><span data-stu-id="3f012-191">**Callback** - the callback function.</span></span>

<span data-ttu-id="3f012-192">Geçerli türler ve istek üstbilgileri listesi için bkz: [anında bildirim hizmeti istek ve yanıt üstbilgileri](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span><span class="sxs-lookup"><span data-stu-id="3f012-192">For a list of valid types and request headers, see [Push notification service request and response headers](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span></span>

<span data-ttu-id="3f012-193">Aşağıdaki kod **WnsService** örneği kullanıma sunulan **NotificationHubService** bir UWP uygulamasına anında iletme bildirim göndermek için:</span><span class="sxs-lookup"><span data-stu-id="3f012-193">The following code uses the **WnsService** instance exposed by the **NotificationHubService** to send a toast push notification to a UWP app:</span></span>

    var payload = '<toast><visual><binding template="ToastText01"><text id="1">Hello!</text></binding></visual></toast>';
    notificationHubService.wns.send(null, payload , 'wns/toast', function(error){
      if(!error){
         // notification sent
      }
    });

## <a name="next-steps"></a><span data-ttu-id="3f012-194">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="3f012-194">Next Steps</span></span>
<span data-ttu-id="3f012-195">Yukarıdaki örnek kod parçacıkları, çok çeşitli aygıtları için anında iletme bildirimleri göndermeyi hizmet altyapısı kolayca oluşturmanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="3f012-195">The sample snippets above allow you to easily build service infrastructure to deliver push notifications to a wide variety of devices.</span></span> <span data-ttu-id="3f012-196">Bildirim hub'ları node.js ile kullanma hakkında temel bilgileri öğrendiğinize göre bu özellikleri daha fazla nasıl genişletebileceğini hakkında daha fazla bilgi edinmek için aşağıdaki bağlantıları izleyin.</span><span class="sxs-lookup"><span data-stu-id="3f012-196">Now that you've learned the basics of using Notification Hubs with node.js, follow these links to learn more about how you can extend these capabilities further.</span></span>

* <span data-ttu-id="3f012-197">MSDN başvuru için bkz: [Azure Notification Hubs](https://msdn.microsoft.com/library/azure/jj927170.aspx).</span><span class="sxs-lookup"><span data-stu-id="3f012-197">See the MSDN Reference for [Azure Notification Hubs](https://msdn.microsoft.com/library/azure/jj927170.aspx).</span></span>
* <span data-ttu-id="3f012-198">Ziyaret [düğümü için Azure SDK] daha fazla örnekleri ve uygulama ayrıntıları için github'da depo.</span><span class="sxs-lookup"><span data-stu-id="3f012-198">Visit the [Azure SDK for Node] repository on GitHub for more samples and implementation details.</span></span>

<span data-ttu-id="3f012-199">[düğümü için Azure SDK]: https://github.com/WindowsAzure/azure-sdk-for-node</span><span class="sxs-lookup"><span data-stu-id="3f012-199">[Azure SDK for Node]: https://github.com/WindowsAzure/azure-sdk-for-node</span></span>
[Next Steps]: #nextsteps
[What are Service Bus Topics and Subscriptions?]: #what-are-service-bus-topics
[Create a Service Namespace]: #create-a-service-namespace
[Obtain the Default Management Credentials for the Namespace]: #obtain-default-credentials
[Create a Node.js Application]: #Create_a_Nodejs_Application
[Configure Your Application to Use Service Bus]: #Configure_Your_Application_to_Use_Service_Bus
[How to: Create a Topic]: #How_to_Create_a_Topic
[How to: Create Subscriptions]: #How_to_Create_Subscriptions
[How to: Send Messages to a Topic]: #How_to_Send_Messages_to_a_Topic
[How to: Receive Messages from a Subscription]: #How_to_Receive_Messages_from_a_Subscription
[How to: Handle Application Crashes and Unreadable Messages]: #How_to_Handle_Application_Crashes_and_Unreadable_Messages
[How to: Delete Topics and Subscriptions]: #How_to_Delete_Topics_and_Subscriptions
[1]: #Next_Steps
[Topic Concepts]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-topics-01.png
[Azure Classic Portal]: http://manage.windowsazure.com
[image]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-03.png
[2]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-04.png
[3]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-05.png
[4]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-06.png
[5]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/sb-queues-07.png
[SqlFilter.SqlExpression]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.sqlexpression.aspx
[Azure Service Bus Notification Hubs]: http://msdn.microsoft.com/library/windowsazure/jj927170.aspx
[SqlFilter]: http://msdn.microsoft.com/library/windowsazure/microsoft.servicebus.messaging.sqlfilter.aspx
<span data-ttu-id="3f012-200">[Web sitesini WebMatrix ile]: /develop/nodejs/tutorials/web-site-with-webmatrix/</span><span class="sxs-lookup"><span data-stu-id="3f012-200">[Web Site with WebMatrix]: /develop/nodejs/tutorials/web-site-with-webmatrix/</span></span>
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Previous Management Portal]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/previous-portal.png
[nodejswebsite]: /develop/nodejs/tutorials/create-a-website-(mac)/
[Node.js Cloud Service with Storage]: /develop/nodejs/tutorials/web-app-with-storage/
[Node.js Web Application with Storage]: /develop/nodejs/tutorials/web-site-with-storage/
<span data-ttu-id="3f012-201">[Azure Portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="3f012-201">[Azure Portal]: https://portal.azure.com</span></span>
