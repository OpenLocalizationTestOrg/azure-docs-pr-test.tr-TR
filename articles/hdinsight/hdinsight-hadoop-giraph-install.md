---
title: "Giraph hadoop'ta aaaInstall ve kullanım Hdınsight'ta - Azure kümeleri | Microsoft Docs"
description: "Toocustomize Hdınsight küme nasıl ile Giraph ve nasıl öğrenin toouse Giraph."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 77a1d0e0-55de-4e61-98a0-060914fb7ca0
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: bd473faca9d3c87c29d7566a18fc94211c50f059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-giraph-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="b6169-103">Yükleme ve Windows tabanlı Hdınsight kümelerinde Giraph kullanma</span><span class="sxs-lookup"><span data-stu-id="b6169-103">Install and use Giraph on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="b6169-104">Betik eylemi kullanarak Giraph ile toocustomize Windows Hdınsight kümesi nasıl ve ne öğrenin toouse Giraph tooprocess büyük ölçekli grafikleri.</span><span class="sxs-lookup"><span data-stu-id="b6169-104">Learn how toocustomize Windows based HDInsight cluster with Giraph using Script Action, and how toouse Giraph tooprocess large-scale graphs.</span></span> <span data-ttu-id="b6169-105">Linux tabanlı bir kümeyle Giraph kullanma hakkında daha fazla bilgi için bkz: [yükleme Giraph Hdınsight Hadoop kümeleri (Linux) üzerinde](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="b6169-105">For information on using Giraph with a Linux-based cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b6169-106">Merhaba Windows tabanlı Hdınsight kümeleri ile bu belgeyi yalnızca çalışma adımları.</span><span class="sxs-lookup"><span data-stu-id="b6169-106">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="b6169-107">Hdınsight yalnızca Windows'da Hdınsight 3.4 ' düşük sürümleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b6169-107">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="b6169-108">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="b6169-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b6169-109">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="b6169-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="b6169-110">Hakkında bilgi için bir Linux tabanlı Hdınsight kümesinde tooinstall Giraph bkz [yükleme Giraph Hdınsight Hadoop kümeleri (Linux) üzerinde](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="b6169-110">For information on how tooinstall Giraph on a Linux-based HDInsight cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>


<span data-ttu-id="b6169-111">Kullanarak Azure Hdınsight (Hadoop, Storm, HBase, Spark) kümede herhangi bir türde üzerinde Giraph yükleyebilirsiniz *betik eylemi*.</span><span class="sxs-lookup"><span data-stu-id="b6169-111">You can install Giraph on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="b6169-112">Hdınsight kümesinde bir örnek komut dosyası tooinstall Giraph salt okunur Azure depolama blobunu gelen kullanılabilir [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="b6169-112">A sample script tooinstall Giraph on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span> <span data-ttu-id="b6169-113">Merhaba örnek betik yalnızca Hdınsight küme sürümü ile 3.1 çalışır.</span><span class="sxs-lookup"><span data-stu-id="b6169-113">hello sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="b6169-114">Hdınsight küme sürümleri hakkında daha fazla bilgi için bkz: [Hdınsight küme sürümleri](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="b6169-114">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="b6169-115">**İlgili makaleler**</span><span class="sxs-lookup"><span data-stu-id="b6169-115">**Related articles**</span></span>

* [<span data-ttu-id="b6169-116">Giraph Hdınsight Hadoop kümeleri (Linux) yükleyin</span><span class="sxs-lookup"><span data-stu-id="b6169-116">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="b6169-117">[Hdınsight'ta Hadoop kümeleri oluşturma](hdinsight-provision-clusters.md): Hdınsight kümeleri oluşturma hakkında genel bilgi.</span><span class="sxs-lookup"><span data-stu-id="b6169-117">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="b6169-118">[Betik eylemi kullanarak Hdınsight kümesi özelleştirme][hdinsight-cluster-customize]: betik eylemi kullanarak Hdınsight kümelerini özelleştirme hakkında genel bilgi.</span><span class="sxs-lookup"><span data-stu-id="b6169-118">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="b6169-119">[Hdınsight için betik eylemi betikleri geliştirme](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="b6169-119">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-giraph"></a><span data-ttu-id="b6169-120">Giraph nedir?</span><span class="sxs-lookup"><span data-stu-id="b6169-120">What is Giraph?</span></span>
<span data-ttu-id="b6169-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> tooperform grafik Hadoop kullanarak işleme sağlar ve Azure Hdınsight ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="b6169-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="b6169-122">Grafikleri hello Internet gibi büyük bir ağdaki yönlendiricileri arasındaki hello bağlantıları gibi nesneler arasındaki ilişkileri modellemek veya sosyal ağlarda (bazen başvurulan tooas sosyal grafiği) arasındaki ilişkileri kişiler.</span><span class="sxs-lookup"><span data-stu-id="b6169-122">Graphs model relationships between objects, such as hello connections between routers on a large network like hello Internet, or relationships between people on social networks (sometimes referred tooas a social graph).</span></span> <span data-ttu-id="b6169-123">Grafik işleme hello bir grafik nesneleri arasındaki ilişkiler hakkında tooreason gibi sağlar:</span><span class="sxs-lookup"><span data-stu-id="b6169-123">Graph processing allows you tooreason about hello relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="b6169-124">Geçerli ilişkilere dayanan olası arkadaş tanımlama.</span><span class="sxs-lookup"><span data-stu-id="b6169-124">Identifying potential friends based on your current relationships.</span></span>
* <span data-ttu-id="b6169-125">Merhaba kısa rotayı bir ağda iki bilgisayar arasında tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="b6169-125">Identifying hello shortest route between two computers in a network.</span></span>
* <span data-ttu-id="b6169-126">Web sayfalarının Hello sayfa derecesini hesaplama.</span><span class="sxs-lookup"><span data-stu-id="b6169-126">Calculating hello page rank of webpages.</span></span>

## <a name="install-giraph-using-portal"></a><span data-ttu-id="b6169-127">Portal kullanarak Giraph yükleyin</span><span class="sxs-lookup"><span data-stu-id="b6169-127">Install Giraph using portal</span></span>
1. <span data-ttu-id="b6169-128">Hello kullanarak bir küme oluşturmaya başlamak **özel Oluştur** konusunda açıklandığı gibi seçeneği [Hdınsight'ta oluşturmak Hadoop kümeleri](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="b6169-128">Start creating a cluster by using hello **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="b6169-129">Hello üzerinde **betik eylemleri** sayfa hello Sihirbazı'nın tıklatın **betik eylemi eklemek** tooprovide aşağıda gösterildiği gibi hello betik eylemi hakkında ayrıntıları:</span><span class="sxs-lookup"><span data-stu-id="b6169-129">On hello **Script Actions** page of hello wizard, click **add script action** tooprovide details about hello script action, as shown below:</span></span>

    <span data-ttu-id="b6169-130">![Betik eylemi toocustomize bir küme kullanın](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "kullanım betik eylemi toocustomize küme")</span><span class="sxs-lookup"><span data-stu-id="b6169-130">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="b6169-131">Özellik</span><span class="sxs-lookup"><span data-stu-id="b6169-131">Property</span></span></th><th><span data-ttu-id="b6169-132">Değer</span><span class="sxs-lookup"><span data-stu-id="b6169-132">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="b6169-133">Ad</span><span class="sxs-lookup"><span data-stu-id="b6169-133">Name</span></span></td>
            <td><span data-ttu-id="b6169-134">Merhaba betik eylemi için bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="b6169-134">Specify a name for hello script action.</span></span> <span data-ttu-id="b6169-135">Örneğin, <b>yükleme Giraph</b>.</span><span class="sxs-lookup"><span data-stu-id="b6169-135">For example, <b>Install Giraph</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="b6169-136">Betik URI'si</span><span class="sxs-lookup"><span data-stu-id="b6169-136">Script URI</span></span></td>
            <td><span data-ttu-id="b6169-137">Çağrılan toocustomize hello küme hello Tekdüzen Kaynak Tanımlayıcısı (URI) toohello komut dosyasını belirtin.</span><span class="sxs-lookup"><span data-stu-id="b6169-137">Specify hello Uniform Resource Identifier (URI) toohello script that is invoked toocustomize hello cluster.</span></span> <span data-ttu-id="b6169-138">Örneğin, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span><span class="sxs-lookup"><span data-stu-id="b6169-138">For example, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="b6169-139">Düğüm Türü</span><span class="sxs-lookup"><span data-stu-id="b6169-139">Node Type</span></span></td>
            <td><span data-ttu-id="b6169-140">Merhaba özelleştirme betik çalıştığı hello düğüm belirtin.</span><span class="sxs-lookup"><span data-stu-id="b6169-140">Specify hello nodes on which hello customization script is run.</span></span> <span data-ttu-id="b6169-141">Seçebileceğiniz <b>tüm düğümleri</b>, <b>Head yalnızca düğümlerin</b>, veya <b>yalnızca çalışan düğümleri</b>.</span><span class="sxs-lookup"><span data-stu-id="b6169-141">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="b6169-142">Parametreler</span><span class="sxs-lookup"><span data-stu-id="b6169-142">Parameters</span></span></td>
            <td><span data-ttu-id="b6169-143">Merhaba komut dosyası için gereken Hello parametreleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="b6169-143">Specify hello parameters, if required by hello script.</span></span> <span data-ttu-id="b6169-144">Bunu boş bırakabilirsiniz şekilde hello betik tooinstall Giraph herhangi bir parametre gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="b6169-144">hello script tooinstall Giraph does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="b6169-145">Birden fazla betik eylemi tooinstall hello kümede birden çok bileşen ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6169-145">You can add more than one script action tooinstall multiple components on hello cluster.</span></span> <span data-ttu-id="b6169-146">Merhaba komut dosyaları ekledikten sonra hello küme oluşturma hello onay işareti toostart tıklayın.</span><span class="sxs-lookup"><span data-stu-id="b6169-146">After you have added hello scripts, click hello checkmark toostart creating hello cluster.</span></span>

## <a name="use-giraph"></a><span data-ttu-id="b6169-147">Giraph kullanma</span><span class="sxs-lookup"><span data-stu-id="b6169-147">Use Giraph</span></span>
<span data-ttu-id="b6169-148">Merhaba SimpleShortestPathsComputation örnek toodemonstrate hello basic kullanırız <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> hello en kısa yolu bir grafik nesneler arasındaki bulmak için uygulama.</span><span class="sxs-lookup"><span data-stu-id="b6169-148">We use hello SimpleShortestPathsComputation example toodemonstrate hello basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implementation for finding hello shortest path between objects in a graph.</span></span> <span data-ttu-id="b6169-149">Merhaba SimpleShortestPathsComputation örneği ve görünüm hello sonuçları kullanarak bir iş çalıştırmak adımları tooupload hello örnek veriler ve hello örnek jar, aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="b6169-149">Use hello following steps tooupload hello sample data and hello sample jar, run a job by using hello SimpleShortestPathsComputation example, and then view hello results.</span></span>

1. <span data-ttu-id="b6169-150">Örnek veri dosyası tooAzure Blob storage'ı yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b6169-150">Upload a sample data file tooAzure Blob storage.</span></span> <span data-ttu-id="b6169-151">Yerel iş istasyonunda, adlı yeni bir dosya oluşturun **tiny_graph.txt**.</span><span class="sxs-lookup"><span data-stu-id="b6169-151">On your local workstation, create a new file named **tiny_graph.txt**.</span></span> <span data-ttu-id="b6169-152">Satırlardan hello içermelidir:</span><span class="sxs-lookup"><span data-stu-id="b6169-152">It should contain hello following lines:</span></span>

        [0,0,[[1,1],[3,3]]]
        [1,0,[[0,1],[2,2],[3,1]]]
        [2,0,[[1,2],[4,4]]]
        [3,0,[[0,3],[1,1],[4,4]]]
        [4,0,[[3,4],[2,4]]]

    <span data-ttu-id="b6169-153">Merhaba tiny_graph.txt dosya toohello birincil depolama Hdınsight kümenizin karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="b6169-153">Upload hello tiny_graph.txt file toohello primary storage for your HDInsight cluster.</span></span> <span data-ttu-id="b6169-154">Yönergeler için tooupload verileri, görmek [hdınsight'ta Hadoop işleri için verileri karşıya yükleme](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="b6169-154">For instructions on how tooupload data, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    <span data-ttu-id="b6169-155">Bu veri hello biçimi kullanarak bir yönlendirilmiş grafik nesneler arasındaki ilişkiyi tanımlayan [kaynak\_kimliği, kaynak\_değeri [[hedef\_kimliği], [Kenar\_değer],...]]. Her satır arasındaki bir ilişkiyi temsil eder bir **kaynak\_kimliği** nesne ve bir veya daha fazla **taşınmaya\_kimliği** nesneleri.</span><span class="sxs-lookup"><span data-stu-id="b6169-155">This data describes a relationship between objects in a directed graph, by using hello format [source\_id, source\_value,[[dest\_id], [edge\_value],...]]. Each line represents a relationship between a **source\_id** object and one or more **dest\_id** objects.</span></span> <span data-ttu-id="b6169-156">Merhaba **kenar\_değeri** (veya ağırlık), hello gücü veya hello bağlantı uzaklığı olarak düşünülebilir **source_id** ve **taşınmaya\_kimliği**.</span><span class="sxs-lookup"><span data-stu-id="b6169-156">hello **edge\_value** (or weight) can be thought of as hello strength or distance of hello connection between **source_id** and **dest\_id**.</span></span>

    <span data-ttu-id="b6169-157">Çıkış çizilmiş ve nesneleri arasındaki hello uzaklığı olarak hello değeri (veya ağırlık) kullanarak, verileri yukarıda hello şuna benzeyebilir:</span><span class="sxs-lookup"><span data-stu-id="b6169-157">Drawn out, and using hello value (or weight) as hello distance between objects, hello above data might look like this:</span></span>

    ![Daireler arasında değişen uzaklığı satır olarak çizilen tiny_graph.txt](./media/hdinsight-hadoop-giraph-install/giraph-graph.png)
2. <span data-ttu-id="b6169-159">Merhaba SimpleShortestPathsComputation örneği çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="b6169-159">Run hello SimpleShortestPathsComputation example.</span></span> <span data-ttu-id="b6169-160">Giriş olarak hello tiny_graph.txt dosyasını kullanarak aşağıdaki Azure PowerShell cmdlet'leri toorun hello örneğine hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="b6169-160">Use hello following Azure PowerShell cmdlets toorun hello example by using hello tiny_graph.txt file as input.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="b6169-161">Azure Service Manager kullanılarak HDInsight kaynaklarının yönetilmesi için Azure PowerShell desteği **kullanım dışı bırakılmış** ve 1 Ocak 2017 tarihinde kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="b6169-161">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="b6169-162">Azure Resource Manager ile çalışan hello adımları bu belgenin kullanımı hello yeni Hdınsight cmdlet'lerini.</span><span class="sxs-lookup"><span data-stu-id="b6169-162">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="b6169-163">Lütfen başlangıç adımları izleyin [yüklemek ve Azure PowerShell yapılandırma](/powershell/azureps-cmdlets-docs) tooinstall hello en son Azure PowerShell sürümü.</span><span class="sxs-lookup"><span data-stu-id="b6169-163">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="b6169-164">Komut dosyalarınız varsa bu gereksinimi toobe Azure Resource Manager ile çalışma toouse hello yeni cmdlet'leri değişiklik için bkz: [geçiş tooAzure Resource Manager tabanlı geliştirme araçları Hdınsight kümeleri için](hdinsight-hadoop-development-using-azure-resource-manager.md) daha fazla bilgi için.</span><span class="sxs-lookup"><span data-stu-id="b6169-164">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

    ```powershell
    $clusterName = "clustername"
    # Giraph examples jar
    $jarFile = "wasb:///example/jars/giraph-examples.jar"
    # Arguments for this job
    $jobArguments = "org.apache.giraph.examples.SimpleShortestPathsComputation",
                    "-ca", "mapred.job.tracker=headnodehost:9010",
                    "-vif", "org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat",
                    "-vip", "wasb:///example/data/tiny_graph.txt",
                    "-vof", "org.apache.giraph.io.formats.IdWithValueTextOutputFormat",
                    "-op",  "wasb:///example/output/shortestpaths",
                    "-w", "2"
    # Create hello definition
    $jobDefinition = New-AzureHDInsightMapReduceJobDefinition
        -JarFile $jarFile
        -ClassName "org.apache.giraph.GiraphRunner"
        -Arguments $jobArguments

    # Run hello job, write output toohello Azure PowerShell window
    $job = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $jobDefinition
    Write-Host "Wait for hello job toocomplete ..." -ForegroundColor Green
    Wait-AzureHDInsightJob -Job $job
    Write-Host "STDERR"
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardError
    Write-Host "Display hello standard output ..." -ForegroundColor Green
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardOutput
    ```

    <span data-ttu-id="b6169-165">Yukarıdaki örnek Hello yerine **clustername** Giraph yüklü olan Hdınsight kümenize hello adı.</span><span class="sxs-lookup"><span data-stu-id="b6169-165">In hello above example, replace **clustername** with hello name of your HDInsight cluster that has Giraph installed.</span></span>
3. <span data-ttu-id="b6169-166">Merhaba sonuçları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="b6169-166">View hello results.</span></span> <span data-ttu-id="b6169-167">Merhaba işi tamamlandıktan sonra hello sonuçları hello iki çıktı dosyalarında depolanır **wasb: / / / örnek/çıkış/shotestpaths** klasör.</span><span class="sxs-lookup"><span data-stu-id="b6169-167">Once hello job has finished, hello results will be stored in two output files in hello **wasb:///example/out/shotestpaths** folder.</span></span> <span data-ttu-id="b6169-168">Merhaba dosyaları çağrılır **bölümü m 00001** ve **bölümü m 00002**.</span><span class="sxs-lookup"><span data-stu-id="b6169-168">hello files are called **part-m-00001** and **part-m-00002**.</span></span> <span data-ttu-id="b6169-169">Aşağıdaki adımları toodownload ve görünüm hello çıktı hello gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="b6169-169">Perform hello following steps toodownload and view hello output:</span></span>

    ```powershell
    $subscriptionName = "<SubscriptionName>"       # Azure subscription name
    $storageAccountName = "<StorageAccountName>"   # Azure Storage account name
    $containerName = "<ContainerName>"             # Blob storage container name

    # Select hello current subscription
    Select-AzureSubscription $subscriptionName

    # Create hello Storage account context object
    $storageAccountKey = Get-AzureStorageKey $storageAccountName | %{ $_.Primary }
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Download hello job output toohello workstation
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00001 -Context $storageContext -Force
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00002 -Context $storageContext -Force
    ```

    <span data-ttu-id="b6169-170">Bu hello oluşturacak **çıkış/örnek/shortestpaths** dizin yapısını hello geçerli dizinde iş istasyonu ve indirme hello iki çıktı dosyaları toothat konumu.</span><span class="sxs-lookup"><span data-stu-id="b6169-170">This will create hello **example/output/shortestpaths** directory structure in hello current directory on your workstation, and download hello two output files toothat location.</span></span>

    <span data-ttu-id="b6169-171">Kullanım hello **kat** cmdlet toodisplay hello hello dosyaların içeriğini:</span><span class="sxs-lookup"><span data-stu-id="b6169-171">Use hello **Cat** cmdlet toodisplay hello contents of hello files:</span></span>

        Cat example/output/shortestpaths/part*

    <span data-ttu-id="b6169-172">Hello çıktı toohello aşağıdaki benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="b6169-172">hello output should appear similar toohello following:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="b6169-173">Merhaba SimpleShortestPathComputation örnek nesne kimliği 1 ile sabit kodlanmış toostart olan ve hello en kısa yolu tooother nesneleri bulun.</span><span class="sxs-lookup"><span data-stu-id="b6169-173">hello SimpleShortestPathComputation example is hard coded toostart with object ID 1 and find hello shortest path tooother objects.</span></span> <span data-ttu-id="b6169-174">Hello çıktı olarak okumanız gereken şekilde `destination_id distance`, uzaklığı hello değeri (veya ağırlık) seyahat hello kenarlarının nesne kimliği 1 ve hello hedef kimliği arasında olduğu</span><span class="sxs-lookup"><span data-stu-id="b6169-174">So hello output should be read as `destination_id distance`, where distance is hello value (or weight) of hello edges traveled between object ID 1 and hello target ID.</span></span>

    <span data-ttu-id="b6169-175">Bu görselleştirme, hello kısa yolları kimliği 1 ile tüm diğer nesnelerin arasında seyahat hello sonuçları doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b6169-175">Visualizing this, you can verify hello results by traveling hello shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="b6169-176">Kimliği 1 ve kimliği 4 arasındaki en kısa yolu hello Not 5'tir.</span><span class="sxs-lookup"><span data-stu-id="b6169-176">Note that hello shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="b6169-177">Merhaba toplam aralıklarını budur <span style="color:orange">kimliği 1 ve 3</span>ve ardından <span style="color:red">kimliği 3 ve 4</span>.</span><span class="sxs-lookup"><span data-stu-id="b6169-177">This is hello total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Nesnelerin arasında çizilmiş kısa yolları daireler olarak çizme](./media/hdinsight-hadoop-giraph-install/giraph-graph-out.png)

## <a name="install-giraph-using-aure-powershell"></a><span data-ttu-id="b6169-179">Giraph işlemleri PowerShell kullanarak yükleme</span><span class="sxs-lookup"><span data-stu-id="b6169-179">Install Giraph using Aure PowerShell</span></span>
<span data-ttu-id="b6169-180">Bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="b6169-180">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="b6169-181">Merhaba örnek gösterilmektedir nasıl tooinstall Azure PowerShell kullanarak Spark.</span><span class="sxs-lookup"><span data-stu-id="b6169-181">hello sample demonstrates how tooinstall Spark using Azure PowerShell.</span></span> <span data-ttu-id="b6169-182">Toocustomize hello betik toouse gerek [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="b6169-182">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="install-giraph-using-net-sdk"></a><span data-ttu-id="b6169-183">.NET SDK kullanarak Giraph yükleyin</span><span class="sxs-lookup"><span data-stu-id="b6169-183">Install Giraph using .NET SDK</span></span>
<span data-ttu-id="b6169-184">Bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="b6169-184">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="b6169-185">Merhaba örnek gösterilmektedir nasıl tooinstall Spark hello .NET SDK kullanarak.</span><span class="sxs-lookup"><span data-stu-id="b6169-185">hello sample demonstrates how tooinstall Spark using hello .NET SDK.</span></span> <span data-ttu-id="b6169-186">Toocustomize hello betik toouse gerek [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="b6169-186">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="b6169-187">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="b6169-187">See also</span></span>
* [<span data-ttu-id="b6169-188">Giraph Hdınsight Hadoop kümeleri (Linux) yükleyin</span><span class="sxs-lookup"><span data-stu-id="b6169-188">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="b6169-189">[Hdınsight'ta Hadoop kümeleri oluşturma](hdinsight-provision-clusters.md): Hdınsight kümeleri oluşturma hakkında genel bilgi.</span><span class="sxs-lookup"><span data-stu-id="b6169-189">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="b6169-190">[Betik eylemi kullanarak Hdınsight kümesi özelleştirme][hdinsight-cluster-customize]: betik eylemi kullanarak Hdınsight kümelerini özelleştirme hakkında genel bilgi.</span><span class="sxs-lookup"><span data-stu-id="b6169-190">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="b6169-191">[Hdınsight için betik eylemi betikleri geliştirme](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="b6169-191">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="b6169-192">[Yükleme ve Spark Hdınsight kümelerinde kullanma][hdinsight-install-spark]: Spark yükleme hakkında örnek betik eylemi.</span><span class="sxs-lookup"><span data-stu-id="b6169-192">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="b6169-193">[Hdınsight kümelerinde R yüklemek][hdinsight-install-r]: betik eylemi örnek r yükleme hakkında</span><span class="sxs-lookup"><span data-stu-id="b6169-193">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="b6169-194">[Hdınsight kümelerinde Solr yükleme](hdinsight-hadoop-solr-install.md): Solr yükleme hakkında örnek betik eylemi.</span><span class="sxs-lookup"><span data-stu-id="b6169-194">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md): Script Action sample about installing Solr.</span></span>

[tools]: https://github.com/Blackmist/hdinsight-tools
[aps]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
