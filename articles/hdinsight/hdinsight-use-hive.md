---
title: "Apache Hive ve HiveQL - Azure Hdınsight aaaWhat olan | Microsoft Docs"
description: "Apache Hive bir veri ambarı için Hadoop sistemidir. HiveQL, hangi benzer tooTransact SQL kullanarak kovanında depolanan verileri sorgulayabilir. Bu belgede, bilgi nasıl toouse Hive ve HiveQL Azure Hdınsight ile."
keywords: "hive, hadoop hiveql nedir hiveql toouse hive nasıl hive nedir hive öğrenin"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2c10f989-7636-41bf-b7f7-c4b67ec0814f
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: a2772312263895ff99b499898264c2e6d5e816e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-apache-hive-and-hiveql-on-azure-hdinsight"></a><span data-ttu-id="85d53-106">Apache Hive ve HiveQL Azure hdınsight'ta nedir?</span><span class="sxs-lookup"><span data-stu-id="85d53-106">What is Apache Hive and HiveQL on Azure HDInsight?</span></span>

<span data-ttu-id="85d53-107">[Apache Hive](http://hive.apache.org/) Hadoop için veri ambarı sistemidir.</span><span class="sxs-lookup"><span data-stu-id="85d53-107">[Apache Hive](http://hive.apache.org/) is a data warehouse system for Hadoop.</span></span> <span data-ttu-id="85d53-108">Hive veri özetleme, sorgulama ve veri analizini sağlar.</span><span class="sxs-lookup"><span data-stu-id="85d53-108">Hive enables data summarization, querying, and analysis of data.</span></span> <span data-ttu-id="85d53-109">Hive sorguları bir sorgu dili benzer tooSQL olan HiveQL yazılır.</span><span class="sxs-lookup"><span data-stu-id="85d53-109">Hive queries are written in HiveQL, which is a query language similar tooSQL.</span></span>

<span data-ttu-id="85d53-110">Hive büyük ölçüde yapılandırılmamış veriler üzerinde tooproject yapısı sağlar.</span><span class="sxs-lookup"><span data-stu-id="85d53-110">Hive allows you tooproject structure on largely unstructured data.</span></span> <span data-ttu-id="85d53-111">Merhaba yapısı tanımladıktan sonra HiveQL tooquery hello verileri Java veya MapReduce bilgisi olmadan kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85d53-111">After you define hello structure, you can use HiveQL tooquery hello data without knowledge of Java or MapReduce.</span></span>

<span data-ttu-id="85d53-112">Hdınsight belirli iş yükleri için ayarlanmış birkaç küme türler sağlar.</span><span class="sxs-lookup"><span data-stu-id="85d53-112">HDInsight provides several cluster types, which are tuned for specific workloads.</span></span> <span data-ttu-id="85d53-113">Küme türleri aşağıdaki hello Hive sorguları için en sık kullanılır:</span><span class="sxs-lookup"><span data-stu-id="85d53-113">hello following cluster types are most often used for Hive queries:</span></span>

* <span data-ttu-id="85d53-114">__Etkileşimli Hive__: sağlayan bir Hadoop kümesine [düşük gecikme süresi analitik işleme (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) işlevselliği tooimprove yanıt sürelerini etkileşimli sorgular.</span><span class="sxs-lookup"><span data-stu-id="85d53-114">__Interactive Hive__: A Hadoop cluster that provides [Low Latency Analytical Processing (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) functionality tooimprove response times for interactive queries.</span></span> <span data-ttu-id="85d53-115">Daha fazla bilgi için bkz: Merhaba [etkileşimli hdınsight'ta Hive ile başlar](hdinsight-hadoop-use-interactive-hive.md) belge.</span><span class="sxs-lookup"><span data-stu-id="85d53-115">For more information, see hello [Start with Interactive Hive in HDInsight](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

* <span data-ttu-id="85d53-116">__Hadoop__: toplu işlem iş yüklerini işlemek için ayarlanmış bir Hadoop kümesi.</span><span class="sxs-lookup"><span data-stu-id="85d53-116">__Hadoop__: A Hadoop cluster that is tuned for batch processing workloads.</span></span> <span data-ttu-id="85d53-117">Daha fazla bilgi için bkz: Merhaba [Başlat hdınsight'ta Hadoop ile](hdinsight-hadoop-linux-tutorial-get-started.md) belge.</span><span class="sxs-lookup"><span data-stu-id="85d53-117">For more information, see hello [Start with Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) document.</span></span>

* <span data-ttu-id="85d53-118">__Spark__: Apache Spark Hive ile çalışmak için yerleşik bir işleve sahiptir.</span><span class="sxs-lookup"><span data-stu-id="85d53-118">__Spark__: Apache Spark has built-in functionality for working with Hive.</span></span> <span data-ttu-id="85d53-119">Daha fazla bilgi için bkz: Merhaba [hdınsight'ta Spark ile başlar](hdinsight-apache-spark-jupyter-spark-sql.md) belge.</span><span class="sxs-lookup"><span data-stu-id="85d53-119">For more information, see hello [Start with Spark on HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) document.</span></span>

* <span data-ttu-id="85d53-120">__HBase__: HiveQL HBase içinde depolanan kullanılan tooquery verileri olabilir.</span><span class="sxs-lookup"><span data-stu-id="85d53-120">__HBase__: HiveQL can be used tooquery data stored in HBase.</span></span> <span data-ttu-id="85d53-121">Daha fazla bilgi için bkz: Merhaba [hdınsight'ta HBase ile başlar](hdinsight-hbase-tutorial-get-started-linux.md) belge.</span><span class="sxs-lookup"><span data-stu-id="85d53-121">For more information, see hello [Start with HBase on HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) document.</span></span>

## <a name="how-toouse-hive"></a><span data-ttu-id="85d53-122">Nasıl toouse yığını</span><span class="sxs-lookup"><span data-stu-id="85d53-122">How toouse Hive</span></span>

<span data-ttu-id="85d53-123">Nasıl toouse Hdınsight ile Hive tablosu toodiscover aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="85d53-123">Use hello following table toodiscover how toouse Hive with HDInsight:</span></span>

| <span data-ttu-id="85d53-124">**Bu yöntemi kullanmak** isterseniz...</span><span class="sxs-lookup"><span data-stu-id="85d53-124">**Use this method** if you want...</span></span> | <span data-ttu-id="85d53-125">.. .an **etkileşimli** Kabuk</span><span class="sxs-lookup"><span data-stu-id="85d53-125">...an **interactive** shell</span></span> | <span data-ttu-id="85d53-126">... **toplu** işleme</span><span class="sxs-lookup"><span data-stu-id="85d53-126">...**batch** processing</span></span> | <span data-ttu-id="85d53-127">.. hemen bu **küme işletim sistemi**</span><span class="sxs-lookup"><span data-stu-id="85d53-127">...with this **cluster operating system**</span></span> | <span data-ttu-id="85d53-128">.. .from bu **istemci işletim sistemi**</span><span class="sxs-lookup"><span data-stu-id="85d53-128">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="85d53-129">Hive görünümü</span><span class="sxs-lookup"><span data-stu-id="85d53-129">Hive View</span></span>](hdinsight-hadoop-use-hive-ambari-view.md) |<span data-ttu-id="85d53-130">✔</span><span class="sxs-lookup"><span data-stu-id="85d53-130">✔</span></span> |<span data-ttu-id="85d53-131">✔</span><span class="sxs-lookup"><span data-stu-id="85d53-131">✔</span></span> |<span data-ttu-id="85d53-132">Linux</span><span class="sxs-lookup"><span data-stu-id="85d53-132">Linux</span></span> |<span data-ttu-id="85d53-133">(Herhangi bir tarayıcı tabanlı)</span><span class="sxs-lookup"><span data-stu-id="85d53-133">Any (browser based)</span></span> |
| [<span data-ttu-id="85d53-134">Beeline istemci</span><span class="sxs-lookup"><span data-stu-id="85d53-134">Beeline client</span></span>](hdinsight-hadoop-use-hive-beeline.md) |<span data-ttu-id="85d53-135">✔</span><span class="sxs-lookup"><span data-stu-id="85d53-135">✔</span></span> |<span data-ttu-id="85d53-136">✔</span><span class="sxs-lookup"><span data-stu-id="85d53-136">✔</span></span> |<span data-ttu-id="85d53-137">Linux</span><span class="sxs-lookup"><span data-stu-id="85d53-137">Linux</span></span> |<span data-ttu-id="85d53-138">Linux, UNIX, Mac OS X veya Windows</span><span class="sxs-lookup"><span data-stu-id="85d53-138">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="85d53-139">REST API</span><span class="sxs-lookup"><span data-stu-id="85d53-139">REST API</span></span>](hdinsight-hadoop-use-hive-curl.md) |&nbsp; |<span data-ttu-id="85d53-140">✔</span><span class="sxs-lookup"><span data-stu-id="85d53-140">✔</span></span> |<span data-ttu-id="85d53-141">Linux veya Windows *</span><span class="sxs-lookup"><span data-stu-id="85d53-141">Linux or Windows*</span></span> |<span data-ttu-id="85d53-142">Linux, UNIX, Mac OS X veya Windows</span><span class="sxs-lookup"><span data-stu-id="85d53-142">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="85d53-143">Visual Studio için Hdınsight araçları</span><span class="sxs-lookup"><span data-stu-id="85d53-143">HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-use-hive-visual-studio.md) |&nbsp; |<span data-ttu-id="85d53-144">✔</span><span class="sxs-lookup"><span data-stu-id="85d53-144">✔</span></span> |<span data-ttu-id="85d53-145">Linux veya Windows *</span><span class="sxs-lookup"><span data-stu-id="85d53-145">Linux or Windows*</span></span> |<span data-ttu-id="85d53-146">Windows</span><span class="sxs-lookup"><span data-stu-id="85d53-146">Windows</span></span> |
| [<span data-ttu-id="85d53-147">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="85d53-147">Windows PowerShell</span></span>](hdinsight-hadoop-use-hive-powershell.md) |&nbsp; |<span data-ttu-id="85d53-148">✔</span><span class="sxs-lookup"><span data-stu-id="85d53-148">✔</span></span> |<span data-ttu-id="85d53-149">Linux veya Windows *</span><span class="sxs-lookup"><span data-stu-id="85d53-149">Linux or Windows*</span></span> |<span data-ttu-id="85d53-150">Windows</span><span class="sxs-lookup"><span data-stu-id="85d53-150">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="85d53-151">\*Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="85d53-151">\* Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="85d53-152">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="85d53-152">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="85d53-153">Bir Windows tabanlı Hdınsight kümesi kullanıyorsanız, hello kullanabilirsiniz [sorgu konsol](hdinsight-hadoop-use-hive-query-console.md) tarayıcınızdan veya [Uzak Masaüstü](hdinsight-hadoop-use-hive-remote-desktop.md) toorun Hive sorguları.</span><span class="sxs-lookup"><span data-stu-id="85d53-153">If you are using a Windows-based HDInsight cluster, you can use hello [Query console](hdinsight-hadoop-use-hive-query-console.md) from your browser or [Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md) toorun Hive queries.</span></span>

## <a name="hiveql-language-reference"></a><span data-ttu-id="85d53-154">HiveQL dil başvurusu</span><span class="sxs-lookup"><span data-stu-id="85d53-154">HiveQL language reference</span></span>

<span data-ttu-id="85d53-155">HiveQL dil başvurusu hello kullanılabilir [dil el ile (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span><span class="sxs-lookup"><span data-stu-id="85d53-155">HiveQL language reference is available in hello [language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span></span>

## <a name="hive-and-data-structure"></a><span data-ttu-id="85d53-156">Hive ve veri yapısı</span><span class="sxs-lookup"><span data-stu-id="85d53-156">Hive and data structure</span></span>

<span data-ttu-id="85d53-157">Hive nasıl toowork ile yapılandırılmış ve yarı yapılandırılmış veri bilir.</span><span class="sxs-lookup"><span data-stu-id="85d53-157">Hive understands how toowork with structured and semi-structured data.</span></span> <span data-ttu-id="85d53-158">Merhaba alanlar belirli karakterleriyle burada sınırlandırılmıştır Örneğin, metin dosyaları.</span><span class="sxs-lookup"><span data-stu-id="85d53-158">For example, text files where hello fields are delimited by specific characters.</span></span> <span data-ttu-id="85d53-159">Aşağıdaki HiveQL ifadeyi hello boşlukla ayrılmış veriler üzerinde bir tablo oluşturur:</span><span class="sxs-lookup"><span data-stu-id="85d53-159">hello following HiveQL statement creates a table over space-delimited data:</span></span>

```hiveql
CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
STORED AS TEXTFILE LOCATION '/example/data/';
```

<span data-ttu-id="85d53-160">Hive ayrıca özel destekler **seri hale getirici/deserializers (SerDe)** karmaşık veya düzensiz yapılandırılmış veriler için.</span><span class="sxs-lookup"><span data-stu-id="85d53-160">Hive also supports custom **serializer/deserializers (SerDe)** for complex or irregularly structured data.</span></span> <span data-ttu-id="85d53-161">Daha fazla bilgi için bkz: Merhaba [nasıl toouse Hdınsight ile özel bir JSON SerDe](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) belge.</span><span class="sxs-lookup"><span data-stu-id="85d53-161">For more information, see hello [How toouse a custom JSON SerDe with HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) document.</span></span>

<span data-ttu-id="85d53-162">Merhaba Hive tarafından desteklenen dosya biçimleri hakkında daha fazla bilgi için bkz: [dil el ile (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span><span class="sxs-lookup"><span data-stu-id="85d53-162">For more information on file formats supported by Hive, see hello [Language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span></span>

## <a name="hive-internal-tables-vs-external-tables"></a><span data-ttu-id="85d53-163">İç tablolar vs dış tablolara yığını</span><span class="sxs-lookup"><span data-stu-id="85d53-163">Hive internal tables vs external tables</span></span>

<span data-ttu-id="85d53-164">Hive ile oluşturabileceğiniz tablolar iki tür vardır:</span><span class="sxs-lookup"><span data-stu-id="85d53-164">There are two types of tables that you can create with Hive:</span></span>

* <span data-ttu-id="85d53-165">__İç__: veri hello Hive veri ambarında depolanır.</span><span class="sxs-lookup"><span data-stu-id="85d53-165">__Internal__: Data is stored in hello Hive data warehouse.</span></span> <span data-ttu-id="85d53-166">Merhaba veri ambarı bulunur `/hive/warehouse/` hello varsayılan depolama hello kümesi için.</span><span class="sxs-lookup"><span data-stu-id="85d53-166">hello data warehouse is located at `/hive/warehouse/` on hello default storage for hello cluster.</span></span>

    <span data-ttu-id="85d53-167">İç kullanım ne zaman tabloları:</span><span class="sxs-lookup"><span data-stu-id="85d53-167">Use internal tables when:</span></span>

    * <span data-ttu-id="85d53-168">Veri geçicidir.</span><span class="sxs-lookup"><span data-stu-id="85d53-168">Data is temporary.</span></span>
    * <span data-ttu-id="85d53-169">Hive toomanage hello yaşam döngüsü hello tablo ve veri istiyor.</span><span class="sxs-lookup"><span data-stu-id="85d53-169">You want Hive toomanage hello lifecycle of hello table and data.</span></span>

* <span data-ttu-id="85d53-170">__Dış__: dışında hello veri ambarında depolanır.</span><span class="sxs-lookup"><span data-stu-id="85d53-170">__External__: Data is stored outside hello data warehouse.</span></span> <span data-ttu-id="85d53-171">Merhaba veri herhangi bir depolama alanı üzerinde erişilebilir hello küme tarafından depolanabilir.</span><span class="sxs-lookup"><span data-stu-id="85d53-171">hello data can be stored on any storage accessible by hello cluster.</span></span>

    <span data-ttu-id="85d53-172">Kullanım dış tablolar:</span><span class="sxs-lookup"><span data-stu-id="85d53-172">Use external tables when:</span></span>

    * <span data-ttu-id="85d53-173">Merhaba verileri de Hive dışında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="85d53-173">hello data is also used outside of Hive.</span></span> <span data-ttu-id="85d53-174">Örneğin, hello veri dosyaları (Merhaba dosyaları kilit yok.) başka bir işlem tarafından güncelleştirilir</span><span class="sxs-lookup"><span data-stu-id="85d53-174">For example, hello data files are updated by another process (that does not lock hello files.)</span></span>
    * <span data-ttu-id="85d53-175">Verilerin bile hello tablo bırakarak sonra konum, temel alınan hello tooremain gerekir.</span><span class="sxs-lookup"><span data-stu-id="85d53-175">Data needs tooremain in hello underlying location, even after dropping hello table.</span></span>
    * <span data-ttu-id="85d53-176">Varsayılan olmayan depolama hesabı gibi özel bir konuma gerekir.</span><span class="sxs-lookup"><span data-stu-id="85d53-176">You need a custom location, such as a non-default storage account.</span></span>
    * <span data-ttu-id="85d53-177">Hive dışında bir program hello veri biçimi, konum vb. yönetir.</span><span class="sxs-lookup"><span data-stu-id="85d53-177">A program other than hive manages hello data format, location, etc.</span></span>

<span data-ttu-id="85d53-178">Merhaba daha fazla bilgi için bkz: [Hive iç ve dış tablolar giriş] [ cindygross-hive-tables] blog postası.</span><span class="sxs-lookup"><span data-stu-id="85d53-178">For more information, see hello [Hive Internal and External Tables Intro][cindygross-hive-tables] blog post.</span></span>

## <a name="user-defined-functions-udf"></a><span data-ttu-id="85d53-179">Kullanıcı tanımlı işlevler (UDF)</span><span class="sxs-lookup"><span data-stu-id="85d53-179">User-defined functions (UDF)</span></span>

<span data-ttu-id="85d53-180">Hive ayrıca uzatabilirsiniz aracılığıyla **kullanıcı tanımlı işlevler (UDF)**.</span><span class="sxs-lookup"><span data-stu-id="85d53-180">Hive can also be extended through **user-defined functions (UDF)**.</span></span> <span data-ttu-id="85d53-181">Bir UDF tooimplement işlev veya HiveQL içinde kolayca modellenir değil mantığı sağlar.</span><span class="sxs-lookup"><span data-stu-id="85d53-181">A UDF allows you tooimplement functionality or logic that isn't easily modeled in HiveQL.</span></span> <span data-ttu-id="85d53-182">UDF'ler ile Hive kullanma örneği için aşağıdaki belgeleri hello bakın:</span><span class="sxs-lookup"><span data-stu-id="85d53-182">For an example of using UDFs with Hive, see hello following documents:</span></span>

* [<span data-ttu-id="85d53-183">Kullanıcı tanımlı bir Java işlev ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="85d53-183">Use a Java user-defined function with Hive</span></span>](hdinsight-hadoop-hive-java-udf.md)

* [<span data-ttu-id="85d53-184">Kullanıcı tanımlı bir Python işlev Hive veya Pig kullanın</span><span class="sxs-lookup"><span data-stu-id="85d53-184">Use a Python user-defined function with Hive and Pig</span></span>](hdinsight-python.md)

* [<span data-ttu-id="85d53-185">C# kullanıcı tanımlı bir işlev Hive veya Pig kullanın</span><span class="sxs-lookup"><span data-stu-id="85d53-185">Use a C# user-defined function with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="85d53-186">Nasıl tooadd özel Hive kullanıcı tanımlı işlev tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="85d53-186">How tooadd a custom Hive user-defined function tooHDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

* [<span data-ttu-id="85d53-187">Bir örnek Hive kullanıcı tanımlı işlev tooconvert tarih/saat tooHive zaman damgası biçimleri</span><span class="sxs-lookup"><span data-stu-id="85d53-187">An example Hive user-defined function tooconvert date/time formats tooHive timestamp</span></span>](https://github.com/Azure-Samples/hdinsight-java-hive-udf)

## <span data-ttu-id="85d53-188"><a id="data"></a>Örnek veri</span><span class="sxs-lookup"><span data-stu-id="85d53-188"><a id="data"></a>Example data</span></span>

<span data-ttu-id="85d53-189">Hdınsight'ta Hive gelen önceden yüklenmiş bir iç tablosu adlı `hivesampletable`.</span><span class="sxs-lookup"><span data-stu-id="85d53-189">Hive on HDInsight comes pre-loaded with an internal table named `hivesampletable`.</span></span> <span data-ttu-id="85d53-190">Hdınsight ile Hive kullanılabilir bir örnek veri kümeleri de sağlar.</span><span class="sxs-lookup"><span data-stu-id="85d53-190">HDInsight also provides example data sets that can be used with Hive.</span></span> <span data-ttu-id="85d53-191">Bu veri kümeleri hello depolanan `/example/data` ve `/HdiSamples` dizinleri.</span><span class="sxs-lookup"><span data-stu-id="85d53-191">These data sets are stored in hello `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="85d53-192">Bu dizinleri, kümeniz için hello varsayılan depolama yok.</span><span class="sxs-lookup"><span data-stu-id="85d53-192">These directories exist in hello default storage for your cluster.</span></span>

## <span data-ttu-id="85d53-193"><a id="job"></a>Örnek Hive sorgusu</span><span class="sxs-lookup"><span data-stu-id="85d53-193"><a id="job"></a>Example Hive query</span></span>

<span data-ttu-id="85d53-194">Aşağıdaki HiveQL ifadelerini proje sütunları hello üzerine hello `/example/data/sample.log` dosyası:</span><span class="sxs-lookup"><span data-stu-id="85d53-194">hello following HiveQL statements project columns onto hello `/example/data/sample.log` file:</span></span>

    set hive.execution.engine=tez;
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

<span data-ttu-id="85d53-195">Hello önceki örnekte, hello HiveQL ifadelerini hello aşağıdaki eylemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="85d53-195">In hello previous example, hello HiveQL statements perform hello following actions:</span></span>

* <span data-ttu-id="85d53-196">`set hive.execution.engine=tez;`: Kümeleri yürütme altyapısı toouse Tez hello.</span><span class="sxs-lookup"><span data-stu-id="85d53-196">`set hive.execution.engine=tez;`: Sets hello execution engine toouse Tez.</span></span> <span data-ttu-id="85d53-197">Tez yerine MapReduce kullanarak sorgu performansı bir artış sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="85d53-197">Using Tez instead of MapReduce can provide an increase in query performance.</span></span> <span data-ttu-id="85d53-198">Tez hakkında daha fazla bilgi için bkz: Merhaba [iyileştirilmiş performans için Apache Tez kullanma](#usetez) bölümü.</span><span class="sxs-lookup"><span data-stu-id="85d53-198">For more information on Tez, see hello [Use Apache Tez for improved performance](#usetez) section.</span></span>

    > [!NOTE]
    > <span data-ttu-id="85d53-199">Bu deyim yalnızca olan Windows tabanlı Hdınsight kümesi kullanılırken gereklidir.</span><span class="sxs-lookup"><span data-stu-id="85d53-199">This statement is only required when using a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="85d53-200">Tez hello varsayılan yürütme Linux tabanlı Hdınsight için altyapısıdır.</span><span class="sxs-lookup"><span data-stu-id="85d53-200">Tez is hello default execution engine for Linux-based HDInsight.</span></span>

* <span data-ttu-id="85d53-201">`DROP TABLE`: Hello tablo zaten varsa dosyayı silin.</span><span class="sxs-lookup"><span data-stu-id="85d53-201">`DROP TABLE`: If hello table already exists, delete it.</span></span>

* <span data-ttu-id="85d53-202">`CREATE EXTERNAL TABLE`: Oluşturur Yeni bir **dış** Hive tablo.</span><span class="sxs-lookup"><span data-stu-id="85d53-202">`CREATE EXTERNAL TABLE`: Creates a new **external** table in Hive.</span></span> <span data-ttu-id="85d53-203">Dış tablolara hello tablo tanımı kovanında yalnızca depolar.</span><span class="sxs-lookup"><span data-stu-id="85d53-203">External tables only store hello table definition in Hive.</span></span> <span data-ttu-id="85d53-204">Merhaba veri hello özgün konumuna hem de hello özgün biçiminde bırakılır.</span><span class="sxs-lookup"><span data-stu-id="85d53-204">hello data is left in hello original location and in hello original format.</span></span>

* <span data-ttu-id="85d53-205">`ROW FORMAT`: Hello verilerin nasıl biçimlendirilmiş Hive söyler.</span><span class="sxs-lookup"><span data-stu-id="85d53-205">`ROW FORMAT`: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="85d53-206">Bu durumda, her günlüğün içinde hello alanlar boşlukla ayrılır.</span><span class="sxs-lookup"><span data-stu-id="85d53-206">In this case, hello fields in each log are separated by a space.</span></span>

* <span data-ttu-id="85d53-207">`STORED AS TEXTFILE LOCATION`: Hive hello burada verilerin depolandığı söyler (Merhaba `example/data` dizini) ve metin olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="85d53-207">`STORED AS TEXTFILE LOCATION`: Tells Hive where hello data is stored (hello `example/data` directory) and that it is stored as text.</span></span> <span data-ttu-id="85d53-208">Merhaba verileri, bir dosyada yer veya hello dizini içindeki birden çok dosya üzerinden yayılan.</span><span class="sxs-lookup"><span data-stu-id="85d53-208">hello data can be in one file or spread across multiple files within hello directory.</span></span>

* <span data-ttu-id="85d53-209">`SELECT`: Tüm satırların sayımını hello burada seçer sütun **t4** hello değeri içeren **[Hata]**.</span><span class="sxs-lookup"><span data-stu-id="85d53-209">`SELECT`: Selects a count of all rows where hello column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="85d53-210">Bu ifade değerini döndürür **3** çünkü bu değer içeren üç satır vardır.</span><span class="sxs-lookup"><span data-stu-id="85d53-210">This statement returns a value of **3** because there are three rows that contain this value.</span></span>

* <span data-ttu-id="85d53-211">`INPUT__FILE__NAME LIKE '%.log'`-Hive tooapply hello şema tooall dosyaları hello dizininde çalışır.</span><span class="sxs-lookup"><span data-stu-id="85d53-211">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts tooapply hello schema tooall files in hello directory.</span></span> <span data-ttu-id="85d53-212">Bu durumda, başlangıç dizini hello şema eşleşmiyor dosyalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="85d53-212">In this case, hello directory contains files that do not match hello schema.</span></span> <span data-ttu-id="85d53-213">tooprevent çöp veriler hello sonuçlarında, bu bildirimi bildirir Hive biz yalnızca veri biten dosyalarından döndürmesi gerektiğini. günlük.</span><span class="sxs-lookup"><span data-stu-id="85d53-213">tooprevent garbage data in hello results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

> [!NOTE]
> <span data-ttu-id="85d53-214">Dış kaynak tarafından güncelleştirilmiş hello temel alınan veri toobe beklediğiniz dış tablolara kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="85d53-214">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="85d53-215">Örneğin, bir otomatik veri karşıya yükleme işlemi veya MapReduce işlemi.</span><span class="sxs-lookup"><span data-stu-id="85d53-215">For example, an automated data upload process, or MapReduce operation.</span></span>
>
> <span data-ttu-id="85d53-216">Bir dış tablo bırakma mu **değil** hello verilerini silmek yalnızca hello tablosu tanımını siler.</span><span class="sxs-lookup"><span data-stu-id="85d53-216">Dropping an external table does **not** delete hello data, it only deletes hello table definition.</span></span>

<span data-ttu-id="85d53-217">toocreate bir **iç** tablo dış yerine, aşağıdaki HiveQL hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="85d53-217">toocreate an **internal** table instead of external, use hello following HiveQL:</span></span>

    set hive.execution.engine=tez;
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs
    SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';

<span data-ttu-id="85d53-218">Bu deyimler hello aşağıdaki eylemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="85d53-218">These statements perform hello following actions:</span></span>

* <span data-ttu-id="85d53-219">`CREATE TABLE IF NOT EXISTS`: Hello tablo mevcut değilse oluşturun.</span><span class="sxs-lookup"><span data-stu-id="85d53-219">`CREATE TABLE IF NOT EXISTS`: If hello table does not exist, create it.</span></span> <span data-ttu-id="85d53-220">Çünkü hello **dış** anahtar sözcüğü kullanılmaz, bu deyim bir iç tablosu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="85d53-220">Because hello **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="85d53-221">Hello tablo hello Hive veri ambarında depolanır ve tamamen Hive tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="85d53-221">hello table is stored in hello Hive data warehouse and is managed completely by Hive.</span></span>

* <span data-ttu-id="85d53-222">`STORED AS ORC`: En iyi duruma getirilmiş satır sütunlu (ORC) biçiminde hello verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="85d53-222">`STORED AS ORC`: Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="85d53-223">ORC Hive verilerini depolamak için yüksek oranda en iyi duruma getirilmiş ve verimli bir biçimidir.</span><span class="sxs-lookup"><span data-stu-id="85d53-223">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

* <span data-ttu-id="85d53-224">`INSERT OVERWRITE ... SELECT`: Hello satırları seçer **log4jLogs** içeren tablo **[Hata]**, ve ardından ekler veri hello hello **günlüklerini** tablo.</span><span class="sxs-lookup"><span data-stu-id="85d53-224">`INSERT OVERWRITE ... SELECT`: Selects rows from hello **log4jLogs** table that contains **[ERROR]**, and then inserts hello data into hello **errorLogs** table.</span></span>

> [!NOTE]
> <span data-ttu-id="85d53-225">Dış tablolara, bir iç tablosu bırakarak hello temel verilerini siler.</span><span class="sxs-lookup"><span data-stu-id="85d53-225">Unlike external tables, dropping an internal table also deletes hello underlying data.</span></span>

## <a name="improve-hive-query-performance"></a><span data-ttu-id="85d53-226">Hive sorgu performansı</span><span class="sxs-lookup"><span data-stu-id="85d53-226">Improve Hive query performance</span></span>

### <span data-ttu-id="85d53-227"><a id="usetez"></a>Apache Tez</span><span class="sxs-lookup"><span data-stu-id="85d53-227"><a id="usetez"></a>Apache Tez</span></span>

<span data-ttu-id="85d53-228">[Apache Tez](http://tez.apache.org) Hive, ölçekte daha verimli bir şekilde toorun gibi veri yoğun uygulamalar sağlayan bir çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="85d53-228">[Apache Tez](http://tez.apache.org) is a framework that allows data intensive applications, such as Hive, toorun much more efficiently at scale.</span></span> <span data-ttu-id="85d53-229">Tez Linux tabanlı Hdınsight kümeleri için varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="85d53-229">Tez is enabled by default for Linux-based HDInsight clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="85d53-230">Tez şu anda Windows tabanlı Hdınsight kümeleri için varsayılan olarak kapalıdır ve etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="85d53-230">Tez is currently off by default for Windows-based HDInsight clusters and it must be enabled.</span></span> <span data-ttu-id="85d53-231">Tez, aşağıdaki değeri hello tootake avantajlarından bir Hive sorgusu için ayarlamanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="85d53-231">tootake advantage of Tez, hello following value must be set for a Hive query:</span></span>
>
> `set hive.execution.engine=tez;`
>
> <span data-ttu-id="85d53-232">Tez hello varsayılan Linux tabanlı Hdınsight kümeleri altyapısıdır.</span><span class="sxs-lookup"><span data-stu-id="85d53-232">Tez is hello default engine for Linux-based HDInsight clusters.</span></span>

<span data-ttu-id="85d53-233">Merhaba [Hive Tez tasarım belgeleri](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) hello uygulama seçeneklerine ve ayarlama yapılandırmalar hakkında ayrıntılar içerir.</span><span class="sxs-lookup"><span data-stu-id="85d53-233">hello [Hive on Tez design documents](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) contains details about hello implementation choices and tuning configurations.</span></span>

<span data-ttu-id="85d53-234">işlerini hata tooaid Tez kullanılarak çalıştırıldı, Hdınsight Tez işlerinde tooview ayrıntılarını izin web Uı'lar aşağıdaki hello sağlar:</span><span class="sxs-lookup"><span data-stu-id="85d53-234">tooaid in debugging jobs ran using Tez, HDInsight provides hello following web UIs that allow you tooview details of Tez jobs:</span></span>

* [<span data-ttu-id="85d53-235">Merhaba Linux tabanlı Hdınsight Ambari Tez görünümünde kullanın</span><span class="sxs-lookup"><span data-stu-id="85d53-235">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

* [<span data-ttu-id="85d53-236">Windows tabanlı Hdınsight üzerinde Hello Tez UI kullanın</span><span class="sxs-lookup"><span data-stu-id="85d53-236">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)

### <a name="low-latency-analytical-processing-llap"></a><span data-ttu-id="85d53-237">Düşük gecikme süresi analitik işleme (LLAP)</span><span class="sxs-lookup"><span data-stu-id="85d53-237">Low Latency Analytical Processing (LLAP)</span></span>

<span data-ttu-id="85d53-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (Canlı uzun ve işlem da bilinir) Hive sorguları bellek içi önbelleğe alma veren 2.0 yeni bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="85d53-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (sometimes known as Live Long and Process) is a new feature in Hive 2.0 that allows in-memory caching of queries.</span></span> <span data-ttu-id="85d53-239">LLAP yapar yukarı daha hızlı Hive sorguları çok[26 x bazı durumlarda 1.x Hive çok hızlı](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span><span class="sxs-lookup"><span data-stu-id="85d53-239">LLAP makes Hive queries much faster, up too[26x faster than Hive 1.x in some cases](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span></span>

<span data-ttu-id="85d53-240">Hdınsight LLAP hello etkileşimli Hive küme türü sağlar.</span><span class="sxs-lookup"><span data-stu-id="85d53-240">HDInsight provides LLAP in hello Interactive Hive cluster type.</span></span> <span data-ttu-id="85d53-241">Merhaba daha fazla bilgi için bkz: [Başlat ile etkileşimli Hive](hdinsight-hadoop-use-interactive-hive.md) belge.</span><span class="sxs-lookup"><span data-stu-id="85d53-241">For more information, see hello [Start with Interactive Hive](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

## <a name="hive-jobs-and-sql-server-integration-services"></a><span data-ttu-id="85d53-242">Hive işleri ve SQL Server Integration Services</span><span class="sxs-lookup"><span data-stu-id="85d53-242">Hive jobs and SQL Server Integration Services</span></span>

<span data-ttu-id="85d53-243">SQL Server Integration Services (SSIS) toorun Hive işi kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="85d53-243">You can use SQL Server Integration Services (SSIS) toorun a Hive job.</span></span> <span data-ttu-id="85d53-244">Hello Azure Feature Pack SSIS için Hdınsight'ta Hive işlerle çalışma bileşenleri aşağıdaki hello sağlar.</span><span class="sxs-lookup"><span data-stu-id="85d53-244">hello Azure Feature Pack for SSIS provides hello following components that work with Hive jobs on HDInsight.</span></span>

* <span data-ttu-id="85d53-245">[Azure Hdınsight Hive görevi][hivetask]</span><span class="sxs-lookup"><span data-stu-id="85d53-245">[Azure HDInsight Hive Task][hivetask]</span></span>

* <span data-ttu-id="85d53-246">[Azure aboneliği Bağlantı Yöneticisi][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="85d53-246">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="85d53-247">Hello Azure Feature Pack hakkında daha fazla bilgi için SSIS [burada][ssispack].</span><span class="sxs-lookup"><span data-stu-id="85d53-247">Learn more about hello Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="85d53-248"><a id="nextsteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="85d53-248"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="85d53-249">Artık Hive nedir öğrendiğinize göre ve nasıl diğer yolları toowork Azure Hdınsight ile aşağıdaki kullanım hello hdınsight'ta Hadoop ile bağlantı tooexplore toouse.</span><span class="sxs-lookup"><span data-stu-id="85d53-249">Now that you've learned what Hive is and how toouse it with Hadoop in HDInsight, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* <span data-ttu-id="85d53-250">[Veri tooHDInsight karşıya yükle][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="85d53-250">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="85d53-251">[HDInsight ile Pig kullanma][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="85d53-251">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="85d53-252">[Hdınsight ile MapReduce işleri kullanma][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="85d53-252">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/
[hivetask]: http://msdn.microsoft.com/library/mt146771(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx

[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md


[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx
