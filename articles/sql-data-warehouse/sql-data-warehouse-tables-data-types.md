---
title: "Azure SQL Data Warehouse aaaData türleri Kılavuzu - | Microsoft Docs"
description: "Öneriler toodefine veri türleri SQL Data Warehouse ile uyumlu değildir."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: d4a1f0a3-ba9f-44b9-95f6-16a4f30746d6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 06/02/2017
ms.author: shigu;barbkess
ms.openlocfilehash: a2f7a394feb73d273b25101735b00eb12db2b292
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="guidance-for-defining-data-types-for-tables-in-sql-data-warehouse"></a>SQL veri ambarı'nda tabloları veri türlerini tanımlama Kılavuzu
SQL veri ambarı ile uyumlu olan bu önerileri toodefine tablo veri türlerini kullanın. Ayrıca veri türlerinin hello boyutu en aza toocompatibility, sorgu performansı artırır.

SQL veri ambarı hello en yaygın olarak kullanılan veri türlerini destekler. Desteklenen hello veri türlerinin listesi için bkz: [veri türleri](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes) hello CREATE TABLE deyimi içinde. 


## <a name="minimize-row-length"></a>Satır uzunluğu simge durumuna küçült
Veri türlerinin Hello boyutu en aza toobetter sorgu performansı müşteri adayları hello satır uzunluğu kısaltır. Çalışan hello en küçük veri türü, verileriniz için kullanın. 

- Büyük varsayılan uzunluk karakter sütunlarla tanımlamamaya özen gösterin. Örneğin, Hello uzun değer 25 karakterden oluşuyorsa, sütun VARCHAR(25) tanımlayın. 
- Kullanmaktan kaçının [NVARCHAR] [ NVARCHAR] yalnızca gerektiğinde VARCHAR.
- Mümkün olduğunda, NVARCHAR(4000) veya VARCHAR(8000) NVARCHAR(MAX) veya VARCHAR(MAX) yerine kullanın.

Polybase tooload tabloları kullanıyorsanız, 1 MB hello tablo satırı tanımlanan hello uzunluğu aşamaz. Değişken uzunluklu veri sahip bir satır 1 MB aştığında hello satır ile BCP, ancak değil PolyBase yükleyebilirsiniz.

## <a name="identify-unsupported-data-types"></a>Desteklenmeyen veri türlerini tanımlayın
Başka bir SQL veritabanı, veritabanınızı geçiriyorsanız, SQL veri ambarı'nda desteklenmeyen veri türleri karşılaşabilirsiniz. Bu sorgu toodiscover desteklenmeyen veri türleri, var olan SQL şemasında kullanın.

```sql
SELECT  t.[name], c.[name], c.[system_type_id], c.[user_type_id], y.[is_user_defined], y.[name]
FROM sys.tables  t
JOIN sys.columns c on t.[object_id]    = c.[object_id]
JOIN sys.types   y on c.[user_type_id] = y.[user_type_id]
WHERE y.[name] IN ('geography','geometry','hierarchyid','image','text','ntext','sql_variant','timestamp','xml')
 AND  y.[is_user_defined] = 1;
```


## <a name="unsupported-data-types"></a>Desteklenmeyen veri türleri için kullanım geçici çözümler

Merhaba aşağıdaki listede hello SQL Data Warehouse desteklemediği veri türleri gösterir ve hello yerine kullanabileceğiniz verir alternatifleri veri türleri desteklenmiyor.

| Desteklenmeyen veri türü | Geçici çözüm |
| --- | --- |
| [geometri][geometry] |[varbinary][varbinary] |
| [coğrafi konum][geography] |[varbinary][varbinary] |
| [HierarchyId][hierarchyid] |[nvarchar][nvarchar](4000) |
| [Görüntü][ntext,text,image] |[varbinary][varbinary] |
| [metin][ntext,text,image] |[varchar][varchar] |
| [ntext][ntext,text,image] |[nvarchar][nvarchar] |
| [sql_variant][sql_variant] |Sütun birkaç kesin türü belirtilmiş sütuna bölün. |
| [Tablo][table] |Tootemporary tabloları Dönüştür. |
| [zaman damgası][timestamp] |Kod toouse rework [datetime2] [ datetime2] ve `CURRENT_TIMESTAMP` işlevi.  Yalnızca sabit değerleri desteklenir varsayılan olarak, bu nedenle current_timestamp varsayılan kısıtlama olarak tanımlanamaz. Toomigrate satır sürümü bir zaman damgası yazılan sütun değerlerinden ihtiyacınız varsa, daha sonra kullanmak [ikili][BINARY](8) veya [VARBINARY][BINARY](8) için NOT NULL veya Satır sürümü değerleri NULL. |
| [XML][xml] |[varchar][varchar] |
| [Kullanıcı tanımlı tür][user defined types] |Mümkün olduğunda geri toohello yerel veri türüne dönüştürün. |
| Varsayılan değerler | Varsayılan değerleri değişmez değerleri ve yalnızca sabitleri desteklemez.  Belirleyici olmayan ifadeleri ve İşlevler, gibi `GETDATE()` veya `CURRENT_TIMESTAMP`, desteklenmez. |


## <a name="next-steps"></a>Sonraki adımlar
toolearn daha bakın:

- [SQL veri ambarı en iyi uygulamalar][SQL Data Warehouse Best Practices]
- [Tablo genel bakış][Overview]
- [Bir tablo dağıtma][Distribute]
- [Bir tablo dizin oluşturma][Index]
- [Bir tablo bölümleme][Partition]
- [Tablo istatistikleri koruma][Statistics]
- [Geçici tablolar][Temporary]

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->

<!--Other Web references-->
[create table]: https://msdn.microsoft.com/library/mt203953.aspx
[bigint]: https://msdn.microsoft.com/library/ms187745.aspx
[binary]: https://msdn.microsoft.com/library/ms188362.aspx
[bit]: https://msdn.microsoft.com/library/ms177603.aspx
[char]: https://msdn.microsoft.com/library/ms176089.aspx
[date]: https://msdn.microsoft.com/library/bb630352.aspx
[datetime]: https://msdn.microsoft.com/library/ms187819.aspx
[datetime2]: https://msdn.microsoft.com/library/bb677335.aspx
[datetimeoffset]: https://msdn.microsoft.com/library/bb630289.aspx
[decimal]: https://msdn.microsoft.com/library/ms187746.aspx
[float]: https://msdn.microsoft.com/library/ms173773.aspx
[geometry]: https://msdn.microsoft.com/library/cc280487.aspx
[geography]: https://msdn.microsoft.com/library/cc280766.aspx
[hierarchyid]: https://msdn.microsoft.com/library/bb677290.aspx
[int]: https://msdn.microsoft.com/library/ms187745.aspx
[money]: https://msdn.microsoft.com/library/ms179882.aspx
[nchar]: https://msdn.microsoft.com/library/ms186939.aspx
[nvarchar]: https://msdn.microsoft.com/library/ms186939.aspx
[ntext,text,image]: https://msdn.microsoft.com/library/ms187993.aspx
[real]: https://msdn.microsoft.com/library/ms173773.aspx
[smalldatetime]: https://msdn.microsoft.com/library/ms182418.aspx
[smallint]: https://msdn.microsoft.com/library/ms187745.aspx
[smallmoney]: https://msdn.microsoft.com/library/ms179882.aspx
[sql_variant]: https://msdn.microsoft.com/library/ms173829.aspx
[sysname]: https://msdn.microsoft.com/library/ms186939.aspx
[table]: https://msdn.microsoft.com/library/ms175010.aspx
[time]: https://msdn.microsoft.com/library/bb677243.aspx
[timestamp]: https://msdn.microsoft.com/library/ms182776.aspx
[tinyint]: https://msdn.microsoft.com/library/ms187745.aspx
[uniqueidentifier]: https://msdn.microsoft.com/library/ms187942.aspx
[varbinary]: https://msdn.microsoft.com/library/ms188362.aspx
[varchar]: https://msdn.microsoft.com/library/ms186939.aspx
[xml]: https://msdn.microsoft.com/library/ms187339.aspx
[user defined types]: https://msdn.microsoft.com/library/ms131694.aspx
