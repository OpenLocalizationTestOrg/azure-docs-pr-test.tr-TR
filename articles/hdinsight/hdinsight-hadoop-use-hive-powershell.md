---
title: "Hdınsight'ta - Azure PowerShell ile Hadoop Hive kullanma | Microsoft Docs"
description: "Hdınsight'ta Hadoop Hive sorguları çalıştırmak için PowerShell kullanın."
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
ms.openlocfilehash: e1cb2e4a1fc82fb43082e79a5feba71b81b3eaa8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="run-hive-queries-using-powershell"></a><span data-ttu-id="c3764-103">PowerShell kullanarak Hive sorguları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="c3764-103">Run Hive queries using PowerShell</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="c3764-104">Bu belge, Hdınsight kümesinde bir Hadoop Hive sorguları çalıştırmak için Azure kaynak grubu modunda Azure PowerShell kullanarak bir örnek sağlar.</span><span class="sxs-lookup"><span data-stu-id="c3764-104">This document provides an example of using Azure PowerShell in the Azure Resource Group mode to run Hive queries in a Hadoop on HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="c3764-105">Bu belgedeki örneklerde kullanılan HiveQL ifadelerini ne ayrıntılı bir açıklama sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="c3764-105">This document does not provide a detailed description of what the HiveQL statements that are used in the examples do.</span></span> <span data-ttu-id="c3764-106">Bu örnekte kullanılan HiveQL hakkında daha fazla bilgi için bkz: [hdınsight'ta Hadoop ile Hive kullanma](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="c3764-106">For information on the HiveQL that is used in this example, see [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="c3764-107">**Önkoşullar**</span><span class="sxs-lookup"><span data-stu-id="c3764-107">**Prerequisites**</span></span>

* <span data-ttu-id="c3764-108">**Azure Hdınsight kümesi**: küme Windows olup olmaması önemli değil ya da Linux tabanlı.</span><span class="sxs-lookup"><span data-stu-id="c3764-108">**An Azure HDInsight cluster**: It does not matter whether the cluster is Windows or Linux-based.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="c3764-109">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="c3764-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c3764-110">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="c3764-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="c3764-111">**Azure PowerShell içeren bir iş istasyonu**.</span><span class="sxs-lookup"><span data-stu-id="c3764-111">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-hive-queries-using-azure-powershell"></a><span data-ttu-id="c3764-112">Azure PowerShell kullanarak Hive sorguları çalıştırma</span><span class="sxs-lookup"><span data-stu-id="c3764-112">Run Hive queries using Azure PowerShell</span></span>

<span data-ttu-id="c3764-113">Azure PowerShell sağlar *cmdlet'leri* uzaktan Hdınsight'ta Hive sorguları çalıştırmanıza izin verir.</span><span class="sxs-lookup"><span data-stu-id="c3764-113">Azure PowerShell provides *cmdlets* that allow you to remotely run Hive queries on HDInsight.</span></span> <span data-ttu-id="c3764-114">Dahili olarak, cmdlet'ler REST çağrı yapmak [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) Hdınsight kümesinde.</span><span class="sxs-lookup"><span data-stu-id="c3764-114">Internally, the cmdlets make REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) on the HDInsight cluster.</span></span>

<span data-ttu-id="c3764-115">Aşağıdaki cmdlet, Hive sorguları bir uzak Hdınsight kümesinde çalıştırılırken kullanılır:</span><span class="sxs-lookup"><span data-stu-id="c3764-115">The following cmdlets are used when running Hive queries in a remote HDInsight cluster:</span></span>

* <span data-ttu-id="c3764-116">**Add-AzureRmAccount**: Azure PowerShell'i Azure aboneliğinize doğrular</span><span class="sxs-lookup"><span data-stu-id="c3764-116">**Add-AzureRmAccount**: Authenticates Azure PowerShell to your Azure subscription</span></span>
* <span data-ttu-id="c3764-117">**AzureRmHDInsightHiveJobDefinition yeni**: oluşturur bir *iş tanımı* belirtilen HiveQL ifadelerini kullanarak</span><span class="sxs-lookup"><span data-stu-id="c3764-117">**New-AzureRmHDInsightHiveJobDefinition**: Creates a *job definition* by using the specified HiveQL statements</span></span>
* <span data-ttu-id="c3764-118">**Başlangıç AzureRmHDInsightJob**: iş tanımı için Hdınsight gönderir, işini başlatır ve döndüren bir *iş* işinin durumunu denetlemek için kullanılan nesne</span><span class="sxs-lookup"><span data-stu-id="c3764-118">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight, starts the job, and returns a *job* object that can be used to check the status of the job</span></span>
* <span data-ttu-id="c3764-119">**Bekleme AzureRmHDInsightJob**: iş nesnesi işinin durumunu denetlemek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="c3764-119">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span></span> <span data-ttu-id="c3764-120">İş tamamlandığında veya bekleme süresi aşılırsa kadar bekler.</span><span class="sxs-lookup"><span data-stu-id="c3764-120">It waits until the job completes or the wait time is exceeded.</span></span>
* <span data-ttu-id="c3764-121">**Get-AzureRmHDInsightJobOutput**: işlemin çıktısını almak için kullanılır</span><span class="sxs-lookup"><span data-stu-id="c3764-121">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job</span></span>
* <span data-ttu-id="c3764-122">**Çağırma AzureRmHDInsightHiveJob**: HiveQL ifadelerini çalıştırmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="c3764-122">**Invoke-AzureRmHDInsightHiveJob**: Used to run HiveQL statements.</span></span> <span data-ttu-id="c3764-123">Bu cmdlet blokları sorgu tamamlandıktan sonra sonuçları döndürür</span><span class="sxs-lookup"><span data-stu-id="c3764-123">This cmdlet blocks the query completes, then returns the results</span></span>
* <span data-ttu-id="c3764-124">**Kullanım AzureRmHDInsightCluster**: için kullanılacak geçerli küme ayarlar **Invoke-AzureRmHDInsightHiveJob** komutu</span><span class="sxs-lookup"><span data-stu-id="c3764-124">**Use-AzureRmHDInsightCluster**: Sets the current cluster to use for the **Invoke-AzureRmHDInsightHiveJob** command</span></span>

<span data-ttu-id="c3764-125">Aşağıdaki adımlarda, bu cmdlet'ler, Hdınsight kümesinde bir işi çalıştırmak için nasıl kullanılacağı gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="c3764-125">The following steps demonstrate how to use these cmdlets to run a job in your HDInsight cluster:</span></span>

1. <span data-ttu-id="c3764-126">Bir düzenleyici kullanarak aşağıdaki kodu olarak Kaydet **hivejob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="c3764-126">Using an editor, save the following code as **hivejob.ps1**.</span></span>

    <span data-ttu-id="c3764-127">[!code-powershell[Ana](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]</span><span class="sxs-lookup"><span data-stu-id="c3764-127">[!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]</span></span>

2. <span data-ttu-id="c3764-128">Yeni bir **Azure PowerShell** komut istemi.</span><span class="sxs-lookup"><span data-stu-id="c3764-128">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="c3764-129">Dizin konumuna değiştirme **hivejob.ps1** dosya sonra komut dosyasını çalıştırmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="c3764-129">Change directories to the location of the **hivejob.ps1** file, then use the following command to run the script:</span></span>

        .\hivejob.ps1

    <span data-ttu-id="c3764-130">Komut dosyası çalıştığında, küme için küme adı ve HTTPS/yönetici hesabı kimlik bilgileri girmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="c3764-130">When the script runs, you are prompted to enter the cluster name and the HTTPS/Admin account credentials for the cluster.</span></span> <span data-ttu-id="c3764-131">Ayrıca Azure aboneliğinizde oturum istenebilir.</span><span class="sxs-lookup"><span data-stu-id="c3764-131">You may also be prompted to log in to your Azure subscription.</span></span>

3. <span data-ttu-id="c3764-132">İş tamamlandığında, bilgileri aşağıdaki thext benzer döndürür:</span><span class="sxs-lookup"><span data-stu-id="c3764-132">When the job completes, it returns information similar to the following thext:</span></span>

        Display the standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. <span data-ttu-id="c3764-133">Daha önce belirtildiği gibi **Invoke-Hive** bir sorgu çalıştırın ve yanıt için beklemek için kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="c3764-133">As mentioned earlier, **Invoke-Hive** can be used to run a query and wait for the response.</span></span> <span data-ttu-id="c3764-134">Invoke-Hive nasıl çalıştığını görmek için aşağıdaki komut dosyasını kullanın:</span><span class="sxs-lookup"><span data-stu-id="c3764-134">Use the following script to see how Invoke-Hive works:</span></span>

    <span data-ttu-id="c3764-135">[!code-powershell[Ana](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]</span><span class="sxs-lookup"><span data-stu-id="c3764-135">[!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]</span></span>

    <span data-ttu-id="c3764-136">Çıktı aşağıdaki metni gibi görünür:</span><span class="sxs-lookup"><span data-stu-id="c3764-136">The output looks like the following text:</span></span>

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > <span data-ttu-id="c3764-137">Uzun HiveQL sorgular için Azure PowerShell'i kullanabilirsiniz **burada dizeleri** cmdlet veya HiveQL komut dosyaları.</span><span class="sxs-lookup"><span data-stu-id="c3764-137">For longer HiveQL queries, you can use the Azure PowerShell **Here-Strings** cmdlet or HiveQL script files.</span></span> <span data-ttu-id="c3764-138">Aşağıdaki kod parçacığını nasıl kullanılacağını gösterir **Invoke-Hive** cmdlet'ini HiveQL komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c3764-138">The following snippet shows how to use the **Invoke-Hive** cmdlet to run a HiveQL script file.</span></span> <span data-ttu-id="c3764-139">HiveQL komut dosyası için wasb yüklenmelidir: / /.</span><span class="sxs-lookup"><span data-stu-id="c3764-139">The HiveQL script file must be uploaded to wasb://.</span></span>
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasb://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > <span data-ttu-id="c3764-140">Hakkında daha fazla bilgi için **burada dizeleri**, bkz: <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">kullanarak Windows PowerShell burada-dizeleri</a>.</span><span class="sxs-lookup"><span data-stu-id="c3764-140">For more information about **Here-Strings**, see <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Using Windows PowerShell Here-Strings</a>.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="c3764-141">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="c3764-141">Troubleshooting</span></span>

<span data-ttu-id="c3764-142">İş tamamlandığında hiçbir bilgi döndürülürse, işleme sırasında bir hata oluşmuş olabilir.</span><span class="sxs-lookup"><span data-stu-id="c3764-142">If no information is returned when the job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="c3764-143">Bu işi için hata bilgilerini görüntülemek için aşağıdaki sonuna ekleyin **hivejob.ps1** dosya, dosyayı kaydedin ve yeniden çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="c3764-143">To view error information for this job, add the following to the end of the **hivejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print the output of the Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="c3764-144">Bu cmdlet iş çalıştırdığınızda STDERR sunucuda yazılır bilgileri döndürür.</span><span class="sxs-lookup"><span data-stu-id="c3764-144">This cmdlet returns the information that is written to STDERR on the server when you ran the job.</span></span>

## <a name="summary"></a><span data-ttu-id="c3764-145">Özet</span><span class="sxs-lookup"><span data-stu-id="c3764-145">Summary</span></span>

<span data-ttu-id="c3764-146">Gördüğünüz gibi Azure PowerShell bir Hdınsight kümesi Hive sorgularını çalıştırma, iş durumunu izleyebilir ve çıkış almak için kolay bir yol sağlar.</span><span class="sxs-lookup"><span data-stu-id="c3764-146">As you can see, Azure PowerShell provides an easy way to run Hive queries in an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3764-147">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c3764-147">Next steps</span></span>

<span data-ttu-id="c3764-148">Hdınsight'ta Hive hakkında genel bilgi için:</span><span class="sxs-lookup"><span data-stu-id="c3764-148">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="c3764-149">Hdınsight'ta Hadoop ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="c3764-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="c3764-150">Diğer yolları hakkında bilgi için hdınsight'ta Hadoop ile çalışabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="c3764-150">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="c3764-151">Hdınsight'ta Hadoop ile pig kullanma</span><span class="sxs-lookup"><span data-stu-id="c3764-151">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="c3764-152">Hdınsight'ta Hadoop ile MapReduce kullanma</span><span class="sxs-lookup"><span data-stu-id="c3764-152">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
