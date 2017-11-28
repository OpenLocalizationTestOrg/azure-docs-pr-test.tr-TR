---
title: Azure SQL Server'da verilerde aaaSample | Microsoft Docs
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
ms.openlocfilehash: dc7f9529c771f6deb633775557e64a04b774f5b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="96ccc-103"><a name="heading"></a>Azure üzerinde SQL Server örnek veri</span><span class="sxs-lookup"><span data-stu-id="96ccc-103"><a name="heading"></a>Sample data in SQL Server on Azure</span></span>
<span data-ttu-id="96ccc-104">Bu belgede Azure üzerinde SQL Server'daki toosample verilerin depolanma SQL veya hello Python programlama dili kullanılarak gösterir.</span><span class="sxs-lookup"><span data-stu-id="96ccc-104">This document shows how toosample data stored in SQL Server on Azure using either SQL or hello Python programming language.</span></span> <span data-ttu-id="96ccc-105">Aynı zamanda, nasıl toomove verileri Azure Machine Learning tooa dosyası, onu karşıya kaydederek tooan Azure blob ve Azure Machine Learning Studio'ya okuma örneklenen gösterir.</span><span class="sxs-lookup"><span data-stu-id="96ccc-105">It also shows how toomove sampled data into Azure Machine Learning by saving it tooa file, uploading it tooan Azure blob, and then reading it into Azure Machine Learning Studio.</span></span>

<span data-ttu-id="96ccc-106">Merhaba Python örnekleme kullanan hello [pyodbc](https://code.google.com/p/pyodbc/) ODBC kitaplığı tooconnect tooSQL Azure ve hello sunucuda [Pandas](http://pandas.pydata.org/) kitaplığı toodo hello örnekleme.</span><span class="sxs-lookup"><span data-stu-id="96ccc-106">hello Python sampling uses hello [pyodbc](https://code.google.com/p/pyodbc/) ODBC library tooconnect tooSQL Server on Azure and hello [Pandas](http://pandas.pydata.org/) library toodo hello sampling.</span></span>

> [!NOTE]
> <span data-ttu-id="96ccc-107">Bu belgedeki Hello örnek SQL kodunu Azure üzerinde bir SQL Server veri bulunduğu bu hello varsayar.</span><span class="sxs-lookup"><span data-stu-id="96ccc-107">hello sample SQL code in this document assumes that hello data is in a SQL Server on Azure.</span></span> <span data-ttu-id="96ccc-108">Lütfen değilse, çok bakın[Azure üzerinde veri tooSQL sunucu taşıma](machine-learning-data-science-move-sql-server-virtual-machine.md) konu hakkında yönergeler için toomove, veri tooSQL Azure sunucusunda.</span><span class="sxs-lookup"><span data-stu-id="96ccc-108">If it is not, please refer too[Move data tooSQL Server on Azure](machine-learning-data-science-move-sql-server-virtual-machine.md) topic for instructions on how toomove your data tooSQL Server on Azure.</span></span>
> 
> 

<span data-ttu-id="96ccc-109">Merhaba aşağıdaki **menü** açıklayan tootopics bağlantıları nasıl çeşitli depolama ortamları toosample verileri.</span><span class="sxs-lookup"><span data-stu-id="96ccc-109">hello following **menu** links tootopics that describe how toosample data from various storage environments.</span></span> 

[!INCLUDE [cap-sample-data-selector](../../includes/cap-sample-data-selector.md)]

<span data-ttu-id="96ccc-110">**Neden verilerinizi örnek?**</span><span class="sxs-lookup"><span data-stu-id="96ccc-110">**Why sample your data?**</span></span>
<span data-ttu-id="96ccc-111">Tooanalyze planladığınız hello veri kümesi, bu genellikle iyi bir fikir toodown örnek hello veri tooreduce büyükse, tooa daha küçük, ancak temsili ve daha kolay yönetilebilir boyutu.</span><span class="sxs-lookup"><span data-stu-id="96ccc-111">If hello dataset you plan tooanalyze is large, it's usually a good idea toodown-sample hello data tooreduce it tooa smaller but representative and more manageable size.</span></span> <span data-ttu-id="96ccc-112">Bu, veri anlama, keşfi ve özellik Mühendisliği kolaylaştırır.</span><span class="sxs-lookup"><span data-stu-id="96ccc-112">This facilitates data understanding, exploration, and feature engineering.</span></span> <span data-ttu-id="96ccc-113">Merhaba, rolde [takım veri bilimi işlem (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) tooenable hızlı prototipi oluşturulurken hello veri işleme işlevleri ve makine öğrenimi modellerinin oluşturulmasına olduğu.</span><span class="sxs-lookup"><span data-stu-id="96ccc-113">Its role in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) is tooenable fast prototyping of hello data processing functions and machine learning models.</span></span>

<span data-ttu-id="96ccc-114">Merhaba adımda bu örnekleme görevdir [takım veri bilimi işlem (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="96ccc-114">This sampling task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

## <span data-ttu-id="96ccc-115"><a name="SQL"></a>SQL kullanarak</span><span class="sxs-lookup"><span data-stu-id="96ccc-115"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="96ccc-116">Bu bölümde hello veritabanındaki SQL tooperform basit rastgele örnekleme hello veri karşı kullanarak çeşitli yöntemler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="96ccc-116">This section describes several methods using SQL tooperform simple random sampling against hello data in hello database.</span></span> <span data-ttu-id="96ccc-117">Lütfen, veri boyutu ve onun dağıtım dayalı bir yöntem seçin.</span><span class="sxs-lookup"><span data-stu-id="96ccc-117">Please choose a method based on your data size and its distribution.</span></span>

<span data-ttu-id="96ccc-118">Merhaba aşağıdaki iki öğeleri nasıl toouse NEWID SQL Server tooperform içinde hello örnekleme gösterir.</span><span class="sxs-lookup"><span data-stu-id="96ccc-118">hello two items below show how toouse newid in SQL Server tooperform hello sampling.</span></span> <span data-ttu-id="96ccc-119">Merhaba seçtiğiniz yöntemi nasıl rastgele hello örnek toobe istediğiniz bağlıdır (aşağıdaki hello örnek kodu pk_id toobe otomatik olarak oluşturulan bir birincil anahtar varsayılır).</span><span class="sxs-lookup"><span data-stu-id="96ccc-119">hello method you choose depends on how random you want hello sample toobe (pk_id in hello sample code below is assumed toobe an auto-generated primary key).</span></span>

1. <span data-ttu-id="96ccc-120">Daha az kesin rasgele örnek</span><span class="sxs-lookup"><span data-stu-id="96ccc-120">Less strict random sample</span></span>
   
        select  * from <table_name> where <primary_key> in 
        (select top 10 percent <primary_key> from <table_name> order by newid())
2. <span data-ttu-id="96ccc-121">Daha fazla rasgele örnek</span><span class="sxs-lookup"><span data-stu-id="96ccc-121">More random sample</span></span> 
   
        SELECT * FROM <table_name>
        WHERE 0.1 >= CAST(CHECKSUM(NEWID(), <primary_key>) & 0x7fffffff AS float)/ CAST (0x7fffffff AS int)

<span data-ttu-id="96ccc-122">Tablesample için örnekleme kullanılan yanı sıra aşağıda gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="96ccc-122">Tablesample can be used for sampling as well as demonstrated below.</span></span> <span data-ttu-id="96ccc-123">Bu daha iyi bir yaklaşım (sihirbazın farklı sayfalarında verileri değil bağıntılı varsayılarak), veri boyutu büyükse ve hello sorgu toocomplete için makul bir sürede olabilir.</span><span class="sxs-lookup"><span data-stu-id="96ccc-123">This may be a better approach if your data size is large (assuming that data on different pages is not correlated) and for hello query toocomplete in a reasonable time.</span></span>

    SELECT *
    FROM <table_name> 
    TABLESAMPLE (10 PERCENT)

> [!NOTE]
> <span data-ttu-id="96ccc-124">Keşfetmek ve yeni bir tabloda depolayarak örneklenen bu verilerden Özellikleri Oluştur</span><span class="sxs-lookup"><span data-stu-id="96ccc-124">You can explore and generate features from this sampled data by storing it in a new table</span></span>
> 
> 

### <span data-ttu-id="96ccc-125"><a name="sql-aml"></a>Machine Learning tooAzure bağlanma</span><span class="sxs-lookup"><span data-stu-id="96ccc-125"><a name="sql-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="96ccc-126">Hello Azure Machine Learning hello örnek sorgular yukarıda doğrudan kullanabilirsiniz [veri içeri aktarma] [ import-data] hello modülü toodown örnek hello verileri uçarak ve bir Azure Machine Learning deneme getirin.</span><span class="sxs-lookup"><span data-stu-id="96ccc-126">You can directly  use hello sample queries above in hello Azure Machine Learning [Import Data][import-data] module toodown-sample hello data on hello fly and bring it into an Azure Machine Learning experiment.</span></span> <span data-ttu-id="96ccc-127">Merhaba okuyucu modülü tooread hello örneklenen verileri kullanarak bir ekran görüntüsü aşağıda gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="96ccc-127">A screen shot of using hello reader module tooread hello sampled data is shown below:</span></span>

![Okuyucu sql][1]

## <span data-ttu-id="96ccc-129"><a name="python"></a>Merhaba Python programlama dilini kullanma</span><span class="sxs-lookup"><span data-stu-id="96ccc-129"><a name="python"></a>Using hello Python programming language</span></span>
<span data-ttu-id="96ccc-130">Bu bölüm hello kullanarak gösterir [pyodbc Kitaplığı](https://code.google.com/p/pyodbc/) tooestablish bir ODBC Python tooa SQL server veritabanına bağlan.</span><span class="sxs-lookup"><span data-stu-id="96ccc-130">This section demonstrates using hello [pyodbc library](https://code.google.com/p/pyodbc/) tooestablish an ODBC connect tooa SQL server database in Python.</span></span> <span data-ttu-id="96ccc-131">Merhaba veritabanı bağlantı dizesi şu şekildedir: (servername, dbname, kullanıcı adı ve parola yapılandırmanızı değiştirin):</span><span class="sxs-lookup"><span data-stu-id="96ccc-131">hello database connection string is as follows: (replace servername, dbname, username and password with your configuration):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="96ccc-132">Merhaba [Pandas](http://pandas.pydata.org/) Python kitaplıkta Python programlama için veri işleme için zengin bir veri yapılarını ve veri çözümleme araçları sağlar.</span><span class="sxs-lookup"><span data-stu-id="96ccc-132">hello [Pandas](http://pandas.pydata.org/) library in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="96ccc-133">Aşağıdaki Hello kodu hello veri % 0,1 örneğini Azure SQL veritabanındaki bir tablo Pandas verisine okur:</span><span class="sxs-lookup"><span data-stu-id="96ccc-133">hello code below reads a 0.1% sample of hello data from a table in Azure SQL database into a Pandas data :</span></span>

    import pandas as pd

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select column1, cloumn2... from <table_name> tablesample (0.1 percent)''', conn)

<span data-ttu-id="96ccc-134">Şimdi örneklenen hello veri hello Pandas veri çerçevesinde çalışabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96ccc-134">You can now work with hello sampled data in hello Pandas data frame.</span></span> 

### <span data-ttu-id="96ccc-135"><a name="python-aml"></a>Machine Learning tooAzure bağlanma</span><span class="sxs-lookup"><span data-stu-id="96ccc-135"><a name="python-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="96ccc-136">Aşağıdaki örnek kod toosave hello aşağı örneklenen verileri tooa dosyasına hello kullanın ve tooan Azure blob yükleyin.</span><span class="sxs-lookup"><span data-stu-id="96ccc-136">You can use hello following sample code toosave hello down-sampled data tooa file and upload it tooan Azure blob.</span></span> <span data-ttu-id="96ccc-137">Merhaba blob Hello verileri doğrudan okunabilir bir Azure Machine Learning deneme hello kullanarak [veri içeri aktarma] [ import-data] modülü.</span><span class="sxs-lookup"><span data-stu-id="96ccc-137">hello data in hello blob can be directly read into an Azure Machine Learning Experiment using hello [Import Data][import-data] module.</span></span> <span data-ttu-id="96ccc-138">Merhaba adımlar aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="96ccc-138">hello steps are as follows:</span></span> 

1. <span data-ttu-id="96ccc-139">Merhaba pandas veri çerçeve tooa yerel dosyasına yazma</span><span class="sxs-lookup"><span data-stu-id="96ccc-139">Write hello pandas data frame tooa local file</span></span>
   
        dataframe.to_csv(os.path.join(os.getcwd(),LOCALFILENAME), sep='\t', encoding='utf-8', index=False)
2. <span data-ttu-id="96ccc-140">Yerel dosya tooAzure blob karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="96ccc-140">Upload local file tooAzure blob</span></span>
   
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
3. <span data-ttu-id="96ccc-141">Azure Machine Learning kullanarak Azure blob üzerinden veri okuma [veri içeri aktarma] [ import-data] Merhaba ekranında Al aşağıda gösterildiği gibi Modülü:</span><span class="sxs-lookup"><span data-stu-id="96ccc-141">Read data from Azure blob using Azure Machine Learning [Import Data][import-data] module as shown in hello screen grab below:</span></span>

![Okuyucu blob][2]

## <a name="hello-team-data-science-process-in-action-example"></a><span data-ttu-id="96ccc-143">Eylem örnekte Hello takım veri bilimi işlemi</span><span class="sxs-lookup"><span data-stu-id="96ccc-143">hello Team Data Science Process in Action example</span></span>
<span data-ttu-id="96ccc-144">Bir ortak bir veri kümesini kullanarak hello takım veri bilimi işlemi bir uçtan uca kılavuz örneği için bkz [takım veri bilimi işlemi sürüyor: SQL sunucusu kullanarak](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="96ccc-144">For an end-to-end walkthrough example of hello Team Data Science Process a using a public dataset, see [Team Data Science Process in Action: using SQL Sever](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_database.png
[2]: ./media/machine-learning-data-science-sample-sql-server-virtual-machine/reader_blob.png

[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
