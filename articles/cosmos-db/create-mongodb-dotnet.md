---
title: "Azure Cosmos DB: .NET ile bir web uygulaması oluşturma ve API MongoDB hello | Microsoft Docs"
description: "Tooconnect tooand sorgu kullanabileceğiniz bir .NET kod örneği hello Azure Cosmos DB MongoDB API sunar"
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
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: c85cc47f772a19aaa7181611b75a8acaedbc4c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-web-app-with-net-and-hello-azure-portal"></a><span data-ttu-id="9a9f7-103">Azure Cosmos DB: .NET ile MongoDB API web uygulaması oluşturma ve Azure portal hello</span><span class="sxs-lookup"><span data-stu-id="9a9f7-103">Azure Cosmos DB: Build a MongoDB API web app with .NET and hello Azure portal</span></span>

<span data-ttu-id="9a9f7-104">Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="9a9f7-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="9a9f7-105">Hızlı bir şekilde oluşturmak ve belge, anahtar/değer ve grafik veritabanları, her biri hello genel dağıtım ve yatay ölçek özelliklerini Azure Cosmos DB'nin hello çekirdek yararlı sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a9f7-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="9a9f7-106">Bu hızlı başlangıç nasıl toocreate Azure Cosmos DB hesabınız, belge veritabanı ve koleksiyonu kullanarak Azure portalında hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="9a9f7-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="9a9f7-107">Daha sonra yapı ve hello üzerinde oluşturulmuş bir görevler listesi web uygulaması dağıtma [MongoDB .NET sürücü](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span><span class="sxs-lookup"><span data-stu-id="9a9f7-107">You'll then build and deploy a tasks list web app built on hello [MongoDB .NET driver](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9a9f7-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9a9f7-108">Prerequisites</span></span>

<span data-ttu-id="9a9f7-109">Visual Studio yüklü 2017 zaten sahip değilseniz, indirin ve hello kullan **ücretsiz** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="9a9f7-109">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="9a9f7-110">Etkinleştirdiğinizden emin olun **Azure geliştirme** hello Visual Studio Kurulumu sırasında.</span><span class="sxs-lookup"><span data-stu-id="9a9f7-110">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="9a9f7-111">Veritabanı hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="9a9f7-111">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="9a9f7-112">Merhaba örnek uygulaması kopyalama</span><span class="sxs-lookup"><span data-stu-id="9a9f7-112">Clone hello sample application</span></span>

<span data-ttu-id="9a9f7-113">Artık şimdi github, kopya bir MongoDB API uygulamasını hello bağlantı dizesini ayarlamak ve çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9a9f7-113">Now let's clone a MongoDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="9a9f7-114">Ne kadar kolay toowork verilerle program aracılığıyla olduğunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="9a9f7-114">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="9a9f7-115">Git bash gibi bir git terminal penceresi açın ve `cd` tooa çalışma dizini.</span><span class="sxs-lookup"><span data-stu-id="9a9f7-115">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="9a9f7-116">Çalışma hello aşağıdaki tooclone hello örnek depo komutu.</span><span class="sxs-lookup"><span data-stu-id="9a9f7-116">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-getting-started.git
    ```

3. <span data-ttu-id="9a9f7-117">Ardından Visual Studio'da hello çözüm dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="9a9f7-117">Then open hello solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="9a9f7-118">Merhaba kod gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="9a9f7-118">Review hello code</span></span>

<span data-ttu-id="9a9f7-119">Neler olduğuna dair hello uygulamada hızlı bir gözden geçirme olalım.</span><span class="sxs-lookup"><span data-stu-id="9a9f7-119">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="9a9f7-120">Açık hello **Dal.cs** dosyasını hello altında **DAL** dizin ve bulabileceğiniz bu kod satırları hello Azure Cosmos DB kaynakları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9a9f7-120">Open hello **Dal.cs** file under hello **DAL** directory and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="9a9f7-121">Merhaba Mongo istemci başlatır.</span><span class="sxs-lookup"><span data-stu-id="9a9f7-121">Initialize hello Mongo Client.</span></span>

    ```cs
        MongoClientSettings settings = new MongoClientSettings();
        settings.Server = new MongoServerAddress(host, 10255);
        settings.UseSsl = true;
        settings.SslSettings = new SslSettings();
        settings.SslSettings.EnabledSslProtocols = SslProtocols.Tls12;

        MongoIdentity identity = new MongoInternalIdentity(dbName, userName);
        MongoIdentityEvidence evidence = new PasswordEvidence(password);

        settings.Credentials = new List<MongoCredential>()
        {
            new MongoCredential("SCRAM-SHA-1", identity, evidence)
        };

        MongoClient client = new MongoClient(settings);
    ```

* <span data-ttu-id="9a9f7-122">Merhaba veritabanı ve hello koleksiyonu alır.</span><span class="sxs-lookup"><span data-stu-id="9a9f7-122">Retrieve hello database and hello collection.</span></span>

    ```cs
    private string dbName = "Tasks";
    private string collectionName = "TasksList";

    var database = client.GetDatabase(dbName);
    var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
    ```

* <span data-ttu-id="9a9f7-123">Tüm belgeleri alın.</span><span class="sxs-lookup"><span data-stu-id="9a9f7-123">Retrieve all documents.</span></span>

    ```cs
    collection.Find(new BsonDocument()).ToList();
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="9a9f7-124">Bağlantı dizenizi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="9a9f7-124">Update your connection string</span></span>

<span data-ttu-id="9a9f7-125">Şimdi Azure portal tooget toohello bağlantı dizesi bilgilerinizi geri dönün ve hello uygulamaya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="9a9f7-125">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="9a9f7-126">Merhaba, [Azure portal](http://portal.azure.com/), Azure Cosmos DB hesap, sol gezinti hello tıklatın **bağlantı dizesi**ve ardından **okuma-yazma anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="9a9f7-126">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Connection String**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="9a9f7-127">Merhaba sonraki adımda hello Dal.cs dosyasına hello Kopyala düğmesi hello sağ tarafında Merhaba ekranında toocopy hello kullanıcı adı, parola ve ana bilgisayar kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="9a9f7-127">You'll use hello copy buttons on hello right side of hello screen toocopy hello Username, Password, and Host into hello Dal.cs file in hello next step.</span></span>

2. <span data-ttu-id="9a9f7-128">Açık hello **Dal.cs** hello dosyasında **DAL** dizin.</span><span class="sxs-lookup"><span data-stu-id="9a9f7-128">Open hello **Dal.cs** file in hello **DAL** directory.</span></span> 

3. <span data-ttu-id="9a9f7-129">Kopyalama, **kullanıcıadı** değeri (Merhaba Kopyala düğmesini kullanarak) hello portalından ve hale hello hello değerini **kullanıcı adı** içinde **Dal.cs** dosya.</span><span class="sxs-lookup"><span data-stu-id="9a9f7-129">Copy your **username** value from hello portal (using hello copy button) and make it hello value of hello **username** in your **Dal.cs** file.</span></span> 

4. <span data-ttu-id="9a9f7-130">Daha sonra kopyalayın, **konak** değer hello portalından ve yapmak hello hello değerini **konak** içinde **Dal.cs** dosya.</span><span class="sxs-lookup"><span data-stu-id="9a9f7-130">Then copy your **host** value from hello portal and make it hello value of hello **host** in your **Dal.cs** file.</span></span> 

5. <span data-ttu-id="9a9f7-131">Son olarak kopyalamak, **parola** değer hello portalından ve hale hello hello değerini **parola** içinde **Dal.cs** dosya.</span><span class="sxs-lookup"><span data-stu-id="9a9f7-131">Finally copy your **password** value from hello portal and make it hello value of hello **password** in your **Dal.cs** file.</span></span> 

<span data-ttu-id="9a9f7-132">Uygulamanızı şimdi güncelleştirdikten toocommunicate Azure Cosmos DB ile gerekli tüm hello bilgilerine sahip.</span><span class="sxs-lookup"><span data-stu-id="9a9f7-132">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-hello-web-app"></a><span data-ttu-id="9a9f7-133">Merhaba web uygulaması çalıştırın</span><span class="sxs-lookup"><span data-stu-id="9a9f7-133">Run hello web app</span></span>

1. <span data-ttu-id="9a9f7-134">Visual Studio'da hello projeye sağ tıklayın **Çözüm Gezgini** ve ardından **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="9a9f7-134">In Visual Studio, right-click on hello project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="9a9f7-135">Merhaba NuGet içinde **Gözat** kutusuna *MongoDB.Driver*.</span><span class="sxs-lookup"><span data-stu-id="9a9f7-135">In hello NuGet **Browse** box, type *MongoDB.Driver*.</span></span>

3. <span data-ttu-id="9a9f7-136">Merhaba sonuçlarından hello yüklemek **MongoDB.Driver** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="9a9f7-136">From hello results, install hello **MongoDB.Driver** library.</span></span> <span data-ttu-id="9a9f7-137">Bu, tüm bağımlılıkları yanı sıra hello MongoDB.Driver paketi yükler.</span><span class="sxs-lookup"><span data-stu-id="9a9f7-137">This installs hello MongoDB.Driver package as well as all dependencies.</span></span>

4. <span data-ttu-id="9a9f7-138">CTRL + F5'e tıklayın toorun Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="9a9f7-138">Click CTRL + F5 toorun hello application.</span></span> <span data-ttu-id="9a9f7-139">Uygulamanız tarayıcınızda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="9a9f7-139">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="9a9f7-140">Tıklatın **oluşturma** hello tarayıcı ve görev listesi uygulamanızda birkaç yeni görevler oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="9a9f7-140">Click **Create** in hello browser and create a few new tasks in your task list app.</span></span>

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="9a9f7-141">Gözden geçirme SLA'hello Azure portalı</span><span class="sxs-lookup"><span data-stu-id="9a9f7-141">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="9a9f7-142">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="9a9f7-142">Clean up resources</span></span>

<span data-ttu-id="9a9f7-143">Toocontinue toouse bu uygulamayı değil kullanacaksanız, bu hızlı başlangıç tarafından hello Azure portalında aşağıdaki adımları hello ile oluşturulan tüm kaynakları silin:</span><span class="sxs-lookup"><span data-stu-id="9a9f7-143">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="9a9f7-144">Merhaba sol taraftaki menüden hello Azure portal'ın, **kaynak grupları** ve ardından oluşturduğunuz hello kaynak hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="9a9f7-144">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="9a9f7-145">Kaynak grubu sayfanızda tıklatın **silmek**hello metin kutusuna hello kaynak toodelete hello adını yazın ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="9a9f7-145">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a9f7-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9a9f7-146">Next steps</span></span>

<span data-ttu-id="9a9f7-147">Bu hızlı başlangıç nasıl toocreate bir Azure Cosmos DB hesap ve bir web uygulamasını kullanarak çalışma MongoDB için API hello öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="9a9f7-147">In this quickstart, you've learned how toocreate an Azure Cosmos DB account and run a web app using hello API for MongoDB.</span></span> <span data-ttu-id="9a9f7-148">Artık ek verileri tooyour Cosmos DB hesap içeri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a9f7-148">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="9a9f7-149">Merhaba MongoDB API Azure Cosmos Veritabanına veri alma</span><span class="sxs-lookup"><span data-stu-id="9a9f7-149">Import data into Azure Cosmos DB for hello MongoDB API</span></span>](mongodb-migrate.md)

