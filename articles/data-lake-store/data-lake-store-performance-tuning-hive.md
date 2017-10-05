---
title: "Azure Data Lake Store'a Hive performans yönergeleri ayarlama | Microsoft Docs"
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
ms.openlocfilehash: e10bf8f7cbae2b81d22823ff74fe652c6bcb2da3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="performance-tuning-guidance-for-hive-on-hdinsight-and-azure-data-lake-store"></a><span data-ttu-id="efd91-103">Performans Kılavuzu Hive Hdınsight ve Azure Data Lake Store için ayarlama</span><span class="sxs-lookup"><span data-stu-id="efd91-103">Performance tuning guidance for Hive on HDInsight and Azure Data Lake Store</span></span>

<span data-ttu-id="efd91-104">Varsayılan ayarları birçok farklı kullanım örnekleri arasında iyi bir performans sağlamak üzere ayarlanmış.</span><span class="sxs-lookup"><span data-stu-id="efd91-104">The default settings have been set to provide good performance across many different use cases.</span></span>  <span data-ttu-id="efd91-105">G/ç yoğun sorgularında Hive ADLS ile daha iyi performans almak için ayarlanabilecek.</span><span class="sxs-lookup"><span data-stu-id="efd91-105">For I/O intensive queries, Hive can be tuned to get better performance with ADLS.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="efd91-106">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="efd91-106">Prerequisites</span></span>

* <span data-ttu-id="efd91-107">**Bir Azure aboneliği**.</span><span class="sxs-lookup"><span data-stu-id="efd91-107">**An Azure subscription**.</span></span> <span data-ttu-id="efd91-108">Bkz. [Azure ücretsiz deneme sürümü alma](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="efd91-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="efd91-109">**Bir Azure Data Lake Store hesabı**.</span><span class="sxs-lookup"><span data-stu-id="efd91-109">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="efd91-110">Bir oluşturma hakkında yönergeler için bkz: [Azure Data Lake Store ile çalışmaya başlama](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="efd91-110">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="efd91-111">**Azure Hdınsight kümesi** bir Data Lake Store hesabına erişim.</span><span class="sxs-lookup"><span data-stu-id="efd91-111">**Azure HDInsight cluster** with access to a Data Lake Store account.</span></span> <span data-ttu-id="efd91-112">Bkz: [Data Lake Store ile bir Hdınsight kümesi oluşturmayı](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="efd91-112">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="efd91-113">Küme için Uzak Masaüstü etkinleştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="efd91-113">Make sure you enable Remote Desktop for the cluster.</span></span>
* <span data-ttu-id="efd91-114">**Hdınsight'ta Hive çalıştıran**.</span><span class="sxs-lookup"><span data-stu-id="efd91-114">**Running Hive on HDInsight**.</span></span>  <span data-ttu-id="efd91-115">[Hive kullanma hdınsight'ta] Hdınsight'ta Hive işleri çalıştırma hakkında bilgi için bkz (https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-hive)</span><span class="sxs-lookup"><span data-stu-id="efd91-115">To learn about running Hive jobs on HDInsight, see [Use Hive on HDInsight] (https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-hive)</span></span>
* <span data-ttu-id="efd91-116">**Performans ayarlama yönergeleri ADLS**.</span><span class="sxs-lookup"><span data-stu-id="efd91-116">**Performance tuning guidelines on ADLS**.</span></span>  <span data-ttu-id="efd91-117">Genel performans için bkz [Data Lake deposu performans rehberi ayarlama](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)</span><span class="sxs-lookup"><span data-stu-id="efd91-117">For general performance concepts, see [Data Lake Store Performance Tuning Guidance](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)</span></span>

## <a name="parameters"></a><span data-ttu-id="efd91-118">Parametreler</span><span class="sxs-lookup"><span data-stu-id="efd91-118">Parameters</span></span>

<span data-ttu-id="efd91-119">ADLS performansı için ince ayar için en önemli ayarları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="efd91-119">Here are the most important settings to tune for improved ADLS performance:</span></span>

* <span data-ttu-id="efd91-120">**Hive.tez.Container.size** – her görevleri tarafından kullanılan bellek miktarı</span><span class="sxs-lookup"><span data-stu-id="efd91-120">**hive.tez.container.size** – the amount of memory used by each tasks</span></span>

* <span data-ttu-id="efd91-121">**Tez.Grouping.Min boyutu** – minimum boyutu her Eşleyici</span><span class="sxs-lookup"><span data-stu-id="efd91-121">**tez.grouping.min-size** – minimum size of each mapper</span></span>

* <span data-ttu-id="efd91-122">**Tez.Grouping.max boyutu** – maksimum boyutu her Eşleyici</span><span class="sxs-lookup"><span data-stu-id="efd91-122">**tez.grouping.max-size** – maximum size of each mapper</span></span>

* <span data-ttu-id="efd91-123">**Hive.Exec.reducer.bytes.Per.reducer** – her reducer boyutu</span><span class="sxs-lookup"><span data-stu-id="efd91-123">**hive.exec.reducer.bytes.per.reducer** – size of each reducer</span></span>

<span data-ttu-id="efd91-124">**Hive.tez.Container.size** -kapsayıcı boyutu her görev için kullanılabilir bellek miktarını belirler.</span><span class="sxs-lookup"><span data-stu-id="efd91-124">**hive.tez.container.size** - The container size determines how much memory is available for each task.</span></span>  <span data-ttu-id="efd91-125">Eşzamanlılık kovanında denetlemek için ana giriş budur.</span><span class="sxs-lookup"><span data-stu-id="efd91-125">This is the main input for controlling the concurrency in Hive.</span></span>  

<span data-ttu-id="efd91-126">**Tez.Grouping.Min boyutu** – Bu parametre her Eşleyici minimum boyutu ayarlamanıza olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="efd91-126">**tez.grouping.min-size** – This parameter allows you to set the minimum size of each mapper.</span></span>  <span data-ttu-id="efd91-127">Tez seçer mappers sayısı bu parametre değerinden daha küçükse, Tez Burada ayarlanan değeri kullanır.</span><span class="sxs-lookup"><span data-stu-id="efd91-127">If the number of mappers that Tez chooses is smaller than the value of this parameter, then Tez will use the value set here.</span></span>  

<span data-ttu-id="efd91-128">**Tez.Grouping.max boyutu** – parametresi, her Eşleyici en büyük boyutunu ayarlamanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="efd91-128">**tez.grouping.max-size** – The parameter allows you to set the maximum size of each mapper.</span></span>  <span data-ttu-id="efd91-129">Tez seçer mappers sayısı bu parametre değerinden büyükse, Tez Burada ayarlanan değeri kullanır.</span><span class="sxs-lookup"><span data-stu-id="efd91-129">If the number of mappers that Tez chooses is larger than the value of this parameter, then Tez will use the value set here.</span></span>  

<span data-ttu-id="efd91-130">**Hive.Exec.reducer.bytes.Per.reducer** – Bu parametre her reducer boyutunu ayarlar.</span><span class="sxs-lookup"><span data-stu-id="efd91-130">**hive.exec.reducer.bytes.per.reducer** – This parameter sets the size of each reducer.</span></span>  <span data-ttu-id="efd91-131">Varsayılan olarak, her reducer 256 MB'tır.</span><span class="sxs-lookup"><span data-stu-id="efd91-131">By default, each reducer is 256MB.</span></span>  

## <a name="guidance"></a><span data-ttu-id="efd91-132">Rehber</span><span class="sxs-lookup"><span data-stu-id="efd91-132">Guidance</span></span>

<span data-ttu-id="efd91-133">**Hive.Exec.reducer.bytes.Per.reducer ayarlamak** – veri sıkıştırılmamış olduğunda varsayılan değer iyi çalışır.</span><span class="sxs-lookup"><span data-stu-id="efd91-133">**Set hive.exec.reducer.bytes.per.reducer** – The default value works well when the data is uncompressed.</span></span>  <span data-ttu-id="efd91-134">Sıkıştırılmış veri boyutu reducer azaltmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="efd91-134">For data that is compressed, you should reduce the size of the reducer.</span></span>  

<span data-ttu-id="efd91-135">**Hive.tez.Container.size ayarlamak** – her bir düğümündeki bellek yarn.nodemanager.resource.memory mb belirtilir ve HDI kümesi üzerinde varsayılan olarak doğru bir şekilde ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="efd91-135">**Set hive.tez.container.size** – In each node, memory is specified by yarn.nodemanager.resource.memory-mb and should be correctly set on HDI cluster by default.</span></span>  <span data-ttu-id="efd91-136">YARN içinde uygun bellek ayarlama hakkında ek bilgi için bkz [sonrası](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-hive-out-of-memory-error-oom).</span><span class="sxs-lookup"><span data-stu-id="efd91-136">For additional information on setting the appropriate memory in YARN, see this [post](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-hive-out-of-memory-error-oom).</span></span>

<span data-ttu-id="efd91-137">G/ç yoğun iş yükleri, Tez kapsayıcı boyutu azaltarak daha fazla paralellik yararlı olabilir.</span><span class="sxs-lookup"><span data-stu-id="efd91-137">I/O intensive workloads can benefit from more parallelism by decreasing the Tez container size.</span></span> <span data-ttu-id="efd91-138">Bu kullanıcı eşzamanlılık artıran daha fazla kapsayıcı sağlar.</span><span class="sxs-lookup"><span data-stu-id="efd91-138">This gives the user more containers which increases concurrency.</span></span>  <span data-ttu-id="efd91-139">Ancak, bazı Hive sorguları önemli miktarda belleği (örneğin MapJoin) gerektirir.</span><span class="sxs-lookup"><span data-stu-id="efd91-139">However, some Hive queries require a significant amount of memory (e.g. MapJoin).</span></span>  <span data-ttu-id="efd91-140">Görev yeterli belleğe sahip değil bir yetersiz bellek özel durumu çalışma zamanı sırasında alırsınız.</span><span class="sxs-lookup"><span data-stu-id="efd91-140">If the task does not have enough memory, you will get an out of memory exception during runtime.</span></span>  <span data-ttu-id="efd91-141">Yetersiz bellek özel durumları alırsanız, bellek artırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="efd91-141">If you receive out of memory exceptions, then you should increase the memory.</span></span>   

<span data-ttu-id="efd91-142">Çalışan görevler veya paralellik eşzamanlı sayısını, toplam YARN bellek tarafından sınırlanmış.</span><span class="sxs-lookup"><span data-stu-id="efd91-142">The concurrent number of tasks running or parallelism will be bounded by the total YARN memory.</span></span>  <span data-ttu-id="efd91-143">YARN kapsayıcı sayısı, kaç tane eş zamanlı görevleri çalıştırabilir benimsendiği belirler.</span><span class="sxs-lookup"><span data-stu-id="efd91-143">The number of YARN containers will dictate how many concurrent tasks can run.</span></span>  <span data-ttu-id="efd91-144">Düğüm başına YARN bellek bulmak için Ambari gidebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="efd91-144">To find the YARN memory per node, you can go to Ambari.</span></span>  <span data-ttu-id="efd91-145">YARN için gidin ve yapılandırmalar sekmesini görüntüleyin.</span><span class="sxs-lookup"><span data-stu-id="efd91-145">Navigate to YARN and view the Configs tab.</span></span>  <span data-ttu-id="efd91-146">YARN bellek Bu pencerede görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="efd91-146">The YARN memory is displayed in this window.</span></span>  

        Total YARN memory = nodes * YARN memory per node
        # of YARN containers = Total YARN memory / Tez container size
<span data-ttu-id="efd91-147">ADLS kullanarak performansı iyileştirme anahtarını mümkün olduğunca eşzamanlılık artırmaktır.</span><span class="sxs-lookup"><span data-stu-id="efd91-147">The key to improving performance using ADLS is to increase the concurrency as much as possible.</span></span>  <span data-ttu-id="efd91-148">Tez ayarlayın gerekmez böylece oluşturulması gereken görevlerin sayısını otomatik olarak hesaplar.</span><span class="sxs-lookup"><span data-stu-id="efd91-148">Tez automatically calculates the number of tasks that should be created so you do not need to set it.</span></span>   

## <a name="example-calculation"></a><span data-ttu-id="efd91-149">Örnek hesaplama</span><span class="sxs-lookup"><span data-stu-id="efd91-149">Example Calculation</span></span>

<span data-ttu-id="efd91-150">Bir 8 düğüm D14 küme sahip varsayalım.</span><span class="sxs-lookup"><span data-stu-id="efd91-150">Let’s say you have an 8 node D14 cluster.</span></span>  

    Total YARN memory = nodes * YARN memory per node
    Total YARN memory = 8 nodes * 96GB = 768GB
    # of YARN containers = 768GB / 3072MB = 256

## <a name="limitations"></a><span data-ttu-id="efd91-151">Sınırlamalar</span><span class="sxs-lookup"><span data-stu-id="efd91-151">Limitations</span></span>
<span data-ttu-id="efd91-152">**ADLS azaltma**</span><span class="sxs-lookup"><span data-stu-id="efd91-152">**ADLS throttling**</span></span> 

<span data-ttu-id="efd91-153">ADLS tarafından sağlanan bant genişliği sınırlarını isabet UIf, görev hataları görmeye başlarsınız.</span><span class="sxs-lookup"><span data-stu-id="efd91-153">UIf you hit the limits of bandwidth provided by ADLS, you would start to see task failures.</span></span> <span data-ttu-id="efd91-154">Bu görev günlükleri gözlemci azaltma hatalar nedeniyle tanımlanamadı.</span><span class="sxs-lookup"><span data-stu-id="efd91-154">This could be identified by observing throttling errors in task logs.</span></span>  <span data-ttu-id="efd91-155">Tez kapsayıcı boyutu artırarak paralellik düşürebilir.</span><span class="sxs-lookup"><span data-stu-id="efd91-155">You can decrease the parallelism by increasing Tez container size.</span></span>  <span data-ttu-id="efd91-156">Daha fazla eşzamanlılık işiniz için ihtiyacınız varsa, lütfen bizimle iletişime geçin.</span><span class="sxs-lookup"><span data-stu-id="efd91-156">If you need more concurrency for your job, please contact us.</span></span>   

<span data-ttu-id="efd91-157">Kısıtlanan durumunda denetlemek için hata ayıklama istemci tarafında günlüğünü etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="efd91-157">To check if you are getting throttled, you need to enable the debug logging on the client side.</span></span> <span data-ttu-id="efd91-158">İşte nasıl bunu yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="efd91-158">Here’s how you can do that:</span></span>

1. <span data-ttu-id="efd91-159">Hive config log4j özelliklerinde aşağıdaki özelliği yerleştirin.</span><span class="sxs-lookup"><span data-stu-id="efd91-159">Put the following property in the log4j properties in Hive config.</span></span> <span data-ttu-id="efd91-160">Bu Ambari görünümünden yapılabilir: log4j.logger.com.microsoft.azure.datalake.store=DEBUG tüm düğümleri/hizmet yapılandırma etkili olması yeniden başlatın.</span><span class="sxs-lookup"><span data-stu-id="efd91-160">This can be done from Ambari view: log4j.logger.com.microsoft.azure.datalake.store=DEBUG Restart all the nodes/service for the config to take effect.</span></span>

2. <span data-ttu-id="efd91-161">Kısıtlanan HTTP 429 hata kodunu hive günlük dosyasında görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="efd91-161">If you are getting throttled, you’ll see the HTTP 429 error code in the hive log file.</span></span> <span data-ttu-id="efd91-162">Hive günlük dosyası içinde /tmp/,&lt;kullanıcı&gt;/hive.log</span><span class="sxs-lookup"><span data-stu-id="efd91-162">The hive log file is in /tmp/&lt;user&gt;/hive.log</span></span>

## <a name="further-information-on-hive-tuning"></a><span data-ttu-id="efd91-163">Hive ayarlama hakkında daha fazla bilgi</span><span class="sxs-lookup"><span data-stu-id="efd91-163">Further information on Hive tuning</span></span>

<span data-ttu-id="efd91-164">Hive sorgularınızı ince ayar yardımcı olacak birkaç Web günlükleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="efd91-164">Here are a few blogs that will help tune your Hive queries:</span></span>
* [<span data-ttu-id="efd91-165">Hdınsight'ta Hadoop için Hive sorguları en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="efd91-165">Optimize Hive queries for Hadoop in HDInsight</span></span>](https://azure.microsoft.com/en-us/documentation/articles/hdinsight-hadoop-optimize-hive-query/)
* [<span data-ttu-id="efd91-166">Hive sorgusu performans sorunlarını giderme</span><span class="sxs-lookup"><span data-stu-id="efd91-166">Troubleshooting Hive query performance</span></span>](https://blogs.msdn.microsoft.com/bigdatasupport/2015/08/13/troubleshooting-hive-query-performance-in-hdinsight-hadoop-cluster/)
* [<span data-ttu-id="efd91-167">Konuşma göz atın üzerinde hdınsight'ta Hive en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="efd91-167">Ignite talk on optimize Hive on HDInsight</span></span>](https://channel9.msdn.com/events/Machine-Learning-and-Data-Sciences-Conference/Data-Science-Summit-2016/MSDSS25)
