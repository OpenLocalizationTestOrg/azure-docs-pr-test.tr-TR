---
title: "aaaData Bilim Scala ve Spark Azure üzerinde kullanarak | Microsoft Docs"
description: "Nasıl toouse Scala denetimli machine learning ile görevleri için Spark ölçeklenebilir Mllib'i ve Spark ML paketleri Azure Hdınsight Spark kümesinde hello."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a7c97153-583e-48fe-b301-365123db3780
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;deguhath
ms.openlocfilehash: e32ebd0b91417183fe48ee10ebc7929fd9605762
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-using-scala-and-spark-on-azure"></a>Azure üzerinde Scala ve Spark kullanan Veri Bilimi
Bu makale bir Azure Hdınsight Spark kümesinde nasıl toouse Scala denetimli makine öğrenimi görevlerini hello Spark ölçeklenebilir Mllib'i ve Spark ML için paketler gösterir. Merhaba oluşturduğunu hello görevlerinde anlatılmaktadır [veri bilimi işlem](http://aka.ms/datascienceprocess): veri alımı ve keşfi, görselleştirme, özellik Mühendisliği, model ve model tüketim. hello makale Hello modellerinde Lojistik ve doğrusal regresyon, rastgele ormanları ve gradyan boosted ağaçları (GBTs) dahil, ayrıca tootwo ortak makine öğrenimi görevlerini denetimli:

* Regresyon sorunu: Tahmin ücreti seyahat için hello ipucu tutar ($)
* İkili sınıflandırma: tahmin ipucu veya ücreti seyahat için ipucu yok (1/0)

İşlem modelleme hello eğitim ve sınama veri kümesi ve ilgili doğruluğu ölçümleri değerlendirme gerektirir. Bu makalede, toostore bunlar nasıl modelleri de öğrenebilirsiniz Azure Blob Depolama ve nasıl tooscore ve Tahmine dayalı kendi performansını değerlendirin. Bu makale çapraz doğrulama ve parametre hyper Süpürme kullanarak toooptimize nasıl modeller, konuları daha gelişmiş hello da kapsar. kullanılan hello verileri hello 2013 NYC ücreti seyahat ve ücreti veri kümesinin Github'da bulunan bir örnektir.

[Scala](http://www.scala-lang.org/), nesne yönelimli ve işlevsel dil kavramları hello Java sanal makineye bağlı bir dil tümleştirir. Bu, hello bulutta işleme uygun toodistributed ve Azure Spark kümeleri üzerinde çalışan ölçeklenebilir bir dildir.

[Spark](http://spark.apache.org/) bellek içi destekleyen bir açık kaynak paralel işleme altyapısıdır işliyor tooboost hello büyük veri analizi uygulamalarının performansını. Merhaba Spark işleme altyapısı hızı, kullanımı kolay, gelişmiş analizler için yerleşik olarak bulunur. Spark'ın bellek içi dağıtılmış hesaplama özellikleri machine learning ve grafik hesaplamalarında yinelemeli algoritmalar için iyi bir seçim yapın. Merhaba [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) paket yardımcı olabilecek çerçeveleri oluşturmak ve ardışık düzen öğrenme pratik makine ayarlamak veri üstünde yerleşik yüksek düzey API'leri Tekdüzen kümesi sağlar. [Mllib'i](http://spark.apache.org/mllib/) modelleme yetenekleri getirir Spark'ın ölçeklenebilir machine learning kitaplığı toothis dağıtılmış ortamı.

[Hdınsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) hello Azure barındırılan açık kaynak Spark, bir tekliftir. Merhaba Spark kümesinde Jupyter Scala dizüstü bilgisayarlar için destek de içerir ve çalışma Spark SQL etkileşimli sorguları tootransform filtre uygulayabilir ve Azure Blob depolamada depolanan verileri görselleştirin. Merhaba çözümleri sağlayan ve hello ilgili çizimleri toovisualize hello verileri göster hello Scala kod parçacıkları bu makalede hello Spark kümeleri üzerinde yüklü Jupyter not defterleri çalıştırın. Aşağıdaki konulardaki Hello modelleme adımları nasıl tootrain, değerlendirmek, kaydetme ve kullanmayı modelinin yazın ve her gösteren kod sahip.

Merhaba kurulum adımlarını ve bu makaledeki kod için Azure Hdınsight 3.4 Spark 1.6 markalarıdır. Ancak, bu makaledeki ve hello kodu hello [Scala Jupyter not defteri](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) geneldir ve tüm Spark kümesi üzerinde çalışması gerekir. Küme kurulumu hello ve bir yönetim adımı Hdınsight Spark kullanmıyorsanız ne bu makalede gösterilenden biraz farklı olabilir.

> [!NOTE]
> Nasıl bir uçtan uca veri bilimi işlemi toouse Scala yerine Python toocomplete görevleri gösterir bir konuya bakın [veri bilimi Azure Hdınsight'ta Spark kullanmanın](machine-learning-data-science-spark-overview.md).
> 
> 

## <a name="prerequisites"></a>Ön koşullar
* Bir Azure aboneliğinizin olması gerekir. Zaten bir yoksa [Azure ücretsiz deneme sürümünü edinin](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Yordamları izleyerek bir Azure Hdınsight 3.4 Spark 1.6 küme toocomplete hello gerekir. toocreate bir küme bkz hello yönergeleri [Başlarken: Azure hdınsight'ta Apache Spark oluşturmak](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md). Merhaba üzerinde hello küme türü ve sürümü ayarlama **küme türü seçin** menüsü.

![Hdınsight küme türü yapılandırma](./media/machine-learning-data-science-process-scala-walkthrough/spark-cluster-on-portal.png)

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

Merhaba NYC ücreti seyahat veri ve nasıl tooexecute kod hello Spark kümesinde Jupyter not defteri gelen yönergeleri açıklaması için hello ilgili bölümlere bakın [genel bakış, verileri Azure Hdınsight'ta Spark kullanmanın Bilim](machine-learning-data-science-spark-overview.md).  

## <a name="execute-scala-code-from-a-jupyter-notebook-on-hello-spark-cluster"></a>Merhaba Spark kümesinde Jupyter not defteri gelen Scala kodu yürütme
Jupyter not defteri hello Azure Portalı'ndan başlatabilirsiniz. Panonuz Hello Spark kümesinde bulun ve sonra tooenter hello Yönetim sayfasında kümeniz için tıklatın. Bundan sonra öğesini **küme panolarında**ve ardından **Jupyter not defteri** tooopen hello not defteri hello Spark kümesi ile ilişkili.

![Küme panosu ve Jupyter Not Defterleri](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-on-portal.png)

Jupyter not defterleri https:// sırasında da erişebilirsiniz&lt;clustername&gt;.azurehdinsight.net/jupyter. Değiştir *clustername* kümenizin hello ada sahip. Yönetici hesabı tooaccess hello Jupyter not defterlerinizi için başlangıç parolası gerekir.

![Merhaba küme adını kullanarak tooJupyter not defterlerini gidin](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-notebook.png)

Seçin **Scala** toosee paketlenmiş not defterlerini birkaçı bu kullanım hello PySpark API sahip bir dizini. Merhaba kod örnekleri üzerinde Spark konular bu paketi kullanılabilir içeren Scala.ipynb Not Defteri kullanarak araştırması modelleme ve puanlama hello [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).

Spark kümesinde hello dizüstü GitHub toohello Jupyter not defteri sunucu doğrudan karşıya yükleyebilirsiniz. Merhaba, Jupyter giriş sayfasında, tıklatın **karşıya** düğmesi. Merhaba dosya Gezgini'nde, hello GitHub (Ham içerik) hello Scala dizüstü URL'sini yapıştırın ve ardından **açık**. Merhaba Scala dizüstü URL aşağıdaki hello kullanılabilir:

[Exploration-Modeling-and-Scoring-using-Scala.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration-Modeling-and-Scoring-using-Scala.ipynb)

## <a name="setup-preset-spark-and-hive-contexts-spark-magics-and-spark-libraries"></a>Kurulumu: Hazır Spark ve Hive bağlamları, Spark sihirler ve Spark kitaplıkları
### <a name="preset-spark-and-hive-contexts"></a>Spark ve Hive bağlamları hazır
    # SET hello START TIME
    import java.util.Calendar
    val beginningTime = Calendar.getInstance().getTime()


Jupyter not defterleri ile sağlanan hello Spark tekrar hazır bağlamları vardır. Geliştirdiğiniz Merhaba uygulaması ile çalışmaya başlamadan önce tooexplicitly kümesi hello Spark veya Hive bağlamları gerekmez. Merhaba hazır bağlamları şunlardır:

* `sc`SparkContext için
* `sqlContext`HiveContext için

### <a name="spark-magics"></a>Spark sihirler
Merhaba Spark çekirdek bazı önceden tanımlanmış "sihirleri" ile çağırabilir özel komutlar olduğu sağlar `%%`. Bu komutların iki kod örnekleri aşağıdaki hello kullanılır.

* `%%local`sonraki satırların Hello kodda yerel olarak yürütülecek belirtir. Merhaba kodu geçerli Scala kodu olmalıdır.
* `%%sql -o <variable name>`bir Hive sorgusu yürütür `sqlContext`. Merhaba, `-o` parametresi geçirilir, hello hello sorgunun sonucu hello kalıcı `%%local` Scala bağlamı Spark veri çerçeve olarak.

İle arama, hello tekrar Jupyter not defterlerini ve bunların önceden tanımlanmış hakkında daha fazla bilgi "magics için" `%%` (örneğin, `%%local`), bkz: [Jupyter not defterlerinde kullanılabilen çekirdekler Hdınsight Spark Linux kümeleri Hdınsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).

### <a name="import-libraries"></a>Kitaplıkları içeri aktarma
Merhaba Spark, Mllib'i ve koddan hello kullanarak gerekir diğer kitaplıkları içeri aktarın.

    # IMPORT SPARK AND JAVA LIBRARIES
    import org.apache.spark.sql.SQLContext
    import org.apache.spark.sql.functions._
    import java.text.SimpleDateFormat
    import java.util.Calendar
    import sqlContext.implicits._
    import org.apache.spark.sql.Row

    # IMPORT SPARK SQL FUNCTIONS
    import org.apache.spark.sql.types.{StructType, StructField, StringType, IntegerType, FloatType, DoubleType}
    import org.apache.spark.sql.functions.rand

    # IMPORT SPARK ML FUNCTIONS
    import org.apache.spark.ml.Pipeline
    import org.apache.spark.ml.feature.{StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer, Binarizer}
    import org.apache.spark.ml.tuning.{ParamGridBuilder, TrainValidationSplit, CrossValidator}
    import org.apache.spark.ml.regression.{LinearRegression, LinearRegressionModel, RandomForestRegressor, RandomForestRegressionModel, GBTRegressor, GBTRegressionModel}
    import org.apache.spark.ml.classification.{LogisticRegression, LogisticRegressionModel, RandomForestClassifier, RandomForestClassificationModel, GBTClassifier, GBTClassificationModel}
    import org.apache.spark.ml.evaluation.{BinaryClassificationEvaluator, RegressionEvaluator, MulticlassClassificationEvaluator}

    # IMPORT SPARK MLLIB FUNCTIONS
    import org.apache.spark.mllib.linalg.{Vector, Vectors}
    import org.apache.spark.mllib.util.MLUtils
    import org.apache.spark.mllib.classification.{LogisticRegressionWithLBFGS, LogisticRegressionModel}
    import org.apache.spark.mllib.regression.{LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel}
    import org.apache.spark.mllib.tree.{GradientBoostedTrees, RandomForest}
    import org.apache.spark.mllib.tree.configuration.BoostingStrategy
    import org.apache.spark.mllib.tree.model.{GradientBoostedTreesModel, RandomForestModel, Predict}
    import org.apache.spark.mllib.evaluation.{BinaryClassificationMetrics, MulticlassMetrics, RegressionMetrics}

    # SPECIFY SQLCONTEXT
    val sqlContext = new SQLContext(sc)


## <a name="data-ingestion"></a>Veri alımı
Merhaba ilk hello veri bilimi işlem tooanalyze istediğiniz tooingest hello veri adımdır. Veri keşfi ve modelleme ortamınıza bulunduğu hello veri dış kaynaklara veya sistemlerinden getirin. Bu makalede, alma hello veri bir birleştirilmiş % 0,1 (.tsv dosyası olarak depolanır) hello ücreti seyahat ve ücreti dosyası örneğidir. Merhaba veri keşfi ve modelleme Spark ortamıdır. Bu bölümde, görev dizisini aşağıdaki hello kod toocomplete hello içerir:

1. Depolama veri ve model için dizin yolu olarak ayarlayın.
2. Merhaba giriş veri kümesindeki (bir .tsv dosyası olarak depolanır) okuyun.
3. Merhaba verileri ve temiz hello verileri için bir şema tanımlayın.
4. Temizlenen veri çerçevesi oluşturun ve bellekte önbelleğe.
5. Merhaba veri SQLContext geçici tablo olarak kaydedin.
6. Merhaba Tablo Sorgu ve veri çerçeveye hello sonuçları alın.

### <a name="set-directory-paths-for-storage-locations-in-azure-blob-storage"></a>Dizin yolları depolama konumları için Azure Blob depolama alanına ayarlayın
Spark okuma ve tooAzure Blob Depolama yazma. Mevcut verilerinizi Spark tooprocess kullanın ve ardından hello sonuçları Blob storage'da depolamak.

toosave modelleri veya Blob storage'da dosyaları, gereksinim duyduğunuz tooproperly hello yolunu belirtin. Başvuru hello varsayılan kapsayıcı bağlı toohello Spark kümesi ile başlayan bir yolu kullanarak `wasb:///`. Diğer konumları kullanarak başvuru `wasb://`.

Merhaba aşağıdaki kod örneği hello giriş verisi toobe okuyun ve ekli toohello Spark küme hello yolu tooBlob depolama hello modeli kaydedileceği hello konumunu belirtir.

    # SET PATHS tooDATA AND MODEL FILE LOCATIONS
    # INGEST DATA AND SPECIFY HEADERS FOR COLUMNS
    val taxi_train_file = sc.textFile("wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv")
    val header = taxi_train_file.first;

    # SET hello MODEL STORAGE DIRECTORY PATH
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS REQUIRED.
    val modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";


### <a name="import-data-create-an-rdd-and-define-a-data-frame-according-toohello-schema"></a>Veri alma, bir RDD oluşturun ve toohello şemasına göre bir veri çerçevesi tanımlayın
    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello SCHEMA BASED ON hello HEADER OF hello FILE
    val sqlContext = new SQLContext(sc)
    val taxi_schema = StructType(
        Array(
            StructField("medallion", StringType, true),
            StructField("hack_license", StringType, true),
            StructField("vendor_id", StringType, true),
            StructField("rate_code", DoubleType, true),
            StructField("store_and_fwd_flag", StringType, true),
            StructField("pickup_datetime", StringType, true),
            StructField("dropoff_datetime", StringType, true),
            StructField("pickup_hour", DoubleType, true),
            StructField("pickup_week", DoubleType, true),
            StructField("weekday", DoubleType, true),
            StructField("passenger_count", DoubleType, true),
            StructField("trip_time_in_secs", DoubleType, true),
            StructField("trip_distance", DoubleType, true),
            StructField("pickup_longitude", DoubleType, true),
            StructField("pickup_latitude", DoubleType, true),
            StructField("dropoff_longitude", DoubleType, true),
            StructField("dropoff_latitude", DoubleType, true),
            StructField("direct_distance", StringType, true),
            StructField("payment_type", StringType, true),
            StructField("fare_amount", DoubleType, true),
            StructField("surcharge", DoubleType, true),
            StructField("mta_tax", DoubleType, true),
            StructField("tip_amount", DoubleType, true),
            StructField("tolls_amount", DoubleType, true),
            StructField("total_amount", DoubleType, true),
            StructField("tipped", DoubleType, true),
            StructField("tip_class", DoubleType, true)
            )
        )

    # CAST VARIABLES ACCORDING toohello SCHEMA
    val taxi_temp = (taxi_train_file.map(_.split("\t"))
                            .filter((r) => r(0) != "medallion")
                            .map(p => Row(p(0), p(1), p(2),
                                p(3).toDouble, p(4), p(5), p(6), p(7).toDouble, p(8).toDouble, p(9).toDouble, p(10).toDouble,
                                p(11).toDouble, p(12).toDouble, p(13).toDouble, p(14).toDouble, p(15).toDouble, p(16).toDouble,
                                p(17), p(18), p(19).toDouble, p(20).toDouble, p(21).toDouble, p(22).toDouble,
                                p(23).toDouble, p(24).toDouble, p(25).toDouble, p(26).toDouble)))


    # CREATE AN INITIAL DATA FRAME AND DROP COLUMNS, AND THEN CREATE A CLEANED DATA FRAME BY FILTERING FOR UNWANTED VALUES OR OUTLIERS
    val taxi_train_df = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    val taxi_df_train_cleaned = (taxi_train_df.drop(taxi_train_df.col("medallion"))
            .drop(taxi_train_df.col("hack_license")).drop(taxi_train_df.col("store_and_fwd_flag"))
            .drop(taxi_train_df.col("pickup_datetime")).drop(taxi_train_df.col("dropoff_datetime"))
            .drop(taxi_train_df.col("pickup_longitude")).drop(taxi_train_df.col("pickup_latitude"))
            .drop(taxi_train_df.col("dropoff_longitude")).drop(taxi_train_df.col("dropoff_latitude"))
            .drop(taxi_train_df.col("surcharge")).drop(taxi_train_df.col("mta_tax"))
            .drop(taxi_train_df.col("direct_distance")).drop(taxi_train_df.col("tolls_amount"))
            .drop(taxi_train_df.col("total_amount")).drop(taxi_train_df.col("tip_class"))
            .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200"));

    # CACHE AND MATERIALIZE hello CLEANED DATA FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER hello DATA FRAME AS A TEMPORARY TABLE IN SQLCONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Çıktı:**

Zaman toorun hello hücre: 8 saniye.

### <a name="query-hello-table-and-import-results-in-a-data-frame"></a>Merhaba Tablo Sorgu ve veri çerçevesinde sonuçları Al
Ardından, ücreti, yolcu ve ipucu veri için sorgu hello tablosu; bozuk ve harici verilerini filtre; ve birkaç satır yazdırın.

    # QUERY hello DATA
    val sqlStatement = """
        SELECT fare_amount, passenger_count, tip_amount, tipped
        FROM taxi_train
        WHERE passenger_count > 0 AND passenger_count < 7
        AND fare_amount > 0 AND fare_amount < 200
        AND payment_type in ('CSH', 'CRD')
        AND tip_amount > 0 AND tip_amount < 25
    """
    val sqlResultsDF = sqlContext.sql(sqlStatement)

    # SHOW ONLY hello TOP THREE ROWS
    sqlResultsDF.show(3)

**Çıktı:**

| fare_amount | passenger_count | tip_amount | Eğimli |
| --- | --- | --- | --- |
|        13.5 |1.0 |2.9 |1.0 |
|        16.0 |2.0 |3.4 |1.0 |
|        10.5 |2.0 |1.0 |1.0 |

## <a name="data-exploration-and-visualization"></a>Veri keşfi ve görselleştirme
Spark hello verileri aldıktan sonra hello sonraki hello veri bilimi işlem toogain hello veri keşfi ve görselleştirme aracılığıyla daha derin bir anlayış adımdır. Bu bölümde, SQL sorguları kullanarak hello ücreti verileri inceleyin. Ardından, bir veri çerçeve tooplot içine hello sonuçlarını içeri aktar hedef değişkenleri ve görsel İnceleme için olası özellikleri Jupyter hello otomatik görselleştirme özelliğini kullanarak hello.

### <a name="use-local-and-sql-magic-tooplot-data"></a>Yerel ve SQL Sihirli tooplot veri kullanın
Varsayılan olarak, Jupyter not defteri çalıştırmak herhangi kod parçacığını hello çıktısını hello çalışan düğümlerine kalıcı hello oturumunun hello bağlam içinde kullanılabilir. Tüm (Merhaba baş düğüm olan) yerel olarak hello Jupyter sunucu düğümünde, hesaplama için gereksinim duyduğunuz verileri Merhaba, hello kullanabilirsiniz ve her hesaplama için seyahat toohello çalışan düğümleri toosave isterseniz `%%local` Sihirli toorun hello kodu kod parçacığında hello Jupyter sunucusunda.

* **SQL Sihirli** (`%%sql`). Merhaba Hdınsight Spark çekirdek SQLContext kolay satır içi HiveQL sorguları destekler. Merhaba (`-o VARIABLE_NAME`) bağımsız değişkeni devam ederse hello SQL sorgusu hello çıktısını hello Jupyter sunucuda Pandas veri çerçeve olarak. Başka bir deyişle, hello yerel modda kullanılabilir olması.
* `%%local`**Sihirli**. Merhaba `%%local` Sihirli çalıştıran hello kod yerel olarak hello Hdınsight kümesi baş düğüm hello hello Jupyter sunucu üzerinde. Genellikle, kullandığınız `%%local` hello birlikte Sihirli `%%sql` hello ile Sihirli `-o` parametresi. Merhaba `-o` parametresi yerel olarak hello SQL sorgusu hello çıktısını kalıcı ve ardından `%%local` Sihirli hello sonraki kod parçacığını toorun yerel olarak yerel olarak kalıcı hello çıktı hello SQL sorgularının karşı kümesini tetiklemek.

### <a name="query-hello-data-by-using-sql"></a>SQL kullanarak Hello veri sorgulama
Bu sorgu hello ücreti dönüşleri ücreti tutarı, yolcu sayısı ve ipucu miktarını alır.

    # RUN hello SQL QUERY
    %%sql -q -o sqlResults
    SELECT fare_amount, passenger_count, tip_amount, tipped FROM taxi_train WHERE passenger_count > 0 AND passenger_count < 7 AND fare_amount > 0 AND fare_amount < 200 AND payment_type in ('CSH', 'CRD') AND tip_amount > 0 AND tip_amount < 25

Koddan hello hello `%%local` Sihirli sqlResults bir yerel veri çerçevesi oluşturur. Matplotlib kullanarak sqlResults tooplot kullanabilirsiniz.

> [!TIP]
> Yerel Sihirli birden çok kez bu makalede kullanılır. Veri kümenizi büyük olursa, lütfen toocreate yerel belleğe sığması veri çerçevesi örnek.
> 
> 

### <a name="plot-hello-data"></a>Çizim hello veri
Yerel bağlamı Pandas veri çerçeve olarak hello veri çerçevesi olduktan sonra Python kodu kullanarak çizebilirsiniz.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES.
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, ETC.)
    sqlResults


 Merhaba kod çalıştırdıktan sonra hello Spark çekirdek (HiveQL) SQL sorguları hello çıktısını otomatik olarak visualizes. Görselleştirmeleri çeşitli türleri arasında seçim yapabilirsiniz:

* Tablo
* Pasta
* Çizgi
* Alan
* Çubuğu

Merhaba kod tooplot hello verileri şöyledir:

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    # PLOT TIP BY PAYMENT TYPE AND PASSENGER COUNT
    ax1 = sqlResults[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # PLOT TIP BY PASSENGER COUNT
    ax2 = sqlResults.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # PLOT TIP AMOUNT BY FARE AMOUNT; SCALE POINTS BY PASSENGER COUNT
    ax = sqlResults.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(sqlResults.passenger_count))
    ax.set_title('Tip amount by Fare amount')
    ax.set_xlabel('Fare Amount ($)')
    ax.set_ylabel('Tip Amount ($)')
    plt.axis([-2, 80, -2, 20])
    plt.show()


**Çıktı:**

![İpucu tutar histogram](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-histogram.png)

![Yolcu sayısına göre ipucu tutar](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-passenger-count.png)

![İpucu tutar ücreti miktar](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-fare-amount.png)

## <a name="create-features-and-transform-features-and-then-prep-data-for-input-into-modeling-functions"></a>Özellikler oluşturmak ve özellikleri dönüştürme ve veri işlevleri modelleme içine girişi için hazırla
Spark ML ve Mllib'i ağaç tabanlı modelleme işlevleri için tooprepare hedef ve özellik binning, dizin oluşturma, bir seyrek kodlama ve vectorization gibi teknikler çeşitli kullanarak vardır. Bu bölümde hello yordamları toofollow şunlardır:

1. Yeni bir özellik tarafından oluşturma **binning** trafiği saate demet saat.
2. Uygulama **dizin oluşturma ve bir hot kodlama** toocategorical özellikleri.
3. **Örnek ve bölünmüş hello veri kümesi** eğitim ve test kesirler içine.
4. **Eğitim değişken ve Özellikler belirtmek**, eğitim kodlanmış dizinlenmiş veya bir dinamik sonra oluşturmak ve esnek giriş etiketli noktası sınama Dağıtılmış veri kümeleri (RDDs) veya veri çerçevesi.
5. Otomatik olarak **kategorilere ayırmak ve özellikleri ve hedefleri vectorize** toouse makine öğrenimi modellerini için girdi olarak.

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a>Yeni bir özellik tarafından binning saatleri trafiği zaman demet oluşturun.
Bu kodu nasıl toocreate saatleri trafiği zamanına binning tarafından yeni bir özellik aralıkları ve nasıl toocache hello bellek ortaya çıkan veri çerçevede gösterir. RDDs ve veri çerçevelerini art arda kullanıldığı önbelleğe alma tooimproved yürütme sürelerinin yol açar. Buna göre aşağıdaki yordamlarını hello çeşitli aşamalarında RDDs ve veri çerçevelerini önbelleğe alacağız.

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    val sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night"
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush"
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_train
    """
    val taxi_df_train_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE hello DATA FRAME IN MEMORY AND MATERIALIZE hello DATA FRAME IN MEMORY
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()


### <a name="indexing-and-one-hot-encoding-of-categorical-features"></a>Dizin oluşturma ve bir hot kategorik özelliklerini kodlama
Modelleme hello ve Mllib'i işlevlerini kategorik giriş verisi toobe özelliklerle dizine veya önceki toouse kodlanmış gerektiren tahmin etmek. Bu bölümde, nasıl gösterilir tooindex veya İşlevler modelleme hello giriş için kategorik özellikleri kodlayın.

Merhaba modeline bağlı olarak, farklı şekillerde Modellerinizi kodlamak veya tooindex gerekir. Örneğin, bir seyrek kodlama Lojistik ve doğrusal regresyon modeli gerektirir. Örneğin, üç kategoride özelliğiyle üç özellik sütunlara genişletilebilir. Her sütun, 0 veya 1 bir gözlem hello kategorisine bağlı olarak içerecektir. Mllib'i sağlar hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) bir hot kodlama için işlevi. Bu Kodlayıcı sütununun etiket dizinlerini tooa ikili vektörlerinin en çok bir değerle tek bir-bir sütun eşler. Bu kodlama ile Lojistik regresyon gibi sayısal değerli özellikleri beklediğiniz algoritmaları uygulanan toocategorical özellikleri olabilir.

Burada karakter dizelerdir yalnızca dört değişkenleri tooshow örnekler dönüştürün. Kategorik değişkenleri olarak sayısal değerleri tarafından temsil edilen diğer gibi değişkenleri hafta içi günü, ayrıca dizin oluşturabilirsiniz.

Dizin oluşturma için kullanmak `StringIndexer()`ve bir hot kodlaması için `OneHotEncoder()` Mllib'i işlevlerden. Kategorik özellikleri kodlanacağını ve kod tooindex hello şöyledir:

    # CREATE INDEXES AND ONE-HOT ENCODED VECTORS FOR SEVERAL CATEGORICAL FEATURES

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # INDEX AND ENCODE VENDOR_ID
    val stringIndexer = new StringIndexer().setInputCol("vendor_id").setOutputCol("vendorIndex").fit(taxi_df_train_with_newFeatures)
    val indexed = stringIndexer.transform(taxi_df_train_with_newFeatures)
    val encoder = new OneHotEncoder().setInputCol("vendorIndex").setOutputCol("vendorVec")
    val encoded1 = encoder.transform(indexed)

    # INDEX AND ENCODE RATE_CODE
    val stringIndexer = new StringIndexer().setInputCol("rate_code").setOutputCol("rateIndex").fit(encoded1)
    val indexed = stringIndexer.transform(encoded1)
    val encoder = new OneHotEncoder().setInputCol("rateIndex").setOutputCol("rateVec")
    val encoded2 = encoder.transform(indexed)

    # INDEX AND ENCODE PAYMENT_TYPE
    val stringIndexer = new StringIndexer().setInputCol("payment_type").setOutputCol("paymentIndex").fit(encoded2)
    val indexed = stringIndexer.transform(encoded2)
    val encoder = new OneHotEncoder().setInputCol("paymentIndex").setOutputCol("paymentVec")
    val encoded3 = encoder.transform(indexed)

    # INDEX AND TRAFFIC TIME BINS
    val stringIndexer = new StringIndexer().setInputCol("TrafficTimeBins").setOutputCol("TrafficTimeBinsIndex").fit(encoded3)
    val indexed = stringIndexer.transform(encoded3)
    val encoder = new OneHotEncoder().setInputCol("TrafficTimeBinsIndex").setOutputCol("TrafficTimeBinsVec")
    val encodedFinal = encoder.transform(indexed)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Çıktı:**

Zaman toorun hello hücre: 4 saniye.

### <a name="sample-and-split-hello-data-set-into-training-and-test-fractions"></a>Örnek ve bölünmüş veri kümesi eğitim ve test kesirler hello
Bu kod bir rastgele örnekleme hello verilerin (Bu örnekte, %25) oluşturur. Örnekleme bu örneğin hello veri kümesinin toohello boyutu nedeniyle gerekli olmamasına karşın, hello makale, böylece bildiğiniz nasıl, örnek oluşturabilirsiniz gösterir nasıl toouse gerektiğinde kendi sorunları için. Örnekleri büyük olduğunda modelleri eğitme sırada bu önemli zaman kazanabilirsiniz. Ardından, bölme hello örnek eğitim bölümü (Bu örnekte, %75) ve bir test olarak sınıflandırma ve regresyon modelleme (Bu örnekte, %25) toouse parçası.

Eğitim sırasında kullanılan tooselect çapraz doğrulama Katlama olan bir (0 ve 1 arasında) rastgele bir sayıyı tooeach satır ("rand" sütununda) ekleyin.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    val samplingFraction = 0.25;
    val trainingFraction = 0.75;
    val testingFraction = (1-trainingFraction);
    val seed = 1234;
    val encodedFinalSampledTmp = encodedFinal.sample(withReplacement = false, fraction = samplingFraction, seed = seed)
    val sampledDFcount = encodedFinalSampledTmp.count().toInt

    val generateRandomDouble = udf(() => {
        scala.util.Random.nextDouble
    })

    # ADD A RANDOM NUMBER FOR CROSS-VALIDATION
    val encodedFinalSampled = encodedFinalSampledTmp.withColumn("rand", generateRandomDouble());

    # SPLIT hello SAMPLED DATA FRAME INTO TRAIN AND TEST, WITH A RANDOM COLUMN ADDED FOR DOING CROSS-VALIDATION (SHOWN LATER)
    # INCLUDE A RANDOM COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    val splits = encodedFinalSampled.randomSplit(Array(trainingFraction, testingFraction), seed = seed)
    val trainData = splits(0)
    val testData = splits(1)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Çıktı:**

Zaman toorun hello hücre: 2 saniye.

### <a name="specify-training-variable-and-features-and-then-create-indexed-or-one-hot-encoded-training-and-testing-input-labeled-point-rdds-or-data-frames"></a>Eğitim değişken ve özellikleri belirtin ve sonra eğitim ve giriş noktası RDDs ya da veri çerçevelerini etiketli test kodlanmış dizinli veya bir hot oluşturun
Bu bölümde nasıl tooindex kategorik metin verileri olarak etiketli bir veri türü gelin ve tootrain ve test Mllib'i Lojistik regresyon ve diğer sınıflandırma modelleri kullanabilmeniz için kodlama gösterir kodunu içerir. Etiketli noktası, girdi verisi olarak machine learning algoritmaları Mllib'i çoğu tarafından gerektiği şekilde biçimlendirilmiş RDDs nesneleridir. A [noktası etiketli](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) yerel bir vektör, yoğun veya seyrek, etiket/yanıt ile ilişkilidir.

Bu kodda hello hedef (bağımlı) değişkeni ve hello özellikleri toouse tootrain modelleri belirtin. Sonra eğitim ve giriş noktası RDDs ya da veri çerçevelerini etiketli test kodlanmış dizinlenmiş veya bir hot oluşturursunuz.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # MAP NAMES OF FEATURES AND TARGETS FOR CLASSIFICATION AND REGRESSION PROBLEMS
    val featuresIndOneHot = List("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))
    val featuresIndIndex = List("paymentIndex", "vendorIndex", "rateIndex", "TrafficTimeBinsIndex", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))

    # SPECIFY hello TARGET FOR CLASSIFICATION ('tipped') AND REGRESSION ('tip_amount') PROBLEMS
    val targetIndBinary = List("tipped").map(encodedFinalSampled.columns.indexOf(_))
    val targetIndRegression = List("tip_amount").map(encodedFinalSampled.columns.indexOf(_))

    # CREATE INDEXED LABELED POINT RDD OBJECTS
    val indexedTRAINbinary = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTbinary = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTRAINreg = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTreg = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))

    # CREATE INDEXED DATA FRAMES THAT YOU CAN USE tooTRAIN BY USING SPARK ML FUNCTIONS
    val indexedTRAINbinaryDF = indexedTRAINbinary.toDF()
    val indexedTESTbinaryDF = indexedTESTbinary.toDF()
    val indexedTRAINregDF = indexedTRAINreg.toDF()
    val indexedTESTregDF = indexedTESTreg.toDF()

    # CREATE ONE-HOT ENCODED (VECTORIZED) DATA FRAMES THAT YOU CAN USE tooTRAIN BY USING SPARK ML FUNCTIONS
    val assemblerOneHot = new VectorAssembler().setInputCols(Array("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount")).setOutputCol("features")
    val OneHotTRAIN = assemblerOneHot.transform(trainData)
    val OneHotTEST = assemblerOneHot.transform(testData)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Çıktı:**

Zaman toorun hello hücre: 4 saniye.

### <a name="automatically-categorize-and-vectorize-features-and-targets-toouse-as-inputs-for-machine-learning-models"></a>Otomatik olarak kategorilere ayırmak ve makine öğrenimi modellerini için girdi olarak özellikleri ve hedefleri toouse vectorize
Hedef ve özellik Spark ML toocategorize hello toouse ağaç tabanlı modelleme işlevlerde kullanın. Merhaba kod iki görevleri tamamlar:

* Sınıflandırma için ikili hedef 0 veya 1 tooeach veri noktası 0 ile 1 arasında bir değer 0,5 eşik değerini kullanarak atayarak oluşturur.
* Otomatik olarak özellikleri kategorilere ayırır. Bu özellik, herhangi bir özellik için farklı sayısal değerleri Hello sayısı 32'den az ise, kategorilere ayrılmıştır.

Burada, bu iki görevler için hello kodu verilmiştir.

    # CATEGORIZE FEATURES AND BINARIZE hello TARGET FOR hello BINARY CLASSIFICATION PROBLEM

    # TRAIN DATA
    val indexer = new VectorIndexer().setInputCol("features").setOutputCol("featuresCat").setMaxCategories(32)
    val indexerModel = indexer.fit(indexedTRAINbinaryDF)
    val indexedTrainwithCatFeat = indexerModel.transform(indexedTRAINbinaryDF)
    val binarizer: Binarizer = new Binarizer().setInputCol("label").setOutputCol("labelBin").setThreshold(0.5)
    val indexedTRAINwithCatFeatBinTarget = binarizer.transform(indexedTrainwithCatFeat)

    # TEST DATA
    val indexerModel = indexer.fit(indexedTESTbinaryDF)
    val indexedTrainwithCatFeat = indexerModel.transform(indexedTESTbinaryDF)
    val binarizer: Binarizer = new Binarizer().setInputCol("label").setOutputCol("labelBin").setThreshold(0.5)
    val indexedTESTwithCatFeatBinTarget = binarizer.transform(indexedTrainwithCatFeat)

    # CATEGORIZE FEATURES FOR hello REGRESSION PROBLEM
    # CREATE PROPERLY INDEXED AND CATEGORIZED DATA FRAMES FOR TREE-BASED MODELS

    # TRAIN DATA
    val indexer = new VectorIndexer().setInputCol("features").setOutputCol("featuresCat").setMaxCategories(32)
    val indexerModel = indexer.fit(indexedTRAINregDF)
    val indexedTRAINwithCatFeat = indexerModel.transform(indexedTRAINregDF)

    # TEST DATA
    val indexerModel = indexer.fit(indexedTESTbinaryDF)
    val indexedTESTwithCatFeat = indexerModel.transform(indexedTESTregDF)



## <a name="binary-classification-model-predict-whether-a-tip-should-be-paid"></a>İkili sınıflandırma modeli: bir ipucu Ücretli olup olmadığını tahmin etme
Bu bölümde, bir ipucu Ücretli desteklemediğini ikili sınıflandırma modelleri toopredict üç tür oluşturun:

* A **Lojistik regresyon modeli** hello Spark ML kullanarak `LogisticRegression()` işlevi
* A **rastgele orman sınıflandırma modeli** hello Spark ML kullanarak `RandomForestClassifier()` işlevi
* A **gradyan artırma ağacı sınıflandırma modeli** hello Mllib'i kullanarak `GradientBoostedTrees()` işlevi

### <a name="create-a-logistic-regression-model"></a>Lojistik regresyon modeli oluşturma
Ardından, hello Spark ML kullanarak Lojistik regresyon modeli oluşturma `LogisticRegression()` işlevi. Bir dizi adımı kodda derleme hello modeli oluşturun:

1. **Tren hello modeli** bir parametre kümesi ile verileri.
2. **Merhaba modelini değerlendir** ölçümlerle sınama veri kümesi üzerinde.
3. **Merhaba modeli kaydedin** gelecekteki tüketimi için Blob Depolama birimindeki.
4. **Puan hello modeli** karşı test verileri.
5. **Merhaba sonuçları çizim** özelliği (ROC) Eğriler işletim alıcı ile.

Bu yordamları hello kodunu şöyledir:

    # CREATE A LOGISTIC REGRESSION MODEL
    val lr = new LogisticRegression().setLabelCol("tipped").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)
    val lrModel = lr.fit(OneHotTRAIN)

    # PREDICT ON hello TEST DATA SET
    val predictions = lrModel.transform(OneHotTEST)

    # SELECT `BinaryClassificationEvaluator()` tooCOMPUTE hello TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)

    # SAVE hello MODEL
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LogisticRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

Yüklemek için Puanlama ve hello sonuçları kaydedin.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD hello SAVED MODEL AND SCORE hello TEST DATA SET
    val savedModel = org.apache.spark.ml.classification.LogisticRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE hello MODEL ON hello TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tipped","probability","rawPrediction")
    predictions.registerTempTable("testResults")

    # SELECT `BinaryClassificationEvaluator()` tooCOMPUTE hello TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello ROC RESULTS
    println("ROC on test data = " + ROC)


**Çıktı:**

Test verileri ROC 0.9827381497557599 =

Python yerel Pandas veri çerçeveleri tooplot hello ROC eğrisi üzerinde kullanın.

    # QUERY hello RESULTS
    %%sql -q -o sqlResults
    SELECT tipped, probability from testResults


    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    sqlResults['probFloat'] = sqlResults.apply(lambda row: row['probability'].values()[0][1], axis=1)
    predictions_pddf = sqlResults[["tipped","probFloat"]]

    # PREDICT hello ROC CURVE
    # predictions_pddf = sqlResults.rename(columns={'_1': 'probability', 'tipped': 'label'})
    prob = predictions_pddf["probFloat"]
    fpr, tpr, thresholds = roc_curve(predictions_pddf['tipped'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT hello ROC CURVE
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


**Çıktı:**

![İpucu veya hiçbir ipucu ROC eğrisi](./media/machine-learning-data-science-process-scala-walkthrough/plot-roc-curve-tip-or-not.png)

### <a name="create-a-random-forest-classification-model"></a>Rastgele orman sınıflandırma modeli oluşturma
Ardından, hello Spark ML kullanarak bir rastgele orman sınıflandırma modeli oluşturma `RandomForestClassifier()` işlev ve test verileri hello modeli değerlendirin.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE hello RANDOM FOREST CLASSIFIER MODEL
    val rf = new RandomForestClassifier().setLabelCol("labelBin").setFeaturesCol("featuresCat").setNumTrees(10).setSeed(1234)

    # FIT hello MODEL
    val rfModel = rf.fit(indexedTRAINwithCatFeatBinTarget)
    val predictions = rfModel.transform(indexedTESTwithCatFeatBinTarget)

    # EVALUATE hello MODEL
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(predictions)
    println("F1 score on test data: " + Test_f1Score);

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # CALCULATE BINARY CLASSIFICATION EVALUATION METRICS
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("label").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)


**Çıktı:**

Test verileri ROC 0.9847103571552683 =

### <a name="create-a-gbt-classification-model"></a>GBT sınıflandırma modeli oluşturma
Ardından, Mllib'i'nın kullanarak GBT sınıflandırma modeli oluşturma `GradientBoostedTrees()` işlev ve test verileri hello modeli değerlendirin.

    # TRAIN A GBT CLASSIFICATION MODEL BY USING MLLIB AND A LABELED POINT

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello GBT CLASSIFICATION MODEL
    val boostingStrategy = BoostingStrategy.defaultParams("Classification")
    boostingStrategy.numIterations = 20
    boostingStrategy.treeStrategy.numClasses = 2
    boostingStrategy.treeStrategy.maxDepth = 5
    boostingStrategy.treeStrategy.categoricalFeaturesInfo = Map[Int, Int]((0,2),(1,2),(2,6),(3,4))

    # TRAIN hello MODEL
    val gbtModel = GradientBoostedTrees.train(indexedTRAINbinary, boostingStrategy)

    # SAVE hello MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "GBT_Classification__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    gbtModel.save(sc, filename);

    # EVALUATE hello MODEL ON TEST INSTANCES AND hello COMPUTE TEST ERROR
    val labelAndPreds = indexedTESTbinary.map { point =>
      val prediction = gbtModel.predict(point.features)
      (point.label, prediction)
    }
    val testErr = labelAndPreds.filter(r => r._1 != r._2).count.toDouble / indexedTRAINbinary.count()
    //println("Learned classification GBT model:\n" + gbtModel.toDebugString)
    println("Test Error = " + testErr)

    # USE BINARY AND MULTICLASS METRICS tooEVALUATE hello MODEL ON hello TEST DATA
    val metrics = new MulticlassMetrics(labelAndPreds)
    println(s"Precision: ${metrics.precision}")
    println(s"Recall: ${metrics.recall}")
    println(s"F1 Score: ${metrics.fMeasure}")

    val metrics = new BinaryClassificationMetrics(labelAndPreds)
    println(s"Area under PR curve: ${metrics.areaUnderPR}")
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello ROC METRIC
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")


**Çıktı:**

ROC eğrisi alanında: 0.9846895479241554

## <a name="regression-model-predict-tip-amount"></a>Regresyon modeli: ipucu miktarı tahmin etmek
Bu bölümde, iki tür regresyon modeli toopredict hello ipucu tutar oluşturun:

* A **regularized doğrusal regresyon modeli** hello Spark ML kullanarak `LinearRegression()` işlevi. Hello modeli kaydedin ve test verileri hello modelini değerlendir.
* A **gradyan artırmanın ağacı regresyon modeli** hello Spark ML kullanarak `GBTRegressor()` işlevi.

### <a name="create-a-regularized-linear-regression-model"></a>Regularized doğrusal regresyon modelini oluşturma
    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE A REGULARIZED LINEAR REGRESSION MODEL BY USING hello SPARK ML FUNCTION AND DATA FRAMES
    val lr = new LinearRegression().setLabelCol("tip_amount").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)

    # FIT hello MODEL BY USING DATA FRAMES
    val lrModel = lr.fit(OneHotTRAIN)
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SUMMARIZE hello MODEL OVER hello TRAINING SET AND PRINT METRICS
    val trainingSummary = lrModel.summary
    println(s"numIterations: ${trainingSummary.totalIterations}")
    println(s"objectiveHistory: ${trainingSummary.objectiveHistory.toList}")
    trainingSummary.residuals.show()
    println(s"RMSE: ${trainingSummary.rootMeanSquaredError}")
    println(s"r2: ${trainingSummary.r2}")

    # SAVE hello MODEL IN AZURE BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LinearRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

    # PRINT hello COEFFICIENTS
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SCORE hello MODEL ON TEST DATA
    val predictions = lrModel.transform(OneHotTEST)

    # EVALUATE hello MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Çıktı:**

Zaman toorun hello hücre: 13 saniye.

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM BLOB STORAGE AND SCORE A TEST DATA SET

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM AZURE BLOB STORAGE
    val savedModel = org.apache.spark.ml.regression.LinearRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE hello MODEL ON TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tip_amount","prediction")
    predictions.registerTempTable("testResults")

    # EVALUATE hello MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello RESULTS
    println("R-sqr on test data = " + r2)


**Çıktı:**

R-sqr test verileri 0.5960320470835743 =

Ardından, sorgu hello test veri çerçevesi ve kullanım AutoVizWidget ve matplotlib toovisualize bunu sonuçlanır.

    # RUN A SQL QUERY
    %%sql -q -o sqlResults
    select * from testResults

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, AND SO ON)
    sqlResults

Merhaba kod yerel veri çerçeve hello sorgu çıktısı oluşturur ve hello veri çizer. Merhaba `%%local` Sihirli oluşturur yerel veri çerçeve `sqlResults`, hangi tooplot matplotlib ile kullanabilirsiniz.

> [!NOTE]
> Bu Spark Sihirli birden çok kez bu makalede kullanılır. Merhaba miktarda veri büyükse, toocreate yerel belleğe sığması veri çerçevesi örnek.
> 
> 

Çizimler, Python matplotlib kullanarak oluşturun.

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    sqlResults
    %matplotlib inline
    import numpy as np

    # PLOT hello RESULTS
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='tip_amount', y='prediction', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['tip_amount'], sqlResults['prediction'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    #ax.plot(sqlResults['tip_amount'], fit[0] * sqlResults['prediction'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 8])
    plt.show(ax)

**Çıktı:**

![Tutar İpucu: Gerçek ve tahmin edilen](./media/machine-learning-data-science-process-scala-walkthrough/plot-actual-vs-predicted-tip-amount.png)

### <a name="create-a-gbt-regression-model"></a>Bir GBT regresyon modeli oluşturma
Merhaba Spark ML kullanarak bir GBT regresyon modeli oluşturma `GBTRegressor()` işlev ve test verileri hello modeli değerlendirin.

[Gradyan boosted ağaçları](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) olan karar ağaçları ensembles. GBTs tren karar tekrarlayarak toominimize kaybı işlevi ağaçları. GBTs regresyon ve sınıflandırma için kullanabilirsiniz. Bunlar kategorik özellikleri işleyebilir, özellik ölçeklendirme gerektirmez ve nonlinearities ve özellik etkileşimleri yakalayabilirsiniz. Bunları bir sınıflandırma veya çoklu sınıflar ayarını da kullanabilirsiniz.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # TRAIN A GBT REGRESSION MODEL
    val gbt = new GBTRegressor().setLabelCol("label").setFeaturesCol("featuresCat").setMaxIter(10)
    val gbtModel = gbt.fit(indexedTRAINwithCatFeat)

    # MAKE PREDICTIONS
    val predictions = gbtModel.transform(indexedTESTwithCatFeat)

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(predictions)


    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello RESULTS
    println("Test R-sqr is: " + Test_R2);


**Çıktı:**

Test R-sqr olduğu: 0.7655383534596654

## <a name="advanced-modeling-utilities-for-optimization"></a>En iyi duruma getirme için Gelişmiş modelleme yardımcı programları
Bu bölümde, geliştiricilerin modeli iyileştirme için sık kullandığınız machine learning yardımcı programlarını kullanın. Özellikle, makine öğrenimi modellerini üç farklı yolla parametre Süpürme ve çapraz doğrulama kullanarak en iyi duruma getirebilirsiniz:

* Tren ve doğrulama kümeleri bölünmüş hello verileri eğitim kümesinde hyper-parametre Süpürme kullanarak hello modeli iyileştirmek ve doğrulama kümesinde (doğrusal regresyon) değerlendir
* Çapraz doğrulama ve hyper-Spark ML'ın CrossValidator işlevi (ikili sınıflandırma) kullanarak yerleştirmez parametresini kullanarak Hello modeli en iyi duruma getirme
* İşlev ve parametre kümesi (doğrusal regresyon) öğrenme herhangi bir makineye özel çapraz doğrulama ve parametre Süpürme kod toouse kullanarak Hello modeli en iyi duruma getirme

**Çapraz doğrulama** ne kadar iyi bilinen bir veri kümesi üzerinde eğitilmiş bir model veri kümeleri üzerinde onu eğitilmedi toopredict hello özelliklerini generalize değerlendirir bir tekniktir. Merhaba genel Bu teknik arkasındaki bir model bilinen veri bir veri kümesinde eğitildi ve ardından hello doğruluğu kendi tahminleri, bağımsız bir veri kümesi karşı test edilmiştir olur. Bir ortak toodivide bir veri kümesine uygulamasıdır *k*-Katlama ve hepsini şekilde hello Katlama biri dışındaki tüm hello modeli eğitmek.

**Hyper-parametre iyileştirme** kümesiyle bir ölçü bağımsız bir veri kümesi üzerinde hello algoritması'nın performansını en iyi duruma getirme genellikle hello amacı hyper-parametrelerini bir öğrenme algoritması seçme hello sorunudur. Parametre hyper hello model eğitim yordamı dışında belirtmelisiniz bir değerdir. Hyper-parametre değerleri hakkında varsayımlar hello esneklik ve hello modeli doğruluğunu etkileyebilir. Karar ağaçları gibi Hello derinliği ve hello ağacında bırakır sayısı istenen hyper-parametreleri, örneğin, sahip. Destek vektör makinesi (SVM) misclassification cezası terim ayarlamanız gerekir.

Ortak bir şekilde tooperform parametresi hyper iyileştirme toouse bir kılavuz arama olarak da bilinir bir **parametresi tarama**. Bir kılavuz aramada ayrıntılı aramasını hello hyper-parametre alan bir öğrenme algoritması için belirtilen bir alt hello değerlerini aracılığıyla gerçekleştirilir. Çapraz doğrulama performans ölçüm toosort hello kılavuz arama algoritması tarafından üretilen hello verimle çıkışı sağlayabilir. Çapraz doğrulama parametre hyper Süpürme kullanırsanız, bir model tootraining verileri overfitting gibi sınırı sorunları yardımcı olabilir. Bu şekilde hello modeli hello kapasite tooapply toohello genel hangi hello eğitim verileri ayıklandı veri kümesini korur.

### <a name="optimize-a-linear-regression-model-with-hyper-parameter-sweeping"></a>Doğrusal regresyon modeli parametre hyper Süpürme ile en iyi duruma getirme
Ardından, veri eğitimi ve doğrulama ayarlar bölme, kullanım hyper-üzerinde bir eğitim yerleştirmez parametre toooptimize hello modelini ayarlamak ve doğrulama kümesinde (doğrusal regresyon) değerlendir.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # RENAME `tip_amount` AS A LABEL
    val OneHotTRAINLabeled = OneHotTRAIN.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    val OneHotTESTLabeled = OneHotTEST.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    OneHotTRAINLabeled.cache()
    OneHotTESTLabeled.cache()

    # DEFINE hello ESTIMATOR FUNCTION: `hello LinearRegression()` FUNCTION
    val lr = new LinearRegression().setLabelCol("label").setFeaturesCol("features").setMaxIter(10)

    # DEFINE hello PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(lr.regParam, Array(0.1, 0.01, 0.001)).addGrid(lr.fitIntercept).addGrid(lr.elasticNetParam, Array(0.1, 0.5, 0.9)).build()

    # DEFINE hello PIPELINE WITH A TRAIN/TEST VALIDATION SPLIT (75% IN hello TRAINING SET), AND THEN hello SPECIFY ESTIMATOR, EVALUATOR, AND PARAMETER GRID
    val trainPct = 0.75
    val trainValidationSplit = new TrainValidationSplit().setEstimator(lr).setEvaluator(new RegressionEvaluator).setEstimatorParamMaps(paramGrid).setTrainRatio(trainPct)

    # RUN hello TRAIN VALIDATION SPLIT AND CHOOSE hello BEST SET OF PARAMETERS
    val model = trainValidationSplit.fit(OneHotTRAINLabeled)

    # MAKE PREDICTIONS ON hello TEST DATA BY USING hello MODEL WITH hello COMBINATION OF PARAMETERS THAT PERFORMS hello BEST
    val testResults = model.transform(OneHotTESTLabeled).select("label", "prediction")

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(testResults)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    println("Test R-sqr is: " + Test_R2);


**Çıktı:**

Test R-sqr olduğu: 0.6226484708501209

### <a name="optimize-hello-binary-classification-model-by-using-cross-validation-and-hyper-parameter-sweeping"></a>Çapraz doğrulama ve parametre hyper Süpürme kullanarak Hello ikili sınıflandırma modeli en iyi duruma getirme
Bu bölümde, nasıl toooptimize ikili sınıflandırma model çapraz doğrulama ve parametre hyper Süpürme kullanarak gösterir. Bu hello Spark ML kullanır `CrossValidator` işlevi.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE DATA FRAMES WITH PROPERLY LABELED COLUMNS tooUSE WITH hello TRAIN AND TEST SPLIT
    val indexedTRAINwithCatFeatBinTargetRF = indexedTRAINwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    val indexedTESTwithCatFeatBinTargetRF = indexedTESTwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    indexedTRAINwithCatFeatBinTargetRF.cache()
    indexedTESTwithCatFeatBinTargetRF.cache()

    # DEFINE hello ESTIMATOR FUNCTION
    val rf = new RandomForestClassifier().setLabelCol("label").setFeaturesCol("features").setImpurity("gini").setSeed(1234).setFeatureSubsetStrategy("auto").setMaxBins(32)

    # DEFINE hello PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(4,8)).addGrid(rf.numTrees, Array(5,10)).addGrid(rf.minInstancesPerNode, Array(100,300)).build()

    # SPECIFY hello NUMBER OF FOLDS
    val numFolds = 3

    # DEFINE hello TRAIN/TEST VALIDATION SPLIT (75% IN hello TRAINING SET)
    val CrossValidator = new CrossValidator().setEstimator(rf).setEvaluator(new BinaryClassificationEvaluator).setEstimatorParamMaps(paramGrid).setNumFolds(numFolds)

    # RUN hello TRAIN VALIDATION SPLIT AND CHOOSE hello BEST SET OF PARAMETERS
    val model = CrossValidator.fit(indexedTRAINwithCatFeatBinTargetRF)

    # MAKE PREDICTIONS ON hello TEST DATA BY USING hello MODEL WITH hello COMBINATION OF PARAMETERS THAT PERFORMS hello BEST
    val testResults = model.transform(indexedTESTwithCatFeatBinTargetRF).select("label", "prediction")

    # COMPUTE hello TEST F1 SCORE
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(testResults)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**Çıktı:**

Zaman toorun hello hücre: 33 saniye.

### <a name="optimize-hello-linear-regression-model-by-using-custom-cross-validation-and-parameter-sweeping-code"></a>Özel çapraz doğrulama ve parametre Süpürme kod kullanarak Hello doğrusal regresyon modeli en iyi duruma getirme
Ardından, özel kod kullanarak hello modeli iyileştirmek ve en yüksek doğruluk hello ölçütünü kullanarak hello en iyi modeli parametreleri tanımlayın. Ardından, hello son model oluşturun, test verileri hello modeli değerlendirin ve Blob depolama alanına hello modeli kaydedin. Son olarak, hello modeli yüklemek için test verileri puan ve doğruluk değerlendirin.

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello PARAMETER GRID AND hello NUMBER OF FOLDS
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(5,10)).addGrid(rf.numTrees, Array(10,25,50)).build()

    val nFolds = 3
    val numModels = paramGrid.size
    val numParamsinGrid = 2

    # SPECIFY hello NUMBER OF CATEGORIES FOR CATEGORICAL VARIABLES
    val categoricalFeaturesInfo = Map[Int, Int]((0,2),(1,2),(2,6),(3,4))

    var maxDepth = -1
    var numTrees = -1
    var param = ""
    var paramval = -1
    var validateLB = -1.0
    var validateUB = -1.0
    val h = 1.0 / nFolds;
    val RMSE  = Array.fill(numModels)(0.0)

    # CREATE K-FOLDS
    val splits = MLUtils.kFold(indexedTRAINbinary, numFolds = nFolds, seed=1234)


    # LOOP THROUGH K-FOLDS AND hello PARAMETER GRID tooGET AND IDENTIFY hello BEST PARAMETER SET BY LEVEL OF ACCURACY
    for (i <- 0 too(nFolds-1)) {
        validateLB = i * h
        validateUB = (i + 1) * h
        val validationCV = trainData.filter($"rand" >= validateLB  && $"rand" < validateUB)
        val trainCV = trainData.filter($"rand" < validateLB  || $"rand" >= validateUB)
        val validationLabPt = validationCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        val trainCVLabPt = trainCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        validationLabPt.cache()
        trainCVLabPt.cache()

        for (nParamSets <- 0 too(numModels-1)) {
            for (nParams <- 0 too(numParamsinGrid-1)) {
                param = paramGrid(nParamSets).toSeq(nParams).param.toString.split("__")(1)
                paramval = paramGrid(nParamSets).toSeq(nParams).value.toString.toInt
                if (param == "maxDepth") {maxDepth = paramval}
                if (param == "numTrees") {numTrees = paramval}
            }
            val rfModel = RandomForest.trainRegressor(trainCVLabPt, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                      numTrees=numTrees, maxDepth=maxDepth,
                                                      featureSubsetStrategy="auto",impurity="variance", maxBins=32)
            val labelAndPreds = validationLabPt.map { point =>
                                                     val prediction = rfModel.predict(point.features)
                                                     ( prediction, point.label )
                                                    }
            val validMetrics = new RegressionMetrics(labelAndPreds)
            val rmse = validMetrics.rootMeanSquaredError
            RMSE(nParamSets) += rmse
        }
        validationLabPt.unpersist();
        trainCVLabPt.unpersist();
    }
    val minRMSEindex = RMSE.indexOf(RMSE.min)

    # GET hello BEST PARAMETERS FROM A CROSS-VALIDATION AND PARAMETER SWEEP
    var best_maxDepth = -1
    var best_numTrees = -1
    for (nParams <- 0 too(numParamsinGrid-1)) {
        param = paramGrid(minRMSEindex).toSeq(nParams).param.toString.split("__")(1)
        paramval = paramGrid(minRMSEindex).toSeq(nParams).value.toString.toInt
        if (param == "maxDepth") {best_maxDepth = paramval}
        if (param == "numTrees") {best_numTrees = paramval}
    }

    # CREATE hello BEST MODEL WITH hello BEST PARAMETERS AND A FULL TRAINING DATA SET
    val best_rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                      numTrees=best_numTrees, maxDepth=best_maxDepth,
                                                      featureSubsetStrategy="auto",impurity="variance", maxBins=32)

    # SAVE hello BEST RANDOM FOREST MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "BestCV_RF_Regression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    best_rfModel.save(sc, filename);

    # PREDICT ON hello TRAINING SET WITH hello BEST MODEL AND THEN EVALUATE
    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = best_rfModel.predict(point.features)
                                            ( prediction, point.label )
                                           }

    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


    # LOAD hello MODEL
    val savedRFModel = RandomForestModel.load(sc, filename)

    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = savedRFModel.predict(point.features)
                                            ( prediction, point.label )
                                           }
    # TEST hello MODEL
    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2


**Çıktı:**

Zaman toorun hello hücre: 61 saniye.

## <a name="consume-spark-built-machine-learning-models-automatically-with-scala"></a>Spark yerleşik makine öğrenimi modellerini Scala ile otomatik olarak kullanma
Azure'da hello veri bilimi işlemi oluşturan hello görevleri rehberlik konuları genel bakış için bkz: [takım veri bilimi işlemi](http://aka.ms/datascienceprocess).

[Ekip veri bilimi süreci gözden geçirmeleri](data-science-process-walkthroughs.md) hello adımları hello takım veri bilimi işlemi belirli senaryoları için gösteren diğer uçtan uca talimatlara açıklar. Hello izlenecek yollar da nasıl toocombine bulut göstermek ve şirket içi araçları ve akıllı bir uygulama bir iş akışı veya ardışık düzen toocreate Hizmetleri.

[Spark yerleşik machine learning modellerini puan](machine-learning-data-science-spark-model-consumption.md) nasıl toouse Scala kod tooautomatically yükleyin ve yeni veri kümeleri ile Spark oluşturulmuş ve Azure Blob depolama alanına kaydedildi machine learning modellerini puan gösterir. Var. hello yönergelerini izleyin ve yalnızca bu makalede otomatik tüketimi için Scala koduyla hello Python kodu değiştirin.

