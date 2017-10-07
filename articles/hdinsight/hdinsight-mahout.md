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
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-hadoop-in-hdinsight-powershell"></a>(PowerShell) hdınsight'ta Hadoop ile Apache Mahout kullanarak film önerileri oluşturma

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

Bilgi nasıl toouse hello [Apache Mahout](http://mahout.apache.org) machine learning kitaplığı Azure Hdınsight toogenerate film önerileri ile. Bu belgedeki Hello örnek Azure PowerShell toorun Mahout işleri kullanır.

## <a name="prerequisites"></a>Ön koşullar

* Linux tabanlı Hdınsight kümesi. Bir oluşturma hakkında daha fazla bilgi için bkz: [Hdınsight'ta Linux tabanlı Hadoop ile çalışmaya başlamak][getstarted].

> [!IMPORTANT]
> Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* [Azure PowerShell](/powershell/azure/overview)

## <a name="recommendations"></a>Azure PowerShell kullanarak önerileri oluşturma

> [!WARNING]
> Bu bölümdeki Hello iş Azure PowerShell kullanarak çalışır. Mahout ile sağlanan hello sınıfların çoğu Azure PowerShell ile şu anda çalışmıyor. Azure PowerShell ile çalışmaz sınıfları listesi için bkz: hello [sorun giderme](#troubleshooting) bölümü.
>
> SSH tooconnect tooHDInsight ve çalışma Mahout örnekler doğrudan hello kümede kullanılarak bir örnek için bkz: [Mahout ve Hdınsight (SSH) kullanarak film önerileri oluşturma](hdinsight-hadoop-mahout-linux-mac.md).

Mahout tarafından sağlanan hello işlevleri bir öneri altyapısı biridir. Bu altyapı hello biçiminde verilerini kabul eden `userID`, `itemId`, ve `prefValue` (Merhaba kullanıcıların tercih hello öğesi için). Mahout hello veri toodetermine kullanıcıları kullanılan toomake önerileri olabilir benzer öğe tercihlerinizle kullanır.

Merhaba aşağıdaki hello öneri işleminin nasıl çalıştığı, Basitleştirilmiş bir gözden geçirme örnektir:

* **Ortak oluşumu**: Can, Alice ve Bob tüm beğendiğinizi *yıldız çatışmaları*, *Empire düşer geri hello*, ve *hello Jedi dönüşünü*. Mahout gibi bu filmler herhangi biri de gibi kullanıcılar diğer iki hello belirler.

* **Ortak oluşumu**: Bob ve Alice de beğendiğinizi *hayali İstilası hello*, *hello klonlar saldırı*, ve *Sith hello Revenge*. Mahout hello önceki üç filmler de ilişkilendirilmiş kullanıcılar bu filmler ister belirler.

* **Benzerlik öneri**: çünkü Joe beğendiğinizi ilk üç filmler hello Mahout bu beğendiğinizi benzer Tercihler başkalarıyla filmler görünür, ancak Joe olmayan izlenen (beğendiğinizi/derecelendirilmiş). Bu durumda, Mahout önerir *hayali İstilası hello*, *hello klonlar saldırı*, ve *Sith hello Revenge*.

### <a name="understanding-hello-data"></a>Merhaba veri anlama

[GroupLens araştırma] [ movielens] Mahout ile uyumlu bir biçimde film derecelendirme veri sağlar. Bu veriler hello varsayılan depolama konumunda kümenize için kullanılabilir `/HdiSamples//HdiSamples/MahoutMovieData`.

İki dosya vardır `moviedb.txt` (Merhaba filmler hakkındaki bilgiler) ve `user-ratings.txt`. Merhaba `user-ratings.txt` dosyası Çözümleme sırasında kullanılır. Merhaba `moviedb.txt` dosya olduğunda kullanılan tooprovide kullanıcı dostu metin hello analiz hello sonuçları görüntüleme.

Merhaba kullanıcı-ratings.txt bulunan verileri olan bir yapısını `userID`, `movieID`, `userRating`, ve `timestamp`, söyleyen bize nasıl yüksek oranda her kullanıcı bir filmi derecelendirilir. Merhaba veri örneği şöyledir:

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

### <a name="run-hello-job"></a>Merhaba işini çalıştır

Windows PowerShell komut dosyası toorun hello film verilerle hello Mahout öneri altyapısı kullanan bir işi aşağıdaki hello kullan:

> [!NOTE]
> Bu dosya için kullanılan tooconnect tooyour Hdınsight kümesi ve çalıştırma işleri bilgileri ister. Merhaba işleri toocomplete birkaç dakikayı ve hello çıktı.txt dosyasını indirin.

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=5-98)]

> [!NOTE]
> Mahout işleri hello işi işlenirken oluşturulan geçici verileri kaldırmayın. Merhaba `--tempDir` parametresi belirli bir dizine hello örnek iş tooisolate hello geçici dosyalarında belirtilir.

Merhaba Mahout iş hello çıktı tooSTDOUT döndürmez. Bunun yerine, onu hello belirtilen çıkış dizinine depolar **bölümü r 00000**. Merhaba komut dosyası yüklemeleri bu dosya çok**çýktý.txt** hello geçerli dizinde istasyonunuzda.

Merhaba aşağıdaki bu dosyanın Merhaba içeriğine bir örnek metindir:

    1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
    2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
    3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
    4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

Merhaba ilk sütundur hello `userID`. Merhaba bulunan değer ' [' ve ']' olan `movieId`:`recommendationScore`.

Merhaba betiğini de hello indirir `moviedb.txt` ve `user-ratings.txt` gerekli tooformat hello çıktı toobe daha okunabilir dosyaları.

### <a name="view-hello-output"></a>Görünüm hello çıktı

Merhaba oluşturulan çıktı Tamam kullanılmak üzere bir uygulama olabilir, ancak kullanıcı dostu değil. Merhaba `moviedb.txt` hello sunucu kullanılan tooresolve hello olabilir `movieId` tooa film adı. Aşağıdaki PowerShell komut dosyası toodisplay önerileri film adlarıyla hello kullan:

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=106-180)]

Aşağıdaki komut toodisplay hello önerileri kullanımı kolay bir biçimde hello kullan: 

```powershell
.\show-recommendation.ps1 -userId 4 -userDataFile .\user-ratings.txt -movieFile .\moviedb.txt -recommendationFile .\output.txt
```

Merhaba, benzer toohello metin aşağıdaki çıktı:

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

## <a name="troubleshooting"></a>Sorun giderme

### <a name="cannot-overwrite-files"></a>Dosyaları üzerine yazılamıyor

Temizlemeden işleme sırasında oluşturulan geçici dosyaları mahout işleri yapın. Ayrıca, hello işleri var olan çıkış dosyasının üzerine yazmaz.

Mahout işleri çalıştırırken tooavoid hata çalıştırmaları arasında geçici ve çıktı dosyaları silin. oluşturulan tooremove hello dosyaları hello tarafından bu belgede, önceki betikler PowerShell Betiği aşağıdaki hello kullanın:

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

### <a name="nopowershell"></a>Azure PowerShell ile çalışmaz sınıfları

Sınıfları aşağıdaki hello kullanan mahout işleri Windows Powershell'den kullanıldığında çeşitli hata iletileri döndürün:

* org.apache.mahout.utils.clustering.ClusterDumper
* org.apache.mahout.utils.SequenceFileDumper
* org.apache.mahout.utils.vectors.lucene.Driver
* org.apache.mahout.utils.vectors.arff.Driver
* org.apache.mahout.text.WikipediaToSequenceFile
* org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles
* org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer
* org.apache.mahout.classifier.sgd.TrainLogistic
* org.apache.mahout.classifier.sgd.RunLogistic
* org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic
* org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic
* org.apache.mahout.classifier.sgd.RunAdaptiveLogistic
* org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer
* org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator
* org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator
* org.apache.mahout.classifier.df.tools.Describe

Bu sınıfları kullanan toorun işleri SSH kullanarak toohello Hdınsight kümesine bağlanın ve hello işleri hello komut satırından çalıştırın. SSH toorun Mahout işleri kullanma örneği için bkz: [Mahout ve Hdınsight (SSH) kullanarak film önerileri oluşturma](hdinsight-hadoop-mahout-linux-mac.md).

## <a name="next-steps"></a>Sonraki adımlar

Artık öğrendiğinize göre nasıl toouse Mahout, hdınsight'taki verileri ile çalışmaya ilişkin diğer yolları Bul:

* [Hdınsight ile hive](hdinsight-use-hive.md)
* [Hdınsight ile pig](hdinsight-use-pig.md)
* [Hdınsight ile MapReduce](hdinsight-use-mapreduce.md)

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
