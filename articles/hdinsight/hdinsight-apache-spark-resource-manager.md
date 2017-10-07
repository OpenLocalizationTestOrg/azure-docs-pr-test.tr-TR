---
title: "Küme Azure Hdınsight'ta Apache Spark için aaaManage kaynakları | Microsoft Docs"
description: "Toouse yönetmek daha iyi performans için Azure hdınsight'ta Spark kümeleri için kaynaklar hakkında bilgi edinin."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9da7d4e3-458e-4296-a628-77b14643f7e4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: e18682a24f77494db884105f9db03c0a350ddad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-resources-for-apache-spark-cluster-on-azure-hdinsight"></a>Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme 

Bu makalede nasıl tooaccess hello arabirimleri Ambari UI, YARN kullanıcı Arabiriminde ve hello Spark geçmişi sunucu gibi Spark kümenizle ilişkilendirilmiş öğreneceksiniz. Nasıl tootune hello en iyi performans için küme yapılandırma hakkında bilgi edineceksiniz.

**Ön koşullar:**

Merhaba şunlara sahip olmanız gerekir:

* Azure aboneliği. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Hdınsight'ta bir Apache Spark kümesi. Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="how-do-i-launch-hello-ambari-web-ui"></a>Merhaba Ambari Web kullanıcı arabirimini nasıl başlatma?
1. Merhaba gelen [Azure Portal](https://portal.azure.com/), (, onu toohello Sabitle) hello Panosu'ndan hello kutucuğuna Spark kümenizin tıklayın. Tooyour küme altında da gidebilirsiniz **tümüne Gözat** > **Hdınsight kümeleri**.
2. Merhaba Spark kümesi dikey penceresinden tıklatın **Pano**. İstendiğinde, hello Spark küme için hello yönetici kimlik bilgilerini girin.

    ![Ambari başlatma](./media/hdinsight-apache-spark-resource-manager/hdinsight-launch-cluster-dashboard.png "Kaynak Yöneticisi'ni Başlat")
3. Aşağıda gösterildiği gibi bu hello Ambari Web kullanıcı ARABİRİMİ'nde, belirmelidir.

    ![Ambari Web kullanıcı Arabirimi](./media/hdinsight-apache-spark-resource-manager/ambari-web-ui.png "Ambari Web kullanıcı Arabirimi")   

## <a name="how-do-i-launch-hello-spark-history-server"></a>Merhaba Spark geçmişi sunucu nasıl başlatma?
1. Merhaba gelen [Azure Portal](https://portal.azure.com/), (, onu toohello Sabitle) hello Panosu'ndan hello kutucuğuna Spark kümenizin tıklayın.
2. Hello dikey penceresinde altında küme **hızlı bağlantılar**, tıklatın **küme Panosu**. Merhaba, **küme Panosu** dikey penceresinde tıklatın **Spark geçmişi sunucu**.

    ![Spark geçmişi sunucu](./media/hdinsight-apache-spark-resource-manager/launch-history-server.png "Spark geçmişi sunucu")

    İstendiğinde, hello Spark küme için hello yönetici kimlik bilgilerini girin.

## <a name="how-do-i-launch-hello-yarn-ui"></a>Merhaba Yarn kullanıcı Arabiriminde nasıl başlatma?
Merhaba Spark kümesi üzerinde çalışmakta olan hello YARN kullanıcı Arabiriminde toomonitor uygulamaları kullanabilir.

1. Merhaba küme dikey penceresinden tıklayın **küme Panosu**ve ardından **YARN**.

    ![YARN kullanıcı arabirimini Başlat](./media/hdinsight-apache-spark-resource-manager/launch-yarn-ui.png)

   > [!TIP]
   > Alternatif olarak, hello YARN kullanıcı Arabiriminde hello Ambari UI alanından başlatabilirsiniz. Merhaba küme dikey penceresinden toolaunch hello Ambari UI'ı tıklatın **küme Panosu**ve ardından **Hdınsight küme Panosu**. Hello ifadesini Ambari UI'ı tıklatın **YARN**, tıklatın **hızlı bağlantılar**hello etkin Kaynak Yöneticisi'ni tıklatın ve ardından **ResourceManager UI**.
   >
   >

## <a name="what-is-hello-optimum-cluster-configuration-toorun-spark-applications"></a>Merhaba optimum küme yapılandırma toorun Spark uygulamaları nedir?
uygulama gereksinimleri bağlı olarak Spark yapılandırması için kullanılan anahtar parametreleri hello üç `spark.executor.instances`, `spark.executor.cores`, ve `spark.executor.memory`. Bir yürütücü Spark uygulama için başlatılan bir işlemdir. Merhaba çalışan düğümünde çalışır ve hello görevlerini Merhaba uygulaması için sorumlu toocarry olduğu. Hello varsayılan sayısı yürütücüler ve her küme için hello Yürütücü boyutları hello sayısını çalışan düğümleri ve hello alt düğüm boyutu temel alınarak hesaplanır. Bunlar depolanmış `spark-defaults.conf` hello küme baş düğümler üzerinde.

Merhaba üç yapılandırma parametreleri (için hello kümede çalışan tüm uygulamaları) hello küme düzeyinde yapılandırılabilir veya her tek tek uygulama için belirtilebilir.

### <a name="change-hello-parameters-using-ambari-ui"></a>Ambari kullanıcı arabirimini kullanarak hello parametrelerini değiştirin
1. Ambari UI Hello tıklatın **Spark**, tıklatın **yapılandırmalar**, genişletin ve ardından **özel spark-varsayılanları**.

    ![Ambari kullanarak parametrelerini](./media/hdinsight-apache-spark-resource-manager/set-parameters-using-ambari.png)
2. Merhaba varsayılan değerleri hello kümede aynı anda çalıştırmak iyi toohave 4 Spark uygulamalardır. Aşağıda gösterildiği gibi değişiklikler hello kullanıcı arabirimi, bu değerleri kullanabilirsiniz.

    ![Ambari kullanarak parametrelerini](./media/hdinsight-apache-spark-resource-manager/set-executor-parameters.png)
3. Tıklatın **kaydetmek** toosave hello yapılandırma değişiklikleri. Merhaba hello sayfanın en üstünde, istenir tüm hello toorestart etkilenen hizmetler. Tıklatın **yeniden**.

    ![Hizmetlerini yeniden başlatın](./media/hdinsight-apache-spark-resource-manager/restart-services.png)

### <a name="change-hello-parameters-for-an-application-running-in-jupyter-notebook"></a>Jupyter not defteri çalışan bir uygulama için Hello parametrelerini değiştir
Merhaba Jupyter not defteri çalışan uygulamalar için hello kullanabilirsiniz `%%configure` Sihirli toomake hello yapılandırma değişiklikleri. İdeal olarak, birinci kod hücresini çalıştırmadan önce Merhaba uygulaması hello başında gibi değişiklikler yapmanız gerekir. Bu, hello yapılandırmayı uygulanan toohello Livy sağlar oluşturulduğu oturumu. Merhaba uygulamada daha sonraki bir aşamada toochange hello yapılandırma istiyorsanız hello kullanmalısınız `-f` parametresi. Ancak, tüm hello ilerleme şekilde yaparak uygulama kaybolur.

Aşağıdaki Hello parçacığı nasıl toochange hello Jupyter'de çalışan bir uygulama için yapılandırma gösterilir.

    %%configure
    {"executorMemory": "3072M", "executorCores": 4, "numExecutors":10}

Yapılandırma parametreleri de JSON dizesi olarak geçirilmelidir ve hello sonraki satırda hello Sihirli sonra hello örnek sütununda gösterildiği gibi olması gerekir.

### <a name="change-hello-parameters-for-an-application-submitted-using-spark-submit"></a>Değişiklik hello parametreleri kullanılarak gönderilen bir uygulama için spark gönderme
Olan bir örneğini nasıl toochange hello yapılandırma parametreleri kullanılarak gönderilen bir batch uygulaması için komutu aşağıdaki `spark-submit`.

    spark-submit --class <hello application class tooexecute> --executor-memory 3072M --executor-cores 4 –-num-executors 10 <location of application jar file> <application parameters>

### <a name="change-hello-parameters-for-an-application-submitted-using-curl"></a>CURL kullanılarak gönderilen bir uygulama için Hello parametrelerini değiştir
Komutu aşağıdaki nasıl toochange hello cURL kullanarak gönderilen bir batch uygulaması için yapılandırma parametreleri, bir örnek verilmiştir.

    curl -k -v -H 'Content-Type: application/json' -X POST -d '{"file":"<location of application jar file>", "className":"<hello application class tooexecute>", "args":[<application parameters>], "numExecutors":10, "executorMemory":"2G", "executorCores":5' localhost:8998/batches

### <a name="how-do-i-change-these-parameters-on-a-spark-thrift-server"></a>Spark Thrift sunucusunun bu parametrelere nasıl değişiyor?
Spark Thrift sunucusu JDBC/ODBC erişim tooa Spark kümesi sağlar ve kullanılan tooservice Spark SQL sorguları. Araçlar Power BI, Tableau vb. gibi çalışır. ODBC Protokolü toocommunicate Spark Thrift sunucusunun tooexecute Spark SQL sorguları ile Spark uygulaması olarak kullanın. Spark kümesi oluşturduğunuzda, Spark Thrift sunucusunun başlatılacağı, hello her baş düğüm birinde iki örneği. Her Spark Thrift sunucusunun Spark uygulama YARN kullanıcı Arabiriminde hello olarak görünür olur.

Spark Thrift sunucusunun kullandığı Spark dinamik Yürütücü ayırma ve bu nedenle hello `spark.executor.instances` kullanılmaz. Bunun yerine, Spark Thrift sunucusunun kullandığı `spark.dynamicAllocation.minExecutors` ve `spark.dynamicAllocation.maxExecutors` toospecify hello Yürütücü sayısı. yapılandırma parametrelerini hello `spark.executor.cores` ve `spark.executor.memory` olan toomodify hello Yürütücü boyutu kullanılır. Bu parametreler aşağıda gösterildiği gibi değiştirebilirsiniz.

* Merhaba genişletin **spark thrift sparkconf Gelişmiş** kategori tooupdate hello parametreleri `spark.dynamicAllocation.minExecutors`, `spark.dynamicAllocation.maxExecutors`, ve `spark.executor.memory`.

    ![Spark thrift sunucusunu yapılandırın](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-1.png)    
* Merhaba genişletin **özel spark thrift sparkconf** kategori tooupdate hello parametresi `spark.executor.cores`.

    ![Spark thrift sunucusunu yapılandırın](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-2.png)

### <a name="how-do-i-change-hello-driver-memory-of-hello-spark-thrift-server"></a>Merhaba sürücü bellek hello Spark Thrift sunucusunun nasıl değişiyor?
Spark Thrift sunucusunun sürücü bellek Hello Toplam RAM hello baş düğüm 14 GB'den büyük boyutudur hello baş düğüm RAM boyutunun yapılandırılmış too25% sağlanır. Merhaba Ambari UI toochange hello sürücü bellek yapılandırması, aşağıda gösterildiği gibi kullanabilirsiniz.

* Ambari UI Hello tıklatın **Spark**, tıklatın **yapılandırmalar**, genişletin **spark env Gelişmiş**, hello değeri girin **spark_thrift_cmd_opts**.

    ![Spark thrift sunucusunun RAM yapılandırın](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-ram.png)

## <a name="i-do-not-use-bi-with-spark-cluster-how-do-i-take-hello-resources-back"></a>I BI ile Spark kümesi kullanmayın. Nasıl hello kaynakları geri yararlanabilir mi?
Spark dinamik ayırma kullandığımız bu yana hello thrift sunucusu tarafından kullanılan kaynakları hello hello iki uygulama yöneticileri için kaynaklardır. Merhaba kümede çalışan Thrift sunucusunun Hizmetleri durdurmalı bu kaynakları hello tooreclaim.

1. Merhaba Ambari UI hello sol bölmesinde, öğesini tıklatın **Spark**.
2. Merhaba sonraki sayfasında tıklatın **Spark Thrift sunucuları**.

    ![Thrift sunucuyu yeniden başlatın](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-1.png)
3. Hangi hello üzerinde Spark Thrift sunucusunun çalıştığından hello iki headnodes görmeniz gerekir. Merhaba headnodes birini tıklatın.

    ![Thrift sunucuyu yeniden başlatın](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-2.png)
4. Hello sonraki sayfada bu headnode üzerinde çalışan tüm hello hizmetler listelenir. Merhaba listeden hello açılan düğmesine bir sonraki tooSpark Thrift sunucusunun tıklayın ve ardından **durdurmak**.

    ![Thrift sunucuyu yeniden başlatın](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-3.png)
5. Diğer headnode de hello bu adımları yineleyin.

## <a name="my-jupyter-notebooks-are-not-running-as-expected-how-can-i-restart-hello-service"></a>My Jupyter not defterleri beklendiği gibi çalışmıyor. Merhaba hizmetini nasıl yeniden başlatabilirsiniz?
Merhaba Ambari Web kullanıcı Arabirimi, yukarıda gösterildiği gibi başlatın. Merhaba sol gezinti bölmesinden tıklatın **Jupyter**, tıklatın **hizmet eylemleri**ve ardından **yeniden tüm**. Bu, tüm hello headnodes üzerinde hello Jupyter hizmetini başlatır.

    ![Restart Jupyter](./media/hdinsight-apache-spark-resource-manager/restart-jupyter.png "Restart Jupyter")

## <a name="how-do-i-know-if-i-am-running-out-of-resources"></a>Kaynaklar yetersiz çalıştırdığım olmadığını nasıl anlayabilirim?
Merhaba Yarn kullanıcı Arabiriminde, yukarıda gösterildiği gibi başlatın. Merhaba ekranında üstünde küme ölçümlerini tabloda değerlerini denetleyin **kullanılan bellek** ve **bellek toplam** sütun. Merhaba 2 değerler çok yakın ise yeterli kaynakları toostart hello sonraki uygulama olmayabilir. Merhaba aynı toohello geçerlidir **VCores kullanılan** ve **VCores toplam** sütun. Varsa ayrıca hello ana görünümünde, bir uygulama içinde stayed **kabul edilen** durumu ve içine geçiş değil **çalıştıran** ya da **başarısız** durumunda, bu da olabilir bir göstergesi Bu BT yeterli kaynakları toostart alamıyorsanız.

    ![Resource Limit](./media/hdinsight-apache-spark-resource-manager/resource-limit.png "Resource Limit")

## <a name="how-do-i-kill-a-running-application-toofree-up-resource"></a>Ne ı KILL çalışan bir uygulama toofree kaynağını?
1. Merhaba Yarn kullanıcı Arabiriminde, hello sol panelindeki tıklatın **çalıştıran**. Çalışan uygulamalar hello listeden hello uygulama toobe sonlandırıldı ve üzerinde hello tıklatın belirlemek **kimliği**.

    ![App1 KILL](./media/hdinsight-apache-spark-resource-manager/kill-app1.png "KILL App1")

2. Tıklatın **KILL uygulama** hello üzerinde sağ üst köşesindeki, ardından **Tamam**.

    ![App2 KILL](./media/hdinsight-apache-spark-resource-manager/kill-app2.png "KILL App2")

## <a name="see-also"></a>Ayrıca bkz.
* [HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama](hdinsight-apache-spark-job-debugging.md)

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
