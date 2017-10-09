---
title: "Apache Hive ve HiveQL - Azure Hdınsight aaaWhat olan | Microsoft Docs"
description: "Apache Hive bir veri ambarı için Hadoop sistemidir. HiveQL, hangi benzer tooTransact SQL kullanarak kovanında depolanan verileri sorgulayabilir. Bu belgede, bilgi nasıl toouse Hive ve HiveQL Azure Hdınsight ile."
keywords: "hive, hadoop hiveql nedir hiveql toouse hive nasıl hive nedir hive öğrenin"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2c10f989-7636-41bf-b7f7-c4b67ec0814f
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: a2772312263895ff99b499898264c2e6d5e816e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-apache-hive-and-hiveql-on-azure-hdinsight"></a>Apache Hive ve HiveQL Azure hdınsight'ta nedir?

[Apache Hive](http://hive.apache.org/) Hadoop için veri ambarı sistemidir. Hive veri özetleme, sorgulama ve veri analizini sağlar. Hive sorguları bir sorgu dili benzer tooSQL olan HiveQL yazılır.

Hive büyük ölçüde yapılandırılmamış veriler üzerinde tooproject yapısı sağlar. Merhaba yapısı tanımladıktan sonra HiveQL tooquery hello verileri Java veya MapReduce bilgisi olmadan kullanabilirsiniz.

Hdınsight belirli iş yükleri için ayarlanmış birkaç küme türler sağlar. Küme türleri aşağıdaki hello Hive sorguları için en sık kullanılır:

* __Etkileşimli Hive__: sağlayan bir Hadoop kümesine [düşük gecikme süresi analitik işleme (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) işlevselliği tooimprove yanıt sürelerini etkileşimli sorgular. Daha fazla bilgi için bkz: Merhaba [etkileşimli hdınsight'ta Hive ile başlar](hdinsight-hadoop-use-interactive-hive.md) belge.

* __Hadoop__: toplu işlem iş yüklerini işlemek için ayarlanmış bir Hadoop kümesi. Daha fazla bilgi için bkz: Merhaba [Başlat hdınsight'ta Hadoop ile](hdinsight-hadoop-linux-tutorial-get-started.md) belge.

* __Spark__: Apache Spark Hive ile çalışmak için yerleşik bir işleve sahiptir. Daha fazla bilgi için bkz: Merhaba [hdınsight'ta Spark ile başlar](hdinsight-apache-spark-jupyter-spark-sql.md) belge.

* __HBase__: HiveQL HBase içinde depolanan kullanılan tooquery verileri olabilir. Daha fazla bilgi için bkz: Merhaba [hdınsight'ta HBase ile başlar](hdinsight-hbase-tutorial-get-started-linux.md) belge.

## <a name="how-toouse-hive"></a>Nasıl toouse yığını

Nasıl toouse Hdınsight ile Hive tablosu toodiscover aşağıdaki hello kullan:

| **Bu yöntemi kullanmak** isterseniz... | .. .an **etkileşimli** Kabuk | ... **toplu** işleme | .. hemen bu **küme işletim sistemi** | .. .from bu **istemci işletim sistemi** |
|:--- |:---:|:---:|:--- |:--- |
| [Hive görünümü](hdinsight-hadoop-use-hive-ambari-view.md) |✔ |✔ |Linux |(Herhangi bir tarayıcı tabanlı) |
| [Beeline istemci](hdinsight-hadoop-use-hive-beeline.md) |✔ |✔ |Linux |Linux, UNIX, Mac OS X veya Windows |
| [REST API](hdinsight-hadoop-use-hive-curl.md) |&nbsp; |✔ |Linux veya Windows * |Linux, UNIX, Mac OS X veya Windows |
| [Visual Studio için Hdınsight araçları](hdinsight-hadoop-use-hive-visual-studio.md) |&nbsp; |✔ |Linux veya Windows * |Windows |
| [Windows PowerShell](hdinsight-hadoop-use-hive-powershell.md) |&nbsp; |✔ |Linux veya Windows * |Windows |

> [!IMPORTANT]
> \*Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Bir Windows tabanlı Hdınsight kümesi kullanıyorsanız, hello kullanabilirsiniz [sorgu konsol](hdinsight-hadoop-use-hive-query-console.md) tarayıcınızdan veya [Uzak Masaüstü](hdinsight-hadoop-use-hive-remote-desktop.md) toorun Hive sorguları.

## <a name="hiveql-language-reference"></a>HiveQL dil başvurusu

HiveQL dil başvurusu hello kullanılabilir [dil el ile (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).

## <a name="hive-and-data-structure"></a>Hive ve veri yapısı

Hive nasıl toowork ile yapılandırılmış ve yarı yapılandırılmış veri bilir. Merhaba alanlar belirli karakterleriyle burada sınırlandırılmıştır Örneğin, metin dosyaları. Aşağıdaki HiveQL ifadeyi hello boşlukla ayrılmış veriler üzerinde bir tablo oluşturur:

```hiveql
CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
STORED AS TEXTFILE LOCATION '/example/data/';
```

Hive ayrıca özel destekler **seri hale getirici/deserializers (SerDe)** karmaşık veya düzensiz yapılandırılmış veriler için. Daha fazla bilgi için bkz: Merhaba [nasıl toouse Hdınsight ile özel bir JSON SerDe](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) belge.

Merhaba Hive tarafından desteklenen dosya biçimleri hakkında daha fazla bilgi için bkz: [dil el ile (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)

## <a name="hive-internal-tables-vs-external-tables"></a>İç tablolar vs dış tablolara yığını

Hive ile oluşturabileceğiniz tablolar iki tür vardır:

* __İç__: veri hello Hive veri ambarında depolanır. Merhaba veri ambarı bulunur `/hive/warehouse/` hello varsayılan depolama hello kümesi için.

    İç kullanım ne zaman tabloları:

    * Veri geçicidir.
    * Hive toomanage hello yaşam döngüsü hello tablo ve veri istiyor.

* __Dış__: dışında hello veri ambarında depolanır. Merhaba veri herhangi bir depolama alanı üzerinde erişilebilir hello küme tarafından depolanabilir.

    Kullanım dış tablolar:

    * Merhaba verileri de Hive dışında kullanılır. Örneğin, hello veri dosyaları (Merhaba dosyaları kilit yok.) başka bir işlem tarafından güncelleştirilir
    * Verilerin bile hello tablo bırakarak sonra konum, temel alınan hello tooremain gerekir.
    * Varsayılan olmayan depolama hesabı gibi özel bir konuma gerekir.
    * Hive dışında bir program hello veri biçimi, konum vb. yönetir.

Merhaba daha fazla bilgi için bkz: [Hive iç ve dış tablolar giriş] [ cindygross-hive-tables] blog postası.

## <a name="user-defined-functions-udf"></a>Kullanıcı tanımlı işlevler (UDF)

Hive ayrıca uzatabilirsiniz aracılığıyla **kullanıcı tanımlı işlevler (UDF)**. Bir UDF tooimplement işlev veya HiveQL içinde kolayca modellenir değil mantığı sağlar. UDF'ler ile Hive kullanma örneği için aşağıdaki belgeleri hello bakın:

* [Kullanıcı tanımlı bir Java işlev ile Hive kullanma](hdinsight-hadoop-hive-java-udf.md)

* [Kullanıcı tanımlı bir Python işlev Hive veya Pig kullanın](hdinsight-python.md)

* [C# kullanıcı tanımlı bir işlev Hive veya Pig kullanın](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [Nasıl tooadd özel Hive kullanıcı tanımlı işlev tooHDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

* [Bir örnek Hive kullanıcı tanımlı işlev tooconvert tarih/saat tooHive zaman damgası biçimleri](https://github.com/Azure-Samples/hdinsight-java-hive-udf)

## <a id="data"></a>Örnek veri

Hdınsight'ta Hive gelen önceden yüklenmiş bir iç tablosu adlı `hivesampletable`. Hdınsight ile Hive kullanılabilir bir örnek veri kümeleri de sağlar. Bu veri kümeleri hello depolanan `/example/data` ve `/HdiSamples` dizinleri. Bu dizinleri, kümeniz için hello varsayılan depolama yok.

## <a id="job"></a>Örnek Hive sorgusu

Aşağıdaki HiveQL ifadelerini proje sütunları hello üzerine hello `/example/data/sample.log` dosyası:

    set hive.execution.engine=tez;
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

Hello önceki örnekte, hello HiveQL ifadelerini hello aşağıdaki eylemleri gerçekleştirin:

* `set hive.execution.engine=tez;`: Kümeleri yürütme altyapısı toouse Tez hello. Tez yerine MapReduce kullanarak sorgu performansı bir artış sağlayabilir. Tez hakkında daha fazla bilgi için bkz: Merhaba [iyileştirilmiş performans için Apache Tez kullanma](#usetez) bölümü.

    > [!NOTE]
    > Bu deyim yalnızca olan Windows tabanlı Hdınsight kümesi kullanılırken gereklidir. Tez hello varsayılan yürütme Linux tabanlı Hdınsight için altyapısıdır.

* `DROP TABLE`: Hello tablo zaten varsa dosyayı silin.

* `CREATE EXTERNAL TABLE`: Oluşturur Yeni bir **dış** Hive tablo. Dış tablolara hello tablo tanımı kovanında yalnızca depolar. Merhaba veri hello özgün konumuna hem de hello özgün biçiminde bırakılır.

* `ROW FORMAT`: Hello verilerin nasıl biçimlendirilmiş Hive söyler. Bu durumda, her günlüğün içinde hello alanlar boşlukla ayrılır.

* `STORED AS TEXTFILE LOCATION`: Hive hello burada verilerin depolandığı söyler (Merhaba `example/data` dizini) ve metin olarak depolanır. Merhaba verileri, bir dosyada yer veya hello dizini içindeki birden çok dosya üzerinden yayılan.

* `SELECT`: Tüm satırların sayımını hello burada seçer sütun **t4** hello değeri içeren **[Hata]**. Bu ifade değerini döndürür **3** çünkü bu değer içeren üç satır vardır.

* `INPUT__FILE__NAME LIKE '%.log'`-Hive tooapply hello şema tooall dosyaları hello dizininde çalışır. Bu durumda, başlangıç dizini hello şema eşleşmiyor dosyalarını içerir. tooprevent çöp veriler hello sonuçlarında, bu bildirimi bildirir Hive biz yalnızca veri biten dosyalarından döndürmesi gerektiğini. günlük.

> [!NOTE]
> Dış kaynak tarafından güncelleştirilmiş hello temel alınan veri toobe beklediğiniz dış tablolara kullanılmalıdır. Örneğin, bir otomatik veri karşıya yükleme işlemi veya MapReduce işlemi.
>
> Bir dış tablo bırakma mu **değil** hello verilerini silmek yalnızca hello tablosu tanımını siler.

toocreate bir **iç** tablo dış yerine, aşağıdaki HiveQL hello kullanın:

    set hive.execution.engine=tez;
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs
    SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';

Bu deyimler hello aşağıdaki eylemleri gerçekleştirin:

* `CREATE TABLE IF NOT EXISTS`: Hello tablo mevcut değilse oluşturun. Çünkü hello **dış** anahtar sözcüğü kullanılmaz, bu deyim bir iç tablosu oluşturur. Hello tablo hello Hive veri ambarında depolanır ve tamamen Hive tarafından yönetilir.

* `STORED AS ORC`: En iyi duruma getirilmiş satır sütunlu (ORC) biçiminde hello verileri depolar. ORC Hive verilerini depolamak için yüksek oranda en iyi duruma getirilmiş ve verimli bir biçimidir.

* `INSERT OVERWRITE ... SELECT`: Hello satırları seçer **log4jLogs** içeren tablo **[Hata]**, ve ardından ekler veri hello hello **günlüklerini** tablo.

> [!NOTE]
> Dış tablolara, bir iç tablosu bırakarak hello temel verilerini siler.

## <a name="improve-hive-query-performance"></a>Hive sorgu performansı

### <a id="usetez"></a>Apache Tez

[Apache Tez](http://tez.apache.org) Hive, ölçekte daha verimli bir şekilde toorun gibi veri yoğun uygulamalar sağlayan bir çerçevedir. Tez Linux tabanlı Hdınsight kümeleri için varsayılan olarak etkindir.

> [!NOTE]
> Tez şu anda Windows tabanlı Hdınsight kümeleri için varsayılan olarak kapalıdır ve etkinleştirilmesi gerekir. Tez, aşağıdaki değeri hello tootake avantajlarından bir Hive sorgusu için ayarlamanız gerekir:
>
> `set hive.execution.engine=tez;`
>
> Tez hello varsayılan Linux tabanlı Hdınsight kümeleri altyapısıdır.

Merhaba [Hive Tez tasarım belgeleri](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) hello uygulama seçeneklerine ve ayarlama yapılandırmalar hakkında ayrıntılar içerir.

işlerini hata tooaid Tez kullanılarak çalıştırıldı, Hdınsight Tez işlerinde tooview ayrıntılarını izin web Uı'lar aşağıdaki hello sağlar:

* [Merhaba Linux tabanlı Hdınsight Ambari Tez görünümünde kullanın](hdinsight-debug-ambari-tez-view.md)

* [Windows tabanlı Hdınsight üzerinde Hello Tez UI kullanın](hdinsight-debug-tez-ui.md)

### <a name="low-latency-analytical-processing-llap"></a>Düşük gecikme süresi analitik işleme (LLAP)

[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (Canlı uzun ve işlem da bilinir) Hive sorguları bellek içi önbelleğe alma veren 2.0 yeni bir özelliktir. LLAP yapar yukarı daha hızlı Hive sorguları çok[26 x bazı durumlarda 1.x Hive çok hızlı](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).

Hdınsight LLAP hello etkileşimli Hive küme türü sağlar. Merhaba daha fazla bilgi için bkz: [Başlat ile etkileşimli Hive](hdinsight-hadoop-use-interactive-hive.md) belge.

## <a name="hive-jobs-and-sql-server-integration-services"></a>Hive işleri ve SQL Server Integration Services

SQL Server Integration Services (SSIS) toorun Hive işi kullanabilirsiniz. Hello Azure Feature Pack SSIS için Hdınsight'ta Hive işlerle çalışma bileşenleri aşağıdaki hello sağlar.

* [Azure Hdınsight Hive görevi][hivetask]

* [Azure aboneliği Bağlantı Yöneticisi][connectionmanager]

Hello Azure Feature Pack hakkında daha fazla bilgi için SSIS [burada][ssispack].

## <a id="nextsteps"></a>Sonraki adımlar

Artık Hive nedir öğrendiğinize göre ve nasıl diğer yolları toowork Azure Hdınsight ile aşağıdaki kullanım hello hdınsight'ta Hadoop ile bağlantı tooexplore toouse.

* [Veri tooHDInsight karşıya yükle][hdinsight-upload-data]
* [HDInsight ile Pig kullanma][hdinsight-use-pig]
* [Hdınsight ile MapReduce işleri kullanma][hdinsight-use-mapreduce]

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/
[hivetask]: http://msdn.microsoft.com/library/mt146771(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx

[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md


[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx
