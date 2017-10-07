---
title: "bir Azure Cosmos DB .NET uygulaması kullanarak aaaBuild hello grafik API'si | Microsoft Docs"
description: "Tooconnect tooand kullanabileceğiniz bir .NET kod örnek sorgu Azure Cosmos DB sunar"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: daacbabf-1bb5-497f-92db-079910703046
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/28/2017
ms.author: denlee
ms.openlocfilehash: f28790fcb8c9f57c7bb3d844d8276fa04abcc39c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-net-application-using-hello-graph-api"></a>Azure Cosmos DB: hello grafik API'sini kullanarak bir .NET uygulaması oluşturma

Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir. Hızlı bir şekilde oluşturmak ve belge, anahtar/değer ve grafik veritabanları, her biri hello genel dağıtım ve yatay ölçek özelliklerini Azure Cosmos DB'nin hello çekirdek yararlı sorgulayabilirsiniz. 

Bu hızlı başlangıç nasıl toocreate bir Azure Cosmos DB hesap, veritabanı ve grafik (kapsayıcı) kullanarak Azure portalında hello gösterir. Ardından derlemeyi ve çalıştırmayı hello üzerinde oluşturulmuş bir konsol uygulaması [grafik API'si](graph-sdk-dotnet.md) (Önizleme).  

## <a name="prerequisites"></a>Ön koşullar

Visual Studio yüklü 2017 zaten sahip değilseniz, indirin ve hello kullan **ücretsiz** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/). Etkinleştirdiğinizden emin olun **Azure geliştirme** hello Visual Studio Kurulumu sırasında.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Veritabanı hesabı oluşturma

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a>Grafik ekleme

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-hello-sample-application"></a>Merhaba örnek uygulaması kopyalama

Artık şimdi kopya grafik API'si uygulama github'dan hello bağlantı dizesini ayarlamak ve çalıştırın. Ne kadar kolay toowork verilerle program aracılığıyla olduğunu görürsünüz. 

1. Git bash gibi bir git terminal penceresi açın ve `cd` tooa çalışma dizini.  

2. Çalışma hello aşağıdaki tooclone hello örnek depo komutu. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-dotnet-getting-started.git
    ```

3. Ardından Visual Studio ve açık hello çözüm dosyasını açın. 

## <a name="review-hello-code"></a>Merhaba kod gözden geçirme

Neler olduğuna dair hello uygulamada hızlı bir gözden geçirme olalım. Bu kod satırları hello Azure Cosmos DB kaynakları oluşturun, açık hello Program.cs dosyasının ve bulabilirsiniz. 

* Merhaba DocumentClient başlatılır. Merhaba önizlemede hello Azure Cosmos DB istemcide bir grafik uzantısı API eklediğimiz. Hello Azure Cosmos DB istemci ve kaynakları ayrılmış bir tek başına grafik istemci üzerinde çalışıyoruz.

    ```csharp
    using (DocumentClient client = new DocumentClient(
        new Uri(endpoint),
        authKey,
        new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp }))
    ```

* Yeni bir veritabanı oluşturulur.

    ```csharp
    Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" });
    ```

* Yeni bir grafik oluşturulur.

    ```csharp
    DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync(
        UriFactory.CreateDatabaseUri("graphdb"),
        new DocumentCollection { Id = "graph" },
        new RequestOptions { OfferThroughput = 1000 });
    ```
* Bir dizi Gremlin adımı hello kullanarak yürütülme `CreateGremlinQuery` yöntemi.

    ```csharp
    // hello CreateGremlinQuery method extensions allow you tooexecute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, "g.V().count()");
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    ```

## <a name="update-your-connection-string"></a>Bağlantı dizenizi güncelleştirme

Şimdi Azure portal tooget toohello bağlantı dizesi bilgilerinizi geri dönün ve hello uygulamaya kopyalayın.

1. Visual Studio 2017 içinde hello App.config dosyasını açın. 

2. Hello Azure Cosmos DB hesabınızdaki Azure portal'ı tıklatın **anahtarları** sol gezinti hello içinde. 

    ![Görüntüleyin ve bir birincil anahtar hello hello anahtarları sayfasında Azure portalı kopyalayın](./media/create-graph-dotnet/keys.png)

3. Kopyalama, **URI** değer hello portalından ve hale hello App.config hello uç nokta anahtar değeri. Ekran görüntüsü toocopy hello değeri önceki hello gösterildiği gibi hello Kopyala düğmesini kullanabilirsiniz.

    `<add key="Endpoint" value="https://FILLME.documents.azure.com:443" />`

4. Kopyalama, **birincil anahtar** değer hello portalından ve hale hello App.Config'de hello AuthKey anahtarının değerini sonra yaptığınız değişiklikleri kaydedin. 

    `<add key="AuthKey" value="FILLME" />`

Uygulamanızı şimdi güncelleştirdikten toocommunicate Azure Cosmos DB ile gerekli tüm hello bilgilerine sahip. 

## <a name="run-hello-console-app"></a>Merhaba konsol uygulamasını çalıştırın

1. Visual Studio'da hello üzerinde sağ **GraphGetStarted** proje **Çözüm Gezgini** ve ardından **NuGet paketlerini Yönet**. 

2. Merhaba NuGet içinde **Gözat** kutusuna *Microsoft.Azure.Graphs* ve hello denetleyin **içeren yayın öncesi** kutusu. 

3. Merhaba sonuçlarından hello yüklemek **Microsoft.Azure.Graphs** kitaplığı. Bu, hello Azure Cosmos DB grafik uzantısı kitaplık paketi ve tüm bağımlılıkları yükler.

    Değişiklikleri toohello çözümü gözden geçirme hakkında bir ileti alırsanız tıklatın **Tamam**. Lisans kabulü hakkında bir ileti alırsanız **Kabul ediyorum**'a tıklayın.

4. CTRL + F5'e tıklayın toorun Merhaba uygulaması.

   Merhaba konsol penceresinde hello köşeleri ve toohello grafik eklenmekte olan kenarları görüntüler. Merhaba betik tamamlandığında, ENTER tuşuna iki kez tooclose hello konsol penceresi. 

## <a name="browse-using-hello-data-explorer"></a>Merhaba Veri Gezgini'ni kullanarak Gözat

Şimdi tooData Explorer hello Azure portal, geri dönün ve da göz atın ve yeni grafik verileri sorgulayabilirsiniz.

1. Veri Gezgini'nde hello yeni veritabanı hello grafikleri bölmesinde görüntülenir. **graphdb**, **graphcollz** öğelerini genişletip **Grafik** öğesine tıklayın.

2. Merhaba tıklatın **Filtre Uygula** düğmesini toouse hello varsayılan sorgu tooview hello Grafikteki tüm hello verticies. Merhaba örnek uygulama tarafından oluşturulan hello veri hello grafikleri bölmesinde görüntülenir.

    Merhaba grafik ve bu moddan yakınlaştırabilirsiniz, hello grafik görüntü alanını genişletin, ek verticies ekleyin ve verticies hello üzerinde yüzeyini görüntülemek taşıma.

    ![Görünüm hello grafikte veri Explorer'da hello Azure portalı](./media/create-graph-dotnet/graph-explorer.png)

## <a name="review-slas-in-hello-azure-portal"></a>Gözden geçirme SLA'hello Azure portalı

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Kaynakları temizleme

Toocontinue toouse bu uygulamayı değil kullanacaksanız, bu hızlı başlangıç tarafından hello Azure portalında aşağıdaki adımları hello ile oluşturulan tüm kaynakları silin: 

1. Merhaba sol taraftaki menüden hello Azure portal'ın, **kaynak grupları** ve ardından oluşturduğunuz hello kaynak hello adına tıklayın. 
2. Kaynak grubu sayfanızda tıklatın **silmek**hello metin kutusuna hello kaynak toodelete hello adını yazın ve ardından **silmek**.

## <a name="next-steps"></a>Sonraki adımlar

Bu hızlı başlangıç toocreate bir Azure Cosmos DB hesap hello Veri Gezgini'ni kullanarak bir grafik oluşturma ve bir uygulama çalıştırmasına öğrendiniz. Artık daha karmaşık sorgular oluşturabilir ve Gremlin kullanarak güçlü grafik geçişi mantığını kullanabilirsiniz. 

> [!div class="nextstepaction"]
> [Gremlin kullanarak sorgulama](tutorial-query-graph.md)

