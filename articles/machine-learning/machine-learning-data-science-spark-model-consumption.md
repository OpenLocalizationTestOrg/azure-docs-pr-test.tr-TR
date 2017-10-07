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
# <a name="operationalize-spark-built-machine-learning-models"></a>Spark yerleşik makine öğrenimi modellerini faaliyete
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

Bu konu Python Hdınsight Spark kullanarak kaydedilmiş makine öğrenimi modeline (ML) nasıl toooperationalize kümeleri gösterir. Tooload makine nasıl Spark Mllib'i kullanılarak oluşturulmuş ve Azure Blob Storage (WASB) depolanan learning modellerini ve nasıl açıklar tooscore de WASB içinde depolanan veri kümeleriyle bunları. Nasıl toopre işlem hello giriş verileri gösterir, dizin oluşturma ve kodlama işlevlerde hello Mllib'i Araç Seti ve nasıl hello ML modelleriyle Puanlama toocreate olarak kullanılan bir etiketli noktası veri nesnesi giriş dönüştürme özellikleri kullanarak hello. Puanlama için kullanılan hello modelleri doğrusal regresyon, lojistik regresyon, rastgele orman modeli ve gradyan artırmanın ağaç modeli içerir.

## <a name="spark-clusters-and-jupyter-notebooks"></a>Spark kümeleri ve Jupyter Not Defterleri
Kurulum adımlarını ve hello kod toooperationalize ML modelinde, bu kılavuzda Spark 2.0 küme yanı sıra bir Hdınsight Spark 1.6 kümesi kullanmak için sağlanır. Bu yordamları Hello kodunu Jupyter not defterlerinde de sağlanır.

### <a name="notebook-for-spark-16"></a>Spark 1.6 için not defteri
Merhaba [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) nasıl toooperationalize Python kullanarak kaydedilmiş modeli kümeleri Jupyter not defteri gösterir. 

### <a name="notebook-for-spark-20"></a>Spark 2.0 için not defteri
bir Hdınsight Spark 2.0 kümesi ile Spark 1.6 toouse toomodify hello Jupyter not defteri hello Python kodu dosyasıyla Değiştir [bu dosyayı](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py). Bu kod tooconsume hello modelleri Spark 2. 0'nasıl oluşturulacağını gösterir.


## <a name="prerequisites"></a>Ön koşullar

1. Bir Azure hesabı ve Spark 1.6 (veya Spark 2.0) ihtiyacınız Hdınsight küme toocomplete Bu izlenecek yol. Merhaba bkz [genel bakış, verileri Azure Hdınsight'ta Spark kullanmanın Bilim](machine-learning-data-science-spark-overview.md) yönelik yönergeler toosatisfy bu gereksinimleri. Bu konu ayrıca açıklamasını hello burada kullanılan NYC 2013 ücreti verileri ve nasıl tooexecute kod hello Spark kümesinde Jupyter not defteri gelen yönergeleri içerir. 
2. Merhaba makine öğrenimi modellerini oluşturmalısınız toobe skoru burada hello aracılığıyla çalışarak [veri keşfi ve modelleme Spark ile](machine-learning-data-science-spark-data-exploration-modeling.md) konu hello Spark 1.6 küme veya hello Spark 2.0 dizüstü bilgisayarlar için. 
3. Merhaba Spark 2.0 not defterlerini hello sınıflandırma görevi, hello iyi bilinen uçak zamanında ayrılma kümesinden 2011 ve 2012 için ek bir veri kümesi kullanın. Merhaba not defterlerini ve bağlantıları toothem açıklamasını hello sağlanan [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) bunları içeren hello GitHub depo. Ayrıca, hello kod burada ve bağlı hello not defterlerini geneldir ve tüm Spark kümesi üzerinde çalışması gerekir. Hdınsight Spark kullanmıyorsanız hello Küme kurulumu ve Yönetimi adımları ne burada gösterilenden biraz farklı olabilir. 

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a>Kurulumu: Spark bağlam depolama konumları, kitaplıklar ve hello hazır
Spark mümkün tooread ve yazma tooan Azure Blob Storage (WASB) olur. Bu nedenle depolanan mevcut verilerinizi Spark kullanarak işlenebilir ve depolanan yeniden WASB hello sonuçlanır.

toosave modelleri veya WASB dosyalarında, hello yolu düzgün belirtilen toobe gerekir. Merhaba varsayılan kapsayıcı bağlı toohello Spark kümesi ile başlayan bir yol kullanarak başvurulabilir: *"wasb / /"*. Merhaba aşağıdaki kod örneği hello konumunu okuma hello veri toobe belirtir ve hello yolu hello modeli depolama dizini toowhich hello modeli çıktı için kaydedilir. 

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a>Dizin yolları için depolama konumları WASB ayarlayın
Modelleri kaydedilir: "wasb: / / / kullanıcı/remoteuser/NYCTaxi/modelleri". Bu yolu düzgün şekilde ayarlanmamışsa, modelleri Puanlama için yüklü değil.

Merhaba puanlanmış sonuçları içinde kaydedildi: "wasb: / / / kullanıcı/remoteuser/NYCTaxi/ScoredResults". Merhaba yolu toofolder yanlış ise, sonuçları klasörde kaydedilmez.   

> [!NOTE]
> Merhaba dosya yolu konumlarını kopyalanır ve bu koddan hello son hello hücrenin hello çıktısını hello yer tutucuları içine yapıştırdığınız **machine-learning-data-science-spark-data-exploration-modeling.ipynb** dizüstü bilgisayar.   
> 
> 

Merhaba kod tooset dizin yolu şöyledir: 

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

**ÇIKTI:**

DateTime.DateTime (2016, 4, 25, 23, 56, 19, 229403)

### <a name="import-libraries"></a>Kitaplıkları içeri aktarma
Spark bağlamını ayarlayın ve gerekli kitaplıkları koddan hello ile içeri aktarma

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


### <a name="preset-spark-context-and-pyspark-magics"></a>Spark bağlamını ve PySpark sihirler hazır
Jupyter not defterleri ile sağlanan hello PySpark tekrar önceden belirlenmiş bir içerik var. Geliştirdiğiniz Merhaba uygulaması ile çalışmaya başlamadan önce bu nedenle, tooset hello Spark veya Hive bağlamları açıkça gerekmez. Bunlar varsayılan olarak sizin için kullanılabilir. Bu içerikler şunlardır:

* SC - Spark 
* sqlContext - Hive için

Merhaba PySpark çekirdeği bazı önceden tanımlanmış "sihirleri" ile çağırabilir özel komutlar olduğu sağlar %%. Bu kod örneklerinde kullanılan olan iki komut vardır.

* **%% yerel** belirtilen sonraki satırların hello kodda yerel olarak yürütülür. Kod geçerli Python kodu olmalıdır.
* **%% sql -o<variable name>** 
* Merhaba sqlContext bir Hive sorgusu yürütür. Merhaba -o parametre aktarılırsa hello hello sorgunun sonucu hello kalıcı %% Pandas dataframe olarak yerel Python bağlamı.

Hello tekrar Jupyter not defterlerini ve önceden tanımlanmış hello hakkında daha fazla bilgi "magics için" sağladıkları, bkz: [Jupyter not defterlerinde kullanılabilen çekirdekler Hdınsight Spark Linux kümeleri Hdınsight'ta](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="ingest-data-and-create-a-cleaned-data-frame"></a>Veri alma ve Temizlenen veri çerçeve oluşturma
Bu bölümde bir dizi görevleri gerekli tooingest hello veri toobe skoru hello kodunu içerir. Bir birleştirilmiş % 0,1 örnek dosyasının (.tsv dosyası olarak depolanır) hello ücreti seyahat ve ücreti biçiminde hello verileri okuma ve ardından temiz veri çerçevesi oluşturur.

Merhaba ücreti seyahat ve ücreti dosyaları alanına göre sağlanan hello yordamı: [takım veri bilimi işlemi eylemde hello: Hdınsight Hadoop kümeleri kullanarak](machine-learning-data-science-process-hive-walkthrough.md) konu.

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

**ÇIKTI:**

Hücre tooexecute geçen süre: 46.37 saniye

## <a name="prepare-data-for-scoring-in-spark"></a>Spark Puanlama için verileri hazırlama
Bu bölümde, nasıl tooindex, kodlama ve kendileri için sınıflandırma ve regresyon Mllib'i denetimli öğrenme algoritmalara kullanın kategorik özellikleri tooprepare ölçeği gösterir.

### <a name="feature-transformation-index-and-encode-categorical-features-for-input-into-models-for-scoring"></a>Özellik dönüşümü: dizin ve puanlama modelleri giriş için kategorik özellikleri kodlama
Bu bölümde gösterilmiştir nasıl tooindex kategorik verileri kullanarak bir `StringIndexer` ve özelliklerle kodlamak `OneHotEncoder` hello modellerini giriş.

Merhaba [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) bir dize sütunu etiketlerini tooa sütununun etiket dizinlerini kodlar. Merhaba dizinlerini etiket sıklıklarını göre sıralanır. 

Merhaba [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) sütununun etiket dizinlerini tooa ikili vektörler, en çok bir değerle tek bir-bir sütun eşler. Bu kodlama Lojistik regresyon gibi sürekli değerli özellikleri beklediğiniz algoritmalarına olanak uygulanan toobe toocategorical özellikleri.

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

**ÇIKTI:**

Hücre tooexecute geçen süre: 5.37 saniye

### <a name="create-rdd-objects-with-feature-arrays-for-input-into-models"></a>Özellik dizisi modelleri giriş için olan RDD nesneleri oluşturma
Bu bölüm, nasıl bir RDD olarak tooindex kategorik metin veri nesnesi ve kullanılan tootrain ve test Mllib'i Lojistik regresyon ve ağaç tabanlı modelleri olamaz bir hot kodlamak gösteren kod içerir. Merhaba dizinlenmiş veri depolanan [dayanıklı Dağıtılmış veri kümesi (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) nesneleri. Merhaba temel soyutlama Spark bunlar. RDD nesne üzerinde Spark ile paralel işletilen öğe değişmez, bölümlenmiş bir koleksiyonunu temsil eder.

Ayrıca nasıl tooscale verilerle hello gösteren kodu içerir `StandardScalar` doğrusal regresyon ile Stokastik gradyan düşüşü (SGD), machine learning modellerini çeşitli eğitim için yaygın olarak kullanılan bir algoritma kullanmak için Mllib'i tarafından sağlanan. Merhaba [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) kullanılan tooscale hello özellikleri toounit farkı değil. Özellik ölçeklendirme, veri normalleştirme da bilinen, yaygın olarak yapılan değerlerle özellikleri olan belirli bir aşırı tartmanız olduğunu hello hedefi işlevinde oluşturmasını sağlar. 

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

**ÇIKTI:**

Hücre tooexecute geçen süre: 11.72 saniye

## <a name="score-with-hello-logistic-regression-model-and-save-output-tooblob"></a>Merhaba ile Lojistik regresyon modeli Puanlama ve çıktı tooblob Kaydet
Bu bölümdeki Hello kodu nasıl tooload Azure'da kaydedilmiş bir Lojistik regresyon modeli blob depolamaya ve ücreti seyahat üzerinde bir ipucu desteklemediğini Ücretli toopredict kullanın, standart sınıflandırma Ölçümleriyle puan ve kaydedin gösterir ve hello sonuçları tooblob çizmek depolama alanı. sonuçları skoru hello RDD nesneleri depolanır. 

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

**ÇIKTI:**

Hücre tooexecute geçen süre: 19.22 saniye

## <a name="score-a-linear-regression-model"></a>Doğrusal regresyon modeli Puanlama
Kullandık [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) tootrain Itanium tabanlı sistemler için en iyi duruma getirme toopredict hello tutar ucunun için Stokastik gradyan düşüşü (SGD) kullanarak bir doğrusal regresyon modeli Ücretli. 

Bu bölümdeki Hello kod nasıl tooload bir doğrusal regresyon modeli Azure blob depolama biriminden ölçeklendirilmiş değişkenler kullanarak Puanlama ve hello sonuçları geri toohello blob kaydedin gösterir.

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


**ÇIKTI:**

Hücre tooexecute geçen süre: 16.63 saniye

## <a name="score-classification-and-regression-random-forest-models"></a>Sınıflandırma ve regresyon rastgele orman modeli Puanlama
Bu bölümdeki Hello kod tooload hello sınıflandırma kaydedilme gösterir ve regresyon rastgele orman Azure blob depolama alanına kaydedildi modelleri standart sınıflandırıcı ve regresyon ölçüleri kendi performansını Puanlama ve hello sonuçları geri tooblob depolama kaydedin.

[Rastgele ormanlar](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) karar ağaçları ensembles şunlardır.  Bunlar, birçok karar ağaçları tooreduce hello riskini overfitting birleştirin. Rastgele ormanlar kategorik özellikleri işleyebilir toohello çok sınıflı sınıflandırma ayarı genişletmek, özellik ölçeklendirme gerektirmez ve mümkün toocapture sapmalar olan ve etkileşimleri özellik. Rastgele ormanlar hello en başarılı machine learning modellerini sınıflandırma ve regresyon biridir.

[Spark.mllib](http://spark.apache.org/mllib/) ve sürekli ve kategorik özelliklerini kullanarak regresyon, çok sınıflı ve ikili sınıflandırma için rastgele ormanlar destekler. 

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

**ÇIKTI:**

Hücre tooexecute geçen süre: 31.07 saniye

## <a name="score-classification-and-regression-gradient-boosting-tree-models"></a>Sınıflandırma ve regresyon gradyan artırmanın ağaç modeli Puanlama
Bu bölümdeki Hello kod nasıl tooload sınıflandırma ve Azure blob depolama biriminden regresyon gradyan artırmanın ağaç modelleri standart sınıflandırıcı ve regresyon ölçüleri kendi performansını Puanlama ve hello sonuçları geri tooblob depolama Kaydet gösterir. 

**Spark.mllib** GBTs ikili sınıflandırma ve regresyon, sürekli ve kategorik özelliklerini kullanmayı destekler. 

[Gradyan artırmanın ağaçları](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) olan karar ağaçları ensembles. GBTs tren karar tekrarlayarak toominimize kaybı işlevi ağaçları. GBTs kategorik özellikleri işleyebilir, özellik ölçeklendirme gerektirmez ve mümkün toocapture sapmalar olan ve etkileşimleri özellik. Bir sınıflandırma veya çoklu sınıflar ayarında de kullanılabilir.

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

**ÇIKTI:**

Hücre tooexecute geçen süre: 14.6 saniye

## <a name="clean-up-objects-from-memory-and-print-scored-file-locations"></a>Nesneleri bellekten temizlemek ve puanlanmış dosya konumları yazdırma
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


**ÇIKTI:**

logisticRegFileLoc: LogisticRegressionWithLBFGS_2016 05 0317_22_38.953814.txt

linearRegFileLoc: LinearRegressionWithSGD_2016 05 0317_22_58.878949

randomForestClassificationFileLoc: RandomForestClassification_2016 05 0317_23_15.939247.txt

randomForestRegFileLoc: RandomForestRegression_2016 05 0317_23_31.459140.txt

BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt

BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt

## <a name="consume-spark-models-through-a-web-interface"></a>Bir web arabirimi üzerinden Spark modelleri kullanma
Spark tooremotely gönderme toplu işleri bir mekanizma sağlar veya Livy adlı bir bileşen bir REST aracılığıyla etkileşimli sorgular arabirim. Livy Hdınsight Spark kümenizin üzerinde varsayılan olarak etkindir. Livy hakkında daha fazla bilgi için bkz: [uzaktan Livy kullanarak Spark gönderme işleri](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md). 

Tooremotely bir Azure blob depolanır ve hello sonuçları tooanother blob yazan bir dosya puanları toplu iş gönderme Livy kullanabilirsiniz. toodo bunu hello Python komut dosyasını karşıya yükle  
[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) toohello blob hello Spark kümesi. Gibi bir araç kullanabilirsiniz **Microsoft Azure Storage Gezgini** veya **AzCopy** toocopy hello betik toohello küme blob. Örneğimizde biz hello betik çok karşıya***wasb:///example/python/ConsumeGBNYCReg.py***.   

> [!NOTE]
> hello Spark kümesi ile ilişkili hello depolama hesabı için hello portalı bulunabilir erişim tuşları hello. 
> 
> 

Toothis konumu karşıya sonra dağıtılmış bir bağlamda hello Spark kümesinde bu komut dosyasını çalıştırır. Merhaba modelini yükler ve giriş dosyaları hello modeline dayalı Öngörüler çalışır.  

Basit bir HTTPS/REST istek üzerinde Livy yaparak, bu komut dosyası uzaktan çağırabilirsiniz.  İşte uzaktan bir curl komutunu tooconstruct hello HTTP isteği tooinvoke hello Python komut dosyası. CLUSTERLOGIN, CLUSTERPASSWORD, CLUSTERNAME Spark kümenizin hello uygun değerlerle değiştirin.

    # CURL COMMAND tooINVOKE PYTHON SCRIPT WITH HTTP REQUEST

    curl -k --user "CLUSTERLOGIN:CLUSTERPASSWORD" -X POST --data "{\"file\": \"wasb:///example/python/ConsumeGBNYCReg.py\"}" -H "Content-Type: application/json" https://CLUSTERNAME.azurehdinsight.net/livy/batches

Temel kimlik doğrulaması ile basit bir HTTPS çağrı yaparak hello uzak sistem tooinvoke hello Spark iş Livy aracılığıyla üzerinde herhangi bir dil kullanabilirsiniz.   

> [!NOTE]
> Bu HTTP arama yaparken bu kullanışlı toouse hello Python istekleri kitaplığı olacaktır, ancak şu anda Azure işlevlerinde varsayılan olarak yüklü değildir. Bu nedenle eski HTTP kitaplıkları onun yerine kullanılır.   
> 
> 

Merhaba Python kodu hello HTTP çağrısı şöyledir:

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


Bu Python kodu çok ekleyebilirsiniz[Azure işlevleri](https://azure.microsoft.com/documentation/services/functions/) tootrigger blob puanlar bir Spark iş gönderme Zamanlayıcı, oluşturma veya güncelleştirme bir BLOB gibi çeşitli olayları temel. 

Kod boş istemci deneyimini tercih ederseniz, hello kullan [Azure Logic Apps](https://azure.microsoft.com/documentation/services/app-service/logic/) tooinvoke hello Spark toplu hello üzerinde bir HTTP eylemi tanımlayarak Puanlama **Logic Apps Tasarımcısı** ve parametrelerini ayarlama. 

* Azure portalından seçerek yeni bir mantıksal uygulama oluşturma **+ yeni** -> **Web + mobil** -> **mantıksal uygulama**. 
* Merhaba yukarı toobring **Logic Apps Tasarımcısı**, hello hello mantıksal uygulama adını ve uygulama hizmeti planı girin.
* Bir HTTP eylem seçin ve aşağıdaki şekilde hello gösterilen hello parametreleri girin:

![Logic Apps Tasarımcısı](./media/machine-learning-data-science-spark-model-consumption/spark-logica-app-client.png)

## <a name="whats-next"></a>Sırada ne var?
**Çapraz doğrulama ve hyperparameter Süpürme**: bkz [veri keşfi ve modelleme Spark ile Gelişmiş](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) modelleri nasıl olabilir üzerinde çapraz doğrulama ve parametre hyper Süpürme kullanılarak eğitilmiş.

