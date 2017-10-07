---
title: "Azure Cosmos DB: .NET ile bir web uygulaması oluşturma ve API MongoDB hello | Microsoft Docs"
description: "Tooconnect tooand sorgu kullanabileceğiniz bir .NET kod örneği hello Azure Cosmos DB MongoDB API sunar"
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
ms.openlocfilehash: c85cc47f772a19aaa7181611b75a8acaedbc4c42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-mongodb-api-web-app-with-net-and-hello-azure-portal"></a>Azure Cosmos DB: .NET ile MongoDB API web uygulaması oluşturma ve Azure portal hello

Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir. Hızlı bir şekilde oluşturmak ve belge, anahtar/değer ve grafik veritabanları, her biri hello genel dağıtım ve yatay ölçek özelliklerini Azure Cosmos DB'nin hello çekirdek yararlı sorgulayabilirsiniz. 

Bu hızlı başlangıç nasıl toocreate Azure Cosmos DB hesabınız, belge veritabanı ve koleksiyonu kullanarak Azure portalında hello gösterir. Daha sonra yapı ve hello üzerinde oluşturulmuş bir görevler listesi web uygulaması dağıtma [MongoDB .NET sürücü](https://docs.mongodb.com/ecosystem/drivers/csharp/). 

## <a name="prerequisites"></a>Ön koşullar

Visual Studio yüklü 2017 zaten sahip değilseniz, indirin ve hello kullan **ücretsiz** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/). Etkinleştirdiğinizden emin olun **Azure geliştirme** hello Visual Studio Kurulumu sırasında.
[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

<a id="create-account"></a>
## <a name="create-a-database-account"></a>Veritabanı hesabı oluşturma

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-hello-sample-application"></a>Merhaba örnek uygulaması kopyalama

Artık şimdi github, kopya bir MongoDB API uygulamasını hello bağlantı dizesini ayarlamak ve çalıştırın. Ne kadar kolay toowork verilerle program aracılığıyla olduğunu görürsünüz. 

1. Git bash gibi bir git terminal penceresi açın ve `cd` tooa çalışma dizini.  

2. Çalışma hello aşağıdaki tooclone hello örnek depo komutu. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-dotnet-getting-started.git
    ```

3. Ardından Visual Studio'da hello çözüm dosyasını açın. 

## <a name="review-hello-code"></a>Merhaba kod gözden geçirme

Neler olduğuna dair hello uygulamada hızlı bir gözden geçirme olalım. Açık hello **Dal.cs** dosyasını hello altında **DAL** dizin ve bulabileceğiniz bu kod satırları hello Azure Cosmos DB kaynakları oluşturun. 

* Merhaba Mongo istemci başlatır.

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

* Merhaba veritabanı ve hello koleksiyonu alır.

    ```cs
    private string dbName = "Tasks";
    private string collectionName = "TasksList";

    var database = client.GetDatabase(dbName);
    var todoTaskCollection = database.GetCollection<MyTask>(collectionName);
    ```

* Tüm belgeleri alın.

    ```cs
    collection.Find(new BsonDocument()).ToList();
    ```

## <a name="update-your-connection-string"></a>Bağlantı dizenizi güncelleştirme

Şimdi Azure portal tooget toohello bağlantı dizesi bilgilerinizi geri dönün ve hello uygulamaya kopyalayın.

1. Merhaba, [Azure portal](http://portal.azure.com/), Azure Cosmos DB hesap, sol gezinti hello tıklatın **bağlantı dizesi**ve ardından **okuma-yazma anahtarları**. Merhaba sonraki adımda hello Dal.cs dosyasına hello Kopyala düğmesi hello sağ tarafında Merhaba ekranında toocopy hello kullanıcı adı, parola ve ana bilgisayar kullanacaksınız.

2. Açık hello **Dal.cs** hello dosyasında **DAL** dizin. 

3. Kopyalama, **kullanıcıadı** değeri (Merhaba Kopyala düğmesini kullanarak) hello portalından ve hale hello hello değerini **kullanıcı adı** içinde **Dal.cs** dosya. 

4. Daha sonra kopyalayın, **konak** değer hello portalından ve yapmak hello hello değerini **konak** içinde **Dal.cs** dosya. 

5. Son olarak kopyalamak, **parola** değer hello portalından ve hale hello hello değerini **parola** içinde **Dal.cs** dosya. 

Uygulamanızı şimdi güncelleştirdikten toocommunicate Azure Cosmos DB ile gerekli tüm hello bilgilerine sahip. 
    
## <a name="run-hello-web-app"></a>Merhaba web uygulaması çalıştırın

1. Visual Studio'da hello projeye sağ tıklayın **Çözüm Gezgini** ve ardından **NuGet paketlerini Yönet**. 

2. Merhaba NuGet içinde **Gözat** kutusuna *MongoDB.Driver*.

3. Merhaba sonuçlarından hello yüklemek **MongoDB.Driver** kitaplığı. Bu, tüm bağımlılıkları yanı sıra hello MongoDB.Driver paketi yükler.

4. CTRL + F5'e tıklayın toorun Merhaba uygulaması. Uygulamanız tarayıcınızda görüntülenir. 

5. Tıklatın **oluşturma** hello tarayıcı ve görev listesi uygulamanızda birkaç yeni görevler oluşturabilir.

## <a name="review-slas-in-hello-azure-portal"></a>Gözden geçirme SLA'hello Azure portalı

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Kaynakları temizleme

Toocontinue toouse bu uygulamayı değil kullanacaksanız, bu hızlı başlangıç tarafından hello Azure portalında aşağıdaki adımları hello ile oluşturulan tüm kaynakları silin:

1. Merhaba sol taraftaki menüden hello Azure portal'ın, **kaynak grupları** ve ardından oluşturduğunuz hello kaynak hello adına tıklayın. 
2. Kaynak grubu sayfanızda tıklatın **silmek**hello metin kutusuna hello kaynak toodelete hello adını yazın ve ardından **silmek**.

## <a name="next-steps"></a>Sonraki adımlar

Bu hızlı başlangıç nasıl toocreate bir Azure Cosmos DB hesap ve bir web uygulamasını kullanarak çalışma MongoDB için API hello öğrendiniz. Artık ek verileri tooyour Cosmos DB hesap içeri aktarabilirsiniz. 

> [!div class="nextstepaction"]
> [Merhaba MongoDB API Azure Cosmos Veritabanına veri alma](mongodb-migrate.md)

