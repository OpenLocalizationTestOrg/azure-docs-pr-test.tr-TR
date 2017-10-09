---
title: "aaaAn giriş tooApache hdınsight'ta - Azure Kafka | Microsoft Docs"
description: "Hdınsight üzerinde Apache Kafka hakkında bilgi edinin: toofind örnekler ve alma bilgilerini başlatıldığı nedir ve ne yaptığını."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: f284b6e3-5f3b-4a50-b455-917e77588069
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: larryfr
ms.openlocfilehash: 1bc198d4cf93a4682030d4fa5f71030f49ad64be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-apache-kafka-on-hdinsight-preview"></a><span data-ttu-id="98587-103">HDInsight üzerinde Apache Kafka’ya giriş (önizleme)</span><span class="sxs-lookup"><span data-stu-id="98587-103">Introducing Apache Kafka on HDInsight (preview)</span></span>

<span data-ttu-id="98587-104">[Apache Kafka](https://kafka.apache.org) kullanılan toobuild gerçek zamanlı olabilir bir açık kaynak dağıtılmış akış platform veri ardışık düzen ve uygulamaları akış.</span><span class="sxs-lookup"><span data-stu-id="98587-104">[Apache Kafka](https://kafka.apache.org) is an open-source distributed streaming platform that can be used toobuild real-time streaming data pipelines and applications.</span></span> <span data-ttu-id="98587-105">Kafka, burada yayımlayın ve toonamed veri akışları abone işlevselliği benzer tooa ileti sırası, ileti Aracısı de sağlar.</span><span class="sxs-lookup"><span data-stu-id="98587-105">Kafka also provides message broker functionality similar tooa message queue, where you can publish and subscribe toonamed data streams.</span></span> <span data-ttu-id="98587-106">Hdınsight üzerinde Kafka hello Microsoft Azure bulutta yönetilen, ölçeklendirilebilir ve yüksek oranda kullanılabilir bir hizmet sağlar.</span><span class="sxs-lookup"><span data-stu-id="98587-106">Kafka on HDInsight provides you with a managed, highly scalable, and highly available service in hello Microsoft Azure cloud.</span></span>

## <a name="why-use-kafka-on-hdinsight"></a><span data-ttu-id="98587-107">HDInsight üzerinde Kafka neden kullanılmalıdır?</span><span class="sxs-lookup"><span data-stu-id="98587-107">Why use Kafka on HDInsight?</span></span>

<span data-ttu-id="98587-108">Kafka hello aşağıdaki özellikleri sağlar:</span><span class="sxs-lookup"><span data-stu-id="98587-108">Kafka provides hello following features:</span></span>

* <span data-ttu-id="98587-109">Mesajlaşma düzeni yayımlama-abonelik: Kafka kayıtları tooa Kafka konu yayımlamak için bir üretici API sağlar.</span><span class="sxs-lookup"><span data-stu-id="98587-109">Publish-subscribe messaging pattern: Kafka provides a Producer API for publishing records tooa Kafka topic.</span></span> <span data-ttu-id="98587-110">Merhaba tüketici API tooa konu abone olduğunda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="98587-110">hello Consumer API is used when subscribing tooa topic.</span></span>

* <span data-ttu-id="98587-111">Akış işleme: Kafka genellikle gerçek zamanlı akış işleme için Apache Storm veya Spark ile birlikte kullanılır.</span><span class="sxs-lookup"><span data-stu-id="98587-111">Stream processing: Kafka is often used with Apache Storm or Spark for real-time stream processing.</span></span> <span data-ttu-id="98587-112">Kafka 0.10.0.0 (Hdınsight sürüm 3.5) çözümleri gerektirmeden Storm veya Spark akış toobuild sağlayan bir akış API sunmuştur.</span><span class="sxs-lookup"><span data-stu-id="98587-112">Kafka 0.10.0.0 (HDInsight version 3.5) introduced a streaming API that allows you toobuild streaming solutions without requiring Storm or Spark.</span></span>

* <span data-ttu-id="98587-113">Yatay Ölçek: Kafka hello Hdınsight kümesinde hello düğümleri arasında akışları bölümler.</span><span class="sxs-lookup"><span data-stu-id="98587-113">Horizontal scale: Kafka partitions streams across hello nodes in hello HDInsight cluster.</span></span> <span data-ttu-id="98587-114">Tüketici işlemleri ayrı ayrı bölümleri tooprovide yük kayıtları kullanırken dengelemesi ile ilişkilendirilebilir.</span><span class="sxs-lookup"><span data-stu-id="98587-114">Consumer processes can be associated with individual partitions tooprovide load balancing when consuming records.</span></span>

* <span data-ttu-id="98587-115">Sıralı teslim: her bölüm içinde kayıtları hello akış bunlar alınan hello sırayla depolanır.</span><span class="sxs-lookup"><span data-stu-id="98587-115">In-order delivery: Within each partition, records are stored in hello stream in hello order that they were received.</span></span> <span data-ttu-id="98587-116">Bölüm başına bir tüketici işlemi ile ilişkilendirerek, kayıtların sırayla işlenmesini garanti edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98587-116">By associating one consumer process per partition, you can guarantee that records are processed in-order.</span></span>

* <span data-ttu-id="98587-117">Hataya dayanıklı: Bölümleri arasında düğümleri tooprovide hata toleransı çoğaltılabilir.</span><span class="sxs-lookup"><span data-stu-id="98587-117">Fault-tolerant: Partitions can be replicated between nodes tooprovide fault tolerance.</span></span>

* <span data-ttu-id="98587-118">Azure yönetilen diskler ile tümleştirme: yönetilen diskleri sağlayan daha yüksek ölçek ve verimlilik hello Hdınsight kümesi hello sanal makineler tarafından kullanılan hello diskler.</span><span class="sxs-lookup"><span data-stu-id="98587-118">Integration with Azure Managed Disks: Managed disks provides higher scale and throughput for hello disks used by hello virtual machines in hello HDInsight cluster.</span></span>

    <span data-ttu-id="98587-119">Yönetilen diskleri hdınsight'ta Kafka için varsayılan olarak etkindir ve düğüm başına kullanılan diskler hello sayısı Hdınsight oluşturma sırasında yapılandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="98587-119">Managed disks are enabled by default for Kafka on HDInsight, and hello number of disks used per node can be configured during HDInsight creation.</span></span> <span data-ttu-id="98587-120">Yönetilen diskler hakkında daha fazla bilgi için bkz. [Azure Yönetilen Diskler](../virtual-machines/windows/managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="98587-120">For more information on managed disks, see [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md).</span></span>

    <span data-ttu-id="98587-121">Yönetilen disklerin HDInsight üzerinde Kafka ile yapılandırılması hakkında bilgi edinmek için bkz. [HDInsight üzerinde Kafka'nın ölçeklenebilirliğini artırma](hdinsight-apache-kafka-scalability.md).</span><span class="sxs-lookup"><span data-stu-id="98587-121">For information on configuring managed disks with Kafka on HDInsight, see [Increase scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span></span>

## <a name="use-cases"></a><span data-ttu-id="98587-122">Uygulama alanları</span><span class="sxs-lookup"><span data-stu-id="98587-122">Use cases</span></span>

* <span data-ttu-id="98587-123">**İleti**: hello desteklediğinden yayımlama-abone ileti deseni, Kafka genellikle bir ileti aracı olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="98587-123">**Messaging**: Since it supports hello publish-subscribe message pattern, Kafka is often used as a message broker.</span></span>

* <span data-ttu-id="98587-124">**İzleme etkinliği**: bu yana Kafka kayıtları sıralı günlüğe kaydedilmesini sağlar, kullanılan tootrack olması ve etkinlikleri yeniden oluşturun.</span><span class="sxs-lookup"><span data-stu-id="98587-124">**Activity tracking**: Since Kafka provides in-order logging of records, it can be used tootrack and re-create activities.</span></span> <span data-ttu-id="98587-125">Örneğin, bir web sitesindeki veya uygulamadaki kullanıcı işlemleri.</span><span class="sxs-lookup"><span data-stu-id="98587-125">For example, user actions on a web site or within an application.</span></span>

* <span data-ttu-id="98587-126">**Toplama**: akış işleme kullanan, farklı akışları toocombine bilgileri toplamak ve işletimsel veri hello bilgileri merkezileştirme.</span><span class="sxs-lookup"><span data-stu-id="98587-126">**Aggregation**: Using stream processing, you can aggregate information from different streams toocombine and centralize hello information into operational data.</span></span>

* <span data-ttu-id="98587-127">**Dönüştürme**: Akış işlemeyi kullanarak, birden fazla girdi konu başlığındaki verileri bir veya daha fazla çıktı konu başlığında birleştirerek verileri zenginleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="98587-127">**Transformation**: Using stream processing, you can combine and enrich data from multiple input topics into one or more output topics.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98587-128">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="98587-128">Next steps</span></span>

<span data-ttu-id="98587-129">Kullanım hello aşağıdaki bağlantılar toolearn nasıl toouse Hdınsight üzerinde Apache Kafka:</span><span class="sxs-lookup"><span data-stu-id="98587-129">Use hello following links toolearn how toouse Apache Kafka on HDInsight:</span></span>

* [<span data-ttu-id="98587-130">HDInsight'ta Kafka kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="98587-130">Get started with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)

* [<span data-ttu-id="98587-131">Hdınsight üzerinde MirrorMaker toocreate Kafka bir kopyasını kullan</span><span class="sxs-lookup"><span data-stu-id="98587-131">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)

* [<span data-ttu-id="98587-132">Apache Storm’u HDInsight üzerinde Kafka ile kullanma</span><span class="sxs-lookup"><span data-stu-id="98587-132">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)

* [<span data-ttu-id="98587-133">Apache Spark’ı HDInsight üzerinde Kafka ile kullanma</span><span class="sxs-lookup"><span data-stu-id="98587-133">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)

* [<span data-ttu-id="98587-134">Bir Azure sanal ağı tooKafka Bağlan</span><span class="sxs-lookup"><span data-stu-id="98587-134">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
