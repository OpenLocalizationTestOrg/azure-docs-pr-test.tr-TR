---
title: "aaaCreate bir Java ile Azure Cosmos DB belge veritabanı | Microsoft Docs | Microsoft Docs"
description: "Tooconnect tooand sorgu kullanabileceğiniz bir Java kod örneği hello Azure Cosmos DB DocumentDB API sunar"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 89ea62bb-c620-46d5-baa0-eefd9888557c
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: hero-article
ms.date: 08/02/2017
ms.author: mimig
ms.openlocfilehash: 400c9e7780034d3e28d749e734786e950edad22f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-create-a-document-database-using-java-and-hello-azure-portal"></a><span data-ttu-id="59dc0-103">Azure Cosmos DB: Java kullanarak bir belge veritabanı oluşturmak ve Azure portal hello</span><span class="sxs-lookup"><span data-stu-id="59dc0-103">Azure Cosmos DB: Create a document database using Java and hello Azure portal</span></span>

<span data-ttu-id="59dc0-104">Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="59dc0-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="59dc0-105">Hızlı bir şekilde oluşturmak ve belge, anahtar/değer ve grafik veritabanları, her biri hello genel dağıtım ve yatay ölçek özelliklerini Azure Cosmos DB'nin hello çekirdek yararlı sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59dc0-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="59dc0-106">Bu hızlı başlangıç bir belge oluşturur Azure Cosmos DB hello Azure portal araçları veritabanını kullanma.</span><span class="sxs-lookup"><span data-stu-id="59dc0-106">This quickstart creates a document database using hello Azure portal tools for Azure Cosmos DB.</span></span> <span data-ttu-id="59dc0-107">Bu hızlı başlangıç ayrıca tooquickly hello kullanarak bir Java konsol uygulaması oluşturma nasıl gösterilmektedir [DocumentDB Java API](documentdb-sdk-java.md).</span><span class="sxs-lookup"><span data-stu-id="59dc0-107">This quickstart also shows you how tooquickly create a Java console app using hello [DocumentDB Java API](documentdb-sdk-java.md).</span></span> <span data-ttu-id="59dc0-108">Bu hızlı başlangıç içinde Hello yönergeler Java çalıştırabilen tüm işletim sisteminde izlenebilir.</span><span class="sxs-lookup"><span data-stu-id="59dc0-108">hello instructions in this quickstart can be followed on any operating system that is capable of running Java.</span></span> <span data-ttu-id="59dc0-109">Bu hızlı başlangıç tamamlayarak oluşturma ve belge veritabanı kaynaklarında hello UI ya da programlı şekilde, tercihinize hangisi değiştirme hakkında bilgi sahibi olması.</span><span class="sxs-lookup"><span data-stu-id="59dc0-109">By completing this quickstart you'll be familiar with creating and modifying document database resources in either hello UI or programatically, whichever is your preference.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59dc0-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="59dc0-110">Prerequisites</span></span>

* [<span data-ttu-id="59dc0-111">Java Development Kit (JDK) 1.7+</span><span class="sxs-lookup"><span data-stu-id="59dc0-111">Java Development Kit (JDK) 1.7+</span></span>](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * <span data-ttu-id="59dc0-112">Ubuntu üzerinde çalıştırmak `apt-get install default-jdk` tooinstall hello JDK.</span><span class="sxs-lookup"><span data-stu-id="59dc0-112">On Ubuntu, run `apt-get install default-jdk` tooinstall hello JDK.</span></span>
    * <span data-ttu-id="59dc0-113">Emin tooset hello JAVA_HOME ortam değişkeni toopoint toohello klasörü hello JDK'ın yüklendiği olabilir.</span><span class="sxs-lookup"><span data-stu-id="59dc0-113">Be sure tooset hello JAVA_HOME environment variable toopoint toohello folder where hello JDK is installed.</span></span>
* <span data-ttu-id="59dc0-114">Bir [Maven](http://maven.apache.org/) ikili arşivi [indirin](http://maven.apache.org/download.cgi) ve [yükleyin](http://maven.apache.org/install.html)</span><span class="sxs-lookup"><span data-stu-id="59dc0-114">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a [Maven](http://maven.apache.org/) binary archive</span></span>
    * <span data-ttu-id="59dc0-115">Ubuntu üzerinde çalıştırdığınız `apt-get install maven` tooinstall Maven.</span><span class="sxs-lookup"><span data-stu-id="59dc0-115">On Ubuntu, you can run `apt-get install maven` tooinstall Maven.</span></span>
* [<span data-ttu-id="59dc0-116">Git</span><span class="sxs-lookup"><span data-stu-id="59dc0-116">Git</span></span>](https://www.git-scm.com/)
    * <span data-ttu-id="59dc0-117">Ubuntu üzerinde çalıştırdığınız `sudo apt-get install git` tooinstall Git.</span><span class="sxs-lookup"><span data-stu-id="59dc0-117">On Ubuntu, you can run `sudo apt-get install git` tooinstall Git.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="59dc0-118">Veritabanı hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="59dc0-118">Create a database account</span></span>

<span data-ttu-id="59dc0-119">Bir belge veritabanı oluşturabilmeniz için önce toocreate Azure Cosmos DB ile (DocumentDB) SQL veritabanı hesabı gerekir.</span><span class="sxs-lookup"><span data-stu-id="59dc0-119">Before you can create a document database, you need toocreate a SQL (DocumentDB) database account with Azure Cosmos DB.</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="59dc0-120">Koleksiyon ekleme</span><span class="sxs-lookup"><span data-stu-id="59dc0-120">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a><span data-ttu-id="59dc0-121">Örnek verileri ekleme</span><span class="sxs-lookup"><span data-stu-id="59dc0-121">Add sample data</span></span>

<span data-ttu-id="59dc0-122">Veri Gezgini'ni kullanarak veri tooyour yeni bir koleksiyon artık ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59dc0-122">You can now add data tooyour new collection using Data Explorer.</span></span>

1. <span data-ttu-id="59dc0-123">Veri Gezgini'nde hello yeni veritabanı hello Koleksiyonlar bölmesinde görünür.</span><span class="sxs-lookup"><span data-stu-id="59dc0-123">In Data Explorer, hello new database appears in hello Collections pane.</span></span> <span data-ttu-id="59dc0-124">Merhaba genişletin **görevleri** veritabanı, hello Genişlet **öğeleri** koleksiyonu tıklatın **belgeleri**ve ardından **yeni belgeler**.</span><span class="sxs-lookup"><span data-stu-id="59dc0-124">Expand hello **Tasks** database, expand hello **Items** collection, click **Documents**, and then click **New Documents**.</span></span> 

   ![Yeni belgeler veri Gezgini'nde hello Azure portal oluşturun.](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. <span data-ttu-id="59dc0-126">Şimdi bir belge toohello Koleksiyonu Yapı izlenerek hello ile ekleyin.</span><span class="sxs-lookup"><span data-stu-id="59dc0-126">Now add a document toohello collection with hello following structure.</span></span>

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. <span data-ttu-id="59dc0-127">Merhaba json toohello ekledikten sonra **belgeleri** sekmesini tıklatın, **kaydetmek**.</span><span class="sxs-lookup"><span data-stu-id="59dc0-127">Once you've added hello json toohello **Documents** tab, click **Save**.</span></span>

    ![JSON verileri kopyalayın ve Veri Gezgini'nde hello Azure portal Kaydet](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  <span data-ttu-id="59dc0-129">Oluştur ve Ekle burada hello için benzersiz bir değer bir daha fazla belgeyi kaydedin `id` özelliği ve diğer özellikleri uygun gördüğünüz şekilde hello Değiştir.</span><span class="sxs-lookup"><span data-stu-id="59dc0-129">Create and save one more document where you insert a unique value for hello `id` property, and change hello other properties as you see fit.</span></span> <span data-ttu-id="59dc0-130">Azure Cosmos DB, verilerinizin bir şemaya uygun olmasını şart koşmadığı için yeni belgelerinizin yapısını istediğiniz şekilde oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59dc0-130">Your new documents can have any structure you want as Azure Cosmos DB doesn't impose any schema on your data.</span></span>

     <span data-ttu-id="59dc0-131">Veri Gezgini tooretrieve verilerinizi hello tıklayarak Sorguların kullandığı artık yapabilecekleriniz **filtresi Düzenle** ve **Filtre Uygula** düğmeler.</span><span class="sxs-lookup"><span data-stu-id="59dc0-131">You can now use queries in Data Explorer tooretrieve your data by clicking hello **Edit Filter** and **Apply Filter** buttons.</span></span> <span data-ttu-id="59dc0-132">Varsayılan olarak, Veri Gezgini kullanır `SELECT * FROM c` tooretrieve tüm belgeleri hello koleksiyonu, ancak siz o tooa farklı değiştirebilirsiniz [SQL sorgusu](documentdb-sql-query.md), gibi `SELECT * FROM c ORDER BY c._ts DESC`, azalan sırada tüm hello belgeleri temel alarak tooreturn kendi zaman damgası.</span><span class="sxs-lookup"><span data-stu-id="59dc0-132">By default, Data Explorer uses `SELECT * FROM c` tooretrieve all documents in hello collection, but you can change that tooa different [SQL query](documentdb-sql-query.md), such as `SELECT * FROM c ORDER BY c._ts DESC`, tooreturn all hello documents in descending order based on their timestamp.</span></span> 
 
     <span data-ttu-id="59dc0-133">Ayrıca Veri Gezgini toocreate saklı yordamlar, UDF'ler ve Tetikleyicileri tooperform sunucu tarafı iş mantığı da kullanabilirsiniz ölçek işleme olarak.</span><span class="sxs-lookup"><span data-stu-id="59dc0-133">You can also use Data Explorer toocreate stored procedures, UDFs, and triggers tooperform server-side business logic as well as scale throughput.</span></span> <span data-ttu-id="59dc0-134">Veri Gezgini tüm hello yerleşik programlı veri erişim hello API'leri kullanılabilir gösterir, ancak tooyour verileri hello Azure portalında kolay erişim sağlar.</span><span class="sxs-lookup"><span data-stu-id="59dc0-134">Data Explorer exposes all of hello built-in programmatic data access available in hello APIs, but provides easy access tooyour data in hello Azure portal.</span></span>

## <a name="clone-hello-sample-application"></a><span data-ttu-id="59dc0-135">Merhaba örnek uygulaması kopyalama</span><span class="sxs-lookup"><span data-stu-id="59dc0-135">Clone hello sample application</span></span>

<span data-ttu-id="59dc0-136">Şimdi şimdi koduyla tooworking geçin.</span><span class="sxs-lookup"><span data-stu-id="59dc0-136">Now let's switch tooworking with code.</span></span> <span data-ttu-id="59dc0-137">Şimdi DocumentDB API uygulaması github'dan hello bağlantı dizesini ayarlamak ve çalıştırın kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="59dc0-137">Let's clone a DocumentDB API app from GitHub, set hello connection string, and run it.</span></span> <span data-ttu-id="59dc0-138">Ne kadar kolay toowork verilerle program aracılığıyla olduğunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="59dc0-138">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="59dc0-139">Git bash gibi bir git terminal penceresi açın ve `CD` tooa çalışma dizini.</span><span class="sxs-lookup"><span data-stu-id="59dc0-139">Open a git terminal window, such as git bash, and `CD` tooa working directory.</span></span>  

2. <span data-ttu-id="59dc0-140">Çalışma hello aşağıdaki tooclone hello örnek depo komutu.</span><span class="sxs-lookup"><span data-stu-id="59dc0-140">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git
    ```

## <a name="review-hello-code"></a><span data-ttu-id="59dc0-141">Merhaba kod gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="59dc0-141">Review hello code</span></span>

<span data-ttu-id="59dc0-142">Neler olduğuna dair hello uygulamada hızlı bir gözden geçirme olalım.</span><span class="sxs-lookup"><span data-stu-id="59dc0-142">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="59dc0-143">Açık hello `Program.java` dosya hello \src\GetStarted klasöründen ve hello Azure Cosmos DB kaynakları oluşturma bu kod satırları bulur.</span><span class="sxs-lookup"><span data-stu-id="59dc0-143">Open hello `Program.java` file from hello \src\GetStarted folder, and find these lines of code that create hello Azure Cosmos DB resources.</span></span> 

* <span data-ttu-id="59dc0-144">Merhaba `DocumentClient` başlatılır.</span><span class="sxs-lookup"><span data-stu-id="59dc0-144">hello `DocumentClient` is initialized.</span></span>

    ```java
    this.client = new DocumentClient("https://FILLME.documents.azure.com",
            "FILLME", 
            new ConnectionPolicy(),
            ConsistencyLevel.Session);
    ```

* <span data-ttu-id="59dc0-145">Yeni bir veritabanı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="59dc0-145">A new database is created.</span></span>

    ```java
    Database database = new Database();
    database.setId(databaseName);
    
    this.client.createDatabase(database, null);
    ```

* <span data-ttu-id="59dc0-146">Yeni bir koleksiyon oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="59dc0-146">A new collection is created.</span></span>

    ```java
    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId(collectionName);

    ...

    this.client.createCollection(databaseLink, collectionInfo, requestOptions);
    ```

* <span data-ttu-id="59dc0-147">Birkaç belge oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="59dc0-147">Some documents are created.</span></span>

    ```java
    // Any Java object within your code can be serialized into JSON and written tooAzure Cosmos DB
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen");
    // More properties

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    this.client.createDocument(collectionLink, family, new RequestOptions(), true);
    ```

* <span data-ttu-id="59dc0-148">JSON üzerinden bir SQL sorgusu gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="59dc0-148">A SQL query over JSON is performed.</span></span>

    ```java
    FeedOptions queryOptions = new FeedOptions();
    queryOptions.setPageSize(-1);
    queryOptions.setEnableCrossPartitionQuery(true);

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    FeedResponse<Document> queryResults = this.client.queryDocuments(
        collectionLink,
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", queryOptions);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }
    ```    

## <a name="update-your-connection-string"></a><span data-ttu-id="59dc0-149">Bağlantı dizenizi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="59dc0-149">Update your connection string</span></span>

<span data-ttu-id="59dc0-150">Şimdi Azure portal tooget toohello bağlantı dizesi bilgilerinizi geri dönün ve hello uygulamaya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="59dc0-150">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span> <span data-ttu-id="59dc0-151">Bu, uygulama toocommunicate barındırılan veritabanınızla olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="59dc0-151">This will enable your app toocommunicate with your hosted database.</span></span>

1. <span data-ttu-id="59dc0-152">Merhaba, [Azure portal](http://portal.azure.com/), Azure Cosmos DB hesap, sol gezinti hello tıklatın **anahtarları**ve ardından **okuma-yazma anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="59dc0-152">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="59dc0-153">Merhaba Kopyala düğmesi hello sağ tarafındaki Merhaba ekranında toocopy hello URI ve birincil anahtar hello kullanacağınız `Program.java` hello sonraki adımda dosya.</span><span class="sxs-lookup"><span data-stu-id="59dc0-153">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and PRIMARY KEY into hello `Program.java` file in hello next step.</span></span>

    ![Görüntüleme ve kopyalama hello Azure portalına erişim tuşu, anahtarlar dikey penceresinde](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="59dc0-155">Merhaba açık olarak `Program.java` dosya, URI değeri (Merhaba Kopyala düğmesini kullanarak) hello Portal'dan kopyalayın ve hale hello hello uç nokta toohello DocumentClient oluşturucuda değerini `Program.java`.</span><span class="sxs-lookup"><span data-stu-id="59dc0-155">In hello open `Program.java` file, copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint toohello DocumentClient constructor in `Program.java`.</span></span> 

    `"https://FILLME.documents.azure.com"`

4. <span data-ttu-id="59dc0-156">Sonra birincil anahtar değer hello Portal'dan kopyalayın ve "kolaylaştırarak FILLME", yapıştırın hello DocumentClient oluşturucuda ikinci parametre hello.</span><span class="sxs-lookup"><span data-stu-id="59dc0-156">Then copy your PRIMARY KEY value from hello portal and paste it over “FILLME”, making it hello second parameter in hello DocumentClient constructor.</span></span> <span data-ttu-id="59dc0-157">Uygulamanızı şimdi güncelleştirdikten toocommunicate Azure Cosmos DB ile gerekli tüm hello bilgilerine sahip.</span><span class="sxs-lookup"><span data-stu-id="59dc0-157">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 
    
## <a name="run-hello-app"></a><span data-ttu-id="59dc0-158">Merhaba uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="59dc0-158">Run hello app</span></span>

1. <span data-ttu-id="59dc0-159">Penceresinde hello git terminal `cd` toohello azure-cosmos-db-documentdb-java-getting-started klasör.</span><span class="sxs-lookup"><span data-stu-id="59dc0-159">In hello git terminal window, `cd` toohello azure-cosmos-db-documentdb-java-getting-started folder.</span></span>

2. <span data-ttu-id="59dc0-160">Merhaba git terminal penceresinde yazın `mvn package` tooinstall hello Java paketleri gereklidir.</span><span class="sxs-lookup"><span data-stu-id="59dc0-160">In hello git terminal window, type `mvn package` tooinstall hello required Java packages.</span></span>

3. <span data-ttu-id="59dc0-161">Merhaba git terminal penceresinde çalıştırın `mvn exec:java -D exec.mainClass=GetStarted.Program` içinde Java uygulamanız terminal penceresi toostart hello.</span><span class="sxs-lookup"><span data-stu-id="59dc0-161">In hello git terminal window, run `mvn exec:java -D exec.mainClass=GetStarted.Program` in hello terminal window toostart your Java application.</span></span>

    <span data-ttu-id="59dc0-162">Merhaba terminal penceresinde veritabanı oluşturuldu FamilyDB hello bildirim ve toopress anahtar toocontinue alırsınız.</span><span class="sxs-lookup"><span data-stu-id="59dc0-162">In hello terminal window, you'll receive notification that hello FamilyDB database was created, and toopress a key toocontinue.</span></span> <span data-ttu-id="59dc0-163">Bir anahtar toocreate hello veritabanı tuşuna basın, sonra toohello Veri Gezgini geçiş ve şimdi FamilyDB veritabanı içerdiği görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="59dc0-163">Press a key toocreate hello database, then switch toohello Data Explorer and you'll see that it now contains a FamilyDB database.</span></span> <span data-ttu-id="59dc0-164">Koleksiyon ve hello toopress anahtarları toocreate hello belgeleri devam ve bir sorgu gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="59dc0-164">Continue toopress keys toocreate hello collection and hello documents and then perform a query.</span></span> <span data-ttu-id="59dc0-165">Merhaba Proje tamamlandığında hello kaynakları hesabınızdan silinir.</span><span class="sxs-lookup"><span data-stu-id="59dc0-165">When hello project completes, hello resources are deleted from your account.</span></span> 

    ![Görüntüleme ve kopyalama hello Azure portalına erişim tuşu, anahtarlar dikey penceresinde](./media/create-documentdb-java/console-output.png)


## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="59dc0-167">Gözden geçirme SLA'hello Azure portalı</span><span class="sxs-lookup"><span data-stu-id="59dc0-167">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="59dc0-168">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="59dc0-168">Clean up resources</span></span>

<span data-ttu-id="59dc0-169">Toocontinue toouse bu uygulamayı değil kullanacaksanız, bu hızlı başlangıç tarafından hello Azure portalında aşağıdaki adımları hello ile oluşturulan tüm kaynakları silin:</span><span class="sxs-lookup"><span data-stu-id="59dc0-169">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="59dc0-170">Merhaba sol taraftaki menüden hello Azure portal'ın, **kaynak grupları** ve ardından oluşturduğunuz hello kaynak hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="59dc0-170">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="59dc0-171">Kaynak grubu sayfanızda tıklatın **silmek**hello metin kutusuna hello kaynak toodelete hello adını yazın ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="59dc0-171">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="59dc0-172">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="59dc0-172">Next steps</span></span>

<span data-ttu-id="59dc0-173">Bu hızlı başlangıç nasıl toocreate Azure Cosmos DB hesabınız, belge veritabanı ve hello Veri Gezgini'ni kullanarak ve bir uygulama toodo çalıştırın koleksiyonu aynısını program aracılığıyla hello öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="59dc0-173">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, document database, and collection using hello Data Explorer, and run an app toodo hello same thing programmatically.</span></span> <span data-ttu-id="59dc0-174">Artık ek verileri tooyour Cosmos DB hesap içeri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59dc0-174">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="59dc0-175">Azure Cosmos DB hesabınıza veri aktarma</span><span class="sxs-lookup"><span data-stu-id="59dc0-175">Import data into Azure Cosmos DB</span></span>](import-data.md)


