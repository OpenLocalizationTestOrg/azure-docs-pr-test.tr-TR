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
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a><span data-ttu-id="d2b0e-103">Hdınsight üzerinde Apache Storm ile twitter oluşturan eğilim konuları belirleme</span><span class="sxs-lookup"><span data-stu-id="d2b0e-103">Determine Twitter trending topics with Apache Storm on HDInsight</span></span>

<span data-ttu-id="d2b0e-104">Nasıl toouse Trident toocreate bir Storm topolojisinin eğilim belirleyen öğrenin Twitter'da konuları (karma etiketleri).</span><span class="sxs-lookup"><span data-stu-id="d2b0e-104">Learn how toouse Trident toocreate a Storm topology that determines trending topics (hash tags) on Twitter.</span></span>

<span data-ttu-id="d2b0e-105">Trident birleşimler, toplamalar, gruplandırma, İşlevler ve filtreleri gibi araçlar sağlayan bir üst düzey bir soyutlamadır.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-105">Trident is a high-level abstraction that provides tools such as joins, aggregations, grouping, functions, and filters.</span></span> <span data-ttu-id="d2b0e-106">Ayrıca, Trident temelleri durum bilgisi olan, artımlı işleme yapmak için ekler.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-106">Additionally, Trident adds primitives for doing stateful, incremental processing.</span></span> <span data-ttu-id="d2b0e-107">Bu belgede kullanılan hello özel spout ve işlev Trident topolojisiyle örnektir.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-107">hello example used in this document is a Trident topology with a custom spout and function.</span></span> <span data-ttu-id="d2b0e-108">Ayrıca, Trident tarafından sağlanan birkaç yerleşik işlevlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-108">It also uses several built-in functions provided by Trident.</span></span>

## <a name="requirements"></a><span data-ttu-id="d2b0e-109">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="d2b0e-109">Requirements</span></span>

* <span data-ttu-id="d2b0e-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java ve hello JDK 1,8</a></span><span class="sxs-lookup"><span data-stu-id="d2b0e-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java and hello JDK 1.8</a></span></span>

* <span data-ttu-id="d2b0e-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span><span class="sxs-lookup"><span data-stu-id="d2b0e-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span></span>

* <span data-ttu-id="d2b0e-112"><a href="http://git-scm.com/" target="_blank">Git</a></span><span class="sxs-lookup"><span data-stu-id="d2b0e-112"><a href="http://git-scm.com/" target="_blank">Git</a></span></span>

* <span data-ttu-id="d2b0e-113">Bir Twitter Geliştirici hesabı</span><span class="sxs-lookup"><span data-stu-id="d2b0e-113">A Twitter developer account</span></span>

## <a name="download-hello-project"></a><span data-ttu-id="d2b0e-114">Merhaba projenizi indirin</span><span class="sxs-lookup"><span data-stu-id="d2b0e-114">Download hello project</span></span>

<span data-ttu-id="d2b0e-115">Kod tooclone hello projesini yerel olarak aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-115">Use hello following code tooclone hello project locally.</span></span>

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-hello-topology"></a><span data-ttu-id="d2b0e-116">Merhaba topolojisini anlama</span><span class="sxs-lookup"><span data-stu-id="d2b0e-116">Understanding hello topology</span></span>

<span data-ttu-id="d2b0e-117">Bu topoloji veri akışını, gösterir Hello aşağıdaki Diyagram:</span><span class="sxs-lookup"><span data-stu-id="d2b0e-117">hello following diagram shows of how data flows through this topology:</span></span>

![topology](./media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> <span data-ttu-id="d2b0e-119">Bu diyagramda, hello topoloji Basitleştirilmiş görünümüdür.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-119">This diagram is a simplified view of hello topology.</span></span> <span data-ttu-id="d2b0e-120">Merhaba bileşenleri birden çok örneğini hello kümedeki hello düğümler arasında dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-120">Multiple instances of hello components are distributed across hello nodes in hello cluster.</span></span>


<span data-ttu-id="d2b0e-121">Merhaba hello topoloji uygulayan Trident kod aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="d2b0e-121">hello Trident code that implements hello topology is as follows:</span></span>

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

<span data-ttu-id="d2b0e-122">Bu kod hello aşağıdaki eylemleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="d2b0e-122">This code performs hello following actions:</span></span>

1. <span data-ttu-id="d2b0e-123">Merhaba spout bir akış oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-123">Creates a stream from hello spout.</span></span> <span data-ttu-id="d2b0e-124">Merhaba spout tweet'leri Twitter'dan alır ve bunları belirli anahtar sözcükler (love, müzik ve bu örnekte kahve) için filtreler.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-124">hello spout retrieves tweets from Twitter, and filters them for specific keywords (love, music, and coffee in this example).</span></span>

2. <span data-ttu-id="d2b0e-125">HashtagExtractor, özel bir işlev her tweet arasında kullanılan tooextract karma etiketler ' dir.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-125">HashtagExtractor, a custom function, is used tooextract hash tags from each tweet.</span></span> <span data-ttu-id="d2b0e-126">Merhaba karma verilmiş toohello akışını etiketleridir.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-126">hello hash tags are emitted toohello stream.</span></span>

3. <span data-ttu-id="d2b0e-127">Merhaba akış karma etikete göre gruplandırılmış ve tooan toplayıcısı geçirildi.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-127">hello stream is grouped by hash tag, and passed tooan aggregator.</span></span> <span data-ttu-id="d2b0e-128">Bu Toplayıcıya her karma etiketi oluştu kaç kez sayısını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-128">This aggregator creates a count of how many times each hash tag has occurred.</span></span> <span data-ttu-id="d2b0e-129">Bu veriler bellekte kalıcıdır.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-129">This data is persisted in memory.</span></span> <span data-ttu-id="d2b0e-130">Son olarak, yeni bir akış hello karma etiketi ve hello sayısını içeren yayınlanır.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-130">Finally, a new stream is emitted that contains hello hash tag and hello count.</span></span>

4. <span data-ttu-id="d2b0e-131">Merhaba **FirstN** derlemedir hello sayısı alana göre uygulanan tooreturn hello ilk 10 değerler yalnızca,.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-131">hello **FirstN** assembly is applied tooreturn only hello top 10 values, based on hello count field.</span></span>

> [!NOTE]
> <span data-ttu-id="d2b0e-132">Merhaba Trident ile çalışma hakkında daha fazla bilgi için bkz: [Trident API genel bakış](http://storm.apache.org/releases/current/Trident-API-Overview.html) belge.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-132">For more information on working with Trident, see hello [Trident API overview](http://storm.apache.org/releases/current/Trident-API-Overview.html) document.</span></span>

### <a name="hello-spout"></a><span data-ttu-id="d2b0e-133">Merhaba spout</span><span class="sxs-lookup"><span data-stu-id="d2b0e-133">hello spout</span></span>

<span data-ttu-id="d2b0e-134">Merhaba spout **TwitterSpout**, kullanan [Twitter4j](http://twitter4j.org/en/) tooretrieve tweet'leri Twitter gelen.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-134">hello spout, **TwitterSpout**, uses [Twitter4j](http://twitter4j.org/en/) tooretrieve tweets from Twitter.</span></span> <span data-ttu-id="d2b0e-135">Bir filtre hello sözcükleri oluşturulur __memnuniyet__, **müzik**, ve **kahve**.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-135">A filter is created for hello words __love__, **music**, and **coffee**.</span></span> <span data-ttu-id="d2b0e-136">Merhaba filtreyle eşleşen gelen tweet'leri (durum) bağlantılı bir engelleme sırasında depolanır.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-136">Incoming tweets (status) that match hello filter are stored in a linked blocking queue.</span></span> <span data-ttu-id="d2b0e-137">Son olarak, öğeleri hello sıra alınır ve toohello topoloji yayılan.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-137">Finally, items are pulled off hello queue and emitted toohello topology.</span></span>

### <a name="hello-hashtagextractor"></a><span data-ttu-id="d2b0e-138">Merhaba HashtagExtractor</span><span class="sxs-lookup"><span data-stu-id="d2b0e-138">hello HashtagExtractor</span></span>

<span data-ttu-id="d2b0e-139">tooextract karma etiketleri, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) kullanılan tooretrieve hello tweet içinde bulunan tüm karma etiketleri olan.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-139">tooextract hash tags, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) is used tooretrieve all hash tags that are contained in hello tweet.</span></span> <span data-ttu-id="d2b0e-140">Bu öğeler sonra verilmiş toohello akış.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-140">These are then emitted toohello stream.</span></span>

## <a name="configure-twitter"></a><span data-ttu-id="d2b0e-141">Twitter yapılandırın</span><span class="sxs-lookup"><span data-stu-id="d2b0e-141">Configure Twitter</span></span>

<span data-ttu-id="d2b0e-142">Merhaba tüketici ve erişim belirteci bilgisi gerekli tooread Twitter'dan elde ve adımları tooregister yeni bir Twitter uygulaması aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="d2b0e-142">Use hello following steps tooregister a new Twitter application and obtain hello consumer and access token information needed tooread from Twitter:</span></span>

1. <span data-ttu-id="d2b0e-143">Çok Git[Twitter uygulamaları](https://apps.twitter.com) hello tıklatıp **yeni uygulama oluştur** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-143">Go too[Twitter Apps](https://apps.twitter.com) and click hello **Create new app** button.</span></span> <span data-ttu-id="d2b0e-144">Merhaba formunda doldururken hello bırakın **geri çağırma URL'si** alanı boş.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-144">When filling in hello form, leave hello **Callback URL** field empty.</span></span>

2. <span data-ttu-id="d2b0e-145">Merhaba uygulama oluşturulduğunda hello tıklatın **anahtarları ve erişim belirteçleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-145">When hello app is created, click hello **Keys and Access Tokens** tab.</span></span>

3. <span data-ttu-id="d2b0e-146">Kopya hello **tüketici anahtarı** ve **tüketici gizli** bilgi.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-146">Copy hello **Consumer Key** and **Consumer Secret** information.</span></span>

4. <span data-ttu-id="d2b0e-147">Merhaba sayfasının Hello altında seçin **my erişim belirteci oluşturma** hiçbir belirteçleri varsa.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-147">At hello bottom of hello page, select **Create my access token** if no tokens exist.</span></span> <span data-ttu-id="d2b0e-148">Merhaba belirteçleri zaman oluşturdunuz, kopyalama hello **erişim belirteci** ve **erişim belirteci gizli anahtarı** bilgi.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-148">When hello tokens have been created, copy hello **Access Token** and **Access Token Secret** information.</span></span>

5. <span data-ttu-id="d2b0e-149">Merhaba, **TwitterSpoutTopology** önceden kopyalanan, açık hello proje **resources/twitter4j.properties** dosya hello önceki adımlarda topladığınız hello bilgilerini eklemek ve hello dosyasını kaydedin .</span><span class="sxs-lookup"><span data-stu-id="d2b0e-149">In hello **TwitterSpoutTopology** project you previously cloned, open hello **resources/twitter4j.properties** file, add hello information you gathered in hello previous steps, and then save hello file.</span></span>

## <a name="build-hello-topology"></a><span data-ttu-id="d2b0e-150">Merhaba topolojisini oluşturmak</span><span class="sxs-lookup"><span data-stu-id="d2b0e-150">Build hello topology</span></span>

<span data-ttu-id="d2b0e-151">Aşağıdaki kod toobuild hello projesi hello kullan:</span><span class="sxs-lookup"><span data-stu-id="d2b0e-151">Use hello following code toobuild hello project:</span></span>

        cd [directoryname]
        mvn compile

## <a name="test-hello-topology"></a><span data-ttu-id="d2b0e-152">Test hello topolojisi</span><span class="sxs-lookup"><span data-stu-id="d2b0e-152">Test hello topology</span></span>

<span data-ttu-id="d2b0e-153">Komut tootest hello topoloji yerel olarak aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="d2b0e-153">Use hello following command tootest hello topology locally:</span></span>

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

<span data-ttu-id="d2b0e-154">Merhaba topoloji başladıktan sonra hello karma içeren hata ayıklama bilgileri etiketleri ve hello topolojisi tarafından verilmiş sayılarını görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="d2b0e-154">After hello topology starts, you should see debug information that contains hello hash tags and counts emitted by hello topology.</span></span> <span data-ttu-id="d2b0e-155">Merhaba çıkış metnini izleyen benzer toohello görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="d2b0e-155">hello output should appear similar toohello following text:</span></span>

    DEBUG: [Quicktellervalentine, 7]
    DEBUG: [GRAMMYs, 7]
    DEBUG: [AskSam, 7]
    DEBUG: [poppunk, 1]
    DEBUG: [rock, 1]
    DEBUG: [punkrock, 1]
    DEBUG: [band, 1]
    DEBUG: [punk, 1]
    DEBUG: [indonesiapunkrock, 1]

## <a name="next-steps"></a><span data-ttu-id="d2b0e-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="d2b0e-156">Next steps</span></span>

<span data-ttu-id="d2b0e-157">Merhaba topoloji yerel olarak test ettiğiniz, nasıl toodeploy hello topoloji Bul: [dağıtma ve Hdınsight üzerinde Apache Storm topolojilerini yönetmek](hdinsight-storm-deploy-monitor-topology.md).</span><span class="sxs-lookup"><span data-stu-id="d2b0e-157">Now that you have tested hello topology locally, discover how toodeploy hello topology: [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology.md).</span></span>

<span data-ttu-id="d2b0e-158">Aşağıdaki Storm konularda hello ilgilenen olabilir:</span><span class="sxs-lookup"><span data-stu-id="d2b0e-158">You may also be interested in hello following Storm topics:</span></span>

* [<span data-ttu-id="d2b0e-159">Maven kullanarak Hdınsight üzerinde Storm için Java topolojisi geliştirme</span><span class="sxs-lookup"><span data-stu-id="d2b0e-159">Develop Java topologies for Storm on HDInsight using Maven</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="d2b0e-160">Visual Studio kullanarak Hdınsight üzerinde Storm için C# topolojileri geliştirme</span><span class="sxs-lookup"><span data-stu-id="d2b0e-160">Develop C# topologies for Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="d2b0e-161">Hdınsight için daha fazla Storm örnekler için:</span><span class="sxs-lookup"><span data-stu-id="d2b0e-161">For more Storm examples for HDInsight:</span></span>

* [<span data-ttu-id="d2b0e-162">HDInsight üzerinde Storm için örnek topolojiler</span><span class="sxs-lookup"><span data-stu-id="d2b0e-162">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

