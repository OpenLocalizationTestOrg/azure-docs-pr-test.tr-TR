---
title: "aaaLoad örnek verileri SQL veri ambarında | Microsoft Docs"
description: "SQL Data Warehouse'a örnek veri yükleme"
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: e338ecf8-cfee-419b-b7b6-98108d381c62
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: 3459c42f3aae51c27fd35db7874faf99e1e577e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="load-sample-data-into-sql-data-warehouse"></a>SQL Data Warehouse'a örnek veri yükleme
Bu basit adımları tooload ve sorgu hello Adventure Works örnek veritabanını izleyin. Bu komut, ilk sqlcmd toorun tabloları ve görünümleri oluşturacak olan SQL kullanın. Tablo oluşturulduktan sonra hello betikleri bcp tooload verileri kullanın.  Sqlcmd ve yüklü bcp zaten sahip değilseniz, bu bağlantıları çok izleyin[bcp yüklemek] [ install bcp] ve çok[sqlcmd yüklemek][install sqlcmd].

## <a name="load-sample-data"></a>Örnek verileri yükleme
1. Merhaba karşıdan [SQL Data Warehouse için Adventure Works örnek komut dosyaları] [ Adventure Works Sample Scripts for SQL Data Warehouse] zip dosyası.
2. Yerel makinenizde indirilen ZIP tooa dizininden Hello dosyaları ayıklayın.
3. Ayıklanan hello dosya aw_create.bat düzenleyin ve değişkenleri hello dosya hello üstünde bulunan aşağıdaki hello ayarlayın.  Hiçbir boşluk arasındaki hello "=" hello parametre emin tooleave olabilir.  Düzenlemeleriniz nasıl görünebileceği örnekleri aşağıda verilmiştir.
   
    ```
    server=mylogicalserver.database.windows.net
    user=mydwuser
    password=Mydwpassw0rd
    database=mydwdatabase
    ```
4. Bir Windows komut isteminden çalıştırma hello aw_create.bat düzenlenemez.  Düzenlenen aw_create.bat sürümünüz kaydettiğiniz hello dizininde olduğundan emin olun.
   Bu komut dosyası olacak...
   
   * Adventure Works tablolar veya veritabanınızda zaten görünümleri bırakın
   * Merhaba Adventure Works tablolar ve görünümler oluşturma
   * BCP kullanarak her Adventure Works tablosu yükleme
   * Her Adventure Works tablo Hello satır sayılarını doğrula
   * Her sütun için her Adventure Works tablo istatistikleri Topla

## <a name="query-sample-data"></a>Örnek verileri Sorgulama
SQL Data Warehouse'a bazı örnek veriler yüklenen sonra birkaç sorgu hızlı bir şekilde çalıştırabilirsiniz.  toorun bir sorgu hello açıklandığı gibi yeni oluşturulan tooyour Adventure Works Visual Studio ve SSDT, kullanarak Azure SQL DW veritabanında bağlanmak [sorgu Visual Studio ile] [ query with Visual Studio] belge.

Basit bir örneği hello çalışan tüm hello bilgilerini deyimi tooget seçin:

```sql
SELECT * FROM DimEmployee;
```

GROUP BY toolook gibi yapıları hello toplam tutarı için tüm sales her gün kullanarak daha karmaşık bir sorgu örneği:

```sql
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

WHERE yan tümcesi toofilter belirli bir tarihten önce siparişleri çıkışı ile bir SELECT örneği:

```
SELECT OrderDateKey, SUM(SalesAmount) AS TotalSales
FROM FactInternetSales
WHERE OrderDateKey > '20020801'
GROUP BY OrderDateKey
ORDER BY OrderDateKey;
```

SQL veri ambarı SQL Server destekleyen neredeyse tüm T-SQL yapılarını destekler.  Farkları belgelenmiştir bizim [kodunu taşıma] [ migrate code] belgeleri.

## <a name="next-steps"></a>Sonraki adımlar
Bazı sorgular örnek verilerle bir fırsat tootry karşılaşmışsınız, nasıl çok denetleyin[geliştirmek][develop], [yük][load], veya [ geçiş] [ migrate] tooSQL veri ambarı.

<!--Image references-->

<!--Article references-->
[migrate]: sql-data-warehouse-overview-migrate.md
[develop]: sql-data-warehouse-overview-develop.md
[load]: sql-data-warehouse-overview-load.md
[query with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[migrate code]: sql-data-warehouse-migrate-code.md
[install bcp]: sql-data-warehouse-load-with-bcp.md
[install sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md

<!--Other Web references-->
[Adventure Works Sample Scripts for SQL Data Warehouse]: https://migrhoststorage.blob.core.windows.net/sqldwsample/AdventureWorksSQLDW2012.zip
