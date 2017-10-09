---
title: "aaaAzure Eclipse - Hdınsight Spark oluşturmak Scala uygulamaları için araç seti | Microsoft Docs"
description: "Eclipse toodevelop Spark Scala içinde yazılmış uygulamalar için Hdınsight araçları Azure araç setindeki kullanın ve tooan Hdınsight Spark kümesi göndermek, doğrudan kendilerinden Eclipse IDE hello."
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
ms.openlocfilehash: 3ab70857c1e81f591a1c7e29bc1706ec4899ff58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-eclipse-toocreate-spark-applications-for-an-hdinsight-cluster"></a>Hdınsight kümesi için Eclipse toocreate Spark uygulamaları için Azure araç kullanma

Eclipse toodevelop Spark Scala içinde yazılmış uygulamalar için Azure araç setindeki Hdınsight araçlarını kullanın ve bunları hello Eclipse IDE doğrudan tooan Azure Hdınsight Spark küme gönderin. Merhaba Hdınsight araçları eklentisi birkaç farklı şekillerde kullanabilirsiniz:

* toodevelop ve Hdınsight Spark kümesi üzerinde bir Scala Spark uygulamasının gönderin
* tooaccess Azure Hdınsight Spark küme kaynakları
* toodevelop ve Scala Spark uygulama yerel olarak çalıştırma

> [!IMPORTANT]
> Bu araç, kullanılan toocreate olması ve yalnızca Linux'ta Hdınsight Spark kümesinde uygulamalar gönderin.
> 
> 

## <a name="prerequisites"></a>Ön koşullar

* Hdınsight'ta bir Apache Spark kümesi. Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).
* Merhaba Eclipse IDE çalışma zamanı için kullanılan oracle Java Geliştirme Seti 8 sürümü. Hello karşıdan [Oracle Web sitesi](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* Eclipse IDE. Bu makalede Eclipse Neon kullanır. Merhaba yükleme [Eclipse Web sitesi](https://www.eclipse.org/downloads/).   
* Spark SDK. Buradan indirebilirsiniz [GitHub](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409).


## <a name="install-hdinsight-tools-in-azure-toolkit-for-eclipse-and-scala-plugin"></a>Eclipse ve Scala eklentisi için Azure araç setindeki Hdınsight araçlarını yükleme
### <a name="install-hdinsight-tools"></a>Hdınsight araçlarını yükleme
Eclipse için Hdınsight araçları kullanılabilir Eclipse için Azure araç seti bir parçası olarak. Yükleme yönergeleri için bkz: [Eclipse için Azure Araç Seti yükleme](../azure-toolkit-for-eclipse-installation.md).
### <a name="install-scala-plugin"></a>Scala eklentisini yükleme
Merhaba Intellij açtığınızda hello Hdınsight araçları otomatik veya Scala eklentisi yüklü olup olmadığını algılar. Tıklatın **Tamam** hello Eclipse Market tarafından hello yönergeleri tooinstall toocontinue ve izleyin.

 ![Otomatik Yükleme Scala eklentisi](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala.png)

## <a name="sign-in-tooyour-azure-subscription"></a>Azure aboneliği tooyour oturum
1. Merhaba Eclipse IDE başlatın ve Azure Gezgini'ni açın. Merhaba üzerinde **penceresi** menüsünde tıklatın **görünümü göster**ve ardından **diğer**. Açılan hello iletişim kutusunda, genişletin **Azure**, tıklatın **Azure Gezgini**ve ardından **Tamam**.

    ![Görünüm iletişim kutusunu göster](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-1.png)
2. Sağ hello **Azure** düğümünü ve ardından **oturum**.
3. Merhaba, **Azure oturum açma** iletişim kutusunda, hello kimlik doğrulaması yöntemi seçin, **oturum**ve Azure kimlik bilgilerinizi girin.
   
    ![Azure oturum açma iletişim kutusu](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-2.png)
4. Oturum açtınız sonra hello **seçin abonelikleri** tüm hello hello kimlik bilgileriyle ilişkili Azure abonelik iletişim kutusu listeler. Tıklatın **seçin** tooclose hello iletişim kutusu.

    ![Abonelikleri iletişim kutusu seç](./media/hdinsight-apache-spark-eclipse-tool-plugin/Select-Subscriptions.png)
5. Merhaba üzerinde **Azure Gezgini** sekmesinde, genişletin **Hdınsight** toosee hello Hdınsight Spark kümeleri, abonelik altında.
   
    ![Azure Explorer'da Hdınsight Spark kümeleri](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-3.png)
6. Daha fazla hello kümesi ile ilişkili bir küme adı düğümü toosee hello kaynakları (örneğin, depolama hesapları) genişletebilirsiniz.
   
    ![Bir küme adı toosee kaynakları genişletme](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-4.png)



## <a name="set-up-a-spark-scala-project-for-an-hdinsight-spark-cluster"></a>Spark Scala proje Hdınsight Spark kümesinde için ayarlama

1. Merhaba Eclipse IDE çalışma alanında tıklatın **dosya**, tıklatın **yeni**ve ardından **proje**. 
2. Merhaba Yeni Proje Sihirbazı'nda genişletin **Hdınsight**seçin **(Scala) hdınsight'ta Spark**ve ardından **sonraki**.

    ![Merhaba Spark Hdınsight (Scala) projede seçme](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-2.png)
3. Merhaba Scala Proje Oluşturma Sihirbazı'nı otomatik veya Scala eklentisi yüklü olup olmadığını algılar. Tıklatın **Tamam** toocontinue hello Scala eklentisi sonra izleme hello yönergeleri toorestart Eclipse yükleniyor.

    ![scala denetimi](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala-2.png)
4. Merhaba, **yeni Hdınsight Scala proje** iletişim kutusu, değerleri aşağıdaki hello sağlayın ve ardından **sonraki**:
   * Başlangıç projesi için bir ad girin.
   * Merhaba, **JRE** alanı olduğundan emin olun **yürütme ortamı JRE kullanın** çok ayarlanır**JavaSE 1.7** ya da daha sonra.
   * Spark SDK hello SDK indirdiğiniz kümesi toohello konumunun olduğundan emin olun. Merhaba bağlantı toohello indirme konumu hello dahil [Önkoşullar](#prerequisites) bu makalenin önceki. Merhaba SDK hello indirebilirsiniz hello iletişim kutusunda içerdiği bağlantı.

    ![Yeni Hdınsight Scala proje iletişim kutusu](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-3.png)
5.  Merhaba Hello sonraki iletişim kutusunda tıklatın **kitaplıkları** sekmesinde ve hello Varsayılanları tutun ve ardından **son**. 
   
    ![Kitaplıklar sekmesi](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-4.png)
  
## <a name="create-a-scala-application-for-an-hdinsight-spark-cluster"></a>Hdınsight Spark kümesinde için Scala uygulama oluşturma

1. Merhaba paketi Gezgini'nden Eclipse IDE içinde daha önce oluşturduğunuz hello proje genişletin, sağ tıklatın **src**, çok noktası**yeni**ve ardından **diğer**.
2. Merhaba, **bir sihirbaz seçin** iletişim kutusunda, genişletin **Scala sihirbazları**, tıklatın **Scala nesne**ve ardından **sonraki**.
   
    ![Bir sihirbaz iletişim kutusu seç](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-1.png)
3. Merhaba, **yeni dosyası oluştur** iletişim kutusu, hello nesnesi için bir ad girin ve ardından **son**.
   
    ![Yeni dosya iletişim kutusu oluşturma](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-2.png)
4. Merhaba metin düzenleyicisinde koddan hello yapıştırın:
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        object MyClusterApp{
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find hello rows that have only one digit in hello seventh column in hello CSV
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACOut")
          }        
        }
5. Bir Hdınsight Spark kümesinde Hello uygulamayı çalıştırın:
   
   1. Paketi Gezgini'nden hello proje adına sağ tıklayın ve ardından **gönderme Spark uygulama tooHDInsight**.        
   2. Merhaba, **Spark gönderme** iletişim kutusu, değerleri aşağıdaki hello sağlayın ve ardından **gönderme**:
      
      * İçin **küme adı**, uygulamanızı seçin hello toorun istediğiniz Hdınsight Spark kümesi.
      * Bir yapı hello Eclipse projeden seçin veya bir sabit sürücüden seçin. Hello varsayılan değer paketi Gezgini'nden sağ hello öğesi bağlıdır.
      * Merhaba, **ana sınıf adı** dropdownlist, Gönderme Sihirbazı seçili projenizden tüm nesne adlarını görüntüler. Seçin veya bir giriş toorun istiyor. Yapı sabit diskten seçerseniz, kendi kendinize ana sınıf adı giriş. 
      * Bu örnekte Hello uygulama kodu herhangi bir komut satırı bağımsız değişkeni gerektirmediği veya Kavanoz veya dosyaları başvurmak için metin kutusu boş kalan hello bırakabilirsiniz.
        
       ![Spark gönderme iletişim kutusu](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-3.png)
   3. Merhaba **Spark gönderme** sekmesini hello ilerleme durumunu görüntüleme başlamalıdır. Merhaba hello kırmızı düğmesini tıklatarak Merhaba uygulaması durdurabilirsiniz **Spark gönderme** penceresi. Merhaba Dünya simgesi (Merhaba mavi kutu hello resim olarak gösterilir) tıklayarak çalıştırın özel bu uygulama için hello günlüklerini de görüntüleyebilirsiniz.
      
       ![Spark gönderme penceresi](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-4.png)

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-hdinsight-tools-in-azure-toolkit-for-eclipse"></a>Erişim ve Hdınsight Spark kümeleri Eclipse için Azure araç setindeki Hdınsight araçları kullanarak yönetme
Merhaba iş çıktısı erişim dahil olmak üzere, Hdınsight araçları kullanarak çeşitli işlemler gerçekleştirebilirsiniz.

### <a name="access-hello-job-view"></a>Erişim hello işi görüntüle
1. Azure Explorer'da genişletin **Hdınsight**hello Spark küme adını genişletin ve ardından **işleri**. 

    ![Proje görünümü düğümü](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. Tıklatın hello üzerinde **işleri** düğümü. Merhaba Hdınsight araçları otomatik-hello E (fx) clipse eklentisi veya yüklü olup olmadığını algılar. Tıklatın **Tamam** tooinstall Eclipse Market hello ve Eclipse'i yeniden toocontinue ve izleme hello yönergeleri.

    ![E (fx) clipse yükleyin](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-efxclipse.png)

3. Açık hello iş görünümünde hello gelen **işleri** düğümü. Merhaba sağ bölmede, hello **Spark iş görünümünde** sekmesi hello küme üzerinde çalıştırılan tüm hello uygulamaları görüntüler. Merhaba uygulaması toosee daha fazla ayrıntı istediğiniz Hello adına tıklayın.

    ![Uygulama Ayrıntıları](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)
4. Hello iş grafiğinin getirirseniz, temel çalışan iş bilgileri görüntüler. Merhaba iş grafikte tıklatarak hello aşamaları grafik ve her iş oluşturur bilgilerini gösterir.

    ![İş aşama ayrıntıları](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

5. Sık kullanılan günlükleri, sürücü Stderr, sürücü Stdout ve dizin bilgisi gibi hello listelenen **günlük** sekmesi.

    ![Günlük Ayrıntıları](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)
6. Merhaba Spark geçmişi kullanıcı Arabirimi ve hello YARN kullanıcı Arabiriminde (Merhaba uygulama düzeyinde) hello penceresinde hello üstündeki hello ilgili köprüyü tıklatarak da açabilirsiniz.

### <a name="access-hello-storage-container-for-hello-cluster"></a>Erişim hello depolama kapsayıcısını hello küme
1. Hello Azure Explorer'da genişletin **Hdınsight** kök düğümü toosee kullanılabilir Hdınsight Spark kümeleri listesi.
2. Merhaba küme adı toosee hello depolama hesabı ve hello küme hello varsayılan depolama kapsayıcısını genişletin.
   
    ![Depolama hesabı ve varsayılan depolama kapsayıcısı](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-5.png)
3. Merhaba kümesi ile ilişkili hello depolama kapsayıcı adına tıklayın. Merhaba Hello sağ bölmede, çift **HVACOut** klasör. Merhaba birini açın **bölümü -** toosee hello çıktı hello uygulamasının dosyaları.

### <a name="access-hello-spark-history-server"></a>Erişim hello Spark geçmişi sunucusu
1. Azure Gezgini'nde, Spark küme adına sağ tıklayın ve ardından **açık Spark geçmişi kullanıcı Arabirimi**. İstendiğinde, hello küme için hello yönetici kimlik bilgilerini girin. Bunlar hello küme hazırlama sırasında belirttiğiniz gerekir.
2. Merhaba Spark geçmişi server panosunda hello uygulama adı toolook yalnızca çalışması sona Merhaba uygulaması için kullanın. Kod önceki hello hello uygulama adı kullanarak ayarladığınız `val conf = new SparkConf().setAppName("MyClusterApp")`. Bu nedenle, Spark uygulamanızın adı olan **MyClusterApp**.

### <a name="start-hello-ambari-portal"></a>Merhaba Ambari portal Başlat
1. Azure Gezgini'nde, Spark küme adına sağ tıklayın ve ardından **açık küme yönetim portalı (Ambari)**. 
2. İstendiğinde, hello küme için hello yönetici kimlik bilgilerini girin. Bunlar hello küme hazırlama sırasında belirttiğiniz gerekir.

### <a name="manage-azure-subscriptions"></a>Azure Aboneliklerini yönetmek
Varsayılan olarak, tüm Azure aboneliklerinden hello Spark kümeleri Azure araç setini Eclipse için Hdınsight araçları listeler. Gerekirse, hello abonelikleri tooaccess hello kümenin istediğinizi belirtebilirsiniz. 

1. Hello Azure Gezgini'nde sağ **Azure** kök düğümünü ve ardından **Aboneliklerini Yönet**. 
2. Merhaba iletişim kutusunda, yoksa tooaccess istediğiniz ve ardından, hello abonelik hello onay kutularını temizleyin **Kapat**. Tıklatarak **oturum kapatma** dışında Azure aboneliğinizin toosign istiyorsanız.

## <a name="run-a-spark-scala-application-locally"></a>Spark Scala uygulama yerel olarak çalıştırma
Hdınsight araçları Azure araç setindeki Eclipse toorun Spark Scala uygulamaları için yerel olarak iş istasyonunuza kullanabilirsiniz. Genellikle, bu uygulamalar gibi bir depolama kapsayıcısı toocluster erişimine gerek yoktur ve çalıştırın ve yerel olarak test.

### <a name="prerequisite"></a>Önkoşul
Bir Windows bilgisayarda hello yerel Spark Scala uygulama çalıştırıyorsanız, ancak açıklandığı gibi bir özel durum alabilirsiniz [SPARK 2356](https://issues.apache.org/jira/browse/SPARK-2356). Bu özel durum oluşur **WinUtils.exe** Windows eksik. 

tooresolve bu hata, gereken [hello yürütülebilir karşıdan](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa konumu ister **C:\WinUtils\bin**. Merhaba ortam değişkeni sonra eklemelisiniz **HADOOP_HOME** ve çok hello hello değişkenin değerini ayarlamak**C\WinUtils**.

### <a name="run-a-local-spark-scala-application"></a>Yerel bir Spark Scala uygulamayı çalıştırın
1. Eclipse'i başlatın ve bir proje oluşturun. Merhaba, **yeni proje** iletişim kutusunda, aşağıdaki seçimleri hello olun ve ardından **sonraki**.
   
   * Merhaba sol bölmesinde seçin **Hdınsight**.
   * Merhaba sağ bölmede seçin **Spark Hdınsight yerel çalıştırma örneği (Scala)**.

    ![Yeni Proje iletişim kutusu](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run.png)
2. tooprovide hello proje ayrıntılarını, 6'dan aracılığıyla 3 adımları hello önceki bölümde [Hdınsight Spark kümesi için Spark Scala proje ayarlama](#set-up-a-spark-scala-project-for-an-hdinsight-spark cluster).
3. Merhaba şablon ekler örnek kod (**LogQuery**) hello altında **src** bilgisayarınızda yerel olarak çalıştırabilirsiniz klasör.
   
    ![LogQuery konumu](./media/hdinsight-apache-spark-eclipse-tool-plugin/local-app.png)
4. Sağ hello **LogQuery** uygulama, çok noktası**Çalıştır**ve ardından **1 Scala uygulama**. Aşağıdaki hello şuna benzer bir çıktı göreceksiniz **konsol** hello altındaki sekmesi:
   
   ![Spark çalıştırma sonucu uygulama yerel](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="faq"></a>SSS
bir uygulama tooAzure Data Lake Store toosubmit seçin **etkileşimli** hello Azure oturum açma işlemi sırasında modu. Seçerseniz **otomatik** modu, bir hata alabilirsiniz.

![signın etkileşim](./media/hdinsight-apache-spark-eclipse-tool-plugin/interactive-authentication.png)

Şimdi, biz bunu çözümlendi. Uygulamanız herhangi bir oturum açma yöntemi bir Azure Data Lake küme toosubmit seçebilirsiniz.

## <a name="feedback-and-known-issues"></a>Geri bildirim ve bilinen sorunlar
Şu anda, Spark çıkışları doğrudan görüntüleme desteklenmiyor.

Tüm öneriler veya Geri bildiriminiz varsa veya bu aracı kullanırken herhangi bir sorunla karşılaşırsanız, bize ücretsiz toosend düşündüğünüz bir e-postası hdivstool@microsoft.com.

## <a name="seealso"></a>Ayrıca bkz.
* [Genel Bakış: Azure HDInsight’ta Apache Spark](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Senaryolar
* [BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme](hdinsight-apache-spark-use-bi-tools.md)
* [Machine Learning ile Spark: HVAC verilerini kullanarak bina sıcaklığını çözümlemek için HDInsight’ta Spark kullanma](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Machine Learning ile Spark: Spark Hdınsight toopredict yemek İnceleme sonuçlarını içinde kullanma](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark Akış: Gerçek zamanlı akış uygulamaları oluşturmak için HDInsight’ta Spark kullanma](hdinsight-apache-spark-eventhub-streaming.md)
* [HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a>Oluşturma ve uygulamaları çalıştırma
* [Scala kullanarak tek başına uygulama oluşturma](hdinsight-apache-spark-create-standalone-application.md)
* [Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Araçlar ve uzantılar
* [Intellij toocreate için Azure araç kullanma ve Spark Scala uygulamaları gönderin](hdinsight-apache-spark-intellij-tool-plugin.md)
* [VPN üzerinden uzaktan Intellij toodebug Spark uygulamaları için Azure araç kullanma](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [SSH üzerinden uzaktan Intellij toodebug Spark uygulamaları için Azure araç kullanma](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [Korumalı alan Hortonworks ile Intellij için Hdınsight araçları kullanma](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Jupyter not defterleri ile dış paketleri kullanma](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter bilgisayarınıza yüklemek ve tooan Hdınsight Spark kümesi bağlanın](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a>Kaynakları yönetme
* [Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme](hdinsight-apache-spark-resource-manager.md)
* [HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama](hdinsight-apache-spark-job-debugging.md)

