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
# <a name="getting-started-with-azure-table-storage-and-visual-studio-connected-services-cloud-services-projects"></a>Azure tablo depolaması ve Visual Studio ile çalışmaya başlama (Projeler bulut Hizmetleri) Hizmetleri bağlı
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a>Genel Bakış
Oluşturulan veya hello Visual Studio kullanarak bir Azure depolama hesabı bulut Hizmetleri projesinde başvurulan sonra Visual Studio'da Azure tablo depolaması kullanarak tooget nasıl başlatılacağını bu makalede **bağlı Hizmetleri Ekle** iletişim . Merhaba **bağlı Hizmetleri Ekle** işlemi hello uygun NuGet paketleri tooaccess Azure depolama projenizde yükler ve proje yapılandırma dosyalarını tooyour hello depolama hesabı için hello bağlantı dizesi ekler.

Hello Azure Table depolama hizmeti toostore büyük miktarlarda yapılandırılmış veri sağlar. Merhaba, iç ve dış hello Azure bulut gelen kimliği doğrulanmış çağrıları kabul eden bir NoSQL veri deposu hizmetidir. Azure tabloları, yapılandırılmış ve ilişkisel olmayan verilerin depolanması için idealdir.

başlatılan tooget önce toocreate bir tablo depolama hesabınızdaki gerekir. Nasıl toocreate Azure tablo kodda ve ayrıca nasıl tooperform temel tablo ekleme, değiştirme, okuma ve okuma gibi varlık işlemlerini varlıklar tablo ve göstereceğiz. Merhaba örnekleri C'de yazılmış\# kod ve hello kullan [.NET için Microsoft Azure Storage istemci Kitaplığı](https://msdn.microsoft.com/library/azure/dn261237.aspx).

**Not:** hello tooAzure depolama giden çağrıları gerçekleştirdiğinizde API'leri bazıları zaman uyumsuzdur. Bkz: [uyumsuz ve bekleme ile zaman uyumsuz programlama](http://msdn.microsoft.com/library/hh191443.aspx) daha fazla bilgi için. Aşağıdaki Hello kodu zaman uyumsuz programlama yöntemleri kullanıldığı varsayılmaktadır.

* Bkz: [.NET kullanarak Azure Table storage'ı kullanmaya başlama](../storage/storage-dotnet-how-to-use-tables.md) program aracılığıyla tablolarını düzenleme hakkında daha fazla bilgi.
* Bkz: [Storage belgeleri](https://azure.microsoft.com/documentation/services/storage/) Azure Storage hakkında genel bilgiler.
* Bkz: [bulut Hizmetleri belgelerinde](https://azure.microsoft.com/documentation/services/cloud-services/) Azure bulut hizmetleri hakkında genel bilgi için.
* Bkz: [ASP.NET](http://www.asp.net) ASP.NET uygulamalarını programlama hakkında daha fazla bilgi.

## <a name="access-tables-in-code"></a>Kod erişim tablolarında
Bulut hizmeti projeleri tooaccess tablolarda, aşağıdaki Azure tablo depolama erişim öğeleri tooany C# kaynak dosyaları tooinclude hello gerekir.

1. Merhaba ad alanı bildirimleri hello dosyanın üst kısmındaki hello C# bu eklediğinizden emin olun **kullanarak** deyimleri.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Table;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. Alma bir **CloudStorageAccount** depolama hesabı bilgilerini temsil eden nesne. Kod tooget hello depolama bağlantı dizesi ve depolama hesabı bilgilerini hello Azure hizmet yapılandırmasından aşağıdaki hello kullanın.
   
         CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
           CloudConfigurationManager.GetSetting("<storage account name>
         _AzureStorageConnectionString"));
   > [!NOTE]
   > Tüm kod hello kod önünde yukarıda hello örnekleri aşağıdaki hello kullanın.
   > 
   > 
3. Alma bir **CloudTableClient** tooreference hello tablo nesneleri depolama hesabınızdaki.
   
         // Create hello table client.
         CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
4. Alma bir **CloudTable** başvuru nesnesi tooreference belirli bir tablo ve varlıklar.
   
        // Get a reference tooa table named "peopleTable".
        CloudTable peopleTable = tableClient.GetTableReference("peopleTable");

## <a name="create-a-table-in-code"></a>Kod içinde bir tablo oluşturma
toocreate hello Azure tablo eklemeniz yeterlidir bir çağrı çok**CreateIfNotExistsAsync** elde sonra toohello bir **CloudTable** nesne hello "Access tabloları kod" bölümünde açıklandığı gibi.

    // Create hello CloudTable if it does not exist.
    await peopleTable.CreateIfNotExistsAsync();

## <a name="add-an-entity-tooa-table"></a>Bir varlık tooa tablo ekleme
bir varlık tooa tablosu tooadd varlığınız hello özelliklerini tanımlayan bir sınıf oluşturun. Merhaba aşağıdaki kodu olarak adlandırılan bir varlık sınıfı tanımlar **CustomerEntity** kullanır hello satır anahtarı olarak müşterinin adını ve hello Soyadı hello bölüm anahtarı olarak hello.

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

Varlıkları içeren tablo işlemleri yapılır hello kullanarak **CloudTable** "Access tabloları kodda." bölümünde daha önce oluşturduğunuz nesnesi Merhaba **TableOperation** nesnesi bitti hello işlemi toobe temsil eder. Kod örnekteki nasıl aşağıdaki hello toocreate bir **CloudTable** nesne ve **CustomerEntity** nesnesi. tooprepare hello işlemi, bir **TableOperation** tooinsert hello müşteri varlık hello tabloya oluşturulur. Son olarak, hello işlemi çağrılarak çalıştırılır **CloudTable.ExecuteAsync**.

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    customer1.PhoneNumber = "425-555-0101";

    // Create hello TableOperation that inserts hello customer entity.
    TableOperation insertOperation = TableOperation.Insert(customer1);

    // Execute hello insert operation.
    await peopleTable.ExecuteAsync(insertOperation);


## <a name="insert-a-batch-of-entities"></a>Toplu işlem varlık yerleştirme
Birden çok varlık, bir tek bir yazma işleminde bir tabloya ekleyebilirsiniz. Merhaba aşağıdaki kod örneği iki varlık nesnesi ("Jeff Smith" ve "Ben Smith") oluşturur, tooa ekler **TableBatchOperation** nesne ekleme yöntemi hello ve çağırarak bu başlatır işlemi hello kullanarak  **CloudTable.ExecuteBatchAsync**.

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

