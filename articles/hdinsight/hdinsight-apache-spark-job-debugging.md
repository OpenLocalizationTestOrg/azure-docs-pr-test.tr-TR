---
title: "aaaDebug Apache Spark Azure Hdınsight üzerinde çalışan işleri | Microsoft Docs"
description: "Azure Hdınsight Spark kümesinde çalışan YARN kullanıcı Arabiriminde, Spark UI ve Spark geçmişi sunucu tootrack ve hata ayıklama işleri"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 59af05a7-2bd9-44b0-b55f-2438d294198b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 33d352a5773920735aa4e5e8532b78122f381377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-apache-spark-jobs-running-on-azure-hdinsight"></a>Çalışan Azure Hdınsight'ta Apache Spark işleri hata ayıklama

Bu makalede nasıl tootrack ve hata ayıklama hello YARN kullanıcı Arabiriminde, Spark UI kullanarak Hdınsight kümelerinde çalışan işleri Spark ve Spark geçmişi sunucu hello öğreneceksiniz. Bu makalede, biz hello Spark kümesi ile kullanılabilir bir Not Defteri kullanarak Spark işi başlatacak **Machine learning: Yemek İnceleme verileri Mllib'i kullanarak Tahmine dayalı analiz**. Örneğin, gönderilen tüm diğer yaklaşımı de kullanarak bir uygulama tootrack hello adımları kullanabilirsiniz **spark gönderme**.

## <a name="prerequisites"></a>Ön koşullar
Merhaba şunlara sahip olmanız gerekir:

* Azure aboneliği. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Hdınsight'ta bir Apache Spark kümesi. Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).
* Merhaba dizüstü çalıştıran başlamış olması gereken  **[Machine learning: Yemek İnceleme verileri Mllib'i kullanarak Tahmine dayalı analiz](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**. Yönergeler için toorun bu not hello bağlantıyı izleyin.  

## <a name="track-an-application-in-hello-yarn-ui"></a>Merhaba YARN kullanıcı Arabiriminde bir uygulamada izleme
1. Merhaba YARN kullanıcı Arabiriminde başlatın. Merhaba küme dikey penceresinden tıklayın **küme Panosu**ve ardından **YARN**.
   
    ![YARN kullanıcı arabirimini Başlat](./media/hdinsight-apache-spark-job-debugging/launch-yarn-ui.png)
   
   > [!TIP]
   > Alternatif olarak, hello YARN kullanıcı Arabiriminde hello Ambari UI alanından başlatabilirsiniz. Merhaba küme dikey penceresinden toolaunch hello Ambari UI'ı tıklatın **küme Panosu**ve ardından **Hdınsight küme Panosu**. Hello ifadesini Ambari UI'ı tıklatın **YARN**, tıklatın **hızlı bağlantılar**hello etkin Kaynak Yöneticisi'ni tıklatın ve ardından **ResourceManager UI**.    
   > 
   > 
2. Merhaba uygulaması hello ada sahip Jupyter not defterlerini kullanarak hello Spark iş başlatıldı olduğundan **remotesparkmagics** (Bu hello hello defterlerinden başlatılan tüm uygulamalar için addır). Hello uygulama kimliği hello uygulama adı tooget karşı hello işi hakkında daha fazla bilgi'ye tıklayın. Merhaba uygulama görünümünü başlatır.
   
    ![Spark uygulama kimliği bulunamıyor](./media/hdinsight-apache-spark-job-debugging/find-application-id.png)
   
    Merhaba Jupyter defterlerinden başlatılan bu tür uygulamalar için hello durumu her zaman olan **çalıştıran** hello dizüstü çıkana kadar.
3. Merhaba uygulama görünümünden toofind hello uygulama ve hello günlükleri (stdout/stderr) ile ilişkili Merhaba kapsayıcılara çıkışı daha fazla ayrıntıya girebilirsiniz. Karşılık gelen toohello bağlama hello tıklayarak hello Spark UI başlatabilirsiniz **izleme URL'si**, aşağıda gösterildiği gibi. 
   
    ![Kapsayıcı günlüklerini indirin](./media/hdinsight-apache-spark-job-debugging/download-container-logs.png)

## <a name="track-an-application-in-hello-spark-ui"></a>Merhaba Spark UI uygulamada izleme
Hello Spark UI'da, daha önce başlatılmış hello uygulama tarafından kökenli hello Spark işlere ayrıntıya girebilirsiniz.

1. Merhaba uygulama görünümünden toolaunch hello Spark UI hello karşı hello bağlantısını tıklatın **izleme URL'si**yukarıdaki hello ekran görüntüsünde gösterildiği gibi. Merhaba Jupyter not defteri çalışan hello uygulama tarafından başlatılan tüm hello Spark işleri görebilirsiniz.
   
    ![Spark işleri görüntüle](./media/hdinsight-apache-spark-job-debugging/view-spark-jobs.png)
2. Merhaba tıklatın **yürütücüler** sekmesinde toosee işleme ve depolama bilgi her Yürütücü için. Merhaba üzerinde tıklayarak hello çağrı yığını alabilirsiniz **iş parçacığı dökümü** bağlantı.
   
    ![Spark yürütücüler görüntüleyin](./media/hdinsight-apache-spark-job-debugging/view-spark-executors.png)
3. Merhaba tıklatın **aşamaları** sekmesinde toosee hello aşamaları hello uygulaması ile ilişkilendirilmiş.
   
    ![Görünüm Spark aşamaları](./media/hdinsight-apache-spark-job-debugging/view-spark-stages.png)
   
    Her aşama için görüntüleyebilirsiniz yürütme istatistikleri, gibi birden çok görev sağlayabilirsiniz aşağıda gösterilen.
   
    ![Görünüm Spark aşamaları](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-details.png) 
4. Merhaba aşama Ayrıntılar sayfası, DAG görselleştirme başlatabilirsiniz. Merhaba genişletin **DAG görselleştirme** aşağıda gösterildiği gibi hello hello sayfanın başında bağlantı.
   
    ![Görünüm Spark DAG görselleştirme aşamaları](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-dag-visualization.png)
   
    DAG veya doğrudan Aclyic grafik Merhaba uygulaması farklı aşamalarda hello temsil eder. Her hello grafik mavi kutuda hello uygulamadan çağrılan bir Spark işlemini temsil eder.
5. Merhaba aşama Ayrıntılar sayfası, hello uygulama Zaman Çizelgesi görünümüne de başlatabilirsiniz. Merhaba genişletin **olay zaman çizelgesi** aşağıda gösterildiği gibi hello hello sayfanın başında bağlantı.
   
    ![Olay Zaman Çizelgesi görünümüne Spark aşamaları](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-event-timeline.png)
   
    Bu, bir zaman çizelgesi hello biçiminde hello Spark olayları görüntüler. Merhaba Zaman Çizelgesi görünümüne üç düzeyde işleri, işindeki ve aşama içinde üzerinden kullanılabilir. Yukarıdaki resimde Hello hello Zaman Çizelgesi görünümüne belirli bir aşama yakalar.
   
   > [!TIP]
   > Merhaba seçerseniz **yakınlaştırma etkinleştirmek** onay kutusu kaydırma sol ve sağ hello zaman çizelgesi görünümü arasında.
   > 
   > 
6. Merhaba Spark UI diğer sekmeleri de hello Spark örneğinde hakkında yararlı bilgiler sağlar.
   
   * Uygulamanızı bir RDDs oluşturursa, depolama sekmesi - hello depolama sekmesi de hakkında bilgi bulabilirsiniz.
   * Ortam sekmesi - Bu sekme çok sayıda Spark örneğinizi hello gibi hakkında yararlı bilgiler sağlar. 
     * Scala sürüm
     * Olay günlüğüne directory Hello kümesi ile ilişkili
     * Merhaba uygulaması için Yürütücü çekirdek sayısı
     * Etc.

## <a name="find-information-about-completed-jobs-using-hello-spark-history-server"></a>Tamamlanan İşler hello Spark geçmişi sunucu kullanma hakkında bilgi
Bir iş tamamlandığında, hello işle ilgili hello bilgileri hello Spark geçmişi sunucu kalıcıdır.

1. Merhaba küme dikey penceresinden toolaunch hello Spark geçmişi sunucu tıklatın **küme Panosu**ve ardından **Spark geçmişi sunucu**.
   
    ![Spark geçmişi sunucu başlatma](./media/hdinsight-apache-spark-job-debugging/launch-spark-history-server.png)
   
   > [!TIP]
   > Alternatif olarak, hello Spark geçmişi sunucu UI hello Ambari UI alanından başlatabilirsiniz. Merhaba küme dikey penceresinden toolaunch hello Ambari UI'ı tıklatın **küme Panosu**ve ardından **Hdınsight küme Panosu**. Hello ifadesini Ambari UI'ı tıklatın **Spark**, tıklatın **hızlı bağlantılar**ve ardından **Spark geçmişi sunucu UI**.
   > 
   > 
2. Listelenen tüm tamamlanan hello uygulamaları görürsünüz. Bir uygulama kimliği toodrill bir uygulamaya daha fazla bilgi için aşağıya tıklayın.
   
    ![Spark geçmişi sunucu başlatma](./media/hdinsight-apache-spark-job-debugging/view-completed-applications.png)

## <a name="see-also"></a>Ayrıca bkz.
*  [Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme](hdinsight-apache-spark-resource-manager.md)

### <a name="for-data-analysts"></a>Veri çözümleyiciler

* [Machine Learning ile Spark: HVAC verilerini kullanarak bina sıcaklığını çözümlemek için HDInsight’ta Spark kullanma](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Machine Learning ile Spark: Spark Hdınsight toopredict yemek İnceleme sonuçlarını içinde kullanma](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [HDInsight’ta Spark kullanarak Application Insight telemetri verilerinin analizi](hdinsight-spark-analyze-application-insight-logs.md)
* [Caffe Azure Hdınsight Spark üzerinde dağıtılmış derin learning için kullanın.](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a>Spark geliştiricileri için

* [Scala kullanarak tek başına uygulama oluşturma](hdinsight-apache-spark-create-standalone-application.md)
* [Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma](hdinsight-apache-spark-livy-rest-interface.md)
* [Intellij Idea toocreate için Hdınsight araçları eklentisi kullanma ve Spark Scala uygulamaları gönderin](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Spark Akış: Gerçek zamanlı akış uygulamaları oluşturmak için HDInsight’ta Spark kullanma](hdinsight-apache-spark-eventhub-streaming.md)
* [Uzaktan Intellij Idea toodebug Spark uygulamaları için Hdınsight araçları eklentisi kullanma](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Jupyter not defterleri ile dış paketleri kullanma](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter bilgisayarınıza yüklemek ve tooan Hdınsight Spark kümesi bağlanın](hdinsight-apache-spark-jupyter-notebook-install-locally.md)


