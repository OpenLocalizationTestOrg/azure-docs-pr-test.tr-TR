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
# <a name="run-mapreduce-jobs-using-hdinsight-net-sdk"></a>Hdınsight .NET SDK kullanarak MapReduce işleri çalıştırma
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

Hdınsight .NET SDK kullanarak nasıl toosubmit MapReduce işleri öğrenin. Hdınsight kümeleri gelen jar dosyasını bazı MapReduce örnekleri ile. Merhaba jar dosyası */example/jars/hadoop-mapreduce-examples.jar*.  Merhaba örnekleri biri *wordcount*. Bir C# konsol uygulaması toosubmit wordcount iş geliştirin.  Merhaba iş okur hello */example/data/gutenberg/davinci.txt* dosya ve çıkışları hello sonuçları çok*/example/data/davinciwordcount*.  Toorerun Merhaba uygulaması istiyorsanız hello çıkış klasörü Temizle gerekir.

> [!NOTE]
> Bu makaledeki adımları Hello bir Windows istemcisinden gerçekleştirilmesi gerekir. Linux, OS X veya UNIX istemcisi toowork ile Hive kullanma hakkında daha fazla bilgi için hello makale hello üstte gösterilen hello sekme seçicisini kullanın.
> 
> 

## <a name="prerequisites"></a>Ön koşullar
Bu makalede başlamadan önce aşağıdaki öğelerindeki hello sahip olmanız gerekir:

* **Hdınsight'ta Hadoop kümesi**. Bkz: [Hdınsight'ta Linux tabanlı Hadoop ile çalışmaya başlamak](./hdinsight-hadoop-linux-tutorial-get-started.md).
* **Visual Studio 2013/2015/2017**.

## <a name="submit-mapreduce-jobs-using-hdinsight-net-sdk"></a>Hdınsight .NET SDK kullanarak MapReduce işleri gönderme
Merhaba Hdınsight .NET SDK'sı .NET istemci kitaplıkları, .NET gelen Hdınsight kümeleri ile daha kolay toowork olmasını sağlayan sağlar. 

**tooSubmit işleri**

1. Visual Studio'da bir C# konsol uygulaması oluşturun.
2. Hello ifadesini Nuget Paket Yöneticisi konsolu hello aşağıdaki komutu çalıştırın:
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. Koddan hello kullan:
   
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
4. Tuşuna **F5** toorun Merhaba uygulaması.

toorun hello işi yeniden değiştirmelisiniz hello çıkış klasörü içindeki iş adı hello örnek, "/ data/örnek/davinciwordcount".

Merhaba işi başarıyla tamamlandığında, Merhaba uygulaması hello çıktı dosyası "bölümü-r-00000" Merhaba içeriğine yazdırır.

## <a name="next-steps"></a>Sonraki adımlar
Bu makalede, çeşitli yolları toocreate Hdınsight kümesi öğrendiniz. toolearn daha makaleler hello bakın:

* Hive işi göndermek için bkz: [Hdınsight .NET SDK kullanarak Hive sorgularını çalıştırma](hdinsight-hadoop-use-hive-dotnet-sdk.md).
* Hdınsight kümeleri oluşturmak için bkz: [Hdınsight oluşturma Linux tabanlı Hadoop kümeleri](hdinsight-hadoop-provision-linux-clusters.md).
* Hdınsight kümeleri için bkz. [Hdınsight'ta Hadoop yönetmek kümeleri](hdinsight-administer-use-portal-linux.md).
* Merhaba Hdınsight .NET SDK'sı öğrenmek için bkz: [Hdınsight .NET SDK'sı başvurusu](https://msdn.microsoft.com/library/mt271028.aspx).
* İçin etkileşimli olmayan tooAzure kimliğini doğrulamak için bkz: [etkileşimli olmayan kimlik doğrulama .NET Hdınsight uygulamaları oluşturma](hdinsight-create-non-interactive-authentication-dotnet-applications.md).

