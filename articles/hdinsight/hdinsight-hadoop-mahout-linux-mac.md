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
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-linux-based-hadoop-in-hdinsight-ssh"></a>Hdınsight (SSH) Linux tabanlı Hadoop ile Apache Mahout kullanarak film önerileri oluşturma

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

Bilgi nasıl toouse hello [Apache Mahout](http://mahout.apache.org) machine learning kitaplığı Azure Hdınsight toogenerate film önerileri ile.

Mahout olan bir [makine öğrenme] [ ml] Apache Hadoop için kitaplığı. Mahout, Sınıflandırma, filtreleme ve kümeleme gibi veri işlemeye algoritmalarını içerir. Bu makalede, arkadaşlarınızın gördünüz filmler dayalı bir öneri altyapısı toogenerate film önerileri kullanın.

## <a name="prerequisites"></a>Ön koşullar

* Linux tabanlı Hdınsight kümesi. Bir oluşturma hakkında daha fazla bilgi için bkz: [Hdınsight'ta Linux tabanlı Hadoop ile çalışmaya başlamak][getstarted].

> [!IMPORTANT]
> Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir. Daha fazla bilgi için bkz. [Windows'da HDInsight'ın kullanımdan kaldırılması](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Bir SSH istemcisi. Daha fazla bilgi için bkz: Merhaba [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md) belge.

## <a name="mahout-versioning"></a>Mahout sürüm oluşturma

Hdınsight'ta Mahout hello sürümü hakkında daha fazla bilgi için bkz: [Hdınsight sürümleri ve Hadoop bileşenleri](hdinsight-component-versioning.md).

## <a name="recommendations"></a>Anlama önerileri

Mahout tarafından sağlanan hello işlevleri bir öneri altyapısı biridir. Bu altyapı hello biçiminde verilerini kabul eden `userID`, `itemId`, ve `prefValue` (Merhaba tercih hello öğesi için). Mahout sonra ortak occurance analiz toodetermine gerçekleştirin: *bir öğe için bir öncelik olan kullanıcıların diğer öğeler bir tercih bunlar için de*. Mahout sonra kullanılan toomake önerileri olabilir benzer öğe Tercihler kullanıcılarla belirler.

Merhaba aşağıdaki iş akışı film verilerini kullanan basitleştirilmiş bir örnek verilmiştir:

* **Ortak occurance**: Can, Alice ve Bob tüm beğendiğinizi *yıldız çatışmaları*, *Empire düşer geri hello*, ve *hello Jedi dönüşünü*. Mahout gibi bu filmler herhangi biri de gibi kullanıcılar diğer iki hello belirler.

* **Ortak occurance**: Bob ve Alice de beğendiğinizi *hayali İstilası hello*, *hello klonlar saldırı*, ve *Sith hello Revenge*. Mahout hello önceki üç filmler de ilişkilendirilmiş kullanıcılar bu üç filmler ister belirler.

* **Benzerlik öneri**: çünkü Joe beğendiğinizi ilk üç filmler hello Mahout bu beğendiğinizi benzer Tercihler başkalarıyla filmler görünür, ancak Joe olmayan izlenen (beğendiğinizi/derecelendirilmiş). Bu durumda, Mahout önerir *hayali İstilası hello*, *hello klonlar saldırı*, ve *Sith hello Revenge*.

### <a name="understanding-hello-data"></a>Merhaba veri anlama

Uygun şekilde, [GroupLens araştırma] [ movielens] Mahout ile uyumlu bir biçimde film derecelendirme veri sağlar. Bu veriler, kümenin varsayılan depolama kullanılabilir `/HdiSamples/HdiSamples/MahoutMovieData`.

İki dosya vardır `moviedb.txt` ve `user-ratings.txt`. moviedb.txt hello analiz hello sonuçlarını görüntülenirken kullanılan tooprovide kullanıcı dostu metin bilgileri durumdayken hello kullanıcı ratings.txt dosyası Çözümleme sırasında kullanılır.

Merhaba kullanıcı-ratings.txt bulunan verileri olan bir yapısını `userID`, `movieID`, `userRating`, ve `timestamp`, söyleyen bize nasıl yüksek oranda her kullanıcı bir filmi derecelendirilir. Merhaba veri örneği şöyledir:

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

## <a name="run-hello-analysis"></a>Merhaba analizini çalıştırma

Bir SSH bağlantısı toohello kümesinden komutu toorun hello öneri işi aşağıdaki hello kullan:

```bash
mahout recommenditembased -s SIMILARITY_COOCCURRENCE -i /HdiSamples/HdiSamples/MahoutMovieData/user-ratings.txt -o /example/data/mahoutout --tempDir /temp/mahouttemp
```

> [!NOTE]
> Merhaba iş birkaç dakika toocomplete alabilir ve birden çok MapReduce işleri çalışabilir.

## <a name="view-hello-output"></a>Görünüm hello çıktı

1. Merhaba işi tamamlandıktan sonra komutu tooview oluşturulan hello çıktısı aşağıdaki hello kullanın:

    ```bash
    hdfs dfs -text /example/data/mahoutout/part-r-00000
    ```

    Merhaba çıktı şu şekilde görünür:

        1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
        2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
        3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
        4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

    Merhaba ilk sütundur hello `userID`. Merhaba bulunan değer ' [' ve ']' olan `movieId`:`recommendationScore`.

2. Daha fazla bilgi hello moviedb.txt, tooprovide birlikte hello çıktı hello öneriler kullanabilirsiniz. İlk olarak, yerel olarak hello aşağıdaki komutları kullanarak toocopy hello dosyaları gerekir:

    ```bash
    hdfs dfs -get /example/data/mahoutout/part-r-00000 recommendations.txt
    hdfs dfs -get /HdiSamples/HdiSamples/MahoutMovieData/* .
    ```

    Kopya hello çıkış veri tooa dosyasını adlı bu komut **recommendations.txt** hello film veri dosyalarının yanı sıra hello geçerli dizinde.

3. Komut toocreate film adları hello önerileri çıktı hello veri arayan bir Python komut dosyası izleyen hello kullan:

    ```bash
    nano show_recommendations.py
    ```

    Merhaba Düzenleyici açıldığında metin hello hello dosyasının içeriğini aşağıdaki hello kullan:

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

    Tuşuna **Ctrl-X**, **Y**ve son olarak **Enter** toosave hello veri.

4. Merhaba Python komut dosyasını çalıştırın. Merhaba aşağıdaki komut tüm hello dosyalarını indirdiğiniz hello dizinde bulunan varsayar:

    ```bash
    python show_recommendations.py 4 user-ratings.txt moviedb.txt recommendations.txt
    ```

    Bu komut kullanıcı kimliği 4 için oluşturulan hello önerileri bakar.

    * Merhaba **kullanıcı ratings.txt** derecelendirilmiş kullanılan tooretrieve filmler bir dosyadır.

    * Merhaba **moviedb.txt** hello filmler kullanılan tooretrieve hello adlarını bir dosyadır.

    * Merhaba **recommendations.txt** hello film önerileri bu kullanıcı için kullanılan tooretrieve değil.

     Merhaba, bu komuttan metin benzer toohello aşağıdaki çıktı:

        Tibet (1997) yedi yıllarda puan 5.0 = Indiana Can ve hello son Crusade (1989), puan 5.0 = Jaws (1975'ten), puan 5.0 = algılama ve Sensibility (1995) puanı 5.0 = bağımsızlığı gün (ID4) (1996) puanı 5.0 My en iyi arkadaşınızın = (1997) Düğün puan 5.0 = Jerry Maguire (1996 ), puan 5.0 = Scream 2 (1997) puanı 5.0 = zaman tooKill, bir (1996), puan 5.0 =

## <a name="delete-temporary-data"></a>Geçici verileri Sil

Mahout işleri hello işi işlenirken oluşturulan geçici verileri kaldırmayın. Merhaba `--tempDir` parametresi kolay silme işlemi için belirli bir yolu içine hello örnek iş tooisolate hello geçici dosyalarında belirtilir. tooremove hello geçici dosyalar, komutu aşağıdaki hello kullan:

```bash
hdfs dfs -rm -f -r /temp/mahouttemp
```

> [!WARNING]
> Toorun hello komutu yeniden istiyorsanız hello çıktı dizini silmeniz gerekir. Bu dizin toodelete aşağıdaki hello kullan:
>
> `hdfs dfs -rm -f -r /example/data/mahoutout`


## <a name="next-steps"></a>Sonraki adımlar

Artık öğrendiğinize göre nasıl toouse Mahout, hdınsight'taki verileri ile çalışmaya ilişkin diğer yolları Bul:

* [Hdınsight ile hive](hdinsight-use-hive.md)
* [Hdınsight ile pig](hdinsight-use-pig.md)
* [Hdınsight ile MapReduce](hdinsight-use-mapreduce.md)

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
