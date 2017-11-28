---
title: "aaaUse boş hdınsight'ta - Azure Hadoop kümelerde edge düğüm | Microsoft Docs"
description: "Nasıl tooadd boş kenar düğümü tooan Hdınsight küme, bir istemci olarak kullanılabilir ve ardından test/Hdınsight uygulamalarınızı ana bilgisayarı."
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
ms.openlocfilehash: 9c910905b51f2fe92e6e5d47d86a32bd5247c2cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-empty-edge-nodes-on-hadoop-clusters-in-hdinsight"></a><span data-ttu-id="aecf6-103">Hdınsight'ta Hadoop kümeleri üzerinde boş kenar düğümleri kullanın</span><span class="sxs-lookup"><span data-stu-id="aecf6-103">Use empty edge nodes on Hadoop clusters in HDInsight</span></span>

<span data-ttu-id="aecf6-104">Nasıl tooadd boş bir kenar düğümü tooan Hdınsight kümesi hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="aecf6-104">Learn how tooadd an empty edge node tooan HDInsight cluster.</span></span> <span data-ttu-id="aecf6-105">Linux sanal makine ile aynı istemci araçları yüklü ve yapılandırılmış olduğu gibi hello headnodes hello ancak çalışan hiçbir Hadoop Hizmetleri bir boş kenar düğümdür.</span><span class="sxs-lookup"><span data-stu-id="aecf6-105">An empty edge node is a Linux virtual machine with hello same client tools installed and configured as in hello headnodes, but with no Hadoop services running.</span></span> <span data-ttu-id="aecf6-106">Merhaba kenar düğümüne hello küme erişmek, istemci uygulamalarınızı test etme ve istemci uygulamalarını barındırmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aecf6-106">You can use hello edge node for accessing hello cluster, testing your client applications, and hosting your client applications.</span></span> 

<span data-ttu-id="aecf6-107">Merhaba Küme oluşturduğunuzda bir boş kenar düğümü tooan varolan Hdınsight kümesi, yeni küme tooa ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aecf6-107">You can add an empty edge node tooan existing HDInsight cluster, tooa new cluster when you create hello cluster.</span></span> <span data-ttu-id="aecf6-108">Bir boş kenar düğümüne ekleyerek yapılır Azure Resource Manager şablonu kullanarak.</span><span class="sxs-lookup"><span data-stu-id="aecf6-108">Adding an empty edge node is done using Azure Resource Manager template.</span></span>  <span data-ttu-id="aecf6-109">Merhaba aşağıdaki örnek nasıl yapıldığını gösteren bir şablon kullanarak:</span><span class="sxs-lookup"><span data-stu-id="aecf6-109">hello following sample demonstrates how it is done using a template:</span></span>

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

<span data-ttu-id="aecf6-110">Merhaba örnekte gösterildiği gibi isteğe bağlı olarak çağırabilirsiniz bir [betik eylemi](hdinsight-hadoop-customize-cluster-linux.md) yükleme gibi ek yapılandırma tooperform, [Apache ton](hdinsight-hadoop-hue-linux.md) hello kenar düğümünde.</span><span class="sxs-lookup"><span data-stu-id="aecf6-110">As shown in hello sample, you can optionally call a [script action](hdinsight-hadoop-customize-cluster-linux.md) tooperform additional configuration, such as installing [Apache Hue](hdinsight-hadoop-hue-linux.md) in hello edge node.</span></span> <span data-ttu-id="aecf6-111">Merhaba betik eylemi betik hello Web'de genel olarak erişilebilir olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="aecf6-111">hello script action script must be publicly accessible on hello web.</span></span>  <span data-ttu-id="aecf6-112">Merhaba komut dosyası Azure depolama alanında depolanır, örneğin, genel kapsayıcılar veya genel BLOB'lar kullanın.</span><span class="sxs-lookup"><span data-stu-id="aecf6-112">For example, if hello script is stored in Azure storage, use either public containers or public blobs.</span></span>

<span data-ttu-id="aecf6-113">Merhaba kenar düğümü sanal makine boyutu hello Hdınsight küme çalışan düğümü vm boyutu gereksinimlerini karşılaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="aecf6-113">hello edge node virtual machine size must meet hello HDInsight cluster worker node vm size requirements.</span></span> <span data-ttu-id="aecf6-114">Merhaba çalışan düğümü vm boyutları önerilen için bkz: [Hdınsight'ta oluşturmak Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span><span class="sxs-lookup"><span data-stu-id="aecf6-114">For hello recommended worker node vm sizes, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>

<span data-ttu-id="aecf6-115">Bir edge düğümünü oluşturduktan sonra SSH kullanarak toohello kenar düğümüne bağlanmak ve istemci araçları tooaccess hello Hadoop kümesi Hdınsight'ta çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="aecf6-115">After you have created an edge node, you can connect toohello edge node using SSH, and run client tools tooaccess hello Hadoop cluster in HDInsight.</span></span>

> [!WARNING] 
> <span data-ttu-id="aecf6-116">Hdınsight ile boş kenar düğümünü kullanarak şu anda önizlemede değil.</span><span class="sxs-lookup"><span data-stu-id="aecf6-116">Using an empty edge node with HDInsight is currently in preview.</span></span> <span data-ttu-id="aecf6-117">Merhaba kenar düğümüne yüklenir özel bileşenler Microsoft ticari koşulların elverdiği oranda makul desteği alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aecf6-117">Custom components that are installed on hello edge node receive commercially reasonable support from Microsoft.</span></span> <span data-ttu-id="aecf6-118">Bu, karşılaştığınız sorunları çözme konusunda neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="aecf6-118">This might result in resolving problems you encounter.</span></span> <span data-ttu-id="aecf6-119">Veya daha fazla yardım için başvurulan toocommunity kaynakları olabilir.</span><span class="sxs-lookup"><span data-stu-id="aecf6-119">Or you may be referred toocommunity resources for further assistance.</span></span> <span data-ttu-id="aecf6-120">Merhaba alma çoğu etkin siteler hello topluluktan Yardım hello bazıları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="aecf6-120">hello following are some of hello most active sites for getting help from hello community:</span></span>
>
> * [<span data-ttu-id="aecf6-121">Hdınsight için MSDN Forumu</span><span class="sxs-lookup"><span data-stu-id="aecf6-121">MSDN forum for HDInsight</span></span>](https://social.msdn.microsoft.com/Forums/azure/home?forum=hdinsight)
> * <span data-ttu-id="aecf6-122">[http://StackOverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="aecf6-122">[http://stackoverflow.com](http://stackoverflow.com).</span></span>
>
> <span data-ttu-id="aecf6-123">Apache teknolojisi kullanıyorsanız, Apache proje sitelerinde hello mümkün toofind yardımla olabilir [http://apache.org](http://apache.org), hello gibi [Hadoop](http://hadoop.apache.org/) site.</span><span class="sxs-lookup"><span data-stu-id="aecf6-123">If you are using an Apache technology, you may be able toofind assistance through hello Apache project sites on [http://apache.org](http://apache.org), such as hello [Hadoop](http://hadoop.apache.org/) site.</span></span>

## <a name="add-an-edge-node-tooan-existing-cluster"></a><span data-ttu-id="aecf6-124">Edge düğüm tooan varolan bir kümeye ekleme</span><span class="sxs-lookup"><span data-stu-id="aecf6-124">Add an edge node tooan existing cluster</span></span>
<span data-ttu-id="aecf6-125">Bu bölümde, Resource Manager şablonu tooadd kenar düğümü tooan varolan Hdınsight kümesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="aecf6-125">In this section, you use a Resource Manager template tooadd an edge node tooan existing HDInsight cluster.</span></span>  <span data-ttu-id="aecf6-126">Merhaba Resource Manager şablonu bulunabilir [GitHub](https://azure.microsoft.com/en-us/resources/templates/101-hdinsight-linux-add-edge-node/).</span><span class="sxs-lookup"><span data-stu-id="aecf6-126">hello Resource Manager template can be found in [GitHub](https://azure.microsoft.com/en-us/resources/templates/101-hdinsight-linux-add-edge-node/).</span></span> <span data-ttu-id="aecf6-127">Merhaba Resource Manager şablonu https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-add-edge-node/scripts/EmptyNodeSetup.sh bulunan bir betik eylemi çağırır. Merhaba betik eylemleri gerçekleştirmez.</span><span class="sxs-lookup"><span data-stu-id="aecf6-127">hello Resource Manager template calls a script action located at https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-add-edge-node/scripts/EmptyNodeSetup.sh. hello script doesn't perform any actions.</span></span>  <span data-ttu-id="aecf6-128">Resource Manager şablonu betik eylemi çağırma toodemonstrate olur.</span><span class="sxs-lookup"><span data-stu-id="aecf6-128">It is toodemonstrate calling script action from a Resource Manager template.</span></span>

<span data-ttu-id="aecf6-129">**tooadd boş kenar düğümü tooan varolan bir kümeye**</span><span class="sxs-lookup"><span data-stu-id="aecf6-129">**tooadd an empty edge node tooan existing cluster**</span></span>

1. <span data-ttu-id="aecf6-130">Henüz yoksa, Hdınsight kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="aecf6-130">Create an HDInsight cluster if you don't have one yet.</span></span>  <span data-ttu-id="aecf6-131">Bkz: [Hadoop Öğreticisi: Hdınsight'ta Hadoop kullanmaya başlamanıza](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="aecf6-131">See [Hadoop tutorial: Get started using Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
2. <span data-ttu-id="aecf6-132">Görüntü toosign tooAzure olarak ve açık hello Azure Resource Manager şablonu hello Azure Portalı'nda aşağıdaki hello'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="aecf6-132">Click hello following image toosign in tooAzure and open hello Azure Resource Manager template in hello Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-add-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy tooAzure"></a>
3. <span data-ttu-id="aecf6-133">Aşağıdaki özelliklere hello yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="aecf6-133">Configure hello following properties:</span></span>
   
   * <span data-ttu-id="aecf6-134">**Abonelik**: hello küme oluşturmak için kullanılan Azure aboneliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="aecf6-134">**Subscription**: Select an Azure subscription used for creating hello cluster.</span></span>
   * <span data-ttu-id="aecf6-135">**Kaynak grubu**: hello varolan Hdınsight kümesi için kullanılan Select hello kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="aecf6-135">**Resource group**: Select hello resource group used for hello existing HDInsight cluster.</span></span>
   * <span data-ttu-id="aecf6-136">**Konum**: hello olan bir Hdınsight kümesine hello konumunu seçin.</span><span class="sxs-lookup"><span data-stu-id="aecf6-136">**Location**: Select hello location of hello existing HDInsight cluster.</span></span>
   * <span data-ttu-id="aecf6-137">**Küme adı**: mevcut bir Hdınsight kümesine hello adını girin.</span><span class="sxs-lookup"><span data-stu-id="aecf6-137">**Cluster Name**: Enter hello name of an existing HDInsight cluster.</span></span>
   * <span data-ttu-id="aecf6-138">**Kenar düğüm boyutu**: hello VM boyutları birini seçin.</span><span class="sxs-lookup"><span data-stu-id="aecf6-138">**Edge Node Size**: Select one of hello VM sizes.</span></span> <span data-ttu-id="aecf6-139">Merhaba vm boyutu hello çalışan düğümü vm boyutu gereksinimlerini karşılaması gerekir.</span><span class="sxs-lookup"><span data-stu-id="aecf6-139">hello vm size must meet hello worker node vm size requirements.</span></span> <span data-ttu-id="aecf6-140">Merhaba çalışan düğümü vm boyutları önerilen için bkz: [Hdınsight'ta oluşturmak Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span><span class="sxs-lookup"><span data-stu-id="aecf6-140">For hello recommended worker node vm sizes, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>
   * <span data-ttu-id="aecf6-141">**Kenar düğümü önek**: hello varsayılan değer **yeni**.</span><span class="sxs-lookup"><span data-stu-id="aecf6-141">**Edge Node Prefix**: hello default value is **new**.</span></span>  <span data-ttu-id="aecf6-142">Merhaba varsayılan değer, hello edge düğüm adı kullanmaktır **edgenode yeni**.</span><span class="sxs-lookup"><span data-stu-id="aecf6-142">Using hello default value, hello edge node name is **new-edgenode**.</span></span>  <span data-ttu-id="aecf6-143">Merhaba portal hello önekten özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aecf6-143">You can customize hello prefix from hello portal.</span></span> <span data-ttu-id="aecf6-144">Merhaba şablondan hello tam adını da özelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aecf6-144">You can also customize hello full name from hello template.</span></span>

4. <span data-ttu-id="aecf6-145">Denetleme **toohello hüküm ve koşullar yukarıda belirtildiği kabul**ve ardından **satın alma** toocreate hello kenar düğümüne.</span><span class="sxs-lookup"><span data-stu-id="aecf6-145">Check **I agree toohello terms and conditions stated above**, and then click  **Purchase** toocreate hello edge node.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="aecf6-146">Merhaba varolan Hdınsight kümesi için emin tooselect hello Azure kaynak grubu olun.</span><span class="sxs-lookup"><span data-stu-id="aecf6-146">Make sure tooselect hello Azure resource group for hello existing HDInsight cluster.</span></span>  <span data-ttu-id="aecf6-147">Aksi takdirde, ileti "iç içe kaynak üzerinde istenen işlem gerçekleştirilemiyor. hello hata Al</span><span class="sxs-lookup"><span data-stu-id="aecf6-147">Otherwise, you get hello error message "Can not perform requested operation on nested resource.</span></span> <span data-ttu-id="aecf6-148">Üst kaynak '&lt;ClusterName >' bulunamadı. "</span><span class="sxs-lookup"><span data-stu-id="aecf6-148">Parent resource '&lt;ClusterName>' not found."</span></span>

## <a name="add-an-edge-node-when-creating-a-cluster"></a><span data-ttu-id="aecf6-149">Bir küme oluştururken bir kenar düğümüne ekleyin</span><span class="sxs-lookup"><span data-stu-id="aecf6-149">Add an edge node when creating a cluster</span></span>
<span data-ttu-id="aecf6-150">Bu bölümde, bir Resource Manager şablonu toocreate Hdınsight kümesi ile bir edge düğümünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="aecf6-150">In this section, you use a Resource Manager template toocreate HDInsight cluster with an edge node.</span></span>  <span data-ttu-id="aecf6-151">Merhaba Resource Manager şablonu hello bulunabilir [Azure hızlı başlangıç Şablon Galerisi](https://azure.microsoft.com/documentation/templates/101-hdinsight-linux-with-edge-node/).</span><span class="sxs-lookup"><span data-stu-id="aecf6-151">hello Resource Manager template can be found in hello [Azure QuickStart Templates gallery](https://azure.microsoft.com/documentation/templates/101-hdinsight-linux-with-edge-node/).</span></span> <span data-ttu-id="aecf6-152">Merhaba Resource Manager şablonu https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-with-edge-node/scripts/EmptyNodeSetup.sh bulunan bir betik eylemi çağırır. Merhaba betik eylemleri gerçekleştirmez.</span><span class="sxs-lookup"><span data-stu-id="aecf6-152">hello Resource Manager template calls a script action located at https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-hdinsight-linux-with-edge-node/scripts/EmptyNodeSetup.sh. hello script doesn't perform any actions.</span></span>  <span data-ttu-id="aecf6-153">Resource Manager şablonu betik eylemi çağırma toodemonstrate olur.</span><span class="sxs-lookup"><span data-stu-id="aecf6-153">It is toodemonstrate calling script action from a Resource Manager template.</span></span>

<span data-ttu-id="aecf6-154">**tooadd boş kenar düğümü tooan varolan bir kümeye**</span><span class="sxs-lookup"><span data-stu-id="aecf6-154">**tooadd an empty edge node tooan existing cluster**</span></span>

1. <span data-ttu-id="aecf6-155">Henüz yoksa, Hdınsight kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="aecf6-155">Create an HDInsight cluster if you don't have one yet.</span></span>  <span data-ttu-id="aecf6-156">Bkz: [Hdınsight'ta Hadoop kullanmaya başlamanıza](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="aecf6-156">See [Get started using Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
2. <span data-ttu-id="aecf6-157">Görüntü toosign tooAzure olarak ve açık hello Azure Resource Manager şablonu hello Azure Portalı'nda aşağıdaki hello'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="aecf6-157">Click hello following image toosign in tooAzure and open hello Azure Resource Manager template in hello Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-edge-node%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apps-use-edge-node/deploy-to-azure.png" alt="Deploy tooAzure"></a>
3. <span data-ttu-id="aecf6-158">Aşağıdaki özelliklere hello yapılandırın:</span><span class="sxs-lookup"><span data-stu-id="aecf6-158">Configure hello following properties:</span></span>
   
   * <span data-ttu-id="aecf6-159">**Abonelik**: hello küme oluşturmak için kullanılan Azure aboneliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="aecf6-159">**Subscription**: Select an Azure subscription used for creating hello cluster.</span></span>
   * <span data-ttu-id="aecf6-160">**Kaynak grubu**: hello kümesi için kullanılan yeni bir kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="aecf6-160">**Resource group**: Create a new resource group used for hello cluster.</span></span>
   * <span data-ttu-id="aecf6-161">**Konum**: hello kaynak grubu için bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="aecf6-161">**Location**: Select a location for hello resource group.</span></span>
   * <span data-ttu-id="aecf6-162">**Küme adı**: hello yeni küme toocreate için bir ad girin.</span><span class="sxs-lookup"><span data-stu-id="aecf6-162">**Cluster Name**: Enter a name for hello new cluster toocreate.</span></span>
   * <span data-ttu-id="aecf6-163">**Oturum açma kullanıcı adı küme**: Merhaba Hadoop HTTP kullanıcı adı girin.</span><span class="sxs-lookup"><span data-stu-id="aecf6-163">**Cluster Login User Name**: Enter hello Hadoop HTTP user name.</span></span>  <span data-ttu-id="aecf6-164">Merhaba varsayılan ad **yönetici**.</span><span class="sxs-lookup"><span data-stu-id="aecf6-164">hello default name is **admin**.</span></span>
   * <span data-ttu-id="aecf6-165">**Oturum açma parolası küme**: Merhaba Hadoop HTTP kullanıcı parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="aecf6-165">**Cluster Login Password**: Enter hello Hadoop HTTP user password.</span></span>
   * <span data-ttu-id="aecf6-166">**SSH kullanıcı adı**: hello SSH kullanıcı adı girin.</span><span class="sxs-lookup"><span data-stu-id="aecf6-166">**Ssh User Name**: Enter hello SSH user name.</span></span> <span data-ttu-id="aecf6-167">Merhaba varsayılan ad **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="aecf6-167">hello default name is **sshuser**.</span></span>
   * <span data-ttu-id="aecf6-168">**SSH parolası**: hello SSH kullanıcı parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="aecf6-168">**Ssh Password**: Enter hello SSH user password.</span></span>
   * <span data-ttu-id="aecf6-169">**Yükleme komut dosyası eylemi**: Bu öğreticide gitmek için varsayılan değer hello tutun.</span><span class="sxs-lookup"><span data-stu-id="aecf6-169">**Install Script Action**: Keep hello default value for going through this tutorial.</span></span>
     
     <span data-ttu-id="aecf6-170">Bazı özellikler sabit kodlanmış hello şablonunda olmuştur: küme türü, küme çalışan düğüm sayısı, Edge düğüm boyutu ve kenar düğüm adı.</span><span class="sxs-lookup"><span data-stu-id="aecf6-170">Some properties have been hardcoded in hello template: Cluster type, Cluster worker node count, Edge node size, and Edge node name.</span></span>
4. <span data-ttu-id="aecf6-171">Denetleyin **toohello hüküm ve koşullar yukarıda belirtildiği kabul**ve ardından **satın alma** toocreate hello küme hello kenar düğümüne sahip.</span><span class="sxs-lookup"><span data-stu-id="aecf6-171">Check **I agree toohello terms and conditions stated above**, and then click  **Purchase** toocreate hello cluster with hello edge node.</span></span>

## <a name="access-an-edge-node"></a><span data-ttu-id="aecf6-172">Bir kenar düğümüne erişin</span><span class="sxs-lookup"><span data-stu-id="aecf6-172">Access an edge node</span></span>
<span data-ttu-id="aecf6-173">Merhaba kenar düğümüne ssh uç noktadır &lt;EdgeNodeName >.&lt; ClusterName >-ssh.azurehdinsight.net:22.</span><span class="sxs-lookup"><span data-stu-id="aecf6-173">hello edge node ssh endpoint is &lt;EdgeNodeName>.&lt;ClusterName>-ssh.azurehdinsight.net:22.</span></span>  <span data-ttu-id="aecf6-174">Örneğin, yeni-edgenode.myedgenode0914-ssh.azurehdinsight.net:22.</span><span class="sxs-lookup"><span data-stu-id="aecf6-174">For example, new-edgenode.myedgenode0914-ssh.azurehdinsight.net:22.</span></span>

<span data-ttu-id="aecf6-175">Merhaba kenar düğümüne hello Azure portalında bir uygulama olarak görünür.</span><span class="sxs-lookup"><span data-stu-id="aecf6-175">hello edge node appears as an application on hello Azure portal.</span></span>  <span data-ttu-id="aecf6-176">bilgi tooaccess hello hello hello portal verir düğümü SSH kullanarak kenar.</span><span class="sxs-lookup"><span data-stu-id="aecf6-176">hello portal gives you hello information tooaccess hello edge node using SSH.</span></span>

<span data-ttu-id="aecf6-177">**tooverify hello kenar düğümü SSH uç noktası**</span><span class="sxs-lookup"><span data-stu-id="aecf6-177">**tooverify hello edge node SSH endpoint**</span></span>

1. <span data-ttu-id="aecf6-178">Toohello üzerinde oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="aecf6-178">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="aecf6-179">Merhaba Hdınsight kümesi ile bir edge düğümünü açın.</span><span class="sxs-lookup"><span data-stu-id="aecf6-179">Open hello HDInsight cluster with an edge node.</span></span>
3. <span data-ttu-id="aecf6-180">Tıklatın **uygulamaları** hello küme dikey penceresinden.</span><span class="sxs-lookup"><span data-stu-id="aecf6-180">Click **Applications** from hello cluster blade.</span></span> <span data-ttu-id="aecf6-181">Merhaba kenar düğümünü göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="aecf6-181">You shall see hello edge node.</span></span>  <span data-ttu-id="aecf6-182">Merhaba varsayılan ad **edgenode yeni**.</span><span class="sxs-lookup"><span data-stu-id="aecf6-182">hello default name is **new-edgenode**.</span></span>
4. <span data-ttu-id="aecf6-183">Merhaba kenar düğümüne tıklayın.</span><span class="sxs-lookup"><span data-stu-id="aecf6-183">Click hello edge node.</span></span> <span data-ttu-id="aecf6-184">Merhaba SSH uç noktası göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="aecf6-184">You shall see hello SSH endpoint.</span></span>

<span data-ttu-id="aecf6-185">**toouse hello kenar düğümüne yığını**</span><span class="sxs-lookup"><span data-stu-id="aecf6-185">**toouse Hive on hello edge node**</span></span>

1. <span data-ttu-id="aecf6-186">SSH tooconnect toohello kenar düğümünü kullanın.</span><span class="sxs-lookup"><span data-stu-id="aecf6-186">Use SSH tooconnect toohello edge node.</span></span> <span data-ttu-id="aecf6-187">Bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="aecf6-187">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="aecf6-188">SSH kullanarak kenar düğümüne toohello bağlandıktan sonra komut tooopen hello Hive konsolundan aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="aecf6-188">After you have connected toohello edge node using SSH, use hello following command tooopen hello Hive console:</span></span>
   
        hive
3. <span data-ttu-id="aecf6-189">Komut tooshow Hive tablolarını hello kümedeki aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="aecf6-189">Run hello following command tooshow Hive tables in hello cluster:</span></span>
   
        show tables;

## <a name="delete-an-edge-node"></a><span data-ttu-id="aecf6-190">Bir kenar düğümüne Sil</span><span class="sxs-lookup"><span data-stu-id="aecf6-190">Delete an edge node</span></span>
<span data-ttu-id="aecf6-191">Azure portal hello bir kenar düğümüne silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aecf6-191">You can delete an edge node from hello Azure portal.</span></span>

<span data-ttu-id="aecf6-192">**tooaccess bir kenar düğümüne**</span><span class="sxs-lookup"><span data-stu-id="aecf6-192">**tooaccess an edge node**</span></span>

1. <span data-ttu-id="aecf6-193">Toohello üzerinde oturum [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="aecf6-193">Sign on toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="aecf6-194">Merhaba Hdınsight kümesi ile bir edge düğümünü açın.</span><span class="sxs-lookup"><span data-stu-id="aecf6-194">Open hello HDInsight cluster with an edge node.</span></span>
3. <span data-ttu-id="aecf6-195">Tıklatın **uygulamaları** hello küme dikey penceresinden.</span><span class="sxs-lookup"><span data-stu-id="aecf6-195">Click **Applications** from hello cluster blade.</span></span> <span data-ttu-id="aecf6-196">Edge düğüm listesi göreceksiniz.</span><span class="sxs-lookup"><span data-stu-id="aecf6-196">You shall see a list of edge nodes.</span></span>  
4. <span data-ttu-id="aecf6-197">Toodelete istediğiniz ve ardından sağ hello kenar düğümüne **silmek**.</span><span class="sxs-lookup"><span data-stu-id="aecf6-197">Right-click hello edge node you want toodelete, and then click **Delete**.</span></span>
5. <span data-ttu-id="aecf6-198">Tıklatın **Evet** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="aecf6-198">Click **Yes** tooconfirm.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aecf6-199">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="aecf6-199">Next steps</span></span>
<span data-ttu-id="aecf6-200">Bu makalede, öğrendiğiniz nasıl tooadd bir edge düğümünü ve nasıl tooaccess kenar düğümüne hello.</span><span class="sxs-lookup"><span data-stu-id="aecf6-200">In this article, you have learned how tooadd an edge node and how tooaccess hello edge node.</span></span> <span data-ttu-id="aecf6-201">toolearn daha makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="aecf6-201">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="aecf6-202">[Hdınsight uygulamaları yükleme](hdinsight-apps-install-applications.md): tooinstall bir Hdınsight uygulaması tooyour nasıl kümeleri öğrenin.</span><span class="sxs-lookup"><span data-stu-id="aecf6-202">[Install HDInsight applications](hdinsight-apps-install-applications.md): Learn how tooinstall an HDInsight application tooyour clusters.</span></span>
* <span data-ttu-id="aecf6-203">[Özel Hdınsight uygulamaları yükleme](hdinsight-apps-install-custom-applications.md): öğrenin nasıl toodeploy yayımlanmamış bir Hdınsight uygulaması tooHDInsight.</span><span class="sxs-lookup"><span data-stu-id="aecf6-203">[Install custom HDInsight applications](hdinsight-apps-install-custom-applications.md): learn how toodeploy an unpublished HDInsight application tooHDInsight.</span></span>
* <span data-ttu-id="aecf6-204">[Hdınsight uygulamalarını yayımlama](hdinsight-apps-publish-applications.md): öğrenin nasıl toopublish, özel Hdınsight uygulamaları tooAzure Market.</span><span class="sxs-lookup"><span data-stu-id="aecf6-204">[Publish HDInsight applications](hdinsight-apps-publish-applications.md): Learn how toopublish your custom HDInsight applications tooAzure Marketplace.</span></span>
* <span data-ttu-id="aecf6-205">[MSDN: Hdınsight uygulaması yükleme](https://msdn.microsoft.com/library/mt706515.aspx): öğrenin nasıl toodefine Hdınsight uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="aecf6-205">[MSDN: Install an HDInsight application](https://msdn.microsoft.com/library/mt706515.aspx): Learn how toodefine HDInsight applications.</span></span>
* <span data-ttu-id="aecf6-206">[Betik eylemi kullanarak Linux tabanlı Hdınsight kümelerini özelleştirme](hdinsight-hadoop-customize-cluster-linux.md): öğrenin nasıl toouse betik eylemi tooinstall ek uygulamalar.</span><span class="sxs-lookup"><span data-stu-id="aecf6-206">[Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md): learn how toouse Script Action tooinstall additional applications.</span></span>
* <span data-ttu-id="aecf6-207">[Resource Manager şablonları kullanarak Hdınsight'ta Linux tabanlı Hadoop kümeleri oluşturma](hdinsight-hadoop-create-linux-clusters-arm-templates.md): nasıl toocall Resource Manager şablonları toocreate Hdınsight kümeleri öğrenin.</span><span class="sxs-lookup"><span data-stu-id="aecf6-207">[Create Linux-based Hadoop clusters in HDInsight using Resource Manager templates](hdinsight-hadoop-create-linux-clusters-arm-templates.md): learn how toocall Resource Manager templates toocreate HDInsight clusters.</span></span>

