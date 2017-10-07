---
title: aaaBuild grafik API'sini kullanarak Azure Cosmos DB Node.js uygulama | Microsoft Docs
description: "Tooconnect tooand kullanabileceğiniz bir Node.js kodu örnek sorgu Azure Cosmos DB sunar"
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
ms.date: 07/14/2017
ms.author: denlee
ms.openlocfilehash: 1445755842bc4e4a84ca2b2f789aadde8467e190
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-nodejs-application-by-using-graph-api"></a>Azure Cosmos DB: Grafik API'sini kullanarak bir Node.js uygulaması oluşturma

Azure Cosmos DB hello Genel dağıtılmış birden çok model veritabanı Microsoft'tan hizmetidir. Hızlı bir şekilde oluşturmak ve belge, anahtar/değer ve grafik veritabanları, her biri hello genel dağıtım ve yatay ölçek özelliklerini Azure Cosmos DB'nin hello çekirdek yararlı sorgulayabilirsiniz. 

Bu hızlı başlangıç makalede nasıl toocreate bir Azure Cosmos DB hesap grafik API'si (Önizleme), veritabanı ve grafik hello Azure portal kullanarak gösterilmektedir. Ardından derleme ve hello açık kaynaklı kullanarak bir konsol uygulaması çalıştırma [Gremlin Node.js](https://www.npmjs.com/package/gremlin-secure) sürücü.  

> [!NOTE]
> Merhaba npm modülünü `gremlin-secure` değiştirilmiş bir sürümüdür `gremlin` modülüyle SSL ve Azure Cosmos DB ile bağlanmak için gereken SASL desteği. Kaynak kodu [GitHub](https://github.com/CosmosDB/gremlin-javascript)’dan edinilebilir.
>

## <a name="prerequisites"></a>Ön koşullar

Bu örneği çalıştırmadan önce aşağıdaki önkoşullar hello sahip olmanız gerekir:
* [Node.js](https://nodejs.org/en/) v0.10.29 sürümü veya sonraki bir sürüm
* [Git](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Veritabanı hesabı oluşturma

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a>Grafik ekleme

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-hello-sample-application"></a>Merhaba örnek uygulaması kopyalama

Artık şimdi kopya grafik API'si uygulama github'dan hello bağlantı dizesini ayarlamak ve çalıştırın. Ne kadar kolay toowork verilerle program aracılığıyla olduğunu görürsünüz. 

1. Git Bash gibi bir Git terminal penceresi açın ve değiştirme (aracılığıyla `cd` komutu) tooa çalışma dizini.  

2. Çalışma hello aşağıdaki tooclone hello örnek depo komutu. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-nodejs-getting-started.git
    ```

3. Visual Studio'da Hello çözüm dosyasını açın. 

## <a name="review-hello-code"></a>Merhaba kod gözden geçirme

Neler olduğuna dair hello uygulamada hızlı bir gözden geçirme olalım. Açık hello `app.js` dosyasını ve kod satırı aşağıdaki hello bulabilirsiniz. 

* Merhaba Gremlin istemci oluşturulur.

    ```nodejs
    const client = Gremlin.createClient(
        443, 
        config.endpoint, 
        { 
            "session": false, 
            "ssl": true, 
            "user": `/dbs/${config.database}/colls/${config.collection}`,
            "password": config.primaryKey
        });
    ```

  Merhaba tümünü bağlantılardır `config.js`, hangi biz bölümden hello düzenleyin.

* Bir dizi Gremlin adımı ile Merhaba yürütülme `client.execute` yöntemi.

    ```nodejs
    console.log('Running Count'); 
    client.execute("g.V().count()", { }, (err, results) => {
        if (err) return console.error(err);
        console.log(JSON.stringify(results));
        console.log();
    });
    ```

## <a name="update-your-connection-string"></a>Bağlantı dizenizi güncelleştirme

1. Açık hello config.js dosyası. 

2. Config.js içinde hello config.endpoint hello anahtarla doldurun **Gremlin URI** başlangıç değerinden **genel bakış** hello Azure portal sayfası. 

    `config.endpoint = "GRAPHENDPOINT";`

    ![Görüntüleme ve kopyalama hello Azure portalına erişim tuşu, anahtarlar dikey penceresinde](./media/create-graph-nodejs/gremlin-uri.png)

   Merhaba, **Gremlin URI** değer boşsa, hello hello değeri oluşturabilir **anahtarları** hello kullanarak hello portal sayfasında **URI** https:// kaldırma ve değiştirme değeri belgeleri toographs.

   Merhaba Gremlin uç noktası olmalıdır hello protokolü/bağlantı noktası numarası olmadan yalnızca hello ana bilgisayar adı gibi `mygraphdb.graphs.azure.com` (değil `https://mygraphdb.graphs.azure.com` veya `mygraphdb.graphs.azure.com:433`).

3. Config.js içinde hello config.primaryKey hello değeri doldurun **birincil anahtar** başlangıç değerinden **anahtarları** hello Azure portal sayfası. 

    `config.primaryKey = "PRIMARYKEY";`

   ![Azure portal anahtarlar dikey penceresinde Hello](./media/create-graph-nodejs/keys.png)

4. Merhaba veritabanı adı ve hello değeri config.database ve config.collection grafik (kapsayıcı) adını girin. 

Aşağıda, tamamlanan config.js dosyanızın nasıl görüneceğine ilişkin bir örnek bulabilirsiniz:

```nodejs
var config = {}

// Note that this must not have HTTPS or hello port number
config.endpoint = "testgraphacct.graphs.azure.com";
config.primaryKey = "Pams6e7LEUS7LJ2Qk0fjZf3eGo65JdMWHmyn65i52w8ozPX2oxY3iP0yu05t9v1WymAHNcMwPIqNAEv3XDFsEg==";
config.database = "graphdb"
config.collection = "Persons"

module.exports = config;
```

## <a name="run-hello-console-app"></a>Merhaba konsol uygulamasını çalıştırın

1. Bir terminal penceresi açın ve değiştirme (aracılığıyla `cd` komutu) toohello yükleme dizini hello projeye dahil hello package.json dosyası için.  

2. Çalıştırma `npm install` tooinstall hello npm modülleri dahil olmak üzere, gerekli `gremlin-secure`.

3. Çalıştırma `node app.js` terminal toostart içinde düğüm uygulamanızı.

## <a name="browse-with-data-explorer"></a>Veri Gezgini ile Göz Ama

Şimdi tooData Explorer hello Azure portal tooview içinde geri dönün, sorgu değiştirin ve yeni grafik verilerinizle çalışır.

Veri Gezgini'nde hello yeni veritabanı hello görünür **grafikleri** bölmesi. Hello koleksiyon tarafından izlenen hello veritabanını genişletin, sonra tıklatın **grafik**.

Merhaba örnek uygulama tarafından oluşturulan hello veri hello içinde hello sonraki bölmesinde görüntülenir **grafik** sekmesine tıkladığınızda **Filtre Uygula**.

Tamamlanıyor deneyin `g.V()` ile `.has('firstName', 'Thomas')` tootest hello filtre. Merhaba değeri büyük küçük harfe duyarlı olduğunu unutmayın.

## <a name="review-slas-in-hello-azure-portal"></a>Gözden geçirme SLA'hello Azure portalı

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-your-resources"></a>Kaynaklarınızı temizleme

Bu uygulamayı kullanarak toocontinue düşünmüyorsanız hello aşağıdakileri yaparak bu makalede oluşturulan tüm kaynakları silin: 

1. Merhaba hello sol gezinti menüsünde, Azure portal'ı tıklatın **kaynak grupları**ve ardından oluşturduğunuz hello kaynak hello adına tıklayın. 
2. Kaynak grubu sayfanızda tıklatın **silmek**, silinen hello kaynak toobe hello adını yazın ve ardından **silmek**.

## <a name="next-steps"></a>Sonraki adımlar

Bu makalede, bir Azure Cosmos DB hesap toocreate Veri Gezgini'ni kullanarak bir grafik oluşturma ve bir uygulama çalıştırmasına öğrendiniz. Artık daha karmaşık sorgular oluşturabilir ve Gremlin kullanarak güçlü grafik geçişi mantığını kullanabilirsiniz. 

> [!div class="nextstepaction"]
> [Gremlin kullanarak sorgulama](tutorial-query-graph.md)
