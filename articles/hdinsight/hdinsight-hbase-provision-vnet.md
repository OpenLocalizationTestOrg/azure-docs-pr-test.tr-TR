---
title: "Sanal bir ağa - Azure HBase kümeleri oluşturma | Microsoft Docs"
description: "Azure Hdınsight'ta HBase kullanarak başlayın. Hdınsight HBase kümeleri Azure sanal ağ oluşturmayı öğrenin."
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
ms.openlocfilehash: 668bd494ce3274188af56cf7d6253cec7af9abbc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="create-hbase-clusters-on-hdinsight-in-azure-virtual-network"></a><span data-ttu-id="76212-104">Azure sanal ağındaki hdınsight'ta HBase kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="76212-104">Create HBase clusters on HDInsight in Azure Virtual Network</span></span>
<span data-ttu-id="76212-105">Azure Hdınsight HBase kümelerini oluşturmayı öğrenin bir [Azure Virtual Network][1].</span><span class="sxs-lookup"><span data-stu-id="76212-105">Learn how to create Azure HDInsight HBase clusters in an [Azure Virtual Network][1].</span></span>

<span data-ttu-id="76212-106">Uygulamalar HBase ile doğrudan iletişim kurabilmesi için sanal ağ tümleştirmesinin ile uygulamalarınızı aynı sanal ağ için HBase kümelerine dağıtılabilir.</span><span class="sxs-lookup"><span data-stu-id="76212-106">With virtual network integration, HBase clusters can be deployed to the same virtual network as your applications so that applications can communicate with HBase directly.</span></span> <span data-ttu-id="76212-107">Avantajlara şunlar dahildir:</span><span class="sxs-lookup"><span data-stu-id="76212-107">The benefits include:</span></span>

* <span data-ttu-id="76212-108">Doğrudan bağlantı HBase Java uzaktan yordam üzerinden iletişimi sağlayan HBase küme düğümleri için web uygulamasının (RPC) API'larını çağırma.</span><span class="sxs-lookup"><span data-stu-id="76212-108">Direct connectivity of the web application to the nodes of the HBase cluster, which enables communication via HBase Java remote procedure call (RPC) APIs.</span></span>
* <span data-ttu-id="76212-109">Geliştirilmiş performans trafiğinizi zorunluluğunu ortadan kaldırarak birden çok ağ geçitleri ve yük dengeleyicileri üzerine gidin.</span><span class="sxs-lookup"><span data-stu-id="76212-109">Improved performance by not having your traffic go over multiple gateways and load-balancers.</span></span>
* <span data-ttu-id="76212-110">Genel bir uç nokta sokmadan hassas bilgileri daha güvenli bir şekilde işleme yeteneği.</span><span class="sxs-lookup"><span data-stu-id="76212-110">The ability to process sensitive information in a more secure manner without exposing a public endpoint.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="76212-111">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="76212-111">Prerequisites</span></span>
<span data-ttu-id="76212-112">Bu öğreticiye başlamadan önce aşağıdaki öğelere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="76212-112">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="76212-113">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="76212-113">**An Azure subscription**.</span></span> <span data-ttu-id="76212-114">Bkz. [Azure ücretsiz deneme sürümü edinme](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="76212-114">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="76212-115">**Azure PowerShell içeren bir iş istasyonu**.</span><span class="sxs-lookup"><span data-stu-id="76212-115">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="76212-116">Bkz: [yükleme ve kullanma Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span><span class="sxs-lookup"><span data-stu-id="76212-116">See [Install and use Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span></span>

## <a name="create-hbase-cluster-into-virtual-network"></a><span data-ttu-id="76212-117">Sanal ağda HBase kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="76212-117">Create HBase cluster into virtual network</span></span>
<span data-ttu-id="76212-118">Bu bölümde, bir Azure sanal ağı kullanarak bağımlı Azure depolama hesabı ile Linux tabanlı HBase kümesi oluşturma bir [Azure Resource Manager şablonu](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="76212-118">In this section, you create a Linux-based HBase cluster with the dependent Azure Storage account in an Azure virtual network using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="76212-119">Diğer küme oluşturma yöntemleri ve ayarlarını anlama, bkz: [Hdınsight kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="76212-119">For other cluster creation methods and understanding the settings, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="76212-120">Hdınsight'ta Hadoop kümeleri oluşturmak için bir şablon kullanma hakkında daha fazla bilgi için bkz: [Azure Resource Manager şablonları kullanarak Hdınsight'ta oluşturmak Hadoop kümeleri](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span><span class="sxs-lookup"><span data-stu-id="76212-120">For more information about using a template to create Hadoop clusters in HDInsight, see [Create Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span></span>

> [!NOTE]
> <span data-ttu-id="76212-121">Bazı özellikler şablonuna sabit kodlanmış.</span><span class="sxs-lookup"><span data-stu-id="76212-121">Some properties are hard-coded into the template.</span></span> <span data-ttu-id="76212-122">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="76212-122">For example:</span></span>
>
> * <span data-ttu-id="76212-123">**Konum**: Doğu ABD 2</span><span class="sxs-lookup"><span data-stu-id="76212-123">**Location**: East US 2</span></span>
> * <span data-ttu-id="76212-124">**Küme sürümü**: 3.5</span><span class="sxs-lookup"><span data-stu-id="76212-124">**Cluster version**: 3.5</span></span>
> * <span data-ttu-id="76212-125">**Çalışan düğüm sayısı küme**: 2</span><span class="sxs-lookup"><span data-stu-id="76212-125">**Cluster worker node count**: 2</span></span>
> * <span data-ttu-id="76212-126">**Varsayılan depolama hesabı**: benzersiz bir dize</span><span class="sxs-lookup"><span data-stu-id="76212-126">**Default storage account**: a unique string</span></span>
> * <span data-ttu-id="76212-127">**Sanal ağ adı**: &lt;küme adı >-vnet</span><span class="sxs-lookup"><span data-stu-id="76212-127">**Virtual network name**: &lt;Cluster Name>-vnet</span></span>
> * <span data-ttu-id="76212-128">**Sanal ağ adres alanı**: 10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="76212-128">**Virtual network address space**: 10.0.0.0/16</span></span>
> * <span data-ttu-id="76212-129">**Alt ağ adı**: subnet1</span><span class="sxs-lookup"><span data-stu-id="76212-129">**Subnet name**: subnet1</span></span>
> * <span data-ttu-id="76212-130">**Alt ağ adres aralığı**: 10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="76212-130">**Subnet address range**: 10.0.0.0/24</span></span>
>
> <span data-ttu-id="76212-131">&lt;Küme adı > şablon kullanırken sağladığınız küme adı ile değiştirilir.</span><span class="sxs-lookup"><span data-stu-id="76212-131">&lt;Cluster Name> is replaced with the cluster name you provide when using the template.</span></span>
>
>

1. <span data-ttu-id="76212-132">Azure Portal'da bir şablonu açmak için aşağıdaki görüntüye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="76212-132">Click the following image to open the template in the Azure portal.</span></span> <span data-ttu-id="76212-133">Şablon bulunan [Azure hızlı başlangıç şablonlarını](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span><span class="sxs-lookup"><span data-stu-id="76212-133">The template is located in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span></span>

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-provision-vnet/deploy-to-azure.png" alt="Deploy to Azure"></a>
2. <span data-ttu-id="76212-134">Gelen **özel dağıtım** dikey penceresinde, aşağıdaki özellikleri girin:</span><span class="sxs-lookup"><span data-stu-id="76212-134">From the **Custom deployment** blade, enter the following properties:</span></span>

   * <span data-ttu-id="76212-135">**Abonelik**: Hdınsight küme, bağımlı depolama hesabı ve Azure sanal ağı oluşturmak için kullanılan Azure aboneliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="76212-135">**Subscription**: Select an Azure subscription used to create the HDInsight cluster, the dependent Storage account and the Azure virtual network.</span></span>
   * <span data-ttu-id="76212-136">**Kaynak grubu**: seçin **Yeni Oluştur**ve yeni bir kaynak grubu adı belirtin.</span><span class="sxs-lookup"><span data-stu-id="76212-136">**Resource group**: Select **Create new**, and specify a new resource group name.</span></span>
   * <span data-ttu-id="76212-137">**Konum**: Kaynak grubu için bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="76212-137">**Location**: Select a location for the resource group.</span></span>
   * <span data-ttu-id="76212-138">**ClusterName**: Oluşturulacak Hadoop kümesi için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="76212-138">**ClusterName**: Enter a name for the Hadoop cluster to be created.</span></span>
   * <span data-ttu-id="76212-139">**Küme oturum açma adı ve parolası**: Varsayılan oturum açma adı **admin** şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="76212-139">**Cluster login name and password**: The default login name is **admin**.</span></span>
   * <span data-ttu-id="76212-140">**SSH kullanıcı adı ve parolası**: Varsayılan kullanıcı adı **sshuser** şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="76212-140">**SSH username and password**: The default username is **sshuser**.</span></span>  <span data-ttu-id="76212-141">Bunu yeniden adlandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76212-141">You can rename it.</span></span>
   * <span data-ttu-id="76212-142">**Hüküm ve koşullar yukarıda belirtildiği ediyorum**: (seçin)</span><span class="sxs-lookup"><span data-stu-id="76212-142">**I agree to the terms and the conditions stated above**: (Select)</span></span>
3. <span data-ttu-id="76212-143">**Satın al**’a tıklayın.</span><span class="sxs-lookup"><span data-stu-id="76212-143">Click **Purchase**.</span></span> <span data-ttu-id="76212-144">Bir küme oluşturmak yaklaşık 20 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="76212-144">It takes about around 20 minutes to create a cluster.</span></span> <span data-ttu-id="76212-145">Küme oluşturulduktan sonra küme dikey penceresini açmak için portalda tıklatabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76212-145">Once the cluster is created, you can click the cluster blade in the portal to open it.</span></span>

<span data-ttu-id="76212-146">Öğreticiyi tamamladıktan sonra kümeyi silmek isteyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76212-146">After you complete the tutorial, you might want to delete the cluster.</span></span> <span data-ttu-id="76212-147">HDInsight ile, verileriniz Azure Storage’da depolanır, böylece kullanılmadığında bir kümeyi güvenle silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="76212-147">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span> <span data-ttu-id="76212-148">Ayrıca, kullanılmıyorken dahi HDInsight kümesi için sizden ücret kesilir.</span><span class="sxs-lookup"><span data-stu-id="76212-148">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="76212-149">Küme ücretleri depolama ücretlerinin birkaç katı olduğundan, kullanılmadığında kümelerin silinmesi mantıklı olandır.</span><span class="sxs-lookup"><span data-stu-id="76212-149">Since the charges for the cluster are many times more than the charges for storage, it makes economic sense to delete clusters when they are not in use.</span></span> <span data-ttu-id="76212-150">Küme silme ilişkin yönergeler için bkz: [yönetmek Hdınsight'ta Hadoop kümeleri Azure portalını kullanarak](hdinsight-administer-use-management-portal.md#delete-clusters).</span><span class="sxs-lookup"><span data-stu-id="76212-150">For the instructions of deleting a cluster, see [Manage Hadoop clusters in HDInsight by using the Azure portal](hdinsight-administer-use-management-portal.md#delete-clusters).</span></span>

<span data-ttu-id="76212-151">Yeni HBase kümesi ile çalışmaya başlamak için bulunan yordamları kullanabilirsiniz [hdınsight'ta Hadoop ile HBase kullanmaya başlamanıza](hdinsight-hbase-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="76212-151">To begin working with your new HBase cluster, you can use the procedures found in [Get started using HBase with Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started.md).</span></span>

## <a name="connect-to-the-hbase-cluster-using-hbase-java-rpc-apis"></a><span data-ttu-id="76212-152">HBase Java RPC API'lerini kullanarak HBase kümeye bağlanın</span><span class="sxs-lookup"><span data-stu-id="76212-152">Connect to the HBase cluster using HBase Java RPC APIs</span></span>
1. <span data-ttu-id="76212-153">Bir altyapı (ıaas) sanal makine olarak aynı Azure sanal ağı ve aynı alt ağ olarak oluşturun.</span><span class="sxs-lookup"><span data-stu-id="76212-153">Create an infrastructure as a service (IaaS) virtual machine into the same Azure virtual network and the same subnet.</span></span> <span data-ttu-id="76212-154">Yeni bir Iaas sanal makine oluşturma ile ilgili yönergeler için bkz: [bir sanal makine çalıştıran Windows Server oluşturma](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="76212-154">For instructions on creating a new IaaS virtual machine, see [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span></span> <span data-ttu-id="76212-155">Bu belgedeki adımları izleyerek, ağ yapılandırması için aşağıdaki değerleri kullanmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="76212-155">When following the steps in this document, you must use the following values for the Network configuration:</span></span>

   * <span data-ttu-id="76212-156">**Sanal ağ**: &lt;küme adı >-vnet</span><span class="sxs-lookup"><span data-stu-id="76212-156">**Virtual network**: &lt;Cluster name>-vnet</span></span>
   * <span data-ttu-id="76212-157">**Alt ağ**: subnet1</span><span class="sxs-lookup"><span data-stu-id="76212-157">**Subnet**: subnet1</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="76212-158">Değiştir &lt;küme adı > önceki adımlarda Hdınsight kümesi oluştururken, kullandığınız ada sahip.</span><span class="sxs-lookup"><span data-stu-id="76212-158">Replace &lt;Cluster name> with the name you used when creating the HDInsight cluster in previous steps.</span></span>
   >
   >

   <span data-ttu-id="76212-159">Bu değerleri kullanarak, sanal makineyi aynı sanal ağ ve alt Hdınsight kümesi olarak yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="76212-159">Using these values, the virtual machine is placed in the same virtual network and subnet as the HDInsight cluster.</span></span> <span data-ttu-id="76212-160">Bu yapılandırma doğrudan birbirleri ile iletişim kurmasına olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="76212-160">This configuration allows them to directly communicate with each other.</span></span> <span data-ttu-id="76212-161">Boş kenar düğümüne ile Hdınsight kümesi oluşturmak için bir yol yoktur.</span><span class="sxs-lookup"><span data-stu-id="76212-161">There is a way to create an HDInsight cluster with an empty edge node.</span></span> <span data-ttu-id="76212-162">Kenar düğümüne kümeyi yönetmek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="76212-162">The edge node can be used to manage the cluster.</span></span>  <span data-ttu-id="76212-163">Daha fazla bilgi için bkz: [Hdınsight'ta boş kenar düğümünü kullanmak](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="76212-163">For more information, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>

2. <span data-ttu-id="76212-164">Bir Java uygulaması HBase için uzaktan bağlanmak için kullanıldığında, tam etki alanı adı (FQDN) kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="76212-164">When using a Java application to connect to HBase remotely, you must use the fully qualified domain name (FQDN).</span></span> <span data-ttu-id="76212-165">Bunu belirlemek için HBase kümesi bağlantıya özgü DNS son ekini edinmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="76212-165">To determine this, you must get the connection-specific DNS suffix of the HBase cluster.</span></span> <span data-ttu-id="76212-166">Bunu yapmak için aşağıdaki yöntemlerden birini kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="76212-166">To do that, you can use one of the following methods:</span></span>

   * <span data-ttu-id="76212-167">Ambari arama yapmak için bir Web tarayıcısı kullanın:</span><span class="sxs-lookup"><span data-stu-id="76212-167">Use a Web browser to make an Ambari call:</span></span>

     <span data-ttu-id="76212-168">Https:// için Gözat&lt;ClusterName >.azurehdinsight.net/api/v1/clusters/&lt;ClusterName > / barındıran? minimal_response = true.</span><span class="sxs-lookup"><span data-stu-id="76212-168">Browse to https://&lt;ClusterName>.azurehdinsight.net/api/v1/clusters/&lt;ClusterName>/hosts?minimal_response=true.</span></span> <span data-ttu-id="76212-169">Bir JSON dosyası DNS sonekleri etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="76212-169">It turns a JSON file with the DNS suffixes.</span></span>
   * <span data-ttu-id="76212-170">Ambari Web sitesi kullanın:</span><span class="sxs-lookup"><span data-stu-id="76212-170">Use the Ambari website:</span></span>

     1. <span data-ttu-id="76212-171">Https:// için Gözat&lt;ClusterName >. azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="76212-171">Browse to  https://&lt;ClusterName>.azurehdinsight.net.</span></span>
     2. <span data-ttu-id="76212-172">Tıklatın **ana** üstteki menüden.</span><span class="sxs-lookup"><span data-stu-id="76212-172">Click **Hosts** from the top menu.</span></span>
   * <span data-ttu-id="76212-173">REST çağrı yapmak için Curl kullanın:</span><span class="sxs-lookup"><span data-stu-id="76212-173">Use Curl to make REST calls:</span></span>

    ```bash
        curl -u <username>:<password> -k https://<clustername>.azurehdinsight.net/ambari/api/v1/clusters/<clustername>.azurehdinsight.net/services/hbase/components/hbrest
    ```

     <span data-ttu-id="76212-174">Döndürülen JavaScript nesne gösterimi (JSON) verileri "host_name" girdiyi bulun.</span><span class="sxs-lookup"><span data-stu-id="76212-174">In the JavaScript Object Notation (JSON) data returned, find the "host_name" entry.</span></span> <span data-ttu-id="76212-175">Kümedeki düğümler için FQDN'yi içerir.</span><span class="sxs-lookup"><span data-stu-id="76212-175">It contains the FQDN for the nodes in the cluster.</span></span> <span data-ttu-id="76212-176">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="76212-176">For example:</span></span>

         ...
         "host_name": "wordkernode0.<clustername>.b1.cloudapp.net
         ...

     <span data-ttu-id="76212-177">Küme adı ile başlayan etki alanı adı DNS soneki bölümüdür.</span><span class="sxs-lookup"><span data-stu-id="76212-177">The portion of the domain name beginning with the cluster name is the DNS suffix.</span></span> <span data-ttu-id="76212-178">Örneğin, mycluster.b1.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="76212-178">For example, mycluster.b1.cloudapp.net.</span></span>
   * <span data-ttu-id="76212-179">Azure PowerShell kullanma</span><span class="sxs-lookup"><span data-stu-id="76212-179">Use Azure PowerShell</span></span>

     <span data-ttu-id="76212-180">Kaydetmek için aşağıdaki Azure PowerShell betiğini kullanın **Get-ClusterDetail** DNS soneki döndürmek için kullanılan işlev:</span><span class="sxs-lookup"><span data-stu-id="76212-180">Use the following Azure PowerShell script to register the **Get-ClusterDetail** function, which can be used to return the DNS suffix:</span></span>

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
            Displays information to facilitate an HDInsight cluster-to-cluster scenario within the same virtual network.
            .Description
            This command shows the following 4 properties of an HDInsight cluster:
            1. ZookeeperQuorum (supports only HBase type cluster)
                Shows the value of HBase property "hbase.zookeeper.quorum".
            2. ZookeeperClientPort (supports only HBase type cluster)
                Shows the value of HBase property "hbase.zookeeper.property.clientPort".
            3. HBaseRestServers (supports only HBase type cluster)
                Shows a list of host FQDNs that run the HBase REST server.
            4. FQDNSuffix (supports all cluster types)
                Shows the FQDN suffix of hosts in the cluster.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperQuorum
            This command shows the value of HBase property "hbase.zookeeper.quorum".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperClientPort
            This command shows the value of HBase property "hbase.zookeeper.property.clientPort".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName HBaseRestServers
            This command shows a list of host FQDNs that run the HBase REST server.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName FQDNSuffix
            This command shows the FQDN suffix of hosts in the cluster.
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

     <span data-ttu-id="76212-181">Azure PowerShell Betiği çalıştırdıktan sonra DNS son ekini kullanarak döndürmek için aşağıdaki komutu kullanın **Get-ClusterDetail** işlevi.</span><span class="sxs-lookup"><span data-stu-id="76212-181">After running the Azure PowerShell script, use the following command to return the DNS suffix by using the **Get-ClusterDetail** function.</span></span> <span data-ttu-id="76212-182">Bu komutu kullanırken Hdınsight HBase küme adı, yönetici adı ve yönetici parolasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="76212-182">Specify your HDInsight HBase cluster name, admin name, and admin password when using this command.</span></span>

    ```powershell
        Get-ClusterDetail -ClusterDnsName <yourclustername> -PropertyName FQDNSuffix -Username <clusteradmin> -Password <clusteradminpassword>
    ```

     <span data-ttu-id="76212-183">Bu komut, DNS son eki döndürür.</span><span class="sxs-lookup"><span data-stu-id="76212-183">This command returns the DNS suffix.</span></span> <span data-ttu-id="76212-184">Örneğin, **yourclustername.b4.internal.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="76212-184">For example, **yourclustername.b4.internal.cloudapp.net**.</span></span>


<!--
3.    Change the primary DNS suffix configuration of the virtual machine. This enables the virtual machine to automatically resolve the host name of the HBase cluster without explicit specification of the suffix. For example, the *workernode0* host name will be correctly resolved to workernode0 of the HBase cluster.

    To make the configuration change:

    1. RDP into the virtual machine.
    2. Open **Local Group Policy Editor**. The executable is gpedit.msc.
    3. Expand **Computer Configuration**, expand **Administrative Templates**, expand **Network**, and then click **DNS Client**.
    - Set **Primary DNS Suffix** to the value obtained in step 2:

        ![hdinsight.hbase.primary.dns.suffix][img-primary-dns-suffix]
    4. Click **OK**.
    5. Reboot the virtual machine.
-->

<span data-ttu-id="76212-185">Sanal makine HBase kümesi ile iletişim kurabildiğinden emin doğrulamak için komutunu kullanın `ping headnode0.<dns suffix>` sanal makineden.</span><span class="sxs-lookup"><span data-stu-id="76212-185">To verify that the virtual machine can communicate with the HBase cluster, use the command `ping headnode0.<dns suffix>` from the virtual machine.</span></span> <span data-ttu-id="76212-186">Örneğin, ping headnode0.mycluster.b1.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="76212-186">For example, ping headnode0.mycluster.b1.cloudapp.net.</span></span>

<span data-ttu-id="76212-187">Bu bilgiler bir Java uygulamasında kullanmak için adımları izleyebilirsiniz [Hdınsight (Hadoop) ile HBase kullanan Java uygulamaları oluşturmak için Maven kullanmak](hdinsight-hbase-build-java-maven.md) bir uygulama oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="76212-187">To use this information in a Java application, you can follow the steps in [Use Maven to build Java applications that use HBase with HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) to create an application.</span></span> <span data-ttu-id="76212-188">Uzak bir HBase sunucuya uygulama sağlamak için değiştirmek **hbase-site.xml** dosyası bu örnekte FQDN için Zookeeper kullanın.</span><span class="sxs-lookup"><span data-stu-id="76212-188">To have the application connect to a remote HBase server, modify the **hbase-site.xml** file in this example to use the FQDN for Zookeeper.</span></span> <span data-ttu-id="76212-189">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="76212-189">For example:</span></span>

    <property>
        <name>hbase.zookeeper.quorum</name>
        <value>zookeeper0.<dns suffix>,zookeeper1.<dns suffix>,zookeeper2.<dns suffix></value>
    </property>

> [!NOTE]
> <span data-ttu-id="76212-190">Azure ad çözümlemesi hakkında daha fazla bilgi için sanal ağlar kendi DNS sunucusunu kullanacak şekilde nasıl dahil olmak üzere, bkz: [adı çözümleme (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="76212-190">For more information about name resolution in Azure virtual networks, including how to use your own DNS server, see [Name Resolution (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="76212-191">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="76212-191">Next steps</span></span>
<span data-ttu-id="76212-192">Bu öğreticide, bir HBase kümesi oluşturmayı öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="76212-192">In this tutorial, you learned how to create an HBase cluster.</span></span> <span data-ttu-id="76212-193">Daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="76212-193">To learn more, see:</span></span>

* [<span data-ttu-id="76212-194">Hdınsight kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="76212-194">Get started with HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="76212-195">Hdınsight'ta boş kenar düğümleri kullanın</span><span class="sxs-lookup"><span data-stu-id="76212-195">Use empty edge nodes in HDInsight</span></span>](hdinsight-apps-use-edge-node.md)
* [<span data-ttu-id="76212-196">HDInsight’ta HBase çoğaltmayı yapılandırma</span><span class="sxs-lookup"><span data-stu-id="76212-196">Configure HBase replication in HDInsight</span></span>](hdinsight-hbase-replication.md)
* [<span data-ttu-id="76212-197">Hdınsight'ta Hadoop kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="76212-197">Create Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="76212-198">Hdınsight'ta Hadoop ile HBase kullanmaya başlamanıza</span><span class="sxs-lookup"><span data-stu-id="76212-198">Get started using HBase with Hadoop in HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
* [<span data-ttu-id="76212-199">Hdınsight'ta HBase ile twitter düşüncelerini çözümleme</span><span class="sxs-lookup"><span data-stu-id="76212-199">Analyze Twitter sentiment with HBase in HDInsight</span></span>](hdinsight-hbase-analyze-twitter-sentiment.md)
* <span data-ttu-id="76212-200">[Sanal ağ genel bakış][vnet-overview]</span><span class="sxs-lookup"><span data-stu-id="76212-200">[Virtual Network Overview][vnet-overview]</span></span>

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
[img-provision-cluster-page1]: ./media/hdinsight-hbase-provision-vnet/hbasewizard1.png "Yeni HBase kümesi ayrıntılarını sağlayın"
[img-provision-cluster-page5]: ./media/hdinsight-hbase-provision-vnet/hbasewizard5.png "Betik eylemi bir HBase kümesi özelleştirmek için kullanın"

[azure-preview-portal]: https://portal.azure.com
