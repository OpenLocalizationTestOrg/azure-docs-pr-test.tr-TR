---
title: "Azure Cosmos DB: .NET ve DocumentDB API'si ile bir web uygulaması derleme | Microsoft Docs"
description: "Azure Cosmos DB DocumentDB API'sine bağlanmak ve sorgu göndermek için kullanabileceğiniz bir .NET kodu örneği sunar"
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
ms.openlocfilehash: 9bb863261da64c97f99757d4a0cb3474a7755591
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-web-app-with-net-and-the-azure-portal"></a><span data-ttu-id="353ad-103">Azure Cosmos DB: .NET ve Azure portalı ile bir DocumentDB API web uygulaması derleme</span><span class="sxs-lookup"><span data-stu-id="353ad-103">Azure Cosmos DB: Build a DocumentDB API web app with .NET and the Azure portal</span></span>

<span data-ttu-id="353ad-104">Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="353ad-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="353ad-105">Bu hizmetle belge, anahtar/değer ve grafik veritabanlarını kolayca oluşturup sorgulayabilir ve tüm bunları yaparken Azure Cosmos DB'nin genel dağıtım ve yatay ölçeklendirme özelliklerinden faydalanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="353ad-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="353ad-106">Bu hızlı başlangıç belgesinde Azure portalı kullanarak bir Azure Cosmos DB hesabını, belge veritabanını ve koleksiyonunu nasıl oluşturacağınız anlatılmıştır.</span><span class="sxs-lookup"><span data-stu-id="353ad-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="353ad-107">Bu işlemlerin ardından aşağıdaki ekran görüntüsünde gösterilen şekilde [DocumentDB .NET API'si](documentdb-sdk-dotnet.md) üzerinde bir yapılacaklar listesi web uygulaması derleyecek ve dağıtacaksınız.</span><span class="sxs-lookup"><span data-stu-id="353ad-107">You'll then build and deploy a todo list web app built on the [DocumentDB .NET API](documentdb-sdk-dotnet.md), as shown in the following screenshot.</span></span> 

![Yapılacaklar listesi uygulaması ve örnek veriler](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

## <a name="prerequisites"></a><span data-ttu-id="353ad-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="353ad-109">Prerequisites</span></span>

<span data-ttu-id="353ad-110">Henüz Visual Studio 2017’yi yüklemediyseniz, **ücretsiz** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/)’ı indirip kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="353ad-110">If you don’t already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="353ad-111">Visual Studio kurulumu sırasında **Azure dağıtımını** etkinleştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="353ad-111">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="353ad-112">Veritabanı hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="353ad-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<a id="create-collection"></a>
## <a name="add-a-collection"></a><span data-ttu-id="353ad-113">Koleksiyon ekleme</span><span class="sxs-lookup"><span data-stu-id="353ad-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="353ad-114">Örnek verileri ekleme</span><span class="sxs-lookup"><span data-stu-id="353ad-114">Add sample data</span></span>

<span data-ttu-id="353ad-115">Şimdi Veri Gezgini'ni kullanarak yeni koleksiyonunuza veri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="353ad-115">You can now add data to your new collection using Data Explorer.</span></span>

1. <span data-ttu-id="353ad-116">Yeni veritabanı, Veri Gezgini'nin Koleksiyonlar bölmesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="353ad-116">In Data Explorer, the new database appears in the Collections pane.</span></span> <span data-ttu-id="353ad-117">**Görevler** veritabanını genişletin, **Öğeler** koleksiyonunu genişletin, **Belgeler**'e ve ardından **Yeni Belge**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="353ad-117">Expand the **Tasks** database, expand the **Items** collection, click **Documents**, and then click **New Documents**.</span></span> 

   ![Azure portalındaki Veri Gezgini'nde yeni belge oluşturma](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. <span data-ttu-id="353ad-119">Şimdi koleksiyona aşağıdaki yapıya sahip bir belge ekleyin.</span><span class="sxs-lookup"><span data-stu-id="353ad-119">Now add a document to the collection with the following structure.</span></span>

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. <span data-ttu-id="353ad-120">JSON öğesini **Belgeler** sekmesine ekledikten sonra **Kaydet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="353ad-120">Once you've added the json to the **Documents** tab, click **Save**.</span></span>

    ![Azure portalında JSON verilerini kopyalayın ve Veri Gezgini'ne kaydedin](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  <span data-ttu-id="353ad-122">`id` özelliği için benzersiz bir değer eklediğiniz yerde bir veya daha fazla belge oluşturun ve kaydedin ve diğer özellikleri uygun şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="353ad-122">Create and save one more document where you insert a unique value for the `id` property, and change the other properties as you see fit.</span></span> <span data-ttu-id="353ad-123">Azure Cosmos DB, verilerinizin bir şemaya uygun olmasını şart koşmadığı için yeni belgelerinizin yapısını istediğiniz şekilde oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="353ad-123">Your new documents can have any structure you want as Azure Cosmos DB doesn't impose any schema on your data.</span></span>

     <span data-ttu-id="353ad-124">Şimdi verilerinizi almak için Veri Gezgini'ndeki sorguları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="353ad-124">You can now use queries in Data Explorer to retrieve your data.</span></span> <span data-ttu-id="353ad-125">Veri Gezgini koleksiyondaki tüm belgeleri almak için varsayılan olarak `SELECT * FROM c` komutunu kullanır ancak bunu `SELECT * FROM c ORDER BY c._ts DESC` gibi farklı bir [SQL sorgusuyla](documentdb-sql-query.md) değiştirerek tüm belgelerin zaman damgasına göre azalan sırada döndürülmesini sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="353ad-125">By default, Data Explorer uses `SELECT * FROM c` to retrieve all documents in the collection, but you can change that to a different [SQL query](documentdb-sql-query.md), such as `SELECT * FROM c ORDER BY c._ts DESC`, to return all the documents in descending order based on their timestamp.</span></span>
 
     <span data-ttu-id="353ad-126">Veri Gezgini'ni kullanarak ayrıca saklı yordamlar, UDF'ler ve tetikleyiciler oluşturabilir, bu sayede sunucu tarafı iş mantığını gerçekleştirebilir ve aktarım hızını ölçeklendirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="353ad-126">You can also use Data Explorer to create stored procedures, UDFs, and triggers to perform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="353ad-127">Veri Gezgini, API'lerdeki tüm yerleşik programlı veri erişimini açığa çıkarır ancak Azure portalındaki verilerinize kolayca erişmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="353ad-127">Data Explorer exposes all of the built-in programmatic data access available in the APIs, but provides easy access to your data in the Azure portal.</span></span>

## <a name="clone-the-sample-application"></a><span data-ttu-id="353ad-128">Örnek uygulamayı kopyalama</span><span class="sxs-lookup"><span data-stu-id="353ad-128">Clone the sample application</span></span>

<span data-ttu-id="353ad-129">Şimdi kod ile çalışmaya geçelim.</span><span class="sxs-lookup"><span data-stu-id="353ad-129">Now let's switch to working with code.</span></span> <span data-ttu-id="353ad-130">GitHub'dan bir DocumentDB API uygulaması kopyalayalım, bağlantı dizesini ayarlayalım ve uygulamayı çalıştıralım.</span><span class="sxs-lookup"><span data-stu-id="353ad-130">Let's clone a DocumentDB API app from GitHub, set the connection string, and run it.</span></span> <span data-ttu-id="353ad-131">Verilerle programlı bir şekilde çalışmanın ne kadar kolay olduğunu göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="353ad-131">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="353ad-132">Git bash gibi bir git terminal penceresi açın ve `CD` ile çalışma dizinine gidin.</span><span class="sxs-lookup"><span data-stu-id="353ad-132">Open a git terminal window, such as git bash, and `CD` to a working directory.</span></span>  

2. <span data-ttu-id="353ad-133">Örnek depoyu kopyalamak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="353ad-133">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/documentdb-dotnet-todo-app.git
    ```

3. <span data-ttu-id="353ad-134">Ardından Visual Studio'daki TODO çözüm dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="353ad-134">Then open the todo solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="353ad-135">Kodu gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="353ad-135">Review the code</span></span>

<span data-ttu-id="353ad-136">Uygulamada gerçekleşen işlemleri hızlıca gözden geçirelim.</span><span class="sxs-lookup"><span data-stu-id="353ad-136">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="353ad-137">DocumentDBRepository.cs dosyasını açtığınızda Azure Cosmos DB kaynaklarını bu kod satırlarının oluşturduğunu göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="353ad-137">Open the DocumentDBRepository.cs file and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="353ad-138">73 satırda DocumentClient başlatılır.</span><span class="sxs-lookup"><span data-stu-id="353ad-138">The DocumentClient is initialized on line 73.</span></span>

    ```csharp
    client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);`
    ```

* <span data-ttu-id="353ad-139">88 satırda yeni bir veritabanı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="353ad-139">A new database is created on line 88.</span></span>

    ```csharp
    await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
    ```

* <span data-ttu-id="353ad-140">107 satırda yeni bir koleksiyon oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="353ad-140">A new collection is created on line 107.</span></span>

    ```csharp
    await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(DatabaseId),
        new DocumentCollection { Id = CollectionId },
        new RequestOptions { OfferThroughput = 1000 });
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="353ad-141">Bağlantı dizenizi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="353ad-141">Update your connection string</span></span>

<span data-ttu-id="353ad-142">Bu adımda Azure portalına dönerek bağlantı dizesi bilgilerinizi kopyalayıp uygulamaya ekleyin.</span><span class="sxs-lookup"><span data-stu-id="353ad-142">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="353ad-143">[Azure portalında](http://portal.azure.com/), Azure Cosmos DB hesabınızın sol taraftaki gezinti menüsünden **Anahtarlar**'a ve ardından **Okuma/Yazma Anahtarları**'na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="353ad-143">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="353ad-144">Ekranın sağ tarafındaki kopyalama düğmelerini kullanarak URI ve Birincil Anahtar değerlerini kopyalayarak sonraki adımda web.config dosyasına yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="353ad-144">You'll use the copy buttons on the right side of the screen to copy the URI and Primary Key into the web.config file in the next step.</span></span>

    ![Azure portalında erişim anahtarı görüntüleme ve kopyalama, Anahtarlar dikey penceresi](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="353ad-146">Visual Studio 2017'de web.config dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="353ad-146">In Visual Studio 2017, open the web.config file.</span></span> 

3. <span data-ttu-id="353ad-147">Portaldaki URI değerinizi kopyalayın (kopyalama düğmesini kullanarak) ve web.config dosyasına uç nokta değeri olarak yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="353ad-147">Copy your URI value from the portal (using the copy button) and make it the value of the endpoint key in web.config.</span></span> 

    `<add key="endpoint" value="FILLME" />`

4. <span data-ttu-id="353ad-148">Ardından portaldaki BİRİNCİL ANAHTAR değerinizi kopyalayıp web.config dosyasına authKey değeri olarak yapıştırın. Bu adımlarla uygulamanıza Azure Cosmos DB ile iletişim kurması için gereken tüm bilgileri eklemiş oldunuz.</span><span class="sxs-lookup"><span data-stu-id="353ad-148">Then copy your PRIMARY KEY value from the portal and make it the value of the authKey in web.config. You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

    `<add key="authKey" value="FILLME" />`
    
## <a name="run-the-web-app"></a><span data-ttu-id="353ad-149">Web uygulamasını çalıştırma</span><span class="sxs-lookup"><span data-stu-id="353ad-149">Run the web app</span></span>
1. <span data-ttu-id="353ad-150">Visual Studio'nun **Çözüm Gezgini** bölümünde projeye sağ tıklayın ve ardından **NuGet Paketlerini Yönet**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="353ad-150">In Visual Studio, right-click on the project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="353ad-151">NuGet **Gözat** kutusuna *DocumentDB* yazın.</span><span class="sxs-lookup"><span data-stu-id="353ad-151">In the NuGet **Browse** box, type *DocumentDB*.</span></span>

3. <span data-ttu-id="353ad-152">Sonuçlardan **Microsoft.Azure.DocumentDB** kitaplığını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="353ad-152">From the results, install the **Microsoft.Azure.DocumentDB** library.</span></span> <span data-ttu-id="353ad-153">Bunu yaptığınızda Microsoft.Azure.DocumentDB paketi ve tüm bağımlılıklar yüklenir.</span><span class="sxs-lookup"><span data-stu-id="353ad-153">This installs the Microsoft.Azure.DocumentDB package as well as all dependencies.</span></span>

4. <span data-ttu-id="353ad-154">Uygulamayı çalıştırmak için CTRL+F5 tuşlarına basın.</span><span class="sxs-lookup"><span data-stu-id="353ad-154">Click CTRL + F5 to run the application.</span></span> <span data-ttu-id="353ad-155">Uygulamanız tarayıcınızda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="353ad-155">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="353ad-156">Tarayıcıda **Create New** (Yeni Oluştur) düğmesine tıklayın ve yapılacaklar listesi uygulamanızda birkaç yeni görev oluşturun.</span><span class="sxs-lookup"><span data-stu-id="353ad-156">Click **Create New** in the browser and create a few new tasks in your to-do app.</span></span>

   ![Yapılacaklar listesi uygulaması ve örnek veriler](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

<span data-ttu-id="353ad-158">Şimdi Veri Gezgini'ne dönüp bu yeni verileri görebilir, sorgulayabilir, değiştirebilir ve onlarla çalışabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="353ad-158">You can now go back to Data Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="353ad-159">Azure portalında SLA'ları gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="353ad-159">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="353ad-160">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="353ad-160">Clean up resources</span></span>

<span data-ttu-id="353ad-161">Bu uygulamayı kullanmaya devam etmeyecekseniz aşağıdaki adımları kullanarak Azure portalında bu hızlı başlangıç tarafından oluşturulan tüm kaynakları silin:</span><span class="sxs-lookup"><span data-stu-id="353ad-161">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="353ad-162">Azure portalında sol taraftaki menüden, **Kaynak grupları**'na ve ardından oluşturduğunuz kaynağın adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="353ad-162">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="353ad-163">Kaynak grubu sayfanızda, **Sil**'e tıklayın, metin kutusuna silinecek kaynağın adını yazın ve ardından **Sil**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="353ad-163">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="353ad-164">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="353ad-164">Next steps</span></span>

<span data-ttu-id="353ad-165">Bu hızlı başlangıçta Azure Cosmos DB hesabı oluşturmayı, Veri Gezgini'ni kullanarak koleksiyon oluşturmayı ve bir web uygulamasını çalıştırmayı öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="353ad-165">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run a web app.</span></span> <span data-ttu-id="353ad-166">Şimdi Cosmos DB hesabınıza ek veri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="353ad-166">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="353ad-167">Azure Cosmos DB hesabınıza veri aktarma</span><span class="sxs-lookup"><span data-stu-id="353ad-167">Import data into Azure Cosmos DB</span></span>](import-data.md)


