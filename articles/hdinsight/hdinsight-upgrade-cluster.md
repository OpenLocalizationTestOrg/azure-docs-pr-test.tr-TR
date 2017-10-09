---
title: "aaaUpgrade Hdınsight küme tooa daha yeni sürümü-Azure | Microsoft Docs"
description: "Nasıl tooUpgrade Hdınsight küme tooa daha yeni sürüm bilgi edinin."
services: hdinsight
documentationcenter: 
author: bhanupr
manager: asadk
editor: bhanupr
ms.assetid: 60eb573c-e639-4815-9fc6-ea8b106d8dbc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/04/2017
ms.author: bhanupr
ms.openlocfilehash: 5fff3c9bc88dfbcbc1ccb0188accdfbbec3a62f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="upgrade-hdinsight-cluster-tooa-newer-version"></a><span data-ttu-id="75c45-103">Hdınsight küme tooa daha yeni sürümüne yükseltin</span><span class="sxs-lookup"><span data-stu-id="75c45-103">Upgrade HDInsight cluster tooa newer version</span></span>
<span data-ttu-id="75c45-104">tootake avantajlarından Merhaba son Hdınsight özellikleri, Hdınsight kümeleri yükseltilmiş toolatest sürüm olmasını öneririz.</span><span class="sxs-lookup"><span data-stu-id="75c45-104">tootake advantage of hello latest HDInsight features, we recommend that HDInsight clusters be upgraded toolatest version.</span></span> <span data-ttu-id="75c45-105">Merhaba yönergeleri tooupgrade aşağıda Hdınsight küme sürümleri izleyin.</span><span class="sxs-lookup"><span data-stu-id="75c45-105">Follow hello below guidelines tooupgrade your HDInsight cluster versions.</span></span>

> [!NOTE]
> <span data-ttu-id="75c45-106">Hdınsight kümesi sürüm 3.2 ve 3.3 tarihten dolmak üzere.</span><span class="sxs-lookup"><span data-stu-id="75c45-106">HDInsight clusters version 3.2 and 3.3 are nearing retirement date.</span></span> <span data-ttu-id="75c45-107">Hdınsight'ın desteklenen sürümünü hakkında daha fazla bilgi için bkz: [Hdınsight bileşen sürümü](hdinsight-component-versioning.md#supported-hdinsight-versions).</span><span class="sxs-lookup"><span data-stu-id="75c45-107">For information on supported version of HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>
>
>

## <a name="upgrade-tasks"></a><span data-ttu-id="75c45-108">Yükseltme görevleri</span><span class="sxs-lookup"><span data-stu-id="75c45-108">Upgrade tasks</span></span>
<span data-ttu-id="75c45-109">Merhaba iş akışı tooupgrade Hdınsight kümesi aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="75c45-109">hello workflow tooupgrade HDInsight Cluster is as follows.</span></span>

![Yükseltme iş akışı diyagramı](./media/hdinsight-upgrade-cluster/upgrade-workflow.png)

1. <span data-ttu-id="75c45-111">Bu belgenin her bölüm Hdınsight kümenize yükseltirken gerekli olabilecek toounderstand değişiklikleri okuyun.</span><span class="sxs-lookup"><span data-stu-id="75c45-111">Read each section of this document toounderstand changes that may be required when upgrading your HDInsight cluster.</span></span>
2. <span data-ttu-id="75c45-112">Bir küme bir test/kalite güvence ortamı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="75c45-112">Create a cluster as a test/quality assurance environment.</span></span> <span data-ttu-id="75c45-113">Küme oluşturma ile ilgili daha fazla bilgi için bkz: [nasıl toocreate Linux tabanlı Hdınsight kümeleri öğrenin](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="75c45-113">For more information on creating a cluster, see [Learn how toocreate Linux-based HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
3. <span data-ttu-id="75c45-114">İşleri, veri kaynakları ve havuzlarını toohello yeni ortam varolan kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="75c45-114">Copy existing jobs, data sources, and sinks toohello new environment.</span></span> <span data-ttu-id="75c45-115">Bkz: [veri Kopyala tooTest ortam](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="75c45-115">See [Copy Data tooTest Environment](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) for more details.</span></span>
4. <span data-ttu-id="75c45-116">Toomake işleriniz hello yeni kümede beklendiği gibi çalıştığından emin sınama doğrulaması gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="75c45-116">Perform validation testing toomake sure that your jobs work as expected on hello new cluster.</span></span>


<span data-ttu-id="75c45-117">Her şeyin beklendiği gibi çalıştığını doğruladıktan sonra hello geçiş için kapalı kalma süresi zamanlayın.</span><span class="sxs-lookup"><span data-stu-id="75c45-117">Once you have verified that everything works as expected, schedule downtime for hello migration.</span></span> <span data-ttu-id="75c45-118">Bu kesinti sırasında aşağıdaki işlemleri hello:</span><span class="sxs-lookup"><span data-stu-id="75c45-118">During this downtime, do hello following actions:</span></span>

1.  <span data-ttu-id="75c45-119">Merhaba küme düğümlerinde yerel olarak depolanan tüm geçici verileri yedekleyin.</span><span class="sxs-lookup"><span data-stu-id="75c45-119">Back up any transient data stored locally on hello cluster nodes.</span></span> <span data-ttu-id="75c45-120">Örneğin, doğrudan bir baş düğüm üzerinde depolanan verileri varsa.</span><span class="sxs-lookup"><span data-stu-id="75c45-120">For example, if you have data stored directly on a head node.</span></span>
2.  <span data-ttu-id="75c45-121">Merhaba var olan küme silin.</span><span class="sxs-lookup"><span data-stu-id="75c45-121">Delete hello existing cluster.</span></span>
3.  <span data-ttu-id="75c45-122">Bir küme oluşturmak hello kullanılan önceki küme hello aynı varsayılan veri deposu hello VNET en son (veya desteklenen) olan bir alt ağ HDI sürümü kullanarak aynı.</span><span class="sxs-lookup"><span data-stu-id="75c45-122">Create a cluster in hello same VNET subnet with latest (or supported) HDI version using hello same default data store that hello previous cluster used.</span></span> <span data-ttu-id="75c45-123">Bu, var olan üretim verileriyle çalışma hello yeni küme toocontinue sağlar.</span><span class="sxs-lookup"><span data-stu-id="75c45-123">This allows hello new cluster toocontinue working against your existing production data.</span></span>
4.  <span data-ttu-id="75c45-124">Yedeklediğiniz herhangi bir geçici veri içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="75c45-124">Import any transient data you backed up.</span></span>
5.  <span data-ttu-id="75c45-125">Başlangıç işleri/hello yeni küme kullanarak işlemeye devam et.</span><span class="sxs-lookup"><span data-stu-id="75c45-125">Start jobs/continue processing using hello new cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="75c45-126">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="75c45-126">Next Steps</span></span>
* [<span data-ttu-id="75c45-127">Nasıl toocreate Linux tabanlı Hdınsight kümeleri öğrenin</span><span class="sxs-lookup"><span data-stu-id="75c45-127">Learn how toocreate Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="75c45-128">SSH kullanarak tooHDInsight Bağlan</span><span class="sxs-lookup"><span data-stu-id="75c45-128">Connect tooHDInsight using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)
* [<span data-ttu-id="75c45-129">Ambari kullanarak Linux tabanlı bir kümeyi yönetmek</span><span class="sxs-lookup"><span data-stu-id="75c45-129">Manage a Linux-based cluster using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

