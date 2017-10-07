---
title: "aaaApache Spark yapılandırılmış akış Kafka - Azure Hdınsight ile | Microsoft Docs"
description: "Bilgi nasıl toouse Apache Spark akış (DStream) tooget verilerini içine veya dışına Apache Kafka. Bu örnekte, Hdınsight'ta Spark gelen Jupyter Not Defteri kullanarak veri akışı."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/09/2017
ms.author: larryfr
ms.openlocfilehash: 0837e8fc5ea314e644daed029d596feeb2b02c68
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-spark-structured-streaming-with-kafka-preview-on-hdinsight"></a>Hdınsight'ta Spark yapılandırılmış akış Kafka (Önizleme) ile kullanma

Bilgi nasıl toouse tooread verilerden Spark yapılandırılmış akış Azure hdınsight'ta Apache Kafka.

Yapılandırılmış Spark akış Spark SQL yerleşik bir akış işleme altyapısıdır. Bu, tooexpress akış hesaplamalar hello toplu hesaplama aynı statik verileri sağlar. Merhaba yapılandırılmış akışı hakkında daha fazla bilgi için bkz: [yapılandırılmış akış Programlama Kılavuzu [alfa]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) Apache.org.

> [!IMPORTANT]
> Bu örnek, Hdınsight 3.6 üzerinde Spark 2.1 kullanılır. Yapılandırılmış akış olarak kabul __alfa__ Spark 2.1 üzerinde.
>
> Bu belgedeki Hello adımlar hem hdınsight'ta Spark ve Hdınsight kümesinde bir Kafka içeren bir Azure kaynak grubu oluşturun. Bu kümeleri, hem bir Azure sanal hello Spark küme toodirectly sağlayan ağ içinde bulunan Kafka küme hello ile iletişim ' dir.
>
> Bu belgedeki hello adımları tamamladığınızda, toodelete hello kümeleri tooavoid aşırı ücretleri unutmayın.

## <a name="create-hello-clusters"></a>Merhaba kümeleri oluşturma

Hdınsight üzerinde Apache Kafka sağlamaz erişim toohello Kafka aracıların üzerinden genel internet hello. Merhaba düğümler aynı Azure sanal ağ konuşmaları tooKafka olmalıdır hello herhangi bir şey Kafka küme hello. Bu örnekte, bir Azure sanal ağında hello Kafka ve Spark kümeleri bulunur. Merhaba Aşağıdaki diyagramda hello kümeleri arasında iletişimi nasıl akacağını gösterilmektedir:

![Bir Azure sanal ağı Spark ve Kafka kümelerde diyagramı](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> Merhaba Kafka hizmet hello sanal ağ içindeki sınırlı toocommunication ' dir. Merhaba kümedeki diğer hizmetler gibi SSH ve Ambari, erişilebilir üzerinden internet hello. Merhaba ortak bağlantı noktaları Hdınsight ile kullanılabilir hakkında daha fazla bilgi için bkz: [bağlantı noktaları ve Hdınsight tarafından kullanılan URI](hdinsight-hadoop-port-settings-for-services.md).

Azure sanal ağı, Kafka ve Spark kümeleri el ile oluşturabileceğiniz olsa da, daha kolay toouse bir Azure Resource Manager şablonu durumdur. Toodeploy Azure sanal ağı, Kafka, kullanım hello aşağıdaki adımları ve tooyour Azure aboneliği Spark kümeleri.

1. Düğme toosign tooAzure içinde ve açık hello şablonunda hello Azure portalı aşağıdaki hello kullanın.
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v4.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    Hello Azure Resource Manager şablonu konumundadır **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.

    Bu şablon, kaynakları aşağıdaki hello oluşturur:

    * Hdınsight 3.5 kümede Kafka.
    * Bir Spark Hdınsight 3.6 kümede.
    * Bir Azure sanal hello Hdınsight kümeleri içeren ağ.

    > [!IMPORTANT]
    > Bu örnekte kullanılan hello yapılandırılmış akış not defteri Spark Hdınsight 3.6 gerektirir. Hdınsight'ta Spark önceki bir sürümünü kullanıyorsanız, hello dizüstü bilgisayar kullanırken hataları alırsınız.

2. Bilgi toopopulate hello girişleri hello üzerinde aşağıdaki kullanım hello **özel dağıtım** dikey penceresinde:
   
    ![Hdınsight özel dağıtım](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * **Kaynak grubu**: bir grup oluşturun veya varolan bir tanesini seçin. Bu grup hello Hdınsight kümesi içerir.

    * **Konum**: konum coğrafi olarak Kapat tooyou seçin.

    * **Temel küme adı**: Bu değer hello Spark ve Kafka kümelerinin hello temel adı olarak kullanılır. Örneğin, **hdı** bir Spark spark hdi__ adlı Küme ve adlı bir Kafka kümesi oluşturur **kafka hdı**.

    * **Oturum açma kullanıcı adı küme**: hello Spark ve Kafka kümelerinin hello Yöneticisi kullanıcı adı.

    * **Oturum açma parolası küme**: hello Spark ve Kafka kümeleri için hello yönetici kullanıcı parolası.

    * **SSH kullanıcı adı**: SSH kullanıcı toocreate hello Spark ve Kafka kümelerinin hello.

    * **SSH parolası**: hello SSH kullanıcı hello Spark ve Kafka kümelerinin hello parolası.

3. Okuma hello **hüküm ve koşullar**ve ardından **toohello hüküm ve koşullar yukarıda belirtildiği kabul**.

4. Son olarak, denetleme **PIN toodashboard** ve ardından **satın alma**. Merhaba kümeleri toocreate yaklaşık 20 dakika sürer.

Merhaba kaynakları oluşturduktan sonra yeniden yönlendirilen toohello kaynak grubu dikey demektir.

![Kaynak grubu dikey hello vnet ve kümeler için](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> Merhaba Hdınsight kümeleri Hello adlarını olduğuna dikkat edin **spark BASENAME** ve **kafka BASENAME**, BASENAME toohello şablonu sağladığınız hello adı olduğu. Bu adları toohello kümeleri bağlanırken daha sonraki adımlarda kullanın.

## <a name="get-hello-kafka-brokers"></a>Aracıların Hello Kafka Al

Merhaba bu örnekteki kod bağlayan toohello Kafka Aracısı hello Kafka küme ana bilgisayarlar. toofind Kafka Aracısı konakları Merhaba, aşağıdaki PowerShell veya Bash örneğine hello kullanın:

```powershell
$creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
$clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
$resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
    -Credential $creds
$respObj = ConvertFrom-Json $resp.Content
$brokerHosts = $respObj.host_components.HostRoles.host_name
($brokerHosts -join ":9092,") + ":9092"
```

```bash
curl -u admin:$PASSWORD -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")'
```

> [!NOTE]
> Bu örnek bekliyor `$PASSWORD` toocontain hello hello küme oturum açma, parolasını ve `$CLUSTERNAME` toocontain hello hello Kafka küme adını.
>
> Bu örnek hello kullanır [jq](https://stedolan.github.io/jq/) yardımcı programı tooparse veri hello JSON belgesi dışında.

Merhaba, benzer toohello metin aşağıdaki çıktı:

`wn0-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn1-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn2-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn3-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092`

Aşağıdaki bölümlerde bu belgenin hello kullanılmak üzere bu bilgileri kaydedin.

## <a name="get-hello-notebooks"></a>Merhaba not defterlerini Al

Bu belgede açıklanan hello örneğin Hello kod şu adreste [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).

## <a name="upload-hello-notebooks"></a>Merhaba not defterlerini karşıya yükle

Adımları tooupload hello not defterlerini hello proje tooyour Spark Hdınsight kümesinde aşağıdaki hello kullan:

1. Web tarayıcınızda toohello Jupyter Not Defteri, Spark kümesinde bağlayın. URL, aşağıdaki Hello yerine `CLUSTERNAME` Kafka kümenizi hello adı:

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    İstendiğinde, hello küme oturum açma (Yönetici) ve hello küme oluştururken kullanılan parolayı girin.

2. Merhaba Hello üst sağından hello sayfasında, kullanmak __karşıya__ düğmesini tooupload hello __akış Tweet'leri To_Kafka.ipynb__ dosya toohello kümesi. Seçin __açık__ toostart hello karşıya yükleme.

    ![Merhaba karşıya yükleme düğmesini tooselect kullanın ve bir dizüstü bilgisayara yüklemek](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-button.png)

    ![Merhaba KafkaStreaming.ipynb dosyasını seçin](./media/hdinsight-apache-kafka-spark-structured-streaming/select-notebook.png)

3. Hello bulur __akış Tweet'leri To_Kafka.ipynb__ not defterlerini seçin ve hello listesi girişi __karşıya__ yanında düğmesi.

    ![Merhaba KafkaStreaming.ipynb girişi tooupload, toohello not defteri sunucu düğmesini kullanın hello karşıya yükleme](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-notebook.png)

4. 1-3 tooload hello arasındaki adımları yineleyin __Spark-yapılandırılmış-akış-gelen-Kafka.ipynb__ dizüstü bilgisayar.

## <a name="load-tweets-into-kafka"></a>Yük tweet'leri Kafka içine

Merhaba dosyaları karşıya sonra hello seçeneğini __akış Tweet'leri To_Kafka.ipynb__ girişi tooopen hello Not. Kafka hello not defteri tooload tweet'leri Hello adımları izleyin.

## <a name="process-tweets-using-spark-structured-streaming"></a>İşlem tweet'leri Spark yapılandırılmış akış kullanma

Merhaba Hello ifadesini Jupyter not defteri giriş sayfası seçin __Spark-yapılandırılmış-akış-gelen-Kafka.ipynb__ girişi. Spark yapılandırılmış akış kullanarak Kafka hello not defteri tooload tweet'leri Hello adımları izleyin.

## <a name="next-steps"></a>Sonraki adımlar

Artık öğrendiğinize göre nasıl toouse Spark yapılandırılmış akış, belgeleri toolearn Spark ve Kafka ile çalışma hakkında daha fazla bilgi aşağıdaki hello bakın:

* [Nasıl toouse Spark Kafka ile akış (DStream)](hdinsight-apache-spark-with-kafka.md).
* [Jupyter not defteri ve hdınsight'ta Spark ile Başlat](hdinsight-apache-spark-jupyter-spark-sql.md)