---
title: "Hdınsight üzerinde Apache Storm ile oluşturan eğilim konuları twitter | Microsoft Docs"
description: "Trident diyez etiketlerini üzerinde temel Twitter'da oluşturan eğilim konuları belirleyen bir Apache Storm topolojisini oluşturmak için nasıl kullanılacağını öğrenin."
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
ms.openlocfilehash: d588221586f151319436525c5098b0bb2694e5f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a>Hdınsight üzerinde Apache Storm ile twitter oluşturan eğilim konuları belirleme

Trident Twitter'da oluşturan eğilim konuları (karma etiketleri) belirleyen bir Storm topolojisinin oluşturmak için nasıl kullanılacağını öğrenin.

Trident birleşimler, toplamalar, gruplandırma, İşlevler ve filtreleri gibi araçlar sağlayan bir üst düzey bir soyutlamadır. Ayrıca, Trident temelleri durum bilgisi olan, artımlı işleme yapmak için ekler. Bu belgede kullanılan özel spout ve işlev Trident topolojisiyle örnektir. Ayrıca, Trident tarafından sağlanan birkaç yerleşik işlevlerini kullanır.

## <a name="requirements"></a>Gereksinimler

* <a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java ve JDK 1,8</a>

* <a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a>

* <a href="http://git-scm.com/" target="_blank">Git</a>

* Bir Twitter Geliştirici hesabı

## <a name="download-the-project"></a>Projenizi indirin

Projeyi yerel olarak kopyalamak için aşağıdaki kodu kullanın.

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-the-topology"></a>Topoloji anlama

Aşağıdaki diyagramda veri bu topoloji nasıl aktığını gösterir:

![topology](./media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> Bu diyagramda, topolojiye Basitleştirilmiş görünümüdür. Birden çok örneğini bileşenleri kümedeki düğümler arasında dağıtılır.


Topoloji uygulayan Trident kod aşağıdaki gibidir:

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

Bu kod, aşağıdaki eylemleri gerçekleştirir:

1. Spout bir akış oluşturur. Spout tweet'leri Twitter'dan alır ve bunları belirli anahtar sözcükler (love, müzik ve bu örnekte kahve) için filtreler.

2. HashtagExtractor, özel bir işlev karma etiketleri her tweet ayıklamak için kullanılır. Karma etiketleri akışa gösterilen.

3. Akış karma etikete göre gruplandırılır ve bir Toplayıcı geçirildi. Bu Toplayıcıya her karma etiketi oluştu kaç kez sayısını oluşturur. Bu veriler bellekte kalıcıdır. Son olarak, yeni bir akış karması etiketi ve sayı içeren yayınlanır.

4. **FirstN** derleme sayısı alana göre yalnızca ilk 10 dönüş değerleri için uygulanır.

> [!NOTE]
> Trident ile çalışma hakkında daha fazla bilgi için bkz: [Trident API genel bakış](http://storm.apache.org/releases/current/Trident-API-Overview.html) belge.

### <a name="the-spout"></a>Spout

Spout **TwitterSpout**, kullanan [Twitter4j](http://twitter4j.org/en/) Twitter'dan tweet'leri alınamadı. Bir filtre sözcüklerini oluşturulur __memnuniyet__, **müzik**, ve **kahve**. Filtreyle eşleşen gelen tweet'leri (durum) bağlantılı bir engelleme sırasında depolanır. Son olarak, öğeleri sıra çekilen ve topolojiye yayılan.

### <a name="the-hashtagextractor"></a>HashtagExtractor

Karma etiketleri ayıklamak için [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) tweet içinde bulunan tüm karma etiketleri almak için kullanılır. Bunlar gösterilen sonra akışa.

## <a name="configure-twitter"></a>Twitter yapılandırın

Yeni bir Twitter uygulamayı kaydedin ve Twitter'dan okumak için gereken tüketici ve erişim belirteci bilgi edinmek için aşağıdaki adımları kullanın:

1. Git [Twitter uygulamaları](https://apps.twitter.com) tıklatıp **yeni uygulama oluştur** düğmesi. Form doldururken bırakın **geri çağırma URL'si** alanı boş.

2. Uygulama oluşturulduğunda tıklayın **anahtarları ve erişim belirteçleri** sekmesi.

3. Kopya **tüketici anahtarı** ve **tüketici gizli** bilgi.

4. Sayfanın alt kısmındaki seçin **my erişim belirteci oluşturma** hiçbir belirteçleri varsa. Belirteçleri oluşturulduktan sonra kopyalama **erişim belirteci** ve **erişim belirteci gizli anahtarı** bilgi.

5. İçinde **TwitterSpoutTopology** kopyalanması, daha önce açık projeniz **resources/twitter4j.properties** dosya, önceki adımlarda topladığınız bilgileri ekleyin ve ardından dosyayı kaydedin.

## <a name="build-the-topology"></a>Topoloji oluşturmak

Projeyi oluşturmak için aşağıdaki kodu kullanın:

        cd [directoryname]
        mvn compile

## <a name="test-the-topology"></a>Topoloji test

Topoloji yerel olarak test etmek için aşağıdaki komutu kullanın:

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

Topoloji başlatıldıktan sonra karma içeren hata ayıklama bilgileri etiketleri ve topolojisi tarafından verilmiş sayılarını görmeniz gerekir. Çıktı aşağıdakine benzer görünmelidir:

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

Topoloji yerel olarak test ettiğiniz, topolojisi dağıtmak nasıl keşfetmek: [dağıtma ve Hdınsight üzerinde Apache Storm topolojilerini yönetmek](hdinsight-storm-deploy-monitor-topology.md).

Aşağıdaki Storm konulardaki ilgilenen olabilir:

* [Maven kullanarak Hdınsight üzerinde Storm için Java topolojisi geliştirme](hdinsight-storm-develop-java-topology.md)
* [Visual Studio kullanarak Hdınsight üzerinde Storm için C# topolojileri geliştirme](hdinsight-storm-develop-csharp-visual-studio-topology.md)

Hdınsight için daha fazla Storm örnekler için:

* [HDInsight üzerinde Storm için örnek topolojiler](hdinsight-storm-example-topology.md)

