---
title: "aaaApache Spark Kafka - Azure Hdınsight akış | Microsoft Docs"
description: "Bilgi nasıl toouse Spark Apache Spark toostream veri ya da Apache DStreams kullanarak Kafka dışında. Bu örnekte, Hdınsight'ta Spark gelen Jupyter Not Defteri kullanarak veri akışı."
keywords: "kafka örnek, kafka zookeeper spark kafka, kafka örnek Spark Akış akış"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: dd8f53c1-bdee-4921-b683-3be4c46c2039
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: f48b37aadafa4979cd27af68e8417db6acc8a0e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-dstream-example-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="9e7b8-105">Apache Spark Hdınsight üzerinde Kafka (Önizleme) ile (DStream) örnek akış</span><span class="sxs-lookup"><span data-stu-id="9e7b8-105">Apache Spark streaming (DStream) example with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="9e7b8-106">Bilgi nasıl toouse Spark Apache Spark toostream veri içine veya dışına DStreams kullanarak Hdınsight üzerinde Apache Kafka.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-106">Learn how toouse Spark Apache Spark toostream data into or out of Apache Kafka on HDInsight using DStreams.</span></span> <span data-ttu-id="9e7b8-107">Bu örnek hello Spark kümesinde çalışan bir Jupyter not defteri kullanır.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-107">This example uses a Jupyter notebook that runs on hello Spark cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="9e7b8-108">Bu belgedeki Hello adımlar hem hdınsight'ta Spark ve Hdınsight kümesinde bir Kafka içeren bir Azure kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-108">hello steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="9e7b8-109">Bu kümeleri, hem bir Azure sanal hello Spark küme toodirectly sağlayan ağ içinde bulunan Kafka küme hello ile iletişim ' dir.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-109">These clusters are both located within an Azure Virtual Network, which allows hello Spark cluster toodirectly communicate with hello Kafka cluster.</span></span>
>
> <span data-ttu-id="9e7b8-110">Bu belgedeki hello adımları tamamladığınızda, toodelete hello kümeleri tooavoid aşırı ücretleri unutmayın.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-110">When you are done with hello steps in this document, remember toodelete hello clusters tooavoid excess charges.</span></span>

## <a name="create-hello-clusters"></a><span data-ttu-id="9e7b8-111">Merhaba kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="9e7b8-111">Create hello clusters</span></span>

<span data-ttu-id="9e7b8-112">Hdınsight üzerinde Apache Kafka sağlamaz erişim toohello Kafka aracıların üzerinden genel internet hello.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-112">Apache Kafka on HDInsight does not provide access toohello Kafka brokers over hello public internet.</span></span> <span data-ttu-id="9e7b8-113">Merhaba düğümler aynı Azure sanal ağ konuşmaları tooKafka olmalıdır hello herhangi bir şey Kafka küme hello.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-113">Anything that talks tooKafka must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="9e7b8-114">Bu örnekte, bir Azure sanal ağında hello Kafka ve Spark kümeleri bulunur.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-114">For this example, both hello Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="9e7b8-115">Merhaba Aşağıdaki diyagramda hello kümeleri arasında iletişimi nasıl akacağını gösterilmektedir:</span><span class="sxs-lookup"><span data-stu-id="9e7b8-115">hello following diagram shows how communication flows between hello clusters:</span></span>

![Bir Azure sanal ağı Spark ve Kafka kümelerde diyagramı](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="9e7b8-117">Kafka kendisini hello sanal ağ içindeki sınırlı toocommunication olsa da, SSH ve Ambari üzerinden erişilebilen gibi diğer hizmetler hello kümede Internet hello.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-117">Though Kafka itself is limited toocommunication within hello virtual network, other services on hello cluster such as SSH and Ambari can be accessed over hello internet.</span></span> <span data-ttu-id="9e7b8-118">Merhaba ortak bağlantı noktaları Hdınsight ile kullanılabilir hakkında daha fazla bilgi için bkz: [bağlantı noktaları ve Hdınsight tarafından kullanılan URI](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="9e7b8-118">For more information on hello public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="9e7b8-119">Azure sanal ağı, Kafka ve Spark kümeleri el ile oluşturabileceğiniz olsa da, daha kolay toouse bir Azure Resource Manager şablonu durumdur.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-119">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="9e7b8-120">Toodeploy Azure sanal ağı, Kafka, kullanım hello aşağıdaki adımları ve tooyour Azure aboneliği Spark kümeleri.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-120">Use hello following steps toodeploy an Azure virtual network, Kafka, and Spark clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="9e7b8-121">Düğme toosign tooAzure içinde ve açık hello şablonunda hello Azure portalı aşağıdaki hello kullanın.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-121">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    <span data-ttu-id="9e7b8-122">Hello Azure Resource Manager şablonu konumundadır **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-122">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="9e7b8-123">Hdınsight üzerinde Kafka kullanılabilirliğini tooguarantee, kümenizi en az üç alt düğümleri içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-123">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="9e7b8-124">Bu şablon, üç alt düğümleri içeren bir Kafka küme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-124">This template creates a Kafka cluster that contains three worker nodes.</span></span>

    <span data-ttu-id="9e7b8-125">Bu şablon, Kafka hem Spark Hdınsight 3.6 küme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-125">This template creates an HDInsight 3.6 cluster for both Kafka and Spark.</span></span>

2. <span data-ttu-id="9e7b8-126">Bilgi toopopulate hello girişleri hello üzerinde aşağıdaki kullanım hello **özel dağıtım** dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="9e7b8-126">Use hello following information toopopulate hello entries on hello **Custom deployment** blade:</span></span>
   
    ![Hdınsight özel dağıtım](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="9e7b8-128">**Kaynak grubu**: bir grup oluşturun veya varolan bir tanesini seçin.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-128">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="9e7b8-129">Bu grup hello Hdınsight kümesi içerir.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-129">This group contains hello HDInsight cluster.</span></span>

    * <span data-ttu-id="9e7b8-130">**Konum**: konum coğrafi olarak Kapat tooyou seçin.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-130">**Location**: Select a location geographically close tooyou.</span></span>

    * <span data-ttu-id="9e7b8-131">**Temel küme adı**: Bu değer hello Spark ve Kafka kümelerinin hello temel adı olarak kullanılır.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-131">**Base Cluster Name**: This value is used as hello base name for hello Spark and Kafka clusters.</span></span> <span data-ttu-id="9e7b8-132">Örneğin, **hdı** bir Spark spark hdi__ adlı Küme ve adlı bir Kafka kümesi oluşturur **kafka hdı**.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-132">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="9e7b8-133">**Oturum açma kullanıcı adı küme**: hello Spark ve Kafka kümelerinin hello Yöneticisi kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-133">**Cluster Login User Name**: hello admin user name for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="9e7b8-134">**Oturum açma parolası küme**: hello Spark ve Kafka kümeleri için hello yönetici kullanıcı parolası.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-134">**Cluster Login Password**: hello admin user password for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="9e7b8-135">**SSH kullanıcı adı**: SSH kullanıcı toocreate hello Spark ve Kafka kümelerinin hello.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-135">**SSH User Name**: hello SSH user toocreate for hello Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="9e7b8-136">**SSH parolası**: hello SSH kullanıcı hello Spark ve Kafka kümelerinin hello parolası.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-136">**SSH Password**: hello password for hello SSH user for hello Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="9e7b8-137">Okuma hello **hüküm ve koşullar**ve ardından **toohello hüküm ve koşullar yukarıda belirtildiği kabul**.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-137">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="9e7b8-138">Son olarak, denetleme **PIN toodashboard** ve ardından **satın alma**.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-138">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="9e7b8-139">Merhaba kümeleri toocreate yaklaşık 20 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-139">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="9e7b8-140">Merhaba kaynakları oluşturduktan sonra yeniden yönlendirilen tooa dikey penceresinde hello kümeleri ve web Pano içeren hello kaynak grubu için demektir.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-140">Once hello resources have been created, you are redirected tooa blade for hello resource group that contains hello clusters and web dashboard.</span></span>

![Kaynak grubu dikey hello vnet ve kümeler için](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="9e7b8-142">Merhaba Hdınsight kümeleri Hello adlarını olduğuna dikkat edin **spark BASENAME** ve **kafka BASENAME**, BASENAME toohello şablonu sağladığınız hello adı olduğu.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-142">Notice that hello names of hello HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="9e7b8-143">Bu adları toohello kümeleri bağlanırken daha sonraki adımlarda kullanın.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-143">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="use-hello-notebooks"></a><span data-ttu-id="9e7b8-144">Merhaba not defterlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="9e7b8-144">Use hello notebooks</span></span>

<span data-ttu-id="9e7b8-145">Bu belgede açıklanan hello örneğin Hello kod şu adreste [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span><span class="sxs-lookup"><span data-stu-id="9e7b8-145">hello code for hello example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span></span>

<span data-ttu-id="9e7b8-146">Merhaba Hello adımları `README.md` toocomplete Bu örnek dosya.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-146">Follow hello steps in hello `README.md` file toocomplete this example.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="9e7b8-147">Merhaba küme silme</span><span class="sxs-lookup"><span data-stu-id="9e7b8-147">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="9e7b8-148">Merhaba adımlar bu belgedeki her ikisi de oluşturma beri kümelerde Merhaba aynı Azure kaynak grubu, hello Azure portal hello kaynak grubunu silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-148">Since hello steps in this document create both clusters in hello same Azure resource group, you can delete hello resource group in hello Azure portal.</span></span> <span data-ttu-id="9e7b8-149">Bu belge, hello Azure sanal ağ ve depolama hesabı hello kümeleri tarafından kullanılan uygulayarak oluşturduğunuz tüm kaynakları silme hello grubunu kaldırır.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-149">Deleting hello group removes all resources created by following this document, hello Azure Virtual Network, and storage account used by hello clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e7b8-150">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="9e7b8-150">Next steps</span></span>

<span data-ttu-id="9e7b8-151">Bu örnekte, nasıl toouse tooread Spark ve tooKafka yazma öğrendiniz.</span><span class="sxs-lookup"><span data-stu-id="9e7b8-151">In this example, you learned how toouse Spark tooread and write tooKafka.</span></span> <span data-ttu-id="9e7b8-152">Aşağıdaki bağlantılar toodiscover hello diğer yolları toowork Kafka ile kullanın:</span><span class="sxs-lookup"><span data-stu-id="9e7b8-152">Use hello following links toodiscover other ways toowork with Kafka:</span></span>

* [<span data-ttu-id="9e7b8-153">Hdınsight üzerinde Apache Kafka kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="9e7b8-153">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="9e7b8-154">Hdınsight üzerinde MirrorMaker toocreate Kafka bir kopyasını kullan</span><span class="sxs-lookup"><span data-stu-id="9e7b8-154">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="9e7b8-155">Apache Storm’u HDInsight üzerinde Kafka ile kullanma</span><span class="sxs-lookup"><span data-stu-id="9e7b8-155">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)

