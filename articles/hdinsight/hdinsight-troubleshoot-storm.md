---
title: "Azure Hdınsight kullanarak Storm aaaTroubleshoot | Microsoft Docs"
description: "Apache Storm Azure Hdınsight ile kullanma hakkında toocommon soruların yanıtlarını alın."
keywords: "Sorun giderme kılavuzu, ortak sorunları azure Hdınsight, Storm, SSS"
services: Azure HDInsight
documentationcenter: na
author: raviperi
manager: 
editor: 
ms.assetid: 74E51183-3EF4-4C67-AA60-6E12FAC999B5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: raviperi
ms.openlocfilehash: 51bcb3dc28eff5ee7bb33252fb2ec71a88ed8e09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-storm-by-using-azure-hdinsight"></a><span data-ttu-id="9c0e0-104">Storm Azure Hdınsight kullanarak sorun giderme</span><span class="sxs-lookup"><span data-stu-id="9c0e0-104">Troubleshoot Storm by using Azure HDInsight</span></span>

<span data-ttu-id="9c0e0-105">Merhaba üst sorunları ve bunların çözümleri için Apache Ambari, Apache Storm yükü ile çalışma hakkında bilgi edinin.</span><span class="sxs-lookup"><span data-stu-id="9c0e0-105">Learn about hello top issues and their resolutions for working with Apache Storm payloads in Apache Ambari.</span></span>

## <a name="how-do-i-access-hello-storm-ui-on-a-cluster"></a><span data-ttu-id="9c0e0-106">Bir küme üzerindeki Storm kullanıcı Arabirimi hello nasıl erişirim</span><span class="sxs-lookup"><span data-stu-id="9c0e0-106">How do I access hello Storm UI on a cluster</span></span>
<span data-ttu-id="9c0e0-107">Merhaba Storm kullanıcı Arabirimi bir tarayıcıdan erişirken için iki seçeneğiniz vardır:</span><span class="sxs-lookup"><span data-stu-id="9c0e0-107">You have two options for accessing hello Storm UI from a browser:</span></span>

### <a name="ambari-ui"></a><span data-ttu-id="9c0e0-108">Ambari kullanıcı Arabirimi</span><span class="sxs-lookup"><span data-stu-id="9c0e0-108">Ambari UI</span></span>
1. <span data-ttu-id="9c0e0-109">Toohello ambarı Pano gidin.</span><span class="sxs-lookup"><span data-stu-id="9c0e0-109">Go toohello Ambari dashboard.</span></span>
2. <span data-ttu-id="9c0e0-110">Hizmetleri Hello listesinde seçin **Storm**.</span><span class="sxs-lookup"><span data-stu-id="9c0e0-110">In hello list of services, select **Storm**.</span></span>
3. <span data-ttu-id="9c0e0-111">Merhaba, **hızlı bağlantılar** menüsünde, select **Storm kullanıcı Arabirimi**.</span><span class="sxs-lookup"><span data-stu-id="9c0e0-111">In hello **Quick Links** menu, select **Storm UI**.</span></span>

### <a name="direct-link"></a><span data-ttu-id="9c0e0-112">Doğrudan bağlantı</span><span class="sxs-lookup"><span data-stu-id="9c0e0-112">Direct link</span></span>
<span data-ttu-id="9c0e0-113">URL aşağıdaki hello adresindeki hello Storm kullanıcı Arabirimi erişebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="9c0e0-113">You can access hello Storm UI at hello following URL:</span></span>

<span data-ttu-id="9c0e0-114">https://\<küme DNS adına\>/stormui</span><span class="sxs-lookup"><span data-stu-id="9c0e0-114">https://\<cluster DNS name\>/stormui</span></span>

<span data-ttu-id="9c0e0-115">Örnek:</span><span class="sxs-lookup"><span data-stu-id="9c0e0-115">Example:</span></span>

 <span data-ttu-id="9c0e0-116">https://stormcluster.azurehdinsight.NET/stormui</span><span class="sxs-lookup"><span data-stu-id="9c0e0-116">https://stormcluster.azurehdinsight.net/stormui</span></span>

## <a name="how-do-i-transfer-storm-event-hub-spout-checkpoint-information-from-one-topology-tooanother"></a><span data-ttu-id="9c0e0-117">Bir topoloji tooanother nasıl Storm olay hub'ı spout denetim noktası bilgilerini Aktarım</span><span class="sxs-lookup"><span data-stu-id="9c0e0-117">How do I transfer Storm event hub spout checkpoint information from one topology tooanother</span></span>

<span data-ttu-id="9c0e0-118">Hdınsight Storm olay hub'ı spout .jar dosyasına hello kullanarak Azure olay hub'larından okumayı topolojileri geliştirirken, yeni kümede aynı adı hello sahip bir topoloji dağıtmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9c0e0-118">When you develop topologies that read from Azure Event Hubs by using hello HDInsight Storm event hub spout .jar file, you must deploy a topology that has hello same name on a new cluster.</span></span> <span data-ttu-id="9c0e0-119">Ancak, kaydedilmiş tooApache ZooKeeper hello eski kümedeki edildi hello denetim noktası verileri korumanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="9c0e0-119">However, you must retain hello checkpoint data that was committed tooApache ZooKeeper on hello old cluster.</span></span>

### <a name="where-checkpoint-data-is-stored"></a><span data-ttu-id="9c0e0-120">Denetim noktası verileri depolandığı</span><span class="sxs-lookup"><span data-stu-id="9c0e0-120">Where checkpoint data is stored</span></span>
<span data-ttu-id="9c0e0-121">Denetim noktası verileri uzaklıkları için Itanium tabanlı sistemler için hello olay hub'ı spout ZooKeeper içinde iki kök yollarda tarafından depolanır:</span><span class="sxs-lookup"><span data-stu-id="9c0e0-121">Checkpoint data for offsets is stored by hello event hub spout in ZooKeeper in two root paths:</span></span>
- <span data-ttu-id="9c0e0-122">İşlem dışı spout kontrol noktaları /eventhubspout içinde depolanır.</span><span class="sxs-lookup"><span data-stu-id="9c0e0-122">Nontransactional spout checkpoints are stored in /eventhubspout.</span></span>
- <span data-ttu-id="9c0e0-123">İşlem spout denetim noktası verileri / işlem depolanır.</span><span class="sxs-lookup"><span data-stu-id="9c0e0-123">Transactional spout checkpoint data is stored in /transactional.</span></span>

### <a name="how-toorestore"></a><span data-ttu-id="9c0e0-124">Nasıl toorestore</span><span class="sxs-lookup"><span data-stu-id="9c0e0-124">How toorestore</span></span>
<span data-ttu-id="9c0e0-125">bkz: tooget hello komut dosyaları ve tooexport veri ZooKeeper dışında kullanın ve yeni bir adla hello veri geri tooZooKeeper içeri aktarma kitaplıkları [Hdınsight Storm örnekler](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).</span><span class="sxs-lookup"><span data-stu-id="9c0e0-125">tooget hello scripts and libraries that you use tooexport data out of ZooKeeper and then import hello data back tooZooKeeper with a new name, see [HDInsight Storm examples](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).</span></span>

<span data-ttu-id="9c0e0-126">Merhaba LIB klasör hello içeri/dışarı aktarma işlemi için başlangıç uygulaması içeren .jar dosyaları içerir.</span><span class="sxs-lookup"><span data-stu-id="9c0e0-126">hello lib folder has .jar files that contain hello implementation for hello export/import operation.</span></span> <span data-ttu-id="9c0e0-127">Merhaba bash klasör nasıl tooexport verilerden ZooKeeper sunucusu hello eski kümedeki hello gösteren örnek bir komut dosyası vardır ve geri toohello ZooKeeper sunucusu hello yeni kümede içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="9c0e0-127">hello bash folder has an example script that demonstrates how tooexport data from hello ZooKeeper server on hello old cluster, and then import it back toohello ZooKeeper server on hello new cluster.</span></span>

<span data-ttu-id="9c0e0-128">Merhaba çalıştırmak [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) hello ZooKeeper düğümleri tooexport komut dosyası ve veri içeri aktarın.</span><span class="sxs-lookup"><span data-stu-id="9c0e0-128">Run hello [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) script from hello ZooKeeper nodes tooexport and then import data.</span></span> <span data-ttu-id="9c0e0-129">Merhaba betik toohello doğru Hortonworks veri Platformu (HDP) sürümünü güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="9c0e0-129">Update hello script toohello correct Hortonworks Data Platform (HDP) version.</span></span> <span data-ttu-id="9c0e0-130">(Bu komut dosyalarını hdınsight'ta genel yapılması çalışıyoruz.</span><span class="sxs-lookup"><span data-stu-id="9c0e0-130">(We are working on making these scripts generic in HDInsight.</span></span> <span data-ttu-id="9c0e0-131">Genel komut dosyası herhangi bir düğümden hello küme hello kullanıcı tarafından değişiklik olmadan çalıştırabilirsiniz.)</span><span class="sxs-lookup"><span data-stu-id="9c0e0-131">Generic scripts can run from any node on hello cluster without modifications by hello user.)</span></span>

<span data-ttu-id="9c0e0-132">Merhaba Dışa Aktar komutunu hello meta veri tooan Apache Hadoop dağıtılmış dosya sistemi (HDFS) yol (bir Azure Blob Storage veya Azure Data Lake Store deposunda) ayarladığınız bir konuma yazar.</span><span class="sxs-lookup"><span data-stu-id="9c0e0-132">hello export command writes hello metadata tooan Apache Hadoop Distributed File System (HDFS) path (in an Azure Blob Storage or Azure Data Lake Store store) at a location that you set.</span></span>

### <a name="examples"></a><span data-ttu-id="9c0e0-133">Örnekler</span><span class="sxs-lookup"><span data-stu-id="9c0e0-133">Examples</span></span>

#### <a name="export-offset-metadata"></a><span data-ttu-id="9c0e0-134">Uzaklık meta verileri dışarı aktarma</span><span class="sxs-lookup"><span data-stu-id="9c0e0-134">Export offset metadata</span></span>
1. <span data-ttu-id="9c0e0-135">SSH toogo toohello ZooKeeper küme hangi hello denetim noktasından uzaklığı dışarı toobe gereken hello kümede kullanın.</span><span class="sxs-lookup"><span data-stu-id="9c0e0-135">Use SSH toogo toohello ZooKeeper cluster on hello cluster from which hello checkpoint offset needs toobe exported.</span></span>
2. <span data-ttu-id="9c0e0-136">Çalışma hello aşağıdaki komutu (Merhaba HDP sürüm dizesi güncelleştirdikten sonra) tooexport ZooKeeper uzaklığı veri toohello /stormmetadta/zkdata HDFS yol:</span><span class="sxs-lookup"><span data-stu-id="9c0e0-136">Run hello following command (after you update hello HDP version string) tooexport ZooKeeper offset data toohello /stormmetadta/zkdata HDFS path:</span></span>

    ```apache   
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter export /eventhubspout /stormmetadata/zkdata
    ```

#### <a name="import-offset-metadata"></a><span data-ttu-id="9c0e0-137">Uzaklık meta verileri içeri aktarma</span><span class="sxs-lookup"><span data-stu-id="9c0e0-137">Import offset metadata</span></span>
1. <span data-ttu-id="9c0e0-138">SSH toogo toohello ZooKeeper küme hangi hello denetim noktasından uzaklığı dışarı toobe gereken hello kümede kullanın.</span><span class="sxs-lookup"><span data-stu-id="9c0e0-138">Use SSH toogo toohello ZooKeeper cluster on hello cluster from which hello checkpoint offset needs toobe exported.</span></span>
2. <span data-ttu-id="9c0e0-139">Çalışma hello (Merhaba HDP sürüm dizesi güncelleştirdikten sonra) komutu aşağıdaki tooimport ZooKeeper hello HDFS yol/stormmetadata/zkdata toohello ZooKeeper sunucuda hello hedef küme verilerden uzaklık:</span><span class="sxs-lookup"><span data-stu-id="9c0e0-139">Run hello following command (after you update hello HDP version string) tooimport ZooKeeper offset data from hello HDFS path /stormmetadata/zkdata toohello ZooKeeper server on hello target cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter import /eventhubspout /home/sshadmin/zkdata
    ```
   
#### <a name="delete-offset-metadata-so-that-topologies-can-start-processing-data-from-hello-beginning-or-from-a-timestamp-that-hello-user-chooses"></a><span data-ttu-id="9c0e0-140">Böylece topolojileri hello başından veri işleme başlayabilirsiniz veya bir zaman damgası hello kullanıcı seçer uzaklık meta verilerini silme</span><span class="sxs-lookup"><span data-stu-id="9c0e0-140">Delete offset metadata so that topologies can start processing data from hello beginning, or from a timestamp that hello user chooses</span></span>
1. <span data-ttu-id="9c0e0-141">SSH toogo toohello ZooKeeper küme hangi hello denetim noktasından uzaklığı dışarı toobe gereken hello kümede kullanın.</span><span class="sxs-lookup"><span data-stu-id="9c0e0-141">Use SSH toogo toohello ZooKeeper cluster on hello cluster from which hello checkpoint offset needs toobe exported.</span></span>
2. <span data-ttu-id="9c0e0-142">Çalışma hello (Merhaba HDP sürüm dizesi güncelleştirdikten sonra) komutu aşağıdaki toodelete tüm ZooKeeper hello geçerli küme verilerde uzaklık:</span><span class="sxs-lookup"><span data-stu-id="9c0e0-142">Run hello following command (after you update hello HDP version string) toodelete all ZooKeeper offset data in hello current cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter delete /eventhubspout
    ```

## <a name="how-do-i-locate-storm-binaries-on-a-cluster"></a><span data-ttu-id="9c0e0-143">Bir kümede nasıl Storm ikili dosyaları bulun</span><span class="sxs-lookup"><span data-stu-id="9c0e0-143">How do I locate Storm binaries on a cluster</span></span>
<span data-ttu-id="9c0e0-144">Merhaba geçerli HDP yığını için Storm ikili dosyalarını /usr/hdp/current/storm-client içinde ' dir.</span><span class="sxs-lookup"><span data-stu-id="9c0e0-144">Storm binaries for hello current HDP stack are in /usr/hdp/current/storm-client.</span></span> <span data-ttu-id="9c0e0-145">Başlangıç konumu olan hello baş düğümler ve çalışan düğümleri için aynı.</span><span class="sxs-lookup"><span data-stu-id="9c0e0-145">hello location is hello same both for head nodes and for worker nodes.</span></span>
 
<span data-ttu-id="9c0e0-146">Birden çok ikili dosyaları /usr/hdp (örneğin, /usr/hdp/2.5.0.1233/storm) belirli HDP sürümlerde için olabilir.</span><span class="sxs-lookup"><span data-stu-id="9c0e0-146">There might be multiple binaries for specific HDP versions in /usr/hdp (for example, /usr/hdp/2.5.0.1233/storm).</span></span> <span data-ttu-id="9c0e0-147">Merhaba kümede çalışan symlinked toohello en son sürümünü Hello /usr/hdp/current/storm-client klasörüdür.</span><span class="sxs-lookup"><span data-stu-id="9c0e0-147">hello /usr/hdp/current/storm-client folder is symlinked toohello latest version that is running on hello cluster.</span></span>

<span data-ttu-id="9c0e0-148">Daha fazla bilgi için bkz: [Bağlan SSH kullanarak Hdınsight kümesi tooan](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) ve [Storm](http://storm.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="9c0e0-148">For more information, see [Connect tooan HDInsight cluster by using SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Storm](http://storm.apache.org/).</span></span>
 
## <a name="how-do-i-determine-hello-deployment-topology-of-a-storm-cluster"></a><span data-ttu-id="9c0e0-149">Bir Storm kümesine hello dağıtım topolojisi nasıl belirlerim</span><span class="sxs-lookup"><span data-stu-id="9c0e0-149">How do I determine hello deployment topology of a Storm cluster</span></span>
<span data-ttu-id="9c0e0-150">İlk olarak, Hdınsight Storm ile yüklenen tüm bileşenler tanımlayın.</span><span class="sxs-lookup"><span data-stu-id="9c0e0-150">First, identify all components that are installed with HDInsight Storm.</span></span> <span data-ttu-id="9c0e0-151">Storm kümesi dört düğüm kategorilerini oluşur:</span><span class="sxs-lookup"><span data-stu-id="9c0e0-151">A Storm cluster consists of four node categories:</span></span>

* <span data-ttu-id="9c0e0-152">Ağ geçidi düğümleri</span><span class="sxs-lookup"><span data-stu-id="9c0e0-152">Gateway nodes</span></span>
* <span data-ttu-id="9c0e0-153">Baş düğümler</span><span class="sxs-lookup"><span data-stu-id="9c0e0-153">Head nodes</span></span>
* <span data-ttu-id="9c0e0-154">ZooKeeper düğümleri</span><span class="sxs-lookup"><span data-stu-id="9c0e0-154">ZooKeeper nodes</span></span>
* <span data-ttu-id="9c0e0-155">Çalışan düğümü</span><span class="sxs-lookup"><span data-stu-id="9c0e0-155">Worker nodes</span></span>
 
### <a name="gateway-nodes"></a><span data-ttu-id="9c0e0-156">Ağ geçidi düğümleri</span><span class="sxs-lookup"><span data-stu-id="9c0e0-156">Gateway nodes</span></span>
<span data-ttu-id="9c0e0-157">Bir ağ geçidi düğümü, bir ağ geçidi ve genel erişim tooan active Ambari yönetim hizmeti sağlayan ters proxy hizmeti olduğu.</span><span class="sxs-lookup"><span data-stu-id="9c0e0-157">A gateway node is a gateway and reverse proxy service that enables public access tooan active Ambari management service.</span></span> <span data-ttu-id="9c0e0-158">Ayrıca, Ambari öncü seçim işler.</span><span class="sxs-lookup"><span data-stu-id="9c0e0-158">It also handles Ambari leader election.</span></span>
 
### <a name="head-nodes"></a><span data-ttu-id="9c0e0-159">Baş düğümler</span><span class="sxs-lookup"><span data-stu-id="9c0e0-159">Head nodes</span></span>
<span data-ttu-id="9c0e0-160">Storm baş düğümler Hizmetleri aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9c0e0-160">Storm head nodes run hello following services:</span></span>
* <span data-ttu-id="9c0e0-161">Nimbus</span><span class="sxs-lookup"><span data-stu-id="9c0e0-161">Nimbus</span></span>
* <span data-ttu-id="9c0e0-162">Ambarı sunucusu</span><span class="sxs-lookup"><span data-stu-id="9c0e0-162">Ambari server</span></span>
* <span data-ttu-id="9c0e0-163">Ambari ölçümleri sunucu</span><span class="sxs-lookup"><span data-stu-id="9c0e0-163">Ambari Metrics server</span></span>
* <span data-ttu-id="9c0e0-164">Ambari ölçümleri Toplayıcı</span><span class="sxs-lookup"><span data-stu-id="9c0e0-164">Ambari Metrics Collector</span></span>
 
### <a name="zookeeper-nodes"></a><span data-ttu-id="9c0e0-165">ZooKeeper düğümleri</span><span class="sxs-lookup"><span data-stu-id="9c0e0-165">ZooKeeper nodes</span></span>
<span data-ttu-id="9c0e0-166">Hdınsight üç düğümü ZooKeeper çekirdek ile birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="9c0e0-166">HDInsight comes with a three-node ZooKeeper quorum.</span></span> <span data-ttu-id="9c0e0-167">Merhaba çekirdek boyutu sabittir ve yapılandırılamayan.</span><span class="sxs-lookup"><span data-stu-id="9c0e0-167">hello quorum size is fixed, and cannot be reconfigured.</span></span>
 
<span data-ttu-id="9c0e0-168">Storm hello kümede yapılandırılmış tooautomatically kullanım hello ZooKeeper çekirdek hizmetleridir.</span><span class="sxs-lookup"><span data-stu-id="9c0e0-168">Storm services in hello cluster are configured tooautomatically use hello ZooKeeper quorum.</span></span>
 
### <a name="worker-nodes"></a><span data-ttu-id="9c0e0-169">Çalışan düğümü</span><span class="sxs-lookup"><span data-stu-id="9c0e0-169">Worker nodes</span></span>
<span data-ttu-id="9c0e0-170">Storm çalışan düğümleri Hizmetleri aşağıdaki hello çalıştırın:</span><span class="sxs-lookup"><span data-stu-id="9c0e0-170">Storm worker nodes run hello following services:</span></span>
* <span data-ttu-id="9c0e0-171">Gözetmen</span><span class="sxs-lookup"><span data-stu-id="9c0e0-171">Supervisor</span></span>
* <span data-ttu-id="9c0e0-172">Çalışan Java topolojileri çalıştırmak için makineleri (JVMs)</span><span class="sxs-lookup"><span data-stu-id="9c0e0-172">Worker Java virtual machines (JVMs), for running topologies</span></span>
* <span data-ttu-id="9c0e0-173">Ambari aracı</span><span class="sxs-lookup"><span data-stu-id="9c0e0-173">Ambari agent</span></span>
 
## <a name="how-do-i-locate-storm-event-hub-spout-binaries-for-development"></a><span data-ttu-id="9c0e0-174">Geliştirme için Storm olay hub'ı spout ikili dosyalarını nasıl bulun</span><span class="sxs-lookup"><span data-stu-id="9c0e0-174">How do I locate Storm event hub spout binaries for development</span></span>
 
<span data-ttu-id="9c0e0-175">Storm olay hub'ı spout .jar dosyaları topolojinizi ile kullanma hakkında daha fazla bilgi için kaynakları aşağıdaki hello bakın.</span><span class="sxs-lookup"><span data-stu-id="9c0e0-175">For more information about using Storm event hub spout .jar files with your topology, see hello following resources.</span></span>
 
### <a name="java-based-topology"></a><span data-ttu-id="9c0e0-176">Java tabanlı topolojisi</span><span class="sxs-lookup"><span data-stu-id="9c0e0-176">Java-based topology</span></span>
[<span data-ttu-id="9c0e0-177">Azure Event hubs'tan (Java) hdınsight'ta Storm işlem olayları</span><span class="sxs-lookup"><span data-stu-id="9c0e0-177">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-java-event-hub-topology)
 
### <a name="c-based-topology-mono-on-hdinsight-34-linux-storm-clusters"></a><span data-ttu-id="9c0e0-178">C#-topoloji (Mono Hdınsight 3.4 + Linux Storm kümeleri üzerinde) temel</span><span class="sxs-lookup"><span data-stu-id="9c0e0-178">C#-based topology (Mono on HDInsight 3.4+ Linux Storm clusters)</span></span>
[<span data-ttu-id="9c0e0-179">HDInsight üzerinde Storm ile Azure Event Hubs’tan olay işleme (C#)</span><span class="sxs-lookup"><span data-stu-id="9c0e0-179">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-csharp-event-hub-topology)
 
### <a name="latest-storm-event-hub-spout-binaries-for-hdinsight-35-linux-storm-clusters"></a><span data-ttu-id="9c0e0-180">Storm event hub'ın en son spout Hdınsight 3.5 + Linux Storm kümeleri için ikili dosyalar</span><span class="sxs-lookup"><span data-stu-id="9c0e0-180">Latest Storm event hub spout binaries for HDInsight 3.5+ Linux Storm clusters</span></span>
<span data-ttu-id="9c0e0-181">toolearn Hdınsight ile 3.5 + çalışan toouse hello son Storm olay hub'ı spout kümelerinde Linux Storm bkz hello mvn-repo [Benioku dosyasını](https://github.com/hdinsight/mvn-repo/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="9c0e0-181">toolearn how toouse hello latest Storm event hub spout that works with HDInsight 3.5+ Linux Storm clusters, see hello mvn-repo [readme file](https://github.com/hdinsight/mvn-repo/blob/master/README.md).</span></span>
 
### <a name="source-code-examples"></a><span data-ttu-id="9c0e0-182">Kaynak kodu örnekleri</span><span class="sxs-lookup"><span data-stu-id="9c0e0-182">Source code examples</span></span>
<span data-ttu-id="9c0e0-183">Bkz: [örnekler](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) nasıl tooread ve Azure Event Hub'ın bir Azure Hdınsight kümesinde (Java'da yazılmış) bir Apache Storm topolojisini kullanarak gelen yazma.</span><span class="sxs-lookup"><span data-stu-id="9c0e0-183">See [examples](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) of how tooread and write from Azure Event Hub using an Apache Storm topology (written in Java) on an Azure HDInsight cluster.</span></span>
 
## <a name="how-do-i-locate-storm-log4j-configuration-files-on-clusters"></a><span data-ttu-id="9c0e0-184">Storm Log4J yapılandırma dosyalarını kümelerde nasıl bulun</span><span class="sxs-lookup"><span data-stu-id="9c0e0-184">How do I locate Storm Log4J configuration files on clusters</span></span>
 
<span data-ttu-id="9c0e0-185">Storm Hizmetleri için tooidentify Apache Log4J yapılandırma dosyaları.</span><span class="sxs-lookup"><span data-stu-id="9c0e0-185">tooidentify Apache Log4J configuration files for Storm services.</span></span>
 
### <a name="on-head-nodes"></a><span data-ttu-id="9c0e0-186">Baş düğümler üzerinde</span><span class="sxs-lookup"><span data-stu-id="9c0e0-186">On head nodes</span></span>
<span data-ttu-id="9c0e0-187">Merhaba Nimbus Log4J yapılandırma okuma/usr/hdp/\<HDP sürüm\>/storm/log4j2/cluster.xml.</span><span class="sxs-lookup"><span data-stu-id="9c0e0-187">hello Nimbus Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
### <a name="on-worker-nodes"></a><span data-ttu-id="9c0e0-188">Alt düğümler üzerinde</span><span class="sxs-lookup"><span data-stu-id="9c0e0-188">On worker nodes</span></span>
<span data-ttu-id="9c0e0-189">Hello Yöneticisi Log4J yapılandırma okuma/usr/hdp/\<HDP sürüm\>/storm/log4j2/cluster.xml.</span><span class="sxs-lookup"><span data-stu-id="9c0e0-189">hello supervisor Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
<span data-ttu-id="9c0e0-190">Merhaba çalışan Log4J yapılandırma dosyasını okuma/usr/hdp/\<HDP sürüm\>/storm/log4j2/worker.xml.</span><span class="sxs-lookup"><span data-stu-id="9c0e0-190">hello worker Log4J configuration file is read from /usr/hdp/\<HDP version\>/storm/log4j2/worker.xml.</span></span>
 
<span data-ttu-id="9c0e0-191">Örnekler: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml</span><span class="sxs-lookup"><span data-stu-id="9c0e0-191">Examples: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml</span></span>

