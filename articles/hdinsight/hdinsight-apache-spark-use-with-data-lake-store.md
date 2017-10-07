---
title: Azure Data Lake Store'da Apache Spark tooanalyze veri aaaUse | Microsoft Docs
description: "Azure Data Lake Store'da depolanan tooanalyze verileri Spark işleri çalıştırma"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 1f174323-c17b-428c-903d-04f0e272784c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 3b7f628f7a8114d2ca6f3f9219ce107905f1c818
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hdinsight-spark-cluster-tooanalyze-data-in-data-lake-store"></a>Hdınsight Spark küme tooanalyze verileri Data Lake Store içinde kullanma

Bu öğreticide, Hdınsight Spark kümeleri toorun bir Data Lake Store hesabından veri okuyan bir iş ile Jupyter not defteri kullanılabilir kullanın.

## <a name="prerequisites"></a>Ön koşullar

* Azure Data Lake Store hesabı. Merhaba yönergeleri izleyin [Azure Data Lake hello Azure Portal kullanarak Store ile çalışmaya başlama](../data-lake-store/data-lake-store-get-started-portal.md).

* Azure Hdınsight Spark, depolama alanı olarak Data Lake Store ile küme. Merhaba yönergeleri izleyin [Azure Portal'ı kullanarak Data Lake Store ile bir Hdınsight kümesi oluşturmayı](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

    
## <a name="prepare-hello-data"></a>Merhaba verileri hazırlama

> [!NOTE]
> Varsayılan depolama olarak Data Lake Store ile Merhaba Hdınsight küme oluşturduysanız bu adımı tooperform gerekmez. Merhaba küme oluşturma işlemlerini hello küme oluştururken belirttiğiniz hello Data Lake Store hesabındaki bazı örnek veri ekler. Atla toohello bölüm [Data Lake Store ile kullanımı Hdınsight Spark kümesi](#use-an-hdinsight-spark-cluster-with-data-lake-store).
>
>

Ek depolama alanı ve varsayılan depolama alanı olarak Azure Storage Blobuna olarak Data Lake Store ile Hdınsight kümesi oluşturduysanız, bazı örnek veri toohello Data Lake Store hesabı kopyalamanız gerekir. Azure Storage Blobuna hello Hdınsight kümesi ile ilişkili hello hello örnek verileri kullanabilirsiniz. Merhaba kullanabilirsiniz [ADLCopy aracı](http://aka.ms/downloadadlcopy) toodo şekilde. Karşıdan yükle ve hello aracı hello bağlantıdan yükleyin.

1. Bir komut istemi açın ve AdlCopy yüklü olduğu, genellikle toohello dizinine gidin `%HOMEPATH%\Documents\adlcopy`.

2. Komut toocopy aşağıdaki hello hello kaynak kapsayıcı tooa Data Lake Store belirli bir blobu çalıştırın:

        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>

    Kopya hello **HVAC.csv** örnek veri dosyası konumunda **/HdiSamples/HdiSamples/SensorSampleData/hvac/** toohello Azure Data Lake Store hesabı. Merhaba kod parçacığını gibi görünmelidir:

        AdlCopy /Source https://mydatastore.blob.core.windows.net/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv /dest swebhdfs://mydatalakestore.azuredatalakestore.net/hvac/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

   > [!WARNING]
   > Dosya hello ve yol adları hello uygun durumda olduğundan emin olun.
   >
   >
3. Merhaba kimlik bilgileri istendiğinde tooenter olacaktır Azure aboneliğinizin Data Lake Store hesabınızın altında elinizde hello. Bir çıkış benzer toohello aşağıdaki görürsünüz:

        Initializing Copy.
        Copy Started.
        100% data copied.
        Copy Completed. 1 file copied.

    Merhaba veri dosyası (**HVAC.csv**) altında bir klasöre kopyalanacak **/hvac** hello Data Lake Store hesabı içinde.

## <a name="use-an-hdinsight-spark-cluster-with-data-lake-store"></a>Hdınsight Spark kümesinde Data Lake Store ile kullanma

1. Merhaba gelen [Azure Portal](https://portal.azure.com/), (, onu toohello Sabitle) hello Panosu'ndan hello kutucuğuna Spark kümenizin tıklayın. Tooyour küme altında da gidebilirsiniz **tümüne Gözat** > **Hdınsight kümeleri**.

2. Merhaba Spark kümesi dikey penceresinden tıklatın **hızlı bağlantılar**ve sonra hello **küme Panosu** dikey penceresinde tıklatın **Jupyter not defteri**. İstenirse, hello küme için hello yönetici kimlik bilgilerini girin.

   > [!NOTE]
   > Kümenizin açma hello tarayıcınızda URL aşağıdaki tarafından hello Jupyter Not Defteri de ulaşabilir. Değiştir **CLUSTERNAME** kümenizi hello adı:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. Yeni bir not defteri oluşturun. **Yeni** ve ardından **PySpark** seçeneğine tıklayın.

    ![Yeni bir Jupyter not defteri oluşturma](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-create-jupyter-notebook.png "Yeni bir Jupyter not defteri oluşturma")

4. Merhaba PySpark çekirdeği kullanarak bir not defteri oluşturduğunuz için siz toocreate bir bağlam açıkça gerekmez. Merhaba birinci kod hücresini çalıştırdığınızda Spark ve Hive bağlamları hello otomatik olarak sizin için oluşturulur. Bu senaryo için gerekli hello türleri içeri aktararak işleme başlayabilirsiniz. toodo, bu nedenle, aşağıdaki kod parçacığını bir hücreye ve tuşuna hello yapıştırın **SHIFT + ENTER**.

        from pyspark.sql.types import *

    Jupyter'de bir işi çalıştırma her zaman, web tarayıcınızın Pencere başlığında gösterecektir bir **(meşgul)** hello not defteri başlığı ile birlikte durum. Ayrıca bir daire sonraki toohello görürsünüz **PySpark** hello sağ üst köşedeki metin. Merhaba iş tamamlandıktan sonra bu tooa boş daire değiştirir.

     ![Jupyter not defteri işinin durumu](./media/hdinsight-apache-spark-use-with-data-lake-store/hdinsight-jupyter-job-status.png "Jupyter not defteri işinin durumu")

5. Hello kullanarak geçici bir tabloya örnek verileri yükleme **HVAC.csv** toohello Data Lake Store hesabı kopyaladığınız dosya. URL deseni takip hello kullanarak hello Data Lake Store hesabındaki hello verilere erişebilir.

    * Data Lake Store varsayılan depolama varsa, HVAC.csv URL aşağıdaki hello yolu benzer toohello olacaktır:

            adl://<data_lake_store_name>.azuredatalakestore.net/<cluster_root>/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

        Ya da kısaltılmış bir biçimi hello aşağıdaki gibi kullanabilirsiniz:

            adl:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv

    * Data Lake Store ek depolama alanı olarak varsa, HVAC.csv, gibi kopyaladığınız hello konumda olacaktır:

            adl://<data_lake_store_name>.azuredatalakestore.net/<path_to_file>

     Boş bir hücre, aşağıdaki kod örneğine Yapıştır hello yerine **MYDATALAKESTORE** Data Lake Store hesap adı ve basın **SHIFT + ENTER**. Bu kod örneği hello veri adlı geçici bir tabloya kaydeder **hvac**.

            # Load hello data. hello path below assumes Data Lake Store is default storage for hello Spark cluster
            hvacText = sc.textFile("adl://MYDATALAKESTORE.azuredatalakestore.net/cluster/mysparkcluster/HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            # Create hello schema
            hvacSchema = StructType([StructField("date", StringType(), False),StructField("time", StringType(), False),StructField("targettemp", IntegerType(), False),StructField("actualtemp", IntegerType(), False),StructField("buildingID", StringType(), False)])

            # Parse hello data in hvacText
            hvac = hvacText.map(lambda s: s.split(",")).filter(lambda s: s[0] != "Date").map(lambda s:(str(s[0]), str(s[1]), int(s[2]), int(s[3]), str(s[6]) ))

            # Create a data frame
            hvacdf = sqlContext.createDataFrame(hvac,hvacSchema)

            # Register hello data fram as a table toorun queries against
            hvacdf.registerTempTable("hvac")

6. Bir PySpark çekirdeği kullandığınız için artık doğrudan bir SQL sorgusu hello geçici tablosunda çalıştırabilirsiniz **hvac** hello kullanarak yeni oluşturduğunuz `%%sql` Sihirli. Merhaba hakkında daha fazla bilgi için `%%sql` hello PySpark çekirdeği kullanılabilen diğer sihirler yanı sıra Sihirli bkz [Spark Hdınsight kümeleri ile Jupyter not defterlerinde kullanılabilen çekirdekler](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

7. Merhaba iş başarıyla tamamlandığında, tablo çıktısı aşağıdaki hello varsayılan olarak görüntülenir.

      ![Sorgu sonucunun tablo çıktısı](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-tabular-output.png "Sorgu sonucunun tablo çıktısı")

     Ayrıca hello sonuçları diğer görselleştirmelerde de görebilirsiniz. Örneğin, bir alan grafiği için hello aynı çıktı hello şu şekilde görünür.

     ![Sorgu sonucunun alan grafiği](./media/hdinsight-apache-spark-use-with-data-lake-store/jupyter-area-output.png "Sorgu sonucunun alan grafiği")

8. Merhaba uygulaması çalıştıran bitirdikten sonra kapatma hello not defteri toorelease hello kaynakları gerekir. toodo çok hello **dosya** hello dizüstü menüsünde **Kapat ve Durdur**. Bu işlem kapatma ve Kapat hello dizüstü.


## <a name="next-steps"></a>Sonraki adımlar

* [Apache Spark kümesinde bir tek başına Scala uygulama toorun oluşturun](hdinsight-apache-spark-create-standalone-application.md)
* [Hdınsight araçları, Hdınsight Spark Linux kümesi için Intellij toocreate Spark uygulamaları için Azure araç setindeki kullanın.](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Hdınsight araçları, Hdınsight Spark Linux kümesi için Eclipse toocreate Spark uygulamaları için Azure araç setindeki kullanın.](hdinsight-apache-spark-eclipse-tool-plugin.md)
