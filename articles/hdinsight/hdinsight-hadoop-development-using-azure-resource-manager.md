---
title: "aaaMigrate tooAzure kaynak yöneticisi için Hdınsight araçları | Microsoft Docs"
description: "Hdınsight kümeleri için nasıl toomigrate tooAzure Resource Manager geliştirme araçları"
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
ms.openlocfilehash: c087ae63d2544e5badae6be9c258f783aa92e2ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-resource-manager-based-development-tools-for-hdinsight-clusters"></a><span data-ttu-id="a7e1a-103">Hdınsight kümeleri geçirme tooAzure Resource Manager tabanlı geliştirme araçları</span><span class="sxs-lookup"><span data-stu-id="a7e1a-103">Migrating tooAzure Resource Manager-based development tools for HDInsight clusters</span></span>

<span data-ttu-id="a7e1a-104">Hdınsight, Hdınsight için Azure Service Manager ASM tabanlı araçlar kaldırmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a7e1a-104">HDInsight is deprecating Azure Service Manager (ASM)-based tools for HDInsight.</span></span> <span data-ttu-id="a7e1a-105">Azure PowerShell, Azure CLI veya hello Hdınsight .NET SDK'sı toowork Hdınsight kümeleri ile kullanıyorsanız, Azure Resource Manager ARM tabanlı kullanmaları toouse hello sürümleri PowerShell'i, CLI ve .NET SDK'sı ileride.</span><span class="sxs-lookup"><span data-stu-id="a7e1a-105">If you have been using Azure PowerShell, Azure CLI, or hello HDInsight .NET SDK toowork with HDInsight clusters, you are encouraged toouse hello Azure Resource Manager (ARM)-based versions of PowerShell, CLI, and .NET SDK going forward.</span></span> <span data-ttu-id="a7e1a-106">Bu makalede işaretçiler hakkında yönergeler sağlar. toomigrate toohello yeni ARM tabanlı yaklaşım.</span><span class="sxs-lookup"><span data-stu-id="a7e1a-106">This article provides pointers on how toomigrate toohello new ARM-based approach.</span></span> <span data-ttu-id="a7e1a-107">Uygun olduğunda, bu makalede hello ASM ve ARM yaklaşımlar Hdınsight için hello farklarını çıkışı da işaret eder.</span><span class="sxs-lookup"><span data-stu-id="a7e1a-107">Wherever applicable, this article also points out hello differences between hello ASM and ARM approaches for HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a7e1a-108">ASM Hello desteği PowerShell'i, CLI, temel ve .NET SDK'yı Durdur **1 Ocak 2017**.</span><span class="sxs-lookup"><span data-stu-id="a7e1a-108">hello support for ASM based PowerShell, CLI, and .NET SDK will discontinue on **January 1, 2017**.</span></span>
> 
> 

## <a name="migrating-azure-cli-tooazure-resource-manager"></a><span data-ttu-id="a7e1a-109">Geçirme Azure CLI tooAzure Kaynak Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="a7e1a-109">Migrating Azure CLI tooAzure Resource Manager</span></span>
<span data-ttu-id="a7e1a-110">önceki bir yükleme Yükseltmekte olduğunuz sürece hello Azure CLI şimdi tooAzure Resource Manager (ARM) mod, varsayılan olarak; Bu durumda, toouse hello gerekebilir `azure config mode arm` komut tooswitch tooARM modu.</span><span class="sxs-lookup"><span data-stu-id="a7e1a-110">hello Azure CLI now defaults tooAzure Resource Manager (ARM) mode, unless you are upgrading from a previous installation; in this case, you may need toouse hello `azure config mode arm` command tooswitch tooARM mode.</span></span>

<span data-ttu-id="a7e1a-111">Merhaba temel komutları o hello toowork Azure Hizmet Yönetimi (ASM) kullanılarak Hdınsight ile sağlanan Azure CLI olan hello aynı ARM kullanırken; Ancak bazı parametreler ve anahtarları yeni adlara sahip ve çok sayıda yeni parametreler kullanılabilir ARM kullanırken yoktur.</span><span class="sxs-lookup"><span data-stu-id="a7e1a-111">hello basic commands that hello Azure CLI provided toowork with HDInsight using Azure Service Management (ASM) are hello same when using ARM; however some parameters and switches may have new names, and there are many new parameters available when using ARM.</span></span> <span data-ttu-id="a7e1a-112">Örneğin, artık kullanabilirsiniz `azure hdinsight cluster create` toospecify hello Azure sanal bir küme içinde oluşturulmalıdır veya Hive ağ ve Oozie meta depo bilgileri.</span><span class="sxs-lookup"><span data-stu-id="a7e1a-112">For example, you can now use `azure hdinsight cluster create` toospecify hello Azure Virtual Network that a cluster should be created in, or Hive and Oozie metastore information.</span></span>

<span data-ttu-id="a7e1a-113">Hdınsight ile Azure Resource Manager ile çalışmak için temel komutlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a7e1a-113">Basic commands for working with HDInsight through Azure Resource Manager are:</span></span>

* <span data-ttu-id="a7e1a-114">`azure hdinsight cluster create`-Yeni bir Hdınsight kümesi oluşturur</span><span class="sxs-lookup"><span data-stu-id="a7e1a-114">`azure hdinsight cluster create` - creates a new HDInsight cluster</span></span>
* <span data-ttu-id="a7e1a-115">`azure hdinsight cluster delete`-Mevcut bir Hdınsight kümesine siler</span><span class="sxs-lookup"><span data-stu-id="a7e1a-115">`azure hdinsight cluster delete` - deletes an existing HDInsight cluster</span></span>
* <span data-ttu-id="a7e1a-116">`azure hdinsight cluster show`-Varolan bir kümeye hakkındaki bilgileri görüntüleme</span><span class="sxs-lookup"><span data-stu-id="a7e1a-116">`azure hdinsight cluster show` - display information about an existing cluster</span></span>
* <span data-ttu-id="a7e1a-117">`azure hdinsight cluster list`-Azure aboneliğiniz için Hdınsight kümeleri listeler</span><span class="sxs-lookup"><span data-stu-id="a7e1a-117">`azure hdinsight cluster list` - lists HDInsight clusters for your Azure subscription</span></span>

<span data-ttu-id="a7e1a-118">Kullanım hello `-h` tooinspect hello parametreleri ve her komut için kullanılabilen anahtarlar geçin.</span><span class="sxs-lookup"><span data-stu-id="a7e1a-118">Use hello `-h` switch tooinspect hello parameters and switches available for each command.</span></span>

### <a name="new-commands"></a><span data-ttu-id="a7e1a-119">Yeni komutları</span><span class="sxs-lookup"><span data-stu-id="a7e1a-119">New commands</span></span>
<span data-ttu-id="a7e1a-120">Azure Resource Manager ile kullanılabilen yeni komutlar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="a7e1a-120">New commands available with Azure Resource Manager are:</span></span>

* <span data-ttu-id="a7e1a-121">`azure hdinsight cluster resize`-değişiklikleri hello kümedeki çalışan düğümü sayısını dinamik olarak hello</span><span class="sxs-lookup"><span data-stu-id="a7e1a-121">`azure hdinsight cluster resize` - dynamically changes hello number of worker nodes in hello cluster</span></span>
* <span data-ttu-id="a7e1a-122">`azure hdinsight cluster enable-http-access`-HTTPs erişim toohello küme sağlar (üzerinde varsayılan olarak)</span><span class="sxs-lookup"><span data-stu-id="a7e1a-122">`azure hdinsight cluster enable-http-access` - enables HTTPs access toohello cluster (on by default)</span></span>
* <span data-ttu-id="a7e1a-123">`azure hdinsight cluster disable-http-access`-HTTPs erişim toohello küme devre dışı bırakır</span><span class="sxs-lookup"><span data-stu-id="a7e1a-123">`azure hdinsight cluster disable-http-access` - disables HTTPs access toohello cluster</span></span>
* <span data-ttu-id="a7e1a-124">`azure hdinsight script-action`-oluşturma/betik eylemleri bir kümede yönetmek için komutlar sağlar</span><span class="sxs-lookup"><span data-stu-id="a7e1a-124">`azure hdinsight script-action` - provides commands for creating/managing Script Actions on a cluster</span></span>
* <span data-ttu-id="a7e1a-125">`azure hdinsight config`-için bir yapılandırma dosyası oluşturma ile Merhaba kullanılabilir komutlar sağlar `hdinsight cluster create` tooprovide yapılandırma bilgilerini komutu.</span><span class="sxs-lookup"><span data-stu-id="a7e1a-125">`azure hdinsight config` - provides commands for creating a configuration file that can be used with hello `hdinsight cluster create` command tooprovide configuration information.</span></span>

### <a name="deprecated-commands"></a><span data-ttu-id="a7e1a-126">Kullanım dışı komutları</span><span class="sxs-lookup"><span data-stu-id="a7e1a-126">Deprecated commands</span></span>
<span data-ttu-id="a7e1a-127">Merhaba kullanırsanız `azure hdinsight job` komutları toosubmit işleri tooyour Hdınsight kümesi, bunlar hello ARM komutlarını kullanılabilir değildir.</span><span class="sxs-lookup"><span data-stu-id="a7e1a-127">If you use hello `azure hdinsight job` commands toosubmit jobs tooyour HDInsight cluster, these are not available through hello ARM commands.</span></span> <span data-ttu-id="a7e1a-128">Tooprogrammatically gönderme işleri tooHDInsight komut dosyalarından gerekiyorsa, bunun yerine hello Hdınsight tarafından sağlanan REST API'lerini kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="a7e1a-128">If you need tooprogrammatically submit jobs tooHDInsight from scripts, you should instead use hello REST APIs provided by HDInsight.</span></span> <span data-ttu-id="a7e1a-129">REST API'lerini kullanarak işlerini göndermenin daha fazla bilgi için aşağıdaki belgeleri hello bakın.</span><span class="sxs-lookup"><span data-stu-id="a7e1a-129">For more information on submitting jobs using REST APIs, see hello following documents.</span></span>

* [<span data-ttu-id="a7e1a-130">CURL kullanarak Hdınsight'ta Hadoop ile MapReduce işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="a7e1a-130">Run MapReduce jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-mapreduce-curl.md)
* [<span data-ttu-id="a7e1a-131">CURL kullanarak Hdınsight'ta Hadoop ile Hive sorguları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="a7e1a-131">Run Hive queries with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-hive-curl.md)
* [<span data-ttu-id="a7e1a-132">CURL kullanarak Hdınsight'ta Hadoop ile pig işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="a7e1a-132">Run Pig jobs with Hadoop on HDInsight using cURL</span></span>](hdinsight-hadoop-use-pig-curl.md)

<span data-ttu-id="a7e1a-133">Diğer yolları toorun MapReduce hakkında bilgi için Hive ve etkileşimli olarak Pig bkz [hdınsight'ta Hadoop ile MapReduce kullanma](hdinsight-use-mapreduce.md), [hdınsight'ta Hadoop ile Hive kullanma](hdinsight-use-hive.md), ve [Hadoop ile Pig kullanma Hdınsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="a7e1a-133">For information on other ways toorun MapReduce, Hive, and Pig interactively, see [Use MapReduce with Hadoop on HDInsight](hdinsight-use-mapreduce.md), [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md), and [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

### <a name="examples"></a><span data-ttu-id="a7e1a-134">Örnekler</span><span class="sxs-lookup"><span data-stu-id="a7e1a-134">Examples</span></span>
<span data-ttu-id="a7e1a-135">**Küme oluşturma**</span><span class="sxs-lookup"><span data-stu-id="a7e1a-135">**Creating a cluster**</span></span>

* <span data-ttu-id="a7e1a-136">Eski komutu (ASM)-`azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="a7e1a-136">Old command (ASM) - `azure hdinsight cluster create myhdicluster --location northeurope --osType linux --storageAccountName mystorage --storageAccountKey <storagekey> --storageContainer mycontainer --userName admin --password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>
* <span data-ttu-id="a7e1a-137">Yeni komutu (ARM)-`azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span><span class="sxs-lookup"><span data-stu-id="a7e1a-137">New command (ARM) - `azure hdinsight cluster create myhdicluster -g myresourcegroup --location northeurope --osType linux --clusterType hadoop --defaultStorageAccountName mystorage --defaultStorageAccountKey <storagekey> --defaultStorageContainer mycontainer --userName admin -password mypassword --sshUserName sshuser --sshPassword mypassword`</span></span>

<span data-ttu-id="a7e1a-138">**Küme silme**</span><span class="sxs-lookup"><span data-stu-id="a7e1a-138">**Deleting a cluster**</span></span>

* <span data-ttu-id="a7e1a-139">Eski komutu (ASM)-`azure hdinsight cluster delete myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="a7e1a-139">Old command (ASM) - `azure hdinsight cluster delete myhdicluster`</span></span>
* <span data-ttu-id="a7e1a-140">Yeni komutu (ARM)-`azure hdinsight cluster delete mycluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="a7e1a-140">New command (ARM) - `azure hdinsight cluster delete mycluster -g myresourcegroup`</span></span>

<span data-ttu-id="a7e1a-141">**Liste kümeleri**</span><span class="sxs-lookup"><span data-stu-id="a7e1a-141">**List clusters**</span></span>

* <span data-ttu-id="a7e1a-142">Eski komutu (ASM)-`azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="a7e1a-142">Old command (ASM) - `azure hdinsight cluster list`</span></span>
* <span data-ttu-id="a7e1a-143">Yeni komutu (ARM)-`azure hdinsight cluster list`</span><span class="sxs-lookup"><span data-stu-id="a7e1a-143">New command (ARM) - `azure hdinsight cluster list`</span></span>

> [!NOTE]
> <span data-ttu-id="a7e1a-144">Merhaba Listele komutu için kaynak grubunu kullanarak hello belirtme `-g` yalnızca hello kümeler hello belirtilen kaynak grubunda döndürür.</span><span class="sxs-lookup"><span data-stu-id="a7e1a-144">For hello list command, specifying hello resource group using `-g` will return only hello clusters in hello specified resource group.</span></span>
> 
> 

<span data-ttu-id="a7e1a-145">**Küme bilgilerini göster**</span><span class="sxs-lookup"><span data-stu-id="a7e1a-145">**Show cluster information**</span></span>

* <span data-ttu-id="a7e1a-146">Eski komutu (ASM)-`azure hdinsight cluster show myhdicluster`</span><span class="sxs-lookup"><span data-stu-id="a7e1a-146">Old command (ASM) - `azure hdinsight cluster show myhdicluster`</span></span>
* <span data-ttu-id="a7e1a-147">Yeni komutu (ARM)-`azure hdinsight cluster show myhdicluster -g myresourcegroup`</span><span class="sxs-lookup"><span data-stu-id="a7e1a-147">New command (ARM) - `azure hdinsight cluster show myhdicluster -g myresourcegroup`</span></span>

## <a name="migrating-azure-powershell-tooazure-resource-manager"></a><span data-ttu-id="a7e1a-148">Geçirme Azure PowerShell tooAzure Kaynak Yöneticisi</span><span class="sxs-lookup"><span data-stu-id="a7e1a-148">Migrating Azure PowerShell tooAzure Resource Manager</span></span>
<span data-ttu-id="a7e1a-149">Merhaba hello Azure Resource Manager (ARM) modunda Azure PowerShell hakkında genel bilgiler bulunabilir [Azure PowerShell kullanarak Azure Resource Manager ile](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="a7e1a-149">hello general information about Azure PowerShell in hello Azure Resource Manager (ARM) mode can be found at [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="a7e1a-150">Hello Azure PowerShell ARM cmdlet'leri yüklü yan yana hello ASM cmdlet'leri ile olabilir.</span><span class="sxs-lookup"><span data-stu-id="a7e1a-150">hello Azure PowerShell ARM cmdlets can be installed side-by-side with hello ASM cmdlets.</span></span> <span data-ttu-id="a7e1a-151">Merhaba iki moddan Hello cmdlet'leri, adlarına göre ayırt edilebilir.</span><span class="sxs-lookup"><span data-stu-id="a7e1a-151">hello cmdlets from hello two modes can be distinguished by their names.</span></span>  <span data-ttu-id="a7e1a-152">Merhaba ARM modu *AzureRmHDInsight* çok karşılaştırma hello cmdlet'in adlarındaki*AzureHDInsight* hello ASM modunda.</span><span class="sxs-lookup"><span data-stu-id="a7e1a-152">hello ARM mode has *AzureRmHDInsight* in hello cmdlet names comparing too*AzureHDInsight* in hello ASM mode.</span></span>  <span data-ttu-id="a7e1a-153">Örneğin, *yeni AzureRmHDInsightCluster* vs. *AzureHDInsightCluster yeni*.</span><span class="sxs-lookup"><span data-stu-id="a7e1a-153">For example, *New-AzureRmHDInsightCluster* vs. *New-AzureHDInsightCluster*.</span></span> <span data-ttu-id="a7e1a-154">Parametreleri ve anahtarları haber adlara sahip ve çok sayıda yeni parametreler kullanılabilir ARM kullanırken yoktur.</span><span class="sxs-lookup"><span data-stu-id="a7e1a-154">Parameters and switches may have news names, and there are many new parameters available when using ARM.</span></span>  <span data-ttu-id="a7e1a-155">Örneğin, birkaç cmdlet'leri adlı yeni bir anahtar gerektiren *- ResourceGroupName*.</span><span class="sxs-lookup"><span data-stu-id="a7e1a-155">For example, several cmdlets require a new switch called *-ResourceGroupName*.</span></span> 

<span data-ttu-id="a7e1a-156">Merhaba Hdınsight cmdlet'lerini kullanmadan önce tooyour Azure hesabı bağlanmak ve yeni bir kaynak grubu oluşturmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="a7e1a-156">Before you can use hello HDInsight cmdlets, you must connect tooyour Azure account, and create a new resource group:</span></span>

* <span data-ttu-id="a7e1a-157">Login-AzureRmAccount veya [seçin AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx).</span><span class="sxs-lookup"><span data-stu-id="a7e1a-157">Login-AzureRmAccount or [Select-AzureRmProfile](https://msdn.microsoft.com/library/mt619310.aspx).</span></span> <span data-ttu-id="a7e1a-158">Bkz: [bir hizmet sorumlusu Azure Resource Manager ile kimlik doğrulaması](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span><span class="sxs-lookup"><span data-stu-id="a7e1a-158">See [Authenticating a service principal with Azure Resource Manager](../azure-resource-manager/resource-group-authenticate-service-principal.md)</span></span>
* [<span data-ttu-id="a7e1a-159">Yeni-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="a7e1a-159">New-AzureRmResourceGroup</span></span>](https://msdn.microsoft.com/library/mt603739.aspx)

### <a name="renamed-cmdlets"></a><span data-ttu-id="a7e1a-160">Yeniden adlandırılmış cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="a7e1a-160">Renamed cmdlets</span></span>
<span data-ttu-id="a7e1a-161">toolist hello Hdınsight ASM cmdlet'lerini Windows PowerShell konsolunda:</span><span class="sxs-lookup"><span data-stu-id="a7e1a-161">toolist hello HDInsight ASM cmdlets in Windows PowerShell console:</span></span>

    help *azurermhdinsight*

<span data-ttu-id="a7e1a-162">Merhaba aşağıdaki tabloda hello ASM cmdlet'leri ve hello ARM modunda adları listelenmektedir:</span><span class="sxs-lookup"><span data-stu-id="a7e1a-162">hello following table lists hello ASM cmdlets and their names in hello ARM mode:</span></span>

| <span data-ttu-id="a7e1a-163">ASM cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="a7e1a-163">ASM cmdlets</span></span> | <span data-ttu-id="a7e1a-164">ARM cmdlet'leri</span><span class="sxs-lookup"><span data-stu-id="a7e1a-164">ARM cmdlets</span></span> |
| --- | --- |
| <span data-ttu-id="a7e1a-165">Add-AzureHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="a7e1a-165">Add-AzureHDInsightConfigValues</span></span> |[<span data-ttu-id="a7e1a-166">Ekleme AzureRmHDInsightConfigValues</span><span class="sxs-lookup"><span data-stu-id="a7e1a-166">Add-AzureRmHDInsightConfigValues</span></span>](https://msdn.microsoft.com/library/mt603530.aspx) |
| <span data-ttu-id="a7e1a-167">Add-AzureHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="a7e1a-167">Add-AzureHDInsightMetastore</span></span> |[<span data-ttu-id="a7e1a-168">Ekleme AzureRmHDInsightMetastore</span><span class="sxs-lookup"><span data-stu-id="a7e1a-168">Add-AzureRmHDInsightMetastore</span></span>](https://msdn.microsoft.com/library/mt603670.aspx) |
| <span data-ttu-id="a7e1a-169">Add-AzureHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="a7e1a-169">Add-AzureHDInsightScriptAction</span></span> |[<span data-ttu-id="a7e1a-170">Ekleme AzureRmHDInsightScriptAction</span><span class="sxs-lookup"><span data-stu-id="a7e1a-170">Add-AzureRmHDInsightScriptAction</span></span>](https://msdn.microsoft.com/library/mt603527.aspx) |
| <span data-ttu-id="a7e1a-171">Add-AzureHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="a7e1a-171">Add-AzureHDInsightStorage</span></span> |[<span data-ttu-id="a7e1a-172">Ekleme AzureRmHDInsightStorage</span><span class="sxs-lookup"><span data-stu-id="a7e1a-172">Add-AzureRmHDInsightStorage</span></span>](https://msdn.microsoft.com/library/mt619445.aspx) |
| <span data-ttu-id="a7e1a-173">Get-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="a7e1a-173">Get-AzureHDInsightCluster</span></span> |[<span data-ttu-id="a7e1a-174">Get-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="a7e1a-174">Get-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619371.aspx) |
| <span data-ttu-id="a7e1a-175">Get-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="a7e1a-175">Get-AzureHDInsightJob</span></span> |[<span data-ttu-id="a7e1a-176">Get-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="a7e1a-176">Get-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603590.aspx) |
| <span data-ttu-id="a7e1a-177">Get-AzureHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="a7e1a-177">Get-AzureHDInsightJobOutput</span></span> |[<span data-ttu-id="a7e1a-178">Get-AzureRmHDInsightJobOutput</span><span class="sxs-lookup"><span data-stu-id="a7e1a-178">Get-AzureRmHDInsightJobOutput</span></span>](https://msdn.microsoft.com/library/mt603793.aspx) |
| <span data-ttu-id="a7e1a-179">Get-AzureHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="a7e1a-179">Get-AzureHDInsightProperties</span></span> |[<span data-ttu-id="a7e1a-180">Get-AzureRmHDInsightProperties</span><span class="sxs-lookup"><span data-stu-id="a7e1a-180">Get-AzureRmHDInsightProperties</span></span>](https://msdn.microsoft.com/library/mt603546.aspx) |
| <span data-ttu-id="a7e1a-181">Grant-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="a7e1a-181">Grant-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="a7e1a-182">GRANT-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="a7e1a-182">Grant-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619407.aspx) |
| <span data-ttu-id="a7e1a-183">Grant-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="a7e1a-183">Grant-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="a7e1a-184">GRANT-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="a7e1a-184">Grant-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603717.aspx) |
| <span data-ttu-id="a7e1a-185">Invoke-AzureHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="a7e1a-185">Invoke-AzureHDInsightHiveJob</span></span> |[<span data-ttu-id="a7e1a-186">Çağırma AzureRmHDInsightHiveJob</span><span class="sxs-lookup"><span data-stu-id="a7e1a-186">Invoke-AzureRmHDInsightHiveJob</span></span>](https://msdn.microsoft.com/library/mt603593.aspx) |
| <span data-ttu-id="a7e1a-187">New-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="a7e1a-187">New-AzureHDInsightCluster</span></span> |[<span data-ttu-id="a7e1a-188">AzureRmHDInsightCluster yeni</span><span class="sxs-lookup"><span data-stu-id="a7e1a-188">New-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619331.aspx) |
| <span data-ttu-id="a7e1a-189">New-AzureHDInsightClusterConfig</span><span class="sxs-lookup"><span data-stu-id="a7e1a-189">New-AzureHDInsightClusterConfig</span></span> |[<span data-ttu-id="a7e1a-190">AzureRmHDInsightClusterConfig yeni</span><span class="sxs-lookup"><span data-stu-id="a7e1a-190">New-AzureRmHDInsightClusterConfig</span></span>](https://msdn.microsoft.com/library/mt603700.aspx) |
| <span data-ttu-id="a7e1a-191">New-AzureHDInsightHiveJobDefinition</span><span class="sxs-lookup"><span data-stu-id="a7e1a-191">New-AzureHDInsightHiveJobDefinition</span></span> |[<span data-ttu-id="a7e1a-192">AzureRmHDInsightHiveJobDefinition yeni</span><span class="sxs-lookup"><span data-stu-id="a7e1a-192">New-AzureRmHDInsightHiveJobDefinition</span></span>](https://msdn.microsoft.com/library/mt619448.aspx) |
| <span data-ttu-id="a7e1a-193">New-AzureHDInsightMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="a7e1a-193">New-AzureHDInsightMapReduceJobDefinition</span></span> |[<span data-ttu-id="a7e1a-194">AzureRmHDInsightMapReduceJobDefinition yeni</span><span class="sxs-lookup"><span data-stu-id="a7e1a-194">New-AzureRmHDInsightMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="a7e1a-195">New-AzureHDInsightPigJobDefinition</span><span class="sxs-lookup"><span data-stu-id="a7e1a-195">New-AzureHDInsightPigJobDefinition</span></span> |[<span data-ttu-id="a7e1a-196">AzureRmHDInsightPigJobDefinition yeni</span><span class="sxs-lookup"><span data-stu-id="a7e1a-196">New-AzureRmHDInsightPigJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603671.aspx) |
| <span data-ttu-id="a7e1a-197">New-AzureHDInsightSqoopJobDefinition</span><span class="sxs-lookup"><span data-stu-id="a7e1a-197">New-AzureHDInsightSqoopJobDefinition</span></span> |[<span data-ttu-id="a7e1a-198">AzureRmHDInsightSqoopJobDefinition yeni</span><span class="sxs-lookup"><span data-stu-id="a7e1a-198">New-AzureRmHDInsightSqoopJobDefinition</span></span>](https://msdn.microsoft.com/library/mt608551.aspx) |
| <span data-ttu-id="a7e1a-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span><span class="sxs-lookup"><span data-stu-id="a7e1a-199">New-AzureHDInsightStreamingMapReduceJobDefinition</span></span> |[<span data-ttu-id="a7e1a-200">AzureRmHDInsightStreamingMapReduceJobDefinition yeni</span><span class="sxs-lookup"><span data-stu-id="a7e1a-200">New-AzureRmHDInsightStreamingMapReduceJobDefinition</span></span>](https://msdn.microsoft.com/library/mt603626.aspx) |
| <span data-ttu-id="a7e1a-201">Remove-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="a7e1a-201">Remove-AzureHDInsightCluster</span></span> |[<span data-ttu-id="a7e1a-202">Remove-AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="a7e1a-202">Remove-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619431.aspx) |
| <span data-ttu-id="a7e1a-203">Revoke-AzureHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="a7e1a-203">Revoke-AzureHDInsightHttpServicesAccess</span></span> |[<span data-ttu-id="a7e1a-204">REVOKE-AzureRmHDInsightHttpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="a7e1a-204">Revoke-AzureRmHDInsightHttpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt619375.aspx) |
| <span data-ttu-id="a7e1a-205">Revoke-AzureHdinsightRdpAccess</span><span class="sxs-lookup"><span data-stu-id="a7e1a-205">Revoke-AzureHdinsightRdpAccess</span></span> |[<span data-ttu-id="a7e1a-206">REVOKE-AzureRmHDInsightRdpServicesAccess</span><span class="sxs-lookup"><span data-stu-id="a7e1a-206">Revoke-AzureRmHDInsightRdpServicesAccess</span></span>](https://msdn.microsoft.com/library/mt603523.aspx) |
| <span data-ttu-id="a7e1a-207">Set-AzureHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="a7e1a-207">Set-AzureHDInsightClusterSize</span></span> |[<span data-ttu-id="a7e1a-208">Set-AzureRmHDInsightClusterSize</span><span class="sxs-lookup"><span data-stu-id="a7e1a-208">Set-AzureRmHDInsightClusterSize</span></span>](https://msdn.microsoft.com/library/mt603513.aspx) |
| <span data-ttu-id="a7e1a-209">Set-AzureHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="a7e1a-209">Set-AzureHDInsightDefaultStorage</span></span> |[<span data-ttu-id="a7e1a-210">Set-AzureRmHDInsightDefaultStorage</span><span class="sxs-lookup"><span data-stu-id="a7e1a-210">Set-AzureRmHDInsightDefaultStorage</span></span>](https://msdn.microsoft.com/library/mt603486.aspx) |
| <span data-ttu-id="a7e1a-211">Start-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="a7e1a-211">Start-AzureHDInsightJob</span></span> |[<span data-ttu-id="a7e1a-212">Start-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="a7e1a-212">Start-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603798.aspx) |
| <span data-ttu-id="a7e1a-213">Stop-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="a7e1a-213">Stop-AzureHDInsightJob</span></span> |[<span data-ttu-id="a7e1a-214">Stop-AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="a7e1a-214">Stop-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt619424.aspx) |
| <span data-ttu-id="a7e1a-215">Use-AzureHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="a7e1a-215">Use-AzureHDInsightCluster</span></span> |[<span data-ttu-id="a7e1a-216">Kullanım AzureRmHDInsightCluster</span><span class="sxs-lookup"><span data-stu-id="a7e1a-216">Use-AzureRmHDInsightCluster</span></span>](https://msdn.microsoft.com/library/mt619442.aspx) |
| <span data-ttu-id="a7e1a-217">Wait-AzureHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="a7e1a-217">Wait-AzureHDInsightJob</span></span> |[<span data-ttu-id="a7e1a-218">Bekleme AzureRmHDInsightJob</span><span class="sxs-lookup"><span data-stu-id="a7e1a-218">Wait-AzureRmHDInsightJob</span></span>](https://msdn.microsoft.com/library/mt603834.aspx) |

### <a name="new-cmdlets"></a><span data-ttu-id="a7e1a-219">Yeni cmdlet’ler</span><span class="sxs-lookup"><span data-stu-id="a7e1a-219">New cmdlets</span></span>
<span data-ttu-id="a7e1a-220">Merhaba, yalnızca hello ARM modunda kullanılabilir hello yeni cmdlet'ler şunlardır.</span><span class="sxs-lookup"><span data-stu-id="a7e1a-220">hello following are hello new cmdlets that are only available in hello ARM mode.</span></span> 

<span data-ttu-id="a7e1a-221">**Betik eylemi cmdlet'leri ilgili:**</span><span class="sxs-lookup"><span data-stu-id="a7e1a-221">**Script action related cmdlets:**</span></span>

* <span data-ttu-id="a7e1a-222">**Get-AzureRmHDInsightPersistedScriptAction**: alır hello bir küme için betik eylemleri kalıcı kronolojik sırayla listelenir ve Ayrıntılar için belirtilen kalıcı betik eylemi alır.</span><span class="sxs-lookup"><span data-stu-id="a7e1a-222">**Get-AzureRmHDInsightPersistedScriptAction**: Gets hello persisted script actions for a cluster and lists them in chronological order, or gets details for a specified persisted script action.</span></span> 
* <span data-ttu-id="a7e1a-223">**Get-AzureRmHDInsightScriptActionHistory**: hello betik eylemi geçmişi bir küme için alır ve geriye doğru kronolojik sırayla listelenir ya da daha önce yürütülen betik eylemi ayrıntılarını alır.</span><span class="sxs-lookup"><span data-stu-id="a7e1a-223">**Get-AzureRmHDInsightScriptActionHistory**: Gets hello script action history for a cluster and lists it in reverse chronological order, or gets details of a previously executed script action.</span></span> 
* <span data-ttu-id="a7e1a-224">**Remove-AzureRmHDInsightPersistedScriptAction**: kalıcı betik eylemi bir Hdınsight kümeden kaldırır.</span><span class="sxs-lookup"><span data-stu-id="a7e1a-224">**Remove-AzureRmHDInsightPersistedScriptAction**: Removes a persisted script action from an HDInsight cluster.</span></span>
* <span data-ttu-id="a7e1a-225">**Set-AzureRmHDInsightPersistedScriptAction**: daha önce yürütülen betik eylemi toobe kalıcı betik eylemi ayarlar.</span><span class="sxs-lookup"><span data-stu-id="a7e1a-225">**Set-AzureRmHDInsightPersistedScriptAction**: Sets a previously executed script action toobe a persisted script action.</span></span>
* <span data-ttu-id="a7e1a-226">**Gönderme AzureRmHDInsightScriptAction**: yeni bir komut dosyası eylemi tooan Azure Hdınsight kümesi gönderir.</span><span class="sxs-lookup"><span data-stu-id="a7e1a-226">**Submit-AzureRmHDInsightScriptAction**: Submits a new script action tooan Azure HDInsight cluster.</span></span> 

<span data-ttu-id="a7e1a-227">Ek kullanım bilgileri için bkz: [özelleştirme Linux tabanlı Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a7e1a-227">For additional usage information, see [Customize Linux-based HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="a7e1a-228">**Clsuter kimlik cmdlet'leri ilgili:**</span><span class="sxs-lookup"><span data-stu-id="a7e1a-228">**Clsuter identity related cmdlets:**</span></span>

* <span data-ttu-id="a7e1a-229">**Ekleme AzureRmHDInsightClusterIdentity**: Merhaba Hdınsight kümesi Azure Data Lake depoları erişebilmesi için bir küme kimlik tooa küme yapılandırma nesnesi ekler.</span><span class="sxs-lookup"><span data-stu-id="a7e1a-229">**Add-AzureRmHDInsightClusterIdentity**: Adds a cluster identity tooa cluster configuration object so that hello HDInsight cluster can access Azure Data Lake Stores.</span></span> <span data-ttu-id="a7e1a-230">Bkz: [Azure PowerShell kullanarak Data Lake Store ile bir Hdınsight kümesi oluşturmayı](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a7e1a-230">See [Create an HDInsight cluster with Data Lake Store using Azure PowerShell](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md).</span></span>

### <a name="examples"></a><span data-ttu-id="a7e1a-231">Örnekler</span><span class="sxs-lookup"><span data-stu-id="a7e1a-231">Examples</span></span>
<span data-ttu-id="a7e1a-232">**Küme oluşturma**</span><span class="sxs-lookup"><span data-stu-id="a7e1a-232">**Create cluster**</span></span>

<span data-ttu-id="a7e1a-233">Eski komutu (ASM):</span><span class="sxs-lookup"><span data-stu-id="a7e1a-233">Old command (ASM):</span></span> 

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

<span data-ttu-id="a7e1a-234">Yeni komut (ARM):</span><span class="sxs-lookup"><span data-stu-id="a7e1a-234">New command (ARM):</span></span>

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


<span data-ttu-id="a7e1a-235">**Küme silme**</span><span class="sxs-lookup"><span data-stu-id="a7e1a-235">**Delete cluster**</span></span>

<span data-ttu-id="a7e1a-236">Eski komutu (ASM):</span><span class="sxs-lookup"><span data-stu-id="a7e1a-236">Old command (ASM):</span></span>

    Remove-AzureHDInsightCluster -name $clusterName 

<span data-ttu-id="a7e1a-237">Yeni komut (ARM):</span><span class="sxs-lookup"><span data-stu-id="a7e1a-237">New command (ARM):</span></span>

    Remove-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName 

<span data-ttu-id="a7e1a-238">**Liste küme**</span><span class="sxs-lookup"><span data-stu-id="a7e1a-238">**List cluster**</span></span>

<span data-ttu-id="a7e1a-239">Eski komutu (ASM):</span><span class="sxs-lookup"><span data-stu-id="a7e1a-239">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster

<span data-ttu-id="a7e1a-240">Yeni komut (ARM):</span><span class="sxs-lookup"><span data-stu-id="a7e1a-240">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster 

<span data-ttu-id="a7e1a-241">**Küme Göster**</span><span class="sxs-lookup"><span data-stu-id="a7e1a-241">**Show cluster**</span></span>

<span data-ttu-id="a7e1a-242">Eski komutu (ASM):</span><span class="sxs-lookup"><span data-stu-id="a7e1a-242">Old command (ASM):</span></span>

    Get-AzureHDInsightCluster -Name $clusterName

<span data-ttu-id="a7e1a-243">Yeni komut (ARM):</span><span class="sxs-lookup"><span data-stu-id="a7e1a-243">New command (ARM):</span></span>

    Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -clusterName $clusterName


#### <a name="other-samples"></a><span data-ttu-id="a7e1a-244">Diğer örnekleri</span><span class="sxs-lookup"><span data-stu-id="a7e1a-244">Other samples</span></span>
* [<span data-ttu-id="a7e1a-245">Hdınsight kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="a7e1a-245">Create HDInsight clusters</span></span>](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)
* [<span data-ttu-id="a7e1a-246">Hive işlerini gönderme</span><span class="sxs-lookup"><span data-stu-id="a7e1a-246">Submit Hive jobs</span></span>](hdinsight-hadoop-use-hive-powershell.md)
* [<span data-ttu-id="a7e1a-247">Pig işleri gönderme</span><span class="sxs-lookup"><span data-stu-id="a7e1a-247">Submit Pig jobs</span></span>](hdinsight-hadoop-use-pig-powershell.md)
* [<span data-ttu-id="a7e1a-248">Sqoop işleri gönderme</span><span class="sxs-lookup"><span data-stu-id="a7e1a-248">Submit Sqoop jobs</span></span>](hdinsight-hadoop-use-sqoop-powershell.md)

## <a name="migrating-toohello-arm-based-hdinsight-net-sdk"></a><span data-ttu-id="a7e1a-249">Geçirme toohello ARM tabanlı Hdınsight .NET SDK'sı</span><span class="sxs-lookup"><span data-stu-id="a7e1a-249">Migrating toohello ARM-based HDInsight .NET SDK</span></span>
<span data-ttu-id="a7e1a-250">Azure Hizmet Yönetimi-based hello [(ASM) Hdınsight .NET SDK'sı](https://msdn.microsoft.com/library/azure/mt416619.aspx) artık kullanım dışı bırakılmıştır.</span><span class="sxs-lookup"><span data-stu-id="a7e1a-250">hello Azure Service Management-based [(ASM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt416619.aspx) is now deprecated.</span></span> <span data-ttu-id="a7e1a-251">Kullanmaları toouse olan Azure kaynak yönetimi tabanlı hello [(ARM) Hdınsight .NET SDK'sı](https://msdn.microsoft.com/library/azure/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="a7e1a-251">You are encouraged toouse hello Azure Resource Management-based [(ARM) HDInsight .NET SDK](https://msdn.microsoft.com/library/azure/mt271028.aspx).</span></span> <span data-ttu-id="a7e1a-252">Merhaba aşağıdaki ASM tabanlı Hdınsight paketleri itibaren kullanımdan kalkacaktır.</span><span class="sxs-lookup"><span data-stu-id="a7e1a-252">hello following ASM-based HDInsight packages are being deprecated.</span></span>

* `Microsoft.WindowsAzure.Management.HDInsight`
* `Microsoft.Hadoop.Client`

<span data-ttu-id="a7e1a-253">Bu bölümde işaretçileri toomore ilgili bilgiler verilmektedir tooperform kullanarak görevleri hello ARM tabanlı SDK belirli.</span><span class="sxs-lookup"><span data-stu-id="a7e1a-253">This section provides pointers toomore information on how tooperform certain tasks using hello ARM-based SDK.</span></span>

| <span data-ttu-id="a7e1a-254">Nasıl yapılır... hello ARM tabanlı Hdınsight SDK kullanarak</span><span class="sxs-lookup"><span data-stu-id="a7e1a-254">How to... using hello ARM-based HDInsight SDK</span></span> | <span data-ttu-id="a7e1a-255">Bağlantılar</span><span class="sxs-lookup"><span data-stu-id="a7e1a-255">Links</span></span> |
| --- | --- |
| <span data-ttu-id="a7e1a-256">.NET SDK kullanarak Hdınsight kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="a7e1a-256">Create HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="a7e1a-257">Bkz: [Hdınsight kümeleri oluşturma .NET SDK kullanarak](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="a7e1a-257">See [Create HDInsight clusters using .NET SDK](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="a7e1a-258">.NET SDK'sı ile betik eylemi kullanarak bir küme özelleştirme</span><span class="sxs-lookup"><span data-stu-id="a7e1a-258">Customize a cluster using Script Action with .NET SDK</span></span> |<span data-ttu-id="a7e1a-259">Bkz: [özelleştirme Hdınsight Linux kümeleri betik eylemi kullanarak](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span><span class="sxs-lookup"><span data-stu-id="a7e1a-259">See [Customize HDInsight Linux clusters using Script Action](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md#use-script-action)</span></span> |
| <span data-ttu-id="a7e1a-260">.NET SDK'sı ile etkileşimli olarak Azure Active Directory kullanarak uygulamaları kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="a7e1a-260">Authenticate applications interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="a7e1a-261">Bkz: [.NET SDK kullanarak Hive sorgularını çalıştırma](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="a7e1a-261">See [Run Hive queries using .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span> <span data-ttu-id="a7e1a-262">Bu makalede Hello kod parçacığını hello etkileşimli kimlik doğrulaması yaklaşımı kullanır.</span><span class="sxs-lookup"><span data-stu-id="a7e1a-262">hello code snippet in this article uses hello interactive authentication approach.</span></span> |
| <span data-ttu-id="a7e1a-263">Uygulamaları etkileşimsiz .NET SDK ile Azure Active Directory'yi kullanarak kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="a7e1a-263">Authenticate applications non-interactively using Azure Active Directory with .NET SDK</span></span> |<span data-ttu-id="a7e1a-264">Bkz: [Hdınsight için etkileşimli olmayan uygulamalar oluşturma](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span><span class="sxs-lookup"><span data-stu-id="a7e1a-264">See [Create non-interactive applications for HDInsight](hdinsight-create-non-interactive-authentication-dotnet-applications.md)</span></span> |
| <span data-ttu-id="a7e1a-265">.NET SDK kullanarak Hive işi Gönder</span><span class="sxs-lookup"><span data-stu-id="a7e1a-265">Submit a Hive job using .NET SDK</span></span> |<span data-ttu-id="a7e1a-266">Bkz: [gönderme Hive işleri](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="a7e1a-266">See [Submit Hive jobs](hdinsight-hadoop-use-hive-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="a7e1a-267">.NET SDK kullanarak bir Pig işi gönderin</span><span class="sxs-lookup"><span data-stu-id="a7e1a-267">Submit a Pig job using .NET SDK</span></span> |<span data-ttu-id="a7e1a-268">Bkz: [gönderme Pig işleri](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="a7e1a-268">See [Submit Pig jobs](hdinsight-hadoop-use-pig-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="a7e1a-269">.NET SDK kullanarak Sqoop işi Gönder</span><span class="sxs-lookup"><span data-stu-id="a7e1a-269">Submit a Sqoop job using .NET SDK</span></span> |<span data-ttu-id="a7e1a-270">Bkz: [gönderme Sqoop işleri](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span><span class="sxs-lookup"><span data-stu-id="a7e1a-270">See [Submit Sqoop jobs](hdinsight-hadoop-use-sqoop-dotnet-sdk.md)</span></span> |
| <span data-ttu-id="a7e1a-271">.NET SDK kullanarak Hdınsight kümeleri listesi</span><span class="sxs-lookup"><span data-stu-id="a7e1a-271">List HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="a7e1a-272">Bkz: [listesi Hdınsight kümeleri](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span><span class="sxs-lookup"><span data-stu-id="a7e1a-272">See [List HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#list-clusters)</span></span> |
| <span data-ttu-id="a7e1a-273">.NET SDK kullanarak Hdınsight kümelerini ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="a7e1a-273">Scale HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="a7e1a-274">Bkz: [ölçek Hdınsight kümeleri](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span><span class="sxs-lookup"><span data-stu-id="a7e1a-274">See [Scale HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#scale-clusters)</span></span> |
| <span data-ttu-id="a7e1a-275">.NET SDK kullanarak Grant/revoke erişim tooHDInsight kümeleri</span><span class="sxs-lookup"><span data-stu-id="a7e1a-275">Grant/revoke access tooHDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="a7e1a-276">Bkz: [Grant/revoke erişim tooHDInsight kümeleri](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span><span class="sxs-lookup"><span data-stu-id="a7e1a-276">See [Grant/revoke access tooHDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#grantrevoke-access)</span></span> |
| <span data-ttu-id="a7e1a-277">HTTP kullanıcı kimlik bilgilerini .NET SDK kullanarak Hdınsight kümelerini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="a7e1a-277">Update HTTP user credentials for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="a7e1a-278">Bkz: [Hdınsight kümeleri için güncelleştirme HTTP kullanıcı kimlik bilgileri](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span><span class="sxs-lookup"><span data-stu-id="a7e1a-278">See [Update HTTP user credentials for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#update-http-user-credentials)</span></span> |
| <span data-ttu-id="a7e1a-279">.NET SDK kullanarak Hdınsight kümeleri için Hello varsayılan depolama hesabı bulunamadı</span><span class="sxs-lookup"><span data-stu-id="a7e1a-279">Find hello default storage account for HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="a7e1a-280">Bkz: [Hdınsight kümeleri için hello varsayılan depolama hesabı bulunamadı](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span><span class="sxs-lookup"><span data-stu-id="a7e1a-280">See [Find hello default storage account for HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#find-the-default-storage-account)</span></span> |
| <span data-ttu-id="a7e1a-281">.NET SDK kullanarak Hdınsight kümelerini Sil</span><span class="sxs-lookup"><span data-stu-id="a7e1a-281">Delete HDInsight clusters using .NET SDK</span></span> |<span data-ttu-id="a7e1a-282">Bkz: [silmek Hdınsight kümeleri](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span><span class="sxs-lookup"><span data-stu-id="a7e1a-282">See [Delete HDInsight clusters](hdinsight-administer-use-dotnet-sdk.md#delete-clusters)</span></span> |

### <a name="examples"></a><span data-ttu-id="a7e1a-283">Örnekler</span><span class="sxs-lookup"><span data-stu-id="a7e1a-283">Examples</span></span>
<span data-ttu-id="a7e1a-284">Nasıl bir işlem olduğunu ilişkin bazı örnekler şunlardır hello ASM tabanlı SDK ve hello eşdeğer kod parçacığını Merhaba ARM tabanlı SDK kullanılarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="a7e1a-284">Following are some examples on how an operation is performed using hello ASM-based SDK and hello equivalent code snippet for hello ARM-based SDK.</span></span>

<span data-ttu-id="a7e1a-285">**Bir küme CRUD istemcisi oluşturma**</span><span class="sxs-lookup"><span data-stu-id="a7e1a-285">**Creating a cluster CRUD client**</span></span>

* <span data-ttu-id="a7e1a-286">Eski komutu (ASM)</span><span class="sxs-lookup"><span data-stu-id="a7e1a-286">Old command (ASM)</span></span>
  
        //Certificate auth
        //This logs hello application in using a subscription administration certificate, which is not offered in Azure Resource Manager (ARM)
  
        const string subid = "454467d4-60ca-4dfd-a556-216eeeeeeee1";
        var cred = new HDInsightCertificateCredential(new Guid(subid), new X509Certificate2(@"path\to\certificate.cer"));
        var client = HDInsightClient.Connect(cred);
* <span data-ttu-id="a7e1a-287">Yeni komutu (ARM) (hizmet sorumlusu yetkilendirme)</span><span class="sxs-lookup"><span data-stu-id="a7e1a-287">New command (ARM) (Service principal authorization)</span></span>
  
        //Service principal auth
        //This will log hello application in as itself, rather than on behalf of a specific user.
        //For details, including how tooset up hello application, see:
        //   https://azure.microsoft.com/en-us/documentation/articles/hdinsight-create-non-interactive-authentication-dotnet-applications/
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.ServicePrincipal, Id = clientId };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, tenantId, secretKey, ShowDialog.Never).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);
* <span data-ttu-id="a7e1a-288">Yeni komutu (ARM) (kullanıcı kimlik doğrulaması)</span><span class="sxs-lookup"><span data-stu-id="a7e1a-288">New command (ARM) (User authorization)</span></span>
  
        //User auth
        //This will log hello application in on behalf of hello user.
        //hello end-user will see a login popup.
  
        var authFactory = new AuthenticationFactory();
  
        var account = new AzureAccount { Type = AzureAccount.AccountType.User, Id = username };
  
        var env = AzureEnvironment.PublicEnvironments[EnvironmentName.AzureCloud];
  
        var accessToken = authFactory.Authenticate(account, env, AuthenticationFactory.CommonAdTenant, password, ShowDialog.Auto).AccessToken;
  
        var creds = new TokenCloudCredentials(subId.ToString(), accessToken);
  
        _hdiManagementClient = new HDInsightManagementClient(creds);

<span data-ttu-id="a7e1a-289">**Küme oluşturma**</span><span class="sxs-lookup"><span data-stu-id="a7e1a-289">**Creating a cluster**</span></span>

* <span data-ttu-id="a7e1a-290">Eski komutu (ASM)</span><span class="sxs-lookup"><span data-stu-id="a7e1a-290">Old command (ASM)</span></span>
  
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
* <span data-ttu-id="a7e1a-291">Yeni komutu (ARM)</span><span class="sxs-lookup"><span data-stu-id="a7e1a-291">New command (ARM)</span></span>
  
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

<span data-ttu-id="a7e1a-292">**HTTP erişimini etkinleştirme**</span><span class="sxs-lookup"><span data-stu-id="a7e1a-292">**Enabling HTTP access**</span></span>

* <span data-ttu-id="a7e1a-293">Eski komutu (ASM)</span><span class="sxs-lookup"><span data-stu-id="a7e1a-293">Old command (ASM)</span></span>
  
        client.EnableHttp(dnsName, "West US", "admin", "*******");
* <span data-ttu-id="a7e1a-294">Yeni komutu (ARM)</span><span class="sxs-lookup"><span data-stu-id="a7e1a-294">New command (ARM)</span></span>
  
        var httpParams = new HttpSettingsParameters
        {
               HttpUserEnabled = true,
               HttpUsername = "admin",
               HttpPassword = "*******",
        };
        client.Clusters.ConfigureHttpSettings(resourceGroup, dnsname, httpParams);

<span data-ttu-id="a7e1a-295">**Küme silme**</span><span class="sxs-lookup"><span data-stu-id="a7e1a-295">**Deleting a cluster**</span></span>

* <span data-ttu-id="a7e1a-296">Eski komutu (ASM)</span><span class="sxs-lookup"><span data-stu-id="a7e1a-296">Old command (ASM)</span></span>
  
        client.DeleteCluster(dnsName);
* <span data-ttu-id="a7e1a-297">Yeni komutu (ARM)</span><span class="sxs-lookup"><span data-stu-id="a7e1a-297">New command (ARM)</span></span>
  
        client.Clusters.Delete(resourceGroup, dnsname);

