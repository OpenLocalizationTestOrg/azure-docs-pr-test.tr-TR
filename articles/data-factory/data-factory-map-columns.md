---
title: "Azure Data Factory veri kümesi sütunlarında aaaMapping | Microsoft Docs"
description: "Nasıl toomap kaynak sütunları toodestination sütunları öğrenin."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 8f78d4af675bec0a70e5f6e83ec1ffb511408b5a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="map-source-dataset-columns-toodestination-dataset-columns"></a>Kaynak veri kümesi sütunları toodestination dataset sütunları eşleme
Sütun eşlemesi nasıl hello Kaynak Tablo eşleme toocolumns "yapısını" belirtilen sütun hello "yapısında" havuz tablosunun belirtilen kullanılan toospecify olabilir. Merhaba **columnMapping** özelliği hello kullanılabilir **typeProperties** hello kopyalama etkinliği bölümü.

Sütun eşlemesi hello aşağıdaki senaryoları destekler:

* Tüm sütunları hello kaynak veri kümesi yapısında hello havuz veri kümesi yapısı eşlenen tooall sütunların içindedir.
* Eşlenen tooall sütunları hello havuz veri kümesi yapısında hello kaynak veri kümesi yapısında hello sütunların alt kümesidir.

Merhaba, bir özel durum neden hata koşulları şunlardır:

* Daha az sütun veya "Merhaba eşlemesinde belirtilen hello"tablosunun yapısı havuz'den daha fazla sütun.
* Yinelenen eşleme.
* SQL sorgu sonucu hello eşleme içinde belirtilen bir sütun adı yok.

> [!NOTE]
> Merhaba aşağıdaki örnekleri Azure SQL ve Azure Blob ancak dikdörtgen veri kümeleri destekleyen geçerli tooany veri deposu. Veri kümesi ve örnekler toopoint toodata hello ilgili veri kaynağındaki bağlantılı hizmet tanımlarında ayarlayın.

## <a name="sample-1--column-mapping-from-azure-sql-tooazure-blob"></a>Örnek 1 – sütun Azure SQL tooAzure blobundan eşleme
Bu örnekte hello giriş tablosu yapısının ve bir Azure SQL veritabanında tooa SQL tablosunu işaret eder.

```json
{
    "name": "AzureSQLInput",
    "properties": {
        "structure": 
         [
           { "name": "userid"},
           { "name": "name"},
           { "name": "group"}
         ],
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```

Bu örnekte, bir yapı hello çıkış tablosuna sahip ve Azure blob depolama alanına tooa blob işaret eder.

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
         "structure": 
          [
                { "name": "myuserid"},
                { "name": "myname" },
                { "name": "mygroup"}
          ],
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder",
            "fileName":"myfile.csv",
            "format":
            {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

JSON aşağıdaki hello kopyalama etkinliği ardışık düzeninde tanımlar. Kaynak Hello sütunlarından eşlenen havuzunda toocolumns (**columnMappings**) hello kullanarak **Çeviricisi** özelliği.

```json
{
    "name": "CopyActivity",
    "description": "description", 
    "type": "Copy",
    "inputs":  [ { "name": "AzureSQLInput"  } ],
    "outputs":  [ { "name": "AzureBlobOutput" } ],
    "typeProperties":    {
        "source":
        {
            "type": "SqlSource"
        },
        "sink":
        {
            "type": "BlobSink"
        },
        "translator": 
        {
            "type": "TabularTranslator",
            "ColumnMappings": "UserId: MyUserId, Group: MyGroup, Name: MyName"
        }
    },
   "scheduler": {
          "frequency": "Hour",
          "interval": 1
        }
}
```
**Sütun eşlemesi akışı:**

![Sütun eşlemesi akışı](./media/data-factory-map-columns/column-mapping-flow.png)

## <a name="sample-2--column-mapping-with-sql-query-from-azure-sql-tooazure-blob"></a>Örnek 2 – sütun Azure SQL tooAzure blob SQL sorgusu ile eşleme
Bu örnekte, bir SQL sorgusu kullanılan tooextract Azure SQL yalnızca hello tablo adı ve hello sütun adları "yapısı" bölümünde belirtmek yerine verilerdir. 

```json
{
    "name": "CopyActivity",
    "description": "description", 
    "type": "CopyActivity",
    "inputs":  [ { "name": " AzureSQLInput"  } ],
    "outputs":  [ { "name": " AzureBlobOutput" } ],
    "typeProperties":
    {
        "source":
        {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartDateTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
        },
        "sink":
        {
            "type": "BlobSink"
        },
        "Translator": 
        {
            "type": "TabularTranslator",
            "ColumnMappings": "UserId: MyUserId, Group: MyGroup,Name: MyName"
        }
    },
    "scheduler": {
          "frequency": "Hour",
          "interval": 1
        }
}
```
Bu durumda, hello sorgu sonuçları kaynak "yapısı" içinde belirtilen ilk eşlenen toocolumns olur. Ardından, kaynak "yapısı" Merhaba sütunlarından kuralları columnMappings içinde belirtilen "yapısıyla" havuzunda eşlenen toocolumns ' dir.  Merhaba sorgunun döndürdüğü 5 sütun, hello kaynak "yapısını" belirtilenlerden iki sütun daha varsayalım.

**Sütun eşlemesi akışı**

![Sütun eşlemesi akış-2](./media/data-factory-map-columns/column-mapping-flow-2.png)

## <a name="next-steps"></a>Sonraki adımlar
Kopyalama etkinliği kullanma hakkında bir öğretici Hello makalesine bakın: 

- [Blob Storage tooSQL veritabanı verilerini kopyalama](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
