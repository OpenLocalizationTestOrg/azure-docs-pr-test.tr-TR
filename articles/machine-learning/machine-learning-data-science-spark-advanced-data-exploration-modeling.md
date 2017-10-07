---
title: "aaaAdvanced veri keşfi ve Spark ile modelleme | Microsoft Docs"
description: "Çapraz doğrulama ve hyperparameter en iyi duruma getirme kullanarak ikili sınıflandırma ve regresyon modeli eğitmek ve Hdınsight Spark toodo veri keşfi kullanın."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f90d9a80-4eaf-437b-a914-23514390cd60
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: 055c342857fd732633cec9810de69cee61db973d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-data-exploration-and-modeling-with-spark"></a>Spark ile gelişmiş veri keşfi ve modelleme
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

Bu kılavuzda Hdınsight Spark toodo veri keşfi ve tren ikili sınıflandırma ve çapraz doğrulama kullanarak regresyon modeli kullanır ve hyperparameter en iyi duruma getirilmesi bir örneği hello NYC Seyahat Ücreti 2013 dataset masrafları. Merhaba hello adımlarda size yol gösterir [veri bilimi işlemi](http://aka.ms/datascienceprocess)için Hdınsight Spark kullanarak uçtan, küme için işleme ve Azure BLOB'ların toostore hello veri ve hello modeller. Hello işlem bir Azure Storage Blobundan getirildi veri visualizes inceler ve ardından hello veri toobuild Tahmine dayalı modelleri hazırlar. Python kullanılan toocode hello çözümü ve tooshow hello ilgili çizimleri olmuştur. Bu modeller hello Spark Mllib'i Araç Seti toodo ikili sınıflandırma ve görevleri modelleme regresyon kullanarak derlemesi ' dir. 

* Merhaba **ikili sınıflandırma** görev gerekmediğini toopredict hello seyahat için ücretli bir ipucu. 
* Merhaba **regresyon** toopredict hello diğer ipucu özelliklerini temel alarak hello ipucu miktarını bir görevdir. 

Merhaba modelleme adımları ayrıca nasıl tootrain, değerlendirmek ve her türde bir model Kaydet gösteren kod içerir. Merhaba konu aynı yerde hello hello bazıları kapsar [veri keşfi ve modelleme Spark ile](machine-learning-data-science-spark-data-exploration-modeling.md) konu. Ancak "de en iyi şekilde doğru sınıflandırma ve regresyon modeli tootrain yerleştirmez hyperparameter ile çapraz doğrulama kullandığından, daha gelişmiş". 

**Çapraz doğrulama (MS)** ne kadar iyi bilinen bir veri kümesi üzerinde eğitilmiş model üzerinde eğitilmedi veri kümeleri toopredicting hello özelliklerini genelleştirir değerlendirir bir tekniktir.  Burada kullanılan yaygın olarak görülen bir uygulama toodivide K Katlama içine bir veri kümesidir ve bir hepsini şekilde hello Katlama biri dışındaki tüm hello modeli eğitmek. Merhaba bağımsız veri kümesi bu kullanılmayan Katlama tootrain hello modelde karşı doğru bir şekilde test edildiğinde hello modeli tooprediction Hello yeteneklerini uygunluk.

**Hyperparameter iyileştirme** kümesiyle bir ölçü bağımsız bir veri kümesi üzerinde hello algoritması'nın performansını en iyi duruma getirme genellikle hello amacı hyperparameters bir öğrenme algoritması seçme hello sorunudur. **Hyperparameters** hello model eğitim yordamı dışında belirtilmelidir değerlerdir. Bu değerler hakkında varsayımlar hello esneklik ve hello modelleri doğruluğunu etkileyebilir. Karar ağaçları gibi Hello derinliği ve hello ağacında bırakır sayısı istenen hyperparameters, örneğin, sahip. Destek vektör makinelerin (SVMs) misclassification cezası terim ayarlanması gerekir. 

Burada kullanılan bir ortak yolu tooperform hyperparameter iyileştirme bir kılavuz arama değil veya **parametresi tarama**. Bu ayrıntılı aramasını hello değerleri aracılığıyla hello hyperparameter alanı belirtilen bir alt bir öğrenme algoritması kümeleri oluşur. Çapraz doğrulama performans ölçüm toosort hello kılavuz arama algoritması tarafından üretilen hello verimle çıkışı sağlayabilir. MS hello modeli korur hello kapasite tooapply toohello genel hangi hello eğitim verileri ayıklandı veri kümesi bir model tootraining verileri overfitting gibi sınırı sorunları hyperparameter sakınımlı yardımcı ile kullanılır.

Merhaba modelleri kullanırız Lojistik ve doğrusal regresyon, rastgele ormanları ve gradyan boosted ağaçları şunlardır:

* [Doğrusal regresyon SGD ile](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) Stokastik gradyan düşüşü (SGD) yöntemini kullanan doğrusal regresyon modeli ve en iyi duruma getirme ve özellik için toopredict hello ipucu tutarlar ölçeklendirme Ücretli. 
* [LBFGS ile Lojistik regresyon](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) veya "logit" regresyon hello bağımlı değişken kategorik toodo veri sınıflandırması olduğunda kullanılabilen bir regresyon modeli. LBFGS sınırlı bir bilgisayarın bellek miktarını kullanarak hello Broyden – Fletcher'dan – Goldfarb – Shanno (BFGS) algoritması benzeyen ve machine learning'de yaygın olarak kullanılan bir yarı-Newton iyileştirme algoritması ' dir.
* [Rastgele ormanlar](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) karar ağaçları ensembles şunlardır.  Bunlar, birçok karar ağaçları tooreduce hello riskini overfitting birleştirin. Rastgele ormanlar regresyon ve sınıflandırma için kullanılır ve kategorik özellikleri işleyebilir ve toohello çok sınıflı sınıflandırma ayarı genişletilebilir. Bunlar, özellik ölçekleme ve bu mümkün toocapture sapmalar ve özellik etkileşimleri gerektirmez. Rastgele ormanlar hello en başarılı machine learning modellerini sınıflandırma ve regresyon biridir.
* [Gradyan boosted ağaçları](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) olan karar ağaçları ensembles. GBTs tren karar tekrarlayarak toominimize kaybı işlevi ağaçları. GBTs regresyon ve sınıflandırma için kullanılır ve kategorik özellikleri işleyebilir, özellik ölçeklendirme gerektirmez ve mümkün toocapture sapmalar ve etkileşimleri özellik. Bir sınıflandırma veya çoklu sınıflar ayarında de kullanılabilir.

MS ve Hyperparameter kullanan örnekler modelleme tarama gösterildiğinden hello ikili sınıflandırma sorunu için. Daha basit örnekler (olmadan parametre dağılımlarında) regresyon görevleri için ana konudaki hello sunulur. Ancak hello ekte esnek net doğrusal regresyon ve MS için parametre tarama için rastgele orman regresyon ile kullanarak doğrulama da sunulur. Merhaba **esnek net** regularized regresyon yöntemi doğrusal regresyon sığdırma, doğrusal olarak modeller için birleştirir hello L1 ve L2 ölçümleri hello cezaları olan [Serbest Şekil](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) ve [ridge](https://en.wikipedia.org/wiki/Tikhonov_regularization) yöntemleri.   

> [!NOTE]
> Merhaba Spark Mllib'i Araç Seti büyük veri kümeleri üzerinde tasarlanmış toowork olsa da, nispeten küçük bir örnek (yaklaşık 30 170 K satır, yaklaşık hello özgün NYC dataset %0,1 kullanarak Mb) burada kolaylık sağlamak için kullanılır. burada verilen hello alıştırma verimli bir şekilde (yaklaşık 10 dakika cinsinden) 2 çalışan düğümleri ile bir Hdınsight kümesi üzerinde çalışır. Merhaba küçük değişiklikler içeren aynı kodu kullanılan tooprocess daha büyük veri-kümeleriyle, verileri bellekte önbelleğe alma ve hello küme boyutunu değiştirmek için uygun değişiklikleri olabilir.
> 
> 

## <a name="setup-spark-clusters-and-notebooks"></a>Kurulum: Spark kümeleri ve dizüstü bilgisayarlar
Kurulum adımlarını ve kod bu kılavuzda bir Hdınsight Spark 1.6 kullanmak için sağlanır. Ancak Jupyter not defterleri Hdınsight Spark 1.6 ve Spark 2.0 kümeleri için sağlanır. Merhaba not defterlerini ve bağlantıları toothem açıklamasını hello sağlanan [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) bunları içeren hello GitHub depo. Ayrıca, hello kod burada ve bağlı hello not defterlerini geneldir ve tüm Spark kümesi üzerinde çalışması gerekir. Hdınsight Spark kullanmıyorsanız hello Küme kurulumu ve Yönetimi adımları ne burada gösterilenden biraz farklı olabilir. Kolaylık olması için Spark 1.6 ve 2.0 toobe hello pyspark Çekirdeği'nde hello Jupyter not defteri sunucu, çalıştırmak için hello bağlantılar toohello Jupyter not defterleri şunlardır:

### <a name="spark-16-notebooks"></a>Spark 1.6 dizüstü bilgisayarlar

[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): Not Defteri #1 ve hyperparameter ayarlama ve çapraz doğrulama kullanarak modeli geliştirme konuları içerir.

### <a name="spark-20-notebooks"></a>Spark 2.0 dizüstü bilgisayarlar

[Spark2.0-pySpark3-Machine-Learning-Data-Science-Spark-Advanced-Data-exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): Bu dosyayı nasıl tooperform veri keşfi, model oluşturma ve Spark 2. 0'Puanlama kümeleri hakkında bilgi sağlar.

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a>Kurulumu: Spark bağlam depolama konumları, kitaplıklar ve hello hazır
Spark mümkün tooread ve yazma tooAzure depolama blobu (WASB olarak da bilinir) olur. Bu nedenle depolanan mevcut verilerinizi Spark kullanarak işlenebilir ve depolanan yeniden WASB hello sonuçlanır.

toosave modelleri veya WASB dosyalarında, hello yolu düzgün belirtilen toobe gerekir. Merhaba varsayılan kapsayıcı bağlı toohello Spark kümesi ile başlayan bir yol kullanarak başvurulabilir: "wasb: / / /". Başka konumlara tarafından başvurulan "wasb: / /".

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a>Dizin yolları için depolama konumları WASB ayarlayın
Hello aşağıdaki kod örneği hello konumunu okuma hello veri toobe belirtir ve hello modeli depolama dizini toowhich hello modeli çıktı hello yolu kaydedilir:

    # SET PATHS tooFILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";


    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";

    # PRINT START TIME
    import datetime
    datetime.datetime.now()

**ÇIKTI**

DateTime.DateTime (2016, 4, 18, 17, 36, 27, 832799)

### <a name="import-libraries"></a>Kitaplıkları içeri aktarma
Gerekli kitaplıkları ile koddan hello içeri aktarın:

    # LOAD PYSPARK LIBRARIES
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
Jupyter not defterleri ile sağlanan hello PySpark tekrar önceden belirlenmiş bir içerik var. Geliştirdiğiniz Merhaba uygulaması ile çalışmaya başlamadan önce bu nedenle, tooset hello Spark veya Hive bağlamları açıkça gerekmez. Bu içerikler varsayılan olarak sizin için kullanılabilir. Bu içerikler şunlardır:

* SC - Spark 
* sqlContext - Hive için

Merhaba PySpark çekirdeği bazı önceden tanımlanmış "sihirleri" ile çağırabilir özel komutlar olduğu sağlar %%. Bu kod örneklerinde kullanılan olan iki komut vardır.

* **%% yerel** sonraki satırların hello kodda yerel olarak yürütülen toobe olduğunu belirtir. Kod geçerli Python kodu olmalıdır.
* **%% sql -o <variable name>**  hello sqlContext bir Hive sorgusu yürütür. Merhaba -o parametre aktarılırsa hello hello sorgunun sonucu hello kalıcı %% Pandas DataFrame olarak yerel Python bağlamı.

Hello tekrar Jupyter not defterlerini ve önceden tanımlanmış hello hakkında daha fazla bilgi "magics için" sağladıkları, bkz: [Jupyter not defterlerinde kullanılabilen çekirdekler Hdınsight Spark Linux kümeleri Hdınsight'ta](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="data-ingestion-from-public-blob"></a>Veri alımı ortak blob gelen:
Merhaba ilk hello veri bilimi işlemi tooingest hello veri toobe veri keşfi ve modelleme ortamınıza bulunduğu kaynaklardan analiz adımdır. Bu Spark bu kılavuzda ortamıdır. Bu bölümde hello kod toocomplete bir dizi görev içerir:

* Merhaba veri örnek toobe Modellenen alma
* (.tsv dosyası olarak depolanır) hello girdi veri kümesi okuyun
* Biçim ve temiz hello verileri
* oluşturma ve nesneleri (RDDs veya veri çerçevelerini) bellekte önbelleğe alma
* SQL bağlam tabloda geçici olarak kaydeder.

Veri alımı için hello kod aşağıdadır.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_train_file = sc.textFile(taxi_train_file_loc)

    # GET SCHEMA OF hello FILE FROM HEADER
    schema_string = taxi_train_file.first()
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

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_header = taxi_train_file.filter(lambda l: "medallion" in l)
    taxi_temp = taxi_train_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))


    # CREATE DATA FRAME
    taxi_train_df = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    # CREATE A CLEANED DATA-FRAME BY DROPPING SOME UN-NECESSARY COLUMNS & FILTERING FOR UNDESIRED VALUES OR OUTLIERS
    taxi_df_train_cleaned = taxi_train_df.drop('medallion').drop('hack_license').drop('store_and_fwd_flag').drop('pickup_datetime')\
        .drop('dropoff_datetime').drop('pickup_longitude').drop('pickup_latitude').drop('dropoff_latitude')\
        .drop('dropoff_longitude').drop('tip_class').drop('total_amount').drop('tolls_amount').drop('mta_tax')\
        .drop('direct_distance').drop('surcharge')\
        .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200" )

    # CACHE & MATERIALIZE DATA-FRAME IN MEMORY. GOING THROUGH AND COUNTING NUMBER OF ROWS MATERIALIZES hello DATA-FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**ÇIKTI**

Hücre tooexecute geçen süre: 276.62 saniye

## <a name="data-exploration--visualization"></a>Veri keşfi & Görselleştirme
Hello veri Spark alındıktan sonra hello sonraki hello veri bilimi işlemi hello veri keşfi ve görselleştirme aracılığıyla daha derin anlayış toogain adımdır. Bu bölümde, SQL sorguları ve çizim hello hedef değişkenleri ve olası özellikleri için görsel denetleme kullanarak hello ücreti verileri inceleyeceğiz. Özellikle, yolcu sayıları ücreti dönüşleri, ipucu tutarlar hello sıklığını ve nasıl ipuçları ödeme tutar ve türüne göre farklılık hello sıklığını çizmek.

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a>Histogram yolcu sayısı frekansların ücreti dönüşleri hello örnekteki Çiz
Bu kodu ve sonraki parçacıkları SQL Sihirli tooquery hello örnek ve yerel Sihirli tooplot hello verileri kullanın.

* **SQL Sihirli (`%%sql`)** hello Hdınsight PySpark çekirdeği kolay satır içi HiveQL sorguları hello sqlContext karşı destekler. Merhaba (-o deðiþken_adý) bağımsız değişkeni devam ederse hello SQL sorgusu hello çıktısını hello Jupyter sunucuda Pandas DataFrame olarak. Bu, hello yerel modda kullanılabilir olduğu anlamına gelir.
* Merhaba  **`%%local` Sihirli** olan toorun kod hello headnode hello Hdınsight kümesinin olduğu hello Jupyter sunucu üzerinde yerel olarak kullanılan. Genellikle, kullandığınız `%%local` hello sonra Sihirli `%%sql -o` Sihirli olduğu kullanılan toorun bir sorgu. Merhaba -o parametresi yerel olarak hello SQL sorgusu hello çıktısını kalıcı. Ardından hello `%%local` Sihirli Tetikleyicileri hello kod parçacıkları toorun yerel olarak yerel olarak kalıcı hello çıktı hello SQL sorgularının karşı sonraki kümesi. Merhaba kod çalıştırdıktan sonra hello çıkış otomatik olarak görünür.

Bu sorgu hello dönüşleri yolcu sayısına göre alır. 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # SQL QUERY
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts FROM taxi_train WHERE passenger_count > 0 and passenger_count < 7 GROUP BY passenger_count


Bu kod bir yerel veri çerçevesi hello sorgu çıktısı oluşturur ve hello veri çizer. Merhaba `%%local` Sihirli oluşturur çerçeve, yerel veri `sqlResults`, kullanılabileceği ile matplotlib çizdirmek için. 

> [!NOTE]
> Bu PySpark Sihirli birden çok kez bu kılavuzda kullanılır. Merhaba miktarda veri büyükse, toocreate yerel belleğe sığması bir veri-çerçeve örnek.
> 
> 

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

Sayıları tarafından yolcu hello kod tooplot hello dönüşleri İşte

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    # PLOT PASSENGER NUMBER VS TRIP COUNTS
    x_labels = sqlResults['passenger_count'].values
    fig = sqlResults[['trip_counts']].plot(kind='bar', facecolor='lightblue')
    fig.set_xticklabels(x_labels)
    fig.set_title('Counts of trips by passenger count')
    fig.set_xlabel('Passenger count in trips')
    fig.set_ylabel('Trip counts')
    plt.show()

**ÇIKTI**

![Dönüş yolcu sayısına göre sıklığı](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/frequency-of-trips-by-passenger-count.png)

Hello kullanarak birkaç farklı türde görselleştirmeleri (tablo, pasta, çizgi, alan veya çubuğu) arasında seçebilirsiniz **türü** menü düğmelerini hello Not. Merhaba çubuğu çizim burada gösterilir.

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a>Çizim histogram ipucu tutarlar ve nasıl ipucu tutar yolcu sayısı ve ücreti tutarlar göre değişir.
Bir SQL sorgusu toosample verileri kullanmak...

    # SQL SQUERY
    %%sql -q -o sqlResults
        SELECT fare_amount, passenger_count, tip_amount, tipped
        FROM taxi_train 
        WHERE passenger_count > 0 
        AND passenger_count < 7
        AND fare_amount > 0 
        AND fare_amount < 200
        AND payment_type in ('CSH', 'CRD')
        AND tip_amount > 0 
        AND tip_amount < 25


Bu kod hücresini hello SQL sorgu toocreate üç çizimleri hello verileri kullanır.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline

    # TIP BY PAYMENT TYPE AND PASSENGER COUNT
    ax1 = resultsPDDF[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # TIP BY PASSENGER COUNT
    ax2 = resultsPDDF.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount ($) by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # TIP AMOUNT BY FARE AMOUNT, POINTS ARE SCALED BY PASSENGER COUNT
    ax = resultsPDDF.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(resultsPDDF.passenger_count))
    ax.set_title('Tip amount by Fare amount ($)')
    ax.set_xlabel('Fare Amount')
    ax.set_ylabel('Tip Amount')
    plt.axis([-2, 120, -2, 30])
    plt.show()


**ÇIKTI:** 

![İpucu tutar dağıtımı](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-distribution.png)

![Yolcu sayısına göre ipucu tutar](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Tutarı Tutar ücreti tarafından İpucu](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a>Modelleme mühendislik, dönüştürme ve veri hazırlığı özelliği
Bu bölümde açıklar ve ML modelleme kullanmak için tooprepare veri hello kod yordamları için kullanılan sağlar. Bunu nasıl toodo hello aşağıdaki görevleri gösterir:

* Yeni bir özellik saatleri trafiği zaman depo bölümleme tarafından oluşturma
* Dizin ve üzerinde hot kategorik özellikleri kodlama
* ML işlevleri giriş etiketli noktası nesneleri oluşturma
* Rastgele bir alt örnekleme hello veri oluşturun ve eğitim ve test kümesi olarak bölme
* Ölçeklendirme özelliği
* Bellek önbelleği nesneleri

### <a name="create-a-new-feature-by-partitioning-traffic-times-into-bins"></a>Depo trafiği kez bölümleme tarafından yeni bir özellik oluşturma
Bu kod toocreate trafiği bölümleme tarafından yeni bir özellik depo nasıl zaman ve ardından nasıl toocache hello bellek ortaya çıkan veri çerçevede gösterir. Tooimproved yürütme süresi, önbelleğe alma dayanıklı Dağıtılmış veri kümeleri (RDDs) ve veri çerçevelerini art arda kullanıldığı yol açar. Bu nedenle, biz RDDs ve veri çerçevelerini bu kılavuz çeşitli aşamalarında önbelleğe alır.

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night" 
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush" 
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_train 
    """
    taxi_df_train_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    # hello .COUNT() GOES THROUGH hello ENTIRE DATA-FRAME,
    # MATERIALIZES IT IN MEMORY, AND GIVES hello COUNT OF ROWS.
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()

**ÇIKTI**

126050

### <a name="index-and-one-hot-encode-categorical-features"></a>Dizini oluşturmak ve bir hot kategorik özellikleri kodlama
Bu bölümde gösterilmiştir nasıl tooindex veya İşlevler modelleme hello giriş için kategorik özellikleri kodlayın. Modelleme hello ve Mllib'i işlevlerini kategorik giriş verisi özelliklerle dizine veya kodlanmış dikkat gerektiren tahmin önceki toouse. 

Merhaba modeline bağlı olarak farklı şekillerde kodlamak olmak veya tooindex gerekir. Örneğin, Logistic ve doğrusal regresyon modeli bir hot kodlama, burada gerektirir, örneğin, üç kategoriye sahip bir özellik içeren her 0 veya 1 bir gözlem hello kategorisine bağlı olarak üç özellik sütunlara genişletilebilir. Mllib'i sağlar [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) bir hot toodo kodlama işlev. Bu Kodlayıcı sütununun etiket dizinlerini tooa ikili vektörler, en çok bir değerle tek bir-bir sütun eşler. Bu kodlama Lojistik regresyon gibi sayısal değerli özellikleri beklediğiniz algoritmalarına olanak uygulanan toobe toocategorical özellikleri.

Kategorik özellikleri kodlanacağını ve kod tooindex hello şöyledir:

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer

    # INDEX AND ENCODE VENDOR_ID
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_train_with_newFeatures) # Input data-frame is hello cleaned one from above
    indexed = model.transform(taxi_df_train_with_newFeatures)
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

    # INDEX AND TRAFFIC TIME BINS
    stringIndexer = StringIndexer(inputCol="TrafficTimeBins", outputCol="TrafficTimeBinsIndex")
    model = stringIndexer.fit(encoded3)
    indexed = model.transform(encoded3)
    encoder = OneHotEncoder(dropLast=False, inputCol="TrafficTimeBinsIndex", outputCol="TrafficTimeBinsVec")
    encodedFinal = encoder.transform(indexed)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**ÇIKTI**

Hücre tooexecute geçen süre: 3.14 saniye

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a>ML işlevleri giriş etiketli noktası nesneleri oluşturma
Bu bölüm, etiketlenmiş noktası veri olarak tooindex kategorik metin veri türü nasıl ve ne gösteren kod içerir tooencode onu. Bu, kullanılan toobe tootrain ve test Mllib'i Lojistik regresyon ve diğer sınıflandırma modelleri hazırlar. Etiketli noktası, esnek Dağıtılmış veri kümeleri (RDD) girdi verisi olarak Mllib'i ML algoritmalara çoğu tarafından gerektiği şekilde biçimlendirilmiş nesneleridir. A [noktası etiketli](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) yerel bir vektör, yoğun veya seyrek, etiket/yanıt ile ilişkilidir.

İşte kod tooindex hello ve ikili sınıflandırma için metin özellikleri kodlayın.

    # FUNCTIONS FOR BINARY CLASSIFICATION

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.pickup_hour, line.weekday,
                             line.passenger_count, line.trip_time_in_secs, line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tipped, features)
        return  labPt

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                   line.vendorVec.toArray(), line.rateVec.toArray(), line.paymentVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tipped, features)
        return  labPt


Doğrusal regresyon çözümlemesi için tooencode ve dizin kategorik metin özelliklerinden hello kod aşağıdadır.

    # FUNCTIONS FOR REGRESSION WITH TIP AMOUNT AS TARGET VARIABLE

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingRegression(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex, 
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO LINEAR REGRESSION MODELS
    def parseRowOneHotRegression(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt


### <a name="create-a-random-sub-sampling-of-hello-data-and-split-it-into-training-and-testing-sets"></a>Rastgele bir alt örnekleme hello veri oluşturun ve eğitim ve test kümesi olarak bölme
Bu kod bir rastgele örnekleme (% 25 burada kullanılır) hello veri oluşturur. Bu örneğin hello kümesinin toohello boyutu nedeniyle gerekli olmamasına karşın, burada hello verileri nasıl örnek gösterilmektedir. Bildiğiniz sonra nasıl toouse gerekirse kendi sorunu için. Örnekleri büyük olduğunda bu eğitim modelleri sırasında önemli zamandan tasarruf edebilirsiniz. Sonraki biz hello örnek eğitim bölümü (burada %75) ve bir test bölümü (% 25 burada) toouse sınıflandırma ve regresyon modelleme bölün.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    from pyspark.sql.functions import rand

    samplingFraction = 0.25;
    trainingFraction = 0.75; testingFraction = (1-trainingFraction);
    seed = 1234;
    encodedFinalSampled = encodedFinal.sample(False, samplingFraction, seed=seed)

    # SPLIT SAMPLED DATA-FRAME INTO TRAIN/TEST, WITH A RANDOM COLUMN ADDED FOR DOING CV (SHOWN LATER)
    # INCLUDE RAND COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    dfTmpRand = encodedFinalSampled.select("*", rand(0).alias("rand"));
    trainData, testData = dfTmpRand.randomSplit([trainingFraction, testingFraction], seed=seed);

    # CACHE TRAIN AND TEST DATA
    trainData.cache()
    testData.cache()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary = trainData.map(parseRowIndexingBinary)
    indexedTESTbinary = testData.map(parseRowIndexingBinary)
    oneHotTRAINbinary = trainData.map(parseRowOneHotBinary)
    oneHotTESTbinary = testData.map(parseRowOneHotBinary)

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg = trainData.map(parseRowIndexingRegression)
    indexedTESTreg = testData.map(parseRowIndexingRegression)
    oneHotTRAINreg = trainData.map(parseRowOneHotRegression)
    oneHotTESTreg = testData.map(parseRowOneHotRegression)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**ÇIKTI**

Hücre tooexecute geçen süre: 0.31 saniye

### <a name="feature-scaling"></a>Ölçeklendirme özelliği
Özellik ölçeklendirme, veri normalleştirme da bilinen, yaygın olarak yapılan değerlerle özellikleri olan belirli bir aşırı tartmanız olduğunu hello hedefi işlevinde oluşturmasını sağlar. Merhaba özelliği ölçeklendirmeye yönelik kodu kullanan hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello özellikleri toounit farkı. Doğrusal regresyon ile Stokastik gradyan düşüşü (SGD) kullanmak için Mllib'i tarafından sağlanır. SGD diğer machine learning modellerini regularized gerileme veya destek vektör makineler (SVM) gibi çeşitli eğitim için yaygın olarak kullanılan bir algoritmadır.   

> [!TIP]
> Merhaba LinearRegressionWithSGD algoritması toobe hassas toofeature ölçeklendirme bulduk.   
> 
> 

Merhaba kod tooscale değişkenlerinin regularized hello doğrusal SGD algoritması ile kullanmak için aşağıda verilmiştir.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from pyspark.mllib.linalg import Vectors
    from pyspark.mllib.feature import StandardScaler, StandardScalerModel
    from pyspark.mllib.util import MLUtils

    # SCALE VARIABLES FOR REGULARIZED LINEAR SGD ALGORITHM
    label = oneHotTRAINreg.map(lambda x: x.label)
    features = oneHotTRAINreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTRAINregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    label = oneHotTESTreg.map(lambda x: x.label)
    features = oneHotTESTreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTESTregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**ÇIKTI**

Hücre tooexecute geçen süre: 11.67 saniye

### <a name="cache-objects-in-memory"></a>Bellek önbelleği nesneleri
Eğitim ve ML algoritmalardan sınamak için harcanan hello süre nesneleri için sınıflandırma, regresyon kullanılan ve özellikleri ölçeklendirilmiş hello giriş verisi çerçeve önbelleğe alarak azaltılabilir.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.cache()
    indexedTESTbinary.cache()
    oneHotTRAINbinary.cache()
    oneHotTESTbinary.cache()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.cache()
    indexedTESTreg.cache()
    oneHotTRAINreg.cache()
    oneHotTESTreg.cache()

    # SCALED FEATURES
    oneHotTRAINregScaled.cache()
    oneHotTESTregScaled.cache()

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**ÇIKTI** 

Hücre tooexecute geçen süre: 0,13 saniye

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a>Bir ipucu ile ikili sınıflandırma modelleri Ücretli olsun veya olmasın tahmin etme
Bu bölümde, bir ipucu ücreti seyahat için ücretli olup olmadığına bakılmaksızın kullanım üç tahmin etmeye hello ikili sınıflandırma görevi için nasıl modeller gösterir. sunulan hello model şunlardır:

* Lojistik regresyon 
* Rastgele orman
* Gradyan artırma ağaçları

Her model kod bölümünde oluşturma adımları ayrılır: 

1. **Eğitim modeli** bir parametre kümesi ile verileri
2. **Model değerlendirme** ölçümlerle sınama veri kümesi üzerinde
3. **Model kaydetme** gelecekteki tüketimi için blob içinde

Gösteriyoruz nasıl toodo çapraz doğrulama (MS) iki yolla yerleştirmez parametresiyle:

1. Kullanarak **genel** uygulanan tooany algoritması Mllib'i ve tooany parametresinde olabilen özel kod bir algoritma ayarlar. 
2. Hello kullanarak **pySpark CrossValidator ardışık düzen işlevi**. Not CrossValidator Spark 1.5.0 için birkaç sınırlamalara sahiptir: 
   
   * Gelecekteki tüketimi için kaydedilen/kalıcı ardışık düzen modelleri olamaz.
   * Bir modeldeki her parametre için kullanılamaz.
   * Her Mllib'i algoritması için kullanılamaz.

### <a name="generic-cross-validation-and-hyperparameter-sweeping-used-with-hello-logistic-regression-algorithm-for-binary-classification"></a>Doğrulama ve ikili sınıflandırma hello Lojistik regresyon algoritması ile kullanılan hyperparameter Süpürme çapraz genel
Bu bölümdeki Hello kod gösterir nasıl tootrain, değerlendirmek ve lojistik regresyon modeli ile Kaydet [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) tahmin bir ipucu seyahat kümesindeki hello NYC ücreti seyahat ve ücreti ödenen olsun veya olmasın. Merhaba model doğrulama (MS) ve Mllib'i algoritmalara öğrenme Merhaba, uygulanan tooany olabilir özel kod ile uygulanan hyperparameter Süpürme çapraz kullanarak eğitildi.   

> [!NOTE]
> Bu özel MS kod Hello yürütmeyi birkaç dakika sürebilir.
> 
> 

**MS ve hyperparameter Süpürme kullanarak hello Lojistik regresyon modelini eğitme**

    # LOGISTIC REGRESSION CLASSIFICATION WITH CV AND HYPERPARAMETER SWEEPING

    # GET ACCURACY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionWithLBFGS 
    from pyspark.mllib.evaluation import BinaryClassificationMetrics

    # CREATE PARAMETER GRID FOR LOGISTIC REGRESSION PARAMETER SWEEP
    from sklearn.grid_search import ParameterGrid
    grid = [{'regParam': [0.01, 0.1], 'iterations': [5, 10], 'regType': ["l1", "l2"], 'tolerance': [1e-3, 1e-4]}]
    paramGrid = list(ParameterGrid(grid))
    numModels = len(paramGrid)

    # SET NUM FOLDS AND NUM PARAMETER SETS tooSWEEP ON
    nFolds = 3;
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    # BEGIN CV WITH PARAMETER SWEEP
    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create LabeledPoints from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowOneHotBinary)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowOneHotBinary)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            regt = paramGrid[j]['regType']
            regp = paramGrid[j]['regParam']
            iters = paramGrid[j]['iterations']
            tol = paramGrid[j]['tolerance']
            # Train logistic regression model with hypermarameter set
            model = LogisticRegressionWithLBFGS.train(trainCVLabPt, regType=regt, iterations=iters,  
                                                      regParam=regp, tolerance = tol, intercept=True)
            predictionAndLabels = validationLabPt.map(lambda lp: (float(model.predict(lp.features)), lp.label))
            # Use ROC-AUC as accuracy metrics
            validMetrics = BinaryClassificationMetrics(predictionAndLabels)
            metric = validMetrics.areaUnderROC
            metricSum[j] += metric

    avgAcc = metricSum / nFolds;
    bestParam = paramGrid[np.argmax(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    # TRAIN ON FULL TRAIING SET USING BEST PARAMETERS FROM CV/PARAMETER SWEEP
    logitBest = LogisticRegressionWithLBFGS.train(oneHotTRAINbinary, regType=bestParam['regType'], 
                                                  iterations=bestParam['iterations'], 
                                                  regParam=bestParam['regParam'], tolerance = bestParam['tolerance'], 
                                                  intercept=True)


    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitBest.weights))
    print("Intercept: " + str(logitBest.intercept))

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**ÇIKTI**

Katsayısını: [0.0082065285375-0.0223675576104,-0.0183812028036, - 3.48124578069e-05-0.00247646947233,-0.00165897881503, 0.0675394837328,-0.111823113101,-0.324609912762,-0.204549780032,-1.36499216354, 0.591088507921,-0.664263411392,-1.00439726852, 3.46567827545,-3.51025855172,-0.0471341112232,-0.043521833294, 0.000243375810385, 0.054518719222]

Intercept:-0.0111216486893

Hücre tooexecute geçen süre: 14.43 saniye

**Standart ölçümlerle Hello ikili sınıflandırma modelini değerlendir**

Bu bölümdeki Hello kodunu nasıl tooevaluate Lojistik regresyon modeli test verileri-hello ROC eğrisi, bir çizim dahil olmak üzere küme karşı gösterir.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT LIBRARIES
    from sklearn.metrics import roc_curve,auc
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # PREDICT ON TEST DATA WITH BEST/FINAL MODEL
    predictionAndLabels = oneHotTESTbinary.map(lambda lp: (float(logitBest.predict(lp.features)), lp.label))

    # INSTANTIATE METRICS OBJECT
    metrics = BinaryClassificationMetrics(predictionAndLabels)

    # AREA UNDER PRECISION-RECALL CURVE
    print("Area under PR = %s" % metrics.areaUnderPR)

    # AREA UNDER ROC CURVE
    print("Area under ROC = %s" % metrics.areaUnderROC)
    metrics = MulticlassMetrics(predictionAndLabels)

    # OVERALL STATISTICS
    precision = metrics.precision()
    recall = metrics.recall()
    f1Score = metrics.fMeasure()
    print("Summary Stats")
    print("Precision = %s" % precision)
    print("Recall = %s" % recall)
    print("F1 Score = %s" % f1Score)

    # OUTPUT PROBABILITIES AND REGISTER TEMP TABLE
    logitBest.clearThreshold(); # This clears threshold for classification (0.5) and outputs probabilities
    predictionAndLabelsDF = predictionAndLabels.toDF()
    predictionAndLabelsDF.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**ÇIKTI**

PR alanında 0.985336538462 =

ROC alanında 0.983383274312 =

Özet istatistikleri

Duyarlık 0.984174341679 =

Geri çağırma 0.984174341679 =

F1 Puan 0.984174341679 =

Hücre tooexecute geçen süre: 2.67 saniye

**Merhaba ROC eğrisi çizme.**

Merhaba *predictionAndLabelsDF* bir tablo olarak kayıtlı *tmp_results*, hello önceki hücrenin. *tmp_results* kullanılan toodo sorgu ve sonuçları çerçevesine hello sqlResults verileri-çizdirmek için çıktı. Merhaba kod aşağıdadır.

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


İşte, hello kod toomake Öngörüler ve çizim hello ROC eğrisi.

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES                              
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    #PREDICTIONS
    predictions_pddf = sqlResults.rename(columns={'_1': 'probability', '_2': 'label'})
    prob = predictions_pddf["probability"] 
    fpr, tpr, thresholds = roc_curve(predictions_pddf['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT ROC CURVES
    plt.figure(figsize=(5,5))
    plt.plot(fpr, tpr, label='ROC curve (area = %0.2f)' % roc_auc)
    plt.plot([0, 1], [0, 1], 'k--')
    plt.xlim([0.0, 1.0])
    plt.ylim([0.0, 1.05])
    plt.xlabel('False Positive Rate')
    plt.ylabel('True Positive Rate')
    plt.title('ROC Curve')
    plt.legend(loc="lower right")
    plt.show()


**ÇIKTI**

![Lojistik regresyon ROC eğrisi genel yaklaşım için](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/logistic-regression-roc-curve.png)

**Gelecekte kullanım için bir blob modelinde Sürdür**

Bu bölümdeki Hello kodu nasıl toosave hello Lojistik regresyon modeli tüketimi için gösterilir.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    # PERSIST MODEL
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp;
    dirfilename = modelDir + logisticregressionfilename;

    logitBest.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";


**ÇIKTI**

Hücre tooexecute geçen süre: 34.57 saniye

### <a name="use-mllibs-crossvalidator-pipeline-function-with-logistic-regression-elastic-regression-model"></a>Lojistik regresyon (esnek regresyon) modeliyle Mllib'i'nın CrossValidator ardışık düzen işlevini kullanın
Bu bölümdeki Hello kod gösterir nasıl tootrain, değerlendirmek ve lojistik regresyon modeli ile Kaydet [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) tahmin bir ipucu seyahat kümesindeki hello NYC ücreti seyahat ve ücreti ödenen olsun veya olmasın. Çapraz doğrulama (MS) kullanarak Hello modeli eğitildi ve hyperparameter Süpürme ile Merhaba Mllib'i CrossValidator ardışık düzen işlevi için MS parametre tarama ile uygulanan.   

> [!NOTE]
> Bu Mllib'i MS kod Hello yürütmeyi birkaç dakika sürebilir.
> 
> 

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.classification import LogisticRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import BinaryClassificationEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder
    from sklearn.metrics import roc_curve,auc

    # DEFINE ALGORITHM / MODEL
    lr = LogisticRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build()

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=BinaryClassificationEvaluator(),
                        numFolds=3)

    # CONVERT tooDATA-FRAME: THIS DOES NOT RUN ON RDDs
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINbinary, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    ## PREDICT AND EVALUATE ON TEST DATA-SET

    # USE TEST DATASET FOR PREDICTION
    testDataFrame = sqlContext.createDataFrame(oneHotTESTbinary, ["features", "label"])
    test_predictions = cv_model.transform(testDataFrame)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

**ÇIKTI**

Hücre tooexecute geçen süre: 107.98 saniye

**Merhaba ROC eğrisi çizme.**

Merhaba *predictionAndLabelsDF* bir tablo olarak kayıtlı *tmp_results*, hello önceki hücrenin. *tmp_results* kullanılan toodo sorgu ve sonuçları çerçevesine hello sqlResults verileri-çizdirmek için çıktı. Merhaba kod aşağıdadır.

    # QUERY RESULTS
    %%sql -q -o sqlResults
    SELECT label, prediction, probability from tmp_results

Merhaba kod tooplot hello ROC eğrisi aşağıdadır.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES 
    %%local
    from sklearn.metrics import roc_curve,auc

    # ROC CURVE
    prob = [x["values"][1] for x in sqlResults["probability"]]
    fpr, tpr, thresholds = roc_curve(sqlResults['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    #PLOT
    plt.figure(figsize=(5,5))
    plt.plot(fpr, tpr, label='ROC curve (area = %0.2f)' % roc_auc)
    plt.plot([0, 1], [0, 1], 'k--')
    plt.xlim([0.0, 1.0])
    plt.ylim([0.0, 1.05])
    plt.xlabel('False Positive Rate')
    plt.ylabel('True Positive Rate')
    plt.title('ROC Curve')
    plt.legend(loc="lower right")
    plt.show()


**ÇIKTI**

![Mllib'i'nın CrossValidator kullanarak Lojistik regresyon ROC eğrisi](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/mllib-crossvalidator-roc-curve.png)

### <a name="random-forest-classification"></a>Rastgele orman sınıflandırma
Bu bölümdeki Hello kodunu nasıl tootrain, değerlendirmek ve ipucu seyahat kümesindeki hello NYC ücreti seyahat ve ücreti ödenen olsun veya olmasın tahmin rastgele orman regresyon kaydedin gösterir.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # TRAIN RANDOMFOREST MODEL
    rfModel = RandomForest.trainClassifier(indexedTRAINbinary, numClasses=2, 
                                           categoricalFeaturesInfo=categoricalFeaturesInfo,
                                           numTrees=25, featureSubsetStrategy="auto",
                                           impurity='gini', maxDepth=5, maxBins=32)
    ## UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = rfModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # AREA UNDER ROC CURVE
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp;
    dirfilename = modelDir + rfclassificationfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**ÇIKTI**

ROC alanında 0.985336538462 =

Hücre tooexecute geçen süre: 26.72 saniye

### <a name="gradient-boosting-trees-classification"></a>Gradyan artırma ağaçları sınıflandırma
Bu bölümdeki Hello kodunu nasıl tootrain, değerlendirmek ve ipucu seyahat kümesindeki hello NYC ücreti seyahat ve ücreti ödenen olsun veya olmasın tahmin bir gradyan artırma ağaçları modeli kaydedin gösterir.

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                    numIterations=10)
    ## UNCOMMENT IF YOU WANT tooPRINT TREE DETAILS
    #print('Learned classification GBT model:')
    #print(bgtModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = gbtModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # Area under ROC curve
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN A BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp;
    dirfilename = modelDir + btclassificationfilename;

    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**ÇIKTI**

ROC alanında 0.985336538462 =

Hücre tooexecute geçen süre: 28.13 saniye

## <a name="predict-tip-amount-with-regression-models-not-using-cv"></a>İpucu tutar (MS kullanarak değil) regresyon modelleriyle tahmin etme
Bu bölümde nasıl hello regresyon görev için üç kullanım modelleri gösterir: tahmin diğer ipucu özelliklerini temel alarak ücreti seyahat için ücretli hello ipucu tutar. sunulan hello model şunlardır:

* Regularized doğrusal regresyon
* Rastgele orman
* Gradyan artırma ağaçları

Bu modeller hello girişte açıklandığı gibi. Her model kod bölümünde oluşturma adımları ayrılır: 

1. **Eğitim modeli** bir parametre kümesi ile verileri
2. **Model değerlendirme** ölçümlerle sınama veri kümesi üzerinde
3. **Model kaydetme** gelecekteki tüketimi için blob içinde   

> AZURE Not: Bu hello Lojistik regresyon modelleri için ayrıntılı gösterildi olduğundan çapraz doğrulama hello üç regresyon modeli, bu bölümde ile kullanılmaz. Merhaba, bu konunun ek toouse MS esnek Net ile doğrusal regresyon için nasıl sağlandığını gösteren bir örnek.
> 
> AZURE Not: deneyimi bizim olabilir yakınsama LinearRegressionWithSGD modellerin ile ilgili sorunları ve parametreleri değiştirilen/dikkatle geçerli bir model almak için en iyi duruma getirilmiş toobe gerekir. Değişkenleri önemli ölçüde ölçeklendirmeyi yakınsama yardımcı olur. Merhaba ek toothis konuda gösterilen esnek net regresyon de LinearRegressionWithSGD yerine kullanılabilir.
> 
> 

### <a name="linear-regression-with-sgd"></a>Doğrusal regresyon SGD ile
Merhaba kod bu bölümdeki toouse özellikleri tootrain iyileştirme için stokastik gradyan düşüşü (SGD) kullanan bir doğrusal regresyon nasıl ölçeklendirilmesi gösterir ve tooscore, değerlendirmek ve Azure Blob Storage (WASB) hello modeli kaydedin.

> [!TIP]
> Deneyimi bizim LinearRegressionWithSGD modellerin hello yakınsama sorunları olabilir ve parametreleri değiştirilen/dikkatle geçerli bir model almak için en iyi duruma getirilmiş toobe gerekir. Değişkenleri önemli ölçüde ölçeklendirmeyi yakınsama yardımcı olur.
> 
> 

    # LINEAR REGRESSION WITH SGD 

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel
    from pyspark.mllib.evaluation import RegressionMetrics
    from scipy import stats

    # USE SCALED FEATURES tooTRAIN MODEL
    linearModel = LinearRegressionWithSGD.train(oneHotTRAINregScaled, iterations=100, step = 0.1, regType='l2', regParam=0.1, intercept = True)

    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(linearModel.weights))
    print("Intercept: " + str(linearModel.intercept))

    # SCORE ON SCALED TEST DATA-SET & EVALUATE
    predictionAndLabels = oneHotTESTregScaled.map(lambda lp: (float(linearModel.predict(lp.features)), lp.label))
    testMetrics = RegressionMetrics(predictionAndLabels)

    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**ÇIKTI**

Katsayısını: [0.0141707753435,-0.0252930927087,-0.0231442517137, 0.247070902996, 0.312544147152, 0.360296120645, 0.0122079566092,-0.00456498588241,-0.0898228505177, 0.0714046248793, 0.102171263868, 0.100022455632,-0.00289545676449,-0.00791124681938, 0.54396316518,-0.536293513569, 0.0119076553369,-0.0173039244582, 0.0119632796147, 0.00146764882502]

Intercept: 0.854507624459

RMSE 1.23485131376 =

R sqr 0.597963951127 =

Hücre tooexecute geçen süre: 38.62 saniye

### <a name="random-forest-regression"></a>Rastgele orman regresyon
Bu bölümdeki Hello kodunu nasıl tootrain, değerlendirmek ve hello NYC ücreti seyahat veri ipucu tutarını tahmin rastgele orman modeli kaydedin gösterir.   

> [!NOTE]
> Çapraz doğrulama özel kod kullanarak yerleştirmez parametresiyle hello ekte sağlanır.
> 
> 

    #PREDICT TIP AMOUNTS USING RANDOM FOREST

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics


    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=25, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=10, maxBins=32)
    # UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT AND EVALUATE ON TEST DATA-SET
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = oneHotTESTreg.map(lambda lp: lp.label).zip(predictions)

    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp;
    dirfilename = modelDir + rfregressionfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**ÇIKTI**

RMSE 0.931981967875 =

R sqr 0.733445485802 =

Hücre tooexecute geçen süre: 25.98 saniye

### <a name="gradient-boosting-trees-regression"></a>Gradyan artırma ağaçları regresyon
Bu bölümdeki Hello kodunu nasıl tootrain, değerlendirmek ve hello NYC ücreti seyahat veri ipucu tutarını tahmin bir gradyan artırma ağaçları modeli kaydedin gösterir.

** Eğitme ve değerlendirme **

    #PREDICT TIP AMOUNTS USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel
    from pyspark.mllib.util import MLUtils

    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    gbtModel = GradientBoostedTrees.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo, 
                                                    numIterations=10, maxBins=32, maxDepth = 4, learningRate=0.1)

    # EVALUATE A TEST DATA-SET
    predictions = gbtModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES
    test_predictions= sqlContext.createDataFrame(predictionAndLabels)
    test_predictions_pddf = test_predictions.toPandas()

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp;
    dirfilename = modelDir + btregressionfilename;
    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**ÇIKTI**

RMSE 0.928172197114 =

R sqr 0.732680354389 =

Hücre tooexecute geçen süre: 20.9 saniye

**Çizim**

*tmp_results* hello önceki hücre Hive tablo olarak kaydedilir. Merhaba tablodan sonuçlar hello içine çıkarılır *sqlResults* çizdirmek için veri çerçeve. Merhaba kod aşağıdadır

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results


Merhaba Jupyter server kullanarak hello kod tooplot hello verilerini aşağıda verilmiştir.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import numpy as np

    # PLOT
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='_1', y='_2', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['_1'], sqlResults['_2'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    ax.plot(sqlResults['_1'], fit[0] * sqlResults['_1'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 15])
    plt.show(ax)

![Fiili-vs-tahmin-ipucu-tutarlar](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="appendix-additional-regression-tasks-using-cross-validation-with-parameter-sweeps"></a>Ek: çapraz doğrulama parametresi dağılımlarında ile kullanarak ek gerileme görevleri
Bu ek kod gösteren içeren nasıl doğrusal regresyon ve nasıl toodo MS parametresiyle sweep rastgele orman regresyon için özel kod kullanarak için esnek net kullanarak toodo MS.

### <a name="cross-validation-using-elastic-net-for-linear-regression"></a>Doğrulama için doğrusal regresyon esnek net kullanarak arası
Bu bölümdeki Hello kod nasıl toodo çapraz doğrulama için doğrusal regresyon esnek net kullanarak ve nasıl tooevaluate hello modeline göre test verilerini gösterir.

    ###  CV USING ELASTIC NET FOR LINEAR REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.regression import LinearRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import RegressionEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder

    # DEFINE ALGORITHM/MODEL
    lr = LinearRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build() 

    # DEFINE PIPELINE 
    # SIMPLY hello MODEL HERE, WITHOUT TRANSFORMATIONS
    pipeline = Pipeline(stages=[lr])

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=RegressionEvaluator(),
                        numFolds=3)

    # CONVERT tooDATA FRAME, AS CROSSVALIDATOR WON'T RUN ON RDDS
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINreg, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    # EVALUATE MODEL ON TEST SET
    testDataFrame = sqlContext.createDataFrame(oneHotTESTreg, ["features", "label"])

    # MAKE PREDICTIONS ON TEST DOCUMENTS
    # cvModel uses hello best model found (lrModel).
    predictionAndLabels = cv_model.transform(testDataFrame)

    # CONVERT tooDF AND SAVE REGISER DF AS TABLE
    predictionAndLabels.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**ÇIKTI**

Hücre tooexecute geçen süre: 161.21 saniye

**R SQR Metrik değerlendir**

*tmp_results* hello önceki hücre Hive tablo olarak kaydedilir. Merhaba tablodan sonuçlar hello içine çıkarılır *sqlResults* çizdirmek için veri çerçeve. Merhaba kod aşağıdadır

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT label,prediction from tmp_results


Merhaba kod toocalculate R sqr aşağıdadır.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    from scipy import stats

    #R-SQR TEST METRIC
    corstats = stats.linregress(sqlResults['label'],sqlResults['prediction'])
    r2 = (corstats[2]*corstats[2])
    print("R-sqr = %s" % r2)


**ÇIKTI**

R sqr 0.619184907088 =

### <a name="cross-validation-with-parameter-sweep-using-custom-code-for-random-forest-regression"></a>Rastgele orman regresyon için özel kod kullanarak parametre tarama ile doğrulama arası
Bu bölümdeki Hello kod nasıl toodo çapraz doğrulama rastgele orman regresyon için özel kod kullanarak parametre tarama ile ve nasıl tooevaluate hello modeline göre test verilerini gösterir.

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    # GET ACCURARY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics
    from sklearn.grid_search import ParameterGrid

    ## CREATE PARAMETER GRID
    grid = [{'maxDepth': [5,10], 'numTrees': [25,50]}]
    paramGrid = list(ParameterGrid(grid))

    ## SPECIFY LEVELS OF CATEGORICAL VARIBLES
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # SPECIFY NUMFOLDS AND ARRAY tooHOLD METRICS
    nFolds = 3;
    numModels = len(paramGrid)
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create labeled points from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowIndexingRegression)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowIndexingRegression)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            maxD = paramGrid[j]['maxDepth']
            numT = paramGrid[j]['numTrees']
            # Train logistic regression model with hypermarameter set
            rfModel = RandomForest.trainRegressor(trainCVLabPt, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=numT, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=maxD, maxBins=32)
            predictions = rfModel.predict(validationLabPt.map(lambda x: x.features))
            predictionAndLabels = validationLabPt.map(lambda lp: lp.label).zip(predictions)
            # Use ROC-AUC as accuracy metrics
            validMetrics = RegressionMetrics(predictionAndLabels)
            metric = validMetrics.rootMeanSquaredError
            metricSum[j] += metric

    avgAcc = metricSum/nFolds;
    bestParam = paramGrid[np.argmin(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    ## TRAIN FINAL MODL WIHT BEST PARAMETERS
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=bestParam['numTrees'], featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=bestParam['maxDepth'], maxBins=32)

    # EVALUATE MODEL ON TEST DATA
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    #PRINT TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**ÇIKTI**

RMSE 0.906972198262 =

R sqr 0.740751197012 =

Hücre tooexecute geçen süre: 69.17 saniye

### <a name="clean-up-objects-from-memory-and-print-model-locations"></a>Bellek ve yazdırma modeli konumları nesneleri Temizle
Kullanım `unpersist()` toodelete nesneleri bellekte önbelleğe alınmış.

    # UNPERSIST OBJECTS CACHED IN MEMORY

    # REMOVE ORIGINAL DFs
    taxi_df_train_cleaned.unpersist()
    taxi_df_train_with_newFeatures.unpersist()
    trainData.unpersist()
    trainData.unpersist()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.unpersist()
    indexedTESTbinary.unpersist()
    oneHotTRAINbinary.unpersist()
    oneHotTESTbinary.unpersist()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.unpersist()
    indexedTESTreg.unpersist()
    oneHotTRAINreg.unpersist()
    oneHotTESTreg.unpersist()

    # SCALED FEATURES
    oneHotTRAINregScaled.unpersist()
    oneHotTESTregScaled.unpersist()


**ÇIKTI**

PythonRDD [122] RDD PythonRDD.scala adresindeki adresindeki: 43

** Çıktının yolu toomodel hello tüketim not defterinde kullanılan toobe dosyaları. ** tooconsume ve puanı bağımsız veri kümesi, toocopy gerekir ve bu dosya adları hello "Tüketim dizüstü" yapıştırın.

    # PRINT MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


**ÇIKTI**

logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"

linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"

randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"

randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"

BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"

BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"

## <a name="whats-next"></a>Sırada ne var?
Spark Mllib'i hello ile regresyon ve sınıflandırma modelleri oluşturduğunuza göre hazır toolearn nasıl olan tooscore ve bu modeller değerlendirin.

**Model tüketimi:** toolearn nasıl tooscore ve bu konuda oluşturulan hello sınıflandırma ve regresyon modelleri değerlendirmek, bkz: [puanı ve Spark yerleşik makine öğrenimi modellerini değerlendirme](machine-learning-data-science-spark-model-consumption.md).

