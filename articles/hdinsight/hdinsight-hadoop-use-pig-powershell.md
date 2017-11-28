---
title: "aaaUse Hadoop Pig hdınsight'ta - Azure PowerShell ile | Microsoft Docs"
description: "Nasıl toosubmit Pig işleri tooa Hadoop küme Azure PowerShell kullanarak Hdınsight'ta öğrenin."
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
ms.openlocfilehash: 771617df203011eaec715a0dba6f5014a42877f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-powershell-toorun-pig-jobs-with-hdinsight"></a><span data-ttu-id="4cdb9-103">Hdınsight ile Azure PowerShell toorun Pig işleri kullanma</span><span class="sxs-lookup"><span data-stu-id="4cdb9-103">Use Azure PowerShell toorun Pig jobs with HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="4cdb9-104">Bu belge, Azure PowerShell toosubmit Pig işleri tooa Hadoop Hdınsight kümesinde kullanmaya ilişkin bir örnek sağlar.</span><span class="sxs-lookup"><span data-stu-id="4cdb9-104">This document provides an example of using Azure PowerShell toosubmit Pig jobs tooa Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="4cdb9-105">Pig veri dönüşümleri modeller bir dili (Pig Latin) kullanılarak toowrite MapReduce işleri verir yerine harita ve işlevleri azaltır.</span><span class="sxs-lookup"><span data-stu-id="4cdb9-105">Pig allows you toowrite MapReduce jobs by using a language (Pig Latin) that models data transformations, rather than map and reduce functions.</span></span>

> [!NOTE]
> <span data-ttu-id="4cdb9-106">Bu belgede ayrıntılı açıklamasını hello örneklerde kullanılan hello Pig Latin ifadeleri ne sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="4cdb9-106">This document does not provide a detailed description of what hello Pig Latin statements used in hello examples do.</span></span> <span data-ttu-id="4cdb9-107">Bu örnekte kullanılan Pig Latin hello hakkında daha fazla bilgi için bkz: [hdınsight'ta Hadoop ile Pig kullanma](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="4cdb9-107">For information about hello Pig Latin used in this example, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

## <span data-ttu-id="4cdb9-108"><a id="prereq"></a>Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="4cdb9-108"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="4cdb9-109">**Azure Hdınsight kümesi**</span><span class="sxs-lookup"><span data-stu-id="4cdb9-109">**An Azure HDInsight cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="4cdb9-110">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="4cdb9-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4cdb9-111">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="4cdb9-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="4cdb9-112">**Azure PowerShell içeren bir iş istasyonu**.</span><span class="sxs-lookup"><span data-stu-id="4cdb9-112">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <span data-ttu-id="4cdb9-113"><a id="powershell"></a>PowerShell kullanarak Pig işleri çalıştırma</span><span class="sxs-lookup"><span data-stu-id="4cdb9-113"><a id="powershell"></a>Run Pig jobs using PowerShell</span></span>

<span data-ttu-id="4cdb9-114">Azure PowerShell sağlar *cmdlet'leri* olanak tanıyacak şekilde çalıştırın tooremotely Pig işleri Hdınsight'ta.</span><span class="sxs-lookup"><span data-stu-id="4cdb9-114">Azure PowerShell provides *cmdlets* that allow you tooremotely run Pig jobs on HDInsight.</span></span> <span data-ttu-id="4cdb9-115">Dahili olarak, PowerShell REST çağrılarını çok kullanır[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) hello Hdınsight kümesinde çalışan.</span><span class="sxs-lookup"><span data-stu-id="4cdb9-115">Internally, PowerShell uses REST calls too[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) running on hello HDInsight cluster.</span></span>

<span data-ttu-id="4cdb9-116">Merhaba aşağıdaki cmdlet'leri uzak bir Hdınsight kümesine Pig işleri çalıştırma sırasında kullanılır:</span><span class="sxs-lookup"><span data-stu-id="4cdb9-116">hello following cmdlets are used when running Pig jobs on a remote HDInsight cluster:</span></span>

* <span data-ttu-id="4cdb9-117">**Login-AzureRmAccount**: Azure PowerShell kimliğini doğrulayan tooyour Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="4cdb9-117">**Login-AzureRmAccount**: Authenticates Azure PowerShell tooyour Azure Subscription</span></span>
* <span data-ttu-id="4cdb9-118">**AzureRmHDInsightPigJobDefinition yeni**: oluşturur bir *iş tanımı* hello kullanarak belirtilen Pig Latin deyimleri</span><span class="sxs-lookup"><span data-stu-id="4cdb9-118">**New-AzureRmHDInsightPigJobDefinition**: Creates a *job definition* by using hello specified Pig Latin statements</span></span>
* <span data-ttu-id="4cdb9-119">**Başlangıç AzureRmHDInsightJob**: hello iş tanımı tooHDInsight gönderir, hello işini başlatır ve döndürür bir *iş* kullanılan toocheck hello hello işinin durumunu olabilir nesnesi</span><span class="sxs-lookup"><span data-stu-id="4cdb9-119">**Start-AzureRmHDInsightJob**: Sends hello job definition tooHDInsight, starts hello job, and returns a *job* object that can be used toocheck hello status of hello job</span></span>
* <span data-ttu-id="4cdb9-120">**Bekleme AzureRmHDInsightJob**: hello iş nesnesi toocheck hello hello işinin durumunu kullanır.</span><span class="sxs-lookup"><span data-stu-id="4cdb9-120">**Wait-AzureRmHDInsightJob**: Uses hello job object toocheck hello status of hello job.</span></span> <span data-ttu-id="4cdb9-121">Merhaba işi tamamlandı veya hello bekleme zamanı aşıldı kadar bekler.</span><span class="sxs-lookup"><span data-stu-id="4cdb9-121">It waits until hello job has completed, or hello wait time has been exceeded.</span></span>
* <span data-ttu-id="4cdb9-122">**Get-AzureRmHDInsightJobOutput**: tooretrieve hello çıktısını hello kullanılan</span><span class="sxs-lookup"><span data-stu-id="4cdb9-122">**Get-AzureRmHDInsightJobOutput**: Used tooretrieve hello output of hello job</span></span>

<span data-ttu-id="4cdb9-123">Merhaba aşağıdaki adımları göstermek nasıl toouse bu cmdlet'leri toorun, Hdınsight kümesinde bir işi.</span><span class="sxs-lookup"><span data-stu-id="4cdb9-123">hello following steps demonstrate how toouse these cmdlets toorun a job on your HDInsight cluster.</span></span>

1. <span data-ttu-id="4cdb9-124">Bir düzenleyici kullanarak Kaydet kodu olarak aşağıdaki hello **pigjob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="4cdb9-124">Using an editor, save hello following code as **pigjob.ps1**.</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]

1. <span data-ttu-id="4cdb9-125">Yeni bir Windows PowerShell komut istemi açın.</span><span class="sxs-lookup"><span data-stu-id="4cdb9-125">Open a new Windows PowerShell command prompt.</span></span> <span data-ttu-id="4cdb9-126">Dizinleri toohello hello konumunu değiştirme **pigjob.ps1** dosya sonra toorun hello komut aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="4cdb9-126">Change directories toohello location of hello **pigjob.ps1** file, then use hello following command toorun hello script:</span></span>

        .\pigjob.ps1

    <span data-ttu-id="4cdb9-127">İstendiğinde toolog tooyour Azure aboneliği içindeki var.</span><span class="sxs-lookup"><span data-stu-id="4cdb9-127">You are prompted toolog in tooyour Azure subscription.</span></span> <span data-ttu-id="4cdb9-128">Ardından, hello HTTPs/Yönetici hesap adı ve parola hello Hdınsight kümesi için istenir.</span><span class="sxs-lookup"><span data-stu-id="4cdb9-128">Then, you are asked for hello HTTPs/Admin account name and password for hello HDInsight cluster.</span></span>

2. <span data-ttu-id="4cdb9-129">Merhaba işi tamamlandığında, metin aşağıdaki bilgileri benzer toohello döndürmesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="4cdb9-129">When hello job completes, it should return information similar toohello following text:</span></span>

        Start hello Pig job ...
        Wait for hello Pig job toocomplete ...
        Display hello standard output ...
        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="4cdb9-130"><a id="troubleshooting"></a>Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="4cdb9-130"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="4cdb9-131">Merhaba işi tamamlandığında hiçbir bilgi döndürülürse, işleme sırasında bir hata oluşmuş olabilir.</span><span class="sxs-lookup"><span data-stu-id="4cdb9-131">If no information is returned when hello job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="4cdb9-132">Bu iş için tooview hata bilgilerini Ekle komutu toohello hello sonuna aşağıdaki hello **pigjob.ps1** dosya, dosyayı kaydedin ve yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="4cdb9-132">tooview error information for this job, add hello following command toohello end of hello **pigjob.ps1** file, save it, and then run it again.</span></span>

    # Print hello output of hello Pig job.
    Write-Host "Display hello standard error output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
            -Clustername $clusterName `
            -JobId $pigJob.JobId `
            -HttpCredential $creds `
            -DisplayOutputType StandardError

<span data-ttu-id="4cdb9-133">Bu hello iş çalıştırdığınızda tooSTDERR hello sunucuda yazıldı hello bilgileri döndürür ve hello iş neden başarısız olduğunu belirlemenize yardımcı.</span><span class="sxs-lookup"><span data-stu-id="4cdb9-133">This returns hello information that was written tooSTDERR on hello server when you ran hello job, and it may help determine why hello job is failing.</span></span>

## <span data-ttu-id="4cdb9-134"><a id="summary"></a>Özet</span><span class="sxs-lookup"><span data-stu-id="4cdb9-134"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="4cdb9-135">Gördüğünüz gibi bir Hdınsight kümesi, hello iş durumunu izleyin ve alma hello çıktı Azure PowerShell kolay bir yolu toorun Pig işleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="4cdb9-135">As you can see, Azure PowerShell provides an easy way toorun Pig jobs on an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <span data-ttu-id="4cdb9-136"><a id="nextsteps"></a>Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="4cdb9-136"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="4cdb9-137">Hdınsight'ta Pig hakkında genel bilgi için:</span><span class="sxs-lookup"><span data-stu-id="4cdb9-137">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="4cdb9-138">Hdınsight'ta Hadoop ile pig kullanma</span><span class="sxs-lookup"><span data-stu-id="4cdb9-138">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="4cdb9-139">Diğer yolları hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="4cdb9-139">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="4cdb9-140">Hdınsight'ta Hadoop ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="4cdb9-140">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="4cdb9-141">Hdınsight'ta Hadoop ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="4cdb9-141">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
