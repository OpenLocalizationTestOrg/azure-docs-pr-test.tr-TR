---
title: "Tablo depolama ve Visual Studio ile çalışmaya nasıl başlayacağınız bağlı Hizmetleri (ASP.NET Core) | Microsoft Docs"
description: "Visual Studio'da ASP.NET Core projesinde Azure Table storage ile Visual Studio kullanarak bir depolama hesabı bağlandıktan sonra nasıl başlayacağınızı Hizmetleri bağlı"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: c3c451d1-71ff-4222-a348-c41c98a02b85
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 8d05fe3ed9a5c66f186a930d4107162c1f322c05
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-get-started-with-azure-table-storage-and-visual-studio-connected-services"></a><span data-ttu-id="fe01a-103">Azure tablo depolaması ve Visual Studio ile çalışmaya nasıl başlayacağınız Hizmetleri bağlı</span><span class="sxs-lookup"><span data-stu-id="fe01a-103">How to get started with Azure Table storage and Visual Studio connected services</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="fe01a-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="fe01a-104">Overview</span></span>
<span data-ttu-id="fe01a-105">Bu makalede nasıl oluşturduğunuz veya Visual Studio kullanarak bir ASP.NET Core projesini bir Azure depolama hesabında başvurulan sonra Visual Studio'da Azure tablo depolaması ile çalışmaya başlamak **bağlı Hizmetleri Ekle** iletişim.</span><span class="sxs-lookup"><span data-stu-id="fe01a-105">This article describes how get started using Azure Table storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using the Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="fe01a-106">Azure Table depolama birimi hizmeti, büyük miktarlarda yapılandırılmış verileri depolamak sağlar.</span><span class="sxs-lookup"><span data-stu-id="fe01a-106">The Azure Table storage service enables you to store large amounts of structured data.</span></span> <span data-ttu-id="fe01a-107">Hizmet, kimliği doğrulanmış çağrılarından içinden ve dışından Azure bulut kabul eden bir NoSQL veri deposudur.</span><span class="sxs-lookup"><span data-stu-id="fe01a-107">The service is a NoSQL data store that accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="fe01a-108">Azure tabloları, yapılandırılmış ve ilişkisel olmayan verilerin depolanması için idealdir.</span><span class="sxs-lookup"><span data-stu-id="fe01a-108">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="fe01a-109">**Bağlı Hizmetleri Ekle** işlemi Azure depolama projenize erişmek için uygun NuGet paketlerini yükler ve proje yapılandırma dosyalarınızı depolama hesabı için bağlantı dizesi ekler.</span><span class="sxs-lookup"><span data-stu-id="fe01a-109">The **Add Connected Services** operation installs the appropriate NuGet packages to access Azure storage in your project and adds the connection string for the storage account to your project configuration files.</span></span>

<span data-ttu-id="fe01a-110">Azure Table storage kullanma hakkında daha fazla genel bilgi için bkz: [.NET kullanarak Azure Table storage'ı kullanmaya başlama](../storage/storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="fe01a-110">For more general information about using Azure Table storage, see [Get started with Azure Table storage using .NET](../storage/storage-dotnet-how-to-use-tables.md).</span></span>

<span data-ttu-id="fe01a-111">Başlamak için önce bir tablo depolama hesabınızdaki oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="fe01a-111">To get started, you first need to create a table in your storage account.</span></span> <span data-ttu-id="fe01a-112">Kodda bir Azure tablo oluşturulacağını göstereceğiz.</span><span class="sxs-lookup"><span data-stu-id="fe01a-112">We'll show you how to create an Azure table in code.</span></span> <span data-ttu-id="fe01a-113">Ayrıca, temel tablo ve ekleme, değiştirme, okuma ve tablo varlıkları okuma gibi varlık işlemlerini gerçekleştirmek nasıl göstereceğiz.</span><span class="sxs-lookup"><span data-stu-id="fe01a-113">We'll also show you how to perform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="fe01a-114">Örnekler C yazılır\# kod ve .NET için Azure Storage istemci kitaplığı kullanın.</span><span class="sxs-lookup"><span data-stu-id="fe01a-114">The samples are written in C\# code and use the Azure Storage Client Library for .NET.</span></span>

<span data-ttu-id="fe01a-115">**Not** -ASP.NET Core Azure depolamaya giden çağrıları gerçekleştirmek API'leri bazıları zaman uyumsuzdur.</span><span class="sxs-lookup"><span data-stu-id="fe01a-115">**NOTE** - Some of the APIs that perform calls out to Azure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="fe01a-116">Bkz: [uyumsuz ve bekleme ile zaman uyumsuz programlama](http://msdn.microsoft.com/library/hh191443.aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="fe01a-116">See [Asynchronous Programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="fe01a-117">Aşağıdaki kodu, zaman uyumsuz programlama yöntemleri kullanıldığı varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="fe01a-117">The code below assumes Async programming methods are being used.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="fe01a-118">Kod erişim tablolarında</span><span class="sxs-lookup"><span data-stu-id="fe01a-118">Access tables in code</span></span>
<span data-ttu-id="fe01a-119">ASP.NET Core projeleri tablolarda erişmek için Azure tablo depolaması erişen tüm C# kaynak dosyaları için aşağıdaki öğeleri eklemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fe01a-119">To access tables in ASP.NET Core projects, you need to include the following items to any C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="fe01a-120">Ad alanı bildirimlerini dosyanın üst kısmındaki C# bu eklediğinizden emin olun **kullanarak** deyimleri.</span><span class="sxs-lookup"><span data-stu-id="fe01a-120">Make sure the namespace declarations at the top of the C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="fe01a-121">Alma bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="fe01a-121">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="fe01a-122">Almak için aşağıdaki kodu kullanın depolama bağlantı dizesini ve Azure hizmet yapılandırma depolama hesabı bilgileri.</span><span class="sxs-lookup"><span data-stu-id="fe01a-122">Use the following code to get the your storage connection string and storage account information from the Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
            CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
   
    <span data-ttu-id="fe01a-123">**Not** -tüm kod önünde Yukarıdaki kod aşağıdaki örneklerde kullanın.</span><span class="sxs-lookup"><span data-stu-id="fe01a-123">**NOTE** - Use all of the above code in front of the code in the following samples.</span></span>
3. <span data-ttu-id="fe01a-124">Alma bir **CloudTableClient** depolama hesabınızdaki tablo nesneleri başvurmak için.</span><span class="sxs-lookup"><span data-stu-id="fe01a-124">Get a **CloudTableClient** object to reference the table objects in your storage account.</span></span>  
   
        // Create the table client.
        CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="fe01a-125">Alma bir **CloudTable** belirli bir tablo ve varlıkları başvurmak için başvuru nesnesi.</span><span class="sxs-lookup"><span data-stu-id="fe01a-125">Get a **CloudTable** reference object to reference a specific table and entities.</span></span>
   
        // Get a reference to a table named "peopleTable"
        CloudTable table = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="fe01a-126">Kod içinde bir tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="fe01a-126">Create a table in code</span></span>
<span data-ttu-id="fe01a-127">Azure tablo oluşturmak için yalnızca bir çağrı ekleyin **CreateIfNotExistsAsync()**.</span><span class="sxs-lookup"><span data-stu-id="fe01a-127">To create the Azure table, just add a call to **CreateIfNotExistsAsync()**.</span></span>

    // Create the CloudTable if it does not exist
    await table.CreateIfNotExistsAsync();

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="fe01a-128">Tabloya bir varlık ekleme</span><span class="sxs-lookup"><span data-stu-id="fe01a-128">Add an entity to a table</span></span>
<span data-ttu-id="fe01a-129">Bir tabloya bir varlık eklemek için varlığınızın özelliklerini tanımlayan bir sınıf oluşturun.</span><span class="sxs-lookup"><span data-stu-id="fe01a-129">To add an entity to a table you create a class that defines the properties of your entity.</span></span> <span data-ttu-id="fe01a-130">Aşağıdaki kod olarak adlandırılan bir varlık sınıfı tanımlar **CustomerEntity** , müşterinin adını satır anahtarını ve Soyadı bölüm anahtarı olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="fe01a-130">The following code defines an entity class called **CustomerEntity** that uses the customer's first name as the row key and last name as the partition key.</span></span>

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

<span data-ttu-id="fe01a-131">Varlıkları içeren tablo işlemleri yapılır kullanarak **CloudTable** "Access tabloları kodda." içinde daha önce oluşturduğunuz nesnesi</span><span class="sxs-lookup"><span data-stu-id="fe01a-131">Table operations involving entities are done using the **CloudTable** object you created earlier in "Access tables in code."</span></span> <span data-ttu-id="fe01a-132">**TableOperation** nesnesi yapılması işlemi temsil eder.</span><span class="sxs-lookup"><span data-stu-id="fe01a-132">The **TableOperation** object represents the operation to be done.</span></span> <span data-ttu-id="fe01a-133">Aşağıdaki kod örneğinde nasıl oluşturulacağını gösterir bir **CloudTable** nesne ve **CustomerEntity** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="fe01a-133">The following code example shows how to create a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="fe01a-134">İşlemi hazırlamak için bir **TableOperation** müşteri varlığını tabloya yerleştirmek için oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="fe01a-134">To prepare the operation, a **TableOperation** is created to insert the customer entity into the table.</span></span> <span data-ttu-id="fe01a-135">Son olarak, işlem CloudTable.ExecuteAsync çağrılarak çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="fe01a-135">Finally, the operation is executed by calling CloudTable.ExecuteAsync.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create the TableOperation that inserts the customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute the insert operation.
    await peopleTable.ExecuteAsync(insertOperation);

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="fe01a-136">Toplu işlem varlık yerleştirme</span><span class="sxs-lookup"><span data-stu-id="fe01a-136">Insert a batch of entities</span></span>
<span data-ttu-id="fe01a-137">Birden çok varlık, bir tek bir yazma işleminde bir tabloya ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe01a-137">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="fe01a-138">Aşağıdaki kod örneği iki varlık nesnesi ("Jeff Smith" ve "Ben Smith") oluşturur, eklenmektedir bir **TableBatchOperation** kullanarak nesne **Ekle** yöntemi, ve ardından CloudTable.ExecuteBatchAsync çağırarak işlemi başlatır.</span><span class="sxs-lookup"><span data-stu-id="fe01a-138">The following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them to a **TableBatchOperation** object using the **Insert** method, and then starts the operation by calling CloudTable.ExecuteBatchAsync.</span></span>

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

## <a name="get-all-of-the-entities-in-a-partition"></a><span data-ttu-id="fe01a-139">Tüm varlıkları bir bölüme alma</span><span class="sxs-lookup"><span data-stu-id="fe01a-139">Get all of the entities in a partition</span></span>
<span data-ttu-id="fe01a-140">Tüm varlıkları bir bölüme için bir tabloyu sorgulamak için kullanın bir **TableQuery** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="fe01a-140">To query a table for all of the entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="fe01a-141">Aşağıdaki kod örneği, ‘Smith’in bölüm anahtarı olduğu varlıklar için bir filtre belirtir.</span><span class="sxs-lookup"><span data-stu-id="fe01a-141">The following code example specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="fe01a-142">Bu örnek sorgu sonuçlarındaki her varlığın alanlarını konsola yazdırır.</span><span class="sxs-lookup"><span data-stu-id="fe01a-142">This example prints the fields of each entity in the query results to the console.</span></span>

    // Construct the query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

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

## <a name="get-a-single-entity"></a><span data-ttu-id="fe01a-143">Tek bir varlık alma</span><span class="sxs-lookup"><span data-stu-id="fe01a-143">Get a single entity</span></span>
<span data-ttu-id="fe01a-144">Tek, belirli bir varlığı almak üzere bir sorgu yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe01a-144">You can write a query to get a single, specific entity.</span></span> <span data-ttu-id="fe01a-145">Aşağıdaki kod bir **TableOperation** 'Ben Smith' adlı bir müşteri belirtmek için nesne.</span><span class="sxs-lookup"><span data-stu-id="fe01a-145">The following code uses a **TableOperation** object to specify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="fe01a-146">Bu yöntem yalnızca tek bir varlık yerine bir koleksiyonu ile döndürülen değeri döndürür **TableResult.Result** olan bir **CustomerEntity** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="fe01a-146">This method returns just one entity, rather than a collection, and the returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="fe01a-147">Tek bir varlık almanın en hızlı yolu olan bir sorguda hem Bölüm hem de satır anahtarını belirterek **tablo** hizmet.</span><span class="sxs-lookup"><span data-stu-id="fe01a-147">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute the retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print the phone number of the result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("The phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="fe01a-148">Bir varlığı silme</span><span class="sxs-lookup"><span data-stu-id="fe01a-148">Delete an entity</span></span>
<span data-ttu-id="fe01a-149">Bunu bulduktan sonra bir varlık silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fe01a-149">You can delete an entity after you find it.</span></span> <span data-ttu-id="fe01a-150">"Ben Smith" adlı bir müşteri varlığı için aşağıdaki kodu arar ve bulursa, onu siler.</span><span class="sxs-lookup"><span data-stu-id="fe01a-150">The following code looks for a customer entity named "Ben Smith" and if it finds it, it deletes it.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="fe01a-151">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fe01a-151">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

