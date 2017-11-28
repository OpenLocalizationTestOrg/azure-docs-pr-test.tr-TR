---
title: "Mahout ve Hdınsight (SSH) - Azure kullanarak aaaGenerate önerileri | Microsoft Docs"
description: "Nasıl toouse hello Apache Mahout machine learning kitaplığı toogenerate film önerileri Hdınsight (Hadoop) ile bilgi edinin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c78ec37c-9a8c-4bb6-9e38-0bdb9e89fbd7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: fedac9ceb4268f8421bce4623a5ad271041b8b3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-linux-based-hadoop-in-hdinsight-ssh"></a><span data-ttu-id="15741-103">Hdınsight (SSH) Linux tabanlı Hadoop ile Apache Mahout kullanarak film önerileri oluşturma</span><span class="sxs-lookup"><span data-stu-id="15741-103">Generate movie recommendations by using Apache Mahout with Linux-based Hadoop in HDInsight (SSH)</span></span>

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

<span data-ttu-id="15741-104">Bilgi nasıl toouse hello [Apache Mahout](http://mahout.apache.org) machine learning kitaplığı Azure Hdınsight toogenerate film önerileri ile.</span><span class="sxs-lookup"><span data-stu-id="15741-104">Learn how toouse hello [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight toogenerate movie recommendations.</span></span>

<span data-ttu-id="15741-105">Mahout olan bir [makine öğrenme] [ ml] Apache Hadoop için kitaplığı.</span><span class="sxs-lookup"><span data-stu-id="15741-105">Mahout is a [machine learning][ml] library for Apache Hadoop.</span></span> <span data-ttu-id="15741-106">Mahout, Sınıflandırma, filtreleme ve kümeleme gibi veri işlemeye algoritmalarını içerir.</span><span class="sxs-lookup"><span data-stu-id="15741-106">Mahout contains algorithms for processing data, such as filtering, classification, and clustering.</span></span> <span data-ttu-id="15741-107">Bu makalede, arkadaşlarınızın gördünüz filmler dayalı bir öneri altyapısı toogenerate film önerileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="15741-107">In this article, you use a recommendation engine toogenerate movie recommendations that are based on movies your friends have seen.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="15741-108">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="15741-108">Prerequisites</span></span>

* <span data-ttu-id="15741-109">Linux tabanlı Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="15741-109">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="15741-110">Bir oluşturma hakkında daha fazla bilgi için bkz: [Hdınsight'ta Linux tabanlı Hadoop ile çalışmaya başlamak][getstarted].</span><span class="sxs-lookup"><span data-stu-id="15741-110">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="15741-111">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="15741-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="15741-112">Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="15741-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="15741-113">Bir SSH istemcisi.</span><span class="sxs-lookup"><span data-stu-id="15741-113">An SSH client.</span></span> <span data-ttu-id="15741-114">Daha fazla bilgi için bkz: Merhaba [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md) belge.</span><span class="sxs-lookup"><span data-stu-id="15741-114">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="mahout-versioning"></a><span data-ttu-id="15741-115">Mahout sürüm oluşturma</span><span class="sxs-lookup"><span data-stu-id="15741-115">Mahout versioning</span></span>

<span data-ttu-id="15741-116">Hdınsight'ta Mahout hello sürümü hakkında daha fazla bilgi için bkz: [Hdınsight sürümleri ve Hadoop bileşenleri](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="15741-116">For more information about hello version of Mahout in HDInsight, see [HDInsight versions and Hadoop components](hdinsight-component-versioning.md).</span></span>

## <span data-ttu-id="15741-117"><a name="recommendations"></a>Anlama önerileri</span><span class="sxs-lookup"><span data-stu-id="15741-117"><a name="recommendations"></a>Understanding recommendations</span></span>

<span data-ttu-id="15741-118">Mahout tarafından sağlanan hello işlevleri bir öneri altyapısı biridir.</span><span class="sxs-lookup"><span data-stu-id="15741-118">One of hello functions that is provided by Mahout is a recommendation engine.</span></span> <span data-ttu-id="15741-119">Bu altyapı hello biçiminde verilerini kabul eden `userID`, `itemId`, ve `prefValue` (Merhaba tercih hello öğesi için).</span><span class="sxs-lookup"><span data-stu-id="15741-119">This engine accepts data in hello format of `userID`, `itemId`, and `prefValue` (hello preference for hello item).</span></span> <span data-ttu-id="15741-120">Mahout sonra ortak occurance analiz toodetermine gerçekleştirin: *bir öğe için bir öncelik olan kullanıcıların diğer öğeler bir tercih bunlar için de*.</span><span class="sxs-lookup"><span data-stu-id="15741-120">Mahout can then perform co-occurance analysis toodetermine: *users who have a preference for an item also have a preference for these other items*.</span></span> <span data-ttu-id="15741-121">Mahout sonra kullanılan toomake önerileri olabilir benzer öğe Tercihler kullanıcılarla belirler.</span><span class="sxs-lookup"><span data-stu-id="15741-121">Mahout then determines users with like-item preferences, which can be used toomake recommendations.</span></span>

<span data-ttu-id="15741-122">Merhaba aşağıdaki iş akışı film verilerini kullanan basitleştirilmiş bir örnek verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="15741-122">hello following workflow is a simplified example that uses movie data:</span></span>

* <span data-ttu-id="15741-123">**Ortak occurance**: Can, Alice ve Bob tüm beğendiğinizi *yıldız çatışmaları*, *Empire düşer geri hello*, ve *hello Jedi dönüşünü*.</span><span class="sxs-lookup"><span data-stu-id="15741-123">**Co-occurance**: Joe, Alice, and Bob all liked *Star Wars*, *hello Empire Strikes Back*, and *Return of hello Jedi*.</span></span> <span data-ttu-id="15741-124">Mahout gibi bu filmler herhangi biri de gibi kullanıcılar diğer iki hello belirler.</span><span class="sxs-lookup"><span data-stu-id="15741-124">Mahout determines that users who like any one of these movies also like hello other two.</span></span>

* <span data-ttu-id="15741-125">**Ortak occurance**: Bob ve Alice de beğendiğinizi *hayali İstilası hello*, *hello klonlar saldırı*, ve *Sith hello Revenge*.</span><span class="sxs-lookup"><span data-stu-id="15741-125">**Co-occurance**: Bob and Alice also liked *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span> <span data-ttu-id="15741-126">Mahout hello önceki üç filmler de ilişkilendirilmiş kullanıcılar bu üç filmler ister belirler.</span><span class="sxs-lookup"><span data-stu-id="15741-126">Mahout determines that users who liked hello previous three movies also like these three movies.</span></span>

* <span data-ttu-id="15741-127">**Benzerlik öneri**: çünkü Joe beğendiğinizi ilk üç filmler hello Mahout bu beğendiğinizi benzer Tercihler başkalarıyla filmler görünür, ancak Joe olmayan izlenen (beğendiğinizi/derecelendirilmiş).</span><span class="sxs-lookup"><span data-stu-id="15741-127">**Similarity recommendation**: Because Joe liked hello first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span></span> <span data-ttu-id="15741-128">Bu durumda, Mahout önerir *hayali İstilası hello*, *hello klonlar saldırı*, ve *Sith hello Revenge*.</span><span class="sxs-lookup"><span data-stu-id="15741-128">In this case, Mahout recommends *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span>

### <a name="understanding-hello-data"></a><span data-ttu-id="15741-129">Merhaba veri anlama</span><span class="sxs-lookup"><span data-stu-id="15741-129">Understanding hello data</span></span>

<span data-ttu-id="15741-130">Uygun şekilde, [GroupLens araştırma] [ movielens] Mahout ile uyumlu bir biçimde film derecelendirme veri sağlar.</span><span class="sxs-lookup"><span data-stu-id="15741-130">Conveniently, [GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span></span> <span data-ttu-id="15741-131">Bu veriler, kümenin varsayılan depolama kullanılabilir `/HdiSamples/HdiSamples/MahoutMovieData`.</span><span class="sxs-lookup"><span data-stu-id="15741-131">This data is available on your cluster's default storage at `/HdiSamples/HdiSamples/MahoutMovieData`.</span></span>

<span data-ttu-id="15741-132">İki dosya vardır `moviedb.txt` ve `user-ratings.txt`.</span><span class="sxs-lookup"><span data-stu-id="15741-132">There are two files, `moviedb.txt` and `user-ratings.txt`.</span></span> <span data-ttu-id="15741-133">moviedb.txt hello analiz hello sonuçlarını görüntülenirken kullanılan tooprovide kullanıcı dostu metin bilgileri durumdayken hello kullanıcı ratings.txt dosyası Çözümleme sırasında kullanılır.</span><span class="sxs-lookup"><span data-stu-id="15741-133">hello user-ratings.txt file is used during analysis, while moviedb.txt is used tooprovide user-friendly text information when displaying hello results of hello analysis.</span></span>

<span data-ttu-id="15741-134">Merhaba kullanıcı-ratings.txt bulunan verileri olan bir yapısını `userID`, `movieID`, `userRating`, ve `timestamp`, söyleyen bize nasıl yüksek oranda her kullanıcı bir filmi derecelendirilir.</span><span class="sxs-lookup"><span data-stu-id="15741-134">hello data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which tells us how highly each user rated a movie.</span></span> <span data-ttu-id="15741-135">Merhaba veri örneği şöyledir:</span><span class="sxs-lookup"><span data-stu-id="15741-135">Here is an example of hello data:</span></span>

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

## <a name="run-hello-analysis"></a><span data-ttu-id="15741-136">Merhaba analizini çalıştırma</span><span class="sxs-lookup"><span data-stu-id="15741-136">Run hello analysis</span></span>

<span data-ttu-id="15741-137">Bir SSH bağlantısı toohello kümesinden komutu toorun hello öneri işi aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="15741-137">From an SSH connection toohello cluster, use hello following command toorun hello recommendation job:</span></span>

```bash
mahout recommenditembased -s SIMILARITY_COOCCURRENCE -i /HdiSamples/HdiSamples/MahoutMovieData/user-ratings.txt -o /example/data/mahoutout --tempDir /temp/mahouttemp
```

> [!NOTE]
> <span data-ttu-id="15741-138">Merhaba iş birkaç dakika toocomplete alabilir ve birden çok MapReduce işleri çalışabilir.</span><span class="sxs-lookup"><span data-stu-id="15741-138">hello job may take several minutes toocomplete, and may run multiple MapReduce jobs.</span></span>

## <a name="view-hello-output"></a><span data-ttu-id="15741-139">Görünüm hello çıktı</span><span class="sxs-lookup"><span data-stu-id="15741-139">View hello output</span></span>

1. <span data-ttu-id="15741-140">Merhaba işi tamamlandıktan sonra komutu tooview oluşturulan hello çıktısı aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="15741-140">Once hello job completes, use hello following command tooview hello generated output:</span></span>

    ```bash
    hdfs dfs -text /example/data/mahoutout/part-r-00000
    ```

    <span data-ttu-id="15741-141">Merhaba çıktı şu şekilde görünür:</span><span class="sxs-lookup"><span data-stu-id="15741-141">hello output appears as follows:</span></span>

        1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
        2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
        3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
        4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

    <span data-ttu-id="15741-142">Merhaba ilk sütundur hello `userID`.</span><span class="sxs-lookup"><span data-stu-id="15741-142">hello first column is hello `userID`.</span></span> <span data-ttu-id="15741-143">Merhaba bulunan değer ' [' ve ']' olan `movieId`:`recommendationScore`.</span><span class="sxs-lookup"><span data-stu-id="15741-143">hello values contained in '[' and ']' are `movieId`:`recommendationScore`.</span></span>

2. <span data-ttu-id="15741-144">Daha fazla bilgi hello moviedb.txt, tooprovide birlikte hello çıktı hello öneriler kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="15741-144">You can use hello output, along with hello moviedb.txt, tooprovide more information on hello recommendations.</span></span> <span data-ttu-id="15741-145">İlk olarak, yerel olarak hello aşağıdaki komutları kullanarak toocopy hello dosyaları gerekir:</span><span class="sxs-lookup"><span data-stu-id="15741-145">First, we need toocopy hello files locally using hello following commands:</span></span>

    ```bash
    hdfs dfs -get /example/data/mahoutout/part-r-00000 recommendations.txt
    hdfs dfs -get /HdiSamples/HdiSamples/MahoutMovieData/* .
    ```

    <span data-ttu-id="15741-146">Kopya hello çıkış veri tooa dosyasını adlı bu komut **recommendations.txt** hello film veri dosyalarının yanı sıra hello geçerli dizinde.</span><span class="sxs-lookup"><span data-stu-id="15741-146">This command copies hello output data tooa file named **recommendations.txt** in hello current directory, along with hello movie data files.</span></span>

3. <span data-ttu-id="15741-147">Komut toocreate film adları hello önerileri çıktı hello veri arayan bir Python komut dosyası izleyen hello kullan:</span><span class="sxs-lookup"><span data-stu-id="15741-147">Use hello following command toocreate a Python script that looks up movie names for hello data in hello recommendations output:</span></span>

    ```bash
    nano show_recommendations.py
    ```

    <span data-ttu-id="15741-148">Merhaba Düzenleyici açıldığında metin hello hello dosyasının içeriğini aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="15741-148">When hello editor opens, use hello following text as hello contents of hello file:</span></span>

   ```python
   #!/usr/bin/env python

   import sys

   if len(sys.argv) != 5:
        print "Arguments: userId userDataFilename movieFilename recommendationFilename"
        sys.exit(1)

   userId, userDataFilename, movieFilename, recommendationFilename = sys.argv[1:]

   print "Reading Movies Descriptions"
   movieFile = open(movieFilename)
   movieById = {}
   for line in movieFile:
       tokens = line.split("|")
       movieById[tokens[0]] = tokens[1:]
   movieFile.close()

   print "Reading Rated Movies"
   userDataFile = open(userDataFilename)
   ratedMovieIds = []
   for line in userDataFile:
       tokens = line.split("\t")
       if tokens[0] == userId:
           ratedMovieIds.append((tokens[1],tokens[2]))
   userDataFile.close()

   print "Reading Recommendations"
   recommendationFile = open(recommendationFilename)
   recommendations = []
   for line in recommendationFile:
       tokens = line.split("\t")
       if tokens[0] == userId:
           movieIdAndScores = tokens[1].strip("[]\n").split(",")
           recommendations = [ movieIdAndScore.split(":") for movieIdAndScore in movieIdAndScores ]
           break
   recommendationFile.close()

   print "Rated Movies"
   print "------------------------"
   for movieId, rating in ratedMovieIds:
       print "%s, rating=%s" % (movieById[movieId][0], rating)
   print "------------------------"

   print "Recommended Movies"
   print "------------------------"
   for movieId, score in recommendations:
       print "%s, score=%s" % (movieById[movieId][0], score)
   print "------------------------"
   ```

    <span data-ttu-id="15741-149">Tuşuna **Ctrl-X**, **Y**ve son olarak **Enter** toosave hello veri.</span><span class="sxs-lookup"><span data-stu-id="15741-149">Press **Ctrl-X**, **Y**, and finally **Enter** toosave hello data.</span></span>

4. <span data-ttu-id="15741-150">Merhaba Python komut dosyasını çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="15741-150">Run hello Python script.</span></span> <span data-ttu-id="15741-151">Merhaba aşağıdaki komut tüm hello dosyalarını indirdiğiniz hello dizinde bulunan varsayar:</span><span class="sxs-lookup"><span data-stu-id="15741-151">hello following command assumes you are in hello directory where all hello files were downloaded:</span></span>

    ```bash
    python show_recommendations.py 4 user-ratings.txt moviedb.txt recommendations.txt
    ```

    <span data-ttu-id="15741-152">Bu komut kullanıcı kimliği 4 için oluşturulan hello önerileri bakar.</span><span class="sxs-lookup"><span data-stu-id="15741-152">This command looks at hello recommendations generated for user ID 4.</span></span>

    * <span data-ttu-id="15741-153">Merhaba **kullanıcı ratings.txt** derecelendirilmiş kullanılan tooretrieve filmler bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="15741-153">hello **user-ratings.txt** file is used tooretrieve movies that have been rated.</span></span>

    * <span data-ttu-id="15741-154">Merhaba **moviedb.txt** hello filmler kullanılan tooretrieve hello adlarını bir dosyadır.</span><span class="sxs-lookup"><span data-stu-id="15741-154">hello **moviedb.txt** file is used tooretrieve hello names of hello movies.</span></span>

    * <span data-ttu-id="15741-155">Merhaba **recommendations.txt** hello film önerileri bu kullanıcı için kullanılan tooretrieve değil.</span><span class="sxs-lookup"><span data-stu-id="15741-155">hello **recommendations.txt** is used tooretrieve hello movie recommendations for this user.</span></span>

     <span data-ttu-id="15741-156">Merhaba, bu komuttan metin benzer toohello aşağıdaki çıktı:</span><span class="sxs-lookup"><span data-stu-id="15741-156">hello output from this command is similar toohello following text:</span></span>

        <span data-ttu-id="15741-157">Tibet (1997) yedi yıllarda puan 5.0 = Indiana Can ve hello son Crusade (1989), puan 5.0 = Jaws (1975'ten), puan 5.0 = algılama ve Sensibility (1995) puanı 5.0 = bağımsızlığı gün (ID4) (1996) puanı 5.0 My en iyi arkadaşınızın = (1997) Düğün puan 5.0 = Jerry Maguire (1996 ), puan 5.0 = Scream 2 (1997) puanı 5.0 = zaman tooKill, bir (1996), puan 5.0 =</span><span class="sxs-lookup"><span data-stu-id="15741-157">Seven Years in Tibet (1997), score=5.0   Indiana Jones and hello Last Crusade (1989), score=5.0   Jaws (1975), score=5.0   Sense and Sensibility (1995), score=5.0   Independence Day (ID4) (1996), score=5.0   My Best Friend's Wedding (1997), score=5.0   Jerry Maguire (1996), score=5.0   Scream 2 (1997), score=5.0   Time tooKill, A (1996), score=5.0</span></span>

## <a name="delete-temporary-data"></a><span data-ttu-id="15741-158">Geçici verileri Sil</span><span class="sxs-lookup"><span data-stu-id="15741-158">Delete temporary data</span></span>

<span data-ttu-id="15741-159">Mahout işleri hello işi işlenirken oluşturulan geçici verileri kaldırmayın.</span><span class="sxs-lookup"><span data-stu-id="15741-159">Mahout jobs do not remove temporary data that is created while processing hello job.</span></span> <span data-ttu-id="15741-160">Merhaba `--tempDir` parametresi kolay silme işlemi için belirli bir yolu içine hello örnek iş tooisolate hello geçici dosyalarında belirtilir.</span><span class="sxs-lookup"><span data-stu-id="15741-160">hello `--tempDir` parameter is specified in hello example job tooisolate hello temporary files into a specific path for easy deletion.</span></span> <span data-ttu-id="15741-161">tooremove hello geçici dosyalar, komutu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="15741-161">tooremove hello temp files, use hello following command:</span></span>

```bash
hdfs dfs -rm -f -r /temp/mahouttemp
```

> [!WARNING]
> <span data-ttu-id="15741-162">Toorun hello komutu yeniden istiyorsanız hello çıktı dizini silmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="15741-162">If you want toorun hello command again, you must also delete hello output directory.</span></span> <span data-ttu-id="15741-163">Bu dizin toodelete aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="15741-163">Use hello following toodelete this directory:</span></span>
>
> `hdfs dfs -rm -f -r /example/data/mahoutout`


## <a name="next-steps"></a><span data-ttu-id="15741-164">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="15741-164">Next steps</span></span>

<span data-ttu-id="15741-165">Artık öğrendiğinize göre nasıl toouse Mahout, hdınsight'taki verileri ile çalışmaya ilişkin diğer yolları Bul:</span><span class="sxs-lookup"><span data-stu-id="15741-165">Now that you have learned how toouse Mahout, discover other ways of working with data on HDInsight:</span></span>

* [<span data-ttu-id="15741-166">Hdınsight ile hive</span><span class="sxs-lookup"><span data-stu-id="15741-166">Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="15741-167">Hdınsight ile pig</span><span class="sxs-lookup"><span data-stu-id="15741-167">Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="15741-168">Hdınsight ile MapReduce</span><span class="sxs-lookup"><span data-stu-id="15741-168">MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[build]: http://mahout.apache.org/developers/buildingmahout.html
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
