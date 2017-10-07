---
title: "Azure Cosmos DB: Merhaba grafik API'si, .NET geliştirme | Microsoft Docs"
description: "Bilgi nasıl toodevelop Azure Cosmos veritabanı DocumentDB .NET kullanarak API ile"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: cc8df0be-672b-493e-95a4-26dd52632261
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.custom: mvc
ms.openlocfilehash: 12e435d8169aeee6e818dac4a3b66c7a0ec5f2d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-graph-api-in-net"></a><span data-ttu-id="2daf1-103">Azure Cosmos DB: Merhaba grafik API'si, .NET geliştirin</span><span class="sxs-lookup"><span data-stu-id="2daf1-103">Azure Cosmos DB: Develop with hello Graph API in .NET</span></span>
<span data-ttu-id="2daf1-104">Azure Cosmos DB Microsoft'un Genel dağıtılmış birden çok model veritabanı hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="2daf1-104">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span></span> <span data-ttu-id="2daf1-105">Hızlı bir şekilde oluşturmak ve belge, anahtar/değer ve grafik veritabanları, her biri hello genel dağıtım ve yatay ölçek özelliklerini Azure Cosmos DB'nin hello çekirdek yararlı sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2daf1-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="2daf1-106">Bu öğretici bir Azure Cosmos DB hesabı kullanarak toocreate hello nasıl Azure portal ve nasıl gösterir toocreate bir grafik veritabanı ve kapsayıcı.</span><span class="sxs-lookup"><span data-stu-id="2daf1-106">This tutorial demonstrates how toocreate an Azure Cosmos DB account using hello Azure portal and how toocreate a graph database and container.</span></span> <span data-ttu-id="2daf1-107">Merhaba uygulama dört kişiler hello kullanarak basit bir sosyal ağ oluşturur [grafik API'si](graph-sdk-dotnet.md) (Önizleme), ardından erişir ve Gremlin kullanarak hello grafik sorgular.</span><span class="sxs-lookup"><span data-stu-id="2daf1-107">hello application then creates a simple social network with four people using hello [Graph API](graph-sdk-dotnet.md) (preview), then traverses and queries hello graph using Gremlin.</span></span>

<span data-ttu-id="2daf1-108">Bu öğretici hello aşağıdaki görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="2daf1-108">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2daf1-109">Azure Cosmos DB hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2daf1-109">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="2daf1-110">Bir grafik veritabanı ve kapsayıcı oluşturun</span><span class="sxs-lookup"><span data-stu-id="2daf1-110">Create a graph database and container</span></span>
> * <span data-ttu-id="2daf1-111">Köşeleri ve kenarları too.NET nesneleri seri hale</span><span class="sxs-lookup"><span data-stu-id="2daf1-111">Serialize vertices and edges too.NET objects</span></span>
> * <span data-ttu-id="2daf1-112">Köşeleri ve kenarları ekleme</span><span class="sxs-lookup"><span data-stu-id="2daf1-112">Add vertices and edges</span></span>
> * <span data-ttu-id="2daf1-113">Sorgu hello grafik Gremlin kullanma</span><span class="sxs-lookup"><span data-stu-id="2daf1-113">Query hello graph using Gremlin</span></span>

## <a name="graphs-in-azure-cosmos-db"></a><span data-ttu-id="2daf1-114">Azure Cosmos DB grafiklerde</span><span class="sxs-lookup"><span data-stu-id="2daf1-114">Graphs in Azure Cosmos DB</span></span>
<span data-ttu-id="2daf1-115">Azure Cosmos DB toocreate, güncelleştirme ve hello kullanarak sorgu grafikleri kullanabilirsiniz [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="2daf1-115">You can use Azure Cosmos DB toocreate, update, and query graphs using hello [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) library.</span></span> <span data-ttu-id="2daf1-116">Merhaba Microsoft.Azure.Graph kitaplığı, bir tek genişletme yöntemi sağlar `CreateGremlinQuery<T>` hello üstünde `DocumentClient` tooexecute Gremlin sorguları sınıfı.</span><span class="sxs-lookup"><span data-stu-id="2daf1-116">hello Microsoft.Azure.Graph library provides a single extension method `CreateGremlinQuery<T>` on top of hello `DocumentClient` class tooexecute Gremlin queries.</span></span>

<span data-ttu-id="2daf1-117">Gremlin destekleyen işlevsel bir programlama dili yazma işlemleri (DML) ve sorgu ve çapraz geçişi işlemleri ' dir.</span><span class="sxs-lookup"><span data-stu-id="2daf1-117">Gremlin is a functional programming language that supports write operations (DML) and query and traversal operations.</span></span> <span data-ttu-id="2daf1-118">Biz bu makalede tooget birkaç örneklerde, başlatılan Gremlin ile kapsar.</span><span class="sxs-lookup"><span data-stu-id="2daf1-118">We cover a few examples in this article tooget your started with Gremlin.</span></span> <span data-ttu-id="2daf1-119">Bkz: [Gremlin sorguları](gremlin-support.md) ayrıntılı kılavuz Gremlin özelliklerinden Azure Cosmos DB içinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="2daf1-119">See [Gremlin queries](gremlin-support.md) for a detailed walkthrough of Gremlin capabilities available in Azure Cosmos DB.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="2daf1-120">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="2daf1-120">Prerequisites</span></span>
<span data-ttu-id="2daf1-121">Merhaba aşağıdaki sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="2daf1-121">Please make sure you have hello following:</span></span>

* <span data-ttu-id="2daf1-122">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="2daf1-122">An active Azure account.</span></span> <span data-ttu-id="2daf1-123">Bir aboneliğiniz yoksa [ücretsiz bir hesap](https://azure.microsoft.com/free/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2daf1-123">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="2daf1-124">Alternatif olarak, hello kullanabilirsiniz [Azure DocumentDB öykünücüsü](local-emulator.md) Bu öğretici için.</span><span class="sxs-lookup"><span data-stu-id="2daf1-124">Alternatively, you can use hello [Azure DocumentDB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="2daf1-125">[Visual Studio](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="2daf1-125">[Visual Studio](http://www.visualstudio.com/).</span></span>

## <a name="create-database-account"></a><span data-ttu-id="2daf1-126">Veritabanı hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="2daf1-126">Create database account</span></span>

<span data-ttu-id="2daf1-127">Hello Azure portalında bir Azure Cosmos DB hesabı oluşturarak başlayalım.</span><span class="sxs-lookup"><span data-stu-id="2daf1-127">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="2daf1-128">Zaten Azure Cosmos DB hesabınız var mı?</span><span class="sxs-lookup"><span data-stu-id="2daf1-128">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="2daf1-129">Bu durumda, İleri çok atlayabilirsiniz[, Visual Studio çözümü ayarlama](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="2daf1-129">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="2daf1-130">Bir Azure DocumentDB hesabına sahip miydiniz?</span><span class="sxs-lookup"><span data-stu-id="2daf1-130">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="2daf1-131">Bu nedenle, hesabınızı şimdi bir Azure Cosmos DB hesabı ise ve şimdi çok atlayabilirsiniz[, Visual Studio çözümü ayarlama](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="2daf1-131">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="2daf1-132">Hello Azure Cosmos DB öykünücüsü kullanıyorsanız, lütfen hello adımları izleyin [Azure Cosmos DB öykünücüsü](local-emulator.md) toosetup öykünücüsü hello ve İleri çok atlayabilirsiniz[, Visual Studio çözümünü kurmak](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="2daf1-132">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
> 

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <span data-ttu-id="2daf1-133"><a id="SetupVS"></a>Visual Studio çözümünüzü kurma</span><span class="sxs-lookup"><span data-stu-id="2daf1-133"><a id="SetupVS"></a>Set up your Visual Studio solution</span></span>
1. <span data-ttu-id="2daf1-134">Bilgisayarınızda **Visual Studio**'yu açın.</span><span class="sxs-lookup"><span data-stu-id="2daf1-134">Open **Visual Studio** on your computer.</span></span>
2. <span data-ttu-id="2daf1-135">Merhaba üzerinde **dosya** menüsünde, select **yeni**ve ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="2daf1-135">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="2daf1-136">Merhaba, **yeni proje** iletişim kutusunda **şablonları** / **Visual C#** / **konsol uygulaması (.NET Framework)**, projenizi adlandırın ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="2daf1-136">In hello **New Project** dialog, select **Templates** / **Visual C#** / **Console App (.NET Framework)**, name your project, and then click **OK**.</span></span>
4. <span data-ttu-id="2daf1-137">Merhaba, **Çözüm Gezgini**, Visual Studio çözümünüzün yeni konsol uygulamanızın üzerinde sağ tıklayın ve ardından **NuGet paketlerini Yönet...**</span><span class="sxs-lookup"><span data-stu-id="2daf1-137">In hello **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
5. <span data-ttu-id="2daf1-138">Merhaba, **NuGet** sekmesini tıklatın, **Gözat**ve türü **Microsoft.Azure.Graphs** hello arama kutusu ve onay hello **yayın öncesi sürümleriiçerir**.</span><span class="sxs-lookup"><span data-stu-id="2daf1-138">In hello **NuGet** tab, click **Browse**, and type **Microsoft.Azure.Graphs** in hello search box, and check hello **Include prerelease versions**.</span></span>
6. <span data-ttu-id="2daf1-139">Merhaba sonuçları içinde bulmak **Microsoft.Azure.Graphs** tıklatıp **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="2daf1-139">Within hello results, find **Microsoft.Azure.Graphs** and click **Install**.</span></span>
   
   <span data-ttu-id="2daf1-140">Değişiklikleri toohello çözümü gözden geçirme hakkında bir ileti alırsanız tıklatın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="2daf1-140">If you get a message about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="2daf1-141">Lisans kabulü hakkında bir ileti alırsanız **Kabul ediyorum**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2daf1-141">If you get a message about license acceptance, click **I accept**.</span></span>
   
    <span data-ttu-id="2daf1-142">Merhaba `Microsoft.Azure.Graphs` kitaplığı, bir tek genişletme yöntemi sağlar `CreateGremlinQuery<T>` Gremlin işlemleri yürütmek.</span><span class="sxs-lookup"><span data-stu-id="2daf1-142">hello `Microsoft.Azure.Graphs` library provides a single extension method `CreateGremlinQuery<T>` for executing Gremlin operations.</span></span> <span data-ttu-id="2daf1-143">Gremlin destekleyen işlevsel bir programlama dili yazma işlemleri (DML) ve sorgu ve çapraz geçişi işlemleri ' dir.</span><span class="sxs-lookup"><span data-stu-id="2daf1-143">Gremlin is a functional programming language that supports write operations (DML) and query and traversal operations.</span></span> <span data-ttu-id="2daf1-144">Biz bu makalede tooget birkaç örneklerde, başlatılan Gremlin ile kapsar.</span><span class="sxs-lookup"><span data-stu-id="2daf1-144">We cover a few examples in this article tooget your started with Gremlin.</span></span> <span data-ttu-id="2daf1-145">[Gremlin sorguları](gremlin-support.md) Azure Cosmos DB'de Gremlin özelliklerinin ayrıntılı bir kılavuz vardır.</span><span class="sxs-lookup"><span data-stu-id="2daf1-145">[Gremlin queries](gremlin-support.md) has a detailed walkthrough of Gremlin capabilities in Azure Cosmos DB.</span></span>

## <span data-ttu-id="2daf1-146"><a id="add-references"></a>Uygulamanızı bağlama</span><span class="sxs-lookup"><span data-stu-id="2daf1-146"><a id="add-references"></a>Connect your app</span></span>

<span data-ttu-id="2daf1-147">Bu iki sabitleri ekleyin ve *istemci* uygulamanızda değişken.</span><span class="sxs-lookup"><span data-stu-id="2daf1-147">Add these two constants and your *client* variable in your application.</span></span> 

```csharp
string endpoint = ConfigurationManager.AppSettings["Endpoint"]; 
string authKey = ConfigurationManager.AppSettings["AuthKey"]; 
``` 
<span data-ttu-id="2daf1-148">Ardından, head geri toohello [Azure portal](https://portal.azure.com) tooretrieve uç noktasının URL'sini ve birincil anahtar.</span><span class="sxs-lookup"><span data-stu-id="2daf1-148">Next, head back toohello [Azure portal](https://portal.azure.com) tooretrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="2daf1-149">Merhaba uç noktasının URL'sini ve birincil anahtar, uygulama toounderstand için gerekli olan nerede tooconnect ve Azure Cosmos DB tootrust için uygulamanızın bağlantı.</span><span class="sxs-lookup"><span data-stu-id="2daf1-149">hello endpoint URL and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span> 

<span data-ttu-id="2daf1-150">İçinde Azure portal Merhaba, tooyour Azure Cosmos DB hesap gidin, tıklatın **anahtarları**ve ardından **okuma-yazma anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="2daf1-150">In hello Azure portal, navigate tooyour Azure Cosmos DB account, click **Keys**, and then click **Read-write Keys**.</span></span> 

<span data-ttu-id="2daf1-151">Merhaba URI hello Portal'dan kopyalayın ve üzerinden yapıştırın `Endpoint` hello uç nokta özelliğinde yukarıdaki.</span><span class="sxs-lookup"><span data-stu-id="2daf1-151">Copy hello URI from hello portal and paste it over `Endpoint` in hello endpoint property above.</span></span> <span data-ttu-id="2daf1-152">Sonra birincil anahtar hello portalından hello kopyalayın ve hello yapıştırma `AuthKey` yukarıdaki özelliği.</span><span class="sxs-lookup"><span data-stu-id="2daf1-152">Then copy hello PRIMARY KEY from hello portal and paste it into hello `AuthKey` property above.</span></span> 

<span data-ttu-id="2daf1-153">! [Hello Azure portal ekran görüntüsü bir C# uygulaması hello öğretici toocreate tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2daf1-153">![Screen shot of hello Azure portal used by hello tutorial toocreate a C# application.</span></span> <span data-ttu-id="2daf1-154">Bir Azure Cosmos DB hesap hello ANAHTARLAR düğmesi vurgulanmış üzerinde hello Azure Cosmos DB gezinti ve anahtarlar dikey penceresinde hello URI ve birincil anahtar değerleri vurgulanmış üzerinde hello gösterir] [Anahtarları]</span><span class="sxs-lookup"><span data-stu-id="2daf1-154">Shows an Azure Cosmos DB account hello KEYS button highlighted on hello Azure Cosmos DB navigation , and hello URI and PRIMARY KEY values highlighted on hello Keys blade][keys]</span></span> 
 
## <span data-ttu-id="2daf1-155"><a id="instantiate"></a>Merhaba DocumentClient örneği</span><span class="sxs-lookup"><span data-stu-id="2daf1-155"><a id="instantiate"></a>Instantiate hello DocumentClient</span></span> 
<span data-ttu-id="2daf1-156">Ardından, hello yeni bir örneğini oluşturun **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="2daf1-156">Next, create a new instance of hello **DocumentClient**.</span></span>  

```csharp 
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey); 
``` 

## <span data-ttu-id="2daf1-157"><a id="create-database"></a>Bir veritabanı oluşturun</span><span class="sxs-lookup"><span data-stu-id="2daf1-157"><a id="create-database"></a>Create a database</span></span> 

<span data-ttu-id="2daf1-158">Şimdi bir Azure Cosmos DB Oluştur [veritabanı](documentdb-resources.md#databases) hello kullanarak [Documentclient](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) yöntemi veya [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) hello yöntemi  **DocumentClient** hello sınıfından [DocumentDB .NET SDK'sı](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="2daf1-158">Now, create an Azure Cosmos DB [database](documentdb-resources.md#databases) by using hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method or [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of hello **DocumentClient** class from hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span></span>  

```csharp 
Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" }); 
``` 
 
## <a name="create-a-graph"></a><span data-ttu-id="2daf1-159">Bir grafik oluşturma</span><span class="sxs-lookup"><span data-stu-id="2daf1-159">Create a graph</span></span> 

<span data-ttu-id="2daf1-160">Ardından, bir grafik kapsayıcı hello kullanarak hello kullanarak oluşturma [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) yöntemi veya [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) hello yöntemi **DocumentClient**  sınıfı.</span><span class="sxs-lookup"><span data-stu-id="2daf1-160">Next, create a graph container by using hello using hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method or [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="2daf1-161">Bir koleksiyon, grafik varlıkların bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="2daf1-161">A collection is a container of graph entities.</span></span> 

```csharp 
DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync( 
    UriFactory.CreateDatabaseUri("graphdb"), 
    new DocumentCollection { Id = "graphcollz" }, 
    new RequestOptions { OfferThroughput = 1000 }); 
``` 

## <span data-ttu-id="2daf1-162"><a id="serializing"></a>Köşeleri ve kenarları too.NET nesneleri seri hale</span><span class="sxs-lookup"><span data-stu-id="2daf1-162"><a id="serializing"></a>Serialize vertices and edges too.NET objects</span></span>
<span data-ttu-id="2daf1-163">Azure Cosmos DB kullanır hello [GraphSON kablo biçiminde](gremlin-support.md), köşe, kenarları ve özellikleri için JSON şeması tanımlar.</span><span class="sxs-lookup"><span data-stu-id="2daf1-163">Azure Cosmos DB uses hello [GraphSON wire format](gremlin-support.md), which defines a JSON schema for vertices, edges, and properties.</span></span> <span data-ttu-id="2daf1-164">bir bağımlılık olarak JSON.NET Hello Azure Cosmos DB .NET SDK'sını içerir ve bu bize tooserialize/seri durumdan GraphSON biz kodda çalışabilirsiniz .NET nesneleri içine sağlar.</span><span class="sxs-lookup"><span data-stu-id="2daf1-164">hello Azure Cosmos DB .NET SDK includes JSON.NET as a dependency, and this allows us tooserialize/deserialize GraphSON into .NET objects that we can work with in code.</span></span>

<span data-ttu-id="2daf1-165">Örnek olarak, basit bir sosyal ağ dört kişilerle şimdi çalışır.</span><span class="sxs-lookup"><span data-stu-id="2daf1-165">As an example, let's work with a simple social network with four people.</span></span> <span data-ttu-id="2daf1-166">Nasıl tümleştirildiği incelenmektedir toocreate `Person` köşeleri eklemek `Knows` arasındaki ilişkileri ardından sorgu ve çapraz hello grafik toofind "arkadaş arkadaş" ilişkiler.</span><span class="sxs-lookup"><span data-stu-id="2daf1-166">We look at how toocreate `Person` vertices, add `Knows` relationships between them, then query and traverse hello graph toofind "friend of friend" relationships.</span></span> 

<span data-ttu-id="2daf1-167">Merhaba `Microsoft.Azure.Graphs.Elements` ad alanı sağlar `Vertex`, `Edge`, `Property` ve `VertexProperty` GraphSON yanıtları toowell tanımlı .NET nesnelerini seri durumdan çıkarmak için sınıflar.</span><span class="sxs-lookup"><span data-stu-id="2daf1-167">hello `Microsoft.Azure.Graphs.Elements` namespace provides `Vertex`, `Edge`, `Property` and `VertexProperty` classes for deserializing GraphSON responses toowell-defined .NET objects.</span></span>

## <a name="run-gremlin-using-creategremlinquery"></a><span data-ttu-id="2daf1-168">Gremlin CreateGremlinQuery kullanarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="2daf1-168">Run Gremlin using CreateGremlinQuery</span></span>
<span data-ttu-id="2daf1-169">SQL gibi gremlin okuma, yazma ve sorgu işlemleri destekler.</span><span class="sxs-lookup"><span data-stu-id="2daf1-169">Gremlin, like SQL, supports read, write, and query operations.</span></span> <span data-ttu-id="2daf1-170">Örneğin, hello aşağıdaki kod parçacığında nasıl toocreate köşeleri kenarlar kullanan bazı örnek sorgular gerçekleştirmek gösterir `CreateGremlinQuery<T>`ve zaman uyumsuz olarak kullanarak bu sonuçlarını yinelemek `ExecuteNextAsync` ve ' HasMoreResults.</span><span class="sxs-lookup"><span data-stu-id="2daf1-170">For example, hello following snippet shows how toocreate vertices, edges, perform some sample queries using `CreateGremlinQuery<T>`, and asynchronously iterate through these results using `ExecuteNextAsync` and \`HasMoreResults.</span></span>

```cs
Dictionary<string, string> gremlinQueries = new Dictionary<string, string>
{
    { "Cleanup",        "g.V().drop()" },
    { "AddVertex 1",    "g.addV('person').property('id', 'thomas').property('firstName', 'Thomas').property('age', 44)" },
    { "AddVertex 2",    "g.addV('person').property('id', 'mary').property('firstName', 'Mary').property('lastName', 'Andersen').property('age', 39)" },
    { "AddVertex 3",    "g.addV('person').property('id', 'ben').property('firstName', 'Ben').property('lastName', 'Miller')" },
    { "AddVertex 4",    "g.addV('person').property('id', 'robin').property('firstName', 'Robin').property('lastName', 'Wakefield')" },
    { "AddEdge 1",      "g.V('thomas').addE('knows').to(g.V('mary'))" },
    { "AddEdge 2",      "g.V('thomas').addE('knows').to(g.V('ben'))" },
    { "AddEdge 3",      "g.V('ben').addE('knows').to(g.V('robin'))" },
    { "UpdateVertex",   "g.V('thomas').property('age', 44)" },
    { "CountVertices",  "g.V().count()" },
    { "Filter Range",   "g.V().hasLabel('person').has('age', gt(40))" },
    { "Project",        "g.V().hasLabel('person').values('firstName')" },
    { "Sort",           "g.V().hasLabel('person').order().by('firstName', decr)" },
    { "Traverse",       "g.V('thomas').outE('knows').inV().hasLabel('person')" },
    { "Traverse 2x",    "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')" },
    { "Loop",           "g.V('thomas').repeat(out()).until(has('id', 'robin')).path()" },
    { "DropEdge",       "g.V('thomas').outE('knows').where(inV().has('id', 'mary')).drop()" },
    { "CountEdges",     "g.E().count()" },
    { "DropVertex",     "g.V('thomas').drop()" },
};

foreach (KeyValuePair<string, string> gremlinQuery in gremlinQueries)
{
    Console.WriteLine($"Running {gremlinQuery.Key}: {gremlinQuery.Value}");

    // hello CreateGremlinQuery method extensions allow you tooexecute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, gremlinQuery.Value);
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    Console.WriteLine();
}
```

## <a name="add-vertices-and-edges"></a><span data-ttu-id="2daf1-171">Köşeleri ve kenarları ekleme</span><span class="sxs-lookup"><span data-stu-id="2daf1-171">Add vertices and edges</span></span>

<span data-ttu-id="2daf1-172">Daha fazla ayrıntı bölüm önceki hello gösterilen hello Gremlin deyimlerini bakalım.</span><span class="sxs-lookup"><span data-stu-id="2daf1-172">Let's look at hello Gremlin statements shown in hello preceding section more detail.</span></span> <span data-ttu-id="2daf1-173">İlk biz Gremlin'ın kullanarak bazı köşeleri `addV` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="2daf1-173">First we some vertices using Gremlin's `addV` method.</span></span> <span data-ttu-id="2daf1-174">Örneğin, hello aşağıdaki kod parçacığında "Kişi" türündeki "Thomas Andersen" köşe ad, Soyadı ve yaş özelliklerini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="2daf1-174">For example, hello following snippet creates a "Thomas Andersen" vertex of type "Person", with properties for first name, last name, and age.</span></span>

```cs
// Create a vertex
IDocumentQuery<Vertex> createVertexQuery = client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.addV('person').property('firstName', 'Thomas')");

while (createVertexQuery.HasMoreResults)
{
    Vertex thomas = (await create.ExecuteNextAsync<Vertex>()).First();
}
```

<span data-ttu-id="2daf1-175">Biz Gremlin'ın kullanarak bu köşeleri arasında bazı kenarları oluşturup `addE` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="2daf1-175">Then we create some edges between these vertices using Gremlin's `addE` method.</span></span> 

```cs
// Add a "knows" edge
IDocumentQuery<Edge> createEdgeQuery = client.CreateGremlinQuery<Edge>(
    graphCollection, 
    "g.V('thomas').addE('knows').to(g.V('mary'))");

while (create.HasMoreResults)
{
    Edge thomasKnowsMaryEdge = (await create.ExecuteNextAsync<Edge>()).First();
}
```

<span data-ttu-id="2daf1-176">Biz kullanarak var olan bir köşe güncelleştirebilirsiniz `properties` Gremlin içinde adım.</span><span class="sxs-lookup"><span data-stu-id="2daf1-176">We can update an existing vertex by using `properties` step in Gremlin.</span></span> <span data-ttu-id="2daf1-177">Biz hello çağrısı tooexecute hello sorgu aracılığıyla atla `HasMoreResults` ve `ExecuteNextAsync` hello örnekler hello geri kalanı için.</span><span class="sxs-lookup"><span data-stu-id="2daf1-177">We skip hello call tooexecute hello query via `HasMoreResults` and `ExecuteNextAsync` for hello rest of hello examples.</span></span>

```cs
// Update a vertex
client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.V('thomas').property('age', 45)");
```

<span data-ttu-id="2daf1-178">Kenarları ve Gremlin'ın kullanarak köşeleri düşürebilir `drop` adım.</span><span class="sxs-lookup"><span data-stu-id="2daf1-178">You can drop edges and vertices using Gremlin's `drop` step.</span></span> <span data-ttu-id="2daf1-179">Gösteren parçacık İşte nasıl toodelete köşe ve bir sınır.</span><span class="sxs-lookup"><span data-stu-id="2daf1-179">Here's a snippet that shows how toodelete a vertex and an edge.</span></span> <span data-ttu-id="2daf1-180">Bir köşe bırakarak art arda silme hello işlemi gerçekleştirir Not kenarları ilişkilendirilmiş.</span><span class="sxs-lookup"><span data-stu-id="2daf1-180">Note that dropping a vertex performs a cascading delete of hello associated edges.</span></span>

```cs
// Drop an edge
client.CreateGremlinQuery(graphCollection, "g.E('thomasKnowsRobin').drop()");

// Drop a vertex
client.CreateGremlinQuery(graphCollection, "g.V('robin').drop()");
```

## <a name="query-hello-graph"></a><span data-ttu-id="2daf1-181">Sorgu hello grafiği</span><span class="sxs-lookup"><span data-stu-id="2daf1-181">Query hello graph</span></span>

<span data-ttu-id="2daf1-182">Sorgular ve ayrıca Gremlin kullanarak çapraz geçişlerine gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2daf1-182">You can perform queries and traversals also using Gremlin.</span></span> <span data-ttu-id="2daf1-183">Örneğin, aşağıdaki kod parçacığında hello nasıl toocount hello hello grafik tepe sayısı gösterilir:</span><span class="sxs-lookup"><span data-stu-id="2daf1-183">For example, hello following snippet shows how toocount hello number of vertices in hello graph:</span></span>

```cs
// Run a query toocount vertices
IDocumentQuery<int> countQuery = client.CreateGremlinQuery<int>(graphCollection, "g.V().count()");
```
<span data-ttu-id="2daf1-184">Gremlin'ın kullanarak filtreler gerçekleştirebilirsiniz `has` ve `hasLabel` adımları ve bunları birleştirmek kullanarak `and`, `or`, ve `not` toobuild daha karmaşık filtreler:</span><span class="sxs-lookup"><span data-stu-id="2daf1-184">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` toobuild more complex filters:</span></span>

```cs
// Run a query with filter
IDocumentQuery<Vertex> personsByAge = client.CreateGremlinQuery<Vertex>(
  graphCollection, 
  "g.V().hasLabel('person').has('age', gt(40))");
```

<span data-ttu-id="2daf1-185">Belirli özellikler hello sorgu sonuçlarındaki hello kullanarak proje `values` . adım:</span><span class="sxs-lookup"><span data-stu-id="2daf1-185">You can project certain properties in hello query results using hello `values` step:</span></span>

```cs
// Run a query with projection
IDocumentQuery<string> firstNames = client.CreateGremlinQuery<string>(
  graphCollection, 
  $"g.V().hasLabel('person').values('firstName')");
```

<span data-ttu-id="2daf1-186">Şu ana kadar yalnızca tüm veritabanındaki iş sorgu işleçleri gördük.</span><span class="sxs-lookup"><span data-stu-id="2daf1-186">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="2daf1-187">Toonavigate toorelated kenarları ve köşeleri gerektiğinde grafikleri hızlı ve verimli çapraz geçiş işlemleri için.</span><span class="sxs-lookup"><span data-stu-id="2daf1-187">Graphs are fast and efficient for traversal operations when you need toonavigate toorelated edges and vertices.</span></span> <span data-ttu-id="2daf1-188">Şimdi tüm arkadaşların Thomas bulun.</span><span class="sxs-lookup"><span data-stu-id="2daf1-188">Let's find all friends of Thomas.</span></span> <span data-ttu-id="2daf1-189">Biz Gremlin'ın kullanarak bunu `outE` tüm hello dışarı Thomas kenarları toofind adım sonra içinde köşe için toohello Gremlin'ın kullanarak bu kenarlarından çapraz geçiş yapan `inV` . adım:</span><span class="sxs-lookup"><span data-stu-id="2daf1-189">We do this by using Gremlin's `outE` step toofind all hello out-edges from Thomas, then traversing toohello in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
// Run a traversal (find friends of Thomas)
IDocumentQuery<Vertex> friendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person')");
```

<span data-ttu-id="2daf1-190">Merhaba sonraki sorgu gerçekleştirir iki atlama toofind tüm "çağırarak Thomas arkadaş arkadaş", `outE` ve `inV` iki kez.</span><span class="sxs-lookup"><span data-stu-id="2daf1-190">hello next query performs two hops toofind all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
// Run a traversal (find friends of friends of Thomas)
IDocumentQuery<Vertex> friendsOfFriendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')");
```

<span data-ttu-id="2daf1-191">Daha karmaşık sorgular derlemek ve Gremlin, kullanarak döngü gerçekleştirme ifadeleri hello dahil olmak üzere karıştırma filtre kullanan güçlü grafik geçişi mantığı uygulamanıza `loop` adım ve hello kullanarak uygulama koşullu Gezinti `choose` adım.</span><span class="sxs-lookup"><span data-stu-id="2daf1-191">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using hello `loop` step, and implementing conditional navigation using hello `choose` step.</span></span> <span data-ttu-id="2daf1-192">İle yapabilecekleriniz hakkında daha fazla bilgi [Gremlin Destek](gremlin-support.md)!</span><span class="sxs-lookup"><span data-stu-id="2daf1-192">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

<span data-ttu-id="2daf1-193">İşte bu kadar bu Azure Cosmos DB öğretici tamamlandı!</span><span class="sxs-lookup"><span data-stu-id="2daf1-193">That's it, this Azure Cosmos DB tutorial is complete!</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="2daf1-194">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="2daf1-194">Clean up resources</span></span>

<span data-ttu-id="2daf1-195">Bu uygulama toocontinue toouse denetlemeyecekseniz tüm kaynaklar Bu öğreticide hello Azure portal tarafından oluşturulan adımları toodelete aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="2daf1-195">If you're not going toocontinue toouse this app, use hello following steps toodelete all resources created by this tutorial in hello Azure portal.</span></span>  

1. <span data-ttu-id="2daf1-196">Merhaba sol taraftaki menüden hello Azure portal'ın, **kaynak grupları** ve ardından oluşturduğunuz hello kaynak hello adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="2daf1-196">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="2daf1-197">Kaynak grubu sayfanızda tıklatın **silmek**hello metin kutusuna hello kaynak toodelete hello adını yazın ve ardından **silmek**.</span><span class="sxs-lookup"><span data-stu-id="2daf1-197">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2daf1-198">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="2daf1-198">Next Steps</span></span>

<span data-ttu-id="2daf1-199">Bu öğreticide, hello aşağıdakileri yaptığınızdan:</span><span class="sxs-lookup"><span data-stu-id="2daf1-199">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2daf1-200">Bir Azure Cosmos DB hesabı oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="2daf1-200">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="2daf1-201">Bir grafik veritabanı ve kapsayıcı oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="2daf1-201">Created a graph database and container</span></span>
> * <span data-ttu-id="2daf1-202">Serileştirilmiş köşeleri ve kenarları too.NET nesneleri</span><span class="sxs-lookup"><span data-stu-id="2daf1-202">Serialized vertices and edges too.NET objects</span></span>
> * <span data-ttu-id="2daf1-203">Eklenen köşeleri ve kenarları</span><span class="sxs-lookup"><span data-stu-id="2daf1-203">Added vertices and edges</span></span>
> * <span data-ttu-id="2daf1-204">Sorgulanan hello grafik Gremlin kullanma</span><span class="sxs-lookup"><span data-stu-id="2daf1-204">Queried hello graph using Gremlin</span></span>

<span data-ttu-id="2daf1-205">Artık daha karmaşık sorgular oluşturabilir ve Gremlin kullanarak güçlü grafik geçişi mantığını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2daf1-205">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="2daf1-206">Gremlin kullanarak sorgulama</span><span class="sxs-lookup"><span data-stu-id="2daf1-206">Query using Gremlin</span></span>](tutorial-query-graph.md)
