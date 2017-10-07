---
title: "aaaCreate azure'da Node.js web uygulamasına | Microsoft Docs"
description: "Azure App Service Web Uygulamalarında ilk Node.js Hello World uygulamanızı birkaç dakika içinde dağıtın."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 582bb3c2-164b-42f5-b081-95bfcb7a502a
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 05/05/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 163edf83b2353755fc9fa2d75aed489038cf7c81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-nodejs-web-app-in-azure"></a><span data-ttu-id="d82ad-103">Azure App Service'te Node.js web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="d82ad-103">Create a Node.js web app in Azure</span></span>

<span data-ttu-id="d82ad-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) yüksek oranda ölçeklenebilen, kendi kendine düzeltme eki uygulayan bir web barındırma hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="d82ad-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="d82ad-105">Bu hızlı başlangıç gösterir nasıl toodeploy bir Node.js uygulaması tooAzure Web uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="d82ad-105">This quickstart shows how toodeploy a Node.js app tooAzure Web Apps.</span></span> <span data-ttu-id="d82ad-106">Hello kullanarak hello web uygulaması oluşturma [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), ve Git toodeploy örnek Node.js kodu toohello web uygulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="d82ad-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git toodeploy sample Node.js code toohello web app.</span></span>

![Azure'da çalışan örnek uygulama](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="d82ad-108">Mac, Windows veya Linux makine kullanarak aşağıda hello adımları izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d82ad-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="d82ad-109">Merhaba önkoşulları yüklendikten sonra yaklaşık beş dakika toocomplete hello tedbirleri alır.</span><span class="sxs-lookup"><span data-stu-id="d82ad-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>   

> [!VIDEO https://channel9.msdn.com/Shows/Azure-for-Node-Developers/Create-a-Nodejs-app-in-Azure-Quickstart/player]   


## <a name="prerequisites"></a><span data-ttu-id="d82ad-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d82ad-110">Prerequisites</span></span>

<span data-ttu-id="d82ad-111">toocomplete Bu hızlı başlangıç:</span><span class="sxs-lookup"><span data-stu-id="d82ad-111">toocomplete this quickstart:</span></span>

* [<span data-ttu-id="d82ad-112">Git'i yükleyin</span><span class="sxs-lookup"><span data-stu-id="d82ad-112">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="d82ad-113">Node.js ve NPM'yi yükleyin</span><span class="sxs-lookup"><span data-stu-id="d82ad-113">Install Node.js and NPM</span></span>](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d82ad-114">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d82ad-114">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="d82ad-115">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="d82ad-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="d82ad-116">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d82ad-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-hello-sample"></a><span data-ttu-id="d82ad-117">Merhaba örnek indirme</span><span class="sxs-lookup"><span data-stu-id="d82ad-117">Download hello sample</span></span>

<span data-ttu-id="d82ad-118">Bir terminal penceresi komutu tooclone hello örnek uygulama havuzu tooyour yerel makine aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d82ad-118">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/nodejs-docs-hello-world
```

<span data-ttu-id="d82ad-119">Bu bir terminal penceresi toorun Bu hızlı başlangıcı tüm hello komutları kullanın.</span><span class="sxs-lookup"><span data-stu-id="d82ad-119">You use this terminal window toorun all hello commands in this quickstart.</span></span>

<span data-ttu-id="d82ad-120">Merhaba örnek kod içeren toohello dizini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d82ad-120">Change toohello directory that contains hello sample code.</span></span>

```bash
cd nodejs-docs-hello-world
```

## <a name="run-hello-app-locally"></a><span data-ttu-id="d82ad-121">Merhaba uygulamayı yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="d82ad-121">Run hello app locally</span></span>

<span data-ttu-id="d82ad-122">Merhaba uygulaması bir terminal penceresi açarak ve hello kullanarak yerel olarak çalıştırın `npm start` betik toolaunch hello Node.js HTTP sunucusu kurulur.</span><span class="sxs-lookup"><span data-stu-id="d82ad-122">Run hello application locally by opening a terminal window and using hello `npm start` script toolaunch hello built in Node.js HTTP server.</span></span>

```bash
npm start
```

<span data-ttu-id="d82ad-123">Bir web tarayıcısı açın ve http://localhost: 1337 toohello örnek uygulamaya gidin.</span><span class="sxs-lookup"><span data-stu-id="d82ad-123">Open a web browser, and navigate toohello sample app at http://localhost:1337.</span></span>

<span data-ttu-id="d82ad-124">Merhaba gördüğünüz **Hello World** hello örnek uygulamadan hello sayfasında görüntülenen ileti.</span><span class="sxs-lookup"><span data-stu-id="d82ad-124">You see hello **Hello World** message from hello sample app displayed in hello page.</span></span>

![Yerel olarak çalışan örnek uygulama](media/app-service-web-get-started-nodejs-poc/localhost-hello-world-in-browser.png)

<span data-ttu-id="d82ad-126">Terminal pencerenizde basın **Ctrl + C** tooexit hello web sunucusu.</span><span class="sxs-lookup"><span data-stu-id="d82ad-126">In your terminal window, press **Ctrl+C** tooexit hello web server.</span></span>

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Boş web uygulaması sayfası](media/app-service-web-get-started-php/app-service-web-service-created.png)

<span data-ttu-id="d82ad-128">Azure'da yeni bir boş uygulama oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="d82ad-128">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 23, done.
Delta compression using up too4 threads.
Compressing objects: 100% (21/21), done.
Writing objects: 100% (23/23), 3.71 KiB | 0 bytes/s, done.
Total 23 (delta 8), reused 7 (delta 1)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'bf114df591'.
remote: Generating deployment script.
remote: Generating deployment script for node.js Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling node.js deployment.
remote: Kudu sync from: '/home/site/repository' to: '/home/site/wwwroot'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Copying file: 'index.js'
remote: Copying file: 'package.json'
remote: Copying file: 'process.json'
remote: Deleting file: 'hostingstart.html'
remote: Ignoring: .git
remote: Using start-up script index.js from package.json.
remote: Node.js versions available on hello platform are: 4.4.7, 4.5.0, 6.2.2, 6.6.0, 6.9.1.
remote: Selected node.js version 6.9.1. Use package.json file toochoose a different version.
remote: Selected npm version 3.10.8
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net:443/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a><span data-ttu-id="d82ad-129">Toohello uygulama Gözat</span><span class="sxs-lookup"><span data-stu-id="d82ad-129">Browse toohello app</span></span>

<span data-ttu-id="d82ad-130">Web tarayıcınız üzerinden dağıtılan toohello uygulama göz atın.</span><span class="sxs-lookup"><span data-stu-id="d82ad-130">Browse toohello deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="d82ad-131">Merhaba Node.js örnek kod bir Azure App Service web uygulaması çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="d82ad-131">hello Node.js sample code is running in an Azure App Service web app.</span></span>

![Azure'da çalışan örnek uygulama](media/app-service-web-get-started-nodejs-poc/hello-world-in-browser.png)

<span data-ttu-id="d82ad-133">**Tebrikler!**</span><span class="sxs-lookup"><span data-stu-id="d82ad-133">**Congratulations!**</span></span> <span data-ttu-id="d82ad-134">İlk Node.js uygulaması tooApp hizmeti dağıttıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="d82ad-134">You've deployed your first Node.js app tooApp Service.</span></span>

## <a name="update-and-redeploy-hello-code"></a><span data-ttu-id="d82ad-135">Güncelleştirme ve hello kodu yeniden dağıtın</span><span class="sxs-lookup"><span data-stu-id="d82ad-135">Update and redeploy hello code</span></span>

<span data-ttu-id="d82ad-136">Bir metin düzenleyicisi kullanarak hello açın `index.js` dosya hello Node.js uygulamasında ve küçük değişiklikler toohello metin hello çağrıda çok olun`response.end`:</span><span class="sxs-lookup"><span data-stu-id="d82ad-136">Using a text editor, open hello `index.js` file in hello Node.js app, and make a small change toohello text in hello call too`response.end`:</span></span>

```nodejs
response.end("Hello Azure!");
```

<span data-ttu-id="d82ad-137">Git yaptığınız değişiklikleri kaydetmek ve hello kod değişiklikleri tooAzure gönderme.</span><span class="sxs-lookup"><span data-stu-id="d82ad-137">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="d82ad-138">Dağıtım tamamlandıktan sonra hello açılan arka toohello tarayıcı penceresine dönün **Gözat toohello uygulama** adım ve yenileme basın.</span><span class="sxs-lookup"><span data-stu-id="d82ad-138">Once deployment has completed, switch back toohello browser window that opened in hello **Browse toohello app** step, and hit refresh.</span></span>

![Azure'da çalışan güncelleştirilmiş örnek uygulama](media/app-service-web-get-started-nodejs-poc/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="d82ad-140">Yeni Azure web uygulamanızı yönetme</span><span class="sxs-lookup"><span data-stu-id="d82ad-140">Manage your new Azure web app</span></span>

<span data-ttu-id="d82ad-141">Toohello Git <a href="https://portal.azure.com" target="_blank">Azure portal</a> oluşturduğunuz toomanage hello web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="d82ad-141">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="d82ad-142">Merhaba sol menüden **uygulama hizmetleri**ve ardından, Azure web uygulamanızın hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="d82ad-142">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Portal Gezinti tooAzure web uygulaması](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="d82ad-144">Web uygulamanızın Genel Bakış sayfasını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="d82ad-144">You see your web app's Overview page.</span></span> <span data-ttu-id="d82ad-145">Buradan göz atma, durdurma, başlatma, yeniden başlatma ve silme gibi temel yönetim görevlerini gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d82ad-145">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Azure portalında App Service dikey penceresi](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="d82ad-147">Merhaba soldaki menüden, uygulamanızı yapılandırmak için farklı sayfaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="d82ad-147">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="d82ad-148">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d82ad-148">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d82ad-149">MongoDB ile Node.js</span><span class="sxs-lookup"><span data-stu-id="d82ad-149">Node.js with MongoDB</span></span>](app-service-web-tutorial-nodejs-mongodb-app.md)
