---
title: "aaaUse hdınsight'ta - Azure Storm Apache Kafka | Microsoft Docs"
description: "Apache Kafka, Hdınsight üzerinde Apache Storm ile yüklenir. Storm ile sağlanan KafkaBolt ve KafkaSpout bileşenleri toowrite tooKafka ve kullanarak okuyun, gelen nasıl hello öğrenin. Ayrıca nasıl toouse Flux framework toodefine hello ve Storm topolojilerini gönderme öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e4941329-1580-4cd8-b82e-a2258802c1a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/21/2017
ms.author: larryfr
ms.openlocfilehash: 95701f51dfdf6f1a859dcde96d7053df4f21701f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-kafka-preview-with-storm-on-hdinsight"></a>Hdınsight üzerinde Storm ile Apache Kafka (Önizleme) kullanın

Bilgi nasıl toouse Apache Storm tooread gelen ve tooApache Kafka yazma. Bu örnek ayrıca nasıl Storm topolojisini toohello HDFS uyumlu toosave verilerden dosya sistemi Hdınsight tarafından kullanılan gösterir.

> [!NOTE]
> Bu belgedeki Hello adımlar hem Hdınsight üzerinde Storm ve Hdınsight kümesinde bir Kafka içeren bir Azure kaynak grubu oluşturun. Bu kümeleri, hem bir Azure sanal hello Storm kümesi toodirectly sağlayan ağ içinde bulunan Kafka küme hello ile iletişim ' dir.
> 
> Bu belgedeki hello adımları tamamladığınızda, toodelete hello kümeleri tooavoid aşırı ücretleri unutmayın.

## <a name="get-hello-code"></a>Merhaba kod alın

Bu belgede kullanılan hello örneğin Hello kod şu adreste [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).

toocompile bu proje için geliştirme ortamınızı yapılandırma aşağıdaki hello gerekir:

* [Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ya da daha yüksek. Java 8 Hdınsight 3.5 veya daha yükseğini gerektirir.

* [Maven 3.x](https://maven.apache.org/download.cgi)

* Bir SSH istemcisi (Merhaba gereksinim `ssh` ve `scp` komutları) - bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

* Bir metin düzenleyicisi veya IDE.

Geliştirme iş istasyonunuza Java ve hello JDK yüklediğinizde hello aşağıdaki ortam değişkenleri ayarlanmış olabilir. Ancak, bunlar mevcut olduğundan ve sisteminiz için doğru değerleri hello içerdikleri denetlemeniz gerekir.

* `JAVA_HOME`-hello JDK yüklendiği toohello dizin işaret etmelidir.
* `PATH`-yolları aşağıdaki hello içermelidir:
  
    * `JAVA_HOME`(veya eşdeğer yolu hello).
    * `JAVA_HOME\bin`(veya eşdeğer yolu hello).
    * Maven'ın yüklendiği başlangıç dizini.

## <a name="create-hello-clusters"></a>Merhaba kümeleri oluşturma

Hdınsight üzerinde Apache Kafka sağlamaz erişim toohello Kafka aracıların üzerinden genel internet hello. Merhaba düğümler aynı Azure sanal ağ konuşmaları tooKafka olmalıdır hello herhangi bir şey Kafka küme hello. Bu örnekte, bir Azure sanal ağında hello Kafka ve Storm kümeleri bulunur. Merhaba Aşağıdaki diyagramda hello kümeleri arasında iletişimi nasıl akacağını gösterilmektedir:

![Bir Azure sanal ağı Storm ve Kafka kümelerde diyagramı](./media/hdinsight-apache-storm-with-kafka/storm-kafka-vnet.png)

> [!NOTE]
> SSH ve Ambari üzerinden erişilebilen gibi diğer hizmetler hello kümede Internet hello. Merhaba ortak bağlantı noktaları Hdınsight ile kullanılabilir hakkında daha fazla bilgi için bkz: [bağlantı noktaları ve Hdınsight tarafından kullanılan URI](hdinsight-hadoop-port-settings-for-services.md).

Azure sanal ağı, Kafka, oluşturabilir ve Storm el ile kümeleri olsa da, daha kolay toouse bir Azure Resource Manager şablonu durumdur. Toodeploy Azure sanal ağı, Kafka, kullanım hello aşağıdaki adımları ve tooyour Azure aboneliği Storm kümeleri.

1. Düğme toosign tooAzure içinde ve açık hello şablonunda hello Azure portalı aşağıdaki hello kullanın.
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-storm-cluster-in-vnet-v2.json" target="_blank"><img src="./media/hdinsight-apache-storm-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    Hello Azure Resource Manager şablonu konumundadır **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**. Kaynakları aşağıdaki hello oluşturur:
    
    * Azure kaynak grubu
    * Azure Sanal Ağ
    * Azure Storage hesabı
    * Hdınsight sürüm 3.6 (üç alt düğümleri) üzerindeki Kafka
    * Sürüm 3.6 (üç alt düğümler) hdınsight'ta Storm

  > [!WARNING]
  > Hdınsight üzerinde Kafka kullanılabilirliğini tooguarantee, kümenizi en az üç alt düğümleri içermesi gerekir. Bu şablon, üç alt düğümleri içeren bir Kafka küme oluşturur.

2. Kılavuzu toopopulate hello girişleri hello üzerinde aşağıdaki kullanım hello **özel dağıtım** dikey penceresinde:
   
    ![Hdınsight özel dağıtım](./media/hdinsight-apache-storm-with-kafka/parameters.png)

    * **Kaynak grubu**: bir grup oluşturun veya varolan bir tanesini seçin. Bu grup hello Hdınsight kümesi içerir.
   
    * **Konum**: konum coğrafi olarak Kapat tooyou seçin.

    * **Temel küme adı**: Bu değer hello Storm ve Kafka kümelerinin hello temel adı olarak kullanılır. Örneğin, **hdı** adlı bir Storm kümesi oluşturur **storm hdı** ve adlı Kafka küme **kafka hdı**.
   
    * **Oturum açma kullanıcı adı küme**: hello Storm ve Kafka kümelerinin hello Yöneticisi kullanıcı adı.
   
    * **Oturum açma parolası küme**: hello Storm ve Kafka kümeleri için hello yönetici kullanıcı parolası.
    
    * **SSH kullanıcı adı**: hello Storm ve Kafka kümeleri için SSH kullanıcı toocreate hello.
    
    * **SSH parolası**: hello SSH kullanıcı hello Storm ve Kafka kümelerinin hello parolası.

3. Okuma hello **hüküm ve koşullar**ve ardından **toohello hüküm ve koşullar yukarıda belirtildiği kabul**.

4. Son olarak, denetleme **PIN toodashboard** ve ardından **satın alma**. Merhaba kümeleri toocreate yaklaşık 20 dakika sürer.

Merhaba kaynakları oluşturduktan sonra hello dikey penceresinde hello kaynak grubu için görüntülenir.

![Kaynak grubu dikey hello vnet ve kümeler için](./media/hdinsight-apache-storm-with-kafka/groupblade.png)

> [!IMPORTANT]
> Merhaba Hdınsight kümeleri Hello adlarını olduğuna dikkat edin **storm BASENAME** ve **kafka BASENAME**, BASENAME toohello şablonu sağladığınız hello adı olduğu. Bu adları toohello kümeleri bağlanırken daha sonraki adımlarda kullanın.

## <a name="understanding-hello-code"></a>Merhaba kodu anlama

Bu proje iki topoloji içerir:

* **KafkaWriter**: hello tarafından tanımlanan **writer.yaml** dosyası, bu topoloji hello Apache Storm ile sağlanan KafkaBolt kullanarak rastgele cümleleri tooKafka yazar.

    Bu topoloji bir özel kullanan **SentenceSpout** bileşen toogenerate rastgele cümleleri.

* **KafkaReader**: hello tarafından tanımlanan **reader.yaml** dosyasını bu topoloji okur veriler Kafka hello Apache Storm ile sağlanan KafkaSpout kullanarak ve ardından günlükleri hello veri toostdout.

    Bu topoloji hello Storm HdfsBolt toowrite veri toodefault depolama hello Storm kümesi için kullanır.
### <a name="flux"></a>Flux

Merhaba topolojileri kullanılarak tanımlanır [Flux](https://storm.apache.org/releases/1.1.0/flux.html). Flux içinde sunulmuştur 0.10.x Storm ve tooseparate hello topoloji yapılandırması hello kodundan sağlar. Merhaba Flux framework kullanan topolojileri hello topoloji YAML dosyasında tanımlanır. Merhaba YAML dosya hello topolojisinin bir parçası olarak dahil olabilir. Ayrıca, hello topoloji gönderdiğinizde kullanılan tek başına dosya de olabilir. Flux çalışma zamanında Bu örnekte kullanılan, değişkeni değiştirme de destekler.

Merhaba aşağıdaki parametreleri bu topolojiler için çalışma zamanında ayarlanır:

* `${kafka.topic}`: hello hello topolojileri okuma/yazma için Kafka konu hello adı.

* `${kafka.broker.hosts}`: hello çalıştıracağınız Kafka aracıların bu hello barındırır. Merhaba aracısı bilgi KafkaBolt hello tarafından tooKafka yazılırken kullanılır.

* `${kafka.zookeeper.hosts}`: Zookeeper çalışan üzerinde hello konakları hello Kafka küme.

Flux topolojileri hakkında daha fazla bilgi için bkz: [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).

## <a name="download-and-compile-hello-project"></a>Karşıdan yükle ve Merhaba projeyi derleyin

1. Geliştirme ortamınızı hello projesinden indirmeniz [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), bir komut satırı açın ve dizinleri toohello konum hello proje indirdiğiniz değiştirin.

2. Merhaba gelen **hdınsight storm java kafka** dizin kullanım hello aşağıdaki komut toocompile hello proje ve dağıtımı için bir paket oluşturun:

  ```bash
  mvn clean package
  ```

    Merhaba paket işlemi adlı bir dosya oluşturur `KafkaTopology-1.0-SNAPSHOT.jar` hello içinde `target` dizin.

3. Komutları toocopy hello paket tooyour Storm Hdınsight kümesinde aşağıdaki hello kullanın. Değiştir **kullanıcıadı** hello küme için hello SSH kullanıcı adı ile. Değiştir **BASENAME** hello temel adıyla hello küme oluşturulurken kullanılır.

  ```bash
  scp ./target/KafkaTopology-1.0-SNAPSHOT.jar USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
  ```

    İstendiğinde, hello kümeleri oluşturulurken kullanılan hello parola girin.

## <a name="configure-hello-topology"></a>Merhaba topolojisini yapılandırma

1. Yöntemleri toodiscover aşağıdaki hello birini kullanın Kafka Aracısı konakları hello:

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $brokerHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($brokerHosts -join ":9092,") + ":9092"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > Merhaba Bash örnek varsayar `$CLUSTERNAME` hello Hdınsight kümesi hello adını içerir. Ayrıca varsayılmaktadır [jq](https://stedolan.github.io/jq/) yüklenir. İstendiğinde, hello küme oturum açma hesabının hello parolasını girin.

    döndürülen hello değeri metin aşağıdaki benzer toohello şöyledir:

        wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092

    > [!IMPORTANT]
    > Kümeniz için ikiden fazla Aracısı konakları olsa tooprovide tüm konaklar tooclients tam listesi gerekmez. Bir veya iki yeterlidir.

2. Yöntemleri toodiscover hello Kafka Zookeeper konakları aşağıdaki hello birini kullanın:

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $zookeeperHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($zookeeperHosts -join ":2181,") + ":2181"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > Merhaba Bash örnek varsayar `$CLUSTERNAME` hello Hdınsight kümesi hello adını içerir. Ayrıca varsayılmaktadır [jq](https://stedolan.github.io/jq/) yüklenir. İstendiğinde, hello küme oturum açma hesabının hello parolasını girin.

    döndürülen hello değeri metin aşağıdaki benzer toohello şöyledir:

        zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181

    > [!IMPORTANT]
    > İkiden fazla Zookeeper düğümleri olsa da, tüm ana bilgisayarlar tooclients tam listesi tooprovide gerekmez. Bir veya iki yeterlidir.

    Bu değer daha sonra kullanılmak üzere kaydedin.

3. Merhaba Düzenle `dev.properties` hello hello proje kökündeki dosyasında. Bu dosyada Hello aracısı ve Zookeeper konakları bilgi toohello eşleşen satırları ekleyin. Merhaba aşağıdaki örnek hello örnek değerler hello önceki adımları kullanarak yapılandırılır:

        kafka.zookeeper.hosts: zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181
        kafka.broker.hosts: wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092
        kafka.topic: stormtopic

4. Merhaba Kaydet `dev.properties` dosya ve hello komut tooupload, toohello Storm kümesi kullanın:

     ```bash
    scp dev.properties USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
    ```

    Değiştir **kullanıcıadı** hello küme için hello SSH kullanıcı adı ile. Değiştir **BASENAME** hello temel adıyla hello küme oluşturulurken kullanılır.

## <a name="start-hello-writer"></a>Merhaba yazan Başlat

1. SSH kullanarak tooconnect toohello Storm kümesi aşağıdaki hello kullanın. Değiştir **kullanıcıadı** hello küme oluşturulurken kullanılan hello SSH kullanıcı adı. Değiştir **BASENAME** hello küme oluşturulurken kullanılan hello temel ada sahip.

  ```bash
  ssh USERNAME@storm-BASENAME-ssh.azurehdinsight.net
  ```

    İstendiğinde, hello kümeleri oluşturulurken kullanılan hello parola girin.
   
    Bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

2. SSH bağlantısı Hello komutu toocreate hello hello topolojisi tarafından kullanılan Kafka konu aşağıdaki hello kullanın:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic stormtopic --zookeeper $KAFKAZKHOSTS
    ```

    Değiştir `$KAFKAZKHOSTS` Zookeeper hello ile Merhaba önceki bölümde alınan bilgileri ana bilgisayar.

2. Merhaba SSH bağlantı toohello Storm kümeden komutu toostart hello yazan topolojisi aşağıdaki hello kullanın:

    ```bash
    storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
    ```

    Bu komutla birlikte kullanılan hello Parametreler şunlardır:

    * `org.apache.storm.flux.Flux`: Flux tooconfigure kullanın ve bu topoloji çalıştırın.

    * `--remote`: Hello topoloji tooNimbus gönderin. Merhaba topoloji hello kümedeki hello çalışan düğümleri arasında dağıtılır.

    * `-R /writer.yaml`: Kullanım Merhaba `writer.yaml` tooconfigure hello topoloji dosya. `-R`Bu kaynak hello jar dosyasına dahil olduğunu gösterir. Bu nedenle hello jar hello kök dizininde olduğundan `/writer.yaml` hello yolu tooit olduğu.

    * `--filter`: Hello girdileri doldurmak `writer.yaml` hello değerleri kullanarak topolojisi `dev.properties` dosya. Örneğin, hello değerini hello `kafka.topic` giriştir hello dosyasında kullanılan tooreplace hello `${kafka.topic}` hello topoloji tanımı girişi.

5. Merhaba topoloji başladıktan sonra veri toohello Kafka konu yazıyor komutu tooverify aşağıdaki hello kullanın:

  ```bash
  /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $KAFKAZKHOSTS --from-beginning --topic stormtopic
  ```

    Değiştir `$KAFKAZKHOSTS` Zookeeper hello ile Merhaba önceki bölümde alınan bilgileri ana bilgisayar.

    Bu komut, Kafka toomonitor hello konu ile birlikte gelen bir komut dosyası kullanır. Bir süre sonra toohello konu yazılmış rastgele cümleleri döndürme başlamalısınız. Merhaba, benzer toohello aşağıdaki örneğine çıktı:

        i am at two with nature             
        an apple a day keeps hello doctor away
        snow white and hello seven dwarfs     
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        four score and seven years ago      
        snow white and hello seven dwarfs     
        snow white and hello seven dwarfs     
        i am at two with nature             
        an apple a day keeps hello doctor away

    Ctrl + c toostop hello komut dosyası kullanın.

## <a name="start-hello-reader"></a>Merhaba reader'ı başlatın

1. Merhaba SSH oturumu toohello Storm kümeden komutu toostart hello okuyucu topolojisi aşağıdaki hello kullanın:

  ```bash
  storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties
  ```

2. Merhaba topoloji başladıktan sonra hello Storm kullanıcı arabirimini açın. Bu web kullanıcı Arabirimi https://storm-BASENAME.azurehdinsight.net/stormui bulunur. Değiştir __BASENAME__ hello küme oluştururken kullandığınız hello temel adı ile. 

    İstendiğinde, hello yönetici oturum açma adı kullanın (varsayılan, `admin`) ve hello küme oluştururken kullanılan parola. Görüntü izleyerek bir web sayfası benzer toohello bakın:

    ![Storm kullanıcı Arabirimi](./media/hdinsight-apache-storm-with-kafka/stormui.png)

3. Storm kullanıcı Arabirimi Hello hello seçin __kafka okuyucu__ hello bağlantıyı __topoloji özeti__ bölümünde hello toodisplay bilgilerini __kafka okuyucu__ topolojisi.

    ![Topoloji özeti kısmını hello Storm web kullanıcı Arabirimi](./media/hdinsight-apache-storm-with-kafka/topology-summary.png)

4. Merhaba Günlükçü Cıvata bileşeninin select hello hello örnekleri hakkında toodisplay bilgi __Günlükçü Cıvata__ hello bağlantıyı __Cıvatalar (her zaman)__ bölümü.

    ![Merhaba Cıvatalar bölümündeki Günlükçü Cıvata bağlantıyı](./media/hdinsight-apache-storm-with-kafka/bolts.png)

5. Merhaba, __yürütücüler__ bölümünde, bir bağlantı hello seçin __bağlantı noktası__ hello bileşenin bu örneği hakkında sütun toodisplay günlük kaydı bilgileri.

    ![Yürütücüler bağlantı](./media/hdinsight-apache-storm-with-kafka/executors.png)

    Merhaba günlük hello Kafka konu ' okunan hello veri günlüğü içerir. Merhaba günlüğünde Hello bilgi metnini izleyen benzer toohello şöyledir:

        2016-11-04 17:47:14.907 c.m.e.LoggerBolt [INFO] Received data: four score and seven years ago
        2016-11-04 17:47:14.907 STDIO [INFO] hello cow jumped over hello moon
        2016-11-04 17:47:14.908 c.m.e.LoggerBolt [INFO] Received data: hello cow jumped over hello moon
        2016-11-04 17:47:14.911 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.911 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.969 STDIO [INFO] an apple a day keeps hello doctor away
        2016-11-04 17:47:14.970 c.m.e.LoggerBolt [INFO] Received data: an apple a day keeps hello doctor away

## <a name="stop-hello-topologies"></a>Merhaba topolojileri Durdur

Bir SSH oturumu toohello Storm kümeden komutları toostop hello Storm topolojilerini aşağıdaki hello kullan:

  ```bash
  storm kill kafka-writer
  storm kill kafka-reader
  ```

## <a name="delete-hello-cluster"></a>Merhaba küme silme

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Merhaba adımlar bu belgedeki her ikisi de oluşturma beri kümelerde Merhaba aynı Azure kaynak grubu, hello Azure portal hello kaynak grubunu silebilirsiniz. Bu belge aşağıdaki tarafından oluşturulan tüm kaynakları silme hello kaynak grubu kaldırır.

## <a name="next-steps"></a>Sonraki adımlar

Hdınsight üzerinde Storm ile kullanılan daha fazla örnek Topolojileri için bkz: [örnek Storm topolojileri ve bileşenleri](hdinsight-storm-example-topology.md).

Dağıtma ve Linux tabanlı Hdınsight üzerinde topolojileri izleme hakkında daha fazla bilgi için bkz: [dağıtma ve Linux tabanlı Hdınsight üzerinde Apache Storm topolojilerini yönetme](hdinsight-storm-deploy-monitor-topology-linux.md)