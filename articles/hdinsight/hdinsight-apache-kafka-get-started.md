---
title: "Apache Kafka'yı Kullanmaya Başlama - Azure HDInsight | Microsoft Docs"
description: "Azure HDInsight üzerinde Apache Kafka kümesi oluşturmayı öğrenin. Konu başlığı, abonelik ve tüketici oluşturmayı öğrenin."
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
ms.openlocfilehash: 03e6996f0f44e04978080b3bd267e924f342b7fc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="start-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="ec52e-104">HDInsight üzerinde Apache Kafka'yı (önizleme) kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="ec52e-104">Start with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="ec52e-105">Azure HDInsight üzerinde [Apache Kafka](https://kafka.apache.org) kümesi oluşturmayı ve kullanmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="ec52e-105">Learn how to create and use an [Apache Kafka](https://kafka.apache.org) cluster on Azure HDInsight.</span></span> <span data-ttu-id="ec52e-106">Kafka, HDInsight ile birlikte kullanılabilen, açık kaynaklı bir dağıtılmış akış platformudur.</span><span class="sxs-lookup"><span data-stu-id="ec52e-106">Kafka is an open-source, distributed streaming platform that is available with HDInsight.</span></span> <span data-ttu-id="ec52e-107">Yayımla-abone ol ileti kuyruğuna benzer işlevler sağladığı için genellikle ileti aracısı olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ec52e-107">It is often used as a message broker, as it provides functionality similar to a publish-subscribe message queue.</span></span>

> [!NOTE]
> <span data-ttu-id="ec52e-108">Kafka’nın şu anda HDInsight ile kullanılabilen iki sürümü vardır: 0.9.0 (HDInsight 3.4) ve 0.10.0 (HDInsight 3.5 ve 3.6).</span><span class="sxs-lookup"><span data-stu-id="ec52e-108">There are currently two versions of Kafka available with HDInsight; 0.9.0 (HDInsight 3.4) and 0.10.0 (HDInsight 3.5 and 3.6).</span></span> <span data-ttu-id="ec52e-109">Bu belgedeki adımlarda HDInsight 3.6 üzerinde Kafka kullandığınız kabul edilmiştir.</span><span class="sxs-lookup"><span data-stu-id="ec52e-109">The steps in this document assume that you are using Kafka on HDInsight 3.6.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="create-a-kafka-cluster"></a><span data-ttu-id="ec52e-110">Kafka kümesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="ec52e-110">Create a Kafka cluster</span></span>

<span data-ttu-id="ec52e-111">HDInsight kümesinde Kafka oluşturmak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="ec52e-111">Use the following steps to create a Kafka on HDInsight cluster:</span></span>

1. <span data-ttu-id="ec52e-112">[Azure portalı](https://portal.azure.com)’ndan **+YENİ**, **Akıllı Özellikler ve Analiz** ve ardından **HDInsight**’ı seçin.</span><span class="sxs-lookup"><span data-stu-id="ec52e-112">From the [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>
   
    ![HDInsight kümesi oluşturma](./media/hdinsight-apache-kafka-get-started/create-hdinsight.png)

2. <span data-ttu-id="ec52e-114">**Temel Bilgiler** bölümünden aşağıdaki bilgileri girin:</span><span class="sxs-lookup"><span data-stu-id="ec52e-114">From **Basics**, enter the following information:</span></span>

    * <span data-ttu-id="ec52e-115">**Küme Adı**: HDInsight kümesinin adı.</span><span class="sxs-lookup"><span data-stu-id="ec52e-115">**Cluster Name**: The name of the HDInsight cluster.</span></span>
    * <span data-ttu-id="ec52e-116">**Abonelik**: Kullanılacak abonelik.</span><span class="sxs-lookup"><span data-stu-id="ec52e-116">**Subscription**: Select the subscription to use.</span></span>
    * <span data-ttu-id="ec52e-117">**Küme oturumu kullanıcı adı** ve **Küme oturumu parolası**: HTTPS üzerinden kümeye erişirken kullanılan oturum açma bilgileri.</span><span class="sxs-lookup"><span data-stu-id="ec52e-117">**Cluster login username** and **Cluster login password**: The login when accessing the cluster over HTTPS.</span></span> <span data-ttu-id="ec52e-118">Ambari Web kullanıcı arabirimi veya REST API gibi hizmetlere erişmek için bu kimlik bilgilerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="ec52e-118">You use these credentials to access services such as the Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="ec52e-119">**Güvenli Kabuk (SSH) kullanıcı adı**: SSH üzerinden kümeye erişirken kullanılan oturum açma bilgileri.</span><span class="sxs-lookup"><span data-stu-id="ec52e-119">**Secure Shell (SSH) username**: The login used when accessing the cluster over SSH.</span></span> <span data-ttu-id="ec52e-120">Varsayılan olarak parola, küme oturum açma parolası ile aynıdır.</span><span class="sxs-lookup"><span data-stu-id="ec52e-120">By default the password is the same as the cluster login password.</span></span>
    * <span data-ttu-id="ec52e-121">**Kaynak Grubu**: Kümenin oluşturulduğu kaynak grubu.</span><span class="sxs-lookup"><span data-stu-id="ec52e-121">**Resource Group**: The resource group to create the cluster in.</span></span>
    * <span data-ttu-id="ec52e-122">**Konum**: Kümenin oluşturulacağı Azure bölgesi.</span><span class="sxs-lookup"><span data-stu-id="ec52e-122">**Location**: The Azure region to create the cluster in.</span></span>
   
 ![Abonelik seçme](./media/hdinsight-apache-kafka-get-started/hdinsight-basic-configuration.png)

3. <span data-ttu-id="ec52e-124">**Küme türü**’nü seçin, sonra **Küme yapılandırması**’ndan aşağıdaki değerleri ayarlayın:</span><span class="sxs-lookup"><span data-stu-id="ec52e-124">Select **Cluster type**, and then set the following values from **Cluster configuration**:</span></span>
   
    * <span data-ttu-id="ec52e-125">**Küme Türü**: Kafka</span><span class="sxs-lookup"><span data-stu-id="ec52e-125">**Cluster Type**: Kafka</span></span>

    * <span data-ttu-id="ec52e-126">**Sürüm**: Kafka 0.10.0 (HDI 3.6)</span><span class="sxs-lookup"><span data-stu-id="ec52e-126">**Version**: Kafka 0.10.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="ec52e-127">**Küme Katmanı**: Standart</span><span class="sxs-lookup"><span data-stu-id="ec52e-127">**Cluster Tier**: Standard</span></span>
     
 <span data-ttu-id="ec52e-128">Son olarak, **Seç** düğmesini kullanarak ayarları kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ec52e-128">Finally, use the **Select** button to save settings.</span></span>
     
 ![Küme türü seçme](./media/hdinsight-apache-kafka-get-started/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="ec52e-130">Küme türünü seçtikten sonra __Seç__ düğmesini kullanarak küme türünü ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ec52e-130">After selecting the cluster type, use the __Select__ button to set the cluster type.</span></span> <span data-ttu-id="ec52e-131">Ardından, __İleri__ düğmesini kullanarak temel yapılandırmayı tamamlayın.</span><span class="sxs-lookup"><span data-stu-id="ec52e-131">Next, use the __Next__ button to finish basic configuration.</span></span>

5. <span data-ttu-id="ec52e-132">**Depolama**’dan bir depolama hesabı seçin veya oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ec52e-132">From **Storage**, select or create a Storage account.</span></span> <span data-ttu-id="ec52e-133">Bu belgedeki adımlar için diğer alanları varsayılan değerlerinde bırakın.</span><span class="sxs-lookup"><span data-stu-id="ec52e-133">For the steps in this document, leave the other fields at the default values.</span></span> <span data-ttu-id="ec52e-134">__İleri__ düğmesini kullanarak depolama yapılandırmasını kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ec52e-134">Use the __Next__ button to save storage configuration.</span></span>

    ![HDInsight depolama hesabı ayarlarını belirleme](./media/hdinsight-apache-kafka-get-started/set-hdinsight-storage-account.png)

6. <span data-ttu-id="ec52e-136">Devam etmek için __Uygulamalar (isteğe bağlı)__ bölümünden __İleri__'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="ec52e-136">From __Applications (optional)__, select __Next__ to continue.</span></span> <span data-ttu-id="ec52e-137">Bu örnek için uygulama gerekmez.</span><span class="sxs-lookup"><span data-stu-id="ec52e-137">No applications are required for this example.</span></span>

7. <span data-ttu-id="ec52e-138">Devam etmek için __Küme boyutu__’ndan __İleri__'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="ec52e-138">From __Cluster size__, select __Next__ to continue.</span></span>

    > [!WARNING]
    > <span data-ttu-id="ec52e-139">HDInsight üzerinde Kafka'yı kullanabilmeniz için kümenizin en az üç çalışan düğümü içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ec52e-139">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span>

    ![Kafka kümesi boyutunu ayarlama](./media/hdinsight-apache-kafka-get-started/kafka-cluster-size.png)

    > [!NOTE]
    > <span data-ttu-id="ec52e-141">**Çalışan düğümü başına disk sayısı** girdisi, HDInsight üzerinde Kafka'nın ölçeklenebilirliğini denetler.</span><span class="sxs-lookup"><span data-stu-id="ec52e-141">The **disks per worker node** entry controls the scalability of Kafka on HDInsight.</span></span> <span data-ttu-id="ec52e-142">Daha fazla bilgi için bkz. [HDInsight üzerinde Kafka'nın depolama alanını ve ölçeklenebilirliğini yapılandırma](hdinsight-apache-kafka-scalability.md).</span><span class="sxs-lookup"><span data-stu-id="ec52e-142">For more information, see [Configure storage and scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span></span>

8. <span data-ttu-id="ec52e-143">Devam etmek için __Gelişmiş ayarlar__’dan __İleri__'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="ec52e-143">From __Advanced settings__, select __Next__ to continue.</span></span>

9. <span data-ttu-id="ec52e-144">**Özet**’ten kümenin yapılandırmasını gözden geçirin.</span><span class="sxs-lookup"><span data-stu-id="ec52e-144">From the **Summary**, review the configuration for the cluster.</span></span> <span data-ttu-id="ec52e-145">Yanlış olan ayarları değiştirmek için __Düzenle__ bağlantılarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="ec52e-145">Use the __Edit__ links to change any settings that are incorrect.</span></span> <span data-ttu-id="ec52e-146">Son olarak, __Oluştur__ düğmesini kullanarak kümeyi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ec52e-146">Finally, use the__Create__ button to create the cluster.</span></span>
   
    ![Küme yapılandırma özeti](./media/hdinsight-apache-kafka-get-started/hdinsight-configuration-summary.png)
   
    > [!NOTE]
    > <span data-ttu-id="ec52e-148">Kümenin oluşturulması 20 dakika sürebilir.</span><span class="sxs-lookup"><span data-stu-id="ec52e-148">It can take up to 20 minutes to create the cluster.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="ec52e-149">Kümeye bağlanma</span><span class="sxs-lookup"><span data-stu-id="ec52e-149">Connect to the cluster</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ec52e-150">Aşağıdaki adımları gerçekleştirirken bir SSH istemcisi kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ec52e-150">When performing the following steps, you must use an SSH client.</span></span> <span data-ttu-id="ec52e-151">Daha fazla bilgi için [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md) belgesine bakın.</span><span class="sxs-lookup"><span data-stu-id="ec52e-151">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

<span data-ttu-id="ec52e-152">Kümeye bağlanmak için istemcinizde SSH kullanın:</span><span class="sxs-lookup"><span data-stu-id="ec52e-152">From your client, use SSH to connect to the cluster:</span></span>

```ssh SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net```

<span data-ttu-id="ec52e-153">**SSHUSER** ifadesini küme oluşturma sırasında sağladığınız SSH kullanıcı adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ec52e-153">Replace **SSHUSER** with the SSH username you provided during cluster creation.</span></span> <span data-ttu-id="ec52e-154">**CLUSTERNAME** değerini kümenin adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ec52e-154">Replace **CLUSTERNAME** with the name of the cluster.</span></span>

<span data-ttu-id="ec52e-155">İstendiğinde, SSH hesabı için kullanılan parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="ec52e-155">When prompted, enter the password you used for the SSH account.</span></span>

<span data-ttu-id="ec52e-156">Bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="ec52e-156">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="ec52e-157"><a id="getkafkainfo"></a>Zookeeper ve Aracı konak bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="ec52e-157"><a id="getkafkainfo"></a>Get the Zookeeper and Broker host information</span></span>

<span data-ttu-id="ec52e-158">Kafka ile çalışırken konak değerlerini bilmeniz gerekir; *Zookeeper* konakları ve *Aracı* konakları.</span><span class="sxs-lookup"><span data-stu-id="ec52e-158">When working with Kafka, you must know two host values; the *Zookeeper* hosts and the *Broker* hosts.</span></span> <span data-ttu-id="ec52e-159">Bu konaklar Kafka API’si ve Kafka ile gönderilen yardımcı programların birçoğu ile birlikte kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ec52e-159">These hosts are used with the Kafka API and many of the utilities that ship with Kafka.</span></span>

<span data-ttu-id="ec52e-160">Konak bilgilerini içeren ortam değişkenlerini oluşturmak için aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="ec52e-160">Use the following steps to create environment variables that contain the host information.</span></span> <span data-ttu-id="ec52e-161">Bu ortam değişkenleri bu belgedeki adımlarda kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ec52e-161">These environment variables are used in the steps in this document.</span></span>

1. <span data-ttu-id="ec52e-162">Küme ile SSH bağlantısından aşağıdaki komutu kullanarak `jq` yardımcı programını yükleyin.</span><span class="sxs-lookup"><span data-stu-id="ec52e-162">From an SSH connection to the cluster, use the following command to install the `jq` utility.</span></span> <span data-ttu-id="ec52e-163">Bu yardımcı program JSON belgelerini ayrıştırmak için kullanılır ve aracı konak bilgilerini almak için yararlıdır:</span><span class="sxs-lookup"><span data-stu-id="ec52e-163">This utility is used to parse JSON documents, and is useful in retrieving the broker host information:</span></span>
   
    ```bash
    sudo apt -y install jq
    ```

2. <span data-ttu-id="ec52e-164">Ambari’den alınan bilgilerle ortam değişkenlerini ayarlamak için aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="ec52e-164">To set the environment variables with information retrieved from Ambari, use the following commands:</span></span>

    ```bash
    CLUSTERNAME='your cluster name'
    PASSWORD='your cluster password'
    export KAFKAZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`

    export KAFKABROKERS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`

    echo '$KAFKAZKHOSTS='$KAFKAZKHOSTS
    echo '$KAFKABROKERS='$KAFKABROKERS
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="ec52e-165">`CLUSTERNAME=` değerini Kafka kümesinin adı olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ec52e-165">Set `CLUSTERNAME=` to the name of the Kafka cluster.</span></span> <span data-ttu-id="ec52e-166">`PASSWORD=` değerini kümeyi oluştururken kullandığınız oturum açma (yönetici) parolası olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ec52e-166">Set `PASSWORD=` to the login (admin) password you used when creating the cluster.</span></span>

    <span data-ttu-id="ec52e-167">Aşağıdaki metin `$KAFKAZKHOSTS` içeriğinin bir örneğidir:</span><span class="sxs-lookup"><span data-stu-id="ec52e-167">The following text is an example of the contents of `$KAFKAZKHOSTS`:</span></span>
   
    `zk0-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk2-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181`
   
    <span data-ttu-id="ec52e-168">Aşağıdaki metin `$KAFKABROKERS` içeriğinin bir örneğidir:</span><span class="sxs-lookup"><span data-stu-id="ec52e-168">The following text is an example of the contents of `$KAFKABROKERS`:</span></span>
   
    `wn1-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092,wn0-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092`

    > [!NOTE]
    > <span data-ttu-id="ec52e-169">`cut` komutu, konak listesini iki konak girdisine düşürmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ec52e-169">The `cut` command is used to trim the list of hosts to two host entries.</span></span> <span data-ttu-id="ec52e-170">Kafka tüketicisi veya üreticisi oluştururken konakların tam listesini sağlamanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="ec52e-170">You do not need to provide the full list of hosts when creating a Kafka consumer or producer.</span></span>
   
    > [!WARNING]
    > <span data-ttu-id="ec52e-171">Bu oturumdan döndürülen bilgileri her zaman doğru olarak kabul etmeyin.</span><span class="sxs-lookup"><span data-stu-id="ec52e-171">Do not rely on the information returned from this session to always be accurate.</span></span> <span data-ttu-id="ec52e-172">Kümeyi ölçeklendirirseniz yeni aracılar eklenir veya kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="ec52e-172">If you scale the cluster, new brokers are added or removed.</span></span> <span data-ttu-id="ec52e-173">Bir hata oluşur ve bir düğüm değiştirilirse, düğümün konak adı değişebilir.</span><span class="sxs-lookup"><span data-stu-id="ec52e-173">If a failure occurs and a node is replaced, the host name for the node may change.</span></span>
    >
    > <span data-ttu-id="ec52e-174">Geçerli bilgilere sahip olduğunuzdan emin olmak için, kullanmadan hemen önce Zookeeper ve aracı konakların bilgilerini almanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ec52e-174">You should retrieve the Zookeeper and broker hosts information shortly before you use it to ensure you have valid information.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="ec52e-175">Konu başlığı oluşturma</span><span class="sxs-lookup"><span data-stu-id="ec52e-175">Create a topic</span></span>

<span data-ttu-id="ec52e-176">Kafka, veri akışlarını *topics* (konu başlıkları) adlı kategorilerde depolar.</span><span class="sxs-lookup"><span data-stu-id="ec52e-176">Kafka stores streams of data in categories called *topics*.</span></span> <span data-ttu-id="ec52e-177">Kafka ile birlikte verilen betiği kullanarak, bir küme baş düğümüne yönelik SSH bağlantısından konu başlığı oluşturun:</span><span class="sxs-lookup"><span data-stu-id="ec52e-177">From An SSH connection to a cluster headnode, use a script provided with Kafka to create a topic:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic test --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="ec52e-178">Bu komut, `$KAFKAZKHOSTS` içinde depolanan konak bilgilerini kullanarak Zookeeper’a bağlanır ve ardından **test** adlı Kafka konu başlığını oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ec52e-178">This command connects to Zookeeper using the host information stored in `$KAFKAZKHOSTS`, and then create Kafka topic named **test**.</span></span> <span data-ttu-id="ec52e-179">Konu başlıklarını listelemek üzere aşağıdaki betiği kullanarak, konu başlığının oluşturulduğunu doğrulayabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="ec52e-179">You can verify that the topic was created by using the following script to list topics:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="ec52e-180">Bu komut, **test** konu başlıklarını içeren Kafka konu başlıklarını listeler.</span><span class="sxs-lookup"><span data-stu-id="ec52e-180">The output of this command lists Kafka topics, which contains the **test** topic.</span></span>

## <a name="produce-and-consume-records"></a><span data-ttu-id="ec52e-181">Kayıt oluşturma ve kullanma</span><span class="sxs-lookup"><span data-stu-id="ec52e-181">Produce and consume records</span></span>

<span data-ttu-id="ec52e-182">Kafka, konu başlıklarında *records* (kayıtlar) depolar.</span><span class="sxs-lookup"><span data-stu-id="ec52e-182">Kafka stores *records* in topics.</span></span> <span data-ttu-id="ec52e-183">Kayıtlar, *Üreticiler* tarafından oluşturulur ve *tüketiciler* tarafından kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ec52e-183">Records are produced by *producers*, and consumed by *consumers*.</span></span> <span data-ttu-id="ec52e-184">Üreticiler, kayıtları Kafka *aracılarından* alır.</span><span class="sxs-lookup"><span data-stu-id="ec52e-184">Producers retrieve records from Kafka *brokers*.</span></span> <span data-ttu-id="ec52e-185">HDInsight kümenizdeki her çalışan düğümü bir Kafka aracısıdır.</span><span class="sxs-lookup"><span data-stu-id="ec52e-185">Each worker node in your HDInsight cluster is a Kafka broker.</span></span>

<span data-ttu-id="ec52e-186">Daha önce oluşturduğunuz test konu başlığında kayıt depolamak ve ardından bir tüketici kullanarak bunları okumak için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="ec52e-186">Use the following steps to store records into the test topic you created earlier, and then read them using a consumer:</span></span>

1. <span data-ttu-id="ec52e-187">SSH oturumundan, Kafka ile birlikte sağlanan bir betik kullanarak kayıtları konu başlığına yazın:</span><span class="sxs-lookup"><span data-stu-id="ec52e-187">From the SSH session, use a script provided with Kafka to write records to the topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $KAFKABROKERS --topic test
    ```
   
    <span data-ttu-id="ec52e-188">Bu komuttan sonra isteme geri döndürülmezsiniz.</span><span class="sxs-lookup"><span data-stu-id="ec52e-188">You are not returned to the prompt after this command.</span></span> <span data-ttu-id="ec52e-189">Bunun yerine, birkaç metin iletisi yazın ve ardından **Ctrl + C** tuşlarını kullanarak, konu başlığına göndermeyi durdurun.</span><span class="sxs-lookup"><span data-stu-id="ec52e-189">Instead, type a few text messages and then use **Ctrl + C** to stop sending to the topic.</span></span> <span data-ttu-id="ec52e-190">Her satır ayrı bir kayıt olarak gönderilir.</span><span class="sxs-lookup"><span data-stu-id="ec52e-190">Each line is sent as a separate record.</span></span>

2. <span data-ttu-id="ec52e-191">Konu başlığından kayıt okumak için, Kafka ile birlikte sağlanan bir betik kullanın:</span><span class="sxs-lookup"><span data-stu-id="ec52e-191">Use a script provided with Kafka to read records from the topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic test --from-beginning
    ```
   
    <span data-ttu-id="ec52e-192">Bu komutla, kayıtlar konu başlığından alınır ve görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="ec52e-192">This command retrieves the records from the topic and displays them.</span></span> <span data-ttu-id="ec52e-193">`--from-beginning` kullanılması, tüketiciye akışın başından başlamasını söyler, böylece tüm kayıtlar alınır.</span><span class="sxs-lookup"><span data-stu-id="ec52e-193">Using `--from-beginning` tells the consumer to start from the beginning of the stream, so all records are retrieved.</span></span>

3. <span data-ttu-id="ec52e-194">Tüketiciyi durdurmak için __Ctrl + C__ tuşlarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="ec52e-194">Use __Ctrl + C__ to stop the consumer.</span></span>

## <a name="producer-and-consumer-api"></a><span data-ttu-id="ec52e-195">Üretici ve tüketici API’si</span><span class="sxs-lookup"><span data-stu-id="ec52e-195">Producer and consumer API</span></span>

<span data-ttu-id="ec52e-196">[Kafka API’lerin,](http://kafka.apache.org/documentation#api) kullanarak, kayıtları programlama yoluyla da üretebilir ve kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ec52e-196">You can also programmatically produce and consume records using the [Kafka APIs](http://kafka.apache.org/documentation#api).</span></span> <span data-ttu-id="ec52e-197">Java üreticisi ve tüketicisi oluşturmak için geliştirme ortamınızdan aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="ec52e-197">To build a Java producer and consumer, use the following steps from your development environment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ec52e-198">Aşağıdaki bileşenlerin geliştirme ortamınızda yüklü olması gerekir:</span><span class="sxs-lookup"><span data-stu-id="ec52e-198">You must have the following components installed in your development environment:</span></span>
>
> * <span data-ttu-id="ec52e-199">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) veya OpenJDK gibi eşdeğeri.</span><span class="sxs-lookup"><span data-stu-id="ec52e-199">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or an equivalent, such as OpenJDK.</span></span>
>
> * [<span data-ttu-id="ec52e-200">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="ec52e-200">Apache Maven</span></span>](http://maven.apache.org/)
>
> * <span data-ttu-id="ec52e-201">Bir SSH istemcisi ve `scp` komutu.</span><span class="sxs-lookup"><span data-stu-id="ec52e-201">An SSH client and the `scp` command.</span></span> <span data-ttu-id="ec52e-202">Daha fazla bilgi için [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md) belgesine bakın.</span><span class="sxs-lookup"><span data-stu-id="ec52e-202">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

1. <span data-ttu-id="ec52e-203">Örnekleri [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) sayfasından indirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ec52e-203">Download the examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span></span> <span data-ttu-id="ec52e-204">Üretici/tüketici örneği için `Producer-Consumer` dizinindeki projeyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="ec52e-204">For the producer/consumer example, use the project in the `Producer-Consumer` directory.</span></span> <span data-ttu-id="ec52e-205">Bu örnek aşağıdaki sınıfları içerir:</span><span class="sxs-lookup"><span data-stu-id="ec52e-205">This example contains the following classes:</span></span>
   
    * <span data-ttu-id="ec52e-206">**Çalıştır** - tüketiciyi veya üreticiyi başlatır.</span><span class="sxs-lookup"><span data-stu-id="ec52e-206">**Run** - starts either the consumer or producer.</span></span>

    * <span data-ttu-id="ec52e-207">**Producer** (Üretici)- konu başlığında 1.000.000 kayıt depolar.</span><span class="sxs-lookup"><span data-stu-id="ec52e-207">**Producer** - stores 1,000,000 records to the topic.</span></span>

    * <span data-ttu-id="ec52e-208">**Consumer** (Tüketici) - konu başlığındaki kayıtları okur.</span><span class="sxs-lookup"><span data-stu-id="ec52e-208">**Consumer** - reads records from the topic.</span></span>

2. <span data-ttu-id="ec52e-209">Bir jar paketi oluşturmak için dizinleri `Producer-Consumer` dizininin konumuna geçirin ve aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="ec52e-209">To create a jar package, change directories to the location of the `Producer-Consumer` directory and use the following command:</span></span>

    ```
    mvn clean package
    ```

    <span data-ttu-id="ec52e-210">Bu komut, `kafka-producer-consumer-1.0-SNAPSHOT.jar` adlı dosyayı içeren `target` adlı bir dizin oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ec52e-210">This command creates a directory named `target`, that contains a file named `kafka-producer-consumer-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="ec52e-211">`kafka-producer-consumer-1.0-SNAPSHOT.jar` dosyasını HDInsight kümenize kopyalamak için aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="ec52e-211">Use the following commands to copy the `kafka-producer-consumer-1.0-SNAPSHOT.jar` file to your HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-producer-consumer-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-producer-consumer.jar
    ```
   
    <span data-ttu-id="ec52e-212">**SSHUSER** değerini kümenizin SSH kullanıcısı ile, **CLUSTERNAME** değerini kümenizin adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ec52e-212">Replace **SSHUSER** with the SSH user for your cluster, and replace **CLUSTERNAME** with the name of your cluster.</span></span> <span data-ttu-id="ec52e-213">İstendiğinde, SSH kullanıcısının parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="ec52e-213">When prompted enter the password for the SSH user.</span></span>

4. <span data-ttu-id="ec52e-214">`scp` komutuyla dosyayı kopyalama işlemi tamamlandığında SSH kullanarak kümeye bağlanın.</span><span class="sxs-lookup"><span data-stu-id="ec52e-214">Once the `scp` command finishes copying the file, connect to the cluster using SSH.</span></span> <span data-ttu-id="ec52e-215">Test konu başlığına kayıt yazmak için şu komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="ec52e-215">Use the following command to write records to the test topic:</span></span>

    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS
    ```

5. <span data-ttu-id="ec52e-216">İşlem tamamlandıktan sonra, konu başlığından okumak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="ec52e-216">Once the process has finished, use the following command to read from the topic:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS
    ```
   
    <span data-ttu-id="ec52e-217">Okunan kayıtlar, kayıt sayısıyla birlikte gösterilir.</span><span class="sxs-lookup"><span data-stu-id="ec52e-217">The records read, along with a count of records, is displayed.</span></span> <span data-ttu-id="ec52e-218">Daha önceki bir adımda, betik kullanarak konu başlığına çok sayıda kayıt gönderdiğiniz için 1.000.000’dan fazla kaydın günlüğe kaydedildiğini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ec52e-218">You may see a few more than 1,000,000 logged as you sent several records to the topic using a script in an earlier step.</span></span>

6. <span data-ttu-id="ec52e-219">Tüketiciden çıkış yapmak için __Ctrl + C__ tuşlarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="ec52e-219">Use __Ctrl + C__ to exit the consumer.</span></span>

### <a name="multiple-consumers"></a><span data-ttu-id="ec52e-220">Birden çok tüketici</span><span class="sxs-lookup"><span data-stu-id="ec52e-220">Multiple consumers</span></span>

<span data-ttu-id="ec52e-221">Kafka tüketicileri kayıtları okurken bir tüketici grubu kullanır.</span><span class="sxs-lookup"><span data-stu-id="ec52e-221">Kafka consumers use a consumer group when reading records.</span></span> <span data-ttu-id="ec52e-222">Birden çok tüketiciyle aynı grubun kullanılması, konu başlığından yük dengeli okuma yapılmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="ec52e-222">Using the same group with multiple consumers results in load balanced reads from a topic.</span></span> <span data-ttu-id="ec52e-223">Gruptaki her bir tüketici, kayıtların bir kısmını alır.</span><span class="sxs-lookup"><span data-stu-id="ec52e-223">Each consumer in the group receives a portion of the records.</span></span> <span data-ttu-id="ec52e-224">Bu işlemi uygulamada görmek için aşağıdaki adımları kullanın:</span><span class="sxs-lookup"><span data-stu-id="ec52e-224">To see this process in action, use the following steps:</span></span>

1. <span data-ttu-id="ec52e-225">Kümede yeni bir SSH oturumu açın, böylece ikisine birden sahip olursunuz.</span><span class="sxs-lookup"><span data-stu-id="ec52e-225">Open a new SSH session to the cluster, so that you have two of them.</span></span> <span data-ttu-id="ec52e-226">Her oturumda aynı tüketici grubu kimliğine sahip bir tüketici başlatmak için aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="ec52e-226">In each session, use the following to start a consumer with the same consumer group ID:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS mygroup
    ```

    <span data-ttu-id="ec52e-227">Bu komut, `mygroup` grup kimliğini kullanarak bir tüketici başlatır.</span><span class="sxs-lookup"><span data-stu-id="ec52e-227">This command starts a consumer using the group ID `mygroup`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ec52e-228">Bu SSH oturumuna yönelik `$KAFKABROKERS` ayarını yapmak için [Zookeeper ve Aracı konak bilgilerini alma](#getkafkainfo) bölümündeki komutları kullanın.</span><span class="sxs-lookup"><span data-stu-id="ec52e-228">Use the commands in the [Get the Zookeeper and Broker host information](#getkafkainfo) section to set `$KAFKABROKERS` for this SSH session.</span></span>

2. <span data-ttu-id="ec52e-229">Her oturumun konu başlığından aldığı kayıtları saymasını izleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ec52e-229">Watch as each session counts the records it receives from the topic.</span></span> <span data-ttu-id="ec52e-230">Her iki oturumun toplamı, daha önce bir tüketiciden aldığınız sayıyla aynı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ec52e-230">The total of both sessions should be the same as you received previously from one consumer.</span></span>

<span data-ttu-id="ec52e-231">Aynı gruptaki istemcilerin tüketimi, konu başlığının bölümleri aracılığıyla işlenir.</span><span class="sxs-lookup"><span data-stu-id="ec52e-231">Consumption by clients within the same group is handled through the partitions for the topic.</span></span> <span data-ttu-id="ec52e-232">Daha önce oluşturulan `test` konu başlığında sekiz bölüm vardır.</span><span class="sxs-lookup"><span data-stu-id="ec52e-232">For the `test` topic created earlier, it has eight partitions.</span></span> <span data-ttu-id="ec52e-233">Sekiz SSH oturumu açıp tüm oturumlarda bir tüketici başlatırsanız her tüketici, konu başlığının tek bir bölümündeki kayıtları okur.</span><span class="sxs-lookup"><span data-stu-id="ec52e-233">If you open eight SSH sessions and launch a consumer in all sessions, each consumer reads records from a single partition for the topic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ec52e-234">Bir tüketici grubunda bölümden daha fazla tüketici örneği olamaz.</span><span class="sxs-lookup"><span data-stu-id="ec52e-234">There cannot be more consumer instances in a consumer group than partitions.</span></span> <span data-ttu-id="ec52e-235">Bu örnekte, konu başlığındaki bölüm sayısı sekiz olduğu için bir tüketici grubu en fazla bu sayıda tüketici içerebilir.</span><span class="sxs-lookup"><span data-stu-id="ec52e-235">In this example, one consumer group can contain up to eight consumers since that is the number of partitions in the topic.</span></span> <span data-ttu-id="ec52e-236">Ya da her biri en fazla sekiz tüketici içeren birden fazla tüketici grubunuz olabilir.</span><span class="sxs-lookup"><span data-stu-id="ec52e-236">Or you can have multiple consumer groups, each with no more than eight consumers.</span></span>

<span data-ttu-id="ec52e-237">Kafka’ya depolanan kayıtlar bir bölümde alındıkları sırayla depolanır.</span><span class="sxs-lookup"><span data-stu-id="ec52e-237">Records stored in Kafka are stored in the order they are received within a partition.</span></span> <span data-ttu-id="ec52e-238">*Bir bölüm* içindeki kayıtlar için sıralı teslim sağlamak üzere, tüketici örneklerinin bölüm sayısıyla eşleştiği bir tüketici grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ec52e-238">To achieve in-ordered delivery for records *within a partition*, create a consumer group where the number of consumer instances matches the number of partitions.</span></span> <span data-ttu-id="ec52e-239">*Konu başlığı içindeki* kayıtların sıralı teslim edilmesini sağlayabilmek için, yalnızca bir tüketici örneği içeren bir tüketici grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ec52e-239">To achieve in-ordered delivery for records *within the topic*, create a consumer group with only one consumer instance.</span></span>

## <a name="streaming-api"></a><span data-ttu-id="ec52e-240">Akış API’si</span><span class="sxs-lookup"><span data-stu-id="ec52e-240">Streaming API</span></span>

<span data-ttu-id="ec52e-241">Akış API’si Kafka’ya sürüm 0.10.0’da eklenmiştir; önceki sürümler, akış işleme için Apache Spark veya Storm kullanır.</span><span class="sxs-lookup"><span data-stu-id="ec52e-241">The streaming API was added to Kafka in version 0.10.0; earlier versions rely on Apache Spark or Storm for stream processing.</span></span>

1. <span data-ttu-id="ec52e-242">Henüz yapmadıysanız, örnekleri [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) sayfasından geliştirme ortamınıza indirin.</span><span class="sxs-lookup"><span data-stu-id="ec52e-242">If you haven't already done so, download the examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) to your development environment.</span></span> <span data-ttu-id="ec52e-243">Akış örneği için `streaming` dizinindeki projeyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="ec52e-243">For the streaming example, use the project in the `streaming` directory.</span></span>
   
    <span data-ttu-id="ec52e-244">Bu proje yalnızca, daha önce `test` konu başlığından kayıtları okuyan `Stream` adlı sınıfı içerir.</span><span class="sxs-lookup"><span data-stu-id="ec52e-244">This project contains only one class, `Stream`, which reads records from the `test` topic created previously.</span></span> <span data-ttu-id="ec52e-245">Okunan sözcükleri sayar ve her sözcük ile sayıyı `wordcounts` adlı konu başlığına iletir.</span><span class="sxs-lookup"><span data-stu-id="ec52e-245">It counts the words read, and emits each word and count to a topic named `wordcounts`.</span></span> <span data-ttu-id="ec52e-246">`wordcounts` konu başlığı, bu bölümün sonraki bir adımında oluşturulur.</span><span class="sxs-lookup"><span data-stu-id="ec52e-246">The `wordcounts` topic is created in a later step in this section.</span></span>

2. <span data-ttu-id="ec52e-247">Geliştirme ortamınızdaki komut satırından, dizinleri `Streaming` dizininin konumuna geçirin ve ardından aşağıdaki komutu kullanarak bir jar paketi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="ec52e-247">From the command line in your development environment, change directories to the location of the `Streaming` directory, and then use the following command to create a jar package:</span></span>

    ```bash
    mvn clean package
    ```

    <span data-ttu-id="ec52e-248">Bu komut, `kafka-streaming-1.0-SNAPSHOT.jar` adlı dosyayı içeren `target` adlı bir dizin oluşturur.</span><span class="sxs-lookup"><span data-stu-id="ec52e-248">This command creates a directory named `target`, which contains a file named `kafka-streaming-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="ec52e-249">`kafka-streaming-1.0-SNAPSHOT.jar` dosyasını HDInsight kümenize kopyalamak için aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="ec52e-249">Use the following commands to copy the `kafka-streaming-1.0-SNAPSHOT.jar` file to your HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-streaming-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-streaming.jar
    ```
   
    <span data-ttu-id="ec52e-250">**SSHUSER** değerini kümenizin SSH kullanıcısı ile, **CLUSTERNAME** değerini kümenizin adıyla değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ec52e-250">Replace **SSHUSER** with the SSH user for your cluster, and replace **CLUSTERNAME** with the name of your cluster.</span></span> <span data-ttu-id="ec52e-251">İstendiğinde, SSH kullanıcısının parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="ec52e-251">When prompted enter the password for the SSH user.</span></span>

4. <span data-ttu-id="ec52e-252">`scp` komutu dosya kopyalamayı tamamladıktan sonra, SSH kullanarak kümeye bağlanın ve ardından aşağıdaki komutu kullanarak `wordcounts` konu başlığını oluşturun:</span><span class="sxs-lookup"><span data-stu-id="ec52e-252">Once the `scp` command finishes copying the file, connect to the cluster using SSH, and then use the following command to create the `wordcounts` topic:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic wordcounts --zookeeper $KAFKAZKHOSTS
    ```

5. <span data-ttu-id="ec52e-253">Ardından, aşağıdaki komutu kullanarak akış işlemini başlatın:</span><span class="sxs-lookup"><span data-stu-id="ec52e-253">Next, start the streaming process by using the following command:</span></span>
   
    ```bash
    java -jar kafka-streaming.jar $KAFKABROKERS $KAFKAZKHOSTS 2>/dev/null &
    ```
   
    <span data-ttu-id="ec52e-254">Bu komut, arka planda akış işlemini başlatır.</span><span class="sxs-lookup"><span data-stu-id="ec52e-254">This command starts the streaming process in the background.</span></span>

6. <span data-ttu-id="ec52e-255">`test` konu başlığına ileti göndermek için aşağıdaki komutu kullanın.</span><span class="sxs-lookup"><span data-stu-id="ec52e-255">Use the following command to send messages to the `test` topic.</span></span> <span data-ttu-id="ec52e-256">Bu iletiler akış örneği tarafından işlenir:</span><span class="sxs-lookup"><span data-stu-id="ec52e-256">These messages are processed by the streaming example:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS &>/dev/null &
    ```

7. <span data-ttu-id="ec52e-257">Akış işlemi tarafından `wordcounts` konu başlığına yazılan çıktıyı görüntülemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="ec52e-257">Use the following command to view the output that is written to the `wordcounts` topic by the streaming process:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic wordcounts --from-beginning --formatter kafka.tools.DefaultMessageFormatter --property print.key=true --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
    ```
   
    > [!NOTE]
    > <span data-ttu-id="ec52e-258">Verileri görüntülemek için, tüketiciye anahtar ve değer için kullanılacak anahtarı ve seri durumdan çıkarma aracını yazdırmasını söylemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ec52e-258">To view the data, you must tell the consumer to print the key and the deserializer to use for the key and value.</span></span> <span data-ttu-id="ec52e-259">Anahtar adı sözcüktür ve anahtar değeri sayıyı içerir.</span><span class="sxs-lookup"><span data-stu-id="ec52e-259">The key name is the word, and the key value contains the count.</span></span>
   
    <span data-ttu-id="ec52e-260">Çıktı aşağıdaki metne benzer:</span><span class="sxs-lookup"><span data-stu-id="ec52e-260">The output is similar to the following text:</span></span>
   
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
    > <span data-ttu-id="ec52e-261">Bir sözcükle karşılaşılan her durumda sayı artar.</span><span class="sxs-lookup"><span data-stu-id="ec52e-261">The count increments each time a word is encountered.</span></span>

7. <span data-ttu-id="ec52e-262">Tüketiciden çıkmak için __Ctrl + C__ tuşlarını kullanın, ardından `fg` komutunu kullanarak akış arka plan görevini ön plana geri getirin.</span><span class="sxs-lookup"><span data-stu-id="ec52e-262">Use the __Ctrl + C__ to exit the consumer, then use the `fg` command to bring the streaming background task back to the foreground.</span></span> <span data-ttu-id="ec52e-263">Çıkış yapmak için de __Ctrl + C__ tuşlarını kullanın.</span><span class="sxs-lookup"><span data-stu-id="ec52e-263">Use __Ctrl + C__ to exit it also.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="ec52e-264">Küme silme</span><span class="sxs-lookup"><span data-stu-id="ec52e-264">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="ec52e-265">Sorun giderme</span><span class="sxs-lookup"><span data-stu-id="ec52e-265">Troubleshoot</span></span>

<span data-ttu-id="ec52e-266">HDInsight kümeleri oluştururken sorun yaşarsanız bkz. [erişim denetimi gereksinimleri](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="ec52e-266">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec52e-267">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ec52e-267">Next steps</span></span>

<span data-ttu-id="ec52e-268">Bu belgede, HDInsight üzerinde Apache Kafka ile çalışmanın temel bilgilerini öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="ec52e-268">In this document, you have learned the basics of working with Apache Kafka on HDInsight.</span></span> <span data-ttu-id="ec52e-269">Kafka ile çalışma hakkında daha fazla bilgi için aşağıdakileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="ec52e-269">Use the following to learn more about working with Kafka:</span></span>

* [<span data-ttu-id="ec52e-270">HDInsight üzerinde Kafka ile verilerinizin yüksek kullanılabilirliğini sağlama</span><span class="sxs-lookup"><span data-stu-id="ec52e-270">Ensure high availability of your data with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-high-availability.md)
* [<span data-ttu-id="ec52e-271">HDInsight üzerinde Kafka ile yönetilen diskleri yapılandırarak ölçeklenebilirliği artırma</span><span class="sxs-lookup"><span data-stu-id="ec52e-271">Increase scalability by configuring managed disks with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-scalability.md)
* <span data-ttu-id="ec52e-272">kafka.apache.org adresindeki [Apache Kafka belgeleri](http://kafka.apache.org/documentation.html).</span><span class="sxs-lookup"><span data-stu-id="ec52e-272">[Apache Kafka documentation](http://kafka.apache.org/documentation.html) at kafka.apache.org.</span></span>
* [<span data-ttu-id="ec52e-273">MirrorMaker kullanarak HDInsight üzerinde Kafka kopyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="ec52e-273">Use MirrorMaker to create a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="ec52e-274">Apache Storm’u HDInsight üzerinde Kafka ile kullanma</span><span class="sxs-lookup"><span data-stu-id="ec52e-274">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="ec52e-275">Apache Spark’ı HDInsight üzerinde Kafka ile kullanma</span><span class="sxs-lookup"><span data-stu-id="ec52e-275">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="ec52e-276">Azure Sanal Ağ üzerinden Kafka’ya bağlanma</span><span class="sxs-lookup"><span data-stu-id="ec52e-276">Connect to Kafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
