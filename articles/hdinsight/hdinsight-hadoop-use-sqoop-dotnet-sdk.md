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
# <a name="run-sqoop-jobs-using-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="9e924-104">Hdınsight'ta Hadoop için .NET SDK kullanarak Sqoop işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="9e924-104">Run Sqoop jobs using .NET SDK for Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="9e924-105">Hdınsight kümesi ve Azure SQL veritabanı veya SQL Server veritabanı arasında dışarı aktarmak ve nasıl toouse Hdınsight .NET SDK'sı toorun Sqoop Hdınsight tooimport işleri öğrenin.</span><span class="sxs-lookup"><span data-stu-id="9e924-105">Learn how toouse HDInsight .NET SDK toorun Sqoop jobs in HDInsight tooimport and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="9e924-106">Bu makaledeki adımları Hello ya da bir Windows veya Linux tabanlı Hdınsight kümesiyle kullanılabilir; Ancak, bu adımlar, yalnızca bir Windows istemcisinden çalışır.</span><span class="sxs-lookup"><span data-stu-id="9e924-106">hello steps in this article can be used with either a Windows-based or Linux-based HDInsight cluster; however, these steps only work from a Windows client.</span></span> <span data-ttu-id="9e924-107">Merhaba sekme seçicisini Bu makale toochoose hello üstündeki diğer yöntemleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="9e924-107">Use hello tab selector on hello top of this article toochoose other methods.</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="9e924-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9e924-108">Prerequisites</span></span>
<span data-ttu-id="9e924-109">Bu öğreticiye başlamadan önce aşağıdaki öğelerindeki hello sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="9e924-109">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="9e924-110">**Hdınsight'ta Hadoop kümesi**.</span><span class="sxs-lookup"><span data-stu-id="9e924-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="9e924-111">Bkz: [küme ve SQL veritabanı oluşturma](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span><span class="sxs-lookup"><span data-stu-id="9e924-111">See [Create cluster and SQL database](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span></span>

## <a name="use-sqoop-on-hdinsight-clusters-using-net-sdk"></a><span data-ttu-id="9e924-112">.NET SDK kullanarak Hdınsight kümelerinde Sqoop kullanma</span><span class="sxs-lookup"><span data-stu-id="9e924-112">Use Sqoop on HDInsight clusters using .NET SDK</span></span>
<span data-ttu-id="9e924-113">Merhaba Hdınsight .NET SDK'sı .NET istemci kitaplıkları, .NET gelen Hdınsight kümeleri ile daha kolay toowork olmasını sağlayan sağlar.</span><span class="sxs-lookup"><span data-stu-id="9e924-113">hello HDInsight .NET SDK provides .NET client libraries, which makes it easier toowork with HDInsight clusters from .NET.</span></span> <span data-ttu-id="9e924-114">Bu bölümde, bu öğreticide daha önce oluşturduğunuz bir C# konsol uygulaması tooexport hello hivesampletable toohello SQL veritabanı tablosu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9e924-114">In this section, you create a C# console application tooexport hello hivesampletable toohello SQL Database table you created earlier in this tutorial.</span></span>

## <a name="submit-a-sqoop-job"></a><span data-ttu-id="9e924-115">Sqoop işi gönderin</span><span class="sxs-lookup"><span data-stu-id="9e924-115">Submit a Sqoop job</span></span>

1. <span data-ttu-id="9e924-116">Visual Studio'da bir C# konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9e924-116">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="9e924-117">Visual Studio Paket Yöneticisi konsolu Hello Nuget komutu tooimport hello paketi aşağıdaki hello çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="9e924-117">From hello Visual Studio Package Manager Console, run hello following Nuget command tooimport hello package.</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="9e924-118">Merhaba Program.cs dosyasındaki kodu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="9e924-118">Use hello following code in hello Program.cs file:</span></span>
   
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
4. <span data-ttu-id="9e924-119">Tuşuna **F5** toorun hello program.</span><span class="sxs-lookup"><span data-stu-id="9e924-119">Press **F5** toorun hello program.</span></span> 

## <a name="limitations"></a><span data-ttu-id="9e924-120">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="9e924-120">Limitations</span></span>
* <span data-ttu-id="9e924-121">Toplu export - ile Linux tabanlı Hdınsight, hello Sqoop kullanılan bağlayıcı tooexport veri tooMicrosoft SQL Server ya da Azure SQL veritabanı toplu eklemeler şu anda desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="9e924-121">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="9e924-122">-Hello kullanırken, Linux tabanlı Hdınsight ile toplu işleme `-batch` eklemeleri gerçekleştirirken geçiş, Sqoop gerçekleştirir hello INSERT işlemlerine toplu işleme yerine birden çok ekler.</span><span class="sxs-lookup"><span data-stu-id="9e924-122">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching hello insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e924-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9e924-123">Next steps</span></span>
<span data-ttu-id="9e924-124">Öğrendiğiniz artık nasıl toouse Sqoop.</span><span class="sxs-lookup"><span data-stu-id="9e924-124">Now you have learned how toouse Sqoop.</span></span> <span data-ttu-id="9e924-125">toolearn daha bakın:</span><span class="sxs-lookup"><span data-stu-id="9e924-125">toolearn more, see:</span></span>

* <span data-ttu-id="9e924-126">[Hdınsight ile Oozie kullanma](hdinsight-use-oozie.md): Oozie iş akışında kullanmak Sqoop eylem.</span><span class="sxs-lookup"><span data-stu-id="9e924-126">[Use Oozie with HDInsight](hdinsight-use-oozie.md): Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="9e924-127">[Hdınsight kullanarak uçuş gecikme verileri analiz](hdinsight-analyze-flight-delay-data.md): kullanmak Hive tooanalyze uçuş gecikme veri ve Sqoop tooexport veri tooan Azure SQL veritabanını kullanın.</span><span class="sxs-lookup"><span data-stu-id="9e924-127">[Analyze flight delay data using HDInsight](hdinsight-analyze-flight-delay-data.md): Use Hive tooanalyze flight delay data, and then use Sqoop tooexport data tooan Azure SQL database.</span></span>
* <span data-ttu-id="9e924-128">[Veri tooHDInsight karşıya](hdinsight-upload-data.md): veri tooHDInsight/Azure Blob Depolama yüklemek için diğer yöntemler bulun.</span><span class="sxs-lookup"><span data-stu-id="9e924-128">[Upload data tooHDInsight](hdinsight-upload-data.md): Find other methods for uploading data tooHDInsight/Azure Blob storage.</span></span>

