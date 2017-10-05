---
title: "Azure'da Python web uygulaması oluşturma | Microsoft Docs"
description: "Azure App Service Web Uygulamalarında ilk Python Hello World uygulamanızı birkaç dakika içinde dağıtın."
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
ms.assetid: 928ee2e5-6143-4c0c-8546-366f5a3d80ce
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 03/17/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 119f9770097c010cc360e0e204d06a307a268814
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-python-web-app-in-azure"></a><span data-ttu-id="ca9c1-103">Azure’da Python web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="ca9c1-103">Create a Python web app in Azure</span></span>

<span data-ttu-id="ca9c1-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) yüksek oranda ölçeklenebilen, kendi kendine düzeltme eki uygulayan bir web barındırma hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="ca9c1-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="ca9c1-105">Bu hızlı başlangıç öğreticisi, Azure Web Apps'te bir Python uygulaması geliştirip dağıtma konusunda yol göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="ca9c1-105">This quickstart walks through how to develop and deploy a Python app to Azure Web Apps.</span></span> <span data-ttu-id="ca9c1-106">Web uygulamasını [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli)'yi kullanarak oluşturabilir ve web uygulamasında örnek Python kodu dağıtmak için Git'i kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca9c1-106">You create the web app using the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git to deploy sample Python code to the web app.</span></span>

![Azure'da çalışan örnek uygulama](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="ca9c1-108">Mac, Windows veya Linux makinesi kullanarak aşağıdaki adımları izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca9c1-108">You can follow the steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="ca9c1-109">Önkoşullar yüklendikten sonra adımların tamamlanması yaklaşık olarak beş dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="ca9c1-109">Once the prerequisites are installed, it takes about five minutes to complete the steps.</span></span>
## <a name="prerequisites"></a><span data-ttu-id="ca9c1-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="ca9c1-110">Prerequisites</span></span>

<span data-ttu-id="ca9c1-111">Bu öğreticiyi tamamlamak için:</span><span class="sxs-lookup"><span data-stu-id="ca9c1-111">To complete this tutorial:</span></span>

1. [<span data-ttu-id="ca9c1-112">Git'i yükleyin</span><span class="sxs-lookup"><span data-stu-id="ca9c1-112">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="ca9c1-113">Python'ı yükleyin</span><span class="sxs-lookup"><span data-stu-id="ca9c1-113">Install Python</span></span>](https://www.python.org/downloads/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="ca9c1-114">CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu başlığı için Azure CLI 2.0 veya sonraki bir sürümünü kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ca9c1-114">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="ca9c1-115">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ca9c1-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="ca9c1-116">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ca9c1-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-the-sample"></a><span data-ttu-id="ca9c1-117">Örneği indirme</span><span class="sxs-lookup"><span data-stu-id="ca9c1-117">Download the sample</span></span>

<span data-ttu-id="ca9c1-118">Bir terminal penceresinde, örnek uygulama deposunu yerel makinenize kopyalamak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ca9c1-118">In a terminal window, run the following command to clone the sample app repository to your local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/python-docs-hello-world
```

<span data-ttu-id="ca9c1-119">Bu hızlı başlangıç öğreticisindeki tüm komutları çalıştırmak için bu terminal penceresini kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="ca9c1-119">You use this terminal window to run all the commands in this quickstart.</span></span>

<span data-ttu-id="ca9c1-120">Örnek kodu içeren dizine geçin.</span><span class="sxs-lookup"><span data-stu-id="ca9c1-120">Change to the directory that contains the sample code.</span></span>

```bash
cd Python-docs-hello-world
```

## <a name="run-the-app-locally"></a><span data-ttu-id="ca9c1-121">Uygulamayı yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="ca9c1-121">Run the app locally</span></span>

<span data-ttu-id="ca9c1-122">Gereken paketleri `pip` kullanarak yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ca9c1-122">Install the required packages using `pip`.</span></span>

```bash
pip install -r requirements.txt
```

<span data-ttu-id="ca9c1-123">Yerleşik Python web sunucusunu başlatmak için bir terminal penceresi açıp ve `Python` komutunu kullanıp uygulamayı yerel olarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="ca9c1-123">Run the application locally by opening a terminal window and using the `Python` command to launch the built-in Python web server.</span></span>

```bash
python main.py
```

<span data-ttu-id="ca9c1-124">Bir web tarayıcısı açın ve http://localhost:5000 konumundaki örnek uygulamaya gidin.</span><span class="sxs-lookup"><span data-stu-id="ca9c1-124">Open a web browser, and navigate to the sample app at http://localhost:5000.</span></span>

<span data-ttu-id="ca9c1-125">Sayfada gösterilen örnek uygulamada **Hello World** iletisini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca9c1-125">You can see the **Hello World** message from the sample app displayed in the page.</span></span>

![Yerel olarak çalışan örnek uygulama](media/app-service-web-get-started-python/localhost-hello-world-in-browser.png)

<span data-ttu-id="ca9c1-127">Terminal pencerenizde **Ctrl+C** tuşlarına basarak web sunucusundan çıkın.</span><span class="sxs-lookup"><span data-stu-id="ca9c1-127">In your terminal window, press **Ctrl+C** to exit the web server.</span></span>

[!INCLUDE [Log in to Azure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Boş web uygulaması sayfası](media/app-service-web-get-started-python/app-service-web-service-created.png)

<span data-ttu-id="ca9c1-129">Azure'da yeni bir boş uygulama oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="ca9c1-129">You’ve created an empty new web app in Azure.</span></span>

## <a name="configure-to-use-python"></a><span data-ttu-id="ca9c1-130">Python kullanacak şekilde yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ca9c1-130">Configure to use Python</span></span>

<span data-ttu-id="ca9c1-131">Web uygulamasını Python `3.4` sürümünü kullanacak şekilde yapılandırmak için [az webapp config set](/cli/azure/webapp/config#set) komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="ca9c1-131">Use the [az webapp config set](/cli/azure/webapp/config#set) command to configure the web app to use Python version `3.4`.</span></span>

```azurecli-interactive
az webapp config set --python-version 3.4 --name <app_name> --resource-group myResourceGroup
```


<span data-ttu-id="ca9c1-132">Python sürümü bu şekilde ayarlandığında, platform tarafından sağlanan varsayılan bir kapsayıcı kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ca9c1-132">Setting the Python version this way uses a default container provided by the platform.</span></span> <span data-ttu-id="ca9c1-133">Kendi kapsayıcınızı kullanmak üzere, [az webapp config container set](/cli/azure/webapp/config/container#set) komutuna ilişkin CLI başvurusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="ca9c1-133">To use your own container, see the CLI reference for the [az webapp config container set](/cli/azure/webapp/config/container#set) command.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push to Azure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 18, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (16/16), done.
Writing objects: 100% (18/18), 4.31 KiB | 0 bytes/s, done.
Total 18 (delta 4), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '44e74fe7dd'.
remote: Generating deployment script.
remote: Generating deployment script for python Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling python deployment.
remote: KuduSync.NET from: 'D:\home\site\repository' to: 'D:\home\site\wwwroot'
remote: Deleting file: 'hostingstart.html'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'main.py'
remote: Copying file: 'README.md'
remote: Copying file: 'requirements.txt'
remote: Copying file: 'virtualenv_proxy.py'
remote: Copying file: 'web.2.7.config'
remote: Copying file: 'web.3.4.config'
remote: Detected requirements.txt.  You can skip Python specific steps with a .skipPythonDeployment file.
remote: Detecting Python runtime from site configuration
remote: Detected python-3.4
remote: Creating python-3.4 virtual environment.
remote: .................................
remote: Pip install requirements.
remote: Successfully installed Flask click itsdangerous Jinja2 Werkzeug MarkupSafe
remote: Cleaning up...
remote: .
remote: Overwriting web.config with web.3.4.config
remote:         1 file(s) copied.
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
To https://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-to-the-app"></a><span data-ttu-id="ca9c1-134">Uygulamaya göz atma</span><span class="sxs-lookup"><span data-stu-id="ca9c1-134">Browse to the app</span></span>

<span data-ttu-id="ca9c1-135">Web tarayıcınızı kullanarak dağıtılan uygulamaya göz atın.</span><span class="sxs-lookup"><span data-stu-id="ca9c1-135">Browse to the deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="ca9c1-136">Python örnek kodu bir Azure App Service web uygulamasında çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="ca9c1-136">The Python sample code is running in an Azure App Service web app.</span></span>

![Azure'da çalışan örnek uygulama](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="ca9c1-138">**Tebrikler!**</span><span class="sxs-lookup"><span data-stu-id="ca9c1-138">**Congratulations!**</span></span> <span data-ttu-id="ca9c1-139">App Service’e ilk Python uygulamanızı dağıttınız.</span><span class="sxs-lookup"><span data-stu-id="ca9c1-139">You've deployed your first Python app to App Service.</span></span>

## <a name="update-and-redeploy-the-code"></a><span data-ttu-id="ca9c1-140">Kodu güncelleştirme ve yeniden dağıtma</span><span class="sxs-lookup"><span data-stu-id="ca9c1-140">Update and redeploy the code</span></span>

<span data-ttu-id="ca9c1-141">Yerel bir metin düzenleyici kullanarak `main.py` dosyasını Python uygulamasında açın ve `return` deyiminin yanındaki metinde küçük bir değişiklik yapın:</span><span class="sxs-lookup"><span data-stu-id="ca9c1-141">Using a local text editor, open the `main.py` file in the Python app, and make a small change to the text next to the `return` statement:</span></span>

```python
return 'Hello, Azure!'
```

<span data-ttu-id="ca9c1-142">Değişikliklerinizi Git’e işleyin ve ardından kod değişikliklerini Azure’a gönderin.</span><span class="sxs-lookup"><span data-stu-id="ca9c1-142">Commit your changes in Git, and then push the code changes to Azure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="ca9c1-143">Dağıtım tamamlandıktan sonra [Uygulamaya göz atma](#browse-to-the-app) adımında açılan tarayıcı penceresine dönüp sayfayı yenileyin.</span><span class="sxs-lookup"><span data-stu-id="ca9c1-143">Once deployment has completed, switch back to the browser window that opened in the [Browse to the app](#browse-to-the-app) step, and refresh the page.</span></span>

![Azure'da çalışan güncelleştirilmiş örnek uygulama](media/app-service-web-get-started-python/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="ca9c1-145">Yeni Azure web uygulamanızı yönetme</span><span class="sxs-lookup"><span data-stu-id="ca9c1-145">Manage your new Azure web app</span></span>

<span data-ttu-id="ca9c1-146">Oluşturduğunuz web uygulamasını yönetmek için <a href="https://portal.azure.com" target="_blank">Azure portalına</a> gidin.</span><span class="sxs-lookup"><span data-stu-id="ca9c1-146">Go to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> to manage the web app you created.</span></span>

<span data-ttu-id="ca9c1-147">Sol menüden **Uygulama Hizmetleri**'ne ve ardından Azure web uygulamanızın adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="ca9c1-147">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Portaldan Azure web uygulamasına gitme](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="ca9c1-149">Web uygulamanızın Genel Bakış sayfasını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="ca9c1-149">You see your web app's Overview page.</span></span> <span data-ttu-id="ca9c1-150">Buradan göz atma, durdurma, başlatma, yeniden başlatma ve silme gibi temel yönetim görevlerini gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca9c1-150">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Azure portalında App Service dikey penceresi](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="ca9c1-152">Soldaki menü, uygulamanızı yapılandırmak için farklı sayfalar sağlar.</span><span class="sxs-lookup"><span data-stu-id="ca9c1-152">The left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="ca9c1-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ca9c1-153">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ca9c1-154">PostgreSQL ile Python</span><span class="sxs-lookup"><span data-stu-id="ca9c1-154">Python with PostgreSQL</span></span>](app-service-web-tutorial-docker-python-postgresql-app.md)
