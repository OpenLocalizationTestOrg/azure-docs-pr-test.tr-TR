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
# <a name="build-a-nodejs-restful-api-and-deploy-it-tooan-api-app-in-azure"></a>Node.js RESTful API'si derleme ve tooan API uygulamasına dağıtma
[!INCLUDE [app-service-api-get-started-selector](../../includes/app-service-api-get-started-selector.md)]

Bu hızlı başlangıç gösterir nasıl toocreate Node.js ile yazılmış bir REST API [Express](http://expressjs.com/)kullanarak bir [Swagger](http://swagger.io/) tanımı ve olarak dağıtmayı bir [API uygulaması](app-service-api-apps-why-best-platform.md) Azure üzerinde. Komut satırı araçlarını kullanarak hello uygulaması oluşturma, kaynakları ile Merhaba yapılandırmak [Azure CLI](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli), Git kullanarak hello uygulamasını ve dağıtın.  İşiniz bittiğinde, Azure’da çalışan bir REST API örneğiniz olur.

## <a name="prerequisites"></a>Ön koşullar

* [Git](https://git-scm.com/)
* [Node.js ve NPM](https://nodejs.org/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir. Çalıştırma `az --version` toofind hello sürümü. Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli). 

## <a name="prepare-your-environment"></a>Ortamınızı hazırlama

1. Bir terminal penceresi komutu tooclone hello örnek tooyour yerel makine aşağıdaki hello çalıştırın.

    ```bash
    git clone https://github.com/Azure-Samples/app-service-api-node-contact-list
    ```

2. Merhaba örnek kod içeren toohello dizini değiştirin.

    ```bash
    cd app-service-api-node-contact-list
    ```

3. Yerel makinenize [Swaggerize](https://www.npmjs.com/package/swaggerize-express)’ı yükleyin. Swaggerize, Swagger tanımından REST API’niz için Node.js kodu oluşturan bir araçtır.

    ```bash
    npm install -g yo
    npm install -g generator-swaggerize
    ```

## <a name="generate-nodejs-code"></a>Node.js kodu oluşturma 

Merhaba öğreticinin bu bölümünde, Swagger meta verileri ilk oluşturun ve o tooscaffold kullanan bir API geliştirme iş akışını modeller (otomatik oluşturmak) hello API için sunucu kodu. 

Değiştirme dizin toohello *Başlat* klasörü, ardından çalıştırın `yo swaggerize`. Swaggerize, API hello Swagger tanımında'için bir Node.js projesi oluşturur *api.json*.

```bash
cd start
yo swaggerize --apiPath api.json --framework express
```

Swaggerize bir proje adı sorduğunda *ContactList* adını kullanın.
   
   ```bash
   Swaggerize Generator
   Tell us a bit about your application
   ? What would you like toocall this project: ContactList
   ? Your name: Francis Totten
   ? Your github user name: fabfrank
   ? Your email: frank@fabrikam.net
   ```
   
## <a name="customize-hello-project-code"></a>Merhaba proje kodu özelleştirme

1. Kopya hello *lib* hello klasörüne *ContactList* tarafından oluşturulan klasör `yo swaggerize`, dizinine değiştirme *ContactList*.

    ```bash
    cp -r lib/ ContactList/
    cd ContactList
    ```

2. Merhaba yüklemek `jsonpath` ve `swaggerize-ui` NPM modülleri. 

    ```bash
    npm install --save jsonpath swaggerize-ui
    ```

3. Merhaba Hello kodla *handlers/contacts.js* koddan hello ile: 
    ```javascript
    'use strict';

    var repository = require('../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.all())
        }
    };
    ```
    Bu kodu depolanan hello JSON verilerini kullanır *lib/contactrepository.js* tarafından sunulan *lib/Contacts.JSON*. Merhaba yeni *contacts.js* kodu tüm kişileri hello deposundaki bir JSON yükü olarak döndürür. 

4. Merhaba Hello kodla **handlers/contacts/{id}.js** koddan hello dosyasıyla:

    ```javascript
    'use strict';

    var repository = require('../../lib/contactRepository');

    module.exports = {
        get: function contacts_get(req, res) {
            res.json(repository.get(req.params['id']));
        }    
    };
    ```

    Bu kod belirtilen kimliğe sahip bir yol değişken tooreturn yalnızca hello kişi kullanmanıza olanak sağlar

5. Merhaba kodla **server.js** koddan hello ile:

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

    Bu kod, bazı küçük değişikliklere toolet Azure uygulama hizmeti ile çalışır hale getirir ve API için etkileşimli web arabirimi gösterir.

### <a name="test-hello-api-locally"></a>Yerel olarak test hello API

1. Merhaba Node.js uygulamasını Başlat
    ```bash
    npm start
    ```
    
2. Toohttp://localhost:8000 Gözat / tooview hello JSON hello tüm kişi listesi için iletişim kurar.
   
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

3. Toohttp://localhost:8000/kişiler/2 tooview hello kişiyle Gözat bir `id` iki.
   
    ```json
    { 
        "id": 2,
        "name": "Lacy Barrera",
        "email": "lacy@contoso.com"
    }
    ```

4. 8000/docs Hello Swagger web Arabirimi'ni kullanarak hello API sınayın.
   
    ![Swagger web arabirimi](media/app-service-api-nodejs-api-app/swagger-ui.png)

## <a id="createapiapp"></a> API Uygulaması oluşturma

Bu bölümde, Azure uygulama hizmeti hello Azure CLI 2.0 toocreate hello kaynakları toohost hello API kullanın. 

1.  Tooyour hello Azure aboneliğiyle oturum [az oturum açma](/cli/azure/#login) komut ve hello ekrandaki yönergeleri izleyin.

    ```azurecli-interactive
    az login
    ```

2. Birden çok Azure aboneliğiniz varsa, bir değişiklik hello varsayılan abonelik toohello istenen.

    ````azurecli-interactive
    az account set --subscription <name or id>
    ````

3. [!INCLUDE [Create resource group](../../includes/app-service-api-create-resource-group.md)] 

4. [!INCLUDE [Create app service plan](../../includes/app-service-api-create-app-service-plan.md)]

5. [!INCLUDE [Create API app](../../includes/app-service-api-create-api-app.md)] 


## <a name="deploy-hello-api-with-git"></a>Merhaba API Git ile dağıtma

Kod toohello API uygulamanız, yerel Git deposu tooAzure uygulama hizmeti işlemeleri ileterek dağıtın.

1. [!INCLUDE [Configure your deployment credentials](../../includes/configure-deployment-user-no-h.md)] 

2. Merhaba, yeni depo başlatmak *ContactList* dizini. 

    ```bash
    git init .
    ```

3. Merhaba hariç *node_modules* Git hello öğreticideki bir önceki adımda npm tarafından oluşturulan dizin. Yeni bir `.gitignore` hello geçerli dizinde dosya ve metin hello dosya başka bir yerindeki yeni bir satıra aşağıdaki hello ekleyin.

    ```
    node_modules/
    ```
    Merhaba onaylayın `node_modules` klasör göz ardı edilir ile `git status`.

4. Merhaba değişiklikleri toohello deposuna uygulayın.
    ```bash
    git add .
    git commit -m "initial version"
    ```

5. [!INCLUDE [Push tooAzure](../../includes/app-service-api-git-push-to-azure.md)]  
 
## <a name="test-hello-api--in-azure"></a>Azure test hello API

1. Bir tarayıcı toohttp://app_name.azurewebsites.net/contacts açın. Merhaba öğreticide daha önce yerel olarak hello istek yapıldığında aynı JSON olarak döndürülen hello bakın.

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

2. Bir tarayıcıda toohello Git `http://app_name.azurewebsites.net/docs` çıkış uç noktası tootry hello Swagger kullanıcı arabirimini Azure üzerinde çalışan.

    ![Swagger Ii](media/app-service-api-nodejs-api-app/swagger-azure-ui.png)

    Güncelleştirmeleri toohello örnek API tooAzure işlemeleri toohello Azure Git deposuna ileterek artık dağıtabilirsiniz.

## <a name="clean-up"></a>Temizleme

Azure CLI komutu aşağıdaki hello çalıştırmak bu başlangıcın oluşturulan hello kaynakları tooclean:

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="next-step"></a>Sonraki adım 
> [!div class="nextstepaction"]
> [CORS ile JavaScript istemcilerinden API uygulamalarını kullanma](app-service-api-cors-consume-javascript.md)

