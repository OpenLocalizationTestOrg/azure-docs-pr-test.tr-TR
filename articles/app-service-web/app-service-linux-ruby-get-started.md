---
title: "aaaCreate bir Ruby uygulaması Linux üzerinde Web uygulamalarıyla | Microsoft Docs"
description: "Toocreate Ruby öğrenin Linux Azure web wpp uygulamalarla."
keywords: Azure uygulama hizmeti, linux, oss, ruby
services: app-service
documentationcenter: 
author: wesmc7777
manager: erikre
editor: 
ms.assetid: 6d00c73c-13cb-446f-8926-923db4101afa
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: wesmc;rachelap
ms.openlocfilehash: 99ce3b5ee16703a147787387bb02973defce8190
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-ruby-app-with-web-apps-on-linux"></a><span data-ttu-id="9e0d1-104">Linux üzerinde Web uygulamaları ile Söyleniş bir uygulama oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9e0d1-104">Create a Ruby App with Web Apps on Linux</span></span> 

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

<span data-ttu-id="9e0d1-105">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) yüksek oranda ölçeklenebilen, kendi kendine düzeltme eki uygulayan bir web barındırma hizmeti sunar.</span><span class="sxs-lookup"><span data-stu-id="9e0d1-105">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="9e0d1-106">Bu hızlı başlangıç toocreate rayları uygulama üzerinde temel bir Ruby sonra dağıtma gösterir tooAzure Linux üzerinde bir Web uygulaması olarak.</span><span class="sxs-lookup"><span data-stu-id="9e0d1-106">This quickstart shows you how toocreate a basic Ruby on Rails application you then deploy it tooAzure as a Web App on Linux.</span></span>

![Merhaba Dünya](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

## <a name="prerequisites"></a><span data-ttu-id="9e0d1-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9e0d1-108">Prerequisites</span></span>

* <span data-ttu-id="9e0d1-109">[Ruby 2.4.1 ya da daha yüksek](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).</span><span class="sxs-lookup"><span data-stu-id="9e0d1-109">[Ruby 2.4.1 or higher](https://www.ruby-lang.org/en/documentation/installation/#rubyinstaller).</span></span>
* <span data-ttu-id="9e0d1-110">[Git](https://git-scm.com/downloads).</span><span class="sxs-lookup"><span data-stu-id="9e0d1-110">[Git](https://git-scm.com/downloads).</span></span>
* <span data-ttu-id="9e0d1-111">Bir [etkin Azure aboneliği](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9e0d1-111">An [active Azure subscription](https://azure.microsoft.com/pricing/free-trial/).</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="download-hello-sample"></a><span data-ttu-id="9e0d1-112">Merhaba örnek indirme</span><span class="sxs-lookup"><span data-stu-id="9e0d1-112">Download hello sample</span></span>

<span data-ttu-id="9e0d1-113">Bir terminal penceresi komutu tooclone hello örnek uygulama havuzu tooyour yerel makine aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9e0d1-113">In a terminal window, run hello following command tooclone hello sample app repository tooyour local machine:</span></span>

```bash
git clone https://github.com/Azure-Samples/ruby-docs-hello-world
```

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="run-hello-application-locally"></a><span data-ttu-id="9e0d1-114">Merhaba uygulama yerel olarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="9e0d1-114">Run hello application locally</span></span>

<span data-ttu-id="9e0d1-115">Merhaba uygulama toowork sırada Hello rayları sunucu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9e0d1-115">Run hello rails server in order for hello application toowork.</span></span> <span data-ttu-id="9e0d1-116">Değiştirme toohello *Merhaba Dünya* dizin ve hello `rails server` başlatır hello sunucu komutu.</span><span class="sxs-lookup"><span data-stu-id="9e0d1-116">Change toohello *hello-world* directory, and hello `rails server` command starts hello server.</span></span>

```bash
cd hello-world\bin
rails server
```
    
<span data-ttu-id="9e0d1-117">Web tarayıcınız üzerinden gidin çok`http://localhost:3000` tootest hello uygulamasını yerel olarak.</span><span class="sxs-lookup"><span data-stu-id="9e0d1-117">Using your web browser, navigate too`http://localhost:3000` tootest hello app locally.</span></span>  

![Merhaba Dünya](./media/app-service-linux-ruby-get-started/hello-world.png)

## <a name="modify-app-toodisplay-welcome-message"></a><span data-ttu-id="9e0d1-119">Uygulama toodisplay Hoş Geldiniz iletisi değiştirme</span><span class="sxs-lookup"><span data-stu-id="9e0d1-119">Modify app toodisplay welcome message</span></span>

<span data-ttu-id="9e0d1-120">Hoş Geldiniz iletisi görüntüler şekilde hello uygulama değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9e0d1-120">Modify hello application so it displays a welcome message.</span></span> <span data-ttu-id="9e0d1-121">Merhaba uygulamanın denetleyicisini selamlama iletisine HTML toohello tarayıcı olarak döndürecek şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9e0d1-121">Change hello application's controller so it returns hello message as HTML toohello browser.</span></span> 

<span data-ttu-id="9e0d1-122">Açık *~/workspace/hello-world/app/controllers/application_controller.rb* düzenlemek için.</span><span class="sxs-lookup"><span data-stu-id="9e0d1-122">Open *~/workspace/hello-world/app/controllers/application_controller.rb* for editing.</span></span> <span data-ttu-id="9e0d1-123">Merhaba değiştirme `ApplicationController` sınıfı toolook hello kodu örneği aşağıdaki gibi:</span><span class="sxs-lookup"><span data-stu-id="9e0d1-123">Modify hello `ApplicationController` class toolook like hello following code sample:</span></span>

  ```ruby
  class ApplicationController > ActionController :: base
    protect_from_forgery with: :exception 
    def hello
      render html: "Hello, world from Azure Web App on Linux!"
    end
  end
  ```

<span data-ttu-id="9e0d1-124">Uygulamanız şimdi yapılandırıldı.</span><span class="sxs-lookup"><span data-stu-id="9e0d1-124">Your app is now configured.</span></span> <span data-ttu-id="9e0d1-125">Web tarayıcınız üzerinden gidin çok`http://localhost:3000` tooconfirm hello kök giriş sayfası.</span><span class="sxs-lookup"><span data-stu-id="9e0d1-125">Using your web browser, navigate too`http://localhost:3000` tooconfirm hello root landing page.</span></span>

![Yapılandırılmış Merhaba Dünya](./media/app-service-linux-ruby-get-started/hello-world-configured.png)

[!INCLUDE [Try Cloud Shell](../../includes/cloud-shell-try-it.md)]

## <a name="create-a-ruby-web-app-on-azure"></a><span data-ttu-id="9e0d1-127">Azure üzerinde bir Söyleniş web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="9e0d1-127">Create a Ruby web app on Azure</span></span>

<span data-ttu-id="9e0d1-128">Kullanım hello [az uygulama hizmeti planı oluşturma](https://docs.microsoft.com/cli/azure/appservice/plan#create) komutu toocreate web uygulamanız için bir app service planı.</span><span class="sxs-lookup"><span data-stu-id="9e0d1-128">Use hello [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) command toocreate an app service plan for your web app.</span></span> 
 
```azurecli-interactive
  az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --is-linux
```

<span data-ttu-id="9e0d1-129">Ardından, hello sorun [az webapp oluşturmak](https://docs.microsoft.com/cli/azure/webapp) yeni oluşturulan hello hizmet planı kullanan komut toocreate hello web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="9e0d1-129">Next, issue hello [az webapp create](https://docs.microsoft.com/cli/azure/webapp) command toocreate hello web app that uses hello newly created service plan.</span></span> <span data-ttu-id="9e0d1-130">Bu hello çalışma zamanı çok ayarlamak fark`ruby|2.3`.</span><span class="sxs-lookup"><span data-stu-id="9e0d1-130">Notice that hello runtime is set too`ruby|2.3`.</span></span> <span data-ttu-id="9e0d1-131">Tooreplace unutmayın `<app name>` benzersiz bir uygulama adına sahip.</span><span class="sxs-lookup"><span data-stu-id="9e0d1-131">Don't forget tooreplace `<app name>` with a unique app name.</span></span>

```azurecli-interactive
  az webapp create --resource-group myResourceGroup --plan myAppServicePlan --name <app name> --runtime "ruby|2.3" --deployment-local-git
```

<span data-ttu-id="9e0d1-132">Merhaba web uygulaması oluşturulduktan sonra bir **genel bakış** kullanılabilir tooview sayfasıdır.</span><span class="sxs-lookup"><span data-stu-id="9e0d1-132">Once hello web app is created, an **Overview** page is available tooview.</span></span> <span data-ttu-id="9e0d1-133">Tooit gidin.</span><span class="sxs-lookup"><span data-stu-id="9e0d1-133">Navigate tooit.</span></span> <span data-ttu-id="9e0d1-134">Giriş sayfası aşağıdaki hello görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="9e0d1-134">hello following splash page is displayed:</span></span>

![Giriş sayfası](./media/app-service-linux-ruby-get-started/splash-page.png)


## <a name="deploy-your-application"></a><span data-ttu-id="9e0d1-136">Uygulamanızı dağıtmak</span><span class="sxs-lookup"><span data-stu-id="9e0d1-136">Deploy your application</span></span>

<span data-ttu-id="9e0d1-137">Git toodeploy hello Ruby uygulaması tooAzure kullanın.</span><span class="sxs-lookup"><span data-stu-id="9e0d1-137">Use Git toodeploy hello Ruby application tooAzure.</span></span> <span data-ttu-id="9e0d1-138">yapılandırılmış bir Git dağıtımı Hello web uygulaması zaten var.</span><span class="sxs-lookup"><span data-stu-id="9e0d1-138">hello web app already has a Git deployment configured.</span></span> <span data-ttu-id="9e0d1-139">Vererek hello dağıtım URL'si alabilir bir [az webapp dağıtım](https://docs.microsoft.com/cli/azure/webapp/deployment) komutu.</span><span class="sxs-lookup"><span data-stu-id="9e0d1-139">You can retrieve hello deployment URL by issuing an [az webapp deployment](https://docs.microsoft.com/cli/azure/webapp/deployment) command.</span></span>  

```bash
az webapp deployment source show --name <app name> --resource-group myResourceGroup
```

<span data-ttu-id="9e0d1-140">Git URL'si hello dikkat edin, web uygulaması adınıza göre form aşağıdaki hello sahiptir:</span><span class="sxs-lookup"><span data-stu-id="9e0d1-140">Notice that hello Git URL has hello following form based on your web app name:</span></span>

```bash
https://<your web app name>.scm.azurewebsites.net/<your web app name>.git
```

[!INCLUDE [Clean-up section](../../includes/configure-deployment-user-no-h.md)]

<span data-ttu-id="9e0d1-141">Komutları toodeploy hello yerel uygulama tooyour Azure Web sitesinde aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9e0d1-141">Run hello following commands toodeploy hello local application tooyour Azure website:</span></span>

```bash
git remote add azure <Git deployment URL from above>
git add -A
git commit -m "Initial deployment commit"
git push azure master
```

<span data-ttu-id="9e0d1-142">Merhaba uzak dağıtım işlemlerini Başarı Raporu onaylayın.</span><span class="sxs-lookup"><span data-stu-id="9e0d1-142">Confirm that hello remote deployment operations report success.</span></span> <span data-ttu-id="9e0d1-143">Merhaba komutları ürettiği benzer toohello metin aşağıdaki çıktı:</span><span class="sxs-lookup"><span data-stu-id="9e0d1-143">hello commands produce output similar toohello following text:</span></span>

```bash
remote: Using sass-rails 5.0.6
remote: Updating files in vendor/cache
remote: Bundle gems are installed into ./vendor/bundle
remote: Updating files in vendor/cache
remote: ~site/repository
remote: Finished successfully.
remote: Running post deployment command(s)...
remote: Deployment successful.
toohttps://<your web app name>.scm.azurewebsites.net/<your web app name>.git
  579ccb....2ca5f31  master -> master
myuser@ubuntu1234:~workspace/<app name>$
```

<span data-ttu-id="9e0d1-144">Merhaba dağıtım tamamlandıktan sonra web uygulamanız için hello dağıtım tootake etkisi hello kullanarak yeniden [az webapp yeniden](https://docs.microsoft.com/cli/azure/webapp#restart) aşağıda gösterildiği gibi komut:</span><span class="sxs-lookup"><span data-stu-id="9e0d1-144">Once hello deployment has completed, restart your web app for hello deployment tootake effect by using hello [az webapp restart](https://docs.microsoft.com/cli/azure/webapp#restart) command, as shown here:</span></span>

```azurecli-interactive 
az webapp restart --name <app name> --resource-group myResourceGroup
```

<span data-ttu-id="9e0d1-145">Tooyour site gidin ve hello sonuçlarını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="9e0d1-145">Navigate tooyour site and verify hello results.</span></span>

```bash
http://<your web app name>.azurewebsites.net
```
![güncelleştirilmiş web uygulaması](./media/app-service-linux-ruby-get-started/hello-world-updated.png)

> [!NOTE]
> <span data-ttu-id="9e0d1-147">Merhaba uygulama yeniden başlatılırken bir HTTP durum kodu toobrowse hello site sonuçlarında çalışırken `Error 503 Server unavailable`.</span><span class="sxs-lookup"><span data-stu-id="9e0d1-147">While hello app is restarting, attempting toobrowse hello site results in an HTTP status code `Error 503 Server unavailable`.</span></span> <span data-ttu-id="9e0d1-148">Birkaç dakika sürebilir toofully yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="9e0d1-148">It may take a few minutes toofully restart.</span></span>
>

[!INCLUDE [Clean-up section](../../includes/cli-script-clean-up.md)]


## <a name="next-steps"></a><span data-ttu-id="9e0d1-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9e0d1-149">Next steps</span></span>

[<span data-ttu-id="9e0d1-150">Azure App Service Web uygulaması Linux SSS</span><span class="sxs-lookup"><span data-stu-id="9e0d1-150">Azure App Service Web App on Linux FAQ</span></span>](https://docs.microsoft.com/azure/app-service-web/app-service-linux-faq.md)