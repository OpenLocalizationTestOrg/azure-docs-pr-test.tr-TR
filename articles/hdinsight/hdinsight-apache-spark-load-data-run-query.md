---
title: "bir Azure Hdınsight Spark kümesinde aaaRun etkileşimli sorgular | Microsoft Docs"
description: "Hdınsight'ta bir Apache Spark toocreate küme nasıl üzerinde Hdınsight Spark hızlı başlangıç."
keywords: "spark hızlı başlangıç,etkileşimli spark,etkileşimli sorgu,hdinsight spark,azure spark"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 3864eba50eb3828a9ecb657ded88080e1974585f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-interactive-queries-on-an-hdinsight-spark-cluster"></a>Bir Hdınsight Spark kümesinde etkileşimli sorgular gerçekleştirme

Bu makalede, bir Jupyter not defteri toorun etkileşimli Spark SQL sorguları bir Spark kümesi kullanın. Jupyter not defteri hello konsol tabanlı etkileşimli deneyiminin toohello Web genişleten bir tarayıcı tabanlı bir uygulamadır. Daha fazla bilgi için bkz: [hello Jupyter not defteri](http://jupyter-notebook.readthedocs.io/en/latest/notebook.html).

Bu öğretici için kullandığınız hello **PySpark** Çekirdeği'nde hello Jupyter not defteri toorun etkileşimli Spark SQL sorgusu. Hdınsight kümeleri Jupyter not defterlerini destekleyen da iki diğer çekirdek - **PySpark3** ve **Spark**. Hello tekrar ve hello kullanmanın avantajları hakkında daha fazla bilgi için **PySpark**, bkz: [Hdınsight'ta Apache Spark kullanım Jupyter not defterlerinde çekirdekler kümeleri](hdinsight-apache-spark-jupyter-notebook-kernels.md).

## <a name="prerequisites"></a>Ön koşullar

* **Azure Hdınsight Spark kümesinde**. Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark kümesi oluşturma](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="create-a-jupyter-notebook-toorun-interactive-queries"></a>Bir Jupyter not defteri toorun etkileşimli sorgular oluşturma

toorun sorguları hello kümesi ile ilişkili hello depolama bulunan varsayılan örnek verileri kullanın. Ancak, öncelikle bu veri Spark dataframe yüklemeniz gerekir. Merhaba dataframe sahip olduğunda, sorguları hello Jupyter Not Defteri kullanarak çalıştırabilirsiniz. Bu bölümde, nasıl bakın:

* Bir örnek veri kümesi Spark dataframe kaydedin.
* Sorgular hello dataframe üzerinde çalışır.

1. Açık hello [Azure portal](https://portal.azure.com/). Toopin hello küme toohello Pano ettiyseniz, hello Pano toolaunch hello küme dikey penceresinden hello küme kutucuğa tıklayın.

    Merhaba sol bölmesinden hello küme toohello Pano değil sabitlerseniz tıklatın **Hdınsight kümeleri**ve ardından oluşturduğunuz hello kümesine tıklayın.

3. **Hızlı bağlantılar** bölümünde **Küme panoları**'na ve ardından **Jupyter Notebook**'a tıklayın. İstenirse, hello küme için hello yönetici kimlik bilgilerini girin.

   ![Açık Jupyter not defteri toorun etkileşimli Spark SQL sorgusu](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-start-jupyter-interactive-spark-sql-query.png "açık Jupyter not defteri toorun etkileşimli Spark SQL sorgusu")

   > [!NOTE]
   > Kümenizin açma hello tarayıcınızda URL aşağıdaki tarafından hello Jupyter Not Defteri de erişebilirsiniz. Değiştir **CLUSTERNAME** kümenizi hello adı:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. Bir not defteri oluşturun. **Yeni** ve ardından **PySpark** seçeneğine tıklayın.

   ![Jupyter not defteri toorun etkileşimli Spark SQL sorgu oluşturma](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "Jupyter not defteri toorun etkileşimli Spark SQL sorgu oluşturma")

   Yeni bir not defteri oluşturulur ve Untitled(Untitled.pynb) hello adı ile açılır.

4. Merhaba üstünde Hello dizüstü bilgisayar adına tıklayın ve isterseniz kolay bir ad girin.

    ![Merhaba Jupter not defteri toorun etkileşimli Spark sorgu için bir ad](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-jupyter-notebook-name.png "hello Jupter not defteri toorun etkileşimli Spark sorgu için bir ad sağlayın")

5. Yapıştır hello aşağıdaki kod boş bir hücreye ve tuşuna basarak **SHIFT + ENTER** toorun hello kodu. Merhaba kod bu senaryo için gerekli hello türleri alır:

        from pyspark.sql.types import *

    Merhaba PySpark çekirdeği kullanarak bir not defteri oluşturduğunuz için siz toocreate bir bağlam açıkça gerekmez. hello birinci kod hücresini çalıştırdığınızda hello Spark ve Hive bağlamları sizin için otomatik olarak oluşturulur.

    ![Etkileşimli Spark SQL sorgusunun durumu](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-interactive-spark-query-status.png "Status of interactive Spark SQL query")

    Jupyter'de bir etkileşimli sorgusu her zaman, web tarayıcınızın Pencere başlığında gösteren bir **(meşgul)** hello not defteri başlığı ile birlikte durum. Ayrıca dolu daire sonraki toohello bkz **PySpark** hello sağ üst köşedeki metin. Merhaba iş tamamlandıktan sonra tooa boş daire değiştirir.

6. Bir Spark küme içinde hello veri yükleme önce bize bir görüntüsünü bakın sağlar. Merhaba Bu öğreticide kullanılan örnek veriler tüm Hdınsight Spark kümeleri, bir CSV dosyası olarak kullanılabilir **\HdiSamples\HdiSamples\SensorSampleData\hvac\hvac.csv**. Merhaba verileri bir yapı hello sıcaklık çeşitlemeleri yakalar. Merhaba verilerin ilk birkaç satırı hello şunlardır.

    ![Etkileşimli Spark SQL sorgusu için verilerin anlık görüntüsünü](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-spark-sample-data-interactive-spark-sql-query.png "etkileşimli Spark SQL sorgusu için verilerin anlık görüntüsünü")

6. Bir dataframe ve geçici bir tablo oluşturma (**hvac**) koddan hello çalıştırarak. Bu öğretici için size tüm hello sütunları hello geçici tabloya hello ham CSV verileri karşılaştırılan toohello sütun olarak oluşturmayın. 

        # Create an RDD from sample data
        hvacText = sc.textFile("wasbs:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        # Create a schema for our data
        Entry = Row('Date', 'Time', 'TargetTemp', 'ActualTemp', 'BuildingID')

        # Parse hello data and create a schema
        hvacParts = hvacText.map(lambda s: s.split(',')).filter(lambda s: s[0] != 'Date')
        hvac = hvacParts.map(lambda p: Entry(str(p[0]), str(p[1]), int(p[2]), int(p[3]), int(p[6])))
        
        # Infer hello schema and create a table       
        hvacTable = sqlContext.createDataFrame(hvac)
        hvacTable.registerTempTable('hvactemptable')
        dfw = DataFrameWriter(hvacTable)
        dfw.saveAsTable('hvac')

7. Merhaba verileri, etkileşimli sorgusu Hello tablo oluşturulduktan sonra aşağıdaki kodu hello kullanın.

        %%sql
        SELECT buildingID, (targettemp - actualtemp) AS temp_diff, date FROM hvac WHERE date = \"6/1/13\"

   Bir PySpark çekirdeği kullandığınız için artık doğrudan etkileşimli bir SQL sorgusu hello geçici tablosunda çalıştırabilirsiniz **hvac** hello kullanılarak oluşturulan `%%sql` Sihirli. Merhaba hakkında daha fazla bilgi için `%%sql` Sihirli ve hello PySpark çekirdeği kullanılabilen diğer sihirler bkz [Spark Hdınsight kümeleri ile Jupyter not defterlerinde kullanılabilen çekirdekler](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).

   Aşağıdaki tablo çıktısı hello varsayılan olarak görüntülenir.

     ![Etkileşimli Spark sorgu sonucunun tablo çıktısı](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result.png "Table output of interactive Spark query result")

    Ayrıca hello sonuçları diğer görselleştirmelerde de görebilirsiniz. Örneğin, bir alan grafiği için hello aynı çıktı hello şu şekilde görünür.

    ![Etkileşimli Spark sorgu sonucunun alan grafiği](./media/hdinsight-apache-spark-load-data-run-query/hdinsight-interactive-spark-query-result-area-chart.png "Area graph of interactive Spark query result")

9. Merhaba uygulaması çalıştıran bitirdikten sonra hello not defteri toorelease hello küme kaynaklarını kapatın. toodo çok hello **dosya** hello dizüstü menüsünde **Kapat ve Durdur**.

## <a name="next-step"></a>Sonraki adım

Bu, nasıl öğrenilen makale Jupyter Not Defteri kullanarak Spark toorun etkileşimli sorgular. Power BI ve Tableau gibi BI analizi aracını içine nasıl Spark kayıtlı hello veri çekilen toohello sonraki makalede toosee ilerleyin. 

> [!div class="nextstepaction"]
>[Spark Azure Hdınsight ile verileri görselleştirme araçlarını kullanarak BI](hdinsight-apache-spark-use-bi-tools.md)




