---
title: "Hdınsight kümesinde - Azure SSH ile Hadoop Pig aaaUse | Microsoft Docs"
description: "Bilgi tooa Linux tabanlı Hadoop kümesi SSH ile nasıl bağlanacağını ve ardından kullanımı hello Pig komutu toorun Pig Latin deyimleri etkileşimli olarak veya toplu olarak iş."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b646a93b-4c51-4ba4-84da-3275d9124ebe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 1da303e239b537e6b331b1d33010058582718c90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-on-a-linux-based-cluster-with-hello-pig-command-ssh"></a><span data-ttu-id="9016a-103">Merhaba Pig komutu (SSH) ile Linux tabanlı kümesi pig işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="9016a-103">Run Pig jobs on a Linux-based cluster with hello Pig command (SSH)</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="9016a-104">Toointeractively çalışma şeklini Pig işleri SSH bağlantı tooyour Hdınsight kümesi hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="9016a-104">Learn how toointeractively run Pig jobs from an SSH connection tooyour HDInsight cluster.</span></span> <span data-ttu-id="9016a-105">Merhaba Pig Latin programlama diline uygulanan toohello giriş veri tooproduce hello istenen çıkış toodescribe dönüşümleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="9016a-105">hello Pig Latin programming language allows you toodescribe transformations that are applied toohello input data tooproduce hello desired output.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9016a-106">Merhaba bu belgedeki adımlar Linux tabanlı Hdınsight kümesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="9016a-106">hello steps in this document require a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="9016a-107">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="9016a-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9016a-108">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="9016a-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="9016a-109"><a id="ssh"></a>SSH ile bağlanma</span><span class="sxs-lookup"><span data-stu-id="9016a-109"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="9016a-110">SSH tooconnect tooyour Hdınsight kümesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="9016a-110">Use SSH tooconnect tooyour HDInsight cluster.</span></span> <span data-ttu-id="9016a-111">Merhaba aşağıdaki örnek bağlayan adlı tooa küme **myhdinsight** adlı hello hesabı olarak **sshuser**:</span><span class="sxs-lookup"><span data-stu-id="9016a-111">hello following example connects tooa cluster named **myhdinsight** as hello account named **sshuser**:</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net

<span data-ttu-id="9016a-112">**SSH kimlik doğrulaması için bir sertifika anahtarı sağladıysanız** hello Hdınsight kümesi oluştururken, istemci sisteminizde toospecify hello hello özel anahtarın konumunu gerekebilir.</span><span class="sxs-lookup"><span data-stu-id="9016a-112">**If you provided a certificate key for SSH authentication** when you created hello HDInsight cluster, you may need toospecify hello location of hello private key on your client system.</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net -i ~/mykey.key

<span data-ttu-id="9016a-113">**SSH kimlik doğrulaması için parola sağladıysanız** hello Hdınsight kümesi oluşturduğunuzda, istendiğinde hello parolasını sağlayın.</span><span class="sxs-lookup"><span data-stu-id="9016a-113">**If you provided a password for SSH authentication** when you created hello HDInsight cluster, provide hello password when prompted.</span></span>

<span data-ttu-id="9016a-114">Hdınsight ile SSH kullanma hakkında daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="9016a-114">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="9016a-115"><a id="pig"></a>Merhaba Pig komutunu kullanın</span><span class="sxs-lookup"><span data-stu-id="9016a-115"><a id="pig"></a>Use hello Pig command</span></span>

1. <span data-ttu-id="9016a-116">Bağlantı kurulduktan sonra komutu aşağıdaki hello kullanarak hello Pig komut satırı arabirimi (CLI) başlatın:</span><span class="sxs-lookup"><span data-stu-id="9016a-116">Once connected, start hello Pig command-line interface (CLI) by using hello following command:</span></span>

        pig

    <span data-ttu-id="9016a-117">Bir süre sonra görmelisiniz bir `grunt>` istemi.</span><span class="sxs-lookup"><span data-stu-id="9016a-117">After a moment, you should see a `grunt>` prompt.</span></span>

2. <span data-ttu-id="9016a-118">Aşağıdaki ifadeyi hello girin:</span><span class="sxs-lookup"><span data-stu-id="9016a-118">Enter hello following statement:</span></span>

        LOGS = LOAD '/example/data/sample.log';

    <span data-ttu-id="9016a-119">Bu komut, oturum AÇTIĞI hello sample.log dosyasının Merhaba içeriğine yükler.</span><span class="sxs-lookup"><span data-stu-id="9016a-119">This command loads hello contents of hello sample.log file into LOGS.</span></span> <span data-ttu-id="9016a-120">Aşağıdaki ifadeyi hello kullanarak hello dosyasının Merhaba içeriğine görüntüleyebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9016a-120">You can view hello contents of hello file by using hello following statement:</span></span>

        DUMP LOGS;

3. <span data-ttu-id="9016a-121">Ardından, aşağıdaki ifadeyi hello kullanarak bir normal ifade tooextract yalnızca hello günlük düzeyi her kayıttan uygulayarak hello verileri dönüştürün:</span><span class="sxs-lookup"><span data-stu-id="9016a-121">Next, transform hello data by applying a regular expression tooextract only hello logging level from each record by using hello following statement:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="9016a-122">Kullanabileceğiniz **dökümü** tooview hello veri hello dönüştürme sonra.</span><span class="sxs-lookup"><span data-stu-id="9016a-122">You can use **DUMP** tooview hello data after hello transformation.</span></span> <span data-ttu-id="9016a-123">Bu durumda, kullanarak `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="9016a-123">In this case, use `DUMP LEVELS;`.</span></span>

4. <span data-ttu-id="9016a-124">Aşağıdaki tablonun hello hello deyimleri kullanarak dönüşümleri uygulama devam edin:</span><span class="sxs-lookup"><span data-stu-id="9016a-124">Continue applying transformations by using hello statements in hello following table:</span></span>

    | <span data-ttu-id="9016a-125">Pig Latin deyimi</span><span class="sxs-lookup"><span data-stu-id="9016a-125">Pig Latin statement</span></span> | <span data-ttu-id="9016a-126">Hangi hello deyimi mu</span><span class="sxs-lookup"><span data-stu-id="9016a-126">What hello statement does</span></span> |
    | ---- | ---- |
    | `FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;` | <span data-ttu-id="9016a-127">Merhaba günlük düzeyi null değerini içeren satırları kaldırır ve hello sonuçları içine depolar `FILTEREDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="9016a-127">Removes rows that contain a null value for hello log level and stores hello results into `FILTEREDLEVELS`.</span></span> |
    | `GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;` | <span data-ttu-id="9016a-128">Grupları hello satırları Günlük düzeyi tarafından ve hello sonuçları içine depolar `GROUPEDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="9016a-128">Groups hello rows by log level and stores hello results into `GROUPEDLEVELS`.</span></span> |
    | `FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;` | <span data-ttu-id="9016a-129">Bir küme oluşturur her benzersiz günlük içeren verilerin düzeyi değeri ve kaç kez oluşur.</span><span class="sxs-lookup"><span data-stu-id="9016a-129">Creates a set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="9016a-130">Merhaba veri kümesi içine depolanır `FREQUENCIES`.</span><span class="sxs-lookup"><span data-stu-id="9016a-130">hello data set is stored into `FREQUENCIES`.</span></span> |
    | `RESULT = order FREQUENCIES by COUNT desc;` | <span data-ttu-id="9016a-131">Merhaba günlük düzeyleri (Azalan) sayısına göre sıralar ve içine depolar `RESULT`.</span><span class="sxs-lookup"><span data-stu-id="9016a-131">Orders hello log levels by count (descending) and stores into `RESULT`.</span></span> |

    > [!TIP]
    > <span data-ttu-id="9016a-132">Kullanım `DUMP` her adımından sonra hello dönüşümünün tooview hello sonucu.</span><span class="sxs-lookup"><span data-stu-id="9016a-132">Use `DUMP` tooview hello result of hello transformation after each step.</span></span>

5. <span data-ttu-id="9016a-133">Hello kullanarak bir dönüşüm hello sonuçlarını da kaydedebilirsiniz `STORE` deyimi.</span><span class="sxs-lookup"><span data-stu-id="9016a-133">You can also save hello results of a transformation by using hello `STORE` statement.</span></span> <span data-ttu-id="9016a-134">Örneğin, aşağıdaki ifadeyi hello hello kaydeder `RESULT` toohello `/example/data/pigout` hello varsayılan depolama kümeniz için dizin:</span><span class="sxs-lookup"><span data-stu-id="9016a-134">For example, hello following statement saves hello `RESULT` toohello `/example/data/pigout` directory on hello default storage for your cluster:</span></span>

        STORE RESULT into '/example/data/pigout';

   > [!NOTE]
   > <span data-ttu-id="9016a-135">Merhaba veri hello adlı dosyaları belirtilen dizinde depolanır `part-nnnnn`.</span><span class="sxs-lookup"><span data-stu-id="9016a-135">hello data is stored in hello specified directory in files named `part-nnnnn`.</span></span> <span data-ttu-id="9016a-136">Merhaba dizini zaten varsa, bir hata alırsınız.</span><span class="sxs-lookup"><span data-stu-id="9016a-136">If hello directory already exists, you receive an error.</span></span>

6. <span data-ttu-id="9016a-137">tooexit hello grunt komut isteminde, aşağıdaki ifadeyi hello girin:</span><span class="sxs-lookup"><span data-stu-id="9016a-137">tooexit hello grunt prompt, enter hello following statement:</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="9016a-138">Pig Latin toplu iş dosyaları</span><span class="sxs-lookup"><span data-stu-id="9016a-138">Pig Latin batch files</span></span>

<span data-ttu-id="9016a-139">Merhaba Pig komutu toorun Pig Latin bir dosyada yer alan de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9016a-139">You can also use hello Pig command toorun Pig Latin contained in a file.</span></span>

1. <span data-ttu-id="9016a-140">Merhaba grunt istemi çıktıktan sonra kullanım hello şu komutu toopipe STDIN adlı bir dosyaya `pigbatch.pig`.</span><span class="sxs-lookup"><span data-stu-id="9016a-140">After exiting hello grunt prompt, use hello following command toopipe STDIN into a file named `pigbatch.pig`.</span></span> <span data-ttu-id="9016a-141">Bu dosya hello hello SSH kullanıcı hesabı için giriş dizini oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="9016a-141">This file is created in hello home directory for hello SSH user account.</span></span>

        cat > ~/pigbatch.pig

2. <span data-ttu-id="9016a-142">Yazın veya satırlardan hello yapıştırın ve sonra Ctrl + D bittiğinde kullanın.</span><span class="sxs-lookup"><span data-stu-id="9016a-142">Type or paste hello following lines, and then use Ctrl+D when finished.</span></span>

        LOGS = LOAD '/example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;

3. <span data-ttu-id="9016a-143">Kullanım hello şu komutu toorun hello `pigbatch.pig` hello Pig komutunu kullanarak dosya.</span><span class="sxs-lookup"><span data-stu-id="9016a-143">Use hello following command toorun hello `pigbatch.pig` file by using hello Pig command.</span></span>

        pig ~/pigbatch.pig

    <span data-ttu-id="9016a-144">Merhaba toplu işi tamamlandıktan sonra çıktı aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="9016a-144">Once hello batch job finishes, you see hello following output:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)


## <span data-ttu-id="9016a-145"><a id="nextsteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9016a-145"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="9016a-146">Hdınsight'ta Pig hakkında genel bilgi için belge aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="9016a-146">For general information on Pig in HDInsight, see hello following document:</span></span>

* [<span data-ttu-id="9016a-147">Hdınsight'ta Hadoop ile pig kullanma</span><span class="sxs-lookup"><span data-stu-id="9016a-147">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="9016a-148">Hdınsight'ta Hadoop ile diğer yolları toowork hakkında daha fazla bilgi için aşağıdaki belgeleri hello bakın:</span><span class="sxs-lookup"><span data-stu-id="9016a-148">For more information on other ways toowork with Hadoop on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="9016a-149">Hdınsight'ta Hadoop ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="9016a-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="9016a-150">Hdınsight'ta Hadoop ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="9016a-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
