---
title: "Azure bildirim hub'ları ve Node.js ile aaaSending anında iletme bildirimleri"
description: "Nasıl toouse bildirim hub'ları toosend anında iletme bildirimleri bir Node.js uygulamasından öğrenin."
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
ms.openlocfilehash: 151d224fa6dd07e4acdc3a4887c4e95ee03168c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="sending-push-notifications-with-azure-notification-hubs-and-nodejs"></a><span data-ttu-id="eca90-104">Azure bildirim hub'ları ve Node.js ile anında iletme bildirimleri gönderme</span><span class="sxs-lookup"><span data-stu-id="eca90-104">Sending push notifications with Azure Notification Hubs and Node.js</span></span>
[!INCLUDE [notification-hubs-backend-how-to-selector](../../includes/notification-hubs-backend-how-to-selector.md)]

## <a name="overview"></a><span data-ttu-id="eca90-105">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="eca90-105">Overview</span></span>
> [!IMPORTANT]
> <span data-ttu-id="eca90-106">toocomplete Bu öğretici, etkin bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="eca90-106">toocomplete this tutorial, you must have an active Azure account.</span></span> <span data-ttu-id="eca90-107">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eca90-107">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="eca90-108">Ayrıntılı bilgi için bkz. [Azure Ücretsiz Deneme Sürümü](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).</span><span class="sxs-lookup"><span data-stu-id="eca90-108">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A643EE910&amp;returnurl=http%3A%2F%2Fazure.microsoft.com%2Fen-us%2Fdocumentation%2Farticles%2Fnotification-hubs-nodejs-how-to-use-notification-hubs).</span></span>
> 
> 

<span data-ttu-id="eca90-109">Bu kılavuz size nasıl toosend anında iletme bildirimleri hello Yardım Azure bildirim hub'larını doğrudan bir Node.js uygulamasından gösterir.</span><span class="sxs-lookup"><span data-stu-id="eca90-109">This guide will show you how toosend push notifications with hello help of Azure Notification Hubs directly from a Node.js application.</span></span> 

<span data-ttu-id="eca90-110">anında iletme bildirimleri tooapplications platformlar aşağıdaki hello üzerinde gönderme kapsamdaki hello senaryolar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="eca90-110">hello scenarios covered include sending push notifications tooapplications on hello following platforms:</span></span>

* <span data-ttu-id="eca90-111">Android</span><span class="sxs-lookup"><span data-stu-id="eca90-111">Android</span></span>
* <span data-ttu-id="eca90-112">iOS</span><span class="sxs-lookup"><span data-stu-id="eca90-112">iOS</span></span>
* <span data-ttu-id="eca90-113">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="eca90-113">Windows Phone</span></span>
* <span data-ttu-id="eca90-114">Evrensel Windows platformu</span><span class="sxs-lookup"><span data-stu-id="eca90-114">Universal Windows Platform</span></span> 

<span data-ttu-id="eca90-115">Bildirim hub'ları hakkında daha fazla bilgi için bkz: Merhaba [sonraki adımlar](#next) bölümü.</span><span class="sxs-lookup"><span data-stu-id="eca90-115">For more information on notification hubs, see hello [Next Steps](#next) section.</span></span>

## <a name="what-are-notification-hubs"></a><span data-ttu-id="eca90-116">Bildirim Hub'ları nedir?</span><span class="sxs-lookup"><span data-stu-id="eca90-116">What are Notification Hubs?</span></span>
<span data-ttu-id="eca90-117">Azure bildirim hub'ları, anında iletme bildirimleri toomobile aygıtları göndermek için kullanımı kolay, çok platformlu, ölçeklenebilir bir altyapı sunar.</span><span class="sxs-lookup"><span data-stu-id="eca90-117">Azure Notification Hubs provide an easy-to-use, multi-platform, scalable infrastructure for sending push notifications toomobile devices.</span></span> <span data-ttu-id="eca90-118">Merhaba hello hizmet altyapısı hakkında daha fazla bilgi için bkz: [Azure Notification Hubs](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) sayfası.</span><span class="sxs-lookup"><span data-stu-id="eca90-118">For details on hello service infrastructure, see hello [Azure Notification Hubs](http://msdn.microsoft.com/library/windowsazure/jj927170.aspx) page.</span></span>

## <a name="create-a-nodejs-application"></a><span data-ttu-id="eca90-119">Bir Node.js uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="eca90-119">Create a Node.js Application</span></span>
<span data-ttu-id="eca90-120">Bu öğreticide Hello ilk adımı, yeni ve boş bir Node.js uygulaması oluşturmaktır.</span><span class="sxs-lookup"><span data-stu-id="eca90-120">hello first step in this tutorial is creating a new blank Node.js application.</span></span> <span data-ttu-id="eca90-121">Bir Node.js uygulaması oluşturma ile ilgili yönergeler için bkz: [oluşturma ve bir Node.js uygulaması tooAzure Web sitesi dağıtma][nodejswebsite], [Node.js bulut hizmeti] [ Node.js Cloud Service] Windows PowerShell kullanarak veya [Web sitesini WebMatrix ile].</span><span class="sxs-lookup"><span data-stu-id="eca90-121">For instructions on creating a Node.js application, see [Create and deploy a Node.js application tooAzure Web Site][nodejswebsite], [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell, or [Web Site with WebMatrix].</span></span>

## <a name="configure-your-application-toouse-notification-hubs"></a><span data-ttu-id="eca90-122">Uygulamanızı tooUse bildirim hub'ları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="eca90-122">Configure Your Application tooUse Notification Hubs</span></span>
<span data-ttu-id="eca90-123">Azure Notification Hubs toouse, gereksinim duyduğunuz toodownload ve kullanım hello Node.js [azure paketi](https://www.npmjs.com/package/azure), hello anında iletme bildirimi REST Hizmetleri ile iletişim yardımcı kitaplıklar yerleşik bir kümesini içerir.</span><span class="sxs-lookup"><span data-stu-id="eca90-123">toouse Azure Notification Hubs, you need toodownload and use hello Node.js [azure package](https://www.npmjs.com/package/azure), which includes a built-in set of helper libraries that communicate with hello push notification REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="eca90-124">Düğüm paketi Yöneticisi (NPM) tooobtain hello paketini kullanın</span><span class="sxs-lookup"><span data-stu-id="eca90-124">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="eca90-125">Bir komut satırı arabirimi gibi kullandığınız **PowerShell** (Windows), **Terminal** (Mac) veya **Bash** (Linux) ve boş uygulamanızı oluşturulduğu toohello klasörüne gidin .</span><span class="sxs-lookup"><span data-stu-id="eca90-125">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Linux) and navigate toohello folder where you created your blank application.</span></span>
2. <span data-ttu-id="eca90-126">Tür **npm yükleme azure sb** hello komut penceresinde.</span><span class="sxs-lookup"><span data-stu-id="eca90-126">Type **npm install azure-sb** in hello command window.</span></span>
3. <span data-ttu-id="eca90-127">Merhaba el ile çalıştırabilirsiniz **ls** veya **dir** komutu tooverify, bir **düğümü\_modülleri** klasörü oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="eca90-127">You can manually run hello **ls** or **dir** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="eca90-128">Bu klasör içinde hello bulur **azure** tooaccess ihtiyacınız hello kitaplıklarını içeren paket hello bildirim hub'ı.</span><span class="sxs-lookup"><span data-stu-id="eca90-128">Inside that folder, find hello **azure** package, which contains hello libraries you need tooaccess hello Notification Hub.</span></span>

> [!NOTE]
> <span data-ttu-id="eca90-129">Merhaba resmi üzerinde NPM yükleme hakkında daha fazla bilgi edinebilirsiniz [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm).</span><span class="sxs-lookup"><span data-stu-id="eca90-129">You can learn more about installing NPM on hello official [NPM blog](http://blog.npmjs.org/post/85484771375/how-to-install-npm).</span></span> 
> 
> 

### <a name="import-hello-module"></a><span data-ttu-id="eca90-130">İçeri aktarma hello Modülü</span><span class="sxs-lookup"><span data-stu-id="eca90-130">Import hello module</span></span>
<span data-ttu-id="eca90-131">Bir metin düzenleyicisi kullanarak eklemek hello toohello üstündeki aşağıdaki hello **server.js** hello uygulama dosyası:</span><span class="sxs-lookup"><span data-stu-id="eca90-131">Using a text editor, add hello following toohello top of hello **server.js** file of hello application:</span></span>

    var azure = require('azure');

### <a name="setup-an-azure-notification-hub-connection"></a><span data-ttu-id="eca90-132">Azure bildirim hub'ı bağlantısı kurma</span><span class="sxs-lookup"><span data-stu-id="eca90-132">Setup an Azure Notification Hub connection</span></span>
<span data-ttu-id="eca90-133">Merhaba **NotificationHubService** nesne notification hubs ile çalışmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="eca90-133">hello **NotificationHubService** object lets you work with notification hubs.</span></span> <span data-ttu-id="eca90-134">Merhaba aşağıdaki kod oluşturur bir **NotificationHubService** hello nofication hub'ı adlı nesne **hubname**.</span><span class="sxs-lookup"><span data-stu-id="eca90-134">hello following code creates a **NotificationHubService** object for hello nofication hub named **hubname**.</span></span> <span data-ttu-id="eca90-135">Merhaba hello yukarıya yakın eklemek **server.js** hello deyimi tooimport hello azure modülü sonra dosyayı:</span><span class="sxs-lookup"><span data-stu-id="eca90-135">Add it near hello top of hello **server.js** file, after hello statement tooimport hello azure module:</span></span>

    var notificationHubService = azure.createNotificationHubService('hubname','connectionstring');

<span data-ttu-id="eca90-136">Merhaba bağlantı **connectionstring** değeri hello elde edilebilir [Azure Portal] hello aşağıdaki adımları gerçekleştirerek:</span><span class="sxs-lookup"><span data-stu-id="eca90-136">hello connection **connectionstring** value can be obtained from hello [Azure Portal] by performing hello following steps:</span></span>

1. <span data-ttu-id="eca90-137">Merhaba sol gezinti bölmesinde **Gözat**.</span><span class="sxs-lookup"><span data-stu-id="eca90-137">In hello left navigation pane, click **Browse**.</span></span>
2. <span data-ttu-id="eca90-138">Seçin **bildirim hub'ları**ve ardından Bul hello hub hello örnek toouse istiyor.</span><span class="sxs-lookup"><span data-stu-id="eca90-138">Select **Notification Hubs**, and then find hello hub you wish toouse for hello sample.</span></span> <span data-ttu-id="eca90-139">Toohello başvurabilir [Windows mağazası Başlarken Öğreticisi](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) yeni bir bildirim hub'ı oluşturma yardıma gereksinim duyarsanız.</span><span class="sxs-lookup"><span data-stu-id="eca90-139">You can refer toohello [Windows Store Getting Started tutorial](notification-hubs-windows-store-dotnet-get-started-wns-push-notification.md) if you need help creating a new Notification Hub.</span></span>
3. <span data-ttu-id="eca90-140">Seçin **ayarları**.</span><span class="sxs-lookup"><span data-stu-id="eca90-140">Select **Settings**.</span></span>
4. <span data-ttu-id="eca90-141">Tıklayın **erişim ilkeleri**.</span><span class="sxs-lookup"><span data-stu-id="eca90-141">Click on **Access Policies**.</span></span> <span data-ttu-id="eca90-142">Her iki paylaşılan ve tam erişim bağlantı dizeleri görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="eca90-142">You will see both shared and full access connection strings.</span></span>

![Azure Portal - bildirim hub'ları](./media/notification-hubs-nodejs-how-to-use-notification-hubs/notification-hubs-portal.png)

> [!NOTE]
> <span data-ttu-id="eca90-144">Hello kullanarak hello bağlantı dizesini de alabilirsiniz **Get-AzureSbNamespace** tarafından sağlanan cmdlet [Azure PowerShell](/powershell/azureps-cmdlets-docs) veya hello **azure sb ad alanı göster** komutunu Merhaba [Azure komut satırı arabirimi (Azure CLI)](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="eca90-144">You can also retrieve hello connection string using hello **Get-AzureSbNamespace** cmdlet provided by [Azure PowerShell](/powershell/azureps-cmdlets-docs) or hello **azure sb namespace show** command with hello [Azure Command-Line Interface (Azure CLI)](../cli-install-nodejs.md).</span></span>
> 
> 

## <a name="general-architecture"></a><span data-ttu-id="eca90-145">Genel mimari</span><span class="sxs-lookup"><span data-stu-id="eca90-145">General architecture</span></span>
<span data-ttu-id="eca90-146">Merhaba **NotificationHubService** nesne anında iletme bildirimleri toospecific cihazları ve uygulamaları göndermek için nesne örnekleri aşağıdaki hello gösterir:</span><span class="sxs-lookup"><span data-stu-id="eca90-146">hello **NotificationHubService** object exposes hello following object instances for sending push notifications toospecific devices and applications:</span></span>

* <span data-ttu-id="eca90-147">**Android** -hello kullan **GcmService** şu adresten edinilebilir nesne **notificationHubService.gcm**</span><span class="sxs-lookup"><span data-stu-id="eca90-147">**Android** - use hello **GcmService** object, which is available at **notificationHubService.gcm**</span></span>
* <span data-ttu-id="eca90-148">**iOS** -hello kullan **ApnsService** adresindeki erişilebilir olan nesne, **notificationHubService.apns**</span><span class="sxs-lookup"><span data-stu-id="eca90-148">**iOS** - use hello **ApnsService** object, which is accessible at **notificationHubService.apns**</span></span>
* <span data-ttu-id="eca90-149">**Windows Phone** -hello kullan **MpnsService** şu adresten edinilebilir nesne **notificationHubService.mpns**</span><span class="sxs-lookup"><span data-stu-id="eca90-149">**Windows Phone** - use hello **MpnsService** object, which is available at **notificationHubService.mpns**</span></span>
* <span data-ttu-id="eca90-150">**Evrensel Windows platformu** -hello kullan **WnsService** şu adresten edinilebilir nesne **notificationHubService.wns**</span><span class="sxs-lookup"><span data-stu-id="eca90-150">**Universal Windows Platform** - use hello **WnsService** object, which is available at **notificationHubService.wns**</span></span>

### <a name="how-to-send-push-notifications-tooandroid-applications"></a><span data-ttu-id="eca90-151">Nasıl yapılır: anında iletme bildirimleri tooAndroid uygulamaları gönderir</span><span class="sxs-lookup"><span data-stu-id="eca90-151">How to: Send push notifications tooAndroid applications</span></span>
<span data-ttu-id="eca90-152">Merhaba **GcmService** nesnesi sağlar bir **Gönder** kullanılan toosend anında iletme bildirimleri tooAndroid uygulamaları kullanılabilecek yöntemi.</span><span class="sxs-lookup"><span data-stu-id="eca90-152">hello **GcmService** object provides a **send** method that can be used toosend push notifications tooAndroid applications.</span></span> <span data-ttu-id="eca90-153">Merhaba **Gönder** yöntemi şu parametreler hello kabul eder:</span><span class="sxs-lookup"><span data-stu-id="eca90-153">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="eca90-154">**Etiketler** -etiketi tanımlayıcı hello.</span><span class="sxs-lookup"><span data-stu-id="eca90-154">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="eca90-155">Hiçbir etiketi sağlanırsa, tooall istemcileri hello bildirim gönderilir.</span><span class="sxs-lookup"><span data-stu-id="eca90-155">If no tag is provided, hello notification will be sent tooall clients.</span></span>
* <span data-ttu-id="eca90-156">**Yükü** -ileti JSON veya ham dize yükü hello.</span><span class="sxs-lookup"><span data-stu-id="eca90-156">**Payload** - hello message's JSON or raw string payload.</span></span>
* <span data-ttu-id="eca90-157">**Geri çağırma** -hello geri çağırma işlevi.</span><span class="sxs-lookup"><span data-stu-id="eca90-157">**Callback** - hello callback function.</span></span>

<span data-ttu-id="eca90-158">Merhaba hello yük biçimi hakkında daha fazla bilgi için bkz: **yükü** hello bölümünü [uygulama GCM Server](http://developer.android.com/google/gcm/server.html#payload) belge.</span><span class="sxs-lookup"><span data-stu-id="eca90-158">For more information on hello payload format, see hello **Payload** section of hello [Implementing GCM Server](http://developer.android.com/google/gcm/server.html#payload) document.</span></span>

<span data-ttu-id="eca90-159">Merhaba aşağıdaki kod kullanır hello **GcmService** hello tarafından kullanıma sunulan örneği **NotificationHubService** toosend anında iletme bildirimi tooall istemciler kayıtlı.</span><span class="sxs-lookup"><span data-stu-id="eca90-159">hello following code uses hello **GcmService** instance exposed by hello **NotificationHubService** toosend a push notification tooall registered clients.</span></span>

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

### <a name="how-to-send-push-notifications-tooios-applications"></a><span data-ttu-id="eca90-160">Nasıl yapılır: anında iletme bildirimleri tooiOS uygulamaları gönderir</span><span class="sxs-lookup"><span data-stu-id="eca90-160">How to: Send push notifications tooiOS applications</span></span>
<span data-ttu-id="eca90-161">Yukarıda açıklanan Android uygulamalarında olduğu gibi aynı hello **ApnsService** nesnesi sağlar bir **Gönder** kullanılan toosend anında iletme bildirimleri tooiOS uygulamaları kullanılabilecek yöntemi.</span><span class="sxs-lookup"><span data-stu-id="eca90-161">Same as with Android applications described above, hello **ApnsService** object provides a **send** method that can be used toosend push notifications tooiOS applications.</span></span> <span data-ttu-id="eca90-162">Merhaba **Gönder** yöntemi şu parametreler hello kabul eder:</span><span class="sxs-lookup"><span data-stu-id="eca90-162">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="eca90-163">**Etiketler** -etiketi tanımlayıcı hello.</span><span class="sxs-lookup"><span data-stu-id="eca90-163">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="eca90-164">Hiçbir etiketi sağlanırsa, tooall istemcileri hello bildirim gönderilir.</span><span class="sxs-lookup"><span data-stu-id="eca90-164">If no tag is provided, hello notification will be sent tooall clients.</span></span>
* <span data-ttu-id="eca90-165">**Yükü** - ileti JSON hello veya dize yükü.</span><span class="sxs-lookup"><span data-stu-id="eca90-165">**Payload** - hello message's JSON or string payload.</span></span>
* <span data-ttu-id="eca90-166">**Geri çağırma** -hello geri çağırma işlevi.</span><span class="sxs-lookup"><span data-stu-id="eca90-166">**Callback** - hello callback function.</span></span>

<span data-ttu-id="eca90-167">Daha fazla bilgi hello yük biçimi için hello bkz **bildirim yükü** hello bölümünü [yerel ve anında iletilen bildirim Programlama Kılavuzu](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) belge.</span><span class="sxs-lookup"><span data-stu-id="eca90-167">For more information hello payload format, see hello **Notification Payload** section of hello [Local and Push Notification Programming Guide](http://developer.apple.com/library/ios/#documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/ApplePushService/ApplePushService.html) document.</span></span>

<span data-ttu-id="eca90-168">Merhaba aşağıdaki kod kullanır hello **ApnsService** hello tarafından kullanıma sunulan örneği **NotificationHubService** toosend bir uyarı iletisi tooall istemciler:</span><span class="sxs-lookup"><span data-stu-id="eca90-168">hello following code uses hello **ApnsService** instance exposed by hello **NotificationHubService** toosend an alert message tooall clients:</span></span>

    var payload={
        alert: 'Hello!'
      };
    notificationHubService.apns.send(null, payload, function(error){
      if(!error){
         // notification sent
      }
    });

### <a name="how-to-send-push-notifications-toowindows-phone-applications"></a><span data-ttu-id="eca90-169">Nasıl yapılır: anında iletme bildirimleri tooWindows Phone uygulamaları Gönder</span><span class="sxs-lookup"><span data-stu-id="eca90-169">How to: Send push notifications tooWindows Phone applications</span></span>
<span data-ttu-id="eca90-170">Merhaba **MpnsService** nesne sağlayan bir **Gönder** kullanılan toosend anında iletme bildirimleri tooWindows Phone uygulamaları olabilir yöntemi.</span><span class="sxs-lookup"><span data-stu-id="eca90-170">hello **MpnsService** object provides a **send** method that can be used toosend push notifications tooWindows Phone applications.</span></span> <span data-ttu-id="eca90-171">Merhaba **Gönder** yöntemi şu parametreler hello kabul eder:</span><span class="sxs-lookup"><span data-stu-id="eca90-171">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="eca90-172">**Etiketler** -etiketi tanımlayıcı hello.</span><span class="sxs-lookup"><span data-stu-id="eca90-172">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="eca90-173">Hiçbir etiketi sağlanırsa, tooall istemcileri hello bildirim gönderilir.</span><span class="sxs-lookup"><span data-stu-id="eca90-173">If no tag is provided, hello notification will be sent tooall clients.</span></span>
* <span data-ttu-id="eca90-174">**Yükü** -ileti XML yükü hello.</span><span class="sxs-lookup"><span data-stu-id="eca90-174">**Payload** - hello message's XML payload.</span></span>
* <span data-ttu-id="eca90-175">**TargetName**  -  `toast` bildirimleri için.</span><span class="sxs-lookup"><span data-stu-id="eca90-175">**TargetName** - `toast` for toast notifications.</span></span> <span data-ttu-id="eca90-176">`token`Döşeme bildirimleri için.</span><span class="sxs-lookup"><span data-stu-id="eca90-176">`token` for tile notifications.</span></span>
* <span data-ttu-id="eca90-177">**NotificationClass** -hello hello bildirim önceliğini.</span><span class="sxs-lookup"><span data-stu-id="eca90-177">**NotificationClass** - hello priority of hello notification.</span></span> <span data-ttu-id="eca90-178">Merhaba bkz **HTTP üstbilgi öğelerini** hello bölümünü [anında iletme bildirimleri bir sunucudan](http://msdn.microsoft.com/library/hh221551.aspx) belge için geçerli değerler.</span><span class="sxs-lookup"><span data-stu-id="eca90-178">See hello **HTTP Header Elements** section of hello [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) document for valid values.</span></span>
* <span data-ttu-id="eca90-179">**Seçenekler** - isteğe bağlı istek üstbilgileri.</span><span class="sxs-lookup"><span data-stu-id="eca90-179">**Options** - optional request headers.</span></span>
* <span data-ttu-id="eca90-180">**Geri çağırma** -hello geri çağırma işlevi.</span><span class="sxs-lookup"><span data-stu-id="eca90-180">**Callback** - hello callback function.</span></span>

<span data-ttu-id="eca90-181">Geçerli bir listesi için **TargetName**, **NotificationClass** ve başlık seçeneklerini denetleme hello [anında iletme bildirimleri bir sunucudan](http://msdn.microsoft.com/library/hh221551.aspx) sayfası.</span><span class="sxs-lookup"><span data-stu-id="eca90-181">For a list of valid **TargetName**, **NotificationClass** and header options, check out hello [Push notifications from a server](http://msdn.microsoft.com/library/hh221551.aspx) page.</span></span>

<span data-ttu-id="eca90-182">Aşağıdaki örnek kod hello kullanan hello **MpnsService** hello tarafından kullanıma sunulan örneği **NotificationHubService** toosend anında bildirim:</span><span class="sxs-lookup"><span data-stu-id="eca90-182">hello following sample code uses hello **MpnsService** instance exposed by hello **NotificationHubService** toosend a toast push notification:</span></span>

    var payload = '<?xml version="1.0" encoding="utf-8"?><wp:Notification xmlns:wp="WPNotification"><wp:Toast><wp:Text1>string</wp:Text1><wp:Text2>string</wp:Text2></wp:Toast></wp:Notification>';
    notificationHubService.mpns.send(null, payload, 'toast', 22, function(error){
      if(!error){
        //notification sent
      }
    });

### <a name="how-to-send-push-notifications-toouniversal-windows-platform-uwp-applications"></a><span data-ttu-id="eca90-183">Nasıl yapılır: anında iletme bildirimleri tooUniversal Windows Platformu (UWP) uygulamaları gönderir</span><span class="sxs-lookup"><span data-stu-id="eca90-183">How to: Send push notifications tooUniversal Windows Platform (UWP) applications</span></span>
<span data-ttu-id="eca90-184">Merhaba **WnsService** nesne sağlayan bir **Gönder** kullanılan toosend anında iletme bildirimleri tooUniversal Windows platformu uygulamaları kullanılabilecek yöntemi.</span><span class="sxs-lookup"><span data-stu-id="eca90-184">hello **WnsService** object provides a **send** method that can be used toosend push notifications tooUniversal Windows Platform applications.</span></span>  <span data-ttu-id="eca90-185">Merhaba **Gönder** yöntemi şu parametreler hello kabul eder:</span><span class="sxs-lookup"><span data-stu-id="eca90-185">hello **send** method accepts hello following parameters:</span></span>

* <span data-ttu-id="eca90-186">**Etiketler** -etiketi tanımlayıcı hello.</span><span class="sxs-lookup"><span data-stu-id="eca90-186">**Tags** - hello tag identifier.</span></span> <span data-ttu-id="eca90-187">Hiçbir etiketi sağlanırsa, kayıtlı tooall istemcileri hello bildirim gönderilir.</span><span class="sxs-lookup"><span data-stu-id="eca90-187">If no tag is provided, hello notification will be sent tooall registered clients.</span></span>
* <span data-ttu-id="eca90-188">**Yükü** -hello XML ileti yükü.</span><span class="sxs-lookup"><span data-stu-id="eca90-188">**Payload** - hello XML message payload.</span></span>
* <span data-ttu-id="eca90-189">**Tür** -hello bildirim türü.</span><span class="sxs-lookup"><span data-stu-id="eca90-189">**Type** - hello notification type.</span></span>
* <span data-ttu-id="eca90-190">**Seçenekler** - isteğe bağlı istek üstbilgileri.</span><span class="sxs-lookup"><span data-stu-id="eca90-190">**Options** - optional request headers.</span></span>
* <span data-ttu-id="eca90-191">**Geri çağırma** -hello geri çağırma işlevi.</span><span class="sxs-lookup"><span data-stu-id="eca90-191">**Callback** - hello callback function.</span></span>

<span data-ttu-id="eca90-192">Geçerli türler ve istek üstbilgileri listesi için bkz: [anında bildirim hizmeti istek ve yanıt üstbilgileri](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span><span class="sxs-lookup"><span data-stu-id="eca90-192">For a list of valid types and request headers, see [Push notification service request and response headers](http://msdn.microsoft.com/library/windows/apps/hh465435.aspx).</span></span>

<span data-ttu-id="eca90-193">Merhaba aşağıdaki kod kullanır hello **WnsService** hello tarafından kullanıma sunulan örneği **NotificationHubService** toosend bir bildirim anında iletme bildirimi tooa UWP uygulaması:</span><span class="sxs-lookup"><span data-stu-id="eca90-193">hello following code uses hello **WnsService** instance exposed by hello **NotificationHubService** toosend a toast push notification tooa UWP app:</span></span>

    var payload = '<toast><visual><binding template="ToastText01"><text id="1">Hello!</text></binding></visual></toast>';
    notificationHubService.wns.send(null, payload , 'wns/toast', function(error){
      if(!error){
         // notification sent
      }
    });

## <a name="next-steps"></a><span data-ttu-id="eca90-194">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="eca90-194">Next Steps</span></span>
<span data-ttu-id="eca90-195">Merhaba örnek parçacıkları yukarıdaki, tooeasily yapı hizmeti altyapı toodeliver anında iletme bildirimleri tooa çeşitli aygıtlar izin verir.</span><span class="sxs-lookup"><span data-stu-id="eca90-195">hello sample snippets above allow you tooeasily build service infrastructure toodeliver push notifications tooa wide variety of devices.</span></span> <span data-ttu-id="eca90-196">Node.js ile bildirim hub'ları kullanarak hello temellerini öğrendiğinize göre bu özellikleri daha fazla nasıl genişletebileceğini hakkında daha fazla bu bağlantılar toolearn izleyin.</span><span class="sxs-lookup"><span data-stu-id="eca90-196">Now that you've learned hello basics of using Notification Hubs with node.js, follow these links toolearn more about how you can extend these capabilities further.</span></span>

* <span data-ttu-id="eca90-197">Bkz. MSDN başvurusunu hello [Azure Notification Hubs](https://msdn.microsoft.com/library/azure/jj927170.aspx).</span><span class="sxs-lookup"><span data-stu-id="eca90-197">See hello MSDN Reference for [Azure Notification Hubs](https://msdn.microsoft.com/library/azure/jj927170.aspx).</span></span>
* <span data-ttu-id="eca90-198">Merhaba ziyaret [düğümü için Azure SDK] daha fazla örnekleri ve uygulama ayrıntıları için github'da depo.</span><span class="sxs-lookup"><span data-stu-id="eca90-198">Visit hello [Azure SDK for Node] repository on GitHub for more samples and implementation details.</span></span>

[düğümü için Azure SDK]: https://github.com/WindowsAzure/azure-sdk-for-node
[Next Steps]: #nextsteps
[What are Service Bus Topics and Subscriptions?]: #what-are-service-bus-topics
[Create a Service Namespace]: #create-a-service-namespace
[Obtain hello Default Management Credentials for hello Namespace]: #obtain-default-credentials
[Create a Node.js Application]: #Create_a_Nodejs_Application
[Configure Your Application tooUse Service Bus]: #Configure_Your_Application_to_Use_Service_Bus
[How to: Create a Topic]: #How_to_Create_a_Topic
[How to: Create Subscriptions]: #How_to_Create_Subscriptions
[How to: Send Messages tooa Topic]: #How_to_Send_Messages_to_a_Topic
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
[Web sitesini WebMatrix ile]: /develop/nodejs/tutorials/web-site-with-webmatrix/
[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Previous Management Portal]: .media/notification-hubs-nodejs-how-to-use-notification-hubs/previous-portal.png
[nodejswebsite]: /develop/nodejs/tutorials/create-a-website-(mac)/
[Node.js Cloud Service with Storage]: /develop/nodejs/tutorials/web-app-with-storage/
[Node.js Web Application with Storage]: /develop/nodejs/tutorials/web-site-with-storage/
[Azure Portal]: https://portal.azure.com
