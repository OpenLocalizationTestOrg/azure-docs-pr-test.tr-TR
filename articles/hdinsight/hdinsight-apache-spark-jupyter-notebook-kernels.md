---
title: "Azure Hdınsight'ta Spark üzerinde Jupyter not defteri aaaKernels kümeleri | Microsoft Docs"
description: "Merhaba PySpark, PySpark3 ve Spark tekrar kullanılabilir Azure hdınsight'ta Spark kümeleri ile Jupyter not defteri için hakkında bilgi edinin."
keywords: "spark, jupyter spark üzerinde jupyter not defteri"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 0719e503-ee6d-41ac-b37e-3d77db8b121b
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: nitinme
ms.openlocfilehash: 560c944fe850c5753ac9fa90550b804f0c47d14c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="kernels-for-jupyter-notebook-on-spark-clusters-in-azure-hdinsight"></a>Azure hdınsight'ta Spark kümeleri Jupyter not defteri için tekrar 

Hdınsight Spark kümeleri uygulamalarınızı test etme için Spark üzerinde hello Jupyter not defteri ile kullanabileceğiniz çekirdek sağlar. Bir çekirdek çalıştıran ve kodunuzu yorumlar bir programdır. Merhaba üç tekrar şunlardır:

- **PySpark** - Python2 içinde yazılmış uygulamalar için
- **PySpark3** - Python3 içinde yazılmış uygulamalar için
- **Spark** - Scala içinde yazılmış uygulamalar için

Bu makalede, bilgi nasıl toouse Bu tekrar ve bunları kullanmanın yararları hello.

## <a name="prerequisites"></a>Ön koşullar

* Hdınsight'ta bir Apache Spark kümesi. Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="create-a-jupyter-notebook-on-spark-hdinsight"></a>Spark Hdınsight üzerinde bir Jupyter not defteri oluşturma

1. Merhaba gelen [Azure portal](https://portal.azure.com/), kümenizi açın.  Bkz: [listesi ve Göster kümeleri](hdinsight-administer-use-portal-linux.md#list-and-show-clusters) hello yönergeler için. Yeni bir portal dikey penceresinde Hello Küme açılır.

2. Merhaba gelen **hızlı bağlantılar** 'yi tıklatın **küme panolar** tooopen hello **küme panolar** dikey.  Görmüyorsanız, **hızlı bağlantılar**, tıklatın **genel bakış** hello dikey penceresinde hello sol menüden.

    ![Jupyter not defteri Spark üzerinde](./media/hdinsight-apache-spark-jupyter-notebook-kernels/hdinsight-jupyter-notebook-on-spark.png "Spark üzerinde Jupyter not defteri") 

3. Tıklatın **Jupyter not defteri**. İstenirse, hello küme için hello yönetici kimlik bilgilerini girin.
   
   > [!NOTE]
   > Merhaba Jupyter not defteri açma hello tarayıcınızda URL aşağıdaki tarafından Spark kümesinde de ulaşabilir. Değiştir **CLUSTERNAME** kümenizi hello adı:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 

3. Tıklatın **yeni**ve ardından ya da **Pyspark**, **PySpark3**, veya **Spark** toocreate bir not defteri. Merhaba Spark çekirdek Scala uygulamaları için PySpark çekirdeği Python2 uygulamaları için ve PySpark3 çekirdek Python3 uygulamalar için kullanın.
   
    ![Spark üzerinde Jupyter not defteri için tekrar](./media/hdinsight-apache-spark-jupyter-notebook-kernels/kernel-jupyter-notebook-on-spark.png "için Spark Jupyter not defterlerinde çekirdekler") 

4. Bir not defteri seçtiğiniz hello çekirdek ile açılır.

## <a name="benefits-of-using-hello-kernels"></a>Merhaba tekrar kullanmanın yararları

Spark Hdınsight kümeleri Jupyter not defteri ile Merhaba yeni tekrar kullanmanın bazı avantajları şunlardır.

- **Bağlamları önceden**. İle **PySpark**, **PySpark3**, veya hello **Spark** çekirdekleri gerektirmeyen tooset hello Spark veya Hive bağlamları açıkça, uygulamalarla çalışmaya başlamadan önce. Bu, varsayılan olarak kullanılabilir. Bu içerikler şunlardır:
   
   * **sc** - Spark bağlamı için
   * **sqlContext** - Hive bağlamı için

    Bu nedenle, hello tooset hello bağlamları aşağıdaki gibi toorun deyimlere yok:

        SC SparkContext('yarn-client') sqlContext = HiveContext(sc) =

    Bunun yerine, doğrudan kullanabileceğiniz hello uygulamanızı bağlamlarda hazır.

- **Hücre sihirleri**. Merhaba PySpark çekirdeği bazı önceden tanımlanmış "sihirleri" ile çağırabilir özel komutlar olduğu sağlar `%%` (örneğin, `%%MAGIC` <args>). Merhaba Sihirli komutu hello birinci kod hücresini Word'de ve içeriği için birden çok satır izin gerekir. Merhaba Sihirli word hello ilk hello hücre Word'de olmalıdır. Merhaba Sihirli, hatta açıklamaları önce herhangi bir şey ekleme bir hataya neden olur.     Sihirler hakkında daha fazla bilgi için bkz: [burada](http://ipython.readthedocs.org/en/stable/interactive/magics.html).
   
    Merhaba aşağıdaki tabloda farklı sihirler hello hello tekrar kullanılabilir listeler.

   | Özel numarası | Örnek | Açıklama |
   | --- | --- | --- |
   | Yardım |`%%help` |Örnek ve açıklama ile tüm hello kullanılabilir sihirler oluşan bir tablo oluşturur |
   | bilgileri |`%%info` |Çıkış oturum bilgilerini hello geçerli Livy uç noktası |
   | Yapılandırma |`%%configure -f`<br>`{"executorMemory": "1000M"`,<br>`"executorCores": 4`} |Oturum oluşturmak için hello parametreler yapılandırır. Force bayrağını hello (-f) bir oturum zaten oluşturulmuşsa, bu hello oturum sağlar bırakılan ve yeniden zorunludur. Bakmak [Livy'nın POST /sessions iste gövde](https://github.com/cloudera/livy#request-body) için geçerli parametrelerin bir listesi. Parametreleri JSON dizesi olarak geçirilmesi gerekir ve hello sonraki satırda hello örnek sütununda gösterildiği gibi hello Sihirli sonra olmalıdır. |
   | SQL |`%%sql -o <variable name>`<br> `SHOW TABLES` |Merhaba sqlContext bir Hive sorgusu yürütür. Merhaba, `-o` parametresi geçirilir, hello hello sorgunun sonucu hello kalıcı %% yerel Python bağlamı olarak bir [Pandas](http://pandas.pydata.org/) dataframe. |
   | Yerel |`%%local`<br>`a=1` |Sonraki satırların tüm hello kodda yerel olarak yürütülür. Kodu dahi, kullanmakta olduğunuz hello çekirdek yedeklemiş geçerli Python2 kodu olmalıdır. Bu nedenle, seçtiğiniz olsa bile **PySpark3** veya **Spark** hello kullanırsanız hello Not Defteri, oluşturma sırasında tekrar `%%local` Sihirli bir hücreye, o hücre yalnızca geçerli Python2 kodu olmalıdır... |
   | günlükler |`%%logs` |Çıktı hello geçerli Livy oturumu için günlükleri hello. |
   | Sil |`%%delete -f -s <session number>` |Belirli bir oturum hello geçerli Livy uç noktasının siler. Başlatılan hello oturumu hello çekirdek kendisi için silemezsiniz unutmayın. |
   | Temizleme |`%%cleanup -f` |Bu not defterinin oturum dahil olmak üzere hello geçerli Livy uç noktası için tüm hello oturumları siler. Merhaba force bayrağını -f zorunludur. |

   > [!NOTE]
   > Ayrıca toohello sihirler eklenen hello PySpark çekirdeği tarafından hello da kullanabilirsiniz [yerleşik IPython sihirler](https://ipython.org/ipython-doc/3/interactive/magics.html#cell-magics)gibi `%%sh`. Merhaba kullanabilirsiniz `%%sh` Sihirli toorun komut dosyaları ve hello küme headnode üzerinde kod bloğu.
   >
   >
2. **Otomatik görselleştirme**. Merhaba **Pyspark** çekirdek otomatik olarak Hive ve SQL sorguları hello çıktısını visualizes. Tablo, pasta, satır, alan, çubuk dahil olmak üzere görselleştirmeleri birkaç farklı türde arasında seçim yapabilirsiniz.

## <a name="parameters-supported-with-hello-sql-magic"></a>Merhaba ile desteklenen parametreler %% sql Sihirli
Merhaba `%%sql` Sihirli toocontrol hello sorguları çalıştırdığınızda, aldığınız çıkış tür kullanabileceğiniz farklı parametreleri destekler. Aşağıdaki tablonun hello hello çıkış listeler.

| Parametre | Örnek | Açıklama |
| --- | --- | --- |
| -o |`-o <VARIABLE NAME>` |Merhaba sorgu, bu parametre toopersist hello sonucunu hello kullanmak %% yerel Python bağlamı olarak bir [Pandas](http://pandas.pydata.org/) dataframe. Hello hello dataframe değişkenin adını, belirttiğiniz hello değişken adıdır. |
| -q |`-q` |Bu tooturn görselleştirmeleri kapalı hello hücre için kullanın. Tooauto istemiyorsanız-bir hücre Merhaba içeriğine görselleştirmek ve yalnızca toocapture istediğiniz bir dataframe olarak daha sonra kullanmak `-q -o <VARIABLE>`. Merhaba sonuçları yakalama olmadan tooturn görselleştirmeleri kapatmak istiyorsanız (örneğin, bir SQL sorgusu gibi çalıştırmak için bir `CREATE TABLE` deyimi), kullanın `-q` belirtmeden bir `-o` bağımsız değişkeni. |
| -m |`-m <METHOD>` |Burada **yöntemi** ya **ele** veya **örnek** (varsayılan değer **ele**). Merhaba yöntemi ise **ele**, hello çekirdek MAXROWS (daha sonra bu tabloda açıklanan) tarafından belirtilen hello sonuç veri kümesinin hello üst öğeden seçer. Merhaba yöntemi ise **örnek**, hello çekirdek rastgele örnekler hello veri çok göre kümenin öğeleri`-r` sonraki bu tabloda açıklanan parametresi. |
| -r |`-r <FRACTION>` |Burada **KESİR** 0,0 ile 1,0 arasında bir kayan noktalı sayı. Merhaba SQL sorgusu Hello örnek yöntemi olarak ayarlanmışsa `sample`, sonra da hello çekirdek rastgele hello belirtilen kesir için ayarladığınız hello sonuç hello öğelerinin örnekleri. Örneğin, bir SQL sorgusu hello bağımsız değişkenlerle çalıştırırsanız `-m sample -r 0.01`, %1 hello sonuç satır rastgele örneklenen sonra. |
| -n |`-n <MAXROWS>` |**MAXROWS** bir tamsayı değil. Merhaba çekirdek sınırlar hello çıkış satır sayısı çok**MAXROWS**. Varsa **MAXROWS** negatif bir sayı olduğu gibi **-1**, hello hello sonuç kümesi satır sayısı sınırlı değildir. |

**Örnek:**

    %%sql -q -m sample -r 0.1 -n 500 -o query2
    SELECT * FROM hivesampletable

Yukarıdaki Hello ifade aşağıdaki hello:

* Tüm kayıtları seçer **hivesampletable**.
* -Q, kullandığımız için otomatik görselleştirme devre dışı bırakır.
* Biz kullandığından `-m sample -r 0.1 -n 500` % 10'hello hivesampletable hello satır rastgele örnekler ve sınırları hello hello sonuç kümesi too500 satır boyutu.
* Son olarak, biz kullanıldığından `-o query2` de adlı bir dataframe hello çıkış kaydeder **sorgu2**.

## <a name="considerations-while-using-hello-new-kernels"></a>Merhaba yeni tekrar kullanırken dikkat edilecek noktalar

Kullanın, hangi çekirdek çalıştıran hello not defterlerini bırakarak hello küme kaynaklarını kullanır.  Bu çekirdekleri hello bağlamları hazır olduğundan, yalnızca hello not defterlerini çıkma hello bağlam KILL değil ve bu nedenle hello küme kaynaklarını toobe kullanımda devam. Toouse hello iyi bir uygulamadır **Kapat ve Durdur** hello not defterinin seçeneğinden **dosya** hello bağlam sonlandırır hello Not Defteri kullanarak tamamlanmış ve sonra not defteri çıkar hello menüsü.     

## <a name="show-me-some-examples"></a>Bazı örnekler Göster

Jupyter not defteri açtığınızda, iki klasör kullanılabilir hello kök düzeyinde görürsünüz.

* Merhaba **PySpark** klasörü bulunan örnek not defterlerini bu kullanım hello yeni **Python** çekirdek.
* Merhaba **Scala** klasörü bulunan örnek not defterlerini bu kullanım hello yeni **Spark** çekirdek.

Merhaba açabilirsiniz **00 - [okuma önce BENİ] Spark Sihirli çekirdek Özellikler** hello dizüstü bilgisayarınızı **PySpark** veya **Spark** klasörü toolearn hakkında hello farklı sihirler kullanılabilir. Aynı zamanda diğer örnek not defterlerini hello iki klasörleri toolearn altında kullanılabilir nasıl hello tooachieve farklı senaryolar Hdınsight Spark kümeleri ile Jupyter not defterlerini kullanarak.

## <a name="where-are-hello-notebooks-stored"></a>Merhaba not defterlerini depolandığı?

Jupyter not defterleri hello altında hello kümeyle ilişkili toohello depolama hesabı kaydedilir **/HdiNotebooks** klasör.  Dizüstü bilgisayarlar, metin dosyaları ve Jupyter içinde oluşturduğunuz klasörler hello depolama hesabından erişilebilir.  Jupyter toocreate bir klasörü kullanırsanız, örneğin, **Klasörüm'ün** ve dizüstü **myfolder/mynotebook.ipynb**, o not defteri konumunda erişebilirsiniz `/HdiNotebooks/myfolder/mynotebook.ipynb` hello depolama hesabındaki.  Merhaba ters de true, diğer bir deyişle, tooyour depolama hesabı doğrudan bir not defteri yüklerseniz `/HdiNotebooks/mynotebook1.ipynb`, hello dizüstü görülebilir Jupyter de.  Hatta hello kümesi silindikten sonra not defterlerini hello depolama hesabında kalır.

not defterlerini toohello depolama hesabı kaydedilir hello ile HDFS uyumlu yoludur. Bunu, SSH kullanabilirsiniz hello kümesine yönetimi komutları hello aşağıdaki kod parçacığında gösterildiği gibi dosyası varsa:

    hdfs dfs -ls /HdiNotebooks                               # List everything at hello root directory – everything in this directory is visible tooJupyter from hello home page
    hdfs dfs –copyToLocal /HdiNotebooks                    # Download hello contents of hello HdiNotebooks folder
    hdfs dfs –copyFromLocal example.ipynb /HdiNotebooks   # Upload a notebook example.ipynb toohello root folder so it’s visible from Jupyter


Durumunda hello hello küme için depolama hesabı erişim sorunları, hello not defterlerini hello headnode üzerinde de kaydedilir `/var/lib/jupyter`.

## <a name="supported-browser"></a>Desteklenen tarayıcı

Spark Hdınsight kümeleri Jupyter not defterlerini yalnızca Google Chrome üzerinde desteklenir.

## <a name="feedback"></a>Geri Bildirim
Hello yeni tekrar aşama gelişen olan ve zaman içinde yetişkin. Bu aynı zamanda bu tekrar yetişkin olarak API'leri değişebilir anlamına gelebilir. Bu yeni tekrar kullanırken sahip herhangi bir geri bildirim veriyoruz. Bu, bu tekrar son sürümünü hello şekillendirmeye yararlıdır. Yorumlar/geribildirim hello altında bırakabilirsiniz **açıklamaları** bu makalenin hello alt kısmına.

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
* [Jupyter not defterleri ile dış paketleri kullanma](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter bilgisayarınıza yüklemek ve tooan Hdınsight Spark kümesi bağlanın](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Kaynakları yönetme
* [Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme](hdinsight-apache-spark-resource-manager.md)
* [HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama](hdinsight-apache-spark-job-debugging.md)
