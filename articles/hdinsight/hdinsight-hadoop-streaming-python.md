---
title: "aaaDevelop MapReduce akış Python işleri Hdınsight - Azure | Microsoft Docs"
description: "Bilgi nasıl MapReduce işleri akış Python toouse. Hadoop, Java dışındaki dillerde yazmak için MapReduce için akış bir API sağlar."
services: hdinsight
keyword: mapreduce python,python map reduce,python mapreduce
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7631d8d9-98ae-42ec-b9ec-ee3cf7e57fb3
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: a6ae3ba650b665ecc5839a4ddf5282f8ccfb6bd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-python-streaming-mapreduce-programs-for-hdinsight"></a><span data-ttu-id="b9229-104">MapReduce programları Hdınsight için akış Python geliştirme</span><span class="sxs-lookup"><span data-stu-id="b9229-104">Develop Python streaming MapReduce programs for HDInsight</span></span>

<span data-ttu-id="b9229-105">Bilgi nasıl MapReduce işlemleri akış Python toouse.</span><span class="sxs-lookup"><span data-stu-id="b9229-105">Learn how toouse Python in streaming MapReduce operations.</span></span> <span data-ttu-id="b9229-106">Hadoop, toowrite harita sağlayan ve Java dışındaki dillerde işlevleri azaltmak MapReduce akış bir API sağlar.</span><span class="sxs-lookup"><span data-stu-id="b9229-106">Hadoop provides a streaming API for MapReduce that enables you toowrite map and reduce functions in languages other than Java.</span></span> <span data-ttu-id="b9229-107">Merhaba bu belgedeki adımları hello eşleme uygulamak ve Python bileşenlerinde azaltır.</span><span class="sxs-lookup"><span data-stu-id="b9229-107">hello steps in this document implement hello Map and Reduce components in Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9229-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="b9229-108">Prerequisites</span></span>

* <span data-ttu-id="b9229-109">Bir Hdınsight kümesinde Linux tabanlı Hadoop</span><span class="sxs-lookup"><span data-stu-id="b9229-109">A Linux-based Hadoop on HDInsight cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="b9229-110">Bu belgedeki Hello adımlar Linux kullanan bir Hdınsight kümesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="b9229-110">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="b9229-111">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="b9229-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b9229-112">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="b9229-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="b9229-113">Bir metin düzenleyicisi</span><span class="sxs-lookup"><span data-stu-id="b9229-113">A text editor</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="b9229-114">Merhaba metin düzenleyicisi LF hello satır bitiş olarak kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b9229-114">hello text editor must use LF as hello line ending.</span></span> <span data-ttu-id="b9229-115">CRLF satır sonu kullanarak hataları hello MapReduce işi Linux tabanlı Hdınsight kümelerinde çalıştırırken neden olur.</span><span class="sxs-lookup"><span data-stu-id="b9229-115">Using a line ending of CRLF causes errors when running hello MapReduce job on Linux-based HDInsight clusters.</span></span>

* <span data-ttu-id="b9229-116">Merhaba `ssh` ve `scp` komutları veya [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span><span class="sxs-lookup"><span data-stu-id="b9229-116">hello `ssh` and `scp` commands, or [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span></span>

## <a name="word-count"></a><span data-ttu-id="b9229-117">Sözcük Sayımı</span><span class="sxs-lookup"><span data-stu-id="b9229-117">Word count</span></span>

<span data-ttu-id="b9229-118">Bu temel sözcük sayımı bir python Eşleyici ve reducer uygulanan bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="b9229-118">This example is a basic word count implemented in a python a mapper and reducer.</span></span> <span data-ttu-id="b9229-119">Merhaba Eşleyici cümleleri tek tek sözcüklere böler ve hello reducer hello sözcükler toplar ve tooproduce hello çıkış sayar.</span><span class="sxs-lookup"><span data-stu-id="b9229-119">hello mapper breaks sentences into individual words, and hello reducer aggregates hello words and counts tooproduce hello output.</span></span>

<span data-ttu-id="b9229-120">Aşağıdaki akış çizelgesi hello ne hello eşleme sırasında olur ve aşamaları azaltmak gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="b9229-120">hello following flowchart illustrates what happens during hello map and reduce phases.</span></span>

![Merhaba mapreduce işlem çizimi](./media/hdinsight-hadoop-streaming-python/HDI.WordCountDiagram.png)

## <a name="streaming-mapreduce"></a><span data-ttu-id="b9229-122">Akış MapReduce</span><span class="sxs-lookup"><span data-stu-id="b9229-122">Streaming MapReduce</span></span>

<span data-ttu-id="b9229-123">Hadoop toospecify hello eşlemesini içerir ve bir iş tarafından kullanılan mantığı azaltmak bir dosyayı sağlar.</span><span class="sxs-lookup"><span data-stu-id="b9229-123">Hadoop allows you toospecify a file that contains hello map and reduce logic that is used by a job.</span></span> <span data-ttu-id="b9229-124">hello için belirli gereksinimler Hello harita ve mantığı azaltmak şunlardır:</span><span class="sxs-lookup"><span data-stu-id="b9229-124">hello specific requirements for hello map and reduce logic are:</span></span>

* <span data-ttu-id="b9229-125">**Giriş**: Merhaba eşleme ve azaltma bileşenleri STDIN giriş verilerinin okuma gerekir.</span><span class="sxs-lookup"><span data-stu-id="b9229-125">**Input**: hello map and reduce components must read input data from STDIN.</span></span>
* <span data-ttu-id="b9229-126">**Çıktı**: Merhaba eşleme ve azaltma bileşenleri çıkış veri tooSTDOUT yazmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b9229-126">**Output**: hello map and reduce components must write output data tooSTDOUT.</span></span>
* <span data-ttu-id="b9229-127">**Veri biçimi**: tüketilen ve üretilen hello veri sekmesi karakteriyle ayrılmış bir anahtar/değer çifti olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="b9229-127">**Data format**: hello data consumed and produced must be a key/value pair, separated by a tab character.</span></span>

<span data-ttu-id="b9229-128">Python kolayca işleyebilir bu gereksinimleri hello kullanarak `sys` STDIN ve kullanarak modülü tooread `print` tooprint tooSTDOUT.</span><span class="sxs-lookup"><span data-stu-id="b9229-128">Python can easily handle these requirements by using hello `sys` module tooread from STDIN and using `print` tooprint tooSTDOUT.</span></span> <span data-ttu-id="b9229-129">Merhaba kalan görev yalnızca bir sekme hello verilerle biçimlendirme (`\t`) hello anahtar ve değer arasında karakter.</span><span class="sxs-lookup"><span data-stu-id="b9229-129">hello remaining task is simply formatting hello data with a tab (`\t`) character between hello key and value.</span></span>

## <a name="create-hello-mapper-and-reducer"></a><span data-ttu-id="b9229-130">Merhaba Eşleyici ve reducer oluşturma</span><span class="sxs-lookup"><span data-stu-id="b9229-130">Create hello mapper and reducer</span></span>

1. <span data-ttu-id="b9229-131">Adlı bir dosya oluşturun `mapper.py` ve kullanım hello aşağıdaki kodu hello içerik olarak:</span><span class="sxs-lookup"><span data-stu-id="b9229-131">Create a file named `mapper.py` and use hello following code as hello content:</span></span>

   ```python
   #!/usr/bin/env python

   # Use hello sys module
   import sys

   # 'file' in this case is STDIN
   def read_input(file):
       # Split each line into words
       for line in file:
           yield line.split()

   def main(separator='\t'):
       # Read hello data using read_input
       data = read_input(sys.stdin)
       # Process each word returned from read_input
       for words in data:
           # Process each word
           for word in words:
               # Write tooSTDOUT
               print '%s%s%d' % (word, separator, 1)

   if __name__ == "__main__":
       main()
   ```

2. <span data-ttu-id="b9229-132">Adlı bir dosya oluşturun **reducer.py** ve kullanım hello aşağıdaki kodu hello içerik olarak:</span><span class="sxs-lookup"><span data-stu-id="b9229-132">Create a file named **reducer.py** and use hello following code as hello content:</span></span>

   ```python
   #!/usr/bin/env python

   # import modules
   from itertools import groupby
   from operator import itemgetter
   import sys

   # 'file' in this case is STDIN
   def read_mapper_output(file, separator='\t'):
       # Go through each line
       for line in file:
           # Strip out hello separator character
           yield line.rstrip().split(separator, 1)

   def main(separator='\t'):
       # Read hello data using read_mapper_output
       data = read_mapper_output(sys.stdin, separator=separator)
       # Group words and counts into 'group'
       #   Since MapReduce is a distributed process, each word
       #   may have multiple counts. 'group' will have all counts
       #   which can be retrieved using hello word as hello key.
       for current_word, group in groupby(data, itemgetter(0)):
           try:
               # For each word, pull hello count(s) for hello word
               #   from 'group' and create a total count
               total_count = sum(int(count) for current_word, count in group)
               # Write toostdout
               print "%s%s%d" % (current_word, separator, total_count)
           except ValueError:
               # Count was not a number, so do nothing
               pass

   if __name__ == "__main__":
       main()
   ```

## <a name="run-using-powershell"></a><span data-ttu-id="b9229-133">PowerShell kullanarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="b9229-133">Run using PowerShell</span></span>

<span data-ttu-id="b9229-134">PowerShell Betiği aşağıdaki kullanım hello dosyalarınızı hello sağ satır sonları sahip tooensure:</span><span class="sxs-lookup"><span data-stu-id="b9229-134">tooensure that your files have hello right line endings, use hello following PowerShell script:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]

<span data-ttu-id="b9229-135">Aşağıdaki PowerShell komut dosyası tooupload hello dosyaları hello kullanın, hello işini çalıştırın ve hello çıktısını görüntüleyin:</span><span class="sxs-lookup"><span data-stu-id="b9229-135">Use hello following PowerShell script tooupload hello files, run hello job, and view hello output:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]

## <a name="run-from-an-ssh-session"></a><span data-ttu-id="b9229-136">Bir SSH oturumunda</span><span class="sxs-lookup"><span data-stu-id="b9229-136">Run from an SSH session</span></span>

1. <span data-ttu-id="b9229-137">Aynı içinde geliştirme ortamınızdan hello olarak dizin `mapper.py` ve `reducer.py` dosyaları, komut aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="b9229-137">From your development environment, in hello same directory as `mapper.py` and `reducer.py` files, use hello following command:</span></span>

    ```bash
    scp mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="b9229-138">Değiştir `username` hello SSH kullanıcı adı, kümeniz için ve `clustername` kümenizin hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="b9229-138">Replace `username` with hello SSH user name for your cluster, and `clustername` with hello name of your cluster.</span></span>

    <span data-ttu-id="b9229-139">Bu komut hello yerel sistem toohello baş düğümünden hello dosyalarını kopyalar.</span><span class="sxs-lookup"><span data-stu-id="b9229-139">This command copies hello files from hello local system toohello head node.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b9229-140">SSH hesabınızın parolası toosecure kullandıysanız, hello parolası istenir.</span><span class="sxs-lookup"><span data-stu-id="b9229-140">If you used a password toosecure your SSH account, you are prompted for hello password.</span></span> <span data-ttu-id="b9229-141">Bir SSH anahtarı kullandıysanız, toouse hello olabilir `-i` parametre ve hello yolu toohello özel anahtarı.</span><span class="sxs-lookup"><span data-stu-id="b9229-141">If you used an SSH key, you may have toouse hello `-i` parameter and hello path toohello private key.</span></span> <span data-ttu-id="b9229-142">Örneğin, `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="b9229-142">For example, `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="b9229-143">SSH kullanarak toohello kümesine bağlanın:</span><span class="sxs-lookup"><span data-stu-id="b9229-143">Connect toohello cluster by using SSH:</span></span>

    ```bash
    ssh username@clustername-ssh.azurehdinsight.net`
    ```

    <span data-ttu-id="b9229-144">Daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="b9229-144">For more information on, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="b9229-145">satır sonları düzeltin, komutları aşağıdaki hello kullan hello tooensure hello mapper.py ve reducer.py vardır:</span><span class="sxs-lookup"><span data-stu-id="b9229-145">tooensure hello mapper.py and reducer.py have hello correct line endings, use hello following commands:</span></span>

    ```bash
    perl -pi -e 's/\r\n/\n/g' mapper.py
    perl -pi -e 's/\r\n/\n/g' reducer.py
    ```

4. <span data-ttu-id="b9229-146">Komut toostart hello MapReduce işi aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="b9229-146">Use hello following command toostart hello MapReduce job.</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files mapper.py,reducer.py -mapper mapper.py -reducer reducer.py -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
    ```

    <span data-ttu-id="b9229-147">Bu komut hello aşağıdaki bölümleri içerir:</span><span class="sxs-lookup"><span data-stu-id="b9229-147">This command has hello following parts:</span></span>

   * <span data-ttu-id="b9229-148">**hadoop streaming.jar**: akış MapReduce işlemleri yaparken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="b9229-148">**hadoop-streaming.jar**: Used when performing streaming MapReduce operations.</span></span> <span data-ttu-id="b9229-149">Bu Hadoop sağladığınız hello dış MapReduce koduyla arabirimleri.</span><span class="sxs-lookup"><span data-stu-id="b9229-149">It interfaces Hadoop with hello external MapReduce code you provide.</span></span>

   * <span data-ttu-id="b9229-150">**-dosyaları**: Belirtilen hello ekler dosyaları toohello MapReduce işi.</span><span class="sxs-lookup"><span data-stu-id="b9229-150">**-files**: Adds hello specified files toohello MapReduce job.</span></span>

   * <span data-ttu-id="b9229-151">**-Eşleyici**: söyler, toouse Eşleyici hello gibi dosya Hadoop.</span><span class="sxs-lookup"><span data-stu-id="b9229-151">**-mapper**: Tells Hadoop which file toouse as hello mapper.</span></span>

   * <span data-ttu-id="b9229-152">**-reducer**: söyler, toouse reducer hello gibi dosya Hadoop.</span><span class="sxs-lookup"><span data-stu-id="b9229-152">**-reducer**: Tells Hadoop which file toouse as hello reducer.</span></span>

   * <span data-ttu-id="b9229-153">**-Giriş**: güvenmemeniz gerekir hello giriş dosyası sözcükleri.</span><span class="sxs-lookup"><span data-stu-id="b9229-153">**-input**: hello input file that we should count words from.</span></span>

   * <span data-ttu-id="b9229-154">**-Çıktı**: çıktı hello hello dizin yazılır.</span><span class="sxs-lookup"><span data-stu-id="b9229-154">**-output**: hello directory that hello output is written to.</span></span>

    <span data-ttu-id="b9229-155">Merhaba MapReduce işi çalışıyor gibi hello işlem yüzde olarak görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="b9229-155">As hello MapReduce job works, hello process is displayed as percentages.</span></span>

        <span data-ttu-id="b9229-156">02/15/05 19:01:04 bilgisi mapreduce. İş: eşleme %0 azaltmak %0 02/15/05 19:01:16 bilgisi mapreduce. İş: % 0 harita % 100 azaltmak 02/15/05 19:01:27 bilgisi mapreduce. İş: eşleme % %100 100 azaltın.</span><span class="sxs-lookup"><span data-stu-id="b9229-156">15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%</span></span>


5. <span data-ttu-id="b9229-157">tooview hello çıkışı, komutu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="b9229-157">tooview hello output, use hello following command:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="b9229-158">Bu komut oluştu sözcükleri ve hello word kaç kez listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="b9229-158">This command displays a list of words and how many times hello word occurred.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9229-159">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="b9229-159">Next steps</span></span>

<span data-ttu-id="b9229-160">Hdınsight ile nasıl MapRedcue akış toouse işleri öğrendiniz, bağlantılar tooexplore aşağıdaki hello Azure Hdınsight ile diğer yolları toowork kullanın.</span><span class="sxs-lookup"><span data-stu-id="b9229-160">Now that you have learned how toouse streaming MapRedcue jobs with HDInsight, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* [<span data-ttu-id="b9229-161">HDInsight ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="b9229-161">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="b9229-162">HDInsight ile Pig kullanma</span><span class="sxs-lookup"><span data-stu-id="b9229-162">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="b9229-163">HDInsight ile MapReduce işleri kullanma</span><span class="sxs-lookup"><span data-stu-id="b9229-163">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
