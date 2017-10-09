---
title: "aaaWhat olan Apache Storm - Azure Hdınsight | Microsoft Docs"
description: "Apache Storm, gerçek zamanlı veri tooprocess akışları sağlar. Azure Hdınsight verir tooeasily hello Azure bulut üzerinde Storm kümeleri oluşturun. Visual Studio ile C# kullanarak Storm çözümleri oluşturma ve Hdınsight Storm kümeleri tooyour dağıtın."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: "apache storm kullanım örnekleri,storm kümesi,apache storm nedir"
ms.assetid: 72d54080-1e48-4a5e-aa50-cce4ffc85077
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: 6c6b2925ef3e5666dfecc3fb3c835bb362902c51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-apache-storm-on-azure-hdinsight"></a>Azure HDInsight’ta Apache Storm nedir?

[Apache Storm](http://storm.apache.org/); dağıtılmış, hataya dayanıklı, açık kaynaklı bir hesaplama sistemidir. Hadoop ile gerçek zamanlı veri Storm tooprocess akışları kullanabilirsiniz. Storm çözümleri ayrıca verilerin garantili işlenmesini sağlayabilir, hello özelliği tooreplay ile başarıyla değildi veri hello ilk kez işlenir.

Hdınsight üzerinde Storm hello aşağıdaki avantajları sağlar:

* Yüzde 99,9 çalışma zamanı SLA'sı ile yönetilen bir hizmet olarak çalışır.

* Oluşturma sırasında veya sonrasında Storm kümesinde betik çalıştırarak kolay özelleştirmeyi destekler. Daha fazla bilgi için bkz. [HDInsight kümelerini betik eylemi kullanarak özelleştirme](hdinsight-hadoop-customize-cluster-linux.md).

* Çeşitli diller kullanır. Storm bileşenleri, Java, C# ve Python gibi tercih ettiğiniz hello dilde yazabilirsiniz.

    * Visual Studio hello geliştirme, yönetim ve C# topolojileri izleme için Hdınsight ile tümleşir. Daha fazla bilgi için bkz: [geliştirmek C# Storm topolojileri hello Visual Studio için Hdınsight araçları ile](hdinsight-storm-develop-csharp-visual-studio-topology.md).

    * Merhaba Trident Java arabirimini destekler. İletilerin tam olarak bir kez işlenmesini, işlemsel veri deposu kalıcılığını ve sık kullanılan Stream Analytics işlemlerini destekleyen Storm topolojileri oluşturabilirsiniz.

*  Storm kümelerinin ölçeğini kolayca artırın veya azaltın. Ekleyebilir veya hiçbir etkisi toorunning Storm topolojileri ile çalışan düğümleri kaldırın.

* Azure Hizmetleri aşağıdaki hello ile entegre olur:

    * Azure Event Hubs

    * Azure Sanal Ağ

    * Azure SQL Database

    * Azure Storage

    * Azure Cosmos DB

* Sanal ağ kullanarak güvenli bir şekilde hello birden fazla Hdınsight kümesinin özelliklerini birleştirir. Storm, Kafka, Spark, HBase veya Hadoop kümeleri kullanan analitik işlem hatları oluşturabilirsiniz.

Gerçek zamanlı analiz çözümleri için Apache Storm kullanan şirketlerin listesi için bkz. [Apache Storm Kullanan Şirketler](https://storm.apache.org/documentation/Powered-By.html).

Storm, kullanmaya tooget bkz [Hdınsight üzerinde Storm kullanmaya başlama][gettingstarted].

## <a name="how-does-storm-work"></a>Storm nasıl çalışır?

Storm topolojileri hello yerine aşina olabilir MapReduce işleri çalıştırır. Storm topolojileri döngüsel olmayan yönlü grafikte (DAG) düzenlenmiş birden fazla bileşenden oluşur. Veriler hello grafik hello bileşenler arasında akar. Her bileşen bir veya daha fazla veri akışı kullanır ve isteğe bağlı olarak bir veya daha fazla akış yayar. Aşağıdaki diyagramda hello temel word-count topolojisi bileşenler arasındaki veri akışını göstermektedir:

![Bileşenlerin bir Storm topolojisinde nasıl düzenlendiğini gösteren örnek](./media/hdinsight-storm-overview/example-apache-storm-topology-diagram.png)

* Spout bileşenleri, verileri bir topolojiye getirir. Bunlar bir veya daha fazla akışları hello topoloji yayma.

* Bolt bileşenleri, spout veya diğer boltlardan yayılan akışları kullanır. Cıvatalar akışları hello topoloji isteğe bağlı olarak yayma. Cıvatalar ayrıca veri tooexternal Hizmetleri veya HDFS, Kafka veya HBase gibi depolama yazmaktan sorumlu değildir.

## <a name="ease-of-creation"></a>Oluşturma kolaylığı

HDInsight üzerinde dakikalar için yeni bir Storm kümesi sağlayabilirsiniz. Storm kümesi oluşturma hakkında daha fazla bilgi için bkz. [HDInsight’ta Storm kullanmaya başlama](hdinsight-apache-storm-tutorial-get-started-linux.md).

## <a name="ease-of-use"></a>Kullanım kolaylığı

* __Güvenli Kabuk (SSH) bağlantı__: SSH kullanarak Storm kümenizin hello baş düğümler hello Internet erişebilirsiniz. SSH kullanarak komutları doğrudan kümeniz üzerinde çalıştırabilirsiniz.

  Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

* __Web Bağlantısı__: tüm Hdınsight kümeleri hello Ambari web kullanıcı Arabirimi sağlar. Kolayca izlemek, yapılandırmak ve hello Ambari web kullanıcı arabirimini kullanarak kümenizde hizmetleri yönetebilirsiniz. Storm kümeleri de hello Storm kullanıcı Arabirimi sağlar. İzleme ve çalışan Storm topolojilerini tarayıcınızdan hello Storm kullanıcı arabirimini kullanarak yönetin.

  Merhaba daha fazla bilgi için bkz [hello Ambari Web kullanıcı arabirimini yönetmek Hdınsight kullanarak](hdinsight-hadoop-manage-ambari.md) ve [İzleyici ve hello Storm kullanıcı arabirimini kullanarak yönetin](hdinsight-storm-deploy-monitor-topology-linux.md#monitor-and-manage-storm-ui) belgeleri.

* __Azure PowerShell ve Azure CLI__: PowerShell ve CLI her ikisi de, istemci sistem toowork Hdınsight ve diğer Azure hizmetleriyle birlikte gelen kullanabileceğiniz komut satırı yardımcı programlarını sağlar.

* __Visual Studio tümleştirmesi__: Visual Studio için Azure Data Lake araçları hello SCP.Net framework kullanarak C# Storm topolojileri oluşturmak için proje şablonları içerir. Data Lake araçları ayrıca sağlayan araçlar toodeploy izlemek ve hdınsight'ta Storm çözümleri yönetmek.

  Daha fazla bilgi için bkz: [geliştirmek C# Storm topolojileri hello Visual Studio için Hdınsight araçları ile](hdinsight-storm-develop-csharp-visual-studio-topology.md).

## <a name="integration-with-other-azure-services"></a>Diğer Azure hizmetleriyle tümleştirme

* __Azure Data Lake Store__: Data Lake Store’u bir Storm kümesi ile kullanmaya ilişkin örnek için bkz. [HDInsight’ta Azure Data Lake Store ile Apache Storm kullanma](hdinsight-storm-write-data-lake-store.md).

* __Olay hub'ları__: belgeleri aşağıdaki hello Storm kümesi ile Event Hubs kullanan bir örnek için bkz:

    * [HDInsight üzerinde Storm için Java tabanlı topoloji geliştirme](hdinsight-storm-develop-java-topology.md)

    * [HDInsight üzerinde Storm ile Azure Event Hubs’tan olay işleme (C#)](hdinsight-storm-develop-csharp-event-hub-topology.md)

* __SQL veritabanı__, __Cosmos DB__, __Event Hubs__, ve __HBase__: şablonu örnekleri Visual Studio için Data Lake araçları hello dahil edilir. Daha fazla bilgi için bkz. [HDInsight'ta Storm için C# topolojisi geliştirme](hdinsight-storm-develop-csharp-visual-studio-topology.md).

## <a name="reliability"></a>Güvenilirlik

Apache Storm bile hello veri analizi yüzlerce düğüme dağıldığında gelen her bir iletinin her zaman tam olarak, işleme güvence altına alır.

Merhaba Nimbus düğümü işlevselliği benzer toohello Hadoop Jobtracker'a sağlar ve Zookeeper aracılığıyla bir kümedeki tooother düğümlere görevler atar. Zookeeper düğümleri küme için eşgüdüm sağlayın ve hello yönetici işlemi hello çalışan düğümleri üzerinde Nimbus arasındaki iletişimi kolaylaştırır. Bir işleme düğümü devre dışı kalırsa, hello Nimbus düğümü bilgilendirilir ve hello görev ve ilişkili veriler tooanother düğüm atar.

Apache Storm kümeleri için Hello varsayılan configuration toohave yalnızca bir Nimbus düğümü olur. HDInsight üzerindeki Storm iki Nimbus düğümü sağlar. Merhaba birincil düğüm başarısız olursa, hello birincil düğüm kurtarılırken hello Storm kümesi toohello ikincil düğüme geçer. Merhaba Aşağıdaki diyagramda hello Görev akışı yapılandırmasını Hdınsight üzerinde Storm için gösterilmektedir:

![Nimbus, zookeeper ve supervisor diyagramı](./media/hdinsight-storm-overview/nimbus.png)

## <a name="scale"></a>Ölçek

Çalışan düğümleri ekleyerek veya kaldırarak HDInsight kümeleri ölçeklendirilebilir. Bu işlem, veriler işlenirken gerçekleştirilebilir.

> [!IMPORTANT]
> Yeni düğümler tootake avantajlarından eklenen ölçeklendirme aracılığıyla hello küme boyutu artırılmadan önce toorebalance Storm topolojilerini gerekir.

## <a name="support"></a>Destek

HDInsight üzerinde Storm kurumsal düzeyde kesintisiz tam destek ile birlikte gelir. HDInsight üzerinde Storm ayrıca yüzde 99,9 SLA’ya sahiptir. Bir Storm kümesine hello süre en az yüzde 99,9 dış bağlantısı olan garanti anlamına gelir.

Daha fazla bilgi için bkz. [Azure desteği](https://azure.microsoft.com/support/options/).

## <a name="apache-storm-use-cases"></a>Apache Storm kullanım örnekleri

Merhaba, Hdınsight üzerinde Storm kullanabilir bazı genel senaryolar şunlardır:

* Nesnelerin İnterneti (IoT)
* Sahtekarlık algılama
* Sosyal analiz
* Ayıklama, dönüşüm ve yükleme (ETL)
* Ağ izleme
* Arama
* Mobil katılım

Gerçek dünya senaryoları hakkında daha fazla bilgi için bkz: Merhaba [şirketler Storm'u nasıl kullanır](https://storm.apache.org/documentation/Powered-By.html) belge.

## <a name="development"></a>Geliştirme

.NET geliştiricileri, Visual Studio için Data Lake Araçları kullanarak C# dilinde topolojiler tasarlayıp uygulayabilir. Ayrıca Java ve C# bileşenlerini kullanan karma topolojiler de oluşturabilirsiniz.

Daha fazla bilgi için bkz. [Visual Studio kullanarak HDInsight üzerinde Storm için C# topolojileri geliştirme](hdinsight-storm-develop-csharp-visual-studio-topology.md).

Java çözümleri geliştirme hello tercih ettiğiniz IDE kullanarak yapabilirsiniz. Daha fazla bilgi için bkz. [HDInsight'ta Storm için Java topolojileri geliştirme](hdinsight-storm-develop-java-topology.md).

Python kullanılan toodevelop Storm bileşenleri de olabilir. Daha fazla bilgi için bkz. [HDInsight’ta Python kullanarak Storm topolojileri geliştirme](hdinsight-storm-develop-python-topology.md).

## <a name="common-development-patterns"></a>Yaygın geliştirme desenleri

### <a name="guaranteed-message-processing"></a>Garantili ileti işleme

Apache Storm farklı düzeylerde garantili ileti işleme sağlayabilir. Örneğin, temel bir Storm uygulaması en az bir kez işlemeyi, Trident ise tam bir kez işlemeyi garanti edebilir.

Daha fazla bilgi için apache.org sayfasındaki [Veri işleme garantileri](https://storm.apache.org/about/guarantees-data-processing.html) bölümüne bakın.

### <a name="ibasicbolt"></a>IBasicBolt

Merhaba sıfır veya daha fazla tanımlama grubu yayma bir girdi tanımlama okuma desenini ve hemen sonunda hello hello hello girdi tanımlama grubunu yürütürken yöntemi yaygındır. Storm sağlar hello [Ibasicbolt](https://storm.apache.org/releases/1.0.3/javadocs/org/apache/storm/topology/IBasicBolt.html) tooautomate bu deseni arabirim.

### <a name="joins"></a>Birleştirme

Uygulamalar arasına veri akışları nasıl katılır? Örneğin, yeni birden fazla akıştaki her bir tanımlama grubunu yeni bir akışta birleştirebilir veya yalnızca toplu tanımlama gruplarını belirli bir pencere için birleştirebilirsiniz. Her iki durumda da katılım, [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-) kullanılarak gerçekleştirilebilir. Gruplandırma alan diziler yönlendirilmiş toobolts ne olduğunu tanımlama bir yoludur.

Aşağıdaki Java örneğine hello fieldsGrouping bileşenleri "1", "2" ve "3" toohello MyJoiner Cıvata kaynaklanan kullanılan tooroute diziler şöyledir:

    builder.setBolt("join", new MyJoiner(), parallelism) .fieldsGrouping("1", new Fields("joinfield1", "joinfield2")) .fieldsGrouping("2", new Fields("joinfield1", "joinfield2")) .fieldsGrouping("3", new Fields("joinfield1", "joinfield2"));

### <a name="batches"></a>Toplu işler

Apache Storm "değer çizgisi tanımlama grubu" olarak bilinen bir iç zamanlama mekanizmasını sağlar. Değer çizgisi tanımlama grubunun topolojiniz içinde ne sıklıkta yayıldığını ayarlayabilirsiniz.

Bir C# bileşeninden değer çizgisi tanımlama grubu kullanımı örneği için bkz. [PartialBoltCount.cs](https://github.com/hdinsight/hdinsight-storm-examples/blob/3b2c960549cac122e8874931df4801f0934fffa7/EventCountExample/EventCountTopology/src/main/java/com/microsoft/hdinsight/storm/examples/PartialCountBolt.java).

### <a name="caches"></a>Caches

Bellek içi önbelleğe alma, sık kullanılan varlıkları bellekte tuttuğu için çoğunlukla işlemeyi hızlandırmaya yönelik bir mekanizma olarak kullanılır. Bir topoloji birden fazla düğüme ve her bir düğüm içindeki birden fazla işleme dağıtıldığı için, [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-) kullanmayı düşünmeniz gerekir. Kullanım `fieldsGrouping` önbellek araması için kullanılan hello alanları içeren tanımlama gruplarının her zaman yönlendirilmiş toohello olduğunu tooensure aynı işlemi. Bu gruplandırma işlevi, süreçler arasında önbellek girişlerinin yinelenmesini önler.

### <a name="stream-top-n"></a>"İlk N" akış

Topolojinizi ilk N değeri hesaplamaya bağlıysa ilk N değeri paralel hello hesaplayın. Ardından birleştirme hello Bu hesaplamaların çıktısını genel bir değer içine. Bu işlem kullanılarak yapılabilir [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-) tooroute paralel işleme alana göre. Ardından hello ilk N değeri genel olarak belirleyen tooa Cıvata yönlendirebilirsiniz.

Merhaba ilk N değeri hesaplama ilişkin bir örnek için bkz: [RollingTopWords](https://github.com/apache/storm/blob/master/examples/storm-starter/src/jvm/org/apache/storm/starter/RollingTopWords.java) örnek.

## <a name="logging"></a>Günlüğe kaydetme

Storm Apache Log4j toolog bilgileri kullanır. Varsayılan olarak, büyük miktarda veri kaydedilir ve hello bilgiler sayesinde zor toosort olabilir. Bir günlük yapılandırma dosyası kullanarak Storm topolojisini toocontrol günlüğe kaydetme davranışını bir parçası olarak dahil edebilirsiniz.

Gösteren bir örnek Topolojileri için günlüğe kaydetme, tooconfigure nasıl görürüm [Java tabanlı WordCount](hdinsight-storm-develop-java-topology.md) Hdınsight üzerinde Storm için örnek.

## <a name="next-steps"></a>Sonraki adımlar

HDInsight üzerinde Storm ile gerçek zamanlı analiz çözümleri hakkında daha fazla bilgi edinin:

* [HDInsight üzerinde Apache Storm kullanmaya başlama][gettingstarted]
* [HDInsight üzerinde Apache Storm için örnek topolojiler](hdinsight-storm-example-topology.md)

[stormtrident]: https://storm.apache.org/documentation/Trident-API-Overview.html
[samoa]: http://yahooeng.tumblr.com/post/65453012905/introducing-samoa-an-open-source-platform-for-mining
[apachetutorial]: https://storm.apache.org/documentation/Tutorial.html
[gettingstarted]: hdinsight-apache-storm-tutorial-get-started-linux.md
