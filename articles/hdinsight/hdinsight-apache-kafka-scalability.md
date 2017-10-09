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
# <a name="configure-storage-and-scalability-for-apache-kafka-on-hdinsight"></a><span data-ttu-id="42d08-103">HDInsight üzerinde Apache Kafka için depolamayı ve ölçeklenebilirliği yapılandırma</span><span class="sxs-lookup"><span data-stu-id="42d08-103">Configure storage and scalability for Apache Kafka on HDInsight</span></span>

<span data-ttu-id="42d08-104">Hdınsight üzerinde Apache Kafka nasıl tooconfigure hello yönetilen disk sayısı kullandığı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="42d08-104">Learn how tooconfigure hello number of managed disks used by Apache Kafka on HDInsight.</span></span>

<span data-ttu-id="42d08-105">Hdınsight üzerinde Kafka hello yerel disk hello sanal makinelerin hello Hdınsight kümesinde kullanır.</span><span class="sxs-lookup"><span data-stu-id="42d08-105">Kafka on HDInsight uses hello local disk of hello virtual machines in hello HDInsight cluster.</span></span> <span data-ttu-id="42d08-106">Kafka çok g/ç yoğun olduğundan [Azure yönetilen diskleri](../virtual-machines/windows/managed-disks-overview.md) kullanılan tooprovide yüksek işleme ve düğüm başına daha fazla depolama alanı sağlar.</span><span class="sxs-lookup"><span data-stu-id="42d08-106">Since Kafka is very I/O heavy, [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md) is used tooprovide high throughput and provide more storage per node.</span></span> <span data-ttu-id="42d08-107">Geleneksel sanal sabit diskleri (VHD) Kafka için kullanıldıysa, her düğüm sınırlı too1 TB'tır.</span><span class="sxs-lookup"><span data-stu-id="42d08-107">If traditional virtual hard drives (VHD) were used for Kafka, each node is limited too1 TB.</span></span> <span data-ttu-id="42d08-108">Birden çok disk tooachieve kullanabileceğiniz yönetilen disklerle hello kümedeki her düğüm için 16 TB.</span><span class="sxs-lookup"><span data-stu-id="42d08-108">With managed disks, you can use multiple disks tooachieve 16 TB for each node in hello cluster.</span></span>

<span data-ttu-id="42d08-109">Merhaba Aşağıdaki diyagramda yönetilen diskleri önce hdınsight'ta Kafka ve Kafka arasında bir karşılaştırma Hdınsight'ta yönetilen disklerle sağlar:</span><span class="sxs-lookup"><span data-stu-id="42d08-109">hello following diagram provides a comparison between Kafka on HDInsight before managed disks, and Kafka on HDInsight with managed disks:</span></span>

![HDInsight üzerinde Kafka'da VM başına tek bir VHD kullanımı ile VM başına birden fazla yönetilen disk kullanımının karşılaştırmasını gösteren diyagram](./media/hdinsight-apache-kafka-scalability/kafka-with-managed-disks-architecture.png)

## <a name="configure-managed-disks-azure-portal"></a><span data-ttu-id="42d08-111">Yönetilen diskleri yapılandırma: Azure portalı</span><span class="sxs-lookup"><span data-stu-id="42d08-111">Configure managed disks: Azure portal</span></span>

1. <span data-ttu-id="42d08-112">Merhaba Hello adımları [Hdınsight kümesi oluşturma](hdinsight-hadoop-create-linux-clusters-portal.md) toounderstand hello ortak adımlar toocreate hello portal kullanarak bir küme.</span><span class="sxs-lookup"><span data-stu-id="42d08-112">Follow hello steps in hello [Create an HDInsight cluster](hdinsight-hadoop-create-linux-clusters-portal.md) toounderstand hello common steps toocreate a cluster using hello portal.</span></span> <span data-ttu-id="42d08-113">Merhaba portal oluşturma işlemi tamamlamayın.</span><span class="sxs-lookup"><span data-stu-id="42d08-113">Do not complete hello portal creation process.</span></span>

2. <span data-ttu-id="42d08-114">Merhaba gelen __küme boyutu__ dikey penceresinde, kullanım hello __çalışan düğümü başına disk__ alan tooconfigure hello disk sayısı.</span><span class="sxs-lookup"><span data-stu-id="42d08-114">From hello __Cluster size__ blade, use hello __Disks per worker node__ field tooconfigure hello number of disks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="42d08-115">Merhaba türde yönetilen disk ya da olabilir __standart__ (HDD) veya __Premium__ (SSD).</span><span class="sxs-lookup"><span data-stu-id="42d08-115">hello type of managed disk can be either __Standard__ (HDD) or __Premium__ (SSD).</span></span> <span data-ttu-id="42d08-116">Premium diskler, DS ve GS serisi VM'lerle kullanılır.</span><span class="sxs-lookup"><span data-stu-id="42d08-116">Premium disks are used with DS and GS series VMs.</span></span> <span data-ttu-id="42d08-117">Diğer tüm VM türleri standart disk kullanır.</span><span class="sxs-lookup"><span data-stu-id="42d08-117">All other VM types use standard.</span></span>

    ![Merhaba küme boyutu dikey vurgulanmış çalışan düğümü başına hello disklerle görüntüsü](./media/hdinsight-apache-kafka-scalability/set-managed-disks-portal.png)

## <a name="configure-managed-disks-resource-manager-template"></a><span data-ttu-id="42d08-119">Yönetilen diskleri yapılandırma: Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="42d08-119">Configure managed disks: Resource Manager template</span></span>

<span data-ttu-id="42d08-120">bir Kafka kümedeki hello şablon bölümünü aşağıdaki kullanım hello hello alt düğümler tarafından kullanılan disk toocontrol hello sayısı:</span><span class="sxs-lookup"><span data-stu-id="42d08-120">toocontrol hello number of disks used by hello worker nodes in a Kafka cluster, use hello following section of hello template:</span></span>

```json
"dataDisksGroups": [
    {
        "disksPerNode": "[variables('disksPerWorkerNode')]"
    }
    ],
```

<span data-ttu-id="42d08-121">Tooconfigure disklere nasıl yönetileceğini göstermektedir tam bir şablon bulabilirsiniz [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).</span><span class="sxs-lookup"><span data-stu-id="42d08-121">You can find a complete template that demonstrates how tooconfigure managed disks at [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="42d08-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="42d08-122">Next steps</span></span>

<span data-ttu-id="42d08-123">Hdınsight'ta Kafka ile çalışma hakkında daha fazla bilgi için aşağıdaki belgeleri hello bakın:</span><span class="sxs-lookup"><span data-stu-id="42d08-123">For more information on working with Kafka on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="42d08-124">Hdınsight üzerinde MirrorMaker toocreate Kafka bir kopyasını kullan</span><span class="sxs-lookup"><span data-stu-id="42d08-124">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="42d08-125">Apache Storm’u HDInsight üzerinde Kafka ile kullanma</span><span class="sxs-lookup"><span data-stu-id="42d08-125">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="42d08-126">Apache Spark’ı HDInsight üzerinde Kafka ile kullanma</span><span class="sxs-lookup"><span data-stu-id="42d08-126">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="42d08-127">Bir Azure sanal ağı tooKafka Bağlan</span><span class="sxs-lookup"><span data-stu-id="42d08-127">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)

* [<span data-ttu-id="42d08-128">Kafka ile yönetilen disklerle ilgili HDInsight blogu</span><span class="sxs-lookup"><span data-stu-id="42d08-128">HDInsight blog on managed disks with Kafka</span></span>](https://azure.microsoft.com/blog/announcing-public-preview-of-apache-kafka-on-hdinsight-with-azure-managed-disks/)