---
title: "Storm hdınsight'ta - Azure Apache Kafka kullanın | Microsoft Docs"
description: "Apache Kafka, Hdınsight üzerinde Apache Storm ile yüklenir. Kafka için yazma ve ondan, Storm ile sağlanan KafkaBolt ve KafkaSpout Bileşenleri'ni kullanarak okunur öğrenin. Ayrıca Flux framework tanımlayın ve Storm topolojilerini göndermek için nasıl kullanılacağını öğrenin."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e4941329-1580-4cd8-b82e-a2258802c1a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/21/2017
ms.author: larryfr
ms.openlocfilehash: e8895ef3c11aea48513e4060a20f5f49b11fc961
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/18/2017
---
# <a name="use-apache-kafka-preview-with-storm-on-hdinsight"></a><span data-ttu-id="da65a-105">Hdınsight üzerinde Storm ile Apache Kafka (Önizleme) kullanın</span><span class="sxs-lookup"><span data-stu-id="da65a-105">Use Apache Kafka (preview) with Storm on HDInsight</span></span>

<span data-ttu-id="da65a-106">Apache Storm okuma ve yazma Apache Kafka için nasıl kullanılacağını öğrenin.</span><span class="sxs-lookup"><span data-stu-id="da65a-106">Learn how to use Apache Storm to read from and write to Apache Kafka.</span></span> <span data-ttu-id="da65a-107">Bu örnek ayrıca bir Storm topolojisinin verilerden Hdınsight tarafından kullanılan HDFS uyumlu dosya sistemine kaydetmek nasıl gösterir.</span><span class="sxs-lookup"><span data-stu-id="da65a-107">This example also demonstrates how to save data from a Storm topology to the HDFS-compatible file system used by HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="da65a-108">Bu belgede yer alan adımlar, hem Hdınsight üzerinde Storm ve Hdınsight kümesinde bir Kafka içeren bir Azure kaynak grubu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="da65a-108">The steps in this document create an Azure resource group that contains both a Storm on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="da65a-109">Bu kümeleri, hem bir Azure sanal Kafka ile doğrudan iletişim kurmak Storm kümesi sağlayan ağ içinde bulunan küme ' dir.</span><span class="sxs-lookup"><span data-stu-id="da65a-109">These clusters are both located within an Azure Virtual Network, which allows the Storm cluster to directly communicate with the Kafka cluster.</span></span>
> 
> <span data-ttu-id="da65a-110">Bu belgedeki adımları tamamladığınızda, aşırı ücretlerden kaçınmak için kümelerini Sil unutmayın.</span><span class="sxs-lookup"><span data-stu-id="da65a-110">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="da65a-111">Kodu alma</span><span class="sxs-lookup"><span data-stu-id="da65a-111">Get the code</span></span>

<span data-ttu-id="da65a-112">Bu belgede kullanılan örnek kodunu şu adresten edinilebilir [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span><span class="sxs-lookup"><span data-stu-id="da65a-112">The code for the example used in this document is available at [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span></span>

<span data-ttu-id="da65a-113">Bu projeyi derlemek için geliştirme ortamınız için aşağıdaki yapılandırma gerekir:</span><span class="sxs-lookup"><span data-stu-id="da65a-113">To compile this project, you need the following configuration for your development environment:</span></span>

* <span data-ttu-id="da65a-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ya da daha yüksek.</span><span class="sxs-lookup"><span data-stu-id="da65a-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="da65a-115">Java 8 Hdınsight 3.5 veya daha yükseğini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="da65a-115">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="da65a-116">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="da65a-116">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

* <span data-ttu-id="da65a-117">Bir SSH istemcisi (ihtiyacınız `ssh` ve `scp` komutları) - bilgi için bkz: [Hdınsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="da65a-117">An SSH client (you need the `ssh` and `scp` commands) - For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="da65a-118">Bir metin düzenleyicisi veya IDE.</span><span class="sxs-lookup"><span data-stu-id="da65a-118">A text editor or IDE.</span></span>

<span data-ttu-id="da65a-119">Geliştirme iş istasyonunuza Java ve JDK yüklediğinizde aşağıdaki ortam değişkenleri ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da65a-119">The following environment variables may be set when you install Java and the JDK on your development workstation.</span></span> <span data-ttu-id="da65a-120">Ancak, bunlar mevcut olduğundan ve sisteminiz için doğru değerleri içerdikleri denetlemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="da65a-120">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="da65a-121">`JAVA_HOME`-JDK yüklendiği dizinine işaret etmelidir.</span><span class="sxs-lookup"><span data-stu-id="da65a-121">`JAVA_HOME` - should point to the directory where the JDK is installed.</span></span>
* <span data-ttu-id="da65a-122">`PATH`-aşağıdaki yolları içermelidir:</span><span class="sxs-lookup"><span data-stu-id="da65a-122">`PATH` - should contain the following paths:</span></span>
  
    * <span data-ttu-id="da65a-123">`JAVA_HOME`(veya eşdeğer yolu).</span><span class="sxs-lookup"><span data-stu-id="da65a-123">`JAVA_HOME` (or the equivalent path).</span></span>
    * <span data-ttu-id="da65a-124">`JAVA_HOME\bin`(veya eşdeğer yolu).</span><span class="sxs-lookup"><span data-stu-id="da65a-124">`JAVA_HOME\bin` (or the equivalent path).</span></span>
    * <span data-ttu-id="da65a-125">Maven'ın yüklendiği dizin.</span><span class="sxs-lookup"><span data-stu-id="da65a-125">The directory where Maven is installed.</span></span>

## <a name="create-the-clusters"></a><span data-ttu-id="da65a-126">Kümeleri oluşturma</span><span class="sxs-lookup"><span data-stu-id="da65a-126">Create the clusters</span></span>

<span data-ttu-id="da65a-127">Hdınsight üzerinde Apache Kafka erişim genel internet üzerinden Kafka aracıların sağlamaz.</span><span class="sxs-lookup"><span data-stu-id="da65a-127">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span></span> <span data-ttu-id="da65a-128">İçin Kafka ettiği herhangi bir şey Kafka kümedeki düğümlerin aynı Azure sanal ağ içinde olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="da65a-128">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="da65a-129">Bu örnekte, bir Azure sanal ağında Kafka ve Storm kümeleri bulunur.</span><span class="sxs-lookup"><span data-stu-id="da65a-129">For this example, both the Kafka and Storm clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="da65a-130">Aşağıdaki diyagramda, iletişim kümeleri arasında nasıl aktığını gösterir:</span><span class="sxs-lookup"><span data-stu-id="da65a-130">The following diagram shows how communication flows between the clusters:</span></span>

![Bir Azure sanal ağı Storm ve Kafka kümelerde diyagramı](./media/hdinsight-apache-storm-with-kafka/storm-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="da65a-132">SSH ve Ambari gibi kümedeki diğer hizmetlerin internet üzerinden erişilebilir.</span><span class="sxs-lookup"><span data-stu-id="da65a-132">Other services on the cluster such as SSH and Ambari can be accessed over the internet.</span></span> <span data-ttu-id="da65a-133">Hdınsight ile kullanılabilen ortak bağlantı noktaları hakkında daha fazla bilgi için bkz: [bağlantı noktaları ve Hdınsight tarafından kullanılan URI](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="da65a-133">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="da65a-134">Azure sanal ağı, Kafka, oluşturabilir ve Storm el ile kümeleri olsa da, bir Azure Resource Manager şablonunu kullanmak daha kolaydır.</span><span class="sxs-lookup"><span data-stu-id="da65a-134">While you can create an Azure virtual network, Kafka, and Storm clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="da65a-135">Azure sanal ağı, Kafka, dağıtmak ve kümeler Azure aboneliğinize Storm için aşağıdaki adımları kullanın.</span><span class="sxs-lookup"><span data-stu-id="da65a-135">Use the following steps to deploy an Azure virtual network, Kafka, and Storm clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="da65a-136">Azure'da oturum açın ve Azure portalında şablon açmak için aşağıdaki düğmesini kullanın.</span><span class="sxs-lookup"><span data-stu-id="da65a-136">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-storm-cluster-in-vnet-v2.json" target="_blank"><img src="./media/hdinsight-apache-storm-with-kafka/deploy-to-azure.png" alt="Deploy to Azure"></a>
   
    <span data-ttu-id="da65a-137">Azure Resource Manager şablonu bulunur **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**.</span><span class="sxs-lookup"><span data-stu-id="da65a-137">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**.</span></span> <span data-ttu-id="da65a-138">Aşağıdaki kaynaklar oluşturur:</span><span class="sxs-lookup"><span data-stu-id="da65a-138">It creates the following resources:</span></span>
    
    * <span data-ttu-id="da65a-139">Azure kaynak grubu</span><span class="sxs-lookup"><span data-stu-id="da65a-139">Azure resource group</span></span>
    * <span data-ttu-id="da65a-140">Azure Sanal Ağ</span><span class="sxs-lookup"><span data-stu-id="da65a-140">Azure Virtual Network</span></span>
    * <span data-ttu-id="da65a-141">Azure Storage hesabı</span><span class="sxs-lookup"><span data-stu-id="da65a-141">Azure Storage account</span></span>
    * <span data-ttu-id="da65a-142">Hdınsight sürüm 3.6 (üç alt düğümleri) üzerindeki Kafka</span><span class="sxs-lookup"><span data-stu-id="da65a-142">Kafka on HDInsight version 3.6 (three worker nodes)</span></span>
    * <span data-ttu-id="da65a-143">Sürüm 3.6 (üç alt düğümler) hdınsight'ta Storm</span><span class="sxs-lookup"><span data-stu-id="da65a-143">Storm on HDInsight version 3.6 (three worker nodes)</span></span>

  > [!WARNING]
  > <span data-ttu-id="da65a-144">HDInsight üzerinde Kafka'yı kullanabilmeniz için kümenizin en az üç çalışan düğümü içermesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="da65a-144">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="da65a-145">Bu şablon, üç alt düğümleri içeren bir Kafka küme oluşturur.</span><span class="sxs-lookup"><span data-stu-id="da65a-145">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="da65a-146">Üzerinde girişleri doldurmak için aşağıdaki yönergeleri kullanın **özel dağıtım** dikey penceresinde:</span><span class="sxs-lookup"><span data-stu-id="da65a-146">Use the following guidance to populate the entries on the **Custom deployment** blade:</span></span>
   
    ![Hdınsight özel dağıtım](./media/hdinsight-apache-storm-with-kafka/parameters.png)

    * <span data-ttu-id="da65a-148">**Kaynak grubu**: bir grup oluşturun veya varolan bir tanesini seçin.</span><span class="sxs-lookup"><span data-stu-id="da65a-148">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="da65a-149">Bu grup, Hdınsight kümesi içerir.</span><span class="sxs-lookup"><span data-stu-id="da65a-149">This group contains the HDInsight cluster.</span></span>
   
    * <span data-ttu-id="da65a-150">**Konum**: coğrafi olarak yakın bir konum seçin.</span><span class="sxs-lookup"><span data-stu-id="da65a-150">**Location**: Select a location geographically close to you.</span></span>

    * <span data-ttu-id="da65a-151">**Temel küme adı**: Bu değer Storm için temel adı olarak kullanılır ve Kafka kümeleri.</span><span class="sxs-lookup"><span data-stu-id="da65a-151">**Base Cluster Name**: This value is used as the base name for the Storm and Kafka clusters.</span></span> <span data-ttu-id="da65a-152">Örneğin, **hdı** adlı bir Storm kümesi oluşturur **storm hdı** ve adlı Kafka küme **kafka hdı**.</span><span class="sxs-lookup"><span data-stu-id="da65a-152">For example, entering **hdi** creates a Storm cluster named **storm-hdi** and a Kafka cluster named **kafka-hdi**.</span></span>
   
    * <span data-ttu-id="da65a-153">**Oturum açma kullanıcı adı küme**: Storm ve Kafka kümeleri için yönetici kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="da65a-153">**Cluster Login User Name**: The admin user name for the Storm and Kafka clusters.</span></span>
   
    * <span data-ttu-id="da65a-154">**Oturum açma parolası küme**: Storm ve Kafka kümeleri için yönetici kullanıcı parolası.</span><span class="sxs-lookup"><span data-stu-id="da65a-154">**Cluster Login Password**: The admin user password for the Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="da65a-155">**SSH kullanıcı adı**: için Storm ve Kafka kümeleri oluşturmak için SSH kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="da65a-155">**SSH User Name**: The SSH user to create for the Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="da65a-156">**SSH parolası**: Storm ve Kafka kümelerinin SSH kullanıcısının parolası.</span><span class="sxs-lookup"><span data-stu-id="da65a-156">**SSH Password**: The password for the SSH user for the Storm and Kafka clusters.</span></span>

3. <span data-ttu-id="da65a-157">Okuma **hüküm ve koşullar**ve ardından **hüküm ve koşulları yukarıda belirtildiği ediyorum**.</span><span class="sxs-lookup"><span data-stu-id="da65a-157">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="da65a-158">Son olarak, denetleme **panoya Sabitle** ve ardından **satın alma**.</span><span class="sxs-lookup"><span data-stu-id="da65a-158">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="da65a-159">Kümeleri oluşturmak için yaklaşık 20 dakika sürer.</span><span class="sxs-lookup"><span data-stu-id="da65a-159">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="da65a-160">Kaynakları oluşturduktan sonra kaynak grubu dikey penceresinde görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="da65a-160">Once the resources have been created, the blade for the resource group is displayed.</span></span>

![Kaynak grubu dikey vnet ve kümeler için](./media/hdinsight-apache-storm-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="da65a-162">Hdınsight kümeleri adlarının bildirimi **storm BASENAME** ve **kafka BASENAME**, BASENAME şablona verdiğiniz adı olduğu.</span><span class="sxs-lookup"><span data-stu-id="da65a-162">Notice that the names of the HDInsight clusters are **storm-BASENAME** and **kafka-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="da65a-163">Kümeye bağlanırken bu adları daha sonraki adımlarda kullanın.</span><span class="sxs-lookup"><span data-stu-id="da65a-163">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="understanding-the-code"></a><span data-ttu-id="da65a-164">Kodu anlama</span><span class="sxs-lookup"><span data-stu-id="da65a-164">Understanding the code</span></span>

<span data-ttu-id="da65a-165">Bu proje iki topoloji içerir:</span><span class="sxs-lookup"><span data-stu-id="da65a-165">This project contains two topologies:</span></span>

* <span data-ttu-id="da65a-166">**KafkaWriter**: tarafından tanımlanan **writer.yaml** dosyası, bu topoloji Yazar rastgele cümleleri Kafka için Apache Storm ile sağlanan KafkaBolt kullanarak.</span><span class="sxs-lookup"><span data-stu-id="da65a-166">**KafkaWriter**: Defined by the **writer.yaml** file, this topology writes random sentences to Kafka using the KafkaBolt provided with Apache Storm.</span></span>

    <span data-ttu-id="da65a-167">Bu topoloji bir özel kullanan **SentenceSpout** rastgele cümleleri oluşturmak için bileşen.</span><span class="sxs-lookup"><span data-stu-id="da65a-167">This topology uses a custom **SentenceSpout** component to generate random sentences.</span></span>

* <span data-ttu-id="da65a-168">**KafkaReader**: tarafından tanımlanan **reader.yaml** dosyası, bu topoloji Kafka Apache Storm ile sağlanan KafkaSpout kullanarak verileri okur ve sonra stdout verilerini kaydeder.</span><span class="sxs-lookup"><span data-stu-id="da65a-168">**KafkaReader**: Defined by the **reader.yaml** file, this topology reads data from Kafka using the KafkaSpout provided with Apache Storm, then logs the data to stdout.</span></span>

    <span data-ttu-id="da65a-169">Bu topoloji Storm HdfsBolt Storm kümesi için varsayılan depolama verileri yazmak için kullanır.</span><span class="sxs-lookup"><span data-stu-id="da65a-169">This topology uses the Storm HdfsBolt to write data to default storage for the Storm cluster.</span></span>
### <a name="flux"></a><span data-ttu-id="da65a-170">Flux</span><span class="sxs-lookup"><span data-stu-id="da65a-170">Flux</span></span>

<span data-ttu-id="da65a-171">Topolojileri kullanılarak tanımlanır [Flux](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="da65a-171">The topologies are defined using [Flux](https://storm.apache.org/releases/1.1.0/flux.html).</span></span> <span data-ttu-id="da65a-172">Flux içinde sunulmuştur 0.10.x Storm ve kodun topoloji yapılandırması ayrı olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="da65a-172">Flux was introduced in Storm 0.10.x and allows you to separate the topology configuration from the code.</span></span> <span data-ttu-id="da65a-173">Flux framework kullanan Topolojileri için topoloji YAML dosyasında tanımlanır.</span><span class="sxs-lookup"><span data-stu-id="da65a-173">For Topologies that use the Flux framework, the topology is defined in a YAML file.</span></span> <span data-ttu-id="da65a-174">YAML dosya topolojisini bir parçası olarak dahil edilebilir.</span><span class="sxs-lookup"><span data-stu-id="da65a-174">The YAML file can be included as part of the topology.</span></span> <span data-ttu-id="da65a-175">Bu topoloji gönderdiğinizde kullanılan tek başına dosya de olabilir.</span><span class="sxs-lookup"><span data-stu-id="da65a-175">It can also be a standalone file used when you submit the topology.</span></span> <span data-ttu-id="da65a-176">Flux çalışma zamanında Bu örnekte kullanılan, değişkeni değiştirme de destekler.</span><span class="sxs-lookup"><span data-stu-id="da65a-176">Flux also supports variable substitution at run-time, which is used in this example.</span></span>

<span data-ttu-id="da65a-177">Aşağıdaki parametreleri bu topolojiler için çalışma zamanında ayarlanır:</span><span class="sxs-lookup"><span data-stu-id="da65a-177">The following parameters are set at run time for these topologies:</span></span>

* <span data-ttu-id="da65a-178">`${kafka.topic}`: Topolojileri okuma/yazma için Kafka konu adı.</span><span class="sxs-lookup"><span data-stu-id="da65a-178">`${kafka.topic}`: The name of the Kafka topic that the topologies read/write to.</span></span>

* <span data-ttu-id="da65a-179">`${kafka.broker.hosts}`: Kafka aracıların konakları çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="da65a-179">`${kafka.broker.hosts}`: The hosts that the Kafka brokers run on.</span></span> <span data-ttu-id="da65a-180">Aracısı bilgileri tarafından KafkaBolt için Kafka yazılırken kullanılır.</span><span class="sxs-lookup"><span data-stu-id="da65a-180">The broker information is used by the KafkaBolt when writing to Kafka.</span></span>

* <span data-ttu-id="da65a-181">`${kafka.zookeeper.hosts}`: Zookeeper Kafka kümesinde çalışır ana bilgisayar.</span><span class="sxs-lookup"><span data-stu-id="da65a-181">`${kafka.zookeeper.hosts}`: The hosts that Zookeeper runs on in the Kafka cluster.</span></span>

<span data-ttu-id="da65a-182">Flux topolojileri hakkında daha fazla bilgi için bkz: [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="da65a-182">For more information on Flux topologies, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="download-and-compile-the-project"></a><span data-ttu-id="da65a-183">Karşıdan yükle ve projeyi derleme</span><span class="sxs-lookup"><span data-stu-id="da65a-183">Download and compile the project</span></span>

1. <span data-ttu-id="da65a-184">Geliştirme ortamınızı projesinden indirmeniz [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), bir komut satırı açın ve dizinleri proje indirdiğiniz konuma değiştirin.</span><span class="sxs-lookup"><span data-stu-id="da65a-184">On your development environment, download the project from [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), open a command-line, and change directories to the location that you downloaded the project.</span></span>

2. <span data-ttu-id="da65a-185">Gelen **hdınsight storm java kafka** dizin, projeyi derlemek ve dağıtım için bir paketi oluşturmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="da65a-185">From the **hdinsight-storm-java-kafka** directory, use the following command to compile the project and create a package for deployment:</span></span>

  ```bash
  mvn clean package
  ```

    <span data-ttu-id="da65a-186">Paket işlemi adlı bir dosya oluşturur `KafkaTopology-1.0-SNAPSHOT.jar` içinde `target` dizin.</span><span class="sxs-lookup"><span data-stu-id="da65a-186">The package process creates a file named `KafkaTopology-1.0-SNAPSHOT.jar` in the `target` directory.</span></span>

3. <span data-ttu-id="da65a-187">Hdınsight kümesi üzerinde storm'a paketi kopyalamak için aşağıdaki komutları kullanın.</span><span class="sxs-lookup"><span data-stu-id="da65a-187">Use the following commands to copy the package to your Storm on HDInsight cluster.</span></span> <span data-ttu-id="da65a-188">Değiştir **kullanıcıadı** küme için SSH kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="da65a-188">Replace **USERNAME** with the SSH user name for the cluster.</span></span> <span data-ttu-id="da65a-189">Değiştir **BASENAME** küme oluştururken kullandığınız temel ada sahip.</span><span class="sxs-lookup"><span data-stu-id="da65a-189">Replace **BASENAME** with the base name you used when creating the cluster.</span></span>

  ```bash
  scp ./target/KafkaTopology-1.0-SNAPSHOT.jar USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
  ```

    <span data-ttu-id="da65a-190">İstendiğinde, kümeler oluşturulurken kullanılan parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="da65a-190">When prompted, enter the password you used when creating the clusters.</span></span>

## <a name="configure-the-topology"></a><span data-ttu-id="da65a-191">Topolojisini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="da65a-191">Configure the topology</span></span>

1. <span data-ttu-id="da65a-192">Kafka Aracısı ana bilgisayarları bulmak için aşağıdaki yöntemlerden birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="da65a-192">Use one of the following methods to discover the Kafka broker hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
    $clusterName = Read-Host -Prompt "Enter the Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $brokerHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($brokerHosts -join ":9092,") + ":9092"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="da65a-193">Bash örnek varsayar `$CLUSTERNAME` Hdınsight kümesi adını içerir.</span><span class="sxs-lookup"><span data-stu-id="da65a-193">The Bash example assumes that `$CLUSTERNAME` contains the name of the HDInsight cluster.</span></span> <span data-ttu-id="da65a-194">Ayrıca varsayılmaktadır [jq](https://stedolan.github.io/jq/) yüklenir.</span><span class="sxs-lookup"><span data-stu-id="da65a-194">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="da65a-195">İstendiğinde, küme oturum açma hesabı için parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="da65a-195">When prompted, enter the password for the cluster login account.</span></span>

    <span data-ttu-id="da65a-196">Döndürülen değer aşağıdakine benzer:</span><span class="sxs-lookup"><span data-stu-id="da65a-196">The value returned is similar to the following text:</span></span>

        wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092

    > [!IMPORTANT]
    > <span data-ttu-id="da65a-197">Kümeniz için ikiden fazla Aracısı konakları olsa istemcilere tüm ana bilgisayarlar, tam bir listesi sağlanmaktadır gerekmez.</span><span class="sxs-lookup"><span data-stu-id="da65a-197">While there may be more than two broker hosts for your cluster, you do not need to provide a full list of all hosts to clients.</span></span> <span data-ttu-id="da65a-198">Bir veya iki yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="da65a-198">One or two is enough.</span></span>

2. <span data-ttu-id="da65a-199">Kafka Zookeeper ana bilgisayarları bulmak için aşağıdaki yöntemlerden birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="da65a-199">Use one of the following methods to discover the Kafka Zookeeper hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
    $clusterName = Read-Host -Prompt "Enter the Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $zookeeperHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($zookeeperHosts -join ":2181,") + ":2181"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="da65a-200">Bash örnek varsayar `$CLUSTERNAME` Hdınsight kümesi adını içerir.</span><span class="sxs-lookup"><span data-stu-id="da65a-200">The Bash example assumes that `$CLUSTERNAME` contains the name of the HDInsight cluster.</span></span> <span data-ttu-id="da65a-201">Ayrıca varsayılmaktadır [jq](https://stedolan.github.io/jq/) yüklenir.</span><span class="sxs-lookup"><span data-stu-id="da65a-201">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="da65a-202">İstendiğinde, küme oturum açma hesabı için parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="da65a-202">When prompted, enter the password for the cluster login account.</span></span>

    <span data-ttu-id="da65a-203">Döndürülen değer aşağıdakine benzer:</span><span class="sxs-lookup"><span data-stu-id="da65a-203">The value returned is similar to the following text:</span></span>

        zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181

    > [!IMPORTANT]
    > <span data-ttu-id="da65a-204">İkiden fazla Zookeeper düğümleri olsa da, tüm konaklar istemcileri için tam bir listesi sağlanmaktadır gerekmez.</span><span class="sxs-lookup"><span data-stu-id="da65a-204">While there are more than two Zookeeper nodes, you do not need to provide a full list of all hosts to clients.</span></span> <span data-ttu-id="da65a-205">Bir veya iki yeterlidir.</span><span class="sxs-lookup"><span data-stu-id="da65a-205">One or two is enough.</span></span>

    <span data-ttu-id="da65a-206">Bu değer daha sonra kullanılmak üzere kaydedin.</span><span class="sxs-lookup"><span data-stu-id="da65a-206">Save this value, as it is used later.</span></span>

3. <span data-ttu-id="da65a-207">Düzen `dev.properties` proje kökündeki dosyasında.</span><span class="sxs-lookup"><span data-stu-id="da65a-207">Edit the `dev.properties` file in the root of the project.</span></span> <span data-ttu-id="da65a-208">Bu dosyadaki eşleşen satır aracısı ve Zookeeper ana bilgisayar bilgilerini ekleyin.</span><span class="sxs-lookup"><span data-stu-id="da65a-208">Add the Broker and Zookeeper hosts information to the matching lines in this file.</span></span> <span data-ttu-id="da65a-209">Aşağıdaki örnek, önceki adımları örnek değerleri kullanarak yapılandırılır:</span><span class="sxs-lookup"><span data-stu-id="da65a-209">The following example is configured using the sample values from the previous steps:</span></span>

        kafka.zookeeper.hosts: zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181
        kafka.broker.hosts: wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092
        kafka.topic: stormtopic

4. <span data-ttu-id="da65a-210">Kaydet `dev.properties` dosya ve Storm kümesi karşıya yüklemek için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="da65a-210">Save the `dev.properties` file and then use the following command to upload it to the Storm cluster:</span></span>

     ```bash
    scp dev.properties USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
    ```

    <span data-ttu-id="da65a-211">Değiştir **kullanıcıadı** küme için SSH kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="da65a-211">Replace **USERNAME** with the SSH user name for the cluster.</span></span> <span data-ttu-id="da65a-212">Değiştir **BASENAME** küme oluştururken kullandığınız temel ada sahip.</span><span class="sxs-lookup"><span data-stu-id="da65a-212">Replace **BASENAME** with the base name you used when creating the cluster.</span></span>

## <a name="start-the-writer"></a><span data-ttu-id="da65a-213">Yazıcı Başlat</span><span class="sxs-lookup"><span data-stu-id="da65a-213">Start the writer</span></span>

1. <span data-ttu-id="da65a-214">SSH kullanarak Storm kümeye bağlanmak için aşağıdakileri kullanın.</span><span class="sxs-lookup"><span data-stu-id="da65a-214">Use the following to connect to the Storm cluster using SSH.</span></span> <span data-ttu-id="da65a-215">Değiştir **kullanıcıadı** küme oluşturulurken kullanılan SSH kullanıcı adı.</span><span class="sxs-lookup"><span data-stu-id="da65a-215">Replace **USERNAME** with the SSH user name used when creating the cluster.</span></span> <span data-ttu-id="da65a-216">Değiştir **BASENAME** küme oluşturulurken kullanılan taban adına sahip.</span><span class="sxs-lookup"><span data-stu-id="da65a-216">Replace **BASENAME** with the base name used when creating the cluster.</span></span>

  ```bash
  ssh USERNAME@storm-BASENAME-ssh.azurehdinsight.net
  ```

    <span data-ttu-id="da65a-217">İstendiğinde, kümeler oluşturulurken kullanılan parolayı girin.</span><span class="sxs-lookup"><span data-stu-id="da65a-217">When prompted, enter the password you used when creating the clusters.</span></span>
   
    <span data-ttu-id="da65a-218">Bilgi için bkz. [HDInsight ile SSH kullanma](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="da65a-218">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="da65a-219">SSH bağlantısı topolojisi tarafından kullanılan Kafka konu oluşturmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="da65a-219">From the SSH connection, use the following command to create the Kafka topic used by the topology:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic stormtopic --zookeeper $KAFKAZKHOSTS
    ```

    <span data-ttu-id="da65a-220">Değiştir `$KAFKAZKHOSTS` Zookeeper ile ana bilgisayar önceki bölümde alınan bilgileri.</span><span class="sxs-lookup"><span data-stu-id="da65a-220">Replace `$KAFKAZKHOSTS` with the Zookeeper host information you retrieved in the previous section.</span></span>

2. <span data-ttu-id="da65a-221">Storm kümesi için SSH bağlantısı yazan topoloji başlatmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="da65a-221">From the SSH connection to the Storm cluster, use the following command to start the writer topology:</span></span>

    ```bash
    storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
    ```

    <span data-ttu-id="da65a-222">Bu komutla birlikte kullanılan parametreler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="da65a-222">The parameters used with this command are:</span></span>

    * <span data-ttu-id="da65a-223">`org.apache.storm.flux.Flux`: Flux yapılandırmak ve bu topoloji çalıştırmak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="da65a-223">`org.apache.storm.flux.Flux`: Use Flux to configure and run this topology.</span></span>

    * <span data-ttu-id="da65a-224">`--remote`: Nimbus topolojiye gönderin.</span><span class="sxs-lookup"><span data-stu-id="da65a-224">`--remote`: Submit the topology to Nimbus.</span></span> <span data-ttu-id="da65a-225">Topoloji kümedeki çalışan düğümü dağıtılır.</span><span class="sxs-lookup"><span data-stu-id="da65a-225">The topology is distributed across the worker nodes in the cluster.</span></span>

    * <span data-ttu-id="da65a-226">`-R /writer.yaml`: Kullanın `writer.yaml` topolojisini yapılandırmak için dosya.</span><span class="sxs-lookup"><span data-stu-id="da65a-226">`-R /writer.yaml`: Use the `writer.yaml` file to configure the topology.</span></span> <span data-ttu-id="da65a-227">`-R`Bu kaynak jar dosyasına dahil olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="da65a-227">`-R` indicates that this resource is included in the jar file.</span></span> <span data-ttu-id="da65a-228">Bu nedenle jar kök dizininde olduğundan `/writer.yaml` yolu.</span><span class="sxs-lookup"><span data-stu-id="da65a-228">It's in the root of the jar, so `/writer.yaml` is the path to it.</span></span>

    * <span data-ttu-id="da65a-229">`--filter`: Girdileri doldurmak `writer.yaml` değerleri kullanarak topolojisi `dev.properties` dosya.</span><span class="sxs-lookup"><span data-stu-id="da65a-229">`--filter`: Populate entries in the `writer.yaml` topology using values in the `dev.properties` file.</span></span> <span data-ttu-id="da65a-230">Örneğin, değeri `kafka.topic` dosyasındaki giriş değiştirmek için kullanılan `${kafka.topic}` topoloji tanımı girişi.</span><span class="sxs-lookup"><span data-stu-id="da65a-230">For example, the value of the `kafka.topic` entry in the file is used to replace the `${kafka.topic}` entry in the topology definition.</span></span>

5. <span data-ttu-id="da65a-231">Topoloji başladıktan sonra bu veriler Kafka konuya yazıyor doğrulamak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="da65a-231">Once the topology has started, use the following command to verify that it is writing data to the Kafka topic:</span></span>

  ```bash
  /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $KAFKAZKHOSTS --from-beginning --topic stormtopic
  ```

    <span data-ttu-id="da65a-232">Değiştir `$KAFKAZKHOSTS` Zookeeper ile ana bilgisayar önceki bölümde alınan bilgileri.</span><span class="sxs-lookup"><span data-stu-id="da65a-232">Replace `$KAFKAZKHOSTS` with the Zookeeper host information you retrieved in the previous section.</span></span>

    <span data-ttu-id="da65a-233">Bu komut Kafka ile birlikte gelen bir komut dosyası konu izlemek için kullanır.</span><span class="sxs-lookup"><span data-stu-id="da65a-233">This command uses a script shipped with Kafka to monitor the topic.</span></span> <span data-ttu-id="da65a-234">Bir süre sonra konu ile yazılmış rastgele cümleleri döndürme başlamalısınız.</span><span class="sxs-lookup"><span data-stu-id="da65a-234">After a moment, it should start returning random sentences that have been written to the topic.</span></span> <span data-ttu-id="da65a-235">Çıktı aşağıdaki örneğe benzer:</span><span class="sxs-lookup"><span data-stu-id="da65a-235">The output is similar to the following example:</span></span>

        i am at two with nature             
        an apple a day keeps the doctor away
        snow white and the seven dwarfs     
        the cow jumped over the moon        
        an apple a day keeps the doctor away
        an apple a day keeps the doctor away
        the cow jumped over the moon        
        an apple a day keeps the doctor away
        an apple a day keeps the doctor away
        four score and seven years ago      
        snow white and the seven dwarfs     
        snow white and the seven dwarfs     
        i am at two with nature             
        an apple a day keeps the doctor away

    <span data-ttu-id="da65a-236">Komut dosyası durdurmak için CTRL + c'ı kullanın.</span><span class="sxs-lookup"><span data-stu-id="da65a-236">Use Ctrl+c to stop the script.</span></span>

## <a name="start-the-reader"></a><span data-ttu-id="da65a-237">Okuyucu Başlat</span><span class="sxs-lookup"><span data-stu-id="da65a-237">Start the reader</span></span>

1. <span data-ttu-id="da65a-238">Storm kümesi için SSH oturumundan okuyucu topoloji başlatmak için aşağıdaki komutu kullanın:</span><span class="sxs-lookup"><span data-stu-id="da65a-238">From the SSH session to the Storm cluster, use the following command to start the reader topology:</span></span>

  ```bash
  storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties
  ```

2. <span data-ttu-id="da65a-239">Topoloji başladıktan sonra Storm kullanıcı arabirimini açın.</span><span class="sxs-lookup"><span data-stu-id="da65a-239">Once the topology starts, open the Storm UI.</span></span> <span data-ttu-id="da65a-240">Bu web kullanıcı Arabirimi https://storm-BASENAME.azurehdinsight.net/stormui bulunur.</span><span class="sxs-lookup"><span data-stu-id="da65a-240">This web UI is located at https://storm-BASENAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="da65a-241">Değiştir __BASENAME__ küme oluştururken kullanılan taban adına sahip.</span><span class="sxs-lookup"><span data-stu-id="da65a-241">Replace __BASENAME__ with the base name used when the cluster was created.</span></span> 

    <span data-ttu-id="da65a-242">İstendiğinde, yönetici oturum açma adı kullanın (varsayılan, `admin`) ve küme oluştururken kullanılan parola.</span><span class="sxs-lookup"><span data-stu-id="da65a-242">When prompted, use the admin login name (default, `admin`) and password used when the cluster was created.</span></span> <span data-ttu-id="da65a-243">Aşağıdaki resme benzeyen bir web sayfasına bakın:</span><span class="sxs-lookup"><span data-stu-id="da65a-243">You see a web page similar to the following image:</span></span>

    ![Storm kullanıcı Arabirimi](./media/hdinsight-apache-storm-with-kafka/stormui.png)

3. <span data-ttu-id="da65a-245">Storm kullanıcı Arabirimi seçin __kafka okuyucu__ bağlamak __topoloji özeti__ hakkında bilgileri görüntülemek için bölüm __kafka okuyucu__ topolojisi.</span><span class="sxs-lookup"><span data-stu-id="da65a-245">From the Storm UI, select the __kafka-reader__ link in the __Topology Summary__ section to display information about the __kafka-reader__ topology.</span></span>

    ![Topoloji özeti kısmını Storm web kullanıcı Arabirimi](./media/hdinsight-apache-storm-with-kafka/topology-summary.png)

4. <span data-ttu-id="da65a-247">Günlükçü Cıvata bileşenin örnekleri hakkında bilgi görüntülemek için seçin __Günlükçü Cıvata__ bağlamak __Cıvatalar (her zaman)__ bölümü.</span><span class="sxs-lookup"><span data-stu-id="da65a-247">To display information about the instances of the logger-bolt component, select the __logger-bolt__ link in the __Bolts (All time)__ section.</span></span>

    ![Cıvatalar bölümündeki Günlükçü Cıvata bağlantıyı](./media/hdinsight-apache-storm-with-kafka/bolts.png)

5. <span data-ttu-id="da65a-249">İçinde __yürütücüler__ bölümünde, bir bağlantıyı seçin __bağlantı noktası__ bileşenin bu örneği günlük bilgilerini görüntülemek için sütun.</span><span class="sxs-lookup"><span data-stu-id="da65a-249">In the __Executors__ section, select a link in the __Port__ column to display logging information about this instance of the component.</span></span>

    ![Yürütücüler bağlantı](./media/hdinsight-apache-storm-with-kafka/executors.png)

    <span data-ttu-id="da65a-251">Günlük Kafka konusundan okunan veriler günlüğünü içerir.</span><span class="sxs-lookup"><span data-stu-id="da65a-251">The log contains a log of the data read from the Kafka topic.</span></span> <span data-ttu-id="da65a-252">Günlük bilgileri aşağıdakine benzer:</span><span class="sxs-lookup"><span data-stu-id="da65a-252">The information in the log is similar to the following text:</span></span>

        2016-11-04 17:47:14.907 c.m.e.LoggerBolt [INFO] Received data: four score and seven years ago
        2016-11-04 17:47:14.907 STDIO [INFO] the cow jumped over the moon
        2016-11-04 17:47:14.908 c.m.e.LoggerBolt [INFO] Received data: the cow jumped over the moon
        2016-11-04 17:47:14.911 STDIO [INFO] snow white and the seven dwarfs
        2016-11-04 17:47:14.911 c.m.e.LoggerBolt [INFO] Received data: snow white and the seven dwarfs
        2016-11-04 17:47:14.932 STDIO [INFO] snow white and the seven dwarfs
        2016-11-04 17:47:14.932 c.m.e.LoggerBolt [INFO] Received data: snow white and the seven dwarfs
        2016-11-04 17:47:14.969 STDIO [INFO] an apple a day keeps the doctor away
        2016-11-04 17:47:14.970 c.m.e.LoggerBolt [INFO] Received data: an apple a day keeps the doctor away

## <a name="stop-the-topologies"></a><span data-ttu-id="da65a-253">Topolojileri Durdur</span><span class="sxs-lookup"><span data-stu-id="da65a-253">Stop the topologies</span></span>

<span data-ttu-id="da65a-254">Storm kümesi için bir SSH oturumundan Storm topolojilerini durdurmak için aşağıdaki komutları kullanın:</span><span class="sxs-lookup"><span data-stu-id="da65a-254">From an SSH session to the Storm cluster, use the following commands to stop the Storm topologies:</span></span>

  ```bash
  storm kill kafka-writer
  storm kill kafka-reader
  ```

## <a name="delete-the-cluster"></a><span data-ttu-id="da65a-255">Küme silme</span><span class="sxs-lookup"><span data-stu-id="da65a-255">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="da65a-256">Bu belgede yer alan adımlar her iki kümeleri aynı Azure kaynak grubu oluşturmak için Azure portalında kaynak grubunu silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="da65a-256">Since the steps in this document create both clusters in the same Azure resource group, you can delete the resource group in the Azure portal.</span></span> <span data-ttu-id="da65a-257">Kaynak grubunun silinmesi, bu belgede aşağıdaki tarafından oluşturulan tüm kaynakları kaldırır.</span><span class="sxs-lookup"><span data-stu-id="da65a-257">Deleting the resource group removes all resources created by following this document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da65a-258">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="da65a-258">Next steps</span></span>

<span data-ttu-id="da65a-259">Hdınsight üzerinde Storm ile kullanılan daha fazla örnek Topolojileri için bkz: [örnek Storm topolojileri ve bileşenleri](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="da65a-259">For more example topologies that can be used with Storm on HDInsight, see [Example Storm topologies and components](hdinsight-storm-example-topology.md).</span></span>

<span data-ttu-id="da65a-260">Dağıtma ve Linux tabanlı Hdınsight üzerinde topolojileri izleme hakkında daha fazla bilgi için bkz: [dağıtma ve Linux tabanlı Hdınsight üzerinde Apache Storm topolojilerini yönetme](hdinsight-storm-deploy-monitor-topology-linux.md)</span><span class="sxs-lookup"><span data-stu-id="da65a-260">For information on deploying and monitoring topologies on Linux-based HDInsight, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>