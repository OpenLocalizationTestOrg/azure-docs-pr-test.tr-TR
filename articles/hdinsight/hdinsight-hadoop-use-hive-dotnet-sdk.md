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
# <a name="run-hive-queries-using-hdinsight-net-sdk"></a>Hdınsight .NET SDK kullanarak Hive sorguları çalıştırma
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Hdınsight .NET SDK kullanarak nasıl toosubmit Hive sorguları hakkında bilgi edinin. C# programı toosubmit Hive tablolarını listeleme bir Hive sorgusu Yaz ve hello sonuçları görüntüler.

> [!NOTE]
> Bu makaledeki adımları Hello bir Windows istemcisinden gerçekleştirilmesi gerekir. Linux, OS X veya UNIX istemcisi toowork ile Hive kullanma hakkında daha fazla bilgi için hello makale hello üstte gösterilen hello sekme seçicisini kullanın.
> 
> 

## <a name="prerequisites"></a>Ön koşullar
Bu makalede başlamadan önce aşağıdaki öğelerindeki hello sahip olmanız gerekir:

* **Hdınsight'ta Hadoop kümesi**. Bkz: [Hdınsight'ta Linux tabanlı Hadoop ile çalışmaya başlamak](./hdinsight-hadoop-linux-tutorial-get-started.md).
* **Visual Studio 2013/2015/2017**.

## <a name="submit-hive-queries-using-hdinsight-net-sdk"></a>Hdınsight .NET SDK kullanarak Hive sorguları gönderme
Merhaba Hdınsight .NET SDK'sı .NET istemci kitaplıkları, .NET gelen Hdınsight kümeleri ile daha kolay toowork olmasını sağlayan sağlar. 

**tooSubmit işleri**

1. Visual Studio'da bir C# konsol uygulaması oluşturun.
2. Hello ifadesini Nuget Paket Yöneticisi konsolu hello aşağıdaki komutu çalıştırın:
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. Koddan hello kullan:

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
4. Tuşuna **F5** toorun Merhaba uygulaması.

Merhaba uygulaması Hello çıktısını benzer olacaktır:

![Hdınsight Hadoop Hive iş çıktısı](./media/hdinsight-hadoop-use-hive-dotnet-sdk/hdinsight-hadoop-use-hive-net-sdk-output.png)

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, çeşitli yolları toocreate Hdınsight kümesi öğrendiniz. toolearn daha makaleler hello bakın:

* [Azure HDInsight'ı Kullanmaya Başlama][hdinsight-get-started]
* [Hdınsight'ta Hadoop kümeleri oluşturma][hdinsight-provision]
* [Hello Azure portal kullanarak hdınsight'ta Hadoop kümelerini yönetme](hdinsight-administer-use-management-portal.md)
* [Hdınsight .NET SDK'sı başvurusu](https://msdn.microsoft.com/library/mt271028.aspx)
* [HDInsight ile Pig kullanma](hdinsight-use-pig.md)
* [Hdınsight ile Sqoop kullanma](hdinsight-use-sqoop-mac-linux.md)
* [Etkileşimli olmayan kimlik doğrulaması .NET HDInsight uygulamaları oluşturma](hdinsight-create-non-interactive-authentication-dotnet-applications.md)

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md


