---
title: "Apache Kafka ölçek artırma - Azure HDInsight | Microsoft Docs"
description: "Ölçeklenebilirliği artırmak için Azure HDInsight üzerinde Apache Kafka kümesi için yönetilen diskleri yapılandırmayı öğrenin."
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
ms.openlocfilehash: 880a186a3d9a23b013294b0121e8265270d160cc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="configure-storage-and-scalability-for-apache-kafka-on-hdinsight"></a><span data-ttu-id="ed428-103">HDInsight üzerinde Apache Kafka için depolamayı ve ölçeklenebilirliği yapılandırma</span><span class="sxs-lookup"><span data-stu-id="ed428-103">Configure storage and scalability for Apache Kafka on HDInsight</span></span>

<span data-ttu-id="ed428-104">HDInsight üzerinde Apache Kafka tarafından kullanılan yönetilen disk sayısını yapılandırmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="ed428-104">Learn how to configure the number of managed disks used by Apache Kafka on HDInsight.</span></span>

<span data-ttu-id="ed428-105">HDInsight üzerinde Kafka, HDInsight kümesindeki sanal makinelerin yerel diskini kullanır.</span><span class="sxs-lookup"><span data-stu-id="ed428-105">Kafka on HDInsight uses the local disk of the virtual machines in the HDInsight cluster.</span></span> <span data-ttu-id="ed428-106">Kafka G/Ç açısından oldukça yoğun olduğundan yüksek aktarım hızı ve düğüm başına daha fazla depolama alanı sağlamak için [Azure Yönetilen Diskler](../virtual-machines/windows/managed-disks-overview.md) kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ed428-106">Since Kafka is very I/O heavy, [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md) is used to provide high throughput and provide more storage per node.</span></span> <span data-ttu-id="ed428-107">Kafka için geleneksel sanal sabit diskler (VHD) kullanıldıysa her düğüm 1 TB ile sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="ed428-107">If traditional virtual hard drives (VHD) were used for Kafka, each node is limited to 1 TB.</span></span> <span data-ttu-id="ed428-108">Yönetilen disklerle kümedeki her düğüm için 16 TB elde etmek üzere birden çok disk kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ed428-108">With managed disks, you can use multiple disks to achieve 16 TB for each node in the cluster.</span></span>

<span data-ttu-id="ed428-109">Aşağıdaki diyagramda, yönetilen diskli HDInsight üzerinde Kafka ile yönetilen disksiz HDInsight üzerinde Kafka karşılaştırılmaktadır:</span><span class="sxs-lookup"><span data-stu-id="ed428-109">The following diagram provides a comparison between Kafka on HDInsight before managed disks, and Kafka on HDInsight with managed disks:</span></span>

![HDInsight üzerinde Kafka'da VM başına tek bir VHD kullanımı ile VM başına birden fazla yönetilen disk kullanımının karşılaştırmasını gösteren diyagram](./media/hdinsight-apache-kafka-scalability/kafka-with-managed-disks-architecture.png)

## <a name="configure-managed-disks-azure-portal"></a><span data-ttu-id="ed428-111">Yönetilen diskleri yapılandırma: Azure portalı</span><span class="sxs-lookup"><span data-stu-id="ed428-111">Configure managed disks: Azure portal</span></span>

1. <span data-ttu-id="ed428-112">Portalı kullanarak küme oluşturmaya yönelik genel adımları öğrenmek için [HDInsight kümesi oluşturma](hdinsight-hadoop-create-linux-clusters-portal.md) bölümündeki adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="ed428-112">Follow the steps in the [Create an HDInsight cluster](hdinsight-hadoop-create-linux-clusters-portal.md) to understand the common steps to create a cluster using the portal.</span></span> <span data-ttu-id="ed428-113">Portal oluşturma işlemini tamamlamayın.</span><span class="sxs-lookup"><span data-stu-id="ed428-113">Do not complete the portal creation process.</span></span>

2. <span data-ttu-id="ed428-114">__Küme boyutu__ dikey penceresinde, disk sayısını yapılandırmak için __çalışan düğümü başına disk sayısı__ alanını kullanın.</span><span class="sxs-lookup"><span data-stu-id="ed428-114">From the __Cluster size__ blade, use the __Disks per worker node__ field to configure the number of disks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ed428-115">Yönetilen diskin türü __Standart__ (HDD) veya __Premium__ (SSD) olabilir.</span><span class="sxs-lookup"><span data-stu-id="ed428-115">The type of managed disk can be either __Standard__ (HDD) or __Premium__ (SSD).</span></span> <span data-ttu-id="ed428-116">Premium diskler, DS ve GS serisi VM'lerle kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ed428-116">Premium disks are used with DS and GS series VMs.</span></span> <span data-ttu-id="ed428-117">Diğer tüm VM türleri standart disk kullanır.</span><span class="sxs-lookup"><span data-stu-id="ed428-117">All other VM types use standard.</span></span>

    ![Çalışan düğümü başına disk sayısı vurgulanmış şekilde küme boyutu dikey penceresinin görüntüsü](./media/hdinsight-apache-kafka-scalability/set-managed-disks-portal.png)

## <a name="configure-managed-disks-resource-manager-template"></a><span data-ttu-id="ed428-119">Yönetilen diskleri yapılandırma: Resource Manager şablonu</span><span class="sxs-lookup"><span data-stu-id="ed428-119">Configure managed disks: Resource Manager template</span></span>

<span data-ttu-id="ed428-120">Kafka kümesindeki çalışan düğümleri tarafından kullanılan disk sayısını denetlemek için şablonun şu bölümünü kullanın:</span><span class="sxs-lookup"><span data-stu-id="ed428-120">To control the number of disks used by the worker nodes in a Kafka cluster, use the following section of the template:</span></span>

```json
"dataDisksGroups": [
    {
        "disksPerNode": "[variables('disksPerWorkerNode')]"
    }
    ],
```

<span data-ttu-id="ed428-121">Yönetilen disklerin nasıl yapılandırıldığını gösteren eksiksiz bir şablon için [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json) adresine gidin.</span><span class="sxs-lookup"><span data-stu-id="ed428-121">You can find a complete template that demonstrates how to configure managed disks at [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed428-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ed428-122">Next steps</span></span>

<span data-ttu-id="ed428-123">HDInsight üzerinde Kafka ile çalışma hakkında daha fazla bilgi için şu belgelere göz atın:</span><span class="sxs-lookup"><span data-stu-id="ed428-123">For more information on working with Kafka on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="ed428-124">MirrorMaker kullanarak HDInsight üzerinde Kafka kopyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="ed428-124">Use MirrorMaker to create a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="ed428-125">Apache Storm’u HDInsight üzerinde Kafka ile kullanma</span><span class="sxs-lookup"><span data-stu-id="ed428-125">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="ed428-126">Apache Spark’ı HDInsight üzerinde Kafka ile kullanma</span><span class="sxs-lookup"><span data-stu-id="ed428-126">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="ed428-127">Azure Sanal Ağ üzerinden Kafka’ya bağlanma</span><span class="sxs-lookup"><span data-stu-id="ed428-127">Connect to Kafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)

* [<span data-ttu-id="ed428-128">Kafka ile yönetilen disklerle ilgili HDInsight blogu</span><span class="sxs-lookup"><span data-stu-id="ed428-128">HDInsight blog on managed disks with Kafka</span></span>](https://azure.microsoft.com/blog/announcing-public-preview-of-apache-kafka-on-hdinsight-with-azure-managed-disks/)