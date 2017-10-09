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
# <a name="fix-a-hive-out-of-memory-error-in-azure-hdinsight"></a>Yetersiz bellek hatasını Azure hdınsight'ta Hive Düzelt

Bilgi nasıl toofix Hive yetersiz bellek hatasını zaman büyük tabloları Hive bellek ayarlarını yapılandırarak işlem.

## <a name="run-hive-query-against-large-tables"></a>Hive sorgusu çalıştırma karşı büyük tabloları

Bir müşteri bir Hive sorgusu çalıştıran:

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

Bu sorgunun bazı küçük farklar:

* T1 bir diğer ad tooa büyük, çok sayıda dize sütun türleri sahip tablo1 tablodur.
* Diğer tablolar değil, büyük ancak çok sayıda sütuna sahip.
* Tüm tabloları birbirlerine tablo1 ve diğerleri birden fazla sütunlu bazı durumlarda birleştirebilirsiniz.

Hello Hive sorgusu 24 düğümü A3 Hdınsight kümesinde toofinish 26 dakika sürdü. uyarı iletilerini aşağıdaki hello müşteri bildirilen hello:

    Warning: Map Join MAPJOIN[428][bigTable=?] in task 'Stage-21:MAPRED' is a cross product
    Warning: Shuffle Join JOIN[8][tables = [t1933775, t1932766]] in Stage 'Stage-4:MAPRED' is a cross product

Merhaba Tez yürütme altyapısı kullanarak. aynı sorgu için 15 dakika çalıştırılmış ve aşağıdaki hata hello belirtti hello:

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

Merhaba hata daha büyük bir sanal makine (örneğin, D12) kullanırken kalır.


## <a name="debug-hello-out-of-memory-error"></a>Yetersiz bellek hatasını Hello hata ayıklama

Bizim desteği ve mühendislik ekipleri birlikte, yetersiz bellek hatasını hello neden hello sorunlardan biri bulundu bir [hello Apache JIRA açıklanan sorunu bilinen](https://issues.apache.org/jira/browse/HIVE-8306):

    When hive.auto.convert.join.noconditionaltask = true we check noconditionaltask.size and if hello sum  of tables sizes in hello map join is less than noconditionaltask.size hello plan would generate a Map join, hello issue with this is that hello calculation doesnt take into account hello overhead introduced by different HashTable implementation as results if hello sum of input sizes is smaller than hello noconditionaltask size by a small margin queries will hit OOM.

Merhaba **hive.auto.convert.join.noconditionaltask** hello hive-site.xml dosyasının çok ayarlandı**true**:

    <property>
        <name>hive.auto.convert.join.noconditionaltask</name>
        <value>true</value>
        <description>
              Whether Hive enables hello optimization about converting common join into mapjoin based on hello input file size.
              If this parameter is on, and hello sum of size for n-1 of hello tables/partitions for a n-way join is smaller than the
              specified size, hello join is directly converted tooa mapjoin (there is no conditional task).
        </description>
      </property>

Büyük olasılıkla harita birleştirme edildi hello Java yığın alanı hello nedenini bizim bellek hatası. Merhaba blog gönderisinde açıklandığı gibi [hdınsight'ta Hadoop Yarn bellek ayarlarını](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), Tez yürütme altyapısıdır kullanılan kullanılan hello yığın alanı gerçekte toohello Tez kapsayıcı ait olduğunda. Görüntü açıklayan hello Tez kapsayıcı bellek aşağıdaki hello bakın.

![Tez kapsayıcı bellek diyagramı: Hive yetersiz bellek hatası](./media/hdinsight-hadoop-hive-out-of-memory-error-oom/hive-out-of-memory-error-oom-tez-container-memory.png)

İki bellek ayarlarını aşağıdaki hello Hello blog gönderisi da anlaşılacağı gibi hello öbek için hello kapsayıcı bellek tanımlayın: **hive.tez.container.size** ve **hive.tez.java.opts**. Bizim deneyimlerden hello kapsayıcı boyutu çok küçük bellek özel durum dışında hello anlamına gelmez. Bu, hello Java yığın boyutu (hive.tez.java.opts) çok küçük anlamına gelir. Bellek yetersiz gördüğünüzde tooincrease deneyebilirsiniz şekilde **hive.tez.java.opts**. Gerekirse tooincrease olabilir **hive.tez.container.size**. Merhaba **java.opts** ayarı yaklaşık % 80'i olmalıdır **container.size**.

> [!NOTE]
> Merhaba ayarı **hive.tez.java.opts** her zaman daha küçük olmalıdır **hive.tez.container.size**.
> 
> 

D12 makinede 28 GB bellek bulunduğundan, biz toouse kapsayıcı boyutu 10 GB (10240 MB) karar ve % 80 toojava.opts atayabilirsiniz:

    SET hive.tez.container.size=10240
    SET hive.tez.java.opts=-Xmx8192m

Merhaba yeni ayarlarla hello sorgu altında 10 dakika içinde başarıyla çalıştırıldı.

## <a name="next-steps"></a>Sonraki adımlar

OOM hata alma mutlaka hello kapsayıcı boyutu çok küçük anlamına gelmez. Bunun yerine, böylece Hello yığın boyutu artar ve hello kapsayıcı bellek boyutu % 80'en az hello bellek ayarlarını yapılandırmanız gerekir. Hive sorguları iyileştirmek için bkz: [hdınsight'ta Hadoop için en iyi duruma getirme Hive sorguları](hdinsight-hadoop-optimize-hive-query.md).
