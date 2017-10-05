---
title: "Azure Cosmos DB: grafik API'si, .NET geliştirme | Microsoft Docs"
description: ".NET kullanarak Azure Cosmos veritabanı DocumentDB API'si ile geliştirmeyi öğrenin"
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
ms.openlocfilehash: eeaa0c4f84a408815371742334d2ba7ce600b72f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-develop-with-the-graph-api-in-net"></a><span data-ttu-id="51ff3-103">Azure Cosmos DB: grafik API'si, .NET geliştirin</span><span class="sxs-lookup"><span data-stu-id="51ff3-103">Azure Cosmos DB: Develop with the Graph API in .NET</span></span>
<span data-ttu-id="51ff3-104">Azure Cosmos DB Microsoft'un Genel dağıtılmış birden çok model veritabanı hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="51ff3-104">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span></span> <span data-ttu-id="51ff3-105">Bu hizmetle belge, anahtar/değer ve grafik veritabanlarını kolayca oluşturup sorgulayabilir ve tüm bunları yaparken Azure Cosmos DB'nin genel dağıtım ve yatay ölçeklendirme özelliklerinden faydalanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51ff3-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="51ff3-106">Bu öğretici, Azure portalını kullanarak bir Azure Cosmos DB hesabının nasıl oluşturulacağını ve grafik veritabanı ve kapsayıcı nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="51ff3-106">This tutorial demonstrates how to create an Azure Cosmos DB account using the Azure portal and how to create a graph database and container.</span></span> <span data-ttu-id="51ff3-107">Uygulama basit bir sosyal ağ kullanan dört kişilerle oluşturur [grafik API'si](graph-sdk-dotnet.md) (Önizleme), ardından erişir ve Gremlin kullanarak grafik sorgular.</span><span class="sxs-lookup"><span data-stu-id="51ff3-107">The application then creates a simple social network with four people using the [Graph API](graph-sdk-dotnet.md) (preview), then traverses and queries the graph using Gremlin.</span></span>

<span data-ttu-id="51ff3-108">Bu öğretici, aşağıdaki görevleri içerir:</span><span class="sxs-lookup"><span data-stu-id="51ff3-108">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="51ff3-109">Azure Cosmos DB hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="51ff3-109">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="51ff3-110">Bir grafik veritabanı ve kapsayıcı oluşturun</span><span class="sxs-lookup"><span data-stu-id="51ff3-110">Create a graph database and container</span></span>
> * <span data-ttu-id="51ff3-111">Köşeleri ve kenarları .NET nesneleri seri hale</span><span class="sxs-lookup"><span data-stu-id="51ff3-111">Serialize vertices and edges to .NET objects</span></span>
> * <span data-ttu-id="51ff3-112">Köşeleri ve kenarları ekleme</span><span class="sxs-lookup"><span data-stu-id="51ff3-112">Add vertices and edges</span></span>
> * <span data-ttu-id="51ff3-113">Grafiğin Gremlin kullanarak sorgulama</span><span class="sxs-lookup"><span data-stu-id="51ff3-113">Query the graph using Gremlin</span></span>

## <a name="graphs-in-azure-cosmos-db"></a><span data-ttu-id="51ff3-114">Azure Cosmos DB grafiklerde</span><span class="sxs-lookup"><span data-stu-id="51ff3-114">Graphs in Azure Cosmos DB</span></span>
<span data-ttu-id="51ff3-115">Azure Cosmos DB oluşturmak, güncelleştirmek ve grafikler kullanarak sorgulamak için kullanabileceğiniz [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="51ff3-115">You can use Azure Cosmos DB to create, update, and query graphs using the [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) library.</span></span> <span data-ttu-id="51ff3-116">Microsoft.Azure.Graph kitaplığı tek genişletme yöntemi sağlar `CreateGremlinQuery<T>` üstünde `DocumentClient` Gremlin sorgularını yürütmek için sınıf.</span><span class="sxs-lookup"><span data-stu-id="51ff3-116">The Microsoft.Azure.Graph library provides a single extension method `CreateGremlinQuery<T>` on top of the `DocumentClient` class to execute Gremlin queries.</span></span>

<span data-ttu-id="51ff3-117">Gremlin destekleyen işlevsel bir programlama dili yazma işlemleri (DML) ve sorgu ve çapraz geçişi işlemleri ' dir.</span><span class="sxs-lookup"><span data-stu-id="51ff3-117">Gremlin is a functional programming language that supports write operations (DML) and query and traversal operations.</span></span> <span data-ttu-id="51ff3-118">Biz bu makalede, başlatılan Gremlin ile almak için birkaç örnek kapsar.</span><span class="sxs-lookup"><span data-stu-id="51ff3-118">We cover a few examples in this article to get your started with Gremlin.</span></span> <span data-ttu-id="51ff3-119">Bkz: [Gremlin sorguları](gremlin-support.md) ayrıntılı kılavuz Gremlin özelliklerinden Azure Cosmos DB içinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="51ff3-119">See [Gremlin queries](gremlin-support.md) for a detailed walkthrough of Gremlin capabilities available in Azure Cosmos DB.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="51ff3-120">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="51ff3-120">Prerequisites</span></span>
<span data-ttu-id="51ff3-121">Lütfen aşağıdakilere sahip olduğunuzdan emin olun:</span><span class="sxs-lookup"><span data-stu-id="51ff3-121">Please make sure you have the following:</span></span>

* <span data-ttu-id="51ff3-122">Etkin bir Azure hesabı.</span><span class="sxs-lookup"><span data-stu-id="51ff3-122">An active Azure account.</span></span> <span data-ttu-id="51ff3-123">Bir aboneliğiniz yoksa [ücretsiz bir hesap](https://azure.microsoft.com/free/) için kaydolabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51ff3-123">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="51ff3-124">Alternatif olarak bu öğretici için [Azure DocumentDB Öykünücüsü](local-emulator.md)’nü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51ff3-124">Alternatively, you can use the [Azure DocumentDB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="51ff3-125">[Visual Studio](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="51ff3-125">[Visual Studio](http://www.visualstudio.com/).</span></span>

## <a name="create-database-account"></a><span data-ttu-id="51ff3-126">Veritabanı hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="51ff3-126">Create database account</span></span>

<span data-ttu-id="51ff3-127">Azure portalında bir Azure Cosmos DB hesabı oluşturarak başlayalım.</span><span class="sxs-lookup"><span data-stu-id="51ff3-127">Let's start by creating an Azure Cosmos DB account in the Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="51ff3-128">Zaten Azure Cosmos DB hesabınız var mı?</span><span class="sxs-lookup"><span data-stu-id="51ff3-128">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="51ff3-129">Bu durumda, İleri için atlayabilirsiniz [, Visual Studio çözümü ayarlama](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="51ff3-129">If so, skip ahead to [Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="51ff3-130">Bir Azure DocumentDB hesabına sahip miydiniz?</span><span class="sxs-lookup"><span data-stu-id="51ff3-130">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="51ff3-131">Bu nedenle, hesabınızı şimdi bir Azure Cosmos DB hesabı ise ve size atlayabilirsiniz [, Visual Studio çözümü ayarlama](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="51ff3-131">If so, your account is now an Azure Cosmos DB account and you can skip ahead to [Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="51ff3-132">Azure Cosmos DB öykünücüsü kullanıyorsanız, lütfen bölümündeki adımları izleyin [Azure Cosmos DB öykünücüsü](local-emulator.md) öykünücü kurulması ve için İleri atlayabilirsiniz [, Visual Studio çözümünü kurmak](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="51ff3-132">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
> 

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <span data-ttu-id="51ff3-133"><a id="SetupVS"></a>Visual Studio çözümünüzü kurma</span><span class="sxs-lookup"><span data-stu-id="51ff3-133"><a id="SetupVS"></a>Set up your Visual Studio solution</span></span>
1. <span data-ttu-id="51ff3-134">Bilgisayarınızda **Visual Studio**'yu açın.</span><span class="sxs-lookup"><span data-stu-id="51ff3-134">Open **Visual Studio** on your computer.</span></span>
2. <span data-ttu-id="51ff3-135">**Dosya** menüsünde **Yeni**'yi seçin ve ardından **Proje**'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="51ff3-135">On the **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="51ff3-136">İçinde **yeni proje** iletişim kutusunda **şablonları** / **Visual C#** / **konsol uygulaması (.NET Framework)** , projenizi adlandırın ve ardından **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="51ff3-136">In the **New Project** dialog, select **Templates** / **Visual C#** / **Console App (.NET Framework)**, name your project, and then click **OK**.</span></span>
4. <span data-ttu-id="51ff3-137">**Çözüm Gezgini**'nde Visual Studio çözümünüzün altındaki yeni konsol uygulamanıza sağ tıklayın ve **NuGet Paketlerini Yönet...** öğesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="51ff3-137">In the **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
5. <span data-ttu-id="51ff3-138">İçinde **NuGet** sekmesini tıklatın, **Gözat**ve türü **Microsoft.Azure.Graphs** arama kutusu ve onay **yayın öncesi sürümlerdahil**.</span><span class="sxs-lookup"><span data-stu-id="51ff3-138">In the **NuGet** tab, click **Browse**, and type **Microsoft.Azure.Graphs** in the search box, and check the **Include prerelease versions**.</span></span>
6. <span data-ttu-id="51ff3-139">Sonuçları içinde bulma **Microsoft.Azure.Graphs** tıklatıp **yükleme**.</span><span class="sxs-lookup"><span data-stu-id="51ff3-139">Within the results, find **Microsoft.Azure.Graphs** and click **Install**.</span></span>
   
   <span data-ttu-id="51ff3-140">Çözümdeki değişiklikleri gözden geçirme hakkında iletiler alırsanız **Tamam**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="51ff3-140">If you get a message about reviewing changes to the solution, click **OK**.</span></span> <span data-ttu-id="51ff3-141">Lisans kabulü hakkında bir ileti alırsanız **Kabul ediyorum**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="51ff3-141">If you get a message about license acceptance, click **I accept**.</span></span>
   
    <span data-ttu-id="51ff3-142">`Microsoft.Azure.Graphs` Kitaplığı, bir tek genişletme yöntemi sağlar `CreateGremlinQuery<T>` Gremlin işlemleri yürütmek.</span><span class="sxs-lookup"><span data-stu-id="51ff3-142">The `Microsoft.Azure.Graphs` library provides a single extension method `CreateGremlinQuery<T>` for executing Gremlin operations.</span></span> <span data-ttu-id="51ff3-143">Gremlin destekleyen işlevsel bir programlama dili yazma işlemleri (DML) ve sorgu ve çapraz geçişi işlemleri ' dir.</span><span class="sxs-lookup"><span data-stu-id="51ff3-143">Gremlin is a functional programming language that supports write operations (DML) and query and traversal operations.</span></span> <span data-ttu-id="51ff3-144">Biz bu makalede, başlatılan Gremlin ile almak için birkaç örnek kapsar.</span><span class="sxs-lookup"><span data-stu-id="51ff3-144">We cover a few examples in this article to get your started with Gremlin.</span></span> <span data-ttu-id="51ff3-145">[Gremlin sorguları](gremlin-support.md) Azure Cosmos DB'de Gremlin özelliklerinin ayrıntılı bir kılavuz vardır.</span><span class="sxs-lookup"><span data-stu-id="51ff3-145">[Gremlin queries](gremlin-support.md) has a detailed walkthrough of Gremlin capabilities in Azure Cosmos DB.</span></span>

## <span data-ttu-id="51ff3-146"><a id="add-references"></a>Uygulamanızı bağlama</span><span class="sxs-lookup"><span data-stu-id="51ff3-146"><a id="add-references"></a>Connect your app</span></span>

<span data-ttu-id="51ff3-147">Bu iki sabitleri ekleyin ve *istemci* uygulamanızda değişken.</span><span class="sxs-lookup"><span data-stu-id="51ff3-147">Add these two constants and your *client* variable in your application.</span></span> 

```csharp
string endpoint = ConfigurationManager.AppSettings["Endpoint"]; 
string authKey = ConfigurationManager.AppSettings["AuthKey"]; 
``` 
<span data-ttu-id="51ff3-148">Head ardından, yeniden [Azure portal](https://portal.azure.com) uç noktasının URL'sini ve birincil anahtar alınamadı.</span><span class="sxs-lookup"><span data-stu-id="51ff3-148">Next, head back to the [Azure portal](https://portal.azure.com) to retrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="51ff3-149">Uç nokta URL’si ve birincil anahtar, uygulamanızın nereye bağlanacağını anlaması ve Azure Cosmos DB’nin uygulamanızın bağlantısına güvenmesi için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="51ff3-149">The endpoint URL and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span> 

<span data-ttu-id="51ff3-150">Azure portalında Azure Cosmos DB hesabınıza gidin, tıklatın **anahtarları**ve ardından **okuma-yazma anahtarları**.</span><span class="sxs-lookup"><span data-stu-id="51ff3-150">In the Azure portal, navigate to your Azure Cosmos DB account, click **Keys**, and then click **Read-write Keys**.</span></span> 

<span data-ttu-id="51ff3-151">URI Portal'dan kopyalayın ve üzerinden yapıştırın `Endpoint` yukarıdaki uç nokta özelliğinde.</span><span class="sxs-lookup"><span data-stu-id="51ff3-151">Copy the URI from the portal and paste it over `Endpoint` in the endpoint property above.</span></span> <span data-ttu-id="51ff3-152">Ardından portaldan birincil anahtarı kopyalayın ve yapıştırın `AuthKey` yukarıdaki özelliği.</span><span class="sxs-lookup"><span data-stu-id="51ff3-152">Then copy the PRIMARY KEY from the portal and paste it into the `AuthKey` property above.</span></span> 

<span data-ttu-id="51ff3-153">! [C# uygulaması oluşturmak için Öğreticisi tarafından kullanılan Azure portal ekran görüntüsü.</span><span class="sxs-lookup"><span data-stu-id="51ff3-153">![Screen shot of the Azure portal used by the tutorial to create a C# application.</span></span> <span data-ttu-id="51ff3-154">Bir Azure Cosmos DB hesap ANAHTARLAR düğmesi üzerinde Azure Cosmos DB Gezinti vurgulanmış ve anahtarlar dikey penceresinde URI ve birincil anahtar değerleri gösterir] [Anahtarları]</span><span class="sxs-lookup"><span data-stu-id="51ff3-154">Shows an Azure Cosmos DB account the KEYS button highlighted on the Azure Cosmos DB navigation , and the URI and PRIMARY KEY values highlighted on the Keys blade][keys]</span></span> 
 
## <span data-ttu-id="51ff3-155"><a id="instantiate"></a>DocumentClient örneği</span><span class="sxs-lookup"><span data-stu-id="51ff3-155"><a id="instantiate"></a>Instantiate the DocumentClient</span></span> 
<span data-ttu-id="51ff3-156">Ardından, yeni bir örneğini oluşturun **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="51ff3-156">Next, create a new instance of the **DocumentClient**.</span></span>  

```csharp 
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey); 
``` 

## <span data-ttu-id="51ff3-157"><a id="create-database"></a>Bir veritabanı oluşturun</span><span class="sxs-lookup"><span data-stu-id="51ff3-157"><a id="create-database"></a>Create a database</span></span> 

<span data-ttu-id="51ff3-158">Şimdi bir Azure Cosmos DB Oluştur [veritabanı](documentdb-resources.md#databases) kullanarak [Documentclient](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) yöntemi veya [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) yöntemi  **DocumentClient** sınıfıyla [DocumentDB .NET SDK'sı](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="51ff3-158">Now, create an Azure Cosmos DB [database](documentdb-resources.md#databases) by using the [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method or [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of the **DocumentClient** class from the [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span></span>  

```csharp 
Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" }); 
``` 
 
## <a name="create-a-graph"></a><span data-ttu-id="51ff3-159">Bir grafik oluşturma</span><span class="sxs-lookup"><span data-stu-id="51ff3-159">Create a graph</span></span> 

<span data-ttu-id="51ff3-160">Ardından, kullanarak kullanarak bir grafik kapsayıcı oluşturmak [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) yöntemi veya [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) yöntemi **DocumentClient** sınıfı.</span><span class="sxs-lookup"><span data-stu-id="51ff3-160">Next, create a graph container by using the using the [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method or [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="51ff3-161">Bir koleksiyon, grafik varlıkların bir kapsayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="51ff3-161">A collection is a container of graph entities.</span></span> 

```csharp 
DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync( 
    UriFactory.CreateDatabaseUri("graphdb"), 
    new DocumentCollection { Id = "graphcollz" }, 
    new RequestOptions { OfferThroughput = 1000 }); 
``` 

## <span data-ttu-id="51ff3-162"><a id="serializing"></a>Köşeleri ve kenarları .NET nesneleri seri hale</span><span class="sxs-lookup"><span data-stu-id="51ff3-162"><a id="serializing"></a>Serialize vertices and edges to .NET objects</span></span>
<span data-ttu-id="51ff3-163">Azure Cosmos DB kullanır [GraphSON kablo biçiminde](gremlin-support.md), köşe, kenarları ve özellikleri için JSON şeması tanımlar.</span><span class="sxs-lookup"><span data-stu-id="51ff3-163">Azure Cosmos DB uses the [GraphSON wire format](gremlin-support.md), which defines a JSON schema for vertices, edges, and properties.</span></span> <span data-ttu-id="51ff3-164">JSON.NET bağımlılık olarak Azure Cosmos DB .NET SDK'sı içerir ve bu bize seri/GraphSON biz kodda çalışabilirsiniz .NET nesneleri içine seri durumdan çıkarılacak sağlar.</span><span class="sxs-lookup"><span data-stu-id="51ff3-164">The Azure Cosmos DB .NET SDK includes JSON.NET as a dependency, and this allows us to serialize/deserialize GraphSON into .NET objects that we can work with in code.</span></span>

<span data-ttu-id="51ff3-165">Örnek olarak, basit bir sosyal ağ dört kişilerle şimdi çalışır.</span><span class="sxs-lookup"><span data-stu-id="51ff3-165">As an example, let's work with a simple social network with four people.</span></span> <span data-ttu-id="51ff3-166">Oluşturmak nasıl tümleştirildiği incelenmektedir `Person` köşeleri eklemek `Knows` arasındaki ilişkileri ardından sorgu ve ilişkileri "arkadaş arkadaş" bulmak için grafiği çapraz geçiş.</span><span class="sxs-lookup"><span data-stu-id="51ff3-166">We look at how to create `Person` vertices, add `Knows` relationships between them, then query and traverse the graph to find "friend of friend" relationships.</span></span> 

<span data-ttu-id="51ff3-167">`Microsoft.Azure.Graphs.Elements` Ad alanı sağlar `Vertex`, `Edge`, `Property` ve `VertexProperty` GraphSON yanıtlarını iyi tanımlanmış .NET nesnelerini seri durumdan çıkarmak için sınıflar.</span><span class="sxs-lookup"><span data-stu-id="51ff3-167">The `Microsoft.Azure.Graphs.Elements` namespace provides `Vertex`, `Edge`, `Property` and `VertexProperty` classes for deserializing GraphSON responses to well-defined .NET objects.</span></span>

## <a name="run-gremlin-using-creategremlinquery"></a><span data-ttu-id="51ff3-168">Gremlin CreateGremlinQuery kullanarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="51ff3-168">Run Gremlin using CreateGremlinQuery</span></span>
<span data-ttu-id="51ff3-169">SQL gibi gremlin okuma, yazma ve sorgu işlemleri destekler.</span><span class="sxs-lookup"><span data-stu-id="51ff3-169">Gremlin, like SQL, supports read, write, and query operations.</span></span> <span data-ttu-id="51ff3-170">Örneğin, aşağıdaki kod parçacığında köşeleri kenarları oluşturmak, kullanan bazı örnek sorgular gerçekleştirmek gösterilmektedir `CreateGremlinQuery<T>`ve zaman uyumsuz olarak kullanarak bu sonuçlarını yinelemek `ExecuteNextAsync` ve ' HasMoreResults.</span><span class="sxs-lookup"><span data-stu-id="51ff3-170">For example, the following snippet shows how to create vertices, edges, perform some sample queries using `CreateGremlinQuery<T>`, and asynchronously iterate through these results using `ExecuteNextAsync` and \`HasMoreResults.</span></span>

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

    // The CreateGremlinQuery method extensions allow you to execute Gremlin queries and iterate
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

## <a name="add-vertices-and-edges"></a><span data-ttu-id="51ff3-171">Köşeleri ve kenarları ekleme</span><span class="sxs-lookup"><span data-stu-id="51ff3-171">Add vertices and edges</span></span>

<span data-ttu-id="51ff3-172">Daha fazla ayrıntı önceki bölümde gösterilen Gremlin deyimlerini bakalım.</span><span class="sxs-lookup"><span data-stu-id="51ff3-172">Let's look at the Gremlin statements shown in the preceding section more detail.</span></span> <span data-ttu-id="51ff3-173">İlk biz Gremlin'ın kullanarak bazı köşeleri `addV` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="51ff3-173">First we some vertices using Gremlin's `addV` method.</span></span> <span data-ttu-id="51ff3-174">Örneğin, aşağıdaki kod parçacığını ad, Soyadı ve yaş özellikleriyle "Kişi" türündeki "Thomas Andersen" köşe oluşturur.</span><span class="sxs-lookup"><span data-stu-id="51ff3-174">For example, the following snippet creates a "Thomas Andersen" vertex of type "Person", with properties for first name, last name, and age.</span></span>

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

<span data-ttu-id="51ff3-175">Biz Gremlin'ın kullanarak bu köşeleri arasında bazı kenarları oluşturup `addE` yöntemi.</span><span class="sxs-lookup"><span data-stu-id="51ff3-175">Then we create some edges between these vertices using Gremlin's `addE` method.</span></span> 

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

<span data-ttu-id="51ff3-176">Biz kullanarak var olan bir köşe güncelleştirebilirsiniz `properties` Gremlin içinde adım.</span><span class="sxs-lookup"><span data-stu-id="51ff3-176">We can update an existing vertex by using `properties` step in Gremlin.</span></span> <span data-ttu-id="51ff3-177">Biz aracılığıyla sorguyu yürütmek için çağrı atla `HasMoreResults` ve `ExecuteNextAsync` örnekler geri kalanı için.</span><span class="sxs-lookup"><span data-stu-id="51ff3-177">We skip the call to execute the query via `HasMoreResults` and `ExecuteNextAsync` for the rest of the examples.</span></span>

```cs
// Update a vertex
client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.V('thomas').property('age', 45)");
```

<span data-ttu-id="51ff3-178">Kenarları ve Gremlin'ın kullanarak köşeleri düşürebilir `drop` adım.</span><span class="sxs-lookup"><span data-stu-id="51ff3-178">You can drop edges and vertices using Gremlin's `drop` step.</span></span> <span data-ttu-id="51ff3-179">Bir köşe kenar silip gösteren bir parçacığı aşağıda verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="51ff3-179">Here's a snippet that shows how to delete a vertex and an edge.</span></span> <span data-ttu-id="51ff3-180">Bir köşe bırakarak ilişkili kenarlarının art arda delete gerçekleştirmediğini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="51ff3-180">Note that dropping a vertex performs a cascading delete of the associated edges.</span></span>

```cs
// Drop an edge
client.CreateGremlinQuery(graphCollection, "g.E('thomasKnowsRobin').drop()");

// Drop a vertex
client.CreateGremlinQuery(graphCollection, "g.V('robin').drop()");
```

## <a name="query-the-graph"></a><span data-ttu-id="51ff3-181">Sorgu grafiği</span><span class="sxs-lookup"><span data-stu-id="51ff3-181">Query the graph</span></span>

<span data-ttu-id="51ff3-182">Sorgular ve ayrıca Gremlin kullanarak çapraz geçişlerine gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51ff3-182">You can perform queries and traversals also using Gremlin.</span></span> <span data-ttu-id="51ff3-183">Örneğin, aşağıdaki kod parçacığında grafiği tepe sayısı gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="51ff3-183">For example, the following snippet shows how to count the number of vertices in the graph:</span></span>

```cs
// Run a query to count vertices
IDocumentQuery<int> countQuery = client.CreateGremlinQuery<int>(graphCollection, "g.V().count()");
```
<span data-ttu-id="51ff3-184">Gremlin'ın kullanarak filtreler gerçekleştirebilirsiniz `has` ve `hasLabel` adımları ve bunları birleştirmek kullanarak `and`, `or`, ve `not` daha karmaşık filtreler oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="51ff3-184">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` to build more complex filters:</span></span>

```cs
// Run a query with filter
IDocumentQuery<Vertex> personsByAge = client.CreateGremlinQuery<Vertex>(
  graphCollection, 
  "g.V().hasLabel('person').has('age', gt(40))");
```

<span data-ttu-id="51ff3-185">Belirli özellikleri kullanarak sorgu sonuçlarındaki proje `values` . adım:</span><span class="sxs-lookup"><span data-stu-id="51ff3-185">You can project certain properties in the query results using the `values` step:</span></span>

```cs
// Run a query with projection
IDocumentQuery<string> firstNames = client.CreateGremlinQuery<string>(
  graphCollection, 
  $"g.V().hasLabel('person').values('firstName')");
```

<span data-ttu-id="51ff3-186">Şu ana kadar yalnızca tüm veritabanındaki iş sorgu işleçleri gördük.</span><span class="sxs-lookup"><span data-stu-id="51ff3-186">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="51ff3-187">İlgili kenarları ve köşeleri gitmek gerektiğinde grafikleri hızlı ve verimli çapraz geçiş işlemleri için.</span><span class="sxs-lookup"><span data-stu-id="51ff3-187">Graphs are fast and efficient for traversal operations when you need to navigate to related edges and vertices.</span></span> <span data-ttu-id="51ff3-188">Şimdi tüm arkadaşların Thomas bulun.</span><span class="sxs-lookup"><span data-stu-id="51ff3-188">Let's find all friends of Thomas.</span></span> <span data-ttu-id="51ff3-189">Biz Gremlin'ın kullanarak bunu `outE` tüm bulmak için adım Thomas silip Gremlin'ın kullanarak bu kenarlarından içinde-köşeleri için çapraz geçiş yapan dışarı kenarları `inV` . adım:</span><span class="sxs-lookup"><span data-stu-id="51ff3-189">We do this by using Gremlin's `outE` step to find all the out-edges from Thomas, then traversing to the in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
// Run a traversal (find friends of Thomas)
IDocumentQuery<Vertex> friendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person')");
```

<span data-ttu-id="51ff3-190">Tüm Thomas' "arkadaş arkadaş", çağırarak bulmak için iki atlama sonraki sorgu gerçekleştirir `outE` ve `inV` iki kez.</span><span class="sxs-lookup"><span data-stu-id="51ff3-190">The next query performs two hops to find all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
// Run a traversal (find friends of friends of Thomas)
IDocumentQuery<Vertex> friendsOfFriendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')");
```

<span data-ttu-id="51ff3-191">Daha karmaşık sorgular derlemek ve döngü kullanarak gerçekleştirmeden, filtre ifadeleri karıştırma dahil olmak üzere Gremlin kullanan güçlü grafik geçişi mantığı uygulamanıza `loop` adım ve uygulama koşullu Gezinti kullanarak `choose` adım.</span><span class="sxs-lookup"><span data-stu-id="51ff3-191">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using the `loop` step, and implementing conditional navigation using the `choose` step.</span></span> <span data-ttu-id="51ff3-192">İle yapabilecekleriniz hakkında daha fazla bilgi [Gremlin Destek](gremlin-support.md)!</span><span class="sxs-lookup"><span data-stu-id="51ff3-192">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

<span data-ttu-id="51ff3-193">İşte bu kadar bu Azure Cosmos DB öğretici tamamlandı!</span><span class="sxs-lookup"><span data-stu-id="51ff3-193">That's it, this Azure Cosmos DB tutorial is complete!</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="51ff3-194">Kaynakları temizleme</span><span class="sxs-lookup"><span data-stu-id="51ff3-194">Clean up resources</span></span>

<span data-ttu-id="51ff3-195">Bu uygulamayı kullanmaya devam etmeyecekseniz aşağıdaki adımları kullanarak Azure portalında bu öğretici tarafından oluşturulan tüm kaynakları silin:</span><span class="sxs-lookup"><span data-stu-id="51ff3-195">If you're not going to continue to use this app, use the following steps to delete all resources created by this tutorial in the Azure portal.</span></span>  

1. <span data-ttu-id="51ff3-196">Azure portalında sol taraftaki menüden, **Kaynak grupları**'na ve ardından oluşturduğunuz kaynağın adına tıklayın.</span><span class="sxs-lookup"><span data-stu-id="51ff3-196">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="51ff3-197">Kaynak grubu sayfanızda, **Sil**'e tıklayın, metin kutusuna silinecek kaynağın adını yazın ve ardından **Sil**'e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="51ff3-197">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="51ff3-198">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="51ff3-198">Next Steps</span></span>

<span data-ttu-id="51ff3-199">Bu öğreticide, aşağıdakileri yaptığınızdan:</span><span class="sxs-lookup"><span data-stu-id="51ff3-199">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="51ff3-200">Bir Azure Cosmos DB hesabı oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="51ff3-200">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="51ff3-201">Bir grafik veritabanı ve kapsayıcı oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="51ff3-201">Created a graph database and container</span></span>
> * <span data-ttu-id="51ff3-202">Serileştirilmiş köşeleri ve kenarları .NET nesneleri</span><span class="sxs-lookup"><span data-stu-id="51ff3-202">Serialized vertices and edges to .NET objects</span></span>
> * <span data-ttu-id="51ff3-203">Eklenen köşeleri ve kenarları</span><span class="sxs-lookup"><span data-stu-id="51ff3-203">Added vertices and edges</span></span>
> * <span data-ttu-id="51ff3-204">Sorgulanan Gremlin kullanarak grafiği</span><span class="sxs-lookup"><span data-stu-id="51ff3-204">Queried the graph using Gremlin</span></span>

<span data-ttu-id="51ff3-205">Artık daha karmaşık sorgular oluşturabilir ve Gremlin kullanarak güçlü grafik geçişi mantığını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51ff3-205">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="51ff3-206">Gremlin kullanarak sorgulama</span><span class="sxs-lookup"><span data-stu-id="51ff3-206">Query using Gremlin</span></span>](tutorial-query-graph.md)
