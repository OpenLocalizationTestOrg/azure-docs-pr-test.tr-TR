---
title: "hdınsight'ta - Azure aaaRun Hadoop MapReduce örnekleri | Microsoft Docs"
description: "MapReduce örnekleri Hdınsight'ta dahil jar dosyalarında kullanmaya başlayın. SSH tooconnect toohello küme kullanıp hello Hadoop komutu toorun örnek işleri kullanın."
keywords: "hadoop örnek jar, hadoop örnekler jar, hadoop mapreduce örnekler, mapreduce örnekleri"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e1d2a0b9-1659-4fab-921e-4a8990cbb30a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 7a16bbd51eb17570fcaa3b1e0f5990fa889c106a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-mapreduce-examples-included-in-hdinsight"></a><span data-ttu-id="bd690-105">Hdınsight'ta dahil hello MapReduce örnekler çalıştırın</span><span class="sxs-lookup"><span data-stu-id="bd690-105">Run hello MapReduce examples included in HDInsight</span></span>

[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

<span data-ttu-id="bd690-106">Hdınsight'ta Hadoop ile nasıl toorun hello MapReduce örnekler dahil öğrenin.</span><span class="sxs-lookup"><span data-stu-id="bd690-106">Learn how toorun hello MapReduce examples included with Hadoop on HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bd690-107">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="bd690-107">Prerequisites</span></span>

* <span data-ttu-id="bd690-108">**Hdınsight kümesi**: bkz [Hadoop ile Linux'ta Hdınsight Hive kullanmaya başlama](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="bd690-108">**An HDInsight cluster**: See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="bd690-109">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="bd690-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="bd690-110">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="bd690-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="bd690-111">**Bir SSH istemcisi**: daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="bd690-111">**An SSH client**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="hello-mapreduce-examples"></a><span data-ttu-id="bd690-112">Merhaba MapReduce örnekleri</span><span class="sxs-lookup"><span data-stu-id="bd690-112">hello MapReduce examples</span></span>

<span data-ttu-id="bd690-113">**Konum**: hello örnekleri Hdınsight küme adresindeki hello bulunur `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="bd690-113">**Location**: hello samples are located on hello HDInsight cluster at `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span></span>

<span data-ttu-id="bd690-114">**İçeriği**: örnekleri aşağıdaki hello bu arşivde bulunur:</span><span class="sxs-lookup"><span data-stu-id="bd690-114">**Contents**: hello following samples are contained in this archive:</span></span>

* <span data-ttu-id="bd690-115">`aggregatewordcount`: Bir toplama hello giriş dosyaları hello sözcükleri sayar mapreduce program temel.</span><span class="sxs-lookup"><span data-stu-id="bd690-115">`aggregatewordcount`: An Aggregate based mapreduce program that counts hello words in hello input files.</span></span>
* <span data-ttu-id="bd690-116">`aggregatewordhist`: Bir toplama hello giriş dosyaları hello sözcükleri hello histogram hesaplar mapreduce program temel.</span><span class="sxs-lookup"><span data-stu-id="bd690-116">`aggregatewordhist`: An Aggregate based mapreduce program that computes hello histogram of hello words in hello input files.</span></span>
* <span data-ttu-id="bd690-117">`bbp`Pi sayısının Bailey Borwein Plouffe toocompute tam basamak kullanır mapreduce program.</span><span class="sxs-lookup"><span data-stu-id="bd690-117">`bbp`: A mapreduce program that uses Bailey-Borwein-Plouffe toocompute exact digits of Pi.</span></span>
* <span data-ttu-id="bd690-118">`dbcount`: Bir veritabanında depolanan hello sayfa görünümü günlükleri sayar bir örnek işi.</span><span class="sxs-lookup"><span data-stu-id="bd690-118">`dbcount`: An example job that counts hello pageview logs stored in a database.</span></span>
* <span data-ttu-id="bd690-119">`distbbp`Pi sayısının BBP türü formül toocompute tam BITS kullanır mapreduce program.</span><span class="sxs-lookup"><span data-stu-id="bd690-119">`distbbp`: A mapreduce program that uses a BBP-type formula toocompute exact bits of Pi.</span></span>
* <span data-ttu-id="bd690-120">`grep`Regex hello girişte, hello sayar mapreduce program eşleşir.</span><span class="sxs-lookup"><span data-stu-id="bd690-120">`grep`: A mapreduce program that counts hello matches of a regex in hello input.</span></span>
* <span data-ttu-id="bd690-121">`join`: Üzerinde birleştirme gerçekleştirir bir iş sıralanmış, veri kümeleri eşit olarak bölümlenmiş.</span><span class="sxs-lookup"><span data-stu-id="bd690-121">`join`: A job that performs a join over sorted, equally partitioned datasets.</span></span>
* <span data-ttu-id="bd690-122">`multifilewc`: Birkaç dosyalarından sözcükleri sayar bir iş.</span><span class="sxs-lookup"><span data-stu-id="bd690-122">`multifilewc`: A job that counts words from several files.</span></span>
* <span data-ttu-id="bd690-123">`pentomino`: Program toofind çözümleri toopentomino sorunları yerleştirmede mapreduce kutucuk.</span><span class="sxs-lookup"><span data-stu-id="bd690-123">`pentomino`: A mapreduce tile laying program toofind solutions toopentomino problems.</span></span>
* <span data-ttu-id="bd690-124">`pi`Yarı Monte kullanarak Pi tahminleri mapreduce program Carlo yöntemi.</span><span class="sxs-lookup"><span data-stu-id="bd690-124">`pi`: A mapreduce program that estimates Pi using a quasi-Monte Carlo method.</span></span>
* <span data-ttu-id="bd690-125">`randomtextwriter`Düğüm başına rastgele metinsel veri 10 GB Yazar mapreduce program.</span><span class="sxs-lookup"><span data-stu-id="bd690-125">`randomtextwriter`: A mapreduce program that writes 10 GB of random textual data per node.</span></span>
* <span data-ttu-id="bd690-126">`randomwriter`Düğüm başına rastgele veri 10 GB Yazar mapreduce program.</span><span class="sxs-lookup"><span data-stu-id="bd690-126">`randomwriter`: A mapreduce program that writes 10 GB of random data per node.</span></span>
* <span data-ttu-id="bd690-127">`secondarysort`: İkincil sıralama toohello tanımlama bir örnek aşaması azaltın.</span><span class="sxs-lookup"><span data-stu-id="bd690-127">`secondarysort`: An example defining a secondary sort toohello reduce phase.</span></span>
* <span data-ttu-id="bd690-128">`sort`Merhaba rastgele yazıcı tarafından yazılan hello veri sıralar mapreduce program.</span><span class="sxs-lookup"><span data-stu-id="bd690-128">`sort`: A mapreduce program that sorts hello data written by hello random writer.</span></span>
* <span data-ttu-id="bd690-129">`sudoku`: Bir sudoku Çözücü.</span><span class="sxs-lookup"><span data-stu-id="bd690-129">`sudoku`: A sudoku solver.</span></span>
* <span data-ttu-id="bd690-130">`teragen`: Merhaba terasort verilerini oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bd690-130">`teragen`: Generate data for hello terasort.</span></span>
* <span data-ttu-id="bd690-131">`terasort`: Merhaba terasort çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="bd690-131">`terasort`: Run hello terasort.</span></span>
* <span data-ttu-id="bd690-132">`teravalidate`: Terasort sonuçlarını denetleniyor.</span><span class="sxs-lookup"><span data-stu-id="bd690-132">`teravalidate`: Checking results of terasort.</span></span>
* <span data-ttu-id="bd690-133">`wordcount`Merhaba hello sözcükleri sayar mapreduce program dosyaları girin.</span><span class="sxs-lookup"><span data-stu-id="bd690-133">`wordcount`: A mapreduce program that counts hello words in hello input files.</span></span>
* <span data-ttu-id="bd690-134">`wordmean`Hello ortalama uzunluğu hello hello sözcükleri sayar mapreduce program dosyaları girin.</span><span class="sxs-lookup"><span data-stu-id="bd690-134">`wordmean`: A mapreduce program that counts hello average length of hello words in hello input files.</span></span>
* <span data-ttu-id="bd690-135">`wordmedian`Merhaba Medyan hello hello sözcükleri uzunluğu sayar mapreduce program dosyaları girin.</span><span class="sxs-lookup"><span data-stu-id="bd690-135">`wordmedian`: A mapreduce program that counts hello median length of hello words in hello input files.</span></span>
* <span data-ttu-id="bd690-136">`wordstandarddeviation`Hello standart sapmasını hello uzunluğu hello hello sözcükleri sayar mapreduce program dosyaları girin.</span><span class="sxs-lookup"><span data-stu-id="bd690-136">`wordstandarddeviation`: A mapreduce program that counts hello standard deviation of hello length of hello words in hello input files.</span></span>

<span data-ttu-id="bd690-137">**Kaynak kodu**: Hdınsight küme adresindeki hello üzerinde bu örnekleri için kaynak kodunu dahil `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span><span class="sxs-lookup"><span data-stu-id="bd690-137">**Source code**: Source code for these samples is included on hello HDInsight cluster at `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span></span>

> [!NOTE]
> <span data-ttu-id="bd690-138">Merhaba `2.2.4.9-1` hello yolu hello Hdınsight kümesi için Hortonworks veri platformu hello hello sürümüdür ve kümeniz için farklı olabilir.</span><span class="sxs-lookup"><span data-stu-id="bd690-138">hello `2.2.4.9-1` in hello path is hello version of hello Hortonworks Data Platform for hello HDInsight cluster, and may be different for your cluster.</span></span>

## <a name="run-hello-wordcount-example"></a><span data-ttu-id="bd690-139">Merhaba wordcount örneği çalıştırma</span><span class="sxs-lookup"><span data-stu-id="bd690-139">Run hello wordcount example</span></span>

1. <span data-ttu-id="bd690-140">SSH kullanarak tooHDInsight bağlayın.</span><span class="sxs-lookup"><span data-stu-id="bd690-140">Connect tooHDInsight using SSH.</span></span> <span data-ttu-id="bd690-141">Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="bd690-141">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="bd690-142">Merhaba gelen `username@#######:~$` isteminde, komut toolist hello örnekleri aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="bd690-142">From hello `username@#######:~$` prompt, use hello following command toolist hello samples:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar
    ```

    <span data-ttu-id="bd690-143">Bu komut hello önceki bölümden bu belgenin hello örnek listesi oluşturur.</span><span class="sxs-lookup"><span data-stu-id="bd690-143">This command generates hello list of sample from hello previous section of this document.</span></span>

3. <span data-ttu-id="bd690-144">Kullanım hello aşağıdaki belirli bir örneği tooget Yardım komutu.</span><span class="sxs-lookup"><span data-stu-id="bd690-144">Use hello following command tooget help on a specific sample.</span></span> <span data-ttu-id="bd690-145">Bu durumda, hello **wordcount** örnek:</span><span class="sxs-lookup"><span data-stu-id="bd690-145">In this case, hello **wordcount** sample:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount
    ```

    <span data-ttu-id="bd690-146">İletiden hello alırsınız:</span><span class="sxs-lookup"><span data-stu-id="bd690-146">You receive hello following message:</span></span>

        Usage: wordcount <in> [<in>...] <out>

    <span data-ttu-id="bd690-147">Bu ileti hello kaynak belgeler için birkaç giriş yollarının sağlayabilir gösterir.</span><span class="sxs-lookup"><span data-stu-id="bd690-147">This message indicates that you can provide several input paths for hello source documents.</span></span> <span data-ttu-id="bd690-148">Merhaba son yol hello çıkış (Merhaba kaynak belgeleri sözcükleri sayısı) depolandığı yerdir.</span><span class="sxs-lookup"><span data-stu-id="bd690-148">hello final path is where hello output (count of words in hello source documents) is stored.</span></span>

4. <span data-ttu-id="bd690-149">Toocount aşağıdaki hello hello dizüstü bilgisayarlar, Leonardo Da örnek veri kümenizle sağlanan Vinci, tüm sözcükleri kullanın:</span><span class="sxs-lookup"><span data-stu-id="bd690-149">Use hello following toocount all words in hello Notebooks of Leonardo Da Vinci, which are provided as sample data with your cluster:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/davinciwordcount
    ```

    <span data-ttu-id="bd690-150">Bu işi okuma girdisi `/example/data/gutenberg/davinci.txt`.</span><span class="sxs-lookup"><span data-stu-id="bd690-150">Input for this job is read from `/example/data/gutenberg/davinci.txt`.</span></span> <span data-ttu-id="bd690-151">Bu örnek depolanan çıktısı `/example/data/davinciwordcount`.</span><span class="sxs-lookup"><span data-stu-id="bd690-151">Output for this example is stored in `/example/data/davinciwordcount`.</span></span> <span data-ttu-id="bd690-152">Her iki yolları hello kümesi, hello yerel dosya sistemi için varsayılan depolama bulunur.</span><span class="sxs-lookup"><span data-stu-id="bd690-152">Both paths are located on default storage for hello cluster, not hello local file system.</span></span>

   > [!NOTE]
   > <span data-ttu-id="bd690-153">Merhaba wordcount örneği hello Yardımı'nda belirtildiği gibi birden fazla girdi dosyası da belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="bd690-153">As noted in hello help for hello wordcount sample, you could also specify multiple input files.</span></span> <span data-ttu-id="bd690-154">Örneğin, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` davinci.txt ve ulysses.txt sözcükleri sayar.</span><span class="sxs-lookup"><span data-stu-id="bd690-154">For example, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` would count words in both davinci.txt and ulysses.txt.</span></span>

5. <span data-ttu-id="bd690-155">Merhaba işi tamamlandıktan sonra komutu tooview hello çıktısı aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="bd690-155">Once hello job completes, use hello following command tooview hello output:</span></span>

    ```bash
    hdfs dfs -cat /example/data/davinciwordcount/*
    ```

    <span data-ttu-id="bd690-156">Bu komut hello iş tarafından üretilen tüm hello çıktı dosyaları art arda ekler.</span><span class="sxs-lookup"><span data-stu-id="bd690-156">This command concatenates all hello output files produced by hello job.</span></span> <span data-ttu-id="bd690-157">Merhaba çıktı toohello Konsolu görüntüler.</span><span class="sxs-lookup"><span data-stu-id="bd690-157">It displays hello output toohello console.</span></span> <span data-ttu-id="bd690-158">Merhaba, benzer toohello metin aşağıdaki çıktı:</span><span class="sxs-lookup"><span data-stu-id="bd690-158">hello output is similar toohello following text:</span></span>

        zum     1
        zur     1
        zwanzig 1
        zweite  1

    <span data-ttu-id="bd690-159">Her satır bir sözcük ve hello oluştu kaç kez giriş temsil eder.</span><span class="sxs-lookup"><span data-stu-id="bd690-159">Each line represents a word and how many times it occurred in hello input data.</span></span>

## <a name="hello-sudoku-example"></a><span data-ttu-id="bd690-160">Merhaba Sudoku örneği</span><span class="sxs-lookup"><span data-stu-id="bd690-160">hello Sudoku example</span></span>

<span data-ttu-id="bd690-161">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) olan dokuz 3 x 3 ızgaralar oluşan bir mantık Bulmacanın.</span><span class="sxs-lookup"><span data-stu-id="bd690-161">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) is a logic puzzle made up of nine 3x3 grids.</span></span> <span data-ttu-id="bd690-162">Hello kılavuzunda bazı hücreler, diğerleri boş ve toosolve hello boş hücrelerin hello hedeftir numaraları içeriyor.</span><span class="sxs-lookup"><span data-stu-id="bd690-162">Some cells in hello grid have numbers, while others are blank, and hello goal is toosolve for hello blank cells.</span></span> <span data-ttu-id="bd690-163">Merhaba önceki bağlantı hello Bulmacanın hakkında daha fazla bilgi gerekiyor, ancak bu örnek hello amacı toosolve hello boş hücreler için.</span><span class="sxs-lookup"><span data-stu-id="bd690-163">hello previous link has more information on hello puzzle, but hello purpose of this sample is toosolve for hello blank cells.</span></span> <span data-ttu-id="bd690-164">Bu nedenle bizim giriş hello biçimini izleyen bir dosya olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="bd690-164">So our input should be a file that is in hello following format:</span></span>

* <span data-ttu-id="bd690-165">Dokuz sütunların dokuz satırları</span><span class="sxs-lookup"><span data-stu-id="bd690-165">Nine rows of nine columns</span></span>
* <span data-ttu-id="bd690-166">Her sütunun bir sayı içerebilir veya `?` (boş bir hücre gösterir)</span><span class="sxs-lookup"><span data-stu-id="bd690-166">Each column can contain either a number or `?` (which indicates a blank cell)</span></span>
* <span data-ttu-id="bd690-167">Hücreleri boşlukla ayrılmış</span><span class="sxs-lookup"><span data-stu-id="bd690-167">Cells are separated by a space</span></span>

<span data-ttu-id="bd690-168">Sudoku yapbozlar belirli bir şekilde tooconstruct yoktur; bir sütun veya satır numarasında yinelenemez.</span><span class="sxs-lookup"><span data-stu-id="bd690-168">There is a certain way tooconstruct Sudoku puzzles; you can't repeat a number in a column or row.</span></span> <span data-ttu-id="bd690-169">Doğru şekilde oluşturulduğundan hello Hdınsight kümesinde bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="bd690-169">There's an example on hello HDInsight cluster that is properly constructed.</span></span> <span data-ttu-id="bd690-170">Şu konumdadır: `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` ve metin aşağıdaki hello içerir:</span><span class="sxs-lookup"><span data-stu-id="bd690-170">It is located at `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` and contains hello following text:</span></span>

    8 5 ? 3 9 ? ? ? ?
    ? ? 2 ? ? ? ? ? ?
    ? ? 6 ? 1 ? ? ? 2
    ? ? 4 ? ? 3 ? 5 9
    ? ? 8 9 ? 1 4 ? ?
    3 2 ? 4 ? ? 8 ? ?
    9 ? ? ? 8 ? 5 ? ?
    ? ? ? ? ? ? 2 ? ?
    ? ? ? ? 4 5 ? 7 8

<span data-ttu-id="bd690-171">Bu örnek sorunu hello Sudoku örnek aracılığıyla toorun kullanmak hello komutu:</span><span class="sxs-lookup"><span data-stu-id="bd690-171">toorun this example problem through hello Sudoku example, use hello following command:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar sudoku /usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta
```

<span data-ttu-id="bd690-172">Merhaba sonuçları metin aşağıdaki benzer toohello görüntülenir:</span><span class="sxs-lookup"><span data-stu-id="bd690-172">hello results appear similar toohello following text:</span></span>

    8 5 1 3 9 2 6 4 7
    4 3 2 6 7 8 1 9 5
    7 9 6 5 1 4 3 8 2
    6 1 4 8 2 3 7 5 9
    5 7 8 9 6 1 4 2 3
    3 2 9 4 5 7 8 1 6
    9 4 7 2 8 6 5 3 1
    1 8 5 7 3 9 2 6 4
    2 6 3 1 4 5 9 7 8

## <a name="pi--example"></a><span data-ttu-id="bd690-173">Pi (π) örneği</span><span class="sxs-lookup"><span data-stu-id="bd690-173">Pi (π) example</span></span>

<span data-ttu-id="bd690-174">Merhaba pi örnek bir istatistik kullanır (yarı Monte Carlo) yöntemi tooestimate hello pi değerini.</span><span class="sxs-lookup"><span data-stu-id="bd690-174">hello pi sample uses a statistical (quasi-Monte Carlo) method tooestimate hello value of pi.</span></span> <span data-ttu-id="bd690-175">Noktaları rastgele bir birim kare yerleştirilir.</span><span class="sxs-lookup"><span data-stu-id="bd690-175">Points are placed at random in a unit square.</span></span> <span data-ttu-id="bd690-176">Merhaba kare bir daire de içerir.</span><span class="sxs-lookup"><span data-stu-id="bd690-176">hello square also contains a circle.</span></span> <span data-ttu-id="bd690-177">Merhaba hello noktaları hello daire içinde kalan olasılığı olan hello eşit toohello alanı yuvarlak, pi/4.</span><span class="sxs-lookup"><span data-stu-id="bd690-177">hello probability that hello points fall within hello circle are equal toohello area of hello circle, pi/4.</span></span> <span data-ttu-id="bd690-178">pi değerini Hello 4R başlangıç değerinden tahmin edilebilir.</span><span class="sxs-lookup"><span data-stu-id="bd690-178">hello value of pi can be estimated from hello value of 4R.</span></span> <span data-ttu-id="bd690-179">R hello daire toohello toplam sayısı hello kare içinde noktalarını içinde olduğunda puan hello sayısının hello orandır.</span><span class="sxs-lookup"><span data-stu-id="bd690-179">R is hello ratio of hello number of points that are inside hello circle toohello total number of points that are within hello square.</span></span> <span data-ttu-id="bd690-180">Merhaba büyük hello kullanılan noktaları, hello daha iyi hello tahmin örneğidir.</span><span class="sxs-lookup"><span data-stu-id="bd690-180">hello larger hello sample of points used, hello better hello estimate is.</span></span>

<span data-ttu-id="bd690-181">Bu örnek komut toorun aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="bd690-181">Use hello following command toorun this sample.</span></span> <span data-ttu-id="bd690-182">Bu komut, 10,000,000 örnekleri tooestimate hello pi değerini ile 16 eşlemeleri kullanır:</span><span class="sxs-lookup"><span data-stu-id="bd690-182">This command uses 16 maps with 10,000,000 samples each tooestimate hello value of pi:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar pi 16 10000000
```

<span data-ttu-id="bd690-183">Merhaba bu komut tarafından döndürülen değeri çok benzer**3.14159155000000000000**.</span><span class="sxs-lookup"><span data-stu-id="bd690-183">hello value returned by this command is similar too**3.14159155000000000000**.</span></span> <span data-ttu-id="bd690-184">Başvurular için hello ilk 10 ondalık pi'nin 3.1415926535 yerlerdir.</span><span class="sxs-lookup"><span data-stu-id="bd690-184">For references, hello first 10 decimal places of pi are 3.1415926535.</span></span>

## <a name="10-gb-greysort-example"></a><span data-ttu-id="bd690-185">10 GB Greysort örneği</span><span class="sxs-lookup"><span data-stu-id="bd690-185">10 GB Greysort example</span></span>

<span data-ttu-id="bd690-186">GraySort Kıyaslama sıralama ' dir.</span><span class="sxs-lookup"><span data-stu-id="bd690-186">GraySort is a benchmark sort.</span></span> <span data-ttu-id="bd690-187">Merhaba, büyük miktarlarda verinin, genellikle en az bir 100 TB sıralama sırasında elde edilen hello sıralama oranı (TB dakikada) ölçümüdür.</span><span class="sxs-lookup"><span data-stu-id="bd690-187">hello metric is hello sort rate (TB/minute) that is achieved while sorting large amounts of data, usually a 100 TB minimum.</span></span>

<span data-ttu-id="bd690-188">Bu örnek uygun bir 10 GB veri kullanır, böylece oldukça hızlı bir şekilde çalıştırılabilir.</span><span class="sxs-lookup"><span data-stu-id="bd690-188">This sample uses a modest 10 GB of data so that it can be run relatively quickly.</span></span> <span data-ttu-id="bd690-189">Owen O'Malley ve Arun Murthy tarafından geliştirilen hello MapReduce uygulamaları kullanır.</span><span class="sxs-lookup"><span data-stu-id="bd690-189">It uses hello MapReduce applications developed by Owen O'Malley and Arun Murthy.</span></span> <span data-ttu-id="bd690-190">Bu uygulamalar hello yıllık genel amaçlı ("daytona") terabayt sıralama Kıyaslama 0.578 TB/dak (100 TB 173 dakika cinsinden) oranı ile 2009 kazanmıştır.</span><span class="sxs-lookup"><span data-stu-id="bd690-190">These applications won hello annual general-purpose ("daytona") terabyte sort benchmark in 2009, with a rate of 0.578 TB/min (100 TB in 173 minutes).</span></span> <span data-ttu-id="bd690-191">Bu ve diğer sıralama değerlendirmeleri hakkında daha fazla bilgi için bkz: Merhaba [Sortbenchmark](http://sortbenchmark.org/) site.</span><span class="sxs-lookup"><span data-stu-id="bd690-191">For more information on this and other sorting benchmarks, see hello [Sortbenchmark](http://sortbenchmark.org/) site.</span></span>

<span data-ttu-id="bd690-192">Bu örnek, MapReduce programlar üç kümesi kullanır:</span><span class="sxs-lookup"><span data-stu-id="bd690-192">This sample uses three sets of MapReduce programs:</span></span>

* <span data-ttu-id="bd690-193">**TeraGen**: veri toosort satırlarını oluşturur A MapReduce programı</span><span class="sxs-lookup"><span data-stu-id="bd690-193">**TeraGen**: A MapReduce program that generates rows of data toosort</span></span>

* <span data-ttu-id="bd690-194">**TeraSort**: örnekler hello giriş verilerini ve MapReduce toosort hello verilerini toplam sıralamaya kullanır</span><span class="sxs-lookup"><span data-stu-id="bd690-194">**TeraSort**: Samples hello input data and uses MapReduce toosort hello data into a total order</span></span>

    <span data-ttu-id="bd690-195">TeraSort özel bölümleyici dışında bir standart MapReduce sıralama ' dir.</span><span class="sxs-lookup"><span data-stu-id="bd690-195">TeraSort is a standard MapReduce sort, except for a custom partitioner.</span></span> <span data-ttu-id="bd690-196">Merhaba bölümleyici her azaltın hello anahtar aralığını tanımlamak örneklenen N-1 anahtarları sıralı listesini kullanır.</span><span class="sxs-lookup"><span data-stu-id="bd690-196">hello partitioner uses a sorted list of N-1 sampled keys that define hello key range for each reduce.</span></span> <span data-ttu-id="bd690-197">Özellikle, [i-1] örnek tüm anahtarları böyle < = anahtar < örnek [i] tooreduce gönderilen ediyorum.</span><span class="sxs-lookup"><span data-stu-id="bd690-197">In particular, all keys such that sample[i-1] <= key < sample[i] are sent tooreduce i.</span></span> <span data-ttu-id="bd690-198">Bu bölümleyici hello çıktısını azaltmak i + 1 değerinden hello çıkışları i azaltmak garanti tüm.</span><span class="sxs-lookup"><span data-stu-id="bd690-198">This partitioner guarantees that hello outputs of reduce i are all less than hello output of reduce i+1.</span></span>

* <span data-ttu-id="bd690-199">**TeraValidate**: Bu hello çıkışı doğrular A MapReduce program Genel sıralanmış</span><span class="sxs-lookup"><span data-stu-id="bd690-199">**TeraValidate**: A MapReduce program that validates that hello output is globally sorted</span></span>

    <span data-ttu-id="bd690-200">Merhaba çıktı dizini içinde dosya başına bir harita oluşturur ve her eşleme her anahtar değerinden küçük veya buna eşit olmasını sağlar toohello öncekinin.</span><span class="sxs-lookup"><span data-stu-id="bd690-200">It creates one map per file in hello output directory, and each map ensures that each key is less than or equal toohello previous one.</span></span> <span data-ttu-id="bd690-201">Merhaba harita işlevi hello kayıtlarının ilk oluşturur ve anahtarları her dosyanın en son.</span><span class="sxs-lookup"><span data-stu-id="bd690-201">hello map function generates records of hello first and last keys of each file.</span></span> <span data-ttu-id="bd690-202">Merhaba azaltmak işlevi bu hello sağlar i dosyasının ilk anahtar hello son anahtarı dosyası i-1 büyük.</span><span class="sxs-lookup"><span data-stu-id="bd690-202">hello reduce function ensures that hello first key of file i is greater than hello last key of file i-1.</span></span> <span data-ttu-id="bd690-203">Herhangi bir sorun bozuk hello anahtarlarla aşaması, hello çıktısı azaltmak olarak bildirilir.</span><span class="sxs-lookup"><span data-stu-id="bd690-203">Any problems are reported as an output of hello reduce phase, with hello keys that are out of order.</span></span>

<span data-ttu-id="bd690-204">Kullanım hello aşağıdaki adımları toogenerate verileri sıralamak ve ardından hello çıkış doğrulayın:</span><span class="sxs-lookup"><span data-stu-id="bd690-204">Use hello following steps toogenerate data, sort, and then validate hello output:</span></span>

1. <span data-ttu-id="bd690-205">10 GB saklı toohello Hdınsight kümenin varsayılan depolama veri oluşturmak, `/example/data/10GB-sort-input`:</span><span class="sxs-lookup"><span data-stu-id="bd690-205">Generate 10 GB of data, which is stored toohello HDInsight cluster's default storage at `/example/data/10GB-sort-input`:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapred.map.tasks=50 100000000 /example/data/10GB-sort-input
    ```

    <span data-ttu-id="bd690-206">Merhaba `-Dmapred.map.tasks` Hadoop bu proje için kaç tane harita görevleri toouse söyler.</span><span class="sxs-lookup"><span data-stu-id="bd690-206">hello `-Dmapred.map.tasks` tells Hadoop how many map tasks toouse for this job.</span></span> <span data-ttu-id="bd690-207">Merhaba son iki parametreleri istemeniz hello iş toocreate 10 GB veri ve toostore adresinden `/example/data/10GB-sort-input`.</span><span class="sxs-lookup"><span data-stu-id="bd690-207">hello final two parameters instruct hello job toocreate 10 GB of data and toostore it at `/example/data/10GB-sort-input`.</span></span>

2. <span data-ttu-id="bd690-208">Komut toosort hello verileri aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="bd690-208">Use hello following command toosort hello data:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-input /example/data/10GB-sort-output
    ```

    <span data-ttu-id="bd690-209">Merhaba `-Dmapred.reduce.tasks` görevleri toouse hello işi için kaç tane azaltmak Hadoop söyler.</span><span class="sxs-lookup"><span data-stu-id="bd690-209">hello `-Dmapred.reduce.tasks` tells Hadoop how many reduce tasks toouse for hello job.</span></span> <span data-ttu-id="bd690-210">Hello son iki Parametreler yalnızca hello girdi ve çıktı verileri için konumları.</span><span class="sxs-lookup"><span data-stu-id="bd690-210">hello final two parameters are just hello input and output locations for data.</span></span>

3. <span data-ttu-id="bd690-211">Merhaba sıralama ölçütü oluşturulan toovalidate hello veri aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="bd690-211">Use hello following toovalidate hello data generated by hello sort:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-output /example/data/10GB-sort-validate
    ```

## <a name="next-steps"></a><span data-ttu-id="bd690-212">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="bd690-212">Next steps</span></span>

<span data-ttu-id="bd690-213">Bu makalede, nasıl toorun başlangıç örnekleri Linux tabanlı Hdınsight kümeleri ile Merhaba dahil öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="bd690-213">From this article, you learned how toorun hello samples included with hello Linux-based HDInsight clusters.</span></span> <span data-ttu-id="bd690-214">Hdınsight ile Pig, Hive ve MapReduce kullanma hakkında daha fazla öğreticileri için aşağıdaki konularda hello bakın:</span><span class="sxs-lookup"><span data-stu-id="bd690-214">For tutorials about using Pig, Hive, and MapReduce with HDInsight, see hello following topics:</span></span>

* <span data-ttu-id="bd690-215">[Hdınsight'ta Hadoop ile pig kullanma][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="bd690-215">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="bd690-216">[Hdınsight'ta Hadoop ile Hive kullanma][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="bd690-216">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="bd690-217">[Hdınsight'ta Hadoop ile MapReduce kullanma][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="bd690-217">[Use MapReduce with Hadoop on HDInsight][hdinsight-use-mapreduce]</span></span>

[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md



[hdinsight-samples]: hdinsight-run-samples.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
