---
title: "C# ile Hive veya Pig hdınsight'ta - Azure hadoop'ta aaaUse | Microsoft Docs"
description: "Bilgi nasıl toouse C# kullanıcı tanımlı işlevler (UDF) Hive veya Pig Azure Hdınsight'ta akış ile."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d83def76-12ad-4538-bb8e-3ba3542b7211
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: dd35409766f2dafe4d8050c3f9bc351949473ad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-user-defined-functions-with-hive-and-pig-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="89c9b-103">C# kullanıcı tanımlı işlevler Hive veya Pig hdınsight'ta Hadoop akış ile kullanma</span><span class="sxs-lookup"><span data-stu-id="89c9b-103">Use C# user-defined functions with Hive and Pig streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="89c9b-104">Nasıl toouse C# kullanıcı Hdınsight üzerinde Apache Hive ve Pig işlevleri (UDF) tanımlanan öğrenin.</span><span class="sxs-lookup"><span data-stu-id="89c9b-104">Learn how toouse C# user defined functions (UDF) with Apache Hive and Pig on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="89c9b-105">Bu belgedeki Hello adımlar Linux tabanlı hem de Windows tabanlı Hdınsight kümeleri ile çalışır.</span><span class="sxs-lookup"><span data-stu-id="89c9b-105">hello steps in this document work with both Linux-based and Windows-based HDInsight clusters.</span></span> <span data-ttu-id="89c9b-106">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="89c9b-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="89c9b-107">Daha fazla bilgi için bkz: [Hdınsight bileşen sürümü oluşturma](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="89c9b-107">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="89c9b-108">Her ikisi de Hive ve Pig veri tooexternal uygulamaları işlemek için geçirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89c9b-108">Both Hive and Pig can pass data tooexternal applications for processing.</span></span> <span data-ttu-id="89c9b-109">Bu işlem olarak bilinir _akış_.</span><span class="sxs-lookup"><span data-stu-id="89c9b-109">This process is known as _streaming_.</span></span> <span data-ttu-id="89c9b-110">.NET applciation kullanırken hello veri üzerinde STDIN toohello uygulama geçirilen ve Merhaba uygulaması STDOUT üzerinde hello sonuçları döndürür.</span><span class="sxs-lookup"><span data-stu-id="89c9b-110">When using a .NET applciation, hello data is passed toohello application on STDIN, and hello application returns hello results on STDOUT.</span></span> <span data-ttu-id="89c9b-111">tooread ve STDIN ve STDOUT yazma, kullanabileceğiniz `Console.ReadLine()` ve `Console.WriteLine()` bir konsol uygulamasından.</span><span class="sxs-lookup"><span data-stu-id="89c9b-111">tooread and write from STDIN and STDOUT, you can use `Console.ReadLine()` and `Console.WriteLine()` from a console application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89c9b-112">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="89c9b-112">Prerequisites</span></span>

* <span data-ttu-id="89c9b-113">Yazma ve .NET Framework 4.5 hedefleyen C# kod oluşturma ile benzer.</span><span class="sxs-lookup"><span data-stu-id="89c9b-113">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span>

    * <span data-ttu-id="89c9b-114">İstediğiniz ne olursa olsun IDE kullanın.</span><span class="sxs-lookup"><span data-stu-id="89c9b-114">Use whatever IDE you want.</span></span> <span data-ttu-id="89c9b-115">Öneririz [Visual Studio](https://www.visualstudio.com/vs) 2015, 2017, veya [Visual Studio Code](https://code.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="89c9b-115">We recommend [Visual Studio](https://www.visualstudio.com/vs) 2015, 2017, or [Visual Studio Code](https://code.visualstudio.com/).</span></span> <span data-ttu-id="89c9b-116">Merhaba, bu belgenin kullanımı Visual Studio 2017 adımları.</span><span class="sxs-lookup"><span data-stu-id="89c9b-116">hello steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="89c9b-117">Bir şekilde tooupload .exe dosyalarını toohello küme ve çalışma Pig ve Hive işleri.</span><span class="sxs-lookup"><span data-stu-id="89c9b-117">A way tooupload .exe files toohello cluster and run Pig and Hive jobs.</span></span> <span data-ttu-id="89c9b-118">Merhaba Data Lake araçları Visual Studio, Azure PowerShell ve Azure CLI için öneririz.</span><span class="sxs-lookup"><span data-stu-id="89c9b-118">We recommend hello Data Lake Tools for Visual Studio, Azure PowerShell and Azure CLI.</span></span> <span data-ttu-id="89c9b-119">Merhaba bu belgedeki adımları hello Data Lake araçları Visual Studio tooupload hello dosyaları için kullanan ve hello örnek Hive sorgusu çalıştırmak.</span><span class="sxs-lookup"><span data-stu-id="89c9b-119">hello steps in this document use hello Data Lake Tools for Visual Studio tooupload hello files and run hello example Hive query.</span></span>

    <span data-ttu-id="89c9b-120">Diğer yolları toorun Hive sorguları ve Pig işleri hakkında daha fazla bilgi için aşağıdaki belgeleri hello bakın:</span><span class="sxs-lookup"><span data-stu-id="89c9b-120">For information on other ways toorun Hive queries and Pig jobs, see hello following documents:</span></span>

    * [<span data-ttu-id="89c9b-121">Apache Hive Hdınsight ile kullanma</span><span class="sxs-lookup"><span data-stu-id="89c9b-121">Use Apache Hive with HDInsight</span></span>](hdinsight-use-hive.md)

    * [<span data-ttu-id="89c9b-122">Hdınsight ile Apache Pig kullanma</span><span class="sxs-lookup"><span data-stu-id="89c9b-122">Use Apache Pig with HDInsight</span></span>](hdinsight-use-pig.md)

* <span data-ttu-id="89c9b-123">Hdınsight kümesi Hadoop'ta.</span><span class="sxs-lookup"><span data-stu-id="89c9b-123">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="89c9b-124">Küme oluşturma ile ilgili daha fazla bilgi için bkz: [bir Hdınsight kümesi oluşturmayı](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="89c9b-124">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="89c9b-125">Hdınsight üzerinde .NET</span><span class="sxs-lookup"><span data-stu-id="89c9b-125">.NET on HDInsight</span></span>

* <span data-ttu-id="89c9b-126">__Linux tabanlı Hdınsight__ kullanarak kümeleri [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET uygulamaları.</span><span class="sxs-lookup"><span data-stu-id="89c9b-126">__Linux-based HDInsight__ clusters using [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET applications.</span></span> <span data-ttu-id="89c9b-127">Mono sürüm 4.2.1 Hdınsight sürüm 3.5 ile dahil edilir.</span><span class="sxs-lookup"><span data-stu-id="89c9b-127">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span>

    <span data-ttu-id="89c9b-128">.NET Framework sürümleri Mono uyumluluğu hakkında daha fazla bilgi için bkz: [Mono Uyumluluk](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="89c9b-128">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

    <span data-ttu-id="89c9b-129">toouse Mono, belirli bir sürümünü görmek hello [yükleme veya güncelleştirme Mono](hdinsight-hadoop-install-mono.md) belge.</span><span class="sxs-lookup"><span data-stu-id="89c9b-129">toouse a specific version of Mono, see hello [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

* <span data-ttu-id="89c9b-130">__Windows tabanlı Hdınsight__ kümeleri hello Microsoft .NET CLR toorun .NET uygulamalarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="89c9b-130">__Windows-based HDInsight__ clusters use hello Microsoft .NET CLR toorun .NET applications.</span></span>

<span data-ttu-id="89c9b-131">Merhaba .NET framework ve Hdınsight sürümleriyle dahil Mono hello sürümü hakkında daha fazla bilgi için bkz: [Hdınsight bileşen sürümü](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="89c9b-131">For more information on hello version of hello .NET framework and Mono included with HDInsight versions, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span>

## <a name="create-hello-c-projects"></a><span data-ttu-id="89c9b-132">Merhaba C oluşturmak\# projeleri</span><span class="sxs-lookup"><span data-stu-id="89c9b-132">Create hello C\# projects</span></span>

### <a name="hive-udf"></a><span data-ttu-id="89c9b-133">UDF yığını</span><span class="sxs-lookup"><span data-stu-id="89c9b-133">Hive UDF</span></span>

1. <span data-ttu-id="89c9b-134">Visual Studio'yu açın ve bir çözüm oluşturun.</span><span class="sxs-lookup"><span data-stu-id="89c9b-134">Open Visual Studio and create a solution.</span></span> <span data-ttu-id="89c9b-135">Merhaba proje türü için **konsol uygulaması (.NET Framework)**ve ad hello yeni proje **HiveCSharp**.</span><span class="sxs-lookup"><span data-stu-id="89c9b-135">For hello project type, select **Console App (.NET Framework)**, and name hello new project **HiveCSharp**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="89c9b-136">Seçin __.NET Framework 4.5__ Linux tabanlı Hdınsight kümesi kullanıyorsanız.</span><span class="sxs-lookup"><span data-stu-id="89c9b-136">Select __.NET Framework 4.5__ if you are using a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="89c9b-137">.NET Framework sürümleri Mono uyumluluğu hakkında daha fazla bilgi için bkz: [Mono Uyumluluk](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="89c9b-137">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

2. <span data-ttu-id="89c9b-138">Merhaba Değiştir **Program.cs** hello aşağıdaki ile:</span><span class="sxs-lookup"><span data-stu-id="89c9b-138">Replace hello contents of **Program.cs** with hello following:</span></span>

    ```csharp
    using System;
    using System.Security.Cryptography;
    using System.Text;
    using System.Threading.Tasks;

    namespace HiveCSharp
    {
        class Program
        {
            static void Main(string[] args)
            {
                string line;
                // Read stdin in a loop
                while ((line = Console.ReadLine()) != null)
                {
                    // Parse hello string, trimming line feeds
                    // and splitting fields at tabs
                    line = line.TrimEnd('\n');
                    string[] field = line.Split('\t');
                    string phoneLabel = field[1] + ' ' + field[2];
                    // Emit new data toostdout, delimited by tabs
                    Console.WriteLine("{0}\t{1}\t{2}", field[0], phoneLabel, GetMD5Hash(phoneLabel));
                }
            }
            /// <summary>
            /// Returns an MD5 hash for hello given string
            /// </summary>
            /// <param name="input">string value</param>
            /// <returns>an MD5 hash</returns>
            static string GetMD5Hash(string input)
            {
                // Step 1, calculate MD5 hash from input
                MD5 md5 = System.Security.Cryptography.MD5.Create();
                byte[] inputBytes = System.Text.Encoding.ASCII.GetBytes(input);
                byte[] hash = md5.ComputeHash(inputBytes);

                // Step 2, convert byte array toohex string
                StringBuilder sb = new StringBuilder();
                for (int i = 0; i < hash.Length; i++)
                {
                    sb.Append(hash[i].ToString("x2"));
                }
                return sb.ToString();
            }
        }
    }
    ```

3. <span data-ttu-id="89c9b-139">Merhaba projeyi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="89c9b-139">Build hello project.</span></span>

### <a name="pig-udf"></a><span data-ttu-id="89c9b-140">Pig UDF</span><span class="sxs-lookup"><span data-stu-id="89c9b-140">Pig UDF</span></span>

1. <span data-ttu-id="89c9b-141">Visual Studio'yu açın ve bir çözüm oluşturun.</span><span class="sxs-lookup"><span data-stu-id="89c9b-141">Open Visual Studio and create a solution.</span></span> <span data-ttu-id="89c9b-142">Merhaba proje türü için **konsol uygulaması**ve ad hello yeni proje **PigUDF**.</span><span class="sxs-lookup"><span data-stu-id="89c9b-142">For hello project type, select **Console Application**, and name hello new project **PigUDF**.</span></span>

2. <span data-ttu-id="89c9b-143">Merhaba Hello içeriğini değiştirin **Program.cs** koddan hello dosyasıyla:</span><span class="sxs-lookup"><span data-stu-id="89c9b-143">Replace hello contents of hello **Program.cs** file with hello following code:</span></span>

    ```csharp
    using System;

    namespace PigUDF
    {
        class Program
        {
            static void Main(string[] args)
            {
                string line;
                // Read stdin in a loop
                while ((line = Console.ReadLine()) != null)
                {
                    // Fix formatting on lines that begin with an exception
                    if(line.StartsWith("java.lang.Exception"))
                    {
                        // Trim hello error info off hello beginning and add a note toohello end of hello line
                        line = line.Remove(0, 21) + " - java.lang.Exception";
                    }
                    // Split hello fields apart at tab characters
                    string[] field = line.Split('\t');
                    // Put fields back together for writing
                    Console.WriteLine(String.Join("\t",field));
                }
            }
        }
    }
    ```

    <span data-ttu-id="89c9b-144">Bu uygulama Pig gönderilen hello satırları ve ile başlayan yeniden biçimlendirme satırları ayrıştırır `java.lang.Exception`.</span><span class="sxs-lookup"><span data-stu-id="89c9b-144">This application parses hello lines sent from Pig, and reformat lines that begin with `java.lang.Exception`.</span></span>

3. <span data-ttu-id="89c9b-145">Kaydet **Program.cs**ve ardından Merhaba projeyi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="89c9b-145">Save **Program.cs**, and then build hello project.</span></span>

## <a name="upload-toostorage"></a><span data-ttu-id="89c9b-146">Toostorage karşıya yükle</span><span class="sxs-lookup"><span data-stu-id="89c9b-146">Upload toostorage</span></span>

1. <span data-ttu-id="89c9b-147">Visual Studio'da açın **Sunucu Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="89c9b-147">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="89c9b-148">**Azure** seçeneğini ve sonra **HDInsight** seçeneğini genişletin.</span><span class="sxs-lookup"><span data-stu-id="89c9b-148">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="89c9b-149">İstenirse, Azure aboneliği kimlik bilgilerinizi girin ve ardından **oturum**.</span><span class="sxs-lookup"><span data-stu-id="89c9b-149">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="89c9b-150">Bu uygulamaya toodeploy istediğiniz hello Hdınsight kümesini genişletin.</span><span class="sxs-lookup"><span data-stu-id="89c9b-150">Expand hello HDInsight cluster that you wish toodeploy this application to.</span></span> <span data-ttu-id="89c9b-151">Bir giriş hello metinle __(varsayılan depolama hesabı)__ listelenir.</span><span class="sxs-lookup"><span data-stu-id="89c9b-151">An entry with hello text __(Default Storage Account)__ is listed.</span></span>

    ![Sunucu Gezgini Hello hello küme için depolama hesabı gösterme](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="89c9b-153">Bu girdi şekilde genişletilebilir, kullanmakta olduğunuz bir __Azure depolama hesabı__ hello küme için varsayılan depolama birimi olarak.</span><span class="sxs-lookup"><span data-stu-id="89c9b-153">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for hello cluster.</span></span> <span data-ttu-id="89c9b-154">Merhaba küme için hello varsayılan depolama tooview hello dosyaları hello girişini genişletin hello çift tıklayın ve ardından __(varsayılan kapsayıcı)__.</span><span class="sxs-lookup"><span data-stu-id="89c9b-154">tooview hello files on hello default storage for hello cluster, expand hello entry and then double-click hello __(Default Container)__.</span></span>

    * <span data-ttu-id="89c9b-155">Bu girdi genişletilemiyor, kullanmakta olduğunuz __Azure Data Lake Store__ hello küme için hello varsayılan depolama birimi olarak.</span><span class="sxs-lookup"><span data-stu-id="89c9b-155">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as hello default storage for hello cluster.</span></span> <span data-ttu-id="89c9b-156">Merhaba küme için hello varsayılan depolama tooview hello dosyaları çift hello __(varsayılan depolama hesabı)__ girişi.</span><span class="sxs-lookup"><span data-stu-id="89c9b-156">tooview hello files on hello default storage for hello cluster, double-click hello __(Default Storage Account)__ entry.</span></span>

6. <span data-ttu-id="89c9b-157">tooupload hello .exe dosyaları, yöntemler aşağıdaki hello birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="89c9b-157">tooupload hello .exe files, use one of hello following methods:</span></span>

    * <span data-ttu-id="89c9b-158">Kullanılıyorsa bir __Azure depolama hesabı__hello karşıya yükleme simgesine tıklayın ve ardından toohello Gözat **bin\debug** hello için klasör **HiveCSharp** projesi.</span><span class="sxs-lookup"><span data-stu-id="89c9b-158">If using an __Azure Storage Account__, click hello upload icon, and then browse toohello **bin\debug** folder for hello **HiveCSharp** project.</span></span> <span data-ttu-id="89c9b-159">Son olarak, hello seçin **HiveCSharp.exe** dosya ve tıklayın **Tamam**.</span><span class="sxs-lookup"><span data-stu-id="89c9b-159">Finally, select hello **HiveCSharp.exe** file and click **Ok**.</span></span>

        ![simgeyi karşıya yükleyin](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="89c9b-161">Kullanıyorsanız __Azure Data Lake Store__hello dosya listesindeki boş bir alana sağ tıklayın ve ardından __karşıya__.</span><span class="sxs-lookup"><span data-stu-id="89c9b-161">If using __Azure Data Lake Store__, right-click an empty area in hello file listing, and then select __Upload__.</span></span> <span data-ttu-id="89c9b-162">Son olarak, hello seçin **HiveCSharp.exe** dosya ve tıklayın **açık**.</span><span class="sxs-lookup"><span data-stu-id="89c9b-162">Finally, select hello **HiveCSharp.exe** file and click **Open**.</span></span>

    <span data-ttu-id="89c9b-163">Bir kez hello __HiveCSharp.exe__ karşıya yükleme tamamlandı, yineleme hello karşıya yükleme işlemi hello için __PigUDF.exe__ dosya.</span><span class="sxs-lookup"><span data-stu-id="89c9b-163">Once hello __HiveCSharp.exe__ upload has finished, repeat hello upload process for hello __PigUDF.exe__ file.</span></span>

## <a name="run-a-hive-query"></a><span data-ttu-id="89c9b-164">Hive sorgusu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="89c9b-164">Run a Hive query</span></span>

1. <span data-ttu-id="89c9b-165">Visual Studio'da açın **Sunucu Gezgini**.</span><span class="sxs-lookup"><span data-stu-id="89c9b-165">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="89c9b-166">**Azure** seçeneğini ve sonra **HDInsight** seçeneğini genişletin.</span><span class="sxs-lookup"><span data-stu-id="89c9b-166">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="89c9b-167">Merhaba dağıtılan sağ hello küme **HiveCSharp** için uygulama ve ardından **Hive sorgusu yaz**.</span><span class="sxs-lookup"><span data-stu-id="89c9b-167">Right-click hello cluster that you deployed hello **HiveCSharp** application to, and then select **Write a Hive Query**.</span></span>

4. <span data-ttu-id="89c9b-168">Metin hello Hive sorgusu için aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="89c9b-168">Use hello following text for hello Hive query:</span></span>

    ```hiveql
    -- Uncomment hello following if you are using Azure Storage
    -- add file wasb:///HiveCSharp.exe;
    -- Uncomment hello following if you are using Azure Data Lake Store
    -- add file adl:///HiveCSharp.exe;

    SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'HiveCSharp.exe' AS
    (clientid string, phoneLabel string, phoneHash string)
    FROM hivesampletable
    ORDER BY clientid LIMIT 50;
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="89c9b-169">Merhaba açıklamadan çıkarın `add file` kümeniz için kullanılan varsayılan depolama hello türüyle eşleşen deyimi.</span><span class="sxs-lookup"><span data-stu-id="89c9b-169">Uncomment hello `add file` statement that matches hello type of default storage used for your cluster.</span></span>

    <span data-ttu-id="89c9b-170">Bu sorgu hello seçer `clientid`, `devicemake`, ve `devicemodel` alanlarını `hivesampletable`ve toohello HiveCSharp.exe uygulama hello alanları geçirir.</span><span class="sxs-lookup"><span data-stu-id="89c9b-170">This query selects hello `clientid`, `devicemake`, and `devicemodel` fields from `hivesampletable`, and passes hello fields toohello HiveCSharp.exe application.</span></span> <span data-ttu-id="89c9b-171">Merhaba sorgu bekliyor olarak depolanan hello uygulama tooreturn üç alanları, `clientid`, `phoneLabel`, ve `phoneHash`.</span><span class="sxs-lookup"><span data-stu-id="89c9b-171">hello query expects hello application tooreturn three fields, which are stored as `clientid`, `phoneLabel`, and `phoneHash`.</span></span> <span data-ttu-id="89c9b-172">Merhaba sorgu de toofind HiveCSharp.exe hello kök hello varsayılan storage kapsayıcısının bekliyor.</span><span class="sxs-lookup"><span data-stu-id="89c9b-172">hello query also expects toofind HiveCSharp.exe in hello root of hello default storage container.</span></span>

5. <span data-ttu-id="89c9b-173">Tıklatın **gönderme** toosubmit hello iş toohello Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="89c9b-173">Click **Submit** toosubmit hello job toohello HDInsight cluster.</span></span> <span data-ttu-id="89c9b-174">Merhaba **Hive işi Özet** penceresi açılır.</span><span class="sxs-lookup"><span data-stu-id="89c9b-174">hello **Hive Job Summary** window opens.</span></span>

6. <span data-ttu-id="89c9b-175">Tıklatın **yenileme** toorefresh hello kadar Özet **iş durumu** çok değiştirir**tamamlandı**.</span><span class="sxs-lookup"><span data-stu-id="89c9b-175">Click **Refresh** toorefresh hello summary until **Job Status** changes too**Completed**.</span></span> <span data-ttu-id="89c9b-176">tooview hello iş çıktısı, tıklatın **iş çıktısı**.</span><span class="sxs-lookup"><span data-stu-id="89c9b-176">tooview hello job output, click **Job Output**.</span></span>

## <a name="run-a-pig-job"></a><span data-ttu-id="89c9b-177">Pig işi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="89c9b-177">Run a Pig job</span></span>

1. <span data-ttu-id="89c9b-178">Yöntemleri tooconnect tooyour Hdınsight kümesi aşağıdaki hello birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="89c9b-178">Use one of hello following methods tooconnect tooyour HDInsight cluster:</span></span>

    * <span data-ttu-id="89c9b-179">Kullanıyorsanız bir __Linux tabanlı__ Hdınsight küme, SSH kullanın.</span><span class="sxs-lookup"><span data-stu-id="89c9b-179">If you are using a __Linux-based__ HDInsight cluster, use SSH.</span></span> <span data-ttu-id="89c9b-180">Örneğin, `ssh sshuser@mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="89c9b-180">For example, `ssh sshuser@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="89c9b-181">Daha fazla bilgi için bkz: [SSH kullanma withHDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="89c9b-181">For more information, see [Use SSH withHDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>
    
    * <span data-ttu-id="89c9b-182">Kullanıyorsanız bir __Windows tabanlı__ Hdınsight kümesi [Uzak Masaüstü kullanarak bağlan toohello küme](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="89c9b-182">If you are using a __Windows-based__ HDInsight cluster, [Connect toohello cluster using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>

2. <span data-ttu-id="89c9b-183">Komut toostart hello Pig komut satırı izleyen bir hello kullan:</span><span class="sxs-lookup"><span data-stu-id="89c9b-183">Use one hello following command toostart hello Pig command line:</span></span>

        pig

    > [!IMPORTANT]
    > <span data-ttu-id="89c9b-184">Windows tabanlı bir küme kullanıyorsanız, komutları bunun yerine aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="89c9b-184">If you are using a Windows-based cluster, use hello following commands instead:</span></span>
    > ```
    > cd %PIG_HOME%
    > bin\pig
    > ```

    <span data-ttu-id="89c9b-185">A `grunt>` komut istemi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="89c9b-185">A `grunt>` prompt is displayed.</span></span>

3. <span data-ttu-id="89c9b-186">Toorun hello .NET Framework uygulama kullanan bir Pig işi aşağıdaki hello girin:</span><span class="sxs-lookup"><span data-stu-id="89c9b-186">Enter hello following toorun a Pig job that uses hello .NET Framework application:</span></span>

        DEFINE streamer `PigUDF.exe` CACHE('/PigUDF.exe');
        LOGS = LOAD '/example/data/sample.log' as (LINE:chararray);
        LOG = FILTER LOGS by LINE is not null;
        DETAILS = STREAM LOG through streamer as (col1, col2, col3, col4, col5);
        DUMP DETAILS;

    <span data-ttu-id="89c9b-187">Merhaba `DEFINE` deyimi bir diğer ad oluşturur `streamer` hello pigudf.exe uygulamalar için ve `CACHE` hello kümenin varsayılan depolama biriminden yükler.</span><span class="sxs-lookup"><span data-stu-id="89c9b-187">hello `DEFINE` statement creates an alias of `streamer` for hello pigudf.exe applications, and `CACHE` loads it from default storage for hello cluster.</span></span> <span data-ttu-id="89c9b-188">Daha sonra `streamer` hello ile kullanılan `STREAM` işleci tooprocess hello günlük ve dönüş hello veri sütunları bir dizi olarak bulunan tek satır.</span><span class="sxs-lookup"><span data-stu-id="89c9b-188">Later, `streamer` is used with hello `STREAM` operator tooprocess hello single lines contained in LOG and return hello data as a series of columns.</span></span>

    > [!NOTE]
    > <span data-ttu-id="89c9b-189">Merhaba tarafından akış için kullanılan hello uygulama adı çevrelenen \` (backtick) ne zaman karakter diğer adı, ve ' (tek tırnak) ile kullanıldığında `SHIP\`.</span><span class="sxs-lookup"><span data-stu-id="89c9b-189">hello application name that is used for streaming must be surrounded by hello \` (backtick) character when aliased, and ' (single quote) when used with `SHIP\`.</span></span>

4. <span data-ttu-id="89c9b-190">Merhaba son satırı girdikten sonra hello iş başlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="89c9b-190">After entering hello last line, hello job should start.</span></span> <span data-ttu-id="89c9b-191">Metin aşağıdaki çıktı benzer toohello döndürür:</span><span class="sxs-lookup"><span data-stu-id="89c9b-191">It returns output similar toohello following text:</span></span>

        (2012-02-03 20:11:56 SampleClass5 [WARN] problem finding id 1358451042 - java.lang.Exception)
        (2012-02-03 20:11:56 SampleClass5 [DEBUG] detail for id 1976092771)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1317358561)
        (2012-02-03 20:11:56 SampleClass5 [TRACE] verbose detail for id 1737534798)
        (2012-02-03 20:11:56 SampleClass7 [DEBUG] detail for id 1475865947)

## <a name="next-steps"></a><span data-ttu-id="89c9b-192">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="89c9b-192">Next steps</span></span>

<span data-ttu-id="89c9b-193">Bu belgede, öğrendiğiniz nasıl toouse bir .NET Framework uygulamasından Hive veya Pig hdınsight'ta.</span><span class="sxs-lookup"><span data-stu-id="89c9b-193">In this document, you have learned how toouse a .NET Framework application from Hive and Pig on HDInsight.</span></span> <span data-ttu-id="89c9b-194">Toolearn nasıl toouse Hive veya Pig, ile Python görmek isterseniz [kullanım Python Hive veya Pig hdınsight'ta ile](hdinsight-python.md).</span><span class="sxs-lookup"><span data-stu-id="89c9b-194">If you would like toolearn how toouse Python with Hive and Pig, see [Use Python with Hive and Pig in HDInsight](hdinsight-python.md).</span></span>

<span data-ttu-id="89c9b-195">Diğer yolları toouse Pig ve Hive ve MapReduce kullanma hakkında toolearn için belgeler aşağıdaki hello bakın:</span><span class="sxs-lookup"><span data-stu-id="89c9b-195">For other ways toouse Pig and Hive, and toolearn about using MapReduce, see hello following documents:</span></span>

* [<span data-ttu-id="89c9b-196">HDInsight ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="89c9b-196">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="89c9b-197">HDInsight ile Pig kullanma</span><span class="sxs-lookup"><span data-stu-id="89c9b-197">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="89c9b-198">Hdınsight ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="89c9b-198">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
