---
title: "aaaWhat Hdınsight, hello Hadoop teknoloji yığınının & kümeleri misiniz? - Azure | Microsoft Docs"
description: "Bir giriş tooHDInsight ve hello Hadoop teknoloji yığınının ve bileşenleri, Spark, Kafka, Hive, HBase büyük veri analizi için de dahil olmak üzere."
keywords: "Azure hadoop, hadoop azure, hadoop giriş, hadoop giriş, hadoop teknoloji yığınının, giriş toohadoop, hadoop kümesi nedir bir hadoop kümesine nedir giriş toohadoop hadoop ne için kullanılır"
services: hdinsight
documentationcenter: 
author: cjgronlund
manager: jhubbard
editor: cgronlun
ms.assetid: e56a396a-1b39-43e0-b543-f2dee5b8dd3a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: cgronlun
ms.openlocfilehash: 0aed3d1a6cf3c0cdc3b036cfa4865a2e0b58e2c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-hdinsight-hello-hadoop-technology-stack-and-hadoop-clusters"></a>Giriş tooAzure Hdınsight, hello Hadoop teknoloji yığınının ve Hadoop kümeleri
 Bu makalede, Hdınsight, bir giriş tooAzure hello Hadoop teknoloji yığınının bir bulut dağıtımını sağlar. Hadoop kümelerinin ne olduğu ve ne zaman kullanılacağı da ele alınmaktadır. 

## <a name="what-is-hdinsight-and-hello-hadoop-technology-stack"></a>Hdınsight ve hello Hadoop teknoloji yığınının nedir? 
Azure Hdınsight olan bir bulut dağıtımını hello hello Hadoop bileşenleri [Hortonworks veri Platformu (HDP)](https://hortonworks.com/products/data-center/hdp/). [Apache Hadoop](http://hadoop.apache.org/) hello özgün açık kaynak framework dağıtılan işleme ve büyük veri kümelerinin bilgisayar kümelerinde analiz edildi. 


Merhaba Hadoop teknoloji yığınının ilgili yazılım ve Apache Hive, HBase, Spark, Kafka ve diğer birçok dahil olmak üzere yardımcı programları içerir. bkz: toosee kullanılabilir Hadoop teknoloji yığınının bileşenleri, hdınsight'ta [bileşenleri ve Hdınsight ile kullanılabilir sürümlerini][component-versioning]. tooread, hdınsight'ta Hadoop hakkında daha fazla bilgi görmek hello [Azure Özellikleri Sayfası Hdınsight için](https://azure.microsoft.com/services/hdinsight/).

## <a name="what-is-a-hadoop-cluster-and-when-do-you-use-it"></a>Hadoop kümesi nedir ve ne zaman kullanılır?
Ayrıca *Hadoop* bir küme türü olarak şunlara da sahiptir:

* İş zamanlama ve kaynak yönetimi için YARN
* Paralel işleme için MapReduce
* Merhaba Hadoop dağıtılmış dosya sistemi (HDFS)
  
Hadoop kümelerinin en sık kullanıldığı senaryo, depolanan verilerin toplu olarak işlenmesidir. HDInsight’taki diğer küme türlerinin ek özellikleri vardır: Hızlı bellek içi işleme özelliği sayesinde Spark'ın popülerliği artmıştır. Ayrıntılı bilgi edinmek için bkz. [HDInsight’taki küme türleri](#overview).

## <a name="what-is-big-data"></a>Büyük veri nedir?
Büyük veri, aşağıdakiler gibi herhangi bir büyük dijital bilgi kütlesini ifade eder:

* Endüstriyel ekipmanlardan toplanan algılayıcı verileri
* Web sitesinden toplanan müşteri etkinliği verileri
* Twitter haber akışı

Büyük veri, artan miktarlarda, yükselen hızlarda ve artan çeşitlilikteki biçimlerde toplanır. (Depolanan geçmiş anlamına gelir) veya gerçek zamanlı (Merhaba kaynağından akışı anlamına gelir) olabilir. 

## <a name="overview"></a>HDInsight’taki küme türleri
HDInsight belirli küme türlerinin yanı sıra bileşen, yardımcı program ve dil ekleme gibi küme özelleştirme özelliklerini de içerir.

### <a name="spark-kafka-interactive-hive-hbase-customized-and-other-cluster-types"></a>Spark, Kafka, Interactive Hive, HBase, özelleştirilmiş ve diğer küme türleri
Hdınsight küme türleri aşağıdaki hello sunar:

* **[Apache Hadoop](https://wiki.apache.org/hadoop)**: kullanan [HDFS](#hdfs), [YARN](#yarn) kaynak yönetimi ve basit bir [MapReduce](#mapreduce) programlama modeli tooprocess ve Toplu veri paralel analiz edin.
* **[Apache Spark](http://spark.apache.org/)**: bellek içi işleme tooboost hello büyük veri analizi uygulamalarının performansını destekleyen paralel bir işleme altyapısı SQL akış verileri için Spark işlerinin ve machine learning. Bkz. [HDInsight’ta Apache Spark nedir?](hdinsight-apache-spark-overview.md)
* **[Apache HBase](http://hbase.apache.org/)**: Büyük miktarlarda yapılandırmamış ve yarı yapılandırılmış veriler (potansiyel olarak milyarlarca satır çarpı milyonlarca sütun) için rastgele erişim ve güçlü tutarlılık özellikleri sağlayan Hadoop'u temel alan bir NoSQL veritabanı. Bkz. [HDInsight'ta HBase nedir?](hdinsight-hbase-overview.md)
* **[Microsoft R Server](https://msdn.microsoft.com/microsoft-r/rserver)**: Paralel ve dağıtılmış R işlemlerini barındırmak ve yönetmek için bir sunucu. Bu veri bilimcilerine ve istatistikçiler R programcıları isteğe bağlı erişim tooscalable, hdınsight'ta analytics dağıtılmış yöntemleri sağlar. Bkz. [HDInsight'ta R Server'a genel bakış](hdinsight-hadoop-r-server-overview.md).
* **[Apache Storm](https://storm.incubator.apache.org/)**: Büyük veri akışlarını hızlı şekilde işlemek için dağıtılmış, gerçek zamanlı bir işlem sistemi. Storm HDInsight’ta yönetilen küme olarak sunulur. Bkz. [Storm ve Hadoop kullanarak gerçek zamanlı algılayıcı verilerini çözümleme](hdinsight-storm-sensor-data-analysis.md).
* **[Apache Interactive Hive önizleme (diğer adı: Live Long and Process)](https://cwiki.apache.org/confluence/display/Hive/LLAP)**: Etkileşimli ve daha hızlı Hive sorguları için bellek içi önbelleğe alma. Bkz. [HDInsight'ta Interactive Hive kullanımı](hdinsight-hadoop-use-interactive-hive.md).
* **[Apache Kafka](https://kafka.apache.org/)**: Akış verisi işlem hatları ve uygulamaları oluşturmak için kullanılan açık kaynak platform. Kafka, ayrıca, toopublish sağlar ve toodata akışları abone ileti sırası işlevsellik sağlar. Bkz: [giriş tooApache hdınsight'ta Kafka](hdinsight-apache-kafka-introduction.md).

Kümeleri hello aşağıdaki yöntemleri kullanarak da yapılandırabilirsiniz:
* **[Etki alanına katılmış kümeleri Önizleme](hdinsight-domain-joined-introduction.md)**: erişimi denetlemek ve veriler için yöneyim sağlamak için bir küme tooan Active Directory etki alanına katıldı.
* **[Betik eylemlerine sahip özel kümeler](hdinsight-hadoop-customize-cluster-linux.md)**: Ek bileşenlerin sağlanması ve yüklenmesi sırasında çalıştırılan betiklere sahip kümeler.

### <a name="example-cluster-customization-scripts"></a>Örnek küme özelleştirme betikleri
Komut dosyası, küme hazırlama sırasında çalıştıran ve kullanılan tooinstall hello kümede ek bileşenleri olabilir Bash betiklerini Linux'ta eylemlerdir. 

Merhaba aşağıdaki örnek betikler hello Hdınsight ekibi tarafından sağlanmıştır:

* **[Hue](hdinsight-hadoop-hue-linux.md)**: bir küme ile web uygulamaları kullanılan toointeract bir dizi. Yalnızca Linux kümeleri.
* **[Giraph](hdinsight-hadoop-giraph-install-linux.md)**: grafik öğeler veya kişiler arasındaki ilişkileri toomodel işleme.
* **[Solr](hdinsight-hadoop-solr-install-linux.md)**: Verilerde tam metin arama yapma olanağı sağlayan kurumsal ölçekte bir arama platformu.

Kendi Betik Eylemlerinizi geliştirme hakkında daha fazla bilgi için bkz. [HDInsight ile Betik Eylemi geliştirme](hdinsight-hadoop-script-actions-linux.md).

## <a name="components-and-utilities-on-hdinsight-clusters"></a>HDInsight kümelerindeki bileşenler ve yardımcı programlar
Merhaba aşağıdaki bileşenler ve yardımcı programları Hdınsight kümelerine dahil edilmiştir:

* **[Ambari](#ambari)**: Küme hazırlama, yönetim, izleme ve yardımcı programları.
* **[Avro](#avro)**  (Avro için Microsoft .NET kitaplığı): hello Microsoft .NET ortamı için veri seri hale getirme. 
* **[Hive & HCatalog](#hive)**: Yapılandırılmış Sorgu Dili (SQL) benzeri sorgulama ile bir tablo ve depolama yönetimi katmanı.
* **[Mahout](#mahout)**: Ölçeklenebilir makine öğrenme uygulamaları için.
* **[MapReduce](#mapreduce)**: Hadoop dağıtılan işleme ve kaynak yönetimi için eski altyapı. Bkz. [YARN](#yarn).
* **[Oozie](#oozie)**: İş akışı yönetimi.
* **[Phoenix](#phoenix)**: HBase üzerinde ilişkisel veritabanı katmanı.
* **[Pig](#pig)**: MapReduce dönüştürmeleri için daha basit betik oluşturma.
* **[Sqoop](#sqoop)**: Verileri içeri ve dışarı aktarma.
* **[Tez](#tez)**: veri kullanımı yoğun işlemlerin toorun verimli bir şekilde ölçekli olarak sağlar.
* **[YARN](#yarn)**: Merhaba Hadoop çekirdek kitaplığı parçası olan kaynak yönetimi.
* **[ZooKeeper](#zookeeper)**: Dağıtılmış sistemlerdeki süreçlerin koordinasyonu.

> [!NOTE]
> Merhaba belirli bileşenler hakkında bilgi ve sürüm bilgileri için bkz: [Hadoop bileşenleri ve hdınsight'ta sürümleri][component-versioning]
>
>

### <a name="ambari"></a>Ambari
Apache Ambari, Apache Hadoop kümelerini hazırlamak, yönetmek ve izlemek içindir. İşleç araçlarının sezgisel bir koleksiyonunu ve sağlam bir Hadoop, kümelerin hello çalışmasını kolaylaştırarak, hello karmaşıklığını Gizle API kümesi içerir. Linux'ta Hdınsight kümeleri hem Ambari web kullanıcı Arabirimi hello hem de Ambari REST API hello sağlar. HDInsight kümelerinde Ambari Görünümleri eklenti kullanıcı arabirimi özelliklerine imkan tanır.
Bkz. [Ambari kullanarak HDInsight kümelerini yönetme](hdinsight-hadoop-manage-ambari.md) ve <a target="_blank" href="https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md">Apache Ambari API başvurusu</a>.

### <a name="avro"></a>Avro (Avro için Microsoft .NET kitaplığı)
Merhaba Avro için Microsoft .NET kitaplığı seri hale getirme hello Microsoft .NET ortamı için hello Apache Avro sıkıştırılmış ikili veri değişim biçimini uygular. Bir dilde seri hale getirilmiş verilerin başka bir dilde okunabilmesi için dilden bağımsız bir şema tanımlar. Merhaba biçim hakkında ayrıntılı bilgi hello bulunabilir < hedef = _ "blank" href = "http://avro.apache.org/docs/current/spec.html" > Apache Avro belirtimi</a>. Avro dosyalarını destekler hello Hello biçimi dağıtılmış MapReduce programlama modeli: dosyaların "bölünebilir" olması, bir dosyada herhangi bir noktasını arayabileceğiniz ve belirli bir bloktan itibaren okumaya başlamanız anlamına gelir. toofind nasıl, bkz: [Avro için Microsoft .NET kitaplığı hello verilerle seri](hdinsight-dotnet-avro-serialization.md). Linux tabanlı küme destek toocome.

### <a name="hdfs"></a>HDFS
Hadoop dağıtılmış dosya sistemi (HDFS), YARN ve MapReduce, Hadoop teknoloji hello çekirdek olan bir dosya sistemidir. Merhaba standart dosya sistemi hdınsight'taki Hadoop kümeleri için kullanıcının. Bkz. [HDFS ile uyumlu depolama alanından veri sorgulama](hdinsight-hadoop-use-blob-storage.md).

### <a name="hive"></a>Hive ve HCatalog
<a target="_blank" href="http://hive.apache.org/">Apache Hive</a> veri ambarı tooquery sağlayan Hadoop'ta oluşturulan yazılım ve HiveQL adında SQL benzeri bir dil kullanarak dağıtılmış depolamada büyük veri kümelerini yönetebilirsiniz. Pig gibi Hive da MapReduce üzerindeki bir soyutlamadır ve sorguları bir dizi MapReduce işine çevirir. Hive, Pig daha yakından tooa ilişkisel veritabanı yönetim sistemi ve daha fazla yapılandırılmış veriyle kullanılır. Yapılandırılmamış veriler için Pig hello daha iyi bir seçimdir. Bkz: [HDInsight’ta Hadoop ile Hive kullanma](hdinsight-use-hive.md).

<a target="_blank" href="https://cwiki.apache.org/confluence/display/Hive/HCatalog/">Apache HCatalog</a>, Hadoop için ilişkisel veri görünümü sunan bir tablo ve depolama yönetimi katmanıdır. HCatalog’da, dosyaları bir Hive SerDe (seri hale getirici-seri kaldırıcı) için uygun olan her biçimde okuyabilir ve yazabilirsiniz.

### <a name="mahout"></a>Mahout
<a target="_blank" href="https://mahout.apache.org/">Apache Mahout</a>, Hadoop üzerinde çalışan bir makine öğrenimleri algoritmaları kitaplığıdır. İstatistik ilkelerini kullanarak, machine learning uygulamaları sistemleri toolearn veri ve sonuçlar toodetermine gelecekteki davranışı geçmiş toouse öğretir. Bkz. [Hadoop’ta Mahout kullanarak film önerileri oluşturma](hdinsight-mahout.md).

### <a name="mapreduce"></a>MapReduce
MapReduce hello eski yazılım Hadoop için uygulamalar toobatch işlem büyük veri kümelerini paralel olarak yazmak için çerçevedir. Bir MapReduce işi, büyük veri kümelerini böler ve hello veri işleme için anahtar-değer çiftleri halinde düzenler. MapReduce işleri [YARN](#yarn) üzerinde çalışır. Bkz: <a target="_blank" href="http://wiki.apache.org/hadoop/MapReduce">MapReduce</a> hello Hadoop Wiki'de içinde.

### <a name="oozie"></a>Oozie
<a target="_blank" href="http://oozie.apache.org/">Apache Oozie</a>, Hadoop işlerini yöneten bir iş akışı koordinasyon sistemidir. Merhaba Hadoop yığını ile tümleştirilir ve MapReduce, Pig, Hive ve Sqoop için Hadoop işlerini destekler. Ayrıca, Java programları veya kabuk betikleri gibi kullanılan tooschedule işleri belirli tooa sistem de oluşturulabilir. Bkz. [Hadoop ile Oozie kullanma](hdinsight-use-oozie-linux-mac.md).

### <a name="phoenix"></a>Phoenix
<a  target="_blank" href="http://phoenix.apache.org/">Apache Phoenix</a>, HBase üzerinde ilişkisel veritabanı katmanıdır. Phoenix tooquery sağlar ve SQL tablolarını doğrudan yöneten bir JDBC sürücüsü içerir. Phoenix, MapReduce kullanmak yerine, sorguları ve diğer ifadeleri yerel NoSQL API çağrılarına çevirir, böylece NoSQL depoları üstünde daha hızlı uygulamalar sağlar. Bkz. [HBase kümeleriyle Apache ve SQuirreL kullanma](hdinsight-hbase-phoenix-squirrel.md).

### <a name="pig"></a>Pig
<a  target="_blank" href="http://pig.apache.org/">Apache Pig</a> Pig Latin adlı basit bir komut dosyası dili kullanılarak büyük veri kümelerinde karmaşık MapReduce dönüşümleri tooperform verir düzeyli bir platformdur. Pig, hadoop'ta çalışacakları şekilde hello Pig Latin betiklerini çevirir. Kullanıcı tanımlı işlevler (UDF'ler) tooextend Pig Latin oluşturabilirsiniz. Bkz. [Hadoop ile Pig kullanma](hdinsight-use-pig.md).

### <a name="sqoop"></a>Sqoop
<a  target="_blank" href="http://sqoop.apache.org/">Apache Sqoop</a>, aktarımları Hadoop ile SQL gibi ilişkisel veritabanları veya diğer yapılandırılmış veri depoları arasında mümkün olduğunca verimli şekilde toplu veri aktaran bir araçtır. Bkz: [Hadoop ile Sqoop kullanma](hdinsight-use-sqoop.md).

### <a name="tez"></a>Tez
<a  target="_blank" href="http://tez.apache.org/">Apache Tez</a>, Hadoop YARN'ı temel alan ve karmaşık, döngüsel olmayan genel veri işleme grafikleri çalıştıran bir uygulama altyapısıdır. Hive, ölçekte daha verimli bir şekilde toorun gibi veri yoğun işlemlere sağlayan bir daha esnek ve güçlü ardıl toohello MapReduce çerçevedir. Bkz. [Hive ve HiveQL Kullanımında "Gelişmiş performans için Apache Tez kullanma"](hdinsight-use-hive.md#usetez).

### <a name="yarn"></a>YARN
Apache YARN hello yeni nesil MapReduce (MapReduce 2.0 veya MRv2) ve daha yüksek ölçeklenebilirlik ve gerçek zamanlı işleme ile MapReduce toplu ötesinde veri işleme senaryolarını destekler. YARN kaynak yönetimi ve dağıtılmış uygulama altyapısı sağlar. MapReduce işleri YARN üzerinde çalışır. Bkz. <a target="_blank" href="http://hadoop.apache.org/docs/current/hadoop-yarn/hadoop-yarn-site/YARN.html">Apache Hadoop NextGen MapReduce (YARN)</a>.

### <a name="zookeeper"></a>ZooKeeper
<a  target="_blank" href="http://zookeeper.apache.org/">Apache ZooKeeper</a>, paylaşılan bir hiyerarşik veri kayıtları ad alanını (znode) kullanarak büyük çaplı dağıtılmış sistemlerde işlemleri koordine eder. Znode'lar az miktarda meta gerekli bilgileri toocoordinate işlemleri: durum, konum, yapılandırma ve benzeri. Örnek olarak bkz. [Bir HBase kümesi ve Apache Phoenix içeren ZooKeeper](hdinsight-hbase-phoenix-squirrel-linux.md). 

## <a name="programming-languages-on-hdinsight"></a>HDInsight’ta programlama dilleri
Spark, HBase, Kafka ve Hadoop gibi HDInsight kümeleri birçok programlama dilini destekler, ancak bunların bazı varsayılan olarak yüklü değildir. Kitaplıklar, modüller veya varsayılan olarak, yüklenmemiş paketleri [bir betik eylemi tooinstall hello bileşenini kullanan](hdinsight-hadoop-script-actions-linux.md). 

### <a name="default-programming-language-support"></a>Varsayılan programlama dili desteği 
Varsayılan olarak, HDInsight kümeleri aşağıdakileri destekler:

* Java
* Python

[Betik eylemleri](hdinsight-hadoop-script-actions-linux.md) kullanılarak ek diller yüklenebilir.

### <a name="java-virtual-machine-jvm-languages"></a>Java sanal makine (JVM) dilleri
Java dışındaki birçok dil Java sanal makinesinde (JVM); çalıştırabilirsiniz Ancak, bu dillerden bazılarını çalıştıran hello kümeye yüklü ek bileşenler gerektirebilir.

Bu JVM tabanlı diller HDInsight kümelerinde desteklenir:

* Clojure
* Jython (Java için Python)
* Scala

### <a name="hadoop-specific-languages"></a>Hadoop’a özgü diller
Hdınsight kümeleri belirli toohello Hadoop teknoloji yığınının dil aşağıdaki hello destekler:

* Pig işleri için Pig Latin
* Hive işleri için HiveQL ve SparkSQL

## <a name="hdinsight-standard-and-hdinsight-premium"></a>HDInsight Standart ve HDInsight Premium
HDInsight, Standart ve Premium olmak üzere, iki kategoride büyük veri bulutu teklifleri sunar. Hdınsight standart, Kurumsal ölçekte küme sağlar kuruluşlar, büyük veri iş yüklerini toorun kullanabilir. HDInsight Premium, Standart özellikleri temel alır ve HDInsight kümesi için gelişmiş bir çözümsel ve güvenlik özellikleri sağlar. Daha fazla bilgi için bkz. [Azure HDInsight Premium](hdinsight-component-versioning.md#hdinsight-standard-and-hdinsight-premium)

## <a name="microsoft-business-intelligence-and-hdinsight"></a>Microsoft iş zekası ve HDInsight
Bilinen iş zekası (BI) araçları almak, çözümlemek ve Power Query eklentisini ya da hello kullanarak Hdınsight ile tümleştirilmiş verileri rapor veya Microsoft Hive ODBC sürücüsü hello:

* [Power Query ile Excel tooHadoop bağlanmak](hdinsight-connect-excel-power-query.md): nasıl tooconnect Excel toohello depolayan Azure Storage hesabı hello Hdınsight kümenize verileri Excel için Microsoft Power Query kullanarak öğrenin. Windows iş istasyonu gereklidir. 
* [Excel tooHadoop hello Microsoft Hive ODBC sürücüsü ile bağlanma](hdinsight-connect-excel-hive-odbc-driver.md): Hdınsight ile tooimport verileri Microsoft Hive ODBC sürücüsü nasıl hello öğrenin. Windows iş istasyonu gereklidir. 
* [Microsoft bulut platformu](http://www.microsoft.com/server-cloud/solutions/business-intelligence/default.aspx): Office 365 için Power BI hakkında bilgi edinin hello SQL Server Deneme sürümünü indirin ve SharePoint Server 2013 ve SQL Server BI ayarlayın.
* [SQL Server Analysis Services](http://msdn.microsoft.com/library/hh231701.aspx)
* [SQL Server Reporting Services](http://msdn.microsoft.com/library/ms159106.aspx)


## <a name="next-steps"></a>Sonraki adımlar

* [HDInsight’ta Hadoop kullanmaya başlama](hdinsight-hadoop-linux-tutorial-get-started.md): HDInsight Hadoop kümeleri hazırlamak ve örnek Hive sorguları çalıştırmak için hızlı başlangıç öğreticisi.
* [HDInsight’ta Spark kullanmaya başlama](hdinsight-apache-spark-jupyter-spark-sql.md): Spark kümesi oluşturmak ve etkileşimli Spark SQL sorguları çalıştırmak için hızlı başlangıç öğreticisi.
* [HDInsight’ta R Sunucusu Kullanma](hdinsight-hadoop-r-server-get-started.md): HDInsight Premium’da R Sunucusu kullanmaya başlayın.
* [Hdınsight kümeleri sağlama](hdinsight-hadoop-provision-linux-clusters.md): Hdınsight Hadoop küme aracılığıyla tooprovision nasıl hello Azure portalı, Azure CLI veya Azure PowerShell öğrenin.


[component-versioning]: hdinsight-component-versioning.md
[zookeeper]: http://zookeeper.apache.org/