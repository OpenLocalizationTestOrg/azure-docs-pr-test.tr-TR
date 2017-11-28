---
title: "aaaRun Apache Pig işleri .NET SDK'sı ile Hadoop - Azure Hdınsight | Microsoft Docs"
description: "Nasıl toouse hello .NET SDK'sı için hdınsight'ta Hadoop toosubmit Pig işleri tooHadoop öğrenin."
services: hdinsight
documentationcenter: .net
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: fa11d49a-328c-47e7-b16d-e7ed2a453195
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 1d4ceebd7c168372d23fe29a088f04676686de30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-using-hello-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="7a54b-103">Pig işleri için hdınsight'ta Hadoop Hello .NET SDK kullanarak çalıştırma</span><span class="sxs-lookup"><span data-stu-id="7a54b-103">Run Pig jobs using hello .NET SDK for Hadoop in HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="7a54b-104">TooHadoop Azure hdınsight'ta Hadoop toosubmit Apache Pig toouse Merhaba .NET SDK'sı nasıl işler öğrenin.</span><span class="sxs-lookup"><span data-stu-id="7a54b-104">Learn how toouse hello .NET SDK for Hadoop toosubmit Apache Pig jobs tooHadoop on Azure HDInsight.</span></span>

<span data-ttu-id="7a54b-105">Merhaba Hdınsight .NET SDK'sı .NET gelen Hdınsight kümeleri ile daha kolay toowork kolaylaştırır .NET istemci kitaplıkları sağlar.</span><span class="sxs-lookup"><span data-stu-id="7a54b-105">hello HDInsight .NET SDK provides .NET client libraries that makes it easier toowork with HDInsight clusters from .NET.</span></span> <span data-ttu-id="7a54b-106">Pig veri dönüşümleri bir dizi modelleme tarafından toocreate MapReduce işlemler sağlar.</span><span class="sxs-lookup"><span data-stu-id="7a54b-106">Pig allows you toocreate MapReduce operations by modeling a series of data transformations.</span></span> <span data-ttu-id="7a54b-107">Bu belgede nasıl toouse temel C# uygulama toosubmit bir Pig proje tooan Hdınsight kümesi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="7a54b-107">In this document, you learn how toouse a basic C# application toosubmit a Pig job tooan HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a54b-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7a54b-108">Prerequisites</span></span>

<span data-ttu-id="7a54b-109">Bu makaledeki toocomplete hello adımları, hello aşağıdaki gerekir.</span><span class="sxs-lookup"><span data-stu-id="7a54b-109">toocomplete hello steps in this article, you need hello following.</span></span>

* <span data-ttu-id="7a54b-110">Azure Hdınsight (Hadoop hdınsight) kümesi (ya da Windows veya Linux tabanlı).</span><span class="sxs-lookup"><span data-stu-id="7a54b-110">An Azure HDInsight (Hadoop on HDInsight) cluster (either Windows or Linux-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="7a54b-111">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="7a54b-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7a54b-112">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="7a54b-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="7a54b-113">Visual Studio 2012 2013, 2015 veya 2017.</span><span class="sxs-lookup"><span data-stu-id="7a54b-113">Visual Studio 2012, 2013, 2015 or 2017.</span></span>

## <a name="create-hello-application"></a><span data-ttu-id="7a54b-114">Merhaba uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="7a54b-114">Create hello application</span></span>

<span data-ttu-id="7a54b-115">Merhaba Hdınsight .NET SDK'sı .NET istemci kitaplıkları, .NET gelen Hdınsight kümeleri ile daha kolay toowork olmasını sağlayan sağlar.</span><span class="sxs-lookup"><span data-stu-id="7a54b-115">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span>

1. <span data-ttu-id="7a54b-116">Merhaba gelen **dosya** menü Visual Studio'da seçin **yeni** ve ardından **proje**.</span><span class="sxs-lookup"><span data-stu-id="7a54b-116">From hello **File** menu in Visual Studio, select **New** and then select **Project**.</span></span>

2. <span data-ttu-id="7a54b-117">Hello yeni proje için değerleri yazın veya aşağıdaki select hello:</span><span class="sxs-lookup"><span data-stu-id="7a54b-117">For hello new project, type or select hello following values:</span></span>

   | <span data-ttu-id="7a54b-118">Özellik</span><span class="sxs-lookup"><span data-stu-id="7a54b-118">Property</span></span> | <span data-ttu-id="7a54b-119">Değer</span><span class="sxs-lookup"><span data-stu-id="7a54b-119">Value</span></span> |
   | ------ | ------ |
   | <span data-ttu-id="7a54b-120">Kategori</span><span class="sxs-lookup"><span data-stu-id="7a54b-120">Category</span></span> | <span data-ttu-id="7a54b-121">Şablonlar/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="7a54b-121">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="7a54b-122">Şablon</span><span class="sxs-lookup"><span data-stu-id="7a54b-122">Template</span></span> | <span data-ttu-id="7a54b-123">Konsol Uygulaması</span><span class="sxs-lookup"><span data-stu-id="7a54b-123">Console Application</span></span> |
   | <span data-ttu-id="7a54b-124">Ad</span><span class="sxs-lookup"><span data-stu-id="7a54b-124">Name</span></span> | <span data-ttu-id="7a54b-125">SubmitPigJob</span><span class="sxs-lookup"><span data-stu-id="7a54b-125">SubmitPigJob</span></span> |

3. <span data-ttu-id="7a54b-126">Tıklatın **Tamam** toocreate hello projesi.</span><span class="sxs-lookup"><span data-stu-id="7a54b-126">Click **OK** toocreate hello project.</span></span>

4. <span data-ttu-id="7a54b-127">Merhaba gelen **Araçları** menüsünde, select **kitaplık Paket Yöneticisi** veya **Nuget Paket Yöneticisi**ve ardından **Paket Yöneticisi Konsolu**.</span><span class="sxs-lookup"><span data-stu-id="7a54b-127">From hello **Tools** menu, select **Library Package Manager** or **Nuget Package Manager**, and then select **Package Manager Console**.</span></span>

5. <span data-ttu-id="7a54b-128">tooinstall hello .NET SDK'sı paketleri, komutu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="7a54b-128">tooinstall hello .NET SDK packages, use hello following command:</span></span>

        Install-Package Microsoft.Azure.Management.HDInsight.Job

6. <span data-ttu-id="7a54b-129">Çözüm Gezgini'nde, çift **Program.cs** tooopen onu.</span><span class="sxs-lookup"><span data-stu-id="7a54b-129">From Solution Explorer, double-click **Program.cs** tooopen it.</span></span> <span data-ttu-id="7a54b-130">Merhaba var olan kodu hello şununla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="7a54b-130">Replace hello existing code with hello following.</span></span>

    ```csharp
    using Microsoft.Azure.Management.HDInsight.Job;
    using Microsoft.Azure.Management.HDInsight.Job.Models;
    using Hyak.Common;

    namespace SubmitHDInsightJobDotNet
    {
        class Program
        {
            private static HDInsightJobManagementClient _hdiJobManagementClient;

            private const string ExistingClusterName = "<Your HDInsight Cluster Name>";
            private const string ExistingClusterUri = ExistingClusterName + ".azurehdinsight.net";
            private const string ExistingClusterUsername = "<Cluster Username>";
            private const string ExistingClusterPassword = "<Cluster User Password>";

            static void Main(string[] args)
            {
                System.Console.WriteLine("hello application is running ...");

                var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);

                SubmitPigJob();

                System.Console.WriteLine("Press ENTER toocontinue ...");
                System.Console.ReadLine();
            }

            private static void SubmitPigJob()
            {
                var parameters = new PigJobSubmissionParameters
                {
                    Query = @"LOGS = LOAD '/example/data/sample.log';
                                LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
                                FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
                                GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
                                FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
                                RESULT = order FREQUENCIES by COUNT desc;
                                DUMP RESULT;"
                };

                System.Console.WriteLine("Submitting hello Pig job toohello cluster...");
                var response = _hdiJobManagementClient.JobManagement.SubmitPigJob(parameters);
                System.Console.WriteLine("Validating that hello response is as expected...");
                System.Console.WriteLine("Response status code is " + response.StatusCode);
                System.Console.WriteLine("Validating hello response object...");
                System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
            }
        }
    }
    ```

7. <span data-ttu-id="7a54b-131">toostart Merhaba uygulaması, basın **F5**.</span><span class="sxs-lookup"><span data-stu-id="7a54b-131">toostart hello application, press **F5**.</span></span>

8. <span data-ttu-id="7a54b-132">tooexit Merhaba uygulaması, basın **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="7a54b-132">tooexit hello application, press **ENTER**.</span></span>

## <a name="summary"></a><span data-ttu-id="7a54b-133">Özet</span><span class="sxs-lookup"><span data-stu-id="7a54b-133">Summary</span></span>

<span data-ttu-id="7a54b-134">Gördüğünüz gibi hello Hadoop için .NET SDK'sı, Pig işleri tooan Hdınsight kümesi gönderin ve hello iş durumunu izlemek toocreate .NET uygulamalarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="7a54b-134">As you can see, hello .NET SDK for Hadoop allows you toocreate .NET applications that submit Pig jobs tooan HDInsight cluster, and monitor hello job status.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a54b-135">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="7a54b-135">Next steps</span></span>

<span data-ttu-id="7a54b-136">Hdınsight'ta Pig hakkında daha fazla bilgi için bkz: [hdınsight'ta Hadoop ile Pig kullanma](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="7a54b-136">For information on Pig in HDInsight, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

<span data-ttu-id="7a54b-137">Hdınsight'ta Hadoop kullanma hakkında daha fazla bilgi için aşağıdaki belgeleri hello bakın:</span><span class="sxs-lookup"><span data-stu-id="7a54b-137">For more information on using Hadoop on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="7a54b-138">Hdınsight'ta Hadoop ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="7a54b-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="7a54b-139">Hdınsight'ta Hadoop ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="7a54b-139">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

[preview-portal]: https://portal.azure.com/
