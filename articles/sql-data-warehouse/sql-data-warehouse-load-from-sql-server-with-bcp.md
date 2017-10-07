---
title: "aaaLoad verileri SQL Server'dan Azure SQL veri ambarında (bcp) | Microsoft Docs"
description: "Küçük boyutlu veriler için SQL Server tooflat dosyalarından bcp tooexport verileri ve hello veri içeri aktarma doğrudan Azure SQL Data Warehouse'a kullanır."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: f87d8d7c-8276-43c5-90e7-d4ccc0e3a224
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: a03b5403d123e8814ae73a7cce8e6851c8b264a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-sql-server-into-azure-sql-data-warehouse-flat-files"></a>SQL Server'dan Azure SQL Data Warehouse'a veri yükleme (düz dosyalar)
> [!div class="op_single_selector"]
> * [SSIS](sql-data-warehouse-load-from-sql-server-with-integration-services.md)
> * [PolyBase](sql-data-warehouse-load-from-sql-server-with-polybase.md)
> * [bcp](sql-data-warehouse-load-from-sql-server-with-bcp.md)
> 
> 

Küçük veri kümeleri için hello bcp komut satırı yardımcı programını tooexport verileri SQL Server'dan kullanın ve tooAzure SQL veri ambarı doğrudan yükleyin.

Bu öğreticide bcp'yi kullanarak şunları yapacaksınız:

* Bir tablodan hello bcp out komutunu kullanarak SQL Server'dan dışarı aktar (veya basit bir örnek dosyası oluşturma)
* Düz dosya tooSQL veri ambarı hello tablosundan alma.
* İstatistikleri hello yüklenen veriler üzerinde oluşturun.

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Loading-data-into-Azure-SQL-Data-Warehouse-with-BCP/player]
> 
> 

## <a name="before-you-begin"></a>Başlamadan önce
### <a name="prerequisites"></a>Ön koşullar
toostep Bu öğreticide, aşağıdakiler gerekir:

* SQL Data Warehouse veritabanı
* Merhaba bcp komut satırı yardımcı programının yüklü olması
* Merhaba sqlcmd komut satırı yardımcı programının yüklü olması

Hello hello bcp ve sqlcmd yardımcı programlarını indirebilirsiniz [Microsoft Download Center][Microsoft Download Center].

### <a name="data-in-ascii-or-utf-16-format"></a>ASCII veya UTF-16 biçimindeki veriler
Bu öğreticiyi kendi verilerinizle deniyorsanız verilerinizin toouse hello ASCII veya UTF-8 bcp desteklemediğinden UTF-16 kodlamasını gerekir. 

PolyBase UTF-8'i destekler ancak henüz UTF-16'yi desteklemiyor. PolyBase ile toocombine bcp istiyorsanız SQL Server'dan dışarı aktardıktan sonra tootransform hello veri tooUTF-8 gerektiğine dikkat edin. 

## <a name="1-create-a-destination-table"></a>1. Hedef tablo oluşturma
SQL veri ambarındaki hello yük hello hedef tablo olacak bir tablo tanımlayın. Merhaba tablodaki Hello sütun toohello veriler, her satır, veri dosyanızın karşılık gelmelidir.

toocreate tablo, bir komut istemi açın ve sqlcmd.exe toorun hello aşağıdaki komutu kullanın:

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


## <a name="2-create-a-source-data-file"></a>2. Kaynak veri dosyası oluşturma
Veri satırlarını yeni bir metin dosyasına aşağıdaki not defteri ve kopyalama hello açın ve ardından bu dosya tooyour yerel geçici dizin, C:\Temp\DimDate2.txt kaydedin. Bu veri ASCII biçimindedir.

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

(İsteğe bağlı) tooexport bir SQL Server veritabanından kendi verilerinizi bir komut istemi açın ve hello aşağıdaki komutu çalıştırın. TableName (Tablo Adı), ServerName (Sunucu Adı), DatabaseName (Veritabanı Adı), Username (Kullanıcı Adı) ve Password (Parola) alanlarına kendi bilgilerinizi yazın.

```sql
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t ','
```



## <a name="3-load-hello-data"></a>3. Merhaba veri yükleme
tooload hello verileri, bir komut istemi açın ve aşağıdaki komut, sunucu adı, veritabanı adı, kullanıcı adı ve parola alanlarına kendi bilgilerinizi hello değerleri değiştirerek hello çalıştırın.

```sql
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ','
```

Bu komut tooverify hello verilerin düzgün şekilde yüklendiğini kullanın

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "SELECT * FROM DimDate2 ORDER BY 1;"
```

Merhaba sonuçları aşağıdaki gibi görünmelidir:

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

## <a name="4-create-statistics"></a>4. İstatistik oluşturma
SQL Data Warehouse henüz istatistiklerin otomatik olarak oluşturulup güncelleştirilmesini desteklemiyor. tooget hello en iyi sorgu performansını, hello ilk yükleme sonrasında veya hello verilerde önemli değişikliklerden sonra tüm tabloların tüm sütunlar üzerinde önemli toocreate istatistikleri değil. İstatistiklerin ayrıntılı bir açıklaması için bkz [istatistikleri][Statistics]. 

Çalışma hello aşağıdaki yeni yüklenen tablonuzda istatistik toocreate komutu.

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    create statistics [DateId] on [DimDate2] ([DateId]);
    create statistics [CalendarQuarter] on [DimDate2] ([CalendarQuarter]);
    create statistics [FiscalQuarter] on [DimDate2] ([FiscalQuarter]);
"
```

## <a name="5-export-data-from-sql-data-warehouse"></a>5. SQL Data Warehouse'dan veri aktarma
Fun için yalnızca geri SQL Data warehouse'dan hello verileri dışarı aktarabilirsiniz.  Merhaba komutu tooexport olan tam olarak hello SQL Server'dan veri aktarma aynıdır.

Ancak, hello sonuçlarda bir fark yoktur. Veri verdiğinizde hello verileri SQL Data warehouse'da dağıtılmış konumlarda depolandığı her işlem düğümü veri toohello çıkış dosyasına yazar. Merhaba hello veri hello çıktı dosyasına büyük olasılıkla toobe hello giriş dosyasındaki hello verileri hello sırasını farklı sırasıdır.

### <a name="export-a-table-and-compare-exported-results"></a>Bir tabloyu dışarı aktarma ve dışarı aktarılan sonuçları karşılaştırma
toosee dışarı aktarılan verileri Merhaba, bir komut istemi açın ve kendi parametrelerinizi kullanarak bu komutu çalıştırın. ServerName hello Azure mantıksal SQL Sunucunuz adıdır.

```sql
bcp DimDate2 out C:\Temp\DimDate2_export.txt -S <Server Name> -d <Database Name> -U <Username> -P <password> -q -c -t ','
```
Merhaba yeni dosyayı açarak verilerin doğru verildiğinden hello doğrulayabilirsiniz. Merhaba dosyasındaki Hello verileri hello metinle eşleşmelidir ancak büyük olasılıkla farklı bir sırada sıralanır:

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

### <a name="export-hello-results-of-a-query"></a>Merhaba bir sorgunun sonuçlarını dışarı aktarma
Merhaba kullanabilirsiniz **queryout** bcp tooexport hello hello tüm tabloyu dışarı yerine bir sorgunun sonuçlarını işlevi. 

## <a name="next-steps"></a>Sonraki adımlar
Yüklemeye genel bakış için bkz. [SQL Veri Ambarı'na veri yükleme][Load data into SQL Data Warehouse].
Geliştirme ile ilgili daha fazla ipucu için bkz. [SQL Veri Ambarı’nda geliştirmeye genel bakış][SQL Data Warehouse development overview].
Bkz: [tablo genel bakışı] [ Table Overview] veya [CREATE TABLE söz dizimi] [ CREATE TABLE syntax] SQL Data Warehouse'da tablo oluşturma hakkında daha fazla bilgi.

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
