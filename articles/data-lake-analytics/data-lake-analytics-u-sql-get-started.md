---
title: "U-SQL dili ile çalışmaya başlama | Microsoft Docs"
description: "Merhaba U-SQL dili Hello temellerini öğrenin."
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
ms.date: 06/23/2017
ms.author: saveenr
ms.openlocfilehash: 5edee0e0d85211e84b3d47895c53d71f0a19f083
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-u-sql"></a><span data-ttu-id="18c49-103">U-SQL ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="18c49-103">Get started with U-SQL</span></span>
<span data-ttu-id="18c49-104">Bildirim temelli SQL birleştiren bir dil olan U-SQL kesinlik temelli C# toolet ile verileri herhangi ölçekli işleme.</span><span class="sxs-lookup"><span data-stu-id="18c49-104">U-SQL is a language that combines declarative SQL with imperative C# toolet you process data at any scale.</span></span> <span data-ttu-id="18c49-105">Merhaba ölçeklenebilir, dağıtılmış sorgu yeteneğini U-SQL, Azure SQL veritabanı gibi ilişkisel depoları arasında veri verimli bir şekilde çözümleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="18c49-105">Through hello scalable, distributed-query capability of U-SQL, you can efficiently analyze data across relational stores such as Azure SQL Database.</span></span> <span data-ttu-id="18c49-106">U-SQL ile yapılandırılmamış veriler üzerinde okuma şema uygulama ve Özel mantık ve UDF'ler ekleme işleyebilir.</span><span class="sxs-lookup"><span data-stu-id="18c49-106">With U-SQL, you can process unstructured data by applying schema on read and inserting custom logic and UDFs.</span></span> <span data-ttu-id="18c49-107">Ayrıca, U-SQL nasıl üzerinde ayrıntılı denetim sağlar genişletilebilirlik içerir ölçekte tooexecute.</span><span class="sxs-lookup"><span data-stu-id="18c49-107">Additionally, U-SQL includes extensibility that gives you fine-grained control over how tooexecute at scale.</span></span> 

## <a name="learning-resources"></a><span data-ttu-id="18c49-108">Öğrenme kaynakları</span><span class="sxs-lookup"><span data-stu-id="18c49-108">Learning resources</span></span>

* <span data-ttu-id="18c49-109">Merhaba [U-SQL öğretici](http://aka.ms/usqltutorial) çoğu hello U-SQL dili için bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="18c49-109">hello [U-SQL Tutorial](http://aka.ms/usqltutorial) provides a guided walkthrough of most of hello U-SQL language.</span></span> <span data-ttu-id="18c49-110">Bu belge, U-SQL toolearn isteyen tüm geliştiriciler için okuma önerilir.</span><span class="sxs-lookup"><span data-stu-id="18c49-110">This document is recommended reading for all developers wanting toolearn U-SQL.</span></span>
* <span data-ttu-id="18c49-111">Merhaba hakkında ayrıntılı bilgi için **U-SQL dili sözdizimi**, hello bkz [U-SQL dili başvurusu](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="18c49-111">For detailed information about hello **U-SQL language syntax**, see hello [U-SQL Language Reference](http://go.microsoft.com/fwlink/p/?LinkId=691348).</span></span>
* <span data-ttu-id="18c49-112">toounderstand hello **U-SQL tasarımı felsefesi**, bkz: hello Visual Studio blog yayını [Tanıtımı U-SQL – büyük veri işleme kolaylaştırır bir dil](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span><span class="sxs-lookup"><span data-stu-id="18c49-112">toounderstand hello **U-SQL design philosophy**, see hello Visual Studio blog post [Introducing U-SQL – A Language that makes Big Data Processing Easy](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18c49-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="18c49-113">Prerequisites</span></span>

<span data-ttu-id="18c49-114">Bu belgedeki hello U-SQL örnekleri üzerinden geçmeden önce okuyun ve tamamlamak [öğretici: Visual Studio için Data Lake Araçları'nı kullanarak geliştirme U-SQL betikleri](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="18c49-114">Before you go through hello U-SQL samples in this document, read and complete [Tutorial: Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span> <span data-ttu-id="18c49-115">Bu öğretici, U-SQL Visual Studio için Azure Data Lake araçları ile kullanma hello mekanizması açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="18c49-115">That tutorial explains hello mechanics of using U-SQL with Azure Data Lake Tools for Visual Studio.</span></span>

## <a name="your-first-u-sql-script"></a><span data-ttu-id="18c49-116">İlk U-SQL betiğiniz</span><span class="sxs-lookup"><span data-stu-id="18c49-116">Your first U-SQL script</span></span>

<span data-ttu-id="18c49-117">U-SQL betiği aşağıdaki hello basittir ve birçok yönlerini hello U-SQL dili keşfetmemizi sağlar.</span><span class="sxs-lookup"><span data-stu-id="18c49-117">hello following U-SQL script is simple and lets us explore many aspects hello U-SQL language.</span></span>

```
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

OUTPUT @searchlog   
    too"/output/SearchLog-first-u-sql.csv"
    USING Outputters.Csv();
```

<span data-ttu-id="18c49-118">Bu betik, herhangi bir dönüştürme adım sahip değil.</span><span class="sxs-lookup"><span data-stu-id="18c49-118">This script doesn't have any transformation steps.</span></span> <span data-ttu-id="18c49-119">Adlı hello kaynak dosyasından okur `SearchLog.tsv`, onu schematizes ve hello satır kümesi geri SearchLog-first-u-sql.csv adlı bir dosyaya yazar.</span><span class="sxs-lookup"><span data-stu-id="18c49-119">It reads from hello source file called `SearchLog.tsv`, schematizes it, and writes hello rowset back into a file called SearchLog-first-u-sql.csv.</span></span>

<span data-ttu-id="18c49-120">Fark hello soru işareti sonraki toohello veri türü hello `Duration` alan.</span><span class="sxs-lookup"><span data-stu-id="18c49-120">Notice hello question mark next toohello data type in hello `Duration` field.</span></span> <span data-ttu-id="18c49-121">Bu hello anlamına gelir `Duration` alanı null olabilir.</span><span class="sxs-lookup"><span data-stu-id="18c49-121">It means that hello `Duration` field could be null.</span></span>

### <a name="key-concepts"></a><span data-ttu-id="18c49-122">Önemli kavramlar</span><span class="sxs-lookup"><span data-stu-id="18c49-122">Key concepts</span></span>
* <span data-ttu-id="18c49-123">**Satır kümesi değişkenleri**: satır üreten her sorgu ifadesi tooa değişkeni atanabilir.</span><span class="sxs-lookup"><span data-stu-id="18c49-123">**Rowset variables**: Each query expression that produces a rowset can be assigned tooa variable.</span></span> <span data-ttu-id="18c49-124">U-SQL hello T-SQL değişken adlandırma deseni izler (`@searchlog`, örneğin) hello komut.</span><span class="sxs-lookup"><span data-stu-id="18c49-124">U-SQL follows hello T-SQL variable naming pattern (`@searchlog`, for example) in hello script.</span></span>
* <span data-ttu-id="18c49-125">Merhaba **AYIKLAMAK** anahtar sözcüğü bir dosyadan veri okuyan ve okuma hello şema tanımlar.</span><span class="sxs-lookup"><span data-stu-id="18c49-125">hello **EXTRACT** keyword reads data from a file and defines hello schema on read.</span></span> <span data-ttu-id="18c49-126">`Extractors.Tsv`Sekme ayrılmış değer dosyaları için yerleşik bir U-SQL Ayıklayıcısı ' dir.</span><span class="sxs-lookup"><span data-stu-id="18c49-126">`Extractors.Tsv` is a built-in U-SQL extractor for tab-separated-value files.</span></span> <span data-ttu-id="18c49-127">Özel ayıklayıcıları geliştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="18c49-127">You can develop custom extractors.</span></span>
* <span data-ttu-id="18c49-128">Merhaba **çıkış** bir satır kümesi tooa dosyasından veri yazar.</span><span class="sxs-lookup"><span data-stu-id="18c49-128">hello **OUTPUT** writes data from a rowset tooa file.</span></span> <span data-ttu-id="18c49-129">`Outputters.Csv()`Yerleşik bir U-SQL outputter toocreate bir virgülle ayrılmış değer dosyasıdır.</span><span class="sxs-lookup"><span data-stu-id="18c49-129">`Outputters.Csv()` is a built-in U-SQL outputter toocreate a comma-separated-value file.</span></span> <span data-ttu-id="18c49-130">Özel outputters geliştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="18c49-130">You can develop custom outputters.</span></span>

### <a name="file-paths"></a><span data-ttu-id="18c49-131">Dosya yolları</span><span class="sxs-lookup"><span data-stu-id="18c49-131">File paths</span></span>

<span data-ttu-id="18c49-132">Merhaba EXTRACT ve çıktı deyimleri dosya yolları kullanın.</span><span class="sxs-lookup"><span data-stu-id="18c49-132">hello EXTRACT and OUTPUT statements use file paths.</span></span> <span data-ttu-id="18c49-133">Dosya yolları mutlak veya göreli olabilir:</span><span class="sxs-lookup"><span data-stu-id="18c49-133">File paths can be absolute or relative:</span></span>

<span data-ttu-id="18c49-134">Bu aşağıdaki mutlak dosya yolu adlı bir Data Lake Store tooa dosyasında başvuruyor `mystore`:</span><span class="sxs-lookup"><span data-stu-id="18c49-134">This following absolute file path refers tooa file in a Data Lake Store named `mystore`:</span></span>

    adl://mystore.azuredatalakestore.net/Samples/Data/SearchLog.tsv

<span data-ttu-id="18c49-135">Bu aşağıdaki dosya yolu ile başlayan `"/"`.</span><span class="sxs-lookup"><span data-stu-id="18c49-135">This following file path starts with `"/"`.</span></span> <span data-ttu-id="18c49-136">Merhaba varsayılan Data Lake Store hesabı tooa dosyasına başvurur:</span><span class="sxs-lookup"><span data-stu-id="18c49-136">It refers tooa file in hello default Data Lake Store account:</span></span>

    /output/SearchLog-first-u-sql.csv

## <a name="use-scalar-variables"></a><span data-ttu-id="18c49-137">Skaler değişkenleri kullanma</span><span class="sxs-lookup"><span data-stu-id="18c49-137">Use scalar variables</span></span>

<span data-ttu-id="18c49-138">Skaler değişkenleri iyi toomake betik bakım daha kolay kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="18c49-138">You can use scalar variables as well toomake your script maintenance easier.</span></span> <span data-ttu-id="18c49-139">Merhaba önceki U-SQL komut dosyası olarak da yazılabilir:</span><span class="sxs-lookup"><span data-stu-id="18c49-139">hello previous U-SQL script can also be written as:</span></span>

    DECLARE @in  string = "/Samples/Data/SearchLog.tsv";
    DECLARE @out string = "/output/SearchLog-scalar-variables.csv";

    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM @in
        USING Extractors.Tsv();

    OUTPUT @searchlog   
        too@out
        USING Outputters.Csv();

## <a name="transform-rowsets"></a><span data-ttu-id="18c49-140">Satır kümeleri dönüştürme</span><span class="sxs-lookup"><span data-stu-id="18c49-140">Transform rowsets</span></span>

<span data-ttu-id="18c49-141">Kullanım **seçin** tootransform satır kümeleri:</span><span class="sxs-lookup"><span data-stu-id="18c49-141">Use **SELECT** tootransform rowsets:</span></span>

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

    @rs1 =
        SELECT Start, Region, Duration
        FROM @searchlog
    WHERE Region == "en-gb";

    OUTPUT @rs1   
        too"/output/SearchLog-transform-rowsets.csv"
        USING Outputters.Csv();

<span data-ttu-id="18c49-142">WHERE yan tümcesi kullanan hello bir [C# Boole ifadesi](https://msdn.microsoft.com/library/6a71f45d.aspx).</span><span class="sxs-lookup"><span data-stu-id="18c49-142">hello WHERE clause uses a [C# Boolean expression](https://msdn.microsoft.com/library/6a71f45d.aspx).</span></span> <span data-ttu-id="18c49-143">Merhaba C# ifade dil toodo kendi ifadeleri ve işlevlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="18c49-143">You can use hello C# expression language toodo your own expressions and functions.</span></span> <span data-ttu-id="18c49-144">Daha karmaşık mantıksal bağlaçlar (kaldırmalı) ve disjunctions (ORs) birleştirerek filtreleme bile gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="18c49-144">You can even perform more complex filtering by combining them with logical conjunctions (ANDs) and disjunctions (ORs).</span></span>

<span data-ttu-id="18c49-145">Merhaba aşağıdaki betiği hello DateTime.Parse() yöntemi ve bir birlikte kullanır.</span><span class="sxs-lookup"><span data-stu-id="18c49-145">hello following script uses hello DateTime.Parse() method and a conjunction.</span></span>

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

    @rs1 =
        SELECT Start, Region, Duration
        FROM @searchlog
    WHERE Region == "en-gb";

    @rs1 =
        SELECT Start, Region, Duration
        FROM @rs1
        WHERE Start >= DateTime.Parse("2012/02/16") AND Start <= DateTime.Parse("2012/02/17");

    OUTPUT @rs1   
        too"/output/SearchLog-transform-datetime.csv"
        USING Outputters.Csv();

 >[!NOTE]
 ><span data-ttu-id="18c49-146">Merhaba ikinci sorguyu hello bileşimi iki filtre oluşturur hello ilk satır hello sonucu üzerinde çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="18c49-146">hello second query is operating on hello result of hello first rowset, which creates a composite of hello two filters.</span></span> <span data-ttu-id="18c49-147">Bir değişken adı yeniden kullanabilir ve hello adları sözcüksel olarak kapsamındaki.</span><span class="sxs-lookup"><span data-stu-id="18c49-147">You can also reuse a variable name, and hello names are scoped lexically.</span></span>

## <a name="aggregate-rowsets"></a><span data-ttu-id="18c49-148">Toplu satır kümeleri</span><span class="sxs-lookup"><span data-stu-id="18c49-148">Aggregate rowsets</span></span>
<span data-ttu-id="18c49-149">Tanıdık ORDER BY, GROUP BY ve toplamalar hello U-SQL sağlar.</span><span class="sxs-lookup"><span data-stu-id="18c49-149">U-SQL gives you hello familiar ORDER BY, GROUP BY, and aggregations.</span></span>

<span data-ttu-id="18c49-150">Merhaba aşağıdaki sorguyu hello toplam süre bölge başına bulur ve ardından hello üst sırada beş süreleri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="18c49-150">hello following query finds hello total duration per region, and then displays hello top five durations in order.</span></span>

<span data-ttu-id="18c49-151">U-SQL satır kümeleri sıralarına hello sonraki sorgu için korumaz.</span><span class="sxs-lookup"><span data-stu-id="18c49-151">U-SQL rowsets do not preserve their order for hello next query.</span></span> <span data-ttu-id="18c49-152">Bu nedenle, çıktı, bir tooorder tooadd ORDER BY toohello çıkış deyimi gerekir:</span><span class="sxs-lookup"><span data-stu-id="18c49-152">Thus, tooorder an output, you need tooadd ORDER BY toohello OUTPUT statement:</span></span>

    DECLARE @outpref string = "/output/Searchlog-aggregation";
    DECLARE @out1    string = @outpref+"_agg.csv";
    DECLARE @out2    string = @outpref+"_top5agg.csv";

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

    @rs1 =
        SELECT
            Region,
            SUM(Duration) AS TotalDuration
        FROM @searchlog
    GROUP BY Region;

    @res =
        SELECT *
        FROM @rs1
        ORDER BY TotalDuration DESC
        FETCH 5 ROWS;

    OUTPUT @rs1
        too@out1
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

    OUTPUT @res
        too@out2
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

<span data-ttu-id="18c49-153">Hello U-SQL ORDER BY yan tümcesi SELECT ifadesinde hello FETCH yan tümcesinin kullanılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="18c49-153">hello U-SQL ORDER BY clause requires using hello FETCH clause in a SELECT expression.</span></span>

<span data-ttu-id="18c49-154">Merhaba U-SQL sahip yan hello HAVING koşulu karşılıyor kullanılan toorestrict hello çıktı toogroups olabilir:</span><span class="sxs-lookup"><span data-stu-id="18c49-154">hello U-SQL HAVING clause can be used toorestrict hello output toogroups that satisfy hello HAVING condition:</span></span>

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

    @res =
        SELECT
            Region,
            SUM(Duration) AS TotalDuration
        FROM @searchlog
        GROUP BY Region
        HAVING SUM(Duration) > 200;

    OUTPUT @res
        too"/output/Searchlog-having.csv"
        ORDER BY TotalDuration DESC
        USING Outputters.Csv();

<span data-ttu-id="18c49-155">Gelişmiş toplama senaryoları için hello hello U-SQL başvuru belgelerine bakın [toplama, çözümleme ve başvuru işlevleri](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)</span><span class="sxs-lookup"><span data-stu-id="18c49-155">For advanced aggregation scenarios, see hello hello U-SQL reference documentation for [aggregate, analytic, and reference functions](https://msdn.microsoft.com/en-us/library/azure/mt621335.aspx)</span></span>

## <a name="next-steps"></a><span data-ttu-id="18c49-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="18c49-156">Next steps</span></span>
* [<span data-ttu-id="18c49-157">Microsoft Azure Data Lake Analytics'e genel bakış</span><span class="sxs-lookup"><span data-stu-id="18c49-157">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="18c49-158">Visual Studio için Data Lake Araçları'nı kullanarak U-SQL betikleri geliştirme</span><span class="sxs-lookup"><span data-stu-id="18c49-158">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
