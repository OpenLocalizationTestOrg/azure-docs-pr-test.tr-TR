---
title: "komut dosyası Eylemler - Azure Hdınsight kümeleri aaaCustomize kullanarak | Microsoft Docs"
description: "Betik eylemi kullanarak nasıl toocustomize Hdınsight kümeleri hakkında bilgi edinin."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3a63e216-4163-40c1-aa04-6b42fd0162ad
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 076fff23e016db47bc7e9963582a545ad638e691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="customize-windows-based-hdinsight-clusters-using-script-action"></a><span data-ttu-id="2abc2-103">Betik eylemi kullanarak Windows tabanlı Hdınsight kümelerini özelleştirme</span><span class="sxs-lookup"><span data-stu-id="2abc2-103">Customize Windows-based HDInsight clusters using Script Action</span></span>
<span data-ttu-id="2abc2-104">**Betik eylemi** kullanılan tooinvoke olabilir [özel komut dosyaları](hdinsight-hadoop-script-actions.md) bir kümede ek yazılım yüklemek için hello küme oluşturma işlemi sırasında.</span><span class="sxs-lookup"><span data-stu-id="2abc2-104">**Script Action** can be used tooinvoke [custom scripts](hdinsight-hadoop-script-actions.md) during hello cluster creation process for installing additional software on a cluster.</span></span>

<span data-ttu-id="2abc2-105">Bu makaledeki Hello bilgiler belirli tooWindows tabanlı Hdınsight kümeleri ' dir.</span><span class="sxs-lookup"><span data-stu-id="2abc2-105">hello information in this article is specific tooWindows-based HDInsight clusters.</span></span> <span data-ttu-id="2abc2-106">Linux tabanlı kümeler için bkz: [özelleştirme Linux tabanlı Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="2abc2-106">For Linux-based clusters, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2abc2-107">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="2abc2-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2abc2-108">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="2abc2-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="2abc2-109">Hdınsight kümeleri dahil olmak üzere ek Azure depolama hesapları gibi başka yöntemlerle de, çeşitli özelleştirilebilir, hello Hadoop değiştirme yapılandırma dosyaları (core-site.xml, hive-site.xml, vb.) veya paylaşılan içine kitaplıklar (örn., Hive, Oozie) ekleme Merhaba küme ortak konumlarda.</span><span class="sxs-lookup"><span data-stu-id="2abc2-109">HDInsight clusters can be customized in a variety of other ways as well, such as including additional Azure Storage accounts, changing hello Hadoop configuration files (core-site.xml, hive-site.xml, etc.), or adding shared libraries (e.g., Hive, Oozie) into common locations in hello cluster.</span></span> <span data-ttu-id="2abc2-110">Bu özelleştirmeler hello Azure Hdınsight .NET SDK'sı, Azure PowerShell aracılığıyla yapılabilir veya Azure portal hello.</span><span class="sxs-lookup"><span data-stu-id="2abc2-110">These customizations can be done through Azure PowerShell, hello Azure HDInsight .NET SDK, or hello Azure portal.</span></span> <span data-ttu-id="2abc2-111">Daha fazla bilgi için bkz: [Hdınsight'ta oluşturmak Hadoop kümeleri][hdinsight-provision-cluster].</span><span class="sxs-lookup"><span data-stu-id="2abc2-111">For more information, see [Create Hadoop clusters in HDInsight][hdinsight-provision-cluster].</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell-cli-and-dotnet-sdk.md)]

## <a name="script-action-in-hello-cluster-creation-process"></a><span data-ttu-id="2abc2-112">Betik eylemi hello küme oluşturma işlemi</span><span class="sxs-lookup"><span data-stu-id="2abc2-112">Script Action in hello cluster creation process</span></span>
<span data-ttu-id="2abc2-113">Bir küme oluşturulmakta hello işlemi içinde iken betik eylemi yalnızca kullanılır.</span><span class="sxs-lookup"><span data-stu-id="2abc2-113">Script Action is only used while a cluster is in hello process of being created.</span></span> <span data-ttu-id="2abc2-114">Betik eylemi hello oluşturma işlemi sırasında çalıştırıldığında hello Aşağıdaki diyagramda gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="2abc2-114">hello following diagram illustrates when Script Action is executed during hello creation process:</span></span>

<span data-ttu-id="2abc2-115">![Hdınsight küme özelleştirme ve küme oluşturma sırasında aşamaları][img-hdi-cluster-states]</span><span class="sxs-lookup"><span data-stu-id="2abc2-115">![HDInsight cluster customization and stages during cluster creation][img-hdi-cluster-states]</span></span>

<span data-ttu-id="2abc2-116">Merhaba komut dosyası çalıştırılırken hello küme hello girer **ClusterCustomization** aşaması.</span><span class="sxs-lookup"><span data-stu-id="2abc2-116">When hello script is running, hello cluster enters hello **ClusterCustomization** stage.</span></span> <span data-ttu-id="2abc2-117">Bu aşamada hello betik hello sistem yönetici hesabı altında çalışır, tüm hello üzerinde paralel hello kümedeki düğümler belirtilen ve hello düğümler üzerinde tam yönetici ayrıcalıkları sağlar.</span><span class="sxs-lookup"><span data-stu-id="2abc2-117">At this stage, hello script is run under hello system admin account, in parallel on all hello specified nodes in hello cluster, and provides full admin privileges on hello nodes.</span></span>

> [!NOTE]
> <span data-ttu-id="2abc2-118">Sırasında hello küme düğümleri üzerinde yönetici ayrıcalıklarına sahip olduğundan **ClusterCustomization** aşama, durdurma ve Hadoop ile ilgili hizmetlerin gibi hizmetler başlatma gibi hello betik tooperform işlemleri kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="2abc2-118">Because you have admin privileges on hello cluster nodes during the **ClusterCustomization** stage, you can use hello script tooperform operations like stopping and starting services, including Hadoop-related services.</span></span> <span data-ttu-id="2abc2-119">Merhaba komut dosyasının bir parçası olarak emin olmalısınız, hello komut dosyası çalıştırma tamamlanmadan önce bu hello Ambari Hizmetleri ve diğer Hadoop ile ilgili hizmetlerin hazır ve çalışır; dolayısıyla.</span><span class="sxs-lookup"><span data-stu-id="2abc2-119">So, as part of hello script, you must ensure that hello Ambari services and other Hadoop-related services are up and running before hello script finishes running.</span></span> <span data-ttu-id="2abc2-120">Bu hizmetler gerekli toosuccessfully, hello sağlık ve hello küme durumunu, oluşturulurken onaylaması.</span><span class="sxs-lookup"><span data-stu-id="2abc2-120">These services are required toosuccessfully ascertain hello health and state of hello cluster while it is being created.</span></span> <span data-ttu-id="2abc2-121">Bu hizmetler etkiler kümedeki herhangi bir yapılandırma değiştirirseniz, sağlanan hello yardımcı işlevleri kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2abc2-121">If you change any configuration on the cluster that affects these services, you must use hello helper functions that are provided.</span></span> <span data-ttu-id="2abc2-122">Yardımcı işlevleri hakkında daha fazla bilgi için bkz: [Hdınsight betik eylemi geliştirme betikleri][hdinsight-write-script].</span><span class="sxs-lookup"><span data-stu-id="2abc2-122">For more information about helper functions, see [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>
>
>

<span data-ttu-id="2abc2-123">Hello çıkış ve hello Hata günlüklerini hello komut dosyası için hello küme için belirtilen hello varsayılan depolama hesabında depolanır.</span><span class="sxs-lookup"><span data-stu-id="2abc2-123">hello output and hello error logs for hello script are stored in hello default Storage account you specified for hello cluster.</span></span> <span data-ttu-id="2abc2-124">Merhaba günlükleri hello adı olan bir tabloda depolanır **u < \cluster-name-fragment >< \time-stamp > setuplog**.</span><span class="sxs-lookup"><span data-stu-id="2abc2-124">hello logs are stored in a table with hello name **u<\cluster-name-fragment><\time-stamp>setuplog**.</span></span> <span data-ttu-id="2abc2-125">Merhaba betiği tüm düğümlerde hello (baş düğüm ve çalışan düğümleri) hello küme Çalıştır toplama günlüklerinden bunlar.</span><span class="sxs-lookup"><span data-stu-id="2abc2-125">These are aggregate logs from hello script run on all hello nodes (head node and worker nodes) in hello cluster.</span></span>

<span data-ttu-id="2abc2-126">Her küme belirtilen hello sırayla çağrılır birden çok betik eylemleri kabul edebilir.</span><span class="sxs-lookup"><span data-stu-id="2abc2-126">Each cluster can accept multiple script actions that are invoked in hello order in which they are specified.</span></span> <span data-ttu-id="2abc2-127">Bir komut dosyasını olması çalıştıran hello baş düğüm, hello çalışan düğümleri veya her ikisi de.</span><span class="sxs-lookup"><span data-stu-id="2abc2-127">A script can be ran on hello head node, hello worker nodes, or both.</span></span>

<span data-ttu-id="2abc2-128">Hdınsight Hdınsight kümelerinde bileşenleri aşağıdaki birkaç betikleri tooinstall hello sağlar:</span><span class="sxs-lookup"><span data-stu-id="2abc2-128">HDInsight provides several scripts tooinstall hello following components on HDInsight clusters:</span></span>

| <span data-ttu-id="2abc2-129">Ad</span><span class="sxs-lookup"><span data-stu-id="2abc2-129">Name</span></span> | <span data-ttu-id="2abc2-130">Betik</span><span class="sxs-lookup"><span data-stu-id="2abc2-130">Script</span></span> |
| --- | --- |
| <span data-ttu-id="2abc2-131">**Spark yükleyin**</span><span class="sxs-lookup"><span data-stu-id="2abc2-131">**Install Spark**</span></span> |<span data-ttu-id="2abc2-132">https://hdiconfigactions.BLOB.Core.Windows.NET/sparkconfigactionv03/Spark-installer-v03.ps1.</span><span class="sxs-lookup"><span data-stu-id="2abc2-132">https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1.</span></span> <span data-ttu-id="2abc2-133">Bkz: [yükleme ve kullanma hdınsight'ta Spark kümeleri][hdinsight-install-spark].</span><span class="sxs-lookup"><span data-stu-id="2abc2-133">See [Install and use Spark on HDInsight clusters][hdinsight-install-spark].</span></span> |
| <span data-ttu-id="2abc2-134">**R yükleme**</span><span class="sxs-lookup"><span data-stu-id="2abc2-134">**Install R**</span></span> |<span data-ttu-id="2abc2-135">https://hdiconfigactions.BLOB.Core.Windows.NET/rconfigactionv02/r-installer-v02.ps1.</span><span class="sxs-lookup"><span data-stu-id="2abc2-135">https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1.</span></span> <span data-ttu-id="2abc2-136">Bkz: [yükleme ve kullanma R Hdınsight kümelerinde][hdinsight-install-r].</span><span class="sxs-lookup"><span data-stu-id="2abc2-136">See [Install and use R on HDInsight clusters][hdinsight-install-r].</span></span> |
| <span data-ttu-id="2abc2-137">**Solr yükleyin**</span><span class="sxs-lookup"><span data-stu-id="2abc2-137">**Install Solr**</span></span> |<span data-ttu-id="2abc2-138">https://hdiconfigactions.BLOB.Core.Windows.NET/solrconfigactionv01/solr-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="2abc2-138">https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1.</span></span> <span data-ttu-id="2abc2-139">Bkz: [yükleme ve kullanma Solr hdınsight kümeleri](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="2abc2-139">See [Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span> |
| <span data-ttu-id="2abc2-140">- **Giraph yükleyin**</span><span class="sxs-lookup"><span data-stu-id="2abc2-140">- **Install Giraph**</span></span> |<span data-ttu-id="2abc2-141">https://hdiconfigactions.BLOB.Core.Windows.NET/giraphconfigactionv01/giraph-installer-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="2abc2-141">https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1.</span></span> <span data-ttu-id="2abc2-142">Bkz: [yükleme ve kullanma Giraph hdınsight kümeleri](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="2abc2-142">See [Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span> |
| <span data-ttu-id="2abc2-143">**Ön yük Hıve kitaplıkları**</span><span class="sxs-lookup"><span data-stu-id="2abc2-143">**Pre-load Hive libraries**</span></span> |<span data-ttu-id="2abc2-144">https://hdiconfigactions.BLOB.Core.Windows.NET/setupcustomhivelibsv01/Setup-customhivelibs-v01.ps1.</span><span class="sxs-lookup"><span data-stu-id="2abc2-144">https://hdiconfigactions.blob.core.windows.net/setupcustomhivelibsv01/setup-customhivelibs-v01.ps1.</span></span> <span data-ttu-id="2abc2-145">Bkz: [eklemek Hive kitaplıkları Hdınsight kümeleri hakkında](hdinsight-hadoop-add-hive-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="2abc2-145">See [Add Hive libraries on HDInsight clusters](hdinsight-hadoop-add-hive-libraries.md)</span></span> |

## <a name="call-scripts-using-hello-azure-portal"></a><span data-ttu-id="2abc2-146">Hello Azure portal kullanarak komut dosyalarını arayın</span><span class="sxs-lookup"><span data-stu-id="2abc2-146">Call scripts using hello Azure portal</span></span>
<span data-ttu-id="2abc2-147">**Azure portal Hello**</span><span class="sxs-lookup"><span data-stu-id="2abc2-147">**From hello Azure portal**</span></span>

1. <span data-ttu-id="2abc2-148">Konusunda açıklandığı gibi bir küme oluşturmaya başlamak [Hdınsight'ta oluşturmak Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="2abc2-148">Start creating a cluster as described at [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
2. <span data-ttu-id="2abc2-149">Hello için isteğe bağlı yapılandırma bölümünde **betik eylemleri** dikey penceresinde tıklatın **betik eylemi eklemek** tooprovide aşağıda gösterildiği gibi hello betik eylemi hakkında ayrıntıları:</span><span class="sxs-lookup"><span data-stu-id="2abc2-149">Under Optional Configuration, for hello **Script Actions** blade, click **add script action** tooprovide details about hello script action, as shown below:</span></span>

    <span data-ttu-id="2abc2-150">![Betik eylemi toocustomize bir küme kullanın](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "kullanım betik eylemi toocustomize küme")</span><span class="sxs-lookup"><span data-stu-id="2abc2-150">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-customize-cluster/HDI.CreateCluster.8.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="2abc2-151">Özellik</span><span class="sxs-lookup"><span data-stu-id="2abc2-151">Property</span></span></th><th><span data-ttu-id="2abc2-152">Değer</span><span class="sxs-lookup"><span data-stu-id="2abc2-152">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="2abc2-153">Ad</span><span class="sxs-lookup"><span data-stu-id="2abc2-153">Name</span></span></td>
            <td><span data-ttu-id="2abc2-154">Merhaba betik eylemi için bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="2abc2-154">Specify a name for hello script action.</span></span></td></tr>
        <tr><td><span data-ttu-id="2abc2-155">Betik URI'si</span><span class="sxs-lookup"><span data-stu-id="2abc2-155">Script URI</span></span></td>
            <td><span data-ttu-id="2abc2-156">Çağrılan toocustomize hello küme hello URI toohello komut dosyasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="2abc2-156">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span> <span data-ttu-id="2abc2-157">s</span><span class="sxs-lookup"><span data-stu-id="2abc2-157">s</span></span></td></tr>
        <tr><td><span data-ttu-id="2abc2-158">HEAD/çalışan</span><span class="sxs-lookup"><span data-stu-id="2abc2-158">Head/Worker</span></span></td>
            <td><span data-ttu-id="2abc2-159">Merhaba düğüm belirtin (**Head** veya **çalışan**) hangi hello özelleştirme betiğini çalıştırın.</b>.</span><span class="sxs-lookup"><span data-stu-id="2abc2-159">Specify hello nodes (**Head** or **Worker**) on which hello customization script is run.</b>.</span></span>
        <tr><td><span data-ttu-id="2abc2-160">Parametreler</span><span class="sxs-lookup"><span data-stu-id="2abc2-160">Parameters</span></span></td>
            <td><span data-ttu-id="2abc2-161">Merhaba komut dosyası için gereken Hello parametreleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="2abc2-161">Specify hello parameters, if required by hello script.</span></span></td></tr>
    </table>

    <span data-ttu-id="2abc2-162">Birden çok bileşeni tek bir betik eylemi tooinstall birden çok ENTER tooadd hello kümede tuşuna basın.</span><span class="sxs-lookup"><span data-stu-id="2abc2-162">Press ENTER tooadd more than one script action tooinstall multiple components on hello cluster.</span></span>
3. <span data-ttu-id="2abc2-163">Tıklatın **seçin** toosave hello betik eylemi yapılandırmasını ve küme oluşturma ile devam edin.</span><span class="sxs-lookup"><span data-stu-id="2abc2-163">Click **Select** toosave hello script action configuration and continue with cluster creation.</span></span>

## <a name="call-scripts-using-azure-powershell"></a><span data-ttu-id="2abc2-164">Azure PowerShell kullanarak komut dosyalarını arayın</span><span class="sxs-lookup"><span data-stu-id="2abc2-164">Call scripts using Azure PowerShell</span></span>
<span data-ttu-id="2abc2-165">Bu aşağıdaki PowerShell betiğini tooinstall Windows üzerinde Spark Hdınsight kümesi nasıl dayalı gösterir.</span><span class="sxs-lookup"><span data-stu-id="2abc2-165">This following PowerShell script demonstrates how tooinstall Spark on Windows based HDInsight cluster.</span></span>  

    # Provide values for these variables
    $subscriptionID = "<Azure Suscription ID>" # After "Login-AzureRmAccount", use "Get-AzureRmSubscription" toolist IDs.

    $nameToken = "<Enter A Name Token>"  # hello token is use toocreate Azure service names.
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")

    $resourceGroupName = $namePrefix + "rg"
    $location = "EAST US 2" # used for creating resource group, storage account, and HDInsight cluster.

    $hdinsightClusterName = $namePrefix + "spark"
    $httpUserName = "admin"
    $httpPassword = "<Enter a Password>"

    $defaultStorageAccountName = "$namePrefix" + "store"
    $defaultBlobContainerName = $hdinsightClusterName

    #############################################################
    # Connect tooAzure
    #############################################################

    Try{
        Get-AzureRmSubscription
    }
    Catch{
        Login-AzureRmAccount
    }
    Select-AzureRmSubscription -SubscriptionId $subscriptionID

    #############################################################
    # Prepare hello dependent components
    #############################################################

    # Create resource group
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location

    # Create storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_GRS
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                    -StorageAccountName $defaultStorageAccountName `
                                    -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext

    #############################################################
    # Create cluster with ApacheSpark
    #############################################################

    # Specify hello configuration options
    $config = New-AzureRmHDInsightClusterConfig `
                -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
                -DefaultStorageAccountKey $defaultStorageAccountKey


    # Add a script action toohello cluster configuration
    $config = Add-AzureRmHDInsightScriptAction `
                -Config $config `
                -Name "Install Spark" `
                -NodeType HeadNode `
                -Uri https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1 `

    # Start creating a cluster with Spark installed
    New-AzureRmHDInsightCluster `
            -ResourceGroupName $resourceGroupName `
            -ClusterName $hdinsightClusterName `
            -Location $location `
            -ClusterSizeInNodes 2 `
            -ClusterType Hadoop `
            -OSType Windows `
            -DefaultStorageContainer $defaultBlobContainerName `
            -Config $config


<span data-ttu-id="2abc2-166">tooinstall diğer yazılım ihtiyacınız olacak hello betik tooreplace hello komut dosyası:</span><span class="sxs-lookup"><span data-stu-id="2abc2-166">tooinstall other software, you will need tooreplace hello script file in hello script:</span></span>

<span data-ttu-id="2abc2-167">İstendiğinde, hello küme için hello kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="2abc2-167">When prompted, enter hello credentials for hello cluster.</span></span> <span data-ttu-id="2abc2-168">Merhaba küme oluşturulmadan önce birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="2abc2-168">It can take several minutes before hello cluster is created.</span></span>

## <a name="call-scripts-using-net-sdk"></a><span data-ttu-id="2abc2-169">.NET SDK kullanarak komut dosyalarını arayın</span><span class="sxs-lookup"><span data-stu-id="2abc2-169">Call scripts using .NET SDK</span></span>
<span data-ttu-id="2abc2-170">Merhaba aşağıdaki örnek tooinstall Windows üzerinde Spark Hdınsight kümesi nasıl dayalı gösterir.</span><span class="sxs-lookup"><span data-stu-id="2abc2-170">hello following sample demonstrates how tooinstall Spark on Windows based HDInsight cluster.</span></span> <span data-ttu-id="2abc2-171">tooinstall diğer yazılım ihtiyacınız olacak hello kod tooreplace hello komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="2abc2-171">tooinstall other software, you will need tooreplace hello script file in hello code.</span></span>

<span data-ttu-id="2abc2-172">**toocreate Spark Hdınsight kümesiyle**</span><span class="sxs-lookup"><span data-stu-id="2abc2-172">**toocreate an HDInsight cluster with Spark**</span></span>

1. <span data-ttu-id="2abc2-173">Visual Studio'da bir C# konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2abc2-173">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="2abc2-174">Hello ifadesini Nuget Paket Yöneticisi konsolu hello aşağıdaki komutu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="2abc2-174">From hello Nuget Package Manager Console, run hello following command.</span></span>

        Install-Package Microsoft.Rest.ClientRuntime.Azure.Authentication -Pre
        Install-Package Microsoft.Azure.Management.ResourceManager -Pre
        Install-Package Microsoft.Azure.Management.HDInsight
3. <span data-ttu-id="2abc2-175">Using deyimleri hello Program.cs dosyasında aşağıdaki kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="2abc2-175">Use hello following using statements in hello Program.cs file:</span></span>

        using System;
        using System.Security;
        using Microsoft.Azure;
        using Microsoft.Azure.Management.HDInsight;
        using Microsoft.Azure.Management.HDInsight.Models;
        using Microsoft.Azure.Management.ResourceManager;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest;
        using Microsoft.Rest.Azure.Authentication;
4. <span data-ttu-id="2abc2-176">Merhaba kodu hello aşağıdaki hello sınıfıyla yerleştirin:</span><span class="sxs-lookup"><span data-stu-id="2abc2-176">Place hello code in hello class with hello following:</span></span>

        private static HDInsightManagementClient _hdiManagementClient;

        // Replace with your AAD tenant ID if necessary
        private const string TenantId = UserTokenProvider.CommonTenantId;
        private const string SubscriptionId = "<Your Azure Subscription ID>";
        // This is hello GUID for hello PowerShell client. Used for interactive logins in this example.
        private const string ClientId = "1950a258-227b-4e31-a9cf-717495945fc2";
        private const string ResourceGroupName = "<ExistingAzureResourceGroupName>";
        private const string NewClusterName = "<NewAzureHDInsightClusterName>";
        private const int NewClusterNumWorkerNodes = 2;
        private const string NewClusterLocation = "East US";
        private const string NewClusterVersion = "3.2";
        private const string ExistingStorageName = "<ExistingAzureStorageAccountName>";
        private const string ExistingStorageKey = "<ExistingAzureStorageAccountKey>";
        private const string ExistingContainer = "<ExistingAzureBlobStorageContainer>";
        private const string NewClusterType = "Hadoop";
        private const OSType NewClusterOSType = OSType.Windows;
        private const string NewClusterUsername = "<HttpUserName>";
        private const string NewClusterPassword = "<HttpUserPassword>";

        static void Main(string[] args)
        {
            System.Console.WriteLine("Running");

            // Authenticate and get a token
            var authToken = Authenticate(TenantId, ClientId, SubscriptionId);
            // Flag subscription for HDInsight, if it isn't already.
            EnableHDInsight(authToken);
            // Get an HDInsight management client
            _hdiManagementClient = new HDInsightManagementClient(authToken);

            CreateCluster();
        }

        private static void CreateCluster()
        {
            var parameters = new ClusterCreateParameters
            {
                ClusterSizeInNodes = NewClusterNumWorkerNodes,
                Location = NewClusterLocation,
                ClusterType = NewClusterType,
                OSType = NewClusterOSType,
                Version = NewClusterVersion,
                DefaultStorageInfo = new AzureStorageInfo(ExistingStorageName, ExistingStorageKey, ExistingContainer),
                UserName = NewClusterUsername,
                Password = NewClusterPassword,
            };

            ScriptAction sparkScriptAction = new ScriptAction("Install Spark",
                new Uri("https://hdiconfigactions.blob.core.windows.net/sparkconfigactionv03/spark-installer-v03.ps1"), "");

            parameters.ScriptActions.Add(ClusterNodeType.HeadNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });
            parameters.ScriptActions.Add(ClusterNodeType.WorkerNode, new System.Collections.Generic.List<ScriptAction> { sparkScriptAction });

            _hdiManagementClient.Clusters.Create(ResourceGroupName, NewClusterName, parameters);
        }

        /// <summary>
        /// Authenticate tooan Azure subscription and retrieve an authentication token
        /// </summary>
        /// <param name="TenantId">hello AAD tenant ID</param>
        /// <param name="ClientId">hello AAD client ID</param>
        /// <param name="SubscriptionId">hello Azure subscription ID</param>
        /// <returns></returns>
        static TokenCloudCredentials Authenticate(string TenantId, string ClientId, string SubscriptionId)
        {
            var authContext = new AuthenticationContext("https://login.microsoftonline.com/" + TenantId);
            var tokenAuthResult = authContext.AcquireToken("https://management.core.windows.net/",
                ClientId,
                new Uri("urn:ietf:wg:oauth:2.0:oob"),
                PromptBehavior.Always,
                UserIdentifier.AnyUser);
            return new TokenCloudCredentials(SubscriptionId, tokenAuthResult.AccessToken);
        }
        /// <summary>
        /// Marks your subscription as one that can use HDInsight, if it has not already been marked as such.
        /// </summary>
        /// <remarks>This is essentially a one-time action; if you have already done something with HDInsight
        /// on your subscription, then this isn't needed at all and will do nothing.</remarks>
        /// <param name="authToken">An authentication token for your Azure subscription</param>
        static void EnableHDInsight(TokenCloudCredentials authToken)
        {
            // Create a client for hello Resource manager and set hello subscription ID
            var resourceManagementClient = new ResourceManagementClient(new TokenCredentials(authToken.Token));
            resourceManagementClient.SubscriptionId = SubscriptionId;
            // Register hello HDInsight provider
            var rpResult = resourceManagementClient.Providers.Register("Microsoft.HDInsight");
        }
5. <span data-ttu-id="2abc2-177">Tuşuna **F5** toorun Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="2abc2-177">Press **F5** toorun hello application.</span></span>

## <a name="support-for-open-source-software-used-on-hdinsight-clusters"></a><span data-ttu-id="2abc2-178">Hdınsight kümelerinde kullanılan açık kaynaklı yazılım desteği</span><span class="sxs-lookup"><span data-stu-id="2abc2-178">Support for open-source software used on HDInsight clusters</span></span>
<span data-ttu-id="2abc2-179">Merhaba Microsoft Azure Hdınsight hizmeti bir ekosistemi Hadoop biçimlendirilmiş açık kaynak teknolojileri kullanarak toobuild büyük veri uygulamaları hello bulutta sağlayan esnek bir platformdur.</span><span class="sxs-lookup"><span data-stu-id="2abc2-179">hello Microsoft Azure HDInsight service is a flexible platform that enables you toobuild big-data applications in hello cloud by using an ecosystem of open-source technologies formed around Hadoop.</span></span> <span data-ttu-id="2abc2-180">Microsoft Azure hello açıklandığı gibi bu genel düzeyde bir destek açık kaynak teknolojileri için sağlar **destek kapsamı** hello bölümünü <a href="http://azure.microsoft.com/support/faq/" target="_blank">Azure destek SSS Web sitesine</a>.</span><span class="sxs-lookup"><span data-stu-id="2abc2-180">Microsoft Azure provides a general level of support for open-source technologies, as discussed in hello **Support Scope** section of hello <a href="http://azure.microsoft.com/support/faq/" target="_blank">Azure Support FAQ website</a>.</span></span> <span data-ttu-id="2abc2-181">Merhaba Hdınsight hizmeti, aşağıda açıklandığı gibi ek düzeyde hello bileşenlerinin bazılarını desteği sağlar.</span><span class="sxs-lookup"><span data-stu-id="2abc2-181">hello HDInsight service provides an additional level of support for some of hello components, as described below.</span></span>

<span data-ttu-id="2abc2-182">Merhaba Hdınsight hizmeti açık kaynak bileşenlerini iki tür vardır:</span><span class="sxs-lookup"><span data-stu-id="2abc2-182">There are two types of open-source components that are available in hello HDInsight service:</span></span>

* <span data-ttu-id="2abc2-183">**Yerleşik bileşenlerini** -bu bileşenler Hdınsight kümelerinde önceden yüklenmiş ve hello küme çekirdek işlevselliğini sağlar.</span><span class="sxs-lookup"><span data-stu-id="2abc2-183">**Built-in components** - These components are pre-installed on HDInsight clusters and provide core functionality of hello cluster.</span></span> <span data-ttu-id="2abc2-184">Örneğin, YARN ResourceManager, hello Hive sorgu dili (HiveQL) ve hello Mahout kitaplık toothis kategori ait.</span><span class="sxs-lookup"><span data-stu-id="2abc2-184">For example, YARN ResourceManager, hello Hive query language (HiveQL), and hello Mahout library belong toothis category.</span></span> <span data-ttu-id="2abc2-185">Küme bileşenlerin tam bir listesi kullanılabilir [Hdınsight tarafından sağlanan hello Hadoop küme sürümlerindeki yenilikler nelerdir?](hdinsight-component-versioning.md) </a>.</span><span class="sxs-lookup"><span data-stu-id="2abc2-185">A full list of cluster components is available in [What's new in hello Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md)</a>.</span></span>
* <span data-ttu-id="2abc2-186">**Özel bileşenler** -, hello küme, bir kullanıcı olarak yükleyebilir veya herhangi bir bileşeni hello topluluk bulunan ya da sizin tarafınızdan oluşturulan, iş yükü kullanın.</span><span class="sxs-lookup"><span data-stu-id="2abc2-186">**Custom components** - You, as a user of hello cluster, can install or use in your workload any component available in hello community or created by you.</span></span>

<span data-ttu-id="2abc2-187">Yerleşik bileşenlerini tam olarak desteklenir ve Microsoft Support tooisolate Yardım ve sorunları ilgili toothese bileşenler çözümlenemiyor.</span><span class="sxs-lookup"><span data-stu-id="2abc2-187">Built-in components are fully supported, and Microsoft Support will help tooisolate and resolve issues related toothese components.</span></span>

> [!WARNING]
> <span data-ttu-id="2abc2-188">Merhaba Hdınsight kümesi ile sağlanan bileşenler tam olarak desteklenir ve Microsoft Support tooisolate Yardım ve sorunları ilgili toothese bileşenler çözümlenemiyor.</span><span class="sxs-lookup"><span data-stu-id="2abc2-188">Components provided with hello HDInsight cluster are fully supported and Microsoft Support will help tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="2abc2-189">Özel bileşenlerini almak ticari koşulların elverdiği oranda makul destek toohelp, toofurther hello sorun giderme.</span><span class="sxs-lookup"><span data-stu-id="2abc2-189">Custom components receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="2abc2-190">Merhaba sorunu çözmek veya tooengage kullanılabilir kanalları hello için bu teknoloji derin uzmanlık bulunduğu kaynak teknolojileri açtığınız isteyen neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="2abc2-190">This might result in resolving hello issue OR asking you tooengage available channels for hello open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="2abc2-191">Örneğin, olduğu gibi kullanılabilecek birçok topluluk siteleri vardır: [Hdınsight için MSDN Forumu](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Apache projeleri proje siteleri de [http://apache.org](http://apache.org), örneğin: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="2abc2-191">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/), [Spark](http://spark.apache.org/).</span></span>
>
>

<span data-ttu-id="2abc2-192">Merhaba Hdınsight hizmeti toouse özel bileşenleri çeşitli yöntemler sağlar.</span><span class="sxs-lookup"><span data-stu-id="2abc2-192">hello HDInsight service provides several ways toouse custom components.</span></span> <span data-ttu-id="2abc2-193">Nasıl bir bileşeni kullanılan veya hello kümeye yüklü bağımsız olarak, hello aynı düzeyde desteği için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="2abc2-193">Regardless of how a component is used or installed on hello cluster, hello same level of support applies.</span></span> <span data-ttu-id="2abc2-194">Özel bileşenler Hdınsight kümelerinde kullanılabilir hello en yaygın şekilde listesi aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="2abc2-194">Below is a list of hello most common ways that custom components can be used on HDInsight clusters:</span></span>

1. <span data-ttu-id="2abc2-195">İş gönderme - Hadoop veya diğer tür execute veya özel bileşenleri kullanan işi gönderilen toohello kümesi olabilir.</span><span class="sxs-lookup"><span data-stu-id="2abc2-195">Job submission - Hadoop or other types of jobs that execute or use custom components can be submitted toohello cluster.</span></span>
2. <span data-ttu-id="2abc2-196">Küme özelleştirme - küme oluşturma sırasında ek ayarlar ve hello küme düğümlerinde yüklü özel bileşenleri belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2abc2-196">Cluster customization - During cluster creation, you can specify additional settings and custom components that will be installed on hello cluster nodes.</span></span>
3. <span data-ttu-id="2abc2-197">Örnekler - popüler özel bileşenleri, Microsoft ve diğerleri için bu bileşenlerin hello Hdınsight kümelerinde nasıl kullanılabileceğini örnek sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="2abc2-197">Samples - For popular custom components, Microsoft and others may provide samples of how these components can be used on hello HDInsight clusters.</span></span> <span data-ttu-id="2abc2-198">Bu örnekler desteği olmadan sağlanır.</span><span class="sxs-lookup"><span data-stu-id="2abc2-198">These samples are provided without support.</span></span>

## <a name="develop-script-action-scripts"></a><span data-ttu-id="2abc2-199">Betik eylemi betikleri geliştirme</span><span class="sxs-lookup"><span data-stu-id="2abc2-199">Develop Script Action scripts</span></span>
<span data-ttu-id="2abc2-200">Bkz: [Hdınsight betik eylemi geliştirme betikleri][hdinsight-write-script].</span><span class="sxs-lookup"><span data-stu-id="2abc2-200">See [Develop Script Action scripts for HDInsight][hdinsight-write-script].</span></span>

## <a name="see-also"></a><span data-ttu-id="2abc2-201">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="2abc2-201">See also</span></span>
* <span data-ttu-id="2abc2-202">[Hdınsight'ta Hadoop kümeleri oluşturma] [ hdinsight-provision-cluster] nasıl toocreate bir Hdınsight küme diğer özel seçenekleri kullanarak yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="2abc2-202">[Create Hadoop clusters in HDInsight][hdinsight-provision-cluster] provides instructions on how toocreate an HDInsight cluster by using other custom options.</span></span>
* <span data-ttu-id="2abc2-203">[Hdınsight için betik eylemi betikleri geliştirme][hdinsight-write-script]</span><span class="sxs-lookup"><span data-stu-id="2abc2-203">[Develop Script Action scripts for HDInsight][hdinsight-write-script]</span></span>
* <span data-ttu-id="2abc2-204">[Yükleme ve Spark Hdınsight kümelerinde kullanma][hdinsight-install-spark]</span><span class="sxs-lookup"><span data-stu-id="2abc2-204">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]</span></span>
* <span data-ttu-id="2abc2-205">[Yükleme ve Hdınsight kümelerinde R kullanma][hdinsight-install-r]</span><span class="sxs-lookup"><span data-stu-id="2abc2-205">[Install and use R on HDInsight clusters][hdinsight-install-r]</span></span>
* <span data-ttu-id="2abc2-206">[Yükleme ve Hdınsight kümelerinde Solr kullanma](hdinsight-hadoop-solr-install.md).</span><span class="sxs-lookup"><span data-stu-id="2abc2-206">[Install and use Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md).</span></span>
* <span data-ttu-id="2abc2-207">[Yükleme ve Hdınsight kümelerinde Giraph kullanma](hdinsight-hadoop-giraph-install.md).</span><span class="sxs-lookup"><span data-stu-id="2abc2-207">[Install and use Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md).</span></span>

[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-write-script]: hdinsight-hadoop-script-actions.md
[hdinsight-provision-cluster]: hdinsight-hadoop-provision-linux-clusters.md
[powershell-install-configure]: /powershell/azureps-cmdlets-docs


[img-hdi-cluster-states]: ./media/hdinsight-hadoop-customize-cluster/HDI-Cluster-state.png "Küme oluşturma sırasında aşamaları"
