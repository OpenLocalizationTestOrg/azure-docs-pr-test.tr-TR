---
title: "Hdınsight - Azure ile MapReduce işleri akış Python geliştirme | Microsoft Docs"
description: "Akış MapReduce işlerinin Python kullanmayı öğrenin. Hadoop, Java dışındaki dillerde yazmak için MapReduce için akış bir API sağlar."
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
ms.openlocfilehash: b86605c49291a99f49c4b2841d46324cfd0db56d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="develop-python-streaming-mapreduce-programs-for-hdinsight"></a><span data-ttu-id="84de1-104">MapReduce programları Hdınsight için akış Python geliştirme</span><span class="sxs-lookup"><span data-stu-id="84de1-104">Develop Python streaming MapReduce programs for HDInsight</span></span>

<span data-ttu-id="84de1-105">Python MapReduce işlemleri akışında kullanmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="84de1-105">Learn how to use Python in streaming MapReduce operations.</span></span> <span data-ttu-id="84de1-106">Hadoop harita yazma ve Java dışındaki dillerde işlevleri azaltmak sağlar MapReduce akış bir API sağlar.</span><span class="sxs-lookup"><span data-stu-id="84de1-106">Hadoop provides a streaming API for MapReduce that enables you to write map and reduce functions in languages other than Java.</span></span> <span data-ttu-id="84de1-107">Bu belgede yer alan adımlar eşleme uygulamak ve Python bileşenlerinde azaltın.</span><span class="sxs-lookup"><span data-stu-id="84de1-107">The steps in this document implement the Map and Reduce components in Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84de1-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="84de1-108">Prerequisites</span></span>

* <span data-ttu-id="84de1-109">Bir Hdınsight kümesinde Linux tabanlı Hadoop</span><span class="sxs-lookup"><span data-stu-id="84de1-109">A Linux-based Hadoop on HDInsight cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="84de1-110">Bu belgede yer alan adımlar Linux kullanan bir Hdınsight kümesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="84de1-110">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="84de1-111">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="84de1-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="84de1-112">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="84de1-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="84de1-113">Bir metin düzenleyicisi</span><span class="sxs-lookup"><span data-stu-id="84de1-113">A text editor</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="84de1-114">Metin Düzenleyicisi LF olarak satırı bitiş kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="84de1-114">The text editor must use LF as the line ending.</span></span> <span data-ttu-id="84de1-115">CRLF satır sonu kullanarak hataları MapReduce işi Linux tabanlı Hdınsight kümelerinde çalıştırırken neden olur.</span><span class="sxs-lookup"><span data-stu-id="84de1-115">Using a line ending of CRLF causes errors when running the MapReduce job on Linux-based HDInsight clusters.</span></span>

* <span data-ttu-id="84de1-116">`ssh` Ve `scp` komutları veya [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span><span class="sxs-lookup"><span data-stu-id="84de1-116">The `ssh` and `scp` commands, or [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span></span>

## <a name="word-count"></a><span data-ttu-id="84de1-117">Sözcük Sayımı</span><span class="sxs-lookup"><span data-stu-id="84de1-117">Word count</span></span>

<span data-ttu-id="84de1-118">Bu temel sözcük sayımı bir python Eşleyici ve reducer uygulanan bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="84de1-118">This example is a basic word count implemented in a python a mapper and reducer.</span></span> <span data-ttu-id="84de1-119">Eşleyici cümleleri tek tek sözcüklere böler ve reducer sözcükleri toplar ve bir çıktı oluşturmak için sayar.</span><span class="sxs-lookup"><span data-stu-id="84de1-119">The mapper breaks sentences into individual words, and the reducer aggregates the words and counts to produce the output.</span></span>

<span data-ttu-id="84de1-120">Aşağıdaki akış çizelgesi ne sırasında harita olur ve aşamaları azaltmak gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="84de1-120">The following flowchart illustrates what happens during the map and reduce phases.</span></span>

![mapreduce işlem çizimi](./media/hdinsight-hadoop-streaming-python/HDI.WordCountDiagram.png)

## <a name="streaming-mapreduce"></a><span data-ttu-id="84de1-122">Akış MapReduce</span><span class="sxs-lookup"><span data-stu-id="84de1-122">Streaming MapReduce</span></span>

<span data-ttu-id="84de1-123">Hadoop, eşleme içeren bir dosya belirtin ve bir iş tarafından kullanılan mantığı azaltmak sağlar.</span><span class="sxs-lookup"><span data-stu-id="84de1-123">Hadoop allows you to specify a file that contains the map and reduce logic that is used by a job.</span></span> <span data-ttu-id="84de1-124">Eşleme için özel gereksinimleri ve mantığı azaltmak şunlardır:</span><span class="sxs-lookup"><span data-stu-id="84de1-124">The specific requirements for the map and reduce logic are:</span></span>

* <span data-ttu-id="84de1-125">**Giriş**: eşleme ve azaltma bileşenleri STDIN giriş verilerinin okuma gerekir.</span><span class="sxs-lookup"><span data-stu-id="84de1-125">**Input**: The map and reduce components must read input data from STDIN.</span></span>
* <span data-ttu-id="84de1-126">**Çıktı**: eşleme ve azaltma bileşenleri STDOUT çıkış veri yazma gerekir.</span><span class="sxs-lookup"><span data-stu-id="84de1-126">**Output**: The map and reduce components must write output data to STDOUT.</span></span>
* <span data-ttu-id="84de1-127">**Veri biçimi**: tüketilen ve üretilen veriler bir sekme karakteriyle ayrılmış bir anahtar/değer çifti olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="84de1-127">**Data format**: The data consumed and produced must be a key/value pair, separated by a tab character.</span></span>

<span data-ttu-id="84de1-128">Python kolayca işleyebilir bu gereksinimleri kullanarak `sys` STDIN ve kullanarak okumak için Modülü `print` STDOUT yazdırmak için.</span><span class="sxs-lookup"><span data-stu-id="84de1-128">Python can easily handle these requirements by using the `sys` module to read from STDIN and using `print` to print to STDOUT.</span></span> <span data-ttu-id="84de1-129">Kalan görev yalnızca bir sekme verilerle biçimlendirme (`\t`) anahtar ve değer arasında karakter.</span><span class="sxs-lookup"><span data-stu-id="84de1-129">The remaining task is simply formatting the data with a tab (`\t`) character between the key and value.</span></span>

## <a name="create-the-mapper-and-reducer"></a><span data-ttu-id="84de1-130">Eşleyici ve reducer oluşturma</span><span class="sxs-lookup"><span data-stu-id="84de1-130">Create the mapper and reducer</span></span>

1. <span data-ttu-id="84de1-131">Adlı bir dosya oluşturun `mapper.py` ve içeriği olarak aşağıdaki kodu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="84de1-131">Create a file named `mapper.py` and use the following code as the content:</span></span>

   ```python
   #!/usr/bin/env python

   # Use the sys module
   import sys

   # 'file' in this case is STDIN
   def read_input(file):
       # Split each line into words
       for line in file:
           yield line.split()

   def main(separator='\t'):
       # Read the data using read_input
       data = read_input(sys.stdin)
       # Process each word returned from read_input
       for words in data:
           # Process each word
           for word in words:
               # Write to STDOUT
               print '%s%s%d' % (word, separator, 1)

   if __name__ == "__main__":
       main()
   ```

2. <span data-ttu-id="84de1-132">Adlı bir dosya oluşturun **reducer.py** ve içeriği olarak aşağıdaki kodu kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="84de1-132">Create a file named **reducer.py** and use the following code as the content:</span></span>

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
           # Strip out the separator character
           yield line.rstrip().split(separator, 1)

   def main(separator='\t'):
       # Read the data using read_mapper_output
       data = read_mapper_output(sys.stdin, separator=separator)
       # Group words and counts into 'group'
       #   Since MapReduce is a distributed process, each word
       #   may have multiple counts. 'group' will have all counts
       #   which can be retrieved using the word as the key.
       for current_word, group in groupby(data, itemgetter(0)):
           try:
               # For each word, pull the count(s) for the word
               #   from 'group' and create a total count
               total_count = sum(int(count) for current_word, count in group)
               # Write to stdout
               print "%s%s%d" % (current_word, separator, total_count)
           except ValueError:
               # Count was not a number, so do nothing
               pass

   if __name__ == "__main__":
       main()
   ```

## <a name="run-using-powershell"></a><span data-ttu-id="84de1-133">PowerShell kullanarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="84de1-133">Run using PowerShell</span></span>

<span data-ttu-id="84de1-134">Dosyalarınızın doğru satır sonları olmasını sağlamak için aşağıdaki PowerShell betiğini kullanın:</span><span class="sxs-lookup"><span data-stu-id="84de1-134">To ensure that your files have the right line endings, use the following PowerShell script:</span></span>

<span data-ttu-id="84de1-135">[!code-powershell[Ana](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]</span><span class="sxs-lookup"><span data-stu-id="84de1-135">[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]</span></span>

<span data-ttu-id="84de1-136">Dosyaları karşıya yükleme, işini çalıştırın ve çıktıyı görüntülemek için aşağıdaki PowerShell betiğini kullanın:</span><span class="sxs-lookup"><span data-stu-id="84de1-136">Use the following PowerShell script to upload the files, run the job, and view the output:</span></span>

<span data-ttu-id="84de1-137">[!code-powershell[Ana](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]</span><span class="sxs-lookup"><span data-stu-id="84de1-137">[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]</span></span>

## <a name="run-from-an-ssh-session"></a><span data-ttu-id="84de1-138">Bir SSH oturumunda</span><span class="sxs-lookup"><span data-stu-id="84de1-138">Run from an SSH session</span></span>

1. <span data-ttu-id="84de1-139">Aynı dizinde, geliştirme ortamınızdan `mapper.py` ve `reducer.py` dosyaları, aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="84de1-139">From your development environment, in the same directory as `mapper.py` and `reducer.py` files, use the following command:</span></span>

    ```bash
    scp mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="84de1-140">Değiştir `username` , kümeniz için SSH kullanıcı adı ve `clustername` , küme adı.</span><span class="sxs-lookup"><span data-stu-id="84de1-140">Replace `username` with the SSH user name for your cluster, and `clustername` with the name of your cluster.</span></span>

    <span data-ttu-id="84de1-141">Bu komut dosyaları, yerel sistemden baş düğüme kopyalar.</span><span class="sxs-lookup"><span data-stu-id="84de1-141">This command copies the files from the local system to the head node.</span></span>

    > [!NOTE]
    > <span data-ttu-id="84de1-142">SSH hesabınızı korumak için parola kullandıysanız, parola istenir.</span><span class="sxs-lookup"><span data-stu-id="84de1-142">If you used a password to secure your SSH account, you are prompted for the password.</span></span> <span data-ttu-id="84de1-143">Bir SSH anahtarı kullandıysanız, kullanmak zorunda kalabilirsiniz `-i` parametre ve özel anahtar yolu.</span><span class="sxs-lookup"><span data-stu-id="84de1-143">If you used an SSH key, you may have to use the `-i` parameter and the path to the private key.</span></span> <span data-ttu-id="84de1-144">Örneğin, `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="84de1-144">For example, `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="84de1-145">SSH kullanarak kümeye bağlanın:</span><span class="sxs-lookup"><span data-stu-id="84de1-145">Connect to the cluster by using SSH:</span></span>

    ```bash
    ssh username@clustername-ssh.azurehdinsight.net`
    ```

    <span data-ttu-id="84de1-146">Daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="84de1-146">For more information on, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="84de1-147">Mapper.py ve reducer.py doğru satır sonları sahip emin olmak için aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="84de1-147">To ensure the mapper.py and reducer.py have the correct line endings, use the following commands:</span></span>

    ```bash
    perl -pi -e 's/\r\n/\n/g' mapper.py
    perl -pi -e 's/\r\n/\n/g' reducer.py
    ```

4. <span data-ttu-id="84de1-148">MapReduce işi başlatmak için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="84de1-148">Use the following command to start the MapReduce job.</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files mapper.py,reducer.py -mapper mapper.py -reducer reducer.py -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
    ```

    <span data-ttu-id="84de1-149">Bu komut, aşağıdaki bölümleri içerir:</span><span class="sxs-lookup"><span data-stu-id="84de1-149">This command has the following parts:</span></span>

   * <span data-ttu-id="84de1-150">**hadoop streaming.jar**: akış MapReduce işlemleri yaparken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="84de1-150">**hadoop-streaming.jar**: Used when performing streaming MapReduce operations.</span></span> <span data-ttu-id="84de1-151">Bu Hadoop MapReduce harici kod sağladığınız arabirimleri.</span><span class="sxs-lookup"><span data-stu-id="84de1-151">It interfaces Hadoop with the external MapReduce code you provide.</span></span>

   * <span data-ttu-id="84de1-152">**-dosyaları**: MapReduce işi belirtilen dosyaları ekler.</span><span class="sxs-lookup"><span data-stu-id="84de1-152">**-files**: Adds the specified files to the MapReduce job.</span></span>

   * <span data-ttu-id="84de1-153">**-Eşleyici**: Hadoop Eşleyici kullanmak için hangi dosya söyler.</span><span class="sxs-lookup"><span data-stu-id="84de1-153">**-mapper**: Tells Hadoop which file to use as the mapper.</span></span>

   * <span data-ttu-id="84de1-154">**-reducer**: Hadoop reducer kullanmak için hangi dosya söyler.</span><span class="sxs-lookup"><span data-stu-id="84de1-154">**-reducer**: Tells Hadoop which file to use as the reducer.</span></span>

   * <span data-ttu-id="84de1-155">**-Giriş**: gelen güvenmemeniz gerekir giriş dosyası sözcükleri.</span><span class="sxs-lookup"><span data-stu-id="84de1-155">**-input**: The input file that we should count words from.</span></span>

   * <span data-ttu-id="84de1-156">**-Çıktı**: çıktı yazılır dizin.</span><span class="sxs-lookup"><span data-stu-id="84de1-156">**-output**: The directory that the output is written to.</span></span>

    <span data-ttu-id="84de1-157">MapReduce işi çalıştığından, işlem yüzde olarak görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="84de1-157">As the MapReduce job works, the process is displayed as percentages.</span></span>

        <span data-ttu-id="84de1-158">02/15/05 19:01:04 bilgisi mapreduce. İş: eşleme %0 azaltmak %0 02/15/05 19:01:16 bilgisi mapreduce. İş: % 0 harita % 100 azaltmak 02/15/05 19:01:27 bilgisi mapreduce. İş: eşleme % %100 100 azaltın.</span><span class="sxs-lookup"><span data-stu-id="84de1-158">15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%</span></span>


5. <span data-ttu-id="84de1-159">Çıktı görüntülemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="84de1-159">To view the output, use the following command:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="84de1-160">Bu komut oluştu sözcükleri ve word kaç kez listesini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="84de1-160">This command displays a list of words and how many times the word occurred.</span></span>

## <a name="next-steps"></a><span data-ttu-id="84de1-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="84de1-161">Next steps</span></span>

<span data-ttu-id="84de1-162">Hdınsight ile akış MapRedcue işi kullanmayı öğrendiniz, Azure Hdınsight ile çalışmak için diğer yollarını keşfetmek için aşağıdaki bağlantıları kullanın.</span><span class="sxs-lookup"><span data-stu-id="84de1-162">Now that you have learned how to use streaming MapRedcue jobs with HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* [<span data-ttu-id="84de1-163">HDInsight ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="84de1-163">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="84de1-164">HDInsight ile Pig kullanma</span><span class="sxs-lookup"><span data-stu-id="84de1-164">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="84de1-165">HDInsight ile MapReduce işleri kullanma</span><span class="sxs-lookup"><span data-stu-id="84de1-165">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
