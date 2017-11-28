---
title: Python ile Azure Table depolama aaaHow toouse | Microsoft Docs
description: "Bir NoSQL veri deposu olan Azure Table storage kullanılarak hello bulutta yapılandırılmış veri depolayın."
services: cosmos-db
documentationcenter: python
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: 7ddb9f3e-4e6d-4103-96e6-f0351d69a17b
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/16/2017
ms.author: mimig
ms.openlocfilehash: 3382fcd5667a93d5533b5f8fad1d3d1c27f23482
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-in-python"></a><span data-ttu-id="3d4df-103">Nasıl toouse Python tablo depolama</span><span class="sxs-lookup"><span data-stu-id="3d4df-103">How toouse Table storage in Python</span></span>

[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

<span data-ttu-id="3d4df-104">Bu kılavuz size nasıl tooperform ortak Azure Table depolama senaryolarda kullanarak Python hello gösterir [Python için Microsoft Azure depolama SDK](https://github.com/Azure/azure-storage-python).</span><span class="sxs-lookup"><span data-stu-id="3d4df-104">This guide shows you how tooperform common Azure Table storage scenarios in Python using hello [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="3d4df-105">Kapsanan hello senaryolar oluşturma ve bir tablo, silme ve ekleme ve varlıkları sorgulama içerir.</span><span class="sxs-lookup"><span data-stu-id="3d4df-105">hello scenarios covered include creating and deleting a table, and inserting and querying entities.</span></span>

<span data-ttu-id="3d4df-106">Çalışırken hello senaryoları aracılığıyla Bu öğreticide, toorefer toohello isteyebilir [Python API Başvurusu için Azure depolama SDK'sı](https://azure-storage.readthedocs.io/en/latest/index.html).</span><span class="sxs-lookup"><span data-stu-id="3d4df-106">While working through hello scenarios in this tutorial, you may wish toorefer toohello [Azure Storage SDK for Python API reference](https://azure-storage.readthedocs.io/en/latest/index.html).</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="install-hello-azure-storage-sdk-for-python"></a><span data-ttu-id="3d4df-107">Python için Hello Azure depolama SDK'sını yükleyin</span><span class="sxs-lookup"><span data-stu-id="3d4df-107">Install hello Azure Storage SDK for Python</span></span>

<span data-ttu-id="3d4df-108">Bir depolama hesabı oluşturduktan sonra sonraki adımınız tooinstall hello olan [Python için Microsoft Azure depolama SDK](https://github.com/Azure/azure-storage-python).</span><span class="sxs-lookup"><span data-stu-id="3d4df-108">Once you've created a storage account, your next step is tooinstall hello [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="3d4df-109">SDK yükleme ile ilgili ayrıntılar hello için toohello başvuran [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) dosyasında hello depolama SDK'sı Python deposu için github'da.</span><span class="sxs-lookup"><span data-stu-id="3d4df-109">For details on installing hello SDK, refer toohello [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) file in hello Storage SDK for Python repository on GitHub.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="3d4df-110">Bir tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="3d4df-110">Create a table</span></span>

<span data-ttu-id="3d4df-111">toowork hello Python Azure tablo hizmeti ile içeri aktarmanız gerekir hello [TableService] [ py_TableService] modülü.</span><span class="sxs-lookup"><span data-stu-id="3d4df-111">toowork with hello Azure Table service in Python, you must import hello [TableService][py_TableService] module.</span></span> <span data-ttu-id="3d4df-112">Tablo varlıklarla çalışmaya beri hello etmeniz [varlık] [ py_Entity] sınıfı.</span><span class="sxs-lookup"><span data-stu-id="3d4df-112">Since you'll be working with Table entities, you also need hello [Entity][py_Entity] class.</span></span> <span data-ttu-id="3d4df-113">Bu kodu hello üstüne yakın, Python dosyası tooimport hem ekleyin:</span><span class="sxs-lookup"><span data-stu-id="3d4df-113">Add this code near hello top your Python file tooimport both:</span></span>

```python
from azure.storage.table import TableService, Entity
```

<span data-ttu-id="3d4df-114">Oluşturma bir [TableService] [ py_TableService] nesnesi, depolama hesabı adı ve hesap anahtarınızı geçirme.</span><span class="sxs-lookup"><span data-stu-id="3d4df-114">Create a [TableService][py_TableService] object, passing in your storage account name and account key.</span></span> <span data-ttu-id="3d4df-115">Değiştir `myaccount` ve `mykey` hesap adı ve anahtar ve çağrı [create_table] [ py_create_table] toocreate hello Azure Storage tablosunda.</span><span class="sxs-lookup"><span data-stu-id="3d4df-115">Replace `myaccount` and `mykey` with your account name and key, and call [create_table][py_create_table] toocreate hello table in Azure Storage.</span></span>

```python
table_service = TableService(account_name='myaccount', account_key='mykey')

table_service.create_table('tasktable')
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="3d4df-116">Bir varlık tooa tablo ekleme</span><span class="sxs-lookup"><span data-stu-id="3d4df-116">Add an entity tooa table</span></span>

<span data-ttu-id="3d4df-117">tooadd varlık önce oluşturmanız, varlık, ardından geçişi hello nesne toohello temsil eden bir nesne [TableService][py_TableService].[ insert_entity] [ py_insert_entity] yöntemi.</span><span class="sxs-lookup"><span data-stu-id="3d4df-117">tooadd an entity, you first create an object that represents your entity, then pass hello object toohello [TableService][py_TableService].[insert_entity][py_insert_entity] method.</span></span> <span data-ttu-id="3d4df-118">Merhaba varlığı nesnesi, bir sözlük veya türünde bir nesne olabilir [varlık][py_Entity]ve, varlığın özellik adlarını ve değerlerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="3d4df-118">hello entity object can be a dictionary or an object of type [Entity][py_Entity], and defines your entity's property names and values.</span></span> <span data-ttu-id="3d4df-119">Her varlık gerekli hello içermelidir [PartitionKey ve RowKey](#partitionkey-and-rowkey) özellikleri, ayrıca tooany diğer özellikleri hello varlık için tanımladığınız.</span><span class="sxs-lookup"><span data-stu-id="3d4df-119">Every entity must include hello required [PartitionKey and RowKey](#partitionkey-and-rowkey) properties, in addition tooany other properties you define for hello entity.</span></span>

<span data-ttu-id="3d4df-120">Bu örnek, bir sözlük nesnesi oluşturur. bir varlığı temsil eden daha sonra geçirir, toohello [insert_entity] [ py_insert_entity] yöntemi tooadd, toohello tablosu:</span><span class="sxs-lookup"><span data-stu-id="3d4df-120">This example creates a dictionary object representing an entity, then passes it toohello [insert_entity][py_insert_entity] method tooadd it toohello table:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

<span data-ttu-id="3d4df-121">Bu örnekte bir [varlık] [ py_Entity] nesne sonra toohello geçirir [insert_entity] [ py_insert_entity] yöntemi tooadd, toohello tablosu:</span><span class="sxs-lookup"><span data-stu-id="3d4df-121">This example creates an [Entity][py_Entity] object, then passes it toohello [insert_entity][py_insert_entity] method tooadd it toohello table:</span></span>

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '002'
task.description = 'Wash hello car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

### <a name="partitionkey-and-rowkey"></a><span data-ttu-id="3d4df-122">PartitionKey ve RowKey</span><span class="sxs-lookup"><span data-stu-id="3d4df-122">PartitionKey and RowKey</span></span>

<span data-ttu-id="3d4df-123">Her ikisini de belirtmelisiniz bir **PartitionKey** ve **RowKey** özelliği her varlık için.</span><span class="sxs-lookup"><span data-stu-id="3d4df-123">You must specify both a **PartitionKey** and a **RowKey** property for every entity.</span></span> <span data-ttu-id="3d4df-124">Merhaba, varlıklarınızı öğesinin benzersiz tanımlayıcıları olarak birlikte bunlar bir varlığın hello birincil anahtarı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="3d4df-124">These are hello unique identifiers of your entities, as together they form hello primary key of an entity.</span></span> <span data-ttu-id="3d4df-125">Bu değerleri yalnızca bu özellikleri dizine olduğundan başka bir varlık özellikleri sorgulayabilirsiniz çok daha hızlı kullanarak sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d4df-125">You can query using these values much faster than you can query any other entity properties because only these properties are indexed.</span></span>

<span data-ttu-id="3d4df-126">Tablo hizmeti kullanan hello **PartitionKey** toointelligently depolama düğümleri arasında tablo varlıkları dağıtın.</span><span class="sxs-lookup"><span data-stu-id="3d4df-126">hello Table service uses **PartitionKey** toointelligently distribute table entities across storage nodes.</span></span> <span data-ttu-id="3d4df-127">Sahip varlıkları aynı hello **PartitionKey** hello üzerinde depolanan aynı düğüm.</span><span class="sxs-lookup"><span data-stu-id="3d4df-127">Entities that have hello same  **PartitionKey** are stored on hello same node.</span></span> <span data-ttu-id="3d4df-128">**RowKey** ait hello bölüm içinde hello varlığın hello benzersiz kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="3d4df-128">**RowKey** is hello unique ID of hello entity within hello partition it belongs to.</span></span>

## <a name="update-an-entity"></a><span data-ttu-id="3d4df-129">Bir varlığı güncelleştirir</span><span class="sxs-lookup"><span data-stu-id="3d4df-129">Update an entity</span></span>

<span data-ttu-id="3d4df-130">Tüm tooupdate hello bir varlığın özellik değerlerinin ikisinin de, çağrı [update_entity] [ py_update_entity] yöntemi.</span><span class="sxs-lookup"><span data-stu-id="3d4df-130">tooupdate all of an entity's property values, call hello [update_entity][py_update_entity] method.</span></span> <span data-ttu-id="3d4df-131">Bu örnekte gösterilir nasıl tooreplace var olan bir varlığı güncelleştirilmiş bir sürüm:</span><span class="sxs-lookup"><span data-stu-id="3d4df-131">This example shows how tooreplace an existing entity with an updated version:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage', 'priority' : 250}
table_service.update_entity('tasktable', task)
```

<span data-ttu-id="3d4df-132">Güncelleştirilmekte hello varlık zaten mevcut değilse hello güncelleştirme işlemi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="3d4df-132">If hello entity that is being updated doesn't already exist, then hello update operation will fail.</span></span> <span data-ttu-id="3d4df-133">Veya var olup olmadığını toostore bir varlık istiyorsanız kullanın [insert_or_replace_entity][py_insert_or_replace_entity].</span><span class="sxs-lookup"><span data-stu-id="3d4df-133">If you want toostore an entity whether it exists or not, use [insert_or_replace_entity][py_insert_or_replace_entity].</span></span> <span data-ttu-id="3d4df-134">Aşağıdaki örneğine hello hello ilk çağrıda hello varolan varlık yerini alır.</span><span class="sxs-lookup"><span data-stu-id="3d4df-134">In hello following example, hello first call will replace hello existing entity.</span></span> <span data-ttu-id="3d4df-135">Merhaba ikinci çağrı yeni bir varlık ekler, hiçbir varlık hello ile PartitionKey ve RowKey belirtilen beri hello tablosunda mevcut.</span><span class="sxs-lookup"><span data-stu-id="3d4df-135">hello second call will insert a new entity, since no entity with hello specified PartitionKey and RowKey exists in hello table.</span></span>

```python
# Replace hello entity created earlier
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', task)

# Insert a new entity
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '003', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', task)
```

> [!TIP]
> <span data-ttu-id="3d4df-136">Merhaba [update_entity] [ py_update_entity] yöntemi, tüm özellikler ve ayrıca varolan bir varlığına değerlerini değiştirir var olan bir varlığı tooremove özelliklerinden kullanın.</span><span class="sxs-lookup"><span data-stu-id="3d4df-136">hello [update_entity][py_update_entity] method replaces all properties and values of an existing entity, which you can also use tooremove properties from an existing entity.</span></span> <span data-ttu-id="3d4df-137">Merhaba kullanabilirsiniz [merge_entity] [ py_merge_entity] yöntemi tooupdate tamamen hello varlık değiştirme olmadan yeni veya değiştirilmiş özellik değerlerini sahip varolan bir varlık.</span><span class="sxs-lookup"><span data-stu-id="3d4df-137">You can use hello [merge_entity][py_merge_entity] method tooupdate an existing entity with new or modified property values without completely replacing hello entity.</span></span>

## <a name="modify-multiple-entities"></a><span data-ttu-id="3d4df-138">Birden çok varlık değiştirme</span><span class="sxs-lookup"><span data-stu-id="3d4df-138">Modify multiple entities</span></span>

<span data-ttu-id="3d4df-139">tooensure hello tablo hizmeti tarafından atomik bir isteğin işlenmesi Merhaba, birden çok işlemlerinde birlikte bir toplu gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d4df-139">tooensure hello atomic processing of a request by hello Table service, you can submit multiple operations together in a batch.</span></span> <span data-ttu-id="3d4df-140">İlk olarak, hello kullanın [TableBatch] [ py_TableBatch] tooadd birden çok operations tooa tek toplu sınıfı.</span><span class="sxs-lookup"><span data-stu-id="3d4df-140">First, use hello [TableBatch][py_TableBatch] class tooadd multiple operations tooa single batch.</span></span> <span data-ttu-id="3d4df-141">Ardından, çağrı [TableService][py_TableService].[ commit_batch] [ py_commit_batch] toosubmit hello işlemlerinde atomik bir işlem.</span><span class="sxs-lookup"><span data-stu-id="3d4df-141">Next, call [TableService][py_TableService].[commit_batch][py_commit_batch] toosubmit hello operations in an atomic operation.</span></span> <span data-ttu-id="3d4df-142">Toplu işlemde değiştiren tüm varlıkları toobe hello olmalıdır aynı bölüm.</span><span class="sxs-lookup"><span data-stu-id="3d4df-142">All entities toobe modified in batch must be in hello same partition.</span></span>

<span data-ttu-id="3d4df-143">Bu örnek iki varlık bir toplu işlemde toplar:</span><span class="sxs-lookup"><span data-stu-id="3d4df-143">This example adds two entities together in a batch:</span></span>

```python
from azure.storage.table import TableBatch
batch = TableBatch()
task004 = {'PartitionKey': 'tasksSeattle', 'RowKey': '004', 'description' : 'Go grocery shopping', 'priority' : 400}
task005 = {'PartitionKey': 'tasksSeattle', 'RowKey': '005', 'description' : 'Clean hello bathroom', 'priority' : 100}
batch.insert_entity(task004)
batch.insert_entity(task005)
table_service.commit_batch('tasktable', batch)
```

<span data-ttu-id="3d4df-144">Toplu hello İçerik Yöneticisi sözdizimi ile de kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="3d4df-144">Batches can also be used with hello context manager syntax:</span></span>

```python
task006 = {'PartitionKey': 'tasksSeattle', 'RowKey': '006', 'description' : 'Go grocery shopping', 'priority' : 400}
task007 = {'PartitionKey': 'tasksSeattle', 'RowKey': '007', 'description' : 'Clean hello bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task006)
    batch.insert_entity(task007)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="3d4df-145">Bir varlık için sorgu</span><span class="sxs-lookup"><span data-stu-id="3d4df-145">Query for an entity</span></span>

<span data-ttu-id="3d4df-146">tooquery bir tabloda, bir varlığın PartitionKey ve RowKey toohello geçirmek [TableService][py_TableService].[ get_entity] [ py_get_entity] yöntemi.</span><span class="sxs-lookup"><span data-stu-id="3d4df-146">tooquery for an entity in a table, pass its PartitionKey and RowKey toohello [TableService][py_TableService].[get_entity][py_get_entity] method.</span></span>

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '001')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="3d4df-147">Varlık kümesi sorgulama</span><span class="sxs-lookup"><span data-stu-id="3d4df-147">Query a set of entities</span></span>

<span data-ttu-id="3d4df-148">Varlık kümesi için bir filtre dizesi hello ile sağlayarak Sorgulayabileceğiniz **filtre** parametresi.</span><span class="sxs-lookup"><span data-stu-id="3d4df-148">You can query for a set of entities by supplying a filter string with hello **filter** parameter.</span></span> <span data-ttu-id="3d4df-149">Bu örnekte, tüm görevler PartitionKey üzerinde filtre uygulayarak Seattle bulur:</span><span class="sxs-lookup"><span data-stu-id="3d4df-149">This example finds all tasks in Seattle by applying a filter on PartitionKey:</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="3d4df-150">Giriş özellikleri alt kümesi sorgulama</span><span class="sxs-lookup"><span data-stu-id="3d4df-150">Query a subset of entity properties</span></span>

<span data-ttu-id="3d4df-151">Sorgudaki her bir varlık için döndürülen hangi özelliklerin de kısıtlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d4df-151">You can also restrict which properties are returned for each entity in a query.</span></span> <span data-ttu-id="3d4df-152">Adlı bu teknik *projeksiyon*, bant genişliğini azaltır ve özellikle büyük varlıklar veya sonuç kümesi için sorgu performansını iyileştirebilir.</span><span class="sxs-lookup"><span data-stu-id="3d4df-152">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities or result sets.</span></span> <span data-ttu-id="3d4df-153">Kullanım hello **seçin** parametre ve geçişi hello adları istediğiniz hello özelliklerinin toohello istemci döndürdü.</span><span class="sxs-lookup"><span data-stu-id="3d4df-153">Use hello **select** parameter and pass hello names of hello properties you want returned toohello client.</span></span>

<span data-ttu-id="3d4df-154">koddan hello Hello sorguda yalnızca hello açıklamaları varlıkların hello tablodaki döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d4df-154">hello query in hello following code returns only hello descriptions of entities in hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="3d4df-155">Aşağıdaki kod parçacığında works yalnızca hello Azure Storage karşı hello.</span><span class="sxs-lookup"><span data-stu-id="3d4df-155">hello following snippet works only against hello Azure Storage.</span></span> <span data-ttu-id="3d4df-156">Merhaba depolama öykünücüsü tarafından desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="3d4df-156">It is not supported by hello storage emulator.</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a><span data-ttu-id="3d4df-157">Bir varlığı silme</span><span class="sxs-lookup"><span data-stu-id="3d4df-157">Delete an entity</span></span>

<span data-ttu-id="3d4df-158">Bir varlığın PartitionKey ve RowKey toohello geçirerek silme [delete_entity] [ py_delete_entity] yöntemi.</span><span class="sxs-lookup"><span data-stu-id="3d4df-158">Delete an entity by passing its PartitionKey and RowKey toohello [delete_entity][py_delete_entity] method.</span></span>

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '001')
```

## <a name="delete-a-table"></a><span data-ttu-id="3d4df-159">Bir tablo silme</span><span class="sxs-lookup"><span data-stu-id="3d4df-159">Delete a table</span></span>

<span data-ttu-id="3d4df-160">Bir tablo veya hello varlıkları hiçbirini artık ihtiyacınız varsa, hello çağrısı [delete_table] [ py_delete_table] yöntemi toopermanently Azure depolama biriminden hello Tablo Sil.</span><span class="sxs-lookup"><span data-stu-id="3d4df-160">If you no longer need a table or any of hello entities within it, call hello [delete_table][py_delete_table] method toopermanently delete hello table from Azure Storage.</span></span>

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a><span data-ttu-id="3d4df-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3d4df-161">Next steps</span></span>

* [<span data-ttu-id="3d4df-162">Azure depolama için SDK'sı Python API Başvurusu</span><span class="sxs-lookup"><span data-stu-id="3d4df-162">Azure Storage SDK for Python API reference</span></span>](https://azure-storage.readthedocs.io/en/latest/index.html)
* [<span data-ttu-id="3d4df-163">Azure depolama için Python SDK'sı</span><span class="sxs-lookup"><span data-stu-id="3d4df-163">Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)
* [<span data-ttu-id="3d4df-164">Python Geliştirici Merkezi</span><span class="sxs-lookup"><span data-stu-id="3d4df-164">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* <span data-ttu-id="3d4df-165">[Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md): görsel olarak Windows, macOS ve Linux Azure Storage ile çalışmak için ücretsiz, platformlar arası bir uygulama.</span><span class="sxs-lookup"><span data-stu-id="3d4df-165">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md): A free, cross-platform application for working visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

[py_commit_batch]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.commit_batch
[py_create_table]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.create_table
[py_delete_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.delete_entity
[py_delete_table]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.delete_table
[py_Entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.models.html#azure.storage.table.models.Entity
[py_get_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.get_entity
[py_insert_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.insert_entity
[py_insert_or_replace_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.insert_or_replace_entity
[py_merge_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.merge_entity
[py_update_entity]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html#azure.storage.table.tableservice.TableService.update_entity
[py_TableService]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tableservice.html
[py_TableBatch]: https://azure-storage.readthedocs.io/en/latest/ref/azure.storage.table.tablebatch.html#azure.storage.table.tablebatch.TableBatch
