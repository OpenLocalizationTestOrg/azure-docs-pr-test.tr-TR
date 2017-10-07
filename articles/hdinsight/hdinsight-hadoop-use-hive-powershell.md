---
title: "aaaUse Hadoop Hive hdınsight'ta - Azure PowerShell ile | Microsoft Docs"
description: "Hdınsight'ta Hadoop PowerShell toorun Hive sorguları kullanın."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cb795b7c-bcd0-497a-a7f0-8ed18ef49195
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 9e0b72a25c5b12431f837b1a34a63ecc06223528
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-powershell"></a><span data-ttu-id="39361-103">PowerShell kullanarak Hive sorguları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="39361-103">Run Hive queries using PowerShell</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="39361-104">Bu belge hello Azure kaynak grubu modu toorun Hive sorguları Hdınsight kümesinde bir Hadoop Azure PowerShell kullanarak bir örnek sağlar.</span><span class="sxs-lookup"><span data-stu-id="39361-104">This document provides an example of using Azure PowerShell in hello Azure Resource Group mode toorun Hive queries in a Hadoop on HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="39361-105">Bu belgede ayrıntılı açıklamasını hello örneklerde kullanılan hello HiveQL ifadelerini ne sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="39361-105">This document does not provide a detailed description of what hello HiveQL statements that are used in hello examples do.</span></span> <span data-ttu-id="39361-106">Bu örnekte kullanılan HiveQL hello hakkında daha fazla bilgi için bkz: [hdınsight'ta Hadoop ile Hive kullanma](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="39361-106">For information on hello HiveQL that is used in this example, see [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="39361-107">**Önkoşullar**</span><span class="sxs-lookup"><span data-stu-id="39361-107">**Prerequisites**</span></span>

* <span data-ttu-id="39361-108">**Azure Hdınsight kümesi**: Windows hello kümedir önemi değil veya Linux tabanlı.</span><span class="sxs-lookup"><span data-stu-id="39361-108">**An Azure HDInsight cluster**: It does not matter whether hello cluster is Windows or Linux-based.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="39361-109">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="39361-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="39361-110">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="39361-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="39361-111">**Azure PowerShell içeren bir iş istasyonu**.</span><span class="sxs-lookup"><span data-stu-id="39361-111">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-hive-queries-using-azure-powershell"></a><span data-ttu-id="39361-112">Azure PowerShell kullanarak Hive sorguları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="39361-112">Run Hive queries using Azure PowerShell</span></span>

<span data-ttu-id="39361-113">Azure PowerShell sağlar *cmdlet'leri* olanak tanıyacak şekilde çalıştırın tooremotely Hive sorguları Hdınsight'ta.</span><span class="sxs-lookup"><span data-stu-id="39361-113">Azure PowerShell provides *cmdlets* that allow you tooremotely run Hive queries on HDInsight.</span></span> <span data-ttu-id="39361-114">Dahili olarak, hello cmdlet'leri REST çok aramalarda[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) hello Hdınsight kümesi üzerinde.</span><span class="sxs-lookup"><span data-stu-id="39361-114">Internally, hello cmdlets make REST calls too[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) on hello HDInsight cluster.</span></span>

<span data-ttu-id="39361-115">Merhaba aşağıdaki cmdlet'leri Hive sorguları bir uzak Hdınsight kümesinde çalıştırılırken kullanılır:</span><span class="sxs-lookup"><span data-stu-id="39361-115">hello following cmdlets are used when running Hive queries in a remote HDInsight cluster:</span></span>

* <span data-ttu-id="39361-116">**Add-AzureRmAccount**: Azure PowerShell kimliğini doğrulayan tooyour Azure aboneliği</span><span class="sxs-lookup"><span data-stu-id="39361-116">**Add-AzureRmAccount**: Authenticates Azure PowerShell tooyour Azure subscription</span></span>
* <span data-ttu-id="39361-117">**AzureRmHDInsightHiveJobDefinition yeni**: oluşturur bir *iş tanımı* hello kullanılarak HiveQL ifadelerini belirtilen</span><span class="sxs-lookup"><span data-stu-id="39361-117">**New-AzureRmHDInsightHiveJobDefinition**: Creates a *job definition* by using hello specified HiveQL statements</span></span>
* <span data-ttu-id="39361-118">**Başlangıç AzureRmHDInsightJob**: hello iş tanımı tooHDInsight gönderir, hello işini başlatır ve döndürür bir *iş* kullanılan toocheck hello hello işinin durumunu olabilir nesnesi</span><span class="sxs-lookup"><span data-stu-id="39361-118">**Start-AzureRmHDInsightJob**: Sends hello job definition tooHDInsight, starts hello job, and returns a *job* object that can be used toocheck hello status of hello job</span></span>
* <span data-ttu-id="39361-119">**Bekleme AzureRmHDInsightJob**: hello iş nesnesi toocheck hello hello işinin durumunu kullanır.</span><span class="sxs-lookup"><span data-stu-id="39361-119">**Wait-AzureRmHDInsightJob**: Uses hello job object toocheck hello status of hello job.</span></span> <span data-ttu-id="39361-120">Merhaba işi tamamlar veya hello bekleme süresi aşılırsa kadar bekler.</span><span class="sxs-lookup"><span data-stu-id="39361-120">It waits until hello job completes or hello wait time is exceeded.</span></span>
* <span data-ttu-id="39361-121">**Get-AzureRmHDInsightJobOutput**: tooretrieve hello çıktısını hello kullanılan</span><span class="sxs-lookup"><span data-stu-id="39361-121">**Get-AzureRmHDInsightJobOutput**: Used tooretrieve hello output of hello job</span></span>
* <span data-ttu-id="39361-122">**Çağırma AzureRmHDInsightHiveJob**: toorun HiveQL ifadelerini kullanılır.</span><span class="sxs-lookup"><span data-stu-id="39361-122">**Invoke-AzureRmHDInsightHiveJob**: Used toorun HiveQL statements.</span></span> <span data-ttu-id="39361-123">Bu cmdlet blokları hello sorgu tamamlandıktan sonra hello sonuçlar döndürür</span><span class="sxs-lookup"><span data-stu-id="39361-123">This cmdlet blocks hello query completes, then returns hello results</span></span>
* <span data-ttu-id="39361-124">**Kullanım AzureRmHDInsightCluster**: kümeleri hello hello için geçerli küme toouse **Invoke-AzureRmHDInsightHiveJob** komutu</span><span class="sxs-lookup"><span data-stu-id="39361-124">**Use-AzureRmHDInsightCluster**: Sets hello current cluster toouse for hello **Invoke-AzureRmHDInsightHiveJob** command</span></span>

<span data-ttu-id="39361-125">Merhaba aşağıdaki adımları göstermek nasıl toouse bu cmdlet'leri toorun Hdınsight kümenize işinde:</span><span class="sxs-lookup"><span data-stu-id="39361-125">hello following steps demonstrate how toouse these cmdlets toorun a job in your HDInsight cluster:</span></span>

1. <span data-ttu-id="39361-126">Bir düzenleyici kullanarak Kaydet kodu olarak aşağıdaki hello **hivejob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="39361-126">Using an editor, save hello following code as **hivejob.ps1**.</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]

2. <span data-ttu-id="39361-127">Yeni bir **Azure PowerShell** komut istemi.</span><span class="sxs-lookup"><span data-stu-id="39361-127">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="39361-128">Dizinleri toohello hello konumunu değiştirme **hivejob.ps1** dosya sonra toorun hello komut aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="39361-128">Change directories toohello location of hello **hivejob.ps1** file, then use hello following command toorun hello script:</span></span>

        .\hivejob.ps1

    <span data-ttu-id="39361-129">Merhaba komut dosyası çalıştığında, istendiğinde tooenter hello küme adını ve hello HTTPS/yönetici hesabı kimlik bilgilerini hello küme demektir.</span><span class="sxs-lookup"><span data-stu-id="39361-129">When hello script runs, you are prompted tooenter hello cluster name and hello HTTPS/Admin account credentials for hello cluster.</span></span> <span data-ttu-id="39361-130">İstendiğinde toolog tooyour Azure aboneliği içindeki de olabilir.</span><span class="sxs-lookup"><span data-stu-id="39361-130">You may also be prompted toolog in tooyour Azure subscription.</span></span>

3. <span data-ttu-id="39361-131">Merhaba işi tamamlandığında thext aşağıdaki bilgileri benzer toohello döndürür:</span><span class="sxs-lookup"><span data-stu-id="39361-131">When hello job completes, it returns information similar toohello following thext:</span></span>

        Display hello standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. <span data-ttu-id="39361-132">Daha önce belirtildiği gibi **Invoke-Hive** sorguda kullanılan toorun kullanılabilir ve hello yanıtı bekleyin.</span><span class="sxs-lookup"><span data-stu-id="39361-132">As mentioned earlier, **Invoke-Hive** can be used toorun a query and wait for hello response.</span></span> <span data-ttu-id="39361-133">Invoke-Hive nasıl çalıştığını betik toosee aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="39361-133">Use hello following script toosee how Invoke-Hive works:</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]

    <span data-ttu-id="39361-134">Merhaba çıktı hello metin aşağıdaki gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="39361-134">hello output looks like hello following text:</span></span>

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > <span data-ttu-id="39361-135">Uzun HiveQL sorgularında hello Azure PowerShell kullanabilirsiniz **burada dizeleri** cmdlet veya HiveQL komut dosyaları.</span><span class="sxs-lookup"><span data-stu-id="39361-135">For longer HiveQL queries, you can use hello Azure PowerShell **Here-Strings** cmdlet or HiveQL script files.</span></span> <span data-ttu-id="39361-136">kod parçacığında gösterildiği nasıl aşağıdaki hello toouse hello **Invoke-Hive** cmdlet toorun HiveQL komut dosyası.</span><span class="sxs-lookup"><span data-stu-id="39361-136">hello following snippet shows how toouse hello **Invoke-Hive** cmdlet toorun a HiveQL script file.</span></span> <span data-ttu-id="39361-137">Merhaba komut dosyası olmalıdır HiveQL karşıya toowasb: / /.</span><span class="sxs-lookup"><span data-stu-id="39361-137">hello HiveQL script file must be uploaded toowasb://.</span></span>
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasb://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > <span data-ttu-id="39361-138">Hakkında daha fazla bilgi için **burada dizeleri**, bkz: <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">kullanarak Windows PowerShell burada-dizeleri</a>.</span><span class="sxs-lookup"><span data-stu-id="39361-138">For more information about **Here-Strings**, see <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Using Windows PowerShell Here-Strings</a>.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="39361-139">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="39361-139">Troubleshooting</span></span>

<span data-ttu-id="39361-140">Merhaba işi tamamlandığında hiçbir bilgi döndürülürse, işleme sırasında bir hata oluşmuş olabilir.</span><span class="sxs-lookup"><span data-stu-id="39361-140">If no information is returned when hello job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="39361-141">Bu iş için tooview hata bilgilerini ekleyin hello toohello sonuna aşağıdaki hello **hivejob.ps1** dosya, dosyayı kaydedin ve yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="39361-141">tooview error information for this job, add hello following toohello end of hello **hivejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print hello output of hello Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="39361-142">Bu cmdlet hello iş çalıştırdığınızda tooSTDERR hello sunucusuna yazılır hello bilgileri döndürür.</span><span class="sxs-lookup"><span data-stu-id="39361-142">This cmdlet returns hello information that is written tooSTDERR on hello server when you ran hello job.</span></span>

## <a name="summary"></a><span data-ttu-id="39361-143">Özet</span><span class="sxs-lookup"><span data-stu-id="39361-143">Summary</span></span>

<span data-ttu-id="39361-144">Gördüğünüz gibi Azure PowerShell kolay bir yolu toorun bir Hdınsight kümesindeki Hive sorguları sağlar, İzleyicisi Merhaba durumu iş ve hello çıkış almak.</span><span class="sxs-lookup"><span data-stu-id="39361-144">As you can see, Azure PowerShell provides an easy way toorun Hive queries in an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39361-145">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="39361-145">Next steps</span></span>

<span data-ttu-id="39361-146">Hdınsight'ta Hive hakkında genel bilgi için:</span><span class="sxs-lookup"><span data-stu-id="39361-146">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="39361-147">Hdınsight'ta Hadoop ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="39361-147">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="39361-148">Diğer yolları hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="39361-148">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="39361-149">Hdınsight'ta Hadoop ile pig kullanma</span><span class="sxs-lookup"><span data-stu-id="39361-149">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="39361-150">Hdınsight'ta Hadoop ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="39361-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
