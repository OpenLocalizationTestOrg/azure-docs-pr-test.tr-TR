---
title: "aaaInvoke saklı yordamı Azure veri fabrikası kopyalama etkinliğinden | Microsoft Docs"
description: "Nasıl tooinvoke saklı yordam, Azure SQL Database veya SQL Server'dan Azure Data Factory kopyalama etkinliği hakkında bilgi edinin."
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
ms.openlocfilehash: 986377118afb8c08607c2325fcc3ab00b3de9268
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-stored-procedure-from-copy-activity-in-azure-data-factory"></a><span data-ttu-id="90c40-103">Kopya etkinliği Azure Data Factory içinde depolanan yordamı çağırma</span><span class="sxs-lookup"><span data-stu-id="90c40-103">Invoke stored procedure from copy activity in Azure Data Factory</span></span>
<span data-ttu-id="90c40-104">Veri kopyalama işlemi sırasında [SQL Server](data-factory-sqlserver-connector.md) veya [Azure SQL veritabanı](data-factory-azure-sql-connector.md), hello yapılandırabilirsiniz **SqlSink** kopyalama etkinliği tooinvoke bir saklı yordam içinde.</span><span class="sxs-lookup"><span data-stu-id="90c40-104">When copying data into [SQL Server](data-factory-sqlserver-connector.md) or [Azure SQL Database](data-factory-azure-sql-connector.md), you can configure hello **SqlSink** in copy activity tooinvoke a stored procedure.</span></span> <span data-ttu-id="90c40-105">(Sütun değerleri, birden çok tablo, vb. ekleme bakarak, birleştirme) herhangi bir ek işlem toohello hedef tabloda veri eklemeden önce gerekli toouse hello saklı yordamı tooperform isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="90c40-105">You may want toouse hello stored procedure tooperform any additional processing (merging columns, looking up values, insertion into multiple tables, etc.) is required before inserting data in toohello destination table.</span></span> <span data-ttu-id="90c40-106">Bu özellik yararlandığı [tablo değerli parametreleri](https://msdn.microsoft.com/library/bb675163.aspx).</span><span class="sxs-lookup"><span data-stu-id="90c40-106">This feature takes advantage of [Table-Valued Parameters](https://msdn.microsoft.com/library/bb675163.aspx).</span></span> 

<span data-ttu-id="90c40-107">Aşağıdaki örnek hello nasıl tooinvoke saklı yordam, bir SQL Server veritabanını Data Factory işlem hattı (kopyalama etkinliği) gösterir:</span><span class="sxs-lookup"><span data-stu-id="90c40-107">hello following sample shows how tooinvoke a stored procedure in a SQL Server database from a Data Factory pipeline (copy activity):</span></span>  

## <a name="output-dataset-json"></a><span data-ttu-id="90c40-108">Çıktı veri kümesi JSON</span><span class="sxs-lookup"><span data-stu-id="90c40-108">Output dataset JSON</span></span>
<span data-ttu-id="90c40-109">Merhaba çıkış dataset JSON, hello ayarlayın **türü** için: **SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="90c40-109">In hello output dataset JSON, set hello **type** to: **SqlServerTable**.</span></span> <span data-ttu-id="90c40-110">Çok ayarlamak**AzureSqlTable** toouse bir Azure SQL veritabanı ile.</span><span class="sxs-lookup"><span data-stu-id="90c40-110">Set it too**AzureSqlTable** toouse with an Azure SQL database.</span></span> <span data-ttu-id="90c40-111">Merhaba değeri **tableName** özelliği hello saklı yordamın ilk parametresinin hello adı eşleşmelidir.</span><span class="sxs-lookup"><span data-stu-id="90c40-111">hello value for **tableName** property must match hello name of first parameter of hello stored procedure.</span></span>  

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

## <a name="sqlsink-section-in-copy-activity-json"></a><span data-ttu-id="90c40-112">Kopyalama etkinliği JSON SqlSink bölümünde</span><span class="sxs-lookup"><span data-stu-id="90c40-112">SqlSink section in copy activity JSON</span></span>
<span data-ttu-id="90c40-113">Merhaba tanımlamak **SqlSink** hello kopyalama etkinliği JSON gibi bölüm.</span><span class="sxs-lookup"><span data-stu-id="90c40-113">Define hello **SqlSink** section in hello copy activity JSON as follows.</span></span> <span data-ttu-id="90c40-114">tooinvoke hello havuz/hedef veritabanına veri ekleme sırasında bir saklı yordam her ikisi için değerleri belirtin **SqlWriterStoredProcedureName** ve **SqlWriterTableType** özellikleri.</span><span class="sxs-lookup"><span data-stu-id="90c40-114">tooinvoke a stored procedure while inserting data into hello sink/destination database, specify values for both **SqlWriterStoredProcedureName** and **SqlWriterTableType** properties.</span></span> <span data-ttu-id="90c40-115">Bu özelliklerin açıklamaları için bkz: [hello SQL Server Bağlayıcısı makaledeki SqlSink bölümüne](data-factory-sqlserver-connector.md#sqlsink).</span><span class="sxs-lookup"><span data-stu-id="90c40-115">For descriptions of these properties, see [SqlSink section in hello SQL Server connector article](data-factory-sqlserver-connector.md#sqlsink).</span></span>

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

## <a name="stored-procedure-definition"></a><span data-ttu-id="90c40-116">Saklı yordam tanımı</span><span class="sxs-lookup"><span data-stu-id="90c40-116">Stored procedure definition</span></span> 
<span data-ttu-id="90c40-117">Aynı ad olarak hello hello depolanan yordamla veritabanınızdaki tanımlamak **SqlWriterStoredProcedureName**.</span><span class="sxs-lookup"><span data-stu-id="90c40-117">In your database, define hello stored procedure with hello same name as **SqlWriterStoredProcedureName**.</span></span> <span data-ttu-id="90c40-118">Merhaba saklı yordamı hello kaynak veri deposu gelen giriş verilerinin işler ve veri hello hedef veritabanındaki bir tablo ekler.</span><span class="sxs-lookup"><span data-stu-id="90c40-118">hello stored procedure handles input data from hello source data store, and inserts data into a table in hello destination database.</span></span> <span data-ttu-id="90c40-119">saklı yordam hello ilk parametresinin Hello adı JSON (pazarlama) hello kümesinde tanımlanan hello tableName eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="90c40-119">hello name of hello first parameter of stored procedure must match hello tableName defined in hello dataset JSON (Marketing).</span></span>

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @stringData varchar(256)
AS
BEGIN
    DELETE FROM [dbo].[Marketing] where ProfileID = @stringData
    INSERT [dbo].[Marketing](ProfileID, State)
    SELECT * FROM @Marketing
END
```

## <a name="table-type-definition"></a><span data-ttu-id="90c40-120">Tablo türü tanımı</span><span class="sxs-lookup"><span data-stu-id="90c40-120">Table type definition</span></span>
<span data-ttu-id="90c40-121">Merhaba tablo türü ile aynı adı olarak hello veritabanınızdaki tanımlamak **SqlWriterTableType**.</span><span class="sxs-lookup"><span data-stu-id="90c40-121">In your database, define hello table type with hello same name as **SqlWriterTableType**.</span></span> <span data-ttu-id="90c40-122">Merhaba tablo türü Hello şeması hello girdi veri kümesi hello şeması eşleşmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="90c40-122">hello schema of hello table type must match hello schema of hello input dataset.</span></span>

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL
)
```

## <a name="next-steps"></a><span data-ttu-id="90c40-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="90c40-123">Next steps</span></span>
<span data-ttu-id="90c40-124">Merhaba, JSON örnekleri tamamlamak için bağlayıcı makaleler gözden geçirin:</span><span class="sxs-lookup"><span data-stu-id="90c40-124">Review hello following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="90c40-125">Azure SQL Veritabanı</span><span class="sxs-lookup"><span data-stu-id="90c40-125">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="90c40-126">SQL Server</span><span class="sxs-lookup"><span data-stu-id="90c40-126">SQL Server</span></span>](data-factory-sqlserver-connector.md)
