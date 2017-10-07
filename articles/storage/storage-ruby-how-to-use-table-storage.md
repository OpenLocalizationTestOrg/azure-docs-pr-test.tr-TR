---
title: "aaaHow toouse Ruby Azure tablo depolamasından | Microsoft Docs"
description: "Bir NoSQL veri deposu olan Azure Table storage kullanılarak hello bulutta yapılandırılmış veri depolayın."
services: storage
documentationcenter: ruby
author: mmacy
manager: timlt
editor: 
ms.assetid: 047cd9ff-17d3-4c15-9284-1b5cc61a3224
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 9c77ff9f384a776c9bc075b60b351685c61acc36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-ruby"></a><span data-ttu-id="c3b44-103">Nasıl toouse Ruby Azure tablo depolamasından</span><span class="sxs-lookup"><span data-stu-id="c3b44-103">How toouse Azure Table Storage from Ruby</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="c3b44-104">Genel Bakış</span><span class="sxs-lookup"><span data-stu-id="c3b44-104">Overview</span></span>
<span data-ttu-id="c3b44-105">Bu kılavuz size nasıl tooperform yaygın senaryolar kullanarak Azure Table hizmet hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="c3b44-105">This guide shows you how tooperform common scenarios using hello Azure Table service.</span></span> <span data-ttu-id="c3b44-106">Merhaba örnekleri hello Ruby API kullanılarak yazılır.</span><span class="sxs-lookup"><span data-stu-id="c3b44-106">hello samples are written using hello Ruby API.</span></span> <span data-ttu-id="c3b44-107">Merhaba kapsanan senaryolar dahil **oluşturma ve bir tablo, ekleme ve bir tablo varlıkları sorgulama**.</span><span class="sxs-lookup"><span data-stu-id="c3b44-107">hello scenarios covered include **creating and deleting a table, inserting and querying entities in a table**.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="c3b44-108">Ruby uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="c3b44-108">Create a Ruby application</span></span>
<span data-ttu-id="c3b44-109">Yönergeler için nasıl toocreate Ruby uygulaması bkz [Azure VM'de rayları Web uygulaması üzerinde Söyleniş](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="c3b44-109">For instructions how toocreate a Ruby application, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="c3b44-110">Uygulama tooaccess depolama yapılandırma</span><span class="sxs-lookup"><span data-stu-id="c3b44-110">Configure your application tooaccess Storage</span></span>
<span data-ttu-id="c3b44-111">Azure Storage toouse, toodownload ve kullanım hello hello depolama REST Hizmetleri ile iletişim kuran bir dizi kolaylık içeren Söyleniş azure paketi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c3b44-111">toouse Azure Storage, you need toodownload and use hello Ruby azure package which includes a set of convenience libraries that communicate with hello Storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="c3b44-112">RubyGems tooobtain hello paketini kullanın</span><span class="sxs-lookup"><span data-stu-id="c3b44-112">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="c3b44-113">Bir komut satırı arabirimi gibi kullandığınız **PowerShell** (Windows), **Terminal** (Mac) veya **Bash** (UNIX).</span><span class="sxs-lookup"><span data-stu-id="c3b44-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="c3b44-114">Tür **gem yükleme azure** hello komut penceresinde tooinstall hello gem ve bağımlılıkları.</span><span class="sxs-lookup"><span data-stu-id="c3b44-114">Type **gem install azure** in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="c3b44-115">Merhaba paketi İçeri Aktar</span><span class="sxs-lookup"><span data-stu-id="c3b44-115">Import hello package</span></span>
<span data-ttu-id="c3b44-116">Sık kullandığınız metin düzenleyiciyi kullanın, hello toouse depolama burada düşündüğünüz Söyleniş dosya toohello üstündeki aşağıdaki hello ekleyin:</span><span class="sxs-lookup"><span data-stu-id="c3b44-116">Use your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse Storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="c3b44-117">Bir Azure depolama bağlantı kurma</span><span class="sxs-lookup"><span data-stu-id="c3b44-117">Set up an Azure Storage connection</span></span>
<span data-ttu-id="c3b44-118">Hello azure modülü hello ortam değişkenleri okur **AZURE\_depolama\_hesap** ve **AZURE\_depolama\_erişim\_anahtar**tooconnect tooyour Azure depolama hesabı için bilgi gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="c3b44-118">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** for information required tooconnect tooyour Azure Storage account.</span></span> <span data-ttu-id="c3b44-119">Bu ortam değişkenleri ayarlanmamışsa, kullanmadan önce hello hesap bilgileri belirtmelisiniz **Azure::TableService** koddan hello ile:</span><span class="sxs-lookup"><span data-stu-id="c3b44-119">If these environment variables are not set, you must specify hello account information before using **Azure::TableService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="c3b44-120">tooobtain hello Azure portal bu değerleri Klasik veya Resource Manager depolama hesabı:</span><span class="sxs-lookup"><span data-stu-id="c3b44-120">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="c3b44-121">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c3b44-121">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c3b44-122">Toouse istediğiniz toohello depolama hesabının gidin.</span><span class="sxs-lookup"><span data-stu-id="c3b44-122">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="c3b44-123">Merhaba sağ üzerinde Hello ayarları dikey penceresinde tıklayın **erişim tuşları**.</span><span class="sxs-lookup"><span data-stu-id="c3b44-123">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="c3b44-124">Görüntülenen hello erişim anahtarları dikey penceresinde hello erişim tuşu 1 ve 2 erişim anahtarı görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c3b44-124">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="c3b44-125">Bunlardan kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3b44-125">You can use either of these.</span></span>
5. <span data-ttu-id="c3b44-126">Merhaba Kopyala simgesi toocopy hello anahtar toohello Pano'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="c3b44-126">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

<span data-ttu-id="c3b44-127">tooobtain hello Klasik Azure Portalı'nda bu değerleri Klasik depolama hesabı:</span><span class="sxs-lookup"><span data-stu-id="c3b44-127">tooobtain these values from a classic storage account in hello classic Azure portal:</span></span>

1. <span data-ttu-id="c3b44-128">İçinde toohello oturum [Klasik Azure portalı](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="c3b44-128">Log in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="c3b44-129">Toouse istediğiniz toohello depolama hesabının gidin.</span><span class="sxs-lookup"><span data-stu-id="c3b44-129">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="c3b44-130">Tıklatın **erişim ANAHTARLARINI Yönet** hello Gezinti bölmesinin hello altındaki.</span><span class="sxs-lookup"><span data-stu-id="c3b44-130">Click **MANAGE ACCESS KEYS** at hello bottom of hello navigation pane.</span></span>
4. <span data-ttu-id="c3b44-131">Merhaba açılan iletişim kutusunda hello depolama hesabı adı, birincil erişim anahtarını ve ikincil erişim anahtarını görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="c3b44-131">In hello pop-up dialog, you'll see hello storage account name, primary access key and secondary access key.</span></span> <span data-ttu-id="c3b44-132">Erişim anahtarı hello birincil veya ikincil bir hello kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3b44-132">For access key, you can use either hello primary one or hello secondary one.</span></span>
5. <span data-ttu-id="c3b44-133">Merhaba Kopyala simgesi toocopy hello anahtar toohello Pano'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="c3b44-133">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="c3b44-134">Bir tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="c3b44-134">Create a table</span></span>
<span data-ttu-id="c3b44-135">Merhaba **Azure::TableService** nesnesi, tabloları ve varlıkları ile çalışmanıza olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="c3b44-135">hello **Azure::TableService** object lets you work with tables and entities.</span></span> <span data-ttu-id="c3b44-136">toocreate bir tablo kullanmak hello **oluşturma\_table()** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="c3b44-136">toocreate a table, use hello **create\_table()** method.</span></span> <span data-ttu-id="c3b44-137">Merhaba aşağıdaki örnek bir tablo oluşturur veya varsa baskı siparişi hata hello.</span><span class="sxs-lookup"><span data-stu-id="c3b44-137">hello following example creates a table or prints hello error if there is any.</span></span>

```ruby
azure_table_service = Azure::TableService.new
begin
    azure_table_service.create_table("testtable")
rescue
    puts $!
end
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="c3b44-138">Bir varlık tooa tablo ekleme</span><span class="sxs-lookup"><span data-stu-id="c3b44-138">Add an entity tooa table</span></span>
<span data-ttu-id="c3b44-139">bir varlık tooadd ilk varlık özelliklerinizi tanımlayan bir karma nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c3b44-139">tooadd an entity, first create a hash object that defines your entity properties.</span></span> <span data-ttu-id="c3b44-140">Her varlık için belirtmelisiniz Not bir **PartitionKey** ve **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="c3b44-140">Note that for every entity you must specify a **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="c3b44-141">Bunlar hello varlıklarınızı öğesinin benzersiz tanımlayıcıları ve çok diğer özelliklerinizi daha hızlı sorgulanabilir değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="c3b44-141">These are hello unique identifiers of your entities, and are values that can be queried much faster than your other properties.</span></span> <span data-ttu-id="c3b44-142">Azure depolama kullanan **PartitionKey** tooautomatically çok sayıda depolama düğümleri Merhaba tablonun varlıklar dağıtın.</span><span class="sxs-lookup"><span data-stu-id="c3b44-142">Azure Storage uses **PartitionKey** tooautomatically distribute hello table's entities over many storage nodes.</span></span> <span data-ttu-id="c3b44-143">Varlıklarla aynı hello **PartitionKey** hello üzerinde depolanan aynı düğüm.</span><span class="sxs-lookup"><span data-stu-id="c3b44-143">Entities with hello same **PartitionKey** are stored on hello same node.</span></span> <span data-ttu-id="c3b44-144">Merhaba **RowKey** ait hello bölüm içinde hello varlığın hello benzersiz kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="c3b44-144">hello **RowKey** is hello unique ID of hello entity within hello partition it belongs to.</span></span>

```ruby
entity = { "content" => "test entity",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.insert_entity("testtable", entity)
```

## <a name="update-an-entity"></a><span data-ttu-id="c3b44-145">Bir varlığı güncelleştirir</span><span class="sxs-lookup"><span data-stu-id="c3b44-145">Update an entity</span></span>
<span data-ttu-id="c3b44-146">Var olan bir varlığı birden çok yöntemleri kullanılabilir tooupdate vardır:</span><span class="sxs-lookup"><span data-stu-id="c3b44-146">There are multiple methods available tooupdate an existing entity:</span></span>

* <span data-ttu-id="c3b44-147">**Güncelleştirme\_entity():** var olan bir varlığı değiştirme tarafından güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="c3b44-147">**update\_entity():** Update an existing entity by replacing it.</span></span>
* <span data-ttu-id="c3b44-148">**birleştirme\_entity():** hello varolan varlık kümesine yeni özellik değerlerinin birleştirerek var olan bir varlığı güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="c3b44-148">**merge\_entity():** Updates an existing entity by merging new property values into hello existing entity.</span></span>
* <span data-ttu-id="c3b44-149">**INSERT\_veya\_birleştirme\_entity():** değiştirme tarafından var olan bir varlığı güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="c3b44-149">**insert\_or\_merge\_entity():** Updates an existing entity by replacing it.</span></span> <span data-ttu-id="c3b44-150">Hiçbir varlık varsa, yeni bir tane eklenir:</span><span class="sxs-lookup"><span data-stu-id="c3b44-150">If no entity exists, a new one will be inserted:</span></span>
* <span data-ttu-id="c3b44-151">**INSERT\_veya\_Değiştir\_entity():** hello varolan varlık kümesine yeni özellik değerlerinin birleştirerek var olan bir varlığı güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="c3b44-151">**insert\_or\_replace\_entity():** Updates an existing entity by merging new property values into hello existing entity.</span></span> <span data-ttu-id="c3b44-152">Hiçbir varlık varsa, yeni bir tane eklenir.</span><span class="sxs-lookup"><span data-stu-id="c3b44-152">If no entity exists, a new one will be inserted.</span></span>

<span data-ttu-id="c3b44-153">Merhaba aşağıdaki örneği kullanarak bir varlık güncelleştirme gösterir **güncelleştirme\_entity()**:</span><span class="sxs-lookup"><span data-stu-id="c3b44-153">hello following example demonstrates updating an entity using **update\_entity()**:</span></span>

```ruby
entity = { "content" => "test entity with updated content",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.update_entity("testtable", entity)
```

<span data-ttu-id="c3b44-154">İle **güncelleştirme\_entity()** ve **birleştirme\_entity()**, güncelleştirdiğiniz hello varlık yoksa hello güncelleştirme işlemi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="c3b44-154">With **update\_entity()** and **merge\_entity()**, if hello entity that you are updating doesn't exist then hello update operation will fail.</span></span> <span data-ttu-id="c3b44-155">Bu nedenle olup zaten var. bakılmaksızın bir varlık toostore istiyorsanız, bunun yerine kullanmalısınız **Ekle\_veya\_Değiştir\_entity()** veya **Ekle\_veya \_birleştirme\_entity()**.</span><span class="sxs-lookup"><span data-stu-id="c3b44-155">Therefore if you wish toostore an entity regardless of whether it already exists, you should instead use **insert\_or\_replace\_entity()** or **insert\_or\_merge\_entity()**.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="c3b44-156">Varlıkları gruplarıyla çalışma</span><span class="sxs-lookup"><span data-stu-id="c3b44-156">Work with groups of entities</span></span>
<span data-ttu-id="c3b44-157">Bazen algılama toosubmit birden çok operations birlikte bir toplu tooensure atomik hello sunucusu tarafından işleme kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="c3b44-157">Sometimes it makes sense toosubmit multiple operations together in a batch tooensure atomic processing by hello server.</span></span> <span data-ttu-id="c3b44-158">tooaccomplish önce oluşturmanız, bir **toplu** nesnesi ve ardından hello **yürütme\_batch()** yöntemi **TableService**.</span><span class="sxs-lookup"><span data-stu-id="c3b44-158">tooaccomplish that, you first create a **Batch** object and then use hello **execute\_batch()** method on **TableService**.</span></span> <span data-ttu-id="c3b44-159">Merhaba aşağıdaki örneği iki varlık RowKey 2 ve 3 toplu gönderme gösterir.</span><span class="sxs-lookup"><span data-stu-id="c3b44-159">hello following example demonstrates submitting two entities with RowKey 2 and 3 in a batch.</span></span> <span data-ttu-id="c3b44-160">Aynı PartitionKey sahip varlıklar için Works hello yalnızca o BT dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="c3b44-160">Notice that it only works for entities with hello same PartitionKey.</span></span>

```ruby
azure_table_service = Azure::TableService.new
batch = Azure::Storage::Table::Batch.new("testtable",
    "test-partition-key") do
    insert "2", { "content" => "new content 2" }
    insert "3", { "content" => "new content 3" }
end
results = azure_table_service.execute_batch(batch)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="c3b44-161">Bir varlık için sorgu</span><span class="sxs-lookup"><span data-stu-id="c3b44-161">Query for an entity</span></span>
<span data-ttu-id="c3b44-162">tooquery kullanım hello bir tablodaki bir varlık **almak\_entity()** hello tablo adı geçirerek yöntemi **PartitionKey** ve **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="c3b44-162">tooquery an entity in a table, use hello **get\_entity()** method, by passing hello table name, **PartitionKey** and **RowKey**.</span></span>

```ruby
result = azure_table_service.get_entity("testtable", "test-partition-key",
    "1")
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="c3b44-163">Varlık kümesi sorgulama</span><span class="sxs-lookup"><span data-stu-id="c3b44-163">Query a set of entities</span></span>
<span data-ttu-id="c3b44-164">tooquery varlıklar bir tabloda bir dizi sorgu karma nesne oluşturma ve hello kullanma **sorgu\_entities()** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="c3b44-164">tooquery a set of entities in a table, create a query hash object and use hello **query\_entities()** method.</span></span> <span data-ttu-id="c3b44-165">Merhaba aşağıdaki örnek hello sahip tüm hello varlık alma gösterir aynı **PartitionKey**:</span><span class="sxs-lookup"><span data-stu-id="c3b44-165">hello following example demonstrates getting all hello entities with hello same **PartitionKey**:</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'" }
result, token = azure_table_service.query_entities("testtable", query)
```

> [!NOTE]
> <span data-ttu-id="c3b44-166">Merhaba sonuç kümesi tek bir sorgu tooreturn için çok büyük ise, bir devamlılık belirteci kullanabileceğiniz döndürülecek tooretrieve sonraki sayfalar.</span><span class="sxs-lookup"><span data-stu-id="c3b44-166">If hello result set is too large for a single query tooreturn, a continuation token will be returned which you can use tooretrieve subsequent pages.</span></span>
>
>

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="c3b44-167">Giriş özellikleri alt kümesi sorgulama</span><span class="sxs-lookup"><span data-stu-id="c3b44-167">Query a subset of entity properties</span></span>
<span data-ttu-id="c3b44-168">Sorgu tooa tabloya bir varlık birkaç özelliği alabilir.</span><span class="sxs-lookup"><span data-stu-id="c3b44-168">A query tooa table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="c3b44-169">"Projeksiyon" olarak adlandırılan bu teknik bant genişliğini azaltır ve özellikle büyük varlıklar için sorgu performansını iyileştirebilir.</span><span class="sxs-lookup"><span data-stu-id="c3b44-169">This technique, called "projection", reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="c3b44-170">Kullanım hello select yan tümcesi ve geçişi hello adlarını toohello istemci toobring istediğiniz özellikleri hello.</span><span class="sxs-lookup"><span data-stu-id="c3b44-170">Use hello select clause and pass hello names of hello properties you would like toobring over toohello client.</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'",
    :select => ["content"] }
result, token = azure_table_service.query_entities("testtable", query)
```

## <a name="delete-an-entity"></a><span data-ttu-id="c3b44-171">Bir varlığı silme</span><span class="sxs-lookup"><span data-stu-id="c3b44-171">Delete an entity</span></span>
<span data-ttu-id="c3b44-172">bir varlık toodelete kullanmak hello **silmek\_entity()** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="c3b44-172">toodelete an entity, use hello **delete\_entity()** method.</span></span> <span data-ttu-id="c3b44-173">Merhaba varlık, hello PartitionKey ve RowKey hello varlığın içeren Merhaba tablonun hello adı toopass gerekir.</span><span class="sxs-lookup"><span data-stu-id="c3b44-173">You need toopass in hello name of hello table which contains hello entity, hello PartitionKey and RowKey of hello entity.</span></span>

```ruby
azure_table_service.delete_entity("testtable", "test-partition-key", "1")
```

## <a name="delete-a-table"></a><span data-ttu-id="c3b44-174">Bir tablo silme</span><span class="sxs-lookup"><span data-stu-id="c3b44-174">Delete a table</span></span>
<span data-ttu-id="c3b44-175">toodelete bir tablo kullanmak hello **silmek\_table()** yöntemi ve hello adını geçişinde hello toodelete istediğiniz tablo.</span><span class="sxs-lookup"><span data-stu-id="c3b44-175">toodelete a table, use hello **delete\_table()** method and pass in hello name of hello table you want toodelete.</span></span>

```ruby
azure_table_service.delete_table("testtable")
```

## <a name="next-steps"></a><span data-ttu-id="c3b44-176">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c3b44-176">Next steps</span></span>

* <span data-ttu-id="c3b44-177">[Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md) Windows, macOS ve Linux Azure Storage verilerle görsel olarak toowork sağlayan Microsoft boş bir tek başına uygulamadır.</span><span class="sxs-lookup"><span data-stu-id="c3b44-177">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="c3b44-178">[Ruby için Azure SDK](http://github.com/WindowsAzure/azure-sdk-for-ruby) github'daki</span><span class="sxs-lookup"><span data-stu-id="c3b44-178">[Azure SDK for Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

