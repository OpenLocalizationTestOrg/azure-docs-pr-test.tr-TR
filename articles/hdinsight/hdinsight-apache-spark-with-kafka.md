---
title: "aaaApache Spark Kafka - Azure Hdınsight akış | Microsoft Docs"
description: "Bilgi nasıl toouse Spark Apache Spark toostream veri ya da Apache DStreams kullanarak Kafka dışında. Bu örnekte, Hdınsight'ta Spark gelen Jupyter Not Defteri kullanarak veri akışı."
keywords: "kafka örnek, kafka zookeeper spark kafka, kafka örnek Spark Akış akış"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: dd8f53c1-bdee-4921-b683-3be4c46c2039
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: f48b37aadafa4979cd27af68e8417db6acc8a0e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-dstream-example-with-kafka-preview-on-hdinsight"></a>Apache Spark Hdınsight üzerinde Kafka (Önizleme) ile (DStream) örnek akış

Bilgi nasıl toouse Spark Apache Spark toostream veri içine veya dışına DStreams kullanarak Hdınsight üzerinde Apache Kafka. Bu örnek hello Spark kümesinde çalışan bir Jupyter not defteri kullanır.
> [!NOTE]
> Bu belgedeki Hello adımlar hem hdınsight'ta Spark ve Hdınsight kümesinde bir Kafka içeren bir Azure kaynak grubu oluşturun. Bu kümeleri, hem bir Azure sanal hello Spark küme toodirectly sağlayan ağ içinde bulunan Kafka küme hello ile iletişim ' dir.
>
> Bu belgedeki hello adımları tamamladığınızda, toodelete hello kümeleri tooavoid aşırı ücretleri unutmayın.

## <a name="create-hello-clusters"></a>Merhaba kümeleri oluşturma

Hdınsight üzerinde Apache Kafka sağlamaz erişim toohello Kafka aracıların üzerinden genel internet hello. Merhaba düğümler aynı Azure sanal ağ konuşmaları tooKafka olmalıdır hello herhangi bir şey Kafka küme hello. Bu örnekte, bir Azure sanal ağında hello Kafka ve Spark kümeleri bulunur. Merhaba Aşağıdaki diyagramda hello kümeleri arasında iletişimi nasıl akacağını gösterilmektedir:

![Bir Azure sanal ağı Spark ve Kafka kümelerde diyagramı](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> Kafka kendisini hello sanal ağ içindeki sınırlı toocommunication olsa da, SSH ve Ambari üzerinden erişilebilen gibi diğer hizmetler hello kümede Internet hello. Merhaba ortak bağlantı noktaları Hdınsight ile kullanılabilir hakkında daha fazla bilgi için bkz: [bağlantı noktaları ve Hdınsight tarafından kullanılan URI](hdinsight-hadoop-port-settings-for-services.md).

Azure sanal ağı, Kafka ve Spark kümeleri el ile oluşturabileceğiniz olsa da, daha kolay toouse bir Azure Resource Manager şablonu durumdur. Toodeploy Azure sanal ağı, Kafka, kullanım hello aşağıdaki adımları ve tooyour Azure aboneliği Spark kümeleri.

1. Düğme toosign tooAzure içinde ve açık hello şablonunda hello Azure portalı aşağıdaki hello kullanın.
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    Hello Azure Resource Manager şablonu konumundadır **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.

    > [!WARNING]
    > Hdınsight üzerinde Kafka kullanılabilirliğini tooguarantee, kümenizi en az üç alt düğümleri içermesi gerekir. Bu şablon, üç alt düğümleri içeren bir Kafka küme oluşturur.

    Bu şablon, Kafka hem Spark Hdınsight 3.6 küme oluşturur.

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

Merhaba kaynakları oluşturduktan sonra yeniden yönlendirilen tooa dikey penceresinde hello kümeleri ve web Pano içeren hello kaynak grubu için demektir.

![Kaynak grubu dikey hello vnet ve kümeler için](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> Merhaba Hdınsight kümeleri Hello adlarını olduğuna dikkat edin **spark BASENAME** ve **kafka BASENAME**, BASENAME toohello şablonu sağladığınız hello adı olduğu. Bu adları toohello kümeleri bağlanırken daha sonraki adımlarda kullanın.

## <a name="use-hello-notebooks"></a>Merhaba not defterlerini kullanma

Bu belgede açıklanan hello örneğin Hello kod şu adreste [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).

Merhaba Hello adımları `README.md` toocomplete Bu örnek dosya.

## <a name="delete-hello-cluster"></a>Merhaba küme silme

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Merhaba adımlar bu belgedeki her ikisi de oluşturma beri kümelerde Merhaba aynı Azure kaynak grubu, hello Azure portal hello kaynak grubunu silebilirsiniz. Bu belge, hello Azure sanal ağ ve depolama hesabı hello kümeleri tarafından kullanılan uygulayarak oluşturduğunuz tüm kaynakları silme hello grubunu kaldırır.

## <a name="next-steps"></a>Sonraki adımlar

Bu örnekte, nasıl toouse tooread Spark ve tooKafka yazma öğrendiniz. Aşağıdaki bağlantılar toodiscover hello diğer yolları toowork Kafka ile kullanın:

* [Hdınsight üzerinde Apache Kafka kullanmaya başlama](hdinsight-apache-kafka-get-started.md)
* [Hdınsight üzerinde MirrorMaker toocreate Kafka bir kopyasını kullan](hdinsight-apache-kafka-mirroring.md)
* [Apache Storm’u HDInsight üzerinde Kafka ile kullanma](hdinsight-apache-storm-with-kafka.md)

