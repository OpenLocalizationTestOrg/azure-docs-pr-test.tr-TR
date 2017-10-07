---
title: "Azure Cosmos DB: .NET ile bir web uygulaması oluşturma ve DocumentDB API hello | Microsoft Docs"
description: "Tooconnect tooand sorgu kullanabileceğiniz bir .NET kod örneği hello Azure Cosmos DB DocumentDB API sunar"
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
ms.openlocfilehash: 35517e35d80c48662a51a99814652ffa1121fc5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-web-app-with-net-and-hello-azure-portal"></a><span data-ttu-id="bd3e1-103">Azure Cosmos DB: .NET ile DocumentDB API web uygulaması oluşturma ve Azure portal hello</span><span class="sxs-lookup"><span data-stu-id="bd3e1-103">Azure Cosmos DB: Build a DocumentDB API web app with .NET and hello Azure portal</span></span>

<span data-ttu-id="bd3e1-104">Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="bd3e1-105">Hızlı bir şekilde oluşturmak ve belge, anahtar/değer ve grafik veritabanları, her biri hello genel dağıtım ve yatay ölçek özelliklerini Azure Cosmos DB'nin hello çekirdek yararlı sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="bd3e1-106">Bu hızlı başlangıç nasıl toocreate Azure Cosmos DB hesabınız, belge veritabanı ve koleksiyonu kullanarak Azure portalında hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="bd3e1-107">Daha sonra yapı ve hello üzerinde oluşturulmuş bir Yapılacaklar listesi web uygulaması dağıtma [DocumentDB .NET API](documentdb-sdk-dotnet.md)hello ekran aşağıdaki gösterildiği gibi.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-107">You'll then build and deploy a todo list web app built on hello [DocumentDB .NET API](documentdb-sdk-dotnet.md), as shown in hello following screenshot.</span></span> 

![Yapılacaklar listesi uygulaması ve örnek veriler](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

## <a name="prerequisites"></a><span data-ttu-id="bd3e1-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="bd3e1-109">Prerequisites</span></span>

<span data-ttu-id="bd3e1-110">Visual Studio yüklü 2017 zaten sahip değilseniz, indirin ve hello kullan **ücretsiz** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="bd3e1-110">If you don’t already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="bd3e1-111">Etkinleştirdiğinizden emin olun **Azure geliştirme** hello Visual Studio Kurulumu sırasında.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-111">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="bd3e1-112">Veritabanı hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="bd3e1-112">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<a id="create-collection"></a>
## <a name="add-a-collection"></a><span data-ttu-id="bd3e1-113">Koleksiyon ekleme</span><span class="sxs-lookup"><span data-stu-id="bd3e1-113">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="bd3e1-114">Örnek verileri ekleme</span><span class="sxs-lookup"><span data-stu-id="bd3e1-114">Add sample data</span></span>

<span data-ttu-id="bd3e1-115">Veri Gezgini'ni kullanarak veri tooyour yeni bir koleksiyon artık ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-115">You can now add data tooyour new collection using Data Explorer.</span></span>

1. <span data-ttu-id="bd3e1-116">Veri Gezgini'nde hello yeni veritabanı hello Koleksiyonlar bölmesinde görünür.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-116">In Data Explorer, hello new database appears in hello Collections pane.</span></span> <span data-ttu-id="bd3e1-117">Merhaba genişletin **görevleri** veritabanı, hello Genişlet **öğeleri** koleksiyonu tıklatın **belgeleri**ve ardından **yeni belgeler**.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-117">Expand hello **Tasks** database, expand hello **Items** collection, click **Documents**, and then click **New Documents**.</span></span> 

   ![Yeni belgeler veri Gezgini'nde hello Azure portal oluşturun.](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. <span data-ttu-id="bd3e1-119">Şimdi bir belge toohello Koleksiyonu Yapı izlenerek hello ile ekleyin.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-119">Now add a document toohello collection with hello following structure.</span></span>

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. <span data-ttu-id="bd3e1-120">Merhaba json toohello ekledikten sonra **belgeleri** sekmesini tıklatın, **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-120">Once you've added hello json toohello **Documents** tab, click **Save**.</span></span>

    ![JSON verileri kopyalayın ve Veri Gezgini'nde hello Azure portal Kaydet](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  <span data-ttu-id="bd3e1-122">Oluştur ve Ekle burada hello için benzersiz bir değer bir daha fazla belgeyi kaydedin `id` özelliği ve diğer özellikleri uygun gördüğünüz şekilde hello Değiştir.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-122">Create and save one more document where you insert a unique value for hello `id` property, and change hello other properties as you see fit.</span></span> <span data-ttu-id="bd3e1-123">Azure Cosmos DB, verilerinizin bir şemaya uygun olmasını şart koşmadığı için yeni belgelerinizin yapısını istediğiniz şekilde oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-123">Your new documents can have any structure you want as Azure Cosmos DB doesn't impose any schema on your data.</span></span>

     <span data-ttu-id="bd3e1-124">Artık, verilerinizi Veri Gezgini tooretrieve sorgularda kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-124">You can now use queries in Data Explorer tooretrieve your data.</span></span> <span data-ttu-id="bd3e1-125">Varsayılan olarak, Veri Gezgini kullanır `SELECT * FROM c` tooretrieve tüm belgeleri hello koleksiyonu, ancak siz o tooa farklı değiştirebilirsiniz [SQL sorgusu](documentdb-sql-query.md), gibi `SELECT * FROM c ORDER BY c._ts DESC`, azalan sırada tüm hello belgeleri temel alarak tooreturn kendi zaman damgası.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-125">By default, Data Explorer uses `SELECT * FROM c` tooretrieve all documents in hello collection, but you can change that tooa different [SQL query](documentdb-sql-query.md), such as `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn all hello documents in descending order based on their timestamp.</span></span>
 
     <span data-ttu-id="bd3e1-126">Ayrıca Veri Gezgini toocreate saklı yordamlar, UDF'ler ve Tetikleyicileri tooperform sunucu tarafı iş mantığı da kullanabilirsiniz ölçek işleme olarak.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-126">You can also use Data Explorer toocreate stored procedures, UDFs, and triggers tooperform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="bd3e1-127">Veri Gezgini tüm hello yerleşik programlı veri erişim hello API'leri kullanılabilir gösterir, ancak tooyour verileri hello Azure portalında kolay erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-127">Data Explorer exposes all of hello built-in programmatic data access available in hello APIs, but provides easy access tooyour data in hello Azure portal.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="bd3e1-128">Merhaba örnek uygulaması kopyalama</span><span class="sxs-lookup"><span data-stu-id="bd3e1-128">Clone hello sample application</span></span>

<span data-ttu-id="bd3e1-129">Şimdi şimdi koduyla tooworking geçin.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-129">Now let's switch tooworking with code.</span></span> <span data-ttu-id="bd3e1-130">Şimdi DocumentDB API uygulaması github'dan hello bağlantı dizesini ayarlamak ve çalıştırın kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-130">Let's clone a DocumentDB API app from GitHub, set hello connection string, and run it.</span></span> <span data-ttu-id="bd3e1-131">Ne kadar kolay toowork verilerle program aracılığıyla olduğunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-131">You'll see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="bd3e1-132">Git bash gibi bir git terminal penceresi açın ve `CD` tooa çalışma dizini.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-132">Open a git terminal window, such as git bash, and `CD` tooa working directory.</span></span>  

2. <span data-ttu-id="bd3e1-133">Çalışma hello aşağıdaki tooclone hello örnek depo komutu.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-133">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/documentdb-dotnet-todo-app.git
    ```

3. <span data-ttu-id="bd3e1-134">Ardından Visual Studio'da hello Yapılacaklar çözüm dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-134">Then open hello todo solution file in Visual Studio.</span></span> 

## <a name="review-hello-code"></a><span data-ttu-id="bd3e1-135">Merhaba kod gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="bd3e1-135">Review hello code</span></span>

<span data-ttu-id="bd3e1-136">Neler olduğuna dair hello uygulamada hızlı bir gözden geçirme olalım.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-136">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="bd3e1-137">Açık hello DocumentDBRepository.cs dosyanız varsa ve bu kod satırları hello Azure Cosmos DB kaynakları oluşturma bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-137">Open hello DocumentDBRepository.cs file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="bd3e1-138">Merhaba DocumentClient 73 satırda başlatılır.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-138">hello DocumentClient is initialized on line 73.</span></span>

    ```csharp
    client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);`
    ```

* <span data-ttu-id="bd3e1-139">88 satırda yeni bir veritabanı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-139">A new database is created on line 88.</span></span>

    ```csharp
    await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
    ```

* <span data-ttu-id="bd3e1-140">107 satırda yeni bir koleksiyon oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-140">A new collection is created on line 107.</span></span>

    ```csharp
    await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(DatabaseId),
        new DocumentCollection { Id = CollectionId },
        new RequestOptions { OfferThroughput = 1000 });
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="bd3e1-141">Bağlantı dizenizi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="bd3e1-141">Update your connection string</span></span>

<span data-ttu-id="bd3e1-142">Şimdi Azure portal tooget toohello bağlantı dizesi bilgilerinizi geri dönün ve hello uygulamaya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-142">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="bd3e1-143">Merhaba, [Azure portal](http://portal.azure.com/), Azure Cosmos DB hesap, sol gezinti hello tıklatın **anahtarları**ve ardından **okuma-yazma anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-143">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="bd3e1-144">Merhaba sonraki adımda hello web.config dosyasına hello Kopyala düğmesi hello sağ tarafında Merhaba ekranında toocopy hello URI ve birincil anahtar kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-144">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello web.config file in hello next step.</span></span>

    ![Görüntüleme ve kopyalama hello Azure portalına erişim tuşu, anahtarlar dikey penceresinde](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="bd3e1-146">Visual Studio 2017 içinde hello web.config dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-146">In Visual Studio 2017, open hello web.config file.</span></span> 

3. <span data-ttu-id="bd3e1-147">URI değeri (Merhaba Kopyala düğmesini kullanarak) hello Portal'dan kopyalayın ve hale hello web.config dosyasında hello uç nokta anahtar değeri.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-147">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint key in web.config.</span></span> 

    `<add key="endpoint" value="FILLME" />`

4. <span data-ttu-id="bd3e1-148">Sonra birincil anahtar değer hello Portal'dan kopyalayın ve kolaylaştırır hello hello authKey web.config dosyasındaki değeri. Uygulamanızı şimdi güncelleştirdikten toocommunicate Azure Cosmos DB ile gerekli tüm hello bilgilerine sahip.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-148">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello authKey in web.config. You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

    `<add key="authKey" value="FILLME" />`
    
## <a name="run-hello-web-app"></a><span data-ttu-id="bd3e1-149">Merhaba web uygulaması çalıştırın</span><span class="sxs-lookup"><span data-stu-id="bd3e1-149">Run hello web app</span></span>
1. <span data-ttu-id="bd3e1-150">Visual Studio'da hello projeye sağ tıklayın **Çözüm Gezgini** ve ardından **NuGet paketlerini Yönet**.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-150">In Visual Studio, right-click on hello project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="bd3e1-151">Merhaba NuGet içinde **Gözat** kutusuna *DocumentDB*.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-151">In hello NuGet **Browse** box, type *DocumentDB*.</span></span>

3. <span data-ttu-id="bd3e1-152">Merhaba sonuçlarından hello yüklemek **Microsoft.Azure.DocumentDB** kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-152">From hello results, install hello **Microsoft.Azure.DocumentDB** library.</span></span> <span data-ttu-id="bd3e1-153">Bu, tüm bağımlılıkları yanı sıra hello Microsoft.Azure.DocumentDB paketi yükler.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-153">This installs hello Microsoft.Azure.DocumentDB package as well as all dependencies.</span></span>

4. <span data-ttu-id="bd3e1-154">CTRL + F5'e tıklayın toorun Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-154">Click CTRL + F5 toorun hello application.</span></span> <span data-ttu-id="bd3e1-155">Uygulamanız tarayıcınızda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-155">Your app displays in your browser.</span></span> 

5. <span data-ttu-id="bd3e1-156">Tıklatın **Yeni Oluştur** hello tarayıcı ve yapılacaklar uygulamanızda birkaç yeni görevler oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-156">Click **Create New** in hello browser and create a few new tasks in your to-do app.</span></span>

   ![Yapılacaklar listesi uygulaması ve örnek veriler](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

<span data-ttu-id="bd3e1-158">Şimdi tooData Explorer geri dönün ve sorgu görmek değiştirmek ve bu yeni verilerle çalışmak.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-158">You can now go back tooData Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="bd3e1-159">Gözden geçirme SLA'hello Azure portalı</span><span class="sxs-lookup"><span data-stu-id="bd3e1-159">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="bd3e1-160">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="bd3e1-160">Clean up resources</span></span>

<span data-ttu-id="bd3e1-161">Toocontinue toouse bu uygulamayı değil kullanacaksanız, bu hızlı başlangıç tarafından hello Azure portalında aşağıdaki adımları hello ile oluşturulan tüm kaynakları silin:</span><span class="sxs-lookup"><span data-stu-id="bd3e1-161">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="bd3e1-162">Merhaba sol taraftaki menüden hello Azure portal'ın, **kaynak grupları** ve ardından oluşturduğunuz hello kaynak hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-162">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="bd3e1-163">Kaynak grubu sayfanızda tıklatın **silmek**hello metin kutusuna hello kaynak toodelete hello adını yazın ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-163">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bd3e1-164">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bd3e1-164">Next steps</span></span>

<span data-ttu-id="bd3e1-165">Bu hızlı başlangıç toocreate bir Azure Cosmos DB hesap hello Veri Gezgini'ni kullanarak bir koleksiyon oluşturma ve bir web uygulamasını çalıştırmak öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-165">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run a web app.</span></span> <span data-ttu-id="bd3e1-166">Artık ek verileri tooyour Cosmos DB hesap içeri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd3e1-166">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="bd3e1-167">Azure Cosmos DB hesabınıza veri aktarma</span><span class="sxs-lookup"><span data-stu-id="bd3e1-167">Import data into Azure Cosmos DB</span></span>](import-data.md)


