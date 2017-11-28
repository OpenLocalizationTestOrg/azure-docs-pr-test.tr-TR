---
title: aaaHow toouse Table storage (C++) | Microsoft Docs
description: "Bir NoSQL veri deposu olan Azure Table storage kullanılarak hello bulutta yapılandırılmış veri depolayın."
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jahogg
editor: tysonn
ms.assetid: f191f308-e4b2-4de9-85cb-551b82b1ea7c
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: mimig
ms.openlocfilehash: 8096fe531427ba4858f7f4cb7f664f941892d1c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-c"></a><span data-ttu-id="cf51d-103">Nasıl toouse C++ tablo depolamasından</span><span class="sxs-lookup"><span data-stu-id="cf51d-103">How toouse Table storage from C++</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="cf51d-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="cf51d-104">Overview</span></span>
<span data-ttu-id="cf51d-105">Bu kılavuz size nasıl tooperform yaygın senaryolar kullanarak Azure Table depolama hizmeti hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="cf51d-105">This guide will show you how tooperform common scenarios by using hello Azure Table storage service.</span></span> <span data-ttu-id="cf51d-106">Merhaba örnekleri C++ ile yazılmış ve hello kullan [C++ için Azure Storage istemci Kitaplığı](https://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="cf51d-106">hello samples are written in C++ and use hello [Azure Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="cf51d-107">Merhaba kapsanan senaryolar dahil **oluşturma ve bir tablo silme** ve **tablo varlıklarla çalışmaya**.</span><span class="sxs-lookup"><span data-stu-id="cf51d-107">hello scenarios covered include **creating and deleting a table** and **working with table entities**.</span></span>

> [!NOTE]
> <span data-ttu-id="cf51d-108">Bu kılavuzu hedefleri c++ sürümü 1.0.0 ve yukarıda Azure Storage istemci kitaplığı hello.</span><span class="sxs-lookup"><span data-stu-id="cf51d-108">This guide targets hello Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="cf51d-109">Merhaba önerilir sürümü aracılığıyla kullanılabilir olan depolama istemci kitaplığı 2.2.0, [NuGet](http://www.nuget.org/packages/wastorage) veya [GitHub](https://github.com/Azure/azure-storage-cpp/).</span><span class="sxs-lookup"><span data-stu-id="cf51d-109">hello recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="cf51d-110">C++ uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="cf51d-110">Create a C++ application</span></span>
<span data-ttu-id="cf51d-111">Bu kılavuzda, C++ uygulamasında çalıştırılabilir depolama özelliklerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="cf51d-111">In this guide, you will use storage features that can be run within a C++ application.</span></span> <span data-ttu-id="cf51d-112">toodo tooinstall ihtiyacınız olacak şekilde, C++ için Azure Storage istemci kitaplığı hello ve Azure aboneliğinizde bir Azure depolama hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cf51d-112">toodo so, you will need tooinstall hello Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>  

<span data-ttu-id="cf51d-113">tooinstall hello Azure Storage istemci kitaplığı C++ için hello aşağıdaki yöntemleri kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="cf51d-113">tooinstall hello Azure Storage Client Library for C++, you can use hello following methods:</span></span>

* <span data-ttu-id="cf51d-114">**Linux:** hello üzerinde verilen hello yönergeleri izleyerek [C++ Benioku için Azure Storage istemci Kitaplığı](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) sayfası.</span><span class="sxs-lookup"><span data-stu-id="cf51d-114">**Linux:** Follow hello instructions given on hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="cf51d-115">**Windows:** Visual Studio'da sırasıyla **Araçlar > NuGet Paket Yöneticisi > Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="cf51d-115">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="cf51d-116">Türü hello şu komutu hello [NuGet Paket Yöneticisi Konsolu](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) ve Enter tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="cf51d-116">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press Enter.</span></span>  
  
     <span data-ttu-id="cf51d-117">Install-Package wastorage</span><span class="sxs-lookup"><span data-stu-id="cf51d-117">Install-Package wastorage</span></span>

## <a name="configure-your-application-tooaccess-table-storage"></a><span data-ttu-id="cf51d-118">Uygulama tooaccess tablo depolama yapılandırma</span><span class="sxs-lookup"><span data-stu-id="cf51d-118">Configure your application tooaccess Table storage</span></span>
<span data-ttu-id="cf51d-119">Deyimleri toohello dosyasının üst kısmında toouse hello Azure depolama API'leri tooaccess tabloları istediğiniz hello C++ Hello şunlar ekleyin:</span><span class="sxs-lookup"><span data-stu-id="cf51d-119">Add hello following include statements toohello top of hello C++ file where you want toouse hello Azure storage APIs tooaccess tables:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/table.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="cf51d-120">Bir Azure depolama bağlantı dizesi ayarlama</span><span class="sxs-lookup"><span data-stu-id="cf51d-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="cf51d-121">Bir Azure storage istemcisi bir depolama bağlantı dizesi toostore uç kullanır ve Veri Yönetimi Hizmetleri erişmek için kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="cf51d-121">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="cf51d-122">Bir istemci uygulaması çalıştırırken hello depolama bağlantı dizesi biçimi aşağıdaki hello olarak sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="cf51d-122">When running a client application, you must provide hello storage connection string in hello following format.</span></span> <span data-ttu-id="cf51d-123">Depolama hesabı ve hello depolama erişim anahtarınızı hello depolama hesabı için kullanım hello adı listelenen hello [Azure Portal](https://portal.azure.com) hello için *AccountName* ve *AccountKey* değerler.</span><span class="sxs-lookup"><span data-stu-id="cf51d-123">Use hello name of your storage account and hello storage access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="cf51d-124">Depolama hesapları ve erişim anahtarları hakkında daha fazla bilgi için bkz: [Azure storage hesapları hakkında](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="cf51d-124">For information on storage accounts and access keys, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="cf51d-125">Bu örnek, bir statik alan toohold hello bağlantı dizesini nasıl bildirebilir gösterir:</span><span class="sxs-lookup"><span data-stu-id="cf51d-125">This example shows how you can declare a static field toohold hello connection string:</span></span>  

```cpp
// Define hello connection string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="cf51d-126">tootest uygulamanız, yerel Windows tabanlı bilgisayarınızın içinde hello Azure kullanabilirsiniz [depolama öykünücüsü](../storage/common/storage-use-emulator.md) ile Merhaba yüklü [Azure SDK'sı](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="cf51d-126">tootest your application in your local Windows-based computer, you can use hello Azure [storage emulator](../storage/common/storage-use-emulator.md) that is installed with hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="cf51d-127">Merhaba depolama öykünücüsü hello Azure Blob, kuyruk ve Tablo Hizmetleri, yerel geliştirme makinenizde kullanılabilir benzetim yapan bir yardımcı programdır.</span><span class="sxs-lookup"><span data-stu-id="cf51d-127">hello storage emulator is a utility that simulates hello Azure Blob, Queue, and Table services available on your local development machine.</span></span> <span data-ttu-id="cf51d-128">Merhaba aşağıdaki örnek bir statik alan toohold hello bağlantı dizesi tooyour yerel depolama öykünücüsü nasıl bildirebilir gösterir:</span><span class="sxs-lookup"><span data-stu-id="cf51d-128">hello following example shows how you can declare a static field toohold hello connection string tooyour local storage emulator:</span></span>  

```cpp
// Define hello connection string with Azure storage emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="cf51d-129">toostart Azure storage öykünücüsü Merhaba, hello tıklatın **Başlat** düğmesini veya tuşuna hello Windows anahtarı.</span><span class="sxs-lookup"><span data-stu-id="cf51d-129">toostart hello Azure storage emulator, click hello **Start** button or press hello Windows key.</span></span> <span data-ttu-id="cf51d-130">Yazmaya başlayın **Azure Storage öykünücüsü**ve ardından **Microsoft Azure Storage öykünücüsü** uygulamaları hello listesinden.</span><span class="sxs-lookup"><span data-stu-id="cf51d-130">Begin typing **Azure Storage Emulator**, and then select **Microsoft Azure Storage Emulator** from hello list of applications.</span></span>  

<span data-ttu-id="cf51d-131">Merhaba aşağıdaki örnekleri bu iki yöntem tooget hello depolama bağlantı dizesi birini kullandığınızı varsayar.</span><span class="sxs-lookup"><span data-stu-id="cf51d-131">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="cf51d-132">Bağlantı dizesi alma</span><span class="sxs-lookup"><span data-stu-id="cf51d-132">Retrieve your connection string</span></span>
<span data-ttu-id="cf51d-133">Merhaba kullanabilirsiniz **cloud_storage_account** toorepresent depolama hesap bilgilerinizi sınıfı.</span><span class="sxs-lookup"><span data-stu-id="cf51d-133">You can use hello **cloud_storage_account** class toorepresent your storage account information.</span></span> <span data-ttu-id="cf51d-134">tooretrieve depolama hesap bilgileri hello depolama bağlantı dizesinden, hello parse yöntemi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cf51d-134">tooretrieve your storage account information from hello storage connection string, you can use hello parse method.</span></span>

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="cf51d-135">Ardından, bir başvuru tooa almak **cloud_table_client** tablolar için başvuru nesneleri alabilmenizi sağlar ve varlıkları tablo depolama hizmeti hello içinde depolanan sınıfı.</span><span class="sxs-lookup"><span data-stu-id="cf51d-135">Next, get a reference tooa **cloud_table_client** class, as it lets you get reference objects for tables and entities stored within hello Table storage service.</span></span> <span data-ttu-id="cf51d-136">Merhaba aşağıdaki kod oluşturur bir **cloud_table_client** biz alınan yukarıda hello depolama hesabı nesnesini kullanarak nesnesi:</span><span class="sxs-lookup"><span data-stu-id="cf51d-136">hello following code creates a **cloud_table_client** object by using hello storage account object we retrieved above:</span></span>  

```cpp
// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();
```

## <a name="create-a-table"></a><span data-ttu-id="cf51d-137">Bir tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="cf51d-137">Create a table</span></span>
<span data-ttu-id="cf51d-138">A **cloud_table_client** nesne tabloları ve varlıkları için başvuru nesneleri almak olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="cf51d-138">A **cloud_table_client** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="cf51d-139">Merhaba aşağıdaki kod oluşturur bir **cloud_table_client** nesne ve toocreate yeni bir tablo kullanır.</span><span class="sxs-lookup"><span data-stu-id="cf51d-139">hello following code creates a **cloud_table_client** object and uses it toocreate a new table.</span></span>

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);  

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();  
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="cf51d-140">Bir varlık tooa tablo ekleme</span><span class="sxs-lookup"><span data-stu-id="cf51d-140">Add an entity tooa table</span></span>
<span data-ttu-id="cf51d-141">tooadd bir varlık tooa tablo oluşturma yeni bir **table_entity** nesne ve çok geçirin**table_operation::insert_entity**.</span><span class="sxs-lookup"><span data-stu-id="cf51d-141">tooadd an entity tooa table, create a new **table_entity** object and pass it too**table_operation::insert_entity**.</span></span> <span data-ttu-id="cf51d-142">Merhaba aşağıdaki kod hello müşterinin adını hello satır anahtarını ve Soyadı hello bölüm anahtarı olarak kullanır.</span><span class="sxs-lookup"><span data-stu-id="cf51d-142">hello following code uses hello customer's first name as hello row key and last name as hello partition key.</span></span> <span data-ttu-id="cf51d-143">Birlikte, bir varlığın bölüm ve satır anahtarı benzersiz şekilde hello varlık hello tablosundaki tanımlar.</span><span class="sxs-lookup"><span data-stu-id="cf51d-143">Together, an entity's partition and row key uniquely identify hello entity in hello table.</span></span> <span data-ttu-id="cf51d-144">Anahtarları aynı bölüm anahtarına farklı olanlar daha hızlı sorgulanabilir hello varlıklarıyla bölüm, ancak farklı bölüm anahtarlarının kullanılması daha fazla paralel işlem ölçeklenebilirlik sağlar.</span><span class="sxs-lookup"><span data-stu-id="cf51d-144">Entities with hello same partition key can be queried faster than those with different partition keys, but using diverse partition keys allows for greater parallel operation scalability.</span></span> <span data-ttu-id="cf51d-145">Daha fazla bilgi için bkz: [Microsoft Azure depolama performans ve ölçeklenebilirlik Yapılacaklar listesi](../storage/common/storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="cf51d-145">For more information, see [Microsoft Azure storage performance and scalability checklist](../storage/common/storage-performance-checklist.md).</span></span>

<span data-ttu-id="cf51d-146">Merhaba aşağıdaki kod oluşturur Yeni bir örneğini **table_entity** depolanan bazı müşteri verileri toobe ile.</span><span class="sxs-lookup"><span data-stu-id="cf51d-146">hello following code creates a new instance of **table_entity** with some customer data toobe stored.</span></span> <span data-ttu-id="cf51d-147">Merhaba kod sonraki çağrılar **table_operation::insert_entity** toocreate bir **table_operation** bir tabloya tooinsert bir varlık nesnesini ve ilişkilendirilmiş bir hello birlikte yeni bir tablo varlık.</span><span class="sxs-lookup"><span data-stu-id="cf51d-147">hello code next calls **table_operation::insert_entity** toocreate a **table_operation** object tooinsert an entity into a table, and associates hello new table entity with it.</span></span> <span data-ttu-id="cf51d-148">Son olarak, hello kod çağrıları Hello yürütme yöntemi hello üzerinde **cloud_table** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="cf51d-148">Finally, hello code calls hello execute method on hello **cloud_table** object.</span></span> <span data-ttu-id="cf51d-149">Ve hello yeni **table_operation** hello "Kişiler" tablosuna isteği toohello tablo hizmeti tooinsert hello yeni müşteri varlık gönderir.</span><span class="sxs-lookup"><span data-stu-id="cf51d-149">And hello new **table_operation** sends a request toohello Table service tooinsert hello new customer entity into hello "people" table.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();

// Create a new customer entity.
azure::storage::table_entity customer1(U("Harp"), U("Walter"));

azure::storage::table_entity::properties_type& properties = customer1.properties();
properties.reserve(2);
properties[U("Email")] = azure::storage::entity_property(U("Walter@contoso.com"));

properties[U("Phone")] = azure::storage::entity_property(U("425-555-0101"));

// Create hello table operation that inserts hello customer entity.
azure::storage::table_operation insert_operation = azure::storage::table_operation::insert_entity(customer1);

// Execute hello insert operation.
azure::storage::table_result insert_result = table.execute(insert_operation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="cf51d-150">Toplu işlem varlık yerleştirme</span><span class="sxs-lookup"><span data-stu-id="cf51d-150">Insert a batch of entities</span></span>
<span data-ttu-id="cf51d-151">Bir yazma işlemi varlıklar toohello tablo hizmeti toplu ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cf51d-151">You can insert a batch of entities toohello Table service in one write operation.</span></span> <span data-ttu-id="cf51d-152">Merhaba aşağıdaki kod oluşturur bir **table_batch_operation** nesne ve üç ekleme işlemleri tooit ekler.</span><span class="sxs-lookup"><span data-stu-id="cf51d-152">hello following code creates a **table_batch_operation** object, and then adds three insert operations tooit.</span></span> <span data-ttu-id="cf51d-153">Her ekleme işlemi, değerlerinin ayarı yeni bir varlık nesnesi oluşturarak eklenir ve hello çağırma hello yöntemi Ekle **table_batch_operation** sahip yeni bir nesne tooassociate hello varlık ekleme işlemi.</span><span class="sxs-lookup"><span data-stu-id="cf51d-153">Each insert operation is added by creating a new entity object, setting its values, and then calling hello insert method on hello **table_batch_operation** object tooassociate hello entity with a new insert operation.</span></span> <span data-ttu-id="cf51d-154">Ardından, **cloud_table.execute** tooexecute hello işlem çağrılır.</span><span class="sxs-lookup"><span data-stu-id="cf51d-154">Then, **cloud_table.execute** is called tooexecute hello operation.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define a batch operation.
azure::storage::table_batch_operation batch_operation;

// Create a customer entity and add it toohello table.
azure::storage::table_entity customer1(U("Smith"), U("Jeff"));

azure::storage::table_entity::properties_type& properties1 = customer1.properties();
properties1.reserve(2);
properties1[U("Email")] = azure::storage::entity_property(U("Jeff@contoso.com"));
properties1[U("Phone")] = azure::storage::entity_property(U("425-555-0104"));

// Create another customer entity and add it toohello table.
azure::storage::table_entity customer2(U("Smith"), U("Ben"));

azure::storage::table_entity::properties_type& properties2 = customer2.properties();
properties2.reserve(2);
properties2[U("Email")] = azure::storage::entity_property(U("Ben@contoso.com"));
properties2[U("Phone")] = azure::storage::entity_property(U("425-555-0102"));

// Create a third customer entity tooadd toohello table.
azure::storage::table_entity customer3(U("Smith"), U("Denise"));

azure::storage::table_entity::properties_type& properties3 = customer3.properties();
properties3.reserve(2);
properties3[U("Email")] = azure::storage::entity_property(U("Denise@contoso.com"));
properties3[U("Phone")] = azure::storage::entity_property(U("425-555-0103"));

// Add customer entities toohello batch insert operation.
batch_operation.insert_or_replace_entity(customer1);
batch_operation.insert_or_replace_entity(customer2);
batch_operation.insert_or_replace_entity(customer3);

// Execute hello batch operation.
std::vector<azure::storage::table_result> results = table.execute_batch(batch_operation);
```

<span data-ttu-id="cf51d-155">Toplu işlemler ile ilgili bazı şeyleri toonote:</span><span class="sxs-lookup"><span data-stu-id="cf51d-155">Some things toonote on batch operations:</span></span>  

* <span data-ttu-id="cf51d-156">Gerçekleştirebileceğiniz too100 ekleme, silme, birleştirme, Değiştir, tek bir toplu işteki herhangi bir birleşimini ekleme veya birleştirme ve ekleme veya değiştirme işlemleri.</span><span class="sxs-lookup"><span data-stu-id="cf51d-156">You can perform up too100 insert, delete, merge, replace, insert-or-merge, and insert-or-replace operations in any combination in a single batch.</span></span>  
* <span data-ttu-id="cf51d-157">Merhaba toplu işlemdeki tek işlem hello olması durumunda toplu işlem bir alma işlemi olabilir.</span><span class="sxs-lookup"><span data-stu-id="cf51d-157">A batch operation can have a retrieve operation, if it is hello only operation in hello batch.</span></span>  
* <span data-ttu-id="cf51d-158">Tek bir toplu işlem tüm varlıkları hello olmalıdır aynı bölüm anahtarı.</span><span class="sxs-lookup"><span data-stu-id="cf51d-158">All entities in a single batch operation must have hello same partition key.</span></span>  
* <span data-ttu-id="cf51d-159">Sınırlı tooa 4 MB veri yükü toplu işlemdir.</span><span class="sxs-lookup"><span data-stu-id="cf51d-159">A batch operation is limited tooa 4-MB data payload.</span></span>  

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="cf51d-160">Tüm varlıkları bir bölüme alma</span><span class="sxs-lookup"><span data-stu-id="cf51d-160">Retrieve all entities in a partition</span></span>
<span data-ttu-id="cf51d-161">tooquery kullanımı bir bölümdeki tüm varlıklar için bir tablo bir **table_query** nesnesi.</span><span class="sxs-lookup"><span data-stu-id="cf51d-161">tooquery a table for all entities in a partition, use a **table_query** object.</span></span> <span data-ttu-id="cf51d-162">Merhaba aşağıdaki kod örneğinde 'Smith' hello bölüm anahtarı olduğu varlıklar için bir filtre belirtir.</span><span class="sxs-lookup"><span data-stu-id="cf51d-162">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="cf51d-163">Bu örnekte her varlığın hello sorgu sonuçları toohello konsolunda hello alanlarını yazdırır.</span><span class="sxs-lookup"><span data-stu-id="cf51d-163">This example prints hello fields of each entity in hello query results toohello console.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Construct hello query operation for all customer entities where PartitionKey="Smith".
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::generate_filter_condition(U("PartitionKey"), azure::storage::query_comparison_operator::equal, U("Smith")));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Print hello fields for each customer.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

<span data-ttu-id="cf51d-164">Bu örnekte Hello sorgu hello filtre ölçütüyle eşleşen tüm hello varlıklar getirir.</span><span class="sxs-lookup"><span data-stu-id="cf51d-164">hello query in this example brings all hello entities that match hello filter criteria.</span></span> <span data-ttu-id="cf51d-165">Büyük tablolar ve toodownload hello tablo varlıkları genellikle ihtiyacınız varsa, verilerinizi Azure storage blobları bunun yerine saklamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="cf51d-165">If you have large tables and need toodownload hello table entities often, we recommend that you store your data in Azure storage blobs instead.</span></span>

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="cf51d-166">Bir bölüme bir grup varlık alma</span><span class="sxs-lookup"><span data-stu-id="cf51d-166">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="cf51d-167">Tüm hello varlıkları bir bölüme tooquery istemiyorsanız, hello bölüm anahtarı Filtresi ile bir satır anahtarı filtresini birleştirerek bir aralık belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cf51d-167">If you don't want tooquery all hello entities in a partition, you can specify a range by combining hello partition key filter with a row key filter.</span></span> <span data-ttu-id="cf51d-168">Merhaba aşağıdaki kod örneği iki filtreleri tooget tüm varlıklar 'hello satır anahtarı (ad) burada hello alfabede 'E' den önceki bir harfle başlayan ve hello sorgu sonuçlarını yazdırır Smith' bölümünde kullanır.</span><span class="sxs-lookup"><span data-stu-id="cf51d-168">hello following code example uses two filters tooget all entities in partition 'Smith' where hello row key (first name) starts with a letter earlier than 'E' in hello alphabet and then prints hello query results.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table query.
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::combine_filter_conditions(
    azure::storage::table_query::generate_filter_condition(U("PartitionKey"),
    azure::storage::query_comparison_operator::equal, U("Smith")),
    azure::storage::query_logical_operator::op_and,
    azure::storage::table_query::generate_filter_condition(U("RowKey"), azure::storage::query_comparison_operator::less_than, U("E"))));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Loop through hello results, displaying information about hello entity.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="cf51d-169">Tek bir varlık alma</span><span class="sxs-lookup"><span data-stu-id="cf51d-169">Retrieve a single entity</span></span>
<span data-ttu-id="cf51d-170">Bir sorgu tooretrieve tek, belirli bir varlığı yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cf51d-170">You can write a query tooretrieve a single, specific entity.</span></span> <span data-ttu-id="cf51d-171">Merhaba aşağıdaki kod kullanır **table_operation::retrieve_entity** toospecify hello Müşteri 'Jeff Smith'.</span><span class="sxs-lookup"><span data-stu-id="cf51d-171">hello following code uses **table_operation::retrieve_entity** toospecify hello customer 'Jeff Smith'.</span></span> <span data-ttu-id="cf51d-172">Bu yöntem bir koleksiyon yerine yalnızca bir varlık döndürür ve hello döndürülen değer olarak **table_result**.</span><span class="sxs-lookup"><span data-stu-id="cf51d-172">This method returns just one entity, rather than a collection, and hello returned value is in **table_result**.</span></span> <span data-ttu-id="cf51d-173">Bir sorguda hem Bölüm hem de satır anahtarını belirterek hello en hızlı yolu tooretrieve hello tablo hizmetinden tek bir varlık olur.</span><span class="sxs-lookup"><span data-stu-id="cf51d-173">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello Table service.</span></span>  

```cpp
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Output hello entity.
azure::storage::table_entity entity = retrieve_result.entity();
const azure::storage::table_entity::properties_type& properties = entity.properties();

std::wcout << U("PartitionKey: ") << entity.partition_key() << U(", RowKey: ") << entity.row_key()
    << U(", Property1: ") << properties.at(U("Email")).string_value()
    << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
```

## <a name="replace-an-entity"></a><span data-ttu-id="cf51d-174">Bir varlığı değiştirme</span><span class="sxs-lookup"><span data-stu-id="cf51d-174">Replace an entity</span></span>
<span data-ttu-id="cf51d-175">bir varlık tooreplace hello tablo hizmetinden alın, hello varlık nesnesini değiştirin ve ardından hello Değişiklikleri Kaydet toohello tablo hizmeti yeniden.</span><span class="sxs-lookup"><span data-stu-id="cf51d-175">tooreplace an entity, retrieve it from hello Table service, modify hello entity object, and then save hello changes back toohello Table service.</span></span> <span data-ttu-id="cf51d-176">Merhaba aşağıdaki kod mevcut bir müşterinin telefon numarası ve e-posta adresini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="cf51d-176">hello following code changes an existing customer's phone number and email address.</span></span> <span data-ttu-id="cf51d-177">Çağırmak yerine **table_operation::insert_entity**, bu kod **table_operation::replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="cf51d-177">Instead of calling **table_operation::insert_entity**, this code uses **table_operation::replace_entity**.</span></span> <span data-ttu-id="cf51d-178">Bu, hello işlemi başarısız olur; bu durumda alındığından beri hello varlık hello sunucuda değiştirilmediği sürece bu tam olarak hello sunucuda yerini hello varlık toobe neden olur.</span><span class="sxs-lookup"><span data-stu-id="cf51d-178">This causes hello entity toobe fully replaced on hello server, unless hello entity on hello server has changed since it was retrieved, in which case hello operation will fail.</span></span> <span data-ttu-id="cf51d-179">Uygulamanızı bir değişikliğin yanlışlıkla üzerine yazılmasını arasında alma hello ve uygulamanızın başka bir bileşen tarafından güncelleştirme yapılan tooprevent hatasıdır.</span><span class="sxs-lookup"><span data-stu-id="cf51d-179">This failure is tooprevent your application from inadvertently overwriting a change made between hello retrieval and update by another component of your application.</span></span> <span data-ttu-id="cf51d-180">Merhaba bu hatanın uygun işleme tooretrieve hello yeniden varlıktır, (hala geçerli ise) değişiklikleri yapın ve ardından başka bir gerçekleştirin **table_operation::replace_entity** işlemi.</span><span class="sxs-lookup"><span data-stu-id="cf51d-180">hello proper handling of this failure is tooretrieve hello entity again, make your changes (if still valid), and then perform another **table_operation::replace_entity** operation.</span></span> <span data-ttu-id="cf51d-181">Merhaba sonraki bölümde gösterir, nasıl toooverride bu davranışı.</span><span class="sxs-lookup"><span data-stu-id="cf51d-181">hello next section will show you how toooverride this behavior.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Replace an entity.
azure::storage::table_entity entity_to_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_replace = entity_to_replace.properties();
properties_to_replace.reserve(2);

// Specify a new phone number.
properties_to_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0106"));

// Specify a new email address.
properties_to_replace[U("Email")] = azure::storage::entity_property(U("JeffS@contoso.com"));

// Create an operation tooreplace hello entity.
azure::storage::table_operation replace_operation = azure::storage::table_operation::replace_entity(entity_to_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result replace_result = table.execute(replace_operation);
```

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="cf51d-182">Bir varlığı yerleştirme veya değiştirme</span><span class="sxs-lookup"><span data-stu-id="cf51d-182">Insert-or-replace an entity</span></span>
<span data-ttu-id="cf51d-183">**table_operation::replace_entity** hello varlık hello sunucudan alındığından beri değiştirilmişse işlemleri başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="cf51d-183">**table_operation::replace_entity** operations will fail if hello entity has been changed since it was retrieved from hello server.</span></span> <span data-ttu-id="cf51d-184">Ayrıca, ilk sırada hello sunucusundan hello varlık almanız gerekir **table_operation::replace_entity** toobe başarılı.</span><span class="sxs-lookup"><span data-stu-id="cf51d-184">Furthermore, you must retrieve hello entity from hello server first in order for **table_operation::replace_entity** toobe successful.</span></span> <span data-ttu-id="cf51d-185">Bazı durumlarda, ancak hello varlık hello sunucuda var ve depolanan hello geçerli değerler ilgisiz tanımadığınız — güncelleştirmeniz tümünün üzerine yazmalıdır.</span><span class="sxs-lookup"><span data-stu-id="cf51d-185">Sometimes, however, you don't know if hello entity exists on hello server and hello current values stored in it are irrelevant—your update should overwrite them all.</span></span> <span data-ttu-id="cf51d-186">tooaccomplish Bu, kullanacağınız bir **table_operation::insert_or_replace_entity** işlemi.</span><span class="sxs-lookup"><span data-stu-id="cf51d-186">tooaccomplish this, you would use a **table_operation::insert_or_replace_entity** operation.</span></span> <span data-ttu-id="cf51d-187">Bu işlem yok veya bu zaman hello yapılan son güncelleştirmeden bağımsız olarak, varsa yerini hello varlık ekler.</span><span class="sxs-lookup"><span data-stu-id="cf51d-187">This operation inserts hello entity if it doesn't exist, or replaces it if it does, regardless of when hello last update was made.</span></span> <span data-ttu-id="cf51d-188">Aşağıdaki kod örneğine hello hello Jeff Smith için müşteri varlığı hala alınabilir, ancak daha sonra geri toohello sunucu aracılığıyla kaydedilir **table_operation::insert_or_replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="cf51d-188">In hello following code example, hello customer entity for Jeff Smith is still retrieved, but it is then saved back toohello server via **table_operation::insert_or_replace_entity**.</span></span> <span data-ttu-id="cf51d-189">Toohello varlık hello alma ve güncelleştirme işlemi arasında yapılan güncelleştirmeler üzerine yazılır.</span><span class="sxs-lookup"><span data-stu-id="cf51d-189">Any updates made toohello entity between hello retrieval and update operation will be overwritten.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Insert-or-replace an entity.
azure::storage::table_entity entity_to_insert_or_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_insert_or_replace = entity_to_insert_or_replace.properties();

properties_to_insert_or_replace.reserve(2);

// Specify a phone number.
properties_to_insert_or_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0107"));

// Specify an email address.
properties_to_insert_or_replace[U("Email")] = azure::storage::entity_property(U("Jeffsm@contoso.com"));

// Create an operation tooinsert-or-replace hello entity.
azure::storage::table_operation insert_or_replace_operation = azure::storage::table_operation::insert_or_replace_entity(entity_to_insert_or_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result insert_or_replace_result = table.execute(insert_or_replace_operation);
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="cf51d-190">Giriş özellikleri alt kümesi sorgulama</span><span class="sxs-lookup"><span data-stu-id="cf51d-190">Query a subset of entity properties</span></span>
<span data-ttu-id="cf51d-191">Sorgu tooa tabloya bir varlık birkaç özelliği alabilir.</span><span class="sxs-lookup"><span data-stu-id="cf51d-191">A query tooa table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="cf51d-192">Merhaba koddan hello sorguda kullanan hello **table_query::set_select_columns** yöntemi tooreturn yalnızca hello e-posta adreslerini hello tablosundaki varlıklar.</span><span class="sxs-lookup"><span data-stu-id="cf51d-192">hello query in hello following code uses hello **table_query::set_select_columns** method tooreturn only hello email addresses of entities in hello table.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define hello query, and select only hello Email property.
azure::storage::table_query query;
std::vector<utility::string_t> columns;

columns.push_back(U("Email"));
query.set_select_columns(columns);

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Display hello results.
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
> <span data-ttu-id="cf51d-193">Bir varlıktaki birkaç özelliği sorgulama tüm özellikleri alınırken değerinden daha verimli bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="cf51d-193">Querying a few properties from an entity is a more efficient operation than retrieving all properties.</span></span>
> 
> 

## <a name="delete-an-entity"></a><span data-ttu-id="cf51d-194">Bir varlığı silme</span><span class="sxs-lookup"><span data-stu-id="cf51d-194">Delete an entity</span></span>
<span data-ttu-id="cf51d-195">Bir varlık, onu aldıktan sonra kolayca silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cf51d-195">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="cf51d-196">Merhaba varlık alındıktan sonra arama **table_operation::delete_entity** hello varlık toodelete ile.</span><span class="sxs-lookup"><span data-stu-id="cf51d-196">Once hello entity is retrieved, call **table_operation::delete_entity** with hello entity toodelete.</span></span> <span data-ttu-id="cf51d-197">Merhaba çağrısı **cloud_table.execute** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="cf51d-197">Then call hello **cloud_table.execute** method.</span></span> <span data-ttu-id="cf51d-198">Merhaba aşağıdaki kodu alır ve bir varlık bir bölüm anahtarı "Smith" ve "Jeff" satır anahtarı ile siler.</span><span class="sxs-lookup"><span data-stu-id="cf51d-198">hello following code retrieves and deletes an entity with a partition key of "Smith" and a row key of "Jeff".</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);  
```

## <a name="delete-a-table"></a><span data-ttu-id="cf51d-199">Bir tablo silme</span><span class="sxs-lookup"><span data-stu-id="cf51d-199">Delete a table</span></span>
<span data-ttu-id="cf51d-200">Son olarak, aşağıdaki kod örneğine hello bir depolama hesabından bir tablo siler.</span><span class="sxs-lookup"><span data-stu-id="cf51d-200">Finally, hello following code example deletes a table from a storage account.</span></span> <span data-ttu-id="cf51d-201">Silinmiş bir tablo bir süre hello silmeyi izleyen yeniden oluşturulacak kullanılamaz toobe olacaktır.</span><span class="sxs-lookup"><span data-stu-id="cf51d-201">A table that has been deleted will be unavailable toobe re-created for a period of time following hello deletion.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);
```

## <a name="next-steps"></a><span data-ttu-id="cf51d-202">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="cf51d-202">Next steps</span></span>
<span data-ttu-id="cf51d-203">Table Storage hello temel bilgileri öğrendiğinize göre Azure Storage hakkında daha fazla bu bağlantılar toolearn izleyin:</span><span class="sxs-lookup"><span data-stu-id="cf51d-203">Now that you've learned hello basics of table storage, follow these links toolearn more about Azure Storage:</span></span>  

* <span data-ttu-id="cf51d-204">[Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md) Windows, macOS ve Linux Azure Storage verilerle görsel olarak toowork sağlayan Microsoft boş bir tek başına uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="cf51d-204">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* [<span data-ttu-id="cf51d-205">Nasıl toouse Blob depolama alanından C++</span><span class="sxs-lookup"><span data-stu-id="cf51d-205">How toouse Blob storage from C++</span></span>](../storage/blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="cf51d-206">Nasıl toouse C++ içinden kuyruk depolama</span><span class="sxs-lookup"><span data-stu-id="cf51d-206">How toouse Queue storage from C++</span></span>](../storage/queues/storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="cf51d-207">C++'ta Azure Storage kaynakları listeler</span><span class="sxs-lookup"><span data-stu-id="cf51d-207">List Azure Storage resources in C++</span></span>](../storage/common/storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="cf51d-208">C++ başvurusu için depolama istemci kitaplığı</span><span class="sxs-lookup"><span data-stu-id="cf51d-208">Storage Client Library for C++ reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="cf51d-209">Azure Storage belgeleri</span><span class="sxs-lookup"><span data-stu-id="cf51d-209">Azure Storage documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
