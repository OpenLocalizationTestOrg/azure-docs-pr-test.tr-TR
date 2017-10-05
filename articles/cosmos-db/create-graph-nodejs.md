---
title: "Grafik API'sini kullanarak Azure Cosmos DB Node.js uygulaması oluşturma | Microsoft Docs"
description: "Azure Cosmos DB'ye bağlanmak ve veritabanını sorgulamak için kullanabileceğiniz bir Node.js kod örneği sunar"
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
ms.openlocfilehash: 6d14719938af0ce825955389824441e111024869
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-build-a-nodejs-application-by-using-graph-api"></a><span data-ttu-id="403ce-103">Azure Cosmos DB: Grafik API'sini kullanarak bir Node.js uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="403ce-103">Azure Cosmos DB: Build a Node.js application by using Graph API</span></span>

<span data-ttu-id="403ce-104">Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="403ce-104">Azure Cosmos DB is the globally distributed multi-model database service from Microsoft.</span></span> <span data-ttu-id="403ce-105">Bu hizmetle belge, anahtar/değer ve grafik veritabanlarını kolayca oluşturup sorgulayabilir ve tüm bunları yaparken Azure Cosmos DB'nin genel dağıtım ve yatay ölçeklendirme özelliklerinden faydalanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="403ce-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="403ce-106">Bu hızlı başlangıç makalesinde, Azure portalı kullanılarak Grafik API'si (önizleme), veritabanı ve grafik için Azure Cosmos DB hesabının nasıl oluşturulacağı gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="403ce-106">This quick-start article demonstrates how to create an Azure Cosmos DB account for Graph API (preview), database, and graph by using the Azure portal.</span></span> <span data-ttu-id="403ce-107">Bu adımların ardından açık kaynaklı [Gremlin Node.js](https://www.npmjs.com/package/gremlin-secure) sürücüsünü kullanarak bir konsol uygulaması oluşturabilir ve çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="403ce-107">You then build and run a console app by using the open-source [Gremlin Node.js](https://www.npmjs.com/package/gremlin-secure) driver.</span></span>  

> [!NOTE]
> <span data-ttu-id="403ce-108">`gremlin-secure` npm modülü, `gremlin` modülünün Azure Cosmos DB ile bağlantı kurmak için gereken SSL ve SASL desteğine sahip değiştirilmiş bir sürümüdür.</span><span class="sxs-lookup"><span data-stu-id="403ce-108">The npm module `gremlin-secure` is a modified version of `gremlin` module, with support for SSL and SASL required for connecting with Azure Cosmos DB.</span></span> <span data-ttu-id="403ce-109">Kaynak kodu [GitHub](https://github.com/CosmosDB/gremlin-javascript)’dan edinilebilir.</span><span class="sxs-lookup"><span data-stu-id="403ce-109">Source code is available on [GitHub](https://github.com/CosmosDB/gremlin-javascript).</span></span>
>

## <a name="prerequisites"></a><span data-ttu-id="403ce-110">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="403ce-110">Prerequisites</span></span>

<span data-ttu-id="403ce-111">Bu örneği çalıştırmadan önce aşağıdaki önkoşullara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="403ce-111">Before you can run this sample, you must have the following prerequisites:</span></span>
* <span data-ttu-id="403ce-112">[Node.js](https://nodejs.org/en/) v0.10.29 sürümü veya sonraki bir sürüm</span><span class="sxs-lookup"><span data-stu-id="403ce-112">[Node.js](https://nodejs.org/en/) version v0.10.29 or later</span></span>
* [<span data-ttu-id="403ce-113">Git</span><span class="sxs-lookup"><span data-stu-id="403ce-113">Git</span></span>](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="403ce-114">Veritabanı hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="403ce-114">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a><span data-ttu-id="403ce-115">Grafik ekleme</span><span class="sxs-lookup"><span data-stu-id="403ce-115">Add a graph</span></span>

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="403ce-116">Örnek uygulamayı kopyalama</span><span class="sxs-lookup"><span data-stu-id="403ce-116">Clone the sample application</span></span>

<span data-ttu-id="403ce-117">Şimdi GitHub'dan bir Grafik API'si uygulaması kopyalayalım, bağlantı dizesini ayarlayalım ve uygulamayı çalıştıralım.</span><span class="sxs-lookup"><span data-stu-id="403ce-117">Now let's clone a Graph API app from GitHub, set the connection string, and run it.</span></span> <span data-ttu-id="403ce-118">Verilerle programlı bir şekilde çalışmanın ne kadar kolay olduğunu göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="403ce-118">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="403ce-119">Git Bash gibi bir Git terminal penceresi açın ve bir çalışma diziniyle değiştirin (`cd` komutuyla).</span><span class="sxs-lookup"><span data-stu-id="403ce-119">Open a Git terminal window, such as Git Bash, and change (via `cd` command) to a working directory.</span></span>  

2. <span data-ttu-id="403ce-120">Örnek depoyu kopyalamak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="403ce-120">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-nodejs-getting-started.git
    ```

3. <span data-ttu-id="403ce-121">Çözüm dosyasını Visual Studio'da açın.</span><span class="sxs-lookup"><span data-stu-id="403ce-121">Open the solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="403ce-122">Kodu gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="403ce-122">Review the code</span></span>

<span data-ttu-id="403ce-123">Uygulamada gerçekleşen işlemleri hızlıca gözden geçirelim.</span><span class="sxs-lookup"><span data-stu-id="403ce-123">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="403ce-124">`app.js` dosyasını açtığınızda aşağıdaki kod satırlarıyla karşılaşacaksınız.</span><span class="sxs-lookup"><span data-stu-id="403ce-124">Open the `app.js` file, and you'll find the following lines of code.</span></span> 

* <span data-ttu-id="403ce-125">Gremlin istemcisi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="403ce-125">The Gremlin client is created.</span></span>

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

  <span data-ttu-id="403ce-126">Tüm yapılandırmalar, aşağıdaki bölümde düzenlediğimiz `config.js` öğesinde yer alır.</span><span class="sxs-lookup"><span data-stu-id="403ce-126">The configurations are all in `config.js`, which we edit in the following section.</span></span>

* <span data-ttu-id="403ce-127">`client.execute` yöntemiyle bir dizi Gremlin adımı yürütülür.</span><span class="sxs-lookup"><span data-stu-id="403ce-127">A series of Gremlin steps are executed with the `client.execute` method.</span></span>

    ```nodejs
    console.log('Running Count'); 
    client.execute("g.V().count()", { }, (err, results) => {
        if (err) return console.error(err);
        console.log(JSON.stringify(results));
        console.log();
    });
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="403ce-128">Bağlantı dizenizi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="403ce-128">Update your connection string</span></span>

1. <span data-ttu-id="403ce-129">Config.js dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="403ce-129">Open the config.js file.</span></span> 

2. <span data-ttu-id="403ce-130">Config.js dosyasında, config.endpoint anahtarını Azure portalının **Genel Bakış** sayfasında bulunan **Gremlin URI** değeriyle doldurun.</span><span class="sxs-lookup"><span data-stu-id="403ce-130">In config.js, fill in the config.endpoint key with the **Gremlin URI** value from the **Overview** page of the Azure portal.</span></span> 

    `config.endpoint = "GRAPHENDPOINT";`

    ![Azure portalında erişim anahtarı görüntüleme ve kopyalama, Anahtarlar dikey penceresi](./media/create-graph-nodejs/gremlin-uri.png)

   <span data-ttu-id="403ce-132">**Gremlin URI** değeri boşsa, portaldaki **Anahtarlar** sayfasında bulunan **URI** değerini kullanıp https:// bölümünü çıkararak ve belgeleri grafiklere dönüştürerek bir değer oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="403ce-132">If the **Gremlin URI** value is blank, you can generate the value from the **Keys** page in the portal, using the **URI** value, removing https://, and changing documents to graphs.</span></span>

   <span data-ttu-id="403ce-133">Gremlin uç noktası, `mygraphdb.graphs.azure.com` (`https://mygraphdb.graphs.azure.com` veya `mygraphdb.graphs.azure.com:433` değil) gibi protokol/bağlantı noktası numarası olmayan tek ana bilgisayar adı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="403ce-133">The Gremlin endpoint must be only the host name without the protocol/port number, like `mygraphdb.graphs.azure.com` (not `https://mygraphdb.graphs.azure.com` or `mygraphdb.graphs.azure.com:433`).</span></span>

3. <span data-ttu-id="403ce-134">Config.js dosyasında, config.primaryKey değerini Azure portalının **Anahtarlar** sayfasında bulunan **Birincil Anahtar** değeriyle doldurun.</span><span class="sxs-lookup"><span data-stu-id="403ce-134">In config.js, fill in the config.primaryKey value in with the **Primary Key** value from the **Keys** page of the Azure portal.</span></span> 

    `config.primaryKey = "PRIMARYKEY";`

   ![Azure portalı Anahtarlar dikey penceresi](./media/create-graph-nodejs/keys.png)

4. <span data-ttu-id="403ce-136">Veritabanı adını ve config.database ve config.collection değerinin grafik (kapsayıcı) adını girin.</span><span class="sxs-lookup"><span data-stu-id="403ce-136">Enter the database name, and graph (container) name for the value of config.database and config.collection.</span></span> 

<span data-ttu-id="403ce-137">Aşağıda, tamamlanan config.js dosyanızın nasıl görüneceğine ilişkin bir örnek bulabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="403ce-137">Here is an example of what your completed config.js file should look like:</span></span>

```nodejs
var config = {}

// Note that this must not have HTTPS or the port number
config.endpoint = "testgraphacct.graphs.azure.com";
config.primaryKey = "Pams6e7LEUS7LJ2Qk0fjZf3eGo65JdMWHmyn65i52w8ozPX2oxY3iP0yu05t9v1WymAHNcMwPIqNAEv3XDFsEg==";
config.database = "graphdb"
config.collection = "Persons"

module.exports = config;
```

## <a name="run-the-console-app"></a><span data-ttu-id="403ce-138">Konsol uygulamasını çalıştırma</span><span class="sxs-lookup"><span data-stu-id="403ce-138">Run the console app</span></span>

1. <span data-ttu-id="403ce-139">Terminal penceresi açın ve projeye dahil olan package.json dosyası için yükleme diziniyle değiştirin (`cd` komutuyla).</span><span class="sxs-lookup"><span data-stu-id="403ce-139">Open a terminal window and change (via `cd` command) to the installation directory for the package.json file that's included in the project.</span></span>  

2. <span data-ttu-id="403ce-140">`gremlin-secure` dahil gerekli npm modüllerini yüklemek için `npm install` öğesini çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="403ce-140">Run `npm install` to install the required npm modules, including `gremlin-secure`.</span></span>

3. <span data-ttu-id="403ce-141">Node.js uygulamanızı başlatmak için bir terminalde `node app.js` komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="403ce-141">Run `node app.js` in a terminal to start your node application.</span></span>

## <a name="browse-with-data-explorer"></a><span data-ttu-id="403ce-142">Veri Gezgini ile Göz Ama</span><span class="sxs-lookup"><span data-stu-id="403ce-142">Browse with Data Explorer</span></span>

<span data-ttu-id="403ce-143">Artık Azure portalındaki Veri Gezgini'ne dönerek yeni grafik verilerinizi görüntüleyebilir, sorgulayabilir, değiştirebilir ve bu verilerle çalışabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="403ce-143">You can now go back to Data Explorer in the Azure portal to view, query, modify, and work with your new graph data.</span></span>

<span data-ttu-id="403ce-144">Yeni veritabanı, Veri Gezgini'nin **Grafikler** bölmesinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="403ce-144">In Data Explorer, the new database appears in the **Graphs** pane.</span></span> <span data-ttu-id="403ce-145">Veritabanını ve ardından koleksiyonu genişletip **Grafik**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="403ce-145">Expand the database, followed by the collection, then click **Graph**.</span></span>

<span data-ttu-id="403ce-146">Örnek uygulama tarafından oluşturulan veriler, **Filtre Uygula**’ya tıkladığınızda **Grafik** sekmesinin sonraki bölmesinde gösterilir.</span><span class="sxs-lookup"><span data-stu-id="403ce-146">The data generated by the sample app is displayed in the next pane within the **Graph** tab when you click **Apply Filter**.</span></span>

<span data-ttu-id="403ce-147">Filtreyi test etmek için `g.V()` işlemini `.has('firstName', 'Thomas')` ile tamamlamayı deneyin.</span><span class="sxs-lookup"><span data-stu-id="403ce-147">Try completing `g.V()` with `.has('firstName', 'Thomas')` to test the filter.</span></span> <span data-ttu-id="403ce-148">Değerin büyük küçük harfe duyarlı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="403ce-148">Do note that the value is case sensitive.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="403ce-149">Azure portalında SLA'ları gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="403ce-149">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-your-resources"></a><span data-ttu-id="403ce-150">Kaynaklarınızı temizleme</span><span class="sxs-lookup"><span data-stu-id="403ce-150">Clean up your resources</span></span>

<span data-ttu-id="403ce-151">Bu uygulamayı kullanmaya devam etmeyi düşünmüyorsanız aşağıdakileri yaparak bu makalede oluşturduğunuz tüm kaynakları silin:</span><span class="sxs-lookup"><span data-stu-id="403ce-151">If you do not plan to continue using this app, delete all resources that you created in this article by doing the following:</span></span> 

1. <span data-ttu-id="403ce-152">Azure portalında sol taraftaki menüden **Kaynak grupları**'na ve ardından oluşturduğunuz kaynağın adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="403ce-152">In the Azure portal, on the left navigation menu, click **Resource groups**, and then click the name of the resource that you created.</span></span> 
2. <span data-ttu-id="403ce-153">Kaynak grubu sayfanızda **Sil**'e tıklayın, silinecek kaynağın adını yazın ve ardından **Sil**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="403ce-153">On your resource group page, click **Delete**, type the name of the resource to be deleted, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="403ce-154">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="403ce-154">Next steps</span></span>

<span data-ttu-id="403ce-155">Bu makalede, Azure Cosmos DB hesabı oluşturmayı, Veri Gezgini'ni kullanarak grafik oluşturmayı ve bir uygulamayı çalıştırmayı öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="403ce-155">In this article, you've learned how to create an Azure Cosmos DB account, create a graph by using Data Explorer, and run an app.</span></span> <span data-ttu-id="403ce-156">Artık daha karmaşık sorgular oluşturabilir ve Gremlin kullanarak güçlü grafik geçişi mantığını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="403ce-156">You can now build more complex queries and implement powerful graph traversal logic by using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="403ce-157">Gremlin kullanarak sorgulama</span><span class="sxs-lookup"><span data-stu-id="403ce-157">Query using Gremlin</span></span>](tutorial-query-graph.md)
