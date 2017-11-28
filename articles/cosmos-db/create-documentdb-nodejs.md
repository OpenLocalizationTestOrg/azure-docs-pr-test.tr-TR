---
title: "Azure Cosmos DB: Node.js ile uygulama oluşturma ve DocumentDB API hello | Microsoft Docs"
description: "Tooconnect tooand sorgu kullanabileceğiniz bir Node.js kodu örneği hello Azure Cosmos DB DocumentDB API sunar"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 9c0f033c-240e-4fee-8421-08907231087f
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 287d860c7d6f788f05a397b238ef0f841c3c30ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-nodejs-and-hello-azure-portal"></a><span data-ttu-id="eb684-103">Azure Cosmos DB: Node.js ile DocumentDB API uygulaması oluşturma ve Azure portal hello</span><span class="sxs-lookup"><span data-stu-id="eb684-103">Azure Cosmos DB: Build a DocumentDB API app with Node.js and hello Azure portal</span></span>

<span data-ttu-id="eb684-104">Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="eb684-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="eb684-105">Hızlı bir şekilde oluşturmak ve belge, anahtar/değer ve grafik veritabanları, her biri hello genel dağıtım ve yatay ölçek özelliklerini Azure Cosmos DB'nin hello çekirdek yararlı sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb684-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="eb684-106">Bu hızlı başlangıç nasıl toocreate Azure Cosmos DB hesabınız, belge veritabanı ve koleksiyonu kullanarak Azure portalında hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="eb684-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="eb684-107">Ardından derlemeyi ve çalıştırmayı hello üzerinde oluşturulmuş bir konsol uygulaması [DocumentDB Node.js API](documentdb-sdk-node.md).</span><span class="sxs-lookup"><span data-stu-id="eb684-107">You then build and run a console app built on hello [DocumentDB Node.js API](documentdb-sdk-node.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eb684-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="eb684-108">Prerequisites</span></span>

* <span data-ttu-id="eb684-109">Bu örneği çalıştırmadan önce aşağıdaki önkoşullar hello sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="eb684-109">Before you can run this sample, you must have hello following prerequisites:</span></span>
    * <span data-ttu-id="eb684-110">[Node.js](https://nodejs.org/en/) sürüm v0.10.29 veya üzeri</span><span class="sxs-lookup"><span data-stu-id="eb684-110">[Node.js](https://nodejs.org/en/) version v0.10.29 or higher</span></span>
    * [<span data-ttu-id="eb684-111">Git</span><span class="sxs-lookup"><span data-stu-id="eb684-111">Git</span></span>](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="eb684-112">Veritabanı hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="eb684-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="eb684-113">Koleksiyon ekleme</span><span class="sxs-lookup"><span data-stu-id="eb684-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="eb684-114">Merhaba örnek uygulaması kopyalama</span><span class="sxs-lookup"><span data-stu-id="eb684-114">Clone hello sample application</span></span>

<span data-ttu-id="eb684-115">Artık şimdi github, kopya bir DocumentDB API uygulamasını hello bağlantı dizesini ayarlamak ve çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="eb684-115">Now let's clone a DocumentDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="eb684-116">Ne kadar kolay toowork verilerle program aracılığıyla olduğunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="eb684-116">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="eb684-117">Git bash gibi bir git terminal penceresi açın ve `CD` tooa çalışma dizini.</span><span class="sxs-lookup"><span data-stu-id="eb684-117">Open a git terminal window, such as git bash, and `CD` tooa working directory.</span></span>  

2. <span data-ttu-id="eb684-118">Çalışma hello aşağıdaki tooclone hello örnek depo komutu.</span><span class="sxs-lookup"><span data-stu-id="eb684-118">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-nodejs-getting-started.git
    ```

## <a name="review-hello-code"></a><span data-ttu-id="eb684-119">Merhaba kod gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="eb684-119">Review hello code</span></span>

<span data-ttu-id="eb684-120">Neler olduğuna dair hello uygulamada hızlı bir gözden geçirme olalım.</span><span class="sxs-lookup"><span data-stu-id="eb684-120">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="eb684-121">Açık hello `app.js` dosyanız varsa ve bulma Bu kod satırları hello Azure Cosmos DB kaynakları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="eb684-121">Open hello `app.js` file and you find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="eb684-122">Merhaba `documentClient` başlatılır.</span><span class="sxs-lookup"><span data-stu-id="eb684-122">hello `documentClient` is initialized.</span></span>

    ```nodejs
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });
    ```

* <span data-ttu-id="eb684-123">Yeni bir veritabanı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="eb684-123">A new database is created.</span></span>

    ```nodejs
    client.createDatabase(config.database, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="eb684-124">Yeni bir koleksiyon oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="eb684-124">A new collection is created.</span></span>

    ```nodejs
    client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="eb684-125">Birkaç belge oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="eb684-125">Some documents are created.</span></span>

    ```nodejs
    client.createDocument(collectionUrl, document, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* <span data-ttu-id="eb684-126">JSON üzerinden bir SQL sorgusu gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="eb684-126">A SQL query over JSON is performed.</span></span>

    ```nodejs
    client.queryDocuments(
        collectionUrl,
        'SELECT VALUE r.children FROM root r WHERE r.lastName = "Andersen"'
    ).toArray((err, results) => {
        if (err) reject(err)
        else {
            for (var queryResult of results) {
                let resultString = JSON.stringify(queryResult);
                console.log(`\tQuery returned ${resultString}`);
            }
            console.log();
            resolve(results);
        }
    });
    ```    

## <a name="update-your-connection-string"></a><span data-ttu-id="eb684-127">Bağlantı dizenizi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="eb684-127">Update your connection string</span></span>

<span data-ttu-id="eb684-128">Şimdi Azure portal tooget toohello bağlantı dizesi bilgilerinizi geri dönün ve hello uygulamaya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="eb684-128">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="eb684-129">Merhaba, [Azure portal](http://portal.azure.com/), Azure Cosmos DB hesap, sol gezinti hello tıklatın **anahtarları**ve ardından **okuma-yazma anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="eb684-129">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="eb684-130">Merhaba Kopyala düğmesi hello sağ tarafındaki Merhaba ekranında toocopy hello URI ve birincil anahtar hello kullanacağınız `config.js` hello sonraki adımda dosya.</span><span class="sxs-lookup"><span data-stu-id="eb684-130">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello `config.js` file in hello next step.</span></span>

    ![Görüntüleme ve kopyalama hello Azure portalına erişim tuşu, anahtarlar dikey penceresinde](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="eb684-132">Açık hello içinde `config.js` dosya.</span><span class="sxs-lookup"><span data-stu-id="eb684-132">In Open hello `config.js` file.</span></span> 

3. <span data-ttu-id="eb684-133">URI değeri (Merhaba Kopyala düğmesini kullanarak) hello Portal'dan kopyalayın ve hale hello hello uç noktası anahtarı değerini `config.js`.</span><span class="sxs-lookup"><span data-stu-id="eb684-133">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint key in `config.js`.</span></span> 

    `config.endpoint = "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="eb684-134">Sonra birincil anahtar değer hello Portal'dan kopyalayın ve kolaylaştırır hello hello değerini `config.primaryKey` içinde `config.js`.</span><span class="sxs-lookup"><span data-stu-id="eb684-134">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello `config.primaryKey` in `config.js`.</span></span> <span data-ttu-id="eb684-135">Uygulamanızı şimdi güncelleştirdikten toocommunicate Azure Cosmos DB ile gerekli tüm hello bilgilerine sahip.</span><span class="sxs-lookup"><span data-stu-id="eb684-135">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

    `config.primaryKey "FILLME"`
    
## <a name="run-hello-app"></a><span data-ttu-id="eb684-136">Merhaba uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="eb684-136">Run hello app</span></span>
1. <span data-ttu-id="eb684-137">Çalıştırma `npm install` npm modülleri içinde terminal tooinstall gerekli</span><span class="sxs-lookup"><span data-stu-id="eb684-137">Run `npm install` in a terminal tooinstall required npm modules</span></span>

2. <span data-ttu-id="eb684-138">Çalıştırma `node app.js` terminal toostart içinde düğüm uygulamanızı.</span><span class="sxs-lookup"><span data-stu-id="eb684-138">Run `node app.js` in a terminal toostart your node application.</span></span>

<span data-ttu-id="eb684-139">Şimdi tooData Explorer geri dönün ve sorgu görmek değiştirmek ve bu yeni verilerle çalışmak.</span><span class="sxs-lookup"><span data-stu-id="eb684-139">You can now go back tooData Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="eb684-140">Gözden geçirme SLA'hello Azure portalı</span><span class="sxs-lookup"><span data-stu-id="eb684-140">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="eb684-141">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="eb684-141">Clean up resources</span></span>

<span data-ttu-id="eb684-142">Toocontinue toouse bu uygulamayı değil kullanacaksanız, bu hızlı başlangıç tarafından hello Azure portalında aşağıdaki adımları hello ile oluşturulan tüm kaynakları silin:</span><span class="sxs-lookup"><span data-stu-id="eb684-142">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="eb684-143">Merhaba sol taraftaki menüden hello Azure portal'ın, **kaynak grupları** ve ardından oluşturduğunuz hello kaynak hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="eb684-143">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="eb684-144">Kaynak grubu sayfanızda tıklatın **silmek**hello metin kutusuna hello kaynak toodelete hello adını yazın ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="eb684-144">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb684-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="eb684-145">Next steps</span></span>

<span data-ttu-id="eb684-146">Bu hızlı başlangıç toocreate bir Azure Cosmos DB hesap hello Veri Gezgini'ni kullanarak bir koleksiyon oluşturma ve bir uygulama çalıştırmasına öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="eb684-146">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run an app.</span></span> <span data-ttu-id="eb684-147">Artık ek verileri tooyour Cosmos DB hesap içeri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eb684-147">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="eb684-148">Azure Cosmos DB hesabınıza veri aktarma</span><span class="sxs-lookup"><span data-stu-id="eb684-148">Import data into Azure Cosmos DB</span></span>](import-data.md)


