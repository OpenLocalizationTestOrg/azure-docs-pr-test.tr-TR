---
title: "Azure Hdınsight kullanarak Storm aaaTroubleshoot | Microsoft Docs"
description: "Apache Storm Azure Hdınsight ile kullanma hakkında toocommon soruların yanıtlarını alın."
keywords: "Sorun giderme kılavuzu, ortak sorunları azure Hdınsight, Storm, SSS"
services: Azure HDInsight
documentationcenter: na
author: raviperi
manager: 
editor: 
ms.assetid: 74E51183-3EF4-4C67-AA60-6E12FAC999B5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: raviperi
ms.openlocfilehash: 51bcb3dc28eff5ee7bb33252fb2ec71a88ed8e09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-storm-by-using-azure-hdinsight"></a>Storm Azure Hdınsight kullanarak sorun giderme

Merhaba üst sorunları ve bunların çözümleri için Apache Ambari, Apache Storm yükü ile çalışma hakkında bilgi edinin.

## <a name="how-do-i-access-hello-storm-ui-on-a-cluster"></a>Bir küme üzerindeki Storm kullanıcı Arabirimi hello nasıl erişirim
Merhaba Storm kullanıcı Arabirimi bir tarayıcıdan erişirken için iki seçeneğiniz vardır:

### <a name="ambari-ui"></a>Ambari kullanıcı Arabirimi
1. Toohello ambarı Pano gidin.
2. Hizmetleri Hello listesinde seçin **Storm**.
3. Merhaba, **hızlı bağlantılar** menüsünde, select **Storm kullanıcı Arabirimi**.

### <a name="direct-link"></a>Doğrudan bağlantı
URL aşağıdaki hello adresindeki hello Storm kullanıcı Arabirimi erişebilirsiniz:

https://\<küme DNS adına\>/stormui

Örnek:

 https://stormcluster.azurehdinsight.NET/stormui

## <a name="how-do-i-transfer-storm-event-hub-spout-checkpoint-information-from-one-topology-tooanother"></a>Bir topoloji tooanother nasıl Storm olay hub'ı spout denetim noktası bilgilerini Aktarım

Hdınsight Storm olay hub'ı spout .jar dosyasına hello kullanarak Azure olay hub'larından okumayı topolojileri geliştirirken, yeni kümede aynı adı hello sahip bir topoloji dağıtmanız gerekir. Ancak, kaydedilmiş tooApache ZooKeeper hello eski kümedeki edildi hello denetim noktası verileri korumanız gerekir.

### <a name="where-checkpoint-data-is-stored"></a>Denetim noktası verileri depolandığı
Denetim noktası verileri uzaklıkları için Itanium tabanlı sistemler için hello olay hub'ı spout ZooKeeper içinde iki kök yollarda tarafından depolanır:
- İşlem dışı spout kontrol noktaları /eventhubspout içinde depolanır.
- İşlem spout denetim noktası verileri / işlem depolanır.

### <a name="how-toorestore"></a>Nasıl toorestore
bkz: tooget hello komut dosyaları ve tooexport veri ZooKeeper dışında kullanın ve yeni bir adla hello veri geri tooZooKeeper içeri aktarma kitaplıkları [Hdınsight Storm örnekler](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).

Merhaba LIB klasör hello içeri/dışarı aktarma işlemi için başlangıç uygulaması içeren .jar dosyaları içerir. Merhaba bash klasör nasıl tooexport verilerden ZooKeeper sunucusu hello eski kümedeki hello gösteren örnek bir komut dosyası vardır ve geri toohello ZooKeeper sunucusu hello yeni kümede içeri aktarın.

Merhaba çalıştırmak [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) hello ZooKeeper düğümleri tooexport komut dosyası ve veri içeri aktarın. Merhaba betik toohello doğru Hortonworks veri Platformu (HDP) sürümünü güncelleştirin. (Bu komut dosyalarını hdınsight'ta genel yapılması çalışıyoruz. Genel komut dosyası herhangi bir düğümden hello küme hello kullanıcı tarafından değişiklik olmadan çalıştırabilirsiniz.)

Merhaba Dışa Aktar komutunu hello meta veri tooan Apache Hadoop dağıtılmış dosya sistemi (HDFS) yol (bir Azure Blob Storage veya Azure Data Lake Store deposunda) ayarladığınız bir konuma yazar.

### <a name="examples"></a>Örnekler

#### <a name="export-offset-metadata"></a>Uzaklık meta verileri dışarı aktarma
1. SSH toogo toohello ZooKeeper küme hangi hello denetim noktasından uzaklığı dışarı toobe gereken hello kümede kullanın.
2. Çalışma hello aşağıdaki komutu (Merhaba HDP sürüm dizesi güncelleştirdikten sonra) tooexport ZooKeeper uzaklığı veri toohello /stormmetadta/zkdata HDFS yol:

    ```apache   
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter export /eventhubspout /stormmetadata/zkdata
    ```

#### <a name="import-offset-metadata"></a>Uzaklık meta verileri içeri aktarma
1. SSH toogo toohello ZooKeeper küme hangi hello denetim noktasından uzaklığı dışarı toobe gereken hello kümede kullanın.
2. Çalışma hello (Merhaba HDP sürüm dizesi güncelleştirdikten sonra) komutu aşağıdaki tooimport ZooKeeper hello HDFS yol/stormmetadata/zkdata toohello ZooKeeper sunucuda hello hedef küme verilerden uzaklık:

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter import /eventhubspout /home/sshadmin/zkdata
    ```
   
#### <a name="delete-offset-metadata-so-that-topologies-can-start-processing-data-from-hello-beginning-or-from-a-timestamp-that-hello-user-chooses"></a>Böylece topolojileri hello başından veri işleme başlayabilirsiniz veya bir zaman damgası hello kullanıcı seçer uzaklık meta verilerini silme
1. SSH toogo toohello ZooKeeper küme hangi hello denetim noktasından uzaklığı dışarı toobe gereken hello kümede kullanın.
2. Çalışma hello (Merhaba HDP sürüm dizesi güncelleştirdikten sonra) komutu aşağıdaki toodelete tüm ZooKeeper hello geçerli küme verilerde uzaklık:

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter delete /eventhubspout
    ```

## <a name="how-do-i-locate-storm-binaries-on-a-cluster"></a>Bir kümede nasıl Storm ikili dosyaları bulun
Merhaba geçerli HDP yığını için Storm ikili dosyalarını /usr/hdp/current/storm-client içinde ' dir. Başlangıç konumu olan hello baş düğümler ve çalışan düğümleri için aynı.
 
Birden çok ikili dosyaları /usr/hdp (örneğin, /usr/hdp/2.5.0.1233/storm) belirli HDP sürümlerde için olabilir. Merhaba kümede çalışan symlinked toohello en son sürümünü Hello /usr/hdp/current/storm-client klasörüdür.

Daha fazla bilgi için bkz: [Bağlan SSH kullanarak Hdınsight kümesi tooan](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) ve [Storm](http://storm.apache.org/).
 
## <a name="how-do-i-determine-hello-deployment-topology-of-a-storm-cluster"></a>Bir Storm kümesine hello dağıtım topolojisi nasıl belirlerim
İlk olarak, Hdınsight Storm ile yüklenen tüm bileşenler tanımlayın. Storm kümesi dört düğüm kategorilerini oluşur:

* Ağ geçidi düğümleri
* Baş düğümler
* ZooKeeper düğümleri
* Çalışan düğümü
 
### <a name="gateway-nodes"></a>Ağ geçidi düğümleri
Bir ağ geçidi düğümü, bir ağ geçidi ve genel erişim tooan active Ambari yönetim hizmeti sağlayan ters proxy hizmeti olduğu. Ayrıca, Ambari öncü seçim işler.
 
### <a name="head-nodes"></a>Baş düğümler
Storm baş düğümler Hizmetleri aşağıdaki hello çalıştırın:
* Nimbus
* Ambarı sunucusu
* Ambari ölçümleri sunucu
* Ambari ölçümleri Toplayıcı
 
### <a name="zookeeper-nodes"></a>ZooKeeper düğümleri
Hdınsight üç düğümü ZooKeeper çekirdek ile birlikte gelir. Merhaba çekirdek boyutu sabittir ve yapılandırılamayan.
 
Storm hello kümede yapılandırılmış tooautomatically kullanım hello ZooKeeper çekirdek hizmetleridir.
 
### <a name="worker-nodes"></a>Çalışan düğümü
Storm çalışan düğümleri Hizmetleri aşağıdaki hello çalıştırın:
* Gözetmen
* Çalışan Java topolojileri çalıştırmak için makineleri (JVMs)
* Ambari aracı
 
## <a name="how-do-i-locate-storm-event-hub-spout-binaries-for-development"></a>Geliştirme için Storm olay hub'ı spout ikili dosyalarını nasıl bulun
 
Storm olay hub'ı spout .jar dosyaları topolojinizi ile kullanma hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın.
 
### <a name="java-based-topology"></a>Java tabanlı topolojisi
[Azure Event hubs'tan (Java) hdınsight'ta Storm işlem olayları](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-java-event-hub-topology)
 
### <a name="c-based-topology-mono-on-hdinsight-34-linux-storm-clusters"></a>C#-topoloji (Mono Hdınsight 3.4 + Linux Storm kümeleri üzerinde) temel
[HDInsight üzerinde Storm ile Azure Event Hubs’tan olay işleme (C#)](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-csharp-event-hub-topology)
 
### <a name="latest-storm-event-hub-spout-binaries-for-hdinsight-35-linux-storm-clusters"></a>Storm event hub'ın en son spout Hdınsight 3.5 + Linux Storm kümeleri için ikili dosyalar
toolearn Hdınsight ile 3.5 + çalışan toouse hello son Storm olay hub'ı spout kümelerinde Linux Storm bkz hello mvn-repo [Benioku dosyasını](https://github.com/hdinsight/mvn-repo/blob/master/README.md).
 
### <a name="source-code-examples"></a>Kaynak kodu örnekleri
Bkz: [örnekler](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) nasıl tooread ve Azure Event Hub'ın bir Azure Hdınsight kümesinde (Java'da yazılmış) bir Apache Storm topolojisini kullanarak gelen yazma.
 
## <a name="how-do-i-locate-storm-log4j-configuration-files-on-clusters"></a>Storm Log4J yapılandırma dosyalarını kümelerde nasıl bulun
 
Storm Hizmetleri için tooidentify Apache Log4J yapılandırma dosyaları.
 
### <a name="on-head-nodes"></a>Baş düğümler üzerinde
Merhaba Nimbus Log4J yapılandırma okuma/usr/hdp/\<HDP sürüm\>/storm/log4j2/cluster.xml.
 
### <a name="on-worker-nodes"></a>Alt düğümler üzerinde
Hello Yöneticisi Log4J yapılandırma okuma/usr/hdp/\<HDP sürüm\>/storm/log4j2/cluster.xml.
 
Merhaba çalışan Log4J yapılandırma dosyasını okuma/usr/hdp/\<HDP sürüm\>/storm/log4j2/worker.xml.
 
Örnekler: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml

