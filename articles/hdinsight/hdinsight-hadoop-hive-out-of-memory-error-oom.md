---
title: "yetersiz bellek hatasını Azure hdınsight'ta Hive aaaFix | Microsoft Docs"
description: "Yetersiz bellek hatasını hdınsight'ta Hive düzeltin. Merhaba müşteri bir sorgu birçok büyük tabloları arasında bir senaryodur."
keywords: "yetersiz bellek hata, OOM, Hive ayarları"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 7bce3dff-9825-4fa0-a568-c52a9f7d1dad
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/17/2017
ms.author: jgao
ms.openlocfilehash: 00a12969322c1e74434ba6593ffd098f342edd84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="fix-a-hive-out-of-memory-error-in-azure-hdinsight"></a><span data-ttu-id="95c4a-105">Yetersiz bellek hatasını Azure hdınsight'ta Hive Düzelt</span><span class="sxs-lookup"><span data-stu-id="95c4a-105">Fix a Hive out of memory error in Azure HDInsight</span></span>

<span data-ttu-id="95c4a-106">Bilgi nasıl toofix Hive yetersiz bellek hatasını zaman büyük tabloları Hive bellek ayarlarını yapılandırarak işlem.</span><span class="sxs-lookup"><span data-stu-id="95c4a-106">Learn how toofix a Hive out of memory error when process large tables by configuring Hive memory settings.</span></span>

## <a name="run-hive-query-against-large-tables"></a><span data-ttu-id="95c4a-107">Hive sorgusu çalıştırma karşı büyük tabloları</span><span class="sxs-lookup"><span data-stu-id="95c4a-107">Run Hive query against large tables</span></span>

<span data-ttu-id="95c4a-108">Bir müşteri bir Hive sorgusu çalıştıran:</span><span class="sxs-lookup"><span data-stu-id="95c4a-108">A customer ran a Hive query:</span></span>

    SELECT
        COUNT (T1.COLUMN1) as DisplayColumn1,
        …
        …
        ….
    FROM
        TABLE1 T1,
        TABLE2 T2,
        TABLE3 T3,
        TABLE5 T4,
        TABLE6 T5,
        TABLE7 T6
    where (T1.KEY1 = T2.KEY1….
        …
        …

<span data-ttu-id="95c4a-109">Bu sorgunun bazı küçük farklar:</span><span class="sxs-lookup"><span data-stu-id="95c4a-109">Some nuances of this query:</span></span>

* <span data-ttu-id="95c4a-110">T1 bir diğer ad tooa büyük, çok sayıda dize sütun türleri sahip tablo1 tablodur.</span><span class="sxs-lookup"><span data-stu-id="95c4a-110">T1 is an alias tooa big table, TABLE1, which has lots of STRING column types.</span></span>
* <span data-ttu-id="95c4a-111">Diğer tablolar değil, büyük ancak çok sayıda sütuna sahip.</span><span class="sxs-lookup"><span data-stu-id="95c4a-111">Other tables are not that big but do have many columns.</span></span>
* <span data-ttu-id="95c4a-112">Tüm tabloları birbirlerine tablo1 ve diğerleri birden fazla sütunlu bazı durumlarda birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="95c4a-112">All tables are joining each other, in some cases with multiple columns in TABLE1 and others.</span></span>

<span data-ttu-id="95c4a-113">Hello Hive sorgusu 24 düğümü A3 Hdınsight kümesinde toofinish 26 dakika sürdü.</span><span class="sxs-lookup"><span data-stu-id="95c4a-113">hello Hive query took 26 minutes toofinish on a 24 node A3 HDInsight cluster.</span></span> <span data-ttu-id="95c4a-114">uyarı iletilerini aşağıdaki hello müşteri bildirilen hello:</span><span class="sxs-lookup"><span data-stu-id="95c4a-114">hello customer noticed hello following warning messages:</span></span>

    Warning: Map Join MAPJOIN[428][bigTable=?] in task 'Stage-21:MAPRED' is a cross product
    Warning: Shuffle Join JOIN[8][tables = [t1933775, t1932766]] in Stage 'Stage-4:MAPRED' is a cross product

<span data-ttu-id="95c4a-115">Merhaba Tez yürütme altyapısı kullanarak.</span><span class="sxs-lookup"><span data-stu-id="95c4a-115">By using hello Tez execution engine.</span></span> <span data-ttu-id="95c4a-116">aynı sorgu için 15 dakika çalıştırılmış ve aşağıdaki hata hello belirtti hello:</span><span class="sxs-lookup"><span data-stu-id="95c4a-116">hello same query ran for 15 minutes, and then threw hello following error:</span></span>

    Status: Failed
    Vertex failed, vertexName=Map 5, vertexId=vertex_1443634917922_0008_1_05, diagnostics=[Task failed, taskId=task_1443634917922_0008_1_05_000006, diagnostics=[TaskAttempt 0 failed, info=[Error: Failure while running task:java.lang.RuntimeException: java.lang.OutOfMemoryError: Java heap space
        at
    org.apache.hadoop.hive.ql.exec.tez.TezProcessor.initializeAndRunProcessor(TezProcessor.java:172)
        at org.apache.hadoop.hive.ql.exec.tez.TezProcessor.run(TezProcessor.java:138)
        at
    org.apache.tez.runtime.LogicalIOProcessorRuntimeTask.run(LogicalIOProcessorRuntimeTask.java:324)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable$1.run(TezTaskRunner.java:176)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable$1.run(TezTaskRunner.java:168)
        at java.security.AccessController.doPrivileged(Native Method)
        at javax.security.auth.Subject.doAs(Subject.java:415)
        at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1628)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable.call(TezTaskRunner.java:168)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable.call(TezTaskRunner.java:163)
        at java.util.concurrent.FutureTask.run(FutureTask.java:262)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
        at java.lang.Thread.run(Thread.java:745)
    Caused by: java.lang.OutOfMemoryError: Java heap space

<span data-ttu-id="95c4a-117">Merhaba hata daha büyük bir sanal makine (örneğin, D12) kullanırken kalır.</span><span class="sxs-lookup"><span data-stu-id="95c4a-117">hello error remains when using a bigger virtual machine (for example, D12).</span></span>


## <a name="debug-hello-out-of-memory-error"></a><span data-ttu-id="95c4a-118">Yetersiz bellek hatasını Hello hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="95c4a-118">Debug hello out of memory error</span></span>

<span data-ttu-id="95c4a-119">Bizim desteği ve mühendislik ekipleri birlikte, yetersiz bellek hatasını hello neden hello sorunlardan biri bulundu bir [hello Apache JIRA açıklanan sorunu bilinen](https://issues.apache.org/jira/browse/HIVE-8306):</span><span class="sxs-lookup"><span data-stu-id="95c4a-119">Our support and engineering teams together found one of hello issues causing hello out of memory error was a [known issue described in hello Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306):</span></span>

    When hive.auto.convert.join.noconditionaltask = true we check noconditionaltask.size and if hello sum  of tables sizes in hello map join is less than noconditionaltask.size hello plan would generate a Map join, hello issue with this is that hello calculation doesnt take into account hello overhead introduced by different HashTable implementation as results if hello sum of input sizes is smaller than hello noconditionaltask size by a small margin queries will hit OOM.

<span data-ttu-id="95c4a-120">Merhaba **hive.auto.convert.join.noconditionaltask** hello hive-site.xml dosyasının çok ayarlandı**true**:</span><span class="sxs-lookup"><span data-stu-id="95c4a-120">hello **hive.auto.convert.join.noconditionaltask** in hello hive-site.xml file was set too**true**:</span></span>

    <property>
        <name>hive.auto.convert.join.noconditionaltask</name>
        <value>true</value>
        <description>
              Whether Hive enables hello optimization about converting common join into mapjoin based on hello input file size.
              If this parameter is on, and hello sum of size for n-1 of hello tables/partitions for a n-way join is smaller than the
              specified size, hello join is directly converted tooa mapjoin (there is no conditional task).
        </description>
      </property>

<span data-ttu-id="95c4a-121">Büyük olasılıkla harita birleştirme edildi hello Java yığın alanı hello nedenini bizim bellek hatası.</span><span class="sxs-lookup"><span data-stu-id="95c4a-121">It is likely map join was hello cause of hello Java Heap Space our of memory error.</span></span> <span data-ttu-id="95c4a-122">Merhaba blog gönderisinde açıklandığı gibi [hdınsight'ta Hadoop Yarn bellek ayarlarını](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), Tez yürütme altyapısıdır kullanılan kullanılan hello yığın alanı gerçekte toohello Tez kapsayıcı ait olduğunda.</span><span class="sxs-lookup"><span data-stu-id="95c4a-122">As explained in hello blog post [Hadoop Yarn memory settings in HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), when Tez execution engine is used hello heap space used actually belongs toohello Tez container.</span></span> <span data-ttu-id="95c4a-123">Görüntü açıklayan hello Tez kapsayıcı bellek aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="95c4a-123">See hello following image describing hello Tez container memory.</span></span>

![Tez kapsayıcı bellek diyagramı: Hive yetersiz bellek hatası](./media/hdinsight-hadoop-hive-out-of-memory-error-oom/hive-out-of-memory-error-oom-tez-container-memory.png)

<span data-ttu-id="95c4a-125">İki bellek ayarlarını aşağıdaki hello Hello blog gönderisi da anlaşılacağı gibi hello öbek için hello kapsayıcı bellek tanımlayın: **hive.tez.container.size** ve **hive.tez.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="95c4a-125">As hello blog post suggests, hello following two memory settings define hello container memory for hello heap: **hive.tez.container.size** and **hive.tez.java.opts**.</span></span> <span data-ttu-id="95c4a-126">Bizim deneyimlerden hello kapsayıcı boyutu çok küçük bellek özel durum dışında hello anlamına gelmez.</span><span class="sxs-lookup"><span data-stu-id="95c4a-126">From our experience, hello out of memory exception does not mean hello container size is too small.</span></span> <span data-ttu-id="95c4a-127">Bu, hello Java yığın boyutu (hive.tez.java.opts) çok küçük anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="95c4a-127">It means hello Java heap size (hive.tez.java.opts) is too small.</span></span> <span data-ttu-id="95c4a-128">Bellek yetersiz gördüğünüzde tooincrease deneyebilirsiniz şekilde **hive.tez.java.opts**.</span><span class="sxs-lookup"><span data-stu-id="95c4a-128">So whenever you see out of memory, you can try tooincrease **hive.tez.java.opts**.</span></span> <span data-ttu-id="95c4a-129">Gerekirse tooincrease olabilir **hive.tez.container.size**.</span><span class="sxs-lookup"><span data-stu-id="95c4a-129">If needed you might have tooincrease **hive.tez.container.size**.</span></span> <span data-ttu-id="95c4a-130">Merhaba **java.opts** ayarı yaklaşık % 80'i olmalıdır **container.size**.</span><span class="sxs-lookup"><span data-stu-id="95c4a-130">hello **java.opts** setting should be around 80% of **container.size**.</span></span>

> [!NOTE]
> <span data-ttu-id="95c4a-131">Merhaba ayarı **hive.tez.java.opts** her zaman daha küçük olmalıdır **hive.tez.container.size**.</span><span class="sxs-lookup"><span data-stu-id="95c4a-131">hello setting **hive.tez.java.opts** must always be smaller than **hive.tez.container.size**.</span></span>
> 
> 

<span data-ttu-id="95c4a-132">D12 makinede 28 GB bellek bulunduğundan, biz toouse kapsayıcı boyutu 10 GB (10240 MB) karar ve % 80 toojava.opts atayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="95c4a-132">Because a D12 machine has 28GB memory, we decided toouse a container size of 10GB (10240MB) and assign 80% toojava.opts:</span></span>

    SET hive.tez.container.size=10240
    SET hive.tez.java.opts=-Xmx8192m

<span data-ttu-id="95c4a-133">Merhaba yeni ayarlarla hello sorgu altında 10 dakika içinde başarıyla çalıştırıldı.</span><span class="sxs-lookup"><span data-stu-id="95c4a-133">With hello new settings, hello query successfully ran in under 10 minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="95c4a-134">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="95c4a-134">Next steps</span></span>

<span data-ttu-id="95c4a-135">OOM hata alma mutlaka hello kapsayıcı boyutu çok küçük anlamına gelmez.</span><span class="sxs-lookup"><span data-stu-id="95c4a-135">Getting an OOM error doesn't necessarily mean hello container size is too small.</span></span> <span data-ttu-id="95c4a-136">Bunun yerine, böylece Hello yığın boyutu artar ve hello kapsayıcı bellek boyutu % 80'en az hello bellek ayarlarını yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="95c4a-136">Instead, you should configure hello memory settings so that hello heap size is increased and is at least 80% of hello container memory size.</span></span> <span data-ttu-id="95c4a-137">Hive sorguları iyileştirmek için bkz: [hdınsight'ta Hadoop için en iyi duruma getirme Hive sorguları](hdinsight-hadoop-optimize-hive-query.md).</span><span class="sxs-lookup"><span data-stu-id="95c4a-137">For optimizing Hive queries, see [Optimize Hive queries for Hadoop in HDInsight](hdinsight-hadoop-optimize-hive-query.md).</span></span>
