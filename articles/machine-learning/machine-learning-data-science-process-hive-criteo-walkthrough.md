---
title: "Azure Hdınsight Hadoop kümesi 1 TB veri kümesinde kullanarak eylem - Hello takım veri bilimi işlemi | Microsoft Docs"
description: "Bir Hdınsight Hadoop kullanan bir uçtan uca senaryo için Hello takım veri bilimi işlemi kullanarak toobuild küme ve bir büyük (1 TB) genel kullanıma açık veri kümesini kullanarak bir model dağıtma"
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 72d958c4-3205-49b9-ad82-47998d400d2b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 59b2af02e7840cb60a4b5b2f2c8ab0611df198ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action---using-an-azure-hdinsight-hadoop-cluster-on-a-1-tb-dataset"></a>Azure Hdınsight Hadoop kümesi 1 TB veri kümesinde kullanarak eylem - Hello takım veri bilimi işlemi

Bu kılavuzda, biz kullanarak gösteren bir uçtan uca senaryoda takım veri bilimi işlemi hello bir [Azure Hdınsight Hadoop kümesi](https://azure.microsoft.com/services/hdinsight/) toostore, keşfetme, özellik mühendislik ve aşağı hello birinden örnek verileri genel olarak kullanılabilir [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) veri kümeleri. Bu veriler üzerinde Azure Machine Learning toobuild ikili sınıflandırma modeli kullanırız. Nasıl toopublish bunlardan birini bir Web hizmeti olarak modelleri de gösterir.

Ayrıca, bir IPython not defteri tooaccomplish hello görevler bu kılavuzda sunulan olası toouse unutulmamalıdır. Bu yaklaşım başvurun tootry gibi hello kullanıcılar [Criteo izlenecek bir Hive ODBC bağlantısı kullanarak](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) konu.

## <a name="dataset"></a>Criteo Dataset açıklaması
Merhaba yaklaşık 370 GB sıkıştırılmış gzip TSV dosyaları (~1.3TB sıkıştırılmamış), bir tıklatın tahmin dataset verilerdir Criteo 4.3 milyardan fazla kayıtları kapsayan. 24 gün gerçekleştirilecek tarafından kullanılabilir duruma verileri tıklatın [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/). Veri bilimcilerine Hello kolaylık sağlamak için şu veri kullanılabilir toous tooexperiment ile sıkıştırması açılmış.

Bu veri kümesi her bir kayıtta 40 sütunları içerir:

* Merhaba ilk sütundur kullanıcı olup olmadığını belirten bir etiket sütunu bir **ekleme** (değer 1) veya bir (0 değeri) tıklatın değil
* sonraki 13 sütunları sayısal, ve
* Son 26 kategorik sütunlar:

Merhaba sütunları gizlidir ve bir dizi numaralandırılmış adları kullanın: (için hello etiket sütun) "Col1" çok ' Col40 "(Merhaba son Kategorik bir sütun için).            

İşte hello bir alıntı ilk 20 sütunlarının bu veri kümesine ilişkin iki gözlem (satır):

    Col1    Col2    Col3    Col4    Col5    Col6    Col7    Col8    Col9    Col10    Col11    Col12    Col13    Col14    Col15            Col16            Col17            Col18            Col19        Col20

    0       40      42      2       54      3       0       0       2       16      0       1       4448    4       1acfe1ee        1b2ff61f        2e8b2631        6faef306        c6fc10d3    6fcd6dcb           
    0               24              27      5               0       2       1               3       10064           9a8cb066        7a06385f        417e6103        2170fc56        acf676aa    6fcd6dcb                      

Bu veri kümesi içinde her iki hello sayısal ve kategorik sütunlarında eksik değerleri vardır. Biz hello eksik değerleri işlemek için basit bir yöntem açıklanmaktadır. Biz Hive tablolara depoladığınızda hello verilerin ek ayrıntılarını incelediniz.

**Tanımı:** *geçişli tıklatma oranı (Ctrl):* bu hello hello verilerdeki tıklama yüzdesidir. Bu Criteo kümesinde yaklaşık %3.3 veya 0.033 hello CTRL değil.

## <a name="mltasks"></a>Tahmin görev örnekleri
İki örnek tahmin sorunların bu kılavuzda ele alınmıştır:

1. **İkili sınıflandırma**: kullanıcı ekleme tıklattınız olup olmadığını tahmin:
   
   * Sınıfı 0: Hiçbir tıklatın
   * Sınıf 1:'ı tıklatın
2. **Regresyon**: kullanıcı özelliklerinden bir reklam tıklatma hello olasılığını tahmin eder.

## <a name="setup"></a>Veri bilimi için ayarlanmış yukarı bir Hdınsight Hadoop kümesi
**Not:** genellikle budur bir **yönetici** görev.

Üç adımda Hdınsight kümeleri ile Tahmine dayalı analiz çözümleri oluşturmak için Azure veri bilimi ortamınızı ayarlayın:

1. [Depolama hesabı oluşturma](../storage/common/storage-create-storage-account.md): kullanılan toostore verileri Azure Blob Depolama bu depolama hesabıdır. Hdınsight kümelerinde kullanılan hello verileri burada depolanır.
2. [Azure Hdınsight Hadoop kümeleri için veri bilimi özelleştirme](machine-learning-data-science-customize-hadoop-cluster.md): Bu adım, 64-bit Anaconda Python 2.7 tüm düğümlerde yüklü olan bir Azure Hdınsight Hadoop kümesi oluşturur. Merhaba Hdınsight kümesi özelleştirirken iki önemli adımlar (Bu konuda açıklanan) toocomplete vardır.
   
   * Merhaba depolama hesabı oluşturulduğunda, Hdınsight kümesi ile 1. adımda oluşturulan bağlamanız gerekir. Bu depolama hesabı hello küme içinde işlenebilecek verilerine erişmek için kullanılır.
   * Oluşturulduktan sonra uzaktan erişim toohello hello küme baş düğümüne etkinleştirmeniz gerekir. Burada belirttiğiniz (Merhaba küme oluşturma sırasında belirtilen kullanılanlardan farklı) başlangıç uzaktan erişim kimlik bilgilerini Hatırla: toocomplete gereksinim hello yordamlar.
3. [Azure ML çalışma alanı oluşturma](machine-learning-create-workspace.md): Bu Azure Machine Learning çalışma alanı, sonra ilk veri keşfi ve örnekleme hello Hdınsight kümesinde aşağı makine öğrenimi modellerini oluşturmak için kullanılır.

## <a name="getdata"></a>Alma ve ortak bir kaynaktan verileri kullanma
Merhaba [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) dataset erişilebilir hello bağlantıyı tıklatmak hello kullanım koşullarını kabul ederek ve sağlayan bir adı. Bunun nasıl göründüğünü, bir anlık görüntüsünü burada gösterilir:

![Criteo koşullarını kabul edin](./media/machine-learning-data-science-process-hive-criteo-walkthrough/hLxfI2E.png)

Tıklatın **devam tooDownload** tooread hello dataset ve onun kullanılabilirliği hakkında daha fazla bilgi.

Hello verilerin bulunduğu bir ortak [Azure blob depolama](../storage/blobs/storage-dotnet-how-to-use-blobs.md) konumu: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/. Merhaba "wasb" tooAzure Blob depolama konumunu belirtir. 

1. Bu ortak blob depolama birimindeki Hello veri sıkıştırması açılmış veri üç alt oluşur.
   
   1. alt hello *ham/sayısı/* hello ilk 21 günlük verilerini - gün içeren\_00 tooday\_20
   2. alt hello *ham/train/* verileri tek bir gününü oluşur gün\_21
   3. alt hello *ham/test/* iki günlük veri oluşur gün\_22 ve günü\_23
2. Kişiler için hello ham gzip verilerle toostart istediğiniz, bu da hello ana klasörde bulunan *ham /* burada NN gider 00 too23 day_NN.gz olarak.

Bir alternatif bir yaklaşım tooaccess keşfedin ve yerel yüklemeleri biz Hive tablolarını oluşturduğunuzda, daha sonra bu kılavuzda açıklanan gerektirmez bu veri modeli.

## <a name="login"></a>Toohello küme headnode oturum
Merhaba kümenin kullanım hello toohello headnode toolog [Azure portal](https://ms.portal.azure.com) toolocate hello küme. Sol hello Hello Hdınsight elephant simgesine tıklayın ve sonra kümenizi hello adına çift tıklayın. Toohello gidin **yapılandırma** sekmesinde hello sayfanın hello hello BAĞLAN simgesine çift tıklayın ve istendiğinde, uzaktan erişim kimlik bilgilerinizi girin. Bu toohello headnode hello kümesinin götürür.

İşte toohello küme headnode tipik ilk günlüğüne benzer:

![İçinde toocluster oturum](./media/machine-learning-data-science-process-hive-criteo-walkthrough/Yys9Vvm.png)

Merhaba solda hello "Hadoop komutu hello veri keşfi için bizim workhorse satırı" bakın. Biz de iki yararlı URL'leri - "Hadoop Yarn durumu" ve "Hadoop adı düğümü" bakın. Merhaba yarn durum URL İş ilerleme durumunu gösterir ve hello adı düğümü URL'si hello küme yapılandırmasına ayrıntılarını verir.

Şimdi biz ayarlanır ve hazır toobegin ilk bölümü hello izlenecek yol: Hive kullanarak ve Azure Machine Learning için verileri hazırlığı veri keşfi.

## <a name="hive-db-tables"></a>Hive veritabanı ve tablo oluşturma
toocreate Hive tabloları bizim Criteo veri kümesi için açık hello ***Hadoop komut satırı*** üzerinde hello Masaüstü hello baş düğümü ve hello komutunu girerek hello Hive dizini girin

    cd %hive_home%\bin

> [!NOTE]
> Tüm Hive komutları bu kılavuzda hello Hive Kutusu'ndan Çalıştır / directory istemi. Bu alan yol sorunları otomatik olarak dikkat edin. "Hive dizin istemi" Merhaba terimleri kullanırız "Hive bin / directory istemi" ve "Hadoop komut satırı" birbirinin yerine.
> 
> [!NOTE]
> tooexecute herhangi Hive sorgusu komutları aşağıdaki hello her zaman kullanabilirsiniz:
> 
> 

        cd %hive_home%\bin
        hive

Hive REPL Hello sonra görünür bir "hive >" oturum, yalnızca kesme ve yapıştırma hello sorgu tooexecute onu.

Merhaba aşağıdaki kod bir veritabanı "criteo" oluşturur ve 4 tablolar oluşturur:

* bir *sayıları oluşturmak için tablo* gün gününde yerleşik\_00 tooday\_20,
* bir *tren dataset hello olarak kullanım için tablo* günü yerleşik\_21, ve
* iki *test tabloları hello olarak kullanmak için veri kümeleri* günü yerleşik\_22 ve günü\_23 sırasıyla.

Biz test kümemize iki farklı tabloya hello gün birini tatil olduğundan ve tatil ve tatil olmayan arasındaki farklar hello geçişli tıklatma kurundan hello modeli algılarsa toodetermine istiyoruz bölün.

Merhaba betik [örnek &#95; hive & #95 oluşturun; &#95; criteo &#95; veritabanı &#95; ve &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) kolaylık sağlamak için burada görüntülenir:

    CREATE DATABASE IF NOT EXISTS criteo;
    DROP TABLE IF EXISTS criteo.criteo_count;
    CREATE TABLE criteo.criteo_count (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/count';

    DROP TABLE IF EXISTS criteo.criteo_train;
    CREATE TABLE criteo.criteo_train (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/train';

    DROP TABLE IF EXISTS criteo.criteo_test_day_22;
    CREATE TABLE criteo.criteo_test_day_22 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_22';

    DROP TABLE IF EXISTS criteo.criteo_test_day_23;
    CREATE TABLE criteo.criteo_test_day_23 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_23';

Bu tablolar biz yalnızca noktası tooAzure Blob Storage (wasb) konumları dış olduğunu unutmayın.

**Şimdi Bahsediyor iki yolu tooexecute herhangi Hive sorgusu vardır.**

1. **Merhaba Hive REPL komut satırı kullanarak**: hello ilk tooissue bir "hive" komutunu ve kopyalama ve bir sorgu Hive REPL komut satırı hello yapıştırın. toodo bunu yapın:
   
        cd %hive_home%\bin
        hive
   
     Merhaba sorgu Hello REPL komut satırı kesme ve yapıştırma şimdi yürütür.
2. **Kaydetme sorgular tooa dosya ve hello komutu yürütülürken**: hello ikinci dosyasıdır toosave hello sorguları tooa .hql ([örnek &#95; hive & #95 oluşturun; &#95; criteo &#95; veritabanı &#95; ve &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) ve ardından sorunu hello aşağıdaki tooexecute hello sorgu komutu:
   
        hive -f C:\temp\sample_hive_create_criteo_database_and_tables.hql

### <a name="confirm-database-and-table-creation"></a>Veritabanı ve tablo oluşturma onaylayın
Ardından, biz hello veritabanını hello oluşturmayı hello Hive Kutusu'ndan komutu aşağıdaki hello doğrulatın / directory istemi:

        hive -e "show databases;"

Bu sunar:

        criteo
        default
        Time taken: 1.25 seconds, Fetched: 2 row(s)

Bu hello yeni veritabanı "criteo" Merhaba oluşturulmasını doğrular.

toosee oluşturduğumuz, hangi tabloları biz yalnızca hello komutu burada hello Hive Kutusu'ndan yürütün / directory istemi:

        hive -e "show tables in criteo;"

Biz ardından çıktı aşağıdaki hello bakın:

        criteo_count
        criteo_test_day_22
        criteo_test_day_23
        criteo_train
        Time taken: 1.437 seconds, Fetched: 4 row(s)

## <a name="exploration"></a>Veri keşfi kovanında
Biz artık toodo bazı temel veri keşfi kovanında hazır. Biz hello tren örneklerde hello sayısı sayım tarafından başlamak ve veri tabloları sınayın.

### <a name="number-of-train-examples"></a>Tren örnek sayısı
Merhaba içeriğine [örnek &#95; hive &#95; sayısı &#95; eğitimi &#95; Tablo &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) burada gösterilir:

        SELECT COUNT(*) FROM criteo.criteo_train;

Bu verir:

        192215183
        Time taken: 264.154 seconds, Fetched: 1 row(s)

Alternatif olarak, biri de hello Hive Kutusu'ndan komutu aşağıdaki hello verebileceği / directory istemi:

        hive -f C:\temp\sample_hive_count_criteo_train_table_examples.hql

### <a name="number-of-test-examples-in-hello-two-test-datasets"></a>Test örnekleri hello iki test kümelerindeki sayısı
Biz şimdi hello hello iki test kümelerindeki örnek sayısı. Merhaba içeriğine [örnek &#95; hive &#95; sayısı &#95; criteo &#95; & #95 test; & #95 gün; 22 &#95; Tablo &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) şunlardır:

        SELECT COUNT(*) FROM criteo.criteo_test_day_22;

Bu verir:

        189747893
        Time taken: 267.968 seconds, Fetched: 1 row(s)

Her zamanki gibi biz de hello betik hello Hive Kutusu'ndan çağırabilir / directory hello komutu göndererek iste:

        hive -f C:\temp\sample_hive_count_criteo_test_day_22_table_examples.hql

Gün bazında hello test veri test örneklerde hello sayısı son olarak, inceleyeceğiz\_23.

Merhaba komutu toodo benzer toohello biri yalnızca gösterilen budur (çok başvuran[örnek &#95; hive &#95; sayısı &#95; criteo &#95; & #95 test; & #95 gün; 23 &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):

        SELECT COUNT(*) FROM criteo.criteo_test_day_23;

Bu sunar:

        178274637
        Time taken: 253.089 seconds, Fetched: 1 row(s)

### <a name="label-distribution-in-hello-train-dataset"></a>Dağıtım hello tren kümesindeki etiket
Merhaba etiket dağıtım hello tren kümesindeki ilginizi çekecektir. toosee Bu, içeriğini gösteriyoruz [örnek &#95; hive &#95; criteo &#95; & #95 etiket; & #95 dağıtım; eğitimi &#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):

        SELECT Col1, COUNT(*) AS CT FROM criteo.criteo_train GROUP BY Col1;

Merhaba etiket dağıtım verir:

        1       6292903
        0       185922280
        Time taken: 459.435 seconds, Fetched: 2 row(s)

Pozitif etiketleri Hello yüzdesi yaklaşık % 3.3 (Merhaba özgün kümesiyle tutarlı) olduğunu unutmayın.

### <a name="histogram-distributions-of-some-numeric-variables-in-hello-train-dataset"></a>Veri kümesi hello sayısal bazı değişkenler Histogram dağıtımlarını eğitme
Hive'nın yerel kullanırız "histogram\_sayısal" Merhaba sayısal değişkenlerin hangi hello dağıtım benzer çıkışı toofind işlev. Merhaba içeriğine işte [örnek &#95; hive &#95; criteo &#95; histogram &#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):

        SELECT CAST(hist.x as int) as bin_center, CAST(hist.y as bigint) as bin_height FROM
            (SELECT
            histogram_numeric(col2, 20) as col2_hist
            FROM
            criteo.criteo_train
            ) a
            LATERAL VIEW explode(col2_hist) exploded_table as hist;

Merhaba aşağıdaki verir:

        26      155878415
        2606    92753
        6755    22086
        11202   6922
        14432   4163
        17815   2488
        21072   1901
        24113   1283
        27429   1225
        30818   906
        34512   723
        38026   387
        41007   290
        43417   312
        45797   571
        49819   428
        53505   328
        56853   527
        61004   160
        65510   3446
        Time taken: 317.851 seconds, Fetched: 20 row(s)

Merhaba YANAL görünümü - Hive görevi görür tooproduce SQL benzeri çıktı hello normal listesi yerine birlikte Aç. Not ın Merhaba, bu tablo, hello ilk sütun toohello depo merkezi ve hello ikinci toohello depo sıklığı karşılık gelir.

### <a name="approximate-percentiles-of-some-numeric-variables-in-hello-train-dataset"></a>Veri kümesi hello bazı sayısal değişkenlerin yaklaşık yüzdebirlik değeri eğitme
Ayrıca sayısal değişkenleriyle yaklaşık yüzdebirlik değeri hello hesaplaması ilgilendirir. Hive yerel "yüzdelik\_yaklaşık" bunu bize yapar. Merhaba içeriğine [örnek &#95; hive &#95; criteo &#95; yaklaşık &#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) şunlardır:

        SELECT MIN(Col2) AS Col2_min, PERCENTILE_APPROX(Col2, 0.1) AS Col2_01, PERCENTILE_APPROX(Col2, 0.3) AS Col2_03, PERCENTILE_APPROX(Col2, 0.5) AS Col2_median, PERCENTILE_APPROX(Col2, 0.8) AS Col2_08, MAX(Col2) AS Col2_max FROM criteo.criteo_train;

Bu verir:

        1.0     2.1418600917169246      2.1418600917169246    6.21887086390288 27.53454893115633       65535.0
        Time taken: 564.953 seconds, Fetched: 1 row(s)

Yüzdebirlik değeri hello dağıtımını yakından ilgili toohello histogram dağıtım tüm sayısal değişkenin genellikle, remark.         

### <a name="find-number-of-unique-values-for-some-categorical-columns-in-hello-train-dataset"></a>Merhaba tren kümesindeki kategorik bazı sütunları için benzersiz değerlerin sayısını bulur
Merhaba veri keşfi, biz Şimdi Bul, bazı kategorik sütunlar için hello aldıkları benzersiz değerlerin sayısını devam ediliyor. toodo Bu, içeriğini gösteriyoruz [örnek &#95; hive &#95; criteo &#95; benzersiz &#95; değerleri &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):

        SELECT COUNT(DISTINCT(Col15)) AS num_uniques FROM criteo.criteo_train;

Bu verir:

        19011825
        Time taken: 448.116 seconds, Fetched: 1 row(s)

Col15 19 M benzersiz değerler olduğunu unutmayın! "Bir hot kodlama" tooencode gibi naïve teknikler kullanılarak yüksek boyutlu tür kategorik değişkenlerinin uygulanamaz. Özellikle, biz açıklayabilir ve adında güçlü, sağlam bir teknik göstermek [ile öğrenme sayar](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) bu sorunu verimli bir şekilde tackling için.

Biz, bu alt bölümde bazı diğer kategorik sütunlar için de benzersiz değerlerin sayısını hello bakarak sonlandırın. Merhaba içeriğine [örnek &#95; hive &#95; criteo &#95; benzersiz &#95; & #95 değerleri; birden çok &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) şunlardır:

        SELECT COUNT(DISTINCT(Col16)), COUNT(DISTINCT(Col17)),
        COUNT(DISTINCT(Col18), COUNT(DISTINCT(Col19), COUNT(DISTINCT(Col20))
        FROM criteo.criteo_train;

Bu verir:

        30935   15200   7349    20067   3
        Time taken: 1933.883 seconds, Fetched: 1 row(s)

Yeniden Col20 hariç, tüm diğer hello olduğunu görmek sütunları birçok benzersiz değerlere sahip.

### <a name="co-occurrence-counts-of-pairs-of-categorical-variables-in-hello-train-dataset"></a>Merhaba tren kümesindeki kategorik değişkenleri çiftlerini ortak oluşum sayısı

Ayrıca ilgi kategorik değişkenleri çiftlerini Hello ortak oluşum sayısı olur. Bu hello kod içinde kullanma belirlenebilir [örnek &#95; hive &#95; criteo &#95; eşleştirilmiş &#95; kategorik &#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):

        SELECT Col15, Col16, COUNT(*) AS paired_count FROM criteo.criteo_train GROUP BY Col15, Col16 ORDER BY paired_count DESC LIMIT 15;

Biz sipariş hello sayıları kendi örneği tarafından ters ve 15 hello üstünde bu durumda bakın. Bu bize sunar:

        ad98e872        cea68cd3        8964458
        ad98e872        3dbb483e        8444762
        ad98e872        43ced263        3082503
        ad98e872        420acc05        2694489
        ad98e872        ac4c5591        2559535
        ad98e872        fb1e95da        2227216
        ad98e872        8af1edc8        1794955
        ad98e872        e56937ee        1643550
        ad98e872        d1fade1c        1348719
        ad98e872        977b4431        1115528
        e5f3fd8d        a15d1051        959252
        ad98e872        dd86c04a        872975
        349b3fec        a52ef97d        821062
        e5f3fd8d        a0aaffa6        792250
        265366bf        6f5c7c41        782142
        Time taken: 560.22 seconds, Fetched: 15 row(s)

## <a name="downsample"></a>Örnek hello veri kümesi Azure Machine Learning için
Keşfedilen hello veri kümeleri sahip ve nasıl biz Azure Machine Learning modellerini oluşturabilmeleri Biz bu tür herhangi bir değişkeni için (dahil olmak üzere birleşimleri), biz şimdi örnek hello veri kümelerini aşağı araştırması yapabilirsiniz gösterilmektedir. Biz odak o hello sorun geri çağırma: örnek öznitelikler (Col2 - Col40 özellik değerleri) kümesi verildiğinde, biz Col1 0 (hiçbir tıklayın) veya 1 (tıklatın) olup olmadığını tahmin.

toodown bizim tren örnek ve hello özgün boyutunun veri kümeleri too1% test, Hive'nın yerel RAND() işlevinin kullanırız. Merhaba sonraki komut [örnek &#95; hive &#95; criteo &#95; alt örnekleyin &#95; eğitimi &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) hello tren veri kümesi için bunu yapar:

        CREATE TABLE criteo.criteo_train_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        ---Now downsample and store in this table

        INSERT OVERWRITE TABLE criteo.criteo_train_downsample_1perc SELECT * FROM criteo.criteo_train WHERE RAND() <= 0.01;

Bu verir:

        Time taken: 12.22 seconds
        Time taken: 298.98 seconds

Merhaba betik [örnek &#95; hive &#95; criteo &#95; alt örnekleyin &#95; & #95 test; & #95 gün; 22 &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) test verileri için mevcut gün\_22:

        --- Now for test data (day_22)

        CREATE TABLE criteo.criteo_test_day_22_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_22_downsample_1perc SELECT * FROM criteo.criteo_test_day_22 WHERE RAND() <= 0.01;

Bu verir:

        Time taken: 1.22 seconds
        Time taken: 317.66 seconds


Son olarak, komut dosyası hello [örnek &#95; hive &#95; criteo &#95; alt örnekleyin &#95; & #95 test; & #95 gün; 23 &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) test verileri için mevcut gün\_23:

        --- Finally test data day_23
        CREATE TABLE criteo.criteo_test_day_23_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 srical feature; tring)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_23_downsample_1perc SELECT * FROM criteo.criteo_test_day_23 WHERE RAND() <= 0.01;

Bu verir:

        Time taken: 1.86 seconds
        Time taken: 300.02 seconds

Bu, biz bizim aşağı örneklenen hazır toouse, eğitim ve test Azure Machine Learning modellerini oluşturmak için veri kümeleri.

Biz sorunları hello sayısı tablosu Machine Learning tooAzure üzerinde taşımadan önce son önemli bileşeni yoktur. Merhaba sonraki alt bölümde, biz bu biraz ayrıntılı olarak ele alınmıştır.

## <a name="count"></a>Merhaba sayısı tablosundaki kısa bir tartışma
Gördüğümüz gibi çeşitli kategorik değişkenler çok yüksek bir boyut sahiptir. Bizim kılavuzda, biz adında güçlü bir teknik sunmak [ile öğrenme sayar](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) tooencode verimli ve güçlü bir şekilde bu değişkenleri. Bu teknik hakkında daha fazla bilgi sağlanan hello içinde bağlantıdır.

[!NOTE]
>Bu kılavuzda, count tabloları tooproduce compact gösterimlerini yüksek boyutlu kategorik özellikleri kullanarak odaklanın. Bu hello tek yolu tooencode kategorik özellikleri değildir; diğer teknikleri hakkında daha fazla bilgi için ilgi kullanıcılar kontrol edebilirsiniz [bir-hot-encoding](http://en.wikipedia.org/wiki/One-hot) ve [özellik karma](http://en.wikipedia.org/wiki/Feature_hashing).
>

Merhaba sayısı verileri toobuild sayısı tablolarda, hello klasörü ham/sayıma hello veri kullanırız. Bölümünde, kullanıcıların gösteriyoruz modelleme hello nasıl toobuild bunlar sayısı sıfırdan veya alternatif olarak toouse kategorik özellikleri için kendi explorations için önceden derlenmiş sayısı tablosu tabloları. Ne de biz başvurduğunuzda aşağıdaki çok "önceden oluşturulmuş sayısı tablolar", sağladığımız hello sayısı tabloları kullanarak anlama. Nasıl tooaccess bu tablolar hello sonraki bölümde sağlanan ayrıntılı yönergeler için.

## <a name="aml"></a>Azure Machine Learning ile bir model oluşturma
Oluşturma işlemi Azure Machine learning'de modelimizi şu adımları izler:

1. [Merhaba verileri Hive tablolardan Azure Machine Learning alın.](#step1)
2. [Merhaba deneme oluşturma: hello veri ve featurize sayısı tablolar ile temizleme](#step2)
3. [Yapı, eğitme ve puanı hello modeli](#step3)
4. [Merhaba modelini değerlendir](#step4)
5. [Web hizmeti olarak Hello modeli yayımlama](#step5)

Artık Azure Machine Learning Studio'da hazır toobuild modelleri bulunur. Aşağı örneklenen verilerimizi hello kümesindeki Hive tablolarını olarak kaydedilir. Hello Azure Machine Learning kullanırız **veri içeri aktarma** modülü tooread bu verileri. Bu kümenin Hello kimlik bilgilerini tooaccess hello depolama hesabı hangi aşağıdaki sağlanır.

### <a name="step1"></a>1. adım: Azure Machine Learning hello veri içeri aktarma modülü kullanılarak Hive tablolarından veri almak ve bir makine öğrenimi denemesinin için seçin
Başlangıç seçerek bir **+ yeni** -> **deneme** -> **boş deneme**. Merhaba öğesinden sonra **arama** hello üst sol, "Veri Al" için arama kutusunu. Sürükle ve bırak hello **veri içeri aktarma** toohello deneme tuvaline (Merhaba ekranında hello Orta bölümü) toouse hello modülü veri erişimi için modülünü.

Hangi hello budur **veri içeri aktarma** gibi görünüyor hello Hive tablodan veri alınırken hata oluştu:

![Veri içeri aktarma verileri alır](./media/machine-learning-data-science-process-hive-criteo-walkthrough/i3zRaoj.png)

Hello için **veri içeri aktarma** modülü, grafik hello olan sağlanan hello yalnızca örnekleri tür değerleri, hello parametrelerinin hello değerleri tooprovide gerekir. İşte bazı genel rehberlik toofill çıkış hello parametresi Merhaba nasıl ayarlanacağını **veri içeri aktarma** modülü.

1. "Hive sorgusu" seçin **veri kaynağı**
2. Merhaba, **Hive veritabanı sorgusu** kutusunda, basit bir SELECT * FROM <,\_veritabanı\_name.your\_tablo\_adı >-yeterlidir.
3. **Hcatalog sunucusu URI**: "abc" kümeniz olduğunu sonra yalnızca budur: https://abc.azurehdinsight.net
4. **Hadoop kullanıcı hesabı adı**: hello küme commissioning hello sırasında seçilen hello kullanıcı adı. (Merhaba uzaktan erişim kullanıcı adı değil!)
5. **Hadoop kullanıcı hesabı parolasını**: hello parolasını hello küme commissioning hello sırasında seçilen hello kullanıcı adı. (Değil hello uzaktan erişim parola!)
6. **Çıktı verilerini konumunu**: "Azure" seçin
7. **Azure depolama hesabı adı**: Merhaba hello kümeyle ilişkili depolama hesabı
8. **Azure depolama hesabı anahtarı**: hello kümesi ile ilişkili hello depolama hesabı hello anahtarı.
9. **Azure kapsayıcı adı**: hello küme adı olduğundan "abc" sonra yalnızca "abc", genellikle budur.

Bir kez hello **veri içeri aktarma** sonlandığında (gördüğünüz hello yeşil onay işareti hello modülü üzerinde) veri alma (tercih ettiğiniz bir adla) bir veri kümesi olarak bu verileri kaydedin. Bunun nasıl göründüğünü:

![Veri alma veri kaydetme](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oxM73Np.png)

Sağ hello çıktı hello bağlantı noktası **veri içeri aktarma** modülü. Bu gösteren bir **veri kümesi Kaydet** seçeneği ve bir **Görselleştir** seçeneği. Merhaba **Görselleştir** seçeneği tıkladıysanız, bazı Özet istatistikleri için yararlı olan bir sağ panelde birlikte hello veri 100 satırı görüntüler. toosave veri seçmeniz yeterlidir **veri kümesi Kaydet** ve yönergeleri izleyin.

tooselect kaydedilen hello kullanılmak üzere bir machine learning deneme bulun hello kullanarak hello veri kümeleri **arama** hello aşağıdaki şekilde gösterilen kutusu. Yalnızca türünü verdiğiniz hello adı öğrenmek hello sonra dataset kısmen ve sürükleme hello üzerine dataset tooaccess hello ana bölmesi. Merhaba ana panelinden bırakmadan machine learning modelleme kullanmak için seçilir.

![Merhaba ana panelinin üzerine Drage veri kümesi](./media/machine-learning-data-science-process-hive-criteo-walkthrough/cl5tpGw.png)

> [!NOTE]
> Merhaba eğitimi ve hello test veri kümeleri için bunu. Ayrıca, toouse hello veritabanı adı ve bu amaçla verdiğiniz tablo adlarının unutmayın. Merhaba şekilde kullanılan hello değerler yalnızca çizim yaratılır * için:
> 
> 

### <a name="step2"></a>2. adım: Azure Machine Learning toopredict tıklatma ile basit bir deneme oluşturma / hiçbir tıklama
Bizim Azure ML deneme şöyle görünür:

![Machine Learning deneme](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xRpVfrY.png)

Şimdi bu deneme anahtar bileşenlerinin hello inceleyeceğiz. Bir hatırlatma bizim kaydedilmiş eğitmek ve tooour deneme tuvalinin veri kümelerinin önce test toodrag gerekir.

#### <a name="clean-missing-data"></a>Eksik verileri temizleme
Merhaba **Clean Missing Data** modülü mu ne adından da anlaşılacağı: kullanıcı tarafından belirtilen yolla eksik verileri temizler. Bu modüle baktığınızda, biz bu bakın:

![Eksik verilerini temizle](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0ycXod6.png)

Burada, tooreplace tüm eksik değerleri 0 ile seçtik. Merhaba bırakmalar hello modülünde bakarak görülebilir diğer seçenekler de vardır.

#### <a name="feature-engineering-on-hello-data"></a>Özellik Mühendisliği hello verileri
Büyük veri kategorik bazı özellikler için benzersiz değerler milyonlarca olabilir. Naïve yöntemlerden biri hot yüksek boyutlu kategorik özelliklerden temsil etmek için kodlama gibi tamamen unfeasible kullanmaktır. Bu kılavuzda, nasıl toouse sayısı özellikleri yerleşik Azure Machine Learning modüllerinin toogenerate kullanarak bu yüksek boyutlu kategorik değişkenleri gösterimlerini compact göstermektedir. Merhaba nihai sonucu daha küçük bir model boyutu, daha hızlı eğitim süreleri, oldukça karşılaştırılabilir toousing olan performans ölçümleri ise başka teknikler.

##### <a name="building-counting-transforms"></a>Dönüşümler sayım oluşturma
toobuild sayısı özellikleri kullanırız hello **yapı sayım dönüştürme** Azure Machine Learning kullanılabilir modül. Merhaba modülü şöyle görünür:

![Sayım dönüştürme modülü oluşturmak](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![yapı sayım dönüştürme Modülü](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)

> [!IMPORTANT] 
> Merhaba, **saymak sütunları** kutusu, biz girin tooperform sayar istediğimiz bu sütunları. Genellikle, bunlar (belirtildiği gibi) yüksek boyutlu kategorik sütun. Merhaba başlangıcında Biz bu hello Criteo dataset 26 kategorik sütunları belirtilen sahip: Col15 tooCol40 gelen. Burada, biz hepsinde saymak ve bunların dizinlerini (gösterildiği gibi virgülle ayırarak 15 too40) verin.
> 

toouse hello modülünde hello MapReduce modu (büyük veri kümeleri için uygundur), biz tooan Hdınsight Hadoop kümesi (Bu amaç için bir özellik araştırması için kullanılan yeniden kullanılabilir hello) ve kimlik bilgileri erişim. Merhaba önceki rakamları görünüm gibi (kendi kullanım durumu için ilgili olanla çizim için sağlanan hello değerleri değiştirin) hello doldurulan değerleri gösterilmektedir.

![Modülü parametreleri](./media/machine-learning-data-science-process-hive-criteo-walkthrough/05IqySf.png)

Yukarıdaki Hello şekil içinde nasıl tooenter hello blob giriş olan gösteriyoruz konumu. Bu konumda sayısı tabloları oluşturma için ayrılmış hello veri yok.

Bu modül çalışması bittikten sonra biz hello dönüştürme için daha sonra hello modülü sağ tıklayıp hello seçerek kaydedebilirsiniz **dönüştürme Kaydet** seçeneği:

!["Dönüştürme Kaydet" seçeneğini](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IcVgvHR.png)

Yukarıda gösterilen bizim deneme mimarisinde hello dataset "ytransform2" tam sayı dönüşümü kaydedilmiş tooa karşılık gelir. Bu deneme Hello kalanı için kullanılan bu hello okuyucu varsayıyoruz bir **yapı sayım dönüştürme** modülü bazı veri toogenerate sayısı ve ardından olabilir, bu sayıları toogenerate sayısı özellikleri hello tren üzerinde kullanmak ve test veri kümeleri.

##### <a name="choosing-what-count-features-tooinclude-as-part-of-hello-train-and-test-datasets"></a>Hangi özellikleri tooinclude hello tren bir parçası olarak say ve veri kümelerini test seçme
Hazır dönüştürme sayısı sahibiz sonra hello kullanıcı kendi tren hangi özellikleri tooinclude seçin ve test hello kullanan veri Setleri **sayısı tablo parametreleri değiştirmek** modülü. Yalnızca bu modül gösteriyoruz burada eksiksiz olması için ancak Basitlik ilgi gerçekten bunu bizim deneme kullanmayın.

![Count tablo parametreleri değiştirin](./media/machine-learning-data-science-process-hive-criteo-walkthrough/PfCHkVg.png)

Bu durumda, görüldüğü gibi biz yalnızca hello günlük büyük olasılıkla toouse seçmiş ve tooignore hello geri sütun devre dışı. Biz de hello çöp depo eşiği düzgünleştirme için kaç tane sözde önceki örnekler tooadd gibi parametreleri ayarlayabilirsiniz ve olup toouse herhangi Laplacian gürültü veya değil. Bunların tümü Gelişmiş Özellikler ve bu toobe hello varsayılan değerleri özelliği nesil yeni toothis türü olan kullanıcılar için iyi bir başlangıç noktası olduğunu belirtilmiştir.

##### <a name="data-transformation-before-generating-hello-count-features"></a>Merhaba sayısı özellikleri oluşturmadan veri dönüştürme
Şimdi biz bizim tren dönüştürme hakkında önemli bir nokta odaklanır ve veri önceki tooactually sayısı özellikleri oluşturma sınayın. İki olduğunu unutmayın **R betiği yürütün** biz hello sayısı dönüştürme tooour verileri uygulamadan önce kullanılan modülleri.

![R betiği modülleri yürütme](./media/machine-learning-data-science-process-hive-criteo-walkthrough/aF59wbc.png)

Merhaba ilk R betiği şöyledir:

![İlk R betiği](./media/machine-learning-data-science-process-hive-criteo-walkthrough/3hkIoMx.png)

Bu R betiği biz bizim sütunları toonames "Col1" çok yeniden adlandırma "Col40". Bu biçim adını Hello sayısı dönüştürme bekliyor olmasıdır.

Merhaba ikinci R komut dosyasında, biz hello dağıtım pozitif ve negatif sınıflar arasında dengeleyin (sırasıyla 1 ve 0 sınıfları) aşağı örnekleme hello negatif sınıfı tarafından. Merhaba R betiği buraya gösterir nasıl toodo bu:

![İkinci R betiği](./media/machine-learning-data-science-process-hive-criteo-walkthrough/91wvcwN.png)

Basit bir R betiği kullanırız "pos\_neg\_oranı" hello pozitif ve negatif hello sınıflar arasında bir denge tooset hello miktarı. Bu sınıf dengesizliği genellikle geliştirme sınıflandırma sorunları için performans avantajı hello sınıfı dağıtım olduğu olduğundan toodo (örneğimizde, biz %3.3 pozitif ve negatif %96.7 sınıf olduğunu geri çağırma) eğri önemlidir.

##### <a name="applying-hello-count-transformation-on-our-data"></a>Verilerimizi uygulanan hello sayısı dönüşümü
Son olarak, biz hello kullanabilirsiniz **uygulamak dönüştürme** modülü tooapply hello bizim tren üzerinde sayısı dönüşümler ve test veri kümeleri. Bu modül bir giriş ve hello eğitmek veya test diğer giriş hello gibi veri kümeleri olarak kaydedilen hello sayısı dönüştürme alır ve sayısı özelliklere sahip verileri döndürür. Burada gösterilir:

![Dönüştürme modülü Uygula](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xnQvsYf.png)

##### <a name="an-excerpt-of-what-hello-count-features-look-like"></a>Merhaba sayısı özellikleri neye benzediğini gösteren bir alıntı
Bu örneğimizde hangi hello sayısı özellikler neye benzediğini gösteren yönergeli toosee olur. Burada bir alıntı bu göster:

![Count özellikleri](./media/machine-learning-data-science-process-hive-criteo-walkthrough/FO1nNfw.png)

Bu alıntı, biz sayılan hello sütunların, biz hello sayılarını elde ve büyük olasılıkla toplama tooany ilgili backoffs oturum olduğunu gösterir.

Şimdi hazır toobuild dönüştürülmüş bu veri kümelerini kullanarak bir Azure Machine Learning modeli duyuyoruz. Merhaba sonraki bölümde, bu nasıl yapılabilir gösterir.

### <a name="step3"></a>3. adım: Oluşturmak, eğitmek ve hello modeli Puanlama

#### <a name="choice-of-learner"></a>Öğrenen seçimi
İlk olarak, toochoose bir öğrenen gerekir. Bizim öğrenen giderek toouse boosted iki sınıf karar ağacı duyuyoruz. Bu öğrenen için hello varsayılan seçenekleri şunlardır:

![İki-Class Boosted karar ağacı parametreleri](./media/machine-learning-data-science-process-hive-criteo-walkthrough/bH3ST2z.png)

Bizim deneme için devam eden toochoose hello varsayılan değerleri duyuyoruz. Bu hello genellikle anlamlı olan ve performansı en iyi yolu tooget hızlı temelleri varsayılanlarını unutmayın. Sahip olduğunuz tooonce seçerseniz, parametreleri temel yerleştirmez tarafından performansını iyileştirebilir.

#### <a name="train-hello-model"></a>Tren hello modeli
Eğitim için biz yalnızca çağırma bir **Train Model** modülü. Merhaba iki girişleri tooit hello iki-Class Boosted karar ağacı öğrenen ve tren kümemize verilmiştir. Bu aşağıda gösterilmiştir:

![Train Model Modülü](./media/machine-learning-data-science-process-hive-criteo-walkthrough/2bZDZTy.png)

#### <a name="score-hello-model"></a>Puan hello modeli
Biz bir modeli eğittikten sonra biz hazır tooscore hello üzerinde kendi performans veri kümesi ve tooevaluate test. Biz hello kullanarak bunu **Score Model** modülü ile birlikte aşağıdaki şekilde, hello gösterildiği bir **Evaluate Model** Modülü:

![Score Model (Model Puanlama) modülü](./media/machine-learning-data-science-process-hive-criteo-walkthrough/fydcv6u.png)

### <a name="step4"></a>4. adım: hello modelini değerlendir
Son olarak, tooanalyze modeli performans isteriz. Genellikle, iki sınıfı (ikili) sınıflandırma sorunu için iyi hello AUC ölçüsüdür. toovisualize Bu, biz hello kanca **Score Model** modülü tooan **Evaluate Model** için bu modülü. Tıklatarak **Görselleştir** hello üzerinde **Evaluate Model** modülü bir aşağıdaki hello gibi bir grafik verir:

![Modül BDT modelini değerlendir](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0Tl0cdg.png)

İkili (veya iki sınıf) sınıflandırma sorunları, tahmin doğruluğunu iyi bir ölçü alanı altında eğri (AUC) hello. Ne izleyen test kümemize bu modeli kullanarak sonuçları gösteriyoruz. tooget Bu, sağ hello çıkış bağlantı noktasına hello **Evaluate Model** modülü ve ardından **Görselleştir**.

![Evaluate Model modülü Görselleştirme](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IRfc7fH.png)

### <a name="step5"></a>5. adım: bir Web hizmeti olarak hello modeli yayımlama
Hello özelliği toopublish web hizmetleri fuss en az olarak bir Azure Machine Learning modeli, yaygın olarak kullanılabilir hale getirme için değerli bir özelliktir. Bu yapıldığında, herkesin çağrıları toohello web hizmeti tahminleri için ihtiyaç duydukları ve hello web hizmeti, bu Öngörüler hello modeli tooreturn kullanır giriş verileri ile yapabilirsiniz.

toodo Bu, biz bizim eğitilen modeli eğitilen Model nesnesi olarak kaydedin. Bu hello sağ tıklayarak yapılır **Train Model** modülü ve hello kullanarak **eğitilen modelini Farklı Kaydet** seçeneği.

Toocreate giriş ve çıkış daha ihtiyacımız bizim web hizmeti için bağlantı noktaları:

* bir giriş bağlantı noktası aynı tahminleri için ihtiyacımız hello veri olarak form hello içinde veri alır.
* bir çıkış bağlantı noktasına hello skoru etiketleri ve ilişkili hello olasılıklar döndürür.

#### <a name="select-a-few-rows-of-data-for-hello-input-port"></a>Veri hello giriş bağlantı noktası için birkaç satır seçin
Uygun toouse olan bir **geçerli SQL dönüştürme** modülü tooselect yalnızca 10 satır tooserve hello olarak giriş bağlantı noktası verileri. Yalnızca bu burada gösterilen hello SQL sorgusunu kullanarak, giriş bağlantı noktası için veri satırı seçin:

![Giriş bağlantı noktası verileri](./media/machine-learning-data-science-process-hive-criteo-walkthrough/XqVtSxu.png)

#### <a name="web-service"></a>Web hizmeti
Biz artık toorun kullanılan toopublish olabilir küçük bir deneme bizim web hizmeti hazır.

#### <a name="generate-input-data-for-webservice"></a>Web hizmeti için giriş verileri oluştur
Sıfırıncı adım olarak hello sayısı tablo büyük olduğundan biz birkaç satırlık bir test verilerini alın ve çıktı verilerini buradan sayısı özelliklerle oluşturun. Bu bizim webservice için hello giriş veri biçimi olarak hizmet verebilir. Bu aşağıda gösterilmiştir:

![BDT giriş verileri oluşturma](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OEJMmst.png)

> [!NOTE]
> Merhaba giriş veri biçimi için şimdi hello hello ÇIKTISINI kullanırız **sayısı Featurizer** modülü. Bu deneme çalıştıran bittikten sonra hello hello çıkış kaydedin **sayısı Featurizer** modülü bir veri kümesi olarak. Bu veri kümesi hello webservice hello girdi verileri için kullanılır.
> 
> 

#### <a name="scoring-experiment-for-publishing-webservice"></a>Deneme için Web Yayımlama hizmeti Puanlama
İlk olarak, bu nasıl göründüğünü gösterir. Merhaba temel yapısı bir **Score Model** bizim eğitilen model nesnesi ve birkaç satırlık biz hello kullanarak hello önceki adımlarda oluşturulan giriş verilerini kabul eden modül **sayısı Featurizer** modülü. "Sütun Dataset içinde seçin" tooproject hello Scored etiketleri ve hello puan olasılıklar kullanırız.

![Veri kümesinde sütun seçme](./media/machine-learning-data-science-process-hive-criteo-walkthrough/kRHrIbe.png)

Nasıl hello fark **Select Columns in Dataset sütun** modülü, 'verileri bir veri kümesinden filtreleme' için kullanılabilir. Biz, burada hello içindekileri göster:

![Veri kümesi modülünde hello Sütunları Seç ile filtreleme](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oVUJC9K.png)

tooget giriş ve çıkış hello mavi bağlantı noktaları, yalnızca tıklattığınız **webservice hazırlama** sağ hello altındaki. Bu deneme çalıştırılması de olanak tanır. bize toopublish hello web hizmeti: hello tıklatın **yayımlama WEB hizmeti** hello alt right, gösterilen burada simgesine tıklayın:

![Web hizmeti yayımlama](./media/machine-learning-data-science-process-hive-criteo-walkthrough/WO0nens.png)

Hello webservice yayımlandığında, şu nedenle yeniden yönlendirilen tooa sayfası alın:

![Web hizmeti Panosu](./media/machine-learning-data-science-process-hive-criteo-walkthrough/YKzxAA5.png)

Biz, hello sol tarafındaki webservices'a için iki bağlantılara bakın:

* Merhaba **istek/yanıt** hizmet (ya da RR) için tek tahminleri tasarlanmıştır ve ne Biz bu Atölye kullanma biçimleridir.
* Merhaba **toplu iş yürütme** hizmeti (BES) için toplu tahminleri kullanılır ve hello kullanılan giriş verileri toomake tahminleri Azure Blob depolama alanına bulunmasını gerektirir.

Merhaba bağlantıyı tıklatmak **istek/yanıt** bize tooa alır bize veriyor sayfa önceden tamamlanmış C#, python ve r kodu Bu kod rahat çağrıları toohello webservice yapmak için kullanılabilir. Kimlik doğrulaması için kullanılan toobe bu hello API anahtarı, bu sayfada gereken unutmayın.

Merhaba IPython Not tooa yeni hücreye üzerinden bu python kodu uygun toocopy olur.

Burada python kodu bir parçasını hello doğru API anahtarıyla gösteriyoruz.

![Python kodu](./media/machine-learning-data-science-process-hive-criteo-walkthrough/f8N4L4g.png)

Biz hello varsayılan API anahtarı bizim webservices'a 's API anahtarı ile değiştirilen unutmayın. Tıklatarak **çalıştırmak** dizüstü bilgisayar üzerinde bir IPython Bu hücrede yanıt aşağıdaki hello ortaya çıkarır:

![IPython yanıt](./media/machine-learning-data-science-process-hive-criteo-walkthrough/KSxmia2.png)

Merhaba için iki (Merhaba JSON framework hello python komut) biz sorulan hakkında örnekler test bkz, biz geri hello formunda "Scored etiketleri, Scored olasılıklar" cevaplar. Bu durumda, biz hello varsayılan değerleri hello önceden tamamlanmış kod seçtiğiniz Not (0'ların tüm sayısal sütunlar ve hello dize tüm kategorik sütunlar için "value") sağlar.

Bu bizim uçtan uca kılavuz gösteren sonucuna nasıl Azure Machine Learning kullanarak toohandle büyük ölçekli veri kümesi. Biz verilerin bir terabayt başlatıldı, bir tahmin modeli oluşturulan ve hello bulutta bir web hizmeti olarak dağıtılmış.

