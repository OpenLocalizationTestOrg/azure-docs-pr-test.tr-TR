---
title: "Azure Cosmos DB: Node.js ile uygulama oluşturma ve DocumentDB API hello | Microsoft Docs"
description: "Tooconnect tooand sorgu kullanabileceğiniz bir Node.js kodu örneği hello Azure Cosmos DB DocumentDB API sunar"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 9c0f033c-240e-4fee-8421-08907231087f
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: hero-article
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 287d860c7d6f788f05a397b238ef0f841c3c30ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-nodejs-and-hello-azure-portal"></a>Azure Cosmos DB: Node.js ile DocumentDB API uygulaması oluşturma ve Azure portal hello

Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir. Hızlı bir şekilde oluşturmak ve belge, anahtar/değer ve grafik veritabanları, her biri hello genel dağıtım ve yatay ölçek özelliklerini Azure Cosmos DB'nin hello çekirdek yararlı sorgulayabilirsiniz. 

Bu hızlı başlangıç nasıl toocreate Azure Cosmos DB hesabınız, belge veritabanı ve koleksiyonu kullanarak Azure portalında hello gösterir. Ardından derlemeyi ve çalıştırmayı hello üzerinde oluşturulmuş bir konsol uygulaması [DocumentDB Node.js API](documentdb-sdk-node.md).

## <a name="prerequisites"></a>Ön koşullar

* Bu örneği çalıştırmadan önce aşağıdaki önkoşullar hello sahip olmanız gerekir:
    * [Node.js](https://nodejs.org/en/) sürüm v0.10.29 veya üzeri
    * [Git](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Veritabanı hesabı oluşturma

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Koleksiyon ekleme

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a>Merhaba örnek uygulaması kopyalama

Artık şimdi github, kopya bir DocumentDB API uygulamasını hello bağlantı dizesini ayarlamak ve çalıştırın. Ne kadar kolay toowork verilerle program aracılığıyla olduğunu görürsünüz. 

1. Git bash gibi bir git terminal penceresi açın ve `CD` tooa çalışma dizini.  

2. Çalışma hello aşağıdaki tooclone hello örnek depo komutu. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-nodejs-getting-started.git
    ```

## <a name="review-hello-code"></a>Merhaba kod gözden geçirme

Neler olduğuna dair hello uygulamada hızlı bir gözden geçirme olalım. Açık hello `app.js` dosyanız varsa ve bulma Bu kod satırları hello Azure Cosmos DB kaynakları oluşturun. 

* Merhaba `documentClient` başlatılır.

    ```nodejs
    var client = new documentClient(config.endpoint, { "masterKey": config.primaryKey });
    ```

* Yeni bir veritabanı oluşturulur.

    ```nodejs
    client.createDatabase(config.database, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* Yeni bir koleksiyon oluşturulur.

    ```nodejs
    client.createCollection(databaseUrl, config.collection, { offerThroughput: 400 }, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* Birkaç belge oluşturulur.

    ```nodejs
    client.createDocument(collectionUrl, document, (err, created) => {
        if (err) reject(err)
        else resolve(created);
    });
    ```

* JSON üzerinden bir SQL sorgusu gerçekleştirilir.

    ```nodejs
    client.queryDocuments(
        collectionUrl,
        'SELECT VALUE r.children FROM root r WHERE r.lastName = "Andersen"'
    ).toArray((err, results) => {
        if (err) reject(err)
        else {
            for (var queryResult of results) {
                let resultString = JSON.stringify(queryResult);
                console.log(`\tQuery returned ${resultString}`);
            }
            console.log();
            resolve(results);
        }
    });
    ```    

## <a name="update-your-connection-string"></a>Bağlantı dizenizi güncelleştirme

Şimdi Azure portal tooget toohello bağlantı dizesi bilgilerinizi geri dönün ve hello uygulamaya kopyalayın.

1. Merhaba, [Azure portal](http://portal.azure.com/), Azure Cosmos DB hesap, sol gezinti hello tıklatın **anahtarları**ve ardından **okuma-yazma anahtarları**. Merhaba Kopyala düğmesi hello sağ tarafındaki Merhaba ekranında toocopy hello URI ve birincil anahtar hello kullanacağınız `config.js` hello sonraki adımda dosya.

    ![Görüntüleme ve kopyalama hello Azure portalına erişim tuşu, anahtarlar dikey penceresinde](./media/create-documentdb-dotnet/keys.png)

2. Açık hello içinde `config.js` dosya. 

3. URI değeri (Merhaba Kopyala düğmesini kullanarak) hello Portal'dan kopyalayın ve hale hello hello uç noktası anahtarı değerini `config.js`. 

    `config.endpoint = "https://FILLME.documents.azure.com"`

4. Sonra birincil anahtar değer hello Portal'dan kopyalayın ve kolaylaştırır hello hello değerini `config.primaryKey` içinde `config.js`. Uygulamanızı şimdi güncelleştirdikten toocommunicate Azure Cosmos DB ile gerekli tüm hello bilgilerine sahip. 

    `config.primaryKey "FILLME"`
    
## <a name="run-hello-app"></a>Merhaba uygulamayı çalıştırma
1. Çalıştırma `npm install` npm modülleri içinde terminal tooinstall gerekli

2. Çalıştırma `node app.js` terminal toostart içinde düğüm uygulamanızı.

Şimdi tooData Explorer geri dönün ve sorgu görmek değiştirmek ve bu yeni verilerle çalışmak. 

## <a name="review-slas-in-hello-azure-portal"></a>Gözden geçirme SLA'hello Azure portalı

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Kaynakları temizleme

Toocontinue toouse bu uygulamayı değil kullanacaksanız, bu hızlı başlangıç tarafından hello Azure portalında aşağıdaki adımları hello ile oluşturulan tüm kaynakları silin:

1. Merhaba sol taraftaki menüden hello Azure portal'ın, **kaynak grupları** ve ardından oluşturduğunuz hello kaynak hello adına tıklayın. 
2. Kaynak grubu sayfanızda tıklatın **silmek**hello metin kutusuna hello kaynak toodelete hello adını yazın ve ardından **silmek**.

## <a name="next-steps"></a>Sonraki adımlar

Bu hızlı başlangıç toocreate bir Azure Cosmos DB hesap hello Veri Gezgini'ni kullanarak bir koleksiyon oluşturma ve bir uygulama çalıştırmasına öğrendiniz. Artık ek verileri tooyour Cosmos DB hesap içeri aktarabilirsiniz. 

> [!div class="nextstepaction"]
> [Azure Cosmos DB hesabınıza veri aktarma](import-data.md)


