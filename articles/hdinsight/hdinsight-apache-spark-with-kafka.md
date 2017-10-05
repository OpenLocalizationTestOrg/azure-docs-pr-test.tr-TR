---
title: "Apache Spark, Kafka - Azure Hdınsight akış | Microsoft Docs"
description: "İçine veya dışına Apache DStreams kullanarak Kafka Spark Apache Spark veri akışı kullanmayı öğrenin. Bu örnekte, Hdınsight'ta Spark gelen Jupyter Not Defteri kullanarak veri akışı."
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
ms.openlocfilehash: 81fa319f6fb94bdabacd8f68d14b9a1063a9749a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/11/2017
---
# <a name="apache-spark-streaming-dstream-example-with-kafka-preview-on-hdinsight"></a><span data-ttu-id="c3ee3-105">Apache Spark Hdınsight üzerinde Kafka (Önizleme) ile (DStream) örnek akış</span><span class="sxs-lookup"><span data-stu-id="c3ee3-105">Apache Spark streaming (DStream) example with Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="c3ee3-106">Spark Apache Spark veri akışı içine veya dışına DStreams kullanarak Hdınsight üzerinde Apache Kafka nasıl kullanılacağını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-106">Learn how to use Spark Apache Spark to stream data into or out of Apache Kafka on HDInsight using DStreams.</span></span> <span data-ttu-id="c3ee3-107">Bu örnek, Spark kümesinde çalışan bir Jupyter not defteri kullanır.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-107">This example uses a Jupyter notebook that runs on the Spark cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="c3ee3-108">Bu belgede yer alan adımlar, hem hdınsight'ta Spark ve Hdınsight kümesinde bir Kafka içeren bir Azure kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-108">The steps in this document create an Azure resource group that contains both a Spark on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="c3ee3-109">Bu kümeleri, hem bir Azure sanal Kafka ile doğrudan iletişim kurmak Spark kümesi sağlayan ağ içinde bulunan küme ' dir.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-109">These clusters are both located within an Azure Virtual Network, which allows the Spark cluster to directly communicate with the Kafka cluster.</span></span>
>
> <span data-ttu-id="c3ee3-110">Bu belgedeki adımları tamamladığınızda, aşırı ücretlerden kaçınmak için kümelerini Sil unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-110">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span></span>

## <a name="create-the-clusters"></a><span data-ttu-id="c3ee3-111">Kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="c3ee3-111">Create the clusters</span></span>

<span data-ttu-id="c3ee3-112">Hdınsight üzerinde Apache Kafka erişim genel internet üzerinden Kafka aracıların sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-112">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span></span> <span data-ttu-id="c3ee3-113">İçin Kafka ettiği herhangi bir şey Kafka kümedeki düğümlerin aynı Azure sanal ağ içinde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-113">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="c3ee3-114">Bu örnekte, bir Azure sanal ağında Kafka ve Spark kümeleri bulunur.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-114">For this example, both the Kafka and Spark clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="c3ee3-115">Aşağıdaki diyagramda, iletişim kümeleri arasında nasıl aktığını gösterir:</span><span class="sxs-lookup"><span data-stu-id="c3ee3-115">The following diagram shows how communication flows between the clusters:</span></span>

![Bir Azure sanal ağı Spark ve Kafka kümelerde diyagramı](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="c3ee3-117">Kafka kendi sanal ağ içinde iletişimi sınırlı olsa da, SSH ve Ambari gibi kümedeki diğer hizmetlerin internet üzerinden erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-117">Though Kafka itself is limited to communication within the virtual network, other services on the cluster such as SSH and Ambari can be accessed over the internet.</span></span> <span data-ttu-id="c3ee3-118">Hdınsight ile kullanılabilen ortak bağlantı noktaları hakkında daha fazla bilgi için bkz: [bağlantı noktaları ve Hdınsight tarafından kullanılan URI](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="c3ee3-118">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="c3ee3-119">Azure sanal ağı, Kafka, oluşturabilir ve el ile Spark kümeleri olsa da, bir Azure Resource Manager şablonunu kullanmak daha kolaydır.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-119">While you can create an Azure virtual network, Kafka, and Spark clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="c3ee3-120">Azure sanal ağı, Kafka, dağıtmak ve Spark kümeleri Azure aboneliğiniz için aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-120">Use the following steps to deploy an Azure virtual network, Kafka, and Spark clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="c3ee3-121">Azure'da oturum açın ve Azure portalında şablon açmak için aşağıdaki düğmesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-121">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy to Azure"></a>
    
    <span data-ttu-id="c3ee3-122">Azure Resource Manager şablonu bulunur **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-122">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="c3ee3-123">HDInsight üzerinde Kafka'yı kullanabilmeniz için kümenizin en az üç çalışan düğümü içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-123">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="c3ee3-124">Bu şablon, üç alt düğümleri içeren bir Kafka küme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-124">This template creates a Kafka cluster that contains three worker nodes.</span></span>

    <span data-ttu-id="c3ee3-125">Bu şablon, Kafka hem Spark Hdınsight 3.6 küme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-125">This template creates an HDInsight 3.6 cluster for both Kafka and Spark.</span></span>

2. <span data-ttu-id="c3ee3-126">Üzerinde girişleri doldurmak için aşağıdaki bilgileri kullanın **özel dağıtım** dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="c3ee3-126">Use the following information to populate the entries on the **Custom deployment** blade:</span></span>
   
    ![Hdınsight özel dağıtım](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * <span data-ttu-id="c3ee3-128">**Kaynak grubu**: bir grup oluşturun veya varolan bir tanesini seçin.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-128">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="c3ee3-129">Bu grup, Hdınsight kümesi içerir.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-129">This group contains the HDInsight cluster.</span></span>

    * <span data-ttu-id="c3ee3-130">**Konum**: coğrafi olarak yakın bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-130">**Location**: Select a location geographically close to you.</span></span>

    * <span data-ttu-id="c3ee3-131">**Temel küme adı**: Bu değer Spark temel adı olarak kullanılır ve Kafka kümeleri.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-131">**Base Cluster Name**: This value is used as the base name for the Spark and Kafka clusters.</span></span> <span data-ttu-id="c3ee3-132">Örneğin, **hdı** bir Spark spark hdi__ adlı Küme ve adlı bir Kafka kümesi oluşturur **kafka hdı**.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-132">For example, entering **hdi** creates a Spark cluster named spark-hdi__ and a Kafka cluster named **kafka-hdi**.</span></span>

    * <span data-ttu-id="c3ee3-133">**Oturum açma kullanıcı adı küme**: Spark ve Kafka kümeleri için yönetici kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-133">**Cluster Login User Name**: The admin user name for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="c3ee3-134">**Oturum açma parolası küme**: Spark ve Kafka kümeleri için yönetici kullanıcı parolası.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-134">**Cluster Login Password**: The admin user password for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="c3ee3-135">**SSH kullanıcı adı**: için Spark ve Kafka kümeleri oluşturmak için SSH kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-135">**SSH User Name**: The SSH user to create for the Spark and Kafka clusters.</span></span>

    * <span data-ttu-id="c3ee3-136">**SSH parolası**: Spark ve Kafka kümelerinin SSH kullanıcısının parolası.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-136">**SSH Password**: The password for the SSH user for the Spark and Kafka clusters.</span></span>

3. <span data-ttu-id="c3ee3-137">Okuma **hüküm ve koşullar**ve ardından **hüküm ve koşulları yukarıda belirtildiği ediyorum**.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-137">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="c3ee3-138">Son olarak, denetleme **panoya Sabitle** ve ardından **satın alma**.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-138">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="c3ee3-139">Kümeleri oluşturmak için yaklaşık 20 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-139">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="c3ee3-140">Kaynakları oluşturduktan sonra kümeler ve web Pano içeren kaynak grubu için bir dikey penceresine yönlendirilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-140">Once the resources have been created, you are redirected to a blade for the resource group that contains the clusters and web dashboard.</span></span>

![Kaynak grubu dikey vnet ve kümeler için](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="c3ee3-142">Hdınsight kümeleri adlarının bildirimi **spark BASENAME** ve **kafka BASENAME**, BASENAME şablona verdiğiniz adı olduğu.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-142">Notice that the names of the HDInsight clusters are **spark-BASENAME** and **kafka-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="c3ee3-143">Kümeye bağlanırken bu adları daha sonraki adımlarda kullanın.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-143">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="use-the-notebooks"></a><span data-ttu-id="c3ee3-144">Not defterlerini kullanma</span><span class="sxs-lookup"><span data-stu-id="c3ee3-144">Use the notebooks</span></span>

<span data-ttu-id="c3ee3-145">Bu belgede açıklanan örnek kodunu şu adresten edinilebilir [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span><span class="sxs-lookup"><span data-stu-id="c3ee3-145">The code for the example described in this document is available at [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).</span></span>

<span data-ttu-id="c3ee3-146">Adımları `README.md` Bu örnek tamamlamak için dosya.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-146">Follow the steps in the `README.md` file to complete this example.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="c3ee3-147">Küme silme</span><span class="sxs-lookup"><span data-stu-id="c3ee3-147">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="c3ee3-148">Bu belgede yer alan adımlar her iki kümeleri aynı Azure kaynak grubu oluşturmak için Azure portalında kaynak grubunu silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-148">Since the steps in this document create both clusters in the same Azure resource group, you can delete the resource group in the Azure portal.</span></span> <span data-ttu-id="c3ee3-149">Grup silindiğinde, bu belge, Azure sanal ağ ve depolama hesabı kümeleri tarafından kullanılan uygulayarak oluşturduğunuz tüm kaynakları kaldırır.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-149">Deleting the group removes all resources created by following this document, the Azure Virtual Network, and storage account used by the clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3ee3-150">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="c3ee3-150">Next steps</span></span>

<span data-ttu-id="c3ee3-151">Bu örnekte, Spark okumak ve yazmak için Kafka için nasıl kullanılacağı hakkında bilgi edindiniz.</span><span class="sxs-lookup"><span data-stu-id="c3ee3-151">In this example, you learned how to use Spark to read and write to Kafka.</span></span> <span data-ttu-id="c3ee3-152">Kafka ile çalışmak için diğer yollarını keşfetmek için aşağıdaki bağlantıları kullanın:</span><span class="sxs-lookup"><span data-stu-id="c3ee3-152">Use the following links to discover other ways to work with Kafka:</span></span>

* [<span data-ttu-id="c3ee3-153">Hdınsight üzerinde Apache Kafka kullanmaya başlama</span><span class="sxs-lookup"><span data-stu-id="c3ee3-153">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="c3ee3-154">MirrorMaker kullanarak HDInsight üzerinde Kafka kopyası oluşturma</span><span class="sxs-lookup"><span data-stu-id="c3ee3-154">Use MirrorMaker to create a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="c3ee3-155">Apache Storm’u HDInsight üzerinde Kafka ile kullanma</span><span class="sxs-lookup"><span data-stu-id="c3ee3-155">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)

