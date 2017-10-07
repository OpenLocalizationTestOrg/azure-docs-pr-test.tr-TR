---
title: "KİMLİK kullanarak aaaCreate yedek anahtarları | Microsoft Docs"
description: "Nasıl toouse kimlik toocreate yedek tablolarınızı anahtarları hakkında bilgi edinin."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 06/13/2017
ms.author: jrj;barbkess
ms.openlocfilehash: 502cdd2b510b229b2a19c1f78b11862a7386ae3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-surrogate-keys-by-using-identity"></a>Yedek anahtarları kimliği kullanarak oluşturma
> [!div class="op_single_selector"]
> * [Genel bakış][Overview]
> * [Veri türleri][Data Types]
> * [Dağıt][Distribute]
> * [Dizin][Index]
> * [Bölüm][Partition]
> * [İstatistikleri][Statistics]
> * [Geçici][Temporary]
> * [Kimlik][Identity]
> 
> 

Veri ambarı modelleri tasarlarken birçok veri modelers tablolarıyla toocreate yedek anahtarları ister. Merhaba kimlik özelliği tooachieve sadece ve etkili bir şekilde bu hedef yükü performansınızı etkilemeden kullanabilirsiniz. 

## <a name="get-started-with-identity"></a>KİMLİĞİ ile çalışmaya başlama
Aşağıdaki ifadeyi benzer toohello olan sözdizimini kullanarak ilk hello tablo oluşturduğunuzda hello kimlik özelliğine sahip olarak bir tablo tanımlayabilirsiniz:

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1) NOT NULL
,   C2 INT NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;
```

Daha sonra `INSERT..SELECT` toopopulate hello tablo.

## <a name="behavior"></a>Davranışı
Merhaba kimlik özelliği çıkışı tasarlanmış tooscale yük performanslarını etkilemeden hello veri ambarındaki tüm hello dağıtımlar arasında değil. Bu nedenle, hello kimlik bu hedeflere ulaşmak doğru yönlendirilmiş uygulamasıdır. Bu bölüm hello nüanslarını vurgular hello uygulama toohelp siz bunları daha tam olarak anlamak.  

### <a name="allocation-of-values"></a>Değerlerin ayırma
Merhaba kimlik özelliği hangi hello ayrılan yedek değerleri, SQL Server ve Azure SQL veritabanı hello davranışını yansıtan hello sipariş garanti etmez. Ancak, Azure SQL veri ambarı'nda bir garanti hello yokluğu daha belirgin olur. 

Aşağıdaki örnek hello çizim şöyledir:

```sql
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)    NOT NULL
,   C2 VARCHAR(30)              NULL
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

INSERT INTO dbo.T1
VALUES (NULL);

INSERT INTO dbo.T1
VALUES (NULL);

SELECT *
FROM dbo.T1;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

Örnek önceki hello iki satır dağıtım 1 landed. Hello ilk satır sütununda hello yedek değeri 1 olan `C1`, ve hello ikinci satırında 61 hello yedek değeri. Bu değerlerin her ikisi de hello kimlik özelliği tarafından üretildi. Ancak, hello ayırma hello değerlerin bitişik değil. Bu davranış tasarım gereğidir.

### <a name="skewed-data"></a>Çarpık veri 
Merhaba hello veri türünün değer aralığını hello dağıtımlar arasında eşit olarak yayılır. Dağıtılmış bir tablo çarpık verileri varsa, kullanılabilir toohello datatype erken tükenmiş olabilir değerlerin hello. Tüm hello verileri sona eriyor, tek bir dağıtım, örneğin, etkili bir şekilde hello tablo hello veri türünün hello değerlerin erişim tooonly bir sixtieth yoktur. Bu nedenle, hello kimlik özelliği çok sınırlı`INT` ve `BIGINT` veri türleri yalnızca.

### <a name="selectinto"></a>SEÇİN... İÇİNE
Varolan bir kimlik sütunu yeni bir tabloya seçildiğinde, hello koşullar aşağıdaki koşullardan biri sürece hello yeni bir sütun hello kimlik özelliği alır:
- Merhaba SELECT deyimi bir birleştirme içerir.
- Birden çok SELECT deyimine birleşim kullanılarak birleştirilmiştir.
- Merhaba kimlik sütunu hello SELECT listesinde birden fazla kez listelenir.
- Merhaba kimlik sütunu bir ifadenin bir parçasıdır.
    
Bu koşulların herhangi biri doğruysa hello sütun hello kimlik özelliğini devralan yerine NOT NULL oluşturulur.

### <a name="create-table-as-select"></a>TABLE AS SELECT OLUŞTURMA
OLUŞTURMA tablo AS seçin (CTAS) aşağıdaki seçim belgelenen aynı SQL Server davranışı hello... . Ancak, bir kimlik özelliği hello sütun tanımında hello belirtemezsiniz `CREATE TABLE` hello deyimi parçası. Merhaba kimlik işlevi hello kullanamazsınız `SELECT` hello CTAS bir parçası. toopopulate bir tablo, gereksinim duyduğunuz toouse `CREATE TABLE` toodefine hello tablo arkasından `INSERT..SELECT` toopopulate onu.

## <a name="explicitly-insert-values-into-an-identity-column"></a>Açıkça değerleri bir kimlik sütununa ekleme 
SQL veri ambarı destekleyen `SET IDENTITY_INSERT <your table> ON|OFF` sözdizimi. Merhaba kimlik sütununa Bu sözdizimi tooexplicitly Ekle değerlerini kullanabilirsiniz.

Toouse önceden tanımlanmış negatif belirli kendi boyutlarını satır değerleri gibi çok sayıda veri modelers. Merhaba -1 veya "Bilinmeyen bir üyeye" satır örneğidir. 

Merhaba sonraki komut dosyası nasıl tooexplicitly eklemek bu satır KÜMESİ IDENTITY_INSERT kullanarak gösterir:

```sql
SET IDENTITY_INSERT dbo.T1 ON;

INSERT INTO dbo.T1
(   C1
,   C2
)
VALUES (-1,'UNKNOWN')
;

SET IDENTITY_INSERT dbo.T1 OFF;

SELECT  *
FROM    dbo.T1
;
```    

## <a name="load-data-into-a-table-with-identity"></a>KİMLİĞİNE sahip bir tabloya veri yükleme

Merhaba kimlik özelliği Hello varlığını bazı etkileri tooyour veri yükleme koduna sahip. Bu bölüm kimliği kullanarak verileri tablolara yüklemek için bazı temel düzenlerden vurgular. 

### <a name="load-data-with-polybase"></a>PolyBase ile veri yükleyin
bir tabloya tooload veri ve kimliği kullanarak bir yedek anahtar oluşturmak, hello tablo oluşturmayı ve ardından Ekle... Seç veya Ekle... DEĞERLERİ tooperform hello yük.

Merhaba aşağıdaki örnek hello temel düzeni vurgular:
 
```sql
--CREATE TABLE with IDENTITY
CREATE TABLE dbo.T1
(   C1 INT IDENTITY(1,1)
,   C2 VARCHAR(30)
)
WITH
(   DISTRIBUTION = HASH(C2)
,   CLUSTERED COLUMNSTORE INDEX
)
;

--Use INSERT..SELECT toopopulate hello table from an external table
INSERT INTO dbo.T1
(C2)
SELECT  C2
FROM    ext.T1
;

SELECT  *
FROM    dbo.T1
;

DBCC PDW_SHOWSPACEUSED('dbo.T1');
```

> [!NOTE] 
> Olası toouse değil `CREATE TABLE AS SELECT` şu anda verileri bir kimlik sütunu olan bir tabloya yüklenirken.
> 

Merhaba toplu kopyalama programı (BCP) aracını kullanarak veri yükleme ile ilgili daha fazla bilgi için aşağıdaki makaleler hello bakın:

- [PolyBase ile yükleme][]
- [PolyBase en iyi uygulamalar][]

### <a name="load-data-with-bcp"></a>BCP ile veri yükleme
BCP, SQL Data Warehouse'a tooload veri kullanabileceğiniz bir komut satırı aracıdır. Parametrelerinden biri (-E) denetimleri hello BCP davranışını verileri bir kimlik sütunu olan bir tabloya yüklenirken. 

-E belirtildiğinde, hello sütun için hello giriş dosyasındaki KİMLİKLE tutulan hello değerleri korunur. -E ise *değil* hello bu sütundaki değerleri yoksayılır belirtilen. Merhaba kimlik sütunu dahil edilmezse, hello veriler normal olarak yüklenir. Merhaba değerleri toohello artırma ve çekirdek İlkesi hello özelliğinin göre oluşturulur.

BCP kullanarak veri yükleme ile ilgili daha fazla bilgi için aşağıdaki makaleler hello bakın:

- [BCP ile yükleme][]
- [BCP MSDN'de][]

## <a name="catalog-views"></a>Katalog görünümleri
SQL veri ambarı destekleyen hello `sys.identity_columns` Katalog görünümü. Bu görünüm, kullanılan tooidentify hello kimlik özelliğine sahip bir sütun olabilir.

Bu örnek hello veritabanı şeması daha iyi anlamak toohelp gösterir nasıl toointegrate `sys.identity_columns` diğer sistem Katalog görünümleri ile:

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       CASE WHEN ic.column_id IS NOT NULL
             THEN 1
        ELSE 0
        END AS is_identity 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
LEFT JOIN   sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="limitations"></a>Sınırlamalar
Merhaba kimlik özelliği senaryoları aşağıdaki hello kullanılamaz:
- Burada hello sütun veri türü tamsayı veya büyük tamsayı değil
- Merhaba sütun hello dağıtım anahtarı da olduğu
- Merhaba tablosu bir dış tablo olduğu 

ilgili işlevleri aşağıdaki hello SQL veri ambarı'nda desteklenmez:

- [IDENTITY()][]
- [@@IDENTITY][]
- [SCOPE_IDENTITY][]
- [IDENT_CURRENT][]
- [IDENT_INCR][]
- [IDENT_SEED][]
- [DBCC CHECK_IDENT()][]

## <a name="tasks"></a>Görevler

Bu bölümde bazı örnek kod, kimlik sütunu ile çalışırken tooperform ortak görevleri kullanabilirsiniz.

> [!NOTE] 
> Sütun C1 hello kimlik görevleri aşağıdaki tüm hello ' dir.
> 
 
### <a name="find-hello-highest-allocated-value-for-a-table"></a>Bir tablo için ayrılan hello en yüksek değeri Bul
Kullanım hello `MAX()` işlev dağıtılmış bir tablo için ayrılan toodetermine hello en yüksek değer:

```sql
SELECT  MAX(C1)
FROM    dbo.T1
``` 

### <a name="find-hello-seed-and-increment-for-hello-identity-property"></a>Merhaba çekirdek ve Artım Merhaba kimlik özelliği Bul
Sorgu aşağıdaki hello kullanarak bir tablo için hello Katalog görünümleri toodiscover hello kimlik artırma ve çekirdek yapılandırma değerlerini kullanabilirsiniz: 

```sql
SELECT  sm.name
,       tb.name
,       co.name
,       ic.seed_value
,       ic.increment_value 
FROM        sys.schemas AS sm
JOIN        sys.tables  AS tb           ON  sm.schema_id = tb.schema_id
JOIN        sys.columns AS co           ON  tb.object_id = co.object_id
JOIN        sys.identity_columns AS ic  ON  co.object_id = ic.object_id
                                        AND co.column_id = ic.column_id
WHERE   sm.name = 'dbo'
AND     tb.name = 'T1'
;
```

## <a name="next-steps"></a>Sonraki adımlar

* tablolar, geliştirme hakkında daha fazla toolearn bkz [tablo genel bakışı][Overview], [tablo veri türleri][Data Types], [bir tabloDağıt] [ Distribute], [Tablo dizin][Index], [tablo bölüm][Partition], ve [ Geçici tablolara][Temporary]. 
* En iyi uygulamalar hakkında daha fazla bilgi için bkz: [SQL veri ambarı en iyi yöntemler][SQL Data Warehouse Best Practices].  

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[Identity]: ./sql-data-warehouse-tables-identity.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

[BCP ile yükleme]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-with-bcp/
[PolyBase ile yükleme]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-from-azure-blob-storage-with-polybase/
[PolyBase en iyi uygulamalar]: https://docs.microsoft.com/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide/


<!--MSDN references-->
[Identity property]: https://msdn.microsoft.com/library/ms186775.aspx
[sys.identity_columns]: https://msdn.microsoft.com/library/ms187334.aspx
[IDENTITY()]: https://msdn.microsoft.com/library/ms189838.aspx
[@@IDENTITY]: https://msdn.microsoft.com/library/ms187342.aspx
[SCOPE_IDENTITY]: https://msdn.microsoft.com/library/ms190315.aspx
[IDENT_CURRENT]: https://msdn.microsoft.com/library/ms175098.aspx
[IDENT_INCR]: https://msdn.microsoft.com/library/ms189795.aspx
[IDENT_SEED]: https://msdn.microsoft.com/library/ms189834.aspx
[DBCC CHECK_IDENT()]: https://msdn.microsoft.com/library/ms176057.aspx

[BCP MSDN'de]: https://msdn.microsoft.com/library/ms162802.aspx
  

<!--Other Web references-->  
