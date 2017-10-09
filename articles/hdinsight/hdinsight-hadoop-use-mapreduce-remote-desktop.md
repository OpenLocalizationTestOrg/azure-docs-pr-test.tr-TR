---
title: "aaaMapReduce ve hdınsight'ta - Azure Hadoop ile Uzak Masaüstü | Microsoft Docs"
description: "Bilgi nasıl toouse Uzak Masaüstü tooconnect tooHadoop Hdınsight ve çalışma MapReduce işleri."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9d3a7b34-7def-4c2e-bb6c-52682d30dee8
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: bdbbcf59ca86dd1b170471aa9e12334a04c23667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="fe184-103">Uzak Masaüstü kullanarak hdınsight'ta Hadoop MapReduce kullanın</span><span class="sxs-lookup"><span data-stu-id="fe184-103">Use MapReduce in Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="fe184-104">Bu makalede, nasıl tooconnect tooa hdınsight'ta Hadoop küme Uzak Masaüstü'nü kullanarak öğrenin ve MapReduce işleri hello Hadoop komutunu kullanarak çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="fe184-104">In this article, you will learn how tooconnect tooa Hadoop on HDInsight cluster by using Remote Desktop and then run MapReduce jobs by using hello Hadoop command.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fe184-105">Uzak Masaüstü yalnızca Windows tabanlı Hdınsight kümelerinde kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fe184-105">Remote Desktop is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="fe184-106">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="fe184-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="fe184-107">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="fe184-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="fe184-108">Hdınsight 3.4 veya büyük, bkz [SSH ile kullanım MapReduce](hdinsight-hadoop-use-mapreduce-ssh.md) toohello Hdınsight kümesine bağlanma ve MapReduce işleri çalıştırma hakkında bilgi için.</span><span class="sxs-lookup"><span data-stu-id="fe184-108">For HDInsight 3.4 or greater, see [Use MapReduce with SSH](hdinsight-hadoop-use-mapreduce-ssh.md) for information on connecting toohello HDInsight cluster and running MapReduce jobs.</span></span>

## <span data-ttu-id="fe184-109"><a id="prereq"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="fe184-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="fe184-110">Bu makaledeki toocomplete hello adımları, hello aşağıdaki gerekir:</span><span class="sxs-lookup"><span data-stu-id="fe184-110">toocomplete hello steps in this article, you will need hello following:</span></span>

* <span data-ttu-id="fe184-111">Bir Windows tabanlı Hdınsight (Hadoop hdınsight) kümesi</span><span class="sxs-lookup"><span data-stu-id="fe184-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="fe184-112">Windows 10, Windows 8 veya Windows 7 çalıştıran bir istemci bilgisayar</span><span class="sxs-lookup"><span data-stu-id="fe184-112">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="fe184-113"><a id="connect"></a>İle Uzak Masaüstü Bağlantısı</span><span class="sxs-lookup"><span data-stu-id="fe184-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="fe184-114">Merhaba Hdınsight kümesi için Uzak Masaüstü'nü etkinleştirin, ardından hello yönergeleri izleyerek tooit bağlayın [RDP kullanarak tooHDInsight kümelerine bağlanmak](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="fe184-114">Enable Remote Desktop for hello HDInsight cluster, then connect tooit by following hello instructions at [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="fe184-115"><a id="hadoop"></a>Merhaba Hadoop komutunu kullanın</span><span class="sxs-lookup"><span data-stu-id="fe184-115"><a id="hadoop"></a>Use hello Hadoop command</span></span>
<span data-ttu-id="fe184-116">Merhaba Hdınsight kümesi için bağlı toohello Masaüstü olduğunda hello Hadoop komutunu kullanarak adımları toorun bir MapReduce işi aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="fe184-116">When you are connected toohello desktop for hello HDInsight cluster, use hello following steps toorun a MapReduce job by using hello Hadoop command:</span></span>

1. <span data-ttu-id="fe184-117">Merhaba Hello Hdınsight masaüstünden başlatmak **Hadoop komut satırı**.</span><span class="sxs-lookup"><span data-stu-id="fe184-117">From hello HDInsight desktop, start hello **Hadoop Command Line**.</span></span> <span data-ttu-id="fe184-118">Bu yeni bir komut istemi hello açar **c:\apps\dist\hadoop-&lt;sürüm numarası >** dizin.</span><span class="sxs-lookup"><span data-stu-id="fe184-118">This opens a new command prompt in hello **c:\apps\dist\hadoop-&lt;version number>** directory.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fe184-119">Hadoop güncelleştirildikçe hello sürüm numarasını değiştirir.</span><span class="sxs-lookup"><span data-stu-id="fe184-119">hello version number changes as Hadoop is updated.</span></span> <span data-ttu-id="fe184-120">Merhaba **HADOOP_HOME** ortam değişkeni kullanılan toofind hello yolu olabilir.</span><span class="sxs-lookup"><span data-stu-id="fe184-120">hello **HADOOP_HOME** environment variable can be used toofind hello path.</span></span> <span data-ttu-id="fe184-121">Örneğin, `cd %HADOOP_HOME%` tooknow hello sürüm numarası gerektirmeden değişiklikleri dizinleri toohello Hadoop dizini.</span><span class="sxs-lookup"><span data-stu-id="fe184-121">For example, `cd %HADOOP_HOME%` changes directories toohello Hadoop directory, without requiring you tooknow hello version number.</span></span>
   >
   >
2. <span data-ttu-id="fe184-122">toouse hello **Hadoop** komut toorun bir örnek MapReduce işi, hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="fe184-122">toouse hello **Hadoop** command toorun an example MapReduce job, use hello following command:</span></span>

        hadoop jar hadoop-mapreduce-examples.jar wordcount wasb:///example/data/gutenberg/davinci.txt wasb:///example/data/WordCountOutput

    <span data-ttu-id="fe184-123">Bu hello başlatır **wordcount** hello bulunan sınıfı **hadoop mapreduce examples.jar** hello geçerli dizinde dosya.</span><span class="sxs-lookup"><span data-stu-id="fe184-123">This starts hello **wordcount** class, which is contained in hello **hadoop-mapreduce-examples.jar** file in hello current directory.</span></span> <span data-ttu-id="fe184-124">İsteğe bağlı olarak giriş olarak hello kullanır **wasb://example/data/gutenberg/davinci.txt** belge ve çıktı konumunda depolanır: **wasb: / / / örnek/data/WordCountOutput**.</span><span class="sxs-lookup"><span data-stu-id="fe184-124">As input, it uses hello **wasb://example/data/gutenberg/davinci.txt** document, and output is stored at: **wasb:///example/data/WordCountOutput**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fe184-125">Bu MapReduce işi ve hello örnek veriler hakkında daha fazla bilgi için bkz: <a href="hdinsight-use-mapreduce.md">Hdınsight Hadoop içinde kullanım MapReduce</a>.</span><span class="sxs-lookup"><span data-stu-id="fe184-125">for more information about this MapReduce job and hello example data, see <a href="hdinsight-use-mapreduce.md">Use MapReduce in HDInsight Hadoop</a>.</span></span>
   >
   >
3. <span data-ttu-id="fe184-126">Merhaba iş ayrıntıları bu işlenir ve hello iş tamamlandığında bilgi benzer toohello aşağıdaki döndürür gösterir:</span><span class="sxs-lookup"><span data-stu-id="fe184-126">hello job emits details as it is processed, and it returns information similar toohello following when hello job is complete:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623
4. <span data-ttu-id="fe184-127">Hello iş tamamlandıktan sonra aşağıdaki komut toolist hello çıktı dosyaları depolandığı hello kullanmak **wasb://example/data/WordCountOutput**:</span><span class="sxs-lookup"><span data-stu-id="fe184-127">When hello job is complete, use hello following command toolist hello output files stored at **wasb://example/data/WordCountOutput**:</span></span>

        hadoop fs -ls wasb:///example/data/WordCountOutput

    <span data-ttu-id="fe184-128">Bu iki dosya görüntülenmelidir **_SUCCESS** ve **bölümü r 00000**.</span><span class="sxs-lookup"><span data-stu-id="fe184-128">This should display two files, **_SUCCESS** and **part-r-00000**.</span></span> <span data-ttu-id="fe184-129">Merhaba **bölümü r 00000** dosyası hello çıktı bu iş için içerir.</span><span class="sxs-lookup"><span data-stu-id="fe184-129">hello **part-r-00000** file contains hello output for this job.</span></span>

   > [!NOTE]
   > <span data-ttu-id="fe184-130">Bazı MapReduce işleri hello sonuçları birden çok bölme **bölümü r ###** dosyaları.</span><span class="sxs-lookup"><span data-stu-id="fe184-130">Some MapReduce jobs may split hello results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="fe184-131">Öyleyse, hello kullan ### soneki hello dosyalarının tooindicate hello sırası.</span><span class="sxs-lookup"><span data-stu-id="fe184-131">If so, use hello ##### suffix tooindicate hello order of hello files.</span></span>
   >
   >
5. <span data-ttu-id="fe184-132">tooview hello çıkışı, komutu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="fe184-132">tooview hello output, use hello following command:</span></span>

        hadoop fs -cat wasb:///example/data/WordCountOutput/part-r-00000

    <span data-ttu-id="fe184-133">Bu hello içerdiği hello sözcüklerin listesini görüntüler **wasb://example/data/gutenberg/davinci.txt** hello her sözcüğün yapma sayısı yanı sıra dosya.</span><span class="sxs-lookup"><span data-stu-id="fe184-133">This displays a list of hello words that are contained in hello **wasb://example/data/gutenberg/davinci.txt** file, along with hello number of times each word occured.</span></span> <span data-ttu-id="fe184-134">Merhaba, hello dosyasında yer alan hello veri örneği aşağıdadır:</span><span class="sxs-lookup"><span data-stu-id="fe184-134">hello following is an example of hello data that will be contained in hello file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <span data-ttu-id="fe184-135"><a id="summary"></a>Özet</span><span class="sxs-lookup"><span data-stu-id="fe184-135"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="fe184-136">Gördüğünüz gibi hello Hadoop komutu kolay bir yolu toorun MapReduce işleri bir Hdınsight kümesi ve görünüm hello iş çıktısı sonra sağlar.</span><span class="sxs-lookup"><span data-stu-id="fe184-136">As you can see, hello Hadoop command provides an easy way toorun MapReduce jobs on an HDInsight cluster and then view hello job output.</span></span>

## <span data-ttu-id="fe184-137"><a id="nextsteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fe184-137"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="fe184-138">Hdınsight'ta MapReduce işleri hakkında genel bilgi için:</span><span class="sxs-lookup"><span data-stu-id="fe184-138">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="fe184-139">Hdınsight Hadoop MapReduce kullanın</span><span class="sxs-lookup"><span data-stu-id="fe184-139">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="fe184-140">Diğer yolları hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fe184-140">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="fe184-141">Hdınsight'ta Hadoop ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="fe184-141">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="fe184-142">Hdınsight'ta Hadoop ile pig kullanma</span><span class="sxs-lookup"><span data-stu-id="fe184-142">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
