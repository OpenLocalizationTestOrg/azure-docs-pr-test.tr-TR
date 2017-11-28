---
title: "aaaCreate Azure App Service'te Socket.IO ile bir Node.js sohbet uygulaması"
description: "Öğretici, Azure üzerinde barındırılan bir node.js web uygulamasında Socket.IO kullanmayı gösterir."
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: c4c4af36-3ecf-4619-b586-ca90d53ce35b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 3bd7867ccc297dc0a21c7a00cc9db06358877f5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-chat-application-with-socketio-in-azure-app-service"></a><span data-ttu-id="27b8e-103">Azure App Service’te Socket.IO ile bir Node.js sohbet uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="27b8e-103">Create a Node.js chat application with Socket.IO in Azure App Service</span></span>
<span data-ttu-id="27b8e-104">Socket.IO WebSockets kullanan istemciler ve node.js sunucu arasında gerçek zamanlı iletişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="27b8e-104">Socket.IO provides real-time communication between your node.js server and clients using WebSockets.</span></span> <span data-ttu-id="27b8e-105">Eski tarayıcıyla iş geri dönüş tooother taşımaları (örneğin, uzun yoklama) da destekler.</span><span class="sxs-lookup"><span data-stu-id="27b8e-105">It also supports fallback tooother transports (such as long polling) that work with older browsers.</span></span> <span data-ttu-id="27b8e-106">Bu öğretici bir temel Socket.IO sohbet uygulaması Azure web uygulaması olarak barındırma aracılığıyla yol ve nasıl tooscale hello kullanarak uygulama Göster [Azure Redis önbelleği].</span><span class="sxs-lookup"><span data-stu-id="27b8e-106">This tutorial will walk you through hosting a Socket.IO based chat application as an Azure web app, and show you how tooscale hello application using [Azure Redis Cache].</span></span> <span data-ttu-id="27b8e-107">Socket.IO ile ilgili daha fazla bilgi için bkz: <http://socket.io/>.</span><span class="sxs-lookup"><span data-stu-id="27b8e-107">For more information on Socket.IO, see <http://socket.io/>.</span></span>

> [!NOTE]
> <span data-ttu-id="27b8e-108">Bu görevde Hello yordamları uygulamak çok[App Service Web Apps]; bulut Hizmetleri için bkz: [bir Node.js sohbet uygulaması Socket.IO ile bir Azure bulut hizmeti oluşturma].</span><span class="sxs-lookup"><span data-stu-id="27b8e-108">hello procedures in this task apply too[App Service Web Apps]; for Cloud Services, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>
> 
> 

## <a name="download-hello-chat-example"></a><span data-ttu-id="27b8e-109">Merhaba sohbet örneği indirin</span><span class="sxs-lookup"><span data-stu-id="27b8e-109">Download hello chat example</span></span>
<span data-ttu-id="27b8e-110">Bu proje için hello sohbet hello örnekten kullanacağız [Socket.IO GitHub deposunu].</span><span class="sxs-lookup"><span data-stu-id="27b8e-110">For this project, we will use hello chat example from hello [Socket.IO GitHub repository].</span></span> <span data-ttu-id="27b8e-111">Aşağıdaki adımları toodownload hello örneğine hello gerçekleştirmek ve daha önce oluşturduğunuz toohello proje ekleyin.</span><span class="sxs-lookup"><span data-stu-id="27b8e-111">Perform hello following steps toodownload hello example and add it toohello project you previously created.</span></span>

1. <span data-ttu-id="27b8e-112">Karşıdan bir [ZIP veya GZ Arşivlenen Sürüm] hello Socket.IO projesinin (sürüm 1.3.5 için bu belgenin kullanıldı)</span><span class="sxs-lookup"><span data-stu-id="27b8e-112">Download a [ZIP or GZ archived release] of hello Socket.IO project (version 1.3.5 was used for this document)</span></span>
2. <span data-ttu-id="27b8e-113">Merhaba Arşiv ve kopyalama hello ayıklamak **örnekler\\sohbet** dizin tooa yeni konumu.</span><span class="sxs-lookup"><span data-stu-id="27b8e-113">Extract hello archive and copy hello **examples\\chat** directory tooa new location.</span></span> <span data-ttu-id="27b8e-114">Örneğin,  **\\düğümü\\sohbet**.</span><span class="sxs-lookup"><span data-stu-id="27b8e-114">For example, **\\node\\chat**.</span></span>

## <a name="modify-appjs-and-install-modules"></a><span data-ttu-id="27b8e-115">App.js'yi değiştirme ve modülleri yükleme</span><span class="sxs-lookup"><span data-stu-id="27b8e-115">Modify app.js and install modules</span></span>
1. <span data-ttu-id="27b8e-116">Merhaba yeniden adlandırma **index.js** çok dosya**app.js**.</span><span class="sxs-lookup"><span data-stu-id="27b8e-116">Rename hello **index.js** file too**app.js**.</span></span> <span data-ttu-id="27b8e-117">Bu, Azure toodetect bir Node.js uygulaması budur sağlar.</span><span class="sxs-lookup"><span data-stu-id="27b8e-117">This allows Azure toodetect that this is a Node.js application.</span></span>
2. <span data-ttu-id="27b8e-118">Açık hello **app.js** dosyasını bir metin düzenleyicisinde.</span><span class="sxs-lookup"><span data-stu-id="27b8e-118">Open hello **app.js** file in a text editor.</span></span> <span data-ttu-id="27b8e-119">Değişiklik hello satırını içeren `var io = require('../..')(server);` aşağıda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="27b8e-119">Change hello line containing `var io = require('../..')(server);` as shown below:</span></span>
   
       var express = require('express');
       var app = express();
       var server = require('http').createServer(app);
       // var io = require('../..')(server);
       // New:
       var io = require('socket.io')(server);
       var port = process.env.PORT || 3000;
3. <span data-ttu-id="27b8e-120">Açık hello **package.json** dosyası ve bir başvuru toosocket.io altında ekleyin `dependencies`, aşağıda gösterildiği gibi:</span><span class="sxs-lookup"><span data-stu-id="27b8e-120">Open hello **package.json** file and add a reference toosocket.io under `dependencies`, as shown below:</span></span>
   
        "dependencies": {
          "express": "3.4.8",
          "socket.io": "1.3.5"
        }
4. <span data-ttu-id="27b8e-121">Komut satırı Hello toohello değiştirme  **\\düğümü\\sohbet** bu uygulama tarafından istenen dizin ve kullanım npm tooinstall hello modülleri:</span><span class="sxs-lookup"><span data-stu-id="27b8e-121">From hello command-line, change toohello **\\node\\chat** directory and use npm tooinstall hello modules required by this application:</span></span>
   
        npm install
   
    <span data-ttu-id="27b8e-122">Bu hello modülleri adlı bir alt klasöre yükler **node_modules**.</span><span class="sxs-lookup"><span data-stu-id="27b8e-122">This will install hello modules into a subfolder named **node_modules**.</span></span>

## <a name="create-an-azure-web-app"></a><span data-ttu-id="27b8e-123">Bir Azure Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="27b8e-123">Create an Azure Web App</span></span>
<span data-ttu-id="27b8e-124">Bu adımları toocreate Azure web uygulaması izleyin, Git yayımlamayı etkinleştirmek ve hello web uygulaması WebSocket desteği etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="27b8e-124">Follow these steps toocreate an Azure web app, enable Git publishing, and then enable WebSocket support for hello web app.</span></span>

> [!NOTE]
> <span data-ttu-id="27b8e-125">toocomplete Bu öğretici bir Azure hesabınızın olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="27b8e-125">toocomplete this tutorial, you need an Azure account.</span></span> <span data-ttu-id="27b8e-126">Bir hesabınız yoksa, yalnızca birkaç dakika içinde ücretsiz bir deneme hesabı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27b8e-126">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="27b8e-127">Ayrıntılı bilgi için bkz. <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Azure Ücretsiz Deneme Sürümü</a>.</span><span class="sxs-lookup"><span data-stu-id="27b8e-127">For details, see <a href="http://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A7171371E" target="_blank">Azure Free Trial</a>.</span></span>
> 
> 

1. <span data-ttu-id="27b8e-128">Hello Azure komut satırı arabirimi (Azure CLI) yükleyin ve tooyour Azure aboneliğine bağlayın.</span><span class="sxs-lookup"><span data-stu-id="27b8e-128">Install hello Azure Command-Line Interface (Azure CLI) and connect tooyour Azure subscription.</span></span> <span data-ttu-id="27b8e-129">Bkz: [hello Azure CLI yükleyip](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="27b8e-129">See [Install and Configure hello Azure CLI](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="27b8e-130">İlk zaman ayarınız Azure deposunu varsa toocreate oturum açma kimlik bilgileri gerekir.</span><span class="sxs-lookup"><span data-stu-id="27b8e-130">If this is your first time setting up a repository in Azure, you need toocreate login credentials.</span></span> <span data-ttu-id="27b8e-131">Hello Azure CLI hello aşağıdaki komutu girin:</span><span class="sxs-lookup"><span data-stu-id="27b8e-131">From hello Azure CLI, enter hello following command:</span></span>
   
        azure site deployment user set [username] [password]
3. <span data-ttu-id="27b8e-132">Değiştirme toohello  **\\node\chat** dizin ve kullanım hello aşağıdaki yeni bir Azure web uygulaması ve bir yerel Git deposu toocreate komutu.</span><span class="sxs-lookup"><span data-stu-id="27b8e-132">Change toohello **\\node\chat** directory and use hello following command toocreate a new Azure web app and a local Git repository.</span></span> <span data-ttu-id="27b8e-133">Bu komut ayrıca bir Git Uzak adlandırılmış 'azure' oluşturur.</span><span class="sxs-lookup"><span data-stu-id="27b8e-133">This command also creates a Git remote named 'azure'.</span></span>
   
        azure site create mysitename --git
   
    <span data-ttu-id="27b8e-134">Web uygulamanız için benzersiz bir ad ile 'mysitename' değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="27b8e-134">You must replace 'mysitename' with a unique name for your web app.</span></span>
4. <span data-ttu-id="27b8e-135">Hello varolan dosyaları toohello yerel deposu, komutları aşağıdaki hello kullanarak kaydedin:</span><span class="sxs-lookup"><span data-stu-id="27b8e-135">Commit hello existing files toohello local repository by using hello following commands:</span></span>
   
        git add .
        git commit -m "Initial commit"
5. <span data-ttu-id="27b8e-136">Merhaba dosyaları toohello Azure Web Apps deposu komutu aşağıdaki hello ile gönderin:</span><span class="sxs-lookup"><span data-stu-id="27b8e-136">Push hello files toohello Azure Web Apps repository with hello following command:</span></span>
   
        git push azure master
   
    <span data-ttu-id="27b8e-137">İstendiğinde, adım 2 kimlik bilgilerinizi girin.</span><span class="sxs-lookup"><span data-stu-id="27b8e-137">When prompted, enter your credentials from step 2.</span></span> <span data-ttu-id="27b8e-138">Merhaba sunucuda modülleri içeri aktarılmış olarak durum iletilerini alacaktır.</span><span class="sxs-lookup"><span data-stu-id="27b8e-138">You will receive status messages as modules are imported on hello server.</span></span> <span data-ttu-id="27b8e-139">Bu işlem tamamlandıktan sonra Merhaba uygulaması Azure web uygulamanızın üzerinde barındırılan.</span><span class="sxs-lookup"><span data-stu-id="27b8e-139">Once this process has completed, hello application will be hosted on your Azure web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="27b8e-140">Modülü yükleme sırasında hatalarla karşılaşabilirsiniz, ' hello... alınan proje bulunamadı '.</span><span class="sxs-lookup"><span data-stu-id="27b8e-140">During module installation, you may notice errors that 'hello imported project ... was not found'.</span></span> <span data-ttu-id="27b8e-141">Bunlar güvenle yoksayılabilir.</span><span class="sxs-lookup"><span data-stu-id="27b8e-141">These can safely be ignored.</span></span>
   > 
   > 
6. <span data-ttu-id="27b8e-142">Azure üzerinde varsayılan olarak etkinleştirilmez WebSockets Socket.IO kullanır.</span><span class="sxs-lookup"><span data-stu-id="27b8e-142">Socket.IO uses WebSockets, which are not enabled by default on Azure.</span></span> <span data-ttu-id="27b8e-143">tooenable web yuvalarını hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="27b8e-143">tooenable web sockets, use hello following command:</span></span>
   
        azure site set -w
   
    <span data-ttu-id="27b8e-144">İstenirse, hello hello web uygulaması adını girin.</span><span class="sxs-lookup"><span data-stu-id="27b8e-144">If prompted, enter hello name of hello web app.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="27b8e-145">'azure sitesine -w set' komutu yalnızca sürümüyle 0.7.4 iş ya da üst hello Azure komut satırı arabirimi sürümünü hello.</span><span class="sxs-lookup"><span data-stu-id="27b8e-145">hello 'azure site set -w' command will work only with version 0.7.4 or higher of hello Azure Command-Line Interface.</span></span> <span data-ttu-id="27b8e-146">Hello kullanarak WebSocket desteği de etkinleştirebilirsiniz [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="27b8e-146">You can also enable WebSocket support using hello [Azure Portal](https://portal.azure.com).</span></span>
   > 
   > <span data-ttu-id="27b8e-147">WebSockets tooenable kullanarak Azure Portal Merhaba, hello Web uygulamaları dikey hello web uygulamasından tıklatın, **tüm ayarları** > **uygulama ayarları**.</span><span class="sxs-lookup"><span data-stu-id="27b8e-147">tooenable WebSockets using hello Azure Portal, click hello web app from hello Web Apps blade, click **All settings** > **Application settings**.</span></span> <span data-ttu-id="27b8e-148">Altında **Web yuvalarını**, tıklatın **üzerinde**.</span><span class="sxs-lookup"><span data-stu-id="27b8e-148">Under **Web Sockets**, click **On**.</span></span> <span data-ttu-id="27b8e-149">Daha sonra **Kaydet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="27b8e-149">Then click **Save**.</span></span>
   > 
   > 
7. <span data-ttu-id="27b8e-150">Azure, kullanım hello aşağıdaki tooview hello web uygulamasında toolaunch web tarayıcınız komut ve toohello barındırılan web uygulamasına gidin:</span><span class="sxs-lookup"><span data-stu-id="27b8e-150">tooview hello web app on Azure, use hello following command toolaunch your web browser and navigate toohello hosted web app:</span></span>
   
        azure site browse

<span data-ttu-id="27b8e-151">Uygulamanız artık Azure üzerinde çalışan ve Sohbet iletilerini Socket.IO kullanarak farklı istemciler arasında geçiş.</span><span class="sxs-lookup"><span data-stu-id="27b8e-151">Your app is now running on Azure, and can relay chat messages between different clients using Socket.IO.</span></span>

## <a name="scale-out"></a><span data-ttu-id="27b8e-152">Ölçeği genişletme</span><span class="sxs-lookup"><span data-stu-id="27b8e-152">Scale out</span></span>
<span data-ttu-id="27b8e-153">Socket.IO uygulamalar ölçeklendirilmiş çıkışı kullanarak bir **bağdaştırıcısı** toodistribute iletileri ve birden çok uygulama örnekleri arasında olaylar.</span><span class="sxs-lookup"><span data-stu-id="27b8e-153">Socket.IO applications can be scaled out by using an **adapter** toodistribute messages and events between multiple application instances.</span></span> <span data-ttu-id="27b8e-154">Kullanılabilir birkaç bağdaştırıcısı varken hello [Socket.IO redis] bağdaştırıcısı hello Azure Redis önbelleği özelliğiyle kolayca da kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="27b8e-154">While there are several adapters available, hello [socket.io-redis] adapter can be easily used with hello Azure Redis Cache feature.</span></span>

> [!NOTE]
> <span data-ttu-id="27b8e-155">Yapışkan oturumları desteği Socket.IO çözüm ölçeklendirmeye yönelik ek bir gereksinimdir.</span><span class="sxs-lookup"><span data-stu-id="27b8e-155">An additional requirement for scaling out a Socket.IO solution is support for sticky sessions.</span></span> <span data-ttu-id="27b8e-156">Yapışkan oturumları, Azure isteği Yönlendirme aracılığıyla Azure Web uygulamaları için varsayılan olarak etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="27b8e-156">Sticky sessions are enabled by default for Azure Web Apps through Azure Request Routing.</span></span> <span data-ttu-id="27b8e-157">Daha fazla bilgi için bkz: [örneğine benzeşimi, Azure Web siteleri].</span><span class="sxs-lookup"><span data-stu-id="27b8e-157">For more information, see [Instance Affinity in Azure Web Sites].</span></span>
> 
> 

### <a name="create-a-redis-cache"></a><span data-ttu-id="27b8e-158">Redis önbelleği oluşturma</span><span class="sxs-lookup"><span data-stu-id="27b8e-158">Create a Redis cache</span></span>
<span data-ttu-id="27b8e-159">Merhaba adımlarını gerçekleştirin [Azure Redis Önbelleği'nde bir önbellek oluşturma] toocreate yeni bir önbellek.</span><span class="sxs-lookup"><span data-stu-id="27b8e-159">Perform hello steps in [Create a cache in Azure Redis Cache] toocreate a new cache.</span></span>

> [!NOTE]
> <span data-ttu-id="27b8e-160">Merhaba Kaydet **ana bilgisayar adı** ve **birincil anahtar** bunlar içinde gerekli şekilde önbelleğiniz için sonraki adımlar hello.</span><span class="sxs-lookup"><span data-stu-id="27b8e-160">Save hello **Host name** and **Primary key** for your cache, as these will be needed in hello next steps.</span></span>
> 
> 

### <a name="add-hello-redis-and-socketio-redis-modules"></a><span data-ttu-id="27b8e-161">Merhaba redis ve Socket.IO redis modülleri ekleme</span><span class="sxs-lookup"><span data-stu-id="27b8e-161">Add hello redis and socket.io-redis modules</span></span>
1. <span data-ttu-id="27b8e-162">Bir komut satırından, toohello değiştirmek  **\\düğümü\\sohbet** komutu aşağıdaki dizin ve kullanım hello.</span><span class="sxs-lookup"><span data-stu-id="27b8e-162">From a command-line, change toohello **\\node\\chat** directory and use hello following command.</span></span>
   
        npm install socket.io-redis@0.1.4 redis@0.12.1 --save
   
   > [!NOTE]
   > <span data-ttu-id="27b8e-163">Bu komutta belirtilen hello sürümleri, bu makalede test edilirken kullanılan hello sürümleridir.</span><span class="sxs-lookup"><span data-stu-id="27b8e-163">hello versions specified in this command are hello versions used when testing this article.</span></span>
   > 
   > 
2. <span data-ttu-id="27b8e-164">Merhaba değiştirme **app.js** dosya tooadd hello aşağıdaki satırları hemen sonra`var io = require('socket.io')(server);`</span><span class="sxs-lookup"><span data-stu-id="27b8e-164">Modify hello **app.js** file tooadd hello following lines immediately after `var io = require('socket.io')(server);`</span></span>
   
        var pub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
        var sub = require('redis').createClient(6379,'redishostname', {auth_pass: 'rediskey', return_buffers: true});
   
        var redis = require('socket.io-redis');
        io.adapter(redis({pubClient: pub, subClient: sub}));
   
    <span data-ttu-id="27b8e-165">Değiştir **redishostname** ve **rediskey** hello ana bilgisayar adı ve Redis önbelleği için anahtar.</span><span class="sxs-lookup"><span data-stu-id="27b8e-165">Replace **redishostname** and **rediskey** with hello host name and key for your Redis cache.</span></span>
   
    <span data-ttu-id="27b8e-166">Bu bir yayımlama oluşturun ve istemci toohello daha önce oluşturduğunuz Redis önbelleği abone olun.</span><span class="sxs-lookup"><span data-stu-id="27b8e-166">This will create a publish and subscribe client toohello Redis cache created previously.</span></span> <span data-ttu-id="27b8e-167">Merhaba istemciler daha sonra hello bağdaştırıcısı tooconfigure Socket.IO toouse hello Redis önbelleği iletileri ve olayları, uygulamanızın örnekleri arasında geçirmek için kullanılır</span><span class="sxs-lookup"><span data-stu-id="27b8e-167">hello clients are then used with hello adapter tooconfigure Socket.IO toouse hello Redis cache for passing messages and events between instances of your application</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="27b8e-168">Merhaba sırasında **Socket.IO redis** bağdaştırıcısı doğrudan tooRedis iletişim, hello geçerli sürümü hello kimlik doğrulaması Azure Redis önbelleği tarafından gerekli desteklemez.</span><span class="sxs-lookup"><span data-stu-id="27b8e-168">While hello **socket.io-redis** adapter can communicate directly tooRedis, hello current version does not support hello authentication required by Azure Redis cache.</span></span> <span data-ttu-id="27b8e-169">Merhaba ilk bağlantı hello kullanılarak oluşturulan şekilde **redis** modülü, ardından hello istemci toohello geçirilir **Socket.IO redis** bağdaştırıcısı.</span><span class="sxs-lookup"><span data-stu-id="27b8e-169">So hello initial connection is created using hello **redis** module, then hello client is passed toohello **socket.io-redis** adapter.</span></span>
   > 
   > <span data-ttu-id="27b8e-170">Azure Redis önbelleği bağlantı noktası 6380 kullanarak güvenli bağlantı desteklerken, bu örnekte kullanılan hello modülleri 14/7/2014 sürümünden itibaren güvenli bağlantılarını desteklemez.</span><span class="sxs-lookup"><span data-stu-id="27b8e-170">While Azure Redis Cache supports secure connections using port 6380, hello modules used in this example do not support secure connections as of 7/14/2014.</span></span> <span data-ttu-id="27b8e-171">kod yukarıda Hello hello varsayılan, 6379 güvenli olmayan bağlantı noktasını kullanır.</span><span class="sxs-lookup"><span data-stu-id="27b8e-171">hello above code uses hello default, unsecure port of 6379.</span></span>
   > 
   > 
3. <span data-ttu-id="27b8e-172">Değiştirilen Kaydet hello **app.js**</span><span class="sxs-lookup"><span data-stu-id="27b8e-172">Save hello modified **app.js**</span></span>

### <a name="commit-changes-and-redeploy"></a><span data-ttu-id="27b8e-173">Değişiklikleri Kaydet ve yeniden dağıtın</span><span class="sxs-lookup"><span data-stu-id="27b8e-173">Commit changes and redeploy</span></span>
<span data-ttu-id="27b8e-174">Merhaba hello komut satırı gelen  **\\düğümü\\sohbet** dizin, aşağıdaki komutları toocommit değişiklikler hello kullanın ve hello uygulama yeniden dağıtın.</span><span class="sxs-lookup"><span data-stu-id="27b8e-174">From hello command-line in hello **\\node\\chat** directory, use hello following commands toocommit changes and redeploy hello application.</span></span>

    git add .
    git commit -m "implementing scale out"
    git push azure master

<span data-ttu-id="27b8e-175">Merhaba değişiklikleri toohello sunucu gönderildikten sonra komutu aşağıdaki hello kullanarak siteniz arasında birden çok örneği ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27b8e-175">Once hello changes have been pushed toohello server, you can scale your site across multiple instances by using hello following command.</span></span>

    azure site scale instances --instances #

<span data-ttu-id="27b8e-176">Burada  **#**  örnekleri toocreate hello sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="27b8e-176">Where **#** is hello number of instances toocreate.</span></span>

<span data-ttu-id="27b8e-177">Doğru tooall istemcileri gönderilen iletileri birden çok tarayıcılar veya bilgisayarlar tooverify tooyour web uygulaması bağlanabilir.</span><span class="sxs-lookup"><span data-stu-id="27b8e-177">You can connect tooyour web app from multiple browsers or computers tooverify that messages are correctly sent tooall clients.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="27b8e-178">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="27b8e-178">Troubleshooting</span></span>
### <a name="connection-limits"></a><span data-ttu-id="27b8e-179">Bağlantı sınırları</span><span class="sxs-lookup"><span data-stu-id="27b8e-179">Connection limits</span></span>
<span data-ttu-id="27b8e-180">Azure Web Apps hello kaynakları kullanılabilir tooyour site belirleyen birden çok SKU içinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="27b8e-180">Azure Web Apps is available in multiple SKUs, which determine hello resources available tooyour site.</span></span> <span data-ttu-id="27b8e-181">Bu, izin verilen WebSocket bağlantı hello sayısını içerir.</span><span class="sxs-lookup"><span data-stu-id="27b8e-181">This includes hello number of allowed WebSocket connections.</span></span> <span data-ttu-id="27b8e-182">Daha fazla bilgi için bkz: Merhaba [Web Apps Fiyatlandırma sayfasında].</span><span class="sxs-lookup"><span data-stu-id="27b8e-182">For more information, see hello [Web Apps Pricing page].</span></span>

### <a name="messages-arent-being-sent-using-websockets"></a><span data-ttu-id="27b8e-183">WebSockets kullanarak iletilerinin gönderilme değil</span><span class="sxs-lookup"><span data-stu-id="27b8e-183">Messages aren't being sent using WebSockets</span></span>
<span data-ttu-id="27b8e-184">İstemci tarayıcıları WebSockets kullanmak yerine yoklama toolong geri dönmeden tutmak, hello aşağıdakilerden biri nedeniyle olabilir.</span><span class="sxs-lookup"><span data-stu-id="27b8e-184">If client browsers keep falling back toolong polling instead of using WebSockets, it may be because of one of hello following.</span></span>

* <span data-ttu-id="27b8e-185">**Merhaba aktarım toojust WebSockets görüntülemeyi deneyin**</span><span class="sxs-lookup"><span data-stu-id="27b8e-185">**Try limiting hello transport toojust WebSockets**</span></span>
  
    <span data-ttu-id="27b8e-186">Socket.IO toouse WebSockets aktarım Mesajlaşma hello olarak hello sunucu ve istemci WebSockets'a desteklemesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="27b8e-186">In order for Socket.IO toouse WebSockets as hello messaging transport, both hello server and client must support WebSockets.</span></span> <span data-ttu-id="27b8e-187">Bir ya da diğer hello yoksa, Socket.IO uzun yoklama gibi başka bir aktarım anlaşmaları.</span><span class="sxs-lookup"><span data-stu-id="27b8e-187">If one or hello other does not, Socket.IO will negotiate another transport, such as long polling.</span></span> <span data-ttu-id="27b8e-188">taşımalar Socket.IO tarafından kullanılan varsayılan listesi Hello ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span><span class="sxs-lookup"><span data-stu-id="27b8e-188">hello default list of transports used by Socket.IO is ` websocket, htmlfile, xhr-polling, jsonp-polling`.</span></span> <span data-ttu-id="27b8e-189">Tooonly kullanım WebSockets kod toohello aşağıdaki hello ekleyerek zorlayabilirsiniz **app.js** hello satırını içeren sonra dosya `, nicknames = {};`.</span><span class="sxs-lookup"><span data-stu-id="27b8e-189">You can force it tooonly use WebSockets by adding hello following code toohello **app.js** file, after hello line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('transports', ['websocket']);
        });
  
  > [!NOTE]
  > <span data-ttu-id="27b8e-190">Yalnızca iletişimi tooWebSockets sınırlar gibi hello kodu yukarıdaki, etkinken WebSockets desteklemeyen eski tarayıcılar mümkün tooconnect toohello site olmayacağını unutmayın.</span><span class="sxs-lookup"><span data-stu-id="27b8e-190">Note that older browsers that do not support WebSockets will not be able tooconnect toohello site while hello above code is active, as it restricts communication tooWebSockets only.</span></span>
  > 
  > 
* <span data-ttu-id="27b8e-191">**SSL kullan**</span><span class="sxs-lookup"><span data-stu-id="27b8e-191">**Use SSL**</span></span>
  
    <span data-ttu-id="27b8e-192">WebSockets dayanır bazı küçük kullanılan HTTP üst bilgileri, hello gibi **yükseltme** üstbilgi.</span><span class="sxs-lookup"><span data-stu-id="27b8e-192">WebSockets relies on some lesser used HTTP headers, such as hello **Upgrade** header.</span></span> <span data-ttu-id="27b8e-193">Web proxy gibi bazı ara ağ aygıtlarını bu üstbilgileri kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27b8e-193">Some intermediate network devices, such as web proxies, may remove these headers.</span></span> <span data-ttu-id="27b8e-194">tooavoid Bu sorun, SSL üzerinden hello WebSocket bağlantısı kurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27b8e-194">tooavoid this problem, you can establish hello WebSocket connection over SSL.</span></span>
  
    <span data-ttu-id="27b8e-195">Kolay bir yolu tooaccomplish tooconfigure Socket.IO çok budur`match origin protocol`.</span><span class="sxs-lookup"><span data-stu-id="27b8e-195">An easy way tooaccomplish this is tooconfigure Socket.IO too`match origin protocol`.</span></span> <span data-ttu-id="27b8e-196">HTTP/HTTPS kaynaklanan hello aynı hello web sayfası için istek Socket.IO toosecure WebSockets iletişim hello bildirir.</span><span class="sxs-lookup"><span data-stu-id="27b8e-196">This instructs Socket.IO toosecure WebSockets communication hello same as hello originating HTTP/HTTPS request for hello web page.</span></span> <span data-ttu-id="27b8e-197">Bir tarayıcı Web sitenizi bir HTTPS URL'si toovisit kullanıyorsa, sonraki WebSocket iletişimleri Socket.IO ile SSL üzerinden güvenli.</span><span class="sxs-lookup"><span data-stu-id="27b8e-197">If a browser uses an HTTPS URL toovisit your website, subsequent WebSocket communications through Socket.IO will be secured over SSL.</span></span>
  
    <span data-ttu-id="27b8e-198">toomodify Bu örnek tooenable bu yapılandırma, kod toohello aşağıdaki hello eklemek **app.js** hello satırını içeren sonra dosyayı `, nicknames = {};`.</span><span class="sxs-lookup"><span data-stu-id="27b8e-198">toomodify this example tooenable this configuration, add hello following code toohello **app.js** file after hello line containing `, nicknames = {};`.</span></span>
  
        io.configure(function() {
          io.set('match origin protocol', true);
        });
* <span data-ttu-id="27b8e-199">**Web.config ayarlarını doğrulayın**</span><span class="sxs-lookup"><span data-stu-id="27b8e-199">**Verify web.config settings**</span></span>
  
    <span data-ttu-id="27b8e-200">Node.js uygulamaları barındırmak azure web uygulamaları kullanın hello **web.config** dosya tooroute gelen istekleri toohello Node.js uygulaması.</span><span class="sxs-lookup"><span data-stu-id="27b8e-200">Azure web apps that host Node.js applications use hello **web.config** file tooroute incoming requests toohello Node.js application.</span></span> <span data-ttu-id="27b8e-201">Node.js uygulamaları ile düzgün şekilde WebSockets toofunction için hello **web.config** girişi aşağıdaki hello içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="27b8e-201">For WebSockets toofunction correctly with Node.js applications, hello **web.config** must contain hello following entry.</span></span>
  
        <webSocket enabled="false"/>
  
    <span data-ttu-id="27b8e-202">Bu, kendi uygulaması WebSockets ve Node.js belirli WebSocket modüllerini Socket.IO gibi çakışıyor içerir hello IIS WebSockets modülü devre dışı bırakır.</span><span class="sxs-lookup"><span data-stu-id="27b8e-202">This disables hello IIS WebSockets module, which includes its own implementation of WebSockets and conflicts with Node.js specific WebSocket modules such as Socket.IO.</span></span> <span data-ttu-id="27b8e-203">Bu satırı mevcut değil veya çok ayarlamak`true`, bu, uygulamanız için hello WebSocket taşıma çalışmıyor hello neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="27b8e-203">If this line is not present, or is set too`true`, this may be hello reason that hello WebSocket transport is not working for your application.</span></span>
  
    <span data-ttu-id="27b8e-204">Normalde, Node.js uygulamalarını içermeyen bir **web.config** dosya şekilde dağıtıldığında, bunlar Azure Web siteleri otomatik olarak Node.js uygulamaları için bir tane oluşturur.</span><span class="sxs-lookup"><span data-stu-id="27b8e-204">Normally, Node.js applications do not include a **web.config** file, so Azure Websites will automatically generate one for Node.js applications when they are deployed.</span></span> <span data-ttu-id="27b8e-205">Bu dosya hello sunucuda otomatik olarak oluşturulan olduğundan, bu dosya için Web sitesi tooview hello FTP veya FTPS URL kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="27b8e-205">Since this file is automatically generated on hello server, you must use hello FTP or FTPS URL for your website tooview this file.</span></span> <span data-ttu-id="27b8e-206">Merhaba FTP ve FTPS URL'leri siteniz için hello Klasik portalında web uygulamanızı seçerek bulabilir ve ardından hello **Pano** bağlantı.</span><span class="sxs-lookup"><span data-stu-id="27b8e-206">You can find hello FTP and FTPS URLs for your site in hello classic portal by selecting your web app, and then hello **Dashboard** link.</span></span> <span data-ttu-id="27b8e-207">Merhaba URL'leri hello görüntülenen **Hızlı Bakış** bölümü.</span><span class="sxs-lookup"><span data-stu-id="27b8e-207">hello URLs are displayed in hello **quick glance** section.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="27b8e-208">Merhaba **web.config** uygulamanız bir sağlamıyorsa dosya Azure Web siteleri tarafından yalnızca oluşturulamaz.</span><span class="sxs-lookup"><span data-stu-id="27b8e-208">hello **web.config** file is only generated by Azure Websites if your application does not provide one.</span></span> <span data-ttu-id="27b8e-209">Sağlarsanız bir **web.config** dosya uygulama projenizin hello kök bunu Azure Web uygulamaları tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="27b8e-209">If you provide a **web.config** file in hello root of your application project, it will be used by Azure Web Apps.</span></span>
  > 
  > 
  
    <span data-ttu-id="27b8e-210">Merhaba girişi mevcut değil veya tooa değerinin ayarlanması, `true`, oluşturup bir **web.config** Merhaba, Node.js uygulamanızın kök ve değerini belirtin `false`.</span><span class="sxs-lookup"><span data-stu-id="27b8e-210">If hello entry is not present, or is set tooa value of `true`, then you should create a **web.config** in hello root of your Node.js application and specify a value of `false`.</span></span>  <span data-ttu-id="27b8e-211">Başvuru için aşağıdaki hello bir varsayılandır **web.config** kullanan bir uygulama için **app.js** hello giriş noktası olarak.</span><span class="sxs-lookup"><span data-stu-id="27b8e-211">For reference, hello below is a default **web.config** for an application that uses **app.js** as hello entry point.</span></span>
  
        <?xml version="1.0" encoding="utf-8"?>
        <!--
             This configuration file is required if iisnode is used toorun node processes behind
             IIS or IIS Express.  For more information, visit:
  
             https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config
        -->
  
        <configuration>
          <system.webServer>
            <!-- Visit http://blogs.msdn.com/b/windowsazure/archive/2013/11/14/introduction-to-websockets-on-windows-azure-web-sites.aspx for more information on WebSocket support -->
            <webSocket enabled="false" />
            <handlers>
              <!-- Indicates that hello server.js file is a node.js web app toobe handled by hello iisnode module -->
              <add name="iisnode" path="app.js" verb="*" modules="iisnode"/>
            </handlers>
            <rewrite>
              <rules>
                <!-- Do not interfere with requests for node-inspector debugging -->
                <rule name="NodeInspector" patternSyntax="ECMAScript" stopProcessing="true">
                  <match url="^app.js\/debug[\/]?" />
                </rule>
  
                <!-- First we consider whether hello incoming URL matches a physical file in hello /public folder -->
                <rule name="StaticContent">
                  <action type="Rewrite" url="public{REQUEST_URI}"/>
                </rule>
  
                <!-- All other URLs are mapped toohello node.js web app entry point -->
                <rule name="DynamicContent">
                  <conditions>
                    <add input="{REQUEST_FILENAME}" matchType="IsFile" negate="True"/>
                  </conditions>
                  <action type="Rewrite" url="app.js"/>
                </rule>
              </rules>
            </rewrite>
            <!--
              You can control how Node is hosted within IIS using hello following options:
                * watchedFiles: semi-colon separated list of files that will be watched for changes toorestart hello server
                * node_env: will be propagated toonode as NODE_ENV environment variable
                * debuggingEnabled - controls whether hello built-in debugger is enabled
  
              See https://github.com/tjanczuk/iisnode/blob/master/src/samples/configuration/web.config for a full list of options
            -->
            <!--<iisnode watchedFiles="web.config;*.js"/>-->
          </system.webServer>
        </configuration>
  
    <span data-ttu-id="27b8e-212">Uygulamanız bir giriş noktası dışındaki kullanıyorsa **app.js**, tüm oluşumlarını değiştirmelisiniz **app.js** giriş noktası ile Merhaba düzeltin.</span><span class="sxs-lookup"><span data-stu-id="27b8e-212">If your application uses an entry point other than **app.js**, you must replace all occurrences of **app.js** with hello correct entry point.</span></span> <span data-ttu-id="27b8e-213">Örneğin, değiştirme **app.js** ile **server.js**.</span><span class="sxs-lookup"><span data-stu-id="27b8e-213">For example, replacing **app.js** with **server.js**.</span></span>

> [!NOTE]
> <span data-ttu-id="27b8e-214">Azure hesabı için kaydolmadan önce Azure App Service ile başlatılan tooget istiyorsanız, çok Git[App Service'i deneyin], burada hemen bir kısa süreli başlangıç web uygulaması App Service'te oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27b8e-214">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="27b8e-215">Kredi kartı ve taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="27b8e-215">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="27b8e-216">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="27b8e-216">Next steps</span></span>
<span data-ttu-id="27b8e-217">Bu öğreticide nasıl toocreate bir Azure web uygulamasında bir sohbet uygulaması barındırılan öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="27b8e-217">In this tutorial you learned how toocreate a chat application hosted in an Azure web app.</span></span> <span data-ttu-id="27b8e-218">Bu uygulamayı bir Azure bulut hizmeti olarak da barındırabilir.</span><span class="sxs-lookup"><span data-stu-id="27b8e-218">You can also host this application as an Azure Cloud Service.</span></span> <span data-ttu-id="27b8e-219">Adımları için tooaccomplish buna ek olarak, bkz: [bir Node.js sohbet uygulaması Socket.IO ile bir Azure bulut hizmeti oluşturma].</span><span class="sxs-lookup"><span data-stu-id="27b8e-219">For steps on how tooaccomplish this, see [Build a Node.js Chat Application with Socket.IO on an Azure Cloud Service].</span></span>

<span data-ttu-id="27b8e-220">Daha fazla bilgi için hello Ayrıca bkz. [Node.js Geliştirici Merkezi].</span><span class="sxs-lookup"><span data-stu-id="27b8e-220">For more information, see also hello [Node.js Developer Center].</span></span>

## <a name="whats-changed"></a><span data-ttu-id="27b8e-221">Yapılan değişiklikler</span><span class="sxs-lookup"><span data-stu-id="27b8e-221">What's changed</span></span>
* <span data-ttu-id="27b8e-222">Web siteleri tooApp hizmet değişikliği Kılavuzu toohello için bkz: [Azure App Service ve mevcut Azure hizmetlerine etkileri].</span><span class="sxs-lookup"><span data-stu-id="27b8e-222">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services].</span></span>

<!-- URL List -->

[Azure Redis önbelleği]: /documentation/services/redis-cache/
[App Service Web Apps]: http://go.microsoft.com/fwlink/?LinkId=529714
[Web Apps Fiyatlandırma sayfasında]: http://go.microsoft.com/fwlink/?LinkId=511643
[bir Node.js sohbet uygulaması Socket.IO ile bir Azure bulut hizmeti oluşturma]: ../cloud-services/cloud-services-nodejs-chat-app-socketio.md
[Install and Configure hello Azure CLI]: ../cli-install-nodejs.md
[Azure App Service ve mevcut Azure hizmetlerine etkileri]: http://go.microsoft.com/fwlink/?LinkId=529714
[Node.js Geliştirici Merkezi]: /develop/nodejs/
[App Service'i deneyin]: https://azure.microsoft.com/try/app-service/
[örneğine benzeşimi, Azure Web siteleri]: https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/
[Azure Redis Önbelleği'nde bir önbellek oluşturma]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md

[Socket.IO redis]: https://github.com/socketio/socket.io-redis
[Socket.IO GitHub deposunu]: https://github.com/socketio/socket.io
[ZIP veya GZ Arşivlenen Sürüm]: https://github.com/socketio/socket.io/releases

<!-- IMG List -->

[chat-example-view]: ./media/web-sites-nodejs-chat-app-socketio/socketio-2.png
[npm-output]: ./media/web-sites-nodejs-chat-app-socketio/socketio-7.png
[completed-app]: ./media/web-sites-nodejs-chat-app-socketio/websitesocketcomplete.png
