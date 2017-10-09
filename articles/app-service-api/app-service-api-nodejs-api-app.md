---
title: "Azure uygulama hizmetinde aaaNode.js API uygulaması | Microsoft Docs"
description: "Bilgi nasıl toocreate Node.js RESTful API'si ve Azure App Service'teki tooan API uygulamasına dağıtabilirsiniz."
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
ms.openlocfilehash: 3b3229c1453b6ca4d06bef26f476e92afda4e244
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-restful-api-and-deploy-it-tooan-api-app-in-azure"></a><span data-ttu-id="d6600-103">Node.js RESTful API'si derleme ve tooan API uygulamasına dağıtma</span><span class="sxs-lookup"><span data-stu-id="d6600-103">Build a Node.js RESTful API and deploy it tooan API app in Azure</span></span>
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

<span data-ttu-id="d6600-104">Bu hızlı başlangıç gösterir nasıl toocreate Node.js ile yazılmış bir REST API [Express](http://expressjs.com/)kullanarak bir [Swagger](http://swagger.io/) tanımı ve olarak dağıtmayı bir [API uygulaması](app-service-api-apps-why-best-platform.md) Azure üzerinde.</span><span class="sxs-lookup"><span data-stu-id="d6600-104">This quickstart shows how toocreate a REST API, written with Node.js [Express](http://expressjs.com/), using a [Swagger](http://swagger.io/) definition and deploying it as an [API app](app-service-api-apps-why-best-platform.md) on Azure.</span></span> <span data-ttu-id="d6600-105">Komut satırı araçlarını kullanarak hello uygulaması oluşturma, kaynakları ile Merhaba yapılandırmak [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), Git kullanarak hello uygulamasını ve dağıtın.</span><span class="sxs-lookup"><span data-stu-id="d6600-105">You create hello app using command-line tools, configure resources with hello [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), and deploy hello app using Git.</span></span>  <span data-ttu-id="d6600-106">İşiniz bittiğinde, Azure’da çalışan bir REST API örneğiniz olur.</span><span class="sxs-lookup"><span data-stu-id="d6600-106">When you've finished, you have a working sample REST API running on Azure.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6600-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d6600-107">Prerequisites</span></span>

* [<span data-ttu-id="d6600-108">Git</span><span class="sxs-lookup"><span data-stu-id="d6600-108">Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="d6600-109">Node.js ve NPM</span><span class="sxs-lookup"><span data-stu-id="d6600-109">Node.js and NPM</span></span>](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d6600-110">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="d6600-110">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="d6600-111">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="d6600-111">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="d6600-112">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="d6600-112">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prepare-your-environment"></a><span data-ttu-id="d6600-113">Ortamınızı hazırlama</span><span class="sxs-lookup"><span data-stu-id="d6600-113">Prepare your environment</span></span>

1. <span data-ttu-id="d6600-114">Bir terminal penceresi komutu tooclone hello örnek tooyour yerel makine aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d6600-114">In a terminal window, run hello following command tooclone hello sample tooyour local machine.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/app-service-api-node-contact-list
    ```

2. <span data-ttu-id="d6600-115">Merhaba örnek kod içeren toohello dizini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d6600-115">Change toohello directory that contains hello sample code.</span></span>

    ```bash
    cd app-service-api-node-contact-list
    ```

3. <span data-ttu-id="d6600-116">Yerel makinenize [Swaggerize](https://www.npmjs.com/package/swaggerize-express)’ı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="d6600-116">Install [Swaggerize](https://www.npmjs.com/package/swaggerize-express) on your local machine.</span></span> <span data-ttu-id="d6600-117">Swaggerize, Swagger tanımından REST API’niz için Node.js kodu oluşturan bir araçtır.</span><span class="sxs-lookup"><span data-stu-id="d6600-117">Swaggerize is a tool that generates Node.js code for your REST API from a Swagger definition.</span></span>

    ```bash
    npm install -g yo
    npm install -g generator-swaggerize
    ```

## <a name="generate-nodejs-code"></a><span data-ttu-id="d6600-118">Node.js kodu oluşturma</span><span class="sxs-lookup"><span data-stu-id="d6600-118">Generate Node.js code</span></span> 

<span data-ttu-id="d6600-119">Merhaba öğreticinin bu bölümünde, Swagger meta verileri ilk oluşturun ve o tooscaffold kullanan bir API geliştirme iş akışını modeller (otomatik oluşturmak) hello API için sunucu kodu.</span><span class="sxs-lookup"><span data-stu-id="d6600-119">This section of hello tutorial models an API development workflow in which you create Swagger metadata first and use that tooscaffold (auto-generate) server code for hello API.</span></span> 

<span data-ttu-id="d6600-120">Değiştirme dizin toohello *Başlat* klasörü, ardından çalıştırın `yo swaggerize`.</span><span class="sxs-lookup"><span data-stu-id="d6600-120">Change directory toohello *start* folder, then run `yo swaggerize`.</span></span> <span data-ttu-id="d6600-121">Swaggerize, API hello Swagger tanımında'için bir Node.js projesi oluşturur *api.json*.</span><span class="sxs-lookup"><span data-stu-id="d6600-121">Swaggerize creates a Node.js project for your API from hello Swagger definition in *api.json*.</span></span>

```bash
cd start
yo swaggerize --apiPath api.json --framework express
```

<span data-ttu-id="d6600-122">Swaggerize bir proje adı sorduğunda *ContactList* adını kullanın.</span><span class="sxs-lookup"><span data-stu-id="d6600-122">When Swaggerize asks for a project name, use *ContactList*.</span></span>
   
   ```bash
   Swaggerize Generator
   Tell us a bit about your application
   ? What would you like toocall this project: ContactList
   ? Your name: Francis Totten
   ? Your github user name: fabfrank
   ? Your email: frank@fabrikam.net
   ```
   
## <a name="customize-hello-project-code"></a><span data-ttu-id="d6600-123">Merhaba proje kodu özelleştirme</span><span class="sxs-lookup"><span data-stu-id="d6600-123">Customize hello project code</span></span>

1. <span data-ttu-id="d6600-124">Kopya hello *lib* hello klasörüne *ContactList* tarafından oluşturulan klasör `yo swaggerize`, dizinine değiştirme *ContactList*.</span><span class="sxs-lookup"><span data-stu-id="d6600-124">Copy hello *lib* folder into hello *ContactList* folder created by `yo swaggerize`, then change directory into *ContactList*.</span></span>

    ```bash
    cp -r lib/ ContactList/
    cd ContactList
    ```

2. <span data-ttu-id="d6600-125">Merhaba yüklemek `jsonpath` ve `swaggerize-ui` NPM modülleri.</span><span class="sxs-lookup"><span data-stu-id="d6600-125">Install hello `jsonpath` and `swaggerize-ui` NPM modules.</span></span> 

    ```bash
    npm install --save jsonpath swaggerize-ui
    ```

3. <span data-ttu-id="d6600-126">Merhaba Hello kodla *handlers/contacts.js* koddan hello ile:</span><span class="sxs-lookup"><span data-stu-id="d6600-126">Replace hello code in hello *handlers/contacts.js* with hello following code:</span></span> 
    ```javascript
    'use strict';

    var repository = require('../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.all())
        }
    };
    ```
    <span data-ttu-id="d6600-127">Bu kodu depolanan hello JSON verilerini kullanır *lib/contactrepository.js* tarafından sunulan *lib/Contacts.JSON*.</span><span class="sxs-lookup"><span data-stu-id="d6600-127">This code uses hello JSON data stored in *lib/contacts.json* served by *lib/contactRepository.js*.</span></span> <span data-ttu-id="d6600-128">Merhaba yeni *contacts.js* kodu tüm kişileri hello deposundaki bir JSON yükü olarak döndürür.</span><span class="sxs-lookup"><span data-stu-id="d6600-128">hello new *contacts.js* code returns all contacts in hello repository as a JSON payload.</span></span> 

4. <span data-ttu-id="d6600-129">Merhaba Hello kodla **handlers/contacts/{id}.js** koddan hello dosyasıyla:</span><span class="sxs-lookup"><span data-stu-id="d6600-129">Replace hello code in hello **handlers/contacts/{id}.js** file with hello following code:</span></span>

    ```javascript
    'use strict';

    var repository = require('../../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.get(req.params['id']));
        }    
    };
    ```

    <span data-ttu-id="d6600-130">Bu kod belirtilen kimliğe sahip bir yol değişken tooreturn yalnızca hello kişi kullanmanıza olanak sağlar</span><span class="sxs-lookup"><span data-stu-id="d6600-130">This code lets you use a path variable tooreturn only hello contact with a given ID.</span></span>

5. <span data-ttu-id="d6600-131">Merhaba kodla **server.js** koddan hello ile:</span><span class="sxs-lookup"><span data-stu-id="d6600-131">Replace hello code in **server.js** with hello following code:</span></span>

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

    <span data-ttu-id="d6600-132">Bu kod, bazı küçük değişikliklere toolet Azure uygulama hizmeti ile çalışır hale getirir ve API için etkileşimli web arabirimi gösterir.</span><span class="sxs-lookup"><span data-stu-id="d6600-132">This code makes some small changes toolet it work with Azure App Service and exposes an interactive web interface for your API.</span></span>

### <a name="test-hello-api-locally"></a><span data-ttu-id="d6600-133">Yerel olarak test hello API</span><span class="sxs-lookup"><span data-stu-id="d6600-133">Test hello API locally</span></span>

1. <span data-ttu-id="d6600-134">Merhaba Node.js uygulamasını Başlat</span><span class="sxs-lookup"><span data-stu-id="d6600-134">Start up hello Node.js app</span></span>
    ```bash
    npm start
    ```
    
2. <span data-ttu-id="d6600-135">Toohttp://localhost:8000 Gözat / tooview hello JSON hello tüm kişi listesi için iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="d6600-135">Browse toohttp://localhost:8000/contacts tooview hello JSON for hello entire contact list.</span></span>
   
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

3. <span data-ttu-id="d6600-136">Toohttp://localhost:8000/kişiler/2 tooview hello kişiyle Gözat bir `id` iki.</span><span class="sxs-lookup"><span data-stu-id="d6600-136">Browse toohttp://localhost:8000/contacts/2 tooview hello contact with an `id` of two.</span></span>
   
    ```json
    { 
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    }
    ```

4. <span data-ttu-id="d6600-137">8000/docs Hello Swagger web Arabirimi'ni kullanarak hello API sınayın.</span><span class="sxs-lookup"><span data-stu-id="d6600-137">Test hello API using hello Swagger web interface at http://localhost:8000/docs.</span></span>
   
    ![Swagger web arabirimi](media/app-service-api-nodejs-api-app/swagger-ui.png)

## <span data-ttu-id="d6600-139"><a id="createapiapp"></a> API Uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="d6600-139"><a id="createapiapp"></a> Create an API App</span></span>

<span data-ttu-id="d6600-140">Bu bölümde, Azure uygulama hizmeti hello Azure CLI 2.0 toocreate hello kaynakları toohost hello API kullanın.</span><span class="sxs-lookup"><span data-stu-id="d6600-140">In this section, you use hello Azure CLI 2.0 toocreate hello resources toohost hello API on Azure App Service.</span></span> 

1.  <span data-ttu-id="d6600-141">Tooyour hello Azure aboneliğiyle oturum [az oturum açma](/cli/azure/#login) komut ve hello ekrandaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="d6600-141">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

    ```azurecli-interactive
    az login
    ```

2. <span data-ttu-id="d6600-142">Birden çok Azure aboneliğiniz varsa, bir değişiklik hello varsayılan abonelik toohello istenen.</span><span class="sxs-lookup"><span data-stu-id="d6600-142">If you have multiple Azure subscriptions, change hello default subscription toohello desired one.</span></span>

    ````azurecli-interactive
    az account set --subscription <name or id>
    ````

3. [!INCLUDE [Create resource group](../../includes/app-service-api-create-resource-group.md)] 

4. [!INCLUDE [Create app service plan](../../includes/app-service-api-create-app-service-plan.md)]

5. [!INCLUDE [Create API app](../../includes/app-service-api-create-api-app.md)] 


## <a name="deploy-hello-api-with-git"></a><span data-ttu-id="d6600-143">Merhaba API Git ile dağıtma</span><span class="sxs-lookup"><span data-stu-id="d6600-143">Deploy hello API with Git</span></span>

<span data-ttu-id="d6600-144">Kod toohello API uygulamanız, yerel Git deposu tooAzure uygulama hizmeti işlemeleri ileterek dağıtın.</span><span class="sxs-lookup"><span data-stu-id="d6600-144">Deploy your code toohello API app by pushing commits from your local Git repository tooAzure App Service.</span></span>

1. [!INCLUDE [Configure your deployment credentials](../../includes/configure-deployment-user-no-h.md)] 

2. <span data-ttu-id="d6600-145">Merhaba, yeni depo başlatmak *ContactList* dizini.</span><span class="sxs-lookup"><span data-stu-id="d6600-145">Initialize a new repo in hello *ContactList* directory.</span></span> 

    ```bash
    git init .
    ```

3. <span data-ttu-id="d6600-146">Merhaba hariç *node_modules* Git hello öğreticideki bir önceki adımda npm tarafından oluşturulan dizin.</span><span class="sxs-lookup"><span data-stu-id="d6600-146">Exclude hello *node_modules* directory created by npm in an earlier step in hello tutorial from Git.</span></span> <span data-ttu-id="d6600-147">Yeni bir `.gitignore` hello geçerli dizinde dosya ve metin hello dosya başka bir yerindeki yeni bir satıra aşağıdaki hello ekleyin.</span><span class="sxs-lookup"><span data-stu-id="d6600-147">Create a new `.gitignore` file in hello current directory and add hello following text on a new line anywhere in hello file.</span></span>

    ```
    node_modules/
    ```
    <span data-ttu-id="d6600-148">Merhaba onaylayın `node_modules` klasör göz ardı edilir ile `git status`.</span><span class="sxs-lookup"><span data-stu-id="d6600-148">Confirm hello `node_modules` folder is being ignored with  `git status`.</span></span>

4. <span data-ttu-id="d6600-149">Merhaba değişiklikleri toohello deposuna uygulayın.</span><span class="sxs-lookup"><span data-stu-id="d6600-149">Commit hello changes toohello repo.</span></span>
    ```bash
    git add .
    git commit -m "initial version"
    ```

5. [!INCLUDE [Push tooAzure](../../includes/app-service-api-git-push-to-azure.md)]  
 
## <a name="test-hello-api--in-azure"></a><span data-ttu-id="d6600-150">Azure test hello API</span><span class="sxs-lookup"><span data-stu-id="d6600-150">Test hello API  in Azure</span></span>

1. <span data-ttu-id="d6600-151">Bir tarayıcı toohttp://app_name.azurewebsites.net/contacts açın.</span><span class="sxs-lookup"><span data-stu-id="d6600-151">Open a browser toohttp://app_name.azurewebsites.net/contacts.</span></span> <span data-ttu-id="d6600-152">Merhaba öğreticide daha önce yerel olarak hello istek yapıldığında aynı JSON olarak döndürülen hello bakın.</span><span class="sxs-lookup"><span data-stu-id="d6600-152">You see hello same JSON returned as when you made hello request locally earlier in hello tutorial.</span></span>

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

2. <span data-ttu-id="d6600-153">Bir tarayıcıda toohello Git `http://app_name.azurewebsites.net/docs` çıkış uç noktası tootry hello Swagger kullanıcı arabirimini Azure üzerinde çalışan.</span><span class="sxs-lookup"><span data-stu-id="d6600-153">In a browser, go toohello `http://app_name.azurewebsites.net/docs` endpoint tootry out hello Swagger UI running on Azure.</span></span>

    ![Swagger Ii](media/app-service-api-nodejs-api-app/swagger-azure-ui.png)

    <span data-ttu-id="d6600-155">Güncelleştirmeleri toohello örnek API tooAzure işlemeleri toohello Azure Git deposuna ileterek artık dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6600-155">You can now deploy updates toohello sample API tooAzure simply by pushing commits toohello Azure Git repository.</span></span>

## <a name="clean-up"></a><span data-ttu-id="d6600-156">Temizleme</span><span class="sxs-lookup"><span data-stu-id="d6600-156">Clean up</span></span>

<span data-ttu-id="d6600-157">Azure CLI komutu aşağıdaki hello çalıştırmak bu başlangıcın oluşturulan hello kaynakları tooclean:</span><span class="sxs-lookup"><span data-stu-id="d6600-157">tooclean up hello resources created in this quickstart, run hello following Azure CLI command:</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-step"></a><span data-ttu-id="d6600-158">Sonraki adım</span><span class="sxs-lookup"><span data-stu-id="d6600-158">Next step</span></span> 
> [!div class="nextstepaction"]
> [<span data-ttu-id="d6600-159">CORS ile JavaScript istemcilerinden API uygulamalarını kullanma</span><span class="sxs-lookup"><span data-stu-id="d6600-159">Consume API apps from JavaScript clients with CORS</span></span>](app-service-api-cors-consume-javascript.md)

