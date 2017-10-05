---
title: Azure Table Storage ruby'den kullanma | Microsoft Docs
description: "Bir NoSQL veri deposu olan Azure Table Storage kullanarak bulutta yapılandırılmış veri depolayın."
services: cosmos-db
documentationcenter: ruby
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 047cd9ff-17d3-4c15-9284-1b5cc61a3224
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 372bc89f75ad4730f0defbf9d6f9f041ae5ce1bf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-azure-table-storage-from-ruby"></a><span data-ttu-id="60289-103">Ruby'den Azure Table Storage kullanma</span><span class="sxs-lookup"><span data-stu-id="60289-103">How to use Azure Table Storage from Ruby</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="60289-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="60289-104">Overview</span></span>
<span data-ttu-id="60289-105">Bu kılavuz Azure Table hizmetini kullanarak yaygın senaryolar gerçekleştirme gösterir.</span><span class="sxs-lookup"><span data-stu-id="60289-105">This guide shows you how to perform common scenarios using the Azure Table service.</span></span> <span data-ttu-id="60289-106">Örnekler, Ruby API kullanılarak yazılır.</span><span class="sxs-lookup"><span data-stu-id="60289-106">The samples are written using the Ruby API.</span></span> <span data-ttu-id="60289-107">Kapsamdaki senaryolar dahil **oluşturma ve bir tablo, ekleme ve bir tablo varlıkları sorgulama**.</span><span class="sxs-lookup"><span data-stu-id="60289-107">The scenarios covered include **creating and deleting a table, inserting and querying entities in a table**.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="60289-108">Ruby uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="60289-108">Create a Ruby application</span></span>
<span data-ttu-id="60289-109">Yönergeler için Ruby uygulaması oluşturma, bkz: [Azure VM'de rayları Web uygulaması üzerinde Söyleniş](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="60289-109">For instructions how to create a Ruby application, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="60289-110">Depolama alanına erişmek için uygulamanızı yapılandırın</span><span class="sxs-lookup"><span data-stu-id="60289-110">Configure your application to access Storage</span></span>
<span data-ttu-id="60289-111">Azure Storage kullanmak için indirme ve depolama REST Hizmetleri ile iletişim kuran bir dizi kolaylık içeren Söyleniş azure paketini kullanmak gerekir.</span><span class="sxs-lookup"><span data-stu-id="60289-111">To use Azure Storage, you need to download and use the Ruby azure package which includes a set of convenience libraries that communicate with the Storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="60289-112">Paket elde etmek için RubyGems kullanın</span><span class="sxs-lookup"><span data-stu-id="60289-112">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="60289-113">Bir komut satırı arabirimi gibi kullandığınız **PowerShell** (Windows), **Terminal** (Mac) veya **Bash** (UNIX).</span><span class="sxs-lookup"><span data-stu-id="60289-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="60289-114">Tür **gem yükleme azure** gem ve bağımlılıklarını yüklemek için komut penceresinde.</span><span class="sxs-lookup"><span data-stu-id="60289-114">Type **gem install azure** in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="60289-115">Paket alma</span><span class="sxs-lookup"><span data-stu-id="60289-115">Import the package</span></span>
<span data-ttu-id="60289-116">Sık kullandığınız metin düzenleyiciyi kullanın, burada depolama kullanmayı düşündüğünüz Söyleniş dosyasının üstüne aşağıdakileri ekleyin:</span><span class="sxs-lookup"><span data-stu-id="60289-116">Use your favorite text editor, add the following to the top of the Ruby file where you intend to use Storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="60289-117">Bir Azure depolama bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="60289-117">Set up an Azure Storage connection</span></span>
<span data-ttu-id="60289-118">Azure modülü ortam değişkenleri okur **AZURE\_depolama\_hesap** ve **AZURE\_depolama\_erişim\_anahtar** Azure depolama hesabınıza bağlanmak için gerekli bilgileri için.</span><span class="sxs-lookup"><span data-stu-id="60289-118">The azure module will read the environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** for information required to connect to your Azure Storage account.</span></span> <span data-ttu-id="60289-119">Bu ortam değişkenleri ayarlanmamışsa, hesap bilgilerini kullanmadan önce belirtmelisiniz **Azure::TableService** aşağıdaki kod ile:</span><span class="sxs-lookup"><span data-stu-id="60289-119">If these environment variables are not set, you must specify the account information before using **Azure::TableService** with the following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="60289-120">Klasik veya Resource Manager depolama hesabı Azure portalında bu değerleri almak için:</span><span class="sxs-lookup"><span data-stu-id="60289-120">To obtain these values from a classic or Resource Manager storage account in the Azure portal:</span></span>

1. <span data-ttu-id="60289-121">[Azure Portal](https://portal.azure.com)’da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="60289-121">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="60289-122">Kullanmak istediğiniz depolama hesabınıza gidin.</span><span class="sxs-lookup"><span data-stu-id="60289-122">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="60289-123">Sağ taraftaki ayarları dikey penceresinde tıklayın **erişim tuşları**.</span><span class="sxs-lookup"><span data-stu-id="60289-123">In the Settings blade on the right, click **Access Keys**.</span></span>
4. <span data-ttu-id="60289-124">Görüntülenen erişim anahtarları dikey penceresinde, erişim tuşu 1 ve 2 erişim anahtarı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="60289-124">In the Access keys blade that appears, you'll see the access key 1 and access key 2.</span></span> <span data-ttu-id="60289-125">Bunlardan kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="60289-125">You can use either of these.</span></span>
5. <span data-ttu-id="60289-126">Anahtarı panoya kopyalamak için Kopyala simgesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="60289-126">Click the copy icon to copy the key to the clipboard.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="60289-127">Bir tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="60289-127">Create a table</span></span>
<span data-ttu-id="60289-128">**Azure::TableService** nesnesi, tabloları ve varlıkları ile çalışmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="60289-128">The **Azure::TableService** object lets you work with tables and entities.</span></span> <span data-ttu-id="60289-129">Bir tablo oluşturmak için kullanmak **oluşturma\_table()** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="60289-129">To create a table, use the **create\_table()** method.</span></span> <span data-ttu-id="60289-130">Aşağıdaki örnek, bir tablo oluşturur veya hata varsa yazdırır.</span><span class="sxs-lookup"><span data-stu-id="60289-130">The following example creates a table or prints the error if there is any.</span></span>

```ruby
azure_table_service = Azure::TableService.new
begin
    azure_table_service.create_table("testtable")
rescue
    puts $!
end
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="60289-131">Tabloya bir varlık ekleme</span><span class="sxs-lookup"><span data-stu-id="60289-131">Add an entity to a table</span></span>
<span data-ttu-id="60289-132">Bir varlık eklemek için önce varlık özelliklerinizi tanımlayan bir karma nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="60289-132">To add an entity, first create a hash object that defines your entity properties.</span></span> <span data-ttu-id="60289-133">Her varlık için belirtmelisiniz Not bir **PartitionKey** ve **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="60289-133">Note that for every entity you must specify a **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="60289-134">Bunlar, varlıklarınızı'nın benzersiz tanımlayıcıları ve çok diğer özelliklerinizi daha hızlı sorgulanabilir değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="60289-134">These are the unique identifiers of your entities, and are values that can be queried much faster than your other properties.</span></span> <span data-ttu-id="60289-135">Azure depolama kullanan **PartitionKey** tablonun varlıklar birçok depolama düğümleri üzerinde otomatik olarak dağıtmak için.</span><span class="sxs-lookup"><span data-stu-id="60289-135">Azure Storage uses **PartitionKey** to automatically distribute the table's entities over many storage nodes.</span></span> <span data-ttu-id="60289-136">Aynı varlıkla **PartitionKey** aynı düğümde depolanır.</span><span class="sxs-lookup"><span data-stu-id="60289-136">Entities with the same **PartitionKey** are stored on the same node.</span></span> <span data-ttu-id="60289-137">**RowKey** varlığın ait bölüm içinde benzersiz kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="60289-137">The **RowKey** is the unique ID of the entity within the partition it belongs to.</span></span>

```ruby
entity = { "content" => "test entity",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.insert_entity("testtable", entity)
```

## <a name="update-an-entity"></a><span data-ttu-id="60289-138">Bir varlığı güncelleştirir</span><span class="sxs-lookup"><span data-stu-id="60289-138">Update an entity</span></span>
<span data-ttu-id="60289-139">Var olan bir varlığı güncelleştirmek için kullanılabilir birden çok yöntemi vardır:</span><span class="sxs-lookup"><span data-stu-id="60289-139">There are multiple methods available to update an existing entity:</span></span>

* <span data-ttu-id="60289-140">**Güncelleştirme\_entity():** var olan bir varlığı değiştirme tarafından güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="60289-140">**update\_entity():** Update an existing entity by replacing it.</span></span>
* <span data-ttu-id="60289-141">**birleştirme\_entity():** varolan varlık kümesine yeni özellik değerlerinin birleştirerek var olan bir varlığı güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="60289-141">**merge\_entity():** Updates an existing entity by merging new property values into the existing entity.</span></span>
* <span data-ttu-id="60289-142">**INSERT\_veya\_birleştirme\_entity():** değiştirme tarafından var olan bir varlığı güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="60289-142">**insert\_or\_merge\_entity():** Updates an existing entity by replacing it.</span></span> <span data-ttu-id="60289-143">Hiçbir varlık varsa, yeni bir tane eklenir:</span><span class="sxs-lookup"><span data-stu-id="60289-143">If no entity exists, a new one will be inserted:</span></span>
* <span data-ttu-id="60289-144">**INSERT\_veya\_Değiştir\_entity():** varolan varlık kümesine yeni özellik değerlerinin birleştirerek var olan bir varlığı güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="60289-144">**insert\_or\_replace\_entity():** Updates an existing entity by merging new property values into the existing entity.</span></span> <span data-ttu-id="60289-145">Hiçbir varlık varsa, yeni bir tane eklenir.</span><span class="sxs-lookup"><span data-stu-id="60289-145">If no entity exists, a new one will be inserted.</span></span>

<span data-ttu-id="60289-146">Aşağıdaki örnek, bir varlık kullanarak güncelleştirme gösterir **güncelleştirme\_entity()**:</span><span class="sxs-lookup"><span data-stu-id="60289-146">The following example demonstrates updating an entity using **update\_entity()**:</span></span>

```ruby
entity = { "content" => "test entity with updated content",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.update_entity("testtable", entity)
```

<span data-ttu-id="60289-147">İle **güncelleştirme\_entity()** ve **birleştirme\_entity()**, güncelleştirdiğiniz varlık yoksa güncelleştirme işlemi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="60289-147">With **update\_entity()** and **merge\_entity()**, if the entity that you are updating doesn't exist then the update operation will fail.</span></span> <span data-ttu-id="60289-148">Bu nedenle olup zaten var. bakılmaksızın bir varlık depolamak istiyorsanız, bunun yerine kullanmalısınız **Ekle\_veya\_Değiştir\_entity()** veya **Ekle\_veya\_birleştirme\_entity()**.</span><span class="sxs-lookup"><span data-stu-id="60289-148">Therefore if you wish to store an entity regardless of whether it already exists, you should instead use **insert\_or\_replace\_entity()** or **insert\_or\_merge\_entity()**.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="60289-149">Varlıkları gruplarıyla çalışma</span><span class="sxs-lookup"><span data-stu-id="60289-149">Work with groups of entities</span></span>
<span data-ttu-id="60289-150">Bazen birden çok sunucu tarafından işleme atomik emin olmak için birlikte toplu iş işlemlerinde göndermek için mantıklıdır.</span><span class="sxs-lookup"><span data-stu-id="60289-150">Sometimes it makes sense to submit multiple operations together in a batch to ensure atomic processing by the server.</span></span> <span data-ttu-id="60289-151">Bunu yapmaya yönelik önce oluşturduğunuz bir **toplu** nesnesi ve ardından **yürütme\_batch()** yöntemi **TableService**.</span><span class="sxs-lookup"><span data-stu-id="60289-151">To accomplish that, you first create a **Batch** object and then use the **execute\_batch()** method on **TableService**.</span></span> <span data-ttu-id="60289-152">Aşağıdaki örnek, iki varlık RowKey 2 ve 3 toplu gönderme gösterir.</span><span class="sxs-lookup"><span data-stu-id="60289-152">The following example demonstrates submitting two entities with RowKey 2 and 3 in a batch.</span></span> <span data-ttu-id="60289-153">Yalnızca aynı PartitionKey sahip varlıklar için çalışır durumda olduğunu dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="60289-153">Notice that it only works for entities with the same PartitionKey.</span></span>

```ruby
azure_table_service = Azure::TableService.new
batch = Azure::Storage::Table::Batch.new("testtable",
    "test-partition-key") do
    insert "2", { "content" => "new content 2" }
    insert "3", { "content" => "new content 3" }
end
results = azure_table_service.execute_batch(batch)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="60289-154">Bir varlık için sorgu</span><span class="sxs-lookup"><span data-stu-id="60289-154">Query for an entity</span></span>
<span data-ttu-id="60289-155">Bir tablodaki bir varlık sorgulamak için kullanın **almak\_entity()** tablo adı geçirerek yöntemi **PartitionKey** ve **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="60289-155">To query an entity in a table, use the **get\_entity()** method, by passing the table name, **PartitionKey** and **RowKey**.</span></span>

```ruby
result = azure_table_service.get_entity("testtable", "test-partition-key",
    "1")
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="60289-156">Varlık kümesi sorgulama</span><span class="sxs-lookup"><span data-stu-id="60289-156">Query a set of entities</span></span>
<span data-ttu-id="60289-157">Bir tablodaki varlıkları kümesinin sorgulamak için bir sorgu karma nesnesi oluşturma ve kullanma **sorgu\_entities()** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="60289-157">To query a set of entities in a table, create a query hash object and use the **query\_entities()** method.</span></span> <span data-ttu-id="60289-158">Aşağıdaki örnek, aynı tüm varlıkları alma gösterir **PartitionKey**:</span><span class="sxs-lookup"><span data-stu-id="60289-158">The following example demonstrates getting all the entities with the same **PartitionKey**:</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'" }
result, token = azure_table_service.query_entities("testtable", query)
```

> [!NOTE]
> <span data-ttu-id="60289-159">Sonuç kümesi döndürmek sonraki sayfalarda almak için kullanabileceğiniz bir devamlılık belirteci döndürülecek tek bir sorgu için çok büyük.</span><span class="sxs-lookup"><span data-stu-id="60289-159">If the result set is too large for a single query to return, a continuation token will be returned which you can use to retrieve subsequent pages.</span></span>
>
>

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="60289-160">Giriş özellikleri alt kümesi sorgulama</span><span class="sxs-lookup"><span data-stu-id="60289-160">Query a subset of entity properties</span></span>
<span data-ttu-id="60289-161">Sorguda bir tabloya bir varlık birkaç özelliği alabilir.</span><span class="sxs-lookup"><span data-stu-id="60289-161">A query to a table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="60289-162">"Projeksiyon" olarak adlandırılan bu teknik bant genişliğini azaltır ve özellikle büyük varlıklar için sorgu performansını iyileştirebilir.</span><span class="sxs-lookup"><span data-stu-id="60289-162">This technique, called "projection", reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="60289-163">Select yan tümcesi kullanın ve istemciye Getir istediğiniz özellik adlarını geçirin.</span><span class="sxs-lookup"><span data-stu-id="60289-163">Use the select clause and pass the names of the properties you would like to bring over to the client.</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'",
    :select => ["content"] }
result, token = azure_table_service.query_entities("testtable", query)
```

## <a name="delete-an-entity"></a><span data-ttu-id="60289-164">Bir varlığı silme</span><span class="sxs-lookup"><span data-stu-id="60289-164">Delete an entity</span></span>
<span data-ttu-id="60289-165">Bir varlığı silmek için kullanın **silmek\_entity()** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="60289-165">To delete an entity, use the **delete\_entity()** method.</span></span> <span data-ttu-id="60289-166">Varlık, varlığın PartitionKey ve RowKey varlık içeren tablo adına geçmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="60289-166">You need to pass in the name of the table which contains the entity, the PartitionKey and RowKey of the entity.</span></span>

```ruby
azure_table_service.delete_entity("testtable", "test-partition-key", "1")
```

## <a name="delete-a-table"></a><span data-ttu-id="60289-167">Bir tablo silme</span><span class="sxs-lookup"><span data-stu-id="60289-167">Delete a table</span></span>
<span data-ttu-id="60289-168">Bir tablo silmek için kullanın **silmek\_table()** yöntemi ve silmek istediğiniz tabloyu adına geçirin.</span><span class="sxs-lookup"><span data-stu-id="60289-168">To delete a table, use the **delete\_table()** method and pass in the name of the table you want to delete.</span></span>

```ruby
azure_table_service.delete_table("testtable")
```

## <a name="next-steps"></a><span data-ttu-id="60289-169">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="60289-169">Next steps</span></span>

* <span data-ttu-id="60289-170">[Microsoft Azure Depolama Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md), Microsoft’un Windows, macOS ve Linux üzerinde Azure Depolama verileriyle görsel olarak çalışmanızı sağlayan ücretsiz ve tek başına uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="60289-170">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="60289-171">[Ruby için Azure SDK](http://github.com/WindowsAzure/azure-sdk-for-ruby) github'daki</span><span class="sxs-lookup"><span data-stu-id="60289-171">[Azure SDK for Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

