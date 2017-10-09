---
title: "aaaExplore verileri içindeki SQL Server sanal makinede Azure | Microsoft Docs"
description: "Nasıl bir SQL Server VM Azure üzerinde depolanan tooexplore veri."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ccbb3085-af9e-4ec2-9df2-15dcab261d05
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: fcc449fc0d0e49be9b673cfb2de347cf44804017
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="explore-data-in-sql-server-virtual-machine-on-azure"></a><span data-ttu-id="a59ee-103">Azure üzerindeki SQL Server Sanal Makinesi verilerini keşfetme</span><span class="sxs-lookup"><span data-stu-id="a59ee-103">Explore data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="a59ee-104">Bu belgede ele alınmaktadır nasıl Azure üzerinde bir SQL Server VM depolanan tooexplore veri.</span><span class="sxs-lookup"><span data-stu-id="a59ee-104">This document covers how tooexplore data that is stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="a59ee-105">Bu SQL kullanarak veri wrangling veya Python gibi bir programlama dili kullanılarak yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="a59ee-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

<span data-ttu-id="a59ee-106">Merhaba aşağıdaki **menü** nasıl toouse tooexplore veri çeşitli depolama ortamlarından araçları açıklamak tootopics bağlar.</span><span class="sxs-lookup"><span data-stu-id="a59ee-106">hello following **menu** links tootopics that describe how toouse tools tooexplore data from various storage environments.</span></span> <span data-ttu-id="a59ee-107">Bu görev hello Cortana analitik işlem (CAP) bir adımdır.</span><span class="sxs-lookup"><span data-stu-id="a59ee-107">This task is a step in hello Cortana Analytics Process (CAP).</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

> [!NOTE]
> <span data-ttu-id="a59ee-108">Merhaba örnek SQL deyimleri bu belgedeki verileri SQL Server'da olduğunu varsayın.</span><span class="sxs-lookup"><span data-stu-id="a59ee-108">hello sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="a59ee-109">Öyle değilse, toohello bulut veri bilimi işlem harita toolearn nasıl başvurmak toomove, veri tooSQL sunucu.</span><span class="sxs-lookup"><span data-stu-id="a59ee-109">If it isn't, refer toohello cloud data science process map toolearn how toomove your data tooSQL Server.</span></span>
> 
> 

## <span data-ttu-id="a59ee-110"><a name="sql-dataexploration"></a>SQL komut dosyaları ile SQL veri keşfedin</span><span class="sxs-lookup"><span data-stu-id="a59ee-110"><a name="sql-dataexploration"></a>Explore SQL data with SQL scripts</span></span>
<span data-ttu-id="a59ee-111">Burada, SQL Server kullanılan tooexplore veri depolarında olabilecek birkaç örnek SQL komut dosyaları bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a59ee-111">Here are a few sample SQL scripts that can be used tooexplore data stores in SQL Server.</span></span>

1. <span data-ttu-id="a59ee-112">Gün başına gözlemleri Hello sayısını alın</span><span class="sxs-lookup"><span data-stu-id="a59ee-112">Get hello count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="a59ee-113">Merhaba düzeylerini kategorik sütunda Al</span><span class="sxs-lookup"><span data-stu-id="a59ee-113">Get hello levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="a59ee-114">İki kategorik sütun arada Hello düzey sayısını Al</span><span class="sxs-lookup"><span data-stu-id="a59ee-114">Get hello number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="a59ee-115">Merhaba dağıtım sayısal sütunlar için alma</span><span class="sxs-lookup"><span data-stu-id="a59ee-115">Get hello distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

> [!NOTE]
> <span data-ttu-id="a59ee-116">Pratik bir örnek için hello kullanabilirsiniz [NYC ücreti dataset](http://www.andresmh.com/nyctaxitrips/) ve toohello başlıklı IPNB başvuruda [IPython not defteri ve SQL Server kullanarak NYC veri wrangling](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) bir uçtan uca gözden geçirme.</span><span class="sxs-lookup"><span data-stu-id="a59ee-116">For a practical example, you can use hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer toohello IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

## <span data-ttu-id="a59ee-117"><a name="python"></a>Python ile SQL veri keşfedin</span><span class="sxs-lookup"><span data-stu-id="a59ee-117"><a name="python"></a>Explore SQL data with Python</span></span>
<span data-ttu-id="a59ee-118">Python tooexplore verileri kullanarak ve veri olan SQL Server'da hello benzer tooprocessing veri Python kullanarak Azure blob içinde açıklandığı gibi olduğunda Özellikleri Oluştur [veri bilimi ortamınızdaki işlem Azure Blob veri](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="a59ee-118">Using Python tooexplore data and generate features when hello data is in SQL Server is similar tooprocessing data in Azure blob using Python, as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="a59ee-119">Merhaba veri pandas DataFrame hello veritabanından yüklenen toobe gerekir ve ardından daha fazla işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="a59ee-119">hello data needs toobe loaded from hello database into a pandas DataFrame and then can be processed further.</span></span> <span data-ttu-id="a59ee-120">Biz toohello veritabanına bağlanma ve bu bölümdeki DataFrame hello içine hello veri yükleme hello işleminde belge.</span><span class="sxs-lookup"><span data-stu-id="a59ee-120">We document hello process of connecting toohello database and loading hello data into hello DataFrame in this section.</span></span>

<span data-ttu-id="a59ee-121">bağlantı dizesi biçimi aşağıdaki hello pyodbc (Değiştir servername, dbname, kullanıcı adı ve parola, belirli değerleri içeren) kullanarak Python kullanılan tooconnect tooa SQL Server veritabanından olabilir:</span><span class="sxs-lookup"><span data-stu-id="a59ee-121">hello following connection string format can be used tooconnect tooa SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="a59ee-122">Merhaba [Pandas Kitaplığı](http://pandas.pydata.org/) Python içinde Python programlama için veri işleme için zengin bir veri yapılarını ve veri çözümleme araçları sağlar.</span><span class="sxs-lookup"><span data-stu-id="a59ee-122">hello [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="a59ee-123">Merhaba aşağıdaki kodu hello sonuçları bir SQL Server veritabanından Pandas veri çerçeveye döndürülen okur:</span><span class="sxs-lookup"><span data-stu-id="a59ee-123">hello following code reads hello results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="a59ee-124">Merhaba konuda anlatıldığı gibi hello Pandas DataFrame ile çalışabilirsiniz artık [veri bilimi ortamınızdaki işlem Azure Blob veri](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="a59ee-124">Now you can work with hello Pandas DataFrame as covered in hello topic [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="cortana-analytics-process-in-action-example"></a><span data-ttu-id="a59ee-125">Eylem örnekte Cortana Analytics işlemi</span><span class="sxs-lookup"><span data-stu-id="a59ee-125">Cortana Analytics Process in Action Example</span></span>
<span data-ttu-id="a59ee-126">Merhaba Cortana Analytics ortak bir veri kümesini kullanarak işlem uçtan uca kılavuz örneği için bkz: [takım veri bilimi işlemi eylemde hello: SQL Server'ı kullanarak](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="a59ee-126">For an end-to-end walkthrough example of hello Cortana Analytics Process using a public dataset, see [hello Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

