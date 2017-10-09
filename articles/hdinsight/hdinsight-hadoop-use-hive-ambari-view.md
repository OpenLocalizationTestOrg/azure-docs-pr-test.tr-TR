---
title: "hdınsight'ta (Hadoop) - Azure Hive ile aaaUse Ambari görünümleri toowork | Microsoft Docs"
description: "Nasıl toouse hello Hive görünümü, web tarayıcısı toosubmit Hive sorgularının öğrenin. Merhaba Hive görünümü Ambari Web kullanıcı Arabirimi ile Linux tabanlı Hdınsight kümenizi sağlanan hello bir parçasıdır."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1abe9104-f4b2-41b9-9161-abbc43de8294
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: f9a77b652e70d34a0ff9165fbb8c2e16d3401ae0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-hive-view-with-hadoop-in-hdinsight"></a>Hdınsight'ta Hadoop ile Hive görünümü Hello kullanın

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Ambari Hive görünümünü kullanarak nasıl toorun Hive sorguları hakkında bilgi edinin. Ambari, yönetim ve izleme yardımcı programı Linux tabanlı Hdınsight kümeleri ile sağlanan ' dir. Ambari sağlanan hello özellikleri kullanılan toorun Hive sorguları olabilecek UI biridir.

> [!NOTE]
> Ambari, bu belgede ele alınan değil birçok özellikleri vardır. Daha fazla bilgi için bkz: [Hdınsight kümelerini yönetme hello Ambari Web kullanıcı arabirimini kullanarak](hdinsight-hadoop-manage-ambari.md).

## <a name="prerequisites"></a>Ön koşullar

* Linux tabanlı Hdınsight kümesi. Küme oluşturma hakkında daha fazla bilgi için bkz: [Linux tabanlı Hdınsight kullanmaya başlama](hdinsight-hadoop-linux-tutorial-get-started.md).

> [!IMPORTANT]
> Bu belgedeki Hello adımlar Linux kullanan bir Hdınsight kümesi gerektirir. Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="open-hello-hive-view"></a>Merhaba Hive görünümü Aç

Ambari görünümleri hello Azure portal ' olabilir; Hdınsight kümenize seçin ve ardından **Ambari görünümleri** hello gelen **hızlı bağlantılar** bölümü.

![Merhaba portalı hızlı bağlantılar bölümü](./media/hdinsight-hadoop-use-hive-ambari-view/quicklinks.png)

Merhaba görünümlerinin hello listesinden __Hive görünümü__.

![Merhaba seçilen Hive görünümü](./media/hdinsight-hadoop-use-hive-ambari-view/select-hive-view.png)

> [!NOTE]
> Ambari erişmek için istendiğinde tooauthenticate toohello site olur. Hello Yöneticisi girin (varsayılan `admin`) hesap adı ve parola oluştururken kullandığınız küme hello.

Aşağıdaki görüntü bir sayfa benzer toohello görmeniz gerekir:

![Merhaba Hive görünümü için hello sorgu çalışma sayfası görüntüsü](./media/hdinsight-hadoop-use-hive-ambari-view/ambari-hive-view.png)

## <a name="hivequery"></a>Sorgu çalıştırma

toorun bir hive sorgusu hello hello Hive görünümünü aşağıdaki adımları kullanın.

1. Merhaba gelen __sorgu__ sekmesinde, HiveQL ifadelerini hello çalışma sayfasına aşağıdaki hello yapıştırın:

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS cnt FROM log4jLogs WHERE t4 = '[ERROR]' GROUP BY t4;
    ```

    Bu deyimler hello aşağıdaki eylemleri gerçekleştirin:

   * `DROP TABLE`-Hello tablo ve hello veri dosyası siler hello tablo zaten mevcut durumda.

   * `CREATE EXTERNAL TABLE`-Kovanında yeni bir "dış" tablo oluşturur.
   Dış tablolara yalnızca hello tablo tanımı kovanında depolar. Merhaba veri hello özgün konumda kalır.

   * `ROW FORMAT`-Nasıl hello veri biçimlendirilir. Bu durumda, her günlüğün içinde hello alanlar boşlukla ayrılır.

   * `STORED AS TEXTFILE LOCATION`-Hello verilerin depolandığı ve metin olarak depolanır.

   * `SELECT`-Hello değer [Hata], sütun t4 içerdiği tüm satırların sayımını seçer.

     > [!NOTE]
     > Dış kaynak tarafından güncelleştirilmiş hello temel alınan veri toobe beklediğiniz dış tablolara kullanılmalıdır. Örneğin, bir otomatik veri karşıya yükleme işlem, veya başka bir MapReduce işlemi tarafından. Bir dış tablo bırakma mu *değil* hello verileri, yalnızca hello tablo tanımını silin.

    > [!IMPORTANT]
    > Merhaba bırakın __veritabanı__ seçimi daha __varsayılan__. Bu belgedeki örneklerde Hello Hdınsight ile dahil hello varsayılan veritabanı kullanın.

2. toostart hello sorgu, kullanım hello **yürütme** hello çalışma aşağıdaki düğmesine. Turuncu ve hello metin değişiklikleri çok renge**durdurmak**.

3. Merhaba sorgu tamamladığında hello **sonuçları** sekmesi hello işlemi hello sonuçlarını görüntüler. metin aşağıdaki hello hello hello sorgu sonucudur:

        sev       cnt
        [ERROR]   3

    Merhaba **günlükleri** sekmesini hello işlem tarafından oluşturulan kullanılan tooview hello günlük bilgileri olabilir.

   > [!TIP]
   > Merhaba **sonuçları kaydetmek** açılan iletişim kutusunda hello üst sol Merhaba **sorgu işleminin sonuçları** bölüm sonuçları kaydetmek veya toodownload sağlar.

4. Select hello ilk dört satırı bu sorgu ardından **yürütme**. Merhaba işi tamamlandığında sonuç olduğuna dikkat edin. Hello kullanarak **yürütme** düğmesinin hello sorgu parçası olduğunda çalışır seçili deyimleri hello yalnızca seçili. Bu durumda, hello seçimi hello tablosundan satır alır hello son deyimini eklemediniz. Yalnızca bu satırı seçin ve kullanırsanız **yürütme**, beklenen hello sonuçları görmeniz gerekir.

5. tooadd bir çalışma kullanmak hello **yeni çalışma sayfası** düğmesi hello hello sonundaki **sorgu Düzenleyicisi'ni**. Merhaba yeni çalışma sayfasında, aşağıdaki HiveQL ifadelerini hello girin:

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';
    ```

  Bu deyimler hello aşağıdaki eylemleri gerçekleştirin:

   * **Tablo IF değil var oluşturmak** -zaten yoksa, bir tablo oluşturur. Merhaba itibaren **dış** anahtar sözcüğü kullanılmaz, bir iç tablosu oluşturulur. Bir iç tablosu hello Hive veri ambarında depolanır ve tamamen Hive tarafından yönetilir. Dış tablolara, bir iç tablosu bırakarak hello temel alınan veri de siler.

   * **AS ORC DEPOLANAN** -en iyi duruma getirilmiş satır sütunlu (ORC) biçiminde hello verileri depolar. ORC Hive verilerini depolamak için yüksek oranda en iyi duruma getirilmiş ve verimli bir biçimidir.

   * **INSERT ÜZERİNE... SEÇİN** -hello satırları seçer **log4jLogs** içeren tablo `[ERROR]`, ve ardından ekler veri hello hello **günlüklerini** tablo.

     Kullanım hello **yürütme** toorun bu sorguyu düğmesine tıklayın. Merhaba **sonuçları** sekmesini hello sorgu sıfır satır geri döndüğünde herhangi bir bilgi içermiyor. Hello durumunu göster olarak **başarılı** hello sorgu işlemi tamamlandıktan sonra.

### <a name="visual-explain"></a>Visual açıklanmaktadır

toodisplay hello sorgu planı, select hello görselleştirmesini **Visual açıklayan** sekmenin hello çalışma altında.

Merhaba **Visual açıklayan** hello sorgu görünümünü karmaşık sorgular hello akışını anlamak yararlı olabilir. Bu görünüm metinsel denk hello kullanarak görüntüleyebileceğiniz **açıklama** hello sorgu Düzenleyicisi'ni düğmesini.

### <a name="tez-ui"></a>Tez kullanıcı Arabirimi

toodisplay hello Tez UI hello sorgu select hello **Tez** sekmenin hello çalışma altında.

> [!IMPORTANT]
> Tez kullanılmaz tooresolve tüm sorgudur. Çok sayıda sorgu, Tez kullanmadan çözülebilir. 

Tez kullanılan tooresolve hello sorgu olduysa, hello yönlendirilmiş Çevrimsiz grafik (DAG) görüntülenir. Tez işlem olduğunuz çalıştırdı hello geçmiş ya da hata ayıklama sorguları hello için tooview hello DAG istiyorsanız, hello kullanın [Tez Görünüm](hdinsight-debug-ambari-tez-view.md) yerine.

## <a name="view-job-history"></a>İş geçmişini görüntüleme

Merhaba __işleri__ sekmesi Hive sorguları geçmişini görüntüler.

![Merhaba iş geçmişi görüntüsü](./media/hdinsight-hadoop-use-hive-ambari-view/job-history.png)

## <a name="database-tables"></a>Veritabanı tabloları

Merhaba kullanabilirsiniz __tabloları__ toowork Hive veritabanındaki tablolarla sekmesinde.

![Merhaba tablolar sekmesini görüntüsü](./media/hdinsight-hadoop-use-hive-ambari-view/tables.png)

## <a name="saved-queries"></a>Kaydedilmiş sorguları

Merhaba sorgu sekmesinden sorguları isteğe bağlı olarak kaydedebilirsiniz. Kaydedildikten sonra hello hello sorgudan yeniden __kaydedilen sorguları__ sekmesi.

![Kaydedilen sorgular sekmesini görüntüsü](./media/hdinsight-hadoop-use-hive-ambari-view/saved-queries.png)

## <a name="user-defined-functions"></a>Kullanıcı tanımlı işlevler

Hive, kullanıcı tanımlı işlevler (UDF) da genişletilebilir. Bir UDF tooimplement işlev veya HiveQL içinde kolayca modellenir değil mantığı sağlar.

Merhaba UDF sekmesini hello Hive görünümü hello üstündeki toodeclare sağlar ve UDF'ler kümesi kaydedin. Bu UDF'ler ile Merhaba kullanılabilir **sorgu Düzenleyicisi'ni**.

![UDF sekmesini görüntüsü](./media/hdinsight-hadoop-use-hive-ambari-view/user-defined-functions.png)

UDF toohello Hive görünümü ekledikten sonra bir **Ekle UDF'ler** düğmesi görünür hello hello altındaki **sorgu Düzenleyicisi'ni**. Bu girdi seçerek hello hello Hive görünümü tanımlı UDF'ler açılan listesini görüntüler. Bir UDF seçerek HiveQL ifadelerini tooyour sorgu tooenable hello UDF ekler.

Örneğin, aşağıdaki özelliklere hello ile bir UDF tanımladıysanız:

* Kaynak adı: myudfs

* Kaynak yol: /myudfs.jar

* UDF ad: myawesomeudf

* UDF sınıf adı: com.myudfs.Awesome

Hello kullanarak **Ekle UDF'ler** düğmesi görüntüler adlı bir girdi **myudfs**, başka bir açılan her UDF bu kaynak için tanımlanan için. Bu durumda, **myawesomeudf**. Bu girdi seçerek hello sorgu toohello başlangıcını izleyen hello ekler:

```hiveql
add jar /myudfs.jar;
create temporary function myawesomeudf as 'com.myudfs.Awesome';
```

Daha sonra sorgunuzu hello UDF kullanabilirsiniz. Örneğin, `SELECT myawesomeudf(name) FROM people;`.

UDF'ler hdınsight'ta Hive kullanma hakkında daha fazla bilgi için aşağıdaki belgeleri hello bakın:

* [Hive veya Pig hdınsight'ta Python kullanarak](hdinsight-python.md)
* [Nasıl tooadd özel bir Hive UDF tooHDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

## <a name="hive-settings"></a>Hive ayarları

Ayarları can kullanılan toochange çeşitli Hive ayarları olabilir. Örneğin, hello yürütme alt yapısı için Hive Tez (Merhaba varsayılan) tooMapReduce değiştirme.

## <a id="nextsteps"></a>Sonraki adımlar

Hdınsight'ta Hive hakkında genel bilgi için:

* [Hdınsight'ta Hadoop ile Hive kullanma](hdinsight-use-hive.md)

Diğer yöntemler hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:

* [Hdınsight'ta Hadoop ile pig kullanma](hdinsight-use-pig.md)
* [Hdınsight'ta Hadoop ile MapReduce kullanma](hdinsight-use-mapreduce.md)
