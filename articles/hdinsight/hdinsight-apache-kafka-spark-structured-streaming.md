---
title: "Apache Spark yapılandırılmış Kafka - Azure Hdınsight akış | Microsoft Docs"
description: "Apache Spark (DStream) akış içine veya dışına Apache Kafka veri almak için nasıl kullanılacağını öğrenin. Bu örnekte, Hdınsight'ta Spark gelen Jupyter Not Defteri kullanarak veri akışı."
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
ms.openlocfilehash: 02b49e13e8f54c3d55310f4d2b21c7e09c91fe81
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-spark-structured-streaming-with-kafka-preview-on-hdinsight"></a>Hdınsight'ta Spark yapılandırılmış akış Kafka (Önizleme) ile kullanma

Spark yapılandırılmış akış verilerini Azure hdınsight'ta Apache Kafka okumak için nasıl kullanılacağını öğrenin.

Yapılandırılmış Spark akış Spark SQL yerleşik bir akış işleme altyapısıdır. Akış hesaplamalar express için toplu hesaplama aynı statik verileri sağlar. Yapılandırılmış akışı hakkında daha fazla bilgi için bkz: [yapılandırılmış akış Programlama Kılavuzu [alfa]](http://spark.apache.org/docs/2.1.0/structured-streaming-programming-guide.html) Apache.org.

> [!IMPORTANT]
> Bu örnek, Hdınsight 3.6 üzerinde Spark 2.1 kullanılır. Yapılandırılmış akış olarak kabul __alfa__ Spark 2.1 üzerinde.
>
> Bu belgede yer alan adımlar, hem hdınsight'ta Spark ve Hdınsight kümesinde bir Kafka içeren bir Azure kaynak grubu oluşturun. Bu kümeleri, hem bir Azure sanal Kafka ile doğrudan iletişim kurmak Spark kümesi sağlayan ağ içinde bulunan küme ' dir.
>
> Bu belgedeki adımları tamamladığınızda, aşırı ücretlerden kaçınmak için kümelerini Sil unutmayın.

## <a name="create-the-clusters"></a>Kümeleri oluşturma

Hdınsight üzerinde Apache Kafka erişim genel internet üzerinden Kafka aracıların sağlamaz. İçin Kafka ettiği herhangi bir şey Kafka kümedeki düğümlerin aynı Azure sanal ağ içinde olmalıdır. Bu örnekte, bir Azure sanal ağında Kafka ve Spark kümeleri bulunur. Aşağıdaki diyagramda, iletişim kümeleri arasında nasıl aktığını gösterir:

![Bir Azure sanal ağı Spark ve Kafka kümelerde diyagramı](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> Sanal ağ içinde iletişimi Kafka hizmet sınırlıdır. Kümedeki SSH ve Ambari, gibi diğer hizmetlerin internet üzerinden erişilebilir. Hdınsight ile kullanılabilen ortak bağlantı noktaları hakkında daha fazla bilgi için bkz: [bağlantı noktaları ve Hdınsight tarafından kullanılan URI](hdinsight-hadoop-port-settings-for-services.md).

Azure sanal ağı, Kafka, oluşturabilir ve el ile Spark kümeleri olsa da, bir Azure Resource Manager şablonunu kullanmak daha kolaydır. Azure sanal ağı, Kafka, dağıtmak ve Spark kümeleri Azure aboneliğiniz için aşağıdaki adımları kullanın.

1. Azure'da oturum açın ve Azure portalında şablon açmak için aşağıdaki düğmesini kullanın.
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v4.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy to Azure"></a>
    
    Azure Resource Manager şablonu bulunur **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v4.1.json**.

    Bu şablon, aşağıdaki kaynaklara oluşturur:

    * Hdınsight 3.5 kümede Kafka.
    * Bir Spark Hdınsight 3.6 kümede.
    * Bir Azure sanal Hdınsight kümeleri içeren ağ.

    > [!IMPORTANT]
    > Bu örnekte kullanılan yapılandırılmış akış dizüstü Spark Hdınsight 3.6 gerektirir. Hdınsight'ta Spark önceki bir sürümünü kullanıyorsanız, dizüstü bilgisayar kullanırken hataları alırsınız.

2. Üzerinde girişleri doldurmak için aşağıdaki bilgileri kullanın **özel dağıtım** dikey penceresinde:
   
    ![Hdınsight özel dağıtım](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * **Kaynak grubu**: bir grup oluşturun veya varolan bir tanesini seçin. Bu grup, Hdınsight kümesi içerir.

    * **Konum**: coğrafi olarak yakın bir konum seçin.

    * **Temel küme adı**: Bu değer Spark temel adı olarak kullanılır ve Kafka kümeleri. Örneğin, **hdı** bir Spark spark hdi__ adlı Küme ve adlı bir Kafka kümesi oluşturur **kafka hdı**.

    * **Oturum açma kullanıcı adı küme**: Spark ve Kafka kümeleri için yönetici kullanıcı adı.

    * **Oturum açma parolası küme**: Spark ve Kafka kümeleri için yönetici kullanıcı parolası.

    * **SSH kullanıcı adı**: için Spark ve Kafka kümeleri oluşturmak için SSH kullanıcı.

    * **SSH parolası**: Spark ve Kafka kümelerinin SSH kullanıcısının parolası.

3. Okuma **hüküm ve koşullar**ve ardından **hüküm ve koşulları yukarıda belirtildiği ediyorum**.

4. Son olarak, denetleme **panoya Sabitle** ve ardından **satın alma**. Kümeleri oluşturmak için yaklaşık 20 dakika sürer.

Kaynakları oluşturduktan sonra kaynak grubu dikey penceresine yönlendirilirsiniz.

![Kaynak grubu dikey vnet ve kümeler için](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> Hdınsight kümeleri adlarının bildirimi **spark BASENAME** ve **kafka BASENAME**, BASENAME şablona verdiğiniz adı olduğu. Kümeye bağlanırken bu adları daha sonraki adımlarda kullanın.

## <a name="get-the-kafka-brokers"></a>Aracıların Kafka Al

Bu örnekteki kod Kafka kümedeki Kafka Aracısı ana bağlanır. Kafka Aracısı ana bilgisayarları bulmak için aşağıdaki PowerShell veya Bash örneği kullanın:

```powershell
$creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
$clusterName = Read-Host -Prompt "Enter the Kafka cluster name"
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
> Bu örnek bekliyor `$PASSWORD` küme oturum açma için parola içerecek şekilde ve `$CLUSTERNAME` Kafka küme adı içeriyor.
>
> Bu örnekte [jq](https://stedolan.github.io/jq/) JSON belgesini dışında verileri ayrıştırmak için yardımcı programı.

Çıktı aşağıdaki metne benzer:

`wn0-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn1-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn2-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092,wn3-kafka.0owcbllr5hze3hxdja3mqlrhhe.ex.internal.cloudapp.net:9092`

Bu belge aşağıdaki bölümlerde kullanılmak üzere bu bilgileri kaydedin.

## <a name="get-the-notebooks"></a>Not defterlerini Al

Bu belgede açıklanan örnek kodunu şu adresten edinilebilir [https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming](https://github.com/Azure-Samples/hdinsight-spark-kafka-structured-streaming).

## <a name="upload-the-notebooks"></a>Not defterlerini karşıya yükle

Proje defterlerinden, Spark Hdınsight kümesinde için karşıya yüklemek için aşağıdaki adımları kullanın:

1. Web tarayıcınız, Spark kümesinde Jupyter not defteri bağlayın. Aşağıdaki URL ile değiştirin `CLUSTERNAME` Kafka kümenizin adıyla:

        https://CLUSTERNAME.azurehdinsight.net/jupyter

    İstendiğinde, küme oturum açma (Yönetici) ve küme oluştururken kullanılan parolayı girin.

2. Sayfanın üst sağ taraftan kullanmak __karşıya__ karşıya yüklemek için düğmeyi __akış Tweet'leri To_Kafka.ipynb__ kümeye dosya. Seçin __açık__ başlatmak için.

    ![Karşıya yükleme düğmesini seçin ve bir dizüstü bilgisayara yüklemek için kullanın](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-button.png)

    ![KafkaStreaming.ipynb dosyasını seçin](./media/hdinsight-apache-kafka-spark-structured-streaming/select-notebook.png)

3. Bul __akış Tweet'leri To_Kafka.ipynb__ not defterlerini ve select listesi girişi __karşıya__ yanında düğmesi.

    ![Not Defteri sunucuya yüklemek için KafkaStreaming.ipynb girişi yanındaki karşıya yükleme düğmesini kullanın](./media/hdinsight-apache-kafka-spark-structured-streaming/upload-notebook.png)

4. Yüklemek için 1-3 arasındaki adımları yineleyin __Spark-yapılandırılmış-akış-gelen-Kafka.ipynb__ dizüstü bilgisayar.

## <a name="load-tweets-into-kafka"></a>Yük tweet'leri Kafka içine

Karşıya yüklenen dosyaların sonra seçeneğini __akış Tweet'leri To_Kafka.ipynb__ girişi not defterini açın. Tweet'leri Kafka yüklemek için Not Defteri'ndaki adımları izleyin.

## <a name="process-tweets-using-spark-structured-streaming"></a>İşlem tweet'leri Spark yapılandırılmış akış kullanma

Jupyter not defteri giriş sayfadan seçin __Spark-yapılandırılmış-akış-gelen-Kafka.ipynb__ girişi. Tweet'leri Kafka Spark yapılandırılmış akış kullanarak yüklemek için not defterindeki adımları izleyin.

## <a name="next-steps"></a>Sonraki adımlar

Spark yapılandırılmış akış kullanmayı öğrendiniz, Spark ve Kafka ile çalışma hakkında daha fazla bilgi için aşağıdaki belgelere bakın:

* [(DStream) ile Kafka Spark akış kullanmayı](hdinsight-apache-spark-with-kafka.md).
* [Jupyter not defteri ve hdınsight'ta Spark ile Başlat](hdinsight-apache-spark-jupyter-spark-sql.md)