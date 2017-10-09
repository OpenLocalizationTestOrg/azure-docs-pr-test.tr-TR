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
# <a name="invoke-stored-procedure-from-copy-activity-in-azure-data-factory"></a>Kopya etkinliği Azure Data Factory içinde depolanan yordamı çağırma
Veri kopyalama işlemi sırasında [SQL Server](data-factory-sqlserver-connector.md) veya [Azure SQL veritabanı](data-factory-azure-sql-connector.md), hello yapılandırabilirsiniz **SqlSink** kopyalama etkinliği tooinvoke bir saklı yordam içinde. (Sütun değerleri, birden çok tablo, vb. ekleme bakarak, birleştirme) herhangi bir ek işlem toohello hedef tabloda veri eklemeden önce gerekli toouse hello saklı yordamı tooperform isteyebilirsiniz. Bu özellik yararlandığı [tablo değerli parametreleri](https://msdn.microsoft.com/library/bb675163.aspx). 

Aşağıdaki örnek hello nasıl tooinvoke saklı yordam, bir SQL Server veritabanını Data Factory işlem hattı (kopyalama etkinliği) gösterir:  

## <a name="output-dataset-json"></a>Çıktı veri kümesi JSON
Merhaba çıkış dataset JSON, hello ayarlayın **türü** için: **SqlServerTable**. Çok ayarlamak**AzureSqlTable** toouse bir Azure SQL veritabanı ile. Merhaba değeri **tableName** özelliği hello saklı yordamın ilk parametresinin hello adı eşleşmelidir.  

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

## <a name="sqlsink-section-in-copy-activity-json"></a>Kopyalama etkinliği JSON SqlSink bölümünde
Merhaba tanımlamak **SqlSink** hello kopyalama etkinliği JSON gibi bölüm. tooinvoke hello havuz/hedef veritabanına veri ekleme sırasında bir saklı yordam her ikisi için değerleri belirtin **SqlWriterStoredProcedureName** ve **SqlWriterTableType** özellikleri. Bu özelliklerin açıklamaları için bkz: [hello SQL Server Bağlayıcısı makaledeki SqlSink bölümüne](data-factory-sqlserver-connector.md#sqlsink).

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

## <a name="stored-procedure-definition"></a>Saklı yordam tanımı 
Aynı ad olarak hello hello depolanan yordamla veritabanınızdaki tanımlamak **SqlWriterStoredProcedureName**. Merhaba saklı yordamı hello kaynak veri deposu gelen giriş verilerinin işler ve veri hello hedef veritabanındaki bir tablo ekler. saklı yordam hello ilk parametresinin Hello adı JSON (pazarlama) hello kümesinde tanımlanan hello tableName eşleşmesi gerekir.

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @stringData varchar(256)
AS
BEGIN
    DELETE FROM [dbo].[Marketing] where ProfileID = @stringData
    INSERT [dbo].[Marketing](ProfileID, State)
    SELECT * FROM @Marketing
END
```

## <a name="table-type-definition"></a>Tablo türü tanımı
Merhaba tablo türü ile aynı adı olarak hello veritabanınızdaki tanımlamak **SqlWriterTableType**. Merhaba tablo türü Hello şeması hello girdi veri kümesi hello şeması eşleşmesi gerekir.

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL
)
```

## <a name="next-steps"></a>Sonraki adımlar
Merhaba, JSON örnekleri tamamlamak için bağlayıcı makaleler gözden geçirin: 

- [Azure SQL Veritabanı](data-factory-azure-sql-connector.md)
- [SQL Server](data-factory-sqlserver-connector.md)
