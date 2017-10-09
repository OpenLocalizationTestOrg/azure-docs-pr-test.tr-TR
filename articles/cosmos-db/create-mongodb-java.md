---
title: "Azure Cosmos DB: Java ile bir konsol uygulaması oluşturun ve MongoDB API hello | Microsoft Docs"
description: "Tooconnect tooand sorgu kullanabileceğiniz bir Java kod örneği hello Azure Cosmos DB MongoDB API sunar"
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
ms.devlang: java
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: fbe416f6b20ed2bb83a1d41eb70ffc6e3cee2b61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-java-and-hello-azure-portal"></a><span data-ttu-id="db585-103">Azure Cosmos DB: Java ile MongoDB API konsol uygulaması oluşturma ve Azure portal hello</span><span class="sxs-lookup"><span data-stu-id="db585-103">Azure Cosmos DB: Build a MongoDB API console app with Java and hello Azure portal</span></span>

<span data-ttu-id="db585-104">Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="db585-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="db585-105">Hızlı bir şekilde oluşturmak ve belge, anahtar/değer ve grafik veritabanları, her biri hello genel dağıtım ve yatay ölçek özelliklerini Azure Cosmos DB'nin hello çekirdek yararlı sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db585-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="db585-106">Bu hızlı başlangıç nasıl toocreate Azure Cosmos DB hesabınız, belge veritabanı ve koleksiyonu kullanarak Azure portalında hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="db585-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="db585-107">Daha sonra yapı ve hello üzerinde oluşturulmuş bir konsol uygulaması dağıtma [MongoDB Java sürücü](https://docs.mongodb.com/ecosystem/drivers/java/).</span><span class="sxs-lookup"><span data-stu-id="db585-107">You'll then build and deploy a console app built on hello [MongoDB Java driver](https://docs.mongodb.com/ecosystem/drivers/java/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="db585-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="db585-108">Prerequisites</span></span>

* <span data-ttu-id="db585-109">Bu örneği çalıştırmadan önce aşağıdaki önkoşullar hello sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="db585-109">Before you can run this sample, you must have hello following prerequisites:</span></span>
   * <span data-ttu-id="db585-110">JDK 1.7+ (JDK yoksa `apt-get install default-jdk` komutunu çalıştırın)</span><span class="sxs-lookup"><span data-stu-id="db585-110">JDK 1.7+ (Run `apt-get install default-jdk` if you don't have JDK)</span></span>
   * <span data-ttu-id="db585-111">Maven (Maven yoksa `apt-get install maven` komutunu çalıştırın)</span><span class="sxs-lookup"><span data-stu-id="db585-111">Maven (Run `apt-get install maven` if you don't have Maven)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="db585-112">Veritabanı hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="db585-112">Create a database account</span></span>

[!INCLUDE [mongodb-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="add-a-collection"></a><span data-ttu-id="db585-113">Koleksiyon ekleme</span><span class="sxs-lookup"><span data-stu-id="db585-113">Add a collection</span></span>

<span data-ttu-id="db585-114">Yeni veritabanınıza **db**, yeni koleksiyonunuza da **coll** adını verin.</span><span class="sxs-lookup"><span data-stu-id="db585-114">Name your new database, **db**, and your new collection, **coll**.</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="db585-115">Merhaba örnek uygulaması kopyalama</span><span class="sxs-lookup"><span data-stu-id="db585-115">Clone hello sample application</span></span>

<span data-ttu-id="db585-116">Artık şimdi github, kopya bir MongoDB API uygulamasını hello bağlantı dizesini ayarlamak ve çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="db585-116">Now let's clone a MongoDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="db585-117">Ne kadar kolay toowork verilerle program aracılığıyla olduğunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="db585-117">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="db585-118">Git bash gibi bir git terminal penceresi açın ve `cd` tooa çalışma dizini.</span><span class="sxs-lookup"><span data-stu-id="db585-118">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="db585-119">Çalışma hello aşağıdaki tooclone hello örnek depo komutu.</span><span class="sxs-lookup"><span data-stu-id="db585-119">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started.git
    ```

3. <span data-ttu-id="db585-120">Ardından Visual Studio'da hello çözüm dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="db585-120">Then open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="db585-121">Merhaba kod gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="db585-121">Review hello code</span></span>

<span data-ttu-id="db585-122">Neler olduğuna dair hello uygulamada hızlı bir gözden geçirme olalım.</span><span class="sxs-lookup"><span data-stu-id="db585-122">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="db585-123">Açık hello `Program.cs` dosyanız varsa ve bulabileceğiniz bu kod satırları hello Azure Cosmos DB kaynakları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="db585-123">Open hello `Program.cs` file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="db585-124">Merhaba DocumentClient başlatılır.</span><span class="sxs-lookup"><span data-stu-id="db585-124">hello DocumentClient is initialized.</span></span>

    ```java
    MongoClientURI uri = new MongoClientURI("FILLME");`

    MongoClient mongoClient = new MongoClient(uri);            
    ```

* <span data-ttu-id="db585-125">Yeni bir veritabanı ve koleksiyonu oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="db585-125">A new database and collection are created.</span></span>

    ```java
    MongoDatabase database = mongoClient.getDatabase("db");

    MongoCollection<Document> collection = database.getCollection("coll");
    ```

* <span data-ttu-id="db585-126">`MongoCollection.insertOne` kullanılarak birkaç belge eklenir</span><span class="sxs-lookup"><span data-stu-id="db585-126">Some documents are inserted using `MongoCollection.insertOne`</span></span>

    ```java
    Document document = new Document("fruit", "apple")
    collection.insertOne(document);
    ```

* <span data-ttu-id="db585-127">`MongoCollection.find` kullanılarak birkaç sorgu gerçekleştirilir</span><span class="sxs-lookup"><span data-stu-id="db585-127">Some queries are performed using `MongoCollection.find`</span></span>

    ```java
    Document queryResult = collection.find(Filters.eq("fruit", "apple")).first();
    System.out.println(queryResult.toJson());       
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="db585-128">Bağlantı dizenizi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="db585-128">Update your connection string</span></span>

<span data-ttu-id="db585-129">Şimdi Azure portal tooget toohello bağlantı dizesi bilgilerinizi geri dönün ve hello uygulamaya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="db585-129">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="db585-130">Hello ifadesini hesabı seçin **Hızlı Başlangıç**Java seçin, ardından hello bağlantı dizesi tooyour Panoya Kopyala</span><span class="sxs-lookup"><span data-stu-id="db585-130">From hello Account, select **Quick Start**, select Java, then copy hello connection string tooyour clipboard</span></span>

2. <span data-ttu-id="db585-131">Açık hello `Program.java` dosya, hello bağımsız değişkeni toohello MongoClientURI Oluşturucusu hello bağlantı dizesi ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="db585-131">Open hello `Program.java` file, replace hello argument toohello MongoClientURI constructor with hello connection string.</span></span> <span data-ttu-id="db585-132">Uygulamanızı şimdi güncelleştirdikten toocommunicate Azure Cosmos DB ile gerekli tüm hello bilgilerine sahip.</span><span class="sxs-lookup"><span data-stu-id="db585-132">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-hello-console-app"></a><span data-ttu-id="db585-133">Merhaba konsol uygulamasını çalıştırın</span><span class="sxs-lookup"><span data-stu-id="db585-133">Run hello console app</span></span>

1. <span data-ttu-id="db585-134">Çalıştırma `mvn package` npm modülleri içinde terminal tooinstall gerekli</span><span class="sxs-lookup"><span data-stu-id="db585-134">Run `mvn package` in a terminal tooinstall required npm modules</span></span>

2. <span data-ttu-id="db585-135">Çalıştırma `mvn exec:java -D exec.mainClass=GetStarted.Program` terminal toostart içinde Java uygulaması.</span><span class="sxs-lookup"><span data-stu-id="db585-135">Run `mvn exec:java -D exec.mainClass=GetStarted.Program` in a terminal toostart your Java application.</span></span>

<span data-ttu-id="db585-136">Artık kullanabilirsiniz [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) tooquery, değiştirebilir ve bu yeni verilerle çalışma.</span><span class="sxs-lookup"><span data-stu-id="db585-136">You can now use [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) tooquery, modify, and work with this new data.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="db585-137">Gözden geçirme SLA'hello Azure portalı</span><span class="sxs-lookup"><span data-stu-id="db585-137">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="db585-138">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="db585-138">Clean up resources</span></span>

<span data-ttu-id="db585-139">Toocontinue toouse bu uygulamayı değil kullanacaksanız, bu hızlı başlangıç tarafından hello Azure portalında aşağıdaki adımları hello ile oluşturulan tüm kaynakları silin:</span><span class="sxs-lookup"><span data-stu-id="db585-139">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="db585-140">Merhaba sol taraftaki menüden hello Azure portal'ın, **kaynak grupları** ve ardından oluşturduğunuz hello kaynak hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="db585-140">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="db585-141">Kaynak grubu sayfanızda tıklatın **silmek**hello metin kutusuna hello kaynak toodelete hello adını yazın ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="db585-141">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="db585-142">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="db585-142">Next steps</span></span>

<span data-ttu-id="db585-143">Bu hızlı başlangıç nasıl toocreate bir Azure Cosmos DB hesap hello Veri Gezgini'ni kullanarak bir koleksiyon oluşturun ve bir konsol uygulaması çalıştırın öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="db585-143">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run a console app.</span></span> <span data-ttu-id="db585-144">Artık ek verileri tooyour Cosmos DB hesap içeri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="db585-144">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="db585-145">Azure Cosmos DB’ye MongoDB verileri aktarma</span><span class="sxs-lookup"><span data-stu-id="db585-145">Import MongoDB data into Azure Cosmos DB</span></span>](mongodb-migrate.md)


