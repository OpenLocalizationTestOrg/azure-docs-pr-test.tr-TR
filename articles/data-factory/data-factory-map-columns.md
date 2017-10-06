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
# <a name="map-source-dataset-columns-toodestination-dataset-columns"></a><span data-ttu-id="c035f-103">Kaynak veri kümesi sütunları toodestination dataset sütunları eşleme</span><span class="sxs-lookup"><span data-stu-id="c035f-103">Map source dataset columns toodestination dataset columns</span></span>
<span data-ttu-id="c035f-104">Sütun eşlemesi nasıl hello Kaynak Tablo eşleme toocolumns "yapısını" belirtilen sütun hello "yapısında" havuz tablosunun belirtilen kullanılan toospecify olabilir.</span><span class="sxs-lookup"><span data-stu-id="c035f-104">Column mapping can be used toospecify how columns specified in hello “structure” of source table map toocolumns specified in hello “structure” of sink table.</span></span> <span data-ttu-id="c035f-105">Merhaba **columnMapping** özelliği hello kullanılabilir **typeProperties** hello kopyalama etkinliği bölümü.</span><span class="sxs-lookup"><span data-stu-id="c035f-105">hello **columnMapping** property is available in hello **typeProperties** section of hello Copy activity.</span></span>

<span data-ttu-id="c035f-106">Sütun eşlemesi hello aşağıdaki senaryoları destekler:</span><span class="sxs-lookup"><span data-stu-id="c035f-106">Column mapping supports hello following scenarios:</span></span>

* <span data-ttu-id="c035f-107">Tüm sütunları hello kaynak veri kümesi yapısında hello havuz veri kümesi yapısı eşlenen tooall sütunların içindedir.</span><span class="sxs-lookup"><span data-stu-id="c035f-107">All columns in hello source dataset structure are mapped tooall columns in hello sink dataset structure.</span></span>
* <span data-ttu-id="c035f-108">Eşlenen tooall sütunları hello havuz veri kümesi yapısında hello kaynak veri kümesi yapısında hello sütunların alt kümesidir.</span><span class="sxs-lookup"><span data-stu-id="c035f-108">A subset of hello columns in hello source dataset structure is mapped tooall columns in hello sink dataset structure.</span></span>

<span data-ttu-id="c035f-109">Merhaba, bir özel durum neden hata koşulları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="c035f-109">hello following are error conditions that result in an exception:</span></span>

* <span data-ttu-id="c035f-110">Daha az sütun veya "Merhaba eşlemesinde belirtilen hello"tablosunun yapısı havuz'den daha fazla sütun.</span><span class="sxs-lookup"><span data-stu-id="c035f-110">Either fewer columns or more columns in hello “structure” of sink table than specified in hello mapping.</span></span>
* <span data-ttu-id="c035f-111">Yinelenen eşleme.</span><span class="sxs-lookup"><span data-stu-id="c035f-111">Duplicate mapping.</span></span>
* <span data-ttu-id="c035f-112">SQL sorgu sonucu hello eşleme içinde belirtilen bir sütun adı yok.</span><span class="sxs-lookup"><span data-stu-id="c035f-112">SQL query result does not have a column name that is specified in hello mapping.</span></span>

> [!NOTE]
> <span data-ttu-id="c035f-113">Merhaba aşağıdaki örnekleri Azure SQL ve Azure Blob ancak dikdörtgen veri kümeleri destekleyen geçerli tooany veri deposu.</span><span class="sxs-lookup"><span data-stu-id="c035f-113">hello following samples are for Azure SQL and Azure Blob but are applicable tooany data store that supports rectangular datasets.</span></span> <span data-ttu-id="c035f-114">Veri kümesi ve örnekler toopoint toodata hello ilgili veri kaynağındaki bağlantılı hizmet tanımlarında ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c035f-114">Adjust dataset and linked service definitions in examples toopoint toodata in hello relevant data source.</span></span>

## <a name="sample-1--column-mapping-from-azure-sql-tooazure-blob"></a><span data-ttu-id="c035f-115">Örnek 1 – sütun Azure SQL tooAzure blobundan eşleme</span><span class="sxs-lookup"><span data-stu-id="c035f-115">Sample 1 – column mapping from Azure SQL tooAzure blob</span></span>
<span data-ttu-id="c035f-116">Bu örnekte hello giriş tablosu yapısının ve bir Azure SQL veritabanında tooa SQL tablosunu işaret eder.</span><span class="sxs-lookup"><span data-stu-id="c035f-116">In this sample, hello input table has a structure and it points tooa SQL table in an Azure SQL database.</span></span>

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

<span data-ttu-id="c035f-117">Bu örnekte, bir yapı hello çıkış tablosuna sahip ve Azure blob depolama alanına tooa blob işaret eder.</span><span class="sxs-lookup"><span data-stu-id="c035f-117">In this sample, hello output table has a structure and it points tooa blob in an Azure blob storage.</span></span>

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

<span data-ttu-id="c035f-118">JSON aşağıdaki hello kopyalama etkinliği ardışık düzeninde tanımlar.</span><span class="sxs-lookup"><span data-stu-id="c035f-118">hello following JSON defines a copy activity in a pipeline.</span></span> <span data-ttu-id="c035f-119">Kaynak Hello sütunlarından eşlenen havuzunda toocolumns (**columnMappings**) hello kullanarak **Çeviricisi** özelliği.</span><span class="sxs-lookup"><span data-stu-id="c035f-119">hello columns from source mapped toocolumns in sink (**columnMappings**) by using hello **Translator** property.</span></span>

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
<span data-ttu-id="c035f-120">**Sütun eşlemesi akışı:**</span><span class="sxs-lookup"><span data-stu-id="c035f-120">**Column mapping flow:**</span></span>

![Sütun eşlemesi akışı](./media/data-factory-map-columns/column-mapping-flow.png)

## <a name="sample-2--column-mapping-with-sql-query-from-azure-sql-tooazure-blob"></a><span data-ttu-id="c035f-122">Örnek 2 – sütun Azure SQL tooAzure blob SQL sorgusu ile eşleme</span><span class="sxs-lookup"><span data-stu-id="c035f-122">Sample 2 – column mapping with SQL query from Azure SQL tooAzure blob</span></span>
<span data-ttu-id="c035f-123">Bu örnekte, bir SQL sorgusu kullanılan tooextract Azure SQL yalnızca hello tablo adı ve hello sütun adları "yapısı" bölümünde belirtmek yerine verilerdir.</span><span class="sxs-lookup"><span data-stu-id="c035f-123">In this sample, a SQL query is used tooextract data from Azure SQL instead of simply specifying hello table name and hello column names in “structure” section.</span></span> 

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
<span data-ttu-id="c035f-124">Bu durumda, hello sorgu sonuçları kaynak "yapısı" içinde belirtilen ilk eşlenen toocolumns olur.</span><span class="sxs-lookup"><span data-stu-id="c035f-124">In this case, hello query results are first mapped toocolumns specified in “structure” of source.</span></span> <span data-ttu-id="c035f-125">Ardından, kaynak "yapısı" Merhaba sütunlarından kuralları columnMappings içinde belirtilen "yapısıyla" havuzunda eşlenen toocolumns ' dir.</span><span class="sxs-lookup"><span data-stu-id="c035f-125">Next, hello columns from source “structure” are mapped toocolumns in sink “structure” with rules specified in columnMappings.</span></span>  <span data-ttu-id="c035f-126">Merhaba sorgunun döndürdüğü 5 sütun, hello kaynak "yapısını" belirtilenlerden iki sütun daha varsayalım.</span><span class="sxs-lookup"><span data-stu-id="c035f-126">Suppose hello query returns 5 columns, two more columns than those specified in hello “structure” of source.</span></span>

<span data-ttu-id="c035f-127">**Sütun eşlemesi akışı**</span><span class="sxs-lookup"><span data-stu-id="c035f-127">**Column mapping flow**</span></span>

![Sütun eşlemesi akış-2](./media/data-factory-map-columns/column-mapping-flow-2.png)

## <a name="next-steps"></a><span data-ttu-id="c035f-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c035f-129">Next steps</span></span>
<span data-ttu-id="c035f-130">Kopyalama etkinliği kullanma hakkında bir öğretici Hello makalesine bakın:</span><span class="sxs-lookup"><span data-stu-id="c035f-130">See hello article for a tutorial on using Copy Activity:</span></span> 

- [<span data-ttu-id="c035f-131">Blob Storage tooSQL veritabanı verilerini kopyalama</span><span class="sxs-lookup"><span data-stu-id="c035f-131">Copy data from Blob Storage tooSQL Database</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
