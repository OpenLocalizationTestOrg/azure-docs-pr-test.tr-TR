---
title: "PowerShell - Azure Hdınsight kullanarak Hadoop kümeleri oluşturma | Microsoft Docs"
description: "Hadoop, HBase, Storm ve Spark kümeleri Linux'ta Hdınsight için Azure PowerShell kullanarak nasıl oluşturulacağını öğrenin."
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
ms.openlocfilehash: ca75974e6ec4f60739137d4cb5458bbfd735de3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-azure-powershell"></a><span data-ttu-id="1839d-103">Azure PowerShell kullanarak Hdınsight'ta Linux tabanlı kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="1839d-103">Create Linux-based clusters in HDInsight using Azure PowerShell</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="1839d-104">Azure PowerShell denetlemek ve dağıtımını ve yönetimini Microsoft Azure, iş yüklerini otomatikleştirmek için kullanabileceğiniz güçlü bir komut dosyası ortamıdır.</span><span class="sxs-lookup"><span data-stu-id="1839d-104">Azure PowerShell is a powerful scripting environment that you can use to control and automate the deployment and management of your workloads in Microsoft Azure.</span></span> <span data-ttu-id="1839d-105">Bu belge, Azure PowerShell kullanarak Linux tabanlı Hdınsight kümesi oluşturma hakkında bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="1839d-105">This document provides information about how to create a Linux-based HDInsight cluster by using Azure PowerShell.</span></span> <span data-ttu-id="1839d-106">Ayrıca, bir örnek komut dosyası içerir.</span><span class="sxs-lookup"><span data-stu-id="1839d-106">It also includes an example script.</span></span>

> [!NOTE]
> <span data-ttu-id="1839d-107">Azure PowerShell yalnızca Windows istemcileri üzerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="1839d-107">Azure PowerShell is only available on Windows clients.</span></span> <span data-ttu-id="1839d-108">Linux, Unix ya da Mac OS X istemci kullanıyorsanız, bkz: [Azure CLI kullanarak bir Linux tabanlı Hdınsight kümesi oluşturma](hdinsight-hadoop-create-linux-clusters-azure-cli.md) bir küme oluşturmak için Azure CLI kullanma hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="1839d-108">If you are using a Linux, Unix, or Mac OS X client, see [Create a Linux-based HDInsight cluster using Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) for information about using the Azure CLI to create a cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1839d-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="1839d-109">Prerequisites</span></span>
<span data-ttu-id="1839d-110">Bu yordama başlamadan önce şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="1839d-110">You must have the following before starting this procedure:</span></span>

* <span data-ttu-id="1839d-111">Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="1839d-111">An Azure subscription.</span></span> <span data-ttu-id="1839d-112">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="1839d-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* [<span data-ttu-id="1839d-113">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1839d-113">Azure PowerShell</span></span>](/powershell/azure/install-azurerm-ps)

    > [!IMPORTANT]
    > <span data-ttu-id="1839d-114">Azure Service Manager kullanılarak HDInsight kaynaklarının yönetilmesi için Azure PowerShell desteği **kullanım dışı bırakılmış** ve 1 Ocak 2017 tarihinde kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="1839d-114">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="1839d-115">Bu belgede yer alan adımlar, Azure Resource Manager ile çalışan yeni HDInsight cmdlet'lerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="1839d-115">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="1839d-116">Lütfen adımları [Azure PowerShell yükleme](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) Azure PowerShell'in en son sürümünü yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="1839d-116">Please follow the steps in [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="1839d-117">Azure Resource Manager’la çalışan yeni cmdlet’lerle kullanmak için değiştirilmesi gereken komut dosyalarınız varsa, daha fazla bilgi için bkz. [HDInsight kümeleri için Azure Resource Manager tabanlı geliştirme araçlarına geçme](hdinsight-hadoop-development-using-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="1839d-117">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

## <a name="create-cluster"></a><span data-ttu-id="1839d-118">Küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="1839d-118">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="1839d-119">Azure PowerShell kullanarak bir Hdınsight kümesi oluşturmak için aşağıdaki yordamları tamamlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="1839d-119">To create an HDInsight cluster by using Azure PowerShell, you must complete the following procedures:</span></span>

* <span data-ttu-id="1839d-120">Bir Azure kaynak grubu oluşturun</span><span class="sxs-lookup"><span data-stu-id="1839d-120">Create an Azure resource group</span></span>
* <span data-ttu-id="1839d-121">Azure Depolama hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="1839d-121">Create an Azure Storage account</span></span>
* <span data-ttu-id="1839d-122">Bir Azure Blob kapsayıcı oluşturun</span><span class="sxs-lookup"><span data-stu-id="1839d-122">Create an Azure Blob container</span></span>
* <span data-ttu-id="1839d-123">Hdınsight kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="1839d-123">Create an HDInsight cluster</span></span>

<span data-ttu-id="1839d-124">Aşağıdaki komut dosyasını yeni bir küme oluşturmak nasıl gösterir:</span><span class="sxs-lookup"><span data-stu-id="1839d-124">The following script demonstrates how to create a new cluster:</span></span>

<span data-ttu-id="1839d-125">[!code-powershell[Ana](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]</span><span class="sxs-lookup"><span data-stu-id="1839d-125">[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]</span></span>

<span data-ttu-id="1839d-126">Küme oturum açma için belirttiğiniz değerleri kümesi için Hadoop kullanıcı hesabı oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1839d-126">The values you specify for the cluster login are used to create the Hadoop user account for the cluster.</span></span> <span data-ttu-id="1839d-127">Web Uı'lar veya REST API'leri gibi küme üzerinde barındırılan hizmetlere bağlanmak için bu hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="1839d-127">Use this account to connect to services hosted on the cluster such as web UIs or REST APIs.</span></span>

<span data-ttu-id="1839d-128">SSH kullanıcı için belirlediğiniz değerler, küme için SSH kullanıcı oluşturmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="1839d-128">The values you specify for the SSH user are used to create the SSH user for the cluster.</span></span> <span data-ttu-id="1839d-129">Küme üzerinde uzak SSH oturumu başlatmak ve işlerini çalıştırmak için bu hesabı kullanın.</span><span class="sxs-lookup"><span data-stu-id="1839d-129">Use this account to start a remote SSH session on the cluster and run jobs.</span></span> <span data-ttu-id="1839d-130">Daha fazla bilgi için [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md) belgesine bakın.</span><span class="sxs-lookup"><span data-stu-id="1839d-130">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1839d-131">32'den fazla alt düğüm (ya da küme oluşturma veya Küme oluşturulduktan sonra ölçeklendirme tarafından) kullanmayı planlıyorsanız, ayrıca bir baş düğüm boyutu, en az 8 çekirdek ve 14 GB RAM belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="1839d-131">If you plan to use more than 32 worker nodes (either at cluster creation or by scaling the cluster after creation), you must also specify a head node size with at least 8 cores and 14 GB of RAM.</span></span>
>
> <span data-ttu-id="1839d-132">Düğümü boyutları ve ilişkili maliyetler hakkında daha fazla bilgi için bkz: [Hdınsight fiyatlandırma](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="1839d-132">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="1839d-133">Bir küme oluşturmak için 20 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="1839d-133">It can take up to 20 minutes to create a cluster.</span></span>

## <a name="create-cluster-configuration-object"></a><span data-ttu-id="1839d-134">Küme oluşturma: Yapılandırma nesnesi</span><span class="sxs-lookup"><span data-stu-id="1839d-134">Create cluster: Configuration object</span></span>

<span data-ttu-id="1839d-135">Ayrıca bir Hdınsight yapılandırma nesnesi kullanarak oluşturabileceğiniz `New-AzureRmHDInsightClusterConfig` cmdlet'i.</span><span class="sxs-lookup"><span data-stu-id="1839d-135">You can also create an HDInsight configuration object using `New-AzureRmHDInsightClusterConfig` cmdlet.</span></span> <span data-ttu-id="1839d-136">Kümeniz için ek yapılandırma seçeneklerini etkinleştirmek için bu yapılandırma nesnesi daha sonra değiştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1839d-136">You can then modify this configuration object to enable additional configuration options for your cluster.</span></span> <span data-ttu-id="1839d-137">Son olarak, `-Config` parametresinin `New-AzureRmHDInsightCluster` yapılandırmasını kullanmak için cmdlet.</span><span class="sxs-lookup"><span data-stu-id="1839d-137">Finally, use the `-Config` parameter of the `New-AzureRmHDInsightCluster` cmdlet to use the configuration.</span></span>

<span data-ttu-id="1839d-138">Aşağıdaki betiği Hdınsight küme türü üzerinde bir R Server yapılandırmak için bir yapılandırma nesnesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="1839d-138">The following script creates a configuration object to configure an R Server on HDInsight cluster type.</span></span> <span data-ttu-id="1839d-139">Yapılandırma, bir edge düğümünü, Rstudio'dan ve ek depolama alanı hesabı etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="1839d-139">The configuration enables an edge node, RStudio, and an additional storage account.</span></span>

<span data-ttu-id="1839d-140">[!code-powershell[Ana](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]</span><span class="sxs-lookup"><span data-stu-id="1839d-140">[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]</span></span>

> [!WARNING]
> <span data-ttu-id="1839d-141">Hdınsight kümesi farklı bir konumda bir depolama hesabıyla desteklenmiyor.</span><span class="sxs-lookup"><span data-stu-id="1839d-141">Using a storage account in a different location than the HDInsight cluster is not supported.</span></span> <span data-ttu-id="1839d-142">Bu örnek kullanırken, sunucu ile aynı konumda ek depolama alanı hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="1839d-142">When using this example, create the additional storage account in the same location as the server.</span></span>

## <a name="customize-clusters"></a><span data-ttu-id="1839d-143">Kümeleri özelleştirme</span><span class="sxs-lookup"><span data-stu-id="1839d-143">Customize clusters</span></span>

* <span data-ttu-id="1839d-144">Bkz: [önyükleme kullanarak özelleştirme Hdınsight kümelerini](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="1839d-144">See [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span></span>
* <span data-ttu-id="1839d-145">Bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="1839d-145">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="1839d-146">Küme silme</span><span class="sxs-lookup"><span data-stu-id="1839d-146">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="1839d-147">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="1839d-147">Troubleshoot</span></span>

<span data-ttu-id="1839d-148">HDInsight kümeleri oluştururken sorun yaşarsanız bkz. [erişim denetimi gereksinimleri](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="1839d-148">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="1839d-149">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="1839d-149">Next steps</span></span>

<span data-ttu-id="1839d-150">Hdınsight kümesi başarıyla oluşturuldu, kümenizi ile çalışmayı öğrenmek için aşağıdaki kaynakları kullanın.</span><span class="sxs-lookup"><span data-stu-id="1839d-150">Now that you have successfully created an HDInsight cluster, use the following resources to learn how to work with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="1839d-151">Hadoop kümeleri</span><span class="sxs-lookup"><span data-stu-id="1839d-151">Hadoop clusters</span></span>

* [<span data-ttu-id="1839d-152">HDInsight ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="1839d-152">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="1839d-153">HDInsight ile Pig kullanma</span><span class="sxs-lookup"><span data-stu-id="1839d-153">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="1839d-154">Hdınsight ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="1839d-154">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="1839d-155">HBase kümeleri</span><span class="sxs-lookup"><span data-stu-id="1839d-155">HBase clusters</span></span>

* [<span data-ttu-id="1839d-156">Hdınsight'ta HBase kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="1839d-156">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="1839d-157">Hdınsight'ta HBase için Java uygulamaları geliştirme</span><span class="sxs-lookup"><span data-stu-id="1839d-157">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="1839d-158">Storm kümeleri</span><span class="sxs-lookup"><span data-stu-id="1839d-158">Storm clusters</span></span>

* [<span data-ttu-id="1839d-159">Hdınsight üzerinde Storm için Java topolojisi geliştirme</span><span class="sxs-lookup"><span data-stu-id="1839d-159">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="1839d-160">Hdınsight üzerinde Storm Python bileşenleri kullanma</span><span class="sxs-lookup"><span data-stu-id="1839d-160">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="1839d-161">Dağıtma ve hdınsight'ta Storm topolojileri izleme</span><span class="sxs-lookup"><span data-stu-id="1839d-161">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a><span data-ttu-id="1839d-162">Spark kümeleri</span><span class="sxs-lookup"><span data-stu-id="1839d-162">Spark clusters</span></span>

* [<span data-ttu-id="1839d-163">Scala kullanarak tek başına uygulama oluşturma</span><span class="sxs-lookup"><span data-stu-id="1839d-163">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="1839d-164">Livy kullanarak Spark kümesinde işleri uzaktan çalıştırma</span><span class="sxs-lookup"><span data-stu-id="1839d-164">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="1839d-165">BI ile Spark: BI araçlarıyla HDInsight’ta Spark kullanarak etkileşimli veri çözümlemesi gerçekleştirme</span><span class="sxs-lookup"><span data-stu-id="1839d-165">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="1839d-166">Machine Learning ile Spark: Yemek inceleme sonuçlarını tahmin etmek için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="1839d-166">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="1839d-167">Spark Akış: Gerçek zamanlı akış uygulamaları oluşturmak için HDInsight’ta Spark kullanma</span><span class="sxs-lookup"><span data-stu-id="1839d-167">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

