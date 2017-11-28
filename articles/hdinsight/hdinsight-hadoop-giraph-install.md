---
title: "Yükleme ve hdınsight'ta - Azure Hadoop kümeleri üzerinde Giraph kullanma | Microsoft Docs"
description: "Giraph Hdınsight kümesiyle özelleştirmeyi ve Giraph kullanmayı öğrenin."
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
ms.openlocfilehash: f0eb5c1f457380600463a370043f03e6d655a02c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="install-and-use-giraph-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="7a684-103">Yükleme ve Windows tabanlı Hdınsight kümelerinde Giraph kullanma</span><span class="sxs-lookup"><span data-stu-id="7a684-103">Install and use Giraph on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="7a684-104">Windows tabanlı Hdınsight kümesi ile betik eylemi kullanarak Giraph özelleştirmeyi ve Giraph büyük ölçekli grafikleri işlemek için nasıl kullanılacağını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="7a684-104">Learn how to customize Windows based HDInsight cluster with Giraph using Script Action, and how to use Giraph to process large-scale graphs.</span></span> <span data-ttu-id="7a684-105">Linux tabanlı bir kümeyle Giraph kullanma hakkında daha fazla bilgi için bkz: [yükleme Giraph Hdınsight Hadoop kümeleri (Linux) üzerinde](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="7a684-105">For information on using Giraph with a Linux-based cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7a684-106">Bu belgede yer alan adımlar, yalnızca Windows tabanlı Hdınsight kümeleri ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="7a684-106">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="7a684-107">Hdınsight yalnızca Windows'da Hdınsight 3.4 ' düşük sürümleri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7a684-107">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="7a684-108">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="7a684-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7a684-109">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="7a684-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="7a684-110">Linux tabanlı Hdınsight kümesinde Giraph yükleme hakkında daha fazla bilgi için bkz: [yükleme Giraph Hdınsight Hadoop kümeleri (Linux) üzerinde](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="7a684-110">For information on how to install Giraph on a Linux-based HDInsight cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>


<span data-ttu-id="7a684-111">Kullanarak Azure Hdınsight (Hadoop, Storm, HBase, Spark) kümede herhangi bir türde üzerinde Giraph yükleyebilirsiniz *betik eylemi*.</span><span class="sxs-lookup"><span data-stu-id="7a684-111">You can install Giraph on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="7a684-112">Giraph bir Hdınsight kümesine yüklemek için örnek komut dosyası salt okunur Azure depolama blobunu gelen kullanılabilir [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="7a684-112">A sample script to install Giraph on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span> <span data-ttu-id="7a684-113">Örnek komut dosyası yalnızca Hdınsight küme sürümü ile 3.1 çalışır.</span><span class="sxs-lookup"><span data-stu-id="7a684-113">The sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="7a684-114">Hdınsight küme sürümleri hakkında daha fazla bilgi için bkz: [Hdınsight küme sürümleri](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="7a684-114">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="7a684-115">**İlgili makaleler**</span><span class="sxs-lookup"><span data-stu-id="7a684-115">**Related articles**</span></span>

* [<span data-ttu-id="7a684-116">Giraph Hdınsight Hadoop kümeleri (Linux) yükleyin</span><span class="sxs-lookup"><span data-stu-id="7a684-116">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="7a684-117">[Hdınsight'ta Hadoop kümeleri oluşturma](hdinsight-provision-clusters.md): Hdınsight kümeleri oluşturma hakkında genel bilgi.</span><span class="sxs-lookup"><span data-stu-id="7a684-117">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="7a684-118">[Betik eylemi kullanarak Hdınsight kümesi özelleştirme][hdinsight-cluster-customize]: betik eylemi kullanarak Hdınsight kümelerini özelleştirme hakkında genel bilgi.</span><span class="sxs-lookup"><span data-stu-id="7a684-118">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="7a684-119">[Hdınsight için betik eylemi betikleri geliştirme](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="7a684-119">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-giraph"></a><span data-ttu-id="7a684-120">Giraph nedir?</span><span class="sxs-lookup"><span data-stu-id="7a684-120">What is Giraph?</span></span>
<span data-ttu-id="7a684-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> Hadoop kullanarak işleme grafik işlemleri yapmanıza olanak tanır ve Azure Hdınsight ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7a684-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="7a684-122">Grafikler Internet gibi büyük bir ağdaki yönlendiricileri veya (bazen bir sosyal grafik adlandırılır) sosyal ağlar üzerindeki kişiler arasındaki ilişkileri arasındaki bağlantıları gibi nesneler arasındaki ilişkileri model.</span><span class="sxs-lookup"><span data-stu-id="7a684-122">Graphs model relationships between objects, such as the connections between routers on a large network like the Internet, or relationships between people on social networks (sometimes referred to as a social graph).</span></span> <span data-ttu-id="7a684-123">Grafik işleme nedeni bir grafik nesneleri arasındaki ilişkiler hakkında gibi sağlar:</span><span class="sxs-lookup"><span data-stu-id="7a684-123">Graph processing allows you to reason about the relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="7a684-124">Geçerli ilişkilere dayanan olası arkadaş tanımlama.</span><span class="sxs-lookup"><span data-stu-id="7a684-124">Identifying potential friends based on your current relationships.</span></span>
* <span data-ttu-id="7a684-125">Bir ağda iki bilgisayar arasındaki en kısa yolu tanımlama.</span><span class="sxs-lookup"><span data-stu-id="7a684-125">Identifying the shortest route between two computers in a network.</span></span>
* <span data-ttu-id="7a684-126">Web sayfalarındaki sayfa derecesini hesaplama.</span><span class="sxs-lookup"><span data-stu-id="7a684-126">Calculating the page rank of webpages.</span></span>

## <a name="install-giraph-using-portal"></a><span data-ttu-id="7a684-127">Portal kullanarak Giraph yükleyin</span><span class="sxs-lookup"><span data-stu-id="7a684-127">Install Giraph using portal</span></span>
1. <span data-ttu-id="7a684-128">Kullanarak bir küme oluşturmaya başlamak **özel Oluştur** konusunda açıklandığı gibi seçeneği [Hdınsight'ta oluşturmak Hadoop kümeleri](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="7a684-128">Start creating a cluster by using the **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="7a684-129">Üzerinde **betik eylemleri** Sayfa Sihirbazı'nın tıklatın **betik eylemi eklemek** aşağıda gösterildiği gibi betik eylemi hakkındaki ayrıntıları sağlamak için:</span><span class="sxs-lookup"><span data-stu-id="7a684-129">On the **Script Actions** page of the wizard, click **add script action** to provide details about the script action, as shown below:</span></span>

    <span data-ttu-id="7a684-130">![Bir küme özelleştirmek için betik eylemi kullanın](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "bir küme özelleştirmek için kullanım betik eylemi")</span><span class="sxs-lookup"><span data-stu-id="7a684-130">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="7a684-131">Özellik</span><span class="sxs-lookup"><span data-stu-id="7a684-131">Property</span></span></th><th><span data-ttu-id="7a684-132">Değer</span><span class="sxs-lookup"><span data-stu-id="7a684-132">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="7a684-133">Ad</span><span class="sxs-lookup"><span data-stu-id="7a684-133">Name</span></span></td>
            <td><span data-ttu-id="7a684-134">Betik eylemi için bir ad belirtin.</span><span class="sxs-lookup"><span data-stu-id="7a684-134">Specify a name for the script action.</span></span> <span data-ttu-id="7a684-135">Örneğin, <b>yükleme Giraph</b>.</span><span class="sxs-lookup"><span data-stu-id="7a684-135">For example, <b>Install Giraph</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="7a684-136">Betik URI'si</span><span class="sxs-lookup"><span data-stu-id="7a684-136">Script URI</span></span></td>
            <td><span data-ttu-id="7a684-137">Küme özelleştirmek için çağrılan betik Tekdüzen Kaynak Tanımlayıcısı (URI) belirtin.</span><span class="sxs-lookup"><span data-stu-id="7a684-137">Specify the Uniform Resource Identifier (URI) to the script that is invoked to customize the cluster.</span></span> <span data-ttu-id="7a684-138">Örneğin, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span><span class="sxs-lookup"><span data-stu-id="7a684-138">For example, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="7a684-139">Düğüm Türü</span><span class="sxs-lookup"><span data-stu-id="7a684-139">Node Type</span></span></td>
            <td><span data-ttu-id="7a684-140">Özelleştirme kodun çalıştığı düğüm belirtin.</span><span class="sxs-lookup"><span data-stu-id="7a684-140">Specify the nodes on which the customization script is run.</span></span> <span data-ttu-id="7a684-141">Seçebileceğiniz <b>tüm düğümleri</b>, <b>Head yalnızca düğümlerin</b>, veya <b>yalnızca çalışan düğümleri</b>.</span><span class="sxs-lookup"><span data-stu-id="7a684-141">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="7a684-142">Parametreler</span><span class="sxs-lookup"><span data-stu-id="7a684-142">Parameters</span></span></td>
            <td><span data-ttu-id="7a684-143">Komut dosyası tarafından gerekli parametreleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="7a684-143">Specify the parameters, if required by the script.</span></span> <span data-ttu-id="7a684-144">Bunu boş bırakabilirsiniz şekilde Giraph yüklemek için komut dosyası herhangi bir parametre gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="7a684-144">The script to install Giraph does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="7a684-145">Küme üzerinde birden çok bileşeni yüklemek için birden fazla betik eylemi ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a684-145">You can add more than one script action to install multiple components on the cluster.</span></span> <span data-ttu-id="7a684-146">Komut dosyaları ekledikten sonra küme oluşturmaya başlamak için onay işaretine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7a684-146">After you have added the scripts, click the checkmark to start creating the cluster.</span></span>

## <a name="use-giraph"></a><span data-ttu-id="7a684-147">Giraph kullanma</span><span class="sxs-lookup"><span data-stu-id="7a684-147">Use Giraph</span></span>
<span data-ttu-id="7a684-148">Temel göstermek için SimpleShortestPathsComputation örnek kullanırız <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> bir grafik nesneler arasındaki en kısa yolu bulmak için uygulama.</span><span class="sxs-lookup"><span data-stu-id="7a684-148">We use the SimpleShortestPathsComputation example to demonstrate the basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implementation for finding the shortest path between objects in a graph.</span></span> <span data-ttu-id="7a684-149">Örnek verileri ve örnek jar karşıya yükleyin, SimpleShortestPathsComputation örnek kullanarak bir iş çalıştırmak için aşağıdaki adımları kullanın ve sonra sonuçları görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="7a684-149">Use the following steps to upload the sample data and the sample jar, run a job by using the SimpleShortestPathsComputation example, and then view the results.</span></span>

1. <span data-ttu-id="7a684-150">Azure Blob depolama alanına örnek veri dosyasını karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="7a684-150">Upload a sample data file to Azure Blob storage.</span></span> <span data-ttu-id="7a684-151">Yerel iş istasyonunda, adlı yeni bir dosya oluşturun **tiny_graph.txt**.</span><span class="sxs-lookup"><span data-stu-id="7a684-151">On your local workstation, create a new file named **tiny_graph.txt**.</span></span> <span data-ttu-id="7a684-152">Aşağıdaki satırları içermelidir:</span><span class="sxs-lookup"><span data-stu-id="7a684-152">It should contain the following lines:</span></span>

        [0,0,[[1,1],[3,3]]]
        [1,0,[[0,1],[2,2],[3,1]]]
        [2,0,[[1,2],[4,4]]]
        [3,0,[[0,3],[1,1],[4,4]]]
        [4,0,[[3,4],[2,4]]]

    <span data-ttu-id="7a684-153">Hdınsight kümeniz için birincil depolama tiny_graph.txt dosyası yükleyin.</span><span class="sxs-lookup"><span data-stu-id="7a684-153">Upload the tiny_graph.txt file to the primary storage for your HDInsight cluster.</span></span> <span data-ttu-id="7a684-154">Veri yükleme hakkında daha fazla yönerge için bkz: [hdınsight'ta Hadoop işleri için verileri karşıya yükleme](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="7a684-154">For instructions on how to upload data, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    <span data-ttu-id="7a684-155">Bu veri biçimi kullanarak bir yönlendirilmiş grafik nesneler arasındaki ilişkiyi tanımlayan [kaynak\_kimliği, kaynak\_değeri [[hedef\_kimliği], [Kenar\_değer],...]].</span><span class="sxs-lookup"><span data-stu-id="7a684-155">This data describes a relationship between objects in a directed graph, by using the format [source\_id, source\_value,[[dest\_id], [edge\_value],...]].</span></span> <span data-ttu-id="7a684-156">Her satır arasındaki bir ilişkiyi temsil eder bir **kaynak\_kimliği** nesne ve bir veya daha fazla **taşınmaya\_kimliği** nesneleri.</span><span class="sxs-lookup"><span data-stu-id="7a684-156">Each line represents a relationship between a **source\_id** object and one or more **dest\_id** objects.</span></span> <span data-ttu-id="7a684-157">**Kenar\_değeri** (veya ağırlık), gücü veya arasındaki bağlantıyı uzaklığını olarak düşünülebilir **source_id** ve **taşınmaya\_kimliği**.</span><span class="sxs-lookup"><span data-stu-id="7a684-157">The **edge\_value** (or weight) can be thought of as the strength or distance of the connection between **source_id** and **dest\_id**.</span></span>

    <span data-ttu-id="7a684-158">Çıkış çizilmiş ve nesneleri arasındaki uzaklığı olarak değeri (veya ağırlık) kullanarak, yukarıdaki verileri şuna benzeyebilir:</span><span class="sxs-lookup"><span data-stu-id="7a684-158">Drawn out, and using the value (or weight) as the distance between objects, the above data might look like this:</span></span>

    ![Daireler arasında değişen uzaklığı satır olarak çizilen tiny_graph.txt](./media/hdinsight-hadoop-giraph-install/giraph-graph.png)
2. <span data-ttu-id="7a684-160">SimpleShortestPathsComputation örneği çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="7a684-160">Run the SimpleShortestPathsComputation example.</span></span> <span data-ttu-id="7a684-161">Örnek giriş olarak tiny_graph.txt dosyasını kullanarak çalıştırmak için aşağıdaki Azure PowerShell cmdlet'lerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="7a684-161">Use the following Azure PowerShell cmdlets to run the example by using the tiny_graph.txt file as input.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="7a684-162">Azure Service Manager kullanılarak HDInsight kaynaklarının yönetilmesi için Azure PowerShell desteği **kullanım dışı bırakılmış** ve 1 Ocak 2017 tarihinde kaldırılmıştır.</span><span class="sxs-lookup"><span data-stu-id="7a684-162">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="7a684-163">Bu belgede yer alan adımlar, Azure Resource Manager ile çalışan yeni HDInsight cmdlet'lerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="7a684-163">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="7a684-164">Azure PowerShell’in en son sürümünü yüklemek için lütfen [Azure PowerShell’i yükleme ve yapılandırma](/powershell/azureps-cmdlets-docs)’daki adımları uygulayın.</span><span class="sxs-lookup"><span data-stu-id="7a684-164">Please follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="7a684-165">Azure Resource Manager’la çalışan yeni cmdlet’lerle kullanmak için değiştirilmesi gereken komut dosyalarınız varsa, daha fazla bilgi için bkz. [HDInsight kümeleri için Azure Resource Manager tabanlı geliştirme araçlarına geçme](hdinsight-hadoop-development-using-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="7a684-165">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

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
    # Create the definition
    $jobDefinition = New-AzureHDInsightMapReduceJobDefinition
        -JarFile $jarFile
        -ClassName "org.apache.giraph.GiraphRunner"
        -Arguments $jobArguments

    # Run the job, write output to the Azure PowerShell window
    $job = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $jobDefinition
    Write-Host "Wait for the job to complete ..." -ForegroundColor Green
    Wait-AzureHDInsightJob -Job $job
    Write-Host "STDERR"
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardError
    Write-Host "Display the standard output ..." -ForegroundColor Green
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardOutput
    ```

    <span data-ttu-id="7a684-166">Yukarıdaki örnekte **clustername** Giraph yüklü olan Hdınsight kümenizin adıyla.</span><span class="sxs-lookup"><span data-stu-id="7a684-166">In the above example, replace **clustername** with the name of your HDInsight cluster that has Giraph installed.</span></span>
3. <span data-ttu-id="7a684-167">Sonuçlara bakın.</span><span class="sxs-lookup"><span data-stu-id="7a684-167">View the results.</span></span> <span data-ttu-id="7a684-168">İş tamamlandıktan sonra sonuçları iki çıktı dosyalarında depolanır **wasb: / / / örnek/çıkış/shotestpaths** klasör.</span><span class="sxs-lookup"><span data-stu-id="7a684-168">Once the job has finished, the results will be stored in two output files in the **wasb:///example/out/shotestpaths** folder.</span></span> <span data-ttu-id="7a684-169">Dosya adında **bölümü m 00001** ve **bölümü m 00002**.</span><span class="sxs-lookup"><span data-stu-id="7a684-169">The files are called **part-m-00001** and **part-m-00002**.</span></span> <span data-ttu-id="7a684-170">Karşıdan yükle ve çıktı görüntülemek için aşağıdaki adımları gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="7a684-170">Perform the following steps to download and view the output:</span></span>

    ```powershell
    $subscriptionName = "<SubscriptionName>"       # Azure subscription name
    $storageAccountName = "<StorageAccountName>"   # Azure Storage account name
    $containerName = "<ContainerName>"             # Blob storage container name

    # Select the current subscription
    Select-AzureSubscription $subscriptionName

    # Create the Storage account context object
    $storageAccountKey = Get-AzureStorageKey $storageAccountName | %{ $_.Primary }
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Download the job output to the workstation
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00001 -Context $storageContext -Force
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00002 -Context $storageContext -Force
    ```

    <span data-ttu-id="7a684-171">Bu oluşturacak **çıkış/örnek/shortestpaths** geçerli dizinde iş istasyonu ve bu konuma çıktı dosyaları indirme iki dizin yapısı.</span><span class="sxs-lookup"><span data-stu-id="7a684-171">This will create the **example/output/shortestpaths** directory structure in the current directory on your workstation, and download the two output files to that location.</span></span>

    <span data-ttu-id="7a684-172">Kullanım **kat** cmdlet dosyaların içeriğini görüntülemek için:</span><span class="sxs-lookup"><span data-stu-id="7a684-172">Use the **Cat** cmdlet to display the contents of the files:</span></span>

        Cat example/output/shortestpaths/part*

    <span data-ttu-id="7a684-173">Çıktı aşağıdakine benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="7a684-173">The output should appear similar to the following:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="7a684-174">Örnek başlamak kodlanmış sabit SimpleShortestPathComputation kimliği 1 nesne ve diğer nesnelere en kısa yolu bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="7a684-174">The SimpleShortestPathComputation example is hard coded to start with object ID 1 and find the shortest path to other objects.</span></span> <span data-ttu-id="7a684-175">Çıktı olarak okumanız gereken şekilde `destination_id distance`, burada uzaklığı nesne kimliği 1 ve hedef kimliği arasında seyahat kenarları değeri (veya ağırlık).</span><span class="sxs-lookup"><span data-stu-id="7a684-175">So the output should be read as `destination_id distance`, where distance is the value (or weight) of the edges traveled between object ID 1 and the target ID.</span></span>

    <span data-ttu-id="7a684-176">Bu görselleştirme, kısa yolları kimliği 1 ile tüm diğer nesnelerin arasında seyahat sonuçları doğrulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a684-176">Visualizing this, you can verify the results by traveling the shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="7a684-177">Kimliği 1 ve kimliği 4 arasındaki en kısa yolu 5 olduğuna dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="7a684-177">Note that the shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="7a684-178">Arasındaki toplam uzaklığı budur <span style="color:orange">kimliği 1 ve 3</span>ve ardından <span style="color:red">kimliği 3 ve 4</span>.</span><span class="sxs-lookup"><span data-stu-id="7a684-178">This is the total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Nesnelerin arasında çizilmiş kısa yolları daireler olarak çizme](./media/hdinsight-hadoop-giraph-install/giraph-graph-out.png)

## <a name="install-giraph-using-aure-powershell"></a><span data-ttu-id="7a684-180">Giraph işlemleri PowerShell kullanarak yükleme</span><span class="sxs-lookup"><span data-stu-id="7a684-180">Install Giraph using Aure PowerShell</span></span>
<span data-ttu-id="7a684-181">Bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="7a684-181">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="7a684-182">Örnek, Azure PowerShell kullanarak Spark yükleneceği gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="7a684-182">The sample demonstrates how to install Spark using Azure PowerShell.</span></span> <span data-ttu-id="7a684-183">Kullanılacak komut dosyasını özelleştirmeniz gerekiyorsa [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="7a684-183">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="install-giraph-using-net-sdk"></a><span data-ttu-id="7a684-184">.NET SDK kullanarak Giraph yükleyin</span><span class="sxs-lookup"><span data-stu-id="7a684-184">Install Giraph using .NET SDK</span></span>
<span data-ttu-id="7a684-185">Bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="7a684-185">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="7a684-186">Örnek, .NET SDK kullanarak Spark yükleneceği gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="7a684-186">The sample demonstrates how to install Spark using the .NET SDK.</span></span> <span data-ttu-id="7a684-187">Kullanılacak komut dosyasını özelleştirmeniz gerekiyorsa [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="7a684-187">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="7a684-188">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="7a684-188">See also</span></span>
* [<span data-ttu-id="7a684-189">Giraph Hdınsight Hadoop kümeleri (Linux) yükleyin</span><span class="sxs-lookup"><span data-stu-id="7a684-189">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="7a684-190">[Hdınsight'ta Hadoop kümeleri oluşturma](hdinsight-provision-clusters.md): Hdınsight kümeleri oluşturma hakkında genel bilgi.</span><span class="sxs-lookup"><span data-stu-id="7a684-190">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="7a684-191">[Betik eylemi kullanarak Hdınsight kümesi özelleştirme][hdinsight-cluster-customize]: betik eylemi kullanarak Hdınsight kümelerini özelleştirme hakkında genel bilgi.</span><span class="sxs-lookup"><span data-stu-id="7a684-191">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="7a684-192">[Hdınsight için betik eylemi betikleri geliştirme](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="7a684-192">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="7a684-193">[Yükleme ve Spark Hdınsight kümelerinde kullanma][hdinsight-install-spark]: Spark yükleme hakkında örnek betik eylemi.</span><span class="sxs-lookup"><span data-stu-id="7a684-193">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="7a684-194">[Hdınsight kümelerinde R yüklemek][hdinsight-install-r]: betik eylemi örnek r yükleme hakkında</span><span class="sxs-lookup"><span data-stu-id="7a684-194">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="7a684-195">[Hdınsight kümelerinde Solr yükleme](hdinsight-hadoop-solr-install.md): Solr yükleme hakkında örnek betik eylemi.</span><span class="sxs-lookup"><span data-stu-id="7a684-195">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md): Script Action sample about installing Solr.</span></span>

[tools]: https://github.com/Blackmist/hdinsight-tools
[aps]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
