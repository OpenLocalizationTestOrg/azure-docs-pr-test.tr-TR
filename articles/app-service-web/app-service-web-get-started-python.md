---
title: "aaaCreate bir Python web uygulamasını Azure | Microsoft Docs"
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
ms.openlocfilehash: 42178d490d8aa8eaf93710667aad598794c62c8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-python-web-app-in-azure"></a><span data-ttu-id="52cbe-103">Azure’da Python web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="52cbe-103">Create a Python web app in Azure</span></span>

<span data-ttu-id="52cbe-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) yüksek oranda ölçeklenebilen, kendi kendine düzeltme eki uygulayan bir web barındırma hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="52cbe-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="52cbe-105">Bu hızlı başlangıç nasıl anlatılmaktadır toodevelop ve Python uygulama tooAzure Web uygulamaları dağıtın.</span><span class="sxs-lookup"><span data-stu-id="52cbe-105">This quickstart walks through how toodevelop and deploy a Python app tooAzure Web Apps.</span></span> <span data-ttu-id="52cbe-106">Hello kullanarak hello web uygulaması oluşturma [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), ve Git toodeploy örnek Python kodu toohello web uygulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="52cbe-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git toodeploy sample Python code toohello web app.</span></span>

![Azure'da çalışan örnek uygulama](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="52cbe-108">Mac, Windows veya Linux makine kullanarak aşağıda hello adımları izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52cbe-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="52cbe-109">Merhaba önkoşulları yüklendikten sonra yaklaşık beş dakika toocomplete hello tedbirleri alır.</span><span class="sxs-lookup"><span data-stu-id="52cbe-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>
## <a name="prerequisites"></a><span data-ttu-id="52cbe-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="52cbe-110">Prerequisites</span></span>

<span data-ttu-id="52cbe-111">toocomplete Bu öğretici:</span><span class="sxs-lookup"><span data-stu-id="52cbe-111">toocomplete this tutorial:</span></span>

1. [<span data-ttu-id="52cbe-112">Git'i yükleyin</span><span class="sxs-lookup"><span data-stu-id="52cbe-112">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="52cbe-113">Python'ı yükleyin</span><span class="sxs-lookup"><span data-stu-id="52cbe-113">Install Python</span></span>](https://www.python.org/downloads/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="52cbe-114">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="52cbe-114">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="52cbe-115">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="52cbe-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="52cbe-116">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="52cbe-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-hello-sample"></a><span data-ttu-id="52cbe-117">Merhaba örnek indirme</span><span class="sxs-lookup"><span data-stu-id="52cbe-117">Download hello sample</span></span>

<span data-ttu-id="52cbe-118">Bir terminal penceresi komutu tooclone hello örnek uygulama havuzu tooyour yerel makine aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="52cbe-118">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/python-docs-hello-world
```

<span data-ttu-id="52cbe-119">Bu bir terminal penceresi toorun Bu hızlı başlangıcı tüm hello komutları kullanın.</span><span class="sxs-lookup"><span data-stu-id="52cbe-119">You use this terminal window toorun all hello commands in this quickstart.</span></span>

<span data-ttu-id="52cbe-120">Merhaba örnek kod içeren toohello dizini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="52cbe-120">Change toohello directory that contains hello sample code.</span></span>

```bash
cd Python-docs-hello-world
```

## <a name="run-hello-app-locally"></a><span data-ttu-id="52cbe-121">Merhaba uygulamayı yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="52cbe-121">Run hello app locally</span></span>

<span data-ttu-id="52cbe-122">Kullanarak hello gerekli paketleri yüklemek `pip`.</span><span class="sxs-lookup"><span data-stu-id="52cbe-122">Install hello required packages using `pip`.</span></span>

```bash
pip install -r requirements.txt
```

<span data-ttu-id="52cbe-123">Merhaba uygulaması bir terminal penceresi açarak ve hello kullanarak yerel olarak çalıştırın `Python` komutu toolaunch hello yerleşik Python web sunucusu.</span><span class="sxs-lookup"><span data-stu-id="52cbe-123">Run hello application locally by opening a terminal window and using hello `Python` command toolaunch hello built-in Python web server.</span></span>

```bash
python main.py
```

<span data-ttu-id="52cbe-124">Bir web tarayıcısı açın ve http://localhost: 5000 toohello örnek uygulamaya gidin.</span><span class="sxs-lookup"><span data-stu-id="52cbe-124">Open a web browser, and navigate toohello sample app at http://localhost:5000.</span></span>

<span data-ttu-id="52cbe-125">Merhaba görebilirsiniz **Hello World** hello örnek uygulamadan hello sayfasında görüntülenen ileti.</span><span class="sxs-lookup"><span data-stu-id="52cbe-125">You can see hello **Hello World** message from hello sample app displayed in hello page.</span></span>

![Yerel olarak çalışan örnek uygulama](media/app-service-web-get-started-python/localhost-hello-world-in-browser.png)

<span data-ttu-id="52cbe-127">Terminal pencerenizde basın **Ctrl + C** tooexit hello web sunucusu.</span><span class="sxs-lookup"><span data-stu-id="52cbe-127">In your terminal window, press **Ctrl+C** tooexit hello web server.</span></span>

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Boş web uygulaması sayfası](media/app-service-web-get-started-python/app-service-web-service-created.png)

<span data-ttu-id="52cbe-129">Azure'da yeni bir boş uygulama oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="52cbe-129">You’ve created an empty new web app in Azure.</span></span>

## <a name="configure-toouse-python"></a><span data-ttu-id="52cbe-130">Toouse Python yapılandırın</span><span class="sxs-lookup"><span data-stu-id="52cbe-130">Configure toouse Python</span></span>

<span data-ttu-id="52cbe-131">Kullanım hello [az webapp yapılandırma kümesi](/cli/azure/webapp/config#set) komutu tooconfigure hello web uygulama toouse Python sürümü `3.4`.</span><span class="sxs-lookup"><span data-stu-id="52cbe-131">Use hello [az webapp config set](/cli/azure/webapp/config#set) command tooconfigure hello web app toouse Python version `3.4`.</span></span>

```azurecli-interactive
az webapp config set --python-version 3.4 --name <app_name> --resource-group myResourceGroup
```


<span data-ttu-id="52cbe-132">Bu şekilde Hello Python sürümü ayarı hello platform tarafından sağlanan varsayılan kapsayıcı kullanır.</span><span class="sxs-lookup"><span data-stu-id="52cbe-132">Setting hello Python version this way uses a default container provided by hello platform.</span></span> <span data-ttu-id="52cbe-133">toouse kendi kapsayıcı bkz hello hello için CLI başvurusu [az webapp config kapsayıcı kümesi](/cli/azure/webapp/config/container#set) komutu.</span><span class="sxs-lookup"><span data-stu-id="52cbe-133">toouse your own container, see hello CLI reference for hello [az webapp config container set](/cli/azure/webapp/config/container#set) command.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 18, done.
Delta compression using up too4 threads.
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
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a><span data-ttu-id="52cbe-134">Toohello uygulama Gözat</span><span class="sxs-lookup"><span data-stu-id="52cbe-134">Browse toohello app</span></span>

<span data-ttu-id="52cbe-135">Web tarayıcınız üzerinden dağıtılan toohello uygulama göz atın.</span><span class="sxs-lookup"><span data-stu-id="52cbe-135">Browse toohello deployed application using your web browser.</span></span>

```bash
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="52cbe-136">Merhaba Python örnek kod bir Azure App Service web uygulaması çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="52cbe-136">hello Python sample code is running in an Azure App Service web app.</span></span>

![Azure'da çalışan örnek uygulama](media/app-service-web-get-started-python/hello-world-in-browser.png)

<span data-ttu-id="52cbe-138">**Tebrikler!**</span><span class="sxs-lookup"><span data-stu-id="52cbe-138">**Congratulations!**</span></span> <span data-ttu-id="52cbe-139">İlk Python uygulaması tooApp hizmeti dağıttıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="52cbe-139">You've deployed your first Python app tooApp Service.</span></span>

## <a name="update-and-redeploy-hello-code"></a><span data-ttu-id="52cbe-140">Güncelleştirme ve hello kodu yeniden dağıtın</span><span class="sxs-lookup"><span data-stu-id="52cbe-140">Update and redeploy hello code</span></span>

<span data-ttu-id="52cbe-141">Bir yerel metin düzenleyicisi kullanarak hello açmak `main.py` dosya hello Python uygulamada ve küçük değişiklikler toohello metin sonraki toohello olun `return` deyimi:</span><span class="sxs-lookup"><span data-stu-id="52cbe-141">Using a local text editor, open hello `main.py` file in hello Python app, and make a small change toohello text next toohello `return` statement:</span></span>

```python
return 'Hello, Azure!'
```

<span data-ttu-id="52cbe-142">Git yaptığınız değişiklikleri kaydetmek ve hello kod değişiklikleri tooAzure gönderme.</span><span class="sxs-lookup"><span data-stu-id="52cbe-142">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated output"
git push azure master
```

<span data-ttu-id="52cbe-143">Dağıtım tamamlandıktan sonra hello açılan arka toohello tarayıcı penceresine dönün [Gözat toohello uygulama](#browse-to-the-app) adım ve yenileme hello sayfası.</span><span class="sxs-lookup"><span data-stu-id="52cbe-143">Once deployment has completed, switch back toohello browser window that opened in hello [Browse toohello app](#browse-to-the-app) step, and refresh hello page.</span></span>

![Azure'da çalışan güncelleştirilmiş örnek uygulama](media/app-service-web-get-started-python/hello-azure-in-browser.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="52cbe-145">Yeni Azure web uygulamanızı yönetme</span><span class="sxs-lookup"><span data-stu-id="52cbe-145">Manage your new Azure web app</span></span>

<span data-ttu-id="52cbe-146">Toohello Git <a href="https://portal.azure.com" target="_blank">Azure portal</a> oluşturduğunuz toomanage hello web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="52cbe-146">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="52cbe-147">Merhaba sol menüden **uygulama hizmetleri**ve ardından, Azure web uygulamanızın hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="52cbe-147">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Portal Gezinti tooAzure web uygulaması](./media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-list.png)

<span data-ttu-id="52cbe-149">Web uygulamanızın Genel Bakış sayfasını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="52cbe-149">You see your web app's Overview page.</span></span> <span data-ttu-id="52cbe-150">Buradan göz atma, durdurma, başlatma, yeniden başlatma ve silme gibi temel yönetim görevlerini gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="52cbe-150">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Azure portalında App Service dikey penceresi](media/app-service-web-get-started-nodejs-poc/nodejs-docs-hello-world-app-service-detail.png)

<span data-ttu-id="52cbe-152">Merhaba soldaki menüden, uygulamanızı yapılandırmak için farklı sayfaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="52cbe-152">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="52cbe-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="52cbe-153">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="52cbe-154">PostgreSQL ile Python</span><span class="sxs-lookup"><span data-stu-id="52cbe-154">Python with PostgreSQL</span></span>](app-service-web-tutorial-docker-python-postgresql-app.md)
