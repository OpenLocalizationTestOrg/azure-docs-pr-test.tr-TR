---
title: "Intellij için Azure Araç Seti: SSH üzerinden uzaktan hata ayıklama Spark uygulamaları | Microsoft Docs"
description: "Hdınsight üzerinde uzaktan Intellij toodebug uygulamalar için Hdınsight araçları Azure Araç Seti toouse SSH nasıl kümeleri üzerinde adım adım yönergeler"
keywords: "ıntellij, debugging ıntellij, ssh, uzak ıntellij, hdınsight uzaktan hata ayıklama, ıntellij, hata ayıklama hata ayıklama"
services: hdinsight
documentationcenter: 
author: jejiang
manager: DJ
editor: Jenny Jiang
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 08/24/2017
ms.author: Jenny Jiang
ms.openlocfilehash: bf3ab9d04c2ff9fcb6bbbdeefb11f55a12fbd845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-spark-applications-on-an-hdinsight-cluster-with-azure-toolkit-for-intellij-through-ssh"></a>SSH aracılığıyla Intellij için Hdınsight kümesinde Azure araç seti ile Spark uygulamalarında hata ayıklama

Bu makalede hakkında adım adım yönergeler sağlar toouse Hdınsight araçları Azure araç seti, Hdınsight kümesi üzerinde uzaktan Intellij toodebug uygulamalar için. toodebug, projenizin hello de görüntüleyebilirsiniz [Intellij için Hdınsight Spark hata ayıklama uygulamaları Azure araç seti ile](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) video.

**Önkoşullar**

* **Azure Araç Seti Intellij için Hdınsight Araçları**. Bu araç Intellij için Azure araç seti bir parçasıdır. Daha fazla bilgi için bkz: [Intellij için Azure Araç Seti yüklemek](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).
* **Intellij için Azure Araç Seti**. Bu araç seti toocreate Spark uygulamaları bir Hdınsight kümesi için kullanın. Daha fazla bilgi için hello yönergeleri izleyin [Hdınsight kümesi için Intellij toocreate Spark uygulamaları için kullanım Azure Araç Seti](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).
* **Hdınsight SSH hizmeti kullanıcı adı ve parola yönetimi ile**. Daha fazla bilgi için bkz: [tooHDInsight (Hadoop) SSH kullanarak bağlanmak](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) ve [kullanım SSH tünel tooaccess Ambari web kullanıcı Arabirimi, kaynak, iş, Oozie ve diğer web Uı'lar](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel). 
 

## <a name="create-a-spark-scala-application-and-configure-it-for-remote-debugging"></a>Spark Scala uygulama oluşturma ve uzaktan hata ayıklama için yapılandırma

1. Intellij Idea başlatın ve bir proje oluşturun. Merhaba, **yeni proje** iletişim kutusunda, aşağıdaki hello:

   a. Seçin **Hdınsight**. 

   b. Tercihinize bağlı bir Java veya Scala şablonu seçin. Seçenekler aşağıdaki hello arasında seçin:

      - **(Scala) hdınsight'ta Spark**

      - **(Java) hdınsight'ta Spark**

      - **Spark Hdınsight kümesi çalışma örneği (Scala)**

      Bu örnekte bir **Spark Hdınsight küme çalıştırmak örneği (Scala)** şablonu.

   c. Merhaba, **oluşturma aracını** listesinde, aşağıdaki, tooyour gerek according hello birini seçin:

      - **Maven**, Scala Proje Oluşturma Sihirbazı'nı desteği

      -  **SBT**, başlangıç bağımlılıkları yönetmek ve için hello Scala projesi oluşturma 

      ![Hata ayıklama projesi oluşturma](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-create-projectfor-debug-remotely.png)

   d. Seçin **sonraki**.     
 
3. Merhaba, sonraki **yeni proje** penceresinde, aşağıdaki hello:

   ![Merhaba Spark SDK'yı seçin](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-new-project.png)

   a. Bir proje adı ve proje konumu girin.

   b. Merhaba, **proje SDK** aşağı açılan listesinden, **Java 1.8** için **2.x Spark** seçin ya da küme **Java 1.7** için **Spark 1. x** küme.

   c. Merhaba, **Spark sürüm** aşağı açılan listesinde, hello Scala Proje Oluşturma Sihirbazı'nı Spark SDK ve Scala SDK hello doğru sürümü tümleştirir. Merhaba spark küme sürüm 2.0 eskiyse, seçin **1.x Spark**. Aksi takdirde seçin **2.x Spark.** Bu örnekte **Spark 2.0.2 (Scala 2.11.8)**.

   d. **Son**’u seçin.

4. Seçin **src** > **ana** > **scala** tooopen hello proje kodunuzda. Bu örnek hello kullanır **SparkCore_wasbloTest** komut dosyası.

5. tooaccess hello **yapılandırmalarını Düzenle** menüsü, hello sağ üst köşesinde select hello simgesi. Bu menüden oluşturabilir veya uzaktan hata ayıklama için hello yapılandırmaları düzenleyebilirsiniz.

   ![Yapılandırmaları Düzenle](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-edit-configurations.png) 

6. Merhaba, **Çalıştır/hata ayıklama yapılandırmaları** iletişim kutusu, select hello artı işareti (**+**). Merhaba seçip **Spark işi Gönder** seçeneği.

   ![Yeni yapılandırma ekleyin](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-add-new-Configuration.png)
7. İçin bilgileri girin **adı**, **Spark kümesi**, ve **ana sınıf adı**. Ardından **Gelişmiş Yapılandırma**. 

   ![Hata ayıklama yapılandırmaları çalıştırma](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-run-debug-configurations.png)

8. Merhaba, **Spark gönderimi Gelişmiş Yapılandırma** iletişim kutusunda **etkinleştirmek Spark uzaktan hata ayıklama**. Merhaba SSH kullanıcı adı girin ve ardından bir parola girin veya özel bir anahtar dosyası kullanın. toosave hello yapılandırma, select **Tamam**.

   ![Spark uzaktan hata ayıklama etkinleştirme](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-enable-spark-remote-debug.png)

9. Merhaba yapılandırma şimdi sağladığınız hello adıyla kaydedilir. tooview hello yapılandırma ayrıntılarını, select hello yapılandırma adı. toomake değişiklikleri seçin **yapılandırmalarını Düzenle**. 

10. Merhaba yapılandırma ayarlarını tamamladığınızda hello uzaktan küme karşı Merhaba projeyi çalıştırın veya uzaktan hata ayıklama gerçekleştirin.

## <a name="learn-how-tooperform-remote-debugging"></a>Bilgi nasıl tooperform uzaktan hata ayıklama
### <a name="scenario-1-perform-remote-run"></a>Senaryo 1: Uzak çalışma gerçekleştirme

Bu bölümde, nasıl gösteriyoruz toodebug sürücüleri ve yürütücüler.

    import org.apache.spark.{SparkConf, SparkContext}

    object LogQuery {
      val exampleApacheLogs = List(
        """10.10.10.10 - "FRED" [18/Jan/2013:17:56:07 +1100] "GET http://images.com/2013/Generic.jpg
          | HTTP/1.1" 304 315 "http://referall.com/" "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1;
          | GTB7.4; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; .NET CLR 3.0.04506.648; .NET CLR
          | 3.5.21022; .NET CLR 3.0.4506.2152; .NET CLR 1.0.3705; .NET CLR 1.1.4322; .NET CLR
          | 3.5.30729; Release=ARP)" "UD-1" - "image/jpeg" "whatever" 0.350 "-" - "" 265 923 934 ""
          | 62.24.11.25 images.com 1358492167 - Whatup""".stripMargin.lines.mkString,
        """10.10.10.10 - "FRED" [18/Jan/2013:18:02:37 +1100] "GET http://images.com/2013/Generic.jpg
          | HTTP/1.1" 304 306 "http:/referall.com" "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1;
          | GTB7.4; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; .NET CLR 3.0.04506.648; .NET CLR
          | 3.5.21022; .NET CLR 3.0.4506.2152; .NET CLR 1.0.3705; .NET CLR 1.1.4322; .NET CLR
          | 3.5.30729; Release=ARP)" "UD-1" - "image/jpeg" "whatever" 0.352 "-" - "" 256 977 988 ""
          | 0 73.23.2.15 images.com 1358492557 - Whatup""".stripMargin.lines.mkString
      )
      def main(args: Array[String]) {
        val sparkconf = new SparkConf().setAppName("Log Query")
        val sc = new SparkContext(sparkconf)
        val dataSet = sc.parallelize(exampleApacheLogs)
        // scalastyle:off
        val apacheLogRegex =
          """^([\d.]+) (\S+) (\S+) \[([\w\d:/]+\s[+\-]\d{4})\] "(.+?)" (\d{3}) ([\d\-]+) "([^"]+)" "([^"]+)".*""".r
        // scalastyle:on
        /** Tracks hello total query count and number of aggregate bytes for a particular group. */
        class Stats(val count: Int, val numBytes: Int) extends Serializable {
          def merge(other: Stats): Stats = new Stats(count + other.count, numBytes + other.numBytes)
          override def toString: String = "bytes=%s\tn=%s".format(numBytes, count)
        }
        def extractKey(line: String): (String, String, String) = {
          apacheLogRegex.findFirstIn(line) match {
            case Some(apacheLogRegex(ip, _, user, dateTime, query, status, bytes, referer, ua)) =>
              if (user != "\"-\"") (ip, user, query)
              else (null, null, null)
            case _ => (null, null, null)
          }
        }
        def extractStats(line: String): Stats = {
          apacheLogRegex.findFirstIn(line) match {
            case Some(apacheLogRegex(ip, _, user, dateTime, query, status, bytes, referer, ua)) =>
              new Stats(1, bytes.toInt)
            case _ => new Stats(1, 0)
          }
        }
        
        dataSet.map(line => (extractKey(line), extractStats(line)))
          .reduceByKey((a, b) => a.merge(b))
          .collect().foreach{
          case (user, query) => println("%s\t%s".format(user, query))}

        sc.stop()
      }
    }


1. Kesme noktaları kurulumu ve hello ardından **hata ayıklama** simgesi.

   ![Merhaba hata ayıklama simgesini seçin](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-icon.png)

2. Merhaba program yürütme hello kesme noktası ulaştığında, gördüğünüz bir **sürücü** sekmesi ve iki **Yürütücü** hello sekmeleri **hata ayıklayıcı** bölmesi. Select hello **Sürdür Program** sonra hello sonraki kesme ulaştığında ve hello karşılık gelen üzerinde odaklanır hello kod çalıştırmasını simgesi toocontinue **Yürütücü** sekmesi. Merhaba karşılık gelen üzerinde hello yürütme günlüklerini gözden geçirebilirsiniz **konsol** sekmesi.

   ![Hata ayıklama sekmesi](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debugger-tab.png)

### <a name="scenario-2-perform-remote-debugging-and-bug-fixing"></a>Senaryo 2: uzaktan hata ayıklama ve hata düzeltme gerçekleştirme
Bu bölümde, nasıl kullanarak toodynamically güncelleştirme hello değişken değeri hello yetenek basit bir düzeltme için hata ayıklama Intellij gösteriyoruz. Aşağıdaki kod örneğine hello Hello hedef dosyası zaten mevcut olduğundan özel durum oluşur.
  
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext

        object SparkCore_WasbIOTest {
          def main(arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkCore_WasbIOTest")
            val sc = new SparkContext(conf)
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            // Find hello rows that have only one digit in hello sixth column.
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)

            try {
              var target = "wasb:///HVACout2_testdebug1";
              rdd1.saveAsTextFile(target);
            } catch {
              case ex: Exception => {
                throw ex;
              }
            }
          }
        }


#### <a name="tooperform-remote-debugging-and-bug-fixing"></a>tooperform uzaktan hata ayıklama ve hata düzeltme
1. İki kesme noktaları kurulumu ve hello ardından **hata ayıklama** simgesi toostart hello uzaktan hata ayıklama işlemi.

2. Merhaba kod hello ilk kesme noktası durdurur ve hello parametre ve değişken bilgileri hello gösterilen **değişkenleri** bölmesi. 

3. Select hello **Sürdür Program** simgesi toocontinue. Merhaba kod hello ikinci noktada durdurur. beklendiği gibi Hello özel durum yakalandı.

  ![Hata durum](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-throw-error.png) 

4. Select hello **Sürdür Program** yeniden simgesi. Merhaba **Hdınsight Spark gönderme** penceresi bir "işi çalıştırma başarısız oldu" hatasını görüntüler.

  ![Hata gönderme](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-error-submission.png) 

5. Merhaba Intellij hata ayıklama özelliğini kullanarak toodynamically güncelleştirme hello değişken değerini seçin **hata ayıklama** yeniden. Merhaba **değişkenleri** yeniden bölmesinde görünür. 

6. Sağ hello hello hedefte **hata ayıklama** sekmesini tıklatın ve ardından **değeri ayarlanmış**. Ardından, hello değişken için yeni bir değer girin. Ardından **Enter** toosave hello değeri. 

  ![Değerini ayarla](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-set-value.png) 

7. Select hello **Sürdür Program** simgesi toocontinue toorun hello program. Bu süre, hiçbir özel durum yakalandı. Merhaba Proje başarıyla tüm özel durumlar çalışır görebilirsiniz.

  ![Özel durum olmadan hata ayıklama](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-without-exception.png)

## <a name="seealso"></a>Sonraki adımlar
* [Genel Bakış: Azure HDInsight’ta Apache Spark](hdinsight-apache-spark-overview.md)

### <a name="demo"></a>Tanıtım
* Scala proje oluştur (video): [Spark Scala uygulamaları oluşturma](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)
* Uzaktan hata ayıklama (video): [Hdınsight kümesi üzerinde uzaktan Intellij toodebug Spark uygulamalar için kullanım Azure Araç Seti](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)

### <a name="scenarios"></a>Senaryolar
* [BI ile Spark: BI araçlarıyla Hdınsight'ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme](hdinsight-apache-spark-use-bi-tools.md)
* [Machine Learning ile Spark: HVAC verilerini kullanarak sıcaklık oluşturma Hdınsight tooanalyze kullanım Spark](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Machine Learning ile Spark: Spark Hdınsight toopredict yemek İnceleme sonuçlarını içinde kullanma](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark akış: Spark Hdınsight toobuild gerçek zamanlı akış uygulamaları kullanma](hdinsight-apache-spark-eventhub-streaming.md)
* [HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Uygulamaları oluşturma ve çalıştırma
* [Scala kullanarak tek başına uygulama oluşturma](hdinsight-apache-spark-create-standalone-application.md)
* [Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Araçlar ve uzantılar
* [Hdınsight kümesi için Intellij toocreate Spark uygulamaları için Azure araç kullanma](hdinsight-apache-spark-intellij-tool-plugin.md)
* [VPN üzerinden uzaktan Intellij toodebug Spark uygulamaları için Azure araç kullanma](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Korumalı alan Hortonworks ile Intellij için Hdınsight araçları kullanma](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Azure araç setini Eclipse toocreate Spark uygulamaları için Hdınsight araçları kullanın](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma](hdinsight-apache-spark-zeppelin-notebook.md)
* [Merhaba Hdınsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Jupyter not defterleri ile dış paketleri kullanma](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter bilgisayarınıza yüklemek ve tooan Hdınsight Spark kümesi bağlanın](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Kaynakları yönetme
* [Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme](hdinsight-apache-spark-resource-manager.md)
* [HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama](hdinsight-apache-spark-job-debugging.md)
