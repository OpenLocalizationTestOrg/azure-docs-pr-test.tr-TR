---
title: "yerel olarak Jupyter aaaInstall & tooan Azure Hdınsight Spark küme bağlanma | Microsoft Docs"
description: "Bilgi nasıl tooinstall Jupyter Not Defteri, bilgisayarınıza yerel olarak ve Azure hdınsight'ta Apache Spark kümesinde tooan bağlanın."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 48593bdf-4122-4f2e-a8ec-fdc009e47c16
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 95c052110b84b677fd23048597af9511365cacfc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-jupyter-notebook-on-your-computer-and-connect-tooapache-spark-on-hdinsight"></a>Jupyter not defteri bilgisayarınıza yüklemek ve tooApache hdınsight'ta Spark bağlanın

Bu makalede, bilgi nasıl tooinstall Jupyter Not Defteri, ile Merhaba (Python için) özel PySpark ve Spark Sihirli ve hello not defteri tooan Hdınsight kümesine bağlanın (Scala için) Spark çekirdekler ile. Yerel bilgisayarınızda nedeniyle tooinstall Jupyter sayısı olabilir ve bazı zorluklar de olabilir. Bunun hakkında daha fazla bilgi için hello bölümüne bakın [neden yüklediğimde Jupyter bilgisayarımda](#why-should-i-install-jupyter-on-my-computer) hello bu makalenin sonunda.

Jupyter ve hello Spark Sihirli bilgisayarınızda yükleme ilgili üç önemli adımlar vardır.

* Jupyter not defteri yükleyin
* Merhaba PySpark ve Spark çekirdekler Spark Sihirli hello ile yükleme
* Hdınsight'ta Spark Sihirli tooaccess Spark kümesi yapılandırın

Merhaba özel tekrar ve hello Spark Sihirli Hdınsight kümesi ile Jupyter not defterleri için kullanılabilir hakkında daha fazla bilgi için bkz: [Jupyter not defterlerinde kullanılabilen çekirdekler Apache Spark Linux kümeleri Hdınsight'ta](hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="prerequisites"></a>Ön koşullar
Burada listelenen hello Önkoşullar Jupyter yüklemek için değildir. Merhaba dizüstü yüklendikten sonra bağlanan hello Jupyter not defteri tooan Hdınsight kümesi için bunlar.

* Azure aboneliği. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Hdınsight'ta bir Apache Spark kümesi. Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="install-jupyter-notebook-on-your-computer"></a>Jupyter not defteri bilgisayarınıza yüklemek

Jupyter not defterleri yükleyebilmek için önce Python yüklemeniz gerekir. Python ve Jupyter kullanılabilir hello bir parçası olarak [Anaconda dağıtım](https://www.continuum.io/downloads). Anaconda yüklediğinizde, Python bir dağıtımını yükleyin. Anaconda yüklendikten sonra uygun komutlarını çalıştırarak hello Jupyter yükleme ekleyin.

1. Merhaba karşıdan [Anaconda yükleyici](https://www.continuum.io/downloads) platform ve çalışma hello kurulumu için. Çalışan hello Kurulum Sihirbazı sırasında hello seçeneği tooadd Anaconda tooyour PATH değişkeni seçtiğinizden emin olun.
2. Çalışma hello aşağıdaki tooinstall Jupyter komutu.

        conda install jupyter

    Jupyter yükleme hakkında daha fazla bilgi için bkz: [Anaconda kullanarak Jupyter yükleme](http://jupyter.readthedocs.io/en/latest/install.html).

## <a name="install-hello-kernels-and-spark-magic"></a>Merhaba tekrar ve Spark Sihirli yükleyin

Yönergeler için nasıl tooinstall hello Spark Sihirli, hello PySpark ve Spark çekirdekler hello Yükleme'ndaki yönergeleri izlediğinizden hello [sparkmagic belgelerine](https://github.com/jupyter-incubator/sparkmagic#installation) github'da. Merhaba hello Spark Sihirli belgelerinde ilk adım, tooinstall Spark Sihirli ister. Bu ilk adım hello bağlantısında komutları, bağlanacağınız hello Hdınsight kümesi hello sürümüne bağlı olarak aşağıdaki hello değiştirin. Bundan sonra hello Spark Sihirli belgelerindeki adımları kalan hello izleyin. Tooinstall hello farklı tekrar istiyorsanız hello Spark Sihirli yükleme yönergeleri bölüm 3. adım gerçekleştirmeniz gerekir.

* Yürüterek sparkmagic 0.2.3 kümeleri v3.4 için yükleyin`pip install sparkmagic==0.2.3`

* Kümeleri v3.5 ve v3.6 için sparkmagic 0.11.2 yürüterek yükleme`pip install sparkmagic==0.11.2`

## <a name="configure-spark-magic-tooconnect-toohdinsight-spark-cluster"></a>Spark Sihirli tooconnect tooHDInsight Spark kümesi yapılandırın

Bu bölümde, Azure Hdınsight'ta oluşturmuş olmalısınız önceki tooconnect tooan Apache Spark kümesi yüklü hello Spark Sihirli yapılandırın.

1. Merhaba Jupyter yapılandırma bilgileri genellikle hello kullanıcıların giriş dizininde depolanır. toolocate giriş dizininize herhangi bir platformda işletim sistemi, türü hello aşağıdaki komutları.

    Merhaba Python Kabuğu'nu başlatın. Bir komut penceresinde hello aşağıdaki komutu yazın:

        python

    Hello Python kabuğu, komut toofind hello giriş dizini çıkışı aşağıdaki hello girin.

        import os
        print(os.path.expanduser('~'))

2. Toohello giriş dizinine gidin ve adlı bir klasör oluşturun **.sparkmagic** zaten yoksa.
3. Merhaba klasör içinde adlı bir dosya oluşturun **config.json** ve JSON parçacığı içindeki aşağıdaki hello ekleyin.

        {
          "kernel_python_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          },
          "kernel_scala_credentials" : {
            "username": "{USERNAME}",
            "base64_password": "{BASE64ENCODEDPASSWORD}",
            "url": "https://{CLUSTERDNSNAME}.azurehdinsight.net/livy"
          }
        }

4. Yedek **{USERNAME}**, **{CLUSTERDNSNAME}**, ve **{BASE64ENCODEDPASSWORD}** uygun değerlere sahip. Sık kullanılan programlama dili veya çevrimiçi toogenerate bir Base64 ile kodlanmış parolayı yardımcı programları sayısı için gerçek parolanızı kullanabilirsiniz.

5. Hello sağ sinyal ayarlarında yapılandırdığınız `config.json`. Aynı düzeydeki hello hello sırasında bu ayarları eklemelisiniz `kernel_python_credentials` ve `kernel_scala_credentials` parçacıkları, eklenen önceki. Bunu nasıl ve nerede tooadd hello sinyal ayarları, bir örnek için bkz [örnek config.json](https://github.com/jupyter-incubator/sparkmagic/blob/master/sparkmagic/example_config.json).

    * İçin `sparkmagic 0.2.3` (v3.4 kümeleri) içerir:

            "should_heartbeat": true,
            "heartbeat_refresh_seconds": 5,
            "heartbeat_retry_seconds": 1

    * İçin `sparkmagic 0.11.2` (kümeleri v3.5 ve v3.6) içerir:

            "heartbeat_refresh_seconds": 5,
            "livy_server_heartbeat_timeout_seconds": 60,
            "heartbeat_retry_seconds": 1

    >[!TIP]
    >Sinyal oturumları sızdırılmaz tooensure gönderilir. Bir bilgisayar toosleep geçip geçmeyeceğini veya kapatılmış açtığınızda hello sinyal gönderilmez, oturum hello olan içinde kaynaklanan temizlendi. Kümeleri v3.4 için bu davranış toodisable istiyorsanız hello Livy config ayarlayabilirsiniz `livy.server.interactive.heartbeat.timeout` çok`0` hello Ambari UI gelen. Yukarıdaki hello 3.5 yapılandırma ayarlamazsanız kümeleri v3.5 için hello oturum silinmez.

6. Jupyter başlatın. Komut hello komut isteminden aşağıdaki hello kullanın.

        jupyter notebook

7. Merhaba Jupyter not defteri ve hello tekrar ile Merhaba Spark Sihirli kullanabileceğiniz kullanarak toohello küme bağlanabildiğini doğrulayın. Merhaba aşağıdaki adımları gerçekleştirin.

    a. Yeni bir not defteri oluşturun. Merhaba sağ köşesinden tıklatın **yeni**. Merhaba varsayılan çekirdek görmelisiniz **Python2** ve yüklediğiniz, iki yeni çekirdek hello **PySpark** ve **Spark**. Tıklatın **PySpark**.

    ![Jupyter not defterlerinde çekirdekler](./media/hdinsight-apache-spark-jupyter-notebook-install-locally/jupyter-kernels.png "Jupyter not defterlerinde çekirdekler")

    b. Aşağıdaki kod parçacığını hello çalıştırın.

        %%sql
        SELECT * FROM hivesampletable LIMIT 5

    Başarılı bir şekilde hello çıkış alabilir, bağlantı toohello Hdınsight kümenize test edilir.

    >[!TIP]
    >Tooupdate hello dizüstü bilgisayar yapılandırmasını tooconnect tooa farklı küme istiyorsanız hello config.json hello yeni değerleri kümesiyle yukarıdaki adım 3'te gösterildiği gibi güncelleştirin.

## <a name="why-should-i-install-jupyter-on-my-computer"></a>Bilgisayarımda neden Jupyter yüklediğimde?
Bir sayı olabilir, neden tooinstall Jupyter bilgisayarınızda istediğiniz, ardından bağlanmak nedeniyle tooa Spark küme Hdınsight'ta.

* Jupyter not defterleri zaten hello Azure hdınsight'ta Spark kümesi üzerinde kullanılabilir olsa bile, bilgisayarınıza Jupyter yükleme seçeneği toocreate defterlerinizi yerel olarak Merhaba, uygulamanızı çalıştıran bir kümeye karşı test etmek ve hello karşıya sağlar not defterlerini toohello küme. tooupload hello not defterlerini toohello küme ya da karşıya yüklediğiniz bunları çalıştıran hello Jupyter Not Defteri veya hello kullanarak küme veya hello kümesi ile ilişkili hello depolama hesabındaki toohello /HdiNotebooks klasörü kaydetmek. Not defterlerini hello kümede nasıl depolandığını daha fazla bilgi için bkz: [Jupyter not defterleri depolandığı](hdinsight-apache-spark-jupyter-notebook-kernels.md#where-are-the-notebooks-stored)?
* Kullanılabilir Hello dizüstü bilgisayarlarla yerel olarak uygulama gereksinimi temel alan toodifferent Spark kümeleri bağlanabilir.
* GitHub tooimplement kaynak denetim sistemi kullanabilir ve sürüm denetimi hello dizüstü bilgisayarlar için sahiptir. Ayrıca, birden çok kullanıcı çalışabilir hello ile aynı işbirliğine dayalı bir ortam olabilir dizüstü bilgisayar.
* Bir küme bile sahip olmadan dizüstü bilgisayarlar ile yerel olarak çalışabilir. Bir küme tootest defterlerinizi karşı yeterlidir, değil toomanually defterlerinizi veya geliştirme ortamında yönetebilirsiniz.
* Bu tooconfigure hello Jupyter yükleme hello kümede olandan daha kolay tooconfigure kendi yerel geliştirme ortamı olabilir.  Bir veya daha fazla uzak kümelerini yapılandırma olmadan yerel olarak yüklü tüm hello yazılım avantajından yararlanabilirsiniz.

> [!WARNING]
> Yerel bilgisayarınızda yüklü Jupyter ile birden çok kullanıcı hello çalıştırabilirsiniz aynı Spark küme hello hello aynı Not aynı anda. Böyle bir durumda, birden çok Livy oturumu oluşturulur. Bir sorunu yaşayıp çalıştırmak ve hangi Livy oturumu toowhich kullanıcının ait olduğu bir karmaşık görev tootrack olacaktır, toodebug istiyorsanız.
>
>

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
* [Intellij Idea toocreate için Hdınsight araçları eklentisi kullanma ve Spark Scala uygulamaları gönderin](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Uzaktan Intellij Idea toodebug Spark uygulamaları için Hdınsight araçları eklentisi kullanma](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [HDInsight’ta Spark kümesi ile Zeppelin not defterlerini kullanma](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight için Spark kümesinde Jupyter not defteri için kullanılabilir çekirdekler](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Jupyter not defterleri ile dış paketleri kullanma](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)

### <a name="manage-resources"></a>Kaynakları yönetme
* [Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme](hdinsight-apache-spark-resource-manager.md)
* [HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama](hdinsight-apache-spark-job-debugging.md)
