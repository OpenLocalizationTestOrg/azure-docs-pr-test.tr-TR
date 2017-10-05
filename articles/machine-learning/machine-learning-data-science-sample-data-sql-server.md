---
title: "Örnek veri Azure üzerinde SQL Server'daki | Microsoft Docs"
description: "Azure SQL Server'da örnek veri"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 33c030d4-5cca-4cc9-99d7-2bd13a3926af
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 1bdcc7175dac325de1144d805e977264524b3fbc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="8b83a-103"><a name="heading"></a>Azure üzerinde SQL Server örnek veri</span><span class="sxs-lookup"><span data-stu-id="8b83a-103"><a name="heading"></a>Sample data in SQL Server on Azure</span></span>
<span data-ttu-id="8b83a-104">Bu belgede Azure SQL sunucusunda depolanan verileri örnek SQL veya Python programlama dili kullanılarak gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="8b83a-104">This document shows how to sample data stored in SQL Server on Azure using either SQL or the Python programming language.</span></span> <span data-ttu-id="8b83a-105">Ayrıca, bir dosyaya kaydetmeyi, bir Azure blob karşıya yükleme ve Azure Machine Learning Studio'ya okuma Azure Machine Learning örneklenen verileri taşımak nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="8b83a-105">It also shows how to move sampled data into Azure Machine Learning by saving it to a file, uploading it to an Azure blob, and then reading it into Azure Machine Learning Studio.</span></span>

<span data-ttu-id="8b83a-106">Python örnekleme kullandığı [pyodbc](https://code.google.com/p/pyodbc/) Azure SQL sunucusuna bağlanmak için ODBC kitaplığı ve [Pandas](http://pandas.pydata.org/) örnekleme yapmak için kitaplık.</span><span class="sxs-lookup"><span data-stu-id="8b83a-106">The Python sampling uses the [pyodbc](https://code.google.com/p/pyodbc/) ODBC library to connect to SQL Server on Azure and the [Pandas](http://pandas.pydata.org/) library to do the sampling.</span></span>

> [!NOTE]
> <span data-ttu-id="8b83a-107">Örnek SQL kod bu belgedeki verileri Azure SQL Server'da olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="8b83a-107">The sample SQL code in this document assumes that the data is in a SQL Server on Azure.</span></span> <span data-ttu-id="8b83a-108">Değilse, lütfen [veri taşıma SQL Server için Azure üzerinde](machine-learning-data-science-move-sql-server-virtual-machine.md) konu verilerinizi Azure üzerinde SQL Server'a taşıma konusunda yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="8b83a-108">If it is not, please refer to [Move data to SQL Server on Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) topic for instructions on how to move your data to SQL Server on Azure.</span></span>
> 
> 

<span data-ttu-id="8b83a-109">Aşağıdaki **menü** çeşitli depolama ortamlarından veri örneği nasıl açıklayan konulara bağlantılar.</span><span class="sxs-lookup"><span data-stu-id="8b83a-109">The following **menu** links to topics that describe how to sample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="8b83a-110">**Neden verilerinizi örnek?**</span><span class="sxs-lookup"><span data-stu-id="8b83a-110">**Why sample your data?**</span></span>
<span data-ttu-id="8b83a-111">Analiz etmek için planlama dataset büyükse, genellikle aşağı örnek için daha küçük, ancak temsili ve daha kolay yönetilebilir bir boyutunu azaltmak için veri için iyi bir fikir değil.</span><span class="sxs-lookup"><span data-stu-id="8b83a-111">If the dataset you plan to analyze is large, it's usually a good idea to down-sample the data to reduce it to a smaller but representative and more manageable size.</span></span> <span data-ttu-id="8b83a-112">Bu, veri anlama, keşfi ve özellik Mühendisliği kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="8b83a-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="8b83a-113">Kendi rolünde [takım veri bilimi işlem (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) hızlı prototipi oluşturulurken veri işleme işlevleri ve makine öğrenimi modellerinin oluşturulmasına olanak sağlamasıdır.</span><span class="sxs-lookup"><span data-stu-id="8b83a-113">Its role in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) is to enable fast prototyping of the data processing functions and machine learning models.</span></span>

<span data-ttu-id="8b83a-114">Bir adımda bu örnekleme görevdir [takım veri bilimi işlem (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="8b83a-114">This sampling task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <span data-ttu-id="8b83a-115"><a name="SQL"></a>SQL kullanarak</span><span class="sxs-lookup"><span data-stu-id="8b83a-115"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="8b83a-116">Bu bölümde SQL kullanarak basit rastgele örnekleme veri karşı veritabanında gerçekleştirmek için çeşitli yöntemler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="8b83a-116">This section describes several methods using SQL to perform simple random sampling against the data in the database.</span></span> <span data-ttu-id="8b83a-117">Lütfen, veri boyutu ve onun dağıtım dayalı bir yöntem seçin.</span><span class="sxs-lookup"><span data-stu-id="8b83a-117">Please choose a method based on your data size and its distribution.</span></span>

<span data-ttu-id="8b83a-118">Aşağıdaki iki öğeyi NEWID SQL Server'da örnekleme gerçekleştirmek için nasıl kullanılacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="8b83a-118">The two items below show how to use newid in SQL Server to perform the sampling.</span></span> <span data-ttu-id="8b83a-119">Seçtiğiniz yöntem nasıl rastgele olması için örnek istediğiniz bağlıdır (Aşağıdaki örnek kodda pk_id olduğu varsayılır otomatik olarak oluşturulan bir birincil anahtar).</span><span class="sxs-lookup"><span data-stu-id="8b83a-119">The method you choose depends on how random you want the sample to be (pk_id in the sample code below is assumed to be an auto-generated primary key).</span></span>

1. <span data-ttu-id="8b83a-120">Daha az kesin rasgele örnek</span><span class="sxs-lookup"><span data-stu-id="8b83a-120">Less strict random sample</span></span>
   
        select  * from <table_name> where <primary_key> in 
        (select top 10 percent <primary_key> from <table_name> order by newid())
2. <span data-ttu-id="8b83a-121">Daha fazla rasgele örnek</span><span class="sxs-lookup"><span data-stu-id="8b83a-121">More random sample</span></span> 
   
        SELECT * FROM <table_name>
        WHERE 0.1 >= CAST(CHECKSUM(NEWID(), <primary_key>) & 0x7fffffff AS float)/ CAST (0x7fffffff AS int)

<span data-ttu-id="8b83a-122">Tablesample için örnekleme kullanılan yanı sıra aşağıda gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="8b83a-122">Tablesample can be used for sampling as well as demonstrated below.</span></span> <span data-ttu-id="8b83a-123">(Veri sihirbazın farklı sayfalarında değil bağıntılı varsayılarak), veri boyutu büyükse ve makul bir sürede tamamlamak bir sorgu için bu daha iyi bir yaklaşım olabilir.</span><span class="sxs-lookup"><span data-stu-id="8b83a-123">This may be a better approach if your data size is large (assuming that data on different pages is not correlated) and for the query to complete in a reasonable time.</span></span>

    SELECT *
    FROM <table_name> 
    TABLESAMPLE (10 PERCENT)

> [!NOTE]
> <span data-ttu-id="8b83a-124">Keşfetmek ve yeni bir tabloda depolayarak örneklenen bu verilerden Özellikleri Oluştur</span><span class="sxs-lookup"><span data-stu-id="8b83a-124">You can explore and generate features from this sampled data by storing it in a new table</span></span>
> 
> 

### <span data-ttu-id="8b83a-125"><a name="sql-aml"></a>Azure Machine Learning ile bağlanma</span><span class="sxs-lookup"><span data-stu-id="8b83a-125"><a name="sql-aml"></a>Connecting to Azure Machine Learning</span></span>
<span data-ttu-id="8b83a-126">Yukarıdaki örnek sorgular Azure Machine Learning ile doğrudan kullanabilirsiniz [veri içeri aktarma] [ import-data] aşağı-kolay bir şekilde veri örneği ve bir Azure Machine Learning deneme hale getirmek için modülü.</span><span class="sxs-lookup"><span data-stu-id="8b83a-126">You can directly  use the sample queries above in the Azure Machine Learning [Import Data][import-data] module to down-sample the data on the fly and bring it into an Azure Machine Learning experiment.</span></span> <span data-ttu-id="8b83a-127">Örneklenen verileri okumak için okuyucu modülü kullanarak bir ekran görüntüsü aşağıda gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="8b83a-127">A screen shot of using the reader module to read the sampled data is shown below:</span></span>

![Okuyucu sql][1]

## <span data-ttu-id="8b83a-129"><a name="python"></a>Python programlama dili kullanma</span><span class="sxs-lookup"><span data-stu-id="8b83a-129"><a name="python"></a>Using the Python programming language</span></span>
<span data-ttu-id="8b83a-130">Bu bölüm kullanarak gösterir [pyodbc Kitaplığı](https://code.google.com/p/pyodbc/) Python bir SQL server veritabanında bir ODBC bağlantı kurulacak.</span><span class="sxs-lookup"><span data-stu-id="8b83a-130">This section demonstrates using the [pyodbc library](https://code.google.com/p/pyodbc/) to establish an ODBC connect to a SQL server database in Python.</span></span> <span data-ttu-id="8b83a-131">Veritabanı bağlantı dizesi şu şekildedir: (servername, dbname, kullanıcı adı ve parola yapılandırmanızı değiştirin):</span><span class="sxs-lookup"><span data-stu-id="8b83a-131">The database connection string is as follows: (replace servername, dbname, username and password with your configuration):</span></span>

    #Set up the SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="8b83a-132">[Pandas](http://pandas.pydata.org/) Python kitaplıkta Python programlama için veri işleme için zengin bir veri yapılarını ve veri çözümleme araçları sağlar.</span><span class="sxs-lookup"><span data-stu-id="8b83a-132">The [Pandas](http://pandas.pydata.org/) library in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="8b83a-133">Aşağıdaki kodu % 0,1 örnek verileri Azure SQL veritabanındaki bir tablo Pandas verisine okur:</span><span class="sxs-lookup"><span data-stu-id="8b83a-133">The code below reads a 0.1% sample of the data from a table in Azure SQL database into a Pandas data :</span></span>

    import pandas as pd

    # Query database and load the returned results in pandas data frame
    data_frame = pd.read_sql('''select column1, cloumn2... from <table_name> tablesample (0.1 percent)''', conn)

<span data-ttu-id="8b83a-134">Şimdi, örneklenen verileri Pandas veri çerçevesinde çalışabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b83a-134">You can now work with the sampled data in the Pandas data frame.</span></span> 

### <span data-ttu-id="8b83a-135"><a name="python-aml"></a>Azure Machine Learning ile bağlanma</span><span class="sxs-lookup"><span data-stu-id="8b83a-135"><a name="python-aml"></a>Connecting to Azure Machine Learning</span></span>
<span data-ttu-id="8b83a-136">Aşağıdaki örnek kod, aşağı örneklenen verileri bir dosyaya kaydedin ve bir Azure blobuna yüklemek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8b83a-136">You can use the following sample code to save the down-sampled data to a file and upload it to an Azure blob.</span></span> <span data-ttu-id="8b83a-137">Blob verileri doğrudan bir Azure Machine Learning deneme okunabilir kullanarak [veri içeri aktarma] [ import-data] modülü.</span><span class="sxs-lookup"><span data-stu-id="8b83a-137">The data in the blob can be directly read into an Azure Machine Learning Experiment using the [Import Data][import-data] module.</span></span> <span data-ttu-id="8b83a-138">Adımlar aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="8b83a-138">The steps are as follows:</span></span> 

1. <span data-ttu-id="8b83a-139">Pandas veri çerçevesi yerel bir dosyaya yazma</span><span class="sxs-lookup"><span data-stu-id="8b83a-139">Write the pandas data frame to a local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="8b83a-140">Yerel dosya Azure blobuna yükle</span><span class="sxs-lookup"><span data-stu-id="8b83a-140">Upload local file to Azure blob</span></span>
   
        from azure.storage import BlobService
        import tables
   
        STORAGEACCOUNTNAME= <storage_account_name>
        LOCALFILENAME= <local_file_name>
        STORAGEACCOUNTKEY= <storage_account_key>
        CONTAINERNAME= <container_name>
        BLOBNAME= <blob_name>
   
        output_blob_service=BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)    
        localfileprocessed = os.path.join(os.getcwd(),LOCALFILENAME) #assuming file is in current working directory
   
        try:
   
        #perform upload
        output_blob_service.put_block_blob_from_path(CONTAINERNAME,BLOBNAME,localfileprocessed)
   
        except:            
            print ("Something went wrong with uploading blob:"+BLOBNAME)
3. <span data-ttu-id="8b83a-141">Azure Machine Learning kullanarak Azure blob üzerinden veri okuma [veri içeri aktarma] [ import-data] ekran Al aşağıda gösterildiği gibi Modülü:</span><span class="sxs-lookup"><span data-stu-id="8b83a-141">Read data from Azure blob using Azure Machine Learning [Import Data][import-data] module as shown in the screen grab below:</span></span>

![Okuyucu blob][2]

## <a name="the-team-data-science-process-in-action-example"></a><span data-ttu-id="8b83a-143">Eylem örnekte takım veri bilimi işlemi</span><span class="sxs-lookup"><span data-stu-id="8b83a-143">The Team Data Science Process in Action example</span></span>
<span data-ttu-id="8b83a-144">Bir ortak bir veri kümesini kullanarak takım veri bilimi işlemi bir uçtan uca kılavuz örneği için bkz [takım veri bilimi işlemi sürüyor: SQL sunucusu kullanarak](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="8b83a-144">For an end-to-end walkthrough example of the Team Data Science Process a using a public dataset, see [Team Data Science Process in Action: using SQL Sever](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_database.png
[2]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_blob.png

[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
