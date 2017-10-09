---
title: "aaaMirror Apache Kafka konuları - Azure Hdınsight | Microsoft Docs"
description: "Nasıl toouse Apache Kafka'nın yansıtma özelliği toomaintain Kafka Hdınsight kümesinde bir kopyasını konuları tooa ikincil küme yansıtma tarafından öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 015d276e-f678-4f2b-9572-75553c56625b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: 5ace0251d7402d4d7d9b28726e253ce7091a87ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-mirrormaker-tooreplicate-apache-kafka-topics-with-kafka-on-hdinsight-preview"></a>(Önizleme) hdınsight'ta Kafka ile MirrorMaker tooreplicate Apache Kafka konuları kullanın

Toouse Apache Kafka özelliği tooreplicate konuları tooa ikincil küme nasıl yansıtma öğrenin. Yansıtma bulunabilir sürekli bir işlem olarak çalışan, veya zaman zaman geçiş işleminin bir yöntem olarak kullanılan bir veri kümesi tooanother.

Bu örnekte, yansıtma kullanılan tooreplicate konular iki Hdınsight kümeleri arasında değil. Her iki küme hello bir Azure sanal ağında bulunan aynı bölgede.

> [!WARNING]
> Yansıtma, bir yol tooachieve hataya dayanıklılık düşünülmemelidir. istemcileri hello iki birbirinin yerine kullanamazlar hello uzaklık tooitems konu içinde hello kaynak ve hedef kümeler arasında farklılık gösterir.
>
> Hataya dayanıklılık hakkında endişeleriniz varsa, küme içinde çoğaltma hello konular için ayarlamanız gerekir. Daha fazla bilgi için bkz: [Kafka hdınsight kullanmaya başlama](hdinsight-apache-kafka-get-started.md).

## <a name="how-kafka-mirroring-works"></a>Yansıtma Kafka nasıl çalışır?

Hello MirrorMaker Aracı (Apache Kafka parçası) tooconsume kullanarak yansıtma works hello kaynak kümesi konulardan kaydeder ve sonra hello hedef kümede yerel bir kopyasını oluşturun. MirrorMaker kullanan bir (veya daha fazla) *tüketicileri* hello kaynak kümeden okuyan ve *üretici* toohello yerel (hedef) küme yazar.

Aşağıdaki diyagramda hello hello yansıtma işlemi gösterilmektedir:

![İşlem yansıtma hello diyagramı](./media/hdinsight-apache-kafka-mirroring/kafka-mirroring.png)

Hdınsight üzerinde Apache Kafka hello erişim toohello Kafka hizmet sağlamaz genel internet. Kafka üreticileri ya da tüketicilere hello olmalıdır hello Kafka küme hello düğümler aynı Azure sanal ağ. Bu örnekte, bir Azure sanal ağında hello Kafka kaynak ve hedef kümeler bulunur. Merhaba Aşağıdaki diyagramda hello kümeleri arasında iletişimi nasıl akacağını gösterilmektedir:

![Kaynak ve hedef Kafka diyagramı bir Azure sanal ağında kümeleri](./media/hdinsight-apache-kafka-mirroring/spark-kafka-vnet.png)

Merhaba kaynak ve hedef kümeler hello sayısında düğümleri ve bölümleri farklı olabilir ve uzaklıkları hello konuları içinde de farklıdır. Kayıt siparişi bir anahtar başına temelinde korunacak şekilde yansıtma bölümleme için kullanılan hello anahtar değerini korur.

### <a name="mirroring-across-network-boundaries"></a>Ağ sınırları boyunca yansıtma

Farklı ağlarda Kafka kümeler arasında toomirror gerekiyorsa, ek hususlar aşağıdaki hello vardır:

* **Ağ geçitleri**: hello ağları hello TCPIP düzeyi adresindeki mümkün toocommunicate olması gerekir.

* **Ad çözümlemesi**: ana bilgisayar adları kullanarak Kafka kümeleri her ağın hello tooeach mümkün tooconnect diğer olmalıdır. Bu, bir etki alanı adı sistemi (DNS) sunucusu olduğu her ağdaki diğer ağlara tooforward istekleri toohello yapılandırılmış gerektirebilir.

    Bir Azure sanal hello ağla otomatik DNS sağlanan hello yerine ağ oluşturulurken bir özel DNS sunucusu ve hello sunucusu için IP adresi hello belirtmeniz gerekir. Hello sanal ağ oluşturulduktan sonra ardından bu IP adresini kullanan bir Azure sanal makine oluşturun ardından yükleyin ve DNS yazılım üzerinde yapılandırmanız gerekir.

    > [!WARNING]
    > Oluşturun ve sanal ağ hello Hdınsight yüklemeden önce hello özel DNS sunucusunu yapılandırın. Merhaba sanal ağ için yapılandırılan Hdınsight toouse hello DNS sunucusu için gereken ek yapılandırma yoktur.

İki Azure sanal ağları bağlama ile ilgili daha fazla bilgi için bkz: [VNet-VNet bağlantı yapılandırma](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).

## <a name="create-kafka-clusters"></a>Kafka kümeleri oluşturma

Bir Azure sanal ağı oluşturmak ve Kafka el ile kümeleri olsa da, daha kolay toouse bir Azure Resource Manager şablonu durumdur. Aşağıdaki adımları toodeploy hello Azure sanal ağı ve iki Kafka kümeleri tooyour Azure aboneliği kullanın.

1. Düğme toosign tooAzure içinde ve açık hello şablonunda hello Azure portalı aşağıdaki hello kullanın.
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-kafka-mirroring/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    Hello Azure Resource Manager şablonu konumundadır **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.

    > [!WARNING]
    > Hdınsight üzerinde Kafka kullanılabilirliğini tooguarantee, kümenizi en az üç alt düğümleri içermesi gerekir. Bu şablon, üç alt düğümleri içeren bir Kafka küme oluşturur.

2. Bilgi toopopulate hello girişleri hello üzerinde aşağıdaki kullanım hello **özel dağıtım** dikey penceresinde:
    
    ![Hdınsight özel dağıtım](./media/hdinsight-apache-kafka-mirroring/parameters.png)
    
    * **Kaynak grubu**: bir grup oluşturun veya varolan bir tanesini seçin. Bu grup hello Hdınsight kümesi içerir.

    * **Konum**: konum coğrafi olarak Kapat tooyou seçin.
     
    * **Temel küme adı**: Bu değer hello Kafka kümeleri için hello temel adı olarak kullanılır. Örneğin, **hdı** adlı kümeleri oluşturur **kaynak hdı** ve **taşınmaya hdı**.

    * **Oturum açma kullanıcı adı küme**: hello kaynak ve hedef için hello yönetici kullanıcı adı Kafka kümeleri.

    * **Oturum açma parolası küme**: Merhaba yönetici kullanıcı parolasını hello kaynak ve hedef Kafka kümeleri.

    * **SSH kullanıcı adı**: hello SSH kullanıcı toocreate hello kaynak ve hedef için Kafka kümeleri.

    * **SSH parolası**: hello parola hello SSH kullanıcı hello kaynak ve hedef için Kafka kümeleri.

3. Okuma hello **hüküm ve koşullar**ve ardından **toohello hüküm ve koşullar yukarıda belirtildiği kabul**.

4. Son olarak, denetleme **PIN toodashboard** ve ardından **satın alma**. Merhaba kümeleri toocreate yaklaşık 20 dakika sürer.

Merhaba kaynakları oluşturduktan sonra yeniden yönlendirilen tooa dikey penceresinde hello kümeleri ve web Pano içeren hello kaynak grubu için demektir.

![Kaynak grubu dikey hello vnet ve kümeler için](./media/hdinsight-apache-kafka-mirroring/groupblade.png)

> [!IMPORTANT]
> Merhaba Hdınsight kümeleri Hello adlarını olduğuna dikkat edin **kaynak BASENAME** ve **taşınmaya BASENAME**, BASENAME toohello şablonu sağladığınız hello adı olduğu. Bu adları toohello kümeleri bağlanırken daha sonraki adımlarda kullanın.

## <a name="create-topics"></a>Konuları oluşturun

1. Toohello bağlanmak **kaynak** SSH kullanarak küme:

    ```bash
    ssh sshuser@source-BASENAME-ssh.azurehdinsight.net
    ```

    Değiştir **sshuser** hello küme oluşturulurken kullanılan hello SSH kullanıcı adı. Değiştir **BASENAME** hello küme oluşturulurken kullanılan hello temel ada sahip.

    Bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Kullanım hello aşağıdaki toofind hello Zookeeper konakları hello kaynak kümesi için komutlar:

    ```bash
    # Install jq if it is not installed
    sudo apt -y install jq
    # get hello zookeeper hosts for hello source cluster
    export SOURCE_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    
    Replace `$PASSWORD` with hello password for hello cluster.

    Replace `$CLUSTERNAME` with hello name of hello source cluster.

3. toocreate a topic named `testtopic`, use hello following command:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 2 --partitions 8 --topic testtopic --zookeeper $SOURCE_ZKHOSTS
    ```

3. Konu hello komutu tooverify aşağıdaki kullanım hello oluşturuldu:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $SOURCE_ZKHOSTS
    ```

    Merhaba yanıtını içeren `testtopic`.

4. Bu tooview hello Zookeeper ana bilgisayar bilgilerini aşağıdaki kullanım hello (Merhaba **kaynak**) küme:

    ```bash
    echo $SOURCE_ZKHOSTS
    ```

    Bu metin aşağıdaki bilgileri benzer toohello döndürür:

    `zk0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181,zk1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181`

    Bu bilgileri kaydedin. Merhaba sonraki bölümde kullanılır.

## <a name="configure-mirroring"></a>Yansıtmasını yapılandırma

1. Toohello bağlanmak **hedef** küme farklı bir SSH oturumu kullanarak:

    ```bash
    ssh sshuser@dest-BASENAME-ssh.azurehdinsight.net
    ```

    Değiştir **sshuser** hello küme oluşturulurken kullanılan hello SSH kullanıcı adı. Değiştir **BASENAME** hello küme oluşturulurken kullanılan hello temel ada sahip.

    Bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Kullanım hello şu komutu toocreate bir `consumer.properties` açıklayan dosyasının nasıl hello ile toocommunicate **kaynak** küme:

    ```bash
    nano consumer.properties
    ```

    Metin hello Merhaba içeriğine aşağıdaki kullanım hello `consumer.properties` dosyası:

    ```yaml
    zookeeper.connect=SOURCE_ZKHOSTS
    group.id=mirrorgroup
    ```

    Değiştir **SOURCE_ZKHOSTS** ile Merhaba Zookeeper hello bilgilerinden barındıran **kaynak** küme.

    Bu dosya, Kafka küme hello kaynağından okunurken hello tüketici bilgi toouse tanımlar. Daha fazla bilgi tüketici yapılandırma için bkz: [tüketici yapılandırmalar](https://kafka.apache.org/documentation#consumerconfigs) kafka.apache.org adresindeki.

    toosave hello dosya, kullanım **Ctrl + X**, **Y**ve ardından **Enter**.

3. Hello hedef küme ile iletişim kurar hello üretici yapılandırmadan önce hello Aracısı konakları Merhaba bulmalıdır **hedef** küme. Aşağıdaki komutları tooretrieve hello bu bilgileri kullanın:

    ```bash
    sudo apt -y install jq
    DEST_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    echo $DEST_BROKERHOSTS
    ```

    Değiştir `$PASSWORD` parolayla hello oturum açma hesabı (Yönetici) hello kümesi için.

    Değiştir `$CLUSTERNAME` hello hedef küme hello adı.

    Bu komutlar bilgi benzer toohello aşağıdaki döndürün:

        wn0-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn1-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092

4. Kullanım hello toocreate izleyen bir `producer.properties` açıklayan dosyasının nasıl hello ile toocommunicate **hedef** küme:

    ```bash
    nano producer.properties
    ```

    Metin hello Merhaba içeriğine aşağıdaki kullanım hello `producer.properties` dosyası:

    ```yaml
    bootstrap.servers=DEST_BROKERS
    compression.type=none
    ```

    Değiştir **DEST_BROKERS** hello önceki adımdaki hello Aracısı bilgilerle.

    Daha fazla bilgi üretici yapılandırma için bkz: [üretici yapılandırmalar](https://kafka.apache.org/documentation#producerconfigs) kafka.apache.org adresindeki.

## <a name="start-mirrormaker"></a>MirrorMaker Başlat

1. Merhaba SSH bağlantı toohello gelen **hedef** küme, komut toostart hello MirrorMaker işlemi aşağıdaki hello kullanın:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-run-class.sh kafka.tools.MirrorMaker --consumer.config consumer.properties --producer.config producer.properties --whitelist testtopic --num.streams 4
    ```

    Bu örnekte kullanılan hello Parametreler şunlardır:

    * **--consumer.config**: tüketici özellikleri içeren hello dosyasını belirtir. Bu özellikler kullanılan toocreate hello okuyan bir tüketici: *kaynak* Kafka küme.

    * **--producer.config**: üretici özellikleri içeren hello dosyasını belirtir. Bu özellikler kullanılan toocreate toohello Yazar bir üretici: *hedef* Kafka küme.

    * **--beyaz liste**: hello kaynak küme toohello hedef MirrorMaker çoğaltır konuların listesi.

    * **--num.streams**: Merhaba tüketici iş parçacığı toocreate sayısı.

 Başlangıç sırasında aşağıdaki metin bilgi benzer toohello MirrorMaker döndürür:

    ```json
    {metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-3, security.protocol=PLAINTEXT}{metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-0, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-kafka.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-2, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-1, security.protocol=PLAINTEXT}
    ```

2. Merhaba SSH bağlantı toohello gelen **kaynak** küme, komut toostart bir üretici aşağıdaki hello kullanın ve iletileri toohello konu gönderin:

    ```bash
    SOURCE_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $SOURCE_BROKERHOSTS --topic testtopic
    ```

    Değiştir `$PASSWORD` hello kaynak kümesi için hello oturum açma (Yönetici) parolayla.

    Değiştir `$CLUSTERNAME` hello kaynak kümesi hello adı.

     Boş bir satırı bir imleç ile geldiğinde, birkaç metin iletileri yazın. Bunlar toohello konu üzerinde hello gönderilen **kaynak** küme. İşiniz bittiğinde, kullanın **Ctrl + C** tooend hello üretici işlemi.

3. Merhaba SSH bağlantı toohello gelen **hedef** küme, kullanın **Ctrl + C** tooend hello MirrorMaker işlemi. Bu hello tooverify kullanım hello aşağıdaki komutları sonra `testtopic` konu oluşturuldu ve bu verileri hello konudaki çoğaltılmış toothis yansıtma idi:

    ```bash
    DEST_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $DEST_ZKHOSTS
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $DEST_ZKHOSTS --topic testtopic --from-beginning
    ```

    Değiştir `$PASSWORD` hello hedef küme için hello oturum açma (Yönetici) parolayla.

    Değiştir `$CLUSTERNAME` hello hedef küme hello adı.

    Merhaba konuların listesi şimdi içeren `testtopic`, MirrorMaster hello kaynak küme toohello hedef hello konusundan yansıtan zaman oluşturuldu. Merhaba konusundan alınan hello iletileri hello kaynak kümede girilen aynı hello ' dir.

## <a name="delete-hello-cluster"></a>Merhaba küme silme

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Merhaba adımlar bu belgedeki her ikisi de oluşturma beri kümelerde Merhaba aynı Azure kaynak grubu, hello Azure portal hello kaynak grubunu silebilirsiniz. Bu belge, hello Azure sanal ağ ve depolama hesabı hello kümeleri tarafından kullanılan uygulayarak oluşturduğunuz tüm kaynakları silme hello kaynak grubunu kaldırır.

## <a name="next-steps"></a>Sonraki Adımlar

Bu belgede nasıl toouse MirrorMaker toocreate bir Kafka çoğaltmasını küme öğrendiniz. Aşağıdaki bağlantılar toodiscover hello diğer yolları toowork Kafka ile kullanın:

* [Apache Kafka MirrorMaker belgelerine](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) cwiki.apache.org adresindeki.
* [Hdınsight üzerinde Apache Kafka kullanmaya başlama](hdinsight-apache-kafka-get-started.md)
* [Apache Spark’ı HDInsight üzerinde Kafka ile kullanma](hdinsight-apache-spark-with-kafka.md)
* [Apache Storm’u HDInsight üzerinde Kafka ile kullanma](hdinsight-apache-storm-with-kafka.md)
* [Bir Azure sanal ağı tooKafka Bağlan](hdinsight-apache-kafka-connect-vpn-gateway.md)
