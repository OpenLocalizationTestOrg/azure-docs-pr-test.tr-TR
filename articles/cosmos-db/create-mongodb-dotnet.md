---
title: "Azure Cosmos DB: .NET ve MongoDB API'si ile bir web uygulaması derleme | Microsoft Docs"
description: "Azure Cosmos DB MongoDB API'sine bağlanmak ve sorgu göndermek için kullanabileceğiniz bir .NET kodu örneği sunar"
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
ms.openlocfilehash: 2d30bec75d701b1fd55355d1e139350b6d828c9a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-web-app-with-net-and-the-azure-portal"></a><span data-ttu-id="daad3-103">Azure Cosmos DB: .NET ve Azure portalı ile bir MongoDB API'si web uygulaması derleme</span><span class="sxs-lookup"><span data-stu-id="daad3-103">Azure Cosmos DB: Build a MongoDB API web app with .NET and the Azure portal</span></span>

<span data-ttu-id="daad3-104">Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="daad3-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="daad3-105">Bu hizmetle belge, anahtar/değer ve grafik veritabanlarını kolayca oluşturup sorgulayabilir ve tüm bunları yaparken Azure Cosmos DB'nin genel dağıtım ve yatay ölçeklendirme özelliklerinden faydalanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="daad3-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="daad3-106">Bu hızlı başlangıç belgesinde Azure portalı kullanarak bir Azure Cosmos DB hesabını, belge veritabanını ve koleksiyonunu nasıl oluşturacağınız anlatılmıştır.</span><span class="sxs-lookup"><span data-stu-id="daad3-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="daad3-107">Bu adımların ardından [MongoDB .NET sürücüsü](https://docs.mongodb.com/ecosystem/drivers/csharp/) üzerinde oluşturulan görev listesi web uygulaması derleyip dağıtacaksınız.</span><span class="sxs-lookup"><span data-stu-id="daad3-107">You'll then build and deploy a tasks list web app built on the [MongoDB .NET driver](https://docs.mongodb.com/ecosystem/drivers/csharp/).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="daad3-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="daad3-108">Prerequisites</span></span>

<span data-ttu-id="daad3-109">Henüz Visual Studio 2017’yi yüklemediyseniz, **ücretsiz** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/)’ı indirip kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="daad3-109">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="daad3-110">Visual Studio kurulumu sırasında **Azure dağıtımını** etkinleştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="daad3-110">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="daad3-111">Veritabanı hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="daad3-111">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="daad3-112">Örnek uygulamayı kopyalama</span><span class="sxs-lookup"><span data-stu-id="daad3-112">Clone the sample application</span></span>

<span data-ttu-id="daad3-113">Şimdi GitHub'dan bir MongoDB API'si uygulaması kopyalayalım, bağlantı dizesini ayarlayalım ve uygulamayı çalıştıralım.</span><span class="sxs-lookup"><span data-stu-id="daad3-113">Now let's clone a MongoDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="daad3-114">Verilerle programlı bir şekilde çalışmanın ne kadar kolay olduğunu göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="daad3-114">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="daad3-115">Git bash gibi bir git terminal penceresi açın ve `cd` ile çalışma dizinine gidin.</span><span class="sxs-lookup"><span data-stu-id="daad3-115">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="daad3-116">Örnek depoyu kopyalamak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="daad3-116">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-getting-started.git
    ```

3. <span data-ttu-id="daad3-117">Ardından çözüm dosyasını Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="daad3-117">Then open the solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="daad3-118">Kodu gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="daad3-118">Review the code</span></span>

<span data-ttu-id="daad3-119">Uygulamada gerçekleşen işlemleri hızlıca gözden geçirelim.</span><span class="sxs-lookup"><span data-stu-id="daad3-119">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="daad3-120">**DAL** dizini altındaki **Dal.cs** dosyasını açtığınızda Azure Cosmos DB kaynaklarını bu kod satırlarının oluşturduğunu göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="daad3-120">Open the **Dal.cs** file under the **DAL** directory and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="daad3-121">Mongo İstemcisini başlatın.</span><span class="sxs-lookup"><span data-stu-id="daad3-121">Initialize the Mongo Client.</span></span>

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

* <span data-ttu-id="daad3-122">Veritabanı ve koleksiyonu alın.</span><span class="sxs-lookup"><span data-stu-id="daad3-122">Retrieve the database and the collection.</span></span>

    ```cs
    private string dbName = "Tasks";
    private string collectionName = "TasksList";

    var database = client.GetDatabase(dbName);
    var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
    ```

* <span data-ttu-id="daad3-123">Tüm belgeleri alın.</span><span class="sxs-lookup"><span data-stu-id="daad3-123">Retrieve all documents.</span></span>

    ```cs
    collection.Find(new BsonDocument()).ToList();
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="daad3-124">Bağlantı dizenizi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="daad3-124">Update your connection string</span></span>

<span data-ttu-id="daad3-125">Bu adımda Azure portalına dönerek bağlantı dizesi bilgilerinizi kopyalayıp uygulamaya ekleyin.</span><span class="sxs-lookup"><span data-stu-id="daad3-125">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="daad3-126">[Azure portalında](http://portal.azure.com/), Azure Cosmos DB hesabınızın sol taraftaki gezinti menüsünden **Bağlantı Dizesi**'ne ve ardından **Okuma-Yazma Anahtarları**'na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="daad3-126">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Connection String**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="daad3-127">Sonraki adımda ekranın sağ tarafındaki kopyalama düğmelerini kullanarak Kullanıcı Adı, Parola ve Ana Bilgisayar değerlerini Dal.cs dosyasına kopyalayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="daad3-127">You'll use the copy buttons on the right side of the screen to copy the Username, Password, and Host into the Dal.cs file in the next step.</span></span>

2. <span data-ttu-id="daad3-128">**DAL** dizinindeki **Dal.cs** dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="daad3-128">Open the **Dal.cs** file in the **DAL** directory.</span></span> 

3. <span data-ttu-id="daad3-129">**userename** değerini portaldan kopyalayın (kopyalama düğmesini kullanarak) ve **Dal.cs** dosyasına **username** değeri olarak yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="daad3-129">Copy your **username** value from the portal (using the copy button) and make it the value of the **username** in your **Dal.cs** file.</span></span> 

4. <span data-ttu-id="daad3-130">Ardından **host** değerini portaldan kopyalayın ve **Dal.cs** dosyanıza **host** değeri olarak yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="daad3-130">Then copy your **host** value from the portal and make it the value of the **host** in your **Dal.cs** file.</span></span> 

5. <span data-ttu-id="daad3-131">Son olarak, **password** değerini portaldan kopyalayın ve **Dal.cs** dosyanıza **password** değeri olarak yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="daad3-131">Finally copy your **password** value from the portal and make it the value of the **password** in your **Dal.cs** file.</span></span> 

<span data-ttu-id="daad3-132">Bu adımlarla uygulamanıza Azure Cosmos DB ile iletişim kurması için gereken tüm bilgileri eklemiş oldunuz.</span><span class="sxs-lookup"><span data-stu-id="daad3-132">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-the-web-app"></a><span data-ttu-id="daad3-133">Web uygulamasını çalıştırma</span><span class="sxs-lookup"><span data-stu-id="daad3-133">Run the web app</span></span>

1. <span data-ttu-id="daad3-134">Visual Studio'nun **Çözüm Gezgini** bölümünde projeye sağ tıklayın ve ardından **NuGet Paketlerini Yönet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="daad3-134">In Visual Studio, right-click on the project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="daad3-135">NuGet **Gözat** kutusuna *MongoDB* yazın.</span><span class="sxs-lookup"><span data-stu-id="daad3-135">In the NuGet **Browse** box, type *MongoDB.Driver*.</span></span>

3. <span data-ttu-id="daad3-136">Sonuçlardan **MongoDB.Driver** kitaplığını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="daad3-136">From the results, install the **MongoDB.Driver** library.</span></span> <span data-ttu-id="daad3-137">Bunu yaptığınızda MongoDB.Driver paketi ve tüm bağımlılıklar yüklenir.</span><span class="sxs-lookup"><span data-stu-id="daad3-137">This installs the MongoDB.Driver package as well as all dependencies.</span></span>

4. <span data-ttu-id="daad3-138">Uygulamayı çalıştırmak için CTRL+F5 tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="daad3-138">Click CTRL + F5 to run the application.</span></span> <span data-ttu-id="daad3-139">Uygulamanız tarayıcınızda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="daad3-139">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="daad3-140">Tarayıcıda **Yeni** düğmesine tıklayın ve görev listesi uygulamanızda birkaç yeni görev oluşturun.</span><span class="sxs-lookup"><span data-stu-id="daad3-140">Click **Create** in the browser and create a few new tasks in your task list app.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="daad3-141">Azure portalında SLA'ları gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="daad3-141">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="daad3-142">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="daad3-142">Clean up resources</span></span>

<span data-ttu-id="daad3-143">Bu uygulamayı kullanmaya devam etmeyecekseniz aşağıdaki adımları kullanarak Azure portalında bu hızlı başlangıç tarafından oluşturulan tüm kaynakları silin:</span><span class="sxs-lookup"><span data-stu-id="daad3-143">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="daad3-144">Azure portalında sol taraftaki menüden, **Kaynak grupları**'na ve ardından oluşturduğunuz kaynağın adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="daad3-144">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="daad3-145">Kaynak grubu sayfanızda, **Sil**'e tıklayın, metin kutusuna silinecek kaynağın adını yazın ve ardından **Sil**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="daad3-145">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="daad3-146">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="daad3-146">Next steps</span></span>

<span data-ttu-id="daad3-147">Bu hızlı başlangıçta Azure Cosmos DB hesabı oluşturmayı ve MongoDB kullanarak bir web uygulamasını çalıştırmayı öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="daad3-147">In this quickstart, you've learned how to create an Azure Cosmos DB account and run a web app using the API for MongoDB.</span></span> <span data-ttu-id="daad3-148">Şimdi Cosmos DB hesabınıza ek veri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="daad3-148">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="daad3-149">MongoDB API'si için Azure Cosmos DB’ye veri aktarma</span><span class="sxs-lookup"><span data-stu-id="daad3-149">Import data into Azure Cosmos DB for the MongoDB API</span></span>](mongodb-migrate.md)

