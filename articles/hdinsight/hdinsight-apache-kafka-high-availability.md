---
title: "Apache Kafka - Azure Hdınsight ile aaaHigh kullanılabilirliğini | Microsoft Docs"
description: "Bilgi nasıl tooensure yüksek kullanılabilirlik ile Azure hdınsight'ta Apache Kafka. Nasıl toorebalance bölüm kopyalarını Kafka böylece Hdınsight içeren Azure bölgesi hello farklı hata etki alanlarını üzerinde olduğu hakkında bilgi edinin."
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
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 337468f36b531f83c2999e87907de89cf3d19dd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-of-your-data-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="f2f41-104">HDInsight’ta Apache Kafka (önizleme) ile verilerinizin yüksek kullanılabilirliği</span><span class="sxs-lookup"><span data-stu-id="f2f41-104">High availability of your data with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="f2f41-105">Temel alınan donanım Kafka konuları tootake avantajlarından tooconfigure çoğaltmalarını yapılandırma nasıl raf öğrenin.</span><span class="sxs-lookup"><span data-stu-id="f2f41-105">Learn how tooconfigure partition replicas for Kafka topics tootake advantage of underlying hardware rack configuration.</span></span> <span data-ttu-id="f2f41-106">Bu yapılandırma, Hdınsight üzerinde Apache Kafka depolanan verileri hello kullanılabilirliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="f2f41-106">This configuration ensures hello availability of data stored in Apache Kafka on HDInsight.</span></span>

## <a name="fault-and-update-domains-with-kafka"></a><span data-ttu-id="f2f41-107">Kafka ile hata ve güncelleme etki alanları</span><span class="sxs-lookup"><span data-stu-id="f2f41-107">Fault and update domains with Kafka</span></span>

<span data-ttu-id="f2f41-108">Hata etki alanı, bir Azure veri merkezinde temel donanımlardan oluşan mantıksal bir gruplandırmadır.</span><span class="sxs-lookup"><span data-stu-id="f2f41-108">A fault domain is a logical grouping of underlying hardware in an Azure data center.</span></span> <span data-ttu-id="f2f41-109">Her hata etki alanı ortak bir güç kaynağı ve ağ anahtarına sahiptir.</span><span class="sxs-lookup"><span data-stu-id="f2f41-109">Each fault domain shares a common power source and network switch.</span></span> <span data-ttu-id="f2f41-110">Bu hata etki alanlarında Hello sanal makineler ve Hdınsight kümesi içinde hello düğümleri uygulamak yönetilen diskleri dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="f2f41-110">hello virtual machines and managed disks that implement hello nodes within an HDInsight cluster are distributed across these fault domains.</span></span> <span data-ttu-id="f2f41-111">Bu mimari, fiziksel donanım hatalarının olası etkisini hello sınırlar.</span><span class="sxs-lookup"><span data-stu-id="f2f41-111">This architecture limits hello potential impact of physical hardware failures.</span></span>

<span data-ttu-id="f2f41-112">Her Azure bölgesinde belirli sayıda hata etki alanı bulunur.</span><span class="sxs-lookup"><span data-stu-id="f2f41-112">Each Azure region has a specific number of fault domains.</span></span> <span data-ttu-id="f2f41-113">Merhaba etki alanları ve içerdikleri hata etki alanı hello sayısı listesi için bkz [kullanılabilirlik kümeleri](../virtual-machines/linux/regions-and-availability.md#availability-sets) belgeleri.</span><span class="sxs-lookup"><span data-stu-id="f2f41-113">For a list of domains and hello number of fault domains they contain, see hello [Availability sets](../virtual-machines/linux/regions-and-availability.md#availability-sets) documentation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f2f41-114">Kafka, hata etki alanları ile uyumlu değildir.</span><span class="sxs-lookup"><span data-stu-id="f2f41-114">Kafka is not aware of fault domains.</span></span> <span data-ttu-id="f2f41-115">Kafka bir konu oluşturduğunuzda, tüm çoğaltmalarını hello depolayabilir aynı hata etki alanı.</span><span class="sxs-lookup"><span data-stu-id="f2f41-115">When you create a topic in Kafka, it may store all partition replicas in hello same fault domain.</span></span> <span data-ttu-id="f2f41-116">toosolve hello sağladığımız Bu sorun [Kafka bölüm yeniden dengeleyin aracını](https://github.com/hdinsight/hdinsight-kafka-tools).</span><span class="sxs-lookup"><span data-stu-id="f2f41-116">toosolve this problem, we provide hello [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools).</span></span>

## <a name="when-toorebalance-partition-replicas"></a><span data-ttu-id="f2f41-117">Ne zaman toorebalance bölüm çoğaltmaları</span><span class="sxs-lookup"><span data-stu-id="f2f41-117">When toorebalance partition replicas</span></span>

<span data-ttu-id="f2f41-118">Kafka verilerinizin tooensure hello yüksek kullanılabilirlik, size hello çoğaltmalarını Konunuzu kez hello adresindeki için yeniden dengelemeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="f2f41-118">tooensure hello highest availability of your Kafka data, you should rebalance hello partition replicas for your topic at hello following times:</span></span>

* <span data-ttu-id="f2f41-119">Yeni bir konu veya bölüm oluşturulduğunda</span><span class="sxs-lookup"><span data-stu-id="f2f41-119">When a new topic or partition is created</span></span>

* <span data-ttu-id="f2f41-120">Bir kümenin ölçeğini artırdığınızda</span><span class="sxs-lookup"><span data-stu-id="f2f41-120">When you scale up a cluster</span></span>

## <a name="replication-factor"></a><span data-ttu-id="f2f41-121">Çoğaltma faktörü</span><span class="sxs-lookup"><span data-stu-id="f2f41-121">Replication factor</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f2f41-122">Üç hata etki alanı içeren ve çoğaltma faktörü 3 olan bir Azure bölgesi kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="f2f41-122">We recommend using an Azure region that contains three fault domains, and using a replication factor of 3.</span></span>

<span data-ttu-id="f2f41-123">Yalnızca iki hata etki alanları içeren bir bölge kullanmanız gerekiyorsa, bir çoğaltma faktörü 4 toospread hello çoğaltmalarının hello iki hata etki alanları arasında eşit olarak kullanın.</span><span class="sxs-lookup"><span data-stu-id="f2f41-123">If you must use a region that contains only two fault domains, use a replication factor of 4 toospread hello replicas evenly across hello two fault domains.</span></span>

<span data-ttu-id="f2f41-124">Hello konuları ve ayarı hello çoğaltma faktörü oluşturma örneği için bkz: [hdınsight'ta Kafka başlayarak](hdinsight-apache-kafka-get-started.md) belge.</span><span class="sxs-lookup"><span data-stu-id="f2f41-124">For an example of creating topics and setting hello replication factor, see hello [Start with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md) document.</span></span>

## <a name="how-toorebalance-partition-replicas"></a><span data-ttu-id="f2f41-125">Nasıl toorebalance bölüm çoğaltmaları</span><span class="sxs-lookup"><span data-stu-id="f2f41-125">How toorebalance partition replicas</span></span>

<span data-ttu-id="f2f41-126">Kullanım hello [Kafka bölüm yeniden dengeleyin aracını](https://github.com/hdinsight/hdinsight-kafka-tools) toorebalance Seçili konular.</span><span class="sxs-lookup"><span data-stu-id="f2f41-126">Use hello [Kafka partition rebalance tool](https://github.com/hdinsight/hdinsight-kafka-tools) toorebalance selected topics.</span></span> <span data-ttu-id="f2f41-127">Bu aracı gerekir olması çalıştırdım bir SSH oturumu toohello baş düğümünden Kafka kümenizin.</span><span class="sxs-lookup"><span data-stu-id="f2f41-127">This tool must be ran from an SSH session toohello head node of your Kafka cluster.</span></span>

<span data-ttu-id="f2f41-128">SSH kullanarak tooHDInsight bağlama hakkında daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md) belge.</span><span class="sxs-lookup"><span data-stu-id="f2f41-128">For more information on connecting tooHDInsight using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2f41-129">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f2f41-129">Next steps</span></span>

* [<span data-ttu-id="f2f41-130">HDInsight’ta Kafka ölçeklenebilirliği</span><span class="sxs-lookup"><span data-stu-id="f2f41-130">Scalability of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-scalability.md)
* [<span data-ttu-id="f2f41-131">HDInsight'ta Kafka ile yansıtma</span><span class="sxs-lookup"><span data-stu-id="f2f41-131">Mirroring with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)