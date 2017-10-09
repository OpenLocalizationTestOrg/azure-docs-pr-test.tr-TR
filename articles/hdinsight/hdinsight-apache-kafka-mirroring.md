---
title: "aaaMirror Apache Kafka konuları - Azure Hdınsight | Microsoft Docs"
description: "Nasıl toouse Apache Kafka'nın yansıtma özelliği toomaintain Kafka Hdınsight kümesinde bir kopyasını konuları tooa ikincil küme yansıtma tarafından öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 015d276e-f678-4f2b-9572-75553c56625b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: 5ace0251d7402d4d7d9b28726e253ce7091a87ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="use-mirrormaker-tooreplicate-apache-kafka-topics-with-kafka-on-hdinsight-preview"></a><span data-ttu-id="855c5-103">(Önizleme) hdınsight'ta Kafka ile MirrorMaker tooreplicate Apache Kafka konuları kullanın</span><span class="sxs-lookup"><span data-stu-id="855c5-103">Use MirrorMaker tooreplicate Apache Kafka topics with Kafka on HDInsight (preview)</span></span>

<span data-ttu-id="855c5-104">Toouse Apache Kafka özelliği tooreplicate konuları tooa ikincil küme nasıl yansıtma öğrenin.</span><span class="sxs-lookup"><span data-stu-id="855c5-104">Learn how toouse Apache Kafka's mirroring feature tooreplicate topics tooa secondary cluster.</span></span> <span data-ttu-id="855c5-105">Yansıtma bulunabilir sürekli bir işlem olarak çalışan, veya zaman zaman geçiş işleminin bir yöntem olarak kullanılan bir veri kümesi tooanother.</span><span class="sxs-lookup"><span data-stu-id="855c5-105">Mirroring can be ran as a continuous process, or used intermittently as a method of migrating data from one cluster tooanother.</span></span>

<span data-ttu-id="855c5-106">Bu örnekte, yansıtma kullanılan tooreplicate konular iki Hdınsight kümeleri arasında değil.</span><span class="sxs-lookup"><span data-stu-id="855c5-106">In this example, mirroring is used tooreplicate topics between two HDInsight clusters.</span></span> <span data-ttu-id="855c5-107">Her iki küme hello bir Azure sanal ağında bulunan aynı bölgede.</span><span class="sxs-lookup"><span data-stu-id="855c5-107">Both clusters are in an Azure Virtual Network in hello same region.</span></span>

> [!WARNING]
> <span data-ttu-id="855c5-108">Yansıtma, bir yol tooachieve hataya dayanıklılık düşünülmemelidir.</span><span class="sxs-lookup"><span data-stu-id="855c5-108">Mirroring should not be considered as a means tooachieve fault-tolerance.</span></span> <span data-ttu-id="855c5-109">istemcileri hello iki birbirinin yerine kullanamazlar hello uzaklık tooitems konu içinde hello kaynak ve hedef kümeler arasında farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="855c5-109">hello offset tooitems within a topic are different between hello source and destination clusters, so clients cannot use hello two interchangeably.</span></span>
>
> <span data-ttu-id="855c5-110">Hataya dayanıklılık hakkında endişeleriniz varsa, küme içinde çoğaltma hello konular için ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="855c5-110">If you are concerned about fault tolerance, you should set replication for hello topics within your cluster.</span></span> <span data-ttu-id="855c5-111">Daha fazla bilgi için bkz: [Kafka hdınsight kullanmaya başlama](hdinsight-apache-kafka-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="855c5-111">For more information, see [Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md).</span></span>

## <a name="how-kafka-mirroring-works"></a><span data-ttu-id="855c5-112">Yansıtma Kafka nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="855c5-112">How Kafka mirroring works</span></span>

<span data-ttu-id="855c5-113">Hello MirrorMaker Aracı (Apache Kafka parçası) tooconsume kullanarak yansıtma works hello kaynak kümesi konulardan kaydeder ve sonra hello hedef kümede yerel bir kopyasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="855c5-113">Mirroring works by using hello MirrorMaker tool (part of Apache Kafka) tooconsume records from topics on hello source cluster and then create a local copy on hello destination cluster.</span></span> <span data-ttu-id="855c5-114">MirrorMaker kullanan bir (veya daha fazla) *tüketicileri* hello kaynak kümeden okuyan ve *üretici* toohello yerel (hedef) küme yazar.</span><span class="sxs-lookup"><span data-stu-id="855c5-114">MirrorMaker uses one (or more) *consumers* that read from hello source cluster, and a *producer* that writes toohello local (destination) cluster.</span></span>

<span data-ttu-id="855c5-115">Aşağıdaki diyagramda hello hello yansıtma işlemi gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="855c5-115">hello following diagram illustrates hello Mirroring process:</span></span>

![İşlem yansıtma hello diyagramı](./media/hdinsight-apache-kafka-mirroring/kafka-mirroring.png)

<span data-ttu-id="855c5-117">Hdınsight üzerinde Apache Kafka hello erişim toohello Kafka hizmet sağlamaz genel internet.</span><span class="sxs-lookup"><span data-stu-id="855c5-117">Apache Kafka on HDInsight does not provide access toohello Kafka service over hello public internet.</span></span> <span data-ttu-id="855c5-118">Kafka üreticileri ya da tüketicilere hello olmalıdır hello Kafka küme hello düğümler aynı Azure sanal ağ.</span><span class="sxs-lookup"><span data-stu-id="855c5-118">Kafka producers or consumers must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="855c5-119">Bu örnekte, bir Azure sanal ağında hello Kafka kaynak ve hedef kümeler bulunur.</span><span class="sxs-lookup"><span data-stu-id="855c5-119">For this example, both hello Kafka source and destination clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="855c5-120">Merhaba Aşağıdaki diyagramda hello kümeleri arasında iletişimi nasıl akacağını gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="855c5-120">hello following diagram shows how communication flows between hello clusters:</span></span>

![Kaynak ve hedef Kafka diyagramı bir Azure sanal ağında kümeleri](./media/hdinsight-apache-kafka-mirroring/spark-kafka-vnet.png)

<span data-ttu-id="855c5-122">Merhaba kaynak ve hedef kümeler hello sayısında düğümleri ve bölümleri farklı olabilir ve uzaklıkları hello konuları içinde de farklıdır.</span><span class="sxs-lookup"><span data-stu-id="855c5-122">hello source and destination clusters can be different in hello number of nodes and partitions, and offsets within hello topics are different also.</span></span> <span data-ttu-id="855c5-123">Kayıt siparişi bir anahtar başına temelinde korunacak şekilde yansıtma bölümleme için kullanılan hello anahtar değerini korur.</span><span class="sxs-lookup"><span data-stu-id="855c5-123">Mirroring maintains hello key value that is used for partitioning, so record order is preserved on a per-key basis.</span></span>

### <a name="mirroring-across-network-boundaries"></a><span data-ttu-id="855c5-124">Ağ sınırları boyunca yansıtma</span><span class="sxs-lookup"><span data-stu-id="855c5-124">Mirroring across network boundaries</span></span>

<span data-ttu-id="855c5-125">Farklı ağlarda Kafka kümeler arasında toomirror gerekiyorsa, ek hususlar aşağıdaki hello vardır:</span><span class="sxs-lookup"><span data-stu-id="855c5-125">If you need toomirror between Kafka clusters in different networks, there are hello following additional considerations:</span></span>

* <span data-ttu-id="855c5-126">**Ağ geçitleri**: hello ağları hello TCPIP düzeyi adresindeki mümkün toocommunicate olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="855c5-126">**Gateways**: hello networks must be able toocommunicate at hello TCPIP level.</span></span>

* <span data-ttu-id="855c5-127">**Ad çözümlemesi**: ana bilgisayar adları kullanarak Kafka kümeleri her ağın hello tooeach mümkün tooconnect diğer olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="855c5-127">**Name resolution**: hello Kafka clusters in each network must be able tooconnect tooeach other by using hostnames.</span></span> <span data-ttu-id="855c5-128">Bu, bir etki alanı adı sistemi (DNS) sunucusu olduğu her ağdaki diğer ağlara tooforward istekleri toohello yapılandırılmış gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="855c5-128">This may require a Domain Name System (DNS) server in each network that is configured tooforward requests toohello other networks.</span></span>

    <span data-ttu-id="855c5-129">Bir Azure sanal hello ağla otomatik DNS sağlanan hello yerine ağ oluşturulurken bir özel DNS sunucusu ve hello sunucusu için IP adresi hello belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="855c5-129">When creating an Azure Virtual Network, instead of using hello automatic DNS provided with hello network, you must specify a custom DNS server and hello IP address for hello server.</span></span> <span data-ttu-id="855c5-130">Hello sanal ağ oluşturulduktan sonra ardından bu IP adresini kullanan bir Azure sanal makine oluşturun ardından yükleyin ve DNS yazılım üzerinde yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="855c5-130">After hello Virtual Network has been created, you must then create an Azure Virtual Machine that uses that IP address, then install and configure DNS software on it.</span></span>

    > [!WARNING]
    > <span data-ttu-id="855c5-131">Oluşturun ve sanal ağ hello Hdınsight yüklemeden önce hello özel DNS sunucusunu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="855c5-131">Create and configure hello custom DNS server before installing HDInsight into hello Virtual Network.</span></span> <span data-ttu-id="855c5-132">Merhaba sanal ağ için yapılandırılan Hdınsight toouse hello DNS sunucusu için gereken ek yapılandırma yoktur.</span><span class="sxs-lookup"><span data-stu-id="855c5-132">There is no additional configuration required for HDInsight toouse hello DNS server configured for hello Virtual Network.</span></span>

<span data-ttu-id="855c5-133">İki Azure sanal ağları bağlama ile ilgili daha fazla bilgi için bkz: [VNet-VNet bağlantı yapılandırma](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="855c5-133">For more information on connecting two Azure Virtual Networks, see [Configure a VNet-to-VNet connection](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span></span>

## <a name="create-kafka-clusters"></a><span data-ttu-id="855c5-134">Kafka kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="855c5-134">Create Kafka clusters</span></span>

<span data-ttu-id="855c5-135">Bir Azure sanal ağı oluşturmak ve Kafka el ile kümeleri olsa da, daha kolay toouse bir Azure Resource Manager şablonu durumdur.</span><span class="sxs-lookup"><span data-stu-id="855c5-135">While you can create an Azure virtual network and Kafka clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="855c5-136">Aşağıdaki adımları toodeploy hello Azure sanal ağı ve iki Kafka kümeleri tooyour Azure aboneliği kullanın.</span><span class="sxs-lookup"><span data-stu-id="855c5-136">Use hello following steps toodeploy an Azure virtual network and two Kafka clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="855c5-137">Düğme toosign tooAzure içinde ve açık hello şablonunda hello Azure portalı aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="855c5-137">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-kafka-mirroring/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    <span data-ttu-id="855c5-138">Hello Azure Resource Manager şablonu konumundadır **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.</span><span class="sxs-lookup"><span data-stu-id="855c5-138">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="855c5-139">Hdınsight üzerinde Kafka kullanılabilirliğini tooguarantee, kümenizi en az üç alt düğümleri içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="855c5-139">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="855c5-140">Bu şablon, üç alt düğümleri içeren bir Kafka küme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="855c5-140">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="855c5-141">Bilgi toopopulate hello girişleri hello üzerinde aşağıdaki kullanım hello **özel dağıtım** dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="855c5-141">Use hello following information toopopulate hello entries on hello **Custom deployment** blade:</span></span>
    
    ![Hdınsight özel dağıtım](./media/hdinsight-apache-kafka-mirroring/parameters.png)
    
    * <span data-ttu-id="855c5-143">**Kaynak grubu**: bir grup oluşturun veya varolan bir tanesini seçin.</span><span class="sxs-lookup"><span data-stu-id="855c5-143">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="855c5-144">Bu grup hello Hdınsight kümesi içerir.</span><span class="sxs-lookup"><span data-stu-id="855c5-144">This group contains hello HDInsight cluster.</span></span>

    * <span data-ttu-id="855c5-145">**Konum**: konum coğrafi olarak Kapat tooyou seçin.</span><span class="sxs-lookup"><span data-stu-id="855c5-145">**Location**: Select a location geographically close tooyou.</span></span>
     
    * <span data-ttu-id="855c5-146">**Temel küme adı**: Bu değer hello Kafka kümeleri için hello temel adı olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="855c5-146">**Base Cluster Name**: This value is used as hello base name for hello Kafka clusters.</span></span> <span data-ttu-id="855c5-147">Örneğin, **hdı** adlı kümeleri oluşturur **kaynak hdı** ve **taşınmaya hdı**.</span><span class="sxs-lookup"><span data-stu-id="855c5-147">For example, entering **hdi** creates clusters named **source-hdi** and **dest-hdi**.</span></span>

    * <span data-ttu-id="855c5-148">**Oturum açma kullanıcı adı küme**: hello kaynak ve hedef için hello yönetici kullanıcı adı Kafka kümeleri.</span><span class="sxs-lookup"><span data-stu-id="855c5-148">**Cluster Login User Name**: hello admin user name for hello source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="855c5-149">**Oturum açma parolası küme**: Merhaba yönetici kullanıcı parolasını hello kaynak ve hedef Kafka kümeleri.</span><span class="sxs-lookup"><span data-stu-id="855c5-149">**Cluster Login Password**: hello admin user password for hello source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="855c5-150">**SSH kullanıcı adı**: hello SSH kullanıcı toocreate hello kaynak ve hedef için Kafka kümeleri.</span><span class="sxs-lookup"><span data-stu-id="855c5-150">**SSH User Name**: hello SSH user toocreate for hello source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="855c5-151">**SSH parolası**: hello parola hello SSH kullanıcı hello kaynak ve hedef için Kafka kümeleri.</span><span class="sxs-lookup"><span data-stu-id="855c5-151">**SSH Password**: hello password for hello SSH user for hello source and destination Kafka clusters.</span></span>

3. <span data-ttu-id="855c5-152">Okuma hello **hüküm ve koşullar**ve ardından **toohello hüküm ve koşullar yukarıda belirtildiği kabul**.</span><span class="sxs-lookup"><span data-stu-id="855c5-152">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="855c5-153">Son olarak, denetleme **PIN toodashboard** ve ardından **satın alma**.</span><span class="sxs-lookup"><span data-stu-id="855c5-153">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="855c5-154">Merhaba kümeleri toocreate yaklaşık 20 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="855c5-154">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="855c5-155">Merhaba kaynakları oluşturduktan sonra yeniden yönlendirilen tooa dikey penceresinde hello kümeleri ve web Pano içeren hello kaynak grubu için demektir.</span><span class="sxs-lookup"><span data-stu-id="855c5-155">Once hello resources have been created, you are redirected tooa blade for hello resource group that contains hello clusters and web dashboard.</span></span>

![Kaynak grubu dikey hello vnet ve kümeler için](./media/hdinsight-apache-kafka-mirroring/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="855c5-157">Merhaba Hdınsight kümeleri Hello adlarını olduğuna dikkat edin **kaynak BASENAME** ve **taşınmaya BASENAME**, BASENAME toohello şablonu sağladığınız hello adı olduğu.</span><span class="sxs-lookup"><span data-stu-id="855c5-157">Notice that hello names of hello HDInsight clusters are **source-BASENAME** and **dest-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="855c5-158">Bu adları toohello kümeleri bağlanırken daha sonraki adımlarda kullanın.</span><span class="sxs-lookup"><span data-stu-id="855c5-158">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="create-topics"></a><span data-ttu-id="855c5-159">Konuları oluşturun</span><span class="sxs-lookup"><span data-stu-id="855c5-159">Create topics</span></span>

1. <span data-ttu-id="855c5-160">Toohello bağlanmak **kaynak** SSH kullanarak küme:</span><span class="sxs-lookup"><span data-stu-id="855c5-160">Connect toohello **source** cluster using SSH:</span></span>

    ```bash
    ssh sshuser@source-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="855c5-161">Değiştir **sshuser** hello küme oluşturulurken kullanılan hello SSH kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="855c5-161">Replace **sshuser** with hello SSH user name used when creating hello cluster.</span></span> <span data-ttu-id="855c5-162">Değiştir **BASENAME** hello küme oluşturulurken kullanılan hello temel ada sahip.</span><span class="sxs-lookup"><span data-stu-id="855c5-162">Replace **BASENAME** with hello base name used when creating hello cluster.</span></span>

    <span data-ttu-id="855c5-163">Bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="855c5-163">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="855c5-164">Kullanım hello aşağıdaki toofind hello Zookeeper konakları hello kaynak kümesi için komutlar:</span><span class="sxs-lookup"><span data-stu-id="855c5-164">Use hello following commands toofind hello Zookeeper hosts for hello source cluster:</span></span>

    ```bash
    # Install jq if it is not installed
    sudo apt -y install jq
    # get hello zookeeper hosts for hello source cluster
    export SOURCE_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    
    Replace `$PASSWORD` with hello password for hello cluster.

    Replace `$CLUSTERNAME` with hello name of hello source cluster.

3. toocreate a topic named `testtopic`, use hello following command:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 2 --partitions 8 --topic testtopic --zookeeper $SOURCE_ZKHOSTS
    ```

3. <span data-ttu-id="855c5-165">Konu hello komutu tooverify aşağıdaki kullanım hello oluşturuldu:</span><span class="sxs-lookup"><span data-stu-id="855c5-165">Use hello following command tooverify that hello topic was created:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="855c5-166">Merhaba yanıtını içeren `testtopic`.</span><span class="sxs-lookup"><span data-stu-id="855c5-166">hello response contains `testtopic`.</span></span>

4. <span data-ttu-id="855c5-167">Bu tooview hello Zookeeper ana bilgisayar bilgilerini aşağıdaki kullanım hello (Merhaba **kaynak**) küme:</span><span class="sxs-lookup"><span data-stu-id="855c5-167">Use hello following tooview hello Zookeeper host information for this (hello **source**) cluster:</span></span>

    ```bash
    echo $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="855c5-168">Bu metin aşağıdaki bilgileri benzer toohello döndürür:</span><span class="sxs-lookup"><span data-stu-id="855c5-168">This returns information similar toohello following text:</span></span>

    `zk0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181,zk1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181`

    <span data-ttu-id="855c5-169">Bu bilgileri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="855c5-169">Save this information.</span></span> <span data-ttu-id="855c5-170">Merhaba sonraki bölümde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="855c5-170">It is used in hello next section.</span></span>

## <a name="configure-mirroring"></a><span data-ttu-id="855c5-171">Yansıtmasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="855c5-171">Configure mirroring</span></span>

1. <span data-ttu-id="855c5-172">Toohello bağlanmak **hedef** küme farklı bir SSH oturumu kullanarak:</span><span class="sxs-lookup"><span data-stu-id="855c5-172">Connect toohello **destination** cluster using a different SSH session:</span></span>

    ```bash
    ssh sshuser@dest-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="855c5-173">Değiştir **sshuser** hello küme oluşturulurken kullanılan hello SSH kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="855c5-173">Replace **sshuser** with hello SSH user name used when creating hello cluster.</span></span> <span data-ttu-id="855c5-174">Değiştir **BASENAME** hello küme oluşturulurken kullanılan hello temel ada sahip.</span><span class="sxs-lookup"><span data-stu-id="855c5-174">Replace **BASENAME** with hello base name used when creating hello cluster.</span></span>

    <span data-ttu-id="855c5-175">Bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="855c5-175">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="855c5-176">Kullanım hello şu komutu toocreate bir `consumer.properties` açıklayan dosyasının nasıl hello ile toocommunicate **kaynak** küme:</span><span class="sxs-lookup"><span data-stu-id="855c5-176">Use hello following command toocreate a `consumer.properties` file that describes how toocommunicate with hello **source** cluster:</span></span>

    ```bash
    nano consumer.properties
    ```

    <span data-ttu-id="855c5-177">Metin hello Merhaba içeriğine aşağıdaki kullanım hello `consumer.properties` dosyası:</span><span class="sxs-lookup"><span data-stu-id="855c5-177">Use hello following text as hello contents of hello `consumer.properties` file:</span></span>

    ```yaml
    zookeeper.connect=SOURCE_ZKHOSTS
    group.id=mirrorgroup
    ```

    <span data-ttu-id="855c5-178">Değiştir **SOURCE_ZKHOSTS** ile Merhaba Zookeeper hello bilgilerinden barındıran **kaynak** küme.</span><span class="sxs-lookup"><span data-stu-id="855c5-178">Replace **SOURCE_ZKHOSTS** with hello Zookeeper hosts information from hello **source** cluster.</span></span>

    <span data-ttu-id="855c5-179">Bu dosya, Kafka küme hello kaynağından okunurken hello tüketici bilgi toouse tanımlar.</span><span class="sxs-lookup"><span data-stu-id="855c5-179">This file describes hello consumer information toouse when reading from hello source Kafka cluster.</span></span> <span data-ttu-id="855c5-180">Daha fazla bilgi tüketici yapılandırma için bkz: [tüketici yapılandırmalar](https://kafka.apache.org/documentation#consumerconfigs) kafka.apache.org adresindeki.</span><span class="sxs-lookup"><span data-stu-id="855c5-180">For more information consumer configuration, see [Consumer Configs](https://kafka.apache.org/documentation#consumerconfigs) at kafka.apache.org.</span></span>

    <span data-ttu-id="855c5-181">toosave hello dosya, kullanım **Ctrl + X**, **Y**ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="855c5-181">toosave hello file, use **Ctrl + X**, **Y**, and then **Enter**.</span></span>

3. <span data-ttu-id="855c5-182">Hello hedef küme ile iletişim kurar hello üretici yapılandırmadan önce hello Aracısı konakları Merhaba bulmalıdır **hedef** küme.</span><span class="sxs-lookup"><span data-stu-id="855c5-182">Before configuring hello producer that communicates with hello destination cluster, you must find hello broker hosts for hello **destination** cluster.</span></span> <span data-ttu-id="855c5-183">Aşağıdaki komutları tooretrieve hello bu bilgileri kullanın:</span><span class="sxs-lookup"><span data-stu-id="855c5-183">Use hello following commands tooretrieve this information:</span></span>

    ```bash
    sudo apt -y install jq
    DEST_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    echo $DEST_BROKERHOSTS
    ```

    <span data-ttu-id="855c5-184">Değiştir `$PASSWORD` parolayla hello oturum açma hesabı (Yönetici) hello kümesi için.</span><span class="sxs-lookup"><span data-stu-id="855c5-184">Replace `$PASSWORD` with hello login account (admin) password for hello cluster.</span></span>

    <span data-ttu-id="855c5-185">Değiştir `$CLUSTERNAME` hello hedef küme hello adı.</span><span class="sxs-lookup"><span data-stu-id="855c5-185">Replace `$CLUSTERNAME` with hello name of hello destination cluster.</span></span>

    <span data-ttu-id="855c5-186">Bu komutlar bilgi benzer toohello aşağıdaki döndürün:</span><span class="sxs-lookup"><span data-stu-id="855c5-186">These commands return information similar toohello following:</span></span>

        wn0-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn1-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092

4. <span data-ttu-id="855c5-187">Kullanım hello toocreate izleyen bir `producer.properties` açıklayan dosyasının nasıl hello ile toocommunicate **hedef** küme:</span><span class="sxs-lookup"><span data-stu-id="855c5-187">Use hello following toocreate a `producer.properties` file that describes how toocommunicate with hello **destination** cluster:</span></span>

    ```bash
    nano producer.properties
    ```

    <span data-ttu-id="855c5-188">Metin hello Merhaba içeriğine aşağıdaki kullanım hello `producer.properties` dosyası:</span><span class="sxs-lookup"><span data-stu-id="855c5-188">Use hello following text as hello contents of hello `producer.properties` file:</span></span>

    ```yaml
    bootstrap.servers=DEST_BROKERS
    compression.type=none
    ```

    <span data-ttu-id="855c5-189">Değiştir **DEST_BROKERS** hello önceki adımdaki hello Aracısı bilgilerle.</span><span class="sxs-lookup"><span data-stu-id="855c5-189">Replace **DEST_BROKERS** with hello broker information from hello previous step.</span></span>

    <span data-ttu-id="855c5-190">Daha fazla bilgi üretici yapılandırma için bkz: [üretici yapılandırmalar](https://kafka.apache.org/documentation#producerconfigs) kafka.apache.org adresindeki.</span><span class="sxs-lookup"><span data-stu-id="855c5-190">For more information producer configuration, see [Producer Configs](https://kafka.apache.org/documentation#producerconfigs) at kafka.apache.org.</span></span>

## <a name="start-mirrormaker"></a><span data-ttu-id="855c5-191">MirrorMaker Başlat</span><span class="sxs-lookup"><span data-stu-id="855c5-191">Start MirrorMaker</span></span>

1. <span data-ttu-id="855c5-192">Merhaba SSH bağlantı toohello gelen **hedef** küme, komut toostart hello MirrorMaker işlemi aşağıdaki hello kullanın:</span><span class="sxs-lookup"><span data-stu-id="855c5-192">From hello SSH connection toohello **destination** cluster, use hello following command toostart hello MirrorMaker process:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-run-class.sh kafka.tools.MirrorMaker --consumer.config consumer.properties --producer.config producer.properties --whitelist testtopic --num.streams 4
    ```

    <span data-ttu-id="855c5-193">Bu örnekte kullanılan hello Parametreler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="855c5-193">hello parameters used in this example are:</span></span>

    * <span data-ttu-id="855c5-194">**--consumer.config**: tüketici özellikleri içeren hello dosyasını belirtir.</span><span class="sxs-lookup"><span data-stu-id="855c5-194">**--consumer.config**: Specifies hello file that contains consumer properties.</span></span> <span data-ttu-id="855c5-195">Bu özellikler kullanılan toocreate hello okuyan bir tüketici: *kaynak* Kafka küme.</span><span class="sxs-lookup"><span data-stu-id="855c5-195">These properties are used toocreate a consumer that reads from hello *source* Kafka cluster.</span></span>

    * <span data-ttu-id="855c5-196">**--producer.config**: üretici özellikleri içeren hello dosyasını belirtir.</span><span class="sxs-lookup"><span data-stu-id="855c5-196">**--producer.config**: Specifies hello file that contains producer properties.</span></span> <span data-ttu-id="855c5-197">Bu özellikler kullanılan toocreate toohello Yazar bir üretici: *hedef* Kafka küme.</span><span class="sxs-lookup"><span data-stu-id="855c5-197">These properties are used toocreate a producer that writes toohello *destination* Kafka cluster.</span></span>

    * <span data-ttu-id="855c5-198">**--beyaz liste**: hello kaynak küme toohello hedef MirrorMaker çoğaltır konuların listesi.</span><span class="sxs-lookup"><span data-stu-id="855c5-198">**--whitelist**: A list of topics that MirrorMaker replicates from hello source cluster toohello destination.</span></span>

    * <span data-ttu-id="855c5-199">**--num.streams**: Merhaba tüketici iş parçacığı toocreate sayısı.</span><span class="sxs-lookup"><span data-stu-id="855c5-199">**--num.streams**: hello number of consumer threads toocreate.</span></span>

 <span data-ttu-id="855c5-200">Başlangıç sırasında aşağıdaki metin bilgi benzer toohello MirrorMaker döndürür:</span><span class="sxs-lookup"><span data-stu-id="855c5-200">On startup, MirrorMaker returns information similar toohello following text:</span></span>

    ```json
    {metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-3, security.protocol=PLAINTEXT}{metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-0, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-kafka.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-2, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-1, security.protocol=PLAINTEXT}
    ```

2. <span data-ttu-id="855c5-201">Merhaba SSH bağlantı toohello gelen **kaynak** küme, komut toostart bir üretici aşağıdaki hello kullanın ve iletileri toohello konu gönderin:</span><span class="sxs-lookup"><span data-stu-id="855c5-201">From hello SSH connection toohello **source** cluster, use hello following command toostart a producer and send messages toohello topic:</span></span>

    ```bash
    SOURCE_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $SOURCE_BROKERHOSTS --topic testtopic
    ```

    <span data-ttu-id="855c5-202">Değiştir `$PASSWORD` hello kaynak kümesi için hello oturum açma (Yönetici) parolayla.</span><span class="sxs-lookup"><span data-stu-id="855c5-202">Replace `$PASSWORD` with hello login (admin) password for hello source cluster.</span></span>

    <span data-ttu-id="855c5-203">Değiştir `$CLUSTERNAME` hello kaynak kümesi hello adı.</span><span class="sxs-lookup"><span data-stu-id="855c5-203">Replace `$CLUSTERNAME` with hello name of hello source cluster.</span></span>

     <span data-ttu-id="855c5-204">Boş bir satırı bir imleç ile geldiğinde, birkaç metin iletileri yazın.</span><span class="sxs-lookup"><span data-stu-id="855c5-204">When you arrive at a blank line with a cursor, type in a few text messages.</span></span> <span data-ttu-id="855c5-205">Bunlar toohello konu üzerinde hello gönderilen **kaynak** küme.</span><span class="sxs-lookup"><span data-stu-id="855c5-205">These are sent toohello topic on hello **source** cluster.</span></span> <span data-ttu-id="855c5-206">İşiniz bittiğinde, kullanın **Ctrl + C** tooend hello üretici işlemi.</span><span class="sxs-lookup"><span data-stu-id="855c5-206">When done, use **Ctrl + C** tooend hello producer process.</span></span>

3. <span data-ttu-id="855c5-207">Merhaba SSH bağlantı toohello gelen **hedef** küme, kullanın **Ctrl + C** tooend hello MirrorMaker işlemi.</span><span class="sxs-lookup"><span data-stu-id="855c5-207">From hello SSH connection toohello **destination** cluster, use **Ctrl + C** tooend hello MirrorMaker process.</span></span> <span data-ttu-id="855c5-208">Bu hello tooverify kullanım hello aşağıdaki komutları sonra `testtopic` konu oluşturuldu ve bu verileri hello konudaki çoğaltılmış toothis yansıtma idi:</span><span class="sxs-lookup"><span data-stu-id="855c5-208">Then use hello following commands tooverify that hello `testtopic` topic was created, and that data in hello topic was replicated toothis mirror:</span></span>

    ```bash
    DEST_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $DEST_ZKHOSTS
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $DEST_ZKHOSTS --topic testtopic --from-beginning
    ```

    <span data-ttu-id="855c5-209">Değiştir `$PASSWORD` hello hedef küme için hello oturum açma (Yönetici) parolayla.</span><span class="sxs-lookup"><span data-stu-id="855c5-209">Replace `$PASSWORD` with hello login (admin) password for hello destination cluster.</span></span>

    <span data-ttu-id="855c5-210">Değiştir `$CLUSTERNAME` hello hedef küme hello adı.</span><span class="sxs-lookup"><span data-stu-id="855c5-210">Replace `$CLUSTERNAME` with hello name of hello destination cluster.</span></span>

    <span data-ttu-id="855c5-211">Merhaba konuların listesi şimdi içeren `testtopic`, MirrorMaster hello kaynak küme toohello hedef hello konusundan yansıtan zaman oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="855c5-211">hello list of topics now includes `testtopic`, which is created when MirrorMaster mirrors hello topic from hello source cluster toohello destination.</span></span> <span data-ttu-id="855c5-212">Merhaba konusundan alınan hello iletileri hello kaynak kümede girilen aynı hello ' dir.</span><span class="sxs-lookup"><span data-stu-id="855c5-212">hello messages retrieved from hello topic are hello same as entered on hello source cluster.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="855c5-213">Merhaba küme silme</span><span class="sxs-lookup"><span data-stu-id="855c5-213">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="855c5-214">Merhaba adımlar bu belgedeki her ikisi de oluşturma beri kümelerde Merhaba aynı Azure kaynak grubu, hello Azure portal hello kaynak grubunu silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="855c5-214">Since hello steps in this document create both clusters in hello same Azure resource group, you can delete hello resource group in hello Azure portal.</span></span> <span data-ttu-id="855c5-215">Bu belge, hello Azure sanal ağ ve depolama hesabı hello kümeleri tarafından kullanılan uygulayarak oluşturduğunuz tüm kaynakları silme hello kaynak grubunu kaldırır.</span><span class="sxs-lookup"><span data-stu-id="855c5-215">Deleting hello resource group removes all resources created by following this document, hello Azure Virtual Network, and storage account used by hello clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="855c5-216">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="855c5-216">Next Steps</span></span>

<span data-ttu-id="855c5-217">Bu belgede nasıl toouse MirrorMaker toocreate bir Kafka çoğaltmasını küme öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="855c5-217">In this document, you learned how toouse MirrorMaker toocreate a replica of a Kafka cluster.</span></span> <span data-ttu-id="855c5-218">Aşağıdaki bağlantılar toodiscover hello diğer yolları toowork Kafka ile kullanın:</span><span class="sxs-lookup"><span data-stu-id="855c5-218">Use hello following links toodiscover other ways toowork with Kafka:</span></span>

* <span data-ttu-id="855c5-219">[Apache Kafka MirrorMaker belgelerine](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) cwiki.apache.org adresindeki.</span><span class="sxs-lookup"><span data-stu-id="855c5-219">[Apache Kafka MirrorMaker documentation](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) at cwiki.apache.org.</span></span>
* [<span data-ttu-id="855c5-220">Hdınsight üzerinde Apache Kafka kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="855c5-220">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="855c5-221">Apache Spark’ı HDInsight üzerinde Kafka ile kullanma</span><span class="sxs-lookup"><span data-stu-id="855c5-221">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="855c5-222">Apache Storm’u HDInsight üzerinde Kafka ile kullanma</span><span class="sxs-lookup"><span data-stu-id="855c5-222">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="855c5-223">Bir Azure sanal ağı tooKafka Bağlan</span><span class="sxs-lookup"><span data-stu-id="855c5-223">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
