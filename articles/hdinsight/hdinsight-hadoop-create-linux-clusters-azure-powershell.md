---
title: "aaaCreate Hadoop kümeleri PowerShell - Azure Hdınsight kullanarak | Microsoft Docs"
description: "Nasıl toocreate Hadoop, HBase, Storm ve Spark Linux'ta Hdınsight için Azure PowerShell kullanarak kümeleri hakkında bilgi edinin."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4208deca-d64a-45e1-8948-2673d5d7678c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 53afe4702f6b61a0720ceda48a4a34d7fa8797d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-azure-powershell"></a><span data-ttu-id="ad601-103">Azure PowerShell kullanarak Hdınsight'ta Linux tabanlı kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="ad601-103">Create Linux-based clusters in HDInsight using Azure PowerShell</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="ad601-104">Azure PowerShell toocontrol kullanın ve hello dağıtımını ve yönetimini Microsoft Azure, iş yüklerini otomatikleştirmek bir güçlü komut dosyası ortamıdır.</span><span class="sxs-lookup"><span data-stu-id="ad601-104">Azure PowerShell is a powerful scripting environment that you can use toocontrol and automate hello deployment and management of your workloads in Microsoft Azure.</span></span> <span data-ttu-id="ad601-105">Bu belge nasıl toocreate Linux tabanlı Hdınsight küme Azure PowerShell kullanarak hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="ad601-105">This document provides information about how toocreate a Linux-based HDInsight cluster by using Azure PowerShell.</span></span> <span data-ttu-id="ad601-106">Ayrıca, bir örnek komut dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="ad601-106">It also includes an example script.</span></span>

> [!NOTE]
> <span data-ttu-id="ad601-107">Azure PowerShell yalnızca Windows istemcileri üzerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ad601-107">Azure PowerShell is only available on Windows clients.</span></span> <span data-ttu-id="ad601-108">Linux, Unix ya da Mac OS X istemci kullanıyorsanız, bkz: [Azure CLI kullanarak bir Linux tabanlı Hdınsight kümesi oluşturma](hdinsight-hadoop-create-linux-clusters-azure-cli.md) hello Azure CLI toocreate bir küme kullanma hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="ad601-108">If you are using a Linux, Unix, or Mac OS X client, see [Create a Linux-based HDInsight cluster using Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) for information about using hello Azure CLI toocreate a cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ad601-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="ad601-109">Prerequisites</span></span>
<span data-ttu-id="ad601-110">Bu yordamı başlatmadan önce hello şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ad601-110">You must have hello following before starting this procedure:</span></span>

* <span data-ttu-id="ad601-111">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="ad601-111">An Azure subscription.</span></span> <span data-ttu-id="ad601-112">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="ad601-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* [<span data-ttu-id="ad601-113">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ad601-113">Azure PowerShell</span></span>](/powershell/azure/install-azurerm-ps)

    > [!IMPORTANT]
    > <span data-ttu-id="ad601-114">Azure Service Manager kullanılarak HDInsight kaynaklarının yönetilmesi için Azure PowerShell desteği **kullanım dışı bırakılmış** ve 1 Ocak 2017 tarihinde kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="ad601-114">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="ad601-115">Azure Resource Manager ile çalışan hello adımları bu belgenin kullanımı hello yeni Hdınsight cmdlet'lerini.</span><span class="sxs-lookup"><span data-stu-id="ad601-115">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="ad601-116">Lütfen başlangıç adımları [Azure PowerShell yükleme](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooinstall hello en son Azure PowerShell sürümü.</span><span class="sxs-lookup"><span data-stu-id="ad601-116">Please follow hello steps in [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="ad601-117">Komut dosyalarınız varsa bu gereksinimi toobe Azure Resource Manager ile çalışma toouse hello yeni cmdlet'leri değişiklik için bkz: [geçiş tooAzure Resource Manager tabanlı geliştirme araçları Hdınsight kümeleri için](hdinsight-hadoop-development-using-azure-resource-manager.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="ad601-117">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

## <a name="create-cluster"></a><span data-ttu-id="ad601-118">Küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="ad601-118">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="ad601-119">Azure PowerShell kullanarak bir Hdınsight kümesi toocreate hello yordamları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ad601-119">toocreate an HDInsight cluster by using Azure PowerShell, you must complete hello following procedures:</span></span>

* <span data-ttu-id="ad601-120">Bir Azure kaynak grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="ad601-120">Create an Azure resource group</span></span>
* <span data-ttu-id="ad601-121">Azure Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ad601-121">Create an Azure Storage account</span></span>
* <span data-ttu-id="ad601-122">Bir Azure Blob kapsayıcı oluşturun</span><span class="sxs-lookup"><span data-stu-id="ad601-122">Create an Azure Blob container</span></span>
* <span data-ttu-id="ad601-123">Hdınsight kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ad601-123">Create an HDInsight cluster</span></span>

<span data-ttu-id="ad601-124">Merhaba aşağıdaki komut dosyası gösterilmektedir nasıl toocreate yeni bir küme:</span><span class="sxs-lookup"><span data-stu-id="ad601-124">hello following script demonstrates how toocreate a new cluster:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]

<span data-ttu-id="ad601-125">Merhaba küme oturum açma için belirttiğiniz hello kullanılan toocreate hello hello kümesi için Hadoop kullanıcı hesabına değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="ad601-125">hello values you specify for hello cluster login are used toocreate hello Hadoop user account for hello cluster.</span></span> <span data-ttu-id="ad601-126">Bu hesap tooconnect tooservices web Uı'lar veya REST API'leri gibi hello kümesi üzerinde barındırılan kullanın.</span><span class="sxs-lookup"><span data-stu-id="ad601-126">Use this account tooconnect tooservices hosted on hello cluster such as web UIs or REST APIs.</span></span>

<span data-ttu-id="ad601-127">Merhaba SSH kullanıcı için belirttiğiniz hello hello kümesi için kullanılan toocreate hello SSH kullanıcı değerlerdir.</span><span class="sxs-lookup"><span data-stu-id="ad601-127">hello values you specify for hello SSH user are used toocreate hello SSH user for hello cluster.</span></span> <span data-ttu-id="ad601-128">Bu hesap uzak SSH oturumu toostart hello kümede ve işleri çalıştırma.</span><span class="sxs-lookup"><span data-stu-id="ad601-128">Use this account toostart a remote SSH session on hello cluster and run jobs.</span></span> <span data-ttu-id="ad601-129">Daha fazla bilgi için bkz: Merhaba [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md) belge.</span><span class="sxs-lookup"><span data-stu-id="ad601-129">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ad601-130">(Küme oluşturma sırasında veya ölçeklendirme hello Küme oluşturulduktan sonra) 32'den fazla çalışan düğümleri toouse planlıyorsanız, ayrıca bir baş düğüm boyutu, en az 8 çekirdek ve 14 GB RAM belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ad601-130">If you plan toouse more than 32 worker nodes (either at cluster creation or by scaling hello cluster after creation), you must also specify a head node size with at least 8 cores and 14 GB of RAM.</span></span>
>
> <span data-ttu-id="ad601-131">Düğümü boyutları ve ilişkili maliyetler hakkında daha fazla bilgi için bkz: [Hdınsight fiyatlandırma](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="ad601-131">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="ad601-132">Bir küme too20 dakika toocreate devam edebilir.</span><span class="sxs-lookup"><span data-stu-id="ad601-132">It can take up too20 minutes toocreate a cluster.</span></span>

## <a name="create-cluster-configuration-object"></a><span data-ttu-id="ad601-133">Küme oluşturma: Yapılandırma nesnesi</span><span class="sxs-lookup"><span data-stu-id="ad601-133">Create cluster: Configuration object</span></span>

<span data-ttu-id="ad601-134">Ayrıca bir Hdınsight yapılandırma nesnesi kullanarak oluşturabileceğiniz `New-AzureRmHDInsightClusterConfig` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="ad601-134">You can also create an HDInsight configuration object using `New-AzureRmHDInsightClusterConfig` cmdlet.</span></span> <span data-ttu-id="ad601-135">Bu yapılandırma nesnesi tooenable ek yapılandırma seçenekleri, kümeniz için daha sonra değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ad601-135">You can then modify this configuration object tooenable additional configuration options for your cluster.</span></span> <span data-ttu-id="ad601-136">Son olarak, hello kullan `-Config` hello parametresinin `New-AzureRmHDInsightCluster` cmdlet toouse hello yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="ad601-136">Finally, use hello `-Config` parameter of hello `New-AzureRmHDInsightCluster` cmdlet toouse hello configuration.</span></span>

<span data-ttu-id="ad601-137">Merhaba aşağıdaki betiği bir yapılandırma nesnesi tooconfigure bir R Server Hdınsight küme türü üzerinde oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ad601-137">hello following script creates a configuration object tooconfigure an R Server on HDInsight cluster type.</span></span> <span data-ttu-id="ad601-138">Merhaba yapılandırma bir edge düğümünü, Rstudio'dan ve ek depolama alanı hesabı etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="ad601-138">hello configuration enables an edge node, RStudio, and an additional storage account.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]

> [!WARNING]
> <span data-ttu-id="ad601-139">Merhaba Hdınsight kümesi farklı bir konumda bir depolama hesabıyla desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="ad601-139">Using a storage account in a different location than hello HDInsight cluster is not supported.</span></span> <span data-ttu-id="ad601-140">Bu örnek kullanırken hello hello ek depolama hesabı oluşturma hello sunucusu olarak aynı konumu.</span><span class="sxs-lookup"><span data-stu-id="ad601-140">When using this example, create hello additional storage account in hello same location as hello server.</span></span>

## <a name="customize-clusters"></a><span data-ttu-id="ad601-141">Kümeleri özelleştirme</span><span class="sxs-lookup"><span data-stu-id="ad601-141">Customize clusters</span></span>

* <span data-ttu-id="ad601-142">Bkz: [önyükleme kullanarak özelleştirme Hdınsight kümelerini](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="ad601-142">See [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span></span>
* <span data-ttu-id="ad601-143">Bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="ad601-143">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="ad601-144">Merhaba küme silme</span><span class="sxs-lookup"><span data-stu-id="ad601-144">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="ad601-145">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="ad601-145">Troubleshoot</span></span>

<span data-ttu-id="ad601-146">HDInsight kümeleri oluştururken sorun yaşarsanız bkz. [erişim denetimi gereksinimleri](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="ad601-146">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad601-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ad601-147">Next steps</span></span>

<span data-ttu-id="ad601-148">Hdınsight kümesi başarıyla oluşturduğunuza göre kaynakları toolearn nasıl aşağıdaki hello kullanmak toowork kümenizi ile.</span><span class="sxs-lookup"><span data-stu-id="ad601-148">Now that you have successfully created an HDInsight cluster, use hello following resources toolearn how toowork with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="ad601-149">Hadoop kümeleri</span><span class="sxs-lookup"><span data-stu-id="ad601-149">Hadoop clusters</span></span>

* [<span data-ttu-id="ad601-150">HDInsight ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="ad601-150">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="ad601-151">HDInsight ile Pig kullanma</span><span class="sxs-lookup"><span data-stu-id="ad601-151">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="ad601-152">Hdınsight ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="ad601-152">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="ad601-153">HBase kümeleri</span><span class="sxs-lookup"><span data-stu-id="ad601-153">HBase clusters</span></span>

* [<span data-ttu-id="ad601-154">Hdınsight'ta HBase kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="ad601-154">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="ad601-155">Hdınsight'ta HBase için Java uygulamaları geliştirme</span><span class="sxs-lookup"><span data-stu-id="ad601-155">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="ad601-156">Storm kümeleri</span><span class="sxs-lookup"><span data-stu-id="ad601-156">Storm clusters</span></span>

* [<span data-ttu-id="ad601-157">Hdınsight üzerinde Storm için Java topolojisi geliştirme</span><span class="sxs-lookup"><span data-stu-id="ad601-157">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="ad601-158">Hdınsight üzerinde Storm Python bileşenleri kullanma</span><span class="sxs-lookup"><span data-stu-id="ad601-158">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="ad601-159">Dağıtma ve hdınsight'ta Storm topolojileri izleme</span><span class="sxs-lookup"><span data-stu-id="ad601-159">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a><span data-ttu-id="ad601-160">Spark kümeleri</span><span class="sxs-lookup"><span data-stu-id="ad601-160">Spark clusters</span></span>

* [<span data-ttu-id="ad601-161">Scala kullanarak tek başına uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="ad601-161">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="ad601-162">Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma</span><span class="sxs-lookup"><span data-stu-id="ad601-162">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="ad601-163">BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="ad601-163">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="ad601-164">Machine Learning ile Spark: Spark Hdınsight toopredict yemek İnceleme sonuçlarını içinde kullanma</span><span class="sxs-lookup"><span data-stu-id="ad601-164">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="ad601-165">Spark Akış: Gerçek zamanlı akış uygulamaları oluşturmak için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="ad601-165">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

