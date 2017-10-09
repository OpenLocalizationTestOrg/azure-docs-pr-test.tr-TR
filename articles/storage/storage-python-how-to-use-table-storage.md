---
title: Python ile Azure Table depolama aaaHow toouse | Microsoft Docs
description: "Bir NoSQL veri deposu olan Azure Table storage kullanılarak hello bulutta yapılandırılmış veri depolayın."
services: storage
documentationcenter: python
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 7ddb9f3e-4e6d-4103-96e6-f0351d69a17b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/16/2017
ms.author: marsma
ms.openlocfilehash: fd0e1b05cc12618f348eaf2d85d0dce5ac32702a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-in-python"></a>Nasıl toouse Python tablo depolama

[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

Bu kılavuz size nasıl tooperform ortak Azure Table depolama senaryolarda kullanarak Python hello gösterir [Python için Microsoft Azure depolama SDK](https://github.com/Azure/azure-storage-python). Kapsanan hello senaryolar oluşturma ve bir tablo, silme ve ekleme ve varlıkları sorgulama içerir.

Çalışırken hello senaryoları aracılığıyla Bu öğreticide, toorefer toohello isteyebilir [Python API Başvurusu için Azure depolama SDK'sı](https://azure-storage.readthedocs.io/en/latest/index.html).

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="install-hello-azure-storage-sdk-for-python"></a>Python için Hello Azure depolama SDK'sını yükleyin

Bir depolama hesabı oluşturduktan sonra sonraki adımınız tooinstall hello olan [Python için Microsoft Azure depolama SDK](https://github.com/Azure/azure-storage-python). SDK yükleme ile ilgili ayrıntılar hello için toohello başvuran [README.rst](https://github.com/Azure/azure-storage-python/blob/master/README.rst) dosyasında hello depolama SDK'sı Python deposu için github'da.

## <a name="create-a-table"></a>Bir tablo oluşturma

toowork hello Python Azure tablo hizmeti ile içeri aktarmanız gerekir hello [TableService] [ py_TableService] modülü. Tablo varlıklarla çalışmaya beri hello etmeniz [varlık] [ py_Entity] sınıfı. Bu kodu hello üstüne yakın, Python dosyası tooimport hem ekleyin:

```python
from azure.storage.table import TableService, Entity
```

Oluşturma bir [TableService] [ py_TableService] nesnesi, depolama hesabı adı ve hesap anahtarınızı geçirme. Değiştir `myaccount` ve `mykey` hesap adı ve anahtar ve çağrı [create_table] [ py_create_table] toocreate hello Azure Storage tablosunda.

```python
table_service = TableService(account_name='myaccount', account_key='mykey')

table_service.create_table('tasktable')
```

## <a name="add-an-entity-tooa-table"></a>Bir varlık tooa tablo ekleme

tooadd varlık önce oluşturmanız, varlık, ardından geçişi hello nesne toohello temsil eden bir nesne [TableService][py_TableService].[ insert_entity] [ py_insert_entity] yöntemi. Merhaba varlığı nesnesi, bir sözlük veya türünde bir nesne olabilir [varlık][py_Entity]ve, varlığın özellik adlarını ve değerlerini tanımlar. Her varlık gerekli hello içermelidir [PartitionKey ve RowKey](#partitionkey-and-rowkey) özellikleri, ayrıca tooany diğer özellikleri hello varlık için tanımladığınız.

Bu örnek, bir sözlük nesnesi oluşturur. bir varlığı temsil eden daha sonra geçirir, toohello [insert_entity] [ py_insert_entity] yöntemi tooadd, toohello tablosu:

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello trash', 'priority' : 200}
table_service.insert_entity('tasktable', task)
```

Bu örnekte bir [varlık] [ py_Entity] nesne sonra toohello geçirir [insert_entity] [ py_insert_entity] yöntemi tooadd, toohello tablosu:

```python
task = Entity()
task.PartitionKey = 'tasksSeattle'
task.RowKey = '002'
task.description = 'Wash hello car'
task.priority = 100
table_service.insert_entity('tasktable', task)
```

### <a name="partitionkey-and-rowkey"></a>PartitionKey ve RowKey

Her ikisini de belirtmelisiniz bir **PartitionKey** ve **RowKey** özelliği her varlık için. Merhaba, varlıklarınızı öğesinin benzersiz tanımlayıcıları olarak birlikte bunlar bir varlığın hello birincil anahtarı oluşturur. Bu değerleri yalnızca bu özellikleri dizine olduğundan başka bir varlık özellikleri sorgulayabilirsiniz çok daha hızlı kullanarak sorgulayabilirsiniz.

Tablo hizmeti kullanan hello **PartitionKey** toointelligently depolama düğümleri arasında tablo varlıkları dağıtın. Sahip varlıkları aynı hello **PartitionKey** hello üzerinde depolanan aynı düğüm. **RowKey** ait hello bölüm içinde hello varlığın hello benzersiz kimliğidir.

## <a name="update-an-entity"></a>Bir varlığı güncelleştirir

Tüm tooupdate hello bir varlığın özellik değerlerinin ikisinin de, çağrı [update_entity] [ py_update_entity] yöntemi. Bu örnekte gösterilir nasıl tooreplace var olan bir varlığı güncelleştirilmiş bir sürüm:

```python
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage', 'priority' : 250}
table_service.update_entity('tasktable', task)
```

Güncelleştirilmekte hello varlık zaten mevcut değilse hello güncelleştirme işlemi başarısız olur. Veya var olup olmadığını toostore bir varlık istiyorsanız kullanın [insert_or_replace_entity][py_insert_or_replace_entity]. Aşağıdaki örneğine hello hello ilk çağrıda hello varolan varlık yerini alır. Merhaba ikinci çağrı yeni bir varlık ekler, hiçbir varlık hello ile PartitionKey ve RowKey belirtilen beri hello tablosunda mevcut.

```python
# Replace hello entity created earlier
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '001', 'description' : 'Take out hello garbage again', 'priority' : 250}
table_service.insert_or_replace_entity('tasktable', task)

# Insert a new entity
task = {'PartitionKey': 'tasksSeattle', 'RowKey': '003', 'description' : 'Buy detergent', 'priority' : 300}
table_service.insert_or_replace_entity('tasktable', task)
```

> [!TIP]
> Merhaba [update_entity] [ py_update_entity] yöntemi, tüm özellikler ve ayrıca varolan bir varlığına değerlerini değiştirir var olan bir varlığı tooremove özelliklerinden kullanın. Merhaba kullanabilirsiniz [merge_entity] [ py_merge_entity] yöntemi tooupdate tamamen hello varlık değiştirme olmadan yeni veya değiştirilmiş özellik değerlerini sahip varolan bir varlık.

## <a name="modify-multiple-entities"></a>Birden çok varlık değiştirme

tooensure hello tablo hizmeti tarafından atomik bir isteğin işlenmesi Merhaba, birden çok işlemlerinde birlikte bir toplu gönderebilirsiniz. İlk olarak, hello kullanın [TableBatch] [ py_TableBatch] tooadd birden çok operations tooa tek toplu sınıfı. Ardından, çağrı [TableService][py_TableService].[ commit_batch] [ py_commit_batch] toosubmit hello işlemlerinde atomik bir işlem. Toplu işlemde değiştiren tüm varlıkları toobe hello olmalıdır aynı bölüm.

Bu örnek iki varlık bir toplu işlemde toplar:

```python
from azure.storage.table import TableBatch
batch = TableBatch()
task004 = {'PartitionKey': 'tasksSeattle', 'RowKey': '004', 'description' : 'Go grocery shopping', 'priority' : 400}
task005 = {'PartitionKey': 'tasksSeattle', 'RowKey': '005', 'description' : 'Clean hello bathroom', 'priority' : 100}
batch.insert_entity(task004)
batch.insert_entity(task005)
table_service.commit_batch('tasktable', batch)
```

Toplu hello İçerik Yöneticisi sözdizimi ile de kullanılabilir:

```python
task006 = {'PartitionKey': 'tasksSeattle', 'RowKey': '006', 'description' : 'Go grocery shopping', 'priority' : 400}
task007 = {'PartitionKey': 'tasksSeattle', 'RowKey': '007', 'description' : 'Clean hello bathroom', 'priority' : 100}

with table_service.batch('tasktable') as batch:
    batch.insert_entity(task006)
    batch.insert_entity(task007)
```

## <a name="query-for-an-entity"></a>Bir varlık için sorgu

tooquery bir tabloda, bir varlığın PartitionKey ve RowKey toohello geçirmek [TableService][py_TableService].[ get_entity] [ py_get_entity] yöntemi.

```python
task = table_service.get_entity('tasktable', 'tasksSeattle', '001')
print(task.description)
print(task.priority)
```

## <a name="query-a-set-of-entities"></a>Varlık kümesi sorgulama

Varlık kümesi için bir filtre dizesi hello ile sağlayarak Sorgulayabileceğiniz **filtre** parametresi. Bu örnekte, tüm görevler PartitionKey üzerinde filtre uygulayarak Seattle bulur:

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'")
for task in tasks:
    print(task.description)
    print(task.priority)
```

## <a name="query-a-subset-of-entity-properties"></a>Giriş özellikleri alt kümesi sorgulama

Sorgudaki her bir varlık için döndürülen hangi özelliklerin de kısıtlayabilirsiniz. Adlı bu teknik *projeksiyon*, bant genişliğini azaltır ve özellikle büyük varlıklar veya sonuç kümesi için sorgu performansını iyileştirebilir. Kullanım hello **seçin** parametre ve geçişi hello adları istediğiniz hello özelliklerinin toohello istemci döndürdü.

koddan hello Hello sorguda yalnızca hello açıklamaları varlıkların hello tablodaki döndürür.

> [!NOTE]
> Aşağıdaki kod parçacığında works yalnızca hello Azure Storage karşı hello. Merhaba depolama öykünücüsü tarafından desteklenmiyor.

```python
tasks = table_service.query_entities('tasktable', filter="PartitionKey eq 'tasksSeattle'", select='description')
for task in tasks:
    print(task.description)
```

## <a name="delete-an-entity"></a>Bir varlığı silme

Bir varlığın PartitionKey ve RowKey toohello geçirerek silme [delete_entity] [ py_delete_entity] yöntemi.

```python
table_service.delete_entity('tasktable', 'tasksSeattle', '001')
```

## <a name="delete-a-table"></a>Bir tablo silme

Bir tablo veya hello varlıkları hiçbirini artık ihtiyacınız varsa, hello çağrısı [delete_table] [ py_delete_table] yöntemi toopermanently Azure depolama biriminden hello Tablo Sil.

```python
table_service.delete_table('tasktable')
```

## <a name="next-steps"></a>Sonraki adımlar

* [Azure depolama için SDK'sı Python API Başvurusu](https://azure-storage.readthedocs.io/en/latest/index.html)
* [Azure depolama için Python SDK'sı](https://github.com/Azure/azure-storage-python)
* [Python Geliştirici Merkezi](https://azure.microsoft.com/develop/python/)
* [Microsoft Azure Storage Gezgini](../vs-azure-tools-storage-manage-with-storage-explorer.md): görsel olarak Windows, macOS ve Linux Azure Storage ile çalışmak için ücretsiz, platformlar arası bir uygulama.

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
