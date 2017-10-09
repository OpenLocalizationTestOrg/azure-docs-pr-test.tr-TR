---
title: "Hdınsight üzerinde Apache Storm ile aaaTwitter oluşturan eğilim konuları | Microsoft Docs"
description: "Nasıl toouse Trident toocreate Twitter'da oluşturan eğilim konuları belirleyen bir Apache Storm topolojisini diyez etiketlerini hakkında temel bilgi edinin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 63b280ea-5c07-4dc8-a35f-dccf5a96ba93
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/14/2017
ms.author: larryfr
ms.openlocfilehash: 0281b495d10833c63868b36856c96369b139c553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a>Hdınsight üzerinde Apache Storm ile twitter oluşturan eğilim konuları belirleme

Nasıl toouse Trident toocreate bir Storm topolojisinin eğilim belirleyen öğrenin Twitter'da konuları (karma etiketleri).

Trident birleşimler, toplamalar, gruplandırma, İşlevler ve filtreleri gibi araçlar sağlayan bir üst düzey bir soyutlamadır. Ayrıca, Trident temelleri durum bilgisi olan, artımlı işleme yapmak için ekler. Bu belgede kullanılan hello özel spout ve işlev Trident topolojisiyle örnektir. Ayrıca, Trident tarafından sağlanan birkaç yerleşik işlevlerini kullanır.

## <a name="requirements"></a>Gereksinimler

* <a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java ve hello JDK 1,8</a>

* <a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a>

* <a href="http://git-scm.com/" target="_blank">Git</a>

* Bir Twitter Geliştirici hesabı

## <a name="download-hello-project"></a>Merhaba projenizi indirin

Kod tooclone hello projesini yerel olarak aşağıdaki hello kullanın.

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-hello-topology"></a>Merhaba topolojisini anlama

Bu topoloji veri akışını, gösterir Hello aşağıdaki Diyagram:

![topology](./media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> Bu diyagramda, hello topoloji Basitleştirilmiş görünümüdür. Merhaba bileşenleri birden çok örneğini hello kümedeki hello düğümler arasında dağıtılır.


Merhaba hello topoloji uygulayan Trident kod aşağıdaki gibidir:

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

Bu kod hello aşağıdaki eylemleri gerçekleştirir:

1. Merhaba spout bir akış oluşturur. Merhaba spout tweet'leri Twitter'dan alır ve bunları belirli anahtar sözcükler (love, müzik ve bu örnekte kahve) için filtreler.

2. HashtagExtractor, özel bir işlev her tweet arasında kullanılan tooextract karma etiketler ' dir. Merhaba karma verilmiş toohello akışını etiketleridir.

3. Merhaba akış karma etikete göre gruplandırılmış ve tooan toplayıcısı geçirildi. Bu Toplayıcıya her karma etiketi oluştu kaç kez sayısını oluşturur. Bu veriler bellekte kalıcıdır. Son olarak, yeni bir akış hello karma etiketi ve hello sayısını içeren yayınlanır.

4. Merhaba **FirstN** derlemedir hello sayısı alana göre uygulanan tooreturn hello ilk 10 değerler yalnızca,.

> [!NOTE]
> Merhaba Trident ile çalışma hakkında daha fazla bilgi için bkz: [Trident API genel bakış](http://storm.apache.org/releases/current/Trident-API-Overview.html) belge.

### <a name="hello-spout"></a>Merhaba spout

Merhaba spout **TwitterSpout**, kullanan [Twitter4j](http://twitter4j.org/en/) tooretrieve tweet'leri Twitter gelen. Bir filtre hello sözcükleri oluşturulur __memnuniyet__, **müzik**, ve **kahve**. Merhaba filtreyle eşleşen gelen tweet'leri (durum) bağlantılı bir engelleme sırasında depolanır. Son olarak, öğeleri hello sıra alınır ve toohello topoloji yayılan.

### <a name="hello-hashtagextractor"></a>Merhaba HashtagExtractor

tooextract karma etiketleri, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) kullanılan tooretrieve hello tweet içinde bulunan tüm karma etiketleri olan. Bu öğeler sonra verilmiş toohello akış.

## <a name="configure-twitter"></a>Twitter yapılandırın

Merhaba tüketici ve erişim belirteci bilgisi gerekli tooread Twitter'dan elde ve adımları tooregister yeni bir Twitter uygulaması aşağıdaki hello kullanın:

1. Çok Git[Twitter uygulamaları](https://apps.twitter.com) hello tıklatıp **yeni uygulama oluştur** düğmesi. Merhaba formunda doldururken hello bırakın **geri çağırma URL'si** alanı boş.

2. Merhaba uygulama oluşturulduğunda hello tıklatın **anahtarları ve erişim belirteçleri** sekmesi.

3. Kopya hello **tüketici anahtarı** ve **tüketici gizli** bilgi.

4. Merhaba sayfasının Hello altında seçin **my erişim belirteci oluşturma** hiçbir belirteçleri varsa. Merhaba belirteçleri zaman oluşturdunuz, kopyalama hello **erişim belirteci** ve **erişim belirteci gizli anahtarı** bilgi.

5. Merhaba, **TwitterSpoutTopology** önceden kopyalanan, açık hello proje **resources/twitter4j.properties** dosya hello önceki adımlarda topladığınız hello bilgilerini eklemek ve hello dosyasını kaydedin .

## <a name="build-hello-topology"></a>Merhaba topolojisini oluşturmak

Aşağıdaki kod toobuild hello projesi hello kullan:

        cd [directoryname]
        mvn compile

## <a name="test-hello-topology"></a>Test hello topolojisi

Komut tootest hello topoloji yerel olarak aşağıdaki hello kullan:

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

Merhaba topoloji başladıktan sonra hello karma içeren hata ayıklama bilgileri etiketleri ve hello topolojisi tarafından verilmiş sayılarını görmeniz gerekir. Merhaba çıkış metnini izleyen benzer toohello görünmelidir:

    DEBUG: [Quicktellervalentine, 7]
    DEBUG: [GRAMMYs, 7]
    DEBUG: [AskSam, 7]
    DEBUG: [poppunk, 1]
    DEBUG: [rock, 1]
    DEBUG: [punkrock, 1]
    DEBUG: [band, 1]
    DEBUG: [punk, 1]
    DEBUG: [indonesiapunkrock, 1]

## <a name="next-steps"></a>Sonraki adımlar

Merhaba topoloji yerel olarak test ettiğiniz, nasıl toodeploy hello topoloji Bul: [dağıtma ve Hdınsight üzerinde Apache Storm topolojilerini yönetmek](hdinsight-storm-deploy-monitor-topology.md).

Aşağıdaki Storm konularda hello ilgilenen olabilir:

* [Maven kullanarak Hdınsight üzerinde Storm için Java topolojisi geliştirme](hdinsight-storm-develop-java-topology.md)
* [Visual Studio kullanarak Hdınsight üzerinde Storm için C# topolojileri geliştirme](hdinsight-storm-develop-csharp-visual-studio-topology.md)

Hdınsight için daha fazla Storm örnekler için:

* [HDInsight üzerinde Storm için örnek topolojiler](hdinsight-storm-example-topology.md)

