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
# <a name="get-started-with-azure-table-storage-using-net"></a>.NET kullanarak Azure Table Storage’ı kullanmaya başlayın
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

Azure Table storage şemasız tasarım ile bir anahtar/öznitelik sağlama verilerini hello bulutta depolamak yapılandırılmış NoSQL depolayan bir hizmettir. Table storage şemasız olduğu için uygulama geliştikçe verilerinizi hello olarak gereken kolay tooadapt var. Erişim tooTable depolama verileri hızlı ve birçok türdeki uygulamayı için düşük maliyetli ve maliyeti genellikle benzer hacimdeki veriler için geleneksel SQL'e daha düşüktür.

Tablo depolama toostore esnek veri kümelerini kullanıcı verilerini gibi web uygulamaları, adres defterleri, cihaz bilgilerini veya diğer hizmetiniz için gerekli meta veri türleri için kullanabilirsiniz. Bir tablodaki herhangi bir sayıda varlık depolayabilirsiniz ve bir depolama hesabı tabloları, hello depolama hesabının kapasite sınırını toohello herhangi bir sayıda içerebilir.

### <a name="about-this-tutorial"></a>Bu öğretici hakkında
Bu öğretici şunların nasıl yapıldığını gösterir toouse hello [.NET için Azure Storage istemci Kitaplığı](https://www.nuget.org/packages/WindowsAzure.Storage/) bazı ortak Azure Table depolama senaryolarında. Bu senaryolar, tablo oluşturup silme ve tablo verileri ekleme, güncelleştirme, silme ve sorgulama işlemleri için C# örnekleri kullanılarak sunulmaktadır.

## <a name="prerequisites"></a>Ön koşullar

Başarıyla Bu öğreticiyi toocomplete hello:

* [Microsoft Visual Studio](https://www.visualstudio.com/downloads/)
* [.NET için Azure Depolama İstemcisi](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [.NET için Azure Yapılandırma Yöneticisi](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* [Azure depolama hesabı](../storage/common/storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a>Daha fazla örnek
Tablo depolama kullanan diğer örnekler için [.NET’te Azure Table Storage Kullanmaya Başlama](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/). Merhaba örnek uygulamayı indirin ve çalıştırın veya hello kodu github'da göz atın.

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a>Using yönergeleri ekleme
Merhaba aşağıdakileri ekleyin **kullanarak** hello yönergeleri toohello üst `Program.cs` dosyası:

```csharp
using Microsoft.Azure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Table; // Namespace for Table storage types
```

### <a name="parse-hello-connection-string"></a>Merhaba bağlantı dizesini ayrıştırma
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-table-service-client"></a>Merhaba tablo hizmeti istemcisi oluşturma
Merhaba [CloudTableClient] [ dotnet_CloudTableClient] sınıfı sağlar, size, tooretrieve tabloları ve varlıkları tablo depolama alanına depolanır. Tek yönlü toocreate hello tablo hizmeti istemcisi şöyledir:

```csharp
// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```

Artık veri okuyan ve yazan veri tooTable depolama hazır toowrite kodu bulunur.

## <a name="create-a-table"></a>Bir tablo oluşturma
Bu örnekte gösterilir nasıl toocreate zaten yoksa, tablo:

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

## <a name="add-an-entity-tooa-table"></a>Bir varlık tooa tablo ekleme
Varlıkları türetilen özel bir sınıf kullanarak tooC # nesnelerini eşleme [TableEntity][dotnet_TableEntity]. bir varlık tooa tablosu tooadd varlığınız hello özelliklerini tanımlayan bir sınıf oluşturun. Merhaba aşağıdaki kod hello müşterinin adını hello satır anahtarını ve Soyadı gibi hello bölüm anahtarı olarak kullanan bir varlık sınıfı tanımlar. Birlikte, bir varlığın bölüm ve satır anahtarı, hello tabloda benzersizce. Anahtarları aynı bölüm anahtarına farklı sahip varlıklar daha hızlı sorgulanabilir hello varlıklarıyla bölüm, ancak farklı bölüm anahtarlarının kullanılması paralel işlemler daha fazla ölçeklenebilirlik sağlar. Varlıkları toobe tablolarında depolanır, örneğin hello türetilen desteklenen bir türde olmalıdır [TableEntity] [ dotnet_TableEntity] sınıfı. Toostore bir tabloda istediğiniz varlık özellikleri hello türünün ortak özelliklerine olması ve alma ve değerlerin ayarını destekler. Bununla birlikte varlık türü parametresiz bir oluşturucu *olmalıdır*.

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

Varlıklarla ilgili tablo işlemleri hello gerçekleştirilir [CloudTable] [ dotnet_CloudTable] hello "bir tablo oluşturma" bölümünde daha önce oluşturduğunuz nesne. Merhaba gerçekleştirilen işlem toobe tarafından temsil edilen bir [TableOperation] [ dotnet_TableOperation] nesnesi. Merhaba aşağıdaki kod örneğinde hello oluşturulmasını hello gösterir [CloudTable] [ dotnet_CloudTable] nesnesi ve ardından bir **CustomerEntity** nesnesi. tooprepare hello işlemi, bir [TableOperation] [ dotnet_TableOperation] nesne hello tabloya tooinsert hello müşteri varlığı oluşturulur. Son olarak, hello işlemi çağrılarak çalıştırılır [CloudTable][dotnet_CloudTable].[ Yürütme][dotnet_CloudTable_Execute].

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

## <a name="insert-a-batch-of-entities"></a>Toplu işlem varlık yerleştirme
Bir tabloya tek bir yazma işlemiyle çok sayıda varlık yerleştirebilirsiniz. Toplu işlemler ile ilgili diğer notlar:

* Güncelleştirmeleri, siler ve eklemeleri gerçekleştirebilirsiniz hello aynı tek toplu işlemi.
* Tek bir toplu işlem too100 varlık içerebilir.
* Tek bir toplu işlem tüm varlıkları hello olmalıdır aynı bölüm anahtarı.
* Olası tooperform toplu işlem olarak bir sorgu olmakla birlikte, hello hello toplu işlemdeki tek işlem olmalıdır.

Merhaba aşağıdaki kod örneği iki varlık nesnesi oluşturur ve her çok ekler[TableBatchOperation] [ dotnet_TableBatchOperation] hello kullanarak [Ekle] [ dotnet_TableBatchOperation_Insert] yöntem. Ardından, [CloudTable][dotnet_CloudTable].[ ExecuteBatch] [ dotnet_CloudTable_ExecuteBatch] tooexecute hello işlem çağrılır.

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

## <a name="retrieve-all-entities-in-a-partition"></a>Tüm varlıkları bir bölüme alma
tooquery kullanımı bir bölümdeki tüm varlıklar için bir tablo bir [TableQuery] [ dotnet_TableQuery] nesnesi. Merhaba aşağıdaki kod örneğinde 'Smith' hello bölüm anahtarı olduğu varlıklar için bir filtre belirtir. Bu örnekte her varlığın hello sorgu sonuçları toohello konsolunda hello alanlarını yazdırır.

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

## <a name="retrieve-a-range-of-entities-in-a-partition"></a>Bir bölüme bir grup varlık alma
Tüm varlıkları bir bölüme tooquery istemiyorsanız, hello bölüm anahtarı Filtresi ile bir satır anahtarı filtresini birleştirerek bir aralık belirtebilirsiniz. Merhaba aşağıdaki kod örneği iki filtreleri tooget tüm varlıklar 'burada hello satır anahtarı (ad) hello alfabede 'E' önce bir harf ile başlar, ardından hello sorgu sonuçlarını yazdırır Smith' bölümünde kullanır.

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

## <a name="retrieve-a-single-entity"></a>Tek bir varlık alma
Bir sorgu tooretrieve tek, belirli bir varlığı yazabilirsiniz. Merhaba aşağıdaki kod kullanır [TableOperation] [ dotnet_TableOperation] toospecify hello Müşteri 'Ben Smith'. Bu yöntem bir koleksiyon yerine yalnızca bir varlık döndürür ve hello döndürülen değer [TableResult][dotnet_TableResult].[ Sonuç] [ dotnet_TableResult_Result] olan bir **CustomerEntity** nesnesi. Bir sorguda hem Bölüm hem de satır anahtarını belirterek hello en hızlı yolu tooretrieve hello tablo hizmetinden tek bir varlık olur.

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

## <a name="replace-an-entity"></a>Bir varlığı değiştirme
bir varlık tooupdate hello tablo hizmetinden alın, hello varlık nesnesini değiştirin ve ardından hello Değişiklikleri Kaydet toohello tablo hizmeti yeniden. Merhaba aşağıdaki kod mevcut bir müşterinin telefon numarasını değiştirir. [Insert][dotnet_TableOperation_Insert] yöntemini çağırmak yerine bu kod [Replace][dotnet_TableOperation_Replace] kullanır. [Değiştir] [ dotnet_TableOperation_Replace] onu, hello işlemi başarısız olur; bu durumda alındığından beri hello varlık hello sunucuda değiştirilmediği sürece nedenler hello varlık toobe tam olarak hello sunucu üzerinde değiştirildi. Uygulamanızı bir değişikliğin yanlışlıkla üzerine yazılmasını arasında alma hello ve uygulamanızın başka bir bileşen tarafından güncelleştirme yapılan tooprevent hatasıdır. Merhaba bu hatanın uygun işleme tooretrieve hello yeniden varlıktır, (hala geçerli ise) değişiklikleri yapın ve ardından başka bir gerçekleştirin [Değiştir] [ dotnet_TableOperation_Replace] işlemi. Merhaba sonraki bölümde gösterir, nasıl toooverride bu davranışı.

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

## <a name="insert-or-replace-an-entity"></a>Bir varlığı yerleştirme veya değiştirme
[Değiştir] [ dotnet_TableOperation_Replace] hello varlık hello sunucudan alındığından beri değiştirilmişse işlemleri başarısız olur. Ayrıca, hello varlık hello sunucusundan ilk sırada hello için aldığınız gerekir [Değiştir] [ dotnet_TableOperation_Replace] toobe işlemi başarılı. Bazı durumlarda, Bununla birlikte, hello varlık hello sunucuda bulunduğundan ve depolanan hello geçerli değerlerin ilgisiz olup olmadığını bilemeyebilirsiniz. Güncelleştirmeniz tümünün üzerine yazmalıdır. tooaccomplish Bu, kullanacağınız bir [Yerleştir veya Değiştir] [ dotnet_TableOperation_InsertOrReplace] işlemi. Bu işlem yok veya bu zaman hello yapılan son güncelleştirmeden bağımsız olarak, varsa yerini hello varlık ekler.

Aşağıdaki kod örneğine hello 'Gamze Can' için müşteri varlığı oluşturulur ve hello 'Kişiler' tablosuna. Merhaba ardından, kullandığımız [Yerleştir veya Değiştir] [ dotnet_TableOperation_InsertOrReplace] işlemi toosave hello sahip bir varlık aynı bölüm anahtarı (CAN) ve satır anahtarı (Gamze) toohello sunucu hello PhoneNumber farklı bir değerle bu süre özellik. [InsertOrReplace][dotnet_TableOperation_InsertOrReplace] özelliğini kullandığımız için tüm özellik değerleri değiştirilir. 'Gamze Can' varlık zaten hello tablosunda yüklediniz, ancak bunu eklenmiş.

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

## <a name="query-a-subset-of-entity-properties"></a>Giriş özellikleri alt kümesi sorgulama
Tablo sorgusu, tüm hello varlık özellikleri yerine bir varlıktaki birkaç özelliği alabilir. Projeksiyon olarak adlandırılan bu yöntem bant genişliğini azaltır ve özellikle büyük varlıklar için sorgu performansını iyileştirebilir. koddan hello Hello sorguda yalnızca hello e-posta adresleri varlıkların hello tablodaki döndürür. Bu, [DynamicTableEntity][dotnet_DynamicTableEntity] ve ayrıca [EntityResolver][dotnet_EntityResolver] sorgusu kullanılarak gerçekleştirilir. Merhaba projeksiyon hakkında daha fazla bilgiyi [Tanıtımı Upsert ve sorgu projeksiyon blog yazısı][blog_post_upsert]. Bu kod yalnızca hello tablo hizmetinde bir hesap kullanırken çalıştırılır şekilde projeksiyon hello depolama öykünücüsü tarafından desteklenmiyor.

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

## <a name="delete-an-entity"></a>Bir varlığı silme
Hello kullanarak aldıktan sonra bir varlık kolayca silebilirsiniz bir varlığı güncelleştirmek için gösterilen aynı düzeni. koddan hello alır ve bir müşteri varlığı siler.

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

## <a name="delete-a-table"></a>Bir tablo silme
Son olarak, aşağıdaki kod örneğine hello bir depolama hesabından bir tablo siler. Silinmiş bir tablo bir süre hello silmeyi izleyen yeniden oluşturulacak kullanılamaz toobe olacaktır.

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

## <a name="retrieve-entities-in-pages-asynchronously"></a>Sayfalarda zaman uyumsuz olarak varlıkları alma
Çok sayıda varlık okuyorsanız ve tooprocess/görüntü varlıklar alındıktan yerine şekilde kendileri için tüm tooreturn bekleniyor, varlıkları bölümlendirilmiş bir sorgu kullanarak alabileceğiniz istediğiniz istiyorsanız. Bu örnek, böylece yürütme sırasında engellenmeyen hello zaman uyumsuz-bekleme düzenini kullanarak sayfaları tooreturn sonuçlarında çok sayıda sonuç tooreturn için nasıl bekliyorsunuz gösterir. Zaman uyumsuz-bekleme yönteminin deseninde .NET ile kullanma hakkında daha fazla ayrıntı hello için bkz: [uyumsuz ve bekleme (C# ve Visual Basic) ile zaman uyumsuz programlama](https://msdn.microsoft.com/library/hh191443.aspx).

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

## <a name="next-steps"></a>Sonraki adımlar
Table Storage hello temel bilgileri öğrendiğinize göre bu bağlantıları toolearn daha karmaşık depolama görevleri hakkında izleyin:

* [Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md) Windows, macOS ve Linux Azure Storage verilerle görsel olarak toowork sağlayan Microsoft boş bir tek başına uygulamadır.
* [.NET’te Azure Table Storage Kullanmaya Başlama](https://azure.microsoft.com/documentation/samples/storage-table-dotnet-getting-started/) bölümünde daha fazla Tablo depolama örneği bulabilirsiniz
* Kullanılabilir API'ler ile ilgili tam Ayrıntılar için Hello tablo hizmeti başvuru belgelerini görüntüleyin:
* [.NET başvurusu için Depolama İstemci Kitaplığı](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)
* [REST API başvurusu](http://msdn.microsoft.com/library/azure/dd179355)
* Nasıl toosimplify hello kodu yazdığınız öğrenin hello kullanarak Azure Storage ile toowork [Azure Web işleri SDK'si](../app-service-web/websites-dotnet-webjobs-sdk-get-started.md)
* Veri depolama için ek seçenekleri hakkında daha fazla özellik kılavuzları toolearn görüntüleyin.
* [.NET kullanarak Azure Blob storage'ı kullanmaya başlama](../storage/blobs/storage-dotnet-how-to-use-blobs.md) toostore yapılandırılmamış veriler.
* [.NET (C#) kullanarak tooSQL veritabanına bağlanma](../sql-database/sql-database-develop-dotnet-simple.md) toostore ilişkisel veri.

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
