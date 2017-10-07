---
title: SQL Data Warehouse'da PolyBase kullanarak aaaGuide | Microsoft Docs
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
ms.openlocfilehash: b05e4c5d528f2fe1c60d6855b5333065f0c908ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="guide-for-using-polybase-in-sql-data-warehouse"></a>SQL Data Warehouse'da PolyBase kullanarak Kılavuzu
Bu kılavuz, SQL Data Warehouse'da PolyBase kullanmaya yönelik pratik bilgileri verir.

başlatıldı, tooget bkz hello [PolyBase ile veri yükleme] [ Load data with PolyBase] Öğreticisi.

## <a name="rotating-storage-keys"></a>Depolama anahtarları döndürme
Saat tootime güvenlik nedenleriyle toochange hello erişim anahtar tooyour blob depolama isteyeceksiniz.

Bu görev toofollow "Merhaba anahtarları döndürme" olarak bilinen bir işlem olduğundan en Zarif yolu tooperform hello. Blob depolama hesabınız için iki depolama anahtarınız olduğunu fark etmiş olabilirsiniz. Böylece geçiş yapabileceğini budur

Azure depolama hesabı anahtarları döndürme basit üç adımı bir işlemdir

1. Merhaba ikincil depolama erişim anahtarı temel ikinci veritabanı kapsamlı kimlik bilgileri oluşturun
2. Bu yeni bir kimlik bilgisi dayalı ikinci dış veri kaynağı oluşturma
3. Bırakma ve toohello yeni dış veri kaynağına işaret eden hello dış tabloları oluşturma

Gerçekleştirebileceğiniz sonra tüm dış tablolara toohello yeni dış veri kaynağınızda geçirdikten sonra hello görevleri temizleyin:

1. Bırakma ilk dış veri kaynağı
2. Kimlik bilgisi hello birincil depolama erişim anahtarı temel açılan ilk veritabanı kapsamlı
3. Azure'da oturum açın ve hello birincil erişim anahtarı Merhaba hazır sonraki sefer yeniden

## <a name="query-azure-blob-storage-data"></a>Azure blob depolama veri sorgulama
İlişkisel bir tablo olduğu gibi sorgulamanıza sorguları dış tablolara yönelik yalnızca hello tablo adı kullanın.

```sql
-- Query Azure storage resident data via external table.
SELECT * FROM [ext].[CarSensor_Data]
;
```

> [!NOTE]
> Bir dış tablo sorgu hello hata ile başarısız olabilir *"Sorgu iptal edildi--hello maksimum Reddet eşik bir dış kaynaktan okurken ulaşıldı"*. Bu, dış veri içerip içermediğini gösterir *kirli* kaydeder. Bir veri kaydı hello gerçek veri türleri/sütun sayısı hello hello dış tablosunun sütun tanımları eşleşmiyorsa veya hello verileri toohello belirtilen dış dosya biçimi uygun değil 'kirli' olarak kabul edilir. toofix Bu, dış tablo ve dış dosya biçimini tanımları doğru ve dış verilerinizi toothese tanımları uyumlu olduğundan emin olun. Dış veri kayıtların bir alt kümesini durumunda kirli, tooreject bu kayıtları sorgularınızı oluşturmak dış tablo DDL hello reddetme seçenekleri kullanılarak seçebilirsiniz.
> 
> 

## <a name="load-data-from-azure-blob-storage"></a>Azure blob depolamadan veri yükleme
Bu örnek verileri Azure blob depolama tooSQL veri ambarı veritabanından yükler.

Verileri doğrudan depolamak hello veri aktarım süresini sorgular için kaldırır. Bir columnstore dizini olan veri depolama too10x tarafından analiz sorguları için sorgu performansı geliştirir.

Bu örnek hello CREATE TABLE AS SELECT deyimi tooload verileri kullanır. Merhaba yeni tablo hello sorguda adlandırılan hello sütunları devralır. Bu sütunların veri türlerini hello hello dış tablo tanımından devralır.

CREATE TABLE AS SELECT bir yüksek oranda kullanıcı paralel tooall hello hello verileri yükler Transact-SQL deyimini işlem düğümleri, SQL Data warehouse'un olur.  Analiz platformu sistemi hello yüksek düzeyde paralel işleme (MPP) altyapısı için geliştirilmiştir ve SQL veri ambarı'nda sunulmuştur.

```sql
-- Load data from Azure blob storage tooSQL Data Warehouse

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
Azure SQL Data Warehouse henüz istatistiklerin otomatik olarak oluşturulup güncelleştirilmesini desteklemiyor.  Sipariş tooget hello en iyi performansı sorgularınızı, istatistikleri hello ilk yükleme işleminden sonra tüm tabloların tüm sütunlarda oluşturulması önemlidir veya hello verilerde önemli değişikliklerden.  Merhaba istatistikleri ayrıntılı bir açıklaması için bkz [istatistikleri] [ Statistics] konu hello geliştirme grubunu konuda.  Aşağıda bu örnekte toocreate istatistik oluşturacağınıza yönelik hello nasıl yüklenir, hızlı bir örnek verilmiştir.

```sql
create statistics [SensorKey] on [Customer_Speed] ([SensorKey]);
create statistics [CustomerKey] on [Customer_Speed] ([CustomerKey]);
create statistics [GeographyKey] on [Customer_Speed] ([GeographyKey]);
create statistics [Speed] on [Customer_Speed] ([Speed]);
create statistics [YearMeasured] on [Customer_Speed] ([YearMeasured]);
```

## <a name="export-data-tooazure-blob-storage"></a>Veri tooAzure blob depolama dışarı aktarma
Bu bölümde, nasıl SQL Data Warehouse tooAzure tooexport verileri blob depolama gösterir. Bu örnek, dış tablo AS yüksek oranda kullanıcı Transact-SQL deyimi tooexport hello veri paralel tüm hello işlem düğümlerinden olan Oluştur kullanır.

Merhaba aşağıdaki örnek sütun tanımları ve dbo verileri kullanarak bir dış tablo Weblogs2014 oluşturur. Web günlüklerini tablo. Merhaba dış tablo tanımındaki SQL veri ambarında depolanır ve hello SELECT deyimi hello sonuçlarını dışarı aktarılan toohello olan "/ / log2014/Arşiv" dizini hello veri kaynağı tarafından belirtilen hello blob kapsayıcısı altında. Merhaba veri hello belirtilen metin dosyası biçiminde dışarı aktarılır.

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
Verileri bir SQL DW yükleyebilirsiniz birden çok kullanıcı genellikle gerek toohave var. Çünkü hello [CREATE TABLE AS SELECT (Transact-SQL)] [ CREATE TABLE AS SELECT (Transact-SQL)] denetim izinleri gerektirir hello veritabanının, Denetim erişimi olan birden çok kullanıcıya sahip tüm şemaları son bulur. toolimit bunu hello REDDET denetim deyimi kullanabilirsiniz.

Örnek: bir bölüm için veritabanı şemalarını schema_A ve Bölüm B izin veritabanı kullanıcıları user_A schema_B göz önünde bulundurun ve kullanıcılar için Bölüm A ve B, sırasıyla Polybase'in user_B olmalıdır. Her ikisi de denetim veritabanı izinleri verildi.
Merhaba oluşturucuları şemasının A ve B şimdi REDDETME kullanılarak kendi şemaları kilitle:

```sql
   DENY CONTROL ON SCHEMA :: schema_A toouser_B;
   DENY CONTROL ON SCHEMA :: schema_B toouser_A;
```   
 Bu, user_A ve user_B şimdi hello kilitlenmesi diğer bölüm 's şema.
 


## <a name="next-steps"></a>Sonraki adımlar
toolearn taşıma veri tooSQL veri ambarı hakkında daha fazla bilgi görmek hello [veri geçişine genel bakış][data migration overview].

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
