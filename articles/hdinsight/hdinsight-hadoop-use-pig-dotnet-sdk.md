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
# <a name="run-pig-jobs-using-hello-net-sdk-for-hadoop-in-hdinsight"></a>Pig işleri için hdınsight'ta Hadoop Hello .NET SDK kullanarak çalıştırma

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

TooHadoop Azure hdınsight'ta Hadoop toosubmit Apache Pig toouse Merhaba .NET SDK'sı nasıl işler öğrenin.

Merhaba Hdınsight .NET SDK'sı .NET gelen Hdınsight kümeleri ile daha kolay toowork kolaylaştırır .NET istemci kitaplıkları sağlar. Pig veri dönüşümleri bir dizi modelleme tarafından toocreate MapReduce işlemler sağlar. Bu belgede nasıl toouse temel C# uygulama toosubmit bir Pig proje tooan Hdınsight kümesi öğrenin.

## <a name="prerequisites"></a>Ön koşullar

Bu makaledeki toocomplete hello adımları, hello aşağıdaki gerekir.

* Azure Hdınsight (Hadoop hdınsight) kümesi (ya da Windows veya Linux tabanlı).

  > [!IMPORTANT]
  > Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Visual Studio 2012 2013, 2015 veya 2017.

## <a name="create-hello-application"></a>Merhaba uygulaması oluşturma

Merhaba Hdınsight .NET SDK'sı .NET istemci kitaplıkları, .NET gelen Hdınsight kümeleri ile daha kolay toowork olmasını sağlayan sağlar.

1. Merhaba gelen **dosya** menü Visual Studio'da seçin **yeni** ve ardından **proje**.

2. Hello yeni proje için değerleri yazın veya aşağıdaki select hello:

   | Özellik | Değer |
   | ------ | ------ |
   | Kategori | Şablonlar/Visual C#/Windows |
   | Şablon | Konsol Uygulaması |
   | Ad | SubmitPigJob |

3. Tıklatın **Tamam** toocreate hello projesi.

4. Merhaba gelen **Araçları** menüsünde, select **kitaplık Paket Yöneticisi** veya **Nuget Paket Yöneticisi**ve ardından **Paket Yöneticisi Konsolu**.

5. tooinstall hello .NET SDK'sı paketleri, komutu aşağıdaki hello kullan:

        Install-Package Microsoft.Azure.Management.HDInsight.Job

6. Çözüm Gezgini'nde, çift **Program.cs** tooopen onu. Merhaba var olan kodu hello şununla değiştirin.

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

7. toostart Merhaba uygulaması, basın **F5**.

8. tooexit Merhaba uygulaması, basın **ENTER**.

## <a name="summary"></a>Özet

Gördüğünüz gibi hello Hadoop için .NET SDK'sı, Pig işleri tooan Hdınsight kümesi gönderin ve hello iş durumunu izlemek toocreate .NET uygulamalarını sağlar.

## <a name="next-steps"></a>Sonraki adımlar

Hdınsight'ta Pig hakkında daha fazla bilgi için bkz: [hdınsight'ta Hadoop ile Pig kullanma](hdinsight-use-pig.md).

Hdınsight'ta Hadoop kullanma hakkında daha fazla bilgi için aşağıdaki belgeleri hello bakın:

* [Hdınsight'ta Hadoop ile Hive kullanma](hdinsight-use-hive.md)
* [Hdınsight'ta Hadoop ile MapReduce kullanma](hdinsight-use-mapreduce.md)

[preview-portal]: https://portal.azure.com/
