---
title: "SQL ve Python kullanarak SQL Server verileri için aaaCreate özellikleri | Microsoft Docs"
description: "SQL Azure işlem verileri"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: 
ms.assetid: bf1f4a6c-7711-4456-beb7-35fdccd46a44
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;fashah;garye
ms.openlocfilehash: 223352edb0377a159333e7528ad03c43902e6f45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-features-for-data-in-sql-server-using-sql-and-python"></a><span data-ttu-id="a9897-103">SQL ve Python kullanarak SQL Server’daki verilerin özelliklerini oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9897-103">Create features for data in SQL Server using SQL and Python</span></span>
<span data-ttu-id="a9897-104">Bu belge nasıl toogenerate özellikleri algoritmaları Yardım Azure üzerinde bir SQL Server VM depolanan veriler için hello verileri daha verimli bir şekilde bilgi gösterir.</span><span class="sxs-lookup"><span data-stu-id="a9897-104">This document shows how toogenerate features for data stored in a SQL Server VM on Azure that help algorithms learn more efficiently from hello data.</span></span> <span data-ttu-id="a9897-105">Bu SQL kullanarak veya Python, her ikisi de aşağıda gösterildiği gibi bir programlama dili kullanılarak yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="a9897-105">This can be done by using SQL or by using a programming language like Python, both of which are demonstrated here.</span></span>

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="a9897-106">Bu **menü** nasıl toocreate çeşitli ortamlarda veri özellikleri açıklamak tootopics bağlar.</span><span class="sxs-lookup"><span data-stu-id="a9897-106">This **menu** links tootopics that describe how toocreate features for data in various environments.</span></span> <span data-ttu-id="a9897-107">Bu görev bir hello adımdır [takım veri bilimi işlem (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span><span class="sxs-lookup"><span data-stu-id="a9897-107">This task is a step in hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

> [!NOTE]
> <span data-ttu-id="a9897-108">Pratik bir örnek için hello başvurabilirsiniz [NYC ücreti dataset](http://www.andresmh.com/nyctaxitrips/) ve toohello başlıklı IPNB başvuruda [IPython not defteri ve SQL Server kullanarak NYC veri wrangling](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) bir uçtan uca gözden geçirme.</span><span class="sxs-lookup"><span data-stu-id="a9897-108">For a practical example, you can consult hello [NYC Taxi dataset](http://www.andresmh.com/nyctaxitrips/) and refer toohello IPNB titled [NYC Data wrangling using IPython Notebook and SQL Server](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-sql-walkthrough.ipynb) for an end-to-end walk-through.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="a9897-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a9897-109">Prerequisites</span></span>
<span data-ttu-id="a9897-110">Bu makalede, sahip olduğunuz varsayılmaktadır:</span><span class="sxs-lookup"><span data-stu-id="a9897-110">This article assumes that you have:</span></span>

* <span data-ttu-id="a9897-111">Bir Azure depolama hesabı oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="a9897-111">Created an Azure storage account.</span></span> <span data-ttu-id="a9897-112">Yönergeler gerekiyorsa bkz [bir Azure depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="a9897-112">If you need instructions, see [Create an Azure Storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account)</span></span>
* <span data-ttu-id="a9897-113">Verilerinizi SQL Server içinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="a9897-113">Stored your data in SQL Server.</span></span> <span data-ttu-id="a9897-114">Yüklemediyseniz, bkz: [Azure Machine Learning için verileri tooan Azure SQL veritabanı taşıma](machine-learning-data-science-move-sql-azure.md) nasıl toomove hello var. veri hakkında yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="a9897-114">If you have not, see [Move data tooan Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md) for instructions on how toomove hello data there.</span></span>

## <span data-ttu-id="a9897-115"><a name="sql-featuregen"></a>SQL ile özelliği oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9897-115"><a name="sql-featuregen"></a>Feature Generation with SQL</span></span>
<span data-ttu-id="a9897-116">Bu bölümde, SQL kullanarak özellik oluşturmanın yolları açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="a9897-116">In this section, we describe ways of generating features using SQL:</span></span>  

1. [<span data-ttu-id="a9897-117">Özellik oluşturma sayısına dayalı</span><span class="sxs-lookup"><span data-stu-id="a9897-117">Count based Feature Generation</span></span>](#sql-countfeature)
2. [<span data-ttu-id="a9897-118">Binning özelliği oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9897-118">Binning Feature Generation</span></span>](#sql-binningfeature)
3. [<span data-ttu-id="a9897-119">Tek bir sütundan Hello özellikleri alınıyor</span><span class="sxs-lookup"><span data-stu-id="a9897-119">Rolling out hello features from a single column</span></span>](#sql-featurerollout)

> [!NOTE]
> <span data-ttu-id="a9897-120">Ek özellikler oluşturmak sonra sütunları toohello var olan tablo olarak ekleyin veya hello ek özellikler ve hello özgün tabloyla katılabilir birincil anahtar, ile yeni bir tablo oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a9897-120">Once you generate additional features, you can either add them as columns toohello existing table or create a new table with hello additional features and primary key, that can be joined with hello original table.</span></span>
> 
> 

### <span data-ttu-id="a9897-121"><a name="sql-countfeature"></a>Özellik oluşturma sayısına dayalı</span><span class="sxs-lookup"><span data-stu-id="a9897-121"><a name="sql-countfeature"></a>Count based Feature Generation</span></span>
<span data-ttu-id="a9897-122">Bu belge sayısı özellikleri oluşturmanın iki yolu gösterir.</span><span class="sxs-lookup"><span data-stu-id="a9897-122">This document demonstrates two ways of generating count features.</span></span> <span data-ttu-id="a9897-123">'where' yan tümcesi hello ikinci yöntemi kullanır hello ve koşullu toplam Hello ilk yöntemi kullanır.</span><span class="sxs-lookup"><span data-stu-id="a9897-123">hello first method uses conditional sum and hello second method uses hello 'where\` clause.</span></span> <span data-ttu-id="a9897-124">Bunlar ardından özelliklerle hello özgün (birincil anahtar sütunlarını kullanarak) tablosu toohave sayısı hello özgün verilerin yanında katılabilir.</span><span class="sxs-lookup"><span data-stu-id="a9897-124">These can then be joined with hello original table (using primary key columns) toohave count features alongside hello original data.</span></span>

    select <column_name1>,<column_name2>,<column_name3>, COUNT(*) as Count_Features from <tablename> group by <column_name1>,<column_name2>,<column_name3>

    select <column_name1>,<column_name2> , sum(1) as Count_Features from <tablename>
    where <column_name3> = '<some_value>' group by <column_name1>,<column_name2>

### <span data-ttu-id="a9897-125"><a name="sql-binningfeature"></a>Binning özelliği oluşturma</span><span class="sxs-lookup"><span data-stu-id="a9897-125"><a name="sql-binningfeature"></a>Binning Feature Generation</span></span>
<span data-ttu-id="a9897-126">Merhaba aşağıdaki örnekte nasıl toogenerate özellikleri (5 depo kullanarak) binning bir özellik olarak bunun yerine kullanılabilir sayısal bir sütun binned gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="a9897-126">hello following example shows how toogenerate binned features by binning (using 5 bins) a numerical column that can be used as a feature instead:</span></span>

    `SELECT <column_name>, NTILE(5) OVER (ORDER BY <column_name>) AS BinNumber from <tablename>`


### <span data-ttu-id="a9897-127"><a name="sql-featurerollout"></a>Tek bir sütundan Hello özellikleri alınıyor</span><span class="sxs-lookup"><span data-stu-id="a9897-127"><a name="sql-featurerollout"></a>Rolling out hello features from a single column</span></span>
<span data-ttu-id="a9897-128">Bu bölümde tooroll kullanıma tek bir sütun tablo toogenerate ek özellikler gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a9897-128">In this section, we demonstrate how tooroll-out a single column in a table toogenerate additional features.</span></span> <span data-ttu-id="a9897-129">Merhaba örneği toogenerate özellikleri çalıştığınız hello tabloda enlem veya boylam bir sütun olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="a9897-129">hello example assumes that there is a latitude or longitude column in hello table from which you are trying toogenerate features.</span></span>

<span data-ttu-id="a9897-130">Enlem/boylam konumu verileri kısa öncü İşte (stackoverflow kaynak var `http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude`).</span><span class="sxs-lookup"><span data-stu-id="a9897-130">Here is a brief primer on latitude/longitude location data (resourced from stackoverflow `http://gis.stackexchange.com/questions/8650/how-to-measure-the-accuracy-of-latitude-and-longitude`).</span></span> <span data-ttu-id="a9897-131">Bu yararlı toounderstand featurizing hello konum alanı önce oluşur:</span><span class="sxs-lookup"><span data-stu-id="a9897-131">This is useful toounderstand before featurizing hello location field:</span></span>

* <span data-ttu-id="a9897-132">Merhaba oturum bize biz Kuzey veya Güney, Doğu veya Batı Merhaba dünya üzerindeki olup söyler.</span><span class="sxs-lookup"><span data-stu-id="a9897-132">hello sign tells us whether we are north or south, east or west on hello globe.</span></span>
* <span data-ttu-id="a9897-133">Sıfır olmayan bir yüzlerce basamağın yuvarlanacağını belirtir bize biz boylam değil enlem kullanmakta olduğunuz!</span><span class="sxs-lookup"><span data-stu-id="a9897-133">A nonzero hundreds digit tells us we're using longitude, not latitude!</span></span>
* <span data-ttu-id="a9897-134">Merhaba onlarca basamaklı bir konum tooabout 1.000 kilometre sağlar.</span><span class="sxs-lookup"><span data-stu-id="a9897-134">hello tens digit gives a position tooabout 1,000 kilometers.</span></span> <span data-ttu-id="a9897-135">Bize ne kıtada veya üzerinde duyuyoruz Okyanusu hakkında yararlı bilgiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="a9897-135">It gives us useful information about what continent or ocean we are on.</span></span>
* <span data-ttu-id="a9897-136">Merhaba birimleri basamak (bir ondalık derece) bir konum yukarı too111 kilometre (60 Deniz mili, yaklaşık 69 mil) sağlar.</span><span class="sxs-lookup"><span data-stu-id="a9897-136">hello units digit (one decimal degree) gives a position up too111 kilometers (60 nautical miles, about 69 miles).</span></span> <span data-ttu-id="a9897-137">Bu kabaca hangi büyük durumunun veya biz bulunan ülke bize.</span><span class="sxs-lookup"><span data-stu-id="a9897-137">It can tell us roughly what large state or country we are in.</span></span>
* <span data-ttu-id="a9897-138">Merhaba ilk ondalık yerdir değerinde too11.1 km: komşu büyük Şehir'dan büyük bir şehir hello konumunu ayırt edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9897-138">hello first decimal place is worth up too11.1 km: it can distinguish hello position of one large city from a neighboring large city.</span></span>
* <span data-ttu-id="a9897-139">Merhaba ikinci ondalık yerdir değerinde too1.1 km: sonraki hello bir village ayırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9897-139">hello second decimal place is worth up too1.1 km: it can separate one village from hello next.</span></span>
* <span data-ttu-id="a9897-140">Merhaba üçüncü ondalık değer too110 m: büyük agricultural alan veya Kurumsal kampüs tanımlayabilirsiniz yerdir.</span><span class="sxs-lookup"><span data-stu-id="a9897-140">hello third decimal place is worth up too110 m: it can identify a large agricultural field or institutional campus.</span></span>
* <span data-ttu-id="a9897-141">Merhaba dördüncü ondalık değer too11 m: kara paket tanımlayabilirsiniz yerdir.</span><span class="sxs-lookup"><span data-stu-id="a9897-141">hello fourth decimal place is worth up too11 m: it can identify a parcel of land.</span></span> <span data-ttu-id="a9897-142">Bu girişim olmadığı düzeltilemeyen bir GPS birimle tipik doğruluğunu karşılaştırılabilir toohello olur.</span><span class="sxs-lookup"><span data-stu-id="a9897-142">It is comparable toohello typical accuracy of an uncorrected GPS unit with no interference.</span></span>
* <span data-ttu-id="a9897-143">Merhaba beşinci ondalık basamak değerinde too1.1 m: olduğu ağaçlar birbirinden ayırt etmek.</span><span class="sxs-lookup"><span data-stu-id="a9897-143">hello fifth decimal place is worth up too1.1 m: it distinguish trees from each other.</span></span> <span data-ttu-id="a9897-144">Doğruluk toothis düzeyi ticari GPS birimleri ile yalnızca ile fark düzeltme elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="a9897-144">Accuracy toothis level with commercial GPS units can only be achieved with differential correction.</span></span>
* <span data-ttu-id="a9897-145">Merhaba altıncı ondalık değer bu yapıları Windows'un, tasarlamak için ayrıntılı yerleştirmek için yollar oluşturma kullanabileceğiniz too0.11 m: yerdir.</span><span class="sxs-lookup"><span data-stu-id="a9897-145">hello sixth decimal place is worth up too0.11 m: you can use this for laying out structures in detail, for designing landscapes, building roads.</span></span> <span data-ttu-id="a9897-146">Glaciers ve rivers hareketlerini izlemek için birden çok iyi yeterli olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a9897-146">It should be more than good enough for tracking movements of glaciers and rivers.</span></span> <span data-ttu-id="a9897-147">Bu differentially düzeltilmiş GPS gibi GPS ile painstaking ölçüleri gerçekleştirerek elde edilebilir.</span><span class="sxs-lookup"><span data-stu-id="a9897-147">This can be achieved by taking painstaking measures with GPS, such as differentially corrected GPS.</span></span>

<span data-ttu-id="a9897-148">Merhaba konum bilgileri featurized gibi bölge, konum ve Şehir bilgilerini ayırma olabilir.</span><span class="sxs-lookup"><span data-stu-id="a9897-148">hello location information can can be featurized as follows, separating out region, location and city information.</span></span> <span data-ttu-id="a9897-149">Bir kez Bing Haritalar API'si adresinde gibi bir REST uç noktası da çağırabilir Not `https://msdn.microsoft.com/library/ff701710.aspx` tooget hello bölge/bölge bilgileri.</span><span class="sxs-lookup"><span data-stu-id="a9897-149">Note that once can also call a REST end point such as Bing Maps API available at `https://msdn.microsoft.com/library/ff701710.aspx` tooget hello region/district information.</span></span>

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

<span data-ttu-id="a9897-150">temel özellikler daha fazla kullanılabilir konum yukarıda Hello toogenerate ek sayısı özellikleri daha önce açıklandığı gibi kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a9897-150">hello above location based features can be further used toogenerate additional count features as described earlier.</span></span>

> [!TIP]
> <span data-ttu-id="a9897-151">Program aracılığıyla dilinizi tercih kullanarak hello kayıtları ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9897-151">You can programmatically insert hello records using your language of choice.</span></span> <span data-ttu-id="a9897-152">Tooinsert hello veri öbekleri tooimprove yazma verimliliği gerekebilir [nasıl hello örnek denetleyin toodo bu pyodbc burada kullanarak](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python).</span><span class="sxs-lookup"><span data-stu-id="a9897-152">You may need tooinsert hello data in chunks tooimprove write efficiency [Check out hello example of how toodo this using pyodbc here](https://code.google.com/p/pypyodbc/wiki/A_HelloWorld_sample_to_access_mssql_with_python).</span></span>
> <span data-ttu-id="a9897-153">Başka bir alternatif veritabanı hello kullanarak tooinsert verilerdir [BCP yardımcı programı](https://msdn.microsoft.com/library/ms162802.aspx)</span><span class="sxs-lookup"><span data-stu-id="a9897-153">Another alternative is tooinsert data in hello database using [BCP utility](https://msdn.microsoft.com/library/ms162802.aspx)</span></span>
> 
> 

### <span data-ttu-id="a9897-154"><a name="sql-aml"></a>Machine Learning tooAzure bağlanma</span><span class="sxs-lookup"><span data-stu-id="a9897-154"><a name="sql-aml"></a>Connecting tooAzure Machine Learning</span></span>
<span data-ttu-id="a9897-155">Yeni oluşturulan hello özelliği sütun tooan var olan tablo olarak eklenebilir veya yeni bir tabloda depolanır ve machine learning için hello özgün tabloyla katılmış.</span><span class="sxs-lookup"><span data-stu-id="a9897-155">hello newly generated feature can be added as a column tooan existing table or stored in a new table and joined with hello original table for machine learning.</span></span> <span data-ttu-id="a9897-156">Özellikler oluşturulan ya da zaten oluşturduysanız, hello kullanılarak erişilir [veri içeri aktarma](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) aşağıda gösterildiği gibi Azure ML modülünde:</span><span class="sxs-lookup"><span data-stu-id="a9897-156">Features can be generated or accessed if already created, using hello [Import Data](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) module in Azure ML as shown below:</span></span>

![azureml okuyucuları](./media/machine-learning-data-science-process-sql-server-virtual-machine/reader_db_featurizedinput.png)

## <span data-ttu-id="a9897-158"><a name="python"></a>Python gibi programlama dilini kullanma</span><span class="sxs-lookup"><span data-stu-id="a9897-158"><a name="python"></a>Using a programming language like Python</span></span>
<span data-ttu-id="a9897-159">Merhaba veriler SQL Server'da olduğunda Python toogenerate özelliklerini kullanarak konusu benzer tooprocessing veri açıklandığı gibi Python kullanarak Azure blob [, veri bilimi ortamında işlem Azure Blob verileri](machine-learning-data-science-process-data-blob.md).</span><span class="sxs-lookup"><span data-stu-id="a9897-159">Using Python toogenerate features when hello data is in SQL Server is similar tooprocessing data in Azure blob using Python as documented in [Process Azure Blob data in you data science environment](machine-learning-data-science-process-data-blob.md).</span></span> <span data-ttu-id="a9897-160">Merhaba veri pandas veri çerçeveye hello veritabanından yüklenen toobe gerekir ve ardından daha fazla işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="a9897-160">hello data needs toobe loaded from hello database into a pandas data frame and then can be processed further.</span></span> <span data-ttu-id="a9897-161">Biz toohello veritabanına bağlanma ve bu bölümdeki hello veri çerçevesine hello verileri yüklenirken hello işleminde belge.</span><span class="sxs-lookup"><span data-stu-id="a9897-161">We document hello process of connecting toohello database and loading hello data into hello data frame in this section.</span></span>

<span data-ttu-id="a9897-162">bağlantı dizesi biçimi aşağıdaki hello pyodbc (Değiştir servername, dbname, kullanıcı adı ve parola, belirli değerleri içeren) kullanarak Python kullanılan tooconnect tooa SQL Server veritabanından olabilir:</span><span class="sxs-lookup"><span data-stu-id="a9897-162">hello following connection string format can be used tooconnect tooa SQL Server database from Python using pyodbc (replace servername, dbname, username and password with your specific values):</span></span>

    #Set up hello SQL Azure connection
    import pyodbc
    conn = pyodbc.connect('DRIVER={SQL Server};SERVER=<servername>;DATABASE=<dbname>;UID=<username>;PWD=<password>')

<span data-ttu-id="a9897-163">Merhaba [Pandas Kitaplığı](http://pandas.pydata.org/) Python içinde Python programlama için veri işleme için zengin bir veri yapılarını ve veri çözümleme araçları sağlar.</span><span class="sxs-lookup"><span data-stu-id="a9897-163">hello [Pandas library](http://pandas.pydata.org/) in Python provides a rich set of data structures and data analysis tools for data manipulation for Python programming.</span></span> <span data-ttu-id="a9897-164">Aşağıdaki Hello kodu hello sonuçları bir SQL Server veritabanından Pandas veri çerçeveye döndürülen okur:</span><span class="sxs-lookup"><span data-stu-id="a9897-164">hello code below reads hello results returned from a SQL Server database into a Pandas data frame:</span></span>

    # Query database and load hello returned results in pandas data frame
    data_frame = pd.read_sql('''select <columnname1>, <cloumnname2>... from <tablename>''', conn)

<span data-ttu-id="a9897-165">Konularda gibi hello Pandas veri çerçevesi ile çalışabilirsiniz artık [Panda kullanarak Azure blob depolama verileri için özellikler oluşturmak](machine-learning-data-science-create-features-blob.md).</span><span class="sxs-lookup"><span data-stu-id="a9897-165">Now you can work with hello Pandas data frame as covered in topics [Create features for Azure blob storage data using Panda](machine-learning-data-science-create-features-blob.md).</span></span>

