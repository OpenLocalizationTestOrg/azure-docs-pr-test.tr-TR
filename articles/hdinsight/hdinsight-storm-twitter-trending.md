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
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a><span data-ttu-id="9ab06-103">Hdınsight üzerinde Apache Storm ile twitter oluşturan eğilim konuları belirleme</span><span class="sxs-lookup"><span data-stu-id="9ab06-103">Determine Twitter trending topics with Apache Storm on HDInsight</span></span>

<span data-ttu-id="9ab06-104">Trident Twitter'da oluşturan eğilim konuları (karma etiketleri) belirleyen bir Storm topolojisinin oluşturmak için nasıl kullanılacağını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="9ab06-104">Learn how to use Trident to create a Storm topology that determines trending topics (hash tags) on Twitter.</span></span>

<span data-ttu-id="9ab06-105">Trident birleşimler, toplamalar, gruplandırma, İşlevler ve filtreleri gibi araçlar sağlayan bir üst düzey bir soyutlamadır.</span><span class="sxs-lookup"><span data-stu-id="9ab06-105">Trident is a high-level abstraction that provides tools such as joins, aggregations, grouping, functions, and filters.</span></span> <span data-ttu-id="9ab06-106">Ayrıca, Trident temelleri durum bilgisi olan, artımlı işleme yapmak için ekler.</span><span class="sxs-lookup"><span data-stu-id="9ab06-106">Additionally, Trident adds primitives for doing stateful, incremental processing.</span></span> <span data-ttu-id="9ab06-107">Bu belgede kullanılan özel spout ve işlev Trident topolojisiyle örnektir.</span><span class="sxs-lookup"><span data-stu-id="9ab06-107">The example used in this document is a Trident topology with a custom spout and function.</span></span> <span data-ttu-id="9ab06-108">Ayrıca, Trident tarafından sağlanan birkaç yerleşik işlevlerini kullanır.</span><span class="sxs-lookup"><span data-stu-id="9ab06-108">It also uses several built-in functions provided by Trident.</span></span>

## <a name="requirements"></a><span data-ttu-id="9ab06-109">Gereksinimler</span><span class="sxs-lookup"><span data-stu-id="9ab06-109">Requirements</span></span>

* <span data-ttu-id="9ab06-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java ve JDK 1,8</a></span><span class="sxs-lookup"><span data-stu-id="9ab06-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java and the JDK 1.8</a></span></span>

* <span data-ttu-id="9ab06-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span><span class="sxs-lookup"><span data-stu-id="9ab06-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span></span>

* <span data-ttu-id="9ab06-112"><a href="http://git-scm.com/" target="_blank">Git</a></span><span class="sxs-lookup"><span data-stu-id="9ab06-112"><a href="http://git-scm.com/" target="_blank">Git</a></span></span>

* <span data-ttu-id="9ab06-113">Bir Twitter Geliştirici hesabı</span><span class="sxs-lookup"><span data-stu-id="9ab06-113">A Twitter developer account</span></span>

## <a name="download-the-project"></a><span data-ttu-id="9ab06-114">Projenizi indirin</span><span class="sxs-lookup"><span data-stu-id="9ab06-114">Download the project</span></span>

<span data-ttu-id="9ab06-115">Projeyi yerel olarak kopyalamak için aşağıdaki kodu kullanın.</span><span class="sxs-lookup"><span data-stu-id="9ab06-115">Use the following code to clone the project locally.</span></span>

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-the-topology"></a><span data-ttu-id="9ab06-116">Topoloji anlama</span><span class="sxs-lookup"><span data-stu-id="9ab06-116">Understanding the topology</span></span>

<span data-ttu-id="9ab06-117">Aşağıdaki diyagramda veri bu topoloji nasıl aktığını gösterir:</span><span class="sxs-lookup"><span data-stu-id="9ab06-117">The following diagram shows of how data flows through this topology:</span></span>

![topology](./media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> <span data-ttu-id="9ab06-119">Bu diyagramda, topolojiye Basitleştirilmiş görünümüdür.</span><span class="sxs-lookup"><span data-stu-id="9ab06-119">This diagram is a simplified view of the topology.</span></span> <span data-ttu-id="9ab06-120">Birden çok örneğini bileşenleri kümedeki düğümler arasında dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="9ab06-120">Multiple instances of the components are distributed across the nodes in the cluster.</span></span>


<span data-ttu-id="9ab06-121">Topoloji uygulayan Trident kod aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="9ab06-121">The Trident code that implements the topology is as follows:</span></span>

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

<span data-ttu-id="9ab06-122">Bu kod, aşağıdaki eylemleri gerçekleştirir:</span><span class="sxs-lookup"><span data-stu-id="9ab06-122">This code performs the following actions:</span></span>

1. <span data-ttu-id="9ab06-123">Spout bir akış oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9ab06-123">Creates a stream from the spout.</span></span> <span data-ttu-id="9ab06-124">Spout tweet'leri Twitter'dan alır ve bunları belirli anahtar sözcükler (love, müzik ve bu örnekte kahve) için filtreler.</span><span class="sxs-lookup"><span data-stu-id="9ab06-124">The spout retrieves tweets from Twitter, and filters them for specific keywords (love, music, and coffee in this example).</span></span>

2. <span data-ttu-id="9ab06-125">HashtagExtractor, özel bir işlev karma etiketleri her tweet ayıklamak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9ab06-125">HashtagExtractor, a custom function, is used to extract hash tags from each tweet.</span></span> <span data-ttu-id="9ab06-126">Karma etiketleri akışa gösterilen.</span><span class="sxs-lookup"><span data-stu-id="9ab06-126">The hash tags are emitted to the stream.</span></span>

3. <span data-ttu-id="9ab06-127">Akış karma etikete göre gruplandırılır ve bir Toplayıcı geçirildi.</span><span class="sxs-lookup"><span data-stu-id="9ab06-127">The stream is grouped by hash tag, and passed to an aggregator.</span></span> <span data-ttu-id="9ab06-128">Bu Toplayıcıya her karma etiketi oluştu kaç kez sayısını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9ab06-128">This aggregator creates a count of how many times each hash tag has occurred.</span></span> <span data-ttu-id="9ab06-129">Bu veriler bellekte kalıcıdır.</span><span class="sxs-lookup"><span data-stu-id="9ab06-129">This data is persisted in memory.</span></span> <span data-ttu-id="9ab06-130">Son olarak, yeni bir akış karması etiketi ve sayı içeren yayınlanır.</span><span class="sxs-lookup"><span data-stu-id="9ab06-130">Finally, a new stream is emitted that contains the hash tag and the count.</span></span>

4. <span data-ttu-id="9ab06-131">**FirstN** derleme sayısı alana göre yalnızca ilk 10 dönüş değerleri için uygulanır.</span><span class="sxs-lookup"><span data-stu-id="9ab06-131">The **FirstN** assembly is applied to return only the top 10 values, based on the count field.</span></span>

> [!NOTE]
> <span data-ttu-id="9ab06-132">Trident ile çalışma hakkında daha fazla bilgi için bkz: [Trident API genel bakış](http://storm.apache.org/releases/current/Trident-API-Overview.html) belge.</span><span class="sxs-lookup"><span data-stu-id="9ab06-132">For more information on working with Trident, see the [Trident API overview](http://storm.apache.org/releases/current/Trident-API-Overview.html) document.</span></span>

### <a name="the-spout"></a><span data-ttu-id="9ab06-133">Spout</span><span class="sxs-lookup"><span data-stu-id="9ab06-133">The spout</span></span>

<span data-ttu-id="9ab06-134">Spout **TwitterSpout**, kullanan [Twitter4j](http://twitter4j.org/en/) Twitter'dan tweet'leri alınamadı.</span><span class="sxs-lookup"><span data-stu-id="9ab06-134">The spout, **TwitterSpout**, uses [Twitter4j](http://twitter4j.org/en/) to retrieve tweets from Twitter.</span></span> <span data-ttu-id="9ab06-135">Bir filtre sözcüklerini oluşturulur __memnuniyet__, **müzik**, ve **kahve**.</span><span class="sxs-lookup"><span data-stu-id="9ab06-135">A filter is created for the words __love__, **music**, and **coffee**.</span></span> <span data-ttu-id="9ab06-136">Filtreyle eşleşen gelen tweet'leri (durum) bağlantılı bir engelleme sırasında depolanır.</span><span class="sxs-lookup"><span data-stu-id="9ab06-136">Incoming tweets (status) that match the filter are stored in a linked blocking queue.</span></span> <span data-ttu-id="9ab06-137">Son olarak, öğeleri sıra çekilen ve topolojiye yayılan.</span><span class="sxs-lookup"><span data-stu-id="9ab06-137">Finally, items are pulled off the queue and emitted to the topology.</span></span>

### <a name="the-hashtagextractor"></a><span data-ttu-id="9ab06-138">HashtagExtractor</span><span class="sxs-lookup"><span data-stu-id="9ab06-138">The HashtagExtractor</span></span>

<span data-ttu-id="9ab06-139">Karma etiketleri ayıklamak için [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) tweet içinde bulunan tüm karma etiketleri almak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9ab06-139">To extract hash tags, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) is used to retrieve all hash tags that are contained in the tweet.</span></span> <span data-ttu-id="9ab06-140">Bunlar gösterilen sonra akışa.</span><span class="sxs-lookup"><span data-stu-id="9ab06-140">These are then emitted to the stream.</span></span>

## <a name="configure-twitter"></a><span data-ttu-id="9ab06-141">Twitter yapılandırın</span><span class="sxs-lookup"><span data-stu-id="9ab06-141">Configure Twitter</span></span>

<span data-ttu-id="9ab06-142">Yeni bir Twitter uygulamayı kaydedin ve Twitter'dan okumak için gereken tüketici ve erişim belirteci bilgi edinmek için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="9ab06-142">Use the following steps to register a new Twitter application and obtain the consumer and access token information needed to read from Twitter:</span></span>

1. <span data-ttu-id="9ab06-143">Git [Twitter uygulamaları](https://apps.twitter.com) tıklatıp **yeni uygulama oluştur** düğmesi.</span><span class="sxs-lookup"><span data-stu-id="9ab06-143">Go to [Twitter Apps](https://apps.twitter.com) and click the **Create new app** button.</span></span> <span data-ttu-id="9ab06-144">Form doldururken bırakın **geri çağırma URL'si** alanı boş.</span><span class="sxs-lookup"><span data-stu-id="9ab06-144">When filling in the form, leave the **Callback URL** field empty.</span></span>

2. <span data-ttu-id="9ab06-145">Uygulama oluşturulduğunda tıklayın **anahtarları ve erişim belirteçleri** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="9ab06-145">When the app is created, click the **Keys and Access Tokens** tab.</span></span>

3. <span data-ttu-id="9ab06-146">Kopya **tüketici anahtarı** ve **tüketici gizli** bilgi.</span><span class="sxs-lookup"><span data-stu-id="9ab06-146">Copy the **Consumer Key** and **Consumer Secret** information.</span></span>

4. <span data-ttu-id="9ab06-147">Sayfanın alt kısmındaki seçin **my erişim belirteci oluşturma** hiçbir belirteçleri varsa.</span><span class="sxs-lookup"><span data-stu-id="9ab06-147">At the bottom of the page, select **Create my access token** if no tokens exist.</span></span> <span data-ttu-id="9ab06-148">Belirteçleri oluşturulduktan sonra kopyalama **erişim belirteci** ve **erişim belirteci gizli anahtarı** bilgi.</span><span class="sxs-lookup"><span data-stu-id="9ab06-148">When the tokens have been created, copy the **Access Token** and **Access Token Secret** information.</span></span>

5. <span data-ttu-id="9ab06-149">İçinde **TwitterSpoutTopology** kopyalanması, daha önce açık projeniz **resources/twitter4j.properties** dosya, önceki adımlarda topladığınız bilgileri ekleyin ve ardından dosyayı kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9ab06-149">In the **TwitterSpoutTopology** project you previously cloned, open the **resources/twitter4j.properties** file, add the information you gathered in the previous steps, and then save the file.</span></span>

## <a name="build-the-topology"></a><span data-ttu-id="9ab06-150">Topoloji oluşturmak</span><span class="sxs-lookup"><span data-stu-id="9ab06-150">Build the topology</span></span>

<span data-ttu-id="9ab06-151">Projeyi oluşturmak için aşağıdaki kodu kullanın:</span><span class="sxs-lookup"><span data-stu-id="9ab06-151">Use the following code to build the project:</span></span>

        cd [directoryname]
        mvn compile

## <a name="test-the-topology"></a><span data-ttu-id="9ab06-152">Topoloji test</span><span class="sxs-lookup"><span data-stu-id="9ab06-152">Test the topology</span></span>

<span data-ttu-id="9ab06-153">Topoloji yerel olarak test etmek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="9ab06-153">Use the following command to test the topology locally:</span></span>

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

<span data-ttu-id="9ab06-154">Topoloji başlatıldıktan sonra karma içeren hata ayıklama bilgileri etiketleri ve topolojisi tarafından verilmiş sayılarını görmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="9ab06-154">After the topology starts, you should see debug information that contains the hash tags and counts emitted by the topology.</span></span> <span data-ttu-id="9ab06-155">Çıktı aşağıdakine benzer görünmelidir:</span><span class="sxs-lookup"><span data-stu-id="9ab06-155">The output should appear similar to the following text:</span></span>

    DEBUG: [Quicktellervalentine, 7]
    DEBUG: [GRAMMYs, 7]
    DEBUG: [AskSam, 7]
    DEBUG: [poppunk, 1]
    DEBUG: [rock, 1]
    DEBUG: [punkrock, 1]
    DEBUG: [band, 1]
    DEBUG: [punk, 1]
    DEBUG: [indonesiapunkrock, 1]

## <a name="next-steps"></a><span data-ttu-id="9ab06-156">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9ab06-156">Next steps</span></span>

<span data-ttu-id="9ab06-157">Topoloji yerel olarak test ettiğiniz, topolojisi dağıtmak nasıl keşfetmek: [dağıtma ve Hdınsight üzerinde Apache Storm topolojilerini yönetmek](hdinsight-storm-deploy-monitor-topology.md).</span><span class="sxs-lookup"><span data-stu-id="9ab06-157">Now that you have tested the topology locally, discover how to deploy the topology: [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology.md).</span></span>

<span data-ttu-id="9ab06-158">Aşağıdaki Storm konulardaki ilgilenen olabilir:</span><span class="sxs-lookup"><span data-stu-id="9ab06-158">You may also be interested in the following Storm topics:</span></span>

* [<span data-ttu-id="9ab06-159">Maven kullanarak Hdınsight üzerinde Storm için Java topolojisi geliştirme</span><span class="sxs-lookup"><span data-stu-id="9ab06-159">Develop Java topologies for Storm on HDInsight using Maven</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="9ab06-160">Visual Studio kullanarak Hdınsight üzerinde Storm için C# topolojileri geliştirme</span><span class="sxs-lookup"><span data-stu-id="9ab06-160">Develop C# topologies for Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="9ab06-161">Hdınsight için daha fazla Storm örnekler için:</span><span class="sxs-lookup"><span data-stu-id="9ab06-161">For more Storm examples for HDInsight:</span></span>

* [<span data-ttu-id="9ab06-162">HDInsight üzerinde Storm için örnek topolojiler</span><span class="sxs-lookup"><span data-stu-id="9ab06-162">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

