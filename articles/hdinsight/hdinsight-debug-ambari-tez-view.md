---
title: "Hdınsight ile - Azure Ambari Tez görünümünü kullanın | Microsoft Docs"
description: "Tez işlerinde hdınsight'ta hata ayıklamak için Ambari Tez görünümü kullanmayı öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 9c39ea56-670b-4699-aba0-0f64c261e411
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 65d89309b9eea8544b85d16687baa90d49688d77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/03/2017
---
# <a name="use-ambari-views-to-debug-tez-jobs-on-hdinsight"></a><span data-ttu-id="64f2b-103">Tez işlerinde hdınsight'ta hata ayıklamak için Ambari görünümleri kullanma</span><span class="sxs-lookup"><span data-stu-id="64f2b-103">Use Ambari Views to debug Tez Jobs on HDInsight</span></span>

<span data-ttu-id="64f2b-104">Hdınsight için Ambari Web kullanıcı arabirimini anlama ve Tez kullanan işleri hata ayıklamak için kullanılan bir Tez görünümü içerir.</span><span class="sxs-lookup"><span data-stu-id="64f2b-104">The Ambari Web UI for HDInsight contains a Tez view that can be used to understand and debug jobs that use Tez.</span></span> <span data-ttu-id="64f2b-105">Tez görünümü iş bağlı öğelerinin bir grafik olarak görselleştirme, her öğenin ayrıntısına ve istatistikler ve günlük bilgileri almasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="64f2b-105">The Tez view allows you to visualize the job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="64f2b-106">Bu belgede yer alan adımlar Linux kullanan bir Hdınsight kümesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="64f2b-106">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="64f2b-107">Linux, HDInsight sürüm 3.4 ve üzerinde kullanılan tek işletim sistemidir.</span><span class="sxs-lookup"><span data-stu-id="64f2b-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="64f2b-108">Daha fazla bilgi için bkz: [Hdınsight bileşen sürümü oluşturma](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="64f2b-108">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64f2b-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="64f2b-109">Prerequisites</span></span>

* <span data-ttu-id="64f2b-110">Linux tabanlı Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="64f2b-110">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="64f2b-111">Küme oluşturma adımları için bkz: [Linux tabanlı Hdınsight kullanmaya başlama](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="64f2b-111">For steps on creating a cluster, see [Get started using Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="64f2b-112">HTML5'i destekleyen modern bir web tarayıcısı.</span><span class="sxs-lookup"><span data-stu-id="64f2b-112">A modern web browser that supports HTML5.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="64f2b-113">Tez anlama</span><span class="sxs-lookup"><span data-stu-id="64f2b-113">Understanding Tez</span></span>

<span data-ttu-id="64f2b-114">Tez geleneksel MapReduce işleme büyük hızlarından sağlayan hadoop'ta veri işleme için genişletilebilir bir çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="64f2b-114">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="64f2b-115">Linux tabanlı Hdınsight kümeleri için onu varsayılan Hive için altyapısıdır.</span><span class="sxs-lookup"><span data-stu-id="64f2b-115">For Linux-based HDInsight clusters, it is the default engine for Hive.</span></span>

<span data-ttu-id="64f2b-116">Tez yönlendirilmiş Çevrimsiz grafik (işlerinin gerekli eylemlerin sırasını açıklayan DAG) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="64f2b-116">Tez creates a Directed Acyclic Graph (DAG) that describes the order of actions required by jobs.</span></span> <span data-ttu-id="64f2b-117">Tek tek Eylemler köşeleri olarak adlandırılır ve genel iş parçası yürütün.</span><span class="sxs-lookup"><span data-stu-id="64f2b-117">Individual actions are called vertices, and execute a piece of the overall job.</span></span> <span data-ttu-id="64f2b-118">Gerçek yürütme köşe tarafından açıklanan iş bir görev çağrılır ve kümedeki birden çok düğüm arasında dağıtılmış.</span><span class="sxs-lookup"><span data-stu-id="64f2b-118">The actual execution of the work described by a vertex is called a task, and may be distributed across multiple nodes in the cluster.</span></span>

### <a name="understanding-the-tez-view"></a><span data-ttu-id="64f2b-119">Tez görünüm anlama</span><span class="sxs-lookup"><span data-stu-id="64f2b-119">Understanding the Tez view</span></span>

<span data-ttu-id="64f2b-120">Tez görünümü, çalışan işlemler üzerinde hem geçmiş bilgileri hem de bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="64f2b-120">The Tez view provides both historical information and information on processes that are running.</span></span> <span data-ttu-id="64f2b-121">Bu bilgileri, bir iş kümeler arasında nasıl dağıtıldığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="64f2b-121">This information shows how a job is distributed across clusters.</span></span> <span data-ttu-id="64f2b-122">Ayrıca, görevler ve köşeleri tarafından kullanılan sayaçlarını ve işle ilgili hata bilgilerini görüntüler.</span><span class="sxs-lookup"><span data-stu-id="64f2b-122">It also displays counters used by tasks and vertices, and error information related to the job.</span></span> <span data-ttu-id="64f2b-123">Aşağıdaki senaryolarda yararlı bilgiler teklif edebilir:</span><span class="sxs-lookup"><span data-stu-id="64f2b-123">It may offer useful information in the following scenarios:</span></span>

* <span data-ttu-id="64f2b-124">Uzun süre çalışan izleme harita ilerlemesini görüntüleme, işler ve görevler azaltır.</span><span class="sxs-lookup"><span data-stu-id="64f2b-124">Monitoring long-running processes, viewing the progress of map and reduce tasks.</span></span>
* <span data-ttu-id="64f2b-125">İşleme nasıl geliştirilmiş veya neden başarısız öğrenmek başarılı veya başarısız işlemler için geçmiş verileri analiz etme.</span><span class="sxs-lookup"><span data-stu-id="64f2b-125">Analyzing historical data for successful or failed processes to learn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="64f2b-126">Bir DAG oluştur</span><span class="sxs-lookup"><span data-stu-id="64f2b-126">Generate a DAG</span></span>

<span data-ttu-id="64f2b-127">Tez görünüm Tez Altyapısı şu anda çalışıyor ya da bırakıldı kullanan önceden çalıştıran bir iş, yalnızca veri içeriyor.</span><span class="sxs-lookup"><span data-stu-id="64f2b-127">The Tez view only contains data if a job that uses the Tez engine is currently running, or has been ran previously.</span></span> <span data-ttu-id="64f2b-128">Basit Hive sorguları, Tez kullanmadan çözülebilir.</span><span class="sxs-lookup"><span data-stu-id="64f2b-128">Simple Hive queries can be resolved without using Tez.</span></span> <span data-ttu-id="64f2b-129">Daha karmaşık Bu filtreleme, gruplama, sıralama, birleşimler, vb. sorgular.</span><span class="sxs-lookup"><span data-stu-id="64f2b-129">More complex queries that do filtering, grouping, ordering, joins, etc.</span></span> <span data-ttu-id="64f2b-130">Tez altyapısını kullanır.</span><span class="sxs-lookup"><span data-stu-id="64f2b-130">use the Tez engine.</span></span>

<span data-ttu-id="64f2b-131">Tez kullanan bir Hive sorgusu çalıştırmak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="64f2b-131">Use the following steps to run a Hive query that uses Tez:</span></span>

1. <span data-ttu-id="64f2b-132">Bir web tarayıcısında https://CLUSTERNAME.azurehdinsight.net için gidin nerede **CLUSTERNAME** Hdınsight kümenizin adıdır.</span><span class="sxs-lookup"><span data-stu-id="64f2b-132">In a web browser, navigate to https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your HDInsight cluster.</span></span>

2. <span data-ttu-id="64f2b-133">Sayfanın üstündeki menüsünden seçin **görünümleri** simgesi.</span><span class="sxs-lookup"><span data-stu-id="64f2b-133">From the menu at the top of the page, select the **Views** icon.</span></span> <span data-ttu-id="64f2b-134">Bu simgeyi bir dizi kare gibi görünüyor.</span><span class="sxs-lookup"><span data-stu-id="64f2b-134">This icon looks like a series of squares.</span></span> <span data-ttu-id="64f2b-135">Görüntülenen açılır menüde seçin **Hive görünümü**.</span><span class="sxs-lookup"><span data-stu-id="64f2b-135">In the dropdown that appears, select **Hive view**.</span></span>

    ![Hive görünümünü seçme](./media/hdinsight-debug-ambari-tez-view/selecthive.png)

3. <span data-ttu-id="64f2b-137">Hive görünümü yüklediğinde, aşağıdaki sorguyu sorgu düzenleyicisine yapıştırın ve ardından **yürütme**.</span><span class="sxs-lookup"><span data-stu-id="64f2b-137">When the Hive view loads, paste the following query into the Query Editor, and then click **execute**.</span></span>

        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;

    <span data-ttu-id="64f2b-138">İş tamamlandıktan sonra görüntülenen bir çıktı göreceksiniz **sorgu işleminin sonuçları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="64f2b-138">Once the job has completed, you should see the output displayed in the **Query Process Results** section.</span></span> <span data-ttu-id="64f2b-139">Sonuçlar aşağıdakine benzer olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="64f2b-139">The results should be similar to the following text:</span></span>

        market  state       country
        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica

4. <span data-ttu-id="64f2b-140">Seçin **günlük** sekmesi.</span><span class="sxs-lookup"><span data-stu-id="64f2b-140">Select the **Log** tab.</span></span> <span data-ttu-id="64f2b-141">Aşağıdakine benzer bilgiler bakın:</span><span class="sxs-lookup"><span data-stu-id="64f2b-141">You see information similar to the following text:</span></span>

        INFO : Session is already open
        INFO :

        INFO : Status: Running (Executing on YARN cluster with App id application_1454546500517_0063)

    <span data-ttu-id="64f2b-142">Kaydet **uygulama kimliği** değeri olarak bu değer bir sonraki bölümde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="64f2b-142">Save the **App id** value, as this value is used in the next section.</span></span>

## <a name="use-the-tez-view"></a><span data-ttu-id="64f2b-143">Tez görünümünü kullanın</span><span class="sxs-lookup"><span data-stu-id="64f2b-143">Use the Tez View</span></span>

1. <span data-ttu-id="64f2b-144">Sayfanın üstündeki menüsünden seçin **görünümleri** simgesi.</span><span class="sxs-lookup"><span data-stu-id="64f2b-144">From the menu at the top of the page, select the **Views** icon.</span></span> <span data-ttu-id="64f2b-145">Görüntülenen açılır menüde seçin **Tez Görünüm**.</span><span class="sxs-lookup"><span data-stu-id="64f2b-145">In the dropdown that appears, select **Tez view**.</span></span>

    ![Tez görünümü seçme](./media/hdinsight-debug-ambari-tez-view/selecttez.png)

2. <span data-ttu-id="64f2b-147">Tez görünüm yüklenirken, şu anda çalışmakta olan veya kaldırılmış hive sorguları listesini küme üzerinde çalışan bakın.</span><span class="sxs-lookup"><span data-stu-id="64f2b-147">When the Tez view loads, you see a list of hive queries that are currently running, or have been ran on the cluster.</span></span>

    ![Tüm DAG'leri](./media/hdinsight-debug-ambari-tez-view/tez-view-home.png)

3. <span data-ttu-id="64f2b-149">Yalnızca bir giriş varsa, önceki bölümde çalıştırdığınız sorgu içindir.</span><span class="sxs-lookup"><span data-stu-id="64f2b-149">If you have only one entry, it is for the query that you ran in the previous section.</span></span> <span data-ttu-id="64f2b-150">Birden çok girdi varsa, sayfanın en üstünde alanlar kullanılarak arayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64f2b-150">If you have multiple entries, you can search by using the fields at the top of the page.</span></span>

4. <span data-ttu-id="64f2b-151">Seçin **sorgu kimliği** bir Hive sorgusu için.</span><span class="sxs-lookup"><span data-stu-id="64f2b-151">Select the **Query ID** for a Hive query.</span></span> <span data-ttu-id="64f2b-152">Sorgu hakkında bilgi görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="64f2b-152">Information about the query is displayed.</span></span>

    ![DAG ayrıntıları](./media/hdinsight-debug-ambari-tez-view/query-details.png)

5. <span data-ttu-id="64f2b-154">Bu sayfa sekmelerinde, aşağıdaki bilgileri görüntülemek izin ver:</span><span class="sxs-lookup"><span data-stu-id="64f2b-154">The tabs on this page allow you to view the following information:</span></span>

    * <span data-ttu-id="64f2b-155">**Sorgu ayrıntıları**: Hive sorgusu hakkında ayrıntılar.</span><span class="sxs-lookup"><span data-stu-id="64f2b-155">**Query Details**: Details about the Hive query.</span></span>
    * <span data-ttu-id="64f2b-156">**Zaman Çizelgesi**: her aşaması ne kadar sürdü hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="64f2b-156">**Timeline**: Information about how long each stage of processing took.</span></span>
    * <span data-ttu-id="64f2b-157">**Yapılandırmaları**: Bu sorgu için kullanılan yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="64f2b-157">**Configurations**: The configuration used for this query.</span></span>

    <span data-ttu-id="64f2b-158">Gelen __sorgu ayrıntıları__ bağlantılar hakkında bilgi bulmak için kullanabileceğiniz __uygulama__ veya __DAG__ bu sorgu için.</span><span class="sxs-lookup"><span data-stu-id="64f2b-158">From __Query Details__ you can use the links to find information about the __Application__ or the __DAG__ for this query.</span></span>
    
    * <span data-ttu-id="64f2b-159">__Uygulama__ bağlantı bu sorgu için YARN uygulaması hakkında daha fazla bilgi görüntüler.</span><span class="sxs-lookup"><span data-stu-id="64f2b-159">The __Application__ link displays information about the YARN application for this query.</span></span> <span data-ttu-id="64f2b-160">Buradan YARN uygulama günlüklerini erişebilir.</span><span class="sxs-lookup"><span data-stu-id="64f2b-160">From here you can access the YARN application logs.</span></span>
    * <span data-ttu-id="64f2b-161">__DAG__ bağlantı yönlendirilmiş Çevrimsiz grafik için bu sorguyu hakkında daha fazla bilgi görüntüler.</span><span class="sxs-lookup"><span data-stu-id="64f2b-161">The __DAG__ link displays information about the directed acyclic graph for this query.</span></span> <span data-ttu-id="64f2b-162">Buradan, grafiksel DAG görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64f2b-162">From here you can view a graphical representation of the DAG.</span></span> <span data-ttu-id="64f2b-163">Ayrıca, DAG içinde köşeleri hakkında bilgi bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="64f2b-163">You can also find information on the vertices within the DAG.</span></span>

## <a name="next-steps"></a><span data-ttu-id="64f2b-164">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="64f2b-164">Next Steps</span></span>

<span data-ttu-id="64f2b-165">Tez görünümü kullanmak öğrendiniz, daha fazla bilgi edinmek [hdınsight'ta Hive kullanarak](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="64f2b-165">Now that you have learned how to use the Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="64f2b-166">Daha ayrıntılı Tez teknik bilgi için bkz: [Hortonworks Tez sayfanın](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="64f2b-166">For more detailed technical information on Tez, see the [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="64f2b-167">Ambari kullanarak Hdınsight ile ilgili daha fazla bilgi için bkz: [Ambari Web kullanıcı arabirimini kullanarak Hdınsight kümelerini yönetme](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="64f2b-167">For more information on using Ambari with HDInsight, see [Manage HDInsight clusters using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md)</span></span>
