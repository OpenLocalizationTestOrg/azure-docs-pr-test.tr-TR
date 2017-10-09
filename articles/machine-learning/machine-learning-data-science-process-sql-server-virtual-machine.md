---
title: Azure SQL Server sanal makineye aaaExplore verileri | Microsoft Docs
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
ms.openlocfilehash: 67f4b058b0f6557ee15fd42795c918d68f1a9871
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="d4ad8-103"><a name="heading"></a>SQL Server sanal makinede Azure üzerinde işlem verileri</span><span class="sxs-lookup"><span data-stu-id="d4ad8-103"><a name="heading"></a>Process Data in SQL Server Virtual Machine on Azure</span></span>
<span data-ttu-id="d4ad8-104">Bu belgede ele alınmaktadır nasıl tooexplore veri ve Azure üzerinde bir SQL Server VM depolanan verilerin özelliklerini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-104">This document covers how tooexplore data and generate features for data stored in a SQL Server VM on Azure.</span></span> <span data-ttu-id="d4ad8-105">Bu SQL kullanarak veri wrangling veya Python gibi bir programlama dili kullanılarak yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-105">This can be done by data wrangling using SQL or by using a programming language like Python.</span></span>

> [!NOTE]
> <span data-ttu-id="d4ad8-106">Merhaba örnek SQL deyimleri bu belgedeki verileri SQL Server'da olduğunu varsayın.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-106">hello sample SQL statements in this document assume that data is in SQL Server.</span></span> <span data-ttu-id="d4ad8-107">Öyle değilse, toohello bulut veri bilimi işlem harita toolearn nasıl başvurmak toomove, veri tooSQL sunucu.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-107">If it isn't, refer toohello cloud data science process map toolearn how toomove your data tooSQL Server.</span></span>
> 
> 

## <span data-ttu-id="d4ad8-108"><a name="SQL"></a>SQL kullanarak</span><span class="sxs-lookup"><span data-stu-id="d4ad8-108"><a name="SQL"></a>Using SQL</span></span>
<span data-ttu-id="d4ad8-109">Biz veri wrangling görevleri SQL kullanarak bu bölümdeki aşağıdaki hello açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="d4ad8-109">We describe hello following data wrangling tasks in this section using SQL:</span></span>

1. [<span data-ttu-id="d4ad8-110">Veri keşfi</span><span class="sxs-lookup"><span data-stu-id="d4ad8-110">Data Exploration</span></span>](#sql-dataexploration)
2. [<span data-ttu-id="d4ad8-111">Özellik oluşturma</span><span class="sxs-lookup"><span data-stu-id="d4ad8-111">Feature Generation</span></span>](#sql-featuregen)

### <span data-ttu-id="d4ad8-112"><a name="sql-dataexploration"></a>Veri keşfi</span><span class="sxs-lookup"><span data-stu-id="d4ad8-112"><a name="sql-dataexploration"></a>Data Exploration</span></span>
<span data-ttu-id="d4ad8-113">Burada, SQL Server kullanılan tooexplore veri depolarında olabilecek birkaç örnek SQL komut dosyaları bulunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-113">Here are a few sample SQL scripts that can be used tooexplore data stores in SQL Server.</span></span>

> [!NOTE]
> <span data-ttu-id="d4ad8-114">Pratik bir örnek için hello kullanabilirsiniz [NYC ücreti dataset](http://www.andresmh.com/nyctaxitrips/) ve toohello başlıklı IPNB başvuruda [IPython not defteri ve SQL Server kullanarak NYC veri wrangling](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) bir uçtan uca gözden geçirme.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-114">For a practical example, you can use hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer toohello IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

1. <span data-ttu-id="d4ad8-115">Gün başına gözlemleri Hello sayısını alın</span><span class="sxs-lookup"><span data-stu-id="d4ad8-115">Get hello count of observations per day</span></span>
   
    `SELECT CONVERT(date, <date_columnname>) as date, count(*) as c from <tablename> group by CONVERT(date, <date_columnname>)` 
2. <span data-ttu-id="d4ad8-116">Merhaba düzeylerini kategorik sütunda Al</span><span class="sxs-lookup"><span data-stu-id="d4ad8-116">Get hello levels in a categorical column</span></span>
   
    `select  distinct <column_name> from <databasename>`
3. <span data-ttu-id="d4ad8-117">İki kategorik sütun arada Hello düzey sayısını Al</span><span class="sxs-lookup"><span data-stu-id="d4ad8-117">Get hello number of levels in combination of two categorical columns</span></span> 
   
    `select <column_a>, <column_b>,count(*) from <tablename> group by <column_a>, <column_b>`
4. <span data-ttu-id="d4ad8-118">Merhaba dağıtım sayısal sütunlar için alma</span><span class="sxs-lookup"><span data-stu-id="d4ad8-118">Get hello distribution for numerical columns</span></span>
   
    `select <column_name>, count(*) from <tablename> group by <column_name>`

### <span data-ttu-id="d4ad8-119"><a name="sql-featuregen"></a>Özellik oluşturma</span><span class="sxs-lookup"><span data-stu-id="d4ad8-119"><a name="sql-featuregen"></a>Feature Generation</span></span>
<span data-ttu-id="d4ad8-120">Bu bölümde, SQL kullanarak özellik oluşturmanın yolları açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="d4ad8-120">In this section, we describe ways of generating features using SQL:</span></span>  

1. [<span data-ttu-id="d4ad8-121">Özellik oluşturma sayısına dayalı</span><span class="sxs-lookup"><span data-stu-id="d4ad8-121">Count based Feature Generation</span></span>](#sql-countfeature)
2. [<span data-ttu-id="d4ad8-122">Binning özelliği oluşturma</span><span class="sxs-lookup"><span data-stu-id="d4ad8-122">Binning Feature Generation</span></span>](#sql-binningfeature)
3. [<span data-ttu-id="d4ad8-123">Tek bir sütundan Hello özellikleri alınıyor</span><span class="sxs-lookup"><span data-stu-id="d4ad8-123">Rolling out hello features from a single column</span></span>](#sql-featurerollout)

> [!NOTE]
> <span data-ttu-id="d4ad8-124">Ek özellikler oluşturmak sonra sütunları toohello var olan tablo olarak ekleyin veya hello ek özellikler ve hello özgün tabloyla katılabilir birincil anahtar, ile yeni bir tablo oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-124">Once you generate additional features, you can either add them as columns toohello existing table or create a new table with hello additional features and primary key, that can be joined with hello original table.</span></span> 
> 
> 

### <span data-ttu-id="d4ad8-125"><a name="sql-countfeature"></a>Özellik oluşturma sayısına dayalı</span><span class="sxs-lookup"><span data-stu-id="d4ad8-125"><a name="sql-countfeature"></a>Count based Feature Generation</span></span>
<span data-ttu-id="d4ad8-126">Merhaba Aşağıdaki örnekler sayısı özellikleri oluşturmanın iki yolu gösterir.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-126">hello following examples demonstrate two ways of generating count features.</span></span> <span data-ttu-id="d4ad8-127">'where' yan tümcesi hello ikinci yöntemi kullanır hello ve koşullu toplam Hello ilk yöntemi kullanır.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-127">hello first method uses conditional sum and hello second method uses hello 'where' clause.</span></span> <span data-ttu-id="d4ad8-128">Bunlar ardından özelliklerle hello özgün (birincil anahtar sütunlarını kullanarak) tablosu toohave sayısı hello özgün verilerin yanında katılabilir.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-128">These can then be joined with hello original table (using primary key columns) toohave count features alongside hello original data.</span></span>

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3> 

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename> 
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2> 

### <span data-ttu-id="d4ad8-129"><a name="sql-binningfeature"></a>Binning özelliği oluşturma</span><span class="sxs-lookup"><span data-stu-id="d4ad8-129"><a name="sql-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="d4ad8-130">Merhaba aşağıdaki örnekte nasıl toogenerate özellikleri (beş depo kullanarak) binning bir özellik olarak bunun yerine kullanılabilir sayısal bir sütun binned gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="d4ad8-130">hello following example shows how toogenerate binned features by binning (using five bins) a numerical column that can be used as a feature instead:</span></span>

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <span data-ttu-id="d4ad8-131"><a name="sql-featurerollout"></a>Tek bir sütundan Hello özellikleri alınıyor</span><span class="sxs-lookup"><span data-stu-id="d4ad8-131"><a name="sql-featurerollout"></a>Rolling out hello features from a single column</span></span>
<span data-ttu-id="d4ad8-132">Bu bölümde gösterilmektedir nasıl tooroll tablo toogenerate ek özellikler tek bir sütun çıkışı.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-132">In this section, we demonstrate how tooroll out a single column in a table toogenerate additional features.</span></span> <span data-ttu-id="d4ad8-133">Merhaba örneği toogenerate özellikleri çalıştığınız hello tabloda enlem veya boylam bir sütun olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-133">hello example assumes that there is a latitude or longitude column in hello table from which you are trying toogenerate features.</span></span>

<span data-ttu-id="d4ad8-134">Enlem/boylam konumu verileri kısa öncü İşte (stackoverflow kaynak var [nasıl toomeasure hello enlem ve boylam doğruluğunu?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)).</span><span class="sxs-lookup"><span data-stu-id="d4ad8-134">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow [How toomeasure hello accuracy of latitude and longitude?](http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude)).</span></span> <span data-ttu-id="d4ad8-135">Bu yararlı toounderstand featurizing hello konum alanı önce oluşur:</span><span class="sxs-lookup"><span data-stu-id="d4ad8-135">This is useful toounderstand before featurizing hello location field:</span></span>

* <span data-ttu-id="d4ad8-136">Merhaba oturum bize biz Kuzey veya Güney, Doğu veya Batı Merhaba dünya üzerindeki olup söyler.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-136">hello sign tells us whether we are north or south, east or west on hello globe.</span></span>
* <span data-ttu-id="d4ad8-137">Sıfır olmayan bir yüzlerce basamağın yuvarlanacağını belirtir bize boylam değil enlem kullanıyorsanız!</span><span class="sxs-lookup"><span data-stu-id="d4ad8-137">A nonzero hundreds digit tells us that we're using longitude, not latitude!</span></span>
* <span data-ttu-id="d4ad8-138">Merhaba onlarca basamaklı bir konum tooabout 1.000 kilometre sağlar.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-138">hello tens digit gives a position tooabout 1,000 kilometers.</span></span> <span data-ttu-id="d4ad8-139">Bize ne kıtada veya üzerinde duyuyoruz Okyanusu hakkında yararlı bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-139">It gives us useful information about what continent or ocean we are on.</span></span>
* <span data-ttu-id="d4ad8-140">Merhaba birimleri basamak (bir ondalık derece) bir konum yukarı too111 kilometre (60 Deniz mili, yaklaşık 69 mil) sağlar.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-140">hello units digit (one decimal degree) gives a position up too111 kilometers (60 nautical miles, about 69 miles).</span></span> <span data-ttu-id="d4ad8-141">Bu kabaca hangi büyük durumunun veya biz bulunan ülke bize.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-141">It can tell us roughly what large state or country we are in.</span></span>
* <span data-ttu-id="d4ad8-142">Merhaba ilk ondalık yerdir değerinde too11.1 km: komşu büyük Şehir'dan büyük bir şehir hello konumunu ayırt edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-142">hello first decimal place is worth up too11.1 km: it can distinguish hello position of one large city from a neighboring large city.</span></span>
* <span data-ttu-id="d4ad8-143">Merhaba ikinci ondalık yerdir değerinde too1.1 km: sonraki hello bir village ayırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-143">hello second decimal place is worth up too1.1 km: it can separate one village from hello next.</span></span>
* <span data-ttu-id="d4ad8-144">Merhaba üçüncü ondalık değer too110 m: büyük agricultural alan veya Kurumsal kampüs tanımlayabilirsiniz yerdir.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-144">hello third decimal place is worth up too110 m: it can identify a large agricultural field or institutional campus.</span></span>
* <span data-ttu-id="d4ad8-145">Merhaba dördüncü ondalık değer too11 m: kara paket tanımlayabilirsiniz yerdir.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-145">hello fourth decimal place is worth up too11 m: it can identify a parcel of land.</span></span> <span data-ttu-id="d4ad8-146">Bu girişim olmadığı düzeltilemeyen bir GPS birimle tipik doğruluğunu karşılaştırılabilir toohello olur.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-146">It is comparable toohello typical accuracy of an uncorrected GPS unit with no interference.</span></span>
* <span data-ttu-id="d4ad8-147">Merhaba beşinci ondalık değer too1.1 m: ağaçları birbirinden ayırt yerdir.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-147">hello fifth decimal place is worth up too1.1 m: it distinguishes trees from each other.</span></span> <span data-ttu-id="d4ad8-148">Doğruluk toothis düzeyi ticari GPS birimleri ile yalnızca ile fark düzeltme elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-148">Accuracy toothis level with commercial GPS units can only be achieved with differential correction.</span></span>
* <span data-ttu-id="d4ad8-149">Merhaba altıncı ondalık değer bu yapıları Windows'un, tasarlamak için ayrıntılı yerleştirmek için yollar oluşturma kullanabileceğiniz too0.11 m: yerdir.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-149">hello sixth decimal place is worth up too0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span></span> <span data-ttu-id="d4ad8-150">Glaciers ve rivers hareketlerini izlemek için birden çok iyi yeterli olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-150">It should be more than good enough for tracking movements of glaciers and rivers.</span></span> <span data-ttu-id="d4ad8-151">Bu differentially düzeltilmiş GPS gibi GPS ile painstaking ölçüleri gerçekleştirerek elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-151">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span></span>

<span data-ttu-id="d4ad8-152">Merhaba konum bilgileri featurized bölge, konum ve Şehir bilgilerini ayırma aşağıdaki gibi olabilir.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-152">hello location information can be featurized as follows, separating out region, location, and city information.</span></span> <span data-ttu-id="d4ad8-153">Bing Haritalar API'si adresinde gibi bir REST uç noktası da çağırabilirsiniz Not [noktası tarafından bir konum bulun](https://msdn.microsoft.com/library/ff701710.aspx) tooget hello bölge/bölge bilgileri.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-153">Note that you can also call a REST end point such as Bing Maps API available at [Find a Location by Point](https://msdn.microsoft.com/library/ff701710.aspx) tooget hello region/district information.</span></span>

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

<span data-ttu-id="d4ad8-154">Daha önce açıklandığı gibi bu konum temelli özellikler kullanılan toogenerate ek sayısı özellikleri daha fazla olabilir.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-154">These location-based features can be further used toogenerate additional count features as described earlier.</span></span> 

> [!TIP]
> <span data-ttu-id="d4ad8-155">Program aracılığıyla dilinizi tercih kullanarak hello kayıtları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-155">You can programmatically insert hello records using your language of choice.</span></span> <span data-ttu-id="d4ad8-156">Tooinsert hello veri öbekleri tooimprove yazma verimliliği gerekebilir (nasıl bir örnek için toodo bu pyodbc kullanarak, bkz: [A HelloWorld örnek tooaccess SQLServer python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)).</span><span class="sxs-lookup"><span data-stu-id="d4ad8-156">You may need tooinsert hello data in chunks tooimprove write efficiency (for an example of how toodo this using pyodbc, see [A HelloWorld sample tooaccess SQLServer with python](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python)).</span></span> <span data-ttu-id="d4ad8-157">Hello kullanarak hello veritabanındaki tooinsert verileri başka bir alternatiftir [BCP yardımcı programı](https://msdn.microsoft.com/library/ms162802.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4ad8-157">Another alternative is tooinsert data in hello database using hello [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx).</span></span>
> 
> 

### <span data-ttu-id="d4ad8-158"><a name="sql-aml"></a>Machine Learning tooAzure bağlanma</span><span class="sxs-lookup"><span data-stu-id="d4ad8-158"><a name="sql-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="d4ad8-159">Yeni oluşturulan hello özelliği sütun tooan var olan tablo olarak eklenebilir veya yeni bir tabloda depolanır ve machine learning için hello özgün tabloyla katılmış.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-159">hello newly generated feature can be added as a column tooan existing table or stored in a new table and joined with hello original table for machine learning.</span></span> <span data-ttu-id="d4ad8-160">Özellikler oluşturulan ya da zaten oluşturduysanız, hello kullanılarak erişilir [veri içeri aktarma] [ import-data] aşağıda gösterildiği gibi Azure Machine Learning modülünde:</span><span class="sxs-lookup"><span data-stu-id="d4ad8-160">Features can be generated or accessed if already created, using hello [Import Data][import-data] module in Azure Machine Learning as shown below:</span></span>

![azureml okuyucuları][1] 

## <span data-ttu-id="d4ad8-162"><a name="python"></a>Python gibi programlama dilini kullanma</span><span class="sxs-lookup"><span data-stu-id="d4ad8-162"><a name="python"></a>Using a programming language like Python</span></span>
<span data-ttu-id="d4ad8-163">Python tooexplore verileri kullanarak ve veri olan SQL Server'da hello açıklandığı gibi Python kullanarak Azure blob benzer tooprocessing veri olduğunda Özellikleri Oluştur [veri bilimi ortamınızdaki işlem Azure Blob veri](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="d4ad8-163">Using Python tooexplore data and generate features when hello data is in SQL Server is similar tooprocessing data in Azure blob using Python as documented in [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="d4ad8-164">Merhaba veri pandas veri çerçeveye hello veritabanından yüklenen toobe gerekir ve ardından daha fazla işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-164">hello data needs toobe loaded from hello database into a pandas data frame and then can be processed further.</span></span> <span data-ttu-id="d4ad8-165">Biz toohello veritabanına bağlanma ve bu bölümdeki hello veri çerçevesine hello verileri yüklenirken hello işleminde belge.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-165">We document hello process of connecting toohello database and loading hello data into hello data frame in this section.</span></span>

<span data-ttu-id="d4ad8-166">bağlantı dizesi biçimi aşağıdaki hello pyodbc (Değiştir servername, dbname, kullanıcı adı ve parola, belirli değerleri içeren) kullanarak Python kullanılan tooconnect tooa SQL Server veritabanından olabilir:</span><span class="sxs-lookup"><span data-stu-id="d4ad8-166">hello following connection string format can be used tooconnect tooa SQL Server database from Python using pyodbc (replace servername, dbname, username, and password with your specific values):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc    
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="d4ad8-167">Merhaba [Pandas Kitaplığı](http://pandas.pydata.org/) Python içinde Python programlama için veri işleme için zengin bir veri yapılarını ve veri çözümleme araçları sağlar.</span><span class="sxs-lookup"><span data-stu-id="d4ad8-167">hello [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="d4ad8-168">Aşağıdaki Hello kodu hello sonuçları bir SQL Server veritabanından Pandas veri çerçeveye döndürülen okur:</span><span class="sxs-lookup"><span data-stu-id="d4ad8-168">hello code below reads hello results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="d4ad8-169">Merhaba makalesinde anlatıldığı gibi hello Pandas veri çerçevesi ile çalışabilirsiniz artık [veri bilimi ortamınızdaki işlem Azure Blob veri](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="d4ad8-169">Now you can work with hello Pandas data frame as covered in hello article [Process Azure Blob data in your data science environment](machine-learning-data-science-process-data-blob.md).</span></span>

## <a name="azure-data-science-in-action-example"></a><span data-ttu-id="d4ad8-170">Azure veri bilimi eylem örnekte</span><span class="sxs-lookup"><span data-stu-id="d4ad8-170">Azure Data Science in Action Example</span></span>
<span data-ttu-id="d4ad8-171">Hello Azure veri bilimi ortak bir veri kümesini kullanarak işlem uçtan uca kılavuz örneği için bkz: [Azure veri bilimi eylem işleminde](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="d4ad8-171">For an end-to-end walkthrough example of hello Azure Data Science Process using a public dataset, see [Azure Data Science Process in Action](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

[1]: ./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/

