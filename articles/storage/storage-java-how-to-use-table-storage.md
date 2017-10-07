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
# <a name="how-toouse-table-storage-from-java"></a><span data-ttu-id="ff1d2-103">Nasıl toouse Java'dan Table storage</span><span class="sxs-lookup"><span data-stu-id="ff1d2-103">How toouse Table storage from Java</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="ff1d2-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="ff1d2-104">Overview</span></span>
<span data-ttu-id="ff1d2-105">Bu kılavuz size nasıl tooperform yaygın senaryolar kullanarak Azure Table depolama hizmeti hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-105">This guide will show you how tooperform common scenarios using hello Azure Table storage service.</span></span> <span data-ttu-id="ff1d2-106">Merhaba örnekleri Java'da yazılmış ve hello kullan [Java için Azure depolama SDK'sı][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="ff1d2-106">hello samples are written in Java and use hello [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="ff1d2-107">Merhaba kapsanan senaryolar dahil **oluşturma**, **listeleme**, ve **silme** tabloları, yanı **ekleme**,  **Sorgulama**, **değiştirme**, ve **silme** bir tabloda varlıklar.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-107">hello scenarios covered include **creating**, **listing**, and **deleting** tables, as well as **inserting**, **querying**, **modifying**, and **deleting** entities in a table.</span></span> <span data-ttu-id="ff1d2-108">Merhaba tabloları hakkında daha fazla bilgi için bkz: [sonraki adımlar](#Next-Steps) bölümü.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-108">For more information on tables, see hello [Next steps](#Next-Steps) section.</span></span>

<span data-ttu-id="ff1d2-109">Not: Bir SDK'sı Android cihazlarda Azure depolama kullanan geliştiriciler için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-109">Note: An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="ff1d2-110">Daha fazla bilgi için bkz: Merhaba [Android için Azure depolama SDK'sı][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="ff1d2-110">For more information, see hello [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="ff1d2-111">Java uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="ff1d2-111">Create a Java application</span></span>
<span data-ttu-id="ff1d2-112">Bu kılavuzda, bir Java uygulaması içinde yerel olarak veya bir web rolü veya Azure çalışan rolünde çalışan kodu çalıştırılabilir depolama özelliklerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-112">In this guide, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="ff1d2-113">toodo tooinstall ihtiyacınız olacak şekilde, Java Geliştirme Seti (JDK) hello ve Azure aboneliğinizde bir Azure depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-113">toodo so, you will need tooinstall hello Java Development Kit (JDK) and create an Azure storage account in your Azure subscription.</span></span> <span data-ttu-id="ff1d2-114">Bunu yaptıktan sonra geliştirme sisteminizde hello en düşük gereksinimleri ve hello listelenen bağımlılıkları karşılayan tooverify gerekir [Java için Azure depolama SDK'sı] [ Azure Storage SDK for Java] github'daki.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-114">Once you have done so, you will need tooverify that your development system meets hello minimum requirements and dependencies which are listed in hello [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="ff1d2-115">Sisteminiz bu gereksinimleri karşılıyorsa, karşıdan yükleme ve bu depodan sisteminizdeki Java için hello Azure depolama kitaplıkları için hello yönergeleri izleyebilir.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-115">If your system meets those requirements, you can follow hello instructions for downloading and installing hello Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="ff1d2-116">Bu görevleri tamamladıktan sonra mümkün toocreate hello örnekleri bu makalede kullanan bir Java uygulaması olacaktır.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-116">Once you have completed those tasks, you will be able toocreate a Java application which uses hello examples in this article.</span></span>

## <a name="configure-your-application-tooaccess-table-storage"></a><span data-ttu-id="ff1d2-117">Uygulama tooaccess tablo depolama alanını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ff1d2-117">Configure your application tooaccess table storage</span></span>
<span data-ttu-id="ff1d2-118">İçeri aktarma deyimlerini toohello dosyasının üst kısmında toouse Microsoft Azure depolama API'leri tooaccess tabloları istediğiniz hello Java aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="ff1d2-118">Add hello following import statements toohello top of hello Java file where you want toouse Microsoft Azure storage APIs tooaccess tables:</span></span>

```java
// Include hello following imports toouse table APIs
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.table.*;
import com.microsoft.azure.storage.table.TableQuery.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="ff1d2-119">Bir Azure depolama bağlantı dizesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="ff1d2-119">Set up an Azure storage connection string</span></span>
<span data-ttu-id="ff1d2-120">Bir Azure storage istemcisi bir depolama bağlantı dizesi toostore uç kullanır ve Veri Yönetimi Hizmetleri erişmek için kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-120">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="ff1d2-121">Bir istemci uygulamasında çalıştırırken hello depolama bağlantı dizesi biçimi aşağıdaki, hello depolama hesabınızın adını kullanarak hello olarak sağlamak ve hello listelenen hello depolama hesabı için birincil erişim anahtarını hello gerekir [Azure portal](https://portal.azure.com)hello için *AccountName* ve *AccountKey* değerleri.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-121">When running in a client application, you must provide hello storage connection string in hello following format, using hello name of your storage account and hello Primary access key for hello storage account listed in hello [Azure portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="ff1d2-122">Bu örnek, bir statik alan toohold hello bağlantı dizesini nasıl bildirebilir gösterir:</span><span class="sxs-lookup"><span data-stu-id="ff1d2-122">This example shows how you can declare a static field toohold hello connection string:</span></span>

```java
// Define hello connection-string with your values.
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="ff1d2-123">Çalışan bir uygulama içinde Microsoft Azure rolünde içinde bu dize hello hizmet yapılandırma dosyasında depolanabilir *ServiceConfiguration.cscfg*ve bir çağrı toohello ile erişilebilir  **RoleEnvironment.getConfigurationSettings** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-123">In an application running within a role in Microsoft Azure, this string can be stored in hello service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call toohello **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="ff1d2-124">Merhaba bağlantı dizesinden alma örneği bir **ayarı** adlı öğe *StorageConnectionString* hello hizmet yapılandırma dosyasında:</span><span class="sxs-lookup"><span data-stu-id="ff1d2-124">Here's an example of getting hello connection string from a **Setting** element named *StorageConnectionString* in hello service configuration file:</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="ff1d2-125">Merhaba aşağıdaki örnekleri bu iki yöntem tooget hello depolama bağlantı dizesi birini kullandığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-125">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>

## <a name="how-to-create-a-table"></a><span data-ttu-id="ff1d2-126">Nasıl yapılır: bir tablo oluştur</span><span class="sxs-lookup"><span data-stu-id="ff1d2-126">How to: Create a table</span></span>
<span data-ttu-id="ff1d2-127">A **CloudTableClient** nesne tabloları ve varlıkları için başvuru nesneleri almak olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-127">A **CloudTableClient** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="ff1d2-128">Merhaba aşağıdaki kod oluşturur bir **CloudTableClient** nesne ve yeni bir toocreate kullanan **CloudTable** tablo temsil eden nesne adında "Kişiler".</span><span class="sxs-lookup"><span data-stu-id="ff1d2-128">hello following code creates a **CloudTableClient** object and uses it toocreate a new **CloudTable** object which represents a table named "people".</span></span> <span data-ttu-id="ff1d2-129">(Not: ek yolları toocreate vardır **CloudStorageAccount** nesneleri; daha fazla bilgi için bkz: **CloudStorageAccount** hello içinde [Azure Storage istemci SDK'sı başvurusu].)</span><span class="sxs-lookup"><span data-stu-id="ff1d2-129">(Note: There are additional ways toocreate **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in hello [Azure Storage Client SDK Reference].)</span></span>

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

## <a name="how-to-list-hello-tables"></a><span data-ttu-id="ff1d2-130">Nasıl yapılır: hello Tabloları Listele</span><span class="sxs-lookup"><span data-stu-id="ff1d2-130">How to: List hello tables</span></span>
<span data-ttu-id="ff1d2-131">tooget tabloları, çağrı hello listesini **CloudTableClient.listTables()** yöntemi tooretrieve tablo adları iterable bir listesi.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-131">tooget a list of tables, call hello **CloudTableClient.listTables()** method tooretrieve an iterable list of table names.</span></span>

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

## <a name="how-to-add-an-entity-tooa-table"></a><span data-ttu-id="ff1d2-132">Nasıl yapılır: bir varlık tooa tablo ekleme</span><span class="sxs-lookup"><span data-stu-id="ff1d2-132">How to: Add an entity tooa table</span></span>
<span data-ttu-id="ff1d2-133">Varlıkları eşleme özel bir sınıf uygulama kullanarak tooJava nesneleri **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-133">Entities map tooJava objects using a custom class implementing **TableEntity**.</span></span> <span data-ttu-id="ff1d2-134">Kolaylık olması için hello **TableServiceEntity** uygulayan sınıf **TableEntity** ve toogetter ve ayarlayıcı yöntemleri adlı için kullandığı yansıma toomap özellikleri hello özellikleri.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-134">For convenience, hello **TableServiceEntity** class implements **TableEntity** and uses reflection toomap properties toogetter and setter methods named for hello properties.</span></span> <span data-ttu-id="ff1d2-135">bir varlık tooa tablosu tooadd ilk varlığınız hello özelliklerini tanımlayan bir sınıf oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-135">tooadd an entity tooa table, first create a class that defines hello properties of your entity.</span></span> <span data-ttu-id="ff1d2-136">Merhaba aşağıdaki kod hello müşterinin adını hello satır anahtarını ve Soyadı hello bölüm anahtarı olarak kullanan bir varlık sınıfı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-136">hello following code defines an entity class which uses hello customer's first name as hello row key, and last name as hello partition key.</span></span> <span data-ttu-id="ff1d2-137">Birlikte, bir varlığın bölüm ve satır anahtarı benzersiz şekilde hello varlık hello tablosundaki tanımlar.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-137">Together, an entity's partition and row key uniquely identify hello entity in hello table.</span></span> <span data-ttu-id="ff1d2-138">Aynı bölüm anahtarına farklı bölüm anahtarlarının göre daha hızlı sorgulanabilir hello olan varlık.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-138">Entities with hello same partition key can be queried faster than those with different partition keys.</span></span>

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

<span data-ttu-id="ff1d2-139">Varlıkları içeren tablo işlemleri gerektiren bir **TableOperation** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-139">Table operations involving entities require a **TableOperation** object.</span></span> <span data-ttu-id="ff1d2-140">Bu nesne ile yürütülebilir bir varlık üzerinde gerçekleştirilen hello işlemi toobe tanımlayan bir **CloudTable** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-140">This object defines hello operation toobe performed on an entity, which can be executed with a **CloudTable** object.</span></span> <span data-ttu-id="ff1d2-141">Merhaba aşağıdaki kod oluşturur hello yeni bir örneğini **CustomerEntity** depolanan bazı müşteri verileri toobe sınıfıyla.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-141">hello following code creates a new instance of hello **CustomerEntity** class with some customer data toobe stored.</span></span> <span data-ttu-id="ff1d2-142">Merhaba kod sonraki çağrılar **TableOperation.insertOrReplace** toocreate bir **TableOperation** bir tabloya tooinsert bir varlık nesnesini ve ilişkilendirilmiş bir hello yeni **CustomerEntity**onunla.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-142">hello code next calls **TableOperation.insertOrReplace** toocreate a **TableOperation** object tooinsert an entity into a table, and associates hello new **CustomerEntity** with it.</span></span> <span data-ttu-id="ff1d2-143">Son olarak, hello kod hello çağırır **yürütme** hello yöntemi **CloudTable** hello "Kişiler" tablosu ve hello yeni belirten nesnesini **TableOperation**, hangi sonra gönderir bir hello "Kişiler" tablosuna toohello depolama hizmeti tooinsert hello yeni müşteri varlığı isteyebilir veya zaten varsa hello varlık değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-143">Finally, hello code calls hello **execute** method on hello **CloudTable** object, specifying hello "people" table and hello new **TableOperation**, which then sends a request toohello storage service tooinsert hello new customer entity into hello "people" table, or replace hello entity if it already exists.</span></span>

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

## <a name="how-to-insert-a-batch-of-entities"></a><span data-ttu-id="ff1d2-144">Nasıl yapılır: bir toplu işlem varlık yerleştirme</span><span class="sxs-lookup"><span data-stu-id="ff1d2-144">How to: Insert a batch of entities</span></span>
<span data-ttu-id="ff1d2-145">Bir yazma işlemi varlıklar toohello tablo hizmeti toplu ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-145">You can insert a batch of entities toohello table service in one write operation.</span></span> <span data-ttu-id="ff1d2-146">Merhaba aşağıdaki kod oluşturur bir **TableBatchOperation** nesne sonra üç ekleme işlemleri tooit ekler.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-146">hello following code creates a **TableBatchOperation** object, then adds three insert operations tooit.</span></span> <span data-ttu-id="ff1d2-147">Her ekleme işlemi yeni bir varlık nesnesi oluşturma değerlerini ayarlama ve hello çağırma eklenir **Ekle** hello yöntemi **TableBatchOperation** tooassociate hello varlık yeni bir nesne işlem ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-147">Each insert operation is added by creating a new entity object, setting its values, and then calling hello **insert** method on hello **TableBatchOperation** object tooassociate hello entity with a new insert operation.</span></span> <span data-ttu-id="ff1d2-148">Ardından, kod çağrıları hello **yürütme** hello üzerinde **CloudTable** hello "Kişiler" tablosu ve hello belirten nesnesini **TableBatchOperation** hello toplu tablo gönderen nesnesi tek bir istekte Operations toohello depolama hizmeti.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-148">Then hello code calls **execute** on hello **CloudTable** object, specifying hello "people" table and hello **TableBatchOperation** object, which sends hello batch of table operations toohello storage service in a single request.</span></span>

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

<span data-ttu-id="ff1d2-149">Toplu işlemler ile ilgili bazı şeyleri toonote:</span><span class="sxs-lookup"><span data-stu-id="ff1d2-149">Some things toonote on batch operations:</span></span>

* <span data-ttu-id="ff1d2-150">Too100 ekleme, silme, birleştirme, Değiştir, ekleme veya birleştirme, gerçekleştirmek eklemek veya tek bir toplu işteki herhangi bir birleşimini işlemlerinde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-150">You can perform up too100 insert, delete, merge, replace, insert or merge, and insert or replace operations in any combination in a single batch.</span></span>
* <span data-ttu-id="ff1d2-151">Merhaba toplu işlemdeki tek işlem hello olması durumunda toplu işlem bir alma işlemi olabilir.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-151">A batch operation can have a retrieve operation, if it is hello only operation in hello batch.</span></span>
* <span data-ttu-id="ff1d2-152">Tek bir toplu işlem tüm varlıkları hello olmalıdır aynı bölüm anahtarı.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-152">All entities in a single batch operation must have hello same partition key.</span></span>
* <span data-ttu-id="ff1d2-153">Sınırlı tooa 4 MB veri yükü toplu işlemdir.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-153">A batch operation is limited tooa 4MB data payload.</span></span>

## <a name="how-to-retrieve-all-entities-in-a-partition"></a><span data-ttu-id="ff1d2-154">Nasıl yapılır: bir bölümdeki tüm varlıkları almak</span><span class="sxs-lookup"><span data-stu-id="ff1d2-154">How to: Retrieve all entities in a partition</span></span>
<span data-ttu-id="ff1d2-155">kullanabileceğiniz tooquery tablo varlıkları bir bölüme için bir **TableQuery**.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-155">tooquery a table for entities in a partition, you can use a **TableQuery**.</span></span> <span data-ttu-id="ff1d2-156">Çağrı **TableQuery.from** toocreate sorguda belirtilen sonuç türü döndüren belirli bir tablo üzerinde.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-156">Call **TableQuery.from** toocreate a query on a particular table that returns a specified result type.</span></span> <span data-ttu-id="ff1d2-157">Merhaba aşağıdaki kod 'Smith' hello bölüm anahtarı olduğu varlıklar için bir filtre belirtir.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-157">hello following code specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="ff1d2-158">**TableQuery.generateFilterCondition** toocreate filtreleri sorgular için bir yardımcı yöntemdir.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-158">**TableQuery.generateFilterCondition** is a helper method toocreate filters for queries.</span></span> <span data-ttu-id="ff1d2-159">Çağrı **nerede** hello tarafından döndürülen hello başvurusundaki **TableQuery.from** yöntemi tooapply hello filtre toohello sorgusu.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-159">Call **where** on hello reference returned by hello **TableQuery.from** method tooapply hello filter toohello query.</span></span> <span data-ttu-id="ff1d2-160">Ne zaman hello sorgu yürütüldüğünde çağrısı ile çok**yürütme** hello üzerinde **CloudTable** nesne döndürdüğü bir **yineleyici** hello ile **CustomerEntity**sonuç türü belirtildi.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-160">When hello query is executed with a call too**execute** on hello **CloudTable** object, it returns an **Iterator** with hello **CustomerEntity** result type specified.</span></span> <span data-ttu-id="ff1d2-161">Merhaba sonra kullanabileceğiniz **yineleyici** döndürülen bir her döngü tooconsume hello sonuçlar için.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-161">You can then use hello **Iterator** returned in a for each loop tooconsume hello results.</span></span> <span data-ttu-id="ff1d2-162">Bu kodu her varlığın hello sorgu sonuçları toohello konsolunda hello alanlarını yazdırır.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-162">This code prints hello fields of each entity in hello query results toohello console.</span></span>

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

## <a name="how-to-retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="ff1d2-163">Nasıl yapılır: bir dizi varlıkları bir bölüme alma</span><span class="sxs-lookup"><span data-stu-id="ff1d2-163">How to: Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="ff1d2-164">Tüm hello varlıkları bir bölüme tooquery istemiyorsanız, bir filtre Karşılaştırma işleçleri kullanarak bir aralığı belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-164">If you don't want tooquery all hello entities in a partition, you can specify a range by using comparison operators in a filter.</span></span> <span data-ttu-id="ff1d2-165">Aşağıdaki iki filtreler tooget "Smith" bölümündeki tüm varlıklar hello satır anahtarı (ad) too'E oluşturan bir harf ile başladığı kod birleştirir hello' hello alfabetik olarak.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-165">hello following code combines two filters tooget all entities in partition "Smith" where hello row key (first name) starts with a letter up too'E' in hello alphabet.</span></span> <span data-ttu-id="ff1d2-166">Ardından hello sorgu sonuçlarını yazdırır.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-166">Then it prints hello query results.</span></span> <span data-ttu-id="ff1d2-167">Kullanıyorsanız hello varlıklar eklenen toohello tablo hello toplu ekleme başlığına bakın, yalnızca iki varlık bu saati (Ben ve Gamze Smith); döndürülür Jeff Smith dahil değildir.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-167">If you use hello entities added toohello table in hello batch insert section of this guide, only two entities are returned this time (Ben and Denise Smith); Jeff Smith is not included.</span></span>

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

## <a name="how-to-retrieve-a-single-entity"></a><span data-ttu-id="ff1d2-168">Nasıl yapılır: tek bir varlık alma</span><span class="sxs-lookup"><span data-stu-id="ff1d2-168">How to: Retrieve a single entity</span></span>
<span data-ttu-id="ff1d2-169">Bir sorgu tooretrieve tek, belirli bir varlığı yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-169">You can write a query tooretrieve a single, specific entity.</span></span> <span data-ttu-id="ff1d2-170">Merhaba aşağıdaki kod çağrıları **TableOperation.retrieve** oluşturmak yerine bölüm anahtarını ve satır anahtar parametreleri toospecify hello müşteri "Jeff Smith" ile bir **TableQuery** ve filtreleri toodo hello kullanma aynı şey.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-170">hello following code calls **TableOperation.retrieve** with partition key and row key parameters toospecify hello customer "Jeff Smith", instead of creating a **TableQuery** and using filters toodo hello same thing.</span></span> <span data-ttu-id="ff1d2-171">Çalıştırıldığında, hello işlemi döndürür yalnızca bir varlık yerine bir koleksiyon alır.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-171">When executed, hello retrieve operation returns just one entity, rather than a collection.</span></span> <span data-ttu-id="ff1d2-172">Merhaba **getResultAsType** yöntemi çevirir hello sonuç toohello türü hello atama hedefinin bir **CustomerEntity** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-172">hello **getResultAsType** method casts hello result toohello type of hello assignment target, a **CustomerEntity** object.</span></span> <span data-ttu-id="ff1d2-173">Bu tür hello sorgu için belirtilen başlangıç türü ile uyumlu değilse, bir özel durum.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-173">If this type is not compatible with hello type specified for hello query, an exception will be thrown.</span></span> <span data-ttu-id="ff1d2-174">Bir tam bölüm ve satır anahtarını eşleşen hiçbir varlık varsa, bir null değeri döndürülür.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-174">A null value is returned if no entity has an exact partition and row key match.</span></span> <span data-ttu-id="ff1d2-175">Bir sorguda hem Bölüm hem de satır anahtarını belirterek hello en hızlı yolu tooretrieve hello tablo hizmetinden tek bir varlık olur.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-175">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello Table service.</span></span>

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

## <a name="how-to-modify-an-entity"></a><span data-ttu-id="ff1d2-176">Nasıl yapılır: bir varlık değiştirme</span><span class="sxs-lookup"><span data-stu-id="ff1d2-176">How to: Modify an entity</span></span>
<span data-ttu-id="ff1d2-177">toomodify bir varlık hello tablo hizmetinden alın, değişiklikleri toohello varlık nesnesini yapın ve hello değişiklikleri geri toohello tablo hizmeti değiştirin veya birleştirme işlemi ile Kaydet.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-177">toomodify an entity, retrieve it from hello table service, make changes toohello entity object, and save hello changes back toohello table service with a replace or merge operation.</span></span> <span data-ttu-id="ff1d2-178">Merhaba aşağıdaki kod mevcut bir müşterinin telefon numarasını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-178">hello following code changes an existing customer's phone number.</span></span> <span data-ttu-id="ff1d2-179">Çağırmak yerine **TableOperation.insert** tooinsert yaptığımız gibi bu kodu çağırır **TableOperation.replace**.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-179">Instead of calling **TableOperation.insert** like we did tooinsert, this code calls **TableOperation.replace**.</span></span> <span data-ttu-id="ff1d2-180">Merhaba **CloudTable.execute** hello tablo hizmeti yöntemini çağırır ve hello varlık değiştirilir, bu uygulama, alınan bu yana başka bir uygulama, başlangıç zamanında değiştirmediyse.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-180">hello **CloudTable.execute** method calls hello table service, and hello entity is replaced, unless another application changed it in hello time since this application retrieved it.</span></span> <span data-ttu-id="ff1d2-181">Bu durum oluştuğunda bir özel durum ve hello varlık gerekir alınan, değiştirilecek ve yeniden kaydedildi.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-181">When that happens, an exception is thrown, and hello entity must be retrieved, modified, and saved again.</span></span> <span data-ttu-id="ff1d2-182">Bu iyimser eşzamanlılık yeniden deneme deseni, bir dağıtılmış depolama sistemi yaygındır.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-182">This optimistic concurrency retry pattern is common in a distributed storage system.</span></span>

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

## <a name="how-to-query-a-subset-of-entity-properties"></a><span data-ttu-id="ff1d2-183">Nasıl yapılır: bir giriş özellikleri alt kümesi sorgulama</span><span class="sxs-lookup"><span data-stu-id="ff1d2-183">How to: Query a subset of entity properties</span></span>
<span data-ttu-id="ff1d2-184">Sorgu tooa tabloya bir varlık birkaç özelliği alabilir.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-184">A query tooa table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="ff1d2-185">Projeksiyon olarak adlandırılan bu yöntem bant genişliğini azaltır ve özellikle büyük varlıklar için sorgu performansını iyileştirebilir.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-185">This technique, called projection, reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="ff1d2-186">Merhaba koddan hello sorguda kullanan hello **seçin** yöntemi tooreturn yalnızca hello e-posta adreslerini hello tablosundaki varlıklar.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-186">hello query in hello following code uses hello **select** method tooreturn only hello email addresses of entities in hello table.</span></span> <span data-ttu-id="ff1d2-187">Merhaba sonuçları bir koleksiyona öngörülen **dize** hello Yardımı ile bir **Varlıkçözümleyicisi**, hangi tür dönüştürme hello sunucusundan döndürülen hello varlıklar üzerinde hello.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-187">hello results are projected into a collection of **String** with hello help of an **EntityResolver**, which does hello type conversion on hello entities returned from hello server.</span></span> <span data-ttu-id="ff1d2-188">İçinde projeksiyon hakkında daha fazla bilgiyi [Azure tabloları: Tanıtımı Upsert ve sorgu projeksiyon][Azure Tables: Introducing Upsert and Query Projection].</span><span class="sxs-lookup"><span data-stu-id="ff1d2-188">You can learn more about projection in [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span> <span data-ttu-id="ff1d2-189">Bu kod yalnızca bir hesap hello tablo hizmetinde kullanırken nedenle projeksiyon hello yerel depolama öykünücüsünde desteklenmez unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-189">Note that projection is not supported on hello local storage emulator, so this code runs only when using an account on hello table service.</span></span>

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

## <a name="how-to-insert-or-replace-an-entity"></a><span data-ttu-id="ff1d2-190">Nasıl yapılır: eklemek ya da bir varlığı değiştirme</span><span class="sxs-lookup"><span data-stu-id="ff1d2-190">How to: Insert or Replace an entity</span></span>
<span data-ttu-id="ff1d2-191">Genellikle tooadd bir varlık tooa tablo hello tablosunda zaten varsa bilmeden istiyor.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-191">Often you want tooadd an entity tooa table without knowing if it already exists in hello table.</span></span> <span data-ttu-id="ff1d2-192">Bir ekleme veya değiştirme işlemi toomake onu yok veya aşması durumunda bir varolan hello yerine gerekiyorsa, hello varlık ekler tek bir istek sağlar.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-192">An insert-or-replace operation allows you toomake a single request which will insert hello entity if it does not exist or replace hello existing one if it does.</span></span> <span data-ttu-id="ff1d2-193">Önceki örneklere oluşturma, hello aşağıdaki kodu ekler veya "Walter Harp için" Merhaba varlığı değiştirir.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-193">Building on prior examples, hello following code inserts or replaces hello entity for "Walter Harp".</span></span> <span data-ttu-id="ff1d2-194">Yeni bir varlık oluşturduktan sonra bu kod, hello'i çağırır **TableOperation.insertOrReplace** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-194">After creating a new entity, this code calls hello **TableOperation.insertOrReplace** method.</span></span> <span data-ttu-id="ff1d2-195">Daha sonra bu kodu çağırır **yürütme** hello üzerinde **CloudTable** nesne ile Merhaba tablo ve hello ekleme veya tablo işlemi hello parametre olarak değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-195">This code then calls **execute** on hello **CloudTable** object with hello table and hello insert or replace table operation as hello parameters.</span></span> <span data-ttu-id="ff1d2-196">bir varlığın, yalnızca bölüm tooupdate hello **TableOperation.insertOrMerge** yöntemi yerine kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-196">tooupdate only part of an entity, hello **TableOperation.insertOrMerge** method can be used instead.</span></span> <span data-ttu-id="ff1d2-197">Bu kod yalnızca bir hesap hello tablo hizmetinde kullanırken çalıştığında, ekleme veya değiştirme hello yerel depolama öykünücüsünde desteklenmez unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-197">Note that insert-or-replace is not supported on hello local storage emulator, so this code runs only when using an account on hello table service.</span></span> <span data-ttu-id="ff1d2-198">Ekleme veya değiştirme ve Ekle-veya-birleştirme bu hakkında daha fazla bilgi edinmek [Azure tabloları: Tanıtımı Upsert ve sorgu projeksiyon][Azure Tables: Introducing Upsert and Query Projection].</span><span class="sxs-lookup"><span data-stu-id="ff1d2-198">You can learn more about insert-or-replace and insert-or-merge in this [Azure Tables: Introducing Upsert and Query Projection][Azure Tables: Introducing Upsert and Query Projection].</span></span>

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

## <a name="how-to-delete-an-entity"></a><span data-ttu-id="ff1d2-199">Nasıl yapılır: bir varlığı silme</span><span class="sxs-lookup"><span data-stu-id="ff1d2-199">How to: Delete an entity</span></span>
<span data-ttu-id="ff1d2-200">Bir varlık, onu aldıktan sonra kolayca silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-200">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="ff1d2-201">Merhaba varlık alındıktan sonra arama **TableOperation.delete** hello varlık toodelete ile.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-201">Once hello entity is retrieved, call **TableOperation.delete** with hello entity toodelete.</span></span> <span data-ttu-id="ff1d2-202">' I çağırın **yürütme** hello üzerinde **CloudTable** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-202">Then call **execute** on hello **CloudTable** object.</span></span> <span data-ttu-id="ff1d2-203">koddan hello alır ve bir müşteri varlığı siler.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-203">hello following code retrieves and deletes a customer entity.</span></span>

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

## <a name="how-to-delete-a-table"></a><span data-ttu-id="ff1d2-204">Nasıl yapılır: bir tablo silme</span><span class="sxs-lookup"><span data-stu-id="ff1d2-204">How to: Delete a table</span></span>
<span data-ttu-id="ff1d2-205">Son olarak, hello aşağıdaki kod bir tablo bir depolama hesabını siler.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-205">Finally, hello following code deletes a table from a storage account.</span></span> <span data-ttu-id="ff1d2-206">Bir süre hello silmeyi, genellikle değerinden kırk saniye izleyen yeniden kullanılamaz toobe, silinmiş olan bir tablo olur.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-206">A table which has been deleted will be unavailable toobe recreated for a period of time following hello deletion, usually less than forty seconds.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ff1d2-207">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ff1d2-207">Next steps</span></span>

* <span data-ttu-id="ff1d2-208">[Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md) Windows, macOS ve Linux Azure Storage verilerle görsel olarak toowork sağlayan Microsoft boş bir tek başına uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="ff1d2-208">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="ff1d2-209">[Azure depolama için Java SDK'sı][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="ff1d2-209">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="ff1d2-210">[Azure Storage istemci SDK'sı başvurusu][Azure Storage istemci SDK'sı başvurusu]</span><span class="sxs-lookup"><span data-stu-id="ff1d2-210">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="ff1d2-211">[Azure Storage REST API][Azure Storage REST API]</span><span class="sxs-lookup"><span data-stu-id="ff1d2-211">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="ff1d2-212">[Azure depolama ekibi blogu][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="ff1d2-212">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="ff1d2-213">Daha fazla bilgi için hello Ayrıca bkz. [Java Geliştirici Merkezi](/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="ff1d2-213">For more information, see also hello [Java Developer Center](/develop/java/).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Azure Storage istemci SDK'sı başvurusu]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Tables: Introducing Upsert and Query Projection]: http://blogs.msdn.com/b/windowsazurestorage/archive/2011/09/15/windows-azure-tables-introducing-upsert-and-query-projection.aspx
