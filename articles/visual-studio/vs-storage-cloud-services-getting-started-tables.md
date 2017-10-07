---
title: "aaaGet, bağlı hizmetler (bulut Hizmetleri) tablo depolama ve Visual Studio ile çalışmaya | Microsoft Docs"
description: "Visual Studio kullanarak tooa depolama hesabı bağlanma Hizmetleri bağlandıktan sonra bir bulut hizmeti projesini Visual Studio'da Azure Table storage kullanarak tooget nasıl başlatılacağını"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: a3a11ed8-ba7f-4193-912b-e555f5b72184
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 36da6ed4a12a3595e7234482e3040ecee8c33b8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-table-storage-and-visual-studio-connected-services-cloud-services-projects"></a><span data-ttu-id="4c54c-103">Azure tablo depolaması ve Visual Studio ile çalışmaya başlama (Projeler bulut Hizmetleri) Hizmetleri bağlı</span><span class="sxs-lookup"><span data-stu-id="4c54c-103">Getting started with Azure table storage and Visual Studio connected services (cloud services projects)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="4c54c-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="4c54c-104">Overview</span></span>
<span data-ttu-id="4c54c-105">Oluşturulan veya hello Visual Studio kullanarak bir Azure depolama hesabı bulut Hizmetleri projesinde başvurulan sonra Visual Studio'da Azure tablo depolaması kullanarak tooget nasıl başlatılacağını bu makalede **bağlı Hizmetleri Ekle** iletişim .</span><span class="sxs-lookup"><span data-stu-id="4c54c-105">This article describes how tooget started using Azure table storage in Visual Studio after you have created or referenced an Azure storage account in a cloud services project by using hello Visual Studio **Add Connected Services** dialog.</span></span> <span data-ttu-id="4c54c-106">Merhaba **bağlı Hizmetleri Ekle** işlemi hello uygun NuGet paketleri tooaccess Azure depolama projenizde yükler ve proje yapılandırma dosyalarını tooyour hello depolama hesabı için hello bağlantı dizesi ekler.</span><span class="sxs-lookup"><span data-stu-id="4c54c-106">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

<span data-ttu-id="4c54c-107">Hello Azure Table depolama hizmeti toostore büyük miktarlarda yapılandırılmış veri sağlar.</span><span class="sxs-lookup"><span data-stu-id="4c54c-107">hello Azure Table storage service enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="4c54c-108">Merhaba, iç ve dış hello Azure bulut gelen kimliği doğrulanmış çağrıları kabul eden bir NoSQL veri deposu hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="4c54c-108">hello service is a NoSQL datastore that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="4c54c-109">Azure tabloları, yapılandırılmış ve ilişkisel olmayan verilerin depolanması için idealdir.</span><span class="sxs-lookup"><span data-stu-id="4c54c-109">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="4c54c-110">başlatılan tooget önce toocreate bir tablo depolama hesabınızdaki gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c54c-110">tooget started, you first need toocreate a table in your storage account.</span></span> <span data-ttu-id="4c54c-111">Nasıl toocreate Azure tablo kodda ve ayrıca nasıl tooperform temel tablo ekleme, değiştirme, okuma ve okuma gibi varlık işlemlerini varlıklar tablo ve göstereceğiz.</span><span class="sxs-lookup"><span data-stu-id="4c54c-111">We'll show you how toocreate an Azure table in code, and also how tooperform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="4c54c-112">Merhaba örnekleri C'de yazılmış\# kod ve hello kullan [.NET için Microsoft Azure Storage istemci Kitaplığı](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="4c54c-112">hello samples are written in C\# code and use hello [Microsoft Azure Storage client library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="4c54c-113">**Not:** hello tooAzure depolama giden çağrıları gerçekleştirdiğinizde API'leri bazıları zaman uyumsuzdur.</span><span class="sxs-lookup"><span data-stu-id="4c54c-113">**NOTE:** Some of hello APIs that perform calls out tooAzure storage are asynchronous.</span></span> <span data-ttu-id="4c54c-114">Bkz: [uyumsuz ve bekleme ile zaman uyumsuz programlama](http://msdn.microsoft.com/library/hh191443.aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="4c54c-114">See [Asynchronous programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="4c54c-115">Aşağıdaki Hello kodu zaman uyumsuz programlama yöntemleri kullanıldığı varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="4c54c-115">hello code below assumes async programming methods are being used.</span></span>

* <span data-ttu-id="4c54c-116">Bkz: [.NET kullanarak Azure Table storage'ı kullanmaya başlama](../storage/storage-dotnet-how-to-use-tables.md) program aracılığıyla tablolarını düzenleme hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="4c54c-116">See [Get started with Azure Table storage using .NET](../storage/storage-dotnet-how-to-use-tables.md) for more information on programmatically manipulating tables.</span></span>
* <span data-ttu-id="4c54c-117">Bkz: [Storage belgeleri](https://azure.microsoft.com/documentation/services/storage/) Azure Storage hakkında genel bilgiler.</span><span class="sxs-lookup"><span data-stu-id="4c54c-117">See [Storage documentation](https://azure.microsoft.com/documentation/services/storage/) for general information about Azure Storage.</span></span>
* <span data-ttu-id="4c54c-118">Bkz: [bulut Hizmetleri belgelerinde](https://azure.microsoft.com/documentation/services/cloud-services/) Azure bulut hizmetleri hakkında genel bilgi için.</span><span class="sxs-lookup"><span data-stu-id="4c54c-118">See [Cloud Services documentation](https://azure.microsoft.com/documentation/services/cloud-services/) for general information about Azure cloud services.</span></span>
* <span data-ttu-id="4c54c-119">Bkz: [ASP.NET](http://www.asp.net) ASP.NET uygulamalarını programlama hakkında daha fazla bilgi.</span><span class="sxs-lookup"><span data-stu-id="4c54c-119">See [ASP.NET](http://www.asp.net) for more information about programming ASP.NET applications.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="4c54c-120">Kod erişim tablolarında</span><span class="sxs-lookup"><span data-stu-id="4c54c-120">Access tables in code</span></span>
<span data-ttu-id="4c54c-121">Bulut hizmeti projeleri tooaccess tablolarda, aşağıdaki Azure tablo depolama erişim öğeleri tooany C# kaynak dosyaları tooinclude hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="4c54c-121">tooaccess tables in cloud service projects, you need tooinclude hello following items tooany C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="4c54c-122">Merhaba ad alanı bildirimleri hello dosyanın üst kısmındaki hello C# bu eklediğinizden emin olun **kullanarak** deyimleri.</span><span class="sxs-lookup"><span data-stu-id="4c54c-122">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="4c54c-123">Alma bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="4c54c-123">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="4c54c-124">Kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgilerini hello Azure hizmet yapılandırmasından aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="4c54c-124">Use hello following code tooget hello storage connection string and storage account information from hello Azure service configuration.</span></span>
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage account name>
         _AzureStorageConnectionString"));
   > [!NOTE]
   > <span data-ttu-id="4c54c-125">Tüm kod hello kod önünde yukarıda hello örnekleri aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="4c54c-125">Use all of hello above code in front of hello code in hello following samples.</span></span>
   > 
   > 
3. <span data-ttu-id="4c54c-126">Alma bir **CloudTableClient** tooreference hello tablo nesneleri depolama hesabınızdaki.</span><span class="sxs-lookup"><span data-stu-id="4c54c-126">Get a **CloudTableClient** object tooreference hello table objects in your storage account.</span></span>
   
         // Create hello table client.
         CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="4c54c-127">Alma bir **CloudTable** başvuru nesnesi tooreference belirli bir tablo ve varlıklar.</span><span class="sxs-lookup"><span data-stu-id="4c54c-127">Get a **CloudTable** reference object tooreference a specific table and entities.</span></span>
   
        // Get a reference tooa table named "peopleTable".
        CloudTable peopleTable = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="4c54c-128">Kod içinde bir tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="4c54c-128">Create a table in code</span></span>
<span data-ttu-id="4c54c-129">toocreate hello Azure tablo eklemeniz yeterlidir bir çağrı çok**CreateIfNotExistsAsync** elde sonra toohello bir **CloudTable** nesne hello "Access tabloları kod" bölümünde açıklandığı gibi.</span><span class="sxs-lookup"><span data-stu-id="4c54c-129">toocreate hello Azure table, just add a call too**CreateIfNotExistsAsync** toohello after you get a **CloudTable** object as described in hello "Access tables in code" section.</span></span>

    // Create hello CloudTable if it does not exist.
    await peopleTable.CreateIfNotExistsAsync();

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="4c54c-130">Bir varlık tooa tablo ekleme</span><span class="sxs-lookup"><span data-stu-id="4c54c-130">Add an entity tooa table</span></span>
<span data-ttu-id="4c54c-131">bir varlık tooa tablosu tooadd varlığınız hello özelliklerini tanımlayan bir sınıf oluşturun.</span><span class="sxs-lookup"><span data-stu-id="4c54c-131">tooadd an entity tooa table, create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="4c54c-132">Merhaba aşağıdaki kodu olarak adlandırılan bir varlık sınıfı tanımlar **CustomerEntity** kullanır hello satır anahtarı olarak müşterinin adını ve hello Soyadı hello bölüm anahtarı olarak hello.</span><span class="sxs-lookup"><span data-stu-id="4c54c-132">hello following code defines an entity class called **CustomerEntity** that uses hello customer's first name as hello row key and hello last name as hello partition key.</span></span>

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

<span data-ttu-id="4c54c-133">Varlıkları içeren tablo işlemleri yapılır hello kullanarak **CloudTable** "Access tabloları kodda." bölümünde daha önce oluşturduğunuz nesnesi</span><span class="sxs-lookup"><span data-stu-id="4c54c-133">Table operations involving entities are done using hello **CloudTable** object that you created earlier in "Access tables in code."</span></span> <span data-ttu-id="4c54c-134">Merhaba **TableOperation** nesnesi bitti hello işlemi toobe temsil eder.</span><span class="sxs-lookup"><span data-stu-id="4c54c-134">hello **TableOperation** object represents hello operation toobe done.</span></span> <span data-ttu-id="4c54c-135">Kod örnekteki nasıl aşağıdaki hello toocreate bir **CloudTable** nesne ve **CustomerEntity** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="4c54c-135">hello following code example shows how toocreate a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="4c54c-136">tooprepare hello işlemi, bir **TableOperation** tooinsert hello müşteri varlık hello tabloya oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="4c54c-136">tooprepare hello operation, a **TableOperation** is created tooinsert hello customer entity into hello table.</span></span> <span data-ttu-id="4c54c-137">Son olarak, hello işlemi çağrılarak çalıştırılır **CloudTable.ExecuteAsync**.</span><span class="sxs-lookup"><span data-stu-id="4c54c-137">Finally, hello operation is executed by calling **CloudTable.ExecuteAsync**.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create hello TableOperation that inserts hello customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute hello insert operation.
    await peopleTable.ExecuteAsync(insertOperation);


## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="4c54c-138">Toplu işlem varlık yerleştirme</span><span class="sxs-lookup"><span data-stu-id="4c54c-138">Insert a batch of entities</span></span>
<span data-ttu-id="4c54c-139">Birden çok varlık, bir tek bir yazma işleminde bir tabloya ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c54c-139">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="4c54c-140">Merhaba aşağıdaki kod örneği iki varlık nesnesi ("Jeff Smith" ve "Ben Smith") oluşturur, tooa ekler **TableBatchOperation** nesne ekleme yöntemi hello ve çağırarak bu başlatır işlemi hello kullanarak  **CloudTable.ExecuteBatchAsync**.</span><span class="sxs-lookup"><span data-stu-id="4c54c-140">hello following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them tooa **TableBatchOperation** object using hello Insert method, and then starts hello operation by calling **CloudTable.ExecuteBatchAsync**.</span></span>

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
    await peopleTable.ExecuteBatchAsync(batchOperation);

## <a name="get-all-of-hello-entities-in-a-partition"></a><span data-ttu-id="4c54c-141">Bir bölüm hello varlıkların alın</span><span class="sxs-lookup"><span data-stu-id="4c54c-141">Get all of hello entities in a partition</span></span>
<span data-ttu-id="4c54c-142">tooquery tüm hello varlıkları bir bölüme kullanmak için bir tablo bir **TableQuery** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="4c54c-142">tooquery a table for all of hello entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="4c54c-143">Merhaba aşağıdaki kod örneğinde 'Smith' hello bölüm anahtarı olduğu varlıklar için bir filtre belirtir.</span><span class="sxs-lookup"><span data-stu-id="4c54c-143">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="4c54c-144">Bu örnekte her varlığın hello sorgu sonuçları toohello konsolunda hello alanlarını yazdırır.</span><span class="sxs-lookup"><span data-stu-id="4c54c-144">This example prints hello fields of each entity in hello query results toohello console.</span></span>

    // Construct hello query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

    // Print hello fields for each customer.
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


## <a name="get-a-single-entity"></a><span data-ttu-id="4c54c-145">Tek bir varlık alma</span><span class="sxs-lookup"><span data-stu-id="4c54c-145">Get a single entity</span></span>
<span data-ttu-id="4c54c-146">Bir sorgu tooget tek, belirli bir varlığı yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c54c-146">You can write a query tooget a single, specific entity.</span></span> <span data-ttu-id="4c54c-147">Merhaba aşağıdaki kod kullanan bir **TableOperation** toospecify 'Ben Smith' adlı bir müşteri nesnesi.</span><span class="sxs-lookup"><span data-stu-id="4c54c-147">hello following code uses a **TableOperation** object toospecify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="4c54c-148">Bu yöntem bir koleksiyon yerine yalnızca bir varlık döndürür ve hello döndürülen değer **TableResult.Result** olan bir **CustomerEntity** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="4c54c-148">This method returns just one entity, rather than a collection, and hello returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="4c54c-149">Bir sorguda hem Bölüm hem de satır anahtarını belirterek olduğu hello en hızlı yolu tooretrieve hello tek bir varlıktan **tablo** hizmet.</span><span class="sxs-lookup"><span data-stu-id="4c54c-149">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print hello phone number of hello result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("hello phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="4c54c-150">Bir varlığı silme</span><span class="sxs-lookup"><span data-stu-id="4c54c-150">Delete an entity</span></span>
<span data-ttu-id="4c54c-151">Bunu bulduktan sonra bir varlık silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4c54c-151">You can delete an entity after you find it.</span></span> <span data-ttu-id="4c54c-152">Merhaba aşağıdaki kod görünür "Ben Smith" adlı bir müşteri varlığı için ve bulursa, onu siler.</span><span class="sxs-lookup"><span data-stu-id="4c54c-152">hello following code looks for a customer entity named "Ben Smith", and if it finds it, it deletes it.</span></span>

    // Create a retrieve operation that expects a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello operation.
    TableResult retrievedResult = peopleTable.Execute(retrieveOperation);

    // Assign hello result tooa CustomerEntity object.
    CustomerEntity deleteEntity = (CustomerEntity)retrievedResult.Result;

    // Create hello Delete TableOperation and then execute it.
    if (deleteEntity != null)
    {
       TableOperation deleteOperation = TableOperation.Delete(deleteEntity);

       // Execute hello operation.
       await peopleTable.ExecuteAsync(deleteOperation);

       Console.WriteLine("Entity deleted.");
    }

    else
       Console.WriteLine("Couldn't delete hello entity.");

## <a name="next-steps"></a><span data-ttu-id="4c54c-153">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4c54c-153">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

