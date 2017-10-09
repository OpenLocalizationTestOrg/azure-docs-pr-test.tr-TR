---
title: "Apache Hive veya Pig - Azure Hdınsight ile UDF aaaPython | Microsoft Docs"
description: "Azure üzerinde toouse Python kullanıcı tanımlı işlevler (UDF) Hive ve hdınsight'ta Hadoop teknoloji hello Pig yığın nasıl öğrenin."
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
ms.openlocfilehash: 26d8160cc6ed7fc22c3f06f7c1c9954c224b2366
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-python-user-defined-functions-udf-with-hive-and-pig-in-hdinsight"></a><span data-ttu-id="de75c-103">Hdınsight'ta kullanım Python kullanıcı tanımlı işlevler (UDF) Hive veya Pig ile</span><span class="sxs-lookup"><span data-stu-id="de75c-103">Use Python User Defined Functions (UDF) with Hive and Pig in HDInsight</span></span>

<span data-ttu-id="de75c-104">Bilgi nasıl toouse Python kullanıcı tanımlı işlevler (UDF) Apache Hive veya Pig içinde Azure hdınsight'ta Hadoop ile.</span><span class="sxs-lookup"><span data-stu-id="de75c-104">Learn how toouse Python user-defined functions (UDF) with Apache Hive and Pig in Hadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="de75c-105"><a name="python"></a>Hdınsight üzerinde Python</span><span class="sxs-lookup"><span data-stu-id="de75c-105"><a name="python"></a>Python on HDInsight</span></span>

<span data-ttu-id="de75c-106">Python2.7 Hdınsight 3.0 ve sonraki sürümlerinde varsayılan olarak yüklenir.</span><span class="sxs-lookup"><span data-stu-id="de75c-106">Python2.7 is installed by default on HDInsight 3.0 and later.</span></span> <span data-ttu-id="de75c-107">Apache Hive Python bu sürümü ile akış işleme için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="de75c-107">Apache Hive can be used with this version of Python for stream processing.</span></span> <span data-ttu-id="de75c-108">Akış işleme Hive ve hello UDF arasında STDOUT ve STDIN toopass verileri kullanır.</span><span class="sxs-lookup"><span data-stu-id="de75c-108">Stream processing uses STDOUT and STDIN toopass data between Hive and hello UDF.</span></span>

<span data-ttu-id="de75c-109">Hdınsight, ayrıca Java'da yazılmış bir Python uygulaması Jython içerir.</span><span class="sxs-lookup"><span data-stu-id="de75c-109">HDInsight also includes Jython, which is a Python implementation written in Java.</span></span> <span data-ttu-id="de75c-110">Jython doğrudan hello Java sanal makinesi'üzerinde çalışır ve akış kullanmaz.</span><span class="sxs-lookup"><span data-stu-id="de75c-110">Jython runs directly on hello Java Virtual Machine and does not use streaming.</span></span> <span data-ttu-id="de75c-111">Jython hello Python yorumlayıcı Python ile Pig kullanırken önerilen ' dir.</span><span class="sxs-lookup"><span data-stu-id="de75c-111">Jython is hello recommended Python interpreter when using Python with Pig.</span></span>

> [!WARNING]
> <span data-ttu-id="de75c-112">Bu belgedeki Hello adımlar varsayımlar aşağıdaki hello olun:</span><span class="sxs-lookup"><span data-stu-id="de75c-112">hello steps in this document make hello following assumptions:</span></span> 
>
> * <span data-ttu-id="de75c-113">Merhaba yerel geliştirme ortamınızı Python komut dosyaları oluşturun.</span><span class="sxs-lookup"><span data-stu-id="de75c-113">You create hello Python scripts on your local development environment.</span></span>
> * <span data-ttu-id="de75c-114">Merhaba betikleri tooHDInsight ya da hello kullanarak karşıya `scp` yerel Bash oturumu veya PowerShell komut dosyası sağlanan hello komutu.</span><span class="sxs-lookup"><span data-stu-id="de75c-114">You upload hello scripts tooHDInsight using either hello `scp` command from a local Bash session or hello provided PowerShell script.</span></span>
>
> <span data-ttu-id="de75c-115">Toouse hello istiyorsanız [Azure bulut Kabuğu (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) gerekir sonra Hdınsight ile toowork önizleme:</span><span class="sxs-lookup"><span data-stu-id="de75c-115">If you want toouse hello [Azure Cloud Shell (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) preview toowork with HDInsight, then you must:</span></span>
>
> * <span data-ttu-id="de75c-116">Merhaba bulut Kabuk ortamı içindeki Hello betikleri oluşturun.</span><span class="sxs-lookup"><span data-stu-id="de75c-116">Create hello scripts inside hello cloud shell environment.</span></span>
> * <span data-ttu-id="de75c-117">Kullanım `scp` tooupload hello hello dosyalarından Kabuk tooHDInsight bulut.</span><span class="sxs-lookup"><span data-stu-id="de75c-117">Use `scp` tooupload hello files from hello cloud shell tooHDInsight.</span></span>
> * <span data-ttu-id="de75c-118">Kullanım `ssh` hello bulut Kabuk tooconnect tooHDInsight ve çalışma hello örnekleri.</span><span class="sxs-lookup"><span data-stu-id="de75c-118">Use `ssh` from hello cloud shell tooconnect tooHDInsight and run hello examples.</span></span>

## <span data-ttu-id="de75c-119"><a name="hivepython"></a>UDF yığını</span><span class="sxs-lookup"><span data-stu-id="de75c-119"><a name="hivepython"></a>Hive UDF</span></span>

<span data-ttu-id="de75c-120">Python olarak kullanılabilir bir UDF Hive gelen HiveQL hello `TRANSFORM` deyimi.</span><span class="sxs-lookup"><span data-stu-id="de75c-120">Python can be used as a UDF from Hive through hello HiveQL `TRANSFORM` statement.</span></span> <span data-ttu-id="de75c-121">Örneğin, aşağıdaki HiveQL hello hello çağırır `hiveudf.py` hello kümesi için hello varsayılan Azure depolama hesabına depolanan dosya.</span><span class="sxs-lookup"><span data-stu-id="de75c-121">For example, hello following HiveQL invokes hello `hiveudf.py` file stored in hello default Azure Storage account for hello cluster.</span></span>

<span data-ttu-id="de75c-122">**Linux tabanlı Hdınsight**</span><span class="sxs-lookup"><span data-stu-id="de75c-122">**Linux-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'python hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

<span data-ttu-id="de75c-123">**Windows tabanlı Hdınsight**</span><span class="sxs-lookup"><span data-stu-id="de75c-123">**Windows-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'D:\Python27\python.exe hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

> [!NOTE]
> <span data-ttu-id="de75c-124">Windows tabanlı Hdınsight kümelerinde hello `USING` yan tümcesi hello tam yolu toopython.exe belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="de75c-124">On Windows-based HDInsight clusters, hello `USING` clause must specify hello full path toopython.exe.</span></span>

<span data-ttu-id="de75c-125">Bu örnek yaptığı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="de75c-125">Here's what this example does:</span></span>

1. <span data-ttu-id="de75c-126">Merhaba `add file` hello dosya hello başında deyiminin ekler hello `hiveudf.py` dosya toohello hello kümedeki tüm düğümler tarafından erişilebilir olması için önbellek, dağıtılmış.</span><span class="sxs-lookup"><span data-stu-id="de75c-126">hello `add file` statement at hello beginning of hello file adds hello `hiveudf.py` file toohello distributed cache, so it's accessible by all nodes in hello cluster.</span></span>
2. <span data-ttu-id="de75c-127">Merhaba `SELECT TRANSFORM ... USING` deyimi hello veri seçer `hivesampletable`.</span><span class="sxs-lookup"><span data-stu-id="de75c-127">hello `SELECT TRANSFORM ... USING` statement selects data from hello `hivesampletable`.</span></span> <span data-ttu-id="de75c-128">Merhaba ClientID, devicemake ve devicemodel değerleri toohello de geçirir `hiveudf.py` komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="de75c-128">It also passes hello clientid, devicemake, and devicemodel values toohello `hiveudf.py` script.</span></span>
3. <span data-ttu-id="de75c-129">Merhaba `AS` yan tümcesi açıklar döndürülen hello alanları `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="de75c-129">hello `AS` clause describes hello fields returned from `hiveudf.py`.</span></span>

<a name="streamingpy"></a>

### <a name="create-hello-hiveudfpy-file"></a><span data-ttu-id="de75c-130">Merhaba hiveudf.py dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="de75c-130">Create hello hiveudf.py file</span></span>


<span data-ttu-id="de75c-131">Geliştirme ortamınızı adlı bir metin dosyası oluşturun `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="de75c-131">On your development environment, create a text file named `hiveudf.py`.</span></span> <span data-ttu-id="de75c-132">Merhaba dosyasının Merhaba içeriğine koddan hello kullan:</span><span class="sxs-lookup"><span data-stu-id="de75c-132">Use hello following code as hello contents of hello file:</span></span>

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

<span data-ttu-id="de75c-133">Bu komut dosyası hello aşağıdaki eylemleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="de75c-133">This script performs hello following actions:</span></span>

1. <span data-ttu-id="de75c-134">Veri satırı STDIN okuyun.</span><span class="sxs-lookup"><span data-stu-id="de75c-134">Read a line of data from STDIN.</span></span>
2. <span data-ttu-id="de75c-135">Yeni satır karakteri sondaki hello kullanarak kaldırılır `string.strip(line, "\n ")`.</span><span class="sxs-lookup"><span data-stu-id="de75c-135">hello trailing newline character is removed using `string.strip(line, "\n ")`.</span></span>
3. <span data-ttu-id="de75c-136">Akış işleme yaparken, tek bir satırı her değer arasında bir sekme karakteri ile tüm hello değerlerini içerir.</span><span class="sxs-lookup"><span data-stu-id="de75c-136">When doing stream processing, a single line contains all hello values with a tab character between each value.</span></span> <span data-ttu-id="de75c-137">Bu nedenle `string.split(line, "\t")` giriş yalnızca hello alanları dönmeden her sekmesi sırasında kullanılan toosplit hello olabilir.</span><span class="sxs-lookup"><span data-stu-id="de75c-137">So `string.split(line, "\t")` can be used toosplit hello input at each tab, returning just hello fields.</span></span>
4. <span data-ttu-id="de75c-138">İşlem tamamlandığında, hello çıktı sekmesi her alanı arasında tek bir satır olarak tooSTDOUT yazılmış olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="de75c-138">When processing is complete, hello output must be written tooSTDOUT as a single line, with a tab between each field.</span></span> <span data-ttu-id="de75c-139">Örneğin, `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span><span class="sxs-lookup"><span data-stu-id="de75c-139">For example, `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span></span>
5. <span data-ttu-id="de75c-140">Merhaba `while` döngü Hayır kadar yinelenir `line` okunur.</span><span class="sxs-lookup"><span data-stu-id="de75c-140">hello `while` loop repeats until no `line` is read.</span></span>

<span data-ttu-id="de75c-141">Merhaba komut çıktısı şöyledir hello giriş değerleri için bir birleşimini `devicemake` ve `devicemodel`, ve hello karmasını birleştirilmiş değer.</span><span class="sxs-lookup"><span data-stu-id="de75c-141">hello script output is a concatenation of hello input values for `devicemake` and `devicemodel`, and a hash of hello concatenated value.</span></span>

<span data-ttu-id="de75c-142">Bkz: [hello örnekleri çalıştırma](#running) nasıl toorun Hdınsight kümenizdeki Bu örnek.</span><span class="sxs-lookup"><span data-stu-id="de75c-142">See [Running hello examples](#running) for how toorun this example on your HDInsight cluster.</span></span>

## <span data-ttu-id="de75c-143"><a name="pigpython"></a>Pig UDF</span><span class="sxs-lookup"><span data-stu-id="de75c-143"><a name="pigpython"></a>Pig UDF</span></span>

<span data-ttu-id="de75c-144">Bir Python komut dosyası olarak bir UDF Pig gelen hello kullanılabilir `GENERATE` deyimi.</span><span class="sxs-lookup"><span data-stu-id="de75c-144">A Python script can be used as a UDF from Pig through hello `GENERATE` statement.</span></span> <span data-ttu-id="de75c-145">Jython veya C Python kullanarak hello komut dosyası çalıştırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de75c-145">You can run hello script using either Jython or C Python.</span></span>

* <span data-ttu-id="de75c-146">Jython JVM hello üzerinde çalışır ve yerel olarak Pig çağrılabilir.</span><span class="sxs-lookup"><span data-stu-id="de75c-146">Jython runs on hello JVM, and can natively be called from Pig.</span></span>
* <span data-ttu-id="de75c-147">C Python bir dış işlem olduğundan, Pig Hello verileri hello üzerinde bir Python işlemde çalışan toohello betik çıkışı JVM gönderilir.</span><span class="sxs-lookup"><span data-stu-id="de75c-147">C Python is an external process, so hello data from Pig on hello JVM is sent out toohello script running in a Python process.</span></span> <span data-ttu-id="de75c-148">Merhaba hello Python komut dosyası çıkışını Pig'ya geri gönderilir.</span><span class="sxs-lookup"><span data-stu-id="de75c-148">hello output of hello Python script is sent back into Pig.</span></span>

<span data-ttu-id="de75c-149">toospecify hello Python Yorumlayıcı, kullanım `register` hello Python betiği başvururken.</span><span class="sxs-lookup"><span data-stu-id="de75c-149">toospecify hello Python interpreter, use `register` when referencing hello Python script.</span></span> <span data-ttu-id="de75c-150">Merhaba Aşağıdaki örnekler komut dosyaları ile Pig kaydetmeye `myfuncs`:</span><span class="sxs-lookup"><span data-stu-id="de75c-150">hello following examples register scripts with Pig as `myfuncs`:</span></span>

* <span data-ttu-id="de75c-151">**toouse Jython**:`register '/path/to/pigudf.py' using jython as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="de75c-151">**toouse Jython**: `register '/path/to/pigudf.py' using jython as myfuncs;`</span></span>
* <span data-ttu-id="de75c-152">**toouse C Python**:`register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="de75c-152">**toouse C Python**: `register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span></span>

> [!IMPORTANT]
> <span data-ttu-id="de75c-153">Jython kullanırken hello yol toohello pig_jython dosya yerel bir yol ya da bir WASB olabilir: / / yolu.</span><span class="sxs-lookup"><span data-stu-id="de75c-153">When using Jython, hello path toohello pig_jython file can be either a local path or a WASB:// path.</span></span> <span data-ttu-id="de75c-154">Ancak, C Python kullanırken, bir dosya toosubmit hello Pig işi kullandığınız hello düğümünün hello yerel dosya sisteminde başvurmalıdır.</span><span class="sxs-lookup"><span data-stu-id="de75c-154">However, when using C Python, you must reference a file on hello local file system of hello node that you are using toosubmit hello Pig job.</span></span>

<span data-ttu-id="de75c-155">Kaydı, bu örnek için Pig Latin hello olduğunda aynı her ikisi için hello:</span><span class="sxs-lookup"><span data-stu-id="de75c-155">Once past registration, hello Pig Latin for this example is hello same for both:</span></span>

```pig
LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
LOG = FILTER LOGS by LINE is not null;
DETAILS = FOREACH LOG GENERATE myfuncs.create_structure(LINE);
DUMP DETAILS;
```

<span data-ttu-id="de75c-156">Bu örnek yaptığı aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="de75c-156">Here's what this example does:</span></span>

1. <span data-ttu-id="de75c-157">Merhaba ilk satırı yükler hello örnek veri dosyası, `sample.log` içine `LOGS`.</span><span class="sxs-lookup"><span data-stu-id="de75c-157">hello first line loads hello sample data file, `sample.log` into `LOGS`.</span></span> <span data-ttu-id="de75c-158">Ayrıca her kayıt olarak tanımlayan bir `chararray`.</span><span class="sxs-lookup"><span data-stu-id="de75c-158">It also defines each record as a `chararray`.</span></span>
2. <span data-ttu-id="de75c-159">hello işleminin hello sonucu depolamak herhangi bir null değeri filtreleyen Hello sonraki satıra `LOG`.</span><span class="sxs-lookup"><span data-stu-id="de75c-159">hello next line filters out any null values, storing hello result of hello operation into `LOG`.</span></span>
3. <span data-ttu-id="de75c-160">Ardından, hello kayıtlarında üzerinden tekrarlanan `LOG` ve kullandığı `GENERATE` tooinvoke hello `create_structure` hello Python/Jython komut dosyasında yer alan yöntemi yüklü olarak `myfuncs`.</span><span class="sxs-lookup"><span data-stu-id="de75c-160">Next, it iterates over hello records in `LOG` and uses `GENERATE` tooinvoke hello `create_structure` method contained in hello Python/Jython script loaded as `myfuncs`.</span></span> <span data-ttu-id="de75c-161">`LINE`kullanılan toopass hello geçerli kayıt toohello işlevdir.</span><span class="sxs-lookup"><span data-stu-id="de75c-161">`LINE` is used toopass hello current record toohello function.</span></span>
4. <span data-ttu-id="de75c-162">Son olarak, hello çıkışları hello kullanarak Dökümü alınan tooSTDOUT olan `DUMP` komutu.</span><span class="sxs-lookup"><span data-stu-id="de75c-162">Finally, hello outputs are dumped tooSTDOUT using hello `DUMP` command.</span></span> <span data-ttu-id="de75c-163">Merhaba işlemi tamamlandıktan sonra bu komut hello sonuçları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="de75c-163">This command displays hello results after hello operation completes.</span></span>

### <a name="create-hello-pigudfpy-file"></a><span data-ttu-id="de75c-164">Merhaba pigudf.py dosyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="de75c-164">Create hello pigudf.py file</span></span>

<span data-ttu-id="de75c-165">Geliştirme ortamınızı adlı bir metin dosyası oluşturun `pigudf.py`.</span><span class="sxs-lookup"><span data-stu-id="de75c-165">On your development environment, create a text file named `pigudf.py`.</span></span> <span data-ttu-id="de75c-166">Merhaba dosyasının Merhaba içeriğine koddan hello kullan:</span><span class="sxs-lookup"><span data-stu-id="de75c-166">Use hello following code as hello contents of hello file:</span></span>

<a name="streamingpy"></a>

```python
# Uncomment hello following if using C Python
#from pig_util import outputSchema

@outputSchema("log: {(date:chararray, time:chararray, classname:chararray, level:chararray, detail:chararray)}")
def create_structure(input):
    if (input.startswith('java.lang.Exception')):
        input = input[21:len(input)] + ' - java.lang.Exception'
    date, time, classname, level, detail = input.split(' ', 4)
    return date, time, classname, level, detail
```

<span data-ttu-id="de75c-167">Merhaba Pig Latin örnekte biz hello tanımlanan `LINE` hello girişi için tutarlı bir şemayı olduğundan chararray girin.</span><span class="sxs-lookup"><span data-stu-id="de75c-167">In hello Pig Latin example, we defined hello `LINE` input as a chararray because there is no consistent schema for hello input.</span></span> <span data-ttu-id="de75c-168">Merhaba Python betiği hello veri çıkışı için tutarlı bir şema dönüştürür.</span><span class="sxs-lookup"><span data-stu-id="de75c-168">hello Python script transforms hello data into a consistent schema for output.</span></span>

1. <span data-ttu-id="de75c-169">Merhaba `@outputSchema` deyimi tooPig döndürülen hello verilerin hello biçimini tanımlar.</span><span class="sxs-lookup"><span data-stu-id="de75c-169">hello `@outputSchema` statement defines hello format of hello data that is returned tooPig.</span></span> <span data-ttu-id="de75c-170">Bu durumda olan bir **veri paketi**, Pig veri türü.</span><span class="sxs-lookup"><span data-stu-id="de75c-170">In this case, it's a **data bag**, which is a Pig data type.</span></span> <span data-ttu-id="de75c-171">Merhaba paketi chararray (dize) tümü alanları izleyen hello içerir:</span><span class="sxs-lookup"><span data-stu-id="de75c-171">hello bag contains hello following fields, all of which are chararray (strings):</span></span>

   * <span data-ttu-id="de75c-172">-Başlangıç tarihi hello günlük girişinin oluşturulduğu tarih</span><span class="sxs-lookup"><span data-stu-id="de75c-172">date - hello date hello log entry was created</span></span>
   * <span data-ttu-id="de75c-173">saati - hello günlük girişinin oluşturulduğu hello</span><span class="sxs-lookup"><span data-stu-id="de75c-173">time - hello time hello log entry was created</span></span>
   * <span data-ttu-id="de75c-174">ClassName - için hello sınıf adı hello girdisi oluşturuldu</span><span class="sxs-lookup"><span data-stu-id="de75c-174">classname - hello class name hello entry was created for</span></span>
   * <span data-ttu-id="de75c-175">Level - hello günlük düzeyi</span><span class="sxs-lookup"><span data-stu-id="de75c-175">level - hello log level</span></span>
   * <span data-ttu-id="de75c-176">Ayrıntı - verbose ayrıntılarını hello günlüğü girişi</span><span class="sxs-lookup"><span data-stu-id="de75c-176">detail - verbose details for hello log entry</span></span>

2. <span data-ttu-id="de75c-177">Ardından, hello `def create_structure(input)` Pig çizgi öğelerine geçirir hello işlevi tanımlar.</span><span class="sxs-lookup"><span data-stu-id="de75c-177">Next, hello `def create_structure(input)` defines hello function that Pig passes line items to.</span></span>

3. <span data-ttu-id="de75c-178">Merhaba örnek veri `sample.log`, çoğunlukla toohello tarih, saat, classname düzeyi, uyumlu ve ayrıntı şema tooreturn istiyoruz.</span><span class="sxs-lookup"><span data-stu-id="de75c-178">hello example data, `sample.log`, mostly conforms toohello date, time, classname, level, and detail schema we want tooreturn.</span></span> <span data-ttu-id="de75c-179">Ancak, ile başlayan birkaç satırları içeren `*java.lang.Exception*`.</span><span class="sxs-lookup"><span data-stu-id="de75c-179">However, it contains a few lines that begin with `*java.lang.Exception*`.</span></span> <span data-ttu-id="de75c-180">Bu satırlar değiştirilmiş toomatch hello şema olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="de75c-180">These lines must be modified toomatch hello schema.</span></span> <span data-ttu-id="de75c-181">Merhaba `if` deyimi için olanlar denetler ve ardından massages hello giriş verisi toomove hello `*java.lang.Exception*` hello veri satır içi bizim beklenen çıkış şemasıyla getiren dize toohello son.</span><span class="sxs-lookup"><span data-stu-id="de75c-181">hello `if` statement checks for those, then massages hello input data toomove hello `*java.lang.Exception*` string toohello end, bringing hello data in-line with our expected output schema.</span></span>

4. <span data-ttu-id="de75c-182">Ardından, hello `split` hello ilk dört boşluk karakterleri kullanılan toosplit hello veri komuttur.</span><span class="sxs-lookup"><span data-stu-id="de75c-182">Next, hello `split` command is used toosplit hello data at hello first four space characters.</span></span> <span data-ttu-id="de75c-183">Merhaba çıkış içine atandığı `date`, `time`, `classname`, `level`, ve `detail`.</span><span class="sxs-lookup"><span data-stu-id="de75c-183">hello output is assigned into `date`, `time`, `classname`, `level`, and `detail`.</span></span>

5. <span data-ttu-id="de75c-184">Son olarak, hello değerleri tooPig döndürülür.</span><span class="sxs-lookup"><span data-stu-id="de75c-184">Finally, hello values are returned tooPig.</span></span>

<span data-ttu-id="de75c-185">Merhaba veri tooPig döndürüldüğünde, onu tutarlı bir şemayı hello tanımlanan sahip `@outputSchema` deyimi.</span><span class="sxs-lookup"><span data-stu-id="de75c-185">When hello data is returned tooPig, it has a consistent schema as defined in hello `@outputSchema` statement.</span></span>

## <span data-ttu-id="de75c-186"><a name="running"></a>Karşıya yükleme ve başlangıç örnekleri çalıştırın</span><span class="sxs-lookup"><span data-stu-id="de75c-186"><a name="running"></a>Upload and run hello examples</span></span>

> [!IMPORTANT]
> <span data-ttu-id="de75c-187">Merhaba **SSH** adımlar, yalnızca Linux tabanlı Hdınsight kümesi ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="de75c-187">hello **SSH** steps only work with a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="de75c-188">Merhaba **PowerShell** adımları bir Linux veya Windows tabanlı Hdınsight kümesi ile çalışır, ancak bir Windows istemci gerektirir.</span><span class="sxs-lookup"><span data-stu-id="de75c-188">hello **PowerShell** steps work with either a Linux or Windows-based HDInsight cluster, but require a Windows client.</span></span>

### <a name="ssh"></a><span data-ttu-id="de75c-189">SSH</span><span class="sxs-lookup"><span data-stu-id="de75c-189">SSH</span></span>

<span data-ttu-id="de75c-190">SSH kullanma hakkında daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="de75c-190">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="de75c-191">Kullanım `scp` toocopy hello dosyaları tooyour Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="de75c-191">Use `scp` toocopy hello files tooyour HDInsight cluster.</span></span> <span data-ttu-id="de75c-192">Örneğin, kopya hello adlı dosyaları tooa küme komutu aşağıdaki hello **mycluster**.</span><span class="sxs-lookup"><span data-stu-id="de75c-192">For example, hello following command copies hello files tooa cluster named **mycluster**.</span></span>

    ```bash
    scp hiveudf.py pigudf.py myuser@mycluster-ssh.azurehdinsight.net:
    ```

2. <span data-ttu-id="de75c-193">SSH tooconnect toohello küme kullanın.</span><span class="sxs-lookup"><span data-stu-id="de75c-193">Use SSH tooconnect toohello cluster.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="de75c-194">Merhaba SSH oturumundan hello python dosyaları toohello WASB depolama hello küme için daha önce karşıya ekleyin.</span><span class="sxs-lookup"><span data-stu-id="de75c-194">From hello SSH session, add hello python files uploaded previously toohello WASB storage for hello cluster.</span></span>

    ```bash
    hdfs dfs -put hiveudf.py /hiveudf.py
    hdfs dfs -put pigudf.py /pigudf.py
    ```

<span data-ttu-id="de75c-195">Merhaba dosyalarını karşıya yükledikten sonra toorun hello Hive ve Pig işleri kullanım hello aşağıdaki adımları.</span><span class="sxs-lookup"><span data-stu-id="de75c-195">After uploading hello files, use hello following steps toorun hello Hive and Pig jobs.</span></span>

#### <a name="use-hello-hive-udf"></a><span data-ttu-id="de75c-196">Merhaba Hive UDF kullanın</span><span class="sxs-lookup"><span data-stu-id="de75c-196">Use hello Hive UDF</span></span>

1. <span data-ttu-id="de75c-197">Kullanım hello `hive` toostart hello hive kabuğunu komutu.</span><span class="sxs-lookup"><span data-stu-id="de75c-197">Use hello `hive` command toostart hello hive shell.</span></span> <span data-ttu-id="de75c-198">Görmeniz gerekir bir `hive>` hello Kabuk yüklendikten sonra ister.</span><span class="sxs-lookup"><span data-stu-id="de75c-198">You should see a `hive>` prompt once hello shell has loaded.</span></span>

2. <span data-ttu-id="de75c-199">Merhaba sorgusu aşağıdaki hello girin `hive>` istemi:</span><span class="sxs-lookup"><span data-stu-id="de75c-199">Enter hello following query at hello `hive>` prompt:</span></span>

   ```hive
   add file wasb:///hiveudf.py;
   SELECT TRANSFORM (clientid, devicemake, devicemodel)
       USING 'python hiveudf.py' AS
       (clientid string, phoneLabel string, phoneHash string)
   FROM hivesampletable
   ORDER BY clientid LIMIT 50;
   ```

3. <span data-ttu-id="de75c-200">Merhaba son satırı girdikten sonra hello iş başlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="de75c-200">After entering hello last line, hello job should start.</span></span> <span data-ttu-id="de75c-201">Merhaba işi tamamlandıktan sonra aşağıdaki örnek çıkış benzer toohello döndürür:</span><span class="sxs-lookup"><span data-stu-id="de75c-201">Once hello job completes, it returns output similar toohello following example:</span></span>

        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="use-hello-pig-udf"></a><span data-ttu-id="de75c-202">Merhaba Pig UDF kullanın</span><span class="sxs-lookup"><span data-stu-id="de75c-202">Use hello Pig UDF</span></span>

1. <span data-ttu-id="de75c-203">Kullanım hello `pig` toostart hello Kabuk komutu.</span><span class="sxs-lookup"><span data-stu-id="de75c-203">Use hello `pig` command toostart hello shell.</span></span> <span data-ttu-id="de75c-204">Gördüğünüz bir `grunt>` hello Kabuk yüklendikten sonra ister.</span><span class="sxs-lookup"><span data-stu-id="de75c-204">You see a `grunt>` prompt once hello shell has loaded.</span></span>

2. <span data-ttu-id="de75c-205">Merhaba deyimlerini aşağıdaki hello girin `grunt>` istemi:</span><span class="sxs-lookup"><span data-stu-id="de75c-205">Enter hello following statements at hello `grunt>` prompt:</span></span>

   ```pig
   Register wasb:///pigudf.py using jython as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

3. <span data-ttu-id="de75c-206">Satır aşağıdaki hello girdikten sonra hello iş başlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="de75c-206">After entering hello following line, hello job should start.</span></span> <span data-ttu-id="de75c-207">Merhaba işi tamamlandığında, çıkış benzer toohello veri aşağıdaki döndürür:</span><span class="sxs-lookup"><span data-stu-id="de75c-207">Once hello job completes, it returns output similar toohello following data:</span></span>

        ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
        ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
        ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
        ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
        ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

4. <span data-ttu-id="de75c-208">Kullanmak `quit` tooexit Grunt Kabuk hello ve aşağıdaki tooedit hello pigudf.py dosyasına hello yerel dosya sisteminde hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="de75c-208">Use `quit` tooexit hello Grunt shell, and then use hello following tooedit hello pigudf.py file on hello local file system:</span></span>

    ```bash
    nano pigudf.py
    ```

5. <span data-ttu-id="de75c-209">Bir kez hello Düzenleyicisi'nde hello kaldırarak satır aşağıdaki hello açıklamadan çıkarın `#` hello satırının hello başından karakteri:</span><span class="sxs-lookup"><span data-stu-id="de75c-209">Once in hello editor, uncomment hello following line by removing hello `#` character from hello beginning of hello line:</span></span>

    ```bash
    #from pig_util import outputSchema
    ```

    <span data-ttu-id="de75c-210">Merhaba değişiklik yapıldıktan sonra Ctrl + X tooexit hello Düzenleyicisi'ni kullanın.</span><span class="sxs-lookup"><span data-stu-id="de75c-210">Once hello change has been made, use Ctrl+X tooexit hello editor.</span></span> <span data-ttu-id="de75c-211">Y seçin ve ardından toosave hello değişiklikleri girin.</span><span class="sxs-lookup"><span data-stu-id="de75c-211">Select Y, and then enter toosave hello changes.</span></span>

6. <span data-ttu-id="de75c-212">Kullanım hello `pig` toostart hello Kabuğu komutunu yeniden.</span><span class="sxs-lookup"><span data-stu-id="de75c-212">Use hello `pig` command toostart hello shell again.</span></span> <span data-ttu-id="de75c-213">Hello olduğunuzda `grunt>` isteminde, hello C Python yorumlayıcı kullanılarak toorun hello Python komut aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="de75c-213">Once you are at hello `grunt>` prompt, use hello following toorun hello Python script using hello C Python interpreter.</span></span>

   ```pig
   Register 'pigudf.py' using streaming_python as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

    <span data-ttu-id="de75c-214">Bu iş tamamlandığında, ne zaman, daha önce Jython kullanılarak hello komut çalıştırıldığı aynı çıktı hello görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="de75c-214">Once this job completes, you should see hello same output as when you previously ran hello script using Jython.</span></span>

### <a name="powershell-upload-hello-files"></a><span data-ttu-id="de75c-215">PowerShell: Karşıya yükleme hello dosyaları</span><span class="sxs-lookup"><span data-stu-id="de75c-215">PowerShell: Upload hello files</span></span>

<span data-ttu-id="de75c-216">PowerShell tooupload hello dosyaları toohello Hdınsight sunucusuna kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="de75c-216">You can use PowerShell tooupload hello files toohello HDInsight server.</span></span> <span data-ttu-id="de75c-217">Aşağıdaki komut dosyası tooupload hello Python dosyaları hello kullan:</span><span class="sxs-lookup"><span data-stu-id="de75c-217">Use hello following script tooupload hello Python files:</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="de75c-218">Bu bölümdeki adımları Hello Azure PowerShell kullanın.</span><span class="sxs-lookup"><span data-stu-id="de75c-218">hello steps in this section use Azure PowerShell.</span></span> <span data-ttu-id="de75c-219">Azure PowerShell kullanma hakkında daha fazla bilgi için bkz: [nasıl tooinstall Azure PowerShell'i ve yapılandırma](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="de75c-219">For more information on using Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
# Change hello path toomatch hello file location on your system
$pathToStreamingFile = "C:\path\to\hiveudf.py"
$pathToJythonFile = "C:\path\to\pigudf.py"

$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName=$clusterInfo.DefaultStorageAccount.split('.')[0]
$container=$clusterInfo.DefaultStorageContainer
$storageAccountKey=(Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage content and upload hello file
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
> <span data-ttu-id="de75c-220">Değişiklik hello `C:\path\to` toohello yolu toohello geliştirme ortamınızı dosyalarda değeri.</span><span class="sxs-lookup"><span data-stu-id="de75c-220">Change hello `C:\path\to` value toohello path toohello files on your development environment.</span></span>

<span data-ttu-id="de75c-221">Bu betiği Hdınsight kümenizle ilgili bilgileri alır ve ardından hello hesabı ve anahtarı hello varsayılan depolama hesabı için ayıklar ve karşıya dosya toohello kök hello kapsayıcısının hello.</span><span class="sxs-lookup"><span data-stu-id="de75c-221">This script retrieves information for your HDInsight cluster, then extracts hello account and key for hello default storage account, and uploads hello files toohello root of hello container.</span></span>

> [!NOTE]
> <span data-ttu-id="de75c-222">Dosyaları karşıya yükleme ile ilgili daha fazla bilgi için bkz: hello [hdınsight'ta Hadoop işleri için verileri karşıya yükleme](hdinsight-upload-data.md) belge.</span><span class="sxs-lookup"><span data-stu-id="de75c-222">For more information on uploading files, see hello [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md) document.</span></span>

#### <a name="powershell-use-hello-hive-udf"></a><span data-ttu-id="de75c-223">PowerShell: hello Hive UDF kullanın</span><span class="sxs-lookup"><span data-stu-id="de75c-223">PowerShell: Use hello Hive UDF</span></span>

<span data-ttu-id="de75c-224">PowerShell çalıştırma kullanılan tooremotely Hive sorguları da olabilir.</span><span class="sxs-lookup"><span data-stu-id="de75c-224">PowerShell can also be used tooremotely run Hive queries.</span></span> <span data-ttu-id="de75c-225">PowerShell komut dosyası toorun kullanan bir Hive sorgusu aşağıdaki kullanım hello **hiveudf.py** komut dosyası:</span><span class="sxs-lookup"><span data-stu-id="de75c-225">Use hello following PowerShell script toorun a Hive query that uses **hiveudf.py** script:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="de75c-226">Çalıştırmadan önce hello betik hello Hdınsight kümeniz için HTTPs/Admin hesap bilgilerini ister.</span><span class="sxs-lookup"><span data-stu-id="de75c-226">Before running, hello script prompts you for hello HTTPs/Admin account information for your HDInsight cluster.</span></span>

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

# If using a Windows-based HDInsight cluster, change hello USING statement to:
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
Write-Host "Wait for hello Hive job toocomplete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -JobId $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment hello following toosee stderr output
# Get-AzureRmHDInsightJobOutput `
#   -Clustername $clusterName `
#   -JobId $job.JobId `
#   -HttpCredential $creds `
#   -DisplayOutputType StandardError
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

<span data-ttu-id="de75c-227">Merhaba hello için çıktı **Hive** işi aşağıdaki örneğine benzer toohello görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="de75c-227">hello output for hello **Hive** job should appear similar toohello following example:</span></span>

    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="pig-jython"></a><span data-ttu-id="de75c-228">Pig (Jython)</span><span class="sxs-lookup"><span data-stu-id="de75c-228">Pig (Jython)</span></span>

<span data-ttu-id="de75c-229">PowerShell kullanılan toorun Pig Latin işleri de olabilir.</span><span class="sxs-lookup"><span data-stu-id="de75c-229">PowerShell can also be used toorun Pig Latin jobs.</span></span> <span data-ttu-id="de75c-230">toorun hello kullanan bir Pig Latin iş **pigudf.py** komut dosyası, PowerShell Betiği aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="de75c-230">toorun a Pig Latin job that uses hello **pigudf.py** script, use hello following PowerShell script:</span></span>

> [!NOTE]
> <span data-ttu-id="de75c-231">PowerShell kullanarak işi uzaktan gönderirken, olası toouse C Python hello yorumlayıcı değil.</span><span class="sxs-lookup"><span data-stu-id="de75c-231">When remotely submitting a job using PowerShell, it is not possible toouse C Python as hello interpreter.</span></span>

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

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

Write-Host "Wait for hello Pig job toocomplete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -Job $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment hello following toosee stderr output
# Get-AzureRmHDInsightJobOutput `
#    -Clustername $clusterName `
#    -JobId $job.JobId `
#    -HttpCredential $creds `
#    -DisplayOutputType StandardError
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

<span data-ttu-id="de75c-232">Merhaba hello için çıktı **Pig** işi veri aşağıdaki benzer toohello görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="de75c-232">hello output for hello **Pig** job should appear similar toohello following data:</span></span>

    ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
    ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
    ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
    ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
    ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

## <span data-ttu-id="de75c-233"><a name="troubleshooting"></a>Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="de75c-233"><a name="troubleshooting"></a>Troubleshooting</span></span>

### <a name="errors-when-running-jobs"></a><span data-ttu-id="de75c-234">İşlerini çalışırken hataları</span><span class="sxs-lookup"><span data-stu-id="de75c-234">Errors when running jobs</span></span>

<span data-ttu-id="de75c-235">Merhaba hive işi çalıştırırken metnini izleyen bir hata benzer toohello karşılaşabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="de75c-235">When running hello hive job, you may encounter an error similar toohello following text:</span></span>

    Caused by: org.apache.hadoop.hive.ql.metadata.HiveException: [Error 20001]: An error occurred while reading or writing tooyour custom script. It may have crashed with an error.

<span data-ttu-id="de75c-236">Bu sorunun nedeni hello satır sonları hello Python dosyasında.</span><span class="sxs-lookup"><span data-stu-id="de75c-236">This problem may be caused by hello line endings in hello Python file.</span></span> <span data-ttu-id="de75c-237">Çok sayıda Windows düzenleyicileri toousing CRLF varsayılan bitiş hello çizgi ancak Linux uygulamalar genellikle LF bekler.</span><span class="sxs-lookup"><span data-stu-id="de75c-237">Many Windows editors default toousing CRLF as hello line ending, but Linux applications usually expect LF.</span></span>

<span data-ttu-id="de75c-238">Merhaba dosya tooHDInsight karşıya yüklemeden önce aşağıdaki PowerShell deyimleri tooremove hello CR karakterleri hello kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="de75c-238">You can use hello following PowerShell statements tooremove hello CR characters before uploading hello file tooHDInsight:</span></span>

```powershell
$original_file ='c:\path\to\hiveudf.py'
$text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
[IO.File]::WriteAllText($original_file, $text)
```

### <a name="powershell-scripts"></a><span data-ttu-id="de75c-239">PowerShell komut dosyaları</span><span class="sxs-lookup"><span data-stu-id="de75c-239">PowerShell scripts</span></span>

<span data-ttu-id="de75c-240">Merhaba örnek PowerShell komut dosyalarını toorun hello örneklerde kullanılan her ikisi de hello işi için hata çıktısını görüntüler açıklamalı bir satır içerir.</span><span class="sxs-lookup"><span data-stu-id="de75c-240">Both of hello example PowerShell scripts used toorun hello examples contain a commented line that displays error output for hello job.</span></span> <span data-ttu-id="de75c-241">Merhaba beklenen çıktı hello işi için görüyorsanız değil, hello aşağıdaki satır ve hello hata bilgileri bir sorun olduğunu gösteriyor varsa bkz açıklamadan çıkarın.</span><span class="sxs-lookup"><span data-stu-id="de75c-241">If you are not seeing hello expected output for hello job, uncomment hello following line and see if hello error information indicates a problem.</span></span>

```powershell
# Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="de75c-242">Ayrıca Hello hata bilgileri (STDERR) ve hello işi (STDOUT) hello sonucunu oturum tooyour Hdınsight depolama değildir.</span><span class="sxs-lookup"><span data-stu-id="de75c-242">hello error information (STDERR) and hello result of hello job (STDOUT) are also logged tooyour HDInsight storage.</span></span>

| <span data-ttu-id="de75c-243">Bu iş için...</span><span class="sxs-lookup"><span data-stu-id="de75c-243">For this job...</span></span> | <span data-ttu-id="de75c-244">Bu dosyalar hello blob kapsayıcısında bakın</span><span class="sxs-lookup"><span data-stu-id="de75c-244">Look at these files in hello blob container</span></span> |
| --- | --- |
| <span data-ttu-id="de75c-245">Hive</span><span class="sxs-lookup"><span data-stu-id="de75c-245">Hive</span></span> |<span data-ttu-id="de75c-246">/ HivePython/stderr</span><span class="sxs-lookup"><span data-stu-id="de75c-246">/HivePython/stderr</span></span><p><span data-ttu-id="de75c-247">/ HivePython/stdout</span><span class="sxs-lookup"><span data-stu-id="de75c-247">/HivePython/stdout</span></span> |
| <span data-ttu-id="de75c-248">Pig</span><span class="sxs-lookup"><span data-stu-id="de75c-248">Pig</span></span> |<span data-ttu-id="de75c-249">/ PigPython/stderr</span><span class="sxs-lookup"><span data-stu-id="de75c-249">/PigPython/stderr</span></span><p><span data-ttu-id="de75c-250">/ PigPython/stdout</span><span class="sxs-lookup"><span data-stu-id="de75c-250">/PigPython/stdout</span></span> |

## <span data-ttu-id="de75c-251"><a name="next"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="de75c-251"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="de75c-252">Varsayılan olarak sağlanmayan tooload Python modülleri gerekirse bkz [nasıl toodeploy modülü tooAzure Hdınsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span><span class="sxs-lookup"><span data-stu-id="de75c-252">If you need tooload Python modules that aren't provided by default, see [How toodeploy a module tooAzure HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span></span>

<span data-ttu-id="de75c-253">Diğer yolları toouse Pig, Hive ve MapReduce kullanma hakkında toolearn için belgeler aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="de75c-253">For other ways toouse Pig, Hive, and toolearn about using MapReduce, see hello following documents:</span></span>

* [<span data-ttu-id="de75c-254">HDInsight ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="de75c-254">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="de75c-255">HDInsight ile Pig kullanma</span><span class="sxs-lookup"><span data-stu-id="de75c-255">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="de75c-256">Hdınsight ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="de75c-256">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
