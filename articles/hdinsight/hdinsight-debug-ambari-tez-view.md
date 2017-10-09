---
title: "aaaUse Ambari Tez görünümü Hdınsight - Azure ile | Microsoft Docs"
description: "Nasıl toouse hello Ambari Tez görüntülemek toodebug Tez işlerinde Hdınsight'ta öğrenin."
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
ms.openlocfilehash: 5d61bd0403c98284c86982073af91468ae62ac60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-ambari-views-toodebug-tez-jobs-on-hdinsight"></a><span data-ttu-id="9ce8e-103">Hdınsight üzerinde Ambari görünümleri toodebug Tez işlerinde kullanın</span><span class="sxs-lookup"><span data-stu-id="9ce8e-103">Use Ambari Views toodebug Tez Jobs on HDInsight</span></span>

<span data-ttu-id="9ce8e-104">Merhaba Hdınsight için Ambari Web kullanıcı Arabirimi Tez kullanan kullanılan toounderstand ve hata ayıklama işleri olabilir bir Tez görünümü içerir.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-104">hello Ambari Web UI for HDInsight contains a Tez view that can be used toounderstand and debug jobs that use Tez.</span></span> <span data-ttu-id="9ce8e-105">bir grafik bağlı öğelerinin her öğenin ayrıntısına ve istatistikleri ve günlük kaydı bilgilerini almak hello Tez görünümü toovisualize hello iş sağlar.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-105">hello Tez view allows you toovisualize hello job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9ce8e-106">Bu belgedeki Hello adımlar Linux kullanan bir Hdınsight kümesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-106">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="9ce8e-107">Linux hello yalnızca Hdınsight sürüm 3.4 veya büyük kullanılan işletim sistemini ' dir.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9ce8e-108">Daha fazla bilgi için bkz: [Hdınsight bileşen sürümü oluşturma](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="9ce8e-108">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9ce8e-109">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="9ce8e-109">Prerequisites</span></span>

* <span data-ttu-id="9ce8e-110">Linux tabanlı Hdınsight kümesi.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-110">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="9ce8e-111">Küme oluşturma adımları için bkz: [Linux tabanlı Hdınsight kullanmaya başlama](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9ce8e-111">For steps on creating a cluster, see [Get started using Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="9ce8e-112">HTML5'i destekleyen modern bir web tarayıcısı.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-112">A modern web browser that supports HTML5.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="9ce8e-113">Tez anlama</span><span class="sxs-lookup"><span data-stu-id="9ce8e-113">Understanding Tez</span></span>

<span data-ttu-id="9ce8e-114">Tez geleneksel MapReduce işleme büyük hızlarından sağlayan hadoop'ta veri işleme için genişletilebilir bir çerçevedir.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-114">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="9ce8e-115">Linux tabanlı Hdınsight kümeleri için bunu hello varsayılan Hive için altyapısıdır.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-115">For Linux-based HDInsight clusters, it is hello default engine for Hive.</span></span>

<span data-ttu-id="9ce8e-116">Tez yönlendirilmiş Çevrimsiz grafik (Merhaba işlerinin gerekli eylemlerin sırasını açıklayan DAG) oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-116">Tez creates a Directed Acyclic Graph (DAG) that describes hello order of actions required by jobs.</span></span> <span data-ttu-id="9ce8e-117">Tek tek Eylemler köşeleri olarak adlandırılır ve hello parçası yürütmek genel işi.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-117">Individual actions are called vertices, and execute a piece of hello overall job.</span></span> <span data-ttu-id="9ce8e-118">Merhaba gerçek yürütme hello iş köşe tarafından tanımlanan bir görev çağrılır ve hello kümedeki birden çok düğüm arasında dağıtılmış.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-118">hello actual execution of hello work described by a vertex is called a task, and may be distributed across multiple nodes in hello cluster.</span></span>

### <a name="understanding-hello-tez-view"></a><span data-ttu-id="9ce8e-119">Anlama hello Tez görünümü</span><span class="sxs-lookup"><span data-stu-id="9ce8e-119">Understanding hello Tez view</span></span>

<span data-ttu-id="9ce8e-120">Hello Tez görünümü, çalışan işlemler üzerinde hem geçmiş bilgileri hem de bilgi sağlar.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-120">hello Tez view provides both historical information and information on processes that are running.</span></span> <span data-ttu-id="9ce8e-121">Bu bilgileri, bir iş kümeler arasında nasıl dağıtıldığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-121">This information shows how a job is distributed across clusters.</span></span> <span data-ttu-id="9ce8e-122">Ayrıca görevleri ve köşeleri tarafından kullanılan sayaçları görüntüler ve toohello iş ilgili hata bilgileri.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-122">It also displays counters used by tasks and vertices, and error information related toohello job.</span></span> <span data-ttu-id="9ce8e-123">Aşağıdaki senaryolar hello yararlı bilgiler teklif edebilir:</span><span class="sxs-lookup"><span data-stu-id="9ce8e-123">It may offer useful information in hello following scenarios:</span></span>

* <span data-ttu-id="9ce8e-124">Uzun süre çalışan işlemleri görüntüleme, izleme harita ilerlemesini hello ve görevleri azaltır.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-124">Monitoring long-running processes, viewing hello progress of map and reduce tasks.</span></span>
* <span data-ttu-id="9ce8e-125">Başarılı veya başarısız işlemler toolearn ilişkin geçmiş verileri analiz etme işleme nasıl geliştirilmiş veya neden başarısız oldu.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-125">Analyzing historical data for successful or failed processes toolearn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="9ce8e-126">Bir DAG oluştur</span><span class="sxs-lookup"><span data-stu-id="9ce8e-126">Generate a DAG</span></span>

<span data-ttu-id="9ce8e-127">Merhaba Tez altyapısı kullanan bir iş hello görünüm yalnızca veri varsa, Tez çalışmakta olduğu veya sahip olan çalıştıran daha önce.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-127">hello Tez view only contains data if a job that uses hello Tez engine is currently running, or has been ran previously.</span></span> <span data-ttu-id="9ce8e-128">Basit Hive sorguları, Tez kullanmadan çözülebilir.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-128">Simple Hive queries can be resolved without using Tez.</span></span> <span data-ttu-id="9ce8e-129">Daha karmaşık Bu filtreleme, gruplama, sıralama, birleşimler, vb. sorgular.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-129">More complex queries that do filtering, grouping, ordering, joins, etc.</span></span> <span data-ttu-id="9ce8e-130">Merhaba Tez altyapısını kullanır.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-130">use hello Tez engine.</span></span>

<span data-ttu-id="9ce8e-131">Aşağıdaki adımları toorun Tez kullanan bir Hive sorgusu hello kullan:</span><span class="sxs-lookup"><span data-stu-id="9ce8e-131">Use hello following steps toorun a Hive query that uses Tez:</span></span>

1. <span data-ttu-id="9ce8e-132">Toohttps://CLUSTERNAME.azurehdinsight.net, bir web tarayıcısında gidin nerede **CLUSTERNAME** Hdınsight kümenize hello adıdır.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-132">In a web browser, navigate toohttps://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of your HDInsight cluster.</span></span>

2. <span data-ttu-id="9ce8e-133">Merhaba hello sayfanın üst kısmındaki hello Hello menüsünden seçin **görünümleri** simgesi.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-133">From hello menu at hello top of hello page, select hello **Views** icon.</span></span> <span data-ttu-id="9ce8e-134">Bu simgeyi bir dizi kare gibi görünüyor.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-134">This icon looks like a series of squares.</span></span> <span data-ttu-id="9ce8e-135">Görüntülenen hello açılır seçin **Hive görünümü**.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-135">In hello dropdown that appears, select **Hive view**.</span></span>

    ![Hive görünümünü seçme](./media/hdinsight-debug-ambari-tez-view/selecthive.png)

3. <span data-ttu-id="9ce8e-137">Merhaba Hive görünümü yüklediğinde, Yapıştır hello aşağıdaki sorgu hello sorgu Düzenleyicisi'ni ve ardından **yürütme**.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-137">When hello Hive view loads, paste hello following query into hello Query Editor, and then click **execute**.</span></span>

        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;

    <span data-ttu-id="9ce8e-138">Merhaba işi tamamlandıktan sonra hello görüntülenen hello çıktı görmeniz gerekir **sorgu işleminin sonuçları** bölümü.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-138">Once hello job has completed, you should see hello output displayed in hello **Query Process Results** section.</span></span> <span data-ttu-id="9ce8e-139">Merhaba sonuçları benzer toohello metin aşağıdaki gibi olmalıdır:</span><span class="sxs-lookup"><span data-stu-id="9ce8e-139">hello results should be similar toohello following text:</span></span>

        market  state       country
        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica

4. <span data-ttu-id="9ce8e-140">Select hello **günlük** sekmesi. Metin aşağıdaki bilgileri benzer toohello bakın:</span><span class="sxs-lookup"><span data-stu-id="9ce8e-140">Select hello **Log** tab. You see information similar toohello following text:</span></span>

        INFO : Session is already open
        INFO :

        INFO : Status: Running (Executing on YARN cluster with App id application_1454546500517_0063)

    <span data-ttu-id="9ce8e-141">Merhaba Kaydet **uygulama kimliği** olarak bu değer hello sonraki bölümde kullanılan değer.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-141">Save hello **App id** value, as this value is used in hello next section.</span></span>

## <a name="use-hello-tez-view"></a><span data-ttu-id="9ce8e-142">Merhaba Tez görünüm kullanın</span><span class="sxs-lookup"><span data-stu-id="9ce8e-142">Use hello Tez View</span></span>

1. <span data-ttu-id="9ce8e-143">Merhaba hello sayfanın üst kısmındaki hello Hello menüsünden seçin **görünümleri** simgesi.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-143">From hello menu at hello top of hello page, select hello **Views** icon.</span></span> <span data-ttu-id="9ce8e-144">Görüntülenen hello açılır seçin **Tez Görünüm**.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-144">In hello dropdown that appears, select **Tez view**.</span></span>

    ![Tez görünümü seçme](./media/hdinsight-debug-ambari-tez-view/selecttez.png)

2. <span data-ttu-id="9ce8e-146">Merhaba Tez görünüm yüklediğinde, şu anda çalışmakta olan veya kaldırılmış hive sorguları listesini hello küme üzerinde çalışan bakın.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-146">When hello Tez view loads, you see a list of hive queries that are currently running, or have been ran on hello cluster.</span></span>

    ![Tüm DAG'leri](./media/hdinsight-debug-ambari-tez-view/tez-view-home.png)

3. <span data-ttu-id="9ce8e-148">Yalnızca bir giriş varsa, önceki bölümde hello çalıştırdığınız hello sorgu içindir.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-148">If you have only one entry, it is for hello query that you ran in hello previous section.</span></span> <span data-ttu-id="9ce8e-149">Birden çok girdi varsa, hello hello sayfanın başında hello alanlarını kullanarak arama yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-149">If you have multiple entries, you can search by using hello fields at hello top of hello page.</span></span>

4. <span data-ttu-id="9ce8e-150">Select hello **sorgu kimliği** bir Hive sorgusu için.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-150">Select hello **Query ID** for a Hive query.</span></span> <span data-ttu-id="9ce8e-151">Merhaba sorgu ilgili bilgiler görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-151">Information about hello query is displayed.</span></span>

    ![DAG ayrıntıları](./media/hdinsight-debug-ambari-tez-view/query-details.png)

5. <span data-ttu-id="9ce8e-153">Bu sayfada Hello sekmeleri bilgisinden tooview hello izin ver:</span><span class="sxs-lookup"><span data-stu-id="9ce8e-153">hello tabs on this page allow you tooview hello following information:</span></span>

    * <span data-ttu-id="9ce8e-154">**Sorgu ayrıntıları**: hello Hive sorgusu hakkında ayrıntılar.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-154">**Query Details**: Details about hello Hive query.</span></span>
    * <span data-ttu-id="9ce8e-155">**Zaman Çizelgesi**: her aşaması ne kadar sürdü hakkında bilgi.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-155">**Timeline**: Information about how long each stage of processing took.</span></span>
    * <span data-ttu-id="9ce8e-156">**Yapılandırmaları**: Bu sorgu için kullanılan hello yapılandırma.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-156">**Configurations**: hello configuration used for this query.</span></span>

    <span data-ttu-id="9ce8e-157">Gelen __sorgu ayrıntıları__ hello bağlantılar toofind hello bilgilerini kullanabilirsiniz __uygulama__ veya hello __DAG__ bu sorgu için.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-157">From __Query Details__ you can use hello links toofind information about hello __Application__ or hello __DAG__ for this query.</span></span>
    
    * <span data-ttu-id="9ce8e-158">Merhaba __uygulama__ bağlantı hello bu sorgu için YARN uygulama hakkında daha fazla bilgi görüntüler.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-158">hello __Application__ link displays information about hello YARN application for this query.</span></span> <span data-ttu-id="9ce8e-159">Buradan hello YARN uygulama günlüklerini erişebilir.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-159">From here you can access hello YARN application logs.</span></span>
    * <span data-ttu-id="9ce8e-160">Merhaba __DAG__ bağlantı hello yönlendirilmiş Çevrimsiz grafik, bu sorgu için hakkında daha fazla bilgi görüntüler.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-160">hello __DAG__ link displays information about hello directed acyclic graph for this query.</span></span> <span data-ttu-id="9ce8e-161">Buradan, grafiksel hello DAG görüntüleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-161">From here you can view a graphical representation of hello DAG.</span></span> <span data-ttu-id="9ce8e-162">Ayrıca hello köşeleri hello DAG içinde hakkında bilgi bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9ce8e-162">You can also find information on hello vertices within hello DAG.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ce8e-163">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="9ce8e-163">Next Steps</span></span>

<span data-ttu-id="9ce8e-164">Toouse hello Tez nasıl görüntüleyebilirim öğrendiniz, daha fazla bilgi edinmek [hdınsight'ta Hive kullanarak](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="9ce8e-164">Now that you have learned how toouse hello Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="9ce8e-165">Daha ayrıntılı Tez teknik bilgi için bkz: Merhaba [Hortonworks Tez sayfanın](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="9ce8e-165">For more detailed technical information on Tez, see hello [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="9ce8e-166">Ambari kullanarak Hdınsight ile ilgili daha fazla bilgi için bkz: [hello Ambari Web kullanıcı arabirimini kullanarak yönetin Hdınsight kümeleri](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="9ce8e-166">For more information on using Ambari with HDInsight, see [Manage HDInsight clusters using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md)</span></span>
