---
title: "PowerShell - Azure Hdınsight'ta Mahout kullanarak öneri oluşturmak | Microsoft Docs"
description: "İstemci üzerinde çalışan bir PowerShell komut dosyasından learning kitaplığı Apache Mahout makine Hdınsight (Hadoop) ile film önerileri oluşturma için nasıl kullanılacağını öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 07b57208-32aa-4e59-900a-6c934fa1b7a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 934de9ca2df48b29ef7a56d5729d59d77875ea7b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-hadoop-in-hdinsight-powershell"></a><span data-ttu-id="0b758-103">(PowerShell) hdınsight'ta Hadoop ile Apache Mahout kullanarak film önerileri oluşturma</span><span class="sxs-lookup"><span data-stu-id="0b758-103">Generate movie recommendations by using Apache Mahout with Hadoop in HDInsight (PowerShell)</span></span>

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

<span data-ttu-id="0b758-104">Nasıl kullanacağınızı öğrenin [Apache Mahout](http://mahout.apache.org) machine learning kitaplığı Azure Hdınsight'ın Film önerileri oluşturma ile.</span><span class="sxs-lookup"><span data-stu-id="0b758-104">Learn how to use the [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight to generate movie recommendations.</span></span> <span data-ttu-id="0b758-105">Bu belge örnekte Mahout işlerini çalıştırmak için Azure PowerShell'i kullanır.</span><span class="sxs-lookup"><span data-stu-id="0b758-105">The example in this document uses Azure PowerShell to run Mahout jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b758-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="0b758-106">Prerequisites</span></span>

* <span data-ttu-id="0b758-107">Linux tabanlı Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="0b758-107">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="0b758-108">Bir oluşturma hakkında daha fazla bilgi için bkz: [Hdınsight'ta Linux tabanlı Hadoop ile çalışmaya başlamak][getstarted].</span><span class="sxs-lookup"><span data-stu-id="0b758-108">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0b758-109">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="0b758-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0b758-110">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="0b758-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="0b758-111">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0b758-111">Azure PowerShell</span></span>](/powershell/azure/overview)

## <span data-ttu-id="0b758-112"><a name="recommendations"></a>Azure PowerShell kullanarak önerileri oluşturma</span><span class="sxs-lookup"><span data-stu-id="0b758-112"><a name="recommendations"></a>Generate recommendations by using Azure PowerShell</span></span>

> [!WARNING]
> <span data-ttu-id="0b758-113">Bu bölümde iş Azure PowerShell kullanarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="0b758-113">The job in this section works by using Azure PowerShell.</span></span> <span data-ttu-id="0b758-114">Mahout ile sağlanan sınıfların çoğu Azure PowerShell ile şu anda çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="0b758-114">Many of the classes provided with Mahout do not currently work with Azure PowerShell.</span></span> <span data-ttu-id="0b758-115">Azure PowerShell ile çalışmaz sınıfları listesi için bkz: [sorun giderme](#troubleshooting) bölümü.</span><span class="sxs-lookup"><span data-stu-id="0b758-115">For a list of classes that do not work with Azure PowerShell, see the [Troubleshooting](#troubleshooting) section.</span></span>
>
> <span data-ttu-id="0b758-116">Hdınsight ve çalışma Mahout örnekler küme üzerinde doğrudan bağlanmak için SSH kullanarak bir örnek için bkz: [Mahout ve Hdınsight (SSH) kullanarak film önerileri oluşturma](hdinsight-hadoop-mahout-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="0b758-116">For an example of using SSH to connect to HDInsight and run Mahout examples directly on the cluster, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span></span>

<span data-ttu-id="0b758-117">Mahout tarafından sağlanan işlevleri bir öneri altyapısı biridir.</span><span class="sxs-lookup"><span data-stu-id="0b758-117">One of the functions that is provided by Mahout is a recommendation engine.</span></span> <span data-ttu-id="0b758-118">Bu altyapı biçiminde verilerini kabul eden `userID`, `itemId`, ve `prefValue` (kullanıcılar tercih öğesi için).</span><span class="sxs-lookup"><span data-stu-id="0b758-118">This engine accepts data in the format of `userID`, `itemId`, and `prefValue` (the users preference for the item).</span></span> <span data-ttu-id="0b758-119">Mahout veri önerileri yapmak için kullanılan benzer öğe Tercihler kullanıcılarla belirlemek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="0b758-119">Mahout uses the data to determine users with like-item preferences, which can be used to make recommendations.</span></span>

<span data-ttu-id="0b758-120">Aşağıdaki örnek öneri işleminin nasıl çalıştığı, Basitleştirilmiş bir gözden geçirme verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="0b758-120">The following example is a simplified walk-through of how the recommendation process works:</span></span>

* <span data-ttu-id="0b758-121">**Ortak oluşumu**: Can, Alice ve Bob tüm beğendiğinizi *yıldız çatışmaları*, *geri Empire düşer*, ve *Jedi dönüşünü*.</span><span class="sxs-lookup"><span data-stu-id="0b758-121">**co-occurrence**: Joe, Alice, and Bob all liked *Star Wars*, *The Empire Strikes Back*, and *Return of the Jedi*.</span></span> <span data-ttu-id="0b758-122">Bu filmler herhangi biri de gibi kullanıcıların diğer iki ister mahout belirler.</span><span class="sxs-lookup"><span data-stu-id="0b758-122">Mahout determines that users who like any one of these movies also like the other two.</span></span>

* <span data-ttu-id="0b758-123">**Ortak oluşumu**: Bob ve Alice de beğendiğinizi *hayali İstilası*, *klonlar saldırı*, ve *Sith Revenge*.</span><span class="sxs-lookup"><span data-stu-id="0b758-123">**co-occurrence**: Bob and Alice also liked *The Phantom Menace*, *Attack of the Clones*, and *Revenge of the Sith*.</span></span> <span data-ttu-id="0b758-124">Önceki üç filmler de ilişkilendirilmiş kullanıcılar bu filmler ister mahout belirler.</span><span class="sxs-lookup"><span data-stu-id="0b758-124">Mahout determines that users who liked the previous three movies also like these movies.</span></span>

* <span data-ttu-id="0b758-125">**Benzerlik öneri**: çünkü Joe beğendiğinizi ilk üç filmler, Mahout o beğendiğinizi benzer Tercihler başkalarıyla filmler görünür, ancak Joe olmayan izlenen (beğendiğinizi/derecelendirilmiş).</span><span class="sxs-lookup"><span data-stu-id="0b758-125">**Similarity recommendation**: Because Joe liked the first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span></span> <span data-ttu-id="0b758-126">Bu durumda, Mahout önerir *hayali İstilası*, *klonlar saldırı*, ve *Sith Revenge*.</span><span class="sxs-lookup"><span data-stu-id="0b758-126">In this case, Mahout recommends *The Phantom Menace*, *Attack of the Clones*, and *Revenge of the Sith*.</span></span>

### <a name="understanding-the-data"></a><span data-ttu-id="0b758-127">Veri anlama</span><span class="sxs-lookup"><span data-stu-id="0b758-127">Understanding the data</span></span>

<span data-ttu-id="0b758-128">[GroupLens araştırma] [ movielens] Mahout ile uyumlu bir biçimde film derecelendirme veri sağlar.</span><span class="sxs-lookup"><span data-stu-id="0b758-128">[GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span></span> <span data-ttu-id="0b758-129">Bu verilerin varsayılan depolama konumunda kümenize için kullanılabilir `/HdiSamples//HdiSamples/MahoutMovieData`.</span><span class="sxs-lookup"><span data-stu-id="0b758-129">This data is available on the default storage for your cluster at `/HdiSamples//HdiSamples/MahoutMovieData`.</span></span>

<span data-ttu-id="0b758-130">İki dosya vardır `moviedb.txt` (filmler hakkındaki bilgiler) ve `user-ratings.txt`.</span><span class="sxs-lookup"><span data-stu-id="0b758-130">There are two files, `moviedb.txt` (information about the movies) and `user-ratings.txt`.</span></span> <span data-ttu-id="0b758-131">`user-ratings.txt` Dosyası Çözümleme sırasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0b758-131">The `user-ratings.txt` file is used during analysis.</span></span> <span data-ttu-id="0b758-132">`moviedb.txt` Dosya çözümleme sonuçlarını görüntülerken, kullanımı kolay metin sağlamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0b758-132">The `moviedb.txt` file is used to provide user-friendly text when displaying the results of the analysis.</span></span>

<span data-ttu-id="0b758-133">Kullanıcı-ratings.txt bulunan verileri yapısını sahip `userID`, `movieID`, `userRating`, ve `timestamp`, söyleyen bize nasıl yüksek oranda her kullanıcı bir filmi derecelendirilir.</span><span class="sxs-lookup"><span data-stu-id="0b758-133">The data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which tells us how highly each user rated a movie.</span></span> <span data-ttu-id="0b758-134">Verileri bir örneği burada verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="0b758-134">Here is an example of the data:</span></span>

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

### <a name="run-the-job"></a><span data-ttu-id="0b758-135">İşi çalıştır</span><span class="sxs-lookup"><span data-stu-id="0b758-135">Run the job</span></span>

<span data-ttu-id="0b758-136">Film verilerle Mahout öneri altyapısı kullanan bir iş çalıştırmak için aşağıdaki Windows PowerShell betiğini kullanın:</span><span class="sxs-lookup"><span data-stu-id="0b758-136">Use the following Windows PowerShell script to run a job that uses the Mahout recommendation engine with the movie data:</span></span>

> [!NOTE]
> <span data-ttu-id="0b758-137">Bu dosya Hdınsight kümenize bağlanmak ve işlerini çalıştırmak için kullanılan bilgileri ister.</span><span class="sxs-lookup"><span data-stu-id="0b758-137">This file prompts you for information that is used to connect to your HDInsight cluster and run jobs.</span></span> <span data-ttu-id="0b758-138">İşlerini tamamlayıp çıktı.txt dosyasını karşıdan yüklemek birkaç dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="0b758-138">It may take several minutes for the jobs to complete and download the output.txt file.</span></span>

<span data-ttu-id="0b758-139">[!code-powershell[Ana](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=5-98)]</span><span class="sxs-lookup"><span data-stu-id="0b758-139">[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=5-98)]</span></span>

> [!NOTE]
> <span data-ttu-id="0b758-140">Mahout işleri iş işlenirken oluşturulan geçici verileri kaldırmayın.</span><span class="sxs-lookup"><span data-stu-id="0b758-140">Mahout jobs do not remove temporary data that is created while processing the job.</span></span> <span data-ttu-id="0b758-141">`--tempDir` Parametresi geçici dosyalar belirli bir dizine yalıtmak için örnek proje belirtilen.</span><span class="sxs-lookup"><span data-stu-id="0b758-141">The `--tempDir` parameter is specified in the example job to isolate the temporary files into a specific directory.</span></span>

<span data-ttu-id="0b758-142">Mahout iş STDOUT çıktı döndürmez.</span><span class="sxs-lookup"><span data-stu-id="0b758-142">The Mahout job does not return the output to STDOUT.</span></span> <span data-ttu-id="0b758-143">Bunun yerine, belirtilen çıkış dizinine depolar **bölümü r 00000**.</span><span class="sxs-lookup"><span data-stu-id="0b758-143">Instead, it stores it in the specified output directory as **part-r-00000**.</span></span> <span data-ttu-id="0b758-144">Bu dosyaya betiğini indirir **çýktý.txt** istasyonunuzda geçerli dizin.</span><span class="sxs-lookup"><span data-stu-id="0b758-144">The script downloads this file to **output.txt** in the current directory on your workstation.</span></span>

<span data-ttu-id="0b758-145">Aşağıdaki metni, bu dosyanın içeriğini örneğidir:</span><span class="sxs-lookup"><span data-stu-id="0b758-145">The following text is an example of the content of this file:</span></span>

    1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
    2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
    3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
    4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

<span data-ttu-id="0b758-146">İlk sütun `userID`.</span><span class="sxs-lookup"><span data-stu-id="0b758-146">The first column is the `userID`.</span></span> <span data-ttu-id="0b758-147">İçinde yer alan değerler ' [' ve ']' olan `movieId`:`recommendationScore`.</span><span class="sxs-lookup"><span data-stu-id="0b758-147">The values contained in '[' and ']' are `movieId`:`recommendationScore`.</span></span>

<span data-ttu-id="0b758-148">Komut dosyası ayrıca indirmeleri `moviedb.txt` ve `user-ratings.txt` daha okunabilir olması için çıktı biçimlendirmek için gereken dosyalar.</span><span class="sxs-lookup"><span data-stu-id="0b758-148">The script also downloads the `moviedb.txt` and `user-ratings.txt` files, which are needed to format the output to be more readable.</span></span>

### <a name="view-the-output"></a><span data-ttu-id="0b758-149">Çıktısını görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="0b758-149">View the output</span></span>

<span data-ttu-id="0b758-150">Oluşturulan çıktı bir uygulamada kullanmak için Tamam olabilir, ancak kullanıcı dostu değil.</span><span class="sxs-lookup"><span data-stu-id="0b758-150">Although the generated output might be OK for use in an application, it's not user-friendly.</span></span> <span data-ttu-id="0b758-151">`moviedb.txt` Sunucudan çözümlemek için kullanılan `movieId` film adı.</span><span class="sxs-lookup"><span data-stu-id="0b758-151">The `moviedb.txt` from the server can be used to resolve the `movieId` to a movie name.</span></span> <span data-ttu-id="0b758-152">Film adları ile ilgili öneriler görüntülemek için aşağıdaki PowerShell betiğini kullanın:</span><span class="sxs-lookup"><span data-stu-id="0b758-152">Use the following PowerShell script to display recommendations with movie names:</span></span>

<span data-ttu-id="0b758-153">[!code-powershell[Ana](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=106-180)]</span><span class="sxs-lookup"><span data-stu-id="0b758-153">[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=106-180)]</span></span>

<span data-ttu-id="0b758-154">Öneriler kullanımı kolay bir biçimde görüntülemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="0b758-154">Use the following command to display the recommendations in a user-friendly format:</span></span> 

```powershell
.\show-recommendation.ps1 -userId 4 -userDataFile .\user-ratings.txt -movieFile .\moviedb.txt -recommendationFile .\output.txt
```

<span data-ttu-id="0b758-155">Çıktı aşağıdaki metne benzer:</span><span class="sxs-lookup"><span data-stu-id="0b758-155">The output is similar to the following text:</span></span>

    Reading movies descriptions
    Reading rated movies
    Reading recommendations
    Rated movies
    ---------------------------
    Movie                                    Rating
    -----                                    ------
    Devil's Own, The (1997)                  1
    Alien: Resurrection (1997)               3
    187 (1997)                               2
    (lines ommitted)

    ---------------------------
    Recommended movies
    ---------------------------

    Movie                                    Score
    -----                                    -----
    Good Will Hunting (1997)                 4.6504064
    Swingers (1996)                          4.6862745
    Wings of the Dove, The (1997)            4.6666665
    People vs. Larry Flynt, The (1996)       4.834559
    Everyone Says I Love You (1996)          4.707071
    Secrets & Lies (1996)                    4.818182
    That Thing You Do! (1996)                4.75
    Grosse Pointe Blank (1997)               4.8235292
    Donnie Brasco (1997)                     4.6792455
    Lone Star (1996)                         4.7099237

## <span data-ttu-id="0b758-156"><a name="troubleshooting"></a>Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="0b758-156"><a name="troubleshooting"></a>Troubleshooting</span></span>

### <a name="cannot-overwrite-files"></a><span data-ttu-id="0b758-157">Dosyaları üzerine yazılamıyor</span><span class="sxs-lookup"><span data-stu-id="0b758-157">Cannot overwrite files</span></span>

<span data-ttu-id="0b758-158">Temizlemeden işleme sırasında oluşturulan geçici dosyaları mahout işleri yapın.</span><span class="sxs-lookup"><span data-stu-id="0b758-158">Mahout jobs do not clean up temporary files that were created during processing.</span></span> <span data-ttu-id="0b758-159">Ayrıca, işleri var olan çıkış dosyasının üzerine yazmaz.</span><span class="sxs-lookup"><span data-stu-id="0b758-159">In addition, the jobs do not overwrite existing output file.</span></span>

<span data-ttu-id="0b758-160">Mahout işleri çalıştırma esnasında oluşacak hataları önlemek için çalıştırmaları arasında geçici ve çıktı dosyaları silin.</span><span class="sxs-lookup"><span data-stu-id="0b758-160">To avoid errors when running Mahout jobs, delete temporary and output files between runs.</span></span> <span data-ttu-id="0b758-161">Bu belgedeki önceki komut dosyaları tarafından oluşturulan dosyaları kaldırmak için aşağıdaki PowerShell betiğini kullanın:</span><span class="sxs-lookup"><span data-stu-id="0b758-161">To remove the files created by the earlier scripts in this document, use the following PowerShell script:</span></span>

```powershell
# Login to your Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
$creds=Get-Credential -Message "Enter the login for the cluster"

#Get the cluster info so we can get the resource group, storage, etc.
$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName = $clusterInfo.DefaultStorageAccount.split('.')[0]
$container = $clusterInfo.DefaultStorageContainer
$storageAccountKey = (Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage context and upload the file
$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey $storageAccountKey

#Azure PowerShell can't delete blobs using wildcard,
#so have to get a list and delete one at a time
# Start with the output
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/out"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
# Next the temp files
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/temp"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
```

### <span data-ttu-id="0b758-162"><a name="nopowershell"></a>Azure PowerShell ile çalışmaz sınıfları</span><span class="sxs-lookup"><span data-stu-id="0b758-162"><a name="nopowershell"></a>Classes that do not work with Azure PowerShell</span></span>

<span data-ttu-id="0b758-163">Aşağıdaki sınıfları kullanan mahout işleri Windows Powershell'den kullanıldığında çeşitli hata iletileri döndürün:</span><span class="sxs-lookup"><span data-stu-id="0b758-163">Mahout jobs that use the following classes return various error messages when used from Windows PowerShell:</span></span>

* <span data-ttu-id="0b758-164">org.apache.mahout.utils.clustering.ClusterDumper</span><span class="sxs-lookup"><span data-stu-id="0b758-164">org.apache.mahout.utils.clustering.ClusterDumper</span></span>
* <span data-ttu-id="0b758-165">org.apache.mahout.utils.SequenceFileDumper</span><span class="sxs-lookup"><span data-stu-id="0b758-165">org.apache.mahout.utils.SequenceFileDumper</span></span>
* <span data-ttu-id="0b758-166">org.apache.mahout.utils.vectors.lucene.Driver</span><span class="sxs-lookup"><span data-stu-id="0b758-166">org.apache.mahout.utils.vectors.lucene.Driver</span></span>
* <span data-ttu-id="0b758-167">org.apache.mahout.utils.vectors.arff.Driver</span><span class="sxs-lookup"><span data-stu-id="0b758-167">org.apache.mahout.utils.vectors.arff.Driver</span></span>
* <span data-ttu-id="0b758-168">org.apache.mahout.text.WikipediaToSequenceFile</span><span class="sxs-lookup"><span data-stu-id="0b758-168">org.apache.mahout.text.WikipediaToSequenceFile</span></span>
* <span data-ttu-id="0b758-169">org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles</span><span class="sxs-lookup"><span data-stu-id="0b758-169">org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles</span></span>
* <span data-ttu-id="0b758-170">org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer</span><span class="sxs-lookup"><span data-stu-id="0b758-170">org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer</span></span>
* <span data-ttu-id="0b758-171">org.apache.mahout.classifier.sgd.TrainLogistic</span><span class="sxs-lookup"><span data-stu-id="0b758-171">org.apache.mahout.classifier.sgd.TrainLogistic</span></span>
* <span data-ttu-id="0b758-172">org.apache.mahout.classifier.sgd.RunLogistic</span><span class="sxs-lookup"><span data-stu-id="0b758-172">org.apache.mahout.classifier.sgd.RunLogistic</span></span>
* <span data-ttu-id="0b758-173">org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="0b758-173">org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic</span></span>
* <span data-ttu-id="0b758-174">org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="0b758-174">org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic</span></span>
* <span data-ttu-id="0b758-175">org.apache.mahout.classifier.sgd.RunAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="0b758-175">org.apache.mahout.classifier.sgd.RunAdaptiveLogistic</span></span>
* <span data-ttu-id="0b758-176">org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer</span><span class="sxs-lookup"><span data-stu-id="0b758-176">org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer</span></span>
* <span data-ttu-id="0b758-177">org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator</span><span class="sxs-lookup"><span data-stu-id="0b758-177">org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator</span></span>
* <span data-ttu-id="0b758-178">org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator</span><span class="sxs-lookup"><span data-stu-id="0b758-178">org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator</span></span>
* <span data-ttu-id="0b758-179">org.apache.mahout.classifier.df.tools.Describe</span><span class="sxs-lookup"><span data-stu-id="0b758-179">org.apache.mahout.classifier.df.tools.Describe</span></span>

<span data-ttu-id="0b758-180">Bu sınıfları kullanan işlerini çalıştırmak için SSH kullanarak Hdınsight kümesine bağlanma ve komut satırından işleri çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="0b758-180">To run jobs that use these classes, connect to the HDInsight cluster using SSH and run the jobs from the command line.</span></span> <span data-ttu-id="0b758-181">Mahout işlerini çalıştırmak için SSH kullanarak bir örnek için bkz: [Mahout ve Hdınsight (SSH) kullanarak film önerileri oluşturma](hdinsight-hadoop-mahout-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="0b758-181">For an example of using SSH to run Mahout jobs, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b758-182">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="0b758-182">Next steps</span></span>

<span data-ttu-id="0b758-183">Mahout kullanmayı öğrendiniz, Hdınsight'ta veri ile çalışmanın diğer yolları Bul:</span><span class="sxs-lookup"><span data-stu-id="0b758-183">Now that you have learned how to use Mahout, discover other ways of working with data on HDInsight:</span></span>

* [<span data-ttu-id="0b758-184">Hdınsight ile hive</span><span class="sxs-lookup"><span data-stu-id="0b758-184">Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="0b758-185">Hdınsight ile pig</span><span class="sxs-lookup"><span data-stu-id="0b758-185">Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="0b758-186">Hdınsight ile MapReduce</span><span class="sxs-lookup"><span data-stu-id="0b758-186">MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[build]: http://mahout.apache.org/developers/buildingmahout.html
[aps]: /powershell/azureps-cmdlets-docs
[movielens]: http://grouplens.org/datasets/movielens/
[100k]: http://files.grouplens.org/datasets/movielens/ml-100k.zip
[getstarted]: hdinsight-hadoop-linux-tutorial-get-started.md
[upload]: hdinsight-upload-data.md
[ml]: http://en.wikipedia.org/wiki/Machine_learning
[forest]: http://en.wikipedia.org/wiki/Random_forest
[enableremote]: ./media/hdinsight-mahout/enableremote.png
[connect]: ./media/hdinsight-mahout/connect.png
[hadoopcli]: ./media/hdinsight-mahout/hadoopcli.png
[tools]: https://github.com/Blackmist/hdinsight-tools
