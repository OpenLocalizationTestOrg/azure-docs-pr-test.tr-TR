---
title: "U-SQL Hello Kataloğu ile çalışmaya başlama | Microsoft Docs"
description: "U-SQL toouse hello nasıl katalog tooshare kodunuz ve verileriniz hakkında bilgi edinin."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 57143396-ab86-47dd-b6f8-613ba28c28d2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/09/2017
ms.author: edmaca
ms.openlocfilehash: 559bb7a3879031eb290a3e82946d7bf42ac9f553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-u-sql-catalog"></a>U-SQL kataloğunu Hello ile çalışmaya başlama

## <a name="create-a-tvf"></a>Bir TVF oluşturma

EXTRACT tooread hello gelen hello kullanımını yinelenen Hello önceki U-SQL komut dosyasında, aynı kaynak dosyası. Merhaba U-SQL tablo değerli işlevi ile (TVF), gelecekte tekrar kullanmak için hello verileri yerleştirebilirsiniz.  

Merhaba aşağıdaki betiği oluşturur adlı bir TVF `Searchlog()` hello varsayılan veritabanı ve şemasında:

```
DROP FUNCTION IF EXISTS Searchlog;

CREATE FUNCTION Searchlog()
RETURNS @searchlog TABLE
(
            UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
)
AS BEGIN
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM "/Samples/Data/SearchLog.tsv"
USING Extractors.Tsv();
RETURN;
END;
```

komut dosyası izleyen hello nasıl toouse hello hello önceki komut dosyasında tanımlanan TVF gösterir:

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM Searchlog() AS S
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    too"/output/SerachLog-use-tvf.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-views"></a>Görünümler oluşturma

TVF yerine tek bir sorgu ifadesi varsa, bu deyim bir U-SQL görünümü tooencapsulate kullanabilirsiniz.

Merhaba aşağıdaki betiği oluşturur adlı bir görünüm `SearchlogView` hello varsayılan veritabanı ve şemasında:

```
DROP VIEW IF EXISTS SearchlogView;

CREATE VIEW SearchlogView AS  
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM "/Samples/Data/SearchLog.tsv"
USING Extractors.Tsv();
```

komut dosyası izleyen hello tanımlanan hello görünüm hello kullanımını göstermektedir:

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM SearchlogView
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    too"/output/Searchlog-use-view.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-tables"></a>Tabloları oluşturma
İlişkisel veritabanı tablolarıyla U-SQL ile bir tablo ile önceden tanımlanmış bir şema oluşturabilir veya bir tablo oluşturmak gibi hello tablosu (olarak da bilinen CREATE TABLE AS SELECT veya CTAS) doldurur hello sorgu hello şemadan oluşturur.

Komut dosyası izleyen hello kullanarak bir veritabanı ve iki tablo oluşturun:

```
DROP DATABASE IF EXISTS SearchLogDb;
CREATE DATABASE SearchLogDb;
USE DATABASE SearchLogDb;

DROP TABLE IF EXISTS SearchLog1;
DROP TABLE IF EXISTS SearchLog2;

CREATE TABLE SearchLog1 (
            UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string,

            INDEX sl_idx CLUSTERED (UserId ASC)
                DISTRIBUTED BY HASH (UserId)
);

INSERT INTO SearchLog1 SELECT * FROM master.dbo.Searchlog() AS s;

CREATE TABLE SearchLog2(
    INDEX sl_idx CLUSTERED (UserId ASC)
            DISTRIBUTED BY HASH (UserId)
) AS SELECT * FROM master.dbo.Searchlog() AS S; // You can use EXTRACT or SELECT here
```

## <a name="query-tables"></a>Sorgu tabloları
Merhaba içinde hello önceki komut oluşturulanlar gibi tabloları sorgulayabilir aynı şekilde hello veri dosyalarını sorgu. EXTRACT kullanarak bir satır kümesi oluşturmak yerine, toohello tablo adı şimdi başvurabilir.

Merhaba tablolardan tooread daha önce kullanılan hello dönüştürme betiği değiştirin:

```
@rs1 =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM SearchLogDb.dbo.SearchLog2
GROUP BY Region;

@res =
    SELECT *
    FROM @rs1
    ORDER BY TotalDuration DESC
    FETCH 5 ROWS;

OUTPUT @res
    too"/output/Searchlog-query-table.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

 >[!NOTE]
 >Şu anda, bir SELECT aynı bir hello gibi komut dosyası hello tablosunda hello tablo oluşturulduğu çalıştıramazsınız.

## <a name="next-steps"></a>Sonraki Adımlar
* [Microsoft Azure Data Lake Analytics'e genel bakış](data-lake-analytics-overview.md)
* [Visual Studio için Data Lake Araçları'nı kullanarak U-SQL betikleri geliştirme](data-lake-analytics-data-lake-tools-get-started.md)
* [Azure portalını kullanarak Azure Data Lake Analytics işlerini izleme ve sorun giderme](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
