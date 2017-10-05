---
title: "Azure App Service'e Sails.js web uygulaması dağıtma | Microsoft Docs"
description: "Bir Node.js uygulamasını Azure App Service dağıtmayı öğrenin. Bu öğretici Sails.js web uygulamasının nasıl dağıtılacağını gösterir."
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
ms.openlocfilehash: e36fc5f5273f98c3cca91973db9910f32443ec7c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="deploy-a-sailsjs-web-app-to-azure-app-service"></a><span data-ttu-id="f16ab-104">Azure App Service’e Sails.js web uygulaması dağıtma</span><span class="sxs-lookup"><span data-stu-id="f16ab-104">Deploy a Sails.js web app to Azure App Service</span></span>
<span data-ttu-id="f16ab-105">Bu öğreticide Azure App Service'e Sails.js uygulama dağıtma gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="f16ab-105">This tutorial shows you how to deploy a Sails.js app to Azure App Service.</span></span> <span data-ttu-id="f16ab-106">Bu süreçte bazı App Service içinde çalıştırmak için Node.js uygulamanızı yapılandırma hakkında genel bilgi glean.</span><span class="sxs-lookup"><span data-stu-id="f16ab-106">In the process, you can glean some general knowledge on how to configure your Node.js app to run in App Service.</span></span>

<span data-ttu-id="f16ab-107">Burada, yararlı becerileri ister öğreneceksiniz:</span><span class="sxs-lookup"><span data-stu-id="f16ab-107">Here, you will learn useful skills like:</span></span>

* <span data-ttu-id="f16ab-108">App Service içinde çalıştırmak Sails.js uygulama yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f16ab-108">Configure a Sails.js app run in App Service.</span></span>
* <span data-ttu-id="f16ab-109">Bir uygulamayı, komut satırından App Service'e dağıtın.</span><span class="sxs-lookup"><span data-stu-id="f16ab-109">Deploy an app to App Service from the command line.</span></span>
* <span data-ttu-id="f16ab-110">Dağıtım sorunları gidermek için okuma stderr ve stdout günlükleri.</span><span class="sxs-lookup"><span data-stu-id="f16ab-110">Read stderr and stdout logs to troubleshoot any deployment issues.</span></span>
* <span data-ttu-id="f16ab-111">Ortam değişkenleri kaynak denetimi dışında depolar.</span><span class="sxs-lookup"><span data-stu-id="f16ab-111">Store environment variables outside of source control.</span></span>
* <span data-ttu-id="f16ab-112">Uygulamanızdan Azure ortam değişkenlerine erişim.</span><span class="sxs-lookup"><span data-stu-id="f16ab-112">Access Azure environment variables from your app.</span></span>
* <span data-ttu-id="f16ab-113">Bir veritabanı (MongoDB) bağlayın.</span><span class="sxs-lookup"><span data-stu-id="f16ab-113">Connect to a database (MongoDB).</span></span>

<span data-ttu-id="f16ab-114">Sails.js bilgiye sahip olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f16ab-114">You should have working knowledge of Sails.js.</span></span> <span data-ttu-id="f16ab-115">Bu öğretici Sail.js genel çalıştırma ile ilgili sorunları yardımcı olmak için tasarlanmamıştır.</span><span class="sxs-lookup"><span data-stu-id="f16ab-115">This tutorial is not intended to help you with issues related to running Sail.js in general.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="f16ab-116">Görevi tamamlamak için kullanılacak CLI sürümleri</span><span class="sxs-lookup"><span data-stu-id="f16ab-116">CLI versions to complete the task</span></span>

<span data-ttu-id="f16ab-117">Görevi aşağıdaki CLI sürümlerinden birini kullanarak tamamlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f16ab-117">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="f16ab-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md): Klasik ve kaynak yönetimi dağıtım modellerine yönelik CLI’mız</span><span class="sxs-lookup"><span data-stu-id="f16ab-118">[Azure CLI 1.0](app-service-web-nodejs-sails-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span>
- <span data-ttu-id="f16ab-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md): Kaynak yönetimi dağıtım modeline yönelik yeni nesil CLI'mız</span><span class="sxs-lookup"><span data-stu-id="f16ab-119">[Azure CLI 2.0](app-service-web-nodejs-sails.md) - our next generation CLI for the resource management deployment model</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f16ab-120">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="f16ab-120">Prerequisites</span></span>
* [<span data-ttu-id="f16ab-121">Node.js</span><span class="sxs-lookup"><span data-stu-id="f16ab-121">Node.js</span></span>](https://nodejs.org/)
* [<span data-ttu-id="f16ab-122">Sails.js</span><span class="sxs-lookup"><span data-stu-id="f16ab-122">Sails.js</span></span>](http://sailsjs.org/get-started)
* [<span data-ttu-id="f16ab-123">Git</span><span class="sxs-lookup"><span data-stu-id="f16ab-123">Git</span></span>](http://www.git-scm.com/downloads)
* [<span data-ttu-id="f16ab-124">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="f16ab-124">Azure CLI 2.0</span></span>](/cli/azure/install-az-cli2)
* <span data-ttu-id="f16ab-125">Bir Microsoft Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="f16ab-125">A Microsoft Azure account.</span></span> <span data-ttu-id="f16ab-126">Bir hesabınız yoksa, [ücretsiz deneme için kaydolabilir](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) veya [Visual Studio abone avantajlarınızı etkinleştirebilirsiniz.](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)</span><span class="sxs-lookup"><span data-stu-id="f16ab-126">If you don't have an account, you can [sign up for a free trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) or [activate your Visual Studio subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F).</span></span>

> [!NOTE]
> <span data-ttu-id="f16ab-127">Azure hesabınız olmadan [App Service'i Deneyebilirsiniz](https://azure.microsoft.com/try/app-service/).</span><span class="sxs-lookup"><span data-stu-id="f16ab-127">You can [Try App Service](https://azure.microsoft.com/try/app-service/) without an Azure account.</span></span> <span data-ttu-id="f16ab-128">Başlangıç uygulaması oluşturun ve bir saate kadar üzerinde çalışın; kredi kartı veya taahhüt gerekmez.</span><span class="sxs-lookup"><span data-stu-id="f16ab-128">Create a starter app and play with it for up to an hour--no credit card required, no commitments.</span></span>
> 
> 

## <a name="step-1-create-and-configure-a-sailsjs-app-locally"></a><span data-ttu-id="f16ab-129">1. adım: Oluşturmak ve Sails.js uygulamayı yerel olarak yapılandırma</span><span class="sxs-lookup"><span data-stu-id="f16ab-129">Step 1: Create and configure a Sails.js app locally</span></span>
<span data-ttu-id="f16ab-130">İlk olarak, hızlı bir şekilde varsayılan Sails.js uygulama geliştirme ortamınızda aşağıdaki adımları izleyerek oluşturun:</span><span class="sxs-lookup"><span data-stu-id="f16ab-130">First, quickly create a default Sails.js app in your development environment by following these steps:</span></span>

1. <span data-ttu-id="f16ab-131">Tercih ettiğiniz komut satırı Terminalini açın ve `CD` bir çalışma dizini için.</span><span class="sxs-lookup"><span data-stu-id="f16ab-131">Open the command-line terminal of your choice and `CD` to a working directory.</span></span>
2. <span data-ttu-id="f16ab-132">Sails.js uygulama oluşturun ve çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f16ab-132">Create a Sails.js app and run it:</span></span>

        sails new <app_name>
        cd <app_name>
        sails lift

    <span data-ttu-id="f16ab-133">Http://localhost:1377 varsayılan giriş sayfasına gidebilirsiniz emin olun.</span><span class="sxs-lookup"><span data-stu-id="f16ab-133">Make sure you can navigate to the default home page at http://localhost:1377.</span></span>

1. <span data-ttu-id="f16ab-134">Ardından, Azure günlüğünü etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="f16ab-134">Next, enable logging for Azure.</span></span> <span data-ttu-id="f16ab-135">Kök dizininizde adlı bir dosya oluşturun `iisnode.yml` ve aşağıdaki iki satırı ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f16ab-135">In your root directory, create a file called `iisnode.yml` and add the following two lines:</span></span>

        loggingEnabled: true
        logDirectory: iisnode

    <span data-ttu-id="f16ab-136">Günlüğe kaydetme için şimdi etkinleştirildiğinde [iisnode](https://github.com/tjanczuk/iisnode) Azure App Service Node.js uygulamalarını çalıştırmak için kullandığı sunucusuna.</span><span class="sxs-lookup"><span data-stu-id="f16ab-136">Logging is now enabled for the [iisnode](https://github.com/tjanczuk/iisnode) server that Azure App Service uses to run Node.js apps.</span></span> 
    <span data-ttu-id="f16ab-137">Bunun nasıl çalıştığı hakkında daha fazla bilgi için bkz: [Azure App Service'te Node.js web uygulamasına hata ayıklama](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="f16ab-137">For more information on how this works, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

2. <span data-ttu-id="f16ab-138">Ardından, Azure ortam değişkenlerini kullanmak üzere Sails.js uygulamayı yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="f16ab-138">Next, configure the Sails.js app to use Azure environment variables.</span></span> <span data-ttu-id="f16ab-139">Üretim ortamınıza yapılandırmak ve ayarlamak için config/env/production.js açmak `port` ve `hookTimeout`:</span><span class="sxs-lookup"><span data-stu-id="f16ab-139">Open config/env/production.js to configure your production environment, and set `port` and `hookTimeout`:</span></span>

        module.exports = {

            // Use process.env.port to handle web requests to the default HTTP port
            port: process.env.port,
            // Increase hooks timout to 30 seconds
            // This avoids the Sails.js error documented at https://github.com/balderdashy/sails/issues/2691
            hookTimeout: 30000,

            ...
        };

    <span data-ttu-id="f16ab-140">Bu yapılandırma ayarları için belgeler bulabilirsiniz [Sails.js belgelerine](http://sailsjs.org/documentation/reference/configuration/sails-config).</span><span class="sxs-lookup"><span data-stu-id="f16ab-140">You can find documentation for these configuration settings in the  [Sails.js Documentation](http://sailsjs.org/documentation/reference/configuration/sails-config).</span></span>

4. <span data-ttu-id="f16ab-141">Ardından, stillerinizin Node.js sürümünü kullanmak istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="f16ab-141">Next, hardcode the Node.js version you want to use.</span></span> <span data-ttu-id="f16ab-142">Package.json'da, aşağıdakileri ekleyin `engines` istiyoruz bir Node.js sürümünü ayarlamak için özellik.</span><span class="sxs-lookup"><span data-stu-id="f16ab-142">In package.json, add the following `engines` property to set the Node.js version to one that we want.</span></span>

        "engines": {
            "node": "6.9.1"
        },

5. <span data-ttu-id="f16ab-143">Son olarak, bir Git deposunu başlatmak ve dosyalarınızı uygulayın.</span><span class="sxs-lookup"><span data-stu-id="f16ab-143">Finally, initialize a Git repository and commit your files.</span></span> <span data-ttu-id="f16ab-144">(Package.json olduğu) uygulama kök aşağıdaki Git komutları çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f16ab-144">In the application root (where package.json is), run the following Git commands:</span></span>

        git init
        git add .
        git commit -m "<your commit message>"

<span data-ttu-id="f16ab-145">Kodunuzu dağıtılmaya hazırdır.</span><span class="sxs-lookup"><span data-stu-id="f16ab-145">Your code is ready to be deployed.</span></span> 

## <a name="step-2-create-an-azure-app-and-deploy-sailsjs"></a><span data-ttu-id="f16ab-146">2. adım: Azure bir uygulama oluşturun ve Sails.js dağıtma</span><span class="sxs-lookup"><span data-stu-id="f16ab-146">Step 2: Create an Azure app and deploy Sails.js</span></span>

<span data-ttu-id="f16ab-147">Ardından, uygulama hizmeti kaynak oluşturmak ve Sails.js uygulamanızı dağıtma.</span><span class="sxs-lookup"><span data-stu-id="f16ab-147">Next, create the App Service resource in Azure and deploy your Sails.js app to it.</span></span>

1. <span data-ttu-id="f16ab-148">Azure benzer şekilde oturum açın:</span><span class="sxs-lookup"><span data-stu-id="f16ab-148">log in to Azure like so:</span></span>

        az login

    <span data-ttu-id="f16ab-149">Azure aboneliğinizin bulunduğu bir Microsoft hesabıyla tarayıcıda oturum açmaya devam etmek için istemi izleyin.</span><span class="sxs-lookup"><span data-stu-id="f16ab-149">Follow the prompt to continue the login in a browser with a Microsoft account that has your Azure subscription.</span></span>

3. <span data-ttu-id="f16ab-150">App Service için dağıtım kullanıcısını ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="f16ab-150">Set the deployment user for App Service.</span></span> <span data-ttu-id="f16ab-151">Kodu daha sonra bu kimlik bilgilerini kullanarak dağıtacaksınız.</span><span class="sxs-lookup"><span data-stu-id="f16ab-151">You will deploy code using these credentials later.</span></span>
   
        az appservice web deployment user set --user-name <username> --password <password>

3. <span data-ttu-id="f16ab-152">Oluşturma bir [kaynak grubu](../azure-resource-manager/resource-group-overview.md) bir ada sahip.</span><span class="sxs-lookup"><span data-stu-id="f16ab-152">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with a name.</span></span> <span data-ttu-id="f16ab-153">Bu Node.js öğreticisi için gerçekten ne olduğunu bilmeniz gerekmez.</span><span class="sxs-lookup"><span data-stu-id="f16ab-153">For this Node.js tutorial, you don't really need to know what it is.</span></span>

        az group create --location "<location>" --name my-sailsjs-app-group

    <span data-ttu-id="f16ab-154">`<location>` için hangi olası değerleri kullanabileceğinizi görmek için `az appservice list-locations` CLI komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="f16ab-154">To see what possible values you can use for `<location>`, use the `az appservice list-locations` CLI command.</span></span>

3. <span data-ttu-id="f16ab-155">"Serbest" oluşturmak [uygulama hizmeti planı](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) bir ada sahip.</span><span class="sxs-lookup"><span data-stu-id="f16ab-155">Create a "FREE" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) with a name.</span></span> <span data-ttu-id="f16ab-156">Bu Node.js öğreticisi için yalnızca, web uygulamaları için bu plan ücret olmaz olduğunu bilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f16ab-156">For this Node.js tutorial, just know that you won't be charged for web apps in this plan.</span></span>

        az appservice plan create --name my-sailsjs-appservice-plan --resource-group my-sailsjs-app-group --sku FREE

4. <span data-ttu-id="f16ab-157">`<app_name>` içinde benzersiz bir ada sahip yeni bir web uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f16ab-157">Create a new web app with a unique name in `<app_name>`.</span></span>

        az appservice web create --name <app_name> --resource-group my-sailsjs-app-group --plan my-sailsjs-appservice-plan

## <a name="step-3-configure-and-deploy-your-sailsjs-app"></a><span data-ttu-id="f16ab-158">Adım 3: Yapılandırma ve Sails.js uygulamanızı dağıtma</span><span class="sxs-lookup"><span data-stu-id="f16ab-158">Step 3: Configure and deploy your Sails.js app</span></span>

1. <span data-ttu-id="f16ab-159">Şu komutla yeni web uygulamanıza yönelik yerel Git dağıtımını yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="f16ab-159">Configure local Git deployment for your new web app with the following command:</span></span>

        az appservice web source-control config-local-git --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="f16ab-160">Buna benzer bir JSON çıktısı alırsınız ve bu çıktı uzak Git deposunun yapılandırıldığı anlamına gelir:</span><span class="sxs-lookup"><span data-stu-id="f16ab-160">You will get a JSON output like this, which means that the remote Git repository is configured:</span></span>

        {
        "url": "https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git"
        }

6. <span data-ttu-id="f16ab-161">JSON'daki URL'yi yerel deponuz (basit olması açısından `azure` diyelim) için bir uzak Git deposu olarak ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f16ab-161">Add the URL in the JSON as a Git remote for your local repository (called `azure` for simplicity).</span></span>

        git remote add azure https://<deployment_user>@<app_name>.scm.azurewebsites.net/<app_name>.git
   
7. <span data-ttu-id="f16ab-162">Örnek kodunuzu `azure` Git uzak deposuna dağıtın.</span><span class="sxs-lookup"><span data-stu-id="f16ab-162">Deploy your sample code to the `azure` Git remote.</span></span> <span data-ttu-id="f16ab-163">Kimlik bilgisi istendiğinde daha önce yapılandırdığınız dağıtım kimlik bilgilerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="f16ab-163">When prompted, use the deployment credentials you configured earlier.</span></span>

        git push azure master

7. <span data-ttu-id="f16ab-164">Son olarak, yalnızca dinamik Azure uygulamanızı tarayıcıda başlatın:</span><span class="sxs-lookup"><span data-stu-id="f16ab-164">Finally, just launch your live Azure app in the browser:</span></span>

        az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="f16ab-165">Aynı Sails.js giriş sayfası görmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="f16ab-165">You should now see the same Sails.js home page.</span></span>

    ![](./media/app-service-web-nodejs-sails/sails-in-azure.png)

## <a name="troubleshoot-your-deployment"></a><span data-ttu-id="f16ab-166">Dağıtımınızın sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="f16ab-166">Troubleshoot your deployment</span></span>
<span data-ttu-id="f16ab-167">Sails.js uygulamanızı App Service içinde herhangi bir nedenle başarısız olursa, onu gidermenize yardımcı olması için stderr günlüklerini Bul.</span><span class="sxs-lookup"><span data-stu-id="f16ab-167">If your Sails.js application fails for some reason in App Service, find the stderr logs to help troubleshoot it.</span></span>
<span data-ttu-id="f16ab-168">Daha fazla bilgi için bkz: [Azure App Service'te Node.js web uygulamasına hata ayıklama](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="f16ab-168">For more information, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>
<span data-ttu-id="f16ab-169">Uygulama başarıyla başlatılmış olup olmadığını, stdout günlük tanıdık iletisini göstermelidir:</span><span class="sxs-lookup"><span data-stu-id="f16ab-169">If the app has started successfully, the stdout log should show you the familiar message:</span></span>

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
    To see your app, visit http://localhost:\\.\pipe\c775303c-0ebc-4854-8ddd-2e280aabccac
    To shut down Sails, press <CTRL> + C at any time.

<span data-ttu-id="f16ab-170">Stdout günlüklerde kesinliği denetleyebilirsiniz [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) dosya.</span><span class="sxs-lookup"><span data-stu-id="f16ab-170">You can control granularity of the stdout logs in the [config/log.js](http://sailsjs.org/#!/documentation/concepts/Logging) file.</span></span>

## <a name="connect-to-a-database-in-azure"></a><span data-ttu-id="f16ab-171">Azure veritabanına bağlan</span><span class="sxs-lookup"><span data-stu-id="f16ab-171">Connect to a database in Azure</span></span>
<span data-ttu-id="f16ab-172">Azure bir veritabanına bağlanmak için Azure, Azure SQL Database, MySQL, MongoDB, Azure (Redis) önbelleği, vb. gibi tercih ettiğiniz veritabanı oluşturun ve karşılık gelen kullanmak [veri deposu bağdaştırıcısı](https://github.com/balderdashy/sails#compatibility) bağlanmak için.</span><span class="sxs-lookup"><span data-stu-id="f16ab-172">To connect to a database in Azure, you create the database of your choice in Azure, such as Azure SQL Database, MySQL, MongoDB, Azure (Redis) Cache, etc., and use the corresponding [datastore adapter](https://github.com/balderdashy/sails#compatibility) to connect to it.</span></span> <span data-ttu-id="f16ab-173">Bu bölümdeki adımları kullanarak MongoDB için bağlanma Göster bir [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) MongoDB istemci bağlantılarını desteklemek veritabanı.</span><span class="sxs-lookup"><span data-stu-id="f16ab-173">The steps in this section show you how to connect to MongoDB by using an [Azure Cosmos DB](../documentdb/documentdb-protocol-mongodb.md) database, which can support MongoDB client connections.</span></span>

1. <span data-ttu-id="f16ab-174">[MongoDB protokol desteği ile Cosmos DB hesabı oluşturma](../documentdb/documentdb-create-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="f16ab-174">[Create a Cosmos DB account with MongoDB protocol support](../documentdb/documentdb-create-mongodb-account.md).</span></span>
2. <span data-ttu-id="f16ab-175">[Cosmos DB koleksiyonu ve veritabanı oluşturma](../documentdb/documentdb-create-collection.md).</span><span class="sxs-lookup"><span data-stu-id="f16ab-175">[Create a Cosmos DB collection and database](../documentdb/documentdb-create-collection.md).</span></span> <span data-ttu-id="f16ab-176">Koleksiyon adı önemli değildir, ancak Sails.js bağlandığınızda veritabanının adı gerekir.</span><span class="sxs-lookup"><span data-stu-id="f16ab-176">The name of the collection doesn't matter, but you need the name of the database when you connect from Sails.js.</span></span>
3. <span data-ttu-id="f16ab-177">[Cosmos DB veritabanınız için bağlantı bilgilerini bulmak](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="f16ab-177">[Find the connection information for your Cosmos DB database](../cosmos-db/connect-mongodb-account.md#GetCustomConnection).</span></span>
2. <span data-ttu-id="f16ab-178">Komut satırı, terminal durumundan MongoDB bağdaştırıcısı yükleyin:</span><span class="sxs-lookup"><span data-stu-id="f16ab-178">From your command-line terminal, install the MongoDB adapter:</span></span>

        npm install sails-mongo --save

3. <span data-ttu-id="f16ab-179">Config/Connections.js açın ve aşağıdaki bağlantı nesnesi listeye ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f16ab-179">Open config/connections.js and add the following connection object to the list:</span></span>

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
    > <span data-ttu-id="f16ab-180">`ssl: true` Seçeneği önemlidir çünkü [Cosmos DB gerektirir](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="f16ab-180">The `ssl: true` option is important because [Cosmos DB requires it](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 
    >
    >

4. <span data-ttu-id="f16ab-181">Her ortam değişkeni için (`process.env.*`), App Service'te ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f16ab-181">For each environment variable (`process.env.*`), you need to set it in App Service.</span></span> <span data-ttu-id="f16ab-182">Bunu yapmak için terminal durumundan aşağıdaki komutları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f16ab-182">To do this, run the following commands from your terminal.</span></span> <span data-ttu-id="f16ab-183">Cosmos DB için bağlantı bilgisini kullanın.</span><span class="sxs-lookup"><span data-stu-id="f16ab-183">Use the connection information for your Cosmos DB.</span></span>

        az appservice web config appsettings update --settings dbuser="<database user>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbpassword="<database password>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbhost="<database hostname>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbport="<database port>" --name <app_name> --resource-group my-sailsjs-app-group
        az appservice web config appsettings update --settings dbname="<database name>" --name <app_name> --resource-group my-sailsjs-app-group

    <span data-ttu-id="f16ab-184">Azure uygulama ayarlarında ayarlarınızı koyma, kaynak denetimi (Git) dışında hassas verileri tutar.</span><span class="sxs-lookup"><span data-stu-id="f16ab-184">Putting your settings in Azure app settings keeps sensitive data out of your source control (Git).</span></span> <span data-ttu-id="f16ab-185">Ardından, geliştirme ortamınızı aynı bağlantı bilgilerini kullanacak şekilde yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="f16ab-185">Next, you will configure your development environment to use the same connection information.</span></span>
5. <span data-ttu-id="f16ab-186">Config/Local.js açın ve aşağıdaki bağlantıları nesne ekleyin:</span><span class="sxs-lookup"><span data-stu-id="f16ab-186">Open config/local.js and add the following connections object:</span></span>

        connections: {
            docDbMongo: {
                user: "<database user>",
                password: "<database password>",
                host: "<database hostname>",
                database: "<database name>",
                ssl: true
            },
        },

    <span data-ttu-id="f16ab-187">Bu yapılandırma config/connections.js dosyanızda yerel ortamınız için ayarları geçersiz kılar.</span><span class="sxs-lookup"><span data-stu-id="f16ab-187">This configuration overrides the settings in your config/connections.js file for the local environment.</span></span> <span data-ttu-id="f16ab-188">Git içinde depolanmaz şekilde bu dosyayı varsayılan .gitignore projenizdeki tarafından dışlandı.</span><span class="sxs-lookup"><span data-stu-id="f16ab-188">This file is excluded by the default .gitignore in your project, so it will not be stored in Git.</span></span> <span data-ttu-id="f16ab-189">Şimdi, Azure web uygulamanız ve yerel geliştirme ortamınızı Cosmos DB (MongoDB) veritabanınıza bağlantı kuramaz.</span><span class="sxs-lookup"><span data-stu-id="f16ab-189">Now, you are able to connect to your Cosmos DB (MongoDB) database both from your Azure web app and from your local development environment.</span></span>
6. <span data-ttu-id="f16ab-190">Üretim ortamınıza yapılandırmak için config/env/production.js açın ve aşağıdakileri ekleyin `models` nesnesi:</span><span class="sxs-lookup"><span data-stu-id="f16ab-190">Open config/env/production.js to configure your production environment, and add the following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'safe'
        },
7. <span data-ttu-id="f16ab-191">Geliştirme ortamınızı yapılandırmak için config/env/development.js açın ve aşağıdakileri ekleyin `models` nesnesi:</span><span class="sxs-lookup"><span data-stu-id="f16ab-191">Open config/env/development.js to configure your development environment, and add the following `models` object:</span></span>

        models: {
            connection: 'docDbMongo',
            migrate: 'alter'
        },

    <span data-ttu-id="f16ab-192">`migrate: 'alter'`Veritabanı geçiş özellikleri oluşturmak ve veritabanı koleksiyonları veya tabloları kolayca güncelleştirmek için kullanmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="f16ab-192">`migrate: 'alter'` lets you use database migration features to create and update database collections or tables easily.</span></span> <span data-ttu-id="f16ab-193">Ancak, `migrate: 'safe'` Sails.js kullanmanıza izin vermediğinden, Azure (üretim) ortamınız için kullanılan `migrate: 'alter'` bir üretim ortamında (bkz [Sails.js belgelerine](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span><span class="sxs-lookup"><span data-stu-id="f16ab-193">However, `migrate: 'safe'` is used for your Azure (production) environment because Sails.js does not allow you to use `migrate: 'alter'` in a production environment (see [Sails.js Documentation](http://sailsjs.org/documentation/concepts/models-and-orm/model-settings)).</span></span>
8. <span data-ttu-id="f16ab-194">Gelen terminal [oluşturmak](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) bir Sails.js [API şeması](http://sailsjs.org/documentation/concepts/blueprints) , normalde sonra çalıştırılır gibi `sails lift` Sails.js veritabanı geçiş ile veritabanı oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="f16ab-194">From the terminal, [generate](http://sailsjs.org/documentation/reference/command-line-interface/sails-generate) a Sails.js [blueprint API](http://sailsjs.org/documentation/concepts/blueprints) like you normally would, then run `sails lift` to create the database with Sails.js database migration.</span></span> <span data-ttu-id="f16ab-195">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="f16ab-195">For example:</span></span>

         sails generate api mywidget
         sails lift

    <span data-ttu-id="f16ab-196">`mywidget` Bu komutu tarafından oluşturulan model boşsa, ancak biz veritabanı bağlantısı sahibiz göstermek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f16ab-196">The `mywidget` model generated by this command is empty, but we can use it to show that we have database connectivity.</span></span>
    <span data-ttu-id="f16ab-197">Çalıştırdığınızda `sails lift`, uygulamanızı eksik koleksiyonlar ve tablolar modelleri için oluşturduğu kullanır.</span><span class="sxs-lookup"><span data-stu-id="f16ab-197">When you run `sails lift`, it creates the missing collections and tables for the models your app uses.</span></span>
9. <span data-ttu-id="f16ab-198">Tarayıcıda oluşturduğunuz API şeması erişin.</span><span class="sxs-lookup"><span data-stu-id="f16ab-198">Access the blueprint API you just created in the browser.</span></span> <span data-ttu-id="f16ab-199">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="f16ab-199">For example:</span></span>

        http://localhost:1337/mywidget/create

    <span data-ttu-id="f16ab-200">API geri koleksiyonunuz başarıyla oluşturuldu anlamına gelir tarayıcı penceresinde için oluşturulan girişi döndürmelidir.</span><span class="sxs-lookup"><span data-stu-id="f16ab-200">The API should return the created entry back to you in the browser window, which means that your collection is created  successfully.</span></span>

        {"id":1,"createdAt":"2016-09-23T13:32:00.000Z","updatedAt":"2016-09-23T13:32:00.000Z"}
10. <span data-ttu-id="f16ab-201">Şimdi, değişikliklerinizi Azure'a gönderin ve çalışmaya devam ettiğinden emin olmak için uygulamanızın göz atın.</span><span class="sxs-lookup"><span data-stu-id="f16ab-201">Now, push your changes to Azure, and browse to your app to make sure it still works.</span></span>

         git add .
         git commit -m "<your commit message>"
         git push azure master
         az appservice web browse --name <app_name> --resource-group my-sailsjs-app-group

11. <span data-ttu-id="f16ab-202">Azure web uygulamanızın API şeması erişin.</span><span class="sxs-lookup"><span data-stu-id="f16ab-202">Access the blueprint API of your Azure web app.</span></span> <span data-ttu-id="f16ab-203">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="f16ab-203">For example:</span></span>

         http://<appname>.azurewebsites.net/mywidget/create

     <span data-ttu-id="f16ab-204">API başka bir yeni giriş döndürürse, Azure web uygulamanızın Cosmos DB (MongoDB) veritabanınızı Bahsediyor.</span><span class="sxs-lookup"><span data-stu-id="f16ab-204">If the API returns another new entry, then your Azure web app is talking to your Cosmos DB (MongoDB) database.</span></span>

## <a name="more-resources"></a><span data-ttu-id="f16ab-205">Diğer kaynaklar</span><span class="sxs-lookup"><span data-stu-id="f16ab-205">More resources</span></span>
* [<span data-ttu-id="f16ab-206">Azure App Service'te Node.js web uygulamalarını kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="f16ab-206">Get started with Node.js web apps in Azure App Service</span></span>](app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="f16ab-207">Azure uygulamalarıyla Node.js Modüllerini kullanma</span><span class="sxs-lookup"><span data-stu-id="f16ab-207">Using Node.js Modules with Azure applications</span></span>](../nodejs-use-node-modules-azure-apps.md)
