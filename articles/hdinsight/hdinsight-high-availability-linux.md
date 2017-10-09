---
title: "Hadoop - Azure Hdınsight için aaaHigh kullanılabilirlik | Microsoft Docs"
description: "Nasıl Hdınsight kümeleri güvenilirlik ve kullanılabilirlik ek bir baş düğüm kullanarak iyileştirmek öğrenin. Tooindividually bağlanmak tooeach baş düğüm SSH kullanarak nasıl bu Ambari ve Hive gibi Hadoop hizmetleri nasıl etkilediğini de öğrenin."
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
ms.openlocfilehash: 9ff62afe6b63b241cb984225233157219f8d7411
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-reliability-of-hadoop-clusters-in-hdinsight"></a><span data-ttu-id="274ea-105">HDInsight'ta Hadoop kümelerinin kullanılabilirliği ve güvenilirliği</span><span class="sxs-lookup"><span data-stu-id="274ea-105">Availability and reliability of Hadoop clusters in HDInsight</span></span>

<span data-ttu-id="274ea-106">Hdınsight kümeleri iki baş düğümler tooincrease hello kullanılabilirliği ve güvenilirliği Hadoop Hizmetleri ve çalışan işlerin sağlar.</span><span class="sxs-lookup"><span data-stu-id="274ea-106">HDInsight clusters provide two head nodes tooincrease hello availability and reliability of Hadoop services and jobs running.</span></span>

<span data-ttu-id="274ea-107">Hadoop bir kümede birden çok düğüm arasında Hizmetleri ve veri çoğaltma tarafından yüksek kullanılabilirlik ve güvenilirlik elde eder.</span><span class="sxs-lookup"><span data-stu-id="274ea-107">Hadoop achieves high availability and reliability by replicating services and data across multiple nodes in a cluster.</span></span> <span data-ttu-id="274ea-108">Ancak standart dağıtımları hadoop genellikle yalnızca tek bir baş düğüm vardır.</span><span class="sxs-lookup"><span data-stu-id="274ea-108">However standard distributions of Hadoop typically have only a single head node.</span></span> <span data-ttu-id="274ea-109">Merhaba tek baş düğümü herhangi kesinti hello küme toostop çalışma neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="274ea-109">Any outage of hello single head node can cause hello cluster toostop working.</span></span> <span data-ttu-id="274ea-110">Hdınsight iki headnodes tooimprove Hadoop'ın kullanılabilirliği ve güvenilirliği sağlar.</span><span class="sxs-lookup"><span data-stu-id="274ea-110">HDInsight provides two headnodes tooimprove Hadoop's availability and reliability.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="274ea-111">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="274ea-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="274ea-112">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="274ea-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="availability-and-reliability-of-nodes"></a><span data-ttu-id="274ea-113">Kullanılabilirliği ve güvenilirliği düğümlerinin</span><span class="sxs-lookup"><span data-stu-id="274ea-113">Availability and reliability of nodes</span></span>

<span data-ttu-id="274ea-114">Hdınsight kümesi düğümünde, Azure sanal makineleri kullanarak uygulanır.</span><span class="sxs-lookup"><span data-stu-id="274ea-114">Nodes in an HDInsight cluster are implemented using Azure Virtual Machines.</span></span> <span data-ttu-id="274ea-115">Merhaba aşağıdaki bölümlerde Hdınsight ile kullanılan hello tek tek düğüm türleri açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="274ea-115">hello following sections discuss hello individual node types used with HDInsight.</span></span> 

> [!NOTE]
> <span data-ttu-id="274ea-116">Tüm düğüm türleri için bir küme türü kullanılır.</span><span class="sxs-lookup"><span data-stu-id="274ea-116">Not all node types are used for a cluster type.</span></span> <span data-ttu-id="274ea-117">Örneğin, Hadoop küme türü hiçbir Nimbus düğümü yok.</span><span class="sxs-lookup"><span data-stu-id="274ea-117">For example, a Hadoop cluster type does not have any Nimbus nodes.</span></span> <span data-ttu-id="274ea-118">Hdınsight küme türleri tarafından kullanılan düğümleri hakkında daha fazla bilgi için hello hello küme türleri bölümüne bakın [Hdınsight oluşturma Linux tabanlı Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) belge.</span><span class="sxs-lookup"><span data-stu-id="274ea-118">For more information on nodes used by HDInsight cluster types, see hello Cluster types section of hello [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) document.</span></span>

### <a name="head-nodes"></a><span data-ttu-id="274ea-119">Baş düğümler</span><span class="sxs-lookup"><span data-stu-id="274ea-119">Head nodes</span></span>

<span data-ttu-id="274ea-120">Hadoop Hizmetleri tooensure yüksek kullanılabilirlik, Hdınsight iki baş düğümler sağlar.</span><span class="sxs-lookup"><span data-stu-id="274ea-120">tooensure high availability of Hadoop services, HDInsight provides two head nodes.</span></span> <span data-ttu-id="274ea-121">Her iki baş düğümler aynı anda etkin ve hello Hdınsight kümesi içinde çalışır durumda.</span><span class="sxs-lookup"><span data-stu-id="274ea-121">Both head nodes are active and running within hello HDInsight cluster simultaneously.</span></span> <span data-ttu-id="274ea-122">HDFS veya YARN gibi bazı hizmetler, herhangi bir anda yalnızca bir baş düğüm üzerinde ' active'.</span><span class="sxs-lookup"><span data-stu-id="274ea-122">Some services, such as HDFS or YARN, are only 'active' on one head node at any given time.</span></span> <span data-ttu-id="274ea-123">HiveServer2 veya Hive meta depo gibi başka hizmetleri hello hem baş düğüm üzerinde etkin olan aynı anda.</span><span class="sxs-lookup"><span data-stu-id="274ea-123">Other services such as HiveServer2 or Hive MetaStore are active on both head nodes at hello same time.</span></span>

<span data-ttu-id="274ea-124">Baş düğümler (ve diğer düğümlere hdınsight'ta) hello hostname hello düğümün bir parçası olarak sayısal bir değere sahip.</span><span class="sxs-lookup"><span data-stu-id="274ea-124">Head nodes (and other nodes in HDInsight) have a numeric value as part of hello hostname of hello node.</span></span> <span data-ttu-id="274ea-125">Örneğin, `hn0-CLUSTERNAME` veya `hn4-CLUSTERNAME`.</span><span class="sxs-lookup"><span data-stu-id="274ea-125">For example, `hn0-CLUSTERNAME` or `hn4-CLUSTERNAME`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="274ea-126">Merhaba sayısal değer, bir düğüm birincil veya ikincil ile ilişkilendirmeyin.</span><span class="sxs-lookup"><span data-stu-id="274ea-126">Do not associate hello numeric value with whether a node is primary or secondary.</span></span> <span data-ttu-id="274ea-127">Merhaba sayısal değer yalnızca mevcut tooprovide her düğüm için benzersiz bir ad değil.</span><span class="sxs-lookup"><span data-stu-id="274ea-127">hello numeric value is only present tooprovide a unique name for each node.</span></span>

### <a name="nimbus-nodes"></a><span data-ttu-id="274ea-128">Nimbus Düğümleri</span><span class="sxs-lookup"><span data-stu-id="274ea-128">Nimbus Nodes</span></span>

<span data-ttu-id="274ea-129">Nimbus düğümü Storm kümeleri ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="274ea-129">Nimbus nodes are available with Storm clusters.</span></span> <span data-ttu-id="274ea-130">Merhaba Nimbus düğümü benzer işlevselliği toohello Hadoop Jobtracker'a dağıtma ve çalışan düğümleri arasında işleme izleme sağlar.</span><span class="sxs-lookup"><span data-stu-id="274ea-130">hello Nimbus nodes provide similar functionality toohello Hadoop JobTracker by distributing and monitoring processing across worker nodes.</span></span> <span data-ttu-id="274ea-131">Hdınsight iki Nimbus düğümü Storm kümeleri için sağlar.</span><span class="sxs-lookup"><span data-stu-id="274ea-131">HDInsight provides two Nimbus nodes for Storm clusters</span></span>

### <a name="zookeeper-nodes"></a><span data-ttu-id="274ea-132">Zookeeper düğümleri</span><span class="sxs-lookup"><span data-stu-id="274ea-132">Zookeeper nodes</span></span>

<span data-ttu-id="274ea-133">[ZooKeeper](http://zookeeper.apache.org/) düğümleri öncü seçim baş düğümler üzerinde ana Hizmetleri için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="274ea-133">[ZooKeeper](http://zookeeper.apache.org/) nodes are used for leader election of master services on head nodes.</span></span> <span data-ttu-id="274ea-134">Ayrıca hizmet ana üzerinde etkin olan baş düğümü Hizmetleri, veri (çalışan) düğümlerini ve ağ geçitleri bilmeniz kullanılan tooinsure oldukları.</span><span class="sxs-lookup"><span data-stu-id="274ea-134">They are also used tooinsure that services, data (worker) nodes, and gateways know which head node a master service is active on.</span></span> <span data-ttu-id="274ea-135">Varsayılan olarak, Hdınsight üç ZooKeeper düğümleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="274ea-135">By default, HDInsight provides three ZooKeeper nodes.</span></span>

### <a name="worker-nodes"></a><span data-ttu-id="274ea-136">Çalışan düğümü</span><span class="sxs-lookup"><span data-stu-id="274ea-136">Worker nodes</span></span>

<span data-ttu-id="274ea-137">Bir işi gönderilen toohello küme olduğunda çalışan düğümleri hello gerçek veri çözümlemesi gerçekleştirme.</span><span class="sxs-lookup"><span data-stu-id="274ea-137">Worker nodes perform hello actual data analysis when a job is submitted toohello cluster.</span></span> <span data-ttu-id="274ea-138">Bir alt düğüm başarısız olursa, onu gerçekleştiren hello gönderilen tooanother çalışan düğüme bir görevdir.</span><span class="sxs-lookup"><span data-stu-id="274ea-138">If a worker node fails, hello task that it was performing is submitted tooanother worker node.</span></span> <span data-ttu-id="274ea-139">Varsayılan olarak, dört alt düğüm Hdınsight oluşturur.</span><span class="sxs-lookup"><span data-stu-id="274ea-139">By default, HDInsight creates four worker nodes.</span></span> <span data-ttu-id="274ea-140">Hem sırasında hem de Küme oluşturulduktan sonra bu sayı toosuit gereksinimlerinizi değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="274ea-140">You can change this number toosuit your needs both during and after cluster creation.</span></span>

### <a name="edge-node"></a><span data-ttu-id="274ea-141">Kenar düğümüne</span><span class="sxs-lookup"><span data-stu-id="274ea-141">Edge node</span></span>

<span data-ttu-id="274ea-142">Bir kenar düğümüne, veri analizi hello kümedeki etkin olarak katılmıyor.</span><span class="sxs-lookup"><span data-stu-id="274ea-142">An edge node does not actively participate in data analysis within hello cluster.</span></span> <span data-ttu-id="274ea-143">Hadoop ile çalışırken, geliştiriciler veya veri bilimcilerine tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="274ea-143">It is used by developers or data scientists when working with Hadoop.</span></span> <span data-ttu-id="274ea-144">Hello kenar düğümü yaşamlarını hello aynı Azure sanal ağ hello kümedeki diğer düğümlere hello ve tüm diğer düğümlere doğrudan erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="274ea-144">hello edge node lives in hello same Azure Virtual Network as hello other nodes in hello cluster, and can directly access all other nodes.</span></span> <span data-ttu-id="274ea-145">Merhaba kenar düğümüne kritik Hadoop Hizmetleri veya analiz işleri çıktığınızda kaynakları bırakmadan kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="274ea-145">hello edge node can be used without taking resources away from critical Hadoop services or analysis jobs.</span></span>

<span data-ttu-id="274ea-146">Şu anda, hdınsight'ta R Server varsayılan olarak bir kenar düğümüne sağlayan hello yalnızca küme türü budur.</span><span class="sxs-lookup"><span data-stu-id="274ea-146">Currently, R Server on HDInsight is hello only cluster type that provides an edge node by default.</span></span> <span data-ttu-id="274ea-147">Merhaba kenar düğümüne hdınsight'ta R Server için kullanılan yerel olarak hello düğümünde toohello küme dağıtılmış işlem için göndermeden önce test R kodu.</span><span class="sxs-lookup"><span data-stu-id="274ea-147">For R Server on HDInsight, hello edge node is used test R code locally on hello node before submitting it toohello cluster for distributed processing.</span></span>

<span data-ttu-id="274ea-148">Merhaba küme türleri R Server dışındaki bir edge düğümünü kullanarak hakkında daha fazla bilgi için bkz [Hdınsight'ta kenar düğümünü kullanmak](hdinsight-apps-use-edge-node.md) belge.</span><span class="sxs-lookup"><span data-stu-id="274ea-148">For information on using an edge node with cluster types other than R Server, see hello [Use edge nodes in HDInsight](hdinsight-apps-use-edge-node.md) document.</span></span>

## <a name="accessing-hello-nodes"></a><span data-ttu-id="274ea-149">Merhaba düğümlere erişme</span><span class="sxs-lookup"><span data-stu-id="274ea-149">Accessing hello nodes</span></span>

<span data-ttu-id="274ea-150">Merhaba üzerinden erişim toohello küme Internet ortak ağ geçidi üzerinden sağlanır.</span><span class="sxs-lookup"><span data-stu-id="274ea-150">Access toohello cluster over hello internet is provided through a public gateway.</span></span> <span data-ttu-id="274ea-151">Erişim sınırlı tooconnecting toohello baş düğümler ve (varsa,) kenar düğümüne hello.</span><span class="sxs-lookup"><span data-stu-id="274ea-151">Access is limited tooconnecting toohello head nodes and (if one exists) hello edge node.</span></span> <span data-ttu-id="274ea-152">Erişim tooservices Hello baş düğümler üzerinde çalışan birden çok baş düğümler sağlayarak parametreden etkilenir değil.</span><span class="sxs-lookup"><span data-stu-id="274ea-152">Access tooservices running on hello head nodes is not effected by having multiple head nodes.</span></span> <span data-ttu-id="274ea-153">İstenen hizmet hello barındıran hello ortak ağ geçidi yollarını istekleri toohello baş düğüm.</span><span class="sxs-lookup"><span data-stu-id="274ea-153">hello public gateway routes requests toohello head node that hosts hello requested service.</span></span> <span data-ttu-id="274ea-154">Örneğin, Ambari şu anda hello ikincil baş düğüm üzerinde barındırılıyorsa hello ağ geçidi Ambari toothat düğümü için gelen istekleri yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="274ea-154">For example, if Ambari is currently hosted on hello secondary head node, hello gateway routes incoming requests for Ambari toothat node.</span></span>

<span data-ttu-id="274ea-155">Merhaba ortak ağ geçidi üzerinden erişim sınırlı tooport 443 (HTTPS), 22 ve 23 ' dir.</span><span class="sxs-lookup"><span data-stu-id="274ea-155">Access over hello public gateway is limited tooport 443 (HTTPS), 22, and 23.</span></span>

* <span data-ttu-id="274ea-156">Bağlantı noktası __443__ kullanılan tooaccess olan Ambari ve diğer web kullanıcı Arabirimi veya hello baş düğümler üzerinde barındırılan REST API'leri.</span><span class="sxs-lookup"><span data-stu-id="274ea-156">Port __443__ is used tooaccess Ambari and other web UI or REST APIs hosted on hello head nodes.</span></span>

* <span data-ttu-id="274ea-157">Bağlantı noktası __22__ kullanılan tooaccess hello birincil baş düğüm veya kenar düğümüne SSH ile.</span><span class="sxs-lookup"><span data-stu-id="274ea-157">Port __22__ is used tooaccess hello primary head node or edge node with SSH.</span></span>

* <span data-ttu-id="274ea-158">Bağlantı noktası __23__ kullanılan tooaccess hello ikincil baş düğüm SSH.</span><span class="sxs-lookup"><span data-stu-id="274ea-158">Port __23__ is used tooaccess hello secondary head node with SSH.</span></span> <span data-ttu-id="274ea-159">Örneğin, `ssh username@mycluster-ssh.azurehdinsight.net` toohello adlı hello kümesinin birincil baş düğümüne bağlanan **mycluster**.</span><span class="sxs-lookup"><span data-stu-id="274ea-159">For example, `ssh username@mycluster-ssh.azurehdinsight.net` connects toohello primary head node of hello cluster named **mycluster**.</span></span>

<span data-ttu-id="274ea-160">Merhaba SSH kullanma hakkında daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md) belge.</span><span class="sxs-lookup"><span data-stu-id="274ea-160">For more information on using SSH, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

### <a name="internal-fully-qualified-domain-names-fqdn"></a><span data-ttu-id="274ea-161">İç tam etki alanı adları (FQDN)</span><span class="sxs-lookup"><span data-stu-id="274ea-161">Internal fully qualified domain names (FQDN)</span></span>

<span data-ttu-id="274ea-162">Bir Hdınsight küme düğümlerinde bir iç IP adresi ve yalnızca hello kümeden erişilebilir FQDN vardır.</span><span class="sxs-lookup"><span data-stu-id="274ea-162">Nodes in an HDInsight cluster have an internal IP address and FQDN that can only be accessed from hello cluster.</span></span> <span data-ttu-id="274ea-163">Merhaba iç FQDN veya IP adresini kullanarak hello küme hizmetlerini erişirken Ambari, tooverify hello IP veya FQDN toouse hello hizmet erişirken kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="274ea-163">When accessing services on hello cluster using hello internal FQDN or IP address, you should use Ambari tooverify hello IP or FQDN toouse when accessing hello service.</span></span>

<span data-ttu-id="274ea-164">Örneğin, hizmet yalnızca bir baş düğüm üzerinde çalıştırmak Oozie hello ve hello kullanarak `oozie` bir SSH oturumu komuttan hello URL toohello hizmetinin gerektirir.</span><span class="sxs-lookup"><span data-stu-id="274ea-164">For example, hello Oozie service can only run on one head node, and using hello `oozie` command from an SSH session requires hello URL toohello service.</span></span> <span data-ttu-id="274ea-165">Bu URL, komutu aşağıdaki hello kullanarak Ambari alınabilir:</span><span class="sxs-lookup"><span data-stu-id="274ea-165">This URL can be retrieved from Ambari by using hello following command:</span></span>

    curl -u admin:PASSWORD "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations?type=oozie-site&tag=TOPOLOGY_RESOLVED" | grep oozie.base.url

<span data-ttu-id="274ea-166">Bu komut bir değer benzer toohello hello İç URL toouse hello ile içeren komutu aşağıdaki döndürür `oozie` komutu:</span><span class="sxs-lookup"><span data-stu-id="274ea-166">This command returns a value similar toohello following command, which contains hello internal URL toouse with hello `oozie` command:</span></span>

    "oozie.base.url": "http://hn0-CLUSTERNAME-randomcharacters.cx.internal.cloudapp.net:11000/oozie"

<span data-ttu-id="274ea-167">Merhaba Ambari REST API ile çalışma hakkında daha fazla bilgi için bkz: [izleme ve yönetme hello Ambari REST API kullanarak Hdınsight'ta](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="274ea-167">For more information on working with hello Ambari REST API, see [Monitor and Manage HDInsight using hello Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

### <a name="accessing-other-node-types"></a><span data-ttu-id="274ea-168">Diğer düğüm türleri erişme</span><span class="sxs-lookup"><span data-stu-id="274ea-168">Accessing other node types</span></span>

<span data-ttu-id="274ea-169">Değil erişilebilir üzerinden hello doğrudan internet yöntemler aşağıdaki hello kullanarak olan toonodes bağlanabilir:</span><span class="sxs-lookup"><span data-stu-id="274ea-169">You can connect toonodes that are not directly accessible over hello internet by using hello following methods:</span></span>

* <span data-ttu-id="274ea-170">**SSH**: tooa baş düğüm SSH, kullanarak bağlandıktan sonra hello baş düğüm tooconnect tooother düğümlerinden hello kümedeki SSH kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="274ea-170">**SSH**: Once connected tooa head node using SSH, you can then use SSH from hello head node tooconnect tooother nodes in hello cluster.</span></span> <span data-ttu-id="274ea-171">Daha fazla bilgi için bkz: Merhaba [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md) belge.</span><span class="sxs-lookup"><span data-stu-id="274ea-171">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

* <span data-ttu-id="274ea-172">**SSH tüneli**: bir web hizmeti barındırılan tooaccess gerekiyorsa değil hello düğümlerinden biri toohello sunulan Internet, SSH tüneli kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="274ea-172">**SSH Tunnel**: If you need tooaccess a web service hosted on one of hello nodes that is not exposed toohello internet, you must use an SSH tunnel.</span></span> <span data-ttu-id="274ea-173">Daha fazla bilgi için bkz: Merhaba [Hdınsight ile SSH tüneli kullanma](hdinsight-linux-ambari-ssh-tunnel.md) belge.</span><span class="sxs-lookup"><span data-stu-id="274ea-173">For more information, see hello [Use an SSH tunnel with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

* <span data-ttu-id="274ea-174">**Azure sanal ağı**: küme herhangi bir kaynak bir Azure sanal ağının parçası olduğundan, Hdınsight aynı Merhaba, sanal ağ hello kümedeki tüm düğümlere doğrudan erişebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="274ea-174">**Azure Virtual Network**: If your HDInsight cluster is part of an Azure Virtual Network, any resource on hello same Virtual Network can directly access all nodes in hello cluster.</span></span> <span data-ttu-id="274ea-175">Daha fazla bilgi için bkz: Merhaba [Azure sanal ağını kullanarak Hdınsight genişletmek](hdinsight-extend-hadoop-virtual-network.md) belge.</span><span class="sxs-lookup"><span data-stu-id="274ea-175">For more information, see hello [Extend HDInsight using Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

## <a name="how-toocheck-on-a-service-status"></a><span data-ttu-id="274ea-176">Nasıl toocheck hizmet durumu hakkında</span><span class="sxs-lookup"><span data-stu-id="274ea-176">How toocheck on a service status</span></span>

<span data-ttu-id="274ea-177">toocheck hello durum hello baş düğümler üzerinde çalışan hizmetleri veya Ambari REST API hello hello Ambari Web kullanıcı arabirimini kullanın.</span><span class="sxs-lookup"><span data-stu-id="274ea-177">toocheck hello status of services that run on hello head nodes, use hello Ambari Web UI or hello Ambari REST API.</span></span>

### <a name="ambari-web-ui"></a><span data-ttu-id="274ea-178">Ambari Web kullanıcı Arabirimi</span><span class="sxs-lookup"><span data-stu-id="274ea-178">Ambari Web UI</span></span>

<span data-ttu-id="274ea-179">Merhaba Ambari Web kullanıcı arabirimini https://CLUSTERNAME.azurehdinsight.net görülebilir.</span><span class="sxs-lookup"><span data-stu-id="274ea-179">hello Ambari Web UI is viewable at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="274ea-180">Değiştir **CLUSTERNAME** kümenizin hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="274ea-180">Replace **CLUSTERNAME** with hello name of your cluster.</span></span> <span data-ttu-id="274ea-181">İstenirse, kümeniz için hello HTTP kullanıcı kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="274ea-181">If prompted, enter hello HTTP user credentials for your cluster.</span></span> <span data-ttu-id="274ea-182">Merhaba varsayılan HTTP kullanıcı adı **yönetici** ve hello parola hello kümesi oluştururken girdiğiniz hello parola.</span><span class="sxs-lookup"><span data-stu-id="274ea-182">hello default HTTP user name is **admin** and hello password is hello password you entered when creating hello cluster.</span></span>

<span data-ttu-id="274ea-183">Hello Ambari sayfasında geldiğinde, yüklü hello Hizmetleri hello sayfa hello sol tarafında listelenir.</span><span class="sxs-lookup"><span data-stu-id="274ea-183">When you arrive on hello Ambari page, hello installed services are listed on hello left of hello page.</span></span>

![Yüklü hizmetleri](./media/hdinsight-high-availability-linux/services.png)

<span data-ttu-id="274ea-185">Sonraki tooa hizmet tooindicate durumu görünebilir simgeleri bir dizi vardır.</span><span class="sxs-lookup"><span data-stu-id="274ea-185">There are a series of icons that may appear next tooa service tooindicate status.</span></span> <span data-ttu-id="274ea-186">İlgili tüm uyarıları tooa hizmet hello kullanarak görüntülenebilir **uyarıları** hello sayfanın üst kısmındaki hello bağlantı.</span><span class="sxs-lookup"><span data-stu-id="274ea-186">Any alerts related tooa service can be viewed using hello **Alerts** link at hello top of hello page.</span></span> <span data-ttu-id="274ea-187">Daha fazla bilgi her hizmet tooview seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="274ea-187">You can select each service tooview more information on it.</span></span>

<span data-ttu-id="274ea-188">Merhaba hizmet sayfası hello durumu ve her hizmetin yapılandırma hakkında bilgi sağlarken, baş düğüm hello hizmeti çalıştığı hakkında bilgi sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="274ea-188">While hello service page provides information on hello status and configuration of each service, it does not provide information on which head node hello service is running on.</span></span> <span data-ttu-id="274ea-189">tooview bu bilgiler, kullanım hello **ana** hello sayfanın üst kısmındaki hello bağlantı.</span><span class="sxs-lookup"><span data-stu-id="274ea-189">tooview this information, use hello **Hosts** link at hello top of hello page.</span></span> <span data-ttu-id="274ea-190">Bu sayfa hello baş düğümler de dahil olmak üzere hello kümedeki konaklar görüntüler.</span><span class="sxs-lookup"><span data-stu-id="274ea-190">This page displays hosts within hello cluster, including hello head nodes.</span></span>

![ana bilgisayarların listesi](./media/hdinsight-high-availability-linux/hosts.png)

<span data-ttu-id="274ea-192">Hello baş düğümlerden seçme hello bağlantısını hello Hizmetleri ve bileşenleri bu düğümde çalışan görüntüler.</span><span class="sxs-lookup"><span data-stu-id="274ea-192">Selecting hello link for one of hello head nodes displays hello services and components running on that node.</span></span>

![Bileşen Durumu](./media/hdinsight-high-availability-linux/nodeservices.png)

<span data-ttu-id="274ea-194">Ambari kullanarak daha fazla bilgi için bkz: [İzleyici ve hello Ambari Web kullanıcı arabirimini kullanarak Hdınsight yönetmek](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="274ea-194">For more information on using Ambari, see [Monitor and manage HDInsight using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

### <a name="ambari-rest-api"></a><span data-ttu-id="274ea-195">Ambari REST API</span><span class="sxs-lookup"><span data-stu-id="274ea-195">Ambari REST API</span></span>

<span data-ttu-id="274ea-196">Merhaba Ambari REST API hello kullanılabilir Internet.</span><span class="sxs-lookup"><span data-stu-id="274ea-196">hello Ambari REST API is available over hello internet.</span></span> <span data-ttu-id="274ea-197">Merhaba Hdınsight ortak ağ geçidi şu anda hello REST API barındıran yönlendirme istekleri toohello baş düğümü işler.</span><span class="sxs-lookup"><span data-stu-id="274ea-197">hello HDInsight public gateway handles routing requests toohello head node that is currently hosting hello REST API.</span></span>

<span data-ttu-id="274ea-198">Komut toocheck hello hello Ambari REST API aracılığıyla bir hizmetin durumunu izleyen hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="274ea-198">You can use hello following command toocheck hello state of a service through hello Ambari REST API:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICENAME?fields=ServiceInfo/state

* <span data-ttu-id="274ea-199">Değiştir **parola** hello HTTP kullanıcı (Yönetici) hesap parolası ile.</span><span class="sxs-lookup"><span data-stu-id="274ea-199">Replace **PASSWORD** with hello HTTP user (admin) account password.</span></span>
* <span data-ttu-id="274ea-200">Değiştir **CLUSTERNAME** hello küme hello adı.</span><span class="sxs-lookup"><span data-stu-id="274ea-200">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>
* <span data-ttu-id="274ea-201">Değiştir **SERVICENAME** hello hello hizmet adıyla toocheck hello durumunu istiyor.</span><span class="sxs-lookup"><span data-stu-id="274ea-201">Replace **SERVICENAME** with hello name of hello service you want toocheck hello status of.</span></span>

<span data-ttu-id="274ea-202">Örneğin, toocheck hello durumunu hello **HDFS** adlı bir kümede hizmet **mycluster**, bir parola ile **parola**, komutu aşağıdaki hello kullanırsınız:</span><span class="sxs-lookup"><span data-stu-id="274ea-202">For example, toocheck hello status of hello **HDFS** service on a cluster named **mycluster**, with a password of **password**, you would use hello following command:</span></span>

    curl -u admin:password https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state

<span data-ttu-id="274ea-203">Merhaba yanıt benzer toohello JSON aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="274ea-203">hello response is similar toohello following JSON:</span></span>

    {
      "href" : "http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8080/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state",
      "ServiceInfo" : {
        "cluster_name" : "mycluster",
        "service_name" : "HDFS",
        "state" : "STARTED"
      }
    }

<span data-ttu-id="274ea-204">Merhaba URL bize hello Hizmet şu anda adlı bir baş düğüm üzerinde çalışan söyler **hn0 CLUSTERNAME**.</span><span class="sxs-lookup"><span data-stu-id="274ea-204">hello URL tells us that hello service is currently running on a head node named **hn0-CLUSTERNAME**.</span></span>

<span data-ttu-id="274ea-205">Merhaba durumu bize hello Hizmet şu anda çalışıyor söyler veya **başlatıldı**.</span><span class="sxs-lookup"><span data-stu-id="274ea-205">hello state tells us that hello service is currently running, or **STARTED**.</span></span>

<span data-ttu-id="274ea-206">Hangi hizmetlerin hello kümeye yüklü bilmiyorsanız komutu tooretrieve listesini aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="274ea-206">If you do not know what services are installed on hello cluster, you can use hello following command tooretrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services

<span data-ttu-id="274ea-207">Merhaba Ambari REST API ile çalışma hakkında daha fazla bilgi için bkz: [izleme ve yönetme hello Ambari REST API kullanarak Hdınsight'ta](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="274ea-207">For more information on working with hello Ambari REST API, see [Monitor and Manage HDInsight using hello Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

#### <a name="service-components"></a><span data-ttu-id="274ea-208">Hizmet bileşenleri</span><span class="sxs-lookup"><span data-stu-id="274ea-208">Service components</span></span>

<span data-ttu-id="274ea-209">Hizmetleri toocheck hello durumunu tek tek istediğiniz bileşenleri içeriyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="274ea-209">Services may contain components that you wish toocheck hello status of individually.</span></span> <span data-ttu-id="274ea-210">Örneğin, HDFS hello iş bileşeni içerir.</span><span class="sxs-lookup"><span data-stu-id="274ea-210">For example, HDFS contains hello NameNode component.</span></span> <span data-ttu-id="274ea-211">tooview bir bileşen hakkında bilgi hello komut şöyle olacaktır:</span><span class="sxs-lookup"><span data-stu-id="274ea-211">tooview information on a component, hello command would be:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

<span data-ttu-id="274ea-212">Hangi bileşenlerin bir hizmeti tarafından sağlanan bilmiyorsanız komutu tooretrieve listesini aşağıdaki hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="274ea-212">If you do not know what components are provided by a service, you can use hello following command tooretrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

## <a name="how-tooaccess-log-files-on-hello-head-nodes"></a><span data-ttu-id="274ea-213">Nasıl tooaccess günlük dosyalarını hello baş düğümler</span><span class="sxs-lookup"><span data-stu-id="274ea-213">How tooaccess log files on hello head nodes</span></span>

### <a name="ssh"></a><span data-ttu-id="274ea-214">SSH</span><span class="sxs-lookup"><span data-stu-id="274ea-214">SSH</span></span>

<span data-ttu-id="274ea-215">Bağlı tooa baş düğüm sırasında SSH aracılığıyla, günlük dosyalarını altında bulunabilir **/var/log**.</span><span class="sxs-lookup"><span data-stu-id="274ea-215">While connected tooa head node through SSH, log files can be found under **/var/log**.</span></span> <span data-ttu-id="274ea-216">Örneğin, **/var/log/hadoop-yarn/yarn** için YARN günlüklerini içerir.</span><span class="sxs-lookup"><span data-stu-id="274ea-216">For example, **/var/log/hadoop-yarn/yarn** contain logs for YARN.</span></span>

<span data-ttu-id="274ea-217">Merhaba hem günlüklerini denetleyin böylece her baş düğüm benzersiz günlük girişlerini olabilir.</span><span class="sxs-lookup"><span data-stu-id="274ea-217">Each head node can have unique log entries, so you should check hello logs on both.</span></span>

### <a name="sftp"></a><span data-ttu-id="274ea-218">SFTP</span><span class="sxs-lookup"><span data-stu-id="274ea-218">SFTP</span></span>

<span data-ttu-id="274ea-219">Merhaba SSH Dosya Aktarım Protokolü veya güvenli Dosya Aktarım Protokolü (SFTP) kullanarak toohello baş düğümüne bağlanmak ve doğrudan hello günlük dosyalarını indirin.</span><span class="sxs-lookup"><span data-stu-id="274ea-219">You can also connect toohello head node using hello SSH File Transfer Protocol or Secure File Transfer Protocol (SFTP), and download hello log files directly.</span></span>

<span data-ttu-id="274ea-220">Benzer toousing sağlamanız gereken toohello küme bağlanırken bir SSH istemcisi SSH kullanıcı hesabı adını ve hello SSH adresini hello küme hello.</span><span class="sxs-lookup"><span data-stu-id="274ea-220">Similar toousing an SSH client, when connecting toohello cluster you must provide hello SSH user account name and hello SSH address of hello cluster.</span></span> <span data-ttu-id="274ea-221">Örneğin, `sftp username@mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="274ea-221">For example, `sftp username@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="274ea-222">İstendiğinde hello hesabı için Hello parola sağlayın veya hello kullanarak bir ortak anahtarı `-i` parametresi.</span><span class="sxs-lookup"><span data-stu-id="274ea-222">Provide hello password for hello account when prompted, or provide a public key using hello `-i` parameter.</span></span>

<span data-ttu-id="274ea-223">Bağlantı kurulduktan sonra size sunulan bir `sftp>` istemi.</span><span class="sxs-lookup"><span data-stu-id="274ea-223">Once connected, you are presented with a `sftp>` prompt.</span></span> <span data-ttu-id="274ea-224">Bu isteminde dizinleri değiştirebilir, dosyaları yükleme ve indirme.</span><span class="sxs-lookup"><span data-stu-id="274ea-224">From this prompt, you can change directories, upload, and download files.</span></span> <span data-ttu-id="274ea-225">Örneğin, aşağıdaki komutları hello değiştirmek dizinleri toohello **/var/log/hadoop/hdfs** dizini ve tüm dosyaların hello dizininde sonra yükleme.</span><span class="sxs-lookup"><span data-stu-id="274ea-225">For example, hello following commands change directories toohello **/var/log/hadoop/hdfs** directory and then download all files in hello directory.</span></span>

    cd /var/log/hadoop/hdfs
    get *

<span data-ttu-id="274ea-226">Kullanılabilir komutlar listesi için girin `help` hello adresindeki `sftp>` istemi.</span><span class="sxs-lookup"><span data-stu-id="274ea-226">For a list of available commands, enter `help` at hello `sftp>` prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="274ea-227">SFTP kullanarak bağlandığında toovisualize hello dosya sistemi izin grafik arabirimleri vardır.</span><span class="sxs-lookup"><span data-stu-id="274ea-227">There are also graphical interfaces that allow you toovisualize hello file system when connected using SFTP.</span></span> <span data-ttu-id="274ea-228">Örneğin, [MobaXTerm](http://mobaxterm.mobatek.net/) bir arabirim benzer tooWindows Explorer kullanarak toobrowse hello dosya sistemi sağlar.</span><span class="sxs-lookup"><span data-stu-id="274ea-228">For example, [MobaXTerm](http://mobaxterm.mobatek.net/) allows you toobrowse hello file system using an interface similar tooWindows Explorer.</span></span>

### <a name="ambari"></a><span data-ttu-id="274ea-229">Ambari</span><span class="sxs-lookup"><span data-stu-id="274ea-229">Ambari</span></span>

> [!NOTE]
> <span data-ttu-id="274ea-230">tooaccess günlük dosyaları Ambari kullanarak, SSH tüneli kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="274ea-230">tooaccess log files using Ambari, you must use an SSH tunnel.</span></span> <span data-ttu-id="274ea-231">Merhaba web arabirimleri hello tek tek Hizmetleri için hello Internet üzerinde herkese açık şekilde sunulmaz.</span><span class="sxs-lookup"><span data-stu-id="274ea-231">hello web interfaces for hello individual services are not exposed publicly on hello Internet.</span></span> <span data-ttu-id="274ea-232">SSH tüneli kullanma hakkında daha fazla bilgi için bkz: hello [kullanım SSH tünel](hdinsight-linux-ambari-ssh-tunnel.md) belge.</span><span class="sxs-lookup"><span data-stu-id="274ea-232">For information on using an SSH tunnel, see hello [Use SSH Tunneling](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="274ea-233">Ambari Web kullanıcı arabirimini Hello tooview günlükleri (örneğin, YARN için) ister hello hizmeti seçin.</span><span class="sxs-lookup"><span data-stu-id="274ea-233">From hello Ambari Web UI, select hello service you wish tooview logs for (for example, YARN).</span></span> <span data-ttu-id="274ea-234">Ardından **hızlı bağlantılar** tooselect hangi baş düğüm tooview hello günlüğe kaydeder.</span><span class="sxs-lookup"><span data-stu-id="274ea-234">Then use **Quick Links** tooselect which head node tooview hello logs for.</span></span>

![Hızlı kullanarak tooview günlükleri bağlar](./media/hdinsight-high-availability-linux/viewlogs.png)

## <a name="how-tooconfigure-hello-node-size"></a><span data-ttu-id="274ea-236">Nasıl tooconfigure hello düğüm boyutu</span><span class="sxs-lookup"><span data-stu-id="274ea-236">How tooconfigure hello node size</span></span>

<span data-ttu-id="274ea-237">bir düğümün başlangıç boyutu, küme oluşturma sırasında yalnızca seçilebilir.</span><span class="sxs-lookup"><span data-stu-id="274ea-237">hello size of a node can only be selected during cluster creation.</span></span> <span data-ttu-id="274ea-238">Kullanılabilir farklı VM boyutları üzerinde hello Hdınsight için hello listesini bulabilirsiniz [Hdınsight fiyatlandırma sayfası](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="274ea-238">You can find a list of hello different VM sizes available for HDInsight on hello [HDInsight pricing page](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="274ea-239">Bir küme oluştururken, hello düğümleri hello boyutunu belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="274ea-239">When creating a cluster, you can specify hello size of hello nodes.</span></span> <span data-ttu-id="274ea-240">Merhaba aşağıdaki bilgileri kılavuz nasıl toospecify hello boyutu kullanarak hello üzerinde sağlar [Azure portal][preview-portal], [Azure PowerShell][azure-powershell], ve hello [Azure CLI][azure-cli]:</span><span class="sxs-lookup"><span data-stu-id="274ea-240">hello following information provides guidance on how toospecify hello size using hello [Azure portal][preview-portal], [Azure PowerShell][azure-powershell], and hello [Azure CLI][azure-cli]:</span></span>

* <span data-ttu-id="274ea-241">**Azure portal**: bir küme oluştururken, hello küme tarafından kullanılan hello düğümleri hello boyutunu ayarlayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="274ea-241">**Azure portal**: When creating a cluster, you can set hello size of hello nodes used by hello cluster:</span></span>

    ![Düğüm boyutu seçimi ile küme oluşturma Sihirbazı'nın resmi](./media/hdinsight-high-availability-linux/headnodesize.png)

* <span data-ttu-id="274ea-243">**Azure CLI**: hello kullanırken `azure hdinsight cluster create` komutunu hello kullanarak hello head, çalışan ve ZooKeeper düğümleri hello boyutunu ayarlayabilirsiniz `--headNodeSize`, `--workerNodeSize`, ve `--zookeeperNodeSize` parametreleri.</span><span class="sxs-lookup"><span data-stu-id="274ea-243">**Azure CLI**: When using hello `azure hdinsight cluster create` command, you can set hello size of hello head, worker, and ZooKeeper nodes by using hello `--headNodeSize`, `--workerNodeSize`, and `--zookeeperNodeSize` parameters.</span></span>

* <span data-ttu-id="274ea-244">**Azure PowerShell**: hello kullanırken `New-AzureRmHDInsightCluster` cmdlet'ini hello kullanarak hello head, çalışan ve ZooKeeper düğümleri hello boyutunu ayarlayabilirsiniz `-HeadNodeVMSize`, `-WorkerNodeSize`, ve `-ZookeeperNodeSize` parametreleri.</span><span class="sxs-lookup"><span data-stu-id="274ea-244">**Azure PowerShell**: When using hello `New-AzureRmHDInsightCluster` cmdlet, you can set hello size of hello head, worker, and ZooKeeper nodes by using hello `-HeadNodeVMSize`, `-WorkerNodeSize`, and `-ZookeeperNodeSize` parameters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="274ea-245">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="274ea-245">Next steps</span></span>

<span data-ttu-id="274ea-246">Bu belgede belirtilen noktalar hakkında daha fazla bağlantılar toolearn aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="274ea-246">Use hello following links toolearn more about things mentioned in this document.</span></span>

* [<span data-ttu-id="274ea-247">Ambari REST başvurusu</span><span class="sxs-lookup"><span data-stu-id="274ea-247">Ambari REST Reference</span></span>](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)
* [<span data-ttu-id="274ea-248">Hello Azure CLI yükleyip</span><span class="sxs-lookup"><span data-stu-id="274ea-248">Install and configure hello Azure CLI</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="274ea-249">Azure PowerShell'i yükleme ve yapılandırma</span><span class="sxs-lookup"><span data-stu-id="274ea-249">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="274ea-250">Ambari kullanarak Hdınsight yönetme</span><span class="sxs-lookup"><span data-stu-id="274ea-250">Manage HDInsight using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)
* [<span data-ttu-id="274ea-251">Linux tabanlı Hdınsight kümeleri hazırlama</span><span class="sxs-lookup"><span data-stu-id="274ea-251">Provision Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)

[preview-portal]: https://portal.azure.com/
[azure-powershell]: /powershell/azureps-cmdlets-docs
[azure-cli]: ../cli-install-nodejs.md
