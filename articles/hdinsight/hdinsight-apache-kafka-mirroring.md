---
title: "Apache Kafka konuları - Azure Hdınsight yansıtma | Microsoft Docs"
description: "İkincil bir küme konulara yansıtma tarafından Kafka Hdınsight kümesinde bir kopyasını korumak için Apache Kafka'nın yansıtma özelliğini kullanmayı öğrenin."
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
ms.openlocfilehash: e418cb01e1a9168e3662e8d6242903e052b6047b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="use-mirrormaker-to-replicate-apache-kafka-topics-with-kafka-on-hdinsight-preview"></a><span data-ttu-id="0a1a3-103">Kafka (Önizleme) hdınsight'ta Apache Kafka konuları çoğaltmak için MirrorMaker kullanın</span><span class="sxs-lookup"><span data-stu-id="0a1a3-103">Use MirrorMaker to replicate Apache Kafka topics with Kafka on HDInsight (preview)</span></span>

<span data-ttu-id="0a1a3-104">İkincil bir kümeye konuları çoğaltmak için Apache Kafka'nın yansıtma özelliğini kullanmayı öğrenin.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-104">Learn how to use Apache Kafka's mirroring feature to replicate topics to a secondary cluster.</span></span> <span data-ttu-id="0a1a3-105">Yansıtma bulunabilir sürekli bir işlem olarak çalışan, veya zaman zaman geçiş işleminin bir yöntem olarak kullanılan bir kümeden veri.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-105">Mirroring can be ran as a continuous process, or used intermittently as a method of migrating data from one cluster to another.</span></span>

<span data-ttu-id="0a1a3-106">Bu örnekte, yansıtma konular iki Hdınsight kümeleri arasında çoğaltmak için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-106">In this example, mirroring is used to replicate topics between two HDInsight clusters.</span></span> <span data-ttu-id="0a1a3-107">Her iki kümeleri aynı bölgede bir Azure sanal ağındaki ' dir.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-107">Both clusters are in an Azure Virtual Network in the same region.</span></span>

> [!WARNING]
> <span data-ttu-id="0a1a3-108">Yansıtma hataya dayanıklılık sağlamak için bir yöntem düşünülmemelidir.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-108">Mirroring should not be considered as a means to achieve fault-tolerance.</span></span> <span data-ttu-id="0a1a3-109">Bir konu içindeki öğeleri uzaklık kaynak ve hedef kümeler arasında farklı istemcileri iki birbirinin yerine kullanamazlar.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-109">The offset to items within a topic are different between the source and destination clusters, so clients cannot use the two interchangeably.</span></span>
>
> <span data-ttu-id="0a1a3-110">Hataya dayanıklılık hakkında endişeleriniz varsa, küme içinde çoğaltma konular için ayarlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-110">If you are concerned about fault tolerance, you should set replication for the topics within your cluster.</span></span> <span data-ttu-id="0a1a3-111">Daha fazla bilgi için bkz: [Kafka hdınsight kullanmaya başlama](hdinsight-apache-kafka-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0a1a3-111">For more information, see [Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md).</span></span>

## <a name="how-kafka-mirroring-works"></a><span data-ttu-id="0a1a3-112">Yansıtma Kafka nasıl çalışır?</span><span class="sxs-lookup"><span data-stu-id="0a1a3-112">How Kafka mirroring works</span></span>

<span data-ttu-id="0a1a3-113">Yansıtma için Works MirrorMaker aracını (Apache Kafka parçası) kullanarak kayıtları kaynak kümede konulardan kullanmak ve sonra hedef kümede yerel bir kopyasını oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-113">Mirroring works by using the MirrorMaker tool (part of Apache Kafka) to consume records from topics on the source cluster and then create a local copy on the destination cluster.</span></span> <span data-ttu-id="0a1a3-114">MirrorMaker kullanan bir (veya daha fazla) *tüketicileri* kaynak kümeden okuyan ve *üretici* yerel (hedef) kümeye yazar.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-114">MirrorMaker uses one (or more) *consumers* that read from the source cluster, and a *producer* that writes to the local (destination) cluster.</span></span>

<span data-ttu-id="0a1a3-115">Aşağıdaki diyagram yansıtma işlemini gösterir:</span><span class="sxs-lookup"><span data-stu-id="0a1a3-115">The following diagram illustrates the Mirroring process:</span></span>

![Yansıtma işlemi diyagramı](./media/hdinsight-apache-kafka-mirroring/kafka-mirroring.png)

<span data-ttu-id="0a1a3-117">Hdınsight üzerinde Apache Kafka, ortak internet üzerinden Kafka hizmetine erişim sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-117">Apache Kafka on HDInsight does not provide access to the Kafka service over the public internet.</span></span> <span data-ttu-id="0a1a3-118">Kafka üreticileri veya tüketicileri Kafka kümedeki düğümlerin aynı Azure sanal ağ içinde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-118">Kafka producers or consumers must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="0a1a3-119">Bu örnekte, Kafka kaynak ve hedef kümeler Azure sanal ağında yer alır.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-119">For this example, both the Kafka source and destination clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="0a1a3-120">Aşağıdaki diyagramda, iletişim kümeleri arasında nasıl aktığını gösterir:</span><span class="sxs-lookup"><span data-stu-id="0a1a3-120">The following diagram shows how communication flows between the clusters:</span></span>

![Kaynak ve hedef Kafka diyagramı bir Azure sanal ağında kümeleri](./media/hdinsight-apache-kafka-mirroring/spark-kafka-vnet.png)

<span data-ttu-id="0a1a3-122">Kaynak ve hedef küme düğümlerini ve bölümleri sayısında farklı olabilir ve uzaklıkları konuları içinde de farklıdır.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-122">The source and destination clusters can be different in the number of nodes and partitions, and offsets within the topics are different also.</span></span> <span data-ttu-id="0a1a3-123">Kayıt siparişi bir anahtar başına temelinde korunacak şekilde yansıtma bölümleme için kullanılan anahtar değerini korur.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-123">Mirroring maintains the key value that is used for partitioning, so record order is preserved on a per-key basis.</span></span>

### <a name="mirroring-across-network-boundaries"></a><span data-ttu-id="0a1a3-124">Ağ sınırları boyunca yansıtma</span><span class="sxs-lookup"><span data-stu-id="0a1a3-124">Mirroring across network boundaries</span></span>

<span data-ttu-id="0a1a3-125">Farklı ağlarda Kafka kümeler arasında yansıtma gerekiyorsa, aşağıdaki dikkat edilecek diğer noktalar vardır:</span><span class="sxs-lookup"><span data-stu-id="0a1a3-125">If you need to mirror between Kafka clusters in different networks, there are the following additional considerations:</span></span>

* <span data-ttu-id="0a1a3-126">**Ağ geçitleri**: ağları TCPIP düzeyinde iletişim kurabilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-126">**Gateways**: The networks must be able to communicate at the TCPIP level.</span></span>

* <span data-ttu-id="0a1a3-127">**Ad çözümlemesi**: her ağ Kafka kümelerde sağlayabilmelidir ana bilgisayar adları kullanarak birbirine bağlamak.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-127">**Name resolution**: The Kafka clusters in each network must be able to connect to each other by using hostnames.</span></span> <span data-ttu-id="0a1a3-128">Bu diğer ağlara istekleri iletmek için yapılandırılan her ağındaki bir etki alanı adı sistemi (DNS) sunucusu gerektirebilir.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-128">This may require a Domain Name System (DNS) server in each network that is configured to forward requests to the other networks.</span></span>

    <span data-ttu-id="0a1a3-129">Bir Azure sanal ağ ile sağlanan otomatik DNS kullanmak yerine ağ oluşturulurken özel bir DNS sunucusu ve sunucunun IP adresini belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-129">When creating an Azure Virtual Network, instead of using the automatic DNS provided with the network, you must specify a custom DNS server and the IP address for the server.</span></span> <span data-ttu-id="0a1a3-130">Sanal ağ oluşturulduktan sonra ardından bu IP adresini kullanan bir Azure sanal makine oluşturmak daha sonra yüklemek ve DNS yazılım üzerinde yapılandırmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-130">After the Virtual Network has been created, you must then create an Azure Virtual Machine that uses that IP address, then install and configure DNS software on it.</span></span>

    > [!WARNING]
    > <span data-ttu-id="0a1a3-131">Oluşturun ve Hdınsight sanal ağınıza yüklemeden önce özel DNS sunucusunu yapılandırın.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-131">Create and configure the custom DNS server before installing HDInsight into the Virtual Network.</span></span> <span data-ttu-id="0a1a3-132">Sanal ağ için yapılandırılan DNS sunucusunun kullanılacağını Hdınsight için gereken ek yapılandırma yoktur.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-132">There is no additional configuration required for HDInsight to use the DNS server configured for the Virtual Network.</span></span>

<span data-ttu-id="0a1a3-133">İki Azure sanal ağları bağlama ile ilgili daha fazla bilgi için bkz: [VNet-VNet bağlantı yapılandırma](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="0a1a3-133">For more information on connecting two Azure Virtual Networks, see [Configure a VNet-to-VNet connection](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span></span>

## <a name="create-kafka-clusters"></a><span data-ttu-id="0a1a3-134">Kafka kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="0a1a3-134">Create Kafka clusters</span></span>

<span data-ttu-id="0a1a3-135">Bir Azure sanal ağı oluşturmak ve Kafka el ile kümeleri olsa da, bir Azure Resource Manager şablonunu kullanmak daha kolaydır.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-135">While you can create an Azure virtual network and Kafka clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="0a1a3-136">Bir Azure sanal ağı ve iki Kafka kümeleri Azure aboneliğinize dağıtmak için aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-136">Use the following steps to deploy an Azure virtual network and two Kafka clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="0a1a3-137">Azure'da oturum açın ve Azure portalında şablon açmak için aşağıdaki düğmesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-137">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-kafka-mirroring/deploy-to-azure.png" alt="Deploy to Azure"></a>
   
    <span data-ttu-id="0a1a3-138">Azure Resource Manager şablonu bulunur **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-138">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="0a1a3-139">HDInsight üzerinde Kafka'yı kullanabilmeniz için kümenizin en az üç çalışan düğümü içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-139">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="0a1a3-140">Bu şablon, üç alt düğümleri içeren bir Kafka küme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-140">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="0a1a3-141">Üzerinde girişleri doldurmak için aşağıdaki bilgileri kullanın **özel dağıtım** dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="0a1a3-141">Use the following information to populate the entries on the **Custom deployment** blade:</span></span>
    
    ![Hdınsight özel dağıtım](./media/hdinsight-apache-kafka-mirroring/parameters.png)
    
    * <span data-ttu-id="0a1a3-143">**Kaynak grubu**: bir grup oluşturun veya varolan bir tanesini seçin.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-143">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="0a1a3-144">Bu grup, Hdınsight kümesi içerir.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-144">This group contains the HDInsight cluster.</span></span>

    * <span data-ttu-id="0a1a3-145">**Konum**: coğrafi olarak yakın bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-145">**Location**: Select a location geographically close to you.</span></span>
     
    * <span data-ttu-id="0a1a3-146">**Temel küme adı**: Kafka kümeleri için bu değer taban adı olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-146">**Base Cluster Name**: This value is used as the base name for the Kafka clusters.</span></span> <span data-ttu-id="0a1a3-147">Örneğin, **hdı** adlı kümeleri oluşturur **kaynak hdı** ve **taşınmaya hdı**.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-147">For example, entering **hdi** creates clusters named **source-hdi** and **dest-hdi**.</span></span>

    * <span data-ttu-id="0a1a3-148">**Oturum açma kullanıcı adı küme**: kaynak ve hedef için yönetici kullanıcı adı Kafka kümeleri.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-148">**Cluster Login User Name**: The admin user name for the source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="0a1a3-149">**Oturum açma parolası küme**: kaynak ve hedef için yönetici kullanıcı parolası Kafka kümeleri.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-149">**Cluster Login Password**: The admin user password for the source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="0a1a3-150">**SSH kullanıcı adı**: kaynak ve hedef Kafka için kümeleri oluşturmak için SSH kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-150">**SSH User Name**: The SSH user to create for the source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="0a1a3-151">**SSH parolası**: kaynak ve hedef SSH kullanıcı için parola Kafka kümeleri.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-151">**SSH Password**: The password for the SSH user for the source and destination Kafka clusters.</span></span>

3. <span data-ttu-id="0a1a3-152">Okuma **hüküm ve koşullar**ve ardından **hüküm ve koşulları yukarıda belirtildiği ediyorum**.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-152">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="0a1a3-153">Son olarak, denetleme **panoya Sabitle** ve ardından **satın alma**.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-153">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="0a1a3-154">Kümeleri oluşturmak için yaklaşık 20 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-154">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="0a1a3-155">Kaynakları oluşturduktan sonra kümeler ve web Pano içeren kaynak grubu için bir dikey penceresine yönlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-155">Once the resources have been created, you are redirected to a blade for the resource group that contains the clusters and web dashboard.</span></span>

![Kaynak grubu dikey vnet ve kümeler için](./media/hdinsight-apache-kafka-mirroring/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="0a1a3-157">Hdınsight kümeleri adlarının bildirimi **kaynak BASENAME** ve **taşınmaya BASENAME**, BASENAME şablona verdiğiniz adı olduğu.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-157">Notice that the names of the HDInsight clusters are **source-BASENAME** and **dest-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="0a1a3-158">Kümeye bağlanırken bu adları daha sonraki adımlarda kullanın.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-158">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="create-topics"></a><span data-ttu-id="0a1a3-159">Konuları oluşturun</span><span class="sxs-lookup"><span data-stu-id="0a1a3-159">Create topics</span></span>

1. <span data-ttu-id="0a1a3-160">Bağlanmak **kaynak** SSH kullanarak küme:</span><span class="sxs-lookup"><span data-stu-id="0a1a3-160">Connect to the **source** cluster using SSH:</span></span>

    ```bash
    ssh sshuser@source-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="0a1a3-161">Değiştir **sshuser** küme oluşturulurken kullanılan SSH kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-161">Replace **sshuser** with the SSH user name used when creating the cluster.</span></span> <span data-ttu-id="0a1a3-162">Değiştir **BASENAME** küme oluşturulurken kullanılan taban adına sahip.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-162">Replace **BASENAME** with the base name used when creating the cluster.</span></span>

    <span data-ttu-id="0a1a3-163">Bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="0a1a3-163">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="0a1a3-164">Kaynak kümenin Zookeeper ana bilgisayarları bulmak için aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="0a1a3-164">Use the following commands to find the Zookeeper hosts for the source cluster:</span></span>

    ```bash
    # Install jq if it is not installed
    sudo apt -y install jq
    # get the zookeeper hosts for the source cluster
    export SOURCE_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    
    Replace `$PASSWORD` with the password for the cluster.

    Replace `$CLUSTERNAME` with the name of the source cluster.

3. To create a topic named `testtopic`, use the following command:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 2 --partitions 8 --topic testtopic --zookeeper $SOURCE_ZKHOSTS
    ```

3. <span data-ttu-id="0a1a3-165">Konu oluşturulduğunu doğrulamak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="0a1a3-165">Use the following command to verify that the topic was created:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="0a1a3-166">Yanıtı içeren `testtopic`.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-166">The response contains `testtopic`.</span></span>

4. <span data-ttu-id="0a1a3-167">Bu Zookeeper ana bilgisayar bilgilerini görüntülemek için aşağıdakini kullanın ( **kaynak**) küme:</span><span class="sxs-lookup"><span data-stu-id="0a1a3-167">Use the following to view the Zookeeper host information for this (the **source**) cluster:</span></span>

    ```bash
    echo $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="0a1a3-168">Bu bilgiler aşağıdaki metni benzer döndürür:</span><span class="sxs-lookup"><span data-stu-id="0a1a3-168">This returns information similar to the following text:</span></span>

    `zk0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181,zk1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181`

    <span data-ttu-id="0a1a3-169">Bu bilgileri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-169">Save this information.</span></span> <span data-ttu-id="0a1a3-170">Sonraki bölümde kullanılır.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-170">It is used in the next section.</span></span>

## <a name="configure-mirroring"></a><span data-ttu-id="0a1a3-171">Yansıtmasını yapılandırma</span><span class="sxs-lookup"><span data-stu-id="0a1a3-171">Configure mirroring</span></span>

1. <span data-ttu-id="0a1a3-172">Bağlanmak **hedef** küme farklı bir SSH oturumu kullanarak:</span><span class="sxs-lookup"><span data-stu-id="0a1a3-172">Connect to the **destination** cluster using a different SSH session:</span></span>

    ```bash
    ssh sshuser@dest-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="0a1a3-173">Değiştir **sshuser** küme oluşturulurken kullanılan SSH kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-173">Replace **sshuser** with the SSH user name used when creating the cluster.</span></span> <span data-ttu-id="0a1a3-174">Değiştir **BASENAME** küme oluşturulurken kullanılan taban adına sahip.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-174">Replace **BASENAME** with the base name used when creating the cluster.</span></span>

    <span data-ttu-id="0a1a3-175">Bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="0a1a3-175">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="0a1a3-176">Oluşturmak için aşağıdaki komutu kullanın bir `consumer.properties` ile iletişim kurmak açıklar dosya **kaynak** küme:</span><span class="sxs-lookup"><span data-stu-id="0a1a3-176">Use the following command to create a `consumer.properties` file that describes how to communicate with the **source** cluster:</span></span>

    ```bash
    nano consumer.properties
    ```

    <span data-ttu-id="0a1a3-177">Aşağıdaki metni içeriğini kullanmak `consumer.properties` dosyası:</span><span class="sxs-lookup"><span data-stu-id="0a1a3-177">Use the following text as the contents of the `consumer.properties` file:</span></span>

    ```yaml
    zookeeper.connect=SOURCE_ZKHOSTS
    group.id=mirrorgroup
    ```

    <span data-ttu-id="0a1a3-178">Değiştir **SOURCE_ZKHOSTS** Zookeeper konakları bilgilerle **kaynak** küme.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-178">Replace **SOURCE_ZKHOSTS** with the Zookeeper hosts information from the **source** cluster.</span></span>

    <span data-ttu-id="0a1a3-179">Bu dosya kaynak Kafka küme okurken kullanılacak tüketici bilgiler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-179">This file describes the consumer information to use when reading from the source Kafka cluster.</span></span> <span data-ttu-id="0a1a3-180">Daha fazla bilgi tüketici yapılandırma için bkz: [tüketici yapılandırmalar](https://kafka.apache.org/documentation#consumerconfigs) kafka.apache.org adresindeki.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-180">For more information consumer configuration, see [Consumer Configs](https://kafka.apache.org/documentation#consumerconfigs) at kafka.apache.org.</span></span>

    <span data-ttu-id="0a1a3-181">Dosyayı kaydetmek için kullanın **Ctrl + X**, **Y**ve ardından **Enter**.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-181">To save the file, use **Ctrl + X**, **Y**, and then **Enter**.</span></span>

3. <span data-ttu-id="0a1a3-182">Hedef küme ile iletişim kurar üretici yapılandırmadan önce ana bilgisayarlar için aracı bulmalıdır **hedef** küme.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-182">Before configuring the producer that communicates with the destination cluster, you must find the broker hosts for the **destination** cluster.</span></span> <span data-ttu-id="0a1a3-183">Bu bilgileri almak için aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="0a1a3-183">Use the following commands to retrieve this information:</span></span>

    ```bash
    sudo apt -y install jq
    DEST_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    echo $DEST_BROKERHOSTS
    ```

    <span data-ttu-id="0a1a3-184">Değiştir `$PASSWORD` küme için oturum açma hesabı (Yönetici) parolayla.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-184">Replace `$PASSWORD` with the login account (admin) password for the cluster.</span></span>

    <span data-ttu-id="0a1a3-185">Değiştir `$CLUSTERNAME` hedef küme adı.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-185">Replace `$CLUSTERNAME` with the name of the destination cluster.</span></span>

    <span data-ttu-id="0a1a3-186">Bu komutlar bilgi aşağıdakine benzer döndürün:</span><span class="sxs-lookup"><span data-stu-id="0a1a3-186">These commands return information similar to the following:</span></span>

        wn0-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn1-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092

4. <span data-ttu-id="0a1a3-187">Oluşturmak için aşağıdakileri kullanın bir `producer.properties` ile iletişim kurmak açıklar dosya **hedef** küme:</span><span class="sxs-lookup"><span data-stu-id="0a1a3-187">Use the following to create a `producer.properties` file that describes how to communicate with the **destination** cluster:</span></span>

    ```bash
    nano producer.properties
    ```

    <span data-ttu-id="0a1a3-188">Aşağıdaki metni içeriğini kullanmak `producer.properties` dosyası:</span><span class="sxs-lookup"><span data-stu-id="0a1a3-188">Use the following text as the contents of the `producer.properties` file:</span></span>

    ```yaml
    bootstrap.servers=DEST_BROKERS
    compression.type=none
    ```

    <span data-ttu-id="0a1a3-189">Değiştir **DEST_BROKERS** önceki adımdan Aracısı bilgilerle.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-189">Replace **DEST_BROKERS** with the broker information from the previous step.</span></span>

    <span data-ttu-id="0a1a3-190">Daha fazla bilgi üretici yapılandırma için bkz: [üretici yapılandırmalar](https://kafka.apache.org/documentation#producerconfigs) kafka.apache.org adresindeki.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-190">For more information producer configuration, see [Producer Configs](https://kafka.apache.org/documentation#producerconfigs) at kafka.apache.org.</span></span>

## <a name="start-mirrormaker"></a><span data-ttu-id="0a1a3-191">MirrorMaker Başlat</span><span class="sxs-lookup"><span data-stu-id="0a1a3-191">Start MirrorMaker</span></span>

1. <span data-ttu-id="0a1a3-192">SSH bağlantı **hedef** küme, MirrorMaker işlemini başlatmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="0a1a3-192">From the SSH connection to the **destination** cluster, use the following command to start the MirrorMaker process:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-run-class.sh kafka.tools.MirrorMaker --consumer.config consumer.properties --producer.config producer.properties --whitelist testtopic --num.streams 4
    ```

    <span data-ttu-id="0a1a3-193">Bu örnekte kullanılan parametreler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="0a1a3-193">The parameters used in this example are:</span></span>

    * <span data-ttu-id="0a1a3-194">**--consumer.config**: tüketici özellikler içeren dosyayı belirtir.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-194">**--consumer.config**: Specifies the file that contains consumer properties.</span></span> <span data-ttu-id="0a1a3-195">Bu özellikleri okur bir tüketici oluşturmak için kullanılan *kaynak* Kafka küme.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-195">These properties are used to create a consumer that reads from the *source* Kafka cluster.</span></span>

    * <span data-ttu-id="0a1a3-196">**--producer.config**: üretici özellikler içeren dosyayı belirtir.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-196">**--producer.config**: Specifies the file that contains producer properties.</span></span> <span data-ttu-id="0a1a3-197">Bu özellikler Yazar bir üretici oluşturmak için kullanılan *hedef* Kafka küme.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-197">These properties are used to create a producer that writes to the *destination* Kafka cluster.</span></span>

    * <span data-ttu-id="0a1a3-198">**--beyaz liste**: MirrorMaker hedef kaynak kümeden çoğaltır konuların listesi.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-198">**--whitelist**: A list of topics that MirrorMaker replicates from the source cluster to the destination.</span></span>

    * <span data-ttu-id="0a1a3-199">**--num.streams**: oluşturmak için tüketici iş parçacığı sayısı.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-199">**--num.streams**: The number of consumer threads to create.</span></span>

 <span data-ttu-id="0a1a3-200">Başlangıç sırasında aşağıdaki metni benzer bilgi MirrorMaker döndürür:</span><span class="sxs-lookup"><span data-stu-id="0a1a3-200">On startup, MirrorMaker returns information similar to the following text:</span></span>

    ```json
    {metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-3, security.protocol=PLAINTEXT}{metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-0, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-kafka.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-2, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-1, security.protocol=PLAINTEXT}
    ```

2. <span data-ttu-id="0a1a3-201">SSH bağlantı **kaynak** küme, bir üretici başlatmak ve konu başlığına ileti göndermek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="0a1a3-201">From the SSH connection to the **source** cluster, use the following command to start a producer and send messages to the topic:</span></span>

    ```bash
    SOURCE_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $SOURCE_BROKERHOSTS --topic testtopic
    ```

    <span data-ttu-id="0a1a3-202">Değiştir `$PASSWORD` kaynak kümesi için oturum açma (Yönetici) parolayla.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-202">Replace `$PASSWORD` with the login (admin) password for the source cluster.</span></span>

    <span data-ttu-id="0a1a3-203">Değiştir `$CLUSTERNAME` kaynak kümesi adı.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-203">Replace `$CLUSTERNAME` with the name of the source cluster.</span></span>

     <span data-ttu-id="0a1a3-204">Boş bir satırı bir imleç ile geldiğinde, birkaç metin iletileri yazın.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-204">When you arrive at a blank line with a cursor, type in a few text messages.</span></span> <span data-ttu-id="0a1a3-205">Bu konu başlığına gönderilen **kaynak** küme.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-205">These are sent to the topic on the **source** cluster.</span></span> <span data-ttu-id="0a1a3-206">İşiniz bittiğinde, kullanın **Ctrl + C** üretici işlemi sonlandırmak için.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-206">When done, use **Ctrl + C** to end the producer process.</span></span>

3. <span data-ttu-id="0a1a3-207">SSH bağlantı **hedef** küme, kullanın **Ctrl + C** MirrorMaker işlemi sonlandırmak için.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-207">From the SSH connection to the **destination** cluster, use **Ctrl + C** to end the MirrorMaker process.</span></span> <span data-ttu-id="0a1a3-208">Doğrulamak için aşağıdaki komutları kullanın `testtopic` konu oluşturuldu ve bu verileri konusunda bu yansıtmaya çoğaltılan:</span><span class="sxs-lookup"><span data-stu-id="0a1a3-208">Then use the following commands to verify that the `testtopic` topic was created, and that data in the topic was replicated to this mirror:</span></span>

    ```bash
    DEST_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $DEST_ZKHOSTS
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $DEST_ZKHOSTS --topic testtopic --from-beginning
    ```

    <span data-ttu-id="0a1a3-209">Değiştir `$PASSWORD` hedef küme için oturum açma (Yönetici) parolayla.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-209">Replace `$PASSWORD` with the login (admin) password for the destination cluster.</span></span>

    <span data-ttu-id="0a1a3-210">Değiştir `$CLUSTERNAME` hedef küme adı.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-210">Replace `$CLUSTERNAME` with the name of the destination cluster.</span></span>

    <span data-ttu-id="0a1a3-211">Konu listesi şimdi içerir `testtopic`, hedef kaynak kümesinden konuya MirrorMaster yansıtan zaman oluşturuldu.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-211">The list of topics now includes `testtopic`, which is created when MirrorMaster mirrors the topic from the source cluster to the destination.</span></span> <span data-ttu-id="0a1a3-212">Konusundan alınan iletileri kaynak kümede girilen adıyla aynıdır.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-212">The messages retrieved from the topic are the same as entered on the source cluster.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="0a1a3-213">Küme silme</span><span class="sxs-lookup"><span data-stu-id="0a1a3-213">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="0a1a3-214">Bu belgede yer alan adımlar her iki kümeleri aynı Azure kaynak grubu oluşturmak için Azure portalında kaynak grubunu silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-214">Since the steps in this document create both clusters in the same Azure resource group, you can delete the resource group in the Azure portal.</span></span> <span data-ttu-id="0a1a3-215">Kaynak grubunun silinmesi bu belge, Azure sanal ağ ve depolama hesabı kümeleri tarafından kullanılan uygulayarak oluşturduğunuz tüm kaynakları kaldırır.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-215">Deleting the resource group removes all resources created by following this document, the Azure Virtual Network, and storage account used by the clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a1a3-216">Sonraki Adımlar</span><span class="sxs-lookup"><span data-stu-id="0a1a3-216">Next Steps</span></span>

<span data-ttu-id="0a1a3-217">Bu belgede, MirrorMaker Kafka küme bir kopyasını oluşturmak için nasıl kullanılacağı hakkında bilgi edindiniz.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-217">In this document, you learned how to use MirrorMaker to create a replica of a Kafka cluster.</span></span> <span data-ttu-id="0a1a3-218">Kafka ile çalışmak için diğer yollarını keşfetmek için aşağıdaki bağlantıları kullanın:</span><span class="sxs-lookup"><span data-stu-id="0a1a3-218">Use the following links to discover other ways to work with Kafka:</span></span>

* <span data-ttu-id="0a1a3-219">[Apache Kafka MirrorMaker belgelerine](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) cwiki.apache.org adresindeki.</span><span class="sxs-lookup"><span data-stu-id="0a1a3-219">[Apache Kafka MirrorMaker documentation](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) at cwiki.apache.org.</span></span>
* [<span data-ttu-id="0a1a3-220">Hdınsight üzerinde Apache Kafka kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="0a1a3-220">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="0a1a3-221">Apache Spark’ı HDInsight üzerinde Kafka ile kullanma</span><span class="sxs-lookup"><span data-stu-id="0a1a3-221">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="0a1a3-222">Apache Storm’u HDInsight üzerinde Kafka ile kullanma</span><span class="sxs-lookup"><span data-stu-id="0a1a3-222">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="0a1a3-223">Azure Sanal Ağ üzerinden Kafka’ya bağlanma</span><span class="sxs-lookup"><span data-stu-id="0a1a3-223">Connect to Kafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
