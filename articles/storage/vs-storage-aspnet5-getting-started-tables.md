---
title: "aaaHow tooget, bağlı hizmetler (ASP.NET Core) tablo depolama ve Visual Studio ile çalışmaya | Microsoft Docs"
description: "Visual Studio kullanarak tooa depolama hesabı bağlanma Hizmetleri bağlandıktan sonra tooget Visual Studio'da ASP.NET Core projesinde Azure Table storage ile çalışmaya nasıl"
services: storage
documentationcenter: 
author: TomArcher
manager: douge
editor: 
ms.assetid: c3c451d1-71ff-4222-a348-c41c98a02b85
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: tarcher
ms.openlocfilehash: 6a8fb6aa085d78a087fcd14adbc765a0d59e0308
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-started-with-azure-table-storage-and-visual-studio-connected-services"></a><span data-ttu-id="9885a-103">Nasıl tooget bağlı hizmetler Azure tablo depolaması ve Visual Studio ile başlatıldı</span><span class="sxs-lookup"><span data-stu-id="9885a-103">How tooget started with Azure Table storage and Visual Studio connected services</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="9885a-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="9885a-104">Overview</span></span>
<span data-ttu-id="9885a-105">Bu makalede nereden Azure Table'ı kullanmaya Visual Studio'da oluşturulan veya kullanarak bir ASP.NET Core projesini bir Azure depolama hesabında başvurulan sonra depolama hello Visual Studio **bağlı Hizmetleri Ekle** iletişim.</span><span class="sxs-lookup"><span data-stu-id="9885a-105">This article describes how get started using Azure Table storage in Visual Studio after you have created or referenced an Azure storage account in an ASP.NET Core project by using hello Visual Studio **Add Connected Services** dialog.</span></span>

<span data-ttu-id="9885a-106">Hello Azure Table depolama hizmeti toostore büyük miktarlarda yapılandırılmış veri sağlar.</span><span class="sxs-lookup"><span data-stu-id="9885a-106">hello Azure Table storage service enables you toostore large amounts of structured data.</span></span> <span data-ttu-id="9885a-107">Merhaba, iç ve dış hello Azure bulut gelen kimliği doğrulanmış çağrıları kabul eden bir NoSQL veri deposu hizmetidir.</span><span class="sxs-lookup"><span data-stu-id="9885a-107">hello service is a NoSQL data store that accepts authenticated calls from inside and outside hello Azure cloud.</span></span> <span data-ttu-id="9885a-108">Azure tabloları, yapılandırılmış ve ilişkisel olmayan verilerin depolanması için idealdir.</span><span class="sxs-lookup"><span data-stu-id="9885a-108">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="9885a-109">Merhaba **bağlı Hizmetleri Ekle** işlemi hello uygun NuGet paketleri tooaccess Azure depolama projenizde yükler ve proje yapılandırma dosyalarını tooyour hello depolama hesabı için hello bağlantı dizesi ekler.</span><span class="sxs-lookup"><span data-stu-id="9885a-109">hello **Add Connected Services** operation installs hello appropriate NuGet packages tooaccess Azure storage in your project and adds hello connection string for hello storage account tooyour project configuration files.</span></span>

<span data-ttu-id="9885a-110">Azure Table storage kullanma hakkında daha fazla genel bilgi için bkz: [.NET kullanarak Azure Table storage'ı kullanmaya başlama](storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="9885a-110">For more general information about using Azure Table storage, see [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span></span>

<span data-ttu-id="9885a-111">başlatılan tooget önce toocreate bir tablo depolama hesabınızdaki gerekir.</span><span class="sxs-lookup"><span data-stu-id="9885a-111">tooget started, you first need toocreate a table in your storage account.</span></span> <span data-ttu-id="9885a-112">Nasıl toocreate Azure tablo kodda göstereceğiz.</span><span class="sxs-lookup"><span data-stu-id="9885a-112">We'll show you how toocreate an Azure table in code.</span></span> <span data-ttu-id="9885a-113">Ayrıca, nasıl tooperform temel tablo ekleme, değiştirme, okuma ve okuma gibi varlık işlemlerini varlıklar tablo ve göstereceğiz.</span><span class="sxs-lookup"><span data-stu-id="9885a-113">We'll also show you how tooperform basic table and entity operations, such as adding, modifying, reading and reading table entities.</span></span> <span data-ttu-id="9885a-114">Merhaba örnekleri C'de yazılmış\# kod ve .NET için Azure Storage istemci kitaplığı hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="9885a-114">hello samples are written in C\# code and use hello Azure Storage Client Library for .NET.</span></span>

<span data-ttu-id="9885a-115">**Not** -hello ASP.NET Core tooAzure depolama giden çağrıları gerçekleştirdiğinizde API'leri bazıları zaman uyumsuzdur.</span><span class="sxs-lookup"><span data-stu-id="9885a-115">**NOTE** - Some of hello APIs that perform calls out tooAzure storage in ASP.NET Core are asynchronous.</span></span> <span data-ttu-id="9885a-116">Bkz: [uyumsuz ve bekleme ile zaman uyumsuz programlama](http://msdn.microsoft.com/library/hh191443.aspx) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="9885a-116">See [Asynchronous Programming with Async and Await](http://msdn.microsoft.com/library/hh191443.aspx) for more information.</span></span> <span data-ttu-id="9885a-117">Aşağıdaki Hello kodu zaman uyumsuz programlama yöntemleri kullanıldığı varsayılmaktadır.</span><span class="sxs-lookup"><span data-stu-id="9885a-117">hello code below assumes Async programming methods are being used.</span></span>

## <a name="access-tables-in-code"></a><span data-ttu-id="9885a-118">Kod erişim tablolarında</span><span class="sxs-lookup"><span data-stu-id="9885a-118">Access tables in code</span></span>
<span data-ttu-id="9885a-119">ASP.NET Core projeleri tooaccess tablolarda, aşağıdaki Azure tablo depolama erişim öğeleri tooany C# kaynak dosyaları tooinclude hello gerekir.</span><span class="sxs-lookup"><span data-stu-id="9885a-119">tooaccess tables in ASP.NET Core projects, you need tooinclude hello following items tooany C# source files that access Azure table storage.</span></span>

1. <span data-ttu-id="9885a-120">Merhaba ad alanı bildirimleri hello dosyanın üst kısmındaki hello C# bu eklediğinizden emin olun **kullanarak** deyimleri.</span><span class="sxs-lookup"><span data-stu-id="9885a-120">Make sure hello namespace declarations at hello top of hello C# file include these **using** statements.</span></span>
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. <span data-ttu-id="9885a-121">Alma bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne.</span><span class="sxs-lookup"><span data-stu-id="9885a-121">Get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="9885a-122">Kod tooget aşağıdaki kullanım hello depolama bağlantı dizesi ve depolama hesabı bilgilerini hello Azure hizmet yapılandırmasından hello.</span><span class="sxs-lookup"><span data-stu-id="9885a-122">Use hello following code tooget hello your storage connection string and storage account information from hello Azure service configuration.</span></span>
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
            CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
   
    <span data-ttu-id="9885a-123">**Not** -tüm kod hello kod önünde yukarıda hello örnekleri aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="9885a-123">**NOTE** - Use all of hello above code in front of hello code in hello following samples.</span></span>
3. <span data-ttu-id="9885a-124">Alma bir **CloudTableClient** tooreference hello tablo nesneleri depolama hesabınızdaki.</span><span class="sxs-lookup"><span data-stu-id="9885a-124">Get a **CloudTableClient** object tooreference hello table objects in your storage account.</span></span>  
   
        // Create hello table client.
        CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. <span data-ttu-id="9885a-125">Alma bir **CloudTable** başvuru nesnesi tooreference belirli bir tablo ve varlıklar.</span><span class="sxs-lookup"><span data-stu-id="9885a-125">Get a **CloudTable** reference object tooreference a specific table and entities.</span></span>
   
        // Get a reference tooa table named "peopleTable"
        CloudTable table = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a><span data-ttu-id="9885a-126">Kod içinde bir tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="9885a-126">Create a table in code</span></span>
<span data-ttu-id="9885a-127">toocreate hello Azure tablo eklemeniz yeterlidir bir çağrı çok**CreateIfNotExistsAsync()**.</span><span class="sxs-lookup"><span data-stu-id="9885a-127">toocreate hello Azure table, just add a call too**CreateIfNotExistsAsync()**.</span></span>

    // Create hello CloudTable if it does not exist
    await table.CreateIfNotExistsAsync();

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="9885a-128">Bir varlık tooa tablo ekleme</span><span class="sxs-lookup"><span data-stu-id="9885a-128">Add an entity tooa table</span></span>
<span data-ttu-id="9885a-129">tooadd sınıf oluşturma bir varlık tooa tablo varlığınız hello özelliklerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="9885a-129">tooadd an entity tooa table you create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="9885a-130">Merhaba aşağıdaki kodu olarak adlandırılan bir varlık sınıfı tanımlar **CustomerEntity** kullanır hello satır anahtarı olarak müşterinin adını ve hello bölüm anahtarı olarak soyadını hello.</span><span class="sxs-lookup"><span data-stu-id="9885a-130">hello following code defines an entity class called **CustomerEntity** that uses hello customer's first name as hello row key and last name as hello partition key.</span></span>

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

<span data-ttu-id="9885a-131">Varlıkları içeren tablo işlemleri yapılır hello kullanarak **CloudTable** "Access tabloları kodda." içinde daha önce oluşturduğunuz nesnesi</span><span class="sxs-lookup"><span data-stu-id="9885a-131">Table operations involving entities are done using hello **CloudTable** object you created earlier in "Access tables in code."</span></span> <span data-ttu-id="9885a-132">Merhaba **TableOperation** nesnesi bitti hello işlemi toobe temsil eder.</span><span class="sxs-lookup"><span data-stu-id="9885a-132">hello **TableOperation** object represents hello operation toobe done.</span></span> <span data-ttu-id="9885a-133">Kod örnekteki nasıl aşağıdaki hello toocreate bir **CloudTable** nesne ve **CustomerEntity** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="9885a-133">hello following code example shows how toocreate a **CloudTable** object and a **CustomerEntity** object.</span></span> <span data-ttu-id="9885a-134">tooprepare hello işlemi, bir **TableOperation** tooinsert hello müşteri varlık hello tabloya oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9885a-134">tooprepare hello operation, a **TableOperation** is created tooinsert hello customer entity into hello table.</span></span> <span data-ttu-id="9885a-135">Son olarak, hello işlemi CloudTable.ExecuteAsync çağrılarak çalıştırılır.</span><span class="sxs-lookup"><span data-stu-id="9885a-135">Finally, hello operation is executed by calling CloudTable.ExecuteAsync.</span></span>

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create hello TableOperation that inserts hello customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute hello insert operation.
    await peopleTable.ExecuteAsync(insertOperation);

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="9885a-136">Toplu işlem varlık yerleştirme</span><span class="sxs-lookup"><span data-stu-id="9885a-136">Insert a batch of entities</span></span>
<span data-ttu-id="9885a-137">Birden çok varlık, bir tek bir yazma işleminde bir tabloya ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9885a-137">You can insert multiple entities into a table in a single write operation.</span></span> <span data-ttu-id="9885a-138">Merhaba aşağıdaki kod örneği iki varlık nesnesi ("Jeff Smith" ve "Ben Smith") oluşturur, tooa ekler **TableBatchOperation** hello kullanarak nesnesi **Ekle** yöntemi ve başlatır hello işlemiyle CloudTable.ExecuteBatchAsync çağrılıyor.</span><span class="sxs-lookup"><span data-stu-id="9885a-138">hello following code example creates two entity objects ("Jeff Smith" and "Ben Smith"), adds them tooa **TableBatchOperation** object using hello **Insert** method, and then starts hello operation by calling CloudTable.ExecuteBatchAsync.</span></span>

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

## <a name="get-all-of-hello-entities-in-a-partition"></a><span data-ttu-id="9885a-139">Bir bölüm hello varlıkların alın</span><span class="sxs-lookup"><span data-stu-id="9885a-139">Get all of hello entities in a partition</span></span>
<span data-ttu-id="9885a-140">tooquery tüm hello varlıkları bir bölüme kullanmak için bir tablo bir **TableQuery** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="9885a-140">tooquery a table for all of hello entities in a partition, use a **TableQuery** object.</span></span> <span data-ttu-id="9885a-141">Merhaba aşağıdaki kod örneğinde 'Smith' hello bölüm anahtarı olduğu varlıklar için bir filtre belirtir.</span><span class="sxs-lookup"><span data-stu-id="9885a-141">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="9885a-142">Bu örnekte her varlığın hello sorgu sonuçları toohello konsolunda hello alanlarını yazdırır.</span><span class="sxs-lookup"><span data-stu-id="9885a-142">This example prints hello fields of each entity in hello query results toohello console.</span></span>

    // Construct hello query operation for all customer entities where PartitionKey="Smith".
    TableQuery<CustomerEntity> query = new TableQuery<CustomerEntity>().Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));

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

## <a name="get-a-single-entity"></a><span data-ttu-id="9885a-143">Tek bir varlık alma</span><span class="sxs-lookup"><span data-stu-id="9885a-143">Get a single entity</span></span>
<span data-ttu-id="9885a-144">Bir sorgu tooget tek, belirli bir varlığı yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9885a-144">You can write a query tooget a single, specific entity.</span></span> <span data-ttu-id="9885a-145">Merhaba aşağıdaki kod kullanan bir **TableOperation** toospecify 'Ben Smith' adlı bir müşteri nesnesi.</span><span class="sxs-lookup"><span data-stu-id="9885a-145">hello following code uses a **TableOperation** object toospecify a customer named 'Ben Smith'.</span></span> <span data-ttu-id="9885a-146">Bu yöntem bir koleksiyon yerine yalnızca bir varlık döndürür ve hello döndürülen değer **TableResult.Result** olan bir **CustomerEntity** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="9885a-146">This method returns just one entity, rather than a collection, and hello returned value in **TableResult.Result** is a **CustomerEntity** object.</span></span> <span data-ttu-id="9885a-147">Bir sorguda hem Bölüm hem de satır anahtarını belirterek olduğu hello en hızlı yolu tooretrieve hello tek bir varlıktan **tablo** hizmet.</span><span class="sxs-lookup"><span data-stu-id="9885a-147">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello **Table** service.</span></span>

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print hello phone number of hello result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("hello phone number could not be retrieved.");

## <a name="delete-an-entity"></a><span data-ttu-id="9885a-148">Bir varlığı silme</span><span class="sxs-lookup"><span data-stu-id="9885a-148">Delete an entity</span></span>
<span data-ttu-id="9885a-149">Bunu bulduktan sonra bir varlık silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9885a-149">You can delete an entity after you find it.</span></span> <span data-ttu-id="9885a-150">Merhaba aşağıdaki kod görünür "Ben Smith" adlı bir müşteri varlığı için ve bulursa, onu siler.</span><span class="sxs-lookup"><span data-stu-id="9885a-150">hello following code looks for a customer entity named "Ben Smith" and if it finds it, it deletes it.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="9885a-151">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9885a-151">Next steps</span></span>
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

