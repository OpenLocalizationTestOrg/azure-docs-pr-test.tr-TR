---
title: ".NET ve Hdınsight - Azure kullanarak aaaRun Sqoop işleri | Microsoft Docs"
description: "Nasıl toouse Hdınsight .NET SDK'sı toorun Sqoop içe ve dışa aktarma Hadoop kümesi ve bir Azure SQL veritabanı arasında bilgi edinin."
keywords: "sqoop işi"
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
ms.assetid: 87bacd13-7775-4b71-91da-161cb6224a96
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: afa0a78ba5e5d89c04ba7be4b58dd24aea4f39ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-using-net-sdk-for-hadoop-in-hdinsight"></a>Hdınsight'ta Hadoop için .NET SDK kullanarak Sqoop işleri çalıştırma
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Hdınsight kümesi ve Azure SQL veritabanı veya SQL Server veritabanı arasında dışarı aktarmak ve nasıl toouse Hdınsight .NET SDK'sı toorun Sqoop Hdınsight tooimport işleri öğrenin.

> [!NOTE]
> Bu makaledeki adımları Hello ya da bir Windows veya Linux tabanlı Hdınsight kümesiyle kullanılabilir; Ancak, bu adımlar, yalnızca bir Windows istemcisinden çalışır. Merhaba sekme seçicisini Bu makale toochoose hello üstündeki diğer yöntemleri kullanın.
> 
> 

### <a name="prerequisites"></a>Ön koşullar
Bu öğreticiye başlamadan önce aşağıdaki öğelerindeki hello sahip olmanız gerekir:

* **Hdınsight'ta Hadoop kümesi**. Bkz: [küme ve SQL veritabanı oluşturma](hdinsight-use-sqoop.md#create-cluster-and-sql-database).

## <a name="use-sqoop-on-hdinsight-clusters-using-net-sdk"></a>.NET SDK kullanarak Hdınsight kümelerinde Sqoop kullanma
Merhaba Hdınsight .NET SDK'sı .NET istemci kitaplıkları, .NET gelen Hdınsight kümeleri ile daha kolay toowork olmasını sağlayan sağlar. Bu bölümde, bu öğreticide daha önce oluşturduğunuz bir C# konsol uygulaması tooexport hello hivesampletable toohello SQL veritabanı tablosu oluşturun.

## <a name="submit-a-sqoop-job"></a>Sqoop işi gönderin

1. Visual Studio'da bir C# konsol uygulaması oluşturun.
2. Visual Studio Paket Yöneticisi konsolu Hello Nuget komutu tooimport hello paketi aşağıdaki hello çalıştırın.
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. Merhaba Program.cs dosyasındaki kodu aşağıdaki hello kullan:
   
        using System.Collections.Generic;
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
   
                    SubmitSqoopJob();
   
                    System.Console.WriteLine("Press ENTER toocontinue ...");
                    System.Console.ReadLine();
                }
   
                private static void SubmitSqoopJob()
                {
                    var sqlDatabaseServerName = "<SQLDatabaseServerName>";
                    var sqlDatabaseLogin = "<SQLDatabaseLogin>";
                    var sqlDatabaseLoginPassword = "<SQLDatabaseLoginPassword>";
                    var sqlDatabaseDatabaseName = "<DatabaseName>";
   
                    var tableName = "<TableName>";
                    var exportDir = "/tutorials/usesqoop/data";
   
                    // Connection string for using Azure SQL Database.
                    // Comment if using SQL Server
                    var connectionString = "jdbc:sqlserver://" + sqlDatabaseServerName + ".database.windows.net;user=" + sqlDatabaseLogin + "@" + sqlDatabaseServerName + ";password=" + sqlDatabaseLoginPassword + ";database=" + sqlDatabaseDatabaseName;
                    // Connection string for using SQL Server.
                    // Uncomment if using SQL Server
                    //var connectionString = "jdbc:sqlserver://" + sqlDatabaseServerName + ";user=" + sqlDatabaseLogin + ";password=" + sqlDatabaseLoginPassword + ";database=" + sqlDatabaseDatabaseName;
   
                    var parameters = new SqoopJobSubmissionParameters
                    {
                        Files = new List<string> { "/user/oozie/share/lib/sqoop/sqljdbc41.jar" }, // This line is required for Linux-based cluster.
                        Command = "export --connect " + connectionString + " --table " + tableName + "_mobile --export-dir " + exportDir + "_mobile --fields-terminated-by \\t -m 1"
                    };
   
                    System.Console.WriteLine("Submitting hello Sqoop job toohello cluster...");
                    var response = _hdiJobManagementClient.JobManagement.SubmitSqoopJob(parameters);
                    System.Console.WriteLine("Validating that hello response is as expected...");
                    System.Console.WriteLine("Response status code is " + response.StatusCode);
                    System.Console.WriteLine("Validating hello response object...");
                    System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
                }
            }
        }
4. Tuşuna **F5** toorun hello program. 

## <a name="limitations"></a>Sınırlamalar
* Toplu export - ile Linux tabanlı Hdınsight, hello Sqoop kullanılan bağlayıcı tooexport veri tooMicrosoft SQL Server ya da Azure SQL veritabanı toplu eklemeler şu anda desteklemiyor.
* -Hello kullanırken, Linux tabanlı Hdınsight ile toplu işleme `-batch` eklemeleri gerçekleştirirken geçiş, Sqoop gerçekleştirir hello INSERT işlemlerine toplu işleme yerine birden çok ekler.

## <a name="next-steps"></a>Sonraki adımlar
Öğrendiğiniz artık nasıl toouse Sqoop. toolearn daha bakın:

* [Hdınsight ile Oozie kullanma](hdinsight-use-oozie.md): Oozie iş akışında kullanmak Sqoop eylem.
* [Hdınsight kullanarak uçuş gecikme verileri analiz](hdinsight-analyze-flight-delay-data.md): kullanmak Hive tooanalyze uçuş gecikme veri ve Sqoop tooexport veri tooan Azure SQL veritabanını kullanın.
* [Veri tooHDInsight karşıya](hdinsight-upload-data.md): veri tooHDInsight/Azure Blob Depolama yüklemek için diğer yöntemler bulun.

