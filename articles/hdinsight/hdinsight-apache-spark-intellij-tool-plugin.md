---
title: "Intellij için Azure Araç Seti: Spark Hdınsight kümesi için uygulama oluşturma | Microsoft Docs"
description: "Intellij toodevelop Spark Scala içinde yazılmış uygulamalar için Hello Azure araç seti kullanın ve bunları tooan Hdınsight Spark kümesi gönderin."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 73304272-6c8b-482e-af7c-cd25d95dab4d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: nitinme
ms.openlocfilehash: 22cce014bb848a54e198e77a50bf13448012310e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toocreate-spark-applications-for-an-hdinsight-cluster"></a>Hdınsight kümesi için Intellij toocreate Spark uygulamaları için Azure araç kullanma

Intellij eklenti toodevelop Spark Scala içinde yazılmış uygulamalar için Hello Azure araç seti kullanın ve bunları tooan Hdınsight Spark kümesi hello Intellij tümleşik geliştirme ortamı (IDE) doğrudan gönderebilirler. Merhaba birkaç yolla eklentisi kullanabilirsiniz:

* Geliştirme ve Hdınsight Spark kümesi üzerinde bir Scala Spark uygulamasının gönderin.
* Azure Hdınsight Spark küme kaynaklarına erişim.
* Geliştirme ve Scala Spark uygulama yerel olarak çalıştırın.

toocreate proje, görünüm hello [hello Intellij için Azure araç seti ile Spark uygulamaları oluşturmak](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) video.

> [!IMPORTANT]
> Bu eklenti toocreate kullanın ve yalnızca Linux'ta Hdınsight Spark kümesinde uygulamalar gönderin.
> 

## <a name="prerequisites"></a>Ön koşullar

- Hdınsight Linux üzerinde Apache Spark kümesi. Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).
- Oracle Java Geliştirme Seti. Merhaba yükleme [Oracle Web sitesi](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
- Intellij Idea. Bu makalede sürümünü 2017.1 kullanır. Merhaba yükleme [JetBrains Web sitesi](https://www.jetbrains.com/idea/download/).

## <a name="install-azure-toolkit-for-intellij"></a>Intellij için Azure Araç Seti yükleyin
Yükleme yönergeleri için bkz: [Intellij için Azure Araç Seti yüklemek](../azure-toolkit-for-intellij-installation.md).

## <a name="sign-in-tooyour-azure-subscription"></a>Azure aboneliği tooyour oturum

1. Merhaba Intellij IDE başlatın ve Azure Gezgini'ni açın. Merhaba üzerinde **Görünüm** menüsünde, select **aracı Windows**ve ardından **Azure Gezgini**.
       
   ![Hello Azure Gezgini bağlantısı](./media/hdinsight-apache-spark-intellij-tool-plugin/show-azure-explorer.png)

2. Sağ hello **Azure** düğümünü ve ardından **oturum**.

3. Merhaba, **Azure oturum açma** iletişim kutusunda **oturum**ve ardından Azure kimlik bilgilerinizi girin.

    ![Hello Azure oturum açma iletişim kutusu](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-2.png)

4. Oturum açtınız sonra hello **seçin abonelikleri** tüm hello ile ilişkili Azure abonelikleri iletişim kutusu listeleri hello kimlik bilgileri. Select hello **seçin** düğmesi.

    ![Merhaba abonelikleri seçin iletişim kutusu](./media/hdinsight-apache-spark-intellij-tool-plugin/Select-Subscriptions.png)

5. Merhaba üzerinde **Azure Gezgini** sekmesinde, genişletin **Hdınsight** aboneliğinizde olan Hdınsight Spark kümeleri tooview hello.
   
    ![Azure Explorer'da Hdınsight Spark kümeleri](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-3.png)

6. hello kümeyle ilişkili tooview hello kaynaklarını (örneğin, depolama hesapları), başka bir küme adı düğümü genişletebilirsiniz.
   
    ![Genişletilmiş bir küme adı düğümü](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-4.png)

## <a name="run-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a>Hdınsight Spark kümesi üzerinde Spark Scala uygulamayı çalıştırın

1. Intellij Idea başlatın ve bir proje oluşturun. Merhaba, **yeni proje** iletişim kutusunda, aşağıdaki hello: 

   a. Seçin **Hdınsight** > **(Scala) hdınsight'ta Spark**.

   b. Merhaba, **oluşturma aracını** listesinde, aşağıdaki, tooyour gerek according hello birini seçin:

      * **Maven**, Scala Proje Oluşturma Sihirbazı'nı desteği
      * **SBT**, başlangıç bağımlılıkları yönetmek ve için hello Scala projesi oluşturma

    ![Merhaba yeni proje iletişim kutusu](./media/hdinsight-apache-spark-intellij-tool-plugin/create-hdi-scala-app.png)

2. Seçin **sonraki**.

3. Merhaba Scala Proje Oluşturma Sihirbazı'nı otomatik olarak hello Scala eklenti yüklediğiniz olup olmadığını algılar. Seçin **yükleme**.

   ![Scala eklentisi onay](./media/hdinsight-apache-spark-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. toodownload hello Scala eklentisi, select **Tamam**. Merhaba yönergeleri toorestart Intellij izleyin. 

   ![Merhaba Scala eklentisi yükleme iletişim kutusu](./media/hdinsight-apache-spark-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. Merhaba, **yeni proje** penceresinde, aşağıdaki hello:  

    ![Merhaba Spark SDK seçme](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-new-project.png)

   a. Bir proje adı ve konum girin.

   b. Merhaba, **proje SDK** aşağı açılan listesinden, **Java 1.8** hello Spark 2.x kümesi ya da seçin **Java 1.7** hello Spark 1.x kümesi için.

   c. Merhaba, **Spark sürüm** aşağı açılan listesinde, Scala Proje Oluşturma Sihirbazı'nı Spark SDK ve Scala SDK hello uygun sürüm tümleştirir. Merhaba Spark küme sürüm 2.0 eskiyse, seçin **1.x Spark**. Aksi takdirde seçin **Spark2.x**. Bu örnekte **Spark 2.0.2 (Scala 2.11.8)**.

6. **Son**’u seçin.

7. Merhaba Spark proje bir yapı sizin için otomatik olarak oluşturur. tooview hello yapı aşağıdaki hello:

   a. Merhaba üzerinde **dosya** menüsünde, select **proje yapısını**.

   b. Merhaba, **proje yapısını** iletişim kutusunda **yapıları** oluşturulan tooview hello varsayılan yapı. Merhaba artı işaretini seçerek kendi yapı de oluşturabilirsiniz (**+**).

      ![Yapı bilgisi hello iletişim kutusunda](./media/hdinsight-apache-spark-intellij-tool-plugin/default-artifact.png)
      
8. Uygulama kaynak koduna hello aşağıdakileri yaparak ekleyin:

   a. Proje Gezgini'nde sağ **src**, çok noktası**yeni**ve ardından **Scala sınıfı**.
      
      ![Proje Gezgini'nde Scala sınıfı oluşturmak için komutları](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code.png)

   b. Merhaba, **yeni Scala Sınıf Oluştur** iletişim kutusunda, bir ad sağlayın, seçin **nesne** hello içinde **türü** kutusuna ve ardından **Tamam**.
      
      ![Yeni Scala sınıf iletişim kutusu oluşturma](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code-object.png)

   c. Merhaba, **MyClusterApp.scala** dosya, hello aşağıdaki kodu yapıştırın. Merhaba kodu HVAC.csv (tüm Hdınsight Spark kümeleri üzerinde kullanılabilir) hello verileri okur, sütununda hello yedinci hello CSV dosyası yalnızca bir rakam olması hello satır alır ve hello çıkış çok yazar**/HVACOut** hello varsayılan altında Merhaba küme depolama kapsayıcısı.

        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
    
        object MyClusterApp{
            def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
    
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
    
            //find hello rows that have only one digit in hello seventh column in hello CSV file
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
    
            rdd1.saveAsTextFile("wasb:///HVACOut")
            }
    
        }

9. Merhaba uygulaması hello aşağıdakileri yaparak bir Hdınsight Spark kümesinde çalıştırın:

   a. Proje Gezgini'nde hello proje adına sağ tıklayın ve ardından **gönderme Spark uygulama tooHDInsight**.
      
      ![Merhaba gönderme Spark uygulama tooHDInsight komutu](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-1.png)

   b. Azure aboneliği kimlik bilgileriniz istendiğinde tooenter şunlardır. Merhaba, **Spark gönderme** iletişim kutusu, değerleri aşağıdaki hello sağlayın ve ardından **gönderme**.
      
      * İçin **Spark kümeleri (yalnızca Linux)**, uygulamanızı seçin hello toorun istediğiniz Hdınsight Spark kümesi.

      * Merhaba Intellij projeden bir yapı seçin veya bir hello sabit sürücü seçin.

      * Merhaba, **ana sınıf adı** kutusunda, select hello üç nokta (**...** ), uygulamanın kaynak kodunda hello ana sınıfı seçin ve ardından **Tamam**.

        ![Merhaba ana sınıf Seç iletişim kutusu](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-3.png)

      * Bu örnekte Hello uygulama kodu komut satırı bağımsız değişkenleri gerektirmediği veya Kavanoz veya dosyaları başvurmak için kutuları boş kalan hello bırakabilirsiniz. Tüm hello bilgileri verdikten sonra hello iletişim kutusu görüntü aşağıdaki hello benzemelidir.
        
        ![Merhaba Spark gönderme iletişim kutusu](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-2.png)

   c. Merhaba **Spark gönderme** sekmesini hello pencerenin hello altındaki hello ilerleme durumunu görüntüleme başlamalıdır. Hello hello kırmızı düğmesini seçerek Merhaba uygulaması durdurabilirsiniz **Spark gönderme** penceresi.
      
      ![Merhaba Spark gönderme penceresi](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-result.png)
      
      toolearn tooaccess iş çıktısı hello nasıl hello bkz "erişim ve Intellij için Azure Araç Seti kullanarak Hdınsight Spark kümeleri yönetmek" bölümünde bu makalenin sonraki bölümlerinde yer.

## <a name="run-or-debug-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a>Çalıştırabilir veya bir Hdınsight Spark kümesi üzerinde Spark Scala uygulamanızın hatalarını ayıklama
Merhaba Spark uygulama toohello küme gönderilmesi bir başka yolu da öneririz. Hello hello parametrelerini ayarlayarak yapabilirsiniz **Çalıştır/hata ayıklama yapılandırmaları** IDE. Daha fazla bilgi için bkz: [SSH aracılığıyla Intellij için Hdınsight kümesinde Azure araç seti ile Spark uygulamalarında uzaktan hata ayıklama](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-azure-toolkit-for-intellij"></a>Erişim ve Hdınsight Spark kümeleri Intellij için Azure Araç Seti kullanarak yönetme
Intellij için Azure Araç Seti kullanarak çeşitli işlemler gerçekleştirebilirsiniz.

### <a name="access-hello-job-view"></a>Erişim hello işi görüntüle
1. Azure Explorer'da genişletin **Hdınsight**hello Spark küme adını genişletin ve ardından **işleri**.  

    ![Proje görünümü düğümü](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. Merhaba sağ bölmede, hello **Spark iş görünümünde** sekmesi hello küme üzerinde çalıştırılan tüm hello uygulamaları görüntüler. Merhaba uygulaması toosee daha fazla ayrıntı istediğiniz Hello adını seçin.

    ![Uygulama Ayrıntıları](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)

3. toodisplay temel çalışan iş bilgileri hello iş grafiğinin üzerine getirin. tooview hello aşamaları grafik ve her iş oluşturur, bilgileri bir düğümde hello iş grafiği seçin.

    ![İş aşama ayrıntıları](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

4. tooview sık kullanılan günlükleri gibi *sürücü Stderr*, *sürücü Stdout*, ve *dizin bilgisi*seçin hello **günlük** sekmesi.

    ![Günlük Ayrıntıları](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)

5. Ayrıca hello Spark geçmişi kullanıcı Arabirimi ve hello YARN kullanıcı Arabiriminde (Merhaba uygulama düzeyinde) hello penceresinde hello üstündeki bağlantısını seçerek görüntüleyebilirsiniz.

### <a name="access-hello-spark-history-server"></a>Erişim hello Spark geçmişi sunucusu
1. Azure Explorer'da genişletin **Hdınsight**Spark küme adına sağ tıklayın ve ardından **açık Spark geçmişi kullanıcı Arabirimi**. 

2. İstendiğinde, hello küme ayarlandığında belirtilen hello kümenin yönetici kimlik girin.

3. Merhaba Spark geçmişi server panosunda hello uygulama adı toolook yalnızca çalışması sona Merhaba uygulaması için kullanabilirsiniz. Kod önceki hello hello uygulama adı kullanarak ayarladığınız `val conf = new SparkConf().setAppName("MyClusterApp")`. Bu nedenle, Spark uygulamanızın adı olan **MyClusterApp**.

### <a name="start-hello-ambari-portal"></a>Merhaba Ambari portal Başlat
1. Azure Explorer'da genişletin **Hdınsight**Spark küme adına sağ tıklayın ve ardından **açık küme yönetim portalı (Ambari)**. 

2. İstendiğinde, hello küme için hello yönetici kimlik bilgilerini girin. Merhaba küme kurulum işlemi sırasında bu kimlik bilgileri belirttiniz.

### <a name="manage-azure-subscriptions"></a>Azure Aboneliklerini yönetmek
Varsayılan olarak, tüm Azure aboneliklerinden hello Spark kümeleri Intellij için Azure Araç Seti listeler. Gerekirse, hello abonelikleri tooaccess istediğinizi belirtebilirsiniz. 

1. Hello Azure Gezgini'nde sağ **Azure** kök düğümünü ve ardından **Aboneliklerini Yönet**. 

2. Merhaba iletişim kutusunda, yoksa tooaccess istediğiniz ve ardından, hello onay kutularını sonraki toohello abonelikleri temizleyin **Kapat**. Öğesini de seçebilirsiniz **oturum kapatma** dışında Azure aboneliğinizin toosign istiyorsanız.

## <a name="run-a-spark-scala-application-locally"></a>Spark Scala uygulama yerel olarak çalıştırma
Azure Araç Seti Intellij toorun Spark Scala uygulamaları için yerel olarak iş istasyonunuza kullanabilirsiniz. Merhaba uygulamalar genellikle depolama kapsayıcıları gibi toocluster kaynakları erişmeyin ve çalıştırma ve bunları yerel olarak test etme.

### <a name="prerequisite"></a>Önkoşul
Bir Windows bilgisayarda hello yerel Spark Scala uygulama çalıştırıyorsanız, ancak açıklandığı gibi bir özel durum alabilirsiniz [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356). WinUtils.exe olmadığından, Windows hello özel durum oluşur. 

tooresolve bu hatayı [hello yürütülebilir karşıdan](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa konum gibi **C:\WinUtils\bin**. Ardından, hello ortam değişkenine ekleyin **HADOOP_HOME**ve çok hello hello değişkenin değerini ayarlamak**C\WinUtils**.

### <a name="run-a-local-spark-scala-application"></a>Yerel bir Spark Scala uygulamayı çalıştırın
1. Intellij Idea başlatın ve bir proje oluşturun. 

2. Merhaba, **yeni proje** iletişim kutusunda, aşağıdaki hello:
   
    a. Seçin **Hdınsight** > **Spark Hdınsight yerel çalışma örneği (Scala)**.

    b. Merhaba, **oluşturma aracını** listesinde, aşağıdaki, tooyour gerek according hello birini seçin:

      * **Maven**, Scala Proje Oluşturma Sihirbazı'nı desteği
      * **SBT**, başlangıç bağımlılıkları yönetmek ve için hello Scala projesi oluşturma

    ![Merhaba yeni proje iletişim kutusu](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run.png)

3. Seçin **sonraki**.
 
4. Merhaba sonraki penceresinde, aşağıdaki hello:
   
    a. Bir proje adı ve konum girin.

    b. Merhaba, **proje SDK** aşağı açılan listesinde, 1.7 sürümünden daha yeni bir Java sürümünü seçin.

    c. Merhaba, **Spark sürüm** açılan listesinden, select hello sürümü toouse istediğiniz Scala: Scala Spark 2.0 veya Scala 2.11.x 2.10.x Spark 1.6 için.

    ![Merhaba yeni proje iletişim kutusu](./media/hdinsight-apache-spark-intellij-tool-plugin/Create-local-project.PNG)

5. **Son**’u seçin.

6. Merhaba şablon ekler örnek kod (**LogQuery**) hello altında **src** bilgisayarınızda yerel olarak çalıştırabilirsiniz klasör.
   
    ![LogQuery konumu](./media/hdinsight-apache-spark-intellij-tool-plugin/local-app.png)

7. Sağ hello **LogQuery** uygulama ve ardından **Çalıştır 'LogQuery'**. Merhaba üzerinde **çalıştırmak** sekmesini hello altındaki hello aşağıdaki gibi bir çıktı görmeniz:
   
   ![Spark uygulama yerel çalıştırma sonucu](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="convert-existing-intellij-idea-applications-toouse-azure-toolkit-for-intellij"></a>Intellij için varolan Intellij Idea uygulamaları toouse Azure Araç Seti Dönüştür
Intellij Idea toobe Intellij için Azure araç seti ile uyumlu oluşturduğunuz hello varolan Spark Scala uygulamaları dönüştürebilirsiniz. Daha sonra hello eklenti toosubmit hello uygulamaları tooan Hdınsight Spark kümesi kullanabilirsiniz.

1. Intellij Idea ile oluşturulmuş bir varolan Spark Scala uygulama için hello ilişkili .iml dosyasını açın.

2. Merhaba kökünde düzeyidir bir **Modülü** öğesi hello aşağıdaki gibi:
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4">

   Merhaba öğesi tooadd Düzenle `UniqueKey="HDInsightTool"` , bu nedenle hello **Modülü** öğesi hello aşağıdaki gibi görünür:
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4" UniqueKey="HDInsightTool">

3. Merhaba değişiklikleri kaydedin. Uygulamanız artık Intellij için Azure araç seti ile uyumlu olması gerekir. Merhaba proje Gezgini'nde proje adına sağ tıklayarak test edebilirsiniz. Hello açılır menüsünden başlangıç seçeneği artık sahiptir **gönderme Spark uygulama tooHDInsight**.

## <a name="troubleshooting"></a>Sorun giderme

### <a name="error-in-local-run-please-use-a-larger-heap-size"></a>Yerel çalıştırma hatası: *Lütfen daha büyük bir öbek boyutu kullanın*
Yerel çalıştırma sırasında bir 32 bit Java SDK'sı kullanıyorsanız, Spark 1.6 içinde aşağıdaki hatalar hello karşılaşabilirsiniz:

    Exception in thread "main" java.lang.IllegalArgumentException: System memory 259522560 must be at least 4.718592E8. Please use a larger heap size.
        at org.apache.spark.memory.UnifiedMemoryManager$.getMaxMemory(UnifiedMemoryManager.scala:193)
        at org.apache.spark.memory.UnifiedMemoryManager$.apply(UnifiedMemoryManager.scala:175)
        at org.apache.spark.SparkEnv$.create(SparkEnv.scala:354)
        at org.apache.spark.SparkEnv$.createDriverEnv(SparkEnv.scala:193)
        at org.apache.spark.SparkContext.createSparkEnv(SparkContext.scala:288)
        at org.apache.spark.SparkContext.<init>(SparkContext.scala:457)
        at LogQuery$.main(LogQuery.scala:53)
        at LogQuery.main(LogQuery.scala)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:606)
        at com.intellij.rt.execution.application.AppMain.main(AppMain.java:144)

Merhaba yığın boyutu Spark toorun için yeterince büyük olduğundan bu hataları gerçekleşir. Spark en az 471 MB gerektirir. (Daha fazla bilgi için bkz: [SPARK 12081](https://issues.apache.org/jira/browse/SPARK-12081).) Bir basit toouse bir 64-bit Java SDK'sı çözümüdür. Seçenekler aşağıdaki hello ekleyerek de Intellij hello JVM ayarları değiştirebilirsiniz:

    -Xms128m -Xmx512m -XX:MaxPermSize=300m -ea

!["VM Seçenekleri" içinde Intellij kutusunda seçenekleri toohello ekleme](./media/hdinsight-apache-spark-intellij-tool-plugin/change-heap-size.png)

## <a name="faq"></a>SSS
bir uygulama tooAzure Data Lake Store toosubmit seçin **etkileşimli** hello Azure oturum açma işlemi sırasında modu. Seçerseniz **otomatik** modu, bir hata alabilirsiniz.

![signın etkileşim](./media/hdinsight-apache-spark-intellij-tool-plugin/interative-signin.png)

Şimdi, biz bunu çözümlendi. Uygulamanız herhangi bir oturum açma yöntemi bir Azure Data Lake küme toosubmit seçebilirsiniz.

## <a name="feedback-and-known-issues"></a>Geri bildirim ve bilinen sorunlar
Şu anda, Spark çıkışları doğrudan görüntüleme desteklenmiyor.

Tüm öneriler veya Geri bildiriminiz varsa veya bu eklenti kullandığınızda herhangi bir sorunla karşılaşırsanız, adresinden bize e-posta hdivstool@microsoft.com.

## <a name="seealso"></a>Sonraki adımlar
* [Genel Bakış: Azure HDInsight’ta Apache Spark](hdinsight-apache-spark-overview.md)

### <a name="demo"></a>Tanıtım
* Scala proje oluştur (video): [Spark Scala uygulamaları oluşturma](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)
* Uzaktan hata ayıklama (video): [Intellij toodebug Spark uygulamalarında uzaktan Hdınsight kümesinde için kullanım Azure Araç Seti](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)

### <a name="scenarios"></a>Senaryolar
* [BI ile Spark: BI araçlarıyla Hdınsight'ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme](hdinsight-apache-spark-use-bi-tools.md)
* [Machine Learning ile Spark: HVAC verilerini kullanarak sıcaklık oluşturma Hdınsight tooanalyze kullanım Spark](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Machine Learning ile Spark: Spark Hdınsight toopredict yemek İnceleme sonuçlarını içinde kullanma](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark akış: Spark Hdınsight toobuild gerçek zamanlı akış uygulamaları kullanma](hdinsight-apache-spark-eventhub-streaming.md)
* [HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a>Oluşturma ve uygulamaları çalıştırma
* [Scala kullanarak tek başına uygulama oluşturma](hdinsight-apache-spark-create-standalone-application.md)
* [Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Araçlar ve uzantılar
* [VPN üzerinden uzaktan Intellij toodebug Spark uygulamaları için Azure araç kullanma](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [SSH üzerinden uzaktan Intellij toodebug Spark uygulamaları için Azure araç kullanma](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [Korumalı alan Hortonworks ile Intellij için Hdınsight araçları kullanma](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Azure araç setini Eclipse toocreate Spark uygulamaları için Hdınsight araçları kullanın](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Jupyter not defterleri ile dış paketleri kullanma](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter bilgisayarınıza yüklemek ve tooan Hdınsight Spark kümesi bağlanın](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a>Kaynakları yönetme
* [Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme](hdinsight-apache-spark-resource-manager.md)
* [HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama](hdinsight-apache-spark-job-debugging.md)

