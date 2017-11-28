---
title: "Hdınsight'ta Hadoop ile MapReduce | Microsoft Docs"
description: "Hdınsight kümelerinde Hadoop MapReduce işleri çalıştırmayı öğrenin."
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
ms.openlocfilehash: df8ac578a56de72df667b1fa7f90f981c79d9999
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight"></a><span data-ttu-id="3440b-103">Hdınsight'ta Hadoop MapReduce kullanın</span><span class="sxs-lookup"><span data-stu-id="3440b-103">Use MapReduce in Hadoop on HDInsight</span></span>

<span data-ttu-id="3440b-104">Hdınsight kümelerinde MapReduce işleri çalıştırmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="3440b-104">Learn how to run MapReduce jobs on HDInsight clusters.</span></span> <span data-ttu-id="3440b-105">MapReduce kullanılabilir çeşitli şekillerde bulmak için aşağıdaki tabloyu kullanın Hdınsight ile:</span><span class="sxs-lookup"><span data-stu-id="3440b-105">Use the following table to discover the various ways that MapReduce can be used with HDInsight:</span></span>

| <span data-ttu-id="3440b-106">**Bu**...</span><span class="sxs-lookup"><span data-stu-id="3440b-106">**Use this**...</span></span> | <span data-ttu-id="3440b-107">**.. .bilgisayarınızın bunu**</span><span class="sxs-lookup"><span data-stu-id="3440b-107">**...to do this**</span></span> | <span data-ttu-id="3440b-108">.. hemen bu **küme işletim sistemi**</span><span class="sxs-lookup"><span data-stu-id="3440b-108">...with this **cluster operating system**</span></span> | <span data-ttu-id="3440b-109">.. .from bu **istemci işletim sistemi**</span><span class="sxs-lookup"><span data-stu-id="3440b-109">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="3440b-110">SSH</span><span class="sxs-lookup"><span data-stu-id="3440b-110">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="3440b-111">Hadoop komutu aracılığıyla kullanmak **SSH**</span><span class="sxs-lookup"><span data-stu-id="3440b-111">Use the Hadoop command through **SSH**</span></span> |<span data-ttu-id="3440b-112">Linux</span><span class="sxs-lookup"><span data-stu-id="3440b-112">Linux</span></span> |<span data-ttu-id="3440b-113">Linux, UNIX, Mac OS X veya Windows</span><span class="sxs-lookup"><span data-stu-id="3440b-113">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="3440b-114">REST</span><span class="sxs-lookup"><span data-stu-id="3440b-114">REST</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="3440b-115">İşi uzaktan kullanarak göndermek **REST** (örnekler cURL kullanın)</span><span class="sxs-lookup"><span data-stu-id="3440b-115">Submit the job remotely by using **REST** (examples use cURL)</span></span> |<span data-ttu-id="3440b-116">Linux veya Windows</span><span class="sxs-lookup"><span data-stu-id="3440b-116">Linux or Windows</span></span> |<span data-ttu-id="3440b-117">Linux, UNIX, Mac OS X veya Windows</span><span class="sxs-lookup"><span data-stu-id="3440b-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="3440b-118">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="3440b-118">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="3440b-119">İşi uzaktan kullanarak göndermek **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="3440b-119">Submit the job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="3440b-120">Linux veya Windows</span><span class="sxs-lookup"><span data-stu-id="3440b-120">Linux or Windows</span></span> |<span data-ttu-id="3440b-121">Windows</span><span class="sxs-lookup"><span data-stu-id="3440b-121">Windows</span></span> |
| <span data-ttu-id="3440b-122">[Uzak Masaüstü](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (Hdınsight 3.2 ve 3.3)</span><span class="sxs-lookup"><span data-stu-id="3440b-122">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="3440b-123">Hadoop komutu aracılığıyla kullanmak **Uzak Masaüstü**</span><span class="sxs-lookup"><span data-stu-id="3440b-123">Use the Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="3440b-124">Windows</span><span class="sxs-lookup"><span data-stu-id="3440b-124">Windows</span></span> |<span data-ttu-id="3440b-125">Windows</span><span class="sxs-lookup"><span data-stu-id="3440b-125">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="3440b-126">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="3440b-126">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3440b-127">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="3440b-127">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="3440b-128"><a id="whatis"></a>MapReduce nedir</span><span class="sxs-lookup"><span data-stu-id="3440b-128"><a id="whatis"></a>What is MapReduce</span></span>

<span data-ttu-id="3440b-129">Hadoop MapReduce, çok büyük miktarda veri işleyen işlerini yazmak için bir yazılım çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="3440b-129">Hadoop MapReduce is a software framework for writing jobs that process vast amounts of data.</span></span> <span data-ttu-id="3440b-130">Giriş verisi ardından düğümler arasında paralel olarak işlenen bağımsız parçalara bölünür.</span><span class="sxs-lookup"><span data-stu-id="3440b-130">Input data is split into independent chunks, which are then processed in parallel across the nodes in your cluster.</span></span> <span data-ttu-id="3440b-131">Bir MapReduce işi, iki işlevden oluşur:</span><span class="sxs-lookup"><span data-stu-id="3440b-131">A MapReduce job consists of two functions:</span></span>

* <span data-ttu-id="3440b-132">**Eşleyici**: giriş verileri kullanır (genellikle filtre ve sıralama işlemleri ile) çözümler ve diziler (anahtar-değer çiftleri) yayar</span><span class="sxs-lookup"><span data-stu-id="3440b-132">**Mapper**: Consumes input data, analyzes it (usually with filter and sorting operations), and emits tuples (key-value pairs)</span></span>

* <span data-ttu-id="3440b-133">**Reducer**: Eşleyicisi tarafından gösterilen diziler kullanır ve Eşleyici verilerden daha küçük, birleşik bir sonuç oluşturur Özet bir işlemi gerçekleştirir</span><span class="sxs-lookup"><span data-stu-id="3440b-133">**Reducer**: Consumes tuples emitted by the Mapper and performs a summary operation that creates a smaller, combined result from the Mapper data</span></span>

<span data-ttu-id="3440b-134">Aşağıdaki şemada temel word sayısı MapReduce işi örneği gösterilmiştir:</span><span class="sxs-lookup"><span data-stu-id="3440b-134">A basic word count MapReduce job example is illustrated in the following diagram:</span></span>

![HDI. WordCountDiagram][image-hdi-wordcountdiagram]

<span data-ttu-id="3440b-136">Bu iş çıktısı, her sözcüğün analiz edildi metinde oluştu kaç kez sayısıdır.</span><span class="sxs-lookup"><span data-stu-id="3440b-136">The output of this job is a count of how many times each word occurred in the text that was analyzed.</span></span>

* <span data-ttu-id="3440b-137">Eşleyici her bir girdi olarak giriş metin satırından alır ve sözcüklere böler.</span><span class="sxs-lookup"><span data-stu-id="3440b-137">The mapper takes each line from the input text as an input and breaks it into words.</span></span> <span data-ttu-id="3440b-138">Bir anahtar/değer yayar çifti bir sözcük sözcüğün her oluştuğunda bir 1 tarafından izlendiği.</span><span class="sxs-lookup"><span data-stu-id="3440b-138">It emits a key/value pair each time a word occurs of the word is followed by a 1.</span></span> <span data-ttu-id="3440b-139">Çıktı için reducer göndermeden önce sıralanır.</span><span class="sxs-lookup"><span data-stu-id="3440b-139">The output is sorted before sending it to reducer.</span></span>
* <span data-ttu-id="3440b-140">Reducer her sözcüğün için bu tek tek sayıları toplar ve onun oluşum toplamı tarafından izlenen sözcüğünü içeren bir tek anahtar/değer çifti yayar.</span><span class="sxs-lookup"><span data-stu-id="3440b-140">The reducer sums these individual counts for each word and emits a single key/value pair that contains the word followed by the sum of its occurrences.</span></span>

<span data-ttu-id="3440b-141">MapReduce, çeşitli dillerde uygulanabilir.</span><span class="sxs-lookup"><span data-stu-id="3440b-141">MapReduce can be implemented in various languages.</span></span> <span data-ttu-id="3440b-142">Java en yaygın uygulamasıdır ve bu belgedeki tanıtım amacıyla kullanılır.</span><span class="sxs-lookup"><span data-stu-id="3440b-142">Java is the most common implementation, and is used for demonstration purposes in this document.</span></span>

## <a name="development-languages"></a><span data-ttu-id="3440b-143">Geliştirme dilleri</span><span class="sxs-lookup"><span data-stu-id="3440b-143">Development languages</span></span>

<span data-ttu-id="3440b-144">Diller veya Java ve Java sanal makinesi bağlı çerçeveler olması başlattıysanız doğrudan bir MapReduce işi.</span><span class="sxs-lookup"><span data-stu-id="3440b-144">Languages or frameworks that are based on Java and the Java Virtual Machine can be ran directly as a MapReduce job.</span></span> <span data-ttu-id="3440b-145">Bu belgede kullanılan örnekte, bir Java MapReduce uygulamasıdır.</span><span class="sxs-lookup"><span data-stu-id="3440b-145">The example used in this document is a Java MapReduce application.</span></span> <span data-ttu-id="3440b-146">C#, Python veya tek başına yürütülebilir dosyaları, gibi olmayan Java diller, Hadoop akış kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3440b-146">Non-Java languages, such as C#, Python, or standalone executables, must use Hadoop streaming.</span></span>

<span data-ttu-id="3440b-147">Hadoop akış Eşleyici ve reducer STDIN ve STDOUT üzerinden iletişim kurar.</span><span class="sxs-lookup"><span data-stu-id="3440b-147">Hadoop streaming communicates with the mapper and reducer over STDIN and STDOUT.</span></span> <span data-ttu-id="3440b-148">Eşleyici ve reducer STDIN aynı anda bir satır veri okuma ve çıktı STDOUT yazma.</span><span class="sxs-lookup"><span data-stu-id="3440b-148">The mapper and reducer read data a line at a time from STDIN, and write the output to STDOUT.</span></span> <span data-ttu-id="3440b-149">Okuma veya Eşleyici ve reducer tarafından gösterilen her satır bir sekme karakteriyle ayrılmış bir anahtar/değer çifti biçiminde olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="3440b-149">Each line read or emitted by the mapper and reducer must be in the format of a key/value pair, delimited by a tab character:</span></span>

    [key]/t[value]

<span data-ttu-id="3440b-150">Daha fazla bilgi için bkz: [Hadoop akış](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span><span class="sxs-lookup"><span data-stu-id="3440b-150">For more information, see [Hadoop Streaming](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span></span>

<span data-ttu-id="3440b-151">Hdınsight ile akış Hadoop kullanım örnekleri için aşağıdaki belgelere bakın:</span><span class="sxs-lookup"><span data-stu-id="3440b-151">For examples of using Hadoop streaming with HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="3440b-152">C# MapReduce işleri geliştirin</span><span class="sxs-lookup"><span data-stu-id="3440b-152">Develop C# MapReduce jobs</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="3440b-153">Python MapReduce işleri geliştirin</span><span class="sxs-lookup"><span data-stu-id="3440b-153">Develop Python MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="3440b-154"><a id="data"></a>Örnek veri</span><span class="sxs-lookup"><span data-stu-id="3440b-154"><a id="data"></a>Example data</span></span>

<span data-ttu-id="3440b-155">Hdınsight içinde depolanan çeşitli örnek veri kümeleri, sağlar `/example/data` ve `/HdiSamples` dizin.</span><span class="sxs-lookup"><span data-stu-id="3440b-155">HDInsight provides various example data sets, which are stored in the `/example/data` and `/HdiSamples` directory.</span></span> <span data-ttu-id="3440b-156">Bu dizinleri, kümeniz için varsayılan depolama arasındadır.</span><span class="sxs-lookup"><span data-stu-id="3440b-156">These directories are in the default storage for your cluster.</span></span> <span data-ttu-id="3440b-157">Bu belgede, kullandığımız `/example/data/gutenberg/davinci.txt` dosya.</span><span class="sxs-lookup"><span data-stu-id="3440b-157">In this document, we use the `/example/data/gutenberg/davinci.txt` file.</span></span> <span data-ttu-id="3440b-158">Bu dosya Leonardo Da Vinci not defterlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="3440b-158">This file contains the notebooks of Leonardo Da Vinci.</span></span>

## <span data-ttu-id="3440b-159"><a id="job"></a>Örnek MapReduce</span><span class="sxs-lookup"><span data-stu-id="3440b-159"><a id="job"></a>Example MapReduce</span></span>

<span data-ttu-id="3440b-160">Bir örnek MapReduce word sayısı uygulaması Hdınsight kümenize dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="3440b-160">An example MapReduce word count application is included with your HDInsight cluster.</span></span> <span data-ttu-id="3440b-161">Bu örnek adresindedir `/example/jars/hadoop-mapreduce-examples.jar` kümeniz için varsayılan depolama.</span><span class="sxs-lookup"><span data-stu-id="3440b-161">This example is located at `/example/jars/hadoop-mapreduce-examples.jar` on the default storage for your cluster.</span></span>

<span data-ttu-id="3440b-162">Aşağıdaki Java kod içinde yer alan MapReduce uygulama kaynağıdır `hadoop-mapreduce-examples.jar` dosyası:</span><span class="sxs-lookup"><span data-stu-id="3440b-162">The following Java code is the source of the MapReduce application contained in the `hadoop-mapreduce-examples.jar` file:</span></span>

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

<span data-ttu-id="3440b-163">Kendi MapReduce uygulamaları yazmak yönergeler için aşağıdaki belgelere bakın:</span><span class="sxs-lookup"><span data-stu-id="3440b-163">For instructions to write your own MapReduce applications, see the following documents:</span></span>

* [<span data-ttu-id="3440b-164">Hdınsight için Java MapReduce uygulamalar geliştirin</span><span class="sxs-lookup"><span data-stu-id="3440b-164">Develop Java MapReduce applications for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="3440b-165">Hdınsight için Python MapReduce uygulamalar geliştirin</span><span class="sxs-lookup"><span data-stu-id="3440b-165">Develop Python MapReduce applications for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="3440b-166"><a id="run"></a>MapReduce Çalıştır</span><span class="sxs-lookup"><span data-stu-id="3440b-166"><a id="run"></a>Run the MapReduce</span></span>

<span data-ttu-id="3440b-167">Hdınsight HiveQL işleri çeşitli yöntemleri kullanarak çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3440b-167">HDInsight can run HiveQL jobs by using various methods.</span></span> <span data-ttu-id="3440b-168">Hangi yöntemi sizin için uygun olduğuna karar vermek için aşağıdaki tabloyu kullanın, sonra bir anlatım için bağlantıyı izleyin.</span><span class="sxs-lookup"><span data-stu-id="3440b-168">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span></span>

| <span data-ttu-id="3440b-169">**Bu**...</span><span class="sxs-lookup"><span data-stu-id="3440b-169">**Use this**...</span></span> | <span data-ttu-id="3440b-170">**.. .bilgisayarınızın bunu**</span><span class="sxs-lookup"><span data-stu-id="3440b-170">**...to do this**</span></span> | <span data-ttu-id="3440b-171">.. hemen bu **küme işletim sistemi**</span><span class="sxs-lookup"><span data-stu-id="3440b-171">...with this **cluster operating system**</span></span> | <span data-ttu-id="3440b-172">.. .from bu **istemci işletim sistemi**</span><span class="sxs-lookup"><span data-stu-id="3440b-172">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="3440b-173">SSH</span><span class="sxs-lookup"><span data-stu-id="3440b-173">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="3440b-174">Hadoop komutu aracılığıyla kullanmak **SSH**</span><span class="sxs-lookup"><span data-stu-id="3440b-174">Use the Hadoop command through **SSH**</span></span> |<span data-ttu-id="3440b-175">Linux</span><span class="sxs-lookup"><span data-stu-id="3440b-175">Linux</span></span> |<span data-ttu-id="3440b-176">Linux, UNIX, Mac OS X veya Windows</span><span class="sxs-lookup"><span data-stu-id="3440b-176">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="3440b-177">Curl</span><span class="sxs-lookup"><span data-stu-id="3440b-177">Curl</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="3440b-178">İşi uzaktan kullanarak göndermek **REST**</span><span class="sxs-lookup"><span data-stu-id="3440b-178">Submit the job remotely by using **REST**</span></span> |<span data-ttu-id="3440b-179">Linux veya Windows</span><span class="sxs-lookup"><span data-stu-id="3440b-179">Linux or Windows</span></span> |<span data-ttu-id="3440b-180">Linux, UNIX, Mac OS X veya Windows</span><span class="sxs-lookup"><span data-stu-id="3440b-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="3440b-181">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="3440b-181">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="3440b-182">İşi uzaktan kullanarak göndermek **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="3440b-182">Submit the job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="3440b-183">Linux veya Windows</span><span class="sxs-lookup"><span data-stu-id="3440b-183">Linux or Windows</span></span> |<span data-ttu-id="3440b-184">Windows</span><span class="sxs-lookup"><span data-stu-id="3440b-184">Windows</span></span> |
| <span data-ttu-id="3440b-185">[Uzak Masaüstü](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (Hdınsight 3.2 ve 3.3)</span><span class="sxs-lookup"><span data-stu-id="3440b-185">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="3440b-186">Hadoop komutu aracılığıyla kullanmak **Uzak Masaüstü**</span><span class="sxs-lookup"><span data-stu-id="3440b-186">Use the Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="3440b-187">Windows</span><span class="sxs-lookup"><span data-stu-id="3440b-187">Windows</span></span> |<span data-ttu-id="3440b-188">Windows</span><span class="sxs-lookup"><span data-stu-id="3440b-188">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="3440b-189">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="3440b-189">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3440b-190">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="3440b-190">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="3440b-191"><a id="nextsteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3440b-191"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="3440b-192">Hdınsight'ta verilerle çalışma hakkında daha fazla bilgi için aşağıdaki belgelere bakın:</span><span class="sxs-lookup"><span data-stu-id="3440b-192">To learn more about working with data in HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="3440b-193">Hdınsight için Java MapReduce programlar geliştirmek</span><span class="sxs-lookup"><span data-stu-id="3440b-193">Develop Java MapReduce programs for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="3440b-194">MapReduce programları Hdınsight için akış Python geliştirme</span><span class="sxs-lookup"><span data-stu-id="3440b-194">Develop Python streaming MapReduce programs for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

* [<span data-ttu-id="3440b-195">Hdınsight'ta Apache Hadoop ile Scalding MapReduce işleri geliştirin</span><span class="sxs-lookup"><span data-stu-id="3440b-195">Develop Scalding MapReduce jobs with Apache Hadoop on HDInsight</span></span>](hdinsight-hadoop-mapreduce-scalding.md)

* <span data-ttu-id="3440b-196">[HDInsight ile Hive kullanma][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="3440b-196">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>

* <span data-ttu-id="3440b-197">[HDInsight ile Pig kullanma][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="3440b-197">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>


[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-develop-mapreduce-jobs]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-wordcountdiagram]: ./media/hdinsight-use-mapreduce/HDI.WordCountDiagram.gif
