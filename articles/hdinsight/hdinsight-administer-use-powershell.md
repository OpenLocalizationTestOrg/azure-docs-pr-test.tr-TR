---
title: "aaaManage Hadoop kümeleri PowerShell - Azure ile hdınsight'ta | Microsoft Docs"
description: "Tooperform yönetim hello için Azure PowerShell kullanarak hdınsight'ta Hadoop kümelerinin nasıl görevleri öğrenin."
services: hdinsight
editor: cgronlun
manager: jhubbard
tags: azure-portal
author: mumian
documentationcenter: 
ms.assetid: bfdfa754-18e5-4ef9-b0d6-2dbdcebc0283
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 3df082d752fa8c703db82a54b82b740290af6729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-azure-powershell"></a><span data-ttu-id="e6fc2-103">Azure PowerShell kullanarak hdınsight'ta Hadoop kümelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="e6fc2-103">Manage Hadoop clusters in HDInsight by using Azure PowerShell</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="e6fc2-104">Azure PowerShell toocontrol kullanın ve hello dağıtımı ve Yönetimi azure'da iş yüklerinizin otomatikleştirmek bir güçlü komut dosyası ortamıdır.</span><span class="sxs-lookup"><span data-stu-id="e6fc2-104">Azure PowerShell is a powerful scripting environment that you can use toocontrol and automate hello deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="e6fc2-105">Bu makalede, Azure hdınsight'ta toomanage Hadoop kümelerini yerel bir Azure PowerShell konsol hello üzerinden kullanarak Windows PowerShell kullanma öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="e6fc2-105">In this article, you will learn how toomanage Hadoop clusters in Azure HDInsight by using a local Azure PowerShell console through hello use of Windows PowerShell.</span></span> <span data-ttu-id="e6fc2-106">Merhaba Hdınsight PowerShell cmdlet'leri Hello listesi için bkz [Hdınsight cmdlet başvurusu][hdinsight-powershell-reference].</span><span class="sxs-lookup"><span data-stu-id="e6fc2-106">For hello list of hello HDInsight PowerShell cmdlets, see [HDInsight cmdlet reference][hdinsight-powershell-reference].</span></span>

<span data-ttu-id="e6fc2-107">**Önkoşullar**</span><span class="sxs-lookup"><span data-stu-id="e6fc2-107">**Prerequisites**</span></span>

<span data-ttu-id="e6fc2-108">Bu makaleye başlamadan önce hello şunlara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e6fc2-108">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="e6fc2-109">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="e6fc2-109">**An Azure subscription**.</span></span> <span data-ttu-id="e6fc2-110">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="e6fc2-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="e6fc2-111">Azure PowerShell'i yükleme</span><span class="sxs-lookup"><span data-stu-id="e6fc2-111">Install Azure PowerShell</span></span>
[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="e6fc2-112">Azure PowerShell sürüm 0.9 yüklediyseniz x, bunu yeni bir sürümünü yüklemeden önce kaldırmalısınız.</span><span class="sxs-lookup"><span data-stu-id="e6fc2-112">If you have installed Azure PowerShell version 0.9x, you must uninstall it before installing a newer version.</span></span>

<span data-ttu-id="e6fc2-113">Merhaba toocheck hello sürümü PowerShell yüklü:</span><span class="sxs-lookup"><span data-stu-id="e6fc2-113">toocheck hello version of hello installed PowerShell:</span></span>

    Get-Module *azure*

<span data-ttu-id="e6fc2-114">toouninstall hello eski sürümü, hello Denetim Masası'ndaki Programlar ve Özellikler çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e6fc2-114">toouninstall hello older version, run Programs and Features in hello control panel.</span></span>

## <a name="create-clusters"></a><span data-ttu-id="e6fc2-115">Küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="e6fc2-115">Create clusters</span></span>
<span data-ttu-id="e6fc2-116">Bkz: [Azure PowerShell kullanarak Hdınsight oluşturma Linux tabanlı kümelerde](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="e6fc2-116">See [Create Linux-based clusters in HDInsight using Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="e6fc2-117">Liste kümeleri</span><span class="sxs-lookup"><span data-stu-id="e6fc2-117">List clusters</span></span>
<span data-ttu-id="e6fc2-118">Komut toolist aşağıdaki hello tüm kümelerin hello geçerli abonelikte kullanın:</span><span class="sxs-lookup"><span data-stu-id="e6fc2-118">Use hello following command toolist all clusters in hello current subscription:</span></span>

    Get-AzureRmHDInsightCluster

## <a name="show-cluster"></a><span data-ttu-id="e6fc2-119">Küme Göster</span><span class="sxs-lookup"><span data-stu-id="e6fc2-119">Show cluster</span></span>
<span data-ttu-id="e6fc2-120">Aşağıdaki komut tooshow ayrıntılara hello geçerli abonelikte belirli bir kümenin hello kullan:</span><span class="sxs-lookup"><span data-stu-id="e6fc2-120">Use hello following command tooshow details of a specific cluster in hello current subscription:</span></span>

    Get-AzureRmHDInsightCluster -ClusterName <Cluster Name>

## <a name="delete-clusters"></a><span data-ttu-id="e6fc2-121">Küme silme</span><span class="sxs-lookup"><span data-stu-id="e6fc2-121">Delete clusters</span></span>
<span data-ttu-id="e6fc2-122">Komut toodelete bir küme aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="e6fc2-122">Use hello following command toodelete a cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName <Cluster Name>

<span data-ttu-id="e6fc2-123">Merhaba küme içeren hello kaynak grubunu kaldırarak bir küme de silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6fc2-123">You can also delete a cluster by removing hello resource group that contains hello cluster.</span></span> <span data-ttu-id="e6fc2-124">Lütfen unutmayın, bu hello varsayılan depolama hesabı dahil olmak üzere hello grubundaki tüm hello kaynaklarını siler.</span><span class="sxs-lookup"><span data-stu-id="e6fc2-124">Please note, this will delete all hello resources in hello group including hello default storage account.</span></span>

    Remove-AzureRmResourceGroup -Name <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="e6fc2-125">Kümeleri ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="e6fc2-125">Scale clusters</span></span>
<span data-ttu-id="e6fc2-126">özellik ölçeklendirme hello küme toochange hello Azure Hdınsight'ta toore gerek kalmadan çalışan bir küme tarafından kullanılan çalışan düğüm sayısı sağlar-hello kümesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e6fc2-126">hello cluster scaling feature allows you toochange hello number of worker nodes used by a cluster that is running in Azure HDInsight without having toore-create hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="e6fc2-127">Yalnızca, Hdınsight sürüm 3.1.3 ile kümeleri veya üzeri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="e6fc2-127">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="e6fc2-128">Kümenizin hello sürümü değilseniz hello özellikler sayfasını kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6fc2-128">If you are unsure of hello version of your cluster, you can check hello Properties page.</span></span>  <span data-ttu-id="e6fc2-129">Bkz: [listesi ve Göster kümeleri](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="e6fc2-129">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
>
>

<span data-ttu-id="e6fc2-130">hello etkisini, her tür Hdınsight tarafından desteklenen küme için veri düğümünün hello numarasını değiştirmek için:</span><span class="sxs-lookup"><span data-stu-id="e6fc2-130">hello impact of changing hello number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="e6fc2-131">Hadoop</span><span class="sxs-lookup"><span data-stu-id="e6fc2-131">Hadoop</span></span>

    <span data-ttu-id="e6fc2-132">Sorunsuz bir şekilde hello tüm bekleyen veya çalışan işler etkilemeden çalıştıran bir Hadoop kümesinde çalışan düğümü sayısını da artırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6fc2-132">You can seamlessly increase hello number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="e6fc2-133">Merhaba işlemi devam ederken yeni işleri da gönderilebilir.</span><span class="sxs-lookup"><span data-stu-id="e6fc2-133">New jobs can also be submitted while hello operation is in progress.</span></span> <span data-ttu-id="e6fc2-134">Böylece Hello küme her zaman işlevsel bir durumda bırakılır bir ölçeklendirme işlemi hatalar düzgün bir şekilde ele alınır.</span><span class="sxs-lookup"><span data-stu-id="e6fc2-134">Failures in a scaling operation are gracefully handled so that hello cluster is always left in a functional state.</span></span>

    <span data-ttu-id="e6fc2-135">Bir Hadoop kümesine veri düğümlerini hello sayısını azaltarak ölçeklendirilir, bazı hello kümedeki hello hizmetleri yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="e6fc2-135">When a Hadoop cluster is scaled down by reducing hello number of data nodes, some of hello services in hello cluster are restarted.</span></span> <span data-ttu-id="e6fc2-136">Bu, tüm çalışan ve işleri toofail hello tamamlanma işlemi ölçeklendirme Merhaba, bekleyen neden olur.</span><span class="sxs-lookup"><span data-stu-id="e6fc2-136">This causes all running and pending jobs toofail at hello completion of hello scaling operation.</span></span> <span data-ttu-id="e6fc2-137">Hello işlemi tamamlandıktan sonra ancak, hello sunmaları olabilir.</span><span class="sxs-lookup"><span data-stu-id="e6fc2-137">You can, however, resubmit hello jobs once hello operation is complete.</span></span>
* <span data-ttu-id="e6fc2-138">HBase</span><span class="sxs-lookup"><span data-stu-id="e6fc2-138">HBase</span></span>

    <span data-ttu-id="e6fc2-139">Sorunsuz bir şekilde ekleme veya düğümleri tooyour HBase kümesi çalışırken kaldırın.</span><span class="sxs-lookup"><span data-stu-id="e6fc2-139">You can seamlessly add or remove nodes tooyour HBase cluster while it is running.</span></span> <span data-ttu-id="e6fc2-140">Bölgesel sunucuları işlemi ölçeklendirme hello tamamladıktan birkaç dakika içinde otomatik olarak dengeli.</span><span class="sxs-lookup"><span data-stu-id="e6fc2-140">Regional Servers are automatically balanced within a few minutes of completing hello scaling operation.</span></span> <span data-ttu-id="e6fc2-141">Ancak, küme ve komutlar bir komut istemi penceresinden aşağıdaki çalışan hello toohello headnode oturum açarak hello bölgesel sunucular el ile de dengeleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="e6fc2-141">However, you can also manually balance hello regional servers by logging in toohello headnode of cluster and running hello following commands from a command prompt window:</span></span>

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="e6fc2-142">Storm</span><span class="sxs-lookup"><span data-stu-id="e6fc2-142">Storm</span></span>

    <span data-ttu-id="e6fc2-143">Sorunsuz bir şekilde ekleyebilir veya çalışırken veri düğümleri tooyour Storm kümesi kaldırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e6fc2-143">You can seamlessly add or remove data nodes tooyour Storm cluster while it is running.</span></span> <span data-ttu-id="e6fc2-144">Ancak hello ölçekleme işlemi başarıyla tamamlandıktan sonra toorebalance hello topoloji gerekir.</span><span class="sxs-lookup"><span data-stu-id="e6fc2-144">But after a successful completion of hello scaling operation, you will need toorebalance hello topology.</span></span>

    <span data-ttu-id="e6fc2-145">İki yolla yeniden dengelenmesi gerçekleştirilebilir:</span><span class="sxs-lookup"><span data-stu-id="e6fc2-145">Rebalancing can be accomplished in two ways:</span></span>

  * <span data-ttu-id="e6fc2-146">Storm web kullanıcı Arabirimi</span><span class="sxs-lookup"><span data-stu-id="e6fc2-146">Storm web UI</span></span>
  * <span data-ttu-id="e6fc2-147">Komut satırı arabirimi (CLI) aracı</span><span class="sxs-lookup"><span data-stu-id="e6fc2-147">Command-line interface (CLI) tool</span></span>

    <span data-ttu-id="e6fc2-148">Lütfen toohello bakın [Apache Storm belgelerine](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="e6fc2-148">Please refer toohello [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>

    <span data-ttu-id="e6fc2-149">Merhaba Storm web kullanıcı Arabirimi hello Hdınsight kümesinde kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="e6fc2-149">hello Storm web UI is available on hello HDInsight cluster:</span></span>

    ![Hdınsight storm ölçek yeniden dengeleyin](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

    <span data-ttu-id="e6fc2-151">Örneği nasıl toouse hello CLI komutu toorebalance hello Storm topolojisini:</span><span class="sxs-lookup"><span data-stu-id="e6fc2-151">Here is an example how toouse hello CLI command toorebalance hello Storm topology:</span></span>

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="e6fc2-152">toochange hello bir istemci makinesinden komutu aşağıdaki hello çalıştırmak, Azure PowerShell kullanarak Hadoop küme boyutu:</span><span class="sxs-lookup"><span data-stu-id="e6fc2-152">toochange hello Hadoop cluster size by using Azure PowerShell, run hello following command from a client machine:</span></span>

    Set-AzureRmHDInsightClusterSize -ClusterName <Cluster Name> -TargetInstanceCount <NewSize>


## <a name="grantrevoke-access"></a><span data-ttu-id="e6fc2-153">GRANT/revoke erişim</span><span class="sxs-lookup"><span data-stu-id="e6fc2-153">Grant/revoke access</span></span>
<span data-ttu-id="e6fc2-154">Hdınsight kümeleri HTTP web Hizmetleri (Bu hizmetlerin tümü için RESTful uç noktaları vardır) aşağıdaki hello vardır:</span><span class="sxs-lookup"><span data-stu-id="e6fc2-154">HDInsight clusters have hello following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="e6fc2-155">ODBC</span><span class="sxs-lookup"><span data-stu-id="e6fc2-155">ODBC</span></span>
* <span data-ttu-id="e6fc2-156">JDBC</span><span class="sxs-lookup"><span data-stu-id="e6fc2-156">JDBC</span></span>
* <span data-ttu-id="e6fc2-157">Ambari</span><span class="sxs-lookup"><span data-stu-id="e6fc2-157">Ambari</span></span>
* <span data-ttu-id="e6fc2-158">Oozie</span><span class="sxs-lookup"><span data-stu-id="e6fc2-158">Oozie</span></span>
* <span data-ttu-id="e6fc2-159">Templeton</span><span class="sxs-lookup"><span data-stu-id="e6fc2-159">Templeton</span></span>

<span data-ttu-id="e6fc2-160">Varsayılan olarak, bu hizmetleri için erişim verilir.</span><span class="sxs-lookup"><span data-stu-id="e6fc2-160">By default, these services are granted for access.</span></span> <span data-ttu-id="e6fc2-161">İptal etme/hello erişim izninin.</span><span class="sxs-lookup"><span data-stu-id="e6fc2-161">You can revoke/grant hello access.</span></span> <span data-ttu-id="e6fc2-162">toorevoke:</span><span class="sxs-lookup"><span data-stu-id="e6fc2-162">toorevoke:</span></span>

    Revoke-AzureRmHDInsightHttpServicesAccess -ClusterName <Cluster Name>

<span data-ttu-id="e6fc2-163">toogrant:</span><span class="sxs-lookup"><span data-stu-id="e6fc2-163">toogrant:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    # Credential option 1
    $hadoopUserName = "admin"
    $hadoopUserPassword = "<Enter hello Password>"
    $hadoopUserPW = ConvertTo-SecureString -String $hadoopUserPassword -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential($hadoopUserName,$hadoopUserPW)

    # Credential option 2
    #$credential = Get-Credential -Message "Enter hello HTTP username and password:" -UserName "admin"

    Grant-AzureRmHDInsightHttpServicesAccess -ClusterName $clusterName -HttpCredential $credential

> [!NOTE]
> <span data-ttu-id="e6fc2-164">Verme/hello erişimi iptal ederek, hello küme kullanıcı adı ve parola sıfırlanır.</span><span class="sxs-lookup"><span data-stu-id="e6fc2-164">By granting/revoking hello access, you will reset hello cluster user name and password.</span></span>
>
>

<span data-ttu-id="e6fc2-165">Bu ayrıca hello Portal yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="e6fc2-165">This can also be done via hello Portal.</span></span> <span data-ttu-id="e6fc2-166">Bkz: [kullanarak Hdınsight yönetmek hello Azure portal][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="e6fc2-166">See [Administer HDInsight by using hello Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="e6fc2-167">HTTP kullanıcı kimlik bilgilerini güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="e6fc2-167">Update HTTP user credentials</span></span>
<span data-ttu-id="e6fc2-168">Aynı hello olan yordamı [Grant/revoke HTTP erişimi](#grant/revoke-access). Merhaba küme hello HTTP erişim verilmişse, öncelikle iptal gerekir.</span><span class="sxs-lookup"><span data-stu-id="e6fc2-168">It is hello same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If hello cluster has been granted hello HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="e6fc2-169">Ve ardından yeni HTTP kullanıcı kimlik bilgileriyle hello erişim verin.</span><span class="sxs-lookup"><span data-stu-id="e6fc2-169">And then grant hello access with new HTTP user credentials.</span></span>

## <a name="find-hello-default-storage-account"></a><span data-ttu-id="e6fc2-170">Merhaba varsayılan depolama hesabı bulunamadı</span><span class="sxs-lookup"><span data-stu-id="e6fc2-170">Find hello default storage account</span></span>
<span data-ttu-id="e6fc2-171">PowerShell Betiği aşağıdaki hello nasıl tooget varsayılan depolama hesabı adı hello ve küme için varsayılan depolama hesabı anahtarı hello gösterir.</span><span class="sxs-lookup"><span data-stu-id="e6fc2-171">hello following Powershell script demonstrates how tooget hello default storage account name and hello default storage account key for a cluster.</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup
    $defaultStorageAccountName = ($cluster.DefaultStorageAccount).Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $cluster.DefaultStorageContainer
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey

## <a name="find-hello-resource-group"></a><span data-ttu-id="e6fc2-172">Merhaba kaynak grup bulunamıyor</span><span class="sxs-lookup"><span data-stu-id="e6fc2-172">Find hello resource group</span></span>
<span data-ttu-id="e6fc2-173">Merhaba Kaynak Yöneticisi modunda tooan Azure kaynak grubu her Hdınsight kümesine ait.</span><span class="sxs-lookup"><span data-stu-id="e6fc2-173">In hello Resource Manager mode, each HDInsight cluster belongs tooan Azure resource group.</span></span>  <span data-ttu-id="e6fc2-174">toofind hello kaynak grubu:</span><span class="sxs-lookup"><span data-stu-id="e6fc2-174">toofind hello resource group:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup


## <a name="submit-jobs"></a><span data-ttu-id="e6fc2-175">İşlerini gönderme</span><span class="sxs-lookup"><span data-stu-id="e6fc2-175">Submit jobs</span></span>
<span data-ttu-id="e6fc2-176">**toosubmit MapReduce işleri**</span><span class="sxs-lookup"><span data-stu-id="e6fc2-176">**toosubmit MapReduce jobs**</span></span>

<span data-ttu-id="e6fc2-177">Bkz: [Windows tabanlı Hdınsight Hadoop MapReduce çalıştırma örnekleri](hdinsight-run-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e6fc2-177">See [Run Hadoop MapReduce samples in Windows-based HDInsight](hdinsight-run-samples.md).</span></span>

<span data-ttu-id="e6fc2-178">**toosubmit Hive işleri**</span><span class="sxs-lookup"><span data-stu-id="e6fc2-178">**toosubmit Hive jobs**</span></span>

<span data-ttu-id="e6fc2-179">Bkz: [PowerShell kullanarak Hive sorgularını çalıştırma](hdinsight-hadoop-use-hive-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e6fc2-179">See [Run Hive queries using PowerShell](hdinsight-hadoop-use-hive-powershell.md).</span></span>

<span data-ttu-id="e6fc2-180">**toosubmit Pig işleri**</span><span class="sxs-lookup"><span data-stu-id="e6fc2-180">**toosubmit Pig jobs**</span></span>

<span data-ttu-id="e6fc2-181">Bkz: [çalıştırmak Pig işleri PowerShell kullanarak](hdinsight-hadoop-use-pig-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e6fc2-181">See [Run Pig jobs using PowerShell](hdinsight-hadoop-use-pig-powershell.md).</span></span>

<span data-ttu-id="e6fc2-182">**toosubmit Sqoop işleri**</span><span class="sxs-lookup"><span data-stu-id="e6fc2-182">**toosubmit Sqoop jobs**</span></span>

<span data-ttu-id="e6fc2-183">Bkz: [Hdınsight ile Sqoop kullanma](hdinsight-use-sqoop.md).</span><span class="sxs-lookup"><span data-stu-id="e6fc2-183">See [Use Sqoop with HDInsight](hdinsight-use-sqoop.md).</span></span>

<span data-ttu-id="e6fc2-184">**toosubmit Oozie işleri**</span><span class="sxs-lookup"><span data-stu-id="e6fc2-184">**toosubmit Oozie jobs**</span></span>

<span data-ttu-id="e6fc2-185">Bkz: [Hadoop toodefine ve çalışma Hdınsight bir iş akışında kullanmak Oozie](hdinsight-use-oozie.md).</span><span class="sxs-lookup"><span data-stu-id="e6fc2-185">See [Use Oozie with Hadoop toodefine and run a workflow in HDInsight](hdinsight-use-oozie.md).</span></span>

## <a name="upload-data-tooazure-blob-storage"></a><span data-ttu-id="e6fc2-186">Veri tooAzure Blob Depolama yükleme</span><span class="sxs-lookup"><span data-stu-id="e6fc2-186">Upload data tooAzure Blob storage</span></span>
<span data-ttu-id="e6fc2-187">Bkz: [karşıya veri tooHDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="e6fc2-187">See [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="e6fc2-188">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="e6fc2-188">See Also</span></span>
* <span data-ttu-id="e6fc2-189">[Hdınsight cmdlet başvuru belgeleri][hdinsight-powershell-reference]</span><span class="sxs-lookup"><span data-stu-id="e6fc2-189">[HDInsight cmdlet reference documentation][hdinsight-powershell-reference]</span></span>
* <span data-ttu-id="e6fc2-190">[Hdınsight hello Azure portal kullanarak yönetme][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="e6fc2-190">[Administer HDInsight by using hello Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="e6fc2-191">[Bir komut satırı arabirimi kullanarak Hdınsight yönetme][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="e6fc2-191">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="e6fc2-192">[Hdınsight kümeleri oluşturma][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="e6fc2-192">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="e6fc2-193">[Veri tooHDInsight karşıya yükle][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="e6fc2-193">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="e6fc2-194">[Hadoop işlerini programlı olarak gönderme][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="e6fc2-194">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="e6fc2-195">[Azure HDInsight'ı Kullanmaya Başlama][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="e6fc2-195">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-provision-custom-options]: hdinsight-hadoop-provision-linux-clusters.md#configuration
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx

[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-ps-provision]: ./media/hdinsight-administer-use-powershell/HDI.PS.Provision.png
