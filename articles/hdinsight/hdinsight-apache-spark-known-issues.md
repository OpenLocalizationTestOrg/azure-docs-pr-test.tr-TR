---
title: "Azure Hdınsight'ta Apache Spark aaaTroubleshoot sorunları küme | Microsoft Docs"
description: "Azure hdınsight'ta Spark kümeleri ilgili tooApache sorunlar hakkında bilgi edinmek ve nasıl toowork geçici olanlar."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 610c4103-ffc8-4ec0-ad06-fdaf3c4d7c10
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 7373b90524ae5dbb10ab8ded593aa38d12c14b55
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="known-issues-for-apache-spark-cluster-on-hdinsight"></a>Hdınsight'ta Apache Spark kümesi için bilinen sorunlar

Bu belge, bilinen sorunlar hello Hdınsight Spark genel Önizleme için tüm hello izler.  

## <a name="livy-leaks-interactive-session"></a>Etkileşimli oturum Livy sızdırıyor
Bir etkileşimli oturum hala canlı Livy (Ambari veya tooheadnode 0 sanal makine yeniden başlatma nedeniyle) yeniden başlatıldığında bir etkileşimli iş oturumu sızmasını. Bu nedenle, yeni işleri can hello kabul edilen durumu takılmış ve başlatılamıyor.

**Azaltma:**

Aşağıdaki yordam tooworkaround hello sorunu hello kullan:

1. SSH headnode içine. Bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Komut toofind Merhaba uygulaması aşağıdaki çalışma hello hello etkileşimli işlerin kimliklerini Livy başlatıldı. 
   
        yarn application –list
   
    Merhaba işleri ile Livy etkileşimli oturum, hello için belirtilen hiçbir açık adları başlatılmış hello varsayılan proje adları Livy olacaktır Jupyter not defteri tarafından başlatılan Livy oturum hello iş adı başlayacak remotesparkmagics_ * ile. 
3. Komut tookill aşağıdaki hello bu işleri çalıştırın. 
   
        yarn application –kill <Application ID>

Yeni iş çalışmaya başlar. 

## <a name="spark-history-server-not-started"></a>Spark geçmişi sunucu başlatılmadı
Spark geçmişi sunucu bir küme oluşturulduktan sonra otomatik olarak başlatılan bir dosya değil.  

**Azaltma:** 

El ile Merhaba geçmişi sunucu Ambari başlatın.

## <a name="permission-issue-in-spark-log-directory"></a>Spark günlük dizini izin sorunu
Hdiuser spark-submit işlemiyle gönderdiğinde, bir hata java.io.FileNotFoundException yoktur: /var/log/spark/sparkdriver_hdiuser.log (izni reddedildi) ve hello sürücü günlüğü yazılmadı. 

**Azaltma:**

1. Hdiuser toohello Hadoop grubunu ekleyin. 
2. 777 izinleri üzerinde /var/log/spark Küme oluşturulduktan sonra sağlayın. 
3. Ambari toobe bir dizin 777 izinlerle kullanarak hello spark günlük konumunu güncelleştirin.  
4. Çalışma spark-gönderme sudo.  

## <a name="spark-phoenix-connector-is-not-supported"></a>Spark Phoenix bağlayıcı desteklenmez

Şu anda hello Spark Phoenix bağlayıcı Hdınsight Spark kümesinde ile desteklenmez.

**Azaltma:**

Merhaba Spark HBase bağlayıcı yerine kullanmanız gerekir. Yönergeler için bkz [nasıl toouse Spark HBase bağlayıcı](https://blogs.msdn.microsoft.com/azuredatalake/2016/07/25/hdinsight-how-to-use-spark-hbase-connector/).

## <a name="issues-related-toojupyter-notebooks"></a>TooJupyter not defterlerini ilgili sorunlar
Aşağıda bazı bilinen sorunlar ilgili tooJupyter not defterlerini verilmiştir.

### <a name="notebooks-with-non-ascii-characters-in-filenames"></a>Dizüstü bilgisayarlarla dosya adları ASCII olmayan karakterler
Spark Hdınsight kümelerinde kullanılan Jupyter not defterleri, ASCII olmayan karakterler adlarında olmalıdır. Tooupload hello Jupyter ASCII olmayan dosya adı olan kullanıcı Arabirimi üzerinden dosya çalışırsanız, sessizce başarısız olur (diğer bir deyişle, Jupyter olmaz sağlar, hello dosyasını karşıya yükleyin, ancak görünebilen bir hata ya da throw olmaz). 

### <a name="error-while-loading-notebooks-of-larger-sizes"></a>Daha büyük boyutta not defterlerini yüklenirken hata oluştu
Bir hata görebilirsiniz ** `Error loading notebook` ** daha büyük boyutta not defterlerini yükleme.  

**Azaltma:**

Bu hata alırsanız, bozuk veya kayıp verilerinizi gelmez.  Yine diskte, dizüstü bilgisayarlarda `/var/lib/jupyter`, ve SSH hello küme tooaccess bunları. Bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

SSH kullanarak toohello küme bağlandıktan sonra önemli bilgileri hello Not yedekleme tooprevent hello kaybı olarak (SCP veya WinSCP kullanarak), küme tooyour yerel makineden defterlerinizi kopyalayabilirsiniz. Bundan sonra SSH tüneli bağlantı noktası 8001 tooaccess Jupyter adresindeki, headnode içine hello ağ geçidi üzerinden geçmeden yapabilirsiniz.  Buradan, dizüstü bilgisayarınızı hello çıktısını temizleyin ve yeniden kaydedin toominimize hello not defterinin boyutu.

tooprevent hello bazı en iyi uygulamaları izlemelidir gelecekte oluşmasını bu hatadan:

* Önemli tookeep hello dizüstü bilgisayar boyutu küçük değil. Spark işleriniz tooJupyter hello not defterinde kalıcı geri gönderilen çıktı.  Jupyter ile en iyi uygulama çalıştıran genel tooavoid içinde olduğu `.collect()` üzerinde büyük RDD'ın veya dataframes; bir RDD'in içeriği adresindeki toopeek istiyorsanız, bunun yerine, çalışan göz önünde bulundurun `.take()` veya `.sample()` böylelikle, çıkış çok büyük açılmıyor.
* Bir not defteri kaydettiğinizde, ayrıca, Temizle tüm hücreleri tooreduce hello boyutu çıktı.

### <a name="notebook-initial-startup-takes-longer-than-expected"></a>Not defteri başlangıç beklenenden uzun sürüyor
Jupyter Not Defteri kullanarak Spark Sihirli ilk kod deyiminde birden fazla bir dakika sürebilir.  

**Açıklama:**

Merhaba birinci kod hücresini çalıştırdığınızda çünkü bu gerçekleşir. Merhaba arka planda bu başlatır oturum yapılandırması ve Spark, SQL ve Hive bağlamları ayarlayın. Bu içerikler ayarladıktan sonra hello ilk deyimi çalıştırın ve bu hello deyimi uzun süre toocomplete sürdü hello izlenim sağlar.

### <a name="jupyter-notebook-timeout-in-creating-hello-session"></a>Merhaba oturum oluşturmayı Jupyter not defteri zaman aşımına uğradı
Spark kümesi kaynaklar yetersiz olduğunda hello Spark ve Pyspark çekirdekler hello Jupyter Not toocreate hello oturum çalışırken zaman aşımına uğrayacağı. 

**Azaltıcı Etkenler:** 

1. Bazı kaynaklar tarafından Spark kümenizdeki boşaltmak:
   
   * Diğer Spark not defterlerini toohello giderek kapatın ve durdurmak menüsü veya kapatma hello not defteri Explorer'da tıklatarak durduruluyor.
   * YARN diğer Spark uygulamalardan durduruluyor.
2. Yukarı toostart çalıştığınız hello dizüstü yeniden başlatın. Yeterli kaynaklara şimdi bir oturum, toocreate kullanılabilir olması gerekir.

## <a name="see-also"></a>Ayrıca bkz.
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
* [Intellij Idea toocreate için Hdınsight araçları eklentisi kullanma ve Spark Scala uygulamaları gönderin](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Uzaktan Intellij Idea toodebug Spark uygulamaları için Hdınsight araçları eklentisi kullanma](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Jupyter not defterleri ile dış paketleri kullanma](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter bilgisayarınıza yüklemek ve tooan Hdınsight Spark kümesi bağlanın](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Kaynakları yönetme
* [Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme](hdinsight-apache-spark-resource-manager.md)
* [HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama](hdinsight-apache-spark-job-debugging.md)

