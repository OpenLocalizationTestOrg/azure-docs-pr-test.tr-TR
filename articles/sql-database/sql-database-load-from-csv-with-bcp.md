---
title: "CSV aaaLoad verilerden dosya Azure SQL veritabanına (bcp) | Microsoft Docs"
description: "Küçük boyutlu veriler için Azure SQL veritabanına bcp tooimport verileri kullanır."
services: sql-database
documentationcenter: NA
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 875f9b8d-f1a1-4895-b717-f45570fb7f80
ms.service: sql-database
ms.custom: load & move data
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 01/10/2017
ms.author: carlrab
ms.openlocfilehash: 9350e459aa844223820fbbd849a830cf0354d4e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-from-csv-into-azure-sql-database-flat-files"></a>CSV dosyasından Azure SQL Veritabanı'na veri yükleme (düz dosyalar)
Azure SQL veritabanına bir CSV dosyasından hello bcp komut satırı yardımcı programını tooimport veri kullanabilirsiniz.

## <a name="before-you-begin"></a>Başlamadan önce
### <a name="prerequisites"></a>Ön koşullar
Bu makalede toocomplete hello adımlar, gerekir:

* Azure SQL Database mantıksal sunucusu ve veritabanı
* Merhaba bcp komut satırı yardımcı programının yüklü olması
* Merhaba sqlcmd komut satırı yardımcı programının yüklü olması

Hello hello bcp ve sqlcmd yardımcı programlarını indirebilirsiniz [Microsoft Download Center][Microsoft Download Center].

### <a name="data-in-ascii-or-utf-16-format"></a>ASCII veya UTF-16 biçimindeki veriler
Bu öğreticiyi kendi verilerinizle deniyorsanız verilerinizin toouse hello ASCII veya UTF-8 bcp desteklemediğinden UTF-16 kodlamasını gerekir. 

## <a name="1-create-a-destination-table"></a>1. Hedef tablo oluşturma
Bir tablo, SQL veritabanında hello hedef tablo olarak tanımlayın. Merhaba tablodaki Hello sütun toohello veriler, her satır, veri dosyanızın karşılık gelmelidir.

toocreate tablo, bir komut istemi açın ve sqlcmd.exe toorun hello aşağıdaki komutu kullanın:

```sql
sqlcmd.exe -S <server name> -d <database name> -U <username> -P <password> -I -Q "
    CREATE TABLE DimDate2
    (
        DateId INT NOT NULL,
        CalendarQuarter TINYINT NOT NULL,
        FiscalQuarter TINYINT NOT NULL
    )
    ;
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

```bcp
bcp <TableName> out C:\Temp\DimDate2_export.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <Password> -q -c -t , 
```

## <a name="3-load-hello-data"></a>3. Merhaba veri yükleme
tooload hello verileri, bir komut istemi açın ve aşağıdaki komut, sunucu adı, veritabanı adı, kullanıcı adı ve parola alanlarına kendi bilgilerinizi hello değerleri değiştirerek hello çalıştırın.

```bcp
bcp DimDate2 in C:\Temp\DimDate2.txt -S <ServerName> -d <DatabaseName> -U <Username> -P <password> -q -c -t  ,
```

Bu komut tooverify hello verilerin düzgün şekilde yüklendiğini kullanın

```bcp
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

## <a name="next-steps"></a>Sonraki adımlar
bir SQL Server veritabanı toomigrate bkz [SQL Server veritabanı geçiş](sql-database-cloud-migrate.md).

<!--MSDN references-->
[bcp]: https://msdn.microsoft.com/library/ms162802.aspx
[CREATE TABLE syntax]: https://msdn.microsoft.com/library/mt203953.aspx

<!--Other Web references-->
[Microsoft Download Center]: https://www.microsoft.com/download/details.aspx?id=36433
