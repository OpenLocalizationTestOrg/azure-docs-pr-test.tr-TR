---
title: "SQL Data Warehouse'da PolyBase kullanarak Kılavuzu | Microsoft Docs"
description: "Kılavuzları ve PolyBase kullanarak SQL Data Warehouse senaryolarda ilgili öneriler."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4757fce1-96b3-48ea-8a51-be1385705f9f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 6/5/2016
ms.custom: loading
ms.author: cakarst;barbkess
ms.openlocfilehash: 6938b92d8e5b46d908dc5b2155bdfdc89bb1dc8c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="guide-for-using-polybase-in-sql-data-warehouse"></a>SQL Data Warehouse'da PolyBase kullanarak Kılavuzu
Bu kılavuz, SQL Data Warehouse'da PolyBase kullanmaya yönelik pratik bilgileri verir.

Başlamak için bkz: [PolyBase ile veri yükleme] [ Load data with PolyBase] Öğreticisi.

## <a name="rotating-storage-keys"></a>Depolama anahtarları döndürme
Zaman zaman güvenlik nedenleriyle blob depolama alanınızın erişim anahtarı değiştirmek isteyeceksiniz.

Bu görevi gerçekleştirmek için en Zarif yolu "anahtarları döndürme" olarak bilinen bir işlem izlemektir. Blob depolama hesabınız için iki depolama anahtarınız olduğunu fark etmiş olabilirsiniz. Böylece geçiş yapabileceğini budur

Azure depolama hesabı anahtarları döndürme basit üç adımı bir işlemdir

1. İkincil depolama erişim anahtarı temel ikinci veritabanı kapsamlı kimlik bilgileri oluşturun
2. Bu yeni bir kimlik bilgisi dayalı ikinci dış veri kaynağı oluşturma
3. Bırakın ve yeni dış veri kaynağına işaret eden dış tabloları oluşturma

Geçirdikten sonra yeni dış veri kaynağına tüm dış tablolar sonra temizleme görevleri gerçekleştirebilirsiniz:

1. Bırakma ilk dış veri kaynağı
2. Birincil depolama erişim anahtarı temel kimlik bilgisi açılan ilk veritabanı kapsamlı
3. Azure'da oturum ve bir sonraki seferde hazır birincil erişim anahtarını yeniden oluşturma

## <a name="query-azure-blob-storage-data"></a>Azure blob depolama veri sorgulama
İlişkisel bir tablo olduğu gibi sorgulamanıza sorguları dış tablolara yönelik yalnızca tablo adı kullanın.

```sql
-- Query Azure storage resident data via external table.
SELECT * FROM [ext].[CarSensor_Data]
;
```

> [!NOTE]
> Bir dış tablo üzerinde bir sorgu hatası ile başarısız olabilir *"Sorgu iptal edildi--bir dış kaynaktan okurken maksimum Reddet Eşiğe ulaşıldığında"*. Bu, dış veri içerip içermediğini gösterir *kirli* kaydeder. Bir veri kaydı gerçek veri türleri/sütun sayısı dış tablosunun sütun tanımları eşleşmiyorsa veya verileri belirtilen dış dosya biçimine uygun değil 'kirli' olarak kabul edilir. Bu sorunu gidermek için dış tablo ve dış dosya biçimini tanımları doğru olduğundan ve bu tanımları, dış veri uyan emin olun. Dış veri kayıtların bir alt kümesini durumunda kirli, sorgularınızı bu kayıtları oluşturma dış tablo DDL Reddet seçeneklerini kullanarak reddetmek seçebilirsiniz.
> 
> 

## <a name="load-data-from-azure-blob-storage"></a>Azure blob depolamadan veri yükleme
Bu örnek verileri Azure blob depolama alanından SQL Data Warehouse veritabanına yükler.

Verileri doğrudan depolama sorguları için veri aktarım süresini kaldırır. Bir columnstore dizini olan verileri depolamak için 10 kat analiz sorgular tarafından sorgu performansı geliştirir.

Bu örnek CREATE TABLE AS SELECT deyimi veri yüklemek için kullanır. Yeni bir tablo sorguda adlandırılan sütunları devralır. Dış tablo tanımı bu sütunların veri türlerini devralır.

CREATE TABLE AS SELECT bir yüksek oranda kullanıcı verileri SQL veri ambarı tüm işlem düğümlerini paralel yükler Transact-SQL deyimini olur.  Analiz platformu sistemi yüksek düzeyde paralel işleme (MPP) altyapısında için geliştirilmiştir ve SQL veri ambarı'nda sunulmuştur.

```sql
-- Load data from Azure blob storage to SQL Data Warehouse

CREATE TABLE [dbo].[Customer_Speed]
WITH
(   
    CLUSTERED COLUMNSTORE INDEX
,    DISTRIBUTION = HASH([CarSensor_Data].[CustomerKey])
)
AS
SELECT *
FROM   [ext].[CarSensor_Data]
;
```

Bkz: [CREATE TABLE AS SELECT (Transact-SQL)][CREATE TABLE AS SELECT (Transact-SQL)].

## <a name="create-statistics-on-newly-loaded-data"></a>Yeni yüklenen verilere ilişkin istatistikler oluşturma
Azure SQL Data Warehouse henüz istatistiklerin otomatik olarak oluşturulup güncelleştirilmesini desteklemiyor.  Sorgularınızdan en iyi performansı elde edebilmeniz için ilk yüklemeden veya verilerdeki önemli değişikliklerden sonra her tablonun her sütununa ilişkin istatistiklerin oluşturulması önemlidir.  İstatistikler hakkında ayrıntılı bir açıklama için Geliştirme ile ilgili konu başlığı grubunda yer alan [İstatistikler][Statistics] bölümüne göz atın.  İstatistik oluşturacağınıza yönelik bu örnekte yüklenen oluşturmak nasıl hızlı bir örneği aşağıdadır.

```sql
create statistics [SensorKey] on [Customer_Speed] ([SensorKey]);
create statistics [CustomerKey] on [Customer_Speed] ([CustomerKey]);
create statistics [GeographyKey] on [Customer_Speed] ([GeographyKey]);
create statistics [Speed] on [Customer_Speed] ([Speed]);
create statistics [YearMeasured] on [Customer_Speed] ([YearMeasured]);
```

## <a name="export-data-to-azure-blob-storage"></a>Azure blob depolama alanına veri dışarı aktarma
Bu bölümde Azure blob depolama alanına SQL veri ambarından verilerin dışarı aktarma gösterir. Bu örnek, dış tablo AS bir yüksek oranda kullanıcı paralel veri tüm işlem düğümlerinden dışarı aktarmak için Transact-SQL deyimini olan Oluştur kullanır.

Aşağıdaki örnek, sütun tanımları ve dbo verileri kullanarak bir dış tablo Weblogs2014 oluşturur. Web günlüklerini tablo. Dış tablo tanımındaki SQL veri ambarı'nda depolanır ve veri kaynağı tarafından belirtilen blob kapsayıcısı altında "/ / log2014/Arşiv" dizinine SELECT deyiminin sonuçlarını dışarı aktarılır. Verileri belirtilen metin dosyası biçiminde dışarı aktarılır.

```sql
CREATE EXTERNAL TABLE Weblogs2014 WITH
(
    LOCATION='/archive/log2014/',
    DATA_SOURCE=azure_storage,
    FILE_FORMAT=text_file_format
)
AS
SELECT
    Uri,
    DateRequested
FROM
    dbo.Weblogs
WHERE
    1=1
    AND DateRequested > '12/31/2013'
    AND DateRequested < '01/01/2015';
```
## <a name="isolate-loading-users"></a>Kullanıcıları yüklenirken yalıtma
Genellikle verileri SQL DW yükleyebilirsiniz birden fazla kullanıcınız gerek yoktur. Çünkü [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] denetim izinleri gerektirir, veritabanını, Denetim erişimi olan birden çok kullanıcıya sahip tüm şemaları son bulur. Bu sınırlamak için REDDETME denetim deyimi kullanabilirsiniz.

Örnek: bir bölüm için veritabanı şemalarını schema_A ve Bölüm B izin veritabanı kullanıcıları user_A schema_B göz önünde bulundurun ve kullanıcılar için Bölüm A ve B, sırasıyla Polybase'in user_B olmalıdır. Her ikisi de denetim veritabanı izinleri verildi.
Şema A ve B şimdi kilidi oluşturucuları REDDETME kullanılarak kendi şemaları aşağı:

```sql
   DENY CONTROL ON SCHEMA :: schema_A TO user_B;
   DENY CONTROL ON SCHEMA :: schema_B TO user_A;
```   
 Bu, user_A ve user_B şimdi diğer bölüm 's şemadan kilitlenmesi.
 


## <a name="next-steps"></a>Sonraki adımlar
SQL Data Warehouse'a veri taşıma hakkında daha fazla bilgi için bkz: [veri geçişine genel bakış][data migration overview].

<!--Image references-->

<!--Article references-->
[Load data with bcp]: ./sql-data-warehouse-load-with-bcp.md
[Load data with PolyBase]: ./sql-data-warehouse-get-started-load-with-polybase.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[data migration overview]: ./sql-data-warehouse-overview-migrate.md

<!--MSDN references-->
[supported source/sink]: https://msdn.microsoft.com/library/dn894007.aspx
[copy activity]: https://msdn.microsoft.com/library/dn835035.aspx
[SQL Server destination adapter]: https://msdn.microsoft.com/library/ms141095.aspx
[SSIS]: https://msdn.microsoft.com/library/ms141026.aspx

[CREATE EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935022.aspx
[CREATE EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/dn935026.aspx
[CREATE EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/dn935021.aspx

[DROP EXTERNAL DATA SOURCE (Transact-SQL)]: https://msdn.microsoft.com/library/mt146367.aspx
[DROP EXTERNAL FILE FORMAT (Transact-SQL)]: https://msdn.microsoft.com/library/mt146379.aspx
[DROP EXTERNAL TABLE (Transact-SQL)]: https://msdn.microsoft.com/library/mt130698.aspx

[CREATE TABLE AS SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/mt204041.aspx
[INSERT...SELECT (Transact-SQL)]: https://msdn.microsoft.com/library/ms174335.aspx
[CREATE MASTER KEY (Transact-SQL)]: https://msdn.microsoft.com/library/ms174382.aspx
[CREATE CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189522.aspx
[CREATE DATABASE SCOPED CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/mt270260.aspx
[DROP CREDENTIAL (Transact-SQL)]: https://msdn.microsoft.com/library/ms189450.aspx

<!-- External Links -->
