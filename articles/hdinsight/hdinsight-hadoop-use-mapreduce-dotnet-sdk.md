---
title: "Hdınsight .NET SDK - Azure kullanarak aaaSubmit MapReduce işleri | Microsoft Docs"
description: "Nasıl tooAzure Hdınsight .NET SDK kullanarak Hdınsight Hadoop toosubmit MapReduce işleri öğrenin."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: c85e44b0-85fd-4185-ad1c-c34a9fe5ef44
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: jgao
ms.openlocfilehash: d00e31400b8fa47982c31d00bfdcdb304bcb0b59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="794dd-103">Hdınsight .NET SDK kullanarak MapReduce işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="794dd-103">Run MapReduce jobs using HDInsight .NET SDK</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="794dd-104">Hdınsight .NET SDK kullanarak nasıl toosubmit MapReduce işleri öğrenin.</span><span class="sxs-lookup"><span data-stu-id="794dd-104">Learn how toosubmit MapReduce jobs using HDInsight .NET SDK.</span></span> <span data-ttu-id="794dd-105">Hdınsight kümeleri gelen jar dosyasını bazı MapReduce örnekleri ile.</span><span class="sxs-lookup"><span data-stu-id="794dd-105">HDInsight clusters come with a jar file with some MapReduce samples.</span></span> <span data-ttu-id="794dd-106">Merhaba jar dosyası */example/jars/hadoop-mapreduce-examples.jar*.</span><span class="sxs-lookup"><span data-stu-id="794dd-106">hello jar file is */example/jars/hadoop-mapreduce-examples.jar*.</span></span>  <span data-ttu-id="794dd-107">Merhaba örnekleri biri *wordcount*.</span><span class="sxs-lookup"><span data-stu-id="794dd-107">One of hello samples is *wordcount*.</span></span> <span data-ttu-id="794dd-108">Bir C# konsol uygulaması toosubmit wordcount iş geliştirin.</span><span class="sxs-lookup"><span data-stu-id="794dd-108">You develop a C# console application toosubmit a wordcount job.</span></span>  <span data-ttu-id="794dd-109">Merhaba iş okur hello */example/data/gutenberg/davinci.txt* dosya ve çıkışları hello sonuçları çok*/example/data/davinciwordcount*.</span><span class="sxs-lookup"><span data-stu-id="794dd-109">hello job reads hello */example/data/gutenberg/davinci.txt* file, and outputs hello results too*/example/data/davinciwordcount*.</span></span>  <span data-ttu-id="794dd-110">Toorerun Merhaba uygulaması istiyorsanız hello çıkış klasörü Temizle gerekir.</span><span class="sxs-lookup"><span data-stu-id="794dd-110">If you want toorerun hello application, you must clean up hello output folder.</span></span>

> [!NOTE]
> <span data-ttu-id="794dd-111">Bu makaledeki adımları Hello bir Windows istemcisinden gerçekleştirilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="794dd-111">hello steps in this article must be performed from a Windows client.</span></span> <span data-ttu-id="794dd-112">Linux, OS X veya UNIX istemcisi toowork ile Hive kullanma hakkında daha fazla bilgi için hello makale hello üstte gösterilen hello sekme seçicisini kullanın.</span><span class="sxs-lookup"><span data-stu-id="794dd-112">For information on using a Linux, OS X, or Unix client toowork with Hive, use hello tab selector shown on hello top of hello article.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="794dd-113">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="794dd-113">Prerequisites</span></span>
<span data-ttu-id="794dd-114">Bu makalede başlamadan önce aşağıdaki öğelerindeki hello sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="794dd-114">Before you begin this article, you must have hello following items:</span></span>

* <span data-ttu-id="794dd-115">**Hdınsight'ta Hadoop kümesi**.</span><span class="sxs-lookup"><span data-stu-id="794dd-115">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="794dd-116">Bkz: [Hdınsight'ta Linux tabanlı Hadoop ile çalışmaya başlamak](./hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="794dd-116">See [Get started using Linux-based Hadoop in HDInsight](./hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="794dd-117">**Visual Studio 2013/2015/2017**.</span><span class="sxs-lookup"><span data-stu-id="794dd-117">**Visual Studio 2013/2015/2017**.</span></span>

## <a name="submit-mapreduce-jobs-using-hdinsight-net-sdk"></a><span data-ttu-id="794dd-118">Hdınsight .NET SDK kullanarak MapReduce işleri gönderme</span><span class="sxs-lookup"><span data-stu-id="794dd-118">Submit MapReduce jobs using HDInsight .NET SDK</span></span>
<span data-ttu-id="794dd-119">Merhaba Hdınsight .NET SDK'sı .NET istemci kitaplıkları, .NET gelen Hdınsight kümeleri ile daha kolay toowork olmasını sağlayan sağlar.</span><span class="sxs-lookup"><span data-stu-id="794dd-119">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span> 

<span data-ttu-id="794dd-120">**tooSubmit işleri**</span><span class="sxs-lookup"><span data-stu-id="794dd-120">**tooSubmit jobs**</span></span>

1. <span data-ttu-id="794dd-121">Visual Studio'da bir C# konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="794dd-121">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="794dd-122">Hello ifadesini Nuget Paket Yöneticisi konsolu hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="794dd-122">From hello Nuget Package Manager Console, run hello following command:</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="794dd-123">Koddan hello kullan:</span><span class="sxs-lookup"><span data-stu-id="794dd-123">Use hello following code:</span></span>
   
        using System.Collections.Generic;
        using System.IO;
        using System.Text;
        using System.Threading;
        using Microsoft.Azure.Management.HDInsight.Job;
        using Microsoft.Azure.Management.HDInsight.Job.Models;
        using Hyak.Common;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;

        namespace SubmitHDInsightJobDotNet
        {
            class Program
            {
                private static HDInsightJobManagementClient _hdiJobManagementClient;
   
                private const string existingClusterName = "<Your HDInsight Cluster Name>";
                private const string existingClusterUri = existingClusterName + ".azurehdinsight.net";
                private const string existingClusterUsername = "<Cluster Username>";
                private const string existingClusterPassword = "<Cluster User Password>";
   
                private const string defaultStorageAccountName = "<Default Storage Account Name>"; //<StorageAccountName>.blob.core.windows.net
                private const string defaultStorageAccountKey = "<Default Storage Account Key>";
                private const string defaultStorageContainerName = "<Default Blob Container Name>";

                private const string sourceFile = "/example/data/gutenberg/davinci.txt";  
                private const string outputFolder = "/example/data/davinciwordcount";
   
                static void Main(string[] args)
                {
                    System.Console.WriteLine("hello application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = existingClusterUsername, Password = existingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(existingClusterUri, clusterCredentials);
   
                    SubmitMRJob();
   
                    System.Console.WriteLine("Press ENTER toocontinue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitMRJob()
                {
                    List<string> args = new List<string> { { "/example/data/gutenberg/davinci.txt" }, { "/example/data/davinciwordcount" } };
   
                    var paras = new MapReduceJobSubmissionParameters
                    {
                        JarFile = @"/example/jars/hadoop-mapreduce-examples.jar",
                        JarClass = "wordcount",
                        Arguments = args
                    };
   
                    System.Console.WriteLine("Submitting hello MR job toohello cluster...");
                    var jobResponse = _hdiJobManagementClient.JobManagement.SubmitMapReduceJob(paras);
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
                    System.Console.WriteLine("Job output is: ");
                    var storageAccess = new AzureStorageAccess(defaultStorageAccountName, defaultStorageAccountKey,
                        defaultStorageContainerName);
        
                    if (jobDetail.ExitValue == 0)
                    {
                        // Create hello storage account object
                        CloudStorageAccount storageAccount = CloudStorageAccount.Parse("DefaultEndpointsProtocol=https;AccountName=" + 
                            defaultStorageAccountName + 
                            ";AccountKey=" + defaultStorageAccountKey);
        
                        // Create hello blob client.
                        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
        
                        // Retrieve reference tooa previously created container.
                        CloudBlobContainer container = blobClient.GetContainerReference(defaultStorageContainerName);
        
                        CloudBlockBlob blockBlob = container.GetBlockBlobReference(outputFolder.Substring(1) + "/part-r-00000");
        
                        using (var stream = blockBlob.OpenRead())
                        {
                            using (StreamReader reader = new StreamReader(stream))
                            {
                                while (!reader.EndOfStream)
                                {
                                    System.Console.WriteLine(reader.ReadLine());
                                }
                            }
                        }
                    }
                    else
                    {
                        // fetch stderr output in case of failure
                        var output = _hdiJobManagementClient.JobManagement.GetJobErrorLogs(jobId, storageAccess); 
        
                        using (var reader = new StreamReader(output, Encoding.UTF8))
                        {
                            string value = reader.ReadToEnd();
                            System.Console.WriteLine(value);
                        }
        
                    }
                }
            }
        }
4. <span data-ttu-id="794dd-124">Tuşuna **F5** toorun Merhaba uygulaması.</span><span class="sxs-lookup"><span data-stu-id="794dd-124">Press **F5** toorun hello application.</span></span>

<span data-ttu-id="794dd-125">toorun hello işi yeniden değiştirmelisiniz hello çıkış klasörü içindeki iş adı hello örnek, "/ data/örnek/davinciwordcount".</span><span class="sxs-lookup"><span data-stu-id="794dd-125">toorun hello job again, you must change hello job output folder name, in hello sample, it is "/example/data/davinciwordcount".</span></span>

<span data-ttu-id="794dd-126">Merhaba işi başarıyla tamamlandığında, Merhaba uygulaması hello çıktı dosyası "bölümü-r-00000" Merhaba içeriğine yazdırır.</span><span class="sxs-lookup"><span data-stu-id="794dd-126">When hello job completes successfully, hello application prints hello content of hello output file "part-r-00000".</span></span>

## <a name="next-steps"></a><span data-ttu-id="794dd-127">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="794dd-127">Next steps</span></span>
<span data-ttu-id="794dd-128">Bu makalede, çeşitli yolları toocreate Hdınsight kümesi öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="794dd-128">In this article, you have learned several ways toocreate an HDInsight cluster.</span></span> <span data-ttu-id="794dd-129">toolearn daha makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="794dd-129">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="794dd-130">Hive işi göndermek için bkz: [Hdınsight .NET SDK kullanarak Hive sorgularını çalıştırma](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="794dd-130">For submitting a Hive job, see [Run Hive queries using HDInsight .NET SDK](hdinsight-hadoop-use-hive-dotnet-sdk.md).</span></span>
* <span data-ttu-id="794dd-131">Hdınsight kümeleri oluşturmak için bkz: [Hdınsight oluşturma Linux tabanlı Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="794dd-131">For creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="794dd-132">Hdınsight kümeleri için bkz. [Hdınsight'ta Hadoop yönetmek kümeleri](hdinsight-administer-use-portal-linux.md).</span><span class="sxs-lookup"><span data-stu-id="794dd-132">For managing HDInsight clusters, see [Manage Hadoop clusters in HDInsight](hdinsight-administer-use-portal-linux.md).</span></span>
* <span data-ttu-id="794dd-133">Merhaba Hdınsight .NET SDK'sı öğrenmek için bkz: [Hdınsight .NET SDK'sı başvurusu](https://msdn.microsoft.com/library/mt271028.aspx).</span><span class="sxs-lookup"><span data-stu-id="794dd-133">For learning hello HDInsight .NET SDK, see [HDInsight .NET SDK reference](https://msdn.microsoft.com/library/mt271028.aspx).</span></span>
* <span data-ttu-id="794dd-134">İçin etkileşimli olmayan tooAzure kimliğini doğrulamak için bkz: [etkileşimli olmayan kimlik doğrulama .NET Hdınsight uygulamaları oluşturma](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span><span class="sxs-lookup"><span data-stu-id="794dd-134">For non-interactive authenticate tooAzure, see [Create non-interactive authentication .NET HDInsight applications](hdinsight-create-non-interactive-authentication-dotnet-applications.md).</span></span>

