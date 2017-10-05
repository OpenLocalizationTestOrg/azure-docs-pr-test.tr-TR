---
title: "Eclipse - Hdınsight Spark oluşturmak Scala uygulamaları için Azure Araç Seti | Microsoft Docs"
description: "Hdınsight araçları Eclipse için Azure Araç Seti Spark Scala içinde yazılmış uygulamalar geliştirmek için kullanabilir ve bunları bir Hdınsight Spark kümesi için doğrudan kendilerinden Eclipse IDE gönderebilirler."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f6c79550-5803-4e13-b541-e86c4abb420b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: nitinme
ms.openlocfilehash: 4bcb1987a62c0b7f4965e6fd257315e820004238
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-toolkit-for-eclipse-to-create-spark-applications-for-an-hdinsight-cluster"></a>Eclipse için Azure Araç Seti Spark Hdınsight kümesi için uygulamalar oluşturmak için kullanın

Spark Scala içinde yazılmış uygulamalar geliştirmek ve bunları bir Azure Hdınsight Spark kümesi için Eclipse IDE içinden doğrudan göndermek için Azure araç setini Eclipse için Hdınsight araçlarını kullanın. Hdınsight araçları eklentisi birkaç farklı şekillerde kullanabilirsiniz:

* Geliştirmek ve Hdınsight Spark kümesi üzerinde bir Scala Spark uygulamasının göndermek için
* Azure Hdınsight Spark küme kaynaklarınıza erişmek için
* Geliştirmek ve Scala Spark uygulamayı yerel olarak çalıştırmak için

> [!IMPORTANT]
> Bu araç, oluşturma ve gönderme yalnızca Linux'ta Hdınsight Spark kümesinde uygulamalar için kullanılabilir.
> 
> 

## <a name="prerequisites"></a>Ön koşullar

* Hdınsight'ta bir Apache Spark kümesi. Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).
* Eclipse IDE çalışma zamanı için kullanılan oracle Java Geliştirme Seti 8 sürümü. Buradan indirebilirsiniz [Oracle Web sitesi](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* Eclipse IDE. Bu makalede Eclipse Neon kullanır. Şuradan yükleyebilirsiniz [Eclipse Web sitesi](https://www.eclipse.org/downloads/).   
* Spark SDK. Buradan indirebilirsiniz [GitHub](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409).


## <a name="install-hdinsight-tools-in-azure-toolkit-for-eclipse-and-scala-plugin"></a>Eclipse ve Scala eklentisi için Azure araç setindeki Hdınsight araçlarını yükleme
### <a name="install-hdinsight-tools"></a>Hdınsight araçlarını yükleme
Eclipse için Hdınsight araçları kullanılabilir Eclipse için Azure araç seti bir parçası olarak. Yükleme yönergeleri için bkz: [Eclipse için Azure Araç Seti yükleme](../azure-toolkit-for-eclipse-installation.md).
### <a name="install-scala-plugin"></a>Scala eklentisini yükleme
Intellij açtığınızda, Hdınsight araçları otomatik veya Scala eklentisi yüklü olup olmadığını algılar. Tıklatın **Tamam** devam ve Eclipse Marketi tarafından yüklemek için yönergeleri izleyin.

 ![Otomatik Yükleme Scala eklentisi](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala.png)

## <a name="sign-in-to-your-azure-subscription"></a>Azure aboneliğinizde oturum açın
1. Eclipse IDE başlatın ve Azure Gezgini'ni açın. Üzerinde **penceresi** menüsünde tıklatın **görünümü göster**ve ardından **diğer**. Açılan iletişim kutusunda genişletin **Azure**, tıklatın **Azure Gezgini**ve ardından **Tamam**.

    ![Görünüm iletişim kutusunu göster](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-1.png)
2. Sağ **Azure** düğümünü ve ardından **oturum**.
3. İçinde **Azure oturum açma** iletişim kutusunda, kimlik doğrulama yöntemi seçin, **oturum**ve Azure kimlik bilgilerinizi girin.
   
    ![Azure oturum açma iletişim kutusu](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-2.png)
4. ' De, oturum açtığınız sonra **seçin abonelikleri** iletişim kutusu kimlik bilgileriyle ilişkili tüm Azure abonelikleri listeler. Tıklatın **seçin** iletişim kutusunu kapatın.

    ![Abonelikleri iletişim kutusu seç](./media/hdinsight-apache-spark-eclipse-tool-plugin/Select-Subscriptions.png)
5. Üzerinde **Azure Gezgini** sekmesinde, genişletin **Hdınsight** Hdınsight Spark kümeleri aboneliğinizde görmek için.
   
    ![Azure Explorer'da Hdınsight Spark kümeleri](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-3.png)
6. Daha fazla kümesi ile ilişkili kaynakları (örneğin, depolama hesapları) görmek için bir küme adı düğümü genişletebilirsiniz.
   
    ![Bir küme adı kaynakları görmek için genişletme](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-4.png)



## <a name="set-up-a-spark-scala-project-for-an-hdinsight-spark-cluster"></a>Spark Scala proje Hdınsight Spark kümesinde için ayarlama

1. Eclipse IDE çalışma alanında tıklatın **dosya**, tıklatın **yeni**ve ardından **proje**. 
2. Yeni Proje Sihirbazı'nda genişletin **Hdınsight**seçin **(Scala) hdınsight'ta Spark**ve ardından **sonraki**.

    ![Spark Hdınsight (Scala) projede seçme](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-2.png)
3. Scala Proje Oluşturma Sihirbazı'nı otomatik veya Scala eklentisi yüklü olup olmadığını algılar. Tıklatın **Tamam** Scala eklentisi indirme devam etmek için Eclipse yeniden başlatmak için yönergeleri izleyin.

    ![scala denetimi](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala-2.png)
4. İçinde **yeni Hdınsight Scala proje** iletişim kutusunda, aşağıdaki değerleri girin ve ardından **sonraki**:
   * Proje için bir ad girin.
   * İçinde **JRE** alanı olduğundan emin olun **yürütme ortamı JRE kullanın** ayarlanır **JavaSE 1.7** veya sonraki bir sürümü.
   * Spark SDK SDK indirdiğiniz konuma ayarlandığından emin olun. Yükleme konumu bağlantısını dahil [Önkoşullar](#prerequisites) bu makalenin önceki. İletişim kutusunda içerdiği bağlantısından SDK de yükleyebilirsiniz.

    ![Yeni Hdınsight Scala proje iletişim kutusu](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-3.png)
5.  Sonraki iletişim kutusunda tıklatın **kitaplıkları** sekmesinde ve Varsayılanları tutun ve ardından **son**. 
   
    ![Kitaplıklar sekmesi](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-4.png)
  
## <a name="create-a-scala-application-for-an-hdinsight-spark-cluster"></a>Hdınsight Spark kümesinde için Scala uygulama oluşturma

1. Eclipse IDE'de paketi Gezgini'nden daha önce oluşturduğunuz projenizi genişletin, sağ **src**, işaret **yeni**ve ardından **diğer**.
2. İçinde **bir sihirbaz seçin** iletişim kutusunda, genişletin **Scala sihirbazları**, tıklatın **Scala nesne**ve ardından **sonraki**.
   
    ![Bir sihirbaz iletişim kutusu seç](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-1.png)
3. İçinde **yeni dosyası oluştur** iletişim kutusu, nesne için bir ad girin ve ardından **son**.
   
    ![Yeni dosya iletişim kutusu oluşturma](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-2.png)
4. Metin Düzenleyicisi'nde aşağıdaki kodu yapıştırın:
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        object MyClusterApp{
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find the rows that have only one digit in the seventh column in the CSV
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACOut")
          }        
        }
5. Uygulamayı bir Hdınsight Spark kümesinde çalıştırın:
   
   1. Paket Gezgini'nde proje adına sağ tıklayın ve ardından **Hdınsight için Spark uygulama gönderme**.        
   2. İçinde **Spark gönderme** iletişim kutusunda, aşağıdaki değerleri girin ve ardından **gönderme**:
      
      * İçin **küme adı**, istediğiniz uygulamanızı çalıştırmak Hdınsight Spark kümesi seçin.
      * Eclipse projeden bir yapı seçin veya bir sabit sürücüden seçin. Varsayılan değer paketi Gezgini'nden sağ öğesi bağlıdır.
      * İçinde **ana sınıf adı** dropdownlist, Gönderme Sihirbazı seçili projenizden tüm nesne adlarını görüntüler. Çalıştırmak istediğiniz bir giriş veya seçin. Yapı sabit diskten seçerseniz, kendi kendinize ana sınıf adı giriş. 
      * Bu örnek uygulama kodunda herhangi bir komut satırı bağımsız değişkeni gerektirmediği veya Kavanoz veya dosyaları başvurmak için kalan metin kutularını boş bırakabilirsiniz.
        
       ![Spark gönderme iletişim kutusu](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-3.png)
   3. **Spark gönderme** sekmesi, ilerleme durumunu görüntüleme başlamalıdır. Kırmızı düğmesini tıklatarak uygulama durdurabilirsiniz **Spark gönderme** penceresi. Ayrıca bu belirli uygulama (mavi kutu resim olarak gösterilir) dünya simgesini tıklatarak çalıştırmak için günlükleri görüntüleyebilirsiniz.
      
       ![Spark gönderme penceresi](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-4.png)

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-hdinsight-tools-in-azure-toolkit-for-eclipse"></a>Erişim ve Hdınsight Spark kümeleri Eclipse için Azure araç setindeki Hdınsight araçları kullanarak yönetme
İş çıktısı erişim dahil olmak üzere, Hdınsight araçları kullanarak çeşitli işlemler gerçekleştirebilirsiniz.

### <a name="access-the-job-view"></a>İş görünüme erişme
1. Azure Explorer'da genişletin **Hdınsight**, Spark küme adını genişletin ve ardından **işleri**. 

    ![Proje görünümü düğümü](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. Tıklayın **işleri** düğümü. Hdınsight araçları otomatik-E (fx) clipse eklentisi veya yüklü olup olmadığını algılar. Tıklatın **Tamam** devam ve Eclipse Market yükleme ve Eclipse yeniden başlatmak için yönergeleri izleyin.

    ![E (fx) clipse yükleyin](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-efxclipse.png)

3. İş görünümünden **işleri** düğümü. Sağ bölmede **Spark iş görünümünde** sekmesi, küme üzerinde çalıştırılan tüm uygulamaları görüntüler. Daha fazla ayrıntı görmek istediğiniz uygulamanın adını tıklatın.

    ![Uygulama Ayrıntıları](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)
4. İş grafiğinin getirirseniz, temel çalışan iş bilgileri görüntüler. İş grafiği tıklatarak aşamaları grafik ve her iş oluşturur bilgilerini gösterir.

    ![İş aşama ayrıntıları](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

5. Sürücü Stderr, sürücü Stdout ve dizin bilgisi gibi sık kullanılan günlükleri içinde listelenen **günlük** sekmesi.

    ![Günlük Ayrıntıları](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)
6. Spark geçmişi kullanıcı Arabirimi ve YARN kullanıcı Arabiriminde (uygulama düzeyinde) pencerenin üstündeki ilgili köprüyü tıklatarak da açabilirsiniz.

### <a name="access-the-storage-container-for-the-cluster"></a>Küme depolama kapsayıcısını erişim
1. Azure Explorer'da genişletin **Hdınsight** kullanılabilir Hdınsight Spark kümeleri listesini görmek için kök düğümü.
2. Depolama hesabı ve kümenin varsayılan depolama kapsayıcısını görmek için küme adını genişletin.
   
    ![Depolama hesabı ve varsayılan depolama kapsayıcısı](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-5.png)
3. Kümeyle ilişkili depolama kapsayıcı adına tıklayın. Sağ bölmede, çift **HVACOut** klasör. Birini açın **bölümü -** uygulamanın çıkışı görmek için dosyaları.

### <a name="access-the-spark-history-server"></a>Spark geçmişi sunucusuna erişim
1. Azure Gezgini'nde, Spark küme adına sağ tıklayın ve ardından **açık Spark geçmişi kullanıcı Arabirimi**. İstendiğinde, küme için yönetici kimlik bilgilerini girin. Bu küme hazırlama sırasında belirttiğiniz gerekir.
2. Spark geçmişi server panosunda, uygulama için yalnızca çalışması sona aramak için uygulama adı kullanın. Önceki kod, uygulamanın adını kullanarak ayarladığınız `val conf = new SparkConf().setAppName("MyClusterApp")`. Bu nedenle, Spark uygulamanızın adı olan **MyClusterApp**.

### <a name="start-the-ambari-portal"></a>Ambari Portalı'nı Başlat
1. Azure Gezgini'nde, Spark küme adına sağ tıklayın ve ardından **açık küme yönetim portalı (Ambari)**. 
2. İstendiğinde, küme için yönetici kimlik bilgilerini girin. Bu küme hazırlama sırasında belirttiğiniz gerekir.

### <a name="manage-azure-subscriptions"></a>Azure Aboneliklerini yönetmek
Varsayılan olarak, tüm Azure aboneliklerinden Spark kümeleri Azure araç setini Eclipse için Hdınsight araçları listeler. Gerekirse, kümeye erişmek istediğiniz abonelikleri belirtebilirsiniz. 

1. Azure Gezgini'nde sağ **Azure** kök düğümünü ve ardından **Aboneliklerini Yönet**. 
2. İletişim kutusunda, erişim ve ardından istemediğiniz abonelik için onay kutularını temizleyin **Kapat**. Tıklatarak **oturum kapatma** dışında Azure aboneliğinizin imzalanacak istiyorsanız.

## <a name="run-a-spark-scala-application-locally"></a>Spark Scala uygulama yerel olarak çalıştırma
Spark Scala uygulamaları iş istasyonunuza yerel olarak çalıştırmak için Hdınsight araçları Azure araç setini Eclipse için kullanabilirsiniz. Genellikle, bu uygulamaları bir depolama kapsayıcısı gibi küme kaynaklarına erişimi gerekmez ve çalıştırma ve bunları yerel olarak test etme.

### <a name="prerequisite"></a>Önkoşul
Bir Windows bilgisayarda yerel Spark Scala uygulama çalıştırıyorsanız, ancak açıklandığı gibi bir özel durum alabilirsiniz [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356). Bu özel durum oluşur **WinUtils.exe** Windows eksik. 

Bu hatayı gidermek için şunları yapmanız gerekir [yürütülebilir dosya indirme](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) gibi bir konuma **C:\WinUtils\bin**. Ortam değişkeni sonra eklemelisiniz **HADOOP_HOME** ve değişkenin değerini ayarlamak **C\WinUtils**.

### <a name="run-a-local-spark-scala-application"></a>Yerel bir Spark Scala uygulamayı çalıştırın
1. Eclipse'i başlatın ve bir proje oluşturun. İçinde **yeni proje** iletişim kutusunda, aşağıdaki seçimleri yapın ve ardından **sonraki**.
   
   * Sol bölmede seçin **Hdınsight**.
   * Sağ bölmede seçin **Spark Hdınsight yerel çalıştırma örneği (Scala)**.

    ![Yeni Proje iletişim kutusu](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run.png)
2. Proje ayrıntılarını sağlamak için önceki bölümdeki 3 ile 6 arasındaki adımları izleyin [Hdınsight Spark kümesi için Spark Scala proje ayarlama](#set-up-a-spark-scala-project-for-an-hdinsight-spark cluster).
3. Örnek kod şablonunu ekler (**LogQuery**) altında **src** bilgisayarınızda yerel olarak çalıştırabilirsiniz klasör.
   
    ![LogQuery konumu](./media/hdinsight-apache-spark-eclipse-tool-plugin/local-app.png)
4. Sağ **LogQuery** uygulama, noktasına **Çalıştır**ve ardından **1 Scala uygulama**. Bu gibi bir çıktı göreceksiniz **konsol** sekmesi altındaki:
   
   ![Spark çalıştırma sonucu uygulama yerel](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="faq"></a>SSS
Azure Data Lake Store uygulamaya göndermek için tercih **etkileşimli** Azure oturum açma işlemi sırasında modu. Seçerseniz **otomatik** modu, bir hata alabilirsiniz.

![signın etkileşim](./media/hdinsight-apache-spark-eclipse-tool-plugin/interactive-authentication.png)

Şimdi, biz bunu çözümlendi. Uygulamanız herhangi bir oturum açma yöntemi göndermek için bir Azure Data Lake küme seçebilirsiniz.

## <a name="feedback-and-known-issues"></a>Geri bildirim ve bilinen sorunlar
Şu anda, Spark çıkışları doğrudan görüntüleme desteklenmiyor.

Tüm öneriler veya Geri bildiriminiz varsa veya bu aracı kullanırken herhangi bir sorunla karşılaşırsanız, bize bir e-postası göndermek çekinmeyin hdivstool@microsoft.com.

## <a name="seealso"></a>Ayrıca bkz.
* [Genel Bakış: Azure HDInsight’ta Apache Spark](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Senaryolar
* [BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme](hdinsight-apache-spark-use-bi-tools.md)
* [Machine Learning ile Spark: HVAC verilerini kullanarak bina sıcaklığını çözümlemek için HDInsight’ta Spark kullanma](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Machine Learning ile Spark: Yemek inceleme sonuçlarını tahmin etmek için HDInsight’ta Spark kullanma](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark Akış: Gerçek zamanlı akış uygulamaları oluşturmak için HDInsight’ta Spark kullanma](hdinsight-apache-spark-eventhub-streaming.md)
* [HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a>Oluşturma ve uygulamaları çalıştırma
* [Scala kullanarak tek başına uygulama oluşturma](hdinsight-apache-spark-create-standalone-application.md)
* [Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Araçlar ve uzantılar
* [Oluşturma ve Spark Scala uygulamaları göndermek amacıyla Intellij için Azure araç seti kullanın](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Spark uygulamalarında VPN üzerinden uzaktan hata ayıklamak için Azure araç Intellij için kullanma](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Spark uygulamalarında SSH üzerinden uzaktan hata ayıklamak için Azure araç Intellij için kullanma](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [Korumalı alan Hortonworks ile Intellij için Hdınsight araçları kullanma](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Jupyter not defterleri ile dış paketleri kullanma](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter’i bilgisayarınıza yükleme ve bir HDInsight Spark kümesine bağlanma](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a>Kaynakları yönetme
* [Azure HDInsight’ta Apache Spark kümesi kaynaklarını yönetme](hdinsight-apache-spark-resource-manager.md)
* [HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama](hdinsight-apache-spark-job-debugging.md)

