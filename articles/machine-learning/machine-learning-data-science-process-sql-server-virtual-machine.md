---
title: "Azure üzerinde bir SQL Server sanal makine keşfedin | Microsoft Docs"
description: "Verileri araştırmak ve özellikleri Azure üzerinde bir SQL Server sanal makine oluştur"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: 
ms.assetid: 3949fb2c-ffab-49fb-908d-27d5e42f743b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: fashah;garye;bradsev
ms.openlocfilehash: 16fabb29bdc8ec770efd843e18e9016e338a8f4e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <span data-ttu-id="8253b-103"><a name="heading"></a>SQL Server sanal makinede Azure üzerinde işlem verileri</span><span class="sxs-lookup"><span data-stu-id="8253b-103"><a name="heading"></a>Process Data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="8253b-104">Bu belge, verileri araştırmak ve Azure üzerinde bir SQL Server VM depolanan veri için özellikleri oluşturmak alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="8253b-104">This document covers how to explore data and generate features for data stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="8253b-105">Bu SQL kullanarak veri wrangling veya Python gibi bir programlama dili kullanılarak yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="8253b-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

> [!NOTE]
> <span data-ttu-id="8253b-106">Bu belgede örnek SQL deyimlerinde veri SQL Server'da olduğunu varsayın.</span><span class="sxs-lookup"><span data-stu-id="8253b-106">The sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="8253b-107">Öyle değilse, SQL Server'a verilerinizi taşıma hakkında bilgi edinmek için bulut veri bilimi işlem eşlemesi bakın.</span><span class="sxs-lookup"><span data-stu-id="8253b-107">If it isn't, refer to the cloud data science process map to learn how to move your data to SQL Server.</span></span>
> 
> 

## <span data-ttu-id="8253b-108"><a name="SQL"></a>SQL kullanarak</span><span class="sxs-lookup"><span data-stu-id="8253b-108"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="8253b-109">Biz SQL kullanarak bu bölümdeki aşağıdaki veri wrangling görevleri açıklar:</span><span class="sxs-lookup"><span data-stu-id="8253b-109">We describe the following data wrangling tasks in this section using SQL:</span></span>

1. [<span data-ttu-id="8253b-110">Veri keşfi</span><span class="sxs-lookup"><span data-stu-id="8253b-110">Data Exploration</span></span>](#sql-dataexploration)
2. [<span data-ttu-id="8253b-111">Özellik oluşturma</span><span class="sxs-lookup"><span data-stu-id="8253b-111">Feature Generation</span></span>](#sql-featuregen)

### <span data-ttu-id="8253b-112"><a name="sql-dataexploration"></a>Veri keşfi</span><span class="sxs-lookup"><span data-stu-id="8253b-112"><a name="sql-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="8253b-113">Burada, SQL Server veri depolarında keşfetmek için kullanılabilecek birkaç örnek SQL komut dosyaları bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="8253b-113">Here are a few sample SQL scripts that can be used to explore data stores in SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="8253b-114">Pratik bir örnek için kullandığınız [NYC ücreti dataset](http://www.andresmh.com/nyctaxitrips/) ve başlıklı IPNB başvuruda [IPython not defteri ve SQL Server kullanarak NYC veri wrangling](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) bir uçtan uca gözden geçirme.</span><span class="sxs-lookup"><span data-stu-id="8253b-114">For a practical example, you can use the [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer to the IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

1. <span data-ttu-id="8253b-115">Gün başına gözlemleri sayısını alın</span><span class="sxs-lookup"><span data-stu-id="8253b-115">Get the count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="8253b-116">Kategorik bir sütunda düzeylerini Al</span><span class="sxs-lookup"><span data-stu-id="8253b-116">Get the levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="8253b-117">İki kategorik sütun arada düzey sayısını Al</span><span class="sxs-lookup"><span data-stu-id="8253b-117">Get the number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="8253b-118">Sayısal sütunlar için dağıtım Al</span><span class="sxs-lookup"><span data-stu-id="8253b-118">Get the distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

### <span data-ttu-id="8253b-119"><a name="sql-featuregen"></a>Özellik oluşturma</span><span class="sxs-lookup"><span data-stu-id="8253b-119"><a name="sql-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="8253b-120">Bu bölümde, SQL kullanarak özellik oluşturmanın yolları açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="8253b-120">In this section, we describe ways of generating features using SQL:</span></span>  

1. [<span data-ttu-id="8253b-121">Özellik oluşturma sayısına dayalı</span><span class="sxs-lookup"><span data-stu-id="8253b-121">Count based Feature Generation</span></span>](#sql-countfeature)
2. [<span data-ttu-id="8253b-122">Binning özelliği oluşturma</span><span class="sxs-lookup"><span data-stu-id="8253b-122">Binning Feature Generation</span></span>](#sql-binningfeature)
3. [<span data-ttu-id="8253b-123">Tek bir sütundan özellikleri alınıyor</span><span class="sxs-lookup"><span data-stu-id="8253b-123">Rolling out the features from a single column</span></span>](#sql-featurerollout)

> [!NOTE]
> <span data-ttu-id="8253b-124">Ek özellikler oluşturmak sonra bunları varolan tablonun sütun olarak ekleyin veya özgün tabloyla katılabilir birincil anahtar ve ek özellikler ile yeni bir tablo oluşturun.</span><span class="sxs-lookup"><span data-stu-id="8253b-124">Once you generate additional features, you can either add them as columns to the existing table or create a new table with the additional features and primary key, that can be joined with the original table.</span></span> 
> 
> 

### <span data-ttu-id="8253b-125"><a name="sql-countfeature"></a>Özellik oluşturma sayısına dayalı</span><span class="sxs-lookup"><span data-stu-id="8253b-125"><a name="sql-countfeature"></a>Count based Feature Generation</span></span>
<span data-ttu-id="8253b-126">Aşağıdaki örnekler sayısı özellikleri oluşturmanın iki yolu gösterir.</span><span class="sxs-lookup"><span data-stu-id="8253b-126">The following examples demonstrate two ways of generating count features.</span></span> <span data-ttu-id="8253b-127">İlk yöntem Koşullu Toplama ve ikinci yöntem 'where' yan tümcesi kullanır.</span><span class="sxs-lookup"><span data-stu-id="8253b-127">The first method uses conditional sum and the second method uses the 'where' clause.</span></span> <span data-ttu-id="8253b-128">Bunlar ardından (birincil anahtar sütunlarını kullanarak) özgün tabloyla özgün verilerin yanı sıra sayısı özelliğiniz katılabilir.</span><span class="sxs-lookup"><span data-stu-id="8253b-128">These can then be joined with the original table (using primary key columns) to have count features alongside the original data.</span></span>

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3> 

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename> 
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2> 

### <span data-ttu-id="8253b-129"><a name="sql-binningfeature"></a>Binning özelliği oluşturma</span><span class="sxs-lookup"><span data-stu-id="8253b-129"><a name="sql-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="8253b-130">Aşağıdaki örnek, bir özellik olarak bunun yerine kullanılabilir sayısal bir sütun (beş depo kullanarak) binning binned özellikleri oluşturmak nasıl gösterir:</span><span class="sxs-lookup"><span data-stu-id="8253b-130">The following example shows how to generate binned features by binning (using five bins) a numerical column that can be used as a feature instead:</span></span>

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <span data-ttu-id="8253b-131"><a name="sql-featurerollout"></a>Tek bir sütundan özellikleri alınıyor</span><span class="sxs-lookup"><span data-stu-id="8253b-131"><a name="sql-featurerollout"></a>Rolling out the features from a single column</span></span>
<span data-ttu-id="8253b-132">Bu bölümde nasıl ek özellikler oluşturmak için bir tablo tek bir sütunda çıkışı alınacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="8253b-132">In this section, we demonstrate how to roll out a single column in a table to generate additional features.</span></span> <span data-ttu-id="8253b-133">Örnek özellikleri Oluştur çalıştığınız tabloda enlem veya boylam bir sütun olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="8253b-133">The example assumes that there is a latitude or longitude column in the table from which you are trying to generate features.</span></span>

<span data-ttu-id="8253b-134">Enlem/boylam konumu verileri kısa öncü İşte (stackoverflow kaynak var [enlem ve boylam doğruluğunu ölçme?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)).</span><span class="sxs-lookup"><span data-stu-id="8253b-134">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow [How to measure the accuracy of latitude and longitude?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)).</span></span> <span data-ttu-id="8253b-135">Bu konum alanı önce featurizing anlamak kullanışlıdır:</span><span class="sxs-lookup"><span data-stu-id="8253b-135">This is useful to understand before featurizing the location field:</span></span>

* <span data-ttu-id="8253b-136">Oturum açma bize olup olmadığını biz Kuzey Güney, Doğu ya veya Batı üzerinde dünya söyler.</span><span class="sxs-lookup"><span data-stu-id="8253b-136">The sign tells us whether we are north or south, east or west on the globe.</span></span>
* <span data-ttu-id="8253b-137">Sıfır olmayan bir yüzlerce basamağın yuvarlanacağını belirtir bize boylam değil enlem kullanıyorsanız!</span><span class="sxs-lookup"><span data-stu-id="8253b-137">A nonzero hundreds digit tells us that we're using longitude, not latitude!</span></span>
* <span data-ttu-id="8253b-138">On basamak yaklaşık 1.000 kilometre için bir konum sağlar.</span><span class="sxs-lookup"><span data-stu-id="8253b-138">The tens digit gives a position to about 1,000 kilometers.</span></span> <span data-ttu-id="8253b-139">Bize ne kıtada veya üzerinde duyuyoruz Okyanusu hakkında yararlı bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="8253b-139">It gives us useful information about what continent or ocean we are on.</span></span>
* <span data-ttu-id="8253b-140">Birimleri basamak (bir ondalık derece) 111 kilometre (60 Deniz mili, yaklaşık 69 mil) bir konum sağlar.</span><span class="sxs-lookup"><span data-stu-id="8253b-140">The units digit (one decimal degree) gives a position up to 111 kilometers (60 nautical miles, about 69 miles).</span></span> <span data-ttu-id="8253b-141">Bu kabaca hangi büyük durumunun veya biz bulunan ülke bize.</span><span class="sxs-lookup"><span data-stu-id="8253b-141">It can tell us roughly what large state or country we are in.</span></span>
* <span data-ttu-id="8253b-142">En fazla 11.1 km ilk ondalık yerdir: komşu büyük Şehir'dan büyük bir şehir konumunu ayırt edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8253b-142">The first decimal place is worth up to 11.1 km: it can distinguish the position of one large city from a neighboring large city.</span></span>
* <span data-ttu-id="8253b-143">İkinci ondalık en fazla 1.1 km yerdir: sonraki bir village ayırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8253b-143">The second decimal place is worth up to 1.1 km: it can separate one village from the next.</span></span>
* <span data-ttu-id="8253b-144">Üçüncü ondalık en fazla 110 m: büyük agricultural alan veya Kurumsal kampüs tanımlayabilirsiniz yerdir.</span><span class="sxs-lookup"><span data-stu-id="8253b-144">The third decimal place is worth up to 110 m: it can identify a large agricultural field or institutional campus.</span></span>
* <span data-ttu-id="8253b-145">Dördüncü ondalık 11 m: kara paket tanımlayabilirsiniz yerdir.</span><span class="sxs-lookup"><span data-stu-id="8253b-145">The fourth decimal place is worth up to 11 m: it can identify a parcel of land.</span></span> <span data-ttu-id="8253b-146">Hiçbir girişim ile karşılaştırılabilir bir düzeltilemeyen GPS birimi tipik doğruluğu için.</span><span class="sxs-lookup"><span data-stu-id="8253b-146">It is comparable to the typical accuracy of an uncorrected GPS unit with no interference.</span></span>
* <span data-ttu-id="8253b-147">Beşinci ondalık en fazla 1.1 m: ağaçları birbirinden ayırt yerdir.</span><span class="sxs-lookup"><span data-stu-id="8253b-147">The fifth decimal place is worth up to 1.1 m: it distinguishes trees from each other.</span></span> <span data-ttu-id="8253b-148">Bu düzey ticari GPS birimleri ile doğruluğu yalnızca fark düzeltmeyle elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="8253b-148">Accuracy to this level with commercial GPS units can only be achieved with differential correction.</span></span>
* <span data-ttu-id="8253b-149">Altıncı ondalık en fazla 0.11 m: Bu yapıları Windows'un, tasarlamak için ayrıntılı yerleştirmek için yollar oluşturma kullanabilirsiniz yerdir.</span><span class="sxs-lookup"><span data-stu-id="8253b-149">The sixth decimal place is worth up to 0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span></span> <span data-ttu-id="8253b-150">Glaciers ve rivers hareketlerini izlemek için birden çok iyi yeterli olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="8253b-150">It should be more than good enough for tracking movements of glaciers and rivers.</span></span> <span data-ttu-id="8253b-151">Bu differentially düzeltilmiş GPS gibi GPS ile painstaking ölçüleri gerçekleştirerek elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="8253b-151">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span></span>

<span data-ttu-id="8253b-152">Konum bilgileri featurized bölge, konum ve Şehir bilgilerini ayırma aşağıdaki gibi olabilir.</span><span class="sxs-lookup"><span data-stu-id="8253b-152">The location information can be featurized as follows, separating out region, location, and city information.</span></span> <span data-ttu-id="8253b-153">Bing Haritalar API'si adresinde gibi bir REST uç noktası da çağırabilirsiniz Not [noktası tarafından bir konum bulun](https://msdn.microsoft.com/library/ff701710.aspx) bölge/bölge bilgileri alınacak.</span><span class="sxs-lookup"><span data-stu-id="8253b-153">Note that you can also call a REST end point such as Bing Maps API available at [Find a Location by Point](https://msdn.microsoft.com/library/ff701710.aspx) to get the region/district information.</span></span>

    select 
        <location_columnname>
        ,round(<location_columnname>,0) as l1        
        ,l2=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 1 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),1,1) else '0' end     
        ,l3=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 2 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),2,1) else '0' end     
        ,l4=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 3 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),3,1) else '0' end     
        ,l5=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 4 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),4,1) else '0' end     
        ,l6=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 5 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),5,1) else '0' end     
        ,l7=case when LEN (PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1)) >= 6 then substring(PARSENAME(round(ABS(<location_columnname>) - FLOOR(ABS(<location_columnname>)),6),1),6,1) else '0' end     
    from <tablename>

<span data-ttu-id="8253b-154">Bu konum temelli özellikleri, daha önce açıklandığı gibi ek sayısı özellikleri oluşturmak için daha fazla kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8253b-154">These location-based features can be further used to generate additional count features as described earlier.</span></span> 

> [!TIP]
> <span data-ttu-id="8253b-155">Program aracılığıyla dilinizi tercih kullanarak kayıtları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8253b-155">You can programmatically insert the records using your language of choice.</span></span> <span data-ttu-id="8253b-156">Veri yazma verimliliğini artırmak için yığınlar halinde eklemek gerekebilir (pyodbc kullanarak bunu nasıl bir örnek için bkz: [SQLServer python ile erişmek için A HelloWorld örnek](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)).</span><span class="sxs-lookup"><span data-stu-id="8253b-156">You may need to insert the data in chunks to improve write efficiency (for an example of how to do this using pyodbc, see [A HelloWorld sample to access SQLServer with python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)).</span></span> <span data-ttu-id="8253b-157">Verileri kullanarak veritabanı eklemek için başka bir alternatiftir [BCP yardımcı programı](https://msdn.microsoft.com/library/ms162802.aspx).</span><span class="sxs-lookup"><span data-stu-id="8253b-157">Another alternative is to insert data in the database using the [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx).</span></span>
> 
> 

### <span data-ttu-id="8253b-158"><a name="sql-aml"></a>Azure Machine Learning ile bağlanma</span><span class="sxs-lookup"><span data-stu-id="8253b-158"><a name="sql-aml"></a>Connecting to Azure Machine Learning</span></span>
<span data-ttu-id="8253b-159">Yeni oluşturulan özellik bir sütun olarak var olan bir tabloya eklenebilir veya yeni bir tabloda depolanır ve machine learning için özgün tabloyla katılmış.</span><span class="sxs-lookup"><span data-stu-id="8253b-159">The newly generated feature can be added as a column to an existing table or stored in a new table and joined with the original table for machine learning.</span></span> <span data-ttu-id="8253b-160">Özellikler oluşturulan ya da zaten oluşturduysanız, kullanılarak erişilir [veri içeri aktarma] [ import-data] aşağıda gösterildiği gibi Azure Machine Learning modülünde:</span><span class="sxs-lookup"><span data-stu-id="8253b-160">Features can be generated or accessed if already created, using the [Import Data][import-data] module in Azure Machine Learning as shown below:</span></span>

![azureml okuyucuları][1] 

## <span data-ttu-id="8253b-162"><a name="python"></a>Python gibi programlama dilini kullanma</span><span class="sxs-lookup"><span data-stu-id="8253b-162"><a name="python"></a>Using a programming language like Python</span></span>
<span data-ttu-id="8253b-163">Verileri araştırmak ve verileri SQL Server olduğunda özellikleri oluşturmak için Python kullanarak benzer açıklandığı gibi Python kullanarak Azure blob veri işleme için [veri bilimi ortamınızdaki işlem Azure Blob veri](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="8253b-163">Using Python to explore data and generate features when the data is in SQL Server is similar to processing data in Azure blob using Python as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="8253b-164">Veriler veritabanından pandas veri çerçeveye yüklenmesi gerektiğini ve ardından daha fazla işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="8253b-164">The data needs to be loaded from the database into a pandas data frame and then can be processed further.</span></span> <span data-ttu-id="8253b-165">Biz, veritabanına bağlanmak ve bu bölümdeki verileri çerçevesine veri yükleme işleminde belge.</span><span class="sxs-lookup"><span data-stu-id="8253b-165">We document the process of connecting to the database and loading the data into the data frame in this section.</span></span>

<span data-ttu-id="8253b-166">Aşağıdaki bağlantı dizesi biçimi Python pyodbc (Değiştir servername, dbname, kullanıcı adı ve parola, belirli değerleri içeren) kullanarak bir SQL Server veritabanına bağlanmak için kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="8253b-166">The following connection string format can be used to connect to a SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up the SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="8253b-167">[Pandas Kitaplığı](http://pandas.pydata.org/) Python içinde Python programlama için veri işleme için zengin bir veri yapılarını ve veri çözümleme araçları sağlar.</span><span class="sxs-lookup"><span data-stu-id="8253b-167">The [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="8253b-168">Aşağıdaki kod, bir SQL Server veritabanından Pandas veri çerçeveye sonuçları döndüren okur:</span><span class="sxs-lookup"><span data-stu-id="8253b-168">The code below reads the results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load the returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="8253b-169">Makalede ele alınan olarak Pandas veri çerçevesi ile çalışabilir artık [veri bilimi ortamınızdaki işlem Azure Blob veri](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="8253b-169">Now you can work with the Pandas data frame as covered in the article [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="azure-data-science-in-action-example"></a><span data-ttu-id="8253b-170">Azure veri bilimi eylem örnekte</span><span class="sxs-lookup"><span data-stu-id="8253b-170">Azure Data Science in Action Example</span></span>
<span data-ttu-id="8253b-171">Azure veri bilimi ortak bir veri kümesini kullanarak işlem uçtan uca kılavuz örneği için bkz: [Azure veri bilimi eylem işleminde](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="8253b-171">For an end-to-end walkthrough example of the Azure Data Science Process using a public dataset, see [Azure Data Science Process in Action](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

