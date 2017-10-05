---
title: "Hadoop Pig hdınsight'ta - Azure Uzak Masaüstü ile kullanma | Microsoft Docs"
description: "Hdınsight'ta bir Windows tabanlı Hadoop kümesine bir Uzak Masaüstü bağlantısı üzerinden Pig Latin deyimleri çalıştırmak için Pig komutu kullanmayı öğrenin."
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
ms.openlocfilehash: 5e8d4fbd8afc54c8bbc1a9a71c66d7022a7d5986
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="run-pig-jobs-from-a-remote-desktop-connection"></a><span data-ttu-id="21c84-103">Uzak Masaüstü bağlantısı üzerinden pig işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="21c84-103">Run Pig jobs from a Remote Desktop connection</span></span>
[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="21c84-104">Bu belge, Pig Latin deyimleri Windows tabanlı Hdınsight kümesi için bir Uzak Masaüstü bağlantısı üzerinden çalıştırmak için Pig komutunu kullanarak bir kılavuz sağlar.</span><span class="sxs-lookup"><span data-stu-id="21c84-104">This document provides a walkthrough for using the Pig command to run Pig Latin statements from a Remote Desktop connection to a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="21c84-105">Pig Latin veri dönüşümleri açıklayarak MapReduce uygulamalar oluşturmak yerine eşleme ve İşlevler azaltmak sağlar.</span><span class="sxs-lookup"><span data-stu-id="21c84-105">Pig Latin allows you to create MapReduce applications by describing data transformations, rather than map and reduce functions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="21c84-106">Uzak Masaüstü, Windows işletim sistemi olarak kullanma Hdınsight kümelerinde yalnızca kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="21c84-106">Remote Desktop is only available on HDInsight clusters that use Windows as the operating system.</span></span> <span data-ttu-id="21c84-107">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="21c84-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="21c84-108">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="21c84-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="21c84-109">Hdınsight 3.4 veya büyük, bkz [Hdınsight ve SSH ile Pig kullanma](hdinsight-hadoop-use-pig-ssh.md) Pig işleri doğrudan kümede bir komut satırından çalıştırma etkileşimli olarak hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="21c84-109">For HDInsight 3.4 or greater, see [Use Pig with HDInsight and SSH](hdinsight-hadoop-use-pig-ssh.md) for information on interactively running Pig jobs directly on the cluster from a command-line.</span></span>

## <span data-ttu-id="21c84-110"><a id="prereq"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="21c84-110"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="21c84-111">Bu makaledeki adımları tamamlamak için aşağıdakiler gerekir.</span><span class="sxs-lookup"><span data-stu-id="21c84-111">To complete the steps in this article, you will need the following.</span></span>

* <span data-ttu-id="21c84-112">Bir Windows tabanlı Hdınsight (Hadoop hdınsight) kümesi</span><span class="sxs-lookup"><span data-stu-id="21c84-112">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="21c84-113">Windows 10, Windows 8 veya Windows 7 çalıştıran bir istemci bilgisayar</span><span class="sxs-lookup"><span data-stu-id="21c84-113">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="21c84-114"><a id="connect"></a>İle Uzak Masaüstü Bağlantısı</span><span class="sxs-lookup"><span data-stu-id="21c84-114"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="21c84-115">Hdınsight kümesi için Uzak Masaüstü'nü etkinleştirin ve ardından yönergeleri izleyerek bağlanmak [RDP kullanarak Hdınsight kümelerini Bağlan](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="21c84-115">Enable Remote Desktop for the HDInsight cluster, then connect to it by following the instructions at [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="21c84-116"><a id="pig"></a>Pig komutunu kullanın</span><span class="sxs-lookup"><span data-stu-id="21c84-116"><a id="pig"></a>Use the Pig command</span></span>
1. <span data-ttu-id="21c84-117">Uzak Masaüstü bağlantı kurduktan sonra Başlangıç **Hadoop komut satırı** masaüstünde simgesini kullanarak.</span><span class="sxs-lookup"><span data-stu-id="21c84-117">After you have a Remote Desktop connection, start the **Hadoop Command Line** by using the icon on the desktop.</span></span>
2. <span data-ttu-id="21c84-118">Pig komutu başlatmak için aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="21c84-118">Use the following to start the Pig command:</span></span>

        %pig_home%\bin\pig

    <span data-ttu-id="21c84-119">İle sunulur bir `grunt>` istemi.</span><span class="sxs-lookup"><span data-stu-id="21c84-119">You will be presented with a `grunt>` prompt.</span></span>
3. <span data-ttu-id="21c84-120">Aşağıdaki deyimi girin:</span><span class="sxs-lookup"><span data-stu-id="21c84-120">Enter the following statement:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';

    <span data-ttu-id="21c84-121">Bu komut sample.log dosyasının içeriğini GÜNLÜKLERİ dosyasına yükler.</span><span class="sxs-lookup"><span data-stu-id="21c84-121">This command loads the contents of the sample.log file into the LOGS file.</span></span> <span data-ttu-id="21c84-122">Aşağıdaki komutu kullanarak dosyanın içeriğini görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="21c84-122">You can view the contents of the file by using the following command:</span></span>

        DUMP LOGS;
4. <span data-ttu-id="21c84-123">Verileri yalnızca günlüğe kaydetme düzeyi her kayıttan ayıklamak için normal bir ifade uygulayarak dönüştürün:</span><span class="sxs-lookup"><span data-stu-id="21c84-123">Transform the data by applying a regular expression to extract only the logging level from each record:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="21c84-124">Kullanabileceğiniz **dökümü** dönüştürme işleminin ardından verileri görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="21c84-124">You can use **DUMP** to view the data after the transformation.</span></span> <span data-ttu-id="21c84-125">Bu durumda, `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="21c84-125">In this case, `DUMP LEVELS;`.</span></span>
5. <span data-ttu-id="21c84-126">Aşağıdaki deyim kullanarak dönüşümleri uygulama devam edin.</span><span class="sxs-lookup"><span data-stu-id="21c84-126">Continue applying transformations by using the following statements.</span></span> <span data-ttu-id="21c84-127">Kullanım `DUMP` her adımından sonra dönüşümünün sonucu görüntülemek için.</span><span class="sxs-lookup"><span data-stu-id="21c84-127">Use `DUMP` to view the result of the transformation after each step.</span></span>

    <table>
    <tr>
    <th><span data-ttu-id="21c84-128">Deyimi</span><span class="sxs-lookup"><span data-stu-id="21c84-128">Statement</span></span></th><th><span data-ttu-id="21c84-129">Neler yapar?</span><span class="sxs-lookup"><span data-stu-id="21c84-129">What it does</span></span></th>
    </tr>
    <tr>
    <td><span data-ttu-id="21c84-130">FILTEREDLEVELS = LOGLEVEL FİLTRE DÜZEYLERİYLE null; değil</span><span class="sxs-lookup"><span data-stu-id="21c84-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span></span></td><td><span data-ttu-id="21c84-131">Günlük düzeyini null değerini içeren satırları kaldırır ve sonuçları FILTEREDLEVELS depolar.</span><span class="sxs-lookup"><span data-stu-id="21c84-131">Removes rows that contain a null value for the log level and stores the results into FILTEREDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="21c84-132">GROUPEDLEVELS Grup FILTEREDLEVELS LOGLEVEL tarafından; =</span><span class="sxs-lookup"><span data-stu-id="21c84-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span></span></td><td><span data-ttu-id="21c84-133">Günlük düzeyi satır grupları ve sonuçları GROUPEDLEVELS depolar.</span><span class="sxs-lookup"><span data-stu-id="21c84-133">Groups the rows by log level and stores the results into GROUPEDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="21c84-134">Sıklık foreach = GROUPEDLEVELS sayısı (FILTEREDLEVELS LOGLEVEL Grup Oluştur. LOGLEVEL) sayısı gibi;</span><span class="sxs-lookup"><span data-stu-id="21c84-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span></span></td><td><span data-ttu-id="21c84-135">Yeni bir küme oluşturur her benzersiz günlük içeren verilerin düzeyi değeri ve kaç kez oluşur.</span><span class="sxs-lookup"><span data-stu-id="21c84-135">Creates a new set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="21c84-136">Bu SIKLIKLARINI depolanır</span><span class="sxs-lookup"><span data-stu-id="21c84-136">This is stored into FREQUENCIES</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="21c84-137">Sonuç order SIKLIĞI sayısı desc tarafından; =</span><span class="sxs-lookup"><span data-stu-id="21c84-137">RESULT = order FREQUENCIES by COUNT desc;</span></span></td><td><span data-ttu-id="21c84-138">Günlük düzeyleri (Azalan) sayısına göre sıralar ve sonucu depolar</span><span class="sxs-lookup"><span data-stu-id="21c84-138">Orders the log levels by count (descending,) and stores into RESULT</span></span></td>
    </tr>
    </table><span data-ttu-id="21c84-139">
6.Kullanarak bir dönüşüm sonuçları kaydedebilirsiniz `STORE` deyimi.</span><span class="sxs-lookup"><span data-stu-id="21c84-139">
6. You can also save the results of a transformation by using the `STORE` statement.</span></span> <span data-ttu-id="21c84-140">Örneğin, aşağıdaki kaydeder komut `RESULT` için **/example/data/pigout** kümeniz için varsayılan depolama kapsayıcısında dizin:</span><span class="sxs-lookup"><span data-stu-id="21c84-140">For example, the following command saves the `RESULT` to the **/example/data/pigout** directory in the default storage container for your cluster:</span></span>

        STORE RESULT into 'wasb:///example/data/pigout'

   > [!NOTE]
   > <span data-ttu-id="21c84-141">Veri adlı dosyaları belirtilen dizinde depolanır **bölümü nnnnn**.</span><span class="sxs-lookup"><span data-stu-id="21c84-141">The data is stored in the specified directory in files named **part-nnnnn**.</span></span> <span data-ttu-id="21c84-142">Dizini zaten varsa, bir hata iletisi alırsınız.</span><span class="sxs-lookup"><span data-stu-id="21c84-142">If the directory already exists, you will receive an error message.</span></span>
   >
   >
7. <span data-ttu-id="21c84-143">Grunt istemi çıkmak için şu deyimi girin.</span><span class="sxs-lookup"><span data-stu-id="21c84-143">To exit the grunt prompt, enter the following statement.</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="21c84-144">Pig Latin toplu iş dosyaları</span><span class="sxs-lookup"><span data-stu-id="21c84-144">Pig Latin batch files</span></span>
<span data-ttu-id="21c84-145">Pig komutu, bir dosyada yer alan Pig Latin çalıştırmak için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21c84-145">You can also use the Pig command to run Pig Latin that is contained in a file.</span></span>

1. <span data-ttu-id="21c84-146">Grunt istemi çıktıktan sonra açmak **not defteri** ve adlı yeni bir dosya oluşturun **pigbatch.pig** içinde **PIG_HOME %** dizin.</span><span class="sxs-lookup"><span data-stu-id="21c84-146">After exiting the grunt prompt, open **Notepad** and create a new file named **pigbatch.pig** in the **%PIG_HOME%** directory.</span></span>
2. <span data-ttu-id="21c84-147">Yazın veya yapıştırın içine aşağıdaki satırları **pigbatch.pig** dosya ve dosyayı kaydedin:</span><span class="sxs-lookup"><span data-stu-id="21c84-147">Type or paste the following lines into the **pigbatch.pig** file, and then save it:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;
3. <span data-ttu-id="21c84-148">Çalıştırmak için aşağıdakileri kullanın **pigbatch.pig** pig komutunu kullanarak dosya.</span><span class="sxs-lookup"><span data-stu-id="21c84-148">Use the following to run the **pigbatch.pig** file using the pig command.</span></span>

        pig %PIG_HOME%\pigbatch.pig

    <span data-ttu-id="21c84-149">Toplu işlem tamamlandığında kullanıldığında, aynı olmalıdır aşağıdaki çıktı görmeniz gerekir `DUMP RESULT;` , önceki adımlarda:</span><span class="sxs-lookup"><span data-stu-id="21c84-149">When the batch job completes, you should see the following output, which should be the same as when you used `DUMP RESULT;` in the previous steps:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="21c84-150"><a id="summary"></a>Özet</span><span class="sxs-lookup"><span data-stu-id="21c84-150"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="21c84-151">Gördüğünüz gibi Pig komutu etkileşimli olarak MapReduce işlemleri çalıştırın veya bir toplu iş dosyasında depolanan Pig Latin işleri çalıştırma olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="21c84-151">As you can see, the Pig command allows you to interactively run MapReduce operations, or run Pig Latin jobs that are stored in a batch file.</span></span>

## <span data-ttu-id="21c84-152"><a id="nextsteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="21c84-152"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="21c84-153">Hdınsight'ta Pig hakkında genel bilgi için:</span><span class="sxs-lookup"><span data-stu-id="21c84-153">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="21c84-154">Hdınsight'ta Hadoop ile pig kullanma</span><span class="sxs-lookup"><span data-stu-id="21c84-154">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="21c84-155">Diğer yolları hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="21c84-155">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="21c84-156">Hdınsight'ta Hadoop ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="21c84-156">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="21c84-157">Hdınsight'ta Hadoop ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="21c84-157">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
