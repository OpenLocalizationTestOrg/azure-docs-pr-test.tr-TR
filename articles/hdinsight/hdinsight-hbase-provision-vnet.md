---
title: "aaaCreate HBase kümeleri sanal bir ağa - Azure | Microsoft Docs"
description: "Azure Hdınsight'ta HBase kullanarak başlayın. Azure sanal ağ üzerinde nasıl toocreate Hdınsight HBase kümeleri hakkında bilgi edinin."
keywords: 
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 8de8e446-f818-4e61-8fad-e9d38421e80d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 097338a5a650bb607a9f6f9ddb59bb88d098b56f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hbase-clusters-on-hdinsight-in-azure-virtual-network"></a><span data-ttu-id="78cf5-104">Azure sanal ağındaki hdınsight'ta HBase kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="78cf5-104">Create HBase clusters on HDInsight in Azure Virtual Network</span></span>
<span data-ttu-id="78cf5-105">İçinde nasıl toocreate Azure Hdınsight HBase kümeleri öğrenin bir [Azure Virtual Network][1].</span><span class="sxs-lookup"><span data-stu-id="78cf5-105">Learn how toocreate Azure HDInsight HBase clusters in an [Azure Virtual Network][1].</span></span>

<span data-ttu-id="78cf5-106">Sanal ağ tümleştirmesinin ile HBase kümeleri aynı sanal ağ, uygulamalarınızın böylece dağıtılan toohello olabilir uygulamalar HBase ile doğrudan iletişim kurabilir.</span><span class="sxs-lookup"><span data-stu-id="78cf5-106">With virtual network integration, HBase clusters can be deployed toohello same virtual network as your applications so that applications can communicate with HBase directly.</span></span> <span data-ttu-id="78cf5-107">Merhaba yararlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="78cf5-107">hello benefits include:</span></span>

* <span data-ttu-id="78cf5-108">Doğrudan bağlantı düğümlerinin hello web uygulama toohello HBase Java uzaktan yordam üzerinden iletişimi sağlayan hello HBase kümesi (RPC) API'larını çağırma.</span><span class="sxs-lookup"><span data-stu-id="78cf5-108">Direct connectivity of hello web application toohello nodes of hello HBase cluster, which enables communication via HBase Java remote procedure call (RPC) APIs.</span></span>
* <span data-ttu-id="78cf5-109">Geliştirilmiş performans trafiğinizi zorunluluğunu ortadan kaldırarak birden çok ağ geçitleri ve yük dengeleyicileri üzerine gidin.</span><span class="sxs-lookup"><span data-stu-id="78cf5-109">Improved performance by not having your traffic go over multiple gateways and load-balancers.</span></span>
* <span data-ttu-id="78cf5-110">Merhaba özelliği tooprocess hassas bilgileri genel bir uç nokta gösterme olmadan daha güvenli bir şekilde.</span><span class="sxs-lookup"><span data-stu-id="78cf5-110">hello ability tooprocess sensitive information in a more secure manner without exposing a public endpoint.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="78cf5-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="78cf5-111">Prerequisites</span></span>
<span data-ttu-id="78cf5-112">Bu öğreticiye başlamadan önce aşağıdaki öğelerindeki hello sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="78cf5-112">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="78cf5-113">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="78cf5-113">**An Azure subscription**.</span></span> <span data-ttu-id="78cf5-114">Bkz. [Azure ücretsiz deneme sürümü edinme](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="78cf5-114">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="78cf5-115">**Azure PowerShell içeren bir iş istasyonu**.</span><span class="sxs-lookup"><span data-stu-id="78cf5-115">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="78cf5-116">Bkz: [yükleme ve kullanma Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span><span class="sxs-lookup"><span data-stu-id="78cf5-116">See [Install and use Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span></span>

## <a name="create-hbase-cluster-into-virtual-network"></a><span data-ttu-id="78cf5-117">Sanal ağda HBase kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="78cf5-117">Create HBase cluster into virtual network</span></span>
<span data-ttu-id="78cf5-118">Bu bölümde, bir Azure sanal ağı kullanarak hello bağımlı Azure depolama hesabıyla Linux tabanlı HBase kümesi oluşturma bir [Azure Resource Manager şablonu](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="78cf5-118">In this section, you create a Linux-based HBase cluster with hello dependent Azure Storage account in an Azure virtual network using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="78cf5-119">Diğer küme oluşturma yöntemleri ve hello ayarlarını anlama, bkz: [Hdınsight kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="78cf5-119">For other cluster creation methods and understanding hello settings, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="78cf5-120">Hdınsight'ta bir şablon toocreate Hadoop kullanma hakkında daha fazla bilgi kümeleri için bkz: [Azure Resource Manager şablonları kullanarak Hdınsight'ta oluşturmak Hadoop kümeleri](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span><span class="sxs-lookup"><span data-stu-id="78cf5-120">For more information about using a template toocreate Hadoop clusters in HDInsight, see [Create Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span></span>

> [!NOTE]
> <span data-ttu-id="78cf5-121">Bazı özellikler hello şablonuna sabit kodlanmış.</span><span class="sxs-lookup"><span data-stu-id="78cf5-121">Some properties are hard-coded into hello template.</span></span> <span data-ttu-id="78cf5-122">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="78cf5-122">For example:</span></span>
>
> * <span data-ttu-id="78cf5-123">**Konum**: Doğu ABD 2</span><span class="sxs-lookup"><span data-stu-id="78cf5-123">**Location**: East US 2</span></span>
> * <span data-ttu-id="78cf5-124">**Küme sürümü**: 3.5</span><span class="sxs-lookup"><span data-stu-id="78cf5-124">**Cluster version**: 3.5</span></span>
> * <span data-ttu-id="78cf5-125">**Çalışan düğüm sayısı küme**: 2</span><span class="sxs-lookup"><span data-stu-id="78cf5-125">**Cluster worker node count**: 2</span></span>
> * <span data-ttu-id="78cf5-126">**Varsayılan depolama hesabı**: benzersiz bir dize</span><span class="sxs-lookup"><span data-stu-id="78cf5-126">**Default storage account**: a unique string</span></span>
> * <span data-ttu-id="78cf5-127">**Sanal ağ adı**: &lt;küme adı >-vnet</span><span class="sxs-lookup"><span data-stu-id="78cf5-127">**Virtual network name**: &lt;Cluster Name>-vnet</span></span>
> * <span data-ttu-id="78cf5-128">**Sanal ağ adres alanı**: 10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="78cf5-128">**Virtual network address space**: 10.0.0.0/16</span></span>
> * <span data-ttu-id="78cf5-129">**Alt ağ adı**: subnet1</span><span class="sxs-lookup"><span data-stu-id="78cf5-129">**Subnet name**: subnet1</span></span>
> * <span data-ttu-id="78cf5-130">**Alt ağ adres aralığı**: 10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="78cf5-130">**Subnet address range**: 10.0.0.0/24</span></span>
>
> <span data-ttu-id="78cf5-131">&lt;Küme adı > merhaba şablon kullanırken sağladığınız hello küme adı ile değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="78cf5-131">&lt;Cluster Name> is replaced with hello cluster name you provide when using hello template.</span></span>
>
>

1. <span data-ttu-id="78cf5-132">Görüntü tooopen hello hello Azure portal şablonda aşağıdaki hello'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="78cf5-132">Click hello following image tooopen hello template in hello Azure portal.</span></span> <span data-ttu-id="78cf5-133">Merhaba şablon bulunduğu [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span><span class="sxs-lookup"><span data-stu-id="78cf5-133">hello template is located in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span></span>

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-provision-vnet/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. <span data-ttu-id="78cf5-134">Merhaba gelen **özel dağıtım** dikey penceresinde, aşağıdaki özelliklere hello girin:</span><span class="sxs-lookup"><span data-stu-id="78cf5-134">From hello **Custom deployment** blade, enter hello following properties:</span></span>

   * <span data-ttu-id="78cf5-135">**Abonelik**: Azure aboneliği kullanılan toocreate hello Hdınsight kümesi seçin, bağımlı depolama hesabı hello ve Azure sanal ağı hello.</span><span class="sxs-lookup"><span data-stu-id="78cf5-135">**Subscription**: Select an Azure subscription used toocreate hello HDInsight cluster, hello dependent Storage account and hello Azure virtual network.</span></span>
   * <span data-ttu-id="78cf5-136">**Kaynak grubu**: seçin **Yeni Oluştur**ve yeni bir kaynak grubu adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="78cf5-136">**Resource group**: Select **Create new**, and specify a new resource group name.</span></span>
   * <span data-ttu-id="78cf5-137">**Konum**: hello kaynak grubu için bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="78cf5-137">**Location**: Select a location for hello resource group.</span></span>
   * <span data-ttu-id="78cf5-138">**ClusterName**: Merhaba Hadoop küme toobe oluşturulan için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="78cf5-138">**ClusterName**: Enter a name for hello Hadoop cluster toobe created.</span></span>
   * <span data-ttu-id="78cf5-139">**Küme oturum açma adı ve parola**: hello varsayılan oturum açma adı **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="78cf5-139">**Cluster login name and password**: hello default login name is **admin**.</span></span>
   * <span data-ttu-id="78cf5-140">**SSH kullanıcı adı ve parola**: hello varsayılan kullanıcı adı **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="78cf5-140">**SSH username and password**: hello default username is **sshuser**.</span></span>  <span data-ttu-id="78cf5-141">Bunu yeniden adlandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78cf5-141">You can rename it.</span></span>
   * <span data-ttu-id="78cf5-142">**Toohello hüküm ve yukarıda belirtilen hello koşullarını kabul ediyorum**: (seçin)</span><span class="sxs-lookup"><span data-stu-id="78cf5-142">**I agree toohello terms and hello conditions stated above**: (Select)</span></span>
3. <span data-ttu-id="78cf5-143">**Satın al**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="78cf5-143">Click **Purchase**.</span></span> <span data-ttu-id="78cf5-144">Bir küme hakkında toocreate yaklaşık 20 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="78cf5-144">It takes about around 20 minutes toocreate a cluster.</span></span> <span data-ttu-id="78cf5-145">Merhaba Küme oluşturulduktan sonra hello küme dikey penceresinde hello portal tooopen tıklatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78cf5-145">Once hello cluster is created, you can click hello cluster blade in hello portal tooopen it.</span></span>

<span data-ttu-id="78cf5-146">Merhaba öğreticiyi tamamladıktan sonra toodelete hello küme isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78cf5-146">After you complete hello tutorial, you might want toodelete hello cluster.</span></span> <span data-ttu-id="78cf5-147">HDInsight ile, verileriniz Azure Storage’da depolanır, böylece kullanılmadığında bir kümeyi güvenle silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78cf5-147">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span> <span data-ttu-id="78cf5-148">Ayrıca, kullanılmıyorken dahi HDInsight kümesi için sizden ücret kesilir.</span><span class="sxs-lookup"><span data-stu-id="78cf5-148">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="78cf5-149">Merhaba ücretleri hello küme için hello ücretleri depolama birkaç katı olduğundan, bunlar kullanımda olmadığında ekonomik toodelete kümeleri mantıklıdır.</span><span class="sxs-lookup"><span data-stu-id="78cf5-149">Since hello charges for hello cluster are many times more than hello charges for storage, it makes economic sense toodelete clusters when they are not in use.</span></span> <span data-ttu-id="78cf5-150">Bir küme silme hello yönergeler için bkz: [kullanarak yönetmek Hadoop kümeleri hdınsight'ta Azure portalına hello](hdinsight-administer-use-management-portal.md#delete-clusters).</span><span class="sxs-lookup"><span data-stu-id="78cf5-150">For hello instructions of deleting a cluster, see [Manage Hadoop clusters in HDInsight by using hello Azure portal](hdinsight-administer-use-management-portal.md#delete-clusters).</span></span>

<span data-ttu-id="78cf5-151">Yeni, HBase kümesi ile çalışma toobegin bulunan hello yordamları kullanabilirsiniz [hdınsight'ta Hadoop ile HBase kullanmaya başlamanıza](hdinsight-hbase-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="78cf5-151">toobegin working with your new HBase cluster, you can use hello procedures found in [Get started using HBase with Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started.md).</span></span>

## <a name="connect-toohello-hbase-cluster-using-hbase-java-rpc-apis"></a><span data-ttu-id="78cf5-152">Toohello HBase kümesi HBase Java RPC API'lerini kullanarak bağlan</span><span class="sxs-lookup"><span data-stu-id="78cf5-152">Connect toohello HBase cluster using HBase Java RPC APIs</span></span>
1. <span data-ttu-id="78cf5-153">Bir hizmet (Iaas) sanal makineye bir altyapı oluşturmanızı hello aynı Azure sanal ağı ve hello aynı alt ağ.</span><span class="sxs-lookup"><span data-stu-id="78cf5-153">Create an infrastructure as a service (IaaS) virtual machine into hello same Azure virtual network and hello same subnet.</span></span> <span data-ttu-id="78cf5-154">Yeni bir Iaas sanal makine oluşturma ile ilgili yönergeler için bkz: [bir sanal makine çalıştıran Windows Server oluşturma](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="78cf5-154">For instructions on creating a new IaaS virtual machine, see [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span></span> <span data-ttu-id="78cf5-155">Bu belgedeki Hello adımları izleyerek, hello ağ yapılandırması için değerleri aşağıdaki hello kullanmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="78cf5-155">When following hello steps in this document, you must use hello following values for hello Network configuration:</span></span>

   * <span data-ttu-id="78cf5-156">**Sanal ağ**: &lt;küme adı >-vnet</span><span class="sxs-lookup"><span data-stu-id="78cf5-156">**Virtual network**: &lt;Cluster name>-vnet</span></span>
   * <span data-ttu-id="78cf5-157">**Alt ağ**: subnet1</span><span class="sxs-lookup"><span data-stu-id="78cf5-157">**Subnet**: subnet1</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="78cf5-158">Değiştir &lt;küme adı > merhaba adıyla önceki adımlarda hello Hdınsight kümesi oluştururken kullandığınız.</span><span class="sxs-lookup"><span data-stu-id="78cf5-158">Replace &lt;Cluster name> with hello name you used when creating hello HDInsight cluster in previous steps.</span></span>
   >
   >

   <span data-ttu-id="78cf5-159">Bu değerleri kullanarak hello sanal makinenin hello aynı yerleştirildiğinden sanal ağ ve alt hello Hdınsight kümesi olarak.</span><span class="sxs-lookup"><span data-stu-id="78cf5-159">Using these values, hello virtual machine is placed in hello same virtual network and subnet as hello HDInsight cluster.</span></span> <span data-ttu-id="78cf5-160">Bu yapılandırma veren toodirectly birbirleri ile iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="78cf5-160">This configuration allows them toodirectly communicate with each other.</span></span> <span data-ttu-id="78cf5-161">Bir Hdınsight kümesini boş kenar düğümüne bir şekilde toocreate yoktur.</span><span class="sxs-lookup"><span data-stu-id="78cf5-161">There is a way toocreate an HDInsight cluster with an empty edge node.</span></span> <span data-ttu-id="78cf5-162">Merhaba kenar düğümüne kullanılan toomanage hello kümesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="78cf5-162">hello edge node can be used toomanage hello cluster.</span></span>  <span data-ttu-id="78cf5-163">Daha fazla bilgi için bkz: [Hdınsight'ta boş kenar düğümünü kullanmak](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="78cf5-163">For more information, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>

2. <span data-ttu-id="78cf5-164">Java uygulama tooconnect tooHBase uzaktan kullanılırken hello tam etki alanı adı (FQDN) kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="78cf5-164">When using a Java application tooconnect tooHBase remotely, you must use hello fully qualified domain name (FQDN).</span></span> <span data-ttu-id="78cf5-165">toodetermine bunu hello bağlantıya özgü DNS soneki hello HBase kümesi almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="78cf5-165">toodetermine this, you must get hello connection-specific DNS suffix of hello HBase cluster.</span></span> <span data-ttu-id="78cf5-166">toodo: yöntemler aşağıdaki hello birini kullanabilirsiniz</span><span class="sxs-lookup"><span data-stu-id="78cf5-166">toodo that, you can use one of hello following methods:</span></span>

   * <span data-ttu-id="78cf5-167">Bir Web tarayıcısı toomake Ambari çağrısı kullanın:</span><span class="sxs-lookup"><span data-stu-id="78cf5-167">Use a Web browser toomake an Ambari call:</span></span>

     <span data-ttu-id="78cf5-168">Toohttps göz atın: / /&lt;ClusterName >.azurehdinsight.net/api/v1/clusters/&lt;ClusterName > / barındıran? minimal_response = true.</span><span class="sxs-lookup"><span data-stu-id="78cf5-168">Browse toohttps://&lt;ClusterName>.azurehdinsight.net/api/v1/clusters/&lt;ClusterName>/hosts?minimal_response=true.</span></span> <span data-ttu-id="78cf5-169">Bir JSON dosyası hello DNS sonekleri etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="78cf5-169">It turns a JSON file with hello DNS suffixes.</span></span>
   * <span data-ttu-id="78cf5-170">Merhaba Ambari Web sitesi kullanın:</span><span class="sxs-lookup"><span data-stu-id="78cf5-170">Use hello Ambari website:</span></span>

     1. <span data-ttu-id="78cf5-171">Çok Gözat https://&lt;ClusterName >. azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="78cf5-171">Browse too https://&lt;ClusterName>.azurehdinsight.net.</span></span>
     2. <span data-ttu-id="78cf5-172">Tıklatın **ana** hello üst menüsünde.</span><span class="sxs-lookup"><span data-stu-id="78cf5-172">Click **Hosts** from hello top menu.</span></span>
   * <span data-ttu-id="78cf5-173">Curl toomake REST çağrılarını kullanın:</span><span class="sxs-lookup"><span data-stu-id="78cf5-173">Use Curl toomake REST calls:</span></span>

    ```bash
        curl -u <username>:<password> -k https://<clustername>.azurehdinsight.net/ambari/api/v1/clusters/<clustername>.azurehdinsight.net/services/hbase/components/hbrest
    ```

     <span data-ttu-id="78cf5-174">Merhaba "host_name" girişini bulun, Hello JavaScript nesne gösterimi (JSON) veri döndürdü.</span><span class="sxs-lookup"><span data-stu-id="78cf5-174">In hello JavaScript Object Notation (JSON) data returned, find hello "host_name" entry.</span></span> <span data-ttu-id="78cf5-175">Merhaba düğümler hello küme için FQDN hello içerir.</span><span class="sxs-lookup"><span data-stu-id="78cf5-175">It contains hello FQDN for hello nodes in hello cluster.</span></span> <span data-ttu-id="78cf5-176">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="78cf5-176">For example:</span></span>

         ...
         "host_name": "wordkernode0.<clustername>.b1.cloudapp.net
         ...

     <span data-ttu-id="78cf5-177">Merhaba hello küme adı ile başlayan hello etki alanı adı hello DNS soneki bölümüdür.</span><span class="sxs-lookup"><span data-stu-id="78cf5-177">hello portion of hello domain name beginning with hello cluster name is hello DNS suffix.</span></span> <span data-ttu-id="78cf5-178">Örneğin, mycluster.b1.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="78cf5-178">For example, mycluster.b1.cloudapp.net.</span></span>
   * <span data-ttu-id="78cf5-179">Azure PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="78cf5-179">Use Azure PowerShell</span></span>

     <span data-ttu-id="78cf5-180">Azure PowerShell komut dosyası tooregister hello aşağıdaki kullanım hello **Get-ClusterDetail** kullanılan tooreturn hello DNS soneki olabilir işlevi:</span><span class="sxs-lookup"><span data-stu-id="78cf5-180">Use hello following Azure PowerShell script tooregister hello **Get-ClusterDetail** function, which can be used tooreturn hello DNS suffix:</span></span>

    ```powershell
        function Get-ClusterDetail(
            [String]
            [Parameter( Position=0, Mandatory=$true )]
            $ClusterDnsName,
            [String]
            [Parameter( Position=1, Mandatory=$true )]
            $Username,
            [String]
            [Parameter( Position=2, Mandatory=$true )]
            $Password,
            [String]
            [Parameter( Position=3, Mandatory=$true )]
            $PropertyName
            )
        {
        <#
            .SYNOPSIS
            Displays information toofacilitate an HDInsight cluster-to-cluster scenario within hello same virtual network.
            .Description
            This command shows hello following 4 properties of an HDInsight cluster:
            1. ZookeeperQuorum (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.quorum".
            2. ZookeeperClientPort (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            3. HBaseRestServers (supports only HBase type cluster)
                Shows a list of host FQDNs that run hello HBase REST server.
            4. FQDNSuffix (supports all cluster types)
                Shows hello FQDN suffix of hosts in hello cluster.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperQuorum
            This command shows hello value of HBase property "hbase.zookeeper.quorum".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperClientPort
            This command shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName HBaseRestServers
            This command shows a list of host FQDNs that run hello HBase REST server.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName FQDNSuffix
            This command shows hello FQDN suffix of hosts in hello cluster.
        #>

            $DnsSuffix = ".azurehdinsight.net"

            $ClusterFQDN = $ClusterDnsName + $DnsSuffix
            $webclient = new-object System.Net.WebClient
            $webclient.Credentials = new-object System.Net.NetworkCredential($Username, $Password)

            if($PropertyName -eq "ZookeeperQuorum")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.quorum"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.quorum'
            }
            if($PropertyName -eq "ZookeeperClientPort")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.property.clientPort"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.property.clientPort'
            }
            if($PropertyName -eq "HBaseRestServers")
            {
                $Url1 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.rest.port"
                $Response1 = $webclient.DownloadString($Url1)
                $JsonObject1 = $Response1 | ConvertFrom-Json
                $PortNumber = $JsonObject1.items[0].properties.'hbase.rest.port'

                $Url2 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/hbase/components/hbrest"
                $Response2 = $webclient.DownloadString($Url2)
                $JsonObject2 = $Response2 | ConvertFrom-Json
                foreach ($host_component in $JsonObject2.host_components)
                {
                    $ConnectionString = $host_component.HostRoles.host_name + ":" + $PortNumber
                    Write-host $ConnectionString
                }
            }
            if($PropertyName -eq "FQDNSuffix")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/YARN/components/RESOURCEMANAGER"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                $FQDN = $JsonObject.host_components[0].HostRoles.host_name
                $pos = $FQDN.IndexOf(".")
                $Suffix = $FQDN.Substring($pos + 1)
                Write-host $Suffix
            }
        }
    ```

     <span data-ttu-id="78cf5-181">Çalışan hello Azure PowerShell Betiği sonra kullanım hello şu komutu tooreturn hello DNS soneki hello kullanarak **Get-ClusterDetail** işlevi.</span><span class="sxs-lookup"><span data-stu-id="78cf5-181">After running hello Azure PowerShell script, use hello following command tooreturn hello DNS suffix by using hello **Get-ClusterDetail** function.</span></span> <span data-ttu-id="78cf5-182">Bu komutu kullanırken Hdınsight HBase küme adı, yönetici adı ve yönetici parolasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="78cf5-182">Specify your HDInsight HBase cluster name, admin name, and admin password when using this command.</span></span>

    ```powershell
        Get-ClusterDetail -ClusterDnsName <yourclustername> -PropertyName FQDNSuffix -Username <clusteradmin> -Password <clusteradminpassword>
    ```

     <span data-ttu-id="78cf5-183">Bu komut hello DNS soneki döndürür.</span><span class="sxs-lookup"><span data-stu-id="78cf5-183">This command returns hello DNS suffix.</span></span> <span data-ttu-id="78cf5-184">Örneğin, **yourclustername.b4.internal.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="78cf5-184">For example, **yourclustername.b4.internal.cloudapp.net**.</span></span>


<!--
3.    Change hello primary DNS suffix configuration of hello virtual machine. This enables hello virtual machine tooautomatically resolve hello host name of hello HBase cluster without explicit specification of hello suffix. For example, hello *workernode0* host name will be correctly resolved tooworkernode0 of hello HBase cluster.

    toomake hello configuration change:

    1. RDP into hello virtual machine.
    2. Open **Local Group Policy Editor**. hello executable is gpedit.msc.
    3. Expand **Computer Configuration**, expand **Administrative Templates**, expand **Network**, and then click **DNS Client**.
    - Set **Primary DNS Suffix** toohello value obtained in step 2:

        ![hdinsight.hbase.primary.dns.suffix][img-primary-dns-suffix]
    4. Click **OK**.
    5. Reboot hello virtual machine.
-->

<span data-ttu-id="78cf5-185">sanal makine hello tooverify HBase kümesi hello ile iletişim kurmak, hello komutunu `ping headnode0.<dns suffix>` hello sanal makineden.</span><span class="sxs-lookup"><span data-stu-id="78cf5-185">tooverify that hello virtual machine can communicate with hello HBase cluster, use hello command `ping headnode0.<dns suffix>` from hello virtual machine.</span></span> <span data-ttu-id="78cf5-186">Örneğin, ping headnode0.mycluster.b1.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="78cf5-186">For example, ping headnode0.mycluster.b1.cloudapp.net.</span></span>

<span data-ttu-id="78cf5-187">toouse bu bilgileri bir Java uygulamasında hello adımları izleyebilirsiniz [Hdınsight (Hadoop) ile HBase kullanan Maven kullanmak toobuild Java uygulamaları](hdinsight-hbase-build-java-maven.md) toocreate bir uygulama.</span><span class="sxs-lookup"><span data-stu-id="78cf5-187">toouse this information in a Java application, you can follow hello steps in [Use Maven toobuild Java applications that use HBase with HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) toocreate an application.</span></span> <span data-ttu-id="78cf5-188">toohave Merhaba uygulaması tooa uzak HBase sunucusuna bağlanma, hello Değiştir **hbase-site.xml** Zookeeper Bu örnek toouse hello FQDN dosyasında.</span><span class="sxs-lookup"><span data-stu-id="78cf5-188">toohave hello application connect tooa remote HBase server, modify hello **hbase-site.xml** file in this example toouse hello FQDN for Zookeeper.</span></span> <span data-ttu-id="78cf5-189">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="78cf5-189">For example:</span></span>

    <property>
        <name>hbase.zookeeper.quorum</name>
        <value>zookeeper0.<dns suffix>,zookeeper1.<dns suffix>,zookeeper2.<dns suffix></value>
    </property>

> [!NOTE]
> <span data-ttu-id="78cf5-190">Azure sanal ağlar, ad çözümleme hakkında daha fazla bilgi için nasıl dahil toouse kendi DNS sunucusu bkz [adı çözümleme (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="78cf5-190">For more information about name resolution in Azure virtual networks, including how toouse your own DNS server, see [Name Resolution (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="78cf5-191">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="78cf5-191">Next steps</span></span>
<span data-ttu-id="78cf5-192">Bu öğreticide, nasıl öğrenilen toocreate bir HBase kümesi.</span><span class="sxs-lookup"><span data-stu-id="78cf5-192">In this tutorial, you learned how toocreate an HBase cluster.</span></span> <span data-ttu-id="78cf5-193">toolearn daha bakın:</span><span class="sxs-lookup"><span data-stu-id="78cf5-193">toolearn more, see:</span></span>

* [<span data-ttu-id="78cf5-194">Hdınsight kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="78cf5-194">Get started with HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="78cf5-195">Hdınsight'ta boş kenar düğümleri kullanın</span><span class="sxs-lookup"><span data-stu-id="78cf5-195">Use empty edge nodes in HDInsight</span></span>](hdinsight-apps-use-edge-node.md)
* [<span data-ttu-id="78cf5-196">HDInsight’ta HBase çoğaltmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="78cf5-196">Configure HBase replication in HDInsight</span></span>](hdinsight-hbase-replication.md)
* [<span data-ttu-id="78cf5-197">Hdınsight'ta Hadoop kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="78cf5-197">Create Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="78cf5-198">Hdınsight'ta Hadoop ile HBase kullanmaya başlamanıza</span><span class="sxs-lookup"><span data-stu-id="78cf5-198">Get started using HBase with Hadoop in HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
* [<span data-ttu-id="78cf5-199">Hdınsight'ta HBase ile twitter düşüncelerini çözümleme</span><span class="sxs-lookup"><span data-stu-id="78cf5-199">Analyze Twitter sentiment with HBase in HDInsight</span></span>](hdinsight-hbase-analyze-twitter-sentiment.md)
* <span data-ttu-id="78cf5-200">[Sanal ağ genel bakış][vnet-overview]</span><span class="sxs-lookup"><span data-stu-id="78cf5-200">[Virtual Network Overview][vnet-overview]</span></span>

[1]: http://azure.microsoft.com/services/virtual-network/
[2]: http://technet.microsoft.com/library/ee176961.aspx
[3]: http://technet.microsoft.com/library/hh847889.aspx

[hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[vnet-overview]: ../virtual-network/virtual-networks-overview.md
[vm-create]: ../virtual-machines/virtual-machines-windows-hero-tutorial.md

[azure-portal]: https://portal.azure.com
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx


[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter


[powershell-install]: /powershell/azureps-cmdlets-docs


[hdinsight-customize-cluster]: hdinsight-hadoop-customize-cluster.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]: ../hdinsight-hadoop-use-blob-storage.md#powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-hbase-replication-dns]: hdinsight-hbase-geo-replication-configure-DNS.md

[img-dns-surffix]: ./media/hdinsight-hbase-provision-vnet/DNSSuffix.png
[img-primary-dns-suffix]: ./media/hdinsight-hbase-provision-vnet/PrimaryDNSSuffix.png
[img-provision-cluster-page1]: ./media/hdinsight-hbase-provision-vnet/hbasewizard1.png "Hello yeni HBase kümesi ayrıntılarını sağlayın"
[img-provision-cluster-page5]: ./media/hdinsight-hbase-provision-vnet/hbasewizard5.png "Betik eylemi toocustomize bir HBase kümesi kullanın"

[azure-preview-portal]: https://portal.azure.com
