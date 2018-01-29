---
title: "Günlük analizi Apache Kafka - Azure Hdınsight | Microsoft Docs"
description: "Azure hdınsight'ta Apache Kafka kümeden günlüklerini çözümlemek için Operations Management Suite kullanmayı öğrenin."
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
ms.date: 11/07/2017
ms.author: larryfr
ms.openlocfilehash: 440133da32f4565aa247b273984b3affe18379ec
ms.sourcegitcommit: 9a61faf3463003375a53279e3adce241b5700879
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/15/2017
---
# <a name="analyze-logs-for-apache-kafka-on-hdinsight"></a>Hdınsight üzerinde Apache Kafka günlüklerini analiz edin

Microsoft Operations Management Suite günlüklerini hdınsight'ta Apache Kafka tarafından oluşturulan çözümlemek için nasıl kullanılacağını öğrenin.

## <a name="enable-oms-for-kafka"></a>OMS Kafka için etkinleştirme

Hdınsight için günlük analizi etkinleştirme adımları tüm Hdınsight kümeleri için aynıdır. Oluşturma ve gerekli hizmetleri yapılandırma anlamak için aşağıdaki bağlantıları kullanın:

1. Günlük analizi çalışma alanı oluşturun. Daha fazla bilgi için bkz: [günlük analizi çalışma alanı ile çalışmaya başlama](https://docs.microsoft.com/azure/log-analytics) belge.

2. Hdınsight kümesinde bir Kafka oluşturun. Daha fazla bilgi için bkz: [Hdınsight üzerinde Apache Kafka başlayarak](apache-kafka-get-started.md) belge.

3. Günlük analizi kullanmak için Kafka küme yapılandırın. Daha fazla bilgi için bkz: [Hdınsight izlemek için kullanım günlük analizi](../hdinsight-hadoop-oms-log-analytics-tutorial.md) belge.

    > [!NOTE]
    > Günlük analizi kullanarak kümeye de yapılandırabilirsiniz `Enable-AzureRmHDInsightOperationsManagementSuite` cmdlet'i. Bu cmdlet, aşağıdaki bilgileri gerektirir:
    >
    > * Hdınsight küme adı.
    > * Günlük analizi çalışma alanı kimliği. Çalışma alanı kimliği için günlük analizi çalışma alanınızda OMS çalışma alanında bulabilirsiniz.
    > * OMS bağlantısı için birincil anahtar. Birincil anahtarı bulmak için günlük analizi örneği seçin ve ardından __OMS portalı__. OMS Portalı'ndan seçin __ayarları__, __bağlı kaynakları__ve ardından __Linux sunucuları__.


> [!IMPORTANT]
> veri günlük analizi için kullanılabilir olmadan önce yaklaşık 20 dakika sürebilir.

## <a name="query-logs"></a>Sorgu günlükleri

1. Gelen [Azure portal](https://portal.azure.com), günlük analizi çalışma alanınızı seçin.

2. Seçin __oturum arama__. Buradan, Kafka toplanan verileri arayabilirsiniz. Bazı örnek aramalar şunlardır:

    * Disk kullanımı:`Type=Perf ObjectName="Logical Disk" (CounterName="Free Megabytes")  InstanceName="_Total" Computer='hn*-*' or Computer='wn*-*' | measure avg(CounterValue) by   Computer interval 1HOUR`
    * CPU kullanımı:`Type:Perf CounterName="% Processor Time" InstanceName="_Total" Computer='hn*-*' or Computer='wn*-*' | measure avg(CounterValue) by Computer interval 1HOUR`
    * Saniye başına gelen iletileri:`Type=metrics_kafka_CL ClusterName_s="your_kafka_cluster_name" InstanceName_s="kafka-BrokerTopicMetrics-MessagesInPerSec-Count" | measure avg(kafka_BrokerTopicMetrics_MessagesInPerSec_Count_value_d) by HostName_s interval 1HOUR`
    * Saniye başına gelen bayt sayısı:`Type=metrics_kafka_CL HostName_s="wn0-kafka" InstanceName_s="kafka-BrokerTopicMetrics-BytesInPerSec-Count" | measure avg(kafka_BrokerTopicMetrics_BytesInPerSec_Count_value_d) interval 1HOUR`
    * Saniye başına Giden bayt sayısı:`Type=metrics_kafka_CL ClusterName_s="your_kafka_cluster_name" InstanceName_s="kafka-BrokerTopicMetrics-BytesOutPerSec-Count" |  measure avg(kafka_BrokerTopicMetrics_BytesOutPerSec_Count_value_d) interval 1HOUR`

    > [!IMPORTANT]
    > Sorgu değerleri kümeye özel bilgileri ile değiştirin. Örneğin, `ClusterName_s` kümenizin adını ayarlamanız gerekir. `HostName_s`Kümedeki çalışan düğümü etki alanı adını ayarlamanız gerekir.

    Ayrıca girebilirsiniz `*` kaydedilen tüm türleri aramak için. Şu anda günlükleri sorgularında kullanılabilir:

    | Günlük türü | Açıklama |
    | ---- | ---- |
    | Günlük\_kafkaserver\_Temizle | Kafka Aracısı server.log |
    | Günlük\_kafkacontroller\_Temizle | Kafka Aracısı controller.log |
    | Ölçümleri\_kafka\_Temizle | Kafka JMX ölçümleri |

    ![CPU kullanımı arama görüntüsü](./media/apache-kafka-log-analytics-operations-management/kafka-cpu-usage.png)
 
 ## <a name="next-steps"></a>Sonraki adımlar

Günlük analizi hakkında daha fazla bilgi için bkz: [günlük analizi çalışma alanı ile çalışmaya başlama](../../log-analytics/log-analytics-get-started.md) belge.

Kafka ile çalışma hakkında daha fazla bilgi için aşağıdaki belgelere bakın:

 * [Hdınsight kümeleri arasında yansıtma Kafka](apache-kafka-mirroring.md)
 * [Hdınsight üzerinde Kafka ölçeklenebilirliği artırmak](apache-kafka-scalability.md)
 * [(DStreams) ile Kafka Spark akış kullanın](../hdinsight-apache-spark-with-kafka.md)
 * [Kafka ile akış yapılandırılmış Spark kullanma](../hdinsight-apache-kafka-spark-structured-streaming.md)