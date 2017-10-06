---
title: "aaaScript eylemi - Azure hdınsight'ta Jupyter ile yükleme Python paketlerini | Microsoft Docs"
description: "Nasıl toouse betik eylemi tooconfigure Jupyter not defterleri ile Hdınsight Spark kullanılabilir kümeleri toouse dış python paketlerini ilişkin adım adım yönergeler için."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21978b71-eb53-480b-a3d1-c5d428a7eb5b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 54db79e67995dee7ca00abff979f7d74ae5ab9cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-script-action-tooinstall-external-python-packages-for-jupyter-notebooks-in-apache-spark-clusters-on-hdinsight"></a>Hdınsight'ta Apache Spark kümeleri Jupyter not defterlerinde için betik eylemi tooinstall dış Python paketlerini kullanma
> [!div class="op_single_selector"]
> * [Hücre Sihirli kullanma](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
> * [Betik eylemi kullanarak](hdinsight-apache-spark-python-package-installation.md)
>
>

Nasıl toouse betik eylemleri tooconfigure Hdınsight (Linux) toouse dış, Apache Spark kümesinde topluluk-katkıda öğrenin **python** hello kümede olmayan paketler dahil Giden kutusu.

> [!NOTE]
> Jupyter Not Defteri kullanarak da yapılandırabilirsiniz `%%configure` Sihirli toouse dış paketler. Yönergeler için bkz: [hdınsight'ta Apache Spark kümeleri Jupyter not defterlerinde ile dış paketleri kullanma](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md).
> 
> 

Merhaba arayabilirsiniz [paket dizini](https://pypi.python.org/pypi) hello tam kullanılabilir paketler listesi. Ayrıca, diğer kaynaklardan kullanılabilir paketlerin listesini alabilirsiniz. Örneğin, kullanılabilir hale paketlerini yükleyebilirsiniz [Anaconda](https://docs.continuum.io/anaconda/pkg-docs) veya [conda oluşturmasına](https://conda-forge.github.io/feedstocks.html).

Bu makalede, öğreneceksiniz nasıl tooinstall hello [TensorFlow](https://www.tensorflow.org/) kümenizde betik Actoin kullanarak paketini ve hello Jupyter not defteri kullanın.

## <a name="prerequisites"></a>Ön koşullar
Merhaba şunlara sahip olmanız gerekir:

* Azure aboneliği. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Hdınsight'ta bir Apache Spark kümesi. Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).

   > [!NOTE]
   > Hdınsight Linux üzerinde Spark kümesi zaten yoksa, küme oluşturma sırasında betik eylemleri çalıştırabilirsiniz. Merhaba belgeleri ziyaret [toouse özel eylemler nasıl komut dosyası](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).
   > 
   > 

## <a name="use-external-packages-with-jupyter-notebooks"></a>Jupyter not defterleri ile dış paketleri kullanma

1. Merhaba gelen [Azure Portal](https://portal.azure.com/), (, onu toohello Sabitle) hello Panosu'ndan hello kutucuğuna Spark kümenizin tıklayın. Tooyour küme altında da gidebilirsiniz **tümüne Gözat** > **Hdınsight kümeleri**.   

2. Merhaba Spark kümesi dikey penceresinden tıklatın **betik eylemleri** altında **kullanım**. Merhaba baş düğümler ve hello çalışan düğümleri TensorFlow yükler hello özel eylemini çalıştırın. Merhaba bash komut dosyası, gelen başvurulabilir: https://hdiconfigactions.blob.core.windows.net/linuxtensorflow/tensorflowinstall.sh ziyaret hello belgelerine [toouse özel eylemler nasıl komut dosyası](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).

   > [!NOTE]
   > Merhaba küme yüklemelerde iki python vardır. Spark hello Anaconda python yükleme konumunda bulunan kullanacağınız `/usr/bin/anaconda/bin`. Bu yükleme, özel eylemleri başvuru `/usr/bin/anaconda/bin/pip` ve `/usr/bin/anaconda/bin/conda`.
   > 
   > 

3. Bir PySpark Jupyter not defteri açın

    ![Yeni bir Jupyter not defteri oluşturma](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-create-notebook.png "Yeni bir Jupyter not defteri oluşturma")

4. Yeni bir not defteri oluşturulur ve Untitled.pynb hello adı ile. Merhaba üstünde Hello dizüstü bilgisayar adına tıklayın ve kolay bir ad girin.

    ![Merhaba dizüstü bilgisayar için bir ad](./media/hdinsight-apache-spark-python-package-installation/hdinsight-spark-name-notebook.png "hello dizüstü bilgisayar için bir ad sağlayın")

5. Şimdi olacak `import tensorflow` ve Merhaba Dünya örneği çalıştırın. 

    Kod toocopy:

        import tensorflow as tf
        hello = tf.constant('Hello, TensorFlow!')
        sess = tf.Session()
        print(sess.run(hello))

    Merhaba sonuç şuna benzeyecektir:
    
    ![TensorFlow kod yürütmeyi](./media/hdinsight-apache-spark-python-package-installation/execution.png "yürütme TensorFlow kodu")



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
* [Hdınsight'ta Apache Spark kümeleri Jupyter not defterlerinde ile dış paketleri kullanma](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Intellij Idea toocreate için Hdınsight araçları eklentisi kullanma ve Spark Scala uygulamaları gönderin](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Uzaktan Intellij Idea toodebug Spark uygulamaları için Hdınsight araçları eklentisi kullanma](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Jupyter bilgisayarınıza yüklemek ve tooan Hdınsight Spark kümesi bağlanın](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Kaynakları yönetme
* [Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme](hdinsight-apache-spark-resource-manager.md)
* [HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama](hdinsight-apache-spark-job-debugging.md)
