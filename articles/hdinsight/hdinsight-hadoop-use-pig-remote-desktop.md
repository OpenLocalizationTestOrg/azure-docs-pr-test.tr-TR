---
title: "aaaUse hdınsight'ta - Azure Uzak Masaüstü ile Hadoop Pig | Microsoft Docs"
description: "Nasıl toouse hello Pig komutu toorun Pig Latin deyimleri kümeden bir Uzak Masaüstü Bağlantısı tooa Windows tabanlı Hadoop hdınsight'ta öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e034a286-de0f-465f-8bf1-3d085ca6abed
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 2a4565fa827cd45fdbe6194b0486df93a6561084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-from-a-remote-desktop-connection"></a><span data-ttu-id="a4428-103">Uzak Masaüstü bağlantısı üzerinden pig işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="a4428-103">Run Pig jobs from a Remote Desktop connection</span></span>
[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="a4428-104">Bu belge, bir Uzak Masaüstü Bağlantısı tooa Windows tabanlı Hdınsight kümeden hello Pig komutu toorun Pig Latin deyimleri kullanmak için bir kılavuz sağlar.</span><span class="sxs-lookup"><span data-stu-id="a4428-104">This document provides a walkthrough for using hello Pig command toorun Pig Latin statements from a Remote Desktop connection tooa Windows-based HDInsight cluster.</span></span> <span data-ttu-id="a4428-105">Pig Latin veri dönüşümleri açıklayarak toocreate MapReduce uygulamaların sağlayan yerine harita ve işlevleri azaltır.</span><span class="sxs-lookup"><span data-stu-id="a4428-105">Pig Latin allows you toocreate MapReduce applications by describing data transformations, rather than map and reduce functions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a4428-106">Uzak Masaüstü, Windows hello işletim sistemi olarak kullanma Hdınsight kümelerinde yalnızca kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="a4428-106">Remote Desktop is only available on HDInsight clusters that use Windows as hello operating system.</span></span> <span data-ttu-id="a4428-107">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="a4428-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a4428-108">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="a4428-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="a4428-109">Hdınsight 3.4 veya büyük, bkz [Hdınsight ve SSH ile Pig kullanma](hdinsight-hadoop-use-pig-ssh.md) etkileşimli olarak Pig çalıştırma hakkında bilgi için doğrudan hello işlerine bir komut satırı ile küme.</span><span class="sxs-lookup"><span data-stu-id="a4428-109">For HDInsight 3.4 or greater, see [Use Pig with HDInsight and SSH](hdinsight-hadoop-use-pig-ssh.md) for information on interactively running Pig jobs directly on hello cluster from a command-line.</span></span>

## <span data-ttu-id="a4428-110"><a id="prereq"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="a4428-110"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="a4428-111">Bu makaledeki toocomplete hello adımları, hello aşağıdaki gerekir.</span><span class="sxs-lookup"><span data-stu-id="a4428-111">toocomplete hello steps in this article, you will need hello following.</span></span>

* <span data-ttu-id="a4428-112">Bir Windows tabanlı Hdınsight (Hadoop hdınsight) kümesi</span><span class="sxs-lookup"><span data-stu-id="a4428-112">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="a4428-113">Windows 10, Windows 8 veya Windows 7 çalıştıran bir istemci bilgisayar</span><span class="sxs-lookup"><span data-stu-id="a4428-113">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="a4428-114"><a id="connect"></a>İle Uzak Masaüstü Bağlantısı</span><span class="sxs-lookup"><span data-stu-id="a4428-114"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="a4428-115">Merhaba Hdınsight kümesi için Uzak Masaüstü'nü etkinleştirin, ardından hello yönergeleri izleyerek tooit bağlayın [RDP kullanarak tooHDInsight kümelerine bağlanmak](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="a4428-115">Enable Remote Desktop for hello HDInsight cluster, then connect tooit by following hello instructions at [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="a4428-116"><a id="pig"></a>Merhaba Pig komutunu kullanın</span><span class="sxs-lookup"><span data-stu-id="a4428-116"><a id="pig"></a>Use hello Pig command</span></span>
1. <span data-ttu-id="a4428-117">Uzak Masaüstü bağlantı kurduktan sonra hello Başlat **Hadoop komut satırı** hello masaüstünde hello simgesini kullanarak.</span><span class="sxs-lookup"><span data-stu-id="a4428-117">After you have a Remote Desktop connection, start hello **Hadoop Command Line** by using hello icon on hello desktop.</span></span>
2. <span data-ttu-id="a4428-118">Toostart hello Pig komutu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="a4428-118">Use hello following toostart hello Pig command:</span></span>

        %pig_home%\bin\pig

    <span data-ttu-id="a4428-119">İle sunulur bir `grunt>` istemi.</span><span class="sxs-lookup"><span data-stu-id="a4428-119">You will be presented with a `grunt>` prompt.</span></span>
3. <span data-ttu-id="a4428-120">Aşağıdaki ifadeyi hello girin:</span><span class="sxs-lookup"><span data-stu-id="a4428-120">Enter hello following statement:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';

    <span data-ttu-id="a4428-121">Bu komut hello sample.log dosyasının Merhaba içeriğine hello GÜNLÜKLERİ dosyasına yükler.</span><span class="sxs-lookup"><span data-stu-id="a4428-121">This command loads hello contents of hello sample.log file into hello LOGS file.</span></span> <span data-ttu-id="a4428-122">Merhaba dosyasının Merhaba içeriğine komutu aşağıdaki hello kullanarak görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a4428-122">You can view hello contents of hello file by using hello following command:</span></span>

        DUMP LOGS;
4. <span data-ttu-id="a4428-123">Merhaba verileri her kaydından bir normal ifade tooextract yalnızca hello günlük düzeyi uygulayarak dönüştürün:</span><span class="sxs-lookup"><span data-stu-id="a4428-123">Transform hello data by applying a regular expression tooextract only hello logging level from each record:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="a4428-124">Kullanabileceğiniz **dökümü** tooview hello veri hello dönüştürme sonra.</span><span class="sxs-lookup"><span data-stu-id="a4428-124">You can use **DUMP** tooview hello data after hello transformation.</span></span> <span data-ttu-id="a4428-125">Bu durumda, `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="a4428-125">In this case, `DUMP LEVELS;`.</span></span>
5. <span data-ttu-id="a4428-126">Deyimlerini aşağıdaki hello kullanarak dönüşümleri uygulama devam edin.</span><span class="sxs-lookup"><span data-stu-id="a4428-126">Continue applying transformations by using hello following statements.</span></span> <span data-ttu-id="a4428-127">Kullanım `DUMP` her adımından sonra hello dönüşümünün tooview hello sonucu.</span><span class="sxs-lookup"><span data-stu-id="a4428-127">Use `DUMP` tooview hello result of hello transformation after each step.</span></span>

    <table>
    <tr>
    <th><span data-ttu-id="a4428-128">Deyimi</span><span class="sxs-lookup"><span data-stu-id="a4428-128">Statement</span></span></th><th><span data-ttu-id="a4428-129">Neler yapar?</span><span class="sxs-lookup"><span data-stu-id="a4428-129">What it does</span></span></th>
    </tr>
    <tr>
    <td><span data-ttu-id="a4428-130">FILTEREDLEVELS = LOGLEVEL FİLTRE DÜZEYLERİYLE null; değil</span><span class="sxs-lookup"><span data-stu-id="a4428-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span></span></td><td><span data-ttu-id="a4428-131">Merhaba günlük düzeyi null değerini içeren satırları kaldırır ve hello sonuçları FILTEREDLEVELS depolar.</span><span class="sxs-lookup"><span data-stu-id="a4428-131">Removes rows that contain a null value for hello log level and stores hello results into FILTEREDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="a4428-132">GROUPEDLEVELS Grup FILTEREDLEVELS LOGLEVEL tarafından; =</span><span class="sxs-lookup"><span data-stu-id="a4428-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span></span></td><td><span data-ttu-id="a4428-133">Grupları hello günlük düzeyi tarafından satırlar ve hello sonuçları GROUPEDLEVELS depolar.</span><span class="sxs-lookup"><span data-stu-id="a4428-133">Groups hello rows by log level and stores hello results into GROUPEDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="a4428-134">Sıklık foreach = GROUPEDLEVELS sayısı (FILTEREDLEVELS LOGLEVEL Grup Oluştur. LOGLEVEL) sayısı gibi;</span><span class="sxs-lookup"><span data-stu-id="a4428-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span></span></td><td><span data-ttu-id="a4428-135">Yeni bir küme oluşturur her benzersiz günlük içeren verilerin düzeyi değeri ve kaç kez oluşur.</span><span class="sxs-lookup"><span data-stu-id="a4428-135">Creates a new set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="a4428-136">Bu SIKLIKLARINI depolanır</span><span class="sxs-lookup"><span data-stu-id="a4428-136">This is stored into FREQUENCIES</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="a4428-137">Sonuç order SIKLIĞI sayısı desc tarafından; =</span><span class="sxs-lookup"><span data-stu-id="a4428-137">RESULT = order FREQUENCIES by COUNT desc;</span></span></td><td><span data-ttu-id="a4428-138">Merhaba günlük düzeyleri (Azalan) sayısı ve depoları sonucu sıralar</span><span class="sxs-lookup"><span data-stu-id="a4428-138">Orders hello log levels by count (descending,) and stores into RESULT</span></span></td>
    </tr>
    </table><span data-ttu-id="a4428-139">
6.Hello kullanarak bir dönüşüm hello sonuçlarını da kaydedebilirsiniz `STORE` deyimi.</span><span class="sxs-lookup"><span data-stu-id="a4428-139">
6. You can also save hello results of a transformation by using hello `STORE` statement.</span></span> <span data-ttu-id="a4428-140">Örneğin, komutu aşağıdaki hello hello kaydeder `RESULT` toohello **/example/data/pigout** kümenizin hello varsayılan depolama kapsayıcısını dizin:</span><span class="sxs-lookup"><span data-stu-id="a4428-140">For example, hello following command saves hello `RESULT` toohello **/example/data/pigout** directory in hello default storage container for your cluster:</span></span>

        STORE RESULT into 'wasb:///example/data/pigout'

   > [!NOTE]
   > <span data-ttu-id="a4428-141">Merhaba veri hello adlı dosyaları belirtilen dizinde depolanır **bölümü nnnnn**.</span><span class="sxs-lookup"><span data-stu-id="a4428-141">hello data is stored in hello specified directory in files named **part-nnnnn**.</span></span> <span data-ttu-id="a4428-142">Merhaba dizini zaten varsa, bir hata iletisi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="a4428-142">If hello directory already exists, you will receive an error message.</span></span>
   >
   >
7. <span data-ttu-id="a4428-143">tooexit hello grunt komut isteminde, aşağıdaki ifadeyi hello girin.</span><span class="sxs-lookup"><span data-stu-id="a4428-143">tooexit hello grunt prompt, enter hello following statement.</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="a4428-144">Pig Latin toplu iş dosyaları</span><span class="sxs-lookup"><span data-stu-id="a4428-144">Pig Latin batch files</span></span>
<span data-ttu-id="a4428-145">Bir dosyada hello Pig komutu toorun yer Pig Latin de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a4428-145">You can also use hello Pig command toorun Pig Latin that is contained in a file.</span></span>

1. <span data-ttu-id="a4428-146">Merhaba grunt istemi çıktıktan sonra açmak **not defteri** ve adlı yeni bir dosya oluşturun **pigbatch.pig** hello içinde **PIG_HOME %** dizin.</span><span class="sxs-lookup"><span data-stu-id="a4428-146">After exiting hello grunt prompt, open **Notepad** and create a new file named **pigbatch.pig** in hello **%PIG_HOME%** directory.</span></span>
2. <span data-ttu-id="a4428-147">Türü veya Yapıştır hello aşağıdaki satırları hello **pigbatch.pig** dosya ve dosyayı kaydedin:</span><span class="sxs-lookup"><span data-stu-id="a4428-147">Type or paste hello following lines into hello **pigbatch.pig** file, and then save it:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;
3. <span data-ttu-id="a4428-148">Kullanım hello toorun hello aşağıdaki **pigbatch.pig** hello pig komutunu kullanarak dosya.</span><span class="sxs-lookup"><span data-stu-id="a4428-148">Use hello following toorun hello **pigbatch.pig** file using hello pig command.</span></span>

        pig %PIG_HOME%\pigbatch.pig

    <span data-ttu-id="a4428-149">Merhaba toplu işi tamamlandığında aynı olarak kullanıldığında hello çıktı aşağıdaki hello görmelisiniz `DUMP RESULT;` hello önceki adımlarda:</span><span class="sxs-lookup"><span data-stu-id="a4428-149">When hello batch job completes, you should see hello following output, which should be hello same as when you used `DUMP RESULT;` in hello previous steps:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="a4428-150"><a id="summary"></a>Özet</span><span class="sxs-lookup"><span data-stu-id="a4428-150"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="a4428-151">Gördüğünüz gibi hello Pig komutu, MapReduce işlemleri çalıştırın ya da bir toplu iş dosyasında depolanan Pig Latin işleri çalıştırma toointeractively sağlar.</span><span class="sxs-lookup"><span data-stu-id="a4428-151">As you can see, hello Pig command allows you toointeractively run MapReduce operations, or run Pig Latin jobs that are stored in a batch file.</span></span>

## <span data-ttu-id="a4428-152"><a id="nextsteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a4428-152"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="a4428-153">Hdınsight'ta Pig hakkında genel bilgi için:</span><span class="sxs-lookup"><span data-stu-id="a4428-153">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="a4428-154">Hdınsight'ta Hadoop ile pig kullanma</span><span class="sxs-lookup"><span data-stu-id="a4428-154">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="a4428-155">Diğer yolları hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="a4428-155">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="a4428-156">Hdınsight'ta Hadoop ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="a4428-156">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="a4428-157">Hdınsight'ta Hadoop ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="a4428-157">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
