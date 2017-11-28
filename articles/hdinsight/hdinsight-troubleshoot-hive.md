---
title: "Azure Hdınsight kullanarak Hive aaaTroubleshoot | Microsoft Docs"
description: "Apache Hive ve Azure Hdınsight ile çalışma hakkında toocommon soruların yanıtlarını alın."
keywords: "Azure Hdınsight, Hive, SSS, sorun giderme kılavuzu, sık sorulan sorular"
services: Azure HDInsight
documentationcenter: na
author: dharmeshkakadia
manager: 
editor: 
ms.assetid: 15B8D0F3-F2D3-4746-BDCB-C72944AA9252
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: dharmeshkakadia
ms.openlocfilehash: ac459316e658d0b29eb66f5685f0bc7e693bb277
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-hive-by-using-azure-hdinsight"></a><span data-ttu-id="08154-104">Hive Azure Hdınsight kullanarak sorun giderme</span><span class="sxs-lookup"><span data-stu-id="08154-104">Troubleshoot Hive by using Azure HDInsight</span></span>

<span data-ttu-id="08154-105">Merhaba üst sorular ve bunların çözümleri hakkında Apache Ambari, Apache Hive yükü ile çalışırken öğrenin.</span><span class="sxs-lookup"><span data-stu-id="08154-105">Learn about hello top questions and their resolutions when working with Apache Hive payloads in Apache Ambari.</span></span>


## <a name="how-do-i-export-a-hive-metastore-and-import-it-on-another-cluster"></a><span data-ttu-id="08154-106">Nasıl bir Hive meta depo dışarı aktarma ve başka bir kümede alma</span><span class="sxs-lookup"><span data-stu-id="08154-106">How do I export a Hive metastore and import it on another cluster</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="08154-107">Çözüm adımları</span><span class="sxs-lookup"><span data-stu-id="08154-107">Resolution steps</span></span>

1. <span data-ttu-id="08154-108">Bir güvenli Kabuk (SSH) istemcisi kullanarak toohello Hdınsight kümesine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="08154-108">Connect toohello HDInsight cluster by using a Secure Shell (SSH) client.</span></span> <span data-ttu-id="08154-109">Daha fazla bilgi için bkz: [ek okuma](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="08154-109">For more information, see [Additional reading](#additional-reading-end).</span></span>

2. <span data-ttu-id="08154-110">Komut tooexport hello meta depo istediğiniz hello Hdınsight kümesinde aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="08154-110">Run hello following command on hello HDInsight cluster from which you want tooexport hello metastore:</span></span>

    ```apache
    for d in `hive -e "show databases"`; do echo "create database $d; use $d;" >> alltables.sql ; for t in `hive --database $d -e "show tables"` ; do ddl=`hive --database $d -e "show create table $t"`; echo "$ddl ;" >> alltables.sql ; echo "$ddl" | grep -q "PARTITIONED\s*BY" && echo "MSCK REPAIR TABLE $t ;" >> alltables.sql ; done; done
    ```

  <span data-ttu-id="08154-111">Bu komut, allatables.sql adlı bir dosya oluşturur.</span><span class="sxs-lookup"><span data-stu-id="08154-111">This command generates a file named allatables.sql.</span></span>

3. <span data-ttu-id="08154-112">Merhaba dosya alltables.sql toohello yeni Hdınsight kümesi kopyalayın ve ardından hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="08154-112">Copy hello file alltables.sql toohello new HDInsight cluster, and then run hello following command:</span></span>

  ```apache
  hive -f alltables.sql
  ```

<span data-ttu-id="08154-113">Merhaba çözüm adımları Hello kodda hello yeni kümede yollardır veri aynı hello veri yolları hello eski kümedeki olarak hello olduğunu varsayar.</span><span class="sxs-lookup"><span data-stu-id="08154-113">hello code in hello resolution steps assumes that data paths on hello new cluster are hello same as hello data paths on hello old cluster.</span></span> <span data-ttu-id="08154-114">Merhaba veri yolları farklıysa, değişiklikleri el ile oluşturulan hello alltables.sql dosya tooreflect düzenleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="08154-114">If hello data paths are different, you can manually edit hello generated alltables.sql file tooreflect any changes.</span></span>

### <a name="additional-reading"></a><span data-ttu-id="08154-115">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="08154-115">Additional reading</span></span>

- [<span data-ttu-id="08154-116">SSH kullanarak tooan Hdınsight kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="08154-116">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-locate-hive-logs-on-a-cluster"></a><span data-ttu-id="08154-117">Bir kümede nasıl Hive günlüklerini bulun</span><span class="sxs-lookup"><span data-stu-id="08154-117">How do I locate Hive logs on a cluster</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="08154-118">Çözüm adımları</span><span class="sxs-lookup"><span data-stu-id="08154-118">Resolution steps</span></span>

1. <span data-ttu-id="08154-119">SSH kullanarak toohello Hdınsight kümesine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="08154-119">Connect toohello HDInsight cluster by using SSH.</span></span> <span data-ttu-id="08154-120">Daha fazla bilgi için bkz: **ek okuma**.</span><span class="sxs-lookup"><span data-stu-id="08154-120">For more information, see **Additional reading**.</span></span>

2. <span data-ttu-id="08154-121">tooview Hive istemci günlükleri hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="08154-121">tooview Hive client logs, use hello following command:</span></span>

  ```apache
  /tmp/<username>/hive.log 
  ```

3. <span data-ttu-id="08154-122">tooview Hive meta depo günlükleri, komutu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="08154-122">tooview Hive metastore logs, use hello following command:</span></span>

  ```apache
  /var/log/hive/hivemetastore.log 
  ```

4. <span data-ttu-id="08154-123">tooview Hiveserver günlükleri, komutu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="08154-123">tooview Hiveserver logs, use hello following command:</span></span>

  ```apache
  /var/log/hive/hiveserver2.log 
  ```

### <a name="additional-reading"></a><span data-ttu-id="08154-124">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="08154-124">Additional reading</span></span>

- [<span data-ttu-id="08154-125">SSH kullanarak tooan Hdınsight kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="08154-125">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-launch-hello-hive-shell-with-specific-configurations-on-a-cluster"></a><span data-ttu-id="08154-126">Merhaba Hive kabuğunu bir kümede belirli yapılandırmalarla nasıl başlatma</span><span class="sxs-lookup"><span data-stu-id="08154-126">How do I launch hello Hive shell with specific configurations on a cluster</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="08154-127">Çözüm adımları</span><span class="sxs-lookup"><span data-stu-id="08154-127">Resolution steps</span></span>

1. <span data-ttu-id="08154-128">Merhaba Hive kabuğunu başlattığınızda yapılandırma anahtar-değer çifti belirtin.</span><span class="sxs-lookup"><span data-stu-id="08154-128">Specify a configuration key-value pair when you start hello Hive shell.</span></span> <span data-ttu-id="08154-129">Daha fazla bilgi için bkz: [ek okuma](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="08154-129">For more information, see [Additional reading](#additional-reading-end).</span></span>

  ```apache
  hive -hiveconf a=b 
  ```

2. <span data-ttu-id="08154-130">tüm etkin yapılandırmaları Hive kabuğunu, aşağıdaki kullanım hello üzerinde toolist komutu:</span><span class="sxs-lookup"><span data-stu-id="08154-130">toolist all effective configurations on Hive shell, use hello following command:</span></span>

  ```apache
  hive> set;
  ```

  <span data-ttu-id="08154-131">Örneğin, komut toostart Hive kabuğunu hello konsolda etkin hata ayıklama günlüğünü ile aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="08154-131">For example, use hello following command toostart Hive shell with debug logging enabled on hello console:</span></span>

  ```apache
  hive -hiveconf hive.root.logger=ALL,console 
  ```

### <a name="additional-reading"></a><span data-ttu-id="08154-132">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="08154-132">Additional reading</span></span>

- [<span data-ttu-id="08154-133">Hive yapılandırma özellikleri</span><span class="sxs-lookup"><span data-stu-id="08154-133">Hive configuration properties</span></span>](https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties)


## <span data-ttu-id="08154-134"><a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>Küme kritik yolunda Tez DAG verileri nasıl çözümlemek</span><span class="sxs-lookup"><span data-stu-id="08154-134"><a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>How do I analyze Tez DAG data on a cluster-critical path</span></span>


### <a name="resolution-steps"></a><span data-ttu-id="08154-135">Çözüm adımları</span><span class="sxs-lookup"><span data-stu-id="08154-135">Resolution steps</span></span>
 
1. <span data-ttu-id="08154-136">tooanalyze bir Apache Tez Çevrimsiz grafik (DAG) bir küme kritik grafikte yönlendirilmiş, SSH kullanarak toohello Hdınsight kümesine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="08154-136">tooanalyze an Apache Tez directed acyclic graph (DAG) on a cluster-critical graph, connect toohello HDInsight cluster by using SSH.</span></span> <span data-ttu-id="08154-137">Daha fazla bilgi için bkz: [ek okuma](#additional-reading-end).</span><span class="sxs-lookup"><span data-stu-id="08154-137">For more information, see [Additional reading](#additional-reading-end).</span></span>

2. <span data-ttu-id="08154-138">Bir komut isteminde hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="08154-138">At a command prompt, run hello following command:</span></span>
   
  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar CriticalPath --saveResults --dagId <DagId> --eventFileName <DagData.zip> 
  ```

3. <span data-ttu-id="08154-139">toolist kullanılan tooanalyze Tez DAG olabilecek diğer çözümleyiciler hello aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="08154-139">toolist other analyzers that can be used tooanalyze Tez DAG, use hello following command:</span></span>

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar
  ```

  <span data-ttu-id="08154-140">Merhaba ilk bağımsız değişkeni olarak bir örnek program sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="08154-140">You must provide an example program as hello first argument.</span></span>

  <span data-ttu-id="08154-141">Geçerli program adları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="08154-141">Valid program names include:</span></span>
    - <span data-ttu-id="08154-142">**ContainerReuseAnalyzer**: yazdırma bir kapsayıcı yeniden ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="08154-142">**ContainerReuseAnalyzer**: Print container reuse details in a DAG</span></span>
    - <span data-ttu-id="08154-143">**CriticalPath**: Bul hello kritik yol, bir dag'nin</span><span class="sxs-lookup"><span data-stu-id="08154-143">**CriticalPath**: Find hello critical path of a DAG</span></span>
    - <span data-ttu-id="08154-144">**LocalityAnalyzer**: yazdırma bir yere göre ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="08154-144">**LocalityAnalyzer**: Print locality details in a DAG</span></span>
    - <span data-ttu-id="08154-145">**ShuffleTimeAnalyzer**: hello karışık saati ayrıntıları bir çözümleme</span><span class="sxs-lookup"><span data-stu-id="08154-145">**ShuffleTimeAnalyzer**: Analyze hello shuffle time details in a DAG</span></span>
    - <span data-ttu-id="08154-146">**SkewAnalyzer**: hello eğme ayrıntıları bir çözümleme</span><span class="sxs-lookup"><span data-stu-id="08154-146">**SkewAnalyzer**: Analyze hello skew details in a DAG</span></span>
    - <span data-ttu-id="08154-147">**SlowNodeAnalyzer**: yazdırma bir düğüm ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="08154-147">**SlowNodeAnalyzer**: Print node details in a DAG</span></span>
    - <span data-ttu-id="08154-148">**SlowTaskIdentifier**: bir yazdırma yavaş görev ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="08154-148">**SlowTaskIdentifier**: Print slow task details in a DAG</span></span>
    - <span data-ttu-id="08154-149">**SlowestVertexAnalyzer**: yazdırma bir yavaş köşe ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="08154-149">**SlowestVertexAnalyzer**: Print slowest vertex details in a DAG</span></span>
    - <span data-ttu-id="08154-150">**SpillAnalyzer**: bir Karmadaki ayrıntılarını yazdırma</span><span class="sxs-lookup"><span data-stu-id="08154-150">**SpillAnalyzer**: Print spill details in a DAG</span></span>
    - <span data-ttu-id="08154-151">**TaskConcurrencyAnalyzer**: hello görev eşzamanlılık ayrıntıları bir yazdırma</span><span class="sxs-lookup"><span data-stu-id="08154-151">**TaskConcurrencyAnalyzer**: Print hello task concurrency details in a DAG</span></span>
    - <span data-ttu-id="08154-152">**VertexLevelCriticalPathAnalyzer**: köşe düzeyinde bir hello kritik yol Bul</span><span class="sxs-lookup"><span data-stu-id="08154-152">**VertexLevelCriticalPathAnalyzer**: Find hello critical path at vertex level in a DAG</span></span>


### <a name="additional-reading"></a><span data-ttu-id="08154-153">Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="08154-153">Additional reading</span></span>

- [<span data-ttu-id="08154-154">SSH kullanarak tooan Hdınsight kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="08154-154">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-download-tez-dag-data-from-a-cluster"></a><span data-ttu-id="08154-155">Bir kümeden nasıl Tez DAG veri karşıdan</span><span class="sxs-lookup"><span data-stu-id="08154-155">How do I download Tez DAG data from a cluster</span></span>


#### <a name="resolution-steps"></a><span data-ttu-id="08154-156">Çözüm adımları</span><span class="sxs-lookup"><span data-stu-id="08154-156">Resolution steps</span></span>

<span data-ttu-id="08154-157">Toocollect hello Tez DAG veri iki yolu vardır:</span><span class="sxs-lookup"><span data-stu-id="08154-157">There are two ways toocollect hello Tez DAG data:</span></span>

- <span data-ttu-id="08154-158">Merhaba komut satırından:</span><span class="sxs-lookup"><span data-stu-id="08154-158">From hello command line:</span></span>
 
    <span data-ttu-id="08154-159">SSH kullanarak toohello Hdınsight kümesine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="08154-159">Connect toohello HDInsight cluster by using SSH.</span></span> <span data-ttu-id="08154-160">Hello komut isteminde hello aşağıdaki komutu çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="08154-160">At hello command prompt, run hello following command:</span></span>

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-history-parser-*.jar org.apache.tez.history.ATSImportTool -downloadDir . -dagId <DagId> 
  ```

- <span data-ttu-id="08154-161">Merhaba Ambari Tez görünümünü kullanın:</span><span class="sxs-lookup"><span data-stu-id="08154-161">Use hello Ambari Tez view:</span></span>
   
  1. <span data-ttu-id="08154-162">TooAmbari gidin.</span><span class="sxs-lookup"><span data-stu-id="08154-162">Go tooAmbari.</span></span> 
  2. <span data-ttu-id="08154-163">Git tooTez Görünüm (altında hello sağ üst köşesinde hello döşeme simgedir).</span><span class="sxs-lookup"><span data-stu-id="08154-163">Go tooTez view (under hello tiles icon in hello upper-right corner).</span></span> 
  3. <span data-ttu-id="08154-164">Merhaba tooview istediğiniz DAG seçin.</span><span class="sxs-lookup"><span data-stu-id="08154-164">Select hello DAG you want tooview.</span></span>
  4. <span data-ttu-id="08154-165">Seçin **karşıdan veri**.</span><span class="sxs-lookup"><span data-stu-id="08154-165">Select **Download data**.</span></span>

### <span data-ttu-id="08154-166"><a name="additional-reading-end"></a>Ek kaynaklar</span><span class="sxs-lookup"><span data-stu-id="08154-166"><a name="additional-reading-end"></a>Additional reading</span></span>

[<span data-ttu-id="08154-167">SSH kullanarak tooan Hdınsight kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="08154-167">Connect tooan HDInsight cluster by using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)






