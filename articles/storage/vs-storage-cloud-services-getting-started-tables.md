---
title: "Tablo depolama ve Visual Studio ile çalışmaya başlama bağlı Hizmetleri (bulut Hizmetleri) | Microsoft Docs"
description: "Visual Studio kullanarak bir depolama hesabına bağlanma Hizmetleri bağlandıktan sonra bir bulut hizmeti projesini Visual Studio'da Azure tablo depolaması ile çalışmaya başlamak nasıl"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: a3a11ed8-ba7f-4193-912b-e555f5b72184
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 3208ddb1a1246a5ff25d272bfc7d8ba842348a36
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-azure-table-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="d2f59-103">Azure tablo depolaması ve Visual Studio ile çalışmaya başlama (Projeler bulut Hizmetleri) Hizmetleri bağlı</span><span class="sxs-lookup"><span data-stu-id="d2f59-103">Getting started with Azure table storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="d2f59-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="d2f59-104">Overview</span></span>
<span data-ttu-id="d2f59-105">Bu makale, oluşturduğunuz veya Visual Studio kullanarak bir Azure depolama hesabı bulut Hizmetleri projesinde başvurulan sonra Visual Studio'da Azure tablo depolaması ile çalışmaya başlamak açıklamaktadır **bağlı Hizmetleri Ekle** iletişim.</span><span class="sxs-lookup"><span data-stu-id="d2f59-105">This article describes how to get started using Azure table storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using the Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="d2f59-106">**Bağlı Hizmetleri Ekle** işlemi Azure depolama projenize erişmek için uygun NuGet paketlerini yükler ve proje yapılandırma dosyalarınızı depolama hesabı için bağlantı dizesi ekler.</span><span class="sxs-lookup"><span data-stu-id="d2f59-106">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span></span>

<span data-ttu-id="d2f59-107">Azure Table depolama birimi hizmeti, büyük miktarlarda yapılandırılmış verileri depolamak sağlar.</span><span class="sxs-lookup"><span data-stu-id="d2f59-107">The Azure Table storage service enables you to store large amounts of structured data.</span></span> <span data-ttu-id="d2f59-108">Kimliği doğrulanmış çağrılarından içinden ve dışından Azure bulut kabul eden bir NoSQL veri deposu hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="d2f59-108">The service is a NoSQL datastore that accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="d2f59-109">Azure tabloları, yapılandırılmış ve ilişkisel olmayan verilerin depolanması için idealdir.</span><span class="sxs-lookup"><span data-stu-id="d2f59-109">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="d2f59-110">Başlamak için önce bir tablo depolama hesabınızdaki oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="d2f59-110">To get started, you first need to create a table in your storage account.</span></span> <span data-ttu-id="d2f59-111">Kod içinde bir Azure tablosu oluşturma ve temel tablo ve ekleme, değiştirme, okuma ve tablo varlıkları okuma gibi varlık işlemlerini gerçekleştirmek nasıl göstereceğiz.</span><span class="sxs-lookup"><span data-stu-id="d2f59-111">We'll show you how to create an Azure table in code, and also how to perform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="d2f59-112">Örnekler C yazılır\# kod ve kullanma [.NET için Microsoft Azure Storage istemci Kitaplığı](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="d2f59-112">The samples are written in C\# code and use the [Microsoft Azure Storage client library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="d2f59-113">**Not:** bazı Azure depolamaya giden çağrıları gerçekleştirdiğinizde API'leri zaman uyumsuzdur.</span><span class="sxs-lookup"><span data-stu-id="d2f59-113">**NOTE:** Some of the APIs that perform calls out to Azure storage are asynchronous.</span></span> <span data-ttu-id="d2f59-114">Bkz: [uyumsuz ve bekleme ile zaman uyumsuz programlama](http://msdn.microsoft.com/library/hh191443.aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="d2f59-114">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="d2f59-115">Aşağıdaki kodu, zaman uyumsuz programlama yöntemleri kullanıldığı varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d2f59-115">The code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="d2f59-116">Bkz: [.NET kullanarak Azure Table storage'ı kullanmaya başlama](storage-dotnet-how-to-use-tables.md) program aracılığıyla tablolarını düzenleme hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="d2f59-116">See [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md) for more information on programmatically manipulating tables.</span></span>
* <span data-ttu-id="d2f59-117">Bkz: [Storage belgeleri](https://azure.microsoft.com/documentation/services/storage/) Azure Storage hakkında genel bilgiler.</span><span class="sxs-lookup"><span data-stu-id="d2f59-117">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="d2f59-118">Bkz: [bulut Hizmetleri belgelerinde](https://azure.microsoft.com/documentation/services/cloud-services/) Azure bulut hizmetleri hakkında genel bilgi için.</span><span class="sxs-lookup"><span data-stu-id="d2f59-118">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="d2f59-119">Bkz: [ASP.NET](http://www.asp.net) ASP.NET uygulamalarını programlama hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="d2f59-119">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="d2f59-120">Kod erişim tablolarında</span><span class="sxs-lookup"><span data-stu-id="d2f59-120">Access tables in code</span></span>
<span data-ttu-id="d2f59-121">Bulut hizmeti projeleri tablolarda erişmek için Azure tablo depolaması erişen tüm C# kaynak dosyaları için aşağıdaki öğeleri eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d2f59-121">To access tables in cloud service projects, you need to include the following items to any C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="d2f59-122">Ad alanı bildirimlerini dosyanın üst kısmındaki C# bu eklediğinizden emin olun **kullanarak** deyimleri.</span><span class="sxs-lookup"><span data-stu-id="d2f59-122">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="d2f59-123">Alma bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="d2f59-123">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="d2f59-124">Azure hizmet yapılandırmasından depolama bağlantı dizesi ve depolama hesabı bilgilerini almak için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="d2f59-124">Use the following code to get the storage connection string and storage account information from the Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage account name>
         _AzureStorageConnectionString"));
   > [!NOTE]
   > <span data-ttu-id="d2f59-125">Tüm kod önünde Yukarıdaki kod, aşağıdaki örneklerde kullanın.</span><span class="sxs-lookup"><span data-stu-id="d2f59-125">Use all of the above code in front of the code in the following samples.</span></span>
   > 
   > 
3. <span data-ttu-id="d2f59-126">Alma bir **CloudTableClient** depolama hesabınızdaki tablo nesneleri başvurmak için.</span><span class="sxs-lookup"><span data-stu-id="d2f59-126">Get a **CloudTableClient** object to reference the table objects in your storage account.</span></span>
   
         // Create the table client.
         CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="d2f59-127">Alma bir **CloudTable** belirli bir tablo ve varlıkları başvurmak için başvuru nesnesi.</span><span class="sxs-lookup"><span data-stu-id="d2f59-127">Get a **CloudTable** reference object to reference a specific table and entities.</span></span>
   
        // Get a reference to a table named "peopleTable".
        CloudTable peopleTable = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="d2f59-128">Kod içinde bir tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="d2f59-128">Create a table in code</span></span>
<span data-ttu-id="d2f59-129">Azure tablo oluşturmak için yalnızca bir çağrı ekleyin **CreateIfNotExistsAsync** için size sonra bir **CloudTable** nesne "kod tablolarda erişim" bölümünde açıklandığı gibi.</span><span class="sxs-lookup"><span data-stu-id="d2f59-129">To create the Azure table, just add a call to **CreateIfNotExistsAsync** to the after you get a **CloudTable** object as described in the "Access tables in code" section.</span></span>

    // Create the CloudTable if it does not exist.
    await peopleTable.CreateIfNotExistsAsync();

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="d2f59-130">Tabloya bir varlık ekleme</span><span class="sxs-lookup"><span data-stu-id="d2f59-130">Add an entity to a table</span></span>
<span data-ttu-id="d2f59-131">Tabloya bir varlık eklemek için varlığınızın özelliklerini tanımlayan bir sınıf oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d2f59-131">To add an entity to a table, create a class that defines the properties of your entity.</span></span> <span data-ttu-id="d2f59-132">Aşağıdaki kod olarak adlandırılan bir varlık sınıfı tanımlar **CustomerEntity** , müşterinin adını satır anahtarını ve Soyadı bölüm anahtarı olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="d2f59-132">The following code defines an entity class called **CustomerEntity** that uses the customer's first name as the row key and the last name as the partition key.</span></span>

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

<span data-ttu-id="d2f59-133">Varlıkları içeren tablo işlemleri yapılır kullanarak **CloudTable** "Access tabloları kodda." bölümünde daha önce oluşturduğunuz nesnesi</span><span class="sxs-lookup"><span data-stu-id="d2f59-133">Table operations involving entities are done using the **CloudTable** object that you created earlier in "Access tables in code."</span></span> <span data-ttu-id="d2f59-134">**TableOperation** nesnesi yapılması işlemi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="d2f59-134">The **TableOperation** object represents the operation to be done.</span></span> <span data-ttu-id="d2f59-135">Aşağıdaki kod örneğinde nasıl oluşturulacağını gösterir bir **CloudTable** nesne ve **CustomerEntity** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="d2f59-135">The following code example shows how to create a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="d2f59-136">İşlemi hazırlamak için bir **TableOperation** müşteri varlığını tabloya yerleştirmek için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="d2f59-136">To prepare the operation, a **TableOperation** is created to insert the customer entity into the table.</span></span> <span data-ttu-id="d2f59-137">Son olarak, işlem çağrılarak çalıştırılır **CloudTable.ExecuteAsync**.</span><span class="sxs-lookup"><span data-stu-id="d2f59-137">Finally, the operation is executed by calling **CloudTable.ExecuteAsync**.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create the TableOperation that inserts the customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute the insert operation.
    await peopleTable.ExecuteAsync(insertOperation);


## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="d2f59-138">Toplu işlem varlık yerleştirme</span><span class="sxs-lookup"><span data-stu-id="d2f59-138">Insert a batch of entities</span></span>
<span data-ttu-id="d2f59-139">Birden çok varlık, bir tek bir yazma işleminde bir tabloya ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d2f59-139">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="d2f59-140">Aşağıdaki kod örneği iki varlık nesnesi ("Jeff Smith" ve "Ben Smith") oluşturur, eklenmektedir bir **TableBatchOperation** Ekle yöntemi kullanılarak nesne ve ardından çağırarak işlemi başlatır **CloudTable.ExecuteBatchAsync**.</span><span class="sxs-lookup"><span data-stu-id="d2f59-140">The following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them to a **TableBatchOperation** object using the Insert method, and then starts the operation by calling **CloudTable.ExecuteBatchAsync**.</span></span>

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
    await peopleTable.ExecuteBatchAsync(batchOperation);

## <a name="get-all-of-the-entities-in-a-partition"></a><span data-ttu-id="d2f59-141">Tüm varlıkları bir bölüme alma</span><span class="sxs-lookup"><span data-stu-id="d2f59-141">Get all of the entities in a partition</span></span>
<span data-ttu-id="d2f59-142">Tüm varlıkları bir bölüme için bir tabloyu sorgulamak için kullanın bir **TableQuery** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="d2f59-142">To query a table for all of the entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="d2f59-143">Aşağıdaki kod örneği, ‘Smith’in bölüm anahtarı olduğu varlıklar için bir filtre belirtir.</span><span class="sxs-lookup"><span data-stu-id="d2f59-143">The following code example specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="d2f59-144">Bu örnek sorgu sonuçlarındaki her varlığın alanlarını konsola yazdırır.</span><span class="sxs-lookup"><span data-stu-id="d2f59-144">This example prints the fields of each entity in the query results to the console.</span></span>

    // Construct the query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

    // Print the fields for each customer.
    TableContinuationToken token = null;
    do
    {
        TableQuerySegment<CustomerEntity> resultSegment = await peopleTable.ExecuteQuerySegmentedAsync(query, token);
        token = resultSegment.ContinuationToken;

        foreach (CustomerEntity entity in resultSegment.Results)
        {
            Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
            entity.Email, entity.PhoneNumber);
        }
    } while (token != null);

    return View();


## <a name="get-a-single-entity"></a><span data-ttu-id="d2f59-145">Tek bir varlık alma</span><span class="sxs-lookup"><span data-stu-id="d2f59-145">Get a single entity</span></span>
<span data-ttu-id="d2f59-146">Tek, belirli bir varlığı almak üzere bir sorgu yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d2f59-146">You can write a query to get a single, specific entity.</span></span> <span data-ttu-id="d2f59-147">Aşağıdaki kod bir **TableOperation** 'Ben Smith' adlı bir müşteri belirtmek için nesne.</span><span class="sxs-lookup"><span data-stu-id="d2f59-147">The following code uses a **TableOperation** object to specify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="d2f59-148">Bu yöntem yalnızca tek bir varlık yerine bir koleksiyonu ile döndürülen değeri döndürür **TableResult.Result** olan bir **CustomerEntity** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="d2f59-148">This method returns just one entity, rather than a collection, and the returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="d2f59-149">Tek bir varlık almanın en hızlı yolu olan bir sorguda hem Bölüm hem de satır anahtarını belirterek **tablo** hizmet.</span><span class="sxs-lookup"><span data-stu-id="d2f59-149">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute the retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print the phone number of the result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("The phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="d2f59-150">Bir varlığı silme</span><span class="sxs-lookup"><span data-stu-id="d2f59-150">Delete an entity</span></span>
<span data-ttu-id="d2f59-151">Bunu bulduktan sonra bir varlık silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d2f59-151">You can delete an entity after you find it.</span></span> <span data-ttu-id="d2f59-152">"Ben Smith" adlı bir müşteri varlığı için aşağıdaki kodu arar ve bulursa, onu siler.</span><span class="sxs-lookup"><span data-stu-id="d2f59-152">The following code looks for a customer entity named "Ben Smith", and if it finds it, it deletes it.</span></span>

    // Create a retrieve operation that expects a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute the operation.
    TableResult retrievedResult = peopleTable.Execute(retrieveOperation);

    // Assign the result to a CustomerEntity object.
    CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

    // Create the Delete TableOperation and then execute it.
    if (deleteEntity != null)
    {
       TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

       // Execute the operation.
       await peopleTable.ExecuteAsync(deleteOperation);

       Console.WriteLine("Entity deleted.");
    }

    else
       Console.WriteLine("Couldn't delete the entity.");

## <a name="next-steps"></a><span data-ttu-id="d2f59-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d2f59-153">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

