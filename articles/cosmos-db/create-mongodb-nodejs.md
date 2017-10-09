---
title: aaaConnect Node.js kullanarak bir MongoDB uygulama tooAzure Cosmos DB | Microsoft Docs
description: "Bilgi nasıl tooconnect var olan bir Node.js MongoDB uygulama tooAzure Cosmos DB"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 06/19/2017
ms.author: mimig
ms.openlocfilehash: 4bc4f17a31d8c18d1ce5e3f002462f4d48eeb1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-migrate-an-existing-nodejs-mongodb-web-app"></a><span data-ttu-id="185dd-103">Azure Cosmos DB: Var olan bir Node.js MongoDB web uygulamasını geçirme</span><span class="sxs-lookup"><span data-stu-id="185dd-103">Azure Cosmos DB: Migrate an existing Node.js MongoDB web app</span></span> 

<span data-ttu-id="185dd-104">Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="185dd-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="185dd-105">Hızlı bir şekilde oluşturmak ve belge, anahtar/değer ve grafik veritabanları, her biri hello genel dağıtım ve yatay ölçek özelliklerini Azure Cosmos DB'nin hello çekirdek yararlı sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="185dd-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="185dd-106">Bu hızlı başlangıç gösteren nasıl varolan toouse [MongoDB](mongodb-introduction.md) Node.js içinde yazılmış uygulama ve MongoDB istemci bağlantılarını destekleyen tooyour Azure Cosmos DB veritabanına bağlanın.</span><span class="sxs-lookup"><span data-stu-id="185dd-106">This quickstart demonstrates how toouse an existing [MongoDB](mongodb-introduction.md) app written in Node.js and connect it tooyour Azure Cosmos DB database, which supports MongoDB client connections.</span></span> <span data-ttu-id="185dd-107">Diğer bir deyişle, Node.js uygulamanızı yalnızca MongoDB API'lerini kullanarak tooa veritabanına bağlanma olduğunu bilir.</span><span class="sxs-lookup"><span data-stu-id="185dd-107">In other words, your Node.js application only knows that it's connecting tooa database using MongoDB APIs.</span></span> <span data-ttu-id="185dd-108">Saydam veri hello toohello uygulama Azure Cosmos DB içinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="185dd-108">It is transparent toohello application that hello data is stored in Azure Cosmos DB.</span></span>

<span data-ttu-id="185dd-109">İşiniz bittiğinde, [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) üzerinde çalışan bir MEAN uygulamanız (MongoDB, Express, AngularJS ve Node.js) olacaktır.</span><span class="sxs-lookup"><span data-stu-id="185dd-109">When you are done, you will have a MEAN application (MongoDB, Express, AngularJS, and Node.js) running on [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span> 

![Azure App Service’te çalışan MEAN.js uygulaması](./media/create-mongodb-nodejs/meanjs-in-azure.png)


[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="185dd-111">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="185dd-111">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="185dd-112">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="185dd-112">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="185dd-113">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="185dd-113">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="185dd-114">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="185dd-114">Prerequisites</span></span> 
<span data-ttu-id="185dd-115">Ayrıca tooAzure CLI, gereksinim duyduğunuz [Node.js](https://nodejs.org/) ve [Git](http://www.git-scm.com/downloads) toorun yerel olarak yüklenmiş `npm` ve `git` komutları.</span><span class="sxs-lookup"><span data-stu-id="185dd-115">In addition tooAzure CLI, you need [Node.js](https://nodejs.org/) and [Git](http://www.git-scm.com/downloads) installed locally toorun `npm` and `git` commands.</span></span>

<span data-ttu-id="185dd-116">Node.js çalıştırma bilgisine sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="185dd-116">You should have working knowledge of Node.js.</span></span> <span data-ttu-id="185dd-117">Bu hızlı başlangıç hedeflenen toohelp değil, genel Node.js uygulamaları geliştirme ile.</span><span class="sxs-lookup"><span data-stu-id="185dd-117">This quickstart is not intended toohelp you with developing Node.js applications in general.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="185dd-118">Merhaba örnek uygulaması kopyalama</span><span class="sxs-lookup"><span data-stu-id="185dd-118">Clone hello sample application</span></span>

<span data-ttu-id="185dd-119">Git bash gibi bir git terminal penceresi açın ve `cd` tooa çalışma dizini.</span><span class="sxs-lookup"><span data-stu-id="185dd-119">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

<span data-ttu-id="185dd-120">Aşağıdaki komutları tooclone hello örnek depo hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="185dd-120">Run hello following commands tooclone hello sample repository.</span></span> <span data-ttu-id="185dd-121">Bu örnek depo hello varsayılan içerir [MEAN.js](http://meanjs.org/) uygulama.</span><span class="sxs-lookup"><span data-stu-id="185dd-121">This sample repository contains hello default [MEAN.js](http://meanjs.org/) application.</span></span> 

```bash
git clone https://github.com/prashanthmadi/mean
```

## <a name="run-hello-application"></a><span data-ttu-id="185dd-122">Merhaba uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="185dd-122">Run hello application</span></span>

<span data-ttu-id="185dd-123">Merhaba gerekli paketleri yüklemek ve hello uygulamasını başlatın.</span><span class="sxs-lookup"><span data-stu-id="185dd-123">Install hello required packages and start hello application.</span></span>

```bash
cd mean
npm install
npm start
```

## <a name="log-in-tooazure"></a><span data-ttu-id="185dd-124">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="185dd-124">Log in tooAzure</span></span>

<span data-ttu-id="185dd-125">Yüklü bir Azure CLI kullanıyorsanız, tooyour hello Azure aboneliğinizle oturumu [az oturum açma](/cli/azure/#login) komut ve hello ekrandaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="185dd-125">If you are using an installed Azure CLI, log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> <span data-ttu-id="185dd-126">Hello Azure bulut Kabuk kullanıyorsanız bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="185dd-126">You can skip this step if you're using hello Azure Cloud Shell.</span></span>

```azurecli
az login 
``` 
   
## <a name="add-hello-azure-cosmos-db-module"></a><span data-ttu-id="185dd-127">Hello Azure Cosmos DB Modül Ekle</span><span class="sxs-lookup"><span data-stu-id="185dd-127">Add hello Azure Cosmos DB module</span></span>

<span data-ttu-id="185dd-128">Yüklü bir Azure CLI kullanıyorsanız, toosee hello denetleyin `cosmosdb` bileşeni zaten yüklüyse hello çalıştırarak `az` komutu.</span><span class="sxs-lookup"><span data-stu-id="185dd-128">If you are using an installed Azure CLI, check toosee if hello `cosmosdb` component is already installed by running hello `az` command.</span></span> <span data-ttu-id="185dd-129">Varsa `cosmosdb` olan hello temel komutların listesi, toohello sonraki komutu devam.</span><span class="sxs-lookup"><span data-stu-id="185dd-129">If `cosmosdb` is in hello list of base commands, proceed toohello next command.</span></span> <span data-ttu-id="185dd-130">Hello Azure bulut Kabuk kullanıyorsanız bu adımı atlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="185dd-130">You can skip this step if you're using hello Azure Cloud Shell.</span></span>

<span data-ttu-id="185dd-131">Varsa `cosmosdb` hello temel komutların listesi, yeniden değil [Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="185dd-131">If `cosmosdb` is not in hello list of base commands, reinstall [Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="185dd-132">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="185dd-132">Create a resource group</span></span>

<span data-ttu-id="185dd-133">Oluşturma bir [kaynak grubu](../azure-resource-manager/resource-group-overview.md) hello ile [az grubu oluşturma](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="185dd-133">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with hello [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="185dd-134">Azure kaynak grubu; web uygulamaları, veritabanları ve depolama hesapları gibi Azure kaynaklarının dağıtıldığı ve yönetildiği bir mantıksal kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="185dd-134">An Azure resource group is a logical container into which Azure resources like web apps, databases and storage accounts are deployed and managed.</span></span> 

<span data-ttu-id="185dd-135">Merhaba aşağıdaki örnekte bir kaynak grubu hello Batı Avrupa bölgede oluşturur.</span><span class="sxs-lookup"><span data-stu-id="185dd-135">hello following example creates a resource group in hello West Europe region.</span></span> <span data-ttu-id="185dd-136">Merhaba kaynak grubu için benzersiz bir ad seçin.</span><span class="sxs-lookup"><span data-stu-id="185dd-136">Choose a unique name for hello resource group.</span></span>

<span data-ttu-id="185dd-137">Azure bulut Kabuk kullanıyorsanız **deneyin**hello ekrandaki yönergeleri toologin izleyin, sonra hello komutu hello komut istemi kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="185dd-137">If you are using Azure Cloud Shell, click **Try It**, follow hello onscreen prompts toologin, then copy hello command into hello command prompt.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="185dd-138">Azure Cosmos DB hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="185dd-138">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="185dd-139">Merhaba ile bir Azure Cosmos DB oluşturursunuz [az cosmosdb oluşturma](/cli/azure/cosmosdb#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="185dd-139">Create an Azure Cosmos DB account with hello [az cosmosdb create](/cli/azure/cosmosdb#create) command.</span></span>

<span data-ttu-id="185dd-140">Hello hello gördüğünüz kendi benzersiz Azure Cosmos DB hesap adı Lütfen yerine komutu, aşağıdaki `<cosmosdb-name>` yer tutucu.</span><span class="sxs-lookup"><span data-stu-id="185dd-140">In hello following command, please substitute your own unique Azure Cosmos DB account name where you see hello `<cosmosdb-name>` placeholder.</span></span> <span data-ttu-id="185dd-141">Bu benzersiz bir ad Azure Cosmos DB uç noktanızı bir parçası olarak kullanılacak (`https://<cosmosdb-name>.documents.azure.com/`), hello adı toobe benzersiz Azure içindeki tüm Azure Cosmos DB hesaplar arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="185dd-141">This unique name will be used as part of your Azure Cosmos DB endpoint (`https://<cosmosdb-name>.documents.azure.com/`), so hello name needs toobe unique across all Azure Cosmos DB accounts in Azure.</span></span> 

```azurecli-interactive
az cosmosdb create --name <cosmosdb-name> --resource-group myResourceGroup --kind MongoDB
```

<span data-ttu-id="185dd-142">Merhaba `--kind MongoDB` parametresi MongoDB istemci bağlantıları sağlar.</span><span class="sxs-lookup"><span data-stu-id="185dd-142">hello `--kind MongoDB` parameter enables MongoDB client connections.</span></span>

<span data-ttu-id="185dd-143">Hello Azure Cosmos DB hesabı oluşturulduğunda, hello Azure CLI örnek aşağıdaki bilgileri benzer toohello gösterir.</span><span class="sxs-lookup"><span data-stu-id="185dd-143">When hello Azure Cosmos DB account is created, hello Azure CLI shows information similar toohello following example.</span></span> 

> [!NOTE]
> <span data-ttu-id="185dd-144">Bu örnek, JSON hello varsayılan değer olan hello Azure CLI çıktı biçimi kullanır.</span><span class="sxs-lookup"><span data-stu-id="185dd-144">This example uses JSON as hello Azure CLI output format, which is hello default.</span></span> <span data-ttu-id="185dd-145">başka bir çıkış toouse biçimlendirmek için bkz: [çıktı biçimi Azure CLI 2.0 komutlar için](https://docs.microsoft.com/cli/azure/format-output-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="185dd-145">toouse another output format, see [Output formats for Azure CLI 2.0 commands](https://docs.microsoft.com/cli/azure/format-output-azure-cli).</span></span>

```json
{
  "databaseAccountOfferType": "Standard",
  "documentEndpoint": "https://<cosmosdb-name>.documents.azure.com:443/",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Document
DB/databaseAccounts/<cosmosdb-name>",
  "kind": "MongoDB",
  "location": "West Europe",
  "name": "<cosmosdb-name>",
  "readLocations": [
    {
      "documentEndpoint": "https://<cosmosdb-name>-westeurope.documents.azure.com:443/",
      "failoverPriority": 0,
      "id": "<cosmosdb-name>-westeurope",
      "locationName": "West Europe",
      "provisioningState": "Succeeded"
    }
  ],
  "resourceGroup": "myResourceGroup",
  "type": "Microsoft.DocumentDB/databaseAccounts",
  "writeLocations": [
    {
      "documentEndpoint": "https://<cosmosdb-name>-westeurope.documents.azure.com:443/",
      "failoverPriority": 0,
      "id": "<cosmosdb-name>-westeurope",
      "locationName": "West Europe",
      "provisioningState": "Succeeded"
    }
  ]
} 
```

## <a name="connect-your-nodejs-application-toohello-database"></a><span data-ttu-id="185dd-146">Node.js uygulaması toohello veritabanına bağlanın</span><span class="sxs-lookup"><span data-stu-id="185dd-146">Connect your Node.js application toohello database</span></span>

<span data-ttu-id="185dd-147">Bu adımda, MongoDB bağlantı dizesi kullanarak oluşturduğunuz MEAN.js örnek uygulama tooan Azure Cosmos DB veritabanınız bağlayın.</span><span class="sxs-lookup"><span data-stu-id="185dd-147">In this step, you connect your MEAN.js sample application tooan Azure Cosmos DB database you just created, using a MongoDB connection string.</span></span> 

<a name="devconfig"></a>
## <a name="configure-hello-connection-string-in-your-nodejs-application"></a><span data-ttu-id="185dd-148">Node.js uygulamanızda Hello bağlantı dizesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="185dd-148">Configure hello connection string in your Node.js application</span></span>

<span data-ttu-id="185dd-149">MEAN.js deponuzda `config/env/local-development.js` dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="185dd-149">In your MEAN.js repository, open `config/env/local-development.js`.</span></span>

<span data-ttu-id="185dd-150">Bu dosyanın Merhaba içeriğine koddan hello ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="185dd-150">Replace hello content of this file with hello following code.</span></span> <span data-ttu-id="185dd-151">Tooalso Değiştir hello iki emin olun `<cosmosdb-name>` Azure Cosmos DB hesap adınızı yer tutucularını.</span><span class="sxs-lookup"><span data-stu-id="185dd-151">Be sure tooalso replace hello two `<cosmosdb-name>` placeholders with your Azure Cosmos DB account name.</span></span>

```javascript
'use strict';

module.exports = {
  db: {
    uri: 'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean-dev?ssl=true&sslverifycertificate=false'
  }
};
```

## <a name="retrieve-hello-key"></a><span data-ttu-id="185dd-152">Başlangıç anahtarı alma</span><span class="sxs-lookup"><span data-stu-id="185dd-152">Retrieve hello key</span></span>

<span data-ttu-id="185dd-153">Sipariş tooconnect tooan Azure Cosmos DB veritabanı'nda hello veritabanı anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="185dd-153">In order tooconnect tooan Azure Cosmos DB database, you need hello database key.</span></span> <span data-ttu-id="185dd-154">Kullanım hello [az cosmosdb listesi anahtarlar](/cli/azure/cosmosdb#list-keys) komutu tooretrieve hello birincil anahtar.</span><span class="sxs-lookup"><span data-stu-id="185dd-154">Use hello [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) command tooretrieve hello primary key.</span></span>

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb-name> --resource-group myResourceGroup --query "primaryMasterKey"
```

<span data-ttu-id="185dd-155">Hello Azure CLI bilgi benzer toohello aşağıdaki örneğine çıkarır.</span><span class="sxs-lookup"><span data-stu-id="185dd-155">hello Azure CLI outputs information similar toohello following example.</span></span> 

```json
"RUayjYjixJDWG5xTqIiXjC..."
```

<span data-ttu-id="185dd-156">Merhaba değerini kopyalayın `primaryMasterKey`.</span><span class="sxs-lookup"><span data-stu-id="185dd-156">Copy hello value of `primaryMasterKey`.</span></span> <span data-ttu-id="185dd-157">Bu hello Yapıştır `<primary_master_key>` içinde `local-development.js`.</span><span class="sxs-lookup"><span data-stu-id="185dd-157">Paste this over hello  `<primary_master_key>` in `local-development.js`.</span></span>

<span data-ttu-id="185dd-158">Yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="185dd-158">Save your changes.</span></span>

### <a name="run-hello-application-again"></a><span data-ttu-id="185dd-159">Merhaba uygulamayı yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="185dd-159">Run hello application again.</span></span>

<span data-ttu-id="185dd-160">`npm start` komutunu yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="185dd-160">Run `npm start` again.</span></span> 

```bash
npm start
```

<span data-ttu-id="185dd-161">Konsol iletisi şimdi bu hello geliştirme ortamı çalışır durumda söyleyecektir.</span><span class="sxs-lookup"><span data-stu-id="185dd-161">A console message should now tell you that hello development environment is up and running.</span></span> 

<span data-ttu-id="185dd-162">Çok gidin`http://localhost:3000` bir tarayıcıda.</span><span class="sxs-lookup"><span data-stu-id="185dd-162">Navigate too`http://localhost:3000` in a browser.</span></span> <span data-ttu-id="185dd-163">Tıklatın **kaydolun** hello üst menü ve try toocreate içinde iki kullanıcılar kukla.</span><span class="sxs-lookup"><span data-stu-id="185dd-163">Click **Sign Up** in hello top menu and try toocreate two dummy users.</span></span> 

<span data-ttu-id="185dd-164">Merhaba MEAN.js örnek uygulamanın kullanıcı verilerini hello veritabanında depolar.</span><span class="sxs-lookup"><span data-stu-id="185dd-164">hello MEAN.js sample application stores user data in hello database.</span></span> <span data-ttu-id="185dd-165">Başarılı ve Azure Cosmos DB bağlantınızın çalıştığından sonra MEAN.js hello oturum açtığında kullanıcı, otomatik olarak oluşturmuştur. istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="185dd-165">If you are successful and MEAN.js automatically signs into hello created user, then your Azure Cosmos DB connection is working.</span></span> 

![MEAN.js tooMongoDB başarıyla bağlanır.](./media/create-mongodb-nodejs/mongodb-connect-success.png)

## <a name="view-data-in-data-explorer"></a><span data-ttu-id="185dd-167">Veri Gezgini’nde verileri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="185dd-167">View data in Data Explorer</span></span>

<span data-ttu-id="185dd-168">Bir Azure Cosmos DB tarafından depolanan verileri kullanılabilir tooview, sorgu ve çalıştırma iş mantığı hello Azure portal açıktır.</span><span class="sxs-lookup"><span data-stu-id="185dd-168">Data stored by an Azure Cosmos DB is available tooview, query, and run business-logic on in hello Azure portal.</span></span>

<span data-ttu-id="185dd-169">tooview, sorgu ve iş hello önceki adımda, oturum açma toohello oluşturduğunuz hello kullanıcı verileriyle [Azure portal](https://portal.azure.com) web tarayıcınızda.</span><span class="sxs-lookup"><span data-stu-id="185dd-169">tooview, query, and work with hello user data created in hello previous step, login toohello [Azure portal](https://portal.azure.com) in your web browser.</span></span>

<span data-ttu-id="185dd-170">Azure Cosmos DB Hello üst arama kutusuna yazın.</span><span class="sxs-lookup"><span data-stu-id="185dd-170">In hello top Search box, type Azure Cosmos DB.</span></span> <span data-ttu-id="185dd-171">Cosmos DB hesabı dikey penceresi açıldığında Cosmos DB hesabınızı seçin.</span><span class="sxs-lookup"><span data-stu-id="185dd-171">When your Cosmos DB account blade opens, select your Cosmos DB account.</span></span> <span data-ttu-id="185dd-172">Sol gezinti hello veri Explorer'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="185dd-172">In hello left navigation, click Data Explorer.</span></span> <span data-ttu-id="185dd-173">Koleksiyonunuz hello Koleksiyonlar bölmesinde genişletin ve ardından hello koleksiyon, sorgu hello veri hello belgeleri görüntülemek ve hatta oluşturabilir ve saklı yordamlar, tetikleyiciler ve UDF'lerin çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="185dd-173">Expand your collection in hello Collections pane, and then you can view hello documents in hello collection, query hello data, and even create and run stored procedures, triggers, and UDFs.</span></span> 

![Hello Azure portal'ın Veri Gezgini](./media/create-mongodb-nodejs/cosmosdb-connect-mongodb-data-explorer.png)


## <a name="deploy-hello-nodejs-application-tooazure"></a><span data-ttu-id="185dd-175">Merhaba Node.js uygulaması tooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="185dd-175">Deploy hello Node.js application tooAzure</span></span>

<span data-ttu-id="185dd-176">Bu adımda, MongoDB bağlı Node.js uygulaması tooAzure Cosmos DB dağıtın.</span><span class="sxs-lookup"><span data-stu-id="185dd-176">In this step, you deploy your MongoDB-connected Node.js application tooAzure Cosmos DB.</span></span>

<span data-ttu-id="185dd-177">Daha önce değiştirilen hello yapılandırma dosyasının hello geliştirme ortamı için olduğunu fark etmiş olabilirsiniz (`/config/env/local-development.js`).</span><span class="sxs-lookup"><span data-stu-id="185dd-177">You may have noticed that hello configuration file that you changed earlier is for hello development environment (`/config/env/local-development.js`).</span></span> <span data-ttu-id="185dd-178">Uygulama tooApp hizmet dağıttığınızda, varsayılan olarak hello üretim ortamında çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="185dd-178">When you deploy your application tooApp Service, it will run in hello production environment by default.</span></span> <span data-ttu-id="185dd-179">Şimdi, toomake hello ihtiyacınız aynı toohello ilgili yapılandırma dosyasını değiştirin.</span><span class="sxs-lookup"><span data-stu-id="185dd-179">So now, you need toomake hello same change toohello respective configuration file.</span></span>

<span data-ttu-id="185dd-180">MEAN.js deponuzda `config/env/production.js` dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="185dd-180">In your MEAN.js repository, open `config/env/production.js`.</span></span>

<span data-ttu-id="185dd-181">Merhaba, `db` nesne, hello değerini `uri` aşağıdaki örneğine hello olarak göster.</span><span class="sxs-lookup"><span data-stu-id="185dd-181">In hello `db` object, replace hello value of `uri` as show in hello following example.</span></span> <span data-ttu-id="185dd-182">Emin tooreplace hello yer tutucu olarak önce olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="185dd-182">Be sure tooreplace hello placeholders as before.</span></span>

```javascript
'mongodb://<cosmosdb-name>:<primary_master_key>@<cosmosdb-name>.documents.azure.com:10255/mean?ssl=true&sslverifycertificate=false',
```

> [!NOTE] 
> <span data-ttu-id="185dd-183">Merhaba `ssl=true` seçeneği önemlidir çünkü [Azure Cosmos DB SSL gerekir](connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="185dd-183">hello `ssl=true` option is important because [Azure Cosmos DB requires SSL](connect-mongodb-account.md#connection-string-requirements).</span></span> 
>
>

<span data-ttu-id="185dd-184">Hello terminal, tüm değişikliklerinizi Git içine uygulayın.</span><span class="sxs-lookup"><span data-stu-id="185dd-184">In hello terminal, commit all your changes into Git.</span></span> <span data-ttu-id="185dd-185">Her iki komutları toorun kopyalayabilirsiniz birlikte bunları.</span><span class="sxs-lookup"><span data-stu-id="185dd-185">You can copy both commands toorun them together.</span></span>

```bash
git add .
git commit -m "configured MongoDB connection string"
```
## <a name="clean-up-resources"></a><span data-ttu-id="185dd-186">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="185dd-186">Clean up resources</span></span>

<span data-ttu-id="185dd-187">Toocontinue toouse bu uygulamayı değil kullanacaksanız, bu hızlı başlangıç tarafından hello Azure portalında aşağıdaki adımları hello ile oluşturulan tüm kaynakları silin:</span><span class="sxs-lookup"><span data-stu-id="185dd-187">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="185dd-188">Merhaba sol taraftaki menüden hello Azure portal'ın, **kaynak grupları** ve ardından oluşturduğunuz hello kaynak hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="185dd-188">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="185dd-189">Kaynak grubu sayfanızda tıklatın **silmek**hello metin kutusuna hello kaynak toodelete hello adını yazın ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="185dd-189">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="185dd-190">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="185dd-190">Next steps</span></span>

<span data-ttu-id="185dd-191">Bu Hızlı Başlangıç, öğrendiğinize nasıl toocreate bir Azure Cosmos DB hesap ve hello Veri Gezgini'ni kullanarak bir MongoDB koleksiyonu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="185dd-191">In this quickstart, you've learned how toocreate an Azure Cosmos DB account and create a MongoDB collection using hello Data Explorer.</span></span> <span data-ttu-id="185dd-192">Şimdi, MongoDB veri tooAzure Cosmos DB geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="185dd-192">You can now migrate your MongoDB data tooAzure Cosmos DB.</span></span>  

> [!div class="nextstepaction"]
> [<span data-ttu-id="185dd-193">Azure Cosmos DB’ye MongoDB verileri aktarma</span><span class="sxs-lookup"><span data-stu-id="185dd-193">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)
