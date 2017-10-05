---
title: SQL Server sanal makine veri azure'de | Microsoft Docs
description: "Azure üzerinde bir SQL Server VM depolanan verileri araştırmak nasıl."
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
ms.openlocfilehash: a2be21ef15b9209db1e97150e0297558fa69a7be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="explore-data-in-sql-server-virtual-machine-on-azure"></a><span data-ttu-id="a5f87-103">Azure üzerindeki SQL Server Sanal Makinesi verilerini keşfetme</span><span class="sxs-lookup"><span data-stu-id="a5f87-103">Explore data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="a5f87-104">Bu belge, Azure üzerinde bir SQL Server VM depolanan verileri araştırmak alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a5f87-104">This document covers how to explore data that is stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="a5f87-105">Bu SQL kullanarak veri wrangling veya Python gibi bir programlama dili kullanılarak yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="a5f87-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

<span data-ttu-id="a5f87-106">Aşağıdaki **menü** araçları çeşitli depolama ortamlarından verileri araştırmak için nasıl kullanılacağını açıklayan konulara bağlantılar.</span><span class="sxs-lookup"><span data-stu-id="a5f87-106">The following **menu** links to topics that describe how to use tools to explore data from various storage environments.</span></span> <span data-ttu-id="a5f87-107">Bu görev Cortana analitik işlem (CAP) bir adımdır.</span><span class="sxs-lookup"><span data-stu-id="a5f87-107">This task is a step in the Cortana Analytics Process (CAP).</span></span>

[!INCLUDE [cap-explore-data-selector](../../includes/cap-explore-data-selector.md)]

> [!NOTE]
> <span data-ttu-id="a5f87-108">Bu belgede örnek SQL deyimlerinde veri SQL Server'da olduğunu varsayın.</span><span class="sxs-lookup"><span data-stu-id="a5f87-108">The sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="a5f87-109">Öyle değilse, SQL Server'a verilerinizi taşıma hakkında bilgi edinmek için bulut veri bilimi işlem eşlemesi bakın.</span><span class="sxs-lookup"><span data-stu-id="a5f87-109">If it isn't, refer to the cloud data science process map to learn how to move your data to SQL Server.</span></span>
> 
> 

## <span data-ttu-id="a5f87-110"><a name="sql-dataexploration"></a>SQL komut dosyaları ile SQL veri keşfedin</span><span class="sxs-lookup"><span data-stu-id="a5f87-110"><a name="sql-dataexploration"></a>Explore SQL data with SQL scripts</span></span>
<span data-ttu-id="a5f87-111">Burada, SQL Server veri depolarında keşfetmek için kullanılabilecek birkaç örnek SQL komut dosyaları bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a5f87-111">Here are a few sample SQL scripts that can be used to explore data stores in SQL Server.</span></span>

1. <span data-ttu-id="a5f87-112">Gün başına gözlemleri sayısını alın</span><span class="sxs-lookup"><span data-stu-id="a5f87-112">Get the count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="a5f87-113">Kategorik bir sütunda düzeylerini Al</span><span class="sxs-lookup"><span data-stu-id="a5f87-113">Get the levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="a5f87-114">İki kategorik sütun arada düzey sayısını Al</span><span class="sxs-lookup"><span data-stu-id="a5f87-114">Get the number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="a5f87-115">Sayısal sütunlar için dağıtım Al</span><span class="sxs-lookup"><span data-stu-id="a5f87-115">Get the distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

> [!NOTE]
> <span data-ttu-id="a5f87-116">Pratik bir örnek için kullandığınız [NYC ücreti dataset](http://www.andresmh.com/nyctaxitrips/) ve başlıklı IPNB başvuruda [IPython not defteri ve SQL Server kullanarak NYC veri wrangling](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) bir uçtan uca gözden geçirme.</span><span class="sxs-lookup"><span data-stu-id="a5f87-116">For a practical example, you can use the [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer to the IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

## <span data-ttu-id="a5f87-117"><a name="python"></a>Python ile SQL veri keşfedin</span><span class="sxs-lookup"><span data-stu-id="a5f87-117"><a name="python"></a>Explore SQL data with Python</span></span>
<span data-ttu-id="a5f87-118">Verileri araştırmak ve verileri SQL Server olduğunda özellikleri oluşturmak için Python kullanarak benzer açıklandığı gibi Python kullanarak Azure blob veri işleme için [veri bilimi ortamınızdaki işlem Azure Blob veri](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="a5f87-118">Using Python to explore data and generate features when the data is in SQL Server is similar to processing data in Azure blob using Python, as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="a5f87-119">Veriler veritabanından pandas DataFrame yüklenmesi gerektiğini ve ardından daha fazla işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="a5f87-119">The data needs to be loaded from the database into a pandas DataFrame and then can be processed further.</span></span> <span data-ttu-id="a5f87-120">Biz, veritabanına bağlanmak ve bu bölümdeki DataFrame içine veri yükleme işleminde belge.</span><span class="sxs-lookup"><span data-stu-id="a5f87-120">We document the process of connecting to the database and loading the data into the DataFrame in this section.</span></span>

<span data-ttu-id="a5f87-121">Aşağıdaki bağlantı dizesi biçimi Python pyodbc (Değiştir servername, dbname, kullanıcı adı ve parola, belirli değerleri içeren) kullanarak bir SQL Server veritabanına bağlanmak için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="a5f87-121">The following connection string format can be used to connect to a SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up the SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="a5f87-122">[Pandas Kitaplığı](http://pandas.pydata.org/) Python içinde Python programlama için veri işleme için zengin bir veri yapılarını ve veri çözümleme araçları sağlar.</span><span class="sxs-lookup"><span data-stu-id="a5f87-122">The [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="a5f87-123">Aşağıdaki kod, bir SQL Server veritabanından Pandas veri çerçeveye sonuçları döndüren okur:</span><span class="sxs-lookup"><span data-stu-id="a5f87-123">The following code reads the results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load the returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="a5f87-124">Konusunda anlatıldığı gibi Pandas DataFrame ile çalışabilirsiniz artık [veri bilimi ortamınızdaki işlem Azure Blob veri](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="a5f87-124">Now you can work with the Pandas DataFrame as covered in the topic [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="cortana-analytics-process-in-action-example"></a><span data-ttu-id="a5f87-125">Eylem örnekte Cortana Analytics işlemi</span><span class="sxs-lookup"><span data-stu-id="a5f87-125">Cortana Analytics Process in Action Example</span></span>
<span data-ttu-id="a5f87-126">Cortana Analytics ortak bir veri kümesini kullanarak işlem uçtan uca kılavuz örneği için bkz: [eylem takım veri bilimi işlem: SQL Server'ı kullanarak](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="a5f87-126">For an end-to-end walkthrough example of the Cortana Analytics Process using a public dataset, see [The Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

