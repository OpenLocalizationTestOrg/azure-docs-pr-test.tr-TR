---
title: "aaaOptimize Hive sorguları Azure Hdınsight'ta | Microsoft Docs"
description: "Nasıl toooptimize için hdınsight'ta Hadoop, Hive sorguları hakkında bilgi edinin."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d6174c08-06aa-42ac-8e9b-8b8718d9978e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/26/2016
ms.author: jgao
ms.openlocfilehash: d27f8100e1e9f4823040ff9f693e7b78d6192c6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-hive-queries-in-azure-hdinsight"></a><span data-ttu-id="fef56-103">Azure hdınsight'ta Hive sorguları en iyi duruma getirme</span><span class="sxs-lookup"><span data-stu-id="fef56-103">Optimize Hive queries in Azure HDInsight</span></span>

<span data-ttu-id="fef56-104">Varsayılan olarak, Hadoop kümeleri için performansı optimize edilmemiş.</span><span class="sxs-lookup"><span data-stu-id="fef56-104">By default, Hadoop clusters are not optimized for performance.</span></span> <span data-ttu-id="fef56-105">Bu makalede tooyour sorguları uygulayabilirsiniz bazı yaygın Hive performansı en iyi duruma getirme yöntemleri kapsar.</span><span class="sxs-lookup"><span data-stu-id="fef56-105">This article covers some most common Hive performance optimization methods that you can apply tooyour queries.</span></span>

## <a name="scale-out-worker-nodes"></a><span data-ttu-id="fef56-106">Çalışan düğümü ölçeklendirme</span><span class="sxs-lookup"><span data-stu-id="fef56-106">Scale out worker nodes</span></span>

<span data-ttu-id="fef56-107">Kümedeki çalışan düğümü Hello sayısını artırmayı paralel olarak çalışan daha fazla mappers ve reducers toobe yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fef56-107">Increasing hello number of worker nodes in a cluster can leverage more mappers and reducers toobe run in parallel.</span></span> <span data-ttu-id="fef56-108">Hdınsight'ta ölçek genişletme artırabilirsiniz iki yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="fef56-108">There are two ways you can increase scale out in HDInsight:</span></span>

* <span data-ttu-id="fef56-109">Merhaba sağlama sırasında hello hello Azure portal, Azure PowerShell veya platformlar arası komut satırı arabirimi kullanarak çalışan düğümü sayısını belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fef56-109">At hello provision time, you can specify hello number of worker nodes using hello Azure portal, Azure PowerShell, or Cross-platform command-line interface.</span></span>  <span data-ttu-id="fef56-110">Daha fazla bilgi için bkz. [HDInsight kümesi oluşturma](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="fef56-110">For more information, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="fef56-111">Merhaba aşağıdaki ekran görüntüsü hello alt düğüm yapılandırması hello Azure portalı üzerinde gösterir:</span><span class="sxs-lookup"><span data-stu-id="fef56-111">hello following screenshot shows hello worker node configuration on hello Azure portal:</span></span>
  
    ![scaleout_1][image-hdi-optimize-hive-scaleout_1]
* <span data-ttu-id="fef56-113">Çalışma zamanı hello sırasında bir yeniden oluşturmadan ayrıca bir küme ölçeklendirebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fef56-113">At hello run time, you can also scale out a cluster without recreating one:</span></span>

    ![scaleout_1][image-hdi-optimize-hive-scaleout_2]

<span data-ttu-id="fef56-115">Merhaba farklı sanal makinelerin Hdınsight tarafından desteklenen hakkında daha fazla bilgi için bkz: [Hdınsight fiyatlandırma](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="fef56-115">For more information about hello different virtual machines supported by HDInsight, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="enable-tez"></a><span data-ttu-id="fef56-116">Tez etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="fef56-116">Enable Tez</span></span>

<span data-ttu-id="fef56-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) bir alternatif yürütme altyapısı toohello MapReduce altyapısıdır:</span><span class="sxs-lookup"><span data-stu-id="fef56-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) is an alternative execution engine toohello MapReduce engine:</span></span>

![tez_1][image-hdi-optimize-hive-tez_1]

<span data-ttu-id="fef56-119">Tez daha hızlı nedeni:</span><span class="sxs-lookup"><span data-stu-id="fef56-119">Tez is faster because:</span></span>

* <span data-ttu-id="fef56-120">**Yönlendirilmiş Çevrimsiz grafik (DAG) hello MapReduce Altyapısı'ndaki tek bir iş olarak çalıştırmak**.</span><span class="sxs-lookup"><span data-stu-id="fef56-120">**Execute Directed Acyclic Graph (DAG) as a single job in hello MapReduce engine**.</span></span> <span data-ttu-id="fef56-121">Merhaba DAG mappers toobe reducers bir kümesi tarafından izlenen her kümesi gerektirir.</span><span class="sxs-lookup"><span data-stu-id="fef56-121">hello DAG requires each set of mappers toobe followed by one set of reducers.</span></span> <span data-ttu-id="fef56-122">Bu, her bir Hive sorgusu için başlar birden çok MapReduce işleri toobe neden olur.</span><span class="sxs-lookup"><span data-stu-id="fef56-122">This causes multiple MapReduce jobs toobe spun off for each Hive query.</span></span> <span data-ttu-id="fef56-123">Tez böyle kısıtlaması yok ve karmaşık DAG böylece iş başlangıç yükünü en aza bir iş olarak işleyebilir.</span><span class="sxs-lookup"><span data-stu-id="fef56-123">Tez does not have such constraint and can process complex DAG as one job thus minimizing job startup overhead.</span></span>
* <span data-ttu-id="fef56-124">**Gereksiz yazma önler**.</span><span class="sxs-lookup"><span data-stu-id="fef56-124">**Avoids unnecessary writes**.</span></span> <span data-ttu-id="fef56-125">Merhaba başlar toomultiple işleri nedeniyle hello MapReduce altyapısındaki her hello çıktısını aynı Hive sorgusu tooHDFS Ara verilerin yazılır.</span><span class="sxs-lookup"><span data-stu-id="fef56-125">Due toomultiple jobs being spun for hello same Hive query in hello MapReduce engine, hello output of each job is written tooHDFS for intermediate data.</span></span> <span data-ttu-id="fef56-126">Tez her Hive sorgusu için iş sayısını en aza indirir olduğundan mümkün tooavoid gereksiz yazma kalır.</span><span class="sxs-lookup"><span data-stu-id="fef56-126">Since Tez minimizes number of jobs for each Hive query it is able tooavoid unnecessary write.</span></span>
* <span data-ttu-id="fef56-127">**Başlangıç gecikmeleri en aza indirir**.</span><span class="sxs-lookup"><span data-stu-id="fef56-127">**Minimizes start-up delays**.</span></span> <span data-ttu-id="fef56-128">Tez toostart ve ayrıca iyileştirme iyileştirme boyunca gereken mappers hello sayısını azaltarak daha iyi mümkün toominimize başlangıç gecikme olur.</span><span class="sxs-lookup"><span data-stu-id="fef56-128">Tez is better able toominimize start-up delay by reducing hello number of mappers it needs toostart and also improving optimization throughout.</span></span>
* <span data-ttu-id="fef56-129">**Kapsayıcıları yeniden kullanır**.</span><span class="sxs-lookup"><span data-stu-id="fef56-129">**Reuses containers**.</span></span> <span data-ttu-id="fef56-130">Olası Tez bu gecikme nedeniyle mümkün tooreuse kapsayıcıları tooensure olduğunda toostarting kapsayıcıları yukarı azalır.</span><span class="sxs-lookup"><span data-stu-id="fef56-130">Whenever possible Tez is able tooreuse containers tooensure that latency due toostarting up containers is reduced.</span></span>
* <span data-ttu-id="fef56-131">**Sürekli iyileştirme tekniklerini**.</span><span class="sxs-lookup"><span data-stu-id="fef56-131">**Continuous optimization techniques**.</span></span> <span data-ttu-id="fef56-132">En iyi duruma getirme derleme aşamasında geleneksel olarak gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="fef56-132">Traditionally optimization was done during compilation phase.</span></span> <span data-ttu-id="fef56-133">Merhaba girişleri hakkında daha fazla bilgi kullanılabilir ancak, çalışma zamanı sırasında daha iyi iyileştirme izin verir.</span><span class="sxs-lookup"><span data-stu-id="fef56-133">However more information about hello inputs is available that allow for better optimization during runtime.</span></span> <span data-ttu-id="fef56-134">Tez hello çalışma zamanı aşaması toooptimize hello daha fazla plan verir sürekli iyileştirme teknikleri kullanır.</span><span class="sxs-lookup"><span data-stu-id="fef56-134">Tez uses continuous optimization techniques that allows it toooptimize hello plan further into hello runtime phase.</span></span>

<span data-ttu-id="fef56-135">Bu kavramlarla ilgili daha fazla ayrıntı için bkz: [Apache TEZ](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="fef56-135">For more details on these concepts, see [Apache TEZ](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="fef56-136">Herhangi bir Hive sorgu hello ayarıyla aşağıdaki hello sorgu ekleyerek etkin Tez yapabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="fef56-136">You can make any Hive query Tez enabled by prefixing hello query with hello setting below:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="fef56-137">Linux tabanlı Hdınsight kümeleri varsayılan olarak etkin Tez sahip.</span><span class="sxs-lookup"><span data-stu-id="fef56-137">Linux-based HDInsight clusters have Tez enabled by default.</span></span>


## <a name="hive-partitioning"></a><span data-ttu-id="fef56-138">Bölümleme yığını</span><span class="sxs-lookup"><span data-stu-id="fef56-138">Hive partitioning</span></span>

<span data-ttu-id="fef56-139">G/ç, Hive sorguları çalıştırmak için hello önemli performans düşüklüğü işlemdir.</span><span class="sxs-lookup"><span data-stu-id="fef56-139">I/O operation is hello major performance bottleneck for running Hive queries.</span></span> <span data-ttu-id="fef56-140">Merhaba performans geliştirilmiş hello toobe gereken veri miktarı olabilir okuyorsanız azalır.</span><span class="sxs-lookup"><span data-stu-id="fef56-140">hello performance can be improved if hello amount of data that needs toobe read can be reduced.</span></span> <span data-ttu-id="fef56-141">Varsayılan olarak, tüm Hive tabloları Hive sorguları tarayın.</span><span class="sxs-lookup"><span data-stu-id="fef56-141">By default, Hive queries scan entire Hive tables.</span></span> <span data-ttu-id="fef56-142">Tablo tarama gibi sorgular için harika bir seçenek budur.</span><span class="sxs-lookup"><span data-stu-id="fef56-142">This is great for queries like table scans.</span></span> <span data-ttu-id="fef56-143">Ancak yalnızca tooscan çok küçük miktarda veri filtreleme ile (sorgular) Örneğin, gereken sorgular için bu davranış yükü gereksiz oluşturur.</span><span class="sxs-lookup"><span data-stu-id="fef56-143">However for queries that only need tooscan a small amount of data (for example, queries with filtering), this behavior creates unnecessary overhead.</span></span> <span data-ttu-id="fef56-144">Hive bölümleme Hive tabloları Hive sorguları tooaccess yalnızca hello gerekli veri miktarını sağlar.</span><span class="sxs-lookup"><span data-stu-id="fef56-144">Hive partitioning allows Hive queries tooaccess only hello necessary amount of data in Hive tables.</span></span>

<span data-ttu-id="fef56-145">Hive bölümleme hello ham verileri yeni dizinlere hello bölüm hello kullanıcı tarafından tanımlandığı kendi dizini - sahip her bir bölümü ile yeniden düzenleme tarafından uygulanır.</span><span class="sxs-lookup"><span data-stu-id="fef56-145">Hive partitioning is implemented by reorganizing hello raw data into new directories with each partition having its own directory - where hello partition is defined by hello user.</span></span> <span data-ttu-id="fef56-146">Merhaba Aşağıdaki diyagramda bir Hive tablosu hello sütuna göre bölümleme gösterilmektedir *yıl*.</span><span class="sxs-lookup"><span data-stu-id="fef56-146">hello following diagram illustrates partitioning a Hive table by hello column *Year*.</span></span> <span data-ttu-id="fef56-147">Her yıl için yeni bir dizin oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="fef56-147">A new directory is created for each year.</span></span>

![Bölümlendirme][image-hdi-optimize-hive-partitioning_1]

<span data-ttu-id="fef56-149">Bölümleme bazı noktalar:</span><span class="sxs-lookup"><span data-stu-id="fef56-149">Some partitioning considerations:</span></span>

* <span data-ttu-id="fef56-150">**Bölüm altında yapmak** -yalnızca birkaç değerlerine sahip sütunlarda bölümleme birkaç bölümleri neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="fef56-150">**Do not under partition** - Partitioning on columns with only a few values can cause few partitions.</span></span> <span data-ttu-id="fef56-151">Örneğin, cinsiyetiniz üzerinde bölümleme yalnızca (Erkek ve Kadın) oluşturulan iki bölüm toobe oluşturur, böylece yalnızca hello maksimum yarısı tarafından gecikmesini.</span><span class="sxs-lookup"><span data-stu-id="fef56-151">For example, partitioning on gender only creates two partitions toobe created (male and female), thus only reduce hello latency by a maximum of half.</span></span>
* <span data-ttu-id="fef56-152">**Değil bölüm yapmak** - Sihirbazın diğer uç Merhaba, benzersiz bir değer (örneğin, USERID) bir sütun üzerinde bölüm oluşturma birden çok bölüm neden olur.</span><span class="sxs-lookup"><span data-stu-id="fef56-152">**Do not over partition** - On hello other extreme, creating a partition on a column with a unique value (for example, userid) causes multiple partitions.</span></span> <span data-ttu-id="fef56-153">Toohandle hello çok sayıda dizinleri taşıdığından bölüm kadar stres hello küme iş üzerinde neden olur.</span><span class="sxs-lookup"><span data-stu-id="fef56-153">Over partition causes much stress on hello cluster namenode as it has toohandle hello large number of directories.</span></span>
* <span data-ttu-id="fef56-154">**Veri eğme kaçının** -bile boyutu tüm bölümleri; böylece bölümleme anahtarınızı dikkatle seçin.</span><span class="sxs-lookup"><span data-stu-id="fef56-154">**Avoid data skew** - Choose your partitioning key wisely so that all partitions are even size.</span></span> <span data-ttu-id="fef56-155">Örneği üzerinde bölümleme *durumu* kayıtları California toobe altında hello sayısı yaklaşık 30 neden olabilir, Vermont toohello fark popülasyondaki son x.</span><span class="sxs-lookup"><span data-stu-id="fef56-155">An example is partitioning on *State* may cause hello number of records under California toobe almost 30x that of Vermont due toohello difference in population.</span></span>

<span data-ttu-id="fef56-156">toocreate bir bölüm tablosu kullanmak hello *bölümlenmiş tarafından* yan tümcesi:</span><span class="sxs-lookup"><span data-stu-id="fef56-156">toocreate a partition table, use hello *Partitioned By* clause:</span></span>

    CREATE TABLE lineitem_part
        (L_ORDERKEY INT, L_PARTKEY INT, L_SUPPKEY INT,L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE            STRING, L_SHIPINSTRUCT STRING, L_SHIPMODE STRING,
         L_COMMENT STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    STORED AS TEXTFILE;

<span data-ttu-id="fef56-157">Merhaba bölümlenmiş tablo oluşturulduktan sonra statik bölümleme veya dinamik bölümleme ya da oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fef56-157">Once hello partitioned table is created, you can either create static partitioning or dynamic partitioning.</span></span>

* <span data-ttu-id="fef56-158">**Statik bölümleme** hello zaten parçalı veriler sahip anlamına gelir uygun dizinleri ve el ile Merhaba dizin konumuna göre Hive bölümleri sorabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fef56-158">**Static partitioning** means that you have already sharded data in hello appropriate directories and you can ask Hive partitions manually based on hello directory location.</span></span> <span data-ttu-id="fef56-159">Aşağıdaki kod parçacığını hello bir örnektir.</span><span class="sxs-lookup"><span data-stu-id="fef56-159">hello following code snippet is an example.</span></span>
  
        INSERT OVERWRITE TABLE lineitem_part
        PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’)
        SELECT * FROM lineitem 
        WHERE lineitem.L_SHIPDATE = ‘5/23/1996 12:00:00 AM’
  
        ALTER TABLE lineitem_part ADD PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’))
        LOCATION ‘wasb://sampledata@ignitedemo.blob.core.windows.net/partitions/5_23_1996/'
* <span data-ttu-id="fef56-160">**Dinamik bölümleme** , Hive toocreate bölümleri otomatik olarak sizin için istediğiniz anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="fef56-160">**Dynamic partitioning** means that you want Hive toocreate partitions automatically for you.</span></span> <span data-ttu-id="fef56-161">Hazırlama tablosuna hello tablosundan bölümleme hello zaten oluşturduk olduğundan, tüm toodo ihtiyacımız olan veri bölümlenmiş toohello Tablosu Ekle:</span><span class="sxs-lookup"><span data-stu-id="fef56-161">Since we have already created hello partitioning table from hello staging table, all we need toodo is insert data toohello partitioned table:</span></span>
  
        SET hive.exec.dynamic.partition = true;
        SET hive.exec.dynamic.partition.mode = nonstrict;
        INSERT INTO TABLE lineitem_part
        PARTITION (L_SHIPDATE)
        SELECT L_ORDERKEY as L_ORDERKEY, L_PARTKEY as L_PARTKEY , 
             L_SUPPKEY as L_SUPPKEY, L_LINENUMBER as L_LINENUMBER,
              L_QUANTITY as L_QUANTITY, L_EXTENDEDPRICE as L_EXTENDEDPRICE,
             L_DISCOUNT as L_DISCOUNT, L_TAX as L_TAX, L_RETURNFLAG as           L_RETURNFLAG, L_LINESTATUS as L_LINESTATUS, L_SHIPDATE as           L_SHIPDATE_PS, L_COMMITDATE as L_COMMITDATE, L_RECEIPTDATE as      L_RECEIPTDATE, L_SHIPINSTRUCT as L_SHIPINSTRUCT, L_SHIPMODE as      L_SHIPMODE, L_COMMENT as L_COMMENT, L_SHIPDATE as L_SHIPDATE FROM lineitem;

<span data-ttu-id="fef56-162">Daha fazla ayrıntı için bkz: [bölümlenmiş tabloları](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span><span class="sxs-lookup"><span data-stu-id="fef56-162">For more details, see [Partitioned Tables](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span></span>

## <a name="use-hello-orcfile-format"></a><span data-ttu-id="fef56-163">Merhaba ORCFile biçimini kullanın</span><span class="sxs-lookup"><span data-stu-id="fef56-163">Use hello ORCFile format</span></span>
<span data-ttu-id="fef56-164">Hive farklı dosya biçimleri destekler.</span><span class="sxs-lookup"><span data-stu-id="fef56-164">Hive supports different file formats.</span></span> <span data-ttu-id="fef56-165">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="fef56-165">For example:</span></span>

* <span data-ttu-id="fef56-166">**Metin**: Bu hello varsayılan dosya biçimidir ve çoğu senaryoları ile çalışır</span><span class="sxs-lookup"><span data-stu-id="fef56-166">**Text**: this is hello default file format and works with most scenarios</span></span>
* <span data-ttu-id="fef56-167">**Avro**: birlikte çalışabilirlik senaryoları için iyi çalışır</span><span class="sxs-lookup"><span data-stu-id="fef56-167">**Avro**: works well for interoperability scenarios</span></span>
* <span data-ttu-id="fef56-168">**ORC/Parquet**: performans için uygundur</span><span class="sxs-lookup"><span data-stu-id="fef56-168">**ORC/Parquet**: best suited for performance</span></span>

<span data-ttu-id="fef56-169">ORC (en iyi duruma getirilmiş satır sütunlu), son derece verimli şekilde toostore Hive veri biçimidir.</span><span class="sxs-lookup"><span data-stu-id="fef56-169">ORC (Optimized Row Columnar) format is a highly efficient way toostore Hive data.</span></span> <span data-ttu-id="fef56-170">Karşılaştırılan tooother biçimleri, ORC hello aşağıdaki avantajları vardır:</span><span class="sxs-lookup"><span data-stu-id="fef56-170">Compared tooother formats, ORC has hello following advantages:</span></span>

* <span data-ttu-id="fef56-171">DateTime ve karmaşık ve yarı yapılandırılmış türleri gibi karmaşık türleri için destek</span><span class="sxs-lookup"><span data-stu-id="fef56-171">support for complex types including DateTime and complex and semi-structured types</span></span>
* <span data-ttu-id="fef56-172">too70% sıkıştırmayı ayarlama</span><span class="sxs-lookup"><span data-stu-id="fef56-172">up too70% compression</span></span>
* <span data-ttu-id="fef56-173">Satır atlanıyor izin her 10.000 satırları dizinler</span><span class="sxs-lookup"><span data-stu-id="fef56-173">indexes every 10,000 rows, which allow skipping rows</span></span>
* <span data-ttu-id="fef56-174">önemli bir düşüş, çalışma zamanı yürütme</span><span class="sxs-lookup"><span data-stu-id="fef56-174">a significant drop in run-time execution</span></span>

<span data-ttu-id="fef56-175">tooenable ORC biçimi, önce oluşturduğunuz bir tablo hello yan tümcesiyle birlikte *ORC depolanan*:</span><span class="sxs-lookup"><span data-stu-id="fef56-175">tooenable ORC format, you first create a table with hello clause *Stored as ORC*:</span></span>

    CREATE TABLE lineitem_orc_part
        (L_ORDERKEY INT, L_PARTKEY INT,L_SUPPKEY INT, L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE STRING,
         L_SHIPINSTRUCT STRING, L_SHIPMODE STRING, L_COMMENT      STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    STORED AS ORC;

<span data-ttu-id="fef56-176">Ardından, tablo hazırlama hello veri toohello ORC tablo ekleyin.</span><span class="sxs-lookup"><span data-stu-id="fef56-176">Next, you insert data toohello ORC table from hello staging table.</span></span> <span data-ttu-id="fef56-177">Örneğin:</span><span class="sxs-lookup"><span data-stu-id="fef56-177">For example:</span></span>

    INSERT INTO TABLE lineitem_orc
    SELECT L_ORDERKEY as L_ORDERKEY, 
           L_PARTKEY as L_PARTKEY , 
           L_SUPPKEY as L_SUPPKEY,
           L_LINENUMBER as L_LINENUMBER,
            L_QUANTITY as L_QUANTITY, 
           L_EXTENDEDPRICE as L_EXTENDEDPRICE,
           L_DISCOUNT as L_DISCOUNT,
           L_TAX as L_TAX,
           L_RETURNFLAG as L_RETURNFLAG,
           L_LINESTATUS as L_LINESTATUS,
           L_SHIPDATE as L_SHIPDATE,
           L_COMMITDATE as L_COMMITDATE,
           L_RECEIPTDATE as L_RECEIPTDATE, 
           L_SHIPINSTRUCT as L_SHIPINSTRUCT,
           L_SHIPMODE as L_SHIPMODE,
           L_COMMENT as L_COMMENT
    FROM lineitem;

<span data-ttu-id="fef56-178">Daha fazla bilgiyi hello ORC biçimi [burada](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span><span class="sxs-lookup"><span data-stu-id="fef56-178">You can read more on hello ORC format [here](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span></span>

## <a name="vectorization"></a><span data-ttu-id="fef56-179">Vectorization</span><span class="sxs-lookup"><span data-stu-id="fef56-179">Vectorization</span></span>

<span data-ttu-id="fef56-180">Vectorization Hive sağlayan bir defada bir satır işleme yerine 1024 toplu birlikte satırları tooprocess.</span><span class="sxs-lookup"><span data-stu-id="fef56-180">Vectorization allows Hive tooprocess a batch of 1024 rows together instead of processing one row at a time.</span></span> <span data-ttu-id="fef56-181">Bu, daha az iç kod toorun gerektiğinden basit işlemleri daha hızlı yapılır anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="fef56-181">It means that simple operations are done faster because less internal code needs toorun.</span></span>

<span data-ttu-id="fef56-182">tooenable vectorization ayarı aşağıdaki hello ile Hive sorgunuzu öneki:</span><span class="sxs-lookup"><span data-stu-id="fef56-182">tooenable vectorization prefix your Hive query with hello following setting:</span></span>

    set hive.vectorized.execution.enabled = true;

<span data-ttu-id="fef56-183">Daha fazla bilgi için bkz: [sorgu yürütme Vectorized](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span><span class="sxs-lookup"><span data-stu-id="fef56-183">For more information, see [Vectorized query execution](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span></span>

## <a name="other-optimization-methods"></a><span data-ttu-id="fef56-184">Diğer en iyi duruma getirme yöntemleri</span><span class="sxs-lookup"><span data-stu-id="fef56-184">Other optimization methods</span></span>
<span data-ttu-id="fef56-185">Örneğin düşünebileceğiniz daha fazla en iyi duruma getirme yöntemi vardır:</span><span class="sxs-lookup"><span data-stu-id="fef56-185">There are more optimization methods that you can consider, for example:</span></span>

* <span data-ttu-id="fef56-186">**Bucketing hive:** toocluster veya segment veri toooptimize sorgu performansını büyük kümeleri olanak sağlayan bir yöntem.</span><span class="sxs-lookup"><span data-stu-id="fef56-186">**Hive bucketing:** a technique that allows toocluster or segment large sets of data toooptimize query performance.</span></span>
* <span data-ttu-id="fef56-187">**En iyi duruma getirme katılma:** tooimprove planlama Hive'nın sorgu yürütme en iyi duruma getirilmesi hello birleştirmeler verimliliğini ve kullanıcı ipuçları hello gereksinimini azaltır.</span><span class="sxs-lookup"><span data-stu-id="fef56-187">**Join optimization:** optimization of Hive's query execution planning tooimprove hello efficiency of joins and reduce hello need for user hints.</span></span> <span data-ttu-id="fef56-188">Daha fazla bilgi için bkz: [katılma en iyi duruma getirme](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span><span class="sxs-lookup"><span data-stu-id="fef56-188">For more information, see [Join optimization](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span></span>
* <span data-ttu-id="fef56-189">**Reducers artırmak**.</span><span class="sxs-lookup"><span data-stu-id="fef56-189">**Increase Reducers**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fef56-190">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="fef56-190">Next steps</span></span>
<span data-ttu-id="fef56-191">Bu makalede, birçok yaygın Hive sorgusu en iyi duruma getirme yöntemleri öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="fef56-191">In this article, you have learned several common Hive query optimization methods.</span></span> <span data-ttu-id="fef56-192">toolearn daha makaleler hello bakın:</span><span class="sxs-lookup"><span data-stu-id="fef56-192">toolearn more, see hello following articles:</span></span>

* [<span data-ttu-id="fef56-193">Hdınsight'ta Apache Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="fef56-193">Use Apache Hive in HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="fef56-194">Hdınsight'ta Hive kullanarak uçuş gecikme verilerini çözümleme</span><span class="sxs-lookup"><span data-stu-id="fef56-194">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="fef56-195">Twitter verilerini hdınsight'ta Hive kullanma çözümleme</span><span class="sxs-lookup"><span data-stu-id="fef56-195">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* [<span data-ttu-id="fef56-196">Hdınsight'ta Hadoop Hive sorgusu konsol Hello kullanarak algılayıcı verilerini çözümleme</span><span class="sxs-lookup"><span data-stu-id="fef56-196">Analyze sensor data using hello Hive Query Console on Hadoop in HDInsight</span></span>](hdinsight-hive-analyze-sensor-data.md)
* [<span data-ttu-id="fef56-197">Web siteleri tooanalyze günlüklerinden Hdınsight ile Hive kullanma</span><span class="sxs-lookup"><span data-stu-id="fef56-197">Use Hive with HDInsight tooanalyze logs from websites</span></span>](hdinsight-hive-analyze-website-log.md)

[image-hdi-optimize-hive-scaleout_1]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_1.png
[image-hdi-optimize-hive-scaleout_2]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_2.png
[image-hdi-optimize-hive-tez_1]: ./media/hdinsight-hadoop-optimize-hive-query/tez_1.png
[image-hdi-optimize-hive-partitioning_1]: ./media/hdinsight-hadoop-optimize-hive-query/partitioning_1.png
