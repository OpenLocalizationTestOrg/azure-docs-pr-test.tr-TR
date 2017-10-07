---
title: Azure SQL Data Warehouse'a (PolyBase) SQL Server'a aaaLoad verilerden | Microsoft Docs
description: "SQL Server tooflat dosyaları, AZCopy tooimport veri tooAzure blob depolama ve PolyBase tooingest hello veri BCP tooexport verilerini Azure SQL Data Warehouse'a kullanır."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: barbkess
editor: 
ms.assetid: 4d42786a-fb28-43c9-9c3b-72d19c0ecc11
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 89e2a91bc97642e9fc18545cb802b42d8dc4ad95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-azcopy"></a>SQL Server'dan Azure SQL Data Warehouse'a veri yükleme (AZCopy)
BCP ve AZCopy komut satırı yardımcı programlarını tooload verileri SQL Server tooAzure blob depolama biriminden kullanın. Daha sonra PolyBase veya Azure Data Factory tooload hello verileri Azure SQL Data Warehouse'a kullanın. 

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
