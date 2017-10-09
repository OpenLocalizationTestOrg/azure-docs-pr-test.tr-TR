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
# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-java-and-hello-azure-portal"></a>Azure Cosmos DB: Java ile MongoDB API konsol uygulaması oluşturma ve Azure portal hello

Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir. Hızlı bir şekilde oluşturmak ve belge, anahtar/değer ve grafik veritabanları, her biri hello genel dağıtım ve yatay ölçek özelliklerini Azure Cosmos DB'nin hello çekirdek yararlı sorgulayabilirsiniz. 

Bu hızlı başlangıç nasıl toocreate Azure Cosmos DB hesabınız, belge veritabanı ve koleksiyonu kullanarak Azure portalında hello gösterir. Daha sonra yapı ve hello üzerinde oluşturulmuş bir konsol uygulaması dağıtma [MongoDB Java sürücü](https://docs.mongodb.com/ecosystem/drivers/java/). 

## <a name="prerequisites"></a>Ön koşullar

* Bu örneği çalıştırmadan önce aşağıdaki önkoşullar hello sahip olmanız gerekir:
   * JDK 1.7+ (JDK yoksa `apt-get install default-jdk` komutunu çalıştırın)
   * Maven (Maven yoksa `apt-get install maven` komutunu çalıştırın)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Veritabanı hesabı oluşturma

[!INCLUDE [mongodb-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="add-a-collection"></a>Koleksiyon ekleme

Yeni veritabanınıza **db**, yeni koleksiyonunuza da **coll** adını verin.

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a>Merhaba örnek uygulaması kopyalama

Artık şimdi github, kopya bir MongoDB API uygulamasını hello bağlantı dizesini ayarlamak ve çalıştırın. Ne kadar kolay toowork verilerle program aracılığıyla olduğunu görürsünüz. 

1. Git bash gibi bir git terminal penceresi açın ve `cd` tooa çalışma dizini.  

2. Çalışma hello aşağıdaki tooclone hello örnek depo komutu. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-java-getting-started.git
    ```

3. Ardından Visual Studio'da hello çözüm dosyasını açın. 

## <a name="review-hello-code"></a>Merhaba kod gözden geçirme

Neler olduğuna dair hello uygulamada hızlı bir gözden geçirme olalım. Açık hello `Program.cs` dosyanız varsa ve bulabileceğiniz bu kod satırları hello Azure Cosmos DB kaynakları oluşturun. 

* Merhaba DocumentClient başlatılır.

    ```java
    MongoClientURI uri = new MongoClientURI("FILLME");`

    MongoClient mongoClient = new MongoClient(uri);            
    ```

* Yeni bir veritabanı ve koleksiyonu oluşturulur.

    ```java
    MongoDatabase database = mongoClient.getDatabase("db");

    MongoCollection<Document> collection = database.getCollection("coll");
    ```

* `MongoCollection.insertOne` kullanılarak birkaç belge eklenir

    ```java
    Document document = new Document("fruit", "apple")
    collection.insertOne(document);
    ```

* `MongoCollection.find` kullanılarak birkaç sorgu gerçekleştirilir

    ```java
    Document queryResult = collection.find(Filters.eq("fruit", "apple")).first();
    System.out.println(queryResult.toJson());       
    ```

## <a name="update-your-connection-string"></a>Bağlantı dizenizi güncelleştirme

Şimdi Azure portal tooget toohello bağlantı dizesi bilgilerinizi geri dönün ve hello uygulamaya kopyalayın.

1. Hello ifadesini hesabı seçin **Hızlı Başlangıç**Java seçin, ardından hello bağlantı dizesi tooyour Panoya Kopyala

2. Açık hello `Program.java` dosya, hello bağımsız değişkeni toohello MongoClientURI Oluşturucusu hello bağlantı dizesi ile değiştirin. Uygulamanızı şimdi güncelleştirdikten toocommunicate Azure Cosmos DB ile gerekli tüm hello bilgilerine sahip. 
    
## <a name="run-hello-console-app"></a>Merhaba konsol uygulamasını çalıştırın

1. Çalıştırma `mvn package` npm modülleri içinde terminal tooinstall gerekli

2. Çalıştırma `mvn exec:java -D exec.mainClass=GetStarted.Program` terminal toostart içinde Java uygulaması.

Artık kullanabilirsiniz [Robomongo](mongodb-robomongo.md) / [Studio 3T](mongodb-mongochef.md) tooquery, değiştirebilir ve bu yeni verilerle çalışma.

## <a name="review-slas-in-hello-azure-portal"></a>Gözden geçirme SLA'hello Azure portalı

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Kaynakları temizleme

Toocontinue toouse bu uygulamayı değil kullanacaksanız, bu hızlı başlangıç tarafından hello Azure portalında aşağıdaki adımları hello ile oluşturulan tüm kaynakları silin:

1. Merhaba sol taraftaki menüden hello Azure portal'ın, **kaynak grupları** ve ardından oluşturduğunuz hello kaynak hello adına tıklayın. 
2. Kaynak grubu sayfanızda tıklatın **silmek**hello metin kutusuna hello kaynak toodelete hello adını yazın ve ardından **silmek**.

## <a name="next-steps"></a>Sonraki adımlar

Bu hızlı başlangıç nasıl toocreate bir Azure Cosmos DB hesap hello Veri Gezgini'ni kullanarak bir koleksiyon oluşturun ve bir konsol uygulaması çalıştırın öğrendiniz. Artık ek verileri tooyour Cosmos DB hesap içeri aktarabilirsiniz. 

> [!div class="nextstepaction"]
> [Azure Cosmos DB’ye MongoDB verileri aktarma](mongodb-migrate.md)


