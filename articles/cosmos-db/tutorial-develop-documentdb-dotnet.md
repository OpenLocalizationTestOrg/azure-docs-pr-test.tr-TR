---
title: "Azure Cosmos DB: Merhaba DocumentDB API .NET geliştirme | Microsoft Docs"
description: "Bilgi nasıl toodevelop Azure Cosmos veritabanı DocumentDB .NET kullanarak API ile"
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
ms.openlocfilehash: 0d3d17afa782054c8fdf3cbac421e5a5d0a6800c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmosdb-develop-with-hello-documentdb-api-in-net"></a><span data-ttu-id="146b8-103">Azure CosmosDB: hello .NET API DocumentDB ile geliştirme</span><span class="sxs-lookup"><span data-stu-id="146b8-103">Azure CosmosDB: Develop with hello DocumentDB API in .NET</span></span>

<span data-ttu-id="146b8-104">Azure Cosmos DB, Microsoft'un genel olarak dağıtılmış çok modelli veritabanı hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="146b8-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="146b8-105">Hızlı bir şekilde oluşturmak ve belge, anahtar/değer ve grafik veritabanları, her biri hello genel dağıtım ve yatay ölçek özelliklerini Azure Cosmos DB'nin hello çekirdek yararlı sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="146b8-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="146b8-106">Bu öğretici nasıl toocreate bir Azure Cosmos DB hesabı kullanarak Azure portal hello ve ardından bir belge veritabanı ve koleksiyonu oluşturun gösterir bir [bölüm anahtarı](documentdb-partition-data.md#partition-keys) hello kullanarak [DocumentDB .NET API](documentdb-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="146b8-106">This tutorial demonstrates how toocreate an Azure Cosmos DB account using hello Azure portal, and then create a document database and collection with a [partition key](documentdb-partition-data.md#partition-keys) using hello [DocumentDB .NET API](documentdb-introduction.md).</span></span> <span data-ttu-id="146b8-107">Verilerinizi büyüdükçe bir koleksiyon oluşturduğunuzda bir bölüm anahtarı tanımlayarak, uygulamanızın tooscale harcamadan hazırlanır.</span><span class="sxs-lookup"><span data-stu-id="146b8-107">By defining a partition key when you create a collection, your application is prepared tooscale effortlessly as your data grows.</span></span> 

<span data-ttu-id="146b8-108">Bu öğretici kapsar hello aşağıdaki görevleri hello kullanarak [DocumentDB .NET API](documentdb-sdk-dotnet.md):</span><span class="sxs-lookup"><span data-stu-id="146b8-108">This tutorial covers hello following tasks by using hello [DocumentDB .NET API](documentdb-sdk-dotnet.md):</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="146b8-109">Azure Cosmos DB hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="146b8-109">Create an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="146b8-110">Bir bölüm anahtarının bir veritabanınızı ve koleksiyonunuzu oluşturun</span><span class="sxs-lookup"><span data-stu-id="146b8-110">Create a database and collection with a partition key</span></span>
> * <span data-ttu-id="146b8-111">JSON belgeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="146b8-111">Create JSON documents</span></span>
> * <span data-ttu-id="146b8-112">Bir belgeyi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="146b8-112">Update a document</span></span>
> * <span data-ttu-id="146b8-113">Bölümlenmiş koleksiyonlar sorgulama</span><span class="sxs-lookup"><span data-stu-id="146b8-113">Query partitioned collections</span></span>
> * <span data-ttu-id="146b8-114">Saklı yordamları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="146b8-114">Run stored procedures</span></span>
> * <span data-ttu-id="146b8-115">Bir belgeyi silme</span><span class="sxs-lookup"><span data-stu-id="146b8-115">Delete a document</span></span>
> * <span data-ttu-id="146b8-116">Bir veritabanını silin</span><span class="sxs-lookup"><span data-stu-id="146b8-116">Delete a database</span></span>

## <a name="prerequisites"></a><span data-ttu-id="146b8-117">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="146b8-117">Prerequisites</span></span>
<span data-ttu-id="146b8-118">Merhaba aşağıdaki sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="146b8-118">Please make sure you have hello following:</span></span>

* <span data-ttu-id="146b8-119">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="146b8-119">An active Azure account.</span></span> <span data-ttu-id="146b8-120">Bir aboneliğiniz yoksa [ücretsiz bir hesap](https://azure.microsoft.com/free/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="146b8-120">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="146b8-121">Alternatif olarak, hello kullanabilirsiniz [Azure Cosmos DB öykünücüsü](local-emulator.md) toouse hello Azure DocumentDB hizmetinin Geliştirme amaçlı öykünen yerel bir ortam isterseniz bu öğretici için.</span><span class="sxs-lookup"><span data-stu-id="146b8-121">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial if you'd like toouse a local environment that emulates hello Azure DocumentDB service for development purposes.</span></span>
* <span data-ttu-id="146b8-122">[Visual Studio](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="146b8-122">[Visual Studio](http://www.visualstudio.com/).</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="146b8-123">Azure Cosmos DB hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="146b8-123">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="146b8-124">Hello Azure portalında bir Azure Cosmos DB hesabı oluşturarak başlayalım.</span><span class="sxs-lookup"><span data-stu-id="146b8-124">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>

> [!TIP]
> * <span data-ttu-id="146b8-125">Zaten Azure Cosmos DB hesabınız var mı?</span><span class="sxs-lookup"><span data-stu-id="146b8-125">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="146b8-126">Bu durumda, İleri çok atlayabilirsiniz[, Visual Studio çözümü ayarlama](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="146b8-126">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="146b8-127">Bir Azure DocumentDB hesabına sahip miydiniz?</span><span class="sxs-lookup"><span data-stu-id="146b8-127">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="146b8-128">Bu nedenle, hesabınızı şimdi bir Azure Cosmos DB hesabı ise ve şimdi çok atlayabilirsiniz[, Visual Studio çözümü ayarlama](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="146b8-128">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="146b8-129">Hello Azure Cosmos DB öykünücüsü kullanıyorsanız, lütfen hello adımları izleyin [Azure Cosmos DB öykünücüsü](local-emulator.md) toosetup öykünücüsü hello ve İleri çok atlayabilirsiniz[, Visual Studio çözümünü kurmak](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="146b8-129">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="146b8-130"><a id="SetupVS"></a>Visual Studio çözümünüzü kurma</span><span class="sxs-lookup"><span data-stu-id="146b8-130"><a id="SetupVS"></a>Set up your Visual Studio solution</span></span>
1. <span data-ttu-id="146b8-131">Bilgisayarınızda **Visual Studio**'yu açın.</span><span class="sxs-lookup"><span data-stu-id="146b8-131">Open **Visual Studio** on your computer.</span></span>
2. <span data-ttu-id="146b8-132">Merhaba üzerinde **dosya** menüsünde, select **yeni**ve ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="146b8-132">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="146b8-133">Merhaba, **yeni proje** iletişim kutusunda **şablonları** / **Visual C#** / **konsol uygulaması (.NET Framework)**, projenizi adlandırın ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="146b8-133">In hello **New Project** dialog, select **Templates** / **Visual C#** / **Console App (.NET Framework)**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="146b8-134">![Merhaba yeni proje penceresinin ekran görüntüsü](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="146b8-134">![Screen shot of hello New Project window](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)</span></span>

4. <span data-ttu-id="146b8-135">Merhaba, **Çözüm Gezgini**, Visual Studio çözümünüzün yeni konsol uygulamanızın üzerinde sağ tıklayın ve ardından **NuGet paketlerini Yönet...**</span><span class="sxs-lookup"><span data-stu-id="146b8-135">In hello **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![Merhaba sağ tıklama menüsünün hello proje için ekran görüntüsü](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="146b8-137">Merhaba, **NuGet** sekmesini tıklatın, **Gözat**ve türü **documentdb** hello arama kutusuna.</span><span class="sxs-lookup"><span data-stu-id="146b8-137">In hello **NuGet** tab, click **Browse**, and type **documentdb** in hello search box.</span></span>
<!---stopped here--->
6. <span data-ttu-id="146b8-138">Merhaba sonuçları içinde bulmak **Microsoft.Azure.DocumentDB** tıklatıp **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="146b8-138">Within hello results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="146b8-139">Merhaba hello Azure Cosmos DB istemci kitaplığı için paket kimliği [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).</span><span class="sxs-lookup"><span data-stu-id="146b8-139">hello package ID for hello Azure Cosmos DB Client Library is [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).</span></span>
   <span data-ttu-id="146b8-140">![Azure Cosmos DB istemci SDK'sını bulmak için NuGet menüsünün hello ekran görüntüsü](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="146b8-140">![Screen shot of hello NuGet Menu for finding Azure Cosmos DB Client SDK](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="146b8-141">Değişiklikleri toohello çözümü gözden geçirme hakkında bir ileti alırsanız tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="146b8-141">If you get a message about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="146b8-142">Lisans kabulü hakkında bir ileti alırsanız **Kabul ediyorum**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="146b8-142">If you get a message about license acceptance, click **I accept**.</span></span>

## <span data-ttu-id="146b8-143"><a id="Connect"></a>Başvuruları tooyour proje ekleyin</span><span class="sxs-lookup"><span data-stu-id="146b8-143"><a id="Connect"></a>Add references tooyour project</span></span>
<span data-ttu-id="146b8-144">Bu öğretici sağla hello DocumentDB API kod parçacıkları gerekli toocreate ve güncelleştirme Azure Cosmos DB kaynakları projenize hello kalan adımları.</span><span class="sxs-lookup"><span data-stu-id="146b8-144">hello remaining steps in this tutorial provide hello DocumentDB API code snippets required toocreate and update Azure Cosmos DB resources in your project.</span></span>

<span data-ttu-id="146b8-145">İlk olarak, bu başvuruları tooyour uygulama ekleyin.</span><span class="sxs-lookup"><span data-stu-id="146b8-145">First, add these references tooyour application.</span></span>
<!---These aren't added by default when you install hello pkg?--->

```csharp
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

## <span data-ttu-id="146b8-146"><a id="add-references"></a>Uygulamanızı bağlama</span><span class="sxs-lookup"><span data-stu-id="146b8-146"><a id="add-references"></a>Connect your app</span></span>

<span data-ttu-id="146b8-147">Ardından, bu iki sabitleri ekleyin ve *istemci* uygulamanızda değişken.</span><span class="sxs-lookup"><span data-stu-id="146b8-147">Next, add these two constants and your *client* variable in your application.</span></span>

```csharp
private const string EndpointUrl = "<your endpoint URL>";
private const string PrimaryKey = "<your primary key>";
private DocumentClient client;
```

<span data-ttu-id="146b8-148">Head toohello geri [Azure portal](https://portal.azure.com) tooretrieve uç noktasının URL'sini ve birincil anahtar.</span><span class="sxs-lookup"><span data-stu-id="146b8-148">Then, head back toohello [Azure portal](https://portal.azure.com) tooretrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="146b8-149">Merhaba uç noktasının URL'sini ve birincil anahtar, uygulama toounderstand için gerekli olan nerede tooconnect ve Azure Cosmos DB tootrust için uygulamanızın bağlantı.</span><span class="sxs-lookup"><span data-stu-id="146b8-149">hello endpoint URL and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="146b8-150">İçinde Azure portal Merhaba, tooyour Azure Cosmos DB hesap gidin, tıklatın **anahtarları**ve ardından **okuma-yazma anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="146b8-150">In hello Azure portal, navigate tooyour Azure Cosmos DB account, click **Keys**, and then click **Read-write Keys**.</span></span>

<span data-ttu-id="146b8-151">Merhaba URI hello Portal'dan kopyalayın ve üzerinden yapıştırın `<your endpoint URL>` hello program.cs dosyasındaki.</span><span class="sxs-lookup"><span data-stu-id="146b8-151">Copy hello URI from hello portal and paste it over `<your endpoint URL>` in hello program.cs file.</span></span> <span data-ttu-id="146b8-152">BİRİNCİL anahtar hello portalından hello kopyalayıp üzerinden yapıştırın sonra `<your primary key>`.</span><span class="sxs-lookup"><span data-stu-id="146b8-152">Then copy hello PRIMARY KEY from hello portal and paste it over `<your primary key>`.</span></span> <span data-ttu-id="146b8-153">Emin tooremove hello olması `<` ve `>` , değerlerinden.</span><span class="sxs-lookup"><span data-stu-id="146b8-153">Be sure tooremove hello `<` and `>` from your values.</span></span>

![Hello Azure portal ekran görüntüsü bir C# konsol uygulaması hello NoSQL Öğreticisi toocreate tarafından kullanılır.](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-keys.png)

## <span data-ttu-id="146b8-156"><a id="instantiate"></a>Merhaba DocumentClient örneği</span><span class="sxs-lookup"><span data-stu-id="146b8-156"><a id="instantiate"></a>Instantiate hello DocumentClient</span></span>

<span data-ttu-id="146b8-157">Şimdi, hello yeni bir örneğini oluşturmak **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="146b8-157">Now, create a new instance of hello **DocumentClient**.</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
```

## <span data-ttu-id="146b8-158"><a id="create-database"></a>Bir veritabanı oluşturun</span><span class="sxs-lookup"><span data-stu-id="146b8-158"><a id="create-database"></a>Create a database</span></span>

<span data-ttu-id="146b8-159">Ardından, bir Azure Cosmos DB Oluştur [veritabanı](documentdb-resources.md#databases) hello kullanarak [Documentclient](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) yöntemi veya [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) hello yöntemi  **DocumentClient** hello sınıfından [DocumentDB .NET SDK'sı](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="146b8-159">Next, create an Azure Cosmos DB [database](documentdb-resources.md#databases) by using hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method or [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of hello **DocumentClient** class from hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="146b8-160">Bir veritabanı hello mantıksal, koleksiyonlar genelinde bölümlenmiş JSON belgesi depolama kapsayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="146b8-160">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

```csharp
await client.CreateDatabaseAsync(new Database { Id = "db" });
```
## <a name="decide-on-a-partition-key"></a><span data-ttu-id="146b8-161">Bir bölüm anahtarı karar verin</span><span class="sxs-lookup"><span data-stu-id="146b8-161">Decide on a partition key</span></span> 

<span data-ttu-id="146b8-162">Koleksiyonlar, belgeleri depolamak için kapsayıcılardır.</span><span class="sxs-lookup"><span data-stu-id="146b8-162">Collections are containers for storing documents.</span></span> <span data-ttu-id="146b8-163">Mantıksal kaynaklar ve yapabilirsiniz [bir veya daha fazla fiziksel bölüm span](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="146b8-163">They are logical resources and can [span one or more physical partitions](partition-data.md).</span></span> <span data-ttu-id="146b8-164">A [bölüm anahtarı](documentdb-partition-data.md) özelliği (veya yol) verileriniz hello sunucuları veya bölümleri arasında kullanılan toodistribute olan belgelerinizi içinde bulunur.</span><span class="sxs-lookup"><span data-stu-id="146b8-164">A [partition key](documentdb-partition-data.md) is a property (or path) within your documents that is used toodistribute your data among hello servers or partitions.</span></span> <span data-ttu-id="146b8-165">Tüm belgeleri aynı bölüm anahtarı depolanır hello ile aynı bölüme hello.</span><span class="sxs-lookup"><span data-stu-id="146b8-165">All documents with hello same partition key are stored in hello same partition.</span></span> 

<span data-ttu-id="146b8-166">Bir koleksiyon oluşturmadan önce bir bölüm anahtarı belirleme önemli karar toomake olur.</span><span class="sxs-lookup"><span data-stu-id="146b8-166">Determining a partition key is an important decision toomake before you create a collection.</span></span> <span data-ttu-id="146b8-167">Bölüm anahtarlarını olabilir, belgeler içinde bir özellik (veya yol) olan birden fazla sunucu veya bölümleri arasında verilerinizi Azure Cosmos DB toodistribute tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="146b8-167">Partition keys are a property (or path) within your documents that can be used by Azure Cosmos DB toodistribute your data among multiple servers or partitions.</span></span> <span data-ttu-id="146b8-168">Cosmos DB hello bölüm anahtarı değerini karıştırır ve karma hello sonuç toodetermine hello bölüm hangi toostore hello belgede kullanır.</span><span class="sxs-lookup"><span data-stu-id="146b8-168">Cosmos DB hashes hello partition key value and uses hello hashed result toodetermine hello partition in which toostore hello document.</span></span> <span data-ttu-id="146b8-169">Tüm belgeleri aynı bölüm anahtarı depolanır hello ile aynı bölüme hello ve bölüm anahtarlarını bir koleksiyon oluşturulduktan sonra değiştirilemez.</span><span class="sxs-lookup"><span data-stu-id="146b8-169">All documents with hello same partition key are stored in hello same partition, and partition keys cannot be changed once a collection is created.</span></span> 

<span data-ttu-id="146b8-170">Bu öğretici için tooset hello bölüm anahtarı çok yapacağız`/deviceId` bu nedenle, hello tüm hello verileri tek bir cihazı tek bir bölüm içinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="146b8-170">For this tutorial, we're going tooset hello partition key too`/deviceId` so that hello all hello data for a single device is stored in a single partition.</span></span> <span data-ttu-id="146b8-171">Toochoose her biri kullanılan değerleri, çok sayıda sahip bir bölüm anahtarı istediğiniz verilerinizi büyür ve hello koleksiyonunun hello tam verimlilik elde adresindeki hello hakkında aynı sıklığı tooensure Cosmos DB yükünü dengelemek.</span><span class="sxs-lookup"><span data-stu-id="146b8-171">You want toochoose a partition key that has a large number of values, each of which are used at about hello same frequency tooensure Cosmos DB can load balance as your data grows and achieve hello full throughput of hello collection.</span></span> 

<span data-ttu-id="146b8-172">Bölümleme hakkında daha fazla bilgi için bkz: [nasıl toopartition ve Azure Cosmos veritabanı ölçek?](partition-data.md)</span><span class="sxs-lookup"><span data-stu-id="146b8-172">For more information about partitioning, see [How toopartition and scale in Azure Cosmos DB?](partition-data.md)</span></span> 

## <span data-ttu-id="146b8-173"><a id="CreateColl"></a>Bir koleksiyon oluşturma</span><span class="sxs-lookup"><span data-stu-id="146b8-173"><a id="CreateColl"></a>Create a collection</span></span> 

<span data-ttu-id="146b8-174">Biz bizim bölüm anahtarı bildiğinize göre `/deviceId`, oluşturma sağlayan bir [koleksiyonu](documentdb-resources.md#collections) hello kullanarak [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) yöntemi veya [ CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) hello yöntemi **DocumentClient** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="146b8-174">Now that we know our partition key, `/deviceId`, lets create a [collection](documentdb-resources.md#collections) by using hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method or [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="146b8-175">Koleksiyon, JSON belgelerinin ve tüm ilişkili JavaScript uygulama mantığının bir kapsayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="146b8-175">A collection is a container of JSON documents and any associated JavaScript application logic.</span></span> 

> [!WARNING]
> <span data-ttu-id="146b8-176">Üretilen iş ile Azure Cosmos DB hello uygulama toocommunicate için ayırma gibi bir koleksiyon oluşturma, fiyatlandırmaya vardır.</span><span class="sxs-lookup"><span data-stu-id="146b8-176">Creating a collection has pricing implications, as you are reserving throughput for hello application toocommunicate with Azure Cosmos DB.</span></span> <span data-ttu-id="146b8-177">Daha fazla ayrıntı için lütfen ziyaret bizim [fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/cosmos-db/)</span><span class="sxs-lookup"><span data-stu-id="146b8-177">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

```csharp
// Collection for device telemetry. Here hello JSON property deviceId is used  
// as hello partition key toospread across partitions. Configured for 2500 RU/s  
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

<span data-ttu-id="146b8-178">Bu yöntem yaptığı bir REST API tooAzure Cosmos DB çağırın ve hizmet hükümleri hello istenen işlemeyi temel alan bölüm sayısı hello.</span><span class="sxs-lookup"><span data-stu-id="146b8-178">This method makes a REST API call tooAzure Cosmos DB, and hello service provisions a number of partitions based on hello requested throughput.</span></span> <span data-ttu-id="146b8-179">Performansınızı hello SDK veya hello kullanarak gelişmesi gibi bir koleksiyon hello verimini değiştirebilirsiniz [Azure portal](set-throughput.md).</span><span class="sxs-lookup"><span data-stu-id="146b8-179">You can change hello throughput of a collection as your performance needs evolve using hello SDK or hello [Azure portal](set-throughput.md).</span></span>

## <span data-ttu-id="146b8-180"><a id="CreateDoc"></a>JSON belgeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="146b8-180"><a id="CreateDoc"></a>Create JSON documents</span></span>
<span data-ttu-id="146b8-181">Şimdi bazı JSON belgeleri Azure Cosmos Veritabanına ekler.</span><span class="sxs-lookup"><span data-stu-id="146b8-181">Let's insert some JSON documents into Azure Cosmos DB.</span></span> <span data-ttu-id="146b8-182">A [belge](documentdb-resources.md#documents) hello kullanarak oluşturulan [Documentclient](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) hello yöntemi **DocumentClient** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="146b8-182">A [document](documentdb-resources.md#documents) can be created by using hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="146b8-183">Belgeler, kullanıcı tanımlı (rastgele) JSON içerikleridir.</span><span class="sxs-lookup"><span data-stu-id="146b8-183">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="146b8-184">Bu örnek sınıf bir koleksiyona okuma yeni bir cihaz aygıt okuma ve çağrısı tooCreateDocumentAsync tooinsert içerir.</span><span class="sxs-lookup"><span data-stu-id="146b8-184">This sample class contains a device reading, and a call tooCreateDocumentAsync tooinsert a new device reading into a collection.</span></span>

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

// Create a document. Here hello partition key is extracted 
// as "XMS-0001" based on hello collection definition
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
## <a name="read-data"></a><span data-ttu-id="146b8-185">Verileri okuma</span><span class="sxs-lookup"><span data-stu-id="146b8-185">Read data</span></span>

<span data-ttu-id="146b8-186">Şimdi hello ReadDocumentAsync yöntemi kullanılarak kimliği ve bölüm anahtarı tarafından hello belgeyi okuyun.</span><span class="sxs-lookup"><span data-stu-id="146b8-186">Let's read hello document by its partition key and Id using hello ReadDocumentAsync method.</span></span> <span data-ttu-id="146b8-187">Merhaba okuma PartitionKey değeri içerdiğini unutmayın (karşılık gelen toohello `x-ms-documentdb-partitionkey` hello REST API istek üstbilgisinde).</span><span class="sxs-lookup"><span data-stu-id="146b8-187">Note that hello reads include a PartitionKey value (corresponding toohello `x-ms-documentdb-partitionkey` request header in hello REST API).</span></span>

```csharp
// Read document. Needs hello partition key and hello Id toobe specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;
```

## <a name="update-data"></a><span data-ttu-id="146b8-188">Verileri güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="146b8-188">Update data</span></span>

<span data-ttu-id="146b8-189">Şimdi şimdi hello ReplaceDocumentAsync yöntemini kullanarak bazı verileri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="146b8-189">Now let's update some data using hello ReplaceDocumentAsync method.</span></span>

```csharp
// Update hello document. Partition key is not required, again extracted from hello document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);
```

## <a name="delete-data"></a><span data-ttu-id="146b8-190">Verileri silme</span><span class="sxs-lookup"><span data-stu-id="146b8-190">Delete data</span></span>

<span data-ttu-id="146b8-191">Şimdi bir belgenin bölüm anahtarı kimliği hello DeleteDocumentAsync yöntemini kullanarak silip olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="146b8-191">Now lets delete a document by partition key and id by using hello DeleteDocumentAsync method.</span></span>

```csharp
// Delete a document. hello partition key is required.
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```
## <a name="query-partitioned-collections"></a><span data-ttu-id="146b8-192">Bölümlenmiş koleksiyonlar sorgulama</span><span class="sxs-lookup"><span data-stu-id="146b8-192">Query partitioned collections</span></span>

<span data-ttu-id="146b8-193">Bölümlenmiş koleksiyonlarda Azure Cosmos DB verileri otomatik olarak sorguladığınızda yolları (varsa) hello filtrede belirtilen toohello bölüm anahtar değerlerine karşılık gelen sorgu toohello bölümleri hello.</span><span class="sxs-lookup"><span data-stu-id="146b8-193">When you query data in partitioned collections, Azure Cosmos DB automatically routes hello query toohello partitions corresponding toohello partition key values specified in hello filter (if there are any).</span></span> <span data-ttu-id="146b8-194">Örneğin, bu sorgu yönlendirilmiş toojust hello bölüm içeren hello bölüm anahtarı "XMS-0001" olur.</span><span class="sxs-lookup"><span data-stu-id="146b8-194">For example, this query is routed toojust hello partition containing hello partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="146b8-195">Merhaba aşağıdaki sorguyu hello bölüm anahtarı (DeviceID) üzerinde bir filtre yok ve hello bölümünün dizin karşı yürütüldüğü tooall bölümleri çıkışı dağıtılmış.</span><span class="sxs-lookup"><span data-stu-id="146b8-195">hello following query does not have a filter on hello partition key (DeviceId) and is fanned out tooall partitions where it is executed against hello partition's index.</span></span> <span data-ttu-id="146b8-196">Toospecify hello EnableCrossPartitionQuery sahip unutmayın (`x-ms-documentdb-query-enablecrosspartition` hello REST API içinde) toohave hello SDK tooexecute bölümleri arasında bir sorgu.</span><span class="sxs-lookup"><span data-stu-id="146b8-196">Note that you have toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in hello REST API) toohave hello SDK tooexecute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

## <a name="parallel-query-execution"></a><span data-ttu-id="146b8-197">Paralel sorgu yürütme</span><span class="sxs-lookup"><span data-stu-id="146b8-197">Parallel query execution</span></span>
<span data-ttu-id="146b8-198">Hello Azure Cosmos DB DocumentDB SDK'ları 1.9.0 ve Destek tooperform düşük gecikme süresi izin paralel sorgu yürütme seçeneklerini sorgular bölümlenmiş koleksiyonlar karşı bile tootouch gerektiğinde çok sayıda bölüm.</span><span class="sxs-lookup"><span data-stu-id="146b8-198">hello Azure Cosmos DB DocumentDB SDKs 1.9.0 and above support parallel query execution options, which allow you tooperform low latency queries against partitioned collections, even when they need tootouch a large number of partitions.</span></span> <span data-ttu-id="146b8-199">Örneğin, sorgu aşağıdaki hello paralel yapılandırılmış toorun bölümler ' dir.</span><span class="sxs-lookup"><span data-stu-id="146b8-199">For example, hello following query is configured toorun in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="146b8-200">Şu parametreler hello ayarlama tarafından paralel sorgu yürütme yönetebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="146b8-200">You can manage parallel query execution by tuning hello following parameters:</span></span>

* <span data-ttu-id="146b8-201">Ayarlayarak `MaxDegreeOfParallelism`, hello paralellik derecesi başka bir deyişle, hello en fazla eşzamanlı ağ bağlantıları toohello koleksiyonunun bölüm sayısı kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="146b8-201">By setting `MaxDegreeOfParallelism`, you can control hello degree of parallelism i.e., hello maximum number of simultaneous network connections toohello collection's partitions.</span></span> <span data-ttu-id="146b8-202">Bu çok 1 ayarlarsanız, hello paralellik derecesi hello SDK tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="146b8-202">If you set this too-1, hello degree of parallelism is managed by hello SDK.</span></span> <span data-ttu-id="146b8-203">Merhaba, `MaxDegreeOfParallelism` belirtilmemişse veya ayarlama hello varsayılan değer olan too0 bir tek bir ağ bağlantısı toohello koleksiyonunun bölümleri olacaktır.</span><span class="sxs-lookup"><span data-stu-id="146b8-203">If hello `MaxDegreeOfParallelism` is not specified or set too0, which is hello default value, there will be a single network connection toohello collection's partitions.</span></span>
* <span data-ttu-id="146b8-204">Ayarlayarak `MaxBufferedItemCount`, sorgu gecikme süresi ve istemci tarafı bellek kullanımı devre dışı ticari.</span><span class="sxs-lookup"><span data-stu-id="146b8-204">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="146b8-205">Bu parametreyi veya bu çok 1 ayarlarsanız hello paralel sorgu yürütme sırasında arabelleğe alınan öğe sayısı hello SDK tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="146b8-205">If you omit this parameter or set this too-1, hello number of items buffered during parallel query execution is managed by hello SDK.</span></span>

<span data-ttu-id="146b8-206">Merhaba verilen aynı duruma hello koleksiyonunun bir paralel sorgu döndürecektir sonuçları seri yürütme olduğu gibi aynı sipariş hello içinde.</span><span class="sxs-lookup"><span data-stu-id="146b8-206">Given hello same state of hello collection, a parallel query will return results in hello same order as in serial execution.</span></span> <span data-ttu-id="146b8-207">(ORDER BY ve/veya üst) sıralama içeren bir çapraz bölüm sorgusu gerçekleştirirken hello DocumentDB SDK'sı hello sorgu paralel bölümler sorunları ve genel sonuçları sıralı hello istemci tarafı tooproduce kısmen sıralanmış sonuçları birleştirir.</span><span class="sxs-lookup"><span data-stu-id="146b8-207">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), hello DocumentDB SDK issues hello query in parallel across partitions and merges partially sorted results in hello client side tooproduce globally ordered results.</span></span>

## <a name="execute-stored-procedures"></a><span data-ttu-id="146b8-208">Saklı yordam yürütme</span><span class="sxs-lookup"><span data-stu-id="146b8-208">Execute stored procedures</span></span>
<span data-ttu-id="146b8-209">Son olarak, atomik işlemleri belgelerle karşı yürütebilir aynı cihaz kimliği, örneğin hello toplamalar koruma veya kod tooyour projesi aşağıdaki hello ekleyerek bir cihazı tek bir belgenin en son durumunu hello.</span><span class="sxs-lookup"><span data-stu-id="146b8-209">Lastly, you can execute atomic transactions against documents with hello same device ID, e.g. if you're maintaining aggregates or hello latest state of a device in a single document by adding hello following code tooyour project.</span></span>

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```

<span data-ttu-id="146b8-210">Ve bu kadar!</span><span class="sxs-lookup"><span data-stu-id="146b8-210">And that's it!</span></span> <span data-ttu-id="146b8-211">Merhaba ana bölümleri arasında bir bölüm anahtarı tooefficiently ölçek veri dağıtım kullanan bir Azure Cosmos DB uygulama bileşenlerinin olanlardır.</span><span class="sxs-lookup"><span data-stu-id="146b8-211">those are hello main components of an Azure Cosmos DB application that uses a partition key tooefficiently scale data distribution across partitions.</span></span>  

## <a name="clean-up-resources"></a><span data-ttu-id="146b8-212">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="146b8-212">Clean up resources</span></span>

<span data-ttu-id="146b8-213">Toocontinue toouse bu uygulamayı değil kullanacaksanız, Bu öğretici hello Azure portalında aşağıdaki adımları hello ile oluşturulan tüm kaynakları silin:</span><span class="sxs-lookup"><span data-stu-id="146b8-213">If you're not going toocontinue toouse this app, delete all resources created by this tutorial in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="146b8-214">Merhaba sol taraftaki menüden hello Azure portal'ın, **kaynak grupları** ve benzersiz bir ad hello oluşturduğunuz hello kaynağının'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="146b8-214">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello unique name of hello resource you created.</span></span> 
2. <span data-ttu-id="146b8-215">Kaynak grubu sayfanızda tıklatın **silmek**hello metin kutusuna hello kaynak toodelete hello adını yazın ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="146b8-215">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="146b8-216">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="146b8-216">Next steps</span></span>

<span data-ttu-id="146b8-217">Bu öğreticide, hello aşağıdakileri yaptığınızdan:</span><span class="sxs-lookup"><span data-stu-id="146b8-217">In this tutorial, you've done hello following:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="146b8-218">Bir Azure Cosmos DB hesabı oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="146b8-218">Created an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="146b8-219">Bir veritabanı ve koleksiyonu bir bölüm anahtarı ile oluşturulan</span><span class="sxs-lookup"><span data-stu-id="146b8-219">Created a database and collection with a partition key</span></span>
> * <span data-ttu-id="146b8-220">Oluşturulan JSON belgeleri</span><span class="sxs-lookup"><span data-stu-id="146b8-220">Created JSON documents</span></span>
> * <span data-ttu-id="146b8-221">Bir belge güncelleştirildi</span><span class="sxs-lookup"><span data-stu-id="146b8-221">Updated a document</span></span>
> * <span data-ttu-id="146b8-222">Sorgulanan bölümlenmiş koleksiyonlar</span><span class="sxs-lookup"><span data-stu-id="146b8-222">Queried partitioned collections</span></span>
> * <span data-ttu-id="146b8-223">Saklı yordam çalıştı</span><span class="sxs-lookup"><span data-stu-id="146b8-223">Ran a stored procedure</span></span>
> * <span data-ttu-id="146b8-224">Bir belge silindi</span><span class="sxs-lookup"><span data-stu-id="146b8-224">Deleted a document</span></span>
> * <span data-ttu-id="146b8-225">Bir veritabanı silindi</span><span class="sxs-lookup"><span data-stu-id="146b8-225">Deleted a database</span></span>

<span data-ttu-id="146b8-226">Şimdi toohello sonraki öğretici devam ve ek veri tooyour Cosmos DB hesap içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="146b8-226">You can now proceed toohello next tutorial and import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="146b8-227">Azure Cosmos DB hesabınıza veri aktarma</span><span class="sxs-lookup"><span data-stu-id="146b8-227">Import data into Azure Cosmos DB</span></span>](import-data.md)
