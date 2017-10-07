---
title: "aaaSpark BI Azure Hdınsight'ta veri görselleştirme araçları kullanarak | Microsoft Docs"
description: "Hdınsight kümelerinde Apache Spark BI'ı kullanarak analiz için verileri görselleştirme araçlarını kullanın"
keywords: "Apache spark BI, spark BI, spark veri görselleştirme, spark iş zekası"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1448b536-9bc8-46bc-bbc6-d7001623642a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: ba4bfff737ce80ffca5c24f1c2c82a1447f467fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-bi-using-data-visualization-tools-with-azure-hdinsight"></a>Apache Spark Azure Hdınsight ile verileri görselleştirme araçlarını kullanarak BI

Nasıl toouse veri görselleştirme gibi Power BI ve Tableau tooanalyze Hdınsight kümelerinde Apache Spark BI'ı kullanarak bir ham örnek veri kümesi araçları hakkında bilgi edinin.

> [!NOTE]
> Bu makalede açıklanan BI araçları ile bağlantı Spark 2.1 Azure Hdınsight 3.6 Önizleme üzerinde desteklenmiyor. Yalnızca Spark sürüm 1.6 ve 2.0 (Hdınsight 3.4, 3.5 sırasıyla) desteklenir.
>

Bu öğretici, bir Hdınsight Spark kümesinde Jupyter not defteri olarak da kullanılabilir. Merhaba not defteri deneyimi hello Python parçacıkları hello dizüstü bilgisayarınızı kendisini çalıştırmadan olanak sağlar. bir not defteri içinde tooperform hello öğretici bir Spark kümesi oluşturma, Jupyter not defteri başlatın (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), ve ardından hello dizüstü çalıştırın **HDInsight.ipynb Apache Spark kullanım BI araçlarıyla** hello altında **Python**  klasörü.

## <a name="prerequisites"></a>Ön koşullar

* Hdınsight'ta bir Apache Spark kümesi. Yönergeler için bkz: [Azure Hdınsight'ta Apache Spark oluşturmak kümeleri](hdinsight-apache-spark-jupyter-spark-sql.md).


## <a name="hivetable"></a>Spark veri görselleştirme için verileri hazırlama

Bu bölümde, hello kullanırız [Jupyter](https://jupyter.org) ham örnek verileri işlemek ve bir tablo olarak kaydetmek bir Hdınsight Spark küme toorun işleri dizüstü bilgisayarınızı. bir .csv dosyası (hvac.csv) kullanılabilir varsayılan olarak tüm kümelerde Hello örnek verilerdir. Verilerinizi bir tablo olarak kaydedildikten sonra sonraki bölümde hello biz BI araçları tooconnect toohello tabloyu kullanın ve veri görselleştirmeleri gerçekleştirin.

> [!NOTE]
> Gerçekleştiriyorsanız hello bu makalede hello yönergeleri tamamladıktan sonra adımları [bir Hdınsight Spark kümesinde etkileşimli sorgular gerçekleştirme](hdinsight-apache-spark-load-data-run-query.md), tooStep 8 aşağıdaki atlayabilirsiniz.
>

1. Merhaba gelen [Azure portal](https://portal.azure.com/), (, onu toohello Sabitle) hello Panosu'ndan hello kutucuğuna Spark kümenizin tıklayın. Tooyour küme altında da gidebilirsiniz **tümüne Gözat** > **Hdınsight kümeleri**.   

2. Merhaba Spark kümesi dikey penceresinden tıklatın **küme Panosu**ve ardından **Jupyter not defteri**. İstenirse, hello küme için hello yönetici kimlik bilgilerini girin.

   > [!NOTE]
   > Kümenizin açma hello tarayıcınızda URL aşağıdaki tarafından hello Jupyter Not Defteri de ulaşabilir. Değiştir **CLUSTERNAME** kümenizi hello adı:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >

3. Bir not defteri oluşturun. **Yeni** ve ardından **PySpark** seçeneğine tıklayın.

    ![Apache Spark BI için bir Jupyter not defteri oluşturma](./media/hdinsight-apache-spark-use-bi-tools/create-jupyter-notebook-for-spark-bi.png "için Apache Spark BI Jupyter not defteri oluşturma")

4. Yeni bir not defteri oluşturulur ve Untitled.pynb hello adı ile. Merhaba üstünde Hello dizüstü bilgisayar adına tıklayın ve kolay bir ad girin.

    ![Apache Spark BI hello dizüstü bilgisayar için ad](./media/hdinsight-apache-spark-use-bi-tools/jupyter-notebook-name-for-spark-bi.png "için Apache Spark BI hello dizüstü bilgisayar için bir ad sağlayın")

5. Merhaba PySpark çekirdeği kullanarak bir not defteri oluşturduğunuz için siz toocreate bir bağlam açıkça gerekmez. hello birinci kod hücresini çalıştırdığınızda hello Spark ve Hive bağlamları sizin için otomatik olarak oluşturulur. Bu senaryo için gerekli hello türleri içeri aktararak işleme başlayabilirsiniz. toodo hello hücre ve tuşuna hello imleç, yerleştirin **SHIFT + ENTER**.

        from pyspark.sql import *

6. Örnek verilerini geçici bir tabloya yükleyin. Merhaba örnek veri dosyası, Hdınsight'ta Spark kümesi oluşturduğunuzda, **hvac.csv**, kopyalanan toohello ilişkili depolama hesabı altında **\HdiSamples\HdiSamples\SensorSampleData\hvac**.

    Boş bir hücreye yapıştırın hello aşağıdaki kod parçacığında ve ENTER tuşuna **SHIFT + ENTER**. Bu kod parçacığında hello veri olarak adlandırılan bir tabloya kaydeder **hvac**.

        # Create an RDD from sample data
        hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

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

7. Merhaba tablosunun başarıyla oluşturulduğundan emin olun. Merhaba kullanabilirsiniz `%%sql` toorun Hive sorguları doğrudan Sihirli. Merhaba hakkında daha fazla bilgi için `%%sql` Sihirli ve hello PySpark çekirdeği kullanılabilen diğer sihirler bkz [Spark Hdınsight kümeleri ile Jupyter not defterlerinde kullanılabilen çekirdekler](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).

        %%sql
        SHOW TABLES

    Aşağıda gösterildiği gibi bir çıktı bakın:

        +---------------+-------------+
        |tableName      |isTemporary  |
        +---------------+-------------+
        |hvactemptable  |true        |
        |hivesampletable|false        |
        |hvac           |false        |
        +---------------+-------------+

    Yalnızca false hello altında sahip tablolar hello **isTemporary** sütun olacak şekilde hello meta depo içinde saklanan ve hello BI Araçları'ndan erişilebilen hive tablosu. Bu öğreticide, biz toohello bağlanmak **hvac** oluşturduğumuz tablo.

8. Merhaba tablosunun hello hedeflenen verileri içerdiğini doğrulayın. Boş bir hücreye hello Not, hello aşağıdakileri kopyalayın parçacığını ve tuşuna **SHIFT + ENTER**.

        %%sql
        SELECT * FROM hvac LIMIT 10

9. Merhaba not defteri toorelease hello kaynakları kapatın. toodo çok hello **dosya** hello dizüstü menüsünde **Kapat ve Durdur**.

## <a name="powerbi"></a>Power BI için Spark veri görselleştirme kullanın

> [!NOTE]
> Bu bölüm, yalnızca Hdınsight 3.4 üzerinde Spark 1.6 ve Hdınsight 3.5 Spark 2.0 için geçerlidir.
>
>

Merhaba verileri tablo olarak kaydettikten sonra Power BI tooconnect toohello verilerini kullanır ve toocreate raporları, görselleştirme vb. panoları.

1. Erişim tooPower BI olduğundan emin olun. Power BI'dan, ücretsiz önizlemeye aboneliği alabilirsiniz [http://www.powerbi.com/](http://www.powerbi.com/).

2. Çok oturum[Power BI](http://www.powerbi.com/).

3. Merhaba sol bölmesinde Hello aşağıdan tıklatın **Veri Al**.

4. Merhaba üzerinde **Veri Al** sayfasında **alma veya tooData bağlanmak**, için **veritabanları**, tıklatın **almak**.

    ![Apache Spark BI için Power BI Veri Al](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-import-data-power-bi.png "veri alma Power BI için Apache Spark BI")

5. Merhaba sonraki ekranda, tıklatın **Azure hdınsight'ta Spark** ve ardından **Bağlan**. İstendiğinde, hello kümesi URL'sini girin (`mysparkcluster.azurehdinsight.net`) ve hello kimlik bilgilerini tooconnect toohello küme.

    ![TooApache Spark BI bağlanmak](./media/hdinsight-apache-spark-use-bi-tools/connect-to-apache-spark-bi.png "tooApache Spark BI Bağlan")

    Merhaba bağlantı kurulduktan sonra Power BI hello Spark Hdınsight kümesinde veri alma başlatır.

6. Power BI hello verileri alır ve ekler bir **Spark** dataset hello altında **veri kümeleri** başlığı. Merhaba veri kümesi tooopen yeni çalışma sayfası toovisualize hello veri'ı tıklatın. Bir rapor olarak hello çalışma da kaydedebilirsiniz. toosave bir çalışma hello sayfasından **dosya** menüsünde tıklatın **kaydetmek**.

    ![Power BI panosundaki Apache Spark BI bölümünden](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-tile-dashboard.png "Power BI panosuna Apache Spark BI kutucuğu")
7. Bu hello fark **alanları** hello Sağdaki liste listeler hello **hvac** daha önce oluşturduğunuz tablo. Not defterinde daha önce tanımlanan hello tablo toosee hello alanları hello tablosundaki genişletin.

      ![Apache Spark BI Panoda Tabloları Listele](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-display-tables.png "Apache Spark BI Panoda Tabloları Listele")

8. Hedef sıcaklık ve her derleme için gerçek sıcaklık arasındaki görselleştirme tooshow hello fark oluşturun. toovisualize yoru verileri seçin **alan grafiği** (kırmızı kutu içinde gösterilmiştir). toodefine hello eksen, sürükle ve bırak hello **BuildingID** altında **eksen**, ve **ActualTemp**/**TargetTemp** altında alanları **değeri**.

    ![Apache Spark BI kullanarak veri görselleştirmeleri Spark oluşturma](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-add-value-columns.png "oluşturma Spark veri görselleştirmeleri Apache Spark BI kullanma")

9. Varsayılan olarak hello görselleştirme için hello toplam gösterir **ActualTemp** ve **TargetTemp**. Her ikisi de alanlardan hello aşağı açılan hello seçin **ortalama** tooget gerçek ortalama ve her iki binalar için hedef etme.

    ![Apache Spark BI kullanarak veri görselleştirmeleri Spark oluşturma](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-average-of-values.png "oluşturma Spark veri görselleştirmeleri Apache Spark BI kullanma")

10. Veri görselleştirme benzer toohello bir hello ekran görüntüsü olması gerekir. İmlecinizi hello görselleştirme tooget araç ipuçları ilgili verilerle üzerine getirin.

    ![Apache Spark BI kullanarak veri görselleştirmeleri Spark oluşturma](./media/hdinsight-apache-spark-use-bi-tools/apache-spark-bi-area-graph.png "oluşturma Spark veri görselleştirmeleri Apache Spark BI kullanma")

11. Tıklatın **kaydetmek** hello gelen üst menüsünde ve bir rapor adı sağlayın. Merhaba visual de sabitleyebilirsiniz. Bir görsel öğe PIN, böylece bir bakışta hello son değer izleyebilirsiniz Panonuzda depolanır.

   İstediğiniz sayıda görsel öğeleri ekleyebilirsiniz hello aynı veri kümesi ve verilerinizin anlık görüntü için toohello Pano sabitleyin. Ayrıca, hdınsight'ta Spark kümeleri BI ile doğrudan bağlantı bağlı tooPower değildir. Bu hello veri kümesi için tooschedule yenilemeleri gerek yoktur Power BI her zaman hello kümenizi en güncel verileri sahip olmasını sağlar.

## <a name="tableau"></a>Spark veri görselleştirme için Tableau Masaüstü'nü kullanın

> [!NOTE]
> Bu bölüm, yalnızca Azure Hdınsight'ta oluşturulan 1.5.2 Spark kümeleri için geçerlidir.
>
>

1. Yükleme [Tableau Masaüstü](http://www.tableau.com/products/desktop) bu Apache Spark BI öğretici çalıştırdığınız hello bilgisayarda.

2. Bu bilgisayarda ayrıca Microsoft Spark ODBC sürücüsü yüklü olduğundan emin olun. Merhaba sürücüsünden yükleyebilirsiniz [burada](http://go.microsoft.com/fwlink/?LinkId=616229).

1. Tableau Masaüstü başlatın. Merhaba sol bölmesinde, sunucu tooconnect için hello listesinden tıklatın **Spark SQL**. Spark SQL hello sol bölmesinde varsayılan olarak listelenmemişse tıklatın bulabilirsiniz **daha sunucuları**.
2. Merhaba ekran görüntüsünde gösterildiği gibi Hello Spark SQL Bağlantısı iletişim kutusunda, hello değerler sağlayın ve ardından **Tamam**.

    ![Apache Spark BI için Bağlan tooa küme](./media/hdinsight-apache-spark-use-bi-tools/connect-to-tableau-apache-spark-bi.png "Bağlan tooa küme Apache Spark BI için")

    kimlik doğrulama açılan listeleri hello **Microsoft Azure Hdınsight hizmeti** yalnızca hello yüklediyseniz bir seçenek olarak [Microsoft Spark ODBC sürücüsü](http://go.microsoft.com/fwlink/?LinkId=616229) hello bilgisayarda.
3. Merhaba gelen hello sonraki ekranında **şema** açılan listesinde, hello tıklatın **Bul** simgesine ve ardından **varsayılan**.

    ![Şema bulmak için Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-schema-apache-spark-bi.png "Apache Spark BI Bul şeması")
4. Hello için **tablo** hello'ı tıklatın **Bul** simge tekrar tüm hello toolist Hive tabloları hello kümede kullanılabilir. Merhaba görmelisiniz **hvac** önceki hello Not Defteri kullanarak oluşturduğunuz tablo.

    ![Tablo için Apache Spark BI Bul](./media/hdinsight-apache-spark-use-bi-tools/tableau-find-table-apache-spark-bi.png "Apache Spark BI Bul tablosu")
5. Merhaba tablo toohello üst kutusunda sağ hello sürükleyip yeniden açın. Tableau hello verileri alır ve hello şemasını hello kırmızı kutu ile vurgulanan görüntüler.

    ![Tablolar tooTableau eklemek için Apache Spark BI](./media/hdinsight-apache-spark-use-bi-tools/tableau-add-table-apache-spark-bi.png "için Apache Spark BI tabloları tooTableau Ekle")
6. Merhaba tıklatın **Sheet1** hello altındaki sol sekmesi. Merhaba ortalama hedef ve tüm binalar için gerçek etme her tarihini gösteren bir görsel öğe olun. Sürükleme **tarih** ve **bina kimliği** çok**sütunları** ve **gerçek Temp**/**hedef Temp**çok**satırları**. Altında **işaretleri**seçin **alanı** toouse Spark veri görselleştirme için alan eşleme.

     ![Spark veri görselleştirme için alanlar ekleyin](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-add-fields.png "Spark veri görselleştirme için alanlar ekleyin")
7. Varsayılan olarak, gösterilen hello sıcaklık alanlar toplama olarak. Bunun yerine tooshow hello ortalama etme istiyorsanız hello açılan listeden, aşağıda gösterildiği gibi bunu yapabilirsiniz.

    ![Sıcaklık Spark veri görselleştirme için ortalama ele](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-average-temperature.png "sıcaklık Spark veri görselleştirme için ortalama alın")

8. Ayrıca Süper-bir ısı Haritası uygulayabilir üzerinde diğer tooget hedef gerçek etme arasındaki farkı daha iyi bir fikir hello. Kırmızı bir daire vurgulanmış hello tanıtıcı şekli gördüğünüz kadar hello fare toohello köşe hello alt alan eşleme taşıyın. Kırmızı dikdörtgende vurgulanmış hello şekli gördüğünüzde hello harita toohello diğer harita üzerinde hello üst ve yayın hello fareyi sürükleyin.

    ![MAPS Spark veri görselleştirme için birleştirme](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-merge-maps.png "birleştirme eşler için Spark veri Görselleştirme")

     Veri görselleştirme hello ekran görüntüsünde gösterildiği gibi değiştirmeniz gerekir:

    ![Spark veri görselleştirme için tableau çıkış](./media/hdinsight-apache-spark-use-bi-tools/spark-data-visualization-tableau-output.png "Tableau çıktı için Spark veri Görselleştirme")
9. Tıklatın **kaydetmek** toosave hello çalışma. Panolar oluşturun ve bir veya daha fazla sayfaları tooit ekleyin.

## <a name="next-steps"></a>Sonraki adımlar

Şu ana kadar toocreate bir küme Spark veri çerçeveleri tooquery verileri oluşturma ve ardından bu BI Araçları'ndan verilere öğrendiniz. Şimdi nasıl toomanage küme kaynaklarını hello ve bir Hdınsight Spark kümesinde çalışan işlerin hata ayıklama yönergeleri bakabilirsiniz.

* [Hello Azure hdınsight'ta Apache Spark küme kaynaklarını yönetme](hdinsight-apache-spark-resource-manager.md)
* [HDInsight’ta bir Apache Spark kümesinde çalışan işleri izleme ve hata ayıklama](hdinsight-apache-spark-job-debugging.md)

