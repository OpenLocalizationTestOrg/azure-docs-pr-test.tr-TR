---
title: "Hdınsight'ta - Azure Hadoop kümeleri üzerinde boş kenar düğümünü kullanmak | Microsoft Docs"
description: "Nasıl bir istemci olarak kullanılabilir ve ardından test/ana Hdınsight uygulamalarınızı Hdınsight kümesi için bir boş kenar düğümüne eklenir."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: mumian
tags: azure-portal
documentationcenter: 
ms.assetid: cdc7d1b4-15d7-4d4d-a13f-c7d3a694b4fb
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jgao
ms.openlocfilehash: e21dabcc6999b1f1047d334e782f723d0c03c2cb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/29/2017
---
# <a name="use-empty-edge-nodes-on-hadoop-clusters-in-hdinsight"></a><span data-ttu-id="f215d-103">Hdınsight'ta Hadoop kümeleri üzerinde boş kenar düğümleri kullanın</span><span class="sxs-lookup"><span data-stu-id="f215d-103">Use empty edge nodes on Hadoop clusters in HDInsight</span></span>

<span data-ttu-id="f215d-104">Bir Hdınsight kümesine bir boş kenar düğümüne eklemeyi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="f215d-104">Learn how to add an empty edge node to an HDInsight cluster.</span></span> <span data-ttu-id="f215d-105">Bir boş kenar düğümüne yüklenir ve yapılandırılır. headnodes olduğu gibi aynı istemci araçları ile ancak çalışan hiçbir Hadoop Hizmetleri Linux sanal makine var.</span><span class="sxs-lookup"><span data-stu-id="f215d-105">An empty edge node is a Linux virtual machine with the same client tools installed and configured as in the headnodes, but with no Hadoop services running.</span></span> <span data-ttu-id="f215d-106">Kenar düğümüne küme erişmek, istemci uygulamalarınızı test etme ve istemci uygulamalarını barındırmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f215d-106">You can use the edge node for accessing the cluster, testing your client applications, and hosting your client applications.</span></span> 

<span data-ttu-id="f215d-107">Var olan Hdınsight kümesine, Küme oluşturduğunuzda, yeni bir kümeye boş kenar düğümüne ekleyin.</span><span class="sxs-lookup"><span data-stu-id="f215d-107">You can add an empty edge node to an existing HDInsight cluster, to a new cluster when you create the cluster.</span></span> <span data-ttu-id="f215d-108">Bir boş kenar düğümüne ekleyerek yapılır Azure Resource Manager şablonu kullanarak.</span><span class="sxs-lookup"><span data-stu-id="f215d-108">Adding an empty edge node is done using Azure Resource Manager template.</span></span>  <span data-ttu-id="f215d-109">Aşağıdaki örnek nasıl yapıldığını gösteren bir şablon kullanarak:</span><span class="sxs-lookup"><span data-stu-id="f215d-109">The following sample demonstrates how it is done using a template:</span></span>

    "resources": [
        {
            "name": "[concat(parameters('clusterName'),'/', variables('applicationName'))]",
            "type": "Microsoft.HDInsight/clusters/applications",
            "apiVersion": "2015-03-01-preview",
            "dependsOn": [ "[concat('Microsoft.HDInsight/clusters/',parameters('clusterName'))]" ],
            "properties": {
                "marketPlaceIdentifier": "EmptyNode",
                "computeProfile": {
                    "roles": [{
                        "name": "edgenode",
                        "targetInstanceCount": 1,
                        "hardwareProfile": {
                            "vmSize": "Standard_D3"
                        }
                    }]
                },
                "installScriptActions": [{
                    "name": "[concat('emptynode','-' ,uniquestring(variables('applicationName')))]",
                    "uri": "[parameters('installScriptAction')]",
                    "roles": ["edgenode"]
                }],
                "uninstallScriptActions": [],
                "httpsEndpoints": [],
                "applicationType": "CustomApplication"
            }
        }
    ],

<span data-ttu-id="f215d-110">Aşağıdaki örnekte gösterildiği gibi isteğe bağlı olarak çağırabilirsiniz bir [betik eylemi](hdinsight-hadoop-customize-cluster-linux.md) yükleme gibi ek yapılandırma gerçekleştirmeniz [Apache ton](hdinsight-hadoop-hue-linux.md) kenar düğümüne içinde.</span><span class="sxs-lookup"><span data-stu-id="f215d-110">As shown in the sample, you can optionally call a [script action](hdinsight-hadoop-customize-cluster-linux.md) to perform additional configuration, such as installing [Apache Hue](hdinsight-hadoop-hue-linux.md) in the edge node.</span></span> <span data-ttu-id="f215d-111">Betik eylemi betik Web'de genel olarak erişilebilir olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="f215d-111">The script action script must be publicly accessible on the web.</span></span>  <span data-ttu-id="f215d-112">Örneğin, komut dosyası Azure depolama alanında depolanıyorsa, genel kapsayıcılar veya genel BLOB'lar kullanın.</span><span class="sxs-lookup"><span data-stu-id="f215d-112">For example, if the script is stored in Azure storage, use either public containers or public blobs.</span></span>

<span data-ttu-id="f215d-113">Edge düğüm sanal makine boyutu Hdınsight küme çalışan düğümü vm boyutu gereksinimlerini karşılaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f215d-113">The edge node virtual machine size must meet the HDInsight cluster worker node vm size requirements.</span></span> <span data-ttu-id="f215d-114">Önerilen çalışan düğümü vm boyutları için bkz: [Hdınsight'ta oluşturmak Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span><span class="sxs-lookup"><span data-stu-id="f215d-114">For the recommended worker node vm sizes, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>

<span data-ttu-id="f215d-115">Bir edge düğümünü oluşturduktan sonra SSH kullanarak kenar düğümüne bağlanmak ve Hdınsight Hadoop kümesinde erişmek için istemci araçlarını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f215d-115">After you have created an edge node, you can connect to the edge node using SSH, and run client tools to access the Hadoop cluster in HDInsight.</span></span>

> [!WARNING] 
> <span data-ttu-id="f215d-116">Hdınsight ile boş kenar düğümünü kullanarak şu anda önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="f215d-116">Using an empty edge node with HDInsight is currently in preview.</span></span> <span data-ttu-id="f215d-117">Kenar düğümüne yüklenir özel bileşenler Microsoft ticari koşulların elverdiği oranda makul desteği alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f215d-117">Custom components that are installed on the edge node receive commercially reasonable support from Microsoft.</span></span> <span data-ttu-id="f215d-118">Bu, karşılaştığınız sorunları çözme konusunda neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="f215d-118">This might result in resolving problems you encounter.</span></span> <span data-ttu-id="f215d-119">Veya daha fazla yardım almak için topluluk kaynaklarına adlandırılabilir.</span><span class="sxs-lookup"><span data-stu-id="f215d-119">Or you may be referred to community resources for further assistance.</span></span> <span data-ttu-id="f215d-120">En etkin topluluktan Yardım almak için sitelere bazıları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="f215d-120">The following are some of the most active sites for getting help from the community:</span></span>
>
> * [<span data-ttu-id="f215d-121">Hdınsight için MSDN Forumu</span><span class="sxs-lookup"><span data-stu-id="f215d-121">MSDN forum for HDInsight</span></span>](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight)
> * <span data-ttu-id="f215d-122">[http://StackOverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="f215d-122">[http://stackoverflow.com](http://stackoverflow.com).</span></span>
>
> <span data-ttu-id="f215d-123">Bir Apache teknolojisi kullanıyorsanız, Apache yardımla üzerinde proje siteleri bulamıyor olabilir [http://apache.org](http://apache.org), gibi [Hadoop](http://hadoop.apache.org/) site.</span><span class="sxs-lookup"><span data-stu-id="f215d-123">If you are using an Apache technology, you may be able to find assistance through the Apache project sites on [http://apache.org](http://apache.org), such as the [Hadoop](http://hadoop.apache.org/) site.</span></span>

## <a name="add-an-edge-node-to-an-existing-cluster"></a><span data-ttu-id="f215d-124">Varolan bir kümeye bir kenar düğümüne ekleyin</span><span class="sxs-lookup"><span data-stu-id="f215d-124">Add an edge node to an existing cluster</span></span>
<span data-ttu-id="f215d-125">Bu bölümde, bir kenar düğümü olan bir Hdınsight kümesine eklemek için bir Resource Manager şablonunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="f215d-125">In this section, you use a Resource Manager template to add an edge node to an existing HDInsight cluster.</span></span>  <span data-ttu-id="f215d-126">Resource Manager şablonu bulunabilir [GitHub](https://azure.microsoft.com/en-us/resources/templates/101-hdinsight-linux-add-edge-node/).</span><span class="sxs-lookup"><span data-stu-id="f215d-126">The Resource Manager template can be found in [GitHub](https://azure.microsoft.com/en-us/resources/templates/101-hdinsight-linux-add-edge-node/).</span></span> <span data-ttu-id="f215d-127">Resource Manager şablonu https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-add-edge-node/scripts/EmptyNodeSetup.sh bulunan bir betik eylemi çağırır. Betik herhangi bir eylem gerçekleştirmez.</span><span class="sxs-lookup"><span data-stu-id="f215d-127">The Resource Manager template calls a script action located at https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-add-edge-node/scripts/EmptyNodeSetup.sh. The script doesn't perform any actions.</span></span>  <span data-ttu-id="f215d-128">Bu arama betik eylemi bir Resource Manager şablonunda göstermektir.</span><span class="sxs-lookup"><span data-stu-id="f215d-128">It is to demonstrate calling script action from a Resource Manager template.</span></span>

<span data-ttu-id="f215d-129">**Bir boş kenar düğümüne varolan bir kümeye eklemek için**</span><span class="sxs-lookup"><span data-stu-id="f215d-129">**To add an empty edge node to an existing cluster**</span></span>

1. <span data-ttu-id="f215d-130">Henüz yoksa, Hdınsight kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f215d-130">Create an HDInsight cluster if you don't have one yet.</span></span>  <span data-ttu-id="f215d-131">Bkz: [Hadoop Öğreticisi: Hdınsight'ta Hadoop kullanmaya başlamanıza](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f215d-131">See [Hadoop tutorial: Get started using Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
2. <span data-ttu-id="f215d-132">Azure'da oturum açın ve Azure portalında Azure Resource Manager şablonunu açmak için aşağıdaki görüntüye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f215d-132">Click the following image to sign in to Azure and open the Azure Resource Manager template in the Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-add-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy to Azure"></a>
3. <span data-ttu-id="f215d-133">Aşağıdaki özellikleri yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="f215d-133">Configure the following properties:</span></span>
   
   * <span data-ttu-id="f215d-134">**Abonelik**: kümeyi oluşturmak için kullanılan Azure aboneliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="f215d-134">**Subscription**: Select an Azure subscription used for creating the cluster.</span></span>
   * <span data-ttu-id="f215d-135">**Kaynak grubu**: Varolan Hdınsight kümesi için kullanılan kaynak grubunu seçin.</span><span class="sxs-lookup"><span data-stu-id="f215d-135">**Resource group**: Select the resource group used for the existing HDInsight cluster.</span></span>
   * <span data-ttu-id="f215d-136">**Konum**: olan bir Hdınsight kümesine konumunu seçin.</span><span class="sxs-lookup"><span data-stu-id="f215d-136">**Location**: Select the location of the existing HDInsight cluster.</span></span>
   * <span data-ttu-id="f215d-137">**Küme adı**: var olan bir Hdınsight kümesi adını girin.</span><span class="sxs-lookup"><span data-stu-id="f215d-137">**Cluster Name**: Enter the name of an existing HDInsight cluster.</span></span>
   * <span data-ttu-id="f215d-138">**Kenar düğüm boyutu**: VM boyutları birini seçin.</span><span class="sxs-lookup"><span data-stu-id="f215d-138">**Edge Node Size**: Select one of the VM sizes.</span></span> <span data-ttu-id="f215d-139">Vm boyutu çalışan düğümü vm boyutu gereksinimlerini karşılaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f215d-139">The vm size must meet the worker node vm size requirements.</span></span> <span data-ttu-id="f215d-140">Önerilen çalışan düğümü vm boyutları için bkz: [Hdınsight'ta oluşturmak Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span><span class="sxs-lookup"><span data-stu-id="f215d-140">For the recommended worker node vm sizes, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>
   * <span data-ttu-id="f215d-141">**Kenar düğümü önek**: varsayılan değer **yeni**.</span><span class="sxs-lookup"><span data-stu-id="f215d-141">**Edge Node Prefix**: The default value is **new**.</span></span>  <span data-ttu-id="f215d-142">Varsayılan değer, edge düğüm adı kullanmaktır **edgenode yeni**.</span><span class="sxs-lookup"><span data-stu-id="f215d-142">Using the default value, the edge node name is **new-edgenode**.</span></span>  <span data-ttu-id="f215d-143">Portal önekten özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f215d-143">You can customize the prefix from the portal.</span></span> <span data-ttu-id="f215d-144">Şablondan tam adını da özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f215d-144">You can also customize the full name from the template.</span></span>

4. <span data-ttu-id="f215d-145">Denetleme **hüküm ve koşulları yukarıda belirtildiği ediyorum**ve ardından **satın alma** kenar düğümüne oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="f215d-145">Check **I agree to the terms and conditions stated above**, and then click  **Purchase** to create the edge node.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="f215d-146">Azure kaynak grubu için var olan Hdınsight kümesi seçtiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="f215d-146">Make sure to select the Azure resource group for the existing HDInsight cluster.</span></span>  <span data-ttu-id="f215d-147">Aksi takdirde, "iç içe kaynak üzerinde istenen işlem gerçekleştirilemiyor. hata iletisi alıyorum</span><span class="sxs-lookup"><span data-stu-id="f215d-147">Otherwise, you get the error message "Can not perform requested operation on nested resource.</span></span> <span data-ttu-id="f215d-148">Üst kaynak '&lt;ClusterName >' bulunamadı. "</span><span class="sxs-lookup"><span data-stu-id="f215d-148">Parent resource '&lt;ClusterName>' not found."</span></span>

## <a name="add-an-edge-node-when-creating-a-cluster"></a><span data-ttu-id="f215d-149">Bir küme oluştururken bir kenar düğümüne ekleyin</span><span class="sxs-lookup"><span data-stu-id="f215d-149">Add an edge node when creating a cluster</span></span>
<span data-ttu-id="f215d-150">Bu bölümde, bir kenar düğümüne ile Hdınsight kümesi oluşturmak için Resource Manager şablonunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="f215d-150">In this section, you use a Resource Manager template to create HDInsight cluster with an edge node.</span></span>  <span data-ttu-id="f215d-151">Resource Manager şablonu bulunabilir [Azure hızlı başlangıç Şablon Galerisi](https://azure.microsoft.com/documentation/templates/101-hdinsight-linux-with-edge-node/).</span><span class="sxs-lookup"><span data-stu-id="f215d-151">The Resource Manager template can be found in the [Azure QuickStart Templates gallery](https://azure.microsoft.com/documentation/templates/101-hdinsight-linux-with-edge-node/).</span></span> <span data-ttu-id="f215d-152">Resource Manager şablonu https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-with-edge-node/scripts/EmptyNodeSetup.sh bulunan bir betik eylemi çağırır. Betik herhangi bir eylem gerçekleştirmez.</span><span class="sxs-lookup"><span data-stu-id="f215d-152">The Resource Manager template calls a script action located at https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-with-edge-node/scripts/EmptyNodeSetup.sh. The script doesn't perform any actions.</span></span>  <span data-ttu-id="f215d-153">Bu arama betik eylemi bir Resource Manager şablonunda göstermektir.</span><span class="sxs-lookup"><span data-stu-id="f215d-153">It is to demonstrate calling script action from a Resource Manager template.</span></span>

<span data-ttu-id="f215d-154">**Bir boş kenar düğümüne varolan bir kümeye eklemek için**</span><span class="sxs-lookup"><span data-stu-id="f215d-154">**To add an empty edge node to an existing cluster**</span></span>

1. <span data-ttu-id="f215d-155">Henüz yoksa, Hdınsight kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f215d-155">Create an HDInsight cluster if you don't have one yet.</span></span>  <span data-ttu-id="f215d-156">Bkz: [Hdınsight'ta Hadoop kullanmaya başlamanıza](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f215d-156">See [Get started using Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
2. <span data-ttu-id="f215d-157">Azure'da oturum açın ve Azure portalında Azure Resource Manager şablonunu açmak için aşağıdaki görüntüye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f215d-157">Click the following image to sign in to Azure and open the Azure Resource Manager template in the Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy to Azure"></a>
3. <span data-ttu-id="f215d-158">Aşağıdaki özellikleri yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="f215d-158">Configure the following properties:</span></span>
   
   * <span data-ttu-id="f215d-159">**Abonelik**: kümeyi oluşturmak için kullanılan Azure aboneliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="f215d-159">**Subscription**: Select an Azure subscription used for creating the cluster.</span></span>
   * <span data-ttu-id="f215d-160">**Kaynak grubu**: küme için kullanılan yeni bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f215d-160">**Resource group**: Create a new resource group used for the cluster.</span></span>
   * <span data-ttu-id="f215d-161">**Konum**: Kaynak grubu için bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="f215d-161">**Location**: Select a location for the resource group.</span></span>
   * <span data-ttu-id="f215d-162">**Küme adı**: oluşturmak yeni küme için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="f215d-162">**Cluster Name**: Enter a name for the new cluster to create.</span></span>
   * <span data-ttu-id="f215d-163">**Oturum açma kullanıcı adı küme**: Hadoop HTTP kullanıcı adı girin.</span><span class="sxs-lookup"><span data-stu-id="f215d-163">**Cluster Login User Name**: Enter the Hadoop HTTP user name.</span></span>  <span data-ttu-id="f215d-164">Varsayılan ad **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="f215d-164">The default name is **admin**.</span></span>
   * <span data-ttu-id="f215d-165">**Oturum açma parolası küme**: Hadoop HTTP kullanıcı parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="f215d-165">**Cluster Login Password**: Enter the Hadoop HTTP user password.</span></span>
   * <span data-ttu-id="f215d-166">**SSH kullanıcı adı**: SSH kullanıcı adı girin.</span><span class="sxs-lookup"><span data-stu-id="f215d-166">**Ssh User Name**: Enter the SSH user name.</span></span> <span data-ttu-id="f215d-167">Varsayılan ad **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="f215d-167">The default name is **sshuser**.</span></span>
   * <span data-ttu-id="f215d-168">**SSH parolası**: SSH kullanıcı parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="f215d-168">**Ssh Password**: Enter the SSH user password.</span></span>
   * <span data-ttu-id="f215d-169">**Yükleme komut dosyası eylemi**: Bu öğreticide gitmek için varsayılan değer tutun.</span><span class="sxs-lookup"><span data-stu-id="f215d-169">**Install Script Action**: Keep the default value for going through this tutorial.</span></span>
     
     <span data-ttu-id="f215d-170">Bazı özellikler sabit kodlanmış şablondaki olmuştur: küme türü, küme çalışan düğüm sayısı, Edge düğüm boyutu ve kenar düğüm adı.</span><span class="sxs-lookup"><span data-stu-id="f215d-170">Some properties have been hardcoded in the template: Cluster type, Cluster worker node count, Edge node size, and Edge node name.</span></span>
4. <span data-ttu-id="f215d-171">Denetleme **hüküm ve koşulları yukarıda belirtildiği ediyorum**ve ardından **satın alma** kenar düğümü ile küme oluşturmak için.</span><span class="sxs-lookup"><span data-stu-id="f215d-171">Check **I agree to the terms and conditions stated above**, and then click  **Purchase** to create the cluster with the edge node.</span></span>

## <a name="access-an-edge-node"></a><span data-ttu-id="f215d-172">Bir kenar düğümüne erişin</span><span class="sxs-lookup"><span data-stu-id="f215d-172">Access an edge node</span></span>
<span data-ttu-id="f215d-173">Kenar düğümüne ssh uç noktadır &lt;EdgeNodeName >.&lt; ClusterName >-ssh.azurehdinsight.net:22.</span><span class="sxs-lookup"><span data-stu-id="f215d-173">The edge node ssh endpoint is &lt;EdgeNodeName>.&lt;ClusterName>-ssh.azurehdinsight.net:22.</span></span>  <span data-ttu-id="f215d-174">Örneğin, yeni-edgenode.myedgenode0914-ssh.azurehdinsight.net:22.</span><span class="sxs-lookup"><span data-stu-id="f215d-174">For example, new-edgenode.myedgenode0914-ssh.azurehdinsight.net:22.</span></span>

<span data-ttu-id="f215d-175">Kenar düğümüne Azure Portal'da bir uygulama olarak görünür.</span><span class="sxs-lookup"><span data-stu-id="f215d-175">The edge node appears as an application on the Azure portal.</span></span>  <span data-ttu-id="f215d-176">Portal SSH kullanarak kenar düğümüne erişmeye bilgileri verir.</span><span class="sxs-lookup"><span data-stu-id="f215d-176">The portal gives you the information to access the edge node using SSH.</span></span>

<span data-ttu-id="f215d-177">**Edge düğüm SSH uç noktası doğrulamak için**</span><span class="sxs-lookup"><span data-stu-id="f215d-177">**To verify the edge node SSH endpoint**</span></span>

1. <span data-ttu-id="f215d-178">[Azure portalı](https://portal.azure.com) üzerinde oturum açın.</span><span class="sxs-lookup"><span data-stu-id="f215d-178">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f215d-179">Hdınsight kümesi ile bir edge düğümünü açın.</span><span class="sxs-lookup"><span data-stu-id="f215d-179">Open the HDInsight cluster with an edge node.</span></span>
3. <span data-ttu-id="f215d-180">Tıklatın **uygulamaları** küme dikey penceresinden.</span><span class="sxs-lookup"><span data-stu-id="f215d-180">Click **Applications** from the cluster blade.</span></span> <span data-ttu-id="f215d-181">Kenar düğümünü göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="f215d-181">You shall see the edge node.</span></span>  <span data-ttu-id="f215d-182">Varsayılan ad **edgenode yeni**.</span><span class="sxs-lookup"><span data-stu-id="f215d-182">The default name is **new-edgenode**.</span></span>
4. <span data-ttu-id="f215d-183">Kenar düğümüne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f215d-183">Click the edge node.</span></span> <span data-ttu-id="f215d-184">SSH uç noktası göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="f215d-184">You shall see the SSH endpoint.</span></span>

<span data-ttu-id="f215d-185">**Edge düğüm üzerinde Hive kullanmak için**</span><span class="sxs-lookup"><span data-stu-id="f215d-185">**To use Hive on the edge node**</span></span>

1. <span data-ttu-id="f215d-186">Kenar düğümüne bağlanmak için SSH kullanın.</span><span class="sxs-lookup"><span data-stu-id="f215d-186">Use SSH to connect to the edge node.</span></span> <span data-ttu-id="f215d-187">Bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f215d-187">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="f215d-188">SSH kullanarak kenar düğümüne bağlandıktan sonra Hive konsolunu açmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="f215d-188">After you have connected to the edge node using SSH, use the following command to open the Hive console:</span></span>
   
        hive
3. <span data-ttu-id="f215d-189">Hive tablolarını kümede göstermek için aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="f215d-189">Run the following command to show Hive tables in the cluster:</span></span>
   
        show tables;

## <a name="delete-an-edge-node"></a><span data-ttu-id="f215d-190">Bir kenar düğümüne Sil</span><span class="sxs-lookup"><span data-stu-id="f215d-190">Delete an edge node</span></span>
<span data-ttu-id="f215d-191">Azure portalından bir kenar düğümüne silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f215d-191">You can delete an edge node from the Azure portal.</span></span>

<span data-ttu-id="f215d-192">**Bir kenar düğümüne erişmek için**</span><span class="sxs-lookup"><span data-stu-id="f215d-192">**To access an edge node**</span></span>

1. <span data-ttu-id="f215d-193">[Azure portalı](https://portal.azure.com) üzerinde oturum açın.</span><span class="sxs-lookup"><span data-stu-id="f215d-193">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f215d-194">Hdınsight kümesi ile bir edge düğümünü açın.</span><span class="sxs-lookup"><span data-stu-id="f215d-194">Open the HDInsight cluster with an edge node.</span></span>
3. <span data-ttu-id="f215d-195">Tıklatın **uygulamaları** küme dikey penceresinden.</span><span class="sxs-lookup"><span data-stu-id="f215d-195">Click **Applications** from the cluster blade.</span></span> <span data-ttu-id="f215d-196">Edge düğüm listesi göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="f215d-196">You shall see a list of edge nodes.</span></span>  
4. <span data-ttu-id="f215d-197">Silin ve ardından istediğiniz kenar düğümüne sağ **silmek**.</span><span class="sxs-lookup"><span data-stu-id="f215d-197">Right-click the edge node you want to delete, and then click **Delete**.</span></span>
5. <span data-ttu-id="f215d-198">Onaylamak için **Evet**’e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="f215d-198">Click **Yes** to confirm.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f215d-199">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="f215d-199">Next steps</span></span>
<span data-ttu-id="f215d-200">Bu makalede, bir kenar düğümüne eklemeyi ve kenar düğümüne erişim öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="f215d-200">In this article, you have learned how to add an edge node and how to access the edge node.</span></span> <span data-ttu-id="f215d-201">Daha fazla bilgi için aşağıdaki makalelere bakın:</span><span class="sxs-lookup"><span data-stu-id="f215d-201">To learn more, see the following articles:</span></span>

* <span data-ttu-id="f215d-202">[HDInsight uygulamaları yükleme](hdinsight-apps-install-applications.md): HDInsight uygulamalarını kümelerinize yükleme hakkında bilgi alın.</span><span class="sxs-lookup"><span data-stu-id="f215d-202">[Install HDInsight applications](hdinsight-apps-install-applications.md): Learn how to install an HDInsight application to your clusters.</span></span>
* <span data-ttu-id="f215d-203">[Özel Hdınsight uygulamaları yükleme](hdinsight-apps-install-custom-applications.md): yayımlanmamış bir Hdınsight uygulamasının Hdınsight'a nasıl yükleneceğini öğrenin.</span><span class="sxs-lookup"><span data-stu-id="f215d-203">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): learn how to deploy an unpublished HDInsight application to HDInsight.</span></span>
* <span data-ttu-id="f215d-204">[HDInsight uygulamalarını yayımlama](hdinsight-apps-publish-applications.md): Özel HDInsight uygulamalarınızı Azure Marketi’nde nasıl yayımlayacağınızı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="f215d-204">[Publish HDInsight applications](hdinsight-apps-publish-applications.md): Learn how to publish your custom HDInsight applications to Azure Marketplace.</span></span>
* <span data-ttu-id="f215d-205">[MSDN: HDInsight uygulaması yükleme](https://msdn.microsoft.com/library/mt706515.aspx): HDInsight uygulamalarını nasıl tanımlayacağınızı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="f215d-205">[MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx): Learn how to define HDInsight applications.</span></span>
* <span data-ttu-id="f215d-206">[Betik Eylemi kullanarak Linux tabanlı HDInsight kümelerini özelleştirme](hdinsight-hadoop-customize-cluster-linux.md): ek uygulamalar yüklemek için Betik Eyleminin nasıl kullanılacağını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="f215d-206">[Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md): learn how to use Script Action to install additional applications.</span></span>
* <span data-ttu-id="f215d-207">[Resource Manager şablonları kullanarak HDInsight’ta Linux tabanlı Hadoop kümeleri oluşturma](hdinsight-hadoop-create-linux-clusters-arm-templates.md): HDInsight kümeleri oluşturmak için Resource Manager şablonlarının nasıl çağrılacağını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="f215d-207">[Create Linux-based Hadoop clusters in HDInsight using Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md): learn how to call Resource Manager templates to create HDInsight clusters.</span></span>

