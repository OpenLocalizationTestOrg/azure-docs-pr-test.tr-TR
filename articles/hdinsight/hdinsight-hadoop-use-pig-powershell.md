---
title: "Hadoop Pig hdınsight'ta - Azure PowerShell ile kullanma | Microsoft Docs"
description: "Azure PowerShell kullanarak hdınsight'ta Hadoop kümesi pig iş göndermek öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 737089c1-b494-4387-9def-7b4dac3be532
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 28904b07609ffb40a8195278fd1afd3957896733
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-powershell-to-run-pig-jobs-with-hdinsight"></a><span data-ttu-id="4855a-103">Hdınsight ile Pig işlerini çalıştırmak için Azure PowerShell'i kullanma</span><span class="sxs-lookup"><span data-stu-id="4855a-103">Use Azure PowerShell to run Pig jobs with HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="4855a-104">Bu belge, Azure PowerShell kullanarak Hdınsight kümesinde bir Hadoop Pig işleri göndermek için bir örnek sağlar.</span><span class="sxs-lookup"><span data-stu-id="4855a-104">This document provides an example of using Azure PowerShell to submit Pig jobs to a Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="4855a-105">Pig, MapReduce işleri dili (Pig Latin) kullanarak bu modeller veri dönüşümleri yazmak yerine eşleme ve İşlevler azaltmak sağlar.</span><span class="sxs-lookup"><span data-stu-id="4855a-105">Pig allows you to write MapReduce jobs by using a language (Pig Latin) that models data transformations, rather than map and reduce functions.</span></span>

> [!NOTE]
> <span data-ttu-id="4855a-106">Bu belgedeki örneklerde kullanılan Pig Latin deyimleri ne ayrıntılı bir açıklama sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="4855a-106">This document does not provide a detailed description of what the Pig Latin statements used in the examples do.</span></span> <span data-ttu-id="4855a-107">Bu örnekte kullanılan Pig Latin hakkında daha fazla bilgi için bkz: [hdınsight'ta Hadoop ile Pig kullanma](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="4855a-107">For information about the Pig Latin used in this example, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

## <span data-ttu-id="4855a-108"><a id="prereq"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="4855a-108"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="4855a-109">**Azure Hdınsight kümesi**</span><span class="sxs-lookup"><span data-stu-id="4855a-109">**An Azure HDInsight cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="4855a-110">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="4855a-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4855a-111">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="4855a-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="4855a-112">**Azure PowerShell içeren bir iş istasyonu**.</span><span class="sxs-lookup"><span data-stu-id="4855a-112">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <span data-ttu-id="4855a-113"><a id="powershell"></a>PowerShell kullanarak Pig işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="4855a-113"><a id="powershell"></a>Run Pig jobs using PowerShell</span></span>

<span data-ttu-id="4855a-114">Azure PowerShell sağlar *cmdlet'leri* Hdınsight'ta Pig işleri uzaktan çalıştırma izin verir.</span><span class="sxs-lookup"><span data-stu-id="4855a-114">Azure PowerShell provides *cmdlets* that allow you to remotely run Pig jobs on HDInsight.</span></span> <span data-ttu-id="4855a-115">Dahili olarak, PowerShell REST çağrılarını kullanır [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) Hdınsight kümesinde çalışan.</span><span class="sxs-lookup"><span data-stu-id="4855a-115">Internally, PowerShell uses REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) running on the HDInsight cluster.</span></span>

<span data-ttu-id="4855a-116">Aşağıdaki cmdlet, Pig işleri uzaktan bir Hdınsight kümesine çalıştırılırken kullanılır:</span><span class="sxs-lookup"><span data-stu-id="4855a-116">The following cmdlets are used when running Pig jobs on a remote HDInsight cluster:</span></span>

* <span data-ttu-id="4855a-117">**Login-AzureRmAccount**: Azure PowerShell'i Azure aboneliğiniz için kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="4855a-117">**Login-AzureRmAccount**: Authenticates Azure PowerShell to your Azure Subscription</span></span>
* <span data-ttu-id="4855a-118">**AzureRmHDInsightPigJobDefinition yeni**: oluşturur bir *iş tanımı* belirtilen Pig Latin deyimleri kullanarak</span><span class="sxs-lookup"><span data-stu-id="4855a-118">**New-AzureRmHDInsightPigJobDefinition**: Creates a *job definition* by using the specified Pig Latin statements</span></span>
* <span data-ttu-id="4855a-119">**Başlangıç AzureRmHDInsightJob**: iş tanımı için Hdınsight gönderir, işini başlatır ve döndüren bir *iş* işinin durumunu denetlemek için kullanılan nesne</span><span class="sxs-lookup"><span data-stu-id="4855a-119">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight, starts the job, and returns a *job* object that can be used to check the status of the job</span></span>
* <span data-ttu-id="4855a-120">**Bekleme AzureRmHDInsightJob**: iş nesnesi işinin durumunu denetlemek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="4855a-120">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span></span> <span data-ttu-id="4855a-121">İş tamamlandı ya da bekleme süresi aşıldı kadar bekler.</span><span class="sxs-lookup"><span data-stu-id="4855a-121">It waits until the job has completed, or the wait time has been exceeded.</span></span>
* <span data-ttu-id="4855a-122">**Get-AzureRmHDInsightJobOutput**: işlemin çıktısını almak için kullanılır</span><span class="sxs-lookup"><span data-stu-id="4855a-122">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job</span></span>

<span data-ttu-id="4855a-123">Aşağıdaki adımlarda bu cmdlet'leri, Hdınsight kümesinde bir işi çalıştırmak için nasıl kullanılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="4855a-123">The following steps demonstrate how to use these cmdlets to run a job on your HDInsight cluster.</span></span>

1. <span data-ttu-id="4855a-124">Bir düzenleyici kullanarak aşağıdaki kodu olarak Kaydet **pigjob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="4855a-124">Using an editor, save the following code as **pigjob.ps1**.</span></span>

    <span data-ttu-id="4855a-125">[!code-powershell[Ana](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]</span><span class="sxs-lookup"><span data-stu-id="4855a-125">[!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]</span></span>

1. <span data-ttu-id="4855a-126">Yeni bir Windows PowerShell komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="4855a-126">Open a new Windows PowerShell command prompt.</span></span> <span data-ttu-id="4855a-127">Dizin konumuna değiştirme **pigjob.ps1** dosya sonra komut dosyasını çalıştırmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="4855a-127">Change directories to the location of the **pigjob.ps1** file, then use the following command to run the script:</span></span>

        .\pigjob.ps1

    <span data-ttu-id="4855a-128">Azure aboneliğinizde oturum istenir.</span><span class="sxs-lookup"><span data-stu-id="4855a-128">You are prompted to log in to your Azure subscription.</span></span> <span data-ttu-id="4855a-129">Ardından, HTTPs/Yönetici hesap adı ve Hdınsight kümesi için parola istenir.</span><span class="sxs-lookup"><span data-stu-id="4855a-129">Then, you are asked for the HTTPs/Admin account name and password for the HDInsight cluster.</span></span>

2. <span data-ttu-id="4855a-130">İş tamamlandığında, bilgileri aşağıdaki metni benzer döndürmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="4855a-130">When the job completes, it should return information similar to the following text:</span></span>

        Start the Pig job ...
        Wait for the Pig job to complete ...
        Display the standard output ...
        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="4855a-131"><a id="troubleshooting"></a>Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="4855a-131"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="4855a-132">İş tamamlandığında hiçbir bilgi döndürülürse, işleme sırasında bir hata oluşmuş olabilir.</span><span class="sxs-lookup"><span data-stu-id="4855a-132">If no information is returned when the job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="4855a-133">Bu işi için hata bilgilerini görüntülemek için aşağıdaki komutu sonuna ekleyin **pigjob.ps1** dosya, dosyayı kaydedin ve yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4855a-133">To view error information for this job, add the following command to the end of the **pigjob.ps1** file, save it, and then run it again.</span></span>

    # Print the output of the Pig job.
    Write-Host "Display the standard error output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
            -Clustername $clusterName `
            -JobId $pigJob.JobId `
            -HttpCredential $creds `
            -DisplayOutputType StandardError

<span data-ttu-id="4855a-134">Bu iş çalıştırıldığında STDERR sunucuda yazıldı bilgileri döndürür ve iş neden başarısız olduğunu belirlemenize yardımcı.</span><span class="sxs-lookup"><span data-stu-id="4855a-134">This returns the information that was written to STDERR on the server when you ran the job, and it may help determine why the job is failing.</span></span>

## <span data-ttu-id="4855a-135"><a id="summary"></a>Özet</span><span class="sxs-lookup"><span data-stu-id="4855a-135"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="4855a-136">Gördüğünüz gibi Azure PowerShell bir Hdınsight kümesine Pig işleri çalıştırma, iş durumunu izleyebilir ve çıkış almak için kolay bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="4855a-136">As you can see, Azure PowerShell provides an easy way to run Pig jobs on an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <span data-ttu-id="4855a-137"><a id="nextsteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4855a-137"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="4855a-138">Hdınsight'ta Pig hakkında genel bilgi için:</span><span class="sxs-lookup"><span data-stu-id="4855a-138">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="4855a-139">Hdınsight'ta Hadoop ile pig kullanma</span><span class="sxs-lookup"><span data-stu-id="4855a-139">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="4855a-140">Diğer yolları hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4855a-140">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="4855a-141">Hdınsight'ta Hadoop ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="4855a-141">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="4855a-142">Hdınsight'ta Hadoop ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="4855a-142">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
