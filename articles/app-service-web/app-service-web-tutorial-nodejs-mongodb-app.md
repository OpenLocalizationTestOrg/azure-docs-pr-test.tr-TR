---
title: "aaaBuild azure'da Node.js ve MongoDB bir web uygulaması | Microsoft Docs"
description: "Bilgi nasıl tooget Azure'da çalışan bir Node.js uygulaması ile bağlantı tooa Cosmos DB veritabanı ile MongoDB bağlantı dizesi."
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 0b4d7d0e-e984-49a1-a57a-3c0caa955f0e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 532251c51ed6f8513e6e366393e889b67a85e5b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-and-mongodb-web-app-in-azure"></a><span data-ttu-id="e37c9-103">Azure'da Node.js ve MongoDB bir web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="e37c9-103">Build a Node.js and MongoDB web app in Azure</span></span>

<span data-ttu-id="e37c9-104">Azure Web Apps düzeyde ölçeklenebilir, otomatik olarak düzeltme eki uygulama web barındırma hizmeti sağlar.</span><span class="sxs-lookup"><span data-stu-id="e37c9-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="e37c9-105">Bu öğretici nasıl toocreate bir Node.js web uygulaması Azure ve tooa MongoDB veritabanı bağlantı gösterir.</span><span class="sxs-lookup"><span data-stu-id="e37c9-105">This tutorial shows how toocreate a Node.js web app in Azure and connect it tooa MongoDB database.</span></span> <span data-ttu-id="e37c9-106">İşiniz bittiğinde, ortalama uygulama (MongoDB, Express, AngularJS ve Node.js) çalışan bir gerekir, [Azure App Service](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e37c9-106">When you're done, you'll have a MEAN application (MongoDB, Express, AngularJS, and Node.js) running in [Azure App Service](app-service-web-overview.md).</span></span> <span data-ttu-id="e37c9-107">Kolaylık olması için hello örnek uygulama hello kullanır [MEAN.js web çerçevesi](http://meanjs.org/).</span><span class="sxs-lookup"><span data-stu-id="e37c9-107">For simplicity, hello sample application uses hello [MEAN.js web framework](http://meanjs.org/).</span></span>

![Azure App Service’te çalışan MEAN.js uygulaması](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="e37c9-109">Öğrenecekleriniz:</span><span class="sxs-lookup"><span data-stu-id="e37c9-109">What you'll learn:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e37c9-110">MongoDB veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e37c9-110">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="e37c9-111">Bir Node.js uygulaması tooMongoDB Bağlan</span><span class="sxs-lookup"><span data-stu-id="e37c9-111">Connect a Node.js app tooMongoDB</span></span>
> * <span data-ttu-id="e37c9-112">Merhaba uygulama tooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="e37c9-112">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="e37c9-113">Merhaba veri modeli güncelleştirmek ve hello uygulama yeniden dağıtın</span><span class="sxs-lookup"><span data-stu-id="e37c9-113">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="e37c9-114">Azure Stream tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="e37c9-114">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="e37c9-115">Merhaba uygulamada hello Azure portalı Yönet</span><span class="sxs-lookup"><span data-stu-id="e37c9-115">Manage hello app in hello Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e37c9-116">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e37c9-116">Prerequisites</span></span>

<span data-ttu-id="e37c9-117">toocomplete Bu öğretici:</span><span class="sxs-lookup"><span data-stu-id="e37c9-117">toocomplete this tutorial:</span></span>

1. [<span data-ttu-id="e37c9-118">Git'i yükleyin</span><span class="sxs-lookup"><span data-stu-id="e37c9-118">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="e37c9-119">Node.js ve NPM'yi yükleyin</span><span class="sxs-lookup"><span data-stu-id="e37c9-119">Install Node.js and NPM</span></span>](https://nodejs.org/)
1. <span data-ttu-id="e37c9-120">[Gulp.js yükleme](http://gulpjs.com/) (gerektirdiği [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))</span><span class="sxs-lookup"><span data-stu-id="e37c9-120">[Install Gulp.js](http://gulpjs.com/) (required by [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started))</span></span>
1. [<span data-ttu-id="e37c9-121">Yükleyip çalıştırabilirsiniz MongoDB Community Edition</span><span class="sxs-lookup"><span data-stu-id="e37c9-121">Install and run MongoDB Community Edition</span></span>](https://docs.mongodb.com/manual/administration/install-community/) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="e37c9-122">Tooinstall seçin ve hello CLI yerel olarak kullanırsanız, bu konuda hello Azure CLI Sürüm 2.0 veya üstü çalıştığını gerektirir.</span><span class="sxs-lookup"><span data-stu-id="e37c9-122">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="e37c9-123">Çalıştırma `az --version` toofind hello sürümü.</span><span class="sxs-lookup"><span data-stu-id="e37c9-123">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="e37c9-124">Tooinstall veya yükseltme gerekirse bkz [Azure CLI 2.0 yükleme]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e37c9-124">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-mongodb"></a><span data-ttu-id="e37c9-125">Test yerel MongoDB</span><span class="sxs-lookup"><span data-stu-id="e37c9-125">Test local MongoDB</span></span>

<span data-ttu-id="e37c9-126">Açık hello terminal penceresi ve `cd` toohello `bin` MongoDB yüklemenizin dizin.</span><span class="sxs-lookup"><span data-stu-id="e37c9-126">Open hello terminal window and `cd` toohello `bin` directory of your MongoDB installation.</span></span> <span data-ttu-id="e37c9-127">Bu bir terminal penceresi toorun Bu öğreticide tüm hello komutlarını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e37c9-127">You can use this terminal window toorun all hello commands in this tutorial.</span></span>

<span data-ttu-id="e37c9-128">Çalıştırma `mongo` hello terminal tooconnect tooyour yerel MongoDB Server.</span><span class="sxs-lookup"><span data-stu-id="e37c9-128">Run `mongo` in hello terminal tooconnect tooyour local MongoDB server.</span></span>

```bash
mongo
```

<span data-ttu-id="e37c9-129">Bağlantı başarılı olursa, MongoDB veritabanı zaten çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="e37c9-129">If your connection is successful, then your MongoDB database is already running.</span></span> <span data-ttu-id="e37c9-130">Aksi takdirde, yerel MongoDB veritabanı hello adımları izleyerek başlatıldığından emin olun [MongoDB Community Edition yüklemek](https://docs.mongodb.com/manual/administration/install-community/).</span><span class="sxs-lookup"><span data-stu-id="e37c9-130">If not, make sure that your local MongoDB database is started by following hello steps at [Install MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/).</span></span> <span data-ttu-id="e37c9-131">Genellikle, MongoDB yüklenir, ancak yine de toostart gerekir çalıştırarak `mongod`.</span><span class="sxs-lookup"><span data-stu-id="e37c9-131">Often, MongoDB is installed, but you still need toostart it by running `mongod`.</span></span> 

<span data-ttu-id="e37c9-132">Bitirdiğinizde, MongoDB veritabanı sınama, yazın `Ctrl+C` hello terminal içinde.</span><span class="sxs-lookup"><span data-stu-id="e37c9-132">When you're done testing your MongoDB database, type `Ctrl+C` in hello terminal.</span></span> 

## <a name="create-local-nodejs-app"></a><span data-ttu-id="e37c9-133">Yerel Node.js uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="e37c9-133">Create local Node.js app</span></span>

<span data-ttu-id="e37c9-134">Bu adımda, hello yerel Node.js projesi ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e37c9-134">In this step, you set up hello local Node.js project.</span></span>

### <a name="clone-hello-sample-application"></a><span data-ttu-id="e37c9-135">Merhaba örnek uygulaması kopyalama</span><span class="sxs-lookup"><span data-stu-id="e37c9-135">Clone hello sample application</span></span>

<span data-ttu-id="e37c9-136">Merhaba terminal penceresinde `cd` tooa çalışma dizini.</span><span class="sxs-lookup"><span data-stu-id="e37c9-136">In hello terminal window, `cd` tooa working directory.</span></span>  

<span data-ttu-id="e37c9-137">Çalışma hello aşağıdaki tooclone hello örnek depo komutu.</span><span class="sxs-lookup"><span data-stu-id="e37c9-137">Run hello following command tooclone hello sample repository.</span></span> 

```bash
git clone https://github.com/Azure-Samples/meanjs.git
```

<span data-ttu-id="e37c9-138">Bu örnek depo hello bir kopyasını içeren [MEAN.js depo](https://github.com/meanjs/mean).</span><span class="sxs-lookup"><span data-stu-id="e37c9-138">This sample repository contains a copy of hello [MEAN.js repository](https://github.com/meanjs/mean).</span></span> <span data-ttu-id="e37c9-139">Uygulama hizmeti üzerinde değiştirilmiş toorun olduğu (Merhaba MEAN.js depo daha fazla bilgi için bkz: [Benioku dosyasını](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).</span><span class="sxs-lookup"><span data-stu-id="e37c9-139">It is modified toorun on App Service (for more information, see hello MEAN.js repository [README file](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).</span></span>

### <a name="run-hello-application"></a><span data-ttu-id="e37c9-140">Merhaba uygulamayı çalıştırın</span><span class="sxs-lookup"><span data-stu-id="e37c9-140">Run hello application</span></span>

<span data-ttu-id="e37c9-141">Aşağıdaki komutları tooinstall hello gerekli paketleri hello çalıştırın ve hello uygulamasını başlatın.</span><span class="sxs-lookup"><span data-stu-id="e37c9-141">Run hello following commands tooinstall hello required packages and start hello application.</span></span>

```bash
cd meanjs
npm install
npm start
```

<span data-ttu-id="e37c9-142">Merhaba uygulama tam olarak yüklendiğinde iletiden benzeri toohello bakın:</span><span class="sxs-lookup"><span data-stu-id="e37c9-142">When hello app is fully loaded, you see something similar toohello following message:</span></span>

```
--
MEAN.JS - Development Environment

Environment:     development
Server:          http://0.0.0.0:3000
Database:        mongodb://localhost/mean-dev
App version:     0.5.0
MEAN.JS version: 0.5.0
--
```

<span data-ttu-id="e37c9-143">Bir tarayıcıda toohttp://localhost:3000 gidin.</span><span class="sxs-lookup"><span data-stu-id="e37c9-143">Navigate toohttp://localhost:3000 in a browser.</span></span> <span data-ttu-id="e37c9-144">Tıklatın **kaydolun** hello üst menü ve test kullanıcısı oluşturma.</span><span class="sxs-lookup"><span data-stu-id="e37c9-144">Click **Sign Up** in hello top menu and create a test user.</span></span> 

<span data-ttu-id="e37c9-145">Merhaba MEAN.js örnek uygulamanın kullanıcı verilerini hello veritabanında depolar.</span><span class="sxs-lookup"><span data-stu-id="e37c9-145">hello MEAN.js sample application stores user data in hello database.</span></span> <span data-ttu-id="e37c9-146">Kullanıcı oluşturma ve oturum açma başarılı olursa, uygulamanızın veri toohello yerel MongoDB veritabanı yazıyor.</span><span class="sxs-lookup"><span data-stu-id="e37c9-146">If you are successful at creating a user and signing in, then your app is writing data toohello local MongoDB database.</span></span>

![MEAN.js tooMongoDB başarıyla bağlanır.](./media/app-service-web-tutorial-nodejs-mongodb-app/mongodb-connect-success.png)

<span data-ttu-id="e37c9-148">Seçin **yönetici > yönetmek makaleleri** tooadd bazı makaleler.</span><span class="sxs-lookup"><span data-stu-id="e37c9-148">Select **Admin > Manage Articles** tooadd some articles.</span></span>

<span data-ttu-id="e37c9-149">herhangi bir zamanda Node.js toostop basın `Ctrl+C` hello terminal içinde.</span><span class="sxs-lookup"><span data-stu-id="e37c9-149">toostop Node.js at any time, press `Ctrl+C` in hello terminal.</span></span> 

## <a name="create-production-mongodb"></a><span data-ttu-id="e37c9-150">Üretim MongoDB oluşturma</span><span class="sxs-lookup"><span data-stu-id="e37c9-150">Create production MongoDB</span></span>

<span data-ttu-id="e37c9-151">Bu adımda, Azure MongoDB veritabanı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e37c9-151">In this step, you create a MongoDB database in Azure.</span></span> <span data-ttu-id="e37c9-152">Uygulamanızı dağıtılan tooAzure olduğunda, bu bulut veritabanını kullanır.</span><span class="sxs-lookup"><span data-stu-id="e37c9-152">When your app is deployed tooAzure, it uses this cloud database.</span></span>

<span data-ttu-id="e37c9-153">MongoDB için Bu öğretici kullanır [Azure Cosmos DB](/azure/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="e37c9-153">For MongoDB, this tutorial uses [Azure Cosmos DB](/azure/documentdb/).</span></span> <span data-ttu-id="e37c9-154">Cosmos DB MongoDB istemci bağlantılarını destekler.</span><span class="sxs-lookup"><span data-stu-id="e37c9-154">Cosmos DB supports MongoDB client connections.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="e37c9-155">İçinde tooAzure oturum</span><span class="sxs-lookup"><span data-stu-id="e37c9-155">Log in tooAzure</span></span>

<span data-ttu-id="e37c9-156">Uygulamanızı Azure'da hello Azure CLI 2.0 toocreate hello gerekli kaynakları toohost kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="e37c9-156">You'll use hello Azure CLI 2.0 toocreate hello resources needed toohost your app in Azure.</span></span> <span data-ttu-id="e37c9-157">Tooyour hello Azure aboneliğiyle oturum [az oturum açma](/cli/azure/#login) komut ve hello ekrandaki yönergeleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="e37c9-157">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span>

```azurecli-interactive
az login
```   

### <a name="create-a-resource-group"></a><span data-ttu-id="e37c9-158">Kaynak grubu oluşturma</span><span class="sxs-lookup"><span data-stu-id="e37c9-158">Create a resource group</span></span>

<span data-ttu-id="e37c9-159">Bir kaynak grubu ile Merhaba oluşturmak [az grubu oluşturma](/cli/azure/group#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="e37c9-159">Create a resource group with hello [az group create](/cli/azure/group#create) command.</span></span>

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="e37c9-160">Merhaba aşağıdaki örnekte bir kaynak grubu hello Batı Avrupa bölgede oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e37c9-160">hello following example creates a resource group in hello West Europe region.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

<span data-ttu-id="e37c9-161">Kullanım hello [az appservice listesi-konumları](/cli/azure/appservice#list-locations) Azure CLI toolist kullanılabilir konumlarını komutu.</span><span class="sxs-lookup"><span data-stu-id="e37c9-161">Use hello [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command toolist available locations.</span></span> 

### <a name="create-a-cosmos-db-account"></a><span data-ttu-id="e37c9-162">Cosmos DB hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e37c9-162">Create a Cosmos DB account</span></span>

<span data-ttu-id="e37c9-163">Cosmos DB hesabı ile Merhaba oluşturma [az cosmosdb oluşturma](/cli/azure/cosmosdb#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="e37c9-163">Create a Cosmos DB account with hello [az cosmosdb create](/cli/azure/cosmosdb#create) command.</span></span>

<span data-ttu-id="e37c9-164">Hello hello için benzersiz bir Cosmos DB ad yerine komutu, aşağıdaki  *\<cosmosdb_name >* yer tutucu.</span><span class="sxs-lookup"><span data-stu-id="e37c9-164">In hello following command, substitute a unique Cosmos DB name for hello *\<cosmosdb_name>* placeholder.</span></span> <span data-ttu-id="e37c9-165">Bu ad hello Cosmos DB endpoint hello parçası olarak kullanılır `https://<cosmosdb_name>.documents.azure.com/`, hello adı toobe benzersiz Azure içindeki tüm Cosmos DB hesaplar arasında olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e37c9-165">This name is used as hello part of hello Cosmos DB endpoint, `https://<cosmosdb_name>.documents.azure.com/`, so hello name needs toobe unique across all Cosmos DB accounts in Azure.</span></span> <span data-ttu-id="e37c9-166">Merhaba adı yalnızca küçük harf, sayı ve hello tire (-) karakterini içermelidir ve 3-50 karakter uzunluğunda olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e37c9-166">hello name must contain only lowercase letters, numbers, and hello hyphen (-) character, and must be between 3 and 50 characters long.</span></span>

```azurecli-interactive
az cosmosdb create \
    --name <cosmosdb_name> \
    --resource-group myResourceGroup \
    --kind MongoDB
```

<span data-ttu-id="e37c9-167">Merhaba *--tür MongoDB* parametresi MongoDB istemci bağlantıları sağlar.</span><span class="sxs-lookup"><span data-stu-id="e37c9-167">hello *--kind MongoDB* parameter enables MongoDB client connections.</span></span>

<span data-ttu-id="e37c9-168">Merhaba Cosmos DB hesabı oluşturulduğunda, hello Azure CLI aşağıdaki örneğine benzer toohello bilgileri gösterir:</span><span class="sxs-lookup"><span data-stu-id="e37c9-168">When hello Cosmos DB account is created, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "consistencyPolicy":
  {
    "defaultConsistencyLevel": "Session",
    "maxIntervalInSeconds": 5,
    "maxStalenessPrefix": 100
  },
  "databaseAccountOfferType": "Standard",
  "documentEndpoint": "https://<cosmosdb_name>.documents.azure.com:443/",
  "failoverPolicies": 
  ...
  < Output truncated for readability >
}
```

## <a name="connect-app-tooproduction-mongodb"></a><span data-ttu-id="e37c9-169">Uygulama tooproduction MongoDB Bağlan</span><span class="sxs-lookup"><span data-stu-id="e37c9-169">Connect app tooproduction MongoDB</span></span>

<span data-ttu-id="e37c9-170">Bu adımda, MongoDB bağlantı dizesi kullanarak oluşturduğunuz MEAN.js örnek uygulama toohello Cosmos DB veritabanınız bağlayın.</span><span class="sxs-lookup"><span data-stu-id="e37c9-170">In this step, you connect your MEAN.js sample application toohello Cosmos DB database you just created, using a MongoDB connection string.</span></span> 

### <a name="retrieve-hello-database-key"></a><span data-ttu-id="e37c9-171">Merhaba veritabanı anahtarı alma</span><span class="sxs-lookup"><span data-stu-id="e37c9-171">Retrieve hello database key</span></span>

<span data-ttu-id="e37c9-172">tooconnect toohello Cosmos DB veritabanı hello veritabanı anahtarı gerekir.</span><span class="sxs-lookup"><span data-stu-id="e37c9-172">tooconnect toohello Cosmos DB database, you need hello database key.</span></span> <span data-ttu-id="e37c9-173">Kullanım hello [az cosmosdb listesi anahtarlar](/cli/azure/cosmosdb#list-keys) komutu tooretrieve hello birincil anahtar.</span><span class="sxs-lookup"><span data-stu-id="e37c9-173">Use hello [az cosmosdb list-keys](/cli/azure/cosmosdb#list-keys) command tooretrieve hello primary key.</span></span>

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb_name> --resource-group myResourceGroup
```

<span data-ttu-id="e37c9-174">Hello Azure CLI aşağıdaki örneğine benzer toohello bilgileri gösterir:</span><span class="sxs-lookup"><span data-stu-id="e37c9-174">hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "primaryMasterKey": "RS4CmUwzGRASJPMoc0kiEvdnKmxyRILC9BWisAYh3Hq4zBYKr0XQiSE4pqx3UchBeO4QRCzUt1i7w0rOkitoJw==",
  "primaryReadonlyMasterKey": "HvitsjIYz8TwRmIuPEUAALRwqgKOzJUjW22wPL2U8zoMVhGvregBkBk9LdMTxqBgDETSq7obbwZtdeFY7hElTg==",
  "secondaryMasterKey": "Lu9aeZTiXU4PjuuyGBbvS1N9IRG3oegIrIh95U6VOstf9bJiiIpw3IfwSUgQWSEYM3VeEyrhHJ4rn3Ci0vuFqA==",
  "secondaryReadonlyMasterKey": "LpsCicpVZqHRy7qbMgrzbRKjbYCwCKPQRl0QpgReAOxMcggTvxJFA94fTi0oQ7xtxpftTJcXkjTirQ0pT7QFrQ=="
}
```

Merhaba değerini kopyalayın `primaryMasterKey`. <span data-ttu-id="e37c9-176">Bu bilgiler sonraki adımda hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="e37c9-176">You need this information in hello next step.</span></span>

<a name="devconfig"></a>
### <a name="configure-hello-connection-string-in-your-nodejs-application"></a><span data-ttu-id="e37c9-177">Node.js uygulamanızda Hello bağlantı dizesini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e37c9-177">Configure hello connection string in your Node.js application</span></span>

<span data-ttu-id="e37c9-178">MEAN.js deponuz açmak _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="e37c9-178">In your MEAN.js repository, open _config/env/production.js_.</span></span>

<span data-ttu-id="e37c9-179">Merhaba, `db` nesne, güncelleştirme hello değerini `uri`:</span><span class="sxs-lookup"><span data-stu-id="e37c9-179">In hello `db` object, update hello value of `uri`:</span></span>

* <span data-ttu-id="e37c9-180">Merhaba iki Değiştir  *\<cosmosdb_name >* Cosmos DB veritabanı adınız yer tutucularını.</span><span class="sxs-lookup"><span data-stu-id="e37c9-180">Replace hello two *\<cosmosdb_name>* placeholders with your Cosmos DB database name.</span></span>
* <span data-ttu-id="e37c9-181">Hello yerine  *\<primary_master_key >* hello önceki adımda kopyaladığınız hello anahtarla yer tutucu.</span><span class="sxs-lookup"><span data-stu-id="e37c9-181">Replace hello *\<primary_master_key>* placeholder with hello key you copied in hello previous step.</span></span>

<span data-ttu-id="e37c9-182">Merhaba aşağıdaki kod gösterir hello `db` nesnesi:</span><span class="sxs-lookup"><span data-stu-id="e37c9-182">hello following code shows hello `db` object:</span></span>

```javascript
db: {
  uri: 'mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false',
  ...
},
```

<span data-ttu-id="e37c9-183">Merhaba `ssl=true` seçeneği, çünkü gereklidir [Cosmos DB SSL gerekir](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span><span class="sxs-lookup"><span data-stu-id="e37c9-183">hello `ssl=true` option is required because [Cosmos DB requires SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements).</span></span> 

<span data-ttu-id="e37c9-184">Yaptığınız değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e37c9-184">Save your changes.</span></span>

### <a name="test-hello-application-in-production-mode"></a><span data-ttu-id="e37c9-185">Üretim modunda Hello uygulamayı test etme</span><span class="sxs-lookup"><span data-stu-id="e37c9-185">Test hello application in production mode</span></span> 

<span data-ttu-id="e37c9-186">Toominify ve paket komut hello üretim ortamı için aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e37c9-186">Run hello following command toominify and bundle scripts for hello production environment.</span></span> <span data-ttu-id="e37c9-187">Bu işlem hello üretim ortamı tarafından gerek hello dosyaları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="e37c9-187">This process generates hello files needed by hello production environment.</span></span>

```bash
gulp prod
```

<span data-ttu-id="e37c9-188">Komut toouse hello bağlantı dizesi, yapılandırdığınız aşağıdaki çalışma hello _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="e37c9-188">Run hello following command toouse hello connection string you configured in _config/env/production.js_.</span></span>

```bash
NODE_ENV=production node server.js
```

<span data-ttu-id="e37c9-189">`NODE_ENV=production`Node.js toorun hello üretim ortamında söyler hello ortam değişkenini ayarlar.</span><span class="sxs-lookup"><span data-stu-id="e37c9-189">`NODE_ENV=production` sets hello environment variable that tells Node.js toorun in hello production environment.</span></span>  <span data-ttu-id="e37c9-190">`node server.js`başlatır hello Node.js sunucusuyla `server.js` depo kök.</span><span class="sxs-lookup"><span data-stu-id="e37c9-190">`node server.js` starts hello Node.js server with `server.js` in your repository root.</span></span> <span data-ttu-id="e37c9-191">Azure'da Node.js uygulamanızı nasıl yüklenir budur.</span><span class="sxs-lookup"><span data-stu-id="e37c9-191">This is how your Node.js application is loaded in Azure.</span></span> 

<span data-ttu-id="e37c9-192">Merhaba uygulama yüklendiğinde toomake hello üretim ortamında çalıştığından emin denetleyin:</span><span class="sxs-lookup"><span data-stu-id="e37c9-192">When hello app is loaded, check toomake sure that it's running in hello production environment:</span></span>

```
--
MEAN.JS

Environment:     production
Server:          http://0.0.0.0:8443
Database:        mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false
App version:     0.5.0
MEAN.JS version: 0.5.0
```

<span data-ttu-id="e37c9-193">Bir tarayıcıda toohttp://localhost:8443 gidin.</span><span class="sxs-lookup"><span data-stu-id="e37c9-193">Navigate toohttp://localhost:8443 in a browser.</span></span> <span data-ttu-id="e37c9-194">Tıklatın **kaydolun** hello üst menü ve test kullanıcısı oluşturma.</span><span class="sxs-lookup"><span data-stu-id="e37c9-194">Click **Sign Up** in hello top menu and create a test user.</span></span> <span data-ttu-id="e37c9-195">Başarılı bir kullanıcı oluşturma ve oturum açma, uygulamanızı Azure'da veri toohello Cosmos DB veritabanı yazıyor.</span><span class="sxs-lookup"><span data-stu-id="e37c9-195">If you are successful creating a user and signing in, then your app is writing data toohello Cosmos DB database in Azure.</span></span> 

<span data-ttu-id="e37c9-196">Yazarak Hello terminal, Node.js durdurun `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="e37c9-196">In hello terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

## <a name="deploy-app-tooazure"></a><span data-ttu-id="e37c9-197">Uygulama tooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="e37c9-197">Deploy app tooAzure</span></span>

<span data-ttu-id="e37c9-198">Bu adımda, MongoDB bağlı Node.js uygulaması tooAzure uygulama hizmeti dağıtın.</span><span class="sxs-lookup"><span data-stu-id="e37c9-198">In this step, you deploy your MongoDB-connected Node.js application tooAzure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="e37c9-199">App Service planı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e37c9-199">Create an App Service plan</span></span>

<span data-ttu-id="e37c9-200">Merhaba ile bir uygulama hizmeti planı oluştur [az uygulama hizmeti planı oluşturma](/cli/azure/appservice/plan#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="e37c9-200">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="e37c9-201">Merhaba aşağıdaki örnekte oluşturur adlı bir uygulama hizmeti planı _myAppServicePlan_ hello kullanarak **serbest** fiyatlandırma katmanı:</span><span class="sxs-lookup"><span data-stu-id="e37c9-201">hello following example creates an App Service plan named _myAppServicePlan_ using hello **FREE** pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="e37c9-202">Uygulama hizmeti planı Hello oluşturulduğunda, hello Azure CLI bilgi benzer toohello aşağıdaki örneğine gösterir:</span><span class="sxs-lookup"><span data-stu-id="e37c9-202">When hello App Service plan is created, hello Azure CLI shows information similar toohello following example:</span></span>

```json 
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
```

### <a name="create-a-web-app"></a><span data-ttu-id="e37c9-203">Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="e37c9-203">Create a web app</span></span>

<span data-ttu-id="e37c9-204">Hello bir web uygulaması oluşturma `myAppServicePlan` hello ile uygulama hizmeti planı [az webapp oluşturmak](/cli/azure/webapp#create) komutu.</span><span class="sxs-lookup"><span data-stu-id="e37c9-204">Create a web app in hello `myAppServicePlan` App Service plan with hello [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="e37c9-205">dağıtılan uygulama, bir barındırma kodunuzu toodeploy boşluk ve sizin için bir URL tooview hello sağlar hello web uygulamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="e37c9-205">hello web app gives you a hosting space toodeploy your code and provides a URL for you tooview hello deployed application.</span></span> <span data-ttu-id="e37c9-206">Toocreate hello web uygulaması kullanın.</span><span class="sxs-lookup"><span data-stu-id="e37c9-206">Use  toocreate hello web app.</span></span> 

<span data-ttu-id="e37c9-207">Hello hello Değiştir komutu, aşağıdaki  *\<app_name >* yer tutucu benzersiz bir uygulama adına sahip.</span><span class="sxs-lookup"><span data-stu-id="e37c9-207">In hello following command, replace hello *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="e37c9-208">Merhaba adının toobe benzersiz Azure App Service'te tüm uygulamalarında gerekir böylece bu adı hello web uygulaması için hello varsayılan URL hello parçası olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e37c9-208">This name is used as hello part of hello default URL for hello web app, so hello name needs toobe unique across all apps in Azure App Service.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="e37c9-209">Merhaba web uygulaması oluşturduğunuzda aşağıdaki örneğine bilgi benzer toohello hello Azure CLI gösterir:</span><span class="sxs-lookup"><span data-stu-id="e37c9-209">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span> 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-an-environment-variable"></a><span data-ttu-id="e37c9-210">Bir ortam değişkeni yapılandırın</span><span class="sxs-lookup"><span data-stu-id="e37c9-210">Configure an environment variable</span></span>

<span data-ttu-id="e37c9-211">Başlangıç Öğreticisi, sabit kodlanmış hello veritabanı bağlantı dizesinde önceki _config/env/production.js_.</span><span class="sxs-lookup"><span data-stu-id="e37c9-211">Earlier in hello tutorial, you hardcoded hello database connection string in _config/env/production.js_.</span></span> <span data-ttu-id="e37c9-212">Mantığıyla en iyi güvenlik uygulaması, tookeep Git deponuzu dışında bu hassas verileri istiyor.</span><span class="sxs-lookup"><span data-stu-id="e37c9-212">In keeping with security best practice, you want tookeep this sensitive data out of your Git repository.</span></span> <span data-ttu-id="e37c9-213">Uygulamanız için Azure'da çalışan, bir ortam değişkeni kullanmanız.</span><span class="sxs-lookup"><span data-stu-id="e37c9-213">For your app running in Azure, you'll use an environment variable instead.</span></span>

<span data-ttu-id="e37c9-214">Ortam değişkenleri olarak ayarladığınız App Service'te _uygulama ayarları_ hello kullanarak [az webapp config appsettings güncelleştirme](/cli/azure/webapp/config/appsettings#update) komutu.</span><span class="sxs-lookup"><span data-stu-id="e37c9-214">In App Service, you set environment variables as _app settings_ by using hello [az webapp config appsettings update](/cli/azure/webapp/config/appsettings#update) command.</span></span> 

<span data-ttu-id="e37c9-215">Merhaba aşağıdaki örnek yapılandırır bir `MONGODB_URI` , Azure web uygulaması uygulama ayarı.</span><span class="sxs-lookup"><span data-stu-id="e37c9-215">hello following example configures a `MONGODB_URI` app setting in your Azure web app.</span></span> <span data-ttu-id="e37c9-216">Hello yerine  *\<app_name >*,  *\<cosmosdb_name >*, ve  *\<primary_master_key >* yer tutucuları.</span><span class="sxs-lookup"><span data-stu-id="e37c9-216">Replace hello *\<app_name>*, *\<cosmosdb_name>*, and *\<primary_master_key>* placeholders.</span></span>

```azurecli-interactive
az webapp config appsettings update \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings MONGODB_URI="mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true"
```

<span data-ttu-id="e37c9-217">Bu uygulama ayarı ile erişim node.js kodu `process.env.MONGODB_URI`herhangi bir ortam değişkeni erişim gibi.</span><span class="sxs-lookup"><span data-stu-id="e37c9-217">In Node.js code, you access this app setting with `process.env.MONGODB_URI`, just like you would access any environment variable.</span></span> 

<span data-ttu-id="e37c9-218">Şimdi, değişiklikleri too_config/env/production.js_ komutu aşağıdaki hello ile geri:</span><span class="sxs-lookup"><span data-stu-id="e37c9-218">Now, undo your changes too_config/env/production.js_ with hello following command:</span></span>

```bash
git checkout -- .
```

<span data-ttu-id="e37c9-219">Açık _config/env/production.js_ yeniden.</span><span class="sxs-lookup"><span data-stu-id="e37c9-219">Open _config/env/production.js_ again.</span></span> <span data-ttu-id="e37c9-220">Bu hello varsayılan MEAN.js uygulama zaten yapılandırılmış toouse hello Not `MONGODB_URI` oluşturduğunuz ortam değişkeni.</span><span class="sxs-lookup"><span data-stu-id="e37c9-220">Note that hello default MEAN.js app is already configured toouse hello `MONGODB_URI` environment variable that you created.</span></span>

```javascript
db: {
  uri: ... || process.env.MONGODB_URI || ...,
  ...
},
```

### <a name="configure-local-git-deployment"></a><span data-ttu-id="e37c9-221">Yerel git dağıtımını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e37c9-221">Configure local git deployment</span></span> 

<span data-ttu-id="e37c9-222">Kullanım hello [az webapp dağıtım kullanıcısı ayarlanmadı](/cli/azure/webapp/deployment/user#set) toocreate kimlik bilgileri dağıtımı için komutu.</span><span class="sxs-lookup"><span data-stu-id="e37c9-222">Use hello [az webapp deployment user set](/cli/azure/webapp/deployment/user#set) command toocreate credentials for deployment.</span></span>

<span data-ttu-id="e37c9-223">Uygulama tooAzure uygulama hizmeti FTP, yerel Git, GitHub, Visual Studio Team Services ve BitBucket dahil olmak üzere çeşitli yollarla dağıtabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e37c9-223">You can deploy your application tooAzure App Service in various ways including FTP, local Git, GitHub, Visual Studio Team Services, and BitBucket.</span></span> <span data-ttu-id="e37c9-224">FTP ve yerel Git için gerekli toohave dağıtım kullanıcı dağıtımınızı hello sunucu tooauthenticate üzerinde yapılandırılmış.</span><span class="sxs-lookup"><span data-stu-id="e37c9-224">For FTP and local Git, it is necessary toohave a deployment user configured on hello server tooauthenticate your deployment.</span></span> <span data-ttu-id="e37c9-225">Bu dağıtım kullanıcı hesabı düzeyi ve Azure abonelik hesabınızdan farklıdır.</span><span class="sxs-lookup"><span data-stu-id="e37c9-225">This deployment user is account-level and is different from your Azure subscription account.</span></span> <span data-ttu-id="e37c9-226">Yalnızca tooconfigure bu dağıtım kullanıcı kez gerekir.</span><span class="sxs-lookup"><span data-stu-id="e37c9-226">You only need tooconfigure this deployment user once.</span></span>

<span data-ttu-id="e37c9-227">Komut, aşağıdaki Hello yerine  *\<kullanıcı adı >* ve  *\<parola >* yeni bir kullanıcı adı ve parola ile.</span><span class="sxs-lookup"><span data-stu-id="e37c9-227">In hello following command, replace *\<user-name>* and *\<password>* with a new user name and password.</span></span> <span data-ttu-id="e37c9-228">Merhaba kullanıcı adının benzersiz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e37c9-228">hello user name must be unique.</span></span> <span data-ttu-id="e37c9-229">Merhaba parola en az sekiz karakter uzunluğunda, iki üç öğeleri aşağıdaki hello olmalıdır: harf, sayı, simge.</span><span class="sxs-lookup"><span data-stu-id="e37c9-229">hello password must be at least eight characters long, with two of hello following three elements:  letters, numbers, symbols.</span></span> <span data-ttu-id="e37c9-230">Alırsanız bir ` 'Conflict'. Details: 409` hata, değişiklik hello kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="e37c9-230">If you get a ` 'Conflict'. Details: 409` error, change hello username.</span></span> <span data-ttu-id="e37c9-231">` 'Bad Request'. Details: 400` hatası alırsanız daha güçlü bir parola kullanın.</span><span class="sxs-lookup"><span data-stu-id="e37c9-231">If you get a ` 'Bad Request'. Details: 400` error, use a stronger password.</span></span>

```azurecli-interactive
az appservice web deployment user set --user-name <username> --password <password>
```

<span data-ttu-id="e37c9-232">Kayıt hello kullanıcı adı ve parola hello uygulamayı dağıttığınızda daha sonraki adımlarda kullanılacak.</span><span class="sxs-lookup"><span data-stu-id="e37c9-232">Record hello user name and password for use in later steps when you deploy hello app.</span></span>

<span data-ttu-id="e37c9-233">Kullanım hello [az webapp dağıtım kaynağı config-yerel-git](/cli/azure/webapp/deployment/source#config-local-git) komutu tooconfigure yerel Git erişim toohello Azure web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="e37c9-233">Use hello [az webapp deployment source config-local-git](/cli/azure/webapp/deployment/source#config-local-git) command tooconfigure local Git access toohello Azure web app.</span></span> 

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup
```

<span data-ttu-id="e37c9-234">Merhaba dağıtım kullanıcı yapılandırıldığında, hello Azure CLI Azure web uygulamanız için hello dağıtım URL biçimi aşağıdaki hello gösterir:</span><span class="sxs-lookup"><span data-stu-id="e37c9-234">When hello deployment user is configured, hello Azure CLI shows hello deployment URL for your Azure web app in hello following format:</span></span>

```bash 
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git 
``` 

<span data-ttu-id="e37c9-235">Merhaba sonraki adımda kullanılacak şekilde hello terminal durumundan çıktı hello kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="e37c9-235">Copy hello output from hello terminal, as it will be used in hello next step.</span></span> 

### <a name="push-tooazure-from-git"></a><span data-ttu-id="e37c9-236">Anında iletme tooAzure Git</span><span class="sxs-lookup"><span data-stu-id="e37c9-236">Push tooAzure from Git</span></span>

<span data-ttu-id="e37c9-237">Bir Azure uzak tooyour yerel Git deposu ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e37c9-237">Add an Azure remote tooyour local Git repository.</span></span> 

```bash
git remote add azure <paste_copied_url_here> 
```

<span data-ttu-id="e37c9-238">Toohello Azure uzak toodeploy Node.js uygulamanızı iletin.</span><span class="sxs-lookup"><span data-stu-id="e37c9-238">Push toohello Azure remote toodeploy your Node.js application.</span></span> <span data-ttu-id="e37c9-239">Merhaba dağıtım kullanıcının hello oluşturmanın bir parçası daha önce sağlanan hello parolası istenir.</span><span class="sxs-lookup"><span data-stu-id="e37c9-239">You will be prompted for hello password you supplied earlier as part of hello creation of hello deployment user.</span></span> 

```bash
git push azure master
```

<span data-ttu-id="e37c9-240">Dağıtım sırasında Azure App Service, ilerleme durumunu Git ile iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="e37c9-240">During deployment, Azure App Service communicates its progress with Git.</span></span>

```bash
Counting objects: 5, done.
Delta compression using up too4 threads.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 489 bytes | 0 bytes/s, done.
Total 5 (delta 3), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '6c7c716eee'.
remote: Running custom deployment command...
remote: Running deployment command...
remote: Handling node.js deployment.
.
.
.
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
``` 

<span data-ttu-id="e37c9-241">Merhaba dağıtım işleminin çalıştığını fark edebilirsiniz [Gulp](http://gulpjs.com/) sonra `npm install`.</span><span class="sxs-lookup"><span data-stu-id="e37c9-241">You may notice that hello deployment process runs [Gulp](http://gulpjs.com/) after `npm install`.</span></span> <span data-ttu-id="e37c9-242">Uygulama hizmeti Gulp veya Grunt görevleri dağıtımı sırasında çalışmaz, bu örnek depo iki nedenle ek kendi kök dizin tooenable, dosyalarını:</span><span class="sxs-lookup"><span data-stu-id="e37c9-242">App Service does not run Gulp or Grunt tasks during deployment, so this sample repository has two additional files in its root directory tooenable it:</span></span> 

- <span data-ttu-id="e37c9-243">_.Deployment_ -uygulama hizmeti toorun bu dosya söyler `bash deploy.sh` hello özel dağıtım komut dosyası olarak.</span><span class="sxs-lookup"><span data-stu-id="e37c9-243">_.deployment_ - This file tells App Service toorun `bash deploy.sh` as hello custom deployment script.</span></span>
- <span data-ttu-id="e37c9-244">_Deploy.sh_ -hello özel dağıtım komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="e37c9-244">_deploy.sh_ - hello custom deployment script.</span></span> <span data-ttu-id="e37c9-245">Merhaba dosya gözden geçirirseniz, çalıştığını görürsünüz `gulp prod` sonra `npm install` ve `bower install`.</span><span class="sxs-lookup"><span data-stu-id="e37c9-245">If you review hello file, you will see that it runs `gulp prod` after `npm install` and `bower install`.</span></span> 

<span data-ttu-id="e37c9-246">Bu yaklaşım tooadd herhangi adım tooyour Git tabanlı bir dağıtım kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e37c9-246">You can use this approach tooadd any step tooyour Git-based deployment.</span></span> <span data-ttu-id="e37c9-247">Uygulama hizmeti, herhangi bir noktada, Azure web uygulamanızın yeniden başlatırsanız, bu otomasyon görevleri yeniden değil.</span><span class="sxs-lookup"><span data-stu-id="e37c9-247">If you restart your Azure web app at any point, App Service doesn't rerun these automation tasks.</span></span>

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="e37c9-248">Toohello Azure web uygulaması Gözat</span><span class="sxs-lookup"><span data-stu-id="e37c9-248">Browse toohello Azure web app</span></span> 

<span data-ttu-id="e37c9-249">Web tarayıcınız üzerinden dağıtılan toohello web uygulaması göz atın.</span><span class="sxs-lookup"><span data-stu-id="e37c9-249">Browse toohello deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
``` 

<span data-ttu-id="e37c9-250">Tıklatın **kaydolun** hello üst menü ve sahte bir kullanıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e37c9-250">Click **Sign Up** in hello top menu and create a dummy user.</span></span> 

<span data-ttu-id="e37c9-251">Başarılı ve hello uygulama otomatik olarak oturum açtığında kullanıcı sonra MEAN.js uygulamanızı Azure içinde oluşturulan toohello bağlantı toohello MongoDB (Cosmos DB) veritabanı yoktur.</span><span class="sxs-lookup"><span data-stu-id="e37c9-251">If you are successful and hello app automatically signs in toohello created user, then your MEAN.js app in Azure has connectivity toohello MongoDB (Cosmos DB) database.</span></span> 

![Azure App Service’te çalışan MEAN.js uygulaması](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

<span data-ttu-id="e37c9-253">Seçin **yönetici > yönetmek makaleleri** tooadd bazı makaleler.</span><span class="sxs-lookup"><span data-stu-id="e37c9-253">Select **Admin > Manage Articles** tooadd some articles.</span></span> 

<span data-ttu-id="e37c9-254">**Tebrikler!**</span><span class="sxs-lookup"><span data-stu-id="e37c9-254">**Congratulations!**</span></span> <span data-ttu-id="e37c9-255">Azure App Service'te veri güdümlü bir Node.js uygulaması kullanıyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="e37c9-255">You're running a data-driven Node.js app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="e37c9-256">Güncelleştirme veri modeli ve yeniden dağıtın</span><span class="sxs-lookup"><span data-stu-id="e37c9-256">Update data model and redeploy</span></span>

<span data-ttu-id="e37c9-257">Bu adımda, hello değiştirmek `article` veri modeli ve değişiklik tooAzure yayımlayın.</span><span class="sxs-lookup"><span data-stu-id="e37c9-257">In this step, you change hello `article` data model and publish your change tooAzure.</span></span>

### <a name="update-hello-data-model"></a><span data-ttu-id="e37c9-258">Güncelleştirme hello veri modeli</span><span class="sxs-lookup"><span data-stu-id="e37c9-258">Update hello data model</span></span>

<span data-ttu-id="e37c9-259">Açık _modules/articles/server/models/article.server.model.js_.</span><span class="sxs-lookup"><span data-stu-id="e37c9-259">Open _modules/articles/server/models/article.server.model.js_.</span></span>

<span data-ttu-id="e37c9-260">İçinde `ArticleSchema`, ekleme bir `String` adlı türü `comment`.</span><span class="sxs-lookup"><span data-stu-id="e37c9-260">In `ArticleSchema`, add a `String` type called `comment`.</span></span> <span data-ttu-id="e37c9-261">İşiniz bittiğinde, şema kodunuzu aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="e37c9-261">When you're done, your schema code should look like this:</span></span>

```javascript
var ArticleSchema = new Schema({
  ...,
  user: {
    type: Schema.ObjectId,
    ref: 'User'
  },
  comment: {
    type: String,
    default: '',
    trim: true
  }
});
```

### <a name="update-hello-articles-code"></a><span data-ttu-id="e37c9-262">Merhaba makaleleri kodunu güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="e37c9-262">Update hello articles code</span></span>

<span data-ttu-id="e37c9-263">Merhaba geri kalanı güncelleştirmek, `articles` toouse kod `comment`.</span><span class="sxs-lookup"><span data-stu-id="e37c9-263">Update hello rest of your `articles` code toouse `comment`.</span></span>

<span data-ttu-id="e37c9-264">Beş dosyaları toomodify ihtiyacınız vardır: hello server denetleyicisi ve hello dört istemci görünümleri.</span><span class="sxs-lookup"><span data-stu-id="e37c9-264">There are five files you need toomodify: hello server controller and hello four client views.</span></span> 

<span data-ttu-id="e37c9-265">Açık _modules/articles/server/controllers/articles.server.controller.js_.</span><span class="sxs-lookup"><span data-stu-id="e37c9-265">Open _modules/articles/server/controllers/articles.server.controller.js_.</span></span>

<span data-ttu-id="e37c9-266">Merhaba, `update` işlev, atama için ekleme `article.comment`.</span><span class="sxs-lookup"><span data-stu-id="e37c9-266">In hello `update` function, add an assignment for `article.comment`.</span></span> <span data-ttu-id="e37c9-267">Merhaba aşağıdaki kod gösterir tamamlandı hello `update` işlevi:</span><span class="sxs-lookup"><span data-stu-id="e37c9-267">hello following code shows hello completed `update` function:</span></span>

```javascript
exports.update = function (req, res) {
  var article = req.article;

  article.title = req.body.title;
  article.content = req.body.content;
  article.comment = req.body.comment;

  ...
};
```

<span data-ttu-id="e37c9-268">Açık _modules/articles/client/views/view-article.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="e37c9-268">Open _modules/articles/client/views/view-article.client.view.html_.</span></span>

<span data-ttu-id="e37c9-269">Merhaba kapanış hemen `</section>` etiket, satır toodisplay aşağıdaki hello eklemek `comment` hello kalan hello makale verileri birlikte:</span><span class="sxs-lookup"><span data-stu-id="e37c9-269">Just above hello closing `</section>` tag, add hello following line toodisplay `comment` along with hello rest of hello article data:</span></span>

```HTML
<p class="lead" ng-bind="vm.article.comment"></p>
```

<span data-ttu-id="e37c9-270">Açık _modules/articles/client/views/list-articles.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="e37c9-270">Open _modules/articles/client/views/list-articles.client.view.html_.</span></span>

<span data-ttu-id="e37c9-271">Merhaba kapanış hemen `</a>` etiket, satır toodisplay aşağıdaki hello eklemek `comment` hello kalan hello makale verileri birlikte:</span><span class="sxs-lookup"><span data-stu-id="e37c9-271">Just above hello closing `</a>` tag, add hello following line toodisplay `comment` along with hello rest of hello article data:</span></span>

```HTML
<p class="list-group-item-text" ng-bind="article.comment"></p>
```

<span data-ttu-id="e37c9-272">Açık _modules/articles/client/views/admin/list-articles.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="e37c9-272">Open _modules/articles/client/views/admin/list-articles.client.view.html_.</span></span>

<span data-ttu-id="e37c9-273">İç hello `<div class="list-group">` öğesi ve hemen önce hello kapanış `</a>` etiket, satır toodisplay aşağıdaki hello eklemek `comment` hello kalan hello makale verileri birlikte:</span><span class="sxs-lookup"><span data-stu-id="e37c9-273">Inside hello `<div class="list-group">` element and just above hello closing `</a>` tag, add hello following line toodisplay `comment` along with hello rest of hello article data:</span></span>

```HTML
<p class="list-group-item-text" data-ng-bind="article.comment"></p>
```

<span data-ttu-id="e37c9-274">Açık _modules/articles/client/views/admin/form-article.client.view.html_.</span><span class="sxs-lookup"><span data-stu-id="e37c9-274">Open _modules/articles/client/views/admin/form-article.client.view.html_.</span></span>

<span data-ttu-id="e37c9-275">Hello bulur `<div class="form-group">` hello Gönder düğmesi, bu gibi görünen içeren öğe:</span><span class="sxs-lookup"><span data-stu-id="e37c9-275">Find hello `<div class="form-group">` element that contains hello submit button, which looks like this:</span></span>

```HTML
<div class="form-group">
  <button type="submit" class="btn btn-default">{{vm.article._id ? 'Update' : 'Create'}}</button>
</div>
```

<span data-ttu-id="e37c9-276">Bu etiketi yalnızca başka bir tane eklemek `<div class="form-group">` hello Düzenle kişiler olanak sağlayan öğe `comment` alan.</span><span class="sxs-lookup"><span data-stu-id="e37c9-276">Just above this tag, add another `<div class="form-group">` element that lets people edit hello `comment` field.</span></span> <span data-ttu-id="e37c9-277">Yeni öğe aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="e37c9-277">Your new element should look like this:</span></span>

```HTML
<div class="form-group">
  <label class="control-label" for="comment">Comment</label>
  <textarea name="comment" data-ng-model="vm.article.comment" id="comment" class="form-control" cols="30" rows="10" placeholder="Comment"></textarea>
</div>
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="e37c9-278">Yaptığınız değişiklikler yerel olarak test etme</span><span class="sxs-lookup"><span data-stu-id="e37c9-278">Test your changes locally</span></span>

<span data-ttu-id="e37c9-279">Yaptığınız tüm değişiklikleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="e37c9-279">Save all your changes.</span></span>

<span data-ttu-id="e37c9-280">Değişikliklerinizi üretim modunda yeniden sınayın.</span><span class="sxs-lookup"><span data-stu-id="e37c9-280">Test your changes in production mode again.</span></span>

```bash
gulp prod
NODE_ENV=production node server.js
```

> [!NOTE]
> <span data-ttu-id="e37c9-281">Unutmayın, _config/env/production.js_ döndürüldü ve hello `MONGODB_URI` ortam değişkeni, Azure web uygulamanızda ve yerel makinenizde değil yalnızca ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e37c9-281">Remember that your _config/env/production.js_ has been reverted, and hello `MONGODB_URI` environment variable is only set in your Azure web app and not on your local machine.</span></span> <span data-ttu-id="e37c9-282">Merhaba yapılandırma dosyasını bakarsanız, o hello bulur üretim yapılandırma Varsayılanları toouse yerel bir MongoDB veritabanı.</span><span class="sxs-lookup"><span data-stu-id="e37c9-282">If you look at hello config file, you find that hello production configuration defaults toouse a local MongoDB database.</span></span> <span data-ttu-id="e37c9-283">Bu kod değişiklikleri yerel olarak test ettiğinizde üretim verileri touch yok emin olur.</span><span class="sxs-lookup"><span data-stu-id="e37c9-283">This makes sure that you don't touch production data when you test your code changes locally.</span></span>

<span data-ttu-id="e37c9-284">Çok gidin`http://localhost:8443` bir tarayıcıda ve oturum açtınız olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="e37c9-284">Navigate too`http://localhost:8443` in a browser and make sure that you're signed in.</span></span>

<span data-ttu-id="e37c9-285">Seçin **yönetici > yönetmek makaleleri**, ardından bir makale hello seçerek eklemek  **+**  düğmesi.</span><span class="sxs-lookup"><span data-stu-id="e37c9-285">Select **Admin > Manage Articles**, then add an article by selecting hello **+** button.</span></span>

<span data-ttu-id="e37c9-286">Merhaba yeni gördüğünüz `Comment` şimdi metin kutusu.</span><span class="sxs-lookup"><span data-stu-id="e37c9-286">You see hello new `Comment` textbox now.</span></span>

![Ek Açıklama alanı tooArticles](./media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field.png)

<span data-ttu-id="e37c9-288">Yazarak Hello terminal, Node.js durdurun `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="e37c9-288">In hello terminal, stop Node.js by typing `Ctrl+C`.</span></span> 

### <a name="publish-changes-tooazure"></a><span data-ttu-id="e37c9-289">Değişiklikleri tooAzure yayımlama</span><span class="sxs-lookup"><span data-stu-id="e37c9-289">Publish changes tooAzure</span></span>

<span data-ttu-id="e37c9-290">Git yaptığınız değişiklikleri kaydetmek ve ardından hello kod değişiklikleri tooAzure gönderme.</span><span class="sxs-lookup"><span data-stu-id="e37c9-290">Commit your changes in Git, then push hello code changes tooAzure.</span></span>

```bash
git commit -am "added article comment"
git push azure master
```

<span data-ttu-id="e37c9-291">Bir kez hello `git push` tamamlamak, tooyour Azure web uygulamasına gidin ve hello yeni işlevselliği deneyin.</span><span class="sxs-lookup"><span data-stu-id="e37c9-291">Once hello `git push` is complete, navigate tooyour Azure web app and try out hello new functionality.</span></span>

![Model ve veritabanı değişikliklerini tooAzure yayımlanan](media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field-published.png)

<span data-ttu-id="e37c9-293">Tüm makaleleri daha önce eklediyseniz, bunları yine görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e37c9-293">If you added any articles earlier, you still can see them.</span></span> <span data-ttu-id="e37c9-294">Cosmos veritabanında var olan veri kaybı olmadığından.</span><span class="sxs-lookup"><span data-stu-id="e37c9-294">Existing data in your Cosmos DB is not lost.</span></span> <span data-ttu-id="e37c9-295">Ayrıca, güncelleştirmelerinin toohello veri şemanızı ve varolan verilerinizi dokunmaz.</span><span class="sxs-lookup"><span data-stu-id="e37c9-295">Also, your updates toohello data schema and leaves your existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="e37c9-296">Akış tanılama günlükleri</span><span class="sxs-lookup"><span data-stu-id="e37c9-296">Stream diagnostic logs</span></span> 

<span data-ttu-id="e37c9-297">Node.js uygulamanızı Azure App Service'te çalışırken hello konsol günlükleri yöneltilen tooyour terminal elde edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e37c9-297">While your Node.js application runs in Azure App Service, you can get hello console logs piped tooyour terminal.</span></span> <span data-ttu-id="e37c9-298">Bu şekilde hello aynı tanılama iletileri alabilirsiniz uygulama hatalarını hata ayıklama toohelp.</span><span class="sxs-lookup"><span data-stu-id="e37c9-298">That way, you can get hello same diagnostic messages toohelp you debug application errors.</span></span>

<span data-ttu-id="e37c9-299">Akış, kullanım hello toostart günlük [az webapp günlük tail](/cli/azure/webapp/log#tail) komutu.</span><span class="sxs-lookup"><span data-stu-id="e37c9-299">toostart log streaming, use hello [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail --name <app_name> --resource-group myResourceGroup
``` 

<span data-ttu-id="e37c9-300">Günlük akış başladıktan sonra Azure web uygulamanızda hello tarayıcı tooget bazı web trafiği yenileyin.</span><span class="sxs-lookup"><span data-stu-id="e37c9-300">Once log streaming has started, refresh your Azure web app in hello browser tooget some web traffic.</span></span> <span data-ttu-id="e37c9-301">Şimdi, konsol günlükleri tooyour terminal yöneltilen bakın.</span><span class="sxs-lookup"><span data-stu-id="e37c9-301">You now see console logs piped tooyour terminal.</span></span>

<span data-ttu-id="e37c9-302">Herhangi bir zamanda yazarak akış günlük durdurma `Ctrl+C`.</span><span class="sxs-lookup"><span data-stu-id="e37c9-302">Stop log streaming at any time by typing `Ctrl+C`.</span></span> 

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="e37c9-303">Azure web uygulamanızı yönetme</span><span class="sxs-lookup"><span data-stu-id="e37c9-303">Manage your Azure web app</span></span>

<span data-ttu-id="e37c9-304">Toohello Git [Azure portal](https://portal.azure.com) oluşturduğunuz toosee hello web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="e37c9-304">Go toohello [Azure portal](https://portal.azure.com) toosee hello web app you created.</span></span>

<span data-ttu-id="e37c9-305">Merhaba sol menüden **uygulama hizmetleri**, Azure web uygulamanızın hello adını tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e37c9-305">From hello left menu, click **App Services**, then click hello name of your Azure web app.</span></span>

![Portal Gezinti tooAzure web uygulaması](./media/app-service-web-tutorial-nodejs-mongodb-app/access-portal.png)

<span data-ttu-id="e37c9-307">Varsayılan olarak, web uygulamanızın hello portal gösterir **genel bakış** sayfası.</span><span class="sxs-lookup"><span data-stu-id="e37c9-307">By default, hello portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="e37c9-308">Bu sayfa, uygulamanızın nasıl çalıştığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="e37c9-308">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="e37c9-309">Buradan ayrıca göz atma, durdurma, başlatma, yeniden başlatma ve silme gibi temel yönetim görevlerini gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e37c9-309">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="e37c9-310">Merhaba sekmeler hello sayfasının sol tarafında hello açabilirsiniz hello farklı yapılandırma sayfaları gösterir.</span><span class="sxs-lookup"><span data-stu-id="e37c9-310">hello tabs on hello left side of hello page show hello different configuration pages you can open.</span></span>

![Azure portalında App Service sayfası](./media/app-service-web-tutorial-nodejs-mongodb-app/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>
## <a name="next-steps"></a><span data-ttu-id="e37c9-312">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e37c9-312">Next steps</span></span>

<span data-ttu-id="e37c9-313">Öğrendiklerinizi:</span><span class="sxs-lookup"><span data-stu-id="e37c9-313">What you learned:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e37c9-314">MongoDB veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="e37c9-314">Create a MongoDB database in Azure</span></span>
> * <span data-ttu-id="e37c9-315">Bir Node.js uygulaması tooMongoDB Bağlan</span><span class="sxs-lookup"><span data-stu-id="e37c9-315">Connect a Node.js app tooMongoDB</span></span>
> * <span data-ttu-id="e37c9-316">Merhaba uygulama tooAzure dağıtma</span><span class="sxs-lookup"><span data-stu-id="e37c9-316">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="e37c9-317">Merhaba veri modeli güncelleştirmek ve hello uygulama yeniden dağıtın</span><span class="sxs-lookup"><span data-stu-id="e37c9-317">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="e37c9-318">Azure tooyour terminal akış günlükleri</span><span class="sxs-lookup"><span data-stu-id="e37c9-318">Stream logs from Azure tooyour terminal</span></span>
> * <span data-ttu-id="e37c9-319">Merhaba uygulamada hello Azure portalı Yönet</span><span class="sxs-lookup"><span data-stu-id="e37c9-319">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="e37c9-320">İlerlemek toohello sonraki öğretici toolearn nasıl toomap özel DNS ad tooyour web uygulaması.</span><span class="sxs-lookup"><span data-stu-id="e37c9-320">Advance toohello next tutorial toolearn how toomap a custom DNS name tooyour web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="e37c9-321">Harita bir var olan özel DNS adı tooAzure Web uygulamaları</span><span class="sxs-lookup"><span data-stu-id="e37c9-321">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
