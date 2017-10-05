---
title: "U-SQL Kataloğu ile çalışmaya başlama | Microsoft Docs"
description: "U-SQL kataloğunu kod ve veri paylaşmak için nasıl kullanılacağını öğrenin."
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
ms.openlocfilehash: 08364c6c7bea53807844e3b1cc327dc3742e0487
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-u-sql-catalog"></a><span data-ttu-id="3895e-103">U-SQL Kataloğu ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="3895e-103">Get started with the U-SQL Catalog</span></span>

## <a name="create-a-tvf"></a><span data-ttu-id="3895e-104">Bir TVF oluşturma</span><span class="sxs-lookup"><span data-stu-id="3895e-104">Create a TVF</span></span>

<span data-ttu-id="3895e-105">Önceki U-SQL komut dosyası aynı kaynak dosyasını okumaya EXTRACT kullanımını yinelenir.</span><span class="sxs-lookup"><span data-stu-id="3895e-105">In the previous U-SQL script, you repeated the use of EXTRACT to read from the same source file.</span></span> <span data-ttu-id="3895e-106">U-SQL tablo değerli işlev (TVF), gelecekte tekrar kullanmak için veri yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3895e-106">With the U-SQL table-valued function (TVF), you can encapsulate the data for future reuse.</span></span>  

<span data-ttu-id="3895e-107">Aşağıdaki komut dosyası olarak adlandırılan bir TVF oluşturur `Searchlog()` şema ve varsayılan veritabanı içinde:</span><span class="sxs-lookup"><span data-stu-id="3895e-107">The following script creates a TVF called `Searchlog()` in the default database and schema:</span></span>

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

<span data-ttu-id="3895e-108">Aşağıdaki komut dosyası önceki betik tanımlandı TVF kullanmayı gösterir:</span><span class="sxs-lookup"><span data-stu-id="3895e-108">The following script shows you how to use the TVF that was defined in the previous script:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM Searchlog() AS S
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    TO "/output/SerachLog-use-tvf.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-views"></a><span data-ttu-id="3895e-109">Görünümler oluşturma</span><span class="sxs-lookup"><span data-stu-id="3895e-109">Create views</span></span>

<span data-ttu-id="3895e-110">Bir tek sorgu ifadesi varsa, TVF yerine, U-SQL görünümü ifade kapsüllemek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3895e-110">If you have a single query expression, instead of a TVF you can use a U-SQL VIEW to encapsulate that expression.</span></span>

<span data-ttu-id="3895e-111">Aşağıdaki komut dosyası adlı bir görünüm oluşturur `SearchlogView` şema ve varsayılan veritabanı içinde:</span><span class="sxs-lookup"><span data-stu-id="3895e-111">The following script creates a view called `SearchlogView` in the default database and schema:</span></span>

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

<span data-ttu-id="3895e-112">Aşağıdaki komut dosyası tanımlı görünüm kullanımını göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="3895e-112">The following script demonstrates the use of the defined view:</span></span>

```
@res =
    SELECT
        Region,
        SUM(Duration) AS TotalDuration
    FROM SearchlogView
GROUP BY Region
HAVING SUM(Duration) > 200;

OUTPUT @res
    TO "/output/Searchlog-use-view.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

## <a name="create-tables"></a><span data-ttu-id="3895e-113">Tabloları oluşturma</span><span class="sxs-lookup"><span data-stu-id="3895e-113">Create tables</span></span>
<span data-ttu-id="3895e-114">İlişkisel veritabanı tablolarıyla U-SQL ile bir tablo ile önceden tanımlanmış bir şema oluşturabilir veya şema sorgusu oluşturur bir tablo oluşturmak gibi tablonun (olarak da bilinen CREATE TABLE AS SELECT veya CTAS) doldurur.</span><span class="sxs-lookup"><span data-stu-id="3895e-114">As with relational database tables, with U-SQL you can create a table with a predefined schema or create a table that infers the schema from the query that populates the table (also known as CREATE TABLE AS SELECT or CTAS).</span></span>

<span data-ttu-id="3895e-115">Aşağıdaki komut dosyası kullanarak bir veritabanı ve iki tablo oluşturun:</span><span class="sxs-lookup"><span data-stu-id="3895e-115">Create a database and two tables by using the following script:</span></span>

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

## <a name="query-tables"></a><span data-ttu-id="3895e-116">Sorgu tabloları</span><span class="sxs-lookup"><span data-stu-id="3895e-116">Query tables</span></span>
<span data-ttu-id="3895e-117">Tablolar, veri dosyalarını sorgu aynı şekilde önceki komut dosyasındaki oluşturulanlar gibi sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3895e-117">You can query tables, such as those created in the previous script, in the same way that you query the data files.</span></span> <span data-ttu-id="3895e-118">EXTRACT kullanarak bir satır kümesi oluşturmak yerine, şimdi tablo adına başvurabilir.</span><span class="sxs-lookup"><span data-stu-id="3895e-118">Instead of creating a rowset by using EXTRACT, you now can refer to the table name.</span></span>

<span data-ttu-id="3895e-119">Tablodan okumak için daha önce kullanılan dönüştürme komut dosyasını değiştirin:</span><span class="sxs-lookup"><span data-stu-id="3895e-119">To read from the tables, modify the transform script that you used previously:</span></span>

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
    TO "/output/Searchlog-query-table.csv"
    ORDER BY TotalDuration DESC
    USING Outputters.Csv();
```

 >[!NOTE]
 ><span data-ttu-id="3895e-120">Şu anda, bir SELECT aynı komut dosyasını bir tabloda tablonun oluşturulduğu çalıştıramazsınız.</span><span class="sxs-lookup"><span data-stu-id="3895e-120">Currently, you cannot run a SELECT on a table in the same script as the one where you created the table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3895e-121">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="3895e-121">Next Steps</span></span>
* [<span data-ttu-id="3895e-122">Microsoft Azure Data Lake Analytics'e genel bakış</span><span class="sxs-lookup"><span data-stu-id="3895e-122">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="3895e-123">Visual Studio için Data Lake Araçları'nı kullanarak U-SQL betikleri geliştirme</span><span class="sxs-lookup"><span data-stu-id="3895e-123">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="3895e-124">Azure portalını kullanarak Azure Data Lake Analytics işlerini izleme ve sorun giderme</span><span class="sxs-lookup"><span data-stu-id="3895e-124">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
