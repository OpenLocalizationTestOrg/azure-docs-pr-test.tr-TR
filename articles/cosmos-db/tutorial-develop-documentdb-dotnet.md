---
title: "Azure Cosmos DB: ' % s'documentdb API .NET geliştirme | Microsoft Docs"
description: ".NET kullanarak Azure Cosmos veritabanı DocumentDB API'si ile geliştirmeyi öğrenin"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.custom: mvc
ms.openlocfilehash: 2eed74ae9bd173b0944ec190dfe5d9a4bdc54c37
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmosdb-develop-with-the-documentdb-api-in-net"></a><span data-ttu-id="65e95-103">Azure CosmosDB: ' % s'documentdb API .NET geliştirin</span><span class="sxs-lookup"><span data-stu-id="65e95-103">Azure CosmosDB: Develop with the DocumentDB API in .NET</span></span>

<span data-ttu-id="65e95-104">Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="65e95-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="65e95-105">Bu hizmetle belge, anahtar/değer ve grafik veritabanlarını kolayca oluşturup sorgulayabilir ve tüm bunları yaparken Azure Cosmos DB'nin genel dağıtım ve yatay ölçeklendirme özelliklerinden faydalanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65e95-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="65e95-106">Bu öğreticide Azure portalını kullanarak bir Azure Cosmos DB hesabı oluşturmak ve bir belge veritabanı ve koleksiyonu oluşturmak nasıl gösteren bir [bölüm anahtarı](documentdb-partition-data.md#partition-keys) kullanarak [DocumentDB .NET API](documentdb-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="65e95-106">This tutorial demonstrates how to create an Azure Cosmos DB account using the Azure portal, and then create a document database and collection with a [partition key](documentdb-partition-data.md#partition-keys) using the [DocumentDB .NET API](documentdb-introduction.md).</span></span> <span data-ttu-id="65e95-107">Bir koleksiyon oluşturduğunuzda bir bölüm anahtarı tanımlayarak, uygulamanızın verilerinizi büyüdükçe harcamadan ölçeklendirmek için hazırlanır.</span><span class="sxs-lookup"><span data-stu-id="65e95-107">By defining a partition key when you create a collection, your application is prepared to scale effortlessly as your data grows.</span></span> 

<span data-ttu-id="65e95-108">Bu öğretici kullanarak aşağıdaki görevleri kapsar [DocumentDB .NET API](documentdb-sdk-dotnet.md):</span><span class="sxs-lookup"><span data-stu-id="65e95-108">This tutorial covers the following tasks by using the [DocumentDB .NET API](documentdb-sdk-dotnet.md):</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="65e95-109">Azure Cosmos DB hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="65e95-109">Create an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="65e95-110">Bir bölüm anahtarının bir veritabanınızı ve koleksiyonunuzu oluşturun</span><span class="sxs-lookup"><span data-stu-id="65e95-110">Create a database and collection with a partition key</span></span>
> * <span data-ttu-id="65e95-111">JSON belgeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="65e95-111">Create JSON documents</span></span>
> * <span data-ttu-id="65e95-112">Bir belgeyi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="65e95-112">Update a document</span></span>
> * <span data-ttu-id="65e95-113">Bölümlenmiş koleksiyonlar sorgulama</span><span class="sxs-lookup"><span data-stu-id="65e95-113">Query partitioned collections</span></span>
> * <span data-ttu-id="65e95-114">Saklı yordamları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="65e95-114">Run stored procedures</span></span>
> * <span data-ttu-id="65e95-115">Bir belgeyi silme</span><span class="sxs-lookup"><span data-stu-id="65e95-115">Delete a document</span></span>
> * <span data-ttu-id="65e95-116">Bir veritabanını silin</span><span class="sxs-lookup"><span data-stu-id="65e95-116">Delete a database</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65e95-117">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="65e95-117">Prerequisites</span></span>
<span data-ttu-id="65e95-118">Lütfen aşağıdakilere sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="65e95-118">Please make sure you have the following:</span></span>

* <span data-ttu-id="65e95-119">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="65e95-119">An active Azure account.</span></span> <span data-ttu-id="65e95-120">Bir aboneliğiniz yoksa [ücretsiz bir hesap](https://azure.microsoft.com/free/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65e95-120">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="65e95-121">Alternatif olarak, kullanabileceğiniz [Azure Cosmos DB öykünücüsü](local-emulator.md) geliştirme amacıyla Azure DocumentDB hizmetinin öykünen yerel bir ortam kullanmak istiyorsanız, Bu öğretici için.</span><span class="sxs-lookup"><span data-stu-id="65e95-121">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial if you'd like to use a local environment that emulates the Azure DocumentDB service for development purposes.</span></span>
* <span data-ttu-id="65e95-122">[Visual Studio](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="65e95-122">[Visual Studio](http://www.visualstudio.com/).</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="65e95-123">Azure Cosmos DB hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="65e95-123">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="65e95-124">Azure portalında bir Azure Cosmos DB hesabı oluşturarak başlayalım.</span><span class="sxs-lookup"><span data-stu-id="65e95-124">Let's start by creating an Azure Cosmos DB account in the Azure portal.</span></span>

> [!TIP]
> * <span data-ttu-id="65e95-125">Zaten Azure Cosmos DB hesabınız var mı?</span><span class="sxs-lookup"><span data-stu-id="65e95-125">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="65e95-126">Bu durumda, İleri için atlayabilirsiniz [, Visual Studio çözümü ayarlama](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="65e95-126">If so, skip ahead to [Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="65e95-127">Bir Azure DocumentDB hesabına sahip miydiniz?</span><span class="sxs-lookup"><span data-stu-id="65e95-127">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="65e95-128">Bu nedenle, hesabınızı şimdi bir Azure Cosmos DB hesabı ise ve size atlayabilirsiniz [, Visual Studio çözümü ayarlama](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="65e95-128">If so, your account is now an Azure Cosmos DB account and you can skip ahead to [Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="65e95-129">Azure Cosmos DB öykünücüsü kullanıyorsanız, lütfen bölümündeki adımları izleyin [Azure Cosmos DB öykünücüsü](local-emulator.md) öykünücü kurulması ve için İleri atlayabilirsiniz [, Visual Studio çözümünü kurmak](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="65e95-129">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="65e95-130"><a id="SetupVS"></a>Visual Studio çözümünüzü kurma</span><span class="sxs-lookup"><span data-stu-id="65e95-130"><a id="SetupVS"></a>Set up your Visual Studio solution</span></span>
1. <span data-ttu-id="65e95-131">Bilgisayarınızda **Visual Studio**'yu açın.</span><span class="sxs-lookup"><span data-stu-id="65e95-131">Open **Visual Studio** on your computer.</span></span>
2. <span data-ttu-id="65e95-132">**Dosya** menüsünde **Yeni**'yi seçin ve ardından **Proje**'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="65e95-132">On the **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="65e95-133">İçinde **yeni proje** iletişim kutusunda **şablonları** / **Visual C#** / **konsol uygulaması (.NET Framework)** , projenizi adlandırın ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="65e95-133">In the **New Project** dialog, select **Templates** / **Visual C#** / **Console App (.NET Framework)**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="65e95-134">![Yeni Proje penceresinin ekran görüntüsü](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="65e95-134">![Screen shot of the New Project window](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)</span></span>

4. <span data-ttu-id="65e95-135">**Çözüm Gezgini**'nde Visual Studio çözümünüzün altındaki yeni konsol uygulamanıza sağ tıklayın ve **NuGet Paketlerini Yönet...** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="65e95-135">In the **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![Proje için Sağ Tıklama Menüsünün ekran görüntüsü](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="65e95-137">İçinde **NuGet** sekmesini tıklatın, **Gözat**ve türü **documentdb** arama kutusuna.</span><span class="sxs-lookup"><span data-stu-id="65e95-137">In the **NuGet** tab, click **Browse**, and type **documentdb** in the search box.</span></span>
<!---stopped here--->
6. <span data-ttu-id="65e95-138">Sonuçlarda **Microsoft.Azure.DocumentDB**'yi bulun ve **Yükle**'ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="65e95-138">Within the results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="65e95-139">Azure Cosmos DB istemci kitaplığı için paket kimliği [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).</span><span class="sxs-lookup"><span data-stu-id="65e95-139">The package ID for the Azure Cosmos DB Client Library is [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).</span></span>
   <span data-ttu-id="65e95-140">![Azure Cosmos DB istemci SDK'sını bulmak için NuGet menüsünün ekran görüntüsü](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="65e95-140">![Screen shot of the NuGet Menu for finding Azure Cosmos DB Client SDK](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="65e95-141">Çözümdeki değişiklikleri gözden geçirme hakkında iletiler alırsanız **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="65e95-141">If you get a message about reviewing changes to the solution, click **OK**.</span></span> <span data-ttu-id="65e95-142">Lisans kabulü hakkında bir ileti alırsanız **Kabul ediyorum**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="65e95-142">If you get a message about license acceptance, click **I accept**.</span></span>

## <span data-ttu-id="65e95-143"><a id="Connect"></a>Başvuruları projenize ekleme</span><span class="sxs-lookup"><span data-stu-id="65e95-143"><a id="Connect"></a>Add references to your project</span></span>
<span data-ttu-id="65e95-144">Bu öğreticide kalan adımlar oluşturmak ve Azure Cosmos DB kaynakları projenize güncelleştirmek için gereken DocumentDB API kod parçacıkları sağlar.</span><span class="sxs-lookup"><span data-stu-id="65e95-144">The remaining steps in this tutorial provide the DocumentDB API code snippets required to create and update Azure Cosmos DB resources in your project.</span></span>

<span data-ttu-id="65e95-145">İlk olarak, uygulamanız bu başvurular ekleyin.</span><span class="sxs-lookup"><span data-stu-id="65e95-145">First, add these references to your application.</span></span>
<!---These aren't added by default when you install the pkg?--->

```csharp
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

## <span data-ttu-id="65e95-146"><a id="add-references"></a>Uygulamanızı bağlama</span><span class="sxs-lookup"><span data-stu-id="65e95-146"><a id="add-references"></a>Connect your app</span></span>

<span data-ttu-id="65e95-147">Ardından, bu iki sabitleri ekleyin ve *istemci* uygulamanızda değişken.</span><span class="sxs-lookup"><span data-stu-id="65e95-147">Next, add these two constants and your *client* variable in your application.</span></span>

```csharp
private const string EndpointUrl = "<your endpoint URL>";
private const string PrimaryKey = "<your primary key>";
private DocumentClient client;
```

<span data-ttu-id="65e95-148">Head ardından, yeniden [Azure portal](https://portal.azure.com) uç noktasının URL'sini ve birincil anahtar alınamadı.</span><span class="sxs-lookup"><span data-stu-id="65e95-148">Then, head back to the [Azure portal](https://portal.azure.com) to retrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="65e95-149">Uç nokta URL’si ve birincil anahtar, uygulamanızın nereye bağlanacağını anlaması ve Azure Cosmos DB’nin uygulamanızın bağlantısına güvenmesi için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="65e95-149">The endpoint URL and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span>

<span data-ttu-id="65e95-150">Azure portalında Azure Cosmos DB hesabınıza gidin, tıklatın **anahtarları**ve ardından **okuma-yazma anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="65e95-150">In the Azure portal, navigate to your Azure Cosmos DB account, click **Keys**, and then click **Read-write Keys**.</span></span>

<span data-ttu-id="65e95-151">URI Portal'dan kopyalayın ve üzerinden yapıştırın `<your endpoint URL>` program.cs dosyasındaki.</span><span class="sxs-lookup"><span data-stu-id="65e95-151">Copy the URI from the portal and paste it over `<your endpoint URL>` in the program.cs file.</span></span> <span data-ttu-id="65e95-152">Ardından portaldan birincil anahtarı kopyalayın ve üzerinden yapıştırın `<your primary key>`.</span><span class="sxs-lookup"><span data-stu-id="65e95-152">Then copy the PRIMARY KEY from the portal and paste it over `<your primary key>`.</span></span> <span data-ttu-id="65e95-153">Kaldırdığınızdan emin olun `<` ve `>` , değerlerinden.</span><span class="sxs-lookup"><span data-stu-id="65e95-153">Be sure to remove the `<` and `>` from your values.</span></span>

![C# konsol uygulaması oluşturmak için NoSQL Öğreticisi tarafından kullanılan Azure portal ekran görüntüsü.](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-keys.png)

## <span data-ttu-id="65e95-156"><a id="instantiate"></a>DocumentClient örneği</span><span class="sxs-lookup"><span data-stu-id="65e95-156"><a id="instantiate"></a>Instantiate the DocumentClient</span></span>

<span data-ttu-id="65e95-157">Şimdi, yeni bir örneğini oluşturmak **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="65e95-157">Now, create a new instance of the **DocumentClient**.</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
```

## <span data-ttu-id="65e95-158"><a id="create-database"></a>Bir veritabanı oluşturun</span><span class="sxs-lookup"><span data-stu-id="65e95-158"><a id="create-database"></a>Create a database</span></span>

<span data-ttu-id="65e95-159">Ardından, bir Azure Cosmos DB Oluştur [veritabanı](documentdb-resources.md#databases) kullanarak [Documentclient](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) yöntemi veya [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) yöntemi  **DocumentClient** sınıfıyla [DocumentDB .NET SDK'sı](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="65e95-159">Next, create an Azure Cosmos DB [database](documentdb-resources.md#databases) by using the [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method or [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of the **DocumentClient** class from the [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="65e95-160">Veritabanı, koleksiyonlar genelinde bölümlenmiş JSON belgesi depolama alanının mantıksal bir kapsayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="65e95-160">A database is the logical container of JSON document storage partitioned across collections.</span></span>

```csharp
await client.CreateDatabaseAsync(new Database { Id = "db" });
```
## <a name="decide-on-a-partition-key"></a><span data-ttu-id="65e95-161">Bir bölüm anahtarı karar verin</span><span class="sxs-lookup"><span data-stu-id="65e95-161">Decide on a partition key</span></span> 

<span data-ttu-id="65e95-162">Koleksiyonlar, belgeleri depolamak için kapsayıcılardır.</span><span class="sxs-lookup"><span data-stu-id="65e95-162">Collections are containers for storing documents.</span></span> <span data-ttu-id="65e95-163">Mantıksal kaynaklar ve yapabilirsiniz [bir veya daha fazla fiziksel bölüm span](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="65e95-163">They are logical resources and can [span one or more physical partitions](partition-data.md).</span></span> <span data-ttu-id="65e95-164">A [bölüm anahtarı](documentdb-partition-data.md) verilerinizi sunucuları veya bölümleri arasında dağıtmak için kullanılan belgelerinizi içinde bir özellik (veya yol) olduğu.</span><span class="sxs-lookup"><span data-stu-id="65e95-164">A [partition key](documentdb-partition-data.md) is a property (or path) within your documents that is used to distribute your data among the servers or partitions.</span></span> <span data-ttu-id="65e95-165">Aynı bölüm anahtarına sahip tüm belgeleri aynı bölümünde depolanır.</span><span class="sxs-lookup"><span data-stu-id="65e95-165">All documents with the same partition key are stored in the same partition.</span></span> 

<span data-ttu-id="65e95-166">Bölüm anahtarı belirleme koleksiyonu oluşturmadan önce yapmak için önemli bir karardır.</span><span class="sxs-lookup"><span data-stu-id="65e95-166">Determining a partition key is an important decision to make before you create a collection.</span></span> <span data-ttu-id="65e95-167">Bölüm anahtarlarını özelliği (veya yol) birden fazla sunucu veya bölümleri arasında verilerinizi dağıtmak için Azure Cosmos DB tarafından kullanılan belgelerinizi ağdadır.</span><span class="sxs-lookup"><span data-stu-id="65e95-167">Partition keys are a property (or path) within your documents that can be used by Azure Cosmos DB to distribute your data among multiple servers or partitions.</span></span> <span data-ttu-id="65e95-168">Cosmos DB bölüm anahtarı değerini karma hale getirir ve karma hale getirilen sonuç belge depolanacağı bölüm belirlemek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="65e95-168">Cosmos DB hashes the partition key value and uses the hashed result to determine the partition in which to store the document.</span></span> <span data-ttu-id="65e95-169">Aynı bölüm anahtarına sahip tüm belgeleri aynı bölümünde depolanır ve bir koleksiyon oluşturulduktan sonra bölüm anahtarlarını değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="65e95-169">All documents with the same partition key are stored in the same partition, and partition keys cannot be changed once a collection is created.</span></span> 

<span data-ttu-id="65e95-170">Bu öğretici için bölüm anahtarı kümesine oluşturacağız `/deviceId` tek bir bölüm böylece tüm verileri tek bir cihaz için depolanır.</span><span class="sxs-lookup"><span data-stu-id="65e95-170">For this tutorial, we're going to set the partition key to `/deviceId` so that the all the data for a single device is stored in a single partition.</span></span> <span data-ttu-id="65e95-171">Değerlerin her biri en aynı frekansı hakkında verilerinizi büyür ve koleksiyon tam verimini elde Cosmos DB yükünü dengelemek sağlamak için kullanılır, çok sayıda sahip bir bölüm anahtarı seçmek istediğiniz.</span><span class="sxs-lookup"><span data-stu-id="65e95-171">You want to choose a partition key that has a large number of values, each of which are used at about the same frequency to ensure Cosmos DB can load balance as your data grows and achieve the full throughput of the collection.</span></span> 

<span data-ttu-id="65e95-172">Bölümleme hakkında daha fazla bilgi için bkz: [bölümleme ve Azure Cosmos veritabanı ölçek?](partition-data.md)</span><span class="sxs-lookup"><span data-stu-id="65e95-172">For more information about partitioning, see [How to partition and scale in Azure Cosmos DB?](partition-data.md)</span></span> 

## <span data-ttu-id="65e95-173"><a id="CreateColl"></a>Bir koleksiyon oluşturma</span><span class="sxs-lookup"><span data-stu-id="65e95-173"><a id="CreateColl"></a>Create a collection</span></span> 

<span data-ttu-id="65e95-174">Biz bizim bölüm anahtarı bildiğinize göre `/deviceId`, oluşturma sağlayan bir [koleksiyonu](documentdb-resources.md#collections) kullanarak [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) yöntemi veya [CreateDocumentCollectionIfNotExistsAsync ](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) yöntemi **DocumentClient** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="65e95-174">Now that we know our partition key, `/deviceId`, lets create a [collection](documentdb-resources.md#collections) by using the [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method or [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="65e95-175">Koleksiyon, JSON belgelerinin ve tüm ilişkili JavaScript uygulama mantığının bir kapsayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="65e95-175">A collection is a container of JSON documents and any associated JavaScript application logic.</span></span> 

> [!WARNING]
> <span data-ttu-id="65e95-176">Uygulamanın Azure Cosmos DB ile iletişim kurmak işleme ayırma gibi bir koleksiyon oluşturma, fiyatlandırmaya vardır.</span><span class="sxs-lookup"><span data-stu-id="65e95-176">Creating a collection has pricing implications, as you are reserving throughput for the application to communicate with Azure Cosmos DB.</span></span> <span data-ttu-id="65e95-177">Daha fazla ayrıntı için lütfen ziyaret bizim [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/cosmos-db/)</span><span class="sxs-lookup"><span data-stu-id="65e95-177">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

```csharp
// Collection for device telemetry. Here the JSON property deviceId is used  
// as the partition key to spread across partitions. Configured for 2500 RU/s  
// throughput and an indexing policy that supports sorting against any  
// number or string property. .
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 2500 });
```

<span data-ttu-id="65e95-178">Bu yöntem için Azure Cosmos DB ve hizmet hükümleri istenen işlemeyi temel alan bölüm sayısı çağırın bir REST API sağlar.</span><span class="sxs-lookup"><span data-stu-id="65e95-178">This method makes a REST API call to Azure Cosmos DB, and the service provisions a number of partitions based on the requested throughput.</span></span> <span data-ttu-id="65e95-179">Performansınızı SDK'sını kullanarak geliştikçe koleksiyonu verimini değiştirebilir veya [Azure portal](set-throughput.md).</span><span class="sxs-lookup"><span data-stu-id="65e95-179">You can change the throughput of a collection as your performance needs evolve using the SDK or the [Azure portal](set-throughput.md).</span></span>

## <span data-ttu-id="65e95-180"><a id="CreateDoc"></a>JSON belgeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="65e95-180"><a id="CreateDoc"></a>Create JSON documents</span></span>
<span data-ttu-id="65e95-181">Şimdi bazı JSON belgeleri Azure Cosmos Veritabanına ekler.</span><span class="sxs-lookup"><span data-stu-id="65e95-181">Let's insert some JSON documents into Azure Cosmos DB.</span></span> <span data-ttu-id="65e95-182">Bir [belge](documentdb-resources.md#documents), **DocumentClient** sınıfının [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) yöntemi kullanılarak oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="65e95-182">A [document](documentdb-resources.md#documents) can be created by using the [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="65e95-183">Belgeler, kullanıcı tanımlı (rastgele) JSON içerikleridir.</span><span class="sxs-lookup"><span data-stu-id="65e95-183">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="65e95-184">Bu örnek sınıfı okuma bir aygıtı ve Documentclient bir koleksiyona okuma yeni aygıt eklemek için bir çağrı içerir.</span><span class="sxs-lookup"><span data-stu-id="65e95-184">This sample class contains a device reading, and a call to CreateDocumentAsync to insert a new device reading into a collection.</span></span>

```csharp
public class DeviceReading
{
    [JsonProperty("id")]
    public string Id;

    [JsonProperty("deviceId")]
    public string DeviceId;

    [JsonConverter(typeof(IsoDateTimeConverter))]
    [JsonProperty("readingTime")]
    public DateTime ReadingTime;

    [JsonProperty("metricType")]
    public string MetricType;

    [JsonProperty("unit")]
    public string Unit;

    [JsonProperty("metricValue")]
    public double MetricValue;
  }

// Create a document. Here the partition key is extracted 
// as "XMS-0001" based on the collection definition
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "coll"),
    new DeviceReading
    {
        Id = "XMS-001-FE24C",
        DeviceId = "XMS-0001",
        MetricType = "Temperature",
        MetricValue = 105.00,
        Unit = "Fahrenheit",
        ReadingTime = DateTime.UtcNow
    });
```
## <a name="read-data"></a><span data-ttu-id="65e95-185">Verileri okuma</span><span class="sxs-lookup"><span data-stu-id="65e95-185">Read data</span></span>

<span data-ttu-id="65e95-186">Şimdi ReadDocumentAsync yöntemi kullanılarak kimliği ve bölüm anahtarı tarafından belgeyi okuyun.</span><span class="sxs-lookup"><span data-stu-id="65e95-186">Let's read the document by its partition key and Id using the ReadDocumentAsync method.</span></span> <span data-ttu-id="65e95-187">Okumaları PartitionKey değeri içerdiğini unutmayın (karşılık gelen `x-ms-documentdb-partitionkey` REST API istek üstbilgisinde).</span><span class="sxs-lookup"><span data-stu-id="65e95-187">Note that the reads include a PartitionKey value (corresponding to the `x-ms-documentdb-partitionkey` request header in the REST API).</span></span>

```csharp
// Read document. Needs the partition key and the Id to be specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;
```

## <a name="update-data"></a><span data-ttu-id="65e95-188">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="65e95-188">Update data</span></span>

<span data-ttu-id="65e95-189">Şimdi şimdi ReplaceDocumentAsync yöntemini kullanarak bazı verileri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="65e95-189">Now let's update some data using the ReplaceDocumentAsync method.</span></span>

```csharp
// Update the document. Partition key is not required, again extracted from the document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);
```

## <a name="delete-data"></a><span data-ttu-id="65e95-190">Verileri silme</span><span class="sxs-lookup"><span data-stu-id="65e95-190">Delete data</span></span>

<span data-ttu-id="65e95-191">Şimdi bir belgenin bölüm anahtarı kimliği DeleteDocumentAsync yöntemini kullanarak silip olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="65e95-191">Now lets delete a document by partition key and id by using the DeleteDocumentAsync method.</span></span>

```csharp
// Delete a document. The partition key is required.
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```
## <a name="query-partitioned-collections"></a><span data-ttu-id="65e95-192">Bölümlenmiş koleksiyonlar sorgulama</span><span class="sxs-lookup"><span data-stu-id="65e95-192">Query partitioned collections</span></span>

<span data-ttu-id="65e95-193">Bölümlenmiş koleksiyonlar verileri sorguladığınızda Azure Cosmos DB sorgu otomatik olarak (varsa) filtrede belirtilen bölüm anahtarı değerine karşılık gelen bölümleri yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="65e95-193">When you query data in partitioned collections, Azure Cosmos DB automatically routes the query to the partitions corresponding to the partition key values specified in the filter (if there are any).</span></span> <span data-ttu-id="65e95-194">Örneğin, bu sorgu "XMS-0001" Bölüm anahtarı içeren bölümün yalnızca yönlendirilir.</span><span class="sxs-lookup"><span data-stu-id="65e95-194">For example, this query is routed to just the partition containing the partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="65e95-195">Aşağıdaki sorgu bir filtre bölüm anahtarı (DeviceID) sahip değil ve bölümün dizin karşı yürütüldüğü tüm bölümler için Dağıtılmış.</span><span class="sxs-lookup"><span data-stu-id="65e95-195">The following query does not have a filter on the partition key (DeviceId) and is fanned out to all partitions where it is executed against the partition's index.</span></span> <span data-ttu-id="65e95-196">EnableCrossPartitionQuery belirtmek zorunda Not (`x-ms-documentdb-query-enablecrosspartition` REST API'sindeki) SDK'sını bölümler bir sorguyu çalıştırmak için.</span><span class="sxs-lookup"><span data-stu-id="65e95-196">Note that you have to specify the EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in the REST API) to have the SDK to execute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

## <a name="parallel-query-execution"></a><span data-ttu-id="65e95-197">Paralel sorgu yürütme</span><span class="sxs-lookup"><span data-stu-id="65e95-197">Parallel query execution</span></span>
<span data-ttu-id="65e95-198">Azure Cosmos DB DocumentDB SDK'ları 1.9.0 ve hatta bunlar çok sayıda bölüm touch gerektiğinde bölümlenmiş koleksiyonlar, düşük gecikme süresi sorguları gerçekleştirmesine izin destek paralel sorgu yürütme seçenekleri üstünde.</span><span class="sxs-lookup"><span data-stu-id="65e95-198">The Azure Cosmos DB DocumentDB SDKs 1.9.0 and above support parallel query execution options, which allow you to perform low latency queries against partitioned collections, even when they need to touch a large number of partitions.</span></span> <span data-ttu-id="65e95-199">Örneğin, aşağıdaki sorguyu bölümler paralel olarak çalıştırmak için yapılandırılır.</span><span class="sxs-lookup"><span data-stu-id="65e95-199">For example, the following query is configured to run in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="65e95-200">Aşağıdaki parametreleri ayarlama tarafından paralel sorgu yürütme yönetebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="65e95-200">You can manage parallel query execution by tuning the following parameters:</span></span>

* <span data-ttu-id="65e95-201">Ayarlayarak `MaxDegreeOfParallelism`, yani, en fazla eşzamanlı ağ bağlantı sayısı koleksiyonunun bölümlere paralellik derecesini kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65e95-201">By setting `MaxDegreeOfParallelism`, you can control the degree of parallelism i.e., the maximum number of simultaneous network connections to the collection's partitions.</span></span> <span data-ttu-id="65e95-202">Bu ayar, -1 olarak paralellik derecesini SDK tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="65e95-202">If you set this to -1, the degree of parallelism is managed by the SDK.</span></span> <span data-ttu-id="65e95-203">Varsa `MaxDegreeOfParallelism` varsayılan değer, belirtilen veya ayarlanmış 0 değil, tek bir ağ bağlantısı koleksiyonunun bölümlere olacaktır.</span><span class="sxs-lookup"><span data-stu-id="65e95-203">If the `MaxDegreeOfParallelism` is not specified or set to 0, which is the default value, there will be a single network connection to the collection's partitions.</span></span>
* <span data-ttu-id="65e95-204">Ayarlayarak `MaxBufferedItemCount`, sorgu gecikme süresi ve istemci tarafı bellek kullanımı devre dışı ticari.</span><span class="sxs-lookup"><span data-stu-id="65e95-204">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="65e95-205">Bu parametreyi veya bu ayarlarsanız -1 olarak paralel sorgu yürütme sırasında arabelleğe alınan öğe sayısı SDK tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="65e95-205">If you omit this parameter or set this to -1, the number of items buffered during parallel query execution is managed by the SDK.</span></span>

<span data-ttu-id="65e95-206">Koleksiyon aynı durumu verildiğinde, paralel sorgu sonuçları seri yürütme olduğu gibi aynı sırada döndürür.</span><span class="sxs-lookup"><span data-stu-id="65e95-206">Given the same state of the collection, a parallel query will return results in the same order as in serial execution.</span></span> <span data-ttu-id="65e95-207">Sıralama (ORDER BY ve/veya üst) içeren bir çapraz bölüm sorgusu gerçekleştirirken, DocumentDB SDK'sı paralel sorguda bölümler sorunları ve genel olarak sipariş edilen sonuçlar için istemci tarafı kısmen sıralanmış sonuçları birleştirir.</span><span class="sxs-lookup"><span data-stu-id="65e95-207">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), the DocumentDB SDK issues the query in parallel across partitions and merges partially sorted results in the client side to produce globally ordered results.</span></span>

## <a name="execute-stored-procedures"></a><span data-ttu-id="65e95-208">Saklı yordam yürütme</span><span class="sxs-lookup"><span data-stu-id="65e95-208">Execute stored procedures</span></span>
<span data-ttu-id="65e95-209">Son olarak, aynı aygıt kimliği belgelerle karşı atomik işlemleri örneğin yürütebilir, toplamalar veya bir cihazı tek bir belgenin en son durumunu projenize aşağıdaki kodu ekleyerek koruma durumunda.</span><span class="sxs-lookup"><span data-stu-id="65e95-209">Lastly, you can execute atomic transactions against documents with the same device ID, e.g. if you're maintaining aggregates or the latest state of a device in a single document by adding the following code to your project.</span></span>

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```

<span data-ttu-id="65e95-210">Ve bu kadar!</span><span class="sxs-lookup"><span data-stu-id="65e95-210">And that's it!</span></span> <span data-ttu-id="65e95-211">ana veri dağıtım bölümler ölçeklendirilmesine olanak bölüm anahtarı kullanan bir Azure Cosmos DB uygulama bileşenlerinin olanlardır.</span><span class="sxs-lookup"><span data-stu-id="65e95-211">those are the main components of an Azure Cosmos DB application that uses a partition key to efficiently scale data distribution across partitions.</span></span>  

## <a name="clean-up-resources"></a><span data-ttu-id="65e95-212">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="65e95-212">Clean up resources</span></span>

<span data-ttu-id="65e95-213">Bu uygulamayı kullanmaya devam etmek için değil kullanacaksanız, bu öğreticide aşağıdaki adımlarla Azure portal tarafından oluşturulan tüm kaynakları silin:</span><span class="sxs-lookup"><span data-stu-id="65e95-213">If you're not going to continue to use this app, delete all resources created by this tutorial in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="65e95-214">Azure portalında sol taraftaki menüden **kaynak grupları** ve oluşturduğunuz kaynak benzersiz adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="65e95-214">From the left-hand menu in the Azure portal, click **Resource groups** and then click the unique name of the resource you created.</span></span> 
2. <span data-ttu-id="65e95-215">Kaynak grubu sayfanızda, **Sil**'e tıklayın, metin kutusuna silinecek kaynağın adını yazın ve ardından **Sil**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="65e95-215">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65e95-216">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="65e95-216">Next steps</span></span>

<span data-ttu-id="65e95-217">Bu öğreticide, aşağıdakileri yaptığınızdan:</span><span class="sxs-lookup"><span data-stu-id="65e95-217">In this tutorial, you've done the following:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="65e95-218">Bir Azure Cosmos DB hesabı oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="65e95-218">Created an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="65e95-219">Bir veritabanı ve koleksiyonu bir bölüm anahtarı ile oluşturulan</span><span class="sxs-lookup"><span data-stu-id="65e95-219">Created a database and collection with a partition key</span></span>
> * <span data-ttu-id="65e95-220">Oluşturulan JSON belgeleri</span><span class="sxs-lookup"><span data-stu-id="65e95-220">Created JSON documents</span></span>
> * <span data-ttu-id="65e95-221">Bir belge güncelleştirildi</span><span class="sxs-lookup"><span data-stu-id="65e95-221">Updated a document</span></span>
> * <span data-ttu-id="65e95-222">Sorgulanan bölümlenmiş koleksiyonlar</span><span class="sxs-lookup"><span data-stu-id="65e95-222">Queried partitioned collections</span></span>
> * <span data-ttu-id="65e95-223">Saklı yordam çalıştı</span><span class="sxs-lookup"><span data-stu-id="65e95-223">Ran a stored procedure</span></span>
> * <span data-ttu-id="65e95-224">Bir belge silindi</span><span class="sxs-lookup"><span data-stu-id="65e95-224">Deleted a document</span></span>
> * <span data-ttu-id="65e95-225">Bir veritabanı silindi</span><span class="sxs-lookup"><span data-stu-id="65e95-225">Deleted a database</span></span>

<span data-ttu-id="65e95-226">Şimdi, sonraki öğretici devam ve Cosmos DB hesabınıza ek verileri alın.</span><span class="sxs-lookup"><span data-stu-id="65e95-226">You can now proceed to the next tutorial and import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="65e95-227">Azure Cosmos DB hesabınıza veri aktarma</span><span class="sxs-lookup"><span data-stu-id="65e95-227">Import data into Azure Cosmos DB</span></span>](import-data.md)
