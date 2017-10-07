---
title: "Azure hdınsight'ta aaaIntroduction tooSpark | Microsoft Docs"
description: "Bu makalede bir giriş tooSpark Spark kümesi Hdınsight'ta olarak kullanmak Hdınsight ve hello farklı senaryolar sağlar."
keywords: "apache spark, spark kümesi, giriş toospark nedir hdınsight'ta spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 82334b9e-4629-4005-8147-19f875c8774e
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/12/2017
ms.author: nitinme
ms.openlocfilehash: 41996e733618b8534469fa239b980ac50161a535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toospark-on-hdinsight"></a>Hdınsight üzerinde giriş tooSpark

Bu makalede, hdınsight'ta giriş tooSpark sağlar. <a href="http://spark.apache.org/" target="_blank">Apache Spark</a> bellek içi destekleyen bir açık kaynaklı bir paralel işleme altyapısıdır işliyor tooboost hello büyük veri analizi uygulamalarının performansını. HDInsight'ta Spark kümesi, Azure Depolama (WASB) ve Azure Data Lake Store ile uyumludur. Böylece Azure’da depolanmakta olan verileriniz, Spark kümesi aracılığıyla kolayca işlenebilir.

HDInsight’ta Spark kümesi oluşturduğunuzda, Spark yüklenmiş ve yapılandırılmış olarak Azure işlem kaynakları oluşturursunuz. Yalnızca, toocreate bir Spark küme Hdınsight'ta yaklaşık on dakika sürer. işlenen hello veri toobe Azure Storage veya Azure Data Lake Store içinde depolanır. Bkz. [HDInsight ile Azure Depolama'yı kullanma](hdinsight-hadoop-use-blob-storage.md).

**toocreate bir Spark Hdınsight küme**, bkz: [hızlı başlangıç: Hdınsight'ta Spark kümesi oluşturma ve Jupyter kullanarak etkileşimli sorgusu](hdinsight-apache-spark-jupyter-spark-sql.md).


## <a name="what-is-apache-spark-on-azure-hdinsight"></a>Azure HDInsight’ta Apache Spark nedir?
HDInsight’ta Spark kümeleri, tam olarak yönetilen bir Spark hizmeti sunar. HDInsight'ta bir Spark kümesi oluşturmanın avantajları burada listelenmiştir.

| Özellik | Açıklama |
| --- | --- |
| Spark kümeleri oluşturma kolaylığı |Hello Azure Portal, Azure PowerShell veya hello Hdınsight .NET SDK kullanarak dakikalar içinde Hdınsight'ta yeni bir Spark kümesi oluşturabilirsiniz. Bkz. [HDInsight’ta Spark kümesi kullanmaya başlama](hdinsight-apache-spark-jupyter-spark-sql.md) |
| Kullanım kolaylığı |HDInsight’ta Spark kümesi, Jupyter ve Zeppelin not defterlerini içerir. Etkileşimli veri işleme ve görselleştirme için bunları kullanabilirsiniz.|
| REST API'leri |Hdınsight'ta Spark kümeleri dahil [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server), REST API tabanlı Spark iş sunucusu tooremotely gönderme ve İzleyici işler. |
| Azure Data Lake Store desteği | Hdınsight'ta Spark kümesinde bir ek depolama alanı yanı sıra birincil depolama (yalnızca Hdınsight 3.5 kümeleri ile) olarak yapılandırılmış toouse Azure Data Lake Store olabilir. Data Lake Store hakkında daha fazla bilgi için bkz. [Azure Data Lake Store’a Genel Bakış](../data-lake-store/data-lake-store-overview.md). |
| Azure hizmetleriyle tümleştirme |Hdınsight'ta Spark kümesinde bağlayıcı tooAzure Event Hubs ile birlikte gelir. Müşteriler hello olay hub'ları, ayrıca çok kullanarak akış uygulamaları derleme[Kafka](http://kafka.apache.org/), hangi kullanılabilir zaten Spark bir parçası olarak. |
| R Server desteği | Hdınsight küme toorun bir Spark kümesiyle taahhüt edilen hello hızdaki R hesaplamaları dağıtılmış Spark üzerinde bir R Server ayarlayabilirsiniz. Daha fazla bilgi için bkz. [HDInsight R Server kullanmaya başlama](hdinsight-hadoop-r-server-get-started.md). |
| Üçüncü taraf IDE’lerle tümleştirme | Hdınsight eklentileri gibi Intellij Idea ve toocreate kullanın ve uygulamaları tooan Hdınsight Spark kümesi göndermek Eclipse IDE sağlar. Daha fazla bilgi için bkz. [IntelliJ IDEA için Azure Araç Seti’ni Kullanma](hdinsight-apache-spark-intellij-tool-plugin.md) ve [Eclipse için Azure Araç Seti’ni Kullanma](hdinsight-apache-spark-eclipse-tool-plugin.md).|
| Eş zamanlı sorgular |HDInsight’ta Spark kümeleri, eş zamanlı sorguları destekler. Bu bir kullanıcıdan veya çeşitli kullanıcılar birden çok sorgularından birden çok sorgu sağlar ve uygulamaları tooshare hello aynı küme kaynaklarında. |
| SSD’de önbelleğe alma |Ssd'lerde toohello küme düğümlerine bağlı veya toocache veri bellekte ya da seçebilirsiniz. Bellekte önbelleğe alma hello en iyi sorgu performansını sağlar, ancak pahalı olabilir; Ssd'lerde önbelleğe hello gerek toocreate gerekli toofit bellekte hello tüm veri kümesinin bir boyutu oluşan bir küme olmadan sorgu performansı artırmak için harika bir seçenek sağlar. |
| BI araçları ile tümleştirme |HDInsight’ta Spark kümeleri, veri analizlerine yönelik olarak BI araçları için [Power BI](http://www.powerbi.com/) ve [Tableau](http://www.tableau.com/products/desktop) gibi bağlayıcılar sağlar. |
| Önceden yüklenmiş Anaconda kitaplıkları |HDInsight’ta Spark kümeleri önceden yüklenmiş Anaconda kitaplıkları ile gelir. [Anaconda](http://docs.continuum.io/anaconda/) machine learning, veri analizi, görselleştirme vb. için Kapat too200 kitaplıkları sağlar. |
| Ölçeklenebilirlik |Oluşturma sırasında kümedeki düğüm hello sayısını belirtebilseniz de, toogrow istediğiniz veya hello küme toomatch iş yükü küçültme. Tüm Hdınsight kümeleri hello kümede toochange hello düğüm sayısını sağlar. Ayrıca, tüm hello veri depolandığından Azure Storage veya Data Lake Store Spark kümeleri hiçbir veri kaybı olmadan bırakılabilir. |
| 7/24 Destek |HDInsight’ta Spark kümeleri, kuruluş düzeyinde 7 gün 24 saat destek ve % 99,9 çalışma süreli SLA ile birlikte sunulur. |

## <a name="what-are-hello-use-cases-for-spark-on-hdinsight"></a>Merhaba kullanım durumları için hdınsight'ta Spark nedir?
Hdınsight'ta Spark kümeleri senaryoları aşağıdaki hello etkinleştirin.

### <a name="interactive-data-analysis-and-bi"></a>Etkileşimli veri analizi ve BI
[Öğreticiye bakın](hdinsight-apache-spark-use-bi-tools.md)

HDInsight'ta Apache Spark, verileri Azure Depolama’da veya Azure Data Lake Store’da depolar. İş uzmanları ve temel karar alıcılar çözümleyebilir ve bu verileri raporlar oluşturmak ve Microsoft Power BI toobuild hello çözümlenen verilerden etkileşimli raporlar kullanın. Analistleri küme depolama alanında yapılandırılmamış/yapılandırılmış yarı veriler başlangıç not defterlerini kullanarak hello veri için bir şema tanımlayın ve ardından Microsoft Power BI kullanarak veri modelleri oluşturabilir. HDInsight’da Spark kümeleri, Tableau gibi çeşitli üçüncü taraf BI araçlarını da desteklediğinden veri analistleri, iş uzmanları ve temel karar alıcılar için ideal bir platformdur.

### <a name="spark-machine-learning"></a>Spark Machine Learning
[Öğreticiye bakın: tahmin HVAC verilerini kullanarak bina sıcaklıklarını tahmin etme](hdinsight-apache-spark-ipython-notebook-machine-learning.md)

[Öğreticiye bakın: Yemek inceleme sonuçlarını tahmin etme](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

Apache Spark, Spark üzerinde kurulu bir makine öğrenimi kitaplığı olan ve HDInsight’ta Spark kümesinden kullanabileceğiniz [MLlib](http://spark.apache.org/mllib/) ile birlikte sunulur. HDInsight’ta Spark kümesi, dağıtımı Python tarafından yapılan ve makine öğrenimi için çeşitli paketlere sahip Anaconda’yı da içerir. Jupyter ve Zeppelin not defterleri için yerleşik destekle bir araya geldiğinde, makine öğrenimi uygulamaları oluşturmak için birinci sınıf bir ortama sahip olmanızı sağlar.

### <a name="spark-streaming-and-real-time-data-analysis"></a>Spark akış ve gerçek zamanlı veri çözümleme
[Öğreticiye bakın](hdinsight-apache-spark-eventhub-streaming.md)

HDInsight’ta Spark kümeleri, gerçek zamanlı analiz çözümleri oluşturmak için zengin destek sunar. Spark zaten bağlayıcılar tooingest veriler Kafka, Flume, Twitter, ZeroMQ veya TCP yuvaları gibi pek çok kaynaktan sahipken, hdınsight'ta Spark Azure Event hubs'tan veri alma için birinci sınıf destek eklemektedir. Olay hub'ları, Azure üzerinde en yaygın şekilde kullanılan sıraya alma hizmeti hello ' dir. Event Hubs için sunulan kullanıma hazır destek, HDInsight’ta Spark kümelerini gerçek zamanlı analiz işlem hattı oluşturmak için ideal bir platform hâline getirir.

## <a name="next-steps"></a>Spark kümesinin birer parçası olarak hangi bileşenler dahildir?
Hdınsight'ta Spark kümeleri hello kümelerinde varsayılan olarak kullanılabilir bileşenleri aşağıdaki hello içerir.

* [Spark Core](https://spark.apache.org/docs/1.5.1/). Spark Core, Spark SQL, Spark akış API’leri, GraphX ve MLlib’i içerir.
* [Anaconda](http://docs.continuum.io/anaconda/)
* [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server)
* [Jupyter not defteri](https://jupyter.org)
* [Zeppelin not defteri](http://zeppelin-project.org/)

Hdınsight'ta Spark kümeleri de sağlar bir [ODBC sürücüsü](http://go.microsoft.com/fwlink/?LinkId=616229) Microsoft Power BI ve Tableau gibi BI araçlarından hdınsight'ta bağlantı tooSpark kümeleri için.

## <a name="where-do-i-start"></a>Nereden başlamalıyım?
İşe HDInsight’ta Spark kümesi oluşturarak başlayın. Bkz. [Hızlı Başlangıç: HDInsight Linux üzerinde Spark kümesi oluşturma ve Jupyter’i kullanarak etkileşimli sorgu çalıştırma](hdinsight-apache-spark-jupyter-spark-sql.md). 

## <a name="next-steps"></a>Sonraki Adımlar
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
* [Azure HDInsight'ta Apache Spark ile ilgili bilinen sorunlar](hdinsight-apache-spark-known-issues.md).
