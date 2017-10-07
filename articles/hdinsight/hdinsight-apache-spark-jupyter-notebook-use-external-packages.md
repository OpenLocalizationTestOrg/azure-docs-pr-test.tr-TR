---
title: "Azure hdınsight'ta Spark Jupyter'de aaaUse özel Maven paketleri | Microsoft Docs"
description: "Nasıl tooconfigure Jupyter not defterleri ile Hdınsight Spark kullanılabilir kümeleri toouse özel Maven paketleri ilişkin adım adım yönergeler için."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2a8bc545-064e-436f-8b5f-e67c26cfbf98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ba8ac13716bc94ab082a18fe02d4a40b2f1e09e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-external-packages-with-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a>Hdınsight'ta Apache Spark kümeleri Jupyter not defterlerinde ile dış paketleri kullanma
> [!div class="op_single_selector"]
> * [Hücre Sihirli kullanma](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [Betik eylemi kullanarak](hdinsight-apache-spark-python-package-installation.md)
>
>

Nasıl tooconfigure Hdınsight toouse dış, Apache Spark kümesinde Jupyter not defteri topluluk-katkıda öğrenin **maven** hello kümede olmayan paketler dahil Giden kutusu. 

Merhaba arayabilirsiniz [Maven depo](http://search.maven.org/) hello tam kullanılabilir paketler listesi. Ayrıca, diğer kaynaklardan kullanılabilir paketlerin listesini alabilirsiniz. Örneğin, tamamını topluluk katkıda bulunan paketlerin listesini adresten edinilebilir [Spark paketleri](http://spark-packages.org/).

Bu makalede, öğreneceksiniz nasıl toouse hello [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) hello Jupyter not defteri paketiyle.



## <a name="prerequisites"></a>Ön koşullar
Merhaba şunlara sahip olmanız gerekir:

* Hdınsight'ta bir Apache Spark kümesi. Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="use-external-packages-with-jupyter-notebooks"></a>Jupyter not defterleri ile dış paketleri kullanma
1. Merhaba gelen [Azure Portal](https://portal.azure.com/), (, onu toohello Sabitle) hello Panosu'ndan hello kutucuğuna Spark kümenizin tıklayın. Tooyour küme altında da gidebilirsiniz **tümüne Gözat** > **Hdınsight kümeleri**.   
2. Merhaba Spark kümesi dikey penceresinden tıklatın **hızlı bağlantılar**ve sonra hello **küme Panosu** dikey penceresinde tıklatın **Jupyter not defteri**. İstenirse, hello küme için hello yönetici kimlik bilgilerini girin.

    > [!NOTE]
    > Kümenizin açma hello tarayıcınızda URL aşağıdaki tarafından hello Jupyter Not Defteri de ulaşabilir. Değiştir **CLUSTERNAME** kümenizi hello adı:
    > 
    > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
    > 

   

3. Yeni bir not defteri oluşturun. Tıklatın **yeni**ve ardından **Spark**.
   
    ![Yeni bir Jupyter not defteri oluşturma](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-create-notebook.png "Yeni bir Jupyter not defteri oluşturma")

4. Yeni bir not defteri oluşturulur ve Untitled.pynb hello adı ile. Merhaba üstünde Hello dizüstü bilgisayar adına tıklayın ve kolay bir ad girin.
   
    ![Merhaba dizüstü bilgisayar için bir ad](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/hdinsight-spark-name-notebook.png "hello dizüstü bilgisayar için bir ad sağlayın")

5. Merhaba kullanacağınız `%%configure` Sihirli tooconfigure hello not defteri toouse bir dış paketi. Dış paketleri kullanma defterlerinde hello çağrı emin olun `%%configure` hello birinci kod hücresini Sihirli. Bu hello oturum başlamadan önce bu hello çekirdek yapılandırılmış toouse hello paketi sağlar.

    >[!IMPORTANT] 
    >Merhaba ilk hücresinde tooconfigure hello çekirdek unutursanız, hello kullanabilirsiniz `%%configure` hello ile `-f` parametre ancak hello oturumu başlatacak ve tüm ilerleme kaybolacak.

    | Hdınsight sürümü | Komut |
    |-------------------|---------|
    |Hdınsight 3.3 ve Hdınsight 3.4 | `%%configure` <br>`{ "packages":["com.databricks:spark-csv_2.10:1.4.0"] }`|
    | Hdınsight 3.5 | `%%configure`<br>`{ "conf": {"spark.jars.packages": "com.databricks:spark-csv_2.10:1.4.0" }}`|

6. Yukarıdaki Hello parçacığında hello maven koordinatları hello dış Maven merkezi bir depoya paketinde için bekliyor. Bu parçacığında bulunan `com.databricks:spark-csv_2.10:1.4.0` hello maven koordinatı olan **spark csv** paket. İşte nasıl hello koordinatları bir paket için oluşturun.
   
    a. Merhaba paketi hello Maven depo bulun. Bu öğretici için kullandığımız [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).
   
    b. Merhaba depodan hello değerlerini toplamak **GroupID**, **Artifactıd**, ve **sürüm**. Merhaba değerleri toplamanız kümenizi eşleştiğinden emin olun. Bu durumda, Scala 2.10 ve Spark 1.4.0 paket kullanıyoruz, ancak kümenizdeki hello için uygun Scala veya Spark sürüm tooselect farklı sürümlerini gerekebilir. Merhaba Scala sürümü kümenizde çalıştırarak bulabileceğiniz `scala.util.Properties.versionString` hello Spark Jupyter çekirdek veya Spark Gönder. Hello Spark sürüm kümenizde çalıştırarak bulabileceğiniz `sc.version` Jupyter Not.
   
    ![Jupyter not defteri ile dış paketleri kullanma](./media/hdinsight-apache-spark-jupyter-notebook-use-external-packages/use-external-packages-with-jupyter.png "Jupyter not defteri ile dış paketleri kullanma")
   
    c. Merhaba üç değerleri, virgülle ayrılmış birleştirme (**:**).
   
        com.databricks:spark-csv_2.10:1.4.0

7. Merhaba kod hücre ile Merhaba çalıştırmak `%%configure` Sihirli. Bu, sağladığınız hello temel Livy oturum toouse hello paket yapılandıracak. Merhaba sonraki hücrelerde hello not defterinde, aşağıda gösterildiği gibi hello paket artık kullanabilirsiniz.
   
        val df = sqlContext.read.format("com.databricks.spark.csv").
        option("header", "true").
        option("inferSchema", "true").
        load("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

8. Merhaba parçacıkları sonra çalıştırabilir, aşağıda gösterilen tooview gibi hello hello dataframe verilerden hello önceki adımda oluşturduğunuz.
   
        df.show()
   
        df.select("Time").count()

## <a name="seealso"></a>Ayrıca bkz.
* [Genel Bakış: Azure HDInsight’ta Apache Spark](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Senaryolar
* [BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme](hdinsight-apache-spark-use-bi-tools.md)
* [Machine Learning ile Spark: HVAC verilerini kullanarak bina sıcaklığını çözümlemek için HDInsight’ta Spark kullanma](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Machine Learning ile Spark: Spark Hdınsight toopredict yemek İnceleme sonuçlarını içinde kullanma](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark Akış: Gerçek zamanlı akış uygulamaları oluşturmak için HDInsight’ta Spark kullanma](hdinsight-apache-spark-eventhub-streaming.md)
* [HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Uygulamaları oluşturma ve çalıştırma
* [Scala kullanarak tek başına uygulama oluşturma](hdinsight-apache-spark-create-standalone-application.md)
* [Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Araçlar ve uzantılar

* [Hdınsight Linux üzerinde Apache Spark kümeleri Jupyter not defterlerinde ile dış python paketlerini kullanma](hdinsight-apache-spark-python-package-installation.md)
* [Intellij Idea toocreate için Hdınsight araçları eklentisi kullanma ve Spark Scala uygulamaları gönderin](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Uzaktan Intellij Idea toodebug Spark uygulamaları için Hdınsight araçları eklentisi kullanma](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Jupyter bilgisayarınıza yüklemek ve tooan Hdınsight Spark kümesi bağlanın](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Kaynakları yönetme
* [Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme](hdinsight-apache-spark-resource-manager.md)
* [HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama](hdinsight-apache-spark-job-debugging.md)

