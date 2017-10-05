---
title: "Hdınsight için Azure Kaynak Yöneticisi Araçları geçirme | Microsoft Docs"
description: "Hdınsight kümeleri için Azure Resource Manager geliştirme araçları geçirme"
services: hdinsight
editor: cgronlun
manager: jhubbard
author: nitinme
documentationcenter: 
ms.assetid: 05efedb5-6456-4552-87ff-156d77fbe2e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 708d22b9ce53d4dbc07c6bcde0c46dcd238291bb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="migrating-to-azure-resource-manager-based-development-tools-for-hdinsight-clusters"></a><span data-ttu-id="7712c-103">Hdınsight kümeleri için Azure Resource Manager tabanlı geliştirme araçlarına geçme</span><span class="sxs-lookup"><span data-stu-id="7712c-103">Migrating to Azure Resource Manager-based development tools for HDInsight clusters</span></span>

<span data-ttu-id="7712c-104">Hdınsight, Hdınsight için Azure Service Manager ASM tabanlı araçlar kaldırmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7712c-104">HDInsight is deprecating Azure Service Manager (ASM)-based tools for HDInsight.</span></span> <span data-ttu-id="7712c-105">Azure PowerShell, Azure CLI veya Hdınsight .NET SDK'sı Hdınsight kümeleriyle çalışmak için kullanıyorsanız, PowerShell'i, CLI ve .NET SDK'sı ileride Azure Resource Manager ARM tabanlı sürümleri kullanmanız önerilir.</span><span class="sxs-lookup"><span data-stu-id="7712c-105">If you have been using Azure PowerShell, Azure CLI, or the HDInsight .NET SDK to work with HDInsight clusters, you are encouraged to use the Azure Resource Manager (ARM)-based versions of PowerShell, CLI, and .NET SDK going forward.</span></span> <span data-ttu-id="7712c-106">Bu makalede yeni ARM tabanlı yaklaşımı geçirmek nasıl işaretçileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="7712c-106">This article provides pointers on how to migrate to the new ARM-based approach.</span></span> <span data-ttu-id="7712c-107">Uygun olduğunda, bu makalede ayrıca ASM ve ARM arasındaki farklar çıkışı yaklaşımlar Hdınsight için işaret eder.</span><span class="sxs-lookup"><span data-stu-id="7712c-107">Wherever applicable, this article also points out the differences between the ASM and ARM approaches for HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7712c-108">ASM desteği PowerShell'i, CLI, temel ve .NET SDK'yı Durdur **1 Ocak 2017**.</span><span class="sxs-lookup"><span data-stu-id="7712c-108">The support for ASM based PowerShell, CLI, and .NET SDK will discontinue on **January 1, 2017**.</span></span>
> 
> 

## <a name="migrating-azure-cli-to-azure-resource-manager"></a><span data-ttu-id="7712c-109">Azure CLI Azure Kaynak Yöneticisi geçirme</span><span class="sxs-lookup"><span data-stu-id="7712c-109">Migrating Azure CLI to Azure Resource Manager</span></span>
<span data-ttu-id="7712c-110">Önceki bir yükleme Yükseltmekte olduğunuz sürece Azure CLI artık Azure Resource Manager (ARM) moduna varsayılan olarak ayarlanır; Bu durumda, kullanmanız gerekebilir `azure config mode arm` ARM moduna geçmek için komutu.</span><span class="sxs-lookup"><span data-stu-id="7712c-110">The Azure CLI now defaults to Azure Resource Manager (ARM) mode, unless you are upgrading from a previous installation; in this case, you may need to use the `azure config mode arm` command to switch to ARM mode.</span></span>

<span data-ttu-id="7712c-111">Azure Hizmet Yönetimi (ASM) kullanılarak Hdınsight ile çalışmak için Azure CLI sağlanan temel komutları ARM kullanırken aynıdır; Ancak bazı parametreler ve anahtarları yeni adlara sahip ve çok sayıda yeni parametreler kullanılabilir ARM kullanırken yoktur.</span><span class="sxs-lookup"><span data-stu-id="7712c-111">The basic commands that the Azure CLI provided to work with HDInsight using Azure Service Management (ASM) are the same when using ARM; however some parameters and switches may have new names, and there are many new parameters available when using ARM.</span></span> <span data-ttu-id="7712c-112">Örneğin, artık kullanabilirsiniz `azure hdinsight cluster create` Azure sanal bir küme içinde oluşturulmalıdır veya Hive ağ ve Oozie meta depo bilgileri belirtmek için.</span><span class="sxs-lookup"><span data-stu-id="7712c-112">For example, you can now use `azure hdinsight cluster create` to specify the Azure Virtual Network that a cluster should be created in, or Hive and Oozie metastore information.</span></span>

<span data-ttu-id="7712c-113">Hdınsight ile Azure Resource Manager ile çalışmak için temel komutlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="7712c-113">Basic commands for working with HDInsight through Azure Resource Manager are:</span></span>

* <span data-ttu-id="7712c-114">`azure hdinsight cluster create`-Yeni bir Hdınsight kümesi oluşturur</span><span class="sxs-lookup"><span data-stu-id="7712c-114">`azure hdinsight cluster create` - creates a new HDInsight cluster</span></span>
* <span data-ttu-id="7712c-115">`azure hdinsight cluster delete`-Mevcut bir Hdınsight kümesine siler</span><span class="sxs-lookup"><span data-stu-id="7712c-115">`azure hdinsight cluster delete` - deletes an existing HDInsight cluster</span></span>
* <span data-ttu-id="7712c-116">`azure hdinsight cluster show`-Varolan bir kümeye hakkındaki bilgileri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="7712c-116">`azure hdinsight cluster show` - display information about an existing cluster</span></span>
* <span data-ttu-id="7712c-117">`azure hdinsight cluster list`-Azure aboneliğiniz için Hdınsight kümeleri listeler</span><span class="sxs-lookup"><span data-stu-id="7712c-117">`azure hdinsight cluster list` - lists HDInsight clusters for your Azure subscription</span></span>

<span data-ttu-id="7712c-118">Kullanım `-h` parametreleri ve her komut için kullanılabilen anahtarlar incelemek için anahtar.</span><span class="sxs-lookup"><span data-stu-id="7712c-118">Use the `-h` switch to inspect the parameters and switches available for each command.</span></span>

### <a name="new-commands"></a><span data-ttu-id="7712c-119">Yeni komutları</span><span class="sxs-lookup"><span data-stu-id="7712c-119">New commands</span></span>
<span data-ttu-id="7712c-120">Azure Resource Manager ile kullanılabilen yeni komutlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="7712c-120">New commands available with Azure Resource Manager are:</span></span>

* <span data-ttu-id="7712c-121">`azure hdinsight cluster resize`-Kümedeki çalışan düğümü sayısını dinamik olarak değiştirir</span><span class="sxs-lookup"><span data-stu-id="7712c-121">`azure hdinsight cluster resize` - dynamically changes the number of worker nodes in the cluster</span></span>
* <span data-ttu-id="7712c-122">`azure hdinsight cluster enable-http-access`-Küme HTTPs erişmesini sağlar (üzerinde varsayılan olarak)</span><span class="sxs-lookup"><span data-stu-id="7712c-122">`azure hdinsight cluster enable-http-access` - enables HTTPs access to the cluster (on by default)</span></span>
* <span data-ttu-id="7712c-123">`azure hdinsight cluster disable-http-access`-kümesine HTTPs erişimi devre dışı bırakır</span><span class="sxs-lookup"><span data-stu-id="7712c-123">`azure hdinsight cluster disable-http-access` - disables HTTPs access to the cluster</span></span>
* <span data-ttu-id="7712c-124">`azure hdinsight script-action`-oluşturma/betik eylemleri bir kümede yönetmek için komutlar sağlar</span><span class="sxs-lookup"><span data-stu-id="7712c-124">`azure hdinsight script-action` - provides commands for creating/managing Script Actions on a cluster</span></span>
* <span data-ttu-id="7712c-125">`azure hdinsight config`-bir yapılandırma dosyası oluşturma ile birlikte kullanılabilir komutlar sağlar `hdinsight cluster create` yapılandırma bilgilerini sağlamak için komutu.</span><span class="sxs-lookup"><span data-stu-id="7712c-125">`azure hdinsight config` - provides commands for creating a configuration file that can be used with the `hdinsight cluster create` command to provide configuration information.</span></span>

### <a name="deprecated-commands"></a><span data-ttu-id="7712c-126">Kullanım dışı komutları</span><span class="sxs-lookup"><span data-stu-id="7712c-126">Deprecated commands</span></span>
<span data-ttu-id="7712c-127">Kullanırsanız `azure hdinsight job` Hdınsight kümenize iş göndermek için komutları bu ARM komutlarını kullanılabilir değil.</span><span class="sxs-lookup"><span data-stu-id="7712c-127">If you use the `azure hdinsight job` commands to submit jobs to your HDInsight cluster, these are not available through the ARM commands.</span></span> <span data-ttu-id="7712c-128">İşlerini Hdınsight'a gelen komut dosyalarını program aracılığıyla göndermek gerekiyorsa, bunun yerine Hdınsight tarafından sağlanan REST API'lerini kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7712c-128">If you need to programmatically submit jobs to HDInsight from scripts, you should instead use the REST APIs provided by HDInsight.</span></span> <span data-ttu-id="7712c-129">REST API'lerini kullanarak işlerini göndermenin daha fazla bilgi için aşağıdaki belgelere bakın.</span><span class="sxs-lookup"><span data-stu-id="7712c-129">For more information on submitting jobs using REST APIs, see the following documents.</span></span>

* [<span data-ttu-id="7712c-130">CURL kullanarak Hdınsight'ta Hadoop ile MapReduce işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="7712c-130">Run MapReduce jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-mapreduce-curl.md)
* [<span data-ttu-id="7712c-131">CURL kullanarak Hdınsight'ta Hadoop ile Hive sorguları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="7712c-131">Run Hive queries with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-hive-curl.md)
* [<span data-ttu-id="7712c-132">CURL kullanarak Hdınsight'ta Hadoop ile pig işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="7712c-132">Run Pig jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-pig-curl.md)

<span data-ttu-id="7712c-133">MapReduce çalıştırmak için diğer yöntemler hakkında bilgi, Hive ve etkileşimli olarak Pig için bkz: [hdınsight'ta Hadoop ile MapReduce kullanma](hdinsight-use-mapreduce.md), [hdınsight'ta Hadoop ile Hive kullanma](hdinsight-use-hive.md), ve [Hadoop ile Pig kullanma Hdınsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="7712c-133">For information on other ways to run MapReduce, Hive, and Pig interactively, see [Use MapReduce with Hadoop on HDInsight](hdinsight-use-mapreduce.md), [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md), and [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

### <a name="examples"></a><span data-ttu-id="7712c-134">Örnekler</span><span class="sxs-lookup"><span data-stu-id="7712c-134">Examples</span></span>
<span data-ttu-id="7712c-135">**Küme oluşturma**</span><span class="sxs-lookup"><span data-stu-id="7712c-135">**Creating a cluster**</span></span>

* <span data-ttu-id="7712c-136">Eski komutu (ASM)-`azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="7712c-136">Old command (ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>
* <span data-ttu-id="7712c-137">Yeni komutu (ARM)-`azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="7712c-137">New command (ARM) - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>

<span data-ttu-id="7712c-138">**Küme silme**</span><span class="sxs-lookup"><span data-stu-id="7712c-138">**Deleting a cluster**</span></span>

* <span data-ttu-id="7712c-139">Eski komutu (ASM)-`azure hdinsight cluster delete myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="7712c-139">Old command (ASM) - `azure hdinsight cluster delete myhdicluster`</span></span>
* <span data-ttu-id="7712c-140">Yeni komutu (ARM)-`azure hdinsight cluster delete mycluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="7712c-140">New command (ARM) - `azure hdinsight cluster delete mycluster -g myresourcegroup`</span></span>

<span data-ttu-id="7712c-141">**Liste kümeleri**</span><span class="sxs-lookup"><span data-stu-id="7712c-141">**List clusters**</span></span>

* <span data-ttu-id="7712c-142">Eski komutu (ASM)-`azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="7712c-142">Old command (ASM) - `azure hdinsight cluster list`</span></span>
* <span data-ttu-id="7712c-143">Yeni komutu (ARM)-`azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="7712c-143">New command (ARM) - `azure hdinsight cluster list`</span></span>

> [!NOTE]
> <span data-ttu-id="7712c-144">Liste komutu için kaynak grubunu kullanarak belirtme `-g` yalnızca kümeler belirtilen kaynak grubunda döndürür.</span><span class="sxs-lookup"><span data-stu-id="7712c-144">For the list command, specifying the resource group using `-g` will return only the clusters in the specified resource group.</span></span>
> 
> 

<span data-ttu-id="7712c-145">**Küme bilgilerini göster**</span><span class="sxs-lookup"><span data-stu-id="7712c-145">**Show cluster information**</span></span>

* <span data-ttu-id="7712c-146">Eski komutu (ASM)-`azure hdinsight cluster show myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="7712c-146">Old command (ASM) - `azure hdinsight cluster show myhdicluster`</span></span>
* <span data-ttu-id="7712c-147">Yeni komutu (ARM)-`azure hdinsight cluster show myhdicluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="7712c-147">New command (ARM) - `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span></span>

## <a name="migrating-azure-powershell-to-azure-resource-manager"></a><span data-ttu-id="7712c-148">Azure Resource Manager Azure PowerShell geçirme</span><span class="sxs-lookup"><span data-stu-id="7712c-148">Migrating Azure PowerShell to Azure Resource Manager</span></span>
<span data-ttu-id="7712c-149">Azure Resource Manager (ARM) modunda Azure PowerShell hakkında genel bilgi şu adreste bulunabilir: [Azure PowerShell kullanarak Azure Resource Manager ile](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="7712c-149">The general information about Azure PowerShell in the Azure Resource Manager (ARM) mode can be found at [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="7712c-150">Azure PowerShell ARM cmdlet'leri yüklü yan yana ASM cmdlet'leri olabilir.</span><span class="sxs-lookup"><span data-stu-id="7712c-150">The Azure PowerShell ARM cmdlets can be installed side-by-side with the ASM cmdlets.</span></span> <span data-ttu-id="7712c-151">İki modun cmdlet'leri, adlarına göre ayırt edilebilir.</span><span class="sxs-lookup"><span data-stu-id="7712c-151">The cmdlets from the two modes can be distinguished by their names.</span></span>  <span data-ttu-id="7712c-152">ARM modu *AzureRmHDInsight* için karşılaştırma cmdlet'in adlarındaki *AzureHDInsight* ASM modunda.</span><span class="sxs-lookup"><span data-stu-id="7712c-152">The ARM mode has *AzureRmHDInsight* in the cmdlet names comparing to *AzureHDInsight* in the ASM mode.</span></span>  <span data-ttu-id="7712c-153">Örneğin, *yeni AzureRmHDInsightCluster* vs. *AzureHDInsightCluster yeni*.</span><span class="sxs-lookup"><span data-stu-id="7712c-153">For example, *New-AzureRmHDInsightCluster* vs. *New-AzureHDInsightCluster*.</span></span> <span data-ttu-id="7712c-154">Parametreleri ve anahtarları haber adlara sahip ve çok sayıda yeni parametreler kullanılabilir ARM kullanırken yoktur.</span><span class="sxs-lookup"><span data-stu-id="7712c-154">Parameters and switches may have news names, and there are many new parameters available when using ARM.</span></span>  <span data-ttu-id="7712c-155">Örneğin, birkaç cmdlet'leri adlı yeni bir anahtar gerektiren *- ResourceGroupName*.</span><span class="sxs-lookup"><span data-stu-id="7712c-155">For example, several cmdlets require a new switch called *-ResourceGroupName*.</span></span> 

<span data-ttu-id="7712c-156">Hdınsight cmdlet'lerini kullanabilmek için Azure hesabınıza bağlanın ve yeni bir kaynak grubu oluşturmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="7712c-156">Before you can use the HDInsight cmdlets, you must connect to your Azure account, and create a new resource group:</span></span>

* <span data-ttu-id="7712c-157">Login-AzureRmAccount veya [seçin AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx).</span><span class="sxs-lookup"><span data-stu-id="7712c-157">Login-AzureRmAccount or [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx).</span></span> <span data-ttu-id="7712c-158">Bkz: [bir hizmet sorumlusu Azure Resource Manager ile kimlik doğrulaması](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span><span class="sxs-lookup"><span data-stu-id="7712c-158">See [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span></span>
* [<span data-ttu-id="7712c-159">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7712c-159">New-AzureRmResourceGroup</span></span>](https://msdn.microsoft.com/library/mt603739.aspx)

### <a name="renamed-cmdlets"></a><span data-ttu-id="7712c-160">Yeniden adlandırılmış cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="7712c-160">Renamed cmdlets</span></span>
<span data-ttu-id="7712c-161">Windows PowerShell konsolunda Hdınsight ASM cmdlet'leri listelemek için:</span><span class="sxs-lookup"><span data-stu-id="7712c-161">To list the HDInsight ASM cmdlets in Windows PowerShell console:</span></span>

    help *azurermhdinsight*

<span data-ttu-id="7712c-162">Aşağıdaki tabloda, ASM cmdlet'leri ve ARM modunda adları listelenmektedir:</span><span class="sxs-lookup"><span data-stu-id="7712c-162">The following table lists the ASM cmdlets and their names in the ARM mode:</span></span>

| <span data-ttu-id="7712c-163">ASM cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="7712c-163">ASM cmdlets</span></span> | <span data-ttu-id="7712c-164">ARM cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="7712c-164">ARM cmdlets</span></span> |
| --- | --- |
| <span data-ttu-id="7712c-165">Add-AzureHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="7712c-165">Add-AzureHDInsightConfigValues</span></span> |[<span data-ttu-id="7712c-166">Ekleme AzureRmHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="7712c-166">Add-AzureRmHDInsightConfigValues</span></span>](https://msdn.microsoft.com/library/mt603530.aspx) |
| <span data-ttu-id="7712c-167">Add-AzureHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="7712c-167">Add-AzureHDInsightMetastore</span></span> |[<span data-ttu-id="7712c-168">Ekleme AzureRmHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="7712c-168">Add-AzureRmHDInsightMetastore</span></span>](https://msdn.microsoft.com/library/mt603670.aspx) |
| <span data-ttu-id="7712c-169">Add-AzureHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="7712c-169">Add-AzureHDInsightScriptAction</span></span> |[<span data-ttu-id="7712c-170">Ekleme AzureRmHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="7712c-170">Add-AzureRmHDInsightScriptAction</span></span>](https://msdn.microsoft.com/library/mt603527.aspx) |
| <span data-ttu-id="7712c-171">Add-AzureHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="7712c-171">Add-AzureHDInsightStorage</span></span> |[<span data-ttu-id="7712c-172">Ekleme AzureRmHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="7712c-172">Add-AzureRmHDInsightStorage</span></span>](https://msdn.microsoft.com/library/mt619445.aspx) |
| <span data-ttu-id="7712c-173">Get-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="7712c-173">Get-AzureHDInsightCluster</span></span> |[<span data-ttu-id="7712c-174">Get-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="7712c-174">Get-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619371.aspx) |
| <span data-ttu-id="7712c-175">Get-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="7712c-175">Get-AzureHDInsightJob</span></span> |[<span data-ttu-id="7712c-176">Get-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="7712c-176">Get-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603590.aspx) |
| <span data-ttu-id="7712c-177">Get-AzureHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="7712c-177">Get-AzureHDInsightJobOutput</span></span> |[<span data-ttu-id="7712c-178">Get-AzureRmHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="7712c-178">Get-AzureRmHDInsightJobOutput</span></span>](https://msdn.microsoft.com/library/mt603793.aspx) |
| <span data-ttu-id="7712c-179">Get-AzureHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="7712c-179">Get-AzureHDInsightProperties</span></span> |[<span data-ttu-id="7712c-180">Get-AzureRmHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="7712c-180">Get-AzureRmHDInsightProperties</span></span>](https://msdn.microsoft.com/library/mt603546.aspx) |
| <span data-ttu-id="7712c-181">Grant-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="7712c-181">Grant-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="7712c-182">GRANT-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="7712c-182">Grant-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619407.aspx) |
| <span data-ttu-id="7712c-183">Grant-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="7712c-183">Grant-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="7712c-184">GRANT-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="7712c-184">Grant-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603717.aspx) |
| <span data-ttu-id="7712c-185">Invoke-AzureHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="7712c-185">Invoke-AzureHDInsightHiveJob</span></span> |[<span data-ttu-id="7712c-186">Çağırma AzureRmHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="7712c-186">Invoke-AzureRmHDInsightHiveJob</span></span>](https://msdn.microsoft.com/library/mt603593.aspx) |
| <span data-ttu-id="7712c-187">New-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="7712c-187">New-AzureHDInsightCluster</span></span> |[<span data-ttu-id="7712c-188">AzureRmHDInsightCluster yeni</span><span class="sxs-lookup"><span data-stu-id="7712c-188">New-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619331.aspx) |
| <span data-ttu-id="7712c-189">New-AzureHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="7712c-189">New-AzureHDInsightClusterConfig</span></span> |[<span data-ttu-id="7712c-190">AzureRmHDInsightClusterConfig yeni</span><span class="sxs-lookup"><span data-stu-id="7712c-190">New-AzureRmHDInsightClusterConfig</span></span>](https://msdn.microsoft.com/library/mt603700.aspx) |
| <span data-ttu-id="7712c-191">New-AzureHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="7712c-191">New-AzureHDInsightHiveJobDefinition</span></span> |[<span data-ttu-id="7712c-192">AzureRmHDInsightHiveJobDefinition yeni</span><span class="sxs-lookup"><span data-stu-id="7712c-192">New-AzureRmHDInsightHiveJobDefinition</span></span>](https://msdn.microsoft.com/library/mt619448.aspx) |
| <span data-ttu-id="7712c-193">New-AzureHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="7712c-193">New-AzureHDInsightMapReduceJobDefinition</span></span> |[<span data-ttu-id="7712c-194">AzureRmHDInsightMapReduceJobDefinition yeni</span><span class="sxs-lookup"><span data-stu-id="7712c-194">New-AzureRmHDInsightMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="7712c-195">New-AzureHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="7712c-195">New-AzureHDInsightPigJobDefinition</span></span> |[<span data-ttu-id="7712c-196">AzureRmHDInsightPigJobDefinition yeni</span><span class="sxs-lookup"><span data-stu-id="7712c-196">New-AzureRmHDInsightPigJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603671.aspx) |
| <span data-ttu-id="7712c-197">New-AzureHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="7712c-197">New-AzureHDInsightSqoopJobDefinition</span></span> |[<span data-ttu-id="7712c-198">AzureRmHDInsightSqoopJobDefinition yeni</span><span class="sxs-lookup"><span data-stu-id="7712c-198">New-AzureRmHDInsightSqoopJobDefinition</span></span>](https://msdn.microsoft.com/library/mt608551.aspx) |
| <span data-ttu-id="7712c-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="7712c-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span></span> |[<span data-ttu-id="7712c-200">AzureRmHDInsightStreamingMapReduceJobDefinition yeni</span><span class="sxs-lookup"><span data-stu-id="7712c-200">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="7712c-201">Remove-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="7712c-201">Remove-AzureHDInsightCluster</span></span> |[<span data-ttu-id="7712c-202">Remove-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="7712c-202">Remove-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619431.aspx) |
| <span data-ttu-id="7712c-203">Revoke-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="7712c-203">Revoke-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="7712c-204">REVOKE-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="7712c-204">Revoke-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619375.aspx) |
| <span data-ttu-id="7712c-205">Revoke-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="7712c-205">Revoke-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="7712c-206">REVOKE-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="7712c-206">Revoke-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603523.aspx) |
| <span data-ttu-id="7712c-207">Set-AzureHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="7712c-207">Set-AzureHDInsightClusterSize</span></span> |[<span data-ttu-id="7712c-208">Set-AzureRmHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="7712c-208">Set-AzureRmHDInsightClusterSize</span></span>](https://msdn.microsoft.com/library/mt603513.aspx) |
| <span data-ttu-id="7712c-209">Set-AzureHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="7712c-209">Set-AzureHDInsightDefaultStorage</span></span> |[<span data-ttu-id="7712c-210">Set-AzureRmHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="7712c-210">Set-AzureRmHDInsightDefaultStorage</span></span>](https://msdn.microsoft.com/library/mt603486.aspx) |
| <span data-ttu-id="7712c-211">Start-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="7712c-211">Start-AzureHDInsightJob</span></span> |[<span data-ttu-id="7712c-212">Start-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="7712c-212">Start-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603798.aspx) |
| <span data-ttu-id="7712c-213">Stop-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="7712c-213">Stop-AzureHDInsightJob</span></span> |[<span data-ttu-id="7712c-214">Stop-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="7712c-214">Stop-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt619424.aspx) |
| <span data-ttu-id="7712c-215">Use-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="7712c-215">Use-AzureHDInsightCluster</span></span> |[<span data-ttu-id="7712c-216">Kullanım AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="7712c-216">Use-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619442.aspx) |
| <span data-ttu-id="7712c-217">Wait-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="7712c-217">Wait-AzureHDInsightJob</span></span> |[<span data-ttu-id="7712c-218">Bekleme AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="7712c-218">Wait-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603834.aspx) |

### <a name="new-cmdlets"></a><span data-ttu-id="7712c-219">Yeni cmdlet’ler</span><span class="sxs-lookup"><span data-stu-id="7712c-219">New cmdlets</span></span>
<span data-ttu-id="7712c-220">Yalnızca ARM modunda kullanılabilir yeni cmdlet'leri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="7712c-220">The following are the new cmdlets that are only available in the ARM mode.</span></span> 

<span data-ttu-id="7712c-221">**Betik eylemi cmdlet'leri ilgili:**</span><span class="sxs-lookup"><span data-stu-id="7712c-221">**Script action related cmdlets:**</span></span>

* <span data-ttu-id="7712c-222">**Get-AzureRmHDInsightPersistedScriptAction**: bir küme için kalıcı betik eylemleri alır ve bunları kronolojik sırada listeler veya ayrıntıları için belirtilen kalıcı betik eylemi alır.</span><span class="sxs-lookup"><span data-stu-id="7712c-222">**Get-AzureRmHDInsightPersistedScriptAction**: Gets the persisted script actions for a cluster and lists them in chronological order, or gets details for a specified persisted script action.</span></span> 
* <span data-ttu-id="7712c-223">**Get-AzureRmHDInsightScriptActionHistory**: bir küme için betik eylemi geçmişi alır ve geriye doğru kronolojik sırada listeler ya da daha önce yürütülen betik eylemi ayrıntılarını alır.</span><span class="sxs-lookup"><span data-stu-id="7712c-223">**Get-AzureRmHDInsightScriptActionHistory**: Gets the script action history for a cluster and lists it in reverse chronological order, or gets details of a previously executed script action.</span></span> 
* <span data-ttu-id="7712c-224">**Remove-AzureRmHDInsightPersistedScriptAction**: kalıcı betik eylemi bir Hdınsight kümeden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="7712c-224">**Remove-AzureRmHDInsightPersistedScriptAction**: Removes a persisted script action from an HDInsight cluster.</span></span>
* <span data-ttu-id="7712c-225">**Set-AzureRmHDInsightPersistedScriptAction**: kalıcı betik eylemi olması için daha önce yürütülen betik eylemi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="7712c-225">**Set-AzureRmHDInsightPersistedScriptAction**: Sets a previously executed script action to be a persisted script action.</span></span>
* <span data-ttu-id="7712c-226">**Gönderme AzureRmHDInsightScriptAction**: Azure Hdınsight kümesi için yeni bir betik eylemi gönderir.</span><span class="sxs-lookup"><span data-stu-id="7712c-226">**Submit-AzureRmHDInsightScriptAction**: Submits a new script action to an Azure HDInsight cluster.</span></span> 

<span data-ttu-id="7712c-227">Ek kullanım bilgileri için bkz: [özelleştirme Linux tabanlı Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="7712c-227">For additional usage information, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="7712c-228">**Clsuter kimlik cmdlet'leri ilgili:**</span><span class="sxs-lookup"><span data-stu-id="7712c-228">**Clsuter identity related cmdlets:**</span></span>

* <span data-ttu-id="7712c-229">**Ekleme AzureRmHDInsightClusterIdentity**: Hdınsight kümesi Azure Data Lake depoları erişebilmesi için bir küme kimliği bir küme yapılandırma nesnesine ekler.</span><span class="sxs-lookup"><span data-stu-id="7712c-229">**Add-AzureRmHDInsightClusterIdentity**: Adds a cluster identity to a cluster configuration object so that the HDInsight cluster can access Azure Data Lake Stores.</span></span> <span data-ttu-id="7712c-230">Bkz: [Azure PowerShell kullanarak Data Lake Store ile bir Hdınsight kümesi oluşturmayı](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="7712c-230">See [Create an HDInsight cluster with Data Lake Store using Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

### <a name="examples"></a><span data-ttu-id="7712c-231">Örnekler</span><span class="sxs-lookup"><span data-stu-id="7712c-231">Examples</span></span>
<span data-ttu-id="7712c-232">**Küme oluşturma**</span><span class="sxs-lookup"><span data-stu-id="7712c-232">**Create cluster**</span></span>

<span data-ttu-id="7712c-233">Eski komutu (ASM):</span><span class="sxs-lookup"><span data-stu-id="7712c-233">Old command (ASM):</span></span> 

    New-AzureHDInsightCluster `
        -Name $clusterName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainerName $containerName `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -Credential $httpCredential `
        -SshCredential $sshCredential

<span data-ttu-id="7712c-234">Yeni komut (ARM):</span><span class="sxs-lookup"><span data-stu-id="7712c-234">New command (ARM):</span></span>

    New-AzureRmHDInsightCluster `
        -ClusterName $clusterName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -DefaultStorageAccountName "$storageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $storageAccountKey `
        -DefaultStorageContainer $containerName  `
        -ClusterSizeInNodes 2 `
        -ClusterType Hadoop `
        -OSType Linux `
        -Version "3.2" `
        -HttpCredential $httpcredentials `
        -SshCredential $sshCredentials


<span data-ttu-id="7712c-235">**Küme silme**</span><span class="sxs-lookup"><span data-stu-id="7712c-235">**Delete cluster**</span></span>

<span data-ttu-id="7712c-236">Eski komutu (ASM):</span><span class="sxs-lookup"><span data-stu-id="7712c-236">Old command (ASM):</span></span>

    Remove-AzureHDInsightCluster -name $clusterName 

<span data-ttu-id="7712c-237">Yeni komut (ARM):</span><span class="sxs-lookup"><span data-stu-id="7712c-237">New command (ARM):</span></span>

    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName 

<span data-ttu-id="7712c-238">**Liste küme**</span><span class="sxs-lookup"><span data-stu-id="7712c-238">**List cluster**</span></span>

<span data-ttu-id="7712c-239">Eski komutu (ASM):</span><span class="sxs-lookup"><span data-stu-id="7712c-239">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster

<span data-ttu-id="7712c-240">Yeni komut (ARM):</span><span class="sxs-lookup"><span data-stu-id="7712c-240">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster 

<span data-ttu-id="7712c-241">**Küme Göster**</span><span class="sxs-lookup"><span data-stu-id="7712c-241">**Show cluster**</span></span>

<span data-ttu-id="7712c-242">Eski komutu (ASM):</span><span class="sxs-lookup"><span data-stu-id="7712c-242">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster -Name $clusterName

<span data-ttu-id="7712c-243">Yeni komut (ARM):</span><span class="sxs-lookup"><span data-stu-id="7712c-243">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -clusterName $clusterName


#### <a name="other-samples"></a><span data-ttu-id="7712c-244">Diğer örnekleri</span><span class="sxs-lookup"><span data-stu-id="7712c-244">Other samples</span></span>
* [<span data-ttu-id="7712c-245">Hdınsight kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="7712c-245">Create HDInsight clusters</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [<span data-ttu-id="7712c-246">Hive işlerini gönderme</span><span class="sxs-lookup"><span data-stu-id="7712c-246">Submit Hive jobs</span></span>](hdinsight-hadoop-use-hive-powershell.md)
* [<span data-ttu-id="7712c-247">Pig işleri gönderme</span><span class="sxs-lookup"><span data-stu-id="7712c-247">Submit Pig jobs</span></span>](hdinsight-hadoop-use-pig-powershell.md)
* [<span data-ttu-id="7712c-248">Sqoop işleri gönderme</span><span class="sxs-lookup"><span data-stu-id="7712c-248">Submit Sqoop jobs</span></span>](hdinsight-hadoop-use-sqoop-powershell.md)

## <a name="migrating-to-the-arm-based-hdinsight-net-sdk"></a><span data-ttu-id="7712c-249">ARM tabanlı Hdınsight .NET SDK'sı geçirme</span><span class="sxs-lookup"><span data-stu-id="7712c-249">Migrating to the ARM-based HDInsight .NET SDK</span></span>
<span data-ttu-id="7712c-250">Azure Hizmet Yönetimi-based [(ASM) Hdınsight .NET SDK'sı](https://msdn.microsoft.com/library/azure/mt416619.aspx) artık kullanım dışı bırakılmıştır.</span><span class="sxs-lookup"><span data-stu-id="7712c-250">The Azure Service Management-based [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) is now deprecated.</span></span> <span data-ttu-id="7712c-251">Azure kaynak yönetimi tabanlı kullanmaları [(ARM) Hdınsight .NET SDK'sı](https://msdn.microsoft.com/library/azure/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="7712c-251">You are encouraged to use the Azure Resource Management-based [(ARM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx).</span></span> <span data-ttu-id="7712c-252">Aşağıdaki ASM tabanlı Hdınsight paketleri kullanım dışıdır.</span><span class="sxs-lookup"><span data-stu-id="7712c-252">The following ASM-based HDInsight packages are being deprecated.</span></span>

* `Microsoft.WindowsAzure.Management.HDInsight`
* `Microsoft.Hadoop.Client`

<span data-ttu-id="7712c-253">Bu bölümde ARM tabanlı SDK'sını kullanarak bazı görevleri gerçekleştirmek hakkında daha fazla bilgi için işaretçiler sağlar.</span><span class="sxs-lookup"><span data-stu-id="7712c-253">This section provides pointers to more information on how to perform certain tasks using the ARM-based SDK.</span></span>

| <span data-ttu-id="7712c-254">Nasıl yapılır... ARM tabanlı Hdınsight SDK kullanarak</span><span class="sxs-lookup"><span data-stu-id="7712c-254">How to... using the ARM-based HDInsight SDK</span></span> | <span data-ttu-id="7712c-255">Bağlantılar</span><span class="sxs-lookup"><span data-stu-id="7712c-255">Links</span></span> |
| --- | --- |
| <span data-ttu-id="7712c-256">.NET SDK kullanarak Hdınsight kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="7712c-256">Create HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="7712c-257">Bkz: [Hdınsight kümeleri oluşturma .NET SDK kullanarak](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="7712c-257">See [Create HDInsight clusters using .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="7712c-258">.NET SDK'sı ile betik eylemi kullanarak bir küme özelleştirme</span><span class="sxs-lookup"><span data-stu-id="7712c-258">Customize a cluster using Script Action with .NET SDK</span></span> |<span data-ttu-id="7712c-259">Bkz: [özelleştirme Hdınsight Linux kümeleri betik eylemi kullanarak](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span><span class="sxs-lookup"><span data-stu-id="7712c-259">See [Customize HDInsight Linux clusters using Script Action](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span></span> |
| <span data-ttu-id="7712c-260">.NET SDK'sı ile etkileşimli olarak Azure Active Directory kullanarak uygulamaları kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="7712c-260">Authenticate applications interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="7712c-261">Bkz: [.NET SDK kullanarak Hive sorgularını çalıştırma](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="7712c-261">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span> <span data-ttu-id="7712c-262">Bu makaledeki kod parçacığında, etkileşimli kimlik doğrulaması yaklaşımı kullanır.</span><span class="sxs-lookup"><span data-stu-id="7712c-262">The code snippet in this article uses the interactive authentication approach.</span></span> |
| <span data-ttu-id="7712c-263">Uygulamaları etkileşimsiz .NET SDK ile Azure Active Directory'yi kullanarak kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="7712c-263">Authenticate applications non-interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="7712c-264">Bkz: [Hdınsight için etkileşimli olmayan uygulamalar oluşturma](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span><span class="sxs-lookup"><span data-stu-id="7712c-264">See [Create non-interactive applications for HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span></span> |
| <span data-ttu-id="7712c-265">.NET SDK kullanarak Hive işi Gönder</span><span class="sxs-lookup"><span data-stu-id="7712c-265">Submit a Hive job using .NET SDK</span></span> |<span data-ttu-id="7712c-266">Bkz: [gönderme Hive işleri](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="7712c-266">See [Submit Hive jobs](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="7712c-267">.NET SDK kullanarak bir Pig işi gönderin</span><span class="sxs-lookup"><span data-stu-id="7712c-267">Submit a Pig job using .NET SDK</span></span> |<span data-ttu-id="7712c-268">Bkz: [gönderme Pig işleri](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="7712c-268">See [Submit Pig jobs](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="7712c-269">.NET SDK kullanarak Sqoop işi Gönder</span><span class="sxs-lookup"><span data-stu-id="7712c-269">Submit a Sqoop job using .NET SDK</span></span> |<span data-ttu-id="7712c-270">Bkz: [gönderme Sqoop işleri](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="7712c-270">See [Submit Sqoop jobs](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="7712c-271">.NET SDK kullanarak Hdınsight kümeleri listesi</span><span class="sxs-lookup"><span data-stu-id="7712c-271">List HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="7712c-272">Bkz: [listesi Hdınsight kümeleri](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span><span class="sxs-lookup"><span data-stu-id="7712c-272">See [List HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span></span> |
| <span data-ttu-id="7712c-273">.NET SDK kullanarak Hdınsight kümelerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="7712c-273">Scale HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="7712c-274">Bkz: [ölçek Hdınsight kümeleri](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span><span class="sxs-lookup"><span data-stu-id="7712c-274">See [Scale HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span></span> |
| <span data-ttu-id="7712c-275">.NET SDK kullanarak Hdınsight kümelerini GRANT/revoke erişimi</span><span class="sxs-lookup"><span data-stu-id="7712c-275">Grant/revoke access to HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="7712c-276">Bkz: [Hdınsight kümelerine Grant/revoke erişim](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span><span class="sxs-lookup"><span data-stu-id="7712c-276">See [Grant/revoke access to HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span></span> |
| <span data-ttu-id="7712c-277">HTTP kullanıcı kimlik bilgilerini .NET SDK kullanarak Hdınsight kümelerini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="7712c-277">Update HTTP user credentials for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="7712c-278">Bkz: [Hdınsight kümeleri için güncelleştirme HTTP kullanıcı kimlik bilgileri](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span><span class="sxs-lookup"><span data-stu-id="7712c-278">See [Update HTTP user credentials for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span></span> |
| <span data-ttu-id="7712c-279">.NET SDK kullanarak Hdınsight kümeleri için varsayılan depolama hesabı bulunamadı</span><span class="sxs-lookup"><span data-stu-id="7712c-279">Find the default storage account for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="7712c-280">Bkz: [Hdınsight kümeleri için varsayılan depolama hesabı bulunamadı](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span><span class="sxs-lookup"><span data-stu-id="7712c-280">See [Find the default storage account for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span></span> |
| <span data-ttu-id="7712c-281">.NET SDK kullanarak Hdınsight kümelerini Sil</span><span class="sxs-lookup"><span data-stu-id="7712c-281">Delete HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="7712c-282">Bkz: [silmek Hdınsight kümeleri](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span><span class="sxs-lookup"><span data-stu-id="7712c-282">See [Delete HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span></span> |

### <a name="examples"></a><span data-ttu-id="7712c-283">Örnekler</span><span class="sxs-lookup"><span data-stu-id="7712c-283">Examples</span></span>
<span data-ttu-id="7712c-284">Nasıl bir işlem olduğunu ilişkin bazı örnekler şunlardır ASM tabanlı SDK'sı ve eşdeğer kod parçacığında için ARM tabanlı SDK kullanılarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="7712c-284">Following are some examples on how an operation is performed using the ASM-based SDK and the equivalent code snippet for the ARM-based SDK.</span></span>

<span data-ttu-id="7712c-285">**Bir küme CRUD istemcisi oluşturma**</span><span class="sxs-lookup"><span data-stu-id="7712c-285">**Creating a cluster CRUD client**</span></span>

* <span data-ttu-id="7712c-286">Eski komutu (ASM)</span><span class="sxs-lookup"><span data-stu-id="7712c-286">Old command (ASM)</span></span>
  
        //Certificate auth
        //This logs the application in using a subscription administration certificate, which is not offered in Azure Resource Manager (ARM)
  
        const string subid = "454467d4-60ca-4dfd-a556-216eeeeeeee1";
        var cred = new HDInsightCertificateCredential(new Guid(subid), new X509Certificate2(@"path\to\certificate.cer"));
        var client = HDInsightClient.Connect(cred);
* <span data-ttu-id="7712c-287">Yeni komutu (ARM) (hizmet sorumlusu yetkilendirme)</span><span class="sxs-lookup"><span data-stu-id="7712c-287">New command (ARM) (Service principal authorization)</span></span>
  
        //Service principal auth
        //This will log the application in as itself, rather than on behalf of a specific user.
        //For details, including how to set up the application, see:
        //   https://azure.microsoft.com/en-us/documentation/articles/hdinsight-create-non-interactive-authentication-dotnet-applications/
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);
* <span data-ttu-id="7712c-288">Yeni komutu (ARM) (kullanıcı kimlik doğrulaması)</span><span class="sxs-lookup"><span data-stu-id="7712c-288">New command (ARM) (User authorization)</span></span>
  
        //User auth
        //This will log the application in on behalf of the user.
        //The end-user will see a login popup.
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.User, Id = username };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, AuthenticationFactory.CommonAdTenant, password, ShowDialog.Auto).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);

<span data-ttu-id="7712c-289">**Küme oluşturma**</span><span class="sxs-lookup"><span data-stu-id="7712c-289">**Creating a cluster**</span></span>

* <span data-ttu-id="7712c-290">Eski komutu (ASM)</span><span class="sxs-lookup"><span data-stu-id="7712c-290">Old command (ASM)</span></span>
  
        var clusterInfo = new ClusterCreateParameters
                    {
                        Name = dnsName,
                        DefaultStorageAccountKey = key,
                        DefaultStorageContainer = defaultStorageContainer,
                        DefaultStorageAccountName = storageAccountDnsName,
                        ClusterSizeInNodes = 1,
                        ClusterType = type,
                        Location = "West US",
                        UserName = "admin",
                        Password = "*******",
                        Version = version,
                        HeadNodeSize = NodeVMSize.Large,
                    };
        clusterInfo.CoreConfiguration.Add(new KeyValuePair<string, string>("config1", "value1"));
        client.CreateCluster(clusterInfo);
* <span data-ttu-id="7712c-291">Yeni komutu (ARM)</span><span class="sxs-lookup"><span data-stu-id="7712c-291">New command (ARM)</span></span>
  
        var clusterCreateParameters = new ClusterCreateParameters
            {
                Location = "West US",
                ClusterType = "Hadoop",
                Version = "3.1",
                OSType = OSType.Linux,
                DefaultStorageAccountName = "mystorage.blob.core.windows.net",
                DefaultStorageAccountKey =
                    "O9EQvp3A3AjXq/W27rst1GQfLllhp0gUeiUUn2D8zX2lU3taiXSSfqkZlcPv+nQcYUxYw==",
                UserName = "hadoopuser",
                Password = "*******",
                HeadNodeSize = "ExtraLarge",
                RdpUsername = "hdirp",
                RdpPassword = ""*******",
                RdpAccessExpiry = new DateTime(2025, 3, 1),
                ClusterSizeInNodes = 5
            };
        var coreConfigs = new Dictionary<string, string> {{"config1", "value1"}};
        clusterCreateParameters.Configurations.Add(ConfigurationKey.CoreSite, coreConfigs);

<span data-ttu-id="7712c-292">**HTTP erişimini etkinleştirme**</span><span class="sxs-lookup"><span data-stu-id="7712c-292">**Enabling HTTP access**</span></span>

* <span data-ttu-id="7712c-293">Eski komutu (ASM)</span><span class="sxs-lookup"><span data-stu-id="7712c-293">Old command (ASM)</span></span>
  
        client.EnableHttp(dnsName, "West US", "admin", "*******");
* <span data-ttu-id="7712c-294">Yeni komutu (ARM)</span><span class="sxs-lookup"><span data-stu-id="7712c-294">New command (ARM)</span></span>
  
        var httpParams = new HttpSettingsParameters
        {
               HttpUserEnabled = true,
               HttpUsername = "admin",
               HttpPassword = "*******",
        };
        client.Clusters.ConfigureHttpSettings(resourceGroup, dnsname, httpParams);

<span data-ttu-id="7712c-295">**Küme silme**</span><span class="sxs-lookup"><span data-stu-id="7712c-295">**Deleting a cluster**</span></span>

* <span data-ttu-id="7712c-296">Eski komutu (ASM)</span><span class="sxs-lookup"><span data-stu-id="7712c-296">Old command (ASM)</span></span>
  
        client.DeleteCluster(dnsName);
* <span data-ttu-id="7712c-297">Yeni komutu (ARM)</span><span class="sxs-lookup"><span data-stu-id="7712c-297">New command (ARM)</span></span>
  
        client.Clusters.Delete(resourceGroup, dnsname);

