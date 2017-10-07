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
# <a name="nosql-tutorial-build-a-documentdb-api-java-console-application"></a>NoSQL Öğreticisi: DocumentDB API Java konsol uygulaması oluşturma
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [MongoDB için Node.js](mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

Merhaba DocumentDB API için toohello NoSQL öğreticisi için Azure Cosmos DB Java SDK'na Hoş Geldiniz! Bu öğreticiyi uyguladıktan sonra, Azure Cosmos DB kaynaklarını oluşturan ve sorgulayan bir konsol uygulamasına sahip olacaksınız.

Kapsanan konular:

* Oluşturma ve tooan Azure Cosmos DB hesabına bağlanma
* Visual Studio Çözümünüzü yapılandırma
* Çevrimiçi bir veritabanı oluşturma
* Koleksiyon oluşturma
* JSON belgeleri oluşturma
* Merhaba koleksiyonu sorgulama
* JSON belgeleri oluşturma
* Merhaba koleksiyonu sorgulama
* Bir belgeyi değiştirme
* Bir belgeyi silme
* Merhaba veritabanını silme

Şimdi başlayalım!

## <a name="prerequisites"></a>Ön koşullar
Merhaba aşağıdaki bulunduğundan emin olun:

* Etkin bir Azure hesabı. Bir aboneliğiniz yoksa [ücretsiz bir hesap](https://azure.microsoft.com/free/) için kaydolabilirsiniz. Alternatif olarak, hello kullanabilirsiniz [Azure Cosmos DB öykünücüsü](local-emulator.md) Bu öğretici için.
* [Git](https://git-scm.com/downloads)
* [Java Geliştirme Seti (JDK) 7 +](http://www.oracle.com/technetwork/java/javase/downloads/index.html).
* [Maven](http://maven.apache.org/download.cgi).

## <a name="step-1-create-an-azure-cosmos-db-account"></a>1. Adım: Azure Cosmos DB hesabı oluşturma
Bir Azure Cosmos DB hesabı oluşturalım. Toouse istediğiniz bir hesap zaten varsa, şimdi çok atlayabilirsiniz[kopya hello GitHub proje](#GitClone). Hello Azure Cosmos DB öykünücüsü kullanıyorsanız, hello adımları izleyin [Azure Cosmos DB öykünücüsü](local-emulator.md) tooset yukarı hello öykünücüsü ve İleri çok atlayabilirsiniz[kopya hello GitHub proje](#GitClone).

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="GitClone"></a>2. adım: Kopya hello GitHub proje
Merhaba GitHub deposunu kopyalanarak başlayabiliriz [Azure Cosmos DB ve Java ile çalışmaya başlama](https://github.com/Azure-Samples/documentdb-java-getting-started). Örneğin, yerel bir dizinden tooretrieve hello örnek projesini yerel olarak aşağıdaki hello çalıştırın.

    git clone git@github.com:Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git

    cd azure-cosmos-db-documentdb-java-getting-started

Merhaba dizini içeren bir `pom.xml` hello projesi için ve bir `src` Java kaynak kodu da dahil olmak üzere içeren klasörü `Program.java` hangi gösterir nasıl basit belgelerin oluşturulması ve içinde veri sorgulama gibi Azure Cosmos DB ile işlemleri bir koleksiyonu. Merhaba `pom.xml` hello üzerinde bir bağımlılığı [üzerinde Maven DocumentDB Java SDK'sı](https://mvnrepository.com/artifact/com.microsoft.azure/azure-documentdb).

    <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>azure-documentdb</artifactId>
        <version>LATEST</version>
    </dependency>

## <a id="Connect"></a>3. adım: tooan Azure Cosmos DB hesap bağlanma
Ardından, head geri toohello [Azure Portal](https://portal.azure.com) tooretrieve uç noktası ve birincil ana anahtar. Hello Azure Cosmos DB uç noktası ve birincil anahtar, uygulama toounderstand için gerekli olduğu tooconnect ve Azure Cosmos DB tootrust için uygulamanızın bağlantı.

İçinde Azure Portal Merhaba, tooyour Azure Cosmos DB hesap gidin ve ardından **anahtarları**. Merhaba URI hello Portal'dan kopyalayın ve yapıştırın `https://FILLME.documents.azure.com` hello Program.java dosyasında. BİRİNCİL anahtar hello portalından hello kopyalayıp yapıştırın sonra `FILLME`.

    this.client = new DocumentClient(
        "https://FILLME.documents.azure.com",
        "FILLME"
        , new ConnectionPolicy(),
        ConsistencyLevel.Session);

![Merhaba hello NoSQL Öğreticisi toocreate bir Java konsol uygulaması tarafından kullanılan Azure Portal ekran görüntüsü. Hesap, hello etkin hub vurgulandığı ile Merhaba hello Azure Cosmos DB hesabı dikey penceresinde ANAHTARLAR düğmesi ve anahtarlar dikey penceresinde hello üzerinde hello URI, birincil anahtar ve ikincil anahtar değerleri vurgulanmış bir Azure Cosmos DB gösterir][keys]

## <a name="step-4-create-a-database"></a>4. Adım: Veritabanı oluşturma
Azure Cosmos DB [veritabanı](documentdb-resources.md#databases) hello kullanarak oluşturulan [createDatabase](/java/api/com.microsoft.azure.documentdb._document_client.createdatabase) hello yöntemi **DocumentClient** sınıfı. Bir veritabanı hello mantıksal, koleksiyonlar genelinde bölümlenmiş JSON belgesi depolama kapsayıcısıdır.

    Database database = new Database();
    database.setId("familydb");
    this.client.createDatabase(database, null);

## <a id="CreateColl"></a>5. Adım: Koleksiyon oluşturma
> [!WARNING]
> **createCollection**, ayrılmış işleme ile yeni bir koleksiyon oluşturur, bu da ücret ödenmesini gerektirebilir. Daha ayrıntılı bilgi için [fiyatlandırma sayfamızı](https://azure.microsoft.com/pricing/details/cosmos-db/) ziyaret edin.
> 
> 

A [koleksiyonu](documentdb-resources.md#collections) hello kullanarak oluşturulan [createCollection](/java/api/com.microsoft.azure.documentdb._document_client.createcollection) hello yöntemi **DocumentClient** sınıfı. Koleksiyon, JSON belgelerinin ve ilişkili JavaScript uygulama mantığının bir kapsayıcısıdır.


    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId("familycoll");

    // Azure Cosmos DB collections can be reserved with throughput specified in request units/second. 
    // Here we create a collection with 400 RU/s.
    RequestOptions requestOptions = new RequestOptions();
    requestOptions.setOfferThroughput(400);

    this.client.createCollection("/dbs/familydb", collectionInfo, requestOptions);

## <a id="CreateDoc"></a>6. Adım: JSON belgeleri oluşturma
A [belge](documentdb-resources.md#documents) hello kullanarak oluşturulan [createDocument](/java/api/com.microsoft.azure.documentdb._document_client.createdocument) hello yöntemi **DocumentClient** sınıfı. Belgeler, kullanıcı tanımlı (rastgele) JSON içerikleridir. Şimdi bir veya daha fazla belge ekleyebiliriz. İstediğiniz toostore veritabanınızda veriler zaten varsa, Azure Cosmos veritabanı kullanabilirsiniz [veri geçiş aracı](import-data.md) tooimport hello verileri bir veritabanına.

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

## <a id="Query"></a>7. Adım: Azure Cosmos DB kaynaklarını sorgulama
Azure Cosmos DB, her bir koleksiyonda depolanan JSON belgeleri için [zengin sorguların](documentdb-sql-query.md) gerçekleştirilmesini destekler.  Aşağıdaki örnek kod hello gösterir nasıl tooquery Azure Cosmos DB'de belgeleri ile Merhaba SQL sözdizimini kullanarak [queryDocuments](/java/api/com.microsoft.azure.documentdb._document_client.querydocuments) yöntemi.

    FeedResponse<Document> queryResults = this.client.queryDocuments(
        "/dbs/familydb/colls/familycoll",
        "SELECT * FROM Family WHERE Family.lastName = 'Andersen'", 
        null);

    System.out.println("Running SQL query...");
    for (Document family : queryResults.getQueryIterable()) {
        System.out.println(String.format("\tRead %s", family));
    }

## <a id="ReplaceDocument"></a>8. Adım: JSON belgesini değiştirme
Azure Cosmos DB destekleyen hello kullanarak güncelleştirme JSON belgeleri [replaceDocument](/java/api/com.microsoft.azure.documentdb._document_client.replacedocument) yöntemi.

    // Update a property
    andersenFamily.Children[0].Grade = 6;

    this.client.replaceDocument(
        "/dbs/familydb/colls/familycoll/docs/Andersen.1", 
        andersenFamily,
        null);

## <a id="DeleteDocument"></a>9. Adım: JSON belgesini silme
Benzer şekilde, Azure Cosmos DB hello kullanarak JSON belgelerini silmeyi destekler [deleteDocument](/java/api/com.microsoft.azure.documentdb._document_client.deletedocument) yöntemi.  

    this.client.delete("/dbs/familydb/colls/familycoll/docs/Andersen.1", null);

## <a id="DeleteDatabase"></a>10. adım: hello veritabanını silme
Oluşturulan hello veritabanı siliniyor hello veritabanı ve tüm alt kaynaklar (koleksiyonlar, belgeler, vb.) kaldırır.

    this.client.deleteDatabase("/dbs/familydb", null);

## <a id="Run"></a>11. Adım: Java konsol uygulamanızı hep birlikte çalıştırın!
toorun hello hello konsol uygulamasından toohello proje klasörünü ve Maven kullanarak derleme gidin:
    
    mvn package

Çalışan `mvn package` Maven hello en son Azure Cosmos DB Kitaplığı indirir ve üreten `GetStarted-0.0.1-SNAPSHOT.jar`. Ardından hello uygulama çalıştırarak çalıştırın:

    mvn exec:java -D exec.mainClass=GetStarted.Program

Tebrikler! Bu NoSQL öğreticisini tamamladınız ve çalışan bir Java konsol uygulamasına sahipsiniz!

## <a name="next-steps"></a>Sonraki adımlar
* Java web uygulaması öğreticisi ister misiniz? Bkz. [Azure Cosmos DB kullanarak Java ile bir web uygulaması oluşturma](documentdb-java-application.md).
* Nasıl çok öğrenin[Azure Cosmos DB hesabını izleme](monitor-accounts.md).
* Merhaba, örnek veri kümelerimizde sorgular çalıştırın [Query Playground](https://www.documentdb.com/sql/demo).
* Merhaba hello hello geliştirme bölümünde programlama modelleri hakkında daha fazla bilgi edinin [Azure Cosmos DB belge sayfasının](https://azure.microsoft.com/documentation/services/documentdb/).

[keys]: media/documentdb-get-started/nosql-tutorial-keys.png
