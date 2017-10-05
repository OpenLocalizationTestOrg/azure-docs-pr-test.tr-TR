---
title: "Daha yeni bir sürüme yükseltme Hdınsight küme-Azure | Microsoft Docs"
description: "Bilgi daha yeni bir sürüme yükseltme Hdınsight kümesi nasıl."
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
ms.openlocfilehash: fa2e37bd922690322ccc3d8f68128180d013b701
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="upgrade-hdinsight-cluster-to-a-newer-version"></a><span data-ttu-id="39898-103">Hdınsight kümesi daha yeni bir sürüme yükseltin</span><span class="sxs-lookup"><span data-stu-id="39898-103">Upgrade HDInsight cluster to a newer version</span></span>
<span data-ttu-id="39898-104">En son Hdınsight özelliklerden yararlanmak için Hdınsight kümeleri en son sürümüne yükseltilmesi önerilir.</span><span class="sxs-lookup"><span data-stu-id="39898-104">To take advantage of the latest HDInsight features, we recommend that HDInsight clusters be upgraded to latest version.</span></span> <span data-ttu-id="39898-105">İzleyin, Hdınsight yükseltmek için yönergeleri sürümleri küme.</span><span class="sxs-lookup"><span data-stu-id="39898-105">Follow the below guidelines to upgrade your HDInsight cluster versions.</span></span>

> [!NOTE]
> <span data-ttu-id="39898-106">Hdınsight kümesi sürüm 3.2 ve 3.3 tarihten dolmak üzere.</span><span class="sxs-lookup"><span data-stu-id="39898-106">HDInsight clusters version 3.2 and 3.3 are nearing retirement date.</span></span> <span data-ttu-id="39898-107">Hdınsight'ın desteklenen sürümünü hakkında daha fazla bilgi için bkz: [Hdınsight bileşen sürümü](hdinsight-component-versioning.md#supported-hdinsight-versions).</span><span class="sxs-lookup"><span data-stu-id="39898-107">For information on supported version of HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>
>
>

## <a name="upgrade-tasks"></a><span data-ttu-id="39898-108">Yükseltme görevleri</span><span class="sxs-lookup"><span data-stu-id="39898-108">Upgrade tasks</span></span>
<span data-ttu-id="39898-109">Hdınsight Küme yükseltme iş akışı aşağıdaki gibidir.</span><span class="sxs-lookup"><span data-stu-id="39898-109">The workflow to upgrade HDInsight Cluster is as follows.</span></span>

![Yükseltme iş akışı diyagramı](./media/hdinsight-upgrade-cluster/upgrade-workflow.png)

1. <span data-ttu-id="39898-111">Hdınsight kümenize yükseltirken gerekli olabilecek değişiklikleri anlamak için bu belgenin her bölümünü okuyun.</span><span class="sxs-lookup"><span data-stu-id="39898-111">Read each section of this document to understand changes that may be required when upgrading your HDInsight cluster.</span></span>
2. <span data-ttu-id="39898-112">Bir küme bir test/kalite güvence ortamı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="39898-112">Create a cluster as a test/quality assurance environment.</span></span> <span data-ttu-id="39898-113">Küme oluşturma ile ilgili daha fazla bilgi için bkz: [Linux tabanlı Hdınsight kümeleri oluşturma hakkında bilgi edinin](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="39898-113">For more information on creating a cluster, see [Learn how to create Linux-based HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
3. <span data-ttu-id="39898-114">Var olan işleri, veri kaynakları ve havuzlarını yeni ortamına kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="39898-114">Copy existing jobs, data sources, and sinks to the new environment.</span></span> <span data-ttu-id="39898-115">Bkz: [Test ortamı için kopyalama veri](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="39898-115">See [Copy Data To Test Environment](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) for more details.</span></span>
4. <span data-ttu-id="39898-116">İşleriniz yeni kümede beklendiği gibi çalıştığından emin olmak için doğrulama testleri gerçekleştirme.</span><span class="sxs-lookup"><span data-stu-id="39898-116">Perform validation testing to make sure that your jobs work as expected on the new cluster.</span></span>


<span data-ttu-id="39898-117">Her şeyin beklendiği gibi çalıştığını doğruladıktan sonra geçiş kapalı kalma süresini zamanlayın.</span><span class="sxs-lookup"><span data-stu-id="39898-117">Once you have verified that everything works as expected, schedule downtime for the migration.</span></span> <span data-ttu-id="39898-118">Bu kesinti sırasında aşağıdaki eylemleri gerçekleştirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="39898-118">During this downtime, do the following actions:</span></span>

1.  <span data-ttu-id="39898-119">Küme düğümlerinde yerel olarak depolanan tüm geçici verileri yedekleyin.</span><span class="sxs-lookup"><span data-stu-id="39898-119">Back up any transient data stored locally on the cluster nodes.</span></span> <span data-ttu-id="39898-120">Örneğin, doğrudan bir baş düğüm üzerinde depolanan verileri varsa.</span><span class="sxs-lookup"><span data-stu-id="39898-120">For example, if you have data stored directly on a head node.</span></span>
2.  <span data-ttu-id="39898-121">Var olan küme silin.</span><span class="sxs-lookup"><span data-stu-id="39898-121">Delete the existing cluster.</span></span>
3.  <span data-ttu-id="39898-122">Bir küme aynı sanal alt ağdaki önceki küme tarafından kullanılan varsayılan veri deposu kullanarak en son (veya desteklenen) HDI sürümü ile oluşturun.</span><span class="sxs-lookup"><span data-stu-id="39898-122">Create a cluster in the same VNET subnet with latest (or supported) HDI version using the same default data store that the previous cluster used.</span></span> <span data-ttu-id="39898-123">Bu, var olan üretim verilerinizi karşı çalışmaya devam etmek yeni küme sağlar.</span><span class="sxs-lookup"><span data-stu-id="39898-123">This allows the new cluster to continue working against your existing production data.</span></span>
4.  <span data-ttu-id="39898-124">Yedeklediğiniz herhangi bir geçici veri içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="39898-124">Import any transient data you backed up.</span></span>
5.  <span data-ttu-id="39898-125">Başlangıç işleri/yeni küme kullanarak işlemeye devam et.</span><span class="sxs-lookup"><span data-stu-id="39898-125">Start jobs/continue processing using the new cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39898-126">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="39898-126">Next Steps</span></span>
* [<span data-ttu-id="39898-127">Linux tabanlı Hdınsight kümeleri oluşturma hakkında bilgi edinin</span><span class="sxs-lookup"><span data-stu-id="39898-127">Learn how to create Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="39898-128">SSH kullanarak Hdınsight Bağlan</span><span class="sxs-lookup"><span data-stu-id="39898-128">Connect to HDInsight using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)
* [<span data-ttu-id="39898-129">Ambari kullanarak Linux tabanlı bir kümeyi yönetmek</span><span class="sxs-lookup"><span data-stu-id="39898-129">Manage a Linux-based cluster using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

