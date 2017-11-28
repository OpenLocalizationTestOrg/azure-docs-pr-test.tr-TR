---
title: "PowerShell - Azure Hdınsight'ta Mahout kullanarak aaaGenerate önerileri | Microsoft Docs"
description: "Nasıl toouse hello kitaplığı toogenerate film önerileri Hdınsight (Hadoop) ile istemci üzerinde çalışan bir PowerShell Betiği öğrenmek Apache Mahout makine öğrenin."
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
ms.openlocfilehash: 675a2cd8ecaf7fc797d6cd094e4e58f9aca7ed92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-hadoop-in-hdinsight-powershell"></a><span data-ttu-id="01c6e-103">(PowerShell) hdınsight'ta Hadoop ile Apache Mahout kullanarak film önerileri oluşturma</span><span class="sxs-lookup"><span data-stu-id="01c6e-103">Generate movie recommendations by using Apache Mahout with Hadoop in HDInsight (PowerShell)</span></span>

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

<span data-ttu-id="01c6e-104">Bilgi nasıl toouse hello [Apache Mahout](http://mahout.apache.org) machine learning kitaplığı Azure Hdınsight toogenerate film önerileri ile.</span><span class="sxs-lookup"><span data-stu-id="01c6e-104">Learn how toouse hello [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight toogenerate movie recommendations.</span></span> <span data-ttu-id="01c6e-105">Bu belgedeki Hello örnek Azure PowerShell toorun Mahout işleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="01c6e-105">hello example in this document uses Azure PowerShell toorun Mahout jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01c6e-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="01c6e-106">Prerequisites</span></span>

* <span data-ttu-id="01c6e-107">Linux tabanlı Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="01c6e-107">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="01c6e-108">Bir oluşturma hakkında daha fazla bilgi için bkz: [Hdınsight'ta Linux tabanlı Hadoop ile çalışmaya başlamak][getstarted].</span><span class="sxs-lookup"><span data-stu-id="01c6e-108">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="01c6e-109">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="01c6e-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="01c6e-110">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="01c6e-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="01c6e-111">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="01c6e-111">Azure PowerShell</span></span>](/powershell/azure/overview)

## <span data-ttu-id="01c6e-112"><a name="recommendations"></a>Azure PowerShell kullanarak önerileri oluşturma</span><span class="sxs-lookup"><span data-stu-id="01c6e-112"><a name="recommendations"></a>Generate recommendations by using Azure PowerShell</span></span>

> [!WARNING]
> <span data-ttu-id="01c6e-113">Bu bölümdeki Hello iş Azure PowerShell kullanarak çalışır.</span><span class="sxs-lookup"><span data-stu-id="01c6e-113">hello job in this section works by using Azure PowerShell.</span></span> <span data-ttu-id="01c6e-114">Mahout ile sağlanan hello sınıfların çoğu Azure PowerShell ile şu anda çalışmıyor.</span><span class="sxs-lookup"><span data-stu-id="01c6e-114">Many of hello classes provided with Mahout do not currently work with Azure PowerShell.</span></span> <span data-ttu-id="01c6e-115">Azure PowerShell ile çalışmaz sınıfları listesi için bkz: hello [sorun giderme](#troubleshooting) bölümü.</span><span class="sxs-lookup"><span data-stu-id="01c6e-115">For a list of classes that do not work with Azure PowerShell, see hello [Troubleshooting](#troubleshooting) section.</span></span>
>
> <span data-ttu-id="01c6e-116">SSH tooconnect tooHDInsight ve çalışma Mahout örnekler doğrudan hello kümede kullanılarak bir örnek için bkz: [Mahout ve Hdınsight (SSH) kullanarak film önerileri oluşturma](hdinsight-hadoop-mahout-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="01c6e-116">For an example of using SSH tooconnect tooHDInsight and run Mahout examples directly on hello cluster, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span></span>

<span data-ttu-id="01c6e-117">Mahout tarafından sağlanan hello işlevleri bir öneri altyapısı biridir.</span><span class="sxs-lookup"><span data-stu-id="01c6e-117">One of hello functions that is provided by Mahout is a recommendation engine.</span></span> <span data-ttu-id="01c6e-118">Bu altyapı hello biçiminde verilerini kabul eden `userID`, `itemId`, ve `prefValue` (Merhaba kullanıcıların tercih hello öğesi için).</span><span class="sxs-lookup"><span data-stu-id="01c6e-118">This engine accepts data in hello format of `userID`, `itemId`, and `prefValue` (hello users preference for hello item).</span></span> <span data-ttu-id="01c6e-119">Mahout hello veri toodetermine kullanıcıları kullanılan toomake önerileri olabilir benzer öğe tercihlerinizle kullanır.</span><span class="sxs-lookup"><span data-stu-id="01c6e-119">Mahout uses hello data toodetermine users with like-item preferences, which can be used toomake recommendations.</span></span>

<span data-ttu-id="01c6e-120">Merhaba aşağıdaki hello öneri işleminin nasıl çalıştığı, Basitleştirilmiş bir gözden geçirme örnektir:</span><span class="sxs-lookup"><span data-stu-id="01c6e-120">hello following example is a simplified walk-through of how hello recommendation process works:</span></span>

* <span data-ttu-id="01c6e-121">**Ortak oluşumu**: Can, Alice ve Bob tüm beğendiğinizi *yıldız çatışmaları*, *Empire düşer geri hello*, ve *hello Jedi dönüşünü*.</span><span class="sxs-lookup"><span data-stu-id="01c6e-121">**co-occurrence**: Joe, Alice, and Bob all liked *Star Wars*, *hello Empire Strikes Back*, and *Return of hello Jedi*.</span></span> <span data-ttu-id="01c6e-122">Mahout gibi bu filmler herhangi biri de gibi kullanıcılar diğer iki hello belirler.</span><span class="sxs-lookup"><span data-stu-id="01c6e-122">Mahout determines that users who like any one of these movies also like hello other two.</span></span>

* <span data-ttu-id="01c6e-123">**Ortak oluşumu**: Bob ve Alice de beğendiğinizi *hayali İstilası hello*, *hello klonlar saldırı*, ve *Sith hello Revenge*.</span><span class="sxs-lookup"><span data-stu-id="01c6e-123">**co-occurrence**: Bob and Alice also liked *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span> <span data-ttu-id="01c6e-124">Mahout hello önceki üç filmler de ilişkilendirilmiş kullanıcılar bu filmler ister belirler.</span><span class="sxs-lookup"><span data-stu-id="01c6e-124">Mahout determines that users who liked hello previous three movies also like these movies.</span></span>

* <span data-ttu-id="01c6e-125">**Benzerlik öneri**: çünkü Joe beğendiğinizi ilk üç filmler hello Mahout bu beğendiğinizi benzer Tercihler başkalarıyla filmler görünür, ancak Joe olmayan izlenen (beğendiğinizi/derecelendirilmiş).</span><span class="sxs-lookup"><span data-stu-id="01c6e-125">**Similarity recommendation**: Because Joe liked hello first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span></span> <span data-ttu-id="01c6e-126">Bu durumda, Mahout önerir *hayali İstilası hello*, *hello klonlar saldırı*, ve *Sith hello Revenge*.</span><span class="sxs-lookup"><span data-stu-id="01c6e-126">In this case, Mahout recommends *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span>

### <a name="understanding-hello-data"></a><span data-ttu-id="01c6e-127">Merhaba veri anlama</span><span class="sxs-lookup"><span data-stu-id="01c6e-127">Understanding hello data</span></span>

<span data-ttu-id="01c6e-128">[GroupLens araştırma] [ movielens] Mahout ile uyumlu bir biçimde film derecelendirme veri sağlar.</span><span class="sxs-lookup"><span data-stu-id="01c6e-128">[GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span></span> <span data-ttu-id="01c6e-129">Bu veriler hello varsayılan depolama konumunda kümenize için kullanılabilir `/HdiSamples//HdiSamples/MahoutMovieData`.</span><span class="sxs-lookup"><span data-stu-id="01c6e-129">This data is available on hello default storage for your cluster at `/HdiSamples//HdiSamples/MahoutMovieData`.</span></span>

<span data-ttu-id="01c6e-130">İki dosya vardır `moviedb.txt` (Merhaba filmler hakkındaki bilgiler) ve `user-ratings.txt`.</span><span class="sxs-lookup"><span data-stu-id="01c6e-130">There are two files, `moviedb.txt` (information about hello movies) and `user-ratings.txt`.</span></span> <span data-ttu-id="01c6e-131">Merhaba `user-ratings.txt` dosyası Çözümleme sırasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="01c6e-131">hello `user-ratings.txt` file is used during analysis.</span></span> <span data-ttu-id="01c6e-132">Merhaba `moviedb.txt` dosya olduğunda kullanılan tooprovide kullanıcı dostu metin hello analiz hello sonuçları görüntüleme.</span><span class="sxs-lookup"><span data-stu-id="01c6e-132">hello `moviedb.txt` file is used tooprovide user-friendly text when displaying hello results of hello analysis.</span></span>

<span data-ttu-id="01c6e-133">Merhaba kullanıcı-ratings.txt bulunan verileri olan bir yapısını `userID`, `movieID`, `userRating`, ve `timestamp`, söyleyen bize nasıl yüksek oranda her kullanıcı bir filmi derecelendirilir.</span><span class="sxs-lookup"><span data-stu-id="01c6e-133">hello data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which tells us how highly each user rated a movie.</span></span> <span data-ttu-id="01c6e-134">Merhaba veri örneği şöyledir:</span><span class="sxs-lookup"><span data-stu-id="01c6e-134">Here is an example of hello data:</span></span>

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

### <a name="run-hello-job"></a><span data-ttu-id="01c6e-135">Merhaba işini çalıştır</span><span class="sxs-lookup"><span data-stu-id="01c6e-135">Run hello job</span></span>

<span data-ttu-id="01c6e-136">Windows PowerShell komut dosyası toorun hello film verilerle hello Mahout öneri altyapısı kullanan bir işi aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="01c6e-136">Use hello following Windows PowerShell script toorun a job that uses hello Mahout recommendation engine with hello movie data:</span></span>

> [!NOTE]
> <span data-ttu-id="01c6e-137">Bu dosya için kullanılan tooconnect tooyour Hdınsight kümesi ve çalıştırma işleri bilgileri ister.</span><span class="sxs-lookup"><span data-stu-id="01c6e-137">This file prompts you for information that is used tooconnect tooyour HDInsight cluster and run jobs.</span></span> <span data-ttu-id="01c6e-138">Merhaba işleri toocomplete birkaç dakikayı ve hello çıktı.txt dosyasını indirin.</span><span class="sxs-lookup"><span data-stu-id="01c6e-138">It may take several minutes for hello jobs toocomplete and download hello output.txt file.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=5-98)]

> [!NOTE]
> <span data-ttu-id="01c6e-139">Mahout işleri hello işi işlenirken oluşturulan geçici verileri kaldırmayın.</span><span class="sxs-lookup"><span data-stu-id="01c6e-139">Mahout jobs do not remove temporary data that is created while processing hello job.</span></span> <span data-ttu-id="01c6e-140">Merhaba `--tempDir` parametresi belirli bir dizine hello örnek iş tooisolate hello geçici dosyalarında belirtilir.</span><span class="sxs-lookup"><span data-stu-id="01c6e-140">hello `--tempDir` parameter is specified in hello example job tooisolate hello temporary files into a specific directory.</span></span>

<span data-ttu-id="01c6e-141">Merhaba Mahout iş hello çıktı tooSTDOUT döndürmez.</span><span class="sxs-lookup"><span data-stu-id="01c6e-141">hello Mahout job does not return hello output tooSTDOUT.</span></span> <span data-ttu-id="01c6e-142">Bunun yerine, onu hello belirtilen çıkış dizinine depolar **bölümü r 00000**.</span><span class="sxs-lookup"><span data-stu-id="01c6e-142">Instead, it stores it in hello specified output directory as **part-r-00000**.</span></span> <span data-ttu-id="01c6e-143">Merhaba komut dosyası yüklemeleri bu dosya çok**çýktý.txt** hello geçerli dizinde istasyonunuzda.</span><span class="sxs-lookup"><span data-stu-id="01c6e-143">hello script downloads this file too**output.txt** in hello current directory on your workstation.</span></span>

<span data-ttu-id="01c6e-144">Merhaba aşağıdaki bu dosyanın Merhaba içeriğine bir örnek metindir:</span><span class="sxs-lookup"><span data-stu-id="01c6e-144">hello following text is an example of hello content of this file:</span></span>

    1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
    2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
    3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
    4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

<span data-ttu-id="01c6e-145">Merhaba ilk sütundur hello `userID`.</span><span class="sxs-lookup"><span data-stu-id="01c6e-145">hello first column is hello `userID`.</span></span> <span data-ttu-id="01c6e-146">Merhaba bulunan değer ' [' ve ']' olan `movieId`:`recommendationScore`.</span><span class="sxs-lookup"><span data-stu-id="01c6e-146">hello values contained in '[' and ']' are `movieId`:`recommendationScore`.</span></span>

<span data-ttu-id="01c6e-147">Merhaba betiğini de hello indirir `moviedb.txt` ve `user-ratings.txt` gerekli tooformat hello çıktı toobe daha okunabilir dosyaları.</span><span class="sxs-lookup"><span data-stu-id="01c6e-147">hello script also downloads hello `moviedb.txt` and `user-ratings.txt` files, which are needed tooformat hello output toobe more readable.</span></span>

### <a name="view-hello-output"></a><span data-ttu-id="01c6e-148">Görünüm hello çıktı</span><span class="sxs-lookup"><span data-stu-id="01c6e-148">View hello output</span></span>

<span data-ttu-id="01c6e-149">Merhaba oluşturulan çıktı Tamam kullanılmak üzere bir uygulama olabilir, ancak kullanıcı dostu değil.</span><span class="sxs-lookup"><span data-stu-id="01c6e-149">Although hello generated output might be OK for use in an application, it's not user-friendly.</span></span> <span data-ttu-id="01c6e-150">Merhaba `moviedb.txt` hello sunucu kullanılan tooresolve hello olabilir `movieId` tooa film adı.</span><span class="sxs-lookup"><span data-stu-id="01c6e-150">hello `moviedb.txt` from hello server can be used tooresolve hello `movieId` tooa movie name.</span></span> <span data-ttu-id="01c6e-151">Aşağıdaki PowerShell komut dosyası toodisplay önerileri film adlarıyla hello kullan:</span><span class="sxs-lookup"><span data-stu-id="01c6e-151">Use hello following PowerShell script toodisplay recommendations with movie names:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=106-180)]

<span data-ttu-id="01c6e-152">Aşağıdaki komut toodisplay hello önerileri kullanımı kolay bir biçimde hello kullan:</span><span class="sxs-lookup"><span data-stu-id="01c6e-152">Use hello following command toodisplay hello recommendations in a user-friendly format:</span></span> 

```powershell
.\show-recommendation.ps1 -userId 4 -userDataFile .\user-ratings.txt -movieFile .\moviedb.txt -recommendationFile .\output.txt
```

<span data-ttu-id="01c6e-153">Merhaba, benzer toohello metin aşağıdaki çıktı:</span><span class="sxs-lookup"><span data-stu-id="01c6e-153">hello output is similar toohello following text:</span></span>

    Reading movies descriptions
    Reading rated movies
    Reading recommendations
    Rated movies
    ---------------------------
    Movie                                    Rating
    -----                                    ------
    Devil's Own, hello (1997)                  1
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
    Wings of hello Dove, hello (1997)            4.6666665
    People vs. Larry Flynt, hello (1996)       4.834559
    Everyone Says I Love You (1996)          4.707071
    Secrets & Lies (1996)                    4.818182
    That Thing You Do! (1996)                4.75
    Grosse Pointe Blank (1997)               4.8235292
    Donnie Brasco (1997)                     4.6792455
    Lone Star (1996)                         4.7099237

## <span data-ttu-id="01c6e-154"><a name="troubleshooting"></a>Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="01c6e-154"><a name="troubleshooting"></a>Troubleshooting</span></span>

### <a name="cannot-overwrite-files"></a><span data-ttu-id="01c6e-155">Dosyaları üzerine yazılamıyor</span><span class="sxs-lookup"><span data-stu-id="01c6e-155">Cannot overwrite files</span></span>

<span data-ttu-id="01c6e-156">Temizlemeden işleme sırasında oluşturulan geçici dosyaları mahout işleri yapın.</span><span class="sxs-lookup"><span data-stu-id="01c6e-156">Mahout jobs do not clean up temporary files that were created during processing.</span></span> <span data-ttu-id="01c6e-157">Ayrıca, hello işleri var olan çıkış dosyasının üzerine yazmaz.</span><span class="sxs-lookup"><span data-stu-id="01c6e-157">In addition, hello jobs do not overwrite existing output file.</span></span>

<span data-ttu-id="01c6e-158">Mahout işleri çalıştırırken tooavoid hata çalıştırmaları arasında geçici ve çıktı dosyaları silin.</span><span class="sxs-lookup"><span data-stu-id="01c6e-158">tooavoid errors when running Mahout jobs, delete temporary and output files between runs.</span></span> <span data-ttu-id="01c6e-159">oluşturulan tooremove hello dosyaları hello tarafından bu belgede, önceki betikler PowerShell Betiği aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="01c6e-159">tooremove hello files created by hello earlier scripts in this document, use hello following PowerShell script:</span></span>

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

#Get hello cluster info so we can get hello resource group, storage, etc.
$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName = $clusterInfo.DefaultStorageAccount.split('.')[0]
$container = $clusterInfo.DefaultStorageContainer
$storageAccountKey = (Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage context and upload hello file
$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey $storageAccountKey

#Azure PowerShell can't delete blobs using wildcard,
#so have tooget a list and delete one at a time
# Start with hello output
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/out"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
# Next hello temp files
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/temp"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
```

### <span data-ttu-id="01c6e-160"><a name="nopowershell"></a>Azure PowerShell ile çalışmaz sınıfları</span><span class="sxs-lookup"><span data-stu-id="01c6e-160"><a name="nopowershell"></a>Classes that do not work with Azure PowerShell</span></span>

<span data-ttu-id="01c6e-161">Sınıfları aşağıdaki hello kullanan mahout işleri Windows Powershell'den kullanıldığında çeşitli hata iletileri döndürün:</span><span class="sxs-lookup"><span data-stu-id="01c6e-161">Mahout jobs that use hello following classes return various error messages when used from Windows PowerShell:</span></span>

* <span data-ttu-id="01c6e-162">org.apache.mahout.utils.clustering.ClusterDumper</span><span class="sxs-lookup"><span data-stu-id="01c6e-162">org.apache.mahout.utils.clustering.ClusterDumper</span></span>
* <span data-ttu-id="01c6e-163">org.apache.mahout.utils.SequenceFileDumper</span><span class="sxs-lookup"><span data-stu-id="01c6e-163">org.apache.mahout.utils.SequenceFileDumper</span></span>
* <span data-ttu-id="01c6e-164">org.apache.mahout.utils.vectors.lucene.Driver</span><span class="sxs-lookup"><span data-stu-id="01c6e-164">org.apache.mahout.utils.vectors.lucene.Driver</span></span>
* <span data-ttu-id="01c6e-165">org.apache.mahout.utils.vectors.arff.Driver</span><span class="sxs-lookup"><span data-stu-id="01c6e-165">org.apache.mahout.utils.vectors.arff.Driver</span></span>
* <span data-ttu-id="01c6e-166">org.apache.mahout.text.WikipediaToSequenceFile</span><span class="sxs-lookup"><span data-stu-id="01c6e-166">org.apache.mahout.text.WikipediaToSequenceFile</span></span>
* <span data-ttu-id="01c6e-167">org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles</span><span class="sxs-lookup"><span data-stu-id="01c6e-167">org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles</span></span>
* <span data-ttu-id="01c6e-168">org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer</span><span class="sxs-lookup"><span data-stu-id="01c6e-168">org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer</span></span>
* <span data-ttu-id="01c6e-169">org.apache.mahout.classifier.sgd.TrainLogistic</span><span class="sxs-lookup"><span data-stu-id="01c6e-169">org.apache.mahout.classifier.sgd.TrainLogistic</span></span>
* <span data-ttu-id="01c6e-170">org.apache.mahout.classifier.sgd.RunLogistic</span><span class="sxs-lookup"><span data-stu-id="01c6e-170">org.apache.mahout.classifier.sgd.RunLogistic</span></span>
* <span data-ttu-id="01c6e-171">org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="01c6e-171">org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic</span></span>
* <span data-ttu-id="01c6e-172">org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="01c6e-172">org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic</span></span>
* <span data-ttu-id="01c6e-173">org.apache.mahout.classifier.sgd.RunAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="01c6e-173">org.apache.mahout.classifier.sgd.RunAdaptiveLogistic</span></span>
* <span data-ttu-id="01c6e-174">org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer</span><span class="sxs-lookup"><span data-stu-id="01c6e-174">org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer</span></span>
* <span data-ttu-id="01c6e-175">org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator</span><span class="sxs-lookup"><span data-stu-id="01c6e-175">org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator</span></span>
* <span data-ttu-id="01c6e-176">org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator</span><span class="sxs-lookup"><span data-stu-id="01c6e-176">org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator</span></span>
* <span data-ttu-id="01c6e-177">org.apache.mahout.classifier.df.tools.Describe</span><span class="sxs-lookup"><span data-stu-id="01c6e-177">org.apache.mahout.classifier.df.tools.Describe</span></span>

<span data-ttu-id="01c6e-178">Bu sınıfları kullanan toorun işleri SSH kullanarak toohello Hdınsight kümesine bağlanın ve hello işleri hello komut satırından çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="01c6e-178">toorun jobs that use these classes, connect toohello HDInsight cluster using SSH and run hello jobs from hello command line.</span></span> <span data-ttu-id="01c6e-179">SSH toorun Mahout işleri kullanma örneği için bkz: [Mahout ve Hdınsight (SSH) kullanarak film önerileri oluşturma](hdinsight-hadoop-mahout-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="01c6e-179">For an example of using SSH toorun Mahout jobs, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="01c6e-180">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="01c6e-180">Next steps</span></span>

<span data-ttu-id="01c6e-181">Artık öğrendiğinize göre nasıl toouse Mahout, hdınsight'taki verileri ile çalışmaya ilişkin diğer yolları Bul:</span><span class="sxs-lookup"><span data-stu-id="01c6e-181">Now that you have learned how toouse Mahout, discover other ways of working with data on HDInsight:</span></span>

* [<span data-ttu-id="01c6e-182">Hdınsight ile hive</span><span class="sxs-lookup"><span data-stu-id="01c6e-182">Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="01c6e-183">Hdınsight ile pig</span><span class="sxs-lookup"><span data-stu-id="01c6e-183">Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="01c6e-184">Hdınsight ile MapReduce</span><span class="sxs-lookup"><span data-stu-id="01c6e-184">MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

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
