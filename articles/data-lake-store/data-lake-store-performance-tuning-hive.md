---
title: "Data Lake Store Hive performans ayarlama yönergeleri aaaAzure | Microsoft Docs"
description: "Azure Data Lake Store'a Hive performans kuralları ayarlama"
services: data-lake-store
documentationcenter: 
author: stewu
manager: amitkul
editor: stewu
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/19/2016
ms.author: stewu
ms.openlocfilehash: e44daeb6ad3b64e893c709df63b56444a330729f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-hive-on-hdinsight-and-azure-data-lake-store"></a><span data-ttu-id="eeb5e-103">Performans Kılavuzu Hive Hdınsight ve Azure Data Lake Store için ayarlama</span><span class="sxs-lookup"><span data-stu-id="eeb5e-103">Performance tuning guidance for Hive on HDInsight and Azure Data Lake Store</span></span>

<span data-ttu-id="eeb5e-104">Merhaba varsayılan ayarları tooprovide iyi bir performans birçok farklı kullanım örnekleri arasında ayarlanmış.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-104">hello default settings have been set tooprovide good performance across many different use cases.</span></span>  <span data-ttu-id="eeb5e-105">G/ç yoğun sorgularında Hive bizi tooget daha iyi performans ADLS sahip olabilir.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-105">For I/O intensive queries, Hive can be tuned tooget better performance with ADLS.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="eeb5e-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="eeb5e-106">Prerequisites</span></span>

* <span data-ttu-id="eeb5e-107">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-107">**An Azure subscription**.</span></span> <span data-ttu-id="eeb5e-108">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="eeb5e-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="eeb5e-109">**Bir Azure Data Lake Store hesabı**.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-109">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="eeb5e-110">Yönergeler için toocreate bir, bkz: [Azure Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="eeb5e-110">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="eeb5e-111">**Azure Hdınsight kümesi** erişim tooa Data Lake Store hesabı ile.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-111">**Azure HDInsight cluster** with access tooa Data Lake Store account.</span></span> <span data-ttu-id="eeb5e-112">Bkz: [Data Lake Store ile bir Hdınsight kümesi oluşturmayı](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="eeb5e-112">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="eeb5e-113">Merhaba küme için Uzak Masaüstü etkinleştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-113">Make sure you enable Remote Desktop for hello cluster.</span></span>
* <span data-ttu-id="eeb5e-114">**Hdınsight'ta Hive çalıştıran**.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-114">**Running Hive on HDInsight**.</span></span>  <span data-ttu-id="eeb5e-115">Hdınsight üzerinde çalışan Hive işi hakkında toolearn bakın [Hive kullanma hdınsight'ta] (https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-hive)</span><span class="sxs-lookup"><span data-stu-id="eeb5e-115">toolearn about running Hive jobs on HDInsight, see [Use Hive on HDInsight] (https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-hive)</span></span>
* <span data-ttu-id="eeb5e-116">**Performans ayarlama yönergeleri ADLS**.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-116">**Performance tuning guidelines on ADLS**.</span></span>  <span data-ttu-id="eeb5e-117">Genel performans için bkz [Data Lake deposu performans rehberi ayarlama](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)</span><span class="sxs-lookup"><span data-stu-id="eeb5e-117">For general performance concepts, see [Data Lake Store Performance Tuning Guidance](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)</span></span>

## <a name="parameters"></a><span data-ttu-id="eeb5e-118">Parametreler</span><span class="sxs-lookup"><span data-stu-id="eeb5e-118">Parameters</span></span>

<span data-ttu-id="eeb5e-119">Merhaba en önemli ayarları tootune ADLS performansı için şunlardır:</span><span class="sxs-lookup"><span data-stu-id="eeb5e-119">Here are hello most important settings tootune for improved ADLS performance:</span></span>

* <span data-ttu-id="eeb5e-120">**Hive.tez.Container.size** – hello her görevleri tarafından kullanılan bellek miktarı</span><span class="sxs-lookup"><span data-stu-id="eeb5e-120">**hive.tez.container.size** – hello amount of memory used by each tasks</span></span>

* <span data-ttu-id="eeb5e-121">**Tez.Grouping.Min boyutu** – minimum boyutu her Eşleyici</span><span class="sxs-lookup"><span data-stu-id="eeb5e-121">**tez.grouping.min-size** – minimum size of each mapper</span></span>

* <span data-ttu-id="eeb5e-122">**Tez.Grouping.max boyutu** – maksimum boyutu her Eşleyici</span><span class="sxs-lookup"><span data-stu-id="eeb5e-122">**tez.grouping.max-size** – maximum size of each mapper</span></span>

* <span data-ttu-id="eeb5e-123">**Hive.Exec.reducer.bytes.Per.reducer** – her reducer boyutu</span><span class="sxs-lookup"><span data-stu-id="eeb5e-123">**hive.exec.reducer.bytes.per.reducer** – size of each reducer</span></span>

<span data-ttu-id="eeb5e-124">**Hive.tez.Container.size** -hello kapsayıcı boyutu belirler her görev için ne kadar kullanılabilir bellek yok.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-124">**hive.tez.container.size** - hello container size determines how much memory is available for each task.</span></span>  <span data-ttu-id="eeb5e-125">Merhaba ana giriş denetleme hello eşzamanlılık kovanında için budur.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-125">This is hello main input for controlling hello concurrency in Hive.</span></span>  

<span data-ttu-id="eeb5e-126">**Tez.Grouping.Min boyutu** – Bu parametre, tooset hello en küçük boyut her Eşleyici sağlar.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-126">**tez.grouping.min-size** – This parameter allows you tooset hello minimum size of each mapper.</span></span>  <span data-ttu-id="eeb5e-127">Tez seçer mappers Hello sayısı bu parametre, başlangıç değerinden daha küçükse, Tez Burada ayarlanan hello değeri kullanır.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-127">If hello number of mappers that Tez chooses is smaller than hello value of this parameter, then Tez will use hello value set here.</span></span>  

<span data-ttu-id="eeb5e-128">**Tez.Grouping.max boyutu** – hello parametresi, tooset hello en büyük boyutu her Eşleyici verir.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-128">**tez.grouping.max-size** – hello parameter allows you tooset hello maximum size of each mapper.</span></span>  <span data-ttu-id="eeb5e-129">Tez seçer mappers Hello sayısı bu parametre, başlangıç değerinden büyük olursa, Tez Burada ayarlanan hello değeri kullanır.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-129">If hello number of mappers that Tez chooses is larger than hello value of this parameter, then Tez will use hello value set here.</span></span>  

<span data-ttu-id="eeb5e-130">**Hive.Exec.reducer.bytes.Per.reducer** – Bu parametre her reducer hello boyutunu ayarlar.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-130">**hive.exec.reducer.bytes.per.reducer** – This parameter sets hello size of each reducer.</span></span>  <span data-ttu-id="eeb5e-131">Varsayılan olarak, her reducer 256 MB'tır.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-131">By default, each reducer is 256MB.</span></span>  

## <a name="guidance"></a><span data-ttu-id="eeb5e-132">Rehber</span><span class="sxs-lookup"><span data-stu-id="eeb5e-132">Guidance</span></span>

<span data-ttu-id="eeb5e-133">**Hive.Exec.reducer.bytes.Per.reducer ayarlamak** – hello veri sıkıştırılmamış olduğunda hello varsayılan değer iyi çalışır.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-133">**Set hive.exec.reducer.bytes.per.reducer** – hello default value works well when hello data is uncompressed.</span></span>  <span data-ttu-id="eeb5e-134">Sıkıştırılmış veri hello reducer hello boyutunu azaltmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-134">For data that is compressed, you should reduce hello size of hello reducer.</span></span>  

<span data-ttu-id="eeb5e-135">**Hive.tez.Container.size ayarlamak** – her bir düğümündeki bellek yarn.nodemanager.resource.memory mb belirtilir ve HDI kümesi üzerinde varsayılan olarak doğru bir şekilde ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-135">**Set hive.tez.container.size** – In each node, memory is specified by yarn.nodemanager.resource.memory-mb and should be correctly set on HDI cluster by default.</span></span>  <span data-ttu-id="eeb5e-136">YARN içinde hello uygun bellek ayarlama hakkında ek bilgi için bkz [sonrası](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-hive-out-of-memory-error-oom).</span><span class="sxs-lookup"><span data-stu-id="eeb5e-136">For additional information on setting hello appropriate memory in YARN, see this [post](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-hive-out-of-memory-error-oom).</span></span>

<span data-ttu-id="eeb5e-137">G/ç yoğun iş yükleri hello Tez kapsayıcı boyutu azaltarak daha fazla paralellik yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-137">I/O intensive workloads can benefit from more parallelism by decreasing hello Tez container size.</span></span> <span data-ttu-id="eeb5e-138">Bu hello kullanıcı eşzamanlılık artıran daha fazla kapsayıcı sağlar.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-138">This gives hello user more containers which increases concurrency.</span></span>  <span data-ttu-id="eeb5e-139">Ancak, bazı Hive sorguları önemli miktarda belleği (örneğin MapJoin) gerektirir.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-139">However, some Hive queries require a significant amount of memory (e.g. MapJoin).</span></span>  <span data-ttu-id="eeb5e-140">Merhaba görev yeterli belleğe sahip değil bir yetersiz bellek özel durumu çalışma zamanı sırasında alırsınız.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-140">If hello task does not have enough memory, you will get an out of memory exception during runtime.</span></span>  <span data-ttu-id="eeb5e-141">Yetersiz bellek özel durumları alırsanız, hello bellek artırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-141">If you receive out of memory exceptions, then you should increase hello memory.</span></span>   

<span data-ttu-id="eeb5e-142">çalışan görevler veya paralellik eşzamanlı sayısını Hello hello toplam YARN bellek tarafından sınırlanmış.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-142">hello concurrent number of tasks running or parallelism will be bounded by hello total YARN memory.</span></span>  <span data-ttu-id="eeb5e-143">YARN kapsayıcı Hello sayısı, kaç tane eş zamanlı görevleri çalıştırabilir benimsendiği belirler.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-143">hello number of YARN containers will dictate how many concurrent tasks can run.</span></span>  <span data-ttu-id="eeb5e-144">Düğüm başına toofind hello YARN bellek, tooAmbari gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-144">toofind hello YARN memory per node, you can go tooAmbari.</span></span>  <span data-ttu-id="eeb5e-145">TooYARN gidin ve hello yapılandırmalar sekmesini görüntüleyin.  Merhaba YARN bellek Bu pencerede görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-145">Navigate tooYARN and view hello Configs tab.  hello YARN memory is displayed in this window.</span></span>  

        Total YARN memory = nodes * YARN memory per node
        # of YARN containers = Total YARN memory / Tez container size
<span data-ttu-id="eeb5e-146">ADLS kullanarak hello anahtar tooimproving performansını tooincrease hello eşzamanlılık mümkün olduğunca ' dir.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-146">hello key tooimproving performance using ADLS is tooincrease hello concurrency as much as possible.</span></span>  <span data-ttu-id="eeb5e-147">Tez tooset gerek yoktur, oluşturulması gereken görevlerin hello sayısını otomatik olarak hesaplar.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-147">Tez automatically calculates hello number of tasks that should be created so you do not need tooset it.</span></span>   

## <a name="example-calculation"></a><span data-ttu-id="eeb5e-148">Örnek hesaplama</span><span class="sxs-lookup"><span data-stu-id="eeb5e-148">Example Calculation</span></span>

<span data-ttu-id="eeb5e-149">Bir 8 düğüm D14 küme sahip varsayalım.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-149">Let’s say you have an 8 node D14 cluster.</span></span>  

    Total YARN memory = nodes * YARN memory per node
    Total YARN memory = 8 nodes * 96GB = 768GB
    # of YARN containers = 768GB / 3072MB = 256

## <a name="limitations"></a><span data-ttu-id="eeb5e-150">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="eeb5e-150">Limitations</span></span>
<span data-ttu-id="eeb5e-151">**ADLS azaltma**</span><span class="sxs-lookup"><span data-stu-id="eeb5e-151">**ADLS throttling**</span></span> 

<span data-ttu-id="eeb5e-152">ADLS tarafından toosee görev hataları başlarsınız sağlanan hello isabet UIf bant genişliği sınırlar.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-152">UIf you hit hello limits of bandwidth provided by ADLS, you would start toosee task failures.</span></span> <span data-ttu-id="eeb5e-153">Bu görev günlükleri gözlemci azaltma hatalar nedeniyle tanımlanamadı.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-153">This could be identified by observing throttling errors in task logs.</span></span>  <span data-ttu-id="eeb5e-154">Tez kapsayıcı boyutu artırarak hello paralellik düşürebilir.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-154">You can decrease hello parallelism by increasing Tez container size.</span></span>  <span data-ttu-id="eeb5e-155">Daha fazla eşzamanlılık işiniz için ihtiyacınız varsa, lütfen bizimle iletişime geçin.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-155">If you need more concurrency for your job, please contact us.</span></span>   

<span data-ttu-id="eeb5e-156">Kısıtlanan durumunda toocheck tooenable hello hata ayıklama hello istemci tarafında günlüğü gerekir.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-156">toocheck if you are getting throttled, you need tooenable hello debug logging on hello client side.</span></span> <span data-ttu-id="eeb5e-157">İşte nasıl bunu yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="eeb5e-157">Here’s how you can do that:</span></span>

1. <span data-ttu-id="eeb5e-158">Merhaba log4j Hive yapılandırma özelliklerinde bir özellik aşağıdaki hello yerleştirin. Bu Ambari görünümünden yapılabilir: log4j.logger.com.microsoft.azure.datalake.store=DEBUG hello config tootake efekti için tüm hello düğümleri/hizmetini yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-158">Put hello following property in hello log4j properties in Hive config. This can be done from Ambari view: log4j.logger.com.microsoft.azure.datalake.store=DEBUG Restart all hello nodes/service for hello config tootake effect.</span></span>

2. <span data-ttu-id="eeb5e-159">Kısıtlanan hello HTTP 429 hata kodunu hello hive günlük dosyasında görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="eeb5e-159">If you are getting throttled, you’ll see hello HTTP 429 error code in hello hive log file.</span></span> <span data-ttu-id="eeb5e-160">Merhaba hive günlük dosyası, içinde /tmp/&lt;kullanıcı&gt;/hive.log</span><span class="sxs-lookup"><span data-stu-id="eeb5e-160">hello hive log file is in /tmp/&lt;user&gt;/hive.log</span></span>

## <a name="further-information-on-hive-tuning"></a><span data-ttu-id="eeb5e-161">Hive ayarlama hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="eeb5e-161">Further information on Hive tuning</span></span>

<span data-ttu-id="eeb5e-162">Hive sorgularınızı ince ayar yardımcı olacak birkaç Web günlükleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="eeb5e-162">Here are a few blogs that will help tune your Hive queries:</span></span>
* [<span data-ttu-id="eeb5e-163">Hdınsight'ta Hadoop için Hive sorguları en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="eeb5e-163">Optimize Hive queries for Hadoop in HDInsight</span></span>](https://azure.microsoft.com/en-us/documentation/articles/hdinsight-hadoop-optimize-hive-query/)
* [<span data-ttu-id="eeb5e-164">Hive sorgusu performans sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="eeb5e-164">Troubleshooting Hive query performance</span></span>](https://blogs.msdn.microsoft.com/bigdatasupport/2015/08/13/troubleshooting-hive-query-performance-in-hdinsight-hadoop-cluster/)
* [<span data-ttu-id="eeb5e-165">Konuşma göz atın üzerinde hdınsight'ta Hive en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="eeb5e-165">Ignite talk on optimize Hive on HDInsight</span></span>](https://channel9.msdn.com/events/Machine-Learning-and-Data-Sciences-Conference/Data-Science-Summit-2016/MSDSS25)
