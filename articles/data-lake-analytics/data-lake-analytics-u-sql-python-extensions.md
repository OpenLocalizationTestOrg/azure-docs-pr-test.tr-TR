---
title: "aaaExtend U-SQL komut dosyaları Azure Data Lake Analytics Python ile | Microsoft Docs"
description: "U-SQL betikleri toorun Python kodu nasıl öğrenin"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: c1c74e5e-3e4a-41ab-9e3f-e9085da1d315
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/20/2017
ms.author: saveenr
ms.openlocfilehash: f051f56f67522d4f2b8e6e54fd21a5c95ce3ba92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-get-started-with-extending-u-sql-with-python"></a><span data-ttu-id="1f8b9-103">Öğretici: U-SQL Python ile genişletme ile çalışmaya başlama</span><span class="sxs-lookup"><span data-stu-id="1f8b9-103">Tutorial: Get started with extending U-SQL with Python</span></span>

<span data-ttu-id="1f8b9-104">U-SQL için Python uzantıları geliştiriciler Python kodu tooperform yüksek düzeyde Paralel yürütme etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="1f8b9-104">Python Extensions for U-SQL enable developers tooperform massively parallel execution of Python code.</span></span> <span data-ttu-id="1f8b9-105">Aşağıdaki örnek hello hello temel adımlar gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="1f8b9-105">hello following example illustrates hello basic steps:</span></span>

* <span data-ttu-id="1f8b9-106">Kullanım hello `REFERENCE ASSEMBLY` hello U-SQL betiği için deyimi tooenable Python uzantıları</span><span class="sxs-lookup"><span data-stu-id="1f8b9-106">Use hello `REFERENCE ASSEMBLY` statement tooenable Python extensions for hello U-SQL Script</span></span>
* <span data-ttu-id="1f8b9-107">Hello kullanarak `REDUCE` işlemi toopartition hello giriş verileri bir anahtarı</span><span class="sxs-lookup"><span data-stu-id="1f8b9-107">Using hello `REDUCE` operation toopartition hello input data on a key</span></span>
* <span data-ttu-id="1f8b9-108">Merhaba U-SQL için Python uzantıları dahil yerleşik reducer (`Extension.Python.Reducer`) her atanan köşe toohello reducer Python kodu çalıştırır</span><span class="sxs-lookup"><span data-stu-id="1f8b9-108">hello Python extensions for U-SQL include a built-in reducer (`Extension.Python.Reducer`) that runs Python code on each vertex assigned toohello reducer</span></span>
* <span data-ttu-id="1f8b9-109">Hello U-SQL betiği içerir adlı bir işlev katıştırılmış hello Python kodu `usqlml_main` pandas DataFrame giriş olarak kabul eder ve pandas DataFrame çıktısı olarak döndürür.</span><span class="sxs-lookup"><span data-stu-id="1f8b9-109">hello U-SQL script contains hello embedded Python code that has a function called `usqlml_main` that accepts a pandas DataFrame as input and returns a pandas DataFrame as output.</span></span>

--

    REFERENCE ASSEMBLY [ExtPython];

    DECLARE @myScript = @"
    def get_mentions(tweet):
        return ';'.join( ( w[1:] for w in tweet.split() if w[0]=='@' ) )

    def usqlml_main(df):
        del df['time']
        del df['author']
        df['mentions'] = df.tweet.apply(get_mentions)
        del df['tweet']
        return df
    ";

    @t  = 
        SELECT * FROM 
           (VALUES
               ("D1","T1","A1","@foo Hello World @bar"),
               ("D2","T2","A2","@baz Hello World @beer")
           ) AS 
               D( date, time, author, tweet );

    @m  =
        REDUCE @t ON date
        PRODUCE date string, mentions string
        USING new Extension.Python.Reducer(pyScript:@myScript);

    OUTPUT @m
        too"/tweetmentions.csv"
        USING Outputters.Csv();

## <a name="how-python-integrates-with-u-sql"></a><span data-ttu-id="1f8b9-110">Python U-SQL ile nasıl tümleşik çalıştığını</span><span class="sxs-lookup"><span data-stu-id="1f8b9-110">How Python Integrates with U-SQL</span></span>

### <a name="datatypes"></a><span data-ttu-id="1f8b9-111">Veri türleri</span><span class="sxs-lookup"><span data-stu-id="1f8b9-111">Datatypes</span></span>

* <span data-ttu-id="1f8b9-112">U-SQL dizesi ve sayısal sütunlarından olarak dönüştürülür-Pandas ve U-SQL arasında</span><span class="sxs-lookup"><span data-stu-id="1f8b9-112">String and numeric columns from U-SQL are converted as-is between Pandas and U-SQL</span></span>
* <span data-ttu-id="1f8b9-113">U-SQL null değerlere olan Pandas gelen dönüştürülmüş tooand `NA` değerleri</span><span class="sxs-lookup"><span data-stu-id="1f8b9-113">U-SQL Nulls are converted tooand from Pandas `NA` values</span></span>

### <a name="schemas"></a><span data-ttu-id="1f8b9-114">Şemalar</span><span class="sxs-lookup"><span data-stu-id="1f8b9-114">Schemas</span></span>

* <span data-ttu-id="1f8b9-115">Dizin vektörlerinin Pandas, U-SQL desteklenmez.</span><span class="sxs-lookup"><span data-stu-id="1f8b9-115">Index vectors in Pandas are not supported in U-SQL.</span></span> <span data-ttu-id="1f8b9-116">Tüm giriş verilerini çerçeveleri hello Python işlevinde her zaman 0 hello sayıda satırı eksi 1 ile 64-bit sayısal dizinden sahiptir.</span><span class="sxs-lookup"><span data-stu-id="1f8b9-116">All input data frames in hello Python function always have a 64-bit numerical index from 0 through hello number of rows minus 1.</span></span> 
* <span data-ttu-id="1f8b9-117">U-SQL veri kümeleri yinelenen sütun adlarına sahip olamaz</span><span class="sxs-lookup"><span data-stu-id="1f8b9-117">U-SQL datasets cannot have duplicate column names</span></span>
* <span data-ttu-id="1f8b9-118">Dize olmayan U-SQL veri kümeleri sütun adları.</span><span class="sxs-lookup"><span data-stu-id="1f8b9-118">U-SQL datasets column names that are not strings.</span></span> 

### <a name="python-versions"></a><span data-ttu-id="1f8b9-119">Python sürümleri</span><span class="sxs-lookup"><span data-stu-id="1f8b9-119">Python Versions</span></span>
<span data-ttu-id="1f8b9-120">Yalnızca Python 3.5.1 (Windows için derlenmiş) desteklenir.</span><span class="sxs-lookup"><span data-stu-id="1f8b9-120">Only Python 3.5.1 (compiled for Windows) is supported.</span></span> 

### <a name="standard-python-modules"></a><span data-ttu-id="1f8b9-121">Standart Python modülleri</span><span class="sxs-lookup"><span data-stu-id="1f8b9-121">Standard Python modules</span></span>
<span data-ttu-id="1f8b9-122">Tüm hello standart Python modülleri dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="1f8b9-122">All hello standard Python modules are included.</span></span>

### <a name="additional-python-modules"></a><span data-ttu-id="1f8b9-123">Ek Python modülleri</span><span class="sxs-lookup"><span data-stu-id="1f8b9-123">Additional Python modules</span></span>
<span data-ttu-id="1f8b9-124">Standart Python kitaplıkları hello yanında birçok yaygın olarak kullanılan python kitaplıkları eklenmiştir:</span><span class="sxs-lookup"><span data-stu-id="1f8b9-124">Besides hello standard Python libraries, several commonly used python libraries are included:</span></span>

    pandas
    numpy
    numexpr

### <a name="exception-messages"></a><span data-ttu-id="1f8b9-125">Özel durum iletileri</span><span class="sxs-lookup"><span data-stu-id="1f8b9-125">Exception Messages</span></span>
<span data-ttu-id="1f8b9-126">Şu anda Python kodu bir özel durum Genel köşe hata olarak görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="1f8b9-126">Currently, an exception in Python code shows up as generic vertex failure.</span></span> <span data-ttu-id="1f8b9-127">Hello gelecekteki, hello U-SQL işi hata iletileri hello Python özel durum iletisi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="1f8b9-127">In hello future, hello U-SQL Job error messages will display hello Python exception message.</span></span>

### <a name="input-and-output-size-limitations"></a><span data-ttu-id="1f8b9-128">Giriş ve çıkış boyutu sınırlamaları</span><span class="sxs-lookup"><span data-stu-id="1f8b9-128">Input and Output size limitations</span></span>
<span data-ttu-id="1f8b9-129">Her köşe sınırlı bir tooit atanan bellek miktarı var.</span><span class="sxs-lookup"><span data-stu-id="1f8b9-129">Every vertex has a limited amount of memory assigned tooit.</span></span> <span data-ttu-id="1f8b9-130">Şu anda bu sınırı bir AU için 6 GB'tır.</span><span class="sxs-lookup"><span data-stu-id="1f8b9-130">Currently, that limit is 6 GB for an AU.</span></span> <span data-ttu-id="1f8b9-131">Merhaba giriş ve çıkış DataFrames hello Python kodu bellekte varolması gerektiğinden, hello giriş ve çıkış toplam boyutu hello 6 GB aşamaz.</span><span class="sxs-lookup"><span data-stu-id="1f8b9-131">Because hello input and output DataFrames must exist in memory in hello Python code, hello total size for hello input and output cannot exceed 6 GB.</span></span>

## <a name="see-also"></a><span data-ttu-id="1f8b9-132">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="1f8b9-132">See also</span></span>
* [<span data-ttu-id="1f8b9-133">Microsoft Azure Data Lake Analytics'e genel bakış</span><span class="sxs-lookup"><span data-stu-id="1f8b9-133">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="1f8b9-134">Visual Studio için Data Lake Araçları'nı kullanarak U-SQL betikleri geliştirme</span><span class="sxs-lookup"><span data-stu-id="1f8b9-134">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
* [<span data-ttu-id="1f8b9-135">Azure Data Lake Analytics işleri için U-SQL penceresi işlevlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="1f8b9-135">Using U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)

