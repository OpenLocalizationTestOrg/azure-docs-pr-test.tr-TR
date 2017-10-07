---
title: "aaaUse C# ile MapReduce hdınsight'ta - Azure hadoop'ta | Microsoft Docs"
description: "Bilgi nasıl Azure hdınsight'ta Hadoop ile toouse C# toocreate MapReduce çözümler."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d83def76-12ad-4538-bb8e-3ba3542b7211
ms.custom: hdinsightactive
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: dd8b684e74155bc1a37d4ab8d6f9033276ef5aa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-with-mapreduce-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="a7036-103">C# MapReduce hdınsight'ta Hadoop akış ile kullanma</span><span class="sxs-lookup"><span data-stu-id="a7036-103">Use C# with MapReduce streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="a7036-104">Bilgi nasıl toouse C# toocreate hdınsight'ta MapReduce çözümü.</span><span class="sxs-lookup"><span data-stu-id="a7036-104">Learn how toouse C# toocreate a MapReduce solution on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a7036-105">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="a7036-105">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a7036-106">Daha fazla bilgi için bkz: [Hdınsight bileşen sürümü oluşturma](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="a7036-106">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="a7036-107">Hadoop akış, bir komut dosyası veya yürütülebilir dosyası kullanan toorun MapReduce işleri sağlayan bir yardımcı programıdır.</span><span class="sxs-lookup"><span data-stu-id="a7036-107">Hadoop streaming is a utility that allows you toorun MapReduce jobs using a script or executable.</span></span> <span data-ttu-id="a7036-108">Bu örnekte, .NET kullanılan tooimplement hello Eşleyici ve word sayısı çözüm reducer ' dir.</span><span class="sxs-lookup"><span data-stu-id="a7036-108">In this example, .NET is used tooimplement hello mapper and reducer for a word count solution.</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="a7036-109">Hdınsight üzerinde .NET</span><span class="sxs-lookup"><span data-stu-id="a7036-109">.NET on HDInsight</span></span>

<span data-ttu-id="a7036-110">__Linux tabanlı Hdınsight__ kümeleri kullanım [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="a7036-110">__Linux-based HDInsight__ clusters use [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET applications.</span></span> <span data-ttu-id="a7036-111">Mono sürüm 4.2.1 Hdınsight sürüm 3.5 ile dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="a7036-111">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="a7036-112">Hdınsight ile dahil Mono hello sürümü hakkında daha fazla bilgi için bkz: [Hdınsight bileşen sürümü](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="a7036-112">For more information on hello version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="a7036-113">toouse Mono, belirli bir sürümünü görmek hello [yükleme veya güncelleştirme Mono](hdinsight-hadoop-install-mono.md) belge.</span><span class="sxs-lookup"><span data-stu-id="a7036-113">toouse a specific version of Mono, see hello [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="a7036-114">.NET Framework sürümleri Mono uyumluluğu hakkında daha fazla bilgi için bkz: [Mono Uyumluluk](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="a7036-114">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

## <a name="how-hadoop-streaming-works"></a><span data-ttu-id="a7036-115">Hadoop akış nasıl çalışır</span><span class="sxs-lookup"><span data-stu-id="a7036-115">How Hadoop streaming works</span></span>

<span data-ttu-id="a7036-116">Bu belgede akış için kullanılan Hello temel işlem aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="a7036-116">hello basic process used for streaming in this document is as follows:</span></span>

1. <span data-ttu-id="a7036-117">Hadoop veri toohello Eşleyici (Bu örnekte mapper.exe) üzerinde STDIN geçirir.</span><span class="sxs-lookup"><span data-stu-id="a7036-117">Hadoop passes data toohello mapper (mapper.exe in this example) on STDIN.</span></span>
2. <span data-ttu-id="a7036-118">Merhaba Eşleyici hello veri işler ve sekmeyle anahtar/değer çiftleri tooSTDOUT yayar.</span><span class="sxs-lookup"><span data-stu-id="a7036-118">hello mapper processes hello data, and emits tab-delimited key/value pairs tooSTDOUT.</span></span>
3. <span data-ttu-id="a7036-119">Merhaba çıktı tarafından Hadoop okuyun ve ardından toohello reducer (Bu örnekte reducer.exe) üzerinde STDIN geçirildi.</span><span class="sxs-lookup"><span data-stu-id="a7036-119">hello output is read by Hadoop, and then passed toohello reducer (reducer.exe in this example) on STDIN.</span></span>
4. <span data-ttu-id="a7036-120">Merhaba reducer sekmeyle hello anahtar/değer çiftleri okur, hello verileri işler ve STDOUT üzerinde sekmeyle anahtar/değer çiftleri olarak hello sonuç yayar.</span><span class="sxs-lookup"><span data-stu-id="a7036-120">hello reducer reads hello tab-delimited key/value pairs, processes hello data, and then emits hello result as tab-delimited key/value pairs on STDOUT.</span></span>
5. <span data-ttu-id="a7036-121">Merhaba çıktı Hadoop tarafından okunabilir ve toohello çıktı dizini yazılabilir.</span><span class="sxs-lookup"><span data-stu-id="a7036-121">hello output is read by Hadoop and written toohello output directory.</span></span>

<span data-ttu-id="a7036-122">Akış ile ilgili daha fazla bilgi için bkz: [Hadoop akış (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).</span><span class="sxs-lookup"><span data-stu-id="a7036-122">For more information on streaming, see [Hadoop Streaming (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a7036-123">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="a7036-123">Prerequisites</span></span>

* <span data-ttu-id="a7036-124">Yazma ve .NET Framework 4.5 hedefleyen C# kod oluşturma ile benzer.</span><span class="sxs-lookup"><span data-stu-id="a7036-124">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span> <span data-ttu-id="a7036-125">Merhaba, bu belgenin kullanımı Visual Studio 2017 adımları.</span><span class="sxs-lookup"><span data-stu-id="a7036-125">hello steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="a7036-126">Bir şekilde tooupload .exe dosyaları toohello kümesi.</span><span class="sxs-lookup"><span data-stu-id="a7036-126">A way tooupload .exe files toohello cluster.</span></span> <span data-ttu-id="a7036-127">Merhaba bu belgedeki adımları hello Data Lake araçları Visual Studio tooupload hello dosyaları tooprimary hello kümesi için kullanır.</span><span class="sxs-lookup"><span data-stu-id="a7036-127">hello steps in this document use hello Data Lake Tools for Visual Studio tooupload hello files tooprimary storage for hello cluster.</span></span>

* <span data-ttu-id="a7036-128">Azure PowerShell veya SSH istemcisi.</span><span class="sxs-lookup"><span data-stu-id="a7036-128">Azure PowerShell or a SSH client.</span></span>

* <span data-ttu-id="a7036-129">Hdınsight kümesi Hadoop'ta.</span><span class="sxs-lookup"><span data-stu-id="a7036-129">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="a7036-130">Küme oluşturma ile ilgili daha fazla bilgi için bkz: [bir Hdınsight kümesi oluşturmayı](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="a7036-130">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

## <a name="create-hello-mapper"></a><span data-ttu-id="a7036-131">Merhaba Eşleyici oluşturma</span><span class="sxs-lookup"><span data-stu-id="a7036-131">Create hello mapper</span></span>

<span data-ttu-id="a7036-132">Visual Studio'da yeni bir oluşturma __konsol uygulaması__ adlı __Eşleyici__.</span><span class="sxs-lookup"><span data-stu-id="a7036-132">In Visual Studio, create a new __Console application__ named __mapper__.</span></span> <span data-ttu-id="a7036-133">Merhaba uygulaması için kod aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="a7036-133">Use hello following code for hello application:</span></span>

```csharp
using System;
using System.Text.RegularExpressions;

namespace mapper
{
    class Program
    {
        static void Main(string[] args)
        {
            string line;
            //Hadoop passes data toohello mapper on STDIN
            while((line = Console.ReadLine()) != null)
            {
                // We only want words, so strip out punctuation, numbers, etc.
                var onlyText = Regex.Replace(line, @"\.|;|:|,|[0-9]|'", "");
                // Split at whitespace.
                var words = Regex.Matches(onlyText, @"[\w]+");
                // Loop over hello words
                foreach(var word in words)
                {
                    //Emit tab-delimited key/value pairs.
                    //In this case, a word and a count of 1.
                    Console.WriteLine("{0}\t1",word);
                }
            }
        }
    }
}
```

<span data-ttu-id="a7036-134">Merhaba uygulaması oluşturduktan sonra tooproduce hello yapı `/bin/Debug/mapper.exe` hello proje dizininde dosya.</span><span class="sxs-lookup"><span data-stu-id="a7036-134">After creating hello application, build it tooproduce hello `/bin/Debug/mapper.exe` file in hello project directory.</span></span>

## <a name="create-hello-reducer"></a><span data-ttu-id="a7036-135">Merhaba reducer oluşturma</span><span class="sxs-lookup"><span data-stu-id="a7036-135">Create hello reducer</span></span>

<span data-ttu-id="a7036-136">Visual Studio'da yeni bir oluşturma __konsol uygulaması__ adlı __reducer__.</span><span class="sxs-lookup"><span data-stu-id="a7036-136">In Visual Studio, create a new __Console application__ named __reducer__.</span></span> <span data-ttu-id="a7036-137">Merhaba uygulaması için kod aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="a7036-137">Use hello following code for hello application:</span></span>

```csharp
using System;
using System.Collections.Generic;

namespace reducer
{
    class Program
    {
        static void Main(string[] args)
        {
            //Dictionary for holding a count of words
            Dictionary<string, int> words = new Dictionary<string, int>();

            string line;
            //Read from STDIN
            while ((line = Console.ReadLine()) != null)
            {
                // Data from Hadoop is tab-delimited key/value pairs
                var sArr = line.Split('\t');
                // Get hello word
                string word = sArr[0];
                // Get hello count
                int count = Convert.ToInt32(sArr[1]);

                //Do we already have a count for hello word?
                if(words.ContainsKey(word))
                {
                    //If so, increment hello count
                    words[word] += count;
                } else
                {
                    //Add hello key toohello collection
                    words.Add(word, count);
                }
            }
            //Finally, emit each word and count
            foreach (var word in words)
            {
                //Emit tab-delimited key/value pairs.
                //In this case, a word and a count of 1.
                Console.WriteLine("{0}\t{1}", word.Key, word.Value);
            }
        }
    }
}
```

<span data-ttu-id="a7036-138">Merhaba uygulaması oluşturduktan sonra tooproduce hello yapı `/bin/Debug/reducer.exe` hello proje dizininde dosya.</span><span class="sxs-lookup"><span data-stu-id="a7036-138">After creating hello application, build it tooproduce hello `/bin/Debug/reducer.exe` file in hello project directory.</span></span>

## <a name="upload-toostorage"></a><span data-ttu-id="a7036-139">Toostorage karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="a7036-139">Upload toostorage</span></span>

1. <span data-ttu-id="a7036-140">Visual Studio'da açın **Sunucu Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="a7036-140">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="a7036-141">**Azure** seçeneğini ve sonra **HDInsight** seçeneğini genişletin.</span><span class="sxs-lookup"><span data-stu-id="a7036-141">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="a7036-142">İstenirse, Azure aboneliği kimlik bilgilerinizi girin ve ardından **oturum**.</span><span class="sxs-lookup"><span data-stu-id="a7036-142">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="a7036-143">Bu uygulamaya toodeploy istediğiniz hello Hdınsight kümesini genişletin.</span><span class="sxs-lookup"><span data-stu-id="a7036-143">Expand hello HDInsight cluster that you wish toodeploy this application to.</span></span> <span data-ttu-id="a7036-144">Bir giriş hello metinle __(varsayılan depolama hesabı)__ listelenir.</span><span class="sxs-lookup"><span data-stu-id="a7036-144">An entry with hello text __(Default Storage Account)__ is listed.</span></span>

    ![Sunucu Gezgini Hello hello küme için depolama hesabı gösterme](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="a7036-146">Bu girdi şekilde genişletilebilir, kullanmakta olduğunuz bir __Azure depolama hesabı__ hello küme için varsayılan depolama birimi olarak.</span><span class="sxs-lookup"><span data-stu-id="a7036-146">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for hello cluster.</span></span> <span data-ttu-id="a7036-147">Merhaba küme için hello varsayılan depolama tooview hello dosyaları hello girişini genişletin hello çift tıklayın ve ardından __(varsayılan kapsayıcı)__.</span><span class="sxs-lookup"><span data-stu-id="a7036-147">tooview hello files on hello default storage for hello cluster, expand hello entry and then double-click hello __(Default Container)__.</span></span>

    * <span data-ttu-id="a7036-148">Bu girdi genişletilemiyor, kullanmakta olduğunuz __Azure Data Lake Store__ hello küme için hello varsayılan depolama birimi olarak.</span><span class="sxs-lookup"><span data-stu-id="a7036-148">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as hello default storage for hello cluster.</span></span> <span data-ttu-id="a7036-149">Merhaba küme için hello varsayılan depolama tooview hello dosyaları çift hello __(varsayılan depolama hesabı)__ girişi.</span><span class="sxs-lookup"><span data-stu-id="a7036-149">tooview hello files on hello default storage for hello cluster, double-click hello __(Default Storage Account)__ entry.</span></span>

5. <span data-ttu-id="a7036-150">tooupload hello .exe dosyaları, yöntemler aşağıdaki hello birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="a7036-150">tooupload hello .exe files, use one of hello following methods:</span></span>

    * <span data-ttu-id="a7036-151">Kullanılıyorsa bir __Azure depolama hesabı__hello karşıya yükleme simgesine tıklayın ve ardından toohello Gözat **bin\debug** hello için klasör **Eşleyici** projesi.</span><span class="sxs-lookup"><span data-stu-id="a7036-151">If using an __Azure Storage Account__, click hello upload icon, and then browse toohello **bin\debug** folder for hello **mapper** project.</span></span> <span data-ttu-id="a7036-152">Son olarak, hello seçin **mapper.exe** dosya ve tıklayın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="a7036-152">Finally, select hello **mapper.exe** file and click **Ok**.</span></span>

        ![simgeyi karşıya yükleyin](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="a7036-154">Kullanıyorsanız __Azure Data Lake Store__hello dosya listesindeki boş bir alana sağ tıklayın ve ardından __karşıya__.</span><span class="sxs-lookup"><span data-stu-id="a7036-154">If using __Azure Data Lake Store__, right-click an empty area in hello file listing, and then select __Upload__.</span></span> <span data-ttu-id="a7036-155">Son olarak, hello seçin **mapper.exe** dosya ve tıklayın **açık**.</span><span class="sxs-lookup"><span data-stu-id="a7036-155">Finally, select hello **mapper.exe** file and click **Open**.</span></span>

    <span data-ttu-id="a7036-156">Bir kez hello __mapper.exe__ karşıya yükleme tamamlandı, yineleme hello karşıya yükleme işlemi hello için __reducer.exe__ dosya.</span><span class="sxs-lookup"><span data-stu-id="a7036-156">Once hello __mapper.exe__ upload has finished, repeat hello upload process for hello __reducer.exe__ file.</span></span>

## <a name="run-a-job-using-an-ssh-session"></a><span data-ttu-id="a7036-157">Bir işi çalıştırın: bir SSH oturumu kullanma</span><span class="sxs-lookup"><span data-stu-id="a7036-157">Run a job: Using an SSH session</span></span>

1. <span data-ttu-id="a7036-158">SSH tooconnect toohello Hdınsight kümesi kullanın.</span><span class="sxs-lookup"><span data-stu-id="a7036-158">Use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="a7036-159">Daha fazla bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="a7036-159">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="a7036-160">Komut toostart hello MapReduce işi aşağıdaki hello birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="a7036-160">Use one of hello following command toostart hello MapReduce job:</span></span>

    * <span data-ttu-id="a7036-161">Kullanıyorsanız __Data Lake Store__ varsayılan depolama olarak:</span><span class="sxs-lookup"><span data-stu-id="a7036-161">If using __Data Lake Store__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files adl:///mapper.exe,adl:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```
    
    * <span data-ttu-id="a7036-162">Kullanıyorsanız __Azure Storage__ varsayılan depolama olarak:</span><span class="sxs-lookup"><span data-stu-id="a7036-162">If using __Azure Storage__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files wasb:///mapper.exe,wasb:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```

    <span data-ttu-id="a7036-163">Her bir parametreyi yaptığı listesi aşağıdaki hello açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="a7036-163">hello following list describes what each parameter does:</span></span>

    * <span data-ttu-id="a7036-164">`hadoop-streaming.jar`: MapReduce işlevselliği akış hello içeren hello jar dosyasını.</span><span class="sxs-lookup"><span data-stu-id="a7036-164">`hadoop-streaming.jar`: hello jar file that contains hello streaming MapReduce functionality.</span></span>
    * <span data-ttu-id="a7036-165">`-files`: Ekler Merhaba `mapper.exe` ve `reducer.exe` dosyaları toothis işi.</span><span class="sxs-lookup"><span data-stu-id="a7036-165">`-files`: Adds hello `mapper.exe` and `reducer.exe` files toothis job.</span></span> <span data-ttu-id="a7036-166">Merhaba `adl:///` veya `wasb:///` her dosya hello yolu toohello hello kümesi için varsayılan depolama köküdür önce.</span><span class="sxs-lookup"><span data-stu-id="a7036-166">hello `adl:///` or `wasb:///` before each file is hello path toohello root of default storage for hello cluster.</span></span>
    * <span data-ttu-id="a7036-167">`-mapper`: Hello Eşleyici hangi dosya uygulayan belirtir.</span><span class="sxs-lookup"><span data-stu-id="a7036-167">`-mapper`: Specifies which file implements hello mapper.</span></span>
    * <span data-ttu-id="a7036-168">`-reducer`: Merhaba reducer hangi dosya uygulayan belirtir.</span><span class="sxs-lookup"><span data-stu-id="a7036-168">`-reducer`: Specifies which file implements hello reducer.</span></span>
    * <span data-ttu-id="a7036-169">`-input`: hello giriş verileri.</span><span class="sxs-lookup"><span data-stu-id="a7036-169">`-input`: hello input data.</span></span>
    * <span data-ttu-id="a7036-170">`-output`: hello çıktı dizini.</span><span class="sxs-lookup"><span data-stu-id="a7036-170">`-output`: hello output directory.</span></span>

3. <span data-ttu-id="a7036-171">Merhaba MapReduce işi tamamlandıktan sonra tooview hello sonuçları aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="a7036-171">Once hello MapReduce job completes, use hello following tooview hello results:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="a7036-172">Merhaba aşağıdaki metni, bu komutu tarafından döndürülen hello veri örneğidir:</span><span class="sxs-lookup"><span data-stu-id="a7036-172">hello following text is an example of hello data returned by this command:</span></span>

        you     1128
        young   38
        younger 1
        youngest        1
        your    338
        yours   4
        yourself        34
        yourselves      3
        youth   17

## <a name="run-a-job-using-powershell"></a><span data-ttu-id="a7036-173">Bir işi çalıştırın: PowerShell'i kullanma</span><span class="sxs-lookup"><span data-stu-id="a7036-173">Run a job: Using PowerShell</span></span>

<span data-ttu-id="a7036-174">PowerShell komut dosyası toorun bir MapReduce işi aşağıdaki hello kullanın ve hello sonuçları indirin.</span><span class="sxs-lookup"><span data-stu-id="a7036-174">Use hello following PowerShell script toorun a MapReduce job and download hello results.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]

<span data-ttu-id="a7036-175">Bu komut dosyası hello küme oturum açma hesabı adı ve parola, hello Hdınsight küme adı ile birlikte ister.</span><span class="sxs-lookup"><span data-stu-id="a7036-175">This script prompts you for hello cluster login account name and password, along with hello HDInsight cluster name.</span></span> <span data-ttu-id="a7036-176">Merhaba işi tamamlandıktan sonra indirilen toohello hello çıkış olduğu `output.txt` olan hello dizin hello betik dosyasında çalıştı.</span><span class="sxs-lookup"><span data-stu-id="a7036-176">Once hello job completes, hello output is downloaded toohello `output.txt` file in hello directory hello script is ran from.</span></span> <span data-ttu-id="a7036-177">Merhaba aşağıdaki metni hello hello verilerde örneğidir `output.txt` dosyası:</span><span class="sxs-lookup"><span data-stu-id="a7036-177">hello following text is an example of hello data in hello `output.txt` file:</span></span>

    you     1128
    young   38
    younger 1
    youngest        1
    your    338
    yours   4
    yourself        34
    yourselves      3
    youth   17

## <a name="next-steps"></a><span data-ttu-id="a7036-178">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="a7036-178">Next steps</span></span>

<span data-ttu-id="a7036-179">Hdınsight ile MapReduce kullanma hakkında daha fazla bilgi için bkz: [Hdınsight ile MapReduce kullanma](hdinsight-use-mapreduce.md).</span><span class="sxs-lookup"><span data-stu-id="a7036-179">For more information on using MapReduce with HDInsight, see [Use MapReduce with HDInsight](hdinsight-use-mapreduce.md).</span></span>

<span data-ttu-id="a7036-180">C# Hive veya Pig kullanma hakkında daha fazla bilgi için bkz: [C# kullanıcı tanımlı işlev Hive veya Pig kullanmak](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="a7036-180">For information on using C# with Hive and Pig, see [Use a C# user defined function with Hive and Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).</span></span>

<span data-ttu-id="a7036-181">C# Hdınsight üzerinde Storm ile kullanma hakkında daha fazla bilgi için bkz: [Hdınsight üzerinde Storm için C# topolojileri](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="a7036-181">For information on using C# with Storm on HDInsight, see [Develop C# topologies for Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>