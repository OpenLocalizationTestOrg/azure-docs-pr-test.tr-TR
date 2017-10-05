---
title: "Hadoop - Azure Hdınsight ile MapReduce ve PowerShell kullanma | Microsoft Docs"
description: "PowerShell uzaktan MapReduce işleri Hdınsight'ta Hadoop ile çalıştırmak için nasıl kullanılacağını öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21b56d32-1785-4d44-8ae8-94467c12cfba
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: c3801573808709f29cb1e563ac803f225a28cafc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-powershell"></a><span data-ttu-id="36a9f-103">PowerShell kullanarak Hdınsight'ta Hadoop ile MapReduce işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="36a9f-103">Run MapReduce jobs with Hadoop on HDInsight using PowerShell</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="36a9f-104">Bu belge, Hdınsight kümesinde bir Hadoop MapReduce işi çalıştırmak için Azure PowerShell kullanarak bir örnek sağlar.</span><span class="sxs-lookup"><span data-stu-id="36a9f-104">This document provides an example of using Azure PowerShell to run a MapReduce job in a Hadoop on HDInsight cluster.</span></span>

## <span data-ttu-id="36a9f-105"><a id="prereq"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="36a9f-105"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="36a9f-106">**Azure Hdınsight (Hadoop hdınsight) kümesi**</span><span class="sxs-lookup"><span data-stu-id="36a9f-106">**An Azure HDInsight (Hadoop on HDInsight) cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="36a9f-107">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="36a9f-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="36a9f-108">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="36a9f-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="36a9f-109">**Azure PowerShell içeren bir iş istasyonu**.</span><span class="sxs-lookup"><span data-stu-id="36a9f-109">**A workstation with Azure PowerShell**.</span></span>

## <span data-ttu-id="36a9f-110"><a id="powershell"></a>Azure PowerShell kullanarak bir MapReduce işi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="36a9f-110"><a id="powershell"></a>Run a MapReduce job using Azure PowerShell</span></span>

<span data-ttu-id="36a9f-111">Azure PowerShell sağlar *cmdlet'leri* Hdınsight'ta MapReduce işleri uzaktan çalıştırma izin verir.</span><span class="sxs-lookup"><span data-stu-id="36a9f-111">Azure PowerShell provides *cmdlets* that allow you to remotely run MapReduce jobs on HDInsight.</span></span> <span data-ttu-id="36a9f-112">Dahili olarak, bu REST çağrılarını kullanarak gerçekleştirilir [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (Templeton adıysa) Hdınsight kümesinde çalışan.</span><span class="sxs-lookup"><span data-stu-id="36a9f-112">Internally, this is accomplished by using REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (formerly called Templeton) running on the HDInsight cluster.</span></span>

<span data-ttu-id="36a9f-113">Aşağıdaki cmdlet, MapReduce işleri uzaktan Hdınsight kümesinde çalıştırılırken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="36a9f-113">The following cmdlets are used when running MapReduce jobs in a remote HDInsight cluster.</span></span>

* <span data-ttu-id="36a9f-114">**Login-AzureRmAccount**: Azure PowerShell'i Azure aboneliğinize kimliğini doğrular.</span><span class="sxs-lookup"><span data-stu-id="36a9f-114">**Login-AzureRmAccount**: Authenticates Azure PowerShell to your Azure subscription.</span></span>

* <span data-ttu-id="36a9f-115">**AzureRmHDInsightMapReduceJobDefinition yeni**: yeni bir *iş tanımı* belirtilen MapReduce bilgileri kullanarak.</span><span class="sxs-lookup"><span data-stu-id="36a9f-115">**New-AzureRmHDInsightMapReduceJobDefinition**: Creates a new *job definition* by using the specified MapReduce information.</span></span>

* <span data-ttu-id="36a9f-116">**Başlangıç AzureRmHDInsightJob**: iş tanımı için Hdınsight gönderir, işini başlatır ve döndüren bir *iş* işinin durumunu denetlemek için kullanılan nesne.</span><span class="sxs-lookup"><span data-stu-id="36a9f-116">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight, starts the job, and returns a *job* object that can be used to check the status of the job.</span></span>

* <span data-ttu-id="36a9f-117">**Bekleme AzureRmHDInsightJob**: iş nesnesi işinin durumunu denetlemek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="36a9f-117">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span></span> <span data-ttu-id="36a9f-118">İş tamamlandığında veya bekleme süresi aşılırsa kadar bekler.</span><span class="sxs-lookup"><span data-stu-id="36a9f-118">It waits until the job completes or the wait time is exceeded.</span></span>

* <span data-ttu-id="36a9f-119">**Get-AzureRmHDInsightJobOutput**: işlemin çıktısını almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="36a9f-119">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job.</span></span>

<span data-ttu-id="36a9f-120">Aşağıdaki adımlarda bu cmdlet'leri Hdınsight kümenizdeki bir işi çalıştırmak için nasıl kullanılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="36a9f-120">The following steps demonstrate how to use these cmdlets to run a job in your HDInsight cluster.</span></span>

1. <span data-ttu-id="36a9f-121">Bir düzenleyici kullanarak aşağıdaki kodu olarak Kaydet **mapreducejob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="36a9f-121">Using an editor, save the following code as **mapreducejob.ps1**.</span></span>

    <span data-ttu-id="36a9f-122">[!code-powershell[Ana](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]</span><span class="sxs-lookup"><span data-stu-id="36a9f-122">[!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]</span></span>

2. <span data-ttu-id="36a9f-123">Yeni bir **Azure PowerShell** komut istemi.</span><span class="sxs-lookup"><span data-stu-id="36a9f-123">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="36a9f-124">Dizin konumuna değiştirme **mapreducejob.ps1** dosya sonra komut dosyasını çalıştırmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="36a9f-124">Change directories to the location of the **mapreducejob.ps1** file, then use the following command to run the script:</span></span>

        .\mapreducejob.ps1

    <span data-ttu-id="36a9f-125">Komut dosyasını çalıştırdığınızda, Hdınsight kümesi adını ve HTTPS/Yönetici hesap adı ve küme için parola istenir.</span><span class="sxs-lookup"><span data-stu-id="36a9f-125">When you run the script, you are prompted for the name of the HDInsight cluster and the HTTPS/Admin account name and password for the cluster.</span></span> <span data-ttu-id="36a9f-126">Ayrıca, Azure aboneliğinizin kimlik doğrulaması istenebilir.</span><span class="sxs-lookup"><span data-stu-id="36a9f-126">You may also be prompted to authenticate to your Azure subscription.</span></span>

3. <span data-ttu-id="36a9f-127">İş tamamlandığında, aşağıdakine benzer bir çıktı alırsınız:</span><span class="sxs-lookup"><span data-stu-id="36a9f-127">When the job completes, you receive output similar to the following text:</span></span>

        Cluster         : CLUSTERNAME
        ExitCode        : 0
        Name            : wordcount
        PercentComplete : map 100% reduce 100%
        Query           :
        State           : Completed
        StatusDirectory : f1ed2028-afe8-402f-a24b-13cc17858097
        SubmissionTime  : 12/5/2014 8:34:09 PM
        JobId           : job_1415949758166_0071

    <span data-ttu-id="36a9f-128">Bu çıktı, iş başarıyla tamamlandığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="36a9f-128">This output indicates that the job completed successfully.</span></span>

    > [!NOTE]
    > <span data-ttu-id="36a9f-129">Varsa **ExitCode** bir değer 0'dan bkz [sorun giderme](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="36a9f-129">If the **ExitCode** is a value other than 0, see [Troubleshooting](#troubleshooting).</span></span>

    <span data-ttu-id="36a9f-130">Bu örnek ayrıca indirilen dosyaları depolayan bir **çýktý.txt** komut dosyasını çalıştırmak dizindeki dosyayı.</span><span class="sxs-lookup"><span data-stu-id="36a9f-130">This example also stores the downloaded files to an **output.txt** file in the directory that you run the script from.</span></span>

### <a name="view-output"></a><span data-ttu-id="36a9f-131">Görünüm çıktı</span><span class="sxs-lookup"><span data-stu-id="36a9f-131">View output</span></span>

<span data-ttu-id="36a9f-132">Açık **çýktý.txt** sözcükler ve iş tarafından üretilen sayılar görmek için bir metin düzenleyicisinde dosya.</span><span class="sxs-lookup"><span data-stu-id="36a9f-132">Open the **output.txt** file in a text editor to see the words and counts produced by the job.</span></span>

> [!NOTE]
> <span data-ttu-id="36a9f-133">Bir MapReduce işi çıktı dosyalarını değişmez.</span><span class="sxs-lookup"><span data-stu-id="36a9f-133">The output files of a MapReduce job are immutable.</span></span> <span data-ttu-id="36a9f-134">Bu nedenle, bu örnek çalıştırırsanız, çıktı dosyası adını değiştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="36a9f-134">So if you rerun this sample, you need to change the name of the output file.</span></span>

## <span data-ttu-id="36a9f-135"><a id="troubleshooting"></a>Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="36a9f-135"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="36a9f-136">İş tamamlandığında hiçbir bilgi döndürülürse, işleme sırasında bir hata oluşmuş olabilir.</span><span class="sxs-lookup"><span data-stu-id="36a9f-136">If no information is returned when the job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="36a9f-137">Bu işi için hata bilgilerini görüntülemek için aşağıdaki komutu sonuna ekleyin **mapreducejob.ps1** dosya, dosyayı kaydedin ve yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="36a9f-137">To view error information for this job, add the following command to the end of the **mapreducejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print the output of the WordCount job.
Write-Host "Display the standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $wordCountJob.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="36a9f-138">Bu cmdlet iş çalıştırdığınızda, STDERR'e sunucuda yazıldı bilgiler döndürür ve iş neden başarısız olduğunu belirlemenize yardımcı.</span><span class="sxs-lookup"><span data-stu-id="36a9f-138">This cmdlet returns the information that was written to STDERR on the server when you ran the job, and it may help determine why the job is failing.</span></span>

## <span data-ttu-id="36a9f-139"><a id="summary"></a>Özet</span><span class="sxs-lookup"><span data-stu-id="36a9f-139"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="36a9f-140">Gördüğünüz gibi Azure PowerShell bir Hdınsight kümesine MapReduce işleri çalıştırma, iş durumunu izleyebilir ve çıkış almak için kolay bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="36a9f-140">As you can see, Azure PowerShell provides an easy way to run MapReduce jobs on an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <span data-ttu-id="36a9f-141"><a id="nextsteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="36a9f-141"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="36a9f-142">Hdınsight'ta MapReduce işleri hakkında genel bilgi için:</span><span class="sxs-lookup"><span data-stu-id="36a9f-142">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="36a9f-143">Hdınsight Hadoop MapReduce kullanın</span><span class="sxs-lookup"><span data-stu-id="36a9f-143">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="36a9f-144">Diğer yolları hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="36a9f-144">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="36a9f-145">Hdınsight'ta Hadoop ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="36a9f-145">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="36a9f-146">Hdınsight'ta Hadoop ile pig kullanma</span><span class="sxs-lookup"><span data-stu-id="36a9f-146">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
