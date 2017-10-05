---
title: Tablo depolama (C++) kullanma | Microsoft Docs
description: "Bir NoSQL veri deposu olan Azure Table Storage kullanarak bulutta yapılandırılmış veri depolayın."
services: storage
documentationcenter: .net
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: f191f308-e4b2-4de9-85cb-551b82b1ea7c
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: seguler
ms.openlocfilehash: d68843153921c72f6e808f62e82d3686c7e2f160
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-table-storage-from-c"></a><span data-ttu-id="093b4-103">Tablo depolama C++ içinden kullanma</span><span class="sxs-lookup"><span data-stu-id="093b4-103">How to use Table storage from C++</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="093b4-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="093b4-104">Overview</span></span>
<span data-ttu-id="093b4-105">Bu kılavuz Azure Table depolama hizmetini kullanarak yaygın senaryolar gerçekleştirmek nasıl yapacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="093b4-105">This guide will show you how to perform common scenarios by using the Azure Table storage service.</span></span> <span data-ttu-id="093b4-106">C++ ve kullanım örnekleri yazılır [C++ için Azure Storage istemci Kitaplığı](https://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="093b4-106">The samples are written in C++ and use the [Azure Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="093b4-107">Kapsamdaki senaryolar dahil **oluşturma ve bir tablo silme** ve **tablo varlıklarla çalışmaya**.</span><span class="sxs-lookup"><span data-stu-id="093b4-107">The scenarios covered include **creating and deleting a table** and **working with table entities**.</span></span>

> [!NOTE]
> <span data-ttu-id="093b4-108">Bu kılavuz, c++ sürümü 1.0.0 ve yukarıda Azure Storage istemci kitaplığı hedefler.</span><span class="sxs-lookup"><span data-stu-id="093b4-108">This guide targets the Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="093b4-109">Aracılığıyla kullanılabilir olan depolama istemci kitaplığı 2.2.0, önerilen sürümüdür [NuGet](http://www.nuget.org/packages/wastorage) veya [GitHub](https://github.com/Azure/azure-storage-cpp/).</span><span class="sxs-lookup"><span data-stu-id="093b4-109">The recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="093b4-110">C++ uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="093b4-110">Create a C++ application</span></span>
<span data-ttu-id="093b4-111">Bu kılavuzda, C++ uygulamasında çalıştırılabilir depolama özelliklerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="093b4-111">In this guide, you will use storage features that can be run within a C++ application.</span></span> <span data-ttu-id="093b4-112">Bunu yapmak için Azure Storage istemci kitaplığı C++ için yükleme ve Azure aboneliğinizde bir Azure depolama hesabı oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="093b4-112">To do so, you will need to install the Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>  

<span data-ttu-id="093b4-113">C++ için Azure Storage istemci kitaplığı yüklemek için aşağıdaki yöntemleri kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="093b4-113">To install the Azure Storage Client Library for C++, you can use the following methods:</span></span>

* <span data-ttu-id="093b4-114">**Linux:** üzerinde verilen yönergeleri izleyin [C++ Benioku için Azure Storage istemci Kitaplığı](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) sayfası.</span><span class="sxs-lookup"><span data-stu-id="093b4-114">**Linux:** Follow the instructions given on the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="093b4-115">**Windows:** Visual Studio'da sırasıyla **Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="093b4-115">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="093b4-116">Aşağıdaki komutu yazın [NuGet Paket Yöneticisi Konsolu](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) ve Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="093b4-116">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press Enter.</span></span>  
  
     <span data-ttu-id="093b4-117">Install-Package wastorage</span><span class="sxs-lookup"><span data-stu-id="093b4-117">Install-Package wastorage</span></span>

## <a name="configure-your-application-to-access-table-storage"></a><span data-ttu-id="093b4-118">Tablo depolama alanına erişmek için uygulamanızı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="093b4-118">Configure your application to access Table storage</span></span>
<span data-ttu-id="093b4-119">Azure depolama API'leri tabloları erişmek için kullanmasını istediğiniz C++ dosyanın en üstüne deyimlerini şunlar ekleyin:</span><span class="sxs-lookup"><span data-stu-id="093b4-119">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access tables:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/table.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="093b4-120">Bir Azure depolama bağlantı dizesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="093b4-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="093b4-121">Bir Azure storage istemci uç noktaları ve Veri Yönetimi Hizmetleri erişmek için kimlik bilgilerini depolamak için bir depolama bağlantı dizesi kullanır.</span><span class="sxs-lookup"><span data-stu-id="093b4-121">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="093b4-122">Bir istemci uygulaması çalışırken, aşağıdaki biçimde depolama bağlantı dizesi belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="093b4-122">When running a client application, you must provide the storage connection string in the following format.</span></span> <span data-ttu-id="093b4-123">Depolama hesap adı depolama hesabınız ve depolama erişim tuşu kullanmak [Azure Portal](https://portal.azure.com) için *AccountName* ve *AccountKey* değerleri.</span><span class="sxs-lookup"><span data-stu-id="093b4-123">Use the name of your storage account and the storage access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="093b4-124">Depolama hesapları ve erişim anahtarları hakkında daha fazla bilgi için bkz: [Azure storage hesapları hakkında](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="093b4-124">For information on storage accounts and access keys, see [About Azure storage accounts](storage-create-storage-account.md).</span></span> <span data-ttu-id="093b4-125">Bu örnek, bağlantı dizesi tutmak için statik bir alana nasıl bildirebilir gösterir:</span><span class="sxs-lookup"><span data-stu-id="093b4-125">This example shows how you can declare a static field to hold the connection string:</span></span>  

```cpp
// Define the connection string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="093b4-126">Yerel Windows tabanlı bilgisayarınızın uygulamanızı test etmek için Azure kullanabilirsiniz [depolama öykünücüsü](storage-use-emulator.md) ile yüklü [Azure SDK'sı](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="093b4-126">To test your application in your local Windows-based computer, you can use the Azure [storage emulator](storage-use-emulator.md) that is installed with the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="093b4-127">Depolama öykünücüsü Azure Blob, kuyruk ve Tablo Hizmetleri, yerel geliştirme makinenizde kullanılabilir benzetim yapan bir yardımcı programdır.</span><span class="sxs-lookup"><span data-stu-id="093b4-127">The storage emulator is a utility that simulates the Azure Blob, Queue, and Table services available on your local development machine.</span></span> <span data-ttu-id="093b4-128">Aşağıdaki örnek, yerel depolama öykünücüsü için bağlantı dizesi tutmak için statik bir alana nasıl bildirebilir gösterir:</span><span class="sxs-lookup"><span data-stu-id="093b4-128">The following example shows how you can declare a static field to hold the connection string to your local storage emulator:</span></span>  

```cpp
// Define the connection string with Azure storage emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="093b4-129">Azure storage öykünücüsü başlatmak için tıklatın **Başlat** düğmesine veya Windows tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="093b4-129">To start the Azure storage emulator, click the **Start** button or press the Windows key.</span></span> <span data-ttu-id="093b4-130">Yazmaya başlayın **Azure Storage öykünücüsü**ve ardından **Microsoft Azure Storage öykünücüsü** uygulamalar listesinden.</span><span class="sxs-lookup"><span data-stu-id="093b4-130">Begin typing **Azure Storage Emulator**, and then select **Microsoft Azure Storage Emulator** from the list of applications.</span></span>  

<span data-ttu-id="093b4-131">Aşağıdaki örnekler, bu iki yöntemden birini depolama bağlantı dizesini almak için kullanılan olduğunu varsayalım.</span><span class="sxs-lookup"><span data-stu-id="093b4-131">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="093b4-132">Bağlantı dizesi alma</span><span class="sxs-lookup"><span data-stu-id="093b4-132">Retrieve your connection string</span></span>
<span data-ttu-id="093b4-133">Kullanabileceğiniz **cloud_storage_account** depolama hesabı bilgileri temsil eden sınıf.</span><span class="sxs-lookup"><span data-stu-id="093b4-133">You can use the **cloud_storage_account** class to represent your storage account information.</span></span> <span data-ttu-id="093b4-134">Depolama bağlantı dizesi, depolama hesabı bilgilerini almak için parse yöntemi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="093b4-134">To retrieve your storage account information from the storage connection string, you can use the parse method.</span></span>

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="093b4-135">Ardından, bir başvuru almak bir **cloud_table_client** sınıfı gibi tablolar ve tablo depolama hizmet içinde depolanan varlıklar için başvuru nesneleri alabilmenizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="093b4-135">Next, get a reference to a **cloud_table_client** class, as it lets you get reference objects for tables and entities stored within the Table storage service.</span></span> <span data-ttu-id="093b4-136">Aşağıdaki kod oluşturur bir **cloud_table_client** biz alınan yukarıda depolama hesabı nesnesini kullanarak nesnesi:</span><span class="sxs-lookup"><span data-stu-id="093b4-136">The following code creates a **cloud_table_client** object by using the storage account object we retrieved above:</span></span>  

```cpp
// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();
```

## <a name="create-a-table"></a><span data-ttu-id="093b4-137">Bir tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="093b4-137">Create a table</span></span>
<span data-ttu-id="093b4-138">A **cloud_table_client** nesne tabloları ve varlıkları için başvuru nesneleri almak olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="093b4-138">A **cloud_table_client** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="093b4-139">Aşağıdaki kod oluşturur bir **cloud_table_client** nesne ve yeni bir tablo oluşturmak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="093b4-139">The following code creates a **cloud_table_client** object and uses it to create a new table.</span></span>

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);  

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference to a table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create the table if it doesn't exist.
table.create_if_not_exists();  
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="093b4-140">Tabloya bir varlık ekleme</span><span class="sxs-lookup"><span data-stu-id="093b4-140">Add an entity to a table</span></span>
<span data-ttu-id="093b4-141">Bir tabloya bir varlık eklemek için yeni bir oluşturma **table_entity** nesne ve ona geçirin **table_operation::insert_entity**.</span><span class="sxs-lookup"><span data-stu-id="093b4-141">To add an entity to a table, create a new **table_entity** object and pass it to **table_operation::insert_entity**.</span></span> <span data-ttu-id="093b4-142">Aşağıdaki kod, bölüm anahtarı olarak müşterinin adını satır anahtarını ve Soyadı kullanır.</span><span class="sxs-lookup"><span data-stu-id="093b4-142">The following code uses the customer's first name as the row key and last name as the partition key.</span></span> <span data-ttu-id="093b4-143">Birlikte, bir varlığın bölüm ve sıra anahtarı varlığı tabloda benzersiz şekilde tanımlar.</span><span class="sxs-lookup"><span data-stu-id="093b4-143">Together, an entity's partition and row key uniquely identify the entity in the table.</span></span> <span data-ttu-id="093b4-144">Aynı bölüm anahtarına sahip varlıklar farklı bölüm anahtarlarının göre daha hızlı sorgulanabilir ancak farklı bölüm anahtarlarının kullanılması daha fazla paralel işlem ölçeklenebilirlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="093b4-144">Entities with the same partition key can be queried faster than those with different partition keys, but using diverse partition keys allows for greater parallel operation scalability.</span></span> <span data-ttu-id="093b4-145">Daha fazla bilgi için bkz: [Microsoft Azure depolama performans ve ölçeklenebilirlik Yapılacaklar listesi](storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="093b4-145">For more information, see [Microsoft Azure storage performance and scalability checklist](storage-performance-checklist.md).</span></span>

<span data-ttu-id="093b4-146">Aşağıdaki kod yeni bir örneğini oluşturur **table_entity** depolanması için bazı müşteri verileri.</span><span class="sxs-lookup"><span data-stu-id="093b4-146">The following code creates a new instance of **table_entity** with some customer data to be stored.</span></span> <span data-ttu-id="093b4-147">Kodun sonraki çağrılar **table_operation::insert_entity** oluşturmak için bir **table_operation** bir tabloya bir varlık eklemek için nesne ve yeni tablo varlığı ile ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="093b4-147">The code next calls **table_operation::insert_entity** to create a **table_operation** object to insert an entity into a table, and associates the new table entity with it.</span></span> <span data-ttu-id="093b4-148">Son olarak, kod üzerinde yürütme yöntemini çağırır **cloud_table** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="093b4-148">Finally, the code calls the execute method on the **cloud_table** object.</span></span> <span data-ttu-id="093b4-149">Ve yeni **table_operation** "Kişiler" tablosuna yeni müşteri varlık eklemek için tablo hizmetine bir istek gönderir.</span><span class="sxs-lookup"><span data-stu-id="093b4-149">And the new **table_operation** sends a request to the Table service to insert the new customer entity into the "people" table.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference to a table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create the table if it doesn't exist.
table.create_if_not_exists();

// Create a new customer entity.
azure::storage::table_entity customer1(U("Harp"), U("Walter"));

azure::storage::table_entity::properties_type& properties = customer1.properties();
properties.reserve(2);
properties[U("Email")] = azure::storage::entity_property(U("Walter@contoso.com"));

properties[U("Phone")] = azure::storage::entity_property(U("425-555-0101"));

// Create the table operation that inserts the customer entity.
azure::storage::table_operation insert_operation = azure::storage::table_operation::insert_entity(customer1);

// Execute the insert operation.
azure::storage::table_result insert_result = table.execute(insert_operation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="093b4-150">Toplu işlem varlık yerleştirme</span><span class="sxs-lookup"><span data-stu-id="093b4-150">Insert a batch of entities</span></span>
<span data-ttu-id="093b4-151">Toplu işlem varlık tablo hizmeti için bir yazma işlemi ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="093b4-151">You can insert a batch of entities to the Table service in one write operation.</span></span> <span data-ttu-id="093b4-152">Aşağıdaki kod oluşturur bir **table_batch_operation** nesne ve üç ekleme işlemleri ona ekler.</span><span class="sxs-lookup"><span data-stu-id="093b4-152">The following code creates a **table_batch_operation** object, and then adds three insert operations to it.</span></span> <span data-ttu-id="093b4-153">Yeni bir varlık nesnesi oluşturarak, kendi değerlerini ayarlama ve üzerinde Insert yöntemini çağırmak her ekleme işlemi eklenen **table_batch_operation** varlığı yeni bir ekleme işlemi ile ilişkilendirmek için nesne.</span><span class="sxs-lookup"><span data-stu-id="093b4-153">Each insert operation is added by creating a new entity object, setting its values, and then calling the insert method on the **table_batch_operation** object to associate the entity with a new insert operation.</span></span> <span data-ttu-id="093b4-154">Ardından, **cloud_table.execute** işlemi yürütmek için çağrılır.</span><span class="sxs-lookup"><span data-stu-id="093b4-154">Then, **cloud_table.execute** is called to execute the operation.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define a batch operation.
azure::storage::table_batch_operation batch_operation;

// Create a customer entity and add it to the table.
azure::storage::table_entity customer1(U("Smith"), U("Jeff"));

azure::storage::table_entity::properties_type& properties1 = customer1.properties();
properties1.reserve(2);
properties1[U("Email")] = azure::storage::entity_property(U("Jeff@contoso.com"));
properties1[U("Phone")] = azure::storage::entity_property(U("425-555-0104"));

// Create another customer entity and add it to the table.
azure::storage::table_entity customer2(U("Smith"), U("Ben"));

azure::storage::table_entity::properties_type& properties2 = customer2.properties();
properties2.reserve(2);
properties2[U("Email")] = azure::storage::entity_property(U("Ben@contoso.com"));
properties2[U("Phone")] = azure::storage::entity_property(U("425-555-0102"));

// Create a third customer entity to add to the table.
azure::storage::table_entity customer3(U("Smith"), U("Denise"));

azure::storage::table_entity::properties_type& properties3 = customer3.properties();
properties3.reserve(2);
properties3[U("Email")] = azure::storage::entity_property(U("Denise@contoso.com"));
properties3[U("Phone")] = azure::storage::entity_property(U("425-555-0103"));

// Add customer entities to the batch insert operation.
batch_operation.insert_or_replace_entity(customer1);
batch_operation.insert_or_replace_entity(customer2);
batch_operation.insert_or_replace_entity(customer3);

// Execute the batch operation.
std::vector<azure::storage::table_result> results = table.execute_batch(batch_operation);
```

<span data-ttu-id="093b4-155">Toplu işlem dikkat edilecek bazı noktalar:</span><span class="sxs-lookup"><span data-stu-id="093b4-155">Some things to note on batch operations:</span></span>  

* <span data-ttu-id="093b4-156">Tek bir toplu işteki herhangi bir arada en fazla 100 Ekle, Sil, birleştirme, Değiştir, ekleme veya birleştirme ve ekleme veya değiştirme işlemleri gerçekleştirebilir.</span><span class="sxs-lookup"><span data-stu-id="093b4-156">You can perform up to 100 insert, delete, merge, replace, insert-or-merge, and insert-or-replace operations in any combination in a single batch.</span></span>  
* <span data-ttu-id="093b4-157">Toplu işlemdeki tek işlem olması durumunda toplu işlem bir alma işlemi olabilir.</span><span class="sxs-lookup"><span data-stu-id="093b4-157">A batch operation can have a retrieve operation, if it is the only operation in the batch.</span></span>  
* <span data-ttu-id="093b4-158">Tek bir toplu işlemdeki tüm varlıkların bölüm anahtarları aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="093b4-158">All entities in a single batch operation must have the same partition key.</span></span>  
* <span data-ttu-id="093b4-159">Bir toplu işlemi için 4 MB veri yükü sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="093b4-159">A batch operation is limited to a 4-MB data payload.</span></span>  

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="093b4-160">Tüm varlıkları bir bölüme alma</span><span class="sxs-lookup"><span data-stu-id="093b4-160">Retrieve all entities in a partition</span></span>
<span data-ttu-id="093b4-161">Bir bölümdeki tüm varlıklar için bir tabloyu sorgulamak için kullanın bir **table_query** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="093b4-161">To query a table for all entities in a partition, use a **table_query** object.</span></span> <span data-ttu-id="093b4-162">Aşağıdaki kod örneği, ‘Smith’in bölüm anahtarı olduğu varlıklar için bir filtre belirtir.</span><span class="sxs-lookup"><span data-stu-id="093b4-162">The following code example specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="093b4-163">Bu örnek sorgu sonuçlarındaki her varlığın alanlarını konsola yazdırır.</span><span class="sxs-lookup"><span data-stu-id="093b4-163">This example prints the fields of each entity in the query results to the console.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Construct the query operation for all customer entities where PartitionKey="Smith".
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::generate_filter_condition(U("PartitionKey"), azure::storage::query_comparison_operator::equal, U("Smith")));

// Execute the query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Print the fields for each customer.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

<span data-ttu-id="093b4-164">Bu örnekte sorgu, filtre ölçütüyle eşleşen tüm varlıkların getirir.</span><span class="sxs-lookup"><span data-stu-id="093b4-164">The query in this example brings all the entities that match the filter criteria.</span></span> <span data-ttu-id="093b4-165">Büyük tabloları varsa ve tablo varlıkları indirmek için genellikle öneririz, verilerinizi Azure storage bloblarında yerine depolar.</span><span class="sxs-lookup"><span data-stu-id="093b4-165">If you have large tables and need to download the table entities often, we recommend that you store your data in Azure storage blobs instead.</span></span>

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="093b4-166">Bir bölüme bir grup varlık alma</span><span class="sxs-lookup"><span data-stu-id="093b4-166">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="093b4-167">Bir bölümdeki tüm varlıkları sorgulamak istemiyorsanız bölüm anahtarı filtresi ile bir satır anahtarı filtresini birleştirerek bir aralık belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="093b4-167">If you don't want to query all the entities in a partition, you can specify a range by combining the partition key filter with a row key filter.</span></span> <span data-ttu-id="093b4-168">Aşağıdaki kod örneği, 'Smith' bölümünde, satır anahtarı (ad) alfabede 'E' harfinden önce gelen bir harfle başlayan tüm varlıkları almak için iki filtre kullanır, ardından sorgu sonuçlarını yazdırır.</span><span class="sxs-lookup"><span data-stu-id="093b4-168">The following code example uses two filters to get all entities in partition 'Smith' where the row key (first name) starts with a letter earlier than 'E' in the alphabet and then prints the query results.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create the table query.
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::combine_filter_conditions(
    azure::storage::table_query::generate_filter_condition(U("PartitionKey"),
    azure::storage::query_comparison_operator::equal, U("Smith")),
    azure::storage::query_logical_operator::op_and,
    azure::storage::table_query::generate_filter_condition(U("RowKey"), azure::storage::query_comparison_operator::less_than, U("E"))));

// Execute the query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Loop through the results, displaying information about the entity.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="093b4-169">Tek bir varlık alma</span><span class="sxs-lookup"><span data-stu-id="093b4-169">Retrieve a single entity</span></span>
<span data-ttu-id="093b4-170">Tek, belirli bir varlığı almak üzere bir sorgu yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="093b4-170">You can write a query to retrieve a single, specific entity.</span></span> <span data-ttu-id="093b4-171">Aşağıdaki kod **table_operation::retrieve_entity** 'Jeff Smith' müşteri belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="093b4-171">The following code uses **table_operation::retrieve_entity** to specify the customer 'Jeff Smith'.</span></span> <span data-ttu-id="093b4-172">Bu yöntem bir koleksiyon yerine yalnızca bir varlık döndürür ve döndürülen değer olarak **table_result**.</span><span class="sxs-lookup"><span data-stu-id="093b4-172">This method returns just one entity, rather than a collection, and the returned value is in **table_result**.</span></span> <span data-ttu-id="093b4-173">Bir sorguda hem bölüm hem de satır anahtarını belirtmek Tablo hizmetinden tek bir varlık almanın en hızlı yoludur.</span><span class="sxs-lookup"><span data-stu-id="093b4-173">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the Table service.</span></span>  

```cpp
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Retrieve the entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Output the entity.
azure::storage::table_entity entity = retrieve_result.entity();
const azure::storage::table_entity::properties_type& properties = entity.properties();

std::wcout << U("PartitionKey: ") << entity.partition_key() << U(", RowKey: ") << entity.row_key()
    << U(", Property1: ") << properties.at(U("Email")).string_value()
    << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
```

## <a name="replace-an-entity"></a><span data-ttu-id="093b4-174">Bir varlığı değiştirme</span><span class="sxs-lookup"><span data-stu-id="093b4-174">Replace an entity</span></span>
<span data-ttu-id="093b4-175">Bir varlığı değiştirmek için tablo hizmetinden alın, varlık nesnesini değiştirin ve değişiklikleri tablo hizmetine geri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="093b4-175">To replace an entity, retrieve it from the Table service, modify the entity object, and then save the changes back to the Table service.</span></span> <span data-ttu-id="093b4-176">Aşağıdaki kod mevcut bir müşterinin telefon numarası ve e-posta adresini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="093b4-176">The following code changes an existing customer's phone number and email address.</span></span> <span data-ttu-id="093b4-177">Çağırmak yerine **table_operation::insert_entity**, bu kod **table_operation::replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="093b4-177">Instead of calling **table_operation::insert_entity**, this code uses **table_operation::replace_entity**.</span></span> <span data-ttu-id="093b4-178">Bu, sunucu üzerindeki varlık alındığından beri değiştirilmemişse varlığın sunucu üzerinde tamamen değiştirilmesini sağlar, aksi takdirde işlem başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="093b4-178">This causes the entity to be fully replaced on the server, unless the entity on the server has changed since it was retrieved, in which case the operation will fail.</span></span> <span data-ttu-id="093b4-179">Bu işlem, uygulamanızın başka bir bileşeninin alım ve güncelleştirme arasında gerçekleştirilen bir değişikliğin yanlışlıkla üzerine yazılmasını engellemek üzere başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="093b4-179">This failure is to prevent your application from inadvertently overwriting a change made between the retrieval and update by another component of your application.</span></span> <span data-ttu-id="093b4-180">Varlığın yeniden alınması, (hala geçerli ise) değişiklikleri yapın ve ardından başka bir gerçekleştirmek için bu hatanın uygun işleme olan **table_operation::replace_entity** işlemi.</span><span class="sxs-lookup"><span data-stu-id="093b4-180">The proper handling of this failure is to retrieve the entity again, make your changes (if still valid), and then perform another **table_operation::replace_entity** operation.</span></span> <span data-ttu-id="093b4-181">Sonraki bölüm bu davranışı nasıl geçersiz kılacağınızı gösterecektir.</span><span class="sxs-lookup"><span data-stu-id="093b4-181">The next section will show you how to override this behavior.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Replace an entity.
azure::storage::table_entity entity_to_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_replace = entity_to_replace.properties();
properties_to_replace.reserve(2);

// Specify a new phone number.
properties_to_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0106"));

// Specify a new email address.
properties_to_replace[U("Email")] = azure::storage::entity_property(U("JeffS@contoso.com"));

// Create an operation to replace the entity.
azure::storage::table_operation replace_operation = azure::storage::table_operation::replace_entity(entity_to_replace);

// Submit the operation to the Table service.
azure::storage::table_result replace_result = table.execute(replace_operation);
```

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="093b4-182">Bir varlığı yerleştirme veya değiştirme</span><span class="sxs-lookup"><span data-stu-id="093b4-182">Insert-or-replace an entity</span></span>
<span data-ttu-id="093b4-183">**table_operation::replace_entity** varlık sunucudan alındığından beri değiştirilmişse işlemleri başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="093b4-183">**table_operation::replace_entity** operations will fail if the entity has been changed since it was retrieved from the server.</span></span> <span data-ttu-id="093b4-184">Ayrıca, varlığın sunucudan ilk sırada aldığınız gerekir **table_operation::replace_entity** başarılı olması için.</span><span class="sxs-lookup"><span data-stu-id="093b4-184">Furthermore, you must retrieve the entity from the server first in order for **table_operation::replace_entity** to be successful.</span></span> <span data-ttu-id="093b4-185">Bazı durumlarda, Bununla birlikte, varlık sunucuda bulunduğundan ve içinde saklı geçerli değerlerin ilgisiz olup olmadığını bilmiyorsanız — güncelleştirmeniz tümünün üzerine yazmalıdır.</span><span class="sxs-lookup"><span data-stu-id="093b4-185">Sometimes, however, you don't know if the entity exists on the server and the current values stored in it are irrelevant—your update should overwrite them all.</span></span> <span data-ttu-id="093b4-186">Bunu gerçekleştirmek için kullanacağınız bir **table_operation::insert_or_replace_entity** işlemi.</span><span class="sxs-lookup"><span data-stu-id="093b4-186">To accomplish this, you would use a **table_operation::insert_or_replace_entity** operation.</span></span> <span data-ttu-id="093b4-187">Bu işlem, varlık mevcut değilse varlığı yerleştirir, eğer varlık mevcutsa yapılan son güncelleştirmeden bağımsız olarak değiştirir.</span><span class="sxs-lookup"><span data-stu-id="093b4-187">This operation inserts the entity if it doesn't exist, or replaces it if it does, regardless of when the last update was made.</span></span> <span data-ttu-id="093b4-188">Aşağıdaki kod örneğinde Jeff Smith için müşteri varlığı hala alınabilir, ancak ardından sunucuya geri kaydedilir **table_operation::insert_or_replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="093b4-188">In the following code example, the customer entity for Jeff Smith is still retrieved, but it is then saved back to the server via **table_operation::insert_or_replace_entity**.</span></span> <span data-ttu-id="093b4-189">Varlığa alma ve güncelleştirme işlemi arasında yapılan güncelleştirmeler üzerine yazılır.</span><span class="sxs-lookup"><span data-stu-id="093b4-189">Any updates made to the entity between the retrieval and update operation will be overwritten.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Insert-or-replace an entity.
azure::storage::table_entity entity_to_insert_or_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_insert_or_replace = entity_to_insert_or_replace.properties();

properties_to_insert_or_replace.reserve(2);

// Specify a phone number.
properties_to_insert_or_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0107"));

// Specify an email address.
properties_to_insert_or_replace[U("Email")] = azure::storage::entity_property(U("Jeffsm@contoso.com"));

// Create an operation to insert-or-replace the entity.
azure::storage::table_operation insert_or_replace_operation = azure::storage::table_operation::insert_or_replace_entity(entity_to_insert_or_replace);

// Submit the operation to the Table service.
azure::storage::table_result insert_or_replace_result = table.execute(insert_or_replace_operation);
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="093b4-190">Giriş özellikleri alt kümesi sorgulama</span><span class="sxs-lookup"><span data-stu-id="093b4-190">Query a subset of entity properties</span></span>
<span data-ttu-id="093b4-191">Sorguda bir tabloya bir varlık birkaç özelliği alabilir.</span><span class="sxs-lookup"><span data-stu-id="093b4-191">A query to a table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="093b4-192">Aşağıdaki kodda sorgusu kullanan **table_query::set_select_columns** tabloda yalnızca e-posta adresleri varlıkların döndürülecek yöntemi.</span><span class="sxs-lookup"><span data-stu-id="093b4-192">The query in the following code uses the **table_query::set_select_columns** method to return only the email addresses of entities in the table.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define the query, and select only the Email property.
azure::storage::table_query query;
std::vector<utility::string_t> columns;

columns.push_back(U("Email"));
query.set_select_columns(columns);

// Execute the query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Display the results.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key();

    const azure::storage::table_entity::properties_type& properties = it->properties();
    for (auto prop_it = properties.begin(); prop_it != properties.end(); ++prop_it)
    {
        std::wcout << ", " << prop_it->first << ": " << prop_it->second.str();
    }

    std::wcout << std::endl;
}
```

> [!NOTE]
> <span data-ttu-id="093b4-193">Bir varlıktaki birkaç özelliği sorgulama tüm özellikleri alınırken değerinden daha verimli bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="093b4-193">Querying a few properties from an entity is a more efficient operation than retrieving all properties.</span></span>
> 
> 

## <a name="delete-an-entity"></a><span data-ttu-id="093b4-194">Bir varlığı silme</span><span class="sxs-lookup"><span data-stu-id="093b4-194">Delete an entity</span></span>
<span data-ttu-id="093b4-195">Bir varlık, onu aldıktan sonra kolayca silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="093b4-195">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="093b4-196">Varlık alındıktan sonra arama **table_operation::delete_entity** varlıkla silin.</span><span class="sxs-lookup"><span data-stu-id="093b4-196">Once the entity is retrieved, call **table_operation::delete_entity** with the entity to delete.</span></span> <span data-ttu-id="093b4-197">' I çağırın **cloud_table.execute** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="093b4-197">Then call the **cloud_table.execute** method.</span></span> <span data-ttu-id="093b4-198">Aşağıdaki kod alır ve bir varlık bir bölüm anahtarı "Smith" ve "Jeff" satır anahtarı ile siler.</span><span class="sxs-lookup"><span data-stu-id="093b4-198">The following code retrieves and deletes an entity with a partition key of "Smith" and a row key of "Jeff".</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation to retrieve the entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation to delete the entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit the delete operation to the Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);  
```

## <a name="delete-a-table"></a><span data-ttu-id="093b4-199">Bir tablo silme</span><span class="sxs-lookup"><span data-stu-id="093b4-199">Delete a table</span></span>
<span data-ttu-id="093b4-200">Son olarak aşağıdaki kod örneği bir depolama hesabından bir tablo siler.</span><span class="sxs-lookup"><span data-stu-id="093b4-200">Finally, the following code example deletes a table from a storage account.</span></span> <span data-ttu-id="093b4-201">Silinen bir tablo, silme işleminin ardından yeniden oluşturma için belirli bir süre kullanılamayacaktır.</span><span class="sxs-lookup"><span data-stu-id="093b4-201">A table that has been deleted will be unavailable to be re-created for a period of time following the deletion.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation to retrieve the entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation to delete the entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit the delete operation to the Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);
```

## <a name="next-steps"></a><span data-ttu-id="093b4-202">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="093b4-202">Next steps</span></span>
<span data-ttu-id="093b4-203">Table Storage öğrendiğinize göre Azure Storage hakkında daha fazla bilgi için aşağıdaki bağlantıları izleyin:</span><span class="sxs-lookup"><span data-stu-id="093b4-203">Now that you've learned the basics of table storage, follow these links to learn more about Azure Storage:</span></span>  

* <span data-ttu-id="093b4-204">[Microsoft Azure Depolama Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md), Microsoft’un Windows, macOS ve Linux üzerinde Azure Depolama verileriyle görsel olarak çalışmanızı sağlayan ücretsiz ve tek başına uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="093b4-204">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* [<span data-ttu-id="093b4-205">C++ içinden BLOB storage kullanma</span><span class="sxs-lookup"><span data-stu-id="093b4-205">How to use Blob storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="093b4-206">C++ içinden kuyruk depolama kullanma</span><span class="sxs-lookup"><span data-stu-id="093b4-206">How to use Queue storage from C++</span></span>](storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="093b4-207">C++'ta Azure Storage kaynakları listeler</span><span class="sxs-lookup"><span data-stu-id="093b4-207">List Azure Storage resources in C++</span></span>](storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="093b4-208">C++ başvurusu için depolama istemci kitaplığı</span><span class="sxs-lookup"><span data-stu-id="093b4-208">Storage Client Library for C++ reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="093b4-209">Azure Storage belgeleri</span><span class="sxs-lookup"><span data-stu-id="093b4-209">Azure Storage documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
