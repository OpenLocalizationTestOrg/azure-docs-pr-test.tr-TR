---
title: "Hdınsight'ta - Azure Hadoop ile MapReduce ve SSH bağlantısı | Microsoft Docs"
description: "MapReduce işleri Hdınsight'ta Hadoop kullanarak çalıştırmak için SSH kullanmayı öğrenin."
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
ms.openlocfilehash: eaf6278f97cd5ddd7e049ff4745181f39d7949a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="use-mapreduce-with-hadoop-on-hdinsight-with-ssh"></a><span data-ttu-id="576dc-103">Hdınsight ile SSH Hadoop ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="576dc-103">Use MapReduce with Hadoop on HDInsight with SSH</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="576dc-104">Güvenli Kabuk (SSH) bağlantısı MapReduce işleri hdınsight'a gönderme öğrenin.</span><span class="sxs-lookup"><span data-stu-id="576dc-104">Learn how to submit MapReduce jobs from a Secure Shell (SSH) connection to HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="576dc-105">Linux tabanlı Hadoop sunucuları kullanarak bilginiz, ancak yeni Hdınsight için, bkz: [Linux tabanlı Hdınsight ipuçları](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="576dc-105">If you are already familiar with using Linux-based Hadoop servers, but you are new to HDInsight, see [Linux-based HDInsight tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="576dc-106"><a id="prereq"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="576dc-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="576dc-107">Linux tabanlı Hdınsight (Hadoop hdınsight) küme</span><span class="sxs-lookup"><span data-stu-id="576dc-107">A Linux-based HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="576dc-108">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="576dc-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="576dc-109">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="576dc-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="576dc-110">Bir SSH istemcisi.</span><span class="sxs-lookup"><span data-stu-id="576dc-110">An SSH client.</span></span> <span data-ttu-id="576dc-111">Daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="576dc-111">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

## <span data-ttu-id="576dc-112"><a id="ssh"></a>SSH ile bağlanma</span><span class="sxs-lookup"><span data-stu-id="576dc-112"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="576dc-113">SSH kullanarak kümeye bağlanın.</span><span class="sxs-lookup"><span data-stu-id="576dc-113">Connect to the cluster using SSH.</span></span> <span data-ttu-id="576dc-114">Örneğin, aşağıdaki komutu adlı bir kümeye bağlanır **myhdinsight**:</span><span class="sxs-lookup"><span data-stu-id="576dc-114">For example, the following command connects to a cluster named **myhdinsight**:</span></span>

```bash
ssh admin@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="576dc-115">**SSH kimlik doğrulaması için bir sertifika anahtarı kullanırsanız**, örneğin, istemci sisteminizde özel anahtarı konumunu belirtmeniz gerekebilir:</span><span class="sxs-lookup"><span data-stu-id="576dc-115">**If you use a certificate key for SSH authentication**, you may need to specify the location of the private key on your client system, for example:</span></span>

```bash
ssh -i ~/mykey.key admin@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="576dc-116">**SSH kimlik doğrulaması için bir parola kullanıyorsanız**, istendiğinde parolayı sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="576dc-116">**If you use a password for SSH authentication**, you need to provide the password when prompted.</span></span>

<span data-ttu-id="576dc-117">Hdınsight ile SSH kullanma hakkında daha fazla bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="576dc-117">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="576dc-118"><a id="hadoop"></a>Hadoop komutları kullanın</span><span class="sxs-lookup"><span data-stu-id="576dc-118"><a id="hadoop"></a>Use Hadoop commands</span></span>

1. <span data-ttu-id="576dc-119">Hdınsight kümesine bağlandıktan sonra bir MapReduce işi başlatmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="576dc-119">After you are connected to the HDInsight cluster, use the following command to start a MapReduce job:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/WordCountOutput
    ```

    <span data-ttu-id="576dc-120">Bu komut başlatır `wordcount` bulunan sınıfı `hadoop-mapreduce-examples.jar` dosya.</span><span class="sxs-lookup"><span data-stu-id="576dc-120">This command starts the `wordcount` class, which is contained in the `hadoop-mapreduce-examples.jar` file.</span></span> <span data-ttu-id="576dc-121">Kullandığı `/example/data/gutenberg/davinci.txt` belge giriş ve çıkış olarak depolandı `/example/data/WordCountOutput`.</span><span class="sxs-lookup"><span data-stu-id="576dc-121">It uses the `/example/data/gutenberg/davinci.txt` document as input, and output is stored at `/example/data/WordCountOutput`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="576dc-122">Bu MapReduce işi ve örnek veriler hakkında daha fazla bilgi için bkz: [hdınsight'ta Hadoop içinde kullanım MapReduce](hdinsight-use-mapreduce.md).</span><span class="sxs-lookup"><span data-stu-id="576dc-122">For more information about this MapReduce job and the example data, see [Use MapReduce in Hadoop on HDInsight](hdinsight-use-mapreduce.md).</span></span>

2. <span data-ttu-id="576dc-123">İş, işler ve iş tamamlandığında, bilgileri aşağıdaki metni benzer döndürür gibi ayrıntıları gösterir:</span><span class="sxs-lookup"><span data-stu-id="576dc-123">The job emits details as it processes, and it returns information similar to the following text when the job completes:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623

3. <span data-ttu-id="576dc-124">İş tamamlandığında, çıkış dosyaları listelemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="576dc-124">When the job completes, use the following command to list the output files:</span></span>

    ```bash
    hdfs dfs -ls /example/data/WordCountOutput
    ```

    <span data-ttu-id="576dc-125">Bu komut, iki dosya görüntülemek `_SUCCESS` ve `part-r-00000`.</span><span class="sxs-lookup"><span data-stu-id="576dc-125">This command display two files, `_SUCCESS` and `part-r-00000`.</span></span> <span data-ttu-id="576dc-126">`part-r-00000` Dosyası bu iş için çıktıyı içerir.</span><span class="sxs-lookup"><span data-stu-id="576dc-126">The `part-r-00000` file contains the output for this job.</span></span>

    > [!NOTE]
    > <span data-ttu-id="576dc-127">Bazı MapReduce işleri sonuçları birden çok bölme **bölümü r ###** dosyaları.</span><span class="sxs-lookup"><span data-stu-id="576dc-127">Some MapReduce jobs may split the results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="576dc-128">Bu durumda, kullanın ### dosyaların sırasını belirtmek için soneki.</span><span class="sxs-lookup"><span data-stu-id="576dc-128">If so, use the ##### suffix to indicate the order of the files.</span></span>

4. <span data-ttu-id="576dc-129">Çıktı görüntülemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="576dc-129">To view the output, use the following command:</span></span>

    ```bash
    hdfs dfs -cat /example/data/WordCountOutput/part-r-00000
    ```

    <span data-ttu-id="576dc-130">Bu komut bulunan sözcüklerin listesini görüntüler **wasb://example/data/gutenberg/davinci.txt** dosya ve her sözcüğün yapma sayısı.</span><span class="sxs-lookup"><span data-stu-id="576dc-130">This command displays a list of the words that are contained in the **wasb://example/data/gutenberg/davinci.txt** file and the number of times each word occurred.</span></span> <span data-ttu-id="576dc-131">Aşağıdaki metin dosyasında bulunan verileri örneğidir:</span><span class="sxs-lookup"><span data-stu-id="576dc-131">The following text is an example of the data that is contained in the file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <span data-ttu-id="576dc-132"><a id="summary"></a>Özet</span><span class="sxs-lookup"><span data-stu-id="576dc-132"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="576dc-133">Gördüğünüz gibi Hadoop komutları bir Hdınsight küme MapReduce işleri çalıştırma ve iş çıktısı görüntülemek için kolay bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="576dc-133">As you can see, Hadoop commands provide an easy way to run MapReduce jobs in an HDInsight cluster and then view the job output.</span></span>

## <span data-ttu-id="576dc-134"><a id="nextsteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="576dc-134"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="576dc-135">Hdınsight'ta MapReduce işleri hakkında genel bilgi için:</span><span class="sxs-lookup"><span data-stu-id="576dc-135">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="576dc-136">Hdınsight Hadoop MapReduce kullanın</span><span class="sxs-lookup"><span data-stu-id="576dc-136">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="576dc-137">Diğer yolları hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="576dc-137">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="576dc-138">Hdınsight'ta Hadoop ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="576dc-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="576dc-139">Hdınsight'ta Hadoop ile pig kullanma</span><span class="sxs-lookup"><span data-stu-id="576dc-139">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
