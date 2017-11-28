---
title: "aaaUse MapReduce ve Hadoop - Azure Hdınsight ile PowerShell | Microsoft Docs"
description: "Toouse PowerShell tooremotely çalışma şeklini MapReduce işleri Hadoop ile Hdınsight'ta öğrenin."
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
ms.openlocfilehash: 59524f0e8813d4c017f92bccb2e50d4c018acf71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-powershell"></a><span data-ttu-id="301c2-103">PowerShell kullanarak Hdınsight'ta Hadoop ile MapReduce işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="301c2-103">Run MapReduce jobs with Hadoop on HDInsight using PowerShell</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="301c2-104">Bu belge, Hdınsight kümesinde bir Hadoop bir MapReduce işi Azure PowerShell toorun kullanmaya ilişkin bir örnek sağlar.</span><span class="sxs-lookup"><span data-stu-id="301c2-104">This document provides an example of using Azure PowerShell toorun a MapReduce job in a Hadoop on HDInsight cluster.</span></span>

## <span data-ttu-id="301c2-105"><a id="prereq"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="301c2-105"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="301c2-106">**Azure Hdınsight (Hadoop hdınsight) kümesi**</span><span class="sxs-lookup"><span data-stu-id="301c2-106">**An Azure HDInsight (Hadoop on HDInsight) cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="301c2-107">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="301c2-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="301c2-108">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="301c2-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="301c2-109">**Azure PowerShell içeren bir iş istasyonu**.</span><span class="sxs-lookup"><span data-stu-id="301c2-109">**A workstation with Azure PowerShell**.</span></span>

## <span data-ttu-id="301c2-110"><a id="powershell"></a>Azure PowerShell kullanarak bir MapReduce işi çalıştırma</span><span class="sxs-lookup"><span data-stu-id="301c2-110"><a id="powershell"></a>Run a MapReduce job using Azure PowerShell</span></span>

<span data-ttu-id="301c2-111">Azure PowerShell sağlar *cmdlet'leri* olanak tanıyacak şekilde çalıştırın tooremotely MapReduce işleri Hdınsight'ta.</span><span class="sxs-lookup"><span data-stu-id="301c2-111">Azure PowerShell provides *cmdlets* that allow you tooremotely run MapReduce jobs on HDInsight.</span></span> <span data-ttu-id="301c2-112">Dahili olarak, bu çok REST çağrılarını kullanarak gerçekleştirilir[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (Templeton adıysa) Hdınsight kümesi hello üzerinde çalışan.</span><span class="sxs-lookup"><span data-stu-id="301c2-112">Internally, this is accomplished by using REST calls too[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (formerly called Templeton) running on hello HDInsight cluster.</span></span>

<span data-ttu-id="301c2-113">Merhaba aşağıdaki cmdlet'ler MapReduce işleri uzaktan Hdınsight kümesinde çalıştırılırken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="301c2-113">hello following cmdlets are used when running MapReduce jobs in a remote HDInsight cluster.</span></span>

* <span data-ttu-id="301c2-114">**Login-AzureRmAccount**: Azure PowerShell kimliğini doğrulayan tooyour Azure aboneliği.</span><span class="sxs-lookup"><span data-stu-id="301c2-114">**Login-AzureRmAccount**: Authenticates Azure PowerShell tooyour Azure subscription.</span></span>

* <span data-ttu-id="301c2-115">**AzureRmHDInsightMapReduceJobDefinition yeni**: yeni bir *iş tanımı* hello kullanarak belirtilen MapReduce bilgi.</span><span class="sxs-lookup"><span data-stu-id="301c2-115">**New-AzureRmHDInsightMapReduceJobDefinition**: Creates a new *job definition* by using hello specified MapReduce information.</span></span>

* <span data-ttu-id="301c2-116">**Başlangıç AzureRmHDInsightJob**: hello iş tanımı tooHDInsight gönderir, hello işini başlatır ve döndürür bir *iş* kullanılan toocheck hello hello işinin durumunu olabilir nesnesi.</span><span class="sxs-lookup"><span data-stu-id="301c2-116">**Start-AzureRmHDInsightJob**: Sends hello job definition tooHDInsight, starts hello job, and returns a *job* object that can be used toocheck hello status of hello job.</span></span>

* <span data-ttu-id="301c2-117">**Bekleme AzureRmHDInsightJob**: hello iş nesnesi toocheck hello hello işinin durumunu kullanır.</span><span class="sxs-lookup"><span data-stu-id="301c2-117">**Wait-AzureRmHDInsightJob**: Uses hello job object toocheck hello status of hello job.</span></span> <span data-ttu-id="301c2-118">Merhaba işi tamamlar veya hello bekleme süresi aşılırsa kadar bekler.</span><span class="sxs-lookup"><span data-stu-id="301c2-118">It waits until hello job completes or hello wait time is exceeded.</span></span>

* <span data-ttu-id="301c2-119">**Get-AzureRmHDInsightJobOutput**: tooretrieve hello çıktısını hello kullanılır.</span><span class="sxs-lookup"><span data-stu-id="301c2-119">**Get-AzureRmHDInsightJobOutput**: Used tooretrieve hello output of hello job.</span></span>

<span data-ttu-id="301c2-120">Merhaba aşağıdaki adımları göstermek nasıl toouse bu cmdlet'leri toorun Hdınsight kümenizdeki bir işi.</span><span class="sxs-lookup"><span data-stu-id="301c2-120">hello following steps demonstrate how toouse these cmdlets toorun a job in your HDInsight cluster.</span></span>

1. <span data-ttu-id="301c2-121">Bir düzenleyici kullanarak Kaydet kodu olarak aşağıdaki hello **mapreducejob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="301c2-121">Using an editor, save hello following code as **mapreducejob.ps1**.</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]

2. <span data-ttu-id="301c2-122">Yeni bir **Azure PowerShell** komut istemi.</span><span class="sxs-lookup"><span data-stu-id="301c2-122">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="301c2-123">Dizinleri toohello hello konumunu değiştirme **mapreducejob.ps1** dosya sonra toorun hello komut aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="301c2-123">Change directories toohello location of hello **mapreducejob.ps1** file, then use hello following command toorun hello script:</span></span>

        .\mapreducejob.ps1

    <span data-ttu-id="301c2-124">Merhaba komut çalıştırdığınızda hello hello Hdınsight küme adını ve hello HTTPS/Yönetici hesap adı ve parola hello kümesi için istenir.</span><span class="sxs-lookup"><span data-stu-id="301c2-124">When you run hello script, you are prompted for hello name of hello HDInsight cluster and hello HTTPS/Admin account name and password for hello cluster.</span></span> <span data-ttu-id="301c2-125">İstendiğinde tooauthenticate tooyour Azure aboneliği de olabilir.</span><span class="sxs-lookup"><span data-stu-id="301c2-125">You may also be prompted tooauthenticate tooyour Azure subscription.</span></span>

3. <span data-ttu-id="301c2-126">Merhaba işi tamamlandığında, çıkış benzer toohello metin aşağıdaki alırsınız:</span><span class="sxs-lookup"><span data-stu-id="301c2-126">When hello job completes, you receive output similar toohello following text:</span></span>

        Cluster         : CLUSTERNAME
        ExitCode        : 0
        Name            : wordcount
        PercentComplete : map 100% reduce 100%
        Query           :
        State           : Completed
        StatusDirectory : f1ed2028-afe8-402f-a24b-13cc17858097
        SubmissionTime  : 12/5/2014 8:34:09 PM
        JobId           : job_1415949758166_0071

    <span data-ttu-id="301c2-127">Bu çıktı, o hello işi başarıyla tamamlandı gösterir.</span><span class="sxs-lookup"><span data-stu-id="301c2-127">This output indicates that hello job completed successfully.</span></span>

    > [!NOTE]
    > <span data-ttu-id="301c2-128">Merhaba, **ExitCode** bir değer 0'dan bkz [sorun giderme](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="301c2-128">If hello **ExitCode** is a value other than 0, see [Troubleshooting](#troubleshooting).</span></span>

    <span data-ttu-id="301c2-129">Bu örnek ayrıca hello indirilen dosyaları tooan depolar **çýktý.txt** hello dizinindeki hello komut dosyasından çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="301c2-129">This example also stores hello downloaded files tooan **output.txt** file in hello directory that you run hello script from.</span></span>

### <a name="view-output"></a><span data-ttu-id="301c2-130">Görünüm çıktı</span><span class="sxs-lookup"><span data-stu-id="301c2-130">View output</span></span>

<span data-ttu-id="301c2-131">Açık hello **çýktý.txt** bir metin düzenleyicisi toosee hello dosyasında sözcükleri ve hello iş tarafından üretilen sayar.</span><span class="sxs-lookup"><span data-stu-id="301c2-131">Open hello **output.txt** file in a text editor toosee hello words and counts produced by hello job.</span></span>

> [!NOTE]
> <span data-ttu-id="301c2-132">Merhaba çıktı dosyalarını bir MapReduce işi değişmez.</span><span class="sxs-lookup"><span data-stu-id="301c2-132">hello output files of a MapReduce job are immutable.</span></span> <span data-ttu-id="301c2-133">Bu nedenle, bu örnek çalıştırırsanız, toochange hello hello çıktı dosyası adını gerekir.</span><span class="sxs-lookup"><span data-stu-id="301c2-133">So if you rerun this sample, you need toochange hello name of hello output file.</span></span>

## <span data-ttu-id="301c2-134"><a id="troubleshooting"></a>Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="301c2-134"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="301c2-135">Merhaba işi tamamlandığında hiçbir bilgi döndürülürse, işleme sırasında bir hata oluşmuş olabilir.</span><span class="sxs-lookup"><span data-stu-id="301c2-135">If no information is returned when hello job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="301c2-136">Bu iş için tooview hata bilgilerini Ekle komutu toohello hello sonuna aşağıdaki hello **mapreducejob.ps1** dosya, dosyayı kaydedin ve yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="301c2-136">tooview error information for this job, add hello following command toohello end of hello **mapreducejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print hello output of hello WordCount job.
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $wordCountJob.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="301c2-137">Bu cmdlet hello işi çalıştırdığınızda, tooSTDERR hello sunucuda yazıldı hello bilgiler döndürür ve hello iş neden başarısız olduğunu belirlemenize yardımcı.</span><span class="sxs-lookup"><span data-stu-id="301c2-137">This cmdlet returns hello information that was written tooSTDERR on hello server when you ran hello job, and it may help determine why hello job is failing.</span></span>

## <span data-ttu-id="301c2-138"><a id="summary"></a>Özet</span><span class="sxs-lookup"><span data-stu-id="301c2-138"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="301c2-139">Gördüğünüz gibi bir Hdınsight kümesi, hello iş durumunu izleyin ve alma hello çıktı Azure PowerShell kolay bir yolu toorun MapReduce işleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="301c2-139">As you can see, Azure PowerShell provides an easy way toorun MapReduce jobs on an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <span data-ttu-id="301c2-140"><a id="nextsteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="301c2-140"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="301c2-141">Hdınsight'ta MapReduce işleri hakkında genel bilgi için:</span><span class="sxs-lookup"><span data-stu-id="301c2-141">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="301c2-142">Hdınsight Hadoop MapReduce kullanın</span><span class="sxs-lookup"><span data-stu-id="301c2-142">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="301c2-143">Diğer yolları hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="301c2-143">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="301c2-144">Hdınsight'ta Hadoop ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="301c2-144">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="301c2-145">Hdınsight'ta Hadoop ile pig kullanma</span><span class="sxs-lookup"><span data-stu-id="301c2-145">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
