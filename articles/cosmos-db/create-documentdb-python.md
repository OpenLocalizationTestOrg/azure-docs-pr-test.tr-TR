---
title: 'Azure Cosmos DB: Python ve DocumentDB API''si ile bir uygulama derleme | Microsoft Docs'
description: "Azure Cosmos DB DocumentDB API'sine bağlanmak ve sorgu göndermek için kullanabileceğiniz bir Python kodu örneği sunar"
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
ms.openlocfilehash: 08d467ea27484e7d1d07d6c21b2e04b6525fbcd8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-python-and-the-azure-portal"></a><span data-ttu-id="adc35-103">Azure Cosmos DB: Python ve Azure portalı ile bir DocumentDB API'si uygulaması derleme</span><span class="sxs-lookup"><span data-stu-id="adc35-103">Azure Cosmos DB: Build a DocumentDB API app with Python and the Azure portal</span></span>

<span data-ttu-id="adc35-104">Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="adc35-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="adc35-105">Bu hizmetle belge, anahtar/değer ve grafik veritabanlarını kolayca oluşturup sorgulayabilir ve tüm bunları yaparken Azure Cosmos DB'nin genel dağıtım ve yatay ölçeklendirme özelliklerinden faydalanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="adc35-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="adc35-106">Bu hızlı başlangıç belgesinde Azure portalı kullanarak bir Azure Cosmos DB hesabını, belge veritabanını ve koleksiyonunu nasıl oluşturacağınız anlatılmıştır.</span><span class="sxs-lookup"><span data-stu-id="adc35-106">This quick start demonstrates how to create an Azure Cosmos DB account, document database, and collection using the Azure portal.</span></span> <span data-ttu-id="adc35-107">Bu adımların ardından [DocumentDB Python API'si](documentdb-sdk-python.md) kullanarak bir konsol uygulaması derleyebilir ve çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="adc35-107">You then build and run a console app built on the [DocumentDB Python API](documentdb-sdk-python.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="adc35-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="adc35-108">Prerequisites</span></span>

* <span data-ttu-id="adc35-109">Bu örneği çalıştırmadan önce aşağıdaki önkoşullara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="adc35-109">Before you can run this sample, you must have the following prerequisites:</span></span>
    * <span data-ttu-id="adc35-110">[Visual Studio 2015](http://www.visualstudio.com/) veya üzeri.</span><span class="sxs-lookup"><span data-stu-id="adc35-110">[Visual Studio 2015](http://www.visualstudio.com/) or higher.</span></span>
    * <span data-ttu-id="adc35-111">[GitHub](http://microsoft.github.io/PTVS/)'dan Visual Studio için Python Araçları.</span><span class="sxs-lookup"><span data-stu-id="adc35-111">Python Tools for Visual Studio from [GitHub](http://microsoft.github.io/PTVS/).</span></span> <span data-ttu-id="adc35-112">Bu öğreticide, VS 2015 için Python Araçları kullanır.</span><span class="sxs-lookup"><span data-stu-id="adc35-112">This tutorial uses Python Tools for VS 2015.</span></span>
    * <span data-ttu-id="adc35-113">[python.org](https://www.python.org/downloads/release/python-2712/) adresinden Python 2.7</span><span class="sxs-lookup"><span data-stu-id="adc35-113">Python 2.7 from [python.org](https://www.python.org/downloads/release/python-2712/)</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="adc35-114">Veritabanı hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="adc35-114">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a><span data-ttu-id="adc35-115">Koleksiyon ekleme</span><span class="sxs-lookup"><span data-stu-id="adc35-115">Add a collection</span></span>

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="adc35-116">Örnek uygulamayı kopyalama</span><span class="sxs-lookup"><span data-stu-id="adc35-116">Clone the sample application</span></span>

<span data-ttu-id="adc35-117">Şimdi GitHub'dan bir DocumentDB API uygulaması kopyalayalım, bağlantı dizesini ayarlayalım ve uygulamayı çalıştıralım.</span><span class="sxs-lookup"><span data-stu-id="adc35-117">Now let's clone a DocumentDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="adc35-118">Verilerle programlı bir şekilde çalışmanın ne kadar kolay olduğunu görüyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="adc35-118">You see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="adc35-119">Git bash gibi bir git terminal penceresi açın ve `cd` ile çalışma dizinine gidin.</span><span class="sxs-lookup"><span data-stu-id="adc35-119">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="adc35-120">Örnek depoyu kopyalamak için aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="adc35-120">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-python-getting-started.git
    ```  
## <a name="review-the-code"></a><span data-ttu-id="adc35-121">Kodu gözden geçirin</span><span class="sxs-lookup"><span data-stu-id="adc35-121">Review the code</span></span>

<span data-ttu-id="adc35-122">Uygulamada gerçekleşen işlemleri hızlıca gözden geçirelim.</span><span class="sxs-lookup"><span data-stu-id="adc35-122">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="adc35-123">DocumentDBGetStarted.py dosyasını açtığınızda Azure Cosmos DB kaynaklarını bu kod satırlarının oluşturduğunu göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="adc35-123">Open the DocumentDBGetStarted.py file and you'll find that these lines of code create the Azure Cosmos DB resources.</span></span> 


* <span data-ttu-id="adc35-124">DocumentClient başlatılır.</span><span class="sxs-lookup"><span data-stu-id="adc35-124">The DocumentClient is initialized.</span></span>

    ```python
    # Initialize the Python DocumentDB client
    client = document_client.DocumentClient(config['ENDPOINT'], {'masterKey': config['MASTERKEY']})
    ```

* <span data-ttu-id="adc35-125">Yeni bir veritabanı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="adc35-125">A new database is created.</span></span>

    ```python
    # Create a database
    db = client.CreateDatabase({ 'id': config['DOCUMENTDB_DATABASE'] })
    ```

* <span data-ttu-id="adc35-126">Yeni bir koleksiyon oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="adc35-126">A new collection is created.</span></span>

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

* <span data-ttu-id="adc35-127">Birkaç belge oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="adc35-127">Some documents are created.</span></span>

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

* <span data-ttu-id="adc35-128">SQL kullanılarak bir sorgu gerçekleştirilir</span><span class="sxs-lookup"><span data-stu-id="adc35-128">A query is performed using SQL</span></span>

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

## <a name="update-your-connection-string"></a><span data-ttu-id="adc35-129">Bağlantı dizenizi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="adc35-129">Update your connection string</span></span>

<span data-ttu-id="adc35-130">Bu adımda Azure portalına dönerek bağlantı dizesi bilgilerinizi kopyalayıp uygulamaya ekleyin.</span><span class="sxs-lookup"><span data-stu-id="adc35-130">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="adc35-131">[Azure portalında](http://portal.azure.com/), Azure Cosmos DB hesabınızın sol taraftaki gezinti menüsünden **Anahtarlar**'a ve ardından **Okuma/Yazma Anahtarları**'na tıklayın.</span><span class="sxs-lookup"><span data-stu-id="adc35-131">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="adc35-132">Ekranın sağ tarafındaki kopyalama düğmelerini kullanarak URI ve Birincil Anahtar değerlerini kopyalayarak sonraki adımda `DocumentDBGetStarted.py` dosyasına yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="adc35-132">You'll use the copy buttons on the right side of the screen to copy the URI and Primary Key into the `DocumentDBGetStarted.py` file in the next step.</span></span>

    ![Azure portalında erişim anahtarı görüntüleme ve kopyalama, Anahtarlar dikey penceresi](./media/create-documentdb-dotnet/keys.png)

2. <span data-ttu-id="adc35-134">`DocumentDBGetStarted.py` dosyasını açın.</span><span class="sxs-lookup"><span data-stu-id="adc35-134">In Open the `DocumentDBGetStarted.py` file.</span></span> 

3. <span data-ttu-id="adc35-135">Portaldaki URI değerinizi kopyalayın (kopyalama düğmesini kullanarak) ve `DocumentDBGetStarted.py` dosyasına uç nokta değeri olarak yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="adc35-135">Copy your URI value from the portal (using the copy button) and make it the value of the endpoint key in `DocumentDBGetStarted.py`.</span></span> 

    `config.ENDPOINT : "https://FILLME.documents.azure.com"`

4. <span data-ttu-id="adc35-136">Ardından portaldaki BİRİNCİL ANAHTAR değerinizi kopyalayıp `DocumentDBGetStarted.py` dosyasına `config.MASTERKEY` değeri olarak yapıştırın.</span><span class="sxs-lookup"><span data-stu-id="adc35-136">Then copy your PRIMARY KEY value from the portal and make it the value of the `config.MASTERKEY` in `DocumentDBGetStarted.py`.</span></span> <span data-ttu-id="adc35-137">Bu adımlarla uygulamanıza Azure Cosmos DB ile iletişim kurması için gereken tüm bilgileri eklemiş oldunuz.</span><span class="sxs-lookup"><span data-stu-id="adc35-137">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> 

    `config.MASTERKEY : "FILLME"`
    
## <a name="run-the-app"></a><span data-ttu-id="adc35-138">Uygulamayı çalıştırma</span><span class="sxs-lookup"><span data-stu-id="adc35-138">Run the app</span></span>
1. <span data-ttu-id="adc35-139">Visual Studio'nun **Çözüm Gezgini** bölümünde projeye sağ tıklayın, geçerli Python ortamını seçin ve sağ tıklayın.</span><span class="sxs-lookup"><span data-stu-id="adc35-139">In Visual Studio, right-click on the project in **Solution Explorer**, select the current Python environment, then right click.</span></span>

2. <span data-ttu-id="adc35-140">Python Paketini Yükle'yi seçip **pydocumentdb** yazın.</span><span class="sxs-lookup"><span data-stu-id="adc35-140">Select Install Python Package, then type in **pydocumentdb**</span></span>

3. <span data-ttu-id="adc35-141">Uygulamayı çalıştırmak için F5'e basın.</span><span class="sxs-lookup"><span data-stu-id="adc35-141">Run F5 to run the application.</span></span> <span data-ttu-id="adc35-142">Uygulamanız tarayıcınızda görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="adc35-142">Your app displays in your browser.</span></span> 

<span data-ttu-id="adc35-143">Şimdi Veri Gezgini'ne dönüp bu yeni verileri görebilir, sorgulayabilir, değiştirebilir ve onlarla çalışabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="adc35-143">You can now go back to Data Explorer and see query, modify, and work with this new data.</span></span> 

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="adc35-144">Azure portalında SLA'ları gözden geçirme</span><span class="sxs-lookup"><span data-stu-id="adc35-144">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="adc35-145">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="adc35-145">Clean up resources</span></span>

<span data-ttu-id="adc35-146">Bu uygulamayı kullanmaya devam etmeyecekseniz aşağıdaki adımları kullanarak Azure portalında bu hızlı başlangıç tarafından oluşturulan tüm kaynakları silin:</span><span class="sxs-lookup"><span data-stu-id="adc35-146">If you're not going to continue to use this app, delete all resources created by this quickstart in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="adc35-147">Azure portalında sol taraftaki menüden, **Kaynak grupları**'na ve ardından oluşturduğunuz kaynağın adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="adc35-147">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="adc35-148">Kaynak grubu sayfanızda, **Sil**'e tıklayın, metin kutusuna silinecek kaynağın adını yazın ve ardından **Sil**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="adc35-148">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="adc35-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="adc35-149">Next steps</span></span>

<span data-ttu-id="adc35-150">Bu hızlı başlangıçta Azure Cosmos DB hesabı oluşturmayı, Veri Gezgini'ni kullanarak koleksiyon oluşturmayı ve bir uygulamayı çalıştırmayı öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="adc35-150">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a collection using the Data Explorer, and run an app.</span></span> <span data-ttu-id="adc35-151">Şimdi Cosmos DB hesabınıza ek veri aktarabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="adc35-151">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="adc35-152">DocumentDB API'si için Azure Cosmos DB içine veri aktarma</span><span class="sxs-lookup"><span data-stu-id="adc35-152">Import data into Azure Cosmos DB for the DocumentDB API</span></span>](import-data.md)


