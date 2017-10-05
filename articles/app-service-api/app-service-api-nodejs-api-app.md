---
title: "Azure Uygulama Hizmeti’ndeki Node.js API uygulaması | Microsoft Belgeleri"
description: "Node.js RESTful API’si oluşturma ve Azure App Service’deki bir API uygulamasına dağıtma hakkında bilgi edinin."
services: app-service\api
documentationcenter: node
author: bradygaster
manager: erikre
editor: 
ms.assetid: a820e400-06af-4852-8627-12b3db4a8e70
ms.service: app-service-api
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: get-started-article
ms.date: 06/13/2017
ms.author: rachelap
ms.openlocfilehash: 806585edd43b9d2d678bfa41523e4d9d40af8cba
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="build-a-nodejs-restful-api-and-deploy-it-to-an-api-app-in-azure"></a><span data-ttu-id="405f8-103">Node.js RESTful API’si derleme ve Azure’daki bir API uygulamasına dağıtma</span><span class="sxs-lookup"><span data-stu-id="405f8-103">Build a Node.js RESTful API and deploy it to an API app in Azure</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="405f8-104">Bu hızlı başlangıçta, [Swagger](http://swagger.io/) tanımı kullanarak Node.js [Express](http://expressjs.com/) ile yazılmış bir REST API’nin nasıl oluşturulacağı ve bunun Azure’da [API uygulaması](app-service-api-apps-why-best-platform.md) olarak nasıl dağıtılacağı gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="405f8-104">This quickstart shows how to create a REST API, written with Node.js [Express](http://expressjs.com/), using a [Swagger](http://swagger.io/) definition and deploying it as an [API app](app-service-api-apps-why-best-platform.md) on Azure.</span></span> <span data-ttu-id="405f8-105">Komut satırı araçlarını kullanarak uygulamayı oluşturur, [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) ile kaynakları yapılandırır ve Git kullanarak uygulamayı dağıtırsınız.</span><span class="sxs-lookup"><span data-stu-id="405f8-105">You create the app using command-line tools, configure resources with the [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and deploy the app using Git.</span></span>  <span data-ttu-id="405f8-106">İşiniz bittiğinde, Azure’da çalışan bir REST API örneğiniz olur.</span><span class="sxs-lookup"><span data-stu-id="405f8-106">When you've finished, you have a working sample REST API running on Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="405f8-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="405f8-107">Prerequisites</span></span>

* [<span data-ttu-id="405f8-108">Git</span><span class="sxs-lookup"><span data-stu-id="405f8-108">Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="405f8-109">Node.js ve NPM</span><span class="sxs-lookup"><span data-stu-id="405f8-109">Node.js and NPM</span></span>](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="405f8-110">CLI'yi yerel olarak yükleyip kullanmayı tercih ederseniz bu konu, Azure CLI 2.0 veya sonraki bir sürümünü kullanmanızı gerektirir.</span><span class="sxs-lookup"><span data-stu-id="405f8-110">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="405f8-111">Sürümü bulmak için `az --version` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="405f8-111">Run `az --version` to find the version.</span></span> <span data-ttu-id="405f8-112">Yüklemeniz veya yükseltmeniz gerekirse, bkz. [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="405f8-112">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-your-environment"></a><span data-ttu-id="405f8-113">Ortamınızı hazırlama</span><span class="sxs-lookup"><span data-stu-id="405f8-113">Prepare your environment</span></span>

1. <span data-ttu-id="405f8-114">Bir terminal penceresinde, aşağıdaki komutu çalıştırarak örneği yerel makinenize kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="405f8-114">In a terminal window, run the following command to clone the sample to your local machine.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/app-service-api-node-contact-list
    ```

2. <span data-ttu-id="405f8-115">Örnek kodu içeren dizine geçin.</span><span class="sxs-lookup"><span data-stu-id="405f8-115">Change to the directory that contains the sample code.</span></span>

    ```bash
    cd app-service-api-node-contact-list
    ```

3. <span data-ttu-id="405f8-116">Yerel makinenize [Swaggerize](https://www.npmjs.com/package/swaggerize-express)’ı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="405f8-116">Install [Swaggerize](https://www.npmjs.com/package/swaggerize-express) on your local machine.</span></span> <span data-ttu-id="405f8-117">Swaggerize, Swagger tanımından REST API’niz için Node.js kodu oluşturan bir araçtır.</span><span class="sxs-lookup"><span data-stu-id="405f8-117">Swaggerize is a tool that generates Node.js code for your REST API from a Swagger definition.</span></span>

    ```bash
    npm install -g yo
    npm install -g generator-swaggerize
    ```

## <a name="generate-nodejs-code"></a><span data-ttu-id="405f8-118">Node.js kodu oluşturma</span><span class="sxs-lookup"><span data-stu-id="405f8-118">Generate Node.js code</span></span> 

<span data-ttu-id="405f8-119">Öğreticinin bu bölümü, içinde ilk olarak Swagger meta verilerini oluşturduğunuz ve bunları API sunucu kodunun iskelesini kurmak (otomatik oluşturmak) için kullandığınız bir API geliştirme iş akışını modeller.</span><span class="sxs-lookup"><span data-stu-id="405f8-119">This section of the tutorial models an API development workflow in which you create Swagger metadata first and use that to scaffold (auto-generate) server code for the API.</span></span> 

<span data-ttu-id="405f8-120">Dizini *başlat* klasörü olarak değiştirin, ardından `yo swaggerize` öğesini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="405f8-120">Change directory to the *start* folder, then run `yo swaggerize`.</span></span> <span data-ttu-id="405f8-121">Swaggerize, *api.json*’da Swagger tanımından API’niz için bir Node.js projesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="405f8-121">Swaggerize creates a Node.js project for your API from the Swagger definition in *api.json*.</span></span>

```bash
cd start
yo swaggerize --apiPath api.json --framework express
```

<span data-ttu-id="405f8-122">Swaggerize bir proje adı sorduğunda *ContactList* adını kullanın.</span><span class="sxs-lookup"><span data-stu-id="405f8-122">When Swaggerize asks for a project name, use *ContactList*.</span></span>
   
   ```bash
   Swaggerize Generator
   Tell us a bit about your application
   ? What would you like to call this project: ContactList
   ? Your name: Francis Totten
   ? Your github user name: fabfrank
   ? Your email: frank@fabrikam.net
   ```
   
## <a name="customize-the-project-code"></a><span data-ttu-id="405f8-123">Proje kodunu özelleştirme</span><span class="sxs-lookup"><span data-stu-id="405f8-123">Customize the project code</span></span>

1. <span data-ttu-id="405f8-124">*lib* klasörünü, `yo swaggerize` tarafından oluşturulan *ContactList* klasörüne kopyalayın, ardından dizini *ContactList* ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="405f8-124">Copy the *lib* folder into the *ContactList* folder created by `yo swaggerize`, then change directory into *ContactList*.</span></span>

    ```bash
    cp -r lib/ ContactList/
    cd ContactList
    ```

2. <span data-ttu-id="405f8-125">`jsonpath` ve `swaggerize-ui` NPM modüllerini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="405f8-125">Install the `jsonpath` and `swaggerize-ui` NPM modules.</span></span> 

    ```bash
    npm install --save jsonpath swaggerize-ui
    ```

3. <span data-ttu-id="405f8-126">*handlers/contacts.js*’deki kodu aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="405f8-126">Replace the code in the *handlers/contacts.js* with the following code:</span></span> 
    ```javascript
    'use strict';

    var repository = require('../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.all())
        }
    };
    ```
    <span data-ttu-id="405f8-127">Bu kod, *lib/contactRepository.js* tarafından sunulan *lib/contacts.json*’da depolanmış JSON verilerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="405f8-127">This code uses the JSON data stored in *lib/contacts.json* served by *lib/contactRepository.js*.</span></span> <span data-ttu-id="405f8-128">Yeni *contacts.js* kodu, depodaki tüm kişileri JSON yükü olarak döndürür.</span><span class="sxs-lookup"><span data-stu-id="405f8-128">The new *contacts.js* code returns all contacts in the repository as a JSON payload.</span></span> 

4. <span data-ttu-id="405f8-129">**handlers/contacts/{id}.js** dosyasındaki kodu, aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="405f8-129">Replace the code in the **handlers/contacts/{id}.js** file with the following code:</span></span>

    ```javascript
    'use strict';

    var repository = require('../../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.get(req.params['id']));
        }    
    };
    ```

    <span data-ttu-id="405f8-130">Bu kod, yalnızca belirtilen kimliğe sahip kişiyi döndürmek için bir yol değişkeni kullanmanıza imkan tanır.</span><span class="sxs-lookup"><span data-stu-id="405f8-130">This code lets you use a path variable to return only the contact with a given ID.</span></span>

5. <span data-ttu-id="405f8-131">**server.js**’deki kodu, aşağıdaki kodla değiştirin:</span><span class="sxs-lookup"><span data-stu-id="405f8-131">Replace the code in **server.js** with the following code:</span></span>

    ```javascript
    'use strict';

    var port = process.env.PORT || 8000; 

    var http = require('http');
    var express = require('express');
    var bodyParser = require('body-parser');
    var swaggerize = require('swaggerize-express');
    var swaggerUi = require('swaggerize-ui'); 
    var path = require('path');
    var fs = require("fs");
    
    fs.existsSync = fs.existsSync || require('path').existsSync;

    var app = express();

    var server = http.createServer(app);

    app.use(bodyParser.json());

    app.use(swaggerize({
        api: path.resolve('./config/swagger.json'),
        handlers: path.resolve('./handlers'),
        docspath: '/swagger' 
    }));

    // change four
    app.use('/docs', swaggerUi({
        docs: '/swagger'  
    }));

    server.listen(port, function () { 
    });
    ```   

    <span data-ttu-id="405f8-132">Bu kod, Azure App Service ile çalışmasını sağlamak için birkaç küçük değişiklik yapar ve API’niz için etkileşimli bir web arabirimini kullanıma sunar.</span><span class="sxs-lookup"><span data-stu-id="405f8-132">This code makes some small changes to let it work with Azure App Service and exposes an interactive web interface for your API.</span></span>

### <a name="test-the-api-locally"></a><span data-ttu-id="405f8-133">API’yi yerel olarak test etme</span><span class="sxs-lookup"><span data-stu-id="405f8-133">Test the API locally</span></span>

1. <span data-ttu-id="405f8-134">Node.js uygulamasını başlatma</span><span class="sxs-lookup"><span data-stu-id="405f8-134">Start up the Node.js app</span></span>
    ```bash
    npm start
    ```
    
2. <span data-ttu-id="405f8-135">Kişi listesinin tamamı için JSON’u görüntülemek üzere http://localhost:8000/contacts’a göz atın.</span><span class="sxs-lookup"><span data-stu-id="405f8-135">Browse to http://localhost:8000/contacts to view the JSON for the entire contact list.</span></span>
   
   ```json
    {
        "id": 1,
        "name": "Barney Poland",
        "email": "barney@contoso.com"
    },
    {
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    },
    {
        "id": 3,
        "name": "Lora Riggs",
        "email": "lora@contoso.com"
    }
   ```

3. <span data-ttu-id="405f8-136">Kişiyi iki `id` arasından biriyle görüntülemek için http://localhost:8000/contacts/2’ye göz atın.</span><span class="sxs-lookup"><span data-stu-id="405f8-136">Browse to http://localhost:8000/contacts/2 to view the contact with an `id` of two.</span></span>
   
    ```json
    { 
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    }
    ```

4. <span data-ttu-id="405f8-137">http://localhost:8000/docs’ta Swagger web arabirimini kullanarak API’yi test edin.</span><span class="sxs-lookup"><span data-stu-id="405f8-137">Test the API using the Swagger web interface at http://localhost:8000/docs.</span></span>
   
    ![Swagger web arabirimi](media/app-service-api-nodejs-api-app/swagger-ui.png)

## <span data-ttu-id="405f8-139"><a id="createapiapp"></a> API Uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="405f8-139"><a id="createapiapp"></a> Create an API App</span></span>

<span data-ttu-id="405f8-140">Bu bölümde, API’yi Azure App Service'te barındırmak için gereken kaynakları oluşturmak amacıyla Azure CLI 2.0’ı kullanırsınız.</span><span class="sxs-lookup"><span data-stu-id="405f8-140">In this section, you use the Azure CLI 2.0 to create the resources to host the API on Azure App Service.</span></span> 

1.  <span data-ttu-id="405f8-141">[az login](/cli/azure/#login) komutuyla Azure aboneliğinizde oturum açın ve ekrandaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="405f8-141">Log in to your Azure subscription with the [az login](/cli/azure/#login) command and follow the on-screen directions.</span></span>

    ```azurecli-interactive
    az login
    ```

2. <span data-ttu-id="405f8-142">Birden çok Azure aboneliğiniz varsa varsayılan aboneliği istediğiniz abonelikle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="405f8-142">If you have multiple Azure subscriptions, change the default subscription to the desired one.</span></span>

    ````azurecli-interactive
    az account set --subscription <name or id>
    ````

3. [!INCLUDE [Create resource group](../../includes/app-service-api-create-resource-group.md)] 

4. [!INCLUDE [Create app service plan](../../includes/app-service-api-create-app-service-plan.md)]

5. [!INCLUDE [Create API app](../../includes/app-service-api-create-api-app.md)] 


## <a name="deploy-the-api-with-git"></a><span data-ttu-id="405f8-143">API’yi Git ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="405f8-143">Deploy the API with Git</span></span>

<span data-ttu-id="405f8-144">İşlemeleri yerel Git deponuzdan Azure App Service’e ileterek kodunuzu API uygulamasına dağıtırsınız.</span><span class="sxs-lookup"><span data-stu-id="405f8-144">Deploy your code to the API app by pushing commits from your local Git repository to Azure App Service.</span></span>

1. [!INCLUDE [Configure your deployment credentials](../../includes/configure-deployment-user-no-h.md)] 

2. <span data-ttu-id="405f8-145">*ContactList* dizininde yeni bir depo başlatın.</span><span class="sxs-lookup"><span data-stu-id="405f8-145">Initialize a new repo in the *ContactList* directory.</span></span> 

    ```bash
    git init .
    ```

3. <span data-ttu-id="405f8-146">Git’teki öğreticinin önceki bir adımında npm tarafından oluşturulan *node_modules* dizinini hariç tutun.</span><span class="sxs-lookup"><span data-stu-id="405f8-146">Exclude the *node_modules* directory created by npm in an earlier step in the tutorial from Git.</span></span> <span data-ttu-id="405f8-147">Geçerli dizinde yeni bir `.gitignore` dosyası oluşturun ve dosyanın herhangi bir yerindeki yeni bir satıra aşağıdaki metni ekleyin.</span><span class="sxs-lookup"><span data-stu-id="405f8-147">Create a new `.gitignore` file in the current directory and add the following text on a new line anywhere in the file.</span></span>

    ```
    node_modules/
    ```
    <span data-ttu-id="405f8-148">`node_modules` klasörünün `git status` ile yoksayıldığını onaylayın.</span><span class="sxs-lookup"><span data-stu-id="405f8-148">Confirm the `node_modules` folder is being ignored with  `git status`.</span></span>

4. <span data-ttu-id="405f8-149">Değişiklikleri depoya uygulayın.</span><span class="sxs-lookup"><span data-stu-id="405f8-149">Commit the changes to the repo.</span></span>
    ```bash
    git add .
    git commit -m "initial version"
    ```

5. [!INCLUDE [Push to Azure](../../includes/app-service-api-git-push-to-azure.md)]  
 
## <a name="test-the-api--in-azure"></a><span data-ttu-id="405f8-150">Azure'da API’yi test etme</span><span class="sxs-lookup"><span data-stu-id="405f8-150">Test the API  in Azure</span></span>

1. <span data-ttu-id="405f8-151">Tarayıcıda http://app_name.azurewebsites.net/contacts adresini açın.</span><span class="sxs-lookup"><span data-stu-id="405f8-151">Open a browser to http://app_name.azurewebsites.net/contacts.</span></span> <span data-ttu-id="405f8-152">Öğreticide daha önce yerel olarak istek yaptığınızda gördüğünüz JSON’un döndürüldüğünü göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="405f8-152">You see the same JSON returned as when you made the request locally earlier in the tutorial.</span></span>

   ```json
   {
       "id": 1,
       "name": "Barney Poland",
       "email": "barney@contoso.com"
   },
   {
       "id": 2,
       "name": "Lacy Barrera",
       "email": "lacy@contoso.com"
   },
   {
       "id": 3,
       "name": "Lora Riggs",
       "email": "lora@contoso.com"
   }
   ```

2. <span data-ttu-id="405f8-153">Bir tarayıcıda, `http://app_name.azurewebsites.net/docs` uç noktasına giderek Azure'da çalışan Swagger kullanıcı arabirimini deneyin.</span><span class="sxs-lookup"><span data-stu-id="405f8-153">In a browser, go to the `http://app_name.azurewebsites.net/docs` endpoint to try out the Swagger UI running on Azure.</span></span>

    ![Swagger Ii](media/app-service-api-nodejs-api-app/swagger-azure-ui.png)

    <span data-ttu-id="405f8-155">Artık işlemleri Azure Git deposuna ileterek örnek API güncelleştirmelerini Azure’a dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="405f8-155">You can now deploy updates to the sample API to Azure simply by pushing commits to the Azure Git repository.</span></span>

## <a name="clean-up"></a><span data-ttu-id="405f8-156">Temizleme</span><span class="sxs-lookup"><span data-stu-id="405f8-156">Clean up</span></span>

<span data-ttu-id="405f8-157">Bu hızlı başlangıçta oluşturulan kaynakları kaldırmak için şu Azure CLI komutunu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="405f8-157">To clean up the resources created in this quickstart, run the following Azure CLI command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-step"></a><span data-ttu-id="405f8-158">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="405f8-158">Next step</span></span> 
> [!div class="nextstepaction"]
> [<span data-ttu-id="405f8-159">CORS ile JavaScript istemcilerinden API uygulamalarını kullanma</span><span class="sxs-lookup"><span data-stu-id="405f8-159">Consume API apps from JavaScript clients with CORS</span></span>](app-service-api-cors-consume-javascript.md)

