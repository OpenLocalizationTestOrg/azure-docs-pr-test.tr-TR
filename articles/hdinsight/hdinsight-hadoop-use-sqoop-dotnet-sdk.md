---
title: ".NET ve Hdınsight - Azure kullanarak Sqoop işleri çalıştırma | Microsoft Docs"
description: "Hdınsight .NET SDK'sı Sqoop alma çalıştırın ve bir Hadoop kümesi ve bir Azure SQL veritabanı arasında dışa aktarmak için nasıl kullanılacağını öğrenin."
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
ms.openlocfilehash: c95641fc6d20e2911e007d1974b9e2c2398b3133
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="run-sqoop-jobs-using-net-sdk-for-hadoop-in-hdinsight"></a><span data-ttu-id="e2053-104">Hdınsight'ta Hadoop için .NET SDK kullanarak Sqoop işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="e2053-104">Run Sqoop jobs using .NET SDK for Hadoop in HDInsight</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="e2053-105">İçeri ve dışarı aktarma Hdınsight kümesi ve Azure SQL veritabanı veya SQL Server veritabanı arasında hdınsight'ta Sqoop işlerini çalıştırmak için Hdınsight .NET SDK'sını kullanmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="e2053-105">Learn how to use HDInsight .NET SDK to run Sqoop jobs in HDInsight to import and export between HDInsight cluster and Azure SQL database or SQL Server database.</span></span>

> [!NOTE]
> <span data-ttu-id="e2053-106">Bu makaledeki adımları ya da bir Windows veya Linux tabanlı Hdınsight kümesiyle kullanılabilir; Ancak, bu adımlar, yalnızca bir Windows istemcisinden çalışır.</span><span class="sxs-lookup"><span data-stu-id="e2053-106">The steps in this article can be used with either a Windows-based or Linux-based HDInsight cluster; however, these steps only work from a Windows client.</span></span> <span data-ttu-id="e2053-107">Bu makalenin üst kısmındaki sekme seçicisini diğer yöntemleri seçmek için kullanın.</span><span class="sxs-lookup"><span data-stu-id="e2053-107">Use the tab selector on the top of this article to choose other methods.</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="e2053-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="e2053-108">Prerequisites</span></span>
<span data-ttu-id="e2053-109">Bu öğreticiye başlamadan önce aşağıdaki öğelere sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="e2053-109">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="e2053-110">**Hdınsight'ta Hadoop kümesi**.</span><span class="sxs-lookup"><span data-stu-id="e2053-110">**A Hadoop cluster in HDInsight**.</span></span> <span data-ttu-id="e2053-111">Bkz: [küme ve SQL veritabanı oluşturma](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span><span class="sxs-lookup"><span data-stu-id="e2053-111">See [Create cluster and SQL database](hdinsight-use-sqoop.md#create-cluster-and-sql-database).</span></span>

## <a name="use-sqoop-on-hdinsight-clusters-using-net-sdk"></a><span data-ttu-id="e2053-112">.NET SDK kullanarak Hdınsight kümelerinde Sqoop kullanma</span><span class="sxs-lookup"><span data-stu-id="e2053-112">Use Sqoop on HDInsight clusters using .NET SDK</span></span>
<span data-ttu-id="e2053-113">Hdınsight .NET SDK'sı .NET istemci kitaplıkları, .NET Hdınsight kümeleriyle çalışmak kolaylaştırır sağlar.</span><span class="sxs-lookup"><span data-stu-id="e2053-113">The HDInsight .NET SDK provides .NET client libraries, which makes it easier to work with HDInsight clusters from .NET.</span></span> <span data-ttu-id="e2053-114">Bu bölümde, bu öğreticide daha önce oluşturduğunuz SQL veritabanı tablosu hivesampletable verilecek bir C# konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e2053-114">In this section, you create a C# console application to export the hivesampletable to the SQL Database table you created earlier in this tutorial.</span></span>

## <a name="submit-a-sqoop-job"></a><span data-ttu-id="e2053-115">Sqoop işi gönderin</span><span class="sxs-lookup"><span data-stu-id="e2053-115">Submit a Sqoop job</span></span>

1. <span data-ttu-id="e2053-116">Visual Studio'da bir C# konsol uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="e2053-116">Create a C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="e2053-117">Visual Studio Paket Yöneticisi Konsolu'ndan paketini içeri aktarmak için aşağıdaki Nuget komutunu çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="e2053-117">From the Visual Studio Package Manager Console, run the following Nuget command to import the package.</span></span>
   
        Install-Package Microsoft.Azure.Management.HDInsight.Job
3. <span data-ttu-id="e2053-118">Aşağıdaki kodu Program.cs dosyasında kullanın:</span><span class="sxs-lookup"><span data-stu-id="e2053-118">Use the following code in the Program.cs file:</span></span>
   
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
                    System.Console.WriteLine("The application is running ...");
   
                    var clusterCredentials = new BasicAuthenticationCloudCredentials { Username = ExistingClusterUsername, Password = ExistingClusterPassword };
                    _hdiJobManagementClient = new HDInsightJobManagementClient(ExistingClusterUri, clusterCredentials);
   
                    SubmitSqoopJob();
   
                    System.Console.WriteLine("Press ENTER to continue ...");
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
   
                    System.Console.WriteLine("Submitting the Sqoop job to the cluster...");
                    var response = _hdiJobManagementClient.JobManagement.SubmitSqoopJob(parameters);
                    System.Console.WriteLine("Validating that the response is as expected...");
                    System.Console.WriteLine("Response status code is " + response.StatusCode);
                    System.Console.WriteLine("Validating the response object...");
                    System.Console.WriteLine("JobId is " + response.JobSubmissionJsonResponse.Id);
                }
            }
        }
4. <span data-ttu-id="e2053-119">Tuşuna **F5** programı çalıştırmak için.</span><span class="sxs-lookup"><span data-stu-id="e2053-119">Press **F5** to run the program.</span></span> 

## <a name="limitations"></a><span data-ttu-id="e2053-120">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="e2053-120">Limitations</span></span>
* <span data-ttu-id="e2053-121">Toplu export - ile Linux tabanlı Hdınsight, Microsoft SQL Server veya Azure SQL veritabanı için verileri dışa aktarmak için kullanılan Sqoop bağlayıcı toplu eklemeler şu anda desteklemiyor.</span><span class="sxs-lookup"><span data-stu-id="e2053-121">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="e2053-122">-Kullanırken, Linux tabanlı Hdınsight ile toplu işleme `-batch` eklemeleri gerçekleştirirken geçiş, Sqoop gerçekleştirir INSERT işlemlerine toplu işleme yerine birden çok ekler.</span><span class="sxs-lookup"><span data-stu-id="e2053-122">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop performs multiple inserts instead of batching the insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2053-123">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="e2053-123">Next steps</span></span>
<span data-ttu-id="e2053-124">Şimdi Sqoop kullanma öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="e2053-124">Now you have learned how to use Sqoop.</span></span> <span data-ttu-id="e2053-125">Daha fazla bilgi için bkz:</span><span class="sxs-lookup"><span data-stu-id="e2053-125">To learn more, see:</span></span>

* <span data-ttu-id="e2053-126">[Hdınsight ile Oozie kullanma](hdinsight-use-oozie.md): Oozie iş akışında kullanmak Sqoop eylem.</span><span class="sxs-lookup"><span data-stu-id="e2053-126">[Use Oozie with HDInsight](hdinsight-use-oozie.md): Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="e2053-127">[Hdınsight kullanarak uçuş gecikme verileri analiz](hdinsight-analyze-flight-delay-data.md): uçuş çözümlemek için kullanmak Hive gecikme veri ve bir Azure SQL veritabanına veri vermek için Sqoop kullanın.</span><span class="sxs-lookup"><span data-stu-id="e2053-127">[Analyze flight delay data using HDInsight](hdinsight-analyze-flight-delay-data.md): Use Hive to analyze flight delay data, and then use Sqoop to export data to an Azure SQL database.</span></span>
* <span data-ttu-id="e2053-128">[Verileri Hdınsight'a yükleme](hdinsight-upload-data.md): Hdınsight/Azure Blob depolama alanına veri yüklemek için diğer yöntemler bulun.</span><span class="sxs-lookup"><span data-stu-id="e2053-128">[Upload data to HDInsight](hdinsight-upload-data.md): Find other methods for uploading data to HDInsight/Azure Blob storage.</span></span>

