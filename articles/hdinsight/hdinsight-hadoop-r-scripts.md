---
title: "Hdınsight kümeleri - Azure özelleştirmek için R kullanımda | Microsoft Docs"
description: "Betik eylemi kullanarak R yüklemeyi öğrenin ve Hdınsight kümelerinde R kullanın."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: be851270-afa5-4af0-a69e-2d343a4deeb7
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 5b9b793d49217acd9f0c6c518596a7afb5600d69
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="install-and-use-r-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="8be44-103">HDInsight'taki Hadoop kümelerinde R programını yükleme ve kullanma</span><span class="sxs-lookup"><span data-stu-id="8be44-103">Install and use R on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="8be44-104">Windows özelleştirmek nasıl Hdınsight kümesi ile betik eylemi kullanarak R dayalı ve kümeleri Hdınsight'ta R kullanmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="8be44-104">Learn how to customize Windows based HDInsight cluster with R using Script Action, and how to use R on HDInsight clusters.</span></span> <span data-ttu-id="8be44-105">[Hdınsight teklifi](https://azure.microsoft.com/pricing/details/hdinsight/) R Server Hdınsight kümenize bir parçası olarak içerir.</span><span class="sxs-lookup"><span data-stu-id="8be44-105">The [HDInsight offering](https://azure.microsoft.com/pricing/details/hdinsight/) includes R Server as part of your HDInsight cluster.</span></span> <span data-ttu-id="8be44-106">Bu, MapReduce ve Spark dağıtılmış hesaplamaları çalıştırmak R betiklerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="8be44-106">This allows R scripts to use MapReduce and Spark to run distributed computations.</span></span> <span data-ttu-id="8be44-107">Daha fazla bilgi için bkz. [HDInsight R Server kullanmaya başlama](hdinsight-hadoop-r-server-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8be44-107">For more information, see [Get started using R Server on HDInsight](hdinsight-hadoop-r-server-get-started.md).</span></span> <span data-ttu-id="8be44-108">Linux tabanlı bir kümeyle R kullanma hakkında daha fazla bilgi için bkz: [yükleme ve kullanma R Hdınsight Hadoop kümeleri (Linux) üzerinde](hdinsight-hadoop-r-scripts-linux.md).</span><span class="sxs-lookup"><span data-stu-id="8be44-108">For information on using R with a Linux-based cluster, see [Install and use R on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-r-scripts-linux.md).</span></span>

<span data-ttu-id="8be44-109">Kullanarak Azure Hdınsight (Hadoop, Storm, HBase, Spark) kümede herhangi bir türde üzerinde R yükleyebilirsiniz *betik eylemi*.</span><span class="sxs-lookup"><span data-stu-id="8be44-109">You can install R on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="8be44-110">R bir Hdınsight kümesine yüklemek için örnek komut dosyası salt okunur Azure depolama blobunu gelen kullanılabilir [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span><span class="sxs-lookup"><span data-stu-id="8be44-110">A sample script to install R on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span></span>

<span data-ttu-id="8be44-111">**İlgili makaleler**</span><span class="sxs-lookup"><span data-stu-id="8be44-111">**Related articles**</span></span>

* [<span data-ttu-id="8be44-112">Yükleme ve Hdınsight Hadoop kümeleri (Linux) R kullanma</span><span class="sxs-lookup"><span data-stu-id="8be44-112">Install and use R on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-r-scripts-linux.md)
* <span data-ttu-id="8be44-113">[Hdınsight'ta Hadoop kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md): Hdınsight kümeleri oluşturma hakkında genel bilgiler</span><span class="sxs-lookup"><span data-stu-id="8be44-113">[Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): general information on creating HDInsight clusters</span></span>
* <span data-ttu-id="8be44-114">[Betik eylemi kullanarak Hdınsight kümesi özelleştirme][hdinsight-cluster-customize]: betik eylemi kullanarak Hdınsight kümelerini özelleştirme hakkında genel bilgiler</span><span class="sxs-lookup"><span data-stu-id="8be44-114">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action</span></span>
* [<span data-ttu-id="8be44-115">Hdınsight için betik eylemi betikleri geliştirme</span><span class="sxs-lookup"><span data-stu-id="8be44-115">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions.md)

## <a name="what-is-r"></a><span data-ttu-id="8be44-116">R nedir?</span><span class="sxs-lookup"><span data-stu-id="8be44-116">What is R?</span></span>
<span data-ttu-id="8be44-117"><a href="http://www.r-project.org/" target="_blank">R proje istatistiksel bilgi işlem için</a> bir açık kaynak dili ve istatistiksel bilgi işlem ortamı.</span><span class="sxs-lookup"><span data-stu-id="8be44-117">The <a href="http://www.r-project.org/" target="_blank">R Project for Statistical Computing</a> is an open source language and environment for statistical computing.</span></span> <span data-ttu-id="8be44-118">R yüzlerce yapı içinde istatistik işlevleri ve işlev ve nesne odaklı programlama yönlerini birleştirir kendi programlama dili sağlar.</span><span class="sxs-lookup"><span data-stu-id="8be44-118">R provides hundreds of build-in statistical functions and its own programming language that combines aspects of functional and object-oriented programming.</span></span> <span data-ttu-id="8be44-119">Yoğun grafik yetenekleri de sağlar.</span><span class="sxs-lookup"><span data-stu-id="8be44-119">It also provides extensive graphical capabilities.</span></span> <span data-ttu-id="8be44-120">R en profesyonel istatistikçiler ve çeşitli alanları bilimcilerine için tercih edilen programlama ortamıdır.</span><span class="sxs-lookup"><span data-stu-id="8be44-120">R is the preferred programming environment for most professional statisticians and scientists in a wide variety of fields.</span></span>

<span data-ttu-id="8be44-121">R Azure Blob Storage (WASB) ile uyumlu, böylelikle var. depolanan verileri R kullanarak işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="8be44-121">R is compatible with Azure Blob Storage (WASB) so that data that is stored there can be processed using R on HDInsight.</span></span>  

## <a name="install-r"></a><span data-ttu-id="8be44-122">R yükleme</span><span class="sxs-lookup"><span data-stu-id="8be44-122">Install R</span></span>
<span data-ttu-id="8be44-123">A [örnek komut dosyası](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) bir Hdınsight'ta R yüklemek için küme salt okunur bir blob Azure depolama alanında kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="8be44-123">A [sample script](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) to install R on an HDInsight cluster is available from a read-only blob in Azure Storage.</span></span> <span data-ttu-id="8be44-124">Bu bölümde Azure Portalı'nı kullanarak küme oluşturulurken örnek betiği kullanmak hakkında yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="8be44-124">This section provides instructions about how to use the sample script while creating the cluster using the Azure Portal.</span></span>

> [!NOTE]
> <span data-ttu-id="8be44-125">Örnek betiği Hdınsight kümesi sürüm 3.1 sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="8be44-125">The sample script was introduced with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="8be44-126">Hdınsight küme sürümleri hakkında daha fazla bilgi için bkz: [Hdınsight küme sürümleri](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="8be44-126">For more information about  HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>
>
>

1. <span data-ttu-id="8be44-127">Portaldan bir Hdınsight kümesi oluştururken tıklatın **isteğe bağlı yapılandırma**ve ardından **betik eylemleri**.</span><span class="sxs-lookup"><span data-stu-id="8be44-127">When you create an HDInsight cluster from the Portal, click **Optional Configuration**, and then click **Script Actions**.</span></span>
2. <span data-ttu-id="8be44-128">Üzerinde **betik eylemleri** sayfasında, aşağıdaki değerleri girin:</span><span class="sxs-lookup"><span data-stu-id="8be44-128">On the **Script Actions** page, enter the following values:</span></span>

    <span data-ttu-id="8be44-129">![Bir küme özelleştirmek için betik eylemi kullanın](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "bir küme özelleştirmek için kullanım betik eylemi")</span><span class="sxs-lookup"><span data-stu-id="8be44-129">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="8be44-130">Özellik</span><span class="sxs-lookup"><span data-stu-id="8be44-130">Property</span></span></th><th><span data-ttu-id="8be44-131">Değer</span><span class="sxs-lookup"><span data-stu-id="8be44-131">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="8be44-132">Ad</span><span class="sxs-lookup"><span data-stu-id="8be44-132">Name</span></span></td>
            <td><span data-ttu-id="8be44-133">Örneğin, betik eylemi için bir ad belirtmeniz <b>R yükleme</b>.</span><span class="sxs-lookup"><span data-stu-id="8be44-133">Specify a name for the script action, for example, <b>Install R</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="8be44-134">Betik URI'si</span><span class="sxs-lookup"><span data-stu-id="8be44-134">Script URI</span></span></td>
            <td><span data-ttu-id="8be44-135">Bu gibi bir durumda küme özelleştirmek için çağrılan betik URI'si belirtin <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></span><span class="sxs-lookup"><span data-stu-id="8be44-135">Specify the URI to the script that is invoked to customize the cluster, for example, <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="8be44-136">Düğüm Türü</span><span class="sxs-lookup"><span data-stu-id="8be44-136">Node Type</span></span></td>
            <td><span data-ttu-id="8be44-137">Özelleştirme kodun çalıştığı düğüm belirtin.</span><span class="sxs-lookup"><span data-stu-id="8be44-137">Specify the nodes on which the customization script is run.</span></span> <span data-ttu-id="8be44-138">Seçebileceğiniz <b>tüm düğümleri</b>, <b>Head yalnızca düğümlerin</b>, veya <b>çalışan düğümleri</b> yalnızca.</span><span class="sxs-lookup"><span data-stu-id="8be44-138">You can choose <b>All Nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes</b> only.</span></span>
        <tr><td><span data-ttu-id="8be44-139">Parametreler</span><span class="sxs-lookup"><span data-stu-id="8be44-139">Parameters</span></span></td>
            <td><span data-ttu-id="8be44-140">Komut dosyası tarafından gerekli parametreleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="8be44-140">Specify the parameters, if required by the script.</span></span> <span data-ttu-id="8be44-141">Ancak, bunu boş bırakabilirsiniz şekilde R yüklemek için komut dosyası herhangi bir parametre gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="8be44-141">However, the script to install R does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="8be44-142">Küme üzerinde birden çok bileşeni yüklemek için birden fazla betik eylemi ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8be44-142">You can add more than one script action to install multiple components on the cluster.</span></span> <span data-ttu-id="8be44-143">Komut dosyaları ekledikten sonra küme crating başlatmak için onay işaretine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8be44-143">After you have added the scripts, click the check mark to start crating the cluster.</span></span>

<span data-ttu-id="8be44-144">Komut dosyası, Azure PowerShell veya Hdınsight .NET SDK kullanarak Hdınsight'ta R yüklemek için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8be44-144">You can also use the script to install R on HDInsight by using Azure PowerShell or the HDInsight .NET SDK.</span></span> <span data-ttu-id="8be44-145">Bu yordamları için yönergeler bu makalenin sonraki bölümlerinde verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8be44-145">Instructions for these procedures are provided later in this article.</span></span>

## <a name="run-r-scripts"></a><span data-ttu-id="8be44-146">R betiği çalıştırın</span><span class="sxs-lookup"><span data-stu-id="8be44-146">Run R scripts</span></span>
<span data-ttu-id="8be44-147">Bu bölümde, Hdınsight ile Hadoop küme üzerinde bir R betiği çalıştırmak açıklar.</span><span class="sxs-lookup"><span data-stu-id="8be44-147">This section describes how to run an R script on the Hadoop cluster with HDInsight.</span></span>

1. <span data-ttu-id="8be44-148">**Küme için Uzak Masaüstü Bağlantısı**: gelen portalı yüklü R ile oluşturduğunuz küme için Uzak masaüstünü etkinleştir ve kümeye bağlanın.</span><span class="sxs-lookup"><span data-stu-id="8be44-148">**Establish a Remote Desktop connection to the cluster**: From the Portal, enable Remote Desktop for the cluster you created with R installed, and then connect to the cluster.</span></span> <span data-ttu-id="8be44-149">Yönergeler için bkz: [RDP kullanarak Hdınsight kümelerini Bağlan](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="8be44-149">For instructions, see [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>
2. <span data-ttu-id="8be44-150">**R Konsolu**: R yükleme baş düğüm masaüstünde R konsola bir bağlantı yerleştirir.</span><span class="sxs-lookup"><span data-stu-id="8be44-150">**Open the R console**: The R installation puts a link to the R console on the desktop of the head node.</span></span> <span data-ttu-id="8be44-151">R konsolunu açmak için tıklayın.</span><span class="sxs-lookup"><span data-stu-id="8be44-151">Click on it to open the R console.</span></span>
3. <span data-ttu-id="8be44-152">**R betiği Çalıştır**: R betiği, yapıştırma seçerek ve ENTER tuşuna basarak doğrudan R konsolundan çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="8be44-152">**Run the R script**: The R script can be run directly from the R console by pasting it, selecting it, and pressing ENTER.</span></span> <span data-ttu-id="8be44-153">Burada, 1 ile 100 arası sayılar oluşturur ve bunları 2 ile çarpar basit bir örnek komut verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8be44-153">Here is a simple example script that generates the numbers 1 to 100 and then multiplies them by 2.</span></span>

        library(rmr2)
        library(rhdfs)
        ints = to.dfs(1:100)
        calc = mapreduce(input = ints, map = function(k, v) cbind(v, 2*v))
        from.dfs(calc)

<span data-ttu-id="8be44-154">İlk iki satır ile r yüklü RHadoop kitaplıkları çağırın Son satırı sonuçlarını konsola yazdırır.</span><span class="sxs-lookup"><span data-stu-id="8be44-154">The first two lines call the RHadoop libraries that are installed with R. The final line prints the results to the console.</span></span> <span data-ttu-id="8be44-155">Çıktı aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="8be44-155">The output should look like this:</span></span>

    [1,]  1 2
    [2,]  2 4
    .
    .
    .
    [98,]  98 196
    [99,]  99 198
    [100,] 100 200


## <a name="install-r-using-aure-powershell"></a><span data-ttu-id="8be44-156">R işlemleri PowerShell kullanarak yükleme</span><span class="sxs-lookup"><span data-stu-id="8be44-156">Install R using Aure PowerShell</span></span>
<span data-ttu-id="8be44-157">Bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="8be44-157">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="8be44-158">Örnek, Azure PowerShell kullanarak Spark yükleneceği gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8be44-158">The sample demonstrates how to install Spark using Azure PowerShell.</span></span> <span data-ttu-id="8be44-159">Kullanılacak komut dosyasını özelleştirmeniz gerekiyorsa [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span><span class="sxs-lookup"><span data-stu-id="8be44-159">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span></span>

## <a name="install-r-using-net-sdk"></a><span data-ttu-id="8be44-160">.NET SDK kullanarak R yükleme</span><span class="sxs-lookup"><span data-stu-id="8be44-160">Install R using .NET SDK</span></span>
<span data-ttu-id="8be44-161">Bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="8be44-161">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="8be44-162">Örnek, .NET SDK kullanarak Spark yükleneceği gösterilmiştir.</span><span class="sxs-lookup"><span data-stu-id="8be44-162">The sample demonstrates how to install Spark using the .NET SDK.</span></span> <span data-ttu-id="8be44-163">Kullanılacak komut dosyasını özelleştirmeniz gerekiyorsa [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11).</span><span class="sxs-lookup"><span data-stu-id="8be44-163">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11).</span></span>

## <a name="see-also"></a><span data-ttu-id="8be44-164">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="8be44-164">See also</span></span>
* [<span data-ttu-id="8be44-165">Yükleme ve Hdınsight Hadoop kümeleri (Linux) R kullanma</span><span class="sxs-lookup"><span data-stu-id="8be44-165">Install and use R on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-r-scripts-linux.md)
* <span data-ttu-id="8be44-166">[Hdınsight'ta Hadoop kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md): Hdınsight kümeleri oluşturma hakkında genel bilgiler</span><span class="sxs-lookup"><span data-stu-id="8be44-166">[Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): general information on creating HDInsight clusters</span></span>
* <span data-ttu-id="8be44-167">[Betik eylemi kullanarak Hdınsight kümesi özelleştirme][hdinsight-cluster-customize]: betik eylemi kullanarak Hdınsight kümelerini özelleştirme hakkında genel bilgiler</span><span class="sxs-lookup"><span data-stu-id="8be44-167">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action</span></span>
* [<span data-ttu-id="8be44-168">Hdınsight için betik eylemi betikleri geliştirme</span><span class="sxs-lookup"><span data-stu-id="8be44-168">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions.md)
* <span data-ttu-id="8be44-169">[Yükleme ve Spark Hdınsight kümelerinde kullanma][hdinsight-install-spark]: betik eylemi örnek Spark yükleme hakkında</span><span class="sxs-lookup"><span data-stu-id="8be44-169">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark</span></span>
* <span data-ttu-id="8be44-170">[Hdınsight kümelerinde Giraph yükleme](hdinsight-hadoop-giraph-install.md): betik eylemi örnek Giraph yükleme hakkında</span><span class="sxs-lookup"><span data-stu-id="8be44-170">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph</span></span>
* <span data-ttu-id="8be44-171">[Hdınsight kümelerinde Solr yükleme](hdinsight-hadoop-solr-install-linux.md): Solr yükleme hakkında örnek betik eylemi.</span><span class="sxs-lookup"><span data-stu-id="8be44-171">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md): Script Action sample about installing Solr.</span></span>

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: ../hdinsight-provision-clusters/
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
[hdinsight-install-spark]: hdinsight-apache-spark-jupyter-spark-sql.md
