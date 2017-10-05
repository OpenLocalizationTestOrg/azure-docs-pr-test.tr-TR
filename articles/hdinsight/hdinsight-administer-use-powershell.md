---
title: "PowerShell - Azure ile hdınsight'ta Hadoop kümelerini yönetme | Microsoft Docs"
description: "Azure PowerShell kullanarak hdınsight'ta Hadoop kümeleri için yönetim görevlerini gerçekleştirmek öğrenin."
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
ms.openlocfilehash: c47dabd7c4aa4ba0be08c419989e536711f03677
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-azure-powershell"></a><span data-ttu-id="8610d-103">Azure PowerShell kullanarak hdınsight'ta Hadoop kümelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="8610d-103">Manage Hadoop clusters in HDInsight by using Azure PowerShell</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="8610d-104">Azure PowerShell denetlemek ve dağıtımını ve yönetimini azure'da, iş yüklerini otomatikleştirmek için kullanabileceğiniz güçlü bir komut dosyası ortamıdır.</span><span class="sxs-lookup"><span data-stu-id="8610d-104">Azure PowerShell is a powerful scripting environment that you can use to control and automate the deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="8610d-105">Bu makalede, Windows PowerShell kullanarak yerel bir Azure PowerShell konsolunu kullanarak Azure hdınsight'ta Hadoop kümelerini yönetme öğreneceksiniz.</span><span class="sxs-lookup"><span data-stu-id="8610d-105">In this article, you will learn how to manage Hadoop clusters in Azure HDInsight by using a local Azure PowerShell console through the use of Windows PowerShell.</span></span> <span data-ttu-id="8610d-106">Hdınsight PowerShell cmdlet'leri listesi için bkz: [Hdınsight cmdlet başvurusu][hdinsight-powershell-reference].</span><span class="sxs-lookup"><span data-stu-id="8610d-106">For the list of the HDInsight PowerShell cmdlets, see [HDInsight cmdlet reference][hdinsight-powershell-reference].</span></span>

<span data-ttu-id="8610d-107">**Önkoşullar**</span><span class="sxs-lookup"><span data-stu-id="8610d-107">**Prerequisites**</span></span>

<span data-ttu-id="8610d-108">Bu makaleye başlamadan önce aşağıdakilere sahip olmanız ve aşağıdaki işlemleri yapmış olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="8610d-108">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="8610d-109">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="8610d-109">**An Azure subscription**.</span></span> <span data-ttu-id="8610d-110">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="8610d-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="8610d-111">Azure PowerShell'i yükleme</span><span class="sxs-lookup"><span data-stu-id="8610d-111">Install Azure PowerShell</span></span>
[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="8610d-112">Azure PowerShell sürüm 0.9 yüklediyseniz x, bunu yeni bir sürümünü yüklemeden önce kaldırmalısınız.</span><span class="sxs-lookup"><span data-stu-id="8610d-112">If you have installed Azure PowerShell version 0.9x, you must uninstall it before installing a newer version.</span></span>

<span data-ttu-id="8610d-113">Yüklü PowerShell sürümü denetlemek için:</span><span class="sxs-lookup"><span data-stu-id="8610d-113">To check the version of the installed PowerShell:</span></span>

    Get-Module *azure*

<span data-ttu-id="8610d-114">Eski sürümünü kaldırmak için Denetim Masası'ndaki Programlar ve Özellikler'ı çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="8610d-114">To uninstall the older version, run Programs and Features in the control panel.</span></span>

## <a name="create-clusters"></a><span data-ttu-id="8610d-115">Küme oluşturma</span><span class="sxs-lookup"><span data-stu-id="8610d-115">Create clusters</span></span>
<span data-ttu-id="8610d-116">Bkz: [Azure PowerShell kullanarak Hdınsight oluşturma Linux tabanlı kümelerde](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="8610d-116">See [Create Linux-based clusters in HDInsight using Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="8610d-117">Liste kümeleri</span><span class="sxs-lookup"><span data-stu-id="8610d-117">List clusters</span></span>
<span data-ttu-id="8610d-118">Tüm kümelerde geçerli abonelik listelemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="8610d-118">Use the following command to list all clusters in the current subscription:</span></span>

    Get-AzureRmHDInsightCluster

## <a name="show-cluster"></a><span data-ttu-id="8610d-119">Küme Göster</span><span class="sxs-lookup"><span data-stu-id="8610d-119">Show cluster</span></span>
<span data-ttu-id="8610d-120">Belirli bir kümeyi ayrıntılarını geçerli abonelikte göstermek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="8610d-120">Use the following command to show details of a specific cluster in the current subscription:</span></span>

    Get-AzureRmHDInsightCluster -ClusterName <Cluster Name>

## <a name="delete-clusters"></a><span data-ttu-id="8610d-121">Küme silme</span><span class="sxs-lookup"><span data-stu-id="8610d-121">Delete clusters</span></span>
<span data-ttu-id="8610d-122">Bir küme silmek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="8610d-122">Use the following command to delete a cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName <Cluster Name>

<span data-ttu-id="8610d-123">Ayrıca, küme içeren kaynak grubunu kaldırarak bir küme silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8610d-123">You can also delete a cluster by removing the resource group that contains the cluster.</span></span> <span data-ttu-id="8610d-124">Lütfen unutmayın, bu varsayılan depolama hesabı dahil olmak üzere gruptaki tüm kaynakları siler.</span><span class="sxs-lookup"><span data-stu-id="8610d-124">Please note, this will delete all the resources in the group including the default storage account.</span></span>

    Remove-AzureRmResourceGroup -Name <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="8610d-125">Kümeleri ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="8610d-125">Scale clusters</span></span>
<span data-ttu-id="8610d-126">Özellik ölçeklendirme küme kümeye yeniden oluşturmak zorunda kalmadan Azure Hdınsight'ta çalıştıran bir küme tarafından kullanılan çalışan düğümü sayısını değiştirmenize izin verir.</span><span class="sxs-lookup"><span data-stu-id="8610d-126">The cluster scaling feature allows you to change the number of worker nodes used by a cluster that is running in Azure HDInsight without having to re-create the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="8610d-127">Yalnızca, Hdınsight sürüm 3.1.3 ile kümeleri veya üzeri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="8610d-127">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="8610d-128">Kümenizin sürümünü emin değilseniz, Özellikler sayfasını kontrol edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8610d-128">If you are unsure of the version of your cluster, you can check the Properties page.</span></span>  <span data-ttu-id="8610d-129">Bkz: [listesi ve Göster kümeleri](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="8610d-129">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
>
>

<span data-ttu-id="8610d-130">Her tür Hdınsight tarafından desteklenen küme için veri düğüm sayısını değiştirme etkisi:</span><span class="sxs-lookup"><span data-stu-id="8610d-130">The impact of changing the number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="8610d-131">Hadoop</span><span class="sxs-lookup"><span data-stu-id="8610d-131">Hadoop</span></span>

    <span data-ttu-id="8610d-132">Sorunsuz bir şekilde tüm bekleyen veya çalışan işler etkilemeden çalıştıran bir Hadoop kümesinde çalışan düğümü sayısını da artırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8610d-132">You can seamlessly increase the number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="8610d-133">İşlemi devam ederken yeni işleri da gönderilebilir.</span><span class="sxs-lookup"><span data-stu-id="8610d-133">New jobs can also be submitted while the operation is in progress.</span></span> <span data-ttu-id="8610d-134">Kümenin her zaman işlevsel bir durumda bırakılır böylece bir ölçeklendirme işlemi hatalar düzgün bir şekilde ele alınır.</span><span class="sxs-lookup"><span data-stu-id="8610d-134">Failures in a scaling operation are gracefully handled so that the cluster is always left in a functional state.</span></span>

    <span data-ttu-id="8610d-135">Bir Hadoop kümesine veri düğüm sayısını azaltarak ölçeklendirilir, bazı kümedeki hizmetleri yeniden başlatılır.</span><span class="sxs-lookup"><span data-stu-id="8610d-135">When a Hadoop cluster is scaled down by reducing the number of data nodes, some of the services in the cluster are restarted.</span></span> <span data-ttu-id="8610d-136">Bu işleri bekleyen tüm çalışan ve ölçeklendirme işlemi tamamlandığında başarısız olmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="8610d-136">This causes all running and pending jobs to fail at the completion of the scaling operation.</span></span> <span data-ttu-id="8610d-137">İşlemi tamamlandıktan sonra ancak, sunmaları olabilir.</span><span class="sxs-lookup"><span data-stu-id="8610d-137">You can, however, resubmit the jobs once the operation is complete.</span></span>
* <span data-ttu-id="8610d-138">HBase</span><span class="sxs-lookup"><span data-stu-id="8610d-138">HBase</span></span>

    <span data-ttu-id="8610d-139">Sorunsuz bir şekilde ekleyebilir veya çalışırken, HBase kümesi düğümleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="8610d-139">You can seamlessly add or remove nodes to your HBase cluster while it is running.</span></span> <span data-ttu-id="8610d-140">Bölgesel sunucular otomatik olarak ölçeklendirme işlemi tamamladıktan birkaç dakika içinde dengeli.</span><span class="sxs-lookup"><span data-stu-id="8610d-140">Regional Servers are automatically balanced within a few minutes of completing the scaling operation.</span></span> <span data-ttu-id="8610d-141">Ancak, küme headnode için oturum açma ve bir komut istemi penceresinden aşağıdaki komutları çalıştırarak el ile de bölgesel sunucular dengeleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8610d-141">However, you can also manually balance the regional servers by logging in to the headnode of cluster and running the following commands from a command prompt window:</span></span>

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="8610d-142">Storm</span><span class="sxs-lookup"><span data-stu-id="8610d-142">Storm</span></span>

    <span data-ttu-id="8610d-143">Sorunsuz bir şekilde ekleyebilir veya çalışırken Storm kümeniz veri düğümleri kaldırın.</span><span class="sxs-lookup"><span data-stu-id="8610d-143">You can seamlessly add or remove data nodes to your Storm cluster while it is running.</span></span> <span data-ttu-id="8610d-144">Ancak ölçeklendirme işlemi başarıyla tamamlandıktan sonra topoloji yeniden dengelemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="8610d-144">But after a successful completion of the scaling operation, you will need to rebalance the topology.</span></span>

    <span data-ttu-id="8610d-145">İki yolla yeniden dengelenmesi gerçekleştirilebilir:</span><span class="sxs-lookup"><span data-stu-id="8610d-145">Rebalancing can be accomplished in two ways:</span></span>

  * <span data-ttu-id="8610d-146">Storm web kullanıcı Arabirimi</span><span class="sxs-lookup"><span data-stu-id="8610d-146">Storm web UI</span></span>
  * <span data-ttu-id="8610d-147">Komut satırı arabirimi (CLI) aracı</span><span class="sxs-lookup"><span data-stu-id="8610d-147">Command-line interface (CLI) tool</span></span>

    <span data-ttu-id="8610d-148">Lütfen [Apache Storm belgelerine](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) daha fazla ayrıntı için.</span><span class="sxs-lookup"><span data-stu-id="8610d-148">Please refer to the [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>

    <span data-ttu-id="8610d-149">Hdınsight kümesinde Storm web kullanıcı Arabirimi kullanılabilir:</span><span class="sxs-lookup"><span data-stu-id="8610d-149">The Storm web UI is available on the HDInsight cluster:</span></span>

    ![Hdınsight storm ölçek yeniden dengeleyin](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

    <span data-ttu-id="8610d-151">Storm topolojisini yeniden dengelemeniz CLI komutunu kullanma örneği şöyledir:</span><span class="sxs-lookup"><span data-stu-id="8610d-151">Here is an example how to use the CLI command to rebalance the Storm topology:</span></span>

        ## Reconfigure the topology "mytopology" to use 5 worker processes,
        ## the spout "blue-spout" to use 3 executors, and
        ## the bolt "yellow-bolt" to use 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="8610d-152">Azure PowerShell kullanarak Hadoop küme boyutunu değiştirmek için bir istemci makinesinden aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="8610d-152">To change the Hadoop cluster size by using Azure PowerShell, run the following command from a client machine:</span></span>

    Set-AzureRmHDInsightClusterSize -ClusterName <Cluster Name> -TargetInstanceCount <NewSize>


## <a name="grantrevoke-access"></a><span data-ttu-id="8610d-153">GRANT/revoke erişim</span><span class="sxs-lookup"><span data-stu-id="8610d-153">Grant/revoke access</span></span>
<span data-ttu-id="8610d-154">Hdınsight kümeleri (Bu hizmetlerin tümü için RESTful uç noktaları vardır) aşağıdaki HTTP web hizmetleri vardır:</span><span class="sxs-lookup"><span data-stu-id="8610d-154">HDInsight clusters have the following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="8610d-155">ODBC</span><span class="sxs-lookup"><span data-stu-id="8610d-155">ODBC</span></span>
* <span data-ttu-id="8610d-156">JDBC</span><span class="sxs-lookup"><span data-stu-id="8610d-156">JDBC</span></span>
* <span data-ttu-id="8610d-157">Ambari</span><span class="sxs-lookup"><span data-stu-id="8610d-157">Ambari</span></span>
* <span data-ttu-id="8610d-158">Oozie</span><span class="sxs-lookup"><span data-stu-id="8610d-158">Oozie</span></span>
* <span data-ttu-id="8610d-159">Templeton</span><span class="sxs-lookup"><span data-stu-id="8610d-159">Templeton</span></span>

<span data-ttu-id="8610d-160">Varsayılan olarak, bu hizmetleri için erişim verilir.</span><span class="sxs-lookup"><span data-stu-id="8610d-160">By default, these services are granted for access.</span></span> <span data-ttu-id="8610d-161">İptal etme / erişim izninin.</span><span class="sxs-lookup"><span data-stu-id="8610d-161">You can revoke/grant the access.</span></span> <span data-ttu-id="8610d-162">İptal etmek için:</span><span class="sxs-lookup"><span data-stu-id="8610d-162">To revoke:</span></span>

    Revoke-AzureRmHDInsightHttpServicesAccess -ClusterName <Cluster Name>

<span data-ttu-id="8610d-163">Vermek için:</span><span class="sxs-lookup"><span data-stu-id="8610d-163">To grant:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    # Credential option 1
    $hadoopUserName = "admin"
    $hadoopUserPassword = "<Enter the Password>"
    $hadoopUserPW = ConvertTo-SecureString -String $hadoopUserPassword -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential($hadoopUserName,$hadoopUserPW)

    # Credential option 2
    #$credential = Get-Credential -Message "Enter the HTTP username and password:" -UserName "admin"

    Grant-AzureRmHDInsightHttpServicesAccess -ClusterName $clusterName -HttpCredential $credential

> [!NOTE]
> <span data-ttu-id="8610d-164">Verme/erişimi iptal ederek, küme kullanıcı adı ve parola sıfırlanır.</span><span class="sxs-lookup"><span data-stu-id="8610d-164">By granting/revoking the access, you will reset the cluster user name and password.</span></span>
>
>

<span data-ttu-id="8610d-165">Bu, Portal üzerinden de yapılabilir.</span><span class="sxs-lookup"><span data-stu-id="8610d-165">This can also be done via the Portal.</span></span> <span data-ttu-id="8610d-166">Bkz: [yönetmek Azure portalını kullanarak Hdınsight][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="8610d-166">See [Administer HDInsight by using the Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="8610d-167">HTTP kullanıcı kimlik bilgilerini güncelleştirin</span><span class="sxs-lookup"><span data-stu-id="8610d-167">Update HTTP user credentials</span></span>
<span data-ttu-id="8610d-168">Yordamın aynısını olan [Grant/revoke HTTP erişimi](#grant/revoke-access). Küme HTTP erişim verilmişse, öncelikle iptal gerekir.</span><span class="sxs-lookup"><span data-stu-id="8610d-168">It is the same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If the cluster has been granted the HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="8610d-169">Ve ardından yeni HTTP kullanıcı kimlik bilgileriyle erişim verin.</span><span class="sxs-lookup"><span data-stu-id="8610d-169">And then grant the access with new HTTP user credentials.</span></span>

## <a name="find-the-default-storage-account"></a><span data-ttu-id="8610d-170">Varsayılan depolama hesabı bulunamadı</span><span class="sxs-lookup"><span data-stu-id="8610d-170">Find the default storage account</span></span>
<span data-ttu-id="8610d-171">Aşağıdaki Powershell betiğini varsayılan depolama hesabı adı ve bir küme için varsayılan depolama hesabı anahtarı alma gösterir.</span><span class="sxs-lookup"><span data-stu-id="8610d-171">The following Powershell script demonstrates how to get the default storage account name and the default storage account key for a cluster.</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup
    $defaultStorageAccountName = ($cluster.DefaultStorageAccount).Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $cluster.DefaultStorageContainer
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey

## <a name="find-the-resource-group"></a><span data-ttu-id="8610d-172">Kaynak Grup bulunamıyor</span><span class="sxs-lookup"><span data-stu-id="8610d-172">Find the resource group</span></span>
<span data-ttu-id="8610d-173">Kaynak Yöneticisi modunda her Hdınsight kümesi bir Azure kaynak grubuna ait.</span><span class="sxs-lookup"><span data-stu-id="8610d-173">In the Resource Manager mode, each HDInsight cluster belongs to an Azure resource group.</span></span>  <span data-ttu-id="8610d-174">Kaynak grubu bulmak için:</span><span class="sxs-lookup"><span data-stu-id="8610d-174">To find the resource group:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup


## <a name="submit-jobs"></a><span data-ttu-id="8610d-175">İşlerini gönderme</span><span class="sxs-lookup"><span data-stu-id="8610d-175">Submit jobs</span></span>
<span data-ttu-id="8610d-176">**MapReduce işleri göndermek için**</span><span class="sxs-lookup"><span data-stu-id="8610d-176">**To submit MapReduce jobs**</span></span>

<span data-ttu-id="8610d-177">Bkz: [Windows tabanlı Hdınsight Hadoop MapReduce çalıştırma örnekleri](hdinsight-run-samples.md).</span><span class="sxs-lookup"><span data-stu-id="8610d-177">See [Run Hadoop MapReduce samples in Windows-based HDInsight](hdinsight-run-samples.md).</span></span>

<span data-ttu-id="8610d-178">**Hive işlerini göndermek için**</span><span class="sxs-lookup"><span data-stu-id="8610d-178">**To submit Hive jobs**</span></span>

<span data-ttu-id="8610d-179">Bkz: [PowerShell kullanarak Hive sorgularını çalıştırma](hdinsight-hadoop-use-hive-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8610d-179">See [Run Hive queries using PowerShell](hdinsight-hadoop-use-hive-powershell.md).</span></span>

<span data-ttu-id="8610d-180">**Pig işleri göndermek için**</span><span class="sxs-lookup"><span data-stu-id="8610d-180">**To submit Pig jobs**</span></span>

<span data-ttu-id="8610d-181">Bkz: [çalıştırmak Pig işleri PowerShell kullanarak](hdinsight-hadoop-use-pig-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8610d-181">See [Run Pig jobs using PowerShell](hdinsight-hadoop-use-pig-powershell.md).</span></span>

<span data-ttu-id="8610d-182">**Sqoop işlerini göndermek için**</span><span class="sxs-lookup"><span data-stu-id="8610d-182">**To submit Sqoop jobs**</span></span>

<span data-ttu-id="8610d-183">Bkz: [Hdınsight ile Sqoop kullanma](hdinsight-use-sqoop.md).</span><span class="sxs-lookup"><span data-stu-id="8610d-183">See [Use Sqoop with HDInsight](hdinsight-use-sqoop.md).</span></span>

<span data-ttu-id="8610d-184">**Oozie işlerini göndermek için**</span><span class="sxs-lookup"><span data-stu-id="8610d-184">**To submit Oozie jobs**</span></span>

<span data-ttu-id="8610d-185">Bkz: [tanımlamak ve Hdınsight'ta bir iş akışını çalıştırmak için Hadoop ile kullanım Oozie](hdinsight-use-oozie.md).</span><span class="sxs-lookup"><span data-stu-id="8610d-185">See [Use Oozie with Hadoop to define and run a workflow in HDInsight](hdinsight-use-oozie.md).</span></span>

## <a name="upload-data-to-azure-blob-storage"></a><span data-ttu-id="8610d-186">Azure Blob depolama alanına veri yükleme</span><span class="sxs-lookup"><span data-stu-id="8610d-186">Upload data to Azure Blob storage</span></span>
<span data-ttu-id="8610d-187">Bkz. [HDInsight'a veri yükleme][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="8610d-187">See [Upload data to HDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="8610d-188">Ayrıca Bkz.</span><span class="sxs-lookup"><span data-stu-id="8610d-188">See Also</span></span>
* <span data-ttu-id="8610d-189">[Hdınsight cmdlet başvuru belgeleri][hdinsight-powershell-reference]</span><span class="sxs-lookup"><span data-stu-id="8610d-189">[HDInsight cmdlet reference documentation][hdinsight-powershell-reference]</span></span>
* <span data-ttu-id="8610d-190">[Hdınsight Azure Portalı'nı kullanarak yönetme][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="8610d-190">[Administer HDInsight by using the Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="8610d-191">[Bir komut satırı arabirimi kullanarak Hdınsight yönetme][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="8610d-191">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="8610d-192">[Hdınsight kümeleri oluşturma][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="8610d-192">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="8610d-193">[HDInsight'a veri yükleme][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="8610d-193">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="8610d-194">[Hadoop işlerini programlı olarak gönderme][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="8610d-194">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="8610d-195">[Azure HDInsight'ı Kullanmaya Başlama][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="8610d-195">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

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
