---
title: "Azure Hdınsight'ta Apache Spark aaaUse Zeppelin not defterlerini küme | Microsoft Docs"
description: "Azure Hdınsight'ta Apache Spark toouse Zeppelin not defterlerini kümeleri nasıl ilişkin adım adım yönergeler için."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: df489d70-7788-4efa-a089-e5e5006421e2
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 3ab479cfccc7fd38a9bf6a9fb4f5928beec8ff7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-zeppelin-notebooks-with-apache-spark-cluster-on-azure-hdinsight"></a>Azure hdınsight'ta Apache Spark kümesinde ile Zeppelin not defterlerini kullanma

Hdınsight Spark kümeleri toorun Spark işlerinin kullanabileceğiniz Zeppelin not defterlerini içerir. Bu makalede, nasıl toouse hello Zeppelin Not Hdınsight kümesinde öğrenin.

> [!NOTE]
> Zeppelin not defterlerini yalnızca 1.6.3 Spark Hdınsight 3.5 ve 2.1.0 Spark Hdınsight 3.6 için kullanılabilir.
>

**Ön koşullar:**

* Azure aboneliği. Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Hdınsight'ta bir Apache Spark kümesi. Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="launch-a-zeppelin-notebook"></a>Bir Zeppelin not defteri Başlat
1. Merhaba Spark kümesi dikey penceresinden tıklatın **küme Panosu**ve ardından **Zeppelin not defteri**. İstenirse, hello küme için hello yönetici kimlik bilgilerini girin.
   
   > [!NOTE]
   > Kümenizin açma hello tarayıcınızda URL aşağıdaki tarafından hello Zeppelin Not Defteri de ulaşabilir. Değiştir **CLUSTERNAME** kümenizi hello adı:
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/zeppelin`
   > 
   > 
2. Yeni bir not defteri oluşturun. Merhaba üstbilgi Bölmesi'nden tıklatın **not defteri**ve ardından **oluşturma Yeni Not**.
   
    ![Yeni bir Zeppelin not defteri oluşturma](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "yeni bir Zeppelin not defteri oluşturma")
   
    Merhaba dizüstü bilgisayar için bir ad girin ve ardından **oluşturma Not**.
3. Ayrıca, bağlı bir durum hello Not Defteri Başlığı gösterdiğinden emin olun. Merhaba sağ üst köşedeki yeşil bir nokta olarak belirtilir.
   
    ![Zeppelin not defteri durumu](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin not defteri durumu")
4. Örnek verilerini geçici bir tabloya yükleyin. Merhaba örnek veri dosyası, Hdınsight'ta Spark kümesi oluşturduğunuzda, **hvac.csv**, kopyalanan toohello ilişkili depolama hesabı altında **\HdiSamples\SensorSampleData\hvac**.
   
    Varsayılan olarak hello yeni not defterinde oluşturulan hello boş paragrafta, aşağıdaki kod parçacığında hello yapıştırın.
   
        %livy.spark
        //hello above magic instructs Zeppelin toouse hello Livy Scala interpreter
   
        // Create an RDD using hello default Spark context, sc
        val hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
        // Define a schema
        case class Hvac(date: String, time: String, targettemp: Integer, actualtemp: Integer, buildingID: String)
   
        // Map hello values in hello .csv file toohello schema
        val hvac = hvacText.map(s => s.split(",")).filter(s => s(0) != "Date").map(
            s => Hvac(s(0), 
                    s(1),
                    s(2).toInt,
                    s(3).toInt,
                    s(6)
            )
        ).toDF()
   
        // Register as a temporary table called "hvac"
        hvac.registerTempTable("hvac")
   
    Tuşuna **SHIFT + ENTER** veya hello tıklatın **yürütmek** hello paragraf toorun hello parçacığı düğmesi. Merhaba paragrafın hello sağ köşesindeki Hello durumu hazır, BEKLİYOR, çalışan tooFINISHED gelen ilerleme. Hello çıktısı görüntülenir hello hello altındaki aynı paragraf. Merhaba ekran hello aşağıdaki gibi görünür:
   
    ![Ham verileri geçici bir tablo oluşturma](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "ham verilerden geçici bir tablo oluştur")
   
    Başlık tooeach paragrafı sağlar. Merhaba sağ köşesinden hello tıklatın **ayarları** simgesine ve ardından **Göster başlık**.
5. Artık hello üzerinde Spark SQL deyimlerini çalıştırabileceğiniz **hvac** tablo. Yeni bir paragraf sorguda aşağıdaki hello yapıştırın. Merhaba sorgu hello bina kimliği ve hello birbirinden hello hedef ve her belirli bir tarihte oluşturmaya yönelik gerçek etme alır. Tuşuna **SHIFT + ENTER**.
   
        %sql
        select buildingID, (targettemp - actualtemp) as temp_diff, date from hvac where date = "6/1/13" 
   
    Merhaba **% sql** deyimi hello başında hello not defteri toouse hello Livy Scala yorumlayıcı söyler.
   
    Merhaba aşağıdaki ekran görüntüsünde hello çıktısını gösterir.
   
    ![Merhaba Not Defteri kullanarak Spark SQL deyimini çalıştırın](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "hello Not Defteri kullanarak Spark SQL deyimini çalıştırın")
   
     Merhaba görüntüleme seçenekleri (vurgulanmış dikdörtgen) tooswitch hello için farklı sunumu arasında tıklatın aynı çıktı. Tıklatın **ayarları** toochoose anahtarı ve değerleri hello çıktısında ne consitutes hello. Merhaba ekran yakalama kullanımlar yukarıda **buildingID** hello anahtar ve hello ortalama olarak **temp_diff** hello değeri olarak.
6. Merhaba sorguda değişkenler kullanarak Spark SQL deyimlerini de çalıştırabilirsiniz. Merhaba sonraki kod parçacığında gösterildiği nasıl toodefine bir değişken **Temp**, hello olası değerler ile Merhaba sorgusunda ile tooquery istiyor. Hello sorgu ilk kez çalıştırdığınızda, bir açılan hello değişkeni için belirtilen hello değerlerle otomatik olarak doldurulur.
   
        %sql
        select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff from hvac where targettemp > "${Temp = 65,65|75|85}" 
   
    Yeni bir paragraf ve tuşuna bu parçacığını yapıştırın **SHIFT + ENTER**. Merhaba aşağıdaki ekran görüntüsünde hello çıktısını gösterir.
   
    ![Merhaba Not Defteri kullanarak Spark SQL deyimini çalıştırın](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "hello Not Defteri kullanarak Spark SQL deyimini çalıştırın")
   
    Sonraki sorgular için yeni bir değer hello açılan listeden seçin ve hello sorguyu yeniden çalıştırın. Tıklatın **ayarları** toochoose anahtarı ve değerleri hello çıktısında ne consitutes hello. Merhaba ekran yakalama kullanımlar yukarıda **buildingID** başlangıç anahtarı olarak ortalama hello **temp_diff** hello değeri olarak ve **targettemp** hello grubu olarak.
7. Merhaba Livy yorumlayıcı tooexit hello uygulamayı yeniden başlatın. toodo, bu nedenle, kullanıcı adı hello sağ üst köşesinden oturum hello tıklayarak yorumlayıcı ayarlarını açın ve ardından **yorumlayıcı**.
   
    ![Yorumlayıcı başlatma](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive çıktı")
8. TooLivy yorumlayıcı Ayarları'e gidin ve ardından **yeniden**.
   
    ![Merhaba Livy intepreter yeniden](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "hello Zeppelin intepreter yeniden başlatın")

## <a name="how-do-i-use-external-packages-with-hello-notebook"></a>Dış paketler hello not defteri ile nasıl kullanabilirim?
Merhaba Zeppelin not defteri dahil out-of--box hello kümede olmayan Hdınsight (Linux) toouse dış, topluluk katkıda bulunan paketler Apache Spark kümesinde yapılandırabilirsiniz. Merhaba arayabilirsiniz [Maven depo](http://search.maven.org/) hello tam kullanılabilir paketler listesi. Ayrıca, diğer kaynaklardan kullanılabilir paketlerin listesini alabilirsiniz. Örneğin, tamamını topluluk katkıda bulunan paketlerin listesini adresten edinilebilir [Spark paketleri](http://spark-packages.org/).

Bu makalede, göreceğiniz nasıl toouse hello [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) hello Jupyter not defteri paketiyle.

1. Yorumlayıcı Ayarları'nı açın. Merhaba sağ üst köşesinden kullanıcı adı oturum hello tıklayın ve ardından **yorumlayıcı**.
   
    ![Yorumlayıcı başlatma](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive çıktı")
2. TooLivy yorumlayıcı Ayarları'e gidin ve ardından **Düzenle**.
   
    ![Yorumlayıcı ayarları değiştirme](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "yorumlayıcı ayarlarını değiştir")
3. Yeni bir anahtar ekleyin adlı **livy.spark.jars.packages** ve hello biçiminde değerini ayarlama `group:id:version`. Bunu, toouse hello istiyorsanız [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) paketi değerine ayarlamanız gerekir hello hello anahtarının çok`com.databricks:spark-csv_2.10:1.4.0`.
   
    ![Yorumlayıcı ayarları değiştirme](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "yorumlayıcı ayarlarını değiştir")
   
    Tıklatın **kaydetmek** ve hello Livy yorumlayıcı yeniden başlatın.
4. **İpucu**: toounderstand nasıl tooarrive hello anahtarının hello değerde girilen burada yukarıdaki 's isteyip istemediğinizi nasıl.
   
    a. Merhaba paketi hello Maven depo bulun. Bu öğretici için kullandık [spark csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).
   
    b. Merhaba depodan hello değerlerini toplamak **GroupID**, **Artifactıd**, ve **sürüm**.
   
    ![Jupyter not defteri ile dış paketleri kullanma](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "Jupyter not defteri ile dış paketleri kullanma")
   
    c. Merhaba üç değerleri, virgülle ayrılmış birleştirme (**:**).
   
        com.databricks:spark-csv_2.10:1.4.0

## <a name="where-are-hello-zeppelin-notebooks-saved"></a>Merhaba kaydedilmiş Zeppelin not defterlerini nerede?
Merhaba Zeppelin not defterlerini toohello küme headnodes kaydedilir. Bu nedenle, hello kümeyi silmeniz halinde hello not defterlerini de silinir. Toopreserve defterlerinizi diğer kümelerinde daha sonra kullanmak isterseniz, hello işleri çalıştırma bitirdikten sonra vermeniz gerekir. tooexport bir not defteri tıklatın hello **verme** hello resimde gösterildiği gibi simgesi.

![Not Defteri karşıdan](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "indirme hello not defteri")

Bu işlem hello dizüstü yükleme konumunuzu bir JSON dosyası olarak kaydeder.

## <a name="livy-session-management"></a>Livy oturum yönetimi
Merhaba ilk kod paragraf Zeppelin not defterinde çalıştırdığınızda, yeni bir Livy oturum Hdınsight Spark kümenizin oluşturulur. Bu oturumda daha sonra oluşturduğunuz tüm Zeppelin not defterlerini arasında paylaşılır. Bazı neden hello örneğin oturum Livy sonlandırıldı (küme yeniden başlatma, vb.), hello Zeppelin not defteri mümkün toorun işlerden olmaz.

Böyle bir durumda hello Zeppelin not defteri çalışan işler başlamadan önce aşağıdaki adımları gerçekleştirmeniz gerekir. 

1. Merhaba Livy yorumlayıcı hello Zeppelin not defteri gelen yeniden başlatın. toodo, bu nedenle, kullanıcı adı hello sağ üst köşesinden oturum hello tıklayarak yorumlayıcı ayarlarını açın ve ardından **yorumlayıcı**.
   
    ![Yorumlayıcı başlatma](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive çıktı")
2. TooLivy yorumlayıcı Ayarları'e gidin ve ardından **yeniden**.
   
    ![Merhaba Livy intepreter yeniden](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "hello Zeppelin intepreter yeniden başlatın")
3. Kod hücresini varolan bir Zeppelin not defterini ' çalıştırın. Bu yeni bir Livy oturum hello Hdınsight kümesi oluşturur.

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







