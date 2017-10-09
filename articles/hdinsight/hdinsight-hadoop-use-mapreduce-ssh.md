---
title: "aaaMapReduce ve hdınsight'ta - Azure Hadoop ile SSH bağlantısı | Microsoft Docs"
description: "Hdınsight'ta Hadoop kullanarak nasıl toouse SSH toorun MapReduce işleri öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 844678ba-1e1f-4fda-b9ef-34df4035d547
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 9626577687fc5cc119a39d65a9c45298f57f81c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-with-hadoop-on-hdinsight-with-ssh"></a><span data-ttu-id="3ec41-103">Hdınsight ile SSH Hadoop ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="3ec41-103">Use MapReduce with Hadoop on HDInsight with SSH</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="3ec41-104">Nasıl bir güvenli Kabuk (SSH) bağlantısı tooHDInsight toosubmit MapReduce işleri öğrenin.</span><span class="sxs-lookup"><span data-stu-id="3ec41-104">Learn how toosubmit MapReduce jobs from a Secure Shell (SSH) connection tooHDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="3ec41-105">Zaten biliyorsanız Linux tabanlı Hadoop kullanmaya sunucuları, ancak yeni tooHDInsight bkz [Linux tabanlı Hdınsight ipuçları](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="3ec41-105">If you are already familiar with using Linux-based Hadoop servers, but you are new tooHDInsight, see [Linux-based HDInsight tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="3ec41-106"><a id="prereq"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="3ec41-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="3ec41-107">Linux tabanlı Hdınsight (Hadoop hdınsight) küme</span><span class="sxs-lookup"><span data-stu-id="3ec41-107">A Linux-based HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="3ec41-108">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="3ec41-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3ec41-109">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="3ec41-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="3ec41-110">Bir SSH istemcisi.</span><span class="sxs-lookup"><span data-stu-id="3ec41-110">An SSH client.</span></span> <span data-ttu-id="3ec41-111">Daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="3ec41-111">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

## <span data-ttu-id="3ec41-112"><a id="ssh"></a>SSH ile bağlanma</span><span class="sxs-lookup"><span data-stu-id="3ec41-112"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="3ec41-113">SSH kullanarak toohello kümesine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="3ec41-113">Connect toohello cluster using SSH.</span></span> <span data-ttu-id="3ec41-114">Örneğin, komutu aşağıdaki hello adlı tooa küme bağlayan **myhdinsight**:</span><span class="sxs-lookup"><span data-stu-id="3ec41-114">For example, hello following command connects tooa cluster named **myhdinsight**:</span></span>

```bash
ssh admin@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="3ec41-115">**SSH kimlik doğrulaması için bir sertifika anahtarı kullanırsanız**, örneğin, istemci sisteminizde toospecify hello hello özel anahtarın konumunu gerekebilir:</span><span class="sxs-lookup"><span data-stu-id="3ec41-115">**If you use a certificate key for SSH authentication**, you may need toospecify hello location of hello private key on your client system, for example:</span></span>

```bash
ssh -i ~/mykey.key admin@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="3ec41-116">**SSH kimlik doğrulaması için bir parola kullanıyorsanız**, istendiğinde tooprovide hello parolası gerekir.</span><span class="sxs-lookup"><span data-stu-id="3ec41-116">**If you use a password for SSH authentication**, you need tooprovide hello password when prompted.</span></span>

<span data-ttu-id="3ec41-117">Hdınsight ile SSH kullanma hakkında daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="3ec41-117">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="3ec41-118"><a id="hadoop"></a>Hadoop komutları kullanın</span><span class="sxs-lookup"><span data-stu-id="3ec41-118"><a id="hadoop"></a>Use Hadoop commands</span></span>

1. <span data-ttu-id="3ec41-119">Bağlı toohello Hdınsight kümesi olduktan sonra komutu toostart bir MapReduce işi aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="3ec41-119">After you are connected toohello HDInsight cluster, use hello following command toostart a MapReduce job:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/WordCountOutput
    ```

    <span data-ttu-id="3ec41-120">Bu komut hello başlatır `wordcount` hello bulunan sınıfı `hadoop-mapreduce-examples.jar` dosya.</span><span class="sxs-lookup"><span data-stu-id="3ec41-120">This command starts hello `wordcount` class, which is contained in hello `hadoop-mapreduce-examples.jar` file.</span></span> <span data-ttu-id="3ec41-121">Merhaba kullanan `/example/data/gutenberg/davinci.txt` belge giriş ve çıkış olarak depolandı `/example/data/WordCountOutput`.</span><span class="sxs-lookup"><span data-stu-id="3ec41-121">It uses hello `/example/data/gutenberg/davinci.txt` document as input, and output is stored at `/example/data/WordCountOutput`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3ec41-122">Bu MapReduce işi ve hello örnek veriler hakkında daha fazla bilgi için bkz: [hdınsight'ta Hadoop içinde kullanım MapReduce](hdinsight-use-mapreduce.md).</span><span class="sxs-lookup"><span data-stu-id="3ec41-122">For more information about this MapReduce job and hello example data, see [Use MapReduce in Hadoop on HDInsight](hdinsight-use-mapreduce.md).</span></span>

2. <span data-ttu-id="3ec41-123">Merhaba iş, işler ve metin hello işi tamamlandığında aşağıdaki bilgileri benzer toohello döndürür Ayrıntılar gösterir:</span><span class="sxs-lookup"><span data-stu-id="3ec41-123">hello job emits details as it processes, and it returns information similar toohello following text when hello job completes:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623

3. <span data-ttu-id="3ec41-124">Merhaba işi tamamlandığında, aşağıdaki komut toolist hello çıktı dosyaları hello kullan:</span><span class="sxs-lookup"><span data-stu-id="3ec41-124">When hello job completes, use hello following command toolist hello output files:</span></span>

    ```bash
    hdfs dfs -ls /example/data/WordCountOutput
    ```

    <span data-ttu-id="3ec41-125">Bu komut, iki dosya görüntülemek `_SUCCESS` ve `part-r-00000`.</span><span class="sxs-lookup"><span data-stu-id="3ec41-125">This command display two files, `_SUCCESS` and `part-r-00000`.</span></span> <span data-ttu-id="3ec41-126">Merhaba `part-r-00000` dosyası hello çıktı bu iş için içerir.</span><span class="sxs-lookup"><span data-stu-id="3ec41-126">hello `part-r-00000` file contains hello output for this job.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3ec41-127">Bazı MapReduce işleri hello sonuçları birden çok bölme **bölümü r ###** dosyaları.</span><span class="sxs-lookup"><span data-stu-id="3ec41-127">Some MapReduce jobs may split hello results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="3ec41-128">Öyleyse, hello kullan ### soneki hello dosyalarının tooindicate hello sırası.</span><span class="sxs-lookup"><span data-stu-id="3ec41-128">If so, use hello ##### suffix tooindicate hello order of hello files.</span></span>

4. <span data-ttu-id="3ec41-129">tooview hello çıkışı, komutu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="3ec41-129">tooview hello output, use hello following command:</span></span>

    ```bash
    hdfs dfs -cat /example/data/WordCountOutput/part-r-00000
    ```

    <span data-ttu-id="3ec41-130">Bu komut hello içerdiği hello sözcüklerin listesini görüntüler **wasb://example/data/gutenberg/davinci.txt** dosya ve hello sayısı her sözcüğün oluştu.</span><span class="sxs-lookup"><span data-stu-id="3ec41-130">This command displays a list of hello words that are contained in hello **wasb://example/data/gutenberg/davinci.txt** file and hello number of times each word occurred.</span></span> <span data-ttu-id="3ec41-131">Merhaba aşağıdaki metni hello dosyasında yer alan hello veri örneğidir:</span><span class="sxs-lookup"><span data-stu-id="3ec41-131">hello following text is an example of hello data that is contained in hello file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <span data-ttu-id="3ec41-132"><a id="summary"></a>Özet</span><span class="sxs-lookup"><span data-stu-id="3ec41-132"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="3ec41-133">Gördüğünüz gibi Hadoop komutları bir Hdınsight kümesi ve sonra Görünüm hello iş çıktısı MapReduce işleri kolay bir yolu toorun sağlar.</span><span class="sxs-lookup"><span data-stu-id="3ec41-133">As you can see, Hadoop commands provide an easy way toorun MapReduce jobs in an HDInsight cluster and then view hello job output.</span></span>

## <span data-ttu-id="3ec41-134"><a id="nextsteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="3ec41-134"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="3ec41-135">Hdınsight'ta MapReduce işleri hakkında genel bilgi için:</span><span class="sxs-lookup"><span data-stu-id="3ec41-135">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="3ec41-136">Hdınsight Hadoop MapReduce kullanın</span><span class="sxs-lookup"><span data-stu-id="3ec41-136">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="3ec41-137">Diğer yolları hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3ec41-137">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="3ec41-138">Hdınsight'ta Hadoop ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="3ec41-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="3ec41-139">Hdınsight'ta Hadoop ile pig kullanma</span><span class="sxs-lookup"><span data-stu-id="3ec41-139">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
