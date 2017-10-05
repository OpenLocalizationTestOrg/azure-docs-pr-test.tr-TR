---
title: "Apache Hive ve HiveQL - Azure Hdınsight nedir | Microsoft Docs"
description: "Apache Hive bir veri ambarı için Hadoop sistemidir. HiveQL, kullanarak kovanında depolanan verileri sorgulayabilir, Transact-SQL benzer. Bu belgede, Azure Hdınsight ile Hive ve HiveQL kullanmayı öğrenin."
keywords: "hive, hadoop hiveql nedir hiveql nasıl hive kullanma, hive, hive nedir öğrenme"
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
ms.openlocfilehash: 6b3ee17141f773bec07cf40e0b6d63363e9b5164
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="what-is-apache-hive-and-hiveql-on-azure-hdinsight"></a><span data-ttu-id="ba04d-106">Apache Hive ve HiveQL Azure hdınsight'ta nedir?</span><span class="sxs-lookup"><span data-stu-id="ba04d-106">What is Apache Hive and HiveQL on Azure HDInsight?</span></span>

<span data-ttu-id="ba04d-107">[Apache Hive](http://hive.apache.org/) Hadoop için veri ambarı sistemidir.</span><span class="sxs-lookup"><span data-stu-id="ba04d-107">[Apache Hive](http://hive.apache.org/) is a data warehouse system for Hadoop.</span></span> <span data-ttu-id="ba04d-108">Hive veri özetleme, sorgulama ve veri analizini sağlar.</span><span class="sxs-lookup"><span data-stu-id="ba04d-108">Hive enables data summarization, querying, and analysis of data.</span></span> <span data-ttu-id="ba04d-109">Hive sorguları SQL benzer bir sorgu dili HiveQL yazılır.</span><span class="sxs-lookup"><span data-stu-id="ba04d-109">Hive queries are written in HiveQL, which is a query language similar to SQL.</span></span>

<span data-ttu-id="ba04d-110">Hive, büyük ölçüde yapılandırılmamış veriler üzerinde proje yapısını olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="ba04d-110">Hive allows you to project structure on largely unstructured data.</span></span> <span data-ttu-id="ba04d-111">Yapı tanımladıktan sonra Java veya MapReduce bilgisi olmadan verileri sorgulamak için HiveQL kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ba04d-111">After you define the structure, you can use HiveQL to query the data without knowledge of Java or MapReduce.</span></span>

<span data-ttu-id="ba04d-112">Hdınsight belirli iş yükleri için ayarlanmış birkaç küme türler sağlar.</span><span class="sxs-lookup"><span data-stu-id="ba04d-112">HDInsight provides several cluster types, which are tuned for specific workloads.</span></span> <span data-ttu-id="ba04d-113">Aşağıdaki küme türleri Hive sorguları için en sık kullanılır:</span><span class="sxs-lookup"><span data-stu-id="ba04d-113">The following cluster types are most often used for Hive queries:</span></span>

* <span data-ttu-id="ba04d-114">__Etkileşimli Hive__: sağlayan bir Hadoop kümesine [düşük gecikme süresi analitik işleme (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) işlevselliği etkileşimli sorgular için yanıt sürelerini geliştirebilir.</span><span class="sxs-lookup"><span data-stu-id="ba04d-114">__Interactive Hive__: A Hadoop cluster that provides [Low Latency Analytical Processing (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) functionality to improve response times for interactive queries.</span></span> <span data-ttu-id="ba04d-115">Daha fazla bilgi için bkz: [başlayarak etkileşimli hdınsight'ta Hive](hdinsight-hadoop-use-interactive-hive.md) belge.</span><span class="sxs-lookup"><span data-stu-id="ba04d-115">For more information, see the [Start with Interactive Hive in HDInsight](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

* <span data-ttu-id="ba04d-116">__Hadoop__: toplu işlem iş yüklerini işlemek için ayarlanmış bir Hadoop kümesi.</span><span class="sxs-lookup"><span data-stu-id="ba04d-116">__Hadoop__: A Hadoop cluster that is tuned for batch processing workloads.</span></span> <span data-ttu-id="ba04d-117">Daha fazla bilgi için bkz: [Başlat hdınsight'ta Hadoop ile](hdinsight-hadoop-linux-tutorial-get-started.md) belge.</span><span class="sxs-lookup"><span data-stu-id="ba04d-117">For more information, see the [Start with Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) document.</span></span>

* <span data-ttu-id="ba04d-118">__Spark__: Apache Spark Hive ile çalışmak için yerleşik bir işleve sahiptir.</span><span class="sxs-lookup"><span data-stu-id="ba04d-118">__Spark__: Apache Spark has built-in functionality for working with Hive.</span></span> <span data-ttu-id="ba04d-119">Daha fazla bilgi için bkz: [hdınsight'ta Spark başlayarak](hdinsight-apache-spark-jupyter-spark-sql.md) belge.</span><span class="sxs-lookup"><span data-stu-id="ba04d-119">For more information, see the [Start with Spark on HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) document.</span></span>

* <span data-ttu-id="ba04d-120">__HBase__: HiveQL, HBase içinde depolanan verileri için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="ba04d-120">__HBase__: HiveQL can be used to query data stored in HBase.</span></span> <span data-ttu-id="ba04d-121">Daha fazla bilgi için bkz: [hdınsight'ta HBase ile başlar](hdinsight-hbase-tutorial-get-started-linux.md) belge.</span><span class="sxs-lookup"><span data-stu-id="ba04d-121">For more information, see the [Start with HBase on HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) document.</span></span>

## <a name="how-to-use-hive"></a><span data-ttu-id="ba04d-122">Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="ba04d-122">How to use Hive</span></span>

<span data-ttu-id="ba04d-123">Hdınsight ile Hive kullanma bulmak için aşağıdaki tabloyu kullanın:</span><span class="sxs-lookup"><span data-stu-id="ba04d-123">Use the following table to discover how to use Hive with HDInsight:</span></span>

| <span data-ttu-id="ba04d-124">**Bu yöntemi kullanmak** isterseniz...</span><span class="sxs-lookup"><span data-stu-id="ba04d-124">**Use this method** if you want...</span></span> | <span data-ttu-id="ba04d-125">.. .an **etkileşimli** Kabuk</span><span class="sxs-lookup"><span data-stu-id="ba04d-125">...an **interactive** shell</span></span> | <span data-ttu-id="ba04d-126">... **toplu** işleme</span><span class="sxs-lookup"><span data-stu-id="ba04d-126">...**batch** processing</span></span> | <span data-ttu-id="ba04d-127">.. hemen bu **küme işletim sistemi**</span><span class="sxs-lookup"><span data-stu-id="ba04d-127">...with this **cluster operating system**</span></span> | <span data-ttu-id="ba04d-128">.. .from bu **istemci işletim sistemi**</span><span class="sxs-lookup"><span data-stu-id="ba04d-128">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="ba04d-129">Hive görünümü</span><span class="sxs-lookup"><span data-stu-id="ba04d-129">Hive View</span></span>](hdinsight-hadoop-use-hive-ambari-view.md) |<span data-ttu-id="ba04d-130">✔</span><span class="sxs-lookup"><span data-stu-id="ba04d-130">✔</span></span> |<span data-ttu-id="ba04d-131">✔</span><span class="sxs-lookup"><span data-stu-id="ba04d-131">✔</span></span> |<span data-ttu-id="ba04d-132">Linux</span><span class="sxs-lookup"><span data-stu-id="ba04d-132">Linux</span></span> |<span data-ttu-id="ba04d-133">(Herhangi bir tarayıcı tabanlı)</span><span class="sxs-lookup"><span data-stu-id="ba04d-133">Any (browser based)</span></span> |
| [<span data-ttu-id="ba04d-134">Beeline istemci</span><span class="sxs-lookup"><span data-stu-id="ba04d-134">Beeline client</span></span>](hdinsight-hadoop-use-hive-beeline.md) |<span data-ttu-id="ba04d-135">✔</span><span class="sxs-lookup"><span data-stu-id="ba04d-135">✔</span></span> |<span data-ttu-id="ba04d-136">✔</span><span class="sxs-lookup"><span data-stu-id="ba04d-136">✔</span></span> |<span data-ttu-id="ba04d-137">Linux</span><span class="sxs-lookup"><span data-stu-id="ba04d-137">Linux</span></span> |<span data-ttu-id="ba04d-138">Linux, UNIX, Mac OS X veya Windows</span><span class="sxs-lookup"><span data-stu-id="ba04d-138">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="ba04d-139">REST API</span><span class="sxs-lookup"><span data-stu-id="ba04d-139">REST API</span></span>](hdinsight-hadoop-use-hive-curl.md) |&nbsp; |<span data-ttu-id="ba04d-140">✔</span><span class="sxs-lookup"><span data-stu-id="ba04d-140">✔</span></span> |<span data-ttu-id="ba04d-141">Linux veya Windows *</span><span class="sxs-lookup"><span data-stu-id="ba04d-141">Linux or Windows*</span></span> |<span data-ttu-id="ba04d-142">Linux, UNIX, Mac OS X veya Windows</span><span class="sxs-lookup"><span data-stu-id="ba04d-142">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="ba04d-143">Visual Studio için Hdınsight araçları</span><span class="sxs-lookup"><span data-stu-id="ba04d-143">HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-use-hive-visual-studio.md) |&nbsp; |<span data-ttu-id="ba04d-144">✔</span><span class="sxs-lookup"><span data-stu-id="ba04d-144">✔</span></span> |<span data-ttu-id="ba04d-145">Linux veya Windows *</span><span class="sxs-lookup"><span data-stu-id="ba04d-145">Linux or Windows*</span></span> |<span data-ttu-id="ba04d-146">Windows</span><span class="sxs-lookup"><span data-stu-id="ba04d-146">Windows</span></span> |
| [<span data-ttu-id="ba04d-147">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba04d-147">Windows PowerShell</span></span>](hdinsight-hadoop-use-hive-powershell.md) |&nbsp; |<span data-ttu-id="ba04d-148">✔</span><span class="sxs-lookup"><span data-stu-id="ba04d-148">✔</span></span> |<span data-ttu-id="ba04d-149">Linux veya Windows *</span><span class="sxs-lookup"><span data-stu-id="ba04d-149">Linux or Windows*</span></span> |<span data-ttu-id="ba04d-150">Windows</span><span class="sxs-lookup"><span data-stu-id="ba04d-150">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="ba04d-151">\*Linux üzerinde Hdınsight sürüm 3.4 veya büyük kullanılan yalnızca işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="ba04d-151">\* Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ba04d-152">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="ba04d-152">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="ba04d-153">Bir Windows tabanlı Hdınsight kümesi kullanıyorsanız, kullanabileceğiniz [sorgu konsol](hdinsight-hadoop-use-hive-query-console.md) tarayıcınızdan veya [Uzak Masaüstü](hdinsight-hadoop-use-hive-remote-desktop.md) Hive sorguları çalıştırmak için.</span><span class="sxs-lookup"><span data-stu-id="ba04d-153">If you are using a Windows-based HDInsight cluster, you can use the [Query console](hdinsight-hadoop-use-hive-query-console.md) from your browser or [Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md) to run Hive queries.</span></span>

## <a name="hiveql-language-reference"></a><span data-ttu-id="ba04d-154">HiveQL dil başvurusu</span><span class="sxs-lookup"><span data-stu-id="ba04d-154">HiveQL language reference</span></span>

<span data-ttu-id="ba04d-155">HiveQL dil başvurusu bulunan [dil el ile (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span><span class="sxs-lookup"><span data-stu-id="ba04d-155">HiveQL language reference is available in the [language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span></span>

## <a name="hive-and-data-structure"></a><span data-ttu-id="ba04d-156">Hive ve veri yapısı</span><span class="sxs-lookup"><span data-stu-id="ba04d-156">Hive and data structure</span></span>

<span data-ttu-id="ba04d-157">Hive yapılandırılmış ve yarı yapılandırılmış verilerle çalışmak nasıl bilir.</span><span class="sxs-lookup"><span data-stu-id="ba04d-157">Hive understands how to work with structured and semi-structured data.</span></span> <span data-ttu-id="ba04d-158">Burada alanları belirli karakterleriyle sınırlandırılır Örneğin, metin dosyaları.</span><span class="sxs-lookup"><span data-stu-id="ba04d-158">For example, text files where the fields are delimited by specific characters.</span></span> <span data-ttu-id="ba04d-159">Aşağıdaki HiveQL deyimi boşlukla ayrılmış veriler üzerinde bir tablo oluşturur:</span><span class="sxs-lookup"><span data-stu-id="ba04d-159">The following HiveQL statement creates a table over space-delimited data:</span></span>

```hiveql
CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
STORED AS TEXTFILE LOCATION '/example/data/';
```

<span data-ttu-id="ba04d-160">Hive ayrıca özel destekler **seri hale getirici/deserializers (SerDe)** karmaşık veya düzensiz yapılandırılmış veriler için.</span><span class="sxs-lookup"><span data-stu-id="ba04d-160">Hive also supports custom **serializer/deserializers (SerDe)** for complex or irregularly structured data.</span></span> <span data-ttu-id="ba04d-161">Daha fazla bilgi için bkz: [Hdınsight ile özel bir JSON SerDe kullanmayı](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) belge.</span><span class="sxs-lookup"><span data-stu-id="ba04d-161">For more information, see the [How to use a custom JSON SerDe with HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) document.</span></span>

<span data-ttu-id="ba04d-162">Hive tarafından desteklenen dosya biçimleri hakkında daha fazla bilgi için bkz: [dil el ile (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span><span class="sxs-lookup"><span data-stu-id="ba04d-162">For more information on file formats supported by Hive, see the [Language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span></span>

## <a name="hive-internal-tables-vs-external-tables"></a><span data-ttu-id="ba04d-163">İç tablolar vs dış tablolara yığını</span><span class="sxs-lookup"><span data-stu-id="ba04d-163">Hive internal tables vs external tables</span></span>

<span data-ttu-id="ba04d-164">Hive ile oluşturabileceğiniz tablolar iki tür vardır:</span><span class="sxs-lookup"><span data-stu-id="ba04d-164">There are two types of tables that you can create with Hive:</span></span>

* <span data-ttu-id="ba04d-165">__İç__: Hive veri ambarında depolanır.</span><span class="sxs-lookup"><span data-stu-id="ba04d-165">__Internal__: Data is stored in the Hive data warehouse.</span></span> <span data-ttu-id="ba04d-166">Veri ambarı bulunur `/hive/warehouse/` kümenin varsayılan depolama.</span><span class="sxs-lookup"><span data-stu-id="ba04d-166">The data warehouse is located at `/hive/warehouse/` on the default storage for the cluster.</span></span>

    <span data-ttu-id="ba04d-167">İç kullanım ne zaman tabloları:</span><span class="sxs-lookup"><span data-stu-id="ba04d-167">Use internal tables when:</span></span>

    * <span data-ttu-id="ba04d-168">Veri geçicidir.</span><span class="sxs-lookup"><span data-stu-id="ba04d-168">Data is temporary.</span></span>
    * <span data-ttu-id="ba04d-169">Hive tablosu ve veri yaşam döngüsü yönetmek istiyorsunuz.</span><span class="sxs-lookup"><span data-stu-id="ba04d-169">You want Hive to manage the lifecycle of the table and data.</span></span>

* <span data-ttu-id="ba04d-170">__Dış__: dışında veri ambarında depolanır.</span><span class="sxs-lookup"><span data-stu-id="ba04d-170">__External__: Data is stored outside the data warehouse.</span></span> <span data-ttu-id="ba04d-171">Veri kümesi tarafından herhangi bir depolama alanı üzerinde erişilebilir depolanabilir.</span><span class="sxs-lookup"><span data-stu-id="ba04d-171">The data can be stored on any storage accessible by the cluster.</span></span>

    <span data-ttu-id="ba04d-172">Kullanım dış tablolar:</span><span class="sxs-lookup"><span data-stu-id="ba04d-172">Use external tables when:</span></span>

    * <span data-ttu-id="ba04d-173">Verileri de Hive dışında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ba04d-173">The data is also used outside of Hive.</span></span> <span data-ttu-id="ba04d-174">Örneğin, veri dosyalarını (yani dosyaları kilit yok.) başka bir işlem tarafından güncelleştirilir</span><span class="sxs-lookup"><span data-stu-id="ba04d-174">For example, the data files are updated by another process (that does not lock the files.)</span></span>
    * <span data-ttu-id="ba04d-175">Veri tablosu bile silmeden sonra temel alınan konumda kalır gerekiyor.</span><span class="sxs-lookup"><span data-stu-id="ba04d-175">Data needs to remain in the underlying location, even after dropping the table.</span></span>
    * <span data-ttu-id="ba04d-176">Varsayılan olmayan depolama hesabı gibi özel bir konuma gerekir.</span><span class="sxs-lookup"><span data-stu-id="ba04d-176">You need a custom location, such as a non-default storage account.</span></span>
    * <span data-ttu-id="ba04d-177">Hive dışında bir program veri biçimi, konum vb. yönetir.</span><span class="sxs-lookup"><span data-stu-id="ba04d-177">A program other than hive manages the data format, location, etc.</span></span>

<span data-ttu-id="ba04d-178">Daha fazla bilgi için bkz: [Hive iç ve dış tablolar giriş] [ cindygross-hive-tables] blog postası.</span><span class="sxs-lookup"><span data-stu-id="ba04d-178">For more information, see the [Hive Internal and External Tables Intro][cindygross-hive-tables] blog post.</span></span>

## <a name="user-defined-functions-udf"></a><span data-ttu-id="ba04d-179">Kullanıcı tanımlı işlevler (UDF)</span><span class="sxs-lookup"><span data-stu-id="ba04d-179">User-defined functions (UDF)</span></span>

<span data-ttu-id="ba04d-180">Hive ayrıca uzatabilirsiniz aracılığıyla **kullanıcı tanımlı işlevler (UDF)**.</span><span class="sxs-lookup"><span data-stu-id="ba04d-180">Hive can also be extended through **user-defined functions (UDF)**.</span></span> <span data-ttu-id="ba04d-181">Bir UDF işlev veya kolayca modellenir değil mantığı içinde HiveQL uygulamak sağlar.</span><span class="sxs-lookup"><span data-stu-id="ba04d-181">A UDF allows you to implement functionality or logic that isn't easily modeled in HiveQL.</span></span> <span data-ttu-id="ba04d-182">UDF'ler ile Hive kullanma örneği için aşağıdaki belgelere bakın:</span><span class="sxs-lookup"><span data-stu-id="ba04d-182">For an example of using UDFs with Hive, see the following documents:</span></span>

* [<span data-ttu-id="ba04d-183">Kullanıcı tanımlı bir Java işlev ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="ba04d-183">Use a Java user-defined function with Hive</span></span>](hdinsight-hadoop-hive-java-udf.md)

* [<span data-ttu-id="ba04d-184">Kullanıcı tanımlı bir Python işlev Hive veya Pig kullanın</span><span class="sxs-lookup"><span data-stu-id="ba04d-184">Use a Python user-defined function with Hive and Pig</span></span>](hdinsight-python.md)

* [<span data-ttu-id="ba04d-185">C# kullanıcı tanımlı bir işlev Hive veya Pig kullanın</span><span class="sxs-lookup"><span data-stu-id="ba04d-185">Use a C# user-defined function with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="ba04d-186">Hdınsight için özel bir Hive kullanıcı tanımlı işlev ekleme</span><span class="sxs-lookup"><span data-stu-id="ba04d-186">How to add a custom Hive user-defined function to HDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

* [<span data-ttu-id="ba04d-187">Tarih/saat biçimlerinden Hive zaman damgası için dönüştürmek için bir örnek Hive kullanıcı tanımlı işlevi</span><span class="sxs-lookup"><span data-stu-id="ba04d-187">An example Hive user-defined function to convert date/time formats to Hive timestamp</span></span>](https://github.com/Azure-Samples/hdinsight-java-hive-udf)

## <span data-ttu-id="ba04d-188"><a id="data"></a>Örnek veri</span><span class="sxs-lookup"><span data-stu-id="ba04d-188"><a id="data"></a>Example data</span></span>

<span data-ttu-id="ba04d-189">Hdınsight'ta Hive gelen önceden yüklenmiş bir iç tablosu adlı `hivesampletable`.</span><span class="sxs-lookup"><span data-stu-id="ba04d-189">Hive on HDInsight comes pre-loaded with an internal table named `hivesampletable`.</span></span> <span data-ttu-id="ba04d-190">Hdınsight ile Hive kullanılabilir bir örnek veri kümeleri de sağlar.</span><span class="sxs-lookup"><span data-stu-id="ba04d-190">HDInsight also provides example data sets that can be used with Hive.</span></span> <span data-ttu-id="ba04d-191">Bu veri kümeleri depolanmış `/example/data` ve `/HdiSamples` dizinleri.</span><span class="sxs-lookup"><span data-stu-id="ba04d-191">These data sets are stored in the `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="ba04d-192">Bu dizinleri, kümeniz için varsayılan depolama yok.</span><span class="sxs-lookup"><span data-stu-id="ba04d-192">These directories exist in the default storage for your cluster.</span></span>

## <span data-ttu-id="ba04d-193"><a id="job"></a>Örnek Hive sorgusu</span><span class="sxs-lookup"><span data-stu-id="ba04d-193"><a id="job"></a>Example Hive query</span></span>

<span data-ttu-id="ba04d-194">Aşağıdaki HiveQL ifadelerini sütunları üzerine proje `/example/data/sample.log` dosyası:</span><span class="sxs-lookup"><span data-stu-id="ba04d-194">The following HiveQL statements project columns onto the `/example/data/sample.log` file:</span></span>

    set hive.execution.engine=tez;
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

<span data-ttu-id="ba04d-195">Önceki örnekte, HiveQL ifadelerini aşağıdaki eylemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ba04d-195">In the previous example, the HiveQL statements perform the following actions:</span></span>

* <span data-ttu-id="ba04d-196">`set hive.execution.engine=tez;`: Yürütme altyapısı, Tez kullanacak şekilde ayarlar.</span><span class="sxs-lookup"><span data-stu-id="ba04d-196">`set hive.execution.engine=tez;`: Sets the execution engine to use Tez.</span></span> <span data-ttu-id="ba04d-197">Tez yerine MapReduce kullanarak sorgu performansı bir artış sağlayabilir.</span><span class="sxs-lookup"><span data-stu-id="ba04d-197">Using Tez instead of MapReduce can provide an increase in query performance.</span></span> <span data-ttu-id="ba04d-198">Tez hakkında daha fazla bilgi için bkz: [iyileştirilmiş performans için Apache Tez kullanma](#usetez) bölümü.</span><span class="sxs-lookup"><span data-stu-id="ba04d-198">For more information on Tez, see the [Use Apache Tez for improved performance](#usetez) section.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ba04d-199">Bu deyim yalnızca olan Windows tabanlı Hdınsight kümesi kullanılırken gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ba04d-199">This statement is only required when using a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="ba04d-200">Tez Linux tabanlı Hdınsight için varsayılan yürütme altyapısıdır.</span><span class="sxs-lookup"><span data-stu-id="ba04d-200">Tez is the default execution engine for Linux-based HDInsight.</span></span>

* <span data-ttu-id="ba04d-201">`DROP TABLE`: Tablo zaten varsa dosyayı silin.</span><span class="sxs-lookup"><span data-stu-id="ba04d-201">`DROP TABLE`: If the table already exists, delete it.</span></span>

* <span data-ttu-id="ba04d-202">`CREATE EXTERNAL TABLE`: Oluşturur Yeni bir **dış** Hive tablo.</span><span class="sxs-lookup"><span data-stu-id="ba04d-202">`CREATE EXTERNAL TABLE`: Creates a new **external** table in Hive.</span></span> <span data-ttu-id="ba04d-203">Dış tablolara tablo tanımı kovanında yalnızca depolar.</span><span class="sxs-lookup"><span data-stu-id="ba04d-203">External tables only store the table definition in Hive.</span></span> <span data-ttu-id="ba04d-204">Veriler özgün konumdaki ve özgün biçiminde bırakılır.</span><span class="sxs-lookup"><span data-stu-id="ba04d-204">The data is left in the original location and in the original format.</span></span>

* <span data-ttu-id="ba04d-205">`ROW FORMAT`: Veri nasıl biçimlendirilmiş Hive söyler.</span><span class="sxs-lookup"><span data-stu-id="ba04d-205">`ROW FORMAT`: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="ba04d-206">Bu durumda, her günlüğün içinde alanlar boşlukla ayrılır.</span><span class="sxs-lookup"><span data-stu-id="ba04d-206">In this case, the fields in each log are separated by a space.</span></span>

* <span data-ttu-id="ba04d-207">`STORED AS TEXTFILE LOCATION`: Veri depolandığı Hive söyler ( `example/data` dizini) ve metin olarak depolanır.</span><span class="sxs-lookup"><span data-stu-id="ba04d-207">`STORED AS TEXTFILE LOCATION`: Tells Hive where the data is stored (the `example/data` directory) and that it is stored as text.</span></span> <span data-ttu-id="ba04d-208">Verileri bir dosyada yer veya birden çok dosya dizininde üzerinden yayılan.</span><span class="sxs-lookup"><span data-stu-id="ba04d-208">The data can be in one file or spread across multiple files within the directory.</span></span>

* <span data-ttu-id="ba04d-209">`SELECT`: Tüm satırların sayımını seçer Burada sütun **t4** değeri içeren **[Hata]**.</span><span class="sxs-lookup"><span data-stu-id="ba04d-209">`SELECT`: Selects a count of all rows where the column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="ba04d-210">Bu ifade değerini döndürür **3** çünkü bu değer içeren üç satır vardır.</span><span class="sxs-lookup"><span data-stu-id="ba04d-210">This statement returns a value of **3** because there are three rows that contain this value.</span></span>

* <span data-ttu-id="ba04d-211">`INPUT__FILE__NAME LIKE '%.log'`-Dizindeki tüm dosyaları şema uygulamak hive çalışır.</span><span class="sxs-lookup"><span data-stu-id="ba04d-211">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts to apply the schema to all files in the directory.</span></span> <span data-ttu-id="ba04d-212">Bu durumda, dizin şeması eşleşmiyor dosyalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="ba04d-212">In this case, the directory contains files that do not match the schema.</span></span> <span data-ttu-id="ba04d-213">Çöp veri sonuçlarında önlemek için bu bildirimi Hive biz yalnızca veri biten dosyalarından döndürmesi gerektiğini bildirir. günlük.</span><span class="sxs-lookup"><span data-stu-id="ba04d-213">To prevent garbage data in the results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

> [!NOTE]
> <span data-ttu-id="ba04d-214">Dış kaynak tarafından güncelleştirilecek temel alınan veri beklediğiniz dış tablolara kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ba04d-214">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="ba04d-215">Örneğin, bir otomatik veri karşıya yükleme işlemi veya MapReduce işlemi.</span><span class="sxs-lookup"><span data-stu-id="ba04d-215">For example, an automated data upload process, or MapReduce operation.</span></span>
>
> <span data-ttu-id="ba04d-216">Bir dış tablo bırakma mu **değil** verileri silmek için yalnızca tablo tanımını siler.</span><span class="sxs-lookup"><span data-stu-id="ba04d-216">Dropping an external table does **not** delete the data, it only deletes the table definition.</span></span>

<span data-ttu-id="ba04d-217">Oluşturmak için bir **iç** tablo dış yerine, aşağıdaki HiveQL kullanın:</span><span class="sxs-lookup"><span data-stu-id="ba04d-217">To create an **internal** table instead of external, use the following HiveQL:</span></span>

    set hive.execution.engine=tez;
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs
    SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';

<span data-ttu-id="ba04d-218">Bu ifadeler aşağıdaki eylemleri gerçekleştirin:</span><span class="sxs-lookup"><span data-stu-id="ba04d-218">These statements perform the following actions:</span></span>

* <span data-ttu-id="ba04d-219">`CREATE TABLE IF NOT EXISTS`: Tablo mevcut değilse oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ba04d-219">`CREATE TABLE IF NOT EXISTS`: If the table does not exist, create it.</span></span> <span data-ttu-id="ba04d-220">Çünkü **dış** anahtar sözcüğü kullanılmaz, bu deyim bir iç tablosu oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ba04d-220">Because the **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="ba04d-221">Tablo Hive veri ambarında depolanır ve tamamen Hive tarafından yönetilir.</span><span class="sxs-lookup"><span data-stu-id="ba04d-221">The table is stored in the Hive data warehouse and is managed completely by Hive.</span></span>

* <span data-ttu-id="ba04d-222">`STORED AS ORC`: En iyi duruma getirilmiş satır sütunlu (ORC) biçiminde verileri depolar.</span><span class="sxs-lookup"><span data-stu-id="ba04d-222">`STORED AS ORC`: Stores the data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="ba04d-223">ORC Hive verilerini depolamak için yüksek oranda en iyi duruma getirilmiş ve verimli bir biçimidir.</span><span class="sxs-lookup"><span data-stu-id="ba04d-223">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

* <span data-ttu-id="ba04d-224">`INSERT OVERWRITE ... SELECT`: Satırları seçer **log4jLogs** içeren tablo **[Hata]**ve ardından verileri ekler **günlüklerini** tablo.</span><span class="sxs-lookup"><span data-stu-id="ba04d-224">`INSERT OVERWRITE ... SELECT`: Selects rows from the **log4jLogs** table that contains **[ERROR]**, and then inserts the data into the **errorLogs** table.</span></span>

> [!NOTE]
> <span data-ttu-id="ba04d-225">Dış tablolara, bir iç tablosu bırakarak temel alınan verileri siler.</span><span class="sxs-lookup"><span data-stu-id="ba04d-225">Unlike external tables, dropping an internal table also deletes the underlying data.</span></span>

## <a name="improve-hive-query-performance"></a><span data-ttu-id="ba04d-226">Hive sorgu performansı</span><span class="sxs-lookup"><span data-stu-id="ba04d-226">Improve Hive query performance</span></span>

### <span data-ttu-id="ba04d-227"><a id="usetez"></a>Apache Tez</span><span class="sxs-lookup"><span data-stu-id="ba04d-227"><a id="usetez"></a>Apache Tez</span></span>

<span data-ttu-id="ba04d-228">[Apache Tez](http://tez.apache.org) çok daha verimli bir şekilde ölçekli olarak çalıştırmak için Hive gibi veri yoğun uygulamalar sağlayan bir çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="ba04d-228">[Apache Tez](http://tez.apache.org) is a framework that allows data intensive applications, such as Hive, to run much more efficiently at scale.</span></span> <span data-ttu-id="ba04d-229">Tez Linux tabanlı Hdınsight kümeleri için varsayılan olarak etkindir.</span><span class="sxs-lookup"><span data-stu-id="ba04d-229">Tez is enabled by default for Linux-based HDInsight clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="ba04d-230">Tez şu anda Windows tabanlı Hdınsight kümeleri için varsayılan olarak kapalıdır ve etkinleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ba04d-230">Tez is currently off by default for Windows-based HDInsight clusters and it must be enabled.</span></span> <span data-ttu-id="ba04d-231">Tez yararlanmak için aşağıdaki değeri bir Hive sorgusu için ayarlanmalıdır:</span><span class="sxs-lookup"><span data-stu-id="ba04d-231">To take advantage of Tez, the following value must be set for a Hive query:</span></span>
>
> `set hive.execution.engine=tez;`
>
> <span data-ttu-id="ba04d-232">Tez Linux tabanlı Hdınsight kümeleri için varsayılan altyapısıdır.</span><span class="sxs-lookup"><span data-stu-id="ba04d-232">Tez is the default engine for Linux-based HDInsight clusters.</span></span>

<span data-ttu-id="ba04d-233">[Hive Tez tasarım belgeleri](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) uygulama seçeneklerine ve ayarlama yapılandırmalar hakkında ayrıntılar içerir.</span><span class="sxs-lookup"><span data-stu-id="ba04d-233">The [Hive on Tez design documents](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) contains details about the implementation choices and tuning configurations.</span></span>

<span data-ttu-id="ba04d-234">İşlerini hata ayıklamaya yardımcı olmak için Tez kullanılarak çalıştırıldı, aşağıdaki web Tez işlerinde ayrıntılarını görüntülemek izin Uı'lar Hdınsight sağlar:</span><span class="sxs-lookup"><span data-stu-id="ba04d-234">To aid in debugging jobs ran using Tez, HDInsight provides the following web UIs that allow you to view details of Tez jobs:</span></span>

* [<span data-ttu-id="ba04d-235">Linux tabanlı Hdınsight üzerinde Ambari Tez görünümünü kullanın</span><span class="sxs-lookup"><span data-stu-id="ba04d-235">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

* [<span data-ttu-id="ba04d-236">Windows tabanlı Hdınsight üzerinde Tez kullanıcı arabirimini kullanma</span><span class="sxs-lookup"><span data-stu-id="ba04d-236">Use the Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)

### <a name="low-latency-analytical-processing-llap"></a><span data-ttu-id="ba04d-237">Düşük gecikme süresi analitik işleme (LLAP)</span><span class="sxs-lookup"><span data-stu-id="ba04d-237">Low Latency Analytical Processing (LLAP)</span></span>

<span data-ttu-id="ba04d-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (Canlı uzun ve işlem da bilinir) Hive sorguları bellek içi önbelleğe alma veren 2.0 yeni bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="ba04d-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (sometimes known as Live Long and Process) is a new feature in Hive 2.0 that allows in-memory caching of queries.</span></span> <span data-ttu-id="ba04d-239">LLAP yapar kadar daha hızlı Hive sorguları [26 x bazı durumlarda 1.x Hive çok hızlı](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span><span class="sxs-lookup"><span data-stu-id="ba04d-239">LLAP makes Hive queries much faster, up to [26x faster than Hive 1.x in some cases](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span></span>

<span data-ttu-id="ba04d-240">Hdınsight LLAP etkileşimli Hive küme türü sağlar.</span><span class="sxs-lookup"><span data-stu-id="ba04d-240">HDInsight provides LLAP in the Interactive Hive cluster type.</span></span> <span data-ttu-id="ba04d-241">Daha fazla bilgi için bkz: [Başlat ile etkileşimli Hive](hdinsight-hadoop-use-interactive-hive.md) belge.</span><span class="sxs-lookup"><span data-stu-id="ba04d-241">For more information, see the [Start with Interactive Hive](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

## <a name="hive-jobs-and-sql-server-integration-services"></a><span data-ttu-id="ba04d-242">Hive işleri ve SQL Server Integration Services</span><span class="sxs-lookup"><span data-stu-id="ba04d-242">Hive jobs and SQL Server Integration Services</span></span>

<span data-ttu-id="ba04d-243">Hive işi çalıştırmak için SQL Server Integration Services (SSIS) kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ba04d-243">You can use SQL Server Integration Services (SSIS) to run a Hive job.</span></span> <span data-ttu-id="ba04d-244">Azure Feature Pack SSIS için Hdınsight'ta Hive işlerle çalışma aşağıdaki bileşenleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="ba04d-244">The Azure Feature Pack for SSIS provides the following components that work with Hive jobs on HDInsight.</span></span>

* <span data-ttu-id="ba04d-245">[Azure Hdınsight Hive görevi][hivetask]</span><span class="sxs-lookup"><span data-stu-id="ba04d-245">[Azure HDInsight Hive Task][hivetask]</span></span>

* <span data-ttu-id="ba04d-246">[Azure aboneliği Bağlantı Yöneticisi][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="ba04d-246">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="ba04d-247">Azure Feature Pack hakkında daha fazla bilgi için SSIS [burada][ssispack].</span><span class="sxs-lookup"><span data-stu-id="ba04d-247">Learn more about the Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="ba04d-248"><a id="nextsteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ba04d-248"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="ba04d-249">Hive nedir ve hdınsight'ta Hadoop ile kullanma öğrendiğinize göre Azure Hdınsight ile çalışmak için diğer yollarını keşfetmek için aşağıdaki bağlantıları kullanın.</span><span class="sxs-lookup"><span data-stu-id="ba04d-249">Now that you've learned what Hive is and how to use it with Hadoop in HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* <span data-ttu-id="ba04d-250">[HDInsight'a veri yükleme][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="ba04d-250">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="ba04d-251">[HDInsight ile Pig kullanma][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="ba04d-251">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="ba04d-252">[Hdınsight ile MapReduce işleri kullanma][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="ba04d-252">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

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
