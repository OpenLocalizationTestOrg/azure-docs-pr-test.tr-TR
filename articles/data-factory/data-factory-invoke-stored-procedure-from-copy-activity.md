---
title: "Azure Data Factory kopyalama etkinliği saklı yordam çağırma | Microsoft Docs"
description: "Bir Azure Data Factory kopyalama etkinliği Azure SQL Database veya SQL Server saklı bir yordam çağırma öğrenin."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: af6e4a57e726598c266ee766656aa2cc22e374e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="invoke-stored-procedure-from-copy-activity-in-azure-data-factory"></a><span data-ttu-id="41fd9-103">Kopya etkinliği Azure Data Factory içinde depolanan yordamı çağırma</span><span class="sxs-lookup"><span data-stu-id="41fd9-103">Invoke stored procedure from copy activity in Azure Data Factory</span></span>
<span data-ttu-id="41fd9-104">Veri kopyalama işlemi sırasında [SQL Server](data-factory-sqlserver-connector.md) veya [Azure SQL veritabanı](data-factory-azure-sql-connector.md), yapılandırabileceğiniz **SqlSink** bir saklı yordam çağrılacak kopyalama etkinliğinde.</span><span class="sxs-lookup"><span data-stu-id="41fd9-104">When copying data into [SQL Server](data-factory-sqlserver-connector.md) or [Azure SQL Database](data-factory-azure-sql-connector.md), you can configure the **SqlSink** in copy activity to invoke a stored procedure.</span></span> <span data-ttu-id="41fd9-105">Saklı kullanmak isteyebilirsiniz (sütun değerleri, birden çok tablo, vb. ekleme bakarak, birleştirme) herhangi bir ek işlem gerçekleştirmek için yordamı verileri hedef tabloyla eklemeden önce gereklidir.</span><span class="sxs-lookup"><span data-stu-id="41fd9-105">You may want to use the stored procedure to perform any additional processing (merging columns, looking up values, insertion into multiple tables, etc.) is required before inserting data in to the destination table.</span></span> <span data-ttu-id="41fd9-106">Bu özellik yararlandığı [tablo değerli parametreleri](https://msdn.microsoft.com/library/bb675163.aspx).</span><span class="sxs-lookup"><span data-stu-id="41fd9-106">This feature takes advantage of [Table-Valued Parameters](https://msdn.microsoft.com/library/bb675163.aspx).</span></span> 

<span data-ttu-id="41fd9-107">Aşağıdaki örnek, bir Data Factory işlem hattı (kopyalama etkinliği) SQL Server veritabanından içinde saklı yordamı çağırma gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="41fd9-107">The following sample shows how to invoke a stored procedure in a SQL Server database from a Data Factory pipeline (copy activity):</span></span>  

## <a name="output-dataset-json"></a><span data-ttu-id="41fd9-108">Çıktı veri kümesi JSON</span><span class="sxs-lookup"><span data-stu-id="41fd9-108">Output dataset JSON</span></span>
<span data-ttu-id="41fd9-109">Çıkış dataset JSON'da, ayarlayın **türü** için: **SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="41fd9-109">In the output dataset JSON, set the **type** to: **SqlServerTable**.</span></span> <span data-ttu-id="41fd9-110">Ayarlamak **AzureSqlTable** bir Azure SQL veritabanı ile kullanmak için.</span><span class="sxs-lookup"><span data-stu-id="41fd9-110">Set it to **AzureSqlTable** to use with an Azure SQL database.</span></span> <span data-ttu-id="41fd9-111">Değeri **tableName** özelliği, saklı yordamın ilk parametresinin adı eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="41fd9-111">The value for **tableName** property must match the name of first parameter of the stored procedure.</span></span>  

```json
{
  "name": "SqlOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlLinkedService",
    "typeProperties": {
      "tableName": "Marketing"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

## <a name="sqlsink-section-in-copy-activity-json"></a><span data-ttu-id="41fd9-112">Kopyalama etkinliği JSON SqlSink bölümünde</span><span class="sxs-lookup"><span data-stu-id="41fd9-112">SqlSink section in copy activity JSON</span></span>
<span data-ttu-id="41fd9-113">Tanımlamak **SqlSink** kopyalama etkinliği JSON gibi bölüm.</span><span class="sxs-lookup"><span data-stu-id="41fd9-113">Define the **SqlSink** section in the copy activity JSON as follows.</span></span> <span data-ttu-id="41fd9-114">Havuz/hedef veritabanına veri eklerken bir saklı yordam çağırmak için değerleri için her ikisini de belirtin **SqlWriterStoredProcedureName** ve **SqlWriterTableType** özellikleri.</span><span class="sxs-lookup"><span data-stu-id="41fd9-114">To invoke a stored procedure while inserting data into the sink/destination database, specify values for both **SqlWriterStoredProcedureName** and **SqlWriterTableType** properties.</span></span> <span data-ttu-id="41fd9-115">Bu özelliklerin açıklamaları için bkz: [SQL Server Bağlayıcısı makaledeki SqlSink bölümüne](data-factory-sqlserver-connector.md#sqlsink).</span><span class="sxs-lookup"><span data-stu-id="41fd9-115">For descriptions of these properties, see [SqlSink section in the SQL Server connector article](data-factory-sqlserver-connector.md#sqlsink).</span></span>

```json
"sink":
{
    "type": "SqlSink",
    "SqlWriterTableType": "MarketingType",
    "SqlWriterStoredProcedureName": "spOverwriteMarketing", 
    "storedProcedureParameters":
            {
                "stringData": 
                {
                    "value": "str1"     
                }
            }
}
```

## <a name="stored-procedure-definition"></a><span data-ttu-id="41fd9-116">Saklı yordam tanımı</span><span class="sxs-lookup"><span data-stu-id="41fd9-116">Stored procedure definition</span></span> 
<span data-ttu-id="41fd9-117">Aynı ada sahip saklı yordam veritabanınızdaki tanımlamak **SqlWriterStoredProcedureName**.</span><span class="sxs-lookup"><span data-stu-id="41fd9-117">In your database, define the stored procedure with the same name as **SqlWriterStoredProcedureName**.</span></span> <span data-ttu-id="41fd9-118">Saklı yordam kaynak veri deposu gelen giriş verilerinin işler ve hedef veritabanı tablosunda veri ekler.</span><span class="sxs-lookup"><span data-stu-id="41fd9-118">The stored procedure handles input data from the source data store, and inserts data into a table in the destination database.</span></span> <span data-ttu-id="41fd9-119">Saklı yordam ilk parametresinin adı JSON (pazarlama) kümesinde tanımlanan tableName eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="41fd9-119">The name of the first parameter of stored procedure must match the tableName defined in the dataset JSON (Marketing).</span></span>

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @stringData varchar(256)
AS
BEGIN
    DELETE FROM [dbo].[Marketing] where ProfileID = @stringData
    INSERT [dbo].[Marketing](ProfileID, State)
    SELECT * FROM @Marketing
END
```

## <a name="table-type-definition"></a><span data-ttu-id="41fd9-120">Tablo türü tanımı</span><span class="sxs-lookup"><span data-stu-id="41fd9-120">Table type definition</span></span>
<span data-ttu-id="41fd9-121">Aynı ada sahip bir tablo türü veritabanınızdaki tanımlamak **SqlWriterTableType**.</span><span class="sxs-lookup"><span data-stu-id="41fd9-121">In your database, define the table type with the same name as **SqlWriterTableType**.</span></span> <span data-ttu-id="41fd9-122">Tablo türü şeması girdi veri kümesi şeması ile eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="41fd9-122">The schema of the table type must match the schema of the input dataset.</span></span>

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL
)
```

## <a name="next-steps"></a><span data-ttu-id="41fd9-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="41fd9-123">Next steps</span></span>
<span data-ttu-id="41fd9-124">Tam JSON örnekler için makaleler aşağıdaki Bağlayıcısı'nı gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="41fd9-124">Review the following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="41fd9-125">Azure SQL Veritabanı</span><span class="sxs-lookup"><span data-stu-id="41fd9-125">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="41fd9-126">SQL Server</span><span class="sxs-lookup"><span data-stu-id="41fd9-126">SQL Server</span></span>](data-factory-sqlserver-connector.md)
