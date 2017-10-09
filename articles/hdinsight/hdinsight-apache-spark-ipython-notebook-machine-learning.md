---
title: "Azure Hdınsight uygulamaları öğrenme aaaBuild Apache Spark machine | Microsoft Docs"
description: "Adım adım yönergeler Jupyter Not Defteri kullanarak nasıl uygulama Hdınsight Spark üzerinde öğrenme toobuild Apache Spark makine kümeleri"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f584ca5e-abee-4b7c-ae58-2e45dfc56bf4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: 332bd89876f7ebf178f7573d6018d064edfe9a8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="build-apache-spark-machine-learning-applications-on-azure-hdinsight"></a>Azure hdınsight'ta Apache Spark machine learning uygulamaları derleme

Nasıl toobuild bir Spark kullanarak Apache Spark machine learning uygulama küme Hdınsight'ta öğrenin. Bu makalede nasıl toouse Jupyter not defteri ile Merhaba küme toobuild kullanılabilir hello ve bu uygulamayı test gösterilmektedir. Merhaba uygulaması varsayılan olarak tüm kümelerde kullanılabilir hello örnek HVAC.csv verileri kullanır.

**Ön koşullar:**

Merhaba şunlara sahip olmanız gerekir:

* Hdınsight'ta bir Apache Spark kümesi. Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md). 

## <a name="data"></a>Merhaba veri kümesi anlama
Bize hello uygulaması oluşturmaya başlamadan önce biz Merhaba uygulaması gerçekleştiririz analiz hello tür hello verileri yapı ve hello verilerin hello yapısını anlayın. 

Bu makalede, kullandığımız hello örnek **HVAC.csv** hello hello Hdınsight kümesi ile ilişkili Azure depolama hesabı kullanılabilir veri dosyası. Merhaba dosya altındadır Hello depolama hesabında **\HdiSamples\HdiSamples\SensorSampleData\hvac**. İndirip hello CSV dosyası tooget hello verilerin bir anlık görüntüsünü açın.  

![Spark machine learning örnek için kullanılan verilerin anlık görüntüsünü](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Spark machine learning örnek için kullanılan verilerin anlık görüntüsünü")

Merhaba verileri hello hedef sıcaklık ve hello gerçek HVAC sistemleri yüklü olan bir bina sıcaklığını gösterir. Merhaba varsayalım **sistem** sütunu temsil eder hello sistem Kimliğini ve hello **SystemAge** sütun hello hello HVAC sistem hello yapı yerinde açıldı yıl sayısını temsil eder.

Bir yapı sistem Kimliğini ve sistem yaş verilen hello hedef sıcaklık üzerinde hotter veya colder tabanlı gerektirmeyeceğini bu verileri toopredict kullanırız.

## <a name="app"></a>Spark Mllib'i kullanarak Spark machine learning uygulaması yazma
Bu uygulamada Spark ML ardışık düzen tooperform bir belge sınıflandırma kullanırız. Merhaba ardışık düzeninde biz sözcüklere hello belgeyi bölme, bir sayısal özellik vektör hello sözcükleri dönüştürme ve son olarak hello özelliği vektörlerinin ve etiketleri kullanarak bir tahmin modeli yapı. Aşağıdaki adımları toocreate Merhaba uygulaması hello gerçekleştirin.

1. Merhaba gelen [Azure Portal](https://portal.azure.com/), (, onu toohello Sabitle) hello Panosu'ndan hello kutucuğuna Spark kümenizin tıklayın. Tooyour küme altında da gidebilirsiniz **tümüne Gözat** > **Hdınsight kümeleri**.   
2. Merhaba Spark kümesi dikey penceresinden tıklatın **küme Panosu**ve ardından **Jupyter not defteri**. İstenirse, hello küme için hello yönetici kimlik bilgilerini girin.
   
   > [!NOTE]
   > Kümenizin açma hello tarayıcınızda URL aşağıdaki tarafından hello Jupyter Not Defteri de ulaşabilir. Değiştir **CLUSTERNAME** kümenizi hello adı:
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 
3. Yeni bir not defteri oluşturun. **Yeni** ve ardından **PySpark** seçeneğine tıklayın.
   
    ![Spark machine learning örneğin Jupyter not defteri oluşturma](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Spark machine learning örneğin Jupyter not defteri oluşturma")
4. Yeni bir not defteri oluşturulur ve Untitled.pynb hello adı ile. Merhaba üstünde Hello dizüstü bilgisayar adına tıklayın ve kolay bir ad girin.
   
    ![Spark machine learning örnek için bir not defteri ad](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Spark machine learning örneğin Not defteri adını belirtin")
5. Merhaba PySpark çekirdeği kullanarak bir not defteri oluşturduğunuz için siz toocreate bir bağlam açıkça gerekmez. Merhaba birinci kod hücresini çalıştırdığınızda Spark ve Hive bağlamları hello otomatik olarak sizin için oluşturulur. Bu senaryo için gerekli olan hello türleri içeri aktararak işleme başlayabilirsiniz. Boş bir hücre parçacığında aşağıdaki hello yapıştırın ve tuşuna basın **SHIFT + ENTER**. 
   
        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
   
        import os
        import sys
        from pyspark.sql.types import *
   
        from pyspark.mllib.classification import LogisticRegressionWithSGD
        from pyspark.mllib.regression import LabeledPoint
        from numpy import array
6. Şimdi hello verileri (hvac.csv) yüklemek, bunu ayrıştırabilir ve gerekir tootrain hello modeli kullanır. Bunun için hello gerçek hello bina sıcaklığını hello hedef sıcaklık büyük olup olmadığını denetler bir işlev tanımlayın. Merhaba gerçek sıcaklık büyük hello yapı hello değeri tarafından belirtilen hareketli, ise, **1.0**. Merhaba gerçek sıcaklık küçük hello yapı hello değeri tarafından belirtilen soğuk, ise, **0,0**. 
   
    Boş bir hücre ve tuşuna parçacığında aşağıdaki Yapıştır hello **SHIFT + ENTER**.

        # List hello structure of data for better understanding. Because hello data will be
        # loaded as an array, this structure makes it easy toounderstand what each element
        # in hello array corresponds to

        # 0 Date
        # 1 Time
        # 2 TargetTemp
        # 3 ActualTemp
        # 4 System
        # 5 SystemAge
        # 6 BuildingID

        LabeledDocument = Row("BuildingID", "SystemInfo", "label")

        # Define a function that parses hello raw CSV file and returns an object of type LabeledDocument

        def parseDocument(line):
            values = [str(x) for x in line.split(',')]
            if (values[3] > values[2]):
                hot = 1.0
            else:
                hot = 0.0        

            textValue = str(values[4]) + " " + str(values[5])

            return LabeledDocument((values[6]), textValue, hot)

        # Load hello raw HVAC.csv file, parse it using hello function
        data = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        documents = data.filter(lambda s: "Date" not in s).map(parseDocument)
        training = documents.toDF()


1. Üç aşamadan oluşur hello Spark machine learning ardışık düzenini yapılandırın: belirteç Oluşturucu, hashingTF ve lr. İşlem hattı nedir ve bakın nasıl çalıştığı hakkında daha fazla bilgi için <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark machine learning ardışık</a>.
   
    Boş bir hücre ve tuşuna parçacığında aşağıdaki Yapıştır hello **SHIFT + ENTER**.
   
        tokenizer = Tokenizer(inputCol="SystemInfo", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
        lr = LogisticRegression(maxIter=10, regParam=0.01)
        pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])
2. Uygun hello ardışık düzen toohello eğitim belgesi. Boş bir hücre ve tuşuna parçacığında aşağıdaki Yapıştır hello **SHIFT + ENTER**.
   
        model = pipeline.fit(training)
3. Merhaba eğitim belge toocheckpoint hello uygulamayla ilerleme durumunuzu doğrulayın. Boş bir hücre ve tuşuna parçacığında aşağıdaki Yapıştır hello **SHIFT + ENTER**.
   
        training.show()
   
    Bu hello çıkış benzer toohello aşağıdaki vermeniz gerekir:
   
        +----------+----------+-----+
        |BuildingID|SystemInfo|label|
        +----------+----------+-----+
        |         4|     13 20|  0.0|
        |        17|      3 20|  0.0|
        |        18|     17 20|  1.0|
        |        15|      2 23|  0.0|
        |         3|      16 9|  1.0|
        |         4|     13 28|  0.0|
        |         2|     12 24|  0.0|
        |        16|     20 26|  1.0|
        |         9|      16 9|  1.0|
        |        12|       6 5|  0.0|
        |        15|     10 17|  1.0|
        |         7|      2 11|  0.0|
        |        15|      14 2|  1.0|
        |         6|       3 2|  0.0|
        |        20|     19 22|  0.0|
        |         8|     19 11|  0.0|
        |         6|      15 7|  0.0|
        |        13|      12 5|  0.0|
        |         4|      8 22|  0.0|
        |         7|      17 5|  0.0|
        +----------+----------+-----+

    Geri dönün ve hello çıktı hello ham CSV dosyası karşı doğrulayın. Örneğin, bu veri hello ilk satır hello CSV dosyası sahiptir:

    ![Çıkış Spark machine learning örnek için anlık görüntü verileri](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Spark machine learning örnek için çıktı veri anlık görüntüsü")

    Merhaba yapı öneren hello hedef sıcaklık soğuk küçüktür hello gerçek sıcaklık nasıl olduğuna dikkat edin. Bu nedenle hello eğitim çıktısında değeri hello **etiket** hello ilk satırıdır **0,0**, yani hello yapı etkin değil.

1. Veri kümesi toorun hello eğitilen model karşı hazırlayın. toodo bu nedenle, biz bir sistem Kimliğini ve sistem yaş geçip geçmeyeceğini (olarak gösterilen **SystemInfo** hello eğitim çıkışı), ve hello modeli tahmin olup hello hotter (gösterilir tarafından 1.0) Bu sistem Kimliğini ve sistem geçerlilik süresi ile oluşturduğunuz veya için ( 0,0 tarafından gösterilen).
   
   Boş bir hücre ve tuşuna parçacığında aşağıdaki Yapıştır hello **SHIFT + ENTER**.
   
       # SystemInfo here is a combination of system ID followed by system age
       Document = Row("id", "SystemInfo")
       test = sc.parallelize([(1L, "20 25"),
                     (2L, "4 15"),
                     (3L, "16 9"),
                     (4L, "9 22"),
                     (5L, "17 10"),
                     (6L, "7 22")]) \
           .map(lambda x: Document(*x)).toDF() 
2. Son olarak, hello test verileri üzerindeki tahminlerde. Boş bir hücre ve tuşuna parçacığında aşağıdaki Yapıştır hello **SHIFT + ENTER**.
   
        # Make predictions on test documents and print columns of interest
        prediction = model.transform(test)
        selected = prediction.select("SystemInfo", "prediction", "probability")
        for row in selected.collect():
            print row
3. Bir çıkış benzer toohello aşağıdaki görmeniz gerekir:
   
       Row(SystemInfo=u'20 25', prediction=1.0, probability=DenseVector([0.4999, 0.5001]))
       Row(SystemInfo=u'4 15', prediction=0.0, probability=DenseVector([0.5016, 0.4984]))
       Row(SystemInfo=u'16 9', prediction=1.0, probability=DenseVector([0.4785, 0.5215]))
       Row(SystemInfo=u'9 22', prediction=1.0, probability=DenseVector([0.4549, 0.5451]))
       Row(SystemInfo=u'17 10', prediction=1.0, probability=DenseVector([0.4925, 0.5075]))
       Row(SystemInfo=u'7 22', prediction=0.0, probability=DenseVector([0.5015, 0.4985]))
   
   İlk satırdaki Hello hello tahmin içinde kimliği 20 ve 25 yıllık sistem geçerlilik süresi ile bir HVAC sistemi için hello yapı etkin olacağını görebilirsiniz (**tahmin = 1.0**). Merhaba ilk değer DenseVector (0.49999) için toohello tahmin 0,0 karşılık gelir ve hello ikinci değer (0.5001) toohello tahmin 1.0 karşılık gelir. Merhaba çıktısında hello ikinci değer yalnızca fazladır daha yüksek olmasına rağmen hello modelini gösteren **tahmin = 1.0**.
4. Merhaba uygulaması çalıştıran bitirdikten sonra kapatma hello not defteri toorelease hello kaynakları gerekir. toodo çok hello **dosya** hello dizüstü menüsünde **Kapat ve Durdur**. Bu işlem kapatma ve Kapat hello dizüstü.

## <a name="anaconda"></a>Anaconda scikit kullanın-Spark machine learning için kitaplık öğrenin
Hdınsight'ta Apache Spark kümeleri Anaconda kitaplıkları içerir. Bu da hello içerir **scikit-öğrenin** machine learning için kitaplık. Merhaba kitaplığı toobuild örnek uygulamalardan doğrudan Jupyter not defteri kullanabileceğiniz çeşitli veri kümeleri de içerir. Scikit kullanma örnekleri hello için-kitaplık bilgi [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).

## <a name="seealso"></a>Ayrıca bkz.
* [Genel Bakış: Azure HDInsight’ta Apache Spark](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Senaryolar
* [BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme](hdinsight-apache-spark-use-bi-tools.md)
* [Machine Learning ile Spark: Spark Hdınsight toopredict yemek İnceleme sonuçlarını içinde kullanma](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark Akış: Gerçek zamanlı akış uygulamaları oluşturmak için HDInsight’ta Spark kullanma](hdinsight-apache-spark-eventhub-streaming.md)
* [HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Uygulamaları oluşturma ve çalıştırma
* [Scala kullanarak tek başına uygulama oluşturma](hdinsight-apache-spark-create-standalone-application.md)
* [Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Araçlar ve uzantılar
* [Intellij Idea toocreate için Hdınsight araçları eklentisi kullanma ve Spark Scala uygulamaları gönderin](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Uzaktan Intellij Idea toodebug Spark uygulamaları için Hdınsight araçları eklentisi kullanma](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Jupyter not defterleri ile dış paketleri kullanma](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter bilgisayarınıza yüklemek ve tooan Hdınsight Spark kümesi bağlanın](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Kaynakları yönetme
* [Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme](hdinsight-apache-spark-resource-manager.md)
* [HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-weblogs-sample]: hdinsight-hive-analyze-website-log.md
[hdinsight-sensor-data-sample]: hdinsight-hive-analyze-sensor-data.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
