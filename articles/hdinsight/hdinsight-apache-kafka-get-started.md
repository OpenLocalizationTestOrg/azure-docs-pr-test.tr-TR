---
title: "Apache Kafka - Azure Hdınsight ile aaaStart | Microsoft Docs"
description: "Azure Hdınsight'ta Apache Kafka toocreate küme nasıl öğrenin. Bilgi nasıl toocreate konuları, aboneleri ve tüketicilerin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 43585abf-bec1-4322-adde-6db21de98d7f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: b93299d88dc2cf9a9764662509308ff75fd74474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="start-with-apache-kafka-preview-on-hdinsight"></a>HDInsight üzerinde Apache Kafka'yı (önizleme) kullanmaya başlama

Bilgi nasıl toocreate ve bir [Apache Kafka](https://kafka.apache.org) Azure Hdınsight kümesinde. Kafka, HDInsight ile birlikte kullanılabilen, açık kaynaklı bir dağıtılmış akış platformudur. Sık kullanılan bir ileti Aracısı benzer işlevsellik sağlar gibi tooa yayımlama-abone olma ileti sırası.

> [!NOTE]
> Kafka’nın şu anda HDInsight ile kullanılabilen iki sürümü vardır: 0.9.0 (HDInsight 3.4) ve 0.10.0 (HDInsight 3.5 ve 3.6). Bu belgedeki Hello adımlar üzerinde Hdınsight 3.6 Kafka kullandığınız varsayılır.

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="create-a-kafka-cluster"></a>Kafka kümesi oluşturma

Adımları toocreate bir Kafka Hdınsight kümesinde aşağıdaki hello kullan:

1. Merhaba gelen [Azure portal](https://portal.azure.com)seçin **+ yeni**, **Intelligence + analiz**ve ardından **Hdınsight**.
   
    ![HDInsight kümesi oluşturma](./media/hdinsight-apache-kafka-get-started/create-hdinsight.png)

2. Gelen **Temelleri**, aşağıdaki bilgilerle hello girin:

    * **Küme adı**: Merhaba Hdınsight kümesi hello adı.
    * **Abonelik**: hello abonelik toouse seçin.
    * **Oturum açma kullanıcı küme** ve **küme oturum açma parolasını**: hello küme HTTPS üzerinden erişirken hello oturum açma. Bu kimlik bilgileri tooaccess Hizmetleri gibi hello Ambari Web kullanıcı Arabirimi veya REST API'yi kullanın.
    * **Güvenli Kabuk (SSH) kullanıcıadı**: hello küme SSH üzerinden erişirken kullanılan hello oturum açma. Varsayılan olarak hello parola olduğu hello hello küme oturum açma parolası ile aynı.
    * **Kaynak grubu**: hello kaynak grubu toocreate hello kümede.
    * **Konum**: hello Azure bölgesi toocreate hello kümede.
   
 ![Abonelik seçme](./media/hdinsight-apache-kafka-get-started/hdinsight-basic-configuration.png)

3. Seçin **küme türü**, ve ardından kümesi hello aşağıdaki değerleri **küme yapılandırması**:
   
    * **Küme Türü**: Kafka

    * **Sürüm**: Kafka 0.10.0 (HDI 3.6)

    * **Küme Katmanı**: Standart
     
 Son olarak, hello kullan **seçin** düğmesini toosave ayarlar.
     
 ![Küme türü seçme](./media/hdinsight-apache-kafka-get-started/set-hdinsight-cluster-type.png)

4. Merhaba küme türü seçtikten sonra hello kullan __seçin__ düğme tooset hello küme türü. Ardından, hello kullanın __sonraki__ düğme toofinish temel yapılandırması.

5. **Depolama**’dan bir depolama hesabı seçin veya oluşturun. Bu belgedeki Hello adımlar için hello diğer alanları hello varsayılan değerleri bırakın. Kullanım hello __sonraki__ düğme toosave depolama yapılandırması.

    ![Hdınsight için Hello depolama hesabı ayarlarını belirleme](./media/hdinsight-apache-kafka-get-started/set-hdinsight-storage-account.png)

6. Gelen __uygulamaları (isteğe bağlı)__seçin __sonraki__ toocontinue. Bu örnek için uygulama gerekmez.

7. Gelen __küme boyutu__seçin __sonraki__ toocontinue.

    > [!WARNING]
    > Hdınsight üzerinde Kafka kullanılabilirliğini tooguarantee, kümenizi en az üç alt düğümleri içermesi gerekir.

    ![Set hello Kafka küme boyutu](./media/hdinsight-apache-kafka-get-started/kafka-cluster-size.png)

    > [!NOTE]
    > Merhaba **çalışan düğümü başına disk** giriş denetimlerini hello hdınsight'ta Kafka ölçeklenebilirliğini. Daha fazla bilgi için bkz. [HDInsight üzerinde Kafka'nın depolama alanını ve ölçeklenebilirliğini yapılandırma](hdinsight-apache-kafka-scalability.md).

8. Gelen __Gelişmiş ayarları__seçin __sonraki__ toocontinue.

9. Merhaba gelen **Özet**, hello kümesi için başlangıç yapılandırmasını gözden geçirin. Kullanım hello __Düzenle__ toochange yanlış ayarları bağlar. Son olarak, the__Create__ düğmesini toocreate hello küme kullanın.
   
    ![Küme yapılandırma özeti](./media/hdinsight-apache-kafka-get-started/hdinsight-configuration-summary.png)
   
    > [!NOTE]
    > Too20 dakika toocreate hello küme alabilir.

## <a name="connect-toohello-cluster"></a>Toohello kümesine bağlanın

> [!IMPORTANT]
> Aşağıdaki adımları hello gerçekleştirirken, bir SSH istemcisi kullanmanız gerekir. Daha fazla bilgi için bkz: Merhaba [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md) belge.

İstemcinizden, SSH tooconnect toohello küme kullanın:

```ssh SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net```

Değiştir **SSHUSER** ile küme oluşturma sırasında sağladığınız hello SSH kullanıcı adı. Değiştir **CLUSTERNAME** hello küme hello adı.

İstendiğinde, hello SSH hesabı için kullanılan hello parola girin.

Bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="getkafkainfo"></a>Merhaba Zookeeper ve Aracısı ana bilgisayar bilgilerini al

Kafka ile çalışırken, iki ana değer bilmeniz gerekir; Merhaba *Zookeeper* konakları ve hello *Aracısı* ana bilgisayar. Bu konaklar hello Kafka API ve birçok sevk hello yardımcı programlarını Kafka ile kullanılır.

Merhaba ana bilgisayar bilgilerini içeren adımları toocreate ortam değişkenleri aşağıdaki hello kullanın. Bu ortam değişkenleri, bu belgedeki hello adımda kullanılır.

1. Bir SSH bağlantısı toohello kümesinden kullanım hello şu komutu tooinstall hello `jq` yardımcı programı. Bu yardımcı program kullanılan tooparse JSON belgeleri olan ve hello Aracısı ana bilgisayar bilgilerini alma yararlıdır:
   
    ```bash
    sudo apt -y install jq
    ```

2. Ambari, aşağıdaki komutları kullanın hello bilgilerle tooset hello ortam değişkenleri alındı:

    ```bash
    CLUSTERNAME='your cluster name'
    PASSWORD='your cluster password'
    export KAFKAZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`

    export KAFKABROKERS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`

    echo '$KAFKAZKHOSTS='$KAFKAZKHOSTS
    echo '$KAFKABROKERS='$KAFKABROKERS
    ```

    > [!IMPORTANT]
    > Ayarlama `CLUSTERNAME=` hello Kafka küme toohello adı. Ayarlama `PASSWORD=` hello küme oluştururken kullandığınız toohello (Yönetici) oturum açma parolası.

    Merhaba aşağıdaki Merhaba içeriğine bir örnek metindir `$KAFKAZKHOSTS`:
   
    `zk0-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk2-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181`
   
    Merhaba aşağıdaki Merhaba içeriğine bir örnek metindir `$KAFKABROKERS`:
   
    `wn1-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092,wn0-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092`

    > [!NOTE]
    > Merhaba `cut` komutu kullanılan tootrim hello konakları tootwo konak girişleri listesi verilmiştir. Bir Kafka tüketici veya üretici oluştururken tooprovide hello tam ana bilgisayar listesini gerekmez.
   
    > [!WARNING]
    > Bu oturumda döndürülen hello bilgi tooalways doğru kullanmayın. Merhaba küme ölçeklendirme, yeni aracıların eklenir veya kaldırılır. Bir hata oluşur ve bir düğüm değiştirilir, hello düğümü hello ana bilgisayar adını değiştirebilir.
    >
    > Kısa süre içinde geçerli bilgilere sahip tooensure kullanabilmek hello Zookeeper ve Aracısı ana bilgisayar bilgilerini almak.

## <a name="create-a-topic"></a>Konu başlığı oluşturma

Kafka, veri akışlarını *topics* (konu başlıkları) adlı kategorilerde depolar. Bir SSH bağlantısı tooa küme headnode, bir konu Kafka toocreate ile sağlanan bir komut dosyasını kullanın:

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic test --zookeeper $KAFKAZKHOSTS
```

Bu komut, depolanan hello konak bilgileri kullanarak tooZookeeper bağlanır `$KAFKAZKHOSTS`ve ardından adlı Kafka konu Oluştur **test**. Bu hello konu aşağıdaki komut dosyası toolist konularda hello kullanılarak oluşturulmuş doğrulayabilirsiniz:

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $KAFKAZKHOSTS
```

Merhaba bu komutun çıktısı Kafka konuları, hello içeren listeler **test** konu.

## <a name="produce-and-consume-records"></a>Kayıt oluşturma ve kullanma

Kafka, konu başlıklarında *records* (kayıtlar) depolar. Kayıtlar, *Üreticiler* tarafından oluşturulur ve *tüketiciler* tarafından kullanılır. Üreticiler, kayıtları Kafka *aracılarından* alır. HDInsight kümenizdeki her çalışan düğümü bir Kafka aracısıdır.

Daha önce oluşturduğunuz ve bunları bir tüketici kullanarak okunur hello test konu ile aşağıdaki adımları toostore kayıtları hello kullan:

1. Merhaba SSH oturumundan Kafka toowrite kayıtları toohello konu ile sağlanan bir komut dosyasını kullanın:
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $KAFKABROKERS --topic test
    ```
   
    Toohello sonra bu komut istemi döndürülmez. Bunun yerine, birkaç metin iletileri yazın ve ardından **Ctrl + C** toostop toohello konu gönderme. Her satır ayrı bir kayıt olarak gönderilir.

2. Kafka tooread kayıtlarla hello konuda sağlanan komut dosyasını kullanın:
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic test --from-beginning
    ```
   
    Bu komut hello konusundan hello kayıtları alır ve bunları görüntüler. Kullanarak `--from-beginning` tüm kayıtlar alınır şekilde hello tüketici toostart hello hello akış başlangıcından söyler.

3. Kullanım __Ctrl + C__ toostop hello tüketici.

## <a name="producer-and-consumer-api"></a>Üretici ve tüketici API’si

Program aracılığıyla da oluşturabilir ve hello kullanarak kayıtları tüketen [Kafka API'leri](http://kafka.apache.org/documentation#api). toobuild Java üretici ve Tüketici ' hello geliştirme ortamınızı aşağıdaki adımları kullanın.

> [!IMPORTANT]
> Geliştirme ortamınızda yüklü bileşenleri aşağıdaki hello sahip olmanız gerekir:
>
> * [Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) veya OpenJDK gibi eşdeğeri.
>
> * [Apache Maven](http://maven.apache.org/)
>
> * Bir SSH istemcisi ve hello `scp` komutu. Daha fazla bilgi için bkz: Merhaba [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md) belge.

1. Merhaba örneklerinden karşıdan [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started). Merhaba üretici/tüketici örneğin hello projesi hello kullanmak `Producer-Consumer` dizin. Bu örnek sınıflar aşağıdaki hello içerir:
   
    * **Çalıştırma** -hello tüketici veya üretici başlatır.

    * **Üretici** -depoları 1.000.000 kayıtları toohello konu.

    * **Tüketici** -hello konusundan kayıtları okur.

2. toocreate jar paket dizinleri toohello hello konumunu değiştirme `Producer-Consumer` komutu aşağıdaki dizin ve kullanım hello:

    ```
    mvn clean package
    ```

    Bu komut, `kafka-producer-consumer-1.0-SNAPSHOT.jar` adlı dosyayı içeren `target` adlı bir dizin oluşturur.

3. Kullanım hello aşağıdaki komutları toocopy hello `kafka-producer-consumer-1.0-SNAPSHOT.jar` dosya tooyour Hdınsight kümesi:
   
    ```bash
    scp ./target/kafka-producer-consumer-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-producer-consumer.jar
    ```
   
    Değiştir **SSHUSER** kümesi ve Değiştir hello SSH kullanıcıyla **CLUSTERNAME** kümenizin hello ada sahip. İstendiğinde hello SSH kullanıcı için hello parola girin.

4. Bir kez hello `scp` komut bittikten hello dosya kopyalama, SSH kullanarak toohello kümesine bağlanın. Komut toowrite kayıtları toohello sınama konusu aşağıdaki hello kullan:

    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS
    ```

5. Merhaba işlemi tamamlandıktan sonra komutu tooread hello konusundan aşağıdaki hello kullan:
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS
    ```
   
    Merhaba kayıtları okuma, bir kayıt sayısı ile birlikte görüntülenir. Bir önceki adımda komut dosyası kullanarak birçok kayıtları toohello konu gönderilen olarak oturum 1.000.000 birden çok birkaç görebilirsiniz.

6. Kullanım __Ctrl + C__ tooexit hello tüketici.

### <a name="multiple-consumers"></a>Birden çok tüketici

Kafka tüketicileri kayıtları okurken bir tüketici grubu kullanır. Birden çok tüketiciye ile aynı grup hello kullanarak bir konu okuma sonuçları yük dengeli. Merhaba grubundaki her bir tüketici hello kayıtları bir kısmını alır. Bu eylem, aşağıdaki kullanım hello işlemde adımları toosee:

1. Yeni bir SSH oturumu toohello kümesi, iki tanesi sahip şekilde açın. Her oturumda hello kullan toostart ile bir tüketici hello aynı tüketici grubu kimliği:
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS mygroup
    ```

    Bu komut hello grup kimliği kullanan bir tüketici başlatır `mygroup`.

    > [!NOTE]
    > Hello Hello komutlarını kullanmak [hello Zookeeper ve Aracısı ana bilgisayar bilgilerini al](#getkafkainfo) bölüm tooset `$KAFKABROKERS` bu SSH oturumu için.

2. Merhaba konusundan aldığı her oturum sayıları hello kayıtları olarak izleyin. Her iki oturumunu Hello toplam olması hello aynı tek bir tüketici önceden alınmış olarak.

İstemciler aynı grup hello bölümler hello konu için aracılığıyla işlenmesini hello içinde tüketimi. Hello için `test` daha önce oluşturduğunuz konu sekiz bölümü vardır. Sekiz SSH oturumları açmak ve bir tüketici tüm oturumları başlatma, her bir tüketici hello konu için tek bir bölüm kayıtları okur.

> [!IMPORTANT]
> Bir tüketici grubunda bölümden daha fazla tüketici örneği olamaz. Hello hello konuda bölüm sayısı olduğundan bu örnekte, tooeight tüketicileri bir tüketici grubu içerebilir. Ya da her biri en fazla sekiz tüketici içeren birden fazla tüketici grubunuz olabilir.

Kayıtları Kafka içinde depolanan bir bölüm içinde alınan hello sırayla depolanır. tooachieve-sıralı teslim kayıtlar için *bölüm içinde*, hello tüketici örneklerinin sayısını hello bölüm sayısı eşleştiği bir tüketici grubu oluşturun. tooachieve-sıralı teslim kayıtlar için *hello konusu içinde*, yalnızca tek bir tüketici örneği ile bir tüketici grubu oluşturun.

## <a name="streaming-api"></a>Akış API’si

API akış hello tooKafka sürüm 0.10.0 eklendi; önceki sürümlerde, Apache Spark veya Storm akış işleme için kullanır.

1. Zaten yapmadıysanız, hello örneklerinden karşıdan [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) tooyour geliştirme ortamı. Örnek akış Merhaba hello projesi hello kullanmak `streaming` dizin.
   
    Bu proje yalnızca bir sınıf içeriyor `Stream`, hello kayıtları okur `test` daha önce oluşturulan konu. Okuma hello sözcükleri sayar ve adlı her word ve sayısı tooa konu yayar `wordcounts`. Merhaba `wordcounts` konu bu bölümde daha sonraki bir adımda oluşturulur.

2. Merhaba komut satırından geliştirme ortamınızda, dizinleri toohello hello konumunu değiştirmek `Streaming` dizin ve komut toocreate jar paketi aşağıdaki kullanım hello:

    ```bash
    mvn clean package
    ```

    Bu komut, `kafka-streaming-1.0-SNAPSHOT.jar` adlı dosyayı içeren `target` adlı bir dizin oluşturur.

3. Kullanım hello aşağıdaki komutları toocopy hello `kafka-streaming-1.0-SNAPSHOT.jar` dosya tooyour Hdınsight kümesi:
   
    ```bash
    scp ./target/kafka-streaming-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-streaming.jar
    ```
   
    Değiştir **SSHUSER** kümesi ve Değiştir hello SSH kullanıcıyla **CLUSTERNAME** kümenizin hello ada sahip. İstendiğinde hello SSH kullanıcı için hello parola girin.

4. Bir kez hello `scp` komutu hello dosya kopyalama tamamlanmadan, SSH kullanarak toohello kümesine bağlanın ve sonra komut toocreate hello aşağıdaki hello `wordcounts` konu:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic wordcounts --zookeeper $KAFKAZKHOSTS
    ```

5. Ardından, komutu aşağıdaki hello kullanarak işlem akış hello başlatın:
   
    ```bash
    java -jar kafka-streaming.jar $KAFKABROKERS $KAFKAZKHOSTS 2>/dev/null &
    ```
   
    Bu komut hello arka planda işlem akış hello başlatır.

6. Kullanım hello şu komutu toosend iletileri toohello `test` konu. Bu iletiler örnek akış hello tarafından işlenir:
   
    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS &>/dev/null &
    ```

7. Kullanım hello toohello yazılan komut tooview hello çıktısı aşağıdaki `wordcounts` konusuna göre işlem akış hello:
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic wordcounts --from-beginning --formatter kafka.tools.DefaultMessageFormatter --property print.key=true --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
    ```
   
    > [!NOTE]
    > tooview hello veri hello tüketici tooprint hello anahtarı ve hello seri durumdan çıkarıcının toouse hello anahtar ve değer bildirmeniz gerekir. Merhaba anahtar adı hello sözcüktür ve hello sayısı hello anahtar değeri içerir.
   
    Merhaba, benzer toohello metin aşağıdaki çıktı:
   
        dwarfs  13635
        ago     13664
        snow    13636
        dwarfs  13636
        ago     13665
        a       13803
        ago     13666
        a       13804
        ago     13667
        ago     13668
        jumped  13640
        jumped  13641
        a       13805
        snow    13637
   
    > [!NOTE]
    > her zaman bir sözcük karşılaştı Hello sayısını artırır.

7. Merhaba kullanmak __Ctrl + C__ tooexit hello tüketici sonra hello kullanın `fg` toobring hello akış arka plan görevi geri toohello ön komutu. Kullanım __Ctrl + C__ tooexit, ayrıca.

## <a name="delete-hello-cluster"></a>Merhaba küme silme

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Sorun giderme

HDInsight kümeleri oluştururken sorun yaşarsanız bkz. [erişim denetimi gereksinimleri](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Sonraki adımlar

Bu belgede, Hdınsight üzerinde Apache Kafka ile çalışmanın temelleri hello öğrendiniz. Kafka ile çalışma hakkında daha fazla toolearn aşağıdaki hello kullan:

* [HDInsight üzerinde Kafka ile verilerinizin yüksek kullanılabilirliğini sağlama](hdinsight-apache-kafka-high-availability.md)
* [HDInsight üzerinde Kafka ile yönetilen diskleri yapılandırarak ölçeklenebilirliği artırma](hdinsight-apache-kafka-scalability.md)
* kafka.apache.org adresindeki [Apache Kafka belgeleri](http://kafka.apache.org/documentation.html).
* [Hdınsight üzerinde MirrorMaker toocreate Kafka bir kopyasını kullan](hdinsight-apache-kafka-mirroring.md)
* [Apache Storm’u HDInsight üzerinde Kafka ile kullanma](hdinsight-apache-storm-with-kafka.md)
* [Apache Spark’ı HDInsight üzerinde Kafka ile kullanma](hdinsight-apache-spark-with-kafka.md)
* [Bir Azure sanal ağı tooKafka Bağlan](hdinsight-apache-kafka-connect-vpn-gateway.md)
