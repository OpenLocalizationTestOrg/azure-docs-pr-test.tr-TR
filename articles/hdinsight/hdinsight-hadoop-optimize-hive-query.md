---
title: "aaaOptimize Hive sorguları Azure Hdınsight'ta | Microsoft Docs"
description: "Nasıl toooptimize için hdınsight'ta Hadoop, Hive sorguları hakkında bilgi edinin."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d6174c08-06aa-42ac-8e9b-8b8718d9978e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/26/2016
ms.author: jgao
ms.openlocfilehash: d27f8100e1e9f4823040ff9f693e7b78d6192c6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-hive-queries-in-azure-hdinsight"></a>Azure hdınsight'ta Hive sorguları en iyi duruma getirme

Varsayılan olarak, Hadoop kümeleri için performansı optimize edilmemiş. Bu makalede tooyour sorguları uygulayabilirsiniz bazı yaygın Hive performansı en iyi duruma getirme yöntemleri kapsar.

## <a name="scale-out-worker-nodes"></a>Çalışan düğümü ölçeklendirme

Kümedeki çalışan düğümü Hello sayısını artırmayı paralel olarak çalışan daha fazla mappers ve reducers toobe yararlanabilirsiniz. Hdınsight'ta ölçek genişletme artırabilirsiniz iki yolu vardır:

* Merhaba sağlama sırasında hello hello Azure portal, Azure PowerShell veya platformlar arası komut satırı arabirimi kullanarak çalışan düğümü sayısını belirtebilirsiniz.  Daha fazla bilgi için bkz. [HDInsight kümesi oluşturma](hdinsight-hadoop-provision-linux-clusters.md). Merhaba aşağıdaki ekran görüntüsü hello alt düğüm yapılandırması hello Azure portalı üzerinde gösterir:
  
    ![scaleout_1][image-hdi-optimize-hive-scaleout_1]
* Çalışma zamanı hello sırasında bir yeniden oluşturmadan ayrıca bir küme ölçeklendirebilirsiniz:

    ![scaleout_1][image-hdi-optimize-hive-scaleout_2]

Merhaba farklı sanal makinelerin Hdınsight tarafından desteklenen hakkında daha fazla bilgi için bkz: [Hdınsight fiyatlandırma](https://azure.microsoft.com/pricing/details/hdinsight/).

## <a name="enable-tez"></a>Tez etkinleştirme

[Apache Tez](http://hortonworks.com/hadoop/tez/) bir alternatif yürütme altyapısı toohello MapReduce altyapısıdır:

![tez_1][image-hdi-optimize-hive-tez_1]

Tez daha hızlı nedeni:

* **Yönlendirilmiş Çevrimsiz grafik (DAG) hello MapReduce Altyapısı'ndaki tek bir iş olarak çalıştırmak**. Merhaba DAG mappers toobe reducers bir kümesi tarafından izlenen her kümesi gerektirir. Bu, her bir Hive sorgusu için başlar birden çok MapReduce işleri toobe neden olur. Tez böyle kısıtlaması yok ve karmaşık DAG böylece iş başlangıç yükünü en aza bir iş olarak işleyebilir.
* **Gereksiz yazma önler**. Merhaba başlar toomultiple işleri nedeniyle hello MapReduce altyapısındaki her hello çıktısını aynı Hive sorgusu tooHDFS Ara verilerin yazılır. Tez her Hive sorgusu için iş sayısını en aza indirir olduğundan mümkün tooavoid gereksiz yazma kalır.
* **Başlangıç gecikmeleri en aza indirir**. Tez toostart ve ayrıca iyileştirme iyileştirme boyunca gereken mappers hello sayısını azaltarak daha iyi mümkün toominimize başlangıç gecikme olur.
* **Kapsayıcıları yeniden kullanır**. Olası Tez bu gecikme nedeniyle mümkün tooreuse kapsayıcıları tooensure olduğunda toostarting kapsayıcıları yukarı azalır.
* **Sürekli iyileştirme tekniklerini**. En iyi duruma getirme derleme aşamasında geleneksel olarak gerçekleştirilir. Merhaba girişleri hakkında daha fazla bilgi kullanılabilir ancak, çalışma zamanı sırasında daha iyi iyileştirme izin verir. Tez hello çalışma zamanı aşaması toooptimize hello daha fazla plan verir sürekli iyileştirme teknikleri kullanır.

Bu kavramlarla ilgili daha fazla ayrıntı için bkz: [Apache TEZ](http://hortonworks.com/hadoop/tez/).

Herhangi bir Hive sorgu hello ayarıyla aşağıdaki hello sorgu ekleyerek etkin Tez yapabilirsiniz:

    set hive.execution.engine=tez;

Linux tabanlı Hdınsight kümeleri varsayılan olarak etkin Tez sahip.


## <a name="hive-partitioning"></a>Bölümleme yığını

G/ç, Hive sorguları çalıştırmak için hello önemli performans düşüklüğü işlemdir. Merhaba performans geliştirilmiş hello toobe gereken veri miktarı olabilir okuyorsanız azalır. Varsayılan olarak, tüm Hive tabloları Hive sorguları tarayın. Tablo tarama gibi sorgular için harika bir seçenek budur. Ancak yalnızca tooscan çok küçük miktarda veri filtreleme ile (sorgular) Örneğin, gereken sorgular için bu davranış yükü gereksiz oluşturur. Hive bölümleme Hive tabloları Hive sorguları tooaccess yalnızca hello gerekli veri miktarını sağlar.

Hive bölümleme hello ham verileri yeni dizinlere hello bölüm hello kullanıcı tarafından tanımlandığı kendi dizini - sahip her bir bölümü ile yeniden düzenleme tarafından uygulanır. Merhaba Aşağıdaki diyagramda bir Hive tablosu hello sütuna göre bölümleme gösterilmektedir *yıl*. Her yıl için yeni bir dizin oluşturulur.

![Bölümlendirme][image-hdi-optimize-hive-partitioning_1]

Bölümleme bazı noktalar:

* **Bölüm altında yapmak** -yalnızca birkaç değerlerine sahip sütunlarda bölümleme birkaç bölümleri neden olabilir. Örneğin, cinsiyetiniz üzerinde bölümleme yalnızca (Erkek ve Kadın) oluşturulan iki bölüm toobe oluşturur, böylece yalnızca hello maksimum yarısı tarafından gecikmesini.
* **Değil bölüm yapmak** - Sihirbazın diğer uç Merhaba, benzersiz bir değer (örneğin, USERID) bir sütun üzerinde bölüm oluşturma birden çok bölüm neden olur. Toohandle hello çok sayıda dizinleri taşıdığından bölüm kadar stres hello küme iş üzerinde neden olur.
* **Veri eğme kaçının** -bile boyutu tüm bölümleri; böylece bölümleme anahtarınızı dikkatle seçin. Örneği üzerinde bölümleme *durumu* kayıtları California toobe altında hello sayısı yaklaşık 30 neden olabilir, Vermont toohello fark popülasyondaki son x.

toocreate bir bölüm tablosu kullanmak hello *bölümlenmiş tarafından* yan tümcesi:

    CREATE TABLE lineitem_part
        (L_ORDERKEY INT, L_PARTKEY INT, L_SUPPKEY INT,L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE            STRING, L_SHIPINSTRUCT STRING, L_SHIPMODE STRING,
         L_COMMENT STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    STORED AS TEXTFILE;

Merhaba bölümlenmiş tablo oluşturulduktan sonra statik bölümleme veya dinamik bölümleme ya da oluşturabilirsiniz.

* **Statik bölümleme** hello zaten parçalı veriler sahip anlamına gelir uygun dizinleri ve el ile Merhaba dizin konumuna göre Hive bölümleri sorabilirsiniz. Aşağıdaki kod parçacığını hello bir örnektir.
  
        INSERT OVERWRITE TABLE lineitem_part
        PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’)
        SELECT * FROM lineitem 
        WHERE lineitem.L_SHIPDATE = ‘5/23/1996 12:00:00 AM’
  
        ALTER TABLE lineitem_part ADD PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’))
        LOCATION ‘wasb://sampledata@ignitedemo.blob.core.windows.net/partitions/5_23_1996/'
* **Dinamik bölümleme** , Hive toocreate bölümleri otomatik olarak sizin için istediğiniz anlamına gelir. Hazırlama tablosuna hello tablosundan bölümleme hello zaten oluşturduk olduğundan, tüm toodo ihtiyacımız olan veri bölümlenmiş toohello Tablosu Ekle:
  
        SET hive.exec.dynamic.partition = true;
        SET hive.exec.dynamic.partition.mode = nonstrict;
        INSERT INTO TABLE lineitem_part
        PARTITION (L_SHIPDATE)
        SELECT L_ORDERKEY as L_ORDERKEY, L_PARTKEY as L_PARTKEY , 
             L_SUPPKEY as L_SUPPKEY, L_LINENUMBER as L_LINENUMBER,
              L_QUANTITY as L_QUANTITY, L_EXTENDEDPRICE as L_EXTENDEDPRICE,
             L_DISCOUNT as L_DISCOUNT, L_TAX as L_TAX, L_RETURNFLAG as           L_RETURNFLAG, L_LINESTATUS as L_LINESTATUS, L_SHIPDATE as           L_SHIPDATE_PS, L_COMMITDATE as L_COMMITDATE, L_RECEIPTDATE as      L_RECEIPTDATE, L_SHIPINSTRUCT as L_SHIPINSTRUCT, L_SHIPMODE as      L_SHIPMODE, L_COMMENT as L_COMMENT, L_SHIPDATE as L_SHIPDATE FROM lineitem;

Daha fazla ayrıntı için bkz: [bölümlenmiş tabloları](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).

## <a name="use-hello-orcfile-format"></a>Merhaba ORCFile biçimini kullanın
Hive farklı dosya biçimleri destekler. Örneğin:

* **Metin**: Bu hello varsayılan dosya biçimidir ve çoğu senaryoları ile çalışır
* **Avro**: birlikte çalışabilirlik senaryoları için iyi çalışır
* **ORC/Parquet**: performans için uygundur

ORC (en iyi duruma getirilmiş satır sütunlu), son derece verimli şekilde toostore Hive veri biçimidir. Karşılaştırılan tooother biçimleri, ORC hello aşağıdaki avantajları vardır:

* DateTime ve karmaşık ve yarı yapılandırılmış türleri gibi karmaşık türleri için destek
* too70% sıkıştırmayı ayarlama
* Satır atlanıyor izin her 10.000 satırları dizinler
* önemli bir düşüş, çalışma zamanı yürütme

tooenable ORC biçimi, önce oluşturduğunuz bir tablo hello yan tümcesiyle birlikte *ORC depolanan*:

    CREATE TABLE lineitem_orc_part
        (L_ORDERKEY INT, L_PARTKEY INT,L_SUPPKEY INT, L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE STRING,
         L_SHIPINSTRUCT STRING, L_SHIPMODE STRING, L_COMMENT      STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    STORED AS ORC;

Ardından, tablo hazırlama hello veri toohello ORC tablo ekleyin. Örneğin:

    INSERT INTO TABLE lineitem_orc
    SELECT L_ORDERKEY as L_ORDERKEY, 
           L_PARTKEY as L_PARTKEY , 
           L_SUPPKEY as L_SUPPKEY,
           L_LINENUMBER as L_LINENUMBER,
            L_QUANTITY as L_QUANTITY, 
           L_EXTENDEDPRICE as L_EXTENDEDPRICE,
           L_DISCOUNT as L_DISCOUNT,
           L_TAX as L_TAX,
           L_RETURNFLAG as L_RETURNFLAG,
           L_LINESTATUS as L_LINESTATUS,
           L_SHIPDATE as L_SHIPDATE,
           L_COMMITDATE as L_COMMITDATE,
           L_RECEIPTDATE as L_RECEIPTDATE, 
           L_SHIPINSTRUCT as L_SHIPINSTRUCT,
           L_SHIPMODE as L_SHIPMODE,
           L_COMMENT as L_COMMENT
    FROM lineitem;

Daha fazla bilgiyi hello ORC biçimi [burada](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).

## <a name="vectorization"></a>Vectorization

Vectorization Hive sağlayan bir defada bir satır işleme yerine 1024 toplu birlikte satırları tooprocess. Bu, daha az iç kod toorun gerektiğinden basit işlemleri daha hızlı yapılır anlamına gelir.

tooenable vectorization ayarı aşağıdaki hello ile Hive sorgunuzu öneki:

    set hive.vectorized.execution.enabled = true;

Daha fazla bilgi için bkz: [sorgu yürütme Vectorized](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).

## <a name="other-optimization-methods"></a>Diğer en iyi duruma getirme yöntemleri
Örneğin düşünebileceğiniz daha fazla en iyi duruma getirme yöntemi vardır:

* **Bucketing hive:** toocluster veya segment veri toooptimize sorgu performansını büyük kümeleri olanak sağlayan bir yöntem.
* **En iyi duruma getirme katılma:** tooimprove planlama Hive'nın sorgu yürütme en iyi duruma getirilmesi hello birleştirmeler verimliliğini ve kullanıcı ipuçları hello gereksinimini azaltır. Daha fazla bilgi için bkz: [katılma en iyi duruma getirme](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).
* **Reducers artırmak**.

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, birçok yaygın Hive sorgusu en iyi duruma getirme yöntemleri öğrendiniz. toolearn daha makaleler hello bakın:

* [Hdınsight'ta Apache Hive kullanma](hdinsight-use-hive.md)
* [Hdınsight'ta Hive kullanarak uçuş gecikme verilerini çözümleme](hdinsight-analyze-flight-delay-data.md)
* [Twitter verilerini hdınsight'ta Hive kullanma çözümleme](hdinsight-analyze-twitter-data.md)
* [Hdınsight'ta Hadoop Hive sorgusu konsol Hello kullanarak algılayıcı verilerini çözümleme](hdinsight-hive-analyze-sensor-data.md)
* [Web siteleri tooanalyze günlüklerinden Hdınsight ile Hive kullanma](hdinsight-hive-analyze-website-log.md)

[image-hdi-optimize-hive-scaleout_1]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_1.png
[image-hdi-optimize-hive-scaleout_2]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_2.png
[image-hdi-optimize-hive-tez_1]: ./media/hdinsight-hadoop-optimize-hive-query/tez_1.png
[image-hdi-optimize-hive-partitioning_1]: ./media/hdinsight-hadoop-optimize-hive-query/partitioning_1.png
