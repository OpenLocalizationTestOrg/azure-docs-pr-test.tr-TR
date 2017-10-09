---
title: "aaaAnalyze uygulama Insight günlükleri - Azure Hdınsight Spark ile | Microsoft Docs"
description: "Hdınsight'ta Spark ile Merhaba günlüklerini çözümlemek ve tooexport uygulama Insight tooblob depolama nasıl günlüğe yazacağını öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 883beae6-9839-45b5-94f7-7eb0f4534ad5
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 11ed8cf68dba8d5f9d6e4a65eba0d2b5a950cd00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-application-insights-telemetry-logs-with-spark-on-hdinsight"></a>Application Insights telemetri günlüklerini hdınsight'ta Spark ile çözümleme

Bilgi nasıl toouse Spark Hdınsight tooanalyze uygulama Insight telemetri verileri.

[Visual Studio Application Insights](../application-insights/app-insights-overview.md) web uygulamalarınızın izleyen bir analiz hizmetidir. Application Insights tarafından oluşturulan telemetri verilerini dışa aktarılan tooAzure depolama olabilir. Merhaba verileri Azure depolama alanında olduğunda, Hdınsight kullanılan tooanalyze olabilir.

## <a name="prerequisites"></a>Ön koşullar

* Bir uygulama toouse Application Insights yapılandırılmış.

* Linux tabanlı Hdınsight kümesi oluşturma ile benzer. Daha fazla bilgi için bkz: [hdınsight'ta Spark oluşturma](hdinsight-apache-spark-jupyter-spark-sql.md).

  > [!IMPORTANT]
  > Bu belgedeki Hello adımlar Linux kullanan bir Hdınsight kümesi gerektirir. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Bir web tarayıcısı.

Merhaba aşağıdaki kaynaklar bu belgeyi test ve geliştirme de kullanılıyordu:

* Uygulama Insights telemetri verilerini kullanarak üretilen bir [Node.js web uygulamasına yapılandırılmış toouse Application Insights](../application-insights/app-insights-nodejs.md).

* Linux tabanlı bir Spark Hdınsight kümesi sürüm 3.5 üzerinde kullanılan tooanalyze hello verisi idi.

## <a name="architecture-and-planning"></a>Mimari ve planlama

Diyagram aşağıdaki hello hello hizmet mimarisi Bu örnek gösterilmektedir:

![hdınsight'ta Spark tarafından işlenmekte olan sonra Application Insights tooblob depolama biriminden akan veri gösteren diyagram](./media/hdinsight-spark-analyze-application-insight-logs/appinsightshdinsight.png)

### <a name="azure-storage"></a>Azure Storage

Application Insights yapılandırılmış toocontinuously verme telemetri bilgileri tooblobs olabilir. Hdınsight hello BLOB'ları depolanan verileri okuyabilir. Ancak, uymanız gereken bazı gereksinimler vardır:

* **Konum**: hello depolama hesabı ve Hdınsight farklı konumlarda varsa, gecikme süresini artırabilir. Çıkış ücretlerini bölgeler arasında taşıma uygulanan toodata olarak da maliyeti artırır.

    > [!WARNING]
    > Hdınsight farklı bir konumda bir depolama hesabıyla desteklenmiyor.

* **BLOB türü**: Hdınsight yalnızca blok bloblarını destekler. Application Insights Hdınsight ile varsayılan olarak çalışması gerekir böylece toousing blok blobları, varsayılan olarak ayarlanır.

Merhaba Hdınsight kümesi varolan ek depolama alanı tooan ekleme hakkında daha fazla bilgi için bkz: [ek depolama hesapları ekleme](hdinsight-hadoop-add-storage.md) belge.

### <a name="data-schema"></a>Veri şeması

Application Insights sağlar [veri modeli verme](../application-insights/app-insights-export-data-model.md) bilgi hello telemetri veri biçimi için dışa aktarılan tooblobs. Bu belgedeki Hello adımları Spark SQL toowork hello verilerle kullanın. Spark SQL, Application Insights tarafından günlüğe kaydedilen hello JSON veri yapısı için bir şema otomatik olarak oluşturabilir.

## <a name="export-telemetry-data"></a>Telemetri verileri dışarı aktarma

Merhaba adımları [yapılandırma sürekli verme](../application-insights/app-insights-export-telemetry.md) tooconfigure, Application Insights tooexport telemetri bilgileri tooan Azure depolama blob.

## <a name="configure-hdinsight-tooaccess-hello-data"></a>Hdınsight tooaccess hello verileri yapılandırma

Hdınsight kümesi oluşturuyorsanız, küme oluşturma sırasında hello depolama hesabı ekleyin.

tooadd hello Azure depolama hesabı tooan var olan küme, hello hello bilgileri kullanmak [ek depolama hesapları ekleme](hdinsight-hadoop-add-storage.md) belge.

## <a name="analyze-hello-data-pyspark"></a>Merhaba verileri çözümlemek: PySpark

1. Merhaba gelen [Azure portal](https://portal.azure.com), Hdınsight kümesinde, Spark seçin. Merhaba gelen **hızlı bağlantılar** bölümünde, select **küme panolarında**ve ardından **Jupyter not defteri** hello küme Dashboard__ dikey penceresinden.

    ![Merhaba küme panolarında](./media/hdinsight-spark-analyze-application-insight-logs/clusterdashboards.png)

2. Merhaba sağ üst köşesindeki hello Jupyter sayfa içinde seçin **yeni**ve ardından **PySpark**. Python tabanlı Jupyter not defteri içeren yeni bir tarayıcı sekmesi açar.

3. Merhaba ilk alanında (adlı bir **hücre**) hello sayfasında metin aşağıdaki hello girin:

   ```python
   sc._jsc.hadoopConfiguration().set('mapreduce.input.fileinputformat.input.dir.recursive', 'true')
   ```

    Bu kod hello giriş verileri için Spark toorecursively erişim hello dizin yapısı yapılandırır. Application Insights telemetrisi olduğundan oturum tooa dizin yapısı benzer toohello `/{telemetry type}/YYYY-MM-DD/{##}/`.

4. Kullanım **SHIFT + ENTER** toorun hello kodu. Sol hello hücre tarafı hello üzerinde bir '\*' hello köşeli tooindicate Bu hücreyi hello kodda yürütülmekte olan görüntülenir. Hello tamamlandığında '\*' değişiklikleri tooa numarası ve çıkış metnini izleyen benzer toohello altında hello hücre görüntülenir:

        Creating SparkContext as 'sc'

        ID    YARN Application ID    Kind    State    Spark UI    Driver log    Current session?
        3    application_1468969497124_0001    pyspark    idle    Link    Link    ✔

        Creating HiveContext as 'sqlContext'
        SparkContext and HiveContext created. Executing user code ...
5. Yeni bir hücre hello altında oluşturulan ilk. Metin hello yeni hücreye aşağıdaki hello girin. Değiştir `CONTAINER` ve `STORAGEACCOUNT` hello Azure depolama hesabı adı ve Application Insights verileri içeren blob kapsayıcı adı.

   ```python
   %%bash
   hdfs dfs -ls wasb://CONTAINER@STORAGEACCOUNT.blob.core.windows.net/
   ```

    Kullanım **SHIFT + ENTER** tooexecute Bu hücreyi. Metin izleyen bir sonuç benzer toohello bakın:

        Found 1 items
        drwxrwxrwx   -          0 1970-01-01 00:00 wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_2bededa61bc741fbdee6b556571a4831

    döndürülen hello wasb yol hello hello Application Insights telemetri verilerini konumudur. Değişiklik hello `hdfs dfs -ls` satır döndürülen hello hücre toouse hello wasb yolunda ve ardından **SHIFT + ENTER** toorun hello yeniden hücre. Bu süre, telemetri verilerini içeren hello dizinleri hello sonuçları görüntülemesi gerekir.

   > [!NOTE]
   > Bu bölümde hello Hello geri kalan adımları için hello `wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_{ID}/Requests` dizin kullanıldı. Dizin yapısını farklı olabilir.

6. Koddan hello Hello sonraki hücreye girin: Değiştir `WASB_PATH` hello önceki adımdaki hello yoluna sahip.

   ```python
   jsonFiles = sc.textFile('WASB_PATH')
   jsonData = sqlContext.read.json(jsonFiles)
   ```

    Bu kod bir dataframe hello sürekli dışa aktarma işlemi tarafından dışarı aktarılan hello JSON dosyaları oluşturur. Kullanım **SHIFT + ENTER** toorun Bu hücreyi.
7. Merhaba sonraki hücresindeki girin ve Spark hello JSON dosyaları için oluşturulan tooview hello şema aşağıdaki hello çalıştırın:

   ```python
   jsonData.printSchema()
   ```

    Merhaba şema telemetri her tür için farklıdır. Merhaba aşağıdaki örnekte olduğu web istekleri için oluşturulan hello şeması (hello depolanan verileri `Requests` alt dizin):

        root
        |-- context: struct (nullable = true)
        |    |-- application: struct (nullable = true)
        |    |    |-- version: string (nullable = true)
        |    |-- custom: struct (nullable = true)
        |    |    |-- dimensions: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |    |-- metrics: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- eventTime: string (nullable = true)
        |    |    |-- isSynthetic: boolean (nullable = true)
        |    |    |-- samplingRate: double (nullable = true)
        |    |    |-- syntheticSource: string (nullable = true)
        |    |-- device: struct (nullable = true)
        |    |    |-- browser: string (nullable = true)
        |    |    |-- browserVersion: string (nullable = true)
        |    |    |-- deviceModel: string (nullable = true)
        |    |    |-- deviceName: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- osVersion: string (nullable = true)
        |    |    |-- type: string (nullable = true)
        |    |-- location: struct (nullable = true)
        |    |    |-- city: string (nullable = true)
        |    |    |-- clientip: string (nullable = true)
        |    |    |-- continent: string (nullable = true)
        |    |    |-- country: string (nullable = true)
        |    |    |-- province: string (nullable = true)
        |    |-- operation: struct (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |-- session: struct (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- isFirst: boolean (nullable = true)
        |    |-- user: struct (nullable = true)
        |    |    |-- anonId: string (nullable = true)
        |    |    |-- isAuthenticated: boolean (nullable = true)
        |-- internal: struct (nullable = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- documentVersion: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |-- request: array (nullable = true)
        |    |-- element: struct (containsNull = true)
        |    |    |-- count: long (nullable = true)
        |    |    |-- durationMetric: struct (nullable = true)
        |    |    |    |-- count: double (nullable = true)
        |    |    |    |-- max: double (nullable = true)
        |    |    |    |-- min: double (nullable = true)
        |    |    |    |-- sampledValue: double (nullable = true)
        |    |    |    |-- stdDev: double (nullable = true)
        |    |    |    |-- value: double (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |    |-- responseCode: long (nullable = true)
        |    |    |-- success: boolean (nullable = true)
        |    |    |-- url: string (nullable = true)
        |    |    |-- urlData: struct (nullable = true)
        |    |    |    |-- base: string (nullable = true)
        |    |    |    |-- hashTag: string (nullable = true)
        |    |    |    |-- host: string (nullable = true)
        |    |    |    |-- protocol: string (nullable = true)
8. Tooregister hello dataframe geçici tablo olarak aşağıdaki hello kullanın ve hello veri karşı bir sorgu çalıştırın:

   ```python
   jsonData.registerTempTable("requests")
   df = sqlContext.sql("select context.location.city from requests where context.location.city is not null")
   df.show()
   ```

    Bu sorgu, burada context.location.city null olmayan hello üst 20 kayıt için hello Şehir bilgileri döndürür.

   > [!NOTE]
   > Merhaba bağlam yapısı Application Insights tarafından günlüğe kaydedilen tüm telemetri bulunur. Merhaba Şehir öğesi, günlüklerinize doldurulmuş değil. Merhaba şema tooidentify günlükleriniz için verileri içerebilir Sorgulayabileceğiniz diğer öğeleri kullanın.

    Bu sorgu metnini izleyen bilgi benzer toohello döndürür:

        +---------+
        |     city|
        +---------+
        | Bellevue|
        |  Redmond|
        |  Seattle|
        |Charlotte|
        ...
        +---------+

## <a name="analyze-hello-data-scala"></a>Merhaba verileri çözümlemek: Scala

1. Merhaba gelen [Azure portal](https://portal.azure.com), Hdınsight kümesinde, Spark seçin. Merhaba gelen **hızlı bağlantılar** bölümünde, select **küme panolarında**ve ardından **Jupyter not defteri** hello küme Dashboard__ dikey penceresinden.

    ![Merhaba küme panolarında](./media/hdinsight-spark-analyze-application-insight-logs/clusterdashboards.png)
2. Merhaba sağ üst köşesindeki hello Jupyter sayfa içinde seçin **yeni**ve ardından **Scala**. Scala tabanlı Jupyter not defteri içeren yeni bir tarayıcı sekmesi görüntülenir.
3. Merhaba ilk alanında (adlı bir **hücre**) hello sayfasında metin aşağıdaki hello girin:

   ```scala
   sc.hadoopConfiguration.set("mapreduce.input.fileinputformat.input.dir.recursive", "true")
   ```

    Bu kod hello giriş verileri için Spark toorecursively erişim hello dizin yapısı yapılandırır. Application Insights telemetri olduğundan oturum tooa dizin yapısına benzer çok`/{telemetry type}/YYYY-MM-DD/{##}/`.

4. Kullanım **SHIFT + ENTER** toorun hello kodu. Sol hello hücre tarafı hello üzerinde bir '\*' hello köşeli tooindicate Bu hücreyi hello kodda yürütülmekte olan görüntülenir. Hello tamamlandığında '\*' değişiklikleri tooa numarası ve çıkış metnini izleyen benzer toohello altında hello hücre görüntülenir:

        Creating SparkContext as 'sc'

        ID    YARN Application ID    Kind    State    Spark UI    Driver log    Current session?
        3    application_1468969497124_0001    spark    idle    Link    Link    ✔

        Creating HiveContext as 'sqlContext'
        SparkContext and HiveContext created. Executing user code ...
5. Yeni bir hücre hello altında oluşturulan ilk. Metin hello yeni hücreye aşağıdaki hello girin. Değiştir `CONTAINER` ve `STORAGEACCOUNT` hello Azure depolama hesabı adı ve Application Insights içeren blob kapsayıcı adı ile günlüğe kaydeder.

   ```scala
   %%bash
   hdfs dfs -ls wasb://CONTAINER@STORAGEACCOUNT.blob.core.windows.net/
   ```

    Kullanım **SHIFT + ENTER** tooexecute Bu hücreyi. Metin izleyen bir sonuç benzer toohello bakın:

        Found 1 items
        drwxrwxrwx   -          0 1970-01-01 00:00 wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_2bededa61bc741fbdee6b556571a4831

    döndürülen hello wasb yol hello hello Application Insights telemetri verilerini konumudur. Değişiklik hello `hdfs dfs -ls` satır döndürülen hello hücre toouse hello wasb yolunda ve ardından **SHIFT + ENTER** toorun hello yeniden hücre. Bu süre, telemetri verilerini içeren hello dizinleri hello sonuçları görüntülemesi gerekir.

   > [!NOTE]
   > Bu bölümde hello Hello geri kalan adımları için hello `wasb://appinsights@contosostore.blob.core.windows.net/contosoappinsights_{ID}/Requests` dizin kullanıldı. Bir web uygulaması için telemetri verilerinizi olmadığı sürece bu dizinin var olmayabilir.

6. Koddan hello Hello sonraki hücreye girin: Değiştir `WASB\_PATH` hello önceki adımdaki hello yoluna sahip.

   ```scala
   var jsonFiles = sc.textFile('WASB_PATH')
   val sqlContext = new org.apache.spark.sql.SQLContext(sc)
   var jsonData = sqlContext.read.json(jsonFiles)
   ```

    Bu kod bir dataframe hello sürekli dışa aktarma işlemi tarafından dışarı aktarılan hello JSON dosyaları oluşturur. Kullanım **SHIFT + ENTER** toorun Bu hücreyi.

7. Merhaba sonraki hücresindeki girin ve Spark hello JSON dosyaları için oluşturulan tooview hello şema aşağıdaki hello çalıştırın:

   ```scala
   jsonData.printSchema
   ```

    Merhaba şema telemetri her tür için farklıdır. Merhaba aşağıdaki örnekte olduğu web istekleri için oluşturulan hello şeması (hello depolanan verileri `Requests` alt dizin):

        root
        |-- context: struct (nullable = true)
        |    |-- application: struct (nullable = true)
        |    |    |-- version: string (nullable = true)
        |    |-- custom: struct (nullable = true)
        |    |    |-- dimensions: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |    |-- metrics: array (nullable = true)
        |    |    |    |-- element: string (containsNull = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- eventTime: string (nullable = true)
        |    |    |-- isSynthetic: boolean (nullable = true)
        |    |    |-- samplingRate: double (nullable = true)
        |    |    |-- syntheticSource: string (nullable = true)
        |    |-- device: struct (nullable = true)
        |    |    |-- browser: string (nullable = true)
        |    |    |-- browserVersion: string (nullable = true)
        |    |    |-- deviceModel: string (nullable = true)
        |    |    |-- deviceName: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- osVersion: string (nullable = true)
        |    |    |-- type: string (nullable = true)
        |    |-- location: struct (nullable = true)
        |    |    |-- city: string (nullable = true)
        |    |    |-- clientip: string (nullable = true)
        |    |    |-- continent: string (nullable = true)
        |    |    |-- country: string (nullable = true)
        |    |    |-- province: string (nullable = true)
        |    |-- operation: struct (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |-- session: struct (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- isFirst: boolean (nullable = true)
        |    |-- user: struct (nullable = true)
        |    |    |-- anonId: string (nullable = true)
        |    |    |-- isAuthenticated: boolean (nullable = true)
        |-- internal: struct (nullable = true)
        |    |-- data: struct (nullable = true)
        |    |    |-- documentVersion: string (nullable = true)
        |    |    |-- id: string (nullable = true)
        |-- request: array (nullable = true)
        |    |-- element: struct (containsNull = true)
        |    |    |-- count: long (nullable = true)
        |    |    |-- durationMetric: struct (nullable = true)
        |    |    |    |-- count: double (nullable = true)
        |    |    |    |-- max: double (nullable = true)
        |    |    |    |-- min: double (nullable = true)
        |    |    |    |-- sampledValue: double (nullable = true)
        |    |    |    |-- stdDev: double (nullable = true)
        |    |    |    |-- value: double (nullable = true)
        |    |    |-- id: string (nullable = true)
        |    |    |-- name: string (nullable = true)
        |    |    |-- responseCode: long (nullable = true)
        |    |    |-- success: boolean (nullable = true)
        |    |    |-- url: string (nullable = true)
        |    |    |-- urlData: struct (nullable = true)
        |    |    |    |-- base: string (nullable = true)
        |    |    |    |-- hashTag: string (nullable = true)
        |    |    |    |-- host: string (nullable = true)
        |    |    |    |-- protocol: string (nullable = true)

8. Tooregister hello dataframe geçici tablo olarak aşağıdaki hello kullanın ve hello veri karşı bir sorgu çalıştırın:

   ```scala
   jsonData.registerTempTable("requests")
   var city = sqlContext.sql("select context.location.city from requests where context.location.city is not null limit 10").show()
   ```

    Bu sorgu, burada context.location.city null olmayan hello üst 20 kayıt için hello Şehir bilgileri döndürür.

   > [!NOTE]
   > Merhaba bağlam yapısı Application Insights tarafından günlüğe kaydedilen tüm telemetri bulunur. Merhaba Şehir öğesi, günlüklerinize doldurulmuş değil. Merhaba şema tooidentify günlükleriniz için verileri içerebilir Sorgulayabileceğiniz diğer öğeleri kullanın.
   >
   >

    Bu sorgu metnini izleyen bilgi benzer toohello döndürür:

        +---------+
        |     city|
        +---------+
        | Bellevue|
        |  Redmond|
        |  Seattle|
        |Charlotte|
        ...
        +---------+

## <a name="next-steps"></a>Sonraki adımlar

Veriler ve Azure Hizmetleri ile Spark toowork kullanarak daha fazla örnekler için aşağıdaki belgeleri hello bakın:

* [BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme](hdinsight-apache-spark-use-bi-tools.md)
* [Machine Learning ile Spark: HVAC verilerini kullanarak bina sıcaklığını çözümlemek için HDInsight’ta Spark kullanma](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Machine Learning ile Spark: Spark Hdınsight toopredict yemek İnceleme sonuçlarını içinde kullanma](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark akış: Akış uygulamaları oluşturmak için hdınsight'ta Spark kullanma](hdinsight-apache-spark-eventhub-streaming.md)
* [HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi](hdinsight-apache-spark-custom-library-website-log-analysis.md)

Oluşturma ve Spark çalışan uygulamalar hakkında daha fazla bilgi için aşağıdaki belgeleri hello bakın:

* [Scala kullanarak tek başına uygulama oluşturma](hdinsight-apache-spark-create-standalone-application.md)
* [Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma](hdinsight-apache-spark-livy-rest-interface.md)
