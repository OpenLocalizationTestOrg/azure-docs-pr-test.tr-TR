---
title: "aaaCreate bir PHP web uygulamasına | Microsoft Docs"
description: "Azure App Service Web Uygulamalarında ilk PHP Hello World uygulamanızı birkaç dakika içinde dağıtın."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 6feac128-c728-4491-8b79-962da9a40788
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 07/21/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 8e1022889ca162f8f15ce7435cc9393cc6efef06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-php-web-app-in-azure"></a><span data-ttu-id="6ac48-103">Azure’da PHP web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="6ac48-103">Create a PHP web app in Azure</span></span>

<span data-ttu-id="6ac48-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) yüksek oranda ölçeklenebilen, kendi kendine düzeltme eki uygulayan bir web barındırma hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="6ac48-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="6ac48-105">Bu hızlı başlangıç Öğreticisi gösterir nasıl toodeploy bir PHP uygulaması tooAzure Web uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="6ac48-105">This quickstart tutorial shows how toodeploy a PHP app tooAzure Web Apps.</span></span> <span data-ttu-id="6ac48-106">Hello kullanarak hello web uygulaması oluşturma [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) içinde bulut kabuk ve Git toodeploy örnek PHP kodunu toohello web uygulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="6ac48-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) in Cloud Shell, and you use Git toodeploy sample PHP code toohello web app.</span></span>

<span data-ttu-id="6ac48-107">![Azure'da çalışan örnek uygulama]](media/app-service-web-get-started-php/hello-world-in-browser.png)</span><span class="sxs-lookup"><span data-stu-id="6ac48-107">![Sample app running in Azure]](media/app-service-web-get-started-php/hello-world-in-browser.png)</span></span>

<span data-ttu-id="6ac48-108">Mac, Windows veya Linux makine kullanarak aşağıda hello adımları izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ac48-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="6ac48-109">Merhaba önkoşulları yüklendikten sonra yaklaşık beş dakika toocomplete hello tedbirleri alır.</span><span class="sxs-lookup"><span data-stu-id="6ac48-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ac48-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="6ac48-110">Prerequisites</span></span>

<span data-ttu-id="6ac48-111">toocomplete Bu hızlı başlangıç:</span><span class="sxs-lookup"><span data-stu-id="6ac48-111">toocomplete this quickstart:</span></span>

* [<span data-ttu-id="6ac48-112">Git'i yükleyin</span><span class="sxs-lookup"><span data-stu-id="6ac48-112">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="6ac48-113">PHP'yi yükleyin</span><span class="sxs-lookup"><span data-stu-id="6ac48-113">Install PHP</span></span>](https://php.net)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample-locally"></a><span data-ttu-id="6ac48-114">Merhaba örnek yerel olarak indir</span><span class="sxs-lookup"><span data-stu-id="6ac48-114">Download hello sample locally</span></span>

<span data-ttu-id="6ac48-115">Bir terminal penceresi hello aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="6ac48-115">In a terminal window, run hello following commands.</span></span> <span data-ttu-id="6ac48-116">Bu hello örnek uygulama tooyour yerel makine ve toohello directory içeren hello örnek kod gidin.</span><span class="sxs-lookup"><span data-stu-id="6ac48-116">This will clone hello sample application tooyour local machine, and navigate toohello directory containing hello sample code.</span></span>

```bash
git clone https://github.com/Azure-Samples/php-docs-hello-world
cd php-docs-hello-world
```

## <a name="run-hello-app-locally"></a><span data-ttu-id="6ac48-117">Merhaba uygulamayı yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="6ac48-117">Run hello app locally</span></span>

<span data-ttu-id="6ac48-118">Merhaba uygulaması bir terminal penceresi açarak ve hello kullanarak yerel olarak çalıştırın `php` komutu toolaunch hello yerleşik PHP web sunucusu.</span><span class="sxs-lookup"><span data-stu-id="6ac48-118">Run hello application locally by opening a terminal window and using hello `php` command toolaunch hello built-in PHP web server.</span></span>

```bash
php -S localhost:8080
```

<span data-ttu-id="6ac48-119">Bir web tarayıcısı açın ve http://localhost: 8080 toohello örnek uygulamaya gidin.</span><span class="sxs-lookup"><span data-stu-id="6ac48-119">Open a web browser, and navigate toohello sample app at http://localhost:8080.</span></span>

<span data-ttu-id="6ac48-120">Merhaba gördüğünüz **Merhaba Dünya!**</span><span class="sxs-lookup"><span data-stu-id="6ac48-120">You see hello **Hello World!**</span></span> <span data-ttu-id="6ac48-121">ileti hello örnek uygulamadan hello sayfasında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="6ac48-121">message from hello sample app displayed in hello page.</span></span>

![Yerel olarak çalışan örnek uygulama](media/app-service-web-get-started-php/localhost-hello-world-in-browser.png)

<span data-ttu-id="6ac48-123">Terminal pencerenizde basın **Ctrl + C** tooexit hello web sunucusu.</span><span class="sxs-lookup"><span data-stu-id="6ac48-123">In your terminal window, press **Ctrl+C** tooexit hello web server.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)]

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)]

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)]

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)]

![Boş web uygulaması sayfası](media/app-service-web-get-started-php/app-service-web-service-created.png)

<span data-ttu-id="6ac48-125">Azure'da yeni bir boş uygulama oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="6ac48-125">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 2, done.
Delta compression using up too4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (2/2), 352 bytes | 0 bytes/s, done.
Total 2 (delta 1), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '25f18051e9'.
remote: Generating deployment script.
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: Kudu sync from: '/home/site/repository' to: '/home/site/wwwroot'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Copying file: 'index.php'
remote: Ignoring: .git
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
   cc39b1e..25f1805  master -> master
```

## <a name="browse-toohello-app-locally"></a><span data-ttu-id="6ac48-126">Yerel olarak toohello uygulama Gözat</span><span class="sxs-lookup"><span data-stu-id="6ac48-126">Browse toohello app locally</span></span>

<span data-ttu-id="6ac48-127">Web tarayıcınız üzerinden dağıtılan toohello uygulama göz atın.</span><span class="sxs-lookup"><span data-stu-id="6ac48-127">Browse toohello deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="6ac48-128">Merhaba PHP örnek kod bir Azure App Service web uygulaması çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="6ac48-128">hello PHP sample code is running in an Azure App Service web app.</span></span>

![Azure'da çalışan örnek uygulama](media/app-service-web-get-started-php/hello-world-in-browser.png)

<span data-ttu-id="6ac48-130">**Tebrikler!**</span><span class="sxs-lookup"><span data-stu-id="6ac48-130">**Congratulations!**</span></span> <span data-ttu-id="6ac48-131">İlk, PHP uygulaması tooApp hizmeti dağıttıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="6ac48-131">You've deployed your first PHP app tooApp Service.</span></span>

## <a name="update-locally-and-redeploy-hello-code"></a><span data-ttu-id="6ac48-132">Yerel olarak güncelleştirin ve hello kodu yeniden dağıtın</span><span class="sxs-lookup"><span data-stu-id="6ac48-132">Update locally and redeploy hello code</span></span>

<span data-ttu-id="6ac48-133">Bir yerel metin düzenleyicisi kullanarak hello açmak `index.php` dosya hello PHP uygulama içinde ve küçük değişiklikler toohello metin hello dizesindeki sonraki çok olun`echo`:</span><span class="sxs-lookup"><span data-stu-id="6ac48-133">Using a local text editor, open hello `index.php` file within hello PHP app, and make a small change toohello text within hello string next too`echo`:</span></span>

```php
echo "Hello Azure!";
```

<span data-ttu-id="6ac48-134">Git yaptığınız değişiklikleri kaydetmek ve hello kod değişiklikleri tooAzure gönderme.</span><span class="sxs-lookup"><span data-stu-id="6ac48-134">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="6ac48-135">Dağıtım tamamlandıktan sonra hello açılan arka toohello tarayıcı penceresine dönün **Gözat toohello uygulama** adım ve yenileme hello sayfası.</span><span class="sxs-lookup"><span data-stu-id="6ac48-135">Once deployment has completed, switch back toohello browser window that opened in hello **Browse toohello app** step, and refresh hello page.</span></span>

![Azure'da çalışan güncelleştirilmiş örnek uygulama](media/app-service-web-get-started-php/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="6ac48-137">Yeni Azure web uygulamanızı yönetme</span><span class="sxs-lookup"><span data-stu-id="6ac48-137">Manage your new Azure web app</span></span>

<span data-ttu-id="6ac48-138">Toohello Git <a href="https://portal.azure.com" target="_blank">Azure portal</a> oluşturduğunuz toomanage hello web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="6ac48-138">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="6ac48-139">Merhaba sol menüden **uygulama hizmetleri**ve ardından, Azure web uygulamanızın hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="6ac48-139">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Portal Gezinti tooAzure web uygulaması](./media/app-service-web-get-started-php/php-docs-hello-world-app-service-list.png)

<span data-ttu-id="6ac48-141">Web uygulamanızın Genel Bakış sayfasını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="6ac48-141">You see your web app's Overview page.</span></span> <span data-ttu-id="6ac48-142">Buradan göz atma, durdurma, başlatma, yeniden başlatma ve silme gibi temel yönetim görevlerini gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ac48-142">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span>

![Azure portalında App Service dikey penceresi](media/app-service-web-get-started-php/php-docs-hello-world-app-service-detail.png)

<span data-ttu-id="6ac48-144">Merhaba soldaki menüden, uygulamanızı yapılandırmak için farklı sayfaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="6ac48-144">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="6ac48-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6ac48-145">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6ac48-146">MySQL ile PHP</span><span class="sxs-lookup"><span data-stu-id="6ac48-146">PHP with MySQL</span></span>](app-service-web-tutorial-php-mysql.md)
