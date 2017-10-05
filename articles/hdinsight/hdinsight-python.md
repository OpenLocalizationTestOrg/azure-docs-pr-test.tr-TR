---
title: "Python UDF Apache ile Hive veya Pig - Azure Hdınsight | Microsoft Docs"
description: "Hdınsight'ta Hadoop teknoloji yığınının Azure üzerinde Python kullanıcı tanımlı işlevler (UDF) Hive ve Pig kullanmayı öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c44d6606-28cd-429b-b535-235e8f34a664
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/17/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 9b67ded05a52f1e68580434667495cf6cf939871
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="use-python-user-defined-functions-udf-with-hive-and-pig-in-hdinsight"></a><span data-ttu-id="185fc-103">Hdınsight'ta kullanım Python kullanıcı tanımlı işlevler (UDF) Hive veya Pig ile</span><span class="sxs-lookup"><span data-stu-id="185fc-103">Use Python User Defined Functions (UDF) with Hive and Pig in HDInsight</span></span>

<span data-ttu-id="185fc-104">Apache Hive veya Pig içinde Azure hdınsight'ta Hadoop ile Python kullanıcı tanımlı işlevler (UDF) kullanmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="185fc-104">Learn how to use Python user-defined functions (UDF) with Apache Hive and Pig in Hadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="185fc-105"><a name="python"></a>Hdınsight üzerinde Python</span><span class="sxs-lookup"><span data-stu-id="185fc-105"><a name="python"></a>Python on HDInsight</span></span>

<span data-ttu-id="185fc-106">Python2.7 Hdınsight 3.0 ve sonraki sürümlerinde varsayılan olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="185fc-106">Python2.7 is installed by default on HDInsight 3.0 and later.</span></span> <span data-ttu-id="185fc-107">Apache Hive Python bu sürümü ile akış işleme için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="185fc-107">Apache Hive can be used with this version of Python for stream processing.</span></span> <span data-ttu-id="185fc-108">Akış işleme, Hive ve UDF arasında veri iletmek için STDOUT ve STDIN kullanır.</span><span class="sxs-lookup"><span data-stu-id="185fc-108">Stream processing uses STDOUT and STDIN to pass data between Hive and the UDF.</span></span>

<span data-ttu-id="185fc-109">Hdınsight, ayrıca Java'da yazılmış bir Python uygulaması Jython içerir.</span><span class="sxs-lookup"><span data-stu-id="185fc-109">HDInsight also includes Jython, which is a Python implementation written in Java.</span></span> <span data-ttu-id="185fc-110">Jython doğrudan Java sanal makinesi üzerinde çalışır ve akış kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="185fc-110">Jython runs directly on the Java Virtual Machine and does not use streaming.</span></span> <span data-ttu-id="185fc-111">Jython önerilen Python yorumlayıcı Python ile Pig kullanıldığında.</span><span class="sxs-lookup"><span data-stu-id="185fc-111">Jython is the recommended Python interpreter when using Python with Pig.</span></span>

> [!WARNING]
> <span data-ttu-id="185fc-112">Bu belgede yer alan adımlar aşağıdaki varsayımlar olun:</span><span class="sxs-lookup"><span data-stu-id="185fc-112">The steps in this document make the following assumptions:</span></span> 
>
> * <span data-ttu-id="185fc-113">Python betiklerini yerel geliştirme ortamınızı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="185fc-113">You create the Python scripts on your local development environment.</span></span>
> * <span data-ttu-id="185fc-114">Komut dosyalarını kullanarak Hdınsight'a yükleme `scp` yerel bir Bash oturumu veya sağlanan PowerShell komut dosyası komutu.</span><span class="sxs-lookup"><span data-stu-id="185fc-114">You upload the scripts to HDInsight using either the `scp` command from a local Bash session or the provided PowerShell script.</span></span>
>
> <span data-ttu-id="185fc-115">Kullanmak istiyorsanız, [Azure bulut Kabuğu (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) gerekir sonra Hdınsight ile çalışmak için önizleme:</span><span class="sxs-lookup"><span data-stu-id="185fc-115">If you want to use the [Azure Cloud Shell (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) preview to work with HDInsight, then you must:</span></span>
>
> * <span data-ttu-id="185fc-116">Bulut Kabuk ortamı içindeki komut dosyaları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="185fc-116">Create the scripts inside the cloud shell environment.</span></span>
> * <span data-ttu-id="185fc-117">Kullanım `scp` Hdınsight bulut Kabuğu'ndan dosyaları karşıya yüklemek için.</span><span class="sxs-lookup"><span data-stu-id="185fc-117">Use `scp` to upload the files from the cloud shell to HDInsight.</span></span>
> * <span data-ttu-id="185fc-118">Kullanım `ssh` Hdınsight'a bağlanmak ve örnekleri çalıştırmak için bulut Kabuğu'ndan.</span><span class="sxs-lookup"><span data-stu-id="185fc-118">Use `ssh` from the cloud shell to connect to HDInsight and run the examples.</span></span>

## <span data-ttu-id="185fc-119"><a name="hivepython"></a>UDF yığını</span><span class="sxs-lookup"><span data-stu-id="185fc-119"><a name="hivepython"></a>Hive UDF</span></span>

<span data-ttu-id="185fc-120">Python, Hive HiveQL üzerinden gelen bir UDF olarak kullanılabilir `TRANSFORM` deyimi.</span><span class="sxs-lookup"><span data-stu-id="185fc-120">Python can be used as a UDF from Hive through the HiveQL `TRANSFORM` statement.</span></span> <span data-ttu-id="185fc-121">Örneğin, aşağıdaki HiveQL çağırır `hiveudf.py` kümesi için varsayılan Azure depolama hesabına depolanan dosya.</span><span class="sxs-lookup"><span data-stu-id="185fc-121">For example, the following HiveQL invokes the `hiveudf.py` file stored in the default Azure Storage account for the cluster.</span></span>

<span data-ttu-id="185fc-122">**Linux tabanlı Hdınsight**</span><span class="sxs-lookup"><span data-stu-id="185fc-122">**Linux-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'python hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

<span data-ttu-id="185fc-123">**Windows tabanlı Hdınsight**</span><span class="sxs-lookup"><span data-stu-id="185fc-123">**Windows-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'D:\Python27\python.exe hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

> [!NOTE]
> <span data-ttu-id="185fc-124">Windows tabanlı Hdınsight kümelerinde `USING` yan tümcesi Python.exe'yi tam yolunu belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="185fc-124">On Windows-based HDInsight clusters, the `USING` clause must specify the full path to python.exe.</span></span>

<span data-ttu-id="185fc-125">Bu örnek yaptığı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="185fc-125">Here's what this example does:</span></span>

1. <span data-ttu-id="185fc-126">`add file` Dosyasının başında deyimi ekler `hiveudf.py` dağıtılmış önbellek kümedeki tüm düğümler tarafından erişilebilir olması için dosyaya.</span><span class="sxs-lookup"><span data-stu-id="185fc-126">The `add file` statement at the beginning of the file adds the `hiveudf.py` file to the distributed cache, so it's accessible by all nodes in the cluster.</span></span>
2. <span data-ttu-id="185fc-127">`SELECT TRANSFORM ... USING` Deyimi seçer verilerden `hivesampletable`.</span><span class="sxs-lookup"><span data-stu-id="185fc-127">The `SELECT TRANSFORM ... USING` statement selects data from the `hivesampletable`.</span></span> <span data-ttu-id="185fc-128">Ayrıca ClientID, devicemake ve devicemodel değerlere geçirir `hiveudf.py` komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="185fc-128">It also passes the clientid, devicemake, and devicemodel values to the `hiveudf.py` script.</span></span>
3. <span data-ttu-id="185fc-129">`AS` Yan tümcesi açıklar döndürülen alanları `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="185fc-129">The `AS` clause describes the fields returned from `hiveudf.py`.</span></span>

<a name="streamingpy"></a>

### <a name="create-the-hiveudfpy-file"></a><span data-ttu-id="185fc-130">Hiveudf.py dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="185fc-130">Create the hiveudf.py file</span></span>


<span data-ttu-id="185fc-131">Geliştirme ortamınızı adlı bir metin dosyası oluşturun `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="185fc-131">On your development environment, create a text file named `hiveudf.py`.</span></span> <span data-ttu-id="185fc-132">Aşağıdaki kod dosyasının içeriği kullanın:</span><span class="sxs-lookup"><span data-stu-id="185fc-132">Use the following code as the contents of the file:</span></span>

```python
#!/usr/bin/env python
import sys
import string
import hashlib

while True:
    line = sys.stdin.readline()
    if not line:
        break

    line = string.strip(line, "\n ")
    clientid, devicemake, devicemodel = string.split(line, "\t")
    phone_label = devicemake + ' ' + devicemodel
    print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])
```

<span data-ttu-id="185fc-133">Bu komut dosyası, aşağıdaki eylemleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="185fc-133">This script performs the following actions:</span></span>

1. <span data-ttu-id="185fc-134">Veri satırı STDIN okuyun.</span><span class="sxs-lookup"><span data-stu-id="185fc-134">Read a line of data from STDIN.</span></span>
2. <span data-ttu-id="185fc-135">Sondaki yeni satır karakteri kullanarak kaldırılır `string.strip(line, "\n ")`.</span><span class="sxs-lookup"><span data-stu-id="185fc-135">The trailing newline character is removed using `string.strip(line, "\n ")`.</span></span>
3. <span data-ttu-id="185fc-136">Akış işleme yaparken, tek bir satırı her değer arasında bir sekme karakteri ile tüm değerler içeriyor.</span><span class="sxs-lookup"><span data-stu-id="185fc-136">When doing stream processing, a single line contains all the values with a tab character between each value.</span></span> <span data-ttu-id="185fc-137">Bu nedenle `string.split(line, "\t")` yalnızca alanları dönmeden her sekme konumundaki giriş bölmek için kullanılan.</span><span class="sxs-lookup"><span data-stu-id="185fc-137">So `string.split(line, "\t")` can be used to split the input at each tab, returning just the fields.</span></span>
4. <span data-ttu-id="185fc-138">İşlem tamamlandığında, çıkış STDOUT sekmesi her alanı arasında tek bir satır olarak yazılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="185fc-138">When processing is complete, the output must be written to STDOUT as a single line, with a tab between each field.</span></span> <span data-ttu-id="185fc-139">Örneğin, `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span><span class="sxs-lookup"><span data-stu-id="185fc-139">For example, `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span></span>
5. <span data-ttu-id="185fc-140">`while` Döngü Hayır kadar yinelenir `line` okunur.</span><span class="sxs-lookup"><span data-stu-id="185fc-140">The `while` loop repeats until no `line` is read.</span></span>

<span data-ttu-id="185fc-141">Komut dosyası çıkışını bir yapıdır giriş değerlerini `devicemake` ve `devicemodel`ve birleştirilmiş değerinin karması.</span><span class="sxs-lookup"><span data-stu-id="185fc-141">The script output is a concatenation of the input values for `devicemake` and `devicemodel`, and a hash of the concatenated value.</span></span>

<span data-ttu-id="185fc-142">Bkz: [örnekleri çalıştırma](#running) nasıl Hdınsight kümenize Bu örneği çalıştırmak.</span><span class="sxs-lookup"><span data-stu-id="185fc-142">See [Running the examples](#running) for how to run this example on your HDInsight cluster.</span></span>

## <span data-ttu-id="185fc-143"><a name="pigpython"></a>Pig UDF</span><span class="sxs-lookup"><span data-stu-id="185fc-143"><a name="pigpython"></a>Pig UDF</span></span>

<span data-ttu-id="185fc-144">Bir Python komut dosyası Pig gelen bir UDF olarak kullanılabilir `GENERATE` deyimi.</span><span class="sxs-lookup"><span data-stu-id="185fc-144">A Python script can be used as a UDF from Pig through the `GENERATE` statement.</span></span> <span data-ttu-id="185fc-145">Jython veya C Python kullanarak komut dosyasını çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="185fc-145">You can run the script using either Jython or C Python.</span></span>

* <span data-ttu-id="185fc-146">Jython JVM üzerinde çalışır ve yerel olarak Pig çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="185fc-146">Jython runs on the JVM, and can natively be called from Pig.</span></span>
* <span data-ttu-id="185fc-147">C Python bir dış işlem olduğundan, Pig JVM üzerinde verilerden bir Python işlemde çalışan komut için gönderilir.</span><span class="sxs-lookup"><span data-stu-id="185fc-147">C Python is an external process, so the data from Pig on the JVM is sent out to the script running in a Python process.</span></span> <span data-ttu-id="185fc-148">Python komut dosyası çıkışını Pig'ya geri gönderilir.</span><span class="sxs-lookup"><span data-stu-id="185fc-148">The output of the Python script is sent back into Pig.</span></span>

<span data-ttu-id="185fc-149">Python yorumlayıcı belirtmek için kullanın `register` Python betiğini başvururken.</span><span class="sxs-lookup"><span data-stu-id="185fc-149">To specify the Python interpreter, use `register` when referencing the Python script.</span></span> <span data-ttu-id="185fc-150">Aşağıdaki örnekler Pig betikleri kaydolmalı `myfuncs`:</span><span class="sxs-lookup"><span data-stu-id="185fc-150">The following examples register scripts with Pig as `myfuncs`:</span></span>

* <span data-ttu-id="185fc-151">**Jython kullanmak için**:`register '/path/to/pigudf.py' using jython as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="185fc-151">**To use Jython**: `register '/path/to/pigudf.py' using jython as myfuncs;`</span></span>
* <span data-ttu-id="185fc-152">**C Python kullanma**:`register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="185fc-152">**To use C Python**: `register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span></span>

> [!IMPORTANT]
> <span data-ttu-id="185fc-153">Jython kullanırken, bir yerel yol veya bir WASB pig_jython dosyasının yolu olabilir: / / yolu.</span><span class="sxs-lookup"><span data-stu-id="185fc-153">When using Jython, the path to the pig_jython file can be either a local path or a WASB:// path.</span></span> <span data-ttu-id="185fc-154">Ancak, C Python kullanırken, Pig işi göndermek için kullanmakta olduğunuz düğümünün yerel dosya sistemindeki bir dosyaya başvurmalıdır.</span><span class="sxs-lookup"><span data-stu-id="185fc-154">However, when using C Python, you must reference a file on the local file system of the node that you are using to submit the Pig job.</span></span>

<span data-ttu-id="185fc-155">Bir kez kayıt Bu örnek için Pig Latin her ikisi için de aynıdır:</span><span class="sxs-lookup"><span data-stu-id="185fc-155">Once past registration, the Pig Latin for this example is the same for both:</span></span>

```pig
LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
LOG = FILTER LOGS by LINE is not null;
DETAILS = FOREACH LOG GENERATE myfuncs.create_structure(LINE);
DUMP DETAILS;
```

<span data-ttu-id="185fc-156">Bu örnek yaptığı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="185fc-156">Here's what this example does:</span></span>

1. <span data-ttu-id="185fc-157">Örnek veri dosyası, ilk satırı yükler `sample.log` içine `LOGS`.</span><span class="sxs-lookup"><span data-stu-id="185fc-157">The first line loads the sample data file, `sample.log` into `LOGS`.</span></span> <span data-ttu-id="185fc-158">Ayrıca her kayıt olarak tanımlayan bir `chararray`.</span><span class="sxs-lookup"><span data-stu-id="185fc-158">It also defines each record as a `chararray`.</span></span>
2. <span data-ttu-id="185fc-159">Sonraki satıra işleminin sonucu depolamak herhangi bir null değeri filtreleyen `LOG`.</span><span class="sxs-lookup"><span data-stu-id="185fc-159">The next line filters out any null values, storing the result of the operation into `LOG`.</span></span>
3. <span data-ttu-id="185fc-160">Ardından, kayıtları üzerinden tekrarlanan `LOG` ve kullandığı `GENERATE` çağrılacak `create_structure` Python/Jython komut dosyasında yer alan yöntemi yüklü olarak `myfuncs`.</span><span class="sxs-lookup"><span data-stu-id="185fc-160">Next, it iterates over the records in `LOG` and uses `GENERATE` to invoke the `create_structure` method contained in the Python/Jython script loaded as `myfuncs`.</span></span> <span data-ttu-id="185fc-161">`LINE`Geçerli kayıt işleve geçirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="185fc-161">`LINE` is used to pass the current record to the function.</span></span>
4. <span data-ttu-id="185fc-162">Son olarak, çıkışları STDOUT atılır kullanarak `DUMP` komutu.</span><span class="sxs-lookup"><span data-stu-id="185fc-162">Finally, the outputs are dumped to STDOUT using the `DUMP` command.</span></span> <span data-ttu-id="185fc-163">İşlem tamamlandıktan sonra bu komutun sonuçlarını görüntüler.</span><span class="sxs-lookup"><span data-stu-id="185fc-163">This command displays the results after the operation completes.</span></span>

### <a name="create-the-pigudfpy-file"></a><span data-ttu-id="185fc-164">Pigudf.py dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="185fc-164">Create the pigudf.py file</span></span>

<span data-ttu-id="185fc-165">Geliştirme ortamınızı adlı bir metin dosyası oluşturun `pigudf.py`.</span><span class="sxs-lookup"><span data-stu-id="185fc-165">On your development environment, create a text file named `pigudf.py`.</span></span> <span data-ttu-id="185fc-166">Aşağıdaki kod dosyasının içeriği kullanın:</span><span class="sxs-lookup"><span data-stu-id="185fc-166">Use the following code as the contents of the file:</span></span>

<a name="streamingpy"></a>

```python
# Uncomment the following if using C Python
#from pig_util import outputSchema

@outputSchema("log: {(date:chararray, time:chararray, classname:chararray, level:chararray, detail:chararray)}")
def create_structure(input):
    if (input.startswith('java.lang.Exception')):
        input = input[21:len(input)] + ' - java.lang.Exception'
    date, time, classname, level, detail = input.split(' ', 4)
    return date, time, classname, level, detail
```

<span data-ttu-id="185fc-167">Biz Pig Latin örnekte tanımlanan `LINE` girişi için tutarlı bir şemayı olduğundan chararray girin.</span><span class="sxs-lookup"><span data-stu-id="185fc-167">In the Pig Latin example, we defined the `LINE` input as a chararray because there is no consistent schema for the input.</span></span> <span data-ttu-id="185fc-168">Python betiğini veri çıkışı için tutarlı bir şema dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="185fc-168">The Python script transforms the data into a consistent schema for output.</span></span>

1. <span data-ttu-id="185fc-169">`@outputSchema` Deyimi için Pig döndürülen verilerin biçimini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="185fc-169">The `@outputSchema` statement defines the format of the data that is returned to Pig.</span></span> <span data-ttu-id="185fc-170">Bu durumda olan bir **veri paketi**, Pig veri türü.</span><span class="sxs-lookup"><span data-stu-id="185fc-170">In this case, it's a **data bag**, which is a Pig data type.</span></span> <span data-ttu-id="185fc-171">Paketi chararray (dize) tümü aşağıdaki alanları içerir:</span><span class="sxs-lookup"><span data-stu-id="185fc-171">The bag contains the following fields, all of which are chararray (strings):</span></span>

   * <span data-ttu-id="185fc-172">tarih - günlük girişinin oluşturulduğu tarih</span><span class="sxs-lookup"><span data-stu-id="185fc-172">date - the date the log entry was created</span></span>
   * <span data-ttu-id="185fc-173">zaman - günlük girişinin oluşturulduğu zaman</span><span class="sxs-lookup"><span data-stu-id="185fc-173">time - the time the log entry was created</span></span>
   * <span data-ttu-id="185fc-174">ClassName - için sınıf adı girişi oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="185fc-174">classname - the class name the entry was created for</span></span>
   * <span data-ttu-id="185fc-175">Level - günlük düzeyini</span><span class="sxs-lookup"><span data-stu-id="185fc-175">level - the log level</span></span>
   * <span data-ttu-id="185fc-176">Ayrıntı - günlük girişi için ayrıntılı ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="185fc-176">detail - verbose details for the log entry</span></span>

2. <span data-ttu-id="185fc-177">Ardından, `def create_structure(input)` Pig çizgi öğelerine geçirir işlevi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="185fc-177">Next, the `def create_structure(input)` defines the function that Pig passes line items to.</span></span>

3. <span data-ttu-id="185fc-178">Örnek veri `sample.log`, çoğunlukla tarih, saat, classname düzeyi, uyumlu ve ayrıntı istiyoruz döndürmek için şema.</span><span class="sxs-lookup"><span data-stu-id="185fc-178">The example data, `sample.log`, mostly conforms to the date, time, classname, level, and detail schema we want to return.</span></span> <span data-ttu-id="185fc-179">Ancak, ile başlayan birkaç satırları içeren `*java.lang.Exception*`.</span><span class="sxs-lookup"><span data-stu-id="185fc-179">However, it contains a few lines that begin with `*java.lang.Exception*`.</span></span> <span data-ttu-id="185fc-180">Bu satırlar şemayla eşleşecek şekilde değiştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="185fc-180">These lines must be modified to match the schema.</span></span> <span data-ttu-id="185fc-181">`if` Deyimi için olanlar denetler ve ardından taşımak için giriş verileri massages `*java.lang.Exception*` veri satır içi bizim beklenen çıkış şemasıyla getiren sonuna dize.</span><span class="sxs-lookup"><span data-stu-id="185fc-181">The `if` statement checks for those, then massages the input data to move the `*java.lang.Exception*` string to the end, bringing the data in-line with our expected output schema.</span></span>

4. <span data-ttu-id="185fc-182">Ardından, `split` komutu ilk dört boşluk karakterleri veri bölmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="185fc-182">Next, the `split` command is used to split the data at the first four space characters.</span></span> <span data-ttu-id="185fc-183">Çıktı içine atanan `date`, `time`, `classname`, `level`, ve `detail`.</span><span class="sxs-lookup"><span data-stu-id="185fc-183">The output is assigned into `date`, `time`, `classname`, `level`, and `detail`.</span></span>

5. <span data-ttu-id="185fc-184">Son olarak, değerleri için Pig döndürülür.</span><span class="sxs-lookup"><span data-stu-id="185fc-184">Finally, the values are returned to Pig.</span></span>

<span data-ttu-id="185fc-185">Verileri için Pig döndürüldüğünde, tutarlı bir şema tanımlandığı şekilde sahip `@outputSchema` deyimi.</span><span class="sxs-lookup"><span data-stu-id="185fc-185">When the data is returned to Pig, it has a consistent schema as defined in the `@outputSchema` statement.</span></span>

## <span data-ttu-id="185fc-186"><a name="running"></a>Karşıya yükleme ve örnekler çalıştırın</span><span class="sxs-lookup"><span data-stu-id="185fc-186"><a name="running"></a>Upload and run the examples</span></span>

> [!IMPORTANT]
> <span data-ttu-id="185fc-187">**SSH** adımlar, yalnızca Linux tabanlı Hdınsight kümesi ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="185fc-187">The **SSH** steps only work with a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="185fc-188">**PowerShell** adımları bir Linux veya Windows tabanlı Hdınsight kümesi ile çalışır, ancak bir Windows istemci gerektirir.</span><span class="sxs-lookup"><span data-stu-id="185fc-188">The **PowerShell** steps work with either a Linux or Windows-based HDInsight cluster, but require a Windows client.</span></span>

### <a name="ssh"></a><span data-ttu-id="185fc-189">SSH</span><span class="sxs-lookup"><span data-stu-id="185fc-189">SSH</span></span>

<span data-ttu-id="185fc-190">SSH kullanma hakkında daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="185fc-190">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="185fc-191">Kullanım `scp` dosyaları Hdınsight kümenize kopyalamak için.</span><span class="sxs-lookup"><span data-stu-id="185fc-191">Use `scp` to copy the files to your HDInsight cluster.</span></span> <span data-ttu-id="185fc-192">Örneğin, aşağıdaki komut dosyaları adlı bir kümeye kopyalar **mycluster**.</span><span class="sxs-lookup"><span data-stu-id="185fc-192">For example, the following command copies the files to a cluster named **mycluster**.</span></span>

    ```bash
    scp hiveudf.py pigudf.py myuser@mycluster-ssh.azurehdinsight.net:
    ```

2. <span data-ttu-id="185fc-193">Kümeye bağlanmak için SSH kullanın.</span><span class="sxs-lookup"><span data-stu-id="185fc-193">Use SSH to connect to the cluster.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="185fc-194">SSH oturumundan WASB depolama küme için daha önce karşıya python dosyalarını ekleyin.</span><span class="sxs-lookup"><span data-stu-id="185fc-194">From the SSH session, add the python files uploaded previously to the WASB storage for the cluster.</span></span>

    ```bash
    hdfs dfs -put hiveudf.py /hiveudf.py
    hdfs dfs -put pigudf.py /pigudf.py
    ```

<span data-ttu-id="185fc-195">Dosyaları karşıya yükleme sonrasında, Hive veya Pig işlerini çalıştırmak için aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="185fc-195">After uploading the files, use the following steps to run the Hive and Pig jobs.</span></span>

#### <a name="use-the-hive-udf"></a><span data-ttu-id="185fc-196">UDF Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="185fc-196">Use the Hive UDF</span></span>

1. <span data-ttu-id="185fc-197">Kullanım `hive` hive kabuğunu başlatmak için komutu.</span><span class="sxs-lookup"><span data-stu-id="185fc-197">Use the `hive` command to start the hive shell.</span></span> <span data-ttu-id="185fc-198">Görmeniz gerekir bir `hive>` Kabuk yüklendikten sonra ister.</span><span class="sxs-lookup"><span data-stu-id="185fc-198">You should see a `hive>` prompt once the shell has loaded.</span></span>

2. <span data-ttu-id="185fc-199">Aşağıdaki sorgu girin `hive>` istemi:</span><span class="sxs-lookup"><span data-stu-id="185fc-199">Enter the following query at the `hive>` prompt:</span></span>

   ```hive
   add file wasb:///hiveudf.py;
   SELECT TRANSFORM (clientid, devicemake, devicemodel)
       USING 'python hiveudf.py' AS
       (clientid string, phoneLabel string, phoneHash string)
   FROM hivesampletable
   ORDER BY clientid LIMIT 50;
   ```

3. <span data-ttu-id="185fc-200">Son satırı girdikten sonra iş başlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="185fc-200">After entering the last line, the job should start.</span></span> <span data-ttu-id="185fc-201">İş tamamlandığında, çıkış aşağıdaki örneğe benzer şekilde döndürür:</span><span class="sxs-lookup"><span data-stu-id="185fc-201">Once the job completes, it returns output similar to the following example:</span></span>

        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="use-the-pig-udf"></a><span data-ttu-id="185fc-202">UDF Pig kullanma</span><span class="sxs-lookup"><span data-stu-id="185fc-202">Use the Pig UDF</span></span>

1. <span data-ttu-id="185fc-203">Kullanım `pig` komut kabuğu'nu başlatın.</span><span class="sxs-lookup"><span data-stu-id="185fc-203">Use the `pig` command to start the shell.</span></span> <span data-ttu-id="185fc-204">Gördüğünüz bir `grunt>` Kabuk yüklendikten sonra ister.</span><span class="sxs-lookup"><span data-stu-id="185fc-204">You see a `grunt>` prompt once the shell has loaded.</span></span>

2. <span data-ttu-id="185fc-205">Aşağıdaki deyimler de girin `grunt>` istemi:</span><span class="sxs-lookup"><span data-stu-id="185fc-205">Enter the following statements at the `grunt>` prompt:</span></span>

   ```pig
   Register wasb:///pigudf.py using jython as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

3. <span data-ttu-id="185fc-206">Aşağıdaki satırı girdikten sonra iş başlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="185fc-206">After entering the following line, the job should start.</span></span> <span data-ttu-id="185fc-207">İş tamamlandığında, çıkış benzer aşağıdaki veriler döndürür:</span><span class="sxs-lookup"><span data-stu-id="185fc-207">Once the job completes, it returns output similar to the following data:</span></span>

        ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
        ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
        ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
        ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
        ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

4. <span data-ttu-id="185fc-208">Kullanmak `quit` Grunt Kabuk çıkın ve ardından yerel dosya sisteminde pigudf.py dosyayı düzenlemek için aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="185fc-208">Use `quit` to exit the Grunt shell, and then use the following to edit the pigudf.py file on the local file system:</span></span>

    ```bash
    nano pigudf.py
    ```

5. <span data-ttu-id="185fc-209">Bir kez Düzenleyicisi'nde aşağıdaki satırı kaldırarak açıklamadan çıkarın `#` karakter satırını başından itibaren:</span><span class="sxs-lookup"><span data-stu-id="185fc-209">Once in the editor, uncomment the following line by removing the `#` character from the beginning of the line:</span></span>

    ```bash
    #from pig_util import outputSchema
    ```

    <span data-ttu-id="185fc-210">Değişikliği yaptıktan sonra düzenleyiciden çıkmak için Ctrl + X kullanın.</span><span class="sxs-lookup"><span data-stu-id="185fc-210">Once the change has been made, use Ctrl+X to exit the editor.</span></span> <span data-ttu-id="185fc-211">Y seçin ve ardından değişiklikleri kaydetmek için girin.</span><span class="sxs-lookup"><span data-stu-id="185fc-211">Select Y, and then enter to save the changes.</span></span>

6. <span data-ttu-id="185fc-212">Kullanım `pig` Kabuğu'nu yeniden başlatmak için komutu.</span><span class="sxs-lookup"><span data-stu-id="185fc-212">Use the `pig` command to start the shell again.</span></span> <span data-ttu-id="185fc-213">Konumundaki olduğunuzda `grunt>` isteminde, aşağıdaki C Python yorumlayıcı kullanarak Python komut dosyasını çalıştırmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="185fc-213">Once you are at the `grunt>` prompt, use the following to run the Python script using the C Python interpreter.</span></span>

   ```pig
   Register 'pigudf.py' using streaming_python as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

    <span data-ttu-id="185fc-214">Bu iş tamamlandığında, ne zaman önceden Jython kullanarak betiği çalıştırdığınız aynı çıktı görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="185fc-214">Once this job completes, you should see the same output as when you previously ran the script using Jython.</span></span>

### <a name="powershell-upload-the-files"></a><span data-ttu-id="185fc-215">PowerShell: dosyaları karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="185fc-215">PowerShell: Upload the files</span></span>

<span data-ttu-id="185fc-216">Hdınsight sunucusuna dosyaları karşıya yükleme için PowerShell kullanın.</span><span class="sxs-lookup"><span data-stu-id="185fc-216">You can use PowerShell to upload the files to the HDInsight server.</span></span> <span data-ttu-id="185fc-217">Python dosyaları karşıya yüklemek için aşağıdaki komut dosyasını kullanın:</span><span class="sxs-lookup"><span data-stu-id="185fc-217">Use the following script to upload the Python files:</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="185fc-218">Bu bölümdeki adımları Azure PowerShell kullanın.</span><span class="sxs-lookup"><span data-stu-id="185fc-218">The steps in this section use Azure PowerShell.</span></span> <span data-ttu-id="185fc-219">Azure PowerShell kullanma hakkında daha fazla bilgi için bkz: [Azure PowerShell'i yükleme ve yapılandırma nasıl](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="185fc-219">For more information on using Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

```powershell
# Login to your Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
# Change the path to match the file location on your system
$pathToStreamingFile = "C:\path\to\hiveudf.py"
$pathToJythonFile = "C:\path\to\pigudf.py"

$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName=$clusterInfo.DefaultStorageAccount.split('.')[0]
$container=$clusterInfo.DefaultStorageContainer
$storageAccountKey=(Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage content and upload the file
$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey $storageAccountKey

Set-AzureStorageBlobContent `
    -File $pathToStreamingFile `
    -Blob "hiveudf.py" `
    -Container $container `
    -Context $context

Set-AzureStorageBlobContent `
    -File $pathToJythonFile `
    -Blob "pigudf.py" `
    -Container $container `
    -Context $context
```
> [!IMPORTANT]
> <span data-ttu-id="185fc-220">Değişiklik `C:\path\to` geliştirme ortamınızı dosyalarda yoluna değeri.</span><span class="sxs-lookup"><span data-stu-id="185fc-220">Change the `C:\path\to` value to the path to the files on your development environment.</span></span>

<span data-ttu-id="185fc-221">Bu komut dosyası Hdınsight kümenizle ilgili bilgileri alır sonra varsayılan depolama hesabı için anahtar ve hesap ayıklar ve kapsayıcı kök dizinine dosyaları yükler.</span><span class="sxs-lookup"><span data-stu-id="185fc-221">This script retrieves information for your HDInsight cluster, then extracts the account and key for the default storage account, and uploads the files to the root of the container.</span></span>

> [!NOTE]
> <span data-ttu-id="185fc-222">Dosyaları karşıya yükleme ile ilgili daha fazla bilgi için bkz: [hdınsight'ta Hadoop işleri için verileri karşıya yükleme](hdinsight-upload-data.md) belge.</span><span class="sxs-lookup"><span data-stu-id="185fc-222">For more information on uploading files, see the [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md) document.</span></span>

#### <a name="powershell-use-the-hive-udf"></a><span data-ttu-id="185fc-223">PowerShell: UDF Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="185fc-223">PowerShell: Use the Hive UDF</span></span>

<span data-ttu-id="185fc-224">PowerShell uzaktan Hive sorguları çalıştırmak için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="185fc-224">PowerShell can also be used to remotely run Hive queries.</span></span> <span data-ttu-id="185fc-225">Kullanan bir Hive sorgusu çalıştırmak için aşağıdaki PowerShell betiğini kullanın **hiveudf.py** komut dosyası:</span><span class="sxs-lookup"><span data-stu-id="185fc-225">Use the following PowerShell script to run a Hive query that uses **hiveudf.py** script:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="185fc-226">Çalıştırmadan önce komut dosyası, Hdınsight kümeniz için HTTPs/Admin hesap bilgilerini ister.</span><span class="sxs-lookup"><span data-stu-id="185fc-226">Before running, the script prompts you for the HTTPs/Admin account information for your HDInsight cluster.</span></span>

```powershell
# Login to your Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
$creds=Get-Credential -Message "Enter the login for the cluster"

# If using a Windows-based HDInsight cluster, change the USING statement to:
# "USING 'D:\Python27\python.exe hiveudf.py' AS " +
$HiveQuery = "add file wasb:///hiveudf.py;" +
                "SELECT TRANSFORM (clientid, devicemake, devicemodel) " +
                "USING 'python hiveudf.py' AS " +
                "(clientid string, phoneLabel string, phoneHash string) " +
                "FROM hivesampletable " +
                "ORDER BY clientid LIMIT 50;"

$jobDefinition = New-AzureRmHDInsightHiveJobDefinition `
    -Query $HiveQuery

$job = Start-AzureRmHDInsightJob `
    -ClusterName $clusterName `
    -JobDefinition $jobDefinition `
    -HttpCredential $creds
Write-Host "Wait for the Hive job to complete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -JobId $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment the following to see stderr output
# Get-AzureRmHDInsightJobOutput `
#   -Clustername $clusterName `
#   -JobId $job.JobId `
#   -HttpCredential $creds `
#   -DisplayOutputType StandardError
Write-Host "Display the standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

<span data-ttu-id="185fc-227">Çıkış için **Hive** işi aşağıdaki örneğe benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="185fc-227">The output for the **Hive** job should appear similar to the following example:</span></span>

    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="pig-jython"></a><span data-ttu-id="185fc-228">Pig (Jython)</span><span class="sxs-lookup"><span data-stu-id="185fc-228">Pig (Jython)</span></span>

<span data-ttu-id="185fc-229">PowerShell, Pig Latin işlerini çalıştırmak için de kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="185fc-229">PowerShell can also be used to run Pig Latin jobs.</span></span> <span data-ttu-id="185fc-230">Kullanan bir Pig Latin işini çalıştırmak için **pigudf.py** komut dosyası, aşağıdaki PowerShell betiğini kullanın:</span><span class="sxs-lookup"><span data-stu-id="185fc-230">To run a Pig Latin job that uses the **pigudf.py** script, use the following PowerShell script:</span></span>

> [!NOTE]
> <span data-ttu-id="185fc-231">Uzaktan PowerShell kullanarak işi gönderirken C Python yorumlayıcı kullanmak mümkün değil.</span><span class="sxs-lookup"><span data-stu-id="185fc-231">When remotely submitting a job using PowerShell, it is not possible to use C Python as the interpreter.</span></span>

```powershell
# Login to your Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
$creds=Get-Credential -Message "Enter the login for the cluster"

$PigQuery = "Register wasb:///pigudf.py using jython as myfuncs;" +
            "LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);" +
            "LOG = FILTER LOGS by LINE is not null;" +
            "DETAILS = foreach LOG generate myfuncs.create_structure(LINE);" +
            "DUMP DETAILS;"

$jobDefinition = New-AzureRmHDInsightPigJobDefinition -Query $PigQuery

$job = Start-AzureRmHDInsightJob `
    -ClusterName $clusterName `
    -JobDefinition $jobDefinition `
    -HttpCredential $creds

Write-Host "Wait for the Pig job to complete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -Job $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment the following to see stderr output
# Get-AzureRmHDInsightJobOutput `
#    -Clustername $clusterName `
#    -JobId $job.JobId `
#    -HttpCredential $creds `
#    -DisplayOutputType StandardError
Write-Host "Display the standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

<span data-ttu-id="185fc-232">Çıkış için **Pig** işi aşağıdaki veri benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="185fc-232">The output for the **Pig** job should appear similar to the following data:</span></span>

    ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
    ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
    ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
    ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
    ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

## <span data-ttu-id="185fc-233"><a name="troubleshooting"></a>Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="185fc-233"><a name="troubleshooting"></a>Troubleshooting</span></span>

### <a name="errors-when-running-jobs"></a><span data-ttu-id="185fc-234">İşlerini çalışırken hataları</span><span class="sxs-lookup"><span data-stu-id="185fc-234">Errors when running jobs</span></span>

<span data-ttu-id="185fc-235">Hive işi çalıştırırken, aşağıdakine benzer bir hata karşılaşabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="185fc-235">When running the hive job, you may encounter an error similar to the following text:</span></span>

    Caused by: org.apache.hadoop.hive.ql.metadata.HiveException: [Error 20001]: An error occurred while reading or writing to your custom script. It may have crashed with an error.

<span data-ttu-id="185fc-236">Bu sorunun nedeni Python dosyasındaki satır sonları.</span><span class="sxs-lookup"><span data-stu-id="185fc-236">This problem may be caused by the line endings in the Python file.</span></span> <span data-ttu-id="185fc-237">CRLF satır bitiş ancak Linux uygulamaları olarak genellikle birçok Windows düzenleyicileri varsayılan olarak LF bekler.</span><span class="sxs-lookup"><span data-stu-id="185fc-237">Many Windows editors default to using CRLF as the line ending, but Linux applications usually expect LF.</span></span>

<span data-ttu-id="185fc-238">Hdınsight için dosyayı karşıya yüklemeden önce CR karakterleri kaldırmak için aşağıdaki PowerShell ifadeleri kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="185fc-238">You can use the following PowerShell statements to remove the CR characters before uploading the file to HDInsight:</span></span>

```powershell
$original_file ='c:\path\to\hiveudf.py'
$text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
[IO.File]::WriteAllText($original_file, $text)
```

### <a name="powershell-scripts"></a><span data-ttu-id="185fc-239">PowerShell komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="185fc-239">PowerShell scripts</span></span>

<span data-ttu-id="185fc-240">Örnekleri çalıştırmak için kullanılan örnek PowerShell komut dosyalarının her ikisi de işi için hata çıktısını görüntüler açıklamalı bir satır içerir.</span><span class="sxs-lookup"><span data-stu-id="185fc-240">Both of the example PowerShell scripts used to run the examples contain a commented line that displays error output for the job.</span></span> <span data-ttu-id="185fc-241">İş için beklenen çıktı görmüyorsanız, aşağıdaki satırı açıklamadan çıkarın ve hata bilgilerini ilgili bir sorunu gösterir, bkz.</span><span class="sxs-lookup"><span data-stu-id="185fc-241">If you are not seeing the expected output for the job, uncomment the following line and see if the error information indicates a problem.</span></span>

```powershell
# Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="185fc-242">Ayrıca hata bilgilerini (STDERR) ve (STDOUT) iş sonucunu Hdınsight depolama alanınızın günlüğe kaydedilir.</span><span class="sxs-lookup"><span data-stu-id="185fc-242">The error information (STDERR) and the result of the job (STDOUT) are also logged to your HDInsight storage.</span></span>

| <span data-ttu-id="185fc-243">Bu iş için...</span><span class="sxs-lookup"><span data-stu-id="185fc-243">For this job...</span></span> | <span data-ttu-id="185fc-244">Bu dosyalar blob kapsayıcısında bakın</span><span class="sxs-lookup"><span data-stu-id="185fc-244">Look at these files in the blob container</span></span> |
| --- | --- |
| <span data-ttu-id="185fc-245">Hive</span><span class="sxs-lookup"><span data-stu-id="185fc-245">Hive</span></span> |<span data-ttu-id="185fc-246">/ HivePython/stderr</span><span class="sxs-lookup"><span data-stu-id="185fc-246">/HivePython/stderr</span></span><p><span data-ttu-id="185fc-247">/ HivePython/stdout</span><span class="sxs-lookup"><span data-stu-id="185fc-247">/HivePython/stdout</span></span> |
| <span data-ttu-id="185fc-248">Pig</span><span class="sxs-lookup"><span data-stu-id="185fc-248">Pig</span></span> |<span data-ttu-id="185fc-249">/ PigPython/stderr</span><span class="sxs-lookup"><span data-stu-id="185fc-249">/PigPython/stderr</span></span><p><span data-ttu-id="185fc-250">/ PigPython/stdout</span><span class="sxs-lookup"><span data-stu-id="185fc-250">/PigPython/stdout</span></span> |

## <span data-ttu-id="185fc-251"><a name="next"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="185fc-251"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="185fc-252">Varsayılan olarak sağlanmayan Python modüllerini yüklemek gerekirse bkz [bir modül Azure Hdınsight dağıtma](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span><span class="sxs-lookup"><span data-stu-id="185fc-252">If you need to load Python modules that aren't provided by default, see [How to deploy a module to Azure HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span></span>

<span data-ttu-id="185fc-253">Diğer yolları için Pig, Hive ve MapReduce kullanma hakkında bilgi edinmek için aşağıdaki belgelere bakın:</span><span class="sxs-lookup"><span data-stu-id="185fc-253">For other ways to use Pig, Hive, and to learn about using MapReduce, see the following documents:</span></span>

* [<span data-ttu-id="185fc-254">HDInsight ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="185fc-254">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="185fc-255">HDInsight ile Pig kullanma</span><span class="sxs-lookup"><span data-stu-id="185fc-255">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="185fc-256">Hdınsight ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="185fc-256">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
