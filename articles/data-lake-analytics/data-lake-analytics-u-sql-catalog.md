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
# <a name="get-started-with-hello-u-sql-catalog"></a><span data-ttu-id="85f76-103">U-SQL kataloğunu Hello ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="85f76-103">Get started with hello U-SQL Catalog</span></span>

## <a name="create-a-tvf"></a><span data-ttu-id="85f76-104">Bir TVF oluşturma</span><span class="sxs-lookup"><span data-stu-id="85f76-104">Create a TVF</span></span>

<span data-ttu-id="85f76-105">EXTRACT tooread hello gelen hello kullanımını yinelenen Hello önceki U-SQL komut dosyasında, aynı kaynak dosyası.</span><span class="sxs-lookup"><span data-stu-id="85f76-105">In hello previous U-SQL script, you repeated hello use of EXTRACT tooread from hello same source file.</span></span> <span data-ttu-id="85f76-106">Merhaba U-SQL tablo değerli işlevi ile (TVF), gelecekte tekrar kullanmak için hello verileri yerleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85f76-106">With hello U-SQL table-valued function (TVF), you can encapsulate hello data for future reuse.</span></span>  

<span data-ttu-id="85f76-107">Merhaba aşağıdaki betiği oluşturur adlı bir TVF `Searchlog()` hello varsayılan veritabanı ve şemasında:</span><span class="sxs-lookup"><span data-stu-id="85f76-107">hello following script creates a TVF called `Searchlog()` in hello default database and schema:</span></span>

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

<span data-ttu-id="85f76-108">komut dosyası izleyen hello nasıl toouse hello hello önceki komut dosyasında tanımlanan TVF gösterir:</span><span class="sxs-lookup"><span data-stu-id="85f76-108">hello following script shows you how toouse hello TVF that was defined in hello previous script:</span></span>

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

## <a name="create-views"></a><span data-ttu-id="85f76-109">Görünümler oluşturma</span><span class="sxs-lookup"><span data-stu-id="85f76-109">Create views</span></span>

<span data-ttu-id="85f76-110">TVF yerine tek bir sorgu ifadesi varsa, bu deyim bir U-SQL görünümü tooencapsulate kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85f76-110">If you have a single query expression, instead of a TVF you can use a U-SQL VIEW tooencapsulate that expression.</span></span>

<span data-ttu-id="85f76-111">Merhaba aşağıdaki betiği oluşturur adlı bir görünüm `SearchlogView` hello varsayılan veritabanı ve şemasında:</span><span class="sxs-lookup"><span data-stu-id="85f76-111">hello following script creates a view called `SearchlogView` in hello default database and schema:</span></span>

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

<span data-ttu-id="85f76-112">komut dosyası izleyen hello tanımlanan hello görünüm hello kullanımını göstermektedir:</span><span class="sxs-lookup"><span data-stu-id="85f76-112">hello following script demonstrates hello use of hello defined view:</span></span>

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

## <a name="create-tables"></a><span data-ttu-id="85f76-113">Tabloları oluşturma</span><span class="sxs-lookup"><span data-stu-id="85f76-113">Create tables</span></span>
<span data-ttu-id="85f76-114">İlişkisel veritabanı tablolarıyla U-SQL ile bir tablo ile önceden tanımlanmış bir şema oluşturabilir veya bir tablo oluşturmak gibi hello tablosu (olarak da bilinen CREATE TABLE AS SELECT veya CTAS) doldurur hello sorgu hello şemadan oluşturur.</span><span class="sxs-lookup"><span data-stu-id="85f76-114">As with relational database tables, with U-SQL you can create a table with a predefined schema or create a table that infers hello schema from hello query that populates hello table (also known as CREATE TABLE AS SELECT or CTAS).</span></span>

<span data-ttu-id="85f76-115">Komut dosyası izleyen hello kullanarak bir veritabanı ve iki tablo oluşturun:</span><span class="sxs-lookup"><span data-stu-id="85f76-115">Create a database and two tables by using hello following script:</span></span>

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

## <a name="query-tables"></a><span data-ttu-id="85f76-116">Sorgu tabloları</span><span class="sxs-lookup"><span data-stu-id="85f76-116">Query tables</span></span>
<span data-ttu-id="85f76-117">Merhaba içinde hello önceki komut oluşturulanlar gibi tabloları sorgulayabilir aynı şekilde hello veri dosyalarını sorgu.</span><span class="sxs-lookup"><span data-stu-id="85f76-117">You can query tables, such as those created in hello previous script, in hello same way that you query hello data files.</span></span> <span data-ttu-id="85f76-118">EXTRACT kullanarak bir satır kümesi oluşturmak yerine, toohello tablo adı şimdi başvurabilir.</span><span class="sxs-lookup"><span data-stu-id="85f76-118">Instead of creating a rowset by using EXTRACT, you now can refer toohello table name.</span></span>

<span data-ttu-id="85f76-119">Merhaba tablolardan tooread daha önce kullanılan hello dönüştürme betiği değiştirin:</span><span class="sxs-lookup"><span data-stu-id="85f76-119">tooread from hello tables, modify hello transform script that you used previously:</span></span>

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
 ><span data-ttu-id="85f76-120">Şu anda, bir SELECT aynı bir hello gibi komut dosyası hello tablosunda hello tablo oluşturulduğu çalıştıramazsınız.</span><span class="sxs-lookup"><span data-stu-id="85f76-120">Currently, you cannot run a SELECT on a table in hello same script as hello one where you created hello table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="85f76-121">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="85f76-121">Next Steps</span></span>
* [<span data-ttu-id="85f76-122">Microsoft Azure Data Lake Analytics'e genel bakış</span><span class="sxs-lookup"><span data-stu-id="85f76-122">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="85f76-123">Visual Studio için Data Lake Araçları'nı kullanarak U-SQL betikleri geliştirme</span><span class="sxs-lookup"><span data-stu-id="85f76-123">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="85f76-124">Azure portalını kullanarak Azure Data Lake Analytics işlerini izleme ve sorun giderme</span><span class="sxs-lookup"><span data-stu-id="85f76-124">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
