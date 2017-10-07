---
title: aaaHow toouse Java'dan Table storage | Microsoft Docs
description: "Bir NoSQL veri deposu olan Azure Table storage kullanılarak hello bulutta yapılandırılmış veri depolayın."
services: storage
documentationcenter: java
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 45145189-e67f-4ca6-b15d-43af7bfd3f97
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: f72cac3fc10cf0aef74780b84c515d93d715d787
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-java"></a>Nasıl toouse Java'dan Table storage
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a>Genel Bakış
Bu kılavuz size nasıl tooperform yaygın senaryolar kullanarak Azure Table depolama hizmeti hello gösterir. Merhaba örnekleri Java'da yazılmış ve hello kullan [Java için Azure depolama SDK'sı][Azure Storage SDK for Java]. Merhaba kapsanan senaryolar dahil **oluşturma**, **listeleme**, ve **silme** tabloları, yanı **ekleme**,  **Sorgulama**, **değiştirme**, ve **silme** bir tabloda varlıklar. Merhaba tabloları hakkında daha fazla bilgi için bkz: [sonraki adımlar](#Next-Steps) bölümü.

Not: Bir SDK'sı Android cihazlarda Azure depolama kullanan geliştiriciler için kullanılabilir. Daha fazla bilgi için bkz: Merhaba [Android için Azure depolama SDK'sı][Azure Storage SDK for Android].

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a>Java uygulaması oluşturma
Bu kılavuzda, bir Java uygulaması içinde yerel olarak veya bir web rolü veya Azure çalışan rolünde çalışan kodu çalıştırılabilir depolama özelliklerini kullanır.

toodo tooinstall ihtiyacınız olacak şekilde, Java Geliştirme Seti (JDK) hello ve Azure aboneliğinizde bir Azure depolama hesabı oluşturun. Bunu yaptıktan sonra geliştirme sisteminizde hello en düşük gereksinimleri ve hello listelenen bağımlılıkları karşılayan tooverify gerekir [Java için Azure depolama SDK'sı] [ Azure Storage SDK for Java] github'daki. Sisteminiz bu gereksinimleri karşılıyorsa, karşıdan yükleme ve bu depodan sisteminizdeki Java için hello Azure depolama kitaplıkları için hello yönergeleri izleyebilir. Bu görevleri tamamladıktan sonra mümkün toocreate hello örnekleri bu makalede kullanan bir Java uygulaması olacaktır.

## <a name="configure-your-application-tooaccess-table-storage"></a>Uygulama tooaccess tablo depolama alanını yapılandırma
İçeri aktarma deyimlerini toohello dosyasının üst kısmında toouse Microsoft Azure depolama API'leri tooaccess tabloları istediğiniz hello Java aşağıdaki hello ekleyin:

```java
// Include hello following imports toouse table APIs
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.table.*;
import com.microsoft.azure.storage.table.TableQuery.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a>Bir Azure depolama bağlantı dizesi ayarlama
Bir Azure storage istemcisi bir depolama bağlantı dizesi toostore uç kullanır ve Veri Yönetimi Hizmetleri erişmek için kimlik bilgileri. Bir istemci uygulamasında çalıştırırken hello depolama bağlantı dizesi biçimi aşağıdaki, hello depolama hesabınızın adını kullanarak hello olarak sağlamak ve hello listelenen hello depolama hesabı için birincil erişim anahtarını hello gerekir [Azure portal](https://portal.azure.com)hello için *AccountName* ve *AccountKey* değerleri. Bu örnek, bir statik alan toohold hello bağlantı dizesini nasıl bildirebilir gösterir:

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

Çalışan bir uygulama içinde Microsoft Azure rolünde içinde bu dize hello hizmet yapılandırma dosyasında depolanabilir *ServiceConfiguration.cscfg*ve bir çağrı toohello ile erişilebilir  **RoleEnvironment.getConfigurationSettings** yöntemi. Merhaba bağlantı dizesinden alma örneği bir **ayarı** adlı öğe *StorageConnectionString* hello hizmet yapılandırma dosyasında:

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

Merhaba aşağıdaki örnekleri bu iki yöntem tooget hello depolama bağlantı dizesi birini kullandığınızı varsayar.

## <a name="how-to-create-a-table"></a>Nasıl yapılır: bir tablo oluştur
A **CloudTableClient** nesne tabloları ve varlıkları için başvuru nesneleri almak olanak sağlar. Merhaba aşağıdaki kod oluşturur bir **CloudTableClient** nesne ve yeni bir toocreate kullanan **CloudTable** tablo temsil eden nesne adında "Kişiler". (Not: ek yolları toocreate vardır **CloudStorageAccount** nesneleri; daha fazla bilgi için bkz: **CloudStorageAccount** hello içinde [Azure Storage istemci SDK'sı başvurusu].)

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create hello table if it doesn't exist.
    String tableName = "people";
    CloudTable cloudTable = tableClient.getTableReference(tableName);
    cloudTable.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-list-hello-tables"></a>Nasıl yapılır: hello Tabloları Listele
tooget tabloları, çağrı hello listesini **CloudTableClient.listTables()** yöntemi tooretrieve tablo adları iterable bir listesi.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Loop through hello collection of table names.
    for (String table : tableClient.listTables())
    {
        // Output each table name.
        System.out.println(table);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-add-an-entity-tooa-table"></a>Nasıl yapılır: bir varlık tooa tablo ekleme
Varlıkları eşleme özel bir sınıf uygulama kullanarak tooJava nesneleri **TableEntity**. Kolaylık olması için hello **TableServiceEntity** uygulayan sınıf **TableEntity** ve toogetter ve ayarlayıcı yöntemleri adlı için kullandığı yansıma toomap özellikleri hello özellikleri. bir varlık tooa tablosu tooadd ilk varlığınız hello özelliklerini tanımlayan bir sınıf oluşturun. Merhaba aşağıdaki kod hello müşterinin adını hello satır anahtarını ve Soyadı hello bölüm anahtarı olarak kullanan bir varlık sınıfı tanımlar. Birlikte, bir varlığın bölüm ve satır anahtarı benzersiz şekilde hello varlık hello tablosundaki tanımlar. Aynı bölüm anahtarına farklı bölüm anahtarlarının göre daha hızlı sorgulanabilir hello olan varlık.

```java
public class CustomerEntity extends TableServiceEntity {
    public CustomerEntity(String lastName, String firstName) {
        this.partitionKey = lastName;
        this.rowKey = firstName;
    }

    public CustomerEntity() { }

    String email;
    String phoneNumber;

    public String getEmail() {
        return this.email;
    }

    public void setEmail(String email) {
        this.email = email;
    }

    public String getPhoneNumber() {
        return this.phoneNumber;
    }

    public void setPhoneNumber(String phoneNumber) {
        this.phoneNumber = phoneNumber;
    }
}
```

Varlıkları içeren tablo işlemleri gerektiren bir **TableOperation** nesnesi. Bu nesne ile yürütülebilir bir varlık üzerinde gerçekleştirilen hello işlemi toobe tanımlayan bir **CloudTable** nesnesi. Merhaba aşağıdaki kod oluşturur hello yeni bir örneğini **CustomerEntity** depolanan bazı müşteri verileri toobe sınıfıyla. Merhaba kod sonraki çağrılar **TableOperation.insertOrReplace** toocreate bir **TableOperation** bir tabloya tooinsert bir varlık nesnesini ve ilişkilendirilmiş bir hello yeni **CustomerEntity**onunla. Son olarak, hello kod hello çağırır **yürütme** hello yöntemi **CloudTable** hello "Kişiler" tablosu ve hello yeni belirten nesnesini **TableOperation**, hangi sonra gönderir bir hello "Kişiler" tablosuna toohello depolama hizmeti tooinsert hello yeni müşteri varlığı isteyebilir veya zaten varsa hello varlık değiştirin.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.setEmail("Walter@contoso.com");
    customer1.setPhoneNumber("425-555-0101");

    // Create an operation tooadd hello new customer toohello people table.
    TableOperation insertCustomer1 = TableOperation.insertOrReplace(customer1);

    // Submit hello operation toohello table service.
    cloudTable.execute(insertCustomer1);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-a-batch-of-entities"></a>Nasıl yapılır: bir toplu işlem varlık yerleştirme
Bir yazma işlemi varlıklar toohello tablo hizmeti toplu ekleyebilirsiniz. Merhaba aşağıdaki kod oluşturur bir **TableBatchOperation** nesne sonra üç ekleme işlemleri tooit ekler. Her ekleme işlemi yeni bir varlık nesnesi oluşturma değerlerini ayarlama ve hello çağırma eklenir **Ekle** hello yöntemi **TableBatchOperation** tooassociate hello varlık yeni bir nesne işlem ekleyin. Ardından, kod çağrıları hello **yürütme** hello üzerinde **CloudTable** hello "Kişiler" tablosu ve hello belirten nesnesini **TableBatchOperation** hello toplu tablo gönderen nesnesi tek bir istekte Operations toohello depolama hizmeti.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Define a batch operation.
    TableBatchOperation batchOperation = new TableBatchOperation();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a customer entity tooadd toohello table.
    CustomerEntity customer = new CustomerEntity("Smith", "Jeff");
    customer.setEmail("Jeff@contoso.com");
    customer.setPhoneNumber("425-555-0104");
    batchOperation.insertOrReplace(customer);

    // Create another customer entity tooadd toohello table.
    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.setEmail("Ben@contoso.com");
    customer2.setPhoneNumber("425-555-0102");
    batchOperation.insertOrReplace(customer2);

    // Create a third customer entity tooadd toohello table.
    CustomerEntity customer3 = new CustomerEntity("Smith", "Denise");
    customer3.setEmail("Denise@contoso.com");
    customer3.setPhoneNumber("425-555-0103");
    batchOperation.insertOrReplace(customer3);

    // Execute hello batch of operations on hello "people" table.
    cloudTable.execute(batchOperation);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

Toplu işlemler ile ilgili bazı şeyleri toonote:

* Too100 ekleme, silme, birleştirme, Değiştir, ekleme veya birleştirme, gerçekleştirmek eklemek veya tek bir toplu işteki herhangi bir birleşimini işlemlerinde değiştirin.
* Merhaba toplu işlemdeki tek işlem hello olması durumunda toplu işlem bir alma işlemi olabilir.
* Tek bir toplu işlem tüm varlıkları hello olmalıdır aynı bölüm anahtarı.
* Sınırlı tooa 4 MB veri yükü toplu işlemdir.

## <a name="how-to-retrieve-all-entities-in-a-partition"></a>Nasıl yapılır: bir bölümdeki tüm varlıkları almak
kullanabileceğiniz tooquery tablo varlıkları bir bölüme için bir **TableQuery**. Çağrı **TableQuery.from** toocreate sorguda belirtilen sonuç türü döndüren belirli bir tablo üzerinde. Merhaba aşağıdaki kod 'Smith' hello bölüm anahtarı olduğu varlıklar için bir filtre belirtir. **TableQuery.generateFilterCondition** toocreate filtreleri sorgular için bir yardımcı yöntemdir. Çağrı **nerede** hello tarafından döndürülen hello başvurusundaki **TableQuery.from** yöntemi tooapply hello filtre toohello sorgusu. Ne zaman hello sorgu yürütüldüğünde çağrısı ile çok**yürütme** hello üzerinde **CloudTable** nesne döndürdüğü bir **yineleyici** hello ile **CustomerEntity**sonuç türü belirtildi. Merhaba sonra kullanabileceğiniz **yineleyici** döndürülen bir her döngü tooconsume hello sonuçlar için. Bu kodu her varlığın hello sorgu sonuçları toohello konsolunda hello alanlarını yazdırır.

```java
try
{
    // Define constants for filters.
    final String PARTITION_KEY = "PartitionKey";
    final String ROW_KEY = "RowKey";
    final String TIMESTAMP = "Timestamp";

    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where hello partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Specify a partition query, using "Smith" as hello partition key filter.
    TableQuery<CustomerEntity> partitionQuery =
        TableQuery.from(CustomerEntity.class)
        .where(partitionFilter);

    // Loop through hello results, displaying information about hello entity.
    for (CustomerEntity entity : cloudTable.execute(partitionQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-range-of-entities-in-a-partition"></a>Nasıl yapılır: bir dizi varlıkları bir bölüme alma
Tüm hello varlıkları bir bölüme tooquery istemiyorsanız, bir filtre Karşılaştırma işleçleri kullanarak bir aralığı belirtebilirsiniz. Aşağıdaki iki filtreler tooget "Smith" bölümündeki tüm varlıklar hello satır anahtarı (ad) too'E oluşturan bir harf ile başladığı kod birleştirir hello' hello alfabetik olarak. Ardından hello sorgu sonuçlarını yazdırır. Kullanıyorsanız hello varlıklar eklenen toohello tablo hello toplu ekleme başlığına bakın, yalnızca iki varlık bu saati (Ben ve Gamze Smith); döndürülür Jeff Smith dahil değildir.

```java
try
{
    // Define constants for filters.
    final String PARTITION_KEY = "PartitionKey";
    final String ROW_KEY = "RowKey";
    final String TIMESTAMP = "Timestamp";

    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a filter condition where hello partition key is "Smith".
    String partitionFilter = TableQuery.generateFilterCondition(
        PARTITION_KEY,
        QueryComparisons.EQUAL,
        "Smith");

    // Create a filter condition where hello row key is less than hello letter "E".
    String rowFilter = TableQuery.generateFilterCondition(
        ROW_KEY,
        QueryComparisons.LESS_THAN,
        "E");

    // Combine hello two conditions into a filter expression.
    String combinedFilter = TableQuery.combineFilters(partitionFilter,
        Operators.AND, rowFilter);

    // Specify a range query, using "Smith" as hello partition key,
    // with hello row key being up toohello letter "E".
    TableQuery<CustomerEntity> rangeQuery =
        TableQuery.from(CustomerEntity.class)
        .where(combinedFilter);

    // Loop through hello results, displaying information about hello entity
    for (CustomerEntity entity : cloudTable.execute(rangeQuery)) {
        System.out.println(entity.getPartitionKey() +
            " " + entity.getRowKey() +
            "\t" + entity.getEmail() +
            "\t" + entity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-retrieve-a-single-entity"></a>Nasıl yapılır: tek bir varlık alma
Bir sorgu tooretrieve tek, belirli bir varlığı yazabilirsiniz. Merhaba aşağıdaki kod çağrıları **TableOperation.retrieve** oluşturmak yerine bölüm anahtarını ve satır anahtar parametreleri toospecify hello müşteri "Jeff Smith" ile bir **TableQuery** ve filtreleri toodo hello kullanma aynı şey. Çalıştırıldığında, hello işlemi döndürür yalnızca bir varlık yerine bir koleksiyon alır. Merhaba **getResultAsType** yöntemi çevirir hello sonuç toohello türü hello atama hedefinin bir **CustomerEntity** nesnesi. Bu tür hello sorgu için belirtilen başlangıç türü ile uyumlu değilse, bir özel durum. Bir tam bölüm ve satır anahtarını eşleşen hiçbir varlık varsa, bir null değeri döndürülür. Bir sorguda hem Bölüm hem de satır anahtarını belirterek hello en hızlı yolu tooretrieve hello tablo hizmetinden tek bir varlık olur.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff"
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit hello operation toohello table service and get hello specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Output hello entity.
    if (specificEntity != null)
    {
        System.out.println(specificEntity.getPartitionKey() +
            " " + specificEntity.getRowKey() +
            "\t" + specificEntity.getEmail() +
            "\t" + specificEntity.getPhoneNumber());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-modify-an-entity"></a>Nasıl yapılır: bir varlık değiştirme
toomodify bir varlık hello tablo hizmetinden alın, değişiklikleri toohello varlık nesnesini yapın ve hello değişiklikleri geri toohello tablo hizmeti değiştirin veya birleştirme işlemi ile Kaydet. Merhaba aşağıdaki kod mevcut bir müşterinin telefon numarasını değiştirir. Çağırmak yerine **TableOperation.insert** tooinsert yaptığımız gibi bu kodu çağırır **TableOperation.replace**. Merhaba **CloudTable.execute** hello tablo hizmeti yöntemini çağırır ve hello varlık değiştirilir, bu uygulama, alınan bu yana başka bir uygulama, başlangıç zamanında değiştirmediyse. Bu durum oluştuğunda bir özel durum ve hello varlık gerekir alınan, değiştirilecek ve yeniden kaydedildi. Bu iyimser eşzamanlılık yeniden deneme deseni, bir dağıtılmış depolama sistemi yaygındır.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff =
        TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Submit hello operation toohello table service and get hello specific entity.
    CustomerEntity specificEntity =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Specify a new phone number.
    specificEntity.setPhoneNumber("425-555-0105");

    // Create an operation tooreplace hello entity.
    TableOperation replaceEntity = TableOperation.replace(specificEntity);

    // Submit hello operation toohello table service.
    cloudTable.execute(replaceEntity);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-query-a-subset-of-entity-properties"></a>Nasıl yapılır: bir giriş özellikleri alt kümesi sorgulama
Sorgu tooa tabloya bir varlık birkaç özelliği alabilir. Projeksiyon olarak adlandırılan bu yöntem bant genişliğini azaltır ve özellikle büyük varlıklar için sorgu performansını iyileştirebilir. Merhaba koddan hello sorguda kullanan hello **seçin** yöntemi tooreturn yalnızca hello e-posta adreslerini hello tablosundaki varlıklar. Merhaba sonuçları bir koleksiyona öngörülen **dize** hello Yardımı ile bir **Varlıkçözümleyicisi**, hangi tür dönüştürme hello sunucusundan döndürülen hello varlıklar üzerinde hello. İçinde projeksiyon hakkında daha fazla bilgiyi [Azure tabloları: Tanıtımı Upsert ve sorgu projeksiyon][Azure Tables: Introducing Upsert and Query Projection]. Bu kod yalnızca bir hesap hello tablo hizmetinde kullanırken nedenle projeksiyon hello yerel depolama öykünücüsünde desteklenmez unutmayın.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Define a projection query that retrieves only hello Email property
    TableQuery<CustomerEntity> projectionQuery =
        TableQuery.from(CustomerEntity.class)
        .select(new String[] {"Email"});

    // Define a Entity resolver tooproject hello entity toohello Email value.
    EntityResolver<String> emailResolver = new EntityResolver<String>() {
        @Override
        public String resolve(String PartitionKey, String RowKey, Date timeStamp, HashMap<String, EntityProperty> properties, String etag) {
            return properties.get("Email").getValueAsString();
        }
    };

    // Loop through hello results, displaying hello Email values.
    for (String projectedString :
        cloudTable.execute(projectionQuery, emailResolver)) {
            System.out.println(projectedString);
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-insert-or-replace-an-entity"></a>Nasıl yapılır: eklemek ya da bir varlığı değiştirme
Genellikle tooadd bir varlık tooa tablo hello tablosunda zaten varsa bilmeden istiyor. Bir ekleme veya değiştirme işlemi toomake onu yok veya aşması durumunda bir varolan hello yerine gerekiyorsa, hello varlık ekler tek bir istek sağlar. Önceki örneklere oluşturma, hello aşağıdaki kodu ekler veya "Walter Harp için" Merhaba varlığı değiştirir. Yeni bir varlık oluşturduktan sonra bu kod, hello'i çağırır **TableOperation.insertOrReplace** yöntemi. Daha sonra bu kodu çağırır **yürütme** hello üzerinde **CloudTable** nesne ile Merhaba tablo ve hello ekleme veya tablo işlemi hello parametre olarak değiştirin. bir varlığın, yalnızca bölüm tooupdate hello **TableOperation.insertOrMerge** yöntemi yerine kullanılabilir. Bu kod yalnızca bir hesap hello tablo hizmetinde kullanırken çalıştığında, ekleme veya değiştirme hello yerel depolama öykünücüsünde desteklenmez unutmayın. Ekleme veya değiştirme ve Ekle-veya-birleştirme bu hakkında daha fazla bilgi edinmek [Azure tabloları: Tanıtımı Upsert ve sorgu projeksiyon][Azure Tables: Introducing Upsert and Query Projection].

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create a new customer entity.
    CustomerEntity customer5 = new CustomerEntity("Harp", "Walter");
    customer5.setEmail("Walter@contoso.com");
    customer5.setPhoneNumber("425-555-0106");

    // Create an operation tooadd hello new customer toohello people table.
    TableOperation insertCustomer5 = TableOperation.insertOrReplace(customer5);

    // Submit hello operation toohello table service.
    cloudTable.execute(insertCustomer5);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-an-entity"></a>Nasıl yapılır: bir varlığı silme
Bir varlık, onu aldıktan sonra kolayca silebilirsiniz. Merhaba varlık alındıktan sonra arama **TableOperation.delete** hello varlık toodelete ile. ' I çağırın **yürütme** hello üzerinde **CloudTable** nesnesi. koddan hello alır ve bir müşteri varlığı siler.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Create a cloud table object for hello table.
    CloudTable cloudTable = tableClient.getTableReference("people");

    // Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
    TableOperation retrieveSmithJeff = TableOperation.retrieve("Smith", "Jeff", CustomerEntity.class);

    // Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
    CustomerEntity entitySmithJeff =
        cloudTable.execute(retrieveSmithJeff).getResultAsType();

    // Create an operation toodelete hello entity.
    TableOperation deleteSmithJeff = TableOperation.delete(entitySmithJeff);

    // Submit hello delete operation toohello table service.
    cloudTable.execute(deleteSmithJeff);
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="how-to-delete-a-table"></a>Nasıl yapılır: bir tablo silme
Son olarak, hello aşağıdaki kod bir tablo bir depolama hesabını siler. Bir süre hello silmeyi, genellikle değerinden kırk saniye izleyen yeniden kullanılamaz toobe, silinmiş olan bir tablo olur.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount =
        CloudStorageAccount.parse(storageConnectionString);

    // Create hello table client.
    CloudTableClient tableClient = storageAccount.createCloudTableClient();

    // Delete hello table and all its data if it exists.
    CloudTable cloudTable = tableClient.getTableReference("people");
    cloudTable.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```
[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="next-steps"></a>Sonraki adımlar

* [Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md) Windows, macOS ve Linux Azure Storage verilerle görsel olarak toowork sağlayan Microsoft boş bir tek başına uygulamadır.
* [Azure depolama için Java SDK'sı][Azure Storage SDK for Java]
* [Azure Storage istemci SDK'sı başvurusu][Azure Storage istemci SDK'sı başvurusu]
* [Azure Storage REST API][Azure Storage REST API]
* [Azure depolama ekibi blogu][Azure Storage Team Blog]

Daha fazla bilgi için hello Ayrıca bkz. [Java Geliştirici Merkezi](/develop/java/).

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Azure Storage istemci SDK'sı başvurusu]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Tables: Introducing Upsert and Query Projection]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx
