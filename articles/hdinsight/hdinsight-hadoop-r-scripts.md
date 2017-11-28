---
title: "Hdınsight toocustomize kümelerinde - Azure R aaaUse | Microsoft Docs"
description: "Bilgi nasıl tooinstall R kullanarak komut dosyası eylemi ve Hdınsight kümelerinde R kullanın."
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
ms.openlocfilehash: bf5adf2e18dc43a743b29fd1567fad731b9c3ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-r-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="a4581-103">HDInsight'taki Hadoop kümelerinde R programını yükleme ve kullanma</span><span class="sxs-lookup"><span data-stu-id="a4581-103">Install and use R on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="a4581-104">Toocustomize Windows Hdınsight kümesi R ile betik eylemi kullanarak nasıl temel ve nasıl hdınsight'ta R toouse kümeleri öğrenin.</span><span class="sxs-lookup"><span data-stu-id="a4581-104">Learn how toocustomize Windows based HDInsight cluster with R using Script Action, and how toouse R on HDInsight clusters.</span></span> <span data-ttu-id="a4581-105">Merhaba [Hdınsight teklifi](https://azure.microsoft.com/pricing/details/hdinsight/) R Server Hdınsight kümenize bir parçası olarak içerir.</span><span class="sxs-lookup"><span data-stu-id="a4581-105">hello [HDInsight offering](https://azure.microsoft.com/pricing/details/hdinsight/) includes R Server as part of your HDInsight cluster.</span></span> <span data-ttu-id="a4581-106">Bu R betiklerini toouse MapReduce ve Spark dağıtılmış toorun hesaplamalar sağlar.</span><span class="sxs-lookup"><span data-stu-id="a4581-106">This allows R scripts toouse MapReduce and Spark toorun distributed computations.</span></span> <span data-ttu-id="a4581-107">Daha fazla bilgi için bkz. [HDInsight R Server kullanmaya başlama](hdinsight-hadoop-r-server-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a4581-107">For more information, see [Get started using R Server on HDInsight](hdinsight-hadoop-r-server-get-started.md).</span></span> <span data-ttu-id="a4581-108">Linux tabanlı bir kümeyle R kullanma hakkında daha fazla bilgi için bkz: [yükleme ve kullanma R Hdınsight Hadoop kümeleri (Linux) üzerinde](hdinsight-hadoop-r-scripts-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a4581-108">For information on using R with a Linux-based cluster, see [Install and use R on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-r-scripts-linux.md).</span></span>

<span data-ttu-id="a4581-109">Kullanarak Azure Hdınsight (Hadoop, Storm, HBase, Spark) kümede herhangi bir türde üzerinde R yükleyebilirsiniz *betik eylemi*.</span><span class="sxs-lookup"><span data-stu-id="a4581-109">You can install R on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="a4581-110">Hdınsight kümesinde bir örnek komut dosyası tooinstall R Salt okunur Azure depolama blobunu gelen kullanılabilir [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span><span class="sxs-lookup"><span data-stu-id="a4581-110">A sample script tooinstall R on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span></span>

<span data-ttu-id="a4581-111">**İlgili makaleler**</span><span class="sxs-lookup"><span data-stu-id="a4581-111">**Related articles**</span></span>

* [<span data-ttu-id="a4581-112">Yükleme ve Hdınsight Hadoop kümeleri (Linux) R kullanma</span><span class="sxs-lookup"><span data-stu-id="a4581-112">Install and use R on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-r-scripts-linux.md)
* <span data-ttu-id="a4581-113">[Hdınsight'ta Hadoop kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md): Hdınsight kümeleri oluşturma hakkında genel bilgiler</span><span class="sxs-lookup"><span data-stu-id="a4581-113">[Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): general information on creating HDInsight clusters</span></span>
* <span data-ttu-id="a4581-114">[Betik eylemi kullanarak Hdınsight kümesi özelleştirme][hdinsight-cluster-customize]: betik eylemi kullanarak Hdınsight kümelerini özelleştirme hakkında genel bilgiler</span><span class="sxs-lookup"><span data-stu-id="a4581-114">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action</span></span>
* [<span data-ttu-id="a4581-115">Hdınsight için betik eylemi betikleri geliştirme</span><span class="sxs-lookup"><span data-stu-id="a4581-115">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions.md)

## <a name="what-is-r"></a><span data-ttu-id="a4581-116">R nedir?</span><span class="sxs-lookup"><span data-stu-id="a4581-116">What is R?</span></span>
<span data-ttu-id="a4581-117">Merhaba <a href="http://www.r-project.org/" target="_blank">R proje istatistiksel bilgi işlem için</a> bir açık kaynak dili ve istatistiksel bilgi işlem ortamı.</span><span class="sxs-lookup"><span data-stu-id="a4581-117">hello <a href="http://www.r-project.org/" target="_blank">R Project for Statistical Computing</a> is an open source language and environment for statistical computing.</span></span> <span data-ttu-id="a4581-118">R yüzlerce yapı içinde istatistik işlevleri ve işlev ve nesne odaklı programlama yönlerini birleştirir kendi programlama dili sağlar.</span><span class="sxs-lookup"><span data-stu-id="a4581-118">R provides hundreds of build-in statistical functions and its own programming language that combines aspects of functional and object-oriented programming.</span></span> <span data-ttu-id="a4581-119">Yoğun grafik yetenekleri de sağlar.</span><span class="sxs-lookup"><span data-stu-id="a4581-119">It also provides extensive graphical capabilities.</span></span> <span data-ttu-id="a4581-120">R hello tercih edilen programlama için en profesyonel istatistikçiler ve çeşitli alanları bilimcilerine ortamıdır.</span><span class="sxs-lookup"><span data-stu-id="a4581-120">R is hello preferred programming environment for most professional statisticians and scientists in a wide variety of fields.</span></span>

<span data-ttu-id="a4581-121">R Azure Blob Storage (WASB) ile uyumlu, böylelikle var. depolanan verileri R kullanarak işlenebilir.</span><span class="sxs-lookup"><span data-stu-id="a4581-121">R is compatible with Azure Blob Storage (WASB) so that data that is stored there can be processed using R on HDInsight.</span></span>  

## <a name="install-r"></a><span data-ttu-id="a4581-122">R yükleme</span><span class="sxs-lookup"><span data-stu-id="a4581-122">Install R</span></span>
<span data-ttu-id="a4581-123">A [örnek komut dosyası](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) tooinstall R Hdınsight kümesinde, Azure storage'da salt okunur bir blob'nden edinilebilir.</span><span class="sxs-lookup"><span data-stu-id="a4581-123">A [sample script](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) tooinstall R on an HDInsight cluster is available from a read-only blob in Azure Storage.</span></span> <span data-ttu-id="a4581-124">Bu bölümde nasıl toouse hello örnek betik hello Azure Portal kullanarak hello küme oluşturulurken bir hata ile ilgili yönergeler sağlar.</span><span class="sxs-lookup"><span data-stu-id="a4581-124">This section provides instructions about how toouse hello sample script while creating hello cluster using hello Azure Portal.</span></span>

> [!NOTE]
> <span data-ttu-id="a4581-125">Merhaba örnek betik, Hdınsight kümesi sürüm 3.1 sunulmuştur.</span><span class="sxs-lookup"><span data-stu-id="a4581-125">hello sample script was introduced with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="a4581-126">Hdınsight küme sürümleri hakkında daha fazla bilgi için bkz: [Hdınsight küme sürümleri](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="a4581-126">For more information about  HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>
>
>

1. <span data-ttu-id="a4581-127">Hello Portalı ' bir Hdınsight kümesi oluştururken tıklatın **isteğe bağlı yapılandırma**ve ardından **betik eylemleri**.</span><span class="sxs-lookup"><span data-stu-id="a4581-127">When you create an HDInsight cluster from hello Portal, click **Optional Configuration**, and then click **Script Actions**.</span></span>
2. <span data-ttu-id="a4581-128">Merhaba üzerinde **betik eylemleri** sayfasında, aşağıdaki değerleri hello girin:</span><span class="sxs-lookup"><span data-stu-id="a4581-128">On hello **Script Actions** page, enter hello following values:</span></span>

    <span data-ttu-id="a4581-129">![Betik eylemi toocustomize bir küme kullanın](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "kullanım betik eylemi toocustomize küme")</span><span class="sxs-lookup"><span data-stu-id="a4581-129">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="a4581-130">Özellik</span><span class="sxs-lookup"><span data-stu-id="a4581-130">Property</span></span></th><th><span data-ttu-id="a4581-131">Değer</span><span class="sxs-lookup"><span data-stu-id="a4581-131">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="a4581-132">Ad</span><span class="sxs-lookup"><span data-stu-id="a4581-132">Name</span></span></td>
            <td><span data-ttu-id="a4581-133">Örneğin, hello betik eylemi için bir ad belirtmeniz <b>R yükleme</b>.</span><span class="sxs-lookup"><span data-stu-id="a4581-133">Specify a name for hello script action, for example, <b>Install R</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="a4581-134">Betik URI'si</span><span class="sxs-lookup"><span data-stu-id="a4581-134">Script URI</span></span></td>
            <td><span data-ttu-id="a4581-135">Çağrılan toocustomize hello küme, örneğin, hello URI toohello komut dosyasını belirtin <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></span><span class="sxs-lookup"><span data-stu-id="a4581-135">Specify hello URI toohello script that is invoked toocustomize hello cluster, for example, <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="a4581-136">Düğüm Türü</span><span class="sxs-lookup"><span data-stu-id="a4581-136">Node Type</span></span></td>
            <td><span data-ttu-id="a4581-137">Merhaba özelleştirme betik çalıştığı hello düğüm belirtin.</span><span class="sxs-lookup"><span data-stu-id="a4581-137">Specify hello nodes on which hello customization script is run.</span></span> <span data-ttu-id="a4581-138">Seçebileceğiniz <b>tüm düğümleri</b>, <b>Head yalnızca düğümlerin</b>, veya <b>çalışan düğümleri</b> yalnızca.</span><span class="sxs-lookup"><span data-stu-id="a4581-138">You can choose <b>All Nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes</b> only.</span></span>
        <tr><td><span data-ttu-id="a4581-139">Parametreler</span><span class="sxs-lookup"><span data-stu-id="a4581-139">Parameters</span></span></td>
            <td><span data-ttu-id="a4581-140">Merhaba komut dosyası için gereken Hello parametreleri belirtin.</span><span class="sxs-lookup"><span data-stu-id="a4581-140">Specify hello parameters, if required by hello script.</span></span> <span data-ttu-id="a4581-141">Ancak, bunu boş bırakabilirsiniz şekilde hello betik tooinstall R herhangi bir parametre gerektirmez.</span><span class="sxs-lookup"><span data-stu-id="a4581-141">However, hello script tooinstall R does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="a4581-142">Birden fazla betik eylemi tooinstall hello kümede birden çok bileşen ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4581-142">You can add more than one script action tooinstall multiple components on hello cluster.</span></span> <span data-ttu-id="a4581-143">Merhaba komut dosyaları ekledikten sonra hello küme crating hello onay işareti toostart'ı tıklatın.</span><span class="sxs-lookup"><span data-stu-id="a4581-143">After you have added hello scripts, click hello check mark toostart crating hello cluster.</span></span>

<span data-ttu-id="a4581-144">Azure PowerShell veya Hdınsight .NET SDK'sı hello kullanarak Hdınsight'ta hello betik tooinstall R de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4581-144">You can also use hello script tooinstall R on HDInsight by using Azure PowerShell or hello HDInsight .NET SDK.</span></span> <span data-ttu-id="a4581-145">Bu yordamları için yönergeler bu makalenin sonraki bölümlerinde verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a4581-145">Instructions for these procedures are provided later in this article.</span></span>

## <a name="run-r-scripts"></a><span data-ttu-id="a4581-146">R betiği çalıştırın</span><span class="sxs-lookup"><span data-stu-id="a4581-146">Run R scripts</span></span>
<span data-ttu-id="a4581-147">Bu bölümde, nasıl toorun bir R betiği hello Hadoop küme Hdınsight ile açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="a4581-147">This section describes how toorun an R script on hello Hadoop cluster with HDInsight.</span></span>

1. <span data-ttu-id="a4581-148">**Uzak Masaüstü Bağlantısı toohello küme kurmak**: hello Portal, yüklü R ile oluşturduğunuz hello küme için Uzak masaüstünü etkinleştir ve toohello kümesine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="a4581-148">**Establish a Remote Desktop connection toohello cluster**: From hello Portal, enable Remote Desktop for hello cluster you created with R installed, and then connect toohello cluster.</span></span> <span data-ttu-id="a4581-149">Yönergeler için bkz: [RDP kullanarak tooHDInsight kümelerine bağlanmak](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="a4581-149">For instructions, see [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>
2. <span data-ttu-id="a4581-150">**Açık hello R konsol**: hello R yükleme hello baş düğüm hello masaüstünde bir bağlantı toohello R konsol koyar.</span><span class="sxs-lookup"><span data-stu-id="a4581-150">**Open hello R console**: hello R installation puts a link toohello R console on hello desktop of hello head node.</span></span> <span data-ttu-id="a4581-151">' I tıklatın, üzerinde tooopen hello R konsol.</span><span class="sxs-lookup"><span data-stu-id="a4581-151">Click on it tooopen hello R console.</span></span>
3. <span data-ttu-id="a4581-152">**Merhaba R betiği çalıştırma**: hello R betiği, yapıştırma seçerek ve ENTER tuşuna basarak doğrudan hello R konsolundan çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="a4581-152">**Run hello R script**: hello R script can be run directly from hello R console by pasting it, selecting it, and pressing ENTER.</span></span> <span data-ttu-id="a4581-153">Burada, hello 1 sayıları too100 oluşturur ve bunları 2 ile çarpar basit bir örnek komut verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="a4581-153">Here is a simple example script that generates hello numbers 1 too100 and then multiplies them by 2.</span></span>

        library(rmr2)
        library(rhdfs)
        ints = to.dfs(1:100)
        calc = mapreduce(input = ints, map = function(k, v) cbind(v, 2*v))
        from.dfs(calc)

<span data-ttu-id="a4581-154">r ile yüklenen hello ilk iki satır çağrısı hello RHadoop kitaplıkları son satırı baskı siparişi hello sonuçları toohello konsol hello.</span><span class="sxs-lookup"><span data-stu-id="a4581-154">hello first two lines call hello RHadoop libraries that are installed with R. hello final line prints hello results toohello console.</span></span> <span data-ttu-id="a4581-155">Merhaba çıktı aşağıdaki gibi görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="a4581-155">hello output should look like this:</span></span>

    [1,]  1 2
    [2,]  2 4
    .
    .
    .
    [98,]  98 196
    [99,]  99 198
    [100,] 100 200


## <a name="install-r-using-aure-powershell"></a><span data-ttu-id="a4581-156">R işlemleri PowerShell kullanarak yükleme</span><span class="sxs-lookup"><span data-stu-id="a4581-156">Install R using Aure PowerShell</span></span>
<span data-ttu-id="a4581-157">Bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="a4581-157">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="a4581-158">Merhaba örnek gösterilmektedir nasıl tooinstall Azure PowerShell kullanarak Spark.</span><span class="sxs-lookup"><span data-stu-id="a4581-158">hello sample demonstrates how tooinstall Spark using Azure PowerShell.</span></span> <span data-ttu-id="a4581-159">Toocustomize hello betik toouse gerek [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span><span class="sxs-lookup"><span data-stu-id="a4581-159">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span></span>

## <a name="install-r-using-net-sdk"></a><span data-ttu-id="a4581-160">.NET SDK kullanarak R yükleme</span><span class="sxs-lookup"><span data-stu-id="a4581-160">Install R using .NET SDK</span></span>
<span data-ttu-id="a4581-161">Bkz: [özelleştirme Hdınsight kümeleri betik eylemi kullanarak](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="a4581-161">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="a4581-162">Merhaba örnek gösterilmektedir nasıl tooinstall Spark hello .NET SDK kullanarak.</span><span class="sxs-lookup"><span data-stu-id="a4581-162">hello sample demonstrates how tooinstall Spark using hello .NET SDK.</span></span> <span data-ttu-id="a4581-163">Toocustomize hello betik toouse gerek [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11).</span><span class="sxs-lookup"><span data-stu-id="a4581-163">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11).</span></span>

## <a name="see-also"></a><span data-ttu-id="a4581-164">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="a4581-164">See also</span></span>
* [<span data-ttu-id="a4581-165">Yükleme ve Hdınsight Hadoop kümeleri (Linux) R kullanma</span><span class="sxs-lookup"><span data-stu-id="a4581-165">Install and use R on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-r-scripts-linux.md)
* <span data-ttu-id="a4581-166">[Hdınsight'ta Hadoop kümeleri oluşturma](hdinsight-hadoop-provision-linux-clusters.md): Hdınsight kümeleri oluşturma hakkında genel bilgiler</span><span class="sxs-lookup"><span data-stu-id="a4581-166">[Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): general information on creating HDInsight clusters</span></span>
* <span data-ttu-id="a4581-167">[Betik eylemi kullanarak Hdınsight kümesi özelleştirme][hdinsight-cluster-customize]: betik eylemi kullanarak Hdınsight kümelerini özelleştirme hakkında genel bilgiler</span><span class="sxs-lookup"><span data-stu-id="a4581-167">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action</span></span>
* [<span data-ttu-id="a4581-168">Hdınsight için betik eylemi betikleri geliştirme</span><span class="sxs-lookup"><span data-stu-id="a4581-168">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions.md)
* <span data-ttu-id="a4581-169">[Yükleme ve Spark Hdınsight kümelerinde kullanma][hdinsight-install-spark]: betik eylemi örnek Spark yükleme hakkında</span><span class="sxs-lookup"><span data-stu-id="a4581-169">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark</span></span>
* <span data-ttu-id="a4581-170">[Hdınsight kümelerinde Giraph yükleme](hdinsight-hadoop-giraph-install.md): betik eylemi örnek Giraph yükleme hakkında</span><span class="sxs-lookup"><span data-stu-id="a4581-170">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph</span></span>
* <span data-ttu-id="a4581-171">[Hdınsight kümelerinde Solr yükleme](hdinsight-hadoop-solr-install-linux.md): Solr yükleme hakkında örnek betik eylemi.</span><span class="sxs-lookup"><span data-stu-id="a4581-171">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md): Script Action sample about installing Solr.</span></span>

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: ../hdinsight-provision-clusters/
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
[hdinsight-install-spark]: hdinsight-apache-spark-jupyter-spark-sql.md
