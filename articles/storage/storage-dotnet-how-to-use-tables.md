---
title: ".NET kullanarak Azure Tablo Depolama’yı kullanmaya başlama | Microsoft Belgeleri"
description: "Bir NoSQL veri deposu olan Azure Table Storage kullanarak bulutta yapılandırılmış veri depolayın."
services: storage
documentationcenter: .net
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: fe46d883-7bed-49dd-980e-5c71df36adb3
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 04/10/2017
ms.author: marsma
ms.openlocfilehash: 16a9dad1b01fdbef5ec8949bf9ff25497f33d994
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-azure-table-storage-using-net"></a><span data-ttu-id="7087e-103">.NET kullanarak Azure Table Storage’ı kullanmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="7087e-103">Get started with Azure Table storage using .NET</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

<span data-ttu-id="7087e-104">Azure Tablo Depolama, yapılandırılmış NoSQL verilerini bulutta depolayan ve şemasız bir tasarım ile anahtar/öznitelik deposu sağlayan bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="7087e-104">Azure Table storage is a service that stores structured NoSQL data in the cloud, providing a key/attribute store with a schemaless design.</span></span> <span data-ttu-id="7087e-105">Table Storage şemasız olduğu için uygulamanızın ihtiyaçları geliştikçe verilerinizi kolayca uyarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7087e-105">Because Table storage is schemaless, it's easy to adapt your data as the needs of your application evolve.</span></span> <span data-ttu-id="7087e-106">Tablo Depolama verilerine erişim, çoğu uygulama türü için hızlı ve ekonomik olmanın yanı sıra benzer veri hacimleri için geleneksel SQL’e kıyasla genellikle daha düşük maliyetlidir.</span><span class="sxs-lookup"><span data-stu-id="7087e-106">Access to Table storage data is fast and cost-effective for many types of applications, and is typically lower in cost than traditional SQL for similar volumes of data.</span></span>

<span data-ttu-id="7087e-107">Web uygulamaları için kullanıcı verileri, adres defterleri, cihaz bilgileri veya hizmetiniz için gerekli olan tüm diğer meta veri türleri gibi esnek veri kümelerini Tablo Depolama ile depolayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7087e-107">You can use Table storage to store flexible datasets like user data for web applications, address books, device information, or other types of metadata your service requires.</span></span> <span data-ttu-id="7087e-108">Bir tabloda istediğiniz kadar varlık depolayabilirsiniz ve bir depolama hesabı kapasite limitini dolduracak kadar tablo içerebilir.</span><span class="sxs-lookup"><span data-stu-id="7087e-108">You can store any number of entities in a table, and a storage account may contain any number of tables, up to the capacity limit of the storage account.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="7087e-109">Bu öğretici hakkında</span><span class="sxs-lookup"><span data-stu-id="7087e-109">About this tutorial</span></span>
<span data-ttu-id="7087e-110">Bu öğreticide, sık kullanılan bazı Azure Tablo Depolama senaryolarında [.NET için Azure Depolama İstemci Kitaplığı](https://www.nuget.org/packages/WindowsAzure.Storage/)’nın nasıl kullanılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="7087e-110">This tutorial shows you how to use the [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) in some common Azure Table storage scenarios.</span></span> <span data-ttu-id="7087e-111">Bu senaryolar, tablo oluşturup silme ve tablo verileri ekleme, güncelleştirme, silme ve sorgulama işlemleri için C# örnekleri kullanılarak sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7087e-111">These scenarios are presented using C# examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7087e-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7087e-112">Prerequisites</span></span>

<span data-ttu-id="7087e-113">Bu öğreticiyi başarıyla tamamlamak için aşağıdakiler gerekir:</span><span class="sxs-lookup"><span data-stu-id="7087e-113">You need the following to complete this tutorial successfully:</span></span>

* [<span data-ttu-id="7087e-114">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7087e-114">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="7087e-115">.NET için Azure Depolama İstemcisi</span><span class="sxs-lookup"><span data-stu-id="7087e-115">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="7087e-116">.NET için Azure Yapılandırma Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="7087e-116">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [<span data-ttu-id="7087e-117">Azure depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="7087e-117">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="7087e-118">Daha fazla örnek</span><span class="sxs-lookup"><span data-stu-id="7087e-118">More samples</span></span>
<span data-ttu-id="7087e-119">Tablo depolama kullanan diğer örnekler için [.NET’te Azure Table Storage Kullanmaya Başlama](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="7087e-119">For additional examples using Table storage, see [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/).</span></span> <span data-ttu-id="7087e-120">Örnek uygulamayı indirip çalıştırabilir veya GitHub’daki örneğe göz atabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7087e-120">You can download the sample application and run it, or browse the code on GitHub.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="7087e-121">Using yönergeleri ekleme</span><span class="sxs-lookup"><span data-stu-id="7087e-121">Add using directives</span></span>
<span data-ttu-id="7087e-122">Aşağıdaki **using** yönergelerini `Program.cs` dosyasının üst tarafına ekleyin:</span><span class="sxs-lookup"><span data-stu-id="7087e-122">Add the following **using** directives to the top of the `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Table; // Namespace for Table storage types
```

### <a name="parse-the-connection-string"></a><span data-ttu-id="7087e-123">Bağlantı dizesini ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="7087e-123">Parse the connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-the-table-service-client"></a><span data-ttu-id="7087e-124">Tablo hizmeti istemcisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="7087e-124">Create the Table service client</span></span>
<span data-ttu-id="7087e-125">[CloudTableClient][dotnet_CloudTableClient] sınıfı, Tablo Depolamada depolanan tabloları ve varlıkları almanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="7087e-125">The [CloudTableClient][dotnet_CloudTableClient] class enables you to retrieve tables and entities stored in Table storage.</span></span> <span data-ttu-id="7087e-126">Tablo hizmeti istemcisini oluşturma yöntemlerinden biri aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="7087e-126">Here's one way to create the Table service client:</span></span>

```csharp
// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```

<span data-ttu-id="7087e-127">Artık Table Storage’dan veri okuyan ve bu depolamaya veri yazan kodu yazmaya hazırsınız.</span><span class="sxs-lookup"><span data-stu-id="7087e-127">Now you are ready to write code that reads data from and writes data to Table storage.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="7087e-128">Bir tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="7087e-128">Create a table</span></span>
<span data-ttu-id="7087e-129">Bu örnek, zaten yoksa, nasıl bir tablo oluşturulacağını gösterir:</span><span class="sxs-lookup"><span data-stu-id="7087e-129">This example shows how to create a table if it does not already exist:</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Retrieve a reference to the table.
CloudTable table = tableClient.GetTableReference("people");

// Create the table if it doesn't exist.
table.CreateIfNotExists();
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="7087e-130">Tabloya bir varlık ekleme</span><span class="sxs-lookup"><span data-stu-id="7087e-130">Add an entity to a table</span></span>
<span data-ttu-id="7087e-131">Varlıklar, [TableEntity][dotnet_TableEntity]’den oluşturulan özel bir sınıf kullanarak C# nesneleriyle eşlenir.</span><span class="sxs-lookup"><span data-stu-id="7087e-131">Entities map to C# objects by using a custom class derived from [TableEntity][dotnet_TableEntity].</span></span> <span data-ttu-id="7087e-132">Tabloya bir varlık eklemek için varlığınızın özelliklerini tanımlayan bir sınıf oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7087e-132">To add an entity to a table, create a class that defines the properties of your entity.</span></span> <span data-ttu-id="7087e-133">Aşağıdaki kod, sıra anahtarı olarak müşterinin adını, bölüm anahtarı olarak soyadını kullanan bir varlık sınıfı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="7087e-133">The following code defines an entity class that uses the customer's first name as the row key and last name as the partition key.</span></span> <span data-ttu-id="7087e-134">Birlikte, bir varlığın bölüm ve sıra anahtarı varlığı tabloda benzersiz şekilde tanımlar.</span><span class="sxs-lookup"><span data-stu-id="7087e-134">Together, an entity's partition and row key uniquely identify it in the table.</span></span> <span data-ttu-id="7087e-135">Aynı bölüm anahtarına sahip varlıklar farklı bölüm anahtarlı varlıklara göre daha hızlı sorgulanabilir ancak farklı bölüm anahtarlarının kullanılması paralel işlemler için daha büyük ölçeklendirme sağlar.</span><span class="sxs-lookup"><span data-stu-id="7087e-135">Entities with the same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="7087e-136">Tablolarda depolanacak varlıklar, [TableEntity][dotnet_TableEntity] sınıfından türetilen türler gibi desteklenen bir türde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7087e-136">Entities to be stored in tables must be of a supported type, for example derived from the [TableEntity][dotnet_TableEntity] class.</span></span> <span data-ttu-id="7087e-137">Bir tabloda depolamak istediğiniz varlık özellikleri, türün genel özellikleri olmalı ve değerleri hem almayı hem de ayarlamayı desteklemelidir.</span><span class="sxs-lookup"><span data-stu-id="7087e-137">Entity properties you'd like to store in a table must be public properties of the type, and support both getting and setting of values.</span></span> <span data-ttu-id="7087e-138">Bununla birlikte varlık türü parametresiz bir oluşturucu *olmalıdır*.</span><span class="sxs-lookup"><span data-stu-id="7087e-138">Also, your entity type *must* expose a parameter-less constructor.</span></span>

```csharp
public class CustomerEntity : TableEntity
{
    public CustomerEntity(string lastName, string firstName)
    {
        this.PartitionKey = lastName;
        this.RowKey = firstName;
    }

    public CustomerEntity() { }

    public string Email { get; set; }

    public string PhoneNumber { get; set; }
}
```

<span data-ttu-id="7087e-139">Varlıklarla ilgili tablo işlemleri daha önce “Tablo oluşturma” bölümünde oluşturduğunuz [CloudTable][dotnet_CloudTable] nesnesi ile gerçekleştirilecektir.</span><span class="sxs-lookup"><span data-stu-id="7087e-139">Table operations that involve entities are performed via the [CloudTable][dotnet_CloudTable] object that you created earlier in the "Create a table" section.</span></span> <span data-ttu-id="7087e-140">Gerçekleştirilecek işlem [TableOperation][dotnet_TableOperation] nesnesi ile belirtilir.</span><span class="sxs-lookup"><span data-stu-id="7087e-140">The operation to be performed is represented by a [TableOperation][dotnet_TableOperation] object.</span></span> <span data-ttu-id="7087e-141">Aşağıdaki kod örneği [CloudTable][dotnet_CloudTable] nesnesi ve ardından **CustomerEntity** nesnesinin oluşturulmasını gösterir.</span><span class="sxs-lookup"><span data-stu-id="7087e-141">The following code example shows the creation of the [CloudTable][dotnet_CloudTable] object and then a **CustomerEntity** object.</span></span> <span data-ttu-id="7087e-142">İşlemi hazırlamak için, müşteri varlığını tabloya yerleştirmek üzere bir [TableOperation][dotnet_TableOperation] nesnesi oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="7087e-142">To prepare the operation, a [TableOperation][dotnet_TableOperation] object is created to insert the customer entity into the table.</span></span> <span data-ttu-id="7087e-143">Son olarak işlem [CloudTable][dotnet_CloudTable].[Execute][dotnet_CloudTable_Execute] çağrılarak çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="7087e-143">Finally, the operation is executed by calling [CloudTable][dotnet_CloudTable].[Execute][dotnet_CloudTable_Execute].</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create the TableOperation object that inserts the customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute the insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="7087e-144">Toplu işlem varlık yerleştirme</span><span class="sxs-lookup"><span data-stu-id="7087e-144">Insert a batch of entities</span></span>
<span data-ttu-id="7087e-145">Bir tabloya tek bir yazma işlemiyle çok sayıda varlık yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7087e-145">You can insert a batch of entities into a table in one write operation.</span></span> <span data-ttu-id="7087e-146">Toplu işlemler ile ilgili diğer notlar:</span><span class="sxs-lookup"><span data-stu-id="7087e-146">Some other notes on batch operations:</span></span>

* <span data-ttu-id="7087e-147">Aynı tek toplu işlemde güncelleştirme, silme ve yerleştirme yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7087e-147">You can perform updates, deletes, and inserts in the same single batch operation.</span></span>
* <span data-ttu-id="7087e-148">Tek bir toplu işlem en fazla 100 varlık içerebilir.</span><span class="sxs-lookup"><span data-stu-id="7087e-148">A single batch operation can include up to 100 entities.</span></span>
* <span data-ttu-id="7087e-149">Tek bir toplu işlemdeki tüm varlıkların bölüm anahtarları aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7087e-149">All entities in a single batch operation must have the same partition key.</span></span>
* <span data-ttu-id="7087e-150">Toplu işlem olarak sorgu gerçekleştirmek mümkün olsa da, toplu işlemdeki tek işlem olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7087e-150">While it is possible to perform a query as a batch operation, it must be the only operation in the batch.</span></span>

<span data-ttu-id="7087e-151">Aşağıdaki kod örneği iki varlık nesnesi oluşturur ve [Insert][dotnet_TableBatchOperation_Insert] yöntemi kullanarak her birini [TableBatchOperation][dotnet_TableBatchOperation]’a ekler.</span><span class="sxs-lookup"><span data-stu-id="7087e-151">The following code example creates two entity objects and adds each to [TableBatchOperation][dotnet_TableBatchOperation] by using the [Insert][dotnet_TableBatchOperation_Insert] method.</span></span> <span data-ttu-id="7087e-152">Ardından, işlemi yürütmek için [CloudTable][dotnet_CloudTable].[Execute][dotnet_CloudTable_ExecuteBatch] çağrılır.</span><span class="sxs-lookup"><span data-stu-id="7087e-152">Then, [CloudTable][dotnet_CloudTable].[ExecuteBatch][dotnet_CloudTable_ExecuteBatch] is called to execute the operation.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create the batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it to the table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it to the table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities to the batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute the batch operation.
table.ExecuteBatch(batchOperation);
```

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="7087e-153">Tüm varlıkları bir bölüme alma</span><span class="sxs-lookup"><span data-stu-id="7087e-153">Retrieve all entities in a partition</span></span>
<span data-ttu-id="7087e-154">Bir bölümdeki tüm varlıklar için bir tabloyu sorgulamak üzere bir [TableQuery][dotnet_TableQuery] nesnesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="7087e-154">To query a table for all entities in a partition, use a [TableQuery][dotnet_TableQuery] object.</span></span> <span data-ttu-id="7087e-155">Aşağıdaki kod örneği, ‘Smith’in bölüm anahtarı olduğu varlıklar için bir filtre belirtir.</span><span class="sxs-lookup"><span data-stu-id="7087e-155">The following code example specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="7087e-156">Bu örnek sorgu sonuçlarındaki her varlığın alanlarını konsola yazdırır.</span><span class="sxs-lookup"><span data-stu-id="7087e-156">This example prints the fields of each entity in the query results to the console.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Construct the query operation for all customer entities where PartitionKey="Smith".
TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

// Print the fields for each customer.
foreach (CustomerEntity entity in table.ExecuteQuery(query))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="7087e-157">Bir bölüme bir grup varlık alma</span><span class="sxs-lookup"><span data-stu-id="7087e-157">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="7087e-158">Bir bölümdeki tüm varlıkları sorgulamak istemiyorsanız bölüm anahtarı filtresi ile bir satır anahtarı filtresini birleştirerek bir aralık belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7087e-158">If you don't want to query all entities in a partition, you can specify a range by combining the partition key filter with a row key filter.</span></span> <span data-ttu-id="7087e-159">Aşağıdaki kod örneği, 'Smith' bölümünde, satır anahtarı (ad) alfabede 'E' harfinden önce gelen bir harfle başlayan tüm varlıkları almak için iki filtre kullanır, ardından sorgu sonuçlarını yazdırır.</span><span class="sxs-lookup"><span data-stu-id="7087e-159">The following code example uses two filters to get all entities in partition 'Smith' where the row key (first name) starts with a letter before 'E' in the alphabet, then prints the query results.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create the table query.
TableQuery<CustomerEntity> rangeQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.CombineFilters(
        TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"),
        TableOperators.And,
        TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.LessThan, "E")));

// Loop through the results, displaying information about the entity.
foreach (CustomerEntity entity in table.ExecuteQuery(rangeQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="7087e-160">Tek bir varlık alma</span><span class="sxs-lookup"><span data-stu-id="7087e-160">Retrieve a single entity</span></span>
<span data-ttu-id="7087e-161">Tek, belirli bir varlığı almak üzere bir sorgu yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7087e-161">You can write a query to retrieve a single, specific entity.</span></span> <span data-ttu-id="7087e-162">Aşağıdaki kod 'Ben Smith' müşterisini belirlemek üzere [TableOperation][dotnet_TableOperation] kullanır.</span><span class="sxs-lookup"><span data-stu-id="7087e-162">The following code uses [TableOperation][dotnet_TableOperation] to specify the customer 'Ben Smith'.</span></span> <span data-ttu-id="7087e-163">Bu yöntem bir koleksiyon yerine yalnızca bir varlık döndürür ve [TableResult][dotnet_TableResult].[Result][dotnet_TableResult_Result]’ta dönen değer **CustomerEntity** nesnesidir.</span><span class="sxs-lookup"><span data-stu-id="7087e-163">This method returns just one entity rather than a collection, and the returned value in [TableResult][dotnet_TableResult].[Result][dotnet_TableResult_Result] is a **CustomerEntity** object.</span></span> <span data-ttu-id="7087e-164">Bir sorguda hem bölüm hem de satır anahtarını belirtmek Tablo hizmetinden tek bir varlık almanın en hızlı yoludur.</span><span class="sxs-lookup"><span data-stu-id="7087e-164">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the Table service.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Print the phone number of the result.
if (retrievedResult.Result != null)
{
    Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
}
else
{
    Console.WriteLine("The phone number could not be retrieved.");
}
```

## <a name="replace-an-entity"></a><span data-ttu-id="7087e-165">Bir varlığı değiştirme</span><span class="sxs-lookup"><span data-stu-id="7087e-165">Replace an entity</span></span>
<span data-ttu-id="7087e-166">Bir varlığı güncelleştirmek için Tablo hizmetinden alın, varlık nesnesini değiştirin ve değişiklikleri Tablo hizmetine geri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="7087e-166">To update an entity, retrieve it from the Table service, modify the entity object, and then save the changes back to the Table service.</span></span> <span data-ttu-id="7087e-167">Aşağıdaki kod mevcut bir müşterinin telefon numarasını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="7087e-167">The following code changes an existing customer's phone number.</span></span> <span data-ttu-id="7087e-168">[Insert][dotnet_TableOperation_Insert] yöntemini çağırmak yerine bu kod [Replace][dotnet_TableOperation_Replace] kullanır.</span><span class="sxs-lookup"><span data-stu-id="7087e-168">Instead of calling [Insert][dotnet_TableOperation_Insert], this code uses [Replace][dotnet_TableOperation_Replace].</span></span> <span data-ttu-id="7087e-169">[Replace][dotnet_TableOperation_Replace], sunucu üzerindeki varlık alındığından beri değiştirilmemişse varlığın sunucu üzerinde tamamen değiştirilmesini sağlar, aksi takdirde işlem başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="7087e-169">[Replace][dotnet_TableOperation_Replace] causes the entity to be fully replaced on the server, unless the entity on the server has changed since it was retrieved, in which case the operation will fail.</span></span> <span data-ttu-id="7087e-170">Bu işlem, uygulamanızın başka bir bileşeninin alım ve güncelleştirme arasında gerçekleştirilen bir değişikliğin yanlışlıkla üzerine yazılmasını engellemek üzere başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="7087e-170">This failure is to prevent your application from inadvertently overwriting a change made between the retrieval and update by another component of your application.</span></span> <span data-ttu-id="7087e-171">Bu başarısız işlem, varlığın yeniden alınması, (hala geçerli ise) değişikliklerin yapılması ve yeni bir [Replace][dotnet_TableOperation_Replace] işleminin gerçekleştirilmesiyle uygun şekilde ele alınır.</span><span class="sxs-lookup"><span data-stu-id="7087e-171">The proper handling of this failure is to retrieve the entity again, make your changes (if still valid), and then perform another [Replace][dotnet_TableOperation_Replace] operation.</span></span> <span data-ttu-id="7087e-172">Sonraki bölüm bu davranışı nasıl geçersiz kılacağınızı gösterecektir.</span><span class="sxs-lookup"><span data-stu-id="7087e-172">The next section will show you how to override this behavior.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign the result to a CustomerEntity object.
CustomerEntity updateEntity = (CustomerEntity)retrievedResult.Result;

if (updateEntity != null)
{
    // Change the phone number.
    updateEntity.PhoneNumber = "425-555-0105";

    // Create the Replace TableOperation.
    TableOperation updateOperation = TableOperation.Replace(updateEntity);

    // Execute the operation.
    table.Execute(updateOperation);

    Console.WriteLine("Entity updated.");
}
else
{
    Console.WriteLine("Entity could not be retrieved.");
}
```

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="7087e-173">Bir varlığı yerleştirme veya değiştirme</span><span class="sxs-lookup"><span data-stu-id="7087e-173">Insert-or-replace an entity</span></span>
<span data-ttu-id="7087e-174">Varlık sunucudan alındığından beri değiştirilmişse, [Replace][dotnet_TableOperation_Replace] işlemleri başarısız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7087e-174">[Replace][dotnet_TableOperation_Replace] operations will fail if the entity has been changed since it was retrieved from the server.</span></span> <span data-ttu-id="7087e-175">Dahası, [Replace][dotnet_TableOperation_Replace] işleminin başarılı olması için ilk olarak varlığın sunucudan alınması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7087e-175">Furthermore, you must retrieve the entity from the server first in order for the [Replace][dotnet_TableOperation_Replace] operation to be successful.</span></span> <span data-ttu-id="7087e-176">Buna karşın bazı durumlarda varlığın sunucuda olup olmadığını ve içinde saklı geçerli değerlerin ilgisiz olup olmadığını bilemeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7087e-176">Sometimes, however, you don't know if the entity exists on the server and the current values stored in it are irrelevant.</span></span> <span data-ttu-id="7087e-177">Güncelleştirmeniz tümünün üzerine yazmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7087e-177">Your update should overwrite them all.</span></span> <span data-ttu-id="7087e-178">Bunu gerçekleştirmek için [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] işlemi kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7087e-178">To accomplish this, you would use an [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation.</span></span> <span data-ttu-id="7087e-179">Bu işlem, varlık mevcut değilse varlığı yerleştirir, eğer varlık mevcutsa yapılan son güncelleştirmeden bağımsız olarak değiştirir.</span><span class="sxs-lookup"><span data-stu-id="7087e-179">This operation inserts the entity if it doesn't exist, or replaces it if it does, regardless of when the last update was made.</span></span>

<span data-ttu-id="7087e-180">Aşağıdaki kod örneğinde, 'Fred Jones' için bir müşteri varlığı oluşturulup 'people' tablosuna eklenir.</span><span class="sxs-lookup"><span data-stu-id="7087e-180">In the following code example, a customer entity for 'Fred Jones' is created and inserted into the 'people' table.</span></span> <span data-ttu-id="7087e-181">Ardından, [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] işlemi ile varlık aynı bölüm anahtarı (Jones) ve satır anahtarı (Fred) ile sunucuya kaydedilir, ancak bu kez PhoneNumber özelliği için farklı bir değer kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7087e-181">Next, we use the [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation to save an entity with the same partition key (Jones) and row key (Fred) to the server, this time with a different value for the PhoneNumber property.</span></span> <span data-ttu-id="7087e-182">[InsertOrReplace][dotnet_TableOperation_InsertOrReplace] özelliğini kullandığımız için tüm özellik değerleri değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="7087e-182">Because we use [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], all of its property values are replaced.</span></span> <span data-ttu-id="7087e-183">Ancak, bir 'Fred Jones' varlığı tabloda mevcut olmasaydı, eklenecekti.</span><span class="sxs-lookup"><span data-stu-id="7087e-183">However, if a 'Fred Jones' entity hadn't already existed in the table, it would have been inserted.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable object that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a customer entity.
CustomerEntity customer3 = new CustomerEntity("Jones", "Fred");
customer3.Email = "Fred@contoso.com";
customer3.PhoneNumber = "425-555-0106";

// Create the TableOperation object that inserts the customer entity.
TableOperation insertOperation = TableOperation.Insert(customer3);

// Execute the operation.
table.Execute(insertOperation);

// Create another customer entity with the same partition key and row key.
// We've already created a 'Fred Jones' entity and saved it to the
// 'people' table, but here we're specifying a different value for the
// PhoneNumber property.
CustomerEntity customer4 = new CustomerEntity("Jones", "Fred");
customer4.Email = "Fred@contoso.com";
customer4.PhoneNumber = "425-555-0107";

// Create the InsertOrReplace TableOperation.
TableOperation insertOrReplaceOperation = TableOperation.InsertOrReplace(customer4);

// Execute the operation. Because a 'Fred Jones' entity already exists in the
// 'people' table, its property values will be overwritten by those in this
// CustomerEntity. If 'Fred Jones' didn't already exist, the entity would be
// added to the table.
table.Execute(insertOrReplaceOperation);
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="7087e-184">Giriş özellikleri alt kümesi sorgulama</span><span class="sxs-lookup"><span data-stu-id="7087e-184">Query a subset of entity properties</span></span>
<span data-ttu-id="7087e-185">Bir tablo sorgusu, varlığın tüm özellikleri yerine bir varlıktaki birkaç özelliği alabilir.</span><span class="sxs-lookup"><span data-stu-id="7087e-185">A table query can retrieve just a few properties from an entity instead of all the entity properties.</span></span> <span data-ttu-id="7087e-186">Projeksiyon olarak adlandırılan bu yöntem bant genişliğini azaltır ve özellikle büyük varlıklar için sorgu performansını iyileştirebilir.</span><span class="sxs-lookup"><span data-stu-id="7087e-186">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="7087e-187">Aşağıdaki kodda yer alan sorgu yalnızca tablodaki varlıkların e-posta adreslerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="7087e-187">The query in the following code returns only the email addresses of entities in the table.</span></span> <span data-ttu-id="7087e-188">Bu, [DynamicTableEntity][dotnet_DynamicTableEntity] ve ayrıca [EntityResolver][dotnet_EntityResolver] sorgusu kullanılarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="7087e-188">This is done by using a query of [DynamicTableEntity][dotnet_DynamicTableEntity] and also [EntityResolver][dotnet_EntityResolver].</span></span> <span data-ttu-id="7087e-189">[Upsert ve Sorgu Projeksiyon Tanıtımı blog yazısı][blog_post_upsert] ile projeksiyon hakkında daha fazla bilgi edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7087e-189">You can learn more about projection in the [Introducing Upsert and Query Projection blog post][blog_post_upsert].</span></span> <span data-ttu-id="7087e-190">Projeksiyon depolama öykünücüsünde desteklenmez, bu nedenle bu kod yalnızca Tablo hizmetinde bir hesap kullanırken çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="7087e-190">Projection is not supported by the storage emulator, so this code runs only when you're using an account in the Table service.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Define the query, and select only the Email property.
TableQuery<DynamicTableEntity> projectionQuery = new TableQuery<DynamicTableEntity>().Select(new string[] { "Email" });

// Define an entity resolver to work with the entity after retrieval.
EntityResolver<string> resolver = (pk, rk, ts, props, etag) => props.ContainsKey("Email") ? props["Email"].StringValue : null;

foreach (string projectedEmail in table.ExecuteQuery(projectionQuery, resolver, null, null))
{
    Console.WriteLine(projectedEmail);
}
```

## <a name="delete-an-entity"></a><span data-ttu-id="7087e-191">Bir varlığı silme</span><span class="sxs-lookup"><span data-stu-id="7087e-191">Delete an entity</span></span>
<span data-ttu-id="7087e-192">Bir varlığı güncelleştirmek için gösterilen aynı yöntemi kullanarak, bir varlığı aldıktan sonra kolayca silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7087e-192">You can easily delete an entity after you have retrieved it by using the same pattern shown for updating an entity.</span></span> <span data-ttu-id="7087e-193">Aşağıdaki kod bir müşteri girişini alır ve siler.</span><span class="sxs-lookup"><span data-stu-id="7087e-193">The following code retrieves and deletes a customer entity.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that expects a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign the result to a CustomerEntity.
CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

// Create the Delete TableOperation.
if (deleteEntity != null)
{
    TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

    // Execute the operation.
    table.Execute(deleteOperation);

    Console.WriteLine("Entity deleted.");
}
else
{
    Console.WriteLine("Could not retrieve the entity.");
}
```

## <a name="delete-a-table"></a><span data-ttu-id="7087e-194">Bir tablo silme</span><span class="sxs-lookup"><span data-stu-id="7087e-194">Delete a table</span></span>
<span data-ttu-id="7087e-195">Son olarak aşağıdaki kod örneği bir depolama hesabından bir tablo siler.</span><span class="sxs-lookup"><span data-stu-id="7087e-195">Finally, the following code example deletes a table from a storage account.</span></span> <span data-ttu-id="7087e-196">Silinen bir tablo, silme işleminin ardından yeniden oluşturma için belirli bir süre kullanılamayacaktır.</span><span class="sxs-lookup"><span data-stu-id="7087e-196">A table that has been deleted will be unavailable to be re-created for a period of time following the deletion.</span></span>

```csharp
// Retrieve the storage account from the connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create the table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create the CloudTable that represents the "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Delete the table it if exists.
table.DeleteIfExists();
```

## <a name="retrieve-entities-in-pages-asynchronously"></a><span data-ttu-id="7087e-197">Sayfalarda zaman uyumsuz olarak varlıkları alma</span><span class="sxs-lookup"><span data-stu-id="7087e-197">Retrieve entities in pages asynchronously</span></span>
<span data-ttu-id="7087e-198">Çok sayıda varlık okuyorsanız ve tamamının dönmesini beklemek yerine alındıkları gibi varlıkları işlemek/görüntülemek istiyorsanız, bölümlendirilmiş bir sorgu kullanarak varlıkları alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7087e-198">If you are reading a large number of entities, and you want to process/display entities as they are retrieved rather than waiting for them all to return, you can retrieve entities by using a segmented query.</span></span> <span data-ttu-id="7087e-199">Bu örnek, geniş bir sonuç kümesinin dönmesini beklerken çalıştırmanın engellenmemesi için Zaman Uyumsuz - Bekleme yöntemi kullanarak sayfalardaki sonuçların nasıl döndürüleceğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="7087e-199">This example shows how to return results in pages by using the Async-Await pattern so that execution is not blocked while you're waiting for a large set of results to return.</span></span> <span data-ttu-id="7087e-200">.NET’te Zaman Uyumsuz-Bekleme yönteminin kullanılması ile ilgili daha fazla ayrıntı için bkz. [Zaman Uyumsuz ve Bekleme ile zaman uyumsuz programlama (C# ve Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span><span class="sxs-lookup"><span data-stu-id="7087e-200">For more details on using the Async-Await pattern in .NET, see [Asynchronous programming with Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span></span>

```csharp
// Initialize a default TableQuery to retrieve all the entities in the table.
TableQuery<CustomerEntity> tableQuery = new TableQuery<CustomerEntity>();

// Initialize the continuation token to null to start from the beginning of the table.
TableContinuationToken continuationToken = null;

do
{
    // Retrieve a segment (up to 1,000 entities).
    TableQuerySegment<CustomerEntity> tableQueryResult =
        await table.ExecuteQuerySegmentedAsync(tableQuery, continuationToken);

    // Assign the new continuation token to tell the service where to
    // continue on the next iteration (or null if it has reached the end).
    continuationToken = tableQueryResult.ContinuationToken;

    // Print the number of rows retrieved.
    Console.WriteLine("Rows retrieved {0}", tableQueryResult.Results.Count);

// Loop until a null continuation token is received, indicating the end of the table.
} while(continuationToken != null);
```

## <a name="next-steps"></a><span data-ttu-id="7087e-201">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7087e-201">Next steps</span></span>
<span data-ttu-id="7087e-202">Table Storage’ın temellerini öğrendiğinize göre, daha karmaşık depolama görevleri hakkında daha fazla bilgi edinmek için bu bağlantıları takip edin:</span><span class="sxs-lookup"><span data-stu-id="7087e-202">Now that you've learned the basics of Table storage, follow these links to learn about more complex storage tasks:</span></span>

* <span data-ttu-id="7087e-203">[Microsoft Azure Depolama Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md), Microsoft’un Windows, macOS ve Linux üzerinde Azure Depolama verileriyle görsel olarak çalışmanızı sağlayan ücretsiz ve tek başına uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="7087e-203">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="7087e-204">[.NET’te Azure Table Storage Kullanmaya Başlama](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/) bölümünde daha fazla Tablo depolama örneği bulabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="7087e-204">See more Table storage samples in [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)</span></span>
* <span data-ttu-id="7087e-205">Kullanılabilir API’ler ile ilgili eksiksiz bilgiler için Tablo hizmeti başvuru belgelerini görüntüleyin:</span><span class="sxs-lookup"><span data-stu-id="7087e-205">View the Table service reference documentation for complete details about available APIs:</span></span>
* [<span data-ttu-id="7087e-206">.NET başvurusu için Depolama İstemci Kitaplığı</span><span class="sxs-lookup"><span data-stu-id="7087e-206">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
* [<span data-ttu-id="7087e-207">REST API başvurusu</span><span class="sxs-lookup"><span data-stu-id="7087e-207">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="7087e-208">[Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md) kullanarak Azure Storage ile birlikte çalışmak üzere yazdığınız kodları nasıl sadeleştireceğinizi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="7087e-208">Learn how to simplify the code you write to work with Azure Storage by using the [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)</span></span>
* <span data-ttu-id="7087e-209">Azure’da veri depolama ile ilgili ek seçenekler hakkında daha fazla bilgi edinmek için daha fazla özellik kılavuzu görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="7087e-209">View more feature guides to learn about additional options for storing data in Azure.</span></span>
* <span data-ttu-id="7087e-210">Yapılandırılmamış verileri depolamak için [.NET kullanarak Azure Blob Storage’ı kullanmaya başlayın](storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="7087e-210">[Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) to store unstructured data.</span></span>
* <span data-ttu-id="7087e-211">İlişkisel verileri depolamak için [.NET (C#) kullanarak SQL Veritabanı'na bağlanın](../sql-database/sql-database-develop-dotnet-simple.md).</span><span class="sxs-lookup"><span data-stu-id="7087e-211">[Connect to SQL Database by using .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) to store relational data.</span></span>

[Download and install the Azure SDK for .NET]: /develop/net/
[Creating an Azure Project in Visual Studio]: http://msdn.microsoft.com/library/azure/ee405487.aspx

[blog_post_upsert]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx

[dotnet_api_ref]: https://msdn.microsoft.com/library/azure/mt347887.aspx
[dotnet_CloudTableClient]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtableclient.aspx
[dotnet_CloudTable]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtable.aspx
[dotnet_CloudTable_Execute]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtable.execute.aspx
[dotnet_CloudTable_ExecuteBatch]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.cloudtable.executebatch.aspx
[dotnet_DynamicTableEntity]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.dynamictableentity.aspx
[dotnet_EntityResolver]: https://msdn.microsoft.com/library/jj733144.aspx
[dotnet_TableBatchOperation]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablebatchoperation.aspx
[dotnet_TableBatchOperation_Insert]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablebatchoperation.insert.aspx
[dotnet_TableEntity]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableentity.aspx
[dotnet_TableOperation]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.aspx
[dotnet_TableOperation_Insert]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.insert.aspx
[dotnet_TableOperation_InsertOrReplace]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.insertorreplace.aspx
[dotnet_TableOperation_Replace]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableoperation.replace.aspx
[dotnet_TableQuery]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tablequery.aspx
[dotnet_TableResult]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableresult.aspx
[dotnet_TableResult_Result]: https://msdn.microsoft.com/library/microsoft.windowsazure.storage.table.tableresult.result.aspx
