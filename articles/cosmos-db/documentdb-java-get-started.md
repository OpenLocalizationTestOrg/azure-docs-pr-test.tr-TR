---
title: "NoSQL Öğreticisi: DocumentDB API Azure Cosmos DB Java SDK'sı | Microsoft Docs"
description: "Çevrimiçi bir veritabanı ve Azure Cosmos DB için hello DocumentDB API kullanarak Java konsol uygulaması oluşturan bir NoSQL Öğreticisi. Azure DocumentDB, JSON için bir NoSQL veritabanıdır."
keywords: "nosql öğreticisi, çevrimiçi veritabanı, java konsol uygulaması"
services: cosmos-db
documentationcenter: Java
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: 75a9efa1-7edd-4fed-9882-c0177274cbb2
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 05/22/2017
ms.author: arramac
ms.openlocfilehash: 1a298a15ab911d140b9df30ad52cfe0fa07c55b8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="nosql-tutorial-build-a-documentdb-api-java-console-application"></a><span data-ttu-id="d12df-105">NoSQL Öğreticisi: DocumentDB API Java konsol uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="d12df-105">NoSQL tutorial: Build a DocumentDB API Java console application</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d12df-106">.NET</span><span class="sxs-lookup"><span data-stu-id="d12df-106">.NET</span></span>](documentdb-get-started.md)
> * [<span data-ttu-id="d12df-107">.NET Core</span><span class="sxs-lookup"><span data-stu-id="d12df-107">.NET Core</span></span>](documentdb-dotnetcore-get-started.md)
> * [<span data-ttu-id="d12df-108">MongoDB için Node.js</span><span class="sxs-lookup"><span data-stu-id="d12df-108">Node.js for MongoDB</span></span>](mongodb-samples.md)
> * [<span data-ttu-id="d12df-109">Node.js</span><span class="sxs-lookup"><span data-stu-id="d12df-109">Node.js</span></span>](documentdb-nodejs-get-started.md)
> * [<span data-ttu-id="d12df-110">Java</span><span class="sxs-lookup"><span data-stu-id="d12df-110">Java</span></span>](documentdb-java-get-started.md)
> * [<span data-ttu-id="d12df-111">C++</span><span class="sxs-lookup"><span data-stu-id="d12df-111">C++</span></span>](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="d12df-112">Merhaba DocumentDB API için toohello NoSQL öğreticisi için Azure Cosmos DB Java SDK'na Hoş Geldiniz!</span><span class="sxs-lookup"><span data-stu-id="d12df-112">Welcome toohello NoSQL tutorial for hello DocumentDB API for Azure Cosmos DB Java SDK!</span></span> <span data-ttu-id="d12df-113">Bu öğreticiyi uyguladıktan sonra, Azure Cosmos DB kaynaklarını oluşturan ve sorgulayan bir konsol uygulamasına sahip olacaksınız.</span><span class="sxs-lookup"><span data-stu-id="d12df-113">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="d12df-114">Kapsanan konular:</span><span class="sxs-lookup"><span data-stu-id="d12df-114">We cover:</span></span>

* <span data-ttu-id="d12df-115">Oluşturma ve tooan Azure Cosmos DB hesabına bağlanma</span><span class="sxs-lookup"><span data-stu-id="d12df-115">Creating and connecting tooan Azure Cosmos DB account</span></span>
* <span data-ttu-id="d12df-116">Visual Studio Çözümünüzü yapılandırma</span><span class="sxs-lookup"><span data-stu-id="d12df-116">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="d12df-117">Çevrimiçi bir veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d12df-117">Creating an online database</span></span>
* <span data-ttu-id="d12df-118">Koleksiyon oluşturma</span><span class="sxs-lookup"><span data-stu-id="d12df-118">Creating a collection</span></span>
* <span data-ttu-id="d12df-119">JSON belgeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="d12df-119">Creating JSON documents</span></span>
* <span data-ttu-id="d12df-120">Merhaba koleksiyonu sorgulama</span><span class="sxs-lookup"><span data-stu-id="d12df-120">Querying hello collection</span></span>
* <span data-ttu-id="d12df-121">JSON belgeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="d12df-121">Creating JSON documents</span></span>
* <span data-ttu-id="d12df-122">Merhaba koleksiyonu sorgulama</span><span class="sxs-lookup"><span data-stu-id="d12df-122">Querying hello collection</span></span>
* <span data-ttu-id="d12df-123">Bir belgeyi değiştirme</span><span class="sxs-lookup"><span data-stu-id="d12df-123">Replacing a document</span></span>
* <span data-ttu-id="d12df-124">Bir belgeyi silme</span><span class="sxs-lookup"><span data-stu-id="d12df-124">Deleting a document</span></span>
* <span data-ttu-id="d12df-125">Merhaba veritabanını silme</span><span class="sxs-lookup"><span data-stu-id="d12df-125">Deleting hello database</span></span>

<span data-ttu-id="d12df-126">Şimdi başlayalım!</span><span class="sxs-lookup"><span data-stu-id="d12df-126">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d12df-127">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="d12df-127">Prerequisites</span></span>
<span data-ttu-id="d12df-128">Merhaba aşağıdaki bulunduğundan emin olun:</span><span class="sxs-lookup"><span data-stu-id="d12df-128">Make sure you have hello following:</span></span>

* <span data-ttu-id="d12df-129">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="d12df-129">An active Azure account.</span></span> <span data-ttu-id="d12df-130">Bir aboneliğiniz yoksa [ücretsiz bir hesap](https://azure.microsoft.com/free/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d12df-130">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> <span data-ttu-id="d12df-131">Alternatif olarak, hello kullanabilirsiniz [Azure Cosmos DB öykünücüsü](local-emulator.md) Bu öğretici için.</span><span class="sxs-lookup"><span data-stu-id="d12df-131">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="d12df-132">Git</span><span class="sxs-lookup"><span data-stu-id="d12df-132">Git</span></span>](https://git-scm.com/downloads)
* <span data-ttu-id="d12df-133">[Java Geliştirme Seti (JDK) 7 +](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="d12df-133">[Java Development Kit (JDK) 7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* <span data-ttu-id="d12df-134">[Maven](http://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="d12df-134">[Maven](http://maven.apache.org/download.cgi).</span></span>

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="d12df-135">1. Adım: Azure Cosmos DB hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d12df-135">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="d12df-136">Bir Azure Cosmos DB hesabı oluşturalım.</span><span class="sxs-lookup"><span data-stu-id="d12df-136">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="d12df-137">Toouse istediğiniz bir hesap zaten varsa, şimdi çok atlayabilirsiniz[kopya hello GitHub proje](#GitClone).</span><span class="sxs-lookup"><span data-stu-id="d12df-137">If you already have an account you want toouse, you can skip ahead too[Clone hello GitHub project](#GitClone).</span></span> <span data-ttu-id="d12df-138">Hello Azure Cosmos DB öykünücüsü kullanıyorsanız, hello adımları izleyin [Azure Cosmos DB öykünücüsü](local-emulator.md) tooset yukarı hello öykünücüsü ve İleri çok atlayabilirsiniz[kopya hello GitHub proje](#GitClone).</span><span class="sxs-lookup"><span data-stu-id="d12df-138">If you are using hello Azure Cosmos DB Emulator, follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) tooset up hello emulator and skip ahead too[Clone hello GitHub project](#GitClone).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="d12df-139"><a id="GitClone"></a>2. adım: Kopya hello GitHub proje</span><span class="sxs-lookup"><span data-stu-id="d12df-139"><a id="GitClone"></a>Step 2: Clone hello GitHub project</span></span>
<span data-ttu-id="d12df-140">Merhaba GitHub deposunu kopyalanarak başlayabiliriz [Azure Cosmos DB ve Java ile çalışmaya başlama](https://github.com/Azure-Samples/documentdb-java-getting-started).</span><span class="sxs-lookup"><span data-stu-id="d12df-140">You can get started by cloning hello GitHub repository for [Get Started with Azure Cosmos DB and Java](https://github.com/Azure-Samples/documentdb-java-getting-started).</span></span> <span data-ttu-id="d12df-141">Örneğin, yerel bir dizinden tooretrieve hello örnek projesini yerel olarak aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="d12df-141">For example, from a local directory run hello following tooretrieve hello sample project locally.</span></span>

    git clone git@github.com:Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git

    cd azure-cosmos-db-documentdb-java-getting-started

<span data-ttu-id="d12df-142">Merhaba dizini içeren bir `pom.xml` hello projesi için ve bir `src` Java kaynak kodu da dahil olmak üzere içeren klasörü `Program.java` hangi gösterir nasıl basit belgelerin oluşturulması ve içinde veri sorgulama gibi Azure Cosmos DB ile işlemleri bir koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="d12df-142">hello directory contains a `pom.xml` for hello project and a `src` folder containing Java source code including `Program.java` which shows how perform simple operations with Azure Cosmos DB like creating documents and querying data within a collection.</span></span> <span data-ttu-id="d12df-143">Merhaba `pom.xml` hello üzerinde bir bağımlılığı [üzerinde Maven DocumentDB Java SDK'sı](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span><span class="sxs-lookup"><span data-stu-id="d12df-143">hello `pom.xml` includes a dependency on hello [DocumentDB Java SDK on Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).</span></span>

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-documentdb</artifactId>
        <version>LATEST</version>
    </dependency>

## <span data-ttu-id="d12df-144"><a id="Connect"></a>3. adım: tooan Azure Cosmos DB hesap bağlanma</span><span class="sxs-lookup"><span data-stu-id="d12df-144"><a id="Connect"></a>Step 3: Connect tooan Azure Cosmos DB account</span></span>
<span data-ttu-id="d12df-145">Ardından, head geri toohello [Azure Portal](https://portal.azure.com) tooretrieve uç noktası ve birincil ana anahtar.</span><span class="sxs-lookup"><span data-stu-id="d12df-145">Next, head back toohello [Azure Portal](https://portal.azure.com) tooretrieve your endpoint and primary master key.</span></span> <span data-ttu-id="d12df-146">Hello Azure Cosmos DB uç noktası ve birincil anahtar, uygulama toounderstand için gerekli olduğu tooconnect ve Azure Cosmos DB tootrust için uygulamanızın bağlantı.</span><span class="sxs-lookup"><span data-stu-id="d12df-146">hello Azure Cosmos DB endpoint and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="d12df-147">İçinde Azure Portal Merhaba, tooyour Azure Cosmos DB hesap gidin ve ardından **anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="d12df-147">In hello Azure Portal, navigate tooyour Azure Cosmos DB account, and then click **Keys**.</span></span> <span data-ttu-id="d12df-148">Merhaba URI hello Portal'dan kopyalayın ve yapıştırın `https://FILLME.documents.azure.com` hello Program.java dosyasında.</span><span class="sxs-lookup"><span data-stu-id="d12df-148">Copy hello URI from hello portal and paste it into `https://FILLME.documents.azure.com` in hello Program.java file.</span></span> <span data-ttu-id="d12df-149">BİRİNCİL anahtar hello portalından hello kopyalayıp yapıştırın sonra `FILLME`.</span><span class="sxs-lookup"><span data-stu-id="d12df-149">Then copy hello PRIMARY KEY from hello portal and paste it into `FILLME`.</span></span>

    this.client = new DocumentClient(
        "https://FILLME.documents.azure.com",
        "FILLME"
        , new ConnectionPolicy(),
        ConsistencyLevel.Session);

![Merhaba hello NoSQL Öğreticisi toocreate bir Java konsol uygulaması tarafından kullanılan Azure Portal ekran görüntüsü.][keys]

## <a name="step-4-create-a-database"></a><span data-ttu-id="d12df-152">4. Adım: Veritabanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="d12df-152">Step 4: Create a database</span></span>
<span data-ttu-id="d12df-153">Azure Cosmos DB [veritabanı](documentdb-resources.md#databases) hello kullanarak oluşturulan [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) hello yöntemi **DocumentClient** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="d12df-153">Your Azure Cosmos DB [database](documentdb-resources.md#databases) can be created by using hello [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="d12df-154">Bir veritabanı hello mantıksal, koleksiyonlar genelinde bölümlenmiş JSON belgesi depolama kapsayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="d12df-154">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

    Database database = new Database();
    database.setId("familydb");
    this.client.createDatabase(database, null);

## <span data-ttu-id="d12df-155"><a id="CreateColl"></a>5. Adım: Koleksiyon oluşturma</span><span class="sxs-lookup"><span data-stu-id="d12df-155"><a id="CreateColl"></a>Step 5: Create a collection</span></span>
> [!WARNING]
> <span data-ttu-id="d12df-156">**createCollection**, ayrılmış işleme ile yeni bir koleksiyon oluşturur, bu da ücret ödenmesini gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="d12df-156">**createCollection** creates a new collection with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="d12df-157">Daha ayrıntılı bilgi için [fiyatlandırma sayfamızı](https://azure.microsoft.com/pricing/details/cosmos-db/) ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="d12df-157">For more details, visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span>
> 
> 

<span data-ttu-id="d12df-158">A [koleksiyonu](documentdb-resources.md#collections) hello kullanarak oluşturulan [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) hello yöntemi **DocumentClient** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="d12df-158">A [collection](documentdb-resources.md#collections) can be created by using hello [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="d12df-159">Koleksiyon, JSON belgelerinin ve ilişkili JavaScript uygulama mantığının bir kapsayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="d12df-159">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>


    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId("familycoll");

    // Azure Cosmos DB collections can be reserved with throughput specified in request units/second. 
    // Here we create a collection with 400 RU/s.
    RequestOptions requestOptions = new RequestOptions();
    requestOptions.setOfferThroughput(400);

    this.client.createCollection("/dbs/familydb", collectionInfo, requestOptions);

## <span data-ttu-id="d12df-160"><a id="CreateDoc"></a>6. Adım: JSON belgeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="d12df-160"><a id="CreateDoc"></a>Step 6: Create JSON documents</span></span>
<span data-ttu-id="d12df-161">A [belge](documentdb-resources.md#documents) hello kullanarak oluşturulan [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) hello yöntemi **DocumentClient** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="d12df-161">A [document](documentdb-resources.md#documents) can be created by using hello [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="d12df-162">Belgeler, kullanıcı tanımlı (rastgele) JSON içerikleridir.</span><span class="sxs-lookup"><span data-stu-id="d12df-162">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="d12df-163">Şimdi bir veya daha fazla belge ekleyebiliriz.</span><span class="sxs-lookup"><span data-stu-id="d12df-163">We can now insert one or more documents.</span></span> <span data-ttu-id="d12df-164">İstediğiniz toostore veritabanınızda veriler zaten varsa, Azure Cosmos veritabanı kullanabilirsiniz [veri geçiş aracı](import-data.md) tooimport hello verileri bir veritabanına.</span><span class="sxs-lookup"><span data-stu-id="d12df-164">If you already have data you'd like toostore in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md) tooimport hello data into a database.</span></span>

    // Insert your Java objects as documents 
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen")

    // More initialization skipped for brevity. You can have nested references
    andersenFamily.setParents(new Parent[] { parent1, parent2 });
    andersenFamily.setDistrict("WA5");
    Address address = new Address();
    address.setCity("Seattle");
    address.setCounty("King");
    address.setState("WA");

    andersenFamily.setAddress(address);
    andersenFamily.setRegistered(true);

    this.client.createDocument("/dbs/familydb/colls/familycoll", family, new RequestOptions(), true);

![Gösteren hello hello hesabı, hello çevrimiçi veritabanı, hello koleksiyon arasındaki hiyerarşik ilişkiyi Diyagram ve bir Java konsol uygulaması hello NoSQL Öğreticisi toocreate tarafından kullanılan hello belgeler](./media/documentdb-get-started/nosql-tutorial-account-database.png)

## <span data-ttu-id="d12df-166"><a id="Query"></a>7. Adım: Azure Cosmos DB kaynaklarını sorgulama</span><span class="sxs-lookup"><span data-stu-id="d12df-166"><a id="Query"></a>Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="d12df-167">Azure Cosmos DB, her bir koleksiyonda depolanan JSON belgeleri için [zengin sorguların](documentdb-sql-query.md) gerçekleştirilmesini destekler.</span><span class="sxs-lookup"><span data-stu-id="d12df-167">Azure Cosmos DB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="d12df-168">Aşağıdaki örnek kod hello gösterir nasıl tooquery Azure Cosmos DB'de belgeleri ile Merhaba SQL sözdizimini kullanarak [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d12df-168">hello following sample code shows how tooquery documents in Azure Cosmos DB using SQL syntax with hello [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) method.</span></span>

    FeedResponse<Document> queryResults = this.client.queryDocuments(
        "/dbs/familydb/colls/familycoll",
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", 
        null);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }

## <span data-ttu-id="d12df-169"><a id="ReplaceDocument"></a>8. Adım: JSON belgesini değiştirme</span><span class="sxs-lookup"><span data-stu-id="d12df-169"><a id="ReplaceDocument"></a>Step 8: Replace JSON document</span></span>
<span data-ttu-id="d12df-170">Azure Cosmos DB destekleyen hello kullanarak güncelleştirme JSON belgeleri [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d12df-170">Azure Cosmos DB supports updating JSON documents using hello [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) method.</span></span>

    // Update a property
    andersenFamily.Children[0].Grade = 6;

    this.client.replaceDocument(
        "/dbs/familydb/colls/familycoll/docs/Andersen.1", 
        andersenFamily,
        null);

## <span data-ttu-id="d12df-171"><a id="DeleteDocument"></a>9. Adım: JSON belgesini silme</span><span class="sxs-lookup"><span data-stu-id="d12df-171"><a id="DeleteDocument"></a>Step 9: Delete JSON document</span></span>
<span data-ttu-id="d12df-172">Benzer şekilde, Azure Cosmos DB hello kullanarak JSON belgelerini silmeyi destekler [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="d12df-172">Similarly, Azure Cosmos DB supports deleting JSON documents using hello [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) method.</span></span>  

    this.client.delete("/dbs/familydb/colls/familycoll/docs/Andersen.1", null);

## <span data-ttu-id="d12df-173"><a id="DeleteDatabase"></a>10. adım: hello veritabanını silme</span><span class="sxs-lookup"><span data-stu-id="d12df-173"><a id="DeleteDatabase"></a>Step 10: Delete hello database</span></span>
<span data-ttu-id="d12df-174">Oluşturulan hello veritabanı siliniyor hello veritabanı ve tüm alt kaynaklar (koleksiyonlar, belgeler, vb.) kaldırır.</span><span class="sxs-lookup"><span data-stu-id="d12df-174">Deleting hello created database removes hello database and all children resources (collections, documents, etc.).</span></span>

    this.client.deleteDatabase("/dbs/familydb", null);

## <span data-ttu-id="d12df-175"><a id="Run"></a>11. Adım: Java konsol uygulamanızı hep birlikte çalıştırın!</span><span class="sxs-lookup"><span data-stu-id="d12df-175"><a id="Run"></a>Step 11: Run your Java console application all together!</span></span>
<span data-ttu-id="d12df-176">toorun hello hello konsol uygulamasından toohello proje klasörünü ve Maven kullanarak derleme gidin:</span><span class="sxs-lookup"><span data-stu-id="d12df-176">toorun hello application from hello console, navigate toohello project folder and compile using Maven:</span></span>
    
    mvn package

<span data-ttu-id="d12df-177">Çalışan `mvn package` Maven hello en son Azure Cosmos DB Kitaplığı indirir ve üreten `GetStarted-0.0.1-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="d12df-177">Running `mvn package` downloads hello latest Azure Cosmos DB library from Maven and produces `GetStarted-0.0.1-SNAPSHOT.jar`.</span></span> <span data-ttu-id="d12df-178">Ardından hello uygulama çalıştırarak çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="d12df-178">Then run hello app by running:</span></span>

    mvn exec:java -D exec.mainClass=GetStarted.Program

<span data-ttu-id="d12df-179">Tebrikler!</span><span class="sxs-lookup"><span data-stu-id="d12df-179">Congratulations!</span></span> <span data-ttu-id="d12df-180">Bu NoSQL öğreticisini tamamladınız ve çalışan bir Java konsol uygulamasına sahipsiniz!</span><span class="sxs-lookup"><span data-stu-id="d12df-180">You've completed this NoSQL tutorial and have a working Java console application!</span></span>

## <a name="next-steps"></a><span data-ttu-id="d12df-181">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d12df-181">Next steps</span></span>
* <span data-ttu-id="d12df-182">Java web uygulaması öğreticisi ister misiniz?</span><span class="sxs-lookup"><span data-stu-id="d12df-182">Want a Java web app tutorial?</span></span> <span data-ttu-id="d12df-183">Bkz. [Azure Cosmos DB kullanarak Java ile bir web uygulaması oluşturma](documentdb-java-application.md).</span><span class="sxs-lookup"><span data-stu-id="d12df-183">See [Build a web application with Java using Azure Cosmos DB](documentdb-java-application.md).</span></span>
* <span data-ttu-id="d12df-184">Nasıl çok öğrenin[Azure Cosmos DB hesabını izleme](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="d12df-184">Learn how too[monitor an Azure Cosmos DB account](monitor-accounts.md).</span></span>
* <span data-ttu-id="d12df-185">Merhaba, örnek veri kümelerimizde sorgular çalıştırın [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="d12df-185">Run queries against our sample dataset in hello [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="d12df-186">Merhaba hello hello geliştirme bölümünde programlama modelleri hakkında daha fazla bilgi edinin [Azure Cosmos DB belge sayfasının](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="d12df-186">Learn more about hello programming model in hello Develop section of hello [Azure Cosmos DB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
