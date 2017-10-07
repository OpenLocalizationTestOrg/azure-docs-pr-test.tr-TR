---
title: "Hdınsight .NET SDK - Azure kullanarak aaaRun Hive sorguları | Microsoft Docs"
description: "Nasıl toosubmit Hadoop tooAzure Hdınsight .NET SDK kullanarak Hdınsight Hadoop işleri öğrenin."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 4e291890-f8b4-426c-b5e8-d4fd512ff042
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: 11f07d90405d3e804774610e242813927df59a03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hdinsight-net-sdk"></a><span data-ttu-id="38ad8-103">Hdınsight .NET SDK kullanarak Hive sorguları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="38ad8-103">Run Hive queries using HDInsight .NET SDK</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="38ad8-104">Hdınsight .NET SDK kullanarak nasıl toosubmit Hive sorguları hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="38ad8-104">Learn how toosubmit Hive queries using HDInsight .NET SDK.</span></span> <span data-ttu-id="38ad8-105">C# programı toosubmit Hive tablolarını listeleme bir Hive sorgusu Yaz ve hello sonuçları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="38ad8-105">You write a C# program toosubmit a Hive query for listing Hive tables, and display hello results.</span></span>

> [!NOTE]
> <span data-ttu-id="38ad8-106">Bu makaledeki adımları Hello bir Windows istemcisinden gerçekleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="38ad8-106">hello steps in this article must be performed from a Windows client.</span></span> <span data-ttu-id="38ad8-107">Linux, OS X veya UNIX istemcisi toowork ile Hive kullanma hakkında daha fazla bilgi için hello makale hello üstte gösterilen hello sekme seçicisini kullanın.</span><span class="sxs-lookup"><span data-stu-id="38ad8-107">For information on using a Linux, OS X, or Unix client toowork with Hive, use hello tab selector shown on hello top of hello article.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="38ad8-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="38ad8-108">Prerequisites</span></span>
<span data-ttu-id="38ad8-109">Bu makalede başlamadan önce aşağıdaki öğelerindeki hello sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="38ad8-109">Before you begin this article, you must have hello following items:</span></span>

* <span data-ttu-id="38ad8-110">**Hdınsight'ta Hadoop kümesi**.</span><span class="sxs-lookup"><span data-stu-id="38ad8-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="38ad8-111">Bkz: [Hdınsight'ta Linux tabanlı Hadoop ile çalışmaya başlamak](./hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="38ad8-111">See [Get started using Linux-based Hadoop in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="38ad8-112">**Visual Studio 2013/2015/2017**.</span><span class="sxs-lookup"><span data-stu-id="38ad8-112">**Visual Studio 2013/2015/2017**.</span></span>

## <a name="submit-hive-queries-using-hdinsight-net-sdk"></a><span data-ttu-id="38ad8-113">Hdınsight .NET SDK kullanarak Hive sorguları gönderme</span><span class="sxs-lookup"><span data-stu-id="38ad8-113">Submit Hive queries using HDInsight .NET SDK</span></span>
<span data-ttu-id="38ad8-114">Merhaba Hdınsight .NET SDK'sı .NET istemci kitaplıkları, .NET gelen Hdınsight kümeleri ile daha kolay toowork olmasını sağlayan sağlar.</span><span class="sxs-lookup"><span data-stu-id="38ad8-114">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span> 

<span data-ttu-id="38ad8-115">**tooSubmit işleri**</span><span class="sxs-lookup"><span data-stu-id="38ad8-115">**tooSubmit jobs**</span></span>

1. <span data-ttu-id="38ad8-116">Visual Studio'da bir C# konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="38ad8-116">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="38ad8-117">Hello ifadesini Nuget Paket Yöneticisi konsolu hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="38ad8-117">From hello Nuget Package Manager Console, run hello following command:</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="38ad8-118">Koddan hello kullan:</span><span class="sxs-lookup"><span data-stu-id="38ad8-118">Use hello following code:</span></span>

    ```csharp
        using System.Collections.Generic;
        using System.IO;
        using System.Text;
        using System.Threading;
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
   
                private const string DefaultStorageAccountName = "<Default Storage Account Name>";
                private const string DefaultStorageAccountKey = "<Default Storage Account Key>";
                private const string DefaultStorageContainerName = "<Default Blob Container Name>";
   
                static void Main(string[] args)
                {
                    System.Console.WriteLine("hello application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitHiveJob();
   
                    System.Console.WriteLine("Press ENTER toocontinue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitHiveJob()
                {
                    Dictionary<string, string> defines = new Dictionary<string, string> { { "hive.execution.engine", "tez" }, { "hive.exec.reducers.max", "1" } };
                    List<string> args = new List<string> { { "argA" }, { "argB" } };
                    var parameters = new HiveJobSubmissionParameters
                    {
                        Query = "SHOW TABLES",
                        Defines = defines,
                        Arguments = args
                    };
   
                    System.Console.WriteLine("Submitting hello Hive job toohello cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitHiveJob(parameters);
                    var jobId = jobResponse.JobSubmissionJsonResponse.Id;
                    System.Console.WriteLine("Response status code is " + jobResponse.StatusCode);
                    System.Console.WriteLine("JobId is " + jobId);
   
                    System.Console.WriteLine("Waiting for hello job completion ...");
   
                    // Wait for job completion
                    var jobDetail = _hdiJobManagementClient.JobManagement.GetJob(jobId).JobDetail;
                    while (!jobDetail.Status.JobComplete)
                    {
                        Thread.Sleep(1000);
                        jobDetail = _hdiJobManagementClient.JobManagement.GetJob(jobId).JobDetail;
                    }
   
                    // Get job output
                    var storageAccess = new AzureStorageAccess(DefaultStorageAccountName, DefaultStorageAccountKey,
                        DefaultStorageContainerName);
                    var output = (jobDetail.ExitValue == 0)
                        ? _hdiJobManagementClient.JobManagement.GetJobOutput(jobId, storageAccess) // fetch stdout output in case of success
                        : _hdiJobManagementClient.JobManagement.GetJobErrorLogs(jobId, storageAccess); // fetch stderr output in case of failure
   
                    System.Console.WriteLine("Job output is: ");
   
                    using (var reader = new StreamReader(output, Encoding.UTF8))
                    {
                        string value = reader.ReadToEnd();
                        System.Console.WriteLine(value);
                    }
                }
            }
        }
    ```
4. <span data-ttu-id="38ad8-119">Tuşuna **F5** toorun Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="38ad8-119">Press **F5** toorun hello application.</span></span>

<span data-ttu-id="38ad8-120">Merhaba uygulaması Hello çıktısını benzer olacaktır:</span><span class="sxs-lookup"><span data-stu-id="38ad8-120">hello output of hello application shall be similar to:</span></span>

![Hdınsight Hadoop Hive iş çıktısı](./media/hdinsight-hadoop-use-hive-dotnet-sdk/hdinsight-hadoop-use-hive-net-sdk-output.png)

## <a name="next-steps"></a><span data-ttu-id="38ad8-122">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="38ad8-122">Next steps</span></span>
<span data-ttu-id="38ad8-123">Bu makalede, çeşitli yolları toocreate Hdınsight kümesi öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="38ad8-123">In this article, you have learned several ways toocreate an HDInsight cluster.</span></span> <span data-ttu-id="38ad8-124">toolearn daha makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="38ad8-124">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="38ad8-125">[Azure HDInsight'ı Kullanmaya Başlama][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="38ad8-125">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="38ad8-126">[Hdınsight'ta Hadoop kümeleri oluşturma][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="38ad8-126">[Create Hadoop clusters in HDInsight][hdinsight-provision]</span></span>
* [<span data-ttu-id="38ad8-127">Hello Azure portal kullanarak hdınsight'ta Hadoop kümelerini yönetme</span><span class="sxs-lookup"><span data-stu-id="38ad8-127">Manage Hadoop clusters in HDInsight by using hello Azure portal</span></span>](hdinsight-administer-use-management-portal.md)
* [<span data-ttu-id="38ad8-128">Hdınsight .NET SDK'sı başvurusu</span><span class="sxs-lookup"><span data-stu-id="38ad8-128">HDInsight .NET SDK reference</span></span>](https://msdn.microsoft.com/library/mt271028.aspx)
* [<span data-ttu-id="38ad8-129">HDInsight ile Pig kullanma</span><span class="sxs-lookup"><span data-stu-id="38ad8-129">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="38ad8-130">Hdınsight ile Sqoop kullanma</span><span class="sxs-lookup"><span data-stu-id="38ad8-130">Use Sqoop with HDInsight</span></span>](hdinsight-use-sqoop-mac-linux.md)
* [<span data-ttu-id="38ad8-131">Etkileşimli olmayan kimlik doğrulaması .NET HDInsight uygulamaları oluşturma</span><span class="sxs-lookup"><span data-stu-id="38ad8-131">Create non-interactive authentication .NET HDInsight applications</span></span>](hdinsight-create-non-interactive-authentication-dotnet-applications.md)

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md


