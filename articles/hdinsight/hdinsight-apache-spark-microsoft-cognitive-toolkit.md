---
title: "aaaMicrosoft Azure Hdınsight Spark ile kavrama Araç Seti için derin öğrenme | Microsoft Docs"
description: "Eğitilmiş bir Microsoft Bilişsel araç nasıl derin learning modeli Azure Hdınsight Spark kümesinde hello Spark Python API kullanarak uygulanan tooa dataset olabilir öğrenin."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: c296d4697f16d4ef6a958fdb55289807d745ea40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-microsoft-cognitive-toolkit-deep-learning-model-with-azure-hdinsight-spark-cluster"></a>Microsoft Azure Hdınsight Spark küme modeliyle öğrenme derin bir Bilişsel araç kullanma

Bu makaledeki adımları izleyerek hello.

1. Özel bir komut dosyası tooinstall Microsoft Bilişsel Araç Seti Azure Hdınsight Spark kümesi üzerinde çalıştırın.

2. Bir Jupyter not defteri toohello Spark küme toosee nasıl karşıya tooapply bir eğitilen Microsoft Bilişsel Araç Seti modeli toofiles hello kullanarak bir Azure Blob Storage hesabında öğrenme derin [Spark Python API (PySpark)](https://spark.apache.org/docs/0.9.0/python-programming-guide.html)

## <a name="prerequisites"></a>Ön koşullar

* **Bir Azure aboneliği**. Bu öğreticiye başlamadan önce bir Azure aboneliğinizin olması gerekir. Bkz. [Ücretsiz Azure hesabınızı hemen oluşturun](https://azure.microsoft.com/free).

* **Azure Hdınsight Spark kümesi**. Bu makalede, bir Spark 2.0 kümesi oluşturun. Yönergeler için bkz: [Azure hdınsight'ta Apache Spark oluşturma küme](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="how-does-this-solution-flow"></a>Bu çözümün nasıl akıyor?

Bu çözüm, bu makalede ve bu öğreticinin bir parçası olarak karşıya Jupyter not defteri arasında bölünür. Bu makalede, hello aşağıdaki adımları tamamlayın:

* Betik eylemi bir Hdınsight Spark kümesinde tooinstall Microsoft Bilişsel Araç Seti ve Python paketlerini çalıştırın.
* Merhaba çözüm toohello Hdınsight Spark kümesinde çalışan hello Jupyter not defteri karşıya yükleyin.

Merhaba bir hello Jupyter Not Defteri en aşağıdaki kalan adımları ele alınmıştır.

- Yük örnek görüntülere Spark Resiliant dağıtılmış Dataset ya da RDD
   - Modülleri yüklemek ve hazır tanımlayın
   - Merhaba dataset hello Spark kümesinde yerel olarak indir
   - Bir RDD Hello dataset Dönüştür
- Bilişsel Araç Seti modeli kullanarak puan hello görüntüleri
   - Eğitilmiş hello Bilişsel Araç Seti modeli toohello Spark kümesi indirin
   - Alt düğümler tarafından kullanılan işlevler toobe tanımlayın
   - Çalışan düğümü puan hello görüntülerde
   - Model doğruluğundan değerlendir


## <a name="install-microsoft-cognitive-toolkit"></a>Microsoft Bilişsel Araç Seti yükleyin

Betik eylemi kullanarak Spark kümesinde Microsoft Bilişsel Araç Seti yükleyebilirsiniz. Betik eylemi özel komut dosyaları tooinstall bileşenler varsayılan olarak kullanılabilir değil hello kümede kullanır. Hdınsight .NET SDK kullanarak ya da Azure PowerShell kullanarak hello Azure Portal, özel betikten hello kullanabilirsiniz. Merhaba betik tooinstall hello Araç Seti parçası olarak küme oluşturma veya hello küme hazır ve çalışır sonra aşağıdakilerden birini de kullanabilirsiniz. 

Bu makalede, Hello Küme oluşturulduktan sonra hello portal tooinstall hello araç seti, kullanırız. Diğer yolları toorun hello özel komut dosyaları için bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md).

### <a name="using-hello-azure-portal"></a>Hello Azure Portal kullanarak

Toouse hello Azure Portal toorun eylem nasıl komut dosyası ile ilgili yönergeler için bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md#use-a-script-action-during-cluster-creation). Girişleri tooinstall Microsoft Bilişsel Araç Seti aşağıdaki hello sağladığınızdan emin olun.

* Merhaba betik eylem adı için bir değer girin.

* İçin **betik URI Bash**, girin `https://raw.githubusercontent.com/Azure-Samples/hdinsight-pyspark-cntk-integration/master/cntk-install.sh`.

* Head ve çalışan düğümleri üzerinde yalnızca hello hello komut dosyasını çalıştırın ve tüm diğer onay kutularını temizleyin hello emin olun.

* **Oluştur**'a tıklayın.

## <a name="upload-hello-jupyter-notebook-tooazure-hdinsight-spark-cluster"></a>Merhaba Jupyter not defteri tooAzure Hdınsight Spark kümesi karşıya yükle

toouse hello Microsoft Bilişsel Araç Seti hello Azure Hdınsight Spark kümesinde ile Merhaba Jupyter not defteri yüklemelisiniz **CNTK_model_scoring_on_Spark_walkthrough.ipynb** toohello Azure Hdınsight Spark kümesi. Bu not defteri github'da kullanılabilir [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration).

1. Kopya hello GitHub deposunu [https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration](https://github.com/Azure-Samples/hdinsight-pyspark-cntk-integration). Yönergeler tooclone için bkz: [depo kopyalama](https://help.github.com/articles/cloning-a-repository/).

2. Zaten sağlanmış tıklatın hello Spark kümesi dikey Hello Azure Portalı ' açmak **küme Panosu**ve ardından **Jupyter not defteri**.

    Toohello URL giderek hello Jupyter not defteri başlatabilirsiniz `https://<clustername>.azurehdinsight.net/jupyter/`. Değiştir \<clustername > Hdınsight kümenize hello adı.

3. Merhaba Jupyter not defteri tıklatın **karşıya** hello sağ üst köşesinde ve hello GitHub deposunu kopyaladığınız toohello konumuna gidin.

    ![Hdınsight Spark kümesinde Jupyter not defteri tooAzure karşıya](./media/hdinsight-apache-spark-microsoft-cognitive-toolkit/hdinsight-microsoft-cognitive-toolkit-load-jupyter-notebook.png "karşıya Jupyter not defteri tooAzure Hdınsight Spark kümesi")

4. Tıklatın **karşıya** yeniden.

5. Hello dizüstü karşıya yüklendikten sonra hello dizüstü hello adına tıklayın ve ardından nasıl tooload veri kümesi hello ve hello öğretici gerçekleştirmek hello Not kendisini hello yönergeleri izleyin.

## <a name="see-also"></a>Ayrıca bkz.
* [Genel Bakış: Azure HDInsight’ta Apache Spark](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Senaryolar
* [BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme](hdinsight-apache-spark-use-bi-tools.md)
* [Machine Learning ile Spark: HVAC verilerini kullanarak bina sıcaklığını çözümlemek için HDInsight’ta Spark kullanma](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Machine Learning ile Spark: Spark Hdınsight toopredict yemek İnceleme sonuçlarını içinde kullanma](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark Akış: Gerçek zamanlı akış uygulamaları oluşturmak için HDInsight’ta Spark kullanma](hdinsight-apache-spark-eventhub-streaming.md)
* [HDInsight’ta Spark kullanarak Web sitesi günlüğü çözümlemesi](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [HDInsight’ta Spark kullanarak Application Insight telemetri verilerinin analizi](hdinsight-spark-analyze-application-insight-logs.md)

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

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
