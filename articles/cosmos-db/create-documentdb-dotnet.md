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
# <a name="azure-cosmos-db-build-a-documentdb-api-web-app-with-net-and-hello-azure-portal"></a>Azure Cosmos DB: .NET ile DocumentDB API web uygulaması oluşturma ve Azure portal hello

Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir. Hızlı bir şekilde oluşturmak ve belge, anahtar/değer ve grafik veritabanları, her biri hello genel dağıtım ve yatay ölçek özelliklerini Azure Cosmos DB'nin hello çekirdek yararlı sorgulayabilirsiniz. 

Bu hızlı başlangıç nasıl toocreate Azure Cosmos DB hesabınız, belge veritabanı ve koleksiyonu kullanarak Azure portalında hello gösterir. Daha sonra yapı ve hello üzerinde oluşturulmuş bir Yapılacaklar listesi web uygulaması dağıtma [DocumentDB .NET API](documentdb-sdk-dotnet.md)hello ekran aşağıdaki gösterildiği gibi. 

![Yapılacaklar listesi uygulaması ve örnek veriler](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

## <a name="prerequisites"></a>Ön koşullar

Visual Studio yüklü 2017 zaten sahip değilseniz, indirin ve hello kullan **ücretsiz** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/). Etkinleştirdiğinizden emin olun **Azure geliştirme** hello Visual Studio Kurulumu sırasında.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a>Veritabanı hesabı oluşturma

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

<a id="create-collection"></a>
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

     Artık, verilerinizi Veri Gezgini tooretrieve sorgularda kullanabilirsiniz. Varsayılan olarak, Veri Gezgini kullanır `SELECT * FROM c` tooretrieve tüm belgeleri hello koleksiyonu, ancak siz o tooa farklı değiştirebilirsiniz [SQL sorgusu](documentdb-sql-query.md), gibi `SELECT * FROM c ORDER BY c._ts DESC`, azalan sırada tüm hello belgeleri temel alarak tooreturn kendi zaman damgası.
 
     Ayrıca Veri Gezgini toocreate saklı yordamlar, UDF'ler ve Tetikleyicileri tooperform sunucu tarafı iş mantığı da kullanabilirsiniz ölçek işleme olarak. Veri Gezgini tüm hello yerleşik programlı veri erişim hello API'leri kullanılabilir gösterir, ancak tooyour verileri hello Azure portalında kolay erişim sağlar.

## <a name="clone-hello-sample-application"></a>Merhaba örnek uygulaması kopyalama

Şimdi şimdi koduyla tooworking geçin. Şimdi DocumentDB API uygulaması github'dan hello bağlantı dizesini ayarlamak ve çalıştırın kopyalayın. Ne kadar kolay toowork verilerle program aracılığıyla olduğunu görürsünüz. 

1. Git bash gibi bir git terminal penceresi açın ve `CD` tooa çalışma dizini.  

2. Çalışma hello aşağıdaki tooclone hello örnek depo komutu. 

    ```bash
    git clone https://github.com/Azure-Samples/documentdb-dotnet-todo-app.git
    ```

3. Ardından Visual Studio'da hello Yapılacaklar çözüm dosyasını açın. 

## <a name="review-hello-code"></a>Merhaba kod gözden geçirme

Neler olduğuna dair hello uygulamada hızlı bir gözden geçirme olalım. Açık hello DocumentDBRepository.cs dosyanız varsa ve bu kod satırları hello Azure Cosmos DB kaynakları oluşturma bulabilirsiniz. 

* Merhaba DocumentClient 73 satırda başlatılır.

    ```csharp
    client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);`
    ```

* 88 satırda yeni bir veritabanı oluşturulur.

    ```csharp
    await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
    ```

* 107 satırda yeni bir koleksiyon oluşturulur.

    ```csharp
    await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(DatabaseId),
        new DocumentCollection { Id = CollectionId },
        new RequestOptions { OfferThroughput = 1000 });
    ```

## <a name="update-your-connection-string"></a>Bağlantı dizenizi güncelleştirme

Şimdi Azure portal tooget toohello bağlantı dizesi bilgilerinizi geri dönün ve hello uygulamaya kopyalayın.

1. Merhaba, [Azure portal](http://portal.azure.com/), Azure Cosmos DB hesap, sol gezinti hello tıklatın **anahtarları**ve ardından **okuma-yazma anahtarları**. Merhaba sonraki adımda hello web.config dosyasına hello Kopyala düğmesi hello sağ tarafında Merhaba ekranında toocopy hello URI ve birincil anahtar kullanacaksınız.

    ![Görüntüleme ve kopyalama hello Azure portalına erişim tuşu, anahtarlar dikey penceresinde](./media/create-documentdb-dotnet/keys.png)

2. Visual Studio 2017 içinde hello web.config dosyasını açın. 

3. URI değeri (Merhaba Kopyala düğmesini kullanarak) hello Portal'dan kopyalayın ve hale hello web.config dosyasında hello uç nokta anahtar değeri. 

    `<add key="endpoint" value="FILLME" />`

4. Sonra birincil anahtar değer hello Portal'dan kopyalayın ve kolaylaştırır hello hello authKey web.config dosyasındaki değeri. Uygulamanızı şimdi güncelleştirdikten toocommunicate Azure Cosmos DB ile gerekli tüm hello bilgilerine sahip. 

    `<add key="authKey" value="FILLME" />`
    
## <a name="run-hello-web-app"></a>Merhaba web uygulaması çalıştırın
1. Visual Studio'da hello projeye sağ tıklayın **Çözüm Gezgini** ve ardından **NuGet paketlerini Yönet**. 

2. Merhaba NuGet içinde **Gözat** kutusuna *DocumentDB*.

3. Merhaba sonuçlarından hello yüklemek **Microsoft.Azure.DocumentDB** kitaplığı. Bu, tüm bağımlılıkları yanı sıra hello Microsoft.Azure.DocumentDB paketi yükler.

4. CTRL + F5'e tıklayın toorun Merhaba uygulaması. Uygulamanız tarayıcınızda görüntülenir. 

5. Tıklatın **Yeni Oluştur** hello tarayıcı ve yapılacaklar uygulamanızda birkaç yeni görevler oluşturabilir.

   ![Yapılacaklar listesi uygulaması ve örnek veriler](./media/create-documentdb-dotnet/azure-comosdb-todo-app-list.png)

Şimdi tooData Explorer geri dönün ve sorgu görmek değiştirmek ve bu yeni verilerle çalışmak. 

## <a name="review-slas-in-hello-azure-portal"></a>Gözden geçirme SLA'hello Azure portalı

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Kaynakları temizleme

Toocontinue toouse bu uygulamayı değil kullanacaksanız, bu hızlı başlangıç tarafından hello Azure portalında aşağıdaki adımları hello ile oluşturulan tüm kaynakları silin:

1. Merhaba sol taraftaki menüden hello Azure portal'ın, **kaynak grupları** ve ardından oluşturduğunuz hello kaynak hello adına tıklayın. 
2. Kaynak grubu sayfanızda tıklatın **silmek**hello metin kutusuna hello kaynak toodelete hello adını yazın ve ardından **silmek**.

## <a name="next-steps"></a>Sonraki adımlar

Bu hızlı başlangıç toocreate bir Azure Cosmos DB hesap hello Veri Gezgini'ni kullanarak bir koleksiyon oluşturma ve bir web uygulamasını çalıştırmak öğrendiniz. Artık ek verileri tooyour Cosmos DB hesap içeri aktarabilirsiniz. 

> [!div class="nextstepaction"]
> [Azure Cosmos DB hesabınıza veri aktarma](import-data.md)


