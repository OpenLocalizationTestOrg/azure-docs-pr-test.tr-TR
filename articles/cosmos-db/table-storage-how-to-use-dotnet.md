---
title: ".NET kullanarak Azure Table storage'ı kullanmaya aaaGet | Microsoft Docs"
description: "Bir NoSQL veri deposu olan Azure Table storage kullanılarak hello bulutta yapılandırılmış veri depolayın."
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: fe46d883-7bed-49dd-980e-5c71df36adb3
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 04/10/2017
ms.author: mimig
ms.openlocfilehash: a3e9a4c6f6fd5e724535b86a3f99cd4c161de6de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-table-storage-using-net"></a><span data-ttu-id="30537-103">.NET kullanarak Azure Table Storage’ı kullanmaya başlayın</span><span class="sxs-lookup"><span data-stu-id="30537-103">Get started with Azure Table storage using .NET</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

<span data-ttu-id="30537-104">Azure Table storage şemasız tasarım ile bir anahtar/öznitelik sağlama verilerini hello bulutta depolamak yapılandırılmış NoSQL depolayan bir hizmettir.</span><span class="sxs-lookup"><span data-stu-id="30537-104">Azure Table storage is a service that stores structured NoSQL data in hello cloud, providing a key/attribute store with a schemaless design.</span></span> <span data-ttu-id="30537-105">Table storage şemasız olduğu için uygulama geliştikçe verilerinizi hello olarak gereken kolay tooadapt var.</span><span class="sxs-lookup"><span data-stu-id="30537-105">Because Table storage is schemaless, it's easy tooadapt your data as hello needs of your application evolve.</span></span> <span data-ttu-id="30537-106">Erişim tooTable depolama verileri hızlı ve birçok türdeki uygulamayı için düşük maliyetli ve maliyeti genellikle benzer hacimdeki veriler için geleneksel SQL'e daha düşüktür.</span><span class="sxs-lookup"><span data-stu-id="30537-106">Access tooTable storage data is fast and cost-effective for many types of applications, and is typically lower in cost than traditional SQL for similar volumes of data.</span></span>

<span data-ttu-id="30537-107">Tablo depolama toostore esnek veri kümelerini kullanıcı verilerini gibi web uygulamaları, adres defterleri, cihaz bilgilerini veya diğer hizmetiniz için gerekli meta veri türleri için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30537-107">You can use Table storage toostore flexible datasets like user data for web applications, address books, device information, or other types of metadata your service requires.</span></span> <span data-ttu-id="30537-108">Bir tablodaki herhangi bir sayıda varlık depolayabilirsiniz ve bir depolama hesabı tabloları, hello depolama hesabının kapasite sınırını toohello herhangi bir sayıda içerebilir.</span><span class="sxs-lookup"><span data-stu-id="30537-108">You can store any number of entities in a table, and a storage account may contain any number of tables, up toohello capacity limit of hello storage account.</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="30537-109">Bu öğretici hakkında</span><span class="sxs-lookup"><span data-stu-id="30537-109">About this tutorial</span></span>
<span data-ttu-id="30537-110">Bu öğretici şunların nasıl yapıldığını gösterir toouse hello [.NET için Azure Storage istemci Kitaplığı](https://www.nuget.org/packages/WindowsAzure.Storage/) bazı ortak Azure Table depolama senaryolarında.</span><span class="sxs-lookup"><span data-stu-id="30537-110">This tutorial shows you how toouse hello [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/) in some common Azure Table storage scenarios.</span></span> <span data-ttu-id="30537-111">Bu senaryolar, tablo oluşturup silme ve tablo verileri ekleme, güncelleştirme, silme ve sorgulama işlemleri için C# örnekleri kullanılarak sunulmaktadır.</span><span class="sxs-lookup"><span data-stu-id="30537-111">These scenarios are presented using C# examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30537-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="30537-112">Prerequisites</span></span>

<span data-ttu-id="30537-113">Başarıyla Bu öğreticiyi toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="30537-113">You need hello following toocomplete this tutorial successfully:</span></span>

* [<span data-ttu-id="30537-114">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="30537-114">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/downloads/)
* [<span data-ttu-id="30537-115">.NET için Azure Depolama İstemcisi</span><span class="sxs-lookup"><span data-stu-id="30537-115">Azure Storage Client Library for .NET</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [<span data-ttu-id="30537-116">.NET için Azure Yapılandırma Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="30537-116">Azure Configuration Manager for .NET</span></span>](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [<span data-ttu-id="30537-117">Azure depolama hesabı</span><span class="sxs-lookup"><span data-stu-id="30537-117">Azure storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a><span data-ttu-id="30537-118">Daha fazla örnek</span><span class="sxs-lookup"><span data-stu-id="30537-118">More samples</span></span>
<span data-ttu-id="30537-119">Tablo depolama kullanan diğer örnekler için [.NET’te Azure Table Storage Kullanmaya Başlama](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="30537-119">For additional examples using Table storage, see [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/).</span></span> <span data-ttu-id="30537-120">Merhaba örnek uygulamayı indirin ve çalıştırın veya hello kodu github'da göz atın.</span><span class="sxs-lookup"><span data-stu-id="30537-120">You can download hello sample application and run it, or browse hello code on GitHub.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a><span data-ttu-id="30537-121">Using yönergeleri ekleme</span><span class="sxs-lookup"><span data-stu-id="30537-121">Add using directives</span></span>
<span data-ttu-id="30537-122">Merhaba aşağıdakileri ekleyin **kullanarak** hello yönergeleri toohello üst `Program.cs` dosyası:</span><span class="sxs-lookup"><span data-stu-id="30537-122">Add hello following **using** directives toohello top of hello `Program.cs` file:</span></span>

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Table; // Namespace for Table storage types
```

### <a name="parse-hello-connection-string"></a><span data-ttu-id="30537-123">Merhaba bağlantı dizesini ayrıştırma</span><span class="sxs-lookup"><span data-stu-id="30537-123">Parse hello connection string</span></span>
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-table-service-client"></a><span data-ttu-id="30537-124">Merhaba tablo hizmeti istemcisi oluşturma</span><span class="sxs-lookup"><span data-stu-id="30537-124">Create hello Table service client</span></span>
<span data-ttu-id="30537-125">Merhaba [CloudTableClient] [ dotnet_CloudTableClient] sınıfı sağlar, size, tooretrieve tabloları ve varlıkları tablo depolama alanına depolanır.</span><span class="sxs-lookup"><span data-stu-id="30537-125">hello [CloudTableClient][dotnet_CloudTableClient] class enables you tooretrieve tables and entities stored in Table storage.</span></span> <span data-ttu-id="30537-126">Tek yönlü toocreate hello tablo hizmeti istemcisi şöyledir:</span><span class="sxs-lookup"><span data-stu-id="30537-126">Here's one way toocreate hello Table service client:</span></span>

```csharp
// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```

<span data-ttu-id="30537-127">Artık veri okuyan ve yazan veri tooTable depolama hazır toowrite kodu bulunur.</span><span class="sxs-lookup"><span data-stu-id="30537-127">Now you are ready toowrite code that reads data from and writes data tooTable storage.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="30537-128">Bir tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="30537-128">Create a table</span></span>
<span data-ttu-id="30537-129">Bu örnekte gösterilir nasıl toocreate zaten yoksa, tablo:</span><span class="sxs-lookup"><span data-stu-id="30537-129">This example shows how toocreate a table if it does not already exist:</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Retrieve a reference toohello table.
CloudTable table = tableClient.GetTableReference("people");

// Create hello table if it doesn't exist.
table.CreateIfNotExists();
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="30537-130">Bir varlık tooa tablo ekleme</span><span class="sxs-lookup"><span data-stu-id="30537-130">Add an entity tooa table</span></span>
<span data-ttu-id="30537-131">Varlıkları türetilen özel bir sınıf kullanarak tooC # nesnelerini eşleme [TableEntity][dotnet_TableEntity].</span><span class="sxs-lookup"><span data-stu-id="30537-131">Entities map tooC# objects by using a custom class derived from [TableEntity][dotnet_TableEntity].</span></span> <span data-ttu-id="30537-132">bir varlık tooa tablosu tooadd varlığınız hello özelliklerini tanımlayan bir sınıf oluşturun.</span><span class="sxs-lookup"><span data-stu-id="30537-132">tooadd an entity tooa table, create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="30537-133">Merhaba aşağıdaki kod hello müşterinin adını hello satır anahtarını ve Soyadı gibi hello bölüm anahtarı olarak kullanan bir varlık sınıfı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="30537-133">hello following code defines an entity class that uses hello customer's first name as hello row key and last name as hello partition key.</span></span> <span data-ttu-id="30537-134">Birlikte, bir varlığın bölüm ve satır anahtarı, hello tabloda benzersizce.</span><span class="sxs-lookup"><span data-stu-id="30537-134">Together, an entity's partition and row key uniquely identify it in hello table.</span></span> <span data-ttu-id="30537-135">Anahtarları aynı bölüm anahtarına farklı sahip varlıklar daha hızlı sorgulanabilir hello varlıklarıyla bölüm, ancak farklı bölüm anahtarlarının kullanılması paralel işlemler daha fazla ölçeklenebilirlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="30537-135">Entities with hello same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="30537-136">Varlıkları toobe tablolarında depolanır, örneğin hello türetilen desteklenen bir türde olmalıdır [TableEntity] [ dotnet_TableEntity] sınıfı.</span><span class="sxs-lookup"><span data-stu-id="30537-136">Entities toobe stored in tables must be of a supported type, for example derived from hello [TableEntity][dotnet_TableEntity] class.</span></span> <span data-ttu-id="30537-137">Toostore bir tabloda istediğiniz varlık özellikleri hello türünün ortak özelliklerine olması ve alma ve değerlerin ayarını destekler.</span><span class="sxs-lookup"><span data-stu-id="30537-137">Entity properties you'd like toostore in a table must be public properties of hello type, and support both getting and setting of values.</span></span> <span data-ttu-id="30537-138">Bununla birlikte varlık türü parametresiz bir oluşturucu *olmalıdır*.</span><span class="sxs-lookup"><span data-stu-id="30537-138">Also, your entity type *must* expose a parameter-less constructor.</span></span>

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

<span data-ttu-id="30537-139">Varlıklarla ilgili tablo işlemleri hello gerçekleştirilir [CloudTable] [ dotnet_CloudTable] hello "bir tablo oluşturma" bölümünde daha önce oluşturduğunuz nesne.</span><span class="sxs-lookup"><span data-stu-id="30537-139">Table operations that involve entities are performed via hello [CloudTable][dotnet_CloudTable] object that you created earlier in hello "Create a table" section.</span></span> <span data-ttu-id="30537-140">Merhaba gerçekleştirilen işlem toobe tarafından temsil edilen bir [TableOperation] [ dotnet_TableOperation] nesnesi.</span><span class="sxs-lookup"><span data-stu-id="30537-140">hello operation toobe performed is represented by a [TableOperation][dotnet_TableOperation] object.</span></span> <span data-ttu-id="30537-141">Merhaba aşağıdaki kod örneğinde hello oluşturulmasını hello gösterir [CloudTable] [ dotnet_CloudTable] nesnesi ve ardından bir **CustomerEntity** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="30537-141">hello following code example shows hello creation of hello [CloudTable][dotnet_CloudTable] object and then a **CustomerEntity** object.</span></span> <span data-ttu-id="30537-142">tooprepare hello işlemi, bir [TableOperation] [ dotnet_TableOperation] nesne hello tabloya tooinsert hello müşteri varlığı oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="30537-142">tooprepare hello operation, a [TableOperation][dotnet_TableOperation] object is created tooinsert hello customer entity into hello table.</span></span> <span data-ttu-id="30537-143">Son olarak, hello işlemi çağrılarak çalıştırılır [CloudTable][dotnet_CloudTable].[ Yürütme][dotnet_CloudTable_Execute].</span><span class="sxs-lookup"><span data-stu-id="30537-143">Finally, hello operation is executed by calling [CloudTable][dotnet_CloudTable].[Execute][dotnet_CloudTable_Execute].</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute hello insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="30537-144">Toplu işlem varlık yerleştirme</span><span class="sxs-lookup"><span data-stu-id="30537-144">Insert a batch of entities</span></span>
<span data-ttu-id="30537-145">Bir tabloya tek bir yazma işlemiyle çok sayıda varlık yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30537-145">You can insert a batch of entities into a table in one write operation.</span></span> <span data-ttu-id="30537-146">Toplu işlemler ile ilgili diğer notlar:</span><span class="sxs-lookup"><span data-stu-id="30537-146">Some other notes on batch operations:</span></span>

* <span data-ttu-id="30537-147">Güncelleştirmeleri, siler ve eklemeleri gerçekleştirebilirsiniz hello aynı tek toplu işlemi.</span><span class="sxs-lookup"><span data-stu-id="30537-147">You can perform updates, deletes, and inserts in hello same single batch operation.</span></span>
* <span data-ttu-id="30537-148">Tek bir toplu işlem too100 varlık içerebilir.</span><span class="sxs-lookup"><span data-stu-id="30537-148">A single batch operation can include up too100 entities.</span></span>
* <span data-ttu-id="30537-149">Tek bir toplu işlem tüm varlıkları hello olmalıdır aynı bölüm anahtarı.</span><span class="sxs-lookup"><span data-stu-id="30537-149">All entities in a single batch operation must have hello same partition key.</span></span>
* <span data-ttu-id="30537-150">Olası tooperform toplu işlem olarak bir sorgu olmakla birlikte, hello hello toplu işlemdeki tek işlem olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="30537-150">While it is possible tooperform a query as a batch operation, it must be hello only operation in hello batch.</span></span>

<span data-ttu-id="30537-151">Merhaba aşağıdaki kod örneği iki varlık nesnesi oluşturur ve her çok ekler[TableBatchOperation] [ dotnet_TableBatchOperation] hello kullanarak [Ekle] [ dotnet_TableBatchOperation_Insert] yöntem.</span><span class="sxs-lookup"><span data-stu-id="30537-151">hello following code example creates two entity objects and adds each too[TableBatchOperation][dotnet_TableBatchOperation] by using hello [Insert][dotnet_TableBatchOperation_Insert] method.</span></span> <span data-ttu-id="30537-152">Ardından, [CloudTable][dotnet_CloudTable].[ ExecuteBatch] [ dotnet_CloudTable_ExecuteBatch] tooexecute hello işlem çağrılır.</span><span class="sxs-lookup"><span data-stu-id="30537-152">Then, [CloudTable][dotnet_CloudTable].[ExecuteBatch][dotnet_CloudTable_ExecuteBatch] is called tooexecute hello operation.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create hello batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it toohello table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it toohello table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities toohello batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute hello batch operation.
table.ExecuteBatch(batchOperation);
```

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="30537-153">Tüm varlıkları bir bölüme alma</span><span class="sxs-lookup"><span data-stu-id="30537-153">Retrieve all entities in a partition</span></span>
<span data-ttu-id="30537-154">tooquery kullanımı bir bölümdeki tüm varlıklar için bir tablo bir [TableQuery] [ dotnet_TableQuery] nesnesi.</span><span class="sxs-lookup"><span data-stu-id="30537-154">tooquery a table for all entities in a partition, use a [TableQuery][dotnet_TableQuery] object.</span></span> <span data-ttu-id="30537-155">Merhaba aşağıdaki kod örneğinde 'Smith' hello bölüm anahtarı olduğu varlıklar için bir filtre belirtir.</span><span class="sxs-lookup"><span data-stu-id="30537-155">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="30537-156">Bu örnekte her varlığın hello sorgu sonuçları toohello konsolunda hello alanlarını yazdırır.</span><span class="sxs-lookup"><span data-stu-id="30537-156">This example prints hello fields of each entity in hello query results toohello console.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Construct hello query operation for all customer entities where PartitionKey="Smith".
TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

// Print hello fields for each customer.
foreach (CustomerEntity entity in table.ExecuteQuery(query))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="30537-157">Bir bölüme bir grup varlık alma</span><span class="sxs-lookup"><span data-stu-id="30537-157">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="30537-158">Tüm varlıkları bir bölüme tooquery istemiyorsanız, hello bölüm anahtarı Filtresi ile bir satır anahtarı filtresini birleştirerek bir aralık belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30537-158">If you don't want tooquery all entities in a partition, you can specify a range by combining hello partition key filter with a row key filter.</span></span> <span data-ttu-id="30537-159">Merhaba aşağıdaki kod örneği iki filtreleri tooget tüm varlıklar 'burada hello satır anahtarı (ad) hello alfabede 'E' önce bir harf ile başlar, ardından hello sorgu sonuçlarını yazdırır Smith' bölümünde kullanır.</span><span class="sxs-lookup"><span data-stu-id="30537-159">hello following code example uses two filters tooget all entities in partition 'Smith' where hello row key (first name) starts with a letter before 'E' in hello alphabet, then prints hello query results.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create hello table query.
TableQuery<CustomerEntity> rangeQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.CombineFilters(
        TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"),
        TableOperators.And,
        TableQuery.GenerateFilterCondition("RowKey", QueryComparisons.LessThan, "E")));

// Loop through hello results, displaying information about hello entity.
foreach (CustomerEntity entity in table.ExecuteQuery(rangeQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="30537-160">Tek bir varlık alma</span><span class="sxs-lookup"><span data-stu-id="30537-160">Retrieve a single entity</span></span>
<span data-ttu-id="30537-161">Bir sorgu tooretrieve tek, belirli bir varlığı yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30537-161">You can write a query tooretrieve a single, specific entity.</span></span> <span data-ttu-id="30537-162">Merhaba aşağıdaki kod kullanır [TableOperation] [ dotnet_TableOperation] toospecify hello Müşteri 'Ben Smith'.</span><span class="sxs-lookup"><span data-stu-id="30537-162">hello following code uses [TableOperation][dotnet_TableOperation] toospecify hello customer 'Ben Smith'.</span></span> <span data-ttu-id="30537-163">Bu yöntem bir koleksiyon yerine yalnızca bir varlık döndürür ve hello döndürülen değer [TableResult][dotnet_TableResult].[ Sonuç] [ dotnet_TableResult_Result] olan bir **CustomerEntity** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="30537-163">This method returns just one entity rather than a collection, and hello returned value in [TableResult][dotnet_TableResult].[Result][dotnet_TableResult_Result] is a **CustomerEntity** object.</span></span> <span data-ttu-id="30537-164">Bir sorguda hem Bölüm hem de satır anahtarını belirterek hello en hızlı yolu tooretrieve hello tablo hizmetinden tek bir varlık olur.</span><span class="sxs-lookup"><span data-stu-id="30537-164">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello Table service.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Print hello phone number of hello result.
if (retrievedResult.Result != null)
{
    Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
}
else
{
    Console.WriteLine("hello phone number could not be retrieved.");
}
```

## <a name="replace-an-entity"></a><span data-ttu-id="30537-165">Bir varlığı değiştirme</span><span class="sxs-lookup"><span data-stu-id="30537-165">Replace an entity</span></span>
<span data-ttu-id="30537-166">bir varlık tooupdate hello tablo hizmetinden alın, hello varlık nesnesini değiştirin ve ardından hello Değişiklikleri Kaydet toohello tablo hizmeti yeniden.</span><span class="sxs-lookup"><span data-stu-id="30537-166">tooupdate an entity, retrieve it from hello Table service, modify hello entity object, and then save hello changes back toohello Table service.</span></span> <span data-ttu-id="30537-167">Merhaba aşağıdaki kod mevcut bir müşterinin telefon numarasını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="30537-167">hello following code changes an existing customer's phone number.</span></span> <span data-ttu-id="30537-168">[Insert][dotnet_TableOperation_Insert] yöntemini çağırmak yerine bu kod [Replace][dotnet_TableOperation_Replace] kullanır.</span><span class="sxs-lookup"><span data-stu-id="30537-168">Instead of calling [Insert][dotnet_TableOperation_Insert], this code uses [Replace][dotnet_TableOperation_Replace].</span></span> <span data-ttu-id="30537-169">[Değiştir] [ dotnet_TableOperation_Replace] onu, hello işlemi başarısız olur; bu durumda alındığından beri hello varlık hello sunucuda değiştirilmediği sürece nedenler hello varlık toobe tam olarak hello sunucu üzerinde değiştirildi.</span><span class="sxs-lookup"><span data-stu-id="30537-169">[Replace][dotnet_TableOperation_Replace] causes hello entity toobe fully replaced on hello server, unless hello entity on hello server has changed since it was retrieved, in which case hello operation will fail.</span></span> <span data-ttu-id="30537-170">Uygulamanızı bir değişikliğin yanlışlıkla üzerine yazılmasını arasında alma hello ve uygulamanızın başka bir bileşen tarafından güncelleştirme yapılan tooprevent hatasıdır.</span><span class="sxs-lookup"><span data-stu-id="30537-170">This failure is tooprevent your application from inadvertently overwriting a change made between hello retrieval and update by another component of your application.</span></span> <span data-ttu-id="30537-171">Merhaba bu hatanın uygun işleme tooretrieve hello yeniden varlıktır, (hala geçerli ise) değişiklikleri yapın ve ardından başka bir gerçekleştirin [Değiştir] [ dotnet_TableOperation_Replace] işlemi.</span><span class="sxs-lookup"><span data-stu-id="30537-171">hello proper handling of this failure is tooretrieve hello entity again, make your changes (if still valid), and then perform another [Replace][dotnet_TableOperation_Replace] operation.</span></span> <span data-ttu-id="30537-172">Merhaba sonraki bölümde gösterir, nasıl toooverride bu davranışı.</span><span class="sxs-lookup"><span data-stu-id="30537-172">hello next section will show you how toooverride this behavior.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign hello result tooa CustomerEntity object.
CustomerEntity updateEntity = (CustomerEntity)retrievedResult.Result;

if (updateEntity != null)
{
    // Change hello phone number.
    updateEntity.PhoneNumber = "425-555-0105";

    // Create hello Replace TableOperation.
    TableOperation updateOperation = TableOperation.Replace(updateEntity);

    // Execute hello operation.
    table.Execute(updateOperation);

    Console.WriteLine("Entity updated.");
}
else
{
    Console.WriteLine("Entity could not be retrieved.");
}
```

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="30537-173">Bir varlığı yerleştirme veya değiştirme</span><span class="sxs-lookup"><span data-stu-id="30537-173">Insert-or-replace an entity</span></span>
<span data-ttu-id="30537-174">[Değiştir] [ dotnet_TableOperation_Replace] hello varlık hello sunucudan alındığından beri değiştirilmişse işlemleri başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="30537-174">[Replace][dotnet_TableOperation_Replace] operations will fail if hello entity has been changed since it was retrieved from hello server.</span></span> <span data-ttu-id="30537-175">Ayrıca, hello varlık hello sunucusundan ilk sırada hello için aldığınız gerekir [Değiştir] [ dotnet_TableOperation_Replace] toobe işlemi başarılı.</span><span class="sxs-lookup"><span data-stu-id="30537-175">Furthermore, you must retrieve hello entity from hello server first in order for hello [Replace][dotnet_TableOperation_Replace] operation toobe successful.</span></span> <span data-ttu-id="30537-176">Bazı durumlarda, Bununla birlikte, hello varlık hello sunucuda bulunduğundan ve depolanan hello geçerli değerlerin ilgisiz olup olmadığını bilemeyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30537-176">Sometimes, however, you don't know if hello entity exists on hello server and hello current values stored in it are irrelevant.</span></span> <span data-ttu-id="30537-177">Güncelleştirmeniz tümünün üzerine yazmalıdır.</span><span class="sxs-lookup"><span data-stu-id="30537-177">Your update should overwrite them all.</span></span> <span data-ttu-id="30537-178">tooaccomplish Bu, kullanacağınız bir [Yerleştir veya Değiştir] [ dotnet_TableOperation_InsertOrReplace] işlemi.</span><span class="sxs-lookup"><span data-stu-id="30537-178">tooaccomplish this, you would use an [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation.</span></span> <span data-ttu-id="30537-179">Bu işlem yok veya bu zaman hello yapılan son güncelleştirmeden bağımsız olarak, varsa yerini hello varlık ekler.</span><span class="sxs-lookup"><span data-stu-id="30537-179">This operation inserts hello entity if it doesn't exist, or replaces it if it does, regardless of when hello last update was made.</span></span>

<span data-ttu-id="30537-180">Aşağıdaki kod örneğine hello 'Gamze Can' için müşteri varlığı oluşturulur ve hello 'Kişiler' tablosuna.</span><span class="sxs-lookup"><span data-stu-id="30537-180">In hello following code example, a customer entity for 'Fred Jones' is created and inserted into hello 'people' table.</span></span> <span data-ttu-id="30537-181">Merhaba ardından, kullandığımız [Yerleştir veya Değiştir] [ dotnet_TableOperation_InsertOrReplace] işlemi toosave hello sahip bir varlık aynı bölüm anahtarı (CAN) ve satır anahtarı (Gamze) toohello sunucu hello PhoneNumber farklı bir değerle bu süre özellik.</span><span class="sxs-lookup"><span data-stu-id="30537-181">Next, we use hello [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] operation toosave an entity with hello same partition key (Jones) and row key (Fred) toohello server, this time with a different value for hello PhoneNumber property.</span></span> <span data-ttu-id="30537-182">[InsertOrReplace][dotnet_TableOperation_InsertOrReplace] özelliğini kullandığımız için tüm özellik değerleri değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="30537-182">Because we use [InsertOrReplace][dotnet_TableOperation_InsertOrReplace], all of its property values are replaced.</span></span> <span data-ttu-id="30537-183">'Gamze Can' varlık zaten hello tablosunda yüklediniz, ancak bunu eklenmiş.</span><span class="sxs-lookup"><span data-stu-id="30537-183">However, if a 'Fred Jones' entity hadn't already existed in hello table, it would have been inserted.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a customer entity.
CustomerEntity customer3 = new CustomerEntity("Jones", "Fred");
customer3.Email = "Fred@contoso.com";
customer3.PhoneNumber = "425-555-0106";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer3);

// Execute hello operation.
table.Execute(insertOperation);

// Create another customer entity with hello same partition key and row key.
// We've already created a 'Fred Jones' entity and saved it toothe
// 'people' table, but here we're specifying a different value for the
// PhoneNumber property.
CustomerEntity customer4 = new CustomerEntity("Jones", "Fred");
customer4.Email = "Fred@contoso.com";
customer4.PhoneNumber = "425-555-0107";

// Create hello InsertOrReplace TableOperation.
TableOperation insertOrReplaceOperation = TableOperation.InsertOrReplace(customer4);

// Execute hello operation. Because a 'Fred Jones' entity already exists in the
// 'people' table, its property values will be overwritten by those in this
// CustomerEntity. If 'Fred Jones' didn't already exist, hello entity would be
// added toohello table.
table.Execute(insertOrReplaceOperation);
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="30537-184">Giriş özellikleri alt kümesi sorgulama</span><span class="sxs-lookup"><span data-stu-id="30537-184">Query a subset of entity properties</span></span>
<span data-ttu-id="30537-185">Tablo sorgusu, tüm hello varlık özellikleri yerine bir varlıktaki birkaç özelliği alabilir.</span><span class="sxs-lookup"><span data-stu-id="30537-185">A table query can retrieve just a few properties from an entity instead of all hello entity properties.</span></span> <span data-ttu-id="30537-186">Projeksiyon olarak adlandırılan bu yöntem bant genişliğini azaltır ve özellikle büyük varlıklar için sorgu performansını iyileştirebilir.</span><span class="sxs-lookup"><span data-stu-id="30537-186">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="30537-187">koddan hello Hello sorguda yalnızca hello e-posta adresleri varlıkların hello tablodaki döndürür.</span><span class="sxs-lookup"><span data-stu-id="30537-187">hello query in hello following code returns only hello email addresses of entities in hello table.</span></span> <span data-ttu-id="30537-188">Bu, [DynamicTableEntity][dotnet_DynamicTableEntity] ve ayrıca [EntityResolver][dotnet_EntityResolver] sorgusu kullanılarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="30537-188">This is done by using a query of [DynamicTableEntity][dotnet_DynamicTableEntity] and also [EntityResolver][dotnet_EntityResolver].</span></span> <span data-ttu-id="30537-189">Merhaba projeksiyon hakkında daha fazla bilgiyi [Tanıtımı Upsert ve sorgu projeksiyon blog yazısı][blog_post_upsert].</span><span class="sxs-lookup"><span data-stu-id="30537-189">You can learn more about projection in hello [Introducing Upsert and Query Projection blog post][blog_post_upsert].</span></span> <span data-ttu-id="30537-190">Bu kod yalnızca hello tablo hizmetinde bir hesap kullanırken çalıştırılır şekilde projeksiyon hello depolama öykünücüsü tarafından desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="30537-190">Projection is not supported by hello storage emulator, so this code runs only when you're using an account in hello Table service.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Define hello query, and select only hello Email property.
TableQuery<DynamicTableEntity> projectionQuery = new TableQuery<DynamicTableEntity>().Select(new string[] { "Email" });

// Define an entity resolver toowork with hello entity after retrieval.
EntityResolver<string> resolver = (pk, rk, ts, props, etag) => props.ContainsKey("Email") ? props["Email"].StringValue : null;

foreach (string projectedEmail in table.ExecuteQuery(projectionQuery, resolver, null, null))
{
    Console.WriteLine(projectedEmail);
}
```

## <a name="delete-an-entity"></a><span data-ttu-id="30537-191">Bir varlığı silme</span><span class="sxs-lookup"><span data-stu-id="30537-191">Delete an entity</span></span>
<span data-ttu-id="30537-192">Hello kullanarak aldıktan sonra bir varlık kolayca silebilirsiniz bir varlığı güncelleştirmek için gösterilen aynı düzeni.</span><span class="sxs-lookup"><span data-stu-id="30537-192">You can easily delete an entity after you have retrieved it by using hello same pattern shown for updating an entity.</span></span> <span data-ttu-id="30537-193">koddan hello alır ve bir müşteri varlığı siler.</span><span class="sxs-lookup"><span data-stu-id="30537-193">hello following code retrieves and deletes a customer entity.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Create a retrieve operation that expects a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello operation.
TableResult retrievedResult = table.Execute(retrieveOperation);

// Assign hello result tooa CustomerEntity.
CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

// Create hello Delete TableOperation.
if (deleteEntity != null)
{
    TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

    // Execute hello operation.
    table.Execute(deleteOperation);

    Console.WriteLine("Entity deleted.");
}
else
{
    Console.WriteLine("Could not retrieve hello entity.");
}
```

## <a name="delete-a-table"></a><span data-ttu-id="30537-194">Bir tablo silme</span><span class="sxs-lookup"><span data-stu-id="30537-194">Delete a table</span></span>
<span data-ttu-id="30537-195">Son olarak, aşağıdaki kod örneğine hello bir depolama hesabından bir tablo siler.</span><span class="sxs-lookup"><span data-stu-id="30537-195">Finally, hello following code example deletes a table from a storage account.</span></span> <span data-ttu-id="30537-196">Silinmiş bir tablo bir süre hello silmeyi izleyen yeniden oluşturulacak kullanılamaz toobe olacaktır.</span><span class="sxs-lookup"><span data-stu-id="30537-196">A table that has been deleted will be unavailable toobe re-created for a period of time following hello deletion.</span></span>

```csharp
// Retrieve hello storage account from hello connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable that represents hello "people" table.
CloudTable table = tableClient.GetTableReference("people");

// Delete hello table it if exists.
table.DeleteIfExists();
```

## <a name="retrieve-entities-in-pages-asynchronously"></a><span data-ttu-id="30537-197">Sayfalarda zaman uyumsuz olarak varlıkları alma</span><span class="sxs-lookup"><span data-stu-id="30537-197">Retrieve entities in pages asynchronously</span></span>
<span data-ttu-id="30537-198">Çok sayıda varlık okuyorsanız ve tooprocess/görüntü varlıklar alındıktan yerine şekilde kendileri için tüm tooreturn bekleniyor, varlıkları bölümlendirilmiş bir sorgu kullanarak alabileceğiniz istediğiniz istiyorsanız.</span><span class="sxs-lookup"><span data-stu-id="30537-198">If you are reading a large number of entities, and you want tooprocess/display entities as they are retrieved rather than waiting for them all tooreturn, you can retrieve entities by using a segmented query.</span></span> <span data-ttu-id="30537-199">Bu örnek, böylece yürütme sırasında engellenmeyen hello zaman uyumsuz-bekleme düzenini kullanarak sayfaları tooreturn sonuçlarında çok sayıda sonuç tooreturn için nasıl bekliyorsunuz gösterir.</span><span class="sxs-lookup"><span data-stu-id="30537-199">This example shows how tooreturn results in pages by using hello Async-Await pattern so that execution is not blocked while you're waiting for a large set of results tooreturn.</span></span> <span data-ttu-id="30537-200">Zaman uyumsuz-bekleme yönteminin deseninde .NET ile kullanma hakkında daha fazla ayrıntı hello için bkz: [uyumsuz ve bekleme (C# ve Visual Basic) ile zaman uyumsuz programlama](https://msdn.microsoft.com/library/hh191443.aspx).</span><span class="sxs-lookup"><span data-stu-id="30537-200">For more details on using hello Async-Await pattern in .NET, see [Asynchronous programming with Async and Await (C# and Visual Basic)](https://msdn.microsoft.com/library/hh191443.aspx).</span></span>

```csharp
// Initialize a default TableQuery tooretrieve all hello entities in hello table.
TableQuery<CustomerEntity> tableQuery = new TableQuery<CustomerEntity>();

// Initialize hello continuation token toonull toostart from hello beginning of hello table.
TableContinuationToken continuationToken = null;

do
{
    // Retrieve a segment (up too1,000 entities).
    TableQuerySegment<CustomerEntity> tableQueryResult =
        await table.ExecuteQuerySegmentedAsync(tableQuery, continuationToken);

    // Assign hello new continuation token tootell hello service where to
    // continue on hello next iteration (or null if it has reached hello end).
    continuationToken = tableQueryResult.ContinuationToken;

    // Print hello number of rows retrieved.
    Console.WriteLine("Rows retrieved {0}", tableQueryResult.Results.Count);

// Loop until a null continuation token is received, indicating hello end of hello table.
} while(continuationToken != null);
```

## <a name="next-steps"></a><span data-ttu-id="30537-201">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="30537-201">Next steps</span></span>
<span data-ttu-id="30537-202">Table Storage hello temel bilgileri öğrendiğinize göre bu bağlantıları toolearn daha karmaşık depolama görevleri hakkında izleyin:</span><span class="sxs-lookup"><span data-stu-id="30537-202">Now that you've learned hello basics of Table storage, follow these links toolearn about more complex storage tasks:</span></span>

* <span data-ttu-id="30537-203">[Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md) Windows, macOS ve Linux Azure Storage verilerle görsel olarak toowork sağlayan Microsoft boş bir tek başına uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="30537-203">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="30537-204">[.NET’te Azure Table Storage Kullanmaya Başlama](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/) bölümünde daha fazla Tablo depolama örneği bulabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="30537-204">See more Table storage samples in [Getting Started with Azure Table Storage in .NET](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/)</span></span>
* <span data-ttu-id="30537-205">Kullanılabilir API'ler ile ilgili tam Ayrıntılar için Hello tablo hizmeti başvuru belgelerini görüntüleyin:</span><span class="sxs-lookup"><span data-stu-id="30537-205">View hello Table service reference documentation for complete details about available APIs:</span></span>
* [<span data-ttu-id="30537-206">.NET başvurusu için Depolama İstemci Kitaplığı</span><span class="sxs-lookup"><span data-stu-id="30537-206">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
* [<span data-ttu-id="30537-207">REST API başvurusu</span><span class="sxs-lookup"><span data-stu-id="30537-207">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="30537-208">Nasıl toosimplify hello kodu yazdığınız öğrenin hello kullanarak Azure Storage ile toowork [Azure Web işleri SDK'si](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="30537-208">Learn how toosimplify hello code you write toowork with Azure Storage by using hello [Azure WebJobs SDK](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)</span></span>
* <span data-ttu-id="30537-209">Veri depolama için ek seçenekleri hakkında daha fazla özellik kılavuzları toolearn görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="30537-209">View more feature guides toolearn about additional options for storing data in Azure.</span></span>
* <span data-ttu-id="30537-210">[.NET kullanarak Azure Blob storage'ı kullanmaya başlama](../storage/blobs/storage-dotnet-how-to-use-blobs.md) toostore yapılandırılmamış veriler.</span><span class="sxs-lookup"><span data-stu-id="30537-210">[Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) toostore unstructured data.</span></span>
* <span data-ttu-id="30537-211">[.NET (C#) kullanarak tooSQL veritabanına bağlanma](../sql-database/sql-database-develop-dotnet-simple.md) toostore ilişkisel veri.</span><span class="sxs-lookup"><span data-stu-id="30537-211">[Connect tooSQL Database by using .NET (C#)](../sql-database/sql-database-develop-dotnet-simple.md) toostore relational data.</span></span>

[Download and install hello Azure SDK for .NET]: /develop/net/
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
