---
title: aaaUse bcp tooload verileri SQL Data Warehouse | Microsoft Docs
description: "BCP'nin ne olduğunu öğrenin ve nasıl toouse veri depolama senaryolarında için."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: f9467d11-fcd6-4131-a65a-2022d2c32d24
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 09a2980585097644924c71899f9e74fb32fbc26d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-with-bcp"></a>BCP ile veri yükleme
> [!div class="op_single_selector"]
> * [Redgate](sql-data-warehouse-load-with-redgate.md)  
> * [Data Factory](sql-data-warehouse-get-started-load-with-azure-data-factory.md)  
> * [PolyBase](sql-data-warehouse-get-started-load-with-polybase.md)  
> * [BCP](sql-data-warehouse-load-with-bcp.md)
> 
> 

**[BCP] [ bcp]**  SQL Server, veri dosyaları ve SQL Data Warehouse arasında toocopy veri sağlayan bir komut satırı toplu yükleme yardımcı programıdır. BCP tooimport çok sayıda satırı SQL Data Warehouse tablolar veya veri dosyaları SQL Server tablolarına tooexport verileri kullanın. Merhaba queryout seçeneğiyle kullanılmadığı sürece dışında Transact-SQL olanağıyla bcp gerektirir.

BCP bir hızlı ve kolay bir yol toomove daha küçük veri kümeleri içine ve dışına SQL veri ambarı veritabanı var. Hello tam tooload/extract bcp aracılığıyla önerilen veri miktarına bağlıdır bağlantı toohello Azure veri merkezi ağ üzerinde.  Genel olarak, boyut tabloları bcp aracılığıyla kolayca yüklenip ayıklanabilir ancak büyük miktarda veriyi yüklemek veya ayıklamak için bcp'nin kullanılması önerilmez.  Polybase aracı yükleme ve SQL Data Warehouse hello yüksek düzeyde paralel işleme mimarisi yararlanarak daha iyi iş yaptığı gibi büyük miktarda veriyi ayıklanması için önerilen hello eder.

bcp ile yapabilecekleriniz:

* Basit komut satırı yardımcı programını tooload verileri SQL Data Warehouse'a kullanın.
* Basit komut satırı yardımcı programını tooextract verileri SQL veri ambarından kullanın.

Bu öğreticide şunları nasıl yapacağınızı gösterilecek:

* Merhaba bcp in komutunu kullanarak bir tabloya veri al
* Veri tablosu sıcaklıklarını hello bcp out komutunu dışarı aktarın

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="prerequisites"></a>Ön koşullar
toostep Bu öğreticide, aşağıdakiler gerekir:

* SQL Data Warehouse veritabanı
* Merhaba bcp komut satırı yardımcı programının yüklü olması
* Merhaba SQLCMD komut satırı yardımcı programının yüklü olması

> [!NOTE]
> Hello hello bcp ve sqlcmd yardımcı programlarını indirebilirsiniz [Microsoft Download Center][Microsoft Download Center].
> 
> 

## <a name="import-data-into-sql-data-warehouse"></a>SQL Data Warehouse'a veri aktarma
Bu öğreticide, Azure SQL Data Warehouse'da bir tablo oluşturup hello tabloya veri alma.

### <a name="step-1-create-a-table-in-azure-sql-data-warehouse"></a>1. Adım: Azure SQL Data Warehouse'da tablo oluşturma
Bir komut isteminden sqlcmd toorun hello sorgu toocreate tablo aşağıdaki Örneğinizde kullanın:

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    WITH
    (
        CLUSTERED COLUMNSTORE INDEX,
        DISTRIBUTION = ROUND_ROBIN
    );
"
```

> [!NOTE]
> Bkz: [tablo genel bakışı] [ Table Overview] veya [CREATE TABLE söz dizimi] [ CREATE TABLE syntax] SQL veri ambarı ve hello tablo oluşturma hakkında daha fazla bilgi  Merhaba WITH yan tümcesinde bulunan seçenekler.
> 
> 

### <a name="step-2-create-a-source-data-file"></a>2. Adım: Kaynak veri dosyası oluşturma
Veri satırlarını yeni bir metin dosyasına aşağıdaki not defteri ve kopyalama hello açın ve ardından bu dosya tooyour yerel geçici dizin, C:\Temp\DimDate2.txt kaydedin.

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

> [!NOTE]
> Önemli tooremember olan bcp.exe hello UTF-8 dosya kodlamasını desteklemiyor. bcp.exe dosyasını kullanırken lütfen ASCII dosyalarını veya UTF-16 kodlu dosyaları kullanın.
> 
> 

### <a name="step-3-connect-and-import-hello-data"></a>3. adım: Bağlanma ve hello veri alma
BCP kullanarak bağlanın ve komutu değiştirerek hello değerleri uygun şekilde aşağıdaki hello kullanarak hello veri içeri aktarın:

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t  ','
```

Merhaba sqlcmd kullanarak sorgu aşağıdaki hello çalıştırarak verilerin yüklendiğini doğrulayabilirsiniz:

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

Bu, sonuçları aşağıdaki hello döndürmesi gerekir:

| DateId | CalendarQuarter | FiscalQuarter |
| --- | --- | --- |
| 20150101 |1 |3 |
| 20150201 |1 |3 |
| 20150301 |1 |3 |
| 20150401 |2 |4 |
| 20150501 |2 |4 |
| 20150601 |2 |4 |
| 20150701 |3 |1 |
| 20150801 |3 |1 |
| 20150801 |3 |1 |
| 20151001 |4 |2 |
| 20151101 |4 |2 |
| 20151201 |4 |2 |

### <a name="step-4-create-statistics-on-your-newly-loaded-data"></a>4. Adım: Yeni yüklenmiş verilerinize ilişkin İstatistikler oluşturma
Azure SQL Data Warehouse henüz istatistiklerin otomatik olarak oluşturulup güncelleştirilmesini desteklemiyor. Sipariş tooget hello en iyi performansı sorgularınızı, istatistikleri hello ilk yükleme işleminden sonra tüm tabloların tüm sütunlarda oluşturulması önemlidir veya hello verilerde önemli değişikliklerden. Merhaba istatistikleri ayrıntılı bir açıklaması için bkz [istatistikleri] [ Statistics] konu hello geliştirme grubunu konuda. Nasıl toocreate istatistik oluşturacağınıza yönelik hello Bu örnekte yüklenen, hızlı bir örnek aşağıda verilmiştir

Bir sqlcmd isteminden CREATE STATISTICS deyimlerini aşağıdaki hello yürütün:

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="export-data-from-sql-data-warehouse"></a>SQL Data Warehouse'dan veri aktarma
Bu öğreticide SQL Data Warehouse'da bulunan bir tablodan veri dosyası oluşturacaksınız. Biz hello verileri DimDate2_export.txt adlı tooa yeni bir veri dosyası oluşturduğumuz verecektir.

### <a name="step-1-export-hello-data"></a>1. adım: hello verileri dışarı aktarma
Hello bcp yardımcı programını kullanarak, bağlanın ve komutu değiştirerek hello değerleri uygun şekilde aşağıdaki hello kullanarak verileri dışarı aktarma:

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
Merhaba yeni dosyayı açarak verilerin doğru verildiğinden hello doğrulayabilirsiniz. Merhaba dosyasındaki Hello verileri hello metinle eşleşmesi gerekir:

```
20150301,1,3
20150501,2,4
20151001,4,2
20150201,1,3
20151201,4,2
20150801,3,1
20150601,2,4
20151101,4,2
20150401,2,4
20150701,3,1
20150901,3,1
20150101,1,3
```

> [!NOTE]
> Toohello yapısı dağıtılmış sistemlerin hello veri sırası SQL Data Warehouse veritabanlarında aynı hello olmayabilir. Başka bir seçenektir toouse hello **queryout** bcp toowrite bir sorgu işlevinin ayıklamak yerine hello tüm tabloyu dışarı aktarma.
> 
> 

## <a name="next-steps"></a>Sonraki adımlar
Yüklemeye genel bakış için bkz. [SQL Veri Ambarı'na veri yükleme][Load data into SQL Data Warehouse].
Geliştirme ile ilgili daha fazla ipucu için bkz. [SQL Veri Ambarı’nda geliştirmeye genel bakış][SQL Data Warehouse development overview].

<!--Image references-->

<!--Article references-->

[Load data into SQL Data Warehouse]: ./sql-data-warehouse-overview-load.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[Table Overview]: ./sql-data-warehouse-tables-overview.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
