---
title: Azure Table storage Python ile kullanma | Microsoft Docs
description: "Bir NoSQL veri deposu olan Azure Table Storage kullanarak bulutta yapılandırılmış veri depolayın."
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
ms.openlocfilehash: 0c46f04786ba4b62bd7ca22c5e25643123e6e136
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-table-storage-in-python"></a><span data-ttu-id="942f5-103">Tablo depolama Python içinde kullanma</span><span class="sxs-lookup"><span data-stu-id="942f5-103">How to use Table storage in Python</span></span>

[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

<span data-ttu-id="942f5-104">Bu kılavuz size nasıl Python kullanarak Azure Table depolama senaryoları gerçekleştirileceğini gösterir [Python için Microsoft Azure depolama SDK](https://github.com/Azure/azure-storage-python).</span><span class="sxs-lookup"><span data-stu-id="942f5-104">This guide shows you how to perform common Azure Table storage scenarios in Python using the [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="942f5-105">Kapsamdaki senaryolar oluşturma ve bir tablo, silme ve ekleme ve varlıkları sorgulama içerir.</span><span class="sxs-lookup"><span data-stu-id="942f5-105">The scenarios covered include creating and deleting a table, and inserting and querying entities.</span></span>

<span data-ttu-id="942f5-106">Çalışırken senaryoları aracılığıyla Bu öğreticide, başvurmak isteyebilirsiniz [Python API Başvurusu için Azure depolama SDK'sı](https://azure-storage.readthedocs.io/en/latest/index.html).</span><span class="sxs-lookup"><span data-stu-id="942f5-106">While working through the scenarios in this tutorial, you may wish to refer to the [Azure Storage SDK for Python API reference](https://azure-storage.readthedocs.io/en/latest/index.html).</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="install-the-azure-storage-sdk-for-python"></a><span data-ttu-id="942f5-107">Python için Azure depolama SDK'sını yükleyin</span><span class="sxs-lookup"><span data-stu-id="942f5-107">Install the Azure Storage SDK for Python</span></span>

<span data-ttu-id="942f5-108">Bir depolama hesabı oluşturduktan sonra sonraki adımınız yüklemektir [Python için Microsoft Azure depolama SDK](https://github.com/Azure/azure-storage-python).</span><span class="sxs-lookup"><span data-stu-id="942f5-108">Once you've created a storage account, your next step is to install the [Microsoft Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span> <span data-ttu-id="942f5-109">SDK'sını yükleme hakkında daha fazla bilgi için başvurmak [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) dosyasında depolama SDK'sı Python deposu için github'da.</span><span class="sxs-lookup"><span data-stu-id="942f5-109">For details on installing the SDK, refer to the [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) file in the Storage SDK for Python repository on GitHub.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="942f5-110">Bir tablo oluşturma</span><span class="sxs-lookup"><span data-stu-id="942f5-110">Create a table</span></span>

<span data-ttu-id="942f5-111">Python Azure tablo hizmetinde çalışmak için içeri aktarmanız gerekir [TableService] [ py_TableService] modülü.</span><span class="sxs-lookup"><span data-stu-id="942f5-111">To work with the Azure Table service in Python, you must import the [TableService][py_TableService] module.</span></span> <span data-ttu-id="942f5-112">Tablo varlıklarla çalışmaya olduğundan, ayrıca gerekir [varlık] [ py_Entity] sınıfı.</span><span class="sxs-lookup"><span data-stu-id="942f5-112">Since you'll be working with Table entities, you also need the [Entity][py_Entity] class.</span></span> <span data-ttu-id="942f5-113">Bu kod ilk her ikisi de içe aktarmak için Python dosyanıza ekleyin:</span><span class="sxs-lookup"><span data-stu-id="942f5-113">Add this code near the top your Python file to import both:</span></span>

```python
from azure.storage.table import TableService, Entity
```

<span data-ttu-id="942f5-114">Oluşturma bir [TableService] [ py_TableService] nesnesi, depolama hesabı adı ve hesap anahtarınızı geçirme.</span><span class="sxs-lookup"><span data-stu-id="942f5-114">Create a [TableService][py_TableService] object, passing in your storage account name and account key.</span></span> <span data-ttu-id="942f5-115">Değiştir `myaccount` ve `mykey` hesap adı ve anahtar ve çağrı [create_table] [ py_create_table] Azure Storage'da bir tablo oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="942f5-115">Replace `myaccount` and `mykey` with your account name and key, and call [create_table][py_create_table] to create the table in Azure Storage.</span></span>

```python
table_service = TableService(account_name='myaccount', account_key='mykey')

table_service.create_table('tasktable')
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="942f5-116">Tabloya bir varlık ekleme</span><span class="sxs-lookup"><span data-stu-id="942f5-116">Add an entity to a table</span></span>

<span data-ttu-id="942f5-117">Bir varlık eklemek için önce varlığı temsil eder ve ardından nesneyi geçirmek bir nesne oluşturma [TableService][py_TableService].[ insert_entity] [ py_insert_entity] yöntemi.</span><span class="sxs-lookup"><span data-stu-id="942f5-117">To add an entity, you first create an object that represents your entity, then pass the object to the [TableService][py_TableService].[insert_entity][py_insert_entity] method.</span></span> <span data-ttu-id="942f5-118">Varlık nesnesi bir sözlük veya türünde bir nesne olabilir [varlık][py_Entity]ve, varlığın özellik adlarını ve değerlerini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="942f5-118">The entity object can be a dictionary or an object of type [Entity][py_Entity], and defines your entity's property names and values.</span></span> <span data-ttu-id="942f5-119">Her varlık gerekli içermelidir [PartitionKey ve RowKey](#partitionkey-and-rowkey) varlık için tanımladığınız diğer özellikleri ek özellikler.</span><span class="sxs-lookup"><span data-stu-id="942f5-119">Every entity must include the required [PartitionKey and RowKey](#partitionkey-and-rowkey) properties, in addition to any other properties you define for the entity.</span></span>

<span data-ttu-id="942f5-120">Bu örnek, bir sözlük nesnesi oluşturur. bir varlığı temsil eden daha sonra geçirir kendisine [insert_entity] [ py_insert_entity] yöntemi tabloya eklemek için:</span><span class="sxs-lookup"><span data-stu-id="942f5-120">This example creates a dictionary object representing an entity, then passes it to the [insert_entity][py_insert_entity] method to add it to the table:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

<span data-ttu-id="942f5-121">Bu örnekte bir [varlık] [ py_Entity] nesnesi, ardından buna ileten [insert_entity] [ py_insert_entity] yöntemi tabloya eklemek için:</span><span class="sxs-lookup"><span data-stu-id="942f5-121">This example creates an [Entity][py_Entity] object, then passes it to the [insert_entity][py_insert_entity] method to add it to the table:</span></span>

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '002'
task.description = 'Wash the car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

### <a name="partitionkey-and-rowkey"></a><span data-ttu-id="942f5-122">PartitionKey ve RowKey</span><span class="sxs-lookup"><span data-stu-id="942f5-122">PartitionKey and RowKey</span></span>

<span data-ttu-id="942f5-123">Her ikisini de belirtmelisiniz bir **PartitionKey** ve **RowKey** özelliği her varlık için.</span><span class="sxs-lookup"><span data-stu-id="942f5-123">You must specify both a **PartitionKey** and a **RowKey** property for every entity.</span></span> <span data-ttu-id="942f5-124">Bunlar, varlıklarınızı'nın benzersiz tanımlayıcıları olarak birbirine bir varlığın birincil anahtarı oluşturur.</span><span class="sxs-lookup"><span data-stu-id="942f5-124">These are the unique identifiers of your entities, as together they form the primary key of an entity.</span></span> <span data-ttu-id="942f5-125">Bu değerleri yalnızca bu özellikleri dizine olduğundan başka bir varlık özellikleri sorgulayabilirsiniz çok daha hızlı kullanarak sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="942f5-125">You can query using these values much faster than you can query any other entity properties because only these properties are indexed.</span></span>

<span data-ttu-id="942f5-126">Tablo hizmeti kullandığı **PartitionKey** tablo varlıkları akıllıca depolama düğümleri arasında dağıtılacak.</span><span class="sxs-lookup"><span data-stu-id="942f5-126">The Table service uses **PartitionKey** to intelligently distribute table entities across storage nodes.</span></span> <span data-ttu-id="942f5-127">Aynı olan varlıkları **PartitionKey** aynı düğümde depolanır.</span><span class="sxs-lookup"><span data-stu-id="942f5-127">Entities that have the same  **PartitionKey** are stored on the same node.</span></span> <span data-ttu-id="942f5-128">**RowKey** varlığın ait bölüm içinde benzersiz kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="942f5-128">**RowKey** is the unique ID of the entity within the partition it belongs to.</span></span>

## <a name="update-an-entity"></a><span data-ttu-id="942f5-129">Bir varlığı güncelleştirir</span><span class="sxs-lookup"><span data-stu-id="942f5-129">Update an entity</span></span>

<span data-ttu-id="942f5-130">Bir varlığın özellik değerlerinin tümü güncelleştirmek için arama [update_entity] [ py_update_entity] yöntemi.</span><span class="sxs-lookup"><span data-stu-id="942f5-130">To update all of an entity's property values, call the [update_entity][py_update_entity] method.</span></span> <span data-ttu-id="942f5-131">Bu örnek, var olan bir varlığı güncelleştirilmiş bir sürümle gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="942f5-131">This example shows how to replace an existing entity with an updated version:</span></span>

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the garbage', 'priority' : 250}
table_service.update_entity('tasktable', task)
```

<span data-ttu-id="942f5-132">Güncelleştirilen varlık zaten mevcut değilse, güncelleştirme işlemi başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="942f5-132">If the entity that is being updated doesn't already exist, then the update operation will fail.</span></span> <span data-ttu-id="942f5-133">Bir varlık depolamak istiyorsanız, bunu var olup olmadığını, kullanın [insert_or_replace_entity][py_insert_or_replace_entity].</span><span class="sxs-lookup"><span data-stu-id="942f5-133">If you want to store an entity whether it exists or not, use [insert_or_replace_entity][py_insert_or_replace_entity].</span></span> <span data-ttu-id="942f5-134">Aşağıdaki örnekte, ilk çağrıda varolan varlık yerini alır.</span><span class="sxs-lookup"><span data-stu-id="942f5-134">In the following example, the first call will replace the existing entity.</span></span> <span data-ttu-id="942f5-135">İkinci çağrı hiçbir varlık belirtilen PartitionKey ile bu yana yeni bir varlık ekler ve RowKey tablosunda yok.</span><span class="sxs-lookup"><span data-stu-id="942f5-135">The second call will insert a new entity, since no entity with the specified PartitionKey and RowKey exists in the table.</span></span>

```python
# Replace the entity created earlier
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out the garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', task)

# Insert a new entity
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '003', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', task)
```

> [!TIP]
> <span data-ttu-id="942f5-136">[Update_entity] [ py_update_entity] yöntemi, tüm özellikler ve var olan bir varlık özellikleri kaldırmak için de kullanabilirsiniz olan bir varlığa değerlerini değiştirir.</span><span class="sxs-lookup"><span data-stu-id="942f5-136">The [update_entity][py_update_entity] method replaces all properties and values of an existing entity, which you can also use to remove properties from an existing entity.</span></span> <span data-ttu-id="942f5-137">Kullanabileceğiniz [merge_entity] [ py_merge_entity] tamamen varlık değiştirmeden yeni veya değiştirilmiş özellik değerleri ile var olan bir varlığı güncelleştirmek için yöntem.</span><span class="sxs-lookup"><span data-stu-id="942f5-137">You can use the [merge_entity][py_merge_entity] method to update an existing entity with new or modified property values without completely replacing the entity.</span></span>

## <a name="modify-multiple-entities"></a><span data-ttu-id="942f5-138">Birden çok varlık değiştirme</span><span class="sxs-lookup"><span data-stu-id="942f5-138">Modify multiple entities</span></span>

<span data-ttu-id="942f5-139">Tablo hizmeti tarafından bir istek atomik işlenmesini sağlamak için birden çok işlemlerinde birlikte bir toplu gönderebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="942f5-139">To ensure the atomic processing of a request by the Table service, you can submit multiple operations together in a batch.</span></span> <span data-ttu-id="942f5-140">İlk olarak, kullanın [TableBatch] [ py_TableBatch] birden çok işlem tek bir toplu eklemek için sınıfı.</span><span class="sxs-lookup"><span data-stu-id="942f5-140">First, use the [TableBatch][py_TableBatch] class to add multiple operations to a single batch.</span></span> <span data-ttu-id="942f5-141">Ardından, çağrı [TableService][py_TableService].[ commit_batch] [ py_commit_batch] atomik bir işlem işlemlerinde göndermek için.</span><span class="sxs-lookup"><span data-stu-id="942f5-141">Next, call [TableService][py_TableService].[commit_batch][py_commit_batch] to submit the operations in an atomic operation.</span></span> <span data-ttu-id="942f5-142">Toplu işlemde değiştirilecek tüm varlıklar aynı bölümde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="942f5-142">All entities to be modified in batch must be in the same partition.</span></span>

<span data-ttu-id="942f5-143">Bu örnek iki varlık bir toplu işlemde toplar:</span><span class="sxs-lookup"><span data-stu-id="942f5-143">This example adds two entities together in a batch:</span></span>

```python
from azure.storage.table import TableBatch
batch = TableBatch()
task004 = {'PartitionKey': 'tasksSeattle', 'RowKey': '004', 'description' : 'Go grocery shopping', 'priority' : 400}
task005 = {'PartitionKey': 'tasksSeattle', 'RowKey': '005', 'description' : 'Clean the bathroom', 'priority' : 100}
batch.insert_entity(task004)
batch.insert_entity(task005)
table_service.commit_batch('tasktable', batch)
```

<span data-ttu-id="942f5-144">Toplu da İçerik Yöneticisi sözdizimiyle kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="942f5-144">Batches can also be used with the context manager syntax:</span></span>

```python
task006 = {'PartitionKey': 'tasksSeattle', 'RowKey': '006', 'description' : 'Go grocery shopping', 'priority' : 400}
task007 = {'PartitionKey': 'tasksSeattle', 'RowKey': '007', 'description' : 'Clean the bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task006)
    batch.insert_entity(task007)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="942f5-145">Bir varlık için sorgu</span><span class="sxs-lookup"><span data-stu-id="942f5-145">Query for an entity</span></span>

<span data-ttu-id="942f5-146">Bir tablodaki bir varlık için sorgulamak üzere kendi PartitionKey ve RowKey için geçirmek [TableService][py_TableService].[ get_entity] [ py_get_entity] yöntemi.</span><span class="sxs-lookup"><span data-stu-id="942f5-146">To query for an entity in a table, pass its PartitionKey and RowKey to the [TableService][py_TableService].[get_entity][py_get_entity] method.</span></span>

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '001')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="942f5-147">Varlık kümesi sorgulama</span><span class="sxs-lookup"><span data-stu-id="942f5-147">Query a set of entities</span></span>

<span data-ttu-id="942f5-148">Varlık kümesi için bir filtre dizesi ile sağlayarak Sorgulayabileceğiniz **filtre** parametresi.</span><span class="sxs-lookup"><span data-stu-id="942f5-148">You can query for a set of entities by supplying a filter string with the **filter** parameter.</span></span> <span data-ttu-id="942f5-149">Bu örnekte, tüm görevler PartitionKey üzerinde filtre uygulayarak Seattle bulur:</span><span class="sxs-lookup"><span data-stu-id="942f5-149">This example finds all tasks in Seattle by applying a filter on PartitionKey:</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="942f5-150">Giriş özellikleri alt kümesi sorgulama</span><span class="sxs-lookup"><span data-stu-id="942f5-150">Query a subset of entity properties</span></span>

<span data-ttu-id="942f5-151">Sorgudaki her bir varlık için döndürülen hangi özelliklerin de kısıtlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="942f5-151">You can also restrict which properties are returned for each entity in a query.</span></span> <span data-ttu-id="942f5-152">Adlı bu teknik *projeksiyon*, bant genişliğini azaltır ve özellikle büyük varlıklar veya sonuç kümesi için sorgu performansını iyileştirebilir.</span><span class="sxs-lookup"><span data-stu-id="942f5-152">This technique, called *projection*, reduces bandwidth and can improve query performance, especially for large entities or result sets.</span></span> <span data-ttu-id="942f5-153">Kullanım **seçin** parametre ve istediğiniz özellik adlarını istemciye döndürülen geçirin.</span><span class="sxs-lookup"><span data-stu-id="942f5-153">Use the **select** parameter and pass the names of the properties you want returned to the client.</span></span>

<span data-ttu-id="942f5-154">Aşağıdaki kod sorguda yalnızca varlıklar açıklamalarını tablodaki döndürür.</span><span class="sxs-lookup"><span data-stu-id="942f5-154">The query in the following code returns only the descriptions of entities in the table.</span></span>

> [!NOTE]
> <span data-ttu-id="942f5-155">Aşağıdaki kod parçacığını yalnızca Azure depolama karşı çalışır.</span><span class="sxs-lookup"><span data-stu-id="942f5-155">The following snippet works only against the Azure Storage.</span></span> <span data-ttu-id="942f5-156">Depolama öykünücüsü tarafından desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="942f5-156">It is not supported by the storage emulator.</span></span>

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a><span data-ttu-id="942f5-157">Bir varlığı silme</span><span class="sxs-lookup"><span data-stu-id="942f5-157">Delete an entity</span></span>

<span data-ttu-id="942f5-158">Bir varlığın PartitionKey ve RowKey için geçirerek silme [delete_entity] [ py_delete_entity] yöntemi.</span><span class="sxs-lookup"><span data-stu-id="942f5-158">Delete an entity by passing its PartitionKey and RowKey to the [delete_entity][py_delete_entity] method.</span></span>

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '001')
```

## <a name="delete-a-table"></a><span data-ttu-id="942f5-159">Bir tablo silme</span><span class="sxs-lookup"><span data-stu-id="942f5-159">Delete a table</span></span>

<span data-ttu-id="942f5-160">Bir tablo veya varlıkları hiçbirini artık ihtiyacınız varsa, çağrı [delete_table] [ py_delete_table] Azure depolama biriminden tabloyu kalıcı olarak silmek için yöntem.</span><span class="sxs-lookup"><span data-stu-id="942f5-160">If you no longer need a table or any of the entities within it, call the [delete_table][py_delete_table] method to permanently delete the table from Azure Storage.</span></span>

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a><span data-ttu-id="942f5-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="942f5-161">Next steps</span></span>

* [<span data-ttu-id="942f5-162">Azure depolama için SDK'sı Python API Başvurusu</span><span class="sxs-lookup"><span data-stu-id="942f5-162">Azure Storage SDK for Python API reference</span></span>](https://azure-storage.readthedocs.io/en/latest/index.html)
* [<span data-ttu-id="942f5-163">Azure depolama için Python SDK'sı</span><span class="sxs-lookup"><span data-stu-id="942f5-163">Azure Storage SDK for Python</span></span>](https://github.com/Azure/azure-storage-python)
* [<span data-ttu-id="942f5-164">Python Geliştirici Merkezi</span><span class="sxs-lookup"><span data-stu-id="942f5-164">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* <span data-ttu-id="942f5-165">[Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md): görsel olarak Windows, macOS ve Linux Azure Storage ile çalışmak için ücretsiz, platformlar arası bir uygulama.</span><span class="sxs-lookup"><span data-stu-id="942f5-165">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md): A free, cross-platform application for working visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

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
