---
title: "Apache Kafka - Azure Hdınsight ile aaaStart | Microsoft Docs"
description: "Azure Hdınsight'ta Apache Kafka toocreate küme nasıl öğrenin. Bilgi nasıl toocreate konuları, aboneleri ve tüketicilerin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 43585abf-bec1-4322-adde-6db21de98d7f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: b93299d88dc2cf9a9764662509308ff75fd74474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="start-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="337e8-104">HDInsight üzerinde Apache Kafka'yı (önizleme) kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="337e8-104">Start with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="337e8-105">Bilgi nasıl toocreate ve bir [Apache Kafka](https://kafka.apache.org) Azure Hdınsight kümesinde.</span><span class="sxs-lookup"><span data-stu-id="337e8-105">Learn how toocreate and use an [Apache Kafka](https://kafka.apache.org) cluster on Azure HDInsight.</span></span> <span data-ttu-id="337e8-106">Kafka, HDInsight ile birlikte kullanılabilen, açık kaynaklı bir dağıtılmış akış platformudur.</span><span class="sxs-lookup"><span data-stu-id="337e8-106">Kafka is an open-source, distributed streaming platform that is available with HDInsight.</span></span> <span data-ttu-id="337e8-107">Sık kullanılan bir ileti Aracısı benzer işlevsellik sağlar gibi tooa yayımlama-abone olma ileti sırası.</span><span class="sxs-lookup"><span data-stu-id="337e8-107">It is often used as a message broker, as it provides functionality similar tooa publish-subscribe message queue.</span></span>

> [!NOTE]
> <span data-ttu-id="337e8-108">Kafka’nın şu anda HDInsight ile kullanılabilen iki sürümü vardır: 0.9.0 (HDInsight 3.4) ve 0.10.0 (HDInsight 3.5 ve 3.6).</span><span class="sxs-lookup"><span data-stu-id="337e8-108">There are currently two versions of Kafka available with HDInsight; 0.9.0 (HDInsight 3.4) and 0.10.0 (HDInsight 3.5 and 3.6).</span></span> <span data-ttu-id="337e8-109">Bu belgedeki Hello adımlar üzerinde Hdınsight 3.6 Kafka kullandığınız varsayılır.</span><span class="sxs-lookup"><span data-stu-id="337e8-109">hello steps in this document assume that you are using Kafka on HDInsight 3.6.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="create-a-kafka-cluster"></a><span data-ttu-id="337e8-110">Kafka kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="337e8-110">Create a Kafka cluster</span></span>

<span data-ttu-id="337e8-111">Adımları toocreate bir Kafka Hdınsight kümesinde aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="337e8-111">Use hello following steps toocreate a Kafka on HDInsight cluster:</span></span>

1. <span data-ttu-id="337e8-112">Merhaba gelen [Azure portal](https://portal.azure.com)seçin **+ yeni**, **Intelligence + analiz**ve ardından **Hdınsight**.</span><span class="sxs-lookup"><span data-stu-id="337e8-112">From hello [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>
   
    ![HDInsight kümesi oluşturma](./media/hdinsight-apache-kafka-get-started/create-hdinsight.png)

2. <span data-ttu-id="337e8-114">Gelen **Temelleri**, aşağıdaki bilgilerle hello girin:</span><span class="sxs-lookup"><span data-stu-id="337e8-114">From **Basics**, enter hello following information:</span></span>

    * <span data-ttu-id="337e8-115">**Küme adı**: Merhaba Hdınsight kümesi hello adı.</span><span class="sxs-lookup"><span data-stu-id="337e8-115">**Cluster Name**: hello name of hello HDInsight cluster.</span></span>
    * <span data-ttu-id="337e8-116">**Abonelik**: hello abonelik toouse seçin.</span><span class="sxs-lookup"><span data-stu-id="337e8-116">**Subscription**: Select hello subscription toouse.</span></span>
    * <span data-ttu-id="337e8-117">**Oturum açma kullanıcı küme** ve **küme oturum açma parolasını**: hello küme HTTPS üzerinden erişirken hello oturum açma.</span><span class="sxs-lookup"><span data-stu-id="337e8-117">**Cluster login username** and **Cluster login password**: hello login when accessing hello cluster over HTTPS.</span></span> <span data-ttu-id="337e8-118">Bu kimlik bilgileri tooaccess Hizmetleri gibi hello Ambari Web kullanıcı Arabirimi veya REST API'yi kullanın.</span><span class="sxs-lookup"><span data-stu-id="337e8-118">You use these credentials tooaccess services such as hello Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="337e8-119">**Güvenli Kabuk (SSH) kullanıcıadı**: hello küme SSH üzerinden erişirken kullanılan hello oturum açma.</span><span class="sxs-lookup"><span data-stu-id="337e8-119">**Secure Shell (SSH) username**: hello login used when accessing hello cluster over SSH.</span></span> <span data-ttu-id="337e8-120">Varsayılan olarak hello parola olduğu hello hello küme oturum açma parolası ile aynı.</span><span class="sxs-lookup"><span data-stu-id="337e8-120">By default hello password is hello same as hello cluster login password.</span></span>
    * <span data-ttu-id="337e8-121">**Kaynak grubu**: hello kaynak grubu toocreate hello kümede.</span><span class="sxs-lookup"><span data-stu-id="337e8-121">**Resource Group**: hello resource group toocreate hello cluster in.</span></span>
    * <span data-ttu-id="337e8-122">**Konum**: hello Azure bölgesi toocreate hello kümede.</span><span class="sxs-lookup"><span data-stu-id="337e8-122">**Location**: hello Azure region toocreate hello cluster in.</span></span>
   
 ![Abonelik seçme](./media/hdinsight-apache-kafka-get-started/hdinsight-basic-configuration.png)

3. <span data-ttu-id="337e8-124">Seçin **küme türü**, ve ardından kümesi hello aşağıdaki değerleri **küme yapılandırması**:</span><span class="sxs-lookup"><span data-stu-id="337e8-124">Select **Cluster type**, and then set hello following values from **Cluster configuration**:</span></span>
   
    * <span data-ttu-id="337e8-125">**Küme Türü**: Kafka</span><span class="sxs-lookup"><span data-stu-id="337e8-125">**Cluster Type**: Kafka</span></span>

    * <span data-ttu-id="337e8-126">**Sürüm**: Kafka 0.10.0 (HDI 3.6)</span><span class="sxs-lookup"><span data-stu-id="337e8-126">**Version**: Kafka 0.10.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="337e8-127">**Küme Katmanı**: Standart</span><span class="sxs-lookup"><span data-stu-id="337e8-127">**Cluster Tier**: Standard</span></span>
     
 <span data-ttu-id="337e8-128">Son olarak, hello kullan **seçin** düğmesini toosave ayarlar.</span><span class="sxs-lookup"><span data-stu-id="337e8-128">Finally, use hello **Select** button toosave settings.</span></span>
     
 ![Küme türü seçme](./media/hdinsight-apache-kafka-get-started/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="337e8-130">Merhaba küme türü seçtikten sonra hello kullan __seçin__ düğme tooset hello küme türü.</span><span class="sxs-lookup"><span data-stu-id="337e8-130">After selecting hello cluster type, use hello __Select__ button tooset hello cluster type.</span></span> <span data-ttu-id="337e8-131">Ardından, hello kullanın __sonraki__ düğme toofinish temel yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="337e8-131">Next, use hello __Next__ button toofinish basic configuration.</span></span>

5. <span data-ttu-id="337e8-132">**Depolama**’dan bir depolama hesabı seçin veya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="337e8-132">From **Storage**, select or create a Storage account.</span></span> <span data-ttu-id="337e8-133">Bu belgedeki Hello adımlar için hello diğer alanları hello varsayılan değerleri bırakın.</span><span class="sxs-lookup"><span data-stu-id="337e8-133">For hello steps in this document, leave hello other fields at hello default values.</span></span> <span data-ttu-id="337e8-134">Kullanım hello __sonraki__ düğme toosave depolama yapılandırması.</span><span class="sxs-lookup"><span data-stu-id="337e8-134">Use hello __Next__ button toosave storage configuration.</span></span>

    ![Hdınsight için Hello depolama hesabı ayarlarını belirleme](./media/hdinsight-apache-kafka-get-started/set-hdinsight-storage-account.png)

6. <span data-ttu-id="337e8-136">Gelen __uygulamaları (isteğe bağlı)__seçin __sonraki__ toocontinue.</span><span class="sxs-lookup"><span data-stu-id="337e8-136">From __Applications (optional)__, select __Next__ toocontinue.</span></span> <span data-ttu-id="337e8-137">Bu örnek için uygulama gerekmez.</span><span class="sxs-lookup"><span data-stu-id="337e8-137">No applications are required for this example.</span></span>

7. <span data-ttu-id="337e8-138">Gelen __küme boyutu__seçin __sonraki__ toocontinue.</span><span class="sxs-lookup"><span data-stu-id="337e8-138">From __Cluster size__, select __Next__ toocontinue.</span></span>

    > [!WARNING]
    > <span data-ttu-id="337e8-139">Hdınsight üzerinde Kafka kullanılabilirliğini tooguarantee, kümenizi en az üç alt düğümleri içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="337e8-139">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span>

    ![Set hello Kafka küme boyutu](./media/hdinsight-apache-kafka-get-started/kafka-cluster-size.png)

    > [!NOTE]
    > <span data-ttu-id="337e8-141">Merhaba **çalışan düğümü başına disk** giriş denetimlerini hello hdınsight'ta Kafka ölçeklenebilirliğini.</span><span class="sxs-lookup"><span data-stu-id="337e8-141">hello **disks per worker node** entry controls hello scalability of Kafka on HDInsight.</span></span> <span data-ttu-id="337e8-142">Daha fazla bilgi için bkz. [HDInsight üzerinde Kafka'nın depolama alanını ve ölçeklenebilirliğini yapılandırma](hdinsight-apache-kafka-scalability.md).</span><span class="sxs-lookup"><span data-stu-id="337e8-142">For more information, see [Configure storage and scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span></span>

8. <span data-ttu-id="337e8-143">Gelen __Gelişmiş ayarları__seçin __sonraki__ toocontinue.</span><span class="sxs-lookup"><span data-stu-id="337e8-143">From __Advanced settings__, select __Next__ toocontinue.</span></span>

9. <span data-ttu-id="337e8-144">Merhaba gelen **Özet**, hello kümesi için başlangıç yapılandırmasını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="337e8-144">From hello **Summary**, review hello configuration for hello cluster.</span></span> <span data-ttu-id="337e8-145">Kullanım hello __Düzenle__ toochange yanlış ayarları bağlar.</span><span class="sxs-lookup"><span data-stu-id="337e8-145">Use hello __Edit__ links toochange any settings that are incorrect.</span></span> <span data-ttu-id="337e8-146">Son olarak, the__Create__ düğmesini toocreate hello küme kullanın.</span><span class="sxs-lookup"><span data-stu-id="337e8-146">Finally, use the__Create__ button toocreate hello cluster.</span></span>
   
    ![Küme yapılandırma özeti](./media/hdinsight-apache-kafka-get-started/hdinsight-configuration-summary.png)
   
    > [!NOTE]
    > <span data-ttu-id="337e8-148">Too20 dakika toocreate hello küme alabilir.</span><span class="sxs-lookup"><span data-stu-id="337e8-148">It can take up too20 minutes toocreate hello cluster.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="337e8-149">Toohello kümesine bağlanın</span><span class="sxs-lookup"><span data-stu-id="337e8-149">Connect toohello cluster</span></span>

> [!IMPORTANT]
> <span data-ttu-id="337e8-150">Aşağıdaki adımları hello gerçekleştirirken, bir SSH istemcisi kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="337e8-150">When performing hello following steps, you must use an SSH client.</span></span> <span data-ttu-id="337e8-151">Daha fazla bilgi için bkz: Merhaba [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md) belge.</span><span class="sxs-lookup"><span data-stu-id="337e8-151">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

<span data-ttu-id="337e8-152">İstemcinizden, SSH tooconnect toohello küme kullanın:</span><span class="sxs-lookup"><span data-stu-id="337e8-152">From your client, use SSH tooconnect toohello cluster:</span></span>

```ssh SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net```

<span data-ttu-id="337e8-153">Değiştir **SSHUSER** ile küme oluşturma sırasında sağladığınız hello SSH kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="337e8-153">Replace **SSHUSER** with hello SSH username you provided during cluster creation.</span></span> <span data-ttu-id="337e8-154">Değiştir **CLUSTERNAME** hello küme hello adı.</span><span class="sxs-lookup"><span data-stu-id="337e8-154">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>

<span data-ttu-id="337e8-155">İstendiğinde, hello SSH hesabı için kullanılan hello parola girin.</span><span class="sxs-lookup"><span data-stu-id="337e8-155">When prompted, enter hello password you used for hello SSH account.</span></span>

<span data-ttu-id="337e8-156">Bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="337e8-156">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="337e8-157"><a id="getkafkainfo"></a>Merhaba Zookeeper ve Aracısı ana bilgisayar bilgilerini al</span><span class="sxs-lookup"><span data-stu-id="337e8-157"><a id="getkafkainfo"></a>Get hello Zookeeper and Broker host information</span></span>

<span data-ttu-id="337e8-158">Kafka ile çalışırken, iki ana değer bilmeniz gerekir; Merhaba *Zookeeper* konakları ve hello *Aracısı* ana bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="337e8-158">When working with Kafka, you must know two host values; hello *Zookeeper* hosts and hello *Broker* hosts.</span></span> <span data-ttu-id="337e8-159">Bu konaklar hello Kafka API ve birçok sevk hello yardımcı programlarını Kafka ile kullanılır.</span><span class="sxs-lookup"><span data-stu-id="337e8-159">These hosts are used with hello Kafka API and many of hello utilities that ship with Kafka.</span></span>

<span data-ttu-id="337e8-160">Merhaba ana bilgisayar bilgilerini içeren adımları toocreate ortam değişkenleri aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="337e8-160">Use hello following steps toocreate environment variables that contain hello host information.</span></span> <span data-ttu-id="337e8-161">Bu ortam değişkenleri, bu belgedeki hello adımda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="337e8-161">These environment variables are used in hello steps in this document.</span></span>

1. <span data-ttu-id="337e8-162">Bir SSH bağlantısı toohello kümesinden kullanım hello şu komutu tooinstall hello `jq` yardımcı programı.</span><span class="sxs-lookup"><span data-stu-id="337e8-162">From an SSH connection toohello cluster, use hello following command tooinstall hello `jq` utility.</span></span> <span data-ttu-id="337e8-163">Bu yardımcı program kullanılan tooparse JSON belgeleri olan ve hello Aracısı ana bilgisayar bilgilerini alma yararlıdır:</span><span class="sxs-lookup"><span data-stu-id="337e8-163">This utility is used tooparse JSON documents, and is useful in retrieving hello broker host information:</span></span>
   
    ```bash
    sudo apt -y install jq
    ```

2. <span data-ttu-id="337e8-164">Ambari, aşağıdaki komutları kullanın hello bilgilerle tooset hello ortam değişkenleri alındı:</span><span class="sxs-lookup"><span data-stu-id="337e8-164">tooset hello environment variables with information retrieved from Ambari, use hello following commands:</span></span>

    ```bash
    CLUSTERNAME='your cluster name'
    PASSWORD='your cluster password'
    export KAFKAZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`

    export KAFKABROKERS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`

    echo '$KAFKAZKHOSTS='$KAFKAZKHOSTS
    echo '$KAFKABROKERS='$KAFKABROKERS
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="337e8-165">Ayarlama `CLUSTERNAME=` hello Kafka küme toohello adı.</span><span class="sxs-lookup"><span data-stu-id="337e8-165">Set `CLUSTERNAME=` toohello name of hello Kafka cluster.</span></span> <span data-ttu-id="337e8-166">Ayarlama `PASSWORD=` hello küme oluştururken kullandığınız toohello (Yönetici) oturum açma parolası.</span><span class="sxs-lookup"><span data-stu-id="337e8-166">Set `PASSWORD=` toohello login (admin) password you used when creating hello cluster.</span></span>

    <span data-ttu-id="337e8-167">Merhaba aşağıdaki Merhaba içeriğine bir örnek metindir `$KAFKAZKHOSTS`:</span><span class="sxs-lookup"><span data-stu-id="337e8-167">hello following text is an example of hello contents of `$KAFKAZKHOSTS`:</span></span>
   
    `zk0-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk2-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181`
   
    <span data-ttu-id="337e8-168">Merhaba aşağıdaki Merhaba içeriğine bir örnek metindir `$KAFKABROKERS`:</span><span class="sxs-lookup"><span data-stu-id="337e8-168">hello following text is an example of hello contents of `$KAFKABROKERS`:</span></span>
   
    `wn1-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092,wn0-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092`

    > [!NOTE]
    > <span data-ttu-id="337e8-169">Merhaba `cut` komutu kullanılan tootrim hello konakları tootwo konak girişleri listesi verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="337e8-169">hello `cut` command is used tootrim hello list of hosts tootwo host entries.</span></span> <span data-ttu-id="337e8-170">Bir Kafka tüketici veya üretici oluştururken tooprovide hello tam ana bilgisayar listesini gerekmez.</span><span class="sxs-lookup"><span data-stu-id="337e8-170">You do not need tooprovide hello full list of hosts when creating a Kafka consumer or producer.</span></span>
   
    > [!WARNING]
    > <span data-ttu-id="337e8-171">Bu oturumda döndürülen hello bilgi tooalways doğru kullanmayın.</span><span class="sxs-lookup"><span data-stu-id="337e8-171">Do not rely on hello information returned from this session tooalways be accurate.</span></span> <span data-ttu-id="337e8-172">Merhaba küme ölçeklendirme, yeni aracıların eklenir veya kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="337e8-172">If you scale hello cluster, new brokers are added or removed.</span></span> <span data-ttu-id="337e8-173">Bir hata oluşur ve bir düğüm değiştirilir, hello düğümü hello ana bilgisayar adını değiştirebilir.</span><span class="sxs-lookup"><span data-stu-id="337e8-173">If a failure occurs and a node is replaced, hello host name for hello node may change.</span></span>
    >
    > <span data-ttu-id="337e8-174">Kısa süre içinde geçerli bilgilere sahip tooensure kullanabilmek hello Zookeeper ve Aracısı ana bilgisayar bilgilerini almak.</span><span class="sxs-lookup"><span data-stu-id="337e8-174">You should retrieve hello Zookeeper and broker hosts information shortly before you use it tooensure you have valid information.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="337e8-175">Konu başlığı oluşturma</span><span class="sxs-lookup"><span data-stu-id="337e8-175">Create a topic</span></span>

<span data-ttu-id="337e8-176">Kafka, veri akışlarını *topics* (konu başlıkları) adlı kategorilerde depolar.</span><span class="sxs-lookup"><span data-stu-id="337e8-176">Kafka stores streams of data in categories called *topics*.</span></span> <span data-ttu-id="337e8-177">Bir SSH bağlantısı tooa küme headnode, bir konu Kafka toocreate ile sağlanan bir komut dosyasını kullanın:</span><span class="sxs-lookup"><span data-stu-id="337e8-177">From An SSH connection tooa cluster headnode, use a script provided with Kafka toocreate a topic:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic test --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="337e8-178">Bu komut, depolanan hello konak bilgileri kullanarak tooZookeeper bağlanır `$KAFKAZKHOSTS`ve ardından adlı Kafka konu Oluştur **test**.</span><span class="sxs-lookup"><span data-stu-id="337e8-178">This command connects tooZookeeper using hello host information stored in `$KAFKAZKHOSTS`, and then create Kafka topic named **test**.</span></span> <span data-ttu-id="337e8-179">Bu hello konu aşağıdaki komut dosyası toolist konularda hello kullanılarak oluşturulmuş doğrulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="337e8-179">You can verify that hello topic was created by using hello following script toolist topics:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="337e8-180">Merhaba bu komutun çıktısı Kafka konuları, hello içeren listeler **test** konu.</span><span class="sxs-lookup"><span data-stu-id="337e8-180">hello output of this command lists Kafka topics, which contains hello **test** topic.</span></span>

## <a name="produce-and-consume-records"></a><span data-ttu-id="337e8-181">Kayıt oluşturma ve kullanma</span><span class="sxs-lookup"><span data-stu-id="337e8-181">Produce and consume records</span></span>

<span data-ttu-id="337e8-182">Kafka, konu başlıklarında *records* (kayıtlar) depolar.</span><span class="sxs-lookup"><span data-stu-id="337e8-182">Kafka stores *records* in topics.</span></span> <span data-ttu-id="337e8-183">Kayıtlar, *Üreticiler* tarafından oluşturulur ve *tüketiciler* tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="337e8-183">Records are produced by *producers*, and consumed by *consumers*.</span></span> <span data-ttu-id="337e8-184">Üreticiler, kayıtları Kafka *aracılarından* alır.</span><span class="sxs-lookup"><span data-stu-id="337e8-184">Producers retrieve records from Kafka *brokers*.</span></span> <span data-ttu-id="337e8-185">HDInsight kümenizdeki her çalışan düğümü bir Kafka aracısıdır.</span><span class="sxs-lookup"><span data-stu-id="337e8-185">Each worker node in your HDInsight cluster is a Kafka broker.</span></span>

<span data-ttu-id="337e8-186">Daha önce oluşturduğunuz ve bunları bir tüketici kullanarak okunur hello test konu ile aşağıdaki adımları toostore kayıtları hello kullan:</span><span class="sxs-lookup"><span data-stu-id="337e8-186">Use hello following steps toostore records into hello test topic you created earlier, and then read them using a consumer:</span></span>

1. <span data-ttu-id="337e8-187">Merhaba SSH oturumundan Kafka toowrite kayıtları toohello konu ile sağlanan bir komut dosyasını kullanın:</span><span class="sxs-lookup"><span data-stu-id="337e8-187">From hello SSH session, use a script provided with Kafka toowrite records toohello topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $KAFKABROKERS --topic test
    ```
   
    <span data-ttu-id="337e8-188">Toohello sonra bu komut istemi döndürülmez.</span><span class="sxs-lookup"><span data-stu-id="337e8-188">You are not returned toohello prompt after this command.</span></span> <span data-ttu-id="337e8-189">Bunun yerine, birkaç metin iletileri yazın ve ardından **Ctrl + C** toostop toohello konu gönderme.</span><span class="sxs-lookup"><span data-stu-id="337e8-189">Instead, type a few text messages and then use **Ctrl + C** toostop sending toohello topic.</span></span> <span data-ttu-id="337e8-190">Her satır ayrı bir kayıt olarak gönderilir.</span><span class="sxs-lookup"><span data-stu-id="337e8-190">Each line is sent as a separate record.</span></span>

2. <span data-ttu-id="337e8-191">Kafka tooread kayıtlarla hello konuda sağlanan komut dosyasını kullanın:</span><span class="sxs-lookup"><span data-stu-id="337e8-191">Use a script provided with Kafka tooread records from hello topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic test --from-beginning
    ```
   
    <span data-ttu-id="337e8-192">Bu komut hello konusundan hello kayıtları alır ve bunları görüntüler.</span><span class="sxs-lookup"><span data-stu-id="337e8-192">This command retrieves hello records from hello topic and displays them.</span></span> <span data-ttu-id="337e8-193">Kullanarak `--from-beginning` tüm kayıtlar alınır şekilde hello tüketici toostart hello hello akış başlangıcından söyler.</span><span class="sxs-lookup"><span data-stu-id="337e8-193">Using `--from-beginning` tells hello consumer toostart from hello beginning of hello stream, so all records are retrieved.</span></span>

3. <span data-ttu-id="337e8-194">Kullanım __Ctrl + C__ toostop hello tüketici.</span><span class="sxs-lookup"><span data-stu-id="337e8-194">Use __Ctrl + C__ toostop hello consumer.</span></span>

## <a name="producer-and-consumer-api"></a><span data-ttu-id="337e8-195">Üretici ve tüketici API’si</span><span class="sxs-lookup"><span data-stu-id="337e8-195">Producer and consumer API</span></span>

<span data-ttu-id="337e8-196">Program aracılığıyla da oluşturabilir ve hello kullanarak kayıtları tüketen [Kafka API'leri](http://kafka.apache.org/documentation#api).</span><span class="sxs-lookup"><span data-stu-id="337e8-196">You can also programmatically produce and consume records using hello [Kafka APIs](http://kafka.apache.org/documentation#api).</span></span> <span data-ttu-id="337e8-197">toobuild Java üretici ve Tüketici ' hello geliştirme ortamınızı aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="337e8-197">toobuild a Java producer and consumer, use hello following steps from your development environment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="337e8-198">Geliştirme ortamınızda yüklü bileşenleri aşağıdaki hello sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="337e8-198">You must have hello following components installed in your development environment:</span></span>
>
> * <span data-ttu-id="337e8-199">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) veya OpenJDK gibi eşdeğeri.</span><span class="sxs-lookup"><span data-stu-id="337e8-199">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or an equivalent, such as OpenJDK.</span></span>
>
> * [<span data-ttu-id="337e8-200">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="337e8-200">Apache Maven</span></span>](http://maven.apache.org/)
>
> * <span data-ttu-id="337e8-201">Bir SSH istemcisi ve hello `scp` komutu.</span><span class="sxs-lookup"><span data-stu-id="337e8-201">An SSH client and hello `scp` command.</span></span> <span data-ttu-id="337e8-202">Daha fazla bilgi için bkz: Merhaba [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md) belge.</span><span class="sxs-lookup"><span data-stu-id="337e8-202">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

1. <span data-ttu-id="337e8-203">Merhaba örneklerinden karşıdan [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span><span class="sxs-lookup"><span data-stu-id="337e8-203">Download hello examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span></span> <span data-ttu-id="337e8-204">Merhaba üretici/tüketici örneğin hello projesi hello kullanmak `Producer-Consumer` dizin.</span><span class="sxs-lookup"><span data-stu-id="337e8-204">For hello producer/consumer example, use hello project in hello `Producer-Consumer` directory.</span></span> <span data-ttu-id="337e8-205">Bu örnek sınıflar aşağıdaki hello içerir:</span><span class="sxs-lookup"><span data-stu-id="337e8-205">This example contains hello following classes:</span></span>
   
    * <span data-ttu-id="337e8-206">**Çalıştırma** -hello tüketici veya üretici başlatır.</span><span class="sxs-lookup"><span data-stu-id="337e8-206">**Run** - starts either hello consumer or producer.</span></span>

    * <span data-ttu-id="337e8-207">**Üretici** -depoları 1.000.000 kayıtları toohello konu.</span><span class="sxs-lookup"><span data-stu-id="337e8-207">**Producer** - stores 1,000,000 records toohello topic.</span></span>

    * <span data-ttu-id="337e8-208">**Tüketici** -hello konusundan kayıtları okur.</span><span class="sxs-lookup"><span data-stu-id="337e8-208">**Consumer** - reads records from hello topic.</span></span>

2. <span data-ttu-id="337e8-209">toocreate jar paket dizinleri toohello hello konumunu değiştirme `Producer-Consumer` komutu aşağıdaki dizin ve kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="337e8-209">toocreate a jar package, change directories toohello location of hello `Producer-Consumer` directory and use hello following command:</span></span>

    ```
    mvn clean package
    ```

    <span data-ttu-id="337e8-210">Bu komut, `kafka-producer-consumer-1.0-SNAPSHOT.jar` adlı dosyayı içeren `target` adlı bir dizin oluşturur.</span><span class="sxs-lookup"><span data-stu-id="337e8-210">This command creates a directory named `target`, that contains a file named `kafka-producer-consumer-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="337e8-211">Kullanım hello aşağıdaki komutları toocopy hello `kafka-producer-consumer-1.0-SNAPSHOT.jar` dosya tooyour Hdınsight kümesi:</span><span class="sxs-lookup"><span data-stu-id="337e8-211">Use hello following commands toocopy hello `kafka-producer-consumer-1.0-SNAPSHOT.jar` file tooyour HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-producer-consumer-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-producer-consumer.jar
    ```
   
    <span data-ttu-id="337e8-212">Değiştir **SSHUSER** kümesi ve Değiştir hello SSH kullanıcıyla **CLUSTERNAME** kümenizin hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="337e8-212">Replace **SSHUSER** with hello SSH user for your cluster, and replace **CLUSTERNAME** with hello name of your cluster.</span></span> <span data-ttu-id="337e8-213">İstendiğinde hello SSH kullanıcı için hello parola girin.</span><span class="sxs-lookup"><span data-stu-id="337e8-213">When prompted enter hello password for hello SSH user.</span></span>

4. <span data-ttu-id="337e8-214">Bir kez hello `scp` komut bittikten hello dosya kopyalama, SSH kullanarak toohello kümesine bağlanın.</span><span class="sxs-lookup"><span data-stu-id="337e8-214">Once hello `scp` command finishes copying hello file, connect toohello cluster using SSH.</span></span> <span data-ttu-id="337e8-215">Komut toowrite kayıtları toohello sınama konusu aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="337e8-215">Use hello following command toowrite records toohello test topic:</span></span>

    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS
    ```

5. <span data-ttu-id="337e8-216">Merhaba işlemi tamamlandıktan sonra komutu tooread hello konusundan aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="337e8-216">Once hello process has finished, use hello following command tooread from hello topic:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS
    ```
   
    <span data-ttu-id="337e8-217">Merhaba kayıtları okuma, bir kayıt sayısı ile birlikte görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="337e8-217">hello records read, along with a count of records, is displayed.</span></span> <span data-ttu-id="337e8-218">Bir önceki adımda komut dosyası kullanarak birçok kayıtları toohello konu gönderilen olarak oturum 1.000.000 birden çok birkaç görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="337e8-218">You may see a few more than 1,000,000 logged as you sent several records toohello topic using a script in an earlier step.</span></span>

6. <span data-ttu-id="337e8-219">Kullanım __Ctrl + C__ tooexit hello tüketici.</span><span class="sxs-lookup"><span data-stu-id="337e8-219">Use __Ctrl + C__ tooexit hello consumer.</span></span>

### <a name="multiple-consumers"></a><span data-ttu-id="337e8-220">Birden çok tüketici</span><span class="sxs-lookup"><span data-stu-id="337e8-220">Multiple consumers</span></span>

<span data-ttu-id="337e8-221">Kafka tüketicileri kayıtları okurken bir tüketici grubu kullanır.</span><span class="sxs-lookup"><span data-stu-id="337e8-221">Kafka consumers use a consumer group when reading records.</span></span> <span data-ttu-id="337e8-222">Birden çok tüketiciye ile aynı grup hello kullanarak bir konu okuma sonuçları yük dengeli.</span><span class="sxs-lookup"><span data-stu-id="337e8-222">Using hello same group with multiple consumers results in load balanced reads from a topic.</span></span> <span data-ttu-id="337e8-223">Merhaba grubundaki her bir tüketici hello kayıtları bir kısmını alır.</span><span class="sxs-lookup"><span data-stu-id="337e8-223">Each consumer in hello group receives a portion of hello records.</span></span> <span data-ttu-id="337e8-224">Bu eylem, aşağıdaki kullanım hello işlemde adımları toosee:</span><span class="sxs-lookup"><span data-stu-id="337e8-224">toosee this process in action, use hello following steps:</span></span>

1. <span data-ttu-id="337e8-225">Yeni bir SSH oturumu toohello kümesi, iki tanesi sahip şekilde açın.</span><span class="sxs-lookup"><span data-stu-id="337e8-225">Open a new SSH session toohello cluster, so that you have two of them.</span></span> <span data-ttu-id="337e8-226">Her oturumda hello kullan toostart ile bir tüketici hello aynı tüketici grubu kimliği:</span><span class="sxs-lookup"><span data-stu-id="337e8-226">In each session, use hello following toostart a consumer with hello same consumer group ID:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS mygroup
    ```

    <span data-ttu-id="337e8-227">Bu komut hello grup kimliği kullanan bir tüketici başlatır `mygroup`.</span><span class="sxs-lookup"><span data-stu-id="337e8-227">This command starts a consumer using hello group ID `mygroup`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="337e8-228">Hello Hello komutlarını kullanmak [hello Zookeeper ve Aracısı ana bilgisayar bilgilerini al](#getkafkainfo) bölüm tooset `$KAFKABROKERS` bu SSH oturumu için.</span><span class="sxs-lookup"><span data-stu-id="337e8-228">Use hello commands in hello [Get hello Zookeeper and Broker host information](#getkafkainfo) section tooset `$KAFKABROKERS` for this SSH session.</span></span>

2. <span data-ttu-id="337e8-229">Merhaba konusundan aldığı her oturum sayıları hello kayıtları olarak izleyin.</span><span class="sxs-lookup"><span data-stu-id="337e8-229">Watch as each session counts hello records it receives from hello topic.</span></span> <span data-ttu-id="337e8-230">Her iki oturumunu Hello toplam olması hello aynı tek bir tüketici önceden alınmış olarak.</span><span class="sxs-lookup"><span data-stu-id="337e8-230">hello total of both sessions should be hello same as you received previously from one consumer.</span></span>

<span data-ttu-id="337e8-231">İstemciler aynı grup hello bölümler hello konu için aracılığıyla işlenmesini hello içinde tüketimi.</span><span class="sxs-lookup"><span data-stu-id="337e8-231">Consumption by clients within hello same group is handled through hello partitions for hello topic.</span></span> <span data-ttu-id="337e8-232">Hello için `test` daha önce oluşturduğunuz konu sekiz bölümü vardır.</span><span class="sxs-lookup"><span data-stu-id="337e8-232">For hello `test` topic created earlier, it has eight partitions.</span></span> <span data-ttu-id="337e8-233">Sekiz SSH oturumları açmak ve bir tüketici tüm oturumları başlatma, her bir tüketici hello konu için tek bir bölüm kayıtları okur.</span><span class="sxs-lookup"><span data-stu-id="337e8-233">If you open eight SSH sessions and launch a consumer in all sessions, each consumer reads records from a single partition for hello topic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="337e8-234">Bir tüketici grubunda bölümden daha fazla tüketici örneği olamaz.</span><span class="sxs-lookup"><span data-stu-id="337e8-234">There cannot be more consumer instances in a consumer group than partitions.</span></span> <span data-ttu-id="337e8-235">Hello hello konuda bölüm sayısı olduğundan bu örnekte, tooeight tüketicileri bir tüketici grubu içerebilir.</span><span class="sxs-lookup"><span data-stu-id="337e8-235">In this example, one consumer group can contain up tooeight consumers since that is hello number of partitions in hello topic.</span></span> <span data-ttu-id="337e8-236">Ya da her biri en fazla sekiz tüketici içeren birden fazla tüketici grubunuz olabilir.</span><span class="sxs-lookup"><span data-stu-id="337e8-236">Or you can have multiple consumer groups, each with no more than eight consumers.</span></span>

<span data-ttu-id="337e8-237">Kayıtları Kafka içinde depolanan bir bölüm içinde alınan hello sırayla depolanır.</span><span class="sxs-lookup"><span data-stu-id="337e8-237">Records stored in Kafka are stored in hello order they are received within a partition.</span></span> <span data-ttu-id="337e8-238">tooachieve-sıralı teslim kayıtlar için *bölüm içinde*, hello tüketici örneklerinin sayısını hello bölüm sayısı eşleştiği bir tüketici grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="337e8-238">tooachieve in-ordered delivery for records *within a partition*, create a consumer group where hello number of consumer instances matches hello number of partitions.</span></span> <span data-ttu-id="337e8-239">tooachieve-sıralı teslim kayıtlar için *hello konusu içinde*, yalnızca tek bir tüketici örneği ile bir tüketici grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="337e8-239">tooachieve in-ordered delivery for records *within hello topic*, create a consumer group with only one consumer instance.</span></span>

## <a name="streaming-api"></a><span data-ttu-id="337e8-240">Akış API’si</span><span class="sxs-lookup"><span data-stu-id="337e8-240">Streaming API</span></span>

<span data-ttu-id="337e8-241">API akış hello tooKafka sürüm 0.10.0 eklendi; önceki sürümlerde, Apache Spark veya Storm akış işleme için kullanır.</span><span class="sxs-lookup"><span data-stu-id="337e8-241">hello streaming API was added tooKafka in version 0.10.0; earlier versions rely on Apache Spark or Storm for stream processing.</span></span>

1. <span data-ttu-id="337e8-242">Zaten yapmadıysanız, hello örneklerinden karşıdan [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) tooyour geliştirme ortamı.</span><span class="sxs-lookup"><span data-stu-id="337e8-242">If you haven't already done so, download hello examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) tooyour development environment.</span></span> <span data-ttu-id="337e8-243">Örnek akış Merhaba hello projesi hello kullanmak `streaming` dizin.</span><span class="sxs-lookup"><span data-stu-id="337e8-243">For hello streaming example, use hello project in hello `streaming` directory.</span></span>
   
    <span data-ttu-id="337e8-244">Bu proje yalnızca bir sınıf içeriyor `Stream`, hello kayıtları okur `test` daha önce oluşturulan konu.</span><span class="sxs-lookup"><span data-stu-id="337e8-244">This project contains only one class, `Stream`, which reads records from hello `test` topic created previously.</span></span> <span data-ttu-id="337e8-245">Okuma hello sözcükleri sayar ve adlı her word ve sayısı tooa konu yayar `wordcounts`.</span><span class="sxs-lookup"><span data-stu-id="337e8-245">It counts hello words read, and emits each word and count tooa topic named `wordcounts`.</span></span> <span data-ttu-id="337e8-246">Merhaba `wordcounts` konu bu bölümde daha sonraki bir adımda oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="337e8-246">hello `wordcounts` topic is created in a later step in this section.</span></span>

2. <span data-ttu-id="337e8-247">Merhaba komut satırından geliştirme ortamınızda, dizinleri toohello hello konumunu değiştirmek `Streaming` dizin ve komut toocreate jar paketi aşağıdaki kullanım hello:</span><span class="sxs-lookup"><span data-stu-id="337e8-247">From hello command line in your development environment, change directories toohello location of hello `Streaming` directory, and then use hello following command toocreate a jar package:</span></span>

    ```bash
    mvn clean package
    ```

    <span data-ttu-id="337e8-248">Bu komut, `kafka-streaming-1.0-SNAPSHOT.jar` adlı dosyayı içeren `target` adlı bir dizin oluşturur.</span><span class="sxs-lookup"><span data-stu-id="337e8-248">This command creates a directory named `target`, which contains a file named `kafka-streaming-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="337e8-249">Kullanım hello aşağıdaki komutları toocopy hello `kafka-streaming-1.0-SNAPSHOT.jar` dosya tooyour Hdınsight kümesi:</span><span class="sxs-lookup"><span data-stu-id="337e8-249">Use hello following commands toocopy hello `kafka-streaming-1.0-SNAPSHOT.jar` file tooyour HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-streaming-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-streaming.jar
    ```
   
    <span data-ttu-id="337e8-250">Değiştir **SSHUSER** kümesi ve Değiştir hello SSH kullanıcıyla **CLUSTERNAME** kümenizin hello ada sahip.</span><span class="sxs-lookup"><span data-stu-id="337e8-250">Replace **SSHUSER** with hello SSH user for your cluster, and replace **CLUSTERNAME** with hello name of your cluster.</span></span> <span data-ttu-id="337e8-251">İstendiğinde hello SSH kullanıcı için hello parola girin.</span><span class="sxs-lookup"><span data-stu-id="337e8-251">When prompted enter hello password for hello SSH user.</span></span>

4. <span data-ttu-id="337e8-252">Bir kez hello `scp` komutu hello dosya kopyalama tamamlanmadan, SSH kullanarak toohello kümesine bağlanın ve sonra komut toocreate hello aşağıdaki hello `wordcounts` konu:</span><span class="sxs-lookup"><span data-stu-id="337e8-252">Once hello `scp` command finishes copying hello file, connect toohello cluster using SSH, and then use hello following command toocreate hello `wordcounts` topic:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic wordcounts --zookeeper $KAFKAZKHOSTS
    ```

5. <span data-ttu-id="337e8-253">Ardından, komutu aşağıdaki hello kullanarak işlem akış hello başlatın:</span><span class="sxs-lookup"><span data-stu-id="337e8-253">Next, start hello streaming process by using hello following command:</span></span>
   
    ```bash
    java -jar kafka-streaming.jar $KAFKABROKERS $KAFKAZKHOSTS 2>/dev/null &
    ```
   
    <span data-ttu-id="337e8-254">Bu komut hello arka planda işlem akış hello başlatır.</span><span class="sxs-lookup"><span data-stu-id="337e8-254">This command starts hello streaming process in hello background.</span></span>

6. <span data-ttu-id="337e8-255">Kullanım hello şu komutu toosend iletileri toohello `test` konu.</span><span class="sxs-lookup"><span data-stu-id="337e8-255">Use hello following command toosend messages toohello `test` topic.</span></span> <span data-ttu-id="337e8-256">Bu iletiler örnek akış hello tarafından işlenir:</span><span class="sxs-lookup"><span data-stu-id="337e8-256">These messages are processed by hello streaming example:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS &>/dev/null &
    ```

7. <span data-ttu-id="337e8-257">Kullanım hello toohello yazılan komut tooview hello çıktısı aşağıdaki `wordcounts` konusuna göre işlem akış hello:</span><span class="sxs-lookup"><span data-stu-id="337e8-257">Use hello following command tooview hello output that is written toohello `wordcounts` topic by hello streaming process:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic wordcounts --from-beginning --formatter kafka.tools.DefaultMessageFormatter --property print.key=true --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
    ```
   
    > [!NOTE]
    > <span data-ttu-id="337e8-258">tooview hello veri hello tüketici tooprint hello anahtarı ve hello seri durumdan çıkarıcının toouse hello anahtar ve değer bildirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="337e8-258">tooview hello data, you must tell hello consumer tooprint hello key and hello deserializer toouse for hello key and value.</span></span> <span data-ttu-id="337e8-259">Merhaba anahtar adı hello sözcüktür ve hello sayısı hello anahtar değeri içerir.</span><span class="sxs-lookup"><span data-stu-id="337e8-259">hello key name is hello word, and hello key value contains hello count.</span></span>
   
    <span data-ttu-id="337e8-260">Merhaba, benzer toohello metin aşağıdaki çıktı:</span><span class="sxs-lookup"><span data-stu-id="337e8-260">hello output is similar toohello following text:</span></span>
   
        dwarfs  13635
        ago     13664
        snow    13636
        dwarfs  13636
        ago     13665
        a       13803
        ago     13666
        a       13804
        ago     13667
        ago     13668
        jumped  13640
        jumped  13641
        a       13805
        snow    13637
   
    > [!NOTE]
    > <span data-ttu-id="337e8-261">her zaman bir sözcük karşılaştı Hello sayısını artırır.</span><span class="sxs-lookup"><span data-stu-id="337e8-261">hello count increments each time a word is encountered.</span></span>

7. <span data-ttu-id="337e8-262">Merhaba kullanmak __Ctrl + C__ tooexit hello tüketici sonra hello kullanın `fg` toobring hello akış arka plan görevi geri toohello ön komutu.</span><span class="sxs-lookup"><span data-stu-id="337e8-262">Use hello __Ctrl + C__ tooexit hello consumer, then use hello `fg` command toobring hello streaming background task back toohello foreground.</span></span> <span data-ttu-id="337e8-263">Kullanım __Ctrl + C__ tooexit, ayrıca.</span><span class="sxs-lookup"><span data-stu-id="337e8-263">Use __Ctrl + C__ tooexit it also.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="337e8-264">Merhaba küme silme</span><span class="sxs-lookup"><span data-stu-id="337e8-264">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="337e8-265">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="337e8-265">Troubleshoot</span></span>

<span data-ttu-id="337e8-266">HDInsight kümeleri oluştururken sorun yaşarsanız bkz. [erişim denetimi gereksinimleri](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="337e8-266">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="337e8-267">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="337e8-267">Next steps</span></span>

<span data-ttu-id="337e8-268">Bu belgede, Hdınsight üzerinde Apache Kafka ile çalışmanın temelleri hello öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="337e8-268">In this document, you have learned hello basics of working with Apache Kafka on HDInsight.</span></span> <span data-ttu-id="337e8-269">Kafka ile çalışma hakkında daha fazla toolearn aşağıdaki hello kullan:</span><span class="sxs-lookup"><span data-stu-id="337e8-269">Use hello following toolearn more about working with Kafka:</span></span>

* [<span data-ttu-id="337e8-270">HDInsight üzerinde Kafka ile verilerinizin yüksek kullanılabilirliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="337e8-270">Ensure high availability of your data with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-high-availability.md)
* [<span data-ttu-id="337e8-271">HDInsight üzerinde Kafka ile yönetilen diskleri yapılandırarak ölçeklenebilirliği artırma</span><span class="sxs-lookup"><span data-stu-id="337e8-271">Increase scalability by configuring managed disks with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-scalability.md)
* <span data-ttu-id="337e8-272">kafka.apache.org adresindeki [Apache Kafka belgeleri](http://kafka.apache.org/documentation.html).</span><span class="sxs-lookup"><span data-stu-id="337e8-272">[Apache Kafka documentation](http://kafka.apache.org/documentation.html) at kafka.apache.org.</span></span>
* [<span data-ttu-id="337e8-273">Hdınsight üzerinde MirrorMaker toocreate Kafka bir kopyasını kullan</span><span class="sxs-lookup"><span data-stu-id="337e8-273">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="337e8-274">Apache Storm’u HDInsight üzerinde Kafka ile kullanma</span><span class="sxs-lookup"><span data-stu-id="337e8-274">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="337e8-275">Apache Spark’ı HDInsight üzerinde Kafka ile kullanma</span><span class="sxs-lookup"><span data-stu-id="337e8-275">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="337e8-276">Bir Azure sanal ağı tooKafka Bağlan</span><span class="sxs-lookup"><span data-stu-id="337e8-276">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
