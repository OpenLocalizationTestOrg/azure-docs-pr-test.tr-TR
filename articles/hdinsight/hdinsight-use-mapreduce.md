---
title: "hdınsight'ta Hadoop ile aaaMapReduce | Microsoft Docs"
description: "Toorun MapReduce Hadoop'ta Hdınsight kümelerinde nasıl işler öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7f321501-d62c-4ffc-b5d6-102ecba6dd76
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 0cf7ad0e6769e678be64f9e4ec8ed7a214ab7af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight"></a><span data-ttu-id="40c28-103">Hdınsight'ta Hadoop MapReduce kullanın</span><span class="sxs-lookup"><span data-stu-id="40c28-103">Use MapReduce in Hadoop on HDInsight</span></span>

<span data-ttu-id="40c28-104">Hdınsight kümelerinde nasıl toorun MapReduce işleri öğrenin.</span><span class="sxs-lookup"><span data-stu-id="40c28-104">Learn how toorun MapReduce jobs on HDInsight clusters.</span></span> <span data-ttu-id="40c28-105">Aşağıdaki tablo toodiscover hello Hdınsight ile MapReduce kullanılabilir çeşitli şekillerde hello kullan:</span><span class="sxs-lookup"><span data-stu-id="40c28-105">Use hello following table toodiscover hello various ways that MapReduce can be used with HDInsight:</span></span>

| <span data-ttu-id="40c28-106">**Bu**...</span><span class="sxs-lookup"><span data-stu-id="40c28-106">**Use this**...</span></span> | <span data-ttu-id="40c28-107">**.. .toodo bu**</span><span class="sxs-lookup"><span data-stu-id="40c28-107">**...toodo this**</span></span> | <span data-ttu-id="40c28-108">.. hemen bu **küme işletim sistemi**</span><span class="sxs-lookup"><span data-stu-id="40c28-108">...with this **cluster operating system**</span></span> | <span data-ttu-id="40c28-109">.. .from bu **istemci işletim sistemi**</span><span class="sxs-lookup"><span data-stu-id="40c28-109">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="40c28-110">SSH</span><span class="sxs-lookup"><span data-stu-id="40c28-110">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="40c28-111">Merhaba Hadoop komutu aracılığıyla kullanmak **SSH**</span><span class="sxs-lookup"><span data-stu-id="40c28-111">Use hello Hadoop command through **SSH**</span></span> |<span data-ttu-id="40c28-112">Linux</span><span class="sxs-lookup"><span data-stu-id="40c28-112">Linux</span></span> |<span data-ttu-id="40c28-113">Linux, UNIX, Mac OS X veya Windows</span><span class="sxs-lookup"><span data-stu-id="40c28-113">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="40c28-114">REST</span><span class="sxs-lookup"><span data-stu-id="40c28-114">REST</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="40c28-115">Merhaba işi uzaktan kullanarak göndermek **REST** (örnekler cURL kullanın)</span><span class="sxs-lookup"><span data-stu-id="40c28-115">Submit hello job remotely by using **REST** (examples use cURL)</span></span> |<span data-ttu-id="40c28-116">Linux veya Windows</span><span class="sxs-lookup"><span data-stu-id="40c28-116">Linux or Windows</span></span> |<span data-ttu-id="40c28-117">Linux, UNIX, Mac OS X veya Windows</span><span class="sxs-lookup"><span data-stu-id="40c28-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="40c28-118">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="40c28-118">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="40c28-119">Merhaba işi uzaktan kullanarak göndermek **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="40c28-119">Submit hello job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="40c28-120">Linux veya Windows</span><span class="sxs-lookup"><span data-stu-id="40c28-120">Linux or Windows</span></span> |<span data-ttu-id="40c28-121">Windows</span><span class="sxs-lookup"><span data-stu-id="40c28-121">Windows</span></span> |
| <span data-ttu-id="40c28-122">[Uzak Masaüstü](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (Hdınsight 3.2 ve 3.3)</span><span class="sxs-lookup"><span data-stu-id="40c28-122">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="40c28-123">Merhaba Hadoop komutu aracılığıyla kullanmak **Uzak Masaüstü**</span><span class="sxs-lookup"><span data-stu-id="40c28-123">Use hello Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="40c28-124">Windows</span><span class="sxs-lookup"><span data-stu-id="40c28-124">Windows</span></span> |<span data-ttu-id="40c28-125">Windows</span><span class="sxs-lookup"><span data-stu-id="40c28-125">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="40c28-126">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="40c28-126">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="40c28-127">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="40c28-127">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="40c28-128"><a id="whatis"></a>MapReduce nedir</span><span class="sxs-lookup"><span data-stu-id="40c28-128"><a id="whatis"></a>What is MapReduce</span></span>

<span data-ttu-id="40c28-129">Hadoop MapReduce, çok büyük miktarda veri işleyen işlerini yazmak için bir yazılım çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="40c28-129">Hadoop MapReduce is a software framework for writing jobs that process vast amounts of data.</span></span> <span data-ttu-id="40c28-130">Giriş verisi kümenizdeki hello düğümleri arasında paralel olarak sonra işlenen bağımsız parçalara bölünür.</span><span class="sxs-lookup"><span data-stu-id="40c28-130">Input data is split into independent chunks, which are then processed in parallel across hello nodes in your cluster.</span></span> <span data-ttu-id="40c28-131">Bir MapReduce işi, iki işlevden oluşur:</span><span class="sxs-lookup"><span data-stu-id="40c28-131">A MapReduce job consists of two functions:</span></span>

* <span data-ttu-id="40c28-132">**Eşleyici**: giriş verileri kullanır (genellikle filtre ve sıralama işlemleri ile) çözümler ve diziler (anahtar-değer çiftleri) yayar</span><span class="sxs-lookup"><span data-stu-id="40c28-132">**Mapper**: Consumes input data, analyzes it (usually with filter and sorting operations), and emits tuples (key-value pairs)</span></span>

* <span data-ttu-id="40c28-133">**Reducer**: hello Eşleyicisi tarafından gösterilen diziler kullanır ve Eşleyici veri hello daha küçük, birleşik bir sonuç oluşturur Özet bir işlemi gerçekleştirir</span><span class="sxs-lookup"><span data-stu-id="40c28-133">**Reducer**: Consumes tuples emitted by hello Mapper and performs a summary operation that creates a smaller, combined result from hello Mapper data</span></span>

<span data-ttu-id="40c28-134">Bir temel word sayısı MapReduce işi örnek diyagramı aşağıdaki hello gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="40c28-134">A basic word count MapReduce job example is illustrated in hello following diagram:</span></span>

![HDI. WordCountDiagram][image-hdi-wordcountdiagram]

<span data-ttu-id="40c28-136">Bu işin Hello çıkış analiz edildi hello metinde her sözcüğün oluştu kaç kez sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="40c28-136">hello output of this job is a count of how many times each word occurred in hello text that was analyzed.</span></span>

* <span data-ttu-id="40c28-137">Merhaba Eşleyici her satır girdi olarak hello giriş metinden alır ve sözcüklere böler.</span><span class="sxs-lookup"><span data-stu-id="40c28-137">hello mapper takes each line from hello input text as an input and breaks it into words.</span></span> <span data-ttu-id="40c28-138">Bir anahtar/değer yayar çifti bir sözcük hello sözcüğün her oluştuğunda bir 1 tarafından izlendiği.</span><span class="sxs-lookup"><span data-stu-id="40c28-138">It emits a key/value pair each time a word occurs of hello word is followed by a 1.</span></span> <span data-ttu-id="40c28-139">Merhaba çıktı tooreducer göndermeden önce sıralanır.</span><span class="sxs-lookup"><span data-stu-id="40c28-139">hello output is sorted before sending it tooreducer.</span></span>
* <span data-ttu-id="40c28-140">Merhaba reducer her sözcüğün için bu tek tek sayıları toplar ve kendi oluşum hello toplamı tarafından izlenen hello sözcüğünü içeren bir tek anahtar/değer çifti yayar.</span><span class="sxs-lookup"><span data-stu-id="40c28-140">hello reducer sums these individual counts for each word and emits a single key/value pair that contains hello word followed by hello sum of its occurrences.</span></span>

<span data-ttu-id="40c28-141">MapReduce, çeşitli dillerde uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="40c28-141">MapReduce can be implemented in various languages.</span></span> <span data-ttu-id="40c28-142">Java hello en yaygın uygulamasıdır ve bu belgedeki tanıtım amacıyla kullanılır.</span><span class="sxs-lookup"><span data-stu-id="40c28-142">Java is hello most common implementation, and is used for demonstration purposes in this document.</span></span>

## <a name="development-languages"></a><span data-ttu-id="40c28-143">Geliştirme dilleri</span><span class="sxs-lookup"><span data-stu-id="40c28-143">Development languages</span></span>

<span data-ttu-id="40c28-144">Diller veya Java'yı dayalı olan ve Java sanal makinesi hello çerçeveleri olması başlattıysanız doğrudan bir MapReduce işi.</span><span class="sxs-lookup"><span data-stu-id="40c28-144">Languages or frameworks that are based on Java and hello Java Virtual Machine can be ran directly as a MapReduce job.</span></span> <span data-ttu-id="40c28-145">Bu belgede kullanılan hello örnek bir Java MapReduce uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="40c28-145">hello example used in this document is a Java MapReduce application.</span></span> <span data-ttu-id="40c28-146">C#, Python veya tek başına yürütülebilir dosyaları, gibi olmayan Java diller, Hadoop akış kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="40c28-146">Non-Java languages, such as C#, Python, or standalone executables, must use Hadoop streaming.</span></span>

<span data-ttu-id="40c28-147">Hadoop akış hello Eşleyici ve reducer STDIN ve STDOUT üzerinden iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="40c28-147">Hadoop streaming communicates with hello mapper and reducer over STDIN and STDOUT.</span></span> <span data-ttu-id="40c28-148">Merhaba Eşleyici ve reducer STDIN aynı anda bir satır veri okuma ve hello çıktı tooSTDOUT yazma.</span><span class="sxs-lookup"><span data-stu-id="40c28-148">hello mapper and reducer read data a line at a time from STDIN, and write hello output tooSTDOUT.</span></span> <span data-ttu-id="40c28-149">Okuma veya hello Eşleyici ve reducer tarafından gösterilen her satır bir sekme karakteriyle ayrılmış bir anahtar/değer çifti hello biçiminde olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="40c28-149">Each line read or emitted by hello mapper and reducer must be in hello format of a key/value pair, delimited by a tab character:</span></span>

    [key]/t[value]

<span data-ttu-id="40c28-150">Daha fazla bilgi için bkz: [Hadoop akış](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span><span class="sxs-lookup"><span data-stu-id="40c28-150">For more information, see [Hadoop Streaming](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span></span>

<span data-ttu-id="40c28-151">Hdınsight ile akış Hadoop kullanım örnekleri için aşağıdaki belgeleri hello bakın:</span><span class="sxs-lookup"><span data-stu-id="40c28-151">For examples of using Hadoop streaming with HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="40c28-152">C# MapReduce işleri geliştirin</span><span class="sxs-lookup"><span data-stu-id="40c28-152">Develop C# MapReduce jobs</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="40c28-153">Python MapReduce işleri geliştirin</span><span class="sxs-lookup"><span data-stu-id="40c28-153">Develop Python MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="40c28-154"><a id="data"></a>Örnek veri</span><span class="sxs-lookup"><span data-stu-id="40c28-154"><a id="data"></a>Example data</span></span>

<span data-ttu-id="40c28-155">Hdınsight sağlar hello depolanan çeşitli örnek veri kümeleri, `/example/data` ve `/HdiSamples` dizin.</span><span class="sxs-lookup"><span data-stu-id="40c28-155">HDInsight provides various example data sets, which are stored in hello `/example/data` and `/HdiSamples` directory.</span></span> <span data-ttu-id="40c28-156">Bu dizinleri, kümeniz için hello varsayılan depolama arasındadır.</span><span class="sxs-lookup"><span data-stu-id="40c28-156">These directories are in hello default storage for your cluster.</span></span> <span data-ttu-id="40c28-157">Bu belgede, kullandığımız hello `/example/data/gutenberg/davinci.txt` dosya.</span><span class="sxs-lookup"><span data-stu-id="40c28-157">In this document, we use hello `/example/data/gutenberg/davinci.txt` file.</span></span> <span data-ttu-id="40c28-158">Bu dosya, Leonardo Da Vinci hello not defterlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="40c28-158">This file contains hello notebooks of Leonardo Da Vinci.</span></span>

## <span data-ttu-id="40c28-159"><a id="job"></a>Örnek MapReduce</span><span class="sxs-lookup"><span data-stu-id="40c28-159"><a id="job"></a>Example MapReduce</span></span>

<span data-ttu-id="40c28-160">Bir örnek MapReduce word sayısı uygulaması Hdınsight kümenize dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="40c28-160">An example MapReduce word count application is included with your HDInsight cluster.</span></span> <span data-ttu-id="40c28-161">Bu örnek adresindedir `/example/jars/hadoop-mapreduce-examples.jar` hello varsayılan depolama kümeniz için.</span><span class="sxs-lookup"><span data-stu-id="40c28-161">This example is located at `/example/jars/hadoop-mapreduce-examples.jar` on hello default storage for your cluster.</span></span>

<span data-ttu-id="40c28-162">Java kod aşağıdaki hello hello hello bulunan MapReduce uygulama hello kaynağı olan `hadoop-mapreduce-examples.jar` dosyası:</span><span class="sxs-lookup"><span data-stu-id="40c28-162">hello following Java code is hello source of hello MapReduce application contained in hello `hadoop-mapreduce-examples.jar` file:</span></span>

```java
package org.apache.hadoop.examples;

import java.io.IOException;
import java.util.StringTokenizer;

import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
import org.apache.hadoop.util.GenericOptionsParser;

public class WordCount {

    public static class TokenizerMapper
        extends Mapper<Object, Text, Text, IntWritable>{

    private final static IntWritable one = new IntWritable(1);
    private Text word = new Text();

    public void map(Object key, Text value, Context context
                    ) throws IOException, InterruptedException {
        StringTokenizer itr = new StringTokenizer(value.toString());
        while (itr.hasMoreTokens()) {
        word.set(itr.nextToken());
        context.write(word, one);
        }
    }
    }

    public static class IntSumReducer
        extends Reducer<Text,IntWritable,Text,IntWritable> {
    private IntWritable result = new IntWritable();

    public void reduce(Text key, Iterable<IntWritable> values,
                        Context context
                        ) throws IOException, InterruptedException {
        int sum = 0;
        for (IntWritable val : values) {
        sum += val.get();
        }
        result.set(sum);
        context.write(key, result);
    }
    }

    public static void main(String[] args) throws Exception {
    Configuration conf = new Configuration();
    String[] otherArgs = new GenericOptionsParser(conf, args).getRemainingArgs();
    if (otherArgs.length != 2) {
        System.err.println("Usage: wordcount <in> <out>");
        System.exit(2);
    }
    Job job = new Job(conf, "word count");
    job.setJarByClass(WordCount.class);
    job.setMapperClass(TokenizerMapper.class);
    job.setCombinerClass(IntSumReducer.class);
    job.setReducerClass(IntSumReducer.class);
    job.setOutputKeyClass(Text.class);
    job.setOutputValueClass(IntWritable.class);
    FileInputFormat.addInputPath(job, new Path(otherArgs[0]));
    FileOutputFormat.setOutputPath(job, new Path(otherArgs[1]));
    System.exit(job.waitForCompletion(true) ? 0 : 1);
    }
}
```

<span data-ttu-id="40c28-163">Kendi MapReduce uygulamalar için yönergeler toowrite belgeleri aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="40c28-163">For instructions toowrite your own MapReduce applications, see hello following documents:</span></span>

* [<span data-ttu-id="40c28-164">Hdınsight için Java MapReduce uygulamalar geliştirin</span><span class="sxs-lookup"><span data-stu-id="40c28-164">Develop Java MapReduce applications for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="40c28-165">Hdınsight için Python MapReduce uygulamalar geliştirin</span><span class="sxs-lookup"><span data-stu-id="40c28-165">Develop Python MapReduce applications for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="40c28-166"><a id="run"></a>Merhaba MapReduce çalıştırın</span><span class="sxs-lookup"><span data-stu-id="40c28-166"><a id="run"></a>Run hello MapReduce</span></span>

<span data-ttu-id="40c28-167">Hdınsight HiveQL işleri çeşitli yöntemleri kullanarak çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="40c28-167">HDInsight can run HiveQL jobs by using various methods.</span></span> <span data-ttu-id="40c28-168">Hangi yöntemi sizin için uygun olan tablo toodecide aşağıdaki hello kullanın ve sonra kılavuz hello bağlantıyı izleyin.</span><span class="sxs-lookup"><span data-stu-id="40c28-168">Use hello following table toodecide which method is right for you, then follow hello link for a walkthrough.</span></span>

| <span data-ttu-id="40c28-169">**Bu**...</span><span class="sxs-lookup"><span data-stu-id="40c28-169">**Use this**...</span></span> | <span data-ttu-id="40c28-170">**.. .toodo bu**</span><span class="sxs-lookup"><span data-stu-id="40c28-170">**...toodo this**</span></span> | <span data-ttu-id="40c28-171">.. hemen bu **küme işletim sistemi**</span><span class="sxs-lookup"><span data-stu-id="40c28-171">...with this **cluster operating system**</span></span> | <span data-ttu-id="40c28-172">.. .from bu **istemci işletim sistemi**</span><span class="sxs-lookup"><span data-stu-id="40c28-172">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="40c28-173">SSH</span><span class="sxs-lookup"><span data-stu-id="40c28-173">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="40c28-174">Merhaba Hadoop komutu aracılığıyla kullanmak **SSH**</span><span class="sxs-lookup"><span data-stu-id="40c28-174">Use hello Hadoop command through **SSH**</span></span> |<span data-ttu-id="40c28-175">Linux</span><span class="sxs-lookup"><span data-stu-id="40c28-175">Linux</span></span> |<span data-ttu-id="40c28-176">Linux, UNIX, Mac OS X veya Windows</span><span class="sxs-lookup"><span data-stu-id="40c28-176">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="40c28-177">Curl</span><span class="sxs-lookup"><span data-stu-id="40c28-177">Curl</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="40c28-178">Merhaba işi uzaktan kullanarak göndermek **REST**</span><span class="sxs-lookup"><span data-stu-id="40c28-178">Submit hello job remotely by using **REST**</span></span> |<span data-ttu-id="40c28-179">Linux veya Windows</span><span class="sxs-lookup"><span data-stu-id="40c28-179">Linux or Windows</span></span> |<span data-ttu-id="40c28-180">Linux, UNIX, Mac OS X veya Windows</span><span class="sxs-lookup"><span data-stu-id="40c28-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="40c28-181">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="40c28-181">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="40c28-182">Merhaba işi uzaktan kullanarak göndermek **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="40c28-182">Submit hello job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="40c28-183">Linux veya Windows</span><span class="sxs-lookup"><span data-stu-id="40c28-183">Linux or Windows</span></span> |<span data-ttu-id="40c28-184">Windows</span><span class="sxs-lookup"><span data-stu-id="40c28-184">Windows</span></span> |
| <span data-ttu-id="40c28-185">[Uzak Masaüstü](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (Hdınsight 3.2 ve 3.3)</span><span class="sxs-lookup"><span data-stu-id="40c28-185">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="40c28-186">Merhaba Hadoop komutu aracılığıyla kullanmak **Uzak Masaüstü**</span><span class="sxs-lookup"><span data-stu-id="40c28-186">Use hello Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="40c28-187">Windows</span><span class="sxs-lookup"><span data-stu-id="40c28-187">Windows</span></span> |<span data-ttu-id="40c28-188">Windows</span><span class="sxs-lookup"><span data-stu-id="40c28-188">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="40c28-189">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="40c28-189">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="40c28-190">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="40c28-190">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="40c28-191"><a id="nextsteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="40c28-191"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="40c28-192">Hdınsight, verileri ile çalışma hakkında daha fazla toolearn belgeleri aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="40c28-192">toolearn more about working with data in HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="40c28-193">Hdınsight için Java MapReduce programlar geliştirmek</span><span class="sxs-lookup"><span data-stu-id="40c28-193">Develop Java MapReduce programs for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="40c28-194">MapReduce programları Hdınsight için akış Python geliştirme</span><span class="sxs-lookup"><span data-stu-id="40c28-194">Develop Python streaming MapReduce programs for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

* [<span data-ttu-id="40c28-195">Hdınsight'ta Apache Hadoop ile Scalding MapReduce işleri geliştirin</span><span class="sxs-lookup"><span data-stu-id="40c28-195">Develop Scalding MapReduce jobs with Apache Hadoop on HDInsight</span></span>](hdinsight-hadoop-mapreduce-scalding.md)

* <span data-ttu-id="40c28-196">[HDInsight ile Hive kullanma][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="40c28-196">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>

* <span data-ttu-id="40c28-197">[HDInsight ile Pig kullanma][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="40c28-197">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>


[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-develop-mapreduce-jobs]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-wordcountdiagram]: ./media/hdinsight-use-mapreduce/HDI.WordCountDiagram.gif
