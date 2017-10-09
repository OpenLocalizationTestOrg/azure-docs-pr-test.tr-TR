---
title: "aaaApache Kafka artırmak ölçek - Azure Hdınsight | Microsoft Docs"
description: "Azure Hdınsight tooincrease ölçeklenebilirlik üzerinde Apache Kafka küme diskleri tooconfigure nasıl yönetileceğini öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/14/2017
ms.author: larryfr
ms.openlocfilehash: b51114b33359f2c385f057a7a7a5b134cad27e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-storage-and-scalability-for-apache-kafka-on-hdinsight"></a>HDInsight üzerinde Apache Kafka için depolamayı ve ölçeklenebilirliği yapılandırma

Hdınsight üzerinde Apache Kafka nasıl tooconfigure hello yönetilen disk sayısı kullandığı öğrenin.

Hdınsight üzerinde Kafka hello yerel disk hello sanal makinelerin hello Hdınsight kümesinde kullanır. Kafka çok g/ç yoğun olduğundan [Azure yönetilen diskleri](../virtual-machines/windows/managed-disks-overview.md) kullanılan tooprovide yüksek işleme ve düğüm başına daha fazla depolama alanı sağlar. Geleneksel sanal sabit diskleri (VHD) Kafka için kullanıldıysa, her düğüm sınırlı too1 TB'tır. Birden çok disk tooachieve kullanabileceğiniz yönetilen disklerle hello kümedeki her düğüm için 16 TB.

Merhaba Aşağıdaki diyagramda yönetilen diskleri önce hdınsight'ta Kafka ve Kafka arasında bir karşılaştırma Hdınsight'ta yönetilen disklerle sağlar:

![HDInsight üzerinde Kafka'da VM başına tek bir VHD kullanımı ile VM başına birden fazla yönetilen disk kullanımının karşılaştırmasını gösteren diyagram](./media/hdinsight-apache-kafka-scalability/kafka-with-managed-disks-architecture.png)

## <a name="configure-managed-disks-azure-portal"></a>Yönetilen diskleri yapılandırma: Azure portalı

1. Merhaba Hello adımları [Hdınsight kümesi oluşturma](hdinsight-hadoop-create-linux-clusters-portal.md) toounderstand hello ortak adımlar toocreate hello portal kullanarak bir küme. Merhaba portal oluşturma işlemi tamamlamayın.

2. Merhaba gelen __küme boyutu__ dikey penceresinde, kullanım hello __çalışan düğümü başına disk__ alan tooconfigure hello disk sayısı.

    > [!NOTE]
    > Merhaba türde yönetilen disk ya da olabilir __standart__ (HDD) veya __Premium__ (SSD). Premium diskler, DS ve GS serisi VM'lerle kullanılır. Diğer tüm VM türleri standart disk kullanır.

    ![Merhaba küme boyutu dikey vurgulanmış çalışan düğümü başına hello disklerle görüntüsü](./media/hdinsight-apache-kafka-scalability/set-managed-disks-portal.png)

## <a name="configure-managed-disks-resource-manager-template"></a>Yönetilen diskleri yapılandırma: Resource Manager şablonu

bir Kafka kümedeki hello şablon bölümünü aşağıdaki kullanım hello hello alt düğümler tarafından kullanılan disk toocontrol hello sayısı:

```json
"dataDisksGroups": [
    {
        "disksPerNode": "[variables('disksPerWorkerNode')]"
    }
    ],
```

Tooconfigure disklere nasıl yönetileceğini göstermektedir tam bir şablon bulabilirsiniz [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).

## <a name="next-steps"></a>Sonraki adımlar

Hdınsight'ta Kafka ile çalışma hakkında daha fazla bilgi için aşağıdaki belgeleri hello bakın:

* [Hdınsight üzerinde MirrorMaker toocreate Kafka bir kopyasını kullan](hdinsight-apache-kafka-mirroring.md)
* [Apache Storm’u HDInsight üzerinde Kafka ile kullanma](hdinsight-apache-storm-with-kafka.md)
* [Apache Spark’ı HDInsight üzerinde Kafka ile kullanma](hdinsight-apache-spark-with-kafka.md)
* [Bir Azure sanal ağı tooKafka Bağlan](hdinsight-apache-kafka-connect-vpn-gateway.md)

* [Kafka ile yönetilen disklerle ilgili HDInsight blogu](https://azure.microsoft.com/blog/announcing-public-preview-of-apache-kafka-on-hdinsight-with-azure-managed-disks/)