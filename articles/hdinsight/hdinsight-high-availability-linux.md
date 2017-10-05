---
title: "Yüksek kullanılabilirlik için Hadoop - Azure Hdınsight | Microsoft Docs"
description: "Nasıl Hdınsight kümeleri güvenilirlik ve kullanılabilirlik ek bir baş düğüm kullanarak iyileştirmek öğrenin. Nasıl bu Ambari ve Hive gibi Hadoop Hizmetleri yanı sıra tek tek SSH kullanarak her baş düğümüne bağlanmak için etkilediğini öğrenin."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: Blackmist
documentationcenter: 
tags: azure-portal
keywords: "hadoop yüksek kullanılabilirlik"
ms.assetid: 99c9f59c-cf6b-4529-99d1-bf060435e8d4
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 07/28/2017
ms.author: larryfr
ms.openlocfilehash: e66ba67a36fc48d1762ba302d708e060489fdc71
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="availability-and-reliability-of-hadoop-clusters-in-hdinsight"></a><span data-ttu-id="7b2a6-105">HDInsight'ta Hadoop kümelerinin kullanılabilirliği ve güvenilirliği</span><span class="sxs-lookup"><span data-stu-id="7b2a6-105">Availability and reliability of Hadoop clusters in HDInsight</span></span>

<span data-ttu-id="7b2a6-106">Hdınsight kümeleri, kullanılabilirlik ve Hadoop Hizmetleri ve çalışan işleri güvenilirliğini artırmak için iki baş düğümler sağlar.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-106">HDInsight clusters provide two head nodes to increase the availability and reliability of Hadoop services and jobs running.</span></span>

<span data-ttu-id="7b2a6-107">Hadoop bir kümede birden çok düğüm arasında Hizmetleri ve veri çoğaltma tarafından yüksek kullanılabilirlik ve güvenilirlik elde eder.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-107">Hadoop achieves high availability and reliability by replicating services and data across multiple nodes in a cluster.</span></span> <span data-ttu-id="7b2a6-108">Ancak standart dağıtımları hadoop genellikle yalnızca tek bir baş düğüm vardır.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-108">However standard distributions of Hadoop typically have only a single head node.</span></span> <span data-ttu-id="7b2a6-109">Tek baş düğümü herhangi kesinti, küme çalışmayı durdurmasına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-109">Any outage of the single head node can cause the cluster to stop working.</span></span> <span data-ttu-id="7b2a6-110">Hdınsight Hadoop'ın kullanılabilirliği ve güvenilirliği iyileştirmek için iki headnodes sağlar.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-110">HDInsight provides two headnodes to improve Hadoop's availability and reliability.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7b2a6-111">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7b2a6-112">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="7b2a6-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="availability-and-reliability-of-nodes"></a><span data-ttu-id="7b2a6-113">Kullanılabilirliği ve güvenilirliği düğümlerinin</span><span class="sxs-lookup"><span data-stu-id="7b2a6-113">Availability and reliability of nodes</span></span>

<span data-ttu-id="7b2a6-114">Hdınsight kümesi düğümünde, Azure sanal makineleri kullanarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-114">Nodes in an HDInsight cluster are implemented using Azure Virtual Machines.</span></span> <span data-ttu-id="7b2a6-115">Aşağıdaki bölümlerde, Hdınsight ile kullanılan tek tek düğüm türleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-115">The following sections discuss the individual node types used with HDInsight.</span></span> 

> [!NOTE]
> <span data-ttu-id="7b2a6-116">Tüm düğüm türleri için bir küme türü kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-116">Not all node types are used for a cluster type.</span></span> <span data-ttu-id="7b2a6-117">Örneğin, Hadoop küme türü hiçbir Nimbus düğümü yok.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-117">For example, a Hadoop cluster type does not have any Nimbus nodes.</span></span> <span data-ttu-id="7b2a6-118">Hdınsight küme türleri tarafından kullanılan düğümleri hakkında daha fazla bilgi için küme türleri bölümüne bakın [Hdınsight oluşturma Linux tabanlı Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) belge.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-118">For more information on nodes used by HDInsight cluster types, see the Cluster types section of the [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) document.</span></span>

### <a name="head-nodes"></a><span data-ttu-id="7b2a6-119">Baş düğümler</span><span class="sxs-lookup"><span data-stu-id="7b2a6-119">Head nodes</span></span>

<span data-ttu-id="7b2a6-120">Hadoop Hizmetleri yüksek kullanılabilirliğini sağlamak için iki baş düğüm Hdınsight sağlar.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-120">To ensure high availability of Hadoop services, HDInsight provides two head nodes.</span></span> <span data-ttu-id="7b2a6-121">Her iki baş düğümler aynı anda etkin ve Hdınsight kümesi içinde çalışır.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-121">Both head nodes are active and running within the HDInsight cluster simultaneously.</span></span> <span data-ttu-id="7b2a6-122">HDFS veya YARN gibi bazı hizmetler, herhangi bir anda yalnızca bir baş düğüm üzerinde ' active'.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-122">Some services, such as HDFS or YARN, are only 'active' on one head node at any given time.</span></span> <span data-ttu-id="7b2a6-123">HiveServer2 veya Hive meta depo gibi başka hizmetleri aynı anda hem baş düğümler üzerinde etkindir.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-123">Other services such as HiveServer2 or Hive MetaStore are active on both head nodes at the same time.</span></span>

<span data-ttu-id="7b2a6-124">Baş düğümler (ve diğer düğümlere hdınsight'ta) ana bilgisayar adı düğümün bir parçası olarak sayısal bir değere sahip.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-124">Head nodes (and other nodes in HDInsight) have a numeric value as part of the hostname of the node.</span></span> <span data-ttu-id="7b2a6-125">Örneğin, `hn0-CLUSTERNAME` veya `hn4-CLUSTERNAME`.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-125">For example, `hn0-CLUSTERNAME` or `hn4-CLUSTERNAME`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7b2a6-126">Sayısal değer, bir düğüm birincil veya ikincil ile ilişkilendirmeyin.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-126">Do not associate the numeric value with whether a node is primary or secondary.</span></span> <span data-ttu-id="7b2a6-127">Sayısal değer yalnızca her düğüm için benzersiz bir ad sağlamak için mevcuttur.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-127">The numeric value is only present to provide a unique name for each node.</span></span>

### <a name="nimbus-nodes"></a><span data-ttu-id="7b2a6-128">Nimbus Düğümleri</span><span class="sxs-lookup"><span data-stu-id="7b2a6-128">Nimbus Nodes</span></span>

<span data-ttu-id="7b2a6-129">Nimbus düğümü Storm kümeleri ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-129">Nimbus nodes are available with Storm clusters.</span></span> <span data-ttu-id="7b2a6-130">Nimbus düğümü dağıtma ve çalışan düğümleri arasında işlem izleme Hadoop Jobtracker'a benzer işlevsellik sağlar.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-130">The Nimbus nodes provide similar functionality to the Hadoop JobTracker by distributing and monitoring processing across worker nodes.</span></span> <span data-ttu-id="7b2a6-131">Hdınsight iki Nimbus düğümü Storm kümeleri için sağlar.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-131">HDInsight provides two Nimbus nodes for Storm clusters</span></span>

### <a name="zookeeper-nodes"></a><span data-ttu-id="7b2a6-132">Zookeeper düğümleri</span><span class="sxs-lookup"><span data-stu-id="7b2a6-132">Zookeeper nodes</span></span>

<span data-ttu-id="7b2a6-133">[ZooKeeper](http://zookeeper.apache.org/) düğümleri öncü seçim baş düğümler üzerinde ana Hizmetleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-133">[ZooKeeper](http://zookeeper.apache.org/) nodes are used for leader election of master services on head nodes.</span></span> <span data-ttu-id="7b2a6-134">Hizmetleri, veri (çalışan) düğümlerini ve ağ geçitlerini hangi baş düğüm hizmet ana etkin biliyor olması güvence altına için de kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-134">They are also used to insure that services, data (worker) nodes, and gateways know which head node a master service is active on.</span></span> <span data-ttu-id="7b2a6-135">Varsayılan olarak, Hdınsight üç ZooKeeper düğümleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-135">By default, HDInsight provides three ZooKeeper nodes.</span></span>

### <a name="worker-nodes"></a><span data-ttu-id="7b2a6-136">Çalışan düğümü</span><span class="sxs-lookup"><span data-stu-id="7b2a6-136">Worker nodes</span></span>

<span data-ttu-id="7b2a6-137">Bir işi kümeye gönderildiğinde çalışan düğümleri gerçek veri çözümlemesi gerçekleştirme.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-137">Worker nodes perform the actual data analysis when a job is submitted to the cluster.</span></span> <span data-ttu-id="7b2a6-138">Çalışan düğüm başarısız olursa, bunu gerçekleştirme görev başka bir çalışan düğümüne gönderilir.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-138">If a worker node fails, the task that it was performing is submitted to another worker node.</span></span> <span data-ttu-id="7b2a6-139">Varsayılan olarak, dört alt düğüm Hdınsight oluşturur.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-139">By default, HDInsight creates four worker nodes.</span></span> <span data-ttu-id="7b2a6-140">Bu numarayı sırasında hem Küme oluşturulduktan sonra gereksinimlerinize uyacak şekilde değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-140">You can change this number to suit your needs both during and after cluster creation.</span></span>

### <a name="edge-node"></a><span data-ttu-id="7b2a6-141">Kenar düğümüne</span><span class="sxs-lookup"><span data-stu-id="7b2a6-141">Edge node</span></span>

<span data-ttu-id="7b2a6-142">Bir kenar düğümüne, veri analizi kümedeki etkin olarak katılmıyor.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-142">An edge node does not actively participate in data analysis within the cluster.</span></span> <span data-ttu-id="7b2a6-143">Hadoop ile çalışırken, geliştiriciler veya veri bilimcilerine tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-143">It is used by developers or data scientists when working with Hadoop.</span></span> <span data-ttu-id="7b2a6-144">Kenar düğümüne kümedeki diğer düğümlere aynı Azure sanal ağ içinde yaşar ve diğer tüm düğümlere doğrudan erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-144">The edge node lives in the same Azure Virtual Network as the other nodes in the cluster, and can directly access all other nodes.</span></span> <span data-ttu-id="7b2a6-145">Kenar düğümüne kritik Hadoop Hizmetleri veya analiz işleri çıktığınızda kaynakları bırakmadan kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-145">The edge node can be used without taking resources away from critical Hadoop services or analysis jobs.</span></span>

<span data-ttu-id="7b2a6-146">Şu anda, hdınsight'ta R Server varsayılan olarak bir kenar düğümüne sağlayan yalnızca küme türüdür.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-146">Currently, R Server on HDInsight is the only cluster type that provides an edge node by default.</span></span> <span data-ttu-id="7b2a6-147">Kenar düğümüne hdınsight'ta R Server için kullanılan düğümde dağıtılan işleme için kümeye göndermeden önce yerel olarak test R kodu.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-147">For R Server on HDInsight, the edge node is used test R code locally on the node before submitting it to the cluster for distributed processing.</span></span>

<span data-ttu-id="7b2a6-148">R Server dışındaki küme türleriyle bir kenar düğümüne kullanma hakkında daha fazla bilgi için bkz: [Hdınsight'ta kenar düğümünü kullanmak](hdinsight-apps-use-edge-node.md) belge.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-148">For information on using an edge node with cluster types other than R Server, see the [Use edge nodes in HDInsight](hdinsight-apps-use-edge-node.md) document.</span></span>

## <a name="accessing-the-nodes"></a><span data-ttu-id="7b2a6-149">Düğümlere erişme</span><span class="sxs-lookup"><span data-stu-id="7b2a6-149">Accessing the nodes</span></span>

<span data-ttu-id="7b2a6-150">Ortak ağ geçidi üzerinden internet üzerinden kümesine erişimi sağlanır.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-150">Access to the cluster over the internet is provided through a public gateway.</span></span> <span data-ttu-id="7b2a6-151">Erişim baş düğümler bağlanmakta sınırlı ve (varsa,) kenar düğümüne.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-151">Access is limited to connecting to the head nodes and (if one exists) the edge node.</span></span> <span data-ttu-id="7b2a6-152">Baş düğümler üzerinde çalışan hizmetlerine erişim birden çok baş düğümler sağlayarak parametreden etkilenir değil.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-152">Access to services running on the head nodes is not effected by having multiple head nodes.</span></span> <span data-ttu-id="7b2a6-153">Ortak ağ geçidi istekleri istenen hizmeti barındıran baş düğüme yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-153">The public gateway routes requests to the head node that hosts the requested service.</span></span> <span data-ttu-id="7b2a6-154">Ambari şu anda ikincil baş düğüm üzerinde barındırılıyorsa, örneğin, ağ geçidi gelen istekleri için Ambari bu düğüme yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-154">For example, if Ambari is currently hosted on the secondary head node, the gateway routes incoming requests for Ambari to that node.</span></span>

<span data-ttu-id="7b2a6-155">Ortak ağ geçidi üzerinden erişim bağlantı noktası 443 (HTTPS), 22 ve 23 sınırlıdır.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-155">Access over the public gateway is limited to port 443 (HTTPS), 22, and 23.</span></span>

* <span data-ttu-id="7b2a6-156">Bağlantı noktası __443__ Ambari ve diğer web kullanıcı Arabirimi veya baş düğümler üzerinde barındırılan REST API'lerine erişmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-156">Port __443__ is used to access Ambari and other web UI or REST APIs hosted on the head nodes.</span></span>

* <span data-ttu-id="7b2a6-157">Bağlantı noktası __22__ birincil baş düğüm veya kenar düğümüne SSH ile erişmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-157">Port __22__ is used to access the primary head node or edge node with SSH.</span></span>

* <span data-ttu-id="7b2a6-158">Bağlantı noktası __23__ ikincil baş düğüm SSH ile erişmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-158">Port __23__ is used to access the secondary head node with SSH.</span></span> <span data-ttu-id="7b2a6-159">Örneğin, `ssh username@mycluster-ssh.azurehdinsight.net` adlı Küme birincil baş düğüme bağlanan **mycluster**.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-159">For example, `ssh username@mycluster-ssh.azurehdinsight.net` connects to the primary head node of the cluster named **mycluster**.</span></span>

<span data-ttu-id="7b2a6-160">SSH kullanma hakkında daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md) belge.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-160">For more information on using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

### <a name="internal-fully-qualified-domain-names-fqdn"></a><span data-ttu-id="7b2a6-161">İç tam etki alanı adları (FQDN)</span><span class="sxs-lookup"><span data-stu-id="7b2a6-161">Internal fully qualified domain names (FQDN)</span></span>

<span data-ttu-id="7b2a6-162">Bir Hdınsight küme düğümlerinde bir iç IP adresi ve yalnızca kümeden erişilebilir FQDN vardır.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-162">Nodes in an HDInsight cluster have an internal IP address and FQDN that can only be accessed from the cluster.</span></span> <span data-ttu-id="7b2a6-163">İç FQDN veya IP adresi kullanarak kümeye Services'de erişilirken, IP veya FQDN hizmeti erişirken kullanılacak doğrulamak için Ambari kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-163">When accessing services on the cluster using the internal FQDN or IP address, you should use Ambari to verify the IP or FQDN to use when accessing the service.</span></span>

<span data-ttu-id="7b2a6-164">Örneğin, Oozie hizmeti yalnızca bir baş düğüm ve kullanarak çalışabilir `oozie` bir SSH oturumu komuttan Hizmeti'ne URL gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-164">For example, the Oozie service can only run on one head node, and using the `oozie` command from an SSH session requires the URL to the service.</span></span> <span data-ttu-id="7b2a6-165">Bu URL, aşağıdaki komutu kullanarak Ambari alınabilir:</span><span class="sxs-lookup"><span data-stu-id="7b2a6-165">This URL can be retrieved from Ambari by using the following command:</span></span>

    curl -u admin:PASSWORD "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations?type=oozie-site&tag=TOPOLOGY_RESOLVED" | grep oozie.base.url

<span data-ttu-id="7b2a6-166">Bu komut bir değer ile kullanılacak İç URL içeren aşağıdaki komutu benzer döndürür `oozie` komutu:</span><span class="sxs-lookup"><span data-stu-id="7b2a6-166">This command returns a value similar to the following command, which contains the internal URL to use with the `oozie` command:</span></span>

    "oozie.base.url": "http://hn0-CLUSTERNAME-randomcharacters.cx.internal.cloudapp.net:11000/oozie"

<span data-ttu-id="7b2a6-167">Ambari REST API ile çalışma hakkında daha fazla bilgi için bkz: [izleme ve yönetme Ambari REST API kullanarak Hdınsight'ta](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="7b2a6-167">For more information on working with the Ambari REST API, see [Monitor and Manage HDInsight using the Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

### <a name="accessing-other-node-types"></a><span data-ttu-id="7b2a6-168">Diğer düğüm türleri erişme</span><span class="sxs-lookup"><span data-stu-id="7b2a6-168">Accessing other node types</span></span>

<span data-ttu-id="7b2a6-169">Internet üzerinden aşağıdaki yöntemleri kullanarak doğrudan erişilemeyen düğümlere bağlanabilir:</span><span class="sxs-lookup"><span data-stu-id="7b2a6-169">You can connect to nodes that are not directly accessible over the internet by using the following methods:</span></span>

* <span data-ttu-id="7b2a6-170">**SSH**: SSH kullanarak bir baş düğüm bağlandıktan sonra ardından SSH baş düğümünden kümedeki diğer düğümlere bağlamak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-170">**SSH**: Once connected to a head node using SSH, you can then use SSH from the head node to connect to other nodes in the cluster.</span></span> <span data-ttu-id="7b2a6-171">Daha fazla bilgi için [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md) belgesine bakın.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-171">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

* <span data-ttu-id="7b2a6-172">**SSH tüneli**: Internet'e gösterilmeyen düğümlerinden biri üzerinde barındırılan bir web hizmetine erişim gerekiyorsa, bir SSH tüneli kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-172">**SSH Tunnel**: If you need to access a web service hosted on one of the nodes that is not exposed to the internet, you must use an SSH tunnel.</span></span> <span data-ttu-id="7b2a6-173">Daha fazla bilgi için bkz: [Hdınsight ile SSH tüneli kullanma](hdinsight-linux-ambari-ssh-tunnel.md) belge.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-173">For more information, see the [Use an SSH tunnel with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

* <span data-ttu-id="7b2a6-174">**Azure sanal ağı**: Hdınsight kümenize bir Azure sanal ağının parçası ise, aynı sanal ağda herhangi bir kaynağa kümedeki tüm düğümlere doğrudan erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-174">**Azure Virtual Network**: If your HDInsight cluster is part of an Azure Virtual Network, any resource on the same Virtual Network can directly access all nodes in the cluster.</span></span> <span data-ttu-id="7b2a6-175">Daha fazla bilgi için bkz: [Azure sanal ağını kullanarak Hdınsight genişletmek](hdinsight-extend-hadoop-virtual-network.md) belge.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-175">For more information, see the [Extend HDInsight using Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

## <a name="how-to-check-on-a-service-status"></a><span data-ttu-id="7b2a6-176">Bir hizmet durumunu denetleme</span><span class="sxs-lookup"><span data-stu-id="7b2a6-176">How to check on a service status</span></span>

<span data-ttu-id="7b2a6-177">Baş düğümler üzerinde çalışan hizmetleri durumunu denetlemek için Ambari Web kullanıcı arabirimini veya Ambari REST API kullanın.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-177">To check the status of services that run on the head nodes, use the Ambari Web UI or the Ambari REST API.</span></span>

### <a name="ambari-web-ui"></a><span data-ttu-id="7b2a6-178">Ambari Web kullanıcı Arabirimi</span><span class="sxs-lookup"><span data-stu-id="7b2a6-178">Ambari Web UI</span></span>

<span data-ttu-id="7b2a6-179">Ambari Web kullanıcı arabirimini https://CLUSTERNAME.azurehdinsight.net görülebilir.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-179">The Ambari Web UI is viewable at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="7b2a6-180">**CLUSTERNAME** değerini kümenizin adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-180">Replace **CLUSTERNAME** with the name of your cluster.</span></span> <span data-ttu-id="7b2a6-181">İstenirse, kümeniz için HTTP kullanıcı kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-181">If prompted, enter the HTTP user credentials for your cluster.</span></span> <span data-ttu-id="7b2a6-182">Varsayılan HTTP kullanıcı adı **yönetici** ve küme oluştururken, girdiğiniz parola paroladır.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-182">The default HTTP user name is **admin** and the password is the password you entered when creating the cluster.</span></span>

<span data-ttu-id="7b2a6-183">Ambari sayfasında geldiğinde, yüklü hizmetleri sayfanın sol tarafta listelenir.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-183">When you arrive on the Ambari page, the installed services are listed on the left of the page.</span></span>

![Yüklü hizmetleri](./media/hdinsight-high-availability-linux/services.png)

<span data-ttu-id="7b2a6-185">Durumu göstermek için bir hizmet yanındaki görünebilir simgeleri bir dizi vardır.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-185">There are a series of icons that may appear next to a service to indicate status.</span></span> <span data-ttu-id="7b2a6-186">Kullanarak bir hizmeti ile ilgili herhangi bir uyarı görüntülenebilir **uyarıları** sayfanın üst kısmındaki bağlantı.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-186">Any alerts related to a service can be viewed using the **Alerts** link at the top of the page.</span></span> <span data-ttu-id="7b2a6-187">Daha fazla bilgi görüntülemek için her hizmet seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-187">You can select each service to view more information on it.</span></span>

<span data-ttu-id="7b2a6-188">Hizmet sayfasının durumu ve her hizmetin yapılandırma hakkında bilgi sağlarken, hangi baş düğümünde hizmetini çalıştıran bilgi sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-188">While the service page provides information on the status and configuration of each service, it does not provide information on which head node the service is running on.</span></span> <span data-ttu-id="7b2a6-189">Bu bilgileri görüntülemek için kullanın **ana** sayfanın üst kısmındaki bağlantı.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-189">To view this information, use the **Hosts** link at the top of the page.</span></span> <span data-ttu-id="7b2a6-190">Bu sayfa baş düğümler de dahil olmak üzere küme içindeki konaklar görüntüler.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-190">This page displays hosts within the cluster, including the head nodes.</span></span>

![ana bilgisayarların listesi](./media/hdinsight-high-availability-linux/hosts.png)

<span data-ttu-id="7b2a6-192">Baş düğümlerden birinde bağlantısını seçerek, o düğümde çalışan bileşenleri ve hizmetleri görüntüler.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-192">Selecting the link for one of the head nodes displays the services and components running on that node.</span></span>

![Bileşen Durumu](./media/hdinsight-high-availability-linux/nodeservices.png)

<span data-ttu-id="7b2a6-194">Ambari kullanarak daha fazla bilgi için bkz: [İzleyici ve Hdınsight Ambari Web kullanıcı arabirimini kullanarak yönetin](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="7b2a6-194">For more information on using Ambari, see [Monitor and manage HDInsight using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

### <a name="ambari-rest-api"></a><span data-ttu-id="7b2a6-195">Ambari REST API</span><span class="sxs-lookup"><span data-stu-id="7b2a6-195">Ambari REST API</span></span>

<span data-ttu-id="7b2a6-196">Ambari REST API Internet üzerinden kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-196">The Ambari REST API is available over the internet.</span></span> <span data-ttu-id="7b2a6-197">Hdınsight ortak ağ geçidi şu anda REST API barındırma baş düğümüne yönlendirme isteklerini işler.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-197">The HDInsight public gateway handles routing requests to the head node that is currently hosting the REST API.</span></span>

<span data-ttu-id="7b2a6-198">Ambari REST API aracılığıyla bir hizmetin durumunu denetlemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="7b2a6-198">You can use the following command to check the state of a service through the Ambari REST API:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICENAME?fields=ServiceInfo/state

* <span data-ttu-id="7b2a6-199">Değiştir **parola** HTTP kullanıcı (Yönetici) hesabı parolası ile.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-199">Replace **PASSWORD** with the HTTP user (admin) account password.</span></span>
* <span data-ttu-id="7b2a6-200">**CLUSTERNAME** değerini kümenin adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-200">Replace **CLUSTERNAME** with the name of the cluster.</span></span>
* <span data-ttu-id="7b2a6-201">Değiştir **SERVICENAME** durumunu denetlemek istediğiniz hizmetin adını.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-201">Replace **SERVICENAME** with the name of the service you want to check the status of.</span></span>

<span data-ttu-id="7b2a6-202">Örneğin, durumunu denetlemek için **HDFS** adlı bir kümede hizmet **mycluster**, bir parola ile **parola**, şu komutu kullanırsınız:</span><span class="sxs-lookup"><span data-stu-id="7b2a6-202">For example, to check the status of the **HDFS** service on a cluster named **mycluster**, with a password of **password**, you would use the following command:</span></span>

    curl -u admin:password https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state

<span data-ttu-id="7b2a6-203">Yanıt aşağıdaki JSON benzer:</span><span class="sxs-lookup"><span data-stu-id="7b2a6-203">The response is similar to the following JSON:</span></span>

    {
      "href" : "http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8080/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state",
      "ServiceInfo" : {
        "cluster_name" : "mycluster",
        "service_name" : "HDFS",
        "state" : "STARTED"
      }
    }

<span data-ttu-id="7b2a6-204">URL bize Hizmet şu anda adlı bir baş düğüm üzerinde çalışan söyler **hn0 CLUSTERNAME**.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-204">The URL tells us that the service is currently running on a head node named **hn0-CLUSTERNAME**.</span></span>

<span data-ttu-id="7b2a6-205">Durum Hizmet şu anda çalışıyor bize bildiren veya **başlatıldı**.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-205">The state tells us that the service is currently running, or **STARTED**.</span></span>

<span data-ttu-id="7b2a6-206">Hangi hizmetlerin kümeye yüklü bilmiyorsanız listesini almak için aşağıdaki komutu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7b2a6-206">If you do not know what services are installed on the cluster, you can use the following command to retrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services

<span data-ttu-id="7b2a6-207">Ambari REST API ile çalışma hakkında daha fazla bilgi için bkz: [izleme ve yönetme Ambari REST API kullanarak Hdınsight'ta](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="7b2a6-207">For more information on working with the Ambari REST API, see [Monitor and Manage HDInsight using the Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

#### <a name="service-components"></a><span data-ttu-id="7b2a6-208">Hizmet bileşenleri</span><span class="sxs-lookup"><span data-stu-id="7b2a6-208">Service components</span></span>

<span data-ttu-id="7b2a6-209">Hizmetleri, ayrı ayrı durumunu denetlemek istediğiniz bileşenleri içeriyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-209">Services may contain components that you wish to check the status of individually.</span></span> <span data-ttu-id="7b2a6-210">Örneğin, HDFS iş bileşeni içerir.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-210">For example, HDFS contains the NameNode component.</span></span> <span data-ttu-id="7b2a6-211">Bir bileşenin bilgilerini görüntülemek için komut olur:</span><span class="sxs-lookup"><span data-stu-id="7b2a6-211">To view information on a component, the command would be:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

<span data-ttu-id="7b2a6-212">Hangi bileşenlerin bir hizmeti tarafından sağlanan bilmiyorsanız listesini almak için aşağıdaki komutu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7b2a6-212">If you do not know what components are provided by a service, you can use the following command to retrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

## <a name="how-to-access-log-files-on-the-head-nodes"></a><span data-ttu-id="7b2a6-213">Baş düğümler günlük dosyalarına erişmek nasıl</span><span class="sxs-lookup"><span data-stu-id="7b2a6-213">How to access log files on the head nodes</span></span>

### <a name="ssh"></a><span data-ttu-id="7b2a6-214">SSH</span><span class="sxs-lookup"><span data-stu-id="7b2a6-214">SSH</span></span>

<span data-ttu-id="7b2a6-215">SSH aracılığıyla bir baş düğüm bağlıyken, günlük dosyalarını altında bulunabilir **/var/log**.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-215">While connected to a head node through SSH, log files can be found under **/var/log**.</span></span> <span data-ttu-id="7b2a6-216">Örneğin, **/var/log/hadoop-yarn/yarn** için YARN günlüklerini içerir.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-216">For example, **/var/log/hadoop-yarn/yarn** contain logs for YARN.</span></span>

<span data-ttu-id="7b2a6-217">Günlükleri, her ikisi de denetlemeniz gerekir böylece her baş düğüm benzersiz günlük girişlerini olabilir.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-217">Each head node can have unique log entries, so you should check the logs on both.</span></span>

### <a name="sftp"></a><span data-ttu-id="7b2a6-218">SFTP</span><span class="sxs-lookup"><span data-stu-id="7b2a6-218">SFTP</span></span>

<span data-ttu-id="7b2a6-219">Ayrıca SSH Dosya Aktarım Protokolü veya güvenli Dosya Aktarım Protokolü (SFTP) kullanarak baş düğümüne bağlanmak ve günlük dosyaları doğrudan indirin.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-219">You can also connect to the head node using the SSH File Transfer Protocol or Secure File Transfer Protocol (SFTP), and download the log files directly.</span></span>

<span data-ttu-id="7b2a6-220">Benzer şekilde bir SSH istemcisi kullanarak, ne zaman kümeye bağlanarak SSH kullanıcı hesabı adını ve kümenin SSH adresi sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-220">Similar to using an SSH client, when connecting to the cluster you must provide the SSH user account name and the SSH address of the cluster.</span></span> <span data-ttu-id="7b2a6-221">Örneğin, `sftp username@mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-221">For example, `sftp username@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="7b2a6-222">İstendiğinde hesabı için parola sağlayın ya da bir ortak anahtar kullanarak sağlayın `-i` parametresi.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-222">Provide the password for the account when prompted, or provide a public key using the `-i` parameter.</span></span>

<span data-ttu-id="7b2a6-223">Bağlantı kurulduktan sonra size sunulan bir `sftp>` istemi.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-223">Once connected, you are presented with a `sftp>` prompt.</span></span> <span data-ttu-id="7b2a6-224">Bu isteminde dizinleri değiştirebilir, dosyaları yükleme ve indirme.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-224">From this prompt, you can change directories, upload, and download files.</span></span> <span data-ttu-id="7b2a6-225">Örneğin, aşağıdaki komutları dizinleri değiştirme **/var/log/hadoop/hdfs** dizin ve dizindeki tüm dosyaları sonra yükleme.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-225">For example, the following commands change directories to the **/var/log/hadoop/hdfs** directory and then download all files in the directory.</span></span>

    cd /var/log/hadoop/hdfs
    get *

<span data-ttu-id="7b2a6-226">Kullanılabilir komutlar listesi için girin `help` adresindeki `sftp>` istemi.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-226">For a list of available commands, enter `help` at the `sftp>` prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="7b2a6-227">Ayrıca, dosya sistemi SFTP kullanarak bağlandığında görselleştirmek izin grafik arabirimi vardır.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-227">There are also graphical interfaces that allow you to visualize the file system when connected using SFTP.</span></span> <span data-ttu-id="7b2a6-228">Örneğin, [MobaXTerm](http://mobaxterm.mobatek.net/) Windows Explorer için benzer bir arabirim kullanarak dosya sistemi göz atmanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-228">For example, [MobaXTerm](http://mobaxterm.mobatek.net/) allows you to browse the file system using an interface similar to Windows Explorer.</span></span>

### <a name="ambari"></a><span data-ttu-id="7b2a6-229">Ambari</span><span class="sxs-lookup"><span data-stu-id="7b2a6-229">Ambari</span></span>

> [!NOTE]
> <span data-ttu-id="7b2a6-230">Ambari kullanarak günlük dosyalarına erişmek için bir SSH tüneli kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-230">To access log files using Ambari, you must use an SSH tunnel.</span></span> <span data-ttu-id="7b2a6-231">Tek tek Hizmetleri için web arabirimleri, Internet üzerinde herkese açık şekilde sunulmaz.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-231">The web interfaces for the individual services are not exposed publicly on the Internet.</span></span> <span data-ttu-id="7b2a6-232">SSH tüneli kullanma hakkında daha fazla bilgi için bkz: [kullanım SSH tünel](hdinsight-linux-ambari-ssh-tunnel.md) belge.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-232">For information on using an SSH tunnel, see the [Use SSH Tunneling](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="7b2a6-233">Ambari Web kullanıcı arabirimini (örneğin, YARN için) günlüklerini görüntülemek istediğiniz hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-233">From the Ambari Web UI, select the service you wish to view logs for (for example, YARN).</span></span> <span data-ttu-id="7b2a6-234">Ardından **hızlı bağlantılar** hangi baş düğüm için günlükleri görüntülemek için seçin.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-234">Then use **Quick Links** to select which head node to view the logs for.</span></span>

![Günlükleri görüntülemek için hızlı bağlantıları kullanma](./media/hdinsight-high-availability-linux/viewlogs.png)

## <a name="how-to-configure-the-node-size"></a><span data-ttu-id="7b2a6-236">Düğüm boyutu yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7b2a6-236">How to configure the node size</span></span>

<span data-ttu-id="7b2a6-237">Bir düğümün boyutu, küme oluşturma sırasında yalnızca seçilebilir.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-237">The size of a node can only be selected during cluster creation.</span></span> <span data-ttu-id="7b2a6-238">Hdınsight üzerinde farklı VM boyutlarının listesini bulabilirsiniz [Hdınsight fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="7b2a6-238">You can find a list of the different VM sizes available for HDInsight on the [HDInsight pricing page](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="7b2a6-239">Bir küme oluştururken, düğümlerin boyutu belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-239">When creating a cluster, you can specify the size of the nodes.</span></span> <span data-ttu-id="7b2a6-240">Aşağıdaki bilgileri boyutu kullanarak belirleme konusunda rehberlik sağlar [Azure portal][preview-portal], [Azure PowerShell][azure-powershell]ve [Azure CLI][azure-cli]:</span><span class="sxs-lookup"><span data-stu-id="7b2a6-240">The following information provides guidance on how to specify the size using the [Azure portal][preview-portal], [Azure PowerShell][azure-powershell], and the [Azure CLI][azure-cli]:</span></span>

* <span data-ttu-id="7b2a6-241">**Azure portal**: bir küme oluştururken, küme tarafından kullanılan düğümlerin boyutu ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="7b2a6-241">**Azure portal**: When creating a cluster, you can set the size of the nodes used by the cluster:</span></span>

    ![Düğüm boyutu seçimi ile küme oluşturma Sihirbazı'nın resmi](./media/hdinsight-high-availability-linux/headnodesize.png)

* <span data-ttu-id="7b2a6-243">**Azure CLI**: kullanırken `azure hdinsight cluster create` komutunu kullanarak head, çalışan ve ZooKeeper düğümleri boyutunu ayarlayabilirsiniz `--headNodeSize`, `--workerNodeSize`, ve `--zookeeperNodeSize` parametreleri.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-243">**Azure CLI**: When using the `azure hdinsight cluster create` command, you can set the size of the head, worker, and ZooKeeper nodes by using the `--headNodeSize`, `--workerNodeSize`, and `--zookeeperNodeSize` parameters.</span></span>

* <span data-ttu-id="7b2a6-244">**Azure PowerShell**: kullanırken `New-AzureRmHDInsightCluster` cmdlet'ini kullanarak head, çalışan ve ZooKeeper düğümleri boyutunu ayarlayabilirsiniz `-HeadNodeVMSize`, `-WorkerNodeSize`, ve `-ZookeeperNodeSize` parametreleri.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-244">**Azure PowerShell**: When using the `New-AzureRmHDInsightCluster` cmdlet, you can set the size of the head, worker, and ZooKeeper nodes by using the `-HeadNodeVMSize`, `-WorkerNodeSize`, and `-ZookeeperNodeSize` parameters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b2a6-245">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7b2a6-245">Next steps</span></span>

<span data-ttu-id="7b2a6-246">Bu belgede belirtilen noktalar hakkında daha fazla bilgi için aşağıdaki bağlantıları kullanın.</span><span class="sxs-lookup"><span data-stu-id="7b2a6-246">Use the following links to learn more about things mentioned in this document.</span></span>

* [<span data-ttu-id="7b2a6-247">Ambari REST başvurusu</span><span class="sxs-lookup"><span data-stu-id="7b2a6-247">Ambari REST Reference</span></span>](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)
* [<span data-ttu-id="7b2a6-248">Azure CLI'yi yükleme ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7b2a6-248">Install and configure the Azure CLI</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="7b2a6-249">Azure PowerShell'i yükleme ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="7b2a6-249">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="7b2a6-250">Ambari kullanarak Hdınsight yönetme</span><span class="sxs-lookup"><span data-stu-id="7b2a6-250">Manage HDInsight using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)
* [<span data-ttu-id="7b2a6-251">Linux tabanlı Hdınsight kümeleri hazırlama</span><span class="sxs-lookup"><span data-stu-id="7b2a6-251">Provision Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)

[preview-portal]: https://portal.azure.com/
[azure-powershell]: /powershell/azureps-cmdlets-docs
[azure-cli]: ../cli-install-nodejs.md
