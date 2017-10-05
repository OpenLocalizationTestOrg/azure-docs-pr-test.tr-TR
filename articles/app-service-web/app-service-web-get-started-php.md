---
title: "Azure'da PHP web uygulaması oluşturma | Microsoft Docs"
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
ms.openlocfilehash: 3a78e0b485046ad6228bf4819d3908042c298d1a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-php-web-app-in-azure"></a><span data-ttu-id="df7d1-103">Azure’da PHP web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="df7d1-103">Create a PHP web app in Azure</span></span>

<span data-ttu-id="df7d1-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) yüksek oranda ölçeklenebilen, kendi kendine düzeltme eki uygulayan bir web barındırma hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="df7d1-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="df7d1-105">Bu hızlı başlangıç öğreticisinde, Azure Web Apps'te bir PHP uygulamasının nasıl dağıtılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="df7d1-105">This quickstart tutorial shows how to deploy a PHP app to Azure Web Apps.</span></span> <span data-ttu-id="df7d1-106">Cloud Shell’de [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) kullanarak web uygulamasını oluşturabilir ve örnek PHP kodunu web uygulamasına dağıtmak için Git kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="df7d1-106">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) in Cloud Shell, and you use Git to deploy sample PHP code to the web app.</span></span>

<span data-ttu-id="df7d1-107">![Azure'da çalışan örnek uygulama]](media/app-service-web-get-started-php/hello-world-in-browser.png)</span><span class="sxs-lookup"><span data-stu-id="df7d1-107">![Sample app running in Azure]](media/app-service-web-get-started-php/hello-world-in-browser.png)</span></span>

<span data-ttu-id="df7d1-108">Mac, Windows veya Linux makinesi kullanarak aşağıdaki adımları izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="df7d1-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="df7d1-109">Önkoşullar yüklendikten sonra adımların tamamlanması yaklaşık olarak beş dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="df7d1-109">Once the prerequisites are installed, it takes about five minutes to complete the steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="df7d1-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="df7d1-110">Prerequisites</span></span>

<span data-ttu-id="df7d1-111">Bu hızlı başlangıcı tamamlamak için:</span><span class="sxs-lookup"><span data-stu-id="df7d1-111">To complete this quickstart:</span></span>

* [<span data-ttu-id="df7d1-112">Git'i yükleyin</span><span class="sxs-lookup"><span data-stu-id="df7d1-112">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="df7d1-113">PHP'yi yükleyin</span><span class="sxs-lookup"><span data-stu-id="df7d1-113">Install PHP</span></span>](https://php.net)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-the-sample-locally"></a><span data-ttu-id="df7d1-114">Örnekleri yerel makineye indirme</span><span class="sxs-lookup"><span data-stu-id="df7d1-114">Download the sample locally</span></span>

<span data-ttu-id="df7d1-115">Bir terminal penceresinde aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="df7d1-115">In a terminal window, run the following commands.</span></span> <span data-ttu-id="df7d1-116">Bu işlem, örnek uygulamanın yerel makinenize kopyalanmasını ve örnek kodu içeren dizine gitmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="df7d1-116">This will clone the sample application to your local machine, and navigate to the directory containing the sample code.</span></span>

```bash
git clone https://github.com/Azure-Samples/php-docs-hello-world
cd php-docs-hello-world
```

## <a name="run-the-app-locally"></a><span data-ttu-id="df7d1-117">Uygulamayı yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="df7d1-117">Run the app locally</span></span>

<span data-ttu-id="df7d1-118">Yerleşik PHP web sunucusunu başlatmak için bir terminal penceresi açıp ve `php` komutunu kullanıp uygulamayı yerel olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="df7d1-118">Run the application locally by opening a terminal window and using the `php` command to launch the built-in PHP web server.</span></span>

```bash
php -S localhost:8080
```

<span data-ttu-id="df7d1-119">Bir web tarayıcısı açın ve http://localhost:8080 konumundaki örnek uygulamaya gidin.</span><span class="sxs-lookup"><span data-stu-id="df7d1-119">Open a web browser, and navigate to the sample app at http://localhost:8080.</span></span>

<span data-ttu-id="df7d1-120">Sayfada gösterilen örnek uygulamada **Merhaba Dünya!**</span><span class="sxs-lookup"><span data-stu-id="df7d1-120">You see the **Hello World!**</span></span> <span data-ttu-id="df7d1-121">iletisini görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="df7d1-121">message from the sample app displayed in the page.</span></span>

![Yerel olarak çalışan örnek uygulama](media/app-service-web-get-started-php/localhost-hello-world-in-browser.png)

<span data-ttu-id="df7d1-123">Terminal pencerenizde **Ctrl+C** tuşlarına basarak web sunucusundan çıkın.</span><span class="sxs-lookup"><span data-stu-id="df7d1-123">In your terminal window, press **Ctrl+C** to exit the web server.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)]

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)]

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)]

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)]

![Boş web uygulaması sayfası](media/app-service-web-get-started-php/app-service-web-service-created.png)

<span data-ttu-id="df7d1-125">Azure'da yeni bir boş uygulama oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="df7d1-125">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push to Azure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 2, done.
Delta compression using up to 4 threads.
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
To https://<app_name>.scm.azurewebsites.net/<app_name>.git
   cc39b1e..25f1805  master -> master
```

## <a name="browse-to-the-app-locally"></a><span data-ttu-id="df7d1-126">Yerel makinede uygulamanın konumuna gitme</span><span class="sxs-lookup"><span data-stu-id="df7d1-126">Browse to the app locally</span></span>

<span data-ttu-id="df7d1-127">Web tarayıcınızı kullanarak, dağıtılan uygulamanın konumuna gidin.</span><span class="sxs-lookup"><span data-stu-id="df7d1-127">Browse to the deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="df7d1-128">PHP örnek kodu bir Azure App Service web uygulamasında çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="df7d1-128">The PHP sample code is running in an Azure App Service web app.</span></span>

![Azure'da çalışan örnek uygulama](media/app-service-web-get-started-php/hello-world-in-browser.png)

<span data-ttu-id="df7d1-130">**Tebrikler!**</span><span class="sxs-lookup"><span data-stu-id="df7d1-130">**Congratulations!**</span></span> <span data-ttu-id="df7d1-131">App Service’e ilk PHP uygulamanızı dağıttınız.</span><span class="sxs-lookup"><span data-stu-id="df7d1-131">You've deployed your first PHP app to App Service.</span></span>

## <a name="update-locally-and-redeploy-the-code"></a><span data-ttu-id="df7d1-132">Kodu yerel makinede güncelleştirme ve yeniden dağıtma</span><span class="sxs-lookup"><span data-stu-id="df7d1-132">Update locally and redeploy the code</span></span>

<span data-ttu-id="df7d1-133">Bir yerel metin düzenleyicisi kullanarak `index.php` dosyasını PHP uygulaması içinde açın ve `echo` öğesinin yanındaki dizenin içinde bulunan metinde küçük bir değişiklik yapın:</span><span class="sxs-lookup"><span data-stu-id="df7d1-133">Using a local text editor, open the `index.php` file within the PHP app, and make a small change to the text within the string next to `echo`:</span></span>

```php
echo "Hello Azure!";
```

<span data-ttu-id="df7d1-134">Değişikliklerinizi Git’e işleyin ve ardından kod değişikliklerini Azure’a gönderin.</span><span class="sxs-lookup"><span data-stu-id="df7d1-134">Commit your changes in Git, and then push the code changes to Azure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="df7d1-135">Dağıtım tamamlandıktan sonra **Uygulamaya göz atma** adımında açılan tarayıcı penceresine dönüp sayfayı yenileyin.</span><span class="sxs-lookup"><span data-stu-id="df7d1-135">Once deployment has completed, switch back to the browser window that opened in the **Browse to the app** step, and refresh the page.</span></span>

![Azure'da çalışan güncelleştirilmiş örnek uygulama](media/app-service-web-get-started-php/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="df7d1-137">Yeni Azure web uygulamanızı yönetme</span><span class="sxs-lookup"><span data-stu-id="df7d1-137">Manage your new Azure web app</span></span>

<span data-ttu-id="df7d1-138">Oluşturduğunuz web uygulamasını yönetmek için <a href="https://portal.azure.com" target="_blank">Azure portalına</a> gidin.</span><span class="sxs-lookup"><span data-stu-id="df7d1-138">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span></span>

<span data-ttu-id="df7d1-139">Sol menüden **Uygulama Hizmetleri**'ne ve ardından Azure web uygulamanızın adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="df7d1-139">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Portaldan Azure web uygulamasına gitme](./media/app-service-web-get-started-php/php-docs-hello-world-app-service-list.png)

<span data-ttu-id="df7d1-141">Web uygulamanızın Genel Bakış sayfasını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="df7d1-141">You see your web app's Overview page.</span></span> <span data-ttu-id="df7d1-142">Buradan göz atma, durdurma, başlatma, yeniden başlatma ve silme gibi temel yönetim görevlerini gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="df7d1-142">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span>

![Azure portalında App Service dikey penceresi](media/app-service-web-get-started-php/php-docs-hello-world-app-service-detail.png)

<span data-ttu-id="df7d1-144">Soldaki menü, uygulamanızı yapılandırmak için farklı sayfalar sağlar.</span><span class="sxs-lookup"><span data-stu-id="df7d1-144">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="df7d1-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="df7d1-145">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="df7d1-146">MySQL ile PHP</span><span class="sxs-lookup"><span data-stu-id="df7d1-146">PHP with MySQL</span></span>](app-service-web-tutorial-php-mysql.md)
