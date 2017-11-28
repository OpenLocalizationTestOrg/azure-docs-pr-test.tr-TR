---
title: "hdınsight'ta Hadoop Pig aaaUse | Microsoft Docs"
description: "Bilgi nasıl toouse Pig hdınsight'ta Hadoop ile."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: acfeb52b-4b81-4a7d-af77-3e9908407404
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 90850f2c742b8954c66ce277127e01b14fc3906f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-pig-with-hadoop-on-hdinsight"></a><span data-ttu-id="6d59d-103">Hdınsight'ta Hadoop ile pig kullanma</span><span class="sxs-lookup"><span data-stu-id="6d59d-103">Use Pig with Hadoop on HDInsight</span></span>

<span data-ttu-id="6d59d-104">Bilgi nasıl toouse [Apache Pig](http://pig.apache.org/) Hdınsight ile...</span><span class="sxs-lookup"><span data-stu-id="6d59d-104">Learn how toouse [Apache Pig](http://pig.apache.org/) with HDInsight...</span></span>

<span data-ttu-id="6d59d-105">Pig olan bir platform olarak bilinen bir yordam dilini kullanarak Hadoop için programlar oluşturma için *Pig Latin*.</span><span class="sxs-lookup"><span data-stu-id="6d59d-105">Pig is a platform for creating programs for Hadoop by using a procedural language known as *Pig Latin*.</span></span> <span data-ttu-id="6d59d-106">Pig olan oluşturmak için bir alternatif tooJava *MapReduce* çözümleri ve bunu Azure Hdınsight ile birlikte.</span><span class="sxs-lookup"><span data-stu-id="6d59d-106">Pig is an alternative tooJava for creating *MapReduce* solutions, and it is included with Azure HDInsight.</span></span> <span data-ttu-id="6d59d-107">Aşağıdaki tablo toodiscover hello Hdınsight ile Pig kullanılabilir çeşitli şekillerde hello kullan:</span><span class="sxs-lookup"><span data-stu-id="6d59d-107">Use hello following table toodiscover hello various ways that Pig can be used with HDInsight:</span></span>

| <span data-ttu-id="6d59d-108">**Bu** isterseniz...</span><span class="sxs-lookup"><span data-stu-id="6d59d-108">**Use this** if you want...</span></span> | <span data-ttu-id="6d59d-109">.. .an **etkileşimli** Kabuk</span><span class="sxs-lookup"><span data-stu-id="6d59d-109">...an **interactive** shell</span></span> | <span data-ttu-id="6d59d-110">... **toplu** işleme</span><span class="sxs-lookup"><span data-stu-id="6d59d-110">...**batch** processing</span></span> | <span data-ttu-id="6d59d-111">.. hemen bu **küme işletim sistemi**</span><span class="sxs-lookup"><span data-stu-id="6d59d-111">...with this **cluster operating system**</span></span> | <span data-ttu-id="6d59d-112">.. .from bu **istemci işletim sistemi**</span><span class="sxs-lookup"><span data-stu-id="6d59d-112">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="6d59d-113">SSH</span><span class="sxs-lookup"><span data-stu-id="6d59d-113">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="6d59d-114">✔</span><span class="sxs-lookup"><span data-stu-id="6d59d-114">✔</span></span> |<span data-ttu-id="6d59d-115">✔</span><span class="sxs-lookup"><span data-stu-id="6d59d-115">✔</span></span> |<span data-ttu-id="6d59d-116">Linux</span><span class="sxs-lookup"><span data-stu-id="6d59d-116">Linux</span></span> |<span data-ttu-id="6d59d-117">Linux, UNIX, Mac OS X veya Windows</span><span class="sxs-lookup"><span data-stu-id="6d59d-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="6d59d-118">REST API</span><span class="sxs-lookup"><span data-stu-id="6d59d-118">REST API</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="6d59d-119">✔</span><span class="sxs-lookup"><span data-stu-id="6d59d-119">✔</span></span> |<span data-ttu-id="6d59d-120">Linux veya Windows</span><span class="sxs-lookup"><span data-stu-id="6d59d-120">Linux or Windows</span></span> |<span data-ttu-id="6d59d-121">Linux, UNIX, Mac OS X veya Windows</span><span class="sxs-lookup"><span data-stu-id="6d59d-121">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="6d59d-122">Hadoop için .NET SDK</span><span class="sxs-lookup"><span data-stu-id="6d59d-122">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="6d59d-123">✔</span><span class="sxs-lookup"><span data-stu-id="6d59d-123">✔</span></span> |<span data-ttu-id="6d59d-124">Linux veya Windows</span><span class="sxs-lookup"><span data-stu-id="6d59d-124">Linux or Windows</span></span> |<span data-ttu-id="6d59d-125">Windows (için şimdi)</span><span class="sxs-lookup"><span data-stu-id="6d59d-125">Windows (for now)</span></span> |
| [<span data-ttu-id="6d59d-126">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="6d59d-126">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="6d59d-127">✔</span><span class="sxs-lookup"><span data-stu-id="6d59d-127">✔</span></span> |<span data-ttu-id="6d59d-128">Linux veya Windows</span><span class="sxs-lookup"><span data-stu-id="6d59d-128">Linux or Windows</span></span> |<span data-ttu-id="6d59d-129">Windows</span><span class="sxs-lookup"><span data-stu-id="6d59d-129">Windows</span></span> |
| <span data-ttu-id="6d59d-130">[Uzak Masaüstü](hdinsight-hadoop-use-pig-remote-desktop.md) (Hdınsight 3.2 ve 3.3)</span><span class="sxs-lookup"><span data-stu-id="6d59d-130">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="6d59d-131">✔</span><span class="sxs-lookup"><span data-stu-id="6d59d-131">✔</span></span> |<span data-ttu-id="6d59d-132">✔</span><span class="sxs-lookup"><span data-stu-id="6d59d-132">✔</span></span> |<span data-ttu-id="6d59d-133">Windows</span><span class="sxs-lookup"><span data-stu-id="6d59d-133">Windows</span></span> |<span data-ttu-id="6d59d-134">Windows</span><span class="sxs-lookup"><span data-stu-id="6d59d-134">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="6d59d-135">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="6d59d-135">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6d59d-136">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="6d59d-136">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="6d59d-137"><a id="why"></a>Pig neden kullanılır?</span><span class="sxs-lookup"><span data-stu-id="6d59d-137"><a id="why"></a>Why use Pig</span></span>

<span data-ttu-id="6d59d-138">Hadoop MapReduce kullanarak veri işleme hello zorluklardan biri, işleme mantığı yalnızca bir eşleme ve azaltma işlevini kullanarak uygular.</span><span class="sxs-lookup"><span data-stu-id="6d59d-138">One of hello challenges of processing data by using MapReduce in Hadoop is implementing your processing logic by using only a map and a reduce function.</span></span> <span data-ttu-id="6d59d-139">Genellikle karmaşık işleme sahip olan birden çok MapReduce işlemlere işleme toobreak tooachieve istenen hello sonuç birbirine zincirlenmiş.</span><span class="sxs-lookup"><span data-stu-id="6d59d-139">For complex processing, you often have toobreak processing into multiple MapReduce operations that are chained together tooachieve hello desired result.</span></span>

<span data-ttu-id="6d59d-140">Pig tooproduce hello istenen çıkış aracılığıyla veri akışları hello dönüşümleri bir dizi olarak işleme toodefine sağlar.</span><span class="sxs-lookup"><span data-stu-id="6d59d-140">Pig allows you toodefine processing as a series of transformations that hello data flows through tooproduce hello desired output.</span></span>

<span data-ttu-id="6d59d-141">Merhaba Pig Latin dili, toodescribe hello veri akışından bir veya daha fazla dönüşümleri, tooproduce hello istenen çıkış aracılığıyla ham giriş sağlar.</span><span class="sxs-lookup"><span data-stu-id="6d59d-141">hello Pig Latin language allows you toodescribe hello data flow from raw input, through one or more transformations, tooproduce hello desired output.</span></span> <span data-ttu-id="6d59d-142">Pig Latin programlar bu genel model izleyin:</span><span class="sxs-lookup"><span data-stu-id="6d59d-142">Pig Latin programs follow this general pattern:</span></span>

* <span data-ttu-id="6d59d-143">**Yük**: hello dosya sisteminden yönetilen veri toobe okuma</span><span class="sxs-lookup"><span data-stu-id="6d59d-143">**Load**: Read data toobe manipulated from hello file system</span></span>

* <span data-ttu-id="6d59d-144">**Dönüştürme**: hello verileri işlemek</span><span class="sxs-lookup"><span data-stu-id="6d59d-144">**Transform**: Manipulate hello data</span></span>

* <span data-ttu-id="6d59d-145">**Döküm veya mağaza**: çıktı veri toohello ekran veya işleme için mağaza</span><span class="sxs-lookup"><span data-stu-id="6d59d-145">**Dump or store**: Output data toohello screen or store it for processing</span></span>

### <a name="user-defined-functions"></a><span data-ttu-id="6d59d-146">Kullanıcı tanımlı işlevler</span><span class="sxs-lookup"><span data-stu-id="6d59d-146">User-defined functions</span></span>

<span data-ttu-id="6d59d-147">Pig Latin kullanıcı tanımlı işlevler (UDF), Pig Latin içinde zor toomodel mantığı uygulamak tooinvoke dış bileşenlere sağlayan de destekler.</span><span class="sxs-lookup"><span data-stu-id="6d59d-147">Pig Latin also supports user-defined functions (UDF), which allows you tooinvoke external components that implement logic that is difficult toomodel in Pig Latin.</span></span>

<span data-ttu-id="6d59d-148">Pig Latin hakkında daha fazla bilgi için bkz: [Pig Latin başvuru el ile 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) ve [Pig Latin başvuru el ile 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).</span><span class="sxs-lookup"><span data-stu-id="6d59d-148">For more information about Pig Latin, see [Pig Latin Reference Manual 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) and [Pig Latin Reference Manual 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).</span></span>

<span data-ttu-id="6d59d-149">UDF'ler ile Pig kullanma örneği için aşağıdaki belgeleri hello bakın:</span><span class="sxs-lookup"><span data-stu-id="6d59d-149">For an example of using UDFs with Pig, see hello following documents:</span></span>

* <span data-ttu-id="6d59d-150">[Pig hdınsight'ta ile DataFu kullanmak](hdinsight-hadoop-use-pig-datafu-udf.md) -DataFu Apache tarafından tutulan yararlı UDF'ler koleksiyonudur</span><span class="sxs-lookup"><span data-stu-id="6d59d-150">[Use DataFu with Pig in HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) - DataFu is a collection of useful UDFs maintained by Apache</span></span>
* [<span data-ttu-id="6d59d-151">Python Pig ve hdınsight'ta Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="6d59d-151">Use Python with Pig and Hive in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="6d59d-152">C# Hive veya Pig hdınsight'ta ile kullanma</span><span class="sxs-lookup"><span data-stu-id="6d59d-152">Use C# with Hive and Pig in HDInsight</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

## <span data-ttu-id="6d59d-153"><a id="data"></a>Örnek veri</span><span class="sxs-lookup"><span data-stu-id="6d59d-153"><a id="data"></a>Example data</span></span>

<span data-ttu-id="6d59d-154">Hdınsight sağlar hello depolanan çeşitli örnek veri kümeleri, `/example/data` ve `/HdiSamples` dizinleri.</span><span class="sxs-lookup"><span data-stu-id="6d59d-154">HDInsight provides various example data sets, which are stored in hello `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="6d59d-155">Bu dizinleri, kümeniz için hello varsayılan depolama arasındadır.</span><span class="sxs-lookup"><span data-stu-id="6d59d-155">These directories are in hello default storage for your cluster.</span></span> <span data-ttu-id="6d59d-156">Bu belgedeki Hello Pig örnek kullanır hello *log4j* dosya `/example/data/sample.log`.</span><span class="sxs-lookup"><span data-stu-id="6d59d-156">hello Pig example in this document uses hello *log4j* file from `/example/data/sample.log`.</span></span>

<span data-ttu-id="6d59d-157">Hello dosyası içindeki her bir günlükteki içeren bir dizi alanlarının oluşan bir `[LOG LEVEL]` alan tooshow hello türü ve hello önem derecesi, örneğin:</span><span class="sxs-lookup"><span data-stu-id="6d59d-157">Each log inside hello file consists of a line of fields that contains a `[LOG LEVEL]` field tooshow hello type and hello severity, for example:</span></span>

    2012-02-03 20:26:41 SampleClass3 [ERROR] verbose detail for id 1527353937

<span data-ttu-id="6d59d-158">Merhaba önceki örnekte hello günlük düzeyi hatasıdır.</span><span class="sxs-lookup"><span data-stu-id="6d59d-158">In hello previous example, hello log level is ERROR.</span></span>

> [!NOTE]
> <span data-ttu-id="6d59d-159">Hello kullanarak log4j dosyasını oluşturabilirsiniz [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) aracı günlüğe kaydetme ve bu dosyayı tooyour blob karşıya yükleyin.</span><span class="sxs-lookup"><span data-stu-id="6d59d-159">You can also generate a log4j file by using hello [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) logging tool and then upload that file tooyour blob.</span></span> <span data-ttu-id="6d59d-160">Bkz: [karşıya veri tooHDInsight](hdinsight-upload-data.md) yönergeler için.</span><span class="sxs-lookup"><span data-stu-id="6d59d-160">See [Upload Data tooHDInsight](hdinsight-upload-data.md) for instructions.</span></span> <span data-ttu-id="6d59d-161">BLOB'ları Azure depolama alanında Hdınsight ile nasıl kullanıldığı konusunda daha fazla bilgi için bkz: [kullanım Azure Blob Storage Hdınsight ile](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="6d59d-161">For more information about how blobs in Azure storage are used with HDInsight, see [Use Azure Blob Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>

## <span data-ttu-id="6d59d-162"><a id="job"></a>Örnek Proje</span><span class="sxs-lookup"><span data-stu-id="6d59d-162"><a id="job"></a>Example job</span></span>

<span data-ttu-id="6d59d-163">Merhaba aşağıdaki Pig Latin iş yükler hello `sample.log` Hdınsight kümenizin hello varsayılan depolama biriminden dosya.</span><span class="sxs-lookup"><span data-stu-id="6d59d-163">hello following Pig Latin job loads hello `sample.log` file from hello default storage for your HDInsight cluster.</span></span> <span data-ttu-id="6d59d-164">Ardından, bir dizi nasıl sayıma birçok kez her günlük düzeyi içinde oluştu hello giriş verilerini neden dönüşümleri gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="6d59d-164">Then it performs a series of transformations that result in a count of how many times each log level occurred in hello input data.</span></span> <span data-ttu-id="6d59d-165">Merhaba sonuçları tooSTDOUT yazılır.</span><span class="sxs-lookup"><span data-stu-id="6d59d-165">hello results are written tooSTDOUT.</span></span>

    LOGS = LOAD 'wasb:///example/data/sample.log';
    LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
    FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
    GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
    FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
    RESULT = order FREQUENCIES by COUNT desc;
    DUMP RESULT;

<span data-ttu-id="6d59d-166">Merhaba aşağıdaki görüntüde her hangi bir dönüşüm toohello veri mu özetini gösterir.</span><span class="sxs-lookup"><span data-stu-id="6d59d-166">hello following image shows a summary of what each transformation does toohello data.</span></span>

![Merhaba dönüşümleri grafik gösterimi][image-hdi-pig-data-transformation]

## <span data-ttu-id="6d59d-168"><a id="run"></a>Merhaba Pig Latin işini çalıştır</span><span class="sxs-lookup"><span data-stu-id="6d59d-168"><a id="run"></a>Run hello Pig Latin job</span></span>

<span data-ttu-id="6d59d-169">Hdınsight, Pig Latin işleri çeşitli yöntemler kullanarak çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d59d-169">HDInsight can run Pig Latin jobs by using a variety of methods.</span></span> <span data-ttu-id="6d59d-170">Hangi yöntemi sizin için uygun olan tablo toodecide aşağıdaki hello kullanın ve sonra kılavuz hello bağlantıyı izleyin.</span><span class="sxs-lookup"><span data-stu-id="6d59d-170">Use hello following table toodecide which method is right for you, then follow hello link for a walkthrough.</span></span>

| <span data-ttu-id="6d59d-171">**Bu** isterseniz...</span><span class="sxs-lookup"><span data-stu-id="6d59d-171">**Use this** if you want...</span></span> | <span data-ttu-id="6d59d-172">.. .an **etkileşimli** Kabuk</span><span class="sxs-lookup"><span data-stu-id="6d59d-172">...an **interactive** shell</span></span> | <span data-ttu-id="6d59d-173">... **toplu** işleme</span><span class="sxs-lookup"><span data-stu-id="6d59d-173">...**batch** processing</span></span> | <span data-ttu-id="6d59d-174">.. hemen bu **küme işletim sistemi**</span><span class="sxs-lookup"><span data-stu-id="6d59d-174">...with this **cluster operating system**</span></span> | <span data-ttu-id="6d59d-175">.. .from bu **istemci**</span><span class="sxs-lookup"><span data-stu-id="6d59d-175">...from this **client**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="6d59d-176">SSH</span><span class="sxs-lookup"><span data-stu-id="6d59d-176">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="6d59d-177">✔</span><span class="sxs-lookup"><span data-stu-id="6d59d-177">✔</span></span> |<span data-ttu-id="6d59d-178">✔</span><span class="sxs-lookup"><span data-stu-id="6d59d-178">✔</span></span> |<span data-ttu-id="6d59d-179">Linux</span><span class="sxs-lookup"><span data-stu-id="6d59d-179">Linux</span></span> |<span data-ttu-id="6d59d-180">Linux, UNIX, Mac OS X veya Windows</span><span class="sxs-lookup"><span data-stu-id="6d59d-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="6d59d-181">Curl</span><span class="sxs-lookup"><span data-stu-id="6d59d-181">Curl</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="6d59d-182">✔</span><span class="sxs-lookup"><span data-stu-id="6d59d-182">✔</span></span> |<span data-ttu-id="6d59d-183">Linux veya Windows</span><span class="sxs-lookup"><span data-stu-id="6d59d-183">Linux or Windows</span></span> |<span data-ttu-id="6d59d-184">Linux, UNIX, Mac OS X veya Windows</span><span class="sxs-lookup"><span data-stu-id="6d59d-184">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="6d59d-185">Hadoop için .NET SDK</span><span class="sxs-lookup"><span data-stu-id="6d59d-185">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="6d59d-186">✔</span><span class="sxs-lookup"><span data-stu-id="6d59d-186">✔</span></span> |<span data-ttu-id="6d59d-187">Linux veya Windows</span><span class="sxs-lookup"><span data-stu-id="6d59d-187">Linux or Windows</span></span> |<span data-ttu-id="6d59d-188">Windows (için şimdi)</span><span class="sxs-lookup"><span data-stu-id="6d59d-188">Windows (for now)</span></span> |
| [<span data-ttu-id="6d59d-189">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="6d59d-189">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="6d59d-190">✔</span><span class="sxs-lookup"><span data-stu-id="6d59d-190">✔</span></span> |<span data-ttu-id="6d59d-191">Linux veya Windows</span><span class="sxs-lookup"><span data-stu-id="6d59d-191">Linux or Windows</span></span> |<span data-ttu-id="6d59d-192">Windows</span><span class="sxs-lookup"><span data-stu-id="6d59d-192">Windows</span></span> |
| <span data-ttu-id="6d59d-193">[Uzak Masaüstü](hdinsight-hadoop-use-pig-remote-desktop.md) (Hdınsight 3.2 ve 3.3)</span><span class="sxs-lookup"><span data-stu-id="6d59d-193">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="6d59d-194">✔</span><span class="sxs-lookup"><span data-stu-id="6d59d-194">✔</span></span> |<span data-ttu-id="6d59d-195">✔</span><span class="sxs-lookup"><span data-stu-id="6d59d-195">✔</span></span> |<span data-ttu-id="6d59d-196">Windows</span><span class="sxs-lookup"><span data-stu-id="6d59d-196">Windows</span></span> |<span data-ttu-id="6d59d-197">Windows</span><span class="sxs-lookup"><span data-stu-id="6d59d-197">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="6d59d-198">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="6d59d-198">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6d59d-199">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="6d59d-199">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="pig-and-sql-server-integration-services"></a><span data-ttu-id="6d59d-200">Pig ve SQL Server Integration Services</span><span class="sxs-lookup"><span data-stu-id="6d59d-200">Pig and SQL Server Integration Services</span></span>

<span data-ttu-id="6d59d-201">SQL Server Integration Services (SSIS) toorun Pig işi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d59d-201">You can use SQL Server Integration Services (SSIS) toorun a Pig job.</span></span> <span data-ttu-id="6d59d-202">Hello Azure Feature Pack SSIS için Hdınsight'ta Pig işlerle çalışma bileşenleri aşağıdaki hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="6d59d-202">hello Azure Feature Pack for SSIS provides hello following components that work with Pig jobs on HDInsight.</span></span>

* <span data-ttu-id="6d59d-203">[Azure Hdınsight Pig görevi][pigtask]</span><span class="sxs-lookup"><span data-stu-id="6d59d-203">[Azure HDInsight Pig Task][pigtask]</span></span>

* <span data-ttu-id="6d59d-204">[Azure aboneliği Bağlantı Yöneticisi][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="6d59d-204">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="6d59d-205">Hello Azure Feature Pack hakkında daha fazla bilgi için SSIS [burada][ssispack].</span><span class="sxs-lookup"><span data-stu-id="6d59d-205">Learn more about hello Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="6d59d-206"><a id="nextsteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="6d59d-206"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="6d59d-207">Göre nasıl toouse aşağıdaki kullanım Merhaba, Hdınsight ile Pig tooexplore diğer yolları toowork Azure Hdınsight ile bağlantıları öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="6d59d-207">Now that you have learned how toouse Pig with HDInsight, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* <span data-ttu-id="6d59d-208">[Veri tooHDInsight karşıya yükle][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="6d59d-208">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="6d59d-209">[HDInsight ile Hive kullanma][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="6d59d-209">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* [<span data-ttu-id="6d59d-210">Hdınsight ile Sqoop kullanma</span><span class="sxs-lookup"><span data-stu-id="6d59d-210">Use Sqoop with HDInsight</span></span>](hdinsight-use-sqoop.md)
* [<span data-ttu-id="6d59d-211">Oozie Hdınsight ile kullanma</span><span class="sxs-lookup"><span data-stu-id="6d59d-211">Use Oozie with HDInsight</span></span>](hdinsight-use-oozie.md)
* <span data-ttu-id="6d59d-212">[Hdınsight ile MapReduce işleri kullanma][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="6d59d-212">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

[apachepig-home]: http://pig.apache.org/
[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html
[curl]: http://curl.haxx.se/
[pigtask]: http://msdn.microsoft.com/library/mt146781(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx


[hdinsight-upload-data]: hdinsight-upload-data.md

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md#mapreduce-sdk

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx


[image-hdi-pig-data-transformation]: ./media/hdinsight-use-pig/HDI.DataTransformation.gif
