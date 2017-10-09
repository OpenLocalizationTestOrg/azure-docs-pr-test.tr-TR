---
title: "aaaHow tooget, bağlı hizmetler (ASP.NET Core) tablo depolama ve Visual Studio ile çalışmaya | Microsoft Docs"
description: "Visual Studio kullanarak tooa depolama hesabı bağlanma Hizmetleri bağlandıktan sonra tooget Visual Studio'da ASP.NET Core projesinde Azure Table storage ile çalışmaya nasıl"
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
ms.openlocfilehash: e3eb3f3e65456108dd3cde7e3e470f98ba456e35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-started-with-azure-table-storage-and-visual-studio-connected-services"></a>Nasıl tooget bağlı hizmetler Azure tablo depolaması ve Visual Studio ile başlatıldı
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>Genel Bakış
Bu makalede nereden Azure Table'ı kullanmaya Visual Studio'da oluşturulan veya kullanarak bir ASP.NET Core projesini bir Azure depolama hesabında başvurulan sonra depolama hello Visual Studio **bağlı Hizmetleri Ekle** iletişim.

Hello Azure Table depolama hizmeti toostore büyük miktarlarda yapılandırılmış veri sağlar. Merhaba, iç ve dış hello Azure bulut gelen kimliği doğrulanmış çağrıları kabul eden bir NoSQL veri deposu hizmetidir. Azure tabloları, yapılandırılmış ve ilişkisel olmayan verilerin depolanması için idealdir.

Merhaba **bağlı Hizmetleri Ekle** işlemi hello uygun NuGet paketleri tooaccess Azure depolama projenizde yükler ve proje yapılandırma dosyalarını tooyour hello depolama hesabı için hello bağlantı dizesi ekler.

Azure Table storage kullanma hakkında daha fazla genel bilgi için bkz: [.NET kullanarak Azure Table storage'ı kullanmaya başlama](../storage/storage-dotnet-how-to-use-tables.md).

başlatılan tooget önce toocreate bir tablo depolama hesabınızdaki gerekir. Nasıl toocreate Azure tablo kodda göstereceğiz. Ayrıca, nasıl tooperform temel tablo ekleme, değiştirme, okuma ve okuma gibi varlık işlemlerini varlıklar tablo ve göstereceğiz. Merhaba örnekleri C'de yazılmış\# kod ve .NET için Azure Storage istemci kitaplığı hello kullanın.

**Not** -hello ASP.NET Core tooAzure depolama giden çağrıları gerçekleştirdiğinizde API'leri bazıları zaman uyumsuzdur. Bkz: [uyumsuz ve bekleme ile zaman uyumsuz programlama](http://msdn.microsoft.com/library/hh191443.aspx) daha fazla bilgi için. Aşağıdaki Hello kodu zaman uyumsuz programlama yöntemleri kullanıldığı varsayılmaktadır.

## <a name="access-tables-in-code"></a>Kod erişim tablolarında
ASP.NET Core projeleri tooaccess tablolarda, aşağıdaki Azure tablo depolama erişim öğeleri tooany C# kaynak dosyaları tooinclude hello gerekir.

1. Merhaba ad alanı bildirimleri hello dosyanın üst kısmındaki hello C# bu eklediğinizden emin olun **kullanarak** deyimleri.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. Alma bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne. Kod tooget aşağıdaki kullanım hello depolama bağlantı dizesi ve depolama hesabı bilgilerini hello Azure hizmet yapılandırmasından hello.
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
            CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
   
    **Not** -tüm kod hello kod önünde yukarıda hello örnekleri aşağıdaki hello kullanın.
3. Alma bir **CloudTableClient** tooreference hello tablo nesneleri depolama hesabınızdaki.  
   
        // Create hello table client.
        CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. Alma bir **CloudTable** başvuru nesnesi tooreference belirli bir tablo ve varlıklar.
   
        // Get a reference tooa table named "peopleTable"
        CloudTable table = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a>Kod içinde bir tablo oluşturma
toocreate hello Azure tablo eklemeniz yeterlidir bir çağrı çok**CreateIfNotExistsAsync()**.

    // Create hello CloudTable if it does not exist
    await table.CreateIfNotExistsAsync();

## <a name="add-an-entity-tooa-table"></a>Bir varlık tooa tablo ekleme
tooadd sınıf oluşturma bir varlık tooa tablo varlığınız hello özelliklerini tanımlar. Merhaba aşağıdaki kodu olarak adlandırılan bir varlık sınıfı tanımlar **CustomerEntity** kullanır hello satır anahtarı olarak müşterinin adını ve hello bölüm anahtarı olarak soyadını hello.

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

Varlıkları içeren tablo işlemleri yapılır hello kullanarak **CloudTable** "Access tabloları kodda." içinde daha önce oluşturduğunuz nesnesi Merhaba **TableOperation** nesnesi bitti hello işlemi toobe temsil eder. Kod örnekteki nasıl aşağıdaki hello toocreate bir **CloudTable** nesne ve **CustomerEntity** nesnesi. tooprepare hello işlemi, bir **TableOperation** tooinsert hello müşteri varlık hello tabloya oluşturulur. Son olarak, hello işlemi CloudTable.ExecuteAsync çağrılarak çalıştırılır.

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create hello TableOperation that inserts hello customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute hello insert operation.
    await peopleTable.ExecuteAsync(insertOperation);

## <a name="insert-a-batch-of-entities"></a>Toplu işlem varlık yerleştirme
Birden çok varlık, bir tek bir yazma işleminde bir tabloya ekleyebilirsiniz. Merhaba aşağıdaki kod örneği iki varlık nesnesi ("Jeff Smith" ve "Ben Smith") oluşturur, tooa ekler **TableBatchOperation** hello kullanarak nesnesi **Ekle** yöntemi ve başlatır hello işlemiyle CloudTable.ExecuteBatchAsync çağrılıyor.

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

## <a name="get-all-of-hello-entities-in-a-partition"></a>Bir bölüm hello varlıkların alın
tooquery tüm hello varlıkları bir bölüme kullanmak için bir tablo bir **TableQuery** nesnesi. Merhaba aşağıdaki kod örneğinde 'Smith' hello bölüm anahtarı olduğu varlıklar için bir filtre belirtir. Bu örnekte her varlığın hello sorgu sonuçları toohello konsolunda hello alanlarını yazdırır.

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

## <a name="get-a-single-entity"></a>Tek bir varlık alma
Bir sorgu tooget tek, belirli bir varlığı yazabilirsiniz. Merhaba aşağıdaki kod kullanan bir **TableOperation** toospecify 'Ben Smith' adlı bir müşteri nesnesi. Bu yöntem bir koleksiyon yerine yalnızca bir varlık döndürür ve hello döndürülen değer **TableResult.Result** olan bir **CustomerEntity** nesnesi. Bir sorguda hem Bölüm hem de satır anahtarını belirterek olduğu hello en hızlı yolu tooretrieve hello tek bir varlıktan **tablo** hizmet.

    // Create a retrieve operation that takes a customer entity.
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

    // Execute hello retrieve operation.
    TableResult retrievedResult = await peopleTable.ExecuteAsync(retrieveOperation);

    // Print hello phone number of hello result.
    if (retrievedResult.Result != null)
       Console.WriteLine(((CustomerEntity)retrievedResult.Result).PhoneNumber);
    else
       Console.WriteLine("hello phone number could not be retrieved.");

## <a name="delete-an-entity"></a>Bir varlığı silme
Bunu bulduktan sonra bir varlık silebilirsiniz. Merhaba aşağıdaki kod görünür "Ben Smith" adlı bir müşteri varlığı için ve bulursa, onu siler.

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

## <a name="next-steps"></a>Sonraki adımlar
[!INCLUDE [vs-storage-dotnet-tables-next-steps](../../includes/vs-storage-dotnet-tables-next-steps.md)]

