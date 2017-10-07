---
title: "Azure web uygulamasında aaaCreate statik HTML | Microsoft Docs"
description: "Bir statik HTML dağıtarak toorun web uygulamaları Azure App Service'deki uygulama nasıl örnek öğrenin."
services: app-service\web
documentationcenter: 
author: rick-anderson
manager: wpickett
editor: 
ms.assetid: 60495cc5-6963-4bf0-8174-52786d226c26
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 05/26/2017
ms.author: riande
ms.custom: mvc
ms.openlocfilehash: efd8c8189a3aa1ac35602b688eeb31bff6f5a373
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-static-html-web-app-in-azure"></a><span data-ttu-id="01ef1-103">Azure'da statik bir HTML web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="01ef1-103">Create a static HTML web app in Azure</span></span>

<span data-ttu-id="01ef1-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) yüksek oranda ölçeklenebilen, kendi kendine düzeltme eki uygulayan bir web barındırma hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="01ef1-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span>  <span data-ttu-id="01ef1-105">Bu hızlı başlangıç nasıl toodeploy temel HTML + CSS site tooAzure Web uygulamaları gösterir.</span><span class="sxs-lookup"><span data-stu-id="01ef1-105">This quickstart shows how toodeploy a basic HTML+CSS site tooAzure Web Apps.</span></span> <span data-ttu-id="01ef1-106">Hello kullanarak hello web uygulaması oluşturma [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), ve Git toodeploy örnek HTML içerik toohello web uygulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="01ef1-106">You create hello web app using hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and you use Git toodeploy sample HTML content toohello web app.</span></span>

![Örnek uygulamanın giriş sayfası](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

<span data-ttu-id="01ef1-108">Mac, Windows veya Linux makine kullanarak aşağıda hello adımları izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01ef1-108">You can follow hello steps below using a Mac, Windows, or Linux machine.</span></span> <span data-ttu-id="01ef1-109">Merhaba önkoşulları yüklendikten sonra yaklaşık beş dakika toocomplete hello tedbirleri alır.</span><span class="sxs-lookup"><span data-stu-id="01ef1-109">Once hello prerequisites are installed, it takes about five minutes toocomplete hello steps.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01ef1-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="01ef1-110">Prerequisites</span></span>

<span data-ttu-id="01ef1-111">toocomplete Bu hızlı başlangıç:</span><span class="sxs-lookup"><span data-stu-id="01ef1-111">toocomplete this quickstart:</span></span>

- <span data-ttu-id="01ef1-112">[Git'i yükleyin](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]</span><span class="sxs-lookup"><span data-stu-id="01ef1-112">[Install Git](https://git-scm.com/)
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="01ef1-113">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="01ef1-113">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="01ef1-114">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="01ef1-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="01ef1-115">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="01ef1-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="download-hello-sample"></a><span data-ttu-id="01ef1-116">Merhaba örnek indirme</span><span class="sxs-lookup"><span data-stu-id="01ef1-116">Download hello sample</span></span>

<span data-ttu-id="01ef1-117">Bir terminal penceresi komutu tooclone hello örnek uygulama havuzu tooyour yerel makine aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="01ef1-117">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine.</span></span>

```bash
git clone https://github.com/Azure-Samples/html-docs-hello-world.git
```

<span data-ttu-id="01ef1-118">Bu bir terminal penceresi toorun Bu hızlı başlangıcı tüm hello komutları kullanın.</span><span class="sxs-lookup"><span data-stu-id="01ef1-118">You use this terminal window toorun all hello commands in this quickstart.</span></span>

## <a name="view-hello-html"></a><span data-ttu-id="01ef1-119">Görünüm başlangıç HTML</span><span class="sxs-lookup"><span data-stu-id="01ef1-119">View hello HTML</span></span>

<span data-ttu-id="01ef1-120">Merhaba örnek HTML içeren toohello dizinine gidin.</span><span class="sxs-lookup"><span data-stu-id="01ef1-120">Navigate toohello directory that contains hello sample HTML.</span></span> <span data-ttu-id="01ef1-121">Açık hello *index.html* dosyayı tarayıcınızda.</span><span class="sxs-lookup"><span data-stu-id="01ef1-121">Open hello *index.html* file in your browser.</span></span>

![Örnek uygulama ana sayfası](media/app-service-web-get-started-html/hello-world-in-browser.png)

[!INCLUDE [Log in tooAzure](../../includes/login-to-azure.md)] 

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user.md)] 

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group.md)] 

[!INCLUDE [Create app service plan](../../includes/app-service-web-create-app-service-plan.md)] 

[!INCLUDE [Create web app](../../includes/app-service-web-create-web-app.md)] 

![Boş web uygulaması sayfası](media/app-service-web-get-started-html/app-service-web-service-created.png)

<span data-ttu-id="01ef1-124">Azure'da yeni bir boş uygulama oluşturdunuz.</span><span class="sxs-lookup"><span data-stu-id="01ef1-124">You’ve created an empty new web app in Azure.</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git.md)] 

[!INCLUDE [Push tooAzure](../../includes/app-service-web-git-push-to-azure.md)] 

```bash
Counting objects: 13, done.
Delta compression using up too4 threads.
Compressing objects: 100% (11/11), done.
Writing objects: 100% (13/13), 2.07 KiB | 0 bytes/s, done.
Total 13 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'cc39b1e4cb'.
remote: Generating deployment script.
remote: Generating deployment script for Web Site
remote: Generated deployment script files
remote: Running deployment command...
remote: Handling Basic Web Site deployment.
remote: KuduSync.NET from: 'D:\home\site\repository' to: 'D:\home\site\wwwroot'
remote: Deleting file: 'hostingstart.html'
remote: Copying file: '.gitignore'
remote: Copying file: 'LICENSE'
remote: Copying file: 'README.md'
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
```

## <a name="browse-toohello-app"></a><span data-ttu-id="01ef1-125">Toohello uygulama Gözat</span><span class="sxs-lookup"><span data-stu-id="01ef1-125">Browse toohello app</span></span>

<span data-ttu-id="01ef1-126">Bir tarayıcıda toohello Azure web uygulaması URL'si gidin:</span><span class="sxs-lookup"><span data-stu-id="01ef1-126">In a browser, go toohello Azure web app URL:</span></span>

```
http://<app_name>.azurewebsites.net
```

<span data-ttu-id="01ef1-127">Başlangıç sayfası, bir Azure App Service web uygulaması çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="01ef1-127">hello page is running as an Azure App Service web app.</span></span>

![Örnek uygulama ana sayfası](media/app-service-web-get-started-html/hello-world-in-browser-az.png)

<span data-ttu-id="01ef1-129">**Tebrikler!**</span><span class="sxs-lookup"><span data-stu-id="01ef1-129">**Congratulations!**</span></span> <span data-ttu-id="01ef1-130">İlk, HTML Uygulama tooApp hizmeti dağıttıktan sonra.</span><span class="sxs-lookup"><span data-stu-id="01ef1-130">You've deployed your first HTML app tooApp Service.</span></span>

## <a name="update-and-redeploy-hello-app"></a><span data-ttu-id="01ef1-131">Güncelleştirme ve hello uygulama yeniden dağıtın</span><span class="sxs-lookup"><span data-stu-id="01ef1-131">Update and redeploy hello app</span></span>

<span data-ttu-id="01ef1-132">Açık hello *index.html* dosyasını bir metin düzenleyicisinde ve değişiklik toohello biçimlendirme yapın.</span><span class="sxs-lookup"><span data-stu-id="01ef1-132">Open hello *index.html* file in a text editor, and make a change toohello markup.</span></span> <span data-ttu-id="01ef1-133">Örneğin, "Azure uygulama hizmeti – örnek statik HTML Site" toojust hello H1 başlığını değiştirme "Azure uygulama hizmeti '.</span><span class="sxs-lookup"><span data-stu-id="01ef1-133">For example, change hello H1 heading from "Azure App Service - Sample Static HTML Site" toojust "Azure App Service\`.</span></span>

<span data-ttu-id="01ef1-134">Git yaptığınız değişiklikleri kaydetmek ve hello kod değişiklikleri tooAzure gönderme.</span><span class="sxs-lookup"><span data-stu-id="01ef1-134">Commit your changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git commit -am "updated HTML"
git push azure master
```

<span data-ttu-id="01ef1-135">Dağıtım tamamlandıktan sonra tarayıcı toosee hello değişikliklerinizi yenileyin.</span><span class="sxs-lookup"><span data-stu-id="01ef1-135">Once deployment has completed, refresh your browser toosee hello changes.</span></span>

![Güncelleştirilen örnek uygulama giriş sayfası](media/app-service-web-get-started-html/hello-azure-in-browser-az.png)

## <a name="manage-your-new-azure-web-app"></a><span data-ttu-id="01ef1-137">Yeni Azure web uygulamanızı yönetme</span><span class="sxs-lookup"><span data-stu-id="01ef1-137">Manage your new Azure web app</span></span>

<span data-ttu-id="01ef1-138">Toohello Git <a href="https://portal.azure.com" target="_blank">Azure portal</a> oluşturduğunuz toomanage hello web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="01ef1-138">Go toohello <a href="https://portal.azure.com" target="_blank">Azure portal</a> toomanage hello web app you created.</span></span>

<span data-ttu-id="01ef1-139">Merhaba sol menüden **uygulama hizmetleri**ve ardından, Azure web uygulamanızın hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="01ef1-139">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Portal Gezinti tooAzure web uygulaması](./media/app-service-web-get-started-html/portal1.png)

<span data-ttu-id="01ef1-141">Web uygulamanızın Genel Bakış sayfasını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="01ef1-141">You see your web app's Overview page.</span></span> <span data-ttu-id="01ef1-142">Buradan göz atma, durdurma, başlatma, yeniden başlatma ve silme gibi temel yönetim görevlerini gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="01ef1-142">Here, you can perform basic management tasks like browse, stop, start, restart, and delete.</span></span> 

![Azure portalında App Service dikey penceresi](./media/app-service-web-get-started-html/portal2.png)

<span data-ttu-id="01ef1-144">Merhaba soldaki menüden, uygulamanızı yapılandırmak için farklı sayfaları sağlar.</span><span class="sxs-lookup"><span data-stu-id="01ef1-144">hello left menu provides different pages for configuring your app.</span></span> 

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a><span data-ttu-id="01ef1-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="01ef1-145">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="01ef1-146">Özel etki alanı eşleme</span><span class="sxs-lookup"><span data-stu-id="01ef1-146">Map custom domain</span></span>](app-service-web-tutorial-custom-domain.md)
