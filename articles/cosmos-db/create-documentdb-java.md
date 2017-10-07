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
# <a name="azure-cosmos-db-create-a-document-database-using-java-and-hello-azure-portal"></a>Azure Cosmos DB: Java kullanarak bir belge veritabanı oluşturmak ve Azure portal hello

Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir. Hızlı bir şekilde oluşturmak ve belge, anahtar/değer ve grafik veritabanları, her biri hello genel dağıtım ve yatay ölçek özelliklerini Azure Cosmos DB'nin hello çekirdek yararlı sorgulayabilirsiniz. 

Bu hızlı başlangıç bir belge oluşturur Azure Cosmos DB hello Azure portal araçları veritabanını kullanma. Bu hızlı başlangıç ayrıca tooquickly hello kullanarak bir Java konsol uygulaması oluşturma nasıl gösterilmektedir [DocumentDB Java API](documentdb-sdk-java.md). Bu hızlı başlangıç içinde Hello yönergeler Java çalıştırabilen tüm işletim sisteminde izlenebilir. Bu hızlı başlangıç tamamlayarak oluşturma ve belge veritabanı kaynaklarında hello UI ya da programlı şekilde, tercihinize hangisi değiştirme hakkında bilgi sahibi olması.

## <a name="prerequisites"></a>Ön koşullar

* [Java Development Kit (JDK) 1.7+](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)
    * Ubuntu üzerinde çalıştırmak `apt-get install default-jdk` tooinstall hello JDK.
    * Emin tooset hello JAVA_HOME ortam değişkeni toopoint toohello klasörü hello JDK'ın yüklendiği olabilir.
* Bir [Maven](http://maven.apache.org/) ikili arşivi [indirin](http://maven.apache.org/download.cgi) ve [yükleyin](http://maven.apache.org/install.html)
    * Ubuntu üzerinde çalıştırdığınız `apt-get install maven` tooinstall Maven.
* [Git](https://www.git-scm.com/)
    * Ubuntu üzerinde çalıştırdığınız `sudo apt-get install git` tooinstall Git.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Veritabanı hesabı oluşturma

Bir belge veritabanı oluşturabilmeniz için önce toocreate Azure Cosmos DB ile (DocumentDB) SQL veritabanı hesabı gerekir.

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Koleksiyon ekleme

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

<a id="add-sample-data"></a>
## <a name="add-sample-data"></a>Örnek verileri ekleme

Veri Gezgini'ni kullanarak veri tooyour yeni bir koleksiyon artık ekleyebilirsiniz.

1. Veri Gezgini'nde hello yeni veritabanı hello Koleksiyonlar bölmesinde görünür. Merhaba genişletin **görevleri** veritabanı, hello Genişlet **öğeleri** koleksiyonu tıklatın **belgeleri**ve ardından **yeni belgeler**. 

   ![Yeni belgeler veri Gezgini'nde hello Azure portal oluşturun.](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-new-document.png)
  
2. Şimdi bir belge toohello Koleksiyonu Yapı izlenerek hello ile ekleyin.

     ```json
     {
         "id": "1",
         "category": "personal",
         "name": "groceries",
         "description": "Pick up apples and strawberries.",
         "isComplete": false
     }
     ```

3. Merhaba json toohello ekledikten sonra **belgeleri** sekmesini tıklatın, **kaydetmek**.

    ![JSON verileri kopyalayın ve Veri Gezgini'nde hello Azure portal Kaydet](./media/create-documentdb-dotnet/azure-cosmosdb-data-explorer-save-document.png)

4.  Oluştur ve Ekle burada hello için benzersiz bir değer bir daha fazla belgeyi kaydedin `id` özelliği ve diğer özellikleri uygun gördüğünüz şekilde hello Değiştir. Azure Cosmos DB, verilerinizin bir şemaya uygun olmasını şart koşmadığı için yeni belgelerinizin yapısını istediğiniz şekilde oluşturabilirsiniz.

     Veri Gezgini tooretrieve verilerinizi hello tıklayarak Sorguların kullandığı artık yapabilecekleriniz **filtresi Düzenle** ve **Filtre Uygula** düğmeler. Varsayılan olarak, Veri Gezgini kullanır `SELECT * FROM c` tooretrieve tüm belgeleri hello koleksiyonu, ancak siz o tooa farklı değiştirebilirsiniz [SQL sorgusu](documentdb-sql-query.md), gibi `SELECT * FROM c ORDER BY c._ts DESC`, azalan sırada tüm hello belgeleri temel alarak tooreturn kendi zaman damgası. 
 
     Ayrıca Veri Gezgini toocreate saklı yordamlar, UDF'ler ve Tetikleyicileri tooperform sunucu tarafı iş mantığı da kullanabilirsiniz ölçek işleme olarak. Veri Gezgini tüm hello yerleşik programlı veri erişim hello API'leri kullanılabilir gösterir, ancak tooyour verileri hello Azure portalında kolay erişim sağlar.

## <a name="clone-hello-sample-application"></a>Merhaba örnek uygulaması kopyalama

Şimdi şimdi koduyla tooworking geçin. Şimdi DocumentDB API uygulaması github'dan hello bağlantı dizesini ayarlamak ve çalıştırın kopyalayın. Ne kadar kolay toowork verilerle program aracılığıyla olduğunu görürsünüz. 

1. Git bash gibi bir git terminal penceresi açın ve `CD` tooa çalışma dizini.  

2. Çalışma hello aşağıdaki tooclone hello örnek depo komutu. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-java-getting-started.git
    ```

## <a name="review-hello-code"></a>Merhaba kod gözden geçirme

Neler olduğuna dair hello uygulamada hızlı bir gözden geçirme olalım. Açık hello `Program.java` dosya hello \src\GetStarted klasöründen ve hello Azure Cosmos DB kaynakları oluşturma bu kod satırları bulur. 

* Merhaba `DocumentClient` başlatılır.

    ```java
    this.client = new DocumentClient("https://FILLME.documents.azure.com",
            "FILLME", 
            new ConnectionPolicy(),
            ConsistencyLevel.Session);
    ```

* Yeni bir veritabanı oluşturulur.

    ```java
    Database database = new Database();
    database.setId(databaseName);
    
    this.client.createDatabase(database, null);
    ```

* Yeni bir koleksiyon oluşturulur.

    ```java
    DocumentCollection collectionInfo = new DocumentCollection();
    collectionInfo.setId(collectionName);

    ...

    this.client.createCollection(databaseLink, collectionInfo, requestOptions);
    ```

* Birkaç belge oluşturulur.

    ```java
    // Any Java object within your code can be serialized into JSON and written tooAzure Cosmos DB
    Family andersenFamily = new Family();
    andersenFamily.setId("Andersen.1");
    andersenFamily.setLastName("Andersen");
    // More properties

    String collectionLink = String.format("/dbs/%s/colls/%s", databaseName, collectionName);
    this.client.createDocument(collectionLink, family, new RequestOptions(), true);
    ```

* JSON üzerinden bir SQL sorgusu gerçekleştirilir.

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

## <a name="update-your-connection-string"></a>Bağlantı dizenizi güncelleştirme

Şimdi Azure portal tooget toohello bağlantı dizesi bilgilerinizi geri dönün ve hello uygulamaya kopyalayın. Bu, uygulama toocommunicate barındırılan veritabanınızla olanak tanır.

1. Merhaba, [Azure portal](http://portal.azure.com/), Azure Cosmos DB hesap, sol gezinti hello tıklatın **anahtarları**ve ardından **okuma-yazma anahtarları**. Merhaba Kopyala düğmesi hello sağ tarafındaki Merhaba ekranında toocopy hello URI ve birincil anahtar hello kullanacağınız `Program.java` hello sonraki adımda dosya.

    ![Görüntüleme ve kopyalama hello Azure portalına erişim tuşu, anahtarlar dikey penceresinde](./media/create-documentdb-dotnet/keys.png)

2. Merhaba açık olarak `Program.java` dosya, URI değeri (Merhaba Kopyala düğmesini kullanarak) hello Portal'dan kopyalayın ve hale hello hello uç nokta toohello DocumentClient oluşturucuda değerini `Program.java`. 

    `"https://FILLME.documents.azure.com"`

4. Sonra birincil anahtar değer hello Portal'dan kopyalayın ve "kolaylaştırarak FILLME", yapıştırın hello DocumentClient oluşturucuda ikinci parametre hello. Uygulamanızı şimdi güncelleştirdikten toocommunicate Azure Cosmos DB ile gerekli tüm hello bilgilerine sahip. 
    
## <a name="run-hello-app"></a>Merhaba uygulamayı çalıştırma

1. Penceresinde hello git terminal `cd` toohello azure-cosmos-db-documentdb-java-getting-started klasör.

2. Merhaba git terminal penceresinde yazın `mvn package` tooinstall hello Java paketleri gereklidir.

3. Merhaba git terminal penceresinde çalıştırın `mvn exec:java -D exec.mainClass=GetStarted.Program` içinde Java uygulamanız terminal penceresi toostart hello.

    Merhaba terminal penceresinde veritabanı oluşturuldu FamilyDB hello bildirim ve toopress anahtar toocontinue alırsınız. Bir anahtar toocreate hello veritabanı tuşuna basın, sonra toohello Veri Gezgini geçiş ve şimdi FamilyDB veritabanı içerdiği görürsünüz. Koleksiyon ve hello toopress anahtarları toocreate hello belgeleri devam ve bir sorgu gerçekleştirin. Merhaba Proje tamamlandığında hello kaynakları hesabınızdan silinir. 

    ![Görüntüleme ve kopyalama hello Azure portalına erişim tuşu, anahtarlar dikey penceresinde](./media/create-documentdb-java/console-output.png)


## <a name="review-slas-in-hello-azure-portal"></a>Gözden geçirme SLA'hello Azure portalı

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Kaynakları temizleme

Toocontinue toouse bu uygulamayı değil kullanacaksanız, bu hızlı başlangıç tarafından hello Azure portalında aşağıdaki adımları hello ile oluşturulan tüm kaynakları silin:

1. Merhaba sol taraftaki menüden hello Azure portal'ın, **kaynak grupları** ve ardından oluşturduğunuz hello kaynak hello adına tıklayın. 
2. Kaynak grubu sayfanızda tıklatın **silmek**hello metin kutusuna hello kaynak toodelete hello adını yazın ve ardından **silmek**.

## <a name="next-steps"></a>Sonraki adımlar

Bu hızlı başlangıç nasıl toocreate Azure Cosmos DB hesabınız, belge veritabanı ve hello Veri Gezgini'ni kullanarak ve bir uygulama toodo çalıştırın koleksiyonu aynısını program aracılığıyla hello öğrendiniz. Artık ek verileri tooyour Cosmos DB hesap içeri aktarabilirsiniz. 

> [!div class="nextstepaction"]
> [Azure Cosmos DB hesabınıza veri aktarma](import-data.md)


