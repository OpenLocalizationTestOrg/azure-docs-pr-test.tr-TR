---
title: "Azure Cosmos DB: Python ile bir uygulama oluşturmak ve DocumentDB API hello | Microsoft Docs"
description: "Tooconnect tooand sorgu kullanabileceğiniz bir Python kodu örneği hello Azure Cosmos DB DocumentDB API sunar"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 51c11be2-af6d-425f-a86a-39cbfe61da29
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 05/13/2017
ms.author: mimig
ms.openlocfilehash: e66965ab493c6ef693e88a3767a401d39e1bde2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-python-and-hello-azure-portal"></a><span data-ttu-id="938d2-103">Azure Cosmos DB: Python ile DocumentDB API uygulaması oluşturma ve Azure portal hello</span><span class="sxs-lookup"><span data-stu-id="938d2-103">Azure Cosmos DB: Build a DocumentDB API app with Python and hello Azure portal</span></span>

<span data-ttu-id="938d2-104">Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="938d2-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="938d2-105">Hızlı bir şekilde oluşturmak ve belge, anahtar/değer ve grafik veritabanları, her biri hello genel dağıtım ve yatay ölçek özelliklerini Azure Cosmos DB'nin hello çekirdek yararlı sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="938d2-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="938d2-106">Bu hızlı başlangıç nasıl toocreate Azure Cosmos DB hesabınız, belge veritabanı ve koleksiyonu kullanarak Azure portalında hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="938d2-106">This quick start demonstrates how toocreate an Azure Cosmos DB account, document database, and collection using hello Azure portal.</span></span> <span data-ttu-id="938d2-107">Ardından derlemeyi ve çalıştırmayı hello üzerinde oluşturulmuş bir konsol uygulaması [DocumentDB Python API](documentdb-sdk-python.md).</span><span class="sxs-lookup"><span data-stu-id="938d2-107">You then build and run a console app built on hello [DocumentDB Python API](documentdb-sdk-python.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="938d2-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="938d2-108">Prerequisites</span></span>

* <span data-ttu-id="938d2-109">Bu örneği çalıştırmadan önce aşağıdaki önkoşullar hello sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="938d2-109">Before you can run this sample, you must have hello following prerequisites:</span></span>
    * <span data-ttu-id="938d2-110">[Visual Studio 2015](http://www.visualstudio.com/) veya üzeri.</span><span class="sxs-lookup"><span data-stu-id="938d2-110">[Visual Studio 2015](http://www.visualstudio.com/) or higher.</span></span>
    * <span data-ttu-id="938d2-111">[GitHub](http://microsoft.github.io/PTVS/)'dan Visual Studio için Python Araçları.</span><span class="sxs-lookup"><span data-stu-id="938d2-111">Python Tools for Visual Studio from [GitHub](http://microsoft.github.io/PTVS/).</span></span> <span data-ttu-id="938d2-112">Bu öğreticide, VS 2015 için Python Araçları kullanır.</span><span class="sxs-lookup"><span data-stu-id="938d2-112">This tutorial uses Python Tools for VS 2015.</span></span>
    * <span data-ttu-id="938d2-113">[python.org](https://www.python.org/downloads/release/python-2712/) adresinden Python 2.7</span><span class="sxs-lookup"><span data-stu-id="938d2-113">Python 2.7 from [python.org](https://www.python.org/downloads/release/python-2712/)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="938d2-114">Veritabanı hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="938d2-114">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="938d2-115">Koleksiyon ekleme</span><span class="sxs-lookup"><span data-stu-id="938d2-115">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a><span data-ttu-id="938d2-116">Merhaba örnek uygulaması kopyalama</span><span class="sxs-lookup"><span data-stu-id="938d2-116">Clone hello sample application</span></span>

<span data-ttu-id="938d2-117">Artık şimdi github, kopya bir DocumentDB API uygulamasını hello bağlantı dizesini ayarlamak ve çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="938d2-117">Now let's clone a DocumentDB API app from github, set hello connection string, and run it.</span></span> <span data-ttu-id="938d2-118">Ne kadar kolay toowork verilerle program aracılığıyla olduğunu görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="938d2-118">You see how easy it is toowork with data programmatically.</span></span> 

1. <span data-ttu-id="938d2-119">Git bash gibi bir git terminal penceresi açın ve `cd` tooa çalışma dizini.</span><span class="sxs-lookup"><span data-stu-id="938d2-119">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="938d2-120">Çalışma hello aşağıdaki tooclone hello örnek depo komutu.</span><span class="sxs-lookup"><span data-stu-id="938d2-120">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-python-getting-started.git
    ```  
## <a name="review-hello-code"></a><span data-ttu-id="938d2-121">Merhaba kod gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="938d2-121">Review hello code</span></span>

<span data-ttu-id="938d2-122">Neler olduğuna dair hello uygulamada hızlı bir gözden geçirme olalım.</span><span class="sxs-lookup"><span data-stu-id="938d2-122">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="938d2-123">Açık hello DocumentDBGetStarted.py dosyanız varsa ve bu kod satırları hello Azure Cosmos DB kaynakları oluşturma bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="938d2-123">Open hello DocumentDBGetStarted.py file and you'll find that these lines of code create hello Azure Cosmos DB resources.</span></span> 


* <span data-ttu-id="938d2-124">Merhaba DocumentClient başlatılır.</span><span class="sxs-lookup"><span data-stu-id="938d2-124">hello DocumentClient is initialized.</span></span>

    ```python
    # Initialize hello Python DocumentDB client
    client = document_client.DocumentClient(config['ENDPOINT'], {'masterKey': config['MASTERKEY']})
    ```

* <span data-ttu-id="938d2-125">Yeni bir veritabanı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="938d2-125">A new database is created.</span></span>

    ```python
    # Create a database
    db = client.CreateDatabase({ 'id': config['DOCUMENTDB_DATABASE'] })
    ```

* <span data-ttu-id="938d2-126">Yeni bir koleksiyon oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="938d2-126">A new collection is created.</span></span>

    ```python
    # Create collection options
    options = {
        'offerEnableRUPerMinuteThroughput': True,
        'offerVersion': "V2",
        'offerThroughput': 400
    }

    # Create a collection
    collection = client.CreateCollection(db['_self'], { 'id': config['DOCUMENTDB_COLLECTION'] }, options)
    ```

* <span data-ttu-id="938d2-127">Birkaç belge oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="938d2-127">Some documents are created.</span></span>

    ```python
    # Create some documents
    document1 = client.CreateDocument(collection['_self'],
        { 
            'id': 'server1',
            'Web Site': 0,
            'Cloud Service': 0,
            'Virtual Machine': 0,
            'name': 'some' 
        })
    ```

* <span data-ttu-id="938d2-128">SQL kullanılarak bir sorgu gerçekleştirilir</span><span class="sxs-lookup"><span data-stu-id="938d2-128">A query is performed using SQL</span></span>

    ```python
    # Query them in SQL
    query = { 'query': 'SELECT * FROM server s' }    
            
    options = {} 
    options['enableCrossPartitionQuery'] = True
    options['maxItemCount'] = 2

    result_iterable = client.QueryDocuments(collection['_self'], query, options)
    results = list(result_iterable);

    print(results)
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="938d2-129">Bağlantı dizenizi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="938d2-129">Update your connection string</span></span>

<span data-ttu-id="938d2-130">Şimdi Azure portal tooget toohello bağlantı dizesi bilgilerinizi geri dönün ve hello uygulamaya kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="938d2-130">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="938d2-131">Merhaba, [Azure portal](http://portal.azure.com/), Azure Cosmos DB hesap, sol gezinti hello tıklatın **anahtarları**ve ardından **okuma-yazma anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="938d2-131">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="938d2-132">Merhaba Kopyala düğmesi hello sağ tarafındaki Merhaba ekranında toocopy hello URI ve birincil anahtar hello kullanacağınız `DocumentDBGetStarted.py` hello sonraki adımda dosya.</span><span class="sxs-lookup"><span data-stu-id="938d2-132">You'll use hello copy buttons on hello right side of hello screen toocopy hello URI and Primary Key into hello `DocumentDBGetStarted.py` file in hello next step.</span></span>

    ![Görüntüleme ve kopyalama hello Azure portalına erişim tuşu, anahtarlar dikey penceresinde](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="938d2-134">Açık hello içinde `DocumentDBGetStarted.py` dosya.</span><span class="sxs-lookup"><span data-stu-id="938d2-134">In Open hello `DocumentDBGetStarted.py` file.</span></span> 

3. <span data-ttu-id="938d2-135">URI değeri (Merhaba Kopyala düğmesini kullanarak) hello Portal'dan kopyalayın ve hale hello hello uç noktası anahtarı değerini `DocumentDBGetStarted.py`.</span><span class="sxs-lookup"><span data-stu-id="938d2-135">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello endpoint key in `DocumentDBGetStarted.py`.</span></span> 

    `config.ENDPOINT : "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="938d2-136">Sonra birincil anahtar değer hello Portal'dan kopyalayın ve kolaylaştırır hello hello değerini `config.MASTERKEY` içinde `DocumentDBGetStarted.py`.</span><span class="sxs-lookup"><span data-stu-id="938d2-136">Then copy your PRIMARY KEY value from hello portal and make it hello value of hello `config.MASTERKEY` in `DocumentDBGetStarted.py`.</span></span> <span data-ttu-id="938d2-137">Uygulamanızı şimdi güncelleştirdikten toocommunicate Azure Cosmos DB ile gerekli tüm hello bilgilerine sahip.</span><span class="sxs-lookup"><span data-stu-id="938d2-137">You've now updated your app with all hello info it needs toocommunicate with Azure Cosmos DB.</span></span> 

    `config.MASTERKEY : "FILLME"`
    
## <a name="run-hello-app"></a><span data-ttu-id="938d2-138">Merhaba uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="938d2-138">Run hello app</span></span>
1. <span data-ttu-id="938d2-139">Visual Studio'da hello projeye sağ tıklayın **Çözüm Gezgini**hello geçerli Python ortamı seçin, sonra sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="938d2-139">In Visual Studio, right-click on hello project in **Solution Explorer**, select hello current Python environment, then right click.</span></span>

2. <span data-ttu-id="938d2-140">Python Paketini Yükle'yi seçip **pydocumentdb** yazın.</span><span class="sxs-lookup"><span data-stu-id="938d2-140">Select Install Python Package, then type in **pydocumentdb**</span></span>

3. <span data-ttu-id="938d2-141">F5 toorun hello uygulamayı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="938d2-141">Run F5 toorun hello application.</span></span> <span data-ttu-id="938d2-142">Uygulamanız tarayıcınızda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="938d2-142">Your app displays in your browser.</span></span> 

<span data-ttu-id="938d2-143">Şimdi tooData Explorer geri dönün ve sorgu görmek değiştirmek ve bu yeni verilerle çalışmak.</span><span class="sxs-lookup"><span data-stu-id="938d2-143">You can now go back tooData Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-hello-azure-portal"></a><span data-ttu-id="938d2-144">Gözden geçirme SLA'hello Azure portalı</span><span class="sxs-lookup"><span data-stu-id="938d2-144">Review SLAs in hello Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="938d2-145">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="938d2-145">Clean up resources</span></span>

<span data-ttu-id="938d2-146">Toocontinue toouse bu uygulamayı değil kullanacaksanız, bu hızlı başlangıç tarafından hello Azure portalında aşağıdaki adımları hello ile oluşturulan tüm kaynakları silin:</span><span class="sxs-lookup"><span data-stu-id="938d2-146">If you're not going toocontinue toouse this app, delete all resources created by this quickstart in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="938d2-147">Merhaba sol taraftaki menüden hello Azure portal'ın, **kaynak grupları** ve ardından oluşturduğunuz hello kaynak hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="938d2-147">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="938d2-148">Kaynak grubu sayfanızda tıklatın **silmek**hello metin kutusuna hello kaynak toodelete hello adını yazın ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="938d2-148">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="938d2-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="938d2-149">Next steps</span></span>

<span data-ttu-id="938d2-150">Bu hızlı başlangıç toocreate bir Azure Cosmos DB hesap hello Veri Gezgini'ni kullanarak bir koleksiyon oluşturma ve bir uygulama çalıştırmasına öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="938d2-150">In this quickstart, you've learned how toocreate an Azure Cosmos DB account, create a collection using hello Data Explorer, and run an app.</span></span> <span data-ttu-id="938d2-151">Artık ek verileri tooyour Cosmos DB hesap içeri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="938d2-151">You can now import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="938d2-152">Merhaba DocumentDB API Azure Cosmos Veritabanına veri alma</span><span class="sxs-lookup"><span data-stu-id="938d2-152">Import data into Azure Cosmos DB for hello DocumentDB API</span></span>](import-data.md)


