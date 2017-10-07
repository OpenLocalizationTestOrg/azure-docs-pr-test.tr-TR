---
title: "sanal ağlar - Azure içinde aaaConfigure HBase kümesi çoğaltma | Microsoft Docs"
description: "Bilgi nasıl tooconfigure HBase çoğaltmayı Yük Dengeleme, yüksek kullanılabilirlik, sıfır kapalı kalma süresi geçiş/güncelleştirme bir Hdınsight sürüm tooanother ve olağanüstü durum kurtarma."
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: ba1c44f26b7cbf4a7a88159b12b3e064ea9f9a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hbase-cluster-replication-within-virtual-networks"></a><span data-ttu-id="e155b-103">Sanal ağlar içinde HBase kümesi çoğaltma yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e155b-103">Configure HBase cluster replication within virtual networks</span></span>

<span data-ttu-id="e155b-104">Bilgi nasıl tooconfigure HBase çoğaltmayı bir sanal ağ (VNet) içinde ya da iki sanal ağ arasında.</span><span class="sxs-lookup"><span data-stu-id="e155b-104">Learn how tooconfigure HBase replication within one virtual network (VNet) or between two virtual networks.</span></span>

<span data-ttu-id="e155b-105">Küme çoğaltma, bir kaynak itme Metodoloji kullanır.</span><span class="sxs-lookup"><span data-stu-id="e155b-105">Cluster replication uses a source-push methodology.</span></span> <span data-ttu-id="e155b-106">Her iki rolleri aynı anda gerçekleştirebilir veya bir kaynak veya hedef bir HBase kümesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="e155b-106">An HBase cluster can be a source or a destination, or it can fulfill both roles at once.</span></span> <span data-ttu-id="e155b-107">Çoğaltma uyumsuzdur ve hello çoğaltma nihai tutarlılık hedefidir.</span><span class="sxs-lookup"><span data-stu-id="e155b-107">Replication is asynchronous, and hello goal of replication is eventual consistency.</span></span> <span data-ttu-id="e155b-108">Merhaba kaynak çoğaltmanın etkinleştirilmiş olduğu bir düzenleme tooa sütun ailesi aldığında, bu düzenleme yayılan tooall hedef küme sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="e155b-108">When hello source receives an edit tooa column family with replication enabled, that edit is propagated tooall destination clusters.</span></span> <span data-ttu-id="e155b-109">Bir küme tooanother veri çoğaltıldığında hello kaynak kümesi ve hello veri zaten tüketilen tüm kümeleri izlenen tooprevent çoğaltma döngüleri var.</span><span class="sxs-lookup"><span data-stu-id="e155b-109">When data is replicated from one cluster tooanother, hello source cluster and all clusters that have already consumed hello data are tracked tooprevent replication loops.</span></span>

<span data-ttu-id="e155b-110">Bu öğreticide, bir kaynak hedef çoğaltma yapılandırır.</span><span class="sxs-lookup"><span data-stu-id="e155b-110">In this tutorial, you will configure a source-destination replication.</span></span> <span data-ttu-id="e155b-111">Diğer küme Topolojileri için bkz: [Apache HBase Başvuru Kılavuzu](http://hbase.apache.org/book.html#_cluster_replication).</span><span class="sxs-lookup"><span data-stu-id="e155b-111">For other cluster topologies, see [Apache HBase Reference Guide](http://hbase.apache.org/book.html#_cluster_replication).</span></span>

<span data-ttu-id="e155b-112">HBase çoğaltma kullanım durumları tek bir sanal ağ için:</span><span class="sxs-lookup"><span data-stu-id="e155b-112">HBase replication usage cases for a single virtual network:</span></span>

* <span data-ttu-id="e155b-113">--Örneğin, tarama veya MapReduce işleri hello hedef küme üzerinde çalışan ve veri hello kaynak kümesi alma Yük Dengeleme</span><span class="sxs-lookup"><span data-stu-id="e155b-113">Load balancing--for example, running scans or MapReduce jobs on hello destination cluster and ingesting data on hello source cluster</span></span>
* <span data-ttu-id="e155b-114">Yüksek kullanılabilirlik</span><span class="sxs-lookup"><span data-stu-id="e155b-114">High availability</span></span>
* <span data-ttu-id="e155b-115">Bir HBase kümesi tooanother gelen verileri geçirme</span><span class="sxs-lookup"><span data-stu-id="e155b-115">Migrating data from one HBase cluster tooanother</span></span>
* <span data-ttu-id="e155b-116">Azure Hdınsight kümesi bir sürüm tooanother yükseltme</span><span class="sxs-lookup"><span data-stu-id="e155b-116">Upgrading an Azure HDInsight cluster from one version tooanother</span></span>

<span data-ttu-id="e155b-117">HBase çoğaltma kullanım durumları iki sanal ağ için:</span><span class="sxs-lookup"><span data-stu-id="e155b-117">HBase replication usage cases for two virtual networks:</span></span>

* <span data-ttu-id="e155b-118">Olağanüstü durum kurtarma</span><span class="sxs-lookup"><span data-stu-id="e155b-118">Disaster recovery</span></span>
* <span data-ttu-id="e155b-119">Yük Dengeleme ve Merhaba uygulaması bölümlendirme</span><span class="sxs-lookup"><span data-stu-id="e155b-119">Load balancing and partitioning hello application</span></span>
* <span data-ttu-id="e155b-120">Yüksek kullanılabilirlik</span><span class="sxs-lookup"><span data-stu-id="e155b-120">High availability</span></span>

<span data-ttu-id="e155b-121">Kümeleri kullanarak çoğaltma [betik eylemi](hdinsight-hadoop-customize-cluster-linux.md) betikleri bulunan [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).</span><span class="sxs-lookup"><span data-stu-id="e155b-121">You replicate clusters by using [script action](hdinsight-hadoop-customize-cluster-linux.md) scripts located at [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e155b-122">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e155b-122">Prerequisites</span></span>
<span data-ttu-id="e155b-123">Bu öğreticiye başlamadan önce bir Azure aboneliğinizin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="e155b-123">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="e155b-124">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="e155b-124">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="configure-hello-environments"></a><span data-ttu-id="e155b-125">Merhaba ortamları yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e155b-125">Configure hello environments</span></span>

<span data-ttu-id="e155b-126">Üç olası yapılandırmaları vardır:</span><span class="sxs-lookup"><span data-stu-id="e155b-126">There are three possible configurations:</span></span>

- <span data-ttu-id="e155b-127">Bir Azure sanal ağı iki HBase kümelerini</span><span class="sxs-lookup"><span data-stu-id="e155b-127">Two HBase clusters in one Azure virtual network</span></span>
- <span data-ttu-id="e155b-128">Aynı bölge içinde iki farklı sanal ağlar iki HBase kümelerini hello</span><span class="sxs-lookup"><span data-stu-id="e155b-128">Two HBase clusters in two different virtual networks in hello same region</span></span>
- <span data-ttu-id="e155b-129">İki HBase kümelerini iki farklı bölgelerde (coğrafi çoğaltma) iki farklı sanal ağlar</span><span class="sxs-lookup"><span data-stu-id="e155b-129">Two HBase clusters in two different virtual networks in two different regions (geo-replication)</span></span>

<span data-ttu-id="e155b-130">toomake bunu daha kolay tooconfigure hello ortamları oluşturduğumuz bazı [Azure Resource Manager şablonları](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e155b-130">toomake it easier tooconfigure hello environments, we have created some [Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="e155b-131">Diğer yöntemleri kullanarak tooconfigure hello ortamları tercih ederseniz, bkz:</span><span class="sxs-lookup"><span data-stu-id="e155b-131">If you prefer tooconfigure hello environments by using other methods, see:</span></span>

- [<span data-ttu-id="e155b-132">Hdınsight'ta Linux tabanlı Hadoop kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="e155b-132">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
- [<span data-ttu-id="e155b-133">Azure sanal ağında HBase kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="e155b-133">Create HBase clusters in Azure Virtual Network</span></span>](hdinsight-hbase-provision-vnet.md)

### <a name="configure-one-virtual-network"></a><span data-ttu-id="e155b-134">Bir sanal ağ yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e155b-134">Configure one virtual network</span></span>

<span data-ttu-id="e155b-135">Merhaba görüntü toocreate iki HBase kümelerini aşağıdaki hello tıklatın aynı sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="e155b-135">Click hello following image toocreate two HBase clusters in hello same virtual network.</span></span> <span data-ttu-id="e155b-136">Merhaba şablon depolanır [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).</span><span class="sxs-lookup"><span data-stu-id="e155b-136">hello template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-one-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

### <a name="configure-two-virtual-networks-in-hello-same-region"></a><span data-ttu-id="e155b-137">Hello iki sanal ağ yapılandırma aynı bölge</span><span class="sxs-lookup"><span data-stu-id="e155b-137">Configure two virtual networks in hello same region</span></span>

<span data-ttu-id="e155b-138">Görüntü toocreate iki sanal ağ VNet eşlemesi ve hello iki HBase kümeleri ile aşağıdaki hello tıklatın aynı bölgede.</span><span class="sxs-lookup"><span data-stu-id="e155b-138">Click hello following image toocreate two virtual networks with VNet peering and two HBase clusters in hello same region.</span></span> <span data-ttu-id="e155b-139">Merhaba şablon depolanır [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).</span><span class="sxs-lookup"><span data-stu-id="e155b-139">hello template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-two-vnets-same-region%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>



<span data-ttu-id="e155b-140">Bu senaryo gerektirir [VNet eşlemesi](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e155b-140">This scenario requires [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> <span data-ttu-id="e155b-141">VNet eşlemesi Hello şablonu sağlar.</span><span class="sxs-lookup"><span data-stu-id="e155b-141">hello template enables VNet peering.</span></span>   

<span data-ttu-id="e155b-142">HBase çoğaltmayı hello ZooKeeper VM'ler IP adreslerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="e155b-142">HBase replication uses IP addresses of hello ZooKeeper VMs.</span></span> <span data-ttu-id="e155b-143">Merhaba hedef HBase ZooKeeper düğümleri için statik IP adresi yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e155b-143">You must configure static IP addresses for hello destination HBase ZooKeeper nodes.</span></span>

<span data-ttu-id="e155b-144">**tooconfigure statik IP adresleri**</span><span class="sxs-lookup"><span data-stu-id="e155b-144">**tooconfigure static IP addresses**</span></span>

1. <span data-ttu-id="e155b-145">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e155b-145">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e155b-146">Merhaba sol menüden **kaynak grupları**.</span><span class="sxs-lookup"><span data-stu-id="e155b-146">From hello left menu, click **Resource Groups**.</span></span>
3. <span data-ttu-id="e155b-147">Merhaba hedef HBase kümesi içeren kaynak grubunuz'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e155b-147">Click your resource group that contains hello destination HBase cluster.</span></span> <span data-ttu-id="e155b-148">Merhaba Resource Manager şablonu toocreate hello ortamı kullanıldığında, belirttiğiniz hello kaynak grubu budur.</span><span class="sxs-lookup"><span data-stu-id="e155b-148">This is hello resource group that you specified when you used hello Resource Manager template toocreate hello environment.</span></span> <span data-ttu-id="e155b-149">Merhaba filtre toonarrow hello listesini aşağı kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e155b-149">You can use hello filter toonarrow down hello list.</span></span> <span data-ttu-id="e155b-150">Merhaba iki sanal ağ içeren kaynakların bir listesini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e155b-150">You can see a list of resources that contains hello two virtual networks.</span></span>
4. <span data-ttu-id="e155b-151">Merhaba hedef HBase kümesi içeren hello sanal ağ'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e155b-151">Click hello virtual network that contains hello destination HBase cluster.</span></span> <span data-ttu-id="e155b-152">Örneğin, **xxxx-vnet2'yi**.</span><span class="sxs-lookup"><span data-stu-id="e155b-152">For example, click **xxxx-vnet2**.</span></span> <span data-ttu-id="e155b-153">İle başlayan üç aygıtlarla adlarını görebilirsiniz **NIC-zookeepermode -**.</span><span class="sxs-lookup"><span data-stu-id="e155b-153">You can see three devices with names that start with **nic-zookeepermode-**.</span></span> <span data-ttu-id="e155b-154">Bu cihazların Merhaba üç ZooKeeper VM'ler ' dir.</span><span class="sxs-lookup"><span data-stu-id="e155b-154">Those devices are hello three ZooKeeper VMs.</span></span>
5. <span data-ttu-id="e155b-155">Merhaba ZooKeeper VM'ler birini tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e155b-155">Click one of hello ZooKeeper VMs.</span></span>
6. <span data-ttu-id="e155b-156">Tıklatın **IP yapılandırmaları**.</span><span class="sxs-lookup"><span data-stu-id="e155b-156">Click **IP configurations**.</span></span>
7. <span data-ttu-id="e155b-157">Tıklatın **ipConfig1** hello listeden.</span><span class="sxs-lookup"><span data-stu-id="e155b-157">Click **ipConfig1** from hello list.</span></span>
8. <span data-ttu-id="e155b-158">Tıklatın **statik**ve hello gerçek IP adresini yazın.</span><span class="sxs-lookup"><span data-stu-id="e155b-158">Click **Static**, and write down hello actual IP address.</span></span> <span data-ttu-id="e155b-159">Merhaba betik eylemi tooenable çoğaltma çalıştırdığınızda, başlangıç IP adresi gerekir.</span><span class="sxs-lookup"><span data-stu-id="e155b-159">You will need hello IP address when you run hello script action tooenable replication.</span></span>

  ![Hdınsight HBase çoğaltma ZooKeeper statik IP](./media/hdinsight-hbase-replication/hdinsight-hbase-replication-zookeeper-static-ip.png)

9. <span data-ttu-id="e155b-161">Adım 6 tooset hello statik IP adresi, diğer iki ZooKeeper düğümleri hello için yineleyin.</span><span class="sxs-lookup"><span data-stu-id="e155b-161">Repeat step 6 tooset hello static IP address for hello other two ZooKeeper nodes.</span></span>

<span data-ttu-id="e155b-162">Merhaba arası VNet senaryosu için hello kullanmalısınız **- IP** hello çağrılırken geçiş **hdi_enable_replication.sh** betik eylemi.</span><span class="sxs-lookup"><span data-stu-id="e155b-162">For hello cross-VNet scenario, you must use hello **-ip** switch when calling hello **hdi_enable_replication.sh** script action.</span></span>

### <a name="configure-two-virtual-networks-in-two-different-regions"></a><span data-ttu-id="e155b-163">İki farklı bölgelerde iki sanal ağ yapılandırma</span><span class="sxs-lookup"><span data-stu-id="e155b-163">Configure two virtual networks in two different regions</span></span>

<span data-ttu-id="e155b-164">Görüntü toocreate iki sanal ağ iki farklı bölgelerdeki aşağıdaki hello'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="e155b-164">Click hello following image toocreate two virtual networks in two different regions.</span></span> <span data-ttu-id="e155b-165">Merhaba şablonu bir ortak Azure Blob kapsayıcısında depolanır.</span><span class="sxs-lookup"><span data-stu-id="e155b-165">hello template is stored in a public Azure Blob container.</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhbaseha%2Fdeploy-hbase-geo-replication.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

<span data-ttu-id="e155b-166">Merhaba iki sanal ağ arasında bir VPN ağ geçidi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e155b-166">Create a VPN gateway between hello two virtual networks.</span></span> <span data-ttu-id="e155b-167">Yönergeler için bkz: [bir siteden siteye bağlantısı olan bir VNet oluşturma](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e155b-167">For instructions, see [Create a VNet with a site-to-site connection](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).</span></span>

<span data-ttu-id="e155b-168">HBase çoğaltmayı hello ZooKeeper VM'ler IP adreslerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="e155b-168">HBase replication uses IP addresses of hello ZooKeeper VMs.</span></span> <span data-ttu-id="e155b-169">Merhaba hedef HBase ZooKeeper düğümleri için statik IP adresi yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="e155b-169">You must configure static IP addresses for hello destination HBase ZooKeeper nodes.</span></span> <span data-ttu-id="e155b-170">statik IP tooconfigure, bu makaledeki hello "yapılandırma iki sanal ağlarda aynı bölgede hello" bölümüne bakın.</span><span class="sxs-lookup"><span data-stu-id="e155b-170">tooconfigure static IP, see hello "Configure two virtual networks in hello same region" section in this article.</span></span>

<span data-ttu-id="e155b-171">Merhaba arası VNet senaryosu için hello kullanmalısınız **- IP** hello çağrılırken geçiş **hdi_enable_replication.sh** betik eylemi.</span><span class="sxs-lookup"><span data-stu-id="e155b-171">For hello cross-VNet scenario, you must use hello **-ip** switch when calling hello **hdi_enable_replication.sh** script action.</span></span>

## <a name="load-test-data"></a><span data-ttu-id="e155b-172">Yük testi verileri</span><span class="sxs-lookup"><span data-stu-id="e155b-172">Load test data</span></span>

<span data-ttu-id="e155b-173">Bir küme çoğalttığınızda, hello tabloları tooreplicate belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="e155b-173">When you replicate a cluster, you must specify hello tables tooreplicate.</span></span> <span data-ttu-id="e155b-174">Bu bölümde, bazı veriler hello kaynak kümesine yükler.</span><span class="sxs-lookup"><span data-stu-id="e155b-174">In this section, you will load some data into hello source cluster.</span></span> <span data-ttu-id="e155b-175">Merhaba sonraki bölümde hello iki küme arasında çoğaltmayı etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="e155b-175">In hello next section, you will enable replication between hello two clusters.</span></span>

<span data-ttu-id="e155b-176">Merhaba yönergeleri izleyin [HBase Öğreticisi: hdınsight'ta Linux tabanlı Hadoop ile Apache HBase kullanmaya başlamanıza](hdinsight-hbase-tutorial-get-started-linux.md) toocreate bir **kişiler** tablo ve bazı verileri hello tabloya ekleyin.</span><span class="sxs-lookup"><span data-stu-id="e155b-176">Follow hello instructions in [HBase tutorial: Get started using Apache HBase with Linux-based Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) toocreate a **Contacts** table and insert some data into hello table.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="e155b-177">Çoğaltmayı etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="e155b-177">Enable replication</span></span>

<span data-ttu-id="e155b-178">Aşağıdaki adımları hello nasıl toocall hello betik eylemi hello Azure portal betikten gösterir.</span><span class="sxs-lookup"><span data-stu-id="e155b-178">hello following steps show how toocall hello script action script from hello Azure portal.</span></span> <span data-ttu-id="e155b-179">Azure PowerShell ve hello Azure komut satırı arabirimi (CLI) kullanarak bir komut dosyası eylemi çalıştırmak için bkz: [özelleştirme Linux tabanlı Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="e155b-179">For running a script action by using Azure PowerShell and hello Azure command-line interface (CLI), see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="e155b-180">**tooenable HBase çoğaltmayı hello Azure portalı**</span><span class="sxs-lookup"><span data-stu-id="e155b-180">**tooenable HBase replication from hello Azure portal**</span></span>

1. <span data-ttu-id="e155b-181">İçinde toohello oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e155b-181">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="e155b-182">Merhaba kaynak HBase kümesi'ni açın.</span><span class="sxs-lookup"><span data-stu-id="e155b-182">Open hello source HBase cluster.</span></span>
3. <span data-ttu-id="e155b-183">Merhaba küme menüden **betik eylemleri**.</span><span class="sxs-lookup"><span data-stu-id="e155b-183">From hello cluster menu, click **Script Actions**.</span></span>
4. <span data-ttu-id="e155b-184">Tıklatın **gönderme yeni** hello dikey hello üstten.</span><span class="sxs-lookup"><span data-stu-id="e155b-184">Click **Submit New** from hello top of hello blade.</span></span>
5. <span data-ttu-id="e155b-185">Aşağıdaki bilgilerle hello girin veya seçin:</span><span class="sxs-lookup"><span data-stu-id="e155b-185">Select or enter hello following information:</span></span>

  - <span data-ttu-id="e155b-186">**Ad**: girin **çoğaltmasını etkinleştir**.</span><span class="sxs-lookup"><span data-stu-id="e155b-186">**Name**: Enter **Enable replication**.</span></span>
  - <span data-ttu-id="e155b-187">**Komut dosyası URL'si bash**: girin **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.</span><span class="sxs-lookup"><span data-stu-id="e155b-187">**Bash Script URL**: Enter **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.</span></span>
  - <span data-ttu-id="e155b-188">**HEAD**: Seçili.</span><span class="sxs-lookup"><span data-stu-id="e155b-188">**Head**: Selected.</span></span> <span data-ttu-id="e155b-189">Clear diğer düğüm türleri hello.</span><span class="sxs-lookup"><span data-stu-id="e155b-189">Clear hello other node types.</span></span>
  - <span data-ttu-id="e155b-190">**Parametreleri**: hello aşağıdaki örnek parametreleri tüm hello varolan tablolar için çoğaltma etkinleştirme ve tüm hello veri hello kaynak küme toohello hedef kümeden kopyalayın:</span><span class="sxs-lookup"><span data-stu-id="e155b-190">**Parameters**: hello following sample parameters enable replication for all hello existing tables and copy all hello data from hello source cluster toohello destination cluster:</span></span>

            -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -copydata

6. <span data-ttu-id="e155b-191">**Oluştur**'a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="e155b-191">Click **Create**.</span></span> <span data-ttu-id="e155b-192">Merhaba betik biraz zaman alabilir özellikle zaman hello - copydata bağımsız değişkeninin değeri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="e155b-192">hello script can take some time, especially when hello -copydata argument is used.</span></span>

<span data-ttu-id="e155b-193">Gerekli bağımsız değişkenler:</span><span class="sxs-lookup"><span data-stu-id="e155b-193">Required arguments:</span></span>

|<span data-ttu-id="e155b-194">Ad</span><span class="sxs-lookup"><span data-stu-id="e155b-194">Name</span></span>|<span data-ttu-id="e155b-195">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e155b-195">Description</span></span>|
|----|-----------|
|<span data-ttu-id="e155b-196">-s--src-küme</span><span class="sxs-lookup"><span data-stu-id="e155b-196">-s, --src-cluster</span></span> | <span data-ttu-id="e155b-197">Merhaba kaynak HBase kümesi Hello DNS adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="e155b-197">Specify hello DNS name of hello source HBase cluster.</span></span> <span data-ttu-id="e155b-198">Örneğin: -s hbsrccluster,--src küme hbsrccluster =</span><span class="sxs-lookup"><span data-stu-id="e155b-198">For example: -s hbsrccluster, --src-cluster=hbsrccluster</span></span> |
|<span data-ttu-id="e155b-199">-d--dst küme</span><span class="sxs-lookup"><span data-stu-id="e155b-199">-d, --dst-cluster</span></span> | <span data-ttu-id="e155b-200">Merhaba hedef (Çoğaltma) HBase kümesi Hello DNS adını belirtin.</span><span class="sxs-lookup"><span data-stu-id="e155b-200">Specify hello DNS name of hello destination (replica) HBase cluster.</span></span> <span data-ttu-id="e155b-201">Örneğin: -s dsthbcluster,--src küme dsthbcluster =</span><span class="sxs-lookup"><span data-stu-id="e155b-201">For example: -s dsthbcluster, --src-cluster=dsthbcluster</span></span> |
|<span data-ttu-id="e155b-202">-sp,--src ambari parolası</span><span class="sxs-lookup"><span data-stu-id="e155b-202">-sp, --src-ambari-password</span></span> | <span data-ttu-id="e155b-203">Merhaba yönetici parolası için Ambari hello kaynak HBase kümesi üzerinde belirtin.</span><span class="sxs-lookup"><span data-stu-id="e155b-203">Specify hello admin password for Ambari on hello source HBase cluster.</span></span> |
|<span data-ttu-id="e155b-204">-dp,--dst ambari parolası</span><span class="sxs-lookup"><span data-stu-id="e155b-204">-dp, --dst-ambari-password</span></span> | <span data-ttu-id="e155b-205">Merhaba yönetici parolası için Ambari hello hedef HBase kümesi üzerinde belirtin.</span><span class="sxs-lookup"><span data-stu-id="e155b-205">Specify hello admin password for Ambari on hello destination HBase cluster.</span></span>|

<span data-ttu-id="e155b-206">İsteğe bağlı bağımsız değişkenler:</span><span class="sxs-lookup"><span data-stu-id="e155b-206">Optional arguments:</span></span>

|<span data-ttu-id="e155b-207">Ad</span><span class="sxs-lookup"><span data-stu-id="e155b-207">Name</span></span>|<span data-ttu-id="e155b-208">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e155b-208">Description</span></span>|
|----|-----------|
|<span data-ttu-id="e155b-209">-su,--src ambari kullanıcı</span><span class="sxs-lookup"><span data-stu-id="e155b-209">-su, --src-ambari-user</span></span> | <span data-ttu-id="e155b-210">Merhaba yönetici kullanıcı için Ambari hello kaynak HBase kümesi üzerinde belirtin.</span><span class="sxs-lookup"><span data-stu-id="e155b-210">Specify hello admin username for Ambari on hello source HBase cluster.</span></span> <span data-ttu-id="e155b-211">Merhaba varsayılan değer **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="e155b-211">hello default value is **admin**.</span></span> |
|<span data-ttu-id="e155b-212">-du,--dst ambari kullanıcı</span><span class="sxs-lookup"><span data-stu-id="e155b-212">-du, --dst-ambari-user</span></span> | <span data-ttu-id="e155b-213">Merhaba yönetici kullanıcı için Ambari hello hedef HBase kümesi üzerinde belirtin.</span><span class="sxs-lookup"><span data-stu-id="e155b-213">Specify hello admin username for Ambari on hello destination HBase cluster.</span></span> <span data-ttu-id="e155b-214">Merhaba varsayılan değer **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="e155b-214">hello default value is **admin**.</span></span> |
|<span data-ttu-id="e155b-215">-t,--Tablo listesi</span><span class="sxs-lookup"><span data-stu-id="e155b-215">-t, --table-list</span></span> | <span data-ttu-id="e155b-216">Çoğaltılan hello tabloları toobe belirtin.</span><span class="sxs-lookup"><span data-stu-id="e155b-216">Specify hello tables toobe replicated.</span></span> <span data-ttu-id="e155b-217">Örneğin: – Tablo listesi = "tablo1; tablo2; Tablo3".</span><span class="sxs-lookup"><span data-stu-id="e155b-217">For example: --table-list="table1;table2;table3".</span></span> <span data-ttu-id="e155b-218">Tabloları belirtmezseniz, tüm var olan HBase tablolarını çoğaltılır.</span><span class="sxs-lookup"><span data-stu-id="e155b-218">If you don't specify tables, all existing HBase tables are replicated.</span></span>|
|<span data-ttu-id="e155b-219">-m,--makine</span><span class="sxs-lookup"><span data-stu-id="e155b-219">-m, --machine</span></span> | <span data-ttu-id="e155b-220">Merhaba betik eylemi çalıştırılacağı hello baş düğüm belirtin.</span><span class="sxs-lookup"><span data-stu-id="e155b-220">Specify hello head node where hello script action will run.</span></span> <span data-ttu-id="e155b-221">Merhaba hn1 veya hn0 değerdir.</span><span class="sxs-lookup"><span data-stu-id="e155b-221">hello value is either hn1 or hn0.</span></span> <span data-ttu-id="e155b-222">Hn0 genellikle yoğun olduğundan hn1 kullanmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="e155b-222">Because hn0 is usually busier, we recommend using hn1.</span></span> <span data-ttu-id="e155b-223">Merhaba $0 betik hello Hdınsight portal ya da Azure PowerShell betik eylemi çalıştırıyorsanız bu seçeneği kullanın.</span><span class="sxs-lookup"><span data-stu-id="e155b-223">You use this option when you're running hello $0 script as a script action from hello HDInsight portal or Azure PowerShell.</span></span>|
|<span data-ttu-id="e155b-224">-IP</span><span class="sxs-lookup"><span data-stu-id="e155b-224">-ip</span></span> | <span data-ttu-id="e155b-225">İki sanal ağ arasında çoğaltmayı etkinleştirirken bu bağımsız değişkeni gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e155b-225">This argument is required when you're enabling replication between two virtual networks.</span></span> <span data-ttu-id="e155b-226">Bir anahtar toouse hello statik IP, ZooKeeper çoğaltma küme düğümü FQDN adları yerine bu bağımsız değişken görür.</span><span class="sxs-lookup"><span data-stu-id="e155b-226">This argument acts as a switch toouse hello static IPs of ZooKeeper nodes from replica clusters instead of FQDN names.</span></span> <span data-ttu-id="e155b-227">Merhaba statik IP çoğaltma etkinleştirmeden önce önceden yapılandırılmış toobe gerekir.</span><span class="sxs-lookup"><span data-stu-id="e155b-227">hello static IPs need toobe preconfigured before you enable replication.</span></span> |
|<span data-ttu-id="e155b-228">-TP, - copydata</span><span class="sxs-lookup"><span data-stu-id="e155b-228">-cp, -copydata</span></span> | <span data-ttu-id="e155b-229">Çoğaltma etkinleştirdiğiniz hello tablolarda varolan verilerin Hello geçişi etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e155b-229">Enable hello migration of existing data on hello tables where replication is enabled.</span></span> |
|<span data-ttu-id="e155b-230">-rpm, - replicate-phoenix-meta</span><span class="sxs-lookup"><span data-stu-id="e155b-230">-rpm, -replicate-phoenix-meta</span></span> | <span data-ttu-id="e155b-231">Phoenix Sistem tabloları çoğaltmayı etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="e155b-231">Enable replication on Phoenix system tables.</span></span> <br><br><span data-ttu-id="e155b-232">*Bu seçeneği dikkatli kullanın.*</span><span class="sxs-lookup"><span data-stu-id="e155b-232">*Use this option with caution.*</span></span> <span data-ttu-id="e155b-233">Bu komut dosyasını kullanmadan önce çoğaltma kümeleri Phoenix tablolarda yeniden oluşturmanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="e155b-233">We recommend that you re-create Phoenix tables on replica clusters before you use this script.</span></span> |
|<span data-ttu-id="e155b-234">-h,--Yardım</span><span class="sxs-lookup"><span data-stu-id="e155b-234">-h, --help</span></span> | <span data-ttu-id="e155b-235">Kullanım bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="e155b-235">Display usage information.</span></span> |

<span data-ttu-id="e155b-236">Merhaba hello print_usage() bölümünü [betik](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) parametreleri ayrıntılı bir açıklamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="e155b-236">hello print_usage() section of hello [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) provides a detailed explanation of parameters.</span></span>

<span data-ttu-id="e155b-237">Merhaba betik eylemi başarıyla tamamlandıktan sonra dağıtılmış, size SSH tooconnect toohello hedef HBase kümesi, kullanıp hello veri çoğaltıldığını doğrulayın.</span><span class="sxs-lookup"><span data-stu-id="e155b-237">After hello script action is successfully deployed, you can use SSH tooconnect toohello destination HBase cluster, and verify hello data has been replicated.</span></span>

### <a name="replication-scenarios"></a><span data-ttu-id="e155b-238">Çoğaltma senaryoları</span><span class="sxs-lookup"><span data-stu-id="e155b-238">Replication scenarios</span></span>

<span data-ttu-id="e155b-239">Merhaba aşağıdaki listede, bazı genel kullanım örnekleri ve parametre ayarlarına gösterir:</span><span class="sxs-lookup"><span data-stu-id="e155b-239">hello following list shows you some general usage cases and their parameter settings:</span></span>

- <span data-ttu-id="e155b-240">**Tüm tablolarda hello iki küme arasında çoğaltmayı etkinleştirmek**.</span><span class="sxs-lookup"><span data-stu-id="e155b-240">**Enable replication on all tables between hello two clusters**.</span></span> <span data-ttu-id="e155b-241">Bu senaryo hello Kopyala/hello tablolarda mevcut verilerin geçişini gerektirmez ve Phoenix tabloları kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="e155b-241">This scenario does not require hello copy/migration of existing data on hello tables, and it does not use Phoenix tables.</span></span> <span data-ttu-id="e155b-242">Şu parametreler hello kullan:</span><span class="sxs-lookup"><span data-stu-id="e155b-242">Use hello following parameters:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password>  

- <span data-ttu-id="e155b-243">**Belirli tablolarda çoğaltmayı etkinleştirme**.</span><span class="sxs-lookup"><span data-stu-id="e155b-243">**Enable replication on specific tables**.</span></span> <span data-ttu-id="e155b-244">Tablo1, tablo2 ve Tablo3 parametreleri tooenable çoğaltma aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="e155b-244">Use hello following parameters tooenable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3"

- <span data-ttu-id="e155b-245">**Belirli tablolarda çoğaltmayı etkinleştirmek ve hello mevcut veri kopyalama**.</span><span class="sxs-lookup"><span data-stu-id="e155b-245">**Enable replication on specific tables and copy hello existing data**.</span></span> <span data-ttu-id="e155b-246">Tablo1, tablo2 ve Tablo3 parametreleri tooenable çoğaltma aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="e155b-246">Use hello following parameters tooenable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -copydata

- <span data-ttu-id="e155b-247">**Phoenix meta veri kaynağı toodestination çoğaltma ile tüm tablolarda çoğaltmayı etkinleştirme**.</span><span class="sxs-lookup"><span data-stu-id="e155b-247">**Enable replication on all tables with replicating phoenix metadata from source toodestination**.</span></span> <span data-ttu-id="e155b-248">Phoenix meta veri çoğaltma kusursuz değildir ve dikkatli bir şekilde etkinleştirilmiş olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="e155b-248">Phoenix metadata replication is not perfect and should be enabled with caution.</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -replicate-phoenix-meta

## <a name="copy-and-migrate-data"></a><span data-ttu-id="e155b-249">Kopyalama ve verileri geçirme</span><span class="sxs-lookup"><span data-stu-id="e155b-249">Copy and migrate data</span></span>

<span data-ttu-id="e155b-250">Kopyalama ve taşıma için iki ayrı komut dosyası eylemi betikleri vardır çoğaltma etkinleştirildikten sonra verileri:</span><span class="sxs-lookup"><span data-stu-id="e155b-250">There are two separate script action scripts for copying/migrating data after replication is enabled:</span></span>

- <span data-ttu-id="e155b-251">[Küçük tablolar için komut dosyası](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (birkaç gigabayttan boyut ve genel kopyasında olduğu beklenen toofinish bir saatten kısa bir süre içinde)</span><span class="sxs-lookup"><span data-stu-id="e155b-251">[Script for small tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (a few gigabytes in size, and overall copy is expected toofinish in less than one hour)</span></span>

- <span data-ttu-id="e155b-252">[Büyük tablolar için komut dosyası](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (beklenen tootake bir saat toocopy uzun)</span><span class="sxs-lookup"><span data-stu-id="e155b-252">[Script for large tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (expected tootake longer than one hour toocopy)</span></span>

<span data-ttu-id="e155b-253">İzleyebileceğiniz hello aynı yordamda [çoğaltmasını etkinleştir](#enable-replication) toocall hello betik eylemi şu parametreler hello ile:</span><span class="sxs-lookup"><span data-stu-id="e155b-253">You can follow hello same procedure in [Enable replication](#enable-replication) toocall hello script action with hello following parameters:</span></span>

    -m hn1 -t <table1:start_timestamp:end_timestamp;table2:start_timestamp:end_timestamp;...> -p <replication_peer> [-everythingTillNow]

<span data-ttu-id="e155b-254">Merhaba hello print_usage() bölümünü [betik](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) parametreleri ayrıntılı bir açıklaması verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="e155b-254">hello print_usage() section of hello [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) provides a detailed description of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="e155b-255">Senaryolar</span><span class="sxs-lookup"><span data-stu-id="e155b-255">Scenarios</span></span>

- <span data-ttu-id="e155b-256">**Şimdi düzenlenen tüm satırlar için belirli tabloları (test1, test2 ve test3) kopyalayın (geçerli zaman damgası)**:</span><span class="sxs-lookup"><span data-stu-id="e155b-256">**Copy specific tables (test1, test2, and test3) for all rows edited till now (current time stamp)**:</span></span>

        -m hn1 -t "test1::;test2::;test3::" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow
  <span data-ttu-id="e155b-257">or</span><span class="sxs-lookup"><span data-stu-id="e155b-257">or</span></span>

        -m hn1 -t "test1::;test2::;test3::" --replication-peer="zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow


- <span data-ttu-id="e155b-258">**Belirtilen zaman aralığı belirli tablolarla kopyalama**:</span><span class="sxs-lookup"><span data-stu-id="e155b-258">**Copy specific tables with specified time range**:</span></span>

        -m hn1 -t "table1:0:452256397;table2:14141444:452256397" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure"


## <a name="disable-replication"></a><span data-ttu-id="e155b-259">Çoğaltma devre dışı bırak</span><span class="sxs-lookup"><span data-stu-id="e155b-259">Disable replication</span></span>

<span data-ttu-id="e155b-260">toodisable çoğaltma konumunda bulunan başka bir komut dosyası eylemi komut dosyasını kullanın [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh).</span><span class="sxs-lookup"><span data-stu-id="e155b-260">toodisable replication, you use another script action script located at [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh).</span></span> <span data-ttu-id="e155b-261">İzleyebileceğiniz hello aynı yordamda [çoğaltmasını etkinleştir](#enable-replication) toocall hello betik eylemi şu parametreler hello ile:</span><span class="sxs-lookup"><span data-stu-id="e155b-261">You can follow hello same procedure in [Enable replication](#enable-replication) toocall hello script action with hello following parameters:</span></span>

    -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari Password> <-all|-t "table1;table2;...">  

<span data-ttu-id="e155b-262">Merhaba hello print_usage() bölümünü [betik](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) parametreleri ayrıntılı bir açıklamasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="e155b-262">hello print_usage() section of hello [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) provides a detailed explanation of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="e155b-263">Senaryolar</span><span class="sxs-lookup"><span data-stu-id="e155b-263">Scenarios</span></span>

- <span data-ttu-id="e155b-264">**Çoğaltma tüm tablolarda devre dışı**:</span><span class="sxs-lookup"><span data-stu-id="e155b-264">**Disable replication on all tables**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp Mypassword\!789 -all
  <span data-ttu-id="e155b-265">or</span><span class="sxs-lookup"><span data-stu-id="e155b-265">or</span></span>

        --src-cluster=<source cluster DNS name> --dst-cluster=<destination cluster DNS name> --src-ambari-user=<source cluster Ambari username> --src-ambari-password=<source cluster Ambari password>

- <span data-ttu-id="e155b-266">**Çoğaltmayı belirtilen tablolarda (tablo1, tablo2 ve Tablo3) devre dışı**:</span><span class="sxs-lookup"><span data-stu-id="e155b-266">**Disable replication on specified tables (table1, table2, and table3)**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari password> -t "table1;table2;table3"

## <a name="next-steps"></a><span data-ttu-id="e155b-267">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e155b-267">Next steps</span></span>

<span data-ttu-id="e155b-268">Bu öğreticide, nasıl öğrenilen tooconfigure HBase çoğaltmayı iki veri merkezi arasında.</span><span class="sxs-lookup"><span data-stu-id="e155b-268">In this tutorial, you learned how tooconfigure HBase replication across two datacenters.</span></span> <span data-ttu-id="e155b-269">Hdınsight ve HBase, hakkında daha fazla toolearn bakın:</span><span class="sxs-lookup"><span data-stu-id="e155b-269">toolearn more about HDInsight and HBase, see:</span></span>

* <span data-ttu-id="e155b-270">[Hdınsight'ta Apache HBase kullanmaya başlama][hdinsight-hbase-get-started]</span><span class="sxs-lookup"><span data-stu-id="e155b-270">[Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started]</span></span>
* <span data-ttu-id="e155b-271">[Hdınsight Hbase'e genel bakış][hdinsight-hbase-overview]</span><span class="sxs-lookup"><span data-stu-id="e155b-271">[HDInsight HBase overview][hdinsight-hbase-overview]</span></span>
* <span data-ttu-id="e155b-272">[Azure sanal ağında HBase kümeleri oluşturma][hdinsight-hbase-provision-vnet]</span><span class="sxs-lookup"><span data-stu-id="e155b-272">[Create HBase clusters in Azure Virtual Network][hdinsight-hbase-provision-vnet]</span></span>
* <span data-ttu-id="e155b-273">[HBase ile Twitter düşüncelerini gerçek zamanlı analiz][hdinsight-hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="e155b-273">[Analyze real-time Twitter sentiment with HBase][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="e155b-274">[Storm ve HBase hdınsight'ta (Hadoop) ile sensör verilerini analiz etme][hdinsight-sensor-data]</span><span class="sxs-lookup"><span data-stu-id="e155b-274">[Analyzing sensor data with Storm and HBase in HDInsight (Hadoop)][hdinsight-sensor-data]</span></span>

[hdinsight-hbase-geo-replication-vnet]: hdinsight-hbase-geo-replication-configure-vnets.md
[hdinsight-hbase-geo-replication-dns]: ../hdinsight-hbase-geo-replication-configure-VNet.md


[img-vnet-diagram]: ./media/hdinsight-hbase-geo-replication/HDInsight.HBase.Replication.Network.diagram.png

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started-linux.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[hdinsight-sensor-data]: hdinsight-storm-sensor-data-analysis.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
