---
title: "aaaDeploy Sails.js web uygulaması tooAzure App Service | Microsoft Docs"
description: "Bilgi nasıl toodeploy bir Node.js uygulamasını Azure App Service. Bu öğretici nasıl toodeploy bir Sails.js web uygulaması gösterir."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 8877ddc8-1476-45ae-9e7f-3c75917b4564
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: f5b2518b9c87c040845f7268763862be8c15e83e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-sailsjs-web-app-tooazure-app-service"></a><span data-ttu-id="c8f22-104">Sails.js web uygulaması tooAzure uygulama hizmeti dağıtma</span><span class="sxs-lookup"><span data-stu-id="c8f22-104">Deploy a Sails.js web app tooAzure App Service</span></span>
<span data-ttu-id="c8f22-105">Bu öğretici şunların nasıl yapıldığını gösterir toodeploy Sails.js uygulama tooAzure uygulama hizmeti.</span><span class="sxs-lookup"><span data-stu-id="c8f22-105">This tutorial shows you how toodeploy a Sails.js app tooAzure App Service.</span></span> <span data-ttu-id="c8f22-106">Merhaba işleminde bazı genel bilgi nasıl glean tooconfigure, App Service'te Node.js uygulaması toorun.</span><span class="sxs-lookup"><span data-stu-id="c8f22-106">In hello process, you can glean some general knowledge on how tooconfigure your Node.js app toorun in App Service.</span></span>

<span data-ttu-id="c8f22-107">Burada, yararlı becerileri ister öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="c8f22-107">Here, you will learn useful skills like:</span></span>

* <span data-ttu-id="c8f22-108">App Service içinde çalıştırmak Sails.js uygulama yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c8f22-108">Configure a Sails.js app run in App Service.</span></span>
* <span data-ttu-id="c8f22-109">Merhaba komut satırından uygulama tooApp hizmet dağıtın.</span><span class="sxs-lookup"><span data-stu-id="c8f22-109">Deploy an app tooApp Service from hello command line.</span></span>
* <span data-ttu-id="c8f22-110">Stderr ve stdout günlükleri tootroubleshoot dağıtım sorunları okuyun.</span><span class="sxs-lookup"><span data-stu-id="c8f22-110">Read stderr and stdout logs tootroubleshoot any deployment issues.</span></span>
* <span data-ttu-id="c8f22-111">Ortam değişkenleri kaynak denetimi dışında depolar.</span><span class="sxs-lookup"><span data-stu-id="c8f22-111">Store environment variables outside of source control.</span></span>
* <span data-ttu-id="c8f22-112">Uygulamanızdan Azure ortam değişkenlerine erişim.</span><span class="sxs-lookup"><span data-stu-id="c8f22-112">Access Azure environment variables from your app.</span></span>
* <span data-ttu-id="c8f22-113">Tooa veritabanı (MongoDB) bağlayın.</span><span class="sxs-lookup"><span data-stu-id="c8f22-113">Connect tooa database (MongoDB).</span></span>

<span data-ttu-id="c8f22-114">Sails.js bilgiye sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c8f22-114">You should have working knowledge of Sails.js.</span></span> <span data-ttu-id="c8f22-115">Bu öğretici hedeflenen toohelp toorunning Sail.js genel sorunları ile ilgili değildir.</span><span class="sxs-lookup"><span data-stu-id="c8f22-115">This tutorial is not intended toohelp you with issues related toorunning Sail.js in general.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="c8f22-116">CLI sürümleri toocomplete hello görevi</span><span class="sxs-lookup"><span data-stu-id="c8f22-116">CLI versions toocomplete hello task</span></span>

<span data-ttu-id="c8f22-117">CLI sürümleri aşağıdaki hello birini kullanarak hello görevi tamamlamak:</span><span class="sxs-lookup"><span data-stu-id="c8f22-117">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="c8f22-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – bizim CLI hello Klasik ve kaynak yönetimi dağıtım modelleri için</span><span class="sxs-lookup"><span data-stu-id="c8f22-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span>
- <span data-ttu-id="c8f22-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) -bizim nesil CLI hello kaynak yönetimi dağıtım modeli için</span><span class="sxs-lookup"><span data-stu-id="c8f22-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) - our next generation CLI for hello resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c8f22-120">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="c8f22-120">Prerequisites</span></span>
* [<span data-ttu-id="c8f22-121">Node.js</span><span class="sxs-lookup"><span data-stu-id="c8f22-121">Node.js</span></span>](https://nodejs.org/)
* [<span data-ttu-id="c8f22-122">Sails.js</span><span class="sxs-lookup"><span data-stu-id="c8f22-122">Sails.js</span></span>](http://sailsjs.org/get-started)
* [<span data-ttu-id="c8f22-123">Git</span><span class="sxs-lookup"><span data-stu-id="c8f22-123">Git</span></span>](http://www.git-scm.com/downloads)
* [<span data-ttu-id="c8f22-124">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c8f22-124">Azure CLI 2.0</span></span>](/cli/azure/install-az-cli2)
* <span data-ttu-id="c8f22-125">Bir Microsoft Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="c8f22-125">A Microsoft Azure account.</span></span> <span data-ttu-id="c8f22-126">Bir hesabınız yoksa, [ücretsiz deneme için kaydolabilir](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) veya [Visual Studio abone avantajlarınızı etkinleştirebilirsiniz.](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="c8f22-126">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="c8f22-127">Azure hesabınız olmadan [App Service'i Deneyebilirsiniz](https://azure.microsoft.com/try/app-service/).</span><span class="sxs-lookup"><span data-stu-id="c8f22-127">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="c8f22-128">Bir başlangıç uygulaması oluşturun ve tooan saat--beraberinde, gerekli herhangi bir kredi kartı veya bir taahhüt yürütebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8f22-128">Create a starter app and play with it for up tooan hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a><span data-ttu-id="c8f22-129">1. adım: Oluşturmak ve Sails.js uygulamayı yerel olarak yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c8f22-129">Step 1: Create and configure a Sails.js app locally</span></span>
<span data-ttu-id="c8f22-130">İlk olarak, hızlı bir şekilde varsayılan Sails.js uygulama geliştirme ortamınızda aşağıdaki adımları izleyerek oluşturun:</span><span class="sxs-lookup"><span data-stu-id="c8f22-130">First, quickly create a default Sails.js app in your development environment by following these steps:</span></span>

1. <span data-ttu-id="c8f22-131">Tercih ettiğiniz komut satırı Terminalini açın hello ve `CD` tooa çalışma dizini.</span><span class="sxs-lookup"><span data-stu-id="c8f22-131">Open hello command-line terminal of your choice and `CD` tooa working directory.</span></span>
2. <span data-ttu-id="c8f22-132">Sails.js uygulama oluşturun ve çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c8f22-132">Create a Sails.js app and run it:</span></span>

        sails new <app_name>
        cd <app_name>
        sails lift

    <span data-ttu-id="c8f22-133">Http://localhost:1377 toohello varsayılan giriş sayfasına gidebilirsiniz emin olun.</span><span class="sxs-lookup"><span data-stu-id="c8f22-133">Make sure you can navigate toohello default home page at http://localhost:1377.</span></span>

1. <span data-ttu-id="c8f22-134">Ardından, Azure günlüğünü etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="c8f22-134">Next, enable logging for Azure.</span></span> <span data-ttu-id="c8f22-135">Kök dizininizde adlı bir dosya oluşturun `iisnode.yml` ve hello aşağıdaki iki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c8f22-135">In your root directory, create a file called `iisnode.yml` and add hello following two lines:</span></span>

        loggingEnabled: true
        logDirectory: iisnode

    <span data-ttu-id="c8f22-136">Günlüğü Merhaba şimdi etkin [iisnode](https://github.com/tjanczuk/iisnode) server Azure App Service Node.js uygulamalarını toorun kullanır.</span><span class="sxs-lookup"><span data-stu-id="c8f22-136">Logging is now enabled for hello [iisnode](https://github.com/tjanczuk/iisnode) server that Azure App Service uses toorun Node.js apps.</span></span> 
    <span data-ttu-id="c8f22-137">Bunun nasıl çalıştığı hakkında daha fazla bilgi için bkz: [nasıl toodebug bir Node.js web uygulamasını Azure App Service'te](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="c8f22-137">For more information on how this works, see [How toodebug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

2. <span data-ttu-id="c8f22-138">Ardından, hello Sails.js uygulama toouse Azure ortam değişkenlerini yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="c8f22-138">Next, configure hello Sails.js app toouse Azure environment variables.</span></span> <span data-ttu-id="c8f22-139">Üretim ortamınıza config/env/Production.js tooconfigure açıp ayarlamak `port` ve `hookTimeout`:</span><span class="sxs-lookup"><span data-stu-id="c8f22-139">Open config/env/production.js tooconfigure your production environment, and set `port` and `hookTimeout`:</span></span>

        module.exports = {

            // Use process.env.port toohandle web requests toohello default HTTP port
            port: process.env.port,
            // Increase hooks timout too30 seconds
            // This avoids hello Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    <span data-ttu-id="c8f22-140">Bu yapılandırma ayarları için belgeler bulabilirsiniz [Sails.js belgelerine](http://sailsjs.org/documentation/reference/configuration/sails-config).</span><span class="sxs-lookup"><span data-stu-id="c8f22-140">You can find documentation for these configuration settings in the  [Sails.js Documentation](http://sailsjs.org/documentation/reference/configuration/sails-config).</span></span>

4. <span data-ttu-id="c8f22-141">Toouse istediğiniz İleri stillerinizin hello Node.js sürümü.</span><span class="sxs-lookup"><span data-stu-id="c8f22-141">Next, hardcode hello Node.js version you want toouse.</span></span> <span data-ttu-id="c8f22-142">Package.json'da, hello aşağıdakileri ekleyin `engines` istediğimiz özelliği tooset hello Node.js sürüm tooone.</span><span class="sxs-lookup"><span data-stu-id="c8f22-142">In package.json, add hello following `engines` property tooset hello Node.js version tooone that we want.</span></span>

        "engines": {
            "node": "6.9.1"
        },

5. <span data-ttu-id="c8f22-143">Son olarak, bir Git deposunu başlatmak ve dosyalarınızı uygulayın.</span><span class="sxs-lookup"><span data-stu-id="c8f22-143">Finally, initialize a Git repository and commit your files.</span></span> <span data-ttu-id="c8f22-144">İçinde uygulama kökü (package.json olduğu) Merhaba, Git komutlarını aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="c8f22-144">In hello application root (where package.json is), run hello following Git commands:</span></span>

        git init
        git add .
        git commit -m "<your commit message>"

<span data-ttu-id="c8f22-145">Kodunuzu dağıtılan hazır toobe ' dir.</span><span class="sxs-lookup"><span data-stu-id="c8f22-145">Your code is ready toobe deployed.</span></span> 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a><span data-ttu-id="c8f22-146">2. adım: Azure bir uygulama oluşturun ve Sails.js dağıtma</span><span class="sxs-lookup"><span data-stu-id="c8f22-146">Step 2: Create an Azure app and deploy Sails.js</span></span>

<span data-ttu-id="c8f22-147">Ardından, Azure'da hello uygulama hizmeti kaynak oluşturup Sails.js uygulama tooit dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8f22-147">Next, create hello App Service resource in Azure and deploy your Sails.js app tooit.</span></span>

1. <span data-ttu-id="c8f22-148">tooAzure günlüğüne şu şekilde:</span><span class="sxs-lookup"><span data-stu-id="c8f22-148">log in tooAzure like so:</span></span>

        az login

    <span data-ttu-id="c8f22-149">Merhaba komut istemi toocontinue hello tarayıcı Azure aboneliğiniz olan bir Microsoft hesabı ile oturum açma izleyin.</span><span class="sxs-lookup"><span data-stu-id="c8f22-149">Follow hello prompt toocontinue hello login in a browser with a Microsoft account that has your Azure subscription.</span></span>

3. <span data-ttu-id="c8f22-150">Merhaba dağıtım kullanıcı için uygulama hizmeti ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c8f22-150">Set hello deployment user for App Service.</span></span> <span data-ttu-id="c8f22-151">Kodu daha sonra bu kimlik bilgilerini kullanarak dağıtacaksınız.</span><span class="sxs-lookup"><span data-stu-id="c8f22-151">You will deploy code using these credentials later.</span></span>
   
        az appservice web deployment user set --user-name <username> --password <password>

3. <span data-ttu-id="c8f22-152">Oluşturma bir [kaynak grubu](../azure-resource-manager/resource-group-overview.md) bir ada sahip.</span><span class="sxs-lookup"><span data-stu-id="c8f22-152">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with a name.</span></span> <span data-ttu-id="c8f22-153">Bu Node.js öğreticisi için nedir gerçekten tooknow gerekmez.</span><span class="sxs-lookup"><span data-stu-id="c8f22-153">For this Node.js tutorial, you don't really need tooknow what it is.</span></span>

        az group create --location "<location>" --name my-sailsjs-app-group

    <span data-ttu-id="c8f22-154">toosee hangi olası değerler için kullanabilmeniz için `<location>`, hello kullan `az appservice list-locations` CLI komutu.</span><span class="sxs-lookup"><span data-stu-id="c8f22-154">toosee what possible values you can use for `<location>`, use hello `az appservice list-locations` CLI command.</span></span>

3. <span data-ttu-id="c8f22-155">"Serbest" oluşturmak [uygulama hizmeti planı](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) bir ada sahip.</span><span class="sxs-lookup"><span data-stu-id="c8f22-155">Create a "FREE" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) with a name.</span></span> <span data-ttu-id="c8f22-156">Bu Node.js öğreticisi için yalnızca, web uygulamaları için bu plan ücret olmaz olduğunu bilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8f22-156">For this Node.js tutorial, just know that you won't be charged for web apps in this plan.</span></span>

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. <span data-ttu-id="c8f22-157">`<app_name>` içinde benzersiz bir ada sahip yeni bir web uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c8f22-157">Create a new web app with a unique name in `<app_name>`.</span></span>

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a><span data-ttu-id="c8f22-158">Adım 3: Yapılandırma ve Sails.js uygulamanızı dağıtma</span><span class="sxs-lookup"><span data-stu-id="c8f22-158">Step 3: Configure and deploy your Sails.js app</span></span>

1. <span data-ttu-id="c8f22-159">Yerel Git dağıtımı yeni web uygulamanız için komutu aşağıdaki hello ile yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="c8f22-159">Configure local Git deployment for your new web app with hello following command:</span></span>

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="c8f22-160">Bu hello uzak Git deposu yapılandırılmış anlamına gelir bunun gibi bir JSON çıktısını alırsınız:</span><span class="sxs-lookup"><span data-stu-id="c8f22-160">You will get a JSON output like this, which means that hello remote Git repository is configured:</span></span>

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. <span data-ttu-id="c8f22-161">Yerel deposu için uzak bir Git olarak hello JSON Hello URL'si ekleyin (adlı `azure` basitleştirmek için).</span><span class="sxs-lookup"><span data-stu-id="c8f22-161">Add hello URL in hello JSON as a Git remote for your local repository (called `azure` for simplicity).</span></span>

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. <span data-ttu-id="c8f22-162">Örnek kod toohello dağıtmak `azure` Git uzaktan.</span><span class="sxs-lookup"><span data-stu-id="c8f22-162">Deploy your sample code toohello `azure` Git remote.</span></span> <span data-ttu-id="c8f22-163">İstendiğinde, daha önce yapılandırılmış hello dağıtım kimlik bilgileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="c8f22-163">When prompted, use hello deployment credentials you configured earlier.</span></span>

        git push azure master

7. <span data-ttu-id="c8f22-164">Son olarak, yalnızca dinamik Azure uygulamanızı hello tarayıcıda başlatın:</span><span class="sxs-lookup"><span data-stu-id="c8f22-164">Finally, just launch your live Azure app in hello browser:</span></span>

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="c8f22-165">Artık görmelisiniz aynı Sails.js giriş sayfası hello.</span><span class="sxs-lookup"><span data-stu-id="c8f22-165">You should now see hello same Sails.js home page.</span></span>

    ![](./media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a><span data-ttu-id="c8f22-166">Dağıtımınızın sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="c8f22-166">Troubleshoot your deployment</span></span>
<span data-ttu-id="c8f22-167">Sails.js uygulamanızı App Service içinde herhangi bir nedenle başarısız olursa, hello stderr günlüklerini bulmak toohelp giderme.</span><span class="sxs-lookup"><span data-stu-id="c8f22-167">If your Sails.js application fails for some reason in App Service, find hello stderr logs toohelp troubleshoot it.</span></span>
<span data-ttu-id="c8f22-168">Daha fazla bilgi için bkz: [nasıl toodebug bir Node.js web uygulamasını Azure App Service'te](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="c8f22-168">For more information, see [How toodebug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>
<span data-ttu-id="c8f22-169">Merhaba uygulama başarıyla başlatılmış olup olmadığını hello stdout günlük göstermelidir hello tanıdık ileti:</span><span class="sxs-lookup"><span data-stu-id="c8f22-169">If hello app has started successfully, hello stdout log should show you hello familiar message:</span></span>

                   .-..-.
    
       Sails              <|    .-..-.
       v0.12.11            |\
                          /|.\
                         / || \
                       ,'  |'  \
                    .-'.-==|/_--'
                    `--'-------' 
       __---___--___---___--___---___--___
     ____---___--___---___--___---___--___-__

    Server lifted in `D:\home\site\wwwroot`
    toosee your app, visit http://localhost:\\.\pipe\c775303c-0ebc-4854-8ddd-2e280aabccac
    tooshut down Sails, press <CTRL> + C at any time.

<span data-ttu-id="c8f22-170">Merhaba stdout hello günlüklerinde kesinliği denetleyebilirsiniz [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) dosya.</span><span class="sxs-lookup"><span data-stu-id="c8f22-170">You can control granularity of hello stdout logs in hello [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) file.</span></span>

## <a name="connect-tooa-database-in-azure"></a><span data-ttu-id="c8f22-171">Azure tooa veritabanına bağlan</span><span class="sxs-lookup"><span data-stu-id="c8f22-171">Connect tooa database in Azure</span></span>
<span data-ttu-id="c8f22-172">tooconnect tooa veritabanı Azure, Azure, Azure SQL Database, MySQL, MongoDB, Azure (Redis) önbelleği, vb. gibi tercih ettiğiniz hello veritabanı oluşturun ve hello karşılık gelen kullanmak [veri deposu bağdaştırıcısı](https://github.com/balderdashy/sails#compatibility) tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="c8f22-172">tooconnect tooa database in Azure, you create hello database of your choice in Azure, such as Azure SQL Database, MySQL, MongoDB, Azure (Redis) Cache, etc., and use hello corresponding [datastore adapter](https://github.com/balderdashy/sails#compatibility) tooconnect tooit.</span></span> <span data-ttu-id="c8f22-173">Merhaba bu bölümdeki adımları şunları nasıl yapacağınızı kullanarak tooconnect tooMongoDB bir [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) MongoDB istemci bağlantılarını desteklemek veritabanı.</span><span class="sxs-lookup"><span data-stu-id="c8f22-173">hello steps in this section show you how tooconnect tooMongoDB by using an [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) database, which can support MongoDB client connections.</span></span>

1. <span data-ttu-id="c8f22-174">[MongoDB protokol desteği ile Cosmos DB hesabı oluşturma](../documentdb/documentdb-create-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="c8f22-174">[Create a Cosmos DB account with MongoDB protocol support](../documentdb/documentdb-create-mongodb-account.md).</span></span>
2. <span data-ttu-id="c8f22-175">[Cosmos DB koleksiyonu ve veritabanı oluşturma](../documentdb/documentdb-create-collection.md).</span><span class="sxs-lookup"><span data-stu-id="c8f22-175">[Create a Cosmos DB collection and database](../documentdb/documentdb-create-collection.md).</span></span> <span data-ttu-id="c8f22-176">Merhaba koleksiyonunun Hello adı önemli değildir, ancak Sails.js bağlandığınızda hello veritabanının hello adı gerekir.</span><span class="sxs-lookup"><span data-stu-id="c8f22-176">hello name of hello collection doesn't matter, but you need hello name of hello database when you connect from Sails.js.</span></span>
3. <span data-ttu-id="c8f22-177">[Cosmos DB veritabanınızı Hello bağlantı bilgilerini bulmak](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="c8f22-177">[Find hello connection information for your Cosmos DB database](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span></span>
2. <span data-ttu-id="c8f22-178">Komut satırı, terminal durumundan hello MongoDB bağdaştırıcısı yükleyin:</span><span class="sxs-lookup"><span data-stu-id="c8f22-178">From your command-line terminal, install hello MongoDB adapter:</span></span>

        npm install sails-mongo --save

3. <span data-ttu-id="c8f22-179">Config/Connections.js açın ve bağlantı nesnesi toohello listesi aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c8f22-179">Open config/connections.js and add hello following connection object toohello list:</span></span>

        docDbMongo: {
            adapter: 'sails-mongo',
            user: process.env.dbuser,
            password: process.env.dbpassword,
            host: process.env.dbhost,
            port: process.env.dbport,
            database: process.env.dbname,
            ssl: true
        },

    > [!NOTE] 
    > <span data-ttu-id="c8f22-180">Merhaba `ssl: true` seçeneği önemlidir çünkü [Cosmos DB gerektirir](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="c8f22-180">hello `ssl: true` option is important because [Cosmos DB requires it](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 
    >
    >

4. <span data-ttu-id="c8f22-181">Her ortam değişkeni için (`process.env.*`), tooset ihtiyacınız App Service içinde.</span><span class="sxs-lookup"><span data-stu-id="c8f22-181">For each environment variable (`process.env.*`), you need tooset it in App Service.</span></span> <span data-ttu-id="c8f22-182">toodo terminal durumundan komutları aşağıdaki Bu, çalışma hello.</span><span class="sxs-lookup"><span data-stu-id="c8f22-182">toodo this, run hello following commands from your terminal.</span></span> <span data-ttu-id="c8f22-183">Merhaba bağlantı bilgilerini Cosmos DB için kullanın.</span><span class="sxs-lookup"><span data-stu-id="c8f22-183">Use hello connection information for your Cosmos DB.</span></span>

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="c8f22-184">Azure uygulama ayarlarında ayarlarınızı koyma, kaynak denetimi (Git) dışında hassas verileri tutar.</span><span class="sxs-lookup"><span data-stu-id="c8f22-184">Putting your settings in Azure app settings keeps sensitive data out of your source control (Git).</span></span> <span data-ttu-id="c8f22-185">Ardından, geliştirme yapılandıracağınız ortamı toouse hello aynı bağlantı bilgileri.</span><span class="sxs-lookup"><span data-stu-id="c8f22-185">Next, you will configure your development environment toouse hello same connection information.</span></span>
5. <span data-ttu-id="c8f22-186">Config/Local.js açın ve bağlantıları nesne aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c8f22-186">Open config/local.js and add hello following connections object:</span></span>

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    <span data-ttu-id="c8f22-187">Bu yapılandırma hello yerel ortamınıza config/connections.js dosyanızdaki hello ayarları geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="c8f22-187">This configuration overrides hello settings in your config/connections.js file for hello local environment.</span></span> <span data-ttu-id="c8f22-188">Git içinde depolanmaz şekilde bu dosyayı hello varsayılan .gitignore projenizdeki tarafından dışlandı.</span><span class="sxs-lookup"><span data-stu-id="c8f22-188">This file is excluded by hello default .gitignore in your project, so it will not be stored in Git.</span></span> <span data-ttu-id="c8f22-189">Şimdi, Azure web uygulamanız ve yerel geliştirme ortamınızı mümkün tooconnect tooyour Cosmos DB (MongoDB) veritabanı misiniz.</span><span class="sxs-lookup"><span data-stu-id="c8f22-189">Now, you are able tooconnect tooyour Cosmos DB (MongoDB) database both from your Azure web app and from your local development environment.</span></span>
6. <span data-ttu-id="c8f22-190">Üretim ortamınıza config/env/Production.js tooconfigure açın ve hello aşağıdakileri ekleyin `models` nesnesi:</span><span class="sxs-lookup"><span data-stu-id="c8f22-190">Open config/env/production.js tooconfigure your production environment, and add hello following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. <span data-ttu-id="c8f22-191">Geliştirme ortamınızı config/env/Development.js tooconfigure açın ve hello aşağıdakileri ekleyin `models` nesnesi:</span><span class="sxs-lookup"><span data-stu-id="c8f22-191">Open config/env/development.js tooconfigure your development environment, and add hello following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    <span data-ttu-id="c8f22-192">`migrate: 'alter'`Veritabanı geçiş özellikleri toocreate kullanın ve veritabanı koleksiyonları veya tabloları kolayca güncelleştirmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="c8f22-192">`migrate: 'alter'` lets you use database migration features toocreate and update database collections or tables easily.</span></span> <span data-ttu-id="c8f22-193">Ancak, `migrate: 'safe'` Sails.js, toouse izin vermediğinden, Azure (üretim) ortamınız için kullanılan `migrate: 'alter'` bir üretim ortamında (bkz [Sails.js belgelerine](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span><span class="sxs-lookup"><span data-stu-id="c8f22-193">However, `migrate: 'safe'` is used for your Azure (production) environment because Sails.js does not allow you toouse `migrate: 'alter'` in a production environment (see [Sails.js Documentation](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span></span>
8. <span data-ttu-id="c8f22-194">Merhaba terminal, gelen [oluşturmak](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) bir Sails.js [API şeması](http://sailsjs.org/documentation/concepts/blueprints) , normalde sonra çalıştırılır gibi `sails lift` ile Sails.js veritabanı geçiş hello veritabanı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="c8f22-194">From hello terminal, [generate](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) a Sails.js [blueprint API](http://sailsjs.org/documentation/concepts/blueprints) like you normally would, then run `sails lift` to create hello database with Sails.js database migration.</span></span> <span data-ttu-id="c8f22-195">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="c8f22-195">For example:</span></span>

         sails generate api mywidget
         sails lift

    <span data-ttu-id="c8f22-196">Merhaba `mywidget` bu komutu tarafından oluşturulan model boşsa, ancak biz veritabanı bağlantısı sahibiz tooshow kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c8f22-196">hello `mywidget` model generated by this command is empty, but we can use it tooshow that we have database connectivity.</span></span>
    <span data-ttu-id="c8f22-197">Çalıştırdığınızda `sails lift`hello eksik koleksiyonları oluşturur ve tablolar hello için modeller, uygulama kullanır.</span><span class="sxs-lookup"><span data-stu-id="c8f22-197">When you run `sails lift`, it creates hello missing collections and tables for hello models your app uses.</span></span>
9. <span data-ttu-id="c8f22-198">Merhaba tarayıcıda oluşturduğunuz erişim hello şeması API.</span><span class="sxs-lookup"><span data-stu-id="c8f22-198">Access hello blueprint API you just created in hello browser.</span></span> <span data-ttu-id="c8f22-199">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="c8f22-199">For example:</span></span>

        http://localhost:1337/mywidget/create

    <span data-ttu-id="c8f22-200">Merhaba API koleksiyonunuz başarıyla oluşturuldu anlamı hello tarayıcı penceresinde hello oluşturulan girişi geri tooyou döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="c8f22-200">hello API should return hello created entry back tooyou in hello browser window, which means that your collection is created  successfully.</span></span>

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. <span data-ttu-id="c8f22-201">Şimdi, değişiklikleri tooAzure anında ve tooyour uygulama toomake çalışmaya devam ettiğinden emin göz atın.</span><span class="sxs-lookup"><span data-stu-id="c8f22-201">Now, push your changes tooAzure, and browse tooyour app toomake sure it still works.</span></span>

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. <span data-ttu-id="c8f22-202">Azure web uygulamanızın erişim hello şeması API.</span><span class="sxs-lookup"><span data-stu-id="c8f22-202">Access hello blueprint API of your Azure web app.</span></span> <span data-ttu-id="c8f22-203">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="c8f22-203">For example:</span></span>

         http://<appname>.azurewebsites.net/mywidget/create

     <span data-ttu-id="c8f22-204">Merhaba API başka bir yeni giriş döndürürse, Azure web uygulamanızın tooyour Cosmos DB (MongoDB) veritabanı Bahsediyor.</span><span class="sxs-lookup"><span data-stu-id="c8f22-204">If hello API returns another new entry, then your Azure web app is talking tooyour Cosmos DB (MongoDB) database.</span></span>

## <a name="more-resources"></a><span data-ttu-id="c8f22-205">Diğer kaynaklar</span><span class="sxs-lookup"><span data-stu-id="c8f22-205">More resources</span></span>
* [<span data-ttu-id="c8f22-206">Azure App Service'te Node.js web uygulamalarını kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="c8f22-206">Get started with Node.js web apps in Azure App Service</span></span>](app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="c8f22-207">Azure uygulamalarıyla Node.js Modüllerini kullanma</span><span class="sxs-lookup"><span data-stu-id="c8f22-207">Using Node.js Modules with Azure applications</span></span>](../nodejs-use-node-modules-azure-apps.md)
