---
title: "aaaOperationalize Spark yerleşik makine öğrenimi modellerinin oluşturulmasına | Microsoft Docs"
description: "Nasıl tooload ve modelleri öğrenme puanı Python ile Azure Blob Storage (WASB) içinde depolanır."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 626305a2-0abf-4642-afb0-dad0f6bd24e9
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: c5fadcb13257b94dcb28a522be454f6e03dfa991
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="operationalize-spark-built-machine-learning-models"></a><span data-ttu-id="480d9-103">Spark yerleşik makine öğrenimi modellerini faaliyete</span><span class="sxs-lookup"><span data-stu-id="480d9-103">Operationalize Spark-built machine learning models</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="480d9-104">Bu konu Python Hdınsight Spark kullanarak kaydedilmiş makine öğrenimi modeline (ML) nasıl toooperationalize kümeleri gösterir.</span><span class="sxs-lookup"><span data-stu-id="480d9-104">This topic shows how toooperationalize a saved machine learning model (ML) using Python on HDInsight Spark clusters.</span></span> <span data-ttu-id="480d9-105">Tooload makine nasıl Spark Mllib'i kullanılarak oluşturulmuş ve Azure Blob Storage (WASB) depolanan learning modellerini ve nasıl açıklar tooscore de WASB içinde depolanan veri kümeleriyle bunları.</span><span class="sxs-lookup"><span data-stu-id="480d9-105">It describes how tooload machine learning models that have been built using Spark MLlib and stored in Azure Blob Storage (WASB), and how tooscore them with datasets that have also been stored in WASB.</span></span> <span data-ttu-id="480d9-106">Nasıl toopre işlem hello giriş verileri gösterir, dizin oluşturma ve kodlama işlevlerde hello Mllib'i Araç Seti ve nasıl hello ML modelleriyle Puanlama toocreate olarak kullanılan bir etiketli noktası veri nesnesi giriş dönüştürme özellikleri kullanarak hello.</span><span class="sxs-lookup"><span data-stu-id="480d9-106">It shows how toopre-process hello input data, transform features using hello indexing and encoding functions in hello MLlib toolkit, and how toocreate a labeled point data object that can be used as input for scoring with hello ML models.</span></span> <span data-ttu-id="480d9-107">Puanlama için kullanılan hello modelleri doğrusal regresyon, lojistik regresyon, rastgele orman modeli ve gradyan artırmanın ağaç modeli içerir.</span><span class="sxs-lookup"><span data-stu-id="480d9-107">hello models used for scoring include Linear Regression, Logistic Regression, Random Forest Models, and Gradient Boosting Tree Models.</span></span>

## <a name="spark-clusters-and-jupyter-notebooks"></a><span data-ttu-id="480d9-108">Spark kümeleri ve Jupyter Not Defterleri</span><span class="sxs-lookup"><span data-stu-id="480d9-108">Spark clusters and Jupyter notebooks</span></span>
<span data-ttu-id="480d9-109">Kurulum adımlarını ve hello kod toooperationalize ML modelinde, bu kılavuzda Spark 2.0 küme yanı sıra bir Hdınsight Spark 1.6 kümesi kullanmak için sağlanır.</span><span class="sxs-lookup"><span data-stu-id="480d9-109">Setup steps and hello code toooperationalize an ML model are provided in this walkthrough for using an HDInsight Spark 1.6 cluster as well as a Spark 2.0 cluster.</span></span> <span data-ttu-id="480d9-110">Bu yordamları Hello kodunu Jupyter not defterlerinde de sağlanır.</span><span class="sxs-lookup"><span data-stu-id="480d9-110">hello code for these procedures is also provided in Jupyter notebooks.</span></span>

### <a name="notebook-for-spark-16"></a><span data-ttu-id="480d9-111">Spark 1.6 için not defteri</span><span class="sxs-lookup"><span data-stu-id="480d9-111">Notebook for Spark 1.6</span></span>
<span data-ttu-id="480d9-112">Merhaba [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) nasıl toooperationalize Python kullanarak kaydedilmiş modeli kümeleri Jupyter not defteri gösterir.</span><span class="sxs-lookup"><span data-stu-id="480d9-112">hello [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) Jupyter notebook shows how toooperationalize a saved model using Python on HDInsight clusters.</span></span> 

### <a name="notebook-for-spark-20"></a><span data-ttu-id="480d9-113">Spark 2.0 için not defteri</span><span class="sxs-lookup"><span data-stu-id="480d9-113">Notebook for Spark 2.0</span></span>
<span data-ttu-id="480d9-114">bir Hdınsight Spark 2.0 kümesi ile Spark 1.6 toouse toomodify hello Jupyter not defteri hello Python kodu dosyasıyla Değiştir [bu dosyayı](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).</span><span class="sxs-lookup"><span data-stu-id="480d9-114">toomodify hello Jupyter notebook for Spark 1.6 toouse with an HDInsight Spark 2.0 cluster, replace hello Python code file with [this file](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).</span></span> <span data-ttu-id="480d9-115">Bu kod tooconsume hello modelleri Spark 2. 0'nasıl oluşturulacağını gösterir.</span><span class="sxs-lookup"><span data-stu-id="480d9-115">This code shows how tooconsume hello models created in Spark 2.0.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="480d9-116">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="480d9-116">Prerequisites</span></span>

1. <span data-ttu-id="480d9-117">Bir Azure hesabı ve Spark 1.6 (veya Spark 2.0) ihtiyacınız Hdınsight küme toocomplete Bu izlenecek yol.</span><span class="sxs-lookup"><span data-stu-id="480d9-117">You need an Azure account and a Spark 1.6 (or Spark 2.0) HDInsight cluster toocomplete this walkthrough.</span></span> <span data-ttu-id="480d9-118">Merhaba bkz [genel bakış, verileri Azure Hdınsight'ta Spark kullanmanın Bilim](machine-learning-data-science-spark-overview.md) yönelik yönergeler toosatisfy bu gereksinimleri.</span><span class="sxs-lookup"><span data-stu-id="480d9-118">See hello [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) for instructions on how toosatisfy these requirements.</span></span> <span data-ttu-id="480d9-119">Bu konu ayrıca açıklamasını hello burada kullanılan NYC 2013 ücreti verileri ve nasıl tooexecute kod hello Spark kümesinde Jupyter not defteri gelen yönergeleri içerir.</span><span class="sxs-lookup"><span data-stu-id="480d9-119">That topic also contains a description of hello NYC 2013 Taxi data used here and instructions on how tooexecute code from a Jupyter notebook on hello Spark cluster.</span></span> 
2. <span data-ttu-id="480d9-120">Merhaba makine öğrenimi modellerini oluşturmalısınız toobe skoru burada hello aracılığıyla çalışarak [veri keşfi ve modelleme Spark ile](machine-learning-data-science-spark-data-exploration-modeling.md) konu hello Spark 1.6 küme veya hello Spark 2.0 dizüstü bilgisayarlar için.</span><span class="sxs-lookup"><span data-stu-id="480d9-120">You must also create hello machine learning models toobe scored here by working through hello [Data exploration and modeling with Spark](machine-learning-data-science-spark-data-exploration-modeling.md) topic for hello Spark 1.6 cluster or hello Spark 2.0 notebooks.</span></span> 
3. <span data-ttu-id="480d9-121">Merhaba Spark 2.0 not defterlerini hello sınıflandırma görevi, hello iyi bilinen uçak zamanında ayrılma kümesinden 2011 ve 2012 için ek bir veri kümesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="480d9-121">hello Spark 2.0 notebooks use an additional data set for hello classification task, hello well-known Airline On-time departure dataset from 2011 and 2012.</span></span> <span data-ttu-id="480d9-122">Merhaba not defterlerini ve bağlantıları toothem açıklamasını hello sağlanan [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) bunları içeren hello GitHub depo.</span><span class="sxs-lookup"><span data-stu-id="480d9-122">A description of hello notebooks and links toothem are provided in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for hello GitHub repository containing them.</span></span> <span data-ttu-id="480d9-123">Ayrıca, hello kod burada ve bağlı hello not defterlerini geneldir ve tüm Spark kümesi üzerinde çalışması gerekir.</span><span class="sxs-lookup"><span data-stu-id="480d9-123">Moreover, hello code here and in hello linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="480d9-124">Hdınsight Spark kullanmıyorsanız hello Küme kurulumu ve Yönetimi adımları ne burada gösterilenden biraz farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="480d9-124">If you are not using HDInsight Spark, hello cluster setup and management steps may be slightly different from what is shown here.</span></span> 

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a><span data-ttu-id="480d9-125">Kurulumu: Spark bağlam depolama konumları, kitaplıklar ve hello hazır</span><span class="sxs-lookup"><span data-stu-id="480d9-125">Setup: storage locations, libraries, and hello preset Spark context</span></span>
<span data-ttu-id="480d9-126">Spark mümkün tooread ve yazma tooan Azure Blob Storage (WASB) olur.</span><span class="sxs-lookup"><span data-stu-id="480d9-126">Spark is able tooread and write tooan Azure Storage Blob (WASB).</span></span> <span data-ttu-id="480d9-127">Bu nedenle depolanan mevcut verilerinizi Spark kullanarak işlenebilir ve depolanan yeniden WASB hello sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="480d9-127">So any of your existing data stored there can be processed using Spark and hello results stored again in WASB.</span></span>

<span data-ttu-id="480d9-128">toosave modelleri veya WASB dosyalarında, hello yolu düzgün belirtilen toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="480d9-128">toosave models or files in WASB, hello path needs toobe specified properly.</span></span> <span data-ttu-id="480d9-129">Merhaba varsayılan kapsayıcı bağlı toohello Spark kümesi ile başlayan bir yol kullanarak başvurulabilir: *"wasb / /"*.</span><span class="sxs-lookup"><span data-stu-id="480d9-129">hello default container attached toohello Spark cluster can be referenced using a path beginning with: *"wasb//"*.</span></span> <span data-ttu-id="480d9-130">Merhaba aşağıdaki kod örneği hello konumunu okuma hello veri toobe belirtir ve hello yolu hello modeli depolama dizini toowhich hello modeli çıktı için kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="480d9-130">hello following code sample specifies hello location of hello data toobe read and hello path for hello model storage directory toowhich hello model output is saved.</span></span> 

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="480d9-131">Dizin yolları için depolama konumları WASB ayarlayın</span><span class="sxs-lookup"><span data-stu-id="480d9-131">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="480d9-132">Modelleri kaydedilir: "wasb: / / / kullanıcı/remoteuser/NYCTaxi/modelleri".</span><span class="sxs-lookup"><span data-stu-id="480d9-132">Models are saved in: "wasb:///user/remoteuser/NYCTaxi/Models".</span></span> <span data-ttu-id="480d9-133">Bu yolu düzgün şekilde ayarlanmamışsa, modelleri Puanlama için yüklü değil.</span><span class="sxs-lookup"><span data-stu-id="480d9-133">If this path is not set properly, models are not loaded for scoring.</span></span>

<span data-ttu-id="480d9-134">Merhaba puanlanmış sonuçları içinde kaydedildi: "wasb: / / / kullanıcı/remoteuser/NYCTaxi/ScoredResults".</span><span class="sxs-lookup"><span data-stu-id="480d9-134">hello scored results have been saved in: "wasb:///user/remoteuser/NYCTaxi/ScoredResults".</span></span> <span data-ttu-id="480d9-135">Merhaba yolu toofolder yanlış ise, sonuçları klasörde kaydedilmez.</span><span class="sxs-lookup"><span data-stu-id="480d9-135">If hello path toofolder is incorrect, results are not saved in that folder.</span></span>   

> [!NOTE]
> <span data-ttu-id="480d9-136">Merhaba dosya yolu konumlarını kopyalanır ve bu koddan hello son hello hücrenin hello çıktısını hello yer tutucuları içine yapıştırdığınız **machine-learning-data-science-spark-data-exploration-modeling.ipynb** dizüstü bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="480d9-136">hello file path locations can be copied and pasted into hello placeholders in this code from hello output of hello last cell of hello **machine-learning-data-science-spark-data-exploration-modeling.ipynb** notebook.</span></span>   
> 
> 

<span data-ttu-id="480d9-137">Merhaba kod tooset dizin yolu şöyledir:</span><span class="sxs-lookup"><span data-stu-id="480d9-137">Here is hello code tooset directory paths:</span></span> 

    # LOCATION OF DATA tooBE SCORED (TEST DATA)
    taxi_test_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Test.tsv";

    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE hello LAST BACKSLASH IN THIS PATH IS NEEDED
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 

    # SET SCORDED RESULT DIRECTORY PATH
    # NOTE hello LAST BACKSLASH IN THIS PATH IS NEEDED
    scoredResultDir = "wasb:///user/remoteuser/NYCTaxi/ScoredResults/"; 

    # FILE LOCATIONS FOR hello MODELS tooBE SCORED
    logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-04-1817_40_35.796789"
    linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-04-1817_44_00.993832"
    randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-04-1817_42_58.899412"
    randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-04-1817_44_27.204734"
    BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-04-1817_43_16.354770"
    BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-04-1817_44_46.206262"

    # RECORD START TIME
    import datetime
    datetime.datetime.now()

<span data-ttu-id="480d9-138">**ÇIKTI:**</span><span class="sxs-lookup"><span data-stu-id="480d9-138">**OUTPUT:**</span></span>

<span data-ttu-id="480d9-139">DateTime.DateTime (2016, 4, 25, 23, 56, 19, 229403)</span><span class="sxs-lookup"><span data-stu-id="480d9-139">datetime.datetime(2016, 4, 25, 23, 56, 19, 229403)</span></span>

### <a name="import-libraries"></a><span data-ttu-id="480d9-140">Kitaplıkları içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="480d9-140">Import libraries</span></span>
<span data-ttu-id="480d9-141">Spark bağlamını ayarlayın ve gerekli kitaplıkları koddan hello ile içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="480d9-141">Set spark context and import necessary libraries with hello following code</span></span>

    #IMPORT LIBRARIES
    import pyspark
    from pyspark import SparkConf
    from pyspark import SparkContext
    from pyspark.sql import SQLContext
    import matplotlib
    import matplotlib.pyplot as plt
    from pyspark.sql import Row
    from pyspark.sql.functions import UserDefinedFunction
    from pyspark.sql.types import *
    import atexit
    from numpy import array
    import numpy as np
    import datetime


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="480d9-142">Spark bağlamını ve PySpark sihirler hazır</span><span class="sxs-lookup"><span data-stu-id="480d9-142">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="480d9-143">Jupyter not defterleri ile sağlanan hello PySpark tekrar önceden belirlenmiş bir içerik var.</span><span class="sxs-lookup"><span data-stu-id="480d9-143">hello PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="480d9-144">Geliştirdiğiniz Merhaba uygulaması ile çalışmaya başlamadan önce bu nedenle, tooset hello Spark veya Hive bağlamları açıkça gerekmez.</span><span class="sxs-lookup"><span data-stu-id="480d9-144">So you do not need tooset hello Spark or Hive contexts explicitly before you start working with hello application you are developing.</span></span> <span data-ttu-id="480d9-145">Bunlar varsayılan olarak sizin için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="480d9-145">These are available for you by default.</span></span> <span data-ttu-id="480d9-146">Bu içerikler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="480d9-146">These contexts are:</span></span>

* <span data-ttu-id="480d9-147">SC - Spark</span><span class="sxs-lookup"><span data-stu-id="480d9-147">sc - for Spark</span></span> 
* <span data-ttu-id="480d9-148">sqlContext - Hive için</span><span class="sxs-lookup"><span data-stu-id="480d9-148">sqlContext - for Hive</span></span>

<span data-ttu-id="480d9-149">Merhaba PySpark çekirdeği bazı önceden tanımlanmış "sihirleri" ile çağırabilir özel komutlar olduğu sağlar %%.</span><span class="sxs-lookup"><span data-stu-id="480d9-149">hello PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="480d9-150">Bu kod örneklerinde kullanılan olan iki komut vardır.</span><span class="sxs-lookup"><span data-stu-id="480d9-150">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="480d9-151">**%% yerel** belirtilen sonraki satırların hello kodda yerel olarak yürütülür.</span><span class="sxs-lookup"><span data-stu-id="480d9-151">**%%local** Specified that hello code in subsequent lines is executed locally.</span></span> <span data-ttu-id="480d9-152">Kod geçerli Python kodu olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="480d9-152">Code must be valid Python code.</span></span>
* <span data-ttu-id="480d9-153">**%% sql -o<variable name>**</span><span class="sxs-lookup"><span data-stu-id="480d9-153">**%%sql -o <variable name>**</span></span> 
* <span data-ttu-id="480d9-154">Merhaba sqlContext bir Hive sorgusu yürütür.</span><span class="sxs-lookup"><span data-stu-id="480d9-154">Executes a Hive query against hello sqlContext.</span></span> <span data-ttu-id="480d9-155">Merhaba -o parametre aktarılırsa hello hello sorgunun sonucu hello kalıcı %% Pandas dataframe olarak yerel Python bağlamı.</span><span class="sxs-lookup"><span data-stu-id="480d9-155">If hello -o parameter is passed, hello result of hello query is persisted in hello %%local Python context as a Pandas dataframe.</span></span>

<span data-ttu-id="480d9-156">Hello tekrar Jupyter not defterlerini ve önceden tanımlanmış hello hakkında daha fazla bilgi "magics için" sağladıkları, bkz: [Jupyter not defterlerinde kullanılabilen çekirdekler Hdınsight Spark Linux kümeleri Hdınsight'ta](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="480d9-156">For more information on hello kernels for Jupyter notebooks and hello predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="ingest-data-and-create-a-cleaned-data-frame"></a><span data-ttu-id="480d9-157">Veri alma ve Temizlenen veri çerçeve oluşturma</span><span class="sxs-lookup"><span data-stu-id="480d9-157">Ingest data and create a cleaned data frame</span></span>
<span data-ttu-id="480d9-158">Bu bölümde bir dizi görevleri gerekli tooingest hello veri toobe skoru hello kodunu içerir.</span><span class="sxs-lookup"><span data-stu-id="480d9-158">This section contains hello code for a series of tasks required tooingest hello data toobe scored.</span></span> <span data-ttu-id="480d9-159">Bir birleştirilmiş % 0,1 örnek dosyasının (.tsv dosyası olarak depolanır) hello ücreti seyahat ve ücreti biçiminde hello verileri okuma ve ardından temiz veri çerçevesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="480d9-159">Read in a joined 0.1% sample of hello taxi trip and fare file (stored as a .tsv file), format hello data, and then creates a clean data frame.</span></span>

<span data-ttu-id="480d9-160">Merhaba ücreti seyahat ve ücreti dosyaları alanına göre sağlanan hello yordamı: [takım veri bilimi işlemi eylemde hello: Hdınsight Hadoop kümeleri kullanarak](machine-learning-data-science-process-hive-walkthrough.md) konu.</span><span class="sxs-lookup"><span data-stu-id="480d9-160">hello taxi trip and fare files were joined based on hello procedure provided in the: [hello Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md) topic.</span></span>

    # INGEST DATA AND CREATE A CLEANED DATA FRAME

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_test_file = sc.textFile(taxi_test_file_loc)

    # GET SCHEMA OF hello FILE FROM HEADER
    taxi_header = taxi_test_file.filter(lambda l: "medallion" in l)

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_temp = taxi_test_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))

    # GET SCHEMA OF hello FILE FROM HEADER
    schema_string = taxi_test_file.first()
    fields = [StructField(field_name, StringType(), True) for field_name in schema_string.split('\t')]
    fields[7].dataType = IntegerType() #Pickup hour
    fields[8].dataType = IntegerType() # Pickup week
    fields[9].dataType = IntegerType() # Weekday
    fields[10].dataType = IntegerType() # Passenger count
    fields[11].dataType = FloatType() # Trip time in secs
    fields[12].dataType = FloatType() # Trip distance
    fields[19].dataType = FloatType() # Fare amount
    fields[20].dataType = FloatType() # Surcharge
    fields[21].dataType = FloatType() # Mta_tax
    fields[22].dataType = FloatType() # Tip amount
    fields[23].dataType = FloatType() # Tolls amount
    fields[24].dataType = FloatType() # Total amount
    fields[25].dataType = IntegerType() # Tipped or not
    fields[26].dataType = IntegerType() # Tip class
    taxi_schema = StructType(fields)

    # CREATE DATA FRAME
    taxi_df_test = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    # CREATE A CLEANED DATA-FRAME BY DROPPING SOME UN-NECESSARY COLUMNS & FILTERING FOR UNDESIRED VALUES OR OUTLIERS
    taxi_df_test_cleaned = taxi_df_test.drop('medallion').drop('hack_license').drop('store_and_fwd_flag').drop('pickup_datetime')\
        .drop('dropoff_datetime').drop('pickup_longitude').drop('pickup_latitude').drop('dropoff_latitude')\
        .drop('dropoff_longitude').drop('tip_class').drop('total_amount').drop('tolls_amount').drop('mta_tax')\
        .drop('direct_distance').drop('surcharge')\
        .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200" )

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_test_cleaned.cache()
    taxi_df_test_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_test_cleaned.registerTempTable("taxi_test")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="480d9-161">**ÇIKTI:**</span><span class="sxs-lookup"><span data-stu-id="480d9-161">**OUTPUT:**</span></span>

<span data-ttu-id="480d9-162">Hücre tooexecute geçen süre: 46.37 saniye</span><span class="sxs-lookup"><span data-stu-id="480d9-162">Time taken tooexecute above cell: 46.37 seconds</span></span>

## <a name="prepare-data-for-scoring-in-spark"></a><span data-ttu-id="480d9-163">Spark Puanlama için verileri hazırlama</span><span class="sxs-lookup"><span data-stu-id="480d9-163">Prepare data for scoring in Spark</span></span>
<span data-ttu-id="480d9-164">Bu bölümde, nasıl tooindex, kodlama ve kendileri için sınıflandırma ve regresyon Mllib'i denetimli öğrenme algoritmalara kullanın kategorik özellikleri tooprepare ölçeği gösterir.</span><span class="sxs-lookup"><span data-stu-id="480d9-164">This section shows how tooindex, encode, and scale categorical features tooprepare them for use in MLlib supervised learning algorithms for classification and regression.</span></span>

### <a name="feature-transformation-index-and-encode-categorical-features-for-input-into-models-for-scoring"></a><span data-ttu-id="480d9-165">Özellik dönüşümü: dizin ve puanlama modelleri giriş için kategorik özellikleri kodlama</span><span class="sxs-lookup"><span data-stu-id="480d9-165">Feature transformation: index and encode categorical features for input into models for scoring</span></span>
<span data-ttu-id="480d9-166">Bu bölümde gösterilmiştir nasıl tooindex kategorik verileri kullanarak bir `StringIndexer` ve özelliklerle kodlamak `OneHotEncoder` hello modellerini giriş.</span><span class="sxs-lookup"><span data-stu-id="480d9-166">This section shows how tooindex categorical data using a `StringIndexer` and encode features with `OneHotEncoder` input into hello models.</span></span>

<span data-ttu-id="480d9-167">Merhaba [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) bir dize sütunu etiketlerini tooa sütununun etiket dizinlerini kodlar.</span><span class="sxs-lookup"><span data-stu-id="480d9-167">hello [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) encodes a string column of labels tooa column of label indices.</span></span> <span data-ttu-id="480d9-168">Merhaba dizinlerini etiket sıklıklarını göre sıralanır.</span><span class="sxs-lookup"><span data-stu-id="480d9-168">hello indices are ordered by label frequencies.</span></span> 

<span data-ttu-id="480d9-169">Merhaba [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) sütununun etiket dizinlerini tooa ikili vektörler, en çok bir değerle tek bir-bir sütun eşler.</span><span class="sxs-lookup"><span data-stu-id="480d9-169">hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) maps a column of label indices tooa column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="480d9-170">Bu kodlama Lojistik regresyon gibi sürekli değerli özellikleri beklediğiniz algoritmalarına olanak uygulanan toobe toocategorical özellikleri.</span><span class="sxs-lookup"><span data-stu-id="480d9-170">This encoding allows algorithms that expect continuous valued features, such as logistic regression, toobe applied toocategorical features.</span></span>

    #INDEX AND ONE-HOT ENCODE CATEGORICAL FEATURES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, VectorIndexer

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night" 
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush" 
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_test 
    """
    taxi_df_test_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_test_with_newFeatures.cache()
    taxi_df_test_with_newFeatures.count()

    # INDEX AND ONE-HOT ENCODING
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_test_with_newFeatures) # Input data-frame is hello cleaned one from above
    indexed = model.transform(taxi_df_test_with_newFeatures)
    encoder = OneHotEncoder(dropLast=False, inputCol="vendorIndex", outputCol="vendorVec")
    encoded1 = encoder.transform(indexed)

    # INDEX AND ENCODE RATE_CODE
    stringIndexer = StringIndexer(inputCol="rate_code", outputCol="rateIndex")
    model = stringIndexer.fit(encoded1)
    indexed = model.transform(encoded1)
    encoder = OneHotEncoder(dropLast=False, inputCol="rateIndex", outputCol="rateVec")
    encoded2 = encoder.transform(indexed)

    # INDEX AND ENCODE PAYMENT_TYPE
    stringIndexer = StringIndexer(inputCol="payment_type", outputCol="paymentIndex")
    model = stringIndexer.fit(encoded2)
    indexed = model.transform(encoded2)
    encoder = OneHotEncoder(dropLast=False, inputCol="paymentIndex", outputCol="paymentVec")
    encoded3 = encoder.transform(indexed)

    # INDEX AND ENCODE TRAFFIC TIME BINS
    stringIndexer = StringIndexer(inputCol="TrafficTimeBins", outputCol="TrafficTimeBinsIndex")
    model = stringIndexer.fit(encoded3)
    indexed = model.transform(encoded3)
    encoder = OneHotEncoder(dropLast=False, inputCol="TrafficTimeBinsIndex", outputCol="TrafficTimeBinsVec")
    encodedFinal = encoder.transform(indexed)

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="480d9-171">**ÇIKTI:**</span><span class="sxs-lookup"><span data-stu-id="480d9-171">**OUTPUT:**</span></span>

<span data-ttu-id="480d9-172">Hücre tooexecute geçen süre: 5.37 saniye</span><span class="sxs-lookup"><span data-stu-id="480d9-172">Time taken tooexecute above cell: 5.37 seconds</span></span>

### <a name="create-rdd-objects-with-feature-arrays-for-input-into-models"></a><span data-ttu-id="480d9-173">Özellik dizisi modelleri giriş için olan RDD nesneleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="480d9-173">Create RDD objects with feature arrays for input into models</span></span>
<span data-ttu-id="480d9-174">Bu bölüm, nasıl bir RDD olarak tooindex kategorik metin veri nesnesi ve kullanılan tootrain ve test Mllib'i Lojistik regresyon ve ağaç tabanlı modelleri olamaz bir hot kodlamak gösteren kod içerir.</span><span class="sxs-lookup"><span data-stu-id="480d9-174">This section contains code that shows how tooindex categorical text data as an RDD object and one-hot encode it so it can be used tootrain and test MLlib logistic regression and tree-based models.</span></span> <span data-ttu-id="480d9-175">Merhaba dizinlenmiş veri depolanan [dayanıklı Dağıtılmış veri kümesi (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) nesneleri.</span><span class="sxs-lookup"><span data-stu-id="480d9-175">hello indexed data is stored in [Resilient Distributed Dataset (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) objects.</span></span> <span data-ttu-id="480d9-176">Merhaba temel soyutlama Spark bunlar.</span><span class="sxs-lookup"><span data-stu-id="480d9-176">These are hello basic abstraction in Spark.</span></span> <span data-ttu-id="480d9-177">RDD nesne üzerinde Spark ile paralel işletilen öğe değişmez, bölümlenmiş bir koleksiyonunu temsil eder.</span><span class="sxs-lookup"><span data-stu-id="480d9-177">An RDD object represents an immutable, partitioned collection of elements that can be operated on in parallel with Spark.</span></span>

<span data-ttu-id="480d9-178">Ayrıca nasıl tooscale verilerle hello gösteren kodu içerir `StandardScalar` doğrusal regresyon ile Stokastik gradyan düşüşü (SGD), machine learning modellerini çeşitli eğitim için yaygın olarak kullanılan bir algoritma kullanmak için Mllib'i tarafından sağlanan.</span><span class="sxs-lookup"><span data-stu-id="480d9-178">It also contains code that shows how tooscale data with hello `StandardScalar` provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD), a popular algorithm for training a wide range of machine learning models.</span></span> <span data-ttu-id="480d9-179">Merhaba [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) kullanılan tooscale hello özellikleri toounit farkı değil.</span><span class="sxs-lookup"><span data-stu-id="480d9-179">hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) is used tooscale hello features toounit variance.</span></span> <span data-ttu-id="480d9-180">Özellik ölçeklendirme, veri normalleştirme da bilinen, yaygın olarak yapılan değerlerle özellikleri olan belirli bir aşırı tartmanız olduğunu hello hedefi işlevinde oluşturmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="480d9-180">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in hello objective function.</span></span> 

    # CREATE RDD OBJECTS WITH FEATURE ARRAYS FOR INPUT INTO MODELS

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT LIBRARIES
    from pyspark.mllib.linalg import Vectors
    from pyspark.mllib.feature import StandardScaler, StandardScalerModel
    from pyspark.mllib.util import MLUtils
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex,
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        return  features

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        return  features

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingRegression(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex, 
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        return  features

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO LINEAR REGRESSION MODELS
    def parseRowOneHotRegression(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        return  features

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTESTbinary = encodedFinal.map(parseRowIndexingBinary)
    oneHotTESTbinary = encodedFinal.map(parseRowOneHotBinary)

    # FOR REGRESSION CLASSIFICATION TRAINING AND TESTING
    indexedTESTreg = encodedFinal.map(parseRowIndexingRegression)
    oneHotTESTreg = encodedFinal.map(parseRowOneHotRegression)

    # SCALING FEATURES FOR LINEARREGRESSIONWITHSGD MODEL
    scaler = StandardScaler(withMean=False, withStd=True).fit(oneHotTESTreg)
    oneHotTESTregScaled = scaler.transform(oneHotTESTreg)

    # CACHE RDDS IN MEMORY
    indexedTESTbinary.cache();
    oneHotTESTbinary.cache();
    indexedTESTreg.cache();
    oneHotTESTreg.cache();
    oneHotTESTregScaled.cache();

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="480d9-181">**ÇIKTI:**</span><span class="sxs-lookup"><span data-stu-id="480d9-181">**OUTPUT:**</span></span>

<span data-ttu-id="480d9-182">Hücre tooexecute geçen süre: 11.72 saniye</span><span class="sxs-lookup"><span data-stu-id="480d9-182">Time taken tooexecute above cell: 11.72 seconds</span></span>

## <a name="score-with-hello-logistic-regression-model-and-save-output-tooblob"></a><span data-ttu-id="480d9-183">Merhaba ile Lojistik regresyon modeli Puanlama ve çıktı tooblob Kaydet</span><span class="sxs-lookup"><span data-stu-id="480d9-183">Score with hello Logistic Regression Model and save output tooblob</span></span>
<span data-ttu-id="480d9-184">Bu bölümdeki Hello kodu nasıl tooload Azure'da kaydedilmiş bir Lojistik regresyon modeli blob depolamaya ve ücreti seyahat üzerinde bir ipucu desteklemediğini Ücretli toopredict kullanın, standart sınıflandırma Ölçümleriyle puan ve kaydedin gösterir ve hello sonuçları tooblob çizmek depolama alanı.</span><span class="sxs-lookup"><span data-stu-id="480d9-184">hello code in this section shows how tooload a Logistic Regression Model that has been saved in Azure blob storage and use it toopredict whether or not a tip is paid on a taxi trip, score it with standard classification metrics, and then save and plot hello results tooblob storage.</span></span> <span data-ttu-id="480d9-185">sonuçları skoru hello RDD nesneleri depolanır.</span><span class="sxs-lookup"><span data-stu-id="480d9-185">hello scored results are stored in RDD objects.</span></span> 

    # SCORE AND EVALUATE LOGISTIC REGRESSION MODEL

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    ## LOAD SAVED MODEL
    savedModel = LogisticRegressionModel.load(sc, logisticRegFileLoc)
    predictions = oneHotTESTbinary.map(lambda features: (float(savedModel.predict(features))))

    ## SAVE SCORED RESULTS (RDD) tooBLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp + ".txt";
    dirfilename = scoredResultDir + logisticregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="480d9-186">**ÇIKTI:**</span><span class="sxs-lookup"><span data-stu-id="480d9-186">**OUTPUT:**</span></span>

<span data-ttu-id="480d9-187">Hücre tooexecute geçen süre: 19.22 saniye</span><span class="sxs-lookup"><span data-stu-id="480d9-187">Time taken tooexecute above cell: 19.22 seconds</span></span>

## <a name="score-a-linear-regression-model"></a><span data-ttu-id="480d9-188">Doğrusal regresyon modeli Puanlama</span><span class="sxs-lookup"><span data-stu-id="480d9-188">Score a Linear Regression Model</span></span>
<span data-ttu-id="480d9-189">Kullandık [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) tootrain Itanium tabanlı sistemler için en iyi duruma getirme toopredict hello tutar ucunun için Stokastik gradyan düşüşü (SGD) kullanarak bir doğrusal regresyon modeli Ücretli.</span><span class="sxs-lookup"><span data-stu-id="480d9-189">We used [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) tootrain a linear regression model using Stochastic Gradient Descent (SGD) for optimization toopredict hello amount of tip paid.</span></span> 

<span data-ttu-id="480d9-190">Bu bölümdeki Hello kod nasıl tooload bir doğrusal regresyon modeli Azure blob depolama biriminden ölçeklendirilmiş değişkenler kullanarak Puanlama ve hello sonuçları geri toohello blob kaydedin gösterir.</span><span class="sxs-lookup"><span data-stu-id="480d9-190">hello code in this section shows how tooload a Linear Regression Model from Azure blob storage, score using scaled variables, and then save hello results back toohello blob.</span></span>

    #SCORE LINEAR REGRESSION MODEL

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #LOAD LIBRARIES
    from pyspark.mllib.regression import LinearRegressionWithSGD, LinearRegressionModel

    # LOAD MODEL AND SCORE USING ** SCALED VARIABLES **
    savedModel = LinearRegressionModel.load(sc, linearRegFileLoc)
    predictions = oneHotTESTregScaled.map(lambda features: (float(savedModel.predict(features))))

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = scoredResultDir + linearregressionfilename;
    predictions.saveAsTextFile(dirfilename)

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="480d9-191">**ÇIKTI:**</span><span class="sxs-lookup"><span data-stu-id="480d9-191">**OUTPUT:**</span></span>

<span data-ttu-id="480d9-192">Hücre tooexecute geçen süre: 16.63 saniye</span><span class="sxs-lookup"><span data-stu-id="480d9-192">Time taken tooexecute above cell: 16.63 seconds</span></span>

## <a name="score-classification-and-regression-random-forest-models"></a><span data-ttu-id="480d9-193">Sınıflandırma ve regresyon rastgele orman modeli Puanlama</span><span class="sxs-lookup"><span data-stu-id="480d9-193">Score classification and regression Random Forest Models</span></span>
<span data-ttu-id="480d9-194">Bu bölümdeki Hello kod tooload hello sınıflandırma kaydedilme gösterir ve regresyon rastgele orman Azure blob depolama alanına kaydedildi modelleri standart sınıflandırıcı ve regresyon ölçüleri kendi performansını Puanlama ve hello sonuçları geri tooblob depolama kaydedin.</span><span class="sxs-lookup"><span data-stu-id="480d9-194">hello code in this section shows how tooload hello saved classification and regression Random Forest Models saved in Azure blob storage, score their performance with standard classifier and regression measures, and then save hello results back tooblob storage.</span></span>

<span data-ttu-id="480d9-195">[Rastgele ormanlar](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) karar ağaçları ensembles şunlardır.</span><span class="sxs-lookup"><span data-stu-id="480d9-195">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="480d9-196">Bunlar, birçok karar ağaçları tooreduce hello riskini overfitting birleştirin.</span><span class="sxs-lookup"><span data-stu-id="480d9-196">They combine many decision trees tooreduce hello risk of overfitting.</span></span> <span data-ttu-id="480d9-197">Rastgele ormanlar kategorik özellikleri işleyebilir toohello çok sınıflı sınıflandırma ayarı genişletmek, özellik ölçeklendirme gerektirmez ve mümkün toocapture sapmalar olan ve etkileşimleri özellik.</span><span class="sxs-lookup"><span data-stu-id="480d9-197">Random forests can handle categorical features, extend toohello multiclass classification setting, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="480d9-198">Rastgele ormanlar hello en başarılı machine learning modellerini sınıflandırma ve regresyon biridir.</span><span class="sxs-lookup"><span data-stu-id="480d9-198">Random forests are one of hello most successful machine learning models for classification and regression.</span></span>

<span data-ttu-id="480d9-199">[Spark.mllib](http://spark.apache.org/mllib/) ve sürekli ve kategorik özelliklerini kullanarak regresyon, çok sınıflı ve ikili sınıflandırma için rastgele ormanlar destekler.</span><span class="sxs-lookup"><span data-stu-id="480d9-199">[spark.mllib](http://spark.apache.org/mllib/) supports random forests for binary and multiclass classification and for regression, using both continuous and categorical features.</span></span> 

    # SCORE RANDOM FOREST MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES    
    from pyspark.mllib.tree import RandomForest, RandomForestModel


    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB
    savedModel = RandomForestModel.load(sc, randomForestClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB
    savedModel = RandomForestModel.load(sc, randomForestRegFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfregressionfilename;
    predictions.saveAsTextFile(dirfilename)

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="480d9-200">**ÇIKTI:**</span><span class="sxs-lookup"><span data-stu-id="480d9-200">**OUTPUT:**</span></span>

<span data-ttu-id="480d9-201">Hücre tooexecute geçen süre: 31.07 saniye</span><span class="sxs-lookup"><span data-stu-id="480d9-201">Time taken tooexecute above cell: 31.07 seconds</span></span>

## <a name="score-classification-and-regression-gradient-boosting-tree-models"></a><span data-ttu-id="480d9-202">Sınıflandırma ve regresyon gradyan artırmanın ağaç modeli Puanlama</span><span class="sxs-lookup"><span data-stu-id="480d9-202">Score classification and regression Gradient Boosting Tree Models</span></span>
<span data-ttu-id="480d9-203">Bu bölümdeki Hello kod nasıl tooload sınıflandırma ve Azure blob depolama biriminden regresyon gradyan artırmanın ağaç modelleri standart sınıflandırıcı ve regresyon ölçüleri kendi performansını Puanlama ve hello sonuçları geri tooblob depolama Kaydet gösterir.</span><span class="sxs-lookup"><span data-stu-id="480d9-203">hello code in this section shows how tooload classification and regression Gradient Boosting Tree Models from Azure blob storage, score their performance with standard classifier and regression measures, and then save hello results back tooblob storage.</span></span> 

<span data-ttu-id="480d9-204">**Spark.mllib** GBTs ikili sınıflandırma ve regresyon, sürekli ve kategorik özelliklerini kullanmayı destekler.</span><span class="sxs-lookup"><span data-stu-id="480d9-204">**spark.mllib** supports GBTs for binary classification and for regression, using both continuous and categorical features.</span></span> 

<span data-ttu-id="480d9-205">[Gradyan artırmanın ağaçları](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) olan karar ağaçları ensembles.</span><span class="sxs-lookup"><span data-stu-id="480d9-205">[Gradient Boosting Trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="480d9-206">GBTs tren karar tekrarlayarak toominimize kaybı işlevi ağaçları.</span><span class="sxs-lookup"><span data-stu-id="480d9-206">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="480d9-207">GBTs kategorik özellikleri işleyebilir, özellik ölçeklendirme gerektirmez ve mümkün toocapture sapmalar olan ve etkileşimleri özellik.</span><span class="sxs-lookup"><span data-stu-id="480d9-207">GBTs can handle categorical features, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="480d9-208">Bir sınıflandırma veya çoklu sınıflar ayarında de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="480d9-208">They can also be used in a multiclass-classification setting.</span></span>

    # SCORE GRADIENT BOOSTING TREE MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB

    #LOAD AND SCORE hello MODEL
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB

    # LOAD AND SCORE MODEL 
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeRegressionFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="480d9-209">**ÇIKTI:**</span><span class="sxs-lookup"><span data-stu-id="480d9-209">**OUTPUT:**</span></span>

<span data-ttu-id="480d9-210">Hücre tooexecute geçen süre: 14.6 saniye</span><span class="sxs-lookup"><span data-stu-id="480d9-210">Time taken tooexecute above cell: 14.6 seconds</span></span>

## <a name="clean-up-objects-from-memory-and-print-scored-file-locations"></a><span data-ttu-id="480d9-211">Nesneleri bellekten temizlemek ve puanlanmış dosya konumları yazdırma</span><span class="sxs-lookup"><span data-stu-id="480d9-211">Clean up objects from memory and print scored file locations</span></span>
    # UNPERSIST OBJECTS CACHED IN MEMORY
    taxi_df_test_cleaned.unpersist()
    indexedTESTbinary.unpersist();
    oneHotTESTbinary.unpersist();
    indexedTESTreg.unpersist();
    oneHotTESTreg.unpersist();
    oneHotTESTregScaled.unpersist();


    # PRINT OUT PATH tooSCORED OUTPUT FILES
    print "logisticRegFileLoc: " + logisticregressionfilename;
    print "linearRegFileLoc: " + linearregressionfilename;
    print "randomForestClassificationFileLoc: " + rfclassificationfilename;
    print "randomForestRegFileLoc: " + rfregressionfilename;
    print "BoostedTreeClassificationFileLoc: " + btclassificationfilename;
    print "BoostedTreeRegressionFileLoc: " + btregressionfilename;


<span data-ttu-id="480d9-212">**ÇIKTI:**</span><span class="sxs-lookup"><span data-stu-id="480d9-212">**OUTPUT:**</span></span>

<span data-ttu-id="480d9-213">logisticRegFileLoc: LogisticRegressionWithLBFGS_2016 05 0317_22_38.953814.txt</span><span class="sxs-lookup"><span data-stu-id="480d9-213">logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt</span></span>

<span data-ttu-id="480d9-214">linearRegFileLoc: LinearRegressionWithSGD_2016 05 0317_22_58.878949</span><span class="sxs-lookup"><span data-stu-id="480d9-214">linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949</span></span>

<span data-ttu-id="480d9-215">randomForestClassificationFileLoc: RandomForestClassification_2016 05 0317_23_15.939247.txt</span><span class="sxs-lookup"><span data-stu-id="480d9-215">randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt</span></span>

<span data-ttu-id="480d9-216">randomForestRegFileLoc: RandomForestRegression_2016 05 0317_23_31.459140.txt</span><span class="sxs-lookup"><span data-stu-id="480d9-216">randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt</span></span>

<span data-ttu-id="480d9-217">BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt</span><span class="sxs-lookup"><span data-stu-id="480d9-217">BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt</span></span>

<span data-ttu-id="480d9-218">BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt</span><span class="sxs-lookup"><span data-stu-id="480d9-218">BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt</span></span>

## <a name="consume-spark-models-through-a-web-interface"></a><span data-ttu-id="480d9-219">Bir web arabirimi üzerinden Spark modelleri kullanma</span><span class="sxs-lookup"><span data-stu-id="480d9-219">Consume Spark Models through a web interface</span></span>
<span data-ttu-id="480d9-220">Spark tooremotely gönderme toplu işleri bir mekanizma sağlar veya Livy adlı bir bileşen bir REST aracılığıyla etkileşimli sorgular arabirim.</span><span class="sxs-lookup"><span data-stu-id="480d9-220">Spark provides a mechanism tooremotely submit batch jobs or interactive queries through a REST interface with a component called Livy.</span></span> <span data-ttu-id="480d9-221">Livy Hdınsight Spark kümenizin üzerinde varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="480d9-221">Livy is enabled by default on your HDInsight Spark cluster.</span></span> <span data-ttu-id="480d9-222">Livy hakkında daha fazla bilgi için bkz: [uzaktan Livy kullanarak Spark gönderme işleri](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="480d9-222">For more information on Livy, see: [Submit Spark jobs remotely using Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md).</span></span> 

<span data-ttu-id="480d9-223">Tooremotely bir Azure blob depolanır ve hello sonuçları tooanother blob yazan bir dosya puanları toplu iş gönderme Livy kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="480d9-223">You can use Livy tooremotely submit a job that batch scores a file that is stored in an Azure blob and then writes hello results tooanother blob.</span></span> <span data-ttu-id="480d9-224">toodo bunu hello Python komut dosyasını karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="480d9-224">toodo this, you upload hello Python script from</span></span>  
<span data-ttu-id="480d9-225">[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) toohello blob hello Spark kümesi.</span><span class="sxs-lookup"><span data-stu-id="480d9-225">[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) toohello blob of hello Spark cluster.</span></span> <span data-ttu-id="480d9-226">Gibi bir araç kullanabilirsiniz **Microsoft Azure Storage Gezgini** veya **AzCopy** toocopy hello betik toohello küme blob.</span><span class="sxs-lookup"><span data-stu-id="480d9-226">You can use a tool like **Microsoft Azure Storage Explorer** or **AzCopy** toocopy hello script toohello cluster blob.</span></span> <span data-ttu-id="480d9-227">Örneğimizde biz hello betik çok karşıya***wasb:///example/python/ConsumeGBNYCReg.py***.</span><span class="sxs-lookup"><span data-stu-id="480d9-227">In our case we uploaded hello script too***wasb:///example/python/ConsumeGBNYCReg.py***.</span></span>   

> [!NOTE]
> <span data-ttu-id="480d9-228">hello Spark kümesi ile ilişkili hello depolama hesabı için hello portalı bulunabilir erişim tuşları hello.</span><span class="sxs-lookup"><span data-stu-id="480d9-228">hello access keys that you need can be found on hello portal for hello storage account associated with hello Spark cluster.</span></span> 
> 
> 

<span data-ttu-id="480d9-229">Toothis konumu karşıya sonra dağıtılmış bir bağlamda hello Spark kümesinde bu komut dosyasını çalıştırır.</span><span class="sxs-lookup"><span data-stu-id="480d9-229">Once uploaded toothis location, this script runs within hello Spark cluster in a distributed context.</span></span> <span data-ttu-id="480d9-230">Merhaba modelini yükler ve giriş dosyaları hello modeline dayalı Öngörüler çalışır.</span><span class="sxs-lookup"><span data-stu-id="480d9-230">It loads hello model and runs predictions on input files based on hello model.</span></span>  

<span data-ttu-id="480d9-231">Basit bir HTTPS/REST istek üzerinde Livy yaparak, bu komut dosyası uzaktan çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="480d9-231">You can invoke this script remotely by making a simple HTTPS/REST request on Livy.</span></span>  <span data-ttu-id="480d9-232">İşte uzaktan bir curl komutunu tooconstruct hello HTTP isteği tooinvoke hello Python komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="480d9-232">Here is a curl command tooconstruct hello HTTP request tooinvoke hello Python script remotely.</span></span> <span data-ttu-id="480d9-233">CLUSTERLOGIN, CLUSTERPASSWORD, CLUSTERNAME Spark kümenizin hello uygun değerlerle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="480d9-233">Replace CLUSTERLOGIN, CLUSTERPASSWORD, CLUSTERNAME with hello appropriate values for your Spark cluster.</span></span>

    # CURL COMMAND tooINVOKE PYTHON SCRIPT WITH HTTP REQUEST

    curl -k --user "CLUSTERLOGIN:CLUSTERPASSWORD" -X POST --data "{\"file\": \"wasb:///example/python/ConsumeGBNYCReg.py\"}" -H "Content-Type: application/json" https://CLUSTERNAME.azurehdinsight.net/livy/batches

<span data-ttu-id="480d9-234">Temel kimlik doğrulaması ile basit bir HTTPS çağrı yaparak hello uzak sistem tooinvoke hello Spark iş Livy aracılığıyla üzerinde herhangi bir dil kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="480d9-234">You can use any language on hello remote system tooinvoke hello Spark job through Livy by making a simple HTTPS call with Basic Authentication.</span></span>   

> [!NOTE]
> <span data-ttu-id="480d9-235">Bu HTTP arama yaparken bu kullanışlı toouse hello Python istekleri kitaplığı olacaktır, ancak şu anda Azure işlevlerinde varsayılan olarak yüklü değildir.</span><span class="sxs-lookup"><span data-stu-id="480d9-235">It would be convenient toouse hello Python Requests library when making this HTTP call, but it is not currently installed by default in Azure Functions.</span></span> <span data-ttu-id="480d9-236">Bu nedenle eski HTTP kitaplıkları onun yerine kullanılır.</span><span class="sxs-lookup"><span data-stu-id="480d9-236">So older HTTP libraries are used instead.</span></span>   
> 
> 

<span data-ttu-id="480d9-237">Merhaba Python kodu hello HTTP çağrısı şöyledir:</span><span class="sxs-lookup"><span data-stu-id="480d9-237">Here is hello Python code for hello HTTP call:</span></span>

    #MAKE AN HTTPS CALL ON LIVY. 

    import os

    # OLDER HTTP LIBRARIES USED HERE INSTEAD OF hello REQUEST LIBRARY AS THEY ARE AVAILBLE BY DEFAULT
    import httplib, urllib, base64

    # REPLACE VALUE WITH ONES FOR YOUR SPARK CLUSTER
    host = '<spark cluster name>.azurehdinsight.net:443'
    username='<username>'
    password='<password>'

    #AUTHORIZATION
    conn = httplib.HTTPSConnection(host)
    auth = base64.encodestring('%s:%s' % (username, password)).replace('\n', '')
    headers = {'Content-Type': 'application/json', 'Authorization': 'Basic %s' % auth}

    # SPECIFY hello PYTHON SCRIPT tooRUN ON hello SPARK CLUSTER
    # IN hello FILE PARAMETER OF hello JSON POST REQUEST BODY
    r=conn.request("POST", '/livy/batches', '{"file": "wasb:///example/python/ConsumeGBNYCReg.py"}', headers )
    response = conn.getresponse().read()
    print(response)
    conn.close()


<span data-ttu-id="480d9-238">Bu Python kodu çok ekleyebilirsiniz[Azure işlevleri](https://azure.microsoft.com/documentation/services/functions/) tootrigger blob puanlar bir Spark iş gönderme Zamanlayıcı, oluşturma veya güncelleştirme bir BLOB gibi çeşitli olayları temel.</span><span class="sxs-lookup"><span data-stu-id="480d9-238">You can also add this Python code too[Azure Functions](https://azure.microsoft.com/documentation/services/functions/) tootrigger a Spark job submission that scores a blob based on various events like a timer, creation, or update of a blob.</span></span> 

<span data-ttu-id="480d9-239">Kod boş istemci deneyimini tercih ederseniz, hello kullan [Azure Logic Apps](https://azure.microsoft.com/documentation/services/app-service/logic/) tooinvoke hello Spark toplu hello üzerinde bir HTTP eylemi tanımlayarak Puanlama **Logic Apps Tasarımcısı** ve parametrelerini ayarlama.</span><span class="sxs-lookup"><span data-stu-id="480d9-239">If you prefer a code free client experience, use hello [Azure Logic Apps](https://azure.microsoft.com/documentation/services/app-service/logic/) tooinvoke hello Spark batch scoring by defining an HTTP action on hello **Logic Apps Designer** and setting its parameters.</span></span> 

* <span data-ttu-id="480d9-240">Azure portalından seçerek yeni bir mantıksal uygulama oluşturma **+ yeni** -> **Web + mobil** -> **mantıksal uygulama**.</span><span class="sxs-lookup"><span data-stu-id="480d9-240">From Azure portal, create a new Logic App by selecting **+New** -> **Web + Mobile** -> **Logic App**.</span></span> 
* <span data-ttu-id="480d9-241">Merhaba yukarı toobring **Logic Apps Tasarımcısı**, hello hello mantıksal uygulama adını ve uygulama hizmeti planı girin.</span><span class="sxs-lookup"><span data-stu-id="480d9-241">toobring up hello **Logic Apps Designer**, enter hello name of hello Logic App and App Service Plan.</span></span>
* <span data-ttu-id="480d9-242">Bir HTTP eylem seçin ve aşağıdaki şekilde hello gösterilen hello parametreleri girin:</span><span class="sxs-lookup"><span data-stu-id="480d9-242">Select an HTTP action and enter hello parameters shown in hello following figure:</span></span>

![Logic Apps Tasarımcısı](./media/machine-learning-data-science-spark-model-consumption/spark-logica-app-client.png)

## <a name="whats-next"></a><span data-ttu-id="480d9-244">Sırada ne var?</span><span class="sxs-lookup"><span data-stu-id="480d9-244">What's next?</span></span>
<span data-ttu-id="480d9-245">**Çapraz doğrulama ve hyperparameter Süpürme**: bkz [veri keşfi ve modelleme Spark ile Gelişmiş](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) modelleri nasıl olabilir üzerinde çapraz doğrulama ve parametre hyper Süpürme kullanılarak eğitilmiş.</span><span class="sxs-lookup"><span data-stu-id="480d9-245">**Cross-validation and hyperparameter sweeping**: See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping.</span></span>

